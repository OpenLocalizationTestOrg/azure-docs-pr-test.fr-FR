---
title: "Déploiement de  ressources avec le modèle et l’API REST | Microsoft Docs"
description: "Utilisez Azure Resource Manager et l’API REST Resource Manager pour déployer des ressources sur Azure. Les ressources sont définies dans un modèle Resource Manager."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 46856a25fb57bb2c5a3c1aeae13c11655e1a58a5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="78298-104">Déployer des ressources à l’aide de modèles Resource Manager et de l’API REST Resource Manager</span><span class="sxs-lookup"><span data-stu-id="78298-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="78298-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="78298-105">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="78298-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="78298-106">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="78298-107">Portail</span><span class="sxs-lookup"><span data-stu-id="78298-107">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="78298-108">API REST</span><span class="sxs-lookup"><span data-stu-id="78298-108">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="78298-109">Cet article explique comment utiliser l’API REST Resource Manager avec les modèles Resource Manager pour déployer vos ressources dans Azure.</span><span class="sxs-lookup"><span data-stu-id="78298-109">This article explains how to use the Resource Manager REST API with Resource Manager templates to deploy your resources to Azure.</span></span>  

> [!TIP]
> <span data-ttu-id="78298-110">Pour obtenir de l’aide dans le débogage d’une erreur pendant le déploiement, consultez :</span><span class="sxs-lookup"><span data-stu-id="78298-110">For help with debugging an error during deployment, see:</span></span>
> 
> * <span data-ttu-id="78298-111">[View deployment operations (Afficher les opérations de déploiement)](resource-manager-deployment-operations.md) pour apprendre à récupérer des informations qui vous aideront à résoudre votre erreur</span><span class="sxs-lookup"><span data-stu-id="78298-111">[View deployment operations](resource-manager-deployment-operations.md) to learn about getting information that helps you troubleshoot your error</span></span>
> * <span data-ttu-id="78298-112">[Résoudre les erreurs courantes lors du déploiement de ressources sur Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md) pour apprendre à résoudre les erreurs de déploiement courantes</span><span class="sxs-lookup"><span data-stu-id="78298-112">[Troubleshoot common errors when deploying resources to Azure with Azure Resource Manager](resource-manager-common-deployment-errors.md) to learn how to resolve common deployment errors</span></span>
> 
> 

