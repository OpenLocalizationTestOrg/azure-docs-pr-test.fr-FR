---
title: "Comment utiliser l'API Engagement sur Windows Universal"
description: "Comment utiliser l'API Engagement sur Windows Universal"
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
ms.openlocfilehash: 75fc134a5535e6113331470cf61df9c06eb8e2ab
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-windows-universal"></a><span data-ttu-id="66b18-103">Comment utiliser l'API Engagement sur Windows Universal</span><span class="sxs-lookup"><span data-stu-id="66b18-103">How to Use the Engagement API on Windows Universal</span></span>
<span data-ttu-id="66b18-104">Ce document est un complément du document [Comment intégrer Engagement sur Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): il explique en détail comment utiliser l'API Engagement pour créer des rapports sur les statistiques de vos applications.</span><span class="sxs-lookup"><span data-stu-id="66b18-104">This document is an add-on to the document [How to Integrate Engagement on Windows Universal](mobile-engagement-windows-store-integrate-engagement.md): it provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="66b18-105">N'oubliez pas que si vous souhaitez seulement qu'Engagement signale les sessions, les activités, les incidents et les informations techniques de votre application, la méthode la plus simple consiste à configurer toutes vos sous-classes `Page` de manière à ce qu’elles héritent de la classe `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="66b18-105">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Page` sub-classes inherit from the `EngagementPage` class.</span></span>

<span data-ttu-id="66b18-106">Si vous souhaitez aller plus loin, par exemple si vous avez besoin de signaler des événements, des erreurs et des travaux spécifiques à l'application, ou si vous devez signaler les activités de votre application d'une manière différente de celle implémentée dans les classes `EngagementPage`, vous devez utiliser l'API Engagement.</span><span class="sxs-lookup"><span data-stu-id="66b18-106">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementPage` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="66b18-107">L'API Engagement est fournie par la classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="66b18-107">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="66b18-108">Vous pouvez accéder à ces méthodes par l'intermédiaire de `EngagementAgent.Instance`.</span><span class="sxs-lookup"><span data-stu-id="66b18-108">You can access to those methods through `EngagementAgent.Instance`.</span></span>

