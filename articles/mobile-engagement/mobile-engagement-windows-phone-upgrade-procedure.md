---
title: "aaaWindows les procédures de mise à niveau Phone Silverlight SDK"
description: "Procédures de mise à niveau du SDK Windows Phone Silverlight pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a>Procédures de mise à niveau du Kit de développement Windows Phone Silverlight
Si vous avez déjà intégré une ancienne version de notre kit de développement logiciel dans votre application, vous avez hello tooconsider hello Kit de développement logiciel de la mise à niveau les points suivants.

Vous avez peut-être toofollow plusieurs procédures issue de plusieurs versions du Kit de développement logiciel de hello. Par exemple, si vous migrez à partir de 0.10.1 too0.11.0 avoir toofirst suivez hello » à partir de 0.9.0 too0.10.1 « procédure puis hello » à partir de 0.10.1 too0.11.0 « procédure.

## <a name="from-200-too330"></a>À partir de 2.0.0 too3.3.0
### <a name="test-logs"></a>Journaux des tests
Journaux de la console produits par hello SDK peuvent être activé/désactivé/filtrées. toocustomize, propriété hello de mise à jour `EngagementAgent.Instance.TestLogEnabled` tooone de valeur hello disponible à partir de hello `EngagementTestLogLevel` énumération, par exemple :

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a>À partir de 1.1.1 too2.0.0
Hello suivante décrit comment toomigrate une intégration du Kit de développement logiciel de hello Capptain service offert par Capptain SAS dans une application grâce à Azure Mobile Engagement. 

> [!IMPORTANT]
> Capptain et Mobile Engagement sont hello pas les mêmes services et procédure hello fourni ci-dessous uniquement met en évidence comment toomigrate hello application cliente. Migration hello SDK dans l’application hello ne fait pas migrer vos données des hello Capptain toohello Mobile Engagement serveurs
> 
> 

Si vous effectuez une migration à partir d’une version antérieure, veuillez consultez hello Capptain site web toomigrate too1.1.1 tout d’abord, appliquez hello procédure

### <a name="nuget-package"></a>Package NuGet
Remplacez **Capptain.WindowsPhone** par le package NuGet **MicrosoftAzure.MobileEngagement**.

### <a name="applying-mobile-engagement"></a>Application d'Engagement Mobile
Hello SDK utilise le terme de hello `Engagement`. Vous devez tooupdate toomatch de votre projet cette modification.

Vous devez toouninstall votre package nuget Capptain. Considérez que toutes vos modifications dans le dossier de ressources Capptain seront supprimées. Si vous souhaitez tookeep ces fichiers, faites une copie d’eux.

Après cela, installer le nouveau package de nuget Microsoft Azure Engagement hello sur votre projet. Vous le trouverez directement sur [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement). Ce remplace action tous les fichiers de ressources utilisées par l’Engagement et ajoute hello nouvelle DLL d’Engagement tooyour les références de projet.

Vous avez tooclean à vos références de projet et en supprimant les références Capptain DLL. Si vous n’apportez pas cette option, version hello de Capptain est en conflit et erreur se produira.

Si vous avez personnalisé les ressources Capptain, copiez votre ancien contenu de fichiers et les coller dans des fichiers de Engagement hello. Notez que les fichiers xaml et cs ont toobe mis à jour.

Une fois ces étapes terminées il vous suffit tooreplace les anciennes références Capptain par nouvelles références d’Engagement hello.

1. Tous les espaces de noms Capptain ont toobe mis à jour.
   
    Avant la migration :
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    Après la migration :
   
        using Microsoft.Azure.Engagement;
2. Toutes les classes Capptain qui contiennent « Capptain » doivent contenir « Engagement ».
   
    Avant la migration :
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    Après la migration :
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. Pour les fichiers xaml, les attributs et les espaces de noms Capptain changent également.
   
    Avant la migration :
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    Après la migration :
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. Pourquoi autres ressources comme des images Capptain, notez qu’ils ont également été renommé toouse « Engagement ».

### <a name="application-id--sdk-key"></a>ID de l'application / clé SDK
Engagement utilise une chaîne de connexion. Vous n’avez pas toospecify un ID d’application et une clé de kit de développement logiciel avec Mobile Engagement, vous devez uniquement toospecify une chaîne de connexion. Vous pouvez la configurer dans votre fichier EngagementConfiguration.

configuration d’Engagement Hello peut être définie dans votre `Resources\EngagementConfiguration.xml` le fichier de votre projet.

Modifiez cette toospecify de fichier :

* Votre chaîne de connexion d'application entre les balises `<connectionString>` and `<\connectionString>`.

Si vous souhaitez toospecify il lors de l’exécution au lieu de cela, vous pouvez appeler suivant de hello méthode avant l’initialisation de l’agent hello Engagement :

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

chaîne de connexion Hello pour votre application s’affiche dans hello portail classique Azure.

### <a name="items-name-change"></a>Changement de noms d'éléments
Tous les éléments nommés *capptain* ont été renommés *engagement*. De même pour *Capptain* trop*Engagement*.

Exemples d'éléments Capptain couramment utilisés :

* CapptainConfiguration se nomme maintenant EngagementConfiguration
* CapptainAgent se nomme maintenant EngagementAgent
* CapptainReach se nomme maintenant EngagementReach
* CapptainHttpConfig se nomme maintenant EngagementHttpConfig
* GetCapptainPageName se nomme maintenant GetEngagementPageName

Notez que ce changement affecte également les méthodes substituées.

