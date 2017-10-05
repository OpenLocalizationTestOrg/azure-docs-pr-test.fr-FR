---
title: "Désinstaller l’outil de tâche de base de données élastique"
description: "Désinstaller l’outil de tâche de base de données élastique"
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
ms.openlocfilehash: ae7f0bce452a0a86f6f1e4d9b0c93a0fa1727f21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="uninstall-elastic-database-jobs-components"></a><span data-ttu-id="6362b-103">Désinstallation des composants de Tâches de bases de données élastiques.</span><span class="sxs-lookup"><span data-stu-id="6362b-103">Uninstall Elastic Database jobs components</span></span>
<span data-ttu-id="6362b-104">**Tâches de bases de données élastiques** peuvent être désinstallés à l'aide du portail ou de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6362b-104">**Elastic Database jobs** components can be uninstalled using either the Portal or PowerShell.</span></span>

## <a name="uninstall-elastic-database-jobs-components-using-the-azure-portal"></a><span data-ttu-id="6362b-105">Désinstallez les composants de Tâches de bases de données élastiques à l'aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="6362b-105">Uninstall Elastic Database jobs components using the Azure portal</span></span>
1. <span data-ttu-id="6362b-106">Ouvrez le [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6362b-106">Open the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="6362b-107">Accédez à l'abonnement qui contient les composants de **Tâches de bases de données élastiques** , à savoir l'abonnement dans lequel les composants de Tâches de bases de données élastiques ont été installés.</span><span class="sxs-lookup"><span data-stu-id="6362b-107">Navigate to the subscription that contains **Elastic Database jobs** components, namely the subscription in which Elastic Database jobs components were installed.</span></span>
3. <span data-ttu-id="6362b-108">Cliquez sur **Parcourir**, puis sur **Groupes de ressources**.</span><span class="sxs-lookup"><span data-stu-id="6362b-108">Click **Browse** and click **Resource groups**.</span></span>
4. <span data-ttu-id="6362b-109">Sélectionnez le groupe de ressources intitulé « __ElasticDatabaseJob ».</span><span class="sxs-lookup"><span data-stu-id="6362b-109">Select the resource group named "__ElasticDatabaseJob".</span></span>
5. <span data-ttu-id="6362b-110">Supprimez le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="6362b-110">Delete the resource group.</span></span>

## <a name="uninstall--elastic-database-jobs-components-using-powershell"></a><span data-ttu-id="6362b-111">Désinstallez les composants de Tâches de bases de données élastiques à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="6362b-111">Uninstall  Elastic Database jobs components using PowerShell</span></span>
1. <span data-ttu-id="6362b-112">Lancez une fenêtre de commande Microsoft Azure PowerShell et accédez au sous-répertoire des outils, sous le dossier Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x : tapez **cd tools**.</span><span class="sxs-lookup"><span data-stu-id="6362b-112">Launch a Microsoft Azure PowerShell command window and navigate to the tools sub-directory under the Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x folder: Type **cd tools**.</span></span>
   
     <span data-ttu-id="6362b-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span><span class="sxs-lookup"><span data-stu-id="6362b-113">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*>cd tools</span></span>
2. <span data-ttu-id="6362b-114">Exécutez le script PowerShell .\UninstallElasticDatabaseJobs.ps1.</span><span class="sxs-lookup"><span data-stu-id="6362b-114">Execute the .\UninstallElasticDatabaseJobs.ps1 PowerShell script.</span></span>
   
     <span data-ttu-id="6362b-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span><span class="sxs-lookup"><span data-stu-id="6362b-115">PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>Unblock-File .\UninstallElasticDatabaseJobs.ps1   PS C:\*Microsoft.Azure.SqlDatabase.Jobs.x.x.xxxx.x*\tools>.\UninstallElasticDatabaseJobs.ps1</span></span>

<span data-ttu-id="6362b-116">Ou exécutez simplement le script suivant, en supposant que les valeurs par défaut ont été utilisées pour l'installation des composants :</span><span class="sxs-lookup"><span data-stu-id="6362b-116">Or simply, execute the following script, assuming default values where used on installation of the components:</span></span>

        $ResourceGroupName = "__ElasticDatabaseJob"
        Switch-AzureMode AzureResourceManager

        $resourceGroup = Get-AzureResourceGroup -Name $ResourceGroupName
        if(!$resourceGroup)
        {
            Write-Host "The Azure Resource Group: $ResourceGroupName has already been deleted.  Elastic database job components are uninstalled."
            return
        }

        Write-Host "Removing the Azure Resource Group: $ResourceGroupName.  This may take a few minutes.”
        Remove-AzureResourceGroup -Name $ResourceGroupName -Force
        Write-Host "Completed removing the Azure Resource Group: $ResourceGroupName.  Elastic database job compoennts are now uninstalled."

## <a name="next-steps"></a><span data-ttu-id="6362b-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6362b-117">Next steps</span></span>
<span data-ttu-id="6362b-118">Pour réinstaller les tâches de bases de données élastiques, consultez [Installation du service de Tâche de bases de données élastiques](sql-database-elastic-jobs-service-installation.md)</span><span class="sxs-lookup"><span data-stu-id="6362b-118">To re-install Elastic Database jobs, see [Installing the Elastic Database job service](sql-database-elastic-jobs-service-installation.md)</span></span>

<span data-ttu-id="6362b-119">Pour plus d’informations concernant les tâches de bases de données élastiques, consultez la rubrique [Vue d’ensemble des tâches de bases de données élastiques](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6362b-119">For an overview of Elastic Database jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span>

<!--Image references-->


