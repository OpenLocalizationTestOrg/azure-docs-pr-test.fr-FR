---
title: "aaaAzure API Kit de développement logiciel de Mobile Engagement Web | Documents Microsoft"
description: "Hello les dernières mises à jour et les procédures à suivre pour hello Web SDK pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="68f91-103">Utilisez hello Azure Mobile Engagement API dans une application web</span><span class="sxs-lookup"><span data-stu-id="68f91-103">Use hello Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="68f91-104">Ce document est un document de toohello d’addition qui vous indique comment trop[intégrer Mobile Engagement dans une application web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="68f91-104">This document is an addition toohello document that tells you how too[integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="68f91-105">Il fournit des informations détaillées à propos de la façon dont toouse hello Azure Mobile Engagement API tooreport vos statistiques de l’application.</span><span class="sxs-lookup"><span data-stu-id="68f91-105">It provides in-depth details about how toouse hello Azure Mobile Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="68f91-106">API d’Engagement Mobile Hello est fournie par hello `engagement.agent` objet.</span><span class="sxs-lookup"><span data-stu-id="68f91-106">hello Mobile Engagement API is provided by hello `engagement.agent` object.</span></span> <span data-ttu-id="68f91-107">Hello par défaut de kit de développement Web Azure Mobile Engagement d’alias est `engagement`.</span><span class="sxs-lookup"><span data-stu-id="68f91-107">hello default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="68f91-108">Vous pouvez redéfinir l’alias à partir de la configuration du Kit de développement logiciel hello.</span><span class="sxs-lookup"><span data-stu-id="68f91-108">You can redefine this alias from hello SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="68f91-109">Concepts de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="68f91-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="68f91-110">Hello parties suivantes affiner commun [concepts de Mobile Engagement](mobile-engagement-concepts.md) pour la plateforme web de hello.</span><span class="sxs-lookup"><span data-stu-id="68f91-110">hello following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for hello web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="68f91-111">`Session` et `Activity`</span><span class="sxs-lookup"><span data-stu-id="68f91-111">`Session` and `Activity`</span></span>
<span data-ttu-id="68f91-112">Si l’utilisateur de hello reste inactif pendant plus de quelques secondes entre deux activités, hello séquence de l’utilisateur des activités est fractionné en deux sessions distinctes.</span><span class="sxs-lookup"><span data-stu-id="68f91-112">If hello user stays idle for more than a few seconds between two activities, hello user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="68f91-113">Délai d’expiration de session hello sont appelés des ces quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="68f91-113">These few seconds are called hello session timeout.</span></span>

<span data-ttu-id="68f91-114">Si votre application web ne déclare pas fin hello d’activités des utilisateurs par lui-même (en appelant hello `engagement.agent.endActivity` fonction), serveur de Mobile Engagement hello expire automatiquement hello session utilisateur dans les trois minutes après la fermeture de la page de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="68f91-114">If your web application doesn't declare hello end of user activities by itself (by calling hello `engagement.agent.endActivity` function), hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span> <span data-ttu-id="68f91-115">Il s’agit de délai d’expiration de session de serveur hello.</span><span class="sxs-lookup"><span data-stu-id="68f91-115">This is called hello server session timeout.</span></span>

