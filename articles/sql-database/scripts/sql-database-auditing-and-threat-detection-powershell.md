---
title: "Exemple PowerShell-audit-détection des menaces-Azure SQL Database | Microsoft Docs"
description: "Exemple de script Azure PowerShell pour configurer l’audit des bases de données et la détection des menaces dans une base de données Azure SQL"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: e039d35474bff3b066a6605a97e04d4a81c365eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="35639-103">Utiliser PowerShell pour configurer l’audit et la détection des menaces SQL Database</span><span class="sxs-lookup"><span data-stu-id="35639-103">Use PowerShell to configure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="35639-104">Cet exemple de script PowerShell configure l’audit et la détection des menaces SQL Database.</span><span class="sxs-lookup"><span data-stu-id="35639-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="35639-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="35639-105">Sample script</span></span>

<span data-ttu-id="35639-106">[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configurer l’audit et la détection des menaces")]</span><span class="sxs-lookup"><span data-stu-id="35639-106">[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="35639-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="35639-107">Clean up deployment</span></span>

<span data-ttu-id="35639-108">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="35639-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="35639-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="35639-109">Script explanation</span></span>

<span data-ttu-id="35639-110">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="35639-110">This script uses the following commands.</span></span> <span data-ttu-id="35639-111">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="35639-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="35639-112">Commande</span><span class="sxs-lookup"><span data-stu-id="35639-112">Command</span></span> | <span data-ttu-id="35639-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="35639-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="35639-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="35639-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="35639-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="35639-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="35639-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="35639-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="35639-117">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="35639-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="35639-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="35639-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="35639-119">Crée une base de données unique ou mise en pool au sein d’un serveur logique.</span><span class="sxs-lookup"><span data-stu-id="35639-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="35639-120">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="35639-120">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="35639-121">Crée un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="35639-121">Creates a Storage account.</span></span> |
| [<span data-ttu-id="35639-122">Set-AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="35639-122">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="35639-123">Définit la stratégie d’audit d’une base de données.</span><span class="sxs-lookup"><span data-stu-id="35639-123">Sets the auditing policy for a database.</span></span> |
| [<span data-ttu-id="35639-124">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="35639-124">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="35639-125">Définit une stratégie de détection des menaces sur une base de données.</span><span class="sxs-lookup"><span data-stu-id="35639-125">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="35639-126">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="35639-126">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="35639-127">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="35639-127">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="35639-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="35639-128">Next steps</span></span>

<span data-ttu-id="35639-129">Pour plus d’informations sur Azure PowerShell, consultez la [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="35639-129">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="35639-130">Vous trouverez des exemples supplémentaires de scripts SQL Database PowerShell sur la page [Scripts PowerShell Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="35639-130">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
