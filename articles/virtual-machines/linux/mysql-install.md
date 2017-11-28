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
# <a name="how-tooinstall-mysql-on-azure"></a><span data-ttu-id="b5854-103">Comment tooinstall MySQL sur Azure</span><span class="sxs-lookup"><span data-stu-id="b5854-103">How tooinstall MySQL on Azure</span></span>
<span data-ttu-id="b5854-104">Dans cet article, vous allez apprendre comment tooinstall et configurer MySQL sur une machine virtuelle Azure exécutant Linux.</span><span class="sxs-lookup"><span data-stu-id="b5854-104">In this article, you will learn how tooinstall and configure MySQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-mysql-on-your-virtual-machine"></a><span data-ttu-id="b5854-105">Installation de MySQL sur votre machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b5854-105">Install MySQL on your virtual machine</span></span>
> [!NOTE]
> <span data-ttu-id="b5854-106">Vous devez déjà disposer d’une machine virtuelle de Microsoft Azure exécutant Linux dans l’ordre toocomplete ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="b5854-106">You must already have a Microsoft Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="b5854-107">Consultez le [didacticiel de la machine virtuelle de Azure Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate et configurer un VM Linux avec `mysqlnode` en tant que nom d’ordinateur virtuel hello et `azureuser` en tant qu’utilisateur avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="b5854-107">Please see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate and set up a Linux VM with `mysqlnode` as hello VM name and `azureuser` as user before proceeding.</span></span>
> 
> 

<span data-ttu-id="b5854-108">Dans ce cas, utilisez 3306 port comme hello MySQL port.</span><span class="sxs-lookup"><span data-stu-id="b5854-108">In this case, use 3306 port as hello MySQL port.</span></span>  

<span data-ttu-id="b5854-109">Se connecter toohello VM Linux vous avez créé via putty.</span><span class="sxs-lookup"><span data-stu-id="b5854-109">Connect toohello Linux VM you created via putty.</span></span> <span data-ttu-id="b5854-110">S’il s’agit hello première fois que vous utilisez Azure Linux VM, consultez Comment toouse putty connecter tooa Linux VM [ici](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b5854-110">If this is hello first time you use Azure Linux VM, see how toouse putty connect tooa Linux VM [here](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b5854-111">Nous allons utiliser référentiel package tooinstall MySQL5.6 d’exemple dans cet article.</span><span class="sxs-lookup"><span data-stu-id="b5854-111">We will use repository package tooinstall MySQL5.6 as an example in this article.</span></span> <span data-ttu-id="b5854-112">En réalité, MySQL5.6 est une version améliorée en termes de performances par rapport à MySQL5.5.</span><span class="sxs-lookup"><span data-stu-id="b5854-112">Actually, MySQL5.6 has more improvement in performance than MySQL5.5.</span></span>  <span data-ttu-id="b5854-113">Plus d’informations [ici](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span><span class="sxs-lookup"><span data-stu-id="b5854-113">More information [here](http://www.mysqlperformanceblog.com/2013/02/18/is-mysql-5-6-slower-than-mysql-5-5/).</span></span>

### <a name="how-tooinstall-mysql56-on-ubuntu"></a><span data-ttu-id="b5854-114">Comment tooinstall MySQL5.6 sur Ubuntu</span><span class="sxs-lookup"><span data-stu-id="b5854-114">How tooinstall MySQL5.6 on Ubuntu</span></span>
<span data-ttu-id="b5854-115">Nous utiliserons ici une machine virtuelle Linux avec Ubuntu à partir d’Azure.</span><span class="sxs-lookup"><span data-stu-id="b5854-115">We will use Linux VM with Ubuntu from Azure here.</span></span>

* <span data-ttu-id="b5854-116">Étape 1 : Installer un serveur MySQL 5.6 basculer trop`root` utilisateur :</span><span class="sxs-lookup"><span data-stu-id="b5854-116">Step 1: Install MySQL Server 5.6   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="b5854-117">Instraller mysql-server 5.6 :</span><span class="sxs-lookup"><span data-stu-id="b5854-117">Install mysql-server 5.6:</span></span>
  
            #[root@mysqlnode ~]# apt-get update
            #[root@mysqlnode ~]# apt-get -y install mysql-server-5.6
  
    <span data-ttu-id="b5854-118">Pendant l’installation, vous verrez un poping de fenêtre de boîte de dialogue des tooask vous tooset MySQL racine et mot de passe ci-dessous, vous devez définir hello mot de passe ici.</span><span class="sxs-lookup"><span data-stu-id="b5854-118">During installation, you will see a dialog window poping up tooask you tooset MySQL root password below, and you need set hello password here.</span></span>
  
    ![image](./media/mysql-install/virtual-machines-linux-install-mysql-p1.png)

    <span data-ttu-id="b5854-120">Mot de passe d’entrée hello tooconfirm à nouveau.</span><span class="sxs-lookup"><span data-stu-id="b5854-120">Input hello password again tooconfirm.</span></span>

    ![image](./media/mysql-install/virtual-machines-linux-install-mysql-p2.png)

* <span data-ttu-id="b5854-122">Étape 2 : connexion au serveur MySQL</span><span class="sxs-lookup"><span data-stu-id="b5854-122">Step 2: Login MySQL Server</span></span>
  
    <span data-ttu-id="b5854-123">Une fois l’installation du serveur MySQL terminée, le service MySQL démarre automatiquement.</span><span class="sxs-lookup"><span data-stu-id="b5854-123">When MySQL server installation finished, MySQL service will be started automatically.</span></span> <span data-ttu-id="b5854-124">Vous pouvez vous connecter au serveur MySQL avec l’utilisateur `root` .</span><span class="sxs-lookup"><span data-stu-id="b5854-124">You can login MySQL Server with `root` user.</span></span>
    <span data-ttu-id="b5854-125">Utilisez hello ci-dessous commande toologin et entrée de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="b5854-125">Use hello below command toologin and input password.</span></span>
  
             #[root@mysqlnode ~]# mysql -uroot -p
* <span data-ttu-id="b5854-126">Étape 3 : Gérez hello service MySQL en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="b5854-126">Step 3: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="b5854-127">(a) Obtenir l’état du service MySQL</span><span class="sxs-lookup"><span data-stu-id="b5854-127">(a) Get status of MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql status
  
    <span data-ttu-id="b5854-128">(b) Démarrer le service MySQL</span><span class="sxs-lookup"><span data-stu-id="b5854-128">(b) Start MySQL Service</span></span>
  
             #[root@mysqlnode ~]# service mysql start
  
    <span data-ttu-id="b5854-129">(c) Arrêter le service MySQL</span><span class="sxs-lookup"><span data-stu-id="b5854-129">(c) Stop MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql stop
  
    <span data-ttu-id="b5854-130">(d) redémarrez le service MySQL de hello</span><span class="sxs-lookup"><span data-stu-id="b5854-130">(d) Restart hello MySQL service</span></span>
  
             #[root@mysqlnode ~]# service mysql restart

### <a name="how-tooinstall-mysql-on-red-hat-os-family-like-centos-oracle-linux"></a><span data-ttu-id="b5854-131">Comment tooinstall MySQL sur la famille de systèmes d’exploitation de Red Hat que CentOS, Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="b5854-131">How tooinstall MySQL on Red Hat OS family like CentOS, Oracle Linux</span></span>
<span data-ttu-id="b5854-132">Nous utiliserons ici des machines virtuelles Linux avec CentOS ou Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="b5854-132">We will use Linux VM with CentOS or Oracle Linux here.</span></span>

* <span data-ttu-id="b5854-133">Étape 1 : Ajouter hello MySQL Yum référentiel commutateur trop`root` utilisateur :</span><span class="sxs-lookup"><span data-stu-id="b5854-133">Step 1: Add hello MySQL Yum repository   Switch too`root` user:</span></span>
  
            #[azureuser@mysqlnode:~]sudo su -
  
    <span data-ttu-id="b5854-134">Téléchargez et installez le package de version de MySQL hello :</span><span class="sxs-lookup"><span data-stu-id="b5854-134">Download and install hello MySQL release package:</span></span>
  
            #[root@mysqlnode ~]# wget http://repo.mysql.com/mysql-community-release-el6-5.noarch.rpm
            #[root@mysqlnode ~]# yum localinstall -y mysql-community-release-el6-5.noarch.rpm
* <span data-ttu-id="b5854-135">Étape 2 : Modifiez ci-dessous le dépôt de fichiers tooenable hello MySQL pour télécharger le package de MySQL5.6 hello.</span><span class="sxs-lookup"><span data-stu-id="b5854-135">Step 2: Edit below file tooenable hello MySQL repository for downloading hello MySQL5.6 package.</span></span>
  
            #[root@mysqlnode ~]# vim /etc/yum.repos.d/mysql-community.repo
  
    <span data-ttu-id="b5854-136">Mise à jour de chaque valeur de cette toobelow de fichier :</span><span class="sxs-lookup"><span data-stu-id="b5854-136">Update each value of this file toobelow:</span></span>
  
        \# *Enable toouse MySQL 5.6*
  
        [mysql56-community]
        name=MySQL 5.6 Community Server
  
        baseurl=http://repo.mysql.com/yum/mysql-5.6-community/el/6/$basearch/
  
        enabled=1
  
        gpgcheck=1
  
        gpgkey=file:/etc/pki/rpm-gpg/RPM-GPG-KEY-mysql
* <span data-ttu-id="b5854-137">Étape 3 : installer MySQL à partir du référentiel MySQL   Installer MySQL:</span><span class="sxs-lookup"><span data-stu-id="b5854-137">Step 3: Install MySQL from MySQL repository   Install MySQL:</span></span>
  
           #[root@mysqlnode ~]#yum install mysql-community-server
  
    <span data-ttu-id="b5854-138">Le package RPM MySQL et tous les packages associés seront installés.</span><span class="sxs-lookup"><span data-stu-id="b5854-138">MySQL RPM package and all related packages will be installed.</span></span>
* <span data-ttu-id="b5854-139">Étape 4 : Gérer hello service MySQL en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="b5854-139">Step 4: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="b5854-140">(a) Vérifiez l’état du service hello du serveur MySQL de hello :</span><span class="sxs-lookup"><span data-stu-id="b5854-140">(a) Check hello service status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]#service mysqld status
  
    <span data-ttu-id="b5854-141">(b) vérifie si le serveur de port de MySQL par défaut hello s’exécute :</span><span class="sxs-lookup"><span data-stu-id="b5854-141">(b) Check whether hello default port of  MySQL server is running:</span></span>
  
           #[root@mysqlnode ~]#netstat  –tunlp|grep 3306

    <span data-ttu-id="b5854-142">(c) Démarrer hello MySQL server :</span><span class="sxs-lookup"><span data-stu-id="b5854-142">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld start

    <span data-ttu-id="b5854-143">(d) arrêter le serveur MySQL de hello :</span><span class="sxs-lookup"><span data-stu-id="b5854-143">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]#service mysqld stop

    <span data-ttu-id="b5854-144">(e) définir MySQL toostart lorsque le système de hello démarrage à distance :</span><span class="sxs-lookup"><span data-stu-id="b5854-144">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]#chkconfig mysqld on


### <a name="how-tooinstall-mysql-on-suse-linux"></a><span data-ttu-id="b5854-145">Comment tooinstall MySQL sur SUSE Linux</span><span class="sxs-lookup"><span data-stu-id="b5854-145">How tooinstall MySQL on SUSE Linux</span></span>
<span data-ttu-id="b5854-146">Nous utiliserons ici une machine virtuelle Linux avec OpenSUSE.</span><span class="sxs-lookup"><span data-stu-id="b5854-146">We will use Linux VM with OpenSUSE here.</span></span>

* <span data-ttu-id="b5854-147">Étape 1 : téléchargez et installez MySQL Server</span><span class="sxs-lookup"><span data-stu-id="b5854-147">Step 1: Download and install MySQL Server</span></span>
  
    <span data-ttu-id="b5854-148">Basculer trop`root` utilisateur par le biais de commande ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b5854-148">Switch too`root` user through below command:</span></span>  
  
           #sudo su -
  
    <span data-ttu-id="b5854-149">Téléchargez et installez le package MySQL :</span><span class="sxs-lookup"><span data-stu-id="b5854-149">Download and install MySQL package:</span></span>
  
           #[root@mysqlnode ~]# zypper update
  
           #[root@mysqlnode ~]# zypper install mysql-server mysql-devel mysql
* <span data-ttu-id="b5854-150">Étape 2 : Gérer hello service MySQL en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="b5854-150">Step 2: Manage hello running MySQL service</span></span>
  
    <span data-ttu-id="b5854-151">(a) vérifier l’état de hello du serveur MySQL de hello :</span><span class="sxs-lookup"><span data-stu-id="b5854-151">(a) Check hello status of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# rcmysql status
  
    <span data-ttu-id="b5854-152">(b) la case hello indique si le port par défaut du serveur MySQL de hello :</span><span class="sxs-lookup"><span data-stu-id="b5854-152">(b) Check whether hello default port of hello MySQL server:</span></span>
  
           #[root@mysqlnode ~]# netstat  –tunlp|grep 3306

    <span data-ttu-id="b5854-153">(c) Démarrer hello MySQL server :</span><span class="sxs-lookup"><span data-stu-id="b5854-153">(c) Start hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql start

    <span data-ttu-id="b5854-154">(d) arrêter le serveur MySQL de hello :</span><span class="sxs-lookup"><span data-stu-id="b5854-154">(d) Stop hello MySQL server:</span></span>

           #[root@mysqlnode ~]# rcmysql stop

    <span data-ttu-id="b5854-155">(e) définir MySQL toostart lorsque le système de hello démarrage à distance :</span><span class="sxs-lookup"><span data-stu-id="b5854-155">(e) Set MySQL toostart when hello system boot-up:</span></span>

           #[root@mysqlnode ~]# insserv mysql

### <a name="next-step"></a><span data-ttu-id="b5854-156">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="b5854-156">Next Step</span></span>
<span data-ttu-id="b5854-157">Vous trouverez plus d’informations sur l’utilisation de MySQL [ici](https://www.mysql.com/).</span><span class="sxs-lookup"><span data-stu-id="b5854-157">Find more usage and information regarding MySQL [Here](https://www.mysql.com/).</span></span>

