---
title: "propriétés de toouse aaaHow dans les stratégies de gestion des API Azure"
description: "Découvrez comment les propriétés de toouse dans les stratégies de gestion des API Azure."
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
ms.openlocfilehash: 1ff096deeb97543b48dcf1f40be9dbfcbcd09542
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-properties-in-azure-api-management-policies"></a><span data-ttu-id="72cb3-103">Comment les propriétés de toouse dans les stratégies de gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="72cb3-103">How toouse properties in Azure API Management policies</span></span>
<span data-ttu-id="72cb3-104">Stratégies de gestion des API constituent une puissante capacité du système hello autoriser la publication de hello toochange hello du comportement de hello API via la configuration.</span><span class="sxs-lookup"><span data-stu-id="72cb3-104">API Management policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="72cb3-105">Les stratégies sont une collection d’instructions qui sont exécutées séquentiellement sur la demande de hello ou de réponse d’une API.</span><span class="sxs-lookup"><span data-stu-id="72cb3-105">Policies are a collection of statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="72cb3-106">Les instructions de la stratégie peuvent être construites à l’aide de valeurs de texte littéral, d’expressions de stratégie et de propriétés.</span><span class="sxs-lookup"><span data-stu-id="72cb3-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="72cb3-107">Chaque instance de service de gestion des API possède une collection de propriétés de paires clé/valeur qui sont globales toohello l’instance de service.</span><span class="sxs-lookup"><span data-stu-id="72cb3-107">Each API Management service instance has a properties collection of key/value pairs that are global toohello service instance.</span></span> <span data-ttu-id="72cb3-108">Ces propriétés peuvent être des valeurs de chaîne constante toomanage utilisé sur toutes les stratégies et de configuration de l’API.</span><span class="sxs-lookup"><span data-stu-id="72cb3-108">These properties can be used toomanage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="72cb3-109">Chaque propriété a hello suivant des attributs.</span><span class="sxs-lookup"><span data-stu-id="72cb3-109">Each property has hello following attributes.</span></span>

| <span data-ttu-id="72cb3-110">Attribut</span><span class="sxs-lookup"><span data-stu-id="72cb3-110">Attribute</span></span> | <span data-ttu-id="72cb3-111">Type</span><span class="sxs-lookup"><span data-stu-id="72cb3-111">Type</span></span> | <span data-ttu-id="72cb3-112">Description</span><span class="sxs-lookup"><span data-stu-id="72cb3-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="72cb3-113">Name</span><span class="sxs-lookup"><span data-stu-id="72cb3-113">Name</span></span> |<span data-ttu-id="72cb3-114">string</span><span class="sxs-lookup"><span data-stu-id="72cb3-114">string</span></span> |<span data-ttu-id="72cb3-115">nom de Hello de propriété de hello.</span><span class="sxs-lookup"><span data-stu-id="72cb3-115">hello name of hello property.</span></span> <span data-ttu-id="72cb3-116">Il peut contenir uniquement des lettres, des chiffres, des points, des tirets et des caractères de soulignement.</span><span class="sxs-lookup"><span data-stu-id="72cb3-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="72cb3-117">Valeur</span><span class="sxs-lookup"><span data-stu-id="72cb3-117">Value</span></span> |<span data-ttu-id="72cb3-118">string</span><span class="sxs-lookup"><span data-stu-id="72cb3-118">string</span></span> |<span data-ttu-id="72cb3-119">valeur de propriété de hello de Hello.</span><span class="sxs-lookup"><span data-stu-id="72cb3-119">hello value of hello property.</span></span> <span data-ttu-id="72cb3-120">Elle ne peut pas être vide ni se composer uniquement d’espaces blancs.</span><span class="sxs-lookup"><span data-stu-id="72cb3-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="72cb3-121">Secret</span><span class="sxs-lookup"><span data-stu-id="72cb3-121">Secret</span></span> |<span data-ttu-id="72cb3-122">booléenne</span><span class="sxs-lookup"><span data-stu-id="72cb3-122">boolean</span></span> |<span data-ttu-id="72cb3-123">Détermine si la valeur de hello est une clé secrète et doit être chiffrée ou non.</span><span class="sxs-lookup"><span data-stu-id="72cb3-123">Determines whether hello value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="72cb3-124">Tags</span><span class="sxs-lookup"><span data-stu-id="72cb3-124">Tags</span></span> |<span data-ttu-id="72cb3-125">tableau de chaînes</span><span class="sxs-lookup"><span data-stu-id="72cb3-125">array of string</span></span> |<span data-ttu-id="72cb3-126">Facultatif les balises qui fourni peut être utilisé toofilter hello propriété liste.</span><span class="sxs-lookup"><span data-stu-id="72cb3-126">Optional tags that when provided can be used toofilter hello property list.</span></span> |

