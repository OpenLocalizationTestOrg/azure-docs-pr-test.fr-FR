---
title: "Mise en cache personnalisée dans Azure API Management"
description: "Découvrez comment mettre en cache des éléments par clé dans le service Azure API Management"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 772bc8dd-5cda-41c4-95bf-b9f6f052bc85
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f5d5f44e34fbcd122a10be0ca5b3001760c4c64d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="d763b-103">Mise en cache personnalisée dans Azure API Management</span><span class="sxs-lookup"><span data-stu-id="d763b-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="d763b-104">Le service Azure API Management prend en charge la [mise en cache de réponses HTTP](api-management-howto-cache.md) en utilisant l’URL de la ressource comme clé.</span><span class="sxs-lookup"><span data-stu-id="d763b-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using the resource URL as the key.</span></span> <span data-ttu-id="d763b-105">La clé peut être modifiée par les en-têtes de requête à l’aide des propriétés `vary-by` .</span><span class="sxs-lookup"><span data-stu-id="d763b-105">The key can be modified by request headers using the `vary-by` properties.</span></span> <span data-ttu-id="d763b-106">Si cette approche permet de mettre en cache l’ensemble des réponses HTTP (également appelées représentations), elle peut être aussi parfois utile pour la mise en cache d’une simple partie d’une représentation.</span><span class="sxs-lookup"><span data-stu-id="d763b-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful to just cache a portion of a representation.</span></span> <span data-ttu-id="d763b-107">Les nouvelles stratégies [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) et [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) permettent de stocker et de récupérer des éléments de données arbitraires à partir des définitions de stratégie.</span><span class="sxs-lookup"><span data-stu-id="d763b-107">The new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide the ability to store and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="d763b-108">Cette fonctionnalité apporte une valeur supplémentaire à la stratégie [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) présentée précédemment, puisqu’elle vous permet de mettre en cache les réponses à partir de services externes.</span><span class="sxs-lookup"><span data-stu-id="d763b-108">This ability also adds value to the previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="d763b-109">Architecture</span><span class="sxs-lookup"><span data-stu-id="d763b-109">Architecture</span></span>
<span data-ttu-id="d763b-110">Le service API Management utilise un cache de données partagé par client, afin que vous puissiez continuer à accéder aux mêmes données mises en cache lorsque vous déployez plusieurs unités.</span><span class="sxs-lookup"><span data-stu-id="d763b-110">API Management service uses a shared per-tenant data cache so that, as you scale up to multiple units you will still get access to the same cached data.</span></span> <span data-ttu-id="d763b-111">Lorsque vous gérez un déploiement dans plusieurs régions, chacune des régions comporte cependant des caches indépendants.</span><span class="sxs-lookup"><span data-stu-id="d763b-111">However, when working with a multi-region deployment there are independent caches within each of the regions.</span></span> <span data-ttu-id="d763b-112">C’est pourquoi il est important de ne pas traiter le cache sous la forme d’un magasin de données où il représente la seule source de certains éléments d’informations.</span><span class="sxs-lookup"><span data-stu-id="d763b-112">Due to this, it is important to not treat the cache as a data store, where it is the only source of some piece of information.</span></span> <span data-ttu-id="d763b-113">Si vous procédez ainsi, et que vous décidez ensuite de tirer parti du déploiement dans plusieurs régions, les clients ayant des utilisateurs nomades risquent de perdre l’accès à ces données mises en cache.</span><span class="sxs-lookup"><span data-stu-id="d763b-113">If you did, and later decided to take advantage of the multi-region deployment, then customers with users that travel may lose access to that cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="d763b-114">Mise en cache de fragments</span><span class="sxs-lookup"><span data-stu-id="d763b-114">Fragment caching</span></span>
<span data-ttu-id="d763b-115">Il peut arriver que, dans les réponses renvoyées, une partie des données soit difficile à déterminer bien qu’elles restent à jour pendant un laps de temps raisonnable.</span><span class="sxs-lookup"><span data-stu-id="d763b-115">There are certain cases where responses being returned contain some portion of data that is expensive to determine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="d763b-116">Pensez, par exemple, à un service généré par une compagnie aérienne qui fournit des informations concernant les réservations de vol, l’état du vol, etc. Si l’utilisateur est membre du programme de points de fidélité de la compagnie aérienne, il obtiendrait également des informations relatives à l’état actuel de son adhésion et au nombre de miles cumulé.</span><span class="sxs-lookup"><span data-stu-id="d763b-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If the user is a member of the airlines points program, they would also have information relating to their current status and mileage accumulated.</span></span> <span data-ttu-id="d763b-117">Ces informations relatives à l’utilisateur peuvent être stockées dans un autre système, mais il peut être souhaitable de les inclure dans les réponses renvoyées concernant les réservations et l’état du vol.</span><span class="sxs-lookup"><span data-stu-id="d763b-117">This user-related information might be stored in a different system, but it may be desirable to include it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="d763b-118">Cette opération peut être effectuée à l’aide d’un processus appelé « mise en cache de fragments ».</span><span class="sxs-lookup"><span data-stu-id="d763b-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="d763b-119">La représentation primaire peut être renvoyée par le serveur d’origine à l’aide d’un type de jeton pour indiquer l’emplacement où les informations relatives à l’utilisateur doivent être insérées.</span><span class="sxs-lookup"><span data-stu-id="d763b-119">The primary representation can be returned from the origin server using some kind of token to indicate where the user-related information is to be inserted.</span></span> 

