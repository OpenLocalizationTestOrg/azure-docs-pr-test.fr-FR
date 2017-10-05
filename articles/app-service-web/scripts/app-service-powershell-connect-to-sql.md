---
title: "Exemple de script Azure PowerShell - Connecter une application web à une instance SQL Database | Microsoft Docs"
description: "Exemple de script Azure PowerShell - Connecter une application web à une instance SQL Database"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 055440a9-fff1-49b2-b964-9c95b364e533
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 5312bf6b81d1cc48490b71c3f77323cca23e1559
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="a4b9c-103">Connecter une application web à une instance SQL Database</span><span class="sxs-lookup"><span data-stu-id="a4b9c-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="a4b9c-104">Dans ce scénario, vous allez apprendre à créer une instance Azure SQL Database et une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="a4b9c-105">Ensuite, vous allez lier l’instance SQL Database à l’application web par le biais des paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-105">Then you will link the SQL database to the web app using app settings.</span></span>

<span data-ttu-id="a4b9c-106">Si nécessaire, installez Azure PowerShell à l’aide des instructions figurant dans le [Guide Azure PowerShell](/powershell/azure/overview), puis exécutez `Login-AzureRmAccount` pour créer une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="a4b9c-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="a4b9c-107">Sample script</span></span>

<span data-ttu-id="a4b9c-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connecter une application web à une instance SQL Database")]</span><span class="sxs-lookup"><span data-stu-id="a4b9c-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connect a web app to a SQL database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a4b9c-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="a4b9c-109">Clean up deployment</span></span> 

<span data-ttu-id="a4b9c-110">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources, l’application web et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="a4b9c-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="a4b9c-111">Script explanation</span></span>

<span data-ttu-id="a4b9c-112">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-112">This script uses the following commands.</span></span> <span data-ttu-id="a4b9c-113">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a4b9c-114">Commande</span><span class="sxs-lookup"><span data-stu-id="a4b9c-114">Command</span></span> | <span data-ttu-id="a4b9c-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="a4b9c-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a4b9c-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a4b9c-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a4b9c-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a4b9c-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="a4b9c-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="a4b9c-119">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="a4b9c-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="a4b9c-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="a4b9c-121">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-121">Creates a web app.</span></span> |
| [<span data-ttu-id="a4b9c-122">New-AzureRMSQLServer</span><span class="sxs-lookup"><span data-stu-id="a4b9c-122">New-AzureRMSQLServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="a4b9c-123">Crée un serveur SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-123">Creates a SQL Database server.</span></span> |
| [<span data-ttu-id="a4b9c-124">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="a4b9c-124">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="a4b9c-125">Crée une règle de pare-feu de serveur SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-125">Creates a firewall rule for a SQL Database server.</span></span> |
| [<span data-ttu-id="a4b9c-126">New-AzureRMSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="a4b9c-126">New-AzureRMSQLDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="a4b9c-127">Crée une base de données ou une base de données élastique.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-127">Creates a database or an elastic database.</span></span> |
| [<span data-ttu-id="a4b9c-128">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="a4b9c-128">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="a4b9c-129">Modifie la configuration d’une application web.</span><span class="sxs-lookup"><span data-stu-id="a4b9c-129">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a4b9c-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a4b9c-130">Next steps</span></span>

<span data-ttu-id="a4b9c-131">Pour plus d’informations sur le module Azure PowerShell, consultez la [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a4b9c-131">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a4b9c-132">Vous trouverez des exemples supplémentaires de scripts Azure PowerShell pour Azure App Service Web Apps sur la page [Azure PowerShell Samples](../app-service-powershell-samples.md) (Exemples Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="a4b9c-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
