---
title: "aaaMigrate un tooSQL de base de données SQL Server Server sur une machine virtuelle | Documents Microsoft"
description: "Découvrez comment toomigrate un utilisateur local de base de données tooSQL Server dans une machine virtuelle Azure."
services: virtual-machines-windows
documentationcenter: 
author: sabotta
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 00fd08c6-98fa-4d62-a3b8-ca20aa5246b1
ms.service: virtual-machines-sql
ms.workload: iaas-sql-server
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: carlasab
ms.openlocfilehash: 9c7aba30304ea40796412d2ddc885f6d4a58be2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-sql-server-database-toosql-server-in-an-azure-vm"></a>Migrer un tooSQL de base de données SQL Server serveur dans une machine virtuelle Azure

Il existe un certain nombre de méthodes toomigrate un tooSQL de base de données utilisateur locale SQL Server serveur dans une machine virtuelle Azure. Cet article sera brièvement traitent des différentes méthodes et recommander hello meilleure méthode pour différents scénarios.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="what-are-hello-primary-migration-methods"></a>Quelles sont les méthodes de migration principal hello ?
méthodes de migration principal Hello sont :

* Effectuer la sauvegarde locale à l’aide de la compression et manuellement le fichier de sauvegarde de copie hello en hello machine virtuelle Azure
* Effectuer une tooURL de sauvegarde et de restauration dans hello machine virtuelle Azure à partir de l’URL de hello
* Et puis copiez hello journaux et des données fichiers tooAzure stockage d’objets blob attacher et détacher puis tooSQL serveur dans la machine virtuelle Azure à partir d’URL
* Convertir physique local VHD tooHyper-V de l’ordinateur, téléchargez le stockage d’objets Blob tooAzure et ensuite déployer la nouvelle machine virtuelle à l’aide de transfert disque dur virtuel
* Expédition du disque dur avec le Service d’importation/exportation Windows
* Si vous avez un déploiement AlwaysOn local, utilisez hello [Assistant Ajouter un réplica](../classic/sql-onprem-availability.md) toocreate un réplica dans Azure, puis pointer l’instance de base de données Azure toohello les utilisateurs de basculement
* Utiliser SQL Server [la réplication transactionnelle](https://msdn.microsoft.com/library/ms151176.aspx) tooconfigure hello Azure SQL Server de l’instance en tant qu’abonné et désactivez la réplication, pointer l’instance de base de données Azure toohello utilisateurs

> [!TIP]
> Vous pouvez également utiliser ces mêmes bases de données toomove techniques entre les machines virtuelles SQL Server dans Azure. Par exemple, il n’existe aucun tooupgrade moyen pris en charge une machine virtuelle image de la galerie de SQL Server à partir d’une édition de la version tooanother. Dans ce cas, vous devez créer une nouvelle machine virtuelle SQL Server avec la nouvelle version/édition de hello, puis utilisez une des techniques de migration hello dans cet article de toomove vos bases de données. 

## <a name="choosing-your-migration-method"></a>Choix de votre méthode de migration
Pour les performances du transfert de données optimal, migrer des fichiers de base de données de hello dans hello Azure VM à l’aide d’un fichier de sauvegarde compressé.

toominimize temps d’arrêt pendant le processus de migration de base de données hello, utilisez l’option d’AlwaysOn hello ou hello la réplication transactionnelle.

Si elle n’est pas hello toouse possible au-dessus de méthodes, migrer manuellement votre base de données. À l’aide de cette méthode, vous démarrez généralement avec une sauvegarde de base de données suivie d’une copie de sauvegarde de base de données hello dans Azure, puis effectuez une restauration de base de données. Vous pouvez également copier les fichiers de base de données hello eux-mêmes dans Azure et définissez-les. Il existe plusieurs méthodes permettant d’effectuer manuellement le processus de migration d’une base de données vers une machine virtuelle Azure.

> [!NOTE]
> Lorsque vous mettez à niveau tooSQL Server 2014 ou SQL Server 2016 à partir de versions antérieures de SQL Server, vous devez envisager si les modifications sont nécessaires. Nous vous recommandons de toutes les dépendances sur les fonctionnalités non prises en charge par hello nouvelle version de SQL Server dans le cadre de votre projet de migration. Pour plus d’informations sur les éditions hello pris en charge et les scénarios, consultez [mise à niveau tooSQL Server](https://msdn.microsoft.com/library/bb677622.aspx).

Hello tableau suivant répertorie chacune des méthodes de migration principal hello et explique quand utiliser chaque méthode hello convient le mieux.

| Méthode | Version de base de données source | Version de base de données de destination | Contrainte de taille pour la sauvegarde de base de données source | Remarques |
| --- | --- | --- | --- | --- |
| [Effectuer la sauvegarde locale à l’aide de la compression et manuellement le fichier de sauvegarde de copie hello en hello machine virtuelle Azure](#backup-and-restore) |SQL Server 2005 ou ultérieur |SQL Server 2005 ou ultérieur |[Limite de stockage de machine virtuelle Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) | Il s’agit d’une technique très simple et éprouvée pour déplacer des bases de données d’une machine à l’autre. |
| [Effectuer une tooURL de sauvegarde et de restauration dans hello machine virtuelle Azure à partir de l’URL de hello](#backup-to-url-and-restore) |SQL Server 2012 SP1 CU2 ou ultérieur |SQL Server 2012 SP1 CU2 ou ultérieur |< 12,8 To pour SQL Server 2016, sinon < 1 To | Cette méthode est simplement une autre façon toomove hello fichier de sauvegarde toohello machine virtuelle à l’aide du stockage Azure. |
| [Et puis copiez hello journaux et des données fichiers tooAzure stockage d’objets blob attacher et détacher puis tooSQL Server dans la machine virtuelle Azure à partir d’URL](#detach-and-attach-from-url) |SQL Server 2005 ou ultérieur |SQL Server 2014 ou ultérieur |[Limite de stockage de machine virtuelle Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Utilisez cette méthode lorsque vous planifiez trop[stocker ces fichiers à l’aide du service de stockage d’objets Blob Azure hello](https://msdn.microsoft.com/library/dn385720.aspx) et définissez-les tooSQL Server en cours d’exécution dans une machine virtuelle Azure, en particulier avec les bases de données très volumineuses. |
| [Convert local disques durs virtuels tooHyper-V de l’ordinateur, téléchargez le stockage d’objets Blob tooAzure et ensuite déployer un ordinateur virtuel à l’aide du disque dur virtuel chargé](#convert-to-vm-and-upload-to-url-and-deploy-as-new-vm) |SQL Server 2005 ou ultérieur |SQL Server 2005 ou ultérieur |[Limite de stockage de machine virtuelle Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Quand utiliser [mettre votre propre licence SQL Server](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md), lors de la migration d’une base de données que vous allez exécuter sur une version antérieure de SQL Server, ou lors de la migration de système et les bases de données utilisateur ensemble dans le cadre de hello migration de base de données dépend d’autres bases de données utilisateur ou des bases de données système. |
| [Expédition du disque dur à l’aide du Service d’importation/exportation Windows](#ship-hard-drive) |SQL Server 2005 ou ultérieur |SQL Server 2005 ou ultérieur |[Limite de stockage de machine virtuelle Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Hello d’utilisation [Service d’importation/exportation Windows](../../../storage/common/storage-import-export-service.md) lorsque la méthode de copie manuelle est trop lente, comme avec les bases de données très volumineuses |
| [Utilisez hello Assistant Ajouter un réplica](../classic/sql-onprem-availability.md) |SQL Server 2012 ou ultérieur |SQL Server 2012 ou ultérieur |[Limite de stockage de machine virtuelle Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Réduit le temps d’arrêt ; à utiliser lorsque vous disposez d’un déploiement local AlwaysOn. |
| [Utiliser la réplication transactionnelle de SQL Server](https://msdn.microsoft.com/library/ms151176.aspx) |SQL Server 2005 ou ultérieur |SQL Server 2005 ou ultérieur |[Limite de stockage de machine virtuelle Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |À utiliser lorsque vous avez besoin de temps d’arrêt toominimize et que vous n’avez pas un déploiement local de AlwaysOn |

## <a name="backup-and-restore"></a>Sauvegarde et restauration
Sauvegardez votre base de données avec la compression, copiez toohello de sauvegarde hello machine virtuelle et puis restaurer la base de données hello. Si votre fichier de sauvegarde est supérieur à 1 To, vous devez la distribuer, car la taille maximale de hello d’un disque de machine virtuelle est de 1 To. Utilisez hello suivant les étapes générales toomigrate une base de données utilisateur à l’aide de cette méthode manuelle :

1. Effectuer un emplacement local de tooan sauvegarde complète de la base de données.
2. Créer ou télécharger une machine virtuelle avec la version de hello de SQL Server souhaité.
3. Configurez la connectivité en fonction de vos besoins. Consultez [connecter tooa Machine virtuelle de SQL Server sur Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).
4. Copiez vos fichiers de sauvegarde de tooyour machine virtuelle à l’aide de la commande à distance copie de bureau, l’Explorateur Windows ou hello à partir d’une invite de commandes.

## <a name="backup-toourl-and-restore"></a>TooURL de sauvegarde et restauration
Au lieu de la sauvegarde de fichier local de tooa, vous pouvez utiliser hello [tooURL sauvegarde](https://msdn.microsoft.com/library/dn435916.aspx) , puis restaurez à partir de l’URL toohello machine virtuelle. Avec SQL Server 2016, les jeux de sauvegarde distribuées sont pris en charge sont recommandés pour des performances et requis des limites de taille hello tooexceed par l’objet blob. Pour les bases de données très volumineuses, hello utilisation de hello [Service d’importation/exportation Windows](../../../storage/common/storage-import-export-service.md) est recommandé.

## <a name="detach-and-attach-from-url"></a>Détacher et attacher à partir d’une URL
Détachez votre base de données et les fichiers journaux et les transfèrent trop[le stockage Blob Azure](https://msdn.microsoft.com/library/dn385720.aspx). Ensuite, attachez de la base de données hello à partir de l’URL de hello sur votre machine virtuelle Azure. Utilisez-le si vous souhaitez que tooreside de fichiers de base de données physique hello dans le stockage Blob. Cela peut être utile pour les bases de données très volumineuses. Utilisez hello suivant les étapes générales toomigrate une base de données utilisateur à l’aide de cette méthode manuelle :

1. Détachez les fichiers de base de données hello à partir de l’instance de base de données locale hello.
2. Copiez les fichiers de base de données détachée de hello dans le stockage d’objets blob Azure à l’aide de hello [utilitaire de ligne de commande AZCopy](../../../storage/common/storage-use-azcopy.md).
3. Permet de joindre des fichiers de base de données de hello d’instance de SQL Server toohello hello URL Azure Bonjour Azure VM.

## <a name="convert-toovm-and-upload-toourl-and-deploy-as-new-vm"></a>Convertir tooVM et tooURL de télécharger et déployer en tant que nouvelle machine virtuelle
Utilisez cette toomigrate méthode toutes les bases de données système et utilisateur dans une machine virtuelle tooAzure d’instance de SQL Server locale. Utilisez hello suivant les étapes générales toomigrate une instance de SQL Server à l’aide de cette méthode manuelle :

1. Conversion physique ou virtuelle machines des disques durs virtuels tooHyper-V à l’aide de [Microsoft Virtual Machine Converter](https://technet.microsoft.com/library/dn874008(v=ws.11).aspx).
2. Télécharger les fichiers de disque dur virtuel tooAzure stockage à l’aide de hello [applet de commande Add-AzureVHD](https://msdn.microsoft.com/library/windowsazure/dn495173.aspx).
3. Déployer une nouvelle machine virtuelle à l’aide de hello téléchargé le disque dur virtuel.

> [!NOTE]
> toomigrate une application entière, envisagez d’utiliser [Azure Site Recovery](../../../site-recovery/site-recovery-overview.md)].

## <a name="ship-hard-drive"></a>Livraison de disque dur
Hello d’utilisation [méthode de Service d’importation/exportation Windows](../../../storage/common/storage-import-export-service.md) tootransfer de grandes quantités de données de fichier tooAzure stockage d’objets Blob dans les situations où le téléchargement via le réseau de hello est prohibitif ou pas possible. Avec ce service, vous envoyez un ou plusieurs disques durs contenant ce centre de données Azure données tooan, où les données seront téléchargement compte de stockage tooyour.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’exécution de SQL Server sur des machines virtuelles Azure, voir [SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).

Pour obtenir des instructions sur la création d’une Machine virtuelle de Azure SQL Server à partir d’une image capturée, consultez [trucs et astuces sur « clonage » des machines virtuelles de SQL Azure à partir d’images capturées](https://blogs.msdn.microsoft.com/psssql/2016/07/06/tips-tricks-on-cloning-azure-sql-virtual-machines-from-captured-images/) sur le blog des ingénieurs du service SQL Server hello.

