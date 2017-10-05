---
title: "Exemple PowerShell-Créer une base de données SQL Azure | Microsoft Docs"
description: "Exemple de script Azure PowerShell pour créer une base de données SQL Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 1b6809007e6717b7f8847452b2fa5b38d4ab5ccc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-create-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="f1590-103">Utiliser PowerShell pour créer une base de données SQL Azure et configurer une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="f1590-103">Use PowerShell to create a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="f1590-104">Cet exemple de script PowerShell crée une base de données SQL Azure et configure une règle de pare-feu au niveau du serveur.</span><span class="sxs-lookup"><span data-stu-id="f1590-104">This PowerShell script example creates an Azure SQL database and configures a server-level firewall rule.</span></span> <span data-ttu-id="f1590-105">Une fois que le script a été exécuté avec succès, l’instance SQL Database est accessible à partir de tous les services Azure et l’adresse IP configurée.</span><span class="sxs-lookup"><span data-stu-id="f1590-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="f1590-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="f1590-106">Sample script</span></span>

<span data-ttu-id="f1590-107">[!code-powershell[principal](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Créer une instance SQL Database")]</span><span class="sxs-lookup"><span data-stu-id="f1590-107">[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f1590-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="f1590-108">Clean up deployment</span></span>

<span data-ttu-id="f1590-109">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="f1590-109">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="f1590-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="f1590-110">Script explanation</span></span>

<span data-ttu-id="f1590-111">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="f1590-111">This script uses the following commands.</span></span> <span data-ttu-id="f1590-112">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="f1590-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f1590-113">Commande</span><span class="sxs-lookup"><span data-stu-id="f1590-113">Command</span></span> | <span data-ttu-id="f1590-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="f1590-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f1590-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f1590-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f1590-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="f1590-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f1590-117">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="f1590-117">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="f1590-118">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="f1590-118">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="f1590-119">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="f1590-119">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="f1590-120">Crée une règle de pare-feu pour autoriser l’accès à toutes les instances SQL Database sur le serveur à partir de la plage d’adresses IP entrée.</span><span class="sxs-lookup"><span data-stu-id="f1590-120">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="f1590-121">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="f1590-121">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="f1590-122">Crée une base de données unique ou mise en pool au sein d’un serveur logique.</span><span class="sxs-lookup"><span data-stu-id="f1590-122">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="f1590-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f1590-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="f1590-124">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="f1590-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="f1590-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f1590-125">Next steps</span></span>

<span data-ttu-id="f1590-126">Pour plus d’informations sur Azure PowerShell, consultez la [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f1590-126">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f1590-127">Vous trouverez des exemples supplémentaires de scripts SQL Database PowerShell sur la page [Scripts PowerShell Azure SQL Database](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f1590-127">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>



