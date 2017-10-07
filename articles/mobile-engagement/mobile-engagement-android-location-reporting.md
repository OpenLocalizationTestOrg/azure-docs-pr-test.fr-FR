---
title: aaaLocation Reporting pour Azure Mobile Engagement Android SDK
description: "Décrit comment emplacement tooconfigure reporting pour Azure Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6cab5ed1-b767-46ac-9f0b-48a4e249d88c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: c2cb097df2a77bee2d56ffe9509dc116548db408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="location-reporting-for-azure-mobile-engagement-android-sdk"></a>Génération de rapports d’emplacement pour le SDK Azure Mobile Engagement pour Android
> [!div class="op_single_selector"]
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Cette rubrique décrit comment emplacement toodo reporting pour votre application Android.

## <a name="prerequisites"></a>Composants requis
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="location-reporting"></a>Rapports d'emplacement
Si vous souhaitez toobe emplacements signalé, vous devez tooadd quelques lignes de configuration (entre hello `<application>` et `</application>` balises).

### <a name="lazy-area-location-reporting"></a>Rapports d'emplacement de zone différé
Signalisation différée de zone emplacement permet de pays hello déclarant, région et localité associées aux périphériques. Ce type de rapport d'emplacement utilise uniquement des emplacements réseau (basés sur l'ID cellulaire ou le Wi-Fi). zone de Hello est signalée au maximum une fois par session. Hello GPS n’est jamais utilisé, et par conséquent, ce type de rapport d’emplacement a un faible impact sur la batterie de hello.

Les zones signalées sont géographique de toocompute utilisé des statistiques sur les utilisateurs, les sessions, les événements et les erreurs. Elles peuvent également servir de critère dans les couvertures campagne.

Vous activez d’emplacement de la zone différée reporting à l’aide de configuration hello mentionnée précédemment dans cette procédure :

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Vous devez également toospecify une autorisation de l’emplacement. Ce code utilise l’autorisation ``COARSE`` :

    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Si votre application l’exige, vous pouvez utiliser ``ACCESS_FINE_LOCATION`` à la place.

### <a name="real-time-location-reporting"></a>Rapports d'emplacement en temps réel
Signalisation de l’emplacement en temps réel permet de création de rapports latitude de hello et la longitude associées aux périphériques. Par défaut, ce type de rapport d'emplacement utilise uniquement des emplacements réseau, basés sur l'ID cellulaire ou le Wi-Fi. Hello reporting est uniquement active lorsque l’application hello s’exécute en premier plan (par exemple, pendant une session).

Emplacements en temps réel sont *pas* utilisé toocompute statistiques. Leur utilisation de hello tooallow de délimitation géographique en temps réel ne sert que \<portée-public-géorepérage\> critère dans les campagnes Reach.

emplacement en temps réel de tooenable création de rapports, ajoutez une ligne de code toowhere permet de chaîne de connexion d’Engagement hello dans l’activité de lanceur hello. résultat de Hello ressemble à hello suivantes :

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

        You also need toospecify a location permission. This code uses ``COARSE`` permission:

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

        If your app requires it, you can use ``ACCESS_FINE_LOCATION`` instead.

#### <a name="gps-based-reporting"></a>Rapports GPS
Par défaut, le rapport d'emplacement en temps réel utilise uniquement des emplacements réseau. utiliser hello tooenable emplacements GPS, qui sont beaucoup plus précises, utiliser l’objet de configuration de hello :

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Vous devez également hello tooadd suivant l’autorisation si manquant :

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>Rapports en arrière-plan
Par défaut, reporting sur l’emplacement en temps réel est uniquement active lorsque l’application hello s’exécute en premier plan (par exemple, pendant une session). hello tooenable reporting également en arrière-plan, utilisez cet objet de configuration :

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> Lors de l’application hello s’exécute en arrière-plan, seuls les emplacements réseau sont signalées, même si vous avez activé hello GPS.
> 
> 

Si l’utilisateur de hello a redémarré à leur appareil, le rapport d’emplacement hello en arrière-plan est arrêté. toomake il redémarre automatiquement au moment du démarrage, ajoutez ce code.

    <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
           android:exported="false">
        <intent-filter>
            <action android:name="android.intent.action.BOOT_COMPLETED" />
        </intent-filter>
    </receiver>

Vous devez également hello tooadd suivant l’autorisation si manquant :

    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

## <a name="android-m-permissions"></a>Autorisations Android M
À partir d’Android M, certaines autorisations sont gérées lors de l’exécution et nécessitent une approbation de l’utilisateur.

Si vous ciblez Android API de niveau 23, les autorisations d’exécution hello sont désactivées par défaut pour les nouvelles installations de l’application. Sinon, elles sont activées par défaut.

Vous pouvez activer ou désactiver ces autorisations à partir du menu Paramètres de périphérique hello. Désactivation des autorisations à partir du menu du système hello arrête les processus d’arrière-plan hello d’application hello, qui est un comportement du système et n’a aucun impact sur la capacité tooreceive par émission de données en arrière-plan.

Dans le contexte de hello d’emplacement de Mobile Engagement reporting, les autorisations hello qui requièrent une approbation lors de l’exécution sont :

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`

Demander des autorisations d’utilisateur hello à l’aide d’une boîte de dialogue système standard. Si l’utilisateur de hello approuve, indiquer ``EngagementAgent`` tootake modifier en compte en temps réel. Dans le cas contraire les modifications hello sont traité hello suivant temps hello lance hello application d’utilisateur.

Voici une toouse d’exemple de code dans une activité de vos autorisations toorequest d’application et le résultat de hello vers l’avant si positif trop``EngagementAgent``:

    @Override
    public void onCreate(Bundle savedInstanceState)
    {
      /* Other code... */

      /* Request permissions */
      requestPermissions();
    }

    @TargetApi(Build.VERSION_CODES.M)
    private void requestPermissions()
    {
      /* Avoid crashing if not on Android M */
      if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M)
      {
        /*
         * Request location permission, but this doesn't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }
