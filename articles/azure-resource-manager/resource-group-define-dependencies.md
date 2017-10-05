---
title: "Définir l’ordre de déploiement des ressources Azure | Microsoft Docs"
description: "Décrit la procédure permettant de définir une ressource comme dépendante d’une autre ressource au cours du déploiement afin de garantir le déploiement des ressources dans l'ordre adéquat."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 3d6a46116ae9d7d940bc10dfa832540f42c0af7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="define-the-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="0d22d-103">Définir l’ordre de déploiement des ressources dans les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0d22d-103">Define the order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="0d22d-104">Une ressource donnée peut comporter d'autres ressources qui doivent exister avant son déploiement.</span><span class="sxs-lookup"><span data-stu-id="0d22d-104">For a given resource, there can be other resources that must exist before the resource is deployed.</span></span> <span data-ttu-id="0d22d-105">Par exemple, un serveur SQL doit exister avant une tentative de déploiement d'une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="0d22d-105">For example, a SQL server must exist before attempting to deploy a SQL database.</span></span> <span data-ttu-id="0d22d-106">Vous définissez cette relation en marquant une seule ressource comme dépendante de l'autre ressource.</span><span class="sxs-lookup"><span data-stu-id="0d22d-106">You define this relationship by marking one resource as dependent on the other resource.</span></span> <span data-ttu-id="0d22d-107">Pour définir une dépendance, vous devez utiliser l’élément **dependsOn** ou la fonction **reference**.</span><span class="sxs-lookup"><span data-stu-id="0d22d-107">You define a dependency with the **dependsOn** element, or by using the **reference** function.</span></span> 

<span data-ttu-id="0d22d-108">Resource Manager évalue les dépendances entre les ressources et les déploie dans leur ordre dépendant.</span><span class="sxs-lookup"><span data-stu-id="0d22d-108">Resource Manager evaluates the dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="0d22d-109">Quand les ressources ne dépendent pas les unes des autres, Resource Manager les déploie en parallèle.</span><span class="sxs-lookup"><span data-stu-id="0d22d-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="0d22d-110">Vous devez uniquement définir des dépendances pour les ressources qui sont déployées dans le même modèle.</span><span class="sxs-lookup"><span data-stu-id="0d22d-110">You only need to define dependencies for resources that are deployed in the same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="0d22d-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="0d22d-111">dependsOn</span></span>
<span data-ttu-id="0d22d-112">Dans votre modèle, l’élément dependsOn vous permet de définir une ressource comme une dépendance sur une ou plusieurs ressources.</span><span class="sxs-lookup"><span data-stu-id="0d22d-112">Within your template, the dependsOn element enables you to define one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="0d22d-113">Sa valeur peut être une liste séparée par des virgules de noms de ressources.</span><span class="sxs-lookup"><span data-stu-id="0d22d-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="0d22d-114">L’exemple suivant montre un groupe identique de machines virtuelles dépendant d’un équilibreur de charge, un réseau virtuel et une boucle qui crée plusieurs comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="0d22d-114">The following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="0d22d-115">Ces autres ressources ne figurent pas dans l’exemple suivant, mais ont besoin d’exister ailleurs dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="0d22d-115">These other resources are not shown in the following example, but they would need to exist elsewhere in the template.</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

