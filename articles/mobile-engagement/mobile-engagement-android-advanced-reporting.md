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
# <a name="advanced-reporting-with-engagement-on-android"></a><span data-ttu-id="0a589-103">Génération de rapports avancés avec Engagement sur Android</span><span class="sxs-lookup"><span data-stu-id="0a589-103">Advanced Reporting with Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0a589-104">Windows universel</span><span class="sxs-lookup"><span data-stu-id="0a589-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="0a589-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="0a589-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="0a589-106">iOS</span><span class="sxs-lookup"><span data-stu-id="0a589-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="0a589-107">Android</span><span class="sxs-lookup"><span data-stu-id="0a589-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="0a589-108">Cette rubrique décrit des scénarios de génération de rapports supplémentaires dans votre application Android.</span><span class="sxs-lookup"><span data-stu-id="0a589-108">This topic describes additional reporting scenarios in your Android application.</span></span> <span data-ttu-id="0a589-109">Vous pouvez appliquer ces options de toohello application créé Bonjour [mise en route](mobile-engagement-android-get-started.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="0a589-109">You can apply these options toohello app created in hello [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a589-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0a589-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

<span data-ttu-id="0a589-111">didacticiel Hello vous terminé a été délibérément simple et directe, mais il sont des options que vous pouvez choisir avancées.</span><span class="sxs-lookup"><span data-stu-id="0a589-111">hello tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span></span>

