---
title: aaaAdvanced Configuration pour Windows applications Engagement SDK Universal
description: "Options de configuration avancées pour Engagement avec des applications Windows Universal"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6d85dd5d-ac07-43ba-bbe4-e91c3a17690b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 23bd05012bc25d438d8d4985a112280bed0292b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-windows-universal-apps-engagement-sdk"></a>Configuration avancée du Kit de développement logiciel (SDK) des applications Windows Universal pour Engagement
> [!div class="op_single_selector"]
> * [Windows universel](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
> 
> 

Cette procédure décrit comment tooconfigure différentes options de configuration pour les applications Azure Mobile Engagement Android.

## <a name="prerequisites"></a>Composants requis
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="advanced-configuration"></a>Configuration avancée
### <a name="disable-automatic-crash-reporting"></a>Désactiver le signalement automatique des incidents
Vous pouvez désactiver hello automatique de rapport d’incident fonctionnalité d’Engagement. Puis, lorsqu’une exception non gérée se produit, Engagement ne fait rien.

> [!WARNING]
> Si vous désactivez cette fonctionnalité, puis lorsqu’un incident non gérée se produit dans votre application, Engagement n’envoie pas de blocage de hello **et** ne ferme pas la session de hello et les travaux.
> 
> 

toodisable automatique sur incident reporting, personnaliser votre configuration en fonction de méthode hello vous l’avez déclarée :

#### <a name="from-engagementconfigurationxml-file"></a>Dans le fichier `EngagementConfiguration.xml`
Définir le rapport incident trop`false` entre `<reportCrash>` et `</reportCrash>` balises.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>Dans l'objet `EngagementConfiguration` au moment l'exécution
Définissez toofalse de panne de rapport à l’aide de votre objet EngagementConfiguration.

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="disable-real-time-reporting"></a>Désactiver les rapports en temps réel
Par défaut, les rapports de service d’Engagement hello journaux en temps réel. Si votre application rapports journaux fréquemment, il est mieux toobuffer hello journaux et tooreport à la fois à une base de temps réguliers. On parle dans ce cas de « mode rafale ».

toodo appeler par conséquent, la méthode hello :

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

l’argument Hello est une valeur dans **millisecondes**. Chaque fois que vous souhaitez que la journalisation en temps réel tooreactivate hello, appelez la méthode hello sans paramètres ou avec la valeur de hello 0.

Mode rafale augmente l’autonomie des batteries hello légèrement mais a un impact sur hello Engagement moniteur : durée des sessions et les travaux toute sont arrondis toohello rafale seuil (par conséquent, les sessions et les travaux plus court que le seuil de croissance hello n’est pas forcément visible). Nous vous recommandons d'utiliser un seuil de rafale inférieur à 30000 (30 s). Journaux enregistrés sont des éléments too300 limité. Si l'envoi est trop long, vous risquez de perdre certains journaux.

> [!WARNING]
> seuil de croissance Hello ne peut pas être configuré tooa période de moins d’une seconde. Si vous le faites, hello SDK montre une trace avec l’erreur de hello et réinitialise automatiquement toohello par défaut, zéro seconde. Cette hello tooreport de déclencheurs hello SDK se connecte en temps réel.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview
