---
title: aaaPolicies dans Gestion des API Azure | Documents Microsoft
description: "Découvrez comment toocreate, modifier et configurer des stratégies de gestion des API."
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
ms.openlocfilehash: 9ab0f884a655004cb10c05085034df1795f512e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="082c7-103">Stratégies dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="082c7-103">Policies in Azure API Management</span></span>
<span data-ttu-id="082c7-104">Gestion des API Azure, les stratégies sont une fonctionnalité puissante du système hello autoriser la publication de hello toochange hello du comportement de hello API via la configuration.</span><span class="sxs-lookup"><span data-stu-id="082c7-104">In Azure API Management, policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="082c7-105">Les stratégies sont une collection d’instructions qui sont exécutées séquentiellement sur la demande de hello ou de réponse d’une API.</span><span class="sxs-lookup"><span data-stu-id="082c7-105">Policies are a collection of Statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="082c7-106">Les instructions populaires incluent une conversion de format à partir de XML tooJSON et limiter ainsi toorestrict hello d’appels entrants à partir d’un développeur de taux d’appels.</span><span class="sxs-lookup"><span data-stu-id="082c7-106">Popular Statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer.</span></span> <span data-ttu-id="082c7-107">De nombreuses stratégies supplémentaires sont disponibles en dehors de la zone de hello.</span><span class="sxs-lookup"><span data-stu-id="082c7-107">Many more policies are available out of hello box.</span></span>

