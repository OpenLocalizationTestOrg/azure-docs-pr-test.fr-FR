---
title: "aaaAzure téléchargement fichiers tooa web app à l’aide de FTP - exemple de Script PowerShell | Documents Microsoft"
description: "Exemple de PowerShell Script Azure - téléchargement fichiers tooa web app à l’aide de FTP"
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
ms.openlocfilehash: 32a0a529e94c1315cc6730faf23fca2693c50ffb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-tooa-web-app-using-ftp"></a><span data-ttu-id="1c0e0-103">Télécharger les fichiers tooa web app à l’aide de FTP</span><span class="sxs-lookup"><span data-stu-id="1c0e0-103">Upload files tooa web app using FTP</span></span>

<span data-ttu-id="1c0e0-104">Cet exemple de script crée une application web dans App Service avec ses ressources associées, puis déploie votre code d’application web au moyen du site FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span><span class="sxs-lookup"><span data-stu-id="1c0e0-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="1c0e0-105">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](/powershell/azure/overview), puis exécutez `Login-AzureRmAccount` toocreate une connexion avec Azure.</span><span class="sxs-lookup"><span data-stu-id="1c0e0-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="1c0e0-106">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="1c0e0-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files tooa web app using FTP")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1c0e0-107">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="1c0e0-107">Clean up deployment</span></span> 

<span data-ttu-id="1c0e0-108">Après exécution de l’exemple de script hello, hello commande suivante peut être groupe de ressources hello tooremove utilisé, l’application web et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="1c0e0-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="1c0e0-109">Explication du script</span><span class="sxs-lookup"><span data-stu-id="1c0e0-109">Script explanation</span></span>

<span data-ttu-id="1c0e0-110">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="1c0e0-110">This script uses hello following commands.</span></span> <span data-ttu-id="1c0e0-111">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="1c0e0-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1c0e0-112">Commande</span><span class="sxs-lookup"><span data-stu-id="1c0e0-112">Command</span></span> | <span data-ttu-id="1c0e0-113">Remarques</span><span class="sxs-lookup"><span data-stu-id="1c0e0-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1c0e0-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1c0e0-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="1c0e0-115">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="1c0e0-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1c0e0-116">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="1c0e0-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="1c0e0-117">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="1c0e0-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="1c0e0-118">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="1c0e0-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="1c0e0-119">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="1c0e0-119">Creates a web app.</span></span> |
| [<span data-ttu-id="1c0e0-120">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="1c0e0-120">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="1c0e0-121">Obtient un profil de publication d’application web.</span><span class="sxs-lookup"><span data-stu-id="1c0e0-121">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1c0e0-122">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1c0e0-122">Next steps</span></span>

<span data-ttu-id="1c0e0-123">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1c0e0-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1c0e0-124">Vous trouverez des exemples supplémentaires de Azure Powershell pour Azure App Service Web Apps Bonjour [exemples Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1c0e0-124">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
