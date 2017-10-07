---
title: "détection de menace l’audit de l’exemple aaaPowerShell-Azure SQL Database | Documents Microsoft"
description: "Azure PowerShell exemple tooconfigure audit et la menace des scripts dans une base de données SQL Azure"
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
ms.openlocfilehash: 97e057ac6efe5e730404ae796bc01e7e5c70df35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="3ea83-103">Utiliser la détection de l’audit et de la base de données SQL des tooconfigure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ea83-103">Use PowerShell tooconfigure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="3ea83-104">Cet exemple de script PowerShell configure l’audit et la détection des menaces SQL Database.</span><span class="sxs-lookup"><span data-stu-id="3ea83-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="3ea83-105">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="3ea83-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]

## <a name="clean-up-deployment"></a><span data-ttu-id="3ea83-106">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="3ea83-106">Clean up deployment</span></span>

<span data-ttu-id="3ea83-107">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="3ea83-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="3ea83-108">Explication du script</span><span class="sxs-lookup"><span data-stu-id="3ea83-108">Script explanation</span></span>

<span data-ttu-id="3ea83-109">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="3ea83-109">This script uses hello following commands.</span></span> <span data-ttu-id="3ea83-110">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="3ea83-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="3ea83-111">Commande</span><span class="sxs-lookup"><span data-stu-id="3ea83-111">Command</span></span> | <span data-ttu-id="3ea83-112">Remarques</span><span class="sxs-lookup"><span data-stu-id="3ea83-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3ea83-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3ea83-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="3ea83-114">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="3ea83-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3ea83-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="3ea83-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="3ea83-116">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="3ea83-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="3ea83-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="3ea83-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="3ea83-118">Crée une base de données unique ou mise en pool au sein d’un serveur logique.</span><span class="sxs-lookup"><span data-stu-id="3ea83-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="3ea83-119">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="3ea83-119">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="3ea83-120">Crée un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="3ea83-120">Creates a Storage account.</span></span> |
| [<span data-ttu-id="3ea83-121">Set-AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="3ea83-121">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="3ea83-122">Définit la stratégie d’audit hello pour une base de données.</span><span class="sxs-lookup"><span data-stu-id="3ea83-122">Sets hello auditing policy for a database.</span></span> |
| [<span data-ttu-id="3ea83-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="3ea83-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="3ea83-124">Définit une stratégie de détection des menaces sur une base de données.</span><span class="sxs-lookup"><span data-stu-id="3ea83-124">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="3ea83-125">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3ea83-125">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="3ea83-126">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="3ea83-126">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="3ea83-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3ea83-127">Next steps</span></span>

<span data-ttu-id="3ea83-128">Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3ea83-128">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3ea83-129">Vous trouverez des exemples supplémentaires de script PowerShell de base de données SQL dans hello [des scripts PowerShell de base de données SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3ea83-129">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
