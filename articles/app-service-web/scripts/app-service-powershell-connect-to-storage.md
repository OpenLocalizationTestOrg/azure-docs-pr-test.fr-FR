---
title: "Exemple de script Azure PowerShell - Connecter une application web à un compte de stockage | Microsoft Docs"
description: "Exemple de script Azure PowerShell - Connecter une application web à un compte de stockage"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4831bdc-2068-4883-9474-0b34c2e3e255
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 481f3efdb1cbbeba328183da7e320c7e5b819b3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-a-web-app-to-a-storage-account"></a><span data-ttu-id="41a30-103">Connecter une application web à un compte de stockage</span><span class="sxs-lookup"><span data-stu-id="41a30-103">Connect a web app to a storage account</span></span>

<span data-ttu-id="41a30-104">Dans ce scénario, vous allez apprendre à créer un compte de stockage Azure et une application web Azure.</span><span class="sxs-lookup"><span data-stu-id="41a30-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="41a30-105">Ensuite, vous allez lier le compte de stockage à l’application web en vous appuyant sur les paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="41a30-105">Then you will link the storage account to the web app using app settings.</span></span>

<span data-ttu-id="41a30-106">Si nécessaire, installez Azure PowerShell à l’aide des instructions figurant dans le [Guide Azure PowerShell](/powershell/azure/overview), puis exécutez `Login-AzureRmAccount` pour créer une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="41a30-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="41a30-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="41a30-107">Sample script</span></span>

<span data-ttu-id="41a30-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connecter une application web à un compte de stockage")]</span><span class="sxs-lookup"><span data-stu-id="41a30-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app to a storage account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="41a30-109">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="41a30-109">Clean up deployment</span></span> 

<span data-ttu-id="41a30-110">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources, l’application web et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="41a30-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="41a30-111">Explication du script</span><span class="sxs-lookup"><span data-stu-id="41a30-111">Script explanation</span></span>

<span data-ttu-id="41a30-112">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="41a30-112">This script uses the following commands.</span></span> <span data-ttu-id="41a30-113">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="41a30-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="41a30-114">Commande</span><span class="sxs-lookup"><span data-stu-id="41a30-114">Command</span></span> | <span data-ttu-id="41a30-115">Remarques</span><span class="sxs-lookup"><span data-stu-id="41a30-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="41a30-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="41a30-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="41a30-117">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="41a30-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="41a30-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="41a30-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="41a30-119">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="41a30-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="41a30-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="41a30-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="41a30-121">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="41a30-121">Creates a web app.</span></span> |
| [<span data-ttu-id="41a30-122">New-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="41a30-122">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="41a30-123">Crée un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="41a30-123">Creates a Storage account.</span></span> |
| [<span data-ttu-id="41a30-124">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="41a30-124">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="41a30-125">Obtient les clés d’accès pour le compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="41a30-125">Gets the access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="41a30-126">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="41a30-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="41a30-127">Modifie la configuration d’une application web.</span><span class="sxs-lookup"><span data-stu-id="41a30-127">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="41a30-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="41a30-128">Next steps</span></span>

<span data-ttu-id="41a30-129">Pour plus d’informations sur le module Azure PowerShell, consultez la [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="41a30-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="41a30-130">Vous trouverez des exemples supplémentaires de scripts Azure PowerShell pour Azure App Service Web Apps sur la page [Azure PowerShell Samples](../app-service-powershell-samples.md) (Exemples Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="41a30-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
