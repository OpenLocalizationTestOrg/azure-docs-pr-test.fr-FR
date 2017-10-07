---
title: configuration aaaAdvanced pour Azure Mobile Engagement Android SDK
description: "Décrit les hello notamment hello manifeste Android avec le SDK Android Azure Mobile Engagement des options de configuration avancées"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 37d2c09a-86fa-473d-8987-c7e35a0eb3e8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 10/04/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 757abf362021fd018f444cae6305524623e77062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-configuration-for-azure-mobile-engagement-android-sdk"></a>Configuration avancée pour le SDK Android pour Azure Mobile Engagement
> [!div class="op_single_selector"]
> * [Windows universel](mobile-engagement-windows-store-advanced-configuration.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-configuration.md)
>
>

Cette procédure décrit comment tooconfigure différentes options de configuration pour les applications Azure Mobile Engagement Android.

## <a name="prerequisites"></a>Composants requis
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

## <a name="permission-requirements"></a>Autorisations requises
Certaines options nécessitent des autorisations spécifiques qui sont répertoriées ici pour référence et en ligne dans la fonctionnalité spécifique de hello. Ajoutez ces toohello autorisations AndroidManifest.xml de votre projet immédiatement avant ou après hello `<application>` balise.

code d’autorisation Hello doit toolook hello suivante, où vous renseignez autorisation appropriée de hello à partir de la table hello qui suit.

    <uses-permission android:name="android.permission.[specific permission]"/>


| Autorisation | Quand l’utiliser |
| --- | --- |
| INTERNET |Obligatoire. Pour la génération de rapports de base |
| ACCESS_NETWORK_STATE |Obligatoire. Pour la génération de rapports de base |
| RECEIVE_BOOT_COMPLETED |Obligatoire. tooshow centre de notifications hello après le redémarrage de l’appareil |
| WAKE_LOCK |Recommandé. Active la collecte de données quand vous utilisez le Wi-Fi ou quand l’écran est éteint |
| VIBRATE |facultatif. Active la vibration lors de la réception des notifications |
| DOWNLOAD_WITHOUT_NOTIFICATION |facultatif. Active la Notification de la vue d’ensemble Android |
| WRITE_EXTERNAL_STORAGE |facultatif. Active la Notification de la vue d’ensemble Android |
| ACCESS_COARSE_LOCATION |facultatif. Active la génération de rapports d’emplacement en temps réel |
| ACCESS_FINE_LOCATION |facultatif. Active la génération de rapports sur l’emplacement GPS |

À partir d’Android M, [certaines autorisations sont gérées au moment de l’exécution](mobile-engagement-android-location-reporting.md#android-m-permissions).

Si vous utilisez déjà ``ACCESS_FINE_LOCATION``, vous avez tooalso utiliser ``ACCESS_COARSE_LOCATION``.

## <a name="android-manifest-configuration-options"></a>Options de configuration de manifeste Android
### <a name="crash-report"></a>Rapport d'incidents
rapports d’incidents toodisable, ajoutez le code entre hello `<application>` et `</application>` balises :

    <meta-data android:name="engagement:reportCrash" android:value="false"/>

### <a name="burst-threshold"></a>Seuil du mode rafale
Par défaut, les rapports de service d’Engagement hello journaux en temps réel. Si vos journaux d’état application varie fréquemment, il est mieux toobuffer hello journaux et tooreport à la fois à une base de temps réguliers (appelée « mode de croissance »). toodo, ajoutez ce code entre hello `<application>` et `</application>` balises :

    <meta-data android:name="engagement:burstThreshold" android:value="{interval between too bursts (in milliseconds)}"/>

Mode rafale augmente l’autonomie des batteries hello légèrement mais a un impact sur hello Engagement moniteur : durée des sessions et les travaux toute sont arrondis toohello rafale seuil (par conséquent, les sessions et les travaux plus court que le seuil de croissance hello n’est pas forcément visible). Votre seuil de rafale ne doit pas dépasser la valeur 30000 (30 s).

### <a name="session-timeout"></a>Délai d'expiration de session
 Vous pouvez terminer une activité en appuyant sur les hello **accueil** ou **précédent** clé, par définition téléphone hello inactif ou passer à une autre application. Par défaut, une session prend fin dix secondes après la fin de hello de sa dernière activité. Cela permet d’éviter un fractionnement de session chaque utilisateur hello se termine et retourne toohello application rapidement, ce qui peut se produire lorsque l’utilisateur de hello sélectionne une image, vérifie une notification, un etc.. Vous souhaiterez toomodify ce paramètre. toodo, ajoutez ce code entre hello `<application>` et `</application>` balises :

    <meta-data android:name="engagement:sessionTimeout" android:value="{session timeout (in milliseconds)}"/>

## <a name="disable-log-reporting"></a>Désactiver les rapports de suivi
### <a name="using-a-method-call"></a>En appelant une méthode
Si vous souhaitez toostop Engagement envoi de journaux, vous pouvez appeler :

    EngagementAgent.getInstance(context).setEnabled(false);

Cet appel est persistant : il utilise un fichier de préférences partagées.

Si l’Engagement est active lorsque vous appelez cette fonction, il peut prendre une minute pour hello service toostop. Toutefois, il ne sera pas lancer service hello en hello tous les prochaine fois que vous lancez application hello.

Vous pouvez activer le journal de création de rapports en appelant hello même fonction avec `true`.

### <a name="integration-in-your-own-preferenceactivity"></a>Intégration dans votre propre `PreferenceActivity`
Au lieu d'appeler cette fonction, vous pouvez également intégrer ce paramètre directement dans votre `PreferenceActivity`.

Vous pouvez configurer toouse Engagement vos préférences de fichier (avec le mode souhaité de hello) de hello `AndroidManifest.xml` de fichiers avec `application meta-data`:

* Hello `engagement:agent:settings:name` clé désigne toodefine utilisé hello du fichier de préférences partagées hello.
* Hello `engagement:agent:settings:mode` clé est en mode de hello toodefine utilisé du fichier de préférences partagées hello. Utilisez hello même mode en tant que dans votre `PreferenceActivity`. mode de Hello doit être passé en tant que nombre : Si vous utilisez une combinaison d’indicateurs de constantes dans votre code, vérifiez la valeur totale de hello.

Engagement toujours utilise hello `engagement:key` booléenne clé dans le fichier de préférences de hello pour gérer ce paramètre.

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