<span data-ttu-id="78298-113">Votre modèle peut être un fichier local ou un fichier externe disponible par le biais d’un URI.</span><span class="sxs-lookup"><span data-stu-id="78298-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="78298-114">Lorsque votre modèle se trouve dans un compte de stockage, vous pouvez restreindre l’accès au modèle et fournir un jeton de signature d’accès partagé (SAP) au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="78298-114">When your template resides in a storage account, you can restrict access to the template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-the-rest-api"></a><span data-ttu-id="78298-115">Déployer avec l’API REST</span><span class="sxs-lookup"><span data-stu-id="78298-115">Deploy with the REST API</span></span>
1. <span data-ttu-id="78298-116">Définissez [des en-têtes et des paramètres communs](https://docs.microsoft.com/rest/api/index), y compris des jetons d’authentification.</span><span class="sxs-lookup"><span data-stu-id="78298-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="78298-117">Si vous n’avez pas de groupe de ressources, créez-en un.</span><span class="sxs-lookup"><span data-stu-id="78298-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="78298-118">Fournissez votre ID abonnement, le nom du groupe de ressources et l’emplacement dont vous avez besoin pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="78298-118">Provide your subscription ID, the name of the new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="78298-119">Pour plus d’informations, consultez [Créer un groupe de ressources](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="78298-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="78298-120">Validez votre déploiement avant son exécution en exécutant l’opération [Valider un déploiement de modèle](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) .</span><span class="sxs-lookup"><span data-stu-id="78298-120">Validate your deployment before executing it by running the [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="78298-121">Lorsque vous testez le déploiement, indiquez les paramètres exactement comme vous le feriez lors de l'exécution du déploiement (voir l'étape suivante).</span><span class="sxs-lookup"><span data-stu-id="78298-121">When testing the deployment, provide parameters exactly as you would when executing the deployment (shown in the next step).</span></span>
4. <span data-ttu-id="78298-122">Créez un déploiement.</span><span class="sxs-lookup"><span data-stu-id="78298-122">Create a deployment.</span></span> <span data-ttu-id="78298-123">Fournissez votre ID abonnement, le nom du groupe de ressources, le nom du déploiement et un lien vers votre modèle.</span><span class="sxs-lookup"><span data-stu-id="78298-123">Provide your subscription ID, the name of the resource group, the name of the deployment, and a link to your template.</span></span> <span data-ttu-id="78298-124">Pour plus d’informations sur le fichier de modèle, consultez [Fichier de paramètres](#parameter-file).</span><span class="sxs-lookup"><span data-stu-id="78298-124">For information about the template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="78298-125">Pour plus d’informations sur l’API REST pour créer un groupe de ressources, consultez [Créer un déploiement de modèle](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="78298-125">For more information about the REST API to create a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="78298-126">Notez que le **Mode** est défini sur **Incremental (Incrémentiel)**.</span><span class="sxs-lookup"><span data-stu-id="78298-126">Notice the **mode** is set to **Incremental**.</span></span> <span data-ttu-id="78298-127">Pour exécuter un déploiement complet, définissez le paramètre **Mode** sur la valeur **Complete (Terminé)**.</span><span class="sxs-lookup"><span data-stu-id="78298-127">To run a complete deployment, set **mode** to **Complete**.</span></span> <span data-ttu-id="78298-128">Soyez prudent lorsque vous utilisez le mode complet, car vous pouvez supprimer par inadvertance des ressources qui ne sont pas dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="78298-128">Be careful when using the complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      <span data-ttu-id="78298-129">Si vous souhaitez consigner le contenu de la réponse et/ou le contenu de la demande, incluez **debugSetting** dans la demande.</span><span class="sxs-lookup"><span data-stu-id="78298-129">If you want to log response content, request content, or both, include **debugSetting** in the request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="78298-130">Vous pouvez configurer votre compte de stockage pour qu’il utilise un jeton de signature d’accès partagé (SAP).</span><span class="sxs-lookup"><span data-stu-id="78298-130">You can set up your storage account to use a shared access signature (SAS) token.</span></span> <span data-ttu-id="78298-131">Pour plus d’informations, consultez [Délégation de l’accès avec une signature d’accès partagé](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="78298-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="78298-132">Obtenez l’état du déploiement du modèle.</span><span class="sxs-lookup"><span data-stu-id="78298-132">Get the status of the template deployment.</span></span> <span data-ttu-id="78298-133">Pour plus d’informations, consultez [Obtenir des informations sur le déploiement d’un modèle](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span><span class="sxs-lookup"><span data-stu-id="78298-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="78298-134">Fichier de paramètres</span><span class="sxs-lookup"><span data-stu-id="78298-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="78298-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="78298-135">Next steps</span></span>
* <span data-ttu-id="78298-136">Pour plus d’informations sur la gestion des opérations REST asynchrones, consultez [Track asynchronous Azure operations (Suivi des opérations asynchrones Azure)](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="78298-136">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="78298-137">Pour découvrir un exemple de déploiement de ressources par le biais de la bibliothèque cliente .NET, consultez [Déployer des ressources à l’aide de bibliothèques .NET et d’un modèle](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="78298-137">For an example of deploying resources through the .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="78298-138">Pour définir des paramètres dans le modèle, consultez [Création de modèles](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="78298-138">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="78298-139">Pour obtenir des instructions sur le déploiement de votre solution dans différents environnements, consultez [Environnements de développement et de test dans Microsoft Azure](solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="78298-139">For guidance on deploying your solution to different environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="78298-140">Pour obtenir des conseils sur l’utilisation de Resource Manager par les entreprises pour gérer efficacement les abonnements, voir [Structure d’Azure Enterprise - Gouvernance normative de l’abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="78298-140">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

