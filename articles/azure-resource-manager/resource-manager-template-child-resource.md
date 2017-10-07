---
title: "ressource enfant d’aaaDefine dans le modèle Azure | Documents Microsoft"
description: "Montre comment tooset hello type de ressource et le nom de ressource enfant dans un modèle Azure Resource Manager"
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
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="29bb7-103">Définir le nom et le type d’une ressource enfant dans un modèle Resource Manager</span><span class="sxs-lookup"><span data-stu-id="29bb7-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="29bb7-104">Lorsque vous créez un modèle, vous devez fréquemment tooinclude une ressource enfant qui est la ressource parent de tooa connexes.</span><span class="sxs-lookup"><span data-stu-id="29bb7-104">When creating a template, you frequently need tooinclude a child resource that is related tooa parent resource.</span></span> <span data-ttu-id="29bb7-105">Par exemple, votre modèle peut inclure un serveur SQL et une base de données.</span><span class="sxs-lookup"><span data-stu-id="29bb7-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="29bb7-106">Hello SQL server est ressource parente de hello, et base de données hello ressource enfant de hello.</span><span class="sxs-lookup"><span data-stu-id="29bb7-106">hello SQL server is hello parent resource, and hello database is hello child resource.</span></span> 

<span data-ttu-id="29bb7-107">format Hello hello enfant du type de ressource est :`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="29bb7-107">hello format of hello child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="29bb7-108">format Hello hello enfant du nom de ressource est :`{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="29bb7-108">hello format of hello child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="29bb7-109">Toutefois, vous spécifiez type de hello et le nom d’un modèle différemment en fonction de si elle est imbriquée dans la ressource parent de hello, ou sur sa propre au niveau supérieur de hello.</span><span class="sxs-lookup"><span data-stu-id="29bb7-109">However, you specify hello type and name in a template differently based on whether it is nested within hello parent resource, or on its own at hello top level.</span></span> <span data-ttu-id="29bb7-110">Cette rubrique montre comment toohandle les deux approches.</span><span class="sxs-lookup"><span data-stu-id="29bb7-110">This topic shows how toohandle both approaches.</span></span>

<span data-ttu-id="29bb7-111">Lors de la construction d’une ressource de tooa référence qualifiée complète, les segments de hello ordre toocombine du type de hello et nom n’est pas une simple concaténation de hello deux.</span><span class="sxs-lookup"><span data-stu-id="29bb7-111">When constructing a fully qualified reference tooa resource, hello order toocombine segments from hello type and name  is not simply a concatenation of hello two.</span></span>  <span data-ttu-id="29bb7-112">Au lieu de cela, utilisez une séquence d’après l’espace de noms hello, *type/nom* paires toomost moins spécifique spécifique :</span><span class="sxs-lookup"><span data-stu-id="29bb7-112">Instead, after hello namespace, use a sequence of *type/name* pairs from least specific toomost specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="29bb7-113">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="29bb7-113">For example:</span></span>

<span data-ttu-id="29bb7-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` est correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` n’est pas correct</span><span class="sxs-lookup"><span data-stu-id="29bb7-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="29bb7-115">Ressource enfant imbriquée</span><span class="sxs-lookup"><span data-stu-id="29bb7-115">Nested child resource</span></span>
<span data-ttu-id="29bb7-116">toodefine de façon plus simple Hello une ressource enfant est toonest dans la ressource parent de hello.</span><span class="sxs-lookup"><span data-stu-id="29bb7-116">hello easiest way toodefine a child resource is toonest it within hello parent resource.</span></span> <span data-ttu-id="29bb7-117">Hello suivant montre une base de données SQL imbriqué dans un serveur SQL Server.</span><span class="sxs-lookup"><span data-stu-id="29bb7-117">hello following example shows a SQL database nested within in a SQL Server.</span></span>

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

<span data-ttu-id="29bb7-118">De la ressource enfant hello, hello type a la valeur trop`databases` mais son type de ressource complet est `Microsoft.Sql/servers/databases`.</span><span class="sxs-lookup"><span data-stu-id="29bb7-118">For hello child resource, hello type is set too`databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="29bb7-119">Vous ne fournissez pas `Microsoft.Sql/servers/` , car il est supposé hello parent type de ressource.</span><span class="sxs-lookup"><span data-stu-id="29bb7-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from hello parent resource type.</span></span> <span data-ttu-id="29bb7-120">nom de la ressource enfant Hello est défini trop`exampledatabase` , mais le nom complet de hello inclut hello parent.</span><span class="sxs-lookup"><span data-stu-id="29bb7-120">hello child resource name is set too`exampledatabase` but hello full name includes hello parent name.</span></span> <span data-ttu-id="29bb7-121">Vous ne fournissez pas `exampleserver` , car il est supposé à partir de la ressource parent de hello.</span><span class="sxs-lookup"><span data-stu-id="29bb7-121">You do not provide `exampleserver` because it is assumed from hello parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="29bb7-122">Ressource enfant de niveau supérieur</span><span class="sxs-lookup"><span data-stu-id="29bb7-122">Top-level child resource</span></span>
<span data-ttu-id="29bb7-123">Vous pouvez définir des ressources enfants de hello au niveau supérieur de hello.</span><span class="sxs-lookup"><span data-stu-id="29bb7-123">You can define hello child resource at hello top level.</span></span> <span data-ttu-id="29bb7-124">Vous pouvez utiliser cette approche si la ressource de hello parent n’est pas déployé de hello même modèle ou si voulez toouse `copy` toocreate plusieurs ressources enfants.</span><span class="sxs-lookup"><span data-stu-id="29bb7-124">You might use this approach if hello parent resource is not deployed in hello same template, or if want toouse `copy` toocreate multiple child resources.</span></span> <span data-ttu-id="29bb7-125">Avec cette approche, vous devez fournir le type de ressource complet hello et inclure le nom de la ressource parent hello dans le nom de la ressource enfant hello.</span><span class="sxs-lookup"><span data-stu-id="29bb7-125">With this approach, you must provide hello full resource type, and include hello parent resource name in hello child resource name.</span></span>

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

<span data-ttu-id="29bb7-126">base de données de Hello est un serveur de toohello de ressources enfants, même si elles sont définies sur le même niveau dans le modèle de hello de hello.</span><span class="sxs-lookup"><span data-stu-id="29bb7-126">hello database is a child resource toohello server even though they are defined on hello same level in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29bb7-127">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29bb7-127">Next steps</span></span>
* <span data-ttu-id="29bb7-128">Pour obtenir des recommandations sur la façon toocreate modèles, consultez [meilleures pratiques pour la création de modèles Azure Resource Manager](resource-manager-template-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="29bb7-128">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="29bb7-129">Pour obtenir un exemple de création de plusieurs ressources enfant, consultez [Déployer plusieurs instances de ressources dans des modèles Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="29bb7-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
