---
title: Comment utiliser l'API Engagement sur Android
description: Dernier SDK Android - Comment utiliser l'API Engagement sur Android
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 09b62659-82ae-4a55-8784-fca0b6b22eaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: article
ms.date: 07/25/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: d353cd2fe47c54a0282cc5bb1b22b4a56e0cd82c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-android"></a><span data-ttu-id="a5e9c-103">Comment utiliser l'API Engagement sur Android</span><span class="sxs-lookup"><span data-stu-id="a5e9c-103">How to Use the Engagement API on Android</span></span>
<span data-ttu-id="a5e9c-104">Ce document vient compléter le document [Options de génération de rapports avancés pour le Kit de développement logiciel (SDK) Azure Mobile Engagement pour Android](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="a5e9c-104">This document is an add-on to the document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="a5e9c-105">Il fournit des informations détaillées sur l'utilisation de l'API Engagement pour signaler les statistiques de votre application.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-105">It provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="a5e9c-106">N'oubliez pas que si vous voulez qu'Engagement ne crée des rapports que sur les sessions, les activités, les blocages et les informations techniques de votre application, le plus simple est de faire hériter vos sous-classes `Activity` de la classe correspondante `EngagementActivity`.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-106">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Activity` sub-classes inherit from the corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="a5e9c-107">Si vous souhaitez aller plus loin, par exemple si vous avez besoin de signaler des événements, des erreurs et des travaux spécifiques à l'application, ou si vous devez signaler les activités de votre application d'une manière différente de celle implémentée dans les classes `EngagementActivity`, vous devez utiliser l'API Engagement.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-107">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementActivity` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="a5e9c-108">L'API Engagement est fournie par la classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="a5e9c-108">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="a5e9c-109">Une instance de cette classe peut être récupérée en appelant la méthode statique `EngagementAgent.getInstance(Context)` (notez que l'objet `EngagementAgent` retourné est un singleton).</span><span class="sxs-lookup"><span data-stu-id="a5e9c-109">An instance of this class can be retrieved by calling the `EngagementAgent.getInstance(Context)` static method (note that the `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="a5e9c-110">Concepts liés à Engagement</span><span class="sxs-lookup"><span data-stu-id="a5e9c-110">Engagement concepts</span></span>
<span data-ttu-id="a5e9c-111">Les sections qui suivent affinent les [concepts Mobile Engagement](mobile-engagement-concepts.md)courants pour la plateforme Android.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for the Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="a5e9c-112">`Session` et `Activity`</span><span class="sxs-lookup"><span data-stu-id="a5e9c-112">`Session` and `Activity`</span></span>
<span data-ttu-id="a5e9c-113">Si l’utilisateur reste inactif plus de quelques secondes entre deux *activités*, sa séquence *d’activités* est fractionnée en deux *sessions* distinctes.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-113">If the user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="a5e9c-114">Ces quelques secondes constituent le « délai d'expiration de session ».</span><span class="sxs-lookup"><span data-stu-id="a5e9c-114">These few seconds are called the "session timeout".</span></span>

<span data-ttu-id="a5e9c-115">Une *activité* est généralement associée à un écran de l’application, c’est-à-dire que *l’activité* démarre quand l’écran s’affiche et s’arrête quand l’écran est fermé. C’est le cas quand le SDK Engagement est intégré à l’aide des classes `EngagementActivity`.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-115">An *activity* is usually associated with one screen of the application, that is to say the *activity* starts when the screen is displayed and stops when the screen is closed: this is the case when the Engagement SDK is integrated by using the `EngagementActivity` classes.</span></span>

<span data-ttu-id="a5e9c-116">Mais les *activités* peuvent également être contrôlées manuellement à l'aide de l'API Engagement.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-116">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="a5e9c-117">Cela permet de fractionner un écran donné en plusieurs sous-parties pour obtenir plus d'informations sur l'utilisation de cet écran (par exemple la fréquence et la durée d'utilisation des boîtes de dialogue dans cet écran).</span><span class="sxs-lookup"><span data-stu-id="a5e9c-117">This allows to split a given screen in several sub parts to get more details about the usage of this screen (for example to known how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="a5e9c-118">Rapports d'activités</span><span class="sxs-lookup"><span data-stu-id="a5e9c-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a5e9c-119">Vous n'êtes pas obligé de signaler les activités décrites dans cette section si vous utilisez la classe `EngagementActivity` et ses variantes, comme expliqué dans le document Comment intégrer Engagement à Android.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-119">You don't need to report activities like described in this section if you are using the `EngagementActivity` class and its variants as explained in the How to Integrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="a5e9c-120">L'utilisateur démarre une nouvelle activité</span><span class="sxs-lookup"><span data-stu-id="a5e9c-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing the current activity is required for Reach to display in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="a5e9c-121">Vous devez appeler `startActivity()` chaque fois que l'activité utilisateur change.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-121">You need to call `startActivity()` each time the user activity changes.</span></span> <span data-ttu-id="a5e9c-122">Le premier appel à cette fonction démarre une nouvelle session utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-122">The first call to this function starts a new user session.</span></span>

<span data-ttu-id="a5e9c-123">Le meilleur moment pour appeler cette fonction est à chaque rappel de l'activité `onResume` .</span><span class="sxs-lookup"><span data-stu-id="a5e9c-123">The best place to call this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="a5e9c-124">L'utilisateur met fin à l'activité en cours</span><span class="sxs-lookup"><span data-stu-id="a5e9c-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="a5e9c-125">Vous devez appeler `endActivity()` au moins une fois quand l'utilisateur termine sa dernière activité.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-125">You need to call `endActivity()` at least once when the user finishes his last activity.</span></span> <span data-ttu-id="a5e9c-126">Cela indique au SDK Engagement que l'utilisateur est inactif et que la session utilisateur doit être fermée à la fin du délai d'expiration de session (si vous appelez `startActivity()` avant l'expiration de la session, la session est simplement reprise).</span><span class="sxs-lookup"><span data-stu-id="a5e9c-126">This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `startActivity()` before the session timeout expires, the session is simply resumed).</span></span>

<span data-ttu-id="a5e9c-127">Le meilleur moment pour appeler cette fonction est à chaque rappel de l'activité `onPause` .</span><span class="sxs-lookup"><span data-stu-id="a5e9c-127">The best place to call this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="a5e9c-128">Rapports d'événements</span><span class="sxs-lookup"><span data-stu-id="a5e9c-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="a5e9c-129">Événements de session</span><span class="sxs-lookup"><span data-stu-id="a5e9c-129">Session events</span></span>
<span data-ttu-id="a5e9c-130">Les événements de session servent généralement à signaler les actions effectuées par un utilisateur lors de sa session.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-130">Session events are usually used to report the actions performed by a user during his session.</span></span>

<span data-ttu-id="a5e9c-131">**Exemple sans données supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="a5e9c-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="a5e9c-132">**Exemple avec des données supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="a5e9c-132">**Example with extra data:**</span></span>

            public MyActivity extends EngagementActivity {
              [...]
              @Override
              public boolean onMenuItemSelected(int featureId, MenuItem item) {
                Bundle extras = new Bundle();
                extras.putInt("id", item.getItemId());
                getEngagementAgent().sendSessionEvent("menu_selected", extras);
              }
              [...]
            }

### <a name="standalone-events"></a><span data-ttu-id="a5e9c-133">Événements autonomes</span><span class="sxs-lookup"><span data-stu-id="a5e9c-133">Standalone Events</span></span>
<span data-ttu-id="a5e9c-134">Contrairement aux événements de session, les événements autonomes peuvent se produire en dehors du contexte d'une session.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-134">Contrary to session events, standalone events can occur outside of the context of a session.</span></span>

<span data-ttu-id="a5e9c-135">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="a5e9c-135">**Example:**</span></span>

<span data-ttu-id="a5e9c-136">Supposons que vous voulez signaler les événements qui se produisent quand un récepteur de diffusion est déclenché :</span><span class="sxs-lookup"><span data-stu-id="a5e9c-136">Suppose you want to report events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="a5e9c-137">Rapports d'erreurs</span><span class="sxs-lookup"><span data-stu-id="a5e9c-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="a5e9c-138">Erreurs de session</span><span class="sxs-lookup"><span data-stu-id="a5e9c-138">Session errors</span></span>
<span data-ttu-id="a5e9c-139">Les erreurs de session servent généralement à signaler les erreurs affectant l'utilisateur lors de sa session.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-139">Session errors are usually used to report the errors impacting the user during his session.</span></span>

<span data-ttu-id="a5e9c-140">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="a5e9c-140">**Example:**</span></span>

            /** The user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* The user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a><span data-ttu-id="a5e9c-141">Erreurs autonomes</span><span class="sxs-lookup"><span data-stu-id="a5e9c-141">Standalone errors</span></span>
<span data-ttu-id="a5e9c-142">Contrairement aux erreurs de session, les erreurs autonomes peuvent se produire en dehors du contexte d'une session.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-142">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

<span data-ttu-id="a5e9c-143">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="a5e9c-143">**Example:**</span></span>

<span data-ttu-id="a5e9c-144">L'exemple suivant montre comment signaler une erreur chaque fois que la mémoire est insuffisante sur le téléphone pendant l'exécution de votre application.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-144">The following example shows how to report an error whenever the memory becomes low on the phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="a5e9c-145">Rapports de travaux</span><span class="sxs-lookup"><span data-stu-id="a5e9c-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="a5e9c-146">Exemple</span><span class="sxs-lookup"><span data-stu-id="a5e9c-146">Example</span></span>
<span data-ttu-id="a5e9c-147">Supposons que vous voulez créer un rapport de la durée de votre processus de connexion :</span><span class="sxs-lookup"><span data-stu-id="a5e9c-147">Suppose you want to report the duration of your login process:</span></span>

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context to call the Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="a5e9c-148">Signaler les erreurs lors d'un travail</span><span class="sxs-lookup"><span data-stu-id="a5e9c-148">Report Errors during a Job</span></span>
<span data-ttu-id="a5e9c-149">Les erreurs peuvent être associées à un travail en cours d'exécution plutôt qu'à la session utilisateur en cours.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-149">Errors can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="a5e9c-150">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="a5e9c-150">**Example:**</span></span>

<span data-ttu-id="a5e9c-151">Supposons que vous voulez signaler une erreur pendant votre connexion :</span><span class="sxs-lookup"><span data-stu-id="a5e9c-151">Suppose you want to report an error during you login process:</span></span>

<span data-ttu-id="a5e9c-152">[...] public void signIn(Context context, ...) {</span><span class="sxs-lookup"><span data-stu-id="a5e9c-152">[...] public void signIn(Context context, ...) {</span></span>

              /* We need an Android context to call the Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try to sign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report the error to Engagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="a5e9c-153">Rapports d'événements pendant une tâche</span><span class="sxs-lookup"><span data-stu-id="a5e9c-153">Reporting Events during a job</span></span>
<span data-ttu-id="a5e9c-154">Les événements peuvent être associés à un travail en cours d'exécution au lieu de se rapporter à la session utilisateur en cours.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-154">Events can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="a5e9c-155">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="a5e9c-155">**Example:**</span></span>

<span data-ttu-id="a5e9c-156">Supposons que nous disposons d'un réseau social et que nous utilisons une tâche pour signaler la durée totale pendant laquelle l'utilisateur est connecté au serveur.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-156">Suppose we have a social network, and we use a job to report the total time during which the user is connected to the server.</span></span> <span data-ttu-id="a5e9c-157">L'utilisateur peut rester connecté en arrière-plan même quand il utilise une autre application ou que le téléphone est en veille, dans ce cas, il n'y a pas de session.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-157">The user can stay connected in background even when he's using another application or when the phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="a5e9c-158">L'utilisateur peut recevoir des messages de ses amis : il s'agit d'un événement de tâche.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-158">The user can receive messages from his friends, this is a job event.</span></span>

            [...]
            public void signin(Context context, ...) {
              [...Sign in code...]
              EngagementAgent.getInstance(context).startJob("connection", null);
            }
            [...]
            public void signout(Context context) {
              [...Sign out code...]
              EngagementAgent.getInstance(context).endJob("connection");
            }
            [...]
            public void onMessageReceived(Context context) {
              [...Notify in status bar...]
              EngagementAgent.getInstance(context).sendJobEvent("message_received", "connection", null);
            }
            [...]

## <a name="extra-parameters"></a><span data-ttu-id="a5e9c-159">Paramètres supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a5e9c-159">Extra parameters</span></span>
<span data-ttu-id="a5e9c-160">Des données arbitraires peuvent être associées à des événements, des erreurs, des activités et des tâches.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-160">Arbitrary data can be attached to events, errors, activities and jobs.</span></span>

<span data-ttu-id="a5e9c-161">Ces données peuvent être structurées, elles utilisent la classe Bundle d'Android (en fait, elles font office de paramètres extras dans les Intents Android).</span><span class="sxs-lookup"><span data-stu-id="a5e9c-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="a5e9c-162">Notez qu'une classe Bundle peut contenir des tableaux ou d'autres instances de classe Bundle.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a5e9c-163">Si vous insérez les paramètres parcelables ou sérialisables, vérifiez que leur méthode `toString()` est implémentée de sorte à retourner une chaîne lisible par l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented to return a human-readable string.</span></span> <span data-ttu-id="a5e9c-164">Les classes sérialisables qui contiennent des champs non temporaires non sérialisables entraînent le blocage d'Android à l'appel de `bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="a5e9c-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="a5e9c-165">Les matrices creuses dans les paramètres extras ne sont pas prises en charge, autrement dit, elles ne sont pas sérialisées sous forme de tableau.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="a5e9c-166">Vous devez les convertir en tableaux standard avant de les utiliser dans les paramètres extras.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="a5e9c-167">Exemple</span><span class="sxs-lookup"><span data-stu-id="a5e9c-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="a5e9c-168">Limites</span><span class="sxs-lookup"><span data-stu-id="a5e9c-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="a5e9c-169">de clés symétriques</span><span class="sxs-lookup"><span data-stu-id="a5e9c-169">Keys</span></span>
<span data-ttu-id="a5e9c-170">Chaque clé dans `Bundle` doit correspondre à l'expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="a5e9c-170">Each key in the `Bundle` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="a5e9c-171">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="a5e9c-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="a5e9c-172">Taille</span><span class="sxs-lookup"><span data-stu-id="a5e9c-172">Size</span></span>
<span data-ttu-id="a5e9c-173">Les paramètres extras sont limités à **1024** caractères par appel (une fois encodés au format JSON par le service Engagement).</span><span class="sxs-lookup"><span data-stu-id="a5e9c-173">Extras are limited to **1024** characters per call (once encoded in JSON by the Engagement service).</span></span>

<span data-ttu-id="a5e9c-174">Dans l'exemple précédent, le JSON envoyé au serveur fait 58 caractères :</span><span class="sxs-lookup"><span data-stu-id="a5e9c-174">In the previous example, the JSON sent to the server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="a5e9c-175">Rapports d'informations sur l'application</span><span class="sxs-lookup"><span data-stu-id="a5e9c-175">Reporting Application Information</span></span>
<span data-ttu-id="a5e9c-176">Vous pouvez signaler manuellement les informations de suivi (ou toutes autres informations spécifiques aux applications) à l'aide de la fonction `sendAppInfo()` .</span><span class="sxs-lookup"><span data-stu-id="a5e9c-176">You can manually report tracking information (or any other application specific information) using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="a5e9c-177">Notez que ces informations peuvent être envoyées de façon incrémentielle : seule la dernière valeur d'une clé donnée sera conservée pour un périphérique donné.</span><span class="sxs-lookup"><span data-stu-id="a5e9c-177">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="a5e9c-178">À l'instar des paramètres extras des événements, la classe Bundle est utilisée pour récupérer les informations de l'application. Notez que les tableaux ou les sous-groupes seront considérés comme des chaînes plates (à l'aide de la sérialisation JSON).</span><span class="sxs-lookup"><span data-stu-id="a5e9c-178">Like event extras, the Bundle class is used to abstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="a5e9c-179">Exemple</span><span class="sxs-lookup"><span data-stu-id="a5e9c-179">Example</span></span>
<span data-ttu-id="a5e9c-180">Voici un exemple de code pour envoyer des informations sur la date de naissance et le sexe de l'utilisateur :</span><span class="sxs-lookup"><span data-stu-id="a5e9c-180">Here is a code sample to send user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="a5e9c-181">Limites</span><span class="sxs-lookup"><span data-stu-id="a5e9c-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="a5e9c-182">de clés symétriques</span><span class="sxs-lookup"><span data-stu-id="a5e9c-182">Keys</span></span>
<span data-ttu-id="a5e9c-183">Chaque clé dans `Bundle` doit correspondre à l'expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="a5e9c-183">Each key in the `Bundle` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="a5e9c-184">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="a5e9c-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="a5e9c-185">Taille</span><span class="sxs-lookup"><span data-stu-id="a5e9c-185">Size</span></span>
<span data-ttu-id="a5e9c-186">Les informations de l'application sont limitées à **1024** caractères par appel (une fois encodées au format JSON par le service Engagement).</span><span class="sxs-lookup"><span data-stu-id="a5e9c-186">Application information are limited to **1024** characters per call (once encoded in JSON by the Engagement service).</span></span>

<span data-ttu-id="a5e9c-187">Dans l'exemple précédent, le JSON envoyé au serveur fait 44 caractères :</span><span class="sxs-lookup"><span data-stu-id="a5e9c-187">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
