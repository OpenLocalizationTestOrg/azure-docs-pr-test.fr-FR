---
title: "Déployer une application web mobile ASP.NET MVC 5 dans Azure App Service"
description: "Didacticiel expliquant comment déployer une application web dans Azure App Service à l’aide des fonctionnalités mobiles de l’application web ASP.NET MVC 5."
services: app-service
documentationcenter: .net
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: 0752c802-8609-4956-a755-686116913645
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: c98e9b485c52a82e5be5c0f6b0b67912d1e890b9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a><span data-ttu-id="47b5f-103">Déployer une application web mobile ASP.NET MVC 5 dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="47b5f-103">Deploy an ASP.NET MVC 5 mobile web app in Azure App Service</span></span>
<span data-ttu-id="47b5f-104">Ce didacticiel aborde les bases de la conception d’une application web ASP.NET MVC 5 adaptée aux appareils mobiles et de son déploiement dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="47b5f-104">This tutorial will teach you the basics of how to build an ASP.NET MVC 5 web app that is mobile-friendly and deploy it to Azure App Service.</span></span> <span data-ttu-id="47b5f-105">Pour ce didacticiel, vous avez besoin de [Visual Studio Express 2013 pour le Web][Visual Studio Express 2013] ou de l’édition professionnelle de Visual Studio si vous l’avez déjà.</span><span class="sxs-lookup"><span data-stu-id="47b5f-105">For this tutorial, you need [Visual Studio Express 2013 for Web][Visual Studio Express 2013] or the professional edition of Visual Studio if you already have that.</span></span> <span data-ttu-id="47b5f-106">Vous pouvez utiliser [Visual Studio 2015] , mais les captures d'écran seront différentes et vous devrez utiliser les modèles ASP.NET 4.x.</span><span class="sxs-lookup"><span data-stu-id="47b5f-106">You can use [Visual Studio 2015] but the screen shots will be different and you must use the ASP.NET 4.x templates.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a><span data-ttu-id="47b5f-107">Contenu</span><span class="sxs-lookup"><span data-stu-id="47b5f-107">What You'll Build</span></span>
<span data-ttu-id="47b5f-108">Pour ce didacticiel, vous devrez ajouter des fonctionnalités mobiles à l’application simple de listes de conférence fournie dans le [projet de départ][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="47b5f-108">For this tutorial, you'll add mobile features to the simple conference-listing application that's provided in the [starter project][StarterProject].</span></span> <span data-ttu-id="47b5f-109">La capture d’écran suivante illustre les sessions ASP.NET dans l’application terminée, telles qu’elles s’affichent dans l’émulateur de navigateur des outils de développement F12 d’Internet Explorer 11.</span><span class="sxs-lookup"><span data-stu-id="47b5f-109">The following screenshot shows the ASP.NET sessions in the completed application, as seen in the browser emulator in Internet Explorer 11 F12 developer tools.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="47b5f-110">Vous pouvez utiliser les outils destinés aux développeurs F12 d’Internet Explorer 11 et [l’outil Fiddler][Fiddler] pour vous aider à déboguer votre application.</span><span class="sxs-lookup"><span data-stu-id="47b5f-110">You can use the Internet Explorer 11 F12 developer tools and the [Fiddler tool][Fiddler] to help debug your application.</span></span> 

## <a name="skills-youll-learn"></a><span data-ttu-id="47b5f-111">Compétences</span><span class="sxs-lookup"><span data-stu-id="47b5f-111">Skills You'll Learn</span></span>
<span data-ttu-id="47b5f-112">Vous apprendrez les compétences suivantes :</span><span class="sxs-lookup"><span data-stu-id="47b5f-112">Here's what you'll learn:</span></span>

* <span data-ttu-id="47b5f-113">Utilisation de Visual Studio 2013 pour publier votre application web directement dans une application web d’Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="47b5f-113">How to use Visual Studio 2013 to publish your web application directly to a web app in Azure App Service.</span></span>
* <span data-ttu-id="47b5f-114">Comment les modèles ASP.NET MVC 5 utilisent l'infrastructure Bootstrap CSS pour optimiser l'affichage sur les appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="47b5f-114">How the ASP.NET MVC 5 templates use the CSS Bootstrap framework to improve display on mobile devices</span></span>
* <span data-ttu-id="47b5f-115">Comment créer des vues adaptées aux appareils mobiles et personnalisées selon les navigateurs mobiles, comme ceux de l'iPhone ou des téléphones Android.</span><span class="sxs-lookup"><span data-stu-id="47b5f-115">How to create mobile-specific views to target specific mobile browsers, such as the iPhone and Android</span></span>
* <span data-ttu-id="47b5f-116">Comment créer des vues réactives (qui fonctionnent sous différents navigateurs et appareils).</span><span class="sxs-lookup"><span data-stu-id="47b5f-116">How to create responsive views (views that respond to different browsers across devices)</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="47b5f-117">Configuration de l’environnement de développement</span><span class="sxs-lookup"><span data-stu-id="47b5f-117">Set up the development environment</span></span>
<span data-ttu-id="47b5f-118">Configurez l’environnement de développement en installant le Kit de développement logiciel (SDK) Azure pour .NET 2.5.1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="47b5f-118">Set up your development environment by installing the Azure SDK for .NET 2.5.1 or later.</span></span> 

1. <span data-ttu-id="47b5f-119">Pour installer le Kit de développement logiciel (SDK) Azure pour .NET, cliquez sur le lien ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="47b5f-119">To install the Azure SDK for .NET, click the link below.</span></span> <span data-ttu-id="47b5f-120">Si Visual Studio 2013 n'est pas encore installé, il le sera par l'intermédiaire de ce lien.</span><span class="sxs-lookup"><span data-stu-id="47b5f-120">If you don't have Visual Studio 2013 installed yet, it will be installed by the link.</span></span> <span data-ttu-id="47b5f-121">Ce didacticiel requiert Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="47b5f-121">This tutorial requires Visual Studio 2013.</span></span> <span data-ttu-id="47b5f-122">[Kit de développement logiciel (SDK) Azure pour Visual Studio 2013][AzureSDKVs2013]</span><span class="sxs-lookup"><span data-stu-id="47b5f-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span></span>
2. <span data-ttu-id="47b5f-123">Dans la fenêtre Web Platform Installer, cliquez sur **Installer** , puis poursuivez l'installation.</span><span class="sxs-lookup"><span data-stu-id="47b5f-123">In the Web Platform Installer window, click **Install** and proceed with the installation.</span></span>

<span data-ttu-id="47b5f-124">Vous aurez également besoin d'un émulateur de navigateur mobile.</span><span class="sxs-lookup"><span data-stu-id="47b5f-124">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="47b5f-125">Vous pouvez utiliser l'un des émulateurs suivants :</span><span class="sxs-lookup"><span data-stu-id="47b5f-125">Any of the following will work:</span></span>

* <span data-ttu-id="47b5f-126">Émulateur de navigateur dans les [outils de développement F12 d’Internet Explorer 11][EmulatorIE11] (utilisés dans toutes les captures d’écran de navigateurs mobiles).</span><span class="sxs-lookup"><span data-stu-id="47b5f-126">Browser Emulator in [Internet Explorer 11 F12 developer tools][EmulatorIE11] (used in all mobile browser screenshots).</span></span> <span data-ttu-id="47b5f-127">Il dispose de présélections de chaîne d'agent utilisateur pour Windows Phone 8, Windows Phone 7 et l'iPad d'Apple.</span><span class="sxs-lookup"><span data-stu-id="47b5f-127">It has user agent string presets for Windows Phone 8, Windows Phone 7, and Apple iPad.</span></span>
* <span data-ttu-id="47b5f-128">Émulateur de navigateur de [Google Chrome DevTools][EmulatorChrome].</span><span class="sxs-lookup"><span data-stu-id="47b5f-128">Browser Emulator in [Google Chrome DevTools][EmulatorChrome].</span></span> <span data-ttu-id="47b5f-129">Il inclut des présélections pour de nombreux périphériques Android, ainsi que pour l'iPhone d'Apple, l'iPad d'Apple et le Kindle Fire d'Amazon.</span><span class="sxs-lookup"><span data-stu-id="47b5f-129">It contains presets for numerous Android devices, as well as Apple iPhone, Apple iPad, and Amazon Kindle Fire.</span></span> <span data-ttu-id="47b5f-130">Il émule également des événements tactiles.</span><span class="sxs-lookup"><span data-stu-id="47b5f-130">It also emulates touch events.</span></span>
* <span data-ttu-id="47b5f-131">[Émulateur mobile Opera][EmulatorOpera]</span><span class="sxs-lookup"><span data-stu-id="47b5f-131">[Opera Mobile Emulator][EmulatorOpera]</span></span>

<span data-ttu-id="47b5f-132">Des projets Visual Studio avec code source C\# sont disponibles pour cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="47b5f-132">Visual Studio projects with C\# source code are available to accompany this topic:</span></span>

* <span data-ttu-id="47b5f-133">[Téléchargement du projet de départ][StarterProject]</span><span class="sxs-lookup"><span data-stu-id="47b5f-133">[Starter project download][StarterProject]</span></span>
* <span data-ttu-id="47b5f-134">[Téléchargement du projet terminé][CompletedProject]</span><span class="sxs-lookup"><span data-stu-id="47b5f-134">[Completed project download][CompletedProject]</span></span>

## <span data-ttu-id="47b5f-135"><a name="bkmk_DeployStarterProject"></a>Déploiement du projet de départ dans une application Web Azure</span><span class="sxs-lookup"><span data-stu-id="47b5f-135"><a name="bkmk_DeployStarterProject"></a>Deploy the starter project to an Azure web app</span></span>
1. <span data-ttu-id="47b5f-136">Téléchargez le [projet de départ][StarterProject] de l’application de listes de conférence.</span><span class="sxs-lookup"><span data-stu-id="47b5f-136">Download the conference-listing application [starter project][StarterProject].</span></span>
2. <span data-ttu-id="47b5f-137">Dans l’Explorateur Windows, cliquez avec le bouton droit sur le fichier ZIP téléchargé, puis sélectionnez *Propriétés*.</span><span class="sxs-lookup"><span data-stu-id="47b5f-137">Then in Windows Explorer, right-click the downloaded ZIP file and choose *Properties*.</span></span>
3. <span data-ttu-id="47b5f-138">Dans la boîte de dialogue **Propriétés**, cliquez sur le bouton **Débloquer**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-138">In the **Properties** dialog box, choose the **Unblock** button.</span></span> <span data-ttu-id="47b5f-139">Le déblocage empêche l’apparition d’un avertissement de sécurité, qui s’affiche normalement lorsque vous essayez d’utiliser un fichier *.zip* téléchargé à partir d’Internet.</span><span class="sxs-lookup"><span data-stu-id="47b5f-139">(Unblocking prevents a security warning that occurs when you try to use a *.zip* file that you've downloaded from the web.)</span></span>
4. <span data-ttu-id="47b5f-140">Cliquez avec le bouton droit sur le fichier ZIP, puis sélectionnez **Extraire tout** pour décompresser le fichier.</span><span class="sxs-lookup"><span data-stu-id="47b5f-140">Right-click the ZIP file and select **Extract All** to unzip the file.</span></span> 
5. <span data-ttu-id="47b5f-141">Dans Visual Studio, ouvrez le fichier *C#\Mvc5Mobile.sln*.</span><span class="sxs-lookup"><span data-stu-id="47b5f-141">In Visual Studio, open the *C#\Mvc5Mobile.sln* file.</span></span>
6. <span data-ttu-id="47b5f-142">Dans l'Explorateur de solutions, cliquez avec le bouton droit sur le projet, puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-142">In Solution Explorer, right-click the project and click **Publish**.</span></span>
   
   ![][DeployClickPublish]
7. <span data-ttu-id="47b5f-143">Dans Publier le site web, cliquez sur **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-143">In Publish Web, click **Microsoft Azure App Service**.</span></span>
   
   ![][DeployClickWebSites]
8. <span data-ttu-id="47b5f-144">Si vous n’êtes pas déjà connecté à Azure, cliquez sur **Ajouter un compte**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-144">If you haven't already logged into Azure, click **Add an account**.</span></span>
   
   ![][DeploySignIn]
9. <span data-ttu-id="47b5f-145">Suivez les instructions de l’invite pour vous connecter à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="47b5f-145">Follow the prompts to log into your Azure account.</span></span>
10. <span data-ttu-id="47b5f-146">La boîte de dialogue App Service doit maintenant indiquer que vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="47b5f-146">The App Service dialog should now show you as signed in.</span></span> <span data-ttu-id="47b5f-147">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-147">Click **New**.</span></span>
    
    ![][DeployNewWebsite]  
11. <span data-ttu-id="47b5f-148">Dans le champ **Nom de l’application web** , indiquez le préfixe d’un nom d’application unique.</span><span class="sxs-lookup"><span data-stu-id="47b5f-148">In the **Web App Name** field, specify a unique app name prefix.</span></span> <span data-ttu-id="47b5f-149">Le nom complet de votre application web est *&lt;prefix>*.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="47b5f-149">Your fully-qualified web app name will be *&lt;prefix>*.azurewebsites.net.</span></span> <span data-ttu-id="47b5f-150">Par ailleurs, sélectionnez ou spécifiez un nouveau nom de groupe de ressources dans **Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-150">Also, select or specify a new resource group name in **Resource group**.</span></span> <span data-ttu-id="47b5f-151">Ensuite, cliquez sur **Nouveau** pour créer un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="47b5f-151">Then, click **New** to create a new App Service plan.</span></span>
    
    ![][DeploySiteSettings]
12. <span data-ttu-id="47b5f-152">Configurez le nouveau plan App Service et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-152">Configure the new App Service plan and click **OK**.</span></span> 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. <span data-ttu-id="47b5f-153">Dans la boîte de dialogue Créer App Service, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-153">Back in the Create App Service dialog, click **Create**.</span></span>
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. <span data-ttu-id="47b5f-154">Une fois les ressources Azure créées, la boîte de dialogue Publier le site web est renseignée avec les paramètres de votre nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="47b5f-154">After the Azure resources are created, the Publish Web dialog will be filled with the settings for your new app.</span></span> <span data-ttu-id="47b5f-155">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-155">Click **Publish**.</span></span>
    
    ![][DeployPublishSite]
    
    <span data-ttu-id="47b5f-156">Une fois que Visual Studio a terminé de publier le projet de démarrage dans l’application web Azure, le navigateur de bureau s’ouvre et affiche l’application web en ligne.</span><span class="sxs-lookup"><span data-stu-id="47b5f-156">Once Visual Studio finishes publishing the starter project to the Azure web app, the desktop browser opens to display the live web app.</span></span>
15. <span data-ttu-id="47b5f-157">Lancez l’émulateur de navigateur mobile, copiez l’URL de l’application de conférence (*<prefix>*.azurewebsites.net) dans l’émulateur, puis cliquez sur le bouton supérieur droit et sélectionnez **Parcourir par balise**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-157">Start your mobile browser emulator, copy the URL for the conference application (*<prefix>*.azurewebsites.net) into the emulator, and then click the top-right button and select **Browse by tag**.</span></span> <span data-ttu-id="47b5f-158">Si Internet Explorer 11 est votre navigateur par défaut, il vous suffit d’appuyer sur la touche `F12` puis sur les touches `Ctrl+8`, et de basculer le profil du navigateur sur **Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-158">If you are using Internet Explorer 11 as the default browser, you just need to type `F12`, then `Ctrl+8`, and then change the browser profile to **Windows Phone**.</span></span> <span data-ttu-id="47b5f-159">L’image suivante illustre la vue *AllTags* en mode portrait (une fois que l’option **Parcourir par balise**a été sélectionnée).</span><span class="sxs-lookup"><span data-stu-id="47b5f-159">The image below shows the *AllTags* view in portrait mode (from choosing **Browse by tag**).</span></span>
    
    ![][AllTags]

> [!TIP]
> <span data-ttu-id="47b5f-160">De même que vous pouvez déboguer votre application MVC 5 dans Visual Studio, vous pouvez republier votre application web dans Azure pour la vérifier en ligne directement à partir de votre navigateur mobile ou d’un émulateur de navigateur.</span><span class="sxs-lookup"><span data-stu-id="47b5f-160">While you can debug your MVC 5 application from within Visual Studio, you can publish your web app to Azure again to verify the live web app directly from your mobile browser or a browser emulator.</span></span>
> 
> 

<span data-ttu-id="47b5f-161">L'affichage est tout à fait lisible sur un appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="47b5f-161">The display is very readable on a mobile device.</span></span> <span data-ttu-id="47b5f-162">Vous pouvez également déjà voir certains effets visuels appliqués par l'infrastructure CSS Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="47b5f-162">You can also already see some of the visual effects applied by the Bootstrap CSS framework.</span></span>
<span data-ttu-id="47b5f-163">Cliquez sur le lien **ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="47b5f-163">Click the **ASP.NET** link.</span></span>

![][SessionsByTagASP.NET]

<span data-ttu-id="47b5f-164">La vue avec balises ASP.NET s’adapte à l’écran, ce que Bootstrap effectue pour vous automatiquement.</span><span class="sxs-lookup"><span data-stu-id="47b5f-164">The ASP.NET tag view is zoom-fitted to the screen, which Bootstrap does for you automatically.</span></span> <span data-ttu-id="47b5f-165">Cependant, vous pouvez optimiser cette vue pour une meilleure adaptation au navigateur mobile.</span><span class="sxs-lookup"><span data-stu-id="47b5f-165">However, you can improve this view to better suit the mobile browser.</span></span> <span data-ttu-id="47b5f-166">Par exemple, la colonne **Date** n’est pas très lisible.</span><span class="sxs-lookup"><span data-stu-id="47b5f-166">For example, the **Date** column is difficult to read.</span></span> <span data-ttu-id="47b5f-167">Plus loin dans ce didacticiel, vous modifierez la vue *AllTags* pour l’adapter aux appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="47b5f-167">Later in the tutorial you'll change the *AllTags* view to make it mobile-friendly.</span></span>

## <span data-ttu-id="47b5f-168"><a name="bkmk_bootstrap"></a> Infrastructure CSS Bootstrap</span><span class="sxs-lookup"><span data-stu-id="47b5f-168"><a name="bkmk_bootstrap"></a> Bootstrap CSS Framework</span></span>
<span data-ttu-id="47b5f-169">La prise en charge de Bootstrap intégrée est une nouveauté du modèle MVC 5.</span><span class="sxs-lookup"><span data-stu-id="47b5f-169">New in the MVC 5 template is built-in Bootstrap support.</span></span> <span data-ttu-id="47b5f-170">Vous avez déjà vu comment cette prise en charge améliore les différentes vues dans votre application.</span><span class="sxs-lookup"><span data-stu-id="47b5f-170">You have already seen how it immediately improves the different views in your application.</span></span> <span data-ttu-id="47b5f-171">Par exemple, la barre de navigation dans la partie supérieure se réduit automatiquement lorsque la largeur du navigateur est inférieure.</span><span class="sxs-lookup"><span data-stu-id="47b5f-171">For example, the navigation bar at the top is automatically collapsible when the browser width is smaller.</span></span> <span data-ttu-id="47b5f-172">Sur le navigateur de bureau, essayez de redimensionner la fenêtre du navigateur et observez le comportement de la barre de navigation.</span><span class="sxs-lookup"><span data-stu-id="47b5f-172">On the desktop browser, try resizing the browser window and see how the navigation bar changes its look and feel.</span></span> <span data-ttu-id="47b5f-173">Il s'agit de la conception de sites web réactive intégrée à Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="47b5f-173">This is the responsive web design that is built into Bootstrap.</span></span>

<span data-ttu-id="47b5f-174">Pour voir à quoi ressemblerait l’application web sans Bootstrap, ouvrez le fichier *App\_Start\\BundleConfig.cs* et placez les lignes qui contiennent *bootstrap.js* et *bootstrap.css* en commentaire.</span><span class="sxs-lookup"><span data-stu-id="47b5f-174">To see how the Web app would look without Bootstrap, open *App\_Start\\BundleConfig.cs* and comment out the lines that contain *bootstrap.js* and *bootstrap.css*.</span></span> <span data-ttu-id="47b5f-175">Le code ci-après indique les deux dernières instructions de la méthode `RegisterBundles` après la modification :</span><span class="sxs-lookup"><span data-stu-id="47b5f-175">The following code shows the last two statements of the `RegisterBundles` method after the change:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

<span data-ttu-id="47b5f-176">Appuyez sur `Ctrl+F5` pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="47b5f-176">Press `Ctrl+F5` to run the application.</span></span>

<span data-ttu-id="47b5f-177">La barre de navigation réductible a maintenant la forme d’une simple liste non triée classique.</span><span class="sxs-lookup"><span data-stu-id="47b5f-177">Observe that the collapsible navigation bar is now just an ordinary unordered list.</span></span> <span data-ttu-id="47b5f-178">Cliquez sur **Parcourir par balise** une nouvelle fois, puis cliquez sur **ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-178">Click **Browse by tag** again, then click **ASP.NET**.</span></span>
<span data-ttu-id="47b5f-179">Dans la vue de l’émulateur mobile, vous voyez maintenant qu’elle n’est plus adaptée à l’écran, et vous devez faire défiler la page horizontalement afin de voir le côté droit du tableau.</span><span class="sxs-lookup"><span data-stu-id="47b5f-179">In the mobile emulator view, you can see now that it is no longer zoom-fitted to the screen, and you must scroll sideways in order to see the right side of the table.</span></span>

![][SessionsByTagASP.NETNoBootstrap]

<span data-ttu-id="47b5f-180">Annulez vos modifications et actualisez le navigateur mobile pour vérifier que l'affichage adapté aux appareils mobiles a été rétabli.</span><span class="sxs-lookup"><span data-stu-id="47b5f-180">Undo your changes and refresh the mobile browser to verify that the mobile-friendly display has been restored.</span></span>

<span data-ttu-id="47b5f-181">Bootstrap n’est pas propre à ASP.NET MVC 5 et vous pouvez tirer parti de ces fonctionnalités dans n’importe quelle application web.</span><span class="sxs-lookup"><span data-stu-id="47b5f-181">Bootstrap is not specific to ASP.NET MVC 5, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="47b5f-182">Désormais, Bootstrap est intégré au modèle de projet ASP.NET MVC 5. Votre application web MVC 5 peut donc tirer parti de Bootstrap par défaut.</span><span class="sxs-lookup"><span data-stu-id="47b5f-182">But it is now built into the ASP.NET MVC 5 project template, so that your MVC 5 Web application can take advantage of Bootstrap by default.</span></span>

<span data-ttu-id="47b5f-183">Pour plus d’informations sur Bootstrap, rendez-vous sur le site [Bootstrap][BootstrapSite].</span><span class="sxs-lookup"><span data-stu-id="47b5f-183">For more information about Bootstrap, go to the [Bootstrap][BootstrapSite] site.</span></span>

<span data-ttu-id="47b5f-184">La section suivante vous indique comment proposer des vues spécialement adaptées aux navigateurs mobiles.</span><span class="sxs-lookup"><span data-stu-id="47b5f-184">In the next section you'll see how to provide mobile-browser specific views.</span></span>

## <span data-ttu-id="47b5f-185"><a name="bkmk_overrideviews"></a> Remplacement des vues, des dispositions et des vues partielles</span><span class="sxs-lookup"><span data-stu-id="47b5f-185"><a name="bkmk_overrideviews"></a> Override the Views, Layouts, and Partial Views</span></span>
<span data-ttu-id="47b5f-186">Vous pouvez remplacer toutes les vues (y compris les dispositions et les vues partielles) des navigateurs mobiles en général, mais aussi d’un navigateur mobile particulier ou encore d’un navigateur spécifique.</span><span class="sxs-lookup"><span data-stu-id="47b5f-186">You can override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="47b5f-187">Pour fournir un affichage mobile, vous pouvez copier un fichier de vue et ajouter *.Mobile* au nom du fichier.</span><span class="sxs-lookup"><span data-stu-id="47b5f-187">To provide a mobile-specific view, you can copy a view file and add *.Mobile* to the file name.</span></span> <span data-ttu-id="47b5f-188">Par exemple, pour créer une vue mobile *Index*, vous pouvez copier *Views\\Home\\Index.cshtml* vers *Views\\Home\\Index.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="47b5f-188">For example, to create a mobile *Index* view, you can copy *Views\\Home\\Index.cshtml* to *Views\\Home\\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="47b5f-189">Dans cette section, vous allez créer un fichier de disposition mobile.</span><span class="sxs-lookup"><span data-stu-id="47b5f-189">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="47b5f-190">Tout d’abord, copiez *Views\\Shared\\\_Layout.cshtml* vers *Views\\Shared\\\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="47b5f-190">To start, copy *Views\\Shared\\\_Layout.cshtml* to *Views\\Shared\\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="47b5f-191">Ouvrez *\_Layout.Mobile.cshtml* et remplacez le titre **MVC5 Application** par **MVC5 Application (Mobile)**.</span><span class="sxs-lookup"><span data-stu-id="47b5f-191">Open *\_Layout.Mobile.cshtml* and change the title from **MVC5 Application** to **MVC5 Application (Mobile)**.</span></span>

<span data-ttu-id="47b5f-192">Dans chaque appel `Html.ActionLink` pour la barre de navigation, supprimez « Parcourir par »de chaque lien *ActionLink*.</span><span class="sxs-lookup"><span data-stu-id="47b5f-192">In each `Html.ActionLink` call for the navigation bar, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="47b5f-193">Le code suivant affiche la balise `<ul class="nav navbar-nav">` terminée d’un fichier de disposition mobile.</span><span class="sxs-lookup"><span data-stu-id="47b5f-193">The following code shows the completed `<ul class="nav navbar-nav">` tag of the mobile layout file.</span></span>

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

<span data-ttu-id="47b5f-194">Copiez le fichier *Views\\Home\\AllTags.cshtml* vers *Views\\Home\\AllTags.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="47b5f-194">Copy the *Views\\Home\\AllTags.cshtml* file to *Views\\Home\\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="47b5f-195">Ouvrez le nouveau fichier et, pour l'élément `<h2>` , remplacez « Tags » par « Tags (M) » :</span><span class="sxs-lookup"><span data-stu-id="47b5f-195">Open the new file and change the `<h2>` element from "Tags" to "Tags (M)":</span></span>

    <h2>Tags (M)</h2>

<span data-ttu-id="47b5f-196">Accédez à la page des balises à l'aide d'un navigateur de Bureau et de l'émulateur de navigateur mobile.</span><span class="sxs-lookup"><span data-stu-id="47b5f-196">Browse to the tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="47b5f-197">L’émulateur de navigateur mobile affiche les deux modifications que vous avez effectuées (le titre de *\_Layout.Mobile.cshtml* et le titre de *AllTags.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="47b5f-197">The mobile browser emulator shows the two changes you made (the title from *\_Layout.Mobile.cshtml* and the title from *AllTags.Mobile.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobile]

<span data-ttu-id="47b5f-198">En revanche, l’affichage du Bureau n’a pas changé (avec des titres de *\_Layout.cshtml* et *AllTags.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="47b5f-198">In contrast, the desktop display has not changed (with titles from *\_Layout.cshtml* and *AllTags.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobileDesktop]

## <span data-ttu-id="47b5f-199"><a name="bkmk_browserviews"></a> Création de vues spécifiques du navigateur</span><span class="sxs-lookup"><span data-stu-id="47b5f-199"><a name="bkmk_browserviews"></a> Create Browser-Specific Views</span></span>
<span data-ttu-id="47b5f-200">Outre les vues mobiles et de bureau, vous pouvez créer des vues pour un navigateur en particulier.</span><span class="sxs-lookup"><span data-stu-id="47b5f-200">In addition to mobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="47b5f-201">Par exemple, il est possible de créer des vues spécialement adaptées aux navigateurs de l'iPhone et sous Android.</span><span class="sxs-lookup"><span data-stu-id="47b5f-201">For example, you can create views that are specifically for the iPhone or the Android browser.</span></span> <span data-ttu-id="47b5f-202">Dans cette section, vous allez créer une disposition pour le navigateur de l’iPhone et une version pour iPhone de la vue *AllTags* .</span><span class="sxs-lookup"><span data-stu-id="47b5f-202">In this section, you'll create a layout for the iPhone browser and an iPhone version of the *AllTags* view.</span></span>

<span data-ttu-id="47b5f-203">Ouvrez le fichier *Global.asax* et ajoutez le code suivant comme dernière ligne de la méthode `Application_Start`.</span><span class="sxs-lookup"><span data-stu-id="47b5f-203">Open the *Global.asax* file and add the following code to the bottom of the `Application_Start` method.</span></span>

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

<span data-ttu-id="47b5f-204">Ce code définit un nouveau mode d’affichage appelé « iPhone », qui répondra à chaque demande entrante.</span><span class="sxs-lookup"><span data-stu-id="47b5f-204">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="47b5f-205">Si la demande entrante correspond à la condition que vous avez définie (c'est-à-dire, si l'agent utilisateur contient la chaîne « iPhone »), ASP.NET MVC recherche des affichages dont le nom contient le suffixe « iPhone ».</span><span class="sxs-lookup"><span data-stu-id="47b5f-205">If the incoming request matches the condition you defined (that is, if the user agent contains the string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

> [!NOTE]
> <span data-ttu-id="47b5f-206">Lors de l’ajout de modes d’affichage de navigateur mobile, pour iPhone et Android par exemple, assurez-vous de définir le premier argument sur `0` (insérez-le en haut de la liste) pour que le mode navigateur ait la priorité sur le modèle mobile (*.Mobile.cshtml).</span><span class="sxs-lookup"><span data-stu-id="47b5f-206">When adding mobile browser-specific display modes, such as for iPhone and Android, be sure to set the first argument to `0` (insert at the top of the list) to make sure that the browser-specific mode takes precedence over the mobile template (*.Mobile.cshtml).</span></span> <span data-ttu-id="47b5f-207">Si le modèle mobile est en haut de la liste, il est sélectionné à la place du mode d'affichage souhaité (le premier résultat est prioritaire et le modèle mobile correspond à tous les navigateurs mobiles).</span><span class="sxs-lookup"><span data-stu-id="47b5f-207">If the mobile template is at the top of the list instead, it will be selected over your intended display mode (the first match wins, and the mobile template matches all mobile browsers).</span></span> 
> 
> 

<span data-ttu-id="47b5f-208">Dans le code, cliquez avec le bouton droit sur `DefaultDisplayMode`, sélectionnez **Résoudre**, puis choisissez `using System.Web.WebPages;`.</span><span class="sxs-lookup"><span data-stu-id="47b5f-208">In the code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="47b5f-209">Cette action permet d’ajouter une référence à l’espace de noms `System.Web.WebPages`, qui se situe là où les types `DisplayModeProvider` et `DefaultDisplayMode` sont définis.</span><span class="sxs-lookup"><span data-stu-id="47b5f-209">This adds a reference to the `System.Web.WebPages` namespace, which is where the `DisplayModeProvider` and `DefaultDisplayMode` types are defined.</span></span>

![][ResolveDefaultDisplayMode]

<span data-ttu-id="47b5f-210">Vous pouvez aussi ajouter manuellement la ligne suivante à la section `using` du fichier.</span><span class="sxs-lookup"><span data-stu-id="47b5f-210">Alternatively, you can just manually add the following line to the `using` section of the file.</span></span>

    using System.Web.WebPages;

<span data-ttu-id="47b5f-211">Enregistrez les modifications.</span><span class="sxs-lookup"><span data-stu-id="47b5f-211">Save the changes.</span></span> <span data-ttu-id="47b5f-212">Copiez le fichier *Views\\Shared\\\_Layout.Mobile.cshtml* vers *Views\\Shared\\\_Layout.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="47b5f-212">Copy the *Views\\Shared\\\_Layout.Mobile.cshtml* file to *Views\\Shared\\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="47b5f-213">Ouvrez le nouveau fichier, puis remplacez le titre `MVC5 Application (Mobile)` par `MVC5 Application (iPhone)`.</span><span class="sxs-lookup"><span data-stu-id="47b5f-213">Open the new file and then change the title from `MVC5 Application (Mobile)` to `MVC5 Application (iPhone)`.</span></span>

<span data-ttu-id="47b5f-214">Copiez le fichier *Views\\Home\\AllTags.Mobile.cshtml* vers *Views\\Home\\AllTags.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="47b5f-214">Copy the *Views\\Home\\AllTags.Mobile.cshtml* file to *Views\\Home\\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="47b5f-215">Dans le nouveau fichier, pour l’élément `<h2>` , remplacez « Tags (M) » par « Tags (iPhone) ».</span><span class="sxs-lookup"><span data-stu-id="47b5f-215">In the new file, change the `<h2>` element from "Tags (M)" to "Tags (iPhone)".</span></span>

<span data-ttu-id="47b5f-216">Exécutez l'application.</span><span class="sxs-lookup"><span data-stu-id="47b5f-216">Run the application.</span></span> <span data-ttu-id="47b5f-217">Lancez un émulateur de navigateur mobile, vérifiez que son agent utilisateur est défini sur « iPhone » et parcourez la vue *AllTags* .</span><span class="sxs-lookup"><span data-stu-id="47b5f-217">Run a mobile browser emulator, make sure its user agent is set to "iPhone", and browse to the *AllTags* view.</span></span> <span data-ttu-id="47b5f-218">Si vous utilisez l’émulateur dans les outils de développement F12 d’Internet Explorer 11,configurez l’émulation comme suit :</span><span class="sxs-lookup"><span data-stu-id="47b5f-218">If you are using the emulator in Internet Explorer 11 F12 developer tools, configure emulation to the following:</span></span>

* <span data-ttu-id="47b5f-219">Profil du navigateur = **Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="47b5f-219">Browser profile = **Windows Phone**</span></span>
* <span data-ttu-id="47b5f-220">Chaîne d’agent utilisateur = **Custom**</span><span class="sxs-lookup"><span data-stu-id="47b5f-220">User agent string =  **Custom**</span></span>
* <span data-ttu-id="47b5f-221">Chaîne personnalisée = **Apple-iPhone5C1/1001.525**</span><span class="sxs-lookup"><span data-stu-id="47b5f-221">Custom string = **Apple-iPhone5C1/1001.525**</span></span>

<span data-ttu-id="47b5f-222">La capture d’écran ci-après présente la vue *AllTags* affichée dans l’émulateur des outils destinés aux développeurs F12 d’Internet Explorer 11, avec la chaîne d’agent utilisateur personnalisée (il s’agit d’une chaîne d’agent utilisateur d’un iPhone 5C).</span><span class="sxs-lookup"><span data-stu-id="47b5f-222">The following screenshot shows the *AllTags* view rendered in the emulator in Internet Explorer 11 F12 developer tools with the custom user agent string (this is an iPhone 5C user agent string).</span></span>

![][AllTagsIPhone_LayoutIPhone]

<span data-ttu-id="47b5f-223">Dans le navigateur mobile, sélectionnez le lien **Intervenants** .</span><span class="sxs-lookup"><span data-stu-id="47b5f-223">In the mobile browser, select the **Speakers** link.</span></span> <span data-ttu-id="47b5f-224">En l’absence d’affichage mobile (*AllSpeakers.Mobile.cshtml*), la vue par défaut des intervenants (*AllSpeakers.cshtml*) est affichée à l’aide du mode de disposition mobile (*\_Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="47b5f-224">Because there's not a mobile view (*AllSpeakers.Mobile.cshtml*), the default speakers view (*AllSpeakers.cshtml*) is rendered using the mobile layout view (*\_Layout.Mobile.cshtml*).</span></span> <span data-ttu-id="47b5f-225">Comme indiqué ci-dessous, le titre **MVC5 Application (Mobile)** est défini dans *\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="47b5f-225">As shown below, the title **MVC5 Application (Mobile)** is defined in *\_Layout.Mobile.cshtml*.</span></span>

![][AllSpeakers_LayoutMobile]

<span data-ttu-id="47b5f-226">Vous pouvez globalement désactiver l’affichage d’une vue par défaut (non mobile) au sein d’une disposition mobile en définissant `RequireConsistentDisplayMode` sur `true` dans le fichier *Views\\\_ViewStart.cshtml*, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="47b5f-226">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in the *Views\\\_ViewStart.cshtml* file, like this:</span></span>

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

<span data-ttu-id="47b5f-227">Lorsque `RequireConsistentDisplayMode` est défini sur `true`, la disposition mobile (*\_Layout.Mobile.cshtml*) est uniquement utilisée pour les vues mobiles (autrement dit, lorsque le fichier de vue se présente sous la forme ***ViewName**.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="47b5f-227">When `RequireConsistentDisplayMode` is set to `true`, the mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views (i.e. when the view file is of the form ***ViewName**.Mobile.cshtml*).</span></span> <span data-ttu-id="47b5f-228">Vous pouvez définir `RequireConsistentDisplayMode` sur `true` si votre disposition mobile ne fonctionne pas correctement avec les vues non mobiles.</span><span class="sxs-lookup"><span data-stu-id="47b5f-228">You might want to set `RequireConsistentDisplayMode` to `true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="47b5f-229">La capture d’écran ci-après indique comment la page *Speakers* s’affiche lorsque `RequireConsistentDisplayMode` est défini sur `true` (sans la chaîne « (Mobile) » dans la barre de navigation supérieure).</span><span class="sxs-lookup"><span data-stu-id="47b5f-229">The screenshot below shows how the *Speakers* page renders when `RequireConsistentDisplayMode` is set to `true` (without the string "(Mobile)" in the navigational bar at the top).</span></span>

![][AllSpeakers_LayoutMobileOverridden]

<span data-ttu-id="47b5f-230">Vous pouvez désactiver le mode d’affichage cohérent dans une vue spécifique en définissant `RequireConsistentDisplayMode` sur `false` dans le fichier de vue.</span><span class="sxs-lookup"><span data-stu-id="47b5f-230">You can disable consistent display mode in a specific view by setting `RequireConsistentDisplayMode` to `false` in the view file.</span></span> <span data-ttu-id="47b5f-231">Le balisage suivant du fichier *View\\Home\\AllSpeakers.cshtml* définit `RequireConsistentDisplayMode` sur `false` :</span><span class="sxs-lookup"><span data-stu-id="47b5f-231">The following markup in the *Views\\Home\\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` to `false`:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

<span data-ttu-id="47b5f-232">Dans cette section, nous avons vu comment créer des dispositions mobiles et des vues, ainsi que des dispositions et des vues pour des appareils spécifiques tels que l’iPhone.</span><span class="sxs-lookup"><span data-stu-id="47b5f-232">In this section we've seen how to create mobile layouts and views and how to create layouts and views for specific devices such as the iPhone.</span></span>
<span data-ttu-id="47b5f-233">Toutefois, le principal avantage de l'infrastructure d'amorçage (Bootstrap) CSS est la disposition réactive, ce qui signifie qu'une seule feuille de style peut être appliquée sur les navigateurs de bureau, de téléphone et de tablette pour créer une apparence cohérente.</span><span class="sxs-lookup"><span data-stu-id="47b5f-233">However, the main advantage of the Bootstrap CSS framework is the responsive layout, which means that a single stylesheet can be applied across desktop, phone, and tablet browsers to create a consistent look and feel.</span></span> <span data-ttu-id="47b5f-234">La section suivante vous indique comment tirer parti de Bootstrap pour créer des vues adaptées aux appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="47b5f-234">In the next section you'll see how to leverage Bootstrap to create mobile-friendly views.</span></span>

## <span data-ttu-id="47b5f-235"><a name="bkmk_Improvespeakerslist"></a> Amélioration de la liste Intervenants</span><span class="sxs-lookup"><span data-stu-id="47b5f-235"><a name="bkmk_Improvespeakerslist"></a> Improve the Speakers List</span></span>
<span data-ttu-id="47b5f-236">Comme vous venez de le voir, la vue *Speakers* est lisible, mais les liens sont petits et il est difficile de les sélectionner sur un appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="47b5f-236">As you just saw, the *Speakers* view is readable, but the links are small and are difficult to tap on a mobile device.</span></span> <span data-ttu-id="47b5f-237">Dans cette section, vous allez adapter la vue *AllSpeakers* aux appareils mobiles. Les liens seront plus grands, faciles à sélectionner et contiendront une zone de recherche pour trouver des intervenants rapidement.</span><span class="sxs-lookup"><span data-stu-id="47b5f-237">In this section, you'll make the *AllSpeakers* view mobile-friendly, which displays large, easy-to-tap links and contains a search box to quickly find speakers.</span></span>

<span data-ttu-id="47b5f-238">Vous pouvez utiliser le style [linked list group][linked list group] pour améliorer la vue *Speakers*.</span><span class="sxs-lookup"><span data-stu-id="47b5f-238">You can use the Bootstrap [linked list group][linked list group] styling to improve the *Speakers* view.</span></span> <span data-ttu-id="47b5f-239">Dans *Views\\Home\\AllSpeakers.cshtml*, remplacez le contenu du fichier Razor par le code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="47b5f-239">In *Views\\Home\\AllSpeakers.cshtml*, replace the contents of the Razor file with the code below.</span></span>

     @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, "SessionsBySpeaker", new { speaker }, new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="47b5f-240">L’attribut `class="list-group"` de la balise `<div>` s’applique au style de liste Bootstrap, tandis que l’attribut `class="input-group-item"` s’applique au style de l’élément de liste Bootstrap pour chaque lien.</span><span class="sxs-lookup"><span data-stu-id="47b5f-240">The `class="list-group"` attribute in the `<div>` tag applies the Bootstrap list styling, and the `class="input-group-item"` attribute applies Bootstrap list item styling to each link.</span></span>

<span data-ttu-id="47b5f-241">Actualisez le navigateur mobile.</span><span class="sxs-lookup"><span data-stu-id="47b5f-241">Refresh the mobile browser.</span></span> <span data-ttu-id="47b5f-242">L'affichage actualisé ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="47b5f-242">The updated view looks like this:</span></span>

![][AllSpeakersFixed]

<span data-ttu-id="47b5f-243">Avec le style [linked list group][linked list group] Bootstrap, toute la zone de chaque lien est cliquable, ce qui confère un expérience utilisateur bien supérieure.</span><span class="sxs-lookup"><span data-stu-id="47b5f-243">The Bootstrap [linked list group][linked list group] styling makes the entire box for each link clickable, which is a much better user experience.</span></span> <span data-ttu-id="47b5f-244">Basculez vers l’affichage de bureau et observez l’homogénéité de l’apparence.</span><span class="sxs-lookup"><span data-stu-id="47b5f-244">Switch to the desktop view and observe the consistent look and feel.</span></span>

![][AllSpeakersFixedDesktop]

<span data-ttu-id="47b5f-245">Certes, l’affichage du navigateur mobile a été amélioré, mais il est tout de même difficile de parcourir la longue liste d’intervenants.</span><span class="sxs-lookup"><span data-stu-id="47b5f-245">Although the mobile browser view has improved, it's difficult to navigate the long list of speakers.</span></span> <span data-ttu-id="47b5f-246">Bootstrap est dépourvu d'une fonction de filtre de recherche en natif. Il est possible d'en ajouter une à l'aide de quelques lignes de code.</span><span class="sxs-lookup"><span data-stu-id="47b5f-246">Bootstrap doesn't provide a search filter functionality out-of-the-box, but you can add it with a few lines of code.</span></span> <span data-ttu-id="47b5f-247">Tout d'abord, vous devez ajouter un champ de recherche à la vue, puis connecter du code JavaScript pour la fonction de filtre.</span><span class="sxs-lookup"><span data-stu-id="47b5f-247">You will first add a search box to the view, then hook up with the JavaScript code for the filter function.</span></span> <span data-ttu-id="47b5f-248">Dans *Views\\Home\\AllSpeakers.cshtml*, ajoutez une balise \<form\> juste après la balise \<h2\>, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="47b5f-248">In *Views\\Home\\AllSpeakers.cshtml*, add a \<form\> tag just after the \<h2\> tag, as shown below:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All Speakers";
    }

    <h2>Speakers</h2>

    <form class="input-group">
        <span class="input-group-addon"><span class="glyphicon glyphicon-search"></span></span>
        <input type="text" class="form-control" placeholder="Search speaker">
    </form>
    <br />
    <div class="list-group">
        @foreach (var speaker in Model)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class = "list-group-item" })
        }
    </div>

<span data-ttu-id="47b5f-249">Notez que les styles Bootstrap sont appliqués aux deux balises `<form>` et `<input>`.</span><span class="sxs-lookup"><span data-stu-id="47b5f-249">Notice that the `<form>` and `<input>` tags both have the Bootstrap styles applied to them.</span></span> <span data-ttu-id="47b5f-250">L’élément `<span>` ajoute un [glyphicon][glyphicon] Bootstrap à la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="47b5f-250">The `<span>` element adds a Bootstrap [glyphicon][glyphicon] to the search box.</span></span>

<span data-ttu-id="47b5f-251">Dans le dossier *Scripts*, ajoutez un fichier JavaScript intitulé *filter.js*.</span><span class="sxs-lookup"><span data-stu-id="47b5f-251">In the *Scripts* folder, add a JavaScript file called *filter.js*.</span></span> <span data-ttu-id="47b5f-252">Ouvrez le fichier et collez-y le code suivant :</span><span class="sxs-lookup"><span data-stu-id="47b5f-252">Open the file and paste the following code into it:</span></span>

    $(function () {

        // reset the search form when the page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up the events to the <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with the typed text and hide others
            for (var i = 0; i < items.length; i++) {
                var val = items[i].text.toLowerCase();
                val = val.substring(0, searchtxt.length);
                if (val == searchtxt) {
                    $(items[i]).show();
                }
                else {
                    $(items[i]).hide();
                }
            }
        });
    });

<span data-ttu-id="47b5f-253">Vous devez également inclure le fichier filter.js à vos lots enregistrés.</span><span class="sxs-lookup"><span data-stu-id="47b5f-253">You also need to include filter.js in your registered bundles.</span></span> <span data-ttu-id="47b5f-254">Ouvrez le fichier *App\_Start\\BundleConfig.cs* et modifiez les premiers lots.</span><span class="sxs-lookup"><span data-stu-id="47b5f-254">Open *App\_Start\\BundleConfig.cs* and change the first bundles.</span></span> <span data-ttu-id="47b5f-255">Modifiez la première instruction `bundles.Add` (pour le lot **jquery**) de manière à inclure le fichier *Scripts\\filter.js*, comme décrit ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="47b5f-255">Change the first `bundles.Add` statement (for the **jquery** bundle) to include *Scripts\\filter.js*, as follows:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

<span data-ttu-id="47b5f-256">Le lot **jquery** est déjà rendu par la vue *\_Layout* par défaut.</span><span class="sxs-lookup"><span data-stu-id="47b5f-256">The **jquery** bundle is already rendered by the default *\_Layout* view.</span></span> <span data-ttu-id="47b5f-257">Plus tard, vous pourrez utiliser le même code JavaScript pour appliquer la fonction de filtre aux autres vues de liste.</span><span class="sxs-lookup"><span data-stu-id="47b5f-257">Later, you can utilize the same JavaScript code to apply the filter functionality to other list views.</span></span>

