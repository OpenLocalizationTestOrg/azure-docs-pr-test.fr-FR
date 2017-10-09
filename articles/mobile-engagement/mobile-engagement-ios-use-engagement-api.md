---
title: aaaHow tooUse hello Engagement API sur iOS
description: "Dernière iOS SDK - comment tooUse hello Engagement API sur iOS"
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
ms.openlocfilehash: 7fb9b95ad319cf3b1e2de81b5d6aee5b30266069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-ios"></a><span data-ttu-id="70980-103">Comment tooUse hello Engagement API sur iOS</span><span class="sxs-lookup"><span data-stu-id="70980-103">How tooUse hello Engagement API on iOS</span></span>
<span data-ttu-id="70980-104">Ce document est un module complémentaire toohello comment tooIntegrate Engagement sur iOS : il fournit obtenir plus de détails sur comment toouse hello Engagement API tooreport vos statistiques de l’application.</span><span class="sxs-lookup"><span data-stu-id="70980-104">This document is an add-on toohello document How tooIntegrate Engagement on iOS: it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="70980-105">Gardez à l’esprit que si vous ne souhaitez qu’Engagement tooreport sessions, activités, blocages et des informations techniques, de votre application puis hello la plus simple façon est toomake toutes vos personnalisé `UIViewController` objets héritent de hello correspondant `EngagementViewController` classe .</span><span class="sxs-lookup"><span data-stu-id="70980-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your custom `UIViewController` objects inherit from hello corresponding `EngagementViewController` class.</span></span>

<span data-ttu-id="70980-106">Si vous voulez toodo plus, par exemple, si vous avez besoin tooreport les événements d’application spécifique, les erreurs et les tâches, ou si vous avez tooreport activités de votre application d’une manière différente d’une implémentation dans hello hello `EngagementViewController` des classes, vous devez toouse hello API d’engagement.</span><span class="sxs-lookup"><span data-stu-id="70980-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementViewController` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="70980-107">API d’Engagement Hello est fournie par hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="70980-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="70980-108">Une instance de cette classe peut être récupérée en appelant hello `[EngagementAgent shared]` méthode statique (Notez que hello `EngagementAgent` objet retourné est un singleton).</span><span class="sxs-lookup"><span data-stu-id="70980-108">An instance of this class can be retrieved by calling hello `[EngagementAgent shared]` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

