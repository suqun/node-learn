# mongodb 备份 还原 导出 导入

mongodb数据备份和还原主要分为二种，一种是`针对于库的mongodump和mongorestore`，一种是`针对库中表的mongoexport和mongoimport`。

##mongodump备份数据库

1. 常用命令格式

  ```
  mongodump -h IP --port 端口 -u 用户名 -p 密码 -d 数据库 -o 文件存在路径
  ```
  
  如果没有用户谁，可以去掉`-u`和`-p`
  
  如果导出本机的数据库，可以去掉`-h`
  
  如果是默认端口，可以去掉`--port`
  
  如果想导出所有数据库，可以去掉`-d`

2. 导出所有数据库

  ```
  mongodump -h 127.0.0.1 -o /home/larry/mongodb/
  ```

3. 导出指定数据库
 
  ```
  mongodump -h 192.168.1.100 -d test -o /home/larry/mongodb/
  ```

##mongorestore还原数据库

 1. 常用命令格式
 
  ```
  mongorestore -h IP --port 端口 -u 用户名 -p 密码 -d 数据库 --drop 文件存在路径
  ```
     
    `--drop`的意思是，先删除所有的记录，然后恢复。

 2. 恢复所有数据库到mongodb中
    
    ```
    mongorestore /home/larry/mongodb/
    ```

    这里的路径是所有库的备份路径

 3. 还原指定的数据库
  
    ```
    mongorestore -d test /home/larry/mongodb/test/
    ```test这个数据库的备份路径

    ```
    mongorestore -d test_new  /home/larry/mongodb/test/
    ```将test还原到test_new数据库中
    
    这二个命令，可以实现数据库的备份与还原，文件格式是json和bson的。无法指写到表备份或者还原。
    
##mongoexport导出表，或者表中部分字段

  1. 常用命令格式
  
    ```
    mongoexport -h IP --port 端口 -u 用户名 -p 密码 -d 数据库 -c 表名 -f 字段 -q 条件导出 --csv -o 文件名
    ```

    上面的参数好理解，重点说一下：
    
    `-f`    导出指字段，以字号分割，`-f name,email,age`导出name,email,age这三个字段
    
    `-q`    可以根查询条件导出，`-q '{ "uid" : "100" }'` 导出uid为100的数据
    
    `--csv` 表示导出的文件格式为csv的，这个比较有用，因为大部分的关系型数据库都是支持csv，在这里有共同点
    
  2. 导出整张表
  
    ```
    mongoexport -d test -c users -o /home/larry/mongodb/test/users.dat
    ```
    
  3. 导出表中部分字段
   
    ```
    mongoexport -d test -c users --csv -f uid,name,sex -o test/users.csv
    ```
  
  4. 根据条件取出数据
  
    ```
    mongoexport -d test -c users -q '{uid:{$gt:1}}' -o test/users.json
    ```

##mongoimport导入表，或者表中部分字段

  1. 常用命令格式
     
    * 还原整表导出的非csv文件
  
    ```
    mongoimport -h IP --port 端口 -u 用户名 -p 密码 -d 数据库 -c 表名 --upsert --drop 文件名
    ```
     
    **重点说一下--upsert，其他参数上面的命令已有提到，--upsert 插入或者更新现有数据**

    * 还原部分字段的导出文件
    
    ```
    mongoimport -h IP --port 端口 -u 用户名 -p 密码 -d 数据库 -c 表名 --upsertFields 字段 --drop 文件名
    ```
    
    **--upsertFields和--upsert一样**

    * 还原导出的csv文件
    
    ```
    mongoimport -h IP --port 端口 -u 用户名 -p 密码 -d 数据库 -c 表名 --type 类型 --headerline --upsert --drop 文件名
    ```
     
    **上面三种情况，还可以有其他排列组合的**
  
  2. 还原导出的表数据
  
    ```
    mongoimport -d test -c users --upsert test/users.dat
    ```

  3. 部分字段的表数据导入
  
    ```
    mongoimport -d test -c users  --upsertFields uid,name,sex  test/users.dat
    ```

  4. 还原csv文件
  
    ```
    mongoimport -d test -c users --type csv --headerline --file test/users.csv
    ```



[参考`海底苍鹰-mongodb备份/还原/导出/导入`](http://blog.51yip.com/nosql/1573.html)