<span data-ttu-id="66b18-109">Même si le module de l'agent n'a pas été initialisé, chaque appel à l'API est différé et réexécuté une fois l'agent disponible.</span><span class="sxs-lookup"><span data-stu-id="66b18-109">Even if the agent module has not been initialized, each call to the API is deferred, and will be executed again when the agent is available.</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="66b18-110">Concepts liés à Engagement</span><span class="sxs-lookup"><span data-stu-id="66b18-110">Engagement concepts</span></span>
<span data-ttu-id="66b18-111">Les sections qui suivent affinent les [concepts Mobile Engagement](mobile-engagement-concepts.md) courants pour la plateforme Windows Universal.</span><span class="sxs-lookup"><span data-stu-id="66b18-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for the Windows Universal platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="66b18-112">`Session` et `Activity`</span><span class="sxs-lookup"><span data-stu-id="66b18-112">`Session` and `Activity`</span></span>
<span data-ttu-id="66b18-113">Une *activité* est généralement associée à une page de l’application, c’est-à-dire que *l’activité* démarre quand la page est affichée et s’arrête quand la page est fermée : c’est le cas quand le SDK Engagement est intégré à l’aide de la classe `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="66b18-113">An *activity* is usually associated with one page of the application, that is to say the *activity* starts when the page is displayed and stops when the page is closed: this is the case when the Engagement SDK is integrated by using the `EngagementPage` class.</span></span>

<span data-ttu-id="66b18-114">Mais les *activités* peuvent également être contrôlées manuellement à l'aide de l'API Engagement.</span><span class="sxs-lookup"><span data-stu-id="66b18-114">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="66b18-115">Cela vous permet de diviser une page donnée en plusieurs sous-parties, afin d'obtenir davantage de détails sur l'utilisation de cette page (par exemple pour connaître la fréquence et la durée de l’utilisation des boîtes de dialogue à l'intérieur de cette page).</span><span class="sxs-lookup"><span data-stu-id="66b18-115">This allows you to split a given page in several sub parts to get more details about the usage of this page (for example to know how often and how long dialogs are used inside this page).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="66b18-116">Rapports d'activités</span><span class="sxs-lookup"><span data-stu-id="66b18-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="66b18-117">L'utilisateur démarre une nouvelle activité</span><span class="sxs-lookup"><span data-stu-id="66b18-117">User starts a new Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="66b18-118">Référence</span><span class="sxs-lookup"><span data-stu-id="66b18-118">Reference</span></span>
            void StartActivity(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="66b18-119">Vous devez appeler `StartActivity()` chaque fois que l'activité utilisateur change.</span><span class="sxs-lookup"><span data-stu-id="66b18-119">You need to call `StartActivity()` each time the user activity changes.</span></span> <span data-ttu-id="66b18-120">Le premier appel à cette fonction démarre une nouvelle session utilisateur.</span><span class="sxs-lookup"><span data-stu-id="66b18-120">The first call to this function starts a new user session.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="66b18-121">Le Kit de développement logiciel (SDK) appelle automatiquement la méthode EndActivity lorsque l'application est fermée.</span><span class="sxs-lookup"><span data-stu-id="66b18-121">The SDK automatically calls the EndActivity method when the application is closed.</span></span> <span data-ttu-id="66b18-122">Par conséquent, il est FORTEMENT recommandé d'appeler la méthode StartActivity chaque fois que l'activité de l'utilisateur change et de ne JAMAIS appeler la méthode EndActivity, celle-ci forçant la fin de la session active.</span><span class="sxs-lookup"><span data-stu-id="66b18-122">Thus, it is HIGHLY recommended to call the StartActivity method whenever the activity of the user changes, and to NEVER call the EndActivity method, since calling this method forces the current session to be ended.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="66b18-123">Exemple</span><span class="sxs-lookup"><span data-stu-id="66b18-123">Example</span></span>
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="66b18-124">L'utilisateur met fin à l'activité en cours</span><span class="sxs-lookup"><span data-stu-id="66b18-124">User ends his current Activity</span></span>
#### <a name="reference"></a><span data-ttu-id="66b18-125">Référence</span><span class="sxs-lookup"><span data-stu-id="66b18-125">Reference</span></span>
            void EndActivity()

<span data-ttu-id="66b18-126">Cela met fin à l'activité et à la session.</span><span class="sxs-lookup"><span data-stu-id="66b18-126">This ends the activity and the session.</span></span> <span data-ttu-id="66b18-127">Vous ne devez pas appeler cette méthode, à moins de savoir exactement ce que vous faites.</span><span class="sxs-lookup"><span data-stu-id="66b18-127">You should not call this method unless you really know what you're doing.</span></span>

#### <a name="example"></a><span data-ttu-id="66b18-128">Exemple</span><span class="sxs-lookup"><span data-stu-id="66b18-128">Example</span></span>
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a><span data-ttu-id="66b18-129">Rapports de travaux</span><span class="sxs-lookup"><span data-stu-id="66b18-129">Reporting Jobs</span></span>
### <a name="start-a-job"></a><span data-ttu-id="66b18-130">Démarrer un travail</span><span class="sxs-lookup"><span data-stu-id="66b18-130">Start a job</span></span>
#### <a name="reference"></a><span data-ttu-id="66b18-131">Référence</span><span class="sxs-lookup"><span data-stu-id="66b18-131">Reference</span></span>
            void StartJob(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="66b18-132">Vous pouvez utiliser le travail pour effectuer le suivi de certaines tâches sur une période donnée.</span><span class="sxs-lookup"><span data-stu-id="66b18-132">You can use the job to track certains tasks over a period of time.</span></span>

#### <a name="example"></a><span data-ttu-id="66b18-133">Exemple</span><span class="sxs-lookup"><span data-stu-id="66b18-133">Example</span></span>
            // An upload begins...

            // Set the extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a><span data-ttu-id="66b18-134">Mettre fin à un travail</span><span class="sxs-lookup"><span data-stu-id="66b18-134">End a job</span></span>
#### <a name="reference"></a><span data-ttu-id="66b18-135">Référence</span><span class="sxs-lookup"><span data-stu-id="66b18-135">Reference</span></span>
            void EndJob(string name)

<span data-ttu-id="66b18-136">Dès qu'une tâche suivie par un travail est terminée, vous devez appeler la méthode EndJob pour ce travail, en fournissant le nom du travail.</span><span class="sxs-lookup"><span data-stu-id="66b18-136">As soon as a task tracked by a job has been terminated, you should call the EndJob method for this job, by supplying the job name.</span></span>

#### <a name="example"></a><span data-ttu-id="66b18-137">Exemple</span><span class="sxs-lookup"><span data-stu-id="66b18-137">Example</span></span>
            // In the previous section, we started an upload tracking with a job
            // Then, the upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a><span data-ttu-id="66b18-138">Rapports d'événements</span><span class="sxs-lookup"><span data-stu-id="66b18-138">Reporting Events</span></span>
<span data-ttu-id="66b18-139">Il existe trois types d'événements :</span><span class="sxs-lookup"><span data-stu-id="66b18-139">There is three types of events :</span></span>

* <span data-ttu-id="66b18-140">Événements autonomes</span><span class="sxs-lookup"><span data-stu-id="66b18-140">Standalone events</span></span>
* <span data-ttu-id="66b18-141">Événements de session</span><span class="sxs-lookup"><span data-stu-id="66b18-141">Session events</span></span>
* <span data-ttu-id="66b18-142">Événements de travail</span><span class="sxs-lookup"><span data-stu-id="66b18-142">Job events</span></span>

### <a name="standalone-events"></a><span data-ttu-id="66b18-143">Événements autonomes</span><span class="sxs-lookup"><span data-stu-id="66b18-143">Standalone Events</span></span>
#### <a name="reference"></a><span data-ttu-id="66b18-144">Référence</span><span class="sxs-lookup"><span data-stu-id="66b18-144">Reference</span></span>
            void SendEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="66b18-145">Les événements autonomes peuvent se produire en dehors du contexte d'une session.</span><span class="sxs-lookup"><span data-stu-id="66b18-145">Standalone events can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="66b18-146">Exemple</span><span class="sxs-lookup"><span data-stu-id="66b18-146">Example</span></span>
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a><span data-ttu-id="66b18-147">Événements de session</span><span class="sxs-lookup"><span data-stu-id="66b18-147">Session events</span></span>
#### <a name="reference"></a><span data-ttu-id="66b18-148">Référence</span><span class="sxs-lookup"><span data-stu-id="66b18-148">Reference</span></span>
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="66b18-149">Les événements de session servent généralement à signaler les actions effectuées par un utilisateur lors de sa session.</span><span class="sxs-lookup"><span data-stu-id="66b18-149">Session events are usually used to report the actions performed by a user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="66b18-150">Exemple</span><span class="sxs-lookup"><span data-stu-id="66b18-150">Example</span></span>
<span data-ttu-id="66b18-151">**Sans données :**</span><span class="sxs-lookup"><span data-stu-id="66b18-151">**Without data :**</span></span>

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

<span data-ttu-id="66b18-152">**Avec données :**</span><span class="sxs-lookup"><span data-stu-id="66b18-152">**With data :**</span></span>

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a><span data-ttu-id="66b18-153">Événements de travail</span><span class="sxs-lookup"><span data-stu-id="66b18-153">Job Events</span></span>
#### <a name="reference"></a><span data-ttu-id="66b18-154">Référence</span><span class="sxs-lookup"><span data-stu-id="66b18-154">Reference</span></span>
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="66b18-155">Les événements de travail servent généralement à signaler les actions effectuées par un utilisateur lors d'un travail.</span><span class="sxs-lookup"><span data-stu-id="66b18-155">Job events are usually used to report the actions performed by a user during a Job.</span></span>

#### <a name="example"></a><span data-ttu-id="66b18-156">Exemple</span><span class="sxs-lookup"><span data-stu-id="66b18-156">Example</span></span>
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a><span data-ttu-id="66b18-157">Rapports d'erreurs</span><span class="sxs-lookup"><span data-stu-id="66b18-157">Reporting Errors</span></span>
<span data-ttu-id="66b18-158">Il existe trois types d’erreurs :</span><span class="sxs-lookup"><span data-stu-id="66b18-158">There are three types of errors :</span></span>

* <span data-ttu-id="66b18-159">Erreurs autonomes</span><span class="sxs-lookup"><span data-stu-id="66b18-159">Standalone errors</span></span>
* <span data-ttu-id="66b18-160">Erreurs de session</span><span class="sxs-lookup"><span data-stu-id="66b18-160">Session errors</span></span>
* <span data-ttu-id="66b18-161">Erreurs de travail</span><span class="sxs-lookup"><span data-stu-id="66b18-161">Job errors</span></span>

### <a name="standalone-errors"></a><span data-ttu-id="66b18-162">Erreurs autonomes</span><span class="sxs-lookup"><span data-stu-id="66b18-162">Standalone errors</span></span>
#### <a name="reference"></a><span data-ttu-id="66b18-163">Référence</span><span class="sxs-lookup"><span data-stu-id="66b18-163">Reference</span></span>
            void SendError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="66b18-164">Contrairement aux erreurs de session, les erreurs autonomes peuvent se produire en dehors du contexte d'une session.</span><span class="sxs-lookup"><span data-stu-id="66b18-164">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

#### <a name="example"></a><span data-ttu-id="66b18-165">Exemple</span><span class="sxs-lookup"><span data-stu-id="66b18-165">Example</span></span>
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a><span data-ttu-id="66b18-166">Erreurs de session</span><span class="sxs-lookup"><span data-stu-id="66b18-166">Session errors</span></span>
#### <a name="reference"></a><span data-ttu-id="66b18-167">Référence</span><span class="sxs-lookup"><span data-stu-id="66b18-167">Reference</span></span>
            void SendSessionError(string name, Dictionary<object, object> extras = null)

<span data-ttu-id="66b18-168">Les erreurs de session servent généralement à signaler les erreurs affectant l'utilisateur lors de sa session.</span><span class="sxs-lookup"><span data-stu-id="66b18-168">Session errors are usually used to report the errors impacting the user during his session.</span></span>

#### <a name="example"></a><span data-ttu-id="66b18-169">Exemple</span><span class="sxs-lookup"><span data-stu-id="66b18-169">Example</span></span>
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a><span data-ttu-id="66b18-170">Erreurs de travail</span><span class="sxs-lookup"><span data-stu-id="66b18-170">Job Errors</span></span>
#### <a name="reference"></a><span data-ttu-id="66b18-171">Référence</span><span class="sxs-lookup"><span data-stu-id="66b18-171">Reference</span></span>
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

<span data-ttu-id="66b18-172">Les erreurs peuvent être associées à un travail en cours d'exécution plutôt qu'à la session utilisateur en cours.</span><span class="sxs-lookup"><span data-stu-id="66b18-172">Errors can be related to a running job instead of being related to the current user session.</span></span>

#### <a name="example"></a><span data-ttu-id="66b18-173">Exemple</span><span class="sxs-lookup"><span data-stu-id="66b18-173">Example</span></span>
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a><span data-ttu-id="66b18-174">Rapports d'incidents</span><span class="sxs-lookup"><span data-stu-id="66b18-174">Reporting Crashes</span></span>
<span data-ttu-id="66b18-175">L'agent fournit deux méthodes pour gérer les incidents.</span><span class="sxs-lookup"><span data-stu-id="66b18-175">The agent provides two methods to deal with crashes.</span></span>

### <a name="send-an-exception"></a><span data-ttu-id="66b18-176">Envoyer une exception</span><span class="sxs-lookup"><span data-stu-id="66b18-176">Send an exception</span></span>
#### <a name="reference"></a><span data-ttu-id="66b18-177">Référence</span><span class="sxs-lookup"><span data-stu-id="66b18-177">Reference</span></span>
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a><span data-ttu-id="66b18-178">Exemple</span><span class="sxs-lookup"><span data-stu-id="66b18-178">Example</span></span>
<span data-ttu-id="66b18-179">Vous pouvez envoyer une exception à tout moment en appelant :</span><span class="sxs-lookup"><span data-stu-id="66b18-179">You can send an exception at any time by calling :</span></span>

            EngagementAgent.Instance.SendCrash(aCatchedException);

<span data-ttu-id="66b18-180">Vous pouvez également utiliser un paramètre facultatif pour mettre fin à la session Engagement en même temps que l'envoi de l'incident.</span><span class="sxs-lookup"><span data-stu-id="66b18-180">You can also use an optional parameter to terminate the engagement session at the same time than sending the crash.</span></span> <span data-ttu-id="66b18-181">Pour ce faire, appelez :</span><span class="sxs-lookup"><span data-stu-id="66b18-181">To do so, call :</span></span>

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

<span data-ttu-id="66b18-182">Si vous procédez ainsi, la session et les travaux sont fermés juste après l'envoi de l'incident.</span><span class="sxs-lookup"><span data-stu-id="66b18-182">If you do that, the session and jobs will be closed just after sending the crash.</span></span>

### <a name="send-an-unhandled-exception"></a><span data-ttu-id="66b18-183">Envoyer une exception non gérée</span><span class="sxs-lookup"><span data-stu-id="66b18-183">Send an unhandled exception</span></span>
#### <a name="reference"></a><span data-ttu-id="66b18-184">Référence</span><span class="sxs-lookup"><span data-stu-id="66b18-184">Reference</span></span>
            void SendCrash(Exception e)

<span data-ttu-id="66b18-185">Engagement fournit également une méthode pour envoyer des exceptions non gérées si vous avez **DÉSACTIVÉ** le signalement automatique **d’incident** Engagement.</span><span class="sxs-lookup"><span data-stu-id="66b18-185">Engagement also provides a method to send unhandled exceptions if you have **DISABLED** Engagement automatic **crash** reporting.</span></span> <span data-ttu-id="66b18-186">Ceci est particulièrement utile en cas d'utilisation dans le Gestionnaire d'événements UnhandledException de l'application.</span><span class="sxs-lookup"><span data-stu-id="66b18-186">This is especially useful when used inside the application UnhandledException event handler.</span></span>

<span data-ttu-id="66b18-187">Cette méthode met **TOUJOURS** fin aux travaux et à la session Engagement après avoir été appelée.</span><span class="sxs-lookup"><span data-stu-id="66b18-187">This method will **ALWAYS** terminate the engagement session and jobs after being called.</span></span>

#### <a name="example"></a><span data-ttu-id="66b18-188">Exemple</span><span class="sxs-lookup"><span data-stu-id="66b18-188">Example</span></span>
<span data-ttu-id="66b18-189">Vous pouvez l'utiliser pour implémenter votre propre gestionnaire UnhandledExceptionEventArgs.</span><span class="sxs-lookup"><span data-stu-id="66b18-189">You can use it to implement your own UnhandledExceptionEventArgs handler.</span></span> <span data-ttu-id="66b18-190">Par exemple, ajoutez la méthode `Current_UnhandledException` du fichier `App.xaml.cs` :</span><span class="sxs-lookup"><span data-stu-id="66b18-190">For example, add the `Current_UnhandledException` method of the `App.xaml.cs` file :</span></span>

            // In your App.xaml.cs file

            // Code to execute on Unhandled Exceptions
            void Current_UnhandledException(object sender, UnhandledExceptionEventArgs e)
            {
               EngagementAgent.Instance.SendCrash(e.Exception,false);
            }

<span data-ttu-id="66b18-191">Dans App.xaml.cs dans « Public App(){} », ajoutez :</span><span class="sxs-lookup"><span data-stu-id="66b18-191">In App.xaml.cs in "Public App(){}" add:</span></span>

            Application.Current.UnhandledException += Current_UnhandledException;

## <a name="device-id"></a><span data-ttu-id="66b18-192">ID de périphérique</span><span class="sxs-lookup"><span data-stu-id="66b18-192">Device Id</span></span>
            String EngagementAgent.Instance.GetDeviceId()

<span data-ttu-id="66b18-193">Vous pouvez obtenir l'ID de périphérique Engagement en appelant cette méthode.</span><span class="sxs-lookup"><span data-stu-id="66b18-193">You can get the engagement device id by calling this method.</span></span>

## <a name="extras-parameters"></a><span data-ttu-id="66b18-194">Paramètres de suppléments</span><span class="sxs-lookup"><span data-stu-id="66b18-194">Extras parameters</span></span>
<span data-ttu-id="66b18-195">Des données arbitraires peuvent être associées à un événement, à une erreur, à une activité ou à un travail.</span><span class="sxs-lookup"><span data-stu-id="66b18-195">Arbitrary data can be attached to an event, an error, an activity or a job.</span></span> <span data-ttu-id="66b18-196">Ces données peuvent être structurées à l'aide d'un dictionnaire.</span><span class="sxs-lookup"><span data-stu-id="66b18-196">These data can be structured using a dictionary.</span></span> <span data-ttu-id="66b18-197">Les clés et les valeurs peuvent être de n'importe quel type.</span><span class="sxs-lookup"><span data-stu-id="66b18-197">Keys and values can be of any type.</span></span>

<span data-ttu-id="66b18-198">Les données de suppléments sont sérialisées ; par conséquent, si vous souhaitez insérer votre propre type dans des suppléments, vous devez ajouter un contrat de données pour ce type.</span><span class="sxs-lookup"><span data-stu-id="66b18-198">Extras data are serialized so if you want to insert your own type in extras you have to add a data contract for this type.</span></span>

### <a name="example"></a><span data-ttu-id="66b18-199">Exemple</span><span class="sxs-lookup"><span data-stu-id="66b18-199">Example</span></span>
<span data-ttu-id="66b18-200">Nous créons une classe nommée « Person ».</span><span class="sxs-lookup"><span data-stu-id="66b18-200">We create a new class "Person".</span></span>

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

<span data-ttu-id="66b18-201">Ensuite, nous ajoutons une instance `Person` à un supplément.</span><span class="sxs-lookup"><span data-stu-id="66b18-201">Then, we will add a `Person` instance to an extra.</span></span>

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> <span data-ttu-id="66b18-202">Si vous placez d'autres types d'objets, assurez-vous que leur méthode ToString() est implémentée pour retourner une chaîne explicite.</span><span class="sxs-lookup"><span data-stu-id="66b18-202">If you put other types of objects, make sure their ToString() method is implemented to return a human readable string.</span></span>
> 
> 

### <a name="limits"></a><span data-ttu-id="66b18-203">Limites</span><span class="sxs-lookup"><span data-stu-id="66b18-203">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="66b18-204">de clés symétriques</span><span class="sxs-lookup"><span data-stu-id="66b18-204">Keys</span></span>
<span data-ttu-id="66b18-205">Chaque clé de l'objet doit correspondre à l'expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="66b18-205">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="66b18-206">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="66b18-206">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="66b18-207">Taille</span><span class="sxs-lookup"><span data-stu-id="66b18-207">Size</span></span>
<span data-ttu-id="66b18-208">Les suppléments sont limités à **1 024** caractères par appel.</span><span class="sxs-lookup"><span data-stu-id="66b18-208">Extras are limited to **1024** characters per call.</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="66b18-209">Rapports d'informations sur l'application</span><span class="sxs-lookup"><span data-stu-id="66b18-209">Reporting Application Information</span></span>
### <a name="reference"></a><span data-ttu-id="66b18-210">Référence</span><span class="sxs-lookup"><span data-stu-id="66b18-210">Reference</span></span>
            void SendAppInfo(Dictionary<object, object> appInfos)

<span data-ttu-id="66b18-211">Vous pouvez signaler manuellement les informations de suivi (ou toute autre information spécifique à l'application) à l'aide de la fonction SendAppInfo().</span><span class="sxs-lookup"><span data-stu-id="66b18-211">You can manually report tracking information (or any other application specific information) using the SendAppInfo() function.</span></span>

<span data-ttu-id="66b18-212">Notez que ces données peuvent être envoyées de façon incrémentielle : seule la dernière valeur d'une clé donnée sera conservée pour un périphérique donné.</span><span class="sxs-lookup"><span data-stu-id="66b18-212">Note that this data can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span> <span data-ttu-id="66b18-213">Comme pour les suppléments d’événements, utilisez un Dictionary\<object, object\> pour joindre des données.</span><span class="sxs-lookup"><span data-stu-id="66b18-213">Like event extras, use a Dictionary\<object, object\> to attach data.</span></span>

### <a name="example"></a><span data-ttu-id="66b18-214">Exemple</span><span class="sxs-lookup"><span data-stu-id="66b18-214">Example</span></span>
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
              {
                {"birthdate", "1983-12-07"},
                {"gender", "female"}
              };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="66b18-215">Limites</span><span class="sxs-lookup"><span data-stu-id="66b18-215">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="66b18-216">de clés symétriques</span><span class="sxs-lookup"><span data-stu-id="66b18-216">Keys</span></span>
<span data-ttu-id="66b18-217">Chaque clé de l'objet doit correspondre à l'expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="66b18-217">Each key in the object must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*$`

