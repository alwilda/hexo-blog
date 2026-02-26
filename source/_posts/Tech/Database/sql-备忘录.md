---
title: SQL 备忘录
tags:
  - SQL
  - Oracle
abbrlink: 4e3f03c2
date: 2023-11-02 18:17:58
categories:
---

# Oracle

## 查询版本

```sql
SELECT *
FROM V$VERSION;
```

<!--more-->

## 创建用户、赋权
<!--more-->

```sql
-- 取消 C## 开头的限制
ALTER SESSION SET "_ORACLE_SCRIPT"= TRUE;

-- 用户名/密码
CREATE USER tom IDENTIFIED BY 123456;

-- 赋予连接权限 
-- CONNECT: 连接数据库、建表…… RESOURCE: 建触发器、过程……
GRANT CONNECT, RESOURCE TO tom;

-- 授予对表空间 'USERS' 的权限。
ALTER USER tom QUOTA UNLIMITED ON USERS;
```

## 将当前用户的表权限赋予另一个用户

```sql
GRANT SELECT, INSERT, UPDATE, DELETE ON Schema.TableNmae TO AnotherSchema;

-- Sequence 等同理
GRANT SELECT ON Schema.SEQ_XXX TO AnotherSchema;
```

### 批量赋权：

```plsql
BEGIN
  FOR UT IN (SELECT TABLE_NAME FROM USER_TABLES)
    LOOP
      -- DBMS_OUTPUT.PUT_LINE(UT.TABLE_NAME);
      EXECUTE IMMEDIATE 'GRANT SELECT, INSERT, UPDATE, DELETE ON ' || UT.TABLE_NAME || ' TO AnotherSchema';
    END LOOP;
END;
```

## 建表

```sql
CREATE TABLE STUDENT
(
    -- 主键，指定名称，自增序列（版本 12c+）
    ID          NUMBER GENERATED AS IDENTITY CONSTRAINT PK_STD_ID PRIMARY KEY,
    STUDENT_ID  VARCHAR2(32),
    -- Check，指定名称
    GENDER      CHAR(1) CONSTRAINT CK_GENDER CHECK ( GENDER IS NULL OR GENDER = 'M' OR GENDER = 'F'),
    -- 外键，指定名称
    ONE_FK      NUMBER  CONSTRAINT FK_ONE_FK REFERENCES AnotherTable(ID) NOT NULL,
    CREATE_TIME DATE DEFAULT SYSDATE
);

-- 唯一索引，指定名称
CREATE UNIQUE INDEX UK_STUDENT_ID ON STUDENT (STUDENT_ID);

-- 表/字段注释
COMMENT ON TABLE STUDENT IS '学生表';
COMMENT ON COLUMN STUDENT.STUDENT_ID IS '学号';
```

## RECORD 与 VARRAY 的用法

```plsql
BEGIN
    DECLARE
        -- 定义 record 类型
        TYPE RECORD_TYPE IS RECORD
                          (
                              FIELD_1    NUMBER(10),
                              -- 引用某个表的字段类型
                              FIELD_2    SYS.XXX.ID%TYPE,
                              FIELD_3    SYS.XXX.NAME%TYPE
                          );

        -- 定义数组类型
        TYPE VARRAY_TYPE IS VARRAY(1000) OF RECORD_TYPE;

        -- 定义一个变量为 record
        V_RT        RECORD_TYPE;
        -- 定义一个变量为数组
        V_ARR VARRAY_TYPE := VARRAY_TYPE();
    BEGIN
        FOR REC IN (SELECT ROWNUM, A, B, C,
                    FROM XXX)
            LOOP
                -- 向数组内添加元素
                V_ARR.EXTEND; -- 在数组末尾添加一个元素
                V_ARR(REC.ROWNUM).FIELD_1 := REC.A;
                V_ARR(REC.ROWNUM).FIELD_2 := REC.B;
                V_ARR(REC.ROWNUM).FIELD_3 := REC.C;
            END LOOP;

        -- 遍历数组
        FOR V_INDEX IN V_ARR.FIRST .. V_ARR.LAST
            LOOP
                V_RT := V_ARR(V_INDEX);
                DBMS_OUTPUT.PUT_LINE(V_RT.FIELD_1);
            END LOOP;
    END;
END;
```