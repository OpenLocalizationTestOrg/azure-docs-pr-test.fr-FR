---
title: "Migrer une base de données SQL Server vers SQL Server sur une machine virtuelle | Microsoft Docs"
description: "Découvrez comment migrer une base de données utilisateur sur site de SQL Server dans une machine virtuelle Azure."
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
ms.openlocfilehash: 68767534298783083a441aa295611914d0df9db0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="migrate-a-sql-server-database-to-sql-server-in-an-azure-vm"></a>Migrer une base de données SQL Server vers SQL Server dans une machine virtuelle Azure

Il existe plusieurs méthodes permettant de migrer une base de données utilisateur SQL Server locale vers SQL Server sur une machine virtuelle Azure. Cet article abordera brièvement différentes méthodes et recommandera la mieux adaptée à différents scénarios.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="what-are-the-primary-migration-methods"></a>Quelles sont les principales méthodes de migration ?
Les méthodes de migration principales consistent à :

* Effectuer une sauvegarde locale par compression et copier manuellement le fichier de sauvegarde dans la machine virtuelle Azure
* Effectuer une sauvegarde vers une URL et exécuter une restauration dans la machine virtuelle Azure à partir de cette URL
* Détacher, puis copier les fichiers journaux et de données vers le stockage d’objets blob Azure, puis les rattacher à SQL Server dans la machine virtuelle Azure depuis une URL
* Convertir une machine physique locale en disque dur virtuel Hyper-V, effectuer un téléchargement vers le stockage d’objets Blob Azure, puis exécuter un déploiement en tant que nouvelle machine virtuelle en utilisant le disque dur virtuel téléchargé
* Expédition du disque dur avec le Service d’importation/exportation Windows
* Si vous disposez d’un déploiement AlwaysOn local, utilisez l’ [Assistant Ajout d’un réplica Azure](../classic/sql-onprem-availability.md) pour créer un réplica dans Azure, puis basculez en dirigeant les utilisateurs vers l’instance de base de données Azure
* Utiliser la [réplication transactionnelle](https://msdn.microsoft.com/library/ms151176.aspx) de SQL Server pour configurer l’instance Azure SQL Server en tant qu’abonné, puis désactiver la réplication en dirigeant les utilisateurs vers l’instance de base de données Azure

> [!TIP]
> Vous pouvez également utiliser ces mêmes techniques pour déplacer des bases de données entre machines virtuelles SQL Server dans Azure. Par exemple, il n’existe aucun moyen pris en charge de mettre à niveau une machine virtuelle d’image de la galerie SQL Server d’une version/édition à l’autre. Dans ce cas, il vous faut créer une nouvelle machine virtuelle SQL Server avec la nouvelle version/édition, puis utiliser l’une des techniques de migration de cet article pour déplacer vos bases de données. 

## <a name="choosing-your-migration-method"></a>Choix de votre méthode de migration
Pour obtenir des performances de transfert de données optimales, migrez les fichiers de base de données de la machine virtuelle Azure à l’aide d’un fichier de sauvegarde compressé.

Pour réduire le temps d’arrêt pendant la migration de base de données, utilisez l’option AlwaysOn ou l’option de réplication transactionnelle.

S’il n’est pas possible d’utiliser les méthodes décrites ci-dessus, migrez manuellement votre base de données. Cette méthode consiste généralement à effectuer une sauvegarde de la base de données, puis une copie de la sauvegarde de la base de données dans Azure, et enfin à effectuer une restauration de la base de données. Vous pouvez également copier les fichiers de base de données eux-mêmes dans Azure, puis les joindre. Il existe plusieurs méthodes permettant d’effectuer manuellement le processus de migration d’une base de données vers une machine virtuelle Azure.

> [!NOTE]
> Lorsque vous procédez à une mise à niveau vers SQL Server 2014 ou SQL Server 2016 depuis des versions antérieures de SQL Server, vous devez prendre en compte les éventuelles modifications nécessaires. Nous vous recommandons de gérer toutes les dépendances de fonctionnalités non prises en charge par la nouvelle version de SQL Server dans le cadre de votre projet de migration. Pour plus d’informations sur les éditions et les scénarios pris en charge, consultez [Mise à niveau vers SQL Server](https://msdn.microsoft.com/library/bb677622.aspx).

Le tableau suivant répertorie les principales méthodes de migration et explique dans quelles circonstances utiliser chacune d’elles.

| Méthode | Version de base de données source | Version de base de données de destination | Contrainte de taille pour la sauvegarde de base de données source | Remarques |
| --- | --- | --- | --- | --- |
| [Effectuer une sauvegarde locale en utilisant la compression et copier manuellement le fichier de sauvegarde dans la machine virtuelle Azure](#backup-and-restore) |SQL Server 2005 ou ultérieur |SQL Server 2005 ou ultérieur |[Limite de stockage de machine virtuelle Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) | Il s’agit d’une technique très simple et éprouvée pour déplacer des bases de données d’une machine à l’autre. |
| [Effectuer une sauvegarde vers l’URL et une restauration dans la machine virtuelle Azure depuis l’URL](#backup-to-url-and-restore) |SQL Server 2012 SP1 CU2 ou ultérieur |SQL Server 2012 SP1 CU2 ou ultérieur |< 12,8 To pour SQL Server 2016, sinon < 1 To | Cette méthode représente simplement une autre façon de déplacer le fichier de sauvegarde sur la machine virtuelle à l’aide du stockage Azure. |
| [Détacher, puis copier les données et les fichiers journaux dans le stockage d’objets blob Azure et les rattacher à SQL Server dans la machine virtuelle Azure à partir d’URL](#detach-and-attach-from-url) |SQL Server 2005 ou ultérieur |SQL Server 2014 ou ultérieur |[Limite de stockage de machine virtuelle Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Utilisez cette méthode quand vous envisagez de [stocker ces fichiers à l’aide du service de stockage d’objets Blob Azure](https://msdn.microsoft.com/library/dn385720.aspx) et de les rattacher à SQL Server s’exécutant dans une machine virtuelle Azure, en particulier avec les bases de données très volumineuses. |
| [Convertir l’ordinateur local pour les disques durs virtuels Hyper-V, charger sur le stockage d’objets Blob Azure, puis déployer une nouvelle machine virtuelle en utilisant le disque dur virtuel chargé](#convert-to-vm-and-upload-to-url-and-deploy-as-new-vm) |SQL Server 2005 ou ultérieur |SQL Server 2005 ou ultérieur |[Limite de stockage de machine virtuelle Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |À utiliser lors de [la mise en service de votre propre licence SQL Server](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md), lors de la migration d’une base de données que vous allez exécuter sur une version plus ancienne de SQL Server, ou lors de la migration d’un système et de bases de données d’un système utilisateur dans le cadre de la migration de base de données dépendant des autres bases de données utilisateur et/ou bases de données système. |
| [Expédition du disque dur à l’aide du Service d’importation/exportation Windows](#ship-hard-drive) |SQL Server 2005 ou ultérieur |SQL Server 2005 ou ultérieur |[Limite de stockage de machine virtuelle Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Utilisez le [Service Import/Export de Windows](../../../storage/common/storage-import-export-service.md) lorsque la méthode de copie manuelle est trop lente, par exemple avec de très grandes bases de données. |
| [Utiliser l’Assistant Ajout d’un réplica Azure](../classic/sql-onprem-availability.md) |SQL Server 2012 ou ultérieur |SQL Server 2012 ou ultérieur |[Limite de stockage de machine virtuelle Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |Réduit le temps d’arrêt ; à utiliser lorsque vous disposez d’un déploiement local AlwaysOn. |
| [Utiliser la réplication transactionnelle de SQL Server](https://msdn.microsoft.com/library/ms151176.aspx) |SQL Server 2005 ou ultérieur |SQL Server 2005 ou ultérieur |[Limite de stockage de machine virtuelle Azure](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |À utiliser si vous devez réduire le temps d’arrêt et que vous ne disposez pas d’un déploiement local AlwaysOn. |

## <a name="backup-and-restore"></a>Sauvegarde et restauration
Sauvegardez votre base de données avec compression, copiez la sauvegarde sur la machine virtuelle, puis restaurez la base de données. Si le volume de votre fichier de sauvegarde est supérieur à 1 To, vous devez le partager parce que la taille maximum d’un disque de machine virtuelle est de 1 To. Utilisez les étapes générales suivantes pour faire migrer une base de données utilisateur à l’aide de cette méthode manuelle :

1. Effectuez une sauvegarde complète de la base de données vers un emplacement sur site.
2. Créez ou téléchargez une machine virtuelle avec la version de SQL Server souhaitée.
3. Configurez la connectivité en fonction de vos besoins. Consultez [Se connecter à une machine virtuelle SQL Server sur Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).
4. Copiez vos fichiers de sauvegarde à votre machine virtuelle à l’aide du Bureau à distance, de l’Explorateur Windows ou de la commande de copie à partir d’une invite de commandes.

## <a name="backup-to-url-and-restore"></a>Sauvegarde vers URL et restauration
Au lieu de sauvegarder dans un fichier local, vous pouvez utiliser la [sauvegarde sur URL](https://msdn.microsoft.com/library/dn435916.aspx), puis effectuer la restauration sur la machine virtuelle à partir de l’URL. Avec SQL Server 2016, les sauvegardes agrégées par bandes sont prises en charge sont recommandés pour les performances et doit dépasser les limites de taille par objet blob. Pour les bases de données très volumineuses, il est recommandé d’utiliser le [Service d’importation/exportation Windows](../../../storage/common/storage-import-export-service.md) .

## <a name="detach-and-attach-from-url"></a>Détacher et attacher à partir d’une URL
Détachez votre base de données et vos fichiers journaux et transférez-les vers le [stockage Blob Azure](https://msdn.microsoft.com/library/dn385720.aspx). Puis attachez la base de données sur votre machine virtuelle Azure à partir de l’URL. Utilisez cette méthode si vous souhaitez que les fichiers de la base de données physique résident dans le stockage Blob. Cela peut être utile pour les bases de données très volumineuses. Utilisez les étapes générales suivantes pour faire migrer une base de données utilisateur à l’aide de cette méthode manuelle :

1. Détachez les fichiers de base de données de l’instance de base de données sur site.
2. Copiez les fichiers de la base de données détachée dans le stockage blob Azure à l’aide de l’ [utilitaire de ligne de commande AZCopy](../../../storage/common/storage-use-azcopy.md).
3. Attachez les fichiers de base de données à partir de l’URL Azure à l’instance de SQL Server dans la machine virtuelle Azure.

## <a name="convert-to-vm-and-upload-to-url-and-deploy-as-new-vm"></a>Effectuez une conversion vers une machine virtuelle et téléchargez vers une URL et déployez en tant que nouvelle machine virtuelle
Cette méthode permet de migrer toutes les bases de données système et utilisateur dans une instance de SQL Server sur site vers une machine virtuelle Azure. Utilisez les étapes générales suivantes pour exécuter la migration d’une instance de SQL Server entière à l’aide de cette méthode manuelle :

1. Convertissez les machines physiques ou virtuelles en disques durs virtuels Hyper-V à l’aide du [Convertisseur Microsoft Virtual Machine](https://technet.microsoft.com/library/dn874008(v=ws.11).aspx).
2. Télécharger les fichiers VHD sur Azure Storage à l’aide de l’ [applet de commande Add-AzureVHD](https://msdn.microsoft.com/library/windowsazure/dn495173.aspx).
3. Déployer une nouvelle machine virtuelle en utilisant le VHD téléchargé.

> [!NOTE]
> Pour migrer une application entière, envisagez d’utiliser [Azure Site Recovery](../../../site-recovery/site-recovery-overview.md)].

## <a name="ship-hard-drive"></a>Livraison de disque dur
Vous pouvez utiliser la [méthode de service Import/Export Azure](../../../storage/common/storage-import-export-service.md) pour transférer de grandes quantités de données de fichiers vers le stockage d’objets blob Azure lorsque le coût de l’opération de téléchargement via le réseau est prohibitif, voire irréalisable. Avec ce service, vous envoyez un ou plusieurs disques durs contenant ces données à un centre de données Azure, où vos données seront téléchargées sur votre compte de stockage.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’exécution de SQL Server sur des machines virtuelles Azure, voir [SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).

Pour obtenir des instructions sur la création d’une machine virtuelle Azure SQL Server à partir d’une image capturée, consultez la page [Tips & Tricks on ‘cloning’ Azure SQL virtual machines from captured images](https://blogs.msdn.microsoft.com/psssql/2016/07/06/tips-tricks-on-cloning-azure-sql-virtual-machines-from-captured-images/) (Trucs et astuces sur le « clonage » des machines virtuelles Azure SQL à partir d’images capturées) du blog des ingénieurs CSS SQL Server.

