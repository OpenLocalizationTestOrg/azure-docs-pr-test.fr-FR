---
title: "aaaAzure intégration du Kit de développement logiciel Android Mobile Engagement"
description: "Dernières mises à jour et procédures du SDK Android pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d72b5014-a22b-4a7f-a470-d2b8145b5b86
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/10/2016
ms.author: piyushjo
ms.openlocfilehash: e81230cbc99a209f2909cc163c4e566df67dc828
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-gcm-with-mobile-engagement"></a>Comment tooIntegrate GCM avec Mobile Engagement
> [!IMPORTANT]
> Vous devez suivre la procédure d’intégration hello décrite dans hello comment tooIntegrate Engagement sur Android document avant de suivre ce guide.
> 
> Ce document est utile uniquement si vous déjà intégré hello atteindre toopush module et le plan de Google Play périphériques. toointegrate couvertures campagne dans votre application, lisez d’abord comment tooIntegrate Engagement atteindre sur Android.
> 
> 

## <a name="introduction"></a>Introduction
Intégration GCM permet à votre toobe application envoyée.

Charges utiles GCM envoyées toohello SDK toujours contient hello `azme` clé dans l’objet de données hello. Donc si vous utilisez GCM à d’autres fins dans votre application, vous pouvez filtrer les notifications Push en fonction de cette clé.

> [!IMPORTANT]
> Seuls les appareils disposant d’Android 2.2 ou version ultérieure, de Google Play et d’une connexion d’arrière-plan à Google peuvent faire l’objet d’une notification Push à l’aide de GCM. Toutefois, vous pouvez intégrer ce code en toute sécurité sur les appareils non pris en charge (car il utilise uniquement des intentions).
> 
> 

## <a name="create-a-google-cloud-messaging-project-with-api-key"></a>Créer un projet Google Cloud Messaging avec une clé API
[!INCLUDE [mobile-engagement-enable-Google-cloud-messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

## <a name="sdk-integration"></a>Intégration du SDK
### <a name="managing-device-registrations"></a>Gestion des inscriptions des appareils
Chaque appareil doit envoyer un toohello de commande d’inscription des serveurs de Google, sinon ils ne peuvent pas être atteint.

Un périphérique peut également annuler l’inscription de notifications GCM (appareil de hello est automatiquement annulée si la désinstallation de l’application hello).

Si vous n’utilisez pas [SDK de Google Play] ou vous ne déjà envoyer intention de l’inscription de hello vous-même, vous pouvez apporter Engagement inscrire les appareils hello automatiquement pour vous.

tooenable, ajouter hello suivant tooyour `AndroidManifest.xml` fichier, à l’intérieur de hello `<application/>` balise :

            <!-- If only 1 sender, don't forget hello \n, otherwise it will be parsed as a negative number... -->
            <meta-data android:name="engagement:gcm:sender" android:value="<Your Google Project Number>\n" />

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>Service de Push de l’Engagement d’enregistrement id toohello de communiquer et de recevoir des notifications
Dans l’ordre toocommunicate hello l’id d’inscription de toohello de périphérique hello Engagement Push du service et recevoir ses notifications, ajouter hello suivant tooyour `AndroidManifest.xml` fichier, à l’intérieur de hello `<application/>` balise (même si vous gérez vous-même inscriptions d’appareils) :

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
              android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
              </intent-filter>
            </receiver>

            <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
              <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<your_package_name>" />
              </intent-filter>
            </receiver>

Assurez-vous d’avoir hello suivant des autorisations dans votre `AndroidManifest.xml` (après hello `</application>` balise).

            <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
            <uses-permission android:name="<your_package_name>.permission.C2D_MESSAGE" />
            <permission android:name="<your_package_name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

## <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>Grant Mobile Engagement accès tooyour clé API GCM
Suivez [ce guide](mobile-engagement-android-get-started.md#grant-mobile-engagement-access-to-your-gcm-api-key) toogrant Mobile Engagement accès tooyour clé API GCM.

[SDK de Google Play]:https://developers.google.com/cloud-messaging/android/start
