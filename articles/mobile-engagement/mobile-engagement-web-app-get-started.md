---
title: "aaaGet main d’Azure Mobile Engagement pour les applications Web | Documents Microsoft"
description: "Découvrez comment toouse Azure Mobile Engagement avec analytique et des notifications push pour les applications Web."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04afe53a-4caf-4c80-bd75-20cc630cd75c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: hero-article
ms.date: 06/01/2016
ms.author: piyushjo
ms.openlocfilehash: a84c96cac13bf3b85e72aef55da5c91693e1766c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a><span data-ttu-id="e16c5-103">Prise en main d’Azure Mobile Engagement pour les applications web</span><span class="sxs-lookup"><span data-stu-id="e16c5-103">Get started with Azure Mobile Engagement for Web Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="e16c5-104">Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application Web.</span><span class="sxs-lookup"><span data-stu-id="e16c5-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your Web App usage.</span></span>

> [!NOTE]
> <span data-ttu-id="e16c5-105">Hello Azure Mobile Engagement service mars 2018 est retirée et est actuellement que les clients tooexisting disponibles.</span><span class="sxs-lookup"><span data-stu-id="e16c5-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="e16c5-106">Pour plus d’informations, consultez [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="e16c5-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="e16c5-107">Ce didacticiel requiert hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="e16c5-107">This tutorial requires hello following:</span></span>

* <span data-ttu-id="e16c5-108">Visual Studio 2015 ou tout autre éditeur de votre choix</span><span class="sxs-lookup"><span data-stu-id="e16c5-108">Visual Studio 2015 or any other editor of your choice</span></span>
* [<span data-ttu-id="e16c5-109">Kit de développement logiciel (SDK) web</span><span class="sxs-lookup"><span data-stu-id="e16c5-109">Web SDK</span></span>](http://aka.ms/P7b453)

<span data-ttu-id="e16c5-110">Ce kit de développement Web est en version préliminaire et prend en charge Analytique moment hello uniquement et ne gère pas encore d’envoi de notifications push de navigateur ou dans l’application.</span><span class="sxs-lookup"><span data-stu-id="e16c5-110">This Web SDK is in Preview and only supports Analytics at hello moment and doesn't support sending browser or in-app push notifications yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="e16c5-111">toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="e16c5-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="e16c5-112">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="e16c5-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e16c5-113">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span><span class="sxs-lookup"><span data-stu-id="e16c5-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a><span data-ttu-id="e16c5-114">Configuration de Mobile Engagement pour votre application web</span><span class="sxs-lookup"><span data-stu-id="e16c5-114">Setup Mobile Engagement for your Web app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="e16c5-115"><a id="connecting-app"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e16c5-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="e16c5-116">Ce didacticiel présente une « intégration de base, » qui est hello ensemble minimal requis toocollect données.</span><span class="sxs-lookup"><span data-stu-id="e16c5-116">This tutorial presents a "basic integration," which is hello minimal set required toocollect data.</span></span>

<span data-ttu-id="e16c5-117">Bien que vous pouvez suivre les étapes de hello avec n’importe quelle application web également créée en dehors de Visual Studio, nous allons créer une application web de base avec l’intégration de Visual Studio toodemonstrate hello.</span><span class="sxs-lookup"><span data-stu-id="e16c5-117">We will create a basic web app with Visual Studio toodemonstrate hello integration though you can follow hello steps with any web application created outside of Visual Studio also.</span></span> 

### <a name="create-a-new-web-app"></a><span data-ttu-id="e16c5-118">Créer une application web</span><span class="sxs-lookup"><span data-stu-id="e16c5-118">Create a new Web App</span></span>
<span data-ttu-id="e16c5-119">Hello étapes suivantes supposent hello utilisation de Visual Studio 2015 bien que les étapes de hello sont similaires dans les versions antérieures de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e16c5-119">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="e16c5-120">Démarrez Visual Studio et Bonjour **accueil** écran, sélectionnez **nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="e16c5-120">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="e16c5-121">Dans la fenêtre contextuelle hello, sélectionnez **Web** -> **Application Web ASP.Net**.</span><span class="sxs-lookup"><span data-stu-id="e16c5-121">In hello pop-up, select **Web** -> **ASP.Net Web Application**.</span></span> <span data-ttu-id="e16c5-122">Renseignez application hello **nom**, **emplacement** et **nom de la Solution**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e16c5-122">Fill in hello app **Name**, **Location** and  **Solution name**, and then click **OK**.</span></span>
3. <span data-ttu-id="e16c5-123">Bonjour **sélectionner un modèle** menu contextuel, sélectionnez **vide** sous **ASP.Net 4.5 modèles** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e16c5-123">In hello **Select a template** popup, select **Empty** under **ASP.Net 4.5 Templates** and click **OK**.</span></span> 

<span data-ttu-id="e16c5-124">Vous venez de créer un nouveau projet d’application Web vide dans lequel nous intégrera hello Kit de développement Web Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="e16c5-124">You have now created a new blank Web App project into which we will integrate hello Azure Mobile Engagement Web SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="e16c5-125">Se connecter à votre serveur principal d’application tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="e16c5-125">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="e16c5-126">Créez un dossier appelé **javascript** dans votre solution et ajoutez hello Web SDK JS fichier **azure-engagement.js** dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="e16c5-126">Create a new folder called **javascript** in your solution and add hello Web SDK JS file **azure-engagement.js** into it.</span></span> 
2. <span data-ttu-id="e16c5-127">Ajouter un nouveau fichier appelé **main.js** dans ce dossier hello suivant du code javascript.</span><span class="sxs-lookup"><span data-stu-id="e16c5-127">Add a new file called **main.js** in this javascript folder with hello following code.</span></span> <span data-ttu-id="e16c5-128">Vérifiez la chaîne de connexion que tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="e16c5-128">Make sure tooupdate hello connection string.</span></span> <span data-ttu-id="e16c5-129">Cela `azureEngagement` objet sera utilisé tooaccess méthodes du Kit de développement Web.</span><span class="sxs-lookup"><span data-stu-id="e16c5-129">This `azureEngagement` object will be used tooaccess Web SDK methods.</span></span> 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Visual Studio avec des fichiers js][1]

