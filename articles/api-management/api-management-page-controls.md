---
title: "contrôles de page de gestion des API aaaAzure | Documents Microsoft"
description: "En savoir plus sur les contrôles de page hello disponibles pour une utilisation dans les modèles de portail de développement de gestion des API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="d2b52-103">Contrôles de page Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="d2b52-103">Azure API Management page controls</span></span>
<span data-ttu-id="d2b52-104">Gestion des API Azure fournit hello suivant des contrôles utilisables dans les modèles de portail de développement hello.</span><span class="sxs-lookup"><span data-stu-id="d2b52-104">Azure API Management provides hello following controls for use in hello developer portal templates.</span></span>  
  
 <span data-ttu-id="d2b52-105">toouse un contrôle, placez-le dans emplacement de hello souhaité dans le modèle de portail de développement hello.</span><span class="sxs-lookup"><span data-stu-id="d2b52-105">toouse a control, place it in hello desired location in hello developer portal template.</span></span> <span data-ttu-id="d2b52-106">Certains contrôles, tels que hello [actions de l’application](#app-actions) , possèdent des paramètres, comme indiqué dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="d2b52-106">Some controls, such as hello [app-actions](#app-actions) control, have parameters, as shown in hello following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="d2b52-107">valeurs Hello pour les paramètres de hello sont transmis comme partie du modèle de données hello pour le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="d2b52-107">hello values for hello parameters are passed in as part of hello data model for hello template.</span></span> <span data-ttu-id="d2b52-108">Dans la plupart des cas, vous pouvez simplement Coller dans hello fournis exemple pour chaque contrôle toowork correctement.</span><span class="sxs-lookup"><span data-stu-id="d2b52-108">In most cases, you can simply paste in hello provided example for each control for it toowork correctly.</span></span> <span data-ttu-id="d2b52-109">Pour plus d’informations sur les valeurs de paramètre hello, vous pouvez voir la section de modèle de données hello pour chaque modèle dans lequel un contrôle peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="d2b52-109">For more information on hello parameter values, you can see hello data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="d2b52-110">Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="d2b52-110">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="d2b52-111">Contrôles de page du modèle dans le portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="d2b52-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="d2b52-112">app-actions</span><span class="sxs-lookup"><span data-stu-id="d2b52-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="d2b52-113">basic-signin</span><span class="sxs-lookup"><span data-stu-id="d2b52-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="d2b52-114">paging-control</span><span class="sxs-lookup"><span data-stu-id="d2b52-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="d2b52-115">fournisseurs</span><span class="sxs-lookup"><span data-stu-id="d2b52-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="d2b52-116">search-control</span><span class="sxs-lookup"><span data-stu-id="d2b52-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="d2b52-117">sign-up</span><span class="sxs-lookup"><span data-stu-id="d2b52-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="d2b52-118">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="d2b52-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="d2b52-119">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="d2b52-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="d2b52-120"><a name="app-actions"></a> app-actions</span><span class="sxs-lookup"><span data-stu-id="d2b52-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="d2b52-121">Hello `app-actions` contrôle fournit une interface utilisateur permettant d’interagir avec des applications sur la page de profil utilisateur hello dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="d2b52-121">hello `app-actions` control provides a user interface for interacting with applications on hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="d2b52-122">![contrôle app-actions](./media/api-management-page-controls/APIM-app-actions-control.png "contrôle app-actions APIM")</span><span class="sxs-lookup"><span data-stu-id="d2b52-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="d2b52-123">Usage</span><span class="sxs-lookup"><span data-stu-id="d2b52-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="d2b52-124">parameters</span><span class="sxs-lookup"><span data-stu-id="d2b52-124">Parameters</span></span>  
  
|<span data-ttu-id="d2b52-125">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d2b52-125">Parameter</span></span>|<span data-ttu-id="d2b52-126">Description</span><span class="sxs-lookup"><span data-stu-id="d2b52-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="d2b52-127">appId</span><span class="sxs-lookup"><span data-stu-id="d2b52-127">appId</span></span>|<span data-ttu-id="d2b52-128">id de Hello de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="d2b52-128">hello id of hello application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="d2b52-129">Modèles du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="d2b52-129">Developer portal templates</span></span>  
 <span data-ttu-id="d2b52-130">Hello `app-actions` contrôle peut être utilisé dans hello suivant modèles portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="d2b52-130">hello `app-actions` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="d2b52-131">Applications</span><span class="sxs-lookup"><span data-stu-id="d2b52-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="d2b52-132"><a name="basic-signin"></a> basic-signin</span><span class="sxs-lookup"><span data-stu-id="d2b52-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="d2b52-133">Hello `basic-signin` contrôle fournit un contrôle de page dans le portail des développeurs hello de connexion informations Bonjour de collecte connexion utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2b52-133">hello `basic-signin` control provides a control for collecting user sign in information in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="d2b52-134">![contrôle basic-signin](./media/api-management-page-controls/APIM-basic-signin-control.png "contrôle basic-signin APIM")</span><span class="sxs-lookup"><span data-stu-id="d2b52-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="d2b52-135">Usage</span><span class="sxs-lookup"><span data-stu-id="d2b52-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="d2b52-136">parameters</span><span class="sxs-lookup"><span data-stu-id="d2b52-136">Parameters</span></span>  
 <span data-ttu-id="d2b52-137">Aucune.</span><span class="sxs-lookup"><span data-stu-id="d2b52-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="d2b52-138">Modèles du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="d2b52-138">Developer portal templates</span></span>  
 <span data-ttu-id="d2b52-139">Hello `basic-signin` contrôle peut être utilisé dans hello suivant modèles portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="d2b52-139">hello `basic-signin` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="d2b52-140">Connexion</span><span class="sxs-lookup"><span data-stu-id="d2b52-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="d2b52-141"><a name="paging-control"></a> paging-control</span><span class="sxs-lookup"><span data-stu-id="d2b52-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="d2b52-142">Hello `paging-control` fournit la fonctionnalité de pagination sur développeur pages du portail qui affichent une liste d’éléments.</span><span class="sxs-lookup"><span data-stu-id="d2b52-142">hello `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="d2b52-143">![paging-control](./media/api-management-page-controls/APIM-paging-control.png "paging-control APIM")</span><span class="sxs-lookup"><span data-stu-id="d2b52-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="d2b52-144">Usage</span><span class="sxs-lookup"><span data-stu-id="d2b52-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="d2b52-145">parameters</span><span class="sxs-lookup"><span data-stu-id="d2b52-145">Parameters</span></span>  
 <span data-ttu-id="d2b52-146">Aucune.</span><span class="sxs-lookup"><span data-stu-id="d2b52-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="d2b52-147">Modèles du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="d2b52-147">Developer portal templates</span></span>  
 <span data-ttu-id="d2b52-148">Hello `paging-control` contrôle peut être utilisé dans hello suivant modèles portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="d2b52-148">hello `paging-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="d2b52-149">Liste d’API</span><span class="sxs-lookup"><span data-stu-id="d2b52-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="d2b52-150">Liste des problèmes</span><span class="sxs-lookup"><span data-stu-id="d2b52-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="d2b52-151">Liste de produits</span><span class="sxs-lookup"><span data-stu-id="d2b52-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="d2b52-152"><a name="providers"></a> providers</span><span class="sxs-lookup"><span data-stu-id="d2b52-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="d2b52-153">Hello `providers` contrôle fournit un contrôle pour la sélection des fournisseurs d’authentification dans la page dans le portail des développeurs hello de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="d2b52-153">hello `providers` control provides a control for selection of authentication providers in hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="d2b52-154">![contrôle providers](./media/api-management-page-controls/APIM-providers-control.png "contrôle providers APIM")</span><span class="sxs-lookup"><span data-stu-id="d2b52-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="d2b52-155">Usage</span><span class="sxs-lookup"><span data-stu-id="d2b52-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="d2b52-156">parameters</span><span class="sxs-lookup"><span data-stu-id="d2b52-156">Parameters</span></span>  
 <span data-ttu-id="d2b52-157">Aucune.</span><span class="sxs-lookup"><span data-stu-id="d2b52-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="d2b52-158">Modèles du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="d2b52-158">Developer portal templates</span></span>  
 <span data-ttu-id="d2b52-159">Hello `providers` contrôle peut être utilisé dans hello suivant modèles portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="d2b52-159">hello `providers` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="d2b52-160">Connexion</span><span class="sxs-lookup"><span data-stu-id="d2b52-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="d2b52-161"><a name="search-control"></a> search-control</span><span class="sxs-lookup"><span data-stu-id="d2b52-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="d2b52-162">Hello `search-control` fournit des fonctionnalités de recherche sur développeur pages du portail qui affichent une liste d’éléments.</span><span class="sxs-lookup"><span data-stu-id="d2b52-162">hello `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="d2b52-163">![search-control](./media/api-management-page-controls/APIM-search-control.png "search-control APIM")</span><span class="sxs-lookup"><span data-stu-id="d2b52-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="d2b52-164">Usage</span><span class="sxs-lookup"><span data-stu-id="d2b52-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="d2b52-165">parameters</span><span class="sxs-lookup"><span data-stu-id="d2b52-165">Parameters</span></span>  
 <span data-ttu-id="d2b52-166">Aucune.</span><span class="sxs-lookup"><span data-stu-id="d2b52-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="d2b52-167">Modèles du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="d2b52-167">Developer portal templates</span></span>  
 <span data-ttu-id="d2b52-168">Hello `search-control` contrôle peut être utilisé dans hello suivant modèles portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="d2b52-168">hello `search-control` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="d2b52-169">Liste d’API</span><span class="sxs-lookup"><span data-stu-id="d2b52-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="d2b52-170">Liste de produits</span><span class="sxs-lookup"><span data-stu-id="d2b52-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="d2b52-171"><a name="sign-up"></a> sign-up</span><span class="sxs-lookup"><span data-stu-id="d2b52-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="d2b52-172">Hello `sign-up` contrôle fournit un contrôle pour la collecte des informations de profil utilisateur dans la page dans le portail des développeurs hello d’inscription hello.</span><span class="sxs-lookup"><span data-stu-id="d2b52-172">hello `sign-up` control provides a control for collecting user profile information in hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="d2b52-173">![sign-up](./media/api-management-page-controls/APIM-sign-up-control.png "sign-up APIM")</span><span class="sxs-lookup"><span data-stu-id="d2b52-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="d2b52-174">Usage</span><span class="sxs-lookup"><span data-stu-id="d2b52-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="d2b52-175">parameters</span><span class="sxs-lookup"><span data-stu-id="d2b52-175">Parameters</span></span>  
 <span data-ttu-id="d2b52-176">Aucune.</span><span class="sxs-lookup"><span data-stu-id="d2b52-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="d2b52-177">Modèles du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="d2b52-177">Developer portal templates</span></span>  
 <span data-ttu-id="d2b52-178">Hello `sign-up` contrôle peut être utilisé dans hello suivant modèles portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="d2b52-178">hello `sign-up` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="d2b52-179">Inscription</span><span class="sxs-lookup"><span data-stu-id="d2b52-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="d2b52-180"><a name="subscribe-button"></a> subscribe-button</span><span class="sxs-lookup"><span data-stu-id="d2b52-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="d2b52-181">Hello `subscribe-button` fournit un contrôle pour s’abonner à un produit de tooa utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2b52-181">hello `subscribe-button` provides a control for subscribing a user tooa product.</span></span>  
  
 <span data-ttu-id="d2b52-182">![contrôle subscribe-button](./media/api-management-page-controls/APIM-subscribe-button-control.png "contrôle subscribe-button APIM")</span><span class="sxs-lookup"><span data-stu-id="d2b52-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="d2b52-183">Usage</span><span class="sxs-lookup"><span data-stu-id="d2b52-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="d2b52-184">parameters</span><span class="sxs-lookup"><span data-stu-id="d2b52-184">Parameters</span></span>  
 <span data-ttu-id="d2b52-185">Aucune.</span><span class="sxs-lookup"><span data-stu-id="d2b52-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="d2b52-186">Modèles du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="d2b52-186">Developer portal templates</span></span>  
 <span data-ttu-id="d2b52-187">Hello `subscribe-button` contrôle peut être utilisé dans hello suivant modèles portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="d2b52-187">hello `subscribe-button` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="d2b52-188">Produit</span><span class="sxs-lookup"><span data-stu-id="d2b52-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="d2b52-189"><a name="subscription-cancel"></a> subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="d2b52-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="d2b52-190">Hello `subscription-cancel` contrôle fournit un contrôle pour l’annulation d’un produit de tooa d’abonnement dans la page de profil utilisateur hello dans le portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="d2b52-190">hello `subscription-cancel` control provides a control for cancelling a subscription tooa product in hello user profile page in hello developer portal.</span></span>  
  
 <span data-ttu-id="d2b52-191">![contrôle subscription-cancel](./media/api-management-page-controls/APIM-subscription-cancel-control.png "contrôle subscription-cancel APIM")</span><span class="sxs-lookup"><span data-stu-id="d2b52-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="d2b52-192">Usage</span><span class="sxs-lookup"><span data-stu-id="d2b52-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="d2b52-193">parameters</span><span class="sxs-lookup"><span data-stu-id="d2b52-193">Parameters</span></span>  
  
|<span data-ttu-id="d2b52-194">Paramètre</span><span class="sxs-lookup"><span data-stu-id="d2b52-194">Parameter</span></span>|<span data-ttu-id="d2b52-195">Description</span><span class="sxs-lookup"><span data-stu-id="d2b52-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="d2b52-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="d2b52-196">subscriptionId</span></span>|<span data-ttu-id="d2b52-197">id de Hello de hello abonnement toocancel.</span><span class="sxs-lookup"><span data-stu-id="d2b52-197">hello id of hello subscription toocancel.</span></span>|  
|<span data-ttu-id="d2b52-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="d2b52-198">cancelUrl</span></span>|<span data-ttu-id="d2b52-199">Annuler l’abonnement de Hello URL.</span><span class="sxs-lookup"><span data-stu-id="d2b52-199">hello subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="d2b52-200">Modèles du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="d2b52-200">Developer portal templates</span></span>  
 <span data-ttu-id="d2b52-201">Hello `subscription-cancel` contrôle peut être utilisé dans hello suivant modèles portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="d2b52-201">hello `subscription-cancel` control may be used in hello following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="d2b52-202">Produit</span><span class="sxs-lookup"><span data-stu-id="d2b52-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="d2b52-203">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d2b52-203">Next steps</span></span>
<span data-ttu-id="d2b52-204">Pour plus d’informations sur l’utilisation des modèles, consultez [comment toocustomize hello portail des développeurs gestion des API à l’aide de modèles](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d2b52-204">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
