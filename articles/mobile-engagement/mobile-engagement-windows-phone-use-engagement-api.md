---
title: "Comment utiliser l'API Engagement sur Windows Phone Silverlight"
description: "Comment utiliser l'API Engagement sur Windows Phone Silverlight"
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
ms.openlocfilehash: ec8b6c13ea052c8063dfde4321cdd286ab6cb817
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-windows-phone-silverlight"></a><span data-ttu-id="51d90-103">Comment utiliser l'API Engagement sur Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="51d90-103">How to Use the Engagement API on Windows Phone Silverlight</span></span>
<span data-ttu-id="51d90-104">Ce document vient compléter celui intitulé [Comment intégrer Mobile Engagement à votre application Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="51d90-104">This document is an add-on to the document [How to integrate Mobile Engagement in your Windows Phone Silverlight app](mobile-engagement-windows-phone-integrate-engagement.md).</span></span> <span data-ttu-id="51d90-105">Il fournit des informations détaillées sur l'utilisation de l'API Engagement pour signaler les statistiques de votre application.</span><span class="sxs-lookup"><span data-stu-id="51d90-105">It provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="51d90-106">Si vous souhaitez qu'Engagement signale uniquement les sessions, activités, incidents et informations techniques de votre application, la méthode la plus simple consiste à configurer toutes vos sous-classes `PhoneApplicationPage` de manière à ce qu'elles héritent de la classe `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="51d90-106">If you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` class.</span></span>

<span data-ttu-id="51d90-107">Si vous souhaitez aller plus loin, par exemple si vous avez besoin de signaler des événements, des erreurs et des travaux spécifiques à l'application, ou si vous devez signaler les activités de votre application d'une manière différente de celle implémentée dans les classes `EngagementPage`, vous devez utiliser l'API Engagement.</span><span class="sxs-lookup"><span data-stu-id="51d90-107">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="51d90-108">L'API Engagement est fournie par la classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="51d90-108">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="51d90-109">Vous pouvez accéder à ces méthodes par l'intermédiaire de `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="51d90-109">You can access to those methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="51d90-110">Même si le module de l'agent n'a pas été initialisé, chaque appel à l'API est différé et réexécuté une fois l'agent disponible.</span><span class="sxs-lookup"><span data-stu-id="51d90-110">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="51d90-111">Concepts liés à Engagement</span><span class="sxs-lookup"><span data-stu-id="51d90-111">Engagement concepts</span></span>
<span data-ttu-id="51d90-112">Les parties suivantes décrivent plus en détail les concepts de Mobile Engagement pour la plateforme Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="51d90-112">The following parts refine the Mobile Engagement Concepts for the Windows Phone platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="51d90-113">`Session` et `Activity`</span><span class="sxs-lookup"><span data-stu-id="51d90-113">`Session` and `Activity`</span></span>
<span data-ttu-id="51d90-114">Une *activité* est généralement associée à une page de l’application, c’est-à-dire que *l’activité* démarre quand la page est affichée et s’arrête quand la page est fermée : c’est le cas quand le SDK Engagement est intégré à l’aide de la classe `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="51d90-114">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span></span>

<span data-ttu-id="51d90-115">Mais les *activités* peuvent également être contrôlées manuellement à l'aide de l'API Engagement.</span><span class="sxs-lookup"><span data-stu-id="51d90-115">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="51d90-116">Cela permet de diviser une page donnée en plusieurs sous-parties, afin d'obtenir davantage de détails sur l'utilisation de cette page (par exemple pour connaître la fréquence et la durée pendant laquelle les boîtes de dialogue sont utilisées à l'intérieur de cette page).</span><span class="sxs-lookup"><span data-stu-id="51d90-116">This allows to split a given page in several sub parts to get more details about the usage of this page (for example to known how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="51d90-117">Rapports d'activités</span><span class="sxs-lookup"><span data-stu-id="51d90-117">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="51d90-118">L'utilisateur démarre une nouvelle activité</span><span class="sxs-lookup"><span data-stu-id="51d90-118">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="51d90-119">Référence</span><span class="sxs-lookup"><span data-stu-id="51d90-119">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="51d90-120">Vous devez appeler `StartActivity()` chaque fois que l'activité utilisateur change.</span><span class="sxs-lookup"><span data-stu-id="51d90-120">You need to call `StartActivity()` each time the user activity changes.</span></span> <span data-ttu-id="51d90-121">Le premier appel à cette fonction démarre une nouvelle session utilisateur.</span><span class="sxs-lookup"><span data-stu-id="51d90-121">The first call to this function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="51d90-122">Le Kit de développement logiciel appelle automatiquement la méthode EndActivity lorsque l'application est fermée.</span><span class="sxs-lookup"><span data-stu-id="51d90-122">The SDK automatically call the EndActivity method when the application is closed.</span></span> <span data-ttu-id="51d90-123">Par conséquent, il est FORTEMENT recommandé d'appeler la méthode StartActivity chaque fois que l'activité de l'utilisateur change et de ne JAMAIS appeler la méthode EndActivity, celle-ci forçant la fin de la session active.</span><span class="sxs-lookup"><span data-stu-id="51d90-123">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user change, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="51d90-124">Exemple</span><span class="sxs-lookup"><span data-stu-id="51d90-124">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="51d90-125">L'utilisateur met fin à l'activité en cours</span><span class="sxs-lookup"><span data-stu-id="51d90-125">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="51d90-126">Référence</span><span class="sxs-lookup"><span data-stu-id="51d90-126">Reference</span></span>
            void EndActivity()

<span data-ttu-id="51d90-127">Vous devez appeler `EndActivity()` au moins une fois quand l'utilisateur termine sa dernière activité.</span><span class="sxs-lookup"><span data-stu-id="51d90-127">You need to call `EndActivity()` at least once when the user finishes his last activity.</span></span> <span data-ttu-id="51d90-128">Cela indique au Kit de développement logiciel Engagement que l'utilisateur est inactif et que la session utilisateur doit être fermée à la fin du délai d'expiration de session (si vous appelez `StartActivity()` avant l'expiration de la session, la session est simplement reprise).</span><span class="sxs-lookup"><span data-stu-id="51d90-128">This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `StartActivity()` before the session timeout expires, the session is simply continued).</span></span>

#### <a name="example"></a><span data-ttu-id="51d90-129">Exemple</span><span class="sxs-lookup"><span data-stu-id="51d90-129">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="51d90-130">Rapports de travaux</span><span class="sxs-lookup"><span data-stu-id="51d90-130">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="51d90-131">Démarrer un travail</span><span class="sxs-lookup"><span data-stu-id="51d90-131">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="51d90-132">Référence</span><span class="sxs-lookup"><span data-stu-id="51d90-132">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="51d90-133">Vous pouvez utiliser le travail pour effectuer le suivi de certaines tâches sur une période donnée.</span><span class="sxs-lookup"><span data-stu-id="51d90-133">You can use the job to track certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="51d90-134">Exemple</span><span class="sxs-lookup"><span data-stu-id="51d90-134">Example</span></span>
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="51d90-135">Mettre fin à un travail</span><span class="sxs-lookup"><span data-stu-id="51d90-135">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="51d90-136">Référence</span><span class="sxs-lookup"><span data-stu-id="51d90-136">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="51d90-137">Dès qu'une tâche suivie par un travail est terminée, vous devez appeler la méthode EndJob pour ce travail, en fournissant le nom du travail.</span><span class="sxs-lookup"><span data-stu-id="51d90-137">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span></span>

#### <a name="example"></a><span data-ttu-id="51d90-138">Exemple</span><span class="sxs-lookup"><span data-stu-id="51d90-138">Example</span></span>
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="51d90-139">Rapports d'événements</span><span class="sxs-lookup"><span data-stu-id="51d90-139">Reporting Events</span></span>
<span data-ttu-id="51d90-140">Il existe trois types d'événements :</span><span class="sxs-lookup"><span data-stu-id="51d90-140">There is three types of events :</span></span>

* <span data-ttu-id="51d90-141">Événements autonomes</span><span class="sxs-lookup"><span data-stu-id="51d90-141">Standalone events</span></span>
* <span data-ttu-id="51d90-142">Événements de session</span><span class="sxs-lookup"><span data-stu-id="51d90-142">Session events</span></span>
* <span data-ttu-id="51d90-143">Événements de travail</span><span class="sxs-lookup"><span data-stu-id="51d90-143">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="51d90-144">Événements autonomes</span><span class="sxs-lookup"><span data-stu-id="51d90-144">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="51d90-145">Référence</span><span class="sxs-lookup"><span data-stu-id="51d90-145">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="51d90-146">Les événements autonomes peuvent se produire en dehors du contexte d'une session.</span><span class="sxs-lookup"><span data-stu-id="51d90-146">Standalone events can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="51d90-147">Exemple</span><span class="sxs-lookup"><span data-stu-id="51d90-147">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="51d90-148">Événements de session</span><span class="sxs-lookup"><span data-stu-id="51d90-148">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="51d90-149">Référence</span><span class="sxs-lookup"><span data-stu-id="51d90-149">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="51d90-150">Les événements de session servent généralement à signaler les actions effectuées par un utilisateur lors de sa session.</span><span class="sxs-lookup"><span data-stu-id="51d90-150">Session events are usually used to report the actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="51d90-151">Exemple</span><span class="sxs-lookup"><span data-stu-id="51d90-151">Example</span></span>
<span data-ttu-id="51d90-152">**Sans données :**</span><span class="sxs-lookup"><span data-stu-id="51d90-152">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="51d90-153">**Avec données :**</span><span class="sxs-lookup"><span data-stu-id="51d90-153">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="51d90-154">Événements de travail</span><span class="sxs-lookup"><span data-stu-id="51d90-154">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="51d90-155">Référence</span><span class="sxs-lookup"><span data-stu-id="51d90-155">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="51d90-156">Les événements de travail servent généralement à signaler les actions effectuées par un utilisateur lors d'un travail.</span><span class="sxs-lookup"><span data-stu-id="51d90-156">Job events are usually used to report the actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="51d90-157">Exemple</span><span class="sxs-lookup"><span data-stu-id="51d90-157">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="51d90-158">Rapports d'erreurs</span><span class="sxs-lookup"><span data-stu-id="51d90-158">Reporting Errors</span></span>
<span data-ttu-id="51d90-159">Il existe trois types d'erreurs :</span><span class="sxs-lookup"><span data-stu-id="51d90-159">There is three types of errors :</span></span>

* <span data-ttu-id="51d90-160">Erreurs autonomes</span><span class="sxs-lookup"><span data-stu-id="51d90-160">Standalone errors</span></span>
* <span data-ttu-id="51d90-161">Erreurs de session</span><span class="sxs-lookup"><span data-stu-id="51d90-161">Session errors</span></span>
* <span data-ttu-id="51d90-162">Erreurs de travail</span><span class="sxs-lookup"><span data-stu-id="51d90-162">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="51d90-163">Erreurs autonomes</span><span class="sxs-lookup"><span data-stu-id="51d90-163">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="51d90-164">Référence</span><span class="sxs-lookup"><span data-stu-id="51d90-164">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="51d90-165">Contrairement aux erreurs de session, les erreurs autonomes peuvent se produire en dehors du contexte d'une session.</span><span class="sxs-lookup"><span data-stu-id="51d90-165">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="51d90-166">Exemple</span><span class="sxs-lookup"><span data-stu-id="51d90-166">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="51d90-167">Erreurs de session</span><span class="sxs-lookup"><span data-stu-id="51d90-167">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="51d90-168">Référence</span><span class="sxs-lookup"><span data-stu-id="51d90-168">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="51d90-169">Les erreurs de session servent généralement à signaler les erreurs affectant l'utilisateur lors de sa session.</span><span class="sxs-lookup"><span data-stu-id="51d90-169">Session errors are usually used to report the errors impacting the user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="51d90-170">Exemple</span><span class="sxs-lookup"><span data-stu-id="51d90-170">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="51d90-171">Erreurs de travail</span><span class="sxs-lookup"><span data-stu-id="51d90-171">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="51d90-172">Référence</span><span class="sxs-lookup"><span data-stu-id="51d90-172">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="51d90-173">Les erreurs peuvent être associées à un travail en cours d'exécution plutôt qu'à la session utilisateur en cours.</span><span class="sxs-lookup"><span data-stu-id="51d90-173">Errors can be related to a running job instead of being related to the current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="51d90-174">Exemple</span><span class="sxs-lookup"><span data-stu-id="51d90-174">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="51d90-175">Rapports d'incidents</span><span class="sxs-lookup"><span data-stu-id="51d90-175">Reporting Crashes</span></span>
<span data-ttu-id="51d90-176">L'agent fournit deux méthodes pour gérer les incidents.</span><span class="sxs-lookup"><span data-stu-id="51d90-176">The agent provides two methods to deal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="51d90-177">Envoyer une exception</span><span class="sxs-lookup"><span data-stu-id="51d90-177">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="51d90-178">Référence</span><span class="sxs-lookup"><span data-stu-id="51d90-178">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="51d90-179">Exemple</span><span class="sxs-lookup"><span data-stu-id="51d90-179">Example</span></span>
<span data-ttu-id="51d90-180">Vous pouvez envoyer une exception à tout moment en appelant :</span><span class="sxs-lookup"><span data-stu-id="51d90-180">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="51d90-181">Vous pouvez également utiliser un paramètre facultatif pour mettre fin à la session Engagement en même temps que l'envoi de l'incident.</span><span class="sxs-lookup"><span data-stu-id="51d90-181">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span></span> <span data-ttu-id="51d90-182">Pour ce faire, appelez :</span><span class="sxs-lookup"><span data-stu-id="51d90-182">To do so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="51d90-183">Si vous procédez ainsi, la session et les travaux sont fermés juste après l'envoi de l'incident.</span><span class="sxs-lookup"><span data-stu-id="51d90-183">If you do that, the session and jobs will be closed just after sending the crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="51d90-184">Envoyer une exception non gérée</span><span class="sxs-lookup"><span data-stu-id="51d90-184">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="51d90-185">Référence</span><span class="sxs-lookup"><span data-stu-id="51d90-185">Reference</span></span>
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

<span data-ttu-id="51d90-186">Engagement offre aussi une méthode pour envoyer les exceptions non gérées.</span><span class="sxs-lookup"><span data-stu-id="51d90-186">Engagement also provides a method to send unhandled exceptions.</span></span> <span data-ttu-id="51d90-187">Elle s'avère particulièrement efficace quand vous l'utilisez dans le Gestionnaire d'événements UnhandledException Silverlight.</span><span class="sxs-lookup"><span data-stu-id="51d90-187">This is especially useful when used inside the silverlight UnhandledException event handler.</span></span>

<span data-ttu-id="51d90-188">Cette méthode met **TOUJOURS** fin aux travaux et à la session Engagement après avoir été appelée.</span><span class="sxs-lookup"><span data-stu-id="51d90-188">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="51d90-189">Exemple</span><span class="sxs-lookup"><span data-stu-id="51d90-189">Example</span></span>
<span data-ttu-id="51d90-190">Vous pouvez l'utiliser pour implémenter votre propre gestionnaire UnhandledException (notamment si vous avez désactivé la fonctionnalité de signalement automatique des incidents d'Engagement).</span><span class="sxs-lookup"><span data-stu-id="51d90-190">You can use it to implement your own UnhandledException handler (especially if you have disabled the automatic crash reporting feature of Engagement).</span></span> <span data-ttu-id="51d90-191">Par exemple, dans la méthode `Application_UnhandledException` du fichier `App.xaml.cs` :</span><span class="sxs-lookup"><span data-stu-id="51d90-191">For example, in the `Application_UnhandledException` method of the `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a><span data-ttu-id="51d90-192">OnActivated</span><span class="sxs-lookup"><span data-stu-id="51d90-192">OnActivated</span></span>
### <a name="reference"></a><span data-ttu-id="51d90-193">Référence</span><span class="sxs-lookup"><span data-stu-id="51d90-193">Reference</span></span>
            void OnActivated(ActivatedEventArgs e)

<span data-ttu-id="51d90-194">Quand l'utilisateur navigue vers l'avant, en dehors d'une application, le système d'exploitation tente de placer l'application dans un état dormant après le déclenchement de l'événement Deactivated.</span><span class="sxs-lookup"><span data-stu-id="51d90-194">When the user navigates forward, away from an application, after the Deactivated event is raised, the operating system will attempt to put the application into a dormant state.</span></span> <span data-ttu-id="51d90-195">Ensuite, l'application est désactivée (« Tombstoning »).</span><span class="sxs-lookup"><span data-stu-id="51d90-195">Then, the application is Tombstoning.</span></span> <span data-ttu-id="51d90-196">Au cours de ce processus, l'application est arrêtée, mais certaines données sur l'état de l'application et les pages individuelles au sein de l'application sont conservées.</span><span class="sxs-lookup"><span data-stu-id="51d90-196">In this process an application is terminated but some data about the state of the application and the individual pages within the application is preserved.</span></span>

<span data-ttu-id="51d90-197">Vous devez insérer `EngagementAgent.Instance.OnActivated(e)` dans la méthode `Application_Activated` à partir du fichier App.xaml.cs pour réinitialiser l'agent Engagement une fois l'application désactivée.</span><span class="sxs-lookup"><span data-stu-id="51d90-197">You have to insert `EngagementAgent.Instance.OnActivated(e)` in the `Application_Activated` method from the App.xaml.cs file to reset the Engagement Agent when the application has been Tombstoned.</span></span>

### <a name="example"></a><span data-ttu-id="51d90-198">Exemple</span><span class="sxs-lookup"><span data-stu-id="51d90-198">Example</span></span>
            // Inside your App.xaml.cs file

            // Code to execute when the application is activated (brought to foreground)
            // This code will not execute when the application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a><span data-ttu-id="51d90-199">ID de périphérique</span><span class="sxs-lookup"><span data-stu-id="51d90-199">Device Id</span></span>
            String GetDeviceId()

<span data-ttu-id="51d90-200">Vous pouvez obtenir l'ID de périphérique Engagement en appelant cette méthode.</span><span class="sxs-lookup"><span data-stu-id="51d90-200">You can get the engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="51d90-201">Paramètres de suppléments</span><span class="sxs-lookup"><span data-stu-id="51d90-201">Extras parameters</span></span>
<span data-ttu-id="51d90-202">Des données arbitraires peuvent être associées à un événement, à une erreur, à une activité ou à un travail.</span><span class="sxs-lookup"><span data-stu-id="51d90-202">Arbitrary data can be attached to an event, an error, an activity or a job.</span></span> <span data-ttu-id="51d90-203">Ces données peuvent être structurées à l'aide d'un dictionnaire.</span><span class="sxs-lookup"><span data-stu-id="51d90-203">These data can be structured using a dictionary.</span></span> <span data-ttu-id="51d90-204">Les clés et les valeurs peuvent être de n'importe quel type.</span><span class="sxs-lookup"><span data-stu-id="51d90-204">Keys and values can be of any type.</span></span>

<span data-ttu-id="51d90-205">Les données de suppléments sont sérialisées ; par conséquent, si vous souhaitez insérer votre propre type dans des suppléments, vous devez ajouter un contrat de données pour ce type.</span><span class="sxs-lookup"><span data-stu-id="51d90-205">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="51d90-206">Exemple</span><span class="sxs-lookup"><span data-stu-id="51d90-206">Example</span></span>
<span data-ttu-id="51d90-207">Nous créons une classe nommée « Person ».</span><span class="sxs-lookup"><span data-stu-id="51d90-207">We create a new class "Person".</span></span>

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

<span data-ttu-id="51d90-208">Ensuite, nous ajoutons une instance `Person` à un supplément.</span><span class="sxs-lookup"><span data-stu-id="51d90-208">Then, we will add a `Person` instance to an extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="51d90-209">Si vous placez d'autres types d'objets, assurez-vous que leur méthode ToString() est implémentée pour retourner une chaîne explicite.</span><span class="sxs-lookup"><span data-stu-id="51d90-209">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="51d90-210">Limites</span><span class="sxs-lookup"><span data-stu-id="51d90-210">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="51d90-211">de clés symétriques</span><span class="sxs-lookup"><span data-stu-id="51d90-211">Keys</span></span>
<span data-ttu-id="51d90-212">Chaque clé de l'objet doit correspondre à l'expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="51d90-212">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="51d90-213">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="51d90-213">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="51d90-214">Taille</span><span class="sxs-lookup"><span data-stu-id="51d90-214">Size</span></span>
<span data-ttu-id="51d90-215">Les suppléments sont limités à **1 024** caractères par appel.</span><span class="sxs-lookup"><span data-stu-id="51d90-215">Extras are limited to **1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="51d90-216">Rapports d'informations sur l'application</span><span class="sxs-lookup"><span data-stu-id="51d90-216">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="51d90-217">Référence</span><span class="sxs-lookup"><span data-stu-id="51d90-217">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="51d90-218">Vous pouvez signaler manuellement les informations de suivi (ou toute autre information spécifique à l'application) à l'aide de la fonction SendAppInfo().</span><span class="sxs-lookup"><span data-stu-id="51d90-218">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span></span>

<span data-ttu-id="51d90-219">Notez que ces informations peuvent être envoyées de façon incrémentielle : seule la dernière valeur d'une clé donnée sera conservée pour un périphérique donné.</span><span class="sxs-lookup"><span data-stu-id="51d90-219">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="51d90-220">Comme pour les suppléments d’événements, utilisez un Dictionary\<object, object\> pour joindre des informations.</span><span class="sxs-lookup"><span data-stu-id="51d90-220">Like event extras, use a Dictionary\<object, object\> to attach informations.</span></span>

### <a name="example"></a><span data-ttu-id="51d90-221">Exemple</span><span class="sxs-lookup"><span data-stu-id="51d90-221">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="51d90-222">Limites</span><span class="sxs-lookup"><span data-stu-id="51d90-222">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="51d90-223">de clés symétriques</span><span class="sxs-lookup"><span data-stu-id="51d90-223">Keys</span></span>
<span data-ttu-id="51d90-224">Chaque clé de l'objet doit correspondre à l'expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="51d90-224">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="51d90-225">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="51d90-225">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="51d90-226">Taille</span><span class="sxs-lookup"><span data-stu-id="51d90-226">Size</span></span>
<span data-ttu-id="51d90-227">Les informations de l'application sont limitées à **1 024** caractères par appel.</span><span class="sxs-lookup"><span data-stu-id="51d90-227">Application information are limited to **1024** characters per call.</span></span>

<span data-ttu-id="51d90-228">Dans l'exemple précédent, le JSON envoyé au serveur fait 44 caractères :</span><span class="sxs-lookup"><span data-stu-id="51d90-228">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a><span data-ttu-id="51d90-229">Journalisation</span><span class="sxs-lookup"><span data-stu-id="51d90-229">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="51d90-230">Activation de la journalisation</span><span class="sxs-lookup"><span data-stu-id="51d90-230">Enable Logging</span></span>
<span data-ttu-id="51d90-231">Le Kit de développement logiciel (SDK) peut être configuré pour générer des journaux de tests dans la console IDE.</span><span class="sxs-lookup"><span data-stu-id="51d90-231">The SDK can be configured to produce test logs in the IDE console.</span></span>
<span data-ttu-id="51d90-232">Ces journaux ne sont pas activés par défaut.</span><span class="sxs-lookup"><span data-stu-id="51d90-232">These logs are not activated by default.</span></span> <span data-ttu-id="51d90-233">Pour personnaliser ce résultat, mettez à jour la propriété `EngagementAgent.Instance.TestLogEnabled` avec une des valeurs disponibles à partir de l'énumération `EngagementTestLogLevel`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="51d90-233">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
