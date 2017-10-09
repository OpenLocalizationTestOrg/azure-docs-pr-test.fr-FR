---
title: "modèles d’aaaDevelop pour la pile de Azure | Documents Microsoft"
description: "Découvrir les meilleures pratiques en matière de modèles Azure Stack"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 8a5bc713-6f51-49c8-aeed-6ced0145e07b
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 01581abcb7a3616469dcd38a646734f68decd3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-considerations"></a><span data-ttu-id="f2bc2-103">Considérations relatives au modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f2bc2-103">Azure Resource Manager template considerations</span></span>
<span data-ttu-id="f2bc2-104">Lorsque vous développez votre application, il est important tooensure la portabilité de modèle entre Azure et Azure pile.</span><span class="sxs-lookup"><span data-stu-id="f2bc2-104">As you develop your application, it is important tooensure template portability between Azure and Azure Stack.</span></span>  <span data-ttu-id="f2bc2-105">Cette rubrique fournit des considérations de développement Azure Resource Manager [modèles](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf), pour vous permettre de prototype de votre déploiement d’application et de test dans Azure sans environnement de Azure pile tooan access.</span><span class="sxs-lookup"><span data-stu-id="f2bc2-105">This topic provides considerations for developing Azure Resource Manager [templates](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf), so you can prototype your application and test deployment in Azure without access tooan Azure Stack environment.</span></span>

## <a name="public-namespaces"></a><span data-ttu-id="f2bc2-106">Espaces de noms publics</span><span class="sxs-lookup"><span data-stu-id="f2bc2-106">Public namespaces</span></span>
<span data-ttu-id="f2bc2-107">Parce que la pile de Azure est hébergé dans votre centre de données, il a des espaces de noms service autre point de terminaison à hello cloud public Azure.</span><span class="sxs-lookup"><span data-stu-id="f2bc2-107">Because Azure Stack is hosted in your datacenter, it has different service endpoint namespaces than hello Azure public cloud.</span></span> <span data-ttu-id="f2bc2-108">Par conséquent, codé en dur des points de terminaison publics dans les modèles de gestionnaire de ressources échouent lorsque vous essayez de toodeploy les tooAzure pile.</span><span class="sxs-lookup"><span data-stu-id="f2bc2-108">As a result, hardcoded public endpoints in Resource Manager templates fail when you try toodeploy them tooAzure Stack.</span></span> <span data-ttu-id="f2bc2-109">Au lieu de cela, vous pouvez utiliser hello *référence* et *concaténer* fonction toodynamically générer le point de terminaison de service hello en fonction des valeurs extraites du fournisseur de ressources hello lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="f2bc2-109">Instead, you can use hello *reference* and *concatenate* function toodynamically build hello service endpoint based on values retrieved from hello resource provider during deployment.</span></span> <span data-ttu-id="f2bc2-110">Par exemple, plutôt que de spécifier *blob.core.windows.net* dans votre modèle, récupérer hello [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) toodynamically définir hello *osDisk.URI* point de terminaison :</span><span class="sxs-lookup"><span data-stu-id="f2bc2-110">For example, rather than specifying *blob.core.windows.net* in your template, retrieve hello [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) toodynamically set hello *osDisk.URI* endpoint:</span></span>

     "osDisk": {"name": "osdisk","vhd": {"uri": 
     "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2015-06-15').primaryEndpoints.blob, variables('vmStorageAccountContainerName'),
      '/',variables('OSDiskName'),'.vhd')]"}}

