---
title: "aaaWindows l’intégration de kit de développement logiciel Silverlight Engagement téléphonique"
description: Comment tooIntegrate Azure Mobile Engagement avec les applications Silverlight Windows Phone
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a>Intégration du Kit de développement logiciel (SDK) d’Engagement Windows Phone Silverlight
> [!div class="op_single_selector"]
> * [Windows Universal](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

Cette procédure décrit Analytique hello la plus simple façon tooactivate Azure Mobile Engagement et l’analyse des fonctions dans votre application Windows Phone Silverlight.

Hello suit est que suffisamment rapport hello tooactivate journaux nécessaires toocompute toutes les statistiques concernant les utilisateurs, Sessions, activités, blocages et Technicals. rapport Hello de journaux nécessaires toocompute autres statistiques telles que les événements, les erreurs et les tâches doivent être effectués manuellement à l’aide des API de l’Engagement de hello (consultez [comment toouse hello avancé Mobile Engagement marquage API dans votre application Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md) ci-dessous) dans la mesure où ces statistiques sont dépend de l’application.

## <a name="supported-versions"></a>Versions prises en charge
Hello le Kit de développement logiciel Mobile Engagement pour Windows Silverlight peut uniquement être intégré dans des applications qui ciblent :

* Windows Phone 8.0
* Windows Phone 8.1 Silverlight

> [!NOTE]
> Si vous ciblez Windows Phone 8.1 (non Silverlight), consultez toohello [procédure d’intégration Windows universel](mobile-engagement-windows-store-integrate-engagement.md).
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a>Installer hello Mobile Engagement Silverlight SDK
Hello Mobile Engagement Kit de développement logiciel de Silverlight pour Windows est disponible comme package Nuget appelé *MicrosoftAzure.MobileEngagement*. Vous pouvez l’installer à partir de hello Gestionnaire de Package Nuget de Visual Studio. 

## <a name="add-hello-capabilities"></a>Ajouter des fonctionnalités hello
Hello SDK de l’Engagement a besoin de certaines fonctionnalités de hello Kit de développement logiciel Windows Phone Silverlight dans l’ordre toowork correctement.

Ouvrez votre `WMAppManifest.xml` de fichiers et assurez-vous que hello suivant des fonctions sont déclarés dans hello `Capabilities` Panneau de configuration :

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a>Initialiser hello Engagement SDK
### <a name="engagement-configuration"></a>Configuration d'Engagement
configuration d’Engagement Hello centralisée dans hello `Resources\EngagementConfiguration.xml` fichier de votre projet.

Modifiez cette toospecify de fichier :

* Votre chaîne de connexion d'application entre les balises `<connectionString>` and `<\connectionString>`.

Si vous souhaitez toospecify il lors de l’exécution au lieu de cela, vous pouvez appeler suivant de hello méthode avant l’initialisation de l’agent hello Engagement :

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

chaîne de connexion Hello pour votre application s’affiche sur hello portail classique Azure.

### <a name="engagement-initialization"></a>Initialisation d'Engagement
Quand vous créez un projet, un fichier `App.xaml.cs` est généré. Cette classe hérite de `Application` et contient de nombreuses méthodes importantes. Il sera également utilisé tooinitialize hello Engagement SDK.

Modifier hello `App.xaml.cs`:

* Ajouter tooyour `using` instructions :
  
      using Microsoft.Azure.Engagement;
* Insérer `EngagementAgent.Instance.Init` Bonjour `Application_Launching` méthode :
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* Insérer `EngagementAgent.Instance.OnActivated` Bonjour `Application_Activated` méthode :
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> Nous vous déconseillons de vous tooadd hello Engagement d’initialisation à un autre endroit de votre application. Toutefois, n’oubliez pas que hello `EngagementAgent.Instance.Init` méthode s’exécute sur un thread dédié et non sur hello thread d’interface utilisateur.
> 
> 

## <a name="basic-reporting"></a>Génération de rapports de base
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a>Méthode recommandée : surchargez vos classes `PhoneApplicationPage`
Dans le rapport de hello order tooactivate de tous les journaux hello requis par Engagement toocompute utilisateurs, Sessions, activités, blocages et statistiques, vous pouvez simplement mettre toutes vos `PhoneApplicationPage` sous-classes héritent hello `EngagementPage` classes.

Voici un exemple de procédure toodo pour une page de votre application. Vous pouvez effectuer hello identiques pour toutes les pages de votre application.

#### <a name="c-source-file"></a>Fichier source C#
Modifiez le fichier `.xaml.cs` de votre page :

* Ajouter tooyour `using` instructions :
  
      using Microsoft.Azure.Engagement;
* Remplacez `PhoneApplicationPage` par `EngagementPage` :

**Sans Engagement :**

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

**Avec Engagement :**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> Si votre page hérite de hello `OnNavigatedTo` (méthode), être prudent toolet hello `base.OnNavigatedTo(e)` appeler. Dans le cas contraire, activité hello n’est pas signalée. En effet, hello `EngagementPage` appelle `StartActivity` à l’intérieur de hello `OnNavigatedTo` (méthode).
> 
> 

#### <a name="xaml-file"></a>Fichier XAML
Modifiez le fichier `.xaml` de votre page :

* Ajoutez les déclarations d’espaces de noms tooyour :
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* Remplacez `phone:PhoneApplicationPage` par `engagement:EngagementPage` :

**Sans Engagement :**

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

**Avec Engagement :**

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a>Substituer le comportement par défaut de hello
Par défaut, nom de la classe de page de hello hello est signalée comme nom de l’activité hello, avec sans supplémentaire. Si la classe hello utilise hello suffixe de « Page », Engagement entraîne également sa suppression.

Si vous souhaitez le comportement par défaut de hello toooverride pour le nom de hello, ajoutez simplement ce code tooyour :

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

Si vous souhaitez tooreport des informations supplémentaires avec votre activité, vous pouvez ajouter ce code tooyour :

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

Ces méthodes sont appelées dans hello `OnNavigatedTo` méthode de votre page.

### <a name="alternate-method-call-startactivity-manually"></a>Autre méthode : appeler `StartActivity()` manuellement
Si vous ne pouvez pas ou ne souhaitez pas que toooverload votre `PhoneApplicationPage` classes, vous pouvez démarrer à la place de vos activités en appelant `EngagementAgent` direct de méthodes.

Nous vous recommandons d’appeler `StartActivity` à l’intérieur de la méthode `OnNavigatedTo` de votre PhoneApplicationPage.

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> Assurez-vous de terminer votre session correctement.
> 
> Kit de développement logiciel de Hello appelle automatiquement hello `EndActivity` méthode lors de l’application hello est fermée. Par conséquent, il est **hautement** recommandé toocall hello `StartActivity` méthode chaque fois que l’activité hello d’utilisateur de hello modifier et trop**jamais** appel hello `EndActivity` (méthode). Cette méthode envoie un message toohello Engagement serveur que l’utilisateur actuel hello a quitté l’application hello et que cela affecte tous les journaux d’application.
> 
> 

## <a name="advanced-reporting"></a>Génération de rapports avancés
Si vous le souhaitez, vous souhaiterez peut-être tooreport les événements d’application spécifique, les erreurs et les travaux, toodo donc, utilisez hello d’autres méthodes trouvés dans hello `EngagementAgent` classe. Hello Engagement API permet toouse toutes les fonctionnalités avancées d’Engagement.

Pour plus d’informations, consultez [comment toouse hello avancé Mobile Engagement marquage API dans votre application Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md).

## <a name="advanced-configuration"></a>Configuration avancée
### <a name="disable-automatic-crash-reporting"></a>Désactiver le signalement automatique des incidents
Vous pouvez désactiver hello automatique de rapport d’incident fonctionnalité d’Engagement. Dans ce cas, si une exception non gérée se produit, Engagement ne fait rien.

> [!WARNING]
> Si vous envisagez de toodisable cette fonctionnalité, gardez à l’esprit que, lorsqu’un incident non géré se produit dans votre application, Engagement n’envoie pas de blocage de hello **AND** il ne ferme pas la session de hello et les travaux.
> 
> 

toodisable automatique sur incident reporting, simplement personnaliser votre configuration en fonction de méthode hello vous l’avez déclarée :

#### <a name="from-engagementconfigurationxml-file"></a>Dans le fichier `EngagementConfiguration.xml`
Définir le rapport incident trop`false` entre `<reportCrash>` et `</reportCrash>` balises.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>Dans l'objet `EngagementConfiguration` au moment l'exécution
Définissez toofalse de panne de rapport à l’aide de votre objet EngagementConfiguration.

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>Mode rafale
Par défaut, les rapports de service d’Engagement hello journaux en temps réel. Si votre application rapports journaux très fréquemment, il est mieux toobuffer hello journaux et tooreport à la fois à une base de temps réguliers (appelée hello « mode de croissance »).

toodo appeler par conséquent, la méthode hello :

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

l’argument Hello est une valeur dans **millisecondes**. À tout moment, si vous souhaitez que la journalisation en temps réel tooreactivate hello, appelez uniquement méthode hello sans paramètres ou avec la valeur de hello 0.

Hello mode rafale légèrement augmenter la batterie de hello vie mais n’a un impact sur hello Engagement moniteur : toutes les sessions et les travaux seront arrondies toohello rafale seuil (par conséquent, les sessions et les travaux plus court que le seuil de croissance hello n’est pas forcément visible). Il est recommandé de toouse un seuil de croissance n’est plus à 30000 (30 s). Vous avez toobe souvenez-vous des journaux enregistrés too300 limité des éléments. Si l'envoi est trop long, vous risquez de perdre certains journaux.

> [!WARNING]
> Hello rafale seuil ne peut pas être configuré période tooa inférieure à une seconde. Si vous essayez donc toodo, hello SDK affiche une trace avec l’erreur de hello et sera automatiquement réinitialise toohello par défaut, c'est-à-dire que zéro seconde. Cette opération déclenche hello SDK tooreport hello journaux en temps réel.
> 
> 

