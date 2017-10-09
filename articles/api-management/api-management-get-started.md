---
title: "aaaManage votre première API de gestion des API Azure | Documents Microsoft"
description: "Découvrez comment toocreate API, ajouter des opérations et commencer à la gestion des API."
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
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a><span data-ttu-id="2ff6f-103">Gérer votre première API dans Gestion des API Azure</span><span class="sxs-lookup"><span data-stu-id="2ff6f-103">Manage your first API in Azure API Management</span></span>
## <span data-ttu-id="2ff6f-104"><a name="overview"></a>Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="2ff6f-104"><a name="overview"> </a>Overview</span></span>
<span data-ttu-id="2ff6f-105">Ce guide vous explique comment tooquickly prise en main d’à l’aide de la gestion des API Azure et votre premier appel d’API.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-105">This guide shows you how tooquickly get started in using Azure API Management and make your first API call.</span></span>

## <span data-ttu-id="2ff6f-106"><a name="concepts"></a>Qu’est-ce que Gestion des API Azure ?</span><span class="sxs-lookup"><span data-stu-id="2ff6f-106"><a name="concepts"> </a>What is Azure API Management?</span></span>
<span data-ttu-id="2ff6f-107">Vous pouvez utiliser Gestion des API Azure tootake n’importe quel serveur principal et lancer un programme API à part entière basé sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-107">You can use Azure API Management tootake any backend and launch a full-fledged API program based on it.</span></span>

<span data-ttu-id="2ff6f-108">Scénarios courants :</span><span class="sxs-lookup"><span data-stu-id="2ff6f-108">Common scenarios include:</span></span>

* <span data-ttu-id="2ff6f-109">**Sécurisation d’infrastructures mobiles** par régulation de l’accès à l’aide de clés d’API pour éviter les attaques par déni de service (DOS) en utilisant la limitation ou des stratégies de sécurité avancées, telles que la validation de jeton JWT</span><span class="sxs-lookup"><span data-stu-id="2ff6f-109">**Securing mobile infrastructure** by gating access with API keys, preventing DOS attacks by using throttling, or using advanced security policies like JWT token validation.</span></span>
* <span data-ttu-id="2ff6f-110">**L’activation des écosystèmes partenaire ISV** en offrant l’intégration de partenaire rapide via le développeur de hello, portail et la création d’un toodecouple de façade API à partir des implémentations internes qui ne sont pas de la consommation du partenaire.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-110">**Enabling ISV partner ecosystems** by offering fast partner onboarding through hello developer portal and building an API facade toodecouple from internal implementations that are not ripe for partner consumption.</span></span>
* <span data-ttu-id="2ff6f-111">**Exécution d’un programme API interne** en offrant un emplacement centralisé pour toocommunicate d’organisation hello sur la disponibilité de hello et de la plus récente des modifications tooAPIs, régulation d’accès basé sur les comptes de société, toutes basées sur un canal sécurisé entre Hello passerelle API et hello back-end.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-111">**Running an internal API program** by offering a centralized location for hello organization toocommunicate about hello availability and latest changes tooAPIs, gating access based on organizational accounts, all based on a secured channel between hello API gateway and hello backend.</span></span>

<span data-ttu-id="2ff6f-112">système de Hello est constitué par hello suivant des composants :</span><span class="sxs-lookup"><span data-stu-id="2ff6f-112">hello system is made up of hello following components:</span></span>

