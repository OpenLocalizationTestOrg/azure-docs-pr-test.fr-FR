---
title: "Limitation de requêtes avancée avec Gestion des API Azure"
description: "Découvrez comment créer et appliquer des stratégies de limitation de fréquence et de quota souples avec Gestion des API Azure."
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: fc813a65-7793-4c17-8bb9-e387838193ae
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 35375e599891a9443a91c4c3a8657e8c9c48c7b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-request-throttling-with-azure-api-management"></a><span data-ttu-id="73a38-103">Limitation de requêtes avancée avec Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="73a38-103">Advanced request throttling with Azure API Management</span></span>
<span data-ttu-id="73a38-104">La possibilité de limiter les requêtes entrantes est un rôle clé du service Gestion des API Azure.</span><span class="sxs-lookup"><span data-stu-id="73a38-104">Being able to throttle incoming requests is a key role of Azure API Management.</span></span> <span data-ttu-id="73a38-105">En contrôlant la fréquence des requêtes ou le nombre total de requêtes/données transférées, Gestion des API permet aux fournisseurs d’API de protéger leurs API contre les abus et de créer de la valeur pour différents niveaux de produits API.</span><span class="sxs-lookup"><span data-stu-id="73a38-105">Either by controlling the rate of requests or the total requests/data transferred, API Management allows API providers to protect their APIs from abuse and create value for different API product tiers.</span></span>

## <a name="product-based-throttling"></a><span data-ttu-id="73a38-106">Limitation en fonction du produit</span><span class="sxs-lookup"><span data-stu-id="73a38-106">Product based throttling</span></span>
<span data-ttu-id="73a38-107">À ce jour, les fonctionnalités de limitation de fréquence sont limitées afin de porter sur un abonnement produit spécifique (essentiellement une clé), défini dans le portail des éditeurs de Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="73a38-107">To date, the rate throttling capabilities have been limited to being scoped to a particular Product subscription (essentially a key), defined in the API Management publisher portal.</span></span> <span data-ttu-id="73a38-108">Cela permet aux fournisseurs d'API d’appliquer des limites aux développeurs qui ont souscrit pour utiliser leurs API ; toutefois, cela ne permet pas, par exemple, de limiter les utilisateurs finaux des API.</span><span class="sxs-lookup"><span data-stu-id="73a38-108">This is useful for the API provider to apply limits on the developers who have signed up to use their API, however, it does not help, for example, in throttling individual end-users of the API.</span></span> <span data-ttu-id="73a38-109">Il est possible pour un seul utilisateur de l'application du développeur de consommer le quota entier et d’empêcher d’autres clients du développeur d'être en mesure d'utiliser l'application.</span><span class="sxs-lookup"><span data-stu-id="73a38-109">It is possible that for single user of the developer's application to consume the entire quota and then prevent other customers of the developer from being able to use the application.</span></span> <span data-ttu-id="73a38-110">De la même façon, plusieurs clients générant un volume élevé de requêtes peuvent limiter l'accès aux utilisateurs occasionnels.</span><span class="sxs-lookup"><span data-stu-id="73a38-110">Also, several customers who might generate a high volume of requests may limit access to occasional users.</span></span>

