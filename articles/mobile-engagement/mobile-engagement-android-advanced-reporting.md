---
title: aaaAdvanced options pour Azure Mobile Engagement Android SDK reporting
description: "Décrit comment toodo avancé reporting toocapture analytique pour Azure Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7da7abd5-19d6-4892-94d8-818e5424b2cd
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 5c8f4ea36c54715f4e09fd43c96132c15019a71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a>Génération de rapports avancés avec Engagement sur Android
> [!div class="op_single_selector"]
> * [Windows universel](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

Cette rubrique décrit des scénarios de génération de rapports supplémentaires dans votre application Android. Vous pouvez appliquer ces options de toohello application créé Bonjour [mise en route](mobile-engagement-android-get-started.md) didacticiel.

## <a name="prerequisites"></a>Composants requis
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

didacticiel Hello vous terminé a été délibérément simple et directe, mais il sont des options que vous pouvez choisir avancées.

## <a name="modifying-your-activity-classes"></a>Modification de vos classes `Activity`
Bonjour [didacticiel de mise en route](mobile-engagement-android-get-started.md), vous n’aviez toodo a été toomake votre `*Activity` sous-classes héritent hello correspondant `Engagement*Activity` classes. Par exemple, si votre activité héritée étendait `ListActivity`, vous deviez faire en sorte qu’elle étende `EngagementListActivity`.

> [!IMPORTANT]
> Lorsque vous utilisez `EngagementListActivity` ou `EngagementExpandableListActivity`, assurez-vous que tout appel trop`requestWindowFeature(...);` est effectuée avant l’appel de hello trop`super.onCreate(...);`, sinon un incident se produit.
> 
> 

Vous pouvez trouver ces classes Bonjour `src` dossier, puis les copier dans votre projet. classes de Hello figurent également dans hello **JavaDoc**.

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a>Méthode alternative : appelez `startActivity()` et `endActivity()` manuellement
Si vous ne pouvez pas ou ne souhaitez pas que toooverload votre `Activity` classes, vous pouvez à la place commencer et se terminer vos activités en appelant hello `EngagementAgent`de méthodes directement.

> [!IMPORTANT]
> Hello du SDK Android n’appelle jamais hello `endActivity()` méthode, même lorsque l’application hello est fermée (sur Android, les applications ne sont jamais fermées). Par conséquent, il est *hautement* recommandé toocall hello `startActivity()` méthode Bonjour `onResume` rappel de *tous les* vos activités et hello `endActivity()` méthode Bonjour `onPause()` rappel de *tous les* vos activités. Il s’agit de toobe moyen hello uniquement assurer que les sessions ne sont pas divulguées. Si une session est perdue, hello service d’Engagement déconnecte jamais hello Engagement principal (étant donné que le service de hello reste connecté en tant qu’une session est en attente).
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

Cet exemple est semblable toohello `EngagementActivity` classe et ses variantes, dont le code source est fourni dans hello `src` dossier.

## <a name="using-applicationoncreate"></a>Utilisation de Application.onCreate()
Tout code que vous placez dans `Application.onCreate()` et dans une autre application de rappels est exécutée pour les processus de tous les votre application, y compris le service d’Engagement hello. Elle peut avoir des effets secondaires indésirables, comme les allocations de mémoire inutiles et les threads de processus de hello Engagement, ou en double diffusion récepteurs ou des services.

Si vous substituez `Application.onCreate()`, nous vous recommandons d’ajouter des hello suivant extrait de code au début de hello de votre `Application.onCreate()` fonction :

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

Vous pouvez effectuer hello même chose pour `Application.onTerminate()`, `Application.onLowMemory()`, et `Application.onConfigurationChanged(...)`.

Vous pouvez également étendre `EngagementApplication` au lieu de l’extension `Application`: hello rappel `Application.onCreate()` hello vérification de processus et les appels `Application.onApplicationProcessCreate()` uniquement si le processus actuel de hello n’est pas hello un hello Engagement service d’hébergement, hello mêmes règles s’appliquent pour Bonjour autres rappels.

## <a name="tags-in-hello-androidmanifestxml-file"></a>Balises dans le fichier AndroidManifest.xml hello
Dans la balise de service hello dans le fichier AndroidManifest.xml hello, hello `android:label` attribut permet de vous toochoose hello nom de service de l’Engagement de hello tel qu’il apparaît aux utilisateurs de tooend l’écran hello « Services en cours d’exécution » de leur téléphone. Nous vous recommandons de définir cet attribut trop`"<Your application name>Service"` (par exemple, `"AcmeFunGameService"`).

En spécifiant hello `android:process` attribut garantit que hello Engagement service s’exécute dans son propre processus (en cours d’exécution Engagement Bonjour même processus que votre application effectue votre thread principal / l’interface utilisateur potentiellement moins sensible).

## <a name="building-with-proguard"></a>Génération avec ProGuard
Si vous générez votre package d’application avec ProGuard, vous devez tookeep certaines classes. Vous pouvez utiliser hello suivant extrait de configuration :

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
