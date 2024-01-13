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

## Makinelerimizin isimlerini değiştirmek için aşağıdaki komutları çalıştırınız. 


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


## *

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
  date: ISODate('2024-01-13T05:52:23.380Z'),
  myState: 1,
  term: Long('1'),
  syncSourceHost: '',
  syncSourceId: -1,
  heartbeatIntervalMillis: Long('2000'),
  majorityVoteCount: 1,
  writeMajorityCount: 1,
  votingMembersCount: 1,
  writableVotingMembersCount: 1,
  optimes: {
    lastCommittedOpTime: { ts: Timestamp({ t: 1705125133, i: 1 }), t: Long('1') },
    lastCommittedWallTime: ISODate('2024-01-13T05:52:13.983Z'),
    readConcernMajorityOpTime: { ts: Timestamp({ t: 1705125133, i: 1 }), t: Long('1') },
    appliedOpTime: { ts: Timestamp({ t: 1705125133, i: 1 }), t: Long('1') },
    durableOpTime: { ts: Timestamp({ t: 1705125133, i: 1 }), t: Long('1') },
    lastAppliedWallTime: ISODate('2024-01-13T05:52:13.983Z'),
    lastDurableWallTime: ISODate('2024-01-13T05:52:13.983Z')
  },
  lastStableRecoveryTimestamp: Timestamp({ t: 1705125123, i: 1 }),
  electionCandidateMetrics: {
    lastElectionReason: 'electionTimeout',
    lastElectionDate: ISODate('2024-01-13T05:45:13.922Z'),
    electionTerm: Long('1'),
    lastCommittedOpTimeAtElection: { ts: Timestamp({ t: 1705124713, i: 1 }), t: Long('-1') },
    lastSeenOpTimeAtElection: { ts: Timestamp({ t: 1705124713, i: 1 }), t: Long('-1') },
    numVotesNeeded: 1,
    priorityAtElection: 1,
    electionTimeoutMillis: Long('10000'),
    newTermStartDate: ISODate('2024-01-13T05:45:13.933Z'),
    wMajorityWriteAvailabilityDate: ISODate('2024-01-13T05:45:13.939Z')
  },
  members: [
    {
      _id: 0,
      name: 'mongo-master-node:27017',
      health: 1,
      state: 1,
      stateStr: 'PRIMARY',
      uptime: 2501,
      optime: { ts: Timestamp({ t: 1705125133, i: 1 }), t: Long('1') },
      optimeDate: ISODate('2024-01-13T05:52:13.000Z'),
      lastAppliedWallTime: ISODate('2024-01-13T05:52:13.983Z'),
      lastDurableWallTime: ISODate('2024-01-13T05:52:13.983Z'),
      syncSourceHost: '',
      syncSourceId: -1,
      infoMessage: '',
      electionTime: Timestamp({ t: 1705124713, i: 2 }),
      electionDate: ISODate('2024-01-13T05:45:13.000Z'),
      configVersion: 3,
      configTerm: 1,
      self: true,
      lastHeartbeatMessage: ''
    },
    {
      _id: 1,
      name: 'mongo-node-1:27017',
      health: 0,
      state: 8,
      stateStr: '(not reachable/healthy)',
      uptime: 0,
      optime: { ts: Timestamp({ t: 0, i: 0 }), t: Long('-1') },
      optimeDurable: { ts: Timestamp({ t: 0, i: 0 }), t: Long('-1') },
      optimeDate: ISODate('1970-01-01T00:00:00.000Z'),
      optimeDurableDate: ISODate('1970-01-01T00:00:00.000Z'),
      lastAppliedWallTime: ISODate('1970-01-01T00:00:00.000Z'),
      lastDurableWallTime: ISODate('1970-01-01T00:00:00.000Z'),
      lastHeartbeat: ISODate('2024-01-13T05:52:21.794Z'),
      lastHeartbeatRecv: ISODate('1970-01-01T00:00:00.000Z'),
      pingMs: Long('0'),
      lastHeartbeatMessage: 'Error connecting to mongo-node-1:27017 (192.168.152.157:27017) :: caused by :: Connection refused',
      syncSourceHost: '',
      syncSourceId: -1,
      infoMessage: '',
      configVersion: -1,
      configTerm: -1
    },
    {
      _id: 2,
      name: 'mongo-node-2:27017',
      health: 0,
      state: 8,
      stateStr: '(not reachable/healthy)',
      uptime: 0,
      optime: { ts: Timestamp({ t: 0, i: 0 }), t: Long('-1') },
      optimeDurable: { ts: Timestamp({ t: 0, i: 0 }), t: Long('-1') },
      optimeDate: ISODate('1970-01-01T00:00:00.000Z'),
      optimeDurableDate: ISODate('1970-01-01T00:00:00.000Z'),
      lastAppliedWallTime: ISODate('1970-01-01T00:00:00.000Z'),
      lastDurableWallTime: ISODate('1970-01-01T00:00:00.000Z'),
      lastHeartbeat: ISODate('2024-01-13T05:52:21.795Z'),
      lastHeartbeatRecv: ISODate('1970-01-01T00:00:00.000Z'),
      pingMs: Long('0'),
      lastHeartbeatMessage: 'Error connecting to mongo-node-2:27017 (192.168.152.158:27017) :: caused by :: Connection refused',
      syncSourceHost: '',
      syncSourceId: -1,
      infoMessage: '',
      configVersion: -1,
      configTerm: -1
    }
  ],
  ok: 1,
  '$clusterTime': {
    clusterTime: Timestamp({ t: 1705125133, i: 1 }),
    signature: {
      hash: Binary.createFromBase64('AAAAAAAAAAAAAAAAAAAAAAAAAAA=', 0),
      keyId: Long('0')
    }
  },
  operationTime: Timestamp({ t: 1705125133, i: 1 })
}

```
