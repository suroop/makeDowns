>������������Դ�롶��MySQL����˼���Ż�����һ�����ĵ�

IN�����Ż�
======
- IN����ֻ�ܽӳ���������಻����200��
- IN���治�ܽ��Ӳ�ѯ

```sql
select * from tb1 where tb1.id in (select id from tb2 where tb2.c1...)
// �Ż���
select tb1.* from tb1, (select id from tb2 where tb2.c1...)t where tb1.id = t.id;
```