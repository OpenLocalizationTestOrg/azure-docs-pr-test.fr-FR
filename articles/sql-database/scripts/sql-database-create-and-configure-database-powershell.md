---
title: "aaaPowerShell la création de l’exemple d’une base de données SQL Azure | Documents Microsoft"
description: "Azure PowerShell exemple script toocreate une base de données SQL Azure"
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
ms.openlocfilehash: ae57b2018f4a550bf2c6da688d6e49bdadf3d3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="903e8-103">Utilisez PowerShell toocreate une base de données SQL Azure et configurer une règle de pare-feu</span><span class="sxs-lookup"><span data-stu-id="903e8-103">Use PowerShell toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="903e8-104">Cet exemple de script PowerShell crée une base de données SQL Azure et configure une règle de pare-feu au niveau du serveur.</span><span class="sxs-lookup"><span data-stu-id="903e8-104">This PowerShell script example creates an Azure SQL database and configures a server-level firewall rule.</span></span> <span data-ttu-id="903e8-105">Une fois l’exécution du script de hello a réussi, hello de que base de données SQL est accessible à partir de tous les services Azure et hello configuré adresse IP.</span><span class="sxs-lookup"><span data-stu-id="903e8-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="903e8-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="903e8-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="903e8-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="903e8-107">Clean up deployment</span></span>

<span data-ttu-id="903e8-108">Après exécution de l’exemple de script hello, hello commande suivante peut être de groupe de ressources utilisé tooremove hello et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="903e8-108">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="903e8-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="903e8-109">Script explanation</span></span>

<span data-ttu-id="903e8-110">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="903e8-110">This script uses hello following commands.</span></span> <span data-ttu-id="903e8-111">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="903e8-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="903e8-112">Commande</span><span class="sxs-lookup"><span data-stu-id="903e8-112">Command</span></span> | <span data-ttu-id="903e8-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="903e8-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="903e8-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="903e8-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="903e8-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="903e8-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="903e8-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="903e8-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="903e8-117">Crée un serveur logique qui héberge une base de données ou un pool élastique.</span><span class="sxs-lookup"><span data-stu-id="903e8-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="903e8-118">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="903e8-118">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="903e8-119">Crée un tooall dans pare-feu règle tooallow accès aux bases de données SQL sur le serveur hello à partir de la plage d’adresses IP hello entré.</span><span class="sxs-lookup"><span data-stu-id="903e8-119">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="903e8-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="903e8-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="903e8-121">Crée une base de données unique ou mise en pool au sein d’un serveur logique.</span><span class="sxs-lookup"><span data-stu-id="903e8-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="903e8-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="903e8-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="903e8-123">Supprime un groupe de ressources, y compris toutes les ressources imbriquées.</span><span class="sxs-lookup"><span data-stu-id="903e8-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="903e8-124">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="903e8-124">Next steps</span></span>

<span data-ttu-id="903e8-125">Pour plus d’informations sur hello Azure PowerShell, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="903e8-125">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="903e8-126">Vous trouverez des exemples supplémentaires de script PowerShell de base de données SQL dans hello [des scripts PowerShell de base de données SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="903e8-126">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>



