---
title: "Stratégies inter-domaines dans Gestion des API Azure | Microsoft Docs"
description: "Découvrez les stratégies inter-domaines disponibles dans Gestion des API Azure."
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
ms.openlocfilehash: ddca9e35b44a21294abbb5eaa4418bcdb85494cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="8791c-103">Gestion des API dans les stratégies de domaine</span><span class="sxs-lookup"><span data-stu-id="8791c-103">API Management cross domain policies</span></span>
<span data-ttu-id="8791c-104">Cette rubrique est une ressource de référence au sujet des stratégies Gestion des API suivantes.</span><span class="sxs-lookup"><span data-stu-id="8791c-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="8791c-105">Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="8791c-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="8791c-106"><a name="CrossDomainPolicies"></a> Stratégies inter-domaines</span><span class="sxs-lookup"><span data-stu-id="8791c-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="8791c-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) : rend l'API accessible depuis les navigateurs clients utilisant Adobe Flash et Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="8791c-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="8791c-108">[CORS](api-management-cross-domain-policies.md#CORS) : ajoute une prise en charge partage des ressources cross-origin (CORS) à une opération ou une API afin de permettre les appels interdomaines depuis les navigateurs clients.</span><span class="sxs-lookup"><span data-stu-id="8791c-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="8791c-109">[JSONP](api-management-cross-domain-policies.md#JSONP) : ajoute une prise en charge de JSON avec remplissage (JSONP) à une opération ou une API afin de permettre les appels interdomaines depuis les navigateurs clients utilisant JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8791c-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="8791c-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span><span class="sxs-lookup"><span data-stu-id="8791c-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="8791c-111">La stratégie `cross-domain` rend l’API accessible depuis les navigateurs clients utilisant Adobe Flash et Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="8791c-111">Use the `cross-domain` policy to make the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8791c-112">Déclaration de stratégie</span><span class="sxs-lookup"><span data-stu-id="8791c-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in the Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="8791c-113">Exemple</span><span class="sxs-lookup"><span data-stu-id="8791c-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="8791c-114">Éléments</span><span class="sxs-lookup"><span data-stu-id="8791c-114">Elements</span></span>  
  