<span data-ttu-id="66b18-218">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="66b18-218">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="66b18-219">Taille</span><span class="sxs-lookup"><span data-stu-id="66b18-219">Size</span></span>
<span data-ttu-id="66b18-220">Les informations de l'application sont limitées à **1 024** caractères par appel.</span><span class="sxs-lookup"><span data-stu-id="66b18-220">Application information is limited to **1024** characters per call.</span></span>

<span data-ttu-id="66b18-221">Dans l'exemple précédent, le JSON envoyé au serveur fait 44 caractères :</span><span class="sxs-lookup"><span data-stu-id="66b18-221">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"birthdate":"1983-12-07","gender":"female"}

## <a name="logging"></a><span data-ttu-id="66b18-222">Journalisation</span><span class="sxs-lookup"><span data-stu-id="66b18-222">Logging</span></span>
### <a name="enable-logging"></a><span data-ttu-id="66b18-223">Activation de la journalisation</span><span class="sxs-lookup"><span data-stu-id="66b18-223">Enable Logging</span></span>
<span data-ttu-id="66b18-224">Le Kit de développement logiciel (SDK) peut être configuré pour générer des journaux de tests dans la console IDE.</span><span class="sxs-lookup"><span data-stu-id="66b18-224">The SDK can be configured to produce test logs in the IDE console.</span></span>
<span data-ttu-id="66b18-225">Ces journaux ne sont pas activés par défaut.</span><span class="sxs-lookup"><span data-stu-id="66b18-225">These logs are not activated by default.</span></span> <span data-ttu-id="66b18-226">Pour personnaliser ce résultat, mettez à jour la propriété `EngagementAgent.Instance.TestLogEnabled` avec une des valeurs disponibles à partir de l'énumération `EngagementTestLogLevel`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="66b18-226">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

