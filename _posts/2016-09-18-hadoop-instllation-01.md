---
layout: post
title: Apache Hadoop Installation
subtitle: A Step by step tutorial
---

You can write regular [markdown](http://markdowntutorial.com/) here and Jekyll will automatically convert it to a nice webpage.  I strongly encourage you to [take 5 minutes to learn how to write in markdown](http://markdowntutorial.com/) - it'll teach you how to transform regular text into bold/italics/headings/tables/etc.

**Installing Hadoop is not much difficult if you properly focus and follow steps**.

**Note:**
* Everyline with '$' is a linux command
* Every line starting with '#' represents comments or remarks
* During installation keep internet connection open

## 1. Updating linux distribution and getting Java

```
$ sudo apt-get install update
$ sudo apt-get install default-jdk
```

## 2. Creating a new user and usergroup (best practice)
you can create user and group with any name that is suitable to you. Here, we have created user with name ***hduser*** and group with the name ***hadoop***
```
$ sudo addgroup hadoop
$ sudo adduser --ingroup hadoop hduser
$ sudo adduser hduser sudo
```

## 3. Getting ssh server and public key
```
# get open ssh server
$ sudo apt-get install openssh-server

$ su hduser
$ ssh-keygen -t rsa -P ""
$ cat $HOME/.ssh/id_rsa.pub >> $HOME/.ssh/authorized_keys

# testing ssh installation
$ ssh localhost
```

## 4. Getting and installing Hadoop

```
$ wget http://www-eu.apache.org/dist/hadoop/common/stable/hadoop-2.7.3.tar.gz
$ tar xvzf hadoop-2.7.3.tar.gz
$ sudo mv hadoop-2.7.3 /usr/local/hadoop

$ sudo chown -R hduser /usr/local
```
## 5. Setting environment
open .bashrc file in gedit to add content
```
$ sudo gedit ~/.bashrc
```
add following content and save the file. Please write the name of java folder that you are using.
```
# Java Configuration
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64

# Hadoop Configurations

export HADOOP_HOME=/usr/local/hadoop
export PATH=$PATH:$HADOOP_HOME/bin
export PATH=$PATH:$HADOOP_HOME/sbin
export HADOOP_MAPRED_HOME=$HADOOP_HOME
export HADOOP_COMMON_HOME=$HADOOP_HOME
export HADOOP_HDFS_HOME=$HADOOP_HOME
export HADOOP_YARN_HOME=$HADOOP_HOME
export HADOOP_COMMIN_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native"
```

