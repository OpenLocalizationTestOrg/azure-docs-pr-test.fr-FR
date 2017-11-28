---
title: "pratiques aaaBest pour la création de modèles Resource Manager | Documents Microsoft"
description: "Instructions pour simplifier vos modèles Azure Resource Manager."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 31b10deb-0183-47ce-a5ba-6d0ff2ae8ab3
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: tomfitz
ms.openlocfilehash: ec9bbe218c4f2c6a92ca44b5e9c9c71029e22151
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-creating-azure-resource-manager-templates"></a><span data-ttu-id="9e67c-103">Bonnes pratiques relatives à la création de modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9e67c-103">Best practices for creating Azure Resource Manager templates</span></span>
<span data-ttu-id="9e67c-104">Ces instructions peuvent vous aider à créer des modèles Azure Resource Manager sont toouse simple et fiable.</span><span class="sxs-lookup"><span data-stu-id="9e67c-104">These guidelines can help you create Azure Resource Manager templates that are reliable and easy toouse.</span></span> <span data-ttu-id="9e67c-105">instructions de Hello sont uniquement des suggestions.</span><span class="sxs-lookup"><span data-stu-id="9e67c-105">hello guidelines are only suggestions.</span></span> <span data-ttu-id="9e67c-106">Il ne s’agit pas de spécifications requises, sauf indication contraire.</span><span class="sxs-lookup"><span data-stu-id="9e67c-106">They are not requirements, except where noted.</span></span> <span data-ttu-id="9e67c-107">Votre scénario peut nécessiter une variante de l’un des hello suivant des approches ou exemples.</span><span class="sxs-lookup"><span data-stu-id="9e67c-107">Your scenario might require a variation of one of hello following approaches or examples.</span></span>

## <a name="resource-names"></a><span data-ttu-id="9e67c-108">Noms de ressource</span><span class="sxs-lookup"><span data-stu-id="9e67c-108">Resource names</span></span>
<span data-ttu-id="9e67c-109">Il existe généralement trois types de noms de ressource avec lesquels vous travaillez dans Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="9e67c-109">Generally, you work with three types of resource names in Resource Manager:</span></span>

* <span data-ttu-id="9e67c-110">des noms de ressource qui doivent être uniques ;</span><span class="sxs-lookup"><span data-stu-id="9e67c-110">Resource names that must be unique.</span></span>
* <span data-ttu-id="9e67c-111">Les noms de ressources qui ne sont pas requis toobe unique, mais que vous choisissez un nom qui peut vous aider à identifier une ressource basée sur le contexte de tooprovide.</span><span class="sxs-lookup"><span data-stu-id="9e67c-111">Resource names that are not required toobe unique, but you choose tooprovide a name that can help you identify a resource based on context.</span></span>
* <span data-ttu-id="9e67c-112">des noms de ressources qui peuvent être génériques.</span><span class="sxs-lookup"><span data-stu-id="9e67c-112">Resource names that can be generic.</span></span>

 <span data-ttu-id="9e67c-113">Pour plus d’informations sur les restrictions de noms de ressource, consultez [Conventions d’affectation de noms recommandées pour les ressources Azure](../guidance/guidance-naming-conventions.md).</span><span class="sxs-lookup"><span data-stu-id="9e67c-113">For information about resource name restrictions, see [Recommended naming conventions for Azure resources](../guidance/guidance-naming-conventions.md).</span></span>

### <a name="unique-resource-names"></a><span data-ttu-id="9e67c-114">Noms de ressource uniques</span><span class="sxs-lookup"><span data-stu-id="9e67c-114">Unique resource names</span></span>
<span data-ttu-id="9e67c-115">Vous devez fournir un nom de ressource unique pour tout type de ressource disposant d’un point de terminaison d’accès aux données.</span><span class="sxs-lookup"><span data-stu-id="9e67c-115">You must provide a unique resource name for any resource type that has a data access endpoint.</span></span> <span data-ttu-id="9e67c-116">Certains types de ressource courants nécessitent un nom unique, notamment :</span><span class="sxs-lookup"><span data-stu-id="9e67c-116">Some common resource types that require a unique name include:</span></span>

* <span data-ttu-id="9e67c-117">Azure Storage<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="9e67c-117">Azure Storage<sup>1</sup></span></span> 
* <span data-ttu-id="9e67c-118">Fonctionnalité Web Apps d’Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9e67c-118">Web Apps feature of Azure App Service</span></span>
* <span data-ttu-id="9e67c-119">SQL Server</span><span class="sxs-lookup"><span data-stu-id="9e67c-119">SQL Server</span></span>
* <span data-ttu-id="9e67c-120">coffre de clés Azure</span><span class="sxs-lookup"><span data-stu-id="9e67c-120">Azure Key Vault</span></span>
* <span data-ttu-id="9e67c-121">Cache Redis Azure</span><span class="sxs-lookup"><span data-stu-id="9e67c-121">Azure Redis Cache</span></span>
* <span data-ttu-id="9e67c-122">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="9e67c-122">Azure Batch</span></span>
* <span data-ttu-id="9e67c-123">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="9e67c-123">Azure Traffic Manager</span></span>
* <span data-ttu-id="9e67c-124">Recherche Azure</span><span class="sxs-lookup"><span data-stu-id="9e67c-124">Azure Search</span></span>
* <span data-ttu-id="9e67c-125">Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e67c-125">Azure HDInsight</span></span>

<span data-ttu-id="9e67c-126"><sup>1</sup> Les noms de compte de stockage doivent être en minuscules, comporter 24 caractères au maximum et ne pas comprendre de traits d’union.</span><span class="sxs-lookup"><span data-stu-id="9e67c-126"><sup>1</sup> Storage account names also must be lowercase, 24 characters or less, and not have any hyphens.</span></span>

