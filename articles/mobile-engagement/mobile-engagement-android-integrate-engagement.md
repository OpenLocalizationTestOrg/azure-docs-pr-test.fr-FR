---
title: "aaaAzure intégration du Kit de développement logiciel Android Mobile Engagement"
description: "Dernières mises à jour et procédures du SDK Android pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a5487793-1a12-4f6c-a1cf-587c5a671e6b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4f79936ea0fa6102023dec2b4682032a4a81fa9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-android"></a>Comment tooIntegrate Engagement sur Android
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
> 
> 

Cette procédure décrit Analytique et surveillance de votre application Android hello la plus simple façon tooactivate Engagement.

> [!IMPORTANT]
> Le niveau minimum de l'API SDK Android doit être égal ou supérieur à 10 (Android 2.3.3 ou version ultérieure).
> 
> 

Hello suit est que suffisamment rapport hello tooactivates journaux nécessaires toocompute toutes les statistiques concernant les utilisateurs, Sessions, activités, blocages et Technicals. rapport Hello de journaux nécessaires toocompute autres statistiques telles que les événements, les erreurs et les tâches doivent être effectués manuellement à l’aide des API de l’Engagement de hello (consultez [comment toouse hello avancé Mobile Engagement marquage API dans votre Android](mobile-engagement-android-use-engagement-api.md) depuis ces les statistiques sont dépend de l’application.

## <a name="embed-hello-engagement-sdk-and-service-into-your-android-project"></a>Incorporer hello Engagement SDK et service dans votre projet Android
Téléchargement hello du SDK Android à partir de [ici](https://aka.ms/vq9mfn) obtenir `mobile-engagement-VERSION.jar` et placez-les dans hello `libs` dossier de votre projet Android (créer le dossier de bibliothèques hello s’il n’existe pas encore).

> [!IMPORTANT]
> Si vous générez votre package d’application avec ProGuard, vous devez tookeep certaines classes. Vous pouvez utiliser hello suivant extrait de configuration :
> 
> -keep public class * extends android.os.IInterface -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
> 
> <methods>; }
> 
> 

Spécifiez votre chaîne de connexion Engagement en appelant hello suivant de méthode dans l’activité de lanceur hello :

            EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
            engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
            EngagementAgent.getInstance(this).init(engagementConfiguration);

chaîne de connexion Hello pour votre application s’affiche sur le portail Azure.

* Si manquant, ajouter hello Android autorisations suivantes (avant hello `<application>` étiquette) :
  
          <uses-permission android:name="android.permission.INTERNET"/>
          <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
* Ajouter hello après section (entre hello `<application>` et `</application>` balises) :
  
          <service
            android:name="com.microsoft.azure.engagement.service.EngagementService"
            android:exported="false"
            android:label="<Your application name>Service"
            android:process=":Engagement"/>
* Modification `<Your application name>` par nom hello de votre application.

> [!TIP]
> Hello `android:label` attribut permet de vous toochoose hello nom de service de l’Engagement de hello tel qu’il apparaîtra aux utilisateurs finaux toohello sur l’écran hello « Services en cours d’exécution » de leur téléphone. Il est recommandé de cet attribut tooset trop`"<Your application name>Service"` (par exemple, `"AcmeFunGameService"`).
> 
> 

En spécifiant hello `android:process` attribut garantit que ce service de l’Engagement hello s’exécute dans son propre processus (en cours d’exécution Engagement Bonjour même processus que votre application permettront à votre thread principal / l’interface utilisateur potentiellement moins sensible).

> [!NOTE]
> Tout code que vous placez dans `Application.onCreate()` et autres rappels de l’application seront exécutés pour les processus de tous les votre application, y compris le service d’Engagement hello. Elle peut avoir des effets secondaires indésirables (par exemple, les allocations de mémoire inutiles et les threads de processus, les récepteurs de diffusion en double ou les services d’Engagement hello).
> 
> 

Si vous substituez `Application.onCreate()`, il est hello tooadd recommandée suivante extrait de code au début de hello de votre `Application.onCreate()` fonction :

             public void onCreate()
             {
               if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
                 return;

               ... Your code...
             }

Vous pouvez effectuer hello même chose pour `Application.onTerminate()`, `Application.onLowMemory()` et `Application.onConfigurationChanged(...)`.

Vous pouvez également étendre `EngagementApplication` au lieu de l’extension `Application`: hello rappel `Application.onCreate()` hello vérification de processus et les appels `Application.onApplicationProcessCreate()` uniquement si le processus actuel de hello n’est pas hello un hello Engagement service d’hébergement, hello mêmes règles s’appliquent pour Bonjour autres rappels.

## <a name="basic-reporting"></a>Génération de rapports de base
### <a name="recommended-method-overload-your-activity-classes"></a>Méthode recommandée : surchargez vos classes `Activity`
Dans le rapport de hello order tooactivate de tous les journaux hello requis par Engagement toocompute utilisateurs, Sessions, activités, blocages et statistiques, il vous suffit toomake tous vos `*Activity` sous-classes héritent hello correspondant `Engagement*Activity` classes (par exemple, si votre activité hérité étend `ListActivity`, assurez-vous qu’il étend `EngagementListActivity`).

**Sans Engagement :**

            package com.company.myapp;

            import android.app.Activity;
            import android.os.Bundle;

            public class MyApp extends Activity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

**Avec Engagement :**

            package com.company.myapp;

            import com.microsoft.azure.engagement.activity.EngagementActivity;
            import android.os.Bundle;

            public class MyApp extends EngagementActivity
            {
              @Override
              public void onCreate(Bundle savedInstanceState)
              {
                super.onCreate(savedInstanceState);
                setContentView(R.layout.main);
              }
            }

> [!IMPORTANT]
> Lorsque vous utilisez `EngagementListActivity` ou `EngagementExpandableListActivity`, assurez-vous que tout appel trop`requestWindowFeature(...);` est effectuée avant l’appel de hello trop`super.onCreate(...);`, sinon un incident se produit.
> 
> 

Vous pouvez trouver ces classes Bonjour `src` dossier, puis les copier dans votre projet. classes de Hello figurent également dans hello **JavaDoc**.

### <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>Méthode alternative : appelez `startActivity()` et `endActivity()` manuellement
Si vous ne pouvez pas ou ne souhaitez pas que toooverload votre `Activity` classes, vous pouvez à la place de début et de fin de vos activités en appelant `EngagementAgent`de méthodes directement.

> [!IMPORTANT]
> Hello du SDK Android n’appelle jamais hello `endActivity()` méthode, même lorsque l’application hello est fermée (sur Android, les applications sont en fait jamais fermées). Par conséquent, il est *hautement* recommandé toocall hello `startActivity()` méthode Bonjour `onResume` rappel de *tous les* vos activités et hello `endActivity()` méthode Bonjour `onPause()` rappel de *tous les* vos activités. Il s’agit de toobe moyen hello uniquement assurer que les sessions ne seront pas divulguées. Si une session est perdue, hello service d’Engagement sera déconnecté jamais hello Engagement principal (étant donné que le service de hello reste connecté en tant qu’une session est en attente).
> 
> 

Voici un exemple :

            public class MyActivity extends Some3rdPartyActivity
            {
              @Override
              protected void onResume()
              {
                super.onResume();
                String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at hello end.
                EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
              }

              @Override
              protected void onPause()
              {
                super.onPause();
                EngagementAgent.getInstance(this).endActivity();
              }
            }

Cette toohello très similaire exemple `EngagementActivity` classe et ses variantes, dont le code source est fourni dans hello `src` dossier.

## <a name="test"></a>Test
Veuillez vérifier maintenant votre intégration en exécutant votre application mobile dans un émulateur ou un appareil et en vérifiant qu’il enregistre une session sur l’onglet de surveillance hello.

les sections suivantes Hello sont facultatifs.

## <a name="location-reporting"></a>Rapports d'emplacement
Si vous souhaitez toobe emplacements signalé, vous devez tooadd quelques lignes de configuration (entre hello `<application>` et `</application>` balises).

### <a name="lazy-area-location-reporting"></a>Rapports d'emplacement de zone différé
Signalisation différée de zone emplacement permet tooreport hello pays, la région et localité associés toodevices. Ce type de rapport d'emplacement utilise uniquement des emplacements réseau (basés sur l'ID cellulaire ou le Wi-Fi). zone de Hello est signalée au maximum une fois par session. Hello GPS n’est jamais utilisé, et par conséquent, ce type de rapport de l’emplacement a très peu (pas toosay aucune) impact sur la batterie de hello.

