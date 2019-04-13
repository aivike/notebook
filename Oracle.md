#Oracle运维
查看Oracle数据库占用CPU高的
根据pid查询oracle执行语句，可以检查那个oracle进程占用资源多
SELECT S.SID,S.SERIAL#, P.SPID, S.STATUS, S.USERNAME,
   S.MACHINE||'('||OSUSER||')' MACHINE,
 S.PROGRAM, SQL_TEXT
    FROM V$SESSION S, V$PROCESS P, SYS.V_$SQL A
    WHERE A.ADDRESS = S.SQL_ADDRESS
           AND A.HASH_VALUE=S.SQL_HASH_VALUE
           AND S.PADDR=P.ADDR
           AND P.SPID=10476   --unix 下的#PID