<span data-ttu-id="47b5f-258">Actualisez le navigateur mobile et accédez à l'affichage *AllSpeakers* .</span><span class="sxs-lookup"><span data-stu-id="47b5f-258">Refresh the mobile browser and go to the *AllSpeakers* view.</span></span> <span data-ttu-id="47b5f-259">Dans la zone de recherche, entrez « sc ».</span><span class="sxs-lookup"><span data-stu-id="47b5f-259">In the search box, type "sc".</span></span> <span data-ttu-id="47b5f-260">La liste des intervenants doit à présent être filtrée selon vos critères de recherche.</span><span class="sxs-lookup"><span data-stu-id="47b5f-260">The speakers list should now be filtered according to your search string.</span></span>

![][AllSpeakersFixedSearchBySC]

## <span data-ttu-id="47b5f-261"><a name="bkmk_improvetags"></a> Amélioration de la liste Balises</span><span class="sxs-lookup"><span data-stu-id="47b5f-261"><a name="bkmk_improvetags"></a> Improve the Tags List</span></span>
<span data-ttu-id="47b5f-262">À l’instar de la vue *Speakers*, la vue *Tags* est lisible, mais les liens sont petits et il est difficile de les sélectionner sur un appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="47b5f-262">Like the *Speakers* view, the *Tags* view is readable, but the links are small and difficult to tap on a mobile device.</span></span> <span data-ttu-id="47b5f-263">Vous pouvez optimiser la vue *Tags* de la même façon que vous l’avez fait avec la vue *Speakers*. Vous devez utiliser les modifications de code décrites plus haut mais en suivant la syntaxe de méthode `Html.ActionLink` dans *Views\\Home\\AllTags.cshtml* :</span><span class="sxs-lookup"><span data-stu-id="47b5f-263">You can fix the *Tags* view the same way you fix the *Speakers* view, if you use the code changes described earlier, but with the following `Html.ActionLink` method syntax in *Views\\Home\\AllTags.cshtml*:</span></span>

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="47b5f-264">Le navigateur de bureau actualisé se présente désormais ainsi :</span><span class="sxs-lookup"><span data-stu-id="47b5f-264">The refreshed desktop browser looks as follows:</span></span>