<span data-ttu-id="d763b-120">Observez la réponse JSON suivante renvoyée par une API du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="d763b-120">Consider the following JSON response from a backend API.</span></span>

```json
{
  "airline" : "Air Canada",
  "flightno" : "871",
  "status" : "ontime",
  "gate" : "B40",
  "terminal" : "2A",
  "userprofile" : "$userprofile$"
}  
```

<span data-ttu-id="d763b-121">Voici la ressource secondaire disponible à l’emplacement `/userprofile/{userid}` :</span><span class="sxs-lookup"><span data-stu-id="d763b-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="d763b-122">Afin de déterminer les informations utilisateur qu’il convient d’inclure, nous devons identifier l’utilisateur final.</span><span class="sxs-lookup"><span data-stu-id="d763b-122">In order to determine the appropriate user information to include, we need to identify who the end user is.</span></span> <span data-ttu-id="d763b-123">Ce mécanisme dépend de l’implémentation.</span><span class="sxs-lookup"><span data-stu-id="d763b-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="d763b-124">Par exemple, j’utilise la revendication `Subject` d’un jeton `JWT`.</span><span class="sxs-lookup"><span data-stu-id="d763b-124">As an example, I am using the `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="d763b-125">Nous stockons cette valeur `enduserid` dans une variable de contexte en vue d’une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d763b-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="d763b-126">L’étape suivante consiste à déterminer si une demande précédente a déjà permis d’extraire les informations de l’utilisateur et de les stocker dans le cache.</span><span class="sxs-lookup"><span data-stu-id="d763b-126">The next step is to determine if a previous request has already retrieved the user information and stored it in the cache.</span></span> <span data-ttu-id="d763b-127">Pour cela, nous utilisons la stratégie `cache-lookup-value` .</span><span class="sxs-lookup"><span data-stu-id="d763b-127">For this we use the `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="d763b-128">Si aucune entrée du cache ne correspond à la valeur de clé, aucune variable de contexte `userprofile` ne sera créée.</span><span class="sxs-lookup"><span data-stu-id="d763b-128">If there is no entry in the cache that corresponds to the key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="d763b-129">Pour vérifier si la recherche a abouti, nous utilisons la stratégie de flux de contrôle `choose` .</span><span class="sxs-lookup"><span data-stu-id="d763b-129">We check the success of the lookup using the `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If the userprofile context variable doesn’t exist, make an HTTP request to retrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="d763b-130">Si la variable de contexte `userprofile` n’existe pas, nous allons devoir exécuter une requête HTTP pour la récupérer.</span><span class="sxs-lookup"><span data-stu-id="d763b-130">If the `userprofile` context variable doesn’t exist, then we are going to have to make an HTTP request to retrieve it.</span></span>

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points to the profile for the current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="d763b-131">Nous utilisons le paramètre `enduserid` pour construire l’URL sur la ressource de profil utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d763b-131">We use the `enduserid` to construct the URL to the user profile resource.</span></span> <span data-ttu-id="d763b-132">Une fois la réponse obtenue, nous pouvons extraire le texte du corps de la réponse et le stocker dans une variable de contexte.</span><span class="sxs-lookup"><span data-stu-id="d763b-132">Once we have the response, we can pull the body text out of the response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="d763b-133">Pour nous éviter d’avoir à réexécuter cette requête HTTP, lorsque l’utilisateur effectue une autre requête, nous pouvons stocker le profil utilisateur dans le cache.</span><span class="sxs-lookup"><span data-stu-id="d763b-133">To avoid us having to make this HTTP request again, when the same user makes another request, we can store the user profile in the cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="d763b-134">Nous stockons la valeur dans le cache en utilisant la même clé que celle que nous avons initialement tenté de récupérer.</span><span class="sxs-lookup"><span data-stu-id="d763b-134">We store the value in the cache using the exact same key that we originally attempted to retrieve it with.</span></span> <span data-ttu-id="d763b-135">La durée du stockage de la valeur doit dépendre de la fréquence à laquelle les informations sont modifiées et du degré de tolérance des utilisateurs face à des informations obsolètes.</span><span class="sxs-lookup"><span data-stu-id="d763b-135">The duration that we choose to store the value should be based on how often the information changes and how tolerant users are to out of date information.</span></span> 

<span data-ttu-id="d763b-136">Il est important de comprendre que la récupération de données du cache est une requête réseau hors processus et qu’elle peut potentiellement ajouter des dizaines de millisecondes à la requête.</span><span class="sxs-lookup"><span data-stu-id="d763b-136">It is important to realize that retrieving from the cache is still an out-of-process, network request and potentially can still add tens of milliseconds to the request.</span></span> <span data-ttu-id="d763b-137">On peut y voir des avantages lorsqu’il faut plus de temps que prévu pour déterminer les informations de profil utilisateur si l’on doit exécuter des requêtes de base de données ou agréger des informations à partir de plusieurs serveurs principaux.</span><span class="sxs-lookup"><span data-stu-id="d763b-137">The benefits come when determining the user profile information takes significantly longer than that due to needing to do database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="d763b-138">La dernière étape du processus consiste à mettre à jour la réponse renvoyée avec nos informations de profil utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d763b-138">The final step in the process is to update the returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="d763b-139">J’ai choisi d’inclure les guillemets dans le jeton de sorte que même si l’opération de remplacement ne se produit pas, la réponse renvoyée prenne toujours la forme d’un script JSON valide.</span><span class="sxs-lookup"><span data-stu-id="d763b-139">I chose to include the quotation marks as part of the token so that even when the replace doesn’t occur, the response was still valid JSON.</span></span> <span data-ttu-id="d763b-140">L’idée était ici principalement de faciliter le débogage.</span><span class="sxs-lookup"><span data-stu-id="d763b-140">This was primarily to make debugging easier.</span></span>

<span data-ttu-id="d763b-141">Une fois que l’on combine toutes ces étapes, on obtient une stratégie semblable à ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="d763b-141">Once you combine all these steps together, the end result is a policy that looks like the following one.</span></span>

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in the cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in the cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request to get user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points to the profile for the current end-user -->
                    <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),(string)context.Variables["enduserid"]).AbsoluteUri)</set-url>
                    <set-method>GET</set-method>
                </send-request>

                <!-- Store response body in context variable -->
                <set-variable
                  name="userprofile"
                  value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />

                <!-- Store result in cache -->
                <cache-store-value
                  key="@("userprofile-" + context.Variables["enduserid"])"
                  value="@((string)context.Variables["userprofile"])"
                  duration="100000" />
            </when>
        </choose>
        <base />
    </inbound>
    <outbound>
        <!-- Update response body with user profile-->
        <find-and-replace
              from='"$userprofile$"'
              to="@((string)context.Variables["userprofile"])" />
        <base />
    </outbound>
</policies>
```

