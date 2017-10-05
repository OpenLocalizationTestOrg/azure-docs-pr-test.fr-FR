---
title: "Comprendre la création de la définition de l’interface utilisateur pour des applications gérées Azure | Microsoft Docs"
description: "Décrit comment créer des définitions d’interface utilisateur pour des applications gérées Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 176b891538f85c5638a2321561c3d8bd377d245b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="f6f9e-103">Prise en main de CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="f6f9e-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="f6f9e-104">Ce document présente les principaux concepts d’une fonction CreateUiDefinition, utilisée par le portail Azure afin de générer l’interface utilisateur pour la création d’une application gérée.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-104">This document introduces the core concepts of a CreateUiDefinition, which is used by the Azure portal to generate the user interface for creating a managed application.</span></span>

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

<span data-ttu-id="f6f9e-105">Une fonction CreateUiDefinition contient toujours trois propriétés :</span><span class="sxs-lookup"><span data-stu-id="f6f9e-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="f6f9e-106">handler</span><span class="sxs-lookup"><span data-stu-id="f6f9e-106">handler</span></span>
* <span data-ttu-id="f6f9e-107">version</span><span class="sxs-lookup"><span data-stu-id="f6f9e-107">version</span></span>
* <span data-ttu-id="f6f9e-108">parameters</span><span class="sxs-lookup"><span data-stu-id="f6f9e-108">parameters</span></span>

