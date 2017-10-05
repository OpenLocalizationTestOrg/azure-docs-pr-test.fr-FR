---
title: "Développer des modèles pour Azure Stack | Microsoft Docs"
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
ms.openlocfilehash: a8468616f924aebb91447b379cea3f926c39de48
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-resource-manager-template-considerations"></a><span data-ttu-id="54928-103">Considérations relatives au modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="54928-103">Azure Resource Manager template considerations</span></span>
<span data-ttu-id="54928-104">Lorsque vous développez votre application, il est important de garantir la portabilité du modèle entre Azure et Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="54928-104">As you develop your application, it is important to ensure template portability between Azure and Azure Stack.</span></span>  <span data-ttu-id="54928-105">Cette rubrique présente des considérations relatives au développement de [modèles](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf) Azure Resource Manager, afin que vous puissiez mettre au point un prototype de votre déploiement d’application et de test dans Azure sans avoir accès à un environnement Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="54928-105">This topic provides considerations for developing Azure Resource Manager [templates](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf), so you can prototype your application and test deployment in Azure without access to an Azure Stack environment.</span></span>

## <a name="public-namespaces"></a><span data-ttu-id="54928-106">Espaces de noms publics</span><span class="sxs-lookup"><span data-stu-id="54928-106">Public namespaces</span></span>
<span data-ttu-id="54928-107">Comme Azure Stack est hébergé dans votre centre de données, il dispose d’espaces de noms de point de terminaison de service autres que le cloud public Azure.</span><span class="sxs-lookup"><span data-stu-id="54928-107">Because Azure Stack is hosted in your datacenter, it has different service endpoint namespaces than the Azure public cloud.</span></span> <span data-ttu-id="54928-108">Par conséquent, les points de terminaison publics codés en dur dans les modèles Resource Manager échouent lorsque vous essayez de les déployer sur Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="54928-108">As a result, hardcoded public endpoints in Resource Manager templates fail when you try to deploy them to Azure Stack.</span></span> <span data-ttu-id="54928-109">Au lieu de cela, vous pouvez utiliser la fonction de *référence* et de *concaténation* pour générer dynamiquement le point de terminaison de service en fonction des valeurs récupérées à partir du fournisseur de ressources lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="54928-109">Instead, you can use the *reference* and *concatenate* function to dynamically build the service endpoint based on values retrieved from the resource provider during deployment.</span></span> <span data-ttu-id="54928-110">Par exemple, au lieu de spécifier *blob.core.windows.net* dans votre modèle, vous devez récupérer l’objet [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) pour définir dynamiquement le point de terminaison *osDisk.URI* :</span><span class="sxs-lookup"><span data-stu-id="54928-110">For example, rather than specifying *blob.core.windows.net* in your template, retrieve the [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) to dynamically set the *osDisk.URI* endpoint:</span></span>

     "osDisk": {"name": "osdisk","vhd": {"uri": 
     "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2015-06-15').primaryEndpoints.blob, variables('vmStorageAccountContainerName'),
      '/',variables('OSDiskName'),'.vhd')]"}}

## <a name="api-versioning"></a><span data-ttu-id="54928-111">Contrôle de version d’API</span><span class="sxs-lookup"><span data-stu-id="54928-111">API versioning</span></span>
<span data-ttu-id="54928-112">Les versions de service Azure peuvent différer entre Azure et Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="54928-112">Azure service versions may differ between Azure and Azure Stack.</span></span> <span data-ttu-id="54928-113">Chaque ressource requiert l’attribut apiVersion, qui définit les fonctionnalités proposées.</span><span class="sxs-lookup"><span data-stu-id="54928-113">Each resource requires the apiVersion attribute, which defines the capabilities offered.</span></span> <span data-ttu-id="54928-114">Pour assurer la compatibilité des versions d’API dans Azure Stack, voici les versions d’API valides pour chaque fournisseur de ressources :</span><span class="sxs-lookup"><span data-stu-id="54928-114">To ensure API version compatibility in Azure Stack, the following are valid API versions for each Resource Provider:</span></span>

| <span data-ttu-id="54928-115">Fournisseur de ressources</span><span class="sxs-lookup"><span data-stu-id="54928-115">Resource Provider</span></span> | <span data-ttu-id="54928-116">apiVersion</span><span class="sxs-lookup"><span data-stu-id="54928-116">apiVersion</span></span> |
| --- | --- |
| <span data-ttu-id="54928-117">Calcul</span><span class="sxs-lookup"><span data-stu-id="54928-117">Compute</span></span> |`'2015-06-15'` |
| <span data-ttu-id="54928-118">Réseau</span><span class="sxs-lookup"><span data-stu-id="54928-118">Network</span></span> |<span data-ttu-id="54928-119">`'2015-06-15'`, `'2015-05-01-preview'`</span><span class="sxs-lookup"><span data-stu-id="54928-119">`'2015-06-15'`, `'2015-05-01-preview'`</span></span> |
| <span data-ttu-id="54928-120">Storage</span><span class="sxs-lookup"><span data-stu-id="54928-120">Storage</span></span> |<span data-ttu-id="54928-121">`'2016-01-01'`, `'2015-06-15'`, `'2015-05-01-preview'`</span><span class="sxs-lookup"><span data-stu-id="54928-121">`'2016-01-01'`, `'2015-06-15'`, `'2015-05-01-preview'`</span></span> |
| <span data-ttu-id="54928-122">KeyVault</span><span class="sxs-lookup"><span data-stu-id="54928-122">KeyVault</span></span> | `'2015-06-01'` |
| <span data-ttu-id="54928-123">App Service</span><span class="sxs-lookup"><span data-stu-id="54928-123">App Service</span></span> |`'2015-08-01'` |
| <span data-ttu-id="54928-124">MySQL</span><span class="sxs-lookup"><span data-stu-id="54928-124">MySQL</span></span> |`'2015-09-01'` |
| <span data-ttu-id="54928-125">SQL</span><span class="sxs-lookup"><span data-stu-id="54928-125">SQL</span></span> |`'2014-04-01-preview'` |

