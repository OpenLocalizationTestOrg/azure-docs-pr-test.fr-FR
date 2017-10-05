---
title: "Exemple de script Azure PowerShell - Télécharger des fichiers vers une application web via FTP | Microsoft Docs"
description: "Exemple de script Azure PowerShell - Télécharger des fichiers vers une application web via FTP"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: b7d46d6f-44fd-454c-8008-87dab6eefbc1
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 96b99110b63b037746fcc40eb15db5d718eb71a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="upload-files-to-a-web-app-using-ftp"></a><span data-ttu-id="0083b-103">Télécharger des fichiers vers une application web via FTP</span><span class="sxs-lookup"><span data-stu-id="0083b-103">Upload files to a web app using FTP</span></span>

<span data-ttu-id="0083b-104">Cet exemple de script crée une application web dans App Service avec ses ressources associées, puis déploie votre code d’application web au moyen du site FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span><span class="sxs-lookup"><span data-stu-id="0083b-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="0083b-105">Si nécessaire, installez Azure PowerShell à l’aide des instructions figurant dans le [guide Azure PowerShell](/powershell/azure/overview), puis exécutez `Login-AzureRmAccount` pour créer une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="0083b-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="0083b-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="0083b-106">Sample script</span></span>

<span data-ttu-id="0083b-107">[!code-powershell[principal](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Télécharger des fichiers vers une application web via FTP")]</span><span class="sxs-lookup"><span data-stu-id="0083b-107">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files to a web app using FTP")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0083b-108">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="0083b-108">Clean up deployment</span></span> 

<span data-ttu-id="0083b-109">Une fois l’exemple de script exécuté, la commande suivante permet de supprimer le groupe de ressources, l’application web et toutes les ressources associées.</span><span class="sxs-lookup"><span data-stu-id="0083b-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="0083b-110">Explication du script</span><span class="sxs-lookup"><span data-stu-id="0083b-110">Script explanation</span></span>

<span data-ttu-id="0083b-111">Ce script utilise les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="0083b-111">This script uses the following commands.</span></span> <span data-ttu-id="0083b-112">Chaque commande du tableau renvoie à une documentation spécifique.</span><span class="sxs-lookup"><span data-stu-id="0083b-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0083b-113">Commande</span><span class="sxs-lookup"><span data-stu-id="0083b-113">Command</span></span> | <span data-ttu-id="0083b-114">Remarques</span><span class="sxs-lookup"><span data-stu-id="0083b-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0083b-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0083b-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="0083b-116">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="0083b-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0083b-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="0083b-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="0083b-118">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="0083b-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="0083b-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="0083b-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="0083b-120">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="0083b-120">Creates a web app.</span></span> |
| [<span data-ttu-id="0083b-121">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="0083b-121">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="0083b-122">Obtient un profil de publication d’application web.</span><span class="sxs-lookup"><span data-stu-id="0083b-122">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0083b-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0083b-123">Next steps</span></span>

<span data-ttu-id="0083b-124">Pour plus d’informations sur le module Azure PowerShell, consultez la [Documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0083b-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0083b-125">Vous trouverez des exemples supplémentaires de scripts Azure PowerShell pour Azure App Service Web Apps sur la page [Azure PowerShell Samples](../app-service-powershell-samples.md) (Exemples Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="0083b-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
