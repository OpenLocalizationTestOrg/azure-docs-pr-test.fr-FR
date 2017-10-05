---
title: "Options de génération de rapports avancés pour le SDK Azure Mobile Engagement pour Android"
description: "Décrit comment générer des rapports avancés visant à capturer des analyses pour le SDK Azure Mobile Engagement pour Android"
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
ms.openlocfilehash: 2a1445afa2c2fca1a31ad9c012b9c8a917ebf65c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-reporting-with-engagement-on-android"></a><span data-ttu-id="b0ae7-103">Génération de rapports avancés avec Engagement sur Android</span><span class="sxs-lookup"><span data-stu-id="b0ae7-103">Advanced Reporting with Engagement on Android</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b0ae7-104">Windows universel</span><span class="sxs-lookup"><span data-stu-id="b0ae7-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="b0ae7-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="b0ae7-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="b0ae7-106">iOS</span><span class="sxs-lookup"><span data-stu-id="b0ae7-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="b0ae7-107">Android</span><span class="sxs-lookup"><span data-stu-id="b0ae7-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="b0ae7-108">Cette rubrique décrit des scénarios de génération de rapports supplémentaires dans votre application Android.</span><span class="sxs-lookup"><span data-stu-id="b0ae7-108">This topic describes additional reporting scenarios in your Android application.</span></span> <span data-ttu-id="b0ae7-109">Vous pouvez appliquer ces options à l’application créée dans le didacticiel [Prise en main](mobile-engagement-android-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="b0ae7-109">You can apply these options to the app created in the [Getting Started](mobile-engagement-android-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0ae7-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="b0ae7-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-android-prereqs.md)]

<span data-ttu-id="b0ae7-111">Le didacticiel que vous avez suivi était délibérément direct et simple, mais vous disposez également d’options avancées.</span><span class="sxs-lookup"><span data-stu-id="b0ae7-111">The tutorial you completed was deliberately direct and simple, but there are advanced options you can choose.</span></span>

## <a name="modifying-your-activity-classes"></a><span data-ttu-id="b0ae7-112">Modification de vos classes `Activity`</span><span class="sxs-lookup"><span data-stu-id="b0ae7-112">Modifying your `Activity` classes</span></span>
<span data-ttu-id="b0ae7-113">Dans le didacticiel de [Prise en main](mobile-engagement-android-get-started.md), il vous suffisait de configurer vos sous-classes `*Activity` pour qu’elles héritent des classes `Engagement*Activity` correspondantes.</span><span class="sxs-lookup"><span data-stu-id="b0ae7-113">In the [Getting Started tutorial](mobile-engagement-android-get-started.md), all you had to do was to make your `*Activity` subclasses inherit from the corresponding `Engagement*Activity` classes.</span></span> <span data-ttu-id="b0ae7-114">Par exemple, si votre activité héritée étendait `ListActivity`, vous deviez faire en sorte qu’elle étende `EngagementListActivity`.</span><span class="sxs-lookup"><span data-stu-id="b0ae7-114">For example, if your legacy activity extended `ListActivity`, you would make it extend `EngagementListActivity`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0ae7-115">Lorsque vous utilisez `EngagementListActivity` ou `EngagementExpandableListActivity`, assurez-vous que tout appel à `requestWindowFeature(...);` est effectué avant l'appel à `super.onCreate(...);`. Dans le cas contraire, un incident se produira.</span><span class="sxs-lookup"><span data-stu-id="b0ae7-115">When using `EngagementListActivity` or `EngagementExpandableListActivity`, make sure any call to `requestWindowFeature(...);` is made before the call to `super.onCreate(...);`, otherwise a crash occurs.</span></span>
> 
> 

<span data-ttu-id="b0ae7-116">Vous trouverez ces classes dans le dossier `src`. Vous pourrez les copier dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="b0ae7-116">You can find these classes in the `src` folder, and can copy them into your project.</span></span> <span data-ttu-id="b0ae7-117">Les classes se trouvent également dans **JavaDoc**.</span><span class="sxs-lookup"><span data-stu-id="b0ae7-117">The classes are also in the **JavaDoc**.</span></span>