## <a name="template-functions"></a><span data-ttu-id="54928-126">Fonctions des modèles de gestionnaire des ressources Azure</span><span class="sxs-lookup"><span data-stu-id="54928-126">Template functions</span></span>
<span data-ttu-id="54928-127">Les [fonctions](../azure-resource-manager/resource-group-template-functions.md) Resource Manager offrent les fonctionnalités nécessaires pour créer des modèles dynamiques.</span><span class="sxs-lookup"><span data-stu-id="54928-127">Resource Manager [functions](../azure-resource-manager/resource-group-template-functions.md) provide capabilities required to build dynamic templates.</span></span> <span data-ttu-id="54928-128">Par exemple, vous pouvez utiliser des fonctions pour des tâches telles que :</span><span class="sxs-lookup"><span data-stu-id="54928-128">As an example, you can use functions for tasks like:</span></span>

* <span data-ttu-id="54928-129">la concaténation ou la troncation des chaînes ;</span><span class="sxs-lookup"><span data-stu-id="54928-129">Concatenating or trimming strings</span></span> 
* <span data-ttu-id="54928-130">le référencement de valeurs d’autres ressources ;</span><span class="sxs-lookup"><span data-stu-id="54928-130">Reference values from other resources</span></span>
* <span data-ttu-id="54928-131">l’itération sur les ressources pour déployer plusieurs instances.</span><span class="sxs-lookup"><span data-stu-id="54928-131">Iterating on resources to deploy multiple instances</span></span> 

<span data-ttu-id="54928-132">Lorsque vous créez vos modèles, certaines fonctions ne sont pas disponibles dans le kit de développement Azure Stack et ne doivent pas être utilisées.</span><span class="sxs-lookup"><span data-stu-id="54928-132">As you build your templates, some functions are not available in Azure Stack Development Kit, and should not be used.</span></span> <span data-ttu-id="54928-133">Ces fonctions sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="54928-133">These functions are:</span></span>

* <span data-ttu-id="54928-134">Skip</span><span class="sxs-lookup"><span data-stu-id="54928-134">Skip</span></span>
* <span data-ttu-id="54928-135">Take</span><span class="sxs-lookup"><span data-stu-id="54928-135">Take</span></span>

## <a name="resource-location"></a><span data-ttu-id="54928-136">Emplacement des ressources</span><span class="sxs-lookup"><span data-stu-id="54928-136">Resource location</span></span>
<span data-ttu-id="54928-137">Les modèles Resource Manager utilisent un attribut d’emplacement pour placer les ressources pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="54928-137">Resource Manager templates use a location attribute to place resources during deployment.</span></span> <span data-ttu-id="54928-138">Dans Azure, les emplacements font référence à une région, par exemple, Ouest des États-Unis ou Amérique du Sud.</span><span class="sxs-lookup"><span data-stu-id="54928-138">In Azure, locations refer to a region like West US or South America.</span></span> <span data-ttu-id="54928-139">Dans Azure Stack, les emplacements sont différents, car Azure Stack est situé dans votre centre de données.</span><span class="sxs-lookup"><span data-stu-id="54928-139">In Azure Stack, locations are different because Azure Stack is in your datacenter.</span></span>  <span data-ttu-id="54928-140">Pour garantir que les modèles sont transférables entre Azure et Azure Stack, vous devez référencer l’emplacement du groupe de ressources lorsque vous déployez des ressources individuelles.</span><span class="sxs-lookup"><span data-stu-id="54928-140">To ensure templates are transferrable between Azure and Azure Stack, you should reference the resource group location as you deploy individual resources.</span></span> <span data-ttu-id="54928-141">Vous pouvez pour cela utiliser `[resourceGroup().Location]` afin de veiller à ce que toutes les ressources héritent de l’emplacement du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="54928-141">You can do this using `[resourceGroup().Location]` to ensure all resources inherit the resource group location.</span></span>  <span data-ttu-id="54928-142">L’extrait de modèle Resource Manager suivant est un exemple d’utilisation de cette fonction lors du déploiement d’un compte de stockage :</span><span class="sxs-lookup"><span data-stu-id="54928-142">The following Resource Manager template excerpt is an example of using this function while deploying a storage account:</span></span>

    "resources": [
    {
      "name": "[variables('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "[variables('apiVersionStorage')]",
      "location": "[resourceGroup().location]",
      "comments": "This storage account is used to store the VM disks",
      "properties": {
      "accountType": "Standard_GRS"
      }
    }
    ]


## <a name="next-steps"></a><span data-ttu-id="54928-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="54928-143">Next steps</span></span>
* [<span data-ttu-id="54928-144">Déployer des modèles avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="54928-144">Deploy templates with PowerShell</span></span>](azure-stack-deploy-template-powershell.md)
* [<span data-ttu-id="54928-145">Déployer des modèles avec l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="54928-145">Deploy templates with Azure CLI</span></span>](azure-stack-deploy-template-command-line.md)
* [<span data-ttu-id="54928-146">Déployer des modèles avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="54928-146">Deploy templates with Visual Studio</span></span>](azure-stack-deploy-template-visual-studio.md)

