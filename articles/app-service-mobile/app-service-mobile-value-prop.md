---
title: "À propos de Mobile Apps dans Azure App Service"
description: "Découvrez les avantages qu’App Service apporte à vos applications mobiles d’entreprise."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: 4e96cb9d-a632-4cf6-8219-0810d8ade3f9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: ac35ff9fe1c5f315c4de08de951f505627ec412b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <span data-ttu-id="cd710-103"><a name="getting-started"> </a>À propos de Mobile Apps dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="cd710-103"><a name="getting-started"> </a>About Mobile Apps in Azure App Service</span></span>
<span data-ttu-id="cd710-104">Azure App Service est une offre de [plateforme en tant que service](https://azure.microsoft.com/overview/what-is-paas/) (PaaS) entièrement gérée pour les développeurs professionnels.</span><span class="sxs-lookup"><span data-stu-id="cd710-104">Azure App Service is a fully managed [platform as a service](https://azure.microsoft.com/overview/what-is-paas/) (PaaS) offering for professional developers.</span></span> <span data-ttu-id="cd710-105">Ce service apporte un ensemble riche de fonctionnalités pour les scénarios web, mobiles et les scénarios d’intégration.</span><span class="sxs-lookup"><span data-stu-id="cd710-105">The service brings a rich set of capabilities to web, mobile, and integration scenarios.</span></span> 

<span data-ttu-id="cd710-106">La fonctionnalité Mobile Apps d’Azure App Service offre aux développeurs et aux intégrateurs de systèmes d’entreprise une plateforme de développement d’applications mobiles très évolutive et disponible dans le monde entier.</span><span class="sxs-lookup"><span data-stu-id="cd710-106">The Mobile Apps feature of Azure App Service gives enterprise developers and system integrators a mobile-application development platform that's highly scalable and globally available.</span></span>

![Aperçu visuel des fonctionnalités Mobile Apps](./media/app-service-mobile-value-prop/overview.png)

## <a name="why-mobile-apps"></a><span data-ttu-id="cd710-108">Pourquoi Mobile Apps ?</span><span class="sxs-lookup"><span data-stu-id="cd710-108">Why Mobile Apps?</span></span>
<span data-ttu-id="cd710-109">Avec la fonctionnalité Mobile Apps, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="cd710-109">With the Mobile Apps feature, you can:</span></span>

* <span data-ttu-id="cd710-110">**Générer des applications natives et multiplateformes** : que vous génériez des applications natives iOS, Android et Windows ou des applications multiplateformes Xamarin ou Cordova (Phonegap), vous pouvez tirer parti d’App Service à l’aide de Kits de développement logiciel (SDK) natifs.</span><span class="sxs-lookup"><span data-stu-id="cd710-110">**Build native and cross-platform apps**: Whether you're building native iOS, Android, and Windows apps or cross-platform Xamarin or Cordova (PhoneGap) apps, you can take advantage of App Service by using native SDKs.</span></span>
* <span data-ttu-id="cd710-111">**Se connecter aux systèmes de votre entreprise** : la fonctionnalité Mobile Apps vous permet d’ajouter une authentification d’entreprise en quelques minutes et de vous connecter à vos ressources locales et cloud d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="cd710-111">**Connect to your enterprise systems**: With the Mobile Apps feature, you can add corporate sign-in in minutes, and connect to your enterprise on-premises or cloud resources.</span></span>
* <span data-ttu-id="cd710-112">**Créer des applications disponibles hors connexion avec la synchronisation des données** : augmentez davantage la productivité de votre personnel mobile en créant des applications qui fonctionnent hors connexion et qui utilisent la fonctionnalité Mobile Apps pour synchroniser les données en arrière-plan quand la connexion est établie avec l’une de vos sources de données d’entreprise ou API de software as a service (SaaS).</span><span class="sxs-lookup"><span data-stu-id="cd710-112">**Build offline-ready apps with data sync**: Make your mobile workforce more productive by building apps that work offline, and use Mobile Apps to sync data in the background when connectivity is present with any of your enterprise data sources or software as a service (SaaS) APIs.</span></span>
* <span data-ttu-id="cd710-113">**Notifications push pour des millions de personnes en quelques secondes** : fidélisez vos clients en leur envoyant en temps opportun des notifications push instantanées, adaptées à leurs besoins et sur n’importe quel appareil.</span><span class="sxs-lookup"><span data-stu-id="cd710-113">**Push notifications to millions in seconds**: Engage your customers with instant push notifications on any device, personalized to their needs and sent when the time is right.</span></span>

## <a name="mobile-apps-features"></a><span data-ttu-id="cd710-114">Fonctionnalités Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="cd710-114">Mobile Apps features</span></span>
<span data-ttu-id="cd710-115">Les fonctions qui suivent sont importantes pour le développement mobile Cloud :</span><span class="sxs-lookup"><span data-stu-id="cd710-115">The following features are important to cloud-enabled mobile development:</span></span>

* <span data-ttu-id="cd710-116">**Authentification et autorisation** : bénéficiez d’une liste toujours plus longue de fournisseurs d’identité, notamment Azure Active Directory pour l’authentification d’entreprise, et de fournisseurs de médias sociaux tels que Facebook, Google, Twitter et les comptes Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cd710-116">**Authentication and authorization**: Select from an ever-growing list of identity providers, including Azure Active Directory for enterprise authentication, plus social providers such as Facebook, Google, Twitter, and Microsoft accounts.</span></span> <span data-ttu-id="cd710-117">Mobile Apps offre un service OAuth 2.0 pour chaque fournisseur.</span><span class="sxs-lookup"><span data-stu-id="cd710-117">Mobile Apps offers an OAuth 2.0 service for each provider.</span></span> <span data-ttu-id="cd710-118">Vous pouvez également intégrer le kit de développement logiciel du fournisseur d’identité pour la fonctionnalité spécifique du fournisseur.</span><span class="sxs-lookup"><span data-stu-id="cd710-118">You can also integrate the SDK for the identity provider for provider-specific functionality.</span></span>

    <span data-ttu-id="cd710-119">Apprenez-en davantage sur nos [fonctionnalités d’authentification].</span><span class="sxs-lookup"><span data-stu-id="cd710-119">Discover more about our [authentication features].</span></span>

* <span data-ttu-id="cd710-120">**Accès aux données** : Mobile Apps offre une source de données OData v3 compatible avec les mobiles liée à SQL Azure Database ou à un serveur SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="cd710-120">**Data access**: Mobile Apps provides a mobile-friendly OData v3 data source that's linked to Azure SQL Database or an on-premises SQL server.</span></span> <span data-ttu-id="cd710-121">Étant donné que ce service peut être développé à partir d’Entity Framework, vous pouvez l’intégrer facilement à d’autres fournisseurs de données NoSQL et SQL, notamment le [Stockage de tables Azure], MongoDB, [Azure Cosmos DB] et des fournisseurs d’API SaaS comme Office 365 et Salesforce.com.</span><span class="sxs-lookup"><span data-stu-id="cd710-121">Because this service can be based on Entity Framework, you can easily integrate with other NoSQL and SQL data providers, including [Azure Table storage], MongoDB, [Azure Cosmos DB], and SaaS API providers such as Office 365 and Salesforce.com.</span></span>

* <span data-ttu-id="cd710-122">**Synchronisation hors connexion** : nos Kits de développement logiciel (SDK) clients permettent de facilement générer des applications mobiles robustes et réactives exploitables sur des jeux de données hors connexion.</span><span class="sxs-lookup"><span data-stu-id="cd710-122">**Offline sync**: Our client SDKs make it easy to build robust and responsive mobile applications that operate with an offline dataset.</span></span> <span data-ttu-id="cd710-123">Vous pouvez synchroniser automatiquement les données principales, y compris la prise en charge de la résolution de conflit.</span><span class="sxs-lookup"><span data-stu-id="cd710-123">You can sync this dataset automatically with the back-end data, including conflict-resolution support.</span></span>

  <span data-ttu-id="cd710-124">Apprenez-en davantage sur nos [fonctionnalités de données].</span><span class="sxs-lookup"><span data-stu-id="cd710-124">Discover more about our [data features].</span></span>

* <span data-ttu-id="cd710-125">**Notifications Push** : nos Kits de développement logiciel (SDK) clients s’intègrent de façon transparente aux fonctionnalités d’inscription d’Azure Notification Hubs afin de pouvoir envoyer des notifications Push à des millions d’utilisateurs simultanément.</span><span class="sxs-lookup"><span data-stu-id="cd710-125">**Push notifications**: Our client SDKs integrate seamlessly with the registration capabilities of Azure Notification Hubs, so you can send push notifications to millions of users simultaneously.</span></span>

  <span data-ttu-id="cd710-126">Apprenez-en davantage sur nos [fonctionnalités de notification Push].</span><span class="sxs-lookup"><span data-stu-id="cd710-126">Discover more about our [push notification features].</span></span>

* <span data-ttu-id="cd710-127">**Kits de développement logiciel clients** : nous fournissons un ensemble complet de Kits de développement logiciel clients qui concernent le développement natif ([iOS], [Android] et [Windows]), le développement multiplateforme ([Xamarin.iOS et Xamarin.Android], [Xamarin.Forms]) et le développement d’applications hybrides ([Apache Cordova]).</span><span class="sxs-lookup"><span data-stu-id="cd710-127">**Client SDKs**: We provide a complete set of client SDKs that cover native development ([iOS], [Android], and [Windows]), cross-platform development ([Xamarin.iOS and Xamarin.Android], [Xamarin.Forms]), and hybrid application development ([Apache Cordova]).</span></span> <span data-ttu-id="cd710-128">Chaque kit de développement logiciel client est disponible avec une licence MIT et open source.</span><span class="sxs-lookup"><span data-stu-id="cd710-128">Each client SDK is available with an MIT license and is open source.</span></span>

## <a name="azure-app-service-features"></a><span data-ttu-id="cd710-129">Fonctionnalités d’Azure App Service</span><span class="sxs-lookup"><span data-stu-id="cd710-129">Azure App Service features</span></span>
<span data-ttu-id="cd710-130">Les fonctionnalités suivantes de la plate-forme sont utiles aux sites de production mobile :</span><span class="sxs-lookup"><span data-stu-id="cd710-130">The following platform features are useful for mobile production sites:</span></span>

* <span data-ttu-id="cd710-131">**Mise à l’échelle automatique** : avec App Service, vous pouvez facilement monter en puissance ou augmenter la taille des instances pour vous adapter à n’importe quelle charge cliente entrante.</span><span class="sxs-lookup"><span data-stu-id="cd710-131">**Autoscaling**: With App Service, you can quickly scale up or scale out to handle any incoming customer load.</span></span> <span data-ttu-id="cd710-132">Sélectionnez manuellement le nombre et la taille des machines virtuelles, ou configurez la mise à l’échelle automatique pour dimensionner votre back end d’application mobile en fonction de la charge ou d’une planification.</span><span class="sxs-lookup"><span data-stu-id="cd710-132">Manually select the number and size of VMs, or set up autoscaling to scale your mobile-app back end based on load or schedule.</span></span>

  <span data-ttu-id="cd710-133">Apprenez-en davantage sur la [Mise à l’échelle automatique].</span><span class="sxs-lookup"><span data-stu-id="cd710-133">Discover more about [autoscaling].</span></span>

* <span data-ttu-id="cd710-134">**Environnements intermédiaires** : App Service peut exécuter plusieurs versions de votre site afin de pouvoir effectuer des tests A/B, de procéder à des tests en production dans le cadre d’un plan DevOps plus étendu et d’effectuer la préproduction sur place d’un nouveau serveur principal.</span><span class="sxs-lookup"><span data-stu-id="cd710-134">**Staging environments**: App Service can run multiple versions of your site, so you can perform A/B testing, test in production as part of a larger DevOps plan, and do in-place staging of a new back end.</span></span>

  <span data-ttu-id="cd710-135">Apprenez-en davantage sur les [Environnements intermédiaires].</span><span class="sxs-lookup"><span data-stu-id="cd710-135">Discover more about [staging environments].</span></span>

* <span data-ttu-id="cd710-136">**Déploiement continu** : App Service peut s’intégrer aux systèmes de gestion de la chaîne d’approvisionnement (SCM) courants afin de déployer automatiquement une nouvelle version de votre serveur principal en le transférant vers une branche de votre système SCM.</span><span class="sxs-lookup"><span data-stu-id="cd710-136">**Continuous deployment**: App Service can integrate with common supply chain management (SCM) systems, so you can automatically deploy a new version of your back end by pushing to a branch of your SCM system.</span></span>

  <span data-ttu-id="cd710-137">Apprenez-en davantage sur les [options de déploiement].</span><span class="sxs-lookup"><span data-stu-id="cd710-137">Discover more about [deployment options].</span></span>

* <span data-ttu-id="cd710-138">**Mise en réseau virtuelle** : App Service peut se connecter à des ressources locales à l’aide de connexions réseau virtuel, ExpressRoute Azure ou hybrides.</span><span class="sxs-lookup"><span data-stu-id="cd710-138">**Virtual networking**: App Service can connect to on-premises resources by using virtual network, Azure ExpressRoute, or hybrid connections.</span></span>

  <span data-ttu-id="cd710-139">Apprenez-en davantage sur les [connexions hybrides], [les réseaux virtuels] et [ExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="cd710-139">Discover more about [hybrid connections], [virtual networks], and [ExpressRoute].</span></span>

* <span data-ttu-id="cd710-140">**Environnements isolés/dédiés** : vous pouvez exécuter App Service dans un environnement totalement isolé et dédié pour exécuter en toute sécurité des applications Azure App Service à grande échelle.</span><span class="sxs-lookup"><span data-stu-id="cd710-140">**Isolated and dedicated environments**: You can run App Service in a fully isolated and dedicated environment for securely running Azure App Service apps at high scale.</span></span> <span data-ttu-id="cd710-141">L’environnement est idéal pour des charges de travail nécessitant un accès à grande échelle, isolé ou avec réseau sécurisé.</span><span class="sxs-lookup"><span data-stu-id="cd710-141">This environment is ideal for application workloads that require high scale, isolation, or secure network access.</span></span>

  <span data-ttu-id="cd710-142">Apprenez-en davantage sur les [environnements App Service].</span><span class="sxs-lookup"><span data-stu-id="cd710-142">Discover more about [App Service environments].</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd710-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cd710-143">Next steps</span></span>

<span data-ttu-id="cd710-144">Pour prendre en main Mobile Apps dans Azure App Service, terminez le didacticiel de [prise en main].</span><span class="sxs-lookup"><span data-stu-id="cd710-144">To get started with Mobile Apps in Azure App Service, complete the [getting started] tutorial.</span></span> <span data-ttu-id="cd710-145">Le didacticiel explique les principes fondamentaux de la production d’un back end mobile et d’un client de votre choix.</span><span class="sxs-lookup"><span data-stu-id="cd710-145">The tutorial covers the basics of producing a mobile back end and client of your choice.</span></span> <span data-ttu-id="cd710-146">Il explique également comment intégrer l’authentification, la synchronisation hors connexion et les notifications push.</span><span class="sxs-lookup"><span data-stu-id="cd710-146">It also covers integrating authentication, offline sync, and push notifications.</span></span> <span data-ttu-id="cd710-147">Vous pouvez effectuer le didacticiel plusieurs fois, une fois pour chaque application cliente.</span><span class="sxs-lookup"><span data-stu-id="cd710-147">You can complete the tutorial multiple times, once for each client application.</span></span>

<span data-ttu-id="cd710-148">Pour plus d’informations sur Mobile Apps, consultez notre [parcours d’apprentissage].</span><span class="sxs-lookup"><span data-stu-id="cd710-148">For more information about Mobile Apps, review our [learning map].</span></span>
<span data-ttu-id="cd710-149">Pour plus d’informations sur la plateforme Azure App Service, consultez la rubrique [Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="cd710-149">For more information about the Azure App Service platform, see [Azure App Service].</span></span>

<!-- URLs. -->
[Migrate your mobile service to App Service]: app-service-mobile-migrating-from-mobile-services.md
[Azure App Service]: ../app-service/app-service-value-prop-what-is.md
[prise en main]: app-service-mobile-ios-get-started.md
[Stockage de tables Azure]:../cosmos-db/table-storage-how-to-use-dotnet.md
[Azure Cosmos DB]: ../cosmos-db/documentdb-get-started.md
[fonctionnalités d’authentification]: ./app-service-mobile-auth.md
[fonctionnalités de données]: ./app-service-mobile-offline-data-sync.md
[fonctionnalités de notification Push]: ../notification-hubs/notification-hubs-push-notification-overview.md
[iOS]: ./app-service-mobile-ios-how-to-use-client-library.md
[Android]: ./app-service-mobile-android-how-to-use-client-library.md
[Windows]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.iOS et Xamarin.Android]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.Forms]: ./app-service-mobile-xamarin-forms-get-started.md
[Apache Cordova]: ./app-service-mobile-cordova-how-to-use-client-library.md
[Mise à l’échelle automatique]: ../app-service-web/web-sites-scale.md
[Environnements intermédiaires]: ../app-service-web/web-sites-staged-publishing.md
[options de déploiement]: ../app-service-web/web-sites-deploy.md
[connexions hybrides]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[les réseaux virtuels]: ../app-service-web/web-sites-integrate-with-vnet.md
[ExpressRoute]: ../app-service-web/app-service-app-service-environment-network-configuration-expressroute.md
[environnements App Service]: ../app-service-web/app-service-app-service-environment-intro.md
[parcours d’apprentissage]: https://azure.microsoft.com/en-us/documentation/learning-paths/appservice-mobileapps/
