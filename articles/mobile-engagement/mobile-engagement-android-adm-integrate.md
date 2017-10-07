---
title: "aaaAzure intégration du Kit de développement logiciel Android Mobile Engagement"
description: "Dernières mises à jour et procédures du SDK Android pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a7d719ec-67b3-4be3-9d7f-0b61a57fe978
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c57132ff49cf8c335627a72b37f9b78529e84f48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-adm-with-engagement"></a>Comment tooIntegrate ADM avec Engagement
> [!IMPORTANT]
> Vous devez suivre la procédure d’intégration hello décrite dans hello comment tooIntegrate Engagement sur Android document avant de suivre ce guide.
> 
> Ce document est utile uniquement si vous hello portée module plan toopush Amazon des appareils et déjà intégré. toointegrate couvertures campagne dans votre application, lisez d’abord comment tooIntegrate Engagement atteindre sur Android.
> 
> 

## <a name="introduction"></a>Introduction
Intégration ADM permet à votre toobe application envoyée lors du ciblage des appareils Amazon Android.

Charges utiles ADM envoyées toohello SDK toujours contient hello `azme` clé dans l’objet de données hello. Donc si vous utilisez ADM à d’autres fins dans votre application, vous pouvez filtrer les notifications push en fonction de cette clé.

> [!IMPORTANT]
> Seuls les appareils Amazon Kindle exécutant Android 4.0.3 ou version ultérieure sont pris en charge par Amazon Device Messaging. Vous pouvez toutefois intégrer ce code en toute sécurité sur d'autres appareils.
> 
> 

## <a name="sign-up-tooadm"></a>S’inscrire tooADM
Si vous ne l'avez pas déjà fait, vous devez activer ADM sur votre compte Amazon.

procédure de Hello est détaillée sur : [ <https://developer.amazon.com/sdk/adm/credentials.html>].

Une fois la procédure de hello, vous obtenez :

* OAuth informations d’identification (un ID Client et une clé secrète Client) pour toopush de Engagement toobe en mesure de vos appareils.
* Une clé d'API qui doit être intégrée à votre application.

## <a name="sdk-integration"></a>Intégration du SDK
### <a name="managing-device-registrations"></a>Gestion des inscriptions des appareils
Chaque appareil doit envoyer un toohello de commande d’inscription des serveurs ADM, sinon ils ne peuvent pas être atteint.

Si vous utilisez déjà hello [bibliothèque cliente ADM]et vous avez déjà [intégré ADM] vous pouvez directement accéder à recevoir de tooandroid-sdk-adm.

Si vous n’avez pas intégré ADM, Engagement a un tooenable de façon plus simple dans votre application :

Modifiez le fichier `AndroidManifest.xml` :

* Ajoutez hello Amazon espace de noms, le fichier de hello doit commencer comme suit :
  
      <?xml version="1.0" encoding="utf-8"?>
      <manifest xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:amazon="http://schemas.amazon.com/apk/res/android"
* À l’intérieur hello `<application/>` , ajoutez cette section :
  
      <amazon:enable-feature
         android:name="com.amazon.device.messaging"
         android:required="false"/>
  
      <meta-data android:name="engagement:adm:register" android:value="true" />
* Après avoir ajouté la balise d’amazon hello, vous avez peut-être une erreur de build si votre cible de Build de projet est sous Android 2.1. Vous avez toouse un **Android 2.1 +** cible de génération (ne vous inquiétez pas, vous pouvez toujours avoir un `minSdkVersion` définir too4).
* Intégrer hello ADM clé d’API comme un élément multimédia en suivant [cette procédure].

Suivez ensuite les instructions hello des sections suivantes de hello.

### <a name="communicate-registration-id-toohello-engagement-push-service-and-receive-notifications"></a>Service de Push de l’Engagement d’enregistrement id toohello de communiquer et de recevoir des notifications
Dans l’ordre toocommunicate hello l’id d’inscription de toohello de périphérique hello Engagement Push du service et recevoir ses notifications, ajouter hello suivant tooyour `AndroidManifest.xml` fichier, à l’intérieur de hello `<application/>` balise (même si vous utilisez ADM sans Engagement) :

        <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMEnabler"
          android:exported="false">
          <intent-filter>
            <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT"/>
          </intent-filter>
        </receiver>

         <receiver android:name="com.microsoft.azure.engagement.adm.EngagementADMReceiver"
           android:permission="com.amazon.device.messaging.permission.SEND">
          <intent-filter>
            <action android:name="com.amazon.device.messaging.intent.REGISTRATION"/>
            <action android:name="com.amazon.device.messaging.intent.RECEIVE"/>
            <category android:name="<your_package_name>"/>
          </intent-filter>
        </receiver>   

Assurez-vous d’avoir hello suivant des autorisations dans votre `AndroidManifest.xml` (avant hello `</application>` balise).

        <uses-permission android:name="android.permission.WAKE_LOCK"/>
        <uses-permission android:name="com.amazon.device.messaging.permission.RECEIVE"/>
        <uses-permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE"/>
        <permission android:name="<your_package_name>.permission.RECEIVE_ADM_MESSAGE" android:protectionLevel="signature"/>

## <a name="grant-engagement-oauth-credentials"></a>Accorder à Engagement des informations d'identification OAuth
Envoyez vos informations d’identification OAuth (ID client et clé secrète client) sur le portail Engagement.

[&lt;https://developer.amazon.com/sdk/adm/credentials.html&gt;]:https://developer.amazon.com/sdk/adm/credentials.html
[bibliothèque cliente ADM]:https://developer.amazon.com/sdk/adm/setup.html
[intégré ADM]:https://developer.amazon.com/sdk/adm/integrating-app.html
[cette procédure]:https://developer.amazon.com/sdk/adm/integrating-app.html#Asset
