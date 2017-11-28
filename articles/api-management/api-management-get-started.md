---
title: "Gérer votre première API dans Gestion des API Azure | Microsoft Docs"
description: "Découvrez comment créer des API et ajouter des opérations et comment prendre en main Gestion des API."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 6e76d1ee08f804637999ef2ebf5d25becf6a0408
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="554b0-103">Gérer votre première API dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="554b0-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="554b0-104"><a name="overview"> </a>Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="554b0-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="554b0-105">Ce guide décrit la prise en main rapide de la gestion des API Azure et la création de votre premier appel d’API.</span><span class="sxs-lookup"><span data-stu-id="554b0-105">This guide shows you how to quickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="554b0-106"><a name="concepts"> </a>Qu’est-ce que Gestion des API Azure ?</span><span class="sxs-lookup"><span data-stu-id="554b0-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="554b0-107">Vous pouvez utiliser la gestion des API Azure pour prendre n’importe quel serveur principal et lancer un programme d’API à part entière qui repose sur ce dernier.</span><span class="sxs-lookup"><span data-stu-id="554b0-107">You can use Azure API Management to take any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="554b0-108">Scénarios courants :</span><span class="sxs-lookup"><span data-stu-id="554b0-108">Common scenarios include:</span></span>

* <span data-ttu-id="554b0-109">**Sécurisation d’infrastructures mobiles** par régulation de l’accès à l’aide de clés d’API pour éviter les attaques par déni de service (DOS) en utilisant la limitation ou des stratégies de sécurité avancées, telles que la validation de jeton JWT</span><span class="sxs-lookup"><span data-stu-id="554b0-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="554b0-110">**Activation d’écosystèmes de partenaires ISV** en proposant une intégration rapide des partenaires via le portail des développeurs et la création d’une façade d’API afin de se dissocier des implémentations internes qui ne sont pas appropriées à la consommation des partenaires.</span><span class="sxs-lookup"><span data-stu-id="554b0-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through the developer portal and building an API facade to decouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="554b0-111">**Exécution d’un programme d’API interne** en offrant un emplacement centralisé à l’organisation pour communiquer sur la disponibilité et les dernières modifications apportées aux API, tout en régulant l’accès basé sur des comptes professionnels, tous basés sur un canal sécurisé entre la passerelle de l’API et le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="554b0-111">**Running an internal API program** by offering a centralized location for the organization to communicate about the availability and latest changes to APIs, gating access based on organizational accounts, all based on a secured channel between the API gateway and the backend.</span></span>

<span data-ttu-id="554b0-112">Le système est constitué des composants suivants :</span><span class="sxs-lookup"><span data-stu-id="554b0-112">The system is made up of the following components:</span></span>

* <span data-ttu-id="554b0-113">La **passerelle d’API** est le point de terminaison qui :</span><span class="sxs-lookup"><span data-stu-id="554b0-113">The **API gateway** is the endpoint that:</span></span>
  
  * <span data-ttu-id="554b0-114">accepte les appels d’API et les dirige vers vos serveurs principaux ;</span><span class="sxs-lookup"><span data-stu-id="554b0-114">Accepts API calls and routes them to your backends.</span></span>
  * <span data-ttu-id="554b0-115">vérifie les clés d’API, les jetons JWT, les certificats et les autres informations d’identification ;</span><span class="sxs-lookup"><span data-stu-id="554b0-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="554b0-116">applique des quotas d’utilisation et des limites de débit ;</span><span class="sxs-lookup"><span data-stu-id="554b0-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="554b0-117">transforme votre API à la volée sans modification de code ;</span><span class="sxs-lookup"><span data-stu-id="554b0-117">Transforms your API on the fly without code modifications.</span></span>
  * <span data-ttu-id="554b0-118">met en cache les réponses du serveur principal lorsqu’il est configuré ;</span><span class="sxs-lookup"><span data-stu-id="554b0-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="554b0-119">enregistre les métadonnées relatives aux appels à des fins d’analyse.</span><span class="sxs-lookup"><span data-stu-id="554b0-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="554b0-120">Le **portail des éditeurs** est l’interface d’administration où vous configurez votre programme d’API.</span><span class="sxs-lookup"><span data-stu-id="554b0-120">The **publisher portal** is the administrative interface where you set up your API program.</span></span> <span data-ttu-id="554b0-121">Utilisez-le pour :</span><span class="sxs-lookup"><span data-stu-id="554b0-121">Use it to:</span></span>
  
  * <span data-ttu-id="554b0-122">définir ou importer le schéma d’API ;</span><span class="sxs-lookup"><span data-stu-id="554b0-122">Define or import API schema.</span></span>
  * <span data-ttu-id="554b0-123">intégrer des API aux produits sous forme de packages ;</span><span class="sxs-lookup"><span data-stu-id="554b0-123">Package APIs into products.</span></span>
  * <span data-ttu-id="554b0-124">définir des stratégies, telles que des quotas ou des transformations sur les API ;</span><span class="sxs-lookup"><span data-stu-id="554b0-124">Set up policies like quotas or transformations on the APIs.</span></span>
  * <span data-ttu-id="554b0-125">obtenir des informations issues de l’analyse ;</span><span class="sxs-lookup"><span data-stu-id="554b0-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="554b0-126">gérer les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="554b0-126">Manage users.</span></span>
