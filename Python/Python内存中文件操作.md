# Python  内存中文件操作

```python
import io
import csv
import zipfile


def generate_csv(th_list, data_list):
    sio = io.StringIO()
    writer = csv.writer(sio)
    writer.writerow(th_list)
    writer.writerows(data_list)
    sio.seek(0)
    csv_data = sio.read()
    return csv_data


def generate_zip(files):
    mem_zip = io.BytesIO()

    with zipfile.ZipFile(mem_zip, mode="w", compression=zipfile.ZIP_DEFLATED) as zf:
        for f in files:
            zf.writestr(f[0], f[1])

    return mem_zip.getvalue()
```