Les zones signalés sont utilisés toocompute des statistiques géographique sur les utilisateurs, des sessions, des événements et des erreurs. Elles peuvent également servir de critère dans les couvertures campagne.

emplacement de la zone différée tooenable reporting, vous pouvez le faire à l’aide de configuration hello mentionnée précédemment dans cette procédure :

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setLazyAreaLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Vous devez également hello tooadd suivant l’autorisation si manquant :

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Ou vous pouvez continuer à utiliser ``ACCESS_FINE_LOCATION`` si vous l’utilisez déjà dans votre application.

### <a name="real-time-location-reporting"></a>Rapports d'emplacement en temps réel
Signalisation de l’emplacement en temps réel permet de latitude de hello tooreport et longitude associés toodevices. Par défaut, ce type d’emplacement reporting utilise uniquement des emplacements réseau (basés sur l’ID de la cellule ou Wi-Fi), et hello reporting est uniquement active lorsque l’application hello s’exécute en premier plan (par exemple, lors d’une session).

Les emplacements en temps réel sont *pas* utilisé toocompute statistiques. Leur utilisation de hello tooallow de délimitation géographique en temps réel ne sert que \<portée-public-géorepérage\> critère dans les campagnes Reach.

emplacement en temps réel du tooenable reporting, vous pouvez le faire à l’aide de configuration hello mentionnée précédemment dans cette procédure :

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Vous devez également hello tooadd suivant l’autorisation si manquant :

            <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