<span data-ttu-id="9e67c-127">Si vous fournissez un paramètre pour un nom de ressource, vous devez fournir un nom unique lorsque vous déployez des ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="9e67c-127">If you provide a parameter for a resource name, you must provide a unique name when you deploy hello resource.</span></span> <span data-ttu-id="9e67c-128">Si vous le souhaitez, vous pouvez créer une variable qui utilise hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) toogenerate un nom de fonction.</span><span class="sxs-lookup"><span data-stu-id="9e67c-128">Optionally, you can create a variable that uses hello [uniqueString()](resource-group-template-functions-string.md#uniquestring) function toogenerate a name.</span></span> 

<span data-ttu-id="9e67c-129">Vous pourrez également voulez tooadd un préfixe ou suffixe toohello **uniqueString** résultat.</span><span class="sxs-lookup"><span data-stu-id="9e67c-129">You also might want tooadd a prefix or suffix toohello **uniqueString** result.</span></span> <span data-ttu-id="9e67c-130">Nom unique des hello modification peut vous aider plus facilement identifier le type de ressource hello du nom de hello.</span><span class="sxs-lookup"><span data-stu-id="9e67c-130">Modifying hello unique name can help you more easily identify hello resource type from hello name.</span></span> <span data-ttu-id="9e67c-131">Par exemple, vous pouvez générer un nom unique pour un compte de stockage à l’aide de hello suivant variable :</span><span class="sxs-lookup"><span data-stu-id="9e67c-131">For example, you can generate a unique name for a storage account by using hello following variable:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniqueString(resourceGroup().id),'storage')]"
}
```

### <a name="resource-names-for-identification"></a><span data-ttu-id="9e67c-132">Noms de ressource pour l’identification</span><span class="sxs-lookup"><span data-stu-id="9e67c-132">Resource names for identification</span></span>
<span data-ttu-id="9e67c-133">Certains types de ressources vous pourriez tooname, mais leurs noms n’ont pas toobe unique.</span><span class="sxs-lookup"><span data-stu-id="9e67c-133">Some resource types you might want tooname, but their names do not have toobe unique.</span></span> <span data-ttu-id="9e67c-134">Pour ces types de ressources, vous pouvez fournir un nom qui identifie le contexte de la ressource hello et type de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="9e67c-134">For these resource types, you can provide a name that identifies both hello resource context and hello resource type.</span></span> <span data-ttu-id="9e67c-135">Fournissez un nom descriptif qui vous permet d’identifier les ressources hello dans une liste de ressources.</span><span class="sxs-lookup"><span data-stu-id="9e67c-135">Provide a descriptive name that helps you identify hello resource in a list of resources.</span></span> <span data-ttu-id="9e67c-136">Si vous avez besoin d’un autre nom de ressource de différents déploiements de toouse, vous pouvez utiliser un paramètre pour le nom de hello :</span><span class="sxs-lookup"><span data-stu-id="9e67c-136">If you need toouse a different resource name for different deployments, you can use a parameter for hello name:</span></span>

```json
"parameters": {
    "vmName": { 
        "type": "string",
        "defaultValue": "demoLinuxVM",
        "metadata": {
            "description": "hello name of hello VM toocreate."
        }
    }
}
```

<span data-ttu-id="9e67c-137">Si vous n’avez pas besoin de toopass dans un nom de durant le déploiement, vous pouvez utiliser une variable :</span><span class="sxs-lookup"><span data-stu-id="9e67c-137">If you do not need toopass in a name during deployment, you can use a variable:</span></span> 

```json
"variables": {
    "vmName": "demoLinuxVM"
}
```

<span data-ttu-id="9e67c-138">Vous pouvez également utiliser une valeur codée en dur :</span><span class="sxs-lookup"><span data-stu-id="9e67c-138">You also can use a hard-coded value:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines",
  "name": "demoLinuxVM",
  ...
}
```

### <a name="generic-resource-names"></a><span data-ttu-id="9e67c-139">Noms de ressource génériques</span><span class="sxs-lookup"><span data-stu-id="9e67c-139">Generic resource names</span></span>
<span data-ttu-id="9e67c-140">Pour les types de ressources auxquels vous accédez principalement via une autre ressource, vous pouvez utiliser un nom générique qui est codé en dur dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="9e67c-140">For resource types that you mostly access through a different resource, you can use a generic name that is hard-coded in hello template.</span></span> <span data-ttu-id="9e67c-141">Par exemple, vous pouvez définir un nom générique standard pour les règles de pare-feu sur un serveur SQL :</span><span class="sxs-lookup"><span data-stu-id="9e67c-141">For example, you can set a standard, generic name for firewall rules on a SQL server:</span></span>

```json
{
    "type": "firewallrules",
    "name": "AllowAllWindowsAzureIps",
    ...
}
```

## <a name="parameters"></a><span data-ttu-id="9e67c-142">Paramètres</span><span class="sxs-lookup"><span data-stu-id="9e67c-142">Parameters</span></span>
<span data-ttu-id="9e67c-143">Hello informations suivantes peuvent être utiles lorsque vous travaillez avec des paramètres :</span><span class="sxs-lookup"><span data-stu-id="9e67c-143">hello following information can be helpful when you work with parameters:</span></span>

