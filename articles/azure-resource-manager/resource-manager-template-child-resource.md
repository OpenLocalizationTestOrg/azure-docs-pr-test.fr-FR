---
title: "Définir des ressources enfant dans un modèle Azure | Microsoft Docs"
description: "Explique comment définir le type et le nom d’une ressource enfant dans un modèle Azure Resource Manager"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: 5b6ce5526f354008eb4a697deec737876f22391f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="18209-103">Définir le nom et le type d’une ressource enfant dans un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="18209-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="18209-104">Quand vous créez un modèle, vous devez souvent inclure une ressource enfant liée à une ressource parent.</span><span class="sxs-lookup"><span data-stu-id="18209-104">When creating a template, you frequently need to include a child resource that is related to a parent resource.</span></span> <span data-ttu-id="18209-105">Par exemple, votre modèle peut inclure un serveur SQL et une base de données.</span><span class="sxs-lookup"><span data-stu-id="18209-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="18209-106">Le serveur SQL est la ressource parent, tandis que la base de données est la ressource enfant.</span><span class="sxs-lookup"><span data-stu-id="18209-106">The SQL server is the parent resource, and the database is the child resource.</span></span> 

<span data-ttu-id="18209-107">Le format du type de la ressource enfant est : `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="18209-107">The format of the child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="18209-108">Le format du nom de la ressource enfant est : `{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="18209-108">The format of the child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="18209-109">Toutefois, vous spécifiez le type et le nom d’un modèle différemment selon qu’il est imbriqué au sein de la ressource parent, ou indépendant au niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="18209-109">However, you specify the type and name in a template differently based on whether it is nested within the parent resource, or on its own at the top level.</span></span> <span data-ttu-id="18209-110">Cette rubrique explique comment gérer les deux approches.</span><span class="sxs-lookup"><span data-stu-id="18209-110">This topic shows how to handle both approaches.</span></span>

<span data-ttu-id="18209-111">Lors de la création d’une référence complète à une ressource, l’ordre utilisé pour combiner les segments de type et de nom n’est pas une simple concaténation des deux.</span><span class="sxs-lookup"><span data-stu-id="18209-111">When constructing a fully qualified reference to a resource, the order to combine segments from the type and name  is not simply a concatenation of the two.</span></span>  <span data-ttu-id="18209-112">Au lieu de cela, utilisez après l’espace de noms une séquence de paires *type/nom* du moins spécifique au plus spécifique :</span><span class="sxs-lookup"><span data-stu-id="18209-112">Instead, after the namespace, use a sequence of *type/name* pairs from least specific to most specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="18209-113">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="18209-113">For example:</span></span>

<span data-ttu-id="18209-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` est correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` n’est pas correct</span><span class="sxs-lookup"><span data-stu-id="18209-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="18209-115">Ressource enfant imbriquée</span><span class="sxs-lookup"><span data-stu-id="18209-115">Nested child resource</span></span>
<span data-ttu-id="18209-116">Pour définir une ressource enfant, la méthode la plus simple consiste à l’imbriquer dans la ressource parent.</span><span class="sxs-lookup"><span data-stu-id="18209-116">The easiest way to define a child resource is to nest it within the parent resource.</span></span> <span data-ttu-id="18209-117">L’exemple suivant montre une base de données SQL imbriquée dans un serveur SQL.</span><span class="sxs-lookup"><span data-stu-id="18209-117">The following example shows a SQL database nested within in a SQL Server.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

<span data-ttu-id="18209-118">Pour la ressource enfant, le type est défini sur `databases`, mais son type de ressource complet est `Microsoft.Sql/servers/databases`.</span><span class="sxs-lookup"><span data-stu-id="18209-118">For the child resource, the type is set to `databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="18209-119">Vous ne fournissez pas `Microsoft.Sql/servers/`, car il est déduit à partir du type de ressource parent.</span><span class="sxs-lookup"><span data-stu-id="18209-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from the parent resource type.</span></span> <span data-ttu-id="18209-120">Le nom de la ressource enfant est défini sur `exampledatabase`, mais le nom complet inclut le nom parent.</span><span class="sxs-lookup"><span data-stu-id="18209-120">The child resource name is set to `exampledatabase` but the full name includes the parent name.</span></span> <span data-ttu-id="18209-121">Vous ne fournissez pas `exampleserver`, car il est déduit à partir de la ressource parent.</span><span class="sxs-lookup"><span data-stu-id="18209-121">You do not provide `exampleserver` because it is assumed from the parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="18209-122">Ressource enfant de niveau supérieur</span><span class="sxs-lookup"><span data-stu-id="18209-122">Top-level child resource</span></span>
<span data-ttu-id="18209-123">Vous pouvez définir la ressource enfant au niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="18209-123">You can define the child resource at the top level.</span></span> <span data-ttu-id="18209-124">Vous pouvez utiliser cette approche si la ressource parent n’est pas déployée dans le même modèle, ou si voulez utiliser `copy` pour créer plusieurs ressources enfant.</span><span class="sxs-lookup"><span data-stu-id="18209-124">You might use this approach if the parent resource is not deployed in the same template, or if want to use `copy` to create multiple child resources.</span></span> <span data-ttu-id="18209-125">Dans le cadre de cette approche, vous devez fournir le type de ressource complet et inclure le nom de la ressource parent dans le nom de la ressource enfant.</span><span class="sxs-lookup"><span data-stu-id="18209-125">With this approach, you must provide the full resource type, and include the parent resource name in the child resource name.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

<span data-ttu-id="18209-126">La base de données est une ressource enfant pour le serveur, même si elle est définie au même niveau dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="18209-126">The database is a child resource to the server even though they are defined on the same level in the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18209-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="18209-127">Next steps</span></span>
* <span data-ttu-id="18209-128">Pour des recommandations sur la création de modèles, consultez [Bonnes pratiques relatives à la création de modèles Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="18209-128">For recommendations about how to create templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="18209-129">Pour obtenir un exemple de création de plusieurs ressources enfant, consultez [Déployer plusieurs instances de ressources dans des modèles Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="18209-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