![][AllTagsFixedDesktop]

<span data-ttu-id="47b5f-265">Quant au navigateur mobile actualisé, il se présente ainsi :</span><span class="sxs-lookup"><span data-stu-id="47b5f-265">And the refreshed mobile browser looks as follows:</span></span> 

![][AllTagsFixed]

> [!NOTE]
> <span data-ttu-id="47b5f-266">Si vous remarquez que le format de liste d’origine apparaît toujours dans le navigateur mobile, et que vous vous demandez ce que votre style Bootstrap est devenu, il s’agit d’un artefact de votre précédente action visant à créer des vues propres aux navigateurs mobiles.</span><span class="sxs-lookup"><span data-stu-id="47b5f-266">If you notice that the original list formatting is still there in the mobile browser and wonder what happened to your nice Bootstrap styling, this is an artifact of your earlier action to create mobile specific views.</span></span> <span data-ttu-id="47b5f-267">Toutefois, maintenant que vous utilisez l'infrastructure CSS Bootstrap pour créer une conception Web réactive, passez à l'étape suivante et supprimez les vues et les dispositions spécifiques aux navigateurs mobiles.</span><span class="sxs-lookup"><span data-stu-id="47b5f-267">However, now that you are using the Bootstrap CSS framework to create a responsive web design, go head and remove these mobile-specific views and the mobile-specific layout views.</span></span> <span data-ttu-id="47b5f-268">Ensuite, le navigateur mobile actualisé affichera le style Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="47b5f-268">Once you have done so, the refreshed mobile browser will show the Bootstrap styling.</span></span>
> 
> 