## <a name="api-versioning"></a><span data-ttu-id="f2bc2-111">Contrôle de version d’API</span><span class="sxs-lookup"><span data-stu-id="f2bc2-111">API versioning</span></span>
<span data-ttu-id="f2bc2-112">Les versions de service Azure peuvent différer entre Azure et Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="f2bc2-112">Azure service versions may differ between Azure and Azure Stack.</span></span> <span data-ttu-id="f2bc2-113">Chaque ressource requiert l’attribut hello apiVersion, qui définit les fonctions hello.</span><span class="sxs-lookup"><span data-stu-id="f2bc2-113">Each resource requires hello apiVersion attribute, which defines hello capabilities offered.</span></span> <span data-ttu-id="f2bc2-114">compatibilité des versions tooensure API dans la pile de Azure, hello suivant sont des versions d’API valides pour chaque fournisseur de ressources :</span><span class="sxs-lookup"><span data-stu-id="f2bc2-114">tooensure API version compatibility in Azure Stack, hello following are valid API versions for each Resource Provider:</span></span>

| <span data-ttu-id="f2bc2-115">Fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="f2bc2-115">Resource Provider</span></span> | <span data-ttu-id="f2bc2-116">apiVersion</span><span class="sxs-lookup"><span data-stu-id="f2bc2-116">apiVersion</span></span> |
| --- | --- |
| <span data-ttu-id="f2bc2-117">Calcul</span><span class="sxs-lookup"><span data-stu-id="f2bc2-117">Compute</span></span> |`'2015-06-15'` |
| <span data-ttu-id="f2bc2-118">Réseau</span><span class="sxs-lookup"><span data-stu-id="f2bc2-118">Network</span></span> |<span data-ttu-id="f2bc2-119">`'2015-06-15'`, `'2015-05-01-preview'`</span><span class="sxs-lookup"><span data-stu-id="f2bc2-119">`'2015-06-15'`, `'2015-05-01-preview'`</span></span> |
| <span data-ttu-id="f2bc2-120">Storage</span><span class="sxs-lookup"><span data-stu-id="f2bc2-120">Storage</span></span> |<span data-ttu-id="f2bc2-121">`'2016-01-01'`, `'2015-06-15'`, `'2015-05-01-preview'`</span><span class="sxs-lookup"><span data-stu-id="f2bc2-121">`'2016-01-01'`, `'2015-06-15'`, `'2015-05-01-preview'`</span></span> |
| <span data-ttu-id="f2bc2-122">KeyVault</span><span class="sxs-lookup"><span data-stu-id="f2bc2-122">KeyVault</span></span> | `'2015-06-01'` |
| <span data-ttu-id="f2bc2-123">App Service</span><span class="sxs-lookup"><span data-stu-id="f2bc2-123">App Service</span></span> |`'2015-08-01'` |
| <span data-ttu-id="f2bc2-124">MySQL</span><span class="sxs-lookup"><span data-stu-id="f2bc2-124">MySQL</span></span> |`'2015-09-01'` |
| <span data-ttu-id="f2bc2-125">SQL</span><span class="sxs-lookup"><span data-stu-id="f2bc2-125">SQL</span></span> |`'2014-04-01-preview'` |

## <a name="template-functions"></a><span data-ttu-id="f2bc2-126">Fonctions des modèles de gestionnaire des ressources Azure</span><span class="sxs-lookup"><span data-stu-id="f2bc2-126">Template functions</span></span>
<span data-ttu-id="f2bc2-127">Le Gestionnaire de ressources [fonctions](../azure-resource-manager/resource-group-template-functions.md) fournissent des modèles dynamiques toobuild requis de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="f2bc2-127">Resource Manager [functions](../azure-resource-manager/resource-group-template-functions.md) provide capabilities required toobuild dynamic templates.</span></span> <span data-ttu-id="f2bc2-128">Par exemple, vous pouvez utiliser des fonctions pour des tâches telles que :</span><span class="sxs-lookup"><span data-stu-id="f2bc2-128">As an example, you can use functions for tasks like:</span></span>

