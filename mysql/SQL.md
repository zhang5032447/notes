

### 关联表查询更新

```sql
update cm_waterfall_hour as t1 
join cm_waterfall_data as t2 on (t1.placement_id=t2.placement_id and t1.ymd = t2.ymd)
set t1.pkg_name = t2.pkg_name

```



ant-table-body-inner

padding-bottom: 15px;

ant-table-body