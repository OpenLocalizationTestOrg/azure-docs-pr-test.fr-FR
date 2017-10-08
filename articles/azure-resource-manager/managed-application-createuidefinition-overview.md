---
title: "aaaUnderstand création de définition d’interface utilisateur pour les Applications managées Azure | Documents Microsoft"
description: "Décrit comment toocreate les définitions d’interface utilisateur pour les Applications managées Azure"
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
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a><span data-ttu-id="f016d-103">Prise en main de CreateUiDefinition</span><span class="sxs-lookup"><span data-stu-id="f016d-103">Getting started with CreateUiDefinition</span></span>
<span data-ttu-id="f016d-104">Ce document présente les concepts fondamentaux de hello de CreateUiDefinition, ce qui est utilisé par l’interface utilisateur de hello toogenerate portail Azure hello pour la création d’une application managée.</span><span class="sxs-lookup"><span data-stu-id="f016d-104">This document introduces hello core concepts of a CreateUiDefinition, which is used by hello Azure portal toogenerate hello user interface for creating a managed application.</span></span>

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

<span data-ttu-id="f016d-105">Une fonction CreateUiDefinition contient toujours trois propriétés :</span><span class="sxs-lookup"><span data-stu-id="f016d-105">A CreateUiDefinition always contains three properties:</span></span> 

* <span data-ttu-id="f016d-106">handler</span><span class="sxs-lookup"><span data-stu-id="f016d-106">handler</span></span>
* <span data-ttu-id="f016d-107">version</span><span class="sxs-lookup"><span data-stu-id="f016d-107">version</span></span>
* <span data-ttu-id="f016d-108">parameters</span><span class="sxs-lookup"><span data-stu-id="f016d-108">parameters</span></span>

