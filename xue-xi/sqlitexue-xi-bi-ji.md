- 不存在记录则插入数据：`insert into deviceentry (customerId,allNumber) select 'c','d' where not exists (select * from deviceentry); `
   