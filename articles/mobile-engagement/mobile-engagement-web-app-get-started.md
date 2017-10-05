---
title: "Bien démarrer avec Azure Mobile Engagement pour les applications web | Microsoft Docs"
description: "Découvrez comment utiliser Azure Mobile Engagement avec les fonctions d’analyse et les notifications Push pour les applications web."
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
ms.openlocfilehash: abcb04e4e0a3ae4fdba3a4ded20b3846ac3b21e6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a><span data-ttu-id="be548-103">Prise en main d’Azure Mobile Engagement pour les applications web</span><span class="sxs-lookup"><span data-stu-id="be548-103">Get started with Azure Mobile Engagement for Web Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="be548-104">Cette rubrique vous indique comment tirer parti d’Azure Mobile Engagement pour comprendre l’utilisation de votre application web.</span><span class="sxs-lookup"><span data-stu-id="be548-104">This topic shows you how to use Azure Mobile Engagement to understand your Web App usage.</span></span>

> [!NOTE]
> <span data-ttu-id="be548-105">Le service Azure Mobile Engagement ne sera plus disponible à partir de mars 2018. Actuellement, il reste uniquement accessible aux clients déjà abonnés à ce service.</span><span class="sxs-lookup"><span data-stu-id="be548-105">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="be548-106">Pour plus d’informations, consultez la page [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="be548-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="be548-107">Ce didacticiel requiert les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="be548-107">This tutorial requires the following:</span></span>

* <span data-ttu-id="be548-108">Visual Studio 2015 ou tout autre éditeur de votre choix</span><span class="sxs-lookup"><span data-stu-id="be548-108">Visual Studio 2015 or any other editor of your choice</span></span>
* [<span data-ttu-id="be548-109">Kit de développement logiciel (SDK) web</span><span class="sxs-lookup"><span data-stu-id="be548-109">Web SDK</span></span>](http://aka.ms/P7b453)

<span data-ttu-id="be548-110">Ce Kit de développement logiciel (SDK) web existe en version préliminaire et prend uniquement en charge les fonctions d’analyse pour l’instant ; il ne gère pas encore l’envoi de notifications Push de navigateur ou dans l’application.</span><span class="sxs-lookup"><span data-stu-id="be548-110">This Web SDK is in Preview and only supports Analytics at the moment and doesn't support sending browser or in-app push notifications yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="be548-111">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="be548-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="be548-112">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="be548-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="be548-113">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span><span class="sxs-lookup"><span data-stu-id="be548-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a><span data-ttu-id="be548-114">Configuration de Mobile Engagement pour votre application web</span><span class="sxs-lookup"><span data-stu-id="be548-114">Setup Mobile Engagement for your Web app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="be548-115"><a id="connecting-app"></a>Connexion de votre application au serveur principal Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="be548-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="be548-116">Ce didacticiel présente une intégration de base qui correspond aux éléments minimaux requis pour la collecte de données.</span><span class="sxs-lookup"><span data-stu-id="be548-116">This tutorial presents a "basic integration," which is the minimal set required to collect data.</span></span>

<span data-ttu-id="be548-117">Afin d’illustrer cette intégration, nous allons créer une application web de base avec Visual Studio, bien que vous puissiez également suivre cette procédure avec toute application web créée en dehors de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="be548-117">We will create a basic web app with Visual Studio to demonstrate the integration though you can follow the steps with any web application created outside of Visual Studio also.</span></span> 

### <a name="create-a-new-web-app"></a><span data-ttu-id="be548-118">Créer une application web</span><span class="sxs-lookup"><span data-stu-id="be548-118">Create a new Web App</span></span>
<span data-ttu-id="be548-119">Les étapes suivantes supposent l’utilisation de Visual Studio 2015, même si elles sont similaires dans les versions antérieures de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="be548-119">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="be548-120">Démarrez Visual Studio, puis, dans l’écran **Accueil**, sélectionnez **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="be548-120">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="be548-121">Dans le menu contextuel, sélectionnez **Web** -> **Application web ASP.Net**.</span><span class="sxs-lookup"><span data-stu-id="be548-121">In the pop-up, select **Web** -> **ASP.Net Web Application**.</span></span> <span data-ttu-id="be548-122">Renseignez les champs **Nom**, **Emplacement** et **Nom de la solution**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="be548-122">Fill in the app **Name**, **Location** and  **Solution name**, and then click **OK**.</span></span>
3. <span data-ttu-id="be548-123">Dans le menu contextuel **Sélectionner un modèle**, sélectionnez **Vide** sous **Modèles ASP.Net 4.5**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="be548-123">In the **Select a template** popup, select **Empty** under **ASP.Net 4.5 Templates** and click **OK**.</span></span> 

<span data-ttu-id="be548-124">Vous avez à présent créé un projet d’application web vide dans lequel nous allons intégrer le SDK web Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="be548-124">You have now created a new blank Web App project into which we will integrate the Azure Mobile Engagement Web SDK.</span></span>

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="be548-125">Connexion de votre application au serveur principal Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="be548-125">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="be548-126">Créez un dossier appelé **javascript** dans votre solution et ajoutez-y le fichier JS **azure-engagement.js** du SDK web.</span><span class="sxs-lookup"><span data-stu-id="be548-126">Create a new folder called **javascript** in your solution and add the Web SDK JS file **azure-engagement.js** into it.</span></span> 
2. <span data-ttu-id="be548-127">Ajoutez un nouveau fichier appelé **main.js** dans ce dossier javascript avec le code suivant.</span><span class="sxs-lookup"><span data-stu-id="be548-127">Add a new file called **main.js** in this javascript folder with the following code.</span></span> <span data-ttu-id="be548-128">Veillez à mettre à jour la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="be548-128">Make sure to update the connection string.</span></span> <span data-ttu-id="be548-129">Cet objet `azureEngagement` permettra d’accéder aux méthodes du SDK web.</span><span class="sxs-lookup"><span data-stu-id="be548-129">This `azureEngagement` object will be used to access Web SDK methods.</span></span> 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Visual Studio avec des fichiers js][1]

## <a name="enable-real-time-monitoring"></a><span data-ttu-id="be548-131">Activer la surveillance en temps réel</span><span class="sxs-lookup"><span data-stu-id="be548-131">Enable real-time monitoring</span></span>
<span data-ttu-id="be548-132">Pour commencer à envoyer des données et vous assurer que les utilisateurs sont actifs, vous devez envoyer au moins une activité au serveur principal Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="be548-132">In order to start sending data and ensuring that the users are active, you must send at least one Activity to the Mobile Engagement backend.</span></span> <span data-ttu-id="be548-133">Dans le contexte d’une application web, une activité est une page web.</span><span class="sxs-lookup"><span data-stu-id="be548-133">An activity in the context of a web app is a web page.</span></span> 

1. <span data-ttu-id="be548-134">Créez une page appelée **home.html** dans votre solution et définissez-la comme page de démarrage de votre application web.</span><span class="sxs-lookup"><span data-stu-id="be548-134">Create a new page called **home.html** in your solution and set it as the starting page for your web app.</span></span> 
2. <span data-ttu-id="be548-135">Incluez dans cette page les deux fichiers JavaScript que nous avons ajoutés précédemment en insérant le code ci-après dans la balise body.</span><span class="sxs-lookup"><span data-stu-id="be548-135">Include the two javascripts we added earlier in this page by adding the following within the body tag.</span></span> 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. <span data-ttu-id="be548-136">Mettez à jour la balise body pour appeler la méthode `startActivity` d’EngagementAgent.</span><span class="sxs-lookup"><span data-stu-id="be548-136">Update the body tag to call EngagementAgent's `startActivity` method</span></span>
   
        <body onload="engagement.agent.startActivity('Home')">
4. <span data-ttu-id="be548-137">Voici à quoi ressemblera le code de votre page **home.html** .</span><span class="sxs-lookup"><span data-stu-id="be548-137">Here is what your **home.html** will look like</span></span>
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="be548-138">Connexion d’application avec l’analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="be548-138">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a><span data-ttu-id="be548-139">Étendre l’analyse</span><span class="sxs-lookup"><span data-stu-id="be548-139">Extend analytics</span></span>
<span data-ttu-id="be548-140">Voici toutes les méthodes actuellement disponibles avec le SDK web que vous pouvez utiliser pour l’analyse :</span><span class="sxs-lookup"><span data-stu-id="be548-140">Here are all the methods currently available with Web SDK that you can use for analytics:</span></span>

1. <span data-ttu-id="be548-141">Activités/pages web :</span><span class="sxs-lookup"><span data-stu-id="be548-141">Activities/Web pages:</span></span>
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. <span data-ttu-id="be548-142">Événements</span><span class="sxs-lookup"><span data-stu-id="be548-142">Events</span></span>
   
        engagement.agent.sendEvent(name, extras);
3. <span data-ttu-id="be548-143">Erreurs</span><span class="sxs-lookup"><span data-stu-id="be548-143">Errors</span></span>
   
        engagement.agent.sendError(name, extras);
4. <span data-ttu-id="be548-144">Travaux</span><span class="sxs-lookup"><span data-stu-id="be548-144">Jobs</span></span>
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

