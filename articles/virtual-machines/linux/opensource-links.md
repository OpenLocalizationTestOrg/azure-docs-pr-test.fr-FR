---
title: aaaLinux et Open Source informatique sur Azure | Documents Microsoft
description: "Répertorie des articles sur Linux et l’informatique open source dans Azure, notamment sur l’utilisation de base de Linux, certains concepts essentiels sur l’exécution ou le téléchargement d’images Linux dans Azure, ainsi que d’autres indications sur des technologies et optimisations spécifiques."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: a7e608b5-26ea-41e0-b46b-1a483a257754
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/27/2016
ms.author: rasquill
ms.openlocfilehash: 3ce0dcc65f28d0dddb29f654409f6dae56213bc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="linux-and-open-source-computing-on-azure"></a>Linux et informatique open-source sur Azure
Rechercher toute la documentation hello vous devez toocreate et gérez des ordinateurs virtuels Linux dans le modèle de déploiement classique hello.

> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

## <a name="get-started"></a>Prise en main
* [Présentation de Linux sous Azure](intro-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Forum aux questions sur les Machines virtuelles Azure créé avec le modèle de déploiement classique de hello](classic/faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [À propos des images pour les machines virtuelles](../windows/classic/about-images.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Chargement de votre propre image de distribution](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) (et instructions d’utilisation d’une [distribution approuvée dans Azure](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))
* [Une session hello de Linux à l’aide de machine virtuelle tooa portail Azure classic](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="set-up"></a>Installation
* [Installer l’interface de ligne de commande Microsoft Azure](../../cli-install-nodejs.md)

## <a name="tutorials"></a>Didacticiels
* [Installer hello pile LAMP sur un ordinateur virtuel de Linux dans Azure](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Application Web Ruby on Rails sur une machine virtuelle Azure](classic/virtual-machines-linux-classic-ruby-rails-web-app.md)
* [Installation d’Apache Qpid Proton-C pour AMQP et Service Bus](../../service-bus-messaging/service-bus-amqp-apache.md)

### <a name="databases"></a>Bases de données
* [optimisation des performances de MySQL dans Azure](classic/optimize-mysql.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [clusters MySQL](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [exécution de Cassandra avec Linux sur Azure et accès au cluster depuis Node.js](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [création d'un cluster multimaîtres de bases de données MariaDb](classic/mariadb-mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="hpc"></a>HPC
* [Prise en main des nœuds de calcul Linux dans un cluster HPC Pack dans Azure](classic/hpcpack-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Exécution de NAMD avec Microsoft HPC Pack sur des nœuds de calcul Linux dans Azure](classic/hpcpack-cluster-namd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Configurer une application MPI de Linux RDMA cluster toorun](classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="docker"></a>Docker
* [À l’aide de hello Extension de machine virtuelle Docker à partir de hello Azure Interface de ligne (Azure)](classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [À l’aide de hello Extension de machine virtuelle Docker à partir de hello portail Azure](classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [La machine docker toouse sur Azure](docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="ubuntu"></a>Ubuntu
* [Clusters MySQL](classic/mysql-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Node.js et Cassandra](classic/cassandra-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="opensuse"></a>OpenSUSE
* [Installation et exécution de MySQL](classic/mysql-on-opensuse.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

### <a name="coreos"></a>CoreOS
* [Utilisation de CoreOS dans Azure](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="planning"></a>Planification
* [Instructions d’implémentation des services d’infrastructure Azure](../windows/infrastructure-subscription-accounts-guidelines.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [sélection de noms d'utilisateurs Linux](usernames.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Comment tooconfigure un ensemble de disponibilité des machines virtuelles dans le modèle de déploiement classique de hello](../windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Comment tooSchedule Maintenance planifiée sur les machines virtuelles Azure](classic/planned-maintenance-schedule.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Gérer la disponibilité hello des machines virtuelles](../windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Maintenance planifiée des machines virtuelles Linux dans Azure](planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="deployment"></a>Déploiement
* [Création d’une machine virtuelle personnalisée exécutant Linux](../windows/classic/createportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Hello notions de base : capture un tooMake Linux VM un modèle](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Informations concernant les distributions non approuvées](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="management"></a>Gestion
* [SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Comment tooReset un mot de passe ou les propriétés SSH pour Linux](classic/reset-access.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [utilisation de la racine](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="azure-resources"></a>Ressources Azure
* [Hello Agent Linux Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Fonctionnalités et extensions de machine virtuelle Azure](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Injecter des données personnalisées dans un toouse de machine virtuelle avec init-Cloud](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="storage"></a>Storage
* [Attachement d’un disque de données de tooa Linux VM](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [détachement d'un disque de données d'une machine virtuelle Linux](classic/detach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a>Mise en réseau
* [Comment tooset des points de terminaison sur un ordinateur virtuel classique dans Azure](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

## <a name="troubleshooting"></a>Résolution des problèmes
* [Résoudre les problèmes de SSH (Secure Shell) connexions tooa basés sur Linux machine virtuelle Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Résoudre les problèmes de déploiement Classic liés à la création d’une machine virtuelle Linux dans Azure](classic/troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)  
* [Résoudre les problèmes de déploiement Classic liés au redémarrage ou au redimensionnement d’une machine virtuelle Linux existante dans Azure](../windows/restart-resize-error-troubleshooting.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) 

## <a name="reference"></a>Référence
* [Commandes de l’interface de ligne de commande Azure en mode Azure Service Management (ASM)](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [API REST de gestion de service Microsoft Azure](https://msdn.microsoft.com/library/azure/ee460799.aspx)

## <a name="general-links"></a>Liens généraux
Hello suivant liens est pour les blogs Microsoft, pages de Technet et des sites externes au lieu de documentation Azure.com comme indiqué ci-dessus. En tant qu’Azure et hello world de calcul open source fast-déplacez des cibles, il est presque certain qu’hello les liens suivants sont obsolètes, *malgré* faits hello que nous allons faire nos meilleures toocontinually ajouter des rubriques plus récente et supprimer ceux qui sont obsolètes. Si nous avons manqué un, veuillez nous savoir dans les commentaires de hello, ou envoyer un tooour de demande d’extraction [référentiel GitHub](https://github.com/Azure/azure-content/).

* [Exécution d'ASP.NET 5 sur Linux à l'aide de conteneurs Docker](http://blogs.msdn.com/b/webdev/archive/2015/01/14/running-asp-net-5-applications-in-linux-containers-with-docker.aspx)
* [Comment tooDeploy une Image de machine virtuelle CentOS par OpenLogic](https://azure.microsoft.com/blog/2013/01/11/deploying-openlogic-centos-images-on-windows-azure-virtual-machines/)
* [SUSE Update Infrastructure (Infrastructure de mise à jour SUSE)](https://forums.suse.com/showthread.php?5622-New-Update-Infrastructure)
* [SUSE Linux Enterprise Server pour SAP Cloud Appliance Library](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver11sp3forsapcloudappliance/)
* [génération d'une distribution Linux à haute disponibilité dans Azure en 12 étapes](http://blogs.technet.com/b/keithmayer/archive/2014/10/03/quick-start-guide-building-highly-available-linux-servers-in-the-cloud-on-microsoft-azure.aspx)
* [Automate Provisioning Linux on Azure with Azure CLI, node.js, jhawk (Automatisation de l’approvisionnement de Linux dans Azure avec l’interface de ligne de commande Azure, node.js et jhawk)](http://blogs.technet.com/b/keithmayer/archive/2014/11/24/step-by-step-automated-provisioning-for-linux-in-the-cloud-with-microsoft-azure-xplat-cli-json-and-node-js-part-1.aspx)
* [GlusterFS sur Azure](http://dastouri.azurewebsites.net/gluster-on-azure-part-1/)

### <a name="freebsd"></a>FreeBSD
* [exécution de FreeBSD dans Azure](https://azure.microsoft.com/blog/2014/05/22/running-freebsd-in-azure/)
* [déploiement facile de FreeBSD](http://msopentech.com/blog/2014/10/24/easy-deploy-freebsd-microsoft-azure-vm-depot/)
* [déploiement d'une image FreeBSD personnalisée](http://msopentech.com/blog/2014/05/14/deploy-customize-freebsd-virtual-machine-image-microsoft-azure/)
* [Kaspersky Antivirus pour Linux File Server](https://azure.microsoft.com/marketplace/partners/kaspersky-lab/kav-for-lfs-kav-for-lfs/)

### <a name="nosql"></a>Nosql
* [8 sources de données NoSql open source pour Azure](http://openness.microsoft.com/blog/2014/11/03/open-source-nosql-databases-microsoft-azure/)
* [Slideshare (MSOpenTech) : Expériences d’utilisation de CouchDb dans Azure](http://www.slideshare.net/brianbenz/experiences-using-couchdb-inside-microsofts-azure-team)
* [exécution de CouchDB-as-a-Service avec node.js, CORS et Grunt](http://msopentech.com/blog/2013/12/19/tutorial-building-multi-tier-windows-azure-web-application-use-cloudants-couchdb-service-node-js-cors-grunt-2/)
* [Redis sur Windows Bonjour Service de Cache Redis Azure](http://msopentech.com/blog/2014/05/12/redis-on-windows/)
* [annonce du fournisseur d'état de session ASP.NET pour la version d'aperçu de Redis](http://blogs.msdn.com/b/webdev/archive/2014/05/12/announcing-asp-net-session-state-provider-for-redis-preview-release.aspx)
* [Blog : RavenHQ désormais disponible Bonjour Azure Marketplace](https://azure.microsoft.com/blog/2014/08/12/ravenhq-now-available-in-the-azure-store/)

### <a name="big-data"></a>Données volumineuses (« Big Data »)
* [installation de Hadoop sur des machines virtuelles Linux Azure](http://blogs.msdn.com/b/benjguin/archive/2013/04/05/how-to-install-hadoop-on-windows-azure-linux-virtual-machines.aspx)
* [Azure HDInsight](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/)

### <a name="relational-database"></a>Base de données relationnelle
* [Architecture de haute disponibilité MySQL dans Microsoft Azure](http://download.microsoft.com/download/6/1/C/61C0E37C-F252-4B33-9557-42B90BA3E472/MySQL_HADR_solution_in_Azure.pdf)
* [Installation de Postgres avec corosync, pg_bouncer en utilisant ILB](https://github.com/chgeuer/postgres-azure)

### <a name="linux-high-performance-computing-hpc"></a>Calcul haute performance (HPC) Linux
* [Modèle de démarrage rapide : Spin up a SLURM cluster](https://github.com/Azure/azure-quickstart-templates/tree/master/slurm) (et [billet de blog](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx))
* [Modèle de démarrage rapide : Création d'un cluster HPC avec des nœuds de calcul Linux](https://azure.microsoft.com/documentation/templates/create-hpc-cluster-linux-cn/)

### <a name="devops-management-and-optimization"></a>DevOps, gestion et optimisation
Hello world de devops, la gestion et l’optimisation est très vaste et change très rapidement, vous devez envisager liste hello sous un point de départ.

* [Vidéo : Azure Virtual Machines : Using Chef, Puppet and Docker for managing Linux VMs (Utilisation de Chef, Puppet et Docker pour la gestion des machines virtuelles Linux)](https://azure.microsoft.com/blog/2014/12/15/azure-virtual-machines-using-chef-puppet-and-docker-for-managing-linux-vms/)
* [Terminer le déploiement de cluster guide tooautomated Kubernetes avec CoreOS et tressé](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
* [Visualiseur Kubernetes](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [Plug-in Jenkins Slave pour Azure](http://msopentech.com/blog/2014/09/23/announcing-jenkins-slave-plugin-azure/)
* [Référentiel GitHub : Plug-in Jenkins Storage pour Azure](https://github.com/jenkinsci/windows-azure-storage-plugin)
* [Tiers : Plug-in Hudson Slave pour Azure](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
* [Tiers : Plug-in Hudson Storage pour Azure](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [Vidéo : Description et fonctionnement de Chef](https://msopentech.com/blog/2014/03/31/using-chef-to-manage-azure-resources/)
* [Vidéo : Comment tooUse Azure Automation avec les machines virtuelles Linux](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* [Blog : Comment toodo DSC Powershell pour Linux](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
* [GitHub : Configuration d’état souhaité du client Docker](https://github.com/anweiss/DockerClientDSC)
* [Plug-in Packer pour Azure](https://github.com/msopentech/packer-azure)