<span data-ttu-id="d763b-142">Cette approche de mise en cache est principalement utilisée dans les sites web où le script HTML est composé côté serveur afin de pouvoir être restitué sur une seule page.</span><span class="sxs-lookup"><span data-stu-id="d763b-142">This caching approach is primarily used in web sites where HTML is composed on the server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="d763b-143">Elle peut toutefois être également utile dans les API où les clients ne peuvent pas effectuer de mise en cache HTTP côté client, ou lorsqu’il est préférable de ne pas confier cette responsabilité au client.</span><span class="sxs-lookup"><span data-stu-id="d763b-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not to put that responsibility on the client.</span></span>

<span data-ttu-id="d763b-144">Ce même type de mise en cache de fragments peut également être effectué sur les serveurs web principaux qui utilisent un serveur de mise en cache Redis ; il est cependant utile de s’appuyer sur le service API Management pour exécuter cette opération lorsque les fragments mis en cache proviennent de serveurs principaux différents de ceux des réponses principales.</span><span class="sxs-lookup"><span data-stu-id="d763b-144">This same kind of fragment caching can also be done on the backend web servers using a Redis caching server, however, using the API Management service to perform this work is useful when the cached fragments are coming from different back-ends than the primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="d763b-145">Contrôle de version transparent</span><span class="sxs-lookup"><span data-stu-id="d763b-145">Transparent versioning</span></span>
<span data-ttu-id="d763b-146">Il n’est pas rare que plusieurs versions différentes d’une implémentation d’une API soient prises en charge simultanément.</span><span class="sxs-lookup"><span data-stu-id="d763b-146">It is common practice for multiple different implementation versions of an API to be supported at any one time.</span></span> <span data-ttu-id="d763b-147">Cette prise en charge simultanée permet, par exemple, de supporter des environnements différents (environnements de développement, de test, de production, etc.) ou bien de prendre en charge les versions antérieures de l’API pour laisser aux consommateurs de l’API le temps de migrer vers des versions plus récentes.</span><span class="sxs-lookup"><span data-stu-id="d763b-147">This is perhaps to support different environments, like dev, test, production, etc, or it may be to support older versions of the API to give time for API consumers to migrate to newer versions.</span></span> 

