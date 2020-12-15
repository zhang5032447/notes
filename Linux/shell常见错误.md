

#### 一、[: =: unary operator expected

```shell
# 脚本代码
read -p "是否发布服务到$host_txt?[y/N]" input
echo $input
if [ $input = "y" ]
then
	echo $input
fi

# 运行后错误提示
# ./fab.sh: line 138: [: =: unary operator expected

# 修改代码
read -p "是否发布服务到$host_txt?[y/N]" input
echo $input
if [[ $input = "y" ]]   # 修改此处
then
	echo $input
fi

# 错误原因
# $input 值为空
```