<span data-ttu-id="082c7-108">Consultez hello [référence de stratégie] [ Policy Reference] pour obtenir la liste complète des instructions de stratégie et leurs paramètres.</span><span class="sxs-lookup"><span data-stu-id="082c7-108">See hello [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="082c7-109">Stratégies sont appliquées à l’intérieur de passerelle hello qui se situe entre les consommateurs d’API hello et hello géré API.</span><span class="sxs-lookup"><span data-stu-id="082c7-109">Policies are applied inside hello gateway which sits between hello API consumer and hello managed API.</span></span> <span data-ttu-id="082c7-110">Hello passerelle reçoit toutes les requêtes et les non modifiée transfère généralement toohello sous-jacent API.</span><span class="sxs-lookup"><span data-stu-id="082c7-110">hello gateway receives all requests and usually forwards them unaltered toohello underlying API.</span></span> <span data-ttu-id="082c7-111">Cependant une stratégie peut s’appliquer demande entrante de modifications tooboth hello et la réponse sortante.</span><span class="sxs-lookup"><span data-stu-id="082c7-111">However a policy can apply changes tooboth hello inbound request and outbound response.</span></span>

<span data-ttu-id="082c7-112">Expressions de stratégie peuvent être utilisées en tant que valeurs d’attribut ou valeurs de texte dans une des stratégies de gestion des API hello, sauf indication contraire de la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="082c7-112">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="082c7-113">Certaines stratégies telles que hello [flux de contrôle] [ Control flow] et [Set variable] [ Set variable] stratégies basées sur des expressions de stratégie.</span><span class="sxs-lookup"><span data-stu-id="082c7-113">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="082c7-114">Pour plus d’informations, consultez les rubriques [Stratégies avancées][Advanced policies] et [Expressions de stratégie][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="082c7-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="082c7-115"><a name="scopes"></a>Comment tooconfigure stratégies</span><span class="sxs-lookup"><span data-stu-id="082c7-115"><a name="scopes"> </a>How tooconfigure policies</span></span>
<span data-ttu-id="082c7-116">Stratégies peuvent être configurées globalement ou au niveau de portée hello d’un [produit][Product], [API] [ API] ou [opération] [Operation].</span><span class="sxs-lookup"><span data-stu-id="082c7-116">Policies can be configured globally or at hello scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="082c7-117">tooconfigure une stratégie, accédez toohello éditeur de stratégies dans le portail de publication hello.</span><span class="sxs-lookup"><span data-stu-id="082c7-117">tooconfigure a policy, navigate toohello Policies editor in hello publisher portal.</span></span>

![Policies menu][policies-menu]

<span data-ttu-id="082c7-119">éditeur de stratégies Hello se compose de trois sections principales : hello stratégie étendue (du haut), hello définition de stratégie dans lequel les stratégies sont modifiés (à gauche) et les instructions hello liste (à droite) :</span><span class="sxs-lookup"><span data-stu-id="082c7-119">hello policies editor consists of three main sections: hello policy scope (top), hello policy definition where policies are edited (left) and hello statements list (right):</span></span>

![Policies editor][policies-editor]

<span data-ttu-id="082c7-121">toobegin configuration d’une stratégie, que vous devez d’abord sélectionner étendue hello à quels hello stratégie doit s’appliquer.</span><span class="sxs-lookup"><span data-stu-id="082c7-121">toobegin configuring a policy you must first select hello scope at which hello policy should apply.</span></span> <span data-ttu-id="082c7-122">Capture d’écran hello ci-dessous hello **Starter** produit est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="082c7-122">In hello screenshot below hello **Starter** product is selected.</span></span> <span data-ttu-id="082c7-123">Notez que ce nom de la stratégie de toohello suivant hello symbole carré indique qu’une stratégie est déjà appliquée à ce niveau.</span><span class="sxs-lookup"><span data-stu-id="082c7-123">Note that hello square symbol next toohello policy name indicates that a policy is already applied at this level.</span></span>

![Scope][policies-scope]

<span data-ttu-id="082c7-125">Dans la mesure où une stratégie a déjà été appliquée, configuration de hello est présentée dans l’affichage de la définition hello.</span><span class="sxs-lookup"><span data-stu-id="082c7-125">Since a policy has already been applied, hello configuration is shown in hello definition view.</span></span>

![Configuration][policies-configure]

<span data-ttu-id="082c7-127">stratégie de Hello est affichée en lecture seule dans un premier temps.</span><span class="sxs-lookup"><span data-stu-id="082c7-127">hello policy is displayed read-only at first.</span></span> <span data-ttu-id="082c7-128">Dans l’ordre tooedit définition de hello, cliquez sur hello **configurer la stratégie** action.</span><span class="sxs-lookup"><span data-stu-id="082c7-128">In order tooedit hello definition click hello **Configure Policy** action.</span></span>

![Modifier][policies-edit]

<span data-ttu-id="082c7-130">définition de stratégie Hello est un document XML simple qui décrit une séquence d’instructions entrantes et sortantes.</span><span class="sxs-lookup"><span data-stu-id="082c7-130">hello policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="082c7-131">Hello XML peut être modifiée directement dans la fenêtre de définition de hello.</span><span class="sxs-lookup"><span data-stu-id="082c7-131">hello XML can be edited directly in hello definition window.</span></span> <span data-ttu-id="082c7-132">Une liste d’instructions est fournie toohello à droite et l’étendue actuelle d’instructions toohello applicables sont activés et mis en surbrillance ; comme indiqué par hello **le taux d’appels limite** instruction dans la capture d’écran hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="082c7-132">A list of statements is provided toohello right and statements applicable toohello current scope are enabled and highlighted; as demonstrated by hello **Limit Call Rate** statement in hello screenshot above.</span></span>

<span data-ttu-id="082c7-133">En cliquant sur une instruction activée ajoutera hello XML approprié à l’emplacement de hello de curseur hello dans l’affichage de la définition hello.</span><span class="sxs-lookup"><span data-stu-id="082c7-133">Clicking an enabled statement will add hello appropriate XML at hello location of hello cursor in hello definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="082c7-134">Si la stratégie de hello que vous souhaitez tooadd n’est pas activée, assurez-vous que vous êtes dans la portée appropriée de hello pour cette stratégie.</span><span class="sxs-lookup"><span data-stu-id="082c7-134">If hello policy that you want tooadd is not enabled, ensure that you are in hello correct scope for that policy.</span></span> <span data-ttu-id="082c7-135">Chaque instruction de stratégie est conçue pour une utilisation dans certaines étendues et sections de la stratégie.</span><span class="sxs-lookup"><span data-stu-id="082c7-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="082c7-136">sections de stratégie tooreview hello et étendues pour une stratégie, vérifiez hello **utilisation** section pour cette stratégie Bonjour [référence de stratégie][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="082c7-136">tooreview hello policy sections and scopes for a policy, check hello **Usage** section for that policy in hello [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="082c7-137">Une liste complète des instructions de stratégie et leurs paramètres sont disponibles dans hello [référence de stratégie][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="082c7-137">A full list of policy statements and their settings are available in hello [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="082c7-138">Par exemple, tooadd un nouveau toorestrict d’instruction entrant demande toospecified des adresses IP, placez le curseur hello à l’intérieur de contenu hello Hello `inbound` hello d’élément et cliquez sur XML **Restrict appelant IPs** instruction.</span><span class="sxs-lookup"><span data-stu-id="082c7-138">For example, tooadd a new statement toorestrict incoming requests toospecified IP addresses, place hello cursor just inside hello content of hello `inbound` XML element and click hello **Restrict caller IPs** statement.</span></span>

![Restriction policies][policies-restrict]

<span data-ttu-id="082c7-140">Cette opération ajoute une toohello d’extrait de code XML `inbound` élément qui fournit des conseils sur la façon dont tooconfigure hello instruction.</span><span class="sxs-lookup"><span data-stu-id="082c7-140">This will add an XML snippet toohello `inbound` element that provides guidance on how tooconfigure hello statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="082c7-141">toolimit les demandes entrantes et acceptez uniquement les à partir d’une adresse IP 1.2.3.4 modifier hello XML comme suit :</span><span class="sxs-lookup"><span data-stu-id="082c7-141">toolimit inbound requests and accept only those from an IP address of 1.2.3.4 modify hello XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Enregistrer][policies-save]

<span data-ttu-id="082c7-143">Configuration des instructions hello pour la stratégie de hello terminé, cliquez sur **enregistrer** et modifications de hello seront passerelle de gestion des API toohello propagées immédiatement.</span><span class="sxs-lookup"><span data-stu-id="082c7-143">When complete configuring hello statements for hello policy, click **Save** and hello changes will be propagated toohello API Management gateway immediately.</span></span>

## <span data-ttu-id="082c7-144"><a name="sections"></a>Configuration de la stratégie</span><span class="sxs-lookup"><span data-stu-id="082c7-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="082c7-145">Une stratégie est une série d'instructions qui s'exécutent dans l'ordre pour une demande et une réponse.</span><span class="sxs-lookup"><span data-stu-id="082c7-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="082c7-146">configuration de Hello est divisée en conséquence `inbound`, `backend`, `outbound`, et `on-error` sections comme indiqué dans la configuration suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="082c7-146">hello configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in hello following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements toobe applied toohello request go here -->
  </inbound>
  <backend>
    <!-- statements toobe applied before hello request is forwarded too
         hello backend service go here -->
  </backend>
  <outbound>
    <!-- statements toobe applied toohello response go here -->
  </outbound>
  <on-error>
    <!-- statements toobe applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="082c7-147">S’il existe une erreur lors du traitement de hello d’une demande, les autres étapes Bonjour `inbound`, `backend`, ou `outbound` sections sont ignorées et l’exécution passe instructions toohello Bonjour `on-error` section.</span><span class="sxs-lookup"><span data-stu-id="082c7-147">If there is an error during hello processing of a request, any remaining steps in hello `inbound`, `backend`, or `outbound` sections are skipped and execution jumps toohello statements in hello `on-error` section.</span></span> <span data-ttu-id="082c7-148">En plaçant des instructions de stratégie Bonjour `on-error` section, vous pouvez consulter les erreurs hello à l’aide de hello `context.LastError` propriété, examiner et personnaliser la réponse d’erreur hello à l’aide de hello `set-body` stratégie et configurer que se passe-t-il si une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="082c7-148">By placing policy statements in hello `on-error` section you can review hello error by using hello `context.LastError` property, inspect and customize hello error response using hello `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="082c7-149">Il existe des codes d’erreur pour obtenir des instructions intégrées et les erreurs qui peuvent se produire pendant le traitement de hello des instructions de stratégie.</span><span class="sxs-lookup"><span data-stu-id="082c7-149">There are error codes for built-in steps and for errors that may occur during hello processing of policy statements.</span></span> <span data-ttu-id="082c7-150">Pour plus d'informations, consultez [Gestion des erreurs dans les stratégies de gestion des API](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span><span class="sxs-lookup"><span data-stu-id="082c7-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="082c7-151">Étant donné que les stratégies peuvent être spécifiés à différents niveaux (globale, produit, api et operation) hello configuration offre un moyen vous ordre de hello toospecify dans laquelle les instructions de définition de stratégie hello s’exécutent avec la stratégie de respect toohello parent.</span><span class="sxs-lookup"><span data-stu-id="082c7-151">Since policies can be specified at different levels (global, product, api and operation) hello configuration provides a way for you toospecify hello order in which hello policy definition's statements execute with respect toohello parent policy.</span></span> 

<span data-ttu-id="082c7-152">Étendues de stratégie sont évalués dans hello suivant l’ordre.</span><span class="sxs-lookup"><span data-stu-id="082c7-152">Policy scopes are evaluated in hello following order.</span></span>

1. <span data-ttu-id="082c7-153">Étendue globale</span><span class="sxs-lookup"><span data-stu-id="082c7-153">Global scope</span></span>
2. <span data-ttu-id="082c7-154">Étendue produit</span><span class="sxs-lookup"><span data-stu-id="082c7-154">Product scope</span></span>
3. <span data-ttu-id="082c7-155">Étendue API</span><span class="sxs-lookup"><span data-stu-id="082c7-155">API scope</span></span>
4. <span data-ttu-id="082c7-156">Étendue opération</span><span class="sxs-lookup"><span data-stu-id="082c7-156">Operation scope</span></span>

<span data-ttu-id="082c7-157">Hello instructions au sein de celles-ci sont évaluées en fonction de la sélection élective toohello Hello `base` élément, s’il est présent.</span><span class="sxs-lookup"><span data-stu-id="082c7-157">hello statements within them are evaluated according toohello placement of hello `base` element, if it is present.</span></span> <span data-ttu-id="082c7-158">La stratégie globale a aucune stratégie parent et à l’aide de hello `<base>` élément qu’il n’a aucun effet.</span><span class="sxs-lookup"><span data-stu-id="082c7-158">Global policy has no parent policy and using hello `<base>` element in it has no effect.</span></span>

<span data-ttu-id="082c7-159">Par exemple, si vous avez une stratégie au niveau global de hello et une stratégie configurée pour une API, puis chaque fois que cette API particulière est utilisée les deux stratégies sont appliquées.</span><span class="sxs-lookup"><span data-stu-id="082c7-159">For example, if you have a policy at hello global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="082c7-160">Gestion des API permettant d’ordre déterministe des instructions de stratégie combinée via l’élément de base hello.</span><span class="sxs-lookup"><span data-stu-id="082c7-160">API Management allows for deterministic ordering of combined policy statements via hello base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="082c7-161">Dans la définition de stratégie exemple hello ci-dessus, hello `cross-domain` instruction exécuterait avant les stratégies plus élevées, qui à leur tour, être suivie hello `find-and-replace` stratégie.</span><span class="sxs-lookup"><span data-stu-id="082c7-161">In hello example policy definition above, hello `cross-domain` statement would execute before any higher policies which would in turn, be followed by hello `find-and-replace` policy.</span></span> 

<span data-ttu-id="082c7-162">stratégies de hello toosee dans l’étendue actuelle de hello dans l’éditeur de stratégie de hello, cliquez sur **recalculer la stratégie effective pour l’étendue sélectionnée**.</span><span class="sxs-lookup"><span data-stu-id="082c7-162">toosee hello policies in hello current scope in hello policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="082c7-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="082c7-163">Next steps</span></span>
<span data-ttu-id="082c7-164">Découvrez la vidéo suivante sur les expressions de stratégie.</span><span class="sxs-lookup"><span data-stu-id="082c7-164">Check out following video on policy expressions.</span></span>

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