* <span data-ttu-id="9e67c-144">Réduisez l’utilisation des paramètres.</span><span class="sxs-lookup"><span data-stu-id="9e67c-144">Minimize your use of parameters.</span></span> <span data-ttu-id="9e67c-145">Si possible, utilisez une variable ou une valeur littérale.</span><span class="sxs-lookup"><span data-stu-id="9e67c-145">Whenever possible, use a variable or a literal value.</span></span> <span data-ttu-id="9e67c-146">Utilisez des paramètres uniquement pour les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="9e67c-146">Use parameters only for these scenarios:</span></span>
   
   * <span data-ttu-id="9e67c-147">Paramètres que vous souhaitez toouse les variations de selon tooenvironment (référence (SKU), taille, capacité).</span><span class="sxs-lookup"><span data-stu-id="9e67c-147">Settings that you want toouse variations of according tooenvironment (SKU, size, capacity).</span></span>
   * <span data-ttu-id="9e67c-148">Noms de ressources que vous souhaitez toospecify pour faciliter l’identification.</span><span class="sxs-lookup"><span data-stu-id="9e67c-148">Resource names that you want toospecify for easy identification.</span></span>
   * <span data-ttu-id="9e67c-149">Valeurs que vous utilisez fréquemment toocomplete autres tâches (par exemple, un nom d’utilisateur admin).</span><span class="sxs-lookup"><span data-stu-id="9e67c-149">Values that you use frequently toocomplete other tasks (such as an admin user name).</span></span>
   * <span data-ttu-id="9e67c-150">les clés secrètes (notamment les mots de passe) ;</span><span class="sxs-lookup"><span data-stu-id="9e67c-150">Secrets (such as passwords).</span></span>
   * <span data-ttu-id="9e67c-151">nombre de Hello ou tableau de valeurs toouse lorsque vous créez plusieurs instances d’un type de ressource.</span><span class="sxs-lookup"><span data-stu-id="9e67c-151">hello number or array of values toouse when you create multiple instances of a resource type.</span></span>
* <span data-ttu-id="9e67c-152">Utilisez la casse mixte pour les noms de paramètre.</span><span class="sxs-lookup"><span data-stu-id="9e67c-152">Use camel case for parameter names.</span></span>
* <span data-ttu-id="9e67c-153">Fournissez une description de chaque paramètre dans les métadonnées de hello :</span><span class="sxs-lookup"><span data-stu-id="9e67c-153">Provide a description of every parameter in hello metadata:</span></span>

   ```json
   "parameters": {
       "storageAccountType": {
           "type": "string",
           "metadata": {
               "description": "hello type of hello new storage account created toostore hello VM disks."
           }
       }
   }
   ```

* <span data-ttu-id="9e67c-154">Définissez des valeurs par défaut pour les paramètres (à l’exception des mots de passe et des clés SSH) :</span><span class="sxs-lookup"><span data-stu-id="9e67c-154">Define default values for parameters (except for passwords and SSH keys):</span></span>
   
   ```json
   "parameters": {
        "storageAccountType": {
            "type": "string",
            "defaultValue": "Standard_GRS",
            "metadata": {
                "description": "hello type of hello new storage account created toostore hello VM disks."
            }
        }
   }
   ```

* <span data-ttu-id="9e67c-155">Utilisez **SecureString** pour tous les mots de passe et les clés secrètes :</span><span class="sxs-lookup"><span data-stu-id="9e67c-155">Use **SecureString** for all passwords and secrets:</span></span> 
   
   ```json
   "parameters": {
       "secretValue": {
           "type": "securestring",
           "metadata": {
               "description": "hello value of hello secret toostore in hello vault."
           }
       }
   }
   ```

