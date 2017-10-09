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
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="694ed-103">Désinstallation des composants de Tâches de bases de données élastiques.</span><span class="sxs-lookup"><span data-stu-id="694ed-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="694ed-104">**Les travaux de base de données élastiques** composants peuvent être désinstallés à l’aide de hello portail ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="694ed-104">**Elastic Database jobs** components can be uninstalled using either hello Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-hello-azure-portal"></a><span data-ttu-id="694ed-105">Désinstallation des composants de travaux élastique de base de données à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="694ed-105">Uninstall Elastic Database jobs components using hello Azure portal</span></span>
1. <span data-ttu-id="694ed-106">Ouvrez hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="694ed-106">Open hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="694ed-107">Accédez abonnement toohello contenant **des travaux de base de données élastique** composants, à savoir hello qu’abonnement dans la base de données élastique composants de travaux ont été installés.</span><span class="sxs-lookup"><span data-stu-id="694ed-107">Navigate toohello subscription that contains **Elastic Database jobs** components, namely hello subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="694ed-108">Cliquez sur **Parcourir**, puis sur **Groupes de ressources**.</span><span class="sxs-lookup"><span data-stu-id="694ed-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="694ed-109">Groupe de ressources hello sélectionnez nommé « __ElasticDatabaseJob ».</span><span class="sxs-lookup"><span data-stu-id="694ed-109">Select hello resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="694ed-110">Supprimer le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="694ed-110">Delete hello resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="694ed-111">Désinstallez les composants de Tâches de bases de données élastiques à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="694ed-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="694ed-112">Lancez une fenêtre de commande PowerShell de Microsoft Azure et accédez toohello outils sous-répertoire sous hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x dossier : Type **outils cd**.</span><span class="sxs-lookup"><span data-stu-id="694ed-112">Launch a Microsoft Azure PowerShell command window and navigate toohello tools sub-directory under hello Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="694ed-113">PS C :\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span><span class="sxs-lookup"><span data-stu-id="694ed-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="694ed-114">Exécutez le script PowerShell de.\UninstallElasticDatabaseJobs.ps1 hello.</span><span class="sxs-lookup"><span data-stu-id="694ed-114">Execute hello .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="694ed-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="694ed-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="694ed-116">Ou simplement, exécutez hello script suivant, en supposant que la valeur par défaut les valeurs de cas d’emploi sur l’installation des composants de hello :</span><span class="sxs-lookup"><span data-stu-id="694ed-116">Or simply, execute hello following script, assuming default values where used on installation of hello components:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="694ed-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="694ed-117">Next steps</span></span>
<span data-ttu-id="694ed-118">tâches de base de données élastique toore-installer, consultez [installation du service de travail de base de données élastique hello](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="694ed-118">toore-install Elastic Database jobs, see [Installing hello Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="694ed-119">Pour plus d’informations concernant les tâches de bases de données élastiques, consultez la rubrique [Vue d’ensemble des tâches de bases de données élastiques](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="694ed-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