## <a name="modifying-your-activity-classes"></a><span data-ttu-id="0a589-112">Modification de vos classes `Activity`</span><span class="sxs-lookup"><span data-stu-id="0a589-112">Modifying your `Activity` classes</span></span>
<span data-ttu-id="0a589-113">Bonjour [didacticiel de mise en route](mobile-engagement-android-get-started.md), vous n’aviez toodo a été toomake votre `*Activity` sous-classes héritent hello correspondant `Engagement*Activity` classes.</span><span class="sxs-lookup"><span data-stu-id="0a589-113">In hello [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had toodo was toomake your `*Activity` subclasses inherit from hello corresponding `Engagement*Activity` classes.</span></span> <span data-ttu-id="0a589-114">Par exemple, si votre activité héritée étendait `ListActivity`, vous deviez faire en sorte qu’elle étende `EngagementListActivity`.</span><span class="sxs-lookup"><span data-stu-id="0a589-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a589-115">Lorsque vous utilisez `EngagementListActivity` ou `EngagementExpandableListActivity`, assurez-vous que tout appel trop`requestWindowFeature(...);` est effectuée avant l’appel de hello trop`super.onCreate(...);`, sinon un incident se produit.</span><span class="sxs-lookup"><span data-stu-id="0a589-115">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call too`requestWindowFeature(...);` is made before hello call too`super.onCreate(...);`, otherwise a crash occurs.</span></span>
> 
> 

<span data-ttu-id="0a589-116">Vous pouvez trouver ces classes Bonjour `src` dossier, puis les copier dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="0a589-116">You can find these classes in hello `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="0a589-117">classes de Hello figurent également dans hello **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="0a589-117">hello classes are also in hello **JavaDoc**.</span></span>

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="0a589-118">Méthode alternative : appelez `startActivity()` et `endActivity()` manuellement</span><span class="sxs-lookup"><span data-stu-id="0a589-118">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="0a589-119">Si vous ne pouvez pas ou ne souhaitez pas que toooverload votre `Activity` classes, vous pouvez à la place commencer et se terminer vos activités en appelant hello `EngagementAgent`de méthodes directement.</span><span class="sxs-lookup"><span data-stu-id="0a589-119">If you cannot or do not want toooverload your `Activity` classes, you can instead start and end your activities by calling hello `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a589-120">Hello du SDK Android n’appelle jamais hello `endActivity()` méthode, même lorsque l’application hello est fermée (sur Android, les applications ne sont jamais fermées).</span><span class="sxs-lookup"><span data-stu-id="0a589-120">hello Android SDK never calls hello `endActivity()` method, even when hello application is closed (on Android, applications are never closed).</span></span> <span data-ttu-id="0a589-121">Par conséquent, il est *hautement* recommandé toocall hello `startActivity()` méthode Bonjour `onResume` rappel de *tous les* vos activités et hello `endActivity()` méthode Bonjour `onPause()` rappel de *tous les* vos activités.</span><span class="sxs-lookup"><span data-stu-id="0a589-121">Thus, it is *HIGHLY* recommended toocall hello `startActivity()` method in hello `onResume` callback of *ALL* your activities, and hello `endActivity()` method in hello `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="0a589-122">Il s’agit de toobe moyen hello uniquement assurer que les sessions ne sont pas divulguées.</span><span class="sxs-lookup"><span data-stu-id="0a589-122">This is hello only way toobe sure that sessions are not leaked.</span></span> <span data-ttu-id="0a589-123">Si une session est perdue, hello service d’Engagement déconnecte jamais hello Engagement principal (étant donné que le service de hello reste connecté en tant qu’une session est en attente).</span><span class="sxs-lookup"><span data-stu-id="0a589-123">If a session is leaked, hello Engagement service never disconnects from hello Engagement backend (since hello service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="0a589-124">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="0a589-124">Here is an example:</span></span>

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

<span data-ttu-id="0a589-125">Cet exemple est semblable toohello `EngagementActivity` classe et ses variantes, dont le code source est fourni dans hello `src` dossier.</span><span class="sxs-lookup"><span data-stu-id="0a589-125">This example is similar toohello `EngagementActivity` class and its variants, whose source code is provided in hello `src` folder.</span></span>

## <a name="using-applicationoncreate"></a><span data-ttu-id="0a589-126">Utilisation de Application.onCreate()</span><span class="sxs-lookup"><span data-stu-id="0a589-126">Using Application.onCreate()</span></span>
<span data-ttu-id="0a589-127">Tout code que vous placez dans `Application.onCreate()` et dans une autre application de rappels est exécutée pour les processus de tous les votre application, y compris le service d’Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="0a589-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including hello Engagement service.</span></span> <span data-ttu-id="0a589-128">Elle peut avoir des effets secondaires indésirables, comme les allocations de mémoire inutiles et les threads de processus de hello Engagement, ou en double diffusion récepteurs ou des services.</span><span class="sxs-lookup"><span data-stu-id="0a589-128">It may have unwanted side effects, like unneeded memory allocations and threads in hello Engagement's process, or duplicate broadcast receivers or services.</span></span>

<span data-ttu-id="0a589-129">Si vous substituez `Application.onCreate()`, nous vous recommandons d’ajouter des hello suivant extrait de code au début de hello de votre `Application.onCreate()` fonction :</span><span class="sxs-lookup"><span data-stu-id="0a589-129">If you override `Application.onCreate()`, we recommend adding hello following code snippet at hello beginning of your `Application.onCreate()` function:</span></span>

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

<span data-ttu-id="0a589-130">Vous pouvez effectuer hello même chose pour `Application.onTerminate()`, `Application.onLowMemory()`, et `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="0a589-130">You can do hello same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="0a589-131">Vous pouvez également étendre `EngagementApplication` au lieu de l’extension `Application`: hello rappel `Application.onCreate()` hello vérification de processus et les appels `Application.onApplicationProcessCreate()` uniquement si le processus actuel de hello n’est pas hello un hello Engagement service d’hébergement, hello mêmes règles s’appliquent pour Bonjour autres rappels.</span><span class="sxs-lookup"><span data-stu-id="0a589-131">You can also extend `EngagementApplication` instead of extending `Application`: hello callback `Application.onCreate()` does hello process check and calls `Application.onApplicationProcessCreate()` only if hello current process is not hello one hosting hello Engagement service, hello same rules apply for hello other callbacks.</span></span>

## <a name="tags-in-hello-androidmanifestxml-file"></a><span data-ttu-id="0a589-132">Balises dans le fichier AndroidManifest.xml hello</span><span class="sxs-lookup"><span data-stu-id="0a589-132">Tags in hello AndroidManifest.xml file</span></span>
<span data-ttu-id="0a589-133">Dans la balise de service hello dans le fichier AndroidManifest.xml hello, hello `android:label` attribut permet de vous toochoose hello nom de service de l’Engagement de hello tel qu’il apparaît aux utilisateurs de tooend l’écran hello « Services en cours d’exécution » de leur téléphone.</span><span class="sxs-lookup"><span data-stu-id="0a589-133">In hello service tag in hello AndroidManifest.xml file, hello `android:label` attribute allows you toochoose hello name of hello Engagement service as it appears tooend users in hello "Running services" screen of their phone.</span></span> <span data-ttu-id="0a589-134">Nous vous recommandons de définir cet attribut trop`"<Your application name>Service"` (par exemple, `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="0a589-134">We recommended setting this attribute too`"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span></span>

<span data-ttu-id="0a589-135">En spécifiant hello `android:process` attribut garantit que hello Engagement service s’exécute dans son propre processus (en cours d’exécution Engagement Bonjour même processus que votre application effectue votre thread principal / l’interface utilisateur potentiellement moins sensible).</span><span class="sxs-lookup"><span data-stu-id="0a589-135">Specifying hello `android:process` attribute ensures that hello Engagement service runs in its own process (running Engagement in hello same process as your application makes your main/UI thread potentially less responsive).</span></span>

## <a name="building-with-proguard"></a><span data-ttu-id="0a589-136">Génération avec ProGuard</span><span class="sxs-lookup"><span data-stu-id="0a589-136">Building with ProGuard</span></span>
<span data-ttu-id="0a589-137">Si vous générez votre package d’application avec ProGuard, vous devez tookeep certaines classes.</span><span class="sxs-lookup"><span data-stu-id="0a589-137">If you build your application package with ProGuard, you need tookeep some classes.</span></span> <span data-ttu-id="0a589-138">Vous pouvez utiliser hello suivant extrait de configuration :</span><span class="sxs-lookup"><span data-stu-id="0a589-138">You can use hello following configuration snippet:</span></span>

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
