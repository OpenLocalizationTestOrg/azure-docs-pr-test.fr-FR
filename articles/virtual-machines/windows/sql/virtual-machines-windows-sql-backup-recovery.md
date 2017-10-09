---
title: aaaBackup et de restauration pour SQL Server | Documents Microsoft
description: "Décrit les considérations relatives à la sauvegarde et à la restauration des bases de données SQL Server s’exécutant sur des machines virtuelles Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-management
ms.assetid: 95a89072-0edf-49b5-88ed-584891c0e066
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 11/15/2016
ms.author: mikeray
ms.openlocfilehash: f85248fecdd5867d91d09650a1a34ad7c7caa920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore-for-sql-server-in-azure-virtual-machines"></a>Sauvegarde et restauration de SQL Server dans les machines virtuelles Azure
## <a name="overview"></a>Vue d'ensemble
Le stockage Azure conserve 3 copies de chaque machine virtuelle Azure disque tooguarantee contre une perte de données ou une altération des données physiques. Par conséquent, contrairement aux localement, vous n’avez pas besoin tooworry sur ces. Toutefois, vous devez sauvegarder toujours votre tooprotect de bases de données SQL Server contre les erreurs d’application ou un utilisateur (par exemple, l’insertion de données est incorrect ou la suppression d’une table) et être en mesure de toorestore tooa point dans le temps.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

