---
title: aaaHow tooUse hello API Engagement sur Windows Phone Silverlight
description: Comment tooUse hello API Engagement sur Windows Phone Silverlight
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ae2ba2e8-f75b-4dee-a164-a7dd65d35a23
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1e84be95cc910be7f1227b4ae60eb483a1939284
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="1d048-103">Comment tooUse hello API Engagement sur Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="1d048-103">How tooUse hello Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="1d048-104">Ce document est un document toohello de module complémentaire [comment toointegrate Mobile Engagement dans votre application Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="1d048-104">This document is an add-on toohello document [How toointegrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="1d048-105">Elle fournit en profondeur plus d’informations sur comment toouse hello Engagement API tooreport vos statistiques de l’application.</span><span class="sxs-lookup"><span data-stu-id="1d048-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="1d048-106">Si vous souhaitez seulement Engagement tooreport sessions, activités, blocages et des informations techniques de votre application, puis hello la plus simple est de façon toomake tous les votre `PhoneApplicationPage` sous-classes héritent hello `EngagementPage` classe.</span><span class="sxs-lookup"><span data-stu-id="1d048-106">If you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="1d048-107">Si vous voulez toodo plus, par exemple, si vous avez besoin tooreport les événements d’application spécifique, les erreurs et les tâches, ou si vous avez tooreport activités de votre application d’une manière différente d’une implémentation dans hello hello `EngagementPage` des classes, vous devez toouse hello API d’engagement.</span><span class="sxs-lookup"><span data-stu-id="1d048-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="1d048-108">API d’Engagement Hello est fournie par hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="1d048-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="1d048-109">Vous pouvez accéder à des méthodes toothose via `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="1d048-109">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="1d048-110">Même si le module de l’agent hello n’a pas été initialisée, chaque API de toohello d’appel est différée et sera exécutée à nouveau lorsque l’agent de hello n’est disponible.</span><span class="sxs-lookup"><span data-stu-id="1d048-110">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="1d048-111">Concepts liés à Engagement</span><span class="sxs-lookup"><span data-stu-id="1d048-111">Engagement concepts</span></span>
<span data-ttu-id="1d048-112">Hello pièces suivantes affiner les Concepts d’Engagement Mobile hello pour la plateforme Windows Phone de hello.</span><span class="sxs-lookup"><span data-stu-id="1d048-112">hello following parts refine hello Mobile Engagement Concepts for hello Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="1d048-113">`Session` et `Activity`</span><span class="sxs-lookup"><span data-stu-id="1d048-113">`Session` and `Activity`</span></span>
<span data-ttu-id="1d048-114">Un *activité* est généralement associé à une page de l’application hello, qui est toosay hello *activité* démarre lorsque la page de hello et s’arrête lorsque la page de hello est fermé : il s’agit des cas hello si hello Engagement SDK est intégré à l’aide de hello `EngagementPage` classe.</span><span class="sxs-lookup"><span data-stu-id="1d048-114">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="1d048-115">Mais *activités* peut également être contrôlée manuellement à l’aide des API de l’Engagement de hello.</span><span class="sxs-lookup"><span data-stu-id="1d048-115">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="1d048-116">Cela permet à une page donnée toosplit dans plusieurs tooget de parties sub plus de détails sur hello d’utilisation de cette page (par exemple tooknown la fréquence et la durée pendant laquelle les boîtes de dialogue sont utilisés à l’intérieur de cette page).</span><span class="sxs-lookup"><span data-stu-id="1d048-116">This allows toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknown how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="1d048-117">Rapports d'activités</span><span class="sxs-lookup"><span data-stu-id="1d048-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="1d048-118">L'utilisateur démarre une nouvelle activité</span><span class="sxs-lookup"><span data-stu-id="1d048-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="1d048-119">Référence</span><span class="sxs-lookup"><span data-stu-id="1d048-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="1d048-120">Vous devez toocall `StartActivity()` chaque activité utilisateur hello change.</span><span class="sxs-lookup"><span data-stu-id="1d048-120">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="1d048-121">Hello premier appel toothis fonction démarre une nouvelle session de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1d048-121">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d048-122">Hello SDK appelle automatiquement la méthode de EndActivity hello lors de la fermeture de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="1d048-122">hello SDK automatically call hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="1d048-123">Par conséquent, il est vivement recommandé toocall hello StartActivity (méthode) chaque fois que l’activité hello de modification d’utilisateur hello et appel de tooNEVER hello méthode EndActivity, depuis l’appel de cette méthode force hello session active toobe s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="1d048-123">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user change, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="1d048-124">Exemple</span><span class="sxs-lookup"><span data-stu-id="1d048-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="1d048-125">L'utilisateur met fin à l'activité en cours</span><span class="sxs-lookup"><span data-stu-id="1d048-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="1d048-126">Référence</span><span class="sxs-lookup"><span data-stu-id="1d048-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="1d048-127">Vous devez toocall `EndActivity()` au moins une fois lorsque hello utilisateur a fini de sa dernière activité.</span><span class="sxs-lookup"><span data-stu-id="1d048-127">You need toocall `EndActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="1d048-128">Cela permet d’informer hello SDK Engagement qu’utilisateur de hello est actuellement inactive et que session d’utilisateur hello devez toobe fermés une fois hello expiration de la session expire (si vous appelez `StartActivity()` avant l’expiration du délai d’expiration de session hello, session de hello est simplement la suite).</span><span class="sxs-lookup"><span data-stu-id="1d048-128">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `StartActivity()` before hello session timeout expires, hello session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="1d048-129">Exemple</span><span class="sxs-lookup"><span data-stu-id="1d048-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="1d048-130">Rapports de travaux</span><span class="sxs-lookup"><span data-stu-id="1d048-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="1d048-131">Démarrer un travail</span><span class="sxs-lookup"><span data-stu-id="1d048-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="1d048-132">Référence</span><span class="sxs-lookup"><span data-stu-id="1d048-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="1d048-133">Vous pouvez utiliser des tâches certains tootrack hello sur une période de temps.</span><span class="sxs-lookup"><span data-stu-id="1d048-133">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="1d048-134">Exemple</span><span class="sxs-lookup"><span data-stu-id="1d048-134">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="1d048-135">Mettre fin à un travail</span><span class="sxs-lookup"><span data-stu-id="1d048-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="1d048-136">Référence</span><span class="sxs-lookup"><span data-stu-id="1d048-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="1d048-137">Dès qu’un objet d’un suivi par une tâche a été arrêtée, vous devez appeler la méthode de EndJob hello pour cette tâche, en fournissant le nom de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="1d048-137">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="1d048-138">Exemple</span><span class="sxs-lookup"><span data-stu-id="1d048-138">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="1d048-139">Rapports d'événements</span><span class="sxs-lookup"><span data-stu-id="1d048-139">Reporting Events</span></span>
<span data-ttu-id="1d048-140">Il existe trois types d'événements :</span><span class="sxs-lookup"><span data-stu-id="1d048-140">There is three types of events :</span></span>

* <span data-ttu-id="1d048-141">Événements autonomes</span><span class="sxs-lookup"><span data-stu-id="1d048-141">Standalone events</span></span>
* <span data-ttu-id="1d048-142">Événements de session</span><span class="sxs-lookup"><span data-stu-id="1d048-142">Session events</span></span>
* <span data-ttu-id="1d048-143">Événements de travail</span><span class="sxs-lookup"><span data-stu-id="1d048-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="1d048-144">Événements autonomes</span><span class="sxs-lookup"><span data-stu-id="1d048-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="1d048-145">Référence</span><span class="sxs-lookup"><span data-stu-id="1d048-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="1d048-146">Les événements autonome peuvent se produire en dehors du contexte hello d’une session.</span><span class="sxs-lookup"><span data-stu-id="1d048-146">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="1d048-147">Exemple</span><span class="sxs-lookup"><span data-stu-id="1d048-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="1d048-148">Événements de session</span><span class="sxs-lookup"><span data-stu-id="1d048-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="1d048-149">Référence</span><span class="sxs-lookup"><span data-stu-id="1d048-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="1d048-150">Événements de session sont des actions de hello tooreport utilisés généralement effectuées par un utilisateur lors de sa session.</span><span class="sxs-lookup"><span data-stu-id="1d048-150">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="1d048-151">Exemple</span><span class="sxs-lookup"><span data-stu-id="1d048-151">Example</span></span>
<span data-ttu-id="1d048-152">**Sans données :**</span><span class="sxs-lookup"><span data-stu-id="1d048-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="1d048-153">**Avec données :**</span><span class="sxs-lookup"><span data-stu-id="1d048-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="1d048-154">Événements de travail</span><span class="sxs-lookup"><span data-stu-id="1d048-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="1d048-155">Référence</span><span class="sxs-lookup"><span data-stu-id="1d048-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="1d048-156">Événements de travail sont des actions de hello tooreport utilisés généralement effectuées par un utilisateur lors d’un travail.</span><span class="sxs-lookup"><span data-stu-id="1d048-156">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="1d048-157">Exemple</span><span class="sxs-lookup"><span data-stu-id="1d048-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="1d048-158">Rapports d'erreurs</span><span class="sxs-lookup"><span data-stu-id="1d048-158">Reporting Errors</span></span>
<span data-ttu-id="1d048-159">Il existe trois types d'erreurs :</span><span class="sxs-lookup"><span data-stu-id="1d048-159">There is three types of errors :</span></span>

* <span data-ttu-id="1d048-160">Erreurs autonomes</span><span class="sxs-lookup"><span data-stu-id="1d048-160">Standalone errors</span></span>
* <span data-ttu-id="1d048-161">Erreurs de session</span><span class="sxs-lookup"><span data-stu-id="1d048-161">Session errors</span></span>
* <span data-ttu-id="1d048-162">Erreurs de travail</span><span class="sxs-lookup"><span data-stu-id="1d048-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="1d048-163">Erreurs autonomes</span><span class="sxs-lookup"><span data-stu-id="1d048-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="1d048-164">Référence</span><span class="sxs-lookup"><span data-stu-id="1d048-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="1d048-165">Erreurs de toosession contraires, autonome erreurs peuvent se produire en dehors du contexte hello d’une session.</span><span class="sxs-lookup"><span data-stu-id="1d048-165">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="1d048-166">Exemple</span><span class="sxs-lookup"><span data-stu-id="1d048-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="1d048-167">Erreurs de session</span><span class="sxs-lookup"><span data-stu-id="1d048-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="1d048-168">Référence</span><span class="sxs-lookup"><span data-stu-id="1d048-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="1d048-169">Session erreurs sont généralement utilisés tooreport hello affecter l’utilisateur de hello lors de sa session.</span><span class="sxs-lookup"><span data-stu-id="1d048-169">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="1d048-170">Exemple</span><span class="sxs-lookup"><span data-stu-id="1d048-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="1d048-171">Erreurs de travail</span><span class="sxs-lookup"><span data-stu-id="1d048-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="1d048-172">Référence</span><span class="sxs-lookup"><span data-stu-id="1d048-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="1d048-173">Les erreurs peuvent être associée tooa travail au lieu d’être en cours d’exécution liées de session utilisateur en cours toohello.</span><span class="sxs-lookup"><span data-stu-id="1d048-173">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="1d048-174">Exemple</span><span class="sxs-lookup"><span data-stu-id="1d048-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="1d048-175">Rapports d'incidents</span><span class="sxs-lookup"><span data-stu-id="1d048-175">Reporting Crashes</span></span>
<span data-ttu-id="1d048-176">l’agent de Hello fournit deux méthodes toodeal se bloque.</span><span class="sxs-lookup"><span data-stu-id="1d048-176">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="1d048-177">Envoyer une exception</span><span class="sxs-lookup"><span data-stu-id="1d048-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="1d048-178">Référence</span><span class="sxs-lookup"><span data-stu-id="1d048-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="1d048-179">Exemple</span><span class="sxs-lookup"><span data-stu-id="1d048-179">Example</span></span>
<span data-ttu-id="1d048-180">Vous pouvez envoyer une exception à tout moment en appelant :</span><span class="sxs-lookup"><span data-stu-id="1d048-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="1d048-181">Vous pouvez également utiliser une session d’engagement paramètre facultatif tooterminate hello en hello même temps que l’envoi de panne de hello.</span><span class="sxs-lookup"><span data-stu-id="1d048-181">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="1d048-182">Par conséquent, appelez le toodo :</span><span class="sxs-lookup"><span data-stu-id="1d048-182">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="1d048-183">Si vous procédez ainsi, les travaux et la session de hello va être fermée juste après l’envoi d’incident de hello.</span><span class="sxs-lookup"><span data-stu-id="1d048-183">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="1d048-184">Envoyer une exception non gérée</span><span class="sxs-lookup"><span data-stu-id="1d048-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="1d048-185">Référence</span><span class="sxs-lookup"><span data-stu-id="1d048-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="1d048-186">Engagement fournit également une méthode toosend non gérée exceptions.</span><span class="sxs-lookup"><span data-stu-id="1d048-186">Engagement also provides a method toosend unhandled exceptions.</span></span> <span data-ttu-id="1d048-187">Ceci est particulièrement utile lorsqu’il est utilisé à l’intérieur du Gestionnaire d’événements UnhandledException hello silverlight.</span><span class="sxs-lookup"><span data-stu-id="1d048-187">This is especially useful when used inside hello silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="1d048-188">Cette méthode sera **toujours** mettre fin à la session d’engagement hello et des travaux après avoir été appelé.</span><span class="sxs-lookup"><span data-stu-id="1d048-188">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="1d048-189">Exemple</span><span class="sxs-lookup"><span data-stu-id="1d048-189">Example</span></span>
<span data-ttu-id="1d048-190">Vous pouvez l’utiliser tooimplement votre propre gestionnaire UnhandledException (surtout si vous avez désactivé hello automatique de rapport d’incident fonctionnalité d’Engagement).</span><span class="sxs-lookup"><span data-stu-id="1d048-190">You can use it tooimplement your own UnhandledException handler (especially if you have disabled hello automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="1d048-191">Par exemple, dans hello `Application_UnhandledException` méthode Hello `App.xaml.cs` fichier :</span><span class="sxs-lookup"><span data-stu-id="1d048-191">For example, in hello `Application_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="1d048-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="1d048-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="1d048-193">Référence</span><span class="sxs-lookup"><span data-stu-id="1d048-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="1d048-194">Lorsqu’il hello utilisateur navigue vers l’avant, en dehors d’une application, une fois hello désactivé est déclenché, le système d’exploitation de hello tentera application hello de tooput à l’état dormant.</span><span class="sxs-lookup"><span data-stu-id="1d048-194">When hello user navigates forward, away from an application, after hello Deactivated event is raised, hello operating system will attempt tooput hello application into a dormant state.</span></span> <span data-ttu-id="1d048-195">Ensuite, application hello est tombstone.</span><span class="sxs-lookup"><span data-stu-id="1d048-195">Then, hello application is Tombstoning.</span></span> <span data-ttu-id="1d048-196">Dans ce processus, une application est arrêtée, mais certaines données sur l’état de hello de l’application hello et des pages individuelles hello au sein de l’application hello sont conservées.</span><span class="sxs-lookup"><span data-stu-id="1d048-196">In this process an application is terminated but some data about hello state of hello application and hello individual pages within hello application is preserved.</span></span>

<span data-ttu-id="1d048-197">Vous avez tooinsert `EngagementAgent.Instance.OnActivated(e)` Bonjour `Application_Activated` méthode Bonjour App.xaml.cs fichier tooreset Bonjour Engagement Agent lors de l’application hello a été désactivé.</span><span class="sxs-lookup"><span data-stu-id="1d048-197">You have tooinsert `EngagementAgent.Instance.OnActivated(e)` in hello `Application_Activated` method from hello App.xaml.cs file tooreset hello Engagement Agent when hello application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="1d048-198">Exemple</span><span class="sxs-lookup"><span data-stu-id="1d048-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code tooexecute when hello application is activated (brought tooforeground)
            // This code will not execute when hello application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="1d048-199">ID de périphérique</span><span class="sxs-lookup"><span data-stu-id="1d048-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="1d048-200">Vous pouvez obtenir l’id d’appareil hello engagement en appelant cette méthode.</span><span class="sxs-lookup"><span data-stu-id="1d048-200">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="1d048-201">Paramètres de suppléments</span><span class="sxs-lookup"><span data-stu-id="1d048-201">Extras parameters</span></span>
<span data-ttu-id="1d048-202">Données arbitraires peuvent être attachés tooan événement, une erreur, une activité ou une tâche.</span><span class="sxs-lookup"><span data-stu-id="1d048-202">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="1d048-203">Ces données peuvent être structurées à l'aide d'un dictionnaire.</span><span class="sxs-lookup"><span data-stu-id="1d048-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="1d048-204">Les clés et les valeurs peuvent être de n'importe quel type.</span><span class="sxs-lookup"><span data-stu-id="1d048-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="1d048-205">Les données de fonctionnalités supplémentaires sont sérialisées afin que si vous souhaitez tooinsert votre propre type de fonctionnalités supplémentaires vous ayez tooadd un contrat de données pour ce type.</span><span class="sxs-lookup"><span data-stu-id="1d048-205">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="1d048-206">Exemple</span><span class="sxs-lookup"><span data-stu-id="1d048-206">Example</span></span>
<span data-ttu-id="1d048-207">Nous créons une classe nommée « Person ».</span><span class="sxs-lookup"><span data-stu-id="1d048-207">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Engagement.Agent
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

<span data-ttu-id="1d048-208">Ensuite, nous allons ajouter un `Person` tooan instance supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="1d048-208">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="1d048-209">Si vous placez des autres types d’objets, assurez-vous que sa méthode ToString() est implémenté tooreturn une chaîne contrôlable de visu.</span><span class="sxs-lookup"><span data-stu-id="1d048-209">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="1d048-210">limites</span><span class="sxs-lookup"><span data-stu-id="1d048-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="1d048-211">Clés</span><span class="sxs-lookup"><span data-stu-id="1d048-211">Keys</span></span>
<span data-ttu-id="1d048-212">Chaque clé de l’objet de hello doit correspondre hello expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="1d048-212">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="1d048-213">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="1d048-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="1d048-214">Taille</span><span class="sxs-lookup"><span data-stu-id="1d048-214">Size</span></span>
<span data-ttu-id="1d048-215">Fonctionnalités supplémentaires sont trop limitées**1024** caractères par l’appel.</span><span class="sxs-lookup"><span data-stu-id="1d048-215">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="1d048-216">Rapports d'informations sur l'application</span><span class="sxs-lookup"><span data-stu-id="1d048-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="1d048-217">Référence</span><span class="sxs-lookup"><span data-stu-id="1d048-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="1d048-218">Vous pouvez manuellement signaler le suivi des informations (ou toutes les autres informations spécifiques aux applications à l’aide de la fonction de SendAppInfo() hello).</span><span class="sxs-lookup"><span data-stu-id="1d048-218">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="1d048-219">Notez que ces informations peuvent être envoyées de façon incrémentielle : uniquement hello valeur la plus récente d’une clé spécifique est conservé pour un périphérique donné.</span><span class="sxs-lookup"><span data-stu-id="1d048-219">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="1d048-220">Comme l’événement extras, utiliser un dictionnaire\<objet, objet\> tooattach informations.</span><span class="sxs-lookup"><span data-stu-id="1d048-220">Like event extras, use a Dictionary\<object, object\> tooattach informations.</span></span>

### <a name="example"></a><span data-ttu-id="1d048-221">Exemple</span><span class="sxs-lookup"><span data-stu-id="1d048-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="1d048-222">Limites</span><span class="sxs-lookup"><span data-stu-id="1d048-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="1d048-223">Clés</span><span class="sxs-lookup"><span data-stu-id="1d048-223">Keys</span></span>
<span data-ttu-id="1d048-224">Chaque clé de l’objet de hello doit correspondre hello expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="1d048-224">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="1d048-225">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="1d048-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="1d048-226">Taille</span><span class="sxs-lookup"><span data-stu-id="1d048-226">Size</span></span>
<span data-ttu-id="1d048-227">Informations sur l’application sont trop limitées**1024** caractères par l’appel.</span><span class="sxs-lookup"><span data-stu-id="1d048-227">Application information are limited too**1024** characters per call.</span></span>

<span data-ttu-id="1d048-228">Bonjour exemple précédent, hello JSON envoyé toohello serveur est 44 caractères :</span><span class="sxs-lookup"><span data-stu-id="1d048-228">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="1d048-229">Journalisation</span><span class="sxs-lookup"><span data-stu-id="1d048-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="1d048-230">Activation de la journalisation</span><span class="sxs-lookup"><span data-stu-id="1d048-230">Enable Logging</span></span>
<span data-ttu-id="1d048-231">Hello SDK peut être configuré tooproduce des journaux de test dans la console hello IDE.</span><span class="sxs-lookup"><span data-stu-id="1d048-231">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="1d048-232">Ces journaux ne sont pas activés par défaut.</span><span class="sxs-lookup"><span data-stu-id="1d048-232">These logs are not activated by default.</span></span> <span data-ttu-id="1d048-233">toocustomize, propriété hello de mise à jour `EngagementAgent.Instance.TestLogEnabled` tooone de valeur hello disponible à partir de hello `EngagementTestLogLevel` énumération, par exemple :</span><span class="sxs-lookup"><span data-stu-id="1d048-233">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