## <a name="enable-real-time-monitoring"></a><span data-ttu-id="e16c5-131">Activer la surveillance en temps réel</span><span class="sxs-lookup"><span data-stu-id="e16c5-131">Enable real-time monitoring</span></span>
<span data-ttu-id="e16c5-132">Dans l’ordre toostart envoi de données et en garantissant que les utilisateurs de hello sont actifs, vous devez envoyer au moins une activité toohello Mobile Engagement principal.</span><span class="sxs-lookup"><span data-stu-id="e16c5-132">In order toostart sending data and ensuring that hello users are active, you must send at least one Activity toohello Mobile Engagement backend.</span></span> <span data-ttu-id="e16c5-133">Une activité dans le contexte de hello d’une application web est une page web.</span><span class="sxs-lookup"><span data-stu-id="e16c5-133">An activity in hello context of a web app is a web page.</span></span> 

1. <span data-ttu-id="e16c5-134">Créer une nouvelle page appelée **home.html** dans votre solution et de la définir en tant que hello démarrage page pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="e16c5-134">Create a new page called **home.html** in your solution and set it as hello starting page for your web app.</span></span> 
2. <span data-ttu-id="e16c5-135">Inclure hello deux scripts JavaScript que nous ajoutés précédemment dans cette page en ajoutant suivant hello au sein de la balise body de hello.</span><span class="sxs-lookup"><span data-stu-id="e16c5-135">Include hello two javascripts we added earlier in this page by adding hello following within hello body tag.</span></span> 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. <span data-ttu-id="e16c5-136">Mettre à jour EngagementAgent hello corps de la balise toocall `startActivity` (méthode)</span><span class="sxs-lookup"><span data-stu-id="e16c5-136">Update hello body tag toocall EngagementAgent's `startActivity` method</span></span>
   
        <body onload="engagement.agent.startActivity('Home')">
4. <span data-ttu-id="e16c5-137">Voici à quoi ressemblera le code de votre page **home.html** .</span><span class="sxs-lookup"><span data-stu-id="e16c5-137">Here is what your **home.html** will look like</span></span>
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="e16c5-138">Connexion d’application avec l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="e16c5-138">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a><span data-ttu-id="e16c5-139">Étendre l’analyse</span><span class="sxs-lookup"><span data-stu-id="e16c5-139">Extend analytics</span></span>
<span data-ttu-id="e16c5-140">Voici toutes les méthodes hello actuellement disponibles avec le Kit de développement logiciel Web que vous pouvez utiliser pour l’analytique :</span><span class="sxs-lookup"><span data-stu-id="e16c5-140">Here are all hello methods currently available with Web SDK that you can use for analytics:</span></span>

1. <span data-ttu-id="e16c5-141">Activités/pages web :</span><span class="sxs-lookup"><span data-stu-id="e16c5-141">Activities/Web pages:</span></span>
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. <span data-ttu-id="e16c5-142">Événements</span><span class="sxs-lookup"><span data-stu-id="e16c5-142">Events</span></span>
   
        engagement.agent.sendEvent(name, extras);
3. <span data-ttu-id="e16c5-143">Erreurs</span><span class="sxs-lookup"><span data-stu-id="e16c5-143">Errors</span></span>
   
        engagement.agent.sendError(name, extras);
4. <span data-ttu-id="e16c5-144">Travaux</span><span class="sxs-lookup"><span data-stu-id="e16c5-144">Jobs</span></span>
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