* <span data-ttu-id="f2bc2-129">la concaténation ou la troncation des chaînes ;</span><span class="sxs-lookup"><span data-stu-id="f2bc2-129">Concatenating or trimming strings</span></span> 
* <span data-ttu-id="f2bc2-130">le référencement de valeurs d’autres ressources ;</span><span class="sxs-lookup"><span data-stu-id="f2bc2-130">Reference values from other resources</span></span>
* <span data-ttu-id="f2bc2-131">Une itération sur les ressources toodeploy plusieurs instances</span><span class="sxs-lookup"><span data-stu-id="f2bc2-131">Iterating on resources toodeploy multiple instances</span></span> 

<span data-ttu-id="f2bc2-132">Lorsque vous créez vos modèles, certaines fonctions ne sont pas disponibles dans le kit de développement Azure Stack et ne doivent pas être utilisées.</span><span class="sxs-lookup"><span data-stu-id="f2bc2-132">As you build your templates, some functions are not available in Azure Stack Development Kit, and should not be used.</span></span> <span data-ttu-id="f2bc2-133">Ces fonctions sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="f2bc2-133">These functions are:</span></span>

* <span data-ttu-id="f2bc2-134">Skip</span><span class="sxs-lookup"><span data-stu-id="f2bc2-134">Skip</span></span>
* <span data-ttu-id="f2bc2-135">Take</span><span class="sxs-lookup"><span data-stu-id="f2bc2-135">Take</span></span>

## <a name="resource-location"></a><span data-ttu-id="f2bc2-136">Emplacement des ressources</span><span class="sxs-lookup"><span data-stu-id="f2bc2-136">Resource location</span></span>
<span data-ttu-id="f2bc2-137">Modèles du Gestionnaire de ressources utilisent un emplacement attribut tooplace des ressources pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f2bc2-137">Resource Manager templates use a location attribute tooplace resources during deployment.</span></span> <span data-ttu-id="f2bc2-138">Dans Azure, emplacements renvoient tooa la région ouest des États-Unis ou en Amérique du Sud.</span><span class="sxs-lookup"><span data-stu-id="f2bc2-138">In Azure, locations refer tooa region like West US or South America.</span></span> <span data-ttu-id="f2bc2-139">Dans Azure Stack, les emplacements sont différents, car Azure Stack est situé dans votre centre de données.</span><span class="sxs-lookup"><span data-stu-id="f2bc2-139">In Azure Stack, locations are different because Azure Stack is in your datacenter.</span></span>  <span data-ttu-id="f2bc2-140">tooensure modèles peuvent être transférées entre Azure et de la pile d’Azure, vous devez référencer emplacement du groupe de ressources hello lorsque vous déployez des ressources individuelles.</span><span class="sxs-lookup"><span data-stu-id="f2bc2-140">tooensure templates are transferrable between Azure and Azure Stack, you should reference hello resource group location as you deploy individual resources.</span></span> <span data-ttu-id="f2bc2-141">Ce faire, vous pouvez utiliser `[resourceGroup().Location]` tooensure héritent de toutes les ressources hello emplacement du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f2bc2-141">You can do this using `[resourceGroup().Location]` tooensure all resources inherit hello resource group location.</span></span>  <span data-ttu-id="f2bc2-142">Bonjour extrait de modèle de gestionnaire de ressources suivant est un exemple d’utilisation de cette fonction lors du déploiement d’un compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="f2bc2-142">hello following Resource Manager template excerpt is an example of using this function while deploying a storage account:</span></span>

    "resources": [
    {
      "name": "[variables('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "[variables('apiVersionStorage')]",
      "location": "[resourceGroup().location]",
      "comments": "This storage account is used toostore hello VM disks",
      "properties": {
      "accountType": "Standard_GRS"
      }
    }
    ]


## <a name="next-steps"></a><span data-ttu-id="f2bc2-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f2bc2-143">Next steps</span></span>
* [<span data-ttu-id="f2bc2-144">Déployer des modèles avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2bc2-144">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
* [<span data-ttu-id="f2bc2-145">Déployer des modèles avec l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="f2bc2-145">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)
* [<span data-ttu-id="f2bc2-146">Déployer des modèles avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f2bc2-146">Deploy templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)

