# Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04


Guide to SonarQube 8.9 Community Edition Installation & Configuration On Ubuntu 22.04


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


## Run the following command to create the 'keyfile'.

## 'keyfike' dosyasını oluşturmak için aşağıdaki komutu çalıştırın.


```
apt-get install genometools
```

![image](https://github.com/R4ynaud/Installation-and-Configuration-of-MongoDB-Cluster-on-Ubuntu-20.04-/assets/93924485/6018c7f1-4199-48b7-b36a-82cf7d0e0aa5)



```
openssl rand -base64 756 &gt; /mnt/keyfile
```

