* <span data-ttu-id="9e67c-156">Si possible, n’utilisez pas un emplacement de toospecify de paramètre.</span><span class="sxs-lookup"><span data-stu-id="9e67c-156">Whenever possible, don't use a parameter toospecify location.</span></span> <span data-ttu-id="9e67c-157">Au lieu de cela, utilisez hello **emplacement** propriété hello du groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="9e67c-157">Instead, use hello **location** property of hello resource group.</span></span> <span data-ttu-id="9e67c-158">À l’aide de hello **resourceGroup () .location** expression pour toutes vos ressources, les ressources dans le modèle de hello sont déployés dans hello même emplacement que le groupe de ressources hello :</span><span class="sxs-lookup"><span data-stu-id="9e67c-158">By using hello **resourceGroup().location** expression for all your resources, resources in hello template are deployed in hello same location as hello resource group:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         ...
     }
   ]
   ```
   
   <span data-ttu-id="9e67c-159">Si un type de ressource est prise en charge uniquement un nombre limité d’emplacements, vous pourriez toospecify un emplacement valide directement dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="9e67c-159">If a resource type is supported in only a limited number of locations, you might want toospecify a valid location directly in hello template.</span></span> <span data-ttu-id="9e67c-160">Si vous devez utiliser un **emplacement** paramètre, partager cette valeur de paramètre autant que possible avec les ressources qui sont susceptibles de toobe Bonjour même emplacement.</span><span class="sxs-lookup"><span data-stu-id="9e67c-160">If you must use a **location** parameter, share that parameter value as much as possible with resources that are likely toobe in hello same location.</span></span> <span data-ttu-id="9e67c-161">Cela réduit le nombre de hello de fois où les utilisateurs sont invités à tooprovide informations d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="9e67c-161">This minimizes hello number of times users are asked tooprovide location information.</span></span>
* <span data-ttu-id="9e67c-162">Évitez d’utiliser un paramètre ou une variable pour la version de l’API hello pour un type de ressource.</span><span class="sxs-lookup"><span data-stu-id="9e67c-162">Avoid using a parameter or variable for hello API version for a resource type.</span></span> <span data-ttu-id="9e67c-163">Les propriétés de ressource et les valeurs peuvent varier selon le numéro de version.</span><span class="sxs-lookup"><span data-stu-id="9e67c-163">Resource properties and values can vary by version number.</span></span> <span data-ttu-id="9e67c-164">IntelliSense dans un éditeur de code ne peut pas déterminer les schéma correct hello lorsque la valeur de version de l’API hello tooa paramètre ou une variable.</span><span class="sxs-lookup"><span data-stu-id="9e67c-164">IntelliSense in a code editor cannot determine hello correct schema when hello API version is set tooa parameter or variable.</span></span> <span data-ttu-id="9e67c-165">Au lieu de cela, coder en dur hello version d’API dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="9e67c-165">Instead, hard-code hello API version in hello template.</span></span>

## <a name="variables"></a><span data-ttu-id="9e67c-166">variables</span><span class="sxs-lookup"><span data-stu-id="9e67c-166">Variables</span></span>
<span data-ttu-id="9e67c-167">Hello informations suivantes peuvent être utiles lorsque vous travaillez avec des variables :</span><span class="sxs-lookup"><span data-stu-id="9e67c-167">hello following information can be helpful when you work with variables:</span></span>

* <span data-ttu-id="9e67c-168">Utiliser des variables pour les valeurs que vous devez toouse plusieurs fois dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="9e67c-168">Use variables for values that you need toouse more than once in a template.</span></span> <span data-ttu-id="9e67c-169">Si une valeur est utilisée qu’une seule fois, une valeur codée en dur rend votre tooread plus facile de modèle.</span><span class="sxs-lookup"><span data-stu-id="9e67c-169">If a value is used only once, a hard-coded value makes your template easier tooread.</span></span>
* <span data-ttu-id="9e67c-170">Vous ne pouvez pas utiliser hello [référence](resource-group-template-functions-resource.md#reference) fonction Bonjour **variables** section du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="9e67c-170">You cannot use hello [reference](resource-group-template-functions-resource.md#reference) function in hello **variables** section of hello template.</span></span> <span data-ttu-id="9e67c-171">Hello **référence** fonction dérive sa valeur à partir de l’état d’exécution de la ressource hello.</span><span class="sxs-lookup"><span data-stu-id="9e67c-171">hello **reference** function derives its value from hello resource's runtime state.</span></span> <span data-ttu-id="9e67c-172">Toutefois, les variables sont résolus pendant hello initiale de l’analyse du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="9e67c-172">However, variables are resolved during hello initial parsing of hello template.</span></span> <span data-ttu-id="9e67c-173">Construire des valeurs qui doivent hello **référence** fonction directement dans hello **ressources** ou **génère** section du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="9e67c-173">Construct values that need hello **reference** function directly in hello **resources** or **outputs** section of hello template.</span></span>
* <span data-ttu-id="9e67c-174">Incluez des variables pour les noms de ressource qui doivent être uniques, comme indiqué dans [Noms de ressources](#resource-names).</span><span class="sxs-lookup"><span data-stu-id="9e67c-174">Include variables for resource names that must be unique, as described in [Resource names](#resource-names).</span></span>
* <span data-ttu-id="9e67c-175">Vous pouvez regrouper des variables dans des objets complexes.</span><span class="sxs-lookup"><span data-stu-id="9e67c-175">You can group variables into complex objects.</span></span> <span data-ttu-id="9e67c-176">Hello d’utilisation **variable.subentry** tooreference une valeur à partir d’un objet complexe de format.</span><span class="sxs-lookup"><span data-stu-id="9e67c-176">Use hello **variable.subentry** format tooreference a value from a complex object.</span></span> <span data-ttu-id="9e67c-177">Le regroupement de variables peut vous aider à effectuer le suivi des variables liées.</span><span class="sxs-lookup"><span data-stu-id="9e67c-177">Grouping variables can help you track related variables.</span></span> <span data-ttu-id="9e67c-178">Il améliore également la lisibilité du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="9e67c-178">It also improves readability of hello template.</span></span> <span data-ttu-id="9e67c-179">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="9e67c-179">Here's an example:</span></span>
   
   ```json
   "variables": {
       "storage": {
           "name": "[concat(uniqueString(resourceGroup().id),'storage')]",
           "type": "Standard_LRS"
       }
   },
   "resources": [
     {
         "type": "Microsoft.Storage/storageAccounts",
         "name": "[variables('storage').name]",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "sku": {
             "name": "[variables('storage').type]"
         },
         ...
     }
   ]
   ```
   
   > [!NOTE]
   > <span data-ttu-id="9e67c-180">Un objet complexe ne peut pas contenir une expression qui fait référence à la valeur d’un objet complexe.</span><span class="sxs-lookup"><span data-stu-id="9e67c-180">A complex object cannot contain an expression that references a value from a complex object.</span></span> <span data-ttu-id="9e67c-181">Définissez une variable distincte à cette fin.</span><span class="sxs-lookup"><span data-stu-id="9e67c-181">Define a separate variable for this purpose.</span></span>
   > 
   > 
   
     <span data-ttu-id="9e67c-182">Pour obtenir des exemples avancés de l’utilisation d’objets complexes en tant que variables, voir [Partage d’état dans les modèles Azure Resource Manager](best-practices-resource-manager-state.md).</span><span class="sxs-lookup"><span data-stu-id="9e67c-182">For advanced examples of using complex objects as variables, see [Share state in Azure Resource Manager templates](best-practices-resource-manager-state.md).</span></span>

## <a name="resources"></a><span data-ttu-id="9e67c-183">Ressources</span><span class="sxs-lookup"><span data-stu-id="9e67c-183">Resources</span></span>
<span data-ttu-id="9e67c-184">Hello informations suivantes peuvent être utiles lorsque vous travaillez avec des ressources :</span><span class="sxs-lookup"><span data-stu-id="9e67c-184">hello following information can be helpful when you work with resources:</span></span>

* <span data-ttu-id="9e67c-185">toohelp autres collaborateurs comprendre objectif hello de ressource de hello, spécifiez **commentaires** pour chaque ressource de modèle de hello :</span><span class="sxs-lookup"><span data-stu-id="9e67c-185">toohelp other contributors understand hello purpose of hello resource, specify **comments** for each resource in hello template:</span></span>
   
   ```json
   "resources": [
     {
         "name": "[variables('storageAccountName')]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "location": "[resourceGroup().location]",
         "comments": "This storage account is used toostore hello VM disks.",
         ...
     }
   ]
   ```

* <span data-ttu-id="9e67c-186">Vous pouvez utiliser des balises tooadd métadonnées tooresources.</span><span class="sxs-lookup"><span data-stu-id="9e67c-186">You can use tags tooadd metadata tooresources.</span></span> <span data-ttu-id="9e67c-187">Utiliser des informations de métadonnées tooadd sur vos ressources.</span><span class="sxs-lookup"><span data-stu-id="9e67c-187">Use metadata tooadd information about your resources.</span></span> <span data-ttu-id="9e67c-188">Par exemple, vous pouvez ajouter des métadonnées toorecord détails sur la facturation pour une ressource.</span><span class="sxs-lookup"><span data-stu-id="9e67c-188">For example, you can add metadata toorecord billing details for a resource.</span></span> <span data-ttu-id="9e67c-189">Pour plus d’informations, consultez [à l’aide des balises tooorganize vos ressources Azure](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="9e67c-189">For more information, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>
* <span data-ttu-id="9e67c-190">Si vous utilisez un *point de terminaison public* dans votre modèle (par exemple, un objet Blob d’Azure stockage public point de terminaison), *pas coder en dur* hello d’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="9e67c-190">If you use a *public endpoint* in your template (such as an Azure Blob storage public endpoint), *do not hard-code* hello namespace.</span></span> <span data-ttu-id="9e67c-191">Hello d’utilisation **référence** fonction toodynamically récupérer l’espace de noms hello.</span><span class="sxs-lookup"><span data-stu-id="9e67c-191">Use hello **reference** function toodynamically retrieve hello namespace.</span></span> <span data-ttu-id="9e67c-192">Vous pouvez utiliser cet espace de noms public environnements d’approche toodeploy hello modèle toodifferent sans modifier manuellement le point de terminaison hello dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="9e67c-192">You can use this approach toodeploy hello template toodifferent public namespace environments without manually changing hello endpoint in hello template.</span></span> <span data-ttu-id="9e67c-193">Définir hello API version toohello même version que vous utilisez pour le compte de stockage hello dans votre modèle :</span><span class="sxs-lookup"><span data-stu-id="9e67c-193">Set hello API version toohello same version that you are using for hello storage account in your template:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="9e67c-194">Si le compte de stockage hello est déployé dans hello même modèle que vous créez, vous n’avez pas besoin toospecify hello fournisseur espace de noms lorsque vous faites référence à des ressources de hello.</span><span class="sxs-lookup"><span data-stu-id="9e67c-194">If hello storage account is deployed in hello same template that you are creating, you do not need toospecify hello provider namespace when you reference hello resource.</span></span> <span data-ttu-id="9e67c-195">Il s’agit de la syntaxe de hello simplifié :</span><span class="sxs-lookup"><span data-stu-id="9e67c-195">This is hello simplified syntax:</span></span>
   
   ```json
   "osDisk": {
       "name": "osdisk",
       "vhd": {
           "uri": "[concat(reference(variables('storageAccountName'), '2016-01-01').primaryEndpoints.blob, variables('vmStorageAccountContainerName'), '/',variables('OSDiskName'),'.vhd')]"
       }
   }
   ```
   
   <span data-ttu-id="9e67c-196">Si vous avez d’autres valeurs dans votre modèle toouse configuré un espace de noms public, modifiez ces valeurs tooreflect hello même **référence** (fonction).</span><span class="sxs-lookup"><span data-stu-id="9e67c-196">If you have other values in your template that are configured toouse a public namespace, change these values tooreflect hello same **reference** function.</span></span> <span data-ttu-id="9e67c-197">Par exemple, vous pouvez définir hello **storageUri** propriété de profil de diagnostics de machine virtuelle hello :</span><span class="sxs-lookup"><span data-stu-id="9e67c-197">For example, you can set hello **storageUri** property of hello virtual machine diagnostics profile:</span></span>
   
   ```json
   "diagnosticsProfile": {
       "bootDiagnostics": {
           "enabled": "true",
           "storageUri": "[reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2016-01-01').primaryEndpoints.blob]"
       }
   }
   ```
   
   <span data-ttu-id="9e67c-198">Vous pouvez également référencer un compte de stockage existant dans un autre groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="9e67c-198">You also can reference an existing storage account that is in a different resource group:</span></span>

   ```json
   "osDisk": {
       "name": "osdisk", 
       "vhd": {
           "uri":"[concat(reference(resourceId(parameters('existingResourceGroup'), 'Microsoft.Storage/storageAccounts/', parameters('existingStorageAccountName')), '2016-01-01').primaryEndpoints.blob,  variables('vmStorageAccountContainerName'), '/', variables('OSDiskName'),'.vhd')]"
       }
   }
   ```

* <span data-ttu-id="9e67c-199">Affecter publique virtuels tooa adresses IP uniquement quand une application requiert.</span><span class="sxs-lookup"><span data-stu-id="9e67c-199">Assign public IP addresses tooa virtual machine only when an application requires it.</span></span> <span data-ttu-id="9e67c-200">tooconnect tooa ordinateur virtuel (VM) pour le débogage, ou de la gestion ou à des fins d’administration, utilisez les règles NAT entrantes, une passerelle de réseau virtuel ou un jumpbox.</span><span class="sxs-lookup"><span data-stu-id="9e67c-200">tooconnect tooa virtual machine (VM) for debugging, or for management or administrative purposes, use inbound NAT rules, a virtual network gateway, or a jumpbox.</span></span>
   
     <span data-ttu-id="9e67c-201">Pour plus d’informations sur la connexion toovirtual machines, consultez :</span><span class="sxs-lookup"><span data-stu-id="9e67c-201">For more information about connecting toovirtual machines, see:</span></span>
   
   * [<span data-ttu-id="9e67c-202">Exécuter des machines virtuelles pour une architecture à plusieurs niveaux dans Azure</span><span class="sxs-lookup"><span data-stu-id="9e67c-202">Run VMs for an N-tier architecture in Azure</span></span>](../guidance/guidance-compute-n-tier-vm.md)
   * [<span data-ttu-id="9e67c-203">Configurer l’accès WinRM pour les machines virtuelles dans Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9e67c-203">Set up WinRM access for VMs in Azure Resource Manager</span></span>](../virtual-machines/windows/winrm.md)
   * [<span data-ttu-id="9e67c-204">Autoriser l’accès externe tooyour machine virtuelle à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="9e67c-204">Allow external access tooyour VM by using hello Azure portal</span></span>](../virtual-machines/windows/nsg-quickstart-portal.md)
   * [<span data-ttu-id="9e67c-205">Autoriser l’accès externe tooyour machine virtuelle à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e67c-205">Allow external access tooyour VM by using PowerShell</span></span>](../virtual-machines/windows/nsg-quickstart-powershell.md)
   * [<span data-ttu-id="9e67c-206">Autoriser l’accès externe tooyour Linux VM à l’aide de CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="9e67c-206">Allow external access tooyour Linux VM by using Azure CLI</span></span>](../virtual-machines/virtual-machines-linux-nsg-quickstart.md)
* <span data-ttu-id="9e67c-207">Hello **domainNameLabel** propriété pour les adresses IP publiques doit être unique.</span><span class="sxs-lookup"><span data-stu-id="9e67c-207">hello **domainNameLabel** property for public IP addresses must be unique.</span></span> <span data-ttu-id="9e67c-208">Hello **domainNameLabel** valeur doit être comprise entre 3 et 63 caractères et suivre les règles de hello spécifiés par cette expression régulière : `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span><span class="sxs-lookup"><span data-stu-id="9e67c-208">hello **domainNameLabel** value must be between 3 and 63 characters long, and follow hello rules specified by this regular expression: `^[a-z][a-z0-9-]{1,61}[a-z0-9]$`.</span></span> <span data-ttu-id="9e67c-209">Étant donné que hello **uniqueString** fonction génère une chaîne qui est 13 caractères hello **dnsPrefixString** paramètre est limitée too50 caractères :</span><span class="sxs-lookup"><span data-stu-id="9e67c-209">Because hello **uniqueString** function generates a string that is 13 characters long, hello **dnsPrefixString** parameter is limited too50 characters:</span></span>

   ```json
   "parameters": {
       "dnsPrefixString": {
           "type": "string",
           "maxLength": 50,
           "metadata": {
               "description": "hello DNS label for hello public IP address. It must be lowercase. It should match hello following regular expression, or it will raise an error: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$"
           }
       }
   },
   "variables": {
       "dnsPrefix": "[concat(parameters('dnsPrefixString'),uniquestring(resourceGroup().id))]"
   }
   ```

