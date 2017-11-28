---
title: API du SDK web Azure Mobile Engagement | Microsoft Docs
description: "Dernières mises à jour et procédures du Kit de développement logiciel (SDK) web pour Azure Mobile Engagement"
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
ms.openlocfilehash: 54c22ce6a03e382b1bbde102bccc97deec249b30
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-azure-mobile-engagement-api-in-a-web-application"></a><span data-ttu-id="c1e8b-103">Utiliser l’API Azure Mobile Engagement dans une application web</span><span class="sxs-lookup"><span data-stu-id="c1e8b-103">Use the Azure Mobile Engagement API in a web application</span></span>
<span data-ttu-id="c1e8b-104">Ce document vient compléter celui vous décrivant comment [intégrer Mobile Engagement dans une application web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="c1e8b-104">This document is an addition to the document that tells you how to [integrate Mobile Engagement in a web application](mobile-engagement-web-integrate-engagement.md).</span></span> <span data-ttu-id="c1e8b-105">Il fournit des informations détaillées sur l’utilisation de l’API Azure Mobile Engagement pour signaler les statistiques de votre application.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-105">It provides in-depth details about how to use the Azure Mobile Engagement API to report your application statistics.</span></span>

<span data-ttu-id="c1e8b-106">L’API Mobile Engagement est fournie par l’objet `engagement.agent` .</span><span class="sxs-lookup"><span data-stu-id="c1e8b-106">The Mobile Engagement API is provided by the `engagement.agent` object.</span></span> <span data-ttu-id="c1e8b-107">L’alias du Kit de développement logiciel (SDK) web d’Azure Mobile Engagement par défaut est `engagement`.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-107">The default Azure Mobile Engagement Web SDK alias is `engagement`.</span></span> <span data-ttu-id="c1e8b-108">Vous pouvez redéfinir cet alias dans la configuration du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="c1e8b-108">You can redefine this alias from the SDK configuration.</span></span>

## <a name="mobile-engagement-concepts"></a><span data-ttu-id="c1e8b-109">Concepts de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="c1e8b-109">Mobile Engagement concepts</span></span>
<span data-ttu-id="c1e8b-110">Les sections qui suivent affinent les [concepts Mobile Engagement](mobile-engagement-concepts.md) courants pour la plateforme web.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-110">The following parts refine common [Mobile Engagement concepts](mobile-engagement-concepts.md) for the web platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="c1e8b-111">`Session` et `Activity`</span><span class="sxs-lookup"><span data-stu-id="c1e8b-111">`Session` and `Activity`</span></span>
<span data-ttu-id="c1e8b-112">Si l’utilisateur reste inactif pendant plus de quelques secondes entre deux activités, sa séquence d’activités est fractionnée en deux sessions distinctes.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-112">If the user stays idle for more than a few seconds between two activities, the user's sequence of activities is split into two distinct sessions.</span></span> <span data-ttu-id="c1e8b-113">Ces quelques secondes constituent le délai d’expiration de session.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-113">These few seconds are called the session timeout.</span></span>

<span data-ttu-id="c1e8b-114">Si votre application web ne déclare pas la fin des activités de l’utilisateur par elle-même (en appelant la fonction `engagement.agent.endActivity` ), le serveur Mobile Engagement termine automatiquement la session de l’utilisateur dans les trois minutes qui suivent la fermeture de la page d’application.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-114">If your web application doesn't declare the end of user activities by itself (by calling the `engagement.agent.endActivity` function), the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span> <span data-ttu-id="c1e8b-115">C’est ce que l’on appelle le délai d’expiration de session du serveur.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-115">This is called the server session timeout.</span></span>

### `Crash`
<span data-ttu-id="c1e8b-116">Les rapports automatisés d’exceptions JavaScript non interceptées ne sont pas créés par défaut.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-116">Automated reports of uncaught JavaScript exceptions are not created by default.</span></span> <span data-ttu-id="c1e8b-117">Toutefois, vous pouvez signaler les incidents manuellement à l’aide de la fonction `sendCrash` (voir la section sur les rapports d’incidents).</span><span class="sxs-lookup"><span data-stu-id="c1e8b-117">However, you can report crashes manually by using the `sendCrash` function (see the section on reporting crashes).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="c1e8b-118">Rapports d’activités</span><span class="sxs-lookup"><span data-stu-id="c1e8b-118">Reporting activities</span></span>
<span data-ttu-id="c1e8b-119">Les rapports d’activités de l’utilisateur incluent le moment où l’utilisateur démarre une nouvelle activité et où l’utilisateur met fin à l’activité en cours.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-119">Reporting on user activity includes when a user starts a new activity, and when the user ends the current activity.</span></span>

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="c1e8b-120">L’utilisateur démarre une nouvelle activité</span><span class="sxs-lookup"><span data-stu-id="c1e8b-120">User starts a new activity</span></span>
    engagement.agent.startActivity("MyUserActivity");

<span data-ttu-id="c1e8b-121">Vous devez appeler `startActivity()` chaque fois que l’activité utilisateur change.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-121">You need to call `startActivity()` each time user activity changes.</span></span> <span data-ttu-id="c1e8b-122">Le premier appel à cette fonction démarre une nouvelle session utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-122">The first call to this function starts a new user session.</span></span>

### <a name="user-ends-the-current-activity"></a><span data-ttu-id="c1e8b-123">L’utilisateur met fin à l’activité en cours</span><span class="sxs-lookup"><span data-stu-id="c1e8b-123">User ends the current activity</span></span>
    engagement.agent.endActivity();

<span data-ttu-id="c1e8b-124">Vous devez appeler `endActivity()` au moins une fois lorsque l’utilisateur termine sa dernière activité.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-124">You need to call `endActivity()` at least once when the user finishes their last activity.</span></span> <span data-ttu-id="c1e8b-125">Le Kit de développement logiciel (SDK) web Mobile Engagement est ainsi informé que l’utilisateur est inactif et que la session utilisateur doit être fermée après le délai d’expiration de session.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-125">This informs the Mobile Engagement Web SDK that the user is currently idle, and that the user session needs to be closed after the session timeout expires.</span></span> <span data-ttu-id="c1e8b-126">Si vous appelez `startActivity()` avant la fin du délai d’expiration de session, la session reprend simplement.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-126">If you call `startActivity()` before the session timeout expires, the session is simply resumed.</span></span>

<span data-ttu-id="c1e8b-127">Étant donné qu’il n’existe aucun appel fiable lors de la fermeture de la fenêtre du navigateur, il est souvent difficile, voire impossible, d’intercepter la fin des activités de l’utilisateur dans un environnement web.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-127">Because there's no reliable call for when the navigator window is closed, it's often difficult or impossible to catch the end of user activities inside a web environment.</span></span> <span data-ttu-id="c1e8b-128">C’est pourquoi le serveur Mobile Engagement termine automatiquement la session de l’utilisateur dans un délai de trois minutes après la fermeture de la page de l’application.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-128">That's why the Mobile Engagement server automatically expires the user session within three minutes after the application page is closed.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="c1e8b-129">Rapports d’événements</span><span class="sxs-lookup"><span data-stu-id="c1e8b-129">Reporting events</span></span>
<span data-ttu-id="c1e8b-130">Les rapports d’événements couvrent les événements de session et les événements autonomes.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-130">Reporting on events covers session events and standalone events.</span></span>

### <a name="session-events"></a><span data-ttu-id="c1e8b-131">Événements de session</span><span class="sxs-lookup"><span data-stu-id="c1e8b-131">Session events</span></span>
<span data-ttu-id="c1e8b-132">Les événements de session servent généralement à signaler les actions effectuées par un utilisateur lors la session de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-132">Session events usually are used to report the actions performed by a user during the user's session.</span></span>

<span data-ttu-id="c1e8b-133">**Exemple sans données supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="c1e8b-133">**Example without extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

<span data-ttu-id="c1e8b-134">**Exemple avec des données supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="c1e8b-134">**Example with extra data:**</span></span>

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a><span data-ttu-id="c1e8b-135">Événements autonomes</span><span class="sxs-lookup"><span data-stu-id="c1e8b-135">Standalone events</span></span>
<span data-ttu-id="c1e8b-136">Contrairement aux événements de session, les événements autonomes peuvent se produire en dehors du contexte d’une session.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-136">Unlike session events, standalone events can occur outside the context of a session.</span></span>

<span data-ttu-id="c1e8b-137">Pour cela, utilisez ``engagement.agent.sendEvent`` au lieu de ``engagement.agent.sendSessionEvent``.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-137">For that, use ``engagement.agent.sendEvent`` instead of ``engagement.agent.sendSessionEvent``.</span></span>

## <a name="reporting-errors"></a><span data-ttu-id="c1e8b-138">Rapports d’erreurs</span><span class="sxs-lookup"><span data-stu-id="c1e8b-138">Reporting errors</span></span>
<span data-ttu-id="c1e8b-139">Les rapports d’erreurs couvrent les erreurs de session et les erreurs autonomes.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-139">Reporting on errors covers session errors and standalone errors.</span></span>

### <a name="session-errors"></a><span data-ttu-id="c1e8b-140">Erreurs de session</span><span class="sxs-lookup"><span data-stu-id="c1e8b-140">Session errors</span></span>
<span data-ttu-id="c1e8b-141">Les erreurs de session servent généralement à signaler les erreurs qui ont un impact sur l’utilisateur pendant la session de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-141">Session errors usually are used to report the errors that have an impact on the user during the user's session.</span></span>

<span data-ttu-id="c1e8b-142">**Exemple sans données supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="c1e8b-142">**Example without extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

<span data-ttu-id="c1e8b-143">**Exemple avec des données supplémentaires :**</span><span class="sxs-lookup"><span data-stu-id="c1e8b-143">**Example with extra data:**</span></span>

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a><span data-ttu-id="c1e8b-144">Erreurs autonomes</span><span class="sxs-lookup"><span data-stu-id="c1e8b-144">Standalone errors</span></span>
<span data-ttu-id="c1e8b-145">Contrairement aux erreurs de session, les erreurs autonomes peuvent se produire en dehors du contexte d’une session.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-145">Unlike session errors, standalone errors can occur outside the context of a session.</span></span>

<span data-ttu-id="c1e8b-146">Pour cela, utilisez `engagement.agent.sendError` au lieu de `engagement.agent.sendSessionError`.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-146">For that, use `engagement.agent.sendError` instead of `engagement.agent.sendSessionError`.</span></span>

## <a name="reporting-jobs"></a><span data-ttu-id="c1e8b-147">Rapports de travaux</span><span class="sxs-lookup"><span data-stu-id="c1e8b-147">Reporting jobs</span></span>
<span data-ttu-id="c1e8b-148">Les rapports de travaux couvrent les erreurs et les événements qui se produisent lors d’un travail, ainsi que les rapports d’incidents.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-148">Reporting on jobs covers reporting errors and events that occur during a job, and reporting crashes.</span></span>

<span data-ttu-id="c1e8b-149">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="c1e8b-149">**Example:**</span></span>

<span data-ttu-id="c1e8b-150">Pour surveiller une requête AJAX, vous utilisez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c1e8b-150">If you want to monitor an AJAX request, you'd use the following:</span></span>

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

### <a name="reporting-errors-during-a-job"></a><span data-ttu-id="c1e8b-151">Signaler les erreurs lors d’un travail</span><span class="sxs-lookup"><span data-stu-id="c1e8b-151">Reporting errors during a job</span></span>
<span data-ttu-id="c1e8b-152">Les erreurs peuvent être associées à un travail en cours d’exécution plutôt qu’à la session utilisateur en cours.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-152">Errors can be related to a running job instead of to the current user session.</span></span>

<span data-ttu-id="c1e8b-153">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="c1e8b-153">**Example:**</span></span>

<span data-ttu-id="c1e8b-154">Pour signaler une erreur si une requête AJAX échoue :</span><span class="sxs-lookup"><span data-stu-id="c1e8b-154">If you want to report an error if an AJAX request fails:</span></span>

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

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="c1e8b-155">Rapports d’événements pendant un travail</span><span class="sxs-lookup"><span data-stu-id="c1e8b-155">Reporting events during a job</span></span>
<span data-ttu-id="c1e8b-156">Les événements peuvent être associés à un travail en cours d’exécution plutôt qu’à la session utilisateur en cours grâce à la fonction `engagement.agent.sendJobEvent` .</span><span class="sxs-lookup"><span data-stu-id="c1e8b-156">Events can be related to a running job instead of to the current user session, thanks to the `engagement.agent.sendJobEvent` function.</span></span>

<span data-ttu-id="c1e8b-157">Cette fonction fonctionne exactement comme `engagement.agent.sendJobError`.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-157">This function works exactly like `engagement.agent.sendJobError`.</span></span>

### <a name="reporting-crashes"></a><span data-ttu-id="c1e8b-158">Rapports d’incidents</span><span class="sxs-lookup"><span data-stu-id="c1e8b-158">Reporting crashes</span></span>
<span data-ttu-id="c1e8b-159">Utilisez la fonction `sendCrash` pour signaler des incidents manuellement.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-159">Use the `sendCrash` function to report crashes manually.</span></span>

<span data-ttu-id="c1e8b-160">L’argument `crashid` est une chaîne qui identifie le type d’incident.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-160">The `crashid` argument is a string that identifies the type of crash.</span></span>
<span data-ttu-id="c1e8b-161">L’argument `crash` correspond généralement à l’arborescence des appels de procédure de l’incident sous forme de chaîne.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-161">The `crash` argument usually is the stack trace of the crash as a string.</span></span>

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a><span data-ttu-id="c1e8b-162">Paramètres supplémentaires</span><span class="sxs-lookup"><span data-stu-id="c1e8b-162">Extra parameters</span></span>
<span data-ttu-id="c1e8b-163">Vous pouvez joindre des données arbitraires à un événement, une erreur, une activité ou un travail.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-163">You can attach arbitrary data to an event, error, activity, or job.</span></span>

<span data-ttu-id="c1e8b-164">Les données peuvent être n’importe quel objet JSON (mais pas un tableau ou un type primitif).</span><span class="sxs-lookup"><span data-stu-id="c1e8b-164">The data can be any JSON object (but not an array or primitive type).</span></span>

<span data-ttu-id="c1e8b-165">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="c1e8b-165">**Example:**</span></span>

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="c1e8b-166">Limites</span><span class="sxs-lookup"><span data-stu-id="c1e8b-166">Limits</span></span>
<span data-ttu-id="c1e8b-167">Les limites qui s’appliquent aux paramètres supplémentaires se situent dans les zones des expressions régulières pour les clés, les types de valeur et la taille.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-167">Limits that apply to extra parameters are in the areas of regular expressions for keys, value types, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="c1e8b-168">de clés symétriques</span><span class="sxs-lookup"><span data-stu-id="c1e8b-168">Keys</span></span>
<span data-ttu-id="c1e8b-169">Chaque clé de l'objet doit correspondre à l'expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="c1e8b-169">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="c1e8b-170">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="c1e8b-170">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="values"></a><span data-ttu-id="c1e8b-171">Valeurs</span><span class="sxs-lookup"><span data-stu-id="c1e8b-171">Values</span></span>
<span data-ttu-id="c1e8b-172">Les valeurs sont limitées aux types chaîne, nombre et Booléen.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-172">Values are limited to string, number, and Boolean types.</span></span>

#### <a name="size"></a><span data-ttu-id="c1e8b-173">Taille</span><span class="sxs-lookup"><span data-stu-id="c1e8b-173">Size</span></span>
<span data-ttu-id="c1e8b-174">Les paramètres supplémentaires sont limités à 1 024 caractères par appel (une fois que le Kit de développement logiciel (SDK) Mobile Engagement Web l’encode dans JSON).</span><span class="sxs-lookup"><span data-stu-id="c1e8b-174">Extras are limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

## <a name="reporting-application-information"></a><span data-ttu-id="c1e8b-175">Rapports d’informations sur l’application</span><span class="sxs-lookup"><span data-stu-id="c1e8b-175">Reporting application information</span></span>
<span data-ttu-id="c1e8b-176">Vous pouvez signaler manuellement les informations de suivi (ou toutes autres informations spécifiques aux applications) à l’aide de la fonction `sendAppInfo()` .</span><span class="sxs-lookup"><span data-stu-id="c1e8b-176">You can manually report tracking information (or any other application-specific information) by using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="c1e8b-177">Notez que ces informations peuvent être envoyées de façon incrémentielle.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-177">Note that this information can be sent incrementally.</span></span> <span data-ttu-id="c1e8b-178">Seule la dernière valeur d’une clé spécifique est conservée pour un appareil donné.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-178">Only the latest value for a specific key will be kept for a specific device.</span></span>

<span data-ttu-id="c1e8b-179">Comme pour les paramètres supplémentaires d’événement, vous pouvez utiliser n’importe quel objet JSON pour extraire des informations sur l’application.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-179">Like event extras, you can use any JSON object to abstract application information.</span></span> <span data-ttu-id="c1e8b-180">Notez que les tableaux ou les sous-objets sont traités comme des chaînes plates (à l’aide de la sérialisation JSON).</span><span class="sxs-lookup"><span data-stu-id="c1e8b-180">Note that arrays or sub-objects are treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="c1e8b-181">**Exemple :**</span><span class="sxs-lookup"><span data-stu-id="c1e8b-181">**Example:**</span></span>

<span data-ttu-id="c1e8b-182">Voici un exemple de code pour l’envoi du sexe et de la date de naissance de l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="c1e8b-182">Here is a code sample for sending the user's gender and birth date:</span></span>

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a><span data-ttu-id="c1e8b-183">Limites</span><span class="sxs-lookup"><span data-stu-id="c1e8b-183">Limits</span></span>
<span data-ttu-id="c1e8b-184">Les limites qui s’appliquent aux informations sur l’application se situent dans les zones des expressions régulières pour les clés et la taille.</span><span class="sxs-lookup"><span data-stu-id="c1e8b-184">Limits that apply to application information are in the areas of regular expressions for keys, and size.</span></span>

#### <a name="keys"></a><span data-ttu-id="c1e8b-185">de clés symétriques</span><span class="sxs-lookup"><span data-stu-id="c1e8b-185">Keys</span></span>
<span data-ttu-id="c1e8b-186">Chaque clé de l'objet doit correspondre à l'expression régulière suivante :</span><span class="sxs-lookup"><span data-stu-id="c1e8b-186">Each key in the object must match the following regular expression:</span></span>

    ^[a-zA-Z][a-zA-Z_0-9]*

<span data-ttu-id="c1e8b-187">Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).</span><span class="sxs-lookup"><span data-stu-id="c1e8b-187">This means that keys must start with at least one letter, followed by letters, digits, or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="c1e8b-188">Taille</span><span class="sxs-lookup"><span data-stu-id="c1e8b-188">Size</span></span>
<span data-ttu-id="c1e8b-189">Les informations sur l’application sont limitées à 1 024 caractères par appel (une fois que le Kit de développement logiciel (SDK) Mobile Engagement Web l’encode dans JSON).</span><span class="sxs-lookup"><span data-stu-id="c1e8b-189">Application information is limited to 1,024 characters per call (after the Mobile Engagement Web SDK encodes it in JSON).</span></span>

<span data-ttu-id="c1e8b-190">Dans l’exemple précédent, le JSON envoyé au serveur fait 44 caractères :</span><span class="sxs-lookup"><span data-stu-id="c1e8b-190">In the preceding example, the JSON sent to the server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
