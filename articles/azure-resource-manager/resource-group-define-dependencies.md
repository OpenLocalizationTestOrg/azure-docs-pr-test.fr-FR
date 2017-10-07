---
title: "ordre de déploiement aaaSet pour les ressources Azure | Documents Microsoft"
description: "Décrit comment tooset une seule ressource comme dépend d’une autre ressource pendant tooensure des ressources de déploiement sont déployés dans l’ordre correct de hello."
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
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="00fbb-103">Définir l’ordre de hello pour le déploiement de ressources dans les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="00fbb-103">Define hello order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="00fbb-104">Pour une ressource donnée, il peut y avoir des autres ressources qui doivent exister pour que la ressource de hello est déployée.</span><span class="sxs-lookup"><span data-stu-id="00fbb-104">For a given resource, there can be other resources that must exist before hello resource is deployed.</span></span> <span data-ttu-id="00fbb-105">Par exemple, un serveur SQL server doit exister avant de tenter de toodeploy une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="00fbb-105">For example, a SQL server must exist before attempting toodeploy a SQL database.</span></span> <span data-ttu-id="00fbb-106">Pour définir cette relation, le marquage d’une ressource en tant que dépendant de hello autre ressource.</span><span class="sxs-lookup"><span data-stu-id="00fbb-106">You define this relationship by marking one resource as dependent on hello other resource.</span></span> <span data-ttu-id="00fbb-107">Vous définissez une dépendance avec hello **dependsOn** élément, ou à l’aide de hello **référence** (fonction).</span><span class="sxs-lookup"><span data-stu-id="00fbb-107">You define a dependency with hello **dependsOn** element, or by using hello **reference** function.</span></span> 

<span data-ttu-id="00fbb-108">Le Gestionnaire de ressources évalue des dépendances hello entre les ressources et les déploie dans leur ordre dépendant.</span><span class="sxs-lookup"><span data-stu-id="00fbb-108">Resource Manager evaluates hello dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="00fbb-109">Quand les ressources ne dépendent pas les unes des autres, Resource Manager les déploie en parallèle.</span><span class="sxs-lookup"><span data-stu-id="00fbb-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="00fbb-110">Vous devez uniquement toodefine dépendances pour les ressources qui sont déployés dans hello même modèle.</span><span class="sxs-lookup"><span data-stu-id="00fbb-110">You only need toodefine dependencies for resources that are deployed in hello same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="00fbb-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="00fbb-111">dependsOn</span></span>
<span data-ttu-id="00fbb-112">Dans votre modèle, élément de dependsOn hello vous permet de toodefine une ressource en tant que dépendant sur une ou plusieurs ressources.</span><span class="sxs-lookup"><span data-stu-id="00fbb-112">Within your template, hello dependsOn element enables you toodefine one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="00fbb-113">Sa valeur peut être une liste séparée par des virgules de noms de ressources.</span><span class="sxs-lookup"><span data-stu-id="00fbb-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="00fbb-114">Hello suivant montre un ensemble d’échelle de machine virtuelle qui dépend d’un équilibrage de charge, le réseau virtuel et une boucle qui crée plusieurs comptes de stockage.</span><span class="sxs-lookup"><span data-stu-id="00fbb-114">hello following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="00fbb-115">Ces autres ressources ne sont pas affichés dans hello l’exemple suivant, mais ils ont besoin tooexist ailleurs dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="00fbb-115">These other resources are not shown in hello following example, but they would need tooexist elsewhere in hello template.</span></span>

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

