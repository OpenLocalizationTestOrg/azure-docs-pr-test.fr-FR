---
title: aaaHow tooUse hello API Engagement sur Android
description: "Dernier Kit de développement logiciel Android - comment tooUse hello API Engagement sur Android"
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
ms.openlocfilehash: e0b2d484616c0c7874e77c5283d94c3063949ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-android"></a><span data-ttu-id="e9be7-103">Comment tooUse hello API Engagement sur Android</span><span class="sxs-lookup"><span data-stu-id="e9be7-103">How tooUse hello Engagement API on Android</span></span>
<span data-ttu-id="e9be7-104">Ce document est un document toohello de module complémentaire [avancé Reporting des options pour le Kit de développement Android Mobile Engagement](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="e9be7-104">This document is an add-on toohello document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="e9be7-105">Elle fournit en profondeur plus d’informations sur comment toouse hello Engagement API tooreport vos statistiques de l’application.</span><span class="sxs-lookup"><span data-stu-id="e9be7-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="e9be7-106">N’oubliez pas que si vous souhaitez uniquement Engagement tooreport sessions, activités, blocages et des informations techniques de votre application, puis hello plus simple consiste toomake tous vos `Activity` sous-classes héritent hello correspondant `EngagementActivity` classe.</span><span class="sxs-lookup"><span data-stu-id="e9be7-106">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Activity` sub-classes inherit from hello corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="e9be7-107">Si vous voulez toodo plus, par exemple, si vous avez besoin tooreport les événements d’application spécifique, les erreurs et les tâches, ou si vous avez tooreport activités de votre application d’une manière différente d’une implémentation dans hello hello `EngagementActivity` des classes, vous devez toouse hello API d’engagement.</span><span class="sxs-lookup"><span data-stu-id="e9be7-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementActivity` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="e9be7-108">API d’Engagement Hello est fournie par hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="e9be7-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="e9be7-109">Une instance de cette classe peut être récupérée en appelant hello `EngagementAgent.getInstance(Context)` méthode statique (Notez que hello `EngagementAgent` objet retourné est un singleton).</span><span class="sxs-lookup"><span data-stu-id="e9be7-109">An instance of this class can be retrieved by calling hello `EngagementAgent.getInstance(Context)` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="e9be7-110">Concepts liés à Engagement</span><span class="sxs-lookup"><span data-stu-id="e9be7-110">Engagement concepts</span></span>
<span data-ttu-id="e9be7-111">parties suivantes Hello affiner hello commun [Concepts d’Engagement Mobile](mobile-engagement-concepts.md), pour la plateforme de Android hello.</span><span class="sxs-lookup"><span data-stu-id="e9be7-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for hello Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="e9be7-112">`Session` et `Activity`</span><span class="sxs-lookup"><span data-stu-id="e9be7-112">`Session` and `Activity`</span></span>
<span data-ttu-id="e9be7-113">Si l’utilisateur de hello reste inactif entre deux de plus de quelques secondes *activités*, puis sa séquence de *activités* est fractionné en deux distinctes *sessions*.</span><span class="sxs-lookup"><span data-stu-id="e9be7-113">If hello user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="e9be7-114">Ces quelques secondes sont appelés hello « session timeout ».</span><span class="sxs-lookup"><span data-stu-id="e9be7-114">These few seconds are called hello "session timeout".</span></span>

<span data-ttu-id="e9be7-115">Un *activité* est généralement associé à un écran de l’application hello, qui est toosay hello *activité* démarre lorsque l’écran hello s’affiche et s’arrête lors de la fermeture de l’écran hello : il s’agit de hello cas, lorsque Kit de développement logiciel Engagement Hello est intégré à l’aide de hello `EngagementActivity` classes.</span><span class="sxs-lookup"><span data-stu-id="e9be7-115">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementActivity` classes.</span></span>

<span data-ttu-id="e9be7-116">Mais *activités* peut également être contrôlée manuellement à l’aide des API de l’Engagement de hello.</span><span class="sxs-lookup"><span data-stu-id="e9be7-116">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="e9be7-117">Cela permet à un écran toosplit dans plusieurs tooget de parties sub plus de détails sur hello d’utilisation de l’écran (par exemple tooknown la fréquence et la durée pendant laquelle les boîtes de dialogue sont utilisés à l’intérieur de cet écran).</span><span class="sxs-lookup"><span data-stu-id="e9be7-117">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="e9be7-118">Rapports d'activités</span><span class="sxs-lookup"><span data-stu-id="e9be7-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e9be7-119">Vous ne devez pas tooreport des activités, telles que décrites dans cette section si vous utilisez hello `EngagementActivity` classe et ses variantes, comme expliqué comment Bonjour tooIntegrate Engagement sur document Android.</span><span class="sxs-lookup"><span data-stu-id="e9be7-119">You don't need tooreport activities like described in this section if you are using hello `EngagementActivity` class and its variants as explained in hello How tooIntegrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="e9be7-120">L'utilisateur démarre une nouvelle activité</span><span class="sxs-lookup"><span data-stu-id="e9be7-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="e9be7-121">Vous devez toocall `startActivity()` chaque activité utilisateur hello change.</span><span class="sxs-lookup"><span data-stu-id="e9be7-121">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="e9be7-122">Hello premier appel toothis fonction démarre une nouvelle session de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e9be7-122">hello first call toothis function starts a new user session.</span></span>

<span data-ttu-id="e9be7-123">Hello meilleures toocall place cette fonction se trouve sur chaque activité `onResume` rappel.</span><span class="sxs-lookup"><span data-stu-id="e9be7-123">hello best place toocall this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="e9be7-124">L'utilisateur met fin à l'activité en cours</span><span class="sxs-lookup"><span data-stu-id="e9be7-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="e9be7-125">Vous devez toocall `endActivity()` au moins une fois lorsque hello utilisateur a fini de sa dernière activité.</span><span class="sxs-lookup"><span data-stu-id="e9be7-125">You need toocall `endActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="e9be7-126">Cela permet d’informer hello SDK Engagement qu’utilisateur de hello est actuellement inactive et que session d’utilisateur hello devez toobe fermés une fois hello expiration de la session expire (si vous appelez `startActivity()` avant l’expiration du délai d’expiration de session hello, hello simplement la reprise de session).</span><span class="sxs-lookup"><span data-stu-id="e9be7-126">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `startActivity()` before hello session timeout expires, hello session is simply resumed).</span></span>

<span data-ttu-id="e9be7-127">Hello meilleures toocall place cette fonction se trouve sur chaque activité `onPause` rappel.</span><span class="sxs-lookup"><span data-stu-id="e9be7-127">hello best place toocall this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="e9be7-128">Rapports d'événements</span><span class="sxs-lookup"><span data-stu-id="e9be7-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="e9be7-129">Événements de session</span><span class="sxs-lookup"><span data-stu-id="e9be7-129">Session events</span></span>
<span data-ttu-id="e9be7-130">Événements de session sont des actions de hello tooreport utilisés généralement effectuées par un utilisateur lors de sa session.</span><span class="sxs-lookup"><span data-stu-id="e9be7-130">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="e9be7-131">**Exemple sans données supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="e9be7-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="e9be7-132">**Exemple avec des données supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="e9be7-132">**Example with extra data:**</span></span>

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

### <a name="standalone-events"></a><span data-ttu-id="e9be7-133">Événements autonomes</span><span class="sxs-lookup"><span data-stu-id="e9be7-133">Standalone Events</span></span>
<span data-ttu-id="e9be7-134">Toosession contraires événements, les événements autonome peuvent se produire en dehors du contexte hello d’une session.</span><span class="sxs-lookup"><span data-stu-id="e9be7-134">Contrary toosession events, standalone events can occur outside of hello context of a session.</span></span>

<span data-ttu-id="e9be7-135">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="e9be7-135">**Example:**</span></span>

<span data-ttu-id="e9be7-136">Supposons que vous souhaitez tooreport les événements qui se produit quand un récepteur de diffusion est déclenché :</span><span class="sxs-lookup"><span data-stu-id="e9be7-136">Suppose you want tooreport events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="e9be7-137">Rapports d'erreurs</span><span class="sxs-lookup"><span data-stu-id="e9be7-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="e9be7-138">Erreurs de session</span><span class="sxs-lookup"><span data-stu-id="e9be7-138">Session errors</span></span>
<span data-ttu-id="e9be7-139">Session erreurs sont généralement utilisés tooreport hello affecter l’utilisateur de hello lors de sa session.</span><span class="sxs-lookup"><span data-stu-id="e9be7-139">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="e9be7-140">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="e9be7-140">**Example:**</span></span>

            /** hello user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* hello user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a><span data-ttu-id="e9be7-141">Erreurs autonomes</span><span class="sxs-lookup"><span data-stu-id="e9be7-141">Standalone errors</span></span>
<span data-ttu-id="e9be7-142">Erreurs de toosession contraires, autonome erreurs peuvent se produire en dehors du contexte hello d’une session.</span><span class="sxs-lookup"><span data-stu-id="e9be7-142">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

<span data-ttu-id="e9be7-143">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="e9be7-143">**Example:**</span></span>

<span data-ttu-id="e9be7-144">Hello suivant montre comment tooreport une erreur chaque fois que la mémoire de hello devient faible sur le téléphone hello lors de l’exécution de votre application est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="e9be7-144">hello following example shows how tooreport an error whenever hello memory becomes low on hello phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="e9be7-145">Rapports de travaux</span><span class="sxs-lookup"><span data-stu-id="e9be7-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="e9be7-146">Exemple</span><span class="sxs-lookup"><span data-stu-id="e9be7-146">Example</span></span>
<span data-ttu-id="e9be7-147">Supposons que vous voulez tooreport hello la durée de votre processus de connexion :</span><span class="sxs-lookup"><span data-stu-id="e9be7-147">Suppose you want tooreport hello duration of your login process:</span></span>

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="e9be7-148">Signaler les erreurs lors d'un travail</span><span class="sxs-lookup"><span data-stu-id="e9be7-148">Report Errors during a Job</span></span>
<span data-ttu-id="e9be7-149">Les erreurs peuvent être associée tooa travail au lieu d’être en cours d’exécution liées de session utilisateur en cours toohello.</span><span class="sxs-lookup"><span data-stu-id="e9be7-149">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="e9be7-150">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="e9be7-150">**Example:**</span></span>

<span data-ttu-id="e9be7-151">Supposons que vous vouliez tooreport une erreur au cours de vous connecter processus :</span><span class="sxs-lookup"><span data-stu-id="e9be7-151">Suppose you want tooreport an error during you login process:</span></span>

<span data-ttu-id="e9be7-152">[...] public void signIn(Context context, ...) {</span><span class="sxs-lookup"><span data-stu-id="e9be7-152">[...] public void signIn(Context context, ...) {</span></span>

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try toosign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report hello error tooEngagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="e9be7-153">Rapports d'événements pendant une tâche</span><span class="sxs-lookup"><span data-stu-id="e9be7-153">Reporting Events during a job</span></span>
<span data-ttu-id="e9be7-154">Les événements peuvent être associée tooa travail au lieu d’être en cours d’exécution liées de session utilisateur en cours toohello.</span><span class="sxs-lookup"><span data-stu-id="e9be7-154">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="e9be7-155">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="e9be7-155">**Example:**</span></span>

<span data-ttu-id="e9be7-156">Supposons que nous disposons d’un réseau social, nous utilisons un temps total hello tooreport travail pendant le hello utilisateur est connecté toohello server.</span><span class="sxs-lookup"><span data-stu-id="e9be7-156">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="e9be7-157">utilisateur de Hello peut rester connecté en arrière-plan même quand il utilise une autre application ou lorsque le téléphone de hello est en veille, donc il n’existe aucune session.</span><span class="sxs-lookup"><span data-stu-id="e9be7-157">hello user can stay connected in background even when he's using another application or when hello phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="e9be7-158">Hello peuvent recevoir des messages de ses amis, il s’agit d’un événement de tâche.</span><span class="sxs-lookup"><span data-stu-id="e9be7-158">hello user can receive messages from his friends, this is a job event.</span></span>

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

## <a name="extra-parameters"></a><span data-ttu-id="e9be7-159">Paramètres supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e9be7-159">Extra parameters</span></span>
<span data-ttu-id="e9be7-160">Données arbitraires peuvent être attachés tooevents, les erreurs, les activités et les tâches.</span><span class="sxs-lookup"><span data-stu-id="e9be7-160">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="e9be7-161">Ces données peuvent être structurées, elles utilisent la classe Bundle d'Android (en fait, elles font office de paramètres extras dans les Intents Android).</span><span class="sxs-lookup"><span data-stu-id="e9be7-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="e9be7-162">Notez qu'une classe Bundle peut contenir des tableaux ou d'autres instances de classe Bundle.</span><span class="sxs-lookup"><span data-stu-id="e9be7-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e9be7-163">Si vous placez dans les paramètres parcelable ou sérialisables, vérifiez que leurs `toString()` méthode est implémentée tooreturn une chaîne contrôlable de visu.</span><span class="sxs-lookup"><span data-stu-id="e9be7-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented tooreturn a human-readable string.</span></span> <span data-ttu-id="e9be7-164">Les classes sérialisables qui contiennent des champs non temporaires non sérialisables entraînent le blocage d'Android à l'appel de `bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="e9be7-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="e9be7-165">Les matrices creuses dans les paramètres extras ne sont pas prises en charge, autrement dit, elles ne sont pas sérialisées sous forme de tableau.</span><span class="sxs-lookup"><span data-stu-id="e9be7-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="e9be7-166">Vous devez les convertir en tableaux standard avant de les utiliser dans les paramètres extras.</span><span class="sxs-lookup"><span data-stu-id="e9be7-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="e9be7-167">Exemple</span><span class="sxs-lookup"><span data-stu-id="e9be7-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="e9be7-168">Limites</span><span class="sxs-lookup"><span data-stu-id="e9be7-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="e9be7-169">Clés</span><span class="sxs-lookup"><span data-stu-id="e9be7-169">Keys</span></span>
<span data-ttu-id="e9be7-170">Chaque clé Bonjour `Bundle` doit correspondre à hello expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="e9be7-170">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="e9be7-171">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="e9be7-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="e9be7-172">Taille</span><span class="sxs-lookup"><span data-stu-id="e9be7-172">Size</span></span>
<span data-ttu-id="e9be7-173">Fonctionnalités supplémentaires sont trop limitées**1024** caractères par appel (une fois encodées au format JSON par le service d’Engagement hello).</span><span class="sxs-lookup"><span data-stu-id="e9be7-173">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="e9be7-174">Bonjour exemple précédent, hello JSON envoyé toohello serveur est 58 caractères :</span><span class="sxs-lookup"><span data-stu-id="e9be7-174">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="e9be7-175">Rapports d'informations sur l'application</span><span class="sxs-lookup"><span data-stu-id="e9be7-175">Reporting Application Information</span></span>
<span data-ttu-id="e9be7-176">Vous pouvez signaler manuellement le suivi des informations (ou toutes les autres informations spécifiques aux applications) à l’aide de hello `sendAppInfo()` (fonction).</span><span class="sxs-lookup"><span data-stu-id="e9be7-176">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="e9be7-177">Notez que ces informations peuvent être envoyées de façon incrémentielle : uniquement hello valeur la plus récente d’une clé spécifique est conservé pour un périphérique donné.</span><span class="sxs-lookup"><span data-stu-id="e9be7-177">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="e9be7-178">Comme événement extras, hello classe de regroupement est utilisée tooabstract informations de l’application, notez que les tableaux ou inférieur regroupe sera traité en tant que chaînes plats (à l’aide de la sérialisation JSON).</span><span class="sxs-lookup"><span data-stu-id="e9be7-178">Like event extras, hello Bundle class is used tooabstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="e9be7-179">Exemple</span><span class="sxs-lookup"><span data-stu-id="e9be7-179">Example</span></span>
<span data-ttu-id="e9be7-180">Voici un sexe de l’utilisateur toosend exemple code et la date de naissance :</span><span class="sxs-lookup"><span data-stu-id="e9be7-180">Here is a code sample toosend user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="e9be7-181">limites</span><span class="sxs-lookup"><span data-stu-id="e9be7-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="e9be7-182">Clés</span><span class="sxs-lookup"><span data-stu-id="e9be7-182">Keys</span></span>
<span data-ttu-id="e9be7-183">Chaque clé Bonjour `Bundle` doit correspondre à hello expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="e9be7-183">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="e9be7-184">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="e9be7-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="e9be7-185">Taille</span><span class="sxs-lookup"><span data-stu-id="e9be7-185">Size</span></span>
<span data-ttu-id="e9be7-186">Informations sur l’application sont trop limitées**1024** caractères par appel (une fois encodées au format JSON par le service d’Engagement hello).</span><span class="sxs-lookup"><span data-stu-id="e9be7-186">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="e9be7-187">Bonjour exemple précédent, hello JSON envoyé toohello serveur est 44 caractères :</span><span class="sxs-lookup"><span data-stu-id="e9be7-187">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
