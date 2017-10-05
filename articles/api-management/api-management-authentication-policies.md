---
title: "Stratégies d’authentification dans Gestion des API Azure | Microsoft Docs"
description: "Découvrez les stratégies d’authentification disponibles dans Gestion des API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 63ef20a56ab7721f9ecc7025d05963cc4b0c27a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="4d986-103">Stratégies d’authentification dans Gestion des API</span><span class="sxs-lookup"><span data-stu-id="4d986-103">API Management authentication policies</span></span>
<span data-ttu-id="4d986-104">Cette rubrique est une ressource de référence au sujet des stratégies Gestion des API suivantes.</span><span class="sxs-lookup"><span data-stu-id="4d986-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="4d986-105">Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="4d986-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="4d986-106"><a name="AuthenticationPolicies"></a> Stratégies d’authentification</span><span class="sxs-lookup"><span data-stu-id="4d986-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="4d986-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) : authentification avec un service principal à l’aide de l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="4d986-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="4d986-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) : authentification avec un service principal à l’aide de certificats clients.</span><span class="sxs-lookup"><span data-stu-id="4d986-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="4d986-109"><a name="Basic"></a> Authenticate with Basic</span><span class="sxs-lookup"><span data-stu-id="4d986-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="4d986-110">La stratégie `authentication-basic` permet l’authentification auprès d’un service principal à l’aide de l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="4d986-110">Use the `authentication-basic` policy to authenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="4d986-111">Cette stratégie définit en réalité l’en-tête d’autorisation HTTP sur la valeur correspondant aux informations d’identification fournies dans la stratégie.</span><span class="sxs-lookup"><span data-stu-id="4d986-111">This policy effectively sets the HTTP Authorization header to the value corresponding to the credentials provided in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="4d986-112">Déclaration de stratégie</span><span class="sxs-lookup"><span data-stu-id="4d986-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="4d986-113">Exemple</span><span class="sxs-lookup"><span data-stu-id="4d986-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="4d986-114">Éléments</span><span class="sxs-lookup"><span data-stu-id="4d986-114">Elements</span></span>  
  
|<span data-ttu-id="4d986-115">Nom</span><span class="sxs-lookup"><span data-stu-id="4d986-115">Name</span></span>|<span data-ttu-id="4d986-116">Description</span><span class="sxs-lookup"><span data-stu-id="4d986-116">Description</span></span>|<span data-ttu-id="4d986-117">Requis</span><span class="sxs-lookup"><span data-stu-id="4d986-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="4d986-118">authentification-basic</span><span class="sxs-lookup"><span data-stu-id="4d986-118">authentication-basic</span></span>|<span data-ttu-id="4d986-119">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="4d986-119">Root element.</span></span>|<span data-ttu-id="4d986-120">Oui</span><span class="sxs-lookup"><span data-stu-id="4d986-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="4d986-121">Attributs</span><span class="sxs-lookup"><span data-stu-id="4d986-121">Attributes</span></span>  
  
|<span data-ttu-id="4d986-122">Nom</span><span class="sxs-lookup"><span data-stu-id="4d986-122">Name</span></span>|<span data-ttu-id="4d986-123">Description</span><span class="sxs-lookup"><span data-stu-id="4d986-123">Description</span></span>|<span data-ttu-id="4d986-124">Requis</span><span class="sxs-lookup"><span data-stu-id="4d986-124">Required</span></span>|<span data-ttu-id="4d986-125">Default</span><span class="sxs-lookup"><span data-stu-id="4d986-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="4d986-126">username</span><span class="sxs-lookup"><span data-stu-id="4d986-126">username</span></span>|<span data-ttu-id="4d986-127">Spécifie le nom d’utilisateur associé aux informations d’identification de base.</span><span class="sxs-lookup"><span data-stu-id="4d986-127">Specifies the username of the Basic credential.</span></span>|<span data-ttu-id="4d986-128">Oui</span><span class="sxs-lookup"><span data-stu-id="4d986-128">Yes</span></span>|<span data-ttu-id="4d986-129">N/A</span><span class="sxs-lookup"><span data-stu-id="4d986-129">N/A</span></span>|  
|<span data-ttu-id="4d986-130">password</span><span class="sxs-lookup"><span data-stu-id="4d986-130">password</span></span>|<span data-ttu-id="4d986-131">Spécifie le mot de passe associé aux informations d’identification de base.</span><span class="sxs-lookup"><span data-stu-id="4d986-131">Specifies the password of the Basic credential.</span></span>|<span data-ttu-id="4d986-132">Oui</span><span class="sxs-lookup"><span data-stu-id="4d986-132">Yes</span></span>|<span data-ttu-id="4d986-133">N/A</span><span class="sxs-lookup"><span data-stu-id="4d986-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="4d986-134">Usage</span><span class="sxs-lookup"><span data-stu-id="4d986-134">Usage</span></span>  
 <span data-ttu-id="4d986-135">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="4d986-135">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="4d986-136">**Sections de la stratégie :** inbound (entrant)</span><span class="sxs-lookup"><span data-stu-id="4d986-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="4d986-137">**Étendues de la stratégie :** API</span><span class="sxs-lookup"><span data-stu-id="4d986-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="4d986-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span><span class="sxs-lookup"><span data-stu-id="4d986-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="4d986-139">La stratégie `authentication-certificate` permet l’authentification auprès d’un service principal à l’aide d’un certificat client.</span><span class="sxs-lookup"><span data-stu-id="4d986-139">Use the `authentication-certificate` policy to authenticate with a backend service using client certificate.</span></span> <span data-ttu-id="4d986-140">Le certificat doit être [installé dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=511599) en premier et identifié par son empreinte.</span><span class="sxs-lookup"><span data-stu-id="4d986-140">The certificate needs to be [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="4d986-141">Déclaration de stratégie</span><span class="sxs-lookup"><span data-stu-id="4d986-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="4d986-142">Exemple</span><span class="sxs-lookup"><span data-stu-id="4d986-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="4d986-143">Éléments</span><span class="sxs-lookup"><span data-stu-id="4d986-143">Elements</span></span>  
  
|<span data-ttu-id="4d986-144">Nom</span><span class="sxs-lookup"><span data-stu-id="4d986-144">Name</span></span>|<span data-ttu-id="4d986-145">Description</span><span class="sxs-lookup"><span data-stu-id="4d986-145">Description</span></span>|<span data-ttu-id="4d986-146">Requis</span><span class="sxs-lookup"><span data-stu-id="4d986-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="4d986-147">authentication-certificate</span><span class="sxs-lookup"><span data-stu-id="4d986-147">authentication-certificate</span></span>|<span data-ttu-id="4d986-148">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="4d986-148">Root element.</span></span>|<span data-ttu-id="4d986-149">Oui</span><span class="sxs-lookup"><span data-stu-id="4d986-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="4d986-150">Attributs</span><span class="sxs-lookup"><span data-stu-id="4d986-150">Attributes</span></span>  
  
|<span data-ttu-id="4d986-151">Nom</span><span class="sxs-lookup"><span data-stu-id="4d986-151">Name</span></span>|<span data-ttu-id="4d986-152">Description</span><span class="sxs-lookup"><span data-stu-id="4d986-152">Description</span></span>|<span data-ttu-id="4d986-153">Requis</span><span class="sxs-lookup"><span data-stu-id="4d986-153">Required</span></span>|<span data-ttu-id="4d986-154">Default</span><span class="sxs-lookup"><span data-stu-id="4d986-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="4d986-155">thumbprint</span><span class="sxs-lookup"><span data-stu-id="4d986-155">thumbprint</span></span>|<span data-ttu-id="4d986-156">Empreinte du certificat client.</span><span class="sxs-lookup"><span data-stu-id="4d986-156">The thumbprint for the client certificate.</span></span>|<span data-ttu-id="4d986-157">Oui</span><span class="sxs-lookup"><span data-stu-id="4d986-157">Yes</span></span>|<span data-ttu-id="4d986-158">N/A</span><span class="sxs-lookup"><span data-stu-id="4d986-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="4d986-159">Usage</span><span class="sxs-lookup"><span data-stu-id="4d986-159">Usage</span></span>  
 <span data-ttu-id="4d986-160">Cette stratégie peut être utilisée dans les [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) de stratégie suivantes.</span><span class="sxs-lookup"><span data-stu-id="4d986-160">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="4d986-161">**Sections de la stratégie :** inbound (entrant)</span><span class="sxs-lookup"><span data-stu-id="4d986-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="4d986-162">**Étendues de la stratégie :** API</span><span class="sxs-lookup"><span data-stu-id="4d986-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="4d986-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4d986-163">Next steps</span></span>
<span data-ttu-id="4d986-164">Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4d986-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  