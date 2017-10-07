---
title: fichier-Azure SQL database aaaPowerShell exemple-import-bacpac | Documents Microsoft
description: "Vignette d’un fichier bacpac tooimport de script Azure PowerShell exemple dans une base de données SQL"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: b85fca1c7fd52037d74254980469f9f53906448e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooimport-a-bacpac-file-into-an-azure-sql-database"></a>Utilisez PowerShell tooimport un fichier bacpac dans une base de données SQL Azure

Cet exemple de script PowerShell importe dans une base de données SQL Azure, la base de données contenue dans un fichier **Bacpac**.  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a>Exemple de script

[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]

## <a name="clean-up-deployment"></a>Nettoyer le déploiement

Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a>Explication du script

Ce script utilise hello suivant les commandes. Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.

| Commande | Remarques |
|---|---|
| [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Crée un groupe de ressources dans lequel toutes les ressources sont stockées. |
| [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) | Crée un serveur logique que les ordinateurs hôtes hello de base de données SQL. |
| [New-AzureRmSqlServerFirewallRule](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | Crée un tooall dans pare-feu règle tooallow accès aux bases de données SQL sur le serveur hello à partir de la plage d’adresses IP hello entré. |
| [New-AzureRmSqlDatabaseImport](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | Importe un .bacpac fichiers et de créer une nouvelle base de données sur le serveur de hello. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Supprime un groupe de ressources, y compris toutes les ressources imbriquées. |

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](/powershell/azure/overview).

Vous trouverez des exemples supplémentaires de script PowerShell de base de données SQL dans hello [des scripts PowerShell de base de données SQL Azure](../sql-database-powershell-samples.md).
