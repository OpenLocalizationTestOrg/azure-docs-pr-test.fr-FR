---
title: "aaaWindows Universal avancé Reporting avec MobileApps Engagement"
description: Comment tooIntegrate Azure Mobile Engagement avec les applications Windows universelles
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a>Création de rapports avancée avec hello universel applications Engagement Kit de développement
> [!div class="op_single_selector"]
> * [Windows universel](mobile-engagement-windows-store-advanced-reporting.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

Cette rubrique décrit des scénarios de génération de rapports supplémentaires dans votre application Windows Universal. Ces scénarios incluent les options que vous pouvez choisir d’application toohello tooapply créé Bonjour [mise en route](mobile-engagement-windows-store-dotnet-get-started.md) didacticiel.

## <a name="prerequisites"></a>Composants requis
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

Avant de commencer ce didacticiel, vous devez d’abord terminer hello [mise en route](mobile-engagement-windows-store-dotnet-get-started.md) (didacticiel), qui est délibérément simple et directe. Ce didacticiel présente les options supplémentaires vous pouvez choisir.

## <a name="specifying-engagement-configuration-at-runtime"></a>Spécification de la configuration d’Engagement lors de l’exécution
configuration d’Engagement Hello centralisée dans hello `Resources\EngagementConfiguration.xml` fichier de votre projet, c'est-à-dire où il a été spécifié dans hello [mise en route](mobile-engagement-windows-store-dotnet-get-started.md) rubrique.

Mais vous pouvez également le spécifier lors de l’exécution : vous pouvez appeler hello méthode avant l’initialisation de l’agent hello Engagement :

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a>Méthode recommandée : surchargez vos classes `Page`
tooactivate hello reporting de tous les journaux hello requis par Engagement toocompute utilisateurs, Sessions, activités, blocages et statistiques, effectuer tous les votre `Page` sous-classes héritent hello `EngagementPage` classes.

Voici un exemple appliqué à une page de votre application. Vous pouvez effectuer hello identiques pour toutes les pages de votre application.

### <a name="c-source-file"></a>Fichier source C#
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
> Si votre page substitue hello `OnNavigatedTo` (méthode), être toocall vraiment `base.OnNavigatedTo(e)`. Sinon, activité hello n’est pas être signalé (hello `EngagementPage` appelle `StartActivity` à l’intérieur de son `OnNavigatedTo` méthode).
> 
> 

### <a name="xaml-file"></a>Fichier XAML
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

### <a name="override-hello-default-behaviour"></a>Substituer le comportement par défaut de hello
Par défaut, nom de la classe de page de hello hello est signalée comme nom de l’activité hello, avec sans supplémentaire. Si la classe hello utilise hello suffixe de « Page », l’Engagement le supprime.

toooverride par défaut hello pour le nom de hello, ajoutez ce code :

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

tooreport des informations supplémentaires avec votre activité, ajoutez le code suivant :

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

Ces méthodes sont appelées dans hello `OnNavigatedTo` méthode de votre page.

### <a name="alternate-method-call-startactivity-manually"></a>Autre méthode : appeler `StartActivity()` manuellement
Si vous ne pouvez pas ou ne souhaitez pas que toooverload votre `Page` classes, vous pouvez démarrer à la place de vos activités en appelant `EngagementAgent` direct de méthodes.

Nous vous recommandons d'appeler `StartActivity` à l'intérieur de la méthode `OnNavigatedTo` de votre page.

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> Assurez-vous de terminer votre session correctement.
> 
> Hello SDK Universal Windows appelle automatiquement hello `EndActivity` méthode lors de l’application hello est fermée. Par conséquent, il est **hautement** recommandé toocall hello `StartActivity` méthode chaque fois que l’activité hello d’utilisateur de hello modifier et trop**jamais** appel hello `EndActivity` (méthode). Cette méthode notifie server d’Engagement hello que l’utilisateur actuel hello a quitté l’application hello, ce qui aura un impact sur tous les journaux d’application.
> 
> 

## <a name="advanced-reporting"></a>Génération de rapports avancés
Si vous le souhaitez, vous souhaiterez peut-être tooreport les événements spécifiques à l’application, les erreurs et les travaux, toodo donc, utilisez hello d’autres méthodes trouvés dans hello `EngagementAgent` classe. Hello Engagement API autorise l’utilisation de fonctions avancées de tous les Engagement.

Pour plus d’informations, consultez [comment toouse hello avancé Mobile Engagement marquage API dans votre application Windows universelle](mobile-engagement-windows-store-use-engagement-api.md).

