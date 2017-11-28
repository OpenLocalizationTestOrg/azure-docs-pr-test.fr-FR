---
title: Utilisation de l'API Engagement sur iOS
description: "Kit de développement logiciel (SDK) iOS le plus récent - Utilisation de l'API Engagement sur iOS"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1fb4509e-3804-46c1-949f-1cf727f91f9f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a31424da98205e97bdf57010cccfd044360f03dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-ios"></a><span data-ttu-id="4ae46-103">Utilisation de l'API Engagement sur iOS</span><span class="sxs-lookup"><span data-stu-id="4ae46-103">How to Use the Engagement API on iOS</span></span>
<span data-ttu-id="4ae46-104">Ce document est un module complémentaire du document Intégration d'Engagement sur iOS : il fournit des informations détaillées sur l'utilisation de l'API Engagement pour signaler les statistiques de votre application.</span><span class="sxs-lookup"><span data-stu-id="4ae46-104">This document is an add-on to the document How to Integrate Engagement on iOS: it provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="4ae46-105">Rappelez-vous que si vous souhaitez qu’Engagement établisse uniquement le rapport des sessions, des activités, des incidents et des informations techniques de votre application, dans ce cas le moyen le plus simple est de faire `UIViewController`hériter tous vos objets personnalisés de la classe `EngagementViewController` correspondante.</span><span class="sxs-lookup"><span data-stu-id="4ae46-105">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your custom `UIViewController` objects inherit from the corresponding `EngagementViewController` class.</span></span>

<span data-ttu-id="4ae46-106">Si vous souhaitez aller plus loin, par exemple si vous avez besoin de signaler des événements, des erreurs et des tâches spécifiques à l'application, ou si vous devez signaler les activités de votre application d'une autre manière que celle implémentée dans les classes `EngagementViewController`, vous devez alors utiliser l'API Engagement.</span><span class="sxs-lookup"><span data-stu-id="4ae46-106">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementViewController` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="4ae46-107">L'API Engagement est fournie par la classe `EngagementAgent` .</span><span class="sxs-lookup"><span data-stu-id="4ae46-107">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="4ae46-108">Une instance de cette classe peut être récupérée en appelant la méthode statique `[EngagementAgent shared]` (notez que l'objet `EngagementAgent` retourné est un singleton).</span><span class="sxs-lookup"><span data-stu-id="4ae46-108">An instance of this class can be retrieved by calling the `[EngagementAgent shared]` static method (note that the `EngagementAgent` object returned is a singleton).</span></span>

<span data-ttu-id="4ae46-109">Avant les appels d'API, l'objet `EngagementAgent` doit être initialisé en appelant la méthode `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span><span class="sxs-lookup"><span data-stu-id="4ae46-109">Before any API calls, the `EngagementAgent` object must be initialized by calling the method `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="4ae46-110">Concepts liés à Engagement</span><span class="sxs-lookup"><span data-stu-id="4ae46-110">Engagement concepts</span></span>
<span data-ttu-id="4ae46-111">Les sections qui suivent affinent les [concepts Mobile Engagement](mobile-engagement-concepts.md) courants pour la plateforme iOS.</span><span class="sxs-lookup"><span data-stu-id="4ae46-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for the iOS platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="4ae46-112">`Session` et `Activity`</span><span class="sxs-lookup"><span data-stu-id="4ae46-112">`Session` and `Activity`</span></span>
<span data-ttu-id="4ae46-113">Une *activité* est généralement associée à un écran de l’application, c’est-à-dire que *l’activité* démarre lorsque l’écran s’affiche et s’arrête lorsque l’écran est fermé. C’est le cas lorsque le Kit de développement logiciel (SDK) Engagement est intégré à l’aide des classes `EngagementViewController`.</span><span class="sxs-lookup"><span data-stu-id="4ae46-113">An *activity* is usually associated with one screen of the application, that is to say the *activity* starts when the screen is displayed and stops when the screen is closed: this is the case when the Engagement SDK is integrated by using the `EngagementViewController` classes.</span></span>

<span data-ttu-id="4ae46-114">Mais les *activités* peuvent également être contrôlées manuellement à l'aide de l'API Engagement.</span><span class="sxs-lookup"><span data-stu-id="4ae46-114">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="4ae46-115">Cela permet de fractionner un écran donné en plusieurs sous-parties pour obtenir plus d'informations sur l'utilisation de cet écran (par exemple la fréquence et la durée d'utilisation des boîtes de dialogue dans cet écran).</span><span class="sxs-lookup"><span data-stu-id="4ae46-115">This allows to split a given screen in several sub parts to get more details about the usage of this screen (for example to known how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="4ae46-116">Rapports d'activités</span><span class="sxs-lookup"><span data-stu-id="4ae46-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="4ae46-117">L'utilisateur démarre une nouvelle activité</span><span class="sxs-lookup"><span data-stu-id="4ae46-117">User starts a new Activity</span></span>
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

<span data-ttu-id="4ae46-118">Vous devez appeler `startActivity()` chaque fois que l'activité utilisateur change.</span><span class="sxs-lookup"><span data-stu-id="4ae46-118">You need to call `startActivity()` each time the user activity changes.</span></span> <span data-ttu-id="4ae46-119">Le premier appel à cette fonction démarre une nouvelle session utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4ae46-119">The first call to this function starts a new user session.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="4ae46-120">L'utilisateur met fin à l'activité en cours</span><span class="sxs-lookup"><span data-stu-id="4ae46-120">User ends his current Activity</span></span>
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> <span data-ttu-id="4ae46-121">Vous ne devez **JAMAIS** appeler cette fonction vous-même, sauf si vous souhaitez fractionner une utilisation de votre application dans plusieurs sessions : un appel de cette fonction mettrait immédiatement fin à la session en cours, et par conséquent un appel ultérieur à `startActivity()` démarrerait une nouvelle session.</span><span class="sxs-lookup"><span data-stu-id="4ae46-121">You should **NEVER** call this function by yourself, except if you want to split one use of your application into several sessions: a call to this function would end the current session immediately, so, a subsequent call to `startActivity()` would start a new session.</span></span> <span data-ttu-id="4ae46-122">Cette fonction est appelée automatiquement par le SDK lorsque votre application est fermée.</span><span class="sxs-lookup"><span data-stu-id="4ae46-122">This function is automatically called by the SDK when your application is closed.</span></span>
> 
> 

## <a name="reporting-events"></a><span data-ttu-id="4ae46-123">Rapports d'événements</span><span class="sxs-lookup"><span data-stu-id="4ae46-123">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="4ae46-124">Événements de session</span><span class="sxs-lookup"><span data-stu-id="4ae46-124">Session events</span></span>
<span data-ttu-id="4ae46-125">Les événements de session servent généralement à signaler les actions effectuées par un utilisateur lors de sa session.</span><span class="sxs-lookup"><span data-stu-id="4ae46-125">Session events are usually used to report the actions performed by a user during his session.</span></span>

<span data-ttu-id="4ae46-126">**Exemple sans données supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="4ae46-126">**Example without extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:nil];
            ...
       }
       [...]
    }