## <span data-ttu-id="47b5f-269"><a name="bkmk_improvedates"></a> Amélioration de la liste Dates</span><span class="sxs-lookup"><span data-stu-id="47b5f-269"><a name="bkmk_improvedates"></a> Improve the Dates List</span></span>
<span data-ttu-id="47b5f-270">Vous pouvez optimiser la vue *Dates* de la même façon que vous l’avez fait avec les vues *Speakers* et *Tags*. Vous devez utiliser les modifications de code décrites plus haut mais en suivant la syntaxe de méthode suivante `Html.ActionLink` dans *Views\\Home\\AllDates.cshtml* :</span><span class="sxs-lookup"><span data-stu-id="47b5f-270">You can improve the *Dates* view like you improved the *Speakers* and *Tags* views if you use the code changes described earlier, but with the following `Html.ActionLink` method syntax in *Views\\Home\\AllDates.cshtml*:</span></span>

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="47b5f-271">La vue du navigateur mobile actualisé se présente ainsi :</span><span class="sxs-lookup"><span data-stu-id="47b5f-271">You will get a refreshed mobile browser view like this:</span></span>

![][AllDatesFixed]

<span data-ttu-id="47b5f-272">Vous pouvez encore optimiser la vue *Dates* en classant les valeurs date-heure par date.</span><span class="sxs-lookup"><span data-stu-id="47b5f-272">You can further improve the *Dates* view by organizing the date-time values by date.</span></span> <span data-ttu-id="47b5f-273">Pour ce faire, vous pouvez utiliser le style [panels][panels] Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="47b5f-273">This can be done with the Bootstrap [panels][panels] styling.</span></span> <span data-ttu-id="47b5f-274">Remplacez le contenu du fichier *Views\\Home\\AllDates.cshtml* par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="47b5f-274">Replace the contents of the *Views\\Home\\AllDates.cshtml* file with the following code:</span></span>

    @model IEnumerable<DateTime>

    @{
        ViewBag.Title = "All Dates";
    }

    <h2>Dates</h2>

    @foreach (var dategroup in Model.GroupBy(x=>x.Date))
    {
        <div class="panel panel-primary">
            <div class="panel-heading">
                @dategroup.Key.ToString("ddd, MMM dd")
            </div>
            <div class="panel-body list-group">
                @foreach (var date in dategroup)
                {
                    @Html.ActionLink(date.ToString("h:mm tt"), 
                                     "SessionsByDate", 
                                     new { date }, 
                                     new { @class = "list-group-item" })
                }
            </div>
        </div>
    }

