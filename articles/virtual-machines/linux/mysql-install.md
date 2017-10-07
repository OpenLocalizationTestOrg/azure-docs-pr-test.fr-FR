---
title: aaaSet de MySQL sur un VM Linux dans Azure | Documents Microsoft
description: "Découvrez comment tooinstall hello MySQL de pile sur un ordinateur virtuel de Linux (Ubuntu ou RedHat famille du système d’exploitation) dans Azure"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 153bae7c-897b-46b3-bd86-192a6efb94fa
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: e47d0de7f0eb5bb873ad20e4bc35f1b5f8d33bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-mysql-on-azure"></a>Comment tooinstall MySQL sur Azure
Dans cet article, vous allez apprendre comment tooinstall et configurer MySQL sur une machine virtuelle Azure exécutant Linux.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a>Installation de MySQL sur votre machine virtuelle
> [!NOTE]
> Vous devez déjà disposer d’une machine virtuelle de Microsoft Azure exécutant Linux dans l’ordre toocomplete ce didacticiel. Consultez le [didacticiel de la machine virtuelle de Azure Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate et configurer un VM Linux avec `mysqlnode` en tant que nom d’ordinateur virtuel hello et `azureuser` en tant qu’utilisateur avant de continuer.
> 
> 

Dans ce cas, utilisez 3306 port comme hello MySQL port.  

Se connecter toohello VM Linux vous avez créé via putty. S’il s’agit hello première fois que vous utilisez Azure Linux VM, consultez Comment toouse putty connecter tooa Linux VM [ici](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Nous allons utiliser référentiel package tooinstall MySQL5.6 d’exemple dans cet article. En réalité, MySQL5.6 est une version améliorée en termes de performances par rapport à MySQL5.5.  Plus d’informations [ici](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).

### <a name="how-tooinstall-mysql56-on-ubuntu"></a>Comment tooinstall MySQL5.6 sur Ubuntu
Nous utiliserons ici une machine virtuelle Linux avec Ubuntu à partir d’Azure.

* Étape 1 : Installer un serveur MySQL 5.6 basculer trop`root` utilisateur :
  
            #[azureuser@mysqlnode:~]sudo su -
  
    Instraller mysql-server 5.6 :
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    Pendant l’installation, vous verrez un poping de fenêtre de boîte de dialogue des tooask vous tooset MySQL racine et mot de passe ci-dessous, vous devez définir hello mot de passe ici.
  
    ![image](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    Mot de passe d’entrée hello tooconfirm à nouveau.

    ![image](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* Étape 2 : connexion au serveur MySQL
  
    Une fois l’installation du serveur MySQL terminée, le service MySQL démarre automatiquement. Vous pouvez vous connecter au serveur MySQL avec l’utilisateur `root` .
    Utilisez hello ci-dessous commande toologin et entrée de mot de passe.
  
             #[root@mysqlnode ~]# mysql -uroot -p
* Étape 3 : Gérez hello service MySQL en cours d’exécution
  
    (a) Obtenir l’état du service MySQL
  
             #[root@mysqlnode ~]# service mysql status
  
    (b) Démarrer le service MySQL
  
             #[root@mysqlnode ~]# service mysql start
  
    (c) Arrêter le service MySQL
  
             #[root@mysqlnode ~]# service mysql stop
  
    (d) redémarrez le service MySQL de hello
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a>Comment tooinstall MySQL sur la famille de systèmes d’exploitation de Red Hat que CentOS, Oracle Linux
Nous utiliserons ici des machines virtuelles Linux avec CentOS ou Oracle Linux.

* Étape 1 : Ajouter hello MySQL Yum référentiel commutateur trop`root` utilisateur :
  
            #[azureuser@mysqlnode:~]sudo su -
  
    Téléchargez et installez le package de version de MySQL hello :
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* Étape 2 : Modifiez ci-dessous le dépôt de fichiers tooenable hello MySQL pour télécharger le package de MySQL5.6 hello.
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    Mise à jour de chaque valeur de cette toobelow de fichier :
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* Étape 3 : installer MySQL à partir du référentiel MySQL   Installer MySQL:
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    Le package RPM MySQL et tous les packages associés seront installés.
* Étape 4 : Gérer hello service MySQL en cours d’exécution
  
    (a) Vérifiez l’état du service hello du serveur MySQL de hello :
  
           #[root@mysqlnode ~]#service mysqld status
  
    (b) vérifie si le serveur de port de MySQL par défaut hello s’exécute :
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    (c) Démarrer hello MySQL server :

           #[root@mysqlnode ~]#service mysqld start

    (d) arrêter le serveur MySQL de hello :

           #[root@mysqlnode ~]#service mysqld stop

    (e) définir MySQL toostart lorsque le système de hello démarrage à distance :

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a>Comment tooinstall MySQL sur SUSE Linux
Nous utiliserons ici une machine virtuelle Linux avec OpenSUSE.

* Étape 1 : téléchargez et installez MySQL Server
  
    Basculer trop`root` utilisateur par le biais de commande ci-dessous :  
  
           #sudo su -
  
    Téléchargez et installez le package MySQL :
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* Étape 2 : Gérer hello service MySQL en cours d’exécution
  
    (a) vérifier l’état de hello du serveur MySQL de hello :
  
           #[root@mysqlnode ~]# rcmysql status
  
    (b) la case hello indique si le port par défaut du serveur MySQL de hello :
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    (c) Démarrer hello MySQL server :

           #[root@mysqlnode ~]# rcmysql start

    (d) arrêter le serveur MySQL de hello :

           #[root@mysqlnode ~]# rcmysql stop

    (e) définir MySQL toostart lorsque le système de hello démarrage à distance :

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a>Étape suivante
Vous trouverez plus d’informations sur l’utilisation de MySQL [ici](https://www.mysql.com/).

