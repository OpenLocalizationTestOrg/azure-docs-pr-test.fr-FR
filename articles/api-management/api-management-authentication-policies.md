---
title: "stratégies d’authentification de gestion des API aaaAzure | Documents Microsoft"
description: "En savoir plus sur les stratégies d’authentification disponibles pour une utilisation dans la gestion des API Azure hello."
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
ms.openlocfilehash: ce93cced66cb67520e97c7c15f3685bffb08e1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="e53ef-103">Stratégies d’authentification dans Gestion des API</span><span class="sxs-lookup"><span data-stu-id="e53ef-103">API Management authentication policies</span></span>
<span data-ttu-id="e53ef-104">Cette rubrique fournit une référence pour hello suivant des stratégies de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="e53ef-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="e53ef-105">Pour plus d'informations sur l'ajout et la configuration des stratégies, consultez la page [Stratégies dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="e53ef-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="e53ef-106"><a name="AuthenticationPolicies"></a> Stratégies d’authentification</span><span class="sxs-lookup"><span data-stu-id="e53ef-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="e53ef-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) : authentification avec un service principal à l’aide de l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="e53ef-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="e53ef-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) : authentification avec un service principal à l’aide de certificats clients.</span><span class="sxs-lookup"><span data-stu-id="e53ef-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="e53ef-109"><a name="Basic"></a> Authenticate with Basic</span><span class="sxs-lookup"><span data-stu-id="e53ef-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="e53ef-110">Hello d’utilisation `authentication-basic` tooauthenticate de stratégie avec un service principal à l’aide de l’authentification de base.</span><span class="sxs-lookup"><span data-stu-id="e53ef-110">Use hello `authentication-basic` policy tooauthenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="e53ef-111">Cette stratégie définit efficacement hello d’autorisation HTTP en-tête toohello valeur correspondante toohello informations d’identification fournies dans la stratégie de hello.</span><span class="sxs-lookup"><span data-stu-id="e53ef-111">This policy effectively sets hello HTTP Authorization header toohello value corresponding toohello credentials provided in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e53ef-112">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="e53ef-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="e53ef-113">Exemple</span><span class="sxs-lookup"><span data-stu-id="e53ef-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="e53ef-114">Éléments</span><span class="sxs-lookup"><span data-stu-id="e53ef-114">Elements</span></span>  
  
|<span data-ttu-id="e53ef-115">Nom</span><span class="sxs-lookup"><span data-stu-id="e53ef-115">Name</span></span>|<span data-ttu-id="e53ef-116">Description</span><span class="sxs-lookup"><span data-stu-id="e53ef-116">Description</span></span>|<span data-ttu-id="e53ef-117">Requis</span><span class="sxs-lookup"><span data-stu-id="e53ef-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e53ef-118">authentification-basic</span><span class="sxs-lookup"><span data-stu-id="e53ef-118">authentication-basic</span></span>|<span data-ttu-id="e53ef-119">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="e53ef-119">Root element.</span></span>|<span data-ttu-id="e53ef-120">Oui</span><span class="sxs-lookup"><span data-stu-id="e53ef-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e53ef-121">Attributs</span><span class="sxs-lookup"><span data-stu-id="e53ef-121">Attributes</span></span>  
  