## <a name="custom-key-based-throttling"></a><span data-ttu-id="73a38-111">Limitation basée sur une clé personnalisée</span><span class="sxs-lookup"><span data-stu-id="73a38-111">Custom key based throttling</span></span>
<span data-ttu-id="73a38-112">Les nouvelles stratégies [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) et [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) fournissent une solution beaucoup plus souple pour le contrôle du trafic.</span><span class="sxs-lookup"><span data-stu-id="73a38-112">The new [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies provide a significantly more flexible solution to traffic control.</span></span> <span data-ttu-id="73a38-113">Ces nouvelles stratégies vous permettent de définir des expressions pour identifier les clés qui serviront à effectuer le suivi de l'utilisation du trafic.</span><span class="sxs-lookup"><span data-stu-id="73a38-113">These new policies allow you to define expressions to identify the keys that will be used to track traffic usage.</span></span> <span data-ttu-id="73a38-114">Il est plus facile d’en comprendre le fonctionnement avec un exemple.</span><span class="sxs-lookup"><span data-stu-id="73a38-114">The way this works is easiest illustrated with an example.</span></span> 

## <a name="ip-address-throttling"></a><span data-ttu-id="73a38-115">Limitation par adresse IP</span><span class="sxs-lookup"><span data-stu-id="73a38-115">IP Address throttling</span></span>
<span data-ttu-id="73a38-116">Les stratégies suivantes limitent l’adresse IP d’un client à 10 appels par minute, avec un total d’un million d’appels et 10 000 Ko de bande passante par mois.</span><span class="sxs-lookup"><span data-stu-id="73a38-116">The following policies restrict a single client IP address to only 10 calls every minute, with a total of 1,000,000 calls and 10,000 kilobytes of bandwidth per month.</span></span> 

```xml
<rate-limit-by-key  calls="10"
          renewal-period="60"
          counter-key="@(context.Request.IpAddress)" />

<quota-by-key calls="1000000"
          bandwidth="10000"
          renewal-period="2629800"
          counter-key="@(context.Request.IpAddress)" />
```

<span data-ttu-id="73a38-117">Si tous les clients sur Internet utilisent une adresse IP unique, cela peut être un moyen efficace de limiter l'utilisation par utilisateur.</span><span class="sxs-lookup"><span data-stu-id="73a38-117">If all clients on the Internet used a unique IP address, this might be an effective way of limiting usage by user.</span></span> <span data-ttu-id="73a38-118">Toutefois, il est probable que plusieurs utilisateurs partagent une même adresse IP publique parce qu’ils accèdent à Internet via un périphérique NAT.</span><span class="sxs-lookup"><span data-stu-id="73a38-118">However, it is quite likely that multiple users will sharing a single public IP address due to them accessing the Internet via a NAT device.</span></span> <span data-ttu-id="73a38-119">En dépit de cela, le `IpAddress` peut être la meilleure option pour les API qui autorisent l’accès non authentifié.</span><span class="sxs-lookup"><span data-stu-id="73a38-119">Despite this, for APIs that allow unauthenticated access the `IpAddress` might be the best option.</span></span>

## <a name="user-identity-throttling"></a><span data-ttu-id="73a38-120">Limitation par identité d'utilisateur</span><span class="sxs-lookup"><span data-stu-id="73a38-120">User identity throttling</span></span>
<span data-ttu-id="73a38-121">Si un utilisateur final est authentifié, une clé de limitation de la clé peut être générée en fonction d’informations qui identifient cet utilisateur de façon unique.</span><span class="sxs-lookup"><span data-stu-id="73a38-121">If an end user is authenticated then a throttling key can be generated based on information that uniquely identifies an that user.</span></span>

```xml
<rate-limit-by-key calls="10"
    renewal-period="60"
    counter-key="@(context.Request.Headers.GetValueOrDefault("Authorization","").AsJwt()?.Subject)" />
```

<span data-ttu-id="73a38-122">Dans cet exemple, nous extrayons l'en-tête d'autorisation, pour la convertir en objet `JWT` et utiliser le sujet du jeton pour identifier l'utilisateur et l'utiliser comme la clé de limitation du débit.</span><span class="sxs-lookup"><span data-stu-id="73a38-122">In this example we extract the Authorization header, convert it to `JWT` object and use the subject of the token to identify the user and use that as the rate limiting key.</span></span> <span data-ttu-id="73a38-123">Si l'identité de l'utilisateur est stockée dans le `JWT` comme une des autres revendications, la valeur peut être utilisée à la place.</span><span class="sxs-lookup"><span data-stu-id="73a38-123">If the user identity is stored in the `JWT` as one of the other claims then that value could be used in its place.</span></span>

## <a name="combined-policies"></a><span data-ttu-id="73a38-124">Stratégies combinées</span><span class="sxs-lookup"><span data-stu-id="73a38-124">Combined policies</span></span>
<span data-ttu-id="73a38-125">Bien que les nouvelles stratégies de limitation offrent davantage de contrôle que les stratégies de limitation existantes, il est toujours utile de combiner les deux fonctions.</span><span class="sxs-lookup"><span data-stu-id="73a38-125">Although the new throttling policies provide more control than the existing throttling policies, there is still value combining both capabilities.</span></span> <span data-ttu-id="73a38-126">La limitation par clé d’abonnement produit ([Limiter la fréquence des appels par abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) et [Définir le quota d’utilisation par abonnement](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) constitue un excellent moyen de permettre la monétisation d’une API en facturant en fonction des niveaux d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="73a38-126">Throttling by product subscription key ([Limit call rate by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRate) and [Set usage quota by subscription](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuota)) is a great way to enable monetizing of an API by charging based on usage levels.</span></span> <span data-ttu-id="73a38-127">Le contrôle plus fin sur la limitation de la bande passante par utilisateur est gratuite et empêche que le comportement de certains utilisateurs dégrade l'expérience des autres.</span><span class="sxs-lookup"><span data-stu-id="73a38-127">The finer grained control of being able to throttle by user is complementary and prevents one user's behavior from degrading the experience of another.</span></span> 

## <a name="client-driven-throttling"></a><span data-ttu-id="73a38-128">Limitation par client</span><span class="sxs-lookup"><span data-stu-id="73a38-128">Client driven throttling</span></span>
<span data-ttu-id="73a38-129">Lorsque la clé de limitation est définie en utilisant une [expression de stratégie](https://msdn.microsoft.com/library/azure/dn910913.aspx), le fournisseur d'API est celui qui choisit comment définir la limitation.</span><span class="sxs-lookup"><span data-stu-id="73a38-129">When the throttling key is defined using a [policy expression](https://msdn.microsoft.com/library/azure/dn910913.aspx), then it is the API provider that is choosing how the throttling is scoped.</span></span> <span data-ttu-id="73a38-130">Toutefois, un développeur peut souhaiter contrôler la limitation de débit de leurs propres clients.</span><span class="sxs-lookup"><span data-stu-id="73a38-130">However, a developer might want to control how they rate limit their own customers.</span></span> <span data-ttu-id="73a38-131">Cela peut être possible si le fournisseur de l'API introduit un en-tête personnalisé afin de permettre à l'application client du développeur de communiquer la clé à l'API.</span><span class="sxs-lookup"><span data-stu-id="73a38-131">This could be enabled by the API provider by introducing a custom header to allow the developer's client application to communicate the key to the API.</span></span>

```xml
<rate-limit-by-key calls="100"
          renewal-period="60"
          counter-key="@(request.Headers.GetValueOrDefault("Rate-Key",""))"/>
```

<span data-ttu-id="73a38-132">Cela permet à l'application client du développeur de laisser le choix de la création de la clé de limitation de la fréquence.</span><span class="sxs-lookup"><span data-stu-id="73a38-132">This enables the developer's client application to choose how they want to create the rate limiting key.</span></span> <span data-ttu-id="73a38-133">Avec un peu d'ingéniosité, un développeur client peut créer ses propres niveaux de fréquence en allouant des jeux de clés aux utilisateurs et grâce à la rotation de l'utilisation de la clé.</span><span class="sxs-lookup"><span data-stu-id="73a38-133">With a little bit of ingenuity a client developer could create their own rate tiers by allocating sets of keys to users and rotating the key usage.</span></span>

## <a name="summary"></a><span data-ttu-id="73a38-134">Résumé</span><span class="sxs-lookup"><span data-stu-id="73a38-134">Summary</span></span>
<span data-ttu-id="73a38-135">Gestion des API Azure permet la limitation du débit et du devis pour à la fois protéger et valoriser votre service API.</span><span class="sxs-lookup"><span data-stu-id="73a38-135">Azure API Management provides rate and quote throttling to both protect and add value to your API service.</span></span> <span data-ttu-id="73a38-136">Les nouvelles stratégies de limitation avec les règles de portée personnalisées vous permettent un contrôle plus fin sur les stratégies afin de permettre à vos clients de créer de meilleures applications.</span><span class="sxs-lookup"><span data-stu-id="73a38-136">The new throttling policies with custom scoping rules allow you finer grained control over those policies to enable your customers to build even better applications.</span></span> <span data-ttu-id="73a38-137">Les exemples de cet article illustrent l'utilisation de ces nouvelles stratégies avec la création de clés de limitation appliquées aux adresses IP clientes, à l’identité de l'utilisateur et les valeurs générées par le client.</span><span class="sxs-lookup"><span data-stu-id="73a38-137">The examples in this article demonstrate the use of these new policies by manufacturing rate limiting keys with client IP addresses, user identity, and client generated values.</span></span> <span data-ttu-id="73a38-138">Toutefois, il existe de nombreuses autres parties du message qui peuvent être utilisées telles que l’agent utilisateur, les fragments de chemin d'URL, ou la taille des messages.</span><span class="sxs-lookup"><span data-stu-id="73a38-138">However, there are many other parts of the message that could be used such as user agent, URL path fragments, message size.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73a38-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="73a38-139">Next steps</span></span>
<span data-ttu-id="73a38-140">Faites-nous part de vos commentaires dans le thread Disqus de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="73a38-140">Please give us your feedback in the Disqus thread for this topic.</span></span> <span data-ttu-id="73a38-141">Il serait intéressant d’en savoir davantage sur les autres valeurs de clé potentielles qui se sont avérées être un choix judicieux dans vos scénarios.</span><span class="sxs-lookup"><span data-stu-id="73a38-141">It would be great to hear about other potential key values that have been a logical choice in your scenarios.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="73a38-142">Regarder une vidéo de présentation de ces stratégies.</span><span class="sxs-lookup"><span data-stu-id="73a38-142">Watch a video overview of these policies</span></span>
<span data-ttu-id="73a38-143">Pour plus d’informations sur les stratégies [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) et [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) abordées dans cet article, regardez la vidéo suivante.</span><span class="sxs-lookup"><span data-stu-id="73a38-143">For more information on the [rate-limit-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) and [quota-by-key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Advanced-Request-Throttling-with-Azure-API-Management/player]
> 
> 