<span data-ttu-id="70980-109">Avant que les appels d’API, hello `EngagementAgent` objet doit être initialisé en appelant la méthode hello`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span><span class="sxs-lookup"><span data-stu-id="70980-109">Before any API calls, hello `EngagementAgent` object must be initialized by calling hello method `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="70980-110">Concepts liés à Engagement</span><span class="sxs-lookup"><span data-stu-id="70980-110">Engagement concepts</span></span>
<span data-ttu-id="70980-111">parties suivantes Hello affiner hello commun [Concepts d’Engagement Mobile](mobile-engagement-concepts.md) pour la plateforme iOS de hello.</span><span class="sxs-lookup"><span data-stu-id="70980-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello iOS platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="70980-112">`Session` et `Activity`</span><span class="sxs-lookup"><span data-stu-id="70980-112">`Session` and `Activity`</span></span>
<span data-ttu-id="70980-113">Un *activité* est généralement associé à un écran de l’application hello, qui est toosay hello *activité* démarre lorsque l’écran hello s’affiche et s’arrête lors de la fermeture de l’écran hello : il s’agit de hello cas, lorsque Kit de développement logiciel Engagement Hello est intégré à l’aide de hello `EngagementViewController` classes.</span><span class="sxs-lookup"><span data-stu-id="70980-113">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementViewController` classes.</span></span>

<span data-ttu-id="70980-114">Mais *activités* peut également être contrôlée manuellement à l’aide des API de l’Engagement de hello.</span><span class="sxs-lookup"><span data-stu-id="70980-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="70980-115">Cela permet à un écran toosplit dans plusieurs tooget de parties sub plus de détails sur hello d’utilisation de l’écran (par exemple tooknown la fréquence et la durée pendant laquelle les boîtes de dialogue sont utilisés à l’intérieur de cet écran).</span><span class="sxs-lookup"><span data-stu-id="70980-115">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="70980-116">Rapports d'activités</span><span class="sxs-lookup"><span data-stu-id="70980-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="70980-117">L'utilisateur démarre une nouvelle activité</span><span class="sxs-lookup"><span data-stu-id="70980-117">User starts a new Activity</span></span>
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

<span data-ttu-id="70980-118">Vous devez toocall `startActivity()` chaque activité utilisateur hello change.</span><span class="sxs-lookup"><span data-stu-id="70980-118">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="70980-119">Hello premier appel toothis fonction démarre une nouvelle session de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="70980-119">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="70980-120">L'utilisateur met fin à l'activité en cours</span><span class="sxs-lookup"><span data-stu-id="70980-120">User ends his current Activity</span></span>
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> <span data-ttu-id="70980-121">Vous devez **jamais** appeler cette fonction par vous-même, sauf si vous souhaitez toosplit une utilisation de votre application dans plusieurs sessions : un appel de fonction de toothis se terminer hello session active immédiatement, par conséquent, un appel ultérieur trop`startActivity()`démarre une nouvelle session.</span><span class="sxs-lookup"><span data-stu-id="70980-121">You should **NEVER** call this function by yourself, except if you want toosplit one use of your application into several sessions: a call toothis function would end hello current session immediately, so, a subsequent call too`startActivity()` would start a new session.</span></span> <span data-ttu-id="70980-122">Cette fonction est appelée automatiquement par le Kit de développement logiciel de hello lorsque votre application est fermée.</span><span class="sxs-lookup"><span data-stu-id="70980-122">This function is automatically called by hello SDK when your application is closed.</span></span>
> 
> 

## <a name="reporting-events"></a><span data-ttu-id="70980-123">Rapports d'événements</span><span class="sxs-lookup"><span data-stu-id="70980-123">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="70980-124">Événements de session</span><span class="sxs-lookup"><span data-stu-id="70980-124">Session events</span></span>
<span data-ttu-id="70980-125">Événements de session sont des actions de hello tooreport utilisés généralement effectuées par un utilisateur lors de sa session.</span><span class="sxs-lookup"><span data-stu-id="70980-125">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="70980-126">**Exemple sans données supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="70980-126">**Example without extra data:**</span></span>

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

<span data-ttu-id="70980-127">**Exemple avec des données supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="70980-127">**Example with extra data:**</span></span>

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

### <a name="standalone-events"></a><span data-ttu-id="70980-128">Événements autonomes</span><span class="sxs-lookup"><span data-stu-id="70980-128">Standalone events</span></span>
<span data-ttu-id="70980-129">Événements de toosession contraires, autonome événements peuvent être utilisés en dehors du contexte hello d’une session.</span><span class="sxs-lookup"><span data-stu-id="70980-129">Contrary toosession events, standalone events can be used outside of hello context of a session.</span></span>

<span data-ttu-id="70980-130">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="70980-130">**Example:**</span></span>

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a><span data-ttu-id="70980-131">Rapports d'erreurs</span><span class="sxs-lookup"><span data-stu-id="70980-131">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="70980-132">Erreurs de session</span><span class="sxs-lookup"><span data-stu-id="70980-132">Session errors</span></span>
<span data-ttu-id="70980-133">Session erreurs sont généralement utilisés tooreport hello affecter l’utilisateur de hello lors de sa session.</span><span class="sxs-lookup"><span data-stu-id="70980-133">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="70980-134">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="70980-134">**Example:**</span></span>

    /** hello user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* hello user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="70980-135">Erreurs autonomes</span><span class="sxs-lookup"><span data-stu-id="70980-135">Standalone errors</span></span>
<span data-ttu-id="70980-136">Erreurs toosession contraires, autonome peuvent être utilisés en dehors du contexte hello d’une session.</span><span class="sxs-lookup"><span data-stu-id="70980-136">Contrary toosession errors, standalone errors can be used outside of hello context of a session.</span></span>

<span data-ttu-id="70980-137">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="70980-137">**Example:**</span></span>

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a><span data-ttu-id="70980-138">Rapports de travaux</span><span class="sxs-lookup"><span data-stu-id="70980-138">Reporting Jobs</span></span>
<span data-ttu-id="70980-139">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="70980-139">**Example:**</span></span>

<span data-ttu-id="70980-140">Supposons que vous voulez tooreport hello la durée de votre processus de connexion :</span><span class="sxs-lookup"><span data-stu-id="70980-140">Suppose you want tooreport hello duration of your login process:</span></span>

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

### <a name="report-errors-during-a-job"></a><span data-ttu-id="70980-141">Signaler les erreurs lors d'un travail</span><span class="sxs-lookup"><span data-stu-id="70980-141">Report Errors during a Job</span></span>
<span data-ttu-id="70980-142">Les erreurs peuvent être associée tooa travail au lieu d’être en cours d’exécution liées de session utilisateur en cours toohello.</span><span class="sxs-lookup"><span data-stu-id="70980-142">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="70980-143">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="70980-143">**Example:**</span></span>

<span data-ttu-id="70980-144">Supposons que vous souhaitez tooreport une erreur pendant le processus de connexion :</span><span class="sxs-lookup"><span data-stu-id="70980-144">Suppose you want tooreport an error during your login process:</span></span>

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try toosign in */
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

### <a name="events-during-a-job"></a><span data-ttu-id="70980-145">Événements lors d'un travail</span><span class="sxs-lookup"><span data-stu-id="70980-145">Events during a job</span></span>
<span data-ttu-id="70980-146">Les événements peuvent être associée tooa travail au lieu d’être en cours d’exécution liées de session utilisateur en cours toohello.</span><span class="sxs-lookup"><span data-stu-id="70980-146">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="70980-147">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="70980-147">**Example:**</span></span>

<span data-ttu-id="70980-148">Supposons que nous disposons d’un réseau social, nous utilisons un temps total hello tooreport travail pendant le hello utilisateur est connecté toohello server.</span><span class="sxs-lookup"><span data-stu-id="70980-148">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="70980-149">Hello peuvent recevoir des messages de ses amis, il s’agit d’un événement de tâche.</span><span class="sxs-lookup"><span data-stu-id="70980-149">hello user can receive messages from his friends, this is a job event.</span></span>

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

## <a name="extra-parameters"></a><span data-ttu-id="70980-150">Paramètres supplémentaires</span><span class="sxs-lookup"><span data-stu-id="70980-150">Extra parameters</span></span>
<span data-ttu-id="70980-151">Données arbitraires peuvent être attachés tooevents, les erreurs, les activités et les tâches.</span><span class="sxs-lookup"><span data-stu-id="70980-151">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="70980-152">Ces données peuvent être structurées, elles utilisent la classe NSDictionary d'iOS.</span><span class="sxs-lookup"><span data-stu-id="70980-152">This data can be structured, it uses iOS's NSDictionary class.</span></span>

<span data-ttu-id="70980-153">Notez que les données supplémentaires peuvent contenir des `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` ou d'autres instances `NSDictionary`.</span><span class="sxs-lookup"><span data-stu-id="70980-153">Note that extras can contain `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` or other `NSDictionary` instances.</span></span>

> [!NOTE]
> <span data-ttu-id="70980-154">Hello paramètre supplémentaire est sérialisé au format JSON.</span><span class="sxs-lookup"><span data-stu-id="70980-154">hello extra parameter is serialized in JSON.</span></span> <span data-ttu-id="70980-155">Si vous souhaitez toopass différents objets que hello ceux décrits précédemment, vous devez implémenter hello suivant de méthode dans votre classe :</span><span class="sxs-lookup"><span data-stu-id="70980-155">If you want toopass different objects than hello ones described above, you must implement hello following method in your class:</span></span>
> 
> <span data-ttu-id="70980-156">-(NSString*)JSONRepresentation;</span><span class="sxs-lookup"><span data-stu-id="70980-156">-(NSString*)JSONRepresentation;</span></span>
> 
> <span data-ttu-id="70980-157">méthode Hello doit retourner une représentation JSON de votre objet.</span><span class="sxs-lookup"><span data-stu-id="70980-157">hello method should return a JSON representation of your object.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="70980-158">Exemple</span><span class="sxs-lookup"><span data-stu-id="70980-158">Example</span></span>
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a><span data-ttu-id="70980-159">Limites</span><span class="sxs-lookup"><span data-stu-id="70980-159">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="70980-160">Clés</span><span class="sxs-lookup"><span data-stu-id="70980-160">Keys</span></span>
<span data-ttu-id="70980-161">Chaque clé Bonjour `NSDictionary` doit correspondre à hello expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="70980-161">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="70980-162">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="70980-162">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="70980-163">Taille</span><span class="sxs-lookup"><span data-stu-id="70980-163">Size</span></span>
<span data-ttu-id="70980-164">Fonctionnalités supplémentaires sont trop limitées**1024** caractères par appel (une fois encodées au format JSON par agent d’Engagement hello).</span><span class="sxs-lookup"><span data-stu-id="70980-164">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="70980-165">Bonjour exemple précédent, hello JSON envoyé toohello serveur est 58 caractères :</span><span class="sxs-lookup"><span data-stu-id="70980-165">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="70980-166">Rapports d'informations sur l'application</span><span class="sxs-lookup"><span data-stu-id="70980-166">Reporting Application Information</span></span>
<span data-ttu-id="70980-167">Vous pouvez signaler manuellement le suivi des informations (ou toutes les autres informations spécifiques aux applications) à l’aide de hello `sendAppInfo:` (fonction).</span><span class="sxs-lookup"><span data-stu-id="70980-167">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo:` function.</span></span>

