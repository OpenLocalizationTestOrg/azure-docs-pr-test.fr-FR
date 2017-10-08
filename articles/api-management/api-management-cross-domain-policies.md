---
title: "Gestion des API d’aaaAzure stratégies inter-domaines | Documents Microsoft"
description: "Découvrez hello stratégies disponibles pour une utilisation dans la gestion des API Azure inter-domaines."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7689d277-8abe-472a-a78c-e6d4bd43455d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: dd5ebfd65b92ebd0c1f589a2bac669a3928d40b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="8736f-103">Gestion des API dans les stratégies de domaine</span><span class="sxs-lookup"><span data-stu-id="8736f-103">API Management cross domain policies</span></span>
<span data-ttu-id="8736f-104">Cette rubrique fournit une référence pour hello suivant des stratégies de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="8736f-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="8736f-105">Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="8736f-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="8736f-106"><a name="CrossDomainPolicies"></a> Stratégies inter-domaines</span><span class="sxs-lookup"><span data-stu-id="8736f-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="8736f-107">[Autoriser les appels inter-domaines](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -rend hello API accessible à partir de clients basés sur navigateur Adobe Flash et Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="8736f-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="8736f-108">[CORS](api-management-cross-domain-policies.md#CORS) -ajoute le partage de ressources cross-origin (CORS) prend en charge les tooan opération ou une API tooallow entre domaines appelle à partir de clients de navigateur.</span><span class="sxs-lookup"><span data-stu-id="8736f-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="8736f-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - ajoute JSON padding (JSONP) de prise en charge tooan opération ou une API tooallow entre domaines appelle à partir de clients basés sur navigateur JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8736f-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="8736f-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span><span class="sxs-lookup"><span data-stu-id="8736f-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="8736f-111">Hello d’utilisation `cross-domain` hello toomake de stratégie API accessible à partir de clients basés sur navigateur Adobe Flash et Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="8736f-111">Use hello `cross-domain` policy toomake hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8736f-112">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="8736f-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="8736f-113">Exemple</span><span class="sxs-lookup"><span data-stu-id="8736f-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="8736f-114">Éléments</span><span class="sxs-lookup"><span data-stu-id="8736f-114">Elements</span></span>  
  
|<span data-ttu-id="8736f-115">Nom</span><span class="sxs-lookup"><span data-stu-id="8736f-115">Name</span></span>|<span data-ttu-id="8736f-116">Description</span><span class="sxs-lookup"><span data-stu-id="8736f-116">Description</span></span>|<span data-ttu-id="8736f-117">Requis</span><span class="sxs-lookup"><span data-stu-id="8736f-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="8736f-118">inter-domaines</span><span class="sxs-lookup"><span data-stu-id="8736f-118">cross-domain</span></span>|<span data-ttu-id="8736f-119">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8736f-119">Root element.</span></span> <span data-ttu-id="8736f-120">Éléments enfants doivent être conformes toohello [spécification de fichier de stratégie inter-domaines Adobe](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span><span class="sxs-lookup"><span data-stu-id="8736f-120">Child elements must conform toohello [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="8736f-121">Oui</span><span class="sxs-lookup"><span data-stu-id="8736f-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8736f-122">Usage</span><span class="sxs-lookup"><span data-stu-id="8736f-122">Usage</span></span>  
 <span data-ttu-id="8736f-123">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="8736f-123">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8736f-124">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="8736f-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="8736f-125">**Étendues de la stratégie :** globale (globale)</span><span class="sxs-lookup"><span data-stu-id="8736f-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="8736f-126"><a name="CORS"></a> CORS</span><span class="sxs-lookup"><span data-stu-id="8736f-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="8736f-127">Hello `cors` stratégie ajoute le partage de ressources cross-origin (CORS) prend en charge les tooan opération ou une API tooallow entre domaines appelle à partir de clients de navigateur.</span><span class="sxs-lookup"><span data-stu-id="8736f-127">hello `cors` policy adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="8736f-128">CORS permet à un navigateur et un serveur toointeract et déterminer ou non de requêtes tooallow spécifique cross-origine (c'est-à-dire des appels xmlhttprequests établis à partir de JavaScript sur une page web des domaines tooother).</span><span class="sxs-lookup"><span data-stu-id="8736f-128">CORS allows a browser and a server toointeract and determine whether or not tooallow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page tooother domains).</span></span> <span data-ttu-id="8736f-129">Cette stratégie offre plus de flexibilité que de simplement autoriser les demandes de même origine, mais elle est plus sûre que d'autoriser toutes les demandes cross-origin.</span><span class="sxs-lookup"><span data-stu-id="8736f-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8736f-130">Déclaration de stratégie</span><span class="sxs-lookup"><span data-stu-id="8736f-130">Policy statement</span></span>  
  
```xml  
<cors allow-credentials="false|true">  
    <allowed-origins>  
        <origin>origin uri</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="number of seconds">  
        <method>http verb</method>  
    </allowed-methods>  
    <allowed-headers>  
        <header>header name</header>  
    </allowed-headers>  
    <expose-headers>  
        <header>header name</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="example"></a><span data-ttu-id="8736f-131">Exemple</span><span class="sxs-lookup"><span data-stu-id="8736f-131">Example</span></span>  
 <span data-ttu-id="8736f-132">Cet exemple montre comment les demandes avant le vol toosupport, telles que celles comportant des en-têtes personnalisés ou de méthodes autres que GET et POST.</span><span class="sxs-lookup"><span data-stu-id="8736f-132">This example demonstrates how toosupport pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="8736f-133">les en-têtes personnalisés toosupport et autres verbes HTTP, utilisez hello `allowed-methods` et `allowed-headers` sections comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="8736f-133">toosupport custom headers and additional HTTP verbs, use hello `allowed-methods` and `allowed-headers` sections as shown in hello following example.</span></span>  
  
```xml  
<cors allow-credentials="true">  
    <allowed-origins>  
        <!-- Localhost useful for development -->  
        <origin>http://localhost:8080/</origin>  
        <origin>http://example.com/</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="300">  
        <method>GET</method>  
        <method>POST</method>  
        <method>PATCH</method>  
        <method>DELETE</method>  
    </allowed-methods>  
    <allowed-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
        <header>x-zumo-version</header>  
        <header>x-zumo-auth</header>  
        <header>content-type</header>  
        <header>accept</header>  
    </allowed-headers>  
    <expose-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="elements"></a><span data-ttu-id="8736f-134">Éléments</span><span class="sxs-lookup"><span data-stu-id="8736f-134">Elements</span></span>  
  
|<span data-ttu-id="8736f-135">Nom</span><span class="sxs-lookup"><span data-stu-id="8736f-135">Name</span></span>|<span data-ttu-id="8736f-136">Description</span><span class="sxs-lookup"><span data-stu-id="8736f-136">Description</span></span>|<span data-ttu-id="8736f-137">Requis</span><span class="sxs-lookup"><span data-stu-id="8736f-137">Required</span></span>|<span data-ttu-id="8736f-138">Default</span><span class="sxs-lookup"><span data-stu-id="8736f-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8736f-139">cors</span><span class="sxs-lookup"><span data-stu-id="8736f-139">cors</span></span>|<span data-ttu-id="8736f-140">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8736f-140">Root element.</span></span>|<span data-ttu-id="8736f-141">Oui</span><span class="sxs-lookup"><span data-stu-id="8736f-141">Yes</span></span>|<span data-ttu-id="8736f-142">N/A</span><span class="sxs-lookup"><span data-stu-id="8736f-142">N/A</span></span>|  
|<span data-ttu-id="8736f-143">allowed-origins</span><span class="sxs-lookup"><span data-stu-id="8736f-143">allowed-origins</span></span>|<span data-ttu-id="8736f-144">Contient `origin` éléments qui décrivent les hello autorisé origines pour les demandes inter-domaines.</span><span class="sxs-lookup"><span data-stu-id="8736f-144">Contains `origin` elements that describe hello allowed origins for cross-domain requests.</span></span> <span data-ttu-id="8736f-145">`allowed-origins`peut contenir un seul `origin` élément spécifie `*` tooallow toute origine, ou une ou plusieurs `origin` éléments contenant un URI.</span><span class="sxs-lookup"><span data-stu-id="8736f-145">`allowed-origins` can contain either a single `origin` element that specifies `*` tooallow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="8736f-146">Oui</span><span class="sxs-lookup"><span data-stu-id="8736f-146">Yes</span></span>|<span data-ttu-id="8736f-147">N/A</span><span class="sxs-lookup"><span data-stu-id="8736f-147">N/A</span></span>|  
|<span data-ttu-id="8736f-148">origin</span><span class="sxs-lookup"><span data-stu-id="8736f-148">origin</span></span>|<span data-ttu-id="8736f-149">Hello valeur peut être `*` tooallow toutes les origines, ou un URI qui spécifie une origine unique.</span><span class="sxs-lookup"><span data-stu-id="8736f-149">hello value can be either `*` tooallow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="8736f-150">Hello URI doit inclure un schéma, hôte et port.</span><span class="sxs-lookup"><span data-stu-id="8736f-150">hello URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="8736f-151">Oui</span><span class="sxs-lookup"><span data-stu-id="8736f-151">Yes</span></span>|<span data-ttu-id="8736f-152">Si le port de hello est omis dans un URI, le port 80 est utilisé pour HTTP et utilise le port 443 pour HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8736f-152">If hello port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="8736f-153">allowed-methods</span><span class="sxs-lookup"><span data-stu-id="8736f-153">allowed-methods</span></span>|<span data-ttu-id="8736f-154">Cet élément est requis si les méthodes autres que GET ou POST sont autorisées.</span><span class="sxs-lookup"><span data-stu-id="8736f-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="8736f-155">Contient des `method` des éléments qui spécifient hello pris en charge les verbes HTTP.</span><span class="sxs-lookup"><span data-stu-id="8736f-155">Contains `method` elements that specify hello supported HTTP verbs.</span></span>|<span data-ttu-id="8736f-156">Non</span><span class="sxs-lookup"><span data-stu-id="8736f-156">No</span></span>|<span data-ttu-id="8736f-157">Si cette section n’est pas présente, les méthodes GET et POST sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="8736f-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="8736f-158">statique</span><span class="sxs-lookup"><span data-stu-id="8736f-158">method</span></span>|<span data-ttu-id="8736f-159">Spécifie un verbe HTTP.</span><span class="sxs-lookup"><span data-stu-id="8736f-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="8736f-160">Au moins un `method` élément est requis si hello `allowed-methods` section est présente.</span><span class="sxs-lookup"><span data-stu-id="8736f-160">At least one `method` element is required if hello `allowed-methods` section is present.</span></span>|<span data-ttu-id="8736f-161">N/A</span><span class="sxs-lookup"><span data-stu-id="8736f-161">N/A</span></span>|  
|<span data-ttu-id="8736f-162">allowed-headers</span><span class="sxs-lookup"><span data-stu-id="8736f-162">allowed-headers</span></span>|<span data-ttu-id="8736f-163">Cet élément contient `header` éléments spécifiant les noms des en-têtes hello qui peuvent être inclus dans la demande hello.</span><span class="sxs-lookup"><span data-stu-id="8736f-163">This element contains `header` elements specifying names of hello headers that can be included in hello request.</span></span>|<span data-ttu-id="8736f-164">Non</span><span class="sxs-lookup"><span data-stu-id="8736f-164">No</span></span>|<span data-ttu-id="8736f-165">N/A</span><span class="sxs-lookup"><span data-stu-id="8736f-165">N/A</span></span>|  
|<span data-ttu-id="8736f-166">expose-headers</span><span class="sxs-lookup"><span data-stu-id="8736f-166">expose-headers</span></span>|<span data-ttu-id="8736f-167">Cet élément contient `header` éléments spécifiant les noms des en-têtes hello qui seront accessibles par le client de hello.</span><span class="sxs-lookup"><span data-stu-id="8736f-167">This element contains `header` elements specifying names of hello headers that will be accessible by hello client.</span></span>|<span data-ttu-id="8736f-168">Non</span><span class="sxs-lookup"><span data-stu-id="8736f-168">No</span></span>|<span data-ttu-id="8736f-169">N/A</span><span class="sxs-lookup"><span data-stu-id="8736f-169">N/A</span></span>|  
|<span data-ttu-id="8736f-170">en-tête</span><span class="sxs-lookup"><span data-stu-id="8736f-170">header</span></span>|<span data-ttu-id="8736f-171">Spécifie un nom d’en-tête.</span><span class="sxs-lookup"><span data-stu-id="8736f-171">Specifies a header name.</span></span>|<span data-ttu-id="8736f-172">Au moins un `header` élément est requis dans `allowed-headers` ou `expose-headers` si hello section est présente.</span><span class="sxs-lookup"><span data-stu-id="8736f-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if hello section is present.</span></span>|<span data-ttu-id="8736f-173">N/A</span><span class="sxs-lookup"><span data-stu-id="8736f-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8736f-174">Attributs</span><span class="sxs-lookup"><span data-stu-id="8736f-174">Attributes</span></span>  
  
|<span data-ttu-id="8736f-175">Nom</span><span class="sxs-lookup"><span data-stu-id="8736f-175">Name</span></span>|<span data-ttu-id="8736f-176">Description</span><span class="sxs-lookup"><span data-stu-id="8736f-176">Description</span></span>|<span data-ttu-id="8736f-177">Requis</span><span class="sxs-lookup"><span data-stu-id="8736f-177">Required</span></span>|<span data-ttu-id="8736f-178">Default</span><span class="sxs-lookup"><span data-stu-id="8736f-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8736f-179">allow-credentials</span><span class="sxs-lookup"><span data-stu-id="8736f-179">allow-credentials</span></span>|<span data-ttu-id="8736f-180">Hello `Access-Control-Allow-Credentials` en-tête dans la réponse préliminaire de hello sera toohello de valeur de cet attribut et affectent les informations d’identification de toosubmit de capacité du client hello dans les demandes inter-domaines.</span><span class="sxs-lookup"><span data-stu-id="8736f-180">hello `Access-Control-Allow-Credentials` header in hello preflight response will be set toohello value of this attribute and affect hello client’s ability toosubmit credentials in cross-domain requests.</span></span>|<span data-ttu-id="8736f-181">Non</span><span class="sxs-lookup"><span data-stu-id="8736f-181">No</span></span>|<span data-ttu-id="8736f-182">false</span><span class="sxs-lookup"><span data-stu-id="8736f-182">false</span></span>|  
|<span data-ttu-id="8736f-183">preflight-result-max-age</span><span class="sxs-lookup"><span data-stu-id="8736f-183">preflight-result-max-age</span></span>|<span data-ttu-id="8736f-184">Hello `Access-Control-Max-Age` en-tête dans la réponse préliminaire de hello sera toohello de valeur de cet attribut et affectent la réponse de l’agent de l’utilisateur hello capacité toocache préliminaire.</span><span class="sxs-lookup"><span data-stu-id="8736f-184">hello `Access-Control-Max-Age` header in hello preflight response will be set toohello value of this attribute and affect hello user agent’s ability toocache pre-flight response.</span></span>|<span data-ttu-id="8736f-185">Non</span><span class="sxs-lookup"><span data-stu-id="8736f-185">No</span></span>|<span data-ttu-id="8736f-186">0</span><span class="sxs-lookup"><span data-stu-id="8736f-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8736f-187">Usage</span><span class="sxs-lookup"><span data-stu-id="8736f-187">Usage</span></span>  
 <span data-ttu-id="8736f-188">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="8736f-188">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8736f-189">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="8736f-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="8736f-190">**Étendues de la stratégie :** API, operation (API, opération)</span><span class="sxs-lookup"><span data-stu-id="8736f-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="8736f-191"><a name="JSONP"></a> JSONP</span><span class="sxs-lookup"><span data-stu-id="8736f-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="8736f-192">Hello `jsonp` ajoute la stratégie avec remplissage opération tooan de support (JSONP) ou une API tooallow les appels interdomaines à partir des clients basés sur navigateur JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8736f-192">hello `jsonp` policy adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="8736f-193">JSONP est une méthode utilisée dans les données de toorequest programmes JavaScript à partir d’un serveur dans un domaine différent.</span><span class="sxs-lookup"><span data-stu-id="8736f-193">JSONP is a method used in JavaScript programs toorequest data from a server in a different domain.</span></span> <span data-ttu-id="8736f-194">JSONP contourne la limitation de hello imposée par la plupart des navigateurs web où les pages d’accès aux tooweb doivent être Bonjour même domaine.</span><span class="sxs-lookup"><span data-stu-id="8736f-194">JSONP bypasses hello limitation enforced by most web browsers where access tooweb pages must be in hello same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8736f-195">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="8736f-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="8736f-196">Exemple</span><span class="sxs-lookup"><span data-stu-id="8736f-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="8736f-197">Si vous appelez la méthode hello sans paramètre de rappel hello ? cb = XXX, elle renvoie un code JSON brut (sans un wrapper d’appel de fonction).</span><span class="sxs-lookup"><span data-stu-id="8736f-197">If you call hello method without hello callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="8736f-198">Si vous ajoutez le paramètre de rappel hello `?cb=XXX` il retournera un résultat JSONP, en encapsulant les résultats JSON d’origine hello autour de fonction de rappel hello comme`XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="8736f-198">If you add hello callback parameter `?cb=XXX` it will return a JSONP result, wrapping hello original JSON results around hello callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="8736f-199">Éléments</span><span class="sxs-lookup"><span data-stu-id="8736f-199">Elements</span></span>  
  
|<span data-ttu-id="8736f-200">Nom</span><span class="sxs-lookup"><span data-stu-id="8736f-200">Name</span></span>|<span data-ttu-id="8736f-201">Description</span><span class="sxs-lookup"><span data-stu-id="8736f-201">Description</span></span>|<span data-ttu-id="8736f-202">Requis</span><span class="sxs-lookup"><span data-stu-id="8736f-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="8736f-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="8736f-203">jsonp</span></span>|<span data-ttu-id="8736f-204">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8736f-204">Root element.</span></span>|<span data-ttu-id="8736f-205">Oui</span><span class="sxs-lookup"><span data-stu-id="8736f-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8736f-206">Attributs</span><span class="sxs-lookup"><span data-stu-id="8736f-206">Attributes</span></span>  
  
|<span data-ttu-id="8736f-207">Nom</span><span class="sxs-lookup"><span data-stu-id="8736f-207">Name</span></span>|<span data-ttu-id="8736f-208">Description</span><span class="sxs-lookup"><span data-stu-id="8736f-208">Description</span></span>|<span data-ttu-id="8736f-209">Requis</span><span class="sxs-lookup"><span data-stu-id="8736f-209">Required</span></span>|<span data-ttu-id="8736f-210">Default</span><span class="sxs-lookup"><span data-stu-id="8736f-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8736f-211">callback-parameter-name</span><span class="sxs-lookup"><span data-stu-id="8736f-211">callback-parameter-name</span></span>|<span data-ttu-id="8736f-212">Hello appel de fonction JavaScript inter-domaines préfixé avec le nom de domaine complet de hello où hello fonction réside.</span><span class="sxs-lookup"><span data-stu-id="8736f-212">hello cross-domain JavaScript function call prefixed with hello fully qualified domain name where hello function resides.</span></span>|<span data-ttu-id="8736f-213">Oui</span><span class="sxs-lookup"><span data-stu-id="8736f-213">Yes</span></span>|<span data-ttu-id="8736f-214">N/A</span><span class="sxs-lookup"><span data-stu-id="8736f-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8736f-215">Usage</span><span class="sxs-lookup"><span data-stu-id="8736f-215">Usage</span></span>  
 <span data-ttu-id="8736f-216">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="8736f-216">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8736f-217">**Sections de la stratégie :** outbound (sortant)</span><span class="sxs-lookup"><span data-stu-id="8736f-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="8736f-218">**Étendues de la stratégie :** global, product, API, operation (global, produit, API, opération)</span><span class="sxs-lookup"><span data-stu-id="8736f-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="8736f-219">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8736f-219">Next steps</span></span>
<span data-ttu-id="8736f-220">Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="8736f-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  