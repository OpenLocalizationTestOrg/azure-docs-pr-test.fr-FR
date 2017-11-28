---
title: aaaCustom mise en cache dans Gestion des API Azure
description: "Découvrez comment les éléments de toocache par clé de gestion des API Azure"
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
ms.openlocfilehash: 681380743c8c96af5d0a8e25948a8c0663e9fd35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="45d13-103">Mise en cache personnalisée dans Azure API Management</span><span class="sxs-lookup"><span data-stu-id="45d13-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="45d13-104">Service de gestion des API Azure a une prise en charge intégrée pour [mise en cache de réponse HTTP](api-management-howto-cache.md) à l’aide des URL de ressource hello en tant que clé de hello.</span><span class="sxs-lookup"><span data-stu-id="45d13-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using hello resource URL as hello key.</span></span> <span data-ttu-id="45d13-105">Hello clé peut être modifiée par des en-têtes de demande à l’aide de hello `vary-by` propriétés.</span><span class="sxs-lookup"><span data-stu-id="45d13-105">hello key can be modified by request headers using hello `vary-by` properties.</span></span> <span data-ttu-id="45d13-106">Cela est utile pour la mise en cache les réponses HTTP entières (également appelé représentations), mais il est parfois utile toojust cache une partie d’une représentation.</span><span class="sxs-lookup"><span data-stu-id="45d13-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful toojust cache a portion of a representation.</span></span> <span data-ttu-id="45d13-107">Hello nouvelle [valeur de recherche de cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) et [valeur du magasin de cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) stratégies permettent hello toostore et récupérer des éléments arbitraires de données à partir de définitions de stratégie.</span><span class="sxs-lookup"><span data-stu-id="45d13-107">hello new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide hello ability toostore and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="45d13-108">Cette possibilité ajoute également toohello valeur précédemment introduit [demande d’envoi](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) stratégie, car vous pouvez maintenant mettre en cache les réponses à partir des services externes.</span><span class="sxs-lookup"><span data-stu-id="45d13-108">This ability also adds value toohello previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="45d13-109">Architecture</span><span class="sxs-lookup"><span data-stu-id="45d13-109">Architecture</span></span>
<span data-ttu-id="45d13-110">Service de gestion des API utilise un cache de données partagées par client, afin que, lorsque vous faites évoluer les unités toomultiple vous obtiendrez toujours accès toohello même les données mises en cache.</span><span class="sxs-lookup"><span data-stu-id="45d13-110">API Management service uses a shared per-tenant data cache so that, as you scale up toomultiple units you will still get access toohello same cached data.</span></span> <span data-ttu-id="45d13-111">Toutefois, lorsque vous travaillez avec un déploiement de plusieurs régions, il existe des caches indépendantes dans chacune des régions de hello.</span><span class="sxs-lookup"><span data-stu-id="45d13-111">However, when working with a multi-region deployment there are independent caches within each of hello regions.</span></span> <span data-ttu-id="45d13-112">Échéance toothis, il est important de toonot traiter le cache de hello comme magasin de données, où il est la seule source de hello de certains éléments d’informations.</span><span class="sxs-lookup"><span data-stu-id="45d13-112">Due toothis, it is important toonot treat hello cache as a data store, where it is hello only source of some piece of information.</span></span> <span data-ttu-id="45d13-113">Si vous avez et ultérieurement décidé parti tootake de déploiement de plusieurs régions hello, les clients avec des utilisateurs qui se déplacent peuvent perdre accéder à des données toothat mis en cache.</span><span class="sxs-lookup"><span data-stu-id="45d13-113">If you did, and later decided tootake advantage of hello multi-region deployment, then customers with users that travel may lose access toothat cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="45d13-114">Mise en cache de fragments</span><span class="sxs-lookup"><span data-stu-id="45d13-114">Fragment caching</span></span>
<span data-ttu-id="45d13-115">Il existe certains cas où les réponses renvoyées contiennent une partie des données qui sont coûteuse toodetermine encore restent à jour pour un délai raisonnable.</span><span class="sxs-lookup"><span data-stu-id="45d13-115">There are certain cases where responses being returned contain some portion of data that is expensive toodetermine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="45d13-116">Pensez, par exemple, à un service généré par une compagnie aérienne qui fournit des informations concernant les réservations de vol, l’état du vol, etc. Si l’utilisateur de hello est membre du programme de points hello airlines, ils auraient pas également des informations concernant l’état actuel de tootheir et mileage accumulées.</span><span class="sxs-lookup"><span data-stu-id="45d13-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If hello user is a member of hello airlines points program, they would also have information relating tootheir current status and mileage accumulated.</span></span> <span data-ttu-id="45d13-117">Ces informations relatives à l’utilisateur peuvent être stockées dans un autre système, mais il peut être souhaitable tooinclude dans les réponses retournée sur le vol et les réservations.</span><span class="sxs-lookup"><span data-stu-id="45d13-117">This user-related information might be stored in a different system, but it may be desirable tooinclude it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="45d13-118">Cette opération peut être effectuée à l’aide d’un processus appelé « mise en cache de fragments ».</span><span class="sxs-lookup"><span data-stu-id="45d13-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="45d13-119">Hello représentation primaire peut être retournée à partir du serveur d’origine hello à l’aide d’un type de jeton tooindicate où hello des informations utilisateur sont toobe inséré.</span><span class="sxs-lookup"><span data-stu-id="45d13-119">hello primary representation can be returned from hello origin server using some kind of token tooindicate where hello user-related information is toobe inserted.</span></span> 

