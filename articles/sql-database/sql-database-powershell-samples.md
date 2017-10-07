---
title: "exemples de script PowerShell aaaAzure pour la base de données SQL | Documents Microsoft"
description: "Azure PowerShell script exemples toohelp vous créez et gérez les serveurs de base de données SQL Azure, pools élastiques, bases de données et les pare-feu."
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: overview-samples
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 1130ffb0e1c2b94c676d564ad5c4eb3b86374dbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-azure-sql-database"></a>Exemples Azure PowerShell pour Azure SQL Database

Hello tableau suivant inclut des liens toosample Azure scripts PowerShell pour la base de données SQL Azure.

| |  |
|---|---|
|**Créer une base de données unique et un pool élastique**||
| [Créer une base de données unique et configurer une règle de pare-feu](scripts/sql-database-create-and-configure-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Ce script PowerShell crée une base de données SQL Azure unique et configure une règle de pare-feu au niveau du serveur. |
| [Créer des pools élastiques et déplacer les bases de données regroupées](scripts/sql-database-move-database-between-pools-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Ce script PowerShell crée des pools élastiques Azure SQL Database, déplace des bases de données mises en pool et modifie les niveaux de performances.|
|**Configurer la géoréplication et le basculement**||
| [Configurer et basculer une base de données unique à l’aide de la géoréplication active](scripts/sql-database-setup-geodr-and-failover-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Ce script PowerShell configure géo-réplication active pour une base de données SQL Azure et il échoue sur un réplica secondaire de toohello. |
| [Configurer et basculer une base de données regroupée à l’aide de la géoréplication active](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Ce script PowerShell configure géo-réplication active pour une base de données SQL Azure dans un pool élastique SQL et il bascule de réplica secondaire de toohello. |
| [Configurer et basculer un groupe de basculement pour une base de données unique (préversion)](scripts/sql-database-setup-geodr-failover-database-failover-group-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Ce script PowerShell configure un groupe de basculement pour une instance de serveur de base de données SQL Azure, ajoute un groupe de basculement de toohello de base de données et il échoue sur un serveur secondaire de toohello |
|**Mettre à l’échelle une base de données unique et un pool élastique**||
| [Mettre à l’échelle une base de données unique](scripts/sql-database-monitor-and-scale-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Ce script PowerShell analyse les métriques de performances hello d’une base de données SQL Azure, il ajuste le niveau de performance supérieur tooa et crée une règle d’alerte sur l’un des métriques de performances hello. |
| [Mettre à l’échelle un pool élastique](scripts/sql-database-monitor-and-scale-pool-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Ce script PowerShell analyse les métriques de performances hello d’un pool élastique de base de données SQL Azure, il ajuste le niveau de performance supérieur tooa et crée une règle d’alerte sur l’un des métriques de performances hello.  |
| **Audit et détection des menaces** |
| [Configurer l’audit et la détection des menaces](scripts/sql-database-auditing-and-threat-detection-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Ce script PowerShell configure les stratégies d’audit et de détection des menaces pour une base de données SQL Azure. |
| **Restaurer, copier et importer une base de données**||
| [Restaurer une base de données](scripts/sql-database-restore-database-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Ce script PowerShell restaure une base de données SQL Azure à partir d’une sauvegarde géo-redondant et restaure une supprimé SQL Azure toohello dernière sauvegarde. |
| [Copier un serveur toonew de base de données](scripts/sql-database-copy-database-to-new-server-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Ce script PowerShell crée une copie d’une base de données SQL Azure existante sur un nouveau serveur SQL Azure. |
| [Importer une base de données à partir d’un fichier bacpac](scripts/sql-database-import-from-bacpac-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| Ce script PowerShell importe un base de données tooan Azure SQL server à partir d’un fichier bacpac. |
| **Synchroniser des données entre des bases de données**||
| [Synchroniser des données entre des bases de données SQL](scripts/sql-database-sync-data-between-sql-databases.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Ce script PowerShell configure toosync de synchronisation des données entre plusieurs bases de données SQL Azure. |
| [Synchroniser des données entre une base de données SQL et un serveur SQL local](scripts/sql-database-sync-data-between-azure-onprem.md?toc=%2fpowershell%2fmodule%2ftoc.json) | Ce script PowerShell configure toosync de synchronisation des données entre une base de données SQL Azure et une base de données SQL Server locale. |
|||
|||