<span data-ttu-id="72cb3-127">Propriétés sont configurées dans le portail de publication hello sur hello **propriétés** onglet. Bonjour l’exemple suivant, trois propriétés sont configurées.</span><span class="sxs-lookup"><span data-stu-id="72cb3-127">Properties are configured in hello publisher portal on hello **Properties** tab. In hello following example, three properties are configured.</span></span>

![Propriétés][api-management-properties]

<span data-ttu-id="72cb3-129">Les valeurs de propriété peuvent contenir des chaînes littérales et des [expressions de stratégie](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="72cb3-129">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="72cb3-130">Hello tableau suivant montre hello précédente trois exemples de propriétés et leurs attributs.</span><span class="sxs-lookup"><span data-stu-id="72cb3-130">hello following table shows hello previous three sample properties and their attributes.</span></span> <span data-ttu-id="72cb3-131">Hello valeur `ExpressionProperty` est une expression de stratégie qui retourne une chaîne contenant hello date et heure actuelles.</span><span class="sxs-lookup"><span data-stu-id="72cb3-131">hello value of `ExpressionProperty` is a policy expression that returns a string containing hello current date and time.</span></span> <span data-ttu-id="72cb3-132">Hello propriété `ContosoHeaderValue` est marquée en tant que secret, donc sa valeur n’est pas affichée.</span><span class="sxs-lookup"><span data-stu-id="72cb3-132">hello property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="72cb3-133">Nom</span><span class="sxs-lookup"><span data-stu-id="72cb3-133">Name</span></span> | <span data-ttu-id="72cb3-134">Valeur</span><span class="sxs-lookup"><span data-stu-id="72cb3-134">Value</span></span> | <span data-ttu-id="72cb3-135">Secret</span><span class="sxs-lookup"><span data-stu-id="72cb3-135">Secret</span></span> | <span data-ttu-id="72cb3-136">Balises</span><span class="sxs-lookup"><span data-stu-id="72cb3-136">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="72cb3-137">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="72cb3-137">ContosoHeader</span></span> |<span data-ttu-id="72cb3-138">TrackingId</span><span class="sxs-lookup"><span data-stu-id="72cb3-138">TrackingId</span></span> |<span data-ttu-id="72cb3-139">False</span><span class="sxs-lookup"><span data-stu-id="72cb3-139">False</span></span> |<span data-ttu-id="72cb3-140">Contoso</span><span class="sxs-lookup"><span data-stu-id="72cb3-140">Contoso</span></span> |
| <span data-ttu-id="72cb3-141">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="72cb3-141">ContosoHeaderValue</span></span> |<span data-ttu-id="72cb3-142">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="72cb3-142">••••••••••••••••••••••</span></span> |<span data-ttu-id="72cb3-143">True</span><span class="sxs-lookup"><span data-stu-id="72cb3-143">True</span></span> |<span data-ttu-id="72cb3-144">Contoso</span><span class="sxs-lookup"><span data-stu-id="72cb3-144">Contoso</span></span> |
| <span data-ttu-id="72cb3-145">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="72cb3-145">ExpressionProperty</span></span> |<span data-ttu-id="72cb3-146">@(DateHeure.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="72cb3-146">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="72cb3-147">False</span><span class="sxs-lookup"><span data-stu-id="72cb3-147">False</span></span> | |

## <a name="toouse-a-property"></a><span data-ttu-id="72cb3-148">toouse une propriété</span><span class="sxs-lookup"><span data-stu-id="72cb3-148">toouse a property</span></span>
<span data-ttu-id="72cb3-149">nom de la propriété hello sur place à l’intérieur d’une double paire d’accolades de toouse une propriété dans une stratégie, comme `{{ContosoHeader}}`, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="72cb3-149">toouse a property in a policy, place hello property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in hello following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="72cb3-150">Dans cet exemple, `ContosoHeader` est utilisé comme nom hello d’un en-tête dans un `set-header` stratégie, et `ContosoHeaderValue` est utilisé en tant que valeur hello de cet en-tête.</span><span class="sxs-lookup"><span data-stu-id="72cb3-150">In this example, `ContosoHeader` is used as hello name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as hello value of that header.</span></span> <span data-ttu-id="72cb3-151">Lorsque cette stratégie est évaluée au cours d’une demande ou réponse toohello API passerelle de gestion, `{{ContosoHeader}}` et `{{ContosoHeaderValue}}` sont remplacés par leurs valeurs de propriété respectives.</span><span class="sxs-lookup"><span data-stu-id="72cb3-151">When this policy is evaluated during a request or response toohello API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="72cb3-152">Propriétés qui peuvent être utilisées en tant qu’attribut complète ou de valeurs d’élément comme indiqué dans l’exemple précédent de hello, mais peut également être insérés dans ou combinés avec partie d’une expression de texte littéral, comme indiqué dans hello l’exemple suivant :`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="72cb3-152">Properties can be used as complete attribute or element values as shown in hello previous example, but they can also be inserted into or combined with part of a literal text expression as shown in hello following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="72cb3-153">Les propriétés peuvent également contenir des expressions de stratégie.</span><span class="sxs-lookup"><span data-stu-id="72cb3-153">Properties can also contain policy expressions.</span></span> <span data-ttu-id="72cb3-154">Dans l’exemple suivant de hello, hello `ExpressionProperty` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="72cb3-154">In hello following example, hello `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="72cb3-155">Lorsque cette stratégie est évaluée, `{{ExpressionProperty}}` est remplacé par sa valeur : `@(DateTime.Now.ToString())`.</span><span class="sxs-lookup"><span data-stu-id="72cb3-155">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="72cb3-156">Étant donné que la valeur de hello est une expression de stratégie, hello expression est évaluée et la stratégie de hello se poursuit son exécution.</span><span class="sxs-lookup"><span data-stu-id="72cb3-156">Since hello value is a policy expression, hello expression is evaluated and hello policy proceeds with its execution.</span></span>

<span data-ttu-id="72cb3-157">Vous pouvez tester ce point dans le portail des développeurs hello en appelant une opération qui a une stratégie avec des propriétés dans la portée.</span><span class="sxs-lookup"><span data-stu-id="72cb3-157">You can test this out in hello developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="72cb3-158">Bonjour l’exemple suivant, une opération est appelée avec l’exemple précédent de hello deux `set-header` stratégies avec des propriétés.</span><span class="sxs-lookup"><span data-stu-id="72cb3-158">In hello following example, an operation is called with hello two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="72cb3-159">Notez que les réponse hello contient deux en-têtes personnalisés qui ont été configurés à l’aide de stratégies avec des propriétés.</span><span class="sxs-lookup"><span data-stu-id="72cb3-159">Note that hello response contains two custom headers that were configured using policies with properties.</span></span>

![Portail des développeurs][api-management-send-results]

<span data-ttu-id="72cb3-161">Si vous examinez hello [trace de l’inspecteur de l’API](api-management-howto-api-inspector.md) pour un appel qui inclut les hello deux stratégies exemple précédente avec les propriétés, vous pouvez voir hello deux `set-header` stratégies avec les valeurs de propriété hello insérées, ainsi que l’expression de stratégie hello évaluation de propriété hello contenant une expression de stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="72cb3-161">If you look at hello [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes hello two previous sample policies with properties, you can see hello two `set-header` policies with hello property values inserted as well as hello policy expression evaluation for hello property that contained hello policy expression.</span></span>

![Suivi de l’inspecteur d’API][api-management-api-inspector-trace]

<span data-ttu-id="72cb3-163">Alors que les valeurs de propriété peuvent contenir des expressions de stratégie, elles ne peuvent pas contenir d’autres propriétés.</span><span class="sxs-lookup"><span data-stu-id="72cb3-163">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="72cb3-164">Si le texte qui contient une référence de propriété est utilisée pour une valeur de propriété, telles que `Property value text {{MyProperty}}`, que la référence de propriété ne sera pas remplacé et sera inclus dans le cadre de la valeur de la propriété hello.</span><span class="sxs-lookup"><span data-stu-id="72cb3-164">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of hello property value.</span></span>

## <a name="toocreate-a-property"></a><span data-ttu-id="72cb3-165">toocreate une propriété</span><span class="sxs-lookup"><span data-stu-id="72cb3-165">toocreate a property</span></span>
<span data-ttu-id="72cb3-166">toocreate une propriété, cliquez sur **Ajouter propriété** sur hello **propriétés** onglet.</span><span class="sxs-lookup"><span data-stu-id="72cb3-166">toocreate a property, click **Add property** on hello **Properties** tab.</span></span>

![Ajouter une propriété][api-management-properties-add-property-menu]

<span data-ttu-id="72cb3-168">**Nom** et **Valeur** doivent être renseignés.</span><span class="sxs-lookup"><span data-stu-id="72cb3-168">**Name** and **Value** are required values.</span></span> <span data-ttu-id="72cb3-169">Si cette valeur de propriété est une clé secrète, vérifiez hello **il s’agit d’une clé secrète** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="72cb3-169">If this property value is a secret, check hello **This is a secret** checkbox.</span></span> <span data-ttu-id="72cb3-170">Entrez un ou plusieurs toohelp balises facultatif en organisant les propriétés, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="72cb3-170">Enter one or more optional tags toohelp with organizing your properties, and click **Save**.</span></span>

![Ajouter une propriété][api-management-properties-add-property]

<span data-ttu-id="72cb3-172">Lorsqu’une nouvelle propriété est enregistrée, hello **propriétés de recherche** textbox est remplie avec le nom de hello de hello nouvelle propriété et la nouvelle propriété de hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="72cb3-172">When a new property is saved, hello **Search property** textbox is populated with hello name of hello new property and hello new property is displayed.</span></span> <span data-ttu-id="72cb3-173">Désactivez de toutes les propriétés, toodisplay hello **propriétés de recherche** zone de texte et appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="72cb3-173">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![Propriétés][api-management-properties-property-saved]

<span data-ttu-id="72cb3-175">Pour plus d’informations sur la création d’une propriété à l’aide de hello API REST, consultez [créer une propriété à l’aide des API REST de hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span><span class="sxs-lookup"><span data-stu-id="72cb3-175">For information on creating a property using hello REST API, see [Create a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="tooedit-a-property"></a><span data-ttu-id="72cb3-176">tooedit une propriété</span><span class="sxs-lookup"><span data-stu-id="72cb3-176">tooedit a property</span></span>
<span data-ttu-id="72cb3-177">tooedit une propriété, cliquez sur **modifier** en regard de tooedit de propriété hello.</span><span class="sxs-lookup"><span data-stu-id="72cb3-177">tooedit a property, click **Edit** beside hello property tooedit.</span></span>

![Modifier la propriété][api-management-properties-edit]

<span data-ttu-id="72cb3-179">Apportez les modifications souhaitées, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="72cb3-179">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="72cb3-180">Si vous modifiez le nom de la propriété hello, toutes les stratégies qui font référence à cette propriété sont nouveau nom de hello toouse mises à jour automatiquement.</span><span class="sxs-lookup"><span data-stu-id="72cb3-180">If you change hello property name, any policies that reference that property are automatically updated toouse hello new name.</span></span>

![Modifier la propriété][api-management-properties-edit-property]

<span data-ttu-id="72cb3-182">Pour plus d’informations sur la modification d’une propriété à l’aide de hello API REST, consultez [modifier une propriété à l’aide des API REST de hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span><span class="sxs-lookup"><span data-stu-id="72cb3-182">For information on editing a property using hello REST API, see [Edit a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="toodelete-a-property"></a><span data-ttu-id="72cb3-183">toodelete une propriété</span><span class="sxs-lookup"><span data-stu-id="72cb3-183">toodelete a property</span></span>
<span data-ttu-id="72cb3-184">toodelete une propriété, cliquez sur **supprimer** en regard de toodelete de propriété hello.</span><span class="sxs-lookup"><span data-stu-id="72cb3-184">toodelete a property, click **Delete** beside hello property toodelete.</span></span>

![Supprimer la propriété][api-management-properties-delete]

<span data-ttu-id="72cb3-186">Cliquez sur **Oui, supprimez-le** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="72cb3-186">Click **Yes, delete it** tooconfirm.</span></span>

![Confirmation de suppression][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="72cb3-188">Si la propriété de hello est référencée par les stratégies, vous ne pouvez pas toosuccessfully supprimer jusqu'à la suppression de la propriété de hello de toutes les stratégies qui l’utilisent.</span><span class="sxs-lookup"><span data-stu-id="72cb3-188">If hello property is referenced by any policies, you will be unable toosuccessfully delete it until you remove hello property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="72cb3-189">Pour plus d’informations sur la suppression d’une propriété à l’aide de hello API REST, consultez [supprimer une propriété à l’aide des API REST de hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span><span class="sxs-lookup"><span data-stu-id="72cb3-189">For information on deleting a property using hello REST API, see [Delete a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="toosearch-and-filter-properties"></a><span data-ttu-id="72cb3-190">propriétés toosearch et filtre</span><span class="sxs-lookup"><span data-stu-id="72cb3-190">toosearch and filter properties</span></span>
<span data-ttu-id="72cb3-191">Hello **propriétés** onglet inclut la recherche et filtrage toohelp fonctionnalités vous gérez vos propriétés.</span><span class="sxs-lookup"><span data-stu-id="72cb3-191">hello **Properties** tab includes searching and filtering capabilities toohelp you manage your properties.</span></span> <span data-ttu-id="72cb3-192">liste de propriétés toofilter hello par nom de propriété, entrez un terme à rechercher dans hello **propriétés de recherche** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="72cb3-192">toofilter hello property list by property name, enter a search term in hello **Search property** textbox.</span></span> <span data-ttu-id="72cb3-193">Désactivez de toutes les propriétés, toodisplay hello **propriétés de recherche** zone de texte et appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="72cb3-193">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![Search][api-management-properties-search]

<span data-ttu-id="72cb3-195">liste de propriétés hello toofilter par des valeurs de balise, entrez une ou plusieurs balises dans hello **filtre par des balises** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="72cb3-195">toofilter hello property list by tag values, enter one or more tags into hello **Filter by tags** textbox.</span></span> <span data-ttu-id="72cb3-196">Désactivez de toutes les propriétés, toodisplay hello **filtre par des balises** zone de texte et appuyez sur ENTRÉE.</span><span class="sxs-lookup"><span data-stu-id="72cb3-196">toodisplay all properties, clear hello **Filter by tags** textbox and press enter.</span></span>

![Filtrer][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="72cb3-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="72cb3-198">Next steps</span></span>
* <span data-ttu-id="72cb3-199">En savoir plus sur l’utilisation des stratégies</span><span class="sxs-lookup"><span data-stu-id="72cb3-199">Learn more about working with policies</span></span>
  * [<span data-ttu-id="72cb3-200">Stratégies dans Gestion des API</span><span class="sxs-lookup"><span data-stu-id="72cb3-200">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="72cb3-201">Référence de stratégie</span><span class="sxs-lookup"><span data-stu-id="72cb3-201">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="72cb3-202">Expressions de stratégie</span><span class="sxs-lookup"><span data-stu-id="72cb3-202">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="72cb3-203">Regarder une vidéo de présentation</span><span class="sxs-lookup"><span data-stu-id="72cb3-203">Watch a video overview</span></span>
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