<span data-ttu-id="f6f9e-109">Pour les applications gérées, le gestionnaire doit toujours être `Microsoft.Compute.MultiVm`, et la version la plus récente `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and the latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="f6f9e-110">Le schéma de la propriété des paramètres dépend de la version et du gestionnaire spécifiés.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-110">The schema of the parameters property depends on the combination of the specified handler and version.</span></span> <span data-ttu-id="f6f9e-111">Pour les applications gérées, les propriétés prises en charge sont `basics`, `steps`, et `outputs`.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-111">For managed applications, the supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="f6f9e-112">Les propriétés basics et steps contiennent des _éléments_, comme des zones de texte et des listes déroulantes, à afficher dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-112">The basics and steps properties contain the _elements_ - like textboxes and dropdowns - to be displayed in the Azure portal.</span></span> <span data-ttu-id="f6f9e-113">La propriété outputs est utilisée pour mettre en correspondance les valeurs de sortie des éléments spécifiés avec les paramètres du modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-113">The outputs property is used to map the output values of the specified elements to the parameters of the Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="f6f9e-114">L’inclusion de `$schema` est recommandée, mais facultative.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="f6f9e-115">Si la valeur de `version` est spécifiée, celle-ci doit correspondre à la version figurant dans l’`$schema` URI.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-115">If specified, the value for `version` must match the version within the `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="f6f9e-116">Concepts de base</span><span class="sxs-lookup"><span data-stu-id="f6f9e-116">Basics</span></span>
<span data-ttu-id="f6f9e-117">L’étape relative aux principes de base est toujours la première étape de l’Assistant générée lors de l’analyse d’une fonction CreateUiDefinition par le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-117">The Basics step is always the first step of the wizard generated when the Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="f6f9e-118">Outre le fait d’afficher des éléments spécifiés dans `basics`, le portail injecte des éléments permettant aux utilisateurs de choisir l’abonnement, le groupe de ressources et l’emplacement du déploiement.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-118">In addition to displaying the elements specified in `basics`, the portal injects elements for users to choose the subscription, resource group, and location for the deployment.</span></span> <span data-ttu-id="f6f9e-119">En règle générale, les éléments demandant des paramètres concernant le déploiement, comme le nom d’un cluster ou des informations d’identification administrateur, doivent figurer dans cette étape.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-119">Generally, elements that query for deployment-wide parameters, like the name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="f6f9e-120">Si le comportement d’un élément dépend de l’abonnement de l’utilisateur, du groupe de ressources ou de l’emplacement, cet élément ne peut pas être utilisé dans les principes de base.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-120">If an element's behavior depends on the user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="f6f9e-121">Par exemple, **Microsoft.Compute.SizeSelector** dépend de l’abonnement et de l’emplacement de l’utilisateur pour déterminer la liste des tailles disponibles.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-121">For example, **Microsoft.Compute.SizeSelector** depends on the user's subscription and location to determine the list of available sizes.</span></span> <span data-ttu-id="f6f9e-122">Par conséquent, **Microsoft.Compute.SizeSelector** ne peut être utilisé que dans steps.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="f6f9e-123">En règle générale, seuls les éléments de l’espace de noms **Microsoft.Common** peuvent être utilisés dans basics.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-123">Generally, only elements in the **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="f6f9e-124">Cependant, certains éléments dans d’autres espaces de noms (comme **Microsoft.Compute.Credentials**) qui ne dépendent pas du contexte de l’utilisateur, sont toujours autorisés.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on the user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="f6f9e-125">Étapes</span><span class="sxs-lookup"><span data-stu-id="f6f9e-125">Steps</span></span>
<span data-ttu-id="f6f9e-126">La propriété steps peut contenir zéro ou plusieurs des étapes supplémentaires à afficher après les principes de base, chacun contenant un ou plusieurs éléments.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-126">The steps property can contain zero or more additional steps to display after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="f6f9e-127">Vous pouvez ajouter des étapes par rôle ou niveau de l’application déployée.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-127">Consider adding steps per role or tier of the application being deployed.</span></span> <span data-ttu-id="f6f9e-128">Par exemple, ajoutez une étape pour les entrées destinées aux nœuds principaux et une étape pour les nœuds de travail à un cluster.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-128">For example, add a step for inputs for the master nodes, and a step for the worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="f6f9e-129">Outputs</span><span class="sxs-lookup"><span data-stu-id="f6f9e-129">Outputs</span></span>
<span data-ttu-id="f6f9e-130">Le portail Azure utilise la propriété `outputs` pour mettre en correspondance des éléments issus de `basics` et `steps` avec les paramètres du modèle de déploiement Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-130">The Azure portal uses the `outputs` property to map elements from `basics` and `steps` to the parameters of the Azure Resource Manager deployment template.</span></span> <span data-ttu-id="f6f9e-131">Les clés de ce dictionnaire sont les noms des paramètres du modèle et les valeurs sont les propriétés des objets de sortie issues des éléments référencés.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-131">The keys of this dictionary are the names of the template parameters, and the values are properties of the output objects from the referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="f6f9e-132">Fonctions</span><span class="sxs-lookup"><span data-stu-id="f6f9e-132">Functions</span></span>
<span data-ttu-id="f6f9e-133">Semblable aux [fonctions de modèle](resource-group-template-functions.md) dans Azure Resource Manager (à la fois en termes de syntaxe et de fonctionnalité), CreateUiDefinition propose des fonctions permettant de travailler avec les entrées et sorties des éléments, ainsi que des fonctions, telles que des logiques conditionnelles.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-133">Similar to [template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6f9e-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f6f9e-134">Next steps</span></span>
<span data-ttu-id="f6f9e-135">CreateUiDefinition elle-même dispose d’un schéma simple.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="f6f9e-136">Sa profondeur réelle provient de l’ensemble des éléments et fonctions pris en charge décrits en détail dans les documents suivants :</span><span class="sxs-lookup"><span data-stu-id="f6f9e-136">The real depth of it comes from all the supported elements and functions, which the following documents describe in wondrous detail:</span></span>

- [<span data-ttu-id="f6f9e-137">Éléments</span><span class="sxs-lookup"><span data-stu-id="f6f9e-137">Elements</span></span>](managed-application-createuidefinition-elements.md)
- [<span data-ttu-id="f6f9e-138">Fonctions</span><span class="sxs-lookup"><span data-stu-id="f6f9e-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="f6f9e-139">Un schéma JSON actuel pour CreateUiDefinition est disponible ici : https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="f6f9e-140">Les versions ultérieures seront disponibles au même emplacement.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-140">Later versions will be available at the same location.</span></span> <span data-ttu-id="f6f9e-141">Remplacez la partie `0.1.2-preview` de l’URL et la valeur `version` par l’identificateur de version que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-141">Replace the `0.1.2-preview` portion of the URL and the `version` value with the version identifier you intend to use.</span></span> <span data-ttu-id="f6f9e-142">Les identificateurs de version actuellement prise en charge sont `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, et `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="f6f9e-142">The currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>