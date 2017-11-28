---
title: "Contrôles de page Gestion des API Azure | Microsoft Docs"
description: "Découvrez les contrôles de page disponibles pour une utilisation dans les modèles du portail des développeurs dans Gestion des API Azure."
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
ms.openlocfilehash: 1ce0657aebe34d093ae94281de208c929067742a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-page-controls"></a><span data-ttu-id="79cf8-103">Contrôles de page Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="79cf8-103">Azure API Management page controls</span></span>
<span data-ttu-id="79cf8-104">Gestion des API Azure fournit les contrôles suivants à utiliser dans les modèles du portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="79cf8-104">Azure API Management provides the following controls for use in the developer portal templates.</span></span>  
  
 <span data-ttu-id="79cf8-105">Pour utiliser un contrôle, placez-le à l’emplacement souhaité dans le modèle du portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="79cf8-105">To use a control, place it in the desired location in the developer portal template.</span></span> <span data-ttu-id="79cf8-106">Certains contrôles, tels que [app-actions](#app-actions), ont des paramètres, comme illustré dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="79cf8-106">Some controls, such as the [app-actions](#app-actions) control, have parameters, as shown in the following example.</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 <span data-ttu-id="79cf8-107">Les valeurs des paramètres sont transmises comme partie du modèle de données pour le modèle.</span><span class="sxs-lookup"><span data-stu-id="79cf8-107">The values for the parameters are passed in as part of the data model for the template.</span></span> <span data-ttu-id="79cf8-108">Dans la plupart des cas, vous pouvez simplement coller l’exemple fourni pour chaque contrôle afin qu’il fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="79cf8-108">In most cases, you can simply paste in the provided example for each control for it to work correctly.</span></span> <span data-ttu-id="79cf8-109">Pour plus d’informations sur les valeurs de paramètre, vous pouvez voir la section de modèle de données pour chaque modèle dans lequel un contrôle peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="79cf8-109">For more information on the parameter values, you can see the data model section for each template in which a control may be used.</span></span>  
  
 <span data-ttu-id="79cf8-110">Pour plus d’informations sur l’utilisation de modèles, consultez [Comment personnaliser le portail des développeurs Gestion des API Azure à l’aide de modèles](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="79cf8-110">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
## <a name="developer-portal-template-page-controls"></a><span data-ttu-id="79cf8-111">Contrôles de page du modèle dans le portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="79cf8-111">Developer portal template page controls</span></span>  
  
-   [<span data-ttu-id="79cf8-112">app-actions</span><span class="sxs-lookup"><span data-stu-id="79cf8-112">app-actions</span></span>](#app-actions)  
  
-   [<span data-ttu-id="79cf8-113">basic-signin</span><span class="sxs-lookup"><span data-stu-id="79cf8-113">basic-signin</span></span>](#basic-signin)  
  
-   [<span data-ttu-id="79cf8-114">paging-control</span><span class="sxs-lookup"><span data-stu-id="79cf8-114">paging-control</span></span>](#paging-control)  
  
-   [<span data-ttu-id="79cf8-115">fournisseurs</span><span class="sxs-lookup"><span data-stu-id="79cf8-115">providers</span></span>](#providers)  
  
-   [<span data-ttu-id="79cf8-116">search-control</span><span class="sxs-lookup"><span data-stu-id="79cf8-116">search-control</span></span>](#search-control)  
  
-   [<span data-ttu-id="79cf8-117">sign-up</span><span class="sxs-lookup"><span data-stu-id="79cf8-117">sign-up</span></span>](#sign-up)  
  
-   [<span data-ttu-id="79cf8-118">subscribe-button</span><span class="sxs-lookup"><span data-stu-id="79cf8-118">subscribe-button</span></span>](#subscribe-button)  
  
-   [<span data-ttu-id="79cf8-119">subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="79cf8-119">subscription-cancel</span></span>](#subscription-cancel)  
  
##  <span data-ttu-id="79cf8-120"><a name="app-actions"></a> app-actions</span><span class="sxs-lookup"><span data-stu-id="79cf8-120"><a name="app-actions"></a> app-actions</span></span>  
 <span data-ttu-id="79cf8-121">Le contrôle `app-actions` fournit une interface utilisateur pour interagir avec les applications sur la page de profil utilisateur dans le portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="79cf8-121">The `app-actions` control provides a user interface for interacting with applications on the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="79cf8-122">![contrôle app-actions](./media/api-management-page-controls/APIM-app-actions-control.png "contrôle app-actions APIM")</span><span class="sxs-lookup"><span data-stu-id="79cf8-122">![app&#45;actions control](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="79cf8-123">Usage</span><span class="sxs-lookup"><span data-stu-id="79cf8-123">Usage</span></span>  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a><span data-ttu-id="79cf8-124">parameters</span><span class="sxs-lookup"><span data-stu-id="79cf8-124">Parameters</span></span>  
  
|<span data-ttu-id="79cf8-125">Paramètre</span><span class="sxs-lookup"><span data-stu-id="79cf8-125">Parameter</span></span>|<span data-ttu-id="79cf8-126">Description</span><span class="sxs-lookup"><span data-stu-id="79cf8-126">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="79cf8-127">appId</span><span class="sxs-lookup"><span data-stu-id="79cf8-127">appId</span></span>|<span data-ttu-id="79cf8-128">ID de l’application.</span><span class="sxs-lookup"><span data-stu-id="79cf8-128">The id of the application.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="79cf8-129">Modèles du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="79cf8-129">Developer portal templates</span></span>  
 <span data-ttu-id="79cf8-130">Le contrôle `app-actions` peut être utilisé dans les modèles suivants du portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="79cf8-130">The `app-actions` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="79cf8-131">Applications</span><span class="sxs-lookup"><span data-stu-id="79cf8-131">Applications</span></span>](api-management-user-profile-templates.md#Applications)  
  
##  <span data-ttu-id="79cf8-132"><a name="basic-signin"></a> basic-signin</span><span class="sxs-lookup"><span data-stu-id="79cf8-132"><a name="basic-signin"></a> basic-signin</span></span>  
 <span data-ttu-id="79cf8-133">Le contrôle `basic-signin` fournit un contrôle pour la collecte des informations de connexion utilisateur dans la page de connexion du portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="79cf8-133">The `basic-signin` control provides a control for collecting user sign in information in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="79cf8-134">![contrôle basic-signin](./media/api-management-page-controls/APIM-basic-signin-control.png "contrôle basic-signin APIM")</span><span class="sxs-lookup"><span data-stu-id="79cf8-134">![basic&#45;signin control](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="79cf8-135">Usage</span><span class="sxs-lookup"><span data-stu-id="79cf8-135">Usage</span></span>  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a><span data-ttu-id="79cf8-136">parameters</span><span class="sxs-lookup"><span data-stu-id="79cf8-136">Parameters</span></span>  
 <span data-ttu-id="79cf8-137">Aucune.</span><span class="sxs-lookup"><span data-stu-id="79cf8-137">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="79cf8-138">Modèles du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="79cf8-138">Developer portal templates</span></span>  
 <span data-ttu-id="79cf8-139">Le contrôle `basic-signin` peut être utilisé dans les modèles suivants du portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="79cf8-139">The `basic-signin` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="79cf8-140">Connexion</span><span class="sxs-lookup"><span data-stu-id="79cf8-140">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="79cf8-141"><a name="paging-control"></a> paging-control</span><span class="sxs-lookup"><span data-stu-id="79cf8-141"><a name="paging-control"></a> paging-control</span></span>  
 <span data-ttu-id="79cf8-142">Le contrôle `paging-control` fournit des fonctionnalités de pagination sur les pages du portail des développeurs qui affichent une liste d’éléments.</span><span class="sxs-lookup"><span data-stu-id="79cf8-142">The `paging-control` provides paging functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="79cf8-143">![paging-control](./media/api-management-page-controls/APIM-paging-control.png "paging-control APIM")</span><span class="sxs-lookup"><span data-stu-id="79cf8-143">![paging control](./media/api-management-page-controls/APIM-paging-control.png "APIM paging control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="79cf8-144">Usage</span><span class="sxs-lookup"><span data-stu-id="79cf8-144">Usage</span></span>  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="79cf8-145">parameters</span><span class="sxs-lookup"><span data-stu-id="79cf8-145">Parameters</span></span>  
 <span data-ttu-id="79cf8-146">Aucune.</span><span class="sxs-lookup"><span data-stu-id="79cf8-146">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="79cf8-147">Modèles du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="79cf8-147">Developer portal templates</span></span>  
 <span data-ttu-id="79cf8-148">Le contrôle `paging-control` peut être utilisé dans les modèles suivants du portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="79cf8-148">The `paging-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="79cf8-149">Liste d’API</span><span class="sxs-lookup"><span data-stu-id="79cf8-149">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="79cf8-150">Liste des problèmes</span><span class="sxs-lookup"><span data-stu-id="79cf8-150">Issue list</span></span>](api-management-issue-templates.md#IssueList)  
  
-   [<span data-ttu-id="79cf8-151">Liste de produits</span><span class="sxs-lookup"><span data-stu-id="79cf8-151">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="79cf8-152"><a name="providers"></a> providers</span><span class="sxs-lookup"><span data-stu-id="79cf8-152"><a name="providers"></a> providers</span></span>  
 <span data-ttu-id="79cf8-153">Le contrôle `providers` fournit un contrôle pour la sélection des fournisseurs d’authentification sur la page de connexion du portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="79cf8-153">The `providers` control provides a control for selection of authentication providers in the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="79cf8-154">![contrôle providers](./media/api-management-page-controls/APIM-providers-control.png "contrôle providers APIM")</span><span class="sxs-lookup"><span data-stu-id="79cf8-154">![providers control](./media/api-management-page-controls/APIM-providers-control.png "APIM providers control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="79cf8-155">Usage</span><span class="sxs-lookup"><span data-stu-id="79cf8-155">Usage</span></span>  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a><span data-ttu-id="79cf8-156">parameters</span><span class="sxs-lookup"><span data-stu-id="79cf8-156">Parameters</span></span>  
 <span data-ttu-id="79cf8-157">Aucune.</span><span class="sxs-lookup"><span data-stu-id="79cf8-157">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="79cf8-158">Modèles du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="79cf8-158">Developer portal templates</span></span>  
 <span data-ttu-id="79cf8-159">Le contrôle `providers` peut être utilisé dans les modèles suivants du portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="79cf8-159">The `providers` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="79cf8-160">Connexion</span><span class="sxs-lookup"><span data-stu-id="79cf8-160">Sign in</span></span>](api-management-page-templates.md#SignIn)  
  
##  <span data-ttu-id="79cf8-161"><a name="search-control"></a> search-control</span><span class="sxs-lookup"><span data-stu-id="79cf8-161"><a name="search-control"></a> search-control</span></span>  
 <span data-ttu-id="79cf8-162">Le contrôle `search-control` fournit des fonctionnalités de recherche sur les pages du portail des développeurs affichant une liste d’éléments.</span><span class="sxs-lookup"><span data-stu-id="79cf8-162">The `search-control` provides search functionality on developer portal pages that display a list of items.</span></span>  
  
 <span data-ttu-id="79cf8-163">![search-control](./media/api-management-page-controls/APIM-search-control.png "search-control APIM")</span><span class="sxs-lookup"><span data-stu-id="79cf8-163">![search control](./media/api-management-page-controls/APIM-search-control.png "APIM search control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="79cf8-164">Usage</span><span class="sxs-lookup"><span data-stu-id="79cf8-164">Usage</span></span>  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a><span data-ttu-id="79cf8-165">parameters</span><span class="sxs-lookup"><span data-stu-id="79cf8-165">Parameters</span></span>  
 <span data-ttu-id="79cf8-166">Aucune.</span><span class="sxs-lookup"><span data-stu-id="79cf8-166">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="79cf8-167">Modèles du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="79cf8-167">Developer portal templates</span></span>  
 <span data-ttu-id="79cf8-168">Le contrôle `search-control` peut être utilisé dans les modèles suivants du portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="79cf8-168">The `search-control` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="79cf8-169">Liste d’API</span><span class="sxs-lookup"><span data-stu-id="79cf8-169">API list</span></span>](api-management-api-templates.md#APIList)  
  
-   [<span data-ttu-id="79cf8-170">Liste de produits</span><span class="sxs-lookup"><span data-stu-id="79cf8-170">Product list</span></span>](api-management-product-templates.md#ProductList)  
  
##  <span data-ttu-id="79cf8-171"><a name="sign-up"></a> sign-up</span><span class="sxs-lookup"><span data-stu-id="79cf8-171"><a name="sign-up"></a> sign-up</span></span>  
 <span data-ttu-id="79cf8-172">Le contrôle `sign-up` fournit un contrôle pour la collecte des informations de profil utilisateur sur la page d’inscription du portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="79cf8-172">The `sign-up` control provides a control for collecting user profile information in the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="79cf8-173">![sign-up](./media/api-management-page-controls/APIM-sign-up-control.png "sign-up APIM")</span><span class="sxs-lookup"><span data-stu-id="79cf8-173">![sign&#45;up control](./media/api-management-page-controls/APIM-sign-up-control.png "APIM sign-up control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="79cf8-174">Usage</span><span class="sxs-lookup"><span data-stu-id="79cf8-174">Usage</span></span>  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a><span data-ttu-id="79cf8-175">parameters</span><span class="sxs-lookup"><span data-stu-id="79cf8-175">Parameters</span></span>  
 <span data-ttu-id="79cf8-176">Aucune.</span><span class="sxs-lookup"><span data-stu-id="79cf8-176">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="79cf8-177">Modèles du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="79cf8-177">Developer portal templates</span></span>  
 <span data-ttu-id="79cf8-178">Le contrôle `sign-up` peut être utilisé dans les modèles suivants du portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="79cf8-178">The `sign-up` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="79cf8-179">Inscription</span><span class="sxs-lookup"><span data-stu-id="79cf8-179">Sign up</span></span>](api-management-page-templates.md#SignUp)  
  
##  <span data-ttu-id="79cf8-180"><a name="subscribe-button"></a> subscribe-button</span><span class="sxs-lookup"><span data-stu-id="79cf8-180"><a name="subscribe-button"></a> subscribe-button</span></span>  
 <span data-ttu-id="79cf8-181">`subscribe-button` fournit un contrôle pour abonner un utilisateur à un produit.</span><span class="sxs-lookup"><span data-stu-id="79cf8-181">The `subscribe-button` provides a control for subscribing a user to a product.</span></span>  
  
 <span data-ttu-id="79cf8-182">![contrôle subscribe-button](./media/api-management-page-controls/APIM-subscribe-button-control.png "contrôle subscribe-button APIM")</span><span class="sxs-lookup"><span data-stu-id="79cf8-182">![subscribe&#45;button control](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="79cf8-183">Usage</span><span class="sxs-lookup"><span data-stu-id="79cf8-183">Usage</span></span>  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a><span data-ttu-id="79cf8-184">parameters</span><span class="sxs-lookup"><span data-stu-id="79cf8-184">Parameters</span></span>  
 <span data-ttu-id="79cf8-185">Aucune.</span><span class="sxs-lookup"><span data-stu-id="79cf8-185">None.</span></span>  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="79cf8-186">Modèles du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="79cf8-186">Developer portal templates</span></span>  
 <span data-ttu-id="79cf8-187">Le contrôle `subscribe-button` peut être utilisé dans les modèles suivants du portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="79cf8-187">The `subscribe-button` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="79cf8-188">Produit</span><span class="sxs-lookup"><span data-stu-id="79cf8-188">Product</span></span>](api-management-product-templates.md#Product)  
  
##  <span data-ttu-id="79cf8-189"><a name="subscription-cancel"></a> subscription-cancel</span><span class="sxs-lookup"><span data-stu-id="79cf8-189"><a name="subscription-cancel"></a> subscription-cancel</span></span>  
 <span data-ttu-id="79cf8-190">Le contrôle `subscription-cancel` fournit un contrôle pour annuler l’abonnement à un produit sur la page de profil utilisateur du portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="79cf8-190">The `subscription-cancel` control provides a control for cancelling a subscription to a product in the user profile page in the developer portal.</span></span>  
  
 <span data-ttu-id="79cf8-191">![contrôle subscription-cancel](./media/api-management-page-controls/APIM-subscription-cancel-control.png "contrôle subscription-cancel APIM")</span><span class="sxs-lookup"><span data-stu-id="79cf8-191">![subscription&#45;cancel control](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel control")</span></span>  
  
### <a name="usage"></a><span data-ttu-id="79cf8-192">Usage</span><span class="sxs-lookup"><span data-stu-id="79cf8-192">Usage</span></span>  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a><span data-ttu-id="79cf8-193">parameters</span><span class="sxs-lookup"><span data-stu-id="79cf8-193">Parameters</span></span>  
  
|<span data-ttu-id="79cf8-194">Paramètre</span><span class="sxs-lookup"><span data-stu-id="79cf8-194">Parameter</span></span>|<span data-ttu-id="79cf8-195">Description</span><span class="sxs-lookup"><span data-stu-id="79cf8-195">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="79cf8-196">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="79cf8-196">subscriptionId</span></span>|<span data-ttu-id="79cf8-197">ID de l’abonnement à annuler.</span><span class="sxs-lookup"><span data-stu-id="79cf8-197">The id of the subscription to cancel.</span></span>|  
|<span data-ttu-id="79cf8-198">cancelUrl</span><span class="sxs-lookup"><span data-stu-id="79cf8-198">cancelUrl</span></span>|<span data-ttu-id="79cf8-199">URL permettant d’annuler l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="79cf8-199">The subscription cancel URL.</span></span>|  
  
### <a name="developer-portal-templates"></a><span data-ttu-id="79cf8-200">Modèles du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="79cf8-200">Developer portal templates</span></span>  
 <span data-ttu-id="79cf8-201">Le contrôle `subscription-cancel` peut être utilisé dans les modèles suivants du portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="79cf8-201">The `subscription-cancel` control may be used in the following developer portal templates.</span></span>  
  
-   [<span data-ttu-id="79cf8-202">Produit</span><span class="sxs-lookup"><span data-stu-id="79cf8-202">Product</span></span>](api-management-product-templates.md#Product)

## <a name="next-steps"></a><span data-ttu-id="79cf8-203">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="79cf8-203">Next steps</span></span>
<span data-ttu-id="79cf8-204">Pour plus d’informations sur l’utilisation de modèles, consultez [Comment personnaliser le portail des développeurs Gestion des API Azure à l’aide de modèles](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="79cf8-204">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>