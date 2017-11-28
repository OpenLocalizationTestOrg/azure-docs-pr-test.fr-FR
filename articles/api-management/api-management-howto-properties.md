---
title: "Utilisation des propriétés dans les stratégies Gestion des API Azure"
description: "Découvrez comment utiliser les propriétés dans les stratégies Gestion des API Azure."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f39b00f-cf6e-4cef-9bf2-1f89202c0bc0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 3b0fe2a300038e13cc488bdb4f50f8be270ea8f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-properties-in-azure-api-management-policies"></a><span data-ttu-id="c455b-103">Utilisation des propriétés dans les stratégies Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="c455b-103">How to use properties in Azure API Management policies</span></span>
<span data-ttu-id="c455b-104">Les stratégies Gestion des API sont une fonctionnalité puissante du système qui permet à l’éditeur de modifier le comportement de l’API grâce à la configuration.</span><span class="sxs-lookup"><span data-stu-id="c455b-104">API Management policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="c455b-105">Les stratégies sont un ensemble d'instructions qui sont exécutées dans l'ordre sur demande ou sur réponse d'une API.</span><span class="sxs-lookup"><span data-stu-id="c455b-105">Policies are a collection of statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="c455b-106">Les instructions de la stratégie peuvent être construites à l’aide de valeurs de texte littéral, d’expressions de stratégie et de propriétés.</span><span class="sxs-lookup"><span data-stu-id="c455b-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="c455b-107">Chaque instance du service Gestion des API possède une collection de propriétés de paires clé/valeur qui s’appliquent à l’instance de service.</span><span class="sxs-lookup"><span data-stu-id="c455b-107">Each API Management service instance has a properties collection of key/value pairs that are global to the service instance.</span></span> <span data-ttu-id="c455b-108">Ces propriétés peuvent être utilisées pour gérer les valeurs de chaîne constantes dans l’ensemble des stratégies et de la configuration de l’API.</span><span class="sxs-lookup"><span data-stu-id="c455b-108">These properties can be used to manage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="c455b-109">Chaque propriété présente les attributs suivants.</span><span class="sxs-lookup"><span data-stu-id="c455b-109">Each property has the following attributes.</span></span>

| <span data-ttu-id="c455b-110">Attribut</span><span class="sxs-lookup"><span data-stu-id="c455b-110">Attribute</span></span> | <span data-ttu-id="c455b-111">Type</span><span class="sxs-lookup"><span data-stu-id="c455b-111">Type</span></span> | <span data-ttu-id="c455b-112">Description</span><span class="sxs-lookup"><span data-stu-id="c455b-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c455b-113">Name</span><span class="sxs-lookup"><span data-stu-id="c455b-113">Name</span></span> |<span data-ttu-id="c455b-114">string</span><span class="sxs-lookup"><span data-stu-id="c455b-114">string</span></span> |<span data-ttu-id="c455b-115">Le nom de la propriété.</span><span class="sxs-lookup"><span data-stu-id="c455b-115">The name of the property.</span></span> <span data-ttu-id="c455b-116">Il peut contenir uniquement des lettres, des chiffres, des points, des tirets et des caractères de soulignement.</span><span class="sxs-lookup"><span data-stu-id="c455b-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="c455b-117">Valeur</span><span class="sxs-lookup"><span data-stu-id="c455b-117">Value</span></span> |<span data-ttu-id="c455b-118">string</span><span class="sxs-lookup"><span data-stu-id="c455b-118">string</span></span> |<span data-ttu-id="c455b-119">Valeur de la propriété.</span><span class="sxs-lookup"><span data-stu-id="c455b-119">The value of the property.</span></span> <span data-ttu-id="c455b-120">Elle ne peut pas être vide ni se composer uniquement d’espaces blancs.</span><span class="sxs-lookup"><span data-stu-id="c455b-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="c455b-121">Secret</span><span class="sxs-lookup"><span data-stu-id="c455b-121">Secret</span></span> |<span data-ttu-id="c455b-122">booléenne</span><span class="sxs-lookup"><span data-stu-id="c455b-122">boolean</span></span> |<span data-ttu-id="c455b-123">Détermine si la valeur est un secret et doit être chiffrée.</span><span class="sxs-lookup"><span data-stu-id="c455b-123">Determines whether the value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="c455b-124">Balises</span><span class="sxs-lookup"><span data-stu-id="c455b-124">Tags</span></span> |<span data-ttu-id="c455b-125">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="c455b-125">array of string</span></span> |<span data-ttu-id="c455b-126">Balises facultatives qui, lorsqu’elles sont fournies, peuvent être utilisées pour filtrer la liste de propriétés.</span><span class="sxs-lookup"><span data-stu-id="c455b-126">Optional tags that when provided can be used to filter the property list.</span></span> |

