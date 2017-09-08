title: SQL
author: Kenny Tang
tags:
  - SQL
  - Oracle
  - DELETE
date: 2017-08-21 11:12:33
---
在日常的开发生活中，经常遇到需要批量进行删除操作的情况，对于一些删除量特别大的情况下，我们往往需要分段进行数据的删除，避免一次性的事务提交对数据库造成过高的负载。
<!-- more -->
```
declare 
ts varchar2 (1000) := 'boss.customer_sale_day,boss_sale.customer_sale_month' ;
v_sql varchar2(2000) ;
v_cnt number  ;
begin 
 -- 删除历史数据
 for t in ( select regexp_substr(ts,'[^,]+', 1, level) name from dual
            connect by regexp_substr(ts, '[^,]+', 1, level) is not null) loop
    v_cnt := 1 ;
    while v_cnt > 0 loop
    execute immediate 'delete from ' || t.name || ' where 1=1 and rownum < 50000';
    v_cnt := sql%rowcount ;
    commit ;
  end loop ;
 end loop ;
end ;
```