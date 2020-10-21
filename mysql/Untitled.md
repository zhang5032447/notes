#### 只有后模糊查询才能使用索引`like 'cc%'`

#### 关系型数据库索引使用的是`B+树`或者`B树`数据结构

https://cloud.tencent.com/developer/article/1536233



```mermaid

```



B树：相对于平衡二叉树，每个节点存储了更多的键值可数据，并且每个节点拥有更多的子节点，这样B树的阶数比平衡二叉树阶数少，减少IO次数

B+树：对B树进一步优化，非叶子节点不存储数据，仅存储键值，这样磁盘中每个数据页可以存储更多的键值，进一步减少阶数，减少IO次数。B+树叶子节点之间通过双向链表连接，并且按照顺序排列，可以使范围查找，排序查找，分组查找以及去重查找变得简单高效。

Mysql的innodb中B+树2中实现方式

1. 聚集索引：用于主键

2. 非聚集索引：用户非主键，叶子节点不存储数据，而是存储主键，再通过主键查找数据，这个过程被称为`回表`

   





/data/presto/presto-cli --server namenode01:7080 --catalog hive --schema dataetl --execute "select * from rpt_ind limit 10" --output-format CSV_HEADER > /data/sa12/abc.csv



./presto-cli --server 18.139.247.152:8080 --catalog hive --schema ta --execute "" output-format CSV_HEADER > abc.csv



SELECT "#event_time", "#distinct_id", imei, "#ip", "#manufacturer", "device_brand", "#device_model",
	"#country_code"，
    "#city", language
    FROM ta_event_4.event_launch_package
    WHERE "#country_code" IN ('US','IQ','SY','TR','AF','PK','LB','JO','SA','YE','OM','AE','QA','EQ','IR','KZ','UZ','TM','KG','TJ','BD','ID','MY','KW','PS','DZ','TH','VN','MM','LA','MN','RU','SD','SS','LY','TN','SO','NE','NG','AL','AZ','CN','TW')
        limit 10



```
SELECT "#event_time", "#distinct_id", imei, "#ip", "#manufacturer", "device_brand", "#device_model",
    case "#country_code"
    when 'US' then 'United States'
        when 'IQ' then 'Iraq'
        when 'SY' then 'Syria'
        when 'TR' then 'Turkey'
        when 'AF' then 'Afghanistan'
        when 'PK' then 'Pakistan'
        when 'LB' then 'Lebanon'
        when 'JO' then 'Jordan'
        when 'SA' then 'Saudi Arabia'
        when 'YE' then 'Yemen'
        when 'OM' then 'Oman'
        when 'AE' then 'United Arab Emirates'
        when 'QA' then 'Qatar'
        when 'EQ' then 'Egypt'
        when 'IR' then 'Iran'
        when 'KZ' then 'Kazakhstan'
        when 'UZ' then 'Uzbekistan'
        when 'TM' then 'Turkmenistan'
        when 'KG' then 'Kyrgyzstan'
        when 'TJ' then 'Tajikistan'
        when 'BD' then 'Bangladesh'
        when 'ID' then 'Indonesia'
        when 'MY' then 'Malaysia'
        when 'KW' then 'Kuwait'
        when 'PS' then 'Palestine'
        when 'DZ' then 'Algeria'
        when 'TH' then 'Thailand'
        when 'VN' then 'Vietnam'
        when 'MM' then 'Myanmar'
        when 'LA' then 'Laos'
        when 'MN' then 'Mongolia'
        when 'RU' then 'Russia'
        when 'SD' then 'Sudan'
        when 'SS' then 'South Sudan'
        when 'LY' then 'Libya'
        when 'TN' then 'Tunisia'
        when 'SO' then 'Somalia'
        when 'NE' then 'Niger'
        when 'NG' then 'Nigeria'
        when 'AL' then 'Albania'
        when 'AZ' then 'Azerbaijan'
        when 'CN' then 'China'
        when 'TW' then 'Taiwan'
         else '' end ,
    "#city", language, '', ''
    FROM hive.ta.v_event_4
    WHERE "$part_event"='event_launch_package' and "$part_date">='2020-08-01' and "$part_date"<='2020-08-31'
        AND "#country_code" IN ('US','IQ','SY','TR','AF','PK','LB','JO','SA','YE','OM','AE','QA','EQ','IR','KZ','UZ','TM','KG','TJ','BD','ID','MY','KW','PS','DZ','TH','VN','MM','LA','MN','RU','SD','SS','LY','TN','SO','NE','NG','AL','AZ','CN','TW')
        limit 10
```



```sql
SELECT
  "#event_time"
, "#distinct_id"
, imei
, "#ip"
, "#manufacturer"
, "device_brand"
, "#device_model"
FROM
  hive.ta.v_event_4
WHERE ((((("$part_event" = 'event_launch_package') AND ("$part_date" >= '2020-08-01')) AND ("$part_date" <= '2020-08-31')) AND ("#distinct_id" IN ('77b459ea32c3a9f0', 'c45b1f38a99690d3'))) AND (NOT ("#country_code" IN ('AF', 'PK'))))

```



