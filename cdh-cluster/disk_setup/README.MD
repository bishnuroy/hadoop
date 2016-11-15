
Reference links for changing the default HDFS datastore.

https://www.cloudera.com/documentation/enterprise/5-5-x/topics/admin_dn_storage_directories.html

http://blog.cloudera.com/blog/2015/05/new-in-cdh-5-4-how-swapping-of-hdfs-datanode-drives/

http://girishkathalagiri.blogspot.in/2012/09/adding-disk-to-hadoop-data-nodesrepeat.html

http://capnjosh.com/blog/adding-more-space-to-your-cloudera-hadoop-nodes/



#### First stop the CDH cluster.

```
# vgcreate hdfsvg /dev/vdc
# lvcreate -L 250G -n hdfslv hdfsvg
# mkfs.ext4 -m1 -O dir_index,extent,sparse_super /dev/hdfsvg/hdfslv
# mkdir /home/dfs
```
* For mounting edit the file /etc/fstab. Add this line:
```
/dev/hdfsvg/hdfslv    /home/dfs   ext4    defaults,noatime 1 2
```
* Then mount it and execute the rest of the commands.
```
# mount -a
# mkdir /home/dfs/nn
# chown -R hdfs:hadoop /home/dfs/nn
# chmod 0700 /home/dfs/nn
```
* Now copy the content of /dfs/nn to newly created /home/dfs/nn as hdfs user.
```
# su - hdfs
$ cp -r -p /dfs/nn/* /home/dfs/nn/
```
* On Secondary Namenode the default Namenode data directory is /dfs/snn. We are going to change it to the newly attached 256GB disk.
```
# vgcreate hdfsvg /dev/vdc
# lvcreate -L 250G -n hdfslv hdfsvg
# mkfs.ext4 -m1 -O dir_index,extent,sparse_super /dev/hdfsvg/hdfslv
# mkdir /home/dfs
```
* For mounting edit the file /etc/fstab. Add this line:
```
/dev/hdfsvg/hdfslv    /home/dfs   ext4    defaults,noatime 1 2
```
* Then mount it and execute the rest of the commands.
```
# mount -a
# mkdir /home/dfs/snn
# chown -R hdfs:hadoop /home/dfs/snn
# chmod 0700 /home/dfs/snn
```
* Now copy the content of /dfs/snn to newly created /home/dfs/snn as hdfs user.
```
# su - hdfs
$ cp -r -p /dfs/snn/* /home/dfs/snn/
```

* On Datanodes the default Datanode data directory is /dfs/dn. We are going to change it to the newly attached 2TB disk.
```
# vgcreate hdfsvg /dev/vdc
# lvcreate -L 2000G -n hdfslv hdfsvg
# mkfs.ext4 -m1 -O dir_index,extent,sparse_super /dev/hdfsvg/hdfslv
# mkdir /home/dfs
```
* For mounting edit the file /etc/fstab. Add this line:
```
/dev/hdfsvg/hdfslv    /home/dfs   ext4    defaults,noatime 1 2
```
* Then mount it and execute the rest of the commands.
```
# mount -a
# mkdir /home/dfs/dn
# chown -R hdfs:hadoop /home/dfs/dn

```
* Now copy the content of /dfs/dn to newly created /home/dfs/dn as hdfs user.
```
# su - hdfs
$ cp -r -p /dfs/dn/* /home/dfs/dn/
```
#### Please note that for datanodes we don't have to change directory permission to 0700. The default permission 0755 applies.

* Once all the hdfs instances are done go to cloudera UI.

##### 1. Go to the HDFS service.
##### 2. Click the Configuration tab.
##### 3. Select Scope > NameNode.
##### 4. Remove the current directory (dfs/nn) and add new one (/home/dfs/nn) to the NameNode Data Directory property.
##### 5. Click Save Changes to commit the changes.

* Repeat the above 5 steps for scopes SecondaryNameNode and Datanode.
* Once done restart the CDH cluster.
