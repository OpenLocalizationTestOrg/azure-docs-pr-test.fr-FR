---
title: aaaSAP HANA Azure Backup sur niveau fichier | Documents Microsoft
description: "Il existe deux grandes méthodes permettant d’effectuer des sauvegardes SAP HANA sur des machines virtuelles Azure. Cet article aborde la sauvegarde SAP HANA sur Azure au niveau fichier."
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ums.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 3/13/2017
ms.author: rclaus
ms.openlocfilehash: d5a55de5634ac7724e7fd0fa3760c6c408c3db74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-azure-backup-on-file-level"></a>Sauvegarde SAP HANA sur Azure au niveau fichier

## <a name="introduction"></a>Introduction

Ce document fait partie d’une série d’articles connexes en trois parties dédiés à la sauvegarde SAP HANA. [Guide de sauvegarde pour SAP HANA sur des Machines virtuelles Azure](./sap-hana-backup-guide.md) fournit une vue d’ensemble et des informations sur la prise en main, et [sauvegarde de SAP HANA basée sur des instantanés de stockage](./sap-hana-backup-storage-snapshots.md) couvre hello basée sur un instantané de sauvegarde option de stockage.

En examinant les tailles de machine virtuelle Azure hello, un peut voir qu’un GS5 autorise 64 disques de données attachés. Pour les grands systèmes SAP HANA, un nombre important de disques peut déjà être utilisé pour les données et les fichiers journaux, éventuellement en association avec un RAID logiciel pour un débit d’E/S de disque optimal. question Hello est où toostore SAP HANA sauvegarder les fichiers, ce qui peut se remplir les données de salutation attachée disques au fil du temps ? Consultez [tailles pour les ordinateurs virtuels Linux dans Azure](../../linux/sizes.md) pour les tables de taille de machine virtuelle Azure hello.

