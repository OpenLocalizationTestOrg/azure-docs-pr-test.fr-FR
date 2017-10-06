---
title: "aaaAzure exemple de Script PowerShell - lier une application du web tooa de certificat SSL personnalisée | Documents Microsoft"
description: "Exemple de PowerShell Script Azure - liaison d’une application web des tooa de certificat personnalisée SSL"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 23e83b74-614a-49a0-bc08-7542120eeec5
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6e249ceedb9e2b8872dd0bc8b0aea0d718b28dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="1ad68-103">Lier une application du web tooa de certificat SSL personnalisée</span><span class="sxs-lookup"><span data-stu-id="1ad68-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="1ad68-104">Cet exemple de script crée une application web dans le Service d’applications avec ses ressources connexes, puis lie le certificat SSL de hello d’un tooit de nom de domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="1ad68-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> 

<span data-ttu-id="1ad68-105">Si nécessaire, installez hello Azure PowerShell en utilisant une instruction de hello trouvé dans hello [guide Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1ad68-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="1ad68-106">Vérifiez également les points suivants :</span><span class="sxs-lookup"><span data-stu-id="1ad68-106">Also, ensure that:</span></span>

- <span data-ttu-id="1ad68-107">Une connexion avec Azure a été créée à l’aide de hello `az login` commande.</span><span class="sxs-lookup"><span data-stu-id="1ad68-107">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="1ad68-108">Vous avez la page de configuration accès tooyour domaine du bureau d’enregistrement DNS.</span><span class="sxs-lookup"><span data-stu-id="1ad68-108">You have access tooyour domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="1ad68-109">Vous avez valide. Le fichier PFX et son mot de passe hello SSL de certificat vous souhaitez tooupload et établir une liaison.</span><span class="sxs-lookup"><span data-stu-id="1ad68-109">You have a valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="1ad68-110">Exemple de script</span><span class="sxs-lookup"><span data-stu-id="1ad68-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1ad68-111">Nettoyer le déploiement</span><span class="sxs-lookup"><span data-stu-id="1ad68-111">Clean up deployment</span></span> 

<span data-ttu-id="1ad68-112">Après exécution de l’exemple de script hello, hello commande suivante peut être groupe de ressources hello tooremove utilisé, l’application web et toutes les ressources.</span><span class="sxs-lookup"><span data-stu-id="1ad68-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="1ad68-113">Explication du script</span><span class="sxs-lookup"><span data-stu-id="1ad68-113">Script explanation</span></span>

<span data-ttu-id="1ad68-114">Ce script utilise hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="1ad68-114">This script uses hello following commands.</span></span> <span data-ttu-id="1ad68-115">Chaque commande figurant dans la documentation spécifique du toocommand liens table hello.</span><span class="sxs-lookup"><span data-stu-id="1ad68-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1ad68-116">Commande</span><span class="sxs-lookup"><span data-stu-id="1ad68-116">Command</span></span> | <span data-ttu-id="1ad68-117">Remarques</span><span class="sxs-lookup"><span data-stu-id="1ad68-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1ad68-118">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1ad68-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="1ad68-119">Crée un groupe de ressources dans lequel toutes les ressources sont stockées.</span><span class="sxs-lookup"><span data-stu-id="1ad68-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1ad68-120">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="1ad68-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="1ad68-121">Crée un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="1ad68-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="1ad68-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="1ad68-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="1ad68-123">Crée une application web.</span><span class="sxs-lookup"><span data-stu-id="1ad68-123">Creates a web app.</span></span> |
| [<span data-ttu-id="1ad68-124">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="1ad68-124">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="1ad68-125">Modifie un toochange du plan App Service à son niveau de tarification.</span><span class="sxs-lookup"><span data-stu-id="1ad68-125">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="1ad68-126">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="1ad68-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="1ad68-127">Modifie la configuration d’une application web.</span><span class="sxs-lookup"><span data-stu-id="1ad68-127">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="1ad68-128">New-AzureRmWebAppSSLBinding</span><span class="sxs-lookup"><span data-stu-id="1ad68-128">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="1ad68-129">Crée une liaison de certificat SSL pour une application web.</span><span class="sxs-lookup"><span data-stu-id="1ad68-129">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1ad68-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1ad68-130">Next steps</span></span>

<span data-ttu-id="1ad68-131">Pour plus d’informations sur le module Azure PowerShell de hello, consultez [documentation Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1ad68-131">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1ad68-132">Vous trouverez des exemples supplémentaires de Azure Powershell pour Azure App Service Web Apps Bonjour [exemples Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1ad68-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
