---
title: aaaCreate une application Cordova sur Azure App Service Mobile Apps | Documents Microsoft
description: "Suivez ce didacticiel tooget un bon départ avec les serveurs principaux de l’application mobile Azure pour le développement d’Apache Cordova"
services: app-service\mobile
documentationcenter: javascript
author: ggailey777
manager: syntaxc4
editor: 
tags: 
keywords: cordova, javascript, mobile, client
ms.assetid: 0b08fc12-0a80-42d3-9cc1-9b3f8d3e3a3f
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: hero-article
ms.date: 07/07/2017
ms.author: glenga
ms.openlocfilehash: 4981cbc0686c15230019ac9f30495f30cbf2c791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-cordova-app"></a><span data-ttu-id="49532-104">Créer une application Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="49532-104">Create an Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="49532-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="49532-105">Overview</span></span>
<span data-ttu-id="49532-106">Ce didacticiel vous montre comment tooadd un backend de cloud service application mobile de tooan Apache Cordova à l’aide d’un serveur principal d’application mobile Azure.</span><span class="sxs-lookup"><span data-stu-id="49532-106">This tutorial shows you how tooadd a cloud-based backend service tooan Apache Cordova mobile app by using an Azure mobile app backend.</span></span>  <span data-ttu-id="49532-107">Vous créez un backend d’application mobile et une simple application Apache Cordova *Todo list* qui stocke les données d’application dans Azure.</span><span class="sxs-lookup"><span data-stu-id="49532-107">You create both a new mobile app backend and a simple *Todo list* Apache Cordova app that stores app data in Azure.</span></span>

<span data-ttu-id="49532-108">Ils auront terminé ce didacticiel est un composant requis pour tous les autres didacticiels Apache Cordova sur l’utilisation de la fonctionnalité des applications mobiles hello dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="49532-108">Completing this tutorial is a prerequisite for all other Apache Cordova tutorials about using hello Mobile Apps feature in Azure App Service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49532-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="49532-109">Prerequisites</span></span>
<span data-ttu-id="49532-110">toocomplete ce didacticiel, vous devez hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="49532-110">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="49532-111">Un PC équipé de [Visual Studio Community 2017] ou d’une version plus récente.</span><span class="sxs-lookup"><span data-stu-id="49532-111">A PC with [Visual Studio Community 2017] or newer.</span></span>
* <span data-ttu-id="49532-112">[Visual Studio Tools pour Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="49532-112">[Visual Studio Tools for Apache Cordova].</span></span>
* <span data-ttu-id="49532-113">Un [compte Azure actif](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49532-113">An [active Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<span data-ttu-id="49532-114">Vous pouvez également contourner Visual Studio et utiliser directement de ligne de commande Apache Cordova hello.</span><span class="sxs-lookup"><span data-stu-id="49532-114">You may also bypass Visual Studio and use hello Apache Cordova command line directly.</span></span>  <span data-ttu-id="49532-115">À l’aide de la ligne de commande hello est utile lorsqu’il a terminé le didacticiel hello sur un ordinateur Mac.</span><span class="sxs-lookup"><span data-stu-id="49532-115">Using hello command line is useful when completing hello tutorial on a Mac computer.</span></span>  <span data-ttu-id="49532-116">Compiler des applications client Apache Cordova à l’aide de la ligne de commande hello n’est pas couverte par ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="49532-116">Compiling Apache Cordova client applications using hello command line is not covered by this tutorial.</span></span>

## <a name="create-an-azure-mobile-app-backend"></a><span data-ttu-id="49532-117">Créer un serveur principal d'applications mobiles Azure</span><span class="sxs-lookup"><span data-stu-id="49532-117">Create an Azure mobile app backend</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

[<span data-ttu-id="49532-118">Regarder une vidéo montrant des étapes similaires</span><span class="sxs-lookup"><span data-stu-id="49532-118">Watch a video showing similar steps</span></span>](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-1-Create-an-Azure-Mobile-App)

## <a name="configure-hello-server-project"></a><span data-ttu-id="49532-119">Configurer le projet de serveur hello</span><span class="sxs-lookup"><span data-stu-id="49532-119">Configure hello server project</span></span>
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-apache-cordova-app"></a><span data-ttu-id="49532-120">Téléchargez et exécutez l’application de hello Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="49532-120">Download and run hello Apache Cordova app</span></span>
[!INCLUDE [app-service-mobile-cordova-run-app](../../includes/app-service-mobile-cordova-run-app.md)]

## <a name="next-steps"></a><span data-ttu-id="49532-121">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="49532-121">Next Steps</span></span>
<span data-ttu-id="49532-122">Maintenant que vous terminé ce didacticiel de démarrage rapide, déplacez les tooone Hello suivant didacticiels :</span><span class="sxs-lookup"><span data-stu-id="49532-122">Now that you completed this quick start tutorial, move on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="49532-123">[Ajouter des données en mode hors connexion](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova application.</span><span class="sxs-lookup"><span data-stu-id="49532-123">[Add Offline Data](app-service-mobile-cordova-get-started-offline-data.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="49532-124">[Ajouter l’authentification](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova application.</span><span class="sxs-lookup"><span data-stu-id="49532-124">[Add Authentication](app-service-mobile-cordova-get-started-users.md) tooyour Apache Cordova app.</span></span>
* <span data-ttu-id="49532-125">[Ajouter des Notifications Push](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova application.</span><span class="sxs-lookup"><span data-stu-id="49532-125">[Add Push Notifications](app-service-mobile-cordova-get-started-push.md) tooyour Apache Cordova app.</span></span>

<span data-ttu-id="49532-126">En savoir plus sur les concepts clés avec Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="49532-126">Learn more about key concepts with Azure App Service.</span></span>

* <span data-ttu-id="49532-127">[Données hors connexion]</span><span class="sxs-lookup"><span data-stu-id="49532-127">[Offline Data]</span></span>
* <span data-ttu-id="49532-128">[Authentification]</span><span class="sxs-lookup"><span data-stu-id="49532-128">[Authentication]</span></span>
* <span data-ttu-id="49532-129">[Notifications Push]</span><span class="sxs-lookup"><span data-stu-id="49532-129">[Push Notifications]</span></span>

<span data-ttu-id="49532-130">Découvrez comment toouse hello kits de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="49532-130">Learn how toouse hello SDKs.</span></span>

* <span data-ttu-id="49532-131">[Kit de développement logiciel (SDK) Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="49532-131">[Apache Cordova SDK]</span></span>
* <span data-ttu-id="49532-132">[Kit de développement logiciel du serveur ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="49532-132">[ASP.NET Server SDK]</span></span>
* <span data-ttu-id="49532-133">[Kit de développement logiciel du serveur Node.js]</span><span class="sxs-lookup"><span data-stu-id="49532-133">[Node.js Server SDK]</span></span>

<!-- Images. -->

<!-- URLs -->
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2017]: http://www.visualstudio.com/
[Visual Studio Tools pour Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Données hors connexion]: app-service-mobile-offline-data-sync.md
[Authentification]: app-service-mobile-auth.md
[Notifications Push]: ../notification-hubs/notification-hubs-push-notification-overview.md
[Kit de développement logiciel (SDK) Apache Cordova]: app-service-mobile-cordova-how-to-use-client-library.md
[Kit de développement logiciel du serveur ASP.NET]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Kit de développement logiciel du serveur Node.js]: app-service-mobile-node-backend-how-to-use-server-sdk.md