<span data-ttu-id="00fbb-116">Bonjour précédent exemple, une dépendance est incluse dans les ressources hello qui sont créés dans une boucle de copie nommée **storageLoop**.</span><span class="sxs-lookup"><span data-stu-id="00fbb-116">In hello preceding example, a dependency is included on hello resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="00fbb-117">Pour obtenir un exemple, consultez [Création de plusieurs instances de ressources dans Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="00fbb-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="00fbb-118">Lors de la définition des dépendances, vous pouvez inclure hello ressource fournisseur espace de noms et de la ressource de type tooavoid toute ambiguïté.</span><span class="sxs-lookup"><span data-stu-id="00fbb-118">When defining dependencies, you can include hello resource provider namespace and resource type tooavoid ambiguity.</span></span> <span data-ttu-id="00fbb-119">Par exemple, tooclarify mettre en forme un équilibreur de charge et le réseau virtuel qui peut avoir hello que mêmes noms que d’autres ressources, hello utilisation suivant :</span><span class="sxs-lookup"><span data-stu-id="00fbb-119">For example, tooclarify a load balancer and virtual network that may have hello same names as other resources, use hello following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="00fbb-120">Vous pouvez être tenté toouse dependsOn toomap relations entre vos ressources, mais il est important toounderstand pourquoi votre travail.</span><span class="sxs-lookup"><span data-stu-id="00fbb-120">While you may be inclined toouse dependsOn toomap relationships between your resources, it's important toounderstand why you're doing it.</span></span> <span data-ttu-id="00fbb-121">Par exemple, la façon dont les ressources sont interconnectés, de toodocument dependsOn n’est pas une approche hello.</span><span class="sxs-lookup"><span data-stu-id="00fbb-121">For example, toodocument how resources are interconnected, dependsOn is not hello right approach.</span></span> <span data-ttu-id="00fbb-122">Vous ne peut pas interroger les ressources qui ont été définies dans l’élément dependsOn de hello après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="00fbb-122">You cannot query which resources were defined in hello dependsOn element after deployment.</span></span> <span data-ttu-id="00fbb-123">En utilisant dependsOn, vous risquez d’avoir un impact sur le temps de déploiement, car Resource Manager ne déploie pas en parallèle deux ressources qui ont une dépendance.</span><span class="sxs-lookup"><span data-stu-id="00fbb-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="00fbb-124">toodocument les relations entre les ressources, utilisez à la place [liaison des ressources](/rest/api/resources/resourcelinks).</span><span class="sxs-lookup"><span data-stu-id="00fbb-124">toodocument relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="00fbb-125">Ressources enfants</span><span class="sxs-lookup"><span data-stu-id="00fbb-125">Child resources</span></span>
<span data-ttu-id="00fbb-126">propriété des ressources Hello vous permet de ressources enfants toospecify toohello connexes des ressources en cours de définition.</span><span class="sxs-lookup"><span data-stu-id="00fbb-126">hello resources property allows you toospecify child resources that are related toohello resource being defined.</span></span> <span data-ttu-id="00fbb-127">Les ressources enfants peuvent uniquement être définies sur cinq niveaux.</span><span class="sxs-lookup"><span data-stu-id="00fbb-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="00fbb-128">Il est important de toonote une dépendance implicite n’est pas créée entre une ressource enfant et la ressource parent de hello.</span><span class="sxs-lookup"><span data-stu-id="00fbb-128">It is important toonote that an implicit dependency is not created between a child resource and hello parent resource.</span></span> <span data-ttu-id="00fbb-129">Si vous avez besoin de hello toobe de ressource enfant déployé après la ressource parent de hello, vous devez déclarer explicitement cette dépendance avec la propriété : dependsOn hello.</span><span class="sxs-lookup"><span data-stu-id="00fbb-129">If you need hello child resource toobe deployed after hello parent resource, you must explicitly state that dependency with hello dependsOn property.</span></span> 

<span data-ttu-id="00fbb-130">Chaque ressource parente accepte uniquement certains types de ressources comme ressources enfants.</span><span class="sxs-lookup"><span data-stu-id="00fbb-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="00fbb-131">Hello accepté de types de ressources sont spécifiés dans hello [schéma de modèle](https://github.com/Azure/azure-resource-manager-schemas) de ressource du parent hello.</span><span class="sxs-lookup"><span data-stu-id="00fbb-131">hello accepted resource types are specified in hello [template schema](https://github.com/Azure/azure-resource-manager-schemas) of hello parent resource.</span></span> <span data-ttu-id="00fbb-132">nom Hello enfant du type de ressource inclut le nom hello hello parent du type de ressource, telles que **Microsoft.Web/sites/config** et **Microsoft.Web/sites/extensions** sont les deux ressources enfant de hello  **Microsoft.Web/sites**.</span><span class="sxs-lookup"><span data-stu-id="00fbb-132">hello name of child resource type includes hello name of hello parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of hello **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="00fbb-133">Bonjour à l’exemple suivant montre un SQL server et la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="00fbb-133">hello following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="00fbb-134">Notez qu’une dépendance explicite est définie entre la base de données SQL hello et SQL server, même si la base de données hello est un enfant du serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="00fbb-134">Notice that an explicit dependency is defined between hello SQL database and SQL server, even though hello database is a child of hello server.</span></span>

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

## <a name="reference-function"></a><span data-ttu-id="00fbb-135">fonction de référence</span><span class="sxs-lookup"><span data-stu-id="00fbb-135">reference function</span></span>
<span data-ttu-id="00fbb-136">Hello [font référence à fonction](resource-group-template-functions-resource.md#reference) permet une tooderive expression sa valeur à partir d’autres paires nom / valeur JSON ou les ressources d’exécution.</span><span class="sxs-lookup"><span data-stu-id="00fbb-136">hello [reference function](resource-group-template-functions-resource.md#reference) enables an expression tooderive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="00fbb-137">Les expressions de référence déclarent implicitement qu’une ressource dépend d’une autre.</span><span class="sxs-lookup"><span data-stu-id="00fbb-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="00fbb-138">le format général Hello est :</span><span class="sxs-lookup"><span data-stu-id="00fbb-138">hello general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="00fbb-139">Bonjour l’exemple suivant, un point de terminaison CDN explicitement dépend hello profil CDN et implicitement dépend d’une application web.</span><span class="sxs-lookup"><span data-stu-id="00fbb-139">In hello following example, a CDN endpoint explicitly depends on hello CDN profile, and implicitly depends on a web app.</span></span>

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

<span data-ttu-id="00fbb-140">Vous pouvez utiliser cet élément ou hello dépendances de toospecify dependsOn élément, mais vous n’avez pas besoin de toouse à la fois pour hello même ressource dépendante.</span><span class="sxs-lookup"><span data-stu-id="00fbb-140">You can use either this element or hello dependsOn element toospecify dependencies, but you do not need toouse both for hello same dependent resource.</span></span> <span data-ttu-id="00fbb-141">Si possible, utilisez un tooavoid de référence implicite Ajout d’une dépendance inutile.</span><span class="sxs-lookup"><span data-stu-id="00fbb-141">Whenever possible, use an implicit reference tooavoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="00fbb-142">toolearn, voir [font référence à fonction](resource-group-template-functions-resource.md#reference).</span><span class="sxs-lookup"><span data-stu-id="00fbb-142">toolearn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="00fbb-143">Recommandations pour la définition des dépendances</span><span class="sxs-lookup"><span data-stu-id="00fbb-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="00fbb-144">Lorsque vous décidez quelles tooset de dépendances, utilisez hello instructions :</span><span class="sxs-lookup"><span data-stu-id="00fbb-144">When deciding what dependencies tooset, use hello following guidelines:</span></span>

* <span data-ttu-id="00fbb-145">Définissez le moins de dépendances possible.</span><span class="sxs-lookup"><span data-stu-id="00fbb-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="00fbb-146">Définissez une ressource enfant comme dépendante de sa ressource parent.</span><span class="sxs-lookup"><span data-stu-id="00fbb-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="00fbb-147">Hello d’utilisation **référence** tooset des dépendances implicite entre les ressources qui doivent tooshare une propriété de fonction.</span><span class="sxs-lookup"><span data-stu-id="00fbb-147">Use hello **reference** function tooset implicit dependencies between resources that need tooshare a property.</span></span> <span data-ttu-id="00fbb-148">N’ajoutez pas de dépendance explicite (**dependsOn**) lorsque vous avez déjà défini une dépendance implicite.</span><span class="sxs-lookup"><span data-stu-id="00fbb-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="00fbb-149">Cette approche réduit le risque de hello d’avoir des dépendances inutiles.</span><span class="sxs-lookup"><span data-stu-id="00fbb-149">This approach reduces hello risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="00fbb-150">Définissez une dépendance lorsqu’une ressource ne peut pas être **créée** sans la fonctionnalité d’une autre ressource.</span><span class="sxs-lookup"><span data-stu-id="00fbb-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="00fbb-151">Ne définissez pas une dépendance si les ressources hello interagissent uniquement après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="00fbb-151">Do not set a dependency if hello resources only interact after deployment.</span></span>
* <span data-ttu-id="00fbb-152">Ajoutez les dépendances l’une après l’autre sans les définir explicitement.</span><span class="sxs-lookup"><span data-stu-id="00fbb-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="00fbb-153">Par exemple, votre machine virtuelle dépend d’une interface réseau virtuelle et interface de réseau virtuel hello dépend d’un réseau virtuel et les adresses IP publiques.</span><span class="sxs-lookup"><span data-stu-id="00fbb-153">For example, your virtual machine depends on a virtual network interface, and hello virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="00fbb-154">Par conséquent, hello est ressources une fois toutes les trois déployées, mais ne définissez pas explicitement de machine virtuelle de hello comme dépend de toutes les ressources de trois.</span><span class="sxs-lookup"><span data-stu-id="00fbb-154">Therefore, hello virtual machine is deployed after all three resources, but do not explicitly set hello virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="00fbb-155">Cette approche précise l’ordre des dépendances hello et rend plus facile modèle de hello toochange plus tard.</span><span class="sxs-lookup"><span data-stu-id="00fbb-155">This approach clarifies hello dependency order and makes it easier toochange hello template later.</span></span>
* <span data-ttu-id="00fbb-156">Si une valeur peut être déterminée avant le déploiement, essayez de déployer des ressources hello sans une dépendance.</span><span class="sxs-lookup"><span data-stu-id="00fbb-156">If a value can be determined before deployment, try deploying hello resource without a dependency.</span></span> <span data-ttu-id="00fbb-157">Par exemple, si une valeur de configuration doit nom hello d’une autre ressource, vous devrez peut-être pas une dépendance.</span><span class="sxs-lookup"><span data-stu-id="00fbb-157">For example, if a configuration value needs hello name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="00fbb-158">Ce guide ne fonctionne pas toujours, car certaines ressources vérifient l’existence de hello Hello autre ressource.</span><span class="sxs-lookup"><span data-stu-id="00fbb-158">This guidance does not always work because some resources verify hello existence of hello other resource.</span></span> <span data-ttu-id="00fbb-159">Si vous recevez une erreur, ajoutez une dépendance.</span><span class="sxs-lookup"><span data-stu-id="00fbb-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="00fbb-160">Resource Manager identifie les dépendances circulaires lors de la validation du modèle.</span><span class="sxs-lookup"><span data-stu-id="00fbb-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="00fbb-161">Si vous recevez un message d’erreur indiquant qu’il existe une dépendance circulaire, évaluez vos toosee modèle si toutes les dépendances ne sont pas nécessaires et peuvent être supprimés.</span><span class="sxs-lookup"><span data-stu-id="00fbb-161">If you receive an error stating that a circular dependency exists, evaluate your template toosee if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="00fbb-162">Si la suppression de dépendances ne fonctionne pas, vous pouvez éviter les dépendances circulaires en déplaçant certaines opérations de déploiement dans les ressources enfants qui sont déployés après ressources hello qui ont une dépendance circulaire hello.</span><span class="sxs-lookup"><span data-stu-id="00fbb-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after hello resources that have hello circular dependency.</span></span> <span data-ttu-id="00fbb-163">Par exemple, supposons que vous déployez deux machines virtuelles, mais vous devez définir des propriétés sur chacun d’eux qui font référence toohello autres.</span><span class="sxs-lookup"><span data-stu-id="00fbb-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="00fbb-164">Vous pouvez les déployer dans hello suivant l’ordre :</span><span class="sxs-lookup"><span data-stu-id="00fbb-164">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="00fbb-165">Machine virtuelle 1</span><span class="sxs-lookup"><span data-stu-id="00fbb-165">vm1</span></span>
2. <span data-ttu-id="00fbb-166">Machine virtuelle 2</span><span class="sxs-lookup"><span data-stu-id="00fbb-166">vm2</span></span>
3. <span data-ttu-id="00fbb-167">L’extension sur la machine virtuelle 1 dépend des machines virtuelles 1 et 2.</span><span class="sxs-lookup"><span data-stu-id="00fbb-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="00fbb-168">extension de Hello définit des valeurs sur vm1 qu’il obtient à partir de l’ordinateur virtuel 2.</span><span class="sxs-lookup"><span data-stu-id="00fbb-168">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="00fbb-169">L’extension sur la machine virtuelle 2 dépend des machines virtuelles 1 et 2.</span><span class="sxs-lookup"><span data-stu-id="00fbb-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="00fbb-170">extension de Hello définit des valeurs sur vm2 qu’il obtient de vm1.</span><span class="sxs-lookup"><span data-stu-id="00fbb-170">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="00fbb-171">Pour plus d’informations sur l’évaluation d’ordre de déploiement hello et la résolution des erreurs de dépendance, consultez [résoudre les erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="00fbb-171">For information about assessing hello deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="00fbb-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="00fbb-172">Next steps</span></span>
* <span data-ttu-id="00fbb-173">toolearn sur la résolution des dépendances au cours du déploiement, consultez [résoudre les erreurs courantes de déploiement Azure avec Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="00fbb-173">toolearn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="00fbb-174">toolearn sur la création de modèles Azure Resource Manager, consultez [création de modèles](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="00fbb-174">toolearn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="00fbb-175">Pour obtenir la liste des fonctions disponibles de hello dans un modèle, consultez [fonctions de modèle](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="00fbb-175">For a list of hello available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

