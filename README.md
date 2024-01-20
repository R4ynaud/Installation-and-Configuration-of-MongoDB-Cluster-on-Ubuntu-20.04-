# Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04 & 22.04


Guide to MongoDB Installation & Configuration On Ubuntu 22.04 & 22.04


![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/cf7c4705-79e1-4dc5-80f2-0ee403accafe)


### What Is an MongoDB ?

MongoDB is a NoSQL (Non-SQL) database management system. It stores data in a document-oriented structure and uses BSON format, which is similar to JSON. MongoDB's flexible schema allows for dynamic changes to data models. This feature provides the advantage of quickly adapting to changes in application requirements. MongoDB's distributed database features enable it to effectively operate on large and scalable datasets.

Key features of MongoDB include:

• Document-oriented data model. 

• Flexible schema structure.

• JSON-like BSON format. 

• High-performance query processing.

• Automatic parallelization and support for distributed databases.

### MongoDB Nedir ? Ne İşe Yarar ?

MongoDB, NoSQL (Non-SQL) veritabanı yönetim sistemlerinden biridir. Verileri doküman tabanlı bir yapıda depolar ve JSON benzeri BSON formatını kullanır. MongoDB'nin esnek şema yapısı, veri modellerini dinamik olarak değiştirmenize olanak tanır. Bu özellik, uygulama gereksinimlerindeki değişikliklere hızlı bir şekilde uyum sağlama avantajı sunar. MongoDB'nin dağıtık veritabanı özellikleri, büyük ve ölçeklenebilir veri setleri üzerinde etkili bir şekilde çalışabilmesini sağlar.

MongoDB'nin temel özellikleri şunlardır:

• Doküman tabanlı veri modeli.

• Esnek şema yapısı.

• JSON benzeri BSON formatı.

• Yüksek performanslı sorgu işleme.

• Otomatik paralelizasyon ve dağıtık veritabanı desteği.

## Before installing, Lets update and upgrade System Packages.


## Kurulumdan önce Sistem Paketlerini güncelleyelim.


```
apt-get update
```

```
apt-get upgrade
```



## You need to update with the IP address and host name of the main machine.


## Ana makinenin IP adresi ve ana bilgisayar adı ile güncelleme yapmamız gerekiyor.


```
vim etc/hosts
```

```
192.168.152.156	mongo-master-node

192.168.152.157 mongo-node-1

192.168.152.158	mongo-node-2
```

```
:wq!
```

![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/542763e8-3868-4e8e-a383-3498a3e71977)

```
cat etc/hosts
```

![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/5232bf5d-a0a5-4f01-acee-5d58f0dac047)


## Install wget and unzip package.


## Wget'i yükleyin ve paketi çıkartın.


```
apt-get install wget unzip -y
```

![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/822b4a78-ab38-4421-a296-839c71501c7f)


## Before installing, Lets update and upgrade System Packages.


## Kurulumdan önce Sistem Paketlerini güncelleyelim.


```
apt-get update
```

```
apt-get upgrade
```


## Once the system is up to date,  install the following essential packages.


## Sistem güncellendikten sonra aşağıdaki temel paketleri yükleyin. 


```
apt install software-properties-common gnupg apt-transport-https ca-certificates -y
```

![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/1211742f-cd8a-47e1-9e61-25351b534000)


## Begin by adding the  MongoDB GPG key.

## MongoDB GPG anahtarını ekleyerek başlayın.

```
wget -qO - https://www.mongodb.org/static/pgp/server-5.0.asc | sudo apt-key add -
```

![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/dcc69a7a-2511-4c30-8d23-d47a2b55b2c0)


## Later, add the MongoDB 5.0 repository to the /etc/apt/sources.list.d directory.

## Daha sonra MongoDB 5.0 deposunu /etc/apt/sources.list.d dizinine ekleyin.


```
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-5.0.list
```


![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/76b556f1-147a-4885-b14d-08f82ed4df46)