Ou vous pouvez continuer à utiliser ``ACCESS_FINE_LOCATION`` si vous l’utilisez déjà dans votre application.

#### <a name="gps-based-reporting"></a>Rapports GPS
Par défaut, le rapport d'emplacement en temps réel utilise uniquement des emplacements réseau. utiliser hello tooenable GPS en fonction des emplacements (qui sont beaucoup plus précises), utilisez l’objet de configuration hello :

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setFineRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

Vous devez également hello tooadd suivant l’autorisation si manquant :

            <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>

#### <a name="background-reporting"></a>Rapports en arrière-plan
Par défaut, reporting en temps réel sur l’emplacement est uniquement active lorsque l’application hello s’exécute en premier plan (par exemple, lors d’une session). hello tooenable reporting également en arrière-plan, utilisez hello configuration objet :

    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
    engagementConfiguration.setRealtimeLocationReport(true);
    engagementConfiguration.setBackgroundRealtimeLocationReport(true);
    EngagementAgent.getInstance(this).init(engagementConfiguration);

> [!NOTE]
> Lors de l’application hello s’exécute en arrière-plan, seuls les emplacements réseau sont signalées, même si vous avez activé hello GPS.
> 
> 

rapport d’emplacement Hello en arrière-plan sera arrêté si l’utilisateur de hello redémarre son appareil, vous pouvez ajouter cette toomake il redémarre automatiquement au moment du démarrage :

            <receiver android:name="com.microsoft.azure.engagement.EngagementLocationBootReceiver"
               android:exported="false">
               <intent-filter>
                  <action android:name="android.intent.action.BOOT_COMPLETED" />
               </intent-filter>
            </receiver>