<span data-ttu-id="f016d-109">Pour les applications managées, le gestionnaire doit toujours être `Microsoft.Compute.MultiVm`, et la version de hello plus récentes prises en charge est `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="f016d-109">For managed applications, handler should always be `Microsoft.Compute.MultiVm`, and hello latest supported version is `0.1.2-preview`.</span></span>

<span data-ttu-id="f016d-110">schéma Hello de propriété de paramètres hello dépend de la combinaison de hello du gestionnaire spécifié de hello et version.</span><span class="sxs-lookup"><span data-stu-id="f016d-110">hello schema of hello parameters property depends on hello combination of hello specified handler and version.</span></span> <span data-ttu-id="f016d-111">Pour les applications managées, les propriétés de hello pris en charge sont `basics`, `steps`, et `outputs`.</span><span class="sxs-lookup"><span data-stu-id="f016d-111">For managed applications, hello supported properties are `basics`, `steps`, and `outputs`.</span></span> <span data-ttu-id="f016d-112">principes de base et les étapes des propriétés Hello contiennent hello _éléments_ , comme les zones de texte et les menus déroulants - toobe affiché dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f016d-112">hello basics and steps properties contain hello _elements_ - like textboxes and dropdowns - toobe displayed in hello Azure portal.</span></span> <span data-ttu-id="f016d-113">sorties Hello propriété est de valeurs de sortie utilisé toomap hello hello paramètres de toohello spécifié d’éléments de modèle de déploiement d’Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="f016d-113">hello outputs property is used toomap hello output values of hello specified elements toohello parameters of hello Azure Resource Manager deployment template.</span></span>

<span data-ttu-id="f016d-114">L’inclusion de `$schema` est recommandée, mais facultative.</span><span class="sxs-lookup"><span data-stu-id="f016d-114">Including `$schema` is recommended, but optional.</span></span> <span data-ttu-id="f016d-115">Si spécifié, de valeur pour hello `version` doit correspondre à une version hello dans hello `$schema` URI.</span><span class="sxs-lookup"><span data-stu-id="f016d-115">If specified, hello value for `version` must match hello version within hello `$schema` URI.</span></span>

## <a name="basics"></a><span data-ttu-id="f016d-116">Concepts de base</span><span class="sxs-lookup"><span data-stu-id="f016d-116">Basics</span></span>
<span data-ttu-id="f016d-117">Hello notions de base étape est toujours hello première étape de l’Assistant hello généré lorsque hello portail Azure traite une CreateUiDefinition.</span><span class="sxs-lookup"><span data-stu-id="f016d-117">hello Basics step is always hello first step of hello wizard generated when hello Azure portal parses a CreateUiDefinition.</span></span> <span data-ttu-id="f016d-118">En outre les éléments de hello toodisplaying spécifié dans `basics`, portail de hello injecte des éléments pour l’abonnement de hello toochoose les utilisateurs, de groupe de ressources et d’emplacement pour le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="f016d-118">In addition toodisplaying hello elements specified in `basics`, hello portal injects elements for users toochoose hello subscription, resource group, and location for hello deployment.</span></span> <span data-ttu-id="f016d-119">En règle générale, il est recommandé d’utiliser des éléments de requête pour les paramètres de déploiement à l’échelle, comme nom hello d’informations d’identification administrateur ou de cluster, dans cette étape.</span><span class="sxs-lookup"><span data-stu-id="f016d-119">Generally, elements that query for deployment-wide parameters, like hello name of a cluster or administrator credentials, should go in this step.</span></span>

<span data-ttu-id="f016d-120">Si le comportement d’un élément dépend de l’utilisateur hello abonnement, groupe de ressources ou l’emplacement, cet élément ne peut pas être utilisé dans les concepts de base.</span><span class="sxs-lookup"><span data-stu-id="f016d-120">If an element's behavior depends on hello user's subscription, resource group, or location, then that element can't be used in basics.</span></span> <span data-ttu-id="f016d-121">Par exemple, **Microsoft.Compute.SizeSelector** dépend d’abonnement et l’emplacement toodetermine hello liste l’utilisateur hello des tailles disponibles.</span><span class="sxs-lookup"><span data-stu-id="f016d-121">For example, **Microsoft.Compute.SizeSelector** depends on hello user's subscription and location toodetermine hello list of available sizes.</span></span> <span data-ttu-id="f016d-122">Par conséquent, **Microsoft.Compute.SizeSelector** ne peut être utilisé que dans steps.</span><span class="sxs-lookup"><span data-stu-id="f016d-122">Therefore, **Microsoft.Compute.SizeSelector** can only be used in steps.</span></span> <span data-ttu-id="f016d-123">En général, seuls les éléments Bonjour **Microsoft.Common** espace de noms peut être utilisé dans les concepts de base.</span><span class="sxs-lookup"><span data-stu-id="f016d-123">Generally, only elements in hello **Microsoft.Common** namespace can be used in basics.</span></span> <span data-ttu-id="f016d-124">Bien que certains éléments dans les autres espaces de noms (comme **Microsoft.Compute.Credentials**) qui ne dépendent pas hello contexte de l’utilisateur, sont toujours autorisés.</span><span class="sxs-lookup"><span data-stu-id="f016d-124">Although some elements in other namespaces (like **Microsoft.Compute.Credentials**) that don't depend on hello user's context, are still allowed.</span></span>

## <a name="steps"></a><span data-ttu-id="f016d-125">Étapes</span><span class="sxs-lookup"><span data-stu-id="f016d-125">Steps</span></span>
<span data-ttu-id="f016d-126">propriété d’étapes Hello peut contenir zéro ou plusieurs toodisplay d’étapes supplémentaires après les principes de base, chacun contenant un ou plusieurs éléments.</span><span class="sxs-lookup"><span data-stu-id="f016d-126">hello steps property can contain zero or more additional steps toodisplay after basics, each of which contains one or more elements.</span></span> <span data-ttu-id="f016d-127">Envisagez d’ajouter des étapes par rôle ou de la couche d’application hello en cours de déploiement.</span><span class="sxs-lookup"><span data-stu-id="f016d-127">Consider adding steps per role or tier of hello application being deployed.</span></span> <span data-ttu-id="f016d-128">Par exemple, ajoutez une étape pour les entrées pour les nœuds principaux hello et qu’une étape pour les nœuds de travail hello dans un cluster.</span><span class="sxs-lookup"><span data-stu-id="f016d-128">For example, add a step for inputs for hello master nodes, and a step for hello worker nodes in a cluster.</span></span>

## <a name="outputs"></a><span data-ttu-id="f016d-129">outputs</span><span class="sxs-lookup"><span data-stu-id="f016d-129">Outputs</span></span>
<span data-ttu-id="f016d-130">portail Azure Hello utilise hello `outputs` éléments toomap de propriété à partir de `basics` et `steps` toohello les paramètres de modèle de déploiement d’Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="f016d-130">hello Azure portal uses hello `outputs` property toomap elements from `basics` and `steps` toohello parameters of hello Azure Resource Manager deployment template.</span></span> <span data-ttu-id="f016d-131">clés de Hello de ce dictionnaire sont les noms de hello hello des paramètres de modèle et les valeurs hello sont des propriétés hello d’objets de sortie à partir d’éléments de hello référencé.</span><span class="sxs-lookup"><span data-stu-id="f016d-131">hello keys of this dictionary are hello names of hello template parameters, and hello values are properties of hello output objects from hello referenced elements.</span></span>

## <a name="functions"></a><span data-ttu-id="f016d-132">Fonctions</span><span class="sxs-lookup"><span data-stu-id="f016d-132">Functions</span></span>
<span data-ttu-id="f016d-133">Similaire trop[fonctions de modèle](resource-group-template-functions.md) dans Azure Resource Manager (à la fois dans la syntaxe et des fonctionnalités), CreateUiDefinition fournit des fonctions pour travailler avec les des éléments entrées et sorties, ainsi que des fonctionnalités telles que des instructions conditionnelles.</span><span class="sxs-lookup"><span data-stu-id="f016d-133">Similar too[template functions](resource-group-template-functions.md) in Azure Resource Manager (both in syntax and functionality), CreateUiDefinition provides functions for working with elements' inputs and outputs, as well as features such as conditionals.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f016d-134">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f016d-134">Next steps</span></span>
<span data-ttu-id="f016d-135">CreateUiDefinition elle-même dispose d’un schéma simple.</span><span class="sxs-lookup"><span data-stu-id="f016d-135">CreateUiDefinition itself has a simple schema.</span></span> <span data-ttu-id="f016d-136">profondeur de réel Hello de celui-ci proviennent de toutes les fonctions, le hello suivant des documents décrivent en détail merveilleuse et les éléments de hello pris en charge :</span><span class="sxs-lookup"><span data-stu-id="f016d-136">hello real depth of it comes from all hello supported elements and functions, which hello following documents describe in wondrous detail:</span></span>

- [<span data-ttu-id="f016d-137">Éléments</span><span class="sxs-lookup"><span data-stu-id="f016d-137">Elements</span></span>](managed-application-createuidefinition-elements.md)
- [<span data-ttu-id="f016d-138">Fonctions</span><span class="sxs-lookup"><span data-stu-id="f016d-138">Functions</span></span>](managed-application-createuidefinition-functions.md)

<span data-ttu-id="f016d-139">Un schéma JSON actuel pour CreateUiDefinition est disponible ici : https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span><span class="sxs-lookup"><span data-stu-id="f016d-139">A current JSON schema for CreateUiDefinition is available here: https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json.</span></span> 

<span data-ttu-id="f016d-140">Les versions ultérieures seront disponibles sur hello même emplacement.</span><span class="sxs-lookup"><span data-stu-id="f016d-140">Later versions will be available at hello same location.</span></span> <span data-ttu-id="f016d-141">Remplacez hello `0.1.2-preview` partie de l’URL de hello et hello `version` valeur avec l’identificateur de version hello vous avez l’intention de toouse.</span><span class="sxs-lookup"><span data-stu-id="f016d-141">Replace hello `0.1.2-preview` portion of hello URL and hello `version` value with hello version identifier you intend toouse.</span></span> <span data-ttu-id="f016d-142">les identificateurs de version Hello actuellement pris en charge sont `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, et `0.1.2-preview`.</span><span class="sxs-lookup"><span data-stu-id="f016d-142">hello currently supported version identifiers are `0.0.1-preview`, `0.1.0-preview`, `0.1.1-preview`, and `0.1.2-preview`.</span></span>
