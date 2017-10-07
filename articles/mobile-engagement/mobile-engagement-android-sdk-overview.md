---
title: "aaaAndroid intégration du Kit de développement logiciel pour Azure Mobile Engagement"
description: "Décrit comment toointegrate Kit de développement logiciel Azure Mobile Engagement dans des applications Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a91ed04f-f3ce-4692-a6dd-b56a28d7dee8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo;ricksal
ms.openlocfilehash: 0c63bfaf673abbda7ea498390f8282c43e2fb8df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="android-sdk-integration-for-azure-mobile-engagement"></a>Intégration du SDK Android pour Azure Mobile Engagement
> [!div class="op_single_selector"]
> * [Windows universel](mobile-engagement-windows-store-sdk-overview.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-sdk-overview.md)
> * [iOS](mobile-engagement-ios-sdk-overview.md)
> * [Android](mobile-engagement-android-sdk-overview.md)
> 
> 

Ce document décrit tous les hello intégration et configuration options disponibles pour Azure Mobile Engagement Android SDK.

## <a name="prerequisites"></a>Composants requis
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="advanced-features"></a>Fonctionnalités avancées
### <a name="reporting-features"></a>Fonctionnalités de génération de rapports
Vous pouvez ajouter les fonctionnalités suivantes :

1. [Options de génération de rapports avancés](mobile-engagement-android-advanced-reporting.md)
2. [Options de génération de rapports d’emplacement](mobile-engagement-android-location-reporting.md)
3. [Options de configuration avancées](mobile-engagement-android-advanced-configuration.md)

### <a name="notifications"></a>Notifications :
[Comment toointegrate portée (Notifications) dans votre application Android](mobile-engagement-android-integrate-engagement-reach.md)

1. Google Cloud Messaging (GCM) : [comment tooIntegrate GCM avec Mobile Engagement](mobile-engagement-android-gcm-integrate.md)
2. Messagerie d’appareil Amazon (ADM) : [comment tooIntegrate ADM avec Mobile Engagement](mobile-engagement-android-adm-integrate.md)

### <a name="tag-plan-implementation"></a>Implémentation du plan de balise :
[Comment toouse hello avancé Mobile Engagement marquage API dans votre application Android](mobile-engagement-android-use-engagement-api.md)

## <a name="release-notes"></a>Notes de publication

### <a name="431-07172017"></a>4.3.1 (07/17/2017)
* Résoudre un incident peut se produire rarement lors de l’appel `EngagementAgentUtils.isInDedicatedEngagementProcess`, qui est également utilisé par hello `EngagementApplication` classe.

### <a name="430-06272017"></a>4.3.0 (06/27/2017)
* Android 8 prise en charge (versions précédentes de hello SDK ne fonctionnera pas sur Android 8).
* Aucune autre dépendance sur la bibliothèque de prise en charge.
* Supprimez la classe `EngagementFragmentActivity`.
* Échéance trop[limites de l’exécution en arrière-plan](https://developer.android.com/preview/features/background.html) sur 8 Android, les journaux en arrière-plan peuvent être retardées jusqu'à ce que l’utilisateur de hello interagit avec les appareils hello, cela aura un impact sur les campagnes de Push **remis** et **Notification système affichée** statistiques retardées si l’appareil de hello était en état de veille (hello notification restent affichée, est en anneau et faire vibrer en temps réel sans problème).
* Échéance trop[arrière-plan emplacement limites](https://developer.android.com/preview/features/background-location-limits.html), emplacement en temps réel de hello en arrière-plan se verra pas fréquemment sur 8 Android.

Pour toutes les versions, consultez hello [terminer les notes de publication](mobile-engagement-android-release-notes.md).

## <a name="upgrade-procedures"></a>Procédures de mise à niveau
Si vous avez déjà intégré une version plus ancienne de notre kit de développement logiciel (SDK) dans votre application, consultez [Procédures de mise à niveau](mobile-engagement-android-upgrade-procedure.md).

