---
layout: post
title:  "Oracle notes"
categories: oracle notes
tags: oracle notes
author: 若水三千
---

* content
{:toc}


系统版本  ： CentOS6.9 
数据库版本： Oracle 11g

### **修改Oracle 服务端数据库字符集** ###


1.切换到oracle用户下

```shell
[root@localhost ~] su oracle
```

2.连接sqlplus

```shell
[oracle@localhost root]$ sqlplus /nolog

```

>    SQL*Plus: Release 11.2.0.4.0 Production on Wed Aug 1 15:28:12 2018
> 
>    Copyright (c) 1982, 2013, Oracle.  All rights reserved.


3.登录数据库

```shell
SQL> conn / as sysdba   
```

>    Connected.

4.关闭数据库实例

```shell
SQL> shutdown immediate;
```

>    SP2-0734: unknown command beginning "shudown im..." - rest of line ignored.
>    
>    Database closed.
>    Database dismounted.
>    ORACLE instance shut down.

5.以mount方式重启数据库

```shell
SQL> startup mount
```

>    ORACLE instance started.
>    
>    Total System Global Area 4960579584 bytes
>    Fixed Size		    2261728 bytes
>    Variable Size		  989859104 bytes
>    Database Buffers	 3959422976 bytes
>    Redo Buffers		    9035776 bytes
>    Database mounted.

6.修改session

```shell
SQL> alter system enable restricted session;                                   
```

>    System altered.

7.修改job

```shell
SQL> alter system set job_queue_processes=0;
```

>    System altered.

8.修改aq_tm_processes

```shell
SQL> alter system set aq_tm_processes=0;
```

>    System altered.

9.open database

```shell
SQL> alter database open; 
```

>    Database altered.

10.修改数据库字符集

```shell
SQL> alter database character set ZHS16GBK;
```

>    alter database character set ZHS16GBK
>    *
>    ERROR at line 1:
>    ORA-12712: new character set must be a superset of old character set

11.修改INTERNAL_USE字符集

```shell
SQL> ALTER DATABASE character set INTERNAL_USE ZHS16GBK;
```
>    Database altered.

12.查看字符集修改情况

```shell
SQL> select * from v$nls_parameters;
```

>```
>    PARAMETER                     VALUE   
>    -----------------------------------------------------------        
>    NLS_LANGUAGE                AMERICAN    
>    NLS_TERRITORY               AMERICA    
>    NLS_CURRENCY                $    
>    NLS_ISO_CURRENCY            AMERICA       
>    NLS_NUMERIC_CHARACTERS      .,    
>    NLS_CALENDAR                GREGORIAN    
>    NLS_DATE_FORMAT             DD-MON-RR    
>    NLS_DATE_LANGUAGE           AMERICAN    
>    NLS_CHARACTERSET            ZHS16GBK
>    NLS_SORT                    BINARY        
>    NLS_TIME_FORMAT             HH.MI.SSXFF AM        
>    NLS_TIMESTAMP_FORMAT        DD-MON-RR HH.MI.SSXFF AM    
>    NLS_TIME_TZ_FORMAT          HH.MI.SSXFF AM TZR    
>    NLS_TIMESTAMP_TZ_FORMAT     DD-MON-RR HH.MI.SSXFF AM TZR   
>    NLS_DUAL_CURRENCY           $    
>    NLS_NCHAR_CHARACTERSET      AL16UTF16    
>    NLS_COMP                    BINARY    
>    NLS_LENGTH_SEMANTICS        BYTE    
>    NLS_NCHAR_CONV_EXCP         FALSE    
>    
>    
>    19 rows selected.
>```

11.关闭数据库实例

```shell
SQL> shutdown immediate;
```

>    Database closed.
>    Database dismounted.
>    ORACLE instance shut down.

12.重启数据库实例

```shell
SQL> startup
```

>    ORACLE instance started.
>    
>    Total System Global Area 4960579584 bytes
>    Fixed Size		    2261728 bytes
>    Variable Size		  989859104 bytes
>    Database Buffers	 3959422976 bytes
>    Redo Buffers		    9035776 bytes
>    Database mounted.
>    Database opened.



### **oracle 开机自启动** ###
oracle 11g centos6.9

1.查看/etc/oratab是否存在，如果存在转2，不存在进行复制

```shell
cp -p /opt/app/oracle/product/11.2.0/dbhome_1/install/oratab /etc/

chmod 744 /etc/oratab
```

2.修改 /etc/oratab

tmsdb:/opt/app/oracle/product/11.2.0/dbhome_1:Y

3.编辑并保存oracle开机脚本oracle至/etc/init.d/或者/etc/rc.d/init.d

```shell

#!/bin/bash

# oracle: Start/Stop Oracle Database 11g R2
#
# chkconfig: 345 90 10
# description: The Oracle Database is an Object-Relational Database Management System.
#
# processname: oracle

. /etc/rc.d/init.d/functions

LOCKFILE=/var/lock/subsys/oracle
ORACLE_HOME=/opt/app/oracle/product/11.2.0/dbhome_1
ORACLE_USER=oracle

case "$1" in
'start')
   if [ -f $LOCKFILE ]; then
      echo $0 already running.
      exit 1
   fi
   echo -n $"Starting Oracle Database:"
   su - $ORACLE_USER -c "$ORACLE_HOME/bin/lsnrctl start"
   su - $ORACLE_USER -c "$ORACLE_HOME/bin/dbstart $ORACLE_HOME"
   su - $ORACLE_USER -c "$ORACLE_HOME/bin/emctl start dbconsole"
   touch $LOCKFILE
   ;;
'stop')
   if [ ! -f $LOCKFILE ]; then
      echo $0 already stopping.
      exit 1
   fi
   echo -n $"Stopping Oracle Database:"
   su - $ORACLE_USER -c "$ORACLE_HOME/bin/lsnrctl stop"
   su - $ORACLE_USER -c "$ORACLE_HOME/bin/dbshut"
   su - $ORACLE_USER -c "$ORACLE_HOME/bin/emctl stop dbconsole"
   rm -f $LOCKFILE
   ;;
'restart')
   $0 stop
   $0 start
   ;;
'status')
   if [ -f $LOCKFILE ]; then
      echo $0 started.
      else
      echo $0 stopped.
   fi
   ;;
*)
   echo "Usage: $0 [start|stop|status]"
   exit 1
esac

exit 0

```

4.使用chkconfig管理oracle开机启动

```shell
chkconfig oracle on
```