## Before installing, Lets update and upgrade System Packages.


## Kurulumdan önce Sistem Paketlerini güncelleyelim.


```
apt-get update
```

```
apt-get upgrade
```


## Now, run the following command to install the MongoDB database. 

## Şimdi MongoDB veritabanını kurmak için aşağıdaki komutu çalıştırın.


```
apt install mongodb-org -y
```

```
mongod --version
```

![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/928d2932-6739-4420-b038-bc2598bbd868)


## We need to run the following commands to activate MongoDB database services.

## MongoDB veritabanı servislerini aktif etmek için aşağıdaki komutları çalıştırmamız gerekiyor. 

```
systemctl start mongod
```
```
systemctl enable mongod
```
```
systemctl status mongod
```

![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/180e71f4-8418-4cd3-a9f3-c96ee8d99a1d)



## Run the following command to access MongoDB.

## MongoDB'e erişmek için aşağıdaki komutu çalıştırın.


```
mongosh
```

![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/8aef6049-6d0a-4e03-a3b6-f95e0b457e77)


## Execute the following query to switch to the admin user.

## Admin kullanıcısına geçmek için aşağıdaki sorguyu çalıştırın. 


```
use admin
```

## To create a new admin user, execute the following query, and 'passwordPrompt()' will prompt you to enter the administrator password.

## Yeni bir Admin kullanıcısı oluşturmak için aşağıdaki sorguyu çalıştırın, 'passwordPrompt()' sizden yönetici şifresini girmenizi isteyecektir. 


```
db.createUser(
  {
    user: "admin-user",
    pwd: passwordPrompt(),
    roles: [ { role: "root", db: "admin" }, "readWriteAnyDatabase" ]
 }
)
```

![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/c153d96a-ed31-4e4e-9d86-5c911f76f109)


```
exit
```


# Follow the steps below for the Master Node configuration.

# Master node yapılandırması için aşağıdaki adımları izleyin. 


## So, first, switch to root user.

## Öncelikle root kullanıcısına geçin.

```
sudo su
```

  
## Edit the 'mongod.conf' file for the Master Node by running the following commands. 

## Aşağıdaki komutları çalıştırarak Master Node için 'mongod.conf' dosyasını düzenleyin.

```
vim  /etc/mongod.conf
```


```
# mongod.conf

# for documentation of all options, see:
#   http://docs.mongodb.org/manual/reference/configuration-options/

# Where and how to store data.
storage:
  dbPath: /var/lib/mongodb
  journal:
    enabled: true
#  engine:
#  wiredTiger:

# where to write logging data.
systemLog:
  destination: file
  logAppend: true
  path: /var/log/mongodb/mongod.log

# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1, mongo-master-node



# how the process runs
processManagement:
  timeZoneInfo: /usr/share/zoneinfo

#security:

#operationProfilin


replication:
 replSetName: "mongorepl"
#sharding:

## Enterprise-Only Options:

#auditLog:

#snmp:

```

![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/28dbca0e-5b42-46ca-b58f-428384f6e9c6)



# Follow the steps below for the Node-1 configuration.

# Node-1 yapılandırması için aşağıdaki adımları izleyin. 


## So, first, switch to root user.

## Öncelikle root kullanıcısına geçin.

```
sudo su
```


## Edit the 'mongod.conf' file for the Node-2 by running the following commands. 

## Aşağıdaki komutları çalıştırarak Node-2 için 'mongod.conf' dosyasını düzenleyin.


```
vim  /etc/mongod.conf
```

```
# mongod.conf

# for documentation of all options, see:
#   http://docs.mongodb.org/manual/reference/configuration-options/

# Where and how to store data.
storage:
  dbPath: /var/lib/mongodb
  journal:
    enabled: true
#  engine:
#  wiredTiger:

# where to write logging data.
systemLog:
  destination: file
  logAppend: true
  path: /var/log/mongodb/mongod.log

# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1, mongo-node-1



# how the process runs
processManagement:
  timeZoneInfo: /usr/share/zoneinfo

#security:

#operationProfilin


replication:
 replSetName: "mongorepl"
#sharding:

## Enterprise-Only Options:

#auditLog:

#snmp:


```