* <span data-ttu-id="554b0-127">Le **portail des développeurs** est le principal lieu sur le web où les développeurs peuvent :</span><span class="sxs-lookup"><span data-stu-id="554b0-127">The **developer portal** serves as the main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="554b0-128">lire la documentation de l’API ;</span><span class="sxs-lookup"><span data-stu-id="554b0-128">Read API documentation.</span></span>
  * <span data-ttu-id="554b0-129">essayer une API via la console interactive ;</span><span class="sxs-lookup"><span data-stu-id="554b0-129">Try out an API via the interactive console.</span></span>
  * <span data-ttu-id="554b0-130">créer un compte et s’abonner pour obtenir les clés d’une API ;</span><span class="sxs-lookup"><span data-stu-id="554b0-130">Create an account and subscribe to get API keys.</span></span>
  * <span data-ttu-id="554b0-131">accéder aux analyses relatives à leur propre utilisation.</span><span class="sxs-lookup"><span data-stu-id="554b0-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="554b0-132"><a name="create-service-instance"> </a>Création d’une instance du service Gestion des API</span><span class="sxs-lookup"><span data-stu-id="554b0-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="554b0-133">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="554b0-133">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="554b0-134">Si vous ne possédez pas de compte, vous pouvez créer un compte gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="554b0-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="554b0-135">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][Azure Free Trial].</span><span class="sxs-lookup"><span data-stu-id="554b0-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="554b0-136">La première étape de travail avec Gestion des API consiste à créer une instance de service.</span><span class="sxs-lookup"><span data-stu-id="554b0-136">The first step in working with API Management is to create a service instance.</span></span> <span data-ttu-id="554b0-137">Connectez-vous au [Portail Azure][Azure Portal] et cliquez sur **Nouveau**, **Web + mobile**, **Gestion des API**.</span><span class="sxs-lookup"><span data-stu-id="554b0-137">Sign in to the [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![Nouvelle instance Gestion des API][api-management-create-instance-menu]

<span data-ttu-id="554b0-139">Pour le **nom**, spécifiez un nom de sous-domaine unique à utiliser pour l’URL du service.</span><span class="sxs-lookup"><span data-stu-id="554b0-139">For **Name**, specify a unique sub-domain name to use for the service URL.</span></span>

<span data-ttu-id="554b0-140">Choisissez **l’abonnement**, le **groupe de ressources** et **l’emplacement** souhaités pour votre instance de service.</span><span class="sxs-lookup"><span data-stu-id="554b0-140">Choose the desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="554b0-141">Entrez **Contoso Ltd.**</span><span class="sxs-lookup"><span data-stu-id="554b0-141">Enter **Contoso Ltd.**</span></span> <span data-ttu-id="554b0-142">pour le **nom de l’organisation**, ainsi que votre adresse de messagerie dans le champ **Adresse de messagerie de l’administrateur**.</span><span class="sxs-lookup"><span data-stu-id="554b0-142">for the **Organization Name**, and enter your email address in the **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="554b0-143">Cette adresse de messagerie est utilisée pour les notifications provenant du système Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="554b0-143">This email address is used for notifications from the API Management system.</span></span> <span data-ttu-id="554b0-144">Pour plus d’informations, consultez [Configuration des notifications et des modèles de messages électroniques dans Gestion des API Azure][How to configure notifications and email templates in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="554b0-144">For more information, see [How to configure notifications and email templates in Azure API Management][How to configure notifications and email templates in Azure API Management].</span></span>
> 
> 

![Nouveau service Gestion des API][api-management-create-instance-step1]

<span data-ttu-id="554b0-146">Les instances du service Gestion des API sont disponibles dans trois niveaux : Développeur, Standard et Premium.</span><span class="sxs-lookup"><span data-stu-id="554b0-146">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="554b0-147">Le niveau Développeur est réservé aux programmes d’API de développement, de test et pilote pour lesquels la haute disponibilité n’est pas un problème.</span><span class="sxs-lookup"><span data-stu-id="554b0-147">The Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="554b0-148">Aux niveaux Standard et Premium, vous pouvez étendre le nombre d’unités réservées pour gérer davantage de trafic.</span><span class="sxs-lookup"><span data-stu-id="554b0-148">In the Standard and Premium tiers, you can scale your reserved unit count to handle more traffic.</span></span> <span data-ttu-id="554b0-149">Les niveaux Standard et Premium permettent à votre service Gestion des API de disposer de la puissance de traitement et des performances maximales.</span><span class="sxs-lookup"><span data-stu-id="554b0-149">The Standard and Premium tiers provide your API Management service with the most processing power and performance.</span></span> <span data-ttu-id="554b0-150">Vous pouvez effectuer ce didacticiel à l’aide de n’importe quel niveau.</span><span class="sxs-lookup"><span data-stu-id="554b0-150">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="554b0-151">Pour en savoir plus sur les niveaux du service Gestion des API, consultez la page relative à la [tarification du service Gestion des API][API Management pricing].</span><span class="sxs-lookup"><span data-stu-id="554b0-151">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="554b0-152">Cliquez sur **Créer** pour démarrer la configuration de votre instance de service.</span><span class="sxs-lookup"><span data-stu-id="554b0-152">Click **Create** to start provisioning your service instance.</span></span>

![Nouveau service Gestion des API][api-management-instance-created]

<span data-ttu-id="554b0-154">Une fois l’instance de service créée, l’étape suivante consiste à créer ou à importer une API.</span><span class="sxs-lookup"><span data-stu-id="554b0-154">Once the service instance is created, the next step is to create or import an API.</span></span>

## <span data-ttu-id="554b0-155"><a name="create-api"> </a>Importation d’une API</span><span class="sxs-lookup"><span data-stu-id="554b0-155"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="554b0-156">Une API se compose d’un ensemble d’opérations pouvant être appelées à partir d’une application cliente.</span><span class="sxs-lookup"><span data-stu-id="554b0-156">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="554b0-157">Les opérations de l’API sont transmises par proxy aux services web existants.</span><span class="sxs-lookup"><span data-stu-id="554b0-157">API operations are proxied to existing web services.</span></span>

<span data-ttu-id="554b0-158">Il est possible de créer des API (et d’ajouter des opérations) manuellement ou de les importer.</span><span class="sxs-lookup"><span data-stu-id="554b0-158">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="554b0-159">Dans ce didacticiel, nous allons importer l’API pour un exemple de service Web de calculatrice fourni par Microsoft et hébergé sur Azure.</span><span class="sxs-lookup"><span data-stu-id="554b0-159">In this tutorial, we will import the API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="554b0-160">Pour plus d’informations sur la création d’une API et l’ajout manuel d’opérations, consultez les rubriques [Création d’API](api-management-howto-create-apis.md) et [Ajout d’opérations à une API](api-management-howto-add-operations.md).</span><span class="sxs-lookup"><span data-stu-id="554b0-160">For guidance on creating an API and manually adding operations, see [How to create APIs](api-management-howto-create-apis.md) and [How to add operations to an API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="554b0-161">Les API sont configurées à partir du portail des éditeurs.</span><span class="sxs-lookup"><span data-stu-id="554b0-161">APIs are configured from the publisher portal.</span></span> <span data-ttu-id="554b0-162">Pour y accéder, cliquez sur **Portail des éditeurs** à partir de la barre d’outils de services.</span><span class="sxs-lookup"><span data-stu-id="554b0-162">To reach it, click **Publisher portal** from the service toolbar.</span></span>

![Portail des éditeurs][api-management-management-console]

<span data-ttu-id="554b0-164">Pour importer l’API de calculatrice, cliquez sur **API** dans le menu **Gestion des API** à gauche, puis sur **Importer l’API**.</span><span class="sxs-lookup"><span data-stu-id="554b0-164">To import the calculator API, click **APIs** from the **API Management** menu on the left, and then click **Import API**.</span></span>

![Bouton Importer l’API][api-management-import-api]

<span data-ttu-id="554b0-166">Procédez comme suit pour configurer l’API de calculatrice :</span><span class="sxs-lookup"><span data-stu-id="554b0-166">Perform the following steps to configure the calculator API:</span></span>

1. <span data-ttu-id="554b0-167">Cliquez sur **À partir d’une URL**, entrez **http://calcapi.cloudapp.net/calcapi.json** dans la zone de texte **URL du document de spécification**, et cliquez sur la case d’option **Swagger**.</span><span class="sxs-lookup"><span data-stu-id="554b0-167">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into the **Specification document URL** text box, and click the **Swagger** radio button.</span></span>
2. <span data-ttu-id="554b0-168">Entrez **calc** dans la zone de texte **Suffixe de l’URL d’API web**.</span><span class="sxs-lookup"><span data-stu-id="554b0-168">Type **calc** into the **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="554b0-169">Cliquez dans la zone **Produits (facultatif)** et choisissez **Starter**.</span><span class="sxs-lookup"><span data-stu-id="554b0-169">Click in the **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="554b0-170">Cliquez sur **Enregistrer** pour importer l’API.</span><span class="sxs-lookup"><span data-stu-id="554b0-170">Click **Save** to import the API.</span></span>

![Ajouter une nouvelle API][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="554b0-172">**Gestion des API** prend actuellement en charge les versions 1.2 et 2.0 du document Swagger dans le cadre d’une importation.</span><span class="sxs-lookup"><span data-stu-id="554b0-172">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="554b0-173">Même si la [spécification Swagger 2.0](http://swagger.io/specification) indique que les propriétés `host`, `basePath` et `schemes` sont facultatives, votre document Swagger 2.0 **DOIT** contenir ces propriétés ; dans le cas contraire, l’importation échouera.</span><span class="sxs-lookup"><span data-stu-id="554b0-173">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="554b0-174">Une fois l’API importée, la page Résumé de l’API s’affiche dans le portail des éditeurs.</span><span class="sxs-lookup"><span data-stu-id="554b0-174">Once the API is imported, the summary page for the API is displayed in the publisher portal.</span></span>

![Résumé des API][api-management-imported-api-summary]

<span data-ttu-id="554b0-176">La section API comporte plusieurs onglets.</span><span class="sxs-lookup"><span data-stu-id="554b0-176">The API section has several tabs.</span></span> <span data-ttu-id="554b0-177">L’onglet **Résumé** affiche les mesures de base et les informations concernant l’API.</span><span class="sxs-lookup"><span data-stu-id="554b0-177">The **Summary** tab displays basic metrics and information about the API.</span></span> <span data-ttu-id="554b0-178">L’onglet [Paramètres](api-management-howto-create-apis.md#configure-api-settings) permet d’afficher et de modifier la configuration d’une API.</span><span class="sxs-lookup"><span data-stu-id="554b0-178">The [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used to view and edit the configuration for an API.</span></span> <span data-ttu-id="554b0-179">L’onglet [Opérations](api-management-howto-add-operations.md) permet de gérer les opérations de l’API.</span><span class="sxs-lookup"><span data-stu-id="554b0-179">The [Operations](api-management-howto-add-operations.md) tab is used to manage the API's operations.</span></span> <span data-ttu-id="554b0-180">L’onglet **Sécurité** permet de configurer l’authentification de la passerelle pour le serveur principal à l’aide de l’authentification de base ou de [l’authentification mutuelle des certificats](api-management-howto-mutual-certificates.md) et de configurer l’[autorisation de l’utilisateur à l’aide d’OAuth 2.0](api-management-howto-oauth2.md).</span><span class="sxs-lookup"><span data-stu-id="554b0-180">The **Security** tab can be used to configure gateway authentication for the backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and to configure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="554b0-181">L’onglet **Problèmes** est utilisé pour afficher les problèmes signalés par les développeurs qui utilisent votre API.</span><span class="sxs-lookup"><span data-stu-id="554b0-181">The **Issues** tab is used to view issues reported by the developers who are using your APIs.</span></span> <span data-ttu-id="554b0-182">L’onglet **Produits** permet de configurer les produits qui contiennent cette API.</span><span class="sxs-lookup"><span data-stu-id="554b0-182">The **Products** tab is used to configure the products that contain this API.</span></span>

<span data-ttu-id="554b0-183">Par défaut, chaque instance Gestion des API est fournie avec deux exemples de produits :</span><span class="sxs-lookup"><span data-stu-id="554b0-183">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="554b0-184">**Starter**</span><span class="sxs-lookup"><span data-stu-id="554b0-184">**Starter**</span></span>
* <span data-ttu-id="554b0-185">**Illimité**</span><span class="sxs-lookup"><span data-stu-id="554b0-185">**Unlimited**</span></span>

<span data-ttu-id="554b0-186">Dans ce didacticiel, l’API de calculatrice de base a été ajoutée au produit Starter lors de l’importation de l’API.</span><span class="sxs-lookup"><span data-stu-id="554b0-186">In this tutorial, the Basic Calculator API was added to the Starter product when the API was imported.</span></span>

<span data-ttu-id="554b0-187">Pour créer des appels à une API, les développeurs doivent commencer par s’abonner à un produit qui leur permet d’y accéder.</span><span class="sxs-lookup"><span data-stu-id="554b0-187">In order to make calls to an API, developers must first subscribe to a product that gives them access to it.</span></span> <span data-ttu-id="554b0-188">Ils peuvent s’abonner aux produits dans le portail des développeurs,ou les administrateurs peuvent les y abonner dans le portail des éditeurs.</span><span class="sxs-lookup"><span data-stu-id="554b0-188">Developers can subscribe to products in the developer portal, or administrators can subscribe developers to products in the publisher portal.</span></span> <span data-ttu-id="554b0-189">Vous êtes considéré comme un administrateur puisque vous avez créé l’instance Gestion des API lors des étapes précédentes du didacticiel. Vous êtes également abonné à tous les produits par défaut.</span><span class="sxs-lookup"><span data-stu-id="554b0-189">You are an administrator since you created the API Management instance in the previous steps in the tutorial, so you are already subscribed to every product by default.</span></span>

## <span data-ttu-id="554b0-190"><a name="call-operation"> </a>Appel d’une opération à partir du portail des développeurs</span><span class="sxs-lookup"><span data-stu-id="554b0-190"><a name="call-operation"> </a>Call an operation from the developer portal</span></span>
<span data-ttu-id="554b0-191">Les opérations peuvent être directement appelées depuis le portail des développeurs, qui permet d’afficher et de tester les opérations d’une API.</span><span class="sxs-lookup"><span data-stu-id="554b0-191">Operations can be called directly from the developer portal, which provides a convenient way to view and test the operations of an API.</span></span> <span data-ttu-id="554b0-192">Dans cette étape du didacticiel, vous appellerez l’opération **Ajouter deux entiers** de l’API de calculatrice de base.</span><span class="sxs-lookup"><span data-stu-id="554b0-192">In this tutorial step, you will call the Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="554b0-193">Cliquez sur **Portail des développeurs** dans le menu en haut à droite du portail des éditeurs.</span><span class="sxs-lookup"><span data-stu-id="554b0-193">Click **Developer portal** from the menu at the top right of the publisher portal.</span></span>

![Portail des développeurs][api-management-developer-portal-menu]

<span data-ttu-id="554b0-195">Cliquez sur **API** dans le menu supérieur, puis sur **Calculatrice de base** pour afficher les opérations disponibles.</span><span class="sxs-lookup"><span data-stu-id="554b0-195">Click **APIs** from the top menu, and then click **Basic Calculator** to see the available operations.</span></span>

![Portail des développeurs][api-management-developer-portal-calc-api]

<span data-ttu-id="554b0-197">Vous remarquerez les exemples de descriptions et de paramètres importés avec l’API et les opérations, qui fournissent de la documentation aux développeurs qui utiliseront cette opération.</span><span class="sxs-lookup"><span data-stu-id="554b0-197">Note the sample descriptions and parameters that were imported along with the API and operations, providing documentation for the developers that will use this operation.</span></span> <span data-ttu-id="554b0-198">Ces descriptions peuvent également être ajoutées lorsque des opérations sont ajoutées manuellement.</span><span class="sxs-lookup"><span data-stu-id="554b0-198">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="554b0-199">Pour appeler l’opération **Ajouter deux entiers**, cliquez sur **Essayer**.</span><span class="sxs-lookup"><span data-stu-id="554b0-199">To call the **Add two integers** operation, click **Try it**.</span></span>

![Essayer][api-management-developer-portal-calc-api-console]

<span data-ttu-id="554b0-201">Vous pouvez entrer des valeurs pour les paramètres ou conserver les valeurs par défaut, puis cliquer sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="554b0-201">You can enter some values for the parameters or keep the defaults, and then click **Send**.</span></span>

![HTTP Get][api-management-invoke-get]

<span data-ttu-id="554b0-203">Après l’appel d’une opération, le portail des développeurs affiche le **statut de réponse**, les **en-têtes de réponse**, et tout **contenu de la réponse**.</span><span class="sxs-lookup"><span data-stu-id="554b0-203">After an operation is invoked, the developer portal displays the **Response status**, the **Response headers**, and any **Response content**.</span></span>

![Réponse][api-management-invoke-get-response]

## <span data-ttu-id="554b0-205"><a name="view-analytics"> </a>Affichage des analyses</span><span class="sxs-lookup"><span data-stu-id="554b0-205"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="554b0-206">Pour afficher les analyses relatives à Calculatrice de base, revenez au portail des éditeurs en sélectionnant **Gérer** dans le menu en haut à droite du portail des développeurs.</span><span class="sxs-lookup"><span data-stu-id="554b0-206">To view analytics for Basic Calculator, switch back to the publisher portal by selecting **Manage** from the menu at the top right of the developer portal.</span></span>

![Gérer][api-management-manage-menu]

<span data-ttu-id="554b0-208">La vue par défaut du portail des éditeurs correspond au **tableau de bord**, lequel offre un aperçu de votre instance Gestion des API.</span><span class="sxs-lookup"><span data-stu-id="554b0-208">The default view for the publisher portal is the **Dashboard**, which provides an overview of your API Management instance.</span></span>

![tableau de bord][api-management-dashboard]

<span data-ttu-id="554b0-210">Passez la souris sur le graphique relatif à **Calculatrice de base** pour afficher les mesures spécifiques de l’utilisation de l’API à une période donnée.</span><span class="sxs-lookup"><span data-stu-id="554b0-210">Hover the mouse over the chart for **Basic Calculator** to see the specific metrics for the usage of the API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="554b0-211">Si vous ne voyez aucune ligne sur votre graphique, revenez au portail des développeurs et créez des appels dans l’API, patientez et revenez au tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="554b0-211">If you don't see any lines on your chart, switch back to the developer portal and make some calls into the API, wait a few moments, and then come back to the dashboard.</span></span>
> 
> 

<span data-ttu-id="554b0-212">Cliquez sur **Afficher les détails** pour afficher la page Résumé de l’API, incluant une version plus importante des mesures affichées.</span><span class="sxs-lookup"><span data-stu-id="554b0-212">Click **View Details** to view the summary page for the API, including a larger version of the displayed metrics.</span></span>

![Analyse][api-management-mouse-over]

![Résumé][api-management-api-summary-metrics]

<span data-ttu-id="554b0-215">Pour des mesures et des rapports détaillés, cliquez sur **Analyse** dans le menu **Gestion des API** à gauche.</span><span class="sxs-lookup"><span data-stu-id="554b0-215">For detailed metrics and reports, click **Analytics** from the **API Management** menu on the left.</span></span>

![Vue d’ensemble][api-management-analytics-overview]

<span data-ttu-id="554b0-217">La section **Analyse** comporte les quatre onglets suivants :</span><span class="sxs-lookup"><span data-stu-id="554b0-217">The **Analytics** section has the following four tabs:</span></span>

* <span data-ttu-id="554b0-218">**Aperçu rapide** présente l’utilisation générale et les mesures d’intégrité ainsi que les produits, les API, les opérations et les développeurs principaux.</span><span class="sxs-lookup"><span data-stu-id="554b0-218">**At a glance** provides overall usage and health metrics, as well as the top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="554b0-219">**Utilisation** fournit une présentation détaillée des appels d’API et de la bande passante, y compris une représentation géographique.</span><span class="sxs-lookup"><span data-stu-id="554b0-219">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="554b0-220">**Intégrité** se concentre sur les codes d'état, les taux de réussite en cache, les temps de réponse et les temps de réponse d'API et de service.</span><span class="sxs-lookup"><span data-stu-id="554b0-220">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="554b0-221">**Activité** fournit des rapports qui présentent une analyse des activités spécifiques par développeur, produit, API et opération.</span><span class="sxs-lookup"><span data-stu-id="554b0-221">**Activity** provides reports that drill down on the specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="554b0-222"><a name="next-steps"> </a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="554b0-222"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="554b0-223">Découvrez comment [protéger votre API avec des limites de débit](api-management-howto-product-with-rules.md).</span><span class="sxs-lookup"><span data-stu-id="554b0-223">Learn how to [Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add the new API to a product]: #add-api-to-product
[Subscribe to the product that contains the API]: #subscribe
[Call an operation from the Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How to manage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How to configure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
