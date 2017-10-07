---
title: "aaaAzure Mobile Engagement iOS intégration SDK | Documents Microsoft"
description: "Dernières mises à jour et procédures du Kit de développement logiciel (SDK) iOS pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 947ea44b-00c1-450f-9a3b-74437954dc56
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 66ce34efabede7d882caa8a91431a8df71e4fb59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-ios"></a>Comment tooIntegrate Engagement sur iOS
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
>
>

Cette procédure décrit hello la plus simple façon tooactivate Engagement Analytique et fonctions dans votre application iOS de surveillance.

Hello Engagement SDK nécessite iOS7 + et Xcode 8 + : cible de déploiement hello de votre application doit être au moins iOS 7.

> [!NOTE]
> Si vous dépendez vraiment de XCode 7, vous pouvez utiliser hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). Il existe un bogue connu sur le module de couverture hello de cette version précédente lors de l’exécution sur des appareils iOS 10, consultez [hello portée module intégration](mobile-engagement-ios-integrate-engagement-reach.md) pour plus d’informations. Si vous choisissez toouse hello SDK v3.2.4 ignorer hello `UserNotifications.framework` importer à l’étape suivante de hello.
>
>

Hello suit est que suffisamment rapport hello tooactivate journaux nécessaires toocompute toutes les statistiques concernant les utilisateurs, Sessions, activités, blocages et Technicals. rapport Hello de journaux nécessaires toocompute autres statistiques telles que les événements, les erreurs et les tâches doivent être effectués manuellement à l’aide des API de l’Engagement de hello (consultez [comment toouse hello avancé Mobile Engagement marquage API dans votre application iOS](mobile-engagement-ios-use-engagement-api.md) depuis ces statistiques dépendent de l’application.

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a>Incorporer hello Engagement SDK dans votre projet iOS
* Télécharger le SDK de hello iOS à partir de [ici](http://aka.ms/qk2rnj).
* Le projet iOS tooyour ajouter hello Engagement SDK : dans Xcode, un clic droit sur votre projet, puis sélectionnez **« ajouter des fichiers trop... »** et choisissez hello `EngagementSDK` dossier.
* Engagement requiert des infrastructures supplémentaires toowork : hello Explorateur de projets, ouvrir votre projet et sélectionnez hello cible correct. Ensuite, ouvrez hello **« Build phases »** onglet et Bonjour **« Binaire avec des bibliothèques de liens »** menu, ajoutez ces infrastructures :

  * `UserNotifications.framework`-définir un lien hello en tant que`Optional`
  * `AdSupport.framework`-définir un lien hello en tant que`Optional`
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> infrastructure de AdSupport Hello peut être supprimée. Engagement doit cette hello de toocollect framework IDFA. Toutefois, la collection de IDFA peut être désactivée \<ios-sdk-engagement-idfa\> toocomply avec hello nouvelle Apple stratégie en matière de ce code.
>
>

## <a name="initialize-hello-engagement-sdk"></a>Initialiser hello Engagement SDK
Vous devez toomodify votre délégué de l’Application :

* En hello en haut de votre fichier d’implémentation, importez l’agent de hello Engagement :

      [...]
      #import "EngagementAgent.h"
* Initialiser l’Engagement au sein de la méthode hello '**applicationDidFinishLaunching :**'ou'**application : didFinishLaunchingWithOptions :**» :

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a>Génération de rapports de base
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a>Méthode recommandée : surchargez vos classes `UIViewController`
Dans le rapport de hello order tooactivate de tous les journaux hello requis par Engagement toocompute utilisateurs, Sessions, activités, blocages et statistiques, vous pouvez simplement mettre tous les votre `UIViewController` sous-classes héritent hello `EngagementViewController` (même règle de classes pour `UITableViewController`  - \> `EngagementTableViewController`).

**Sans Engagement :**

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

**Avec Engagement :**

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a>Autre méthode : appeler `startActivity()` manuellement
Si vous ne pouvez pas ou ne souhaitez pas que toooverload votre `UIViewController` classes, vous pouvez démarrer à la place de vos activités en appelant `EngagementAgent`de méthodes directement.

> [!IMPORTANT]
> Hello, iOS SDK appelle automatiquement hello `endActivity()` méthode lors de l’application hello est fermée. Par conséquent, il est *hautement* recommandé toocall hello `startActivity` méthode chaque fois que l’activité hello d’utilisateur de hello modifier et trop*jamais* appel hello `endActivity` méthode, depuis l’appel de cette méthode force Bonjour toobe de session en cours s’est terminée.
>
>

## <a name="location-reporting"></a>Rapports d'emplacement
Conditions d’utilisation de Apple n’autorisent pas les applications emplacement toouse suivi uniquement à des fins de statistiques. Par conséquent, il est recommandé de tooenable emplacement rapports uniquement si votre application utilise également hello suivi d’emplacement pour une autre raison.

À compter d’iOS 8, vous devez fournir une description de votre application utilise les services d’emplacement en définissant une chaîne de clé de hello [NSLocationWhenInUseUsageDescription] ou [NSLocationAlwaysUsageDescription]dans le fichier Info.plist de votre application. Si vous souhaitez emplacement tooreport en arrière-plan hello avec Engagement, ajoutez la clé de hello NSLocationAlwaysUsageDescription. Dans tous les autres cas, ajoutez la clé de hello NSLocationWhenInUseUsageDescription. Notez que vous avez besoin d’emplacement d’arrière-plan tooreport NSLocationAlwaysAndWhenInUseUsageDescription et NSLocationWhenInUseUsageDescription sur iOS 11.

### <a name="lazy-area-location-reporting"></a>Rapports d'emplacement de zone différé
Signalisation différée de zone emplacement permet tooreport hello pays, la région et localité associés toodevices. Ce type de rapport d'emplacement utilise uniquement des emplacements réseau (basés sur l'ID cellulaire ou le Wi-Fi). zone de Hello est signalée au maximum une fois par session. Hello GPS n’est jamais utilisé, et par conséquent, ce type de rapport de l’emplacement a très peu (pas toosay aucune) impact sur la batterie de hello.

Les zones signalés sont utilisés toocompute des statistiques géographique sur les utilisateurs, des sessions, des événements et des erreurs. Elles peuvent également servir de critère dans les couvertures campagne. Hello dernière connue zone signalé pour un périphérique peut être récupérée Merci toohello [Device API].

emplacement de zone différée tooenable reporting, ajoutez hello ligne suivante après l’initialisation de l’agent de hello Engagement :

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a>Rapports d'emplacement en temps réel
Signalisation de l’emplacement en temps réel permet de latitude de hello tooreport et longitude associés toodevices. Par défaut, ce type d’emplacement reporting utilise uniquement des emplacements réseau (basés sur l’ID de la cellule ou Wi-Fi), et hello reporting est uniquement active lorsque l’application hello s’exécute en premier plan (par exemple, lors d’une session).

Les emplacements en temps réel sont *pas* utilisé toocompute statistiques. Leur utilisation de hello tooallow de délimitation géographique en temps réel ne sert que \<portée-public-géorepérage\> critère dans les campagnes Reach.

emplacement en temps réel de tooenable création de rapports, ajoutez hello ligne suivante après l’initialisation de l’agent de hello Engagement :

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a>Rapports GPS
Par défaut, le rapport d'emplacement en temps réel utilise uniquement des emplacements réseau. utilisation de hello tooenable de GPS en fonction des emplacements (qui sont beaucoup plus précises), ajoutez :

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a>Rapports en arrière-plan
Par défaut, reporting en temps réel sur l’emplacement est uniquement active lorsque l’application hello s’exécute en premier plan (par exemple, lors d’une session). hello tooenable reporting également en arrière-plan, ajoutez :

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> Lors de l’application hello s’exécute en arrière-plan, seuls les emplacements réseau sont signalées, même si vous avez activé hello GPS.
>
>

Implémentation de cette fonction appelle [startMonitoringSignificantLocationChanges] lorsque votre application passe en arrière-plan de hello. N’oubliez pas qu’il sera automatiquement relancer votre application en arrière-plan de hello si l’arrivée d’un nouvel événement d’emplacement.

## <a name="advanced-reporting"></a>Génération de rapports avancés
Si vous le souhaitez, si vous souhaitez tooreport les événements d’application spécifique, les erreurs et les tâches, vous devez toouse hello Engagement API via les méthodes hello Hello `EngagementAgent` classe. Un objet de cette classe peut être récupéré en appelant hello `[EngagementAgent shared]` méthode statique.

permet de toouse toutes les fonctionnalités avancées d’Engagement Hello Engagement API et est détaillée dans hello comment tooUse l’API d’Engagement sur iOS (ainsi que dans la documentation technique de hello Hello `EngagementAgent` classe).

## <a name="disable-idfa-collection"></a>Désactiver la collecte de l'IDFA
Par défaut, Engagement utilisera hello [IDFA] toouniquely identifier un utilisateur. Mais si vous n’utilisez pas de publication ailleurs dans l’application hello, vous pourrez être rejetée par le processus de révision App Store de hello. Collection de IDFA peut être désactivée en ajoutant la macro de préprocesseur hello `ENGAGEMENT_DISABLE_IDFA` dans votre fichier pch (ou Bonjour `Build Settings` de votre application). Cela permet de garantir qu’il n’existe aucune référence trop`ASIdentifierManager`, `advertisingIdentifier` ou `isAdvertisingTrackingEnabled` dans la build d’application hello.

Intégration dans hello **prefix.pch** fichier :

    #define ENGAGEMENT_DISABLE_IDFA
    ...

Vous pouvez vérifier que collection IDFA de hello est correctement désactivée dans votre application en vérifiant les journaux des tests hello Engagement. Consultez hello des tests d’intégration\<idfa du test engagement ios sdk\> documentation pour plus d’informations.

## <a name="disable-log-reporting"></a>Désactiver les rapports de suivi
### <a name="using-a-method-call"></a>En appelant une méthode
Si vous souhaitez toostop Engagement envoi de journaux, vous pouvez appeler :

    [[EngagementAgent shared] setEnabled:NO];

Cet appel est persistant : il utilise `NSUserDefaults` plus d’informations toostore hello.

Vous pouvez activer le journal de création de rapports en appelant hello même fonction avec `YES`.

### <a name="integration-in-your-settings-bundle"></a>Intégration dans votre groupe de paramètres
Au lieu d'appeler cette fonction, vous pouvez également intégrer ce paramètre directement dans votre fichier `Settings.bundle` existant. Hello chaîne `engagement_agent_enabled` doit être utilisé comme un identificateur de préférence hello et il doivent être associé tooa bouton bascule (`PSToggleSwitchSpecifier`).

Hello selon l’exemple de `Settings.bundle` montre comment tooimplement il :

    <dict>
        <key>PreferenceSpecifiers</key>
        <array>
            <dict>
                <key>DefaultValue</key>
                <true/>
                <key>Key</key>
                <string>engagement_agent_enabled</string>
                <key>Title</key>
                <string>Log reporting enabled</string>
                <key>Type</key>
                <string>PSToggleSwitchSpecifier</string>
            </dict>
        </array>
        <key>StringsTable</key>
        <string>Root</string>
    </dict>

<!-- URLs. -->
[Device API]: http://go.microsoft.com/?linkid=9876094
[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26
[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18
[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges
[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier
