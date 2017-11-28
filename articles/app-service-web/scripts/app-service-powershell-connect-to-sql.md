---
title: "aaaAzure exemple de Script PowerShell - se connecter à une base de données SQL de web application tooa | Documents Microsoft"
description: "Script Azure PowerShell exemple - se connecter à une base de données SQL de tooa application web"
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
ms.openlocfilehash: 8f80b940378d020cbcaec2c1bbc28bae1a3ef35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-sql-database"></a><span data-ttu-id="872fd-103">Se connecter à une base de données SQL de tooa application web</span><span class="sxs-lookup"><span data-stu-id="872fd-103">Connect a web app tooa SQL database</span></span>

<span data-ttu-id="872fd-104">Dans ce scénario, vous allez apprendre comment toocreate une base de données SQL Azure et Azure web app.</span><span class="sxs-lookup"><span data-stu-id="872fd-104">In this scenario you will learn how toocreate an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="872fd-105">Ensuite, vous allez lier hello SQL de base de données toohello l’application web à l’aide des paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="872fd-105">Then you will link hello SQL database toohello web app using app settings.</span></span>

<span data-ttu-id="872fd-106">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](/powershell/azure/overview), puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="872fd-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="872fd-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="872fd-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connect a web app tooa SQL database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="872fd-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="872fd-108">Clean up deployment</span></span> 

<span data-ttu-id="872fd-109">Après exécution de l’exemple de script hello, hello commande suivante peut être groupe de ressources hello tooremove utilisé, l’application web et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="872fd-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="872fd-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="872fd-110">Script explanation</span></span>

<span data-ttu-id="872fd-111">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="872fd-111">This script uses hello following commands.</span></span> <span data-ttu-id="872fd-112">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="872fd-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="872fd-113">Commande</span><span class="sxs-lookup"><span data-stu-id="872fd-113">Command</span></span> | <span data-ttu-id="872fd-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="872fd-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="872fd-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="872fd-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="872fd-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="872fd-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="872fd-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="872fd-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="872fd-118">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="872fd-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="872fd-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="872fd-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="872fd-120">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="872fd-120">Creates a web app.</span></span> |
| [<span data-ttu-id="872fd-121">New-AzureRMSQLServer</span><span class="sxs-lookup"><span data-stu-id="872fd-121">New-AzureRMSQLServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="872fd-122">Crée un serveur SQL Database.</span><span class="sxs-lookup"><span data-stu-id="872fd-122">Creates a SQL Database server.</span></span> |
| [<span data-ttu-id="872fd-123">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="872fd-123">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="872fd-124">Crée une règle de pare-feu de serveur SQL Database.</span><span class="sxs-lookup"><span data-stu-id="872fd-124">Creates a firewall rule for a SQL Database server.</span></span> |
| [<span data-ttu-id="872fd-125">New-AzureRMSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="872fd-125">New-AzureRMSQLDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="872fd-126">Crée une base de données ou une base de données élastique.</span><span class="sxs-lookup"><span data-stu-id="872fd-126">Creates a database or an elastic database.</span></span> |
| [<span data-ttu-id="872fd-127">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="872fd-127">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="872fd-128">Modifie la configuration d’une application web.</span><span class="sxs-lookup"><span data-stu-id="872fd-128">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="872fd-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="872fd-129">Next steps</span></span>

<span data-ttu-id="872fd-130">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="872fd-130">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="872fd-131">Vous trouverez des exemples supplémentaires de Azure Powershell pour Azure App Service Web Apps Bonjour [exemples Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="872fd-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
