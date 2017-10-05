---
title: "Ressources - fonctions de modèle Azure Resource Manager | Microsoft Docs"
description: "Décrit les fonctions à utiliser dans un modèle Azure Resource Manager pour récupérer des valeurs sur les ressources."
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
ms.openlocfilehash: 494ade55f21c19d9c68d5cc52756528401d9bb77
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="0877b-103">Fonctions de ressources pour les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0877b-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="0877b-104">Resource Manager offre les fonctions ci-après pour obtenir des valeurs de ressource :</span><span class="sxs-lookup"><span data-stu-id="0877b-104">Resource Manager provides the following functions for getting resource values:</span></span>

* [<span data-ttu-id="0877b-105">listKeys and list{Value}</span><span class="sxs-lookup"><span data-stu-id="0877b-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="0877b-106">fournisseurs</span><span class="sxs-lookup"><span data-stu-id="0877b-106">providers</span></span>](#providers)
* [<span data-ttu-id="0877b-107">reference</span><span class="sxs-lookup"><span data-stu-id="0877b-107">reference</span></span>](#reference)
* [<span data-ttu-id="0877b-108">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="0877b-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="0877b-109">resourceId</span><span class="sxs-lookup"><span data-stu-id="0877b-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="0877b-110">abonnement</span><span class="sxs-lookup"><span data-stu-id="0877b-110">subscription</span></span>](#subscription)

<span data-ttu-id="0877b-111">Pour obtenir des valeurs de paramètres, de variables ou du déploiement actuel, consultez [Fonctions de valeur de déploiement](resource-group-template-functions-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="0877b-111">To get values from parameters, variables, or the current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="0877b-112">listKeys and list{Value}</span><span class="sxs-lookup"><span data-stu-id="0877b-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="0877b-113">Renvoie les valeurs pour n’importe quel type de ressource qui prend en charge l’opération list.</span><span class="sxs-lookup"><span data-stu-id="0877b-113">Returns the values for any resource type that supports the list operation.</span></span> <span data-ttu-id="0877b-114">L’utilisation la plus courante est `listKeys`.</span><span class="sxs-lookup"><span data-stu-id="0877b-114">The most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="0877b-115">Paramètres</span><span class="sxs-lookup"><span data-stu-id="0877b-115">Parameters</span></span>

| <span data-ttu-id="0877b-116">Paramètre</span><span class="sxs-lookup"><span data-stu-id="0877b-116">Parameter</span></span> | <span data-ttu-id="0877b-117">Requis</span><span class="sxs-lookup"><span data-stu-id="0877b-117">Required</span></span> | <span data-ttu-id="0877b-118">Type</span><span class="sxs-lookup"><span data-stu-id="0877b-118">Type</span></span> | <span data-ttu-id="0877b-119">Description</span><span class="sxs-lookup"><span data-stu-id="0877b-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0877b-120">nom_ressource ou identificateur_ressource</span><span class="sxs-lookup"><span data-stu-id="0877b-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="0877b-121">Oui</span><span class="sxs-lookup"><span data-stu-id="0877b-121">Yes</span></span> |<span data-ttu-id="0877b-122">string</span><span class="sxs-lookup"><span data-stu-id="0877b-122">string</span></span> |<span data-ttu-id="0877b-123">Identificateur unique pour la ressource.</span><span class="sxs-lookup"><span data-stu-id="0877b-123">Unique identifier for the resource.</span></span> |
| <span data-ttu-id="0877b-124">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0877b-124">apiVersion</span></span> |<span data-ttu-id="0877b-125">Oui</span><span class="sxs-lookup"><span data-stu-id="0877b-125">Yes</span></span> |<span data-ttu-id="0877b-126">string</span><span class="sxs-lookup"><span data-stu-id="0877b-126">string</span></span> |<span data-ttu-id="0877b-127">Version d'API de l'état d'exécution des ressources.</span><span class="sxs-lookup"><span data-stu-id="0877b-127">API version of resource runtime state.</span></span> <span data-ttu-id="0877b-128">En règle générale, au format, **aaaa-mm-jj**.</span><span class="sxs-lookup"><span data-stu-id="0877b-128">Typically, in the format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="0877b-129">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="0877b-129">Return value</span></span>

<span data-ttu-id="0877b-130">L’objet renvoyé par listKeys a le format suivant :</span><span class="sxs-lookup"><span data-stu-id="0877b-130">The returned object from listKeys has the following format:</span></span>

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

<span data-ttu-id="0877b-131">D’autres fonctions de liste ont différents formats de retour.</span><span class="sxs-lookup"><span data-stu-id="0877b-131">Other list functions have different return formats.</span></span> <span data-ttu-id="0877b-132">Pour afficher le format d’une fonction, incluez-le dans la section des sorties comme indiqué dans l’exemple de modèle.</span><span class="sxs-lookup"><span data-stu-id="0877b-132">To see the format of a function, include it in the outputs section as shown in the example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="0877b-133">Remarques</span><span class="sxs-lookup"><span data-stu-id="0877b-133">Remarks</span></span>

<span data-ttu-id="0877b-134">Toute opération qui commence par **list** peut être utilisée en tant que fonction dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="0877b-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="0877b-135">Les opérations disponibles incluent non seulement listKeys, mais également des opérations telles que `list`, `listAdminKeys` et `listStatus`.</span><span class="sxs-lookup"><span data-stu-id="0877b-135">The available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="0877b-136">Toutefois, vous ne pouvez pas utiliser les opérations de **liste** qui requièrent des valeurs dans le corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="0877b-136">However, you cannot use **list** operations that require values in the request body.</span></span> <span data-ttu-id="0877b-137">Par exemple, l’opération de [signature d’accès partagé de compte de liste](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) nécessite des paramètres de corps de la demande, tels que *signedExpiry* ; par conséquent, vous ne pouvez pas l’utiliser dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="0877b-137">For example, the [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="0877b-138">Pour déterminer les types de ressources qui ont une opération de liste, utilisez les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="0877b-138">To determine which resource types have a list operation, you have the following options:</span></span>

* <span data-ttu-id="0877b-139">Affichez les [opérations d’API REST](/rest/api/) pour un fournisseur de ressources et recherchez les opérations de liste.</span><span class="sxs-lookup"><span data-stu-id="0877b-139">View the [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="0877b-140">Par exemple, les comptes de stockage présentent l’[opération listKeys](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span><span class="sxs-lookup"><span data-stu-id="0877b-140">For example, storage accounts have the [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="0877b-141">Utilisez l’applet de commande PowerShell [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation).</span><span class="sxs-lookup"><span data-stu-id="0877b-141">Use the [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="0877b-142">L’exemple ci-dessous obtient toutes les opérations de liste pour les comptes de stockage :</span><span class="sxs-lookup"><span data-stu-id="0877b-142">The following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="0877b-143">Utilisez la commande Azure CLI suivante pour filtrer uniquement les opérations de liste :</span><span class="sxs-lookup"><span data-stu-id="0877b-143">Use the following Azure CLI command to filter only the list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="0877b-144">Spécifiez la ressource en utilisant la [fonction resourceId](#resourceid) ou le format `{providerNamespace}/{resourceType}/{resourceName}`.</span><span class="sxs-lookup"><span data-stu-id="0877b-144">Specify the resource by using either the [resourceId function](#resourceid), or the format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="0877b-145">Exemple</span><span class="sxs-lookup"><span data-stu-id="0877b-145">Example</span></span>

<span data-ttu-id="0877b-146">L’exemple suivant montre comment renvoyer les clés primaires et secondaires à partir d’un compte de stockage dans la section outputs.</span><span class="sxs-lookup"><span data-stu-id="0877b-146">The following example shows how to return the primary and secondary keys from a storage account in the outputs section.</span></span>

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

## <a name="providers"></a><span data-ttu-id="0877b-147">fournisseurs</span><span class="sxs-lookup"><span data-stu-id="0877b-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="0877b-148">Renvoie des informations sur un fournisseur de ressources et les types de ressources qu’il prend en charge.</span><span class="sxs-lookup"><span data-stu-id="0877b-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="0877b-149">Si vous ne fournissez pas un type de ressource, la fonction renvoie tous les types pris en charge pour le fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="0877b-149">If you do not provide a resource type, the function returns all the supported types for the resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="0877b-150">Paramètres</span><span class="sxs-lookup"><span data-stu-id="0877b-150">Parameters</span></span>

| <span data-ttu-id="0877b-151">Paramètre</span><span class="sxs-lookup"><span data-stu-id="0877b-151">Parameter</span></span> | <span data-ttu-id="0877b-152">Requis</span><span class="sxs-lookup"><span data-stu-id="0877b-152">Required</span></span> | <span data-ttu-id="0877b-153">Type</span><span class="sxs-lookup"><span data-stu-id="0877b-153">Type</span></span> | <span data-ttu-id="0877b-154">Description</span><span class="sxs-lookup"><span data-stu-id="0877b-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0877b-155">espacedenoms_fournisseur</span><span class="sxs-lookup"><span data-stu-id="0877b-155">providerNamespace</span></span> |<span data-ttu-id="0877b-156">Oui</span><span class="sxs-lookup"><span data-stu-id="0877b-156">Yes</span></span> |<span data-ttu-id="0877b-157">string</span><span class="sxs-lookup"><span data-stu-id="0877b-157">string</span></span> |<span data-ttu-id="0877b-158">Espace de noms du fournisseur.</span><span class="sxs-lookup"><span data-stu-id="0877b-158">Namespace of the provider</span></span> |
| <span data-ttu-id="0877b-159">resourceType</span><span class="sxs-lookup"><span data-stu-id="0877b-159">resourceType</span></span> |<span data-ttu-id="0877b-160">Non</span><span class="sxs-lookup"><span data-stu-id="0877b-160">No</span></span> |<span data-ttu-id="0877b-161">string</span><span class="sxs-lookup"><span data-stu-id="0877b-161">string</span></span> |<span data-ttu-id="0877b-162">Type de ressource dans l'espace de noms spécifié.</span><span class="sxs-lookup"><span data-stu-id="0877b-162">The type of resource within the specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="0877b-163">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="0877b-163">Return value</span></span>

<span data-ttu-id="0877b-164">Chaque type pris en charge est renvoyé au format suivant :</span><span class="sxs-lookup"><span data-stu-id="0877b-164">Each supported type is returned in the following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="0877b-165">Le classement du tableau des valeurs renvoyées n’est pas garanti.</span><span class="sxs-lookup"><span data-stu-id="0877b-165">Array ordering of the returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="0877b-166">Exemple</span><span class="sxs-lookup"><span data-stu-id="0877b-166">Example</span></span>

<span data-ttu-id="0877b-167">L'exemple suivant montre comment utiliser la fonction provider :</span><span class="sxs-lookup"><span data-stu-id="0877b-167">The following example shows how to use the provider function:</span></span>

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

<span data-ttu-id="0877b-168">L’exemple précédent renvoie un objet dans le format suivant :</span><span class="sxs-lookup"><span data-stu-id="0877b-168">The preceding example returns an object in the following format:</span></span>

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

## <a name="reference"></a><span data-ttu-id="0877b-169">reference</span><span class="sxs-lookup"><span data-stu-id="0877b-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="0877b-170">Renvoie un objet représentant l’état d’exécution d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="0877b-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="0877b-171">Paramètres</span><span class="sxs-lookup"><span data-stu-id="0877b-171">Parameters</span></span>

| <span data-ttu-id="0877b-172">Paramètre</span><span class="sxs-lookup"><span data-stu-id="0877b-172">Parameter</span></span> | <span data-ttu-id="0877b-173">Requis</span><span class="sxs-lookup"><span data-stu-id="0877b-173">Required</span></span> | <span data-ttu-id="0877b-174">Type</span><span class="sxs-lookup"><span data-stu-id="0877b-174">Type</span></span> | <span data-ttu-id="0877b-175">Description</span><span class="sxs-lookup"><span data-stu-id="0877b-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0877b-176">nom_ressource ou identificateur_ressource</span><span class="sxs-lookup"><span data-stu-id="0877b-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="0877b-177">Oui</span><span class="sxs-lookup"><span data-stu-id="0877b-177">Yes</span></span> |<span data-ttu-id="0877b-178">string</span><span class="sxs-lookup"><span data-stu-id="0877b-178">string</span></span> |<span data-ttu-id="0877b-179">Nom ou identificateur unique d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="0877b-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="0877b-180">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0877b-180">apiVersion</span></span> |<span data-ttu-id="0877b-181">Non</span><span class="sxs-lookup"><span data-stu-id="0877b-181">No</span></span> |<span data-ttu-id="0877b-182">string</span><span class="sxs-lookup"><span data-stu-id="0877b-182">string</span></span> |<span data-ttu-id="0877b-183">Version d’API de la ressource spécifiée.</span><span class="sxs-lookup"><span data-stu-id="0877b-183">API version of the specified resource.</span></span> <span data-ttu-id="0877b-184">Incluez ce paramètre lorsque la ressource n’est pas approvisionnée dans le même modèle.</span><span class="sxs-lookup"><span data-stu-id="0877b-184">Include this parameter when the resource is not provisioned within same template.</span></span> <span data-ttu-id="0877b-185">En règle générale, au format, **aaaa-mm-jj**.</span><span class="sxs-lookup"><span data-stu-id="0877b-185">Typically, in the format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="0877b-186">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="0877b-186">Return value</span></span>

<span data-ttu-id="0877b-187">Chaque type de ressource retourne des propriétés différentes pour la fonction de référence.</span><span class="sxs-lookup"><span data-stu-id="0877b-187">Every resource type returns different properties for the reference function.</span></span> <span data-ttu-id="0877b-188">La fonction ne retourne pas un format prédéfini unique.</span><span class="sxs-lookup"><span data-stu-id="0877b-188">The function does not return a single, predefined format.</span></span> <span data-ttu-id="0877b-189">Pour afficher les propriétés d’un type de ressource, renvoyez l’objet dans la section des sorties comme indiqué dans l’exemple.</span><span class="sxs-lookup"><span data-stu-id="0877b-189">To see the properties for a resource type, return the object in the outputs section as shown in the example.</span></span>

### <a name="remarks"></a><span data-ttu-id="0877b-190">Remarques</span><span class="sxs-lookup"><span data-stu-id="0877b-190">Remarks</span></span>

<span data-ttu-id="0877b-191">La fonction reference dérive sa valeur d'un état d'exécution, et ne peut donc pas être utilisée dans la section variables.</span><span class="sxs-lookup"><span data-stu-id="0877b-191">The reference function derives its value from a runtime state, and therefore cannot be used in the variables section.</span></span> <span data-ttu-id="0877b-192">Elle peut être utilisée dans la section outputs d'un modèle.</span><span class="sxs-lookup"><span data-stu-id="0877b-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="0877b-193">En utilisant la fonction « reference », vous déclarez de manière implicite qu’une ressource dépend d’une autre ressource si la ressource référencée est configurée dans le même modèle.</span><span class="sxs-lookup"><span data-stu-id="0877b-193">By using the reference function, you implicitly declare that one resource depends on another resource if the referenced resource is provisioned within same template.</span></span> <span data-ttu-id="0877b-194">Vous n’avez pas besoin d’utiliser également la propriété dependsOn.</span><span class="sxs-lookup"><span data-stu-id="0877b-194">You do not need to also use the dependsOn property.</span></span> <span data-ttu-id="0877b-195">La fonction n’est pas évaluée tant que le déploiement de la ressource référencée n’est pas terminé.</span><span class="sxs-lookup"><span data-stu-id="0877b-195">The function is not evaluated until the referenced resource has completed deployment.</span></span>

<span data-ttu-id="0877b-196">Pour afficher les noms et les valeurs des propriétés pour un type de ressource donné, créez un modèle qui retourne l’objet dans la section outputs.</span><span class="sxs-lookup"><span data-stu-id="0877b-196">To see the property names and values for a resource type, create a template that returns the object in the outputs section.</span></span> <span data-ttu-id="0877b-197">Si vous disposez déjà d’une ressource de ce type, votre modèle retourne l’objet sans déployer de nouvelles ressources.</span><span class="sxs-lookup"><span data-stu-id="0877b-197">If you have an existing resource of that type, your template returns the object without deploying any new resources.</span></span> 

<span data-ttu-id="0877b-198">En règle générale, vous utilisez la fonction de **référence** pour renvoyer une valeur particulière d’un objet, telle que l’URI du point de terminaison d’objet blob ou le nom de domaine complet.</span><span class="sxs-lookup"><span data-stu-id="0877b-198">Typically, you use the **reference** function to return a particular value from an object, such as the blob endpoint URI or fully qualified domain name.</span></span>

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

### <a name="example"></a><span data-ttu-id="0877b-199">Exemple</span><span class="sxs-lookup"><span data-stu-id="0877b-199">Example</span></span>

<span data-ttu-id="0877b-200">Pour déployer et faire référence à la ressource dans le même modèle, utilisez :</span><span class="sxs-lookup"><span data-stu-id="0877b-200">To deploy and reference the resource in the same template, use:</span></span>

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

<span data-ttu-id="0877b-201">L’exemple précédent renvoie un objet dans le format suivant :</span><span class="sxs-lookup"><span data-stu-id="0877b-201">The preceding example returns an object in the following format:</span></span>

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

<span data-ttu-id="0877b-202">L’exemple ci-après référence un compte de stockage déployé dans un modèle différent.</span><span class="sxs-lookup"><span data-stu-id="0877b-202">The following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="0877b-203">Le compte de stockage existe déjà dans le même groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0877b-203">The storage account already exists within the same resource group.</span></span>

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

## <a name="resourcegroup"></a><span data-ttu-id="0877b-204">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="0877b-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="0877b-205">Renvoie un objet qui représente le groupe de ressources actuel.</span><span class="sxs-lookup"><span data-stu-id="0877b-205">Returns an object that represents the current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="0877b-206">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="0877b-206">Return value</span></span>

<span data-ttu-id="0877b-207">L’objet renvoyé présente le format suivant :</span><span class="sxs-lookup"><span data-stu-id="0877b-207">The returned object is in the following format:</span></span>

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

### <a name="remarks"></a><span data-ttu-id="0877b-208">Remarques</span><span class="sxs-lookup"><span data-stu-id="0877b-208">Remarks</span></span>

<span data-ttu-id="0877b-209">Une utilisation courante de la fonction resourceGroup consiste à créer des ressources dans le même emplacement que le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0877b-209">A common use of the resourceGroup function is to create resources in the same location as the resource group.</span></span> <span data-ttu-id="0877b-210">L'exemple suivant utilise l'emplacement du groupe de ressources pour affecter l'emplacement d'un site web.</span><span class="sxs-lookup"><span data-stu-id="0877b-210">The following example uses the resource group location to assign the location for a web site.</span></span>

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

### <a name="example"></a><span data-ttu-id="0877b-211">Exemple</span><span class="sxs-lookup"><span data-stu-id="0877b-211">Example</span></span>

<span data-ttu-id="0877b-212">Le modèle suivant retourne les propriétés du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0877b-212">The following template returns the properties of the resource group.</span></span>

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

<span data-ttu-id="0877b-213">L’exemple précédent renvoie un objet dans le format suivant :</span><span class="sxs-lookup"><span data-stu-id="0877b-213">The preceding example returns an object in the following format:</span></span>

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

## <a name="resourceid"></a><span data-ttu-id="0877b-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="0877b-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="0877b-215">Retourne l'identificateur unique d'une ressource.</span><span class="sxs-lookup"><span data-stu-id="0877b-215">Returns the unique identifier of a resource.</span></span> <span data-ttu-id="0877b-216">Vous utilisez cette fonction lorsque le nom de la ressource est ambigu ou non configuré dans le même modèle.</span><span class="sxs-lookup"><span data-stu-id="0877b-216">You use this function when the resource name is ambiguous or not provisioned within the same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="0877b-217">Paramètres</span><span class="sxs-lookup"><span data-stu-id="0877b-217">Parameters</span></span>

| <span data-ttu-id="0877b-218">Paramètre</span><span class="sxs-lookup"><span data-stu-id="0877b-218">Parameter</span></span> | <span data-ttu-id="0877b-219">Requis</span><span class="sxs-lookup"><span data-stu-id="0877b-219">Required</span></span> | <span data-ttu-id="0877b-220">Type</span><span class="sxs-lookup"><span data-stu-id="0877b-220">Type</span></span> | <span data-ttu-id="0877b-221">Description</span><span class="sxs-lookup"><span data-stu-id="0877b-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0877b-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="0877b-222">subscriptionId</span></span> |<span data-ttu-id="0877b-223">Non</span><span class="sxs-lookup"><span data-stu-id="0877b-223">No</span></span> |<span data-ttu-id="0877b-224">string (au format GUID)</span><span class="sxs-lookup"><span data-stu-id="0877b-224">string (In GUID format)</span></span> |<span data-ttu-id="0877b-225">La valeur par défaut est l’abonnement actuel.</span><span class="sxs-lookup"><span data-stu-id="0877b-225">Default value is the current subscription.</span></span> <span data-ttu-id="0877b-226">Spécifiez cette valeur lorsque vous devez récupérer une ressource se trouvant dans un autre abonnement.</span><span class="sxs-lookup"><span data-stu-id="0877b-226">Specify this value when you need to retrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="0877b-227">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="0877b-227">resourceGroupName</span></span> |<span data-ttu-id="0877b-228">Non</span><span class="sxs-lookup"><span data-stu-id="0877b-228">No</span></span> |<span data-ttu-id="0877b-229">string</span><span class="sxs-lookup"><span data-stu-id="0877b-229">string</span></span> |<span data-ttu-id="0877b-230">La valeur par défaut est le groupe de ressources actuel.</span><span class="sxs-lookup"><span data-stu-id="0877b-230">Default value is current resource group.</span></span> <span data-ttu-id="0877b-231">Spécifiez cette valeur lorsque vous devez récupérer une ressource se trouvant dans un autre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0877b-231">Specify this value when you need to retrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="0877b-232">resourceType</span><span class="sxs-lookup"><span data-stu-id="0877b-232">resourceType</span></span> |<span data-ttu-id="0877b-233">Oui</span><span class="sxs-lookup"><span data-stu-id="0877b-233">Yes</span></span> |<span data-ttu-id="0877b-234">string</span><span class="sxs-lookup"><span data-stu-id="0877b-234">string</span></span> |<span data-ttu-id="0877b-235">Type de ressource, y compris l'espace de noms du fournisseur de ressources.</span><span class="sxs-lookup"><span data-stu-id="0877b-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="0877b-236">nom_ressource1</span><span class="sxs-lookup"><span data-stu-id="0877b-236">resourceName1</span></span> |<span data-ttu-id="0877b-237">Oui</span><span class="sxs-lookup"><span data-stu-id="0877b-237">Yes</span></span> |<span data-ttu-id="0877b-238">string</span><span class="sxs-lookup"><span data-stu-id="0877b-238">string</span></span> |<span data-ttu-id="0877b-239">Nom de la ressource.</span><span class="sxs-lookup"><span data-stu-id="0877b-239">Name of resource.</span></span> |
| <span data-ttu-id="0877b-240">nom_ressource2</span><span class="sxs-lookup"><span data-stu-id="0877b-240">resourceName2</span></span> |<span data-ttu-id="0877b-241">Non</span><span class="sxs-lookup"><span data-stu-id="0877b-241">No</span></span> |<span data-ttu-id="0877b-242">string</span><span class="sxs-lookup"><span data-stu-id="0877b-242">string</span></span> |<span data-ttu-id="0877b-243">Segment de nom de ressource suivant si la ressource est imbriquée.</span><span class="sxs-lookup"><span data-stu-id="0877b-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="0877b-244">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="0877b-244">Return value</span></span>

<span data-ttu-id="0877b-245">L'identificateur est retourné au format suivant :</span><span class="sxs-lookup"><span data-stu-id="0877b-245">The identifier is returned in the following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="0877b-246">Remarques</span><span class="sxs-lookup"><span data-stu-id="0877b-246">Remarks</span></span>

<span data-ttu-id="0877b-247">Les valeurs de paramètre spécifiées varient selon que la ressource se trouve ou non dans le même abonnement et le même groupe de ressources que le déploiement actuel.</span><span class="sxs-lookup"><span data-stu-id="0877b-247">The parameter values you specify depend on whether the resource is in the same subscription and resource group as the current deployment.</span></span>

<span data-ttu-id="0877b-248">Pour obtenir l’ID de ressource d’un compte de stockage se trouvant dans le même abonnement et le même groupe de ressources, utilisez :</span><span class="sxs-lookup"><span data-stu-id="0877b-248">To get the resource ID for a storage account in the same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="0877b-249">Pour obtenir l’ID de ressource d’un compte de stockage se trouvant dans le même abonnement mais dans un groupe de ressources différent, utilisez :</span><span class="sxs-lookup"><span data-stu-id="0877b-249">To get the resource ID for a storage account in the same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="0877b-250">Pour obtenir l’ID de ressource d’un compte de stockage se trouvant dans un abonnement et un groupe de ressources différents, utilisez :</span><span class="sxs-lookup"><span data-stu-id="0877b-250">To get the resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="0877b-251">Pour obtenir l’ID de ressource d’une base de données se trouvant dans un groupe de ressources différent, utilisez :</span><span class="sxs-lookup"><span data-stu-id="0877b-251">To get the resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="0877b-252">Souvent, vous devez utiliser cette fonction lorsque vous utilisez un compte de stockage ou un réseau virtuel se trouvant dans un autre groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0877b-252">Often, you need to use this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="0877b-253">L'exemple suivant montre comment une ressource d'un groupe de ressources externe peut être facilement utilisée :</span><span class="sxs-lookup"><span data-stu-id="0877b-253">The following example shows how a resource from an external resource group can easily be used:</span></span>

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

### <a name="example"></a><span data-ttu-id="0877b-254">Exemple</span><span class="sxs-lookup"><span data-stu-id="0877b-254">Example</span></span>

<span data-ttu-id="0877b-255">L’exemple suivant retourne l’ID de ressource pour un compte de stockage dans le groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="0877b-255">The following example returns the resource ID for a storage account in the resource group:</span></span>

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

<span data-ttu-id="0877b-256">La sortie de l’exemple précédent avec les valeurs par défaut se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="0877b-256">The output from the preceding example with the default values is:</span></span>

| <span data-ttu-id="0877b-257">Nom</span><span class="sxs-lookup"><span data-stu-id="0877b-257">Name</span></span> | <span data-ttu-id="0877b-258">Type</span><span class="sxs-lookup"><span data-stu-id="0877b-258">Type</span></span> | <span data-ttu-id="0877b-259">Valeur</span><span class="sxs-lookup"><span data-stu-id="0877b-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="0877b-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="0877b-260">sameRGOutput</span></span> | <span data-ttu-id="0877b-261">String</span><span class="sxs-lookup"><span data-stu-id="0877b-261">String</span></span> | <span data-ttu-id="0877b-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="0877b-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="0877b-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="0877b-263">differentRGOutput</span></span> | <span data-ttu-id="0877b-264">String</span><span class="sxs-lookup"><span data-stu-id="0877b-264">String</span></span> | <span data-ttu-id="0877b-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="0877b-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="0877b-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="0877b-266">differentSubOutput</span></span> | <span data-ttu-id="0877b-267">String</span><span class="sxs-lookup"><span data-stu-id="0877b-267">String</span></span> | <span data-ttu-id="0877b-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="0877b-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="0877b-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="0877b-269">nestedResourceOutput</span></span> | <span data-ttu-id="0877b-270">String</span><span class="sxs-lookup"><span data-stu-id="0877b-270">String</span></span> | <span data-ttu-id="0877b-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="0877b-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="0877b-272">abonnement</span><span class="sxs-lookup"><span data-stu-id="0877b-272">subscription</span></span>
`subscription()`

<span data-ttu-id="0877b-273">Retourne des détails concernant l’abonnement pour le déploiement actuel.</span><span class="sxs-lookup"><span data-stu-id="0877b-273">Returns details about the subscription for the current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="0877b-274">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="0877b-274">Return value</span></span>

<span data-ttu-id="0877b-275">La fonction retourne les informations au format suivant :</span><span class="sxs-lookup"><span data-stu-id="0877b-275">The function returns the following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="0877b-276">Exemple</span><span class="sxs-lookup"><span data-stu-id="0877b-276">Example</span></span>

<span data-ttu-id="0877b-277">L’exemple suivant montre la fonction subscription appelée dans la section outputs.</span><span class="sxs-lookup"><span data-stu-id="0877b-277">The following example shows the subscription function called in the outputs section.</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="0877b-278">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0877b-278">Next steps</span></span>
* <span data-ttu-id="0877b-279">Pour obtenir une description des sections d’un modèle Azure Resource Manager, consultez [Création de modèles Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0877b-279">For a description of the sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="0877b-280">Pour fusionner plusieurs modèles, consultez [Utilisation de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0877b-280">To merge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="0877b-281">Pour itérer un nombre de fois spécifié lors de la création d'un type de ressource, consultez [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="0877b-281">To iterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="0877b-282">Pour savoir comment déployer le modèle que vous avez créé, consultez [Déploiement d’une application avec un modèle Azure Resource Manager](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="0877b-282">To see how to deploy the template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

