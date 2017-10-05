---
title: "Ajout de notifications Push à votre application Android à l’aide de Mobile Apps | Microsoft Docs"
description: "Découvrez comment utiliser Mobile Apps pour envoyer des notifications Push à votre application Android."
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
ms.openlocfilehash: b89e9af55342d5d7473d848956996f846250b4b5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-android-app"></a><span data-ttu-id="63304-103">Ajout de notifications Push à votre application Android</span><span class="sxs-lookup"><span data-stu-id="63304-103">Add push notifications to your Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="63304-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="63304-104">Overview</span></span>
<span data-ttu-id="63304-105">Dans ce didacticiel, vous ajoutez des notifications Push au projet [Démarrage rapide Android] afin qu'une notification Push soit envoyée chaque fois qu'un enregistrement est inséré.</span><span class="sxs-lookup"><span data-stu-id="63304-105">In this tutorial, you add push notifications to the [Android quick start] project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="63304-106">Si vous n’utilisez pas le projet de serveur du démarrage rapide téléchargé, vous devrez ajouter le package d’extension de notification Push.</span><span class="sxs-lookup"><span data-stu-id="63304-106">If you do not use the downloaded quick start server project, you need the push notification extension package.</span></span> <span data-ttu-id="63304-107">Consultez [Fonctionnement avec le Kit de développement logiciel (SDK) du serveur principal .NET pour Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="63304-107">For more information, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63304-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="63304-108">Prerequisites</span></span>
<span data-ttu-id="63304-109">Vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="63304-109">You need the following:</span></span>

* <span data-ttu-id="63304-110">Un IDE, en fonction du serveur principal de votre projet :</span><span class="sxs-lookup"><span data-stu-id="63304-110">An IDE, depending on your project's back end:</span></span>

  * <span data-ttu-id="63304-111">[Android Studio](https://developer.android.com/sdk/index.html) si cette application a un serveur principal Node.js.</span><span class="sxs-lookup"><span data-stu-id="63304-111">[Android Studio](https://developer.android.com/sdk/index.html) if this app has a Node.js back end.</span></span>
  * <span data-ttu-id="63304-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) ou version ultérieure si cette application a un serveur principal .NET Microsoft.</span><span class="sxs-lookup"><span data-stu-id="63304-112">[Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) or later if this app has a Microsoft .NET back end.</span></span>
* <span data-ttu-id="63304-113">Android 2.3 ou version ultérieure, Révision du référentiel Google 27 ou version ultérieure et Services Google Play 9.0.2 ou version ultérieure pour Firebase Cloud Messaging.</span><span class="sxs-lookup"><span data-stu-id="63304-113">Android 2.3 or later, Google Repository revision 27 or later, and Google Play Services 9.0.2 or later for Firebase Cloud Messaging.</span></span>
* <span data-ttu-id="63304-114">Terminer le [Démarrage rapide Android].</span><span class="sxs-lookup"><span data-stu-id="63304-114">Complete the [Android quick start].</span></span>

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a><span data-ttu-id="63304-115">Créer un projet qui prend en charge Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="63304-115">Create a project that supports Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a><span data-ttu-id="63304-116">Configurer un hub de notification</span><span class="sxs-lookup"><span data-stu-id="63304-116">Configure a notification hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-to-send-push-notifications"></a><span data-ttu-id="63304-117">Configurer Azure pour l’envoi de notifications Push</span><span class="sxs-lookup"><span data-stu-id="63304-117">Configure Azure to send push notifications</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-the-server-project"></a><span data-ttu-id="63304-118">Activation des notifications push pour le projet de serveur</span><span class="sxs-lookup"><span data-stu-id="63304-118">Enable push notifications for the server project</span></span>
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-to-your-app"></a><span data-ttu-id="63304-119">Ajout de notifications Push à votre application</span><span class="sxs-lookup"><span data-stu-id="63304-119">Add push notifications to your app</span></span>
<span data-ttu-id="63304-120">Dans cette section, vous mettez à jour votre application Android client pour gérer les notifications push.</span><span class="sxs-lookup"><span data-stu-id="63304-120">In this section, you update your client Android app to handle push notifications.</span></span>

### <a name="verify-android-sdk-version"></a><span data-ttu-id="63304-121">Vérification de la version du Kit de développement logiciel (SDK) Android</span><span class="sxs-lookup"><span data-stu-id="63304-121">Verify Android SDK version</span></span>
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

<span data-ttu-id="63304-122">L'étape suivante consiste à installer les services Google Play.</span><span class="sxs-lookup"><span data-stu-id="63304-122">Your next step is to install Google Play services.</span></span> <span data-ttu-id="63304-123">Google Cloud Messaging a des spécifications requises d’API minimales pour le développement et les tests, auxquelles la propriété **minSdkVersion** du manifeste doit se conformer.</span><span class="sxs-lookup"><span data-stu-id="63304-123">Google Cloud Messaging has some minimum API level requirements for development and testing, which the **minSdkVersion** property in the manifest must conform to.</span></span>

<span data-ttu-id="63304-124">Si vous procédez à un test avec un appareil ancien, consultez la rubrique [Configuration du Kit de développement logiciel (SDK) des services Google Play] pour déterminer comment définir cette valeur.</span><span class="sxs-lookup"><span data-stu-id="63304-124">If you are testing with an older device, consult [Set Up Google Play Services SDK] to determine how low you can set this value, and set it appropriately.</span></span>

### <a name="add-google-play-services-to-the-project"></a><span data-ttu-id="63304-125">Ajout de services Google Play au projet</span><span class="sxs-lookup"><span data-stu-id="63304-125">Add Google Play services to the project</span></span>
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a><span data-ttu-id="63304-126">Ajout de code</span><span class="sxs-lookup"><span data-stu-id="63304-126">Add code</span></span>
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-the-app-against-the-published-mobile-service"></a><span data-ttu-id="63304-127">Test de l'application avec le service mobile publié</span><span class="sxs-lookup"><span data-stu-id="63304-127">Test the app against the published mobile service</span></span>
<span data-ttu-id="63304-128">Vous pouvez tester l’application en connectant directement un téléphone Android via un câble USB, ou en utilisant un appareil virtuel dans l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="63304-128">You can test the app by directly attaching an Android phone with a USB cable, or by using a virtual device in the emulator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63304-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="63304-129">Next steps</span></span>
<span data-ttu-id="63304-130">Maintenant que vous avez terminé ce didacticiel, vous pouvez passer à l’un des didacticiels suivants :</span><span class="sxs-lookup"><span data-stu-id="63304-130">Now that you completed this tutorial, consider continuing on to one of the following tutorials:</span></span>

* <span data-ttu-id="63304-131">[Ajout de l’authentification à votre application Android](app-service-mobile-android-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="63304-131">[Add authentication to your Android app](app-service-mobile-android-get-started-users.md).</span></span>
  <span data-ttu-id="63304-132">Découvrez comment ajouter l’authentification au projet de démarrage rapide todolist sur Android en faisant appel à un fournisseur d’identité pris en charge.</span><span class="sxs-lookup"><span data-stu-id="63304-132">Learn how to add authentication to the todolist quickstart project on Android using a supported identity provider.</span></span>
* <span data-ttu-id="63304-133">[Activation de la synchronisation hors connexion pour votre application Android](app-service-mobile-android-get-started-offline-data.md).</span><span class="sxs-lookup"><span data-stu-id="63304-133">[Enable offline sync for your Android app](app-service-mobile-android-get-started-offline-data.md).</span></span>
  <span data-ttu-id="63304-134">Découvrez comment ajouter une prise en charge hors connexion à votre application à l’aide d’un serveur principal Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="63304-134">Learn how to add offline support to your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="63304-135">La synchronisation hors connexion permet aux utilisateurs d’interagir avec une application mobile &mdash;pour afficher, ajouter ou modifier des données&mdash;, même lorsqu’il n’existe aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="63304-135">With offline sync, users can interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- URLs -->
<span data-ttu-id="63304-136">[Démarrage rapide Android]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="63304-136">[Android quick start]: app-service-mobile-android-get-started.md</span></span>

<span data-ttu-id="63304-137">[Configuration du Kit de développement logiciel (SDK) des services Google Play]:https://developers.google.com/android/guides/setup</span><span class="sxs-lookup"><span data-stu-id="63304-137">[Set Up Google Play Services SDK]:https://developers.google.com/android/guides/setup</span></span>