<span data-ttu-id="47b5f-275">Ce code crée une balise `<div class="panel panel-primary">` distincte pour chaque date de la liste et utilise le style [linked list group][linked list group] pour les liens respectifs, comme avant.</span><span class="sxs-lookup"><span data-stu-id="47b5f-275">This code creates a separate `<div class="panel panel-primary">` tag for each distinct date in the list, and uses the [linked list group][linked list group] for the respective links as before.</span></span> <span data-ttu-id="47b5f-276">Voici à quoi le navigateur mobile ressemble lorsque ce code est exécuté :</span><span class="sxs-lookup"><span data-stu-id="47b5f-276">Here's what the mobile browser looks like when this code runs:</span></span>

![][AllDatesFixed2]

<span data-ttu-id="47b5f-277">Basculez vers le navigateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="47b5f-277">Switch to the desktop browser.</span></span> <span data-ttu-id="47b5f-278">Remarquez l'aspect cohérent.</span><span class="sxs-lookup"><span data-stu-id="47b5f-278">Again, note the consistent look.</span></span>

![][AllDatesFixed2Desktop]

## <span data-ttu-id="47b5f-279"><a name="bkmk_improvesessionstable"></a> Amélioration de la vue SessionsTable</span><span class="sxs-lookup"><span data-stu-id="47b5f-279"><a name="bkmk_improvesessionstable"></a> Improve the SessionsTable View</span></span>
<span data-ttu-id="47b5f-280">Dans cette section, vous allez faire en sorte que la vue *SessionsTable* soit mieux adaptée aux appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="47b5f-280">In this section, you'll make the *SessionsTable* view more mobile-friendly.</span></span> <span data-ttu-id="47b5f-281">Cette modification est plus importante que les précédentes.</span><span class="sxs-lookup"><span data-stu-id="47b5f-281">This change is more extensive the previous changes.</span></span>