<span data-ttu-id="45d13-120">Envisagez de hello suivant la réponse JSON à partir d’une API de service principal.</span><span class="sxs-lookup"><span data-stu-id="45d13-120">Consider hello following JSON response from a backend API.</span></span>

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

<span data-ttu-id="45d13-121">Voici la ressource secondaire disponible à l’emplacement `/userprofile/{userid}` :</span><span class="sxs-lookup"><span data-stu-id="45d13-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="45d13-122">Dans l’ordre toodetermine hello utilisateur approprié informations tooinclude, nous devons tooidentify qui est de l’utilisateur final de hello.</span><span class="sxs-lookup"><span data-stu-id="45d13-122">In order toodetermine hello appropriate user information tooinclude, we need tooidentify who hello end user is.</span></span> <span data-ttu-id="45d13-123">Ce mécanisme dépend de l’implémentation.</span><span class="sxs-lookup"><span data-stu-id="45d13-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="45d13-124">Par exemple, j’utilise hello `Subject` revendication d’un `JWT` jeton.</span><span class="sxs-lookup"><span data-stu-id="45d13-124">As an example, I am using hello `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="45d13-125">Nous stockons cette valeur `enduserid` dans une variable de contexte en vue d’une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="45d13-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="45d13-126">étape suivante de Hello est toodetermine si une demande précédente a déjà les informations utilisateur hello récupérées et stocké dans le cache de hello.</span><span class="sxs-lookup"><span data-stu-id="45d13-126">hello next step is toodetermine if a previous request has already retrieved hello user information and stored it in hello cache.</span></span> <span data-ttu-id="45d13-127">Pour cela, nous utilisons hello `cache-lookup-value` stratégie.</span><span class="sxs-lookup"><span data-stu-id="45d13-127">For this we use hello `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="45d13-128">S’il n’existe aucune entrée dans le cache hello qui correspond la valeur de la clé toohello, puis non `userprofile` variable contextuelle sera créé.</span><span class="sxs-lookup"><span data-stu-id="45d13-128">If there is no entry in hello cache that corresponds toohello key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="45d13-129">Nous vérifions réussite hello de recherche de hello à l’aide de hello `choose` stratégie de flux de contrôle.</span><span class="sxs-lookup"><span data-stu-id="45d13-129">We check hello success of hello lookup using hello `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="45d13-130">Si hello `userprofile` variable contextuelle n’existe pas, puis nous sommes continu toohave toomake HTTP demande tooretrieve il.</span><span class="sxs-lookup"><span data-stu-id="45d13-130">If hello `userprofile` context variable doesn’t exist, then we are going toohave toomake an HTTP request tooretrieve it.</span></span>

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points toohello profile for hello current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="45d13-131">Nous utilisons hello `enduserid` ressource de profil utilisateur tooconstruct hello URL toohello.</span><span class="sxs-lookup"><span data-stu-id="45d13-131">We use hello `enduserid` tooconstruct hello URL toohello user profile resource.</span></span> <span data-ttu-id="45d13-132">Une fois que nous avons la réponse de hello, nous pouvons extraire le corps du texte hello en dehors de la réponse de hello et stockez-le dans une variable de contexte.</span><span class="sxs-lookup"><span data-stu-id="45d13-132">Once we have hello response, we can pull hello body text out of hello response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="45d13-133">tooavoid de nous avoir toomake cette requête HTTP, lorsque le même utilisateur hello effectue une autre requête, nous pouvons stocker hello profil dans le cache de hello.</span><span class="sxs-lookup"><span data-stu-id="45d13-133">tooavoid us having toomake this HTTP request again, when hello same user makes another request, we can store hello user profile in hello cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="45d13-134">Nous stockons les valeur hello dans le cache de hello à l’aide de la clé exacte même hello que nous avons tenté initialement tooretrieve avec.</span><span class="sxs-lookup"><span data-stu-id="45d13-134">We store hello value in hello cache using hello exact same key that we originally attempted tooretrieve it with.</span></span> <span data-ttu-id="45d13-135">Hello durée nous choisir la valeur de hello toostore doit être basée sur la fréquence à laquelle hello modification des informations et des utilisateurs à la tolérance de panne sont tooout d’informations de date.</span><span class="sxs-lookup"><span data-stu-id="45d13-135">hello duration that we choose toostore hello value should be based on how often hello information changes and how tolerant users are tooout of date information.</span></span> 

<span data-ttu-id="45d13-136">Il est toorealize important que la récupération à partir du cache de hello est toujours un out-of-process, la demande réseau et potentiellement pouvez toujours ajouter des dizaines de millisecondes toohello demande.</span><span class="sxs-lookup"><span data-stu-id="45d13-136">It is important toorealize that retrieving from hello cache is still an out-of-process, network request and potentially can still add tens of milliseconds toohello request.</span></span> <span data-ttu-id="45d13-137">avantages de Hello sont fournis lorsque les informations de profil utilisateur hello déterminant dure plus longtemps que celle en raison de requêtes de base de données tooneeding toodo ou des informations d’agrégation à partir de plusieurs systèmes principaux.</span><span class="sxs-lookup"><span data-stu-id="45d13-137">hello benefits come when determining hello user profile information takes significantly longer than that due tooneeding toodo database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="45d13-138">Hello dernière étape du processus de hello est hello tooupdate a retourné une réponse avec ses informations de profil utilisateur.</span><span class="sxs-lookup"><span data-stu-id="45d13-138">hello final step in hello process is tooupdate hello returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="45d13-139">J’ai choisi tooinclude hello guillemets dans le cadre du jeton de hello afin que même lorsque hello remplacer ne se produit pas, réponse de hello a été JSON toujours valide.</span><span class="sxs-lookup"><span data-stu-id="45d13-139">I chose tooinclude hello quotation marks as part of hello token so that even when hello replace doesn’t occur, hello response was still valid JSON.</span></span> <span data-ttu-id="45d13-140">Il s’agit principalement les toomake débogage.</span><span class="sxs-lookup"><span data-stu-id="45d13-140">This was primarily toomake debugging easier.</span></span>

<span data-ttu-id="45d13-141">Une fois que vous combinez toutes ces étapes, le résultat final de hello est une stratégie qui ressemble à hello suivant un.</span><span class="sxs-lookup"><span data-stu-id="45d13-141">Once you combine all these steps together, hello end result is a policy that looks like hello following one.</span></span>

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in hello cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in hello cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request tooget user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points toohello profile for hello current end-user -->
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

<span data-ttu-id="45d13-142">Cette approche de mise en cache est principalement utilisée dans les sites web où HTML est composé du côté serveur de hello afin qu’il peut être rendu en tant qu’une seule page.</span><span class="sxs-lookup"><span data-stu-id="45d13-142">This caching approach is primarily used in web sites where HTML is composed on hello server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="45d13-143">Toutefois, il peut également être utile dans les API dans lequel les clients ne peuvent pas faire client côté mise en cache HTTP ou il est préférable de tooput pas cette responsabilité sur le client de hello.</span><span class="sxs-lookup"><span data-stu-id="45d13-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not tooput that responsibility on hello client.</span></span>

<span data-ttu-id="45d13-144">Ce même type de mise en cache de fragment peut également être effectué sur les serveurs web de hello principaux à l’aide d’un serveur de mise en cache de Redis, toutefois, à l’aide de tooperform de service de gestion des API hello ce travail est utile lorsque les fragments hello mises en cache provenant de différents systèmes principaux à hello réponses principales.</span><span class="sxs-lookup"><span data-stu-id="45d13-144">This same kind of fragment caching can also be done on hello backend web servers using a Redis caching server, however, using hello API Management service tooperform this work is useful when hello cached fragments are coming from different back-ends than hello primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="45d13-145">Contrôle de version transparent</span><span class="sxs-lookup"><span data-stu-id="45d13-145">Transparent versioning</span></span>
<span data-ttu-id="45d13-146">Il est pratique courante pour plusieurs versions d’implémentation différente d’une toobe API prises en charge à la fois.</span><span class="sxs-lookup"><span data-stu-id="45d13-146">It is common practice for multiple different implementation versions of an API toobe supported at any one time.</span></span> <span data-ttu-id="45d13-147">Il s’agit peut-être toosupport différents environnements, tels que le développement, test, production, etc., ou il peut être toosupport des versions antérieures de temps de toogive hello API pour les versions d’API consommateurs toomigrate toonewer.</span><span class="sxs-lookup"><span data-stu-id="45d13-147">This is perhaps toosupport different environments, like dev, test, production, etc, or it may be toosupport older versions of hello API toogive time for API consumers toomigrate toonewer versions.</span></span> 

<span data-ttu-id="45d13-148">Toohandling une approche ce à la place de demander aux clients aux développeurs toochange hello URL à partir de `/v1/customers` trop`/v2/customers` est toostore dans les données de profil du consommateur hello quelle version de hello API ils actuellement souhaitent toouse et appellent hello approprié URL du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="45d13-148">One approach toohandling this instead of requiring client developers toochange hello URLs from `/v1/customers` too`/v2/customers` is toostore in hello consumer’s profile data which version of hello API they currently wish toouse and call hello appropriate backend URL.</span></span> <span data-ttu-id="45d13-149">Dans toocall URL ordre toodetermine hello principal correct pour un client particulier, il est nécessaire tooquery certaines données de configuration.</span><span class="sxs-lookup"><span data-stu-id="45d13-149">In order toodetermine hello correct backend URL toocall for a particular client, it is necessary tooquery some configuration data.</span></span> <span data-ttu-id="45d13-150">En mettant en cache les données de cette configuration, nous pouvons réduire baisse des performances de cette recherche hello.</span><span class="sxs-lookup"><span data-stu-id="45d13-150">By caching this configuration data, we can minimize hello performance penalty of doing this lookup.</span></span>

<span data-ttu-id="45d13-151">Hello première étape est l’identificateur de hello toodetermine utilisait la version souhaitée de tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="45d13-151">hello first step is toodetermine hello identifier used tooconfigure hello desired version.</span></span> <span data-ttu-id="45d13-152">Dans cet exemple, j’ai choisi de clé d’abonnement tooassociate hello version toohello produit.</span><span class="sxs-lookup"><span data-stu-id="45d13-152">In this example, I chose tooassociate hello version toohello product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="45d13-153">Nous avons ensuite procéder à une toosee de recherche de cache si nous avons déjà récupéré la version du client souhaité hello.</span><span class="sxs-lookup"><span data-stu-id="45d13-153">We then do a cache lookup toosee if we already have retrieved hello desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="45d13-154">Puis nous vérifions toosee si nous n’a pas le trouvé dans le cache de hello.</span><span class="sxs-lookup"><span data-stu-id="45d13-154">Then we check toosee if we did not find it in hello cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="45d13-155">Dans le cas contraire, il est alors possible de l’extraire.</span><span class="sxs-lookup"><span data-stu-id="45d13-155">If we didn’t then we go and retrieve it.</span></span>

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

<span data-ttu-id="45d13-156">Extrayez le texte du corps de réponse hello de réponse de hello.</span><span class="sxs-lookup"><span data-stu-id="45d13-156">Extract hello response body text from hello response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="45d13-157">Stockez-le dans cache hello pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="45d13-157">Store it back in hello cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="45d13-158">Et enfin à jour hello principal URL tooselect hello version de service hello souhaité par le client de hello.</span><span class="sxs-lookup"><span data-stu-id="45d13-158">And finally update hello back-end URL tooselect hello version of hello service desired by hello client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="45d13-159">Bonjour complètement stratégie est comme suit.</span><span class="sxs-lookup"><span data-stu-id="45d13-159">hello completely policy is as follows.</span></span>

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in hello cache, make a request for it and store it -->
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

<span data-ttu-id="45d13-160">L’activation du contrôle de tootransparently consommateurs API version principale est accessible par les clients sans avoir tooupdate et redéployer les clients est une solution élégante qui traite de nombreux problèmes de contrôle de version d’API.</span><span class="sxs-lookup"><span data-stu-id="45d13-160">Enabling API consumers tootransparently control which backend version is being accessed by clients without having tooupdate and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="45d13-161">Isolation des locataires</span><span class="sxs-lookup"><span data-stu-id="45d13-161">Tenant Isolation</span></span>
<span data-ttu-id="45d13-162">Dans les déploiements mutualisés plus volumineux, certaines entreprises créent des groupes de locataires spécifiques sur des déploiements distincts de matériel du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="45d13-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="45d13-163">Cela réduit le nombre de hello de clients qui sont affectés à un problème matériel sur hello principal.</span><span class="sxs-lookup"><span data-stu-id="45d13-163">This minimizes hello number of customers who are impacted by a hardware issue on hello backend.</span></span> <span data-ttu-id="45d13-164">Il permet également de nouvelles toobe de versions logicielles transférée par étapes.</span><span class="sxs-lookup"><span data-stu-id="45d13-164">It also enables new software versions toobe rolled out in stages.</span></span> <span data-ttu-id="45d13-165">Dans l’idéal, cette architecture de serveur principal doit être transparent tooAPI consommateurs.</span><span class="sxs-lookup"><span data-stu-id="45d13-165">Ideally this backend architecture should be transparent tooAPI consumers.</span></span> <span data-ttu-id="45d13-166">Cela peut être effectuée dans un contrôle de version de tootransparent façon similaire, car il est basé sur hello même technique de manipulation des URL de serveur principal hello en utilisant l’état de configuration par clé d’API.</span><span class="sxs-lookup"><span data-stu-id="45d13-166">This can be achieved in a similar way tootransparent versioning because it is based on hello same technique of manipulating hello backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="45d13-167">Au lieu de retourner une version préférée du hello API pour chaque clé d’abonnement, vous devez retourner un identificateur qui est lié à un groupe de matériel client toohello attribué.</span><span class="sxs-lookup"><span data-stu-id="45d13-167">Instead of returning a preferred version of hello API for each subscription key, you would return an identifier that relates a tenant toohello assigned hardware group.</span></span> <span data-ttu-id="45d13-168">Cet identificateur peut être utilisé tooconstruct hello principaux appropriés URL.</span><span class="sxs-lookup"><span data-stu-id="45d13-168">That identifier can be used tooconstruct hello appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="45d13-169">Résumé</span><span class="sxs-lookup"><span data-stu-id="45d13-169">Summary</span></span>
<span data-ttu-id="45d13-170">hello toouse de liberté Hello du cache de gestion des API Azure pour stocker n’importe quel type de données permet de données tooconfiguration un accès efficace qui peuvent affecter de manière hello qu'une demande entrante est traitée.</span><span class="sxs-lookup"><span data-stu-id="45d13-170">hello freedom toouse hello Azure API management cache for storing any kind of data enables efficient access tooconfiguration data that can affect hello way an inbound request is processed.</span></span> <span data-ttu-id="45d13-171">Il peut également être utilisé toostore les fragments de données qui peuvent augmenter les réponses retournées à partir d’une API de service principal.</span><span class="sxs-lookup"><span data-stu-id="45d13-171">It can also be used toostore data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45d13-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="45d13-172">Next steps</span></span>
<span data-ttu-id="45d13-173">Veuillez envoyez-nous vos commentaires Bonjour Disqus thread de cette rubrique s’il existe d’autres scénarios que ces stratégies ont activé pour vous, ou s’il existe des scénarios vous aimeriez tooachieve mais que vous n’êtes pas sont actuellement possibles.</span><span class="sxs-lookup"><span data-stu-id="45d13-173">Please give us your feedback in hello Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like tooachieve but do not feel are currently possible.</span></span>

