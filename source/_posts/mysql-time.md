---
title: mysql_time
date: 2017-05-17 21:11:35
tags:
categories:
---
DATETIME

create table user(id int auto_increment primary key, username char(50), password char(50));

create table picture(id int auto_increment primary key, uid int, content text, filename char(50), size int, type char(50), filepic text, mtime DATETIME, foreign key(uid) references user(id));


create table comment(id int auto_increment, pid int, uid int, content text, mtime DATETIME, primary key(id, pid), foreign key(pid) references picture(id), foreign key(uid) references user(id));

create table likes(uid int, pid int, t_like boolean, mtime DATETIME, primary key(uid, pid), foreign key(uid) references user(id), foreign key(pid) references picture(id));