Vous devez également hello tooadd suivant l’autorisation si manquant :

            <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />

### <a name="android-m-permissions"></a>Autorisations Android M
À partir d’Android M, certaines autorisations sont gérées lors de l’exécution et nécessitent une approbation de l’utilisateur.

autorisations d’exécution Hello seront désactivées par défaut pour les nouvelles installations de l’application si vous ciblez l’API Android de niveau 23. Sinon, elles seront activées par défaut.

utilisateur de Hello peut activer ou désactiver ces autorisations à partir du menu Paramètres de périphérique hello. Désactivation des autorisations à partir du menu système arrête les processus d’arrière-plan de l’application hello, ceci est un comportement du système et n’a aucun impact sur la capacité tooreceive par émission de données en arrière-plan.

Dans le contexte de hello de Mobile Engagement, autorisations hello qui requièrent une approbation lors de l’exécution sont :

* `ACCESS_COARSE_LOCATION`
* `ACCESS_FINE_LOCATION`
* `WRITE_EXTERNAL_STORAGE` (uniquement lors du ciblage de niveau d’API Android 23 pour cet élément)

un stockage externe Hello est utilisé uniquement pour la fonctionnalité de vue d’ensemble de portée. Si vous trouvez demandant aux utilisateurs de cette autorisation toobe interruption de service, vous pouvez le supprimer si vous l’avez utilisé seulement pour Mobile Engagement, mais au coût hello de désactiver la fonctionnalité de vue d’ensemble.

Pour les fonctionnalités d’emplacement hello, vous devez demander toouser d’autorisations à l’aide d’une boîte de dialogue système standard. Si l’utilisateur de hello approuve, vous devez tootell ``EngagementAgent`` tootake modifier en compte en temps réel (modification de hello sinon sera traité hello suivant temps hello utilisateur lance hello application).

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
         * Request location permission, but this won't explain why it is needed toohello user.
         * hello standard Android documentation explains with more details how toodisplay a rationale activity tooexplain hello user why hello permission is needed in your application.
         * Putting COARSE vs FINE has no impact here, they are part of hello same group for runtime permission management.
         */
        if (checkSelfPermission(android.Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.ACCESS_FINE_LOCATION }, 0);

        /* Only if you want tookeep features using external storage */
        if (checkSelfPermission(android.Manifest.permission.WRITE_EXTERNAL_STORAGE) != PackageManager.PERMISSION_GRANTED)
          requestPermissions(new String[] { android.Manifest.permission.WRITE_EXTERNAL_STORAGE }, 1);
      }
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, String[] permissions, int[] grantResults)
    {
      /* Only a positive location permission update requires engagement agent refresh, hence hello request code matching from above function */
      if (requestCode == 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED)
        getEngagementAgent().refreshPermissions();
    }

## <a name="advanced-reporting"></a>Génération de rapports avancés
Si vous le souhaitez, si vous souhaitez tooreport les événements d’application spécifique, les erreurs et les tâches, vous devez toouse hello Engagement API via les méthodes hello Hello `EngagementAgent` classe. Un objet de cette classe permettre être récupérés en appelant hello `EngagementAgent.getInstance()` méthode statique.

permet de toouse toutes les fonctionnalités avancées d’Engagement Hello Engagement API et est détaillée dans hello comment tooUse l’API d’Engagement sur Android (ainsi que dans la documentation technique de hello Hello `EngagementAgent` classe).

## <a name="advanced-configuration-in-androidmanifestxml"></a>Configuration avancée (dans AndroidManifest.xml)
### <a name="wake-locks"></a>Verrous d'activation
Si vous souhaitez toobe assurer que les statistiques sont envoyées en temps réel lors de l’utilisation du Wi-Fi ou dans l’écran hello est désactivé, ajoutez hello suivant autorisation facultatif :

            <uses-permission android:name="android.permission.WAKE_LOCK"/>