|<span data-ttu-id="e53ef-122">Nom</span><span class="sxs-lookup"><span data-stu-id="e53ef-122">Name</span></span>|<span data-ttu-id="e53ef-123">Description</span><span class="sxs-lookup"><span data-stu-id="e53ef-123">Description</span></span>|<span data-ttu-id="e53ef-124">Requis</span><span class="sxs-lookup"><span data-stu-id="e53ef-124">Required</span></span>|<span data-ttu-id="e53ef-125">Default</span><span class="sxs-lookup"><span data-stu-id="e53ef-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e53ef-126">username</span><span class="sxs-lookup"><span data-stu-id="e53ef-126">username</span></span>|<span data-ttu-id="e53ef-127">Spécifie le nom d’utilisateur hello des informations d’identification de base hello.</span><span class="sxs-lookup"><span data-stu-id="e53ef-127">Specifies hello username of hello Basic credential.</span></span>|<span data-ttu-id="e53ef-128">Oui</span><span class="sxs-lookup"><span data-stu-id="e53ef-128">Yes</span></span>|<span data-ttu-id="e53ef-129">N/A</span><span class="sxs-lookup"><span data-stu-id="e53ef-129">N/A</span></span>|  
|<span data-ttu-id="e53ef-130">password</span><span class="sxs-lookup"><span data-stu-id="e53ef-130">password</span></span>|<span data-ttu-id="e53ef-131">Spécifie le mot de passe hello des informations d’identification de base hello.</span><span class="sxs-lookup"><span data-stu-id="e53ef-131">Specifies hello password of hello Basic credential.</span></span>|<span data-ttu-id="e53ef-132">Oui</span><span class="sxs-lookup"><span data-stu-id="e53ef-132">Yes</span></span>|<span data-ttu-id="e53ef-133">N/A</span><span class="sxs-lookup"><span data-stu-id="e53ef-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e53ef-134">Usage</span><span class="sxs-lookup"><span data-stu-id="e53ef-134">Usage</span></span>  
 <span data-ttu-id="e53ef-135">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e53ef-135">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e53ef-136">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="e53ef-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e53ef-137">**Étendues de la stratégie :** API</span><span class="sxs-lookup"><span data-stu-id="e53ef-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="e53ef-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span><span class="sxs-lookup"><span data-stu-id="e53ef-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="e53ef-139">Hello d’utilisation `authentication-certificate` tooauthenticate de stratégie avec un service principal à l’aide du certificat client.</span><span class="sxs-lookup"><span data-stu-id="e53ef-139">Use hello `authentication-certificate` policy tooauthenticate with a backend service using client certificate.</span></span> <span data-ttu-id="e53ef-140">certificat de Hello doit toobe [installé dans Gestion des API](http://go.microsoft.com/fwlink/?LinkID=511599) premier et est identifiée par son empreinte numérique.</span><span class="sxs-lookup"><span data-stu-id="e53ef-140">hello certificate needs toobe [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e53ef-141">Instruction de la stratégie</span><span class="sxs-lookup"><span data-stu-id="e53ef-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="e53ef-142">Exemple</span><span class="sxs-lookup"><span data-stu-id="e53ef-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="e53ef-143">Éléments</span><span class="sxs-lookup"><span data-stu-id="e53ef-143">Elements</span></span>  
  
|<span data-ttu-id="e53ef-144">Nom</span><span class="sxs-lookup"><span data-stu-id="e53ef-144">Name</span></span>|<span data-ttu-id="e53ef-145">Description</span><span class="sxs-lookup"><span data-stu-id="e53ef-145">Description</span></span>|<span data-ttu-id="e53ef-146">Requis</span><span class="sxs-lookup"><span data-stu-id="e53ef-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e53ef-147">authentication-certificate</span><span class="sxs-lookup"><span data-stu-id="e53ef-147">authentication-certificate</span></span>|<span data-ttu-id="e53ef-148">Élément racine.</span><span class="sxs-lookup"><span data-stu-id="e53ef-148">Root element.</span></span>|<span data-ttu-id="e53ef-149">Oui</span><span class="sxs-lookup"><span data-stu-id="e53ef-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e53ef-150">Attributs</span><span class="sxs-lookup"><span data-stu-id="e53ef-150">Attributes</span></span>  
  
|<span data-ttu-id="e53ef-151">Nom</span><span class="sxs-lookup"><span data-stu-id="e53ef-151">Name</span></span>|<span data-ttu-id="e53ef-152">Description</span><span class="sxs-lookup"><span data-stu-id="e53ef-152">Description</span></span>|<span data-ttu-id="e53ef-153">Requis</span><span class="sxs-lookup"><span data-stu-id="e53ef-153">Required</span></span>|<span data-ttu-id="e53ef-154">Default</span><span class="sxs-lookup"><span data-stu-id="e53ef-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e53ef-155">thumbprint</span><span class="sxs-lookup"><span data-stu-id="e53ef-155">thumbprint</span></span>|<span data-ttu-id="e53ef-156">Bonjour à l’empreinte numérique du certificat client hello.</span><span class="sxs-lookup"><span data-stu-id="e53ef-156">hello thumbprint for hello client certificate.</span></span>|<span data-ttu-id="e53ef-157">Oui</span><span class="sxs-lookup"><span data-stu-id="e53ef-157">Yes</span></span>|<span data-ttu-id="e53ef-158">N/A</span><span class="sxs-lookup"><span data-stu-id="e53ef-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e53ef-159">Usage</span><span class="sxs-lookup"><span data-stu-id="e53ef-159">Usage</span></span>  
 <span data-ttu-id="e53ef-160">Cette stratégie peut être utilisée dans hello suivant stratégie [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) et [étendues](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e53ef-160">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e53ef-161">**Sections de la stratégie :** inbound</span><span class="sxs-lookup"><span data-stu-id="e53ef-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e53ef-162">**Étendues de la stratégie :** API</span><span class="sxs-lookup"><span data-stu-id="e53ef-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="e53ef-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e53ef-163">Next steps</span></span>
<span data-ttu-id="e53ef-164">Pour plus d’informations sur l’utilisation des stratégies, consultez la page [Stratégies dans la Gestion des API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="e53ef-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  