---
title: "aaaResource fonctions de modèle Manager | Documents Microsoft"
description: "Décrit les hello fonctions toouse une valeurs tooretrieve du modèle Azure Resource Manager, travailler avec des chaînes et des valeurs numériques et récupérer des informations de déploiement."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 0644abe1-abaa-443d-820d-1966d7d26bfd
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: tomfitz
ms.openlocfilehash: d1b2e68a33d75058f83d6972dadb33a6390d49b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-functions"></a><span data-ttu-id="072fb-103">Fonctions des modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="072fb-103">Azure Resource Manager template functions</span></span>
<span data-ttu-id="072fb-104">Cette rubrique décrit toutes les fonctions hello que vous pouvez utiliser dans un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="072fb-104">This topic describes all hello functions you can use in an Azure Resource Manager template.</span></span>

<span data-ttu-id="072fb-105">Vous ajoutez des fonctions dans vos modèles en les plaçant entre crochets : `[` et `]`, respectivement.</span><span class="sxs-lookup"><span data-stu-id="072fb-105">You add functions in your templates by enclosing them within brackets: `[` and `]`, respectively.</span></span> <span data-ttu-id="072fb-106">expression de Hello est évaluée lors du déploiement.</span><span class="sxs-lookup"><span data-stu-id="072fb-106">hello expression is evaluated during deployment.</span></span> <span data-ttu-id="072fb-107">Écrite sous la forme d’un littéral de chaîne, résultat hello de l’évaluation d’expression de hello sont d’un autre type JSON, tel qu’un tableau, un objet ou un entier.</span><span class="sxs-lookup"><span data-stu-id="072fb-107">While written as a string literal, hello result of evaluating hello expression can be of a different JSON type, such as an array, object, or integer.</span></span> <span data-ttu-id="072fb-108">Comme en JavaScript, les appels de fonction sont formatés comme suit : `functionName(arg1,arg2,arg3)`.</span><span class="sxs-lookup"><span data-stu-id="072fb-108">Just like in JavaScript, function calls are formatted as `functionName(arg1,arg2,arg3)`.</span></span> <span data-ttu-id="072fb-109">Référencer des propriétés en utilisant des opérateurs de point et [index] hello.</span><span class="sxs-lookup"><span data-stu-id="072fb-109">You reference properties by using hello dot and [index] operators.</span></span>

<span data-ttu-id="072fb-110">Une expression de modèle ne peut pas dépasser 24 576 caractères.</span><span class="sxs-lookup"><span data-stu-id="072fb-110">A template expression cannot exceed 24,576 characters.</span></span>

<span data-ttu-id="072fb-111">Les fonctions des modèles et leurs paramètres ne respectent pas la casse.</span><span class="sxs-lookup"><span data-stu-id="072fb-111">Template functions and their parameters are case-insensitive.</span></span> <span data-ttu-id="072fb-112">Par exemple, le Gestionnaire de ressources résout **variables('var1')** et **VARIABLES('VAR1')** comme hello identiques.</span><span class="sxs-lookup"><span data-stu-id="072fb-112">For example, Resource Manager resolves **variables('var1')** and **VARIABLES('VAR1')** as hello same.</span></span> <span data-ttu-id="072fb-113">Lors de l’évaluation, à moins que la fonction hello modifie expressément cas (par exemple, toUpper ou toLower), fonction hello préserve la casse de hello.</span><span class="sxs-lookup"><span data-stu-id="072fb-113">When evaluated, unless hello function expressly modifies case (such as toUpper or toLower), hello function preserves hello case.</span></span> <span data-ttu-id="072fb-114">Certains types de ressources peuvent avoir des exigences de casse, quelle que soit la manière dont les fonctions sont évaluées.</span><span class="sxs-lookup"><span data-stu-id="072fb-114">Certain resource types may have case requirements irrespective of how functions are evaluated.</span></span>

<a id="array" />
<a id="coalesce" />
<a id="concatarray" />
<a id="contains" />
<a id="createarray" />
<a id="empty" />
<a id="first" />
<a id="intersection" />
<a id="last" />
<a id="length" />
<a id="min" />
<a id="max" />
<a id="range" />
<a id="skip" />
<a id="take" />
<a id="union" />