<span data-ttu-id="0d22d-116">Dans l’exemple précédent, une dépendance est incluse sur les ressources créées par le biais d’une boucle de copie nommée **storageLoop**.</span><span class="sxs-lookup"><span data-stu-id="0d22d-116">In the preceding example, a dependency is included on the resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="0d22d-117">Pour obtenir un exemple, consultez [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="0d22d-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="0d22d-118">Lors de la définition des dépendances, vous pouvez inclure l’espace de noms du fournisseur de ressources et le type de ressource pour éviter toute ambiguïté.</span><span class="sxs-lookup"><span data-stu-id="0d22d-118">When defining dependencies, you can include the resource provider namespace and resource type to avoid ambiguity.</span></span> <span data-ttu-id="0d22d-119">Par exemple, pour distinguer un équilibrage de charge et un réseau virtuel qui peuvent avoir les mêmes noms que d’autres ressources, utilisez le format suivant :</span><span class="sxs-lookup"><span data-stu-id="0d22d-119">For example, to clarify a load balancer and virtual network that may have the same names as other resources, use the following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="0d22d-120">Vous pouvez être tenté d’utiliser dependsOn pour mapper les relations entre vos ressources. Il est toutefois important de comprendre pourquoi vous le faites.</span><span class="sxs-lookup"><span data-stu-id="0d22d-120">While you may be inclined to use dependsOn to map relationships between your resources, it's important to understand why you're doing it.</span></span> <span data-ttu-id="0d22d-121">Par exemple, pour documenter la manière dont les ressources sont liées entre elles, dependsOn n’est pas la bonne approche.</span><span class="sxs-lookup"><span data-stu-id="0d22d-121">For example, to document how resources are interconnected, dependsOn is not the right approach.</span></span> <span data-ttu-id="0d22d-122">Vous ne pourrez pas lancer de requête pour savoir quelles ressources ont été définies dans l’élément dependsOn après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="0d22d-122">You cannot query which resources were defined in the dependsOn element after deployment.</span></span> <span data-ttu-id="0d22d-123">En utilisant dependsOn, vous risquez d’avoir un impact sur le temps de déploiement, car Resource Manager ne déploie pas en parallèle deux ressources qui ont une dépendance.</span><span class="sxs-lookup"><span data-stu-id="0d22d-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="0d22d-124">Pour documenter les relations entre les ressources, utilisez plutôt la [liaison de ressources](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="0d22d-124">To document relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="0d22d-125">Ressources enfants</span><span class="sxs-lookup"><span data-stu-id="0d22d-125">Child resources</span></span>
<span data-ttu-id="0d22d-126">La propriété de ressources vous permet de vous permet de spécifier les ressources enfants associées à la ressource en cours de définition.</span><span class="sxs-lookup"><span data-stu-id="0d22d-126">The resources property allows you to specify child resources that are related to the resource being defined.</span></span> <span data-ttu-id="0d22d-127">Les ressources enfants peuvent uniquement être définies sur cinq niveaux.</span><span class="sxs-lookup"><span data-stu-id="0d22d-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="0d22d-128">Il est important de noter qu’aucune dépendance implicite n’est créée entre une ressources enfant et la ressource parent.</span><span class="sxs-lookup"><span data-stu-id="0d22d-128">It is important to note that an implicit dependency is not created between a child resource and the parent resource.</span></span> <span data-ttu-id="0d22d-129">Si vous avez besoin de déployer la ressource enfant après la ressource parent, vous devez déclarer explicitement cette dépendance avec la propriété dependsOn.</span><span class="sxs-lookup"><span data-stu-id="0d22d-129">If you need the child resource to be deployed after the parent resource, you must explicitly state that dependency with the dependsOn property.</span></span> 

<span data-ttu-id="0d22d-130">Chaque ressource parente accepte uniquement certains types de ressources comme ressources enfants.</span><span class="sxs-lookup"><span data-stu-id="0d22d-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="0d22d-131">Les types de ressource acceptés sont spécifiés dans le [schéma de modèle](https://github.com/Azure/azure-resource-manager-schemas) de la ressource parente.</span><span class="sxs-lookup"><span data-stu-id="0d22d-131">The accepted resource types are specified in the [template schema](https://github.com/Azure/azure-resource-manager-schemas) of the parent resource.</span></span> <span data-ttu-id="0d22d-132">Le nom du type de ressource enfant inclut le nom du type de ressource parente. Par exemple, **Microsoft.Web/sites/config** et **Microsoft.Web/sites/extensions** sont deux ressources enfants de **Microsoft.Web/sites**.</span><span class="sxs-lookup"><span data-stu-id="0d22d-132">The name of child resource type includes the name of the parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of the **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="0d22d-133">L'exemple suivant montre un serveur SQL et une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="0d22d-133">The following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="0d22d-134">Notez qu'une dépendance explicite est définie entre la base de données SQL et le serveur SQL, même si la base de données est un enfant du serveur.</span><span class="sxs-lookup"><span data-stu-id="0d22d-134">Notice that an explicit dependency is defined between the SQL database and SQL server, even though the database is a child of the server.</span></span>

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a><span data-ttu-id="0d22d-135">fonction de référence</span><span class="sxs-lookup"><span data-stu-id="0d22d-135">reference function</span></span>
<span data-ttu-id="0d22d-136">La [fonction de référence](resource-group-template-functions-resource.md#reference) permet à une expression de tirer sa valeur d’un autre nom JSON et de paires de valeurs ou de ressources runtime.</span><span class="sxs-lookup"><span data-stu-id="0d22d-136">The [reference function](resource-group-template-functions-resource.md#reference) enables an expression to derive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="0d22d-137">Les expressions de référence déclarent implicitement qu’une ressource dépend d’une autre.</span><span class="sxs-lookup"><span data-stu-id="0d22d-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="0d22d-138">Le format général est le suivant :</span><span class="sxs-lookup"><span data-stu-id="0d22d-138">The general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="0d22d-139">Dans l’exemple suivant, un point de terminaison CDN dépend explicitement du profil CDN et implicitement d’une application web.</span><span class="sxs-lookup"><span data-stu-id="0d22d-139">In the following example, a CDN endpoint explicitly depends on the CDN profile, and implicitly depends on a web app.</span></span>

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

<span data-ttu-id="0d22d-140">Vous pouvez utiliser cet élément ou l’élément dependsOn pour spécifier les dépendances, mais il est inutile d’utiliser les deux pour la même ressource dépendante.</span><span class="sxs-lookup"><span data-stu-id="0d22d-140">You can use either this element or the dependsOn element to specify dependencies, but you do not need to use both for the same dependent resource.</span></span> <span data-ttu-id="0d22d-141">Si possible, utilisez une référence implicite pour éviter d’ajouter une dépendance inutile.</span><span class="sxs-lookup"><span data-stu-id="0d22d-141">Whenever possible, use an implicit reference to avoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="0d22d-142">Pour plus d’informations, consultez la [fonction de référence](resource-group-template-functions-resource.md#reference).</span><span class="sxs-lookup"><span data-stu-id="0d22d-142">To learn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="0d22d-143">Recommandations pour la définition des dépendances</span><span class="sxs-lookup"><span data-stu-id="0d22d-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="0d22d-144">Lorsque vous décidez des dépendances à définir, appliquez les recommandations suivantes :</span><span class="sxs-lookup"><span data-stu-id="0d22d-144">When deciding what dependencies to set, use the following guidelines:</span></span>

* <span data-ttu-id="0d22d-145">Définissez le moins de dépendances possible.</span><span class="sxs-lookup"><span data-stu-id="0d22d-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="0d22d-146">Définissez une ressource enfant comme dépendante de sa ressource parent.</span><span class="sxs-lookup"><span data-stu-id="0d22d-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="0d22d-147">Utilisez la fonction **reference** pour définir les dépendances implicites entre les ressources qui doivent partager une propriété.</span><span class="sxs-lookup"><span data-stu-id="0d22d-147">Use the **reference** function to set implicit dependencies between resources that need to share a property.</span></span> <span data-ttu-id="0d22d-148">N’ajoutez pas de dépendance explicite (**dependsOn**) lorsque vous avez déjà défini une dépendance implicite.</span><span class="sxs-lookup"><span data-stu-id="0d22d-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="0d22d-149">Cette approche permet de réduire le risque d’avoir des dépendances inutiles.</span><span class="sxs-lookup"><span data-stu-id="0d22d-149">This approach reduces the risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="0d22d-150">Définissez une dépendance lorsqu’une ressource ne peut pas être **créée** sans la fonctionnalité d’une autre ressource.</span><span class="sxs-lookup"><span data-stu-id="0d22d-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="0d22d-151">Ne définissez pas de dépendance si les ressources interagissent uniquement après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="0d22d-151">Do not set a dependency if the resources only interact after deployment.</span></span>
* <span data-ttu-id="0d22d-152">Ajoutez les dépendances l’une après l’autre sans les définir explicitement.</span><span class="sxs-lookup"><span data-stu-id="0d22d-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="0d22d-153">Par exemple, votre machine virtuelle dépend d’une interface de réseau virtuel, et l’interface de réseau virtuelle dépend d’un réseau virtuel et d’adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="0d22d-153">For example, your virtual machine depends on a virtual network interface, and the virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="0d22d-154">Par conséquent, la machine virtuelle est déployée après les trois ressources. Cependant, ne définissez pas explicitement la machine virtuelle comme dépendante de ces trois ressources.</span><span class="sxs-lookup"><span data-stu-id="0d22d-154">Therefore, the virtual machine is deployed after all three resources, but do not explicitly set the virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="0d22d-155">Cette approche permet de clarifier l’ordre des dépendances et de simplifier les modifications ultérieures du modèle.</span><span class="sxs-lookup"><span data-stu-id="0d22d-155">This approach clarifies the dependency order and makes it easier to change the template later.</span></span>
* <span data-ttu-id="0d22d-156">Si une valeur peut être déterminée avant le déploiement, essayez de déployer la ressource sans dépendance.</span><span class="sxs-lookup"><span data-stu-id="0d22d-156">If a value can be determined before deployment, try deploying the resource without a dependency.</span></span> <span data-ttu-id="0d22d-157">Par exemple, si une valeur de configuration a besoin du nom d’une autre ressource, vous n’avez pas forcément besoin d’une dépendance.</span><span class="sxs-lookup"><span data-stu-id="0d22d-157">For example, if a configuration value needs the name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="0d22d-158">Cette recommandation n’est pas toujours applicable, car certaines ressources vérifient l’existence de l’autre ressource.</span><span class="sxs-lookup"><span data-stu-id="0d22d-158">This guidance does not always work because some resources verify the existence of the other resource.</span></span> <span data-ttu-id="0d22d-159">Si vous recevez une erreur, ajoutez une dépendance.</span><span class="sxs-lookup"><span data-stu-id="0d22d-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="0d22d-160">Resource Manager identifie les dépendances circulaires lors de la validation du modèle.</span><span class="sxs-lookup"><span data-stu-id="0d22d-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="0d22d-161">Si vous recevez une erreur indiquant qu’il existe une dépendance circulaire, évaluez votre modèle pour déterminer si certaines dépendances sont inutiles et peuvent être supprimées.</span><span class="sxs-lookup"><span data-stu-id="0d22d-161">If you receive an error stating that a circular dependency exists, evaluate your template to see if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="0d22d-162">Si la suppression de ces dépendances n’a aucun effet, vous pouvez éliminer les dépendances circulaires en déplaçant certaines opérations de déploiement dans les ressources enfants qui sont déployées après les ressources présentant la dépendance circulaire.</span><span class="sxs-lookup"><span data-stu-id="0d22d-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after the resources that have the circular dependency.</span></span> <span data-ttu-id="0d22d-163">Par exemple, supposons que vous déployiez deux machines virtuelles, mais que vous deviez définir sur chacune d’elles des propriétés faisant référence les unes aux autres.</span><span class="sxs-lookup"><span data-stu-id="0d22d-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span></span> <span data-ttu-id="0d22d-164">Vous pouvez les déployer dans l’ordre suivant :</span><span class="sxs-lookup"><span data-stu-id="0d22d-164">You can deploy them in the following order:</span></span>

1. <span data-ttu-id="0d22d-165">Machine virtuelle 1</span><span class="sxs-lookup"><span data-stu-id="0d22d-165">vm1</span></span>
2. <span data-ttu-id="0d22d-166">Machine virtuelle 2</span><span class="sxs-lookup"><span data-stu-id="0d22d-166">vm2</span></span>
3. <span data-ttu-id="0d22d-167">L’extension sur la machine virtuelle 1 dépend des machines virtuelles 1 et 2.</span><span class="sxs-lookup"><span data-stu-id="0d22d-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="0d22d-168">L’extension définit sur la machine virtuelle 1 des valeurs qu’elle obtient de la machine virtuelle 2.</span><span class="sxs-lookup"><span data-stu-id="0d22d-168">The extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="0d22d-169">L’extension sur la machine virtuelle 2 dépend des machines virtuelles 1 et 2.</span><span class="sxs-lookup"><span data-stu-id="0d22d-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="0d22d-170">L’extension définit sur la machine virtuelle 2 des valeurs qu’elle obtient de la machine virtuelle 1.</span><span class="sxs-lookup"><span data-stu-id="0d22d-170">The extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="0d22d-171">Pour plus d’informations sur l’évaluation de l’ordre de déploiement et la résolution des erreurs de dépendance, consultez l’article [Résolution des erreurs courantes dans des déploiements Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="0d22d-171">For information about assessing the deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d22d-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0d22d-172">Next steps</span></span>
* <span data-ttu-id="0d22d-173">Pour en savoir plus sur la résolution des problèmes liés aux dépendances lors du déploiement, consultez [Résolution des erreurs courantes dans des déploiements Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="0d22d-173">To learn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="0d22d-174">Pour en savoir plus sur la création de modèles Azure Resource Manager, consultez [Création de modèles](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0d22d-174">To learn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="0d22d-175">Pour obtenir la liste des fonctions disponibles dans un modèle, consultez [Fonctions de modèle](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="0d22d-175">For a list of the available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

