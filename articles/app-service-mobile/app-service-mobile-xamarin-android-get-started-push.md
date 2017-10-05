---
title: "Ajout de notifications Push à votre application Xamarin.Android | Microsoft Docs"
description: "Découvrez comment utiliser Azure App Service et Azure Notification Hubs pour envoyer des notifications Push à votre application Xamarin Android."
services: app-service\mobile
documentationcenter: xamarin
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6f7e8517-e532-4559-9b07-874115f4c65b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: c3757d56fb1792092710740dc5ffbd64f18730cf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="add-push-notifications-to-your-xamarinandroid-app"></a><span data-ttu-id="29c86-103">Ajouter des notifications push à votre application Xamarin.Android</span><span class="sxs-lookup"><span data-stu-id="29c86-103">Add push notifications to your Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="29c86-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="29c86-104">Overview</span></span>
<span data-ttu-id="29c86-105">Dans ce didacticiel, vous ajoutez des notifications Push au projet [Démarrage rapide Xamarin.Android](app-service-mobile-windows-store-dotnet-get-started.md) afin qu'une notification Push soit envoyée chaque fois qu'un enregistrement est inséré.</span><span class="sxs-lookup"><span data-stu-id="29c86-105">In this tutorial, you add push notifications to the [Xamarin.Android quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent to the device every time a record is inserted.</span></span>

<span data-ttu-id="29c86-106">Si vous n’utilisez pas le projet de serveur du démarrage rapide téléchargé, vous devrez ajouter le package d’extension de notification Push.</span><span class="sxs-lookup"><span data-stu-id="29c86-106">If you do not use the downloaded quick start server project, you will need the push notification extension package.</span></span> <span data-ttu-id="29c86-107">Consultez [Fonctionnement avec le Kit de développement logiciel (SDK) du serveur principal .NET pour Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="29c86-107">See [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29c86-108">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="29c86-108">Prerequisites</span></span>
<span data-ttu-id="29c86-109">Ce didacticiel requiert les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="29c86-109">This tutorial requires the following:</span></span>

* <span data-ttu-id="29c86-110">Un compte Google actif.</span><span class="sxs-lookup"><span data-stu-id="29c86-110">An active Google account.</span></span> <span data-ttu-id="29c86-111">Vous pouvez vous connecter à un compte Google sur [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span><span class="sxs-lookup"><span data-stu-id="29c86-111">You can sign up for a Google account at [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).</span></span>
* <span data-ttu-id="29c86-112">Le composant client [Google Cloud Messaging](http://components.xamarin.com/view/GCMClient/).</span><span class="sxs-lookup"><span data-stu-id="29c86-112">[Google Cloud Messaging Client Component](http://components.xamarin.com/view/GCMClient/).</span></span>

## <span data-ttu-id="29c86-113"><a name="configure-hub"></a>Configurer un nouveau hub de notification</span><span class="sxs-lookup"><span data-stu-id="29c86-113"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <span data-ttu-id="29c86-114"><a id="register"></a>Activation de Firebase Cloud Messaging</span><span class="sxs-lookup"><span data-stu-id="29c86-114"><a id="register"></a>Enable Firebase Cloud Messaging</span></span>
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-to-send-push-requests"></a><span data-ttu-id="29c86-115">Configuration d’Azure pour l’envoi de demandes push</span><span class="sxs-lookup"><span data-stu-id="29c86-115">Configure Azure to send push requests</span></span>
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <span data-ttu-id="29c86-116"><a id="update-server"></a>Mettre à jour le projet de serveur pour l’envoi de notifications Push</span><span class="sxs-lookup"><span data-stu-id="29c86-116"><a id="update-server"></a>Update the server project to send push notifications</span></span>
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <span data-ttu-id="29c86-117"><a id="configure-app"></a>Configurer le projet client pour les notifications push</span><span class="sxs-lookup"><span data-stu-id="29c86-117"><a id="configure-app"></a>Configure the client project for push notifications</span></span>
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <span data-ttu-id="29c86-118"><a id="add-push"></a>Ajouter le code des notifications push à votre application</span><span class="sxs-lookup"><span data-stu-id="29c86-118"><a id="add-push"></a>Add push notifications code to your app</span></span>
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <span data-ttu-id="29c86-119"><a name="test"></a>Tester les notifications push dans votre application</span><span class="sxs-lookup"><span data-stu-id="29c86-119"><a name="test"></a>Test push notifications in your app</span></span>
<span data-ttu-id="29c86-120">Vous pouvez tester l’application à l’aide d’un appareil virtuel dans l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="29c86-120">You can test the app by using a virtual device in the emulator.</span></span> <span data-ttu-id="29c86-121">Des étapes de configuration supplémentaires sont requises lors de l’exécution sur un émulateur.</span><span class="sxs-lookup"><span data-stu-id="29c86-121">There are additional configuration steps required when running on an emulator.</span></span>

1. <span data-ttu-id="29c86-122">Assurez-vous de procéder au déploiement ou au débogage sur un périphérique virtuel sur lequel les API Google sont définis comme cible, comme indiqué dans le Gestionnaire d’appareil virtuel Android (AVD).</span><span class="sxs-lookup"><span data-stu-id="29c86-122">Make sure that you are deploying to or debugging on a virtual device that has Google APIs set as the target, as shown below in the Android Virtual Device (AVD) manager.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. <span data-ttu-id="29c86-123">Ajouter un compte Google à l’appareil Android en cliquant sur **Applications** > **Paramètres** > **Ajouter un compte**, puis suivez les invites.</span><span class="sxs-lookup"><span data-stu-id="29c86-123">Add a Google account to the Android device by clicking **Apps** > **Settings** > **Add account**, then follow the prompts.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. <span data-ttu-id="29c86-124">Exécutez normalement l’application todolist et insérez un nouvel élément todo.</span><span class="sxs-lookup"><span data-stu-id="29c86-124">Run the todolist app as before and insert a new todo item.</span></span> <span data-ttu-id="29c86-125">Cette fois, une icône de notification s’affiche dans la zone de notification.</span><span class="sxs-lookup"><span data-stu-id="29c86-125">This time, a notification icon is displayed in the notification area.</span></span> <span data-ttu-id="29c86-126">Vous pouvez ouvrir le tiroir de notification pour afficher le texte intégral de la notification.</span><span class="sxs-lookup"><span data-stu-id="29c86-126">You can open the notification drawer to view the full text of the notification.</span></span>
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
