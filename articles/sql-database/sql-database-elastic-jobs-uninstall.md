---
title: "outil de travaux aaaHow toouninstall élastique de base de données"
description: "Comment toouninstall hello outil de travaux de base de données élastique"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: bfc9d820-edbd-4fca-bfbf-1f339cfcc448
ms.service: sql-database
ms.workload: sql-database
ms.custom: scale out apps
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 3bc1e889d5042bc3eaa9fd9da89816737e0b8df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a>Désinstallation des composants de Tâches de bases de données élastiques.
**Les travaux de base de données élastiques** composants peuvent être désinstallés à l’aide de hello portail ou PowerShell.

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a>Désinstallation des composants de travaux élastique de base de données à l’aide de hello portail Azure
1. Ouvrez hello [portail Azure](https://portal.azure.com/).
2. Accédez abonnement toohello contenant **des travaux de base de données élastique** composants, à savoir hello qu’abonnement dans la base de données élastique composants de travaux ont été installés.
3. Cliquez sur **Parcourir**, puis sur **Groupes de ressources**.
4. Groupe de ressources hello sélectionnez nommé « __ElasticDatabaseJob ».
5. Supprimer le groupe de ressources hello.

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a>Désinstallez les composants de Tâches de bases de données élastiques à l’aide de PowerShell
1. Lancez une fenêtre de commande PowerShell de Microsoft Azure et accédez toohello outils sous-répertoire sous hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x dossier : Type **outils cd**.
   
     PS C :\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools
2. Exécutez le script PowerShell de.\UninstallElasticDatabaseJobs.ps1 hello.
   
     PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1

Ou simplement, exécutez hello script suivant, en supposant que la valeur par défaut les valeurs de cas d’emploi sur l’installation des composants de hello :

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "hello Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing hello Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing hello Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a>Étapes suivantes
tâches de base de données élastique toore-installer, consultez [installation du service de travail de base de données élastique hello](sql-database-elastic-jobs-service-installation.md)

Pour plus d’informations concernant les tâches de bases de données élastiques, consultez la rubrique [Vue d’ensemble des tâches de bases de données élastiques](sql-database-elastic-jobs-overview.md).

<!--Image references-->