<span data-ttu-id="70980-168">Notez que ces informations peuvent être envoyées de façon incrémentielle : uniquement hello valeur la plus récente d’une clé spécifique est conservé pour un périphérique donné.</span><span class="sxs-lookup"><span data-stu-id="70980-168">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="70980-169">Comme les autres fonctionnalités d’événement, hello `NSDictionary` classe informations tooabstract utilisés de l’application, notez que les tableaux ou les dictionnaires secondaire seront traités en tant que chaînes plats (à l’aide de la sérialisation JSON).</span><span class="sxs-lookup"><span data-stu-id="70980-169">Like event extras, hello `NSDictionary` class is used tooabstract application information, note that arrays or sub-dictionaries will be treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="70980-170">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="70980-170">**Example:**</span></span>

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a><span data-ttu-id="70980-171">Limites</span><span class="sxs-lookup"><span data-stu-id="70980-171">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="70980-172">Clés</span><span class="sxs-lookup"><span data-stu-id="70980-172">Keys</span></span>
<span data-ttu-id="70980-173">Chaque clé Bonjour `NSDictionary` doit correspondre à hello expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="70980-173">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="70980-174">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="70980-174">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="70980-175">Taille</span><span class="sxs-lookup"><span data-stu-id="70980-175">Size</span></span>
<span data-ttu-id="70980-176">Informations sur l’application sont trop limitées**1024** caractères par appel (une fois encodées au format JSON par agent d’Engagement hello).</span><span class="sxs-lookup"><span data-stu-id="70980-176">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="70980-177">Bonjour exemple précédent, hello JSON envoyé toohello serveur est 44 caractères :</span><span class="sxs-lookup"><span data-stu-id="70980-177">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