### `Crash`
<span data-ttu-id="68f91-116">Les rapports automatisés d’exceptions JavaScript non interceptées ne sont pas créés par défaut.</span><span class="sxs-lookup"><span data-stu-id="68f91-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="68f91-117">Toutefois, vous pouvez signaler les pannes manuellement à l’aide de hello `sendCrash` (voir la section de hello sur les rapports d’incidents).</span><span class="sxs-lookup"><span data-stu-id="68f91-117">However, you can report crashes manually by using hello `sendCrash` function (see hello section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="68f91-118">Rapports d’activités</span><span class="sxs-lookup"><span data-stu-id="68f91-118">Reporting activities</span></span>
<span data-ttu-id="68f91-119">Création de rapports sur l’activité des utilisateurs inclut lorsqu’un utilisateur démarre une nouvelle activité et lorsque l’utilisateur de hello met fin à l’activité en cours hello.</span><span class="sxs-lookup"><span data-stu-id="68f91-119">Reporting on user activity includes when a user starts a new activity, and when hello user ends hello current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="68f91-120">L’utilisateur démarre une nouvelle activité</span><span class="sxs-lookup"><span data-stu-id="68f91-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="68f91-121">Vous devez toocall `startActivity()` chaque activité utilisateur change.</span><span class="sxs-lookup"><span data-stu-id="68f91-121">You need toocall `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="68f91-122">Hello premier appel toothis fonction démarre une nouvelle session de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="68f91-122">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-hello-current-activity"></a><span data-ttu-id="68f91-123">Utilisateur met fin à l’activité en cours hello</span><span class="sxs-lookup"><span data-stu-id="68f91-123">User ends hello current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="68f91-124">Vous devez toocall `endActivity()` au moins une fois lorsque hello utilisateur a fini de leur dernière activité.</span><span class="sxs-lookup"><span data-stu-id="68f91-124">You need toocall `endActivity()` at least once when hello user finishes their last activity.</span></span> <span data-ttu-id="68f91-125">Cela permet d’informer hello Kit de développement Web Mobile Engagement qu’utilisateur de hello est actuellement inactif et que la session d’utilisateur hello a besoin toobe fermés après l’expiration du délai d’expiration de session hello.</span><span class="sxs-lookup"><span data-stu-id="68f91-125">This informs hello Mobile Engagement Web SDK that hello user is currently idle, and that hello user session needs toobe closed after hello session timeout expires.</span></span> <span data-ttu-id="68f91-126">Si vous appelez `startActivity()` avant l’expiration du délai d’expiration de session hello, hello simplement la reprise de session.</span><span class="sxs-lookup"><span data-stu-id="68f91-126">If you call `startActivity()` before hello session timeout expires, hello session is simply resumed.</span></span>

<span data-ttu-id="68f91-127">Étant donné qu’aucun appel fiable pour la fermeture de la fenêtre de navigateur hello, il est souvent de fin de hello toocatch impossible ou difficile d’activités des utilisateurs à l’intérieur d’un environnement web.</span><span class="sxs-lookup"><span data-stu-id="68f91-127">Because there's no reliable call for when hello navigator window is closed, it's often difficult or impossible toocatch hello end of user activities inside a web environment.</span></span> <span data-ttu-id="68f91-128">Qui est hello pourquoi Mobile Engagement serveur expire automatiquement session d’utilisateur hello dans les trois minutes après la fermeture de la page de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="68f91-128">That's why hello Mobile Engagement server automatically expires hello user session within three minutes after hello application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="68f91-129">Rapports d’événements</span><span class="sxs-lookup"><span data-stu-id="68f91-129">Reporting events</span></span>
<span data-ttu-id="68f91-130">Les rapports d’événements couvrent les événements de session et les événements autonomes.</span><span class="sxs-lookup"><span data-stu-id="68f91-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="68f91-131">Événements de session</span><span class="sxs-lookup"><span data-stu-id="68f91-131">Session events</span></span>
<span data-ttu-id="68f91-132">Événements de session sont généralement des actions de hello tooreport utilisé effectuées par un utilisateur au cours de la session de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="68f91-132">Session events usually are used tooreport hello actions performed by a user during hello user's session.</span></span>

<span data-ttu-id="68f91-133">**Exemple sans données supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="68f91-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="68f91-134">**Exemple avec des données supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="68f91-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="68f91-135">Événements autonomes</span><span class="sxs-lookup"><span data-stu-id="68f91-135">Standalone events</span></span>
<span data-ttu-id="68f91-136">Contrairement aux événements de session, les événements autonome peuvent se produire en dehors du contexte hello d’une session.</span><span class="sxs-lookup"><span data-stu-id="68f91-136">Unlike session events, standalone events can occur outside hello context of a session.</span></span>

<span data-ttu-id="68f91-137">Pour cela, utilisez ``engagement.agent.sendEvent`` au lieu de ``engagement.agent.sendSessionEvent``.</span><span class="sxs-lookup"><span data-stu-id="68f91-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="68f91-138">Rapports d’erreurs</span><span class="sxs-lookup"><span data-stu-id="68f91-138">Reporting errors</span></span>
<span data-ttu-id="68f91-139">Les rapports d’erreurs couvrent les erreurs de session et les erreurs autonomes.</span><span class="sxs-lookup"><span data-stu-id="68f91-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="68f91-140">Erreurs de session</span><span class="sxs-lookup"><span data-stu-id="68f91-140">Session errors</span></span>
<span data-ttu-id="68f91-141">Erreurs de session sont généralement des erreurs hello tooreport utilisé qui ont un impact sur l’utilisateur de hello pendant la session de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="68f91-141">Session errors usually are used tooreport hello errors that have an impact on hello user during hello user's session.</span></span>

