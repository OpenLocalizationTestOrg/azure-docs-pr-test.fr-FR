---
title: aaaAdd mise en cache des performances tooimprove dans Gestion des API Azure | Documents Microsoft
description: "Découvrez comment tooimprove hello latence, la consommation de bande passante et service web de charge pour les appels de service de gestion des API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 740f6a27-8323-474d-ade2-828ae0c75e7a
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 056ab7cf788218327e30bd5c028b76e3b1977fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-caching-tooimprove-performance-in-azure-api-management"></a><span data-ttu-id="9da95-103">Ajouter des performances tooimprove mise en cache dans la gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="9da95-103">Add caching tooimprove performance in Azure API Management</span></span>
<span data-ttu-id="9da95-104">Les opérations dans Gestion des API Azure peuvent être configurées pour mettre en cache la réponse.</span><span class="sxs-lookup"><span data-stu-id="9da95-104">Operations in API Management can be configured for response caching.</span></span> <span data-ttu-id="9da95-105">La mise en cache de la réponse peut réduire de façon importante la latence de l'API, la consommation de bande passante et la charge du service web pour les données qui ne changent pas fréquemment.</span><span class="sxs-lookup"><span data-stu-id="9da95-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span></span>

<span data-ttu-id="9da95-106">Ce guide vous montre comment tooadd réponse mise en cache pour votre API et de configurer des stratégies pour les opérations de l’API d’écho exemple hello.</span><span class="sxs-lookup"><span data-stu-id="9da95-106">This guide shows you how tooadd response caching for your API and configure policies for hello sample Echo API operations.</span></span> <span data-ttu-id="9da95-107">Vous pouvez ensuite appeler l’opération de hello de hello développeur tooverify portail mise en cache en action.</span><span class="sxs-lookup"><span data-stu-id="9da95-107">You can then call hello operation from hello developer portal tooverify caching in action.</span></span>