* <span data-ttu-id="9e67c-210">Lorsque vous ajoutez une extension de script personnalisé tooa mot de passe, utilisez hello **commandToExecute** propriété Bonjour **protectedSettings** propriété :</span><span class="sxs-lookup"><span data-stu-id="9e67c-210">When you add a password tooa custom script extension, use hello **commandToExecute** property in hello **protectedSettings** property:</span></span>
   
   ```json
   "properties": {
       "publisher": "Microsoft.Azure.Extensions",
       "type": "CustomScript",
       "typeHandlerVersion": "2.0",
       "autoUpgradeMinorVersion": true,
       "settings": {
           "fileUris": [
               "[concat(variables('template').assets, '/lamp-app/install_lamp.sh')]"
           ]
       },
       "protectedSettings": {
           "commandToExecute": "[concat('sh install_lamp.sh ', parameters('mySqlPassword'))]"
       }
   }
   ```
   
   > [!NOTE]
   > <span data-ttu-id="9e67c-211">tooensure les clés secrètes sont chiffrés lorsqu’ils sont passés comme paramètres tooVMs et extensions, utilisez hello **protectedSettings** propriété des extensions de pertinentes hello.</span><span class="sxs-lookup"><span data-stu-id="9e67c-211">tooensure that secrets are encrypted when they are passed as parameters tooVMs and extensions, use hello **protectedSettings** property of hello relevant extensions.</span></span>
   > 
   > 

