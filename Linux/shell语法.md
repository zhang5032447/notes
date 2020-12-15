### 循环

1. for ... in

```shell
#!/bin/bash
hosts=("127.0.0.1" "localhost")
for host in ${hosts[*]};do
    echo $host
done
```

2. while

```shell
#!/bin/bash
int=1
while(( $int<=5 ))
do
    echo $int
    let "int++"
done
```