> [!NOTE]
> <span data-ttu-id="9da95-108">Pour plus d’informations sur la mise en cache des éléments par clé à l’aide d’expressions de stratégie, consultez [Mise en cache personnalisée dans la gestion des API Azure](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="9da95-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="9da95-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9da95-109">Prerequisites</span></span>
<span data-ttu-id="9da95-110">Avant de hello suivant les étapes de ce guide, vous devez disposer d’une instance de service de gestion des API avec une API et un produit configuré.</span><span class="sxs-lookup"><span data-stu-id="9da95-110">Before following hello steps in this guide, you must have an API Management service instance with an API and a product configured.</span></span> <span data-ttu-id="9da95-111">Si vous n’avez pas encore créé une instance de service de gestion des API, consultez [de créer une instance de service de gestion des API] [ Create an API Management service instance] Bonjour [prise en main Azure API Management] [ Get started with Azure API Management] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9da95-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

## <span data-ttu-id="9da95-112"><a name="configure-caching"></a>Configuration d’une opération de mise en cache</span><span class="sxs-lookup"><span data-stu-id="9da95-112"><a name="configure-caching"> </a>Configure an operation for caching</span></span>
<span data-ttu-id="9da95-113">Dans cette étape, vous allez examiner hello mise en cache des paramètres de hello **obtenir des ressources (mise en cache)** l’opération de l’exemple hello Echo API.</span><span class="sxs-lookup"><span data-stu-id="9da95-113">In this step, you will review hello caching settings of hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

> [!NOTE]
> <span data-ttu-id="9da95-114">Chaque instance de service de gestion des API est préconfiguré avec une API d’écho qui peuvent être utilisé tooexperiment avec et en savoir plus sur la gestion des API.</span><span class="sxs-lookup"><span data-stu-id="9da95-114">Each API Management service instance comes preconfigured with an Echo API that can be used tooexperiment with and learn about API Management.</span></span> <span data-ttu-id="9da95-115">Pour plus d'informations, consultez la page [Prise en main de Gestion des API Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="9da95-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span></span>
> 
> 

<span data-ttu-id="9da95-116">tooget démarré, cliquez sur **portail de publication** Bonjour portail Azure pour votre service de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="9da95-116">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span> <span data-ttu-id="9da95-117">Cela vous prend un portail de publication de gestion des API toohello.</span><span class="sxs-lookup"><span data-stu-id="9da95-117">This takes you toohello API Management publisher portal.</span></span>

![Portail des éditeurs][api-management-management-console]

<span data-ttu-id="9da95-119">Cliquez sur **API** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="9da95-119">Click **APIs** from hello **API Management** menu on hello left, and then click **Echo API**.</span></span>

![API Echo][api-management-echo-api]

<span data-ttu-id="9da95-121">Cliquez sur hello **Operations** onglet, puis cliquez sur hello **obtenir des ressources (mise en cache)** opération hello **Operations** liste.</span><span class="sxs-lookup"><span data-stu-id="9da95-121">Click hello **Operations** tab, and then click hello **GET Resource (cached)** operation from hello **Operations** list.</span></span>

![Echo API operations][api-management-echo-api-operations]

<span data-ttu-id="9da95-123">Cliquez sur hello **mise en cache** hello de tooview onglet mise en cache des paramètres pour cette opération.</span><span class="sxs-lookup"><span data-stu-id="9da95-123">Click hello **Caching** tab tooview hello caching settings for this operation.</span></span>

![Caching tab][api-management-caching-tab]

<span data-ttu-id="9da95-125">tooenable mise en cache pour une opération, sélectionnez hello **activer** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="9da95-125">tooenable caching for an operation, select hello **Enable** check box.</span></span> <span data-ttu-id="9da95-126">Dans cet exemple, la mise en cache est activée.</span><span class="sxs-lookup"><span data-stu-id="9da95-126">In this example, caching is enabled.</span></span>

<span data-ttu-id="9da95-127">Chaque réponse de l’opération est indexé, en fonction des valeurs hello hello **variation par paramètres de chaîne de requête** et **variation par en-têtes** champs.</span><span class="sxs-lookup"><span data-stu-id="9da95-127">Each operation response is keyed, based on hello values in hello **Vary by query string parameters** and **Vary by headers** fields.</span></span> <span data-ttu-id="9da95-128">Si vous souhaitez toocache plusieurs réponses selon les paramètres de chaîne de requête ou les en-têtes, vous pouvez les configurer dans ces deux champs.</span><span class="sxs-lookup"><span data-stu-id="9da95-128">If you want toocache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span></span>

<span data-ttu-id="9da95-129">**Durée** Spécifie l’intervalle d’expiration de hello des réponses de hello mis en cache.</span><span class="sxs-lookup"><span data-stu-id="9da95-129">**Duration** specifies hello expiration interval of hello cached responses.</span></span> <span data-ttu-id="9da95-130">Dans cet exemple, l’intervalle de salutation est **3600** secondes, ce qui est équivalent tooone heure.</span><span class="sxs-lookup"><span data-stu-id="9da95-130">In this example, hello interval is **3600** seconds, which is equivalent tooone hour.</span></span>

<span data-ttu-id="9da95-131">À l’aide de hello mise en cache de configuration dans cet exemple, hello première demande toohello **obtenir des ressources (mise en cache)** opération renvoie une réponse à partir du service principal de hello.</span><span class="sxs-lookup"><span data-stu-id="9da95-131">Using hello caching configuration in this example, hello first request toohello **GET Resource (cached)** operation returns a response from hello backend service.</span></span> <span data-ttu-id="9da95-132">Cette réponse est mises en cache, indexé par hello spécifié paramètres de chaîne de requête et les en-têtes.</span><span class="sxs-lookup"><span data-stu-id="9da95-132">This response will be cached, keyed by hello specified headers and query string parameters.</span></span> <span data-ttu-id="9da95-133">Les appels suivants toohello opération, avec des paramètres, de correspondance aura hello mis en cache la réponse retourné, jusqu'à ce que l’intervalle de durée hello du cache a expiré.</span><span class="sxs-lookup"><span data-stu-id="9da95-133">Subsequent calls toohello operation, with matching parameters, will have hello cached response returned, until hello cache duration interval has expired.</span></span>

## <span data-ttu-id="9da95-134"><a name="caching-policies"></a>Hello révision des stratégies de mise en cache</span><span class="sxs-lookup"><span data-stu-id="9da95-134"><a name="caching-policies"> </a>Review hello caching policies</span></span>
<span data-ttu-id="9da95-135">Dans cette étape, vous passez en revue hello mise en cache des paramètres pour hello **obtenir des ressources (mise en cache)** l’opération de l’exemple hello Echo API.</span><span class="sxs-lookup"><span data-stu-id="9da95-135">In this step, you review hello caching settings for hello **GET Resource (cached)** operation of hello sample Echo API.</span></span>

<span data-ttu-id="9da95-136">Lorsque les paramètres de mise en cache sont configurés pour une opération sur hello **mise en cache** sous l’onglet mise en cache des stratégies sont ajoutés pour l’opération de hello.</span><span class="sxs-lookup"><span data-stu-id="9da95-136">When caching settings are configured for an operation on hello **Caching** tab, caching policies are added for hello operation.</span></span> <span data-ttu-id="9da95-137">Ces stratégies peuvent être affichées et modifiées dans l’éditeur de stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="9da95-137">These policies can be viewed and edited in hello policy editor.</span></span>

<span data-ttu-id="9da95-138">Cliquez sur **stratégies** de hello **gestion des API** menu hello gauche et sélectionnez **Echo API / obtenir des ressources (mise en cache)** de hello **opération**liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="9da95-138">Click **Policies** from hello **API Management** menu on hello left, and then select **Echo API / GET Resource (cached)** from hello **Operation** drop-down list.</span></span>

![Policy scope operation][api-management-operation-dropdown]

<span data-ttu-id="9da95-140">Cela affiche les stratégies de hello pour cette opération dans l’éditeur de stratégie hello.</span><span class="sxs-lookup"><span data-stu-id="9da95-140">This displays hello policies for this operation in hello policy editor.</span></span>

![API Management policy editor][api-management-policy-editor]

<span data-ttu-id="9da95-142">définition de la stratégie Hello pour cette opération inclut hello stratégies qui définissent hello mise en cache de configuration qui ont été vérifiés à l’aide de hello **mise en cache** onglet à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="9da95-142">hello policy definition for this operation includes hello policies that define hello caching configuration that were reviewed using hello **Caching** tab in hello previous step.</span></span>

```xml
<policies>
    <inbound>
        <base />
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false">
            <vary-by-header>Accept</vary-by-header>
            <vary-by-header>Accept-Charset</vary-by-header>
        </cache-lookup>
        <rewrite-uri template="/resource" />
    </inbound>
    <outbound>
        <base />
        <cache-store caching-mode="cache-on" duration="3600" />
    </outbound>
</policies>
```

> [!NOTE]
> <span data-ttu-id="9da95-143">Toohello modifications mise en cache des stratégies dans l’éditeur de stratégie hello apparaîtront sur hello **mise en cache** onglet d’une opération et vice versa.</span><span class="sxs-lookup"><span data-stu-id="9da95-143">Changes made toohello caching policies in hello policy editor will be reflected on hello **Caching** tab of an operation, and vice-versa.</span></span>
> 
> 

## <span data-ttu-id="9da95-144"><a name="test-operation"></a>Appeler une opération et tester la mise en cache hello</span><span class="sxs-lookup"><span data-stu-id="9da95-144"><a name="test-operation"> </a>Call an operation and test hello caching</span></span>
<span data-ttu-id="9da95-145">toosee hello mise en cache en action, nous pouvons appeler l’opération de hello à partir du portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="9da95-145">toosee hello caching in action, we can call hello operation from hello developer portal.</span></span> <span data-ttu-id="9da95-146">Cliquez sur **portail des développeurs** dans le menu supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="9da95-146">Click **Developer portal** in hello top right menu.</span></span>

![Portail des développeurs][api-management-developer-portal-menu]

<span data-ttu-id="9da95-148">Cliquez sur **API** dans hello menu supérieur, puis sélectionnez **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="9da95-148">Click **APIs** in hello top menu, and then select **Echo API**.</span></span>

![API Echo][api-management-apis-echo-api]

> <span data-ttu-id="9da95-150">Si vous n'avez qu’une seule API configurée ou tooyour visible compte, puis en cliquant sur API vous amène directement operations toohello pour cette API.</span><span class="sxs-lookup"><span data-stu-id="9da95-150">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="9da95-151">Sélectionnez hello **obtenir des ressources (mise en cache)** opération, puis cliquez sur **ouvrir la Console**.</span><span class="sxs-lookup"><span data-stu-id="9da95-151">Select hello **GET Resource (cached)** operation, and then click **Open Console**.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="9da95-153">Hello console permet les opérations tooinvoke directement depuis le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="9da95-153">hello console allows you tooinvoke operations directly from hello developer portal.</span></span>

![Console][api-management-console]

<span data-ttu-id="9da95-155">Conserver les valeurs par défaut de hello **param1** et **param2**.</span><span class="sxs-lookup"><span data-stu-id="9da95-155">Keep hello default values for **param1** and **param2**.</span></span>

<span data-ttu-id="9da95-156">Sélectionnez hello clé souhaitée à partir de hello **clé d’abonnement** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="9da95-156">Select hello desired key from hello **subscription-key** drop-down list.</span></span> <span data-ttu-id="9da95-157">Si votre compte n’a qu’un abonnement, celui-ci est déjà sélectionné.</span><span class="sxs-lookup"><span data-stu-id="9da95-157">If your account has only one subscription, it will already be selected.</span></span>

<span data-ttu-id="9da95-158">Entrez **sampleheader:value1** Bonjour **en-têtes de demande** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="9da95-158">Enter **sampleheader:value1** in hello **Request headers** text box.</span></span>

<span data-ttu-id="9da95-159">Cliquez sur **HTTP Get** et prenez note de hello en-têtes de réponse.</span><span class="sxs-lookup"><span data-stu-id="9da95-159">Click **HTTP Get** and make a note of hello response headers.</span></span>

<span data-ttu-id="9da95-160">Entrez **sampleheader:value2** Bonjour **en-têtes de demande** zone de texte, puis cliquez sur **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="9da95-160">Enter **sampleheader:value2** in hello **Request headers** text box, and then click **HTTP Get**.</span></span>

<span data-ttu-id="9da95-161">Notez que valeur hello de **sampleheader** est toujours **value1** dans la réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="9da95-161">Note that hello value of **sampleheader** is still **value1** in hello response.</span></span> <span data-ttu-id="9da95-162">Essayez certaines des valeurs différentes, et notez que hello réponse mise en cache à partir du premier appel de hello est retournée.</span><span class="sxs-lookup"><span data-stu-id="9da95-162">Try some different values and note that hello cached response from hello first call is returned.</span></span>

<span data-ttu-id="9da95-163">Entrez **25** dans hello **param2** champ, puis cliquez sur **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="9da95-163">Enter **25** into hello **param2** field, and then click **HTTP Get**.</span></span>

<span data-ttu-id="9da95-164">Notez que valeur hello de **sampleheader** Bonjour réponse est désormais **value2**.</span><span class="sxs-lookup"><span data-stu-id="9da95-164">Note that hello value of **sampleheader** in hello response is now **value2**.</span></span> <span data-ttu-id="9da95-165">Étant donné que les résultats de l’opération hello sont indexées par chaîne de requête, la réponse mise en cache de hello précédente n’a pas retourné.</span><span class="sxs-lookup"><span data-stu-id="9da95-165">Because hello operation results are keyed by query string, hello previous cached response was not returned.</span></span>

## <span data-ttu-id="9da95-166"><a name="next-steps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9da95-166"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="9da95-167">Pour plus d’informations sur la mise en cache des stratégies, consultez [mise en cache des stratégies] [ Caching policies] Bonjour [référence de stratégie de gestion des API][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="9da95-167">For more information about caching policies, see [Caching policies][Caching policies] in hello [API Management policy reference][API Management policy reference].</span></span>
* <span data-ttu-id="9da95-168">Pour plus d’informations sur la mise en cache des éléments par clé à l’aide d’expressions de stratégie, consultez [Mise en cache personnalisée dans la gestion des API Azure](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="9da95-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>

[api-management-management-console]: ./media/api-management-howto-cache/api-management-management-console.png
[api-management-echo-api]: ./media/api-management-howto-cache/api-management-echo-api.png
[api-management-echo-api-operations]: ./media/api-management-howto-cache/api-management-echo-api-operations.png
[api-management-caching-tab]: ./media/api-management-howto-cache/api-management-caching-tab.png
[api-management-operation-dropdown]: ./media/api-management-howto-cache/api-management-operation-dropdown.png
[api-management-policy-editor]: ./media/api-management-howto-cache/api-management-policy-editor.png
[api-management-developer-portal-menu]: ./media/api-management-howto-cache/api-management-developer-portal-menu.png
[api-management-apis-echo-api]: ./media/api-management-howto-cache/api-management-apis-echo-api.png
[api-management-open-console]: ./media/api-management-howto-cache/api-management-open-console.png
[api-management-console]: ./media/api-management-howto-cache/api-management-console.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review hello caching policies]: #caching-policies
[Call an operation and test hello caching]: #test-operation
[Next steps]: #next-steps
