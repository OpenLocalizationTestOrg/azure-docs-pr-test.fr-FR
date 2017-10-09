---
title: "ressources aaaDeploy avec l’API REST et modèle | Documents Microsoft"
description: "Utilisez le Gestionnaire de ressources Azure et les REST API du Gestionnaire de ressources toodeploy une tooAzure de ressources. ressources de Hello sont définies dans un modèle de gestionnaire de ressources."
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
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a><span data-ttu-id="088d2-104">Déployer des ressources à l’aide de modèles Resource Manager et de l’API REST Resource Manager</span><span class="sxs-lookup"><span data-stu-id="088d2-104">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="088d2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="088d2-105">PowerShell</span></span>](resource-group-template-deploy.md)
> * [<span data-ttu-id="088d2-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="088d2-106">Azure CLI</span></span>](resource-group-template-deploy-cli.md)
> * [<span data-ttu-id="088d2-107">Portail</span><span class="sxs-lookup"><span data-stu-id="088d2-107">Portal</span></span>](resource-group-template-deploy-portal.md)
> * [<span data-ttu-id="088d2-108">API REST</span><span class="sxs-lookup"><span data-stu-id="088d2-108">REST API</span></span>](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="088d2-109">Cet article explique comment toouse hello REST API du Gestionnaire de ressources avec le Gestionnaire de ressources modèles toodeploy, tooAzure de vos ressources.</span><span class="sxs-lookup"><span data-stu-id="088d2-109">This article explains how toouse hello Resource Manager REST API with Resource Manager templates toodeploy your resources tooAzure.</span></span>  

> [!TIP]
> <span data-ttu-id="088d2-110">Pour obtenir de l’aide dans le débogage d’une erreur pendant le déploiement, consultez :</span><span class="sxs-lookup"><span data-stu-id="088d2-110">For help with debugging an error during deployment, see:</span></span>
> 
> * <span data-ttu-id="088d2-111">[Afficher les opérations de déploiement](resource-manager-deployment-operations.md) toolearn sur l’obtention des informations qui vous permet de corriger votre erreur</span><span class="sxs-lookup"><span data-stu-id="088d2-111">[View deployment operations](resource-manager-deployment-operations.md) toolearn about getting information that helps you troubleshoot your error</span></span>
> * <span data-ttu-id="088d2-112">[Résoudre les erreurs courantes lors du déploiement de ressources tooAzure avec Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn comment les erreurs de déploiement courantes tooresolve</span><span class="sxs-lookup"><span data-stu-id="088d2-112">[Troubleshoot common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn how tooresolve common deployment errors</span></span>
> 
> 

<span data-ttu-id="088d2-113">Votre modèle peut être un fichier local ou un fichier externe disponible par le biais d’un URI.</span><span class="sxs-lookup"><span data-stu-id="088d2-113">Your template can be either a local file or an external file that is available through a URI.</span></span> <span data-ttu-id="088d2-114">Lorsque votre modèle se trouve dans un compte de stockage, vous pouvez restreindre le modèle de toohello access et fournir un jeton de signature (SAS) d’accès partagé au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="088d2-114">When your template resides in a storage account, you can restrict access toohello template and provide a shared access signature (SAS) token during deployment.</span></span>

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a><span data-ttu-id="088d2-115">Déployer avec hello API REST</span><span class="sxs-lookup"><span data-stu-id="088d2-115">Deploy with hello REST API</span></span>
1. <span data-ttu-id="088d2-116">Définissez [des en-têtes et des paramètres communs](https://docs.microsoft.com/rest/api/index), y compris des jetons d’authentification.</span><span class="sxs-lookup"><span data-stu-id="088d2-116">Set [common parameters and headers](https://docs.microsoft.com/rest/api/index), including authentication tokens.</span></span>
2. <span data-ttu-id="088d2-117">Si vous n’avez pas de groupe de ressources, créez-en un.</span><span class="sxs-lookup"><span data-stu-id="088d2-117">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="088d2-118">Fournissez votre ID d’abonnement, le nom de hello du nouveau groupe de ressources hello et l’emplacement que vous avez besoin pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="088d2-118">Provide your subscription ID, hello name of hello new resource group, and location that you need for your solution.</span></span> <span data-ttu-id="088d2-119">Pour plus d’informations, consultez [Créer un groupe de ressources](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="088d2-119">For more information, see [Create a resource group](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).</span></span>
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. <span data-ttu-id="088d2-120">Valider votre déploiement avant son exécution en exécutant hello [valider un déploiement de modèle](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) opération.</span><span class="sxs-lookup"><span data-stu-id="088d2-120">Validate your deployment before executing it by running hello [Validate a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) operation.</span></span> <span data-ttu-id="088d2-121">Lorsque vous testez le déploiement de hello, spécifiez les paramètres exactement comme vous le feriez lors de l’exécution du déploiement hello (illustrée dans l’étape suivante de hello).</span><span class="sxs-lookup"><span data-stu-id="088d2-121">When testing hello deployment, provide parameters exactly as you would when executing hello deployment (shown in hello next step).</span></span>
4. <span data-ttu-id="088d2-122">Créez un déploiement.</span><span class="sxs-lookup"><span data-stu-id="088d2-122">Create a deployment.</span></span> <span data-ttu-id="088d2-123">Fournissez votre ID d’abonnement, hello nom hello du groupe de ressources, hello nom du déploiement de hello et un modèle de tooyour de lien.</span><span class="sxs-lookup"><span data-stu-id="088d2-123">Provide your subscription ID, hello name of hello resource group, hello name of hello deployment, and a link tooyour template.</span></span> <span data-ttu-id="088d2-124">Pour plus d’informations sur le fichier de modèle hello, consultez [fichier de paramètres](#parameter-file).</span><span class="sxs-lookup"><span data-stu-id="088d2-124">For information about hello template file, see [Parameter file](#parameter-file).</span></span> <span data-ttu-id="088d2-125">Pour plus d’informations sur l’API REST de hello toocreate un groupe de ressources, consultez [créer un déploiement de modèle](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="088d2-125">For more information about hello REST API toocreate a resource group, see [Create a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate).</span></span> <span data-ttu-id="088d2-126">Hello d’avis **mode** est défini trop**incrémentiel**.</span><span class="sxs-lookup"><span data-stu-id="088d2-126">Notice hello **mode** is set too**Incremental**.</span></span> <span data-ttu-id="088d2-127">toorun un déploiement complet, définissez **mode** trop**Complete**.</span><span class="sxs-lookup"><span data-stu-id="088d2-127">toorun a complete deployment, set **mode** too**Complete**.</span></span> <span data-ttu-id="088d2-128">Soyez prudent lorsque le mode hello complète que vous pouvez supprimer par inadvertance des ressources qui ne sont pas dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="088d2-128">Be careful when using hello complete mode as you can inadvertently delete resources that are not in your template.</span></span>
   
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
   
      <span data-ttu-id="088d2-129">Si vous souhaitez toolog contenu de la réponse, le contenu de la demande ou les deux, inclure **debugSetting** dans la demande hello.</span><span class="sxs-lookup"><span data-stu-id="088d2-129">If you want toolog response content, request content, or both, include **debugSetting** in hello request.</span></span>
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      <span data-ttu-id="088d2-130">Vous pouvez configurer votre toouse de compte de stockage un jeton de signature (SAS) d’accès partagé.</span><span class="sxs-lookup"><span data-stu-id="088d2-130">You can set up your storage account toouse a shared access signature (SAS) token.</span></span> <span data-ttu-id="088d2-131">Pour plus d’informations, consultez [Délégation de l’accès avec une signature d’accès partagé](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="088d2-131">For more information, see [Delegating Access with a Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).</span></span>
5. <span data-ttu-id="088d2-132">Obtenir l’état de hello de déploiement de modèle hello.</span><span class="sxs-lookup"><span data-stu-id="088d2-132">Get hello status of hello template deployment.</span></span> <span data-ttu-id="088d2-133">Pour plus d’informations, consultez [Obtenir des informations sur le déploiement d’un modèle](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span><span class="sxs-lookup"><span data-stu-id="088d2-133">For more information, see [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span></span>
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a><span data-ttu-id="088d2-134">Fichier de paramètres</span><span class="sxs-lookup"><span data-stu-id="088d2-134">Parameter file</span></span>

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a><span data-ttu-id="088d2-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="088d2-135">Next steps</span></span>
* <span data-ttu-id="088d2-136">toolearn sur la gestion des opérations asynchrones de REST, consultez [le suivi des opérations asynchrones Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="088d2-136">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
* <span data-ttu-id="088d2-137">Pour obtenir un exemple de déploiement de ressources via la bibliothèque cliente .NET hello, consultez [déployer des ressources à l’aide de bibliothèques .NET et un modèle](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="088d2-137">For an example of deploying resources through hello .NET client library, see [Deploy resources using .NET libraries and a template](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="088d2-138">paramètres de toodefine dans le modèle, consultez [création de modèles](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="088d2-138">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="088d2-139">Pour obtenir des conseils sur le déploiement de vos environnements toodifferent de solution, consultez [environnements de développement et de test dans Microsoft Azure](solution-dev-test-environments.md).</span><span class="sxs-lookup"><span data-stu-id="088d2-139">For guidance on deploying your solution toodifferent environments, see [Development and test environments in Microsoft Azure](solution-dev-test-environments.md).</span></span>
* <span data-ttu-id="088d2-140">Pour obtenir des conseils comment les entreprises peuvent utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise - gouvernance de l’abonnement normative](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="088d2-140">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

