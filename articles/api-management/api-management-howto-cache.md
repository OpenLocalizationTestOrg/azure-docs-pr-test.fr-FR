---
title: "Ajout de la mise en cache pour améliorer les performances de Gestion des API Azure | Microsoft Docs"
description: "Apprenez à améliorer la latence, la consommation de bande passante et la charge du service web pour les appels du service Gestion des API."
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
ms.openlocfilehash: 59c595f0d5ce849f44c46fdb6cab0b44d35fffa0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-caching-to-improve-performance-in-azure-api-management"></a><span data-ttu-id="343e8-103">Ajout de mise en cache pour améliorer les performances dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="343e8-103">Add caching to improve performance in Azure API Management</span></span>
<span data-ttu-id="343e8-104">Les opérations dans Gestion des API Azure peuvent être configurées pour mettre en cache la réponse.</span><span class="sxs-lookup"><span data-stu-id="343e8-104">Operations in API Management can be configured for response caching.</span></span> <span data-ttu-id="343e8-105">La mise en cache de la réponse peut réduire de façon importante la latence de l'API, la consommation de bande passante et la charge du service web pour les données qui ne changent pas fréquemment.</span><span class="sxs-lookup"><span data-stu-id="343e8-105">Response caching can significantly reduce API latency, bandwidth consumption, and web service load for data that does not change frequently.</span></span>

<span data-ttu-id="343e8-106">Ce guide vous montre comment ajouter une mise en cache de la réponse pour votre API et configurer des stratégies pour les exemples d’opérations de l’API Echo.</span><span class="sxs-lookup"><span data-stu-id="343e8-106">This guide shows you how to add response caching for your API and configure policies for the sample Echo API operations.</span></span> <span data-ttu-id="343e8-107">Vous pouvez ensuite appeler l’opération depuis le portail des développeurs pour vérifier l’action de mise en cache.</span><span class="sxs-lookup"><span data-stu-id="343e8-107">You can then call the operation from the developer portal to verify caching in action.</span></span>

