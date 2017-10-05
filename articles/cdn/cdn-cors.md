---
title: "Utilisation d’Azure CDN avec CORS | Microsoft Docs"
description: "Découvrez comment utiliser Azure CDN (Content Delivery Network) avec CORS (Cross-Origin Resource Sharing)."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 86740a96-4269-4060-aba3-a69f00e6f14e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 7070397f6e69b21add75bad8220f0b8ebe36d266
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="48a86-103">Utilisation d’Azure CDN avec CORS</span><span class="sxs-lookup"><span data-stu-id="48a86-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="48a86-104">Présentation de CORS</span><span class="sxs-lookup"><span data-stu-id="48a86-104">What is CORS?</span></span>
<span data-ttu-id="48a86-105">CORS (Cross Origin Resource Sharing) est une fonctionnalité HTTP qui permet à une application web exécutée dans un domaine d’accéder aux ressources d’un autre domaine.</span><span class="sxs-lookup"><span data-stu-id="48a86-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain to access resources in another domain.</span></span> <span data-ttu-id="48a86-106">Pour réduire le risque d’attaques de script entre sites, tous les navigateurs web modernes implémentent une restriction de sécurité appelée [stratégie de même origine](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span><span class="sxs-lookup"><span data-stu-id="48a86-106">In order to reduce the possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="48a86-107">Celle-ci empêche une page web d’appeler des API dans un autre domaine.</span><span class="sxs-lookup"><span data-stu-id="48a86-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="48a86-108">CORS permet à une origine (le domaine d’origine) d’appeler des API dans un autre domaine de façon sécurisée.</span><span class="sxs-lookup"><span data-stu-id="48a86-108">CORS provides a secure way to allow one origin (the origin domain) to call APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="48a86-109">Fonctionnement</span><span class="sxs-lookup"><span data-stu-id="48a86-109">How it works</span></span>
<span data-ttu-id="48a86-110">Il existe deux types de demandes CORS : les *demandes simples* et *les demandes complexes*.</span><span class="sxs-lookup"><span data-stu-id="48a86-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="48a86-111">Pour les demandes simples :</span><span class="sxs-lookup"><span data-stu-id="48a86-111">For simple requests:</span></span>

1. <span data-ttu-id="48a86-112">Le navigateur envoie la demande CORS avec un en-tête de demande HTTP d’**origine** supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="48a86-112">The browser sends the CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="48a86-113">La valeur de cet en-tête est l’origine qui a servi la page mère, définie comme la combinaison du *protocole,* du *domaine* et du *port*.</span><span class="sxs-lookup"><span data-stu-id="48a86-113">The value of this header is the origin that served the parent page, which is defined as the combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="48a86-114">Quand une page de https://www.contoso.com tente d’accéder aux données d’un utilisateur dans l’origine fabrikam.com, l’en-tête de demande suivant est envoyé à fabrikam.com :</span><span class="sxs-lookup"><span data-stu-id="48a86-114">When a page from https://www.contoso.com attempts to access a user's data in the fabrikam.com origin, the following request header would be sent to fabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="48a86-115">Le serveur peut renvoyer les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="48a86-115">The server may respond with any of the following:</span></span>

   * <span data-ttu-id="48a86-116">Un en-tête **Access-Control-Allow-Origin** indiquant le site d’origine autorisé.</span><span class="sxs-lookup"><span data-stu-id="48a86-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="48a86-117">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="48a86-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="48a86-118">Un code d’erreur HTTP comme 403 si le serveur n’autorise pas la demande d’origine croisée après avoir vérifié l’en-tête d’origine.</span><span class="sxs-lookup"><span data-stu-id="48a86-118">An HTTP error code such as 403 if the server does not allow the cross-origin request after checking the Origin header</span></span>

   * <span data-ttu-id="48a86-119">Un en-tête **Access-Control-Allow-Origin** avec un caractère générique qui autorise toutes les origines :</span><span class="sxs-lookup"><span data-stu-id="48a86-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="48a86-120">Pour les demandes complexes :</span><span class="sxs-lookup"><span data-stu-id="48a86-120">For complex requests:</span></span>

<span data-ttu-id="48a86-121">Une demande complexe est une demande CORS où le navigateur est nécessaire pour envoyer une *demande préliminaire* (c’est-à-dire une sonde préliminaire) avant d’envoyer la demande CORS.</span><span class="sxs-lookup"><span data-stu-id="48a86-121">A complex request is a CORS request where the browser is required to send a *preflight request* (i.e. a preliminary probe) before sending the actual CORS request.</span></span> <span data-ttu-id="48a86-122">La demande préliminaire demande l’autorisation au serveur si la demande CORS d’origine peut se poursuivre et est une demande `OPTIONS` transmise à la même URL.</span><span class="sxs-lookup"><span data-stu-id="48a86-122">The preflight request asks the server permission if the original CORS request can proceed and is an `OPTIONS` request to the same URL.</span></span>