* <span data-ttu-id="2ff6f-113">Hello **passerelle API** est le point de terminaison hello qui :</span><span class="sxs-lookup"><span data-stu-id="2ff6f-113">hello **API gateway** is hello endpoint that:</span></span>
  
  * <span data-ttu-id="2ff6f-114">Accepte les API appelle et les route les serveurs principaux tooyour.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-114">Accepts API calls and routes them tooyour backends.</span></span>
  * <span data-ttu-id="2ff6f-115">vérifie les clés d’API, les jetons JWT, les certificats et les autres informations d’identification ;</span><span class="sxs-lookup"><span data-stu-id="2ff6f-115">Verifies API keys, JWT tokens, certificates, and other credentials.</span></span>
  * <span data-ttu-id="2ff6f-116">applique des quotas d’utilisation et des limites de débit ;</span><span class="sxs-lookup"><span data-stu-id="2ff6f-116">Enforces usage quotas and rate limits.</span></span>
  * <span data-ttu-id="2ff6f-117">Transforme votre API hello volée, sans modification de code.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-117">Transforms your API on hello fly without code modifications.</span></span>
  * <span data-ttu-id="2ff6f-118">met en cache les réponses du serveur principal lorsqu’il est configuré ;</span><span class="sxs-lookup"><span data-stu-id="2ff6f-118">Caches backend responses where set up.</span></span>
  * <span data-ttu-id="2ff6f-119">enregistre les métadonnées relatives aux appels à des fins d’analyse.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-119">Logs call metadata for analytics purposes.</span></span>
* <span data-ttu-id="2ff6f-120">Hello **portail de publication** est hello interface d’administration dans lequel vous configurez votre programme API.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-120">hello **publisher portal** is hello administrative interface where you set up your API program.</span></span> <span data-ttu-id="2ff6f-121">Utilisez-le pour :</span><span class="sxs-lookup"><span data-stu-id="2ff6f-121">Use it to:</span></span>
  
  * <span data-ttu-id="2ff6f-122">définir ou importer le schéma d’API ;</span><span class="sxs-lookup"><span data-stu-id="2ff6f-122">Define or import API schema.</span></span>
  * <span data-ttu-id="2ff6f-123">intégrer des API aux produits sous forme de packages ;</span><span class="sxs-lookup"><span data-stu-id="2ff6f-123">Package APIs into products.</span></span>
  * <span data-ttu-id="2ff6f-124">Configurer des stratégies, telles que les quotas ou transformations sur hello API.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-124">Set up policies like quotas or transformations on hello APIs.</span></span>
  * <span data-ttu-id="2ff6f-125">obtenir des informations issues de l’analyse ;</span><span class="sxs-lookup"><span data-stu-id="2ff6f-125">Get insights from analytics.</span></span>
  * <span data-ttu-id="2ff6f-126">gérer les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-126">Manage users.</span></span>
* <span data-ttu-id="2ff6f-127">Hello **portail des développeurs** sert de présence du site web principal hello pour les développeurs, où ils peuvent :</span><span class="sxs-lookup"><span data-stu-id="2ff6f-127">hello **developer portal** serves as hello main web presence for developers, where they can:</span></span>
  
  * <span data-ttu-id="2ff6f-128">lire la documentation de l’API ;</span><span class="sxs-lookup"><span data-stu-id="2ff6f-128">Read API documentation.</span></span>
  * <span data-ttu-id="2ff6f-129">Essayer une API via une console interactive de hello.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-129">Try out an API via hello interactive console.</span></span>
  * <span data-ttu-id="2ff6f-130">Créer un compte et vous abonner tooget API clés.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-130">Create an account and subscribe tooget API keys.</span></span>
  * <span data-ttu-id="2ff6f-131">accéder aux analyses relatives à leur propre utilisation.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-131">Access analytics on their own usage.</span></span>

## <span data-ttu-id="2ff6f-132"><a name="create-service-instance"></a>Création d’une instance du service Gestion des API</span><span class="sxs-lookup"><span data-stu-id="2ff6f-132"><a name="create-service-instance"> </a>Create an API Management instance</span></span>
> [!NOTE]
> <span data-ttu-id="2ff6f-133">toocomplete ce didacticiel, vous avez besoin d’un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-133">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="2ff6f-134">Si vous ne possédez pas de compte, vous pouvez créer un compte gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-134">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="2ff6f-135">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][Azure Free Trial].</span><span class="sxs-lookup"><span data-stu-id="2ff6f-135">For details, see [Azure Free Trial][Azure Free Trial].</span></span>
> 
> 

