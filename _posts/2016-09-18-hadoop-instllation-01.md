---
layout: post
title: Apache Hadoop Installation (Single Node)
subtitle: A Step by step tutorial
---

You can write regular [markdown](http://markdowntutorial.com/) here and Jekyll will automatically convert it to a nice webpage.  I strongly encourage you to [take 5 minutes to learn how to write in markdown](http://markdowntutorial.com/) - it'll teach you how to transform regular text into bold/italics/headings/tables/etc.

If you are new to Hadoop and getting curious that how to install Hadoop from scratch then this tutorial will help you to understand the setup process. By following these steps you can setup and run your single hadoop cluster. 


**Note:**
* Everyline with `$` is a linux command
* Every line starting with `#` represents comments or remarks
* During installation keep internet connection open

## 1. Updating linux distribution and getting Java

```
$ sudo apt-get install update
$ sudo apt-get install default-jdk
```

## 2. Creating a new user and usergroup (best practice)
you can create user and group with any name that is suitable to you. Here, we have created user with name `hduser` and group with the name `hadoop`

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
open `.bashrc` file in gedit to add content

```
$ sudo gedit ~/.bashrc
```

Now, add following content and save the file. In case if you are not using `java-8`, please replace `java-8-openjdk-amd64` with the name of java folder that you have installed.

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

## 6. Hadoop configuration

(i) - Edit File `core-site.xml` by using following command

```
$ sudo gedit core-site.xml
```
and add following content inside `<configuration>` ... `</configuration>` tags

```
<property>
<name>fs.default.name</name>
<value>hdfs://localhost:9000</value>
</property>
```

(ii) - Edit File `hdfs-site.xml` by using following command

```
$ sudo gedit hdfs-site.xml
```

and add following content inside `<configuration>` ...`</configuration>` tags.

The `hdfs-site.xml` is used to specify the namenode and datanode directories. Before modifying this file, we create the namenode and datanode directories. You can create folder with any name in our case we named it `hadoop_store`.

```
$ sudo mkdir -p /usr/local/hadoop_store/hdfs/namenode
$ sudo mkdir -p /usr/local/hadoop_store/hdfs/datanode

# grant access to hduser to the folder.
$ sudo chown -R hduser /usr/local/hadoop_store
```

```
<property>
    <name>dfs.replication</name>
    <value>4</value>
</property>
<property>
        <name>dfs.namenode.name.dir</name>
        <value> file:/usr/local/hadoop_store/hdfs/namenode </value>
</property>
<property>
        <name>dfs.datanode.data.dir</name>
        <value> file:/usr/local/hadoop_store/hdfs/datanode </value>
</property>
```
(iii) - Edit File `yarn-site.xml` by using following command

```
$ sudo gedit yarn-site.xml
```

and add following content inside `<configuration>` ...`</configuration>` tags.

```
# linux command to open the file to edit
$ sudo gedit yarn-site.xml
```

```
<property>
    <name>yarn.nodemanager.aux-services</name>
    <value>mapreduce_shuffle</value>
</property>
<property>
    <name>yarn.nodemanager.aux-services.mapreduce.shuffle.class</name>
    <value>org.apache.hadoop.mapred.ShuffleHandler</value>
</property>
```

(iv) - Edit File `mapred-site.xml` by using following command

```
$ sudo gedit mapred-site.xml
```

and add following content inside `<configuration>` ...`</configuration>` tags.

```
$ cp mapred-site.xml.template mapred-site.xml
$ sudo gedit mapred_site.xml
```

```
<property>
    <name>mapred.job.tracker</name>
    <value>localhost:9001</value>
</property>
<property>
    <name>mapreduce.framework.name</name>
    <value>yarn</value>
</property>
```

(v) - Edit file `hadoop-env.sh` and locate for the line `export JAVA_HOME=${JAVA_HOME}` and change it with right java home path like in our case it will be `export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64` 

## 7. Format the Hadoop file system

To format the file system run following command. This will initialize the hadoop file system.

```
$ hdfs namenode -format
```

## 8. Running 'Single Node' cluster

```
$ start-dfs.sh
$ start-yarn.sh
$ jps
```

## 9. See the status on Web Interface

* goto `http://localhost:8088` to see Main Cluster
* goto `http://localhost:50070` to see detailed status
* 
 
**External Useful Links:**

* Prof. Anand Nayyar's  [post](https://www.facebook.com/expertresearcher/posts/1630329467227609)
* Tutorial posted on HadoopWorld [Youtube Channel](https://www.youtube.com/watch?v=YY8QL25KCOg) 
* Book "Hadoop: The Definitive Guide"
* [Edureka Hadoop Installation Guide](http://www.edureka.co/app/webroot/img/source_code/gzw/module_1388139836.pdf)

