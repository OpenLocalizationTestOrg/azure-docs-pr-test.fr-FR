---
title: "aaaAzure intégration du Kit de développement Web Mobile Engagement | Documents Microsoft"
description: "Hello les dernières mises à jour et les procédures à suivre pour hello Kit de développement Web Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: b5daa2a2-942b-489d-aa1d-568c3b25e56f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 02/29/2016
ms.author: piyushjo
ms.openlocfilehash: 99613b68b615bec4ddcfcc8e4e0133ce9d887bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="361cc-103">Intégration d’Azure Mobile Engagement dans une application web</span><span class="sxs-lookup"><span data-stu-id="361cc-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="361cc-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="361cc-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="361cc-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="361cc-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="361cc-106">iOS</span><span class="sxs-lookup"><span data-stu-id="361cc-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="361cc-107">Android</span><span class="sxs-lookup"><span data-stu-id="361cc-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="361cc-108">les procédures de Hello dans cet article décrivent analytique de hello la plus simple façon tooactivate hello et de surveillance dans Azure Mobile Engagement dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="361cc-108">hello procedures in this article describe hello simplest way tooactivate hello analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="361cc-109">Suivez hello étapes tooactivate hello journal des rapports qui sont nécessaire toocompute toutes les statistiques sur les utilisateurs, les sessions, les activités, blocages et technicals.</span><span class="sxs-lookup"><span data-stu-id="361cc-109">Follow hello steps tooactivate hello log reports that are needed toocompute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="361cc-110">Pour les statistiques dépend de l’application, telles que des événements, les erreurs et les tâches, vous devez activer manuellement les rapports du journal à l’aide de hello Azure Mobile Engagement API.</span><span class="sxs-lookup"><span data-stu-id="361cc-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using hello Azure Mobile Engagement API.</span></span> <span data-ttu-id="361cc-111">Pour plus d’informations, Découvrez [comment toouse hello avancé Mobile Engagement marquage API dans une application web](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="361cc-111">For more information, learn [how toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="361cc-112">Introduction</span><span class="sxs-lookup"><span data-stu-id="361cc-112">Introduction</span></span>
<span data-ttu-id="361cc-113">[Télécharger hello Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span><span class="sxs-lookup"><span data-stu-id="361cc-113">[Download hello Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="361cc-114">Hello Web d’Engagement Mobile Kit de développement logiciel est fourni en tant qu’un seul fichier JavaScript, engagement.js azure, ce qui vous avez tooinclude dans chaque page de votre application ou un site web.</span><span class="sxs-lookup"><span data-stu-id="361cc-114">hello Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have tooinclude in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="361cc-115">Avant d’exécuter ce script, vous devez exécuter un script ou code extrait de code que vous écrivez tooconfigure Mobile Engagement pour votre application.</span><span class="sxs-lookup"><span data-stu-id="361cc-115">Before you run this script, you must run a script or code snippet that you write tooconfigure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="361cc-116">Compatibilité des navigateurs</span><span class="sxs-lookup"><span data-stu-id="361cc-116">Browser compatibility</span></span>
<span data-ttu-id="361cc-117">Hello Kit de développement Web Mobile Engagement utilise JSON natif codage et décodage de plus les requêtes AJAX toocross-domaine (partie de confiance sur la spécification du W3C CORS hello).</span><span class="sxs-lookup"><span data-stu-id="361cc-117">hello Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition toocross-domain AJAX requests (relying on hello W3C CORS specification).</span></span> <span data-ttu-id="361cc-118">Il est compatible avec hello suivant navigateurs :</span><span class="sxs-lookup"><span data-stu-id="361cc-118">It's compatible with hello following browsers:</span></span>

* <span data-ttu-id="361cc-119">Microsoft Edge 12+</span><span class="sxs-lookup"><span data-stu-id="361cc-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="361cc-120">Internet Explorer 10+</span><span class="sxs-lookup"><span data-stu-id="361cc-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="361cc-121">Firefox 3.5+</span><span class="sxs-lookup"><span data-stu-id="361cc-121">Firefox 3.5+</span></span>
* <span data-ttu-id="361cc-122">Chrome 4+</span><span class="sxs-lookup"><span data-stu-id="361cc-122">Chrome 4+</span></span>
* <span data-ttu-id="361cc-123">Safari 6+</span><span class="sxs-lookup"><span data-stu-id="361cc-123">Safari 6+</span></span>
* <span data-ttu-id="361cc-124">Opera 12+</span><span class="sxs-lookup"><span data-stu-id="361cc-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="361cc-125">Configuration de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="361cc-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="361cc-126">Écrire un script qui crée un global `azureEngagement` objet JavaScript, comme dans l’exemple suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="361cc-126">Write a script that creates a global `azureEngagement` JavaScript object, as in hello following example.</span></span> <span data-ttu-id="361cc-127">Étant donné que votre site peut comporter plusieurs pages, cet exemple suppose que ce script est inclus dans chaque page.</span><span class="sxs-lookup"><span data-stu-id="361cc-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="361cc-128">Dans cet exemple, l’objet JavaScript de hello est nommé `azure-engagement-conf.js`.</span><span class="sxs-lookup"><span data-stu-id="361cc-128">In this example, hello JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="361cc-129">Hello `connectionString` valeur de votre application s’affiche dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="361cc-129">hello `connectionString` value for your application is displayed in hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="361cc-130">Les valeurs `appVersionName` et `appVersionCode` sont facultatives.</span><span class="sxs-lookup"><span data-stu-id="361cc-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="361cc-131">Toutefois, nous vous recommandons de les configurer pour que les analyses puissent traiter les informations de version.</span><span class="sxs-lookup"><span data-stu-id="361cc-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="361cc-132">Inclure des scripts Mobile Engagement dans vos pages</span><span class="sxs-lookup"><span data-stu-id="361cc-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="361cc-133">Ajouter des pages de tooyour de scripts de Mobile Engagement dans un des hello suivant façons :</span><span class="sxs-lookup"><span data-stu-id="361cc-133">Add Mobile Engagement scripts tooyour pages in one of hello following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="361cc-134">Ou cela :</span><span class="sxs-lookup"><span data-stu-id="361cc-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="361cc-135">Alias</span><span class="sxs-lookup"><span data-stu-id="361cc-135">Alias</span></span>
<span data-ttu-id="361cc-136">Une fois hello script du Kit de développement Web Mobile Engagement est chargé, il crée hello **engagement** alias tooaccess hello API du Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="361cc-136">After hello Mobile Engagement Web SDK script is loaded, it creates hello **engagement** alias tooaccess hello SDK APIs.</span></span> <span data-ttu-id="361cc-137">Vous ne pouvez pas utiliser cette configuration de kit de développement logiciel alias toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="361cc-137">You cannot use this alias toodefine hello SDK configuration.</span></span> <span data-ttu-id="361cc-138">Cet alias est utilisé comme référence dans cette documentation.</span><span class="sxs-lookup"><span data-stu-id="361cc-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="361cc-139">Notez que si l’alias par défaut de hello est en conflit avec une autre variable globale à partir de votre page, vous pouvez redéfinir il dans la configuration de hello comme suit avant de les charger hello Kit de développement Web Mobile Engagement :</span><span class="sxs-lookup"><span data-stu-id="361cc-139">Note that if hello default alias conflicts with another global variable from your page, you can redefine it in hello configuration as follows before you load hello Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="361cc-140">Génération de rapports de base</span><span class="sxs-lookup"><span data-stu-id="361cc-140">Basic reporting</span></span>
<span data-ttu-id="361cc-141">La section Génération de rapports de base de Mobile Engagement présente les statistiques au niveau de la session, notamment les statistiques sur les utilisateurs, les sessions, les activités et les incidents.</span><span class="sxs-lookup"><span data-stu-id="361cc-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="361cc-142">Suivi de session</span><span class="sxs-lookup"><span data-stu-id="361cc-142">Session tracking</span></span>
<span data-ttu-id="361cc-143">Une session Mobile Engagement est divisée en une séquence d’activités, chacune identifiée par un nom.</span><span class="sxs-lookup"><span data-stu-id="361cc-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="361cc-144">Dans un site web classique, nous vous recommandons de déclarer une autre activité sur chaque page de votre site.</span><span class="sxs-lookup"><span data-stu-id="361cc-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="361cc-145">Pour une site Web ou une application web dans le hello page actuelle change jamais, vous pourriez tootrack des activités de hello sur une plus petite échelle, comme dans la page de hello.</span><span class="sxs-lookup"><span data-stu-id="361cc-145">For a website or web application in which hello current page never changes, you might want tootrack hello activities on a smaller scale, such as within hello page.</span></span>

<span data-ttu-id="361cc-146">Soit, toostart ou modification hello activité utilisateur en cours, appel hello `engagement.agent.startActivity` (fonction).</span><span class="sxs-lookup"><span data-stu-id="361cc-146">Either way, toostart or change hello current user activity, call hello `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="361cc-147">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="361cc-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="361cc-148">serveur de Mobile Engagement Hello termine automatiquement une session ouverte dans les trois minutes après la fermeture de la page de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="361cc-148">hello Mobile Engagement server automatically ends an open session within three minutes after hello application page is closed.</span></span>

<span data-ttu-id="361cc-149">Ou vous pouvez terminer une session manuellement en appelant `engagement.agent.endActivity`.</span><span class="sxs-lookup"><span data-stu-id="361cc-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="361cc-150">Cela définit too'Idle activité utilisateur en cours de hello. »</span><span class="sxs-lookup"><span data-stu-id="361cc-150">This sets hello current user activity too'Idle.'</span></span>  <span data-ttu-id="361cc-151">Hello prendra fin 10 secondes plus tard, sauf si un nouvel appel`engagement.agent.startActivity` reprend la session de hello.</span><span class="sxs-lookup"><span data-stu-id="361cc-151">hello session will end 10 seconds later unless a new call too`engagement.agent.startActivity` resumes hello session.</span></span>

<span data-ttu-id="361cc-152">Vous pouvez configurer délai de 10 secondes hello dans l’objet d’engagement global hello, comme suit :</span><span class="sxs-lookup"><span data-stu-id="361cc-152">You can configure hello 10-second delay in hello global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end hello session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="361cc-153">Vous ne pouvez pas utiliser `engagement.agent.endActivity` Bonjour `onunload` rappel étant donné que vous ne pouvez pas les appels AJAX à ce stade.</span><span class="sxs-lookup"><span data-stu-id="361cc-153">You cannot use `engagement.agent.endActivity` in hello `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="361cc-154">Génération de rapports avancés</span><span class="sxs-lookup"><span data-stu-id="361cc-154">Advanced reporting</span></span>
<span data-ttu-id="361cc-155">Si vous le souhaitez, si vous souhaitez que les travaux, les erreurs et les événements d’application tooreport, vous devez toouse hello API d’Engagement Mobile.</span><span class="sxs-lookup"><span data-stu-id="361cc-155">Optionally, if you want tooreport application-specific events, errors, and jobs, you need toouse hello Mobile Engagement API.</span></span> <span data-ttu-id="361cc-156">Vous accédez hello API d’Engagement Mobile via hello `engagement.agent` objet.</span><span class="sxs-lookup"><span data-stu-id="361cc-156">You access hello Mobile Engagement API through hello `engagement.agent` object.</span></span>

<span data-ttu-id="361cc-157">Vous pouvez accéder à tous les hello avancées dans Mobile Engagement Bonjour API d’Engagement Mobile.</span><span class="sxs-lookup"><span data-stu-id="361cc-157">You can access all of hello advanced capabilities in Mobile Engagement in hello Mobile Engagement API.</span></span> <span data-ttu-id="361cc-158">Hello API est détaillée dans l’article de hello [comment toouse hello avancé Mobile Engagement marquage API dans une application web](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="361cc-158">hello API is detailed in hello article [How toouse hello advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-hello-urls-used-for-ajax-calls"></a><span data-ttu-id="361cc-159">Personnaliser des URL hello utilisés pour les appels AJAX</span><span class="sxs-lookup"><span data-stu-id="361cc-159">Customize hello URLs used for AJAX calls</span></span>
<span data-ttu-id="361cc-160">Vous pouvez personnaliser les URL que hello qu'utilise du Kit de développement Web Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="361cc-160">You can customize URLs that hello Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="361cc-161">Par exemple, les URL de connexion de hello tooredefine (hello SDK point de terminaison pour la journalisation), vous pouvez remplacer la configuration de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="361cc-161">For example, tooredefine hello log URL (hello SDK endpoint for logging), you can override hello configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="361cc-162">Si votre URL renvoient une chaîne qui commence par `/`, `//`, `http://`, ou `https://`, schéma par défaut de hello n’est pas utilisé.</span><span class="sxs-lookup"><span data-stu-id="361cc-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, hello default scheme is not used.</span></span> <span data-ttu-id="361cc-163">Par défaut, hello `https://` schéma est utilisé pour les URL.</span><span class="sxs-lookup"><span data-stu-id="361cc-163">By default, hello `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="361cc-164">Si vous souhaitez que le schéma par défaut de hello toocustomize, remplacer la configuration de hello, comme suit :</span><span class="sxs-lookup"><span data-stu-id="361cc-164">If you want toocustomize hello default scheme, override hello configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