> [!NOTE]
> <span data-ttu-id="343e8-108">Pour plus d’informations sur la mise en cache des éléments par clé à l’aide d’expressions de stratégie, consultez [Mise en cache personnalisée dans la gestion des API Azure](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="343e8-108">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="343e8-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="343e8-109">Prerequisites</span></span>
<span data-ttu-id="343e8-110">Avant de suivre la procédure décrite dans ce guide, vous devez disposer d’une instance de service de Gestion des API avec une API et un produit configurés.</span><span class="sxs-lookup"><span data-stu-id="343e8-110">Before following the steps in this guide, you must have an API Management service instance with an API and a product configured.</span></span> <span data-ttu-id="343e8-111">Si vous n’avez pas encore créé une instance de service Gestion des API, consultez la page de [création d’une instance de service Gestion des API][Create an API Management service instance] dans le didacticiel de [prise en main de Gestion des API Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="343e8-111">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>

## <span data-ttu-id="343e8-112"><a name="configure-caching"> </a>Configuration d’une opération de mise en cache</span><span class="sxs-lookup"><span data-stu-id="343e8-112"><a name="configure-caching"> </a>Configure an operation for caching</span></span>
<span data-ttu-id="343e8-113">Dans cette étape, vous allez consulter les paramètres de mise en cache de l’opération **GET Resource (cached)** de l’exemple d’API Echo.</span><span class="sxs-lookup"><span data-stu-id="343e8-113">In this step, you will review the caching settings of the **GET Resource (cached)** operation of the sample Echo API.</span></span>

> [!NOTE]
> <span data-ttu-id="343e8-114">Chaque instance du service Gestion des API est préconfigurée avec une API Echo qui peut être utilisée pour faire des expériences et en savoir plus sur la gestion des API.</span><span class="sxs-lookup"><span data-stu-id="343e8-114">Each API Management service instance comes preconfigured with an Echo API that can be used to experiment with and learn about API Management.</span></span> <span data-ttu-id="343e8-115">Pour plus d'informations, consultez la page [Prise en main de Gestion des API Azure][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="343e8-115">For more information, see [Get started with Azure API Management][Get started with Azure API Management].</span></span>
> 
> 

<span data-ttu-id="343e8-116">Pour commencer, cliquez sur **Portail des éditeurs** dans le portail Azure de votre service Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="343e8-116">To get started, click **Publisher portal** in the Azure Portal for your API Management service.</span></span> <span data-ttu-id="343e8-117">Vous accédez au portail des éditeurs Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="343e8-117">This takes you to the API Management publisher portal.</span></span>

![Portail des éditeurs][api-management-management-console]

<span data-ttu-id="343e8-119">Cliquez sur **API** dans le menu **Gestion des API** à gauche, puis sur **API Echo**.</span><span class="sxs-lookup"><span data-stu-id="343e8-119">Click **APIs** from the **API Management** menu on the left, and then click **Echo API**.</span></span>

![API Echo][api-management-echo-api]

<span data-ttu-id="343e8-121">Cliquez sur l’onglet **Opérations**, puis sur l’opération **GET Resource (cached)** dans la liste **Opérations**.</span><span class="sxs-lookup"><span data-stu-id="343e8-121">Click the **Operations** tab, and then click the **GET Resource (cached)** operation from the **Operations** list.</span></span>

![Echo API operations][api-management-echo-api-operations]

<span data-ttu-id="343e8-123">Cliquez sur l’onglet **Mise en cache** pour consulter les paramètres de mise en cache de cette opération.</span><span class="sxs-lookup"><span data-stu-id="343e8-123">Click the **Caching** tab to view the caching settings for this operation.</span></span>

![Caching tab][api-management-caching-tab]

<span data-ttu-id="343e8-125">Pour activer la mise en cache pour une opération, sélectionnez la case à cocher **Activer** .</span><span class="sxs-lookup"><span data-stu-id="343e8-125">To enable caching for an operation, select the **Enable** check box.</span></span> <span data-ttu-id="343e8-126">Dans cet exemple, la mise en cache est activée.</span><span class="sxs-lookup"><span data-stu-id="343e8-126">In this example, caching is enabled.</span></span>

<span data-ttu-id="343e8-127">Chaque réponse de l’opération est générée en fonction des valeurs des champs **Variation par paramètres de chaîne de requête** et **Variation par en-têtes**.</span><span class="sxs-lookup"><span data-stu-id="343e8-127">Each operation response is keyed, based on the values in the **Vary by query string parameters** and **Vary by headers** fields.</span></span> <span data-ttu-id="343e8-128">Si vous souhaitez mettre en cache plusieurs réponses en fonction des paramètres ou des en-têtes de la chaîne de requête, vous pouvez les configurer dans ces deux champs.</span><span class="sxs-lookup"><span data-stu-id="343e8-128">If you want to cache multiple responses based on query string parameters or headers, you can configure them in these two fields.</span></span>

<span data-ttu-id="343e8-129">**Durée** spécifie l'intervalle d'expiration des réponses mises en cache.</span><span class="sxs-lookup"><span data-stu-id="343e8-129">**Duration** specifies the expiration interval of the cached responses.</span></span> <span data-ttu-id="343e8-130">Dans cet exemple, l’intervalle est de **3600** secondes, ce qui équivaut à une heure.</span><span class="sxs-lookup"><span data-stu-id="343e8-130">In this example, the interval is **3600** seconds, which is equivalent to one hour.</span></span>

<span data-ttu-id="343e8-131">Selon la configuration de mise en cache de cet exemple, la première demande envoyée à l’opération **GET Resource (cached)** renvoie une réponse du service principal.</span><span class="sxs-lookup"><span data-stu-id="343e8-131">Using the caching configuration in this example, the first request to the **GET Resource (cached)** operation returns a response from the backend service.</span></span> <span data-ttu-id="343e8-132">Cette réponse sera mise en cache, du fait des en-têtes et des paramètres de chaîne de requête spécifiés.</span><span class="sxs-lookup"><span data-stu-id="343e8-132">This response will be cached, keyed by the specified headers and query string parameters.</span></span> <span data-ttu-id="343e8-133">Les autres appels à l'opération comportant des paramètres correspondants recevront la réponse mise en cache, jusqu'à expiration de la durée de mise en cache.</span><span class="sxs-lookup"><span data-stu-id="343e8-133">Subsequent calls to the operation, with matching parameters, will have the cached response returned, until the cache duration interval has expired.</span></span>

## <span data-ttu-id="343e8-134"><a name="caching-policies"> </a>Révision des stratégies de mise en cache</span><span class="sxs-lookup"><span data-stu-id="343e8-134"><a name="caching-policies"> </a>Review the caching policies</span></span>
<span data-ttu-id="343e8-135">Dans cette étape, vous allez consulter les paramètres de mise en cache de l’opération **GET Resource (cached)** de l’exemple d’API Echo.</span><span class="sxs-lookup"><span data-stu-id="343e8-135">In this step, you review the caching settings for the **GET Resource (cached)** operation of the sample Echo API.</span></span>

<span data-ttu-id="343e8-136">Lorsque les paramètres de mise en cache sont configurés pour une opération dans l'onglet **Mise en cache** , les stratégies de mise en cache sont ajoutées pour cette opération.</span><span class="sxs-lookup"><span data-stu-id="343e8-136">When caching settings are configured for an operation on the **Caching** tab, caching policies are added for the operation.</span></span> <span data-ttu-id="343e8-137">Ces stratégies peuvent être consultées et modifiées dans l'éditeur de stratégies.</span><span class="sxs-lookup"><span data-stu-id="343e8-137">These policies can be viewed and edited in the policy editor.</span></span>

<span data-ttu-id="343e8-138">Cliquez sur **Stratégies** dans le menu **Gestion des API** à gauche, puis sélectionnez **Echo API / GET Resource (cached)** dans la liste déroulante **Opération**.</span><span class="sxs-lookup"><span data-stu-id="343e8-138">Click **Policies** from the **API Management** menu on the left, and then select **Echo API / GET Resource (cached)** from the **Operation** drop-down list.</span></span>

![Policy scope operation][api-management-operation-dropdown]

<span data-ttu-id="343e8-140">Affiche les stratégies de cette opération dans l'éditeur de stratégies.</span><span class="sxs-lookup"><span data-stu-id="343e8-140">This displays the policies for this operation in the policy editor.</span></span>

![API Management policy editor][api-management-policy-editor]

<span data-ttu-id="343e8-142">La définition de stratégie de cette opération comprend les stratégies qui définissent la configuration de la mise en cache que nous avons vues dans l'onglet **Mise en cache** lors de l'étape précédente.</span><span class="sxs-lookup"><span data-stu-id="343e8-142">The policy definition for this operation includes the policies that define the caching configuration that were reviewed using the **Caching** tab in the previous step.</span></span>

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
> <span data-ttu-id="343e8-143">Les modifications apportées aux stratégies de mise en cache dans l’éditeur de stratégies sont affichées sous l’onglet **Mise en cache** d’une opération, et vice-versa.</span><span class="sxs-lookup"><span data-stu-id="343e8-143">Changes made to the caching policies in the policy editor will be reflected on the **Caching** tab of an operation, and vice-versa.</span></span>
> 
> 

## <span data-ttu-id="343e8-144"><a name="test-operation"> </a>Appel d’une opération et test de la mise en cache</span><span class="sxs-lookup"><span data-stu-id="343e8-144"><a name="test-operation"> </a>Call an operation and test the caching</span></span>
<span data-ttu-id="343e8-145">Pour voir la mise en cache en action, nous pouvons appeler l'opération depuis le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="343e8-145">To see the caching in action, we can call the operation from the developer portal.</span></span> <span data-ttu-id="343e8-146">Cliquez sur **Portail de développement** dans le menu supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="343e8-146">Click **Developer portal** in the top right menu.</span></span>

![Portail des développeurs][api-management-developer-portal-menu]

<span data-ttu-id="343e8-148">Cliquez sur **API** dans le menu supérieur, puis sélectionnez **API Echo**.</span><span class="sxs-lookup"><span data-stu-id="343e8-148">Click **APIs** in the top menu, and then select **Echo API**.</span></span>

![API Echo][api-management-apis-echo-api]

> <span data-ttu-id="343e8-150">Si vous n'avez qu'une API configurée ou visible dans votre compte, cliquez sur des API pour accéder directement aux opérations associées.</span><span class="sxs-lookup"><span data-stu-id="343e8-150">If you have only one API configured or visible to your account, then clicking APIs takes you directly to the operations for that API.</span></span>
> 
> 

<span data-ttu-id="343e8-151">Sélectionnez l’opération **Ressource GET (cached)**, puis cliquez sur **Ouvrir la console**.</span><span class="sxs-lookup"><span data-stu-id="343e8-151">Select the **GET Resource (cached)** operation, and then click **Open Console**.</span></span>

![Open console][api-management-open-console]

<span data-ttu-id="343e8-153">La console vous permet d'appeler des opérations directement depuis le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="343e8-153">The console allows you to invoke operations directly from the developer portal.</span></span>

![Console][api-management-console]

<span data-ttu-id="343e8-155">Conservez les valeurs par défaut de **param1** et **param2**.</span><span class="sxs-lookup"><span data-stu-id="343e8-155">Keep the default values for **param1** and **param2**.</span></span>

<span data-ttu-id="343e8-156">Sélectionnez la clé souhaitée dans la liste déroulante **subscription-key** .</span><span class="sxs-lookup"><span data-stu-id="343e8-156">Select the desired key from the **subscription-key** drop-down list.</span></span> <span data-ttu-id="343e8-157">Si votre compte n’a qu’un abonnement, celui-ci est déjà sélectionné.</span><span class="sxs-lookup"><span data-stu-id="343e8-157">If your account has only one subscription, it will already be selected.</span></span>

<span data-ttu-id="343e8-158">Entrez **sampleheader:value1** dans la zone de texte des **en-têtes de la demande**.</span><span class="sxs-lookup"><span data-stu-id="343e8-158">Enter **sampleheader:value1** in the **Request headers** text box.</span></span>

<span data-ttu-id="343e8-159">Cliquez sur **HTTP Get** et notez les en-têtes de réponse.</span><span class="sxs-lookup"><span data-stu-id="343e8-159">Click **HTTP Get** and make a note of the response headers.</span></span>

<span data-ttu-id="343e8-160">Entrez **sampleheader:value2** dans la zone de texte des **en-têtes de la demande**, puis cliquez sur **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="343e8-160">Enter **sampleheader:value2** in the **Request headers** text box, and then click **HTTP Get**.</span></span>

<span data-ttu-id="343e8-161">Notez que la valeur de **sampleheader** est toujours **value1** dans la réponse.</span><span class="sxs-lookup"><span data-stu-id="343e8-161">Note that the value of **sampleheader** is still **value1** in the response.</span></span> <span data-ttu-id="343e8-162">Essayez d'autres valeurs. Vous constatez que la réponse mise en cache lors du premier appel est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="343e8-162">Try some different values and note that the cached response from the first call is returned.</span></span>

<span data-ttu-id="343e8-163">Entrez **25** dans le champ **param2**, puis cliquez sur **HTTP Get**.</span><span class="sxs-lookup"><span data-stu-id="343e8-163">Enter **25** into the **param2** field, and then click **HTTP Get**.</span></span>

<span data-ttu-id="343e8-164">Notez que la valeur de **sampleheader** dans la réponse est désormais **value2**.</span><span class="sxs-lookup"><span data-stu-id="343e8-164">Note that the value of **sampleheader** in the response is now **value2**.</span></span> <span data-ttu-id="343e8-165">Comme les résultats de l'opération dépendent de la chaîne de requête, la réponse précédemment mise en cache n'est pas renvoyée.</span><span class="sxs-lookup"><span data-stu-id="343e8-165">Because the operation results are keyed by query string, the previous cached response was not returned.</span></span>

## <span data-ttu-id="343e8-166"><a name="next-steps"> </a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="343e8-166"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="343e8-167">Pour plus d’informations sur les stratégies de mise en cache, voir la section [Stratégies de mise en cache][Caching policies] dans [Référence de stratégie de Gestion des API][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="343e8-167">For more information about caching policies, see [Caching policies][Caching policies] in the [API Management policy reference][API Management policy reference].</span></span>
* <span data-ttu-id="343e8-168">Pour plus d’informations sur la mise en cache des éléments par clé à l’aide d’expressions de stratégie, consultez [Mise en cache personnalisée dans la gestion des API Azure](api-management-sample-cache-by-key.md).</span><span class="sxs-lookup"><span data-stu-id="343e8-168">For information on caching items by key using policy expressions, see [Custom caching in Azure API Management](api-management-sample-cache-by-key.md).</span></span>

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


[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md

[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx

[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[Configure an operation for caching]: #configure-caching
[Review the caching policies]: #caching-policies
[Call an operation and test the caching]: #test-operation
[Next steps]: #next-steps
