---
title: aaaUsing CDN Azure avec CORS | Documents Microsoft
description: "Découvrez comment toouse hello toowith de réseau de distribution contenu (CDN) Azure de partage de ressources Cross-Origin (CORS)."
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
ms.openlocfilehash: 6c743b56c32a2d3aacc9a77094cb87d61b95d2f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-cdn-with-cors"></a><span data-ttu-id="a1c31-103">Utilisation d’Azure CDN avec CORS</span><span class="sxs-lookup"><span data-stu-id="a1c31-103">Using Azure CDN with CORS</span></span>
## <a name="what-is-cors"></a><span data-ttu-id="a1c31-104">Présentation de CORS</span><span class="sxs-lookup"><span data-stu-id="a1c31-104">What is CORS?</span></span>
<span data-ttu-id="a1c31-105">CORS (cross-Origin Resource Sharing) est une fonctionnalité HTTP qui permet à une application web en cours d’exécution ressources de tooaccess sous un domaine dans un autre domaine.</span><span class="sxs-lookup"><span data-stu-id="a1c31-105">CORS (Cross Origin Resource Sharing) is an HTTP feature that enables a web application running under one domain tooaccess resources in another domain.</span></span> <span data-ttu-id="a1c31-106">Dans le risque de hello ordre tooreduce d’attaques de script entre sites, tous les navigateurs web modernes implémentent une restriction de sécurité appelée [stratégie de même origine](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span><span class="sxs-lookup"><span data-stu-id="a1c31-106">In order tooreduce hello possibility of cross-site scripting attacks, all modern web browsers implement a security restriction known as [same-origin policy](http://www.w3.org/Security/wiki/Same_Origin_Policy).</span></span>  <span data-ttu-id="a1c31-107">Celle-ci empêche une page web d’appeler des API dans un autre domaine.</span><span class="sxs-lookup"><span data-stu-id="a1c31-107">This prevents a web page from calling APIs in a different domain.</span></span>  <span data-ttu-id="a1c31-108">CORS constitue un toocall de (domaine d’origine hello) une origine de tooallow sûre API dans une autre origine.</span><span class="sxs-lookup"><span data-stu-id="a1c31-108">CORS provides a secure way tooallow one origin (hello origin domain) toocall APIs in another origin.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="a1c31-109">Fonctionnement</span><span class="sxs-lookup"><span data-stu-id="a1c31-109">How it works</span></span>
<span data-ttu-id="a1c31-110">Il existe deux types de demandes CORS : les *demandes simples* et *les demandes complexes*.</span><span class="sxs-lookup"><span data-stu-id="a1c31-110">There are two types of CORS requests, *simple requests* and *complex requests.*</span></span>

### <a name="for-simple-requests"></a><span data-ttu-id="a1c31-111">Pour les demandes simples :</span><span class="sxs-lookup"><span data-stu-id="a1c31-111">For simple requests:</span></span>

1. <span data-ttu-id="a1c31-112">navigateur de Hello envoie hello CORS demande supplémentaire **origine** en-tête de demande HTTP.</span><span class="sxs-lookup"><span data-stu-id="a1c31-112">hello browser sends hello CORS request with an additional **Origin** HTTP request header.</span></span> <span data-ttu-id="a1c31-113">valeur Hello de cet en-tête est origine hello qui a traité la page parente hello, qui est défini en tant que combinaison de hello de *protocole,* *domaine,* et *port.*</span><span class="sxs-lookup"><span data-stu-id="a1c31-113">hello value of this header is hello origin that served hello parent page, which is defined as hello combination of *protocol,* *domain,* and *port.*</span></span>  <span data-ttu-id="a1c31-114">Lorsqu’une page à partir de https://www.contoso.com essaie de données d’un utilisateur à l’origine de fabrikam.com hello tooaccess, hello suivant l’en-tête de la requête sera donc envoyé toofabrikam.com :</span><span class="sxs-lookup"><span data-stu-id="a1c31-114">When a page from https://www.contoso.com attempts tooaccess a user's data in hello fabrikam.com origin, hello following request header would be sent toofabrikam.com:</span></span>

   `Origin: https://www.contoso.com`

2. <span data-ttu-id="a1c31-115">serveur de Hello peut répondre par hello suivants :</span><span class="sxs-lookup"><span data-stu-id="a1c31-115">hello server may respond with any of hello following:</span></span>

   * <span data-ttu-id="a1c31-116">Un en-tête **Access-Control-Allow-Origin** indiquant le site d’origine autorisé.</span><span class="sxs-lookup"><span data-stu-id="a1c31-116">An **Access-Control-Allow-Origin** header in its response indicating which origin site is allowed.</span></span> <span data-ttu-id="a1c31-117">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="a1c31-117">For example:</span></span>

     `Access-Control-Allow-Origin: https://www.contoso.com`

   * <span data-ttu-id="a1c31-118">Une erreur HTTP de code tels que 403 si les serveur hello n’autorise pas de demande de cross-origin hello après avoir vérifié l’en-tête d’origine hello</span><span class="sxs-lookup"><span data-stu-id="a1c31-118">An HTTP error code such as 403 if hello server does not allow hello cross-origin request after checking hello Origin header</span></span>

   * <span data-ttu-id="a1c31-119">Un en-tête **Access-Control-Allow-Origin** avec un caractère générique qui autorise toutes les origines :</span><span class="sxs-lookup"><span data-stu-id="a1c31-119">An **Access-Control-Allow-Origin** header with a wildcard that allows all origins:</span></span>

     `Access-Control-Allow-Origin: *`

### <a name="for-complex-requests"></a><span data-ttu-id="a1c31-120">Pour les demandes complexes :</span><span class="sxs-lookup"><span data-stu-id="a1c31-120">For complex requests:</span></span>

<span data-ttu-id="a1c31-121">Une requête complexe est une demande CORS où le navigateur de hello est requis toosend un *demande préliminaire* (autrement dit, une sonde préliminaire) avant d’envoyer la demande CORS réelle de hello.</span><span class="sxs-lookup"><span data-stu-id="a1c31-121">A complex request is a CORS request where hello browser is required toosend a *preflight request* (i.e. a preliminary probe) before sending hello actual CORS request.</span></span> <span data-ttu-id="a1c31-122">Hello demande préliminaire demande autorisation de serveur hello si demande CORS d’origine de hello peut continuer et est un `OPTIONS` demande toohello même URL.</span><span class="sxs-lookup"><span data-stu-id="a1c31-122">hello preflight request asks hello server permission if hello original CORS request can proceed and is an `OPTIONS` request toohello same URL.</span></span>

> [!TIP]
> <span data-ttu-id="a1c31-123">Pour plus d’informations sur les flux CORS et pièges les plus courants, afficher hello [Guide tooCORS pour l’API REST](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span><span class="sxs-lookup"><span data-stu-id="a1c31-123">For more details on CORS flows and common pitfalls, view hello [Guide tooCORS for REST APIs](https://www.moesif.com/blog/technical/cors/Authoritative-Guide-to-CORS-Cross-Origin-Resource-Sharing-for-REST-APIs/).</span></span>
>
>

## <a name="wildcard-or-single-origin-scenarios"></a><span data-ttu-id="a1c31-124">Scénarios avec caractère générique ou à origine unique</span><span class="sxs-lookup"><span data-stu-id="a1c31-124">Wildcard or single origin scenarios</span></span>
<span data-ttu-id="a1c31-125">CORS sur Azure CDN fonctionnent automatiquement sans aucune configuration supplémentaire lorsque hello **Access-Control-Allow-Origin** en-tête a la valeur toowildcard (*) ou une origine unique.</span><span class="sxs-lookup"><span data-stu-id="a1c31-125">CORS on Azure CDN will work automatically with no additional configuration when hello **Access-Control-Allow-Origin** header is set toowildcard (*) or a single origin.</span></span>  <span data-ttu-id="a1c31-126">Hello CDN mettra en cache les première réponse de hello et les demandes ultérieures utiliseront hello même en-tête.</span><span class="sxs-lookup"><span data-stu-id="a1c31-126">hello CDN will cache hello first response and subsequent requests will use hello same header.</span></span>

<span data-ttu-id="a1c31-127">Si les demandes ont déjà été apportées à tooCORS préalable du CDN toohello qui est définie sur hello votre origine, vous devez toopurge contenu sur votre hello tooreload contenu de point de terminaison avec hello **Access-Control-Allow-Origin** en-tête.</span><span class="sxs-lookup"><span data-stu-id="a1c31-127">If requests have already been made toohello CDN prior tooCORS being set on hello your origin, you will need toopurge content on your endpoint content tooreload hello content with hello **Access-Control-Allow-Origin** header.</span></span>

## <a name="multiple-origin-scenarios"></a><span data-ttu-id="a1c31-128">Scénarios avec plusieurs origines</span><span class="sxs-lookup"><span data-stu-id="a1c31-128">Multiple origin scenarios</span></span>
<span data-ttu-id="a1c31-129">Si vous devez tooallow une liste spécifique de toobe origines autorisée pour le service CORS, les choses deviennent un peu plus compliquées.</span><span class="sxs-lookup"><span data-stu-id="a1c31-129">If you need tooallow a specific list of origins toobe allowed for CORS, things get a little more complicated.</span></span> <span data-ttu-id="a1c31-130">problème de Hello se produit quand hello CDN met en cache hello **Access-Control-Allow-Origin** en-tête d’origine CORS de la première hello.</span><span class="sxs-lookup"><span data-stu-id="a1c31-130">hello problem occurs when hello CDN caches hello **Access-Control-Allow-Origin** header for hello first CORS origin.</span></span>  <span data-ttu-id="a1c31-131">Une origine CORS différente lorsqu’une demande ultérieure, hello CDN servira hello mis en cache **Access-Control-Allow-Origin** en-tête qui ne correspondre pas.</span><span class="sxs-lookup"><span data-stu-id="a1c31-131">When a different CORS origin makes a subsequent request, hello CDN will serve hello cached **Access-Control-Allow-Origin** header, which won't match.</span></span>  <span data-ttu-id="a1c31-132">Il existe plusieurs façons toocorrect cela.</span><span class="sxs-lookup"><span data-stu-id="a1c31-132">There are several ways toocorrect this.</span></span>

### <a name="azure-cdn-premium-from-verizon"></a><span data-ttu-id="a1c31-133">CDN Azure Premium fourni par Verizon</span><span class="sxs-lookup"><span data-stu-id="a1c31-133">Azure CDN Premium from Verizon</span></span>
<span data-ttu-id="a1c31-134">Hello la meilleure façon tooenable il s’agit de toouse **Azure CDN Premium de Verizon**, qui expose certaines fonctionnalités avancées.</span><span class="sxs-lookup"><span data-stu-id="a1c31-134">hello best way tooenable this is toouse **Azure CDN Premium from Verizon**, which exposes some advanced functionality.</span></span> 

<span data-ttu-id="a1c31-135">Vous devez trop[créer une règle](cdn-rules-engine.md) toocheck hello **origine** en-tête de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="a1c31-135">You'll need too[create a rule](cdn-rules-engine.md) toocheck hello **Origin** header on hello request.</span></span>  <span data-ttu-id="a1c31-136">S’il s’agit d’une origine valide, votre règle définit hello **Access-Control-Allow-Origin** en-tête avec origine hello fournie dans la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="a1c31-136">If it's a valid origin, your rule will set hello **Access-Control-Allow-Origin** header with hello origin provided in hello request.</span></span>  <span data-ttu-id="a1c31-137">Si les origine hello spécifié dans hello **origine** en-tête n’est pas autorisé, votre règle doit omettre hello **Access-Control-Allow-Origin** en-tête, ce qui entraîne la demande de hello navigateur tooreject hello.</span><span class="sxs-lookup"><span data-stu-id="a1c31-137">If hello origin specified in hello **Origin** header is not allowed, your rule should omit hello **Access-Control-Allow-Origin** header which will cause hello browser tooreject hello request.</span></span> 

<span data-ttu-id="a1c31-138">Il existe deux façons toodo cela avec le moteur de règles hello.</span><span class="sxs-lookup"><span data-stu-id="a1c31-138">There are two ways toodo this with hello rules engine.</span></span>  <span data-ttu-id="a1c31-139">Dans les deux cas, hello **Access-Control-Allow-Origin** en-tête à partir du serveur d’origine du fichier hello est complètement ignoré, moteur de règles du CDN hello gère hello autorisé origines CORS.</span><span class="sxs-lookup"><span data-stu-id="a1c31-139">In both cases, hello **Access-Control-Allow-Origin** header from hello file's origin server is completely ignored, hello CDN's rules engine completely manages hello allowed CORS origins.</span></span>

#### <a name="one-regular-expression-with-all-valid-origins"></a><span data-ttu-id="a1c31-140">Une expression régulière avec toutes les origines valides</span><span class="sxs-lookup"><span data-stu-id="a1c31-140">One regular expression with all valid origins</span></span>
<span data-ttu-id="a1c31-141">Dans ce cas, vous allez créer une expression régulière qui inclut toutes les origines de hello souhaité tooallow :</span><span class="sxs-lookup"><span data-stu-id="a1c31-141">In this case, you'll create a regular expression that includes all of hello origins you want tooallow:</span></span> 

    https?:\/\/(www\.contoso\.com|contoso\.com|www\.microsoft\.com|microsoft.com\.com)$

> [!TIP]
> <span data-ttu-id="a1c31-142">**CDN Azure fourni par Verizon** utilise [PCRE (Perl Compatible Regular Expressions)](http://pcre.org/) comme moteur pour les expressions régulières.</span><span class="sxs-lookup"><span data-stu-id="a1c31-142">**Azure CDN from Verizon** uses [Perl Compatible Regular Expressions](http://pcre.org/) as its engine for regular expressions.</span></span>  <span data-ttu-id="a1c31-143">Vous pouvez utiliser un outil tel que [101 d’Expressions régulières](https://regex101.com/) toovalidate votre expression régulière.</span><span class="sxs-lookup"><span data-stu-id="a1c31-143">You can use a tool like [Regular Expressions 101](https://regex101.com/) toovalidate your regular expression.</span></span>  <span data-ttu-id="a1c31-144">Notez que hello « / » de caractères est valide dans les expressions régulières et n’a pas besoin de toobe d’échappement, toutefois, ce caractère d’échappement est considérée comme une meilleure pratique et n’est attendue par certains programmes de validation d’expression régulière.</span><span class="sxs-lookup"><span data-stu-id="a1c31-144">Note that hello "/" character is valid in regular expressions and doesn't need toobe escaped, however, escaping that character is considered a best practice and is expected by some regex validators.</span></span>
> 
> 

<span data-ttu-id="a1c31-145">Si l’expression régulière de hello correspond à, votre règle remplacera hello **Access-Control-Allow-Origin** en-tête (le cas échéant) à partir de l’origine hello avec origine hello qui a envoyé la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="a1c31-145">If hello regular expression matches, your rule will replace hello **Access-Control-Allow-Origin** header (if any) from hello origin with hello origin that sent hello request.</span></span>  <span data-ttu-id="a1c31-146">Vous pouvez également ajouter des en-têtes CORS, comme **Access-Control-Allow-Methods**.</span><span class="sxs-lookup"><span data-stu-id="a1c31-146">You can also add additional CORS headers, such as **Access-Control-Allow-Methods**.</span></span>

![Exemple de règles avec expression régulière](./media/cdn-cors/cdn-cors-regex.png)

#### <a name="request-header-rule-for-each-origin"></a><span data-ttu-id="a1c31-148">Règle d’en-tête de demande pour chaque origine</span><span class="sxs-lookup"><span data-stu-id="a1c31-148">Request header rule for each origin.</span></span>
<span data-ttu-id="a1c31-149">Au lieu d’expressions régulières, vous pouvez créer un distinct pour chaque origine de la règle vous souhaitez tooallow à l’aide de hello **génériques d’en-tête de demande** [correspondent à condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span><span class="sxs-lookup"><span data-stu-id="a1c31-149">Rather than regular expressions, you can instead create a separate rule for each origin you wish tooallow using hello **Request Header Wildcard** [match condition](https://msdn.microsoft.com/library/mt757336.aspx#Anchor_1).</span></span> <span data-ttu-id="a1c31-150">Comme avec la méthode d’expression régulière hello, hello moteur de règles définit uniquement les en-têtes CORS hello.</span><span class="sxs-lookup"><span data-stu-id="a1c31-150">As with hello regular expression method, hello rules engine alone sets hello CORS headers.</span></span> 

![Exemple de règles sans expression régulière](./media/cdn-cors/cdn-cors-no-regex.png)

> [!TIP]
> <span data-ttu-id="a1c31-152">Dans l’exemple hello ci-dessus, hello utilisation du caractère générique de hello * indique au moteur de règles de hello toomatch HTTP et HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a1c31-152">In hello example above, hello use of hello wildcard character * tells hello rules engine toomatch both HTTP and HTTPS.</span></span>
> 
> 

### <a name="azure-cdn-standard"></a><span data-ttu-id="a1c31-153">Azure CDN Standard</span><span class="sxs-lookup"><span data-stu-id="a1c31-153">Azure CDN Standard</span></span>
<span data-ttu-id="a1c31-154">Sur les profils d’Azure CDN Standard, hello tooallow mécanisme pour plusieurs origines sans utiliser de hello d’origine des caractères génériques hello est toouse [mise en cache de la chaîne de requête](cdn-query-string.md).</span><span class="sxs-lookup"><span data-stu-id="a1c31-154">On Azure CDN Standard profiles, hello only mechanism tooallow for multiple origins without hello use of hello wildcard origin is toouse [query string caching](cdn-query-string.md).</span></span>  <span data-ttu-id="a1c31-155">Vous devez tooenable paramètre de chaîne de requête pour le point de terminaison CDN hello et puis utilisez une chaîne de requête unique pour les demandes à partir de chaque domaine autorisé.</span><span class="sxs-lookup"><span data-stu-id="a1c31-155">You need tooenable query string setting for hello CDN endpoint and then use a unique query string for requests from each allowed domain.</span></span> <span data-ttu-id="a1c31-156">Cette opération entraîne hello CDN mise en cache d’un objet distinct pour chaque chaîne de requête unique.</span><span class="sxs-lookup"><span data-stu-id="a1c31-156">Doing this will result in hello CDN caching a separate object for each unique query string.</span></span> <span data-ttu-id="a1c31-157">Cette approche n’est pas idéale, toutefois, il entraînera des copies de hello même fichier mis en cache sur hello CDN.</span><span class="sxs-lookup"><span data-stu-id="a1c31-157">This approach is not ideal, however, as it will result in multiple copies of hello same file cached on hello CDN.</span></span>  