<span data-ttu-id="4ae46-127">**Exemple avec des données supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="4ae46-127">**Example with extra data:**</span></span>

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        NSMutableDictionary* extras = [NSMutableDictionary dictionary];
        [extras setObject:[NSNumber numberWithInt:toInterfaceOrientation] forKey:@"to_orientation_id"];
        [extras setObject:[NSNumber numberWithDouble:duration] forKey:@"duration"];
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:extras];
            ...
       }
       [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="4ae46-128">Événements autonomes</span><span class="sxs-lookup"><span data-stu-id="4ae46-128">Standalone events</span></span>
<span data-ttu-id="4ae46-129">Contrairement aux événements de session, les événements d'autonomes peuvent être utilisés en dehors du contexte d'une session.</span><span class="sxs-lookup"><span data-stu-id="4ae46-129">Contrary to session events, standalone events can be used outside of the context of a session.</span></span>

<span data-ttu-id="4ae46-130">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="4ae46-130">**Example:**</span></span>

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a><span data-ttu-id="4ae46-131">Rapports d'erreurs</span><span class="sxs-lookup"><span data-stu-id="4ae46-131">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="4ae46-132">Erreurs de session</span><span class="sxs-lookup"><span data-stu-id="4ae46-132">Session errors</span></span>
<span data-ttu-id="4ae46-133">Les erreurs de session servent généralement à signaler les erreurs affectant l'utilisateur lors de sa session.</span><span class="sxs-lookup"><span data-stu-id="4ae46-133">Session errors are usually used to report the errors impacting the user during his session.</span></span>

<span data-ttu-id="4ae46-134">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="4ae46-134">**Example:**</span></span>

    /** The user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* The user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="4ae46-135">Erreurs autonomes</span><span class="sxs-lookup"><span data-stu-id="4ae46-135">Standalone errors</span></span>
<span data-ttu-id="4ae46-136">Contrairement aux erreurs de session, les erreurs autonomes peuvent être utilisées en dehors du contexte d'une session.</span><span class="sxs-lookup"><span data-stu-id="4ae46-136">Contrary to session errors, standalone errors can be used outside of the context of a session.</span></span>

<span data-ttu-id="4ae46-137">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="4ae46-137">**Example:**</span></span>

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a><span data-ttu-id="4ae46-138">Rapports de travaux</span><span class="sxs-lookup"><span data-stu-id="4ae46-138">Reporting Jobs</span></span>
<span data-ttu-id="4ae46-139">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="4ae46-139">**Example:**</span></span>

<span data-ttu-id="4ae46-140">Supposons que vous voulez créer un rapport de la durée de votre processus de connexion :</span><span class="sxs-lookup"><span data-stu-id="4ae46-140">Suppose you want to report the duration of your login process:</span></span>

    [...]
    -(void)signIn
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      [... sign in ...]

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    }
    [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="4ae46-141">Signaler les erreurs lors d'un travail</span><span class="sxs-lookup"><span data-stu-id="4ae46-141">Report Errors during a Job</span></span>
<span data-ttu-id="4ae46-142">Les erreurs peuvent être associées à un travail en cours d'exécution plutôt qu'à la session utilisateur en cours.</span><span class="sxs-lookup"><span data-stu-id="4ae46-142">Errors can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="4ae46-143">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="4ae46-143">**Example:**</span></span>

<span data-ttu-id="4ae46-144">Supposons que vous souhaitez signaler une erreur pendant le processus de connexion :</span><span class="sxs-lookup"><span data-stu-id="4ae46-144">Suppose you want to report an error during your login process:</span></span>

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try to sign in */
        NSError* error = nil;
        [self trySigin:&error];
        success = error == nil;

        /* If an error occured report it */
        if(!success)
        {
          [[EngagementAgent shared] sendJobError:@"sign_in_error"
                         jobName:@"sign_in"
                          extras:[NSDictionary dictionaryWithObject:[error localizedDescription] forKey:@"error"]];

          /* Retry after a moment */
          [NSThread sleepForTimeInterval:20];
        }
      }

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    };
    [...]

### <a name="events-during-a-job"></a><span data-ttu-id="4ae46-145">Événements lors d'un travail</span><span class="sxs-lookup"><span data-stu-id="4ae46-145">Events during a job</span></span>
<span data-ttu-id="4ae46-146">Les événements peuvent être associés à un travail en cours d'exécution au lieu de se rapporter à la session utilisateur en cours.</span><span class="sxs-lookup"><span data-stu-id="4ae46-146">Events can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="4ae46-147">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="4ae46-147">**Example:**</span></span>

<span data-ttu-id="4ae46-148">Supposons que nous disposons d'un réseau social et que nous utilisons une tâche pour signaler la durée totale pendant laquelle l'utilisateur est connecté au serveur.</span><span class="sxs-lookup"><span data-stu-id="4ae46-148">Suppose we have a social network, and we use a job to report the total time during which the user is connected to the server.</span></span> <span data-ttu-id="4ae46-149">L'utilisateur peut recevoir des messages de ses amis : il s'agit d'un événement de tâche.</span><span class="sxs-lookup"><span data-stu-id="4ae46-149">The user can receive messages from his friends, this is a job event.</span></span>

    [...]
    - (void) signin
    {
      [...Sign in code...]
      [[EngagementAgent shared] startJob:@"connection" extras:nil];
    }
    [...]
    - (void) signout
    {
      [...Sign out code...]
      [[EngagementAgent shared] endJob:@"connection"];
    }
    [...]
    - (void) onMessageReceived
    {
      [...Notify user...]
      [[EngagementAgent shared] sendJobEvent:@"connection" jobName:@"message_received" extras:nil];
    }
    [...]

## <a name="extra-parameters"></a><span data-ttu-id="4ae46-150">Paramètres supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4ae46-150">Extra parameters</span></span>
<span data-ttu-id="4ae46-151">Des données arbitraires peuvent être associées à des événements, des erreurs, des activités et des tâches.</span><span class="sxs-lookup"><span data-stu-id="4ae46-151">Arbitrary data can be attached to events, errors, activities and jobs.</span></span>

<span data-ttu-id="4ae46-152">Ces données peuvent être structurées, elles utilisent la classe NSDictionary d'iOS.</span><span class="sxs-lookup"><span data-stu-id="4ae46-152">This data can be structured, it uses iOS's NSDictionary class.</span></span>

<span data-ttu-id="4ae46-153">Notez que les données supplémentaires peuvent contenir des `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` ou d'autres instances `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="4ae46-153">Note that extras can contain `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` or other `NSDictionary` instances.</span></span>