|<span data-ttu-id="8791c-115">Nom</span><span class="sxs-lookup"><span data-stu-id="8791c-115">Name</span></span>|<span data-ttu-id="8791c-116">Description</span><span class="sxs-lookup"><span data-stu-id="8791c-116">Description</span></span>|<span data-ttu-id="8791c-117">Requis</span><span class="sxs-lookup"><span data-stu-id="8791c-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="8791c-118">inter-domaines</span><span class="sxs-lookup"><span data-stu-id="8791c-118">cross-domain</span></span>|<span data-ttu-id="8791c-119">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8791c-119">Root element.</span></span> <span data-ttu-id="8791c-120">Les éléments enfants doivent être conformes à la [spécification de fichier de stratégie inter-domaines Adobe](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span><span class="sxs-lookup"><span data-stu-id="8791c-120">Child elements must conform to the [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="8791c-121">Oui</span><span class="sxs-lookup"><span data-stu-id="8791c-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8791c-122">Usage</span><span class="sxs-lookup"><span data-stu-id="8791c-122">Usage</span></span>  
 <span data-ttu-id="8791c-123">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="8791c-123">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8791c-124">**Sections de la stratégie :** inbound (entrant)</span><span class="sxs-lookup"><span data-stu-id="8791c-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="8791c-125">**Étendues de la stratégie :** globale (globale)</span><span class="sxs-lookup"><span data-stu-id="8791c-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="8791c-126"><a name="CORS"></a> CORS</span><span class="sxs-lookup"><span data-stu-id="8791c-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="8791c-127">La stratégie `cors` ajoute la prise en charge du partage des ressources cross-origin (CORS) à une opération ou une API afin de permettre les appels inter-domaines à partir des navigateurs clients.</span><span class="sxs-lookup"><span data-stu-id="8791c-127">The `cors` policy adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="8791c-128">CORS permet à un navigateur et à un serveur d'interagir et de déterminer si les demandes cross-origin doivent être autorisées ou non, par exemple dans le cas d'appels XMLHttpRequests passés via JavaScript sur une page web vers d'autres domaines).</span><span class="sxs-lookup"><span data-stu-id="8791c-128">CORS allows a browser and a server to interact and determine whether or not to allow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page to other domains).</span></span> <span data-ttu-id="8791c-129">Cette stratégie offre plus de flexibilité que de simplement autoriser les demandes de même origine, mais elle est plus sûre que d'autoriser toutes les demandes cross-origin.</span><span class="sxs-lookup"><span data-stu-id="8791c-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8791c-130">Déclaration de stratégie</span><span class="sxs-lookup"><span data-stu-id="8791c-130">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="8791c-131">Exemple</span><span class="sxs-lookup"><span data-stu-id="8791c-131">Example</span></span>  
 <span data-ttu-id="8791c-132">Cet exemple montre comment prendre en charge les demandes en amont, telles que celles comportant des en-têtes personnalisés ou des méthodes autres que GET et POST.</span><span class="sxs-lookup"><span data-stu-id="8791c-132">This example demonstrates how to support pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="8791c-133">Pour prendre en charge les en-têtes personnalisés et autres verbes HTTP, utilisez les sections `allowed-methods` et `allowed-headers` comme indiqué dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="8791c-133">To support custom headers and additional HTTP verbs, use the `allowed-methods` and `allowed-headers` sections as shown in the following example.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="8791c-134">Éléments</span><span class="sxs-lookup"><span data-stu-id="8791c-134">Elements</span></span>  
  
|<span data-ttu-id="8791c-135">Nom</span><span class="sxs-lookup"><span data-stu-id="8791c-135">Name</span></span>|<span data-ttu-id="8791c-136">Description</span><span class="sxs-lookup"><span data-stu-id="8791c-136">Description</span></span>|<span data-ttu-id="8791c-137">Requis</span><span class="sxs-lookup"><span data-stu-id="8791c-137">Required</span></span>|<span data-ttu-id="8791c-138">Default</span><span class="sxs-lookup"><span data-stu-id="8791c-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8791c-139">cors</span><span class="sxs-lookup"><span data-stu-id="8791c-139">cors</span></span>|<span data-ttu-id="8791c-140">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8791c-140">Root element.</span></span>|<span data-ttu-id="8791c-141">Oui</span><span class="sxs-lookup"><span data-stu-id="8791c-141">Yes</span></span>|<span data-ttu-id="8791c-142">N/A</span><span class="sxs-lookup"><span data-stu-id="8791c-142">N/A</span></span>|  
|<span data-ttu-id="8791c-143">allowed-origins</span><span class="sxs-lookup"><span data-stu-id="8791c-143">allowed-origins</span></span>|<span data-ttu-id="8791c-144">Contient des éléments `origin` qui décrivent les origines autorisées pour les demandes inter-domaines.</span><span class="sxs-lookup"><span data-stu-id="8791c-144">Contains `origin` elements that describe the allowed origins for cross-domain requests.</span></span> <span data-ttu-id="8791c-145">`allowed-origins` peut contenir un seul élément `origin` qui spécifie `*` pour autoriser toute origine, ou un ou plusieurs éléments `origin` contenant un URI.</span><span class="sxs-lookup"><span data-stu-id="8791c-145">`allowed-origins` can contain either a single `origin` element that specifies `*` to allow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="8791c-146">Oui</span><span class="sxs-lookup"><span data-stu-id="8791c-146">Yes</span></span>|<span data-ttu-id="8791c-147">N/A</span><span class="sxs-lookup"><span data-stu-id="8791c-147">N/A</span></span>|  
|<span data-ttu-id="8791c-148">origin</span><span class="sxs-lookup"><span data-stu-id="8791c-148">origin</span></span>|<span data-ttu-id="8791c-149">La valeur peut être `*` pour autoriser toutes les origines, ou un URI qui spécifie une origine unique.</span><span class="sxs-lookup"><span data-stu-id="8791c-149">The value can be either `*` to allow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="8791c-150">L'URI doit comprendre un modèle, un hôte et un port.</span><span class="sxs-lookup"><span data-stu-id="8791c-150">The URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="8791c-151">Oui</span><span class="sxs-lookup"><span data-stu-id="8791c-151">Yes</span></span>|<span data-ttu-id="8791c-152">Si le port n’est pas spécifié dans l’URI, le port 80 est utilisé pour HTTP et le port 443 pour HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8791c-152">If the port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="8791c-153">allowed-methods</span><span class="sxs-lookup"><span data-stu-id="8791c-153">allowed-methods</span></span>|<span data-ttu-id="8791c-154">Cet élément est requis si les méthodes autres que GET ou POST sont autorisées.</span><span class="sxs-lookup"><span data-stu-id="8791c-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="8791c-155">Contient des éléments `method` qui spécifient les verbes HTTP pris en charge.</span><span class="sxs-lookup"><span data-stu-id="8791c-155">Contains `method` elements that specify the supported HTTP verbs.</span></span>|<span data-ttu-id="8791c-156">Non</span><span class="sxs-lookup"><span data-stu-id="8791c-156">No</span></span>|<span data-ttu-id="8791c-157">Si cette section n’est pas présente, les méthodes GET et POST sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="8791c-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="8791c-158">statique</span><span class="sxs-lookup"><span data-stu-id="8791c-158">method</span></span>|<span data-ttu-id="8791c-159">Spécifie un verbe HTTP.</span><span class="sxs-lookup"><span data-stu-id="8791c-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="8791c-160">Au moins un élément `method` est requis si la section `allowed-methods` est présente.</span><span class="sxs-lookup"><span data-stu-id="8791c-160">At least one `method` element is required if the `allowed-methods` section is present.</span></span>|<span data-ttu-id="8791c-161">N/A</span><span class="sxs-lookup"><span data-stu-id="8791c-161">N/A</span></span>|  
|<span data-ttu-id="8791c-162">allowed-headers</span><span class="sxs-lookup"><span data-stu-id="8791c-162">allowed-headers</span></span>|<span data-ttu-id="8791c-163">Cet élément contient des éléments `header` spécifiant les noms des en-têtes qui peuvent être inclus dans la demande.</span><span class="sxs-lookup"><span data-stu-id="8791c-163">This element contains `header` elements specifying names of the headers that can be included in the request.</span></span>|<span data-ttu-id="8791c-164">Non</span><span class="sxs-lookup"><span data-stu-id="8791c-164">No</span></span>|<span data-ttu-id="8791c-165">N/A</span><span class="sxs-lookup"><span data-stu-id="8791c-165">N/A</span></span>|  
|<span data-ttu-id="8791c-166">expose-headers</span><span class="sxs-lookup"><span data-stu-id="8791c-166">expose-headers</span></span>|<span data-ttu-id="8791c-167">Cet élément contient des éléments `header` spécifiant les noms des en-têtes accessibles par le client.</span><span class="sxs-lookup"><span data-stu-id="8791c-167">This element contains `header` elements specifying names of the headers that will be accessible by the client.</span></span>|<span data-ttu-id="8791c-168">Non</span><span class="sxs-lookup"><span data-stu-id="8791c-168">No</span></span>|<span data-ttu-id="8791c-169">N/A</span><span class="sxs-lookup"><span data-stu-id="8791c-169">N/A</span></span>|  
|<span data-ttu-id="8791c-170">en-tête</span><span class="sxs-lookup"><span data-stu-id="8791c-170">header</span></span>|<span data-ttu-id="8791c-171">Spécifie un nom d’en-tête.</span><span class="sxs-lookup"><span data-stu-id="8791c-171">Specifies a header name.</span></span>|<span data-ttu-id="8791c-172">Au moins un élément `header` est requis dans `allowed-headers` ou `expose-headers` si la section est présente.</span><span class="sxs-lookup"><span data-stu-id="8791c-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if the section is present.</span></span>|<span data-ttu-id="8791c-173">N/A</span><span class="sxs-lookup"><span data-stu-id="8791c-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8791c-174">Attributs</span><span class="sxs-lookup"><span data-stu-id="8791c-174">Attributes</span></span>  
  
|<span data-ttu-id="8791c-175">Nom</span><span class="sxs-lookup"><span data-stu-id="8791c-175">Name</span></span>|<span data-ttu-id="8791c-176">Description</span><span class="sxs-lookup"><span data-stu-id="8791c-176">Description</span></span>|<span data-ttu-id="8791c-177">Requis</span><span class="sxs-lookup"><span data-stu-id="8791c-177">Required</span></span>|<span data-ttu-id="8791c-178">Default</span><span class="sxs-lookup"><span data-stu-id="8791c-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8791c-179">allow-credentials</span><span class="sxs-lookup"><span data-stu-id="8791c-179">allow-credentials</span></span>|<span data-ttu-id="8791c-180">L’en-tête `Access-Control-Allow-Credentials` dans la réponse en amont est défini sur la valeur de cet attribut et affecte la capacité du client à envoyer des informations d’identification dans les demandes inter-domaines.</span><span class="sxs-lookup"><span data-stu-id="8791c-180">The `Access-Control-Allow-Credentials` header in the preflight response will be set to the value of this attribute and affect the client’s ability to submit credentials in cross-domain requests.</span></span>|<span data-ttu-id="8791c-181">Non</span><span class="sxs-lookup"><span data-stu-id="8791c-181">No</span></span>|<span data-ttu-id="8791c-182">false</span><span class="sxs-lookup"><span data-stu-id="8791c-182">false</span></span>|  
|<span data-ttu-id="8791c-183">preflight-result-max-age</span><span class="sxs-lookup"><span data-stu-id="8791c-183">preflight-result-max-age</span></span>|<span data-ttu-id="8791c-184">L’en-tête `Access-Control-Max-Age` dans la réponse en amont est défini sur la valeur de cet attribut et affecte la capacité de l’agent utilisateur à mettre en cache la réponse en amont.</span><span class="sxs-lookup"><span data-stu-id="8791c-184">The `Access-Control-Max-Age` header in the preflight response will be set to the value of this attribute and affect the user agent’s ability to cache pre-flight response.</span></span>|<span data-ttu-id="8791c-185">Non</span><span class="sxs-lookup"><span data-stu-id="8791c-185">No</span></span>|<span data-ttu-id="8791c-186">0</span><span class="sxs-lookup"><span data-stu-id="8791c-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8791c-187">Usage</span><span class="sxs-lookup"><span data-stu-id="8791c-187">Usage</span></span>  
 <span data-ttu-id="8791c-188">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="8791c-188">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8791c-189">**Sections de la stratégie :** inbound (entrant)</span><span class="sxs-lookup"><span data-stu-id="8791c-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="8791c-190">**Étendues de la stratégie :** API, operation (API, opération)</span><span class="sxs-lookup"><span data-stu-id="8791c-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="8791c-191"><a name="JSONP"></a> JSONP</span><span class="sxs-lookup"><span data-stu-id="8791c-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="8791c-192">La stratégie `jsonp` ajoute la prise en charge de JSON avec remplissage (JSONP) à une opération ou une API afin de permettre les appels inter-domaines à partir des navigateurs clients utilisant JavaScript.</span><span class="sxs-lookup"><span data-stu-id="8791c-192">The `jsonp` policy adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="8791c-193">JSONP est une méthode utilisée par les programmes JavaScript pour demander des données à un serveur se trouvant dans un autre domaine.</span><span class="sxs-lookup"><span data-stu-id="8791c-193">JSONP is a method used in JavaScript programs to request data from a server in a different domain.</span></span> <span data-ttu-id="8791c-194">JSONP passe outre la limite appliquée par la plupart des navigateurs web, selon laquelle l'accès aux pages web doit se trouver dans le même domaine.</span><span class="sxs-lookup"><span data-stu-id="8791c-194">JSONP bypasses the limitation enforced by most web browsers where access to web pages must be in the same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="8791c-195">Déclaration de stratégie</span><span class="sxs-lookup"><span data-stu-id="8791c-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="8791c-196">Exemple</span><span class="sxs-lookup"><span data-stu-id="8791c-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="8791c-197">Si vous appelez la méthode sans le paramètre de rappel ?cb=XXX, elle renvoie un code JSON simple (sans enveloppe d’appel de fonction).</span><span class="sxs-lookup"><span data-stu-id="8791c-197">If you call the method without the callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="8791c-198">Si vous ajoutez le paramètre de rappel `?cb=XXX`, il renvoie un résultat JSONP, enveloppant les résultats JSON d’origine autour de la fonction de rappel, comme `XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="8791c-198">If you add the callback parameter `?cb=XXX` it will return a JSONP result, wrapping the original JSON results around the callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="8791c-199">Éléments</span><span class="sxs-lookup"><span data-stu-id="8791c-199">Elements</span></span>  
  
|<span data-ttu-id="8791c-200">Nom</span><span class="sxs-lookup"><span data-stu-id="8791c-200">Name</span></span>|<span data-ttu-id="8791c-201">Description</span><span class="sxs-lookup"><span data-stu-id="8791c-201">Description</span></span>|<span data-ttu-id="8791c-202">Requis</span><span class="sxs-lookup"><span data-stu-id="8791c-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="8791c-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="8791c-203">jsonp</span></span>|<span data-ttu-id="8791c-204">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="8791c-204">Root element.</span></span>|<span data-ttu-id="8791c-205">Oui</span><span class="sxs-lookup"><span data-stu-id="8791c-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="8791c-206">Attributs</span><span class="sxs-lookup"><span data-stu-id="8791c-206">Attributes</span></span>  
  
|<span data-ttu-id="8791c-207">Nom</span><span class="sxs-lookup"><span data-stu-id="8791c-207">Name</span></span>|<span data-ttu-id="8791c-208">Description</span><span class="sxs-lookup"><span data-stu-id="8791c-208">Description</span></span>|<span data-ttu-id="8791c-209">Requis</span><span class="sxs-lookup"><span data-stu-id="8791c-209">Required</span></span>|<span data-ttu-id="8791c-210">Default</span><span class="sxs-lookup"><span data-stu-id="8791c-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="8791c-211">callback-parameter-name</span><span class="sxs-lookup"><span data-stu-id="8791c-211">callback-parameter-name</span></span>|<span data-ttu-id="8791c-212">Appel de fonction JavaScript interdomaines avec comme préfixe le nom de domaine complet de l'emplacement de la fonction.</span><span class="sxs-lookup"><span data-stu-id="8791c-212">The cross-domain JavaScript function call prefixed with the fully qualified domain name where the function resides.</span></span>|<span data-ttu-id="8791c-213">Oui</span><span class="sxs-lookup"><span data-stu-id="8791c-213">Yes</span></span>|<span data-ttu-id="8791c-214">N/A</span><span class="sxs-lookup"><span data-stu-id="8791c-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="8791c-215">Usage</span><span class="sxs-lookup"><span data-stu-id="8791c-215">Usage</span></span>  
 <span data-ttu-id="8791c-216">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) suivantes.</span><span class="sxs-lookup"><span data-stu-id="8791c-216">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="8791c-217">**Sections de la stratégie :** outbound (sortant)</span><span class="sxs-lookup"><span data-stu-id="8791c-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="8791c-218">**Étendues de la stratégie :** global, product, API, operation (global, produit, API, opération)</span><span class="sxs-lookup"><span data-stu-id="8791c-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="8791c-219">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8791c-219">Next steps</span></span>
<span data-ttu-id="8791c-220">Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="8791c-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  