<span data-ttu-id="47b5f-282">Dans le navigateur mobile, appuyez sur le bouton **Balise**, puis entrez `asp` dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="47b5f-282">In the mobile browser, tap the **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="47b5f-283">Appuyez sur le lien **ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="47b5f-283">Tap the **ASP.NET** link.</span></span>

![][SessionsTableTagASP.NET]

<span data-ttu-id="47b5f-284">Comme vous pouvez le constater, l’affichage se fait sous forme de tableau, actuellement conçu pour être affiché sur le navigateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="47b5f-284">As you can see, the display is formatted as a table, which is currently designed to be viewed in the desktop browser.</span></span> <span data-ttu-id="47b5f-285">Malheureusement, ce type d'affichage n'est pas adapté à un navigateur mobile.</span><span class="sxs-lookup"><span data-stu-id="47b5f-285">However, it's a little bit difficult to read on a mobile browser.</span></span> <span data-ttu-id="47b5f-286">Pour remédier au problème, ouvrez le fichier *Views\\Home\\SessionsTable.cshtml* et remplacez son contenu par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="47b5f-286">To fix this, open *Views\\Home\\SessionsTable.cshtml* and then replace the contents of the file with the following code:</span></span>

    @model IEnumerable<Mvc5Mobile.Models.Session>

    <h2>@ViewBag.Title</h2>

    <div class="container">
        <div class="row">
            @foreach (var session in Model)
            {
                <div class="col-md-4">
                    <div class="list-group">
                        @Html.ActionLink(session.Title, 
                                         "SessionByCode", 
                                         new { session.Code }, 
                                         new { @class="list-group-item active" })
                        <div class="list-group-item">
                            <div class="list-group-item-text">
                                @Html.Partial("_SpeakersLinks", session)
                            </div>
                            <div class="list-group-item-info">
                                @session.DateText
                            </div>
                            <div class="list-group-item-info small hidden-xs">
                                @Html.Partial("_TagsLinks", session)
                            </div>
                        </div>
                    </div>
                </div>
            }
        </div>
    </div>

<span data-ttu-id="47b5f-287">Le code se compose de trois étapes :</span><span class="sxs-lookup"><span data-stu-id="47b5f-287">The code does 3 things:</span></span>

* <span data-ttu-id="47b5f-288">Il utilise le style [custom linked list group][custom linked list group] Bootstrap pour mettre en forme les informations de session de façon verticale. Ainsi, toutes ces informations sont lisibles sur un navigateur mobile (à l’aide de classes telles que list-group-item-text).</span><span class="sxs-lookup"><span data-stu-id="47b5f-288">uses the Bootstrap [custom linked list group][custom linked list group] to format the session information vertically, so that all this information is readable on a mobile browser (using classes such as list-group-item-text)</span></span>
* <span data-ttu-id="47b5f-289">Il applique le [système de grille][grid system] à la disposition, afin que les éléments de session s’affichent à l’horizontale dans le navigateur de bureau et à la verticale dans le navigateur mobile (à l’aide de la classe col-md-4).</span><span class="sxs-lookup"><span data-stu-id="47b5f-289">applies the [grid system][grid system] to the layout, so that the session items flow horizontally in the desktop browser and vertically in the mobile browser (using the col-md-4 class)</span></span>
* <span data-ttu-id="47b5f-290">Il utilise les [utilitaires réactifs][responsive utilities] pour masquer les balises de session lorsqu’elles s’affichent dans le navigateur mobile (à l’aide de la classe hidden-xs).</span><span class="sxs-lookup"><span data-stu-id="47b5f-290">uses the [responsive utilities][responsive utilities] to hide the session tags when viewed in the mobile browser (using the hidden-xs class)</span></span>

<span data-ttu-id="47b5f-291">Vous pouvez aussi appuyer sur le lien d'un titre pour accéder à la session associée.</span><span class="sxs-lookup"><span data-stu-id="47b5f-291">You can also tap a title link to go to the respective session.</span></span> <span data-ttu-id="47b5f-292">L'image qui suit reflète les changements réalisés à l'aide du code.</span><span class="sxs-lookup"><span data-stu-id="47b5f-292">The image below reflects the code changes.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="47b5f-293">Le système de grille Bootstrap que vous avez automatiquement appliqué permet d’organiser les sessions à la verticale dans le navigateur mobile.</span><span class="sxs-lookup"><span data-stu-id="47b5f-293">The Bootstrap grid system that you applied automatically arranges the sessions vertically in the mobile browser.</span></span> <span data-ttu-id="47b5f-294">En outre, vous remarquerez que les balises ne s'affichent pas.</span><span class="sxs-lookup"><span data-stu-id="47b5f-294">Also, notice that the tags are not shown.</span></span> <span data-ttu-id="47b5f-295">Basculez vers le navigateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="47b5f-295">Switch to the desktop browser.</span></span>

![][SessionsTableFixedTagASP.NETDesktop]

<span data-ttu-id="47b5f-296">Dans le navigateur de bureau, vous remarquez que les balises s'affichent désormais.</span><span class="sxs-lookup"><span data-stu-id="47b5f-296">In the desktop browser, notice that the tags are now displayed.</span></span> <span data-ttu-id="47b5f-297">De même, vous pouvez constater que le système de grille Bootstrap que vous avez appliqué classe les éléments de session en deux colonnes.</span><span class="sxs-lookup"><span data-stu-id="47b5f-297">Also, you can see that the Bootstrap grid system you applied arranges the session items in two columns.</span></span> <span data-ttu-id="47b5f-298">Si vous agrandissez le navigateur, l’organisation s’étend sur trois colonnes.</span><span class="sxs-lookup"><span data-stu-id="47b5f-298">If you enlarge the browser, you will see that the arrangement changes to three columns.</span></span>

## <span data-ttu-id="47b5f-299"><a name="bkmk_improvesessionbycode"></a> Amélioration de la vue SessionByCode</span><span class="sxs-lookup"><span data-stu-id="47b5f-299"><a name="bkmk_improvesessionbycode"></a> Improve the SessionByCode View</span></span>
<span data-ttu-id="47b5f-300">Dernière étape, vous allez optimiser la vue *SessionByCode* pour l'adapter aux périphériques mobiles.</span><span class="sxs-lookup"><span data-stu-id="47b5f-300">Finally, you'll fix the *SessionByCode* view to make it mobile-friendly.</span></span>

<span data-ttu-id="47b5f-301">Dans le navigateur mobile, appuyez sur le bouton **Balise**, puis entrez `asp` dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="47b5f-301">In the mobile browser, tap the **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="47b5f-302">Appuyez sur le lien **ASP.NET** .</span><span class="sxs-lookup"><span data-stu-id="47b5f-302">Tap the **ASP.NET** link.</span></span> <span data-ttu-id="47b5f-303">Les sessions de balise ASP.NET s'affichent.</span><span class="sxs-lookup"><span data-stu-id="47b5f-303">Sessions for the ASP.NET tag are displayed.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="47b5f-304">Cliquez sur le lien **Conception d’une application à page unique avec ASP.NET et AngularJS** .</span><span class="sxs-lookup"><span data-stu-id="47b5f-304">Choose the **Building a Single Page Application with ASP.NET and AngularJS** link.</span></span>

![][SessionByCode3-644]

<span data-ttu-id="47b5f-305">Si la vue bureau par défaut convient tout à fait, vous pouvez facilement améliorer son aspect à l'aide des composants d'interface graphique Bootstrap.</span><span class="sxs-lookup"><span data-stu-id="47b5f-305">The default desktop view is fine, but you can improve the look easily by using some Bootstrap GUI components.</span></span>

<span data-ttu-id="47b5f-306">Ouvrez le fichier *Views\\Home\\SessionByCode.cshtml* et remplacez le contenu par le balisage suivant :</span><span class="sxs-lookup"><span data-stu-id="47b5f-306">Open *Views\\Home\\SessionByCode.cshtml* and replace the contents with the following markup:</span></span>

    @model Mvc5Mobile.Models.Session

    @{
        ViewBag.Title = "Session details";
    }
    <h3>@Model.Title (@Model.Code)</h3>
    <p>
        <strong>@Model.DateText</strong> in <strong>@Model.Room</strong>
    </p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Speakers
        </div>
        @foreach (var speaker in Model.Speakers)
        {
            @Html.ActionLink(speaker, 
                             "SessionsBySpeaker", 
                             new { speaker }, 
                             new { @class="panel-body" })
        }
    </div>

    <p>@Model.Abstract</p>

    <div class="panel panel-primary">
        <div class="panel-heading">
            Tags
        </div>
        @foreach (var tag in Model.Tags)
        {
            @Html.ActionLink(tag, 
                             "SessionsByTag", 
                             new { tag }, 
                             new { @class = "panel-body" })
        }
    </div>