<span data-ttu-id="2ff6f-136">Hello première étape de travail avec la gestion des API est toocreate une instance de service.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-136">hello first step in working with API Management is toocreate a service instance.</span></span> <span data-ttu-id="2ff6f-137">Connectez-vous à toohello [Azure Portal] [ Azure Portal] et cliquez sur **nouveau**, **Web + Mobile**, **gestion des API**.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-137">Sign in toohello [Azure Portal][Azure Portal] and click **New**, **Web + Mobile**, **API Management**.</span></span>

![Nouvelle instance Gestion des API][api-management-create-instance-menu]

<span data-ttu-id="2ff6f-139">Pour **nom**, spécifiez un toouse de nom de sous-domaine unique pour l’URL du service hello.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-139">For **Name**, specify a unique sub-domain name toouse for hello service URL.</span></span>

<span data-ttu-id="2ff6f-140">Choisissez hello souhaité **abonnement**, **groupe de ressources** et **emplacement** pour votre instance de service.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-140">Choose hello desired **Subscription**, **Resource group** and **Location** for your service instance.</span></span>

<span data-ttu-id="2ff6f-141">Entrez **Contoso Ltd.** pour hello **nom de l’organisation**, puis entrez votre adresse de messagerie dans hello **E-Mail administrateur** champ.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-141">Enter **Contoso Ltd.** for hello **Organization Name**, and enter your email address in hello **Administrator E-Mail** field.</span></span>

> [!NOTE]
> <span data-ttu-id="2ff6f-142">Cette adresse de messagerie est utilisée pour les notifications de hello système de gestion des API.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-142">This email address is used for notifications from hello API Management system.</span></span> <span data-ttu-id="2ff6f-143">Pour plus d’informations, consultez [comment tooconfigure notifications et modèles dans Azure API Management de messagerie][How tooconfigure notifications and email templates in Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="2ff6f-143">For more information, see [How tooconfigure notifications and email templates in Azure API Management][How tooconfigure notifications and email templates in Azure API Management].</span></span>
> 
> 

![Nouveau service Gestion des API][api-management-create-instance-step1]

<span data-ttu-id="2ff6f-145">Les instances du service Gestion des API sont disponibles dans trois niveaux : Développeur, Standard et Premium.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-145">API Management service instances are available in three tiers: Developer, Standard, and Premium.</span></span>

> [!NOTE]
> <span data-ttu-id="2ff6f-146">Hello niveau développeur est pour le développement, le test et des programmes d’API pilotes lorsque la haute disponibilité n’est pas un problème.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-146">hello Developer Tier is for development, testing, and pilot API programs where high availability is not a concern.</span></span> <span data-ttu-id="2ff6f-147">Dans hello Standard et les niveaux Premium, vous pouvez faire évoluer votre toohandle de nombre d’unités réservées plus de trafic.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-147">In hello Standard and Premium tiers, you can scale your reserved unit count toohandle more traffic.</span></span> <span data-ttu-id="2ff6f-148">les niveaux Standard et Premium Hello fournissent votre service de gestion des API avec hello plus de puissance de traitement et de performances.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-148">hello Standard and Premium tiers provide your API Management service with hello most processing power and performance.</span></span> <span data-ttu-id="2ff6f-149">Vous pouvez effectuer ce didacticiel à l’aide de n’importe quel niveau.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-149">You can complete this tutorial by using any tier.</span></span> <span data-ttu-id="2ff6f-150">Pour en savoir plus sur les niveaux du service Gestion des API, consultez la page relative à la [tarification du service Gestion des API][API Management pricing].</span><span class="sxs-lookup"><span data-stu-id="2ff6f-150">For more information about API Management tiers, see [API Management pricing][API Management pricing].</span></span>
> 
> 

<span data-ttu-id="2ff6f-151">Cliquez sur **créer** toostart votre instance du service de configuration.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-151">Click **Create** toostart provisioning your service instance.</span></span>

![Nouveau service Gestion des API][api-management-instance-created]

<span data-ttu-id="2ff6f-153">Après la création de l’instance de service de hello, étape suivante de hello est toocreate ou importer une API.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-153">Once hello service instance is created, hello next step is toocreate or import an API.</span></span>