## <a name="array-and-object-functions"></a><span data-ttu-id="072fb-115">Fonctions de tableau et d’objet</span><span class="sxs-lookup"><span data-stu-id="072fb-115">Array and object functions</span></span>
<span data-ttu-id="072fb-116">Resource Manager fournit les fonctions ci-après pour travailler avec des tableaux et des objets.</span><span class="sxs-lookup"><span data-stu-id="072fb-116">Resource Manager provides several functions for working with arrays and objects.</span></span>

* [<span data-ttu-id="072fb-117">array</span><span class="sxs-lookup"><span data-stu-id="072fb-117">array</span></span>](resource-group-template-functions-array.md#array)
* [<span data-ttu-id="072fb-118">coalesce</span><span class="sxs-lookup"><span data-stu-id="072fb-118">coalesce</span></span>](resource-group-template-functions-array.md#coalesce)
* [<span data-ttu-id="072fb-119">concat</span><span class="sxs-lookup"><span data-stu-id="072fb-119">concat</span></span>](resource-group-template-functions-array.md#concat)
* [<span data-ttu-id="072fb-120">contains</span><span class="sxs-lookup"><span data-stu-id="072fb-120">contains</span></span>](resource-group-template-functions-array.md#contains)
* [<span data-ttu-id="072fb-121">createArray</span><span class="sxs-lookup"><span data-stu-id="072fb-121">createArray</span></span>](resource-group-template-functions-array.md#createarray)
* [<span data-ttu-id="072fb-122">empty</span><span class="sxs-lookup"><span data-stu-id="072fb-122">empty</span></span>](resource-group-template-functions-array.md#empty)
* [<span data-ttu-id="072fb-123">first</span><span class="sxs-lookup"><span data-stu-id="072fb-123">first</span></span>](resource-group-template-functions-array.md#first)
* [<span data-ttu-id="072fb-124">intersection</span><span class="sxs-lookup"><span data-stu-id="072fb-124">intersection</span></span>](resource-group-template-functions-array.md#intersection)
* [<span data-ttu-id="072fb-125">json</span><span class="sxs-lookup"><span data-stu-id="072fb-125">json</span></span>](resource-group-template-functions-array.md#json)
* [<span data-ttu-id="072fb-126">last</span><span class="sxs-lookup"><span data-stu-id="072fb-126">last</span></span>](resource-group-template-functions-array.md#last)
* [<span data-ttu-id="072fb-127">length</span><span class="sxs-lookup"><span data-stu-id="072fb-127">length</span></span>](resource-group-template-functions-array.md#length)
* [<span data-ttu-id="072fb-128">min</span><span class="sxs-lookup"><span data-stu-id="072fb-128">min</span></span>](resource-group-template-functions-array.md#min)
* [<span data-ttu-id="072fb-129">max</span><span class="sxs-lookup"><span data-stu-id="072fb-129">max</span></span>](resource-group-template-functions-array.md#max)
* [<span data-ttu-id="072fb-130">range</span><span class="sxs-lookup"><span data-stu-id="072fb-130">range</span></span>](resource-group-template-functions-array.md#range)
* [<span data-ttu-id="072fb-131">skip</span><span class="sxs-lookup"><span data-stu-id="072fb-131">skip</span></span>](resource-group-template-functions-array.md#skip)
* [<span data-ttu-id="072fb-132">take</span><span class="sxs-lookup"><span data-stu-id="072fb-132">take</span></span>](resource-group-template-functions-array.md#take)
* [<span data-ttu-id="072fb-133">union</span><span class="sxs-lookup"><span data-stu-id="072fb-133">union</span></span>](resource-group-template-functions-array.md#union)

<a id="equals" />
<a id="less" />
<a id="lessorequals" />
<a id="greater" />
<a id="greaterorequals" />

## <a name="comparison-functions"></a><span data-ttu-id="072fb-134">Fonctions de comparaison</span><span class="sxs-lookup"><span data-stu-id="072fb-134">Comparison functions</span></span>
<span data-ttu-id="072fb-135">Resource Manager fournit plusieurs fonctions pour effectuer des comparaisons dans vos modèles.</span><span class="sxs-lookup"><span data-stu-id="072fb-135">Resource Manager provides several functions for making comparisons in your templates.</span></span>

* [<span data-ttu-id="072fb-136">equals</span><span class="sxs-lookup"><span data-stu-id="072fb-136">equals</span></span>](resource-group-template-functions-comparison.md#equals)
* [<span data-ttu-id="072fb-137">less</span><span class="sxs-lookup"><span data-stu-id="072fb-137">less</span></span>](resource-group-template-functions-comparison.md#less)
* [<span data-ttu-id="072fb-138">lessOrEquals</span><span class="sxs-lookup"><span data-stu-id="072fb-138">lessOrEquals</span></span>](resource-group-template-functions-comparison.md#lessorequals)
* [<span data-ttu-id="072fb-139">greater</span><span class="sxs-lookup"><span data-stu-id="072fb-139">greater</span></span>](resource-group-template-functions-comparison.md#greater)
* [<span data-ttu-id="072fb-140">greaterOrEquals</span><span class="sxs-lookup"><span data-stu-id="072fb-140">greaterOrEquals</span></span>](resource-group-template-functions-comparison.md#greaterorequals)

<a id="deployment" />
<a id="parameters" />
<a id="variables" />

## <a name="deployment-value-functions"></a><span data-ttu-id="072fb-141">Fonctions de valeur de déploiement</span><span class="sxs-lookup"><span data-stu-id="072fb-141">Deployment value functions</span></span>
<span data-ttu-id="072fb-142">Gestionnaire de ressources fournit suivant de hello fonctionne pour l’obtention des valeurs à partir des sections du modèle de hello et valeurs connexes toohello déploiement :</span><span class="sxs-lookup"><span data-stu-id="072fb-142">Resource Manager provides hello following functions for getting values from sections of hello template and values related toohello deployment:</span></span>

* [<span data-ttu-id="072fb-143">deployment</span><span class="sxs-lookup"><span data-stu-id="072fb-143">deployment</span></span>](resource-group-template-functions-deployment.md#deployment)
* [<span data-ttu-id="072fb-144">parameters</span><span class="sxs-lookup"><span data-stu-id="072fb-144">parameters</span></span>](resource-group-template-functions-deployment.md#parameters)
* [<span data-ttu-id="072fb-145">variables</span><span class="sxs-lookup"><span data-stu-id="072fb-145">variables</span></span>](resource-group-template-functions-deployment.md#variables)

<a id="add" />
<a id="copyindex" />
<a id="div" />
<a id="float" />
<a id="int" />
<a id="minint" />
<a id="maxint" />
<a id="mod" />
<a id="mul" />
<a id="sub" />

## <a name="logical-functions"></a><span data-ttu-id="072fb-146">Fonctions logiques</span><span class="sxs-lookup"><span data-stu-id="072fb-146">Logical functions</span></span>
<span data-ttu-id="072fb-147">Gestionnaire de ressources fournit hello suivant des fonctions pour l’utilisation des conditions logiques :</span><span class="sxs-lookup"><span data-stu-id="072fb-147">Resource Manager provides hello following functions for working with logical conditions:</span></span>

* [<span data-ttu-id="072fb-148">et</span><span class="sxs-lookup"><span data-stu-id="072fb-148">and</span></span>](resource-group-template-functions-logical.md#and)
* [<span data-ttu-id="072fb-149">bool</span><span class="sxs-lookup"><span data-stu-id="072fb-149">bool</span></span>](resource-group-template-functions-logical.md#bool)
* [<span data-ttu-id="072fb-150">si</span><span class="sxs-lookup"><span data-stu-id="072fb-150">if</span></span>](resource-group-template-functions-logical.md#if)
* [<span data-ttu-id="072fb-151">non</span><span class="sxs-lookup"><span data-stu-id="072fb-151">not</span></span>](resource-group-template-functions-logical.md#not)
* [<span data-ttu-id="072fb-152">ou</span><span class="sxs-lookup"><span data-stu-id="072fb-152">or</span></span>](resource-group-template-functions-logical.md#or)

## <a name="numeric-functions"></a><span data-ttu-id="072fb-153">Fonctions numériques</span><span class="sxs-lookup"><span data-stu-id="072fb-153">Numeric functions</span></span>
<span data-ttu-id="072fb-154">Gestionnaire de ressources fournit hello suivant des fonctions permettant de travailler avec des entiers :</span><span class="sxs-lookup"><span data-stu-id="072fb-154">Resource Manager provides hello following functions for working with integers:</span></span>

* [<span data-ttu-id="072fb-155">ajouter</span><span class="sxs-lookup"><span data-stu-id="072fb-155">add</span></span>](resource-group-template-functions-numeric.md#add)
* [<span data-ttu-id="072fb-156">copyIndex</span><span class="sxs-lookup"><span data-stu-id="072fb-156">copyIndex</span></span>](resource-group-template-functions-numeric.md#copyindex)
* [<span data-ttu-id="072fb-157">div</span><span class="sxs-lookup"><span data-stu-id="072fb-157">div</span></span>](resource-group-template-functions-numeric.md#div)
* [<span data-ttu-id="072fb-158">float</span><span class="sxs-lookup"><span data-stu-id="072fb-158">float</span></span>](resource-group-template-functions-numeric.md#float)
* [<span data-ttu-id="072fb-159">int</span><span class="sxs-lookup"><span data-stu-id="072fb-159">int</span></span>](resource-group-template-functions-numeric.md#int)
* [<span data-ttu-id="072fb-160">min</span><span class="sxs-lookup"><span data-stu-id="072fb-160">min</span></span>](resource-group-template-functions-numeric.md#min)
* [<span data-ttu-id="072fb-161">max</span><span class="sxs-lookup"><span data-stu-id="072fb-161">max</span></span>](resource-group-template-functions-numeric.md#max)
* [<span data-ttu-id="072fb-162">mod</span><span class="sxs-lookup"><span data-stu-id="072fb-162">mod</span></span>](resource-group-template-functions-numeric.md#mod)
* [<span data-ttu-id="072fb-163">mul</span><span class="sxs-lookup"><span data-stu-id="072fb-163">mul</span></span>](resource-group-template-functions-numeric.md#mul)
* [<span data-ttu-id="072fb-164">sub</span><span class="sxs-lookup"><span data-stu-id="072fb-164">sub</span></span>](resource-group-template-functions-numeric.md#sub)

<a id="listkeys" />
<a id="list" />
<a id="providers" />
<a id="reference" />
<a id="resourcegroup" />
<a id="resourceid" />
<a id="subscription" />

## <a name="resource-functions"></a><span data-ttu-id="072fb-165">Fonctions de ressource</span><span class="sxs-lookup"><span data-stu-id="072fb-165">Resource functions</span></span>
<span data-ttu-id="072fb-166">Gestionnaire de ressources fournit hello suivant des fonctions pour obtenir des valeurs de ressource :</span><span class="sxs-lookup"><span data-stu-id="072fb-166">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="072fb-167">listKeys and list{Value}</span><span class="sxs-lookup"><span data-stu-id="072fb-167">listKeys and list{Value}</span></span>](resource-group-template-functions-resource.md#listkeys)
* [<span data-ttu-id="072fb-168">fournisseurs</span><span class="sxs-lookup"><span data-stu-id="072fb-168">providers</span></span>](resource-group-template-functions-resource.md#providers)
* [<span data-ttu-id="072fb-169">reference</span><span class="sxs-lookup"><span data-stu-id="072fb-169">reference</span></span>](resource-group-template-functions-resource.md#reference)
* [<span data-ttu-id="072fb-170">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="072fb-170">resourceGroup</span></span>](resource-group-template-functions-resource.md#resourcegroup)
* [<span data-ttu-id="072fb-171">resourceId</span><span class="sxs-lookup"><span data-stu-id="072fb-171">resourceId</span></span>](resource-group-template-functions-resource.md#resourceid)
* [<span data-ttu-id="072fb-172">abonnement</span><span class="sxs-lookup"><span data-stu-id="072fb-172">subscription</span></span>](resource-group-template-functions-resource.md#subscription)

<a id="base64" />
<a id="base64tojson" />
<a id="base64tostring" />
<a id="concat" />
<a id="containsstring" />
<a id="datauri" />
<a id="datauritostring" />
<a id="emptystring" />
<a id="endswith" />
<a id="firststring" />
<a id="indexof" />
<a id="laststring" />
<a id="lastindexof" />
<a id="lengthstring" />
<a id="padleft" />
<a id="replace" />
<a id="skipstring" />
<a id="split" />
<a id="startswith" />
<a id="string" />
<a id="substring" />
<a id="takestring" />
<a id="tolower" />
<a id="toupper" />
<a id="trim" />
<a id="uniquestring" />
<a id="uri" />
<a id="uricomponent" />
<a id="uricomponenttostring" />

## <a name="string-functions"></a><span data-ttu-id="072fb-173">Fonctions de chaîne</span><span class="sxs-lookup"><span data-stu-id="072fb-173">String functions</span></span>
<span data-ttu-id="072fb-174">Gestionnaire de ressources fournit hello suivant des fonctions pour manipuler des chaînes :</span><span class="sxs-lookup"><span data-stu-id="072fb-174">Resource Manager provides hello following functions for working with strings:</span></span>

* [<span data-ttu-id="072fb-175">base64</span><span class="sxs-lookup"><span data-stu-id="072fb-175">base64</span></span>](resource-group-template-functions-string.md#base64)
* [<span data-ttu-id="072fb-176">base64ToJson</span><span class="sxs-lookup"><span data-stu-id="072fb-176">base64ToJson</span></span>](resource-group-template-functions-string.md#base64tojson)
* [<span data-ttu-id="072fb-177">base64ToString</span><span class="sxs-lookup"><span data-stu-id="072fb-177">base64ToString</span></span>](resource-group-template-functions-string.md#base64tostring)
* [<span data-ttu-id="072fb-178">concat</span><span class="sxs-lookup"><span data-stu-id="072fb-178">concat</span></span>](resource-group-template-functions-string.md#concat)
* [<span data-ttu-id="072fb-179">contains</span><span class="sxs-lookup"><span data-stu-id="072fb-179">contains</span></span>](resource-group-template-functions-string.md#contains)
* [<span data-ttu-id="072fb-180">dataUri</span><span class="sxs-lookup"><span data-stu-id="072fb-180">dataUri</span></span>](resource-group-template-functions-string.md#datauri)
* [<span data-ttu-id="072fb-181">dataUriToString</span><span class="sxs-lookup"><span data-stu-id="072fb-181">dataUriToString</span></span>](resource-group-template-functions-string.md#datauritostring)
* [<span data-ttu-id="072fb-182">empty</span><span class="sxs-lookup"><span data-stu-id="072fb-182">empty</span></span>](resource-group-template-functions-string.md#empty)
* [<span data-ttu-id="072fb-183">endsWith</span><span class="sxs-lookup"><span data-stu-id="072fb-183">endsWith</span></span>](resource-group-template-functions-string.md#endswith)
* [<span data-ttu-id="072fb-184">first</span><span class="sxs-lookup"><span data-stu-id="072fb-184">first</span></span>](resource-group-template-functions-string.md#first)
* [<span data-ttu-id="072fb-185">indexOf</span><span class="sxs-lookup"><span data-stu-id="072fb-185">indexOf</span></span>](resource-group-template-functions-string.md#indexof)
* [<span data-ttu-id="072fb-186">last</span><span class="sxs-lookup"><span data-stu-id="072fb-186">last</span></span>](resource-group-template-functions-string.md#last)
* [<span data-ttu-id="072fb-187">lastIndexOf</span><span class="sxs-lookup"><span data-stu-id="072fb-187">lastIndexOf</span></span>](resource-group-template-functions-string.md#lastindexof)
* [<span data-ttu-id="072fb-188">length</span><span class="sxs-lookup"><span data-stu-id="072fb-188">length</span></span>](resource-group-template-functions-string.md#length)
* [<span data-ttu-id="072fb-189">padLeft</span><span class="sxs-lookup"><span data-stu-id="072fb-189">padLeft</span></span>](resource-group-template-functions-string.md#padleft)
* [<span data-ttu-id="072fb-190">replace</span><span class="sxs-lookup"><span data-stu-id="072fb-190">replace</span></span>](resource-group-template-functions-string.md#replace)
* [<span data-ttu-id="072fb-191">skip</span><span class="sxs-lookup"><span data-stu-id="072fb-191">skip</span></span>](resource-group-template-functions-string.md#skip)
* [<span data-ttu-id="072fb-192">split</span><span class="sxs-lookup"><span data-stu-id="072fb-192">split</span></span>](resource-group-template-functions-string.md#split)
* [<span data-ttu-id="072fb-193">startsWith</span><span class="sxs-lookup"><span data-stu-id="072fb-193">startsWith</span></span>](resource-group-template-functions-string.md#startswith)
* [<span data-ttu-id="072fb-194">string</span><span class="sxs-lookup"><span data-stu-id="072fb-194">string</span></span>](resource-group-template-functions-string.md#string)
* [<span data-ttu-id="072fb-195">substring</span><span class="sxs-lookup"><span data-stu-id="072fb-195">substring</span></span>](resource-group-template-functions-string.md#substring)
* [<span data-ttu-id="072fb-196">take</span><span class="sxs-lookup"><span data-stu-id="072fb-196">take</span></span>](resource-group-template-functions-string.md#take)
* [<span data-ttu-id="072fb-197">toLower</span><span class="sxs-lookup"><span data-stu-id="072fb-197">toLower</span></span>](resource-group-template-functions-string.md#tolower)
* [<span data-ttu-id="072fb-198">toUpper</span><span class="sxs-lookup"><span data-stu-id="072fb-198">toUpper</span></span>](resource-group-template-functions-string.md#toupper)
* [<span data-ttu-id="072fb-199">découper</span><span class="sxs-lookup"><span data-stu-id="072fb-199">trim</span></span>](resource-group-template-functions-string.md#trim)
* [<span data-ttu-id="072fb-200">uniqueString</span><span class="sxs-lookup"><span data-stu-id="072fb-200">uniqueString</span></span>](resource-group-template-functions-string.md#uniquestring)
* [<span data-ttu-id="072fb-201">URI</span><span class="sxs-lookup"><span data-stu-id="072fb-201">uri</span></span>](resource-group-template-functions-string.md#uri)
* [<span data-ttu-id="072fb-202">uriComponent</span><span class="sxs-lookup"><span data-stu-id="072fb-202">uriComponent</span></span>](resource-group-template-functions-string.md#uricomponent)
* [<span data-ttu-id="072fb-203">uriComponentToString</span><span class="sxs-lookup"><span data-stu-id="072fb-203">uriComponentToString</span></span>](resource-group-template-functions-string.md#uricomponenttostring)


## <a name="next-steps"></a><span data-ttu-id="072fb-204">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="072fb-204">Next steps</span></span>
* <span data-ttu-id="072fb-205">Pour obtenir une description des sections de hello dans un modèle Azure Resource Manager, consultez [les modèles de programmation Azure Resource Manager](resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="072fb-205">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="072fb-206">consultez de plusieurs modèles toomerge [à l’aide de modèles liés avec Azure Resource Manager](resource-group-linked-templates.md)</span><span class="sxs-lookup"><span data-stu-id="072fb-206">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md)</span></span>
* <span data-ttu-id="072fb-207">tooiterate un nombre spécifié de fois lors de la création d’un type de ressource, consultez [créer plusieurs instances de ressources dans le Gestionnaire de ressources Azure](resource-group-create-multiple.md)</span><span class="sxs-lookup"><span data-stu-id="072fb-207">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md)</span></span>
* <span data-ttu-id="072fb-208">toosee modèle de hello toodeploy que vous avez créé, voir [déployer une application avec le modèle Azure Resource Manager](resource-group-template-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="072fb-208">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md)</span></span>