<span data-ttu-id="68f91-142">**Exemple sans données supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="68f91-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="68f91-143">**Exemple avec des données supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="68f91-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="68f91-144">Erreurs autonomes</span><span class="sxs-lookup"><span data-stu-id="68f91-144">Standalone errors</span></span>
<span data-ttu-id="68f91-145">Contrairement aux erreurs de session, les erreurs autonome peuvent se produire en dehors du contexte hello d’une session.</span><span class="sxs-lookup"><span data-stu-id="68f91-145">Unlike session errors, standalone errors can occur outside hello context of a session.</span></span>

<span data-ttu-id="68f91-146">Pour cela, utilisez `engagement.agent.sendError` au lieu de `engagement.agent.sendSessionError`.</span><span class="sxs-lookup"><span data-stu-id="68f91-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="68f91-147">Rapports de travaux</span><span class="sxs-lookup"><span data-stu-id="68f91-147">Reporting jobs</span></span>
<span data-ttu-id="68f91-148">Les rapports de travaux couvrent les erreurs et les événements qui se produisent lors d’un travail, ainsi que les rapports d’incidents.</span><span class="sxs-lookup"><span data-stu-id="68f91-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="68f91-149">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="68f91-149">**Example:**</span></span>

<span data-ttu-id="68f91-150">Si vous souhaitez toomonitor une requête AJAX, vous utiliseriez suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="68f91-150">If you want toomonitor an AJAX request, you'd use hello following:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="68f91-151">Signaler les erreurs lors d’un travail</span><span class="sxs-lookup"><span data-stu-id="68f91-151">Reporting errors during a job</span></span>
<span data-ttu-id="68f91-152">Erreurs peuvent être associée tooa travail au lieu de la session utilisateur en cours toohello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="68f91-152">Errors can be related tooa running job instead of toohello current user session.</span></span>

<span data-ttu-id="68f91-153">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="68f91-153">**Example:**</span></span>

