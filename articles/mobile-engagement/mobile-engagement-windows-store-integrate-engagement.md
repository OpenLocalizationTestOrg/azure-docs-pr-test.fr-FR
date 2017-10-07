---
title: "aaaWindows intégration de kit de développement logiciel Engagement applications universel"
description: Comment tooIntegrate Azure Mobile Engagement avec les applications Windows universelles
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 18543798099c233dbe55cc387ba0216e369c8596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a>Intégration du Kit de développement logiciel du module Engagement des applications universelles Windows
> [!div class="op_single_selector"]
> * [Windows universel](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

Cette procédure décrit Analytique hello la plus simple façon tooactivate Engagement et l’analyse des fonctions dans votre application Windows universelle.

Hello suit est que suffisamment rapport hello tooactivate journaux nécessaires toocompute toutes les statistiques concernant les utilisateurs, Sessions, activités, blocages et Technicals. rapport Hello de journaux nécessaires toocompute autres statistiques telles que les événements, les erreurs et les tâches doivent être effectués manuellement à l’aide des API de l’Engagement de hello (consultez [comment toouse hello avancé Mobile Engagement marquage API dans votre application Windows universelle](mobile-engagement-windows-store-use-engagement-api.md) depuis Ces statistiques sont dépend de l’application.

## <a name="supported-versions"></a>Versions prises en charge
Hello Mobile Engagement SDK pour applications Windows universelles peut uniquement être intégré dans Windows Runtime et les applications de plateforme Windows universelle qui ciblent :

* Windows 8
* Windows 8.1
* Windows Phone 8.1
* Windows 10 (gammes mobiles et de bureau)

> [!NOTE]
> Si vous ciblez Windows Phone Silverlight, consultez toohello [procédure d’intégration de Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a>Installer hello SDK des applications Universal Mobile Engagement
### <a name="all-platforms"></a>Toutes les plateformes
Hello Mobile Engagement SDK pour Windows application universelle est disponible comme package Nuget appelé *MicrosoftAzure.MobileEngagement*. Vous pouvez l’installer à partir de hello Gestionnaire de Package Nuget de Visual Studio.

### <a name="windows-8x-and-windows-phone-81"></a>Windows 8.x et Windows Phone 8.1
NuGet déploie automatiquement les ressources du Kit de développement logiciel hello Bonjour `Resources` dossier à votre projet d’application hello racine.

### <a name="windows-10-universal-windows-platform-applications"></a>Applications de la plateforme Windows universelle Windows 10
NuGet ne déploie pas automatiquement les ressources du Kit de développement logiciel hello dans votre application UWP encore. Vous avez toodo manuellement avant le déploiement de ressources est réintroduit dans NuGet :

1. Ouvrez votre Explorateur de fichiers.
2. Accédez toohello l’emplacement suivant (**x.x.x** est la version hello d’Engagement que vous installez) : *% USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\*  *x.x.x**\\content\win81*
3. Glisser- déposer hello **ressources** dossier hello fichier explorer toohello de racine de votre projet dans Visual Studio.
4. Dans Visual Studio, sélectionnez votre projet et activer hello **afficher tous les fichiers** icône au-dessus hello **l’Explorateur de solutions**.
5. Certains fichiers ne sont pas inclus dans le projet de hello. tooimport à la fois avec le bouton droit à cliquer sur hello **ressources** dossier, **exclure du projet** puis un autre avec le bouton droit sur hello **ressources** dossier **Include dans le projet** toore-inclure la totalité du dossier hello. Tous les fichiers à partir de hello **ressources** dossier sont désormais incluses dans votre projet.

## <a name="add-hello-capabilities"></a>Ajouter des fonctionnalités hello
Hello SDK de l’Engagement a besoin de certaines fonctionnalités de hello Kit de développement dans l’ordre toowork correctement.

Ouvrez votre `Package.appxmanifest` de fichiers et assurez-vous que hello suivant des fonctions sont déclarés :

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a>Initialiser hello Engagement SDK
### <a name="engagement-configuration"></a>Configuration d'Engagement
configuration d’Engagement Hello centralisée dans hello `Resources\EngagementConfiguration.xml` fichier de votre projet.

Modifiez cette toospecify de fichier :

* Votre chaîne de connexion d'application entre les balises `<connectionString>` and `<\connectionString>`.

Si vous souhaitez toospecify il lors de l’exécution au lieu de cela, vous pouvez appeler suivant de hello méthode avant l’initialisation de l’agent hello Engagement :

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

chaîne de connexion Hello pour votre application s’affiche sur hello portail classique Azure.

### <a name="engagement-initialization"></a>Initialisation d'Engagement
Quand vous créez un projet, un fichier `App.xaml.cs` est généré. Cette classe hérite de `Application` et contient de nombreuses méthodes importantes. Il sera également utilisé tooinitialize hello Engagement SDK.

Modifier hello `App.xaml.cs`:

* Ajouter tooyour `using` instructions :
  
      using Microsoft.Azure.Engagement;
* Définissez une initialisation d’Engagement méthode tooshare hello qu’une seule fois pour tous les appels :
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* Appelez `InitEngagement` Bonjour `OnLaunched` méthode :
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* Lorsque votre application est lancée à l’aide d’un schéma personnalisé, une autre ligne de commande de l’application ou hello hello puis `OnActivated` méthode est appelée. Vous devez également tooinitiate hello Engagement SDK quand votre application est activée. toodo donc remplacer `OnActivated` méthode :
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> Nous vous déconseillons de vous tooadd hello Engagement d’initialisation à un autre endroit de votre application.
> 
> 

## <a name="basic-reporting"></a>Génération de rapports de base
### <a name="recommended-method-overload-your-page-classes"></a>Méthode recommandée : surchargez vos classes `Page`
Dans le rapport de hello order tooactivate de tous les journaux hello requis par Engagement toocompute utilisateurs, Sessions, activités, blocages et statistiques, vous pouvez simplement mettre toutes vos `Page` sous-classes héritent hello `EngagementPage` classes.

Voici un exemple de procédure toodo pour une page de votre application. Vous pouvez effectuer hello identiques pour toutes les pages de votre application.

#### <a name="c-source-file"></a>Fichier source C#
Modifiez le fichier `.xaml.cs` de votre page :

* Ajouter tooyour `using` instructions :
  
      using Microsoft.Azure.Engagement;
* Remplacez `Page` par `EngagementPage` :

**Sans Engagement :**

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

**Avec Engagement :**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> Si votre page substitue hello `OnNavigatedTo` (méthode), être toocall vraiment `base.OnNavigatedTo(e)`. Dans le cas contraire, activité hello n’est pas signalée (hello `EngagementPage` appelle `StartActivity` à l’intérieur de son `OnNavigatedTo` méthode).
> 
> 

#### <a name="xaml-file"></a>Fichier XAML
Modifiez le fichier `.xaml` de votre page :

* Ajoutez les déclarations d’espaces de noms tooyour :
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* Remplacez `Page` par `engagement:EngagementPage` :

**Sans Engagement :**

        <Page>
            <!-- layout -->
            ...
        </Page>

**Avec Engagement :**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a>Substituer le comportement par défaut de hello
Par défaut, nom de la classe de page de hello hello est signalée comme nom de l’activité hello, avec sans supplémentaire. Si la classe hello utilise hello suffixe de « Page », Engagement entraîne également sa suppression.

Si vous souhaitez le comportement par défaut de hello toooverride pour le nom de hello, ajoutez simplement ce code tooyour :

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

Si vous souhaitez tooreport certaines informations supplémentaires avec votre activité, vous pouvez ajouter ce code tooyour :

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

Ces méthodes sont appelées dans hello `OnNavigatedTo` méthode de votre page.

### <a name="alternate-method-call-startactivity-manually"></a>Autre méthode : appeler `StartActivity()` manuellement
Si vous ne pouvez pas ou ne souhaitez pas que toooverload votre `Page` classes, vous pouvez démarrer à la place de vos activités en appelant `EngagementAgent` direct de méthodes.

Nous vous recommandons de toocall `StartActivity` à l’intérieur de votre `OnNavigatedTo` méthode de votre Page.

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> Assurez-vous de terminer votre session correctement.
> 
> Hello SDK Universal Windows appelle automatiquement hello `EndActivity` méthode lors de l’application hello est fermée. Par conséquent, il est **hautement** recommandé toocall hello `StartActivity` méthode chaque fois que l’activité hello d’utilisateur de hello modifier et trop**jamais** appel hello `EndActivity` (méthode), cette méthode envoie tooEngagement serveur que l’utilisateur actuel a laissez hello application, ce sera a un impact sur tous les journaux d’application.
> 
> 

## <a name="advanced-reporting"></a>Génération de rapports avancés
Si vous le souhaitez, vous souhaiterez peut-être tooreport les événements d’application spécifique, les erreurs et les travaux, toodo donc, utilisez hello d’autres méthodes trouvés dans hello `EngagementAgent` classe. Hello Engagement API permet toouse toutes les fonctionnalités avancées d’Engagement.

Pour plus d’informations, consultez [comment toouse hello avancé Mobile Engagement marquage API dans votre application Windows universelle](mobile-engagement-windows-store-use-engagement-api.md).

## <a name="advanced-configuration"></a>Configuration avancée
### <a name="disable-automatic-crash-reporting"></a>Désactiver le signalement automatique des incidents
Vous pouvez désactiver hello automatique de rapport d’incident fonctionnalité d’Engagement. Dans ce cas, si une exception non gérée se produit, Engagement ne fait rien.

> [!WARNING]
> Si vous envisagez de toodisable cette fonctionnalité, gardez à l’esprit que, lorsqu’un incident non géré se produit dans votre application, Engagement n’envoie pas de blocage de hello **et** ne ferme pas la session de hello et les travaux.
> 
> 

toodisable automatique sur incident reporting, simplement personnaliser votre configuration en fonction de méthode hello vous l’avez déclarée :

#### <a name="from-engagementconfigurationxml-file"></a>Dans le fichier `EngagementConfiguration.xml`
Définir le rapport incident trop`false` entre `<reportCrash>` et `</reportCrash>` balises.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>Dans l'objet `EngagementConfiguration` au moment l'exécution
Définissez toofalse de panne de rapport à l’aide de votre objet EngagementConfiguration.

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>Mode rafale
Par défaut, les rapports de service d’Engagement hello journaux en temps réel. Si votre application rapports journaux très fréquemment, il est mieux toobuffer hello journaux et tooreport à la fois à une base de temps réguliers (appelée hello « mode de croissance »).

toodo appeler par conséquent, la méthode hello :

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

l’argument Hello est une valeur dans **millisecondes**. À tout moment, si vous souhaitez que la journalisation en temps réel tooreactivate hello, appelez uniquement méthode hello sans paramètres ou avec la valeur de hello 0.

Hello mode rafale légèrement augmenter la batterie de hello vie mais n’a un impact sur hello Engagement moniteur : toutes les sessions et les travaux seront arrondies toohello rafale seuil (par conséquent, les sessions et les travaux plus court que le seuil de croissance hello n’est pas forcément visible). Il est recommandé de toouse un seuil de croissance n’est plus à 30000 (30 s). Vous avez toobe souvenez-vous des journaux enregistrés too300 limité des éléments. Si l'envoi est trop long, vous risquez de perdre certains journaux.

> [!WARNING]
> seuil de croissance Hello ne peut pas être configurée période tooa inférieur à 1 s. Si vous essayez donc toodo, hello SDK affiche une trace avec l’erreur de hello et sera automatiquement réinitialisé toohello par défaut, c'est-à-dire 0. Cette opération déclenche hello SDK tooreport hello journaux en temps réel.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

