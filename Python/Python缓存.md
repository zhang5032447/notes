# Python 缓存

```python
import queue
import time
import threading


class Cache:
    def __init__(self, name):
        self.queue = queue.Queue()
        self.data = {}
        self.heap = []
        self.active = True
        self.name = name

        m = threading.Thread(target=cache_loop, args=(self,), name=name)
        m.setDaemon(True)
        m.start()

    def set_data(self, k, v, ex=60):
        ex_time = int(time.time()) + ex
        item = {
            'v': v,
            'k': k,
            'ex': ex_time
        }
        self.data[k] = item
        self.queue.put(item)

    def get_data(self, k):
        data = self.data.get(k)
        if data:
            if data['ex'] > int(time.time()):
                return data['v']
            else:
                self.queue.put(1)
        return None

    def del_data(self, k):
        try:
            del self.data[k]
        except Exception as exc:
            pass

    def clear_ex_data(self):
        ex_time = int(time.time())
        while self.heap:
            if self.heap[0]['ex'] > ex_time:
                break
            item = self.heappop()
            if item['ex'] > ex_time:
                self.heappush(item)
                break
            self.del_data(item['k'])

    def heappush(self, item):
        self.heap.append(item)
        self._siftdown(0, len(self.heap) - 1)

    def heappop(self):
        lastelt = self.heap.pop()
        if self.heap:
            returnitem = self.heap[0]
            self.heap[0] = lastelt
            self._siftup(0)
            return returnitem
        return lastelt

    def _siftup(self, pos):
        endpos = len(self.heap)
        startpos = pos
        newitem = self.heap[pos]
        childpos = 2 * pos + 1
        while childpos < endpos:
            rightpos = childpos + 1
            if rightpos < endpos and not self.heap[childpos]['ex'] < self.heap[rightpos]['ex']:
                childpos = rightpos
            self.heap[pos] = self.heap[childpos]
            pos = childpos
            childpos = 2 * pos + 1
        self.heap[pos] = newitem
        self._siftdown(startpos, pos)

    def _siftdown(self, startpos, pos):
        newitem = self.heap[pos]
        while pos > startpos:
            parentpos = (pos - 1) >> 1
            parent = self.heap[parentpos]
            if newitem['ex'] < parent['ex']:
                self.heap[pos] = parent
                pos = parentpos
                continue
            break
        self.heap[pos] = newitem

    def destroy(self):
        # TODO
        self.queue.put(0)
        self.active = False

    def is_active(self):
        return self.active


def cache_loop(cache: Cache):
    while True:
        task = cache.queue.get(block=True)
        if type(task) is dict:
            cache.heappush(task)
            cache.data[task['k']] = task
        if task == 0:
            # TODO
            break
        cache.clear_ex_data()


cache = Cache('')


```

