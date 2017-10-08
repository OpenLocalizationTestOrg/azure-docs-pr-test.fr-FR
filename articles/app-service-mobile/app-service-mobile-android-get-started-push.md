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
# <a name="add-push-notifications-tooyour-android-app"></a>Ajouter l’application Android de tooyour de notifications push
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Vue d'ensemble
Dans ce didacticiel, vous allez ajouter toohello de notifications push [Android démarrage rapide] projet afin qu’une notification push est envoyée toohello périphérique chaque fois qu’un enregistrement est inséré.

Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez hello package d’extension de notification push. Pour plus d’informations, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="prerequisites"></a>Composants requis
Éléments de hello suivants sont nécessaires :

* Un IDE, en fonction du serveur principal de votre projet :

  * [Android Studio](https://developer.android.com/sdk/index.html) si cette application a un serveur principal Node.js.
  * [Visual Studio Community 2013](https://go.microsoft.com/fwLink/p/?LinkID=391934) ou version ultérieure si cette application a un serveur principal .NET Microsoft.
* Android 2.3 ou version ultérieure, Révision du référentiel Google 27 ou version ultérieure et Services Google Play 9.0.2 ou version ultérieure pour Firebase Cloud Messaging.
* Hello complète [Android démarrage rapide].

## <a name="create-a-project-that-supports-firebase-cloud-messaging"></a>Créer un projet qui prend en charge Firebase Cloud Messaging
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-a-notification-hub"></a>Configurer un hub de notification
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="configure-azure-toosend-push-notifications"></a>Configurer des notifications push de toosend Azure
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a name="enable-push-notifications-for-hello-server-project"></a>Activer les notifications push pour le projet de serveur hello
[!INCLUDE [app-service-mobile-dotnet-backend-configure-push-google](../../includes/app-service-mobile-dotnet-backend-configure-push-google.md)]

## <a name="add-push-notifications-tooyour-app"></a>Ajouter une application de tooyour de notifications push
Dans cette section, vous mettez à jour vos notifications de push toohandle client application Android.

### <a name="verify-android-sdk-version"></a>Vérification de la version du Kit de développement logiciel (SDK) Android
[!INCLUDE [app-service-mobile-verify-android-sdk-version](../../includes/app-service-mobile-verify-android-sdk-version.md)]

L’étape suivante consiste aux services Google Play tooinstall. Messagerie Cloud Google a certaines exigences minimales de niveau API pour le développement et de test, le hello **minSdkVersion** propriété dans le manifeste de hello doit respecter.

Si vous testez avec un périphérique plus ancien, consultez [définir des Google Play Services SDK] toodetermine basse comment vous pouvez définir cette valeur et définir de manière appropriée.

### <a name="add-google-play-services-toohello-project"></a>Ajouter un projet de toohello services Google Play
[!INCLUDE [Add Play Services](../../includes/app-service-mobile-add-google-play-services.md)]

### <a name="add-code"></a>Ajout de code
[!INCLUDE [app-service-mobile-android-getting-started-with-push](../../includes/app-service-mobile-android-getting-started-with-push.md)]

## <a name="test-hello-app-against-hello-published-mobile-service"></a>Application de test de hello contre hello publié service mobile
Vous pouvez tester application hello par attachement d’un téléphone Android avec un câble USB directement ou à l’aide d’un périphérique virtuel dans l’émulateur de hello.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous terminé ce didacticiel, pensez à poursuivre sur tooone Hello suivant didacticiels :

* [Ajouter une application Android de l’authentification tooyour](app-service-mobile-android-get-started-users.md).
  Découvrez comment tooadd authentification toohello todolist quickstart project sur Android à l’aide d’un fournisseur d’identité pris en charge.
* [Activation de la synchronisation hors connexion pour votre application Android](app-service-mobile-android-get-started-offline-data.md).
  Découvrez comment tooadd hors connexion prennent en charge tooyour application à l’aide d’un principal des applications mobiles. La synchronisation hors connexion permet aux utilisateurs d’interagir avec une application mobile &mdash;pour afficher, ajouter ou modifier des données&mdash;, même lorsqu’il n’existe aucune connexion réseau.

<!-- URLs -->
[Android démarrage rapide]: app-service-mobile-android-get-started.md

[définir des Google Play Services SDK]:https://developers.google.com/android/guides/setup