Pour SQL Server est en cours d’exécution dans des machines virtuelles Azure, vous pouvez utiliser la sauvegarde en mode natif et restaurer les techniques à l’aide de disques attachés pour la destination hello hello des fichiers de sauvegarde. Toutefois, a un toohello limiter le nombre de disques que vous pouvez attacher tooan machine virtuelle Azure, en fonction de hello [taille de machine virtuelle de hello](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Il existe également une surcharge de hello de tooconsider de gestion de disque.

À partir de SQL Server 2014, vous pouvez sauvegarder et restaurer le stockage d’objets Blob Azure tooMicrosoft. SQL Server 2016 apporte également des améliorations pour cette option. Par ailleurs, pour les fichiers de base de données stockés dans le stockage d’objets blob Microsoft Azure, SQL Server 2016 propose une option pour effectuer des sauvegardes quasi instantanées et des restaurations rapides à l’aide d’instantanés Azure. Cet article fournit une vue d’ensemble de ces options. Pour plus d’informations, consultez [Sauvegarde et restauration SQL Server avec le service Stockage Blob Microsoft Azure](https://msdn.microsoft.com/library/jj919148.aspx).

> [!NOTE]
> Pour en savoir plus sur les options de hello pour la sauvegarde des bases de données très volumineuses, consultez [stratégies de sauvegarde de base de données de plusieurs téraoctets SQL Server pour les Machines virtuelles Azure](http://blogs.msdn.com/b/igorpag/archive/2015/07/28/multi-terabyte-sql-server-database-backup-strategies-for-azure-virtual-machines.aspx).
> 
> 

les sections de Hello ci-dessous fournissent des informations spécifiques toohello différentes versions de SQL Server prises en charge dans une machine virtuelle Azure.

## <a name="sql-server-virtual-machines"></a>Machines virtuelles SQL Server
Lorsque votre instance SQL Server est en cours d’exécution sur une machine virtuelle Azure, vos fichiers de base de données se trouvent déjà sur les disques de données dans Azure. Ces disques se situent dans le stockage d’objets blob Azure. Par conséquent, les raisons hello pour la sauvegarde de vos solutions de base de données et hello que vous déconnecter changer légèrement. Considérez les éléments suivants de hello. 

* Vous n’avez plus besoin tooperform de base de données des sauvegardes tooprovide une protection contre les défaillances de matériel ou de support, car Microsoft Azure fournit cette protection en tant que partie de hello service Microsoft Azure.
* Vous devez toujours tooperform base de données des sauvegardes tooprovide protection contre les erreurs de l’utilisateur ou à des fins d’archivage, des raisons réglementaires ou à des fins d’administration.
* Vous pouvez stocker le fichier de sauvegarde hello directement dans Azure. Pour plus d’informations, consultez hello les sections qui fournissent des conseils pour hello différentes versions de SQL Server suivantes.

## <a name="sql-server-2016"></a>SQL Server 2016
Microsoft SQL Server 2016 prend en charge les fonctionnalités de [sauvegarde et de restauration d’objets blob Azure](https://msdn.microsoft.com/library/jj919148.aspx) disponibles dans SQL Server 2014. Mais il inclut également hello suivant améliorations :

| Améliorations en 2016 | Détails |
| --- | --- |
| **Entrelacement** |Lorsque vous sauvegardez tooMicrosoft stockage d’objets blob Azure, SQL Server 2016 prend en charge la sauvegarde tooenable d’objets BLOB toomultiple sauvegarde des bases de données volumineuses, les tooa jusqu'à 12,8 To. |
| **Sauvegarde instantanée** |Via l’utilisation de hello d’instantanés Azure, la sauvegarde d’instantanés de fichier SQL Server fournit des sauvegardes quasi instantanées et des restaurations pour les fichiers de base de données stockées à l’aide du service de stockage d’objets Blob Azure hello. Cette fonctionnalité permet de vous toosimplify vos stratégies de sauvegarde et de restauration. La sauvegarde instantanée de fichier prend également en charge la limite de restauration dans le temps. Pour plus d'informations, consultez [File-Snapshot Backups for Database Files in Azure](https://msdn.microsoft.com/library/mt169363%28v=sql.130%29.aspx)(en anglais). |
| **Planification de sauvegarde gérée** |Sauvegarde managée SQL Server tooAzure prend désormais en charge des planifications personnalisées. Pour plus d’informations, consultez [tooMicrosoft de sauvegarde managée SQL Server Azure](https://msdn.microsoft.com/library/dn449496.aspx). |

Pour obtenir un didacticiel de fonctionnalités hello de SQL Server 2016, l’utilisation du stockage d’objets Blob Azure, consultez [didacticiel : à l’aide du service de stockage d’objets Blob Microsoft Azure hello avec les bases de données SQL Server 2016](https://msdn.microsoft.com/library/dn466438.aspx).

## <a name="sql-server-2014"></a>SQL Server 2014
SQL Server 2014 inclut hello suivant améliorations :

1. **Sauvegarde et restauration tooAzure**:
   
   * *Sauvegarde SQL Server tooURL* prend désormais en charge dans SQL Server Management Studio. tooback d’option Hello des tooAzure est désormais disponible lors de l’utilisation de la tâche de sauvegarde ou de restauration ou Assistant plan de maintenance dans SQL Server Management Studio. Pour plus d’informations, consultez [tooURL de sauvegarde SQL Server](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx).
   * *Sauvegarde managée SQL Server tooAzure* a une nouvelle fonctionnalité qui permet la gestion de sauvegarde automatisée. Cela est particulièrement utile pour automatiser la gestion des sauvegardes pour les instances SQL Server 2014 s’exécutant sur une machine virtuelle Azure. Pour plus d’informations, consultez [tooMicrosoft de sauvegarde managée SQL Server Azure](https://msdn.microsoft.com/library/dn449496%28v=sql.120%29.aspx).
   * *Sauvegarde automatisée* fournit une automatisation supplémentaire tooautomatically activer *sauvegarde managée SQL Server tooAzure* sur toutes les bases de données existantes et nouvelles pour une machine virtuelle SQL Server dans Azure. Pour plus d’informations, voir [Sauvegarde automatisée pour SQL Server dans les machines virtuelles Azure](virtual-machines-windows-sql-automated-backup.md).
   * Pour une vue d’ensemble de toutes les options hello tooAzure de sauvegarde de SQL Server 2014, consultez [SQL Server sauvegarde et restauration avec Microsoft Azure Blob Storage Service](https://msdn.microsoft.com/library/jj919148%28v=sql.120%29.aspx).
2. **Chiffrement**: SQL Server 2014 prend en charge le chiffrement des données lors de la création d’une sauvegarde. Il prend en charge plusieurs algorithmes de chiffrement et hello utiliser osf un certificat ou une clé asymétrique. Pour plus d’informations, voir [Chiffrement de sauvegarde](https://msdn.microsoft.com/library/dn449489%28v=sql.120%29.aspx).

## <a name="sql-server-2012"></a>SQL Server 2012
Pour plus d'informations sur la sauvegarde et la restauration dans SQL Server 2012, consultez [Backup and Restore of SQL Server Databases (SQL Server 2012)](https://msdn.microsoft.com/library/ms187048%28v=sql.110%29.aspx)(en anglais).

À compter de SQL Server 2012 SP1 Cumulative Update 2, vous pouvez sauvegarder des tooand restauration à partir de hello service de stockage d’objets Blob Azure. Cette amélioration peut être utilisé tooback des bases de données SQL Server sur un serveur SQL Server s’exécutant sur une Machine virtuelle Azure ou une instance locale. Pour plus d’informations, voir [SQL Server Backup and Restore with Azure Blob Storage Service](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx)(en anglais).

Quelques-uns des avantages hello de service de stockage d’objets Blob Azure hello hello capacité toobypass hello 16 limite de disque pour les disques attachés, facilité de gestion, la disponibilité directe de hello d’instance de tooanother hello fichier de sauvegarde de l’instance de SQL Server s’exécutant sur Azure machine virtuelle, ou une instance locale pour la récupération d’urgence ou de migration. Pour obtenir une liste complète des avantages toousing un service de stockage d’objets blob Azure pour les sauvegardes de SQL Server, consultez hello *avantages* section [SQL Server sauvegarde et restauration avec le Service de stockage d’objets Blob Azure](https://msdn.microsoft.com/library/jj919148%28v=sql.110%29.aspx).

Pour prendre connaissance des recommandations et des informations de dépannage, voir [Backup and Restore Best Practices (Azure Blob Storage Service)](https://msdn.microsoft.com/library/jj919149%28v=sql.110%29.aspx)(en anglais).

## <a name="sql-server-2008"></a>SQL Server 2008
Pour la sauvegarde et la restauration de SQL Server dans SQL Server 2008 R2, voir [Sauvegarde et restauration de bases de données dans SQL Server (SQL Server 2008 R2)](https://msdn.microsoft.com/library/ms187048%28v=sql.105%29.aspx).

Pour la sauvegarde et la restauration de SQL Server dans SQL Server 2008, voir [Sauvegarde et restauration de bases de données dans SQL Server (SQL Server 2008)](https://msdn.microsoft.com/library/ms187048%28v=sql.100%29.aspx).

## <a name="next-steps"></a>Étapes suivantes
Si vous planifiez votre déploiement de SQL Server dans une machine virtuelle Azure, vous trouverez des conseils de configuration hello suivant le didacticiel : [approvisionnement d’une Machine virtuelle de SQL Server sur Azure avec Azure Resource Manager](virtual-machines-windows-portal-sql-server-provision.md).

Bien que la sauvegarde et de restauration peut être utilisé toomigrate vos données, il existe potentiellement plus facile tooSQL données migration chemins d’accès serveur sur une machine virtuelle Azure. Pour obtenir une description complète des options de migration et des recommandations, consultez [migrer une base de données de tooSQL Server sur une machine virtuelle Azure](virtual-machines-windows-migrate-sql.md).

Passez en revue les autres [ressources liées à l’exécution de SQL Server dans des machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).