### <a name="crash-report"></a>Rapport d'incidents
Si vous souhaitez que les rapports d’incidents toodisable, ajoutez ceci (entre hello `<application>` et `</application>` balises) :

            <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>Seuil du mode rafale
Par défaut, les rapports de service d’Engagement hello journaux en temps réel. Si votre application rapports journaux très fréquemment, il est mieux toobuffer hello journaux et tooreport à la fois à une base de temps réguliers (appelée hello « mode de croissance »). toodo, ajoutez ceci (entre hello `<application>` et `</application>` balises) :

            <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

Hello mode rafale légèrement augmenter la batterie de hello vie mais n’a un impact sur hello Engagement moniteur : toutes les sessions et les travaux seront arrondies toohello rafale seuil (par conséquent, les sessions et les travaux plus court que le seuil de croissance hello n’est pas forcément visible). Il est recommandé de toouse un seuil de croissance n’est plus à 30000 (30 s).

### <a name="session-timeout"></a>Délai d'expiration de session
Par défaut, une session est 10 s terminée après la fin de hello de sa dernière activité (qui se produit en appuyant sur le hello accueil ou sauvegardez la clé, par définition téléphone hello inactif ou passer à une autre application généralement). Il s’agit de tooavoid un fractionnement de session chaque utilisateur hello quitter et revenir toohello application très rapidement (qui peut se produire lorsqu’il chercher une image, vérifier une notification, etc..). Vous souhaiterez toomodify ce paramètre. toodo, ajoutez ceci (entre hello `<application>` et `</application>` balises) :

            <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>Désactiver les rapports de suivi
### <a name="using-a-method-call"></a>En appelant une méthode
Si vous souhaitez toostop Engagement envoi de journaux, vous pouvez appeler :

            EngagementAgent.getInstance(context).setEnabled(false);

Cet appel est persistant : il utilise un fichier de préférences partagées.

Si l’Engagement est active lorsque vous appelez cette fonction, peut prendre une minute pour hello service toostop. Toutefois, il ne sera pas lancer service hello en hello tous les prochaine fois que vous lancez application hello.

Vous pouvez activer le journal de création de rapports en appelant hello même fonction avec `true`.

### <a name="integration-in-your-own-preferenceactivity"></a>Intégration dans votre propre `PreferenceActivity`
Au lieu d'appeler cette fonction, vous pouvez également intégrer ce paramètre directement dans votre `PreferenceActivity`.

Vous pouvez configurer toouse Engagement vos préférences de fichier (avec le mode souhaité de hello) de hello `AndroidManifest.xml` de fichiers avec `application meta-data`:

* Hello `engagement:agent:settings:name` clé désigne toodefine utilisé hello du fichier de préférences partagées hello.
* Hello `engagement:agent:settings:mode` clé est en mode de hello toodefine utilisé du fichier de préférences partagées hello, vous devez utiliser hello même mode comme dans votre `PreferenceActivity`. mode de Hello doit être passé en tant que nombre : Si vous utilisez une combinaison d’indicateurs de constantes dans votre code, vérifiez la valeur totale de hello.

Engagement de toujours utiliser hello `engagement:key` booléenne clé dans le fichier de préférences de hello pour gérer ce paramètre.

Hello selon l’exemple de `AndroidManifest.xml` affiche hello des valeurs par défaut :

            <application>
                [...]
                <meta-data
                  android:name="engagement:agent:settings:name"
                  android:value="engagement.agent" />
                <meta-data
                  android:name="engagement:agent:settings:mode"
                  android:value="0" />

Vous pouvez ensuite ajouter un `CheckBoxPreference` dans la disposition de préférence comme hello suivant un :

            <CheckBoxPreference
              android:key="engagement:enabled"
              android:defaultValue="true"
              android:title="Use Engagement"
              android:summaryOn="Engagement is enabled."
              android:summaryOff="Engagement is disabled." />

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