<span data-ttu-id="d763b-148">Au lieu de demander aux développeurs client de modifier les URL de `/v1/customers` à `/v2/customers`, il est envisageable de stocker dans les données de profil du consommateur la version de l’API qu’il souhaite actuellement utiliser et d’appeler l’URL du serveur principal concerné.</span><span class="sxs-lookup"><span data-stu-id="d763b-148">One approach to handling this instead of requiring client developers to change the URLs from `/v1/customers` to `/v2/customers` is to store in the consumer’s profile data which version of the API they currently wish to use and call the appropriate backend URL.</span></span> <span data-ttu-id="d763b-149">Afin de déterminer l’URL de serveur principal qu’il convient d’appeler pour un client particulier, il est nécessaire d’interroger des données de configuration.</span><span class="sxs-lookup"><span data-stu-id="d763b-149">In order to determine the correct backend URL to call for a particular client, it is necessary to query some configuration data.</span></span> <span data-ttu-id="d763b-150">En mettant en cache ces données de configuration, nous pouvons limiter la perte de performances associée à ce processus de recherche.</span><span class="sxs-lookup"><span data-stu-id="d763b-150">By caching this configuration data, we can minimize the performance penalty of doing this lookup.</span></span>

<span data-ttu-id="d763b-151">La première étape consiste à déterminer l’identificateur utilisé pour configurer la version souhaitée.</span><span class="sxs-lookup"><span data-stu-id="d763b-151">The first step is to determine the identifier used to configure the desired version.</span></span> <span data-ttu-id="d763b-152">Dans cet exemple, j’ai choisi d’associer la version à la clé d’abonnement du produit.</span><span class="sxs-lookup"><span data-stu-id="d763b-152">In this example, I chose to associate the version to the product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="d763b-153">Nous devons ensuite effectuer une recherche dans le cache pour vérifier si nous avons déjà récupéré la version client appropriée.</span><span class="sxs-lookup"><span data-stu-id="d763b-153">We then do a cache lookup to see if we already have retrieved the desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="d763b-154">Puis nous vérifions si cette version a ou non été trouvée dans le cache.</span><span class="sxs-lookup"><span data-stu-id="d763b-154">Then we check to see if we did not find it in the cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="d763b-155">Dans le cas contraire, il est alors possible de l’extraire.</span><span class="sxs-lookup"><span data-stu-id="d763b-155">If we didn’t then we go and retrieve it.</span></span>

```xml
<send-request
    mode="new"
    response-variable-name="clientconfiguresponse"
    timeout="10"
    ignore-error="true">
            <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
            <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="d763b-156">Extrayez le texte du corps de réponse à partir de la réponse.</span><span class="sxs-lookup"><span data-stu-id="d763b-156">Extract the response body text from the response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="d763b-157">Stockez-le de nouveau dans le cache pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d763b-157">Store it back in the cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="d763b-158">Pour finir, mettez à jour l’URL du serveur principal pour sélectionner la version du service souhaitée par le client.</span><span class="sxs-lookup"><span data-stu-id="d763b-158">And finally update the back-end URL to select the version of the service desired by the client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="d763b-159">La stratégie complète se présente comme suit.</span><span class="sxs-lookup"><span data-stu-id="d763b-159">The completely policy is as follows.</span></span>

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in the cache, make a request for it and store it -->
    <choose>
        <when condition="@(!context.Variables.ContainsKey("clientversion"))">
            <send-request mode="new" response-variable-name="clientconfiguresponse" timeout="10" ignore-error="true">
                <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
                <set-method>GET</set-method>
            </send-request>
            <!-- Store response body in context variable -->
            <set-variable name="clientversion" value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
            <!-- Store result in cache -->
            <cache-store-value key="@("clientversion-" + context.Variables["clientid"])" value="@((string)context.Variables["clientversion"])" duration="100000" />
        </when>
    </choose>
    <set-backend-service base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
</inbound>
```

<span data-ttu-id="d763b-160">En permettant aux consommateurs d’API de contrôler en toute transparence la version du serveur principal utilisée par les clients sans avoir à mettre à jour et redéployer les clients, nous proposons une solution pratique qui résout de nombreux problèmes liés au contrôle de version des API.</span><span class="sxs-lookup"><span data-stu-id="d763b-160">Enabling API consumers to transparently control which backend version is being accessed by clients without having to update and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="d763b-161">Isolation des locataires</span><span class="sxs-lookup"><span data-stu-id="d763b-161">Tenant Isolation</span></span>
<span data-ttu-id="d763b-162">Dans les déploiements mutualisés plus volumineux, certaines entreprises créent des groupes de locataires spécifiques sur des déploiements distincts de matériel du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="d763b-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="d763b-163">Cette approche contribue à réduire au minimum le nombre de clients affectés par un problème matériel sur le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="d763b-163">This minimizes the number of customers who are impacted by a hardware issue on the backend.</span></span> <span data-ttu-id="d763b-164">Elle permet également de déployer de nouvelles versions de logiciels de manière progressive.</span><span class="sxs-lookup"><span data-stu-id="d763b-164">It also enables new software versions to be rolled out in stages.</span></span> <span data-ttu-id="d763b-165">Dans l’idéal, cette architecture de serveur principal doit être transparente pour les consommateurs d’API.</span><span class="sxs-lookup"><span data-stu-id="d763b-165">Ideally this backend architecture should be transparent to API consumers.</span></span> <span data-ttu-id="d763b-166">Cet objectif est réalisable en adoptant une approche similaire à celle du contrôle de version transparent, puisqu’il repose sur la même technique de manipulation de l’URL du serveur principal qui utilise un état de configuration par clé d’API.</span><span class="sxs-lookup"><span data-stu-id="d763b-166">This can be achieved in a similar way to transparent versioning because it is based on the same technique of manipulating the backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="d763b-167">Au lieu de renvoyer une version par défaut de l’API pour chaque clé d’abonnement, vous devez retourner un identificateur qui associe un locataire au groupe matériel attribué.</span><span class="sxs-lookup"><span data-stu-id="d763b-167">Instead of returning a preferred version of the API for each subscription key, you would return an identifier that relates a tenant to the assigned hardware group.</span></span> <span data-ttu-id="d763b-168">Cet identificateur peut être utilisé pour construire l’URL du serveur principal approprié.</span><span class="sxs-lookup"><span data-stu-id="d763b-168">That identifier can be used to construct the appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="d763b-169">Résumé</span><span class="sxs-lookup"><span data-stu-id="d763b-169">Summary</span></span>
<span data-ttu-id="d763b-170">L’utilisation du cache du service Azure API Management pour le stockage de n’importe quel type de données permet d’accéder efficacement aux données de configuration susceptibles d’affecter le mode de traitement d’une demande entrante.</span><span class="sxs-lookup"><span data-stu-id="d763b-170">The freedom to use the Azure API management cache for storing any kind of data enables efficient access to configuration data that can affect the way an inbound request is processed.</span></span> <span data-ttu-id="d763b-171">Cette mise en cache peut également être utilisée pour stocker des fragments de données pouvant augmenter les réponses retournées à partir d’une API du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="d763b-171">It can also be used to store data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d763b-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d763b-172">Next steps</span></span>
<span data-ttu-id="d763b-173">Faites-nous part de vos commentaires dans le thread Disqus de cette rubrique si l’utilisation des stratégies décrites s’est révélée adaptée à d’autres scénarios, ou s’il existe des scénarios que vous souhaiteriez mettre en œuvre mais qu’il vous semble impossible de déployer actuellement.</span><span class="sxs-lookup"><span data-stu-id="d763b-173">Please give us your feedback in the Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like to achieve but do not feel are currently possible.</span></span>

