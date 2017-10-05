---
title: "Stratégies dans Gestion des API Azure | Microsoft Docs"
description: "Apprenez à créer, à modifier et à configurer des stratégies dans Gestion des API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 537e5caf-708b-430e-a83f-72b70af28aa9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7c1f235343074ec11c635097f2b094a10f3fe781
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="7fd31-103">Stratégies dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="7fd31-103">Policies in Azure API Management</span></span>
<span data-ttu-id="7fd31-104">Dans Gestion des API Azure, les stratégies sont une fonctionnalité puissante du système qui permet à l’éditeur de modifier le comportement de l’API grâce à la configuration.</span><span class="sxs-lookup"><span data-stu-id="7fd31-104">In Azure API Management, policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="7fd31-105">Les stratégies sont un ensemble d'instructions qui sont exécutées dans l'ordre sur demande ou sur réponse d'une API.</span><span class="sxs-lookup"><span data-stu-id="7fd31-105">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="7fd31-106">Les instructions les plus utilisées comprennent la conversion du format XML au format JSON et la limitation du débit d'appels pour restreindre la quantité d'appels entrants d'un développeur.</span><span class="sxs-lookup"><span data-stu-id="7fd31-106">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="7fd31-107">De nombreuses autres stratégies sont disponibles.</span><span class="sxs-lookup"><span data-stu-id="7fd31-107">Many more policies are available out of the box.</span></span>