## <a name="outputs"></a><span data-ttu-id="9e67c-212">outputs</span><span class="sxs-lookup"><span data-stu-id="9e67c-212">Outputs</span></span>
<span data-ttu-id="9e67c-213">Si vous utilisez un modèle toocreate des adresses IP publiques, inclure une **génère** section qui renvoie les détails de l’adresse IP de hello et nom de domaine complet de hello (FQDN).</span><span class="sxs-lookup"><span data-stu-id="9e67c-213">If you use a template toocreate public IP addresses, include an **outputs** section that returns details of hello IP address and hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="9e67c-214">Vous pouvez utiliser la sortie valeurs tooeasily récupérer détails sur les adresses IP et les noms de domaine complets public après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="9e67c-214">You can use output values tooeasily retrieve details about public IP addresses and FQDNs after deployment.</span></span> <span data-ttu-id="9e67c-215">Lorsque vous référencez des ressources de hello, utilisez la version hello API que vous avez utilisé toocreate il :</span><span class="sxs-lookup"><span data-stu-id="9e67c-215">When you reference hello resource, use hello API version that you used toocreate it:</span></span> 

```json
"outputs": {
    "fqdn": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').dnsSettings.fqdn]",
        "type": "string"
    },
    "ipaddress": {
        "value": "[reference(resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName')), '2016-07-01').ipAddress]",
        "type": "string"
    }
}
```

