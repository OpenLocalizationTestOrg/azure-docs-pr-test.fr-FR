---
title: "Stratégies de transformation de la Gestion des API Azure | Microsoft Docs"
description: "Découvrez les stratégies de transformation disponibles dans la Gestion des API Azure."
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
ms.openlocfilehash: c2bed904b82c569b28a6e00d0cc9b49107c148dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="beb22-103">Stratégies de transformation de la Gestion des API</span><span class="sxs-lookup"><span data-stu-id="beb22-103">API Management transformation policies</span></span>
<span data-ttu-id="beb22-104">Cette rubrique est une ressource de référence au sujet des stratégies Gestion des API suivantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="beb22-105">Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="beb22-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="beb22-106"><a name="TransformationPolicies"></a> Stratégies de transformation</span><span class="sxs-lookup"><span data-stu-id="beb22-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="beb22-107">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) : convertit le corps de la demande ou de la réponse de JSON en XML.</span><span class="sxs-lookup"><span data-stu-id="beb22-107">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
-   <span data-ttu-id="beb22-108">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) :convertit le corps de la demande ou de la réponse de XML en JSON.</span><span class="sxs-lookup"><span data-stu-id="beb22-108">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
-   <span data-ttu-id="beb22-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) : recherche une sous-chaîne de demande ou de réponse et la remplace par une autre sous-chaîne.</span><span class="sxs-lookup"><span data-stu-id="beb22-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="beb22-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) : réécrit (masque) les liens dans le corps de la réponse afin qu’ils pointent vers un lien équivalent via la passerelle.</span><span class="sxs-lookup"><span data-stu-id="beb22-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
-   <span data-ttu-id="beb22-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) : modifie le service principal pour une demande entrante.</span><span class="sxs-lookup"><span data-stu-id="beb22-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="beb22-112">[Set body](api-management-transformation-policies.md#SetBody) : définit le corps du message pour les demandes entrantes et sortantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="beb22-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) : affecte une valeur à un en-tête de réponse et/ou de demande existant ou bien ajoute un nouvel en-tête de réponse et/ou de demande.</span><span class="sxs-lookup"><span data-stu-id="beb22-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="beb22-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) : ajoute, supprime un paramètre de chaîne de requête de la demande ou le remplace par une autre valeur.</span><span class="sxs-lookup"><span data-stu-id="beb22-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="beb22-115">[URL de réécriture](api-management-transformation-policies.md#RewriteURL) : convertit une URL de demande de sa forme publique en une forme attendue par le service web.</span><span class="sxs-lookup"><span data-stu-id="beb22-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
-   <span data-ttu-id="beb22-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) : applique une transformation de XSL en XML dans le corps de la réponse ou de la demande.</span><span class="sxs-lookup"><span data-stu-id="beb22-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
##  <span data-ttu-id="beb22-117"><a name="ConvertJSONtoXML"></a> Convert JSON to XML</span><span class="sxs-lookup"><span data-stu-id="beb22-117"><a name="ConvertJSONtoXML"></a> Convert JSON to XML</span></span>  
 <span data-ttu-id="beb22-118">La stratégie `json-to-xml` convertit le corps de la demande ou de la réponse de JSON en XML.</span><span class="sxs-lookup"><span data-stu-id="beb22-118">The `json-to-xml` policy converts a request or response body from JSON to XML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="beb22-119">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="beb22-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="beb22-120">Exemple</span><span class="sxs-lookup"><span data-stu-id="beb22-120">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="beb22-121">Éléments</span><span class="sxs-lookup"><span data-stu-id="beb22-121">Elements</span></span>  
  
|<span data-ttu-id="beb22-122">Nom</span><span class="sxs-lookup"><span data-stu-id="beb22-122">Name</span></span>|<span data-ttu-id="beb22-123">Description</span><span class="sxs-lookup"><span data-stu-id="beb22-123">Description</span></span>|<span data-ttu-id="beb22-124">Requis</span><span class="sxs-lookup"><span data-stu-id="beb22-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="beb22-125">json-to-xml</span><span class="sxs-lookup"><span data-stu-id="beb22-125">json-to-xml</span></span>|<span data-ttu-id="beb22-126">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="beb22-126">Root element.</span></span>|<span data-ttu-id="beb22-127">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="beb22-128">Attributs</span><span class="sxs-lookup"><span data-stu-id="beb22-128">Attributes</span></span>  
  
|<span data-ttu-id="beb22-129">Nom</span><span class="sxs-lookup"><span data-stu-id="beb22-129">Name</span></span>|<span data-ttu-id="beb22-130">Description</span><span class="sxs-lookup"><span data-stu-id="beb22-130">Description</span></span>|<span data-ttu-id="beb22-131">Requis</span><span class="sxs-lookup"><span data-stu-id="beb22-131">Required</span></span>|<span data-ttu-id="beb22-132">Default</span><span class="sxs-lookup"><span data-stu-id="beb22-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="beb22-133">apply</span><span class="sxs-lookup"><span data-stu-id="beb22-133">apply</span></span>|<span data-ttu-id="beb22-134">L’attribut doit avoir l’une des valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-134">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="beb22-135">-   always : toujours appliquer la conversion.</span><span class="sxs-lookup"><span data-stu-id="beb22-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="beb22-136">-   content-type-json : ne convertir que si l’en-tête de réponse Content-Type indique la présence de JSON.</span><span class="sxs-lookup"><span data-stu-id="beb22-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="beb22-137">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-137">Yes</span></span>|<span data-ttu-id="beb22-138">N/A</span><span class="sxs-lookup"><span data-stu-id="beb22-138">N/A</span></span>|  
|<span data-ttu-id="beb22-139">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="beb22-139">consider-accept-header</span></span>|<span data-ttu-id="beb22-140">L’attribut doit avoir l’une des valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-140">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="beb22-141">-   true : appliquer la conversion si le format JSON est demandé dans l’en-tête d’acceptation de la demande.</span><span class="sxs-lookup"><span data-stu-id="beb22-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="beb22-142">-   false : toujours appliquer la conversion.</span><span class="sxs-lookup"><span data-stu-id="beb22-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="beb22-143">Non</span><span class="sxs-lookup"><span data-stu-id="beb22-143">No</span></span>|<span data-ttu-id="beb22-144">true</span><span class="sxs-lookup"><span data-stu-id="beb22-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="beb22-145">Usage</span><span class="sxs-lookup"><span data-stu-id="beb22-145">Usage</span></span>  
 <span data-ttu-id="beb22-146">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-146">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="beb22-147">**Sections de la stratégie :** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="beb22-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="beb22-148">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="beb22-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="beb22-149"><a name="ConvertXMLtoJSON"></a> Convert XML to JSON</span><span class="sxs-lookup"><span data-stu-id="beb22-149"><a name="ConvertXMLtoJSON"></a> Convert XML to JSON</span></span>  
 <span data-ttu-id="beb22-150">La stratégie `xml-to-json` convertit le corps de la demande ou de la réponse de XML en JSON.</span><span class="sxs-lookup"><span data-stu-id="beb22-150">The `xml-to-json` policy converts a request or response body from XML to JSON.</span></span> <span data-ttu-id="beb22-151">Cette stratégie peut être utilisée pour moderniser les API basées sur des services web exclusivement en XML.</span><span class="sxs-lookup"><span data-stu-id="beb22-151">This policy can be used to modernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="beb22-152">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="beb22-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="beb22-153">Exemple</span><span class="sxs-lookup"><span data-stu-id="beb22-153">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="beb22-154">Éléments</span><span class="sxs-lookup"><span data-stu-id="beb22-154">Elements</span></span>  
  
|<span data-ttu-id="beb22-155">Nom</span><span class="sxs-lookup"><span data-stu-id="beb22-155">Name</span></span>|<span data-ttu-id="beb22-156">Description</span><span class="sxs-lookup"><span data-stu-id="beb22-156">Description</span></span>|<span data-ttu-id="beb22-157">Requis</span><span class="sxs-lookup"><span data-stu-id="beb22-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="beb22-158">xml-to-json</span><span class="sxs-lookup"><span data-stu-id="beb22-158">xml-to-json</span></span>|<span data-ttu-id="beb22-159">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="beb22-159">Root element.</span></span>|<span data-ttu-id="beb22-160">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="beb22-161">Attributs</span><span class="sxs-lookup"><span data-stu-id="beb22-161">Attributes</span></span>  
  
|<span data-ttu-id="beb22-162">Nom</span><span class="sxs-lookup"><span data-stu-id="beb22-162">Name</span></span>|<span data-ttu-id="beb22-163">Description</span><span class="sxs-lookup"><span data-stu-id="beb22-163">Description</span></span>|<span data-ttu-id="beb22-164">Requis</span><span class="sxs-lookup"><span data-stu-id="beb22-164">Required</span></span>|<span data-ttu-id="beb22-165">Default</span><span class="sxs-lookup"><span data-stu-id="beb22-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="beb22-166">kind</span><span class="sxs-lookup"><span data-stu-id="beb22-166">kind</span></span>|<span data-ttu-id="beb22-167">L’attribut doit avoir l’une des valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-167">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="beb22-168">-   javascript-friendly : le JSON converti présente un format familier aux développeurs JavaScript.</span><span class="sxs-lookup"><span data-stu-id="beb22-168">-   javascript-friendly - the converted JSON has a form friendly to JavaScript developers.</span></span><br /><span data-ttu-id="beb22-169">-   direct : le JSON converti reflète la structure d’origine du document XML.</span><span class="sxs-lookup"><span data-stu-id="beb22-169">-   direct - the converted JSON reflects the original XML document's structure.</span></span>|<span data-ttu-id="beb22-170">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-170">Yes</span></span>|<span data-ttu-id="beb22-171">N/A</span><span class="sxs-lookup"><span data-stu-id="beb22-171">N/A</span></span>|  
|<span data-ttu-id="beb22-172">apply</span><span class="sxs-lookup"><span data-stu-id="beb22-172">apply</span></span>|<span data-ttu-id="beb22-173">L’attribut doit avoir l’une des valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-173">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="beb22-174">-   always : toujours convertir.</span><span class="sxs-lookup"><span data-stu-id="beb22-174">-   always - convert always.</span></span><br /><span data-ttu-id="beb22-175">-   content-type-xml : ne convertir que si l’en-tête de réponse Content-Type indique la présence de XML.</span><span class="sxs-lookup"><span data-stu-id="beb22-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="beb22-176">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-176">Yes</span></span>|<span data-ttu-id="beb22-177">N/A</span><span class="sxs-lookup"><span data-stu-id="beb22-177">N/A</span></span>|  
|<span data-ttu-id="beb22-178">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="beb22-178">consider-accept-header</span></span>|<span data-ttu-id="beb22-179">L’attribut doit avoir l’une des valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-179">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="beb22-180">-   true : appliquer la conversion si le format XML est demandé dans l’en-tête d’acceptation de la demande.</span><span class="sxs-lookup"><span data-stu-id="beb22-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="beb22-181">-   false : toujours appliquer la conversion.</span><span class="sxs-lookup"><span data-stu-id="beb22-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="beb22-182">Non</span><span class="sxs-lookup"><span data-stu-id="beb22-182">No</span></span>|<span data-ttu-id="beb22-183">true</span><span class="sxs-lookup"><span data-stu-id="beb22-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="beb22-184">Usage</span><span class="sxs-lookup"><span data-stu-id="beb22-184">Usage</span></span>  
 <span data-ttu-id="beb22-185">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-185">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="beb22-186">**Sections de la stratégie :** inbound, outbound, on-error</span><span class="sxs-lookup"><span data-stu-id="beb22-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="beb22-187">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="beb22-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="beb22-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span><span class="sxs-lookup"><span data-stu-id="beb22-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="beb22-189">La stratégie `find-and-replace` recherche une sous-chaîne de demande ou de réponse et la remplace par une autre sous-chaîne.</span><span class="sxs-lookup"><span data-stu-id="beb22-189">The `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="beb22-190">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="beb22-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what to replace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="beb22-191">Exemple</span><span class="sxs-lookup"><span data-stu-id="beb22-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="beb22-192">Éléments</span><span class="sxs-lookup"><span data-stu-id="beb22-192">Elements</span></span>  
  
|<span data-ttu-id="beb22-193">Nom</span><span class="sxs-lookup"><span data-stu-id="beb22-193">Name</span></span>|<span data-ttu-id="beb22-194">Description</span><span class="sxs-lookup"><span data-stu-id="beb22-194">Description</span></span>|<span data-ttu-id="beb22-195">Requis</span><span class="sxs-lookup"><span data-stu-id="beb22-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="beb22-196">find-and-replace</span><span class="sxs-lookup"><span data-stu-id="beb22-196">find-and-replace</span></span>|<span data-ttu-id="beb22-197">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="beb22-197">Root element.</span></span>|<span data-ttu-id="beb22-198">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="beb22-199">Attributs</span><span class="sxs-lookup"><span data-stu-id="beb22-199">Attributes</span></span>  
  
|<span data-ttu-id="beb22-200">Nom</span><span class="sxs-lookup"><span data-stu-id="beb22-200">Name</span></span>|<span data-ttu-id="beb22-201">Description</span><span class="sxs-lookup"><span data-stu-id="beb22-201">Description</span></span>|<span data-ttu-id="beb22-202">Requis</span><span class="sxs-lookup"><span data-stu-id="beb22-202">Required</span></span>|<span data-ttu-id="beb22-203">Default</span><span class="sxs-lookup"><span data-stu-id="beb22-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="beb22-204">from</span><span class="sxs-lookup"><span data-stu-id="beb22-204">from</span></span>|<span data-ttu-id="beb22-205">Chaîne à rechercher.</span><span class="sxs-lookup"><span data-stu-id="beb22-205">The string to search for.</span></span>|<span data-ttu-id="beb22-206">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-206">Yes</span></span>|<span data-ttu-id="beb22-207">N/A</span><span class="sxs-lookup"><span data-stu-id="beb22-207">N/A</span></span>|  
|<span data-ttu-id="beb22-208">to</span><span class="sxs-lookup"><span data-stu-id="beb22-208">to</span></span>|<span data-ttu-id="beb22-209">Chaîne de remplacement.</span><span class="sxs-lookup"><span data-stu-id="beb22-209">The replacement string.</span></span> <span data-ttu-id="beb22-210">Spécifiez une chaîne de remplacement nulle pour supprimer la chaîne de recherche.</span><span class="sxs-lookup"><span data-stu-id="beb22-210">Specify a zero length replacement string to remove the search string.</span></span>|<span data-ttu-id="beb22-211">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-211">Yes</span></span>|<span data-ttu-id="beb22-212">N/A</span><span class="sxs-lookup"><span data-stu-id="beb22-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="beb22-213">Usage</span><span class="sxs-lookup"><span data-stu-id="beb22-213">Usage</span></span>  
 <span data-ttu-id="beb22-214">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-214">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="beb22-215">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="beb22-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="beb22-216">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="beb22-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="beb22-217"><a name="MaskURLSContent"></a> Mask URLs in content</span><span class="sxs-lookup"><span data-stu-id="beb22-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="beb22-218">La stratégie `redirect-content-urls` réécrit (masque) les liens dans le corps de la réponse afin qu’ils pointent vers un lien équivalent par l’intermédiaire de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="beb22-218">The `redirect-content-urls` policy re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span> <span data-ttu-id="beb22-219">À utiliser dans la section outbound pour réécrire les liens du corps de réponse afin qu’ils pointent vers la passerelle.</span><span class="sxs-lookup"><span data-stu-id="beb22-219">Use in the outbound section to re-write response body links to make them point to the gateway.</span></span> <span data-ttu-id="beb22-220">À utiliser dans la section inbound pour obtenir l’effet opposé.</span><span class="sxs-lookup"><span data-stu-id="beb22-220">Use in the inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="beb22-221">Cette stratégie ne change pas les valeurs d’en-têtes, notamment des en-têtes `Location`.</span><span class="sxs-lookup"><span data-stu-id="beb22-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="beb22-222">Pour modifier les valeurs d’en-têtes, utilisez la stratégie [set-header](api-management-transformation-policies.md#SetHTTPheader).</span><span class="sxs-lookup"><span data-stu-id="beb22-222">To change header values, use the [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="beb22-223">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="beb22-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="beb22-224">Exemple</span><span class="sxs-lookup"><span data-stu-id="beb22-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="beb22-225">Éléments</span><span class="sxs-lookup"><span data-stu-id="beb22-225">Elements</span></span>  
  
|<span data-ttu-id="beb22-226">Nom</span><span class="sxs-lookup"><span data-stu-id="beb22-226">Name</span></span>|<span data-ttu-id="beb22-227">Description</span><span class="sxs-lookup"><span data-stu-id="beb22-227">Description</span></span>|<span data-ttu-id="beb22-228">Requis</span><span class="sxs-lookup"><span data-stu-id="beb22-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="beb22-229">redirect-content-urls</span><span class="sxs-lookup"><span data-stu-id="beb22-229">redirect-content-urls</span></span>|<span data-ttu-id="beb22-230">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="beb22-230">Root element.</span></span>|<span data-ttu-id="beb22-231">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="beb22-232">Usage</span><span class="sxs-lookup"><span data-stu-id="beb22-232">Usage</span></span>  
 <span data-ttu-id="beb22-233">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-233">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="beb22-234">**Sections de la stratégie :** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="beb22-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="beb22-235">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="beb22-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="beb22-236"><a name="SetBackendService"></a> Set backend service</span><span class="sxs-lookup"><span data-stu-id="beb22-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="beb22-237">Utilisez la stratégie `set-backend-service` pour rediriger une demande entrante vers un service principal autre que celui qui est spécifié dans les paramètres d’API de cette opération.</span><span class="sxs-lookup"><span data-stu-id="beb22-237">Use the `set-backend-service` policy to redirect an incoming request to a different backend than the one specified in the API settings for that operation.</span></span> <span data-ttu-id="beb22-238">Cette stratégie remplace l’URL de base du service principal de la demande entrante par celle qui est spécifiée dans la stratégie.</span><span class="sxs-lookup"><span data-stu-id="beb22-238">This policy changes the backend service base URL of the incoming request to the one specified in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="beb22-239">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="beb22-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of the backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="beb22-240">Exemple</span><span class="sxs-lookup"><span data-stu-id="beb22-240">Example</span></span>  
  
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
<span data-ttu-id="beb22-241">Dans cet exemple, la stratégie du service principal définie achemine les demandes en fonction de la valeur de version transmise dans la chaîne de requête à un service principal autre que celui qui est spécifié dans l’API.</span><span class="sxs-lookup"><span data-stu-id="beb22-241">In this example the set backend service policy routes requests based on the version value passed in the query string to a different backend service than the one specified in the API.</span></span>
  
<span data-ttu-id="beb22-242">À l’origine, l’URL de base du service principal est dérivée des paramètres d’API.</span><span class="sxs-lookup"><span data-stu-id="beb22-242">Initially the backend service base URL is derived from the API settings.</span></span> <span data-ttu-id="beb22-243">Par conséquent, l’URL de la demande `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` devient `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef`, où `http://contoso.com/api/10.4/` est l’URL du service principal spécifiée dans les paramètres d’API.</span><span class="sxs-lookup"><span data-stu-id="beb22-243">So the request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is the backend service URL specified in the API settings.</span></span>  
  
<span data-ttu-id="beb22-244">Lorsque la déclaration de stratégie [<choose\>](api-management-advanced-policies.md#choose) est appliquée, l’URL de base du service principal être de nouveau remplacée par `http://contoso.com/api/8.2` ou `http://contoso.com/api/9.1`, selon la valeur du paramètre de requête de la demande de version.</span><span class="sxs-lookup"><span data-stu-id="beb22-244">When the [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied the backend service base URL may change again either to `http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on the value of the version request query parameter.</span></span> <span data-ttu-id="beb22-245">Par exemple, si la valeur est `"2013-15"`, l’URL de demande finale devient `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span><span class="sxs-lookup"><span data-stu-id="beb22-245">For example, if the value is `"2013-15"` the final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="beb22-246">Pour effectuer davantage de transformations de la demande, il est possible d’utiliser d’autres [Stratégies de transformation](api-management-transformation-policies.md#TransformationPolicies).</span><span class="sxs-lookup"><span data-stu-id="beb22-246">If further transformation of the request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="beb22-247">Par exemple, pour supprimer le paramètre de requête de la version maintenant que la demande est acheminée vers un service principal propre à la version, la stratégie [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) peut être utilisée afin de supprimer l’attribut de version désormais superflu.</span><span class="sxs-lookup"><span data-stu-id="beb22-247">For example, to remove the version query parameter now that the request is being routed to a version specific backend, the  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used to remove the now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="beb22-248">Exemple</span><span class="sxs-lookup"><span data-stu-id="beb22-248">Example</span></span>  
  
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
<span data-ttu-id="beb22-249">Dans cet exemple, la stratégie permet d’acheminer la requête vers un serveur principal Service Fabric, à l’aide de la chaîne de requêtes userid en tant que clé de partition et à l’aide du réplica primaire de la partition.</span><span class="sxs-lookup"><span data-stu-id="beb22-249">In this example the policy routes the request to a service fabric backend, using the userId query string as the partition key and using the primary replica of the partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="beb22-250">Éléments</span><span class="sxs-lookup"><span data-stu-id="beb22-250">Elements</span></span>  
  
|<span data-ttu-id="beb22-251">Nom</span><span class="sxs-lookup"><span data-stu-id="beb22-251">Name</span></span>|<span data-ttu-id="beb22-252">Description</span><span class="sxs-lookup"><span data-stu-id="beb22-252">Description</span></span>|<span data-ttu-id="beb22-253">Requis</span><span class="sxs-lookup"><span data-stu-id="beb22-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="beb22-254">set-backend-service</span><span class="sxs-lookup"><span data-stu-id="beb22-254">set-backend-service</span></span>|<span data-ttu-id="beb22-255">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="beb22-255">Root element.</span></span>|<span data-ttu-id="beb22-256">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="beb22-257">Attributs</span><span class="sxs-lookup"><span data-stu-id="beb22-257">Attributes</span></span>  
  
|<span data-ttu-id="beb22-258">Nom</span><span class="sxs-lookup"><span data-stu-id="beb22-258">Name</span></span>|<span data-ttu-id="beb22-259">Description</span><span class="sxs-lookup"><span data-stu-id="beb22-259">Description</span></span>|<span data-ttu-id="beb22-260">Requis</span><span class="sxs-lookup"><span data-stu-id="beb22-260">Required</span></span>|<span data-ttu-id="beb22-261">Default</span><span class="sxs-lookup"><span data-stu-id="beb22-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="beb22-262">base-url</span><span class="sxs-lookup"><span data-stu-id="beb22-262">base-url</span></span>|<span data-ttu-id="beb22-263">Nouvelle URL de base du service principal.</span><span class="sxs-lookup"><span data-stu-id="beb22-263">New backend service base URL.</span></span>|<span data-ttu-id="beb22-264">Non</span><span class="sxs-lookup"><span data-stu-id="beb22-264">No</span></span>|<span data-ttu-id="beb22-265">N/A</span><span class="sxs-lookup"><span data-stu-id="beb22-265">N/A</span></span>|  
|<span data-ttu-id="beb22-266">id de principal</span><span class="sxs-lookup"><span data-stu-id="beb22-266">backend-id</span></span>|<span data-ttu-id="beb22-267">Identificateur du serveur principal pour l’acheminement.</span><span class="sxs-lookup"><span data-stu-id="beb22-267">Identifier of the backend to route to.</span></span>|<span data-ttu-id="beb22-268">Non</span><span class="sxs-lookup"><span data-stu-id="beb22-268">No</span></span>|<span data-ttu-id="beb22-269">N/A</span><span class="sxs-lookup"><span data-stu-id="beb22-269">N/A</span></span>|  
|<span data-ttu-id="beb22-270">clé de partition SF</span><span class="sxs-lookup"><span data-stu-id="beb22-270">sf-partition-key</span></span>|<span data-ttu-id="beb22-271">Applicable uniquement lorsque le serveur principal est un service Service Fabric et qu’il est spécifié à l’aide de « id principal ».</span><span class="sxs-lookup"><span data-stu-id="beb22-271">Only applicable when the backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="beb22-272">Utilisé pour résoudre une partition spécifique à partir du service de résolution des noms.</span><span class="sxs-lookup"><span data-stu-id="beb22-272">Used to resolve a specific partition from the name resolution service.</span></span>|<span data-ttu-id="beb22-273">Non</span><span class="sxs-lookup"><span data-stu-id="beb22-273">No</span></span>|<span data-ttu-id="beb22-274">N/A</span><span class="sxs-lookup"><span data-stu-id="beb22-274">N/A</span></span>|  
|<span data-ttu-id="beb22-275">type de réplica SF</span><span class="sxs-lookup"><span data-stu-id="beb22-275">sf-replica-type</span></span>|<span data-ttu-id="beb22-276">Applicable uniquement lorsque le serveur principal est un service Service Fabric et qu’il est spécifié à l’aide de « id principal ».</span><span class="sxs-lookup"><span data-stu-id="beb22-276">Only applicable when the backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="beb22-277">Contrôle si la requête doit atteindre le réplica principal ou secondaire d’une partition.</span><span class="sxs-lookup"><span data-stu-id="beb22-277">Controls if the request should go to the primary or secondary replica of a partition.</span></span> |<span data-ttu-id="beb22-278">Non</span><span class="sxs-lookup"><span data-stu-id="beb22-278">No</span></span>|<span data-ttu-id="beb22-279">N/A</span><span class="sxs-lookup"><span data-stu-id="beb22-279">N/A</span></span>|    
|<span data-ttu-id="beb22-280">condition de résolution SF</span><span class="sxs-lookup"><span data-stu-id="beb22-280">sf-resolve-condition</span></span>|<span data-ttu-id="beb22-281">Applicable uniquement lorsque le serveur principal est un service Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="beb22-281">Only applicable when the backend is a Service Fabric service.</span></span> <span data-ttu-id="beb22-282">Condition identifiant si l’appel au serveur principal Service Fabric doit être répété avec une nouvelle résolution.</span><span class="sxs-lookup"><span data-stu-id="beb22-282">Condition identifying if the call to Service Fabric backend has to be repeated with new resolution.</span></span>|<span data-ttu-id="beb22-283">Non</span><span class="sxs-lookup"><span data-stu-id="beb22-283">No</span></span>|<span data-ttu-id="beb22-284">N/A</span><span class="sxs-lookup"><span data-stu-id="beb22-284">N/A</span></span>|    
|<span data-ttu-id="beb22-285">nom d’instance de service DF</span><span class="sxs-lookup"><span data-stu-id="beb22-285">sf-service-instance-name</span></span>|<span data-ttu-id="beb22-286">Applicable uniquement lorsque le serveur principal est un service Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="beb22-286">Only applicable when the backend is a Service Fabric service.</span></span> <span data-ttu-id="beb22-287">Permet de modifier les instances de service lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="beb22-287">Allows to change service instances at runtime.</span></span> |<span data-ttu-id="beb22-288">Non</span><span class="sxs-lookup"><span data-stu-id="beb22-288">No</span></span>|<span data-ttu-id="beb22-289">N/A </span><span class="sxs-lookup"><span data-stu-id="beb22-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="beb22-290">Usage</span><span class="sxs-lookup"><span data-stu-id="beb22-290">Usage</span></span>  
 <span data-ttu-id="beb22-291">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-291">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="beb22-292">**Sections de la stratégie :** inbound, backend</span><span class="sxs-lookup"><span data-stu-id="beb22-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="beb22-293">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="beb22-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="beb22-294"><a name="SetBody"></a> Set body</span><span class="sxs-lookup"><span data-stu-id="beb22-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="beb22-295">Utilisez la stratégie `set-body` pour définir le corps du message pour les demandes entrantes et sortantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-295">Use the `set-body` policy to set the message body for incoming and outgoing requests.</span></span> <span data-ttu-id="beb22-296">Pour accéder au corps du message, vous pouvez utiliser la propriété `context.Request.Body` ou `context.Response.Body`, selon que la stratégie se trouve dans la section inbound ou outbound.</span><span class="sxs-lookup"><span data-stu-id="beb22-296">To access the message body you can use the `context.Request.Body` property or the `context.Response.Body`, depending on whether the policy is in the inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="beb22-297">Notez que, par défaut, lorsque vous accédez au corps du message avec `context.Request.Body` ou `context.Response.Body`, le corps du message d’origine est perdu et doit être défini en renvoyant le corps dans l’expression.</span><span class="sxs-lookup"><span data-stu-id="beb22-297">Note that by default when you access the message body using `context.Request.Body` or `context.Response.Body`, the original message body is lost and must be set by returning the body back in the expression.</span></span> <span data-ttu-id="beb22-298">Pour conserver le contenu du corps, donnez la valeur `true` au paramètre `preserveContent` lorsque vous accédez au message.</span><span class="sxs-lookup"><span data-stu-id="beb22-298">To preserve the body content, set the `preserveContent` parameter to `true` when accessing the message.</span></span> <span data-ttu-id="beb22-299">Si `preserveContent` a la valeur `true` et qu’un autre corps est renvoyé par l’expression, le corps renvoyé est utilisé.</span><span class="sxs-lookup"><span data-stu-id="beb22-299">If `preserveContent` is set to `true` and a different body is returned by the expression, the returned body is used.</span></span>  
>   
>  <span data-ttu-id="beb22-300">Notez les points suivants lorsque vous utilisez la stratégie `set-body`.</span><span class="sxs-lookup"><span data-stu-id="beb22-300">Please note the following considerations when using the `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="beb22-301">Si vous utilisez la stratégie `set-body` pour renvoyer un nouveau corps ou un corps mis à jour, vous n’avez pas besoin de donner la valeur `true` à `preserveContent` parce que vous fournissez explicitement le nouveau contenu du corps.</span><span class="sxs-lookup"><span data-stu-id="beb22-301">If you are using the `set-body` policy to return a new or updated body you don't need to set `preserveContent` to `true` because you are explicitly supplying the new body contents.</span></span>  
> -   <span data-ttu-id="beb22-302">Conserver le contenu d’une réponse dans le pipeline inbound n’est pas judicieux, car il n’existe encore aucune réponse.</span><span class="sxs-lookup"><span data-stu-id="beb22-302">Preserving the content of a response in the inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="beb22-303">Conserver le contenu d’une demande dans le pipeline de sortie n’est pas judicieux, car la demande a déjà été envoyée au service principal à ce stade.</span><span class="sxs-lookup"><span data-stu-id="beb22-303">Preserving the content of a request in the outbound pipeline doesn't make sense because the request has already been sent to the backend at this point.</span></span>  
> -   <span data-ttu-id="beb22-304">Si cette stratégie est utilisée en l’absence de corps de message, par exemple dans une requête GET inbound, une exception est levée.</span><span class="sxs-lookup"><span data-stu-id="beb22-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="beb22-305">Pour plus d’informations, consultez les sections `context.Request.Body`, `context.Response.Body` et `IMessage` dans le tableau [Variable contextuelle](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="beb22-305">For more information, see the `context.Request.Body`, `context.Response.Body`, and the `IMessage` sections in the [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="beb22-306">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="beb22-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="beb22-307">Exemples</span><span class="sxs-lookup"><span data-stu-id="beb22-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="beb22-308">Exemple de texte littéral</span><span class="sxs-lookup"><span data-stu-id="beb22-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-the-body-as-a-string-note-that-we-are-preserving-the-original-request-body-so-that-we-can-access-it-later-in-the-pipeline"></a><span data-ttu-id="beb22-309">Exemple d’accès au corps sous forme de chaîne.</span><span class="sxs-lookup"><span data-stu-id="beb22-309">Example accessing the body as a string.</span></span> <span data-ttu-id="beb22-310">Notez que nous conservons le corps de la demande d’origine et que nous pouvons ainsi y accéder plus tard dans le pipeline.</span><span class="sxs-lookup"><span data-stu-id="beb22-310">Note that we are preserving the original request body so that we can access it later in the pipeline.</span></span>
  
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
  
#### <a name="example-accessing-the-body-as-a-jobject-note-that-since-we-are-not-reserving-the-original-request-body-accesing-it-later-in-the-pipeline-will-result-in-an-exception"></a><span data-ttu-id="beb22-311">Exemple d’accès au corps sous forme de JObject.</span><span class="sxs-lookup"><span data-stu-id="beb22-311">Example accessing the body as a JObject.</span></span> <span data-ttu-id="beb22-312">Notez que puisque nous ne conservons pas le corps de la demande d’origine, une tentative pour y accéder ultérieurement dans le pipeline entraîne une exception.</span><span class="sxs-lookup"><span data-stu-id="beb22-312">Note that since we are not reserving the original request body, accesing it later in the pipeline will result in an exception.</span></span>  
  
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
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="beb22-313">Filtrer la réponse en fonction du produit</span><span class="sxs-lookup"><span data-stu-id="beb22-313">Filter response based on product</span></span>  
 <span data-ttu-id="beb22-314">Cet exemple montre comment effectuer un filtrage du contenu en supprimant des éléments de données de la réponse reçue du service principal en cas d’utilisation du produit `Starter`.</span><span class="sxs-lookup"><span data-stu-id="beb22-314">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="beb22-315">Pour une démonstration de la configuration et de l’utilisation de cette stratégie, consultez la page [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Cloud Cover, épisode 177 : Plus de fonctionnalités de la Gestion des API avec Vlad Vinogradsky) et rendez-vous directement à 34 min 30 s.</span><span class="sxs-lookup"><span data-stu-id="beb22-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="beb22-316">Commencez à 31 min 50 s pour voir une présentation de [l’API The Dark Sky Forecast](https://developer.forecast.io/) utilisée pour cette démonstration.</span><span class="sxs-lookup"><span data-stu-id="beb22-316">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into the outbound section to remove a number of data elements from the response received from the backend service based on the name of the api product -->  
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

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="beb22-317">Utilisation de modèles Liquid avec Set body</span><span class="sxs-lookup"><span data-stu-id="beb22-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="beb22-318">La stratégie `set-body` peut être configurée pour utiliser le langage de modèle [Liquid](https://shopify.github.io/liquid/basics/introduction/) pour transformer le corps d’une requête ou réponse.</span><span class="sxs-lookup"><span data-stu-id="beb22-318">The `set-body` policy can be configured to use the [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language to transfom the body of a request or response.</span></span> <span data-ttu-id="beb22-319">Cela peut être très efficace si vous avez besoin de modifier complètement le format de votre message.</span><span class="sxs-lookup"><span data-stu-id="beb22-319">This can be very effective if you need to completely reshape the format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="beb22-320">L’implémentation Liquid utilisée dans la stratégie `set-body` est configurée en mode « C# ».</span><span class="sxs-lookup"><span data-stu-id="beb22-320">The implementation of Liquid used in the `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="beb22-321">Cela est particulièrement important lors d’opérations telles que le filtrage.</span><span class="sxs-lookup"><span data-stu-id="beb22-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="beb22-322">Par exemple, l’utilisation d’un filtre de date nécessite l’emploi de la casse Pascal et de la mise en forme de date de C#, par exemple :</span><span class="sxs-lookup"><span data-stu-id="beb22-322">As an example, using a date filter requires the use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="beb22-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span><span class="sxs-lookup"><span data-stu-id="beb22-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="beb22-324">Pour établir correctement une liaison avec un corps XML à l’aide du modèle Liquid, utilisez une stratégie `set-header` pour définir Content-Type pour application/xml, text/xml (ou n’importe quel type se terminant par +xml). Pour un corps JSON, la valeur doit être application/json, text/json (ou n’importe quel type se terminant par +json).</span><span class="sxs-lookup"><span data-stu-id="beb22-324">In order to correctly bind to an XML body using the Liquid template, use a `set-header` policy to set Content-Type to either application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-to-soap-using-a-liquid-template"></a><span data-ttu-id="beb22-325">Conversion de JSON en SOAP à l’aide d’un modèle Liquid</span><span class="sxs-lookup"><span data-stu-id="beb22-325">Convert JSON to SOAP using a Liquid template</span></span>
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

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="beb22-326">Transformation de JSON à l’aide d’un modèle Liquid</span><span class="sxs-lookup"><span data-stu-id="beb22-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="beb22-327">Éléments</span><span class="sxs-lookup"><span data-stu-id="beb22-327">Elements</span></span>  
  
|<span data-ttu-id="beb22-328">Nom</span><span class="sxs-lookup"><span data-stu-id="beb22-328">Name</span></span>|<span data-ttu-id="beb22-329">Description</span><span class="sxs-lookup"><span data-stu-id="beb22-329">Description</span></span>|<span data-ttu-id="beb22-330">Requis</span><span class="sxs-lookup"><span data-stu-id="beb22-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="beb22-331">set-body</span><span class="sxs-lookup"><span data-stu-id="beb22-331">set-body</span></span>|<span data-ttu-id="beb22-332">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="beb22-332">Root element.</span></span> <span data-ttu-id="beb22-333">Contient le corps du texte ou une expression qui renvoie un corps.</span><span class="sxs-lookup"><span data-stu-id="beb22-333">Contains the body text or an expressions that returns a body.</span></span>|<span data-ttu-id="beb22-334">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="beb22-335">Propriétés</span><span class="sxs-lookup"><span data-stu-id="beb22-335">Properties</span></span>  
  
|<span data-ttu-id="beb22-336">Nom</span><span class="sxs-lookup"><span data-stu-id="beb22-336">Name</span></span>|<span data-ttu-id="beb22-337">Description</span><span class="sxs-lookup"><span data-stu-id="beb22-337">Description</span></span>|<span data-ttu-id="beb22-338">Requis</span><span class="sxs-lookup"><span data-stu-id="beb22-338">Required</span></span>|<span data-ttu-id="beb22-339">Default</span><span class="sxs-lookup"><span data-stu-id="beb22-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="beb22-340">template</span><span class="sxs-lookup"><span data-stu-id="beb22-340">template</span></span>|<span data-ttu-id="beb22-341">Permet de modifier le mode de création du modèle dans lequel la stratégie Set body sera exécutée.</span><span class="sxs-lookup"><span data-stu-id="beb22-341">Used to change the templating mode that the set body policy will run in.</span></span> <span data-ttu-id="beb22-342">Actuellement, la seule valeur possible est :</span><span class="sxs-lookup"><span data-stu-id="beb22-342">Currently the only supported value is:</span></span><br /><br /><span data-ttu-id="beb22-343">- liquid - la stratégie Set body utilisera le moteur de création de modèle Liquid</span><span class="sxs-lookup"><span data-stu-id="beb22-343">- liquid - the set body policy will use the liquid templating engine</span></span> |<span data-ttu-id="beb22-344">Non</span><span class="sxs-lookup"><span data-stu-id="beb22-344">No</span></span>|<span data-ttu-id="beb22-345">liquid</span><span class="sxs-lookup"><span data-stu-id="beb22-345">liquid</span></span>|  

<span data-ttu-id="beb22-346">Pour accéder aux informations sur la requête et la réponse, le modèle Liquid peut lier à un objet de contexte aux propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="beb22-346">For accessing information about the request and response, the Liquid template can bind to a context object with the following properties:</span></span> <br />
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



### <a name="usage"></a><span data-ttu-id="beb22-347">Usage</span><span class="sxs-lookup"><span data-stu-id="beb22-347">Usage</span></span>  
 <span data-ttu-id="beb22-348">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-348">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="beb22-349">**Sections de la stratégie :** inbound, outbound, backend</span><span class="sxs-lookup"><span data-stu-id="beb22-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="beb22-350">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="beb22-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="beb22-351"><a name="SetHTTPheader"></a> Set HTTP header</span><span class="sxs-lookup"><span data-stu-id="beb22-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="beb22-352">La stratégie `set-header` affecte une valeur à un en-tête de réponse et/ou de demande existant ou bien ajoute un nouvel en-tête de réponse et/ou de demande.</span><span class="sxs-lookup"><span data-stu-id="beb22-352">The `set-header` policy assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="beb22-353">Insère une liste d'en-têtes HTTP dans un message HTTP.</span><span class="sxs-lookup"><span data-stu-id="beb22-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="beb22-354">Lorsqu'elle est placée dans un pipeline entrant, cette stratégie définit les en-têtes HTTP pour la demande transmise au service cible.</span><span class="sxs-lookup"><span data-stu-id="beb22-354">When placed in an inbound pipeline, this policy sets the HTTP headers for the request being passed to the target service.</span></span> <span data-ttu-id="beb22-355">Lorsqu’elle est placée dans un pipeline outbound, cette stratégie définit les en-têtes HTTP pour la réponse envoyée au client de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="beb22-355">When placed in an outbound pipeline, this policy sets the HTTP headers for the response being sent to the gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="beb22-356">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="beb22-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with the same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="beb22-357">Exemples</span><span class="sxs-lookup"><span data-stu-id="beb22-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="beb22-358">Exemple</span><span class="sxs-lookup"><span data-stu-id="beb22-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="beb22-359">Transférer des informations de contexte au service principal</span><span class="sxs-lookup"><span data-stu-id="beb22-359">Forward context information to the backend service</span></span>  
 <span data-ttu-id="beb22-360">Cet exemple montre comment appliquer la stratégie au niveau de l’API pour fournir des informations de contexte au service principal.</span><span class="sxs-lookup"><span data-stu-id="beb22-360">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="beb22-361">Pour une démonstration de la configuration et de l’utilisation de cette stratégie, consultez la page [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Cloud Cover, épisode 177 : Plus de fonctionnalités de la Gestion des API avec Vlad Vinogradsky) et rendez-vous directement à 10 min 30 s.</span><span class="sxs-lookup"><span data-stu-id="beb22-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="beb22-362">À 12 min 10 s, une démonstration de l’appel d’une opération dans le portail des développeurs montre la stratégie à l’œuvre.</span><span class="sxs-lookup"><span data-stu-id="beb22-362">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward some context information, user id and the region the gateway is hosted in, to the backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="beb22-363">Pour plus d’informations, consultez les pages [Expressions de stratégie](api-management-policy-expressions.md) et [Variable de contexte](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="beb22-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="beb22-364">Éléments</span><span class="sxs-lookup"><span data-stu-id="beb22-364">Elements</span></span>  
  
|<span data-ttu-id="beb22-365">Nom</span><span class="sxs-lookup"><span data-stu-id="beb22-365">Name</span></span>|<span data-ttu-id="beb22-366">Description</span><span class="sxs-lookup"><span data-stu-id="beb22-366">Description</span></span>|<span data-ttu-id="beb22-367">Requis</span><span class="sxs-lookup"><span data-stu-id="beb22-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="beb22-368">set-header</span><span class="sxs-lookup"><span data-stu-id="beb22-368">set-header</span></span>|<span data-ttu-id="beb22-369">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="beb22-369">Root element.</span></span>|<span data-ttu-id="beb22-370">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-370">Yes</span></span>|  
|<span data-ttu-id="beb22-371">value</span><span class="sxs-lookup"><span data-stu-id="beb22-371">value</span></span>|<span data-ttu-id="beb22-372">Spécifie la valeur de l'en-tête à définir.</span><span class="sxs-lookup"><span data-stu-id="beb22-372">Specifies the value of the header to be set.</span></span> <span data-ttu-id="beb22-373">Si plusieurs en-têtes portent le même nom, ajoutez d’autres éléments `value`.</span><span class="sxs-lookup"><span data-stu-id="beb22-373">For multiple headers with the same name add additional `value` elements.</span></span>|<span data-ttu-id="beb22-374">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="beb22-375">Propriétés</span><span class="sxs-lookup"><span data-stu-id="beb22-375">Properties</span></span>  
  
|<span data-ttu-id="beb22-376">Nom</span><span class="sxs-lookup"><span data-stu-id="beb22-376">Name</span></span>|<span data-ttu-id="beb22-377">Description</span><span class="sxs-lookup"><span data-stu-id="beb22-377">Description</span></span>|<span data-ttu-id="beb22-378">Requis</span><span class="sxs-lookup"><span data-stu-id="beb22-378">Required</span></span>|<span data-ttu-id="beb22-379">Default</span><span class="sxs-lookup"><span data-stu-id="beb22-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="beb22-380">exists-action</span><span class="sxs-lookup"><span data-stu-id="beb22-380">exists-action</span></span>|<span data-ttu-id="beb22-381">Spécifie l’action à entreprendre lorsque l’en-tête est déjà spécifié.</span><span class="sxs-lookup"><span data-stu-id="beb22-381">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="beb22-382">Cet attribut doit avoir une des valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-382">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="beb22-383">- override : remplace la valeur de l’en-tête actuel.</span><span class="sxs-lookup"><span data-stu-id="beb22-383">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="beb22-384">- skip : ne remplace pas la valeur de l’en-tête actuel.</span><span class="sxs-lookup"><span data-stu-id="beb22-384">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="beb22-385">- append : ajoute la valeur à celle de l’en-tête actuel.</span><span class="sxs-lookup"><span data-stu-id="beb22-385">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="beb22-386">- delete : supprime l’en-tête de la demande.</span><span class="sxs-lookup"><span data-stu-id="beb22-386">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="beb22-387">S’il a la valeur `override`, l’inscription de plusieurs entrées portant le même nom fait que l’en-tête est défini selon toutes les entrées (qui figurent plusieurs fois) ; seules les valeurs listées seront définies dans le résultat.</span><span class="sxs-lookup"><span data-stu-id="beb22-387">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="beb22-388">Non</span><span class="sxs-lookup"><span data-stu-id="beb22-388">No</span></span>|<span data-ttu-id="beb22-389">override</span><span class="sxs-lookup"><span data-stu-id="beb22-389">override</span></span>|  
|<span data-ttu-id="beb22-390">name</span><span class="sxs-lookup"><span data-stu-id="beb22-390">name</span></span>|<span data-ttu-id="beb22-391">Spécifie le nom de l'en-tête à définir.</span><span class="sxs-lookup"><span data-stu-id="beb22-391">Specifies name of the header to be set.</span></span>|<span data-ttu-id="beb22-392">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-392">Yes</span></span>|<span data-ttu-id="beb22-393">N/A</span><span class="sxs-lookup"><span data-stu-id="beb22-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="beb22-394">Usage</span><span class="sxs-lookup"><span data-stu-id="beb22-394">Usage</span></span>  
 <span data-ttu-id="beb22-395">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-395">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="beb22-396">**Sections de la stratégie :** inbound, outbound, backend, on-error</span><span class="sxs-lookup"><span data-stu-id="beb22-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="beb22-397">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="beb22-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="beb22-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span><span class="sxs-lookup"><span data-stu-id="beb22-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="beb22-399">La stratégie `set-query-parameter` ajoute, supprime un paramètre de chaîne de requête de la demande ou le remplace par une autre valeur.</span><span class="sxs-lookup"><span data-stu-id="beb22-399">The `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="beb22-400">Peut être utilisée pour transmettre les paramètres de requête attendus par le service principal qui sont facultatifs ou ne sont jamais présents dans la demande.</span><span class="sxs-lookup"><span data-stu-id="beb22-400">Can be used to pass query parameters expected by the backend service which are optional or never present in the request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="beb22-401">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="beb22-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with the same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="beb22-402">Exemples</span><span class="sxs-lookup"><span data-stu-id="beb22-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="beb22-403">Exemple</span><span class="sxs-lookup"><span data-stu-id="beb22-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with the same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="beb22-404">Transférer des informations de contexte au service principal</span><span class="sxs-lookup"><span data-stu-id="beb22-404">Forward context information to the backend service</span></span>  
 <span data-ttu-id="beb22-405">Cet exemple montre comment appliquer la stratégie au niveau de l’API pour fournir des informations de contexte au service principal.</span><span class="sxs-lookup"><span data-stu-id="beb22-405">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="beb22-406">Pour une démonstration de la configuration et de l’utilisation de cette stratégie, consultez la page [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Cloud Cover, épisode 177 : Plus de fonctionnalités de la Gestion des API avec Vlad Vinogradsky) et rendez-vous directement à 10 min 30 s.</span><span class="sxs-lookup"><span data-stu-id="beb22-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="beb22-407">À 12 min 10 s, une démonstration de l’appel d’une opération dans le portail des développeurs montre la stratégie à l’œuvre.</span><span class="sxs-lookup"><span data-stu-id="beb22-407">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward a piece of context, product name in this example, to the backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="beb22-408">Pour plus d’informations, consultez les pages [Expressions de stratégie](api-management-policy-expressions.md) et [Variable de contexte](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="beb22-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="beb22-409">Éléments</span><span class="sxs-lookup"><span data-stu-id="beb22-409">Elements</span></span>  
  
|<span data-ttu-id="beb22-410">Nom</span><span class="sxs-lookup"><span data-stu-id="beb22-410">Name</span></span>|<span data-ttu-id="beb22-411">Description</span><span class="sxs-lookup"><span data-stu-id="beb22-411">Description</span></span>|<span data-ttu-id="beb22-412">Requis</span><span class="sxs-lookup"><span data-stu-id="beb22-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="beb22-413">set-query-parameter</span><span class="sxs-lookup"><span data-stu-id="beb22-413">set-query-parameter</span></span>|<span data-ttu-id="beb22-414">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="beb22-414">Root element.</span></span>|<span data-ttu-id="beb22-415">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-415">Yes</span></span>|  
|<span data-ttu-id="beb22-416">value</span><span class="sxs-lookup"><span data-stu-id="beb22-416">value</span></span>|<span data-ttu-id="beb22-417">Fournissez une valeur au paramètre de requête à définir.</span><span class="sxs-lookup"><span data-stu-id="beb22-417">Specifies the value of the query parameter to be set.</span></span> <span data-ttu-id="beb22-418">Si plusieurs paramètres de requête portent le même nom, ajoutez d’autres éléments `value`.</span><span class="sxs-lookup"><span data-stu-id="beb22-418">For multiple query parameters with the same name add additional `value` elements.</span></span>|<span data-ttu-id="beb22-419">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="beb22-420">Propriétés</span><span class="sxs-lookup"><span data-stu-id="beb22-420">Properties</span></span>  
  
|<span data-ttu-id="beb22-421">Nom</span><span class="sxs-lookup"><span data-stu-id="beb22-421">Name</span></span>|<span data-ttu-id="beb22-422">Description</span><span class="sxs-lookup"><span data-stu-id="beb22-422">Description</span></span>|<span data-ttu-id="beb22-423">Requis</span><span class="sxs-lookup"><span data-stu-id="beb22-423">Required</span></span>|<span data-ttu-id="beb22-424">Default</span><span class="sxs-lookup"><span data-stu-id="beb22-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="beb22-425">exists-action</span><span class="sxs-lookup"><span data-stu-id="beb22-425">exists-action</span></span>|<span data-ttu-id="beb22-426">Spécifie l’action à entreprendre lorsque le paramètre de requête est déjà spécifié.</span><span class="sxs-lookup"><span data-stu-id="beb22-426">Specifies what action to take when the query parameter is already specified.</span></span> <span data-ttu-id="beb22-427">Cet attribut doit avoir une des valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-427">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="beb22-428">- override : remplace la valeur du paramètre actuel.</span><span class="sxs-lookup"><span data-stu-id="beb22-428">-   override - replaces the value of the existing parameter.</span></span><br /><span data-ttu-id="beb22-429">- skip : ne remplace pas la valeur du paramètre de requête actuel.</span><span class="sxs-lookup"><span data-stu-id="beb22-429">-   skip - does not replace the existing query parameter value.</span></span><br /><span data-ttu-id="beb22-430">- append : ajoute la valeur à celle du paramètre de requête actuel.</span><span class="sxs-lookup"><span data-stu-id="beb22-430">-   append - appends the value to the existing query parameter value.</span></span><br /><span data-ttu-id="beb22-431">- delete : supprime le paramètre de requête de la demande.</span><span class="sxs-lookup"><span data-stu-id="beb22-431">-   delete - removes the query parameter from the request.</span></span><br /><br /> <span data-ttu-id="beb22-432">S’il a la valeur `override`, l’ajout de plusieurs entrées portant le même nom fait que le paramètre de requête est défini selon toutes les entrées (qui figurent plusieurs fois) ; seules les valeurs listées seront définies dans le résultat.</span><span class="sxs-lookup"><span data-stu-id="beb22-432">When set to `override` enlisting multiple entries with the same name results in the query parameter being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="beb22-433">Non</span><span class="sxs-lookup"><span data-stu-id="beb22-433">No</span></span>|<span data-ttu-id="beb22-434">override</span><span class="sxs-lookup"><span data-stu-id="beb22-434">override</span></span>|  
|<span data-ttu-id="beb22-435">name</span><span class="sxs-lookup"><span data-stu-id="beb22-435">name</span></span>|<span data-ttu-id="beb22-436">Spécifie le nom du paramètre de requête à définir.</span><span class="sxs-lookup"><span data-stu-id="beb22-436">Specifies name of the query parameter to be set.</span></span>|<span data-ttu-id="beb22-437">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-437">Yes</span></span>|<span data-ttu-id="beb22-438">N/A</span><span class="sxs-lookup"><span data-stu-id="beb22-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="beb22-439">Usage</span><span class="sxs-lookup"><span data-stu-id="beb22-439">Usage</span></span>  
 <span data-ttu-id="beb22-440">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-440">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="beb22-441">**Sections de la stratégie :** inbound, backend</span><span class="sxs-lookup"><span data-stu-id="beb22-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="beb22-442">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="beb22-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="beb22-443"><a name="RewriteURL"></a> Rewrite URL</span><span class="sxs-lookup"><span data-stu-id="beb22-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="beb22-444">La stratégie `rewrite-uri` convertit une URL de demande de sa forme publique en une forme attendue par le service web, comme le montre l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="beb22-444">The `rewrite-uri` policy converts a request URL from its public form to the form expected by the web service, as shown in the following example.</span></span>  
  
-   <span data-ttu-id="beb22-445">URL publique : `http://api.example.com/storenumber/ordernumber`</span><span class="sxs-lookup"><span data-stu-id="beb22-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="beb22-446">URL de la demande : `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span><span class="sxs-lookup"><span data-stu-id="beb22-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="beb22-447">Cette stratégie peut être utilisée lorsqu’une URL compréhensible par un humain et/ou un navigateur doit être transformée au format d’URL attendu par le service web.</span><span class="sxs-lookup"><span data-stu-id="beb22-447">This policy can be used when a human and/or browser-friendly URL should be transformed into the URL format expected by the web service.</span></span> <span data-ttu-id="beb22-448">Cette stratégie ne doit être appliquée qu’en cas d’exposition d’un autre format d’URL, comme les URL propres, les URL RESTful, les URL conviviales ou les URL adaptées au SEO qui sont des URL purement structurelles ne contenant pas de chaîne de requête et ne contenant que le chemin d’accès de la ressource (après le schéma et l’autorité).</span><span class="sxs-lookup"><span data-stu-id="beb22-448">This policy only needs to be applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only the path of the resource (after the scheme and the authority).</span></span> <span data-ttu-id="beb22-449">C'est souvent le cas pour des raisons d'esthétique, de simplicité d'utilisation ou bien pour l'optimisation des résultats de recherche (SEO).</span><span class="sxs-lookup"><span data-stu-id="beb22-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="beb22-450">Vous ne pouvez ajouter que des paramètres de chaîne de requête avec la stratégie.</span><span class="sxs-lookup"><span data-stu-id="beb22-450">You can only add query string parameters using the policy.</span></span> <span data-ttu-id="beb22-451">Vous ne pouvez pas ajouter de paramètres de chemin d’accès de modèle dans l’URL de réécriture.</span><span class="sxs-lookup"><span data-stu-id="beb22-451">You cannot add extra template path parameters in the rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="beb22-452">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="beb22-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="beb22-453">Exemple</span><span class="sxs-lookup"><span data-stu-id="beb22-453">Example</span></span>  
  
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
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

### <a name="elements"></a><span data-ttu-id="beb22-454">Éléments</span><span class="sxs-lookup"><span data-stu-id="beb22-454">Elements</span></span>  
  
|<span data-ttu-id="beb22-455">Nom</span><span class="sxs-lookup"><span data-stu-id="beb22-455">Name</span></span>|<span data-ttu-id="beb22-456">Description</span><span class="sxs-lookup"><span data-stu-id="beb22-456">Description</span></span>|<span data-ttu-id="beb22-457">Requis</span><span class="sxs-lookup"><span data-stu-id="beb22-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="beb22-458">rewrite-uri</span><span class="sxs-lookup"><span data-stu-id="beb22-458">rewrite-uri</span></span>|<span data-ttu-id="beb22-459">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="beb22-459">Root element.</span></span>|<span data-ttu-id="beb22-460">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="beb22-461">Attributs</span><span class="sxs-lookup"><span data-stu-id="beb22-461">Attributes</span></span>  
  
|<span data-ttu-id="beb22-462">Attribut</span><span class="sxs-lookup"><span data-stu-id="beb22-462">Attribute</span></span>|<span data-ttu-id="beb22-463">Description</span><span class="sxs-lookup"><span data-stu-id="beb22-463">Description</span></span>|<span data-ttu-id="beb22-464">Requis</span><span class="sxs-lookup"><span data-stu-id="beb22-464">Required</span></span>|<span data-ttu-id="beb22-465">Default</span><span class="sxs-lookup"><span data-stu-id="beb22-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="beb22-466">template</span><span class="sxs-lookup"><span data-stu-id="beb22-466">template</span></span>|<span data-ttu-id="beb22-467">URL de service web réelle avec les paramètres de chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="beb22-467">The actual web service URL with any query string parameters.</span></span> <span data-ttu-id="beb22-468">Lorsque vous utilisez des expressions, la valeur entière doit être une expression.</span><span class="sxs-lookup"><span data-stu-id="beb22-468">When using expressions, the whole value must be an expression.</span></span>|<span data-ttu-id="beb22-469">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-469">Yes</span></span>|<span data-ttu-id="beb22-470">N/A</span><span class="sxs-lookup"><span data-stu-id="beb22-470">N/A</span></span>|  
|<span data-ttu-id="beb22-471">copy-unmatched-params</span><span class="sxs-lookup"><span data-stu-id="beb22-471">copy-unmatched-params</span></span>|<span data-ttu-id="beb22-472">Spécifie si les paramètres de requête dans la requête entrante non présents dans le modèle d’URL d’origine sont ajoutés à l’URL définie par le modèle de réécriture</span><span class="sxs-lookup"><span data-stu-id="beb22-472">Specifies whether query parameters in the incoming request not present in the original URL template are added to the URL defined by the re-write template</span></span>|<span data-ttu-id="beb22-473">Non</span><span class="sxs-lookup"><span data-stu-id="beb22-473">No</span></span>|<span data-ttu-id="beb22-474">true</span><span class="sxs-lookup"><span data-stu-id="beb22-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="beb22-475">Usage</span><span class="sxs-lookup"><span data-stu-id="beb22-475">Usage</span></span>  
 <span data-ttu-id="beb22-476">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-476">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="beb22-477">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="beb22-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="beb22-478">**Étendues de la stratégie :** product, API, operation</span><span class="sxs-lookup"><span data-stu-id="beb22-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="beb22-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span><span class="sxs-lookup"><span data-stu-id="beb22-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="beb22-480">La stratégie `Transform XML using an XSLT` applique une transformation de XSL en XML dans le corps de la réponse ou de la demande.</span><span class="sxs-lookup"><span data-stu-id="beb22-480">The `Transform XML using an XSLT` policy applies an XSL transformation to XML in the request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="beb22-481">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="beb22-481">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="beb22-482">Exemple</span><span class="sxs-lookup"><span data-stu-id="beb22-482">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="beb22-483">Éléments</span><span class="sxs-lookup"><span data-stu-id="beb22-483">Elements</span></span>  
  
|<span data-ttu-id="beb22-484">Nom</span><span class="sxs-lookup"><span data-stu-id="beb22-484">Name</span></span>|<span data-ttu-id="beb22-485">Description</span><span class="sxs-lookup"><span data-stu-id="beb22-485">Description</span></span>|<span data-ttu-id="beb22-486">Requis</span><span class="sxs-lookup"><span data-stu-id="beb22-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="beb22-487">xsl-transform</span><span class="sxs-lookup"><span data-stu-id="beb22-487">xsl-transform</span></span>|<span data-ttu-id="beb22-488">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="beb22-488">Root element.</span></span>|<span data-ttu-id="beb22-489">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-489">Yes</span></span>|  
|<span data-ttu-id="beb22-490">paramètre</span><span class="sxs-lookup"><span data-stu-id="beb22-490">parameter</span></span>|<span data-ttu-id="beb22-491">Permet de définir des variables utilisées dans la transformation</span><span class="sxs-lookup"><span data-stu-id="beb22-491">Used to define variables used in the transform</span></span>|<span data-ttu-id="beb22-492">Non</span><span class="sxs-lookup"><span data-stu-id="beb22-492">No</span></span>|  
|<span data-ttu-id="beb22-493">xsl:stylesheet</span><span class="sxs-lookup"><span data-stu-id="beb22-493">xsl:stylesheet</span></span>|<span data-ttu-id="beb22-494">Élément feuille de style racine.</span><span class="sxs-lookup"><span data-stu-id="beb22-494">Root stylesheet element.</span></span> <span data-ttu-id="beb22-495">Tous les éléments et attributs définis à l’intérieur respectent la [Spécification XSLT](http://www.w3.org/TR/xslt) standard.</span><span class="sxs-lookup"><span data-stu-id="beb22-495">All elements and attributes defined within follow the standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="beb22-496">Oui</span><span class="sxs-lookup"><span data-stu-id="beb22-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="beb22-497">Usage</span><span class="sxs-lookup"><span data-stu-id="beb22-497">Usage</span></span>  
 <span data-ttu-id="beb22-498">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="beb22-498">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="beb22-499">**Sections de la stratégie :** inbound, outbound</span><span class="sxs-lookup"><span data-stu-id="beb22-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="beb22-500">**Étendues de la stratégie :** global, product, API, operation</span><span class="sxs-lookup"><span data-stu-id="beb22-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="beb22-501">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="beb22-501">Next steps</span></span>
<span data-ttu-id="beb22-502">Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="beb22-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