> [!NOTE]
> <span data-ttu-id="4ae46-154">Le paramètre supplémentaire est sérialisé au format JSON.</span><span class="sxs-lookup"><span data-stu-id="4ae46-154">The extra parameter is serialized in JSON.</span></span> <span data-ttu-id="4ae46-155">Si vous souhaitez transmettre des objets différents de ceux décrits ci-dessus, vous devez implémenter la méthode suivante dans votre classe :</span><span class="sxs-lookup"><span data-stu-id="4ae46-155">If you want to pass different objects than the ones described above, you must implement the following method in your class:</span></span>
> 
> <span data-ttu-id="4ae46-156">-(NSString*)JSONRepresentation;</span><span class="sxs-lookup"><span data-stu-id="4ae46-156">-(NSString*)JSONRepresentation;</span></span>
> 
> <span data-ttu-id="4ae46-157">La méthode doit retourner une représentation JSON de votre objet.</span><span class="sxs-lookup"><span data-stu-id="4ae46-157">The method should return a JSON representation of your object.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="4ae46-158">Exemple</span><span class="sxs-lookup"><span data-stu-id="4ae46-158">Example</span></span>
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a><span data-ttu-id="4ae46-159">Limites</span><span class="sxs-lookup"><span data-stu-id="4ae46-159">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="4ae46-160">de clés symétriques</span><span class="sxs-lookup"><span data-stu-id="4ae46-160">Keys</span></span>
<span data-ttu-id="4ae46-161">Chaque clé dans `NSDictionary` doit correspondre à l'expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="4ae46-161">Each key in the `NSDictionary` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="4ae46-162">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="4ae46-162">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="4ae46-163">Taille</span><span class="sxs-lookup"><span data-stu-id="4ae46-163">Size</span></span>
<span data-ttu-id="4ae46-164">Les données supplémentaires sont limitées à **1024** caractères par appel (une fois codées au format JSON par l'agent Engagement).</span><span class="sxs-lookup"><span data-stu-id="4ae46-164">Extras are limited to **1024** characters per call (once encoded in JSON by the Engagement agent).</span></span>

<span data-ttu-id="4ae46-165">Dans l'exemple précédent, le JSON envoyé au serveur compte 58 caractères :</span><span class="sxs-lookup"><span data-stu-id="4ae46-165">In the previous example, the JSON sent to the server is 58 characters long:</span></span>

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="4ae46-166">Rapports d'informations sur l'application</span><span class="sxs-lookup"><span data-stu-id="4ae46-166">Reporting Application Information</span></span>
<span data-ttu-id="4ae46-167">Vous pouvez signaler manuellement les informations de suivi (ou toutes autres informations spécifiques aux applications) à l'aide de la fonction `sendAppInfo:` .</span><span class="sxs-lookup"><span data-stu-id="4ae46-167">You can manually report tracking information (or any other application specific information) using the `sendAppInfo:` function.</span></span>

<span data-ttu-id="4ae46-168">Notez que ces informations peuvent être envoyées de façon incrémentielle : seule la dernière valeur d'une clé donnée sera conservée pour un périphérique donné.</span><span class="sxs-lookup"><span data-stu-id="4ae46-168">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="4ae46-169">Comme c'est le cas avec les suppléments d'événement, la classe `NSDictionary` est utilisée pour extraire des informations de l'application. Notez que les tableaux ou sous-dictionnaires seront traités en tant que chaînes plates (à l'aide de la sérialisation JSON).</span><span class="sxs-lookup"><span data-stu-id="4ae46-169">Like event extras, the `NSDictionary` class is used to abstract application information, note that arrays or sub-dictionaries will be treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="4ae46-170">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="4ae46-170">**Example:**</span></span>

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a><span data-ttu-id="4ae46-171">Limites</span><span class="sxs-lookup"><span data-stu-id="4ae46-171">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="4ae46-172">de clés symétriques</span><span class="sxs-lookup"><span data-stu-id="4ae46-172">Keys</span></span>
<span data-ttu-id="4ae46-173">Chaque clé dans `NSDictionary` doit correspondre à l'expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="4ae46-173">Each key in the `NSDictionary` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="4ae46-174">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="4ae46-174">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="4ae46-175">Taille</span><span class="sxs-lookup"><span data-stu-id="4ae46-175">Size</span></span>
<span data-ttu-id="4ae46-176">Les informations sur l'application sont limitées à **1024** caractères par appel (une fois codées au format JSON par l'agent Engagement).</span><span class="sxs-lookup"><span data-stu-id="4ae46-176">Application information are limited to **1024** characters per call (once encoded in JSON by the Engagement agent).</span></span>

<span data-ttu-id="4ae46-177">Dans l'exemple précédent, le JSON envoyé au serveur fait 44 caractères :</span><span class="sxs-lookup"><span data-stu-id="4ae46-177">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
