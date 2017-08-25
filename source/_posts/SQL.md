title: SQL
author: Kenny Tang
date: 2017-08-21 11:12:33
tags:
---
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