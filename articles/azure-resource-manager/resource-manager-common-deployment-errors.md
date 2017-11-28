---
title: "erreurs de déploiement Azure courantes aaaTroubleshoot | Documents Microsoft"
description: "Décrit comment tooresolve les erreurs courantes lors du déploiement de tooAzure de ressources à l’aide du Gestionnaire de ressources Azure."
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: "Erreur de déploiement, déploiement d’azure, déployez tooazure"
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="cd859-104">Résolution des erreurs courantes dans des déploiements Azure avec Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cd859-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="cd859-105">Cette rubrique décrit comment résoudre certaines erreurs courantes liées au déploiement d’Azure que vous pouvez rencontrer.</span><span class="sxs-lookup"><span data-stu-id="cd859-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

<span data-ttu-id="cd859-106">Hello suivant des codes d’erreur est décrites dans cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="cd859-106">hello following error codes are described in this topic:</span></span>

* [<span data-ttu-id="cd859-107">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="cd859-107">AccountNameInvalid</span></span>](#accountnameinvalid)
* [<span data-ttu-id="cd859-108">Échec de l’autorisation</span><span class="sxs-lookup"><span data-stu-id="cd859-108">Authorization failed</span></span>](#authorization-failed)
* [<span data-ttu-id="cd859-109">BadRequest</span><span class="sxs-lookup"><span data-stu-id="cd859-109">BadRequest</span></span>](#badrequest)
* [<span data-ttu-id="cd859-110">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="cd859-110">DeploymentFailed</span></span>](#deploymentfailed)
* [<span data-ttu-id="cd859-111">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="cd859-111">DisallowedOperation</span></span>](#disallowedoperation)
* [<span data-ttu-id="cd859-112">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="cd859-112">InvalidContentLink</span></span>](#invalidcontentlink)
* [<span data-ttu-id="cd859-113">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="cd859-113">InvalidTemplate</span></span>](#invalidtemplate)
* [<span data-ttu-id="cd859-114">MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="cd859-114">MissingSubscriptionRegistration</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="cd859-115">NotFound</span><span class="sxs-lookup"><span data-stu-id="cd859-115">NotFound</span></span>](#notfound)
* [<span data-ttu-id="cd859-116">NoRegisteredProviderFound</span><span class="sxs-lookup"><span data-stu-id="cd859-116">NoRegisteredProviderFound</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="cd859-117">OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="cd859-117">OperationNotAllowed</span></span>](#quotaexceeded)
* [<span data-ttu-id="cd859-118">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="cd859-118">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* [<span data-ttu-id="cd859-119">QuotaExceeded</span><span class="sxs-lookup"><span data-stu-id="cd859-119">QuotaExceeded</span></span>](#quotaexceeded)
* [<span data-ttu-id="cd859-120">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="cd859-120">RequestDisallowedByPolicy</span></span>](#requestdisallowedbypolicy)
* [<span data-ttu-id="cd859-121">ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="cd859-121">ResourceNotFound</span></span>](#notfound)
* [<span data-ttu-id="cd859-122">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="cd859-122">SkuNotAvailable</span></span>](#skunotavailable)
* [<span data-ttu-id="cd859-123">StorageAccountAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="cd859-123">StorageAccountAlreadyExists</span></span>](#storagenamenotunique)
* [<span data-ttu-id="cd859-124">StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="cd859-124">StorageAccountAlreadyTaken</span></span>](#storagenamenotunique)

## <a name="deploymentfailed"></a><span data-ttu-id="cd859-125">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="cd859-125">DeploymentFailed</span></span>

<span data-ttu-id="cd859-126">Ce code d’erreur indique une erreur de déploiement général, mais il n’est pas code d’erreur hello vous devez toostart résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="cd859-126">This error code indicates a general deployment error, but it is not hello error code you need toostart troubleshooting.</span></span> <span data-ttu-id="cd859-127">code d’erreur Hello réellement vous aide à résoudre le problème de hello est généralement un niveau en dessous de cette erreur.</span><span class="sxs-lookup"><span data-stu-id="cd859-127">hello error code that actually helps you resolve hello issue is usually one level below this error.</span></span> <span data-ttu-id="cd859-128">Par exemple, hello image suivante montre hello **RequestDisallowedByPolicy** code d’erreur qui se trouve sous l’erreur de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="cd859-128">For example, hello following image shows hello **RequestDisallowedByPolicy** error code that is under hello deployment error.</span></span>

![afficher le code d'erreur](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a><span data-ttu-id="cd859-130">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="cd859-130">SkuNotAvailable</span></span>

<span data-ttu-id="cd859-131">Lors du déploiement d’une ressource (en général, un ordinateur virtuel), hello message erreur et le code d’erreur suivant peut s’afficher :</span><span class="sxs-lookup"><span data-stu-id="cd859-131">When deploying a resource (typically a virtual machine), you may receive hello following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

<span data-ttu-id="cd859-132">Vous recevez cette erreur lorsque la ressource de hello référence (SKU) que vous avez sélectionné (par exemple, la taille de machine virtuelle) n’est pas disponible pour l’emplacement hello que vous avez sélectionné.</span><span class="sxs-lookup"><span data-stu-id="cd859-132">You receive this error when hello resource SKU you have selected (such as VM size) is not available for hello location you have selected.</span></span> <span data-ttu-id="cd859-133">tooresolve ce problème, vous devez toodetermine les références (SKU) disponibles dans une région.</span><span class="sxs-lookup"><span data-stu-id="cd859-133">tooresolve this issue, you need toodetermine which SKUs are available in a region.</span></span> <span data-ttu-id="cd859-134">Vous pouvez utiliser PowerShell, hello portail ou un toofind d’opération REST références disponibles.</span><span class="sxs-lookup"><span data-stu-id="cd859-134">You can use PowerShell, hello portal, or a REST operation toofind available SKUs.</span></span>

- <span data-ttu-id="cd859-135">Pour PowerShell, utilisez [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) et filtrez par emplacement.</span><span class="sxs-lookup"><span data-stu-id="cd859-135">For PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) and filter by location.</span></span> <span data-ttu-id="cd859-136">Vous devez disposer de hello dernière version de PowerShell pour cette commande.</span><span class="sxs-lookup"><span data-stu-id="cd859-136">You must have hello latest version of PowerShell for this command.</span></span>

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  <span data-ttu-id="cd859-137">résultats de Hello incluent une liste de références (SKU) pour l’emplacement de hello et des restrictions pour cette version de Windows.</span><span class="sxs-lookup"><span data-stu-id="cd859-137">hello results include a list of SKUs for hello location and any restrictions for that SKU.</span></span>

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- <span data-ttu-id="cd859-138">toouse hello [portal](https://portal.azure.com), connectez-vous au portail de toohello et ajouter une ressource via une interface de hello.</span><span class="sxs-lookup"><span data-stu-id="cd859-138">toouse hello [portal](https://portal.azure.com), log in toohello portal and add a resource through hello interface.</span></span> <span data-ttu-id="cd859-139">Lorsque vous définissez les valeurs hello, vous voyez hello références disponibles pour cette ressource.</span><span class="sxs-lookup"><span data-stu-id="cd859-139">As you set hello values, you see hello available SKUs for that resource.</span></span> <span data-ttu-id="cd859-140">Vous n’avez pas besoin de déploiement de hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="cd859-140">You do not need toocomplete hello deployment.</span></span>

    ![Références disponibles](./media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="cd859-142">toouse hello API REST pour les machines virtuelles, envoyer hello demande :</span><span class="sxs-lookup"><span data-stu-id="cd859-142">toouse hello REST API for virtual machines, send hello following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="cd859-143">Elle retourne des références (SKU) et les régions disponibles dans hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="cd859-143">It returns available SKUs and regions in hello following format:</span></span>

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

<span data-ttu-id="cd859-144">Si vous êtes toofind Impossible d’une référence (SKU) appropriée dans cette région ou une autre région qui répond aux besoins de votre entreprise, envoyer un [demande de référence (SKU)](https://aka.ms/skurestriction) tooAzure prise en charge.</span><span class="sxs-lookup"><span data-stu-id="cd859-144">If you are unable toofind a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) tooAzure Support.</span></span>

## <a name="disallowedoperation"></a><span data-ttu-id="cd859-145">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="cd859-145">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="cd859-146">Si vous recevez cette erreur, vous utilisez un abonnement qui n’est pas autorisée tooaccess tous les services Azure autres que Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cd859-146">If you receive this error, you are using a subscription that is not permitted tooaccess any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="cd859-147">Vous pouvez avoir ce type d’abonnement quand vous avez besoin de portail classique de hello tooaccess toodeploy ressources ne sont pas autorisées.</span><span class="sxs-lookup"><span data-stu-id="cd859-147">You might have this type of subscription when you need tooaccess hello classic portal but are not permitted toodeploy resources.</span></span> <span data-ttu-id="cd859-148">tooresolve ce problème, vous devez utiliser un abonnement qui contient des ressources de toodeploy d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="cd859-148">tooresolve this issue, you must use a subscription that has permission toodeploy resources.</span></span>  

<span data-ttu-id="cd859-149">tooview vos abonnements disponibles avec PowerShell, utilisez :</span><span class="sxs-lookup"><span data-stu-id="cd859-149">tooview your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="cd859-150">Et tooset hello abonnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="cd859-150">And, tooset hello current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="cd859-151">tooview vos abonnements disponibles avec Azure CLI 2.0, utilisez :</span><span class="sxs-lookup"><span data-stu-id="cd859-151">tooview your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="cd859-152">Et tooset hello abonnement, utilisez :</span><span class="sxs-lookup"><span data-stu-id="cd859-152">And, tooset hello current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a><span data-ttu-id="cd859-153">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="cd859-153">InvalidTemplate</span></span>
<span data-ttu-id="cd859-154">Cette erreur peut résulter de différents types d’erreurs.</span><span class="sxs-lookup"><span data-stu-id="cd859-154">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="cd859-155">Erreur de syntaxe</span><span class="sxs-lookup"><span data-stu-id="cd859-155">Syntax error</span></span>

   <span data-ttu-id="cd859-156">Si vous recevez un message d’erreur qui indique la validation du modèle a échoué hello, vous avez peut-être un problème de syntaxe dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="cd859-156">If you receive an error message that indicates hello template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="cd859-157">Cette erreur est toomake facile, car les expressions de modèle peuvent être complexes.</span><span class="sxs-lookup"><span data-stu-id="cd859-157">This error is easy toomake because template expressions can be intricate.</span></span> <span data-ttu-id="cd859-158">Par exemple, hello affectation de nom suivante pour un compte de stockage contient un jeu de crochets, trois fonctions, trois jeux de parenthèses, un seul jeu de guillemets simples et une propriété :</span><span class="sxs-lookup"><span data-stu-id="cd859-158">For example, hello following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="cd859-159">Si vous ne fournissez pas de syntaxe de correspondance hello, modèle de hello génère une valeur qui est différente de celle de votre intention.</span><span class="sxs-lookup"><span data-stu-id="cd859-159">If you do not provide hello matching syntax, hello template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="cd859-160">Lorsque vous recevez ce type d’erreur, lisez attentivement la syntaxe d’expression hello.</span><span class="sxs-lookup"><span data-stu-id="cd859-160">When you receive this type of error, carefully review hello expression syntax.</span></span> <span data-ttu-id="cd859-161">Vous pouvez utiliser un éditeur JSON comme [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) ou [Visual Studio Code](resource-manager-vs-code.md), qui vous signale des erreurs de syntaxe.</span><span class="sxs-lookup"><span data-stu-id="cd859-161">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="cd859-162">Longueurs de segments incorrectes</span><span class="sxs-lookup"><span data-stu-id="cd859-162">Incorrect segment lengths</span></span>

   <span data-ttu-id="cd859-163">Une autre erreur de modèle non valide se produit lorsque le nom de la ressource hello n’est pas au format correct de hello.</span><span class="sxs-lookup"><span data-stu-id="cd859-163">Another invalid template error occurs when hello resource name is not in hello correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="cd859-164">Une ressource de niveau racine doit avoir un segment inférieur dans nom hello que dans le type de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="cd859-164">A root level resource must have one less segment in hello name than in hello resource type.</span></span> <span data-ttu-id="cd859-165">Chaque segment se différencie par une barre oblique.</span><span class="sxs-lookup"><span data-stu-id="cd859-165">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="cd859-166">Dans l’exemple suivant de hello, type de hello possède deux segments et nom de hello a un seul segment, donc il est un **nom valide**.</span><span class="sxs-lookup"><span data-stu-id="cd859-166">In hello following example, hello type has two segments and hello name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="cd859-167">Mais hello l’exemple suivant est **pas un nom valide** , car il a hello même nombre de segments en tant que type de hello.</span><span class="sxs-lookup"><span data-stu-id="cd859-167">But hello next example is **not a valid name** because it has hello same number of segments as hello type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="cd859-168">Pour les ressources enfants, hello type et le nom ont hello même nombre de segments.</span><span class="sxs-lookup"><span data-stu-id="cd859-168">For child resources, hello type and name have hello same number of segments.</span></span> <span data-ttu-id="cd859-169">Ce nombre de segments de sens, car le nom complet de hello et type pour les enfants hello inclut le type et le nom du parent hello.</span><span class="sxs-lookup"><span data-stu-id="cd859-169">This number of segments makes sense because hello full name and type for hello child includes hello parent name and type.</span></span> <span data-ttu-id="cd859-170">Par conséquent, nom complet de hello dispose toujours d’un segment à moins que complet de type hello.</span><span class="sxs-lookup"><span data-stu-id="cd859-170">Therefore, hello full name still has one less segment than hello full type.</span></span>

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

   <span data-ttu-id="cd859-171">Lors de l’obtention de segments hello droit peuvent être compliquées avec les types de gestionnaire de ressources qui sont appliquées sur des fournisseurs de ressources.</span><span class="sxs-lookup"><span data-stu-id="cd859-171">Getting hello segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="cd859-172">Par exemple, l’application d’un site web de ressource verrou tooa nécessite un type avec quatre segments.</span><span class="sxs-lookup"><span data-stu-id="cd859-172">For example, applying a resource lock tooa web site requires a type with four segments.</span></span> <span data-ttu-id="cd859-173">Par conséquent, le nom de hello est trois segments :</span><span class="sxs-lookup"><span data-stu-id="cd859-173">Therefore, hello name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="cd859-174">La copie de l’index n’est pas prévue.</span><span class="sxs-lookup"><span data-stu-id="cd859-174">Copy index is not expected</span></span>

   <span data-ttu-id="cd859-175">Ce problème survient **InvalidTemplate** erreur lorsque vous avez appliqué hello **copie** partie tooa d’élément de modèle hello qui ne prend pas en charge cet élément.</span><span class="sxs-lookup"><span data-stu-id="cd859-175">You encounter this **InvalidTemplate** error when you have applied hello **copy** element tooa part of hello template that does not support this element.</span></span> <span data-ttu-id="cd859-176">Vous pouvez uniquement appliquer le type de ressource hello copie élément tooa.</span><span class="sxs-lookup"><span data-stu-id="cd859-176">You can only apply hello copy element tooa resource type.</span></span> <span data-ttu-id="cd859-177">Vous ne pouvez pas appliquer de propriété tooa de copie au sein d’un type de ressource.</span><span class="sxs-lookup"><span data-stu-id="cd859-177">You cannot apply copy tooa property within a resource type.</span></span> <span data-ttu-id="cd859-178">Par exemple, vous appliquez la machine virtuelle de tooa copie, mais ne peut pas appliquer les disques toohello du système d’exploitation pour un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="cd859-178">For example, you apply copy tooa virtual machine, but you cannot apply it toohello OS disks for a virtual machine.</span></span> <span data-ttu-id="cd859-179">Dans certains cas, vous pouvez convertir un toocreate des ressources de parent enfant ressource tooa une boucle de copie.</span><span class="sxs-lookup"><span data-stu-id="cd859-179">In some cases, you can convert a child resource tooa parent resource toocreate a copy loop.</span></span> <span data-ttu-id="cd859-180">Pour plus d’informations sur l’utilisation de copy, voir [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="cd859-180">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="cd859-181">Le paramètre n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="cd859-181">Parameter is not valid</span></span>

   <span data-ttu-id="cd859-182">Si le modèle de hello spécifie les valeurs autorisées pour un paramètre, et vous fournir une valeur qui n’est pas un de ces valeurs, vous recevez un toohello similaire message l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="cd859-182">If hello template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar toohello following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   <span data-ttu-id="cd859-183">Vérifiez hello valeurs autorisées dans le modèle de hello et fournir une au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="cd859-183">Double check hello allowed values in hello template, and provide one during deployment.</span></span>

- <span data-ttu-id="cd859-184">Dépendance circulaire détectée</span><span class="sxs-lookup"><span data-stu-id="cd859-184">Circular dependency detected</span></span>

   <span data-ttu-id="cd859-185">Vous recevez cette erreur lorsque les ressources dépendent eux d’une manière qui empêche le déploiement hello de démarrer.</span><span class="sxs-lookup"><span data-stu-id="cd859-185">You receive this error when resources depend on each other in a way that prevents hello deployment from starting.</span></span> <span data-ttu-id="cd859-186">À cause de l’effet combiné d’interdépendances, plusieurs ressources attendent d’autres ressources qui sont elles aussi en attente.</span><span class="sxs-lookup"><span data-stu-id="cd859-186">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="cd859-187">Par exemple, la ressource 1 dépend de la ressource 3, la ressource 2 de la ressource 1 et la ressource 3 de la ressource 2.</span><span class="sxs-lookup"><span data-stu-id="cd859-187">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="cd859-188">Vous pouvez généralement résoudre ce problème en supprimant les dépendances inutiles.</span><span class="sxs-lookup"><span data-stu-id="cd859-188">You can usually solve this problem by removing unnecessary dependencies.</span></span> 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="cd859-189">NotFound et ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="cd859-189">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="cd859-190">Lorsque votre modèle inclut le nom hello d’une ressource qui ne peut pas être résolue, vous recevez une erreur similaire à :</span><span class="sxs-lookup"><span data-stu-id="cd859-190">When your template includes hello name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="cd859-191">Si vous essayez de hello toodeploy ressource dans le modèle de hello manquante, vérifiez si vous devez tooadd une dépendance.</span><span class="sxs-lookup"><span data-stu-id="cd859-191">If you are attempting toodeploy hello missing resource in hello template, check whether you need tooadd a dependency.</span></span> <span data-ttu-id="cd859-192">Resource Manager optimise le déploiement en créant des ressources en parallèle, quand cela est possible.</span><span class="sxs-lookup"><span data-stu-id="cd859-192">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="cd859-193">Si une ressource doit être déployée après une autre ressource, vous devez toouse hello **dependsOn** élément dans votre toocreate modèle une dépendance sur hello autre ressource.</span><span class="sxs-lookup"><span data-stu-id="cd859-193">If one resource must be deployed after another resource, you need toouse hello **dependsOn** element in your template toocreate a dependency on hello other resource.</span></span> <span data-ttu-id="cd859-194">Par exemple, lorsque vous déployez une application web, hello plan App Service doit exister.</span><span class="sxs-lookup"><span data-stu-id="cd859-194">For example, when deploying a web app, hello App Service plan must exist.</span></span> <span data-ttu-id="cd859-195">Si vous n’avez pas spécifié cette application web de hello dépend hello plan App Service, le Gestionnaire de ressources crée les deux ressources à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="cd859-195">If you have not specified that hello web app depends on hello App Service plan, Resource Manager creates both resources at hello same time.</span></span> <span data-ttu-id="cd859-196">Vous recevez une erreur indiquant que hello ressources du plan App Service est introuvable, car il n’existe pas encore lors de la tentative de tooset une propriété sur l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="cd859-196">You receive an error stating that hello App Service plan resource cannot be found, because it does not exist yet when attempting tooset a property on hello web app.</span></span> <span data-ttu-id="cd859-197">Vous éviter cette erreur en définissant la dépendance de hello dans hello web app.</span><span class="sxs-lookup"><span data-stu-id="cd859-197">You prevent this error by setting hello dependency in hello web app.</span></span>

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

<span data-ttu-id="cd859-198">Pour obtenir des conseils sur la résolution des erreurs de dépendance, consultez [Vérifier la séquence de déploiement](#check-deployment-sequence).</span><span class="sxs-lookup"><span data-stu-id="cd859-198">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="cd859-199">Cette erreur est également survenir lors de la ressource de hello existe dans un autre groupe de ressources que hello un déploiement sur.</span><span class="sxs-lookup"><span data-stu-id="cd859-199">You also see this error when hello resource exists in a different resource group than hello one being deployed to.</span></span> <span data-ttu-id="cd859-200">Dans ce cas, utilisez hello [fonction resourceId](resource-group-template-functions-resource.md#resourceid) nom qualifié complet de hello tooget de ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="cd859-200">In that case, use hello [resourceId function](resource-group-template-functions-resource.md#resourceid) tooget hello fully qualified name of hello resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="cd859-201">Si vous essayez de toouse hello [référence](resource-group-template-functions-resource.md#reference) ou [listKeys](resource-group-template-functions-resource.md#listkeys) fonctions avec une ressource qui ne peut pas être résolu, vous recevez hello l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="cd859-201">If you attempt toouse hello [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that cannot be resolved, you receive hello following error:</span></span>

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="cd859-202">Recherchez une expression qui inclut hello **référence** (fonction).</span><span class="sxs-lookup"><span data-stu-id="cd859-202">Look for an expression that includes hello **reference** function.</span></span> <span data-ttu-id="cd859-203">Vérifiez que les valeurs de paramètre hello sont corrects.</span><span class="sxs-lookup"><span data-stu-id="cd859-203">Double check that hello parameter values are correct.</span></span>

## <a name="parentresourcenotfound"></a><span data-ttu-id="cd859-204">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="cd859-204">ParentResourceNotFound</span></span>

<span data-ttu-id="cd859-205">Lorsqu’une ressource est une ressource de tooanother parent, ressource parente de hello doit exister avant de créer la ressource de hello enfant.</span><span class="sxs-lookup"><span data-stu-id="cd859-205">When one resource is a parent tooanother resource, hello parent resource must exist before creating hello child resource.</span></span> <span data-ttu-id="cd859-206">Si elle n’existe pas encore, vous recevez hello l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="cd859-206">If it does not yet exist, you receive hello following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="cd859-207">nom Hello de ressource enfant de hello inclut nom hello du parent.</span><span class="sxs-lookup"><span data-stu-id="cd859-207">hello name of hello child resource includes hello parent name.</span></span> <span data-ttu-id="cd859-208">Par exemple, une base de données SQL peut être définie de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="cd859-208">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="cd859-209">Mais, si vous ne spécifiez pas une dépendance sur la ressource parent de hello, ressource enfant de hello peut obtenir déployé avant le parent de hello.</span><span class="sxs-lookup"><span data-stu-id="cd859-209">But, if you do not specify a dependency on hello parent resource, hello child resource may get deployed before hello parent.</span></span> <span data-ttu-id="cd859-210">tooresolve cette erreur, inclure une dépendance.</span><span class="sxs-lookup"><span data-stu-id="cd859-210">tooresolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="cd859-211">StorageAccountAlreadyExists et StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="cd859-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="cd859-212">Pour les comptes de stockage, vous devez fournir un nom pour la ressource hello qui est unique dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cd859-212">For storage accounts, you must provide a name for hello resource that is unique across Azure.</span></span> <span data-ttu-id="cd859-213">Si vous ne fournissez pas un nom unique, une erreur de ce type s’affiche :</span><span class="sxs-lookup"><span data-stu-id="cd859-213">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

<span data-ttu-id="cd859-214">Vous pouvez créer un nom unique en concaténant votre convention d’affectation de noms avec un résultat de hello hello [uniqueString](resource-group-template-functions-string.md#uniquestring) (fonction).</span><span class="sxs-lookup"><span data-stu-id="cd859-214">You can create a unique name by concatenating your naming convention with hello result of hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="cd859-215">Si vous déployez un compte de stockage avec hello de même nom qu’un compte de stockage existant dans votre abonnement, mais fournissent un autre emplacement, vous recevez une erreur indiquant compte de stockage hello existe déjà dans un autre emplacement.</span><span class="sxs-lookup"><span data-stu-id="cd859-215">If you deploy a storage account with hello same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating hello storage account already exists in a different location.</span></span> <span data-ttu-id="cd859-216">Supprimez le compte de stockage existant hello, ou fournissez hello même emplacement que hello compte de stockage existant.</span><span class="sxs-lookup"><span data-stu-id="cd859-216">Either delete hello existing storage account, or provide hello same location as hello existing storage account.</span></span>

## <a name="accountnameinvalid"></a><span data-ttu-id="cd859-217">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="cd859-217">AccountNameInvalid</span></span>
<span data-ttu-id="cd859-218">Vous consultez hello **AccountNameInvalid** lors de la tentative de toogive un stockage compte un nom qui inclut des caractères interdits.</span><span class="sxs-lookup"><span data-stu-id="cd859-218">You see hello **AccountNameInvalid** error when attempting toogive a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="cd859-219">Ce nom doit comprendre entre 3 et 24 caractères, uniquement des lettres en minuscules et des nombres.</span><span class="sxs-lookup"><span data-stu-id="cd859-219">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="cd859-220">Hello [uniqueString](resource-group-template-functions-string.md#uniquestring) fonction retourne 13 caractères.</span><span class="sxs-lookup"><span data-stu-id="cd859-220">hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="cd859-221">Si vous concaténez un préfixe toohello **uniqueString** entraîner, fournir un préfixe est de 11 caractères ou moins.</span><span class="sxs-lookup"><span data-stu-id="cd859-221">If you concatenate a prefix toohello **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

## <a name="badrequest"></a><span data-ttu-id="cd859-222">BadRequest</span><span class="sxs-lookup"><span data-stu-id="cd859-222">BadRequest</span></span>

<span data-ttu-id="cd859-223">L’état BadRequest peut survenir lorsque vous spécifiez une valeur de propriété non valide.</span><span class="sxs-lookup"><span data-stu-id="cd859-223">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="cd859-224">Par exemple, si vous fournissez une valeur incorrecte de la référence (SKU) pour un compte de stockage, déploiement de hello échoue.</span><span class="sxs-lookup"><span data-stu-id="cd859-224">For example, if you provide an incorrect SKU value for a storage account, hello deployment fails.</span></span> <span data-ttu-id="cd859-225">toodetermine les valeurs valides pour la propriété, examinez hello [API REST](/rest/api) pour le type de ressource hello vous déployez.</span><span class="sxs-lookup"><span data-stu-id="cd859-225">toodetermine valid values for property, look at hello [REST API](/rest/api) for hello resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="cd859-226">NoRegisteredProviderFound et MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="cd859-226">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="cd859-227">Lors du déploiement de ressources, vous pouvez hello suivant le code d’erreur de réception et de message :</span><span class="sxs-lookup"><span data-stu-id="cd859-227">When deploying resource, you may receive hello following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="cd859-228">Vous pouvez sinon recevoir un message similaire indiquant :</span><span class="sxs-lookup"><span data-stu-id="cd859-228">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

<span data-ttu-id="cd859-229">Ces erreurs apparaissent pour l’une des trois raisons suivantes :</span><span class="sxs-lookup"><span data-stu-id="cd859-229">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="cd859-230">fournisseur de ressources Hello n’a pas été inscrit pour votre abonnement</span><span class="sxs-lookup"><span data-stu-id="cd859-230">hello resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="cd859-231">Version de l’API non prises en charge pour le type de ressource hello</span><span class="sxs-lookup"><span data-stu-id="cd859-231">API version not supported for hello resource type</span></span>
3. <span data-ttu-id="cd859-232">Emplacement non pris en charge pour le type de ressource hello</span><span class="sxs-lookup"><span data-stu-id="cd859-232">Location not supported for hello resource type</span></span>

<span data-ttu-id="cd859-233">message d’erreur Hello doit vous fournir des suggestions pour les emplacements de hello pris en charge et les versions d’API.</span><span class="sxs-lookup"><span data-stu-id="cd859-233">hello error message should give you suggestions for hello supported locations and API versions.</span></span> <span data-ttu-id="cd859-234">Vous pouvez modifier votre tooone modèle Hello valeurs suggérées.</span><span class="sxs-lookup"><span data-stu-id="cd859-234">You can change your template tooone of hello suggested values.</span></span> <span data-ttu-id="cd859-235">La plupart des fournisseurs sont inscrits automatiquement par hello Azure portal ou hello une interface de ligne que vous utilisez, mais pas toutes.</span><span class="sxs-lookup"><span data-stu-id="cd859-235">Most providers are registered automatically by hello Azure portal or hello command-line interface you are using, but not all.</span></span> <span data-ttu-id="cd859-236">Si vous n’avez pas utilisé un fournisseur de ressources particulier avant, vous devrez peut-être tooregister ce fournisseur.</span><span class="sxs-lookup"><span data-stu-id="cd859-236">If you have not used a particular resource provider before, you may need tooregister that provider.</span></span> <span data-ttu-id="cd859-237">Vous pouvez en savoir plus sur les fournisseurs de ressources via PowerShell ou l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="cd859-237">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="cd859-238">**Portail**</span><span class="sxs-lookup"><span data-stu-id="cd859-238">**Portal**</span></span>

<span data-ttu-id="cd859-239">Vous pouvez voir l’état de l’inscription hello et enregistrer un espace de noms du fournisseur de ressources via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="cd859-239">You can see hello registration status and register a resource provider namespace through hello portal.</span></span>

1. <span data-ttu-id="cd859-240">Sur votre abonnement, sélectionnez **Fournisseurs de ressources**.</span><span class="sxs-lookup"><span data-stu-id="cd859-240">For your subscription, select **Resource providers**.</span></span>

   ![sélectionner Fournisseurs de ressources](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="cd859-242">Examinez la liste hello des fournisseurs de ressources et si nécessaire, sélectionnez hello **inscrire** fournisseur de ressources de lien tooregister hello du type de hello vous essayez de toodeploy.</span><span class="sxs-lookup"><span data-stu-id="cd859-242">Look at hello list of resource providers, and if necessary, select hello **Register** link tooregister hello resource provider of hello type you are trying toodeploy.</span></span>

   ![répertorier les fournisseurs de ressources](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="cd859-244">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="cd859-244">**PowerShell**</span></span>

<span data-ttu-id="cd859-245">toosee votre statut d’enregistrement, utilisez **Get-AzureRmResourceProvider**.</span><span class="sxs-lookup"><span data-stu-id="cd859-245">toosee your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="cd859-246">tooregister un fournisseur, utilisez **AzureRmResourceProvider de Registre** et fournissez hello nom de fournisseur de ressources hello vous souhaitez tooregister.</span><span class="sxs-lookup"><span data-stu-id="cd859-246">tooregister a provider, use **Register-AzureRmResourceProvider** and provide hello name of hello resource provider you wish tooregister.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="cd859-247">tooget les emplacements de hello pris en charge pour un type particulier de ressource, utilisez :</span><span class="sxs-lookup"><span data-stu-id="cd859-247">tooget hello supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="cd859-248">tooget hello pris en charge les versions d’API pour un type particulier de ressource, utilisez :</span><span class="sxs-lookup"><span data-stu-id="cd859-248">tooget hello supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="cd859-249">**Interface de ligne de commande Azure**</span><span class="sxs-lookup"><span data-stu-id="cd859-249">**Azure CLI**</span></span>

<span data-ttu-id="cd859-250">toosee si le fournisseur de hello est inscrit, utilisez hello `azure provider list` commande.</span><span class="sxs-lookup"><span data-stu-id="cd859-250">toosee whether hello provider is registered, use hello `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="cd859-251">tooregister un fournisseur de ressources, utilisez hello `azure provider register` de commandes et spécifiez hello *espace de noms* tooregister.</span><span class="sxs-lookup"><span data-stu-id="cd859-251">tooregister a resource provider, use hello `azure provider register` command, and specify hello *namespace* tooregister.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="cd859-252">emplacements de hello pris en charge toosee et versions d’API pour un type de ressource, utilisez :</span><span class="sxs-lookup"><span data-stu-id="cd859-252">toosee hello supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="cd859-253">QuotaExceeded et OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="cd859-253">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="cd859-254">Vous pouvez rencontrer des problèmes quand un déploiement dépasse un quota qui peut concerner entre autres les groupes de ressources, les abonnements ou les comptes.</span><span class="sxs-lookup"><span data-stu-id="cd859-254">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="cd859-255">Par exemple, votre abonnement est peut-être configuré de nombre de hello toolimit de cœurs pour une région.</span><span class="sxs-lookup"><span data-stu-id="cd859-255">For example, your subscription may be configured toolimit hello number of cores for a region.</span></span> <span data-ttu-id="cd859-256">Si vous essayez de toodeploy une machine virtuelle avec davantage de cœurs que hello Montant admis, vous recevez une erreur indiquant que hello quota a été dépassé.</span><span class="sxs-lookup"><span data-stu-id="cd859-256">If you attempt toodeploy a virtual machine with more cores than hello permitted amount, you receive an error stating hello quota has been exceeded.</span></span>
<span data-ttu-id="cd859-257">Pour obtenir des informations complètes sur les quotas, consultez [Abonnement Azure et limites, quotas et contraintes du service](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="cd859-257">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="cd859-258">tooexamine les quotas de votre abonnement pour cœurs, vous pouvez utiliser hello `azure vm list-usage` commande hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="cd859-258">tooexamine your subscription's quotas for cores, you can use hello `azure vm list-usage` command in hello Azure CLI.</span></span> <span data-ttu-id="cd859-259">Bonjour à l’exemple suivant illustre ce quota de cœurs hello pour un compte d’évaluation gratuite est 4 :</span><span class="sxs-lookup"><span data-stu-id="cd859-259">hello following example illustrates that hello core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="cd859-260">Résultat :</span><span class="sxs-lookup"><span data-stu-id="cd859-260">Which returns:</span></span>

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

<span data-ttu-id="cd859-261">Si vous déployez un modèle qui crée le plus de quatre cœurs dans la région ouest des États-Unis hello, vous obtenez une erreur de déploiement qui ressemble à :</span><span class="sxs-lookup"><span data-stu-id="cd859-261">If you deploy a template that creates more than four cores in hello West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="cd859-262">Dans PowerShell, vous pouvez également utiliser hello **Get-AzureRmVMUsage** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="cd859-262">Or in PowerShell, you can use hello **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="cd859-263">Résultat :</span><span class="sxs-lookup"><span data-stu-id="cd859-263">Which returns:</span></span>

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

<span data-ttu-id="cd859-264">Dans ces cas, vous devez accéder toohello portail et votre quota pour la région de hello dans lequel vous souhaitez toodeploy un tooraise de problème de prise en charge du fichier.</span><span class="sxs-lookup"><span data-stu-id="cd859-264">In these cases, you should go toohello portal and file a support issue tooraise your quota for hello region into which you want toodeploy.</span></span>

> [!NOTE]
> <span data-ttu-id="cd859-265">N’oubliez pas que pour les groupes de ressources, le quota de hello est pour chacune des régions, pas pour tout abonnement de hello.</span><span class="sxs-lookup"><span data-stu-id="cd859-265">Remember that for resource groups, hello quota is for each individual region, not for hello entire subscription.</span></span> <span data-ttu-id="cd859-266">Si vous avez besoin de 30 cœurs toodeploy ouest des États-Unis, vous avez tooask pour 30 cœurs de gestionnaire de ressources dans l’ouest des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="cd859-266">If you need toodeploy 30 cores in West US, you have tooask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="cd859-267">Si vous avez besoin de cœurs de 30 toodeploy dans un des hello régions toowhich vous avez accès, vous devez demander de 30 cœurs de gestionnaire de ressources dans toutes les régions.</span><span class="sxs-lookup"><span data-stu-id="cd859-267">If you need toodeploy 30 cores in any of hello regions toowhich you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

## <a name="invalidcontentlink"></a><span data-ttu-id="cd859-268">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="cd859-268">InvalidContentLink</span></span>
<span data-ttu-id="cd859-269">Lorsque vous recevez le message d’erreur hello :</span><span class="sxs-lookup"><span data-stu-id="cd859-269">When you receive hello error message:</span></span>

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

<span data-ttu-id="cd859-270">Vous avez probablement tenté modèle imbriqué toolink tooa qui n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="cd859-270">You have most likely attempted toolink tooa nested template that is not available.</span></span> <span data-ttu-id="cd859-271">Vérifiez hello URI que vous avez fourni pour les modèles imbriqués hello.</span><span class="sxs-lookup"><span data-stu-id="cd859-271">Double check hello URI you provided for hello nested template.</span></span> <span data-ttu-id="cd859-272">Si le modèle de hello existe dans un compte de stockage, vérifiez que hello URI est accessible.</span><span class="sxs-lookup"><span data-stu-id="cd859-272">If hello template exists in a storage account, make sure hello URI is accessible.</span></span> <span data-ttu-id="cd859-273">Vous devrez peut-être toopass un jeton SAP.</span><span class="sxs-lookup"><span data-stu-id="cd859-273">You may need toopass a SAS token.</span></span> <span data-ttu-id="cd859-274">Pour plus d’informations, consultez [Utilisation de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="cd859-274">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="requestdisallowedbypolicy"></a><span data-ttu-id="cd859-275">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="cd859-275">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="cd859-276">Vous recevez cette erreur lorsque votre abonnement inclut une stratégie de ressources qui empêche une action que vous essayez de tooperform durant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="cd859-276">You receive this error when your subscription includes a resource policy that prevents an action you are trying tooperform during deployment.</span></span> <span data-ttu-id="cd859-277">Dans le message d’erreur hello, recherchez l’identificateur de stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="cd859-277">In hello error message, look for hello policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="cd859-278">Dans **PowerShell**, fournir cet identificateur de stratégie en tant que hello **Id** détails du paramètre tooretrieve sur la stratégie hello qui a bloqué votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="cd859-278">In **PowerShell**, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="cd859-279">Dans **CLI d’Azure**, fournir le nom hello de définition de stratégie hello :</span><span class="sxs-lookup"><span data-stu-id="cd859-279">In **Azure CLI**, provide hello name of hello policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="cd859-280">Pour plus d’informations, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="cd859-280">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="cd859-281">Erreur RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="cd859-281">RequestDisallowedByPolicy error</span></span>](resource-manager-policy-requestdisallowedbypolicy-error.md)
- <span data-ttu-id="cd859-282">[Utiliser les ressources de la stratégie toomanage et contrôler l’accès](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="cd859-282">[Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>

## <a name="authorization-failed"></a><span data-ttu-id="cd859-283">Échec de l’autorisation</span><span class="sxs-lookup"><span data-stu-id="cd859-283">Authorization failed</span></span>
<span data-ttu-id="cd859-284">Vous pouvez recevoir une erreur lors du déploiement car hello compte ou le service principal d’essayer de ressources de hello toodeploy n’a pas accès tooperform ces actions.</span><span class="sxs-lookup"><span data-stu-id="cd859-284">You may receive an error during deployment because hello account or service principal attempting toodeploy hello resources does not have access tooperform those actions.</span></span> <span data-ttu-id="cd859-285">Azure Active Directory permet de vous ou votre toocontrol administrateur les identités peuvent accéder à quelles ressources avec un plus grand degré de précision.</span><span class="sxs-lookup"><span data-stu-id="cd859-285">Azure Active Directory enables you or your administrator toocontrol which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="cd859-286">Par exemple, si le rôle de lecteur toohello est affecté à votre compte, vous n’êtes pas en mesure de toocreate ressources.</span><span class="sxs-lookup"><span data-stu-id="cd859-286">For example, if your account is assigned toohello Reader role, you are not able toocreate resources.</span></span> <span data-ttu-id="cd859-287">Dans ce cas, vous voyez un message d’erreur indiquant que l’autorisation a échoué.</span><span class="sxs-lookup"><span data-stu-id="cd859-287">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="cd859-288">Pour plus d’informations sur le contrôle d’accès en fonction du rôle, consultez la rubrique [Contrôle d’accès en fonction du rôle d’Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="cd859-288">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="cd859-289">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cd859-289">Next steps</span></span>
* <span data-ttu-id="cd859-290">toolearn sur l’audit des actions, consultez [auditer les opérations effectuées avec le Gestionnaire de ressources](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="cd859-290">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="cd859-291">toolearn sur les erreurs de hello toodetermine actions pendant le déploiement, consultez [afficher les opérations de déploiement](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="cd859-291">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