```
systemctl restart mongod
```


![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/e4e3bdbd-bcd6-47e9-969d-ac48a22a07b1)





# Follow the steps below for the Node-2 configuration.

# Node-2 yapılandırması için aşağıdaki adımları izleyin. 


## So, first, switch to root user.

## Öncelikle root kullanıcısına geçin.

```
sudo su
```



## Edit the 'mongod.conf' file for the Node-2 by running the following commands. 

## Aşağıdaki komutları çalıştırarak Node-2 için 'mongod.conf' dosyasını düzenleyin.


```
vim  /etc/mongod.conf
```

```
# mongod.conf

# for documentation of all options, see:
#   http://docs.mongodb.org/manual/reference/configuration-options/

# Where and how to store data.
storage:
  dbPath: /var/lib/mongodb
  journal:
    enabled: true
#  engine:
#  wiredTiger:

# where to write logging data.
systemLog:
  destination: file
  logAppend: true
  path: /var/log/mongodb/mongod.log

# network interfaces
net:
  port: 27017
  bindIp: 127.0.0.1, mongo-node-2



# how the process runs
processManagement:
  timeZoneInfo: /usr/share/zoneinfo

#security:

#operationProfilin


replication:
 replSetName: "mongorepl"
#sharding:

## Enterprise-Only Options:

#auditLog:

#snmp:


```

```
systemctl restart mongod
```


![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/17ed8a99-89a6-40b0-8b3a-2634367a9a3e)


## Run the following commands to change the names of our machines.

## Makinelerimizin isimlerini değiştirmek için aşağıdaki komutları çalıştırın. 


## For Master Node.

## Master Node için.

```
hostnamectl set-hostname mongo-master-node
```

## For Node 1.

## Node 1 için.

```
hostnamectl set-hostname mongo-node-1
```

## For Node 2.

## Node 2 için.

```
hostnamectl set-hostname mongo-node-2
```


## Connect to our database from the Master Node server using the 'mongosh' command.

## 'mongosh' komutunu kullanarak Master Node sunucusundan veritabanına bağlanın.


```
mongosh
```

## Switch to the admin user.

## Yönetici kullanıcıya geçin.


```
use admin
```


![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/517d5e4c-3319-4a1d-86df-d8aba488d27b)


## Run the following command to set up the cluster.

## Cluster kurulu için aşağıdaki komutu çalıştırın.


```
rs.initiate()
```

![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/3d7fb968-53eb-4aa4-bb55-b0656553346f)




## Run the following query to add Node 1.

## Node 1'i eklemek için aşağıdaki sorguyu çalıştırın.

```
rs.add("mongo-node-1")
```


![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/4c5d3b46-5807-4064-a169-ace1b4d4036c)


## Run the following query to add Node 2.

## Node 2'i eklemek için aşağıdaki sorguyu çalıştırın.

```
rs.add("mongo-node-2")
```

![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/8c3545cb-bf00-4876-b00b-8d3e4dcc1d92)


## After adding Node 1 and Node 2, you should get an output similar to the following.

## Node 1 ve Node 2’yi ekledikten sonra aşağıdakine benzer bir çıktı almalısınız.

![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/32de71d1-0f06-4d1c-93cd-5451f38b5474)
 


## And finally, run the following command to complete the cluster setup.

## ! NOTE: If the output of this command is not as expected, there may be an issue; review all your installations once again.

## Ve son olarak Cluster kurulumunu tamamlamak için aşağıdaki komutu çalıştırın.

## ! NOT: Bu komutun çıktısı beklendiği gibi değilse bir sorun olabilir; tüm kurulumlarınızı bir kez daha gözden geçirin.


