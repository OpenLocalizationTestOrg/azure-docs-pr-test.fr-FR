---
title: "Intégration du SDK web Azure Mobile Engagement | Microsoft Docs"
description: "Dernières mises à jour et procédures du Kit de développement logiciel (SDK) web Azure Mobile Engagement"
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
ms.openlocfilehash: 7d8eaa180e277741a583522ee62d68f5247b92bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-mobile-engagement-in-a-web-application"></a><span data-ttu-id="01978-103">Intégration d’Azure Mobile Engagement dans une application web</span><span class="sxs-lookup"><span data-stu-id="01978-103">Integrate Azure Mobile Engagement in a web application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="01978-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="01978-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="01978-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="01978-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="01978-106">iOS</span><span class="sxs-lookup"><span data-stu-id="01978-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="01978-107">Android</span><span class="sxs-lookup"><span data-stu-id="01978-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
> 
> 

<span data-ttu-id="01978-108">Les procédures de cet article décrivent la méthode la plus simple pour activer les fonctions d’analyse et de surveillance d’Azure Mobile Engagement dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="01978-108">The procedures in this article describe the simplest way to activate the analytics and monitoring functions in Azure Mobile Engagement in your web application.</span></span>

<span data-ttu-id="01978-109">Suivez ces étapes afin d’activer la génération des journaux nécessaires pour calculer toutes les statistiques concernant les utilisateurs, les sessions, les activités, les incidents et les informations techniques.</span><span class="sxs-lookup"><span data-stu-id="01978-109">Follow the steps to activate the log reports that are needed to compute all statistics about users, sessions, activities, crashes, and technicals.</span></span> <span data-ttu-id="01978-110">Pour les statistiques liées à l’application, telles que les événements, erreurs et tâches, vous devez activer manuellement les journaux à l’aide de l’API Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="01978-110">For application-dependent statistics, such as events, errors, and jobs, you must activate log reports manually by using the Azure Mobile Engagement API.</span></span> <span data-ttu-id="01978-111">Pour plus d’informations, consultez [Utilisation de l’API avancée de balisage de Mobile Engagement dans votre application web](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="01978-111">For more information, learn [how to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="01978-112">Introduction</span><span class="sxs-lookup"><span data-stu-id="01978-112">Introduction</span></span>
<span data-ttu-id="01978-113">[Téléchargez le Kit de développement logiciel (SDK) web Azure Mobile Engagement](http://aka.ms/P7b453).</span><span class="sxs-lookup"><span data-stu-id="01978-113">[Download the Azure Mobile Engagement Web SDK](http://aka.ms/P7b453).</span></span>
<span data-ttu-id="01978-114">Le Kit de développement logiciel (SDK) web Mobile Engagement est fourni sous la forme d’un seul fichier JavaScript, azure-engagement.js, à inclure dans chaque page de votre site ou de votre application web.</span><span class="sxs-lookup"><span data-stu-id="01978-114">The Mobile Engagement Web SDK is shipped as a single JavaScript file, azure-engagement.js, which you have to include in each page of your site or web application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="01978-115">Avant d’exécuter ce script, vous devez exécuter un script ou un extrait de code écrit par vous pour configurer Mobile Engagement pour votre application.</span><span class="sxs-lookup"><span data-stu-id="01978-115">Before you run this script, you must run a script or code snippet that you write to configure Mobile Engagement for your application.</span></span>
> 
> 

## <a name="browser-compatibility"></a><span data-ttu-id="01978-116">Compatibilité des navigateurs</span><span class="sxs-lookup"><span data-stu-id="01978-116">Browser compatibility</span></span>
<span data-ttu-id="01978-117">Le Kit de développement logiciel (SDK) web Mobile Engagement utilise un codage/décodage JSON natif en complément de requêtes AJAX interdomaines (reposant sur la spécification W3C CORS).</span><span class="sxs-lookup"><span data-stu-id="01978-117">The Mobile Engagement Web SDK uses native JSON encoding and decoding, in addition to cross-domain AJAX requests (relying on the W3C CORS specification).</span></span> <span data-ttu-id="01978-118">Il est compatible avec les navigateurs suivants :</span><span class="sxs-lookup"><span data-stu-id="01978-118">It's compatible with the following browsers:</span></span>

* <span data-ttu-id="01978-119">Microsoft Edge 12+</span><span class="sxs-lookup"><span data-stu-id="01978-119">Microsoft Edge 12+</span></span>
* <span data-ttu-id="01978-120">Internet Explorer 10+</span><span class="sxs-lookup"><span data-stu-id="01978-120">Internet Explorer 10+</span></span>
* <span data-ttu-id="01978-121">Firefox 3.5+</span><span class="sxs-lookup"><span data-stu-id="01978-121">Firefox 3.5+</span></span>
* <span data-ttu-id="01978-122">Chrome 4+</span><span class="sxs-lookup"><span data-stu-id="01978-122">Chrome 4+</span></span>
* <span data-ttu-id="01978-123">Safari 6+</span><span class="sxs-lookup"><span data-stu-id="01978-123">Safari 6+</span></span>
* <span data-ttu-id="01978-124">Opera 12+</span><span class="sxs-lookup"><span data-stu-id="01978-124">Opera 12+</span></span>

## <a name="configure-mobile-engagement"></a><span data-ttu-id="01978-125">Configuration de Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="01978-125">Configure Mobile Engagement</span></span>
<span data-ttu-id="01978-126">Écrivez un script qui crée un objet JavaScript `azureEngagement` global comme dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="01978-126">Write a script that creates a global `azureEngagement` JavaScript object, as in the following example.</span></span> <span data-ttu-id="01978-127">Étant donné que votre site peut comporter plusieurs pages, cet exemple suppose que ce script est inclus dans chaque page.</span><span class="sxs-lookup"><span data-stu-id="01978-127">Because your site might have multiples pages, this example assumes that this script is included in every page.</span></span> <span data-ttu-id="01978-128">Dans cet exemple, l’objet JavaScript est nommé `azure-engagement-conf.js`.</span><span class="sxs-lookup"><span data-stu-id="01978-128">In this example, the JavaScript object is named `azure-engagement-conf.js`.</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
    };

<span data-ttu-id="01978-129">La valeur `connectionString` de votre application s’affiche sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="01978-129">The `connectionString` value for your application is displayed in the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="01978-130">Les valeurs `appVersionName` et `appVersionCode` sont facultatives.</span><span class="sxs-lookup"><span data-stu-id="01978-130">`appVersionName` and `appVersionCode` are optional.</span></span> <span data-ttu-id="01978-131">Toutefois, nous vous recommandons de les configurer pour que les analyses puissent traiter les informations de version.</span><span class="sxs-lookup"><span data-stu-id="01978-131">However, we recommend that you configure them so that analytics can process version information.</span></span>
> 
> 

## <a name="include-mobile-engagement-scripts-in-your-pages"></a><span data-ttu-id="01978-132">Inclure des scripts Mobile Engagement dans vos pages</span><span class="sxs-lookup"><span data-stu-id="01978-132">Include Mobile Engagement scripts in your pages</span></span>
<span data-ttu-id="01978-133">Ajoutez des scripts Mobile Engagement à vos pages de l’une des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="01978-133">Add Mobile Engagement scripts to your pages in one of the following ways:</span></span>

    <head>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </head>

<span data-ttu-id="01978-134">Ou cela :</span><span class="sxs-lookup"><span data-stu-id="01978-134">Or this:</span></span>

    <body>
      ...
      <script type="text/javascript" src="azure-engagement-conf.js"></script>
      <script type="text/javascript" src="azure-engagement.js"></script>
      ...
    </body>

## <a name="alias"></a><span data-ttu-id="01978-135">Alias</span><span class="sxs-lookup"><span data-stu-id="01978-135">Alias</span></span>
<span data-ttu-id="01978-136">Une fois le script du Kit de développement (SDK) web Mobile Engagement chargé, il crée l’alias **engagement** pour accéder aux API du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="01978-136">After the Mobile Engagement Web SDK script is loaded, it creates the **engagement** alias to access the SDK APIs.</span></span> <span data-ttu-id="01978-137">Vous ne pouvez pas utiliser cet alias pour définir la configuration du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="01978-137">You cannot use this alias to define the SDK configuration.</span></span> <span data-ttu-id="01978-138">Cet alias est utilisé comme référence dans cette documentation.</span><span class="sxs-lookup"><span data-stu-id="01978-138">This alias is used as a reference in this documentation.</span></span>

<span data-ttu-id="01978-139">Notez que si l’alias par défaut est en conflit avec une autre variable globale de votre page, vous pouvez le redéfinir comme suit dans la configuration avant de charger le Kit de développement logiciel (SDK) web Mobile Engagement :</span><span class="sxs-lookup"><span data-stu-id="01978-139">Note that if the default alias conflicts with another global variable from your page, you can redefine it in the configuration as follows before you load the Mobile Engagement Web SDK:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      appVersionName: '1.0.0',
      appVersionCode: 1
      alias:'anotherAlias'
    };

## <a name="basic-reporting"></a><span data-ttu-id="01978-140">Génération de rapports de base</span><span class="sxs-lookup"><span data-stu-id="01978-140">Basic reporting</span></span>
<span data-ttu-id="01978-141">La section Génération de rapports de base de Mobile Engagement présente les statistiques au niveau de la session, notamment les statistiques sur les utilisateurs, les sessions, les activités et les incidents.</span><span class="sxs-lookup"><span data-stu-id="01978-141">Basic reporting in Mobile Engagement covers session-level statistics, such as statistics about users, sessions, activities, and crashes.</span></span>

### <a name="session-tracking"></a><span data-ttu-id="01978-142">Suivi de session</span><span class="sxs-lookup"><span data-stu-id="01978-142">Session tracking</span></span>
<span data-ttu-id="01978-143">Une session Mobile Engagement est divisée en une séquence d’activités, chacune identifiée par un nom.</span><span class="sxs-lookup"><span data-stu-id="01978-143">A Mobile Engagement session is divided into a sequence of activities, each identified by a name.</span></span>

<span data-ttu-id="01978-144">Dans un site web classique, nous vous recommandons de déclarer une autre activité sur chaque page de votre site.</span><span class="sxs-lookup"><span data-stu-id="01978-144">In a classic website, we recommend that you declare a different activity on each page of your site.</span></span> <span data-ttu-id="01978-145">Pour une site ou une application web dans lesquels la page actuelle ne change jamais, vous pouvez suivre les activités à une plus petite échelle, par exemple au niveau de la page.</span><span class="sxs-lookup"><span data-stu-id="01978-145">For a website or web application in which the current page never changes, you might want to track the activities on a smaller scale, such as within the page.</span></span>

<span data-ttu-id="01978-146">Dans les deux cas, pour démarrer ou modifier l’activité utilisateur en cours, appelez la fonction `engagement.agent.startActivity` .</span><span class="sxs-lookup"><span data-stu-id="01978-146">Either way, to start or change the current user activity, call the `engagement.agent.startActivity` function.</span></span> <span data-ttu-id="01978-147">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="01978-147">For example:</span></span>

    <body onload="yourOnload()">

    <!-- -->

    yourOnload = function() {
      [...]
      engagement.agent.startActivity('welcome');
    };

<span data-ttu-id="01978-148">Le serveur Mobile Engagement termine automatiquement une session ouverte dans un délai de trois minutes après la fermeture de la page de l’application.</span><span class="sxs-lookup"><span data-stu-id="01978-148">The Mobile Engagement server automatically ends an open session within three minutes after the application page is closed.</span></span>

<span data-ttu-id="01978-149">Ou vous pouvez terminer une session manuellement en appelant `engagement.agent.endActivity`.</span><span class="sxs-lookup"><span data-stu-id="01978-149">Alternatively, you can end a session manually by calling `engagement.agent.endActivity`.</span></span> <span data-ttu-id="01978-150">Cette opération définit l’activité de l’utilisateur en cours sur « Idle » (inactive).</span><span class="sxs-lookup"><span data-stu-id="01978-150">This sets the current user activity to 'Idle.'</span></span>  <span data-ttu-id="01978-151">La session se terminera 10 secondes plus tard, sauf si un nouvel appel à `engagement.agent.startActivity` reprend la session.</span><span class="sxs-lookup"><span data-stu-id="01978-151">The session will end 10 seconds later unless a new call to `engagement.agent.startActivity` resumes the session.</span></span>

<span data-ttu-id="01978-152">Vous pouvez configurer le délai de 10 secondes dans l’objet Engagement global, comme suit :</span><span class="sxs-lookup"><span data-stu-id="01978-152">You can configure the 10-second delay in the global engagement object, as follows:</span></span>

    engagement.sessionTimeout = 2000; // 2 seconds
    // or
    engagement.sessionTimeout = 0; // end the session as soon as endActivity is called

> [!NOTE]
> <span data-ttu-id="01978-153">Vous ne pouvez pas utiliser `engagement.agent.endActivity` dans le rappel `onunload` car vous ne pouvez pas effectuer d’appels AJAX à ce stade.</span><span class="sxs-lookup"><span data-stu-id="01978-153">You cannot use `engagement.agent.endActivity` in the `onunload` callback because you cannot make AJAX calls at this stage.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="01978-154">Génération de rapports avancés</span><span class="sxs-lookup"><span data-stu-id="01978-154">Advanced reporting</span></span>
<span data-ttu-id="01978-155">Éventuellement, si vous voulez signaler des événements, des erreurs et des tâches de l'application spécifiques, vous devez utiliser l'API Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="01978-155">Optionally, if you want to report application-specific events, errors, and jobs, you need to use the Mobile Engagement API.</span></span> <span data-ttu-id="01978-156">Vous accédez à l’API Mobile Engagement sur mobile via l’objet `engagement.agent` .</span><span class="sxs-lookup"><span data-stu-id="01978-156">You access the Mobile Engagement API through the `engagement.agent` object.</span></span>

<span data-ttu-id="01978-157">Vous pouvez accéder à toutes les fonctionnalités avancées d’Engagement Mobile dans l’API Engagement Mobile.</span><span class="sxs-lookup"><span data-stu-id="01978-157">You can access all of the advanced capabilities in Mobile Engagement in the Mobile Engagement API.</span></span> <span data-ttu-id="01978-158">L’API est détaillée dans l’article [Utilisation de l’API avancée de balisage de Mobile Engagement dans votre application web](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="01978-158">The API is detailed in the article [How to use the advanced Mobile Engagement tagging API in a web application](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="customize-the-urls-used-for-ajax-calls"></a><span data-ttu-id="01978-159">Personnaliser les URL utilisées pour les appels AJAX</span><span class="sxs-lookup"><span data-stu-id="01978-159">Customize the URLs used for AJAX calls</span></span>
<span data-ttu-id="01978-160">Vous pouvez personnaliser les URL utilisées par le Kit de développement logiciel (SDK) web Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="01978-160">You can customize URLs that the Mobile Engagement Web SDK uses.</span></span> <span data-ttu-id="01978-161">Par exemple, pour redéfinir l’URL de connexion (le point de terminaison du kit de développement logiciel pour l’enregistrement), vous pouvez remplacer la configuration comme suit :</span><span class="sxs-lookup"><span data-stu-id="01978-161">For example, to redefine the log URL (the SDK endpoint for logging), you can override the configuration like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...        
        getLoggerUrl: function() {
        return 'someProxy/log';
        }
      }
    };

<span data-ttu-id="01978-162">Si vos fonctions URL renvoient une chaîne commençant par `/`, `//`, `http://` ou `https://`, le schéma par défaut n’est pas utilisé.</span><span class="sxs-lookup"><span data-stu-id="01978-162">If your URL functions return a string that begins with `/`, `//`, `http://`, or `https://`, the default scheme is not used.</span></span> <span data-ttu-id="01978-163">Par défaut, le schéma `https://` est utilisé pour ces URL.</span><span class="sxs-lookup"><span data-stu-id="01978-163">By default, the `https://` scheme is used for those URLs.</span></span> <span data-ttu-id="01978-164">Si vous voulez personnaliser le schéma par défaut, remplacez la configuration par ceci :</span><span class="sxs-lookup"><span data-stu-id="01978-164">If you want to customize the default scheme, override the configuration, like this:</span></span>

    window.azureEngagement = {
      ...
      urls: {
        ...         
        scheme: '//'
      }
    };