<span data-ttu-id="c455b-127">Les propriétés sont configurées dans le portail des éditeurs sous l’onglet **Propriétés** .</span><span class="sxs-lookup"><span data-stu-id="c455b-127">Properties are configured in the publisher portal on the **Properties** tab.</span></span> <span data-ttu-id="c455b-128">Dans l’exemple suivant, trois propriétés sont configurées.</span><span class="sxs-lookup"><span data-stu-id="c455b-128">In the following example, three properties are configured.</span></span>

![Propriétés][api-management-properties]

<span data-ttu-id="c455b-130">Les valeurs de propriété peuvent contenir des chaînes littérales et des [expressions de stratégie](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="c455b-130">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="c455b-131">Le tableau suivant répertorie les trois exemples de propriétés précédents et leurs attributs.</span><span class="sxs-lookup"><span data-stu-id="c455b-131">The following table shows the previous three sample properties and their attributes.</span></span> <span data-ttu-id="c455b-132">La valeur de `ExpressionProperty` est une expression de stratégie qui renvoie une chaîne contenant la date et l’heure actuelles.</span><span class="sxs-lookup"><span data-stu-id="c455b-132">The value of `ExpressionProperty` is a policy expression that returns a string containing the current date and time.</span></span> <span data-ttu-id="c455b-133">La propriété `ContosoHeaderValue` est marquée en tant que secret. Sa valeur ne s’affiche donc pas.</span><span class="sxs-lookup"><span data-stu-id="c455b-133">The property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="c455b-134">Nom</span><span class="sxs-lookup"><span data-stu-id="c455b-134">Name</span></span> | <span data-ttu-id="c455b-135">Valeur</span><span class="sxs-lookup"><span data-stu-id="c455b-135">Value</span></span> | <span data-ttu-id="c455b-136">Secret</span><span class="sxs-lookup"><span data-stu-id="c455b-136">Secret</span></span> | <span data-ttu-id="c455b-137">Balises</span><span class="sxs-lookup"><span data-stu-id="c455b-137">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c455b-138">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="c455b-138">ContosoHeader</span></span> |<span data-ttu-id="c455b-139">TrackingId</span><span class="sxs-lookup"><span data-stu-id="c455b-139">TrackingId</span></span> |<span data-ttu-id="c455b-140">False</span><span class="sxs-lookup"><span data-stu-id="c455b-140">False</span></span> |<span data-ttu-id="c455b-141">Contoso</span><span class="sxs-lookup"><span data-stu-id="c455b-141">Contoso</span></span> |
| <span data-ttu-id="c455b-142">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="c455b-142">ContosoHeaderValue</span></span> |<span data-ttu-id="c455b-143">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="c455b-143">••••••••••••••••••••••</span></span> |<span data-ttu-id="c455b-144">True</span><span class="sxs-lookup"><span data-stu-id="c455b-144">True</span></span> |<span data-ttu-id="c455b-145">Contoso</span><span class="sxs-lookup"><span data-stu-id="c455b-145">Contoso</span></span> |
| <span data-ttu-id="c455b-146">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="c455b-146">ExpressionProperty</span></span> |<span data-ttu-id="c455b-147">@(DateHeure.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="c455b-147">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="c455b-148">False</span><span class="sxs-lookup"><span data-stu-id="c455b-148">False</span></span> | |

## <a name="to-use-a-property"></a><span data-ttu-id="c455b-149">Pour utiliser une propriété</span><span class="sxs-lookup"><span data-stu-id="c455b-149">To use a property</span></span>
<span data-ttu-id="c455b-150">Pour utiliser une propriété dans une stratégie, placez le nom de la propriété dans une paire d’accolades telle que `{{ContosoHeader}}`, comme illustré dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="c455b-150">To use a property in a policy, place the property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in the following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="c455b-151">Dans cet exemple, `ContosoHeader` est utilisé comme nom d’en-tête d’une stratégie `set-header`, et `ContosoHeaderValue` comme valeur de cet en-tête.</span><span class="sxs-lookup"><span data-stu-id="c455b-151">In this example, `ContosoHeader` is used as the name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as the value of that header.</span></span> <span data-ttu-id="c455b-152">Lorsque cette stratégie est évaluée lors d’une demande ou d’une réponse à la passerelle Gestion des API, `{{ContosoHeader}}` et `{{ContosoHeaderValue}}` sont remplacés par leurs valeurs de propriété respectives.</span><span class="sxs-lookup"><span data-stu-id="c455b-152">When this policy is evaluated during a request or response to the API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="c455b-153">Les propriétés peuvent être utilisées en tant qu’attribut complet ou valeurs d’élément, comme indiqué dans l’exemple précédent. Elles peuvent également être insérées dans ou combinés avec une partie d’une expression de texte littéral, comme illustré dans l’exemple suivant : `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="c455b-153">Properties can be used as complete attribute or element values as shown in the previous example, but they can also be inserted into or combined with part of a literal text expression as shown in the following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="c455b-154">Les propriétés peuvent également contenir des expressions de stratégie.</span><span class="sxs-lookup"><span data-stu-id="c455b-154">Properties can also contain policy expressions.</span></span> <span data-ttu-id="c455b-155">Dans l’exemple suivant, `ExpressionProperty` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="c455b-155">In the following example, the `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="c455b-156">Lorsque cette stratégie est évaluée, `{{ExpressionProperty}}` est remplacé par sa valeur : `@(DateTime.Now.ToString())`.</span><span class="sxs-lookup"><span data-stu-id="c455b-156">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="c455b-157">Étant donné que la valeur est une expression de stratégie, l’expression est évaluée et la stratégie poursuit son exécution.</span><span class="sxs-lookup"><span data-stu-id="c455b-157">Since the value is a policy expression, the expression is evaluated and the policy proceeds with its execution.</span></span>

<span data-ttu-id="c455b-158">Vous pouvez tester cette opération dans le portail des développeurs en appelant une opération qui a une stratégie dont l’étendue inclut des propriétés.</span><span class="sxs-lookup"><span data-stu-id="c455b-158">You can test this out in the developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="c455b-159">Dans l’exemple suivant, une opération est appelée avec les deux stratégies `set-header` de l’exemple précédent incluant des propriétés.</span><span class="sxs-lookup"><span data-stu-id="c455b-159">In the following example, an operation is called with the two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="c455b-160">Notez que la réponse contient deux en-têtes personnalisés configurés à l’aide de stratégies et de propriétés.</span><span class="sxs-lookup"><span data-stu-id="c455b-160">Note that the response contains two custom headers that were configured using policies with properties.</span></span>

![Portail des développeurs][api-management-send-results]

<span data-ttu-id="c455b-162">Si vous examinez le [suivi de l’inspecteur d’API](api-management-howto-api-inspector.md) pour un appel qui inclut les deux exemples de stratégies précédents incluant des propriétés, vous pouvez voir les deux stratégies `set-header` avec les valeurs de propriété insérées, ainsi que l’évaluation d’expression de stratégie pour la propriété contenant l’expression de stratégie.</span><span class="sxs-lookup"><span data-stu-id="c455b-162">If you look at the [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes the two previous sample policies with properties, you can see the two `set-header` policies with the property values inserted as well as the policy expression evaluation for the property that contained the policy expression.</span></span>

![Suivi de l’inspecteur d’API][api-management-api-inspector-trace]

<span data-ttu-id="c455b-164">Alors que les valeurs de propriété peuvent contenir des expressions de stratégie, elles ne peuvent pas contenir d’autres propriétés.</span><span class="sxs-lookup"><span data-stu-id="c455b-164">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="c455b-165">Si le texte contenant une référence de propriété est utilisé pour une valeur de propriété, comme `Property value text {{MyProperty}}`, cette référence de propriété n’est pas remplacée et est incluse dans la valeur de propriété.</span><span class="sxs-lookup"><span data-stu-id="c455b-165">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of the property value.</span></span>

## <a name="to-create-a-property"></a><span data-ttu-id="c455b-166">Pour créer une propriété</span><span class="sxs-lookup"><span data-stu-id="c455b-166">To create a property</span></span>
<span data-ttu-id="c455b-167">Pour créer une propriété, cliquez sur **Ajouter une propriété** sous l’onglet **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="c455b-167">To create a property, click **Add property** on the **Properties** tab.</span></span>

![Ajouter une propriété][api-management-properties-add-property-menu]

<span data-ttu-id="c455b-169">**Nom** et **Valeur** doivent être renseignés.</span><span class="sxs-lookup"><span data-stu-id="c455b-169">**Name** and **Value** are required values.</span></span> <span data-ttu-id="c455b-170">Si la valeur de propriété est un secret, cochez la case **Il s’agit d’une clé secrète** .</span><span class="sxs-lookup"><span data-stu-id="c455b-170">If this property value is a secret, check the **This is a secret** checkbox.</span></span> <span data-ttu-id="c455b-171">Entrez une ou plusieurs balises facultatives pour aider à organiser vos propriétés, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c455b-171">Enter one or more optional tags to help with organizing your properties, and click **Save**.</span></span>

![Ajouter une propriété][api-management-properties-add-property]

<span data-ttu-id="c455b-173">Lorsqu’une propriété est enregistrée, la zone de texte **Propriétés de recherche** est remplie avec le nom de la nouvelle propriété et la nouvelle propriété s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c455b-173">When a new property is saved, the **Search property** textbox is populated with the name of the new property and the new property is displayed.</span></span> <span data-ttu-id="c455b-174">Pour afficher toutes les propriétés, effacez la zone de texte **Propriétés de recherche** , puis appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="c455b-174">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![Propriétés][api-management-properties-property-saved]

<span data-ttu-id="c455b-176">Pour plus d’informations sur la création d’une propriété à l’aide de l’API REST, consultez [Créer une propriété à l’aide de l’API REST](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span><span class="sxs-lookup"><span data-stu-id="c455b-176">For information on creating a property using the REST API, see [Create a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="to-edit-a-property"></a><span data-ttu-id="c455b-177">Pour modifier une propriété</span><span class="sxs-lookup"><span data-stu-id="c455b-177">To edit a property</span></span>
<span data-ttu-id="c455b-178">Pour modifier une propriété, cliquez sur **Modifier** en regard de la propriété à modifier.</span><span class="sxs-lookup"><span data-stu-id="c455b-178">To edit a property, click **Edit** beside the property to edit.</span></span>

![Modifier la propriété][api-management-properties-edit]

<span data-ttu-id="c455b-180">Apportez les modifications souhaitées, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c455b-180">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="c455b-181">Si vous modifiez le nom de propriété, toutes les stratégies qui font référence à cette propriété sont automatiquement mises à jour pour utiliser le nouveau nom.</span><span class="sxs-lookup"><span data-stu-id="c455b-181">If you change the property name, any policies that reference that property are automatically updated to use the new name.</span></span>

![Modifier la propriété][api-management-properties-edit-property]

<span data-ttu-id="c455b-183">Pour plus d’informations sur la modification d’une propriété à l’aide de l’API REST, consultez [Modifier une propriété à l’aide de l’API REST](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span><span class="sxs-lookup"><span data-stu-id="c455b-183">For information on editing a property using the REST API, see [Edit a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="to-delete-a-property"></a><span data-ttu-id="c455b-184">Pour supprimer une propriété</span><span class="sxs-lookup"><span data-stu-id="c455b-184">To delete a property</span></span>
<span data-ttu-id="c455b-185">Pour supprimer une propriété, cliquez sur **Supprimer** en regard de la propriété à supprimer.</span><span class="sxs-lookup"><span data-stu-id="c455b-185">To delete a property, click **Delete** beside the property to delete.</span></span>

![Supprimer la propriété][api-management-properties-delete]

<span data-ttu-id="c455b-187">Cliquez sur **Oui, le supprimer** pour confirmer la suppression.</span><span class="sxs-lookup"><span data-stu-id="c455b-187">Click **Yes, delete it** to confirm.</span></span>

![Confirmation de suppression][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="c455b-189">Si la propriété est référencée par des stratégies, vous ne pouvez pas la supprimer correctement tant que vous ne l’avez pas supprimée de toutes les stratégies qui l’utilisent.</span><span class="sxs-lookup"><span data-stu-id="c455b-189">If the property is referenced by any policies, you will be unable to successfully delete it until you remove the property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="c455b-190">Pour plus d’informations sur la suppression d’une propriété à l’aide de l’API REST, consultez [Supprimer une propriété à l’aide de l’API REST](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span><span class="sxs-lookup"><span data-stu-id="c455b-190">For information on deleting a property using the REST API, see [Delete a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="to-search-and-filter-properties"></a><span data-ttu-id="c455b-191">Pour rechercher et filtrer les propriétés</span><span class="sxs-lookup"><span data-stu-id="c455b-191">To search and filter properties</span></span>
<span data-ttu-id="c455b-192">L’onglet **Propriétés** inclut des fonctionnalités de recherche et de filtrage pour vous aider à gérer vos propriétés.</span><span class="sxs-lookup"><span data-stu-id="c455b-192">The **Properties** tab includes searching and filtering capabilities to help you manage your properties.</span></span> <span data-ttu-id="c455b-193">Pour filtrer la liste des propriétés par nom de propriété, entrez un terme à rechercher dans la zone de texte **Propriétés de recherche** .</span><span class="sxs-lookup"><span data-stu-id="c455b-193">To filter the property list by property name, enter a search term in the **Search property** textbox.</span></span> <span data-ttu-id="c455b-194">Pour afficher toutes les propriétés, effacez la zone de texte **Propriétés de recherche** , puis appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="c455b-194">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![Search][api-management-properties-search]

<span data-ttu-id="c455b-196">Pour filtrer la liste des propriétés en fonction des valeurs de balise, entrez une ou plusieurs balises dans la zone de texte **Filtrer par balises** .</span><span class="sxs-lookup"><span data-stu-id="c455b-196">To filter the property list by tag values, enter one or more tags into the **Filter by tags** textbox.</span></span> <span data-ttu-id="c455b-197">Pour afficher toutes les propriétés, effacez la zone de texte **Filtrer par balises** , puis appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="c455b-197">To display all properties, clear the **Filter by tags** textbox and press enter.</span></span>

![Filtre][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="c455b-199">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c455b-199">Next steps</span></span>
* <span data-ttu-id="c455b-200">En savoir plus sur l’utilisation des stratégies</span><span class="sxs-lookup"><span data-stu-id="c455b-200">Learn more about working with policies</span></span>
  * [<span data-ttu-id="c455b-201">Stratégies dans Gestion des API</span><span class="sxs-lookup"><span data-stu-id="c455b-201">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="c455b-202">Référence de stratégie</span><span class="sxs-lookup"><span data-stu-id="c455b-202">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="c455b-203">Expressions de stratégie</span><span class="sxs-lookup"><span data-stu-id="c455b-203">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="c455b-204">Regarder une vidéo de présentation</span><span class="sxs-lookup"><span data-stu-id="c455b-204">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Use-Properties-in-Policies/player]
> 
> 

[api-management-properties]: ./media/api-management-howto-properties/api-management-properties.png
[api-management-properties-add-property]: ./media/api-management-howto-properties/api-management-properties-add-property.png
[api-management-properties-edit-property]: ./media/api-management-howto-properties/api-management-properties-edit-property.png
[api-management-properties-add-property-menu]: ./media/api-management-howto-properties/api-management-properties-add-property-menu.png
[api-management-properties-property-saved]: ./media/api-management-howto-properties/api-management-properties-property-saved.png
[api-management-properties-delete]: ./media/api-management-howto-properties/api-management-properties-delete.png
[api-management-properties-edit]: ./media/api-management-howto-properties/api-management-properties-edit.png
[api-management-delete-confirm]: ./media/api-management-howto-properties/api-management-delete-confirm.png
[api-management-properties-search]: ./media/api-management-howto-properties/api-management-properties-search.png
[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png