```
rs.status()
```


```
{
  set: 'mongorepl',
  date: ISODate('2024-01-13T06:19:12.632Z'),
  myState: 1,
  term: Long('2'),
  syncSourceHost: '',
  syncSourceId: -1,
  heartbeatIntervalMillis: Long('2000'),
  majorityVoteCount: 2,
  writeMajorityCount: 2,
  votingMembersCount: 3,
  writableVotingMembersCount: 3,
  optimes: {
    lastCommittedOpTime: { ts: Timestamp({ t: 1705126750, i: 1 }), t: Long('2') },
    lastCommittedWallTime: ISODate('2024-01-13T06:19:10.482Z'),
    readConcernMajorityOpTime: { ts: Timestamp({ t: 1705126750, i: 1 }), t: Long('2') },
    appliedOpTime: { ts: Timestamp({ t: 1705126750, i: 1 }), t: Long('2') },
    durableOpTime: { ts: Timestamp({ t: 1705126750, i: 1 }), t: Long('2') },
    lastAppliedWallTime: ISODate('2024-01-13T06:19:10.482Z'),
    lastDurableWallTime: ISODate('2024-01-13T06:19:10.482Z')
  },
  lastStableRecoveryTimestamp: Timestamp({ t: 1705126740, i: 1 }),
  electionCandidateMetrics: {
    lastElectionReason: 'electionTimeout',
    lastElectionDate: ISODate('2024-01-13T06:18:20.452Z'),
    electionTerm: Long('2'),
    lastCommittedOpTimeAtElection: { ts: Timestamp({ t: 0, i: 0 }), t: Long('-1') },
    lastSeenOpTimeAtElection: { ts: Timestamp({ t: 1705126634, i: 1 }), t: Long('1') },
    numVotesNeeded: 1,
    priorityAtElection: 1,
    electionTimeoutMillis: Long('10000'),
    numCatchUpOps: Long('0'),
    newTermStartDate: ISODate('2024-01-13T06:18:20.473Z'),
    wMajorityWriteAvailabilityDate: ISODate('2024-01-13T06:18:20.484Z')
  },
  members: [
    {
      _id: 0,
      name: 'mongo-master-node:27017',
      health: 1,
      state: 1,
      stateStr: 'PRIMARY',
      uptime: 65,
      optime: { ts: Timestamp({ t: 1705126750, i: 1 }), t: Long('2') },
      optimeDate: ISODate('2024-01-13T06:19:10.000Z'),
      lastAppliedWallTime: ISODate('2024-01-13T06:19:10.482Z'),
      lastDurableWallTime: ISODate('2024-01-13T06:19:10.482Z'),
      syncSourceHost: '',
      syncSourceId: -1,
      infoMessage: '',
      electionTime: Timestamp({ t: 1705126700, i: 1 }),
      electionDate: ISODate('2024-01-13T06:18:20.000Z'),
      configVersion: 5,
      configTerm: 2,
      self: true,
      lastHeartbeatMessage: ''
    },
    {
      _id: 1,
      name: 'mongo-node-1:27017',
      health: 1,
      state: 2,
      stateStr: 'SECONDARY',
      uptime: 62,
      optime: { ts: Timestamp({ t: 1705126750, i: 1 }), t: Long('2') },
      optimeDurable: { ts: Timestamp({ t: 1705126750, i: 1 }), t: Long('2') },
      optimeDate: ISODate('2024-01-13T06:19:10.000Z'),
      optimeDurableDate: ISODate('2024-01-13T06:19:10.000Z'),
      lastAppliedWallTime: ISODate('2024-01-13T06:19:10.482Z'),
      lastDurableWallTime: ISODate('2024-01-13T06:19:10.482Z'),
      lastHeartbeat: ISODate('2024-01-13T06:19:12.620Z'),
      lastHeartbeatRecv: ISODate('2024-01-13T06:19:10.786Z'),
      pingMs: Long('0'),
      lastHeartbeatMessage: '',
      syncSourceHost: 'mongo-master-node:27017',
      syncSourceId: 0,
      infoMessage: '',
      configVersion: 5,
      configTerm: 2
    },
    {
      _id: 2,
      name: 'mongo-node-2:27017',
      health: 1,
      state: 2,
      stateStr: 'SECONDARY',
      uptime: 62,
      optime: { ts: Timestamp({ t: 1705126750, i: 1 }), t: Long('2') },
      optimeDurable: { ts: Timestamp({ t: 1705126750, i: 1 }), t: Long('2') },
      optimeDate: ISODate('2024-01-13T06:19:10.000Z'),
      optimeDurableDate: ISODate('2024-01-13T06:19:10.000Z'),
      lastAppliedWallTime: ISODate('2024-01-13T06:19:10.482Z'),
      lastDurableWallTime: ISODate('2024-01-13T06:19:10.482Z'),
      lastHeartbeat: ISODate('2024-01-13T06:19:12.620Z'),
      lastHeartbeatRecv: ISODate('2024-01-13T06:19:10.912Z'),
      pingMs: Long('0'),
      lastHeartbeatMessage: '',
      syncSourceHost: 'mongo-master-node:27017',
      syncSourceId: 0,
      infoMessage: '',
      configVersion: 5,
      configTerm: 2
    }
  ],
  ok: 1,
  '$clusterTime': {
    clusterTime: Timestamp({ t: 1705126750, i: 1 }),
    signature: {
      hash: Binary.createFromBase64('AAAAAAAAAAAAAAAAAAAAAAAAAAA=', 0),
      keyId: Long('0')
    }
  },
  operationTime: Timestamp({ t: 1705126750, i: 1 })
}


```


