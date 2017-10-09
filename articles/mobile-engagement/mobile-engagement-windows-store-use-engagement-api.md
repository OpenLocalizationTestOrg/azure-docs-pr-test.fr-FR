---
title: aaaHow tooUse hello API Engagement sur Windows universel
description: Comment tooUse hello API Engagement sur Windows universel
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: bb501fca-9cfe-4495-81df-b5efd6e0137b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0256b839c28e4ef6c530106408d744038fa711ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-universal"></a><span data-ttu-id="222cf-103">Comment tooUse hello API Engagement sur Windows universel</span><span class="sxs-lookup"><span data-stu-id="222cf-103">How tooUse hello Engagement API on Windows Universal</span></span>
<span data-ttu-id="222cf-104">Ce document est un document toohello de module complémentaire [comment tooIntegrate Engagement sur Windows universel](mobile-engagement-windows-store-integrate-engagement.md): il fournit obtenir plus de détails sur comment toouse hello Engagement API tooreport vos statistiques de l’application.</span><span class="sxs-lookup"><span data-stu-id="222cf-104">This document is an add-on toohello document [How tooIntegrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="222cf-105">N’oubliez pas que si vous souhaitez uniquement Engagement tooreport sessions, activités, blocages et des informations techniques de votre application, puis hello plus simple consiste toomake tous vos `Page` sous-classes héritent hello `EngagementPage` classe.</span><span class="sxs-lookup"><span data-stu-id="222cf-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Page` sub-classes inherit from hello `EngagementPage` class.</span></span>

<span data-ttu-id="222cf-106">Si vous voulez toodo plus, par exemple, si vous avez besoin tooreport les événements d’application spécifique, les erreurs et les tâches, ou si vous avez tooreport activités de votre application d’une manière différente d’une implémentation dans hello hello `EngagementPage` des classes, vous devez toouse hello API d’engagement.</span><span class="sxs-lookup"><span data-stu-id="222cf-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementPage` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="222cf-107">API d’Engagement Hello est fournie par hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="222cf-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="222cf-108">Vous pouvez accéder à des méthodes toothose via `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="222cf-108">You can access toothose methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="222cf-109">Même si le module de l’agent hello n’a pas été initialisée, chaque API de toohello d’appel est différée et sera exécutée à nouveau lorsque l’agent de hello n’est disponible.</span><span class="sxs-lookup"><span data-stu-id="222cf-109">Even if hello agent module has not been initialized, each call toohello API is deferred, and will be executed again when hello agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="222cf-110">Concepts liés à Engagement</span><span class="sxs-lookup"><span data-stu-id="222cf-110">Engagement concepts</span></span>
<span data-ttu-id="222cf-111">parties suivantes Hello affiner hello commun [Concepts d’Engagement Mobile](mobile-engagement-concepts.md) pour la plateforme Windows universelle de hello.</span><span class="sxs-lookup"><span data-stu-id="222cf-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="222cf-112">`Session` et `Activity`</span><span class="sxs-lookup"><span data-stu-id="222cf-112">`Session` and `Activity`</span></span>
<span data-ttu-id="222cf-113">Un *activité* est généralement associé à une page de l’application hello, qui est toosay hello *activité* démarre lorsque la page de hello et s’arrête lorsque la page de hello est fermé : il s’agit des cas hello si hello Engagement SDK est intégré à l’aide de hello `EngagementPage` classe.</span><span class="sxs-lookup"><span data-stu-id="222cf-113">An *activity* is usually associated with one page of hello application, that is toosay hello *activity* starts when hello page is displayed and stops when hello page is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementPage` class.</span></span>

<span data-ttu-id="222cf-114">Mais *activités* peut également être contrôlée manuellement à l’aide des API de l’Engagement de hello.</span><span class="sxs-lookup"><span data-stu-id="222cf-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="222cf-115">Cela vous permet de toosplit une page donnée dans plusieurs sub parties tooget plus de détails sur l’utilisation de hello de cette page (par exemple tooknow la fréquence et la durée pendant laquelle les boîtes de dialogue sont utilisés à l’intérieur de cette page).</span><span class="sxs-lookup"><span data-stu-id="222cf-115">This allows you toosplit a given page in several sub parts tooget more details about hello usage of this page (for example tooknow how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="222cf-116">Rapports d'activités</span><span class="sxs-lookup"><span data-stu-id="222cf-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="222cf-117">L'utilisateur démarre une nouvelle activité</span><span class="sxs-lookup"><span data-stu-id="222cf-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="222cf-118">Référence</span><span class="sxs-lookup"><span data-stu-id="222cf-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="222cf-119">Vous devez toocall `StartActivity()` chaque activité utilisateur hello change.</span><span class="sxs-lookup"><span data-stu-id="222cf-119">You need toocall `StartActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="222cf-120">Hello premier appel toothis fonction démarre une nouvelle session de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="222cf-120">hello first call toothis function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="222cf-121">Hello SDK appelle automatiquement la méthode EndActivity de hello lors de l’application hello est fermée.</span><span class="sxs-lookup"><span data-stu-id="222cf-121">hello SDK automatically calls hello EndActivity method when hello application is closed.</span></span> <span data-ttu-id="222cf-122">Par conséquent, il est vivement recommandé toocall hello StartActivity (méthode) chaque fois que l’activité hello d’utilisateur de hello change, et la fin de l’appel tooNEVER hello méthode EndActivity, depuis l’appel de cette méthode force toobe de session en cours hello.</span><span class="sxs-lookup"><span data-stu-id="222cf-122">Thus, it is HIGHLY recommended toocall hello StartActivity method whenever hello activity of hello user changes, and tooNEVER call hello EndActivity method, since calling this method forces hello current session toobe ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="222cf-123">Exemple</span><span class="sxs-lookup"><span data-stu-id="222cf-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="222cf-124">L'utilisateur met fin à l'activité en cours</span><span class="sxs-lookup"><span data-stu-id="222cf-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="222cf-125">Référence</span><span class="sxs-lookup"><span data-stu-id="222cf-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="222cf-126">Activité hello et la session de hello se termine.</span><span class="sxs-lookup"><span data-stu-id="222cf-126">This ends hello activity and hello session.</span></span> <span data-ttu-id="222cf-127">Vous ne devez pas appeler cette méthode, à moins de savoir exactement ce que vous faites.</span><span class="sxs-lookup"><span data-stu-id="222cf-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="222cf-128">Exemple</span><span class="sxs-lookup"><span data-stu-id="222cf-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="222cf-129">Rapports de travaux</span><span class="sxs-lookup"><span data-stu-id="222cf-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="222cf-130">Démarrer un travail</span><span class="sxs-lookup"><span data-stu-id="222cf-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="222cf-131">Référence</span><span class="sxs-lookup"><span data-stu-id="222cf-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="222cf-132">Vous pouvez utiliser des tâches certains tootrack hello sur une période de temps.</span><span class="sxs-lookup"><span data-stu-id="222cf-132">You can use hello job tootrack certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="222cf-133">Exemple</span><span class="sxs-lookup"><span data-stu-id="222cf-133">Example</span></span>
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="222cf-134">Mettre fin à un travail</span><span class="sxs-lookup"><span data-stu-id="222cf-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="222cf-135">Référence</span><span class="sxs-lookup"><span data-stu-id="222cf-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="222cf-136">Dès qu’un objet d’un suivi par une tâche a été arrêtée, vous devez appeler la méthode de EndJob hello pour cette tâche, en fournissant le nom de la tâche hello.</span><span class="sxs-lookup"><span data-stu-id="222cf-136">As soon as a task tracked by a job has been terminated, you should call hello EndJob method for this job, by supplying hello job name.</span></span>

#### <a name="example"></a><span data-ttu-id="222cf-137">Exemple</span><span class="sxs-lookup"><span data-stu-id="222cf-137">Example</span></span>
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="222cf-138">Rapports d'événements</span><span class="sxs-lookup"><span data-stu-id="222cf-138">Reporting Events</span></span>
<span data-ttu-id="222cf-139">Il existe trois types d'événements :</span><span class="sxs-lookup"><span data-stu-id="222cf-139">There is three types of events :</span></span>

* <span data-ttu-id="222cf-140">Événements autonomes</span><span class="sxs-lookup"><span data-stu-id="222cf-140">Standalone events</span></span>
* <span data-ttu-id="222cf-141">Événements de session</span><span class="sxs-lookup"><span data-stu-id="222cf-141">Session events</span></span>
* <span data-ttu-id="222cf-142">Événements de travail</span><span class="sxs-lookup"><span data-stu-id="222cf-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="222cf-143">Événements autonomes</span><span class="sxs-lookup"><span data-stu-id="222cf-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="222cf-144">Référence</span><span class="sxs-lookup"><span data-stu-id="222cf-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="222cf-145">Les événements autonome peuvent se produire en dehors du contexte hello d’une session.</span><span class="sxs-lookup"><span data-stu-id="222cf-145">Standalone events can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="222cf-146">Exemple</span><span class="sxs-lookup"><span data-stu-id="222cf-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="222cf-147">Événements de session</span><span class="sxs-lookup"><span data-stu-id="222cf-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="222cf-148">Référence</span><span class="sxs-lookup"><span data-stu-id="222cf-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="222cf-149">Événements de session sont des actions de hello tooreport utilisés généralement effectuées par un utilisateur lors de sa session.</span><span class="sxs-lookup"><span data-stu-id="222cf-149">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="222cf-150">Exemple</span><span class="sxs-lookup"><span data-stu-id="222cf-150">Example</span></span>
<span data-ttu-id="222cf-151">**Sans données :**</span><span class="sxs-lookup"><span data-stu-id="222cf-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="222cf-152">**Avec données :**</span><span class="sxs-lookup"><span data-stu-id="222cf-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="222cf-153">Événements de travail</span><span class="sxs-lookup"><span data-stu-id="222cf-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="222cf-154">Référence</span><span class="sxs-lookup"><span data-stu-id="222cf-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="222cf-155">Événements de travail sont des actions de hello tooreport utilisés généralement effectuées par un utilisateur lors d’un travail.</span><span class="sxs-lookup"><span data-stu-id="222cf-155">Job events are usually used tooreport hello actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="222cf-156">Exemple</span><span class="sxs-lookup"><span data-stu-id="222cf-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="222cf-157">Rapports d'erreurs</span><span class="sxs-lookup"><span data-stu-id="222cf-157">Reporting Errors</span></span>
<span data-ttu-id="222cf-158">Il existe trois types d’erreurs :</span><span class="sxs-lookup"><span data-stu-id="222cf-158">There are three types of errors :</span></span>

* <span data-ttu-id="222cf-159">Erreurs autonomes</span><span class="sxs-lookup"><span data-stu-id="222cf-159">Standalone errors</span></span>
* <span data-ttu-id="222cf-160">Erreurs de session</span><span class="sxs-lookup"><span data-stu-id="222cf-160">Session errors</span></span>
* <span data-ttu-id="222cf-161">Erreurs de travail</span><span class="sxs-lookup"><span data-stu-id="222cf-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="222cf-162">Erreurs autonomes</span><span class="sxs-lookup"><span data-stu-id="222cf-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="222cf-163">Référence</span><span class="sxs-lookup"><span data-stu-id="222cf-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="222cf-164">Erreurs de toosession contraires, autonome erreurs peuvent se produire en dehors du contexte hello d’une session.</span><span class="sxs-lookup"><span data-stu-id="222cf-164">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="222cf-165">Exemple</span><span class="sxs-lookup"><span data-stu-id="222cf-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="222cf-166">Erreurs de session</span><span class="sxs-lookup"><span data-stu-id="222cf-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="222cf-167">Référence</span><span class="sxs-lookup"><span data-stu-id="222cf-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="222cf-168">Session erreurs sont généralement utilisés tooreport hello affecter l’utilisateur de hello lors de sa session.</span><span class="sxs-lookup"><span data-stu-id="222cf-168">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="222cf-169">Exemple</span><span class="sxs-lookup"><span data-stu-id="222cf-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="222cf-170">Erreurs de travail</span><span class="sxs-lookup"><span data-stu-id="222cf-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="222cf-171">Référence</span><span class="sxs-lookup"><span data-stu-id="222cf-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="222cf-172">Les erreurs peuvent être associée tooa travail au lieu d’être en cours d’exécution liées de session utilisateur en cours toohello.</span><span class="sxs-lookup"><span data-stu-id="222cf-172">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="222cf-173">Exemple</span><span class="sxs-lookup"><span data-stu-id="222cf-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="222cf-174">Rapports d'incidents</span><span class="sxs-lookup"><span data-stu-id="222cf-174">Reporting Crashes</span></span>
<span data-ttu-id="222cf-175">l’agent de Hello fournit deux méthodes toodeal se bloque.</span><span class="sxs-lookup"><span data-stu-id="222cf-175">hello agent provides two methods toodeal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="222cf-176">Envoyer une exception</span><span class="sxs-lookup"><span data-stu-id="222cf-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="222cf-177">Référence</span><span class="sxs-lookup"><span data-stu-id="222cf-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="222cf-178">Exemple</span><span class="sxs-lookup"><span data-stu-id="222cf-178">Example</span></span>
<span data-ttu-id="222cf-179">Vous pouvez envoyer une exception à tout moment en appelant :</span><span class="sxs-lookup"><span data-stu-id="222cf-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="222cf-180">Vous pouvez également utiliser une session d’engagement paramètre facultatif tooterminate hello en hello même temps que l’envoi de panne de hello.</span><span class="sxs-lookup"><span data-stu-id="222cf-180">You can also use an optional parameter tooterminate hello engagement session at hello same time than sending hello crash.</span></span> <span data-ttu-id="222cf-181">Par conséquent, appelez le toodo :</span><span class="sxs-lookup"><span data-stu-id="222cf-181">toodo so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="222cf-182">Si vous procédez ainsi, les travaux et la session de hello va être fermée juste après l’envoi d’incident de hello.</span><span class="sxs-lookup"><span data-stu-id="222cf-182">If you do that, hello session and jobs will be closed just after sending hello crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="222cf-183">Envoyer une exception non gérée</span><span class="sxs-lookup"><span data-stu-id="222cf-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="222cf-184">Référence</span><span class="sxs-lookup"><span data-stu-id="222cf-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="222cf-185">Engagement fournit également une méthode toosend non gérée exceptions si vous avez **désactivé** Engagement automatique **incident** reporting.</span><span class="sxs-lookup"><span data-stu-id="222cf-185">Engagement also provides a method toosend unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="222cf-186">Ceci est particulièrement utile lorsqu’il est utilisé à l’intérieur du Gestionnaire d’événements UnhandledException hello application.</span><span class="sxs-lookup"><span data-stu-id="222cf-186">This is especially useful when used inside hello application UnhandledException event handler.</span></span>

<span data-ttu-id="222cf-187">Cette méthode sera **toujours** mettre fin à la session d’engagement hello et des travaux après avoir été appelé.</span><span class="sxs-lookup"><span data-stu-id="222cf-187">This method will **ALWAYS** terminate hello engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="222cf-188">Exemple</span><span class="sxs-lookup"><span data-stu-id="222cf-188">Example</span></span>
<span data-ttu-id="222cf-189">Vous pouvez l’utiliser tooimplement votre propre gestionnaire UnhandledExceptionEventArgs.</span><span class="sxs-lookup"><span data-stu-id="222cf-189">You can use it tooimplement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="222cf-190">Par exemple, ajouter hello `Current_UnhandledException` méthode Hello `App.xaml.cs` fichier :</span><span class="sxs-lookup"><span data-stu-id="222cf-190">For example, add hello `Current_UnhandledException` method of hello `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="222cf-191">Dans App.xaml.cs dans « Public App(){} », ajoutez :</span><span class="sxs-lookup"><span data-stu-id="222cf-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="222cf-192">ID de périphérique</span><span class="sxs-lookup"><span data-stu-id="222cf-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="222cf-193">Vous pouvez obtenir l’id d’appareil hello engagement en appelant cette méthode.</span><span class="sxs-lookup"><span data-stu-id="222cf-193">You can get hello engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="222cf-194">Paramètres de suppléments</span><span class="sxs-lookup"><span data-stu-id="222cf-194">Extras parameters</span></span>
<span data-ttu-id="222cf-195">Données arbitraires peuvent être attachés tooan événement, une erreur, une activité ou une tâche.</span><span class="sxs-lookup"><span data-stu-id="222cf-195">Arbitrary data can be attached tooan event, an error, an activity or a job.</span></span> <span data-ttu-id="222cf-196">Ces données peuvent être structurées à l'aide d'un dictionnaire.</span><span class="sxs-lookup"><span data-stu-id="222cf-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="222cf-197">Les clés et les valeurs peuvent être de n'importe quel type.</span><span class="sxs-lookup"><span data-stu-id="222cf-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="222cf-198">Les données de fonctionnalités supplémentaires sont sérialisées afin que si vous souhaitez tooinsert votre propre type de fonctionnalités supplémentaires vous ayez tooadd un contrat de données pour ce type.</span><span class="sxs-lookup"><span data-stu-id="222cf-198">Extras data are serialized so if you want tooinsert your own type in extras you have tooadd a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="222cf-199">Exemple</span><span class="sxs-lookup"><span data-stu-id="222cf-199">Example</span></span>
<span data-ttu-id="222cf-200">Nous créons une classe nommée « Person ».</span><span class="sxs-lookup"><span data-stu-id="222cf-200">We create a new class "Person".</span></span>

            using System.Runtime.Serialization;

            namespace Microsoft.Azure.Engagement
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

<span data-ttu-id="222cf-201">Ensuite, nous allons ajouter un `Person` tooan instance supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="222cf-201">Then, we will add a `Person` instance tooan extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="222cf-202">Si vous placez des autres types d’objets, assurez-vous que sa méthode ToString() est implémenté tooreturn une chaîne contrôlable de visu.</span><span class="sxs-lookup"><span data-stu-id="222cf-202">If you put other types of objects, make sure their ToString() method is implemented tooreturn a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="222cf-203">limites</span><span class="sxs-lookup"><span data-stu-id="222cf-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="222cf-204">Clés</span><span class="sxs-lookup"><span data-stu-id="222cf-204">Keys</span></span>
<span data-ttu-id="222cf-205">Chaque clé de l’objet de hello doit correspondre hello expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="222cf-205">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="222cf-206">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="222cf-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="222cf-207">Taille</span><span class="sxs-lookup"><span data-stu-id="222cf-207">Size</span></span>
<span data-ttu-id="222cf-208">Fonctionnalités supplémentaires sont trop limitées**1024** caractères par l’appel.</span><span class="sxs-lookup"><span data-stu-id="222cf-208">Extras are limited too**1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="222cf-209">Rapports d'informations sur l'application</span><span class="sxs-lookup"><span data-stu-id="222cf-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="222cf-210">Référence</span><span class="sxs-lookup"><span data-stu-id="222cf-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="222cf-211">Vous pouvez manuellement signaler le suivi des informations (ou toutes les autres informations spécifiques aux applications à l’aide de la fonction de SendAppInfo() hello).</span><span class="sxs-lookup"><span data-stu-id="222cf-211">You can manually report tracking information (or any other application specific information) using hello SendAppInfo() function.</span></span>

<span data-ttu-id="222cf-212">Notez que ces données peuvent être envoyées de façon incrémentielle : uniquement hello valeur la plus récente d’une clé spécifique est conservé pour un périphérique donné.</span><span class="sxs-lookup"><span data-stu-id="222cf-212">Note that this data can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="222cf-213">Comme l’événement extras, utiliser un dictionnaire\<objet, objet\> tooattach données.</span><span class="sxs-lookup"><span data-stu-id="222cf-213">Like event extras, use a Dictionary\<object, object\> tooattach data.</span></span>

### <a name="example"></a><span data-ttu-id="222cf-214">Exemple</span><span class="sxs-lookup"><span data-stu-id="222cf-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="222cf-215">Limites</span><span class="sxs-lookup"><span data-stu-id="222cf-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="222cf-216">Clés</span><span class="sxs-lookup"><span data-stu-id="222cf-216">Keys</span></span>
<span data-ttu-id="222cf-217">Chaque clé de l’objet de hello doit correspondre hello expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="222cf-217">Each key in hello object must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="222cf-218">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="222cf-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="222cf-219">Taille</span><span class="sxs-lookup"><span data-stu-id="222cf-219">Size</span></span>
<span data-ttu-id="222cf-220">Informations de l’application sont trop limitées**1024** caractères par l’appel.</span><span class="sxs-lookup"><span data-stu-id="222cf-220">Application information is limited too**1024** characters per call.</span></span>

<span data-ttu-id="222cf-221">Bonjour exemple précédent, hello JSON envoyé toohello serveur est 44 caractères :</span><span class="sxs-lookup"><span data-stu-id="222cf-221">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="222cf-222">Journalisation</span><span class="sxs-lookup"><span data-stu-id="222cf-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="222cf-223">Activation de la journalisation</span><span class="sxs-lookup"><span data-stu-id="222cf-223">Enable Logging</span></span>
<span data-ttu-id="222cf-224">Hello SDK peut être configuré tooproduce des journaux de test dans la console hello IDE.</span><span class="sxs-lookup"><span data-stu-id="222cf-224">hello SDK can be configured tooproduce test logs in hello IDE console.</span></span>
<span data-ttu-id="222cf-225">Ces journaux ne sont pas activés par défaut.</span><span class="sxs-lookup"><span data-stu-id="222cf-225">These logs are not activated by default.</span></span> <span data-ttu-id="222cf-226">toocustomize, propriété hello de mise à jour `EngagementAgent.Instance.TestLogEnabled` tooone de valeur hello disponible à partir de hello `EngagementTestLogLevel` énumération, par exemple :</span><span class="sxs-lookup"><span data-stu-id="222cf-226">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