Aucune intégration de sauvegarde SAP HANA n’est disponible avec le service Azure Backup pour l’instant. méthode standard de Hello toomanage sauvegarde/restauration au niveau du fichier hello est avec une sauvegarde de fichiers via SAP HANA Studio ou les instructions SQL de HANA SAP. Pour plus d’informations, voir [SQL SAP HANA et référence des vues système](https://help.sap.com/hana/SAP_HANA_SQL_and_System_Views_Reference_en.pdf).

![Cette illustration montre la boîte de dialogue de hello d’élément de menu sauvegarde hello dans SAP HANA Studio](media/sap-hana-backup-file-level/image022.png)

Cette illustration montre la boîte de dialogue de hello d’élément de menu sauvegarde hello dans SAP HANA Studio. Lors du choix du type &quot;fichier&quot; un a toospecify un chemin d’accès dans le système de fichiers hello où SAP HANA écrit les fichiers de sauvegarde hello. Fonctionnement de la restauration hello identique.

Bien que ce choix semble simple et direct, certains points doivent être pris en compte. Comme indiqué précédemment, les machines virtuelles Azure ont une limite en termes de nombre de disques de données qui peuvent être liés. Peut-être capacité toostore SAP HANA fichiers de sauvegarde sur les systèmes de fichiers hello Hello machine virtuelle, selon la taille de hello de hello de base de données et le disque exigences de débit, ce qui peut impliquer des logiciels RAID à l’aide de la répartition entre les données sur plusieurs disques. Plus loin dans cet article, nous aborderons différentes options permettant de déplacer ces fichiers de sauvegarde et de gérer les restrictions concernant la taille des fichiers et les performances lors du traitement de plusieurs téraoctets de données.

Une autre possibilité, qui offre davantage de liberté en ce qui concerne la capacité totale, est le stockage Blob Azure. Lors d’un seul objet blob est également limité too1 to, hello capacité totale d’un conteneur d’objet blob unique est actuellement 500 To. En outre, elle offre aux clients hello un choix tooselect dite &quot;froid&quot; stockage, qui présente un avantage de coût d’objets blob. Pour plus d’informations sur le stockage Blob froid, voir [Stockage Blob Azure : niveaux de stockage chauds et froids](../../../storage/blobs/storage-blob-storage-tiers.md).

Pour une sécurité supplémentaire, utilisez une sauvegarde de stockage avec réplication géographique compte toostore hello SAP HANA. Pour plus d’informations sur la réplication des comptes de stockage, voir [Réplication Azure Storage](../../../storage/common/storage-redundancy.md).

Vous pouvez placer des disques durs virtuels dédiés aux sauvegardes SAP HANA dans un compte de stockage de sauvegarde dédié géo-répliqué. Faute de quoi une pu copier les disques durs virtuels hello conserver les sauvegardes SAP HANA hello compte de stockage avec réplication géographique tooa ou compte de stockage tooa qui se trouve dans une autre région.

## <a name="azure-backup-agent"></a>Agent Azure Backup

Les offres de sauvegarde Azure hello option toonot uniquement sauvegarder complète machines virtuelles, mais également les fichiers et les répertoires via l’agent de sauvegarde hello, qui a toobe installé sur le système d’exploitation invité de hello. Mais à compter de 2016 de décembre, cet agent est prise en charge uniquement Windows (consultez [sauvegarder un tooAzure ou client Windows Server à l’aide du modèle de déploiement du Gestionnaire de ressources hello](../../../backup/backup-configure-vault.md)).

Une solution de contournement est la copie de toofirst tooa de fichiers de sauvegarde SAP HANA Windows VM sur Azure (par exemple, via le partage SAMBA), puis utilisez hello agent de sauvegarde Azure à partir de là. Bien qu’il soit techniquement possible, il serait renforce la complexité et ralentir la sauvegarde de hello ou de restaurer les processus mal en raison de la copie toohello entre hello Linux et hello machine virtuelle Windows. Il n’est pas recommandé toofollow cette approche.

## <a name="azure-blobxfer-utility-details"></a>Détails de l’utilitaire blobxfer Azure

toostore répertoires et fichiers sur le stockage Azure, un peut utiliser CLI ou PowerShell, ou développez un outil à l’aide de hello [kits de développement logiciel Azure](https://azure.microsoft.com/downloads/). Il existe également un utilitaire prêt à l’emploi, AzCopy, pour la copie de stockage des données tooAzure, mais il est Windows uniquement (consultez [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](../../../storage/common/storage-use-azcopy.md)).

Par conséquent, blobxfer a été utilisé pour copier les fichiers de sauvegarde SAP HANA. Il s’agit d’un outil Open Source utilisé par de nombreux clients dans leur environnement de production. Il est disponible sur [GitHub](https://github.com/Azure/blobxfer). Cet outil permet de données toocopy directement tooeither Azure blob storage ou partage de fichiers Azure. Il inclut également de nombreuses fonctionnalités utiles, telles que le code de hachage md5 ou le parallélisme automatique lors de la copie d’un répertoire contenant plusieurs fichiers.

## <a name="sap-hana-backup-performance"></a>Performances de sauvegarde SAP HANA

![Cette capture d’écran est de la console de sauvegarde de SAP HANA hello de SAP HANA Studio](media/sap-hana-backup-file-level/image023.png)

Cette capture d’écran est de la console de sauvegarde de SAP HANA hello de SAP HANA Studio. Sauvegarde de minutes environ 42 toodo hello. durée : Hello 230 Go sur un disque de stockage standard Azure unique jointe toohello HANA VM à l’aide du système de fichiers XFS.

![Cette capture d’écran est de YaST sur la machine virtuelle de test SAP HANA hello](media/sap-hana-backup-file-level/image024.png)

Cette capture d’écran est de YaST sur la machine virtuelle de test SAP HANA hello. Un peut voir hello 1 to seul disque pour la sauvegarde de SAP HANA comme mentionné précédemment. Elle a duré environ 42 minutes toobackup 230 Go. En outre, cinq disques de 200 Go ont été liés et le RAID logiciel md0 a été créé, avec un entrelacement sur ces cinq disques de données Azure.

![Répétition hello même de sauvegarde sur les volumes RAID logiciels l’agrégation par bandes sur cinq de disques de données de stockage standard Azure associés](media/sap-hana-backup-file-level/image025.png)

Hello extensible même de sauvegarde sur les volumes RAID logiciels l’agrégation par bandes sur cinq attaché heure de sauvegarde Azure stockage standard données disques mis hello de 42 minutes vers le bas too10 minutes. les disques Hello ont été attachés sans mise en cache toohello machine virtuelle. Il est donc évident débit d’écriture disque l’importance est pour l’heure de la sauvegarde hello. Un a pu puis commutateur tooAzure premium storage toofurther accélérer hello pour des performances optimales. En général, le stockage Azure Premium doit être utilisé pour les systèmes de production.

## <a name="copy-sap-hana-backup-files-tooazure-blob-storage"></a>Copiez le stockage d’objets blob tooAzure SAP HANA fichiers de sauvegarde

Comme hello mieux de décembre 2016, fichiers de sauvegarde option tooquickly magasin SAP HANA est stockage d’objets blob Azure. Un conteneur d’objet blob unique a une limite de 500 To, suffisante pour la plupart des systèmes SAP HANA, en cours d’exécution dans une machine virtuelle GS5 sur Azure, les sauvegardes SAP HANA suffisamment tookeep. Choix de hello entre les clients ont &quot;à chaud&quot; et &quot;à froid&quot; stockage d’objets blob (voir [stockage d’objets Blob Azure : à chaud et refroidir des niveaux de stockage](../../../storage/blobs/storage-blob-storage-tiers.md)).

L’outil blobxfer hello toocopy facile hello SAP HANA sauvegarde fichiers sont directement tooAzure stockage d’objets blob.

![Ici une peut voir les fichiers de hello d’une sauvegarde de fichier SAP HANA complète](media/sap-hana-backup-file-level/image026.png)

Un trouverez ici des fichiers hello d’une sauvegarde de fichier SAP HANA complète. Il existe quatre fichiers et un plus grand hello a environ 230 Go.

![Elle a duré environ 3 000 secondes toocopy hello 230 Go tooan standard compte blob conteneur de stockage Azure](media/sap-hana-backup-file-level/image027.png)

Utilisez ne pas le hachage md5 dans le test initial de hello, il a fallu environ 3 000 secondes toocopy hello 230 Go tooan standard compte blob conteneur de stockage Azure.

![Dans cette capture d’écran, un peut vérifier son fonctionnement sur hello portail Azure](media/sap-hana-backup-file-level/image028.png)

Dans cette capture d’écran, un peut vérifier son fonctionnement sur hello portail Azure. Un conteneur d’objets blob nommé &quot;sauvegardes de sap hana&quot; a été créé et inclut des blobs hello quatre, qui représentent les fichiers de sauvegarde de SAP HANA hello. L’un d’eux fait environ 230 Go.

console de sauvegarde Hello HANA Studio permet une taille de fichier maximale hello toorestrict HANA des fichiers de sauvegarde. Dans l’environnement d’exemple hello, il des performances accrues en rendant possible toohave les fichiers de sauvegarde plus petit multiples, au lieu d’un seul grand fichier 230 Go.

![Paramètre de limite de taille de fichier de sauvegarde hello sur hello HANA côté n &#39; t améliorer le temps de sauvegarde hello](media/sap-hana-backup-file-level/image029.png)

Paramètre de limite de taille de fichier de sauvegarde hello sur hello HANA côté n &#39; t améliorent les temps de sauvegarde hello, car les fichiers hello sont écrits séquentiellement, comme indiqué dans cette illustration. limite de taille de fichier Hello a été défini too60 Go, afin de la création de la sauvegarde hello quatre fichiers de données volumineux au lieu de 230 Go hello fichier unique.

![tootest le parallélisme de l’outil de blobxfer hello, taille de fichier maximale hello pour les sauvegardes HANA a ensuite été défini too15 Go](media/sap-hana-backup-file-level/image030.png)

tootest le parallélisme de l’outil de blobxfer hello, taille de fichier maximale hello pour les sauvegardes HANA a ensuite été défini too15 Go, ce qui a entraîné des fichiers de sauvegarde 19. Cette configuration mis temps hello pour le stockage d’objets blob tooAzure blobxfer toocopy hello 230 Go à partir de 3 000 secondes too875 secondes.

Ce résultat est dû limite toohello de 60 Mo/s pour l’écriture d’un objet blob Azure. Parallélisme via plusieurs objets BLOB résout goulot d’étranglement hello, mais présente un inconvénient : augmente la performance de hello blobxfer outil toocopy tous les tooAzure de ces fichiers de sauvegarde HANA le stockage d’objets blob place charge sur hello HANA VM et hello réseau. Le fonctionnement du système HANA s’en trouve affecté.

## <a name="blob-copy-of-dedicated-azure-data-disks-in-backup-software-raid"></a>Copie blob des disques de données Azure dédiés dans le RAID logiciel de sauvegarde

Contrairement aux hello manuelle VM données sauvegarde sur disque, dans cette approche ne pas sauvegarder tous les disques de données hello sur une machine virtuelle toosave hello toute installation SAP, y compris les données HANA HANA fichiers journaux et fichiers de configuration. Au lieu de cela, hello idée est toohave dédié les volumes RAID logiciels l’agrégation par bandes sur plusieurs disques durs virtuels de données Azure pour stocker une sauvegarde de fichier SAP HANA. Une copie uniquement ces disques, qui présentent la sauvegarde de SAP HANA hello. Ils pourrait facilement être conservées dans un compte de stockage de sauvegarde HANA dédié ou joint tooa dédié &quot;gestion des ordinateurs virtuels de sauvegarde&quot; pour un traitement ultérieur.

![Tous les disques durs virtuels impliquées ont été copiés à l’aide de hello ** démarrer-azurestorageblobcopy ** commande PowerShell](media/sap-hana-backup-file-level/image031.png)

Après l’exécution de logiciels locaux de sauvegarde toohello hello RAID, tous les disques durs virtuels impliquées ont été copiés à l’aide de hello **start-azurestorageblobcopy** commande PowerShell (voir [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy)). Comme elle n’affecte que le système de fichiers hello dédié pour conserver les fichiers de sauvegarde hello, il n’y a aucun problème sur SAP HANA données ou journaux la cohérence des fichiers sur le disque de hello. L’avantage de cette commande est qu’elle fonctionne tandis que hello machine virtuelle reste en ligne. toobe certain qu’aucun processus n’écrit toohello sauvegarde agrégat, être toounmount vraiment avant hello copie d’objets blob et l’installer à nouveau par la suite. Ou vous pouvez utiliser une trop&quot;Figer&quot; hello du système de fichiers. Par exemple, via xfs\_figer hello XFS système de fichiers.

![Cette capture d’écran montre la liste hello d’objets BLOB dans le conteneur de disques durs virtuels hello sur hello portail Azure](media/sap-hana-backup-file-level/image032.png)

Cette capture d’écran montre la liste hello d’objets BLOB Bonjour &quot;disques durs virtuels&quot; conteneur sur hello portail Azure. capture d’écran de Hello affiche hello cinq disques durs virtuels, qui ont été joints toohello SAP HANA serveur VM tooserve que hello logiciel RAID tookeep SAP HANA fichiers de sauvegarde. Il montre également hello cinq copies, qui ont été effectuées via la commande de copie d’objet blob hello.

![À des fins de test, les copies hello de disques RAID de hello SAP HANA logiciel de sauvegarde ont été toohello joint le serveur application machine virtuelle](media/sap-hana-backup-file-level/image033.png)

À des fins de test, les copies hello de disques RAID de hello SAP HANA logiciel de sauvegarde ont été toohello joint le serveur application machine virtuelle.

![le serveur d’application Hello machine virtuelle a été arrêté tooattach hello disque copies](media/sap-hana-backup-file-level/image034.png)

le serveur d’application Hello machine virtuelle a été arrêté tooattach hello disque copies. Après avoir démarré hello machine virtuelle, des disques hello et hello RAID découverts correctement (monté via UUID). Seul le point de montage hello est manquant, lequel a été créée par le biais de partitionneur YaST hello. Par la suite des copies de fichier de sauvegarde de SAP HANA hello est désormais visibles au niveau du système d’exploitation.

## <a name="copy-sap-hana-backup-files-toonfs-share"></a>Copiez les fichiers de sauvegarde SAP HANA tooNFS partager

toolessen hello impact potentiel sur hello système SAP HANA à partir d’une performance ou une perspective d’espace disque, il peut considérer le stockage des fichiers de sauvegarde SAP HANA hello sur un partage NFS. Techniquement, il fonctionne, mais elle signifie à l’aide d’une deuxième machine virtuelle de Azure en tant qu’hôte hello Hello de partage NFS. Ne doit pas être une petite taille de machine virtuelle, en raison de la bande passante du réseau toohello machine virtuelle. Il serait logique puis tooshut réduire cette &quot;sauvegarde d’ordinateurs virtuels&quot; et uniquement pour l’exécution de la sauvegarde de SAP HANA hello. L’écriture sur un NFS partage place la charge sur le réseau de hello et impacts hello système de SAP HANA, mais simplement la gestion hello des fichiers de sauvegarde par la suite sur hello &quot;sauvegarde VM&quot; influencerait pas système de SAP HANA hello du tout.

![Un partage NFS à partir d’une autre machine virtuelle de Azure a été monté toohello machine virtuelle du serveur SAP HANA](media/sap-hana-backup-file-level/image035.png)

cas d’usage tooverify hello NFS, un partage NFS à partir d’une autre machine virtuelle de Azure a été monté toohello machine virtuelle du serveur SAP HANA. Aucun réglage NFS spécifique n’a été effectué.

![Durée : sauvegarde de 1 heure et 46 minutes toodo hello directement](media/sap-hana-backup-file-level/image036.png)

partage de Hello NFS a été un agrégat rapide comme hello une sur le serveur de SAP HANA hello. Néanmoins, il a fallu 1 heure et hello toodo de 46 minutes sauvegarde directement sur un partage NFS de hello au lieu de 10 minutes, lors de l’écriture du jeu de bandes local de tooa.

![alternative de Hello n’a pas été beaucoup plus rapidement à 1 heure et 43 minutes](media/sap-hana-backup-file-level/image037.png)

alternative Hello effectuant un jeu de bandes local de sauvegarde tooa et la copie de toohello de partage NFS au niveau du système d’exploitation (un simple **cp - avr** commande) n’a pas été beaucoup plus rapidement. Elle a pris 1 heure et 43 minutes.

Il fonctionne, mais les performances n’était pas approprié pour le test de sauvegarde hello 230 Go. La situation serait encore pire pour plusieurs téraoctets.

## <a name="copy-sap-hana-backup-files-tooazure-file-service"></a>Copie les fichiers de sauvegarde de SAP HANA tooAzure service de fichier

Il est possible de toomount un fichier Azure partager à l’intérieur d’une machine virtuelle Linux de Azure. article de Hello [comment toouse stockage Azure files avec Linux](../../../storage/files/storage-how-to-use-files-linux.md) fournit des détails sur la façon de toodo il. N’oubliez pas qu’il existe actuellement une limite de 5 To pour un partage de fichiers Azure, et une limite de taille de fichier de 1 To. Pour plus d’informations sur les limites de stockage, voir [Objectifs de performance et évolutivité du stockage Azure](../../../storage/common/storage-scalability-targets.md).

Des tests ont toutefois démontré que la sauvegarde SAP HANA ne fonctionne pas directement avec ce type de montage CIFS. La [note SAP 1820529](https://launchpad.support.sap.com/#/notes/1820529) indique également que CIFS n’est pas recommandé.

![Cette illustration montre une erreur dans la boîte de dialogue sauvegarde hello dans SAP HANA Studio](media/sap-hana-backup-file-level/image038.png)

Cette illustration présente une erreur dans la boîte de dialogue sauvegarde hello dans SAP HANA Studio, lors de la tentative de tooback directement le partage de fichiers Azure montés CIFS tooa. Ainsi une dispose d’une standard SAP HANA une sauvegarde dans un système de fichiers de machine virtuelle toodo tout d’abord, puis les fichiers de sauvegarde de hello copie à partir de là tooAzure service de fichiers.

![Cette figure montre qu’il a fallu presque 929 secondes toocopy 19 SAP HANA fichiers de sauvegarde](media/sap-hana-backup-file-level/image039.png)

Cette figure montre qu’il a fallu presque 929 secondes toocopy 19 fichiers de sauvegarde SAP HANA avec une taille totale à peu près 230 Go toohello Azure du partage de fichiers.

![structure de répertoire source Hello sur hello SAP HANA VM a été partage de fichiers Azure toohello copiés](media/sap-hana-backup-file-level/image040.png)

Dans cette capture d’écran, un peut voir que structure de répertoire source hello sur hello SAP HANA VM a partage de fichiers Azure toohello copié : un répertoire (hana\_sauvegarde\_personnalisés adaptés\_15 Go) et les fichiers de sauvegarde individuels 19.

Le stockage des fichiers de sauvegarde SAP HANA sur des fichiers Azure peut être une option intéressante Bonjour futures lors de sauvegardes de fichiers SAP HANA prennent en charge directement. Lorsqu’il devient possible toomount Azure fichiers ou via NFS et limite de quota maximale hello est nettement supérieur à 5 To.

## <a name="next-steps"></a>Étapes suivantes
* L’article [Guide de sauvegarde pour SAP HANA sur les machines virtuelles Azure](sap-hana-backup-guide.md) fournit une vue d’ensemble et des informations sur la mise en route.
* [Sauvegarde de SAP HANA basée sur des instantanés de stockage](sap-hana-backup-storage-snapshots.md) décrit l’option sauvegarde basée sur un instantané stockage hello.
* toolearn comment tooestablish haute disponibilité et le plan de récupération d’urgence de SAP HANA sur Azure (instances de grande taille), consultez [SAP HANA (instances de grande taille) haute disponibilité et récupération d’urgence sur Azure](hana-overview-high-availability-disaster-recovery.md).