## To verify our cluster setup, we will create a new database and manually add data. Run the following queries sequentially.

## ! NOTE: If the output of these commands is not as expected, there may be an issue; review all your installations once again.




## Cluster yapımızı kontrol etmek için yeni bir veritabanı oluşturup manuel data ekleyeceğiz bunun için aşağıdaki sorguları sırası ile çalıştırmamız gerekiyor. 

## ! NOT : Bu sorguların çıktısı aşağıdaki gibi değilse bir problem var demektir tekrardan tüm kurulumlarınızı gözden geçirin. 




## 1-) 

```
mongosh
```

## 2-) 

```
use testdb
```


## 3-) 

```
db.employees.insert({Name: "Andrew", Age: 31, City: "Istanbul", Status: "Married"})
```


## 4-) 

```
db.employees.find()
```

![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/e84ee942-2a4a-404c-b91c-9bdc6859939e)



## 5-) 

```
show dbs
```

![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/9bb7f8b5-ccb3-4754-8d54-cb55ae563dc4)



![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/5da5083c-463f-4a58-a41f-fdcb08a95211)



## Finally, execute the following query on all nodes, and you need to restart all your machines. After this process, MongoDB will start functioning as a cluster.


## Ve son olarak aşağıdaki sorugu tüm nodlarda çalıştırıyoruz ve tüm makinalarımızı yeniden başlatmamız gerekiyor bu işlem sonunda MongoDB cluster olarak çalışmaya başlayacaktır.


```
db.getMongo().setReadPref("primaryPreferred")
```




## If you want to check the success of our installation, run the following command on Node 1 or Node 2. The purpose of this is that when we insert data into the database on the Master Node, the same data should be written to Node 1 and Node 2 instantly.


## Eğer kurulumumuzun başarılı olduğu kontrol etmek istiyorsak aşağıdaki komutu Node 1 veya Node 2'de çalıştırın. Bunu yapmamızdaki amaç Master Node'da database e bir data insert ettiğimizde aynı datayı Node 1 ve Node 2'e yazması gerekiyor anlık olarak.

```
db.employees.find()
```

![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/cae10eb9-590c-47c5-8db1-201b6a0e74a9)




