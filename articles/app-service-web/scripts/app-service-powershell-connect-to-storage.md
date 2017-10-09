---
title: "aaaAzure exemple de Script PowerShell - se connecter à un compte de stockage web application tooa | Documents Microsoft"
description: "Script Azure PowerShell exemple - se connecter à un compte de stockage tooa application web"
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
ms.openlocfilehash: 07693366d32fbaefe92c18df67ded81661e1a2df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-storage-account"></a><span data-ttu-id="28b0a-103">Se connecter à un compte de stockage tooa application web</span><span class="sxs-lookup"><span data-stu-id="28b0a-103">Connect a web app tooa storage account</span></span>

<span data-ttu-id="28b0a-104">Dans ce scénario, vous allez apprendre comment toocreate un compte de stockage Azure et Azure web app.</span><span class="sxs-lookup"><span data-stu-id="28b0a-104">In this scenario you will learn how toocreate an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="28b0a-105">Ensuite, vous allez lier hello stockage compte toohello web app à l’aide des paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="28b0a-105">Then you will link hello storage account toohello web app using app settings.</span></span>

<span data-ttu-id="28b0a-106">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](/powershell/azure/overview), puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="28b0a-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="28b0a-107">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="28b0a-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app tooa storage account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="28b0a-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="28b0a-108">Clean up deployment</span></span> 

<span data-ttu-id="28b0a-109">Après exécution de l’exemple de script hello, hello commande suivante peut être groupe de ressources hello tooremove utilisé, l’application web et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="28b0a-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="28b0a-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="28b0a-110">Script explanation</span></span>

<span data-ttu-id="28b0a-111">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="28b0a-111">This script uses hello following commands.</span></span> <span data-ttu-id="28b0a-112">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="28b0a-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="28b0a-113">Commande</span><span class="sxs-lookup"><span data-stu-id="28b0a-113">Command</span></span> | <span data-ttu-id="28b0a-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="28b0a-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="28b0a-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="28b0a-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="28b0a-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="28b0a-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="28b0a-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="28b0a-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="28b0a-118">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="28b0a-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="28b0a-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="28b0a-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="28b0a-120">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="28b0a-120">Creates a web app.</span></span> |
| [<span data-ttu-id="28b0a-121">New-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="28b0a-121">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="28b0a-122">Crée un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="28b0a-122">Creates a Storage account.</span></span> |
| [<span data-ttu-id="28b0a-123">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="28b0a-123">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="28b0a-124">Obtient les clés d’accès hello pour un compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="28b0a-124">Gets hello access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="28b0a-125">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="28b0a-125">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="28b0a-126">Modifie la configuration d’une application web.</span><span class="sxs-lookup"><span data-stu-id="28b0a-126">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="28b0a-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="28b0a-127">Next steps</span></span>

<span data-ttu-id="28b0a-128">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="28b0a-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="28b0a-129">Vous trouverez des exemples supplémentaires de Azure Powershell pour Azure App Service Web Apps Bonjour [exemples Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="28b0a-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