## <a name="alternate-method-call-startactivity-and-endactivity-manually"></a><span data-ttu-id="b0ae7-118">Méthode alternative : appelez `startActivity()` et `endActivity()` manuellement</span><span class="sxs-lookup"><span data-stu-id="b0ae7-118">Alternate method: call `startActivity()` and `endActivity()` manually</span></span>
<span data-ttu-id="b0ae7-119">Si vous ne pouvez pas ou ne voulez pas surcharger vos classes `Activity`, vous pouvez démarrer et terminer vos activités en appelant les méthodes d’`EngagementAgent` directement.</span><span class="sxs-lookup"><span data-stu-id="b0ae7-119">If you cannot or do not want to overload your `Activity` classes, you can instead start and end your activities by calling the `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b0ae7-120">Le Kit de développement logiciel (SDK) Android n'appelle jamais la méthode `endActivity()`, même quand l'application est fermée (sur Android, les applications ne sont jamais fermées).</span><span class="sxs-lookup"><span data-stu-id="b0ae7-120">The Android SDK never calls the `endActivity()` method, even when the application is closed (on Android, applications are never closed).</span></span> <span data-ttu-id="b0ae7-121">Il est donc *FORTEMENT* recommandé d’appeler la méthode `startActivity()` dans le rappel `onResume` de *TOUTES* vos activités, et la méthode `endActivity()` dans le rappel `onPause()` de *TOUTES* vos activités.</span><span class="sxs-lookup"><span data-stu-id="b0ae7-121">Thus, it is *HIGHLY* recommended to call the `startActivity()` method in the `onResume` callback of *ALL* your activities, and the `endActivity()` method in the `onPause()` callback of *ALL* your activities.</span></span> <span data-ttu-id="b0ae7-122">Il s'agit de la seule façon d'empêcher la fuite de sessions.</span><span class="sxs-lookup"><span data-stu-id="b0ae7-122">This is the only way to be sure that sessions are not leaked.</span></span> <span data-ttu-id="b0ae7-123">Dans le cas d'une fuite de session, le service Engagement n'est jamais déconnecté du serveur principal d'Engagement (étant donné que le service reste connecté tant qu'une session est en cours).</span><span class="sxs-lookup"><span data-stu-id="b0ae7-123">If a session is leaked, the Engagement service never disconnects from the Engagement backend (since the service stays connected as long as a session is pending).</span></span>
> 
> 

<span data-ttu-id="b0ae7-124">Voici un exemple :</span><span class="sxs-lookup"><span data-stu-id="b0ae7-124">Here is an example:</span></span>

    public class MyActivity extends Some3rdPartyActivity
    {
      @Override
      protected void onResume()
      {
        super.onResume();
        String activityNameOnEngagement = EngagementAgentUtils.buildEngagementActivityName(getClass()); // Uses short class name and removes "Activity" at the end.
        EngagementAgent.getInstance(this).startActivity(this, activityNameOnEngagement, null);
      }

      @Override
      protected void onPause()
      {
        super.onPause();
        EngagementAgent.getInstance(this).endActivity();
      }
    }

<span data-ttu-id="b0ae7-125">Cet exemple est similaire à la classe `EngagementActivity` et à ses variantes, dont le code source est fourni dans le dossier `src`.</span><span class="sxs-lookup"><span data-stu-id="b0ae7-125">This example is similar to the `EngagementActivity` class and its variants, whose source code is provided in the `src` folder.</span></span>

## <a name="using-applicationoncreate"></a><span data-ttu-id="b0ae7-126">Utilisation de Application.onCreate()</span><span class="sxs-lookup"><span data-stu-id="b0ae7-126">Using Application.onCreate()</span></span>
<span data-ttu-id="b0ae7-127">Tout code que vous placez dans `Application.onCreate()` et dans les autres rappels d’application sera exécuté pour l’ensemble des processus de votre application, notamment le service Engagement.</span><span class="sxs-lookup"><span data-stu-id="b0ae7-127">Any code you place in `Application.onCreate()` and in other application callbacks is run for all your application's processes, including the Engagement service.</span></span> <span data-ttu-id="b0ae7-128">Cela peut avoir des effets indésirables, tels que des allocations de mémoire et des threads inutiles dans le processus Engagement, ou des récepteurs ou services de diffusion en double.</span><span class="sxs-lookup"><span data-stu-id="b0ae7-128">It may have unwanted side effects, like unneeded memory allocations and threads in the Engagement's process, or duplicate broadcast receivers or services.</span></span>

<span data-ttu-id="b0ae7-129">Si vous remplacez `Application.onCreate()`, nous vous recommandons d’ajouter l’extrait de code suivant au début de la fonction `Application.onCreate()` :</span><span class="sxs-lookup"><span data-stu-id="b0ae7-129">If you override `Application.onCreate()`, we recommend adding the following code snippet at the beginning of your `Application.onCreate()` function:</span></span>

     public void onCreate()
     {
       if (EngagementAgentUtils.isInDedicatedEngagementProcess(this))
         return;

       ... Your code...
     }

<span data-ttu-id="b0ae7-130">Vous pouvez faire la même chose pour `Application.onTerminate()`, `Application.onLowMemory()` et `Application.onConfigurationChanged(...)`.</span><span class="sxs-lookup"><span data-stu-id="b0ae7-130">You can do the same thing for `Application.onTerminate()`, `Application.onLowMemory()`, and `Application.onConfigurationChanged(...)`.</span></span>

<span data-ttu-id="b0ae7-131">Vous pouvez également étendre `EngagementApplication` au lieu d'étendre `Application` : le rappel `Application.onCreate()` effectue la vérification du processus et appelle `Application.onApplicationProcessCreate()` uniquement si le processus actuel n'est pas celui qui héberge le service Engagement. Les mêmes règles s'appliquent pour les autres rappels.</span><span class="sxs-lookup"><span data-stu-id="b0ae7-131">You can also extend `EngagementApplication` instead of extending `Application`: the callback `Application.onCreate()` does the process check and calls `Application.onApplicationProcessCreate()` only if the current process is not the one hosting the Engagement service, the same rules apply for the other callbacks.</span></span>

## <a name="tags-in-the-androidmanifestxml-file"></a><span data-ttu-id="b0ae7-132">Balises dans le fichier AndroidManifest.xml</span><span class="sxs-lookup"><span data-stu-id="b0ae7-132">Tags in the AndroidManifest.xml file</span></span>
<span data-ttu-id="b0ae7-133">Dans la balise service du fichier AndroidManifest.xml, l’attribut `android:label` vous permet de choisir le nom du service Engagement tel qu’il apparaîtra aux utilisateurs finaux dans l’écran Services en cours d’exécution de leur téléphone.</span><span class="sxs-lookup"><span data-stu-id="b0ae7-133">In the service tag in the AndroidManifest.xml file, the `android:label` attribute allows you to choose the name of the Engagement service as it appears to end users in the "Running services" screen of their phone.</span></span> <span data-ttu-id="b0ae7-134">Nous vous recommandons d’affecter la valeur `"<Your application name>Service"` à cet attribut (par exemple `"AcmeFunGameService"`).</span><span class="sxs-lookup"><span data-stu-id="b0ae7-134">We recommended setting this attribute to `"<Your application name>Service"` (for example, `"AcmeFunGameService"`).</span></span>

<span data-ttu-id="b0ae7-135">La spécification de l'attribut `android:process` permet au service Engagement d'être exécuté dans le cadre de son propre processus (l'exécution d'Engagement dans le même processus que votre application peut rendre votre thread principal/d'interface utilisateur moins réactif).</span><span class="sxs-lookup"><span data-stu-id="b0ae7-135">Specifying the `android:process` attribute ensures that the Engagement service runs in its own process (running Engagement in the same process as your application makes your main/UI thread potentially less responsive).</span></span>

## <a name="building-with-proguard"></a><span data-ttu-id="b0ae7-136">Génération avec ProGuard</span><span class="sxs-lookup"><span data-stu-id="b0ae7-136">Building with ProGuard</span></span>
<span data-ttu-id="b0ae7-137">Si vous générez votre package d'application avec ProGuard, vous devez conserver certaines classes.</span><span class="sxs-lookup"><span data-stu-id="b0ae7-137">If you build your application package with ProGuard, you need to keep some classes.</span></span> <span data-ttu-id="b0ae7-138">Vous pouvez utiliser l'extrait de configuration suivant :</span><span class="sxs-lookup"><span data-stu-id="b0ae7-138">You can use the following configuration snippet:</span></span>

    -keep public class * extends android.os.IInterface
    -keep class com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity$EngagementReachContentJS {
    <methods>;
     }