<span data-ttu-id="7fd31-108">Pour obtenir la liste complète des instructions et des paramètres de stratégie, consultez la section [Référence de stratégie][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="7fd31-108">See the [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="7fd31-109">Les stratégies sont appliquées au niveau de la passerelle qui se trouve entre le consommateur de l’API et l’API managée.</span><span class="sxs-lookup"><span data-stu-id="7fd31-109">Policies are applied inside the gateway which sits between the API consumer and the managed API.</span></span> <span data-ttu-id="7fd31-110">La passerelle reçoit toutes les demandes et les transfère normalement sans les modifier à l’API sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="7fd31-110">The gateway receives all requests and usually forwards them unaltered to the underlying API.</span></span> <span data-ttu-id="7fd31-111">Cependant, une stratégie peut appliquer des modifications à la demande entrante et à la réponse sortante.</span><span class="sxs-lookup"><span data-stu-id="7fd31-111">However a policy can apply changes to both the inbound request and outbound response.</span></span>

<span data-ttu-id="7fd31-112">Les expressions de stratégie peuvent être utilisées comme valeurs d’attribut ou valeurs de texte dans l’une des stratégies de Gestion des API, sauf si la stratégie le spécifie autrement.</span><span class="sxs-lookup"><span data-stu-id="7fd31-112">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="7fd31-113">Certaines stratégies, telles que les stratégies [Contrôler le flux][Control flow] et [Définir la variable][Set variable], sont basées sur des expressions de stratégie.</span><span class="sxs-lookup"><span data-stu-id="7fd31-113">Some policies such as the [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="7fd31-114">Pour plus d’informations, consultez les rubriques [Stratégies avancées][Advanced policies] et [Expressions de stratégie][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="7fd31-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="7fd31-115"><a name="scopes"> </a>Configuration des stratégies</span><span class="sxs-lookup"><span data-stu-id="7fd31-115"><a name="scopes"> </a>How to configure policies</span></span>
<span data-ttu-id="7fd31-116">Les stratégies peuvent être configurées de façon globale, ou bien au niveau d’un [produit][Product], d’une [API][API] ou d’une [opération][Operation].</span><span class="sxs-lookup"><span data-stu-id="7fd31-116">Policies can be configured globally or at the scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="7fd31-117">Pour configurer une stratégie, accédez à l'éditeur Stratégies dans le portail des éditeurs.</span><span class="sxs-lookup"><span data-stu-id="7fd31-117">To configure a policy, navigate to the Policies editor in the publisher portal.</span></span>

![Policies menu][policies-menu]

<span data-ttu-id="7fd31-119">L’éditeur de stratégies se compose de trois sections principales : la portée de la stratégie (en haut), la définition de la stratégie, là où les stratégies sont modifiées (à gauche) et la liste des instructions (à droite) :</span><span class="sxs-lookup"><span data-stu-id="7fd31-119">The policies editor consists of three main sections: the policy scope (top), the policy definition where policies are edited (left) and the statements list (right):</span></span>

![Policies editor][policies-editor]

<span data-ttu-id="7fd31-121">Pour configurer une stratégie, vous devez d'abord sélectionner la portée à laquelle elle doit s'appliquer.</span><span class="sxs-lookup"><span data-stu-id="7fd31-121">To begin configuring a policy you must first select the scope at which the policy should apply.</span></span> <span data-ttu-id="7fd31-122">Dans la capture d'écran ci-dessous, le produit **Starter** est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="7fd31-122">In the screenshot below the **Starter** product is selected.</span></span> <span data-ttu-id="7fd31-123">Notez que le symbole carré à côté du nom de la stratégie indique qu'une stratégie est déjà appliquée à ce niveau.</span><span class="sxs-lookup"><span data-stu-id="7fd31-123">Note that the square symbol next to the policy name indicates that a policy is already applied at this level.</span></span>

![Scope][policies-scope]

<span data-ttu-id="7fd31-125">Comme une stratégie est déjà appliquée, la configuration est présentée dans l'affichage de la définition.</span><span class="sxs-lookup"><span data-stu-id="7fd31-125">Since a policy has already been applied, the configuration is shown in the definition view.</span></span>

![Configuration][policies-configure]

<span data-ttu-id="7fd31-127">Initialement, la stratégie est affichée uniquement en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="7fd31-127">The policy is displayed read-only at first.</span></span> <span data-ttu-id="7fd31-128">Pour pouvoir modifier la définition, cliquez sur l’action **Configurer la stratégie** .</span><span class="sxs-lookup"><span data-stu-id="7fd31-128">In order to edit the definition click the **Configure Policy** action.</span></span>

![Modifier][policies-edit]

<span data-ttu-id="7fd31-130">La définition de la stratégie est un simple document XML qui décrit une séquence d'instructions entrantes et sortantes.</span><span class="sxs-lookup"><span data-stu-id="7fd31-130">The policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="7fd31-131">Le code XML peut être modifié directement dans la fenêtre de définition.</span><span class="sxs-lookup"><span data-stu-id="7fd31-131">The XML can be edited directly in the definition window.</span></span> <span data-ttu-id="7fd31-132">Une liste d’instructions est fournie à droite. Les instructions applicables à la portée actuelle sont activées et mises en surbrillance, comme l’instruction **Limit Call Rate** dans la capture d’écran ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7fd31-132">A list of statements is provided to the right and statements applicable to the current scope are enabled and highlighted; as demonstrated by the **Limit Call Rate** statement in the screenshot above.</span></span>

<span data-ttu-id="7fd31-133">Lorsque vous cliquez sur une instruction active, le code XML correspondant est inséré à l'emplacement du curseur dans la fenêtre de définition.</span><span class="sxs-lookup"><span data-stu-id="7fd31-133">Clicking an enabled statement will add the appropriate XML at the location of the cursor in the definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="7fd31-134">Si la stratégie que vous souhaitez ajouter n’est pas activée, vérifiez que vous êtes dans l’étendue correcte pour cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="7fd31-134">If the policy that you want to add is not enabled, ensure that you are in the correct scope for that policy.</span></span> <span data-ttu-id="7fd31-135">Chaque instruction de stratégie est conçue pour une utilisation dans certaines étendues et sections de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="7fd31-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="7fd31-136">Pour consulter les sections de la stratégie et les étendues pour une stratégie, consultez la section **Utilisation** de cette stratégie dans la [Référence de la stratégie][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="7fd31-136">To review the policy sections and scopes for a policy, check the **Usage** section for that policy in the [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="7fd31-137">La liste complète des instructions et des paramètres des stratégies se trouve dans la section [Référence de stratégie][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="7fd31-137">A full list of policy statements and their settings are available in the [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="7fd31-138">Par exemple, pour ajouter une nouvelle instruction pour limiter les demandes entrantes à certaines adresses IP, placez le curseur juste à l'intérieur du contenu de l'élément `inbound` XML, puis cliquez sur l'instruction **Restrict caller IP** .</span><span class="sxs-lookup"><span data-stu-id="7fd31-138">For example, to add a new statement to restrict incoming requests to specified IP addresses, place the cursor just inside the content of the `inbound` XML element and click the **Restrict caller IPs** statement.</span></span>

![Restriction policies][policies-restrict]

<span data-ttu-id="7fd31-140">Ceci ajoute un code XML à l'élément `inbound` , indiquant comment configurer l'instruction.</span><span class="sxs-lookup"><span data-stu-id="7fd31-140">This will add an XML snippet to the `inbound` element that provides guidance on how to configure the statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="7fd31-141">Pour limiter les demandes entrantes et n'accepter que celles venant de l'adresse IP 1.2.3.4, modifiez le code XML comme suit :</span><span class="sxs-lookup"><span data-stu-id="7fd31-141">To limit inbound requests and accept only those from an IP address of 1.2.3.4 modify the XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Enregistrer][policies-save]

<span data-ttu-id="7fd31-143">Lorsque vous avez terminé la configuration des instructions de la stratégie, cliquez sur **Enregistrer**. Les modifications sont ajoutées immédiatement à la passerelle Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="7fd31-143">When complete configuring the statements for the policy, click **Save** and the changes will be propagated to the API Management gateway immediately.</span></span>

## <span data-ttu-id="7fd31-144"><a name="sections"> </a>Configuration de la stratégie</span><span class="sxs-lookup"><span data-stu-id="7fd31-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="7fd31-145">Une stratégie est une série d'instructions qui s'exécutent dans l'ordre pour une demande et une réponse.</span><span class="sxs-lookup"><span data-stu-id="7fd31-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="7fd31-146">La configuration se compose des sections `inbound`, `backend`, `outbound` et `on-error`, comme présenté dans la configuration suivante.</span><span class="sxs-lookup"><span data-stu-id="7fd31-146">The configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in the following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements to be applied to the request go here -->
  </inbound>
  <backend>
    <!-- statements to be applied before the request is forwarded to 
         the backend service go here -->
  </backend>
  <outbound>
    <!-- statements to be applied to the response go here -->
  </outbound>
  <on-error>
    <!-- statements to be applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="7fd31-147">S'il existe une erreur lors du traitement d'une demande, les autres étapes des sections `inbound`, `backend` ou `outbound` sont ignorées et l'exécution passe aux instructions de la section `on-error`.</span><span class="sxs-lookup"><span data-stu-id="7fd31-147">If there is an error during the processing of a request, any remaining steps in the `inbound`, `backend`, or `outbound` sections are skipped and execution jumps to the statements in the `on-error` section.</span></span> <span data-ttu-id="7fd31-148">En plaçant des instructions de stratégie dans la section `on-error`, vous pouvez consulter l'erreur à l'aide de la propriété `context.LastError`, inspecter et personnaliser la réponse à l'erreur à l'aide de la stratégie `set-body`, puis configurer ce qui se passe si une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="7fd31-148">By placing policy statements in the `on-error` section you can review the error by using the `context.LastError` property, inspect and customize the error response using the `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="7fd31-149">Il existe des codes d'erreur pour les étapes intégrées et pour les erreurs qui peuvent se produire pendant le traitement d'instructions de stratégie.</span><span class="sxs-lookup"><span data-stu-id="7fd31-149">There are error codes for built-in steps and for errors that may occur during the processing of policy statements.</span></span> <span data-ttu-id="7fd31-150">Pour plus d'informations, consultez [Gestion des erreurs dans les stratégies de gestion des API](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span><span class="sxs-lookup"><span data-stu-id="7fd31-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="7fd31-151">Comme les stratégies peuvent être spécifiées à différents niveaux (globale, produits, API et opérations), la configuration vous permet de spécifier l'ordre dans lequel les instructions de la définition de la stratégie sont exécutées par rapport à la stratégie parente.</span><span class="sxs-lookup"><span data-stu-id="7fd31-151">Since policies can be specified at different levels (global, product, api and operation) the configuration provides a way for you to specify the order in which the policy definition's statements execute with respect to the parent policy.</span></span> 

<span data-ttu-id="7fd31-152">Les étendues de stratégie sont évaluées dans l'ordre suivant.</span><span class="sxs-lookup"><span data-stu-id="7fd31-152">Policy scopes are evaluated in the following order.</span></span>

1. <span data-ttu-id="7fd31-153">Étendue globale</span><span class="sxs-lookup"><span data-stu-id="7fd31-153">Global scope</span></span>
2. <span data-ttu-id="7fd31-154">Étendue produit</span><span class="sxs-lookup"><span data-stu-id="7fd31-154">Product scope</span></span>
3. <span data-ttu-id="7fd31-155">Étendue API</span><span class="sxs-lookup"><span data-stu-id="7fd31-155">API scope</span></span>
4. <span data-ttu-id="7fd31-156">Étendue opération</span><span class="sxs-lookup"><span data-stu-id="7fd31-156">Operation scope</span></span>

<span data-ttu-id="7fd31-157">Les instructions qu'elles contiennent sont évaluées en fonction de l'emplacement de l'élément `base` , s'il est présent.</span><span class="sxs-lookup"><span data-stu-id="7fd31-157">The statements within them are evaluated according to the placement of the `base` element, if it is present.</span></span> <span data-ttu-id="7fd31-158">Une stratégie globale n’a aucune stratégie parente et l’utilisation de l’élément `<base>` n’a aucun effet.</span><span class="sxs-lookup"><span data-stu-id="7fd31-158">Global policy has no parent policy and using the `<base>` element in it has no effect.</span></span>

<span data-ttu-id="7fd31-159">Par exemple, si vous avez une stratégie configurée au niveau global et une stratégie configurée pour une API, dès que cette API est utilisée, les deux stratégies sont appliquées.</span><span class="sxs-lookup"><span data-stu-id="7fd31-159">For example, if you have a policy at the global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="7fd31-160">Le service Gestion des API permet de trier de façon déterminée les instructions de stratégie combinées via l'élément de base.</span><span class="sxs-lookup"><span data-stu-id="7fd31-160">API Management allows for deterministic ordering of combined policy statements via the base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="7fd31-161">Dans l'exemple de définition de stratégie ci-dessus, l'instruction `cross-domain` s'exécute avant toutes les autres stratégies de niveau supérieur, qui sont à leur tour suivies de la stratégie `find-and-replace`.</span><span class="sxs-lookup"><span data-stu-id="7fd31-161">In the example policy definition above, the `cross-domain` statement would execute before any higher policies which would in turn, be followed by the `find-and-replace` policy.</span></span> 

<span data-ttu-id="7fd31-162">Pour afficher les stratégies dans l'étendue actuelle dans l'éditeur de stratégie, cliquez sur **Recalculer la stratégie en vigueur pour l'étendue sélectionnée**.</span><span class="sxs-lookup"><span data-stu-id="7fd31-162">To see the policies in the current scope in the policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7fd31-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7fd31-163">Next steps</span></span>
<span data-ttu-id="7fd31-164">Découvrez la vidéo suivante sur les expressions de stratégie.</span><span class="sxs-lookup"><span data-stu-id="7fd31-164">Check out following video on policy expressions.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Policy Reference]: api-management-policy-reference.md
[Product]: api-management-howto-add-products.md
[API]: api-management-howto-add-products.md#add-apis 
[Operation]: api-management-howto-add-operations.md

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx

[policies-menu]: ./media/api-management-howto-policies/api-management-policies-menu.png
[policies-editor]: ./media/api-management-howto-policies/api-management-policies-editor.png
[policies-scope]: ./media/api-management-howto-policies/api-management-policies-scope.png
[policies-configure]: ./media/api-management-howto-policies/api-management-policies-configure.png
[policies-edit]: ./media/api-management-howto-policies/api-management-policies-edit.png
[policies-restrict]: ./media/api-management-howto-policies/api-management-policies-restrict.png
[policies-save]: ./media/api-management-howto-policies/api-management-policies-save.png
