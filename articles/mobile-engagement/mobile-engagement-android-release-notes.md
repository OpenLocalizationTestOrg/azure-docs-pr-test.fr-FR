---
title: "aaaAzure intégration du Kit de développement logiciel Android Mobile Engagement"
description: "Dernières mises à jour et procédures du SDK Android pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 585341f9-3f39-459a-af42-864e400a0128
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 16b098198674c49567d720d0c01d984cb763ed8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes"></a>Notes de publication

## <a name="431-07172017"></a>4.3.1 (07/17/2017)
* Résoudre un incident peut se produire rarement lors de l’appel `EngagementAgentUtils.isInDedicatedEngagementProcess`, qui est également utilisé par hello `EngagementApplication` classe.

## <a name="430-06272017"></a>4.3.0 (06/27/2017)
* Android 8 prise en charge (versions précédentes de hello SDK ne fonctionnera pas sur Android 8).
* Aucune autre dépendance sur la bibliothèque de prise en charge.
* Supprimez la classe `EngagementFragmentActivity`.
* Échéance trop[limites de l’exécution en arrière-plan](https://developer.android.com/preview/features/background.html) sur 8 Android, les journaux en arrière-plan peuvent être retardées jusqu'à ce que l’utilisateur de hello interagit avec les appareils hello, cela aura un impact sur les campagnes de Push **remis** et **Notification système affichée** statistiques retardées si l’appareil de hello était en état de veille (hello notification restent affichée, est en anneau et faire vibrer en temps réel sans problème).
* Échéance trop[arrière-plan emplacement limites](https://developer.android.com/preview/features/background-location-limits.html), emplacement en temps réel de hello en arrière-plan se verra pas fréquemment sur 8 Android.

## <a name="424-03302017"></a>4.2.4 (03/30/2017)
* Corrigez la notification dans l’application des couleurs de texte sur 7 Android toobe même hello en tant que les versions antérieures d’Android.

## <a name="423-08102016"></a>4.2.3 (08/10/2016)
* Plus aucun verrou Wi-Fi.
* Résolution d'un blocage lors de l’appel de getDeviceId avant init (bogue introduit dans 4.2.0).

## <a name="422-05172016"></a>4.2.2 (05/17/2016)
* Améliorations de la stabilité.

## <a name="421-05102016"></a>4.2.1 (05/10/2016)
* Sécurité : Désactivation de l’accès aux fichiers locaux dans les vues web.
* Sécurité : Suppression de la classe `EngagementPreferenceActivity` qui étend la classe `PreferenceActivity` obsolète et non sécurisée.
* Sécurité : portée d’activités sont maintenant documentées toouse `exported="false"`, cet indicateur peut également être utilisé dans les versions précédentes du Kit de développement logiciel.

## <a name="420-03112016"></a>4.2.0 (03/11/2016)
* Hello Kit de développement logiciel est désormais sous licence MIT.
* Autorise la spécification d’un identificateur d’appareil personnalisé au moment de l’initialisation du Kit de développement logiciel (SDK).

## <a name="415-02012016"></a>4.1.5 (01/02/2016)
* Améliorations de la stabilité.

## <a name="414-01262016"></a>4.1.4 (26/01/2016)
* Améliorations de la stabilité.

## <a name="413-1292015"></a>4.1.3 (12/9/2015)
* Améliorations de la stabilité.

## <a name="412-11252015"></a>4.1.2 (25/11/2015)
* Améliorations de la stabilité.

## <a name="411-11042015"></a>4.1.1 (11/04/2015)
* Améliorations de la stabilité.

## <a name="410-08252015"></a>4.1.0 (25/08/2015)
* Gestion du nouveau modèle d’autorisation pour Android M.
* Vous pouvez désormais configurer les fonctionnalités de localisation lors de l’exécution au lieu d’utiliser `AndroidManifest.xml`.
* Résolution d’un bogue d’autorisation : si vous utilisez `ACCESS_FINE_LOCATION`, `ACCESS_COARSE_LOCATION` n’est plus nécessaire.
* Améliorations de la stabilité.

## <a name="400-07062015"></a>4.0.0 (06/07/2015)
* Protocole interne change toomake analytique et push plus fiable.
* Push natif (GCM/ADM) est désormais également utilisé pour des notifications de l’application vous devez configurer les informations d’identification de push natif hello pour n’importe quel type de campagne push.
* Correction de la notification de la vue d’ensemble : elle ne s’affichait que 10 s après avoir été transmise.
* Corriger un bogue dans l’affichage web : en cliquant sur un lien également en cours d’exécution hello URL de l’action par défaut.
* Résoudre un incident rares liées toolocal gestion du stockage.
* Correction de la gestion des chaînes de configuration dynamique.
* Mise à jour du CLUF.

## <a name="300-02172015"></a>3.0.0 (17/02/2015)
* Version initiale d'Azure Engagement Mobile
* La configuration d'appId est remplacée par la configuration d'une chaîne de connexion.
* Supprimé API toosend et recevoir des messages XMPP arbitraires à partir des entités XMPP arbitraires.
* Supprimé toosend d’API et de recevoir des messages entre les appareils.
* Améliorations de sécurité.
* Suppression du suivi de Google Play et SmartAd.