## <a name="single-template-vs-nested-templates"></a><span data-ttu-id="9e67c-216">Modèle unique ou modèles imbriqués</span><span class="sxs-lookup"><span data-stu-id="9e67c-216">Single template vs. nested templates</span></span>
<span data-ttu-id="9e67c-217">toodeploy votre solution, vous pouvez utiliser un modèle unique ou un modèle principal avec plusieurs modèles imbriqués.</span><span class="sxs-lookup"><span data-stu-id="9e67c-217">toodeploy your solution, you can use either a single template or a main template with multiple nested templates.</span></span> <span data-ttu-id="9e67c-218">Les modèles imbriqués sont courants dans des scénarios plus avancés.</span><span class="sxs-lookup"><span data-stu-id="9e67c-218">Nested templates are common for more advanced scenarios.</span></span> <span data-ttu-id="9e67c-219">À l’aide d’une offre de modèle imbriqué vous hello suivant avantages :</span><span class="sxs-lookup"><span data-stu-id="9e67c-219">Using a nested template gives you hello following advantages:</span></span>

* <span data-ttu-id="9e67c-220">Ils permettent de décomposer une solution en composants ciblés.</span><span class="sxs-lookup"><span data-stu-id="9e67c-220">You can break down a solution into targeted components.</span></span>
* <span data-ttu-id="9e67c-221">Ils peuvent être réutilisés dans différents modèles principaux.</span><span class="sxs-lookup"><span data-stu-id="9e67c-221">You can reuse nested templates with different main templates.</span></span>

<span data-ttu-id="9e67c-222">Si vous choisissez les modèles toouse imbriqué, hello suivant les recommandations peut vous aider à normaliser la conception de votre modèle.</span><span class="sxs-lookup"><span data-stu-id="9e67c-222">If you choose toouse nested templates, hello following guidelines can help you standardize your template design.</span></span> <span data-ttu-id="9e67c-223">Ces instructions sont basées sur les [modèles pour la conception de modèles Azure Resource Manager](best-practices-resource-manager-design-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9e67c-223">These guidelines are based on [patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="9e67c-224">Nous vous recommandons une conception qui a hello suivant de modèles :</span><span class="sxs-lookup"><span data-stu-id="9e67c-224">We recommend a design that has hello following templates:</span></span>

* <span data-ttu-id="9e67c-225">**Modèle principal** (azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="9e67c-225">**Main template** (azuredeploy.json).</span></span> <span data-ttu-id="9e67c-226">À utiliser pour les paramètres d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="9e67c-226">Use for hello input parameters.</span></span>
* <span data-ttu-id="9e67c-227">**Modèle de ressource partagé**.</span><span class="sxs-lookup"><span data-stu-id="9e67c-227">**Shared resources template**.</span></span> <span data-ttu-id="9e67c-228">Toodeploy d’utilisation des ressources qui utilisent de toutes les autres ressources partagées (par exemple, virtuel réseau et la disponibilité ensembles).</span><span class="sxs-lookup"><span data-stu-id="9e67c-228">Use toodeploy shared resources that all other resources use (for example, virtual network and availability sets).</span></span> <span data-ttu-id="9e67c-229">Hello d’utilisation **dependsOn** tooensure expression que ce modèle est déployé avant les autres modèles.</span><span class="sxs-lookup"><span data-stu-id="9e67c-229">Use hello **dependsOn** expression tooensure that this template is deployed before other templates.</span></span>
* <span data-ttu-id="9e67c-230">**Modèle de ressource facultatif**.</span><span class="sxs-lookup"><span data-stu-id="9e67c-230">**Optional resources template**.</span></span> <span data-ttu-id="9e67c-231">Utilisez tooconditionally déployer les ressources basées sur un paramètre (par exemple, un jumpbox).</span><span class="sxs-lookup"><span data-stu-id="9e67c-231">Use tooconditionally deploy resources based on a parameter (for example, a jumpbox).</span></span>
* <span data-ttu-id="9e67c-232">**Modèle de ressource de membre**.</span><span class="sxs-lookup"><span data-stu-id="9e67c-232">**Member resources template**.</span></span> <span data-ttu-id="9e67c-233">Chaque type d’instance dans une couche application a sa propre configuration.</span><span class="sxs-lookup"><span data-stu-id="9e67c-233">Each instance type within an application tier has its own configuration.</span></span> <span data-ttu-id="9e67c-234">Au sein d’un niveau, vous pouvez définir différents types d’instance.</span><span class="sxs-lookup"><span data-stu-id="9e67c-234">Within a tier, you can define different instance types.</span></span> <span data-ttu-id="9e67c-235">(Par exemple, hello première instance crée un cluster et des instances supplémentaires sont ajoutées cluster existant de toohello.) Chaque type d’instance a son propre modèle de déploiement.</span><span class="sxs-lookup"><span data-stu-id="9e67c-235">(For example, hello first instance creates a cluster, and additional instances are added toohello existing cluster.) Each instance type has its own deployment template.</span></span>
* <span data-ttu-id="9e67c-236">**Scripts**.</span><span class="sxs-lookup"><span data-stu-id="9e67c-236">**Scripts**.</span></span> <span data-ttu-id="9e67c-237">Des scripts largement réutilisables sont applicables pour chaque type d’instance (par exemple, l’initialisation et le formatage de disques supplémentaires).</span><span class="sxs-lookup"><span data-stu-id="9e67c-237">Widely reusable scripts are applicable for each instance type (for example, initialize and format additional disks).</span></span> <span data-ttu-id="9e67c-238">Les scripts personnalisés que vous créez dans un but de personnalisation spécifiques sont différents, selon le type d’instance hello.</span><span class="sxs-lookup"><span data-stu-id="9e67c-238">Custom scripts that you create for a specific customization purpose are different, based on hello instance type.</span></span>

![Modèle imbriqué](./media/resource-manager-template-best-practices/nestedTemplateDesign.png)

<span data-ttu-id="9e67c-240">Pour plus d’informations, voir [Utilisation de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9e67c-240">For more information, see [Use linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="conditionally-link-toonested-templates"></a><span data-ttu-id="9e67c-241">Lier de manière conditionnelle toonested modèles</span><span class="sxs-lookup"><span data-stu-id="9e67c-241">Conditionally link toonested templates</span></span>
<span data-ttu-id="9e67c-242">Vous pouvez utiliser un paramètre tooconditionally lien toonested des modèles.</span><span class="sxs-lookup"><span data-stu-id="9e67c-242">You can use a parameter tooconditionally link toonested templates.</span></span> <span data-ttu-id="9e67c-243">paramètre Hello devient partie intégrante de hello URI pour le modèle de hello :</span><span class="sxs-lookup"><span data-stu-id="9e67c-243">hello parameter becomes part of hello URI for hello template:</span></span>

```json
"parameters": {
    "newOrExisting": {
        "type": "String",
        "allowedValues": [
            "new",
            "existing"
        ]
    }
},
"variables": {
    "templatelink": "[concat('https://raw.githubusercontent.com/Contoso/Templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
},
"resources": [
    {
        "apiVersion": "2015-01-01",
        "name": "nestedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
            "mode": "incremental",
            "templateLink": {
                "uri": "[variables('templatelink')]",
                "contentVersion": "1.0.0.0"
            },
            "parameters": {
            }
        }
    }
]
```

## <a name="template-format"></a><span data-ttu-id="9e67c-244">Format de modèle</span><span class="sxs-lookup"><span data-stu-id="9e67c-244">Template format</span></span>
<span data-ttu-id="9e67c-245">Il s’agit d’une bonne approche en matière toopass votre modèle via un validateur JSON.</span><span class="sxs-lookup"><span data-stu-id="9e67c-245">It's a good practice toopass your template through a JSON validator.</span></span> <span data-ttu-id="9e67c-246">Un validateur peut vous aider à supprimer les virgules, parenthèses et crochets superflus susceptibles de provoquer une erreur lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="9e67c-246">A validator can help you remove extraneous commas, parentheses, and brackets that might cause an error during deployment.</span></span> <span data-ttu-id="9e67c-247">Essayez [JSONlint](http://jsonlint.com/) ou un package de linter pour votre environnement d’édition favori (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="9e67c-247">Try [JSONLint](http://jsonlint.com/) or a linter package for your favorite editing environment (Visual Studio Code, Atom, Sublime Text, Visual Studio).</span></span>

<span data-ttu-id="9e67c-248">Il est également une bonne idée tooformat votre JSON pour une meilleure lisibilité.</span><span class="sxs-lookup"><span data-stu-id="9e67c-248">It's also a good idea tooformat your JSON for better readability.</span></span> <span data-ttu-id="9e67c-249">Vous pouvez utiliser un package de formatage JSON de votre éditeur local.</span><span class="sxs-lookup"><span data-stu-id="9e67c-249">You can use a JSON formatter package for your local editor.</span></span> <span data-ttu-id="9e67c-250">Dans Visual Studio, le document de hello tooformat, appuyez sur **Ctrl + K, Ctrl + D**.</span><span class="sxs-lookup"><span data-stu-id="9e67c-250">In Visual Studio, tooformat hello document, press **Ctrl+K, Ctrl+D**.</span></span> <span data-ttu-id="9e67c-251">Dans Visual Studio Code, appuyez sur **Alt + Maj + F**.</span><span class="sxs-lookup"><span data-stu-id="9e67c-251">In Visual Studio Code, press **Alt+Shift+F**.</span></span> <span data-ttu-id="9e67c-252">Si votre éditeur local ne de format de document de hello, vous pouvez utiliser un [formateur en ligne](https://www.bing.com/search?q=json+formatter).</span><span class="sxs-lookup"><span data-stu-id="9e67c-252">If your local editor doesn't format hello document, you can use an [online formatter](https://www.bing.com/search?q=json+formatter).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e67c-253">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9e67c-253">Next steps</span></span>
* <span data-ttu-id="9e67c-254">Pour obtenir des conseils sur la conception de votre solution pour des machines virtuelles, voir [Exécution d’une machine virtuelle Windows sur Azure](../guidance/guidance-compute-single-vm.md) et [Exécution d’une machine virtuelle Linux sur Azure](../guidance/guidance-compute-single-vm-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9e67c-254">For guidance on architecting your solution for virtual machines, see [Run a Windows VM in Azure](../guidance/guidance-compute-single-vm.md) and [Run a Linux VM in Azure](../guidance/guidance-compute-single-vm-linux.md).</span></span>
* <span data-ttu-id="9e67c-255">Pour des conseils sur la configuration d’un compte de stockage, voir [Liste de contrôle des performances et de l’extensibilité d’Azure Storage](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="9e67c-255">For guidance on setting up a storage account, see [Azure Storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>
* <span data-ttu-id="9e67c-256">toolearn sur comment une entreprise peut utiliser le Gestionnaire de ressources tooeffectively gérer les abonnements, consultez [une vue de structure Azure enterprise : la gouvernance des abonnement](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="9e67c-256">toolearn about how an enterprise can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold: Prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

