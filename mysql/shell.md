



### shell mysql 查询，解析结果，更新

```shell
#!/bin/bash

MYSQL="mysql -h 127.0.0.1 -uroot -p123456"

query_sql="select concat(batch_number, '|', report_to, '|', email) from settlement_admin.payroll_email;"
eval "$MYSQL -s -e \"$query_sql\"" | while IFS= read -r ROW
do
    batch_number=$(echo $ROW | awk -F'|' '{print $1}')
    report_to=$(echo $ROW | awk -F'|' '{print $2}')
    email=$(echo $ROW | awk -F'|' '{print $3}')

    up_sql="update settlement_admin.payroll_salary_report_to set email='$email' where batch_number='$batch_number' and report_to='$report_to'"
    echo $up_sql

    eval "$MYSQL -s -e \"$up_sql\""
done

```



