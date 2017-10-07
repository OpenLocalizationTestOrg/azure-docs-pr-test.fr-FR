---
title: application de Xamarin.Android aaaAdd push notifications tooyour | Documents Microsoft
description: "Découvrez comment toouse du Service d’applications Azure et Azure Notification Hubs toosend push notifications tooyour Xamarin.Android application"
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
ms.openlocfilehash: c93d1d0cae06ab15e3e3e5c4b342808b2cd49113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-xamarinandroid-app"></a>Ajouter une application de Xamarin.Android de tooyour de notifications push
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Vue d'ensemble
Dans ce didacticiel, vous allez ajouter toohello de notifications push [démarrage rapide de Xamarin.Android](app-service-mobile-windows-store-dotnet-get-started.md) de projet afin qu’une notification push est envoyée toohello périphérique chaque fois qu’un enregistrement est inséré.

Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez serez hello package d’extension de notification push. Consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) pour plus d’informations.

## <a name="prerequisites"></a>Composants requis
Ce didacticiel requiert hello qui suit :

* Un compte Google actif. Vous pouvez vous connecter à un compte Google sur [accounts.google.com](http://go.microsoft.com/fwlink/p/?LinkId=268302).
* Le composant client [Google Cloud Messaging](http://components.xamarin.com/view/GCMClient/).

## <a name="configure-hub"></a>Configurer un nouveau hub de notification
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a id="register"></a>Activation de Firebase Cloud Messaging
[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

## <a name="configure-azure-toosend-push-requests"></a>Configurer les demandes de transmission toosend Azure
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push-for-firebase.md)]

## <a id="update-server"></a>Mettre à jour des notifications push de hello serveur projet toosend
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a id="configure-app"></a>Configurer le projet de client hello pour les notifications push
[!INCLUDE [mobile-services-xamarin-android-push-configure-project](../../includes/mobile-services-xamarin-android-push-configure-project.md)]

## <a id="add-push"></a>Ajouter une application de tooyour de code de notifications push
[!INCLUDE [app-service-mobile-xamarin-android-push-add-to-app](../../includes/app-service-mobile-xamarin-android-push-add-to-app.md)]

## <a name="test"></a>Tester les notifications push dans votre application
Vous pouvez tester l’application hello à l’aide d’un périphérique virtuel dans l’émulateur de hello. Des étapes de configuration supplémentaires sont requises lors de l’exécution sur un émulateur.

1. Assurez-vous que vous déployez tooor débogage sur un périphérique virtuel qui a APIs Google définir comme cible de hello, comme indiqué ci-dessous dans le Gestionnaire de périphériques virtuels Android (AVD) hello.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/google-apis-avd-settings.png)
2. Ajouter un appareil Android de Google compte toohello en cliquant sur **applications** > **paramètres** > **Ajouter compte**, puis suivez les invites hello.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/add-google-account.png)
3. Exécutez hello d’application todolist comme avant et insérer un nouvel élément de tâche. Cette fois-ci, une icône de notification s’affiche dans la zone de notification hello. Vous pouvez ouvrir hello notification tiroir tooview hello texte intégral de la notification de hello.
   
    ![](./media/app-service-mobile-xamarin-android-get-started-push/android-notifications.png)

<!-- URLs. -->
[Xamarin.Android quick start]: app-service-mobile-xamarin-android-get-started.md
[Google Cloud Messaging Client Component]: http://components.xamarin.com/view/GCMClient/
[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