> [!TIP]
> <span data-ttu-id="48a86-123">Pour plus d’informations sur les flux CORS et les pièges les plus courants, consultez le [Authoritative guide to CORS (Cross-Origin Resource Sharing) for REST APIs (Guide de référence sur CORS (Cross-Origin Resource Sharing) pour les API REST)](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span><span class="sxs-lookup"><span data-stu-id="48a86-123">For more details on CORS flows and common pitfalls, view the [Guide to CORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="48a86-124">Scénarios avec caractère générique ou à origine unique</span><span class="sxs-lookup"><span data-stu-id="48a86-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="48a86-125">CORS sur Azure CDN fonctionne automatiquement sans aucune configuration supplémentaire quand l’en-tête **Access-Control-Allow-Origin** est défini sur le caractère générique (*) ou une origine unique.</span><span class="sxs-lookup"><span data-stu-id="48a86-125">CORS on Azure CDN will work automatically with no additional configuration when the **Access-Control-Allow-Origin** header is set to wildcard (*) or a single origin.</span></span>  <span data-ttu-id="48a86-126">Le CDN met en cache la première réponse, et les demandes suivantes utilisent le même en-tête.</span><span class="sxs-lookup"><span data-stu-id="48a86-126">The CDN will cache the first response and subsequent requests will use the same header.</span></span>

<span data-ttu-id="48a86-127">Si les demandes sont communiquées au CDN avant que CORS ne soit défini sur l’origine, vous devez vider le contenu de votre point de terminaison pour recharger le contenu avec l’en-tête **Access-Control-Allow-Origin** .</span><span class="sxs-lookup"><span data-stu-id="48a86-127">If requests have already been made to the CDN prior to CORS being set on the your origin, you will need to purge content on your endpoint content to reload the content with the **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="48a86-128">Scénarios avec plusieurs origines</span><span class="sxs-lookup"><span data-stu-id="48a86-128">Multiple origin scenarios</span></span>
<span data-ttu-id="48a86-129">Si une liste d’origines spécifique doit être autorisée pour CORS, les choses se compliquent un peu plus.</span><span class="sxs-lookup"><span data-stu-id="48a86-129">If you need to allow a specific list of origins to be allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="48a86-130">Le problème se produit quand le CDN met en cache l’en-tête **Access-Control-Allow-Origin** pour la première origine CORS.</span><span class="sxs-lookup"><span data-stu-id="48a86-130">The problem occurs when the CDN caches the **Access-Control-Allow-Origin** header for the first CORS origin.</span></span>  <span data-ttu-id="48a86-131">Quand une autre origine CORS envoie une demande ultérieure, le CDN utilise l’en-tête **Access-Control-Allow-Origin** mis en cache, qui ne correspond pas.</span><span class="sxs-lookup"><span data-stu-id="48a86-131">When a different CORS origin makes a subsequent request, the CDN will serve the cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="48a86-132">Il existe plusieurs façons de corriger cette situation.</span><span class="sxs-lookup"><span data-stu-id="48a86-132">There are several ways to correct this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="48a86-133">CDN Azure Premium fourni par Verizon</span><span class="sxs-lookup"><span data-stu-id="48a86-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="48a86-134">La meilleure façon de procéder consiste à utiliser **CDN Azure Premium fourni par Verizon**, qui expose certaines fonctionnalités avancées.</span><span class="sxs-lookup"><span data-stu-id="48a86-134">The best way to enable this is to use **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="48a86-135">Vous devez [créer une règle](cdn-rules-engine.md) pour vérifier l’en-tête **Origin** dans la demande.</span><span class="sxs-lookup"><span data-stu-id="48a86-135">You'll need to [create a rule](cdn-rules-engine.md) to check the **Origin** header on the request.</span></span>  <span data-ttu-id="48a86-136">S’il s’agit d’une origine valide, votre règle définit l’en-tête **Access-Control-Allow-Origin** avec l’origine fournie dans la demande.</span><span class="sxs-lookup"><span data-stu-id="48a86-136">If it's a valid origin, your rule will set the **Access-Control-Allow-Origin** header with the origin provided in the request.</span></span>  <span data-ttu-id="48a86-137">Si l’origine spécifiée dans l’en-tête **Origin** n’est pas autorisée, votre règle doit omettre l’en-tête **Access-Control-Allow-Origin**, ce qui amène le navigateur à rejeter la demande.</span><span class="sxs-lookup"><span data-stu-id="48a86-137">If the origin specified in the **Origin** header is not allowed, your rule should omit the **Access-Control-Allow-Origin** header which will cause the browser to reject the request.</span></span> 

<span data-ttu-id="48a86-138">Vous pouvez mettre en place cette procédure de deux façons avec le moteur de règles.</span><span class="sxs-lookup"><span data-stu-id="48a86-138">There are two ways to do this with the rules engine.</span></span>  <span data-ttu-id="48a86-139">Dans les deux cas, l’en-tête **Access-Control-Allow-Origin** issu du serveur d’origine du fichier est ignoré en totalité, et le moteur de règles du CDN gère complètement les origines CORS autorisées.</span><span class="sxs-lookup"><span data-stu-id="48a86-139">In both cases, the **Access-Control-Allow-Origin** header from the file's origin server is completely ignored, the CDN's rules engine completely manages the allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="48a86-140">Une expression régulière avec toutes les origines valides</span><span class="sxs-lookup"><span data-stu-id="48a86-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="48a86-141">Dans ce cas, vous allez créer une expression régulière qui inclut toutes les origines que vous souhaitez autoriser :</span><span class="sxs-lookup"><span data-stu-id="48a86-141">In this case, you'll create a regular expression that includes all of the origins you want to allow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="48a86-142">**CDN Azure fourni par Verizon** utilise [PCRE (Perl Compatible Regular Expressions)](http://pcre.org/) comme moteur pour les expressions régulières.</span><span class="sxs-lookup"><span data-stu-id="48a86-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="48a86-143">Vous pouvez utiliser un outil tel que [Regular Expressions 101](https://regex101.com/) pour valider votre expression régulière.</span><span class="sxs-lookup"><span data-stu-id="48a86-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) to validate your regular expression.</span></span>  <span data-ttu-id="48a86-144">Notez que le caractère « / » est valide dans les expressions régulières et n’a pas besoin d’être échappé ; toutefois, échapper ce caractère est une pratique recommandée et attendue par certains validateurs d’expression régulière.</span><span class="sxs-lookup"><span data-stu-id="48a86-144">Note that the "/" character is valid in regular expressions and doesn't need to be escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="48a86-145">Si l’expression régulière correspond, votre règle remplace l’en-tête **Access-Control-Allow-Origin** (le cas échéant) de l’origine par l’origine qui a envoyé la demande.</span><span class="sxs-lookup"><span data-stu-id="48a86-145">If the regular expression matches, your rule will replace the **Access-Control-Allow-Origin** header (if any) from the origin with the origin that sent the request.</span></span>  <span data-ttu-id="48a86-146">Vous pouvez également ajouter des en-têtes CORS, comme **Access-Control-Allow-Methods**.</span><span class="sxs-lookup"><span data-stu-id="48a86-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![Exemple de règles avec expression régulière](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="48a86-148">Règle d’en-tête de demande pour chaque origine</span><span class="sxs-lookup"><span data-stu-id="48a86-148">Request header rule for each origin.</span></span>
<span data-ttu-id="48a86-149">Au lieu de recourir à des expressions régulières, vous pouvez créer une règle pour chaque origine à autoriser en utilisant la [condition de correspondance](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1) **Request Header Wildcard** (Caractère générique pour l’en-tête de la demande).</span><span class="sxs-lookup"><span data-stu-id="48a86-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish to allow using the **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="48a86-150">Comme dans le cas de la méthode des expressions régulières, seul le moteur de règles définit les en-têtes CORS.</span><span class="sxs-lookup"><span data-stu-id="48a86-150">As with the regular expression method, the rules engine alone sets the CORS headers.</span></span> 

![Exemple de règles sans expression régulière](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="48a86-152">Dans l’exemple ci-dessus, l’utilisation du caractère générique * indique au moteur de règles que HTTP et HTTPS satisfont tous les deux à la condition.</span><span class="sxs-lookup"><span data-stu-id="48a86-152">In the example above, the use of the wildcard character * tells the rules engine to match both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="48a86-153">Azure CDN Standard</span><span class="sxs-lookup"><span data-stu-id="48a86-153">Azure CDN Standard</span></span>
<span data-ttu-id="48a86-154">Sur les profils Azure CDN Standard, le seul mécanisme autorisant plusieurs origines sans recourir à l’origine avec caractère générique consiste à utiliser la [mise en cache de chaîne de requête](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="48a86-154">On Azure CDN Standard profiles, the only mechanism to allow for multiple origins without the use of the wildcard origin is to use [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="48a86-155">Vous devez activer le paramètre de chaîne de requête pour le point de terminaison CDN, puis utiliser une chaîne de requête unique pour les demandes à partir de chaque domaine autorisé.</span><span class="sxs-lookup"><span data-stu-id="48a86-155">You need to enable query string setting for the CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="48a86-156">Ainsi, le CDN met en cache un objet distinct pour chaque chaîne de requête unique.</span><span class="sxs-lookup"><span data-stu-id="48a86-156">Doing this will result in the CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="48a86-157">Cette approche n’est pas idéale, toutefois, car plusieurs copies du même fichier sont mises en cache sur le CDN.</span><span class="sxs-lookup"><span data-stu-id="48a86-157">This approach is not ideal, however, as it will result in multiple copies of the same file cached on the CDN.</span></span>  