<span data-ttu-id="68f91-154">Si vous souhaitez tooreport une erreur si une requête AJAX échoue :</span><span class="sxs-lookup"><span data-stu-id="68f91-154">If you want tooreport an error if an AJAX request fails:</span></span>

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="68f91-155">Rapports d’événements pendant un travail</span><span class="sxs-lookup"><span data-stu-id="68f91-155">Reporting events during a job</span></span>
<span data-ttu-id="68f91-156">Les événements peuvent être associée tooa exécution de travail au lieu de la session utilisateur en cours toohello, grâce toohello `engagement.agent.sendJobEvent` (fonction).</span><span class="sxs-lookup"><span data-stu-id="68f91-156">Events can be related tooa running job instead of toohello current user session, thanks toohello `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="68f91-157">Cette fonction fonctionne exactement comme `engagement.agent.sendJobError`.</span><span class="sxs-lookup"><span data-stu-id="68f91-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="68f91-158">Rapports d’incidents</span><span class="sxs-lookup"><span data-stu-id="68f91-158">Reporting crashes</span></span>
<span data-ttu-id="68f91-159">Hello d’utilisation `sendCrash` fonction tooreport tombe en panne manuellement.</span><span class="sxs-lookup"><span data-stu-id="68f91-159">Use hello `sendCrash` function tooreport crashes manually.</span></span>

<span data-ttu-id="68f91-160">Hello `crashid` argument est une chaîne qui identifie le type hello d’incident.</span><span class="sxs-lookup"><span data-stu-id="68f91-160">hello `crashid` argument is a string that identifies hello type of crash.</span></span>
<span data-ttu-id="68f91-161">Hello `crash` argument est généralement la trace de la pile hello d’incident hello sous forme de chaîne.</span><span class="sxs-lookup"><span data-stu-id="68f91-161">hello `crash` argument usually is hello stack trace of hello crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="68f91-162">Paramètres supplémentaires</span><span class="sxs-lookup"><span data-stu-id="68f91-162">Extra parameters</span></span>
<span data-ttu-id="68f91-163">Vous pouvez attacher des événements de tooan de données arbitraires, erreur, activité ou la tâche.</span><span class="sxs-lookup"><span data-stu-id="68f91-163">You can attach arbitrary data tooan event, error, activity, or job.</span></span>

<span data-ttu-id="68f91-164">les données de salutation peuvent être n’importe quel objet JSON (mais pas un tableau ou type primitif).</span><span class="sxs-lookup"><span data-stu-id="68f91-164">hello data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="68f91-165">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="68f91-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="68f91-166">limites</span><span class="sxs-lookup"><span data-stu-id="68f91-166">Limits</span></span>
<span data-ttu-id="68f91-167">Les limites qui s’appliquent les paramètres tooextra sont dans des domaines de hello des expressions régulières pour les clés, les types valeur et taille.</span><span class="sxs-lookup"><span data-stu-id="68f91-167">Limits that apply tooextra parameters are in hello areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="68f91-168">Clés</span><span class="sxs-lookup"><span data-stu-id="68f91-168">Keys</span></span>
<span data-ttu-id="68f91-169">Chaque clé de l’objet de hello doit correspondre hello expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="68f91-169">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="68f91-170">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="68f91-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="68f91-171">Valeurs</span><span class="sxs-lookup"><span data-stu-id="68f91-171">Values</span></span>
<span data-ttu-id="68f91-172">Les valeurs sont limitée toostring, nombre et types booléens.</span><span class="sxs-lookup"><span data-stu-id="68f91-172">Values are limited toostring, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="68f91-173">Taille</span><span class="sxs-lookup"><span data-stu-id="68f91-173">Size</span></span>
<span data-ttu-id="68f91-174">Fonctionnalités supplémentaires sont limitées too1, 024 caractères par appel (après que hello Kit de développement Web Mobile Engagement qu’elle l’encode au format JSON).</span><span class="sxs-lookup"><span data-stu-id="68f91-174">Extras are limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="68f91-175">Rapports d’informations sur l’application</span><span class="sxs-lookup"><span data-stu-id="68f91-175">Reporting application information</span></span>
<span data-ttu-id="68f91-176">Vous pouvez signaler manuellement le suivi des informations (ou toutes autres informations spécifiques à l’application) à l’aide de hello `sendAppInfo()` (fonction).</span><span class="sxs-lookup"><span data-stu-id="68f91-176">You can manually report tracking information (or any other application-specific information) by using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="68f91-177">Notez que ces informations peuvent être envoyées de façon incrémentielle.</span><span class="sxs-lookup"><span data-stu-id="68f91-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="68f91-178">Uniquement hello valeur la plus récente pour une clé spécifique est conservé pour un périphérique spécifique.</span><span class="sxs-lookup"><span data-stu-id="68f91-178">Only hello latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="68f91-179">Comme événement extras, vous pouvez utiliser les informations de l’application de JSON objet tooabstract.</span><span class="sxs-lookup"><span data-stu-id="68f91-179">Like event extras, you can use any JSON object tooabstract application information.</span></span> <span data-ttu-id="68f91-180">Notez que les tableaux ou les sous-objets sont traités comme des chaînes plates (à l’aide de la sérialisation JSON).</span><span class="sxs-lookup"><span data-stu-id="68f91-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="68f91-181">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="68f91-181">**Example:**</span></span>

<span data-ttu-id="68f91-182">Voici un exemple de code pour le sexe de l’utilisateur expéditeur hello et date de naissance :</span><span class="sxs-lookup"><span data-stu-id="68f91-182">Here is a code sample for sending hello user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="68f91-183">limites</span><span class="sxs-lookup"><span data-stu-id="68f91-183">Limits</span></span>
<span data-ttu-id="68f91-184">Les limites qui s’appliquent les informations de tooapplication sont dans des zones de hello des expressions régulières pour les clés et la taille.</span><span class="sxs-lookup"><span data-stu-id="68f91-184">Limits that apply tooapplication information are in hello areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="68f91-185">Clés</span><span class="sxs-lookup"><span data-stu-id="68f91-185">Keys</span></span>
<span data-ttu-id="68f91-186">Chaque clé de l’objet de hello doit correspondre hello expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="68f91-186">Each key in hello object must match hello following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="68f91-187">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="68f91-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="68f91-188">Taille</span><span class="sxs-lookup"><span data-stu-id="68f91-188">Size</span></span>
<span data-ttu-id="68f91-189">Informations de l’application sont limitée too1, 024 caractères par appel (après que hello Kit de développement Web Mobile Engagement qu’elle l’encode au format JSON).</span><span class="sxs-lookup"><span data-stu-id="68f91-189">Application information is limited too1,024 characters per call (after hello Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="68f91-190">Bonjour précédent exemple, hello JSON envoyé toohello server est 44 caractères :</span><span class="sxs-lookup"><span data-stu-id="68f91-190">In hello preceding example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
