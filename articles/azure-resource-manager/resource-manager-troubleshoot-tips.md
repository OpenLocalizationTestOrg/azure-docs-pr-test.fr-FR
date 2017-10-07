---
title: "erreurs de déploiement Azure aaaUnderstand | Documents Microsoft"
description: "Décrit comment toolearn sur les erreurs de déploiement Azure."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Erreur de déploiement, déploiement d’azure, déployez tooazure"
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: a335e121e9b908a763374907e34b1f6e823d6e96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-deployment-errors"></a><span data-ttu-id="94c07-104">Comprendre les erreurs de déploiement Azure</span><span class="sxs-lookup"><span data-stu-id="94c07-104">Understand Azure deployment errors</span></span>
<span data-ttu-id="94c07-105">Cette rubrique décrit les erreurs de déploiement et vous explique comment obtenir plus d’informations sur une erreur.</span><span class="sxs-lookup"><span data-stu-id="94c07-105">This topic describes deployment errors and how you can discover more information about an error.</span></span> <span data-ttu-id="94c07-106">Pour des erreurs de déploiement toocommon résolutions, consultez [résoudre les erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="94c07-106">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="two-types-of-errors"></a><span data-ttu-id="94c07-107">Deux types d’erreur</span><span class="sxs-lookup"><span data-stu-id="94c07-107">Two types of errors</span></span>
<span data-ttu-id="94c07-108">Il existe deux types d’erreurs que vous pouvez rencontrer :</span><span class="sxs-lookup"><span data-stu-id="94c07-108">There are two types of errors you can receive:</span></span>

* <span data-ttu-id="94c07-109">des erreurs de validation</span><span class="sxs-lookup"><span data-stu-id="94c07-109">validation errors</span></span>
* <span data-ttu-id="94c07-110">des erreurs de déploiement</span><span class="sxs-lookup"><span data-stu-id="94c07-110">deployment errors</span></span>

<span data-ttu-id="94c07-111">Hello suivant image montre le journal d’activité hello pour un abonnement.</span><span class="sxs-lookup"><span data-stu-id="94c07-111">hello following image shows hello activity log for a subscription.</span></span> <span data-ttu-id="94c07-112">Deux déploiements sont représentés.</span><span class="sxs-lookup"><span data-stu-id="94c07-112">It represents two deployments.</span></span> <span data-ttu-id="94c07-113">Dans un déploiement, le modèle de hello validation a échoué (**Validate**) et ne pas été effectuée.</span><span class="sxs-lookup"><span data-stu-id="94c07-113">In one deployment, hello template failed validation (**Validate**) and did not proceed.</span></span> <span data-ttu-id="94c07-114">Dans hello autre déploiement, modèle de hello ont réussi la validation, mais a échoué lors de la création de ressources de hello (**écrire des déploiements**).</span><span class="sxs-lookup"><span data-stu-id="94c07-114">In hello other deployment, hello template passed validation but failed when creating hello resources (**Write Deployments**).</span></span> 

![afficher le code d'erreur](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

<span data-ttu-id="94c07-116">Les erreurs de validation sont liées à des scénarios pouvant être identifiés avant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="94c07-116">Validation errors arise from scenarios that can be determined before deployment.</span></span> <span data-ttu-id="94c07-117">Elles incluent des erreurs de syntaxe dans votre modèle, ou lors de la tentative ressources toodeploy dépassent vos quotas d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="94c07-117">They include syntax errors in your template, or trying toodeploy resources that would exceed your subscription quotas.</span></span> <span data-ttu-id="94c07-118">Erreurs de déploiement sont dues aux conditions qui se produisent pendant le processus de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="94c07-118">Deployment errors arise from conditions that occur during hello deployment process.</span></span> <span data-ttu-id="94c07-119">Ils comprennent la tentative de tooaccess une ressource qui est déployée en parallèle.</span><span class="sxs-lookup"><span data-stu-id="94c07-119">They include trying tooaccess a resource that is being deployed in parallel.</span></span>

<span data-ttu-id="94c07-120">Les deux types de retour d’erreurs que vous utilisez tootroubleshoot hello déploiement un code d’erreur.</span><span class="sxs-lookup"><span data-stu-id="94c07-120">Both types of errors return an error code that you use tootroubleshoot hello deployment.</span></span> <span data-ttu-id="94c07-121">Les deux types d’erreurs s’affichent dans hello [le journal d’activité](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="94c07-121">Both types of errors appear in hello [activity log](resource-group-audit.md).</span></span> <span data-ttu-id="94c07-122">Toutefois, les erreurs de validation n’apparaissent pas dans l’historique de votre déploiement, car le déploiement de hello jamais démarré.</span><span class="sxs-lookup"><span data-stu-id="94c07-122">However, validation errors do not appear in your deployment history because hello deployment never started.</span></span>

## <a name="determine-error-code"></a><span data-ttu-id="94c07-123">Déterminer le code d’erreur</span><span class="sxs-lookup"><span data-stu-id="94c07-123">Determine error code</span></span>

<span data-ttu-id="94c07-124">Vous pouvez en savoir plus sur une erreur en examinant de message d’erreur hello et code d’erreur hello.</span><span class="sxs-lookup"><span data-stu-id="94c07-124">You can learn about an error by looking at hello error message and hello error code.</span></span> <span data-ttu-id="94c07-125">Hello [résoudre les erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md) article répertorie les résolutions par code d’erreur.</span><span class="sxs-lookup"><span data-stu-id="94c07-125">hello [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md) article lists resolutions by error code.</span></span> <span data-ttu-id="94c07-126">Cette rubrique montre comment toouse hello le code d’erreur hello toodiscover portail Azure.</span><span class="sxs-lookup"><span data-stu-id="94c07-126">This topic shows how toouse hello Azure portal toodiscover hello error code.</span></span>

### <a name="validation-errors"></a><span data-ttu-id="94c07-127">Erreurs de validation</span><span class="sxs-lookup"><span data-stu-id="94c07-127">Validation errors</span></span>

<span data-ttu-id="94c07-128">Lors du déploiement via le portail de hello, vous voyez une erreur de validation après avoir soumis vos valeurs.</span><span class="sxs-lookup"><span data-stu-id="94c07-128">When deploying through hello portal, you see a validation error after submitting your values.</span></span>

![afficher l’erreur de validation dans le portail](./media/resource-manager-troubleshoot-tips/validation-error.png)

<span data-ttu-id="94c07-130">Sélectionnez le message de type hello pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="94c07-130">Select hello message for more details.</span></span> <span data-ttu-id="94c07-131">Bonjour suivant l’image, vous voyez un **InvalidTemplateDeployment** d’erreur et un message qui indique une stratégie de déploiement bloqué.</span><span class="sxs-lookup"><span data-stu-id="94c07-131">In hello following image, you see an **InvalidTemplateDeployment** error and a message that indicates a policy blocked deployment.</span></span>

![afficher les détails de validation](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a><span data-ttu-id="94c07-133">Erreurs de déploiement</span><span class="sxs-lookup"><span data-stu-id="94c07-133">Deployment errors</span></span>

<span data-ttu-id="94c07-134">Lors de l’opération de hello passe la validation, mais échoue pendant le déploiement, vous voyez erreur hello dans les notifications de hello.</span><span class="sxs-lookup"><span data-stu-id="94c07-134">When hello operation passes validation, but fails during deployment, you see hello error in hello notifications.</span></span> <span data-ttu-id="94c07-135">Sélectionnez hello notification.</span><span class="sxs-lookup"><span data-stu-id="94c07-135">Select hello notification.</span></span>

![erreur de notification](./media/resource-manager-troubleshoot-tips/notification.png)

<span data-ttu-id="94c07-137">Vous voyez plus d’informations sur le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="94c07-137">You see more details about hello deployment.</span></span> <span data-ttu-id="94c07-138">Sélectionnez hello option toofind plus d’informations sur l’erreur de hello.</span><span class="sxs-lookup"><span data-stu-id="94c07-138">Select hello option toofind more information about hello error.</span></span>

![échec du déploiement](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

<span data-ttu-id="94c07-140">Vous consultez codes d’erreur et le message d’erreur hello.</span><span class="sxs-lookup"><span data-stu-id="94c07-140">You see hello error message and error codes.</span></span> <span data-ttu-id="94c07-141">Notez qu’il y a deux codes d’erreur.</span><span class="sxs-lookup"><span data-stu-id="94c07-141">Notice there are two error codes.</span></span> <span data-ttu-id="94c07-142">Hello premier code d’erreur (**DeploymentFailed**) est une erreur générale qui ne fournit pas de hello détails que vous avez besoin d’erreur de hello toosolve.</span><span class="sxs-lookup"><span data-stu-id="94c07-142">hello first error code (**DeploymentFailed**) is a general error that does not provide hello details you need toosolve hello error.</span></span> <span data-ttu-id="94c07-143">Hello deuxième code d’erreur (**StorageAccountNotFound**) fournit des détails hello vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="94c07-143">hello second error code (**StorageAccountNotFound**) provides hello details you need.</span></span> 

![détails de l’erreur](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a><span data-ttu-id="94c07-145">Activer l’enregistrement du débogage</span><span class="sxs-lookup"><span data-stu-id="94c07-145">Enable debug logging</span></span>
<span data-ttu-id="94c07-146">Vous devez parfois plus d’informations sur toodiscover de demande et de réponse hello cause du problème.</span><span class="sxs-lookup"><span data-stu-id="94c07-146">Sometimes you need more information about hello request and response toodiscover what went wrong.</span></span> <span data-ttu-id="94c07-147">Avec PowerShell ou l’interface de ligne de commande Azure, vous pouvez demander la journalisation d’informations supplémentaires lors d’un déploiement.</span><span class="sxs-lookup"><span data-stu-id="94c07-147">By using PowerShell or Azure CLI, you can request that additional information is logged during a deployment.</span></span>

- <span data-ttu-id="94c07-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="94c07-148">PowerShell</span></span>

   <span data-ttu-id="94c07-149">Dans PowerShell, définissez hello **DeploymentDebugLogLevel** tooAll de paramètre, le ResponseContent ou RequestContent.</span><span class="sxs-lookup"><span data-stu-id="94c07-149">In PowerShell, set hello **DeploymentDebugLogLevel** parameter tooAll, ResponseContent, or RequestContent.</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   <span data-ttu-id="94c07-150">Examinez le contenu de demande de hello avec hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="94c07-150">Examine hello request content with hello following cmdlet:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   <span data-ttu-id="94c07-151">Ou bien, hello du contenu à l’aide de la réponse :</span><span class="sxs-lookup"><span data-stu-id="94c07-151">Or, hello response content with:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   <span data-ttu-id="94c07-152">Ces informations peuvent vous aider à déterminer si une valeur dans le modèle de hello est incorrectement définie.</span><span class="sxs-lookup"><span data-stu-id="94c07-152">This information can help you determine whether a value in hello template is being incorrectly set.</span></span>

- <span data-ttu-id="94c07-153">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="94c07-153">Azure CLI</span></span>

   <span data-ttu-id="94c07-154">Examiner les opérations de déploiement hello avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="94c07-154">Examine hello deployment operations with hello following command:</span></span>

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- <span data-ttu-id="94c07-155">Modèle imbriqué</span><span class="sxs-lookup"><span data-stu-id="94c07-155">Nested template</span></span>

   <span data-ttu-id="94c07-156">toolog les informations de débogage pour un modèle imbriqué, utilisez hello **debugSetting** élément.</span><span class="sxs-lookup"><span data-stu-id="94c07-156">toolog debug information for a nested template, use hello **debugSetting** element.</span></span>

  ```json
  {
      "apiVersion": "2016-09-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
          "mode": "Incremental",
          "templateLink": {
              "uri": "{template-uri}",
              "contentVersion": "1.0.0.0"
          },
          "debugSetting": {
             "detailLevel": "requestContent, responseContent"
          }
      }
  }
  ```


## <a name="create-a-troubleshooting-template"></a><span data-ttu-id="94c07-157">Création d’un modèle de résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="94c07-157">Create a troubleshooting template</span></span>
<span data-ttu-id="94c07-158">Dans certains cas, hello tootroubleshoot de façon plus simple votre modèle est tootest des parties de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="94c07-158">In some cases, hello easiest way tootroubleshoot your template is tootest parts of it.</span></span> <span data-ttu-id="94c07-159">Vous pouvez créer un modèle simplifié qui vous permet de toofocus sur la partie hello que vous pensez être provoque l’erreur de hello.</span><span class="sxs-lookup"><span data-stu-id="94c07-159">You can create a simplified template that enables you toofocus on hello part that you believe is causing hello error.</span></span> <span data-ttu-id="94c07-160">Par exemple, supposons que vous recevez une erreur lorsque vous référencez une ressource.</span><span class="sxs-lookup"><span data-stu-id="94c07-160">For example, suppose you are receiving an error when referencing a resource.</span></span> <span data-ttu-id="94c07-161">Au lieu de traiter un modèle complet, créez un modèle qui retourne une partie hello qui peut être à l’origine de votre problème.</span><span class="sxs-lookup"><span data-stu-id="94c07-161">Rather than dealing with an entire template, create a template that returns hello part that may be causing your problem.</span></span> <span data-ttu-id="94c07-162">Il peut vous aider à déterminer si vous passez dans les paramètres appropriés de hello, à l’aide des fonctions de modèle correctement, et obtention de la ressource de hello souhaitées.</span><span class="sxs-lookup"><span data-stu-id="94c07-162">It can help you determine whether you are passing in hello right parameters, using template functions correctly, and getting hello resource you expect.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageName": {
        "type": "string"
    },
    "storageResourceGroup": {
        "type": "string"
    }
  },
  "variables": {},
  "resources": [],
  "outputs": {
    "exampleOutput": {
        "value": "[reference(resourceId(parameters('storageResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('storageName')), '2016-05-01')]",
        "type" : "object"
    }
  }
}
```

<span data-ttu-id="94c07-163">Ou bien, supposons que vous rencontrez des erreurs de déploiement que vous pensez être liés tooincorrectly définir des dépendances.</span><span class="sxs-lookup"><span data-stu-id="94c07-163">Or, suppose you are encountering deployment errors that you believe are related tooincorrectly set dependencies.</span></span> <span data-ttu-id="94c07-164">vous pouvez tester votre modèle en le divisant en modèles plus simples.</span><span class="sxs-lookup"><span data-stu-id="94c07-164">Test your template by breaking it into simplified templates.</span></span> <span data-ttu-id="94c07-165">Commencez par créer un modèle déployant une seule ressource (comme un serveur SQL Server).</span><span class="sxs-lookup"><span data-stu-id="94c07-165">First, create a template that deploys only a single resource (like a SQL Server).</span></span> <span data-ttu-id="94c07-166">Lorsque vous êtes sûr que cette ressource est correctement définie, ajoutez une ressource qui en dépend (par exemple une base de données SQL).</span><span class="sxs-lookup"><span data-stu-id="94c07-166">When you are sure you have that resource correctly defined, add a resource that depends on it (like a SQL Database).</span></span> <span data-ttu-id="94c07-167">Une fois ces deux ressources correctement définies, ajoutez les autres ressources dépendantes (telles que les stratégies d’audit).</span><span class="sxs-lookup"><span data-stu-id="94c07-167">When you have those two resources correctly defined, add other dependent resources (like auditing policies).</span></span> <span data-ttu-id="94c07-168">Entre chaque déploiement de test, supprimez hello groupe toomake que vous correctement test hello des dépendances de ressource.</span><span class="sxs-lookup"><span data-stu-id="94c07-168">In between each test deployment, delete hello resource group toomake sure you adequately testing hello dependencies.</span></span> 

## <a name="check-deployment-sequence"></a><span data-ttu-id="94c07-169">Vérifier la séquence de déploiement</span><span class="sxs-lookup"><span data-stu-id="94c07-169">Check deployment sequence</span></span>

<span data-ttu-id="94c07-170">De nombreuses erreurs de déploiement se produisent lorsque des ressources sont déployées selon une séquence inattendue.</span><span class="sxs-lookup"><span data-stu-id="94c07-170">Many deployment errors happen when resources are deployed in an unexpected sequence.</span></span> <span data-ttu-id="94c07-171">Ces erreurs surviennent lorsque les dépendances ne sont pas définies correctement.</span><span class="sxs-lookup"><span data-stu-id="94c07-171">These errors arise when dependencies are not correctly set.</span></span> <span data-ttu-id="94c07-172">Lorsqu’il manque une dépendance nécessaire, une ressource tentatives toouse qu'une valeur pour une autre ressource mais hello autres n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="94c07-172">When you are missing a needed dependency, one resource attempts toouse a value for another resource but hello other does not yet exist.</span></span> <span data-ttu-id="94c07-173">Vous obtenez une erreur indiquant qu’une ressource est introuvable.</span><span class="sxs-lookup"><span data-stu-id="94c07-173">You get an error stating that a resource is not found.</span></span> <span data-ttu-id="94c07-174">Si vous rencontrez ce type d’erreur par intermittence, car le temps de déploiement hello pour chaque ressource peut varier.</span><span class="sxs-lookup"><span data-stu-id="94c07-174">You may encounter this type of error intermittently because hello deployment time for each resource can vary.</span></span> <span data-ttu-id="94c07-175">Par exemple, votre premier toodeploy de tentative de vos ressources réussit car une ressource requise se termine de façon aléatoire dans le temps.</span><span class="sxs-lookup"><span data-stu-id="94c07-175">For example, your first attempt toodeploy your resources succeeds because a required resource randomly completes in time.</span></span> <span data-ttu-id="94c07-176">Toutefois, votre deuxième tentative échoue car hello requis de ressource ne s’est pas terminée dans le temps.</span><span class="sxs-lookup"><span data-stu-id="94c07-176">However, your second attempt fails because hello required resource did not complete in time.</span></span> 

<span data-ttu-id="94c07-177">Toutefois, vous souhaitez que les dépendances de paramètre tooavoid qui ne sont pas nécessaires.</span><span class="sxs-lookup"><span data-stu-id="94c07-177">But, you want tooavoid setting dependencies that are not needed.</span></span> <span data-ttu-id="94c07-178">Lorsque vous avez des dépendances inutiles, vous prolonger la durée hello du déploiement de hello en empêchant les ressources qui ne sont pas dépendants sur eux d’être déployé en parallèle.</span><span class="sxs-lookup"><span data-stu-id="94c07-178">When you have unnecessary dependencies, you prolong hello duration of hello deployment by preventing resources that are not dependent on each other from being deployed in parallel.</span></span> <span data-ttu-id="94c07-179">En outre, vous pouvez créer des dépendances circulaires qui bloquent le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="94c07-179">In addition, you may create circular dependencies that block hello deployment.</span></span> <span data-ttu-id="94c07-180">Hello [référence](resource-group-template-functions-resource.md#reference) fonction crée une dépendance implicite sur la ressource hello référencée lorsque cette ressource est déployée dans hello même modèle.</span><span class="sxs-lookup"><span data-stu-id="94c07-180">hello [reference](resource-group-template-functions-resource.md#reference) function creates an implicit dependency on hello referenced resource, when that resource is deployed in hello same template.</span></span> <span data-ttu-id="94c07-181">Par conséquent, vous pouvez avoir des dépendances plus que les dépendances de hello spécifiés dans hello **dependsOn** propriété.</span><span class="sxs-lookup"><span data-stu-id="94c07-181">Therefore, you may have more dependencies than hello dependencies specified in hello **dependsOn** property.</span></span> <span data-ttu-id="94c07-182">Hello [resourceId](resource-group-template-functions-resource.md#resourceid) fonction ne pas créer une relation implicite ou valider l’existence de la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="94c07-182">hello [resourceId](resource-group-template-functions-resource.md#resourceid) function does not create an implicit dependency or validate that hello resource exists.</span></span>

<span data-ttu-id="94c07-183">Lorsque vous rencontrez des problèmes de dépendance, vous devez toogain idée commande hello de déploiement de ressources.</span><span class="sxs-lookup"><span data-stu-id="94c07-183">When you encounter dependency problems, you need toogain insight into hello order of resource deployment.</span></span> <span data-ttu-id="94c07-184">ordre de hello tooview d’opérations de déploiement :</span><span class="sxs-lookup"><span data-stu-id="94c07-184">tooview hello order of deployment operations:</span></span>

1. <span data-ttu-id="94c07-185">Sélectionnez l’historique de déploiement hello pour votre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="94c07-185">Select hello deployment history for your resource group.</span></span>

   ![sélectionner l’historique de déploiement](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. <span data-ttu-id="94c07-187">Sélectionnez un déploiement à partir de l’historique de hello, puis sélectionnez **événements**.</span><span class="sxs-lookup"><span data-stu-id="94c07-187">Select a deployment from hello history, and select **Events**.</span></span>

   ![sélectionner les événements de déploiement](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. <span data-ttu-id="94c07-189">Examiner la séquence de hello d’événements pour chaque ressource.</span><span class="sxs-lookup"><span data-stu-id="94c07-189">Examine hello sequence of events for each resource.</span></span> <span data-ttu-id="94c07-190">État de toohello attention de chaque opération de paie.</span><span class="sxs-lookup"><span data-stu-id="94c07-190">Pay attention toohello status of each operation.</span></span> <span data-ttu-id="94c07-191">Par exemple, hello image suivante montre trois comptes de stockage déploiement en parallèle.</span><span class="sxs-lookup"><span data-stu-id="94c07-191">For example, hello following image shows three storage accounts that deployed in parallel.</span></span> <span data-ttu-id="94c07-192">Notez que hello trois comptes de stockage sont démarrés à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="94c07-192">Notice that hello three storage accounts are started at hello same time.</span></span>

   ![déploiement en parallèle](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   <span data-ttu-id="94c07-194">image de Hello suivant montre trois comptes de stockage qui ne sont pas déployés en parallèle.</span><span class="sxs-lookup"><span data-stu-id="94c07-194">hello next image shows three storage accounts that are not deployed in parallel.</span></span> <span data-ttu-id="94c07-195">compte de stockage deuxième Hello varie selon le premier compte de stockage hello et compte de stockage tiers hello dépend de la deuxième compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="94c07-195">hello second storage account depends on hello first storage account, and hello third storage account depends on hello second storage account.</span></span> <span data-ttu-id="94c07-196">Par conséquent, premier compte de stockage hello est démarré, accepté et s’est terminée avant hello est redémarrée.</span><span class="sxs-lookup"><span data-stu-id="94c07-196">Therefore, hello first storage account is started, accepted, and completed before hello next is started.</span></span>

   ![déploiement séquentiel](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

<span data-ttu-id="94c07-198">Même pour les scénarios plus complexes, vous pouvez utiliser hello même technique toodiscover lorsque le déploiement est démarré et s’est terminée pour chaque ressource.</span><span class="sxs-lookup"><span data-stu-id="94c07-198">Even for more complicated scenarios, you can use hello same technique toodiscover when deployment is started and completed for each resource.</span></span> <span data-ttu-id="94c07-199">Examinez votre toosee d’événements de déploiement si la séquence de hello est différente de celle attendue.</span><span class="sxs-lookup"><span data-stu-id="94c07-199">Look through your deployment events toosee if hello sequence is different than you would expect.</span></span> <span data-ttu-id="94c07-200">Dans ce cas, réévaluez les dépendances hello pour cette ressource.</span><span class="sxs-lookup"><span data-stu-id="94c07-200">If so, reevaluate hello dependencies for this resource.</span></span>

<span data-ttu-id="94c07-201">Resource Manager identifie les dépendances circulaires lors de la validation du modèle.</span><span class="sxs-lookup"><span data-stu-id="94c07-201">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="94c07-202">Il renvoie un message d’erreur indiquant spécifiquement qu’il existe une dépendance circulaire.</span><span class="sxs-lookup"><span data-stu-id="94c07-202">It returns an error message that specifically states a circular dependency exists.</span></span> <span data-ttu-id="94c07-203">toosolve une dépendance circulaire :</span><span class="sxs-lookup"><span data-stu-id="94c07-203">toosolve a circular dependency:</span></span>

1. <span data-ttu-id="94c07-204">Dans votre modèle, de trouver la ressource hello identifié une dépendance circulaire hello.</span><span class="sxs-lookup"><span data-stu-id="94c07-204">In your template, find hello resource identified in hello circular dependency.</span></span> 
2. <span data-ttu-id="94c07-205">Pour cette ressource, examinez hello **dependsOn** propriété et toutes les utilisations de hello **référence** toosee les ressources dont il dépend de la fonction.</span><span class="sxs-lookup"><span data-stu-id="94c07-205">For that resource, examine hello **dependsOn** property and any uses of hello **reference** function toosee which resources it depends on.</span></span> 
3. <span data-ttu-id="94c07-206">Examinez ces toosee de ressources que les ressources dont ils dépendent.</span><span class="sxs-lookup"><span data-stu-id="94c07-206">Examine those resources toosee which resources they depend on.</span></span> <span data-ttu-id="94c07-207">Suivre les dépendances de hello jusqu'à ce que vous remarquez une ressource dont dépend la ressource d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="94c07-207">Follow hello dependencies until you notice a resource that depends on hello original resource.</span></span>
5. <span data-ttu-id="94c07-208">Pour les ressources de hello impliquées dans une dépendance circulaire hello, examinez attentivement toutes les utilisations de hello **dependsOn** propriété tooidentify toutes les dépendances qui ne sont pas nécessaires.</span><span class="sxs-lookup"><span data-stu-id="94c07-208">For hello resources involved in hello circular dependency, carefully examine all uses of hello **dependsOn** property tooidentify any dependencies that are not needed.</span></span> <span data-ttu-id="94c07-209">Supprimer ces dépendances.</span><span class="sxs-lookup"><span data-stu-id="94c07-209">Remove those dependencies.</span></span> <span data-ttu-id="94c07-210">Si vous n’êtes pas certain qu’une dépendance soit nécessaire, essayez de la supprimer.</span><span class="sxs-lookup"><span data-stu-id="94c07-210">If you are unsure that a dependency is needed, try removing it.</span></span> 
6. <span data-ttu-id="94c07-211">Redéployez le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="94c07-211">Redeploy hello template.</span></span>

<span data-ttu-id="94c07-212">Suppression des valeurs de hello **dependsOn** propriété peut provoquer des erreurs lorsque vous déployez le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="94c07-212">Removing values from hello **dependsOn** property can cause errors when you deploy hello template.</span></span> <span data-ttu-id="94c07-213">Si vous rencontrez une erreur, ajoutez la dépendance hello dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="94c07-213">If you encounter an error, add hello dependency back into hello template.</span></span> 

<span data-ttu-id="94c07-214">Si cette approche ne résout pas une dépendance circulaire hello, déplacez la partie de votre logique de déploiement dans les ressources enfants (par exemple, des extensions ou des paramètres de configuration).</span><span class="sxs-lookup"><span data-stu-id="94c07-214">If that approach does not solve hello circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span></span> <span data-ttu-id="94c07-215">Configurer les toodeploy de ressources enfant après ressources hello impliquées dans une dépendance circulaire hello.</span><span class="sxs-lookup"><span data-stu-id="94c07-215">Configure those child resources toodeploy after hello resources involved in hello circular dependency.</span></span> <span data-ttu-id="94c07-216">Par exemple, supposons que vous déployez deux machines virtuelles, mais vous devez définir des propriétés sur chacun d’eux qui font référence toohello autres.</span><span class="sxs-lookup"><span data-stu-id="94c07-216">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="94c07-217">Vous pouvez les déployer dans hello suivant l’ordre :</span><span class="sxs-lookup"><span data-stu-id="94c07-217">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="94c07-218">Machine virtuelle 1</span><span class="sxs-lookup"><span data-stu-id="94c07-218">vm1</span></span>
2. <span data-ttu-id="94c07-219">Machine virtuelle 2</span><span class="sxs-lookup"><span data-stu-id="94c07-219">vm2</span></span>
3. <span data-ttu-id="94c07-220">L’extension sur la machine virtuelle 1 dépend des machines virtuelles 1 et 2.</span><span class="sxs-lookup"><span data-stu-id="94c07-220">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="94c07-221">extension de Hello définit des valeurs sur vm1 qu’il obtient à partir de l’ordinateur virtuel 2.</span><span class="sxs-lookup"><span data-stu-id="94c07-221">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="94c07-222">L’extension sur la machine virtuelle 2 dépend des machines virtuelles 1 et 2.</span><span class="sxs-lookup"><span data-stu-id="94c07-222">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="94c07-223">extension de Hello définit des valeurs sur vm2 qu’il obtient de vm1.</span><span class="sxs-lookup"><span data-stu-id="94c07-223">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="94c07-224">Hello même approche fonctionne pour les applications de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="94c07-224">hello same approach works for App Service apps.</span></span> <span data-ttu-id="94c07-225">Envisagez de passer des valeurs de configuration dans une ressource enfant de ressource d’application hello.</span><span class="sxs-lookup"><span data-stu-id="94c07-225">Consider moving configuration values into a child resource of hello app resource.</span></span> <span data-ttu-id="94c07-226">Vous pouvez déployer des applications web deux Bonjour suivant l’ordre :</span><span class="sxs-lookup"><span data-stu-id="94c07-226">You can deploy two web apps in hello following order:</span></span>

1. <span data-ttu-id="94c07-227">Application web 1</span><span class="sxs-lookup"><span data-stu-id="94c07-227">webapp1</span></span>
2. <span data-ttu-id="94c07-228">Application web 2</span><span class="sxs-lookup"><span data-stu-id="94c07-228">webapp2</span></span>
3. <span data-ttu-id="94c07-229">La configuration de l’application web 1 dépend des applications web 1 et 2.</span><span class="sxs-lookup"><span data-stu-id="94c07-229">config for webapp1 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="94c07-230">Elle contient des paramètres d’application avec les valeurs de l’application web 2.</span><span class="sxs-lookup"><span data-stu-id="94c07-230">It contains app settings with values from webapp2.</span></span>
4. <span data-ttu-id="94c07-231">La configuration de l’application web 2 dépend des applications web 1 et 2.</span><span class="sxs-lookup"><span data-stu-id="94c07-231">config for webapp2 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="94c07-232">Elle contient des paramètres d’application avec les valeurs de l’application web 1.</span><span class="sxs-lookup"><span data-stu-id="94c07-232">It contains app settings with values from webapp1.</span></span>


## <a name="next-steps"></a><span data-ttu-id="94c07-233">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="94c07-233">Next steps</span></span>
* <span data-ttu-id="94c07-234">Pour des erreurs de déploiement toocommon résolutions, consultez [résoudre les erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="94c07-234">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="94c07-235">toolearn sur l’audit des actions, consultez [auditer les opérations effectuées avec le Gestionnaire de ressources](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="94c07-235">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="94c07-236">toolearn sur les erreurs de hello toodetermine actions pendant le déploiement, consultez [afficher les opérations de déploiement](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="94c07-236">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
