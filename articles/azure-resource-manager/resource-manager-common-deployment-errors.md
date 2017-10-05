---
title: "Résolution des erreurs courantes lors du déploiement Azure | Microsoft Docs"
description: "Décrit comment résoudre les erreurs courantes lors du déploiement de ressources sur Azure à l’aide d’Azure Resource Manager."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "erreur de déploiement, déploiement Azure, déployer dans azure"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 30adc10d01290f14a3e116813b19916fa36ab0bc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="3f04b-104">Résolution des erreurs courantes dans des déploiements Azure avec Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3f04b-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="3f04b-105">Cette rubrique décrit comment résoudre certaines erreurs courantes liées au déploiement d’Azure que vous pouvez rencontrer.</span><span class="sxs-lookup"><span data-stu-id="3f04b-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

<span data-ttu-id="3f04b-106">Les codes d’erreur suivants sont décrits dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="3f04b-106">The following error codes are described in this topic:</span></span>

* [<span data-ttu-id="3f04b-107">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="3f04b-107">AccountNameInvalid</span></span>](#accountnameinvalid)
* [<span data-ttu-id="3f04b-108">Échec de l’autorisation</span><span class="sxs-lookup"><span data-stu-id="3f04b-108">Authorization failed</span></span>](#authorization-failed)
* [<span data-ttu-id="3f04b-109">BadRequest</span><span class="sxs-lookup"><span data-stu-id="3f04b-109">BadRequest</span></span>](#badrequest)
* [<span data-ttu-id="3f04b-110">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="3f04b-110">DeploymentFailed</span></span>](#deploymentfailed)
* [<span data-ttu-id="3f04b-111">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="3f04b-111">DisallowedOperation</span></span>](#disallowedoperation)
* [<span data-ttu-id="3f04b-112">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="3f04b-112">InvalidContentLink</span></span>](#invalidcontentlink)
* [<span data-ttu-id="3f04b-113">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="3f04b-113">InvalidTemplate</span></span>](#invalidtemplate)
* [<span data-ttu-id="3f04b-114">MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="3f04b-114">MissingSubscriptionRegistration</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="3f04b-115">NotFound</span><span class="sxs-lookup"><span data-stu-id="3f04b-115">NotFound</span></span>](#notfound)
* [<span data-ttu-id="3f04b-116">NoRegisteredProviderFound</span><span class="sxs-lookup"><span data-stu-id="3f04b-116">NoRegisteredProviderFound</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="3f04b-117">OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="3f04b-117">OperationNotAllowed</span></span>](#quotaexceeded)
* [<span data-ttu-id="3f04b-118">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="3f04b-118">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* [<span data-ttu-id="3f04b-119">QuotaExceeded</span><span class="sxs-lookup"><span data-stu-id="3f04b-119">QuotaExceeded</span></span>](#quotaexceeded)
* [<span data-ttu-id="3f04b-120">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="3f04b-120">RequestDisallowedByPolicy</span></span>](#requestdisallowedbypolicy)
* [<span data-ttu-id="3f04b-121">ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="3f04b-121">ResourceNotFound</span></span>](#notfound)
* [<span data-ttu-id="3f04b-122">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="3f04b-122">SkuNotAvailable</span></span>](#skunotavailable)
* [<span data-ttu-id="3f04b-123">StorageAccountAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="3f04b-123">StorageAccountAlreadyExists</span></span>](#storagenamenotunique)
* [<span data-ttu-id="3f04b-124">StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="3f04b-124">StorageAccountAlreadyTaken</span></span>](#storagenamenotunique)

## <a name="deploymentfailed"></a><span data-ttu-id="3f04b-125">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="3f04b-125">DeploymentFailed</span></span>

<span data-ttu-id="3f04b-126">Ce code d’erreur indique une erreur de déploiement générale, mais il ne s’agit pas du code d’erreur dont vous avez besoin pour la résolution du problème.</span><span class="sxs-lookup"><span data-stu-id="3f04b-126">This error code indicates a general deployment error, but it is not the error code you need to start troubleshooting.</span></span> <span data-ttu-id="3f04b-127">Le code d’erreur qui vous permet de résoudre le problème se trouve généralement à un niveau en dessous de cette erreur.</span><span class="sxs-lookup"><span data-stu-id="3f04b-127">The error code that actually helps you resolve the issue is usually one level below this error.</span></span> <span data-ttu-id="3f04b-128">Par exemple, l’illustration suivante montre le code d’erreur **RequestDisallowedByPolicy** qui se trouve sous l’erreur de déploiement.</span><span class="sxs-lookup"><span data-stu-id="3f04b-128">For example, the following image shows the **RequestDisallowedByPolicy** error code that is under the deployment error.</span></span>

![afficher le code d'erreur](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a><span data-ttu-id="3f04b-130">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="3f04b-130">SkuNotAvailable</span></span>

<span data-ttu-id="3f04b-131">Lors du déploiement d’une ressource (généralement une machine virtuelle), vous pouvez recevoir le message et le code d’erreur suivants :</span><span class="sxs-lookup"><span data-stu-id="3f04b-131">When deploying a resource (typically a virtual machine), you may receive the following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: The requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy to a different location.
```

<span data-ttu-id="3f04b-132">Vous recevez cette erreur lorsque la ressource de référence (SKU) que vous avez sélectionnée (par exemple, la taille de la machine virtuelle) n’est pas disponible pour l’emplacement que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="3f04b-132">You receive this error when the resource SKU you have selected (such as VM size) is not available for the location you have selected.</span></span> <span data-ttu-id="3f04b-133">Pour résoudre ce problème, vous devez déterminer quelles références sont disponibles dans une région.</span><span class="sxs-lookup"><span data-stu-id="3f04b-133">To resolve this issue, you need to determine which SKUs are available in a region.</span></span> <span data-ttu-id="3f04b-134">Pour identifier les références disponibles, vous pouvez utiliser PowerShell, le portail ou une opération REST.</span><span class="sxs-lookup"><span data-stu-id="3f04b-134">You can use PowerShell, the portal, or a REST operation to find available SKUs.</span></span>

- <span data-ttu-id="3f04b-135">Pour PowerShell, utilisez [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) et filtrez par emplacement.</span><span class="sxs-lookup"><span data-stu-id="3f04b-135">For PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) and filter by location.</span></span> <span data-ttu-id="3f04b-136">Pour cette commande, vous devez disposer de la version la plus récente de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3f04b-136">You must have the latest version of PowerShell for this command.</span></span>

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  <span data-ttu-id="3f04b-137">Les résultats incluent une liste de références pour l’emplacement et toutes les restrictions éventuellement liées aux références concernées.</span><span class="sxs-lookup"><span data-stu-id="3f04b-137">The results include a list of SKUs for the location and any restrictions for that SKU.</span></span>

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- <span data-ttu-id="3f04b-138">Pour utiliser le [portail](https://portal.azure.com), connectez-vous au portail et ajoutez une ressource à l’aide de l’interface.</span><span class="sxs-lookup"><span data-stu-id="3f04b-138">To use the [portal](https://portal.azure.com), log in to the portal and add a resource through the interface.</span></span> <span data-ttu-id="3f04b-139">Lorsque vous définissez les valeurs, vous voyez les références (SKU) disponibles pour cette ressource.</span><span class="sxs-lookup"><span data-stu-id="3f04b-139">As you set the values, you see the available SKUs for that resource.</span></span> <span data-ttu-id="3f04b-140">Vous n’avez pas besoin de terminer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="3f04b-140">You do not need to complete the deployment.</span></span>

    ![Références disponibles](./media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="3f04b-142">Pour utiliser l’API REST pour des machines virtuelles, envoyez la demande suivante :</span><span class="sxs-lookup"><span data-stu-id="3f04b-142">To use the REST API for virtual machines, send the following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="3f04b-143">Elle renvoie les références et les régions disponibles dans le format suivant :</span><span class="sxs-lookup"><span data-stu-id="3f04b-143">It returns available SKUs and regions in the following format:</span></span>

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

<span data-ttu-id="3f04b-144">Si vous ne parvenez pas à trouver une référence appropriée dans cette région ou une autre qui réponde aux besoins de votre entreprise, envoyez une [demande de référence SKU](https://aka.ms/skurestriction) au support Azure.</span><span class="sxs-lookup"><span data-stu-id="3f04b-144">If you are unable to find a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) to Azure Support.</span></span>

## <a name="disallowedoperation"></a><span data-ttu-id="3f04b-145">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="3f04b-145">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: The current subscription type is not permitted to perform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="3f04b-146">Si vous recevez cette erreur, vous utilisez un abonnement qui n’est pas autorisé à accéder à des services Azure autres qu’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3f04b-146">If you receive this error, you are using a subscription that is not permitted to access any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="3f04b-147">Vous pouvez avoir ce type d’abonnement lorsque vous avez besoin d’accéder au Portail Classic mais que vous n’êtes pas autorisé à déployer des ressources.</span><span class="sxs-lookup"><span data-stu-id="3f04b-147">You might have this type of subscription when you need to access the classic portal but are not permitted to deploy resources.</span></span> <span data-ttu-id="3f04b-148">Pour résoudre ce problème, vous devez utiliser un abonnement qui dispose de l’autorisation de déployer des ressources.</span><span class="sxs-lookup"><span data-stu-id="3f04b-148">To resolve this issue, you must use a subscription that has permission to deploy resources.</span></span>  

<span data-ttu-id="3f04b-149">Pour afficher vos abonnements disponibles avec PowerShell, utilisez :</span><span class="sxs-lookup"><span data-stu-id="3f04b-149">To view your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="3f04b-150">Pour définir l’abonnement actif, utilisez :</span><span class="sxs-lookup"><span data-stu-id="3f04b-150">And, to set the current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="3f04b-151">Pour afficher vos abonnements disponibles avec Azure CLI 2.0, utilisez :</span><span class="sxs-lookup"><span data-stu-id="3f04b-151">To view your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="3f04b-152">Pour définir l’abonnement actif, utilisez :</span><span class="sxs-lookup"><span data-stu-id="3f04b-152">And, to set the current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a><span data-ttu-id="3f04b-153">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="3f04b-153">InvalidTemplate</span></span>
<span data-ttu-id="3f04b-154">Cette erreur peut résulter de différents types d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="3f04b-154">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="3f04b-155">Erreur de syntaxe</span><span class="sxs-lookup"><span data-stu-id="3f04b-155">Syntax error</span></span>

   <span data-ttu-id="3f04b-156">Si vous recevez un message d’erreur qui indique que la validation du modèle a échoué, vous avez peut-être un problème de syntaxe dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="3f04b-156">If you receive an error message that indicates the template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="3f04b-157">Cette erreur est facile à commettre car les expressions de modèle peuvent être complexes.</span><span class="sxs-lookup"><span data-stu-id="3f04b-157">This error is easy to make because template expressions can be intricate.</span></span> <span data-ttu-id="3f04b-158">Par exemple, l’affectation de nom suivante pour un compte de stockage contient un jeu de crochets, trois fonctions, trois jeux de parenthèses, un jeu de guillemets simples et une propriété :</span><span class="sxs-lookup"><span data-stu-id="3f04b-158">For example, the following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="3f04b-159">Si vous ne fournissez pas la syntaxe correspondante, le modèle produit une valeur très différente de votre intention.</span><span class="sxs-lookup"><span data-stu-id="3f04b-159">If you do not provide the matching syntax, the template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="3f04b-160">Lorsque vous recevez ce type d’erreur, examinez attentivement la syntaxe d’expression.</span><span class="sxs-lookup"><span data-stu-id="3f04b-160">When you receive this type of error, carefully review the expression syntax.</span></span> <span data-ttu-id="3f04b-161">Vous pouvez utiliser un éditeur JSON comme [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) ou [Visual Studio Code](resource-manager-vs-code.md), qui vous signale des erreurs de syntaxe.</span><span class="sxs-lookup"><span data-stu-id="3f04b-161">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="3f04b-162">Longueurs de segments incorrectes</span><span class="sxs-lookup"><span data-stu-id="3f04b-162">Incorrect segment lengths</span></span>

   <span data-ttu-id="3f04b-163">Une autre erreur de modèle non valide se produit lorsque le nom de la ressource n’est pas au format approprié.</span><span class="sxs-lookup"><span data-stu-id="3f04b-163">Another invalid template error occurs when the resource name is not in the correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'The template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="3f04b-164">Une ressource au niveau racine doit avoir un segment de moins dans le nom que dans le type de ressource.</span><span class="sxs-lookup"><span data-stu-id="3f04b-164">A root level resource must have one less segment in the name than in the resource type.</span></span> <span data-ttu-id="3f04b-165">Chaque segment se différencie par une barre oblique.</span><span class="sxs-lookup"><span data-stu-id="3f04b-165">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="3f04b-166">Dans l’exemple suivant, le type comporte deux segments et le nom un segment : il s’agit donc d’un **nom valide**.</span><span class="sxs-lookup"><span data-stu-id="3f04b-166">In the following example, the type has two segments and the name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="3f04b-167">Mais l’exemple suivant n’est **pas un nom valide** car il possède le même nombre de segments que le type.</span><span class="sxs-lookup"><span data-stu-id="3f04b-167">But the next example is **not a valid name** because it has the same number of segments as the type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="3f04b-168">Pour les ressources enfants, le type et le nom ont le même nombre de segments.</span><span class="sxs-lookup"><span data-stu-id="3f04b-168">For child resources, the type and name have the same number of segments.</span></span> <span data-ttu-id="3f04b-169">Ce nombre de segments est logique, car le nom complet et le type de l’enfant incluent le nom du parent et le type.</span><span class="sxs-lookup"><span data-stu-id="3f04b-169">This number of segments makes sense because the full name and type for the child includes the parent name and type.</span></span> <span data-ttu-id="3f04b-170">Par conséquent, le nom complet a toujours un segment de moins que le type complet.</span><span class="sxs-lookup"><span data-stu-id="3f04b-170">Therefore, the full name still has one less segment than the full type.</span></span>

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   <span data-ttu-id="3f04b-171">Obtenir des segments valides peut être difficile si des types Resource Manager sont appliqués à plusieurs fournisseurs de ressources.</span><span class="sxs-lookup"><span data-stu-id="3f04b-171">Getting the segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="3f04b-172">Par exemple, l’installation d’un verrou de ressource sur un site web nécessite un type avec quatre segments.</span><span class="sxs-lookup"><span data-stu-id="3f04b-172">For example, applying a resource lock to a web site requires a type with four segments.</span></span> <span data-ttu-id="3f04b-173">Par conséquent, le nom comporte 3 segments :</span><span class="sxs-lookup"><span data-stu-id="3f04b-173">Therefore, the name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="3f04b-174">La copie de l’index n’est pas prévue.</span><span class="sxs-lookup"><span data-stu-id="3f04b-174">Copy index is not expected</span></span>

   <span data-ttu-id="3f04b-175">Vous rencontrez cette erreur **InvalidTemplate** lorsque vous avez appliqué l’élément **copy** à une partie du modèle qui ne prend pas en charge cet élément.</span><span class="sxs-lookup"><span data-stu-id="3f04b-175">You encounter this **InvalidTemplate** error when you have applied the **copy** element to a part of the template that does not support this element.</span></span> <span data-ttu-id="3f04b-176">Vous pouvez uniquement appliquer l’élément copy à un type de ressource.</span><span class="sxs-lookup"><span data-stu-id="3f04b-176">You can only apply the copy element to a resource type.</span></span> <span data-ttu-id="3f04b-177">Vous ne pouvez pas appliquer l’élément copy à une propriété au sein d’un type de ressource.</span><span class="sxs-lookup"><span data-stu-id="3f04b-177">You cannot apply copy to a property within a resource type.</span></span> <span data-ttu-id="3f04b-178">Par exemple, vous appliquez copy à une machine virtuelle, mais ne pouvez pas l’appliquer aux disques du système d’exploitation pour une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="3f04b-178">For example, you apply copy to a virtual machine, but you cannot apply it to the OS disks for a virtual machine.</span></span> <span data-ttu-id="3f04b-179">Dans certains cas, vous pouvez convertir une ressource enfant en ressource parent afin de créer une boucle de copie.</span><span class="sxs-lookup"><span data-stu-id="3f04b-179">In some cases, you can convert a child resource to a parent resource to create a copy loop.</span></span> <span data-ttu-id="3f04b-180">Pour plus d’informations sur l’utilisation de copy, voir [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="3f04b-180">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="3f04b-181">Le paramètre n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="3f04b-181">Parameter is not valid</span></span>

   <span data-ttu-id="3f04b-182">Si le modèle spécifie les valeurs autorisées pour un paramètre et que vous fournissez une valeur qui n’est pas une de ces valeurs, vous recevez un message similaire à l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="3f04b-182">If the template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar to the following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'The provided value {parameter value}
  for the template parameter {parameter name} is not valid. The parameter value is not
  part of the allowed values
  ``` 

   <span data-ttu-id="3f04b-183">Vérifiez les valeurs autorisées dans le modèle et fournissez-en une pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="3f04b-183">Double check the allowed values in the template, and provide one during deployment.</span></span>

- <span data-ttu-id="3f04b-184">Dépendance circulaire détectée</span><span class="sxs-lookup"><span data-stu-id="3f04b-184">Circular dependency detected</span></span>

   <span data-ttu-id="3f04b-185">Vous recevez cette erreur lorsque des ressources dépendant les unes des autres empêchent le déploiement de démarrer.</span><span class="sxs-lookup"><span data-stu-id="3f04b-185">You receive this error when resources depend on each other in a way that prevents the deployment from starting.</span></span> <span data-ttu-id="3f04b-186">À cause de l’effet combiné d’interdépendances, plusieurs ressources attendent d’autres ressources qui sont elles aussi en attente.</span><span class="sxs-lookup"><span data-stu-id="3f04b-186">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="3f04b-187">Par exemple, la ressource 1 dépend de la ressource 3, la ressource 2 de la ressource 1 et la ressource 3 de la ressource 2.</span><span class="sxs-lookup"><span data-stu-id="3f04b-187">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="3f04b-188">Vous pouvez généralement résoudre ce problème en supprimant les dépendances inutiles.</span><span class="sxs-lookup"><span data-stu-id="3f04b-188">You can usually solve this problem by removing unnecessary dependencies.</span></span> 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="3f04b-189">NotFound et ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="3f04b-189">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="3f04b-190">Lorsque votre modèle inclut le nom d’une ressource qui ne peut pas être résolue, vous recevez une erreur similaire à la suivante :</span><span class="sxs-lookup"><span data-stu-id="3f04b-190">When your template includes the name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="3f04b-191">Si vous tentez de déployer la ressource manquante dans le modèle, vérifiez si vous devez ajouter une dépendance.</span><span class="sxs-lookup"><span data-stu-id="3f04b-191">If you are attempting to deploy the missing resource in the template, check whether you need to add a dependency.</span></span> <span data-ttu-id="3f04b-192">Resource Manager optimise le déploiement en créant des ressources en parallèle, quand cela est possible.</span><span class="sxs-lookup"><span data-stu-id="3f04b-192">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="3f04b-193">Si une ressource doit être déployée après une autre ressource, vous devez utiliser l’élément **dependsOn** de votre modèle pour créer une dépendance avec l’autre ressource.</span><span class="sxs-lookup"><span data-stu-id="3f04b-193">If one resource must be deployed after another resource, you need to use the **dependsOn** element in your template to create a dependency on the other resource.</span></span> <span data-ttu-id="3f04b-194">Par exemple, quand vous déployez une application web, le plan App Service doit être présent.</span><span class="sxs-lookup"><span data-stu-id="3f04b-194">For example, when deploying a web app, the App Service plan must exist.</span></span> <span data-ttu-id="3f04b-195">Si vous n’avez pas spécifié que l’application web est dépendante du plan App Service, Resource Manager crée les deux ressources en même temps.</span><span class="sxs-lookup"><span data-stu-id="3f04b-195">If you have not specified that the web app depends on the App Service plan, Resource Manager creates both resources at the same time.</span></span> <span data-ttu-id="3f04b-196">Vous recevez une erreur indiquant que la ressource du plan App Service est introuvable, car elle n’existe pas encore quand vous tentez de définir une propriété sur l’application web.</span><span class="sxs-lookup"><span data-stu-id="3f04b-196">You receive an error stating that the App Service plan resource cannot be found, because it does not exist yet when attempting to set a property on the web app.</span></span> <span data-ttu-id="3f04b-197">Vous pouvez éviter cette erreur en définissant la dépendance dans l’application web.</span><span class="sxs-lookup"><span data-stu-id="3f04b-197">You prevent this error by setting the dependency in the web app.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

<span data-ttu-id="3f04b-198">Pour obtenir des conseils sur la résolution des erreurs de dépendance, consultez [Vérifier la séquence de déploiement](#check-deployment-sequence).</span><span class="sxs-lookup"><span data-stu-id="3f04b-198">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="3f04b-199">Vous pouvez également voir cette erreur lorsque la ressource se trouve dans un groupe de ressources différent de celui faisant l’objet d’un déploiement.</span><span class="sxs-lookup"><span data-stu-id="3f04b-199">You also see this error when the resource exists in a different resource group than the one being deployed to.</span></span> <span data-ttu-id="3f04b-200">Dans ce cas, utilisez la [fonction resourceId](resource-group-template-functions-resource.md#resourceid) pour obtenir le nom complet de la ressource.</span><span class="sxs-lookup"><span data-stu-id="3f04b-200">In that case, use the [resourceId function](resource-group-template-functions-resource.md#resourceid) to get the fully qualified name of the resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="3f04b-201">Si vous essayez d’utiliser les fonctions [reference](resource-group-template-functions-resource.md#reference) ou [listKeys](resource-group-template-functions-resource.md#listkeys) avec une ressource qui ne peut pas être résolue, vous recevez l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="3f04b-201">If you attempt to use the [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that cannot be resolved, you receive the following error:</span></span>

```
Code=ResourceNotFound;
Message=The Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="3f04b-202">Recherchez une expression qui inclut la fonction **reference**.</span><span class="sxs-lookup"><span data-stu-id="3f04b-202">Look for an expression that includes the **reference** function.</span></span> <span data-ttu-id="3f04b-203">Vérifiez que les valeurs des paramètres sont corrects.</span><span class="sxs-lookup"><span data-stu-id="3f04b-203">Double check that the parameter values are correct.</span></span>

## <a name="parentresourcenotfound"></a><span data-ttu-id="3f04b-204">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="3f04b-204">ParentResourceNotFound</span></span>

<span data-ttu-id="3f04b-205">Lorsqu’une ressource est parent d’une autre ressource, la ressource parent doit exister avant de créer la ressource enfant.</span><span class="sxs-lookup"><span data-stu-id="3f04b-205">When one resource is a parent to another resource, the parent resource must exist before creating the child resource.</span></span> <span data-ttu-id="3f04b-206">Si elle n’existe pas encore, vous recevez l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="3f04b-206">If it does not yet exist, you receive the following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="3f04b-207">Le nom de la ressource enfant inclut le nom de la ressource parent.</span><span class="sxs-lookup"><span data-stu-id="3f04b-207">The name of the child resource includes the parent name.</span></span> <span data-ttu-id="3f04b-208">Par exemple, une base de données SQL peut être définie de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="3f04b-208">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="3f04b-209">Toutefois, si vous ne spécifiez pas de dépendance sur la ressource parent, la ressource enfant peut être déployée avant cette dernière.</span><span class="sxs-lookup"><span data-stu-id="3f04b-209">But, if you do not specify a dependency on the parent resource, the child resource may get deployed before the parent.</span></span> <span data-ttu-id="3f04b-210">Pour corriger cette erreur, incluez une dépendance.</span><span class="sxs-lookup"><span data-stu-id="3f04b-210">To resolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="3f04b-211">StorageAccountAlreadyExists et StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="3f04b-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="3f04b-212">Pour les comptes de stockage, vous devez fournir un nom pour la ressource qui est unique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3f04b-212">For storage accounts, you must provide a name for the resource that is unique across Azure.</span></span> <span data-ttu-id="3f04b-213">Si vous ne fournissez pas un nom unique, une erreur de ce type s’affiche :</span><span class="sxs-lookup"><span data-stu-id="3f04b-213">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=The storage account named mystorage is already taken.
```

<span data-ttu-id="3f04b-214">Vous pouvez créer un nom unique en concaténant votre nommage avec le résultat de la fonction [uniqueString](resource-group-template-functions-string.md#uniquestring) .</span><span class="sxs-lookup"><span data-stu-id="3f04b-214">You can create a unique name by concatenating your naming convention with the result of the [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="3f04b-215">Si vous déployez un compte de stockage portant le même nom qu’un compte de stockage existant dans votre abonnement, mais que vous indiquez un emplacement différent, vous recevez une erreur indiquant que le compte de stockage existe déjà dans un autre emplacement.</span><span class="sxs-lookup"><span data-stu-id="3f04b-215">If you deploy a storage account with the same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating the storage account already exists in a different location.</span></span> <span data-ttu-id="3f04b-216">Supprimez le compte de stockage existant ou indiquez le même emplacement que le compte de stockage existant.</span><span class="sxs-lookup"><span data-stu-id="3f04b-216">Either delete the existing storage account, or provide the same location as the existing storage account.</span></span>

## <a name="accountnameinvalid"></a><span data-ttu-id="3f04b-217">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="3f04b-217">AccountNameInvalid</span></span>
<span data-ttu-id="3f04b-218">Vous voyez l’erreur **AccountNameInvalid** lorsque vous tentez de donner à un compte de stockage un nom qui inclut des caractères interdits.</span><span class="sxs-lookup"><span data-stu-id="3f04b-218">You see the **AccountNameInvalid** error when attempting to give a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="3f04b-219">Ce nom doit comprendre entre 3 et 24 caractères, uniquement des lettres en minuscules et des nombres.</span><span class="sxs-lookup"><span data-stu-id="3f04b-219">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="3f04b-220">La fonction [uniqueString](resource-group-template-functions-string.md#uniquestring) renvoie 13 caractères.</span><span class="sxs-lookup"><span data-stu-id="3f04b-220">The [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="3f04b-221">Si vous concaténez un préfixe au résultat de la fonction **uniqueString**, fournissez un préfixe de 11 caractères maximum.</span><span class="sxs-lookup"><span data-stu-id="3f04b-221">If you concatenate a prefix to the **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

## <a name="badrequest"></a><span data-ttu-id="3f04b-222">BadRequest</span><span class="sxs-lookup"><span data-stu-id="3f04b-222">BadRequest</span></span>

<span data-ttu-id="3f04b-223">L’état BadRequest peut survenir lorsque vous spécifiez une valeur de propriété non valide.</span><span class="sxs-lookup"><span data-stu-id="3f04b-223">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="3f04b-224">Par exemple, si vous indiquez une valeur de référence (SKU) incorrecte pour un compte de stockage, le déploiement échoue.</span><span class="sxs-lookup"><span data-stu-id="3f04b-224">For example, if you provide an incorrect SKU value for a storage account, the deployment fails.</span></span> <span data-ttu-id="3f04b-225">Pour déterminer les valeurs valides pour la propriété, consultez la [documentation de l’API REST](/rest/api) pour le type de ressource que vous déployez.</span><span class="sxs-lookup"><span data-stu-id="3f04b-225">To determine valid values for property, look at the [REST API](/rest/api) for the resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="3f04b-226">NoRegisteredProviderFound et MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="3f04b-226">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="3f04b-227">Lorsque vous déployez une ressource, vous pouvez recevoir le message et le code d’erreur suivants :</span><span class="sxs-lookup"><span data-stu-id="3f04b-227">When deploying resource, you may receive the following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="3f04b-228">Vous pouvez sinon recevoir un message similaire indiquant :</span><span class="sxs-lookup"><span data-stu-id="3f04b-228">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: The subscription is not registered to use namespace {resource-provider-namespace}
```

<span data-ttu-id="3f04b-229">Ces erreurs apparaissent pour l’une des trois raisons suivantes :</span><span class="sxs-lookup"><span data-stu-id="3f04b-229">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="3f04b-230">Le fournisseur de ressources n’a pas été inscrit pour votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="3f04b-230">The resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="3f04b-231">La version de l’API n’est pas prise en charge pour le type de ressource.</span><span class="sxs-lookup"><span data-stu-id="3f04b-231">API version not supported for the resource type</span></span>
3. <span data-ttu-id="3f04b-232">L’emplacement n’est pas pris en charge pour le type de ressource.</span><span class="sxs-lookup"><span data-stu-id="3f04b-232">Location not supported for the resource type</span></span>

<span data-ttu-id="3f04b-233">Le message d’erreur doit fournir des suggestions pour les emplacements et les versions d’API pris en charge.</span><span class="sxs-lookup"><span data-stu-id="3f04b-233">The error message should give you suggestions for the supported locations and API versions.</span></span> <span data-ttu-id="3f04b-234">Vous pouvez changer votre modèle en l’une des valeurs suggérées.</span><span class="sxs-lookup"><span data-stu-id="3f04b-234">You can change your template to one of the suggested values.</span></span> <span data-ttu-id="3f04b-235">La plupart des fournisseurs sont inscrits automatiquement par le portail Azure ou l’interface de ligne de commande que vous utilisez, mais pas tous.</span><span class="sxs-lookup"><span data-stu-id="3f04b-235">Most providers are registered automatically by the Azure portal or the command-line interface you are using, but not all.</span></span> <span data-ttu-id="3f04b-236">Si vous n’avez pas déjà utilisé un fournisseur de ressources spécifique, vous devrez peut-être inscrire ce dernier.</span><span class="sxs-lookup"><span data-stu-id="3f04b-236">If you have not used a particular resource provider before, you may need to register that provider.</span></span> <span data-ttu-id="3f04b-237">Vous pouvez en savoir plus sur les fournisseurs de ressources via PowerShell ou l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="3f04b-237">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="3f04b-238">**Portail**</span><span class="sxs-lookup"><span data-stu-id="3f04b-238">**Portal**</span></span>

<span data-ttu-id="3f04b-239">Vous pouvez voir l’état de l’inscription et inscrire un espace de noms de fournisseur de ressources par le biais du portail.</span><span class="sxs-lookup"><span data-stu-id="3f04b-239">You can see the registration status and register a resource provider namespace through the portal.</span></span>

1. <span data-ttu-id="3f04b-240">Sur votre abonnement, sélectionnez **Fournisseurs de ressources**.</span><span class="sxs-lookup"><span data-stu-id="3f04b-240">For your subscription, select **Resource providers**.</span></span>

   ![sélectionner Fournisseurs de ressources](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="3f04b-242">Passez en revue la liste des fournisseurs de ressources et, si nécessaire, sélectionnez le lien **Inscrire** pour inscrire le fournisseur de ressources du type que vous voulez déployer.</span><span class="sxs-lookup"><span data-stu-id="3f04b-242">Look at the list of resource providers, and if necessary, select the **Register** link to register the resource provider of the type you are trying to deploy.</span></span>

   ![répertorier les fournisseurs de ressources](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="3f04b-244">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="3f04b-244">**PowerShell**</span></span>

<span data-ttu-id="3f04b-245">Pour afficher l’état de votre inscription, utilisez **Get-AzureRmResourceProvider**.</span><span class="sxs-lookup"><span data-stu-id="3f04b-245">To see your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="3f04b-246">Pour inscrire un fournisseur, utilisez **Register-AzureRmResourceProvider** et indiquez le nom du fournisseur de ressources que vous voulez inscrire.</span><span class="sxs-lookup"><span data-stu-id="3f04b-246">To register a provider, use **Register-AzureRmResourceProvider** and provide the name of the resource provider you wish to register.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="3f04b-247">Pour obtenir les emplacements pris en charge d’un type particulier de ressource, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3f04b-247">To get the supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="3f04b-248">Pour obtenir les versions d’API prises en charge d’un type particulier de ressource, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3f04b-248">To get the supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="3f04b-249">**Interface de ligne de commande Azure**</span><span class="sxs-lookup"><span data-stu-id="3f04b-249">**Azure CLI**</span></span>

<span data-ttu-id="3f04b-250">Pour voir si le fournisseur est inscrit, utilisez la commande `azure provider list` .</span><span class="sxs-lookup"><span data-stu-id="3f04b-250">To see whether the provider is registered, use the `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="3f04b-251">Pour inscrire un fournisseur de ressources, utilisez la commande `azure provider register` et indiquez *l’espace de noms* à inscrire.</span><span class="sxs-lookup"><span data-stu-id="3f04b-251">To register a resource provider, use the `azure provider register` command, and specify the *namespace* to register.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="3f04b-252">Pour afficher les emplacements et les versions d’API pris en charge pour un type de ressources, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3f04b-252">To see the supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="3f04b-253">QuotaExceeded et OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="3f04b-253">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="3f04b-254">Vous pouvez rencontrer des problèmes quand un déploiement dépasse un quota qui peut concerner entre autres les groupes de ressources, les abonnements ou les comptes.</span><span class="sxs-lookup"><span data-stu-id="3f04b-254">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="3f04b-255">Par exemple, votre abonnement peut être configuré pour limiter le nombre de cœurs dans une région.</span><span class="sxs-lookup"><span data-stu-id="3f04b-255">For example, your subscription may be configured to limit the number of cores for a region.</span></span> <span data-ttu-id="3f04b-256">Si vous tentez de déployer une machine virtuelle avec plus de cœurs que la quantité autorisée, vous recevez une erreur indiquant que le quota a été dépassé.</span><span class="sxs-lookup"><span data-stu-id="3f04b-256">If you attempt to deploy a virtual machine with more cores than the permitted amount, you receive an error stating the quota has been exceeded.</span></span>
<span data-ttu-id="3f04b-257">Pour obtenir des informations complètes sur les quotas, consultez [Abonnement Azure et limites, quotas et contraintes du service](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="3f04b-257">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="3f04b-258">Pour examiner les quotas de cœurs de votre abonnement, vous pouvez utiliser la commande `azure vm list-usage` dans l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="3f04b-258">To examine your subscription's quotas for cores, you can use the `azure vm list-usage` command in the Azure CLI.</span></span> <span data-ttu-id="3f04b-259">L’exemple suivant montre que le quota de cœurs d’un compte d’évaluation gratuit est de 4 :</span><span class="sxs-lookup"><span data-stu-id="3f04b-259">The following example illustrates that the core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="3f04b-260">Résultat :</span><span class="sxs-lookup"><span data-stu-id="3f04b-260">Which returns:</span></span>

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

<span data-ttu-id="3f04b-261">Si vous déployez un modèle qui crée plus de quatre cœurs dans la région ouest des États-Unis, vous obtenez une erreur de déploiement similaire à la suivante :</span><span class="sxs-lookup"><span data-stu-id="3f04b-261">If you deploy a template that creates more than four cores in the West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="3f04b-262">Dans PowerShell, vous pouvez également utiliser l’applet de commande **Get-AzureRmVMUsage** .</span><span class="sxs-lookup"><span data-stu-id="3f04b-262">Or in PowerShell, you can use the **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="3f04b-263">Résultat :</span><span class="sxs-lookup"><span data-stu-id="3f04b-263">Which returns:</span></span>

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

<span data-ttu-id="3f04b-264">Dans ce cas, vous devez accéder au portail et signaler un problème de support afin d’augmenter votre quota pour la région vers laquelle vous souhaitez procéder au déploiement.</span><span class="sxs-lookup"><span data-stu-id="3f04b-264">In these cases, you should go to the portal and file a support issue to raise your quota for the region into which you want to deploy.</span></span>

> [!NOTE]
> <span data-ttu-id="3f04b-265">N’oubliez pas que pour les groupes de ressources, le quota est défini pour chaque région, pas pour tout l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="3f04b-265">Remember that for resource groups, the quota is for each individual region, not for the entire subscription.</span></span> <span data-ttu-id="3f04b-266">Si vous devez déployer 30 cœurs dans l’Ouest des États-Unis, vous devez demander 30 cœurs Resource Manager dans l’Ouest des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="3f04b-266">If you need to deploy 30 cores in West US, you have to ask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="3f04b-267">Si vous devez déployer 30 cœurs dans l’une des régions auxquelles vous avez accès, vous devez demander 30 cœurs Resource Manager dans toutes les régions.</span><span class="sxs-lookup"><span data-stu-id="3f04b-267">If you need to deploy 30 cores in any of the regions to which you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

## <a name="invalidcontentlink"></a><span data-ttu-id="3f04b-268">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="3f04b-268">InvalidContentLink</span></span>
<span data-ttu-id="3f04b-269">Lorsque vous recevez le message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="3f04b-269">When you receive the error message:</span></span>

```
Code=InvalidContentLink
Message=Unable to download deployment content from ...
```

<span data-ttu-id="3f04b-270">Vous avez probablement tenté d’établir une liaison avec un modèle imbriqué qui n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="3f04b-270">You have most likely attempted to link to a nested template that is not available.</span></span> <span data-ttu-id="3f04b-271">Vérifiez l’URI que vous avez indiqué pour le modèle imbriqué.</span><span class="sxs-lookup"><span data-stu-id="3f04b-271">Double check the URI you provided for the nested template.</span></span> <span data-ttu-id="3f04b-272">Si le modèle existe dans un compte de stockage, assurez-vous que l’URI est accessible.</span><span class="sxs-lookup"><span data-stu-id="3f04b-272">If the template exists in a storage account, make sure the URI is accessible.</span></span> <span data-ttu-id="3f04b-273">Vous devrez peut-être valider un jeton SAS.</span><span class="sxs-lookup"><span data-stu-id="3f04b-273">You may need to pass a SAS token.</span></span> <span data-ttu-id="3f04b-274">Pour plus d’informations, consultez [Utilisation de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3f04b-274">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="requestdisallowedbypolicy"></a><span data-ttu-id="3f04b-275">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="3f04b-275">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="3f04b-276">Vous recevez cette erreur lorsque votre abonnement inclut une stratégie de ressource qui empêche une action que vous tentez d’exécuter au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="3f04b-276">You receive this error when your subscription includes a resource policy that prevents an action you are trying to perform during deployment.</span></span> <span data-ttu-id="3f04b-277">Dans le message d’erreur, recherchez l’identificateur de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="3f04b-277">In the error message, look for the policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="3f04b-278">Dans **PowerShell**, fournissez cet identificateur de stratégie en tant que paramètre **Id** pour extraire des informations sur la stratégie qui a bloqué votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="3f04b-278">In **PowerShell**, provide that policy identifier as the **Id** parameter to retrieve details about the policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="3f04b-279">Dans **Interface de ligne de commande Azure**, indiquez le nom de la définition de stratégie :</span><span class="sxs-lookup"><span data-stu-id="3f04b-279">In **Azure CLI**, provide the name of the policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="3f04b-280">Pour plus d’informations, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="3f04b-280">For more information, see the following articles:</span></span>

- [<span data-ttu-id="3f04b-281">Erreur RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="3f04b-281">RequestDisallowedByPolicy error</span></span>](resource-manager-policy-requestdisallowedbypolicy-error.md)
- <span data-ttu-id="3f04b-282">[Utilisez le service Policy pour gérer les ressources et contrôler l’accès](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="3f04b-282">[Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>

## <a name="authorization-failed"></a><span data-ttu-id="3f04b-283">Échec de l’autorisation</span><span class="sxs-lookup"><span data-stu-id="3f04b-283">Authorization failed</span></span>
<span data-ttu-id="3f04b-284">Vous pouvez recevoir une erreur lors du déploiement, car le compte ou le principal du service qui tente de déployer les ressources n’a pas accès à ces actions.</span><span class="sxs-lookup"><span data-stu-id="3f04b-284">You may receive an error during deployment because the account or service principal attempting to deploy the resources does not have access to perform those actions.</span></span> <span data-ttu-id="3f04b-285">Azure Active Directory permet à votre administrateur ou à vous-même de contrôler très précisément quelles identités peuvent accéder à quelles ressources.</span><span class="sxs-lookup"><span data-stu-id="3f04b-285">Azure Active Directory enables you or your administrator to control which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="3f04b-286">Par exemple, si votre compte est affecté au rôle de lecteur, vous ne pouvez pas créer de ressources.</span><span class="sxs-lookup"><span data-stu-id="3f04b-286">For example, if your account is assigned to the Reader role, you are not able to create resources.</span></span> <span data-ttu-id="3f04b-287">Dans ce cas, vous voyez un message d’erreur indiquant que l’autorisation a échoué.</span><span class="sxs-lookup"><span data-stu-id="3f04b-287">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="3f04b-288">Pour plus d’informations sur le contrôle d’accès en fonction du rôle, consultez la rubrique [Contrôle d’accès en fonction du rôle d’Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="3f04b-288">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="3f04b-289">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3f04b-289">Next steps</span></span>
* <span data-ttu-id="3f04b-290">Pour en savoir plus sur les actions d’audit, consultez [Opérations d’audit avec Resource Manager](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="3f04b-290">To learn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="3f04b-291">Pour en savoir plus sur les actions visant à déterminer les erreurs au cours du déploiement, consultez [Voir les opérations de déploiement](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="3f04b-291">To learn about actions to determine the errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