## <span data-ttu-id="2ff6f-154"><a name="create-api"></a>Importation d’une API</span><span class="sxs-lookup"><span data-stu-id="2ff6f-154"><a name="create-api"> </a>Import an API</span></span>
<span data-ttu-id="2ff6f-155">Une API se compose d’un ensemble d’opérations pouvant être appelées à partir d’une application cliente.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-155">An API consists of a set of operations that can be invoked from a client application.</span></span> <span data-ttu-id="2ff6f-156">Opérations d’API sont traitées tooexisting des services web.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-156">API operations are proxied tooexisting web services.</span></span>

<span data-ttu-id="2ff6f-157">Il est possible de créer des API (et d’ajouter des opérations) manuellement ou de les importer.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-157">APIs can be created (and operations can be added) manually, or they can be imported.</span></span> <span data-ttu-id="2ff6f-158">Dans ce didacticiel, nous allons importer hello API pour un service web de calculatrice exemple fourni par Microsoft et hébergé sur Azure.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-158">In this tutorial, we will import hello API for a sample calculator web service provided by Microsoft and hosted on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="2ff6f-159">Pour obtenir des conseils sur la création d’une API et l’ajout manuel des opérations, consultez [comment toocreate API](api-management-howto-create-apis.md) et [comment tooadd opérations tooan API](api-management-howto-add-operations.md).</span><span class="sxs-lookup"><span data-stu-id="2ff6f-159">For guidance on creating an API and manually adding operations, see [How toocreate APIs](api-management-howto-create-apis.md) and [How tooadd operations tooan API](api-management-howto-add-operations.md).</span></span>
> 
> 

<span data-ttu-id="2ff6f-160">API est configurés à partir du portail de publication hello.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-160">APIs are configured from hello publisher portal.</span></span> <span data-ttu-id="2ff6f-161">tooreach, cliquez sur **portail de publication** à partir de la barre d’outils du service hello.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-161">tooreach it, click **Publisher portal** from hello service toolbar.</span></span>

![Portail des éditeurs][api-management-management-console]

<span data-ttu-id="2ff6f-163">calcul de hello tooimport API, cliquez sur **API** de hello **gestion des API** menu sur hello gauche, puis cliquez sur **API d’importation**.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-163">tooimport hello calculator API, click **APIs** from hello **API Management** menu on hello left, and then click **Import API**.</span></span>

![Bouton Importer l’API][api-management-import-api]

<span data-ttu-id="2ff6f-165">Effectuez hello suivant les étapes tooconfigure hello calculatrice API :</span><span class="sxs-lookup"><span data-stu-id="2ff6f-165">Perform hello following steps tooconfigure hello calculator API:</span></span>

1. <span data-ttu-id="2ff6f-166">Cliquez sur **From URL**, entrez **http://calcapi.cloudapp.net/calcapi.json** dans hello **URL du document de spécification** texte, puis cliquez sur hello **Swagger**  case d’option.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-166">Click **From URL**, enter **http://calcapi.cloudapp.net/calcapi.json** into hello **Specification document URL** text box, and click hello **Swagger** radio button.</span></span>
2. <span data-ttu-id="2ff6f-167">Type **calc** dans hello **suffixe d’URL d’API Web** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-167">Type **calc** into hello **Web API URL suffix** text box.</span></span>
3. <span data-ttu-id="2ff6f-168">Cliquez sur Bonjour **produits (facultatifs)** et sélectionnez **Starter**.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-168">Click in hello **Products (optional)** box and choose **Starter**.</span></span>
4. <span data-ttu-id="2ff6f-169">Cliquez sur **enregistrer** tooimport hello API.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-169">Click **Save** tooimport hello API.</span></span>

![Ajouter une nouvelle API][api-management-import-new-api]

> [!NOTE]
> <span data-ttu-id="2ff6f-171">**Gestion des API** prend actuellement en charge les versions 1.2 et 2.0 du document Swagger dans le cadre d’une importation.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-171">**API Management** currently supports both 1.2 and 2.0 version of Swagger document for import.</span></span> <span data-ttu-id="2ff6f-172">Même si la [spécification Swagger 2.0](http://swagger.io/specification) indique que les propriétés `host`, `basePath` et `schemes` sont facultatives, votre document Swagger 2.0 **DOIT** contenir ces propriétés ; dans le cas contraire, l’importation échouera.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-172">Make sure that, even though [Swagger 2.0 specification](http://swagger.io/specification) declares that `host`, `basePath`, and `schemes` properties are optional, your Swagger 2.0 document **MUST** contain those properties; otherwise it won't get imported.</span></span> 
> 
> 

<span data-ttu-id="2ff6f-173">Une fois les API hello est importé, hello page Résumé pour l’API de hello s’affiche dans le portail de publication hello.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-173">Once hello API is imported, hello summary page for hello API is displayed in hello publisher portal.</span></span>

![Résumé des API][api-management-imported-api-summary]

<span data-ttu-id="2ff6f-175">Hello section API comporte plusieurs onglets.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-175">hello API section has several tabs.</span></span> <span data-ttu-id="2ff6f-176">Hello **Résumé** onglet affiche les mesures de base et de plus d’informations sur les API de hello.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-176">hello **Summary** tab displays basic metrics and information about hello API.</span></span> <span data-ttu-id="2ff6f-177">Hello [paramètres](api-management-howto-create-apis.md#configure-api-settings) onglet est utilisée configuration hello tooview et modifier d’API.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-177">hello [Settings](api-management-howto-create-apis.md#configure-api-settings) tab is used tooview and edit hello configuration for an API.</span></span> <span data-ttu-id="2ff6f-178">Hello [Operations](api-management-howto-add-operations.md) onglet est les opérations utilisées toomanage hello l’API.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-178">hello [Operations](api-management-howto-add-operations.md) tab is used toomanage hello API's operations.</span></span> <span data-ttu-id="2ff6f-179">Hello **sécurité** onglet peut être l’authentification de la passerelle tooconfigure utilisé pour le serveur principal de hello à l’aide de l’authentification de base ou [authentification mutuelle des certificats](api-management-howto-mutual-certificates.md)et tooconfigure [ autorisation de l’utilisateur à l’aide d’OAuth 2.0](api-management-howto-oauth2.md).</span><span class="sxs-lookup"><span data-stu-id="2ff6f-179">hello **Security** tab can be used tooconfigure gateway authentication for hello backend server by using Basic authentication or [mutual certificate authentication](api-management-howto-mutual-certificates.md), and tooconfigure [user authorization by using OAuth 2.0](api-management-howto-oauth2.md).</span></span>  <span data-ttu-id="2ff6f-180">Hello **problèmes** onglet est tooview utilisé les problèmes signalés par les développeurs de hello qui sont à l’aide de votre API.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-180">hello **Issues** tab is used tooview issues reported by hello developers who are using your APIs.</span></span> <span data-ttu-id="2ff6f-181">Hello **produits** onglet est produits hello tooconfigure utilisé qui contiennent cette API.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-181">hello **Products** tab is used tooconfigure hello products that contain this API.</span></span>

<span data-ttu-id="2ff6f-182">Par défaut, chaque instance Gestion des API est fournie avec deux exemples de produits :</span><span class="sxs-lookup"><span data-stu-id="2ff6f-182">By default, each API Management instance comes with two sample products:</span></span>

* <span data-ttu-id="2ff6f-183">**Starter**</span><span class="sxs-lookup"><span data-stu-id="2ff6f-183">**Starter**</span></span>
* <span data-ttu-id="2ff6f-184">**Illimité**</span><span class="sxs-lookup"><span data-stu-id="2ff6f-184">**Unlimited**</span></span>

<span data-ttu-id="2ff6f-185">Dans ce didacticiel, hello API de calculatrice de base a été ajouté produit des Starter toohello lorsque hello API a été importé.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-185">In this tutorial, hello Basic Calculator API was added toohello Starter product when hello API was imported.</span></span>

<span data-ttu-id="2ff6f-186">Dans l’ordre toomake appelle tooan API, les développeurs doivent tout d’abord s’abonnent produit tooa qui leur donne accès tooit.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-186">In order toomake calls tooan API, developers must first subscribe tooa product that gives them access tooit.</span></span> <span data-ttu-id="2ff6f-187">Les développeurs peuvent s’abonner tooproducts dans le portail des développeurs hello ou les administrateurs peuvent s’abonner tooproducts les développeurs dans le portail de publication hello.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-187">Developers can subscribe tooproducts in hello developer portal, or administrators can subscribe developers tooproducts in hello publisher portal.</span></span> <span data-ttu-id="2ff6f-188">Vous êtes un administrateur depuis la création d’instance gestion des API de hello Bonjour étapes précédentes dans le didacticiel de hello, donc vous sentez déjà abonnés tooevery produit par défaut.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-188">You are an administrator since you created hello API Management instance in hello previous steps in hello tutorial, so you are already subscribed tooevery product by default.</span></span>

## <span data-ttu-id="2ff6f-189"><a name="call-operation"></a>Appeler une opération à partir du portail des développeurs hello</span><span class="sxs-lookup"><span data-stu-id="2ff6f-189"><a name="call-operation"> </a>Call an operation from hello developer portal</span></span>
<span data-ttu-id="2ff6f-190">Opérations peuvent être appelées directement depuis le portail des développeurs hello, qui fournit un moyen pratique de tooview et tester le fonctionnement d’une API hello.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-190">Operations can be called directly from hello developer portal, which provides a convenient way tooview and test hello operations of an API.</span></span> <span data-ttu-id="2ff6f-191">Dans cette étape du didacticiel, vous appelez l’API du calcul de base hello **ajouter deux entiers** opération.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-191">In this tutorial step, you will call hello Basic Calculator API's **Add two integers** operation.</span></span> <span data-ttu-id="2ff6f-192">Cliquez sur **portail des développeurs** à partir du menu de hello en hello haut à droite de portail de publication hello.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-192">Click **Developer portal** from hello menu at hello top right of hello publisher portal.</span></span>

![Portail des développeurs][api-management-developer-portal-menu]

<span data-ttu-id="2ff6f-194">Cliquez sur **API** dans le menu du haut hello, puis cliquez sur **calculatrice de base** toosee hello opérations disponibles.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-194">Click **APIs** from hello top menu, and then click **Basic Calculator** toosee hello available operations.</span></span>

![Portail des développeurs][api-management-developer-portal-calc-api]

<span data-ttu-id="2ff6f-196">Notez les descriptions d’exemple hello et les paramètres qui ont été importées avec hello API et opérations, en fournissant une documentation pour les développeurs hello qui utilisera cette opération.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-196">Note hello sample descriptions and parameters that were imported along with hello API and operations, providing documentation for hello developers that will use this operation.</span></span> <span data-ttu-id="2ff6f-197">Ces descriptions peuvent également être ajoutées lorsque des opérations sont ajoutées manuellement.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-197">These descriptions can also be added when operations are added manually.</span></span>

<span data-ttu-id="2ff6f-198">toocall hello **ajouter deux entiers** opération, cliquez sur **essayez-la**.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-198">toocall hello **Add two integers** operation, click **Try it**.</span></span>

![Essayer][api-management-developer-portal-calc-api-console]

<span data-ttu-id="2ff6f-200">Vous pouvez entrer des valeurs pour les paramètres de hello ou conserver les valeurs par défaut hello, puis cliquez sur **envoyer**.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-200">You can enter some values for hello parameters or keep hello defaults, and then click **Send**.</span></span>

![HTTP Get][api-management-invoke-get]

<span data-ttu-id="2ff6f-202">Une fois une opération est appelée, le portail des développeurs hello affiche hello **état de la réponse**, hello **les en-têtes de réponse**et n’importe quel **contenu de la réponse**.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-202">After an operation is invoked, hello developer portal displays hello **Response status**, hello **Response headers**, and any **Response content**.</span></span>

![Réponse][api-management-invoke-get-response]

## <span data-ttu-id="2ff6f-204"><a name="view-analytics"></a>Affichage des analyses</span><span class="sxs-lookup"><span data-stu-id="2ff6f-204"><a name="view-analytics"> </a>View analytics</span></span>
<span data-ttu-id="2ff6f-205">analytique tooview de calculatrice de base, portail de publication commutateur toohello arrière en sélectionnant **gérer** à partir du menu de hello en hello supérieur droit du portail des développeurs hello.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-205">tooview analytics for Basic Calculator, switch back toohello publisher portal by selecting **Manage** from hello menu at hello top right of hello developer portal.</span></span>

![Gérer][api-management-manage-menu]

<span data-ttu-id="2ff6f-207">vue par défaut pour le portail de publication hello Hello est hello **tableau de bord**, qui fournit une vue d’ensemble de votre instance de la gestion des API.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-207">hello default view for hello publisher portal is hello **Dashboard**, which provides an overview of your API Management instance.</span></span>

![tableau de bord][api-management-dashboard]

<span data-ttu-id="2ff6f-209">Pointez la souris de hello sur graphique hello pour **calculatrice de base** toosee des métriques hello spécifiques pour l’utilisation de hello Hello API pour une période donnée.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-209">Hover hello mouse over hello chart for **Basic Calculator** toosee hello specific metrics for hello usage of hello API for a given time period.</span></span>

> [!NOTE]
> <span data-ttu-id="2ff6f-210">Si vous ne voyez pas toutes les lignes de votre graphique, basculez le portail des développeurs toohello arrière effectuer des appels dans hello API, attendez quelques instants et puis revenir toohello le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-210">If you don't see any lines on your chart, switch back toohello developer portal and make some calls into hello API, wait a few moments, and then come back toohello dashboard.</span></span>
> 
> 

<span data-ttu-id="2ff6f-211">Cliquez sur **afficher les détails** tooview page de résumé hello pour hello API, y compris une version supérieure de métriques de hello affiché.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-211">Click **View Details** tooview hello summary page for hello API, including a larger version of hello displayed metrics.</span></span>

![Analyse][api-management-mouse-over]

![Résumé][api-management-api-summary-metrics]

<span data-ttu-id="2ff6f-214">Pour les métriques détaillées et des rapports, cliquez sur **Analytique** de hello **gestion des API** menu à gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-214">For detailed metrics and reports, click **Analytics** from hello **API Management** menu on hello left.</span></span>

![Vue d'ensemble][api-management-analytics-overview]

<span data-ttu-id="2ff6f-216">Hello **Analytique** section a hello suivant quatre onglets :</span><span class="sxs-lookup"><span data-stu-id="2ff6f-216">hello **Analytics** section has hello following four tabs:</span></span>

* <span data-ttu-id="2ff6f-217">**Un coup de œil** fournit de l’utilisation globale et des mesures de santé, également hello développeurs, produits principaux, API supérieur et opérations supérieure.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-217">**At a glance** provides overall usage and health metrics, as well as hello top developers, top products, top APIs, and top operations.</span></span>
* <span data-ttu-id="2ff6f-218">**Utilisation** fournit une présentation détaillée des appels d’API et de la bande passante, y compris une représentation géographique.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-218">**Usage** provides an in-depth look at API calls and bandwidth, including a geographical representation.</span></span>
* <span data-ttu-id="2ff6f-219">**Intégrité** se concentre sur les codes d'état, les taux de réussite en cache, les temps de réponse et les temps de réponse d'API et de service.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-219">**Health** focuses on status codes, cache success rates, response times, and API and service response times.</span></span>
* <span data-ttu-id="2ff6f-220">**Activité** fournit des rapports qui explorent sur une activité spécifique par le développeur, produit, API et opération hello.</span><span class="sxs-lookup"><span data-stu-id="2ff6f-220">**Activity** provides reports that drill down on hello specific activity by developer, product, API, and operation.</span></span>

## <span data-ttu-id="2ff6f-221"><a name="next-steps"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2ff6f-221"><a name="next-steps"> </a>Next steps</span></span>
* <span data-ttu-id="2ff6f-222">Découvrez comment trop[protéger votre API avec les limites de taux](api-management-howto-product-with-rules.md).</span><span class="sxs-lookup"><span data-stu-id="2ff6f-222">Learn how too[Protect your API with rate limits](api-management-howto-product-with-rules.md).</span></span>

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
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
