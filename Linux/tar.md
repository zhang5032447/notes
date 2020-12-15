



```shell
tar -zcvf --exclude='.git' --exclude='.gitignore' -f vline_live.tar.gz ./*
sudo tar --exclude='logs' -zcvf /data/srv/vline/vline_live_202000.tar.gz /data/srv/vline/vline_live

sed -i "s/dev_test.yaml/test.yaml/g"  vline_live/src/main.py
```

