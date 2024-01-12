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


## Install wget and unzip package.


## Wget'i yükleyin ve paketi çıkartın.


```
apt-get install wget unzip -y
```


![image](https://github.com/R4ynaud/SonarQube-Community-Edition-Installation-configuration-on-Ubuntu-22.04/assets/93924485/67ebdb4b-5855-4687-87e5-de0fcdd62f22)


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










