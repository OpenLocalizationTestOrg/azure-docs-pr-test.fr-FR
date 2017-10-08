---
title: "fonctions de modèle de gestionnaire de ressources aaaAzure - ressources | Documents Microsoft"
description: "Décrit toouse de fonctions hello dans des valeurs de tooretrieve modèles Azure Resource Manager sur les ressources."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="34cfc-103">Fonctions de ressources pour les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="34cfc-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="34cfc-104">Gestionnaire de ressources fournit hello suivant des fonctions pour obtenir des valeurs de ressource :</span><span class="sxs-lookup"><span data-stu-id="34cfc-104">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="34cfc-105">listKeys and list{Value}</span><span class="sxs-lookup"><span data-stu-id="34cfc-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="34cfc-106">fournisseurs</span><span class="sxs-lookup"><span data-stu-id="34cfc-106">providers</span></span>](#providers)
* [<span data-ttu-id="34cfc-107">reference</span><span class="sxs-lookup"><span data-stu-id="34cfc-107">reference</span></span>](#reference)
* [<span data-ttu-id="34cfc-108">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="34cfc-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="34cfc-109">resourceId</span><span class="sxs-lookup"><span data-stu-id="34cfc-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="34cfc-110">abonnement</span><span class="sxs-lookup"><span data-stu-id="34cfc-110">subscription</span></span>](#subscription)

<span data-ttu-id="34cfc-111">tooget les valeurs de paramètres, variables ou hello en cours de déploiement, consultez [fonctions déploiement](resource-group-template-functions-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="34cfc-111">tooget values from parameters, variables, or hello current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="34cfc-112">listKeys and list{Value}</span><span class="sxs-lookup"><span data-stu-id="34cfc-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="34cfc-113">Retourne hello des valeurs pour n’importe quel type de ressource qui prend en charge d’opération de liste hello.</span><span class="sxs-lookup"><span data-stu-id="34cfc-113">Returns hello values for any resource type that supports hello list operation.</span></span> <span data-ttu-id="34cfc-114">est de l’utilisation la plus courante Hello `listKeys`.</span><span class="sxs-lookup"><span data-stu-id="34cfc-114">hello most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="34cfc-115">Paramètres</span><span class="sxs-lookup"><span data-stu-id="34cfc-115">Parameters</span></span>

| <span data-ttu-id="34cfc-116">Paramètre</span><span class="sxs-lookup"><span data-stu-id="34cfc-116">Parameter</span></span> | <span data-ttu-id="34cfc-117">Requis</span><span class="sxs-lookup"><span data-stu-id="34cfc-117">Required</span></span> | <span data-ttu-id="34cfc-118">Type</span><span class="sxs-lookup"><span data-stu-id="34cfc-118">Type</span></span> | <span data-ttu-id="34cfc-119">Description</span><span class="sxs-lookup"><span data-stu-id="34cfc-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="34cfc-120">nom_ressource ou identificateur_ressource</span><span class="sxs-lookup"><span data-stu-id="34cfc-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="34cfc-121">Oui</span><span class="sxs-lookup"><span data-stu-id="34cfc-121">Yes</span></span> |<span data-ttu-id="34cfc-122">string</span><span class="sxs-lookup"><span data-stu-id="34cfc-122">string</span></span> |<span data-ttu-id="34cfc-123">Identificateur unique pour la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="34cfc-123">Unique identifier for hello resource.</span></span> |
| <span data-ttu-id="34cfc-124">apiVersion</span><span class="sxs-lookup"><span data-stu-id="34cfc-124">apiVersion</span></span> |<span data-ttu-id="34cfc-125">Oui</span><span class="sxs-lookup"><span data-stu-id="34cfc-125">Yes</span></span> |<span data-ttu-id="34cfc-126">string</span><span class="sxs-lookup"><span data-stu-id="34cfc-126">string</span></span> |<span data-ttu-id="34cfc-127">Version d'API de l'état d'exécution des ressources.</span><span class="sxs-lookup"><span data-stu-id="34cfc-127">API version of resource runtime state.</span></span> <span data-ttu-id="34cfc-128">En règle générale, dans le format de hello, **aaaa-mm-jj**.</span><span class="sxs-lookup"><span data-stu-id="34cfc-128">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="34cfc-129">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="34cfc-129">Return value</span></span>

<span data-ttu-id="34cfc-130">Hello a renvoyé un objet de listKeys aura hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="34cfc-130">hello returned object from listKeys has hello following format:</span></span>

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

<span data-ttu-id="34cfc-131">D’autres fonctions de liste ont différents formats de retour.</span><span class="sxs-lookup"><span data-stu-id="34cfc-131">Other list functions have different return formats.</span></span> <span data-ttu-id="34cfc-132">format de hello toosee d’une fonction, incluez-le dans la section des sorties hello comme indiqué dans l’exemple de modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="34cfc-132">toosee hello format of a function, include it in hello outputs section as shown in hello example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="34cfc-133">Remarques</span><span class="sxs-lookup"><span data-stu-id="34cfc-133">Remarks</span></span>

<span data-ttu-id="34cfc-134">Toute opération qui commence par **list** peut être utilisée en tant que fonction dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="34cfc-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="34cfc-135">les opérations disponibles Hello incluent non seulement le listKeys, mais également des opérations telles que `list`, `listAdminKeys`, et `listStatus`.</span><span class="sxs-lookup"><span data-stu-id="34cfc-135">hello available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="34cfc-136">Toutefois, vous ne pouvez pas utiliser **liste** les opérations qui requièrent des valeurs Bonjour corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="34cfc-136">However, you cannot use **list** operations that require values in hello request body.</span></span> <span data-ttu-id="34cfc-137">Par exemple, hello [liste compte SAP](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) opération nécessite des paramètres de corps de la demande, tels que *signedExpiry*, vous ne pouvez pas l’utiliser dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="34cfc-137">For example, hello [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="34cfc-138">toodetermine les types de ressources dont une opération de liste, vous avez hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="34cfc-138">toodetermine which resource types have a list operation, you have hello following options:</span></span>

* <span data-ttu-id="34cfc-139">Hello de vue [opérations d’API REST](/rest/api/) pour un fournisseur de ressources et recherchez les opérations de liste.</span><span class="sxs-lookup"><span data-stu-id="34cfc-139">View hello [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="34cfc-140">Par exemple, comptes de stockage se hello [listKeys opération](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span><span class="sxs-lookup"><span data-stu-id="34cfc-140">For example, storage accounts have hello [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="34cfc-141">Hello d’utilisation [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="34cfc-141">Use hello [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="34cfc-142">Hello exemple ci-dessous obtient toutes les opérations de liste pour les comptes de stockage :</span><span class="sxs-lookup"><span data-stu-id="34cfc-142">hello following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="34cfc-143">Utilisez hello commande CLI d’Azure toofilter hello uniquement les opérations de la liste suivante :</span><span class="sxs-lookup"><span data-stu-id="34cfc-143">Use hello following Azure CLI command toofilter only hello list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="34cfc-144">Spécifier les ressources hello à l’aide soit hello [fonction resourceId](#resourceid), ou le format de hello `{providerNamespace}/{resourceType}/{resourceName}`.</span><span class="sxs-lookup"><span data-stu-id="34cfc-144">Specify hello resource by using either hello [resourceId function](#resourceid), or hello format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="34cfc-145">Exemple</span><span class="sxs-lookup"><span data-stu-id="34cfc-145">Example</span></span>

<span data-ttu-id="34cfc-146">Hello suivant montre comment tooreturn hello secondaire les clés primaires et à partir d’un compte de stockage Bonjour génère la section.</span><span class="sxs-lookup"><span data-stu-id="34cfc-146">hello following example shows how tooreturn hello primary and secondary keys from a storage account in hello outputs section.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a><span data-ttu-id="34cfc-147">fournisseurs</span><span class="sxs-lookup"><span data-stu-id="34cfc-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="34cfc-148">Renvoie des informations sur un fournisseur de ressources et les types de ressources qu’il prend en charge.</span><span class="sxs-lookup"><span data-stu-id="34cfc-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="34cfc-149">Si vous ne fournissez pas un type de ressource, la fonction hello retourne tous les types hello pris en charge pour le fournisseur de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="34cfc-149">If you do not provide a resource type, hello function returns all hello supported types for hello resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="34cfc-150">Paramètres</span><span class="sxs-lookup"><span data-stu-id="34cfc-150">Parameters</span></span>

| <span data-ttu-id="34cfc-151">Paramètre</span><span class="sxs-lookup"><span data-stu-id="34cfc-151">Parameter</span></span> | <span data-ttu-id="34cfc-152">Requis</span><span class="sxs-lookup"><span data-stu-id="34cfc-152">Required</span></span> | <span data-ttu-id="34cfc-153">Type</span><span class="sxs-lookup"><span data-stu-id="34cfc-153">Type</span></span> | <span data-ttu-id="34cfc-154">Description</span><span class="sxs-lookup"><span data-stu-id="34cfc-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="34cfc-155">espacedenoms_fournisseur</span><span class="sxs-lookup"><span data-stu-id="34cfc-155">providerNamespace</span></span> |<span data-ttu-id="34cfc-156">Oui</span><span class="sxs-lookup"><span data-stu-id="34cfc-156">Yes</span></span> |<span data-ttu-id="34cfc-157">string</span><span class="sxs-lookup"><span data-stu-id="34cfc-157">string</span></span> |<span data-ttu-id="34cfc-158">Namespace du fournisseur de hello</span><span class="sxs-lookup"><span data-stu-id="34cfc-158">Namespace of hello provider</span></span> |
| <span data-ttu-id="34cfc-159">resourceType</span><span class="sxs-lookup"><span data-stu-id="34cfc-159">resourceType</span></span> |<span data-ttu-id="34cfc-160">Non</span><span class="sxs-lookup"><span data-stu-id="34cfc-160">No</span></span> |<span data-ttu-id="34cfc-161">string</span><span class="sxs-lookup"><span data-stu-id="34cfc-161">string</span></span> |<span data-ttu-id="34cfc-162">type Hello de ressource dans hello spécifié l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="34cfc-162">hello type of resource within hello specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="34cfc-163">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="34cfc-163">Return value</span></span>

<span data-ttu-id="34cfc-164">Chaque type pris en charge est retourné dans hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="34cfc-164">Each supported type is returned in hello following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="34cfc-165">Tableau classement Hello retourné de valeurs n’est pas garantie.</span><span class="sxs-lookup"><span data-stu-id="34cfc-165">Array ordering of hello returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="34cfc-166">Exemple</span><span class="sxs-lookup"><span data-stu-id="34cfc-166">Example</span></span>

<span data-ttu-id="34cfc-167">Bonjour à l’exemple suivant montre comment toouse hello fonction du fournisseur :</span><span class="sxs-lookup"><span data-stu-id="34cfc-167">hello following example shows how toouse hello provider function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="34cfc-168">Hello exemple précédent retourne un objet Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="34cfc-168">hello preceding example returns an object in hello following format:</span></span>

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a><span data-ttu-id="34cfc-169">reference</span><span class="sxs-lookup"><span data-stu-id="34cfc-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="34cfc-170">Renvoie un objet représentant l’état d’exécution d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="34cfc-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="34cfc-171">Paramètres</span><span class="sxs-lookup"><span data-stu-id="34cfc-171">Parameters</span></span>

| <span data-ttu-id="34cfc-172">Paramètre</span><span class="sxs-lookup"><span data-stu-id="34cfc-172">Parameter</span></span> | <span data-ttu-id="34cfc-173">Requis</span><span class="sxs-lookup"><span data-stu-id="34cfc-173">Required</span></span> | <span data-ttu-id="34cfc-174">Type</span><span class="sxs-lookup"><span data-stu-id="34cfc-174">Type</span></span> | <span data-ttu-id="34cfc-175">Description</span><span class="sxs-lookup"><span data-stu-id="34cfc-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="34cfc-176">nom_ressource ou identificateur_ressource</span><span class="sxs-lookup"><span data-stu-id="34cfc-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="34cfc-177">Oui</span><span class="sxs-lookup"><span data-stu-id="34cfc-177">Yes</span></span> |<span data-ttu-id="34cfc-178">string</span><span class="sxs-lookup"><span data-stu-id="34cfc-178">string</span></span> |<span data-ttu-id="34cfc-179">Nom ou identificateur unique d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="34cfc-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="34cfc-180">apiVersion</span><span class="sxs-lookup"><span data-stu-id="34cfc-180">apiVersion</span></span> |<span data-ttu-id="34cfc-181">Non</span><span class="sxs-lookup"><span data-stu-id="34cfc-181">No</span></span> |<span data-ttu-id="34cfc-182">string</span><span class="sxs-lookup"><span data-stu-id="34cfc-182">string</span></span> |<span data-ttu-id="34cfc-183">Version de l’API de hello la ressource spécifiée.</span><span class="sxs-lookup"><span data-stu-id="34cfc-183">API version of hello specified resource.</span></span> <span data-ttu-id="34cfc-184">Incluez ce paramètre lors de la ressource de hello n’est pas configuré dans le même modèle.</span><span class="sxs-lookup"><span data-stu-id="34cfc-184">Include this parameter when hello resource is not provisioned within same template.</span></span> <span data-ttu-id="34cfc-185">En règle générale, dans le format de hello, **aaaa-mm-jj**.</span><span class="sxs-lookup"><span data-stu-id="34cfc-185">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="34cfc-186">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="34cfc-186">Return value</span></span>

<span data-ttu-id="34cfc-187">Chaque type de ressource retourne des propriétés différentes pour la fonction de référence hello.</span><span class="sxs-lookup"><span data-stu-id="34cfc-187">Every resource type returns different properties for hello reference function.</span></span> <span data-ttu-id="34cfc-188">fonction Hello ne retourne pas un format unique, prédéfini.</span><span class="sxs-lookup"><span data-stu-id="34cfc-188">hello function does not return a single, predefined format.</span></span> <span data-ttu-id="34cfc-189">propriétés de hello toosee pour un type de ressource, retourner objet hello Bonjour génère section comme indiqué dans l’exemple de hello.</span><span class="sxs-lookup"><span data-stu-id="34cfc-189">toosee hello properties for a resource type, return hello object in hello outputs section as shown in hello example.</span></span>

### <a name="remarks"></a><span data-ttu-id="34cfc-190">Remarques</span><span class="sxs-lookup"><span data-stu-id="34cfc-190">Remarks</span></span>

<span data-ttu-id="34cfc-191">référence de fonction Hello dérive sa valeur à partir d’un état d’exécution et ne peut donc pas être utilisé dans la section des variables hello.</span><span class="sxs-lookup"><span data-stu-id="34cfc-191">hello reference function derives its value from a runtime state, and therefore cannot be used in hello variables section.</span></span> <span data-ttu-id="34cfc-192">Elle peut être utilisée dans la section outputs d'un modèle.</span><span class="sxs-lookup"><span data-stu-id="34cfc-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="34cfc-193">À l’aide de référence de fonction hello, vous déclarez implicitement qu’une ressource dépend d’une autre ressource, si les ressources hello référencé sont configuré au sein du même modèle.</span><span class="sxs-lookup"><span data-stu-id="34cfc-193">By using hello reference function, you implicitly declare that one resource depends on another resource if hello referenced resource is provisioned within same template.</span></span> <span data-ttu-id="34cfc-194">Vous n’avez pas besoin de la propriété : dependsOn de tooalso utiliser hello.</span><span class="sxs-lookup"><span data-stu-id="34cfc-194">You do not need tooalso use hello dependsOn property.</span></span> <span data-ttu-id="34cfc-195">Hello fonction n’est pas été évaluée jusqu'à hello ressource référencée fin de déploiement.</span><span class="sxs-lookup"><span data-stu-id="34cfc-195">hello function is not evaluated until hello referenced resource has completed deployment.</span></span>

<span data-ttu-id="34cfc-196">toosee hello noms et valeurs pour un type de ressource, créez un modèle qui retourne un objet de hello dans la section des sorties hello.</span><span class="sxs-lookup"><span data-stu-id="34cfc-196">toosee hello property names and values for a resource type, create a template that returns hello object in hello outputs section.</span></span> <span data-ttu-id="34cfc-197">Si vous disposez d’une ressource de ce type, votre modèle retourne les objet hello sans déployer toutes les nouvelles ressources.</span><span class="sxs-lookup"><span data-stu-id="34cfc-197">If you have an existing resource of that type, your template returns hello object without deploying any new resources.</span></span> 

<span data-ttu-id="34cfc-198">En général, vous utilisez hello **référence** tooreturn une valeur particulière d’un objet, tel que du point de terminaison hello blob URI ou le nom de domaine complet de la fonction.</span><span class="sxs-lookup"><span data-stu-id="34cfc-198">Typically, you use hello **reference** function tooreturn a particular value from an object, such as hello blob endpoint URI or fully qualified domain name.</span></span>

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a><span data-ttu-id="34cfc-199">Exemple</span><span class="sxs-lookup"><span data-stu-id="34cfc-199">Example</span></span>

<span data-ttu-id="34cfc-200">Guide de référence et toodeploy ressource hello Bonjour même modèle, utilisez :</span><span class="sxs-lookup"><span data-stu-id="34cfc-200">toodeploy and reference hello resource in hello same template, use:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

<span data-ttu-id="34cfc-201">Hello exemple précédent retourne un objet Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="34cfc-201">hello preceding example returns an object in hello following format:</span></span>

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

<span data-ttu-id="34cfc-202">Hello exemple suivant fait référence à un compte de stockage qui n’est pas déployé dans ce modèle.</span><span class="sxs-lookup"><span data-stu-id="34cfc-202">hello following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="34cfc-203">Hello compte de stockage existe déjà dans hello même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="34cfc-203">hello storage account already exists within hello same resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a><span data-ttu-id="34cfc-204">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="34cfc-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="34cfc-205">Retourne un objet qui représente le groupe de ressources actuel hello.</span><span class="sxs-lookup"><span data-stu-id="34cfc-205">Returns an object that represents hello current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="34cfc-206">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="34cfc-206">Return value</span></span>

<span data-ttu-id="34cfc-207">Hello retournée objet est Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="34cfc-207">hello returned object is in hello following format:</span></span>

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a><span data-ttu-id="34cfc-208">Remarques</span><span class="sxs-lookup"><span data-stu-id="34cfc-208">Remarks</span></span>

<span data-ttu-id="34cfc-209">Une utilisation courante de la fonction du groupe de ressources hello est ressources toocreate Bonjour même emplacement que le groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="34cfc-209">A common use of hello resourceGroup function is toocreate resources in hello same location as hello resource group.</span></span> <span data-ttu-id="34cfc-210">Hello exemple suivant utilise hello ressource groupe emplacement tooassign hello emplacement pour un site web.</span><span class="sxs-lookup"><span data-stu-id="34cfc-210">hello following example uses hello resource group location tooassign hello location for a web site.</span></span>

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="34cfc-211">Exemple</span><span class="sxs-lookup"><span data-stu-id="34cfc-211">Example</span></span>

<span data-ttu-id="34cfc-212">Hello modèle suivant retourne les propriétés hello hello du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="34cfc-212">hello following template returns hello properties of hello resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="34cfc-213">Hello exemple précédent retourne un objet Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="34cfc-213">hello preceding example returns an object in hello following format:</span></span>

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a><span data-ttu-id="34cfc-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="34cfc-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="34cfc-215">Retourne hello identificateur unique d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="34cfc-215">Returns hello unique identifier of a resource.</span></span> <span data-ttu-id="34cfc-216">Vous utilisez cette fonction lorsque le nom de la ressource hello est ambigu ou non configuré dans hello même modèle.</span><span class="sxs-lookup"><span data-stu-id="34cfc-216">You use this function when hello resource name is ambiguous or not provisioned within hello same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="34cfc-217">Paramètres</span><span class="sxs-lookup"><span data-stu-id="34cfc-217">Parameters</span></span>

| <span data-ttu-id="34cfc-218">Paramètre</span><span class="sxs-lookup"><span data-stu-id="34cfc-218">Parameter</span></span> | <span data-ttu-id="34cfc-219">Requis</span><span class="sxs-lookup"><span data-stu-id="34cfc-219">Required</span></span> | <span data-ttu-id="34cfc-220">Type</span><span class="sxs-lookup"><span data-stu-id="34cfc-220">Type</span></span> | <span data-ttu-id="34cfc-221">Description</span><span class="sxs-lookup"><span data-stu-id="34cfc-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="34cfc-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="34cfc-222">subscriptionId</span></span> |<span data-ttu-id="34cfc-223">Non</span><span class="sxs-lookup"><span data-stu-id="34cfc-223">No</span></span> |<span data-ttu-id="34cfc-224">string (au format GUID)</span><span class="sxs-lookup"><span data-stu-id="34cfc-224">string (In GUID format)</span></span> |<span data-ttu-id="34cfc-225">Valeur par défaut est un abonnement hello.</span><span class="sxs-lookup"><span data-stu-id="34cfc-225">Default value is hello current subscription.</span></span> <span data-ttu-id="34cfc-226">Spécifiez cette valeur lorsque vous avez besoin de tooretrieve une ressource dans un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="34cfc-226">Specify this value when you need tooretrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="34cfc-227">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="34cfc-227">resourceGroupName</span></span> |<span data-ttu-id="34cfc-228">Non</span><span class="sxs-lookup"><span data-stu-id="34cfc-228">No</span></span> |<span data-ttu-id="34cfc-229">string</span><span class="sxs-lookup"><span data-stu-id="34cfc-229">string</span></span> |<span data-ttu-id="34cfc-230">La valeur par défaut est le groupe de ressources actuel.</span><span class="sxs-lookup"><span data-stu-id="34cfc-230">Default value is current resource group.</span></span> <span data-ttu-id="34cfc-231">Spécifiez cette valeur lorsque vous avez besoin de tooretrieve une ressource dans un autre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="34cfc-231">Specify this value when you need tooretrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="34cfc-232">resourceType</span><span class="sxs-lookup"><span data-stu-id="34cfc-232">resourceType</span></span> |<span data-ttu-id="34cfc-233">Oui</span><span class="sxs-lookup"><span data-stu-id="34cfc-233">Yes</span></span> |<span data-ttu-id="34cfc-234">string</span><span class="sxs-lookup"><span data-stu-id="34cfc-234">string</span></span> |<span data-ttu-id="34cfc-235">Type de ressource, y compris l'espace de noms du fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="34cfc-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="34cfc-236">nom_ressource1</span><span class="sxs-lookup"><span data-stu-id="34cfc-236">resourceName1</span></span> |<span data-ttu-id="34cfc-237">Oui</span><span class="sxs-lookup"><span data-stu-id="34cfc-237">Yes</span></span> |<span data-ttu-id="34cfc-238">string</span><span class="sxs-lookup"><span data-stu-id="34cfc-238">string</span></span> |<span data-ttu-id="34cfc-239">Nom de la ressource.</span><span class="sxs-lookup"><span data-stu-id="34cfc-239">Name of resource.</span></span> |
| <span data-ttu-id="34cfc-240">nom_ressource2</span><span class="sxs-lookup"><span data-stu-id="34cfc-240">resourceName2</span></span> |<span data-ttu-id="34cfc-241">Non</span><span class="sxs-lookup"><span data-stu-id="34cfc-241">No</span></span> |<span data-ttu-id="34cfc-242">string</span><span class="sxs-lookup"><span data-stu-id="34cfc-242">string</span></span> |<span data-ttu-id="34cfc-243">Segment de nom de ressource suivant si la ressource est imbriquée.</span><span class="sxs-lookup"><span data-stu-id="34cfc-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="34cfc-244">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="34cfc-244">Return value</span></span>

<span data-ttu-id="34cfc-245">identificateur de Hello est retourné dans hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="34cfc-245">hello identifier is returned in hello following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="34cfc-246">Remarques</span><span class="sxs-lookup"><span data-stu-id="34cfc-246">Remarks</span></span>

<span data-ttu-id="34cfc-247">Hello des valeurs de paramètre que vous spécifiez dépendent de la ressource de hello Bonjour même groupe d’abonnement et de ressources en tant que déploiement hello en cours.</span><span class="sxs-lookup"><span data-stu-id="34cfc-247">hello parameter values you specify depend on whether hello resource is in hello same subscription and resource group as hello current deployment.</span></span>

<span data-ttu-id="34cfc-248">ID de ressource de hello tooget pour un compte de stockage Bonjour même abonnement et le groupe de ressources, utilisez :</span><span class="sxs-lookup"><span data-stu-id="34cfc-248">tooget hello resource ID for a storage account in hello same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="34cfc-249">ID de ressource tooget hello pour un compte de stockage dans hello même abonnement, mais d’un autre groupe de ressources, utilisez :</span><span class="sxs-lookup"><span data-stu-id="34cfc-249">tooget hello resource ID for a storage account in hello same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="34cfc-250">ID de ressource tooget hello pour un compte de stockage dans un autre abonnement et le groupe de ressources, utilisez :</span><span class="sxs-lookup"><span data-stu-id="34cfc-250">tooget hello resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="34cfc-251">ID de ressource tooget hello pour une base de données dans un autre groupe de ressources, utilisez :</span><span class="sxs-lookup"><span data-stu-id="34cfc-251">tooget hello resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="34cfc-252">Vous devez souvent toouse cette fonction lorsque vous utilisez un compte de stockage ou d’un réseau virtuel dans un groupe de ressources différent.</span><span class="sxs-lookup"><span data-stu-id="34cfc-252">Often, you need toouse this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="34cfc-253">Hello exemple suivant montre comment une ressource à partir d’un groupe de ressources externes peut facilement être utilisée :</span><span class="sxs-lookup"><span data-stu-id="34cfc-253">hello following example shows how a resource from an external resource group can easily be used:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a><span data-ttu-id="34cfc-254">Exemple</span><span class="sxs-lookup"><span data-stu-id="34cfc-254">Example</span></span>

<span data-ttu-id="34cfc-255">Hello exemple suivant renvoie les ID de ressource hello pour un compte de stockage dans le groupe de ressources hello :</span><span class="sxs-lookup"><span data-stu-id="34cfc-255">hello following example returns hello resource ID for a storage account in hello resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="34cfc-256">Hello de sortie à partir de hello précédent exemple hello valeurs par défaut est :</span><span class="sxs-lookup"><span data-stu-id="34cfc-256">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="34cfc-257">Nom</span><span class="sxs-lookup"><span data-stu-id="34cfc-257">Name</span></span> | <span data-ttu-id="34cfc-258">Type</span><span class="sxs-lookup"><span data-stu-id="34cfc-258">Type</span></span> | <span data-ttu-id="34cfc-259">Valeur</span><span class="sxs-lookup"><span data-stu-id="34cfc-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="34cfc-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="34cfc-260">sameRGOutput</span></span> | <span data-ttu-id="34cfc-261">String</span><span class="sxs-lookup"><span data-stu-id="34cfc-261">String</span></span> | <span data-ttu-id="34cfc-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="34cfc-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="34cfc-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="34cfc-263">differentRGOutput</span></span> | <span data-ttu-id="34cfc-264">String</span><span class="sxs-lookup"><span data-stu-id="34cfc-264">String</span></span> | <span data-ttu-id="34cfc-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="34cfc-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="34cfc-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="34cfc-266">differentSubOutput</span></span> | <span data-ttu-id="34cfc-267">String</span><span class="sxs-lookup"><span data-stu-id="34cfc-267">String</span></span> | <span data-ttu-id="34cfc-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="34cfc-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="34cfc-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="34cfc-269">nestedResourceOutput</span></span> | <span data-ttu-id="34cfc-270">String</span><span class="sxs-lookup"><span data-stu-id="34cfc-270">String</span></span> | <span data-ttu-id="34cfc-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="34cfc-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="34cfc-272">abonnement</span><span class="sxs-lookup"><span data-stu-id="34cfc-272">subscription</span></span>
`subscription()`

<span data-ttu-id="34cfc-273">Retourne le plus d’informations sur l’abonnement hello pour le déploiement en cours de hello.</span><span class="sxs-lookup"><span data-stu-id="34cfc-273">Returns details about hello subscription for hello current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="34cfc-274">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="34cfc-274">Return value</span></span>

<span data-ttu-id="34cfc-275">fonction Hello renvoie hello suivant le format :</span><span class="sxs-lookup"><span data-stu-id="34cfc-275">hello function returns hello following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="34cfc-276">Exemple</span><span class="sxs-lookup"><span data-stu-id="34cfc-276">Example</span></span>

<span data-ttu-id="34cfc-277">Hello exemple suivant illustre hello abonnement fonction est appelée dans la section des sorties hello.</span><span class="sxs-lookup"><span data-stu-id="34cfc-277">hello following example shows hello subscription function called in hello outputs section.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="34cfc-278">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="34cfc-278">Next steps</span></span>
* <span data-ttu-id="34cfc-279">Pour obtenir une description des sections de hello dans un modèle Azure Resource Manager, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="34cfc-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="34cfc-280">consultez de plusieurs modèles toomerge [à l’aide de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="34cfc-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="34cfc-281">tooiterate un nombre spécifié de fois lors de la création d’un type de ressource, consultez [créer plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="34cfc-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="34cfc-282">toosee modèle de hello toodeploy que vous avez créé, voir [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="34cfc-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

