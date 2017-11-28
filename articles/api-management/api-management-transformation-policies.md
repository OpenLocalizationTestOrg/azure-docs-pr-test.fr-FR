---
title: "stratégies de transformation de gestion des API aaaAzure | Documents Microsoft"
description: "En savoir plus sur les stratégies de transformation hello disponibles pour une utilisation dans la gestion des API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7406a8ce-5f9c-4fae-9b0f-e574befb2ee9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2891cc52d0017b717b3c12a98bc4941b5fd7ea78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="137eb-103">Stratégies de transformation de la Gestion des API</span><span class="sxs-lookup"><span data-stu-id="137eb-103">API Management transformation policies</span></span>
<span data-ttu-id="137eb-104">Cette rubrique fournit une référence pour hello suivant des stratégies de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="137eb-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="137eb-105">Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="137eb-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="137eb-106"><a name="TransformationPolicies"></a> Stratégies de transformation</span><span class="sxs-lookup"><span data-stu-id="137eb-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="137eb-107">[Convertir en JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - convertit demande ou le corps de la réponse de JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="137eb-107">[Convert JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON tooXML.</span></span>  
  
-   <span data-ttu-id="137eb-108">[Convertir XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - convertit demande ou le corps de la réponse à partir de XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="137eb-108">[Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML tooJSON.</span></span>  
  
-   <span data-ttu-id="137eb-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) : recherche une sous-chaîne de demande ou de réponse et la remplace par une autre sous-chaîne.</span><span class="sxs-lookup"><span data-stu-id="137eb-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="137eb-110">[Masquer des URL dans le contenu](api-management-transformation-policies.md#MaskURLSContent) -réécrit (masque) des liens dans la réponse de hello corps afin qu’ils pointent toohello le lien équivalent via une passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>  
  
-   <span data-ttu-id="137eb-111">[Définir le service principal](api-management-transformation-policies.md#SetBackendService) -modifie le service principal de hello pour une demande entrante.</span><span class="sxs-lookup"><span data-stu-id="137eb-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes hello backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="137eb-112">[Définir le corps](api-management-transformation-policies.md#SetBody) -définit le corps du message hello pour les demandes entrantes et sortantes.</span><span class="sxs-lookup"><span data-stu-id="137eb-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets hello message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="137eb-113">[En-tête HTTP](api-management-transformation-policies.md#SetHTTPheader) - assigne une réponse existante de valeur tooan et/ou d’un en-tête de demande ou ajoute un nouvel en-tête de réponse et/ou de demande.</span><span class="sxs-lookup"><span data-stu-id="137eb-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="137eb-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) : ajoute, supprime un paramètre de chaîne de requête de la demande ou le remplace par une autre valeur.</span><span class="sxs-lookup"><span data-stu-id="137eb-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="137eb-115">[Réécriture d’URL](api-management-transformation-policies.md#RewriteURL) -convertit une URL de demande à partir de sa forme toohello de formulaire public attendu par le service web hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form toohello form expected by hello web service.</span></span>  
  
-   <span data-ttu-id="137eb-116">[Transformer du code XML à l’aide d’une transformation XSLT](api-management-transformation-policies.md#XSLTransform) -applique un tooXML de la transformation XSL dans le corps de demande ou réponse hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
##  <span data-ttu-id="137eb-117"><a name="ConvertJSONtoXML"></a>Convertir en JSON tooXML</span><span class="sxs-lookup"><span data-stu-id="137eb-117"><a name="ConvertJSONtoXML"></a> Convert JSON tooXML</span></span>  
 <span data-ttu-id="137eb-118">Hello `json-to-xml` stratégie convertit un corps de demande ou de réponse de JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="137eb-118">hello `json-to-xml` policy converts a request or response body from JSON tooXML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="137eb-119">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="137eb-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="137eb-120">Exemple</span><span class="sxs-lookup"><span data-stu-id="137eb-120">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <json-to-xml apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="137eb-121">Éléments</span><span class="sxs-lookup"><span data-stu-id="137eb-121">Elements</span></span>  
  
|<span data-ttu-id="137eb-122">Nom</span><span class="sxs-lookup"><span data-stu-id="137eb-122">Name</span></span>|<span data-ttu-id="137eb-123">Description</span><span class="sxs-lookup"><span data-stu-id="137eb-123">Description</span></span>|<span data-ttu-id="137eb-124">Requis</span><span class="sxs-lookup"><span data-stu-id="137eb-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="137eb-125">json-to-xml</span><span class="sxs-lookup"><span data-stu-id="137eb-125">json-to-xml</span></span>|<span data-ttu-id="137eb-126">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="137eb-126">Root element.</span></span>|<span data-ttu-id="137eb-127">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="137eb-128">Attributs</span><span class="sxs-lookup"><span data-stu-id="137eb-128">Attributes</span></span>  
  
|<span data-ttu-id="137eb-129">Nom</span><span class="sxs-lookup"><span data-stu-id="137eb-129">Name</span></span>|<span data-ttu-id="137eb-130">Description</span><span class="sxs-lookup"><span data-stu-id="137eb-130">Description</span></span>|<span data-ttu-id="137eb-131">Requis</span><span class="sxs-lookup"><span data-stu-id="137eb-131">Required</span></span>|<span data-ttu-id="137eb-132">Default</span><span class="sxs-lookup"><span data-stu-id="137eb-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="137eb-133">apply</span><span class="sxs-lookup"><span data-stu-id="137eb-133">apply</span></span>|<span data-ttu-id="137eb-134">attribut de Hello doit être définie tooone Hello valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="137eb-134">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="137eb-135">-   always : toujours appliquer la conversion.</span><span class="sxs-lookup"><span data-stu-id="137eb-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="137eb-136">-   content-type-json : ne convertir que si l’en-tête de réponse Content-Type indique la présence de JSON.</span><span class="sxs-lookup"><span data-stu-id="137eb-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="137eb-137">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-137">Yes</span></span>|<span data-ttu-id="137eb-138">N/A</span><span class="sxs-lookup"><span data-stu-id="137eb-138">N/A</span></span>|  
|<span data-ttu-id="137eb-139">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="137eb-139">consider-accept-header</span></span>|<span data-ttu-id="137eb-140">attribut de Hello doit être définie tooone Hello valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="137eb-140">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="137eb-141">-   true : appliquer la conversion si le format JSON est demandé dans l’en-tête d’acceptation de la demande.</span><span class="sxs-lookup"><span data-stu-id="137eb-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="137eb-142">-   false : toujours appliquer la conversion.</span><span class="sxs-lookup"><span data-stu-id="137eb-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="137eb-143">Non</span><span class="sxs-lookup"><span data-stu-id="137eb-143">No</span></span>|<span data-ttu-id="137eb-144">true</span><span class="sxs-lookup"><span data-stu-id="137eb-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="137eb-145">Usage</span><span class="sxs-lookup"><span data-stu-id="137eb-145">Usage</span></span>  
 <span data-ttu-id="137eb-146">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="137eb-146">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="137eb-147">**Sections de la stratégie :** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="137eb-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="137eb-148">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="137eb-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="137eb-149"><a name="ConvertXMLtoJSON"></a>Convertir XML tooJSON</span><span class="sxs-lookup"><span data-stu-id="137eb-149"><a name="ConvertXMLtoJSON"></a> Convert XML tooJSON</span></span>  
 <span data-ttu-id="137eb-150">Hello `xml-to-json` stratégie convertit un corps de demande ou de réponse XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="137eb-150">hello `xml-to-json` policy converts a request or response body from XML tooJSON.</span></span> <span data-ttu-id="137eb-151">Cette stratégie peut être utilisé toomodernize API basé sur les services web principaux uniquement XML.</span><span class="sxs-lookup"><span data-stu-id="137eb-151">This policy can be used toomodernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="137eb-152">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="137eb-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="137eb-153">Exemple</span><span class="sxs-lookup"><span data-stu-id="137eb-153">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <xml-to-json kind="direct" apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="137eb-154">Éléments</span><span class="sxs-lookup"><span data-stu-id="137eb-154">Elements</span></span>  
  
|<span data-ttu-id="137eb-155">Nom</span><span class="sxs-lookup"><span data-stu-id="137eb-155">Name</span></span>|<span data-ttu-id="137eb-156">Description</span><span class="sxs-lookup"><span data-stu-id="137eb-156">Description</span></span>|<span data-ttu-id="137eb-157">Requis</span><span class="sxs-lookup"><span data-stu-id="137eb-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="137eb-158">xml-to-json</span><span class="sxs-lookup"><span data-stu-id="137eb-158">xml-to-json</span></span>|<span data-ttu-id="137eb-159">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="137eb-159">Root element.</span></span>|<span data-ttu-id="137eb-160">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="137eb-161">Attributs</span><span class="sxs-lookup"><span data-stu-id="137eb-161">Attributes</span></span>  
  
|<span data-ttu-id="137eb-162">Nom</span><span class="sxs-lookup"><span data-stu-id="137eb-162">Name</span></span>|<span data-ttu-id="137eb-163">Description</span><span class="sxs-lookup"><span data-stu-id="137eb-163">Description</span></span>|<span data-ttu-id="137eb-164">Requis</span><span class="sxs-lookup"><span data-stu-id="137eb-164">Required</span></span>|<span data-ttu-id="137eb-165">Default</span><span class="sxs-lookup"><span data-stu-id="137eb-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="137eb-166">kind</span><span class="sxs-lookup"><span data-stu-id="137eb-166">kind</span></span>|<span data-ttu-id="137eb-167">attribut de Hello doit être définie tooone Hello valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="137eb-167">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="137eb-168">-javascript friendly : hello converti JSON a un tooJavaScript convivial aux développeurs.</span><span class="sxs-lookup"><span data-stu-id="137eb-168">-   javascript-friendly - hello converted JSON has a form friendly tooJavaScript developers.</span></span><br /><span data-ttu-id="137eb-169">-direct - hello JSON converti reflète la structure de hello XML document d’origine.</span><span class="sxs-lookup"><span data-stu-id="137eb-169">-   direct - hello converted JSON reflects hello original XML document's structure.</span></span>|<span data-ttu-id="137eb-170">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-170">Yes</span></span>|<span data-ttu-id="137eb-171">N/A</span><span class="sxs-lookup"><span data-stu-id="137eb-171">N/A</span></span>|  
|<span data-ttu-id="137eb-172">apply</span><span class="sxs-lookup"><span data-stu-id="137eb-172">apply</span></span>|<span data-ttu-id="137eb-173">attribut de Hello doit être définie tooone Hello valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="137eb-173">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="137eb-174">-   always : toujours convertir.</span><span class="sxs-lookup"><span data-stu-id="137eb-174">-   always - convert always.</span></span><br /><span data-ttu-id="137eb-175">-   content-type-xml : ne convertir que si l’en-tête de réponse Content-Type indique la présence de XML.</span><span class="sxs-lookup"><span data-stu-id="137eb-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="137eb-176">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-176">Yes</span></span>|<span data-ttu-id="137eb-177">N/A</span><span class="sxs-lookup"><span data-stu-id="137eb-177">N/A</span></span>|  
|<span data-ttu-id="137eb-178">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="137eb-178">consider-accept-header</span></span>|<span data-ttu-id="137eb-179">attribut de Hello doit être définie tooone Hello valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="137eb-179">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="137eb-180">-   true : appliquer la conversion si le format XML est demandé dans l’en-tête d’acceptation de la demande.</span><span class="sxs-lookup"><span data-stu-id="137eb-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="137eb-181">-   false : toujours appliquer la conversion.</span><span class="sxs-lookup"><span data-stu-id="137eb-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="137eb-182">Non</span><span class="sxs-lookup"><span data-stu-id="137eb-182">No</span></span>|<span data-ttu-id="137eb-183">true</span><span class="sxs-lookup"><span data-stu-id="137eb-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="137eb-184">Usage</span><span class="sxs-lookup"><span data-stu-id="137eb-184">Usage</span></span>  
 <span data-ttu-id="137eb-185">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="137eb-185">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="137eb-186">**Sections de la stratégie :** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="137eb-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="137eb-187">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="137eb-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="137eb-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span><span class="sxs-lookup"><span data-stu-id="137eb-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="137eb-189">Hello `find-and-replace` stratégie recherche une sous-chaîne de demande ou de réponse et le remplace par une autre sous-chaîne.</span><span class="sxs-lookup"><span data-stu-id="137eb-189">hello `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="137eb-190">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="137eb-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="137eb-191">Exemple</span><span class="sxs-lookup"><span data-stu-id="137eb-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="137eb-192">Éléments</span><span class="sxs-lookup"><span data-stu-id="137eb-192">Elements</span></span>  
  
|<span data-ttu-id="137eb-193">Nom</span><span class="sxs-lookup"><span data-stu-id="137eb-193">Name</span></span>|<span data-ttu-id="137eb-194">Description</span><span class="sxs-lookup"><span data-stu-id="137eb-194">Description</span></span>|<span data-ttu-id="137eb-195">Requis</span><span class="sxs-lookup"><span data-stu-id="137eb-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="137eb-196">find-and-replace</span><span class="sxs-lookup"><span data-stu-id="137eb-196">find-and-replace</span></span>|<span data-ttu-id="137eb-197">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="137eb-197">Root element.</span></span>|<span data-ttu-id="137eb-198">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="137eb-199">Attributs</span><span class="sxs-lookup"><span data-stu-id="137eb-199">Attributes</span></span>  
  
|<span data-ttu-id="137eb-200">Nom</span><span class="sxs-lookup"><span data-stu-id="137eb-200">Name</span></span>|<span data-ttu-id="137eb-201">Description</span><span class="sxs-lookup"><span data-stu-id="137eb-201">Description</span></span>|<span data-ttu-id="137eb-202">Requis</span><span class="sxs-lookup"><span data-stu-id="137eb-202">Required</span></span>|<span data-ttu-id="137eb-203">Default</span><span class="sxs-lookup"><span data-stu-id="137eb-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="137eb-204">from</span><span class="sxs-lookup"><span data-stu-id="137eb-204">from</span></span>|<span data-ttu-id="137eb-205">toosearch de chaîne Hello pour.</span><span class="sxs-lookup"><span data-stu-id="137eb-205">hello string toosearch for.</span></span>|<span data-ttu-id="137eb-206">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-206">Yes</span></span>|<span data-ttu-id="137eb-207">N/A</span><span class="sxs-lookup"><span data-stu-id="137eb-207">N/A</span></span>|  
|<span data-ttu-id="137eb-208">to</span><span class="sxs-lookup"><span data-stu-id="137eb-208">to</span></span>|<span data-ttu-id="137eb-209">chaîne de remplacement Hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-209">hello replacement string.</span></span> <span data-ttu-id="137eb-210">Spécifiez une remplacement chaîne tooremove hello recherche chaîne de longueur zéro.</span><span class="sxs-lookup"><span data-stu-id="137eb-210">Specify a zero length replacement string tooremove hello search string.</span></span>|<span data-ttu-id="137eb-211">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-211">Yes</span></span>|<span data-ttu-id="137eb-212">N/A</span><span class="sxs-lookup"><span data-stu-id="137eb-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="137eb-213">Usage</span><span class="sxs-lookup"><span data-stu-id="137eb-213">Usage</span></span>  
 <span data-ttu-id="137eb-214">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="137eb-214">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="137eb-215">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="137eb-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="137eb-216">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="137eb-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="137eb-217"><a name="MaskURLSContent"></a> Mask URLs in content</span><span class="sxs-lookup"><span data-stu-id="137eb-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="137eb-218">Hello `redirect-content-urls` stratégie réécrit (masque) des liens dans le corps de la réponse hello afin qu’ils pointent toohello le lien équivalent via une passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-218">hello `redirect-content-urls` policy re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span> <span data-ttu-id="137eb-219">Utilisez-les dans toomake des liens des corps de réponse hello section sortante toore-écriture toohello de point de passerelle.</span><span class="sxs-lookup"><span data-stu-id="137eb-219">Use in hello outbound section toore-write response body links toomake them point toohello gateway.</span></span> <span data-ttu-id="137eb-220">Utilisation de hello entrants de section d’un effet opposé.</span><span class="sxs-lookup"><span data-stu-id="137eb-220">Use in hello inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="137eb-221">Cette stratégie ne change pas les valeurs d’en-têtes, notamment des en-têtes `Location`.</span><span class="sxs-lookup"><span data-stu-id="137eb-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="137eb-222">les valeurs d’en-tête toochange, utilisez hello [-en-tête](api-management-transformation-policies.md#SetHTTPheader) stratégie.</span><span class="sxs-lookup"><span data-stu-id="137eb-222">toochange header values, use hello [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="137eb-223">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="137eb-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="137eb-224">Exemple</span><span class="sxs-lookup"><span data-stu-id="137eb-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="137eb-225">Éléments</span><span class="sxs-lookup"><span data-stu-id="137eb-225">Elements</span></span>  
  
|<span data-ttu-id="137eb-226">Nom</span><span class="sxs-lookup"><span data-stu-id="137eb-226">Name</span></span>|<span data-ttu-id="137eb-227">Description</span><span class="sxs-lookup"><span data-stu-id="137eb-227">Description</span></span>|<span data-ttu-id="137eb-228">Requis</span><span class="sxs-lookup"><span data-stu-id="137eb-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="137eb-229">redirect-content-urls</span><span class="sxs-lookup"><span data-stu-id="137eb-229">redirect-content-urls</span></span>|<span data-ttu-id="137eb-230">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="137eb-230">Root element.</span></span>|<span data-ttu-id="137eb-231">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="137eb-232">Usage</span><span class="sxs-lookup"><span data-stu-id="137eb-232">Usage</span></span>  
 <span data-ttu-id="137eb-233">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="137eb-233">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="137eb-234">**Sections de la stratégie :** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="137eb-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="137eb-235">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="137eb-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="137eb-236"><a name="SetBackendService"></a> Set backend service</span><span class="sxs-lookup"><span data-stu-id="137eb-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="137eb-237">Hello d’utilisation `set-backend-service` stratégie tooredirect un entrant demande principal différent de tooa que celui spécifié dans les paramètres de hello API pour cette opération hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-237">Use hello `set-backend-service` policy tooredirect an incoming request tooa different backend than hello one specified in hello API settings for that operation.</span></span> <span data-ttu-id="137eb-238">Cette stratégie modifie hello URL du service principal de toohello demande entrants hello celui spécifié dans la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-238">This policy changes hello backend service base URL of hello incoming request toohello one specified in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="137eb-239">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="137eb-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="137eb-240">Exemple</span><span class="sxs-lookup"><span data-stu-id="137eb-240">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <choose>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2013-05")">  
                <set-backend-service base-url="http://contoso.com/api/8.2/" />  
            </when>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2014-03")">  
                <set-backend-service base-url="http://contoso.com/api/9.1/" />  
            </when>  
        </choose>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
<span data-ttu-id="137eb-241">Bonjour de cet exemple stratégie de service principal définie achemine les demandes en fonction de la valeur de la version hello passé hello requête chaîne tooa service principal différent hello hello spécifié dans une API.</span><span class="sxs-lookup"><span data-stu-id="137eb-241">In this example hello set backend service policy routes requests based on hello version value passed in hello query string tooa different backend service than hello one specified in hello API.</span></span>
  
<span data-ttu-id="137eb-242">Initialement hello URL du service principal est dérivée de paramètres de l’API hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-242">Initially hello backend service base URL is derived from hello API settings.</span></span> <span data-ttu-id="137eb-243">Hello par conséquent, les URL de demande `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` devient `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` où `http://contoso.com/api/10.4/` est l’URL du service principal hello spécifié dans les paramètres de l’API de hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-243">So hello request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is hello backend service URL specified in hello API settings.</span></span>  
  
<span data-ttu-id="137eb-244">Hello lorsque [< choisissez\> ](api-management-advanced-policies.md#choose) l’instruction de stratégie est appliquée hello URL du service principal peut changer à nouveau trop`http://contoso.com/api/8.2` ou `http://contoso.com/api/9.1`, selon la valeur hello hello version demande du paramètre de requête.</span><span class="sxs-lookup"><span data-stu-id="137eb-244">When hello [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied hello backend service base URL may change again either too`http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on hello value of hello version request query parameter.</span></span> <span data-ttu-id="137eb-245">Par exemple, si hello valeur est `"2013-15"` hello dernière demande URL devient `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span><span class="sxs-lookup"><span data-stu-id="137eb-245">For example, if hello value is `"2013-15"` hello final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="137eb-246">Si davantage la transformation de requête de hello est souhaitée, d’autres [stratégies de Transformation](api-management-transformation-policies.md#TransformationPolicies) peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="137eb-246">If further transformation of hello request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="137eb-247">Par exemple, tooremove hello version requête routé maintenant que hello demande est en cours de paramètre hello tooa version principales, [définir le paramètre de chaîne de requête](api-management-transformation-policies.md#SetQueryStringParameter) stratégie peut être l’attribut de version désormais redondant hello tooremove utilisé.</span><span class="sxs-lookup"><span data-stu-id="137eb-247">For example, tooremove hello version query parameter now that hello request is being routed tooa version specific backend, hello  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used tooremove hello now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="137eb-248">Exemple</span><span class="sxs-lookup"><span data-stu-id="137eb-248">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <set-backend-service backend-id="my-sf-service" sf-partition-key="@(context.Request.Url.Query.GetValueOrDefault("userId","")" sf-replica-type="primary" /> 
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
<span data-ttu-id="137eb-249">Dans cet exemple hello stratégie itinéraires hello demande tooa service fabric service principal, à l’aide de la chaîne de requête userId hello en tant que clé de partition hello et à l’aide de hello réplica principal de la partition de hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-249">In this example hello policy routes hello request tooa service fabric backend, using hello userId query string as hello partition key and using hello primary replica of hello partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="137eb-250">Éléments</span><span class="sxs-lookup"><span data-stu-id="137eb-250">Elements</span></span>  
  
|<span data-ttu-id="137eb-251">Nom</span><span class="sxs-lookup"><span data-stu-id="137eb-251">Name</span></span>|<span data-ttu-id="137eb-252">Description</span><span class="sxs-lookup"><span data-stu-id="137eb-252">Description</span></span>|<span data-ttu-id="137eb-253">Requis</span><span class="sxs-lookup"><span data-stu-id="137eb-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="137eb-254">set-backend-service</span><span class="sxs-lookup"><span data-stu-id="137eb-254">set-backend-service</span></span>|<span data-ttu-id="137eb-255">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="137eb-255">Root element.</span></span>|<span data-ttu-id="137eb-256">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="137eb-257">Attributs</span><span class="sxs-lookup"><span data-stu-id="137eb-257">Attributes</span></span>  
  
|<span data-ttu-id="137eb-258">Nom</span><span class="sxs-lookup"><span data-stu-id="137eb-258">Name</span></span>|<span data-ttu-id="137eb-259">Description</span><span class="sxs-lookup"><span data-stu-id="137eb-259">Description</span></span>|<span data-ttu-id="137eb-260">Requis</span><span class="sxs-lookup"><span data-stu-id="137eb-260">Required</span></span>|<span data-ttu-id="137eb-261">Default</span><span class="sxs-lookup"><span data-stu-id="137eb-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="137eb-262">base-url</span><span class="sxs-lookup"><span data-stu-id="137eb-262">base-url</span></span>|<span data-ttu-id="137eb-263">Nouvelle URL de base du service principal.</span><span class="sxs-lookup"><span data-stu-id="137eb-263">New backend service base URL.</span></span>|<span data-ttu-id="137eb-264">Non</span><span class="sxs-lookup"><span data-stu-id="137eb-264">No</span></span>|<span data-ttu-id="137eb-265">N/A</span><span class="sxs-lookup"><span data-stu-id="137eb-265">N/A</span></span>|  
|<span data-ttu-id="137eb-266">id de principal</span><span class="sxs-lookup"><span data-stu-id="137eb-266">backend-id</span></span>|<span data-ttu-id="137eb-267">Identificateur de tooroute de back-end hello pour.</span><span class="sxs-lookup"><span data-stu-id="137eb-267">Identifier of hello backend tooroute to.</span></span>|<span data-ttu-id="137eb-268">Non</span><span class="sxs-lookup"><span data-stu-id="137eb-268">No</span></span>|<span data-ttu-id="137eb-269">N/A</span><span class="sxs-lookup"><span data-stu-id="137eb-269">N/A</span></span>|  
|<span data-ttu-id="137eb-270">clé de partition SF</span><span class="sxs-lookup"><span data-stu-id="137eb-270">sf-partition-key</span></span>|<span data-ttu-id="137eb-271">S’applique seulement lorsque hello principal est un service Service Fabric et qu’il est spécifié à l’aide de 'id principal'.</span><span class="sxs-lookup"><span data-stu-id="137eb-271">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="137eb-272">Utilisé tooresolve une partition spécifique à partir du service de résolution de noms hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-272">Used tooresolve a specific partition from hello name resolution service.</span></span>|<span data-ttu-id="137eb-273">Non</span><span class="sxs-lookup"><span data-stu-id="137eb-273">No</span></span>|<span data-ttu-id="137eb-274">N/A</span><span class="sxs-lookup"><span data-stu-id="137eb-274">N/A</span></span>|  
|<span data-ttu-id="137eb-275">type de réplica SF</span><span class="sxs-lookup"><span data-stu-id="137eb-275">sf-replica-type</span></span>|<span data-ttu-id="137eb-276">S’applique seulement lorsque hello principal est un service Service Fabric et qu’il est spécifié à l’aide de 'id principal'.</span><span class="sxs-lookup"><span data-stu-id="137eb-276">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="137eb-277">Contrôle si la demande de hello doit devenir toohello un réplica principal ou secondaire d’une partition.</span><span class="sxs-lookup"><span data-stu-id="137eb-277">Controls if hello request should go toohello primary or secondary replica of a partition.</span></span> |<span data-ttu-id="137eb-278">Non</span><span class="sxs-lookup"><span data-stu-id="137eb-278">No</span></span>|<span data-ttu-id="137eb-279">N/A</span><span class="sxs-lookup"><span data-stu-id="137eb-279">N/A</span></span>|    
|<span data-ttu-id="137eb-280">condition de résolution SF</span><span class="sxs-lookup"><span data-stu-id="137eb-280">sf-resolve-condition</span></span>|<span data-ttu-id="137eb-281">Applicable uniquement lorsque hello principal est un service Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="137eb-281">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="137eb-282">Identifiant de condition Si hello appelez principal de l’ensemble fibre optique tooService a toobe répété avec la nouvelle résolution.</span><span class="sxs-lookup"><span data-stu-id="137eb-282">Condition identifying if hello call tooService Fabric backend has toobe repeated with new resolution.</span></span>|<span data-ttu-id="137eb-283">Non</span><span class="sxs-lookup"><span data-stu-id="137eb-283">No</span></span>|<span data-ttu-id="137eb-284">N/A</span><span class="sxs-lookup"><span data-stu-id="137eb-284">N/A</span></span>|    
|<span data-ttu-id="137eb-285">nom d’instance de service DF</span><span class="sxs-lookup"><span data-stu-id="137eb-285">sf-service-instance-name</span></span>|<span data-ttu-id="137eb-286">Applicable uniquement lorsque hello principal est un service Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="137eb-286">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="137eb-287">Permet des instances de service toochange lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="137eb-287">Allows toochange service instances at runtime.</span></span> |<span data-ttu-id="137eb-288">Non</span><span class="sxs-lookup"><span data-stu-id="137eb-288">No</span></span>|<span data-ttu-id="137eb-289">N/A </span><span class="sxs-lookup"><span data-stu-id="137eb-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="137eb-290">Usage</span><span class="sxs-lookup"><span data-stu-id="137eb-290">Usage</span></span>  
 <span data-ttu-id="137eb-291">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="137eb-291">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="137eb-292">**Sections de la stratégie :** inbound, backend</span><span class="sxs-lookup"><span data-stu-id="137eb-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="137eb-293">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="137eb-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="137eb-294"><a name="SetBody"></a> Set body</span><span class="sxs-lookup"><span data-stu-id="137eb-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="137eb-295">Hello d’utilisation `set-body` corps du message stratégie tooset hello pour les demandes entrantes et sortantes.</span><span class="sxs-lookup"><span data-stu-id="137eb-295">Use hello `set-body` policy tooset hello message body for incoming and outgoing requests.</span></span> <span data-ttu-id="137eb-296">tooaccess hello corps de message que vous pouvez utiliser hello `context.Request.Body` propriété ou hello `context.Response.Body`, selon que la stratégie de hello est Bonjour section entrante ou sortante.</span><span class="sxs-lookup"><span data-stu-id="137eb-296">tooaccess hello message body you can use hello `context.Request.Body` property or hello `context.Response.Body`, depending on whether hello policy is in hello inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="137eb-297">Notez que, par défaut lorsque vous accédez à hello du corps du message à l’aide `context.Request.Body` ou `context.Response.Body`, message d’origine de type hello corps est perdu et doit être défini en renvoyant le corps de hello dans expression de hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-297">Note that by default when you access hello message body using `context.Request.Body` or `context.Response.Body`, hello original message body is lost and must be set by returning hello body back in hello expression.</span></span> <span data-ttu-id="137eb-298">corps de hello toopreserve contenu, définissez hello `preserveContent` paramètre trop`true` lors de l’accès de message de type hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-298">toopreserve hello body content, set hello `preserveContent` parameter too`true` when accessing hello message.</span></span> <span data-ttu-id="137eb-299">Si `preserveContent` est défini trop`true` et un corps différent est renvoyé par l’expression de hello, hello corps est utilisé.</span><span class="sxs-lookup"><span data-stu-id="137eb-299">If `preserveContent` is set too`true` and a different body is returned by hello expression, hello returned body is used.</span></span>  
>   
>  <span data-ttu-id="137eb-300">Veuillez noter hello suivant Considérations lors de l’utilisation de hello `set-body` stratégie.</span><span class="sxs-lookup"><span data-stu-id="137eb-300">Please note hello following considerations when using hello `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="137eb-301">Si vous utilisez hello `set-body` stratégie tooreturn un corps de nouveau ou mis à jour que vous n’avez pas besoin de tooset `preserveContent` trop`true` parce que vous fournissez explicitement contenu du corps de la nouvelle hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-301">If you are using hello `set-body` policy tooreturn a new or updated body you don't need tooset `preserveContent` too`true` because you are explicitly supplying hello new body contents.</span></span>  
> -   <span data-ttu-id="137eb-302">En conservant le contenu d’une réponse hello dans pipeline entrant de hello n’a aucune signification, car il n’existe encore aucune réponse.</span><span class="sxs-lookup"><span data-stu-id="137eb-302">Preserving hello content of a response in hello inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="137eb-303">En conservant le contenu d’une demande de hello dans le pipeline de sortie hello n’a aucune signification car hello demande a déjà été envoyée toohello principal à ce stade.</span><span class="sxs-lookup"><span data-stu-id="137eb-303">Preserving hello content of a request in hello outbound pipeline doesn't make sense because hello request has already been sent toohello backend at this point.</span></span>  
> -   <span data-ttu-id="137eb-304">Si cette stratégie est utilisée en l’absence de corps de message, par exemple dans une requête GET inbound, une exception est levée.</span><span class="sxs-lookup"><span data-stu-id="137eb-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="137eb-305">Pour plus d’informations, consultez hello `context.Request.Body`, `context.Response.Body`et hello `IMessage` sections Bonjour [variable contextuelle](api-management-policy-expressions.md#ContextVariables) table.</span><span class="sxs-lookup"><span data-stu-id="137eb-305">For more information, see hello `context.Request.Body`, `context.Response.Body`, and hello `IMessage` sections in hello [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="137eb-306">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="137eb-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="137eb-307">Exemples</span><span class="sxs-lookup"><span data-stu-id="137eb-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="137eb-308">Exemple de texte littéral</span><span class="sxs-lookup"><span data-stu-id="137eb-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a><span data-ttu-id="137eb-309">Exemple d’accès au corps hello sous forme de chaîne.</span><span class="sxs-lookup"><span data-stu-id="137eb-309">Example accessing hello body as a string.</span></span> <span data-ttu-id="137eb-310">Notez que nous allons conserver les corps de la demande d’origine hello afin que nous pouvons accéder à plus tard dans le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-310">Note that we are preserving hello original request body so that we can access it later in hello pipeline.</span></span>
  
```xml  
<set-body>  
@{   
    string inBody = context.Request.Body.As<string>(preserveContent: true);   
    if (inBody[0] =='c') {   
        inBody[0] = 'm';   
    }   
    return inBody;   
}  
</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a><span data-ttu-id="137eb-311">Exemple d’accès au corps hello en tant que JObject.</span><span class="sxs-lookup"><span data-stu-id="137eb-311">Example accessing hello body as a JObject.</span></span> <span data-ttu-id="137eb-312">Notez qu’étant donné que nous ne sommes pas réservation hello d’origine corps de la demande, accès plus loin dans le pipeline de hello entraîne une exception.</span><span class="sxs-lookup"><span data-stu-id="137eb-312">Note that since we are not reserving hello original request body, accesing it later in hello pipeline will result in an exception.</span></span>  
  
```xml  
<set-body>   
@{   
    JObject inBody = context.Request.Body.As<JObject>();   
    if (inBody.attribute == <tag>) {   
        inBody[0] = 'm';   
    }   
    return inBody.ToString();   
}   
</set-body>  
  
```  
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="137eb-313">Filtrer la réponse en fonction du produit</span><span class="sxs-lookup"><span data-stu-id="137eb-313">Filter response based on product</span></span>  
 <span data-ttu-id="137eb-314">Cet exemple montre comment tooperform le filtrage de contenu en supprimant des éléments de données à partir de la réponse de hello reçu hello principal service lors de l’utilisation de hello `Starter` produit.</span><span class="sxs-lookup"><span data-stu-id="137eb-314">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="137eb-315">Pour une démonstration de la configuration et l’utilisation de cette stratégie, consultez [Cloud couvrent épisode 177 : plus les fonctionnalités de gestion des API avec Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) et avançons too34:30.</span><span class="sxs-lookup"><span data-stu-id="137eb-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="137eb-316">Démarrer à 31:50 toosee une vue d’ensemble de [hello API de prévision ciel foncé](https://developer.forecast.io/) utilisée pour cette démonstration.</span><span class="sxs-lookup"><span data-stu-id="137eb-316">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="137eb-317">Utilisation de modèles Liquid avec Set body</span><span class="sxs-lookup"><span data-stu-id="137eb-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="137eb-318">Hello `set-body` stratégie peut être configurée toouse hello [liquide](https://shopify.github.io/liquid/basics/introduction/) corps de création de modèles language tootransfom hello d’une demande ou réponse.</span><span class="sxs-lookup"><span data-stu-id="137eb-318">hello `set-body` policy can be configured toouse hello [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language tootransfom hello body of a request or response.</span></span> <span data-ttu-id="137eb-319">Cela peut être très efficace si vous avez besoin de format de hello toocompletely la mise en forme du message.</span><span class="sxs-lookup"><span data-stu-id="137eb-319">This can be very effective if you need toocompletely reshape hello format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="137eb-320">Hello d’implémentation de liquide utilisé Bonjour `set-body` stratégie est configurée en « mode C# ».</span><span class="sxs-lookup"><span data-stu-id="137eb-320">hello implementation of Liquid used in hello `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="137eb-321">Cela est particulièrement important lors d’opérations telles que le filtrage.</span><span class="sxs-lookup"><span data-stu-id="137eb-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="137eb-322">Par exemple, à l’aide d’un filtre de date nécessite l’utilisation de hello de Pascal casse et C# date mise en forme, par exemple :</span><span class="sxs-lookup"><span data-stu-id="137eb-322">As an example, using a date filter requires hello use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="137eb-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span><span class="sxs-lookup"><span data-stu-id="137eb-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="137eb-324">Dans l’ordre toocorrectly bind tooan corps de XML à l’aide du modèle de liquide hello, utilisez un `set-header` stratégie tooset Content-Type tooeither application/xml, texte/xml (ou n’importe quel type se terminant par + xml) ; pour un corps JSON, il doit être application/json, texte/json (ou fin de n’importe quel type avec + json).</span><span class="sxs-lookup"><span data-stu-id="137eb-324">In order toocorrectly bind tooan XML body using hello Liquid template, use a `set-header` policy tooset Content-Type tooeither application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-toosoap-using-a-liquid-template"></a><span data-ttu-id="137eb-325">Convertir tooSOAP JSON à l’aide d’un modèle liquide</span><span class="sxs-lookup"><span data-stu-id="137eb-325">Convert JSON tooSOAP using a Liquid template</span></span>
```xml
<set-body template="liquid">
    <soap:Envelope xmlns="http://tempuri.org/" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <GetOpenOrders>
                <cust>{{body.getOpenOrders.cust}}</cust>
            </GetOpenOrders>
        </soap:Body>
    </soap:Envelope>
</set-body>
```

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="137eb-326">Transformation de JSON à l’aide d’un modèle Liquid</span><span class="sxs-lookup"><span data-stu-id="137eb-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="137eb-327">Éléments</span><span class="sxs-lookup"><span data-stu-id="137eb-327">Elements</span></span>  
  
|<span data-ttu-id="137eb-328">Nom</span><span class="sxs-lookup"><span data-stu-id="137eb-328">Name</span></span>|<span data-ttu-id="137eb-329">Description</span><span class="sxs-lookup"><span data-stu-id="137eb-329">Description</span></span>|<span data-ttu-id="137eb-330">Requis</span><span class="sxs-lookup"><span data-stu-id="137eb-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="137eb-331">set-body</span><span class="sxs-lookup"><span data-stu-id="137eb-331">set-body</span></span>|<span data-ttu-id="137eb-332">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="137eb-332">Root element.</span></span> <span data-ttu-id="137eb-333">Contient hello corps du texte ou une expression qui renvoie un corps.</span><span class="sxs-lookup"><span data-stu-id="137eb-333">Contains hello body text or an expressions that returns a body.</span></span>|<span data-ttu-id="137eb-334">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="137eb-335">Propriétés</span><span class="sxs-lookup"><span data-stu-id="137eb-335">Properties</span></span>  
  
|<span data-ttu-id="137eb-336">Nom</span><span class="sxs-lookup"><span data-stu-id="137eb-336">Name</span></span>|<span data-ttu-id="137eb-337">Description</span><span class="sxs-lookup"><span data-stu-id="137eb-337">Description</span></span>|<span data-ttu-id="137eb-338">Requis</span><span class="sxs-lookup"><span data-stu-id="137eb-338">Required</span></span>|<span data-ttu-id="137eb-339">Default</span><span class="sxs-lookup"><span data-stu-id="137eb-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="137eb-340">template</span><span class="sxs-lookup"><span data-stu-id="137eb-340">template</span></span>|<span data-ttu-id="137eb-341">Mode de création de modèles toochange utilisé hello hello ensemble corps de la stratégie s’exécutera dans.</span><span class="sxs-lookup"><span data-stu-id="137eb-341">Used toochange hello templating mode that hello set body policy will run in.</span></span> <span data-ttu-id="137eb-342">Valeur de hello uniquement pris en charge actuellement est :</span><span class="sxs-lookup"><span data-stu-id="137eb-342">Currently hello only supported value is:</span></span><br /><br /><span data-ttu-id="137eb-343">hello - liquide - définir une stratégie corps utilisera le moteur de création de modèles liquide hello</span><span class="sxs-lookup"><span data-stu-id="137eb-343">- liquid - hello set body policy will use hello liquid templating engine</span></span> |<span data-ttu-id="137eb-344">Non</span><span class="sxs-lookup"><span data-stu-id="137eb-344">No</span></span>|<span data-ttu-id="137eb-345">liquid</span><span class="sxs-lookup"><span data-stu-id="137eb-345">liquid</span></span>|  

<span data-ttu-id="137eb-346">Pour accéder aux informations sur la demande de hello et de réponse, hello liquide peut liez par modèle objet de contexte tooa avec hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="137eb-346">For accessing information about hello request and response, hello Liquid template can bind tooa context object with hello following properties:</span></span> <br />
<pre>context.
    Request.
        Url
        Method
        OriginalMethod
        OriginalUrl
        IpAddress
        MatchedParameters
        HasBody
        ClientCertificates
        Headers

    Response.
        StatusCode
        Method
        Headers
Url.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString

OriginalUrl.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString
</pre>



### <a name="usage"></a><span data-ttu-id="137eb-347">Usage</span><span class="sxs-lookup"><span data-stu-id="137eb-347">Usage</span></span>  
 <span data-ttu-id="137eb-348">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="137eb-348">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="137eb-349">**Sections de la stratégie :** inbound, outbound, backend</span><span class="sxs-lookup"><span data-stu-id="137eb-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="137eb-350">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="137eb-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="137eb-351"><a name="SetHTTPheader"></a> Set HTTP header</span><span class="sxs-lookup"><span data-stu-id="137eb-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="137eb-352">Hello `set-header` stratégie affecte une réponse existante de valeur tooan et/ou d’un en-tête de demande ou ajoute un nouvel en-tête de réponse et/ou de demande.</span><span class="sxs-lookup"><span data-stu-id="137eb-352">hello `set-header` policy assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="137eb-353">Insère une liste d'en-têtes HTTP dans un message HTTP.</span><span class="sxs-lookup"><span data-stu-id="137eb-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="137eb-354">Lorsqu’elle est placée dans un pipeline entrant, cette stratégie définit les en-têtes HTTP hello pour demande hello transmise service cible de toohello.</span><span class="sxs-lookup"><span data-stu-id="137eb-354">When placed in an inbound pipeline, this policy sets hello HTTP headers for hello request being passed toohello target service.</span></span> <span data-ttu-id="137eb-355">Lorsqu’elle est placée dans un pipeline sortant, cette stratégie définit les en-têtes HTTP hello pour réponse hello envoyée client de la passerelle toohello.</span><span class="sxs-lookup"><span data-stu-id="137eb-355">When placed in an outbound pipeline, this policy sets hello HTTP headers for hello response being sent toohello gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="137eb-356">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="137eb-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="137eb-357">Exemples</span><span class="sxs-lookup"><span data-stu-id="137eb-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="137eb-358">Exemple</span><span class="sxs-lookup"><span data-stu-id="137eb-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="137eb-359">Transférer le service principal de contexte informations toohello</span><span class="sxs-lookup"><span data-stu-id="137eb-359">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="137eb-360">Cet exemple montre comment stratégie tooapply à hello API niveau le service principal toohello toosupply contexte plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="137eb-360">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="137eb-361">Pour une démonstration de la configuration et l’utilisation de cette stratégie, consultez [Cloud couvrent épisode 177 : plus les fonctionnalités de gestion des API avec Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) et avançons too10:30.</span><span class="sxs-lookup"><span data-stu-id="137eb-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="137eb-362">À 12:10, il existe une démonstration de l’appel à une opération dans le portail des développeurs hello où vous pouvez consulter la stratégie hello au travail.</span><span class="sxs-lookup"><span data-stu-id="137eb-362">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="137eb-363">Pour plus d’informations, consultez les pages [Expressions de stratégie](api-management-policy-expressions.md) et [Variable de contexte](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="137eb-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="137eb-364">Éléments</span><span class="sxs-lookup"><span data-stu-id="137eb-364">Elements</span></span>  
  
|<span data-ttu-id="137eb-365">Nom</span><span class="sxs-lookup"><span data-stu-id="137eb-365">Name</span></span>|<span data-ttu-id="137eb-366">Description</span><span class="sxs-lookup"><span data-stu-id="137eb-366">Description</span></span>|<span data-ttu-id="137eb-367">Requis</span><span class="sxs-lookup"><span data-stu-id="137eb-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="137eb-368">set-header</span><span class="sxs-lookup"><span data-stu-id="137eb-368">set-header</span></span>|<span data-ttu-id="137eb-369">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="137eb-369">Root element.</span></span>|<span data-ttu-id="137eb-370">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-370">Yes</span></span>|  
|<span data-ttu-id="137eb-371">value</span><span class="sxs-lookup"><span data-stu-id="137eb-371">value</span></span>|<span data-ttu-id="137eb-372">Spécifie la valeur hello hello en-tête toobe ensemble.</span><span class="sxs-lookup"><span data-stu-id="137eb-372">Specifies hello value of hello header toobe set.</span></span> <span data-ttu-id="137eb-373">Pour plusieurs en-têtes hello avec le même nom, ajoutez des `value` éléments.</span><span class="sxs-lookup"><span data-stu-id="137eb-373">For multiple headers with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="137eb-374">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="137eb-375">Propriétés</span><span class="sxs-lookup"><span data-stu-id="137eb-375">Properties</span></span>  
  
|<span data-ttu-id="137eb-376">Nom</span><span class="sxs-lookup"><span data-stu-id="137eb-376">Name</span></span>|<span data-ttu-id="137eb-377">Description</span><span class="sxs-lookup"><span data-stu-id="137eb-377">Description</span></span>|<span data-ttu-id="137eb-378">Requis</span><span class="sxs-lookup"><span data-stu-id="137eb-378">Required</span></span>|<span data-ttu-id="137eb-379">Default</span><span class="sxs-lookup"><span data-stu-id="137eb-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="137eb-380">exists-action</span><span class="sxs-lookup"><span data-stu-id="137eb-380">exists-action</span></span>|<span data-ttu-id="137eb-381">Spécifie quelles tootake action lorsque hello en-tête est déjà spécifié.</span><span class="sxs-lookup"><span data-stu-id="137eb-381">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="137eb-382">Cet attribut doit avoir une des valeurs suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-382">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="137eb-383">-remplacer - valeur de hello remplace d’en-tête existant de hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-383">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="137eb-384">-ignorer - ne remplace pas la valeur d’en-tête hello existant.</span><span class="sxs-lookup"><span data-stu-id="137eb-384">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="137eb-385">-Ajouter - ajoute la valeur d’en-tête existant hello valeur toohello.</span><span class="sxs-lookup"><span data-stu-id="137eb-385">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="137eb-386">-Supprimer - supprime les en-tête de hello de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-386">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="137eb-387">Lorsque la valeur trop`override` l’inscription de plusieurs entrées avec hello même nom que les résultats dans l’en-tête de hello en cours en fonction tooall entrées (qui apparaissent plusieurs fois) ; seules les valeurs inscrites seront définies dans le résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-387">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="137eb-388">Non</span><span class="sxs-lookup"><span data-stu-id="137eb-388">No</span></span>|<span data-ttu-id="137eb-389">override</span><span class="sxs-lookup"><span data-stu-id="137eb-389">override</span></span>|  
|<span data-ttu-id="137eb-390">name</span><span class="sxs-lookup"><span data-stu-id="137eb-390">name</span></span>|<span data-ttu-id="137eb-391">Spécifie le nom du jeu de toobe en-tête hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-391">Specifies name of hello header toobe set.</span></span>|<span data-ttu-id="137eb-392">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-392">Yes</span></span>|<span data-ttu-id="137eb-393">N/A</span><span class="sxs-lookup"><span data-stu-id="137eb-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="137eb-394">Usage</span><span class="sxs-lookup"><span data-stu-id="137eb-394">Usage</span></span>  
 <span data-ttu-id="137eb-395">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="137eb-395">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="137eb-396">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="137eb-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="137eb-397">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="137eb-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="137eb-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span><span class="sxs-lookup"><span data-stu-id="137eb-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="137eb-399">Hello `set-query-parameter` ajoute de la stratégie, remplace la valeur, ou paramètre de chaîne de requête de demande de suppressions.</span><span class="sxs-lookup"><span data-stu-id="137eb-399">hello `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="137eb-400">Peut être utilisé toopass paramètres de requête attendus par le service principal hello, qui sont facultatifs ou toujours absents dans la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-400">Can be used toopass query parameters expected by hello backend service which are optional or never present in hello request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="137eb-401">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="137eb-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="137eb-402">Exemples</span><span class="sxs-lookup"><span data-stu-id="137eb-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="137eb-403">Exemple</span><span class="sxs-lookup"><span data-stu-id="137eb-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="137eb-404">Transférer le service principal de contexte informations toohello</span><span class="sxs-lookup"><span data-stu-id="137eb-404">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="137eb-405">Cet exemple montre comment stratégie tooapply à hello API niveau le service principal toohello toosupply contexte plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="137eb-405">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="137eb-406">Pour une démonstration de la configuration et l’utilisation de cette stratégie, consultez [Cloud couvrent épisode 177 : plus les fonctionnalités de gestion des API avec Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) et avançons too10:30.</span><span class="sxs-lookup"><span data-stu-id="137eb-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="137eb-407">À 12:10, il existe une démonstration de l’appel à une opération dans le portail des développeurs hello où vous pouvez consulter la stratégie hello au travail.</span><span class="sxs-lookup"><span data-stu-id="137eb-407">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="137eb-408">Pour plus d’informations, consultez les pages [Expressions de stratégie](api-management-policy-expressions.md) et [Variable de contexte](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="137eb-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="137eb-409">Éléments</span><span class="sxs-lookup"><span data-stu-id="137eb-409">Elements</span></span>  
  
|<span data-ttu-id="137eb-410">Nom</span><span class="sxs-lookup"><span data-stu-id="137eb-410">Name</span></span>|<span data-ttu-id="137eb-411">Description</span><span class="sxs-lookup"><span data-stu-id="137eb-411">Description</span></span>|<span data-ttu-id="137eb-412">Requis</span><span class="sxs-lookup"><span data-stu-id="137eb-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="137eb-413">set-query-parameter</span><span class="sxs-lookup"><span data-stu-id="137eb-413">set-query-parameter</span></span>|<span data-ttu-id="137eb-414">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="137eb-414">Root element.</span></span>|<span data-ttu-id="137eb-415">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-415">Yes</span></span>|  
|<span data-ttu-id="137eb-416">value</span><span class="sxs-lookup"><span data-stu-id="137eb-416">value</span></span>|<span data-ttu-id="137eb-417">Spécifie la valeur hello hello paramètre toobe du jeu de requête.</span><span class="sxs-lookup"><span data-stu-id="137eb-417">Specifies hello value of hello query parameter toobe set.</span></span> <span data-ttu-id="137eb-418">Plusieurs paramètres de requête par hello même nom, ajoutez des `value` éléments.</span><span class="sxs-lookup"><span data-stu-id="137eb-418">For multiple query parameters with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="137eb-419">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="137eb-420">Propriétés</span><span class="sxs-lookup"><span data-stu-id="137eb-420">Properties</span></span>  
  
|<span data-ttu-id="137eb-421">Nom</span><span class="sxs-lookup"><span data-stu-id="137eb-421">Name</span></span>|<span data-ttu-id="137eb-422">Description</span><span class="sxs-lookup"><span data-stu-id="137eb-422">Description</span></span>|<span data-ttu-id="137eb-423">Requis</span><span class="sxs-lookup"><span data-stu-id="137eb-423">Required</span></span>|<span data-ttu-id="137eb-424">Default</span><span class="sxs-lookup"><span data-stu-id="137eb-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="137eb-425">exists-action</span><span class="sxs-lookup"><span data-stu-id="137eb-425">exists-action</span></span>|<span data-ttu-id="137eb-426">Spécifie quelles tootake action lorsque le paramètre de requête hello est déjà spécifié.</span><span class="sxs-lookup"><span data-stu-id="137eb-426">Specifies what action tootake when hello query parameter is already specified.</span></span> <span data-ttu-id="137eb-427">Cet attribut doit avoir une des valeurs suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-427">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="137eb-428">-remplacer - valeur hello remplace paramètre existant hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-428">-   override - replaces hello value of hello existing parameter.</span></span><br /><span data-ttu-id="137eb-429">-ignorer - ne remplace pas la valeur de paramètre de requête existant hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-429">-   skip - does not replace hello existing query parameter value.</span></span><br /><span data-ttu-id="137eb-430">-Ajouter - ajoute la valeur du paramètre requête existant hello valeur toohello.</span><span class="sxs-lookup"><span data-stu-id="137eb-430">-   append - appends hello value toohello existing query parameter value.</span></span><br /><span data-ttu-id="137eb-431">-Supprimer - supprime le paramètre de requête hello à partir de la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-431">-   delete - removes hello query parameter from hello request.</span></span><br /><br /> <span data-ttu-id="137eb-432">Lorsque la valeur trop`override` l’inscription de plusieurs entrées avec hello même nom que les résultats dans le paramètre de requête hello en cours en fonction tooall entrées (qui apparaissent plusieurs fois) ; seules les valeurs inscrites seront définies dans le résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-432">When set too`override` enlisting multiple entries with hello same name results in hello query parameter being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="137eb-433">Non</span><span class="sxs-lookup"><span data-stu-id="137eb-433">No</span></span>|<span data-ttu-id="137eb-434">override</span><span class="sxs-lookup"><span data-stu-id="137eb-434">override</span></span>|  
|<span data-ttu-id="137eb-435">name</span><span class="sxs-lookup"><span data-stu-id="137eb-435">name</span></span>|<span data-ttu-id="137eb-436">Spécifie le nom du jeu de toobe de paramètre de requête hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-436">Specifies name of hello query parameter toobe set.</span></span>|<span data-ttu-id="137eb-437">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-437">Yes</span></span>|<span data-ttu-id="137eb-438">N/A</span><span class="sxs-lookup"><span data-stu-id="137eb-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="137eb-439">Usage</span><span class="sxs-lookup"><span data-stu-id="137eb-439">Usage</span></span>  
 <span data-ttu-id="137eb-440">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="137eb-440">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="137eb-441">**Sections de la stratégie :** inbound, backend</span><span class="sxs-lookup"><span data-stu-id="137eb-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="137eb-442">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="137eb-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="137eb-443"><a name="RewriteURL"></a> Rewrite URL</span><span class="sxs-lookup"><span data-stu-id="137eb-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="137eb-444">Hello `rewrite-uri` stratégie convertit une URL de demande à partir de sa forme toohello de formulaire public attendu par le service web hello, comme illustré dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="137eb-444">hello `rewrite-uri` policy converts a request URL from its public form toohello form expected by hello web service, as shown in hello following example.</span></span>  
  
-   <span data-ttu-id="137eb-445">URL publique : `http://api.example.com/storenumber/ordernumber`</span><span class="sxs-lookup"><span data-stu-id="137eb-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="137eb-446">URL de la demande : `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span><span class="sxs-lookup"><span data-stu-id="137eb-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="137eb-447">Cette stratégie peut être utilisée lorsqu’une URL de l’opérateur humaine et/ou le nom convivial de l’Explorateur doit être transformée en format d’URL hello attendu par le service web hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-447">This policy can be used when a human and/or browser-friendly URL should be transformed into hello URL format expected by hello web service.</span></span> <span data-ttu-id="137eb-448">Cette stratégie ne doit toobe appliqué lors de l’exposition d’un autre format d’URL, tels que les URL propre, URL RESTful, une URL conviviale ou les URL compatibles avec les moteurs de recherche qui sont des URL purement structurelles qui ne contient pas une chaîne de requête et à la place contenir uniquement hello chemin d’accès de hello ressources (après le schéma de hello et autorité de hello).</span><span class="sxs-lookup"><span data-stu-id="137eb-448">This policy only needs toobe applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only hello path of hello resource (after hello scheme and hello authority).</span></span> <span data-ttu-id="137eb-449">C'est souvent le cas pour des raisons d'esthétique, de simplicité d'utilisation ou bien pour l'optimisation des résultats de recherche (SEO).</span><span class="sxs-lookup"><span data-stu-id="137eb-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="137eb-450">Vous pouvez uniquement ajouter des paramètres de chaîne de requête à l’aide de la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-450">You can only add query string parameters using hello policy.</span></span> <span data-ttu-id="137eb-451">Vous ne pouvez pas ajouter de paramètres de chemin d’accès de modèle supplémentaire dans hello réécriture d’URL.</span><span class="sxs-lookup"><span data-stu-id="137eb-451">You cannot add extra template path parameters in hello rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="137eb-452">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="137eb-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="137eb-453">Exemple</span><span class="sxs-lookup"><span data-stu-id="137eb-453">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/v2/US/hardware/{storenumber}&{ordernumber}?City=city&State=state" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put?c=d -->
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" copy-unmatched-params="false" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put -->
```

### <a name="elements"></a><span data-ttu-id="137eb-454">Éléments</span><span class="sxs-lookup"><span data-stu-id="137eb-454">Elements</span></span>  
  
|<span data-ttu-id="137eb-455">Nom</span><span class="sxs-lookup"><span data-stu-id="137eb-455">Name</span></span>|<span data-ttu-id="137eb-456">Description</span><span class="sxs-lookup"><span data-stu-id="137eb-456">Description</span></span>|<span data-ttu-id="137eb-457">Requis</span><span class="sxs-lookup"><span data-stu-id="137eb-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="137eb-458">rewrite-uri</span><span class="sxs-lookup"><span data-stu-id="137eb-458">rewrite-uri</span></span>|<span data-ttu-id="137eb-459">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="137eb-459">Root element.</span></span>|<span data-ttu-id="137eb-460">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="137eb-461">Attributs</span><span class="sxs-lookup"><span data-stu-id="137eb-461">Attributes</span></span>  
  
|<span data-ttu-id="137eb-462">Attribut</span><span class="sxs-lookup"><span data-stu-id="137eb-462">Attribute</span></span>|<span data-ttu-id="137eb-463">Description</span><span class="sxs-lookup"><span data-stu-id="137eb-463">Description</span></span>|<span data-ttu-id="137eb-464">Requis</span><span class="sxs-lookup"><span data-stu-id="137eb-464">Required</span></span>|<span data-ttu-id="137eb-465">Default</span><span class="sxs-lookup"><span data-stu-id="137eb-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="137eb-466">template</span><span class="sxs-lookup"><span data-stu-id="137eb-466">template</span></span>|<span data-ttu-id="137eb-467">URL du service web réel Hello avec les paramètres de chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="137eb-467">hello actual web service URL with any query string parameters.</span></span> <span data-ttu-id="137eb-468">Lorsque vous utilisez des expressions, toute valeur de hello doit être une expression.</span><span class="sxs-lookup"><span data-stu-id="137eb-468">When using expressions, hello whole value must be an expression.</span></span>|<span data-ttu-id="137eb-469">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-469">Yes</span></span>|<span data-ttu-id="137eb-470">N/A</span><span class="sxs-lookup"><span data-stu-id="137eb-470">N/A</span></span>|  
|<span data-ttu-id="137eb-471">copy-unmatched-params</span><span class="sxs-lookup"><span data-stu-id="137eb-471">copy-unmatched-params</span></span>|<span data-ttu-id="137eb-472">Spécifie si les paramètres de requête dans la demande entrante de hello ne figure pas dans le modèle d’URL d’origine hello sont ajoutés les URL toohello définie par hello rédigez à nouveau modèle</span><span class="sxs-lookup"><span data-stu-id="137eb-472">Specifies whether query parameters in hello incoming request not present in hello original URL template are added toohello URL defined by hello re-write template</span></span>|<span data-ttu-id="137eb-473">Non</span><span class="sxs-lookup"><span data-stu-id="137eb-473">No</span></span>|<span data-ttu-id="137eb-474">true</span><span class="sxs-lookup"><span data-stu-id="137eb-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="137eb-475">Usage</span><span class="sxs-lookup"><span data-stu-id="137eb-475">Usage</span></span>  
 <span data-ttu-id="137eb-476">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="137eb-476">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="137eb-477">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="137eb-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="137eb-478">**Étendues de la stratégie :** product, API, operation</span><span class="sxs-lookup"><span data-stu-id="137eb-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="137eb-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span><span class="sxs-lookup"><span data-stu-id="137eb-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="137eb-480">Hello `Transform XML using an XSLT` stratégie s’applique à une tooXML de la transformation XSL dans le corps de demande ou réponse hello.</span><span class="sxs-lookup"><span data-stu-id="137eb-480">hello `Transform XML using an XSLT` policy applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="137eb-481">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="137eb-481">Policy statement</span></span>  
  
```xml  
<xsl-transform>  
    <parameter name="User-Agent">@(context.Request.Headers.GetValueOrDefault("User-Agent","non-specified"))</parameter>  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
        <xsl:output method="xml" indent="yes" />  
        <xsl:param name="User-Agent" />  
        <xsl:template match="* | @* | node()">  
            <xsl:copy>  
                <xsl:if test="self::* and not(parent::*)">  
                    <xsl:attribute name="User-Agent">  
                        <xsl:value-of select="$User-Agent" />  
                    </xsl:attribute>  
                </xsl:if>  
                <xsl:apply-templates select="* | @* | node()" />  
            </xsl:copy>  
        </xsl:template>  
    </xsl:stylesheet>  
  </xsl-transform>  
```  
  
### <a name="example"></a><span data-ttu-id="137eb-482">Exemple</span><span class="sxs-lookup"><span data-stu-id="137eb-482">Example</span></span>  
  
```xml  
<policies>  
  <inbound>  
      <base />  
  </inbound>  
  <outbound>  
      <base />  
      <xsl-transform>  
        <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
            <xsl:output omit-xml-declaration="yes" method="xml" indent="yes" />  
            <!-- Copy all nodes directly-->  
            <xsl:template match="node()| @*|*">  
                <xsl:copy>  
                    <xsl:apply-templates select="@* | node()|*" />  
                </xsl:copy>  
            </xsl:template>  
        </xsl:stylesheet>  
    </xsl-transform>  
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="137eb-483">Éléments</span><span class="sxs-lookup"><span data-stu-id="137eb-483">Elements</span></span>  
  
|<span data-ttu-id="137eb-484">Nom</span><span class="sxs-lookup"><span data-stu-id="137eb-484">Name</span></span>|<span data-ttu-id="137eb-485">Description</span><span class="sxs-lookup"><span data-stu-id="137eb-485">Description</span></span>|<span data-ttu-id="137eb-486">Requis</span><span class="sxs-lookup"><span data-stu-id="137eb-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="137eb-487">xsl-transform</span><span class="sxs-lookup"><span data-stu-id="137eb-487">xsl-transform</span></span>|<span data-ttu-id="137eb-488">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="137eb-488">Root element.</span></span>|<span data-ttu-id="137eb-489">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-489">Yes</span></span>|  
|<span data-ttu-id="137eb-490">paramètre</span><span class="sxs-lookup"><span data-stu-id="137eb-490">parameter</span></span>|<span data-ttu-id="137eb-491">Variables utilisées toodefine utilisées dans une transformation hello</span><span class="sxs-lookup"><span data-stu-id="137eb-491">Used toodefine variables used in hello transform</span></span>|<span data-ttu-id="137eb-492">Non</span><span class="sxs-lookup"><span data-stu-id="137eb-492">No</span></span>|  
|<span data-ttu-id="137eb-493">xsl:stylesheet</span><span class="sxs-lookup"><span data-stu-id="137eb-493">xsl:stylesheet</span></span>|<span data-ttu-id="137eb-494">Élément feuille de style racine.</span><span class="sxs-lookup"><span data-stu-id="137eb-494">Root stylesheet element.</span></span> <span data-ttu-id="137eb-495">Tous les éléments et attributs définis dans suivent standard de hello [spécification XSLT](http://www.w3.org/TR/xslt)</span><span class="sxs-lookup"><span data-stu-id="137eb-495">All elements and attributes defined within follow hello standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="137eb-496">Oui</span><span class="sxs-lookup"><span data-stu-id="137eb-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="137eb-497">Usage</span><span class="sxs-lookup"><span data-stu-id="137eb-497">Usage</span></span>  
 <span data-ttu-id="137eb-498">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="137eb-498">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="137eb-499">**Sections de la stratégie :** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="137eb-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="137eb-500">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="137eb-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="137eb-501">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="137eb-501">Next steps</span></span>
<span data-ttu-id="137eb-502">Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="137eb-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