<span data-ttu-id="47b5f-307">Le nouveau balisage utilise le style de volets Bootstrap pour optimiser la vue mobile.</span><span class="sxs-lookup"><span data-stu-id="47b5f-307">The new markup uses Bootstrap panels styling to improve the mobile view.</span></span> 

<span data-ttu-id="47b5f-308">Actualisez le navigateur mobile.</span><span class="sxs-lookup"><span data-stu-id="47b5f-308">Refresh the mobile browser.</span></span> <span data-ttu-id="47b5f-309">L'image suivante reflète les changements que vous venez de réaliser à l'aide du code :</span><span class="sxs-lookup"><span data-stu-id="47b5f-309">The following image reflects the code changes that you just made:</span></span>

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a><span data-ttu-id="47b5f-310">Conclusion</span><span class="sxs-lookup"><span data-stu-id="47b5f-310">Wrap Up and Review</span></span>
<span data-ttu-id="47b5f-311">Ce didacticiel vous a guidé dans l’utilisation d’ASP.NET MVC 5 pour développer des applications web adaptées aux appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="47b5f-311">This tutorial has shown you how to use ASP.NET MVC 5 to develop mobile-friendly Web applications.</span></span> <span data-ttu-id="47b5f-312">Vous avez notamment vu les points suivants :</span><span class="sxs-lookup"><span data-stu-id="47b5f-312">These include:</span></span>

* <span data-ttu-id="47b5f-313">Déployer une application ASP.NET MVC 5 dans une application web d’App Service</span><span class="sxs-lookup"><span data-stu-id="47b5f-313">Deploy an ASP.NET MVC 5 application to an App Service web app</span></span>
* <span data-ttu-id="47b5f-314">Utiliser Bootstrap pour créer une disposition web réactive dans votre application MVC 5</span><span class="sxs-lookup"><span data-stu-id="47b5f-314">Use Bootstrap to create responsive web layout in your MVC 5 application</span></span>
* <span data-ttu-id="47b5f-315">Remplacer la disposition, les vues, les vues partielles, de façon globale ou pour une vue spécifique</span><span class="sxs-lookup"><span data-stu-id="47b5f-315">Override layout, views, and partial views, both globally and for an individual view</span></span>
* <span data-ttu-id="47b5f-316">Contrôler la disposition et l’application de remplacement partiel à l’aide de la propriété `RequireConsistentDisplayMode`</span><span class="sxs-lookup"><span data-stu-id="47b5f-316">Control layout and partial override enforcement using the `RequireConsistentDisplayMode` property</span></span>
* <span data-ttu-id="47b5f-317">Créer des vues ciblant des navigateurs spécifiques, comme celui de l’iPhone</span><span class="sxs-lookup"><span data-stu-id="47b5f-317">Create views that target specific browsers, such as the iPhone browser</span></span>
* <span data-ttu-id="47b5f-318">Appliquer des styles Bootstrap dans le code Razor</span><span class="sxs-lookup"><span data-stu-id="47b5f-318">Apply Bootstrap styling in Razor code</span></span>

## <a name="see-also"></a><span data-ttu-id="47b5f-319">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="47b5f-319">See Also</span></span>
* [<span data-ttu-id="47b5f-320">9 principes de base de la conception web réactive (en anglais)</span><span class="sxs-lookup"><span data-stu-id="47b5f-320">9 basic principles of responsive web design</span></span>](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* <span data-ttu-id="47b5f-321">[Bootstrap][BootstrapSite]</span><span class="sxs-lookup"><span data-stu-id="47b5f-321">[Bootstrap][BootstrapSite]</span></span>
* <span data-ttu-id="47b5f-322">[Blog Bootstrap officiel (en anglais)][Official Bootstrap Blog]</span><span class="sxs-lookup"><span data-stu-id="47b5f-322">[Official Bootstrap Blog][Official Bootstrap Blog]</span></span>
* <span data-ttu-id="47b5f-323">[Tutoriel Bootstrap Twitter de Tutorial Republic (en anglais)][Twitter Bootstrap Tutorial from Tutorial Republic]</span><span class="sxs-lookup"><span data-stu-id="47b5f-323">[Twitter Bootstrap Tutorial from Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span></span>
* <span data-ttu-id="47b5f-324">[The Bootstrap Playground (en anglais)][The Bootstrap Playground]</span><span class="sxs-lookup"><span data-stu-id="47b5f-324">[The Bootstrap Playground][The Bootstrap Playground]</span></span>
* <span data-ttu-id="47b5f-325">[Bonnes pratiques pour les applications web mobiles des recommandations W3C (en anglais)][W3C Recommendation Mobile Web Application Best Practices]</span><span class="sxs-lookup"><span data-stu-id="47b5f-325">[W3C Recommendation Mobile Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span></span>
* <span data-ttu-id="47b5f-326">[Candidat à la recommandation du W3C concernant les requêtes de média (en anglais)][W3C Candidate Recommendation for media queries]</span><span class="sxs-lookup"><span data-stu-id="47b5f-326">[W3C Candidate Recommendation for media queries][W3C Candidate Recommendation for media queries]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="47b5f-327">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="47b5f-327">What's changed</span></span>
* <span data-ttu-id="47b5f-328">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="47b5f-328">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- Internal Links -->
[Deploy the starter project to an Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override the Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve the Speakers List]: #bkmk_Improvespeakerslist
[Improve the Tags List]: #bkmk_improvetags
[Improve the Dates List]: #bkmk_improvedates
[Improve the SessionsTable View]: #bkmk_improvesessionstable
[Improve the SessionByCode View]: #bkmk_improvesessionbycode

<!-- External Links -->
[Visual Studio Express 2013]: http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-web
[Visual Studio 2015]: https://www.visualstudio.com/downloads/download-visual-studio-vs
[AzureSDKVs2013]: http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409
[Fiddler]: http://www.fiddler2.com/fiddler2/
[EmulatorIE11]: http://msdn.microsoft.com/library/ie/dn255001.aspx
[EmulatorChrome]: https://developers.google.com/chrome-developer-tools/docs/mobile-emulation
[EmulatorOpera]: http://www.opera.com/developer/tools/mobile/
[StarterProject]: http://go.microsoft.com/fwlink/?LinkID=398780&clcid=0x409
[CompletedProject]: http://go.microsoft.com/fwlink/?LinkID=398781&clcid=0x409
[BootstrapSite]: http://getbootstrap.com/
[WebPIAzureSdk23NetVS13]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/WebPIAzureSdk23NetVS13.png
[linked list group]: http://getbootstrap.com/components/#list-group-linked
[glyphicon]: http://getbootstrap.com/components/#glyphicons
[panels]: http://getbootstrap.com/components/#panels
[custom linked list group]: http://getbootstrap.com/components/#list-group-custom-content
[grid system]: http://getbootstrap.com/css/#grid
[responsive utilities]: http://getbootstrap.com/css/#responsive-utilities
[Official Bootstrap Blog]: http://blog.getbootstrap.com/
[Twitter Bootstrap Tutorial from Tutorial Republic]: http://www.tutorialrepublic.com/twitter-bootstrap-tutorial/
[The Bootstrap Playground]: http://www.bootply.com/
[W3C Recommendation Mobile Web Application Best Practices]: http://www.w3.org/TR/mwabp/
[W3C Candidate Recommendation for media queries]: http://www.w3.org/TR/css3-mediaqueries/

<!-- Images -->
[DeployClickPublish]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-1.png
[DeployClickWebSites]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-2.png
[DeploySignIn]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-3.png
[DeployUsername]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-4.png
[DeployPassword]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-5.png
[DeployNewWebsite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-6.png
[DeploySiteSettings]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7.png
[DeployPublishSite]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-8.png
[MobileHomePage]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/mobile-home-page.png
[FixedSessionsByTag]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-Fixed.png
[AllTags]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags.png
[SessionsByTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET.png
[SessionsByTagASP.NETNoBootstrap]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsByTag-ASP.NET-NoBootstrap.png
[AllTagsMobile_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile.png
[AllTagsMobile_LayoutMobileDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsMobile-_LayoutMobile-Desktop.png
[ResolveDefaultDisplayMode]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/Resolve-DefaultDisplayMode.png
[AllTagsIPhone_LayoutIPhone]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTagsIPhone-_LayoutIPhone.png
[AllSpeakers_LayoutMobile]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile.png
[AllSpeakers_LayoutMobileOverridden]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-_LayoutMobile-Overridden.png
[AllSpeakersFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed.png
[AllSpeakersFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-Desktop.png
[AllSpeakersFixedSearchBySC]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllSpeakers-Fixed-SearchBySC.png
[AllTagsFixedDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-Desktop.png 
[AllTagsFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed.png
[AllDatesFixed]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed.png
[AllDatesFixed2]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2.png
[AllDatesFixed2Desktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllDates-Fixed2-Desktop.png
[AllTagsFixedSearchByASP]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/AllTags-Fixed-SearchByASP.png
[SessionsTableTagASP.NET]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Tag-ASP.NET.png
[SessionsTableFixedTagASP.NETDesktop]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionsTable-Fixed-Tag-ASP.NET-Desktop.png
[SessionByCode3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-3-644.png
[SessionByCodeFixed3-644]: ./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/SessionByCode-Fixed-3-644.png

