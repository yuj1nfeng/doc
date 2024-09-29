**安装
```bash
docker run --detach \
--name ora \
--restart always \
--publish 1521:1521 \
--publish 1522:1522 \
container-registry.oracle.com/database/free:latest
```

**设置密码 账号sys
```bash
docker exec -it ora ./setPassword.sh 123456
```

**创建表空间
```sql
create tablespace exam datafile "test.dbf" size 2G autoextend on next 32m maxsize unlimited extent management local segment space management auto;
```

**创建用户
```sql
create user c##exam identified by 123456;
```

**设置用户默认表空间
```sql
alter user c##exam default tablespace exam;
```

**授权
```sql
grant connect,resource TO c##exam;
```