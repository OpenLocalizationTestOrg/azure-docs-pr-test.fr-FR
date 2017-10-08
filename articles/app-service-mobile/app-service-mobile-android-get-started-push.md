---
title: aaaAdd push notifications tooyour des applications Android avec des applications mobiles | Documents Microsoft
description: "Découvrez comment toosend des applications mobiles toouse push application Android tooyour de notifications."
services: app-service\mobile
documentationcenter: android
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 9058ed6d-e871-4179-86af-0092d0ca09d3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/12/2016
ms.author: glenga
ms.openlocfilehash: dcfb8463b395904b4bd0bf9bde2f71f259894066
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-android-app"></a><span data-ttu-id="c4f5d-103">Ajouter l’application Android de tooyour de notifications push</span><span class="sxs-lookup"><span data-stu-id="c4f5d-103">Add push notifications tooyour Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="c4f5d-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c4f5d-104">Overview</span></span>
<span data-ttu-id="c4f5d-105">Dans ce didacticiel, vous allez ajouter toohello de notifications push [Android démarrage rapide] projet afin qu’une notification push est envoyée toohello périphérique chaque fois qu’un enregistrement est inséré.</span><span class="sxs-lookup"><span data-stu-id="c4f5d-105">In this tutorial, you add push notifications toohello [Android quick start] project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="c4f5d-106">Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez hello package d’extension de notification push.</span><span class="sxs-lookup"><span data-stu-id="c4f5d-106">If you do not use hello downloaded quick start server project, you need hello push notification extension package.</span></span> <span data-ttu-id="c4f5d-107">Pour plus d’informations, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="c4f5d-107">For more information, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4f5d-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c4f5d-108">Prerequisites</span></span>
<span data-ttu-id="c4f5d-109">Éléments de hello suivants sont nécessaires :</span><span class="sxs-lookup"><span data-stu-id="c4f5d-109">You need hello following:</span></span>

* <span data-ttu-id="c4f5d-110">Un IDE, en fonction du serveur principal de votre projet :</span><span class="sxs-lookup"><span data-stu-id="c4f5d-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="c4f5d-111">[Android Studio](https://developer.android.com/sdk/index.html) si cette application a un serveur principal Node.js.</span><span class="sxs-lookup"><span data-stu-id="c4f5d-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="c4f5d-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) ou version ultérieure si cette application a un serveur principal .NET Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c4f5d-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="c4f5d-113">Android 2.3 ou version ultérieure, Révision du référentiel Google 27 ou version ultérieure et Services Google Play 9.0.2 ou version ultérieure pour Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="c4f5d-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="c4f5d-114">Hello complète [Android démarrage rapide].</span><span class="sxs-lookup"><span data-stu-id="c4f5d-114">Complete hello [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="c4f5d-115">Créer un projet qui prend en charge Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="c4f5d-115">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="c4f5d-116">Configurer un hub de notification</span><span class="sxs-lookup"><span data-stu-id="c4f5d-116">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a><span data-ttu-id="c4f5d-117">Configurer des notifications push de toosend Azure</span><span class="sxs-lookup"><span data-stu-id="c4f5d-117">Configure Azure toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a><span data-ttu-id="c4f5d-118">Activer les notifications push pour le projet de serveur hello</span><span class="sxs-lookup"><span data-stu-id="c4f5d-118">Enable push notifications for hello server project</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a><span data-ttu-id="c4f5d-119">Ajouter une application de tooyour de notifications push</span><span class="sxs-lookup"><span data-stu-id="c4f5d-119">Add push notifications tooyour app</span></span>
<span data-ttu-id="c4f5d-120">Dans cette section, vous mettez à jour vos notifications de push toohandle client application Android.</span><span class="sxs-lookup"><span data-stu-id="c4f5d-120">In this section, you update your client Android app toohandle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="c4f5d-121">Vérification de la version du Kit de développement logiciel (SDK) Android</span><span class="sxs-lookup"><span data-stu-id="c4f5d-121">Verify Android SDK version</span></span>
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="c4f5d-122">L’étape suivante consiste aux services Google Play tooinstall.</span><span class="sxs-lookup"><span data-stu-id="c4f5d-122">Your next step is tooinstall Google Play services.</span></span> <span data-ttu-id="c4f5d-123">Messagerie Cloud Google a certaines exigences minimales de niveau API pour le développement et de test, le hello **minSdkVersion** propriété dans le manifeste de hello doit respecter.</span><span class="sxs-lookup"><span data-stu-id="c4f5d-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which hello **minSdkVersion** property in hello manifest must conform to.</span></span>

<span data-ttu-id="c4f5d-124">Si vous testez avec un périphérique plus ancien, consultez [définir des Google Play Services SDK] toodetermine basse comment vous pouvez définir cette valeur et définir de manière appropriée.</span><span class="sxs-lookup"><span data-stu-id="c4f5d-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] toodetermine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-google-play-services-toohello-project"></a><span data-ttu-id="c4f5d-125">Ajouter un projet de toohello services Google Play</span><span class="sxs-lookup"><span data-stu-id="c4f5d-125">Add Google Play services toohello project</span></span>
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a><span data-ttu-id="c4f5d-126">Ajout de code</span><span class="sxs-lookup"><span data-stu-id="c4f5d-126">Add code</span></span>
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a><span data-ttu-id="c4f5d-127">Application de test de hello contre hello publié service mobile</span><span class="sxs-lookup"><span data-stu-id="c4f5d-127">Test hello app against hello published mobile service</span></span>
<span data-ttu-id="c4f5d-128">Vous pouvez tester application hello par attachement d’un téléphone Android avec un câble USB directement ou à l’aide d’un périphérique virtuel dans l’émulateur de hello.</span><span class="sxs-lookup"><span data-stu-id="c4f5d-128">You can test hello app by directly attaching an Android phone with a USB cable, or by using a virtual device in hello emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4f5d-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c4f5d-129">Next steps</span></span>
<span data-ttu-id="c4f5d-130">Maintenant que vous terminé ce didacticiel, pensez à poursuivre sur tooone Hello suivant didacticiels :</span><span class="sxs-lookup"><span data-stu-id="c4f5d-130">Now that you completed this tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* <span data-ttu-id="c4f5d-131">[Ajouter une application Android de l’authentification tooyour](app-service-mobile-android-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="c4f5d-131">[Add authentication tooyour Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="c4f5d-132">Découvrez comment tooadd authentification toohello todolist quickstart project sur Android à l’aide d’un fournisseur d’identité pris en charge.</span><span class="sxs-lookup"><span data-stu-id="c4f5d-132">Learn how tooadd authentication toohello todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="c4f5d-133">[Activation de la synchronisation hors connexion pour votre application Android](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="c4f5d-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="c4f5d-134">Découvrez comment tooadd hors connexion prennent en charge tooyour application à l’aide d’un principal des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="c4f5d-134">Learn how tooadd offline support tooyour app by using a Mobile Apps back end.</span></span> <span data-ttu-id="c4f5d-135">La synchronisation hors connexion permet aux utilisateurs d’interagir avec une application mobile &mdash;pour afficher, ajouter ou modifier des données&mdash;, même lorsqu’il n’existe aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="c4f5d-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
[Android démarrage rapide]: app-service-mobile-android-get-started.md

[définir des Google Play Services SDK]:https://developers.google.com/android/guides/setup
