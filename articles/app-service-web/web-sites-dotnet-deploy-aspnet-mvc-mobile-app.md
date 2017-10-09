---
title: "application web mobile d’aaaDeploy un ASP.NET MVC 5 dans Azure App Service"
description: "Un didacticiel vous apprend comment toodeploy un tooAzure d’application web du Service d’applications à l’aide de mobile fonctionnalités dans ASP.NET MVC 5 application web."
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
ms.openlocfilehash: 01119c07246c0252fd357562774a2e90b3ef77d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-aspnet-mvc-5-mobile-web-app-in-azure-app-service"></a><span data-ttu-id="05655-103">Déployer une application web mobile ASP.NET MVC 5 dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="05655-103">Deploy an ASP.NET MVC 5 mobile web app in Azure App Service</span></span>
<span data-ttu-id="05655-104">Ce didacticiel vous hello notions de base de comment toobuild un ASP.NET MVC 5 web application adaptés aux appareils mobiles et le déployer tooAzure du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="05655-104">This tutorial will teach you hello basics of how toobuild an ASP.NET MVC 5 web app that is mobile-friendly and deploy it tooAzure App Service.</span></span> <span data-ttu-id="05655-105">Pour ce didacticiel, vous devez [Visual Studio Express 2013 pour le Web] [ Visual Studio Express 2013] hello éditions ou professional de Visual Studio si vous l’avez déjà.</span><span class="sxs-lookup"><span data-stu-id="05655-105">For this tutorial, you need [Visual Studio Express 2013 for Web][Visual Studio Express 2013] or hello professional edition of Visual Studio if you already have that.</span></span> <span data-ttu-id="05655-106">Vous pouvez utiliser [Visual Studio 2015] mais captures d’écran hello sera différentes, et vous devez utiliser des modèles de hello ASP.NET 4.x.</span><span class="sxs-lookup"><span data-stu-id="05655-106">You can use [Visual Studio 2015] but hello screen shots will be different and you must use hello ASP.NET 4.x templates.</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="what-youll-build"></a><span data-ttu-id="05655-107">Contenu</span><span class="sxs-lookup"><span data-stu-id="05655-107">What You'll Build</span></span>
<span data-ttu-id="05655-108">Pour ce didacticiel, vous allez ajouter des fonctionnalités mobiles toohello annonce de conférence application simple qui est fournie dans hello [projet de démarrage][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="05655-108">For this tutorial, you'll add mobile features toohello simple conference-listing application that's provided in hello [starter project][StarterProject].</span></span> <span data-ttu-id="05655-109">Hello capture d’écran suivante montre les sessions ASP.NET hello dans hello terminée application, comme indiqué dans l’émulateur de navigateur hello dans les outils de développement Internet Explorer 11 F12.</span><span class="sxs-lookup"><span data-stu-id="05655-109">hello following screenshot shows hello ASP.NET sessions in hello completed application, as seen in hello browser emulator in Internet Explorer 11 F12 developer tools.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="05655-110">Vous pouvez utiliser les outils de développement hello Internet Explorer 11 F12 et hello [outil Fiddler] [ Fiddler] toohelp déboguer votre application.</span><span class="sxs-lookup"><span data-stu-id="05655-110">You can use hello Internet Explorer 11 F12 developer tools and hello [Fiddler tool][Fiddler] toohelp debug your application.</span></span> 

## <a name="skills-youll-learn"></a><span data-ttu-id="05655-111">Compétences</span><span class="sxs-lookup"><span data-stu-id="05655-111">Skills You'll Learn</span></span>
<span data-ttu-id="05655-112">Vous apprendrez les compétences suivantes :</span><span class="sxs-lookup"><span data-stu-id="05655-112">Here's what you'll learn:</span></span>

* <span data-ttu-id="05655-113">Comment toouse Visual Studio 2013 toopublish votre application web directement tooa web application dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="05655-113">How toouse Visual Studio 2013 toopublish your web application directly tooa web app in Azure App Service.</span></span>
* <span data-ttu-id="05655-114">Utilisent des modèles de hello ASP.NET MVC 5 framework du programme d’amorçage CSS hello pour améliorer l’affichage sur les périphériques mobiles</span><span class="sxs-lookup"><span data-stu-id="05655-114">How hello ASP.NET MVC 5 templates use hello CSS Bootstrap framework to improve display on mobile devices</span></span>
* <span data-ttu-id="05655-115">Comment toocreate mobiles spécifiques vues tootarget certains navigateurs mobiles, tels que les iPhone hello et Android</span><span class="sxs-lookup"><span data-stu-id="05655-115">How toocreate mobile-specific views tootarget specific mobile browsers, such as hello iPhone and Android</span></span>
* <span data-ttu-id="05655-116">Comment toocreate les vues réactive (vues qui répondent toodifferent navigateurs pour les appareils)</span><span class="sxs-lookup"><span data-stu-id="05655-116">How toocreate responsive views (views that respond toodifferent browsers across devices)</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="05655-117">Configuration d’environnement de développement hello</span><span class="sxs-lookup"><span data-stu-id="05655-117">Set up hello development environment</span></span>
<span data-ttu-id="05655-118">Configurer votre environnement de développement en installant hello Azure SDK pour .NET 2.5.1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="05655-118">Set up your development environment by installing hello Azure SDK for .NET 2.5.1 or later.</span></span> 

1. <span data-ttu-id="05655-119">tooinstall hello Azure SDK pour .NET, cliquez sur lien hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="05655-119">tooinstall hello Azure SDK for .NET, click hello link below.</span></span> <span data-ttu-id="05655-120">Si vous n’avez pas encore installé de Visual Studio 2013, il sera installé par un lien de hello.</span><span class="sxs-lookup"><span data-stu-id="05655-120">If you don't have Visual Studio 2013 installed yet, it will be installed by hello link.</span></span> <span data-ttu-id="05655-121">Ce didacticiel requiert Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="05655-121">This tutorial requires Visual Studio 2013.</span></span> <span data-ttu-id="05655-122">[Kit de développement logiciel (SDK) Azure pour Visual Studio 2013][AzureSDKVs2013]</span><span class="sxs-lookup"><span data-stu-id="05655-122">[Azure SDK for Visual Studio 2013][AzureSDKVs2013]</span></span>
2. <span data-ttu-id="05655-123">Dans la fenêtre de Web Platform Installer hello, cliquez sur **installer** et poursuivre l’installation de hello.</span><span class="sxs-lookup"><span data-stu-id="05655-123">In hello Web Platform Installer window, click **Install** and proceed with hello installation.</span></span>

<span data-ttu-id="05655-124">Vous aurez également besoin d'un émulateur de navigateur mobile.</span><span class="sxs-lookup"><span data-stu-id="05655-124">You will also need a mobile browser emulator.</span></span> <span data-ttu-id="05655-125">Hello suivantes ne fonctionnent pas :</span><span class="sxs-lookup"><span data-stu-id="05655-125">Any of hello following will work:</span></span>

* <span data-ttu-id="05655-126">Émulateur de navigateur dans les [outils de développement F12 d’Internet Explorer 11][EmulatorIE11] (utilisés dans toutes les captures d’écran de navigateurs mobiles).</span><span class="sxs-lookup"><span data-stu-id="05655-126">Browser Emulator in [Internet Explorer 11 F12 developer tools][EmulatorIE11] (used in all mobile browser screenshots).</span></span> <span data-ttu-id="05655-127">Il dispose de présélections de chaîne d'agent utilisateur pour Windows Phone 8, Windows Phone 7 et l'iPad d'Apple.</span><span class="sxs-lookup"><span data-stu-id="05655-127">It has user agent string presets for Windows Phone 8, Windows Phone 7, and Apple iPad.</span></span>
* <span data-ttu-id="05655-128">Émulateur de navigateur de [Google Chrome DevTools][EmulatorChrome].</span><span class="sxs-lookup"><span data-stu-id="05655-128">Browser Emulator in [Google Chrome DevTools][EmulatorChrome].</span></span> <span data-ttu-id="05655-129">Il inclut des présélections pour de nombreux périphériques Android, ainsi que pour l'iPhone d'Apple, l'iPad d'Apple et le Kindle Fire d'Amazon.</span><span class="sxs-lookup"><span data-stu-id="05655-129">It contains presets for numerous Android devices, as well as Apple iPhone, Apple iPad, and Amazon Kindle Fire.</span></span> <span data-ttu-id="05655-130">Il émule également des événements tactiles.</span><span class="sxs-lookup"><span data-stu-id="05655-130">It also emulates touch events.</span></span>
* <span data-ttu-id="05655-131">[Émulateur mobile Opera][EmulatorOpera]</span><span class="sxs-lookup"><span data-stu-id="05655-131">[Opera Mobile Emulator][EmulatorOpera]</span></span>

<span data-ttu-id="05655-132">Les projets Visual Studio avec C\# code source est disponible tooaccompany cette rubrique :</span><span class="sxs-lookup"><span data-stu-id="05655-132">Visual Studio projects with C\# source code are available tooaccompany this topic:</span></span>

* <span data-ttu-id="05655-133">[Téléchargement du projet de départ][StarterProject]</span><span class="sxs-lookup"><span data-stu-id="05655-133">[Starter project download][StarterProject]</span></span>
* <span data-ttu-id="05655-134">[Téléchargement du projet terminé][CompletedProject]</span><span class="sxs-lookup"><span data-stu-id="05655-134">[Completed project download][CompletedProject]</span></span>

## <span data-ttu-id="05655-135"><a name="bkmk_DeployStarterProject"></a>Déployer le projet hello starter tooan l’application web Azure</span><span class="sxs-lookup"><span data-stu-id="05655-135"><a name="bkmk_DeployStarterProject"></a>Deploy hello starter project tooan Azure web app</span></span>
1. <span data-ttu-id="05655-136">Télécharger l’application de liste de conférence hello [projet de démarrage][StarterProject].</span><span class="sxs-lookup"><span data-stu-id="05655-136">Download hello conference-listing application [starter project][StarterProject].</span></span>
2. <span data-ttu-id="05655-137">Dans l’Explorateur Windows, fichier ZIP de hello téléchargé avec le bouton droit, puis choisissez *propriétés*.</span><span class="sxs-lookup"><span data-stu-id="05655-137">Then in Windows Explorer, right-click hello downloaded ZIP file and choose *Properties*.</span></span>
3. <span data-ttu-id="05655-138">Bonjour **propriétés** boîte de dialogue, choisissez hello **Unblock** bouton.</span><span class="sxs-lookup"><span data-stu-id="05655-138">In hello **Properties** dialog box, choose hello **Unblock** button.</span></span> <span data-ttu-id="05655-139">(Le déblocage empêche un avertissement de sécurité qui se produit lorsque vous essayez de toouse un *.zip* fichier que vous avez téléchargé à partir du web de hello.)</span><span class="sxs-lookup"><span data-stu-id="05655-139">(Unblocking prevents a security warning that occurs when you try toouse a *.zip* file that you've downloaded from hello web.)</span></span>
4. <span data-ttu-id="05655-140">Cliquez sur le fichier ZIP de hello et sélectionnez **extraire tout** afin de décompresser le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="05655-140">Right-click hello ZIP file and select **Extract All** to unzip hello file.</span></span> 
5. <span data-ttu-id="05655-141">Dans Visual Studio, ouvrez hello *C#\Mvc5Mobile.sln* fichier.</span><span class="sxs-lookup"><span data-stu-id="05655-141">In Visual Studio, open hello *C#\Mvc5Mobile.sln* file.</span></span>
6. <span data-ttu-id="05655-142">Dans l’Explorateur de solutions, cliquez sur projet de hello, sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="05655-142">In Solution Explorer, right-click hello project and click **Publish**.</span></span>
   
   ![][DeployClickPublish]
7. <span data-ttu-id="05655-143">Dans Publier le site web, cliquez sur **Microsoft Azure App Service**.</span><span class="sxs-lookup"><span data-stu-id="05655-143">In Publish Web, click **Microsoft Azure App Service**.</span></span>
   
   ![][DeployClickWebSites]
8. <span data-ttu-id="05655-144">Si vous n’êtes pas déjà connecté à Azure, cliquez sur **Ajouter un compte**.</span><span class="sxs-lookup"><span data-stu-id="05655-144">If you haven't already logged into Azure, click **Add an account**.</span></span>
   
   ![][DeploySignIn]
9. <span data-ttu-id="05655-145">Suivez hello invites toolog à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="05655-145">Follow hello prompts toolog into your Azure account.</span></span>
10. <span data-ttu-id="05655-146">Hello, boîte de dialogue du Service d’applications doit maintenant afficher comme connecté.</span><span class="sxs-lookup"><span data-stu-id="05655-146">hello App Service dialog should now show you as signed in.</span></span> <span data-ttu-id="05655-147">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="05655-147">Click **New**.</span></span>
    
    ![][DeployNewWebsite]  
11. <span data-ttu-id="05655-148">Bonjour **nom de l’application Web** Indiquez un préfixe de nom d’application unique.</span><span class="sxs-lookup"><span data-stu-id="05655-148">In hello **Web App Name** field, specify a unique app name prefix.</span></span> <span data-ttu-id="05655-149">Le nom complet de votre application web est *&lt;prefix>*.azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="05655-149">Your fully-qualified web app name will be *&lt;prefix>*.azurewebsites.net.</span></span> <span data-ttu-id="05655-150">Par ailleurs, sélectionnez ou spécifiez un nouveau nom de groupe de ressources dans **Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="05655-150">Also, select or specify a new resource group name in **Resource group**.</span></span> <span data-ttu-id="05655-151">Ensuite, cliquez sur **nouveau** toocreate un nouveau plan de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="05655-151">Then, click **New** toocreate a new App Service plan.</span></span>
    
    ![][DeploySiteSettings]
12. <span data-ttu-id="05655-152">Configurez le nouveau plan de Service de l’application hello, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="05655-152">Configure hello new App Service plan and click **OK**.</span></span> 
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7a.png)
13. <span data-ttu-id="05655-153">Dans la boîte de dialogue Créer un Service application hello, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="05655-153">Back in hello Create App Service dialog, click **Create**.</span></span>
    
    ![](./media/web-sites-dotnet-deploy-aspnet-mvc-mobile-app/deploy-to-azure-website-7b.png) 
14. <span data-ttu-id="05655-154">Une fois hello ressources Azure sont créés, boîte de dialogue Publier le site Web hello est rempli avec des paramètres pour votre nouvelle application hello.</span><span class="sxs-lookup"><span data-stu-id="05655-154">After hello Azure resources are created, hello Publish Web dialog will be filled with hello settings for your new app.</span></span> <span data-ttu-id="05655-155">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="05655-155">Click **Publish**.</span></span>
    
    ![][DeployPublishSite]
    
    <span data-ttu-id="05655-156">Une fois que Visual Studio a terminé l’application de publication toohello hello starter projet web Azure, navigateur de bureau hello ouvre toodisplay hello dynamique web app.</span><span class="sxs-lookup"><span data-stu-id="05655-156">Once Visual Studio finishes publishing hello starter project toohello Azure web app, hello desktop browser opens toodisplay hello live web app.</span></span>
15. <span data-ttu-id="05655-157">Démarrer l’émulateur de votre navigateur mobile, de copier l’URL de hello pour l’application de conférence hello (*<prefix>*. azurewebsites.net) dans l’émulateur de hello, puis cliquez sur le bouton droit et sélectionnez **Parcourir par balise**.</span><span class="sxs-lookup"><span data-stu-id="05655-157">Start your mobile browser emulator, copy hello URL for hello conference application (*<prefix>*.azurewebsites.net) into hello emulator, and then click the top-right button and select **Browse by tag**.</span></span> <span data-ttu-id="05655-158">Si vous utilisez Internet Explorer 11 comme navigateur par défaut de hello, vous devez simplement tootype `F12`, puis `Ctrl+8`, puis modifiez profil de navigateur hello trop**Windows Phone**.</span><span class="sxs-lookup"><span data-stu-id="05655-158">If you are using Internet Explorer 11 as hello default browser, you just need tootype `F12`, then `Ctrl+8`, and then change hello browser profile too**Windows Phone**.</span></span> <span data-ttu-id="05655-159">L’image ci-dessous montre hello *AllTags* affichage en mode portrait (choisisse **Parcourir par balise**).</span><span class="sxs-lookup"><span data-stu-id="05655-159">The image below shows hello *AllTags* view in portrait mode (from choosing **Browse by tag**).</span></span>
    
    ![][AllTags]

> [!TIP]
> <span data-ttu-id="05655-160">Pendant que vous pouvez déboguer votre application MVC 5 à partir de Visual Studio, vous pouvez publier votre tooAzure d’application web à nouveau tooverify hello web dynamique application directement à partir de votre navigateur mobile ou un émulateur de navigateur.</span><span class="sxs-lookup"><span data-stu-id="05655-160">While you can debug your MVC 5 application from within Visual Studio, you can publish your web app tooAzure again tooverify hello live web app directly from your mobile browser or a browser emulator.</span></span>
> 
> 

<span data-ttu-id="05655-161">affichage de Hello est très lisible sur un appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="05655-161">hello display is very readable on a mobile device.</span></span> <span data-ttu-id="05655-162">Vous pouvez également déjà voir certains des effets visuels de hello appliqués par le framework d’amorçage CSS hello.</span><span class="sxs-lookup"><span data-stu-id="05655-162">You can also already see some of hello visual effects applied by hello Bootstrap CSS framework.</span></span>
<span data-ttu-id="05655-163">Cliquez sur hello **ASP.NET** lien.</span><span class="sxs-lookup"><span data-stu-id="05655-163">Click hello **ASP.NET** link.</span></span>

![][SessionsByTagASP.NET]

<span data-ttu-id="05655-164">Hello vue des balises ASP.NET est ajusté de zoom de toohello écran, ce programme d’amorçage fait automatiquement pour vous.</span><span class="sxs-lookup"><span data-stu-id="05655-164">hello ASP.NET tag view is zoom-fitted toohello screen, which Bootstrap does for you automatically.</span></span> <span data-ttu-id="05655-165">Toutefois, vous pouvez améliorer ce navigateur mobile vue toobetter couleur hello.</span><span class="sxs-lookup"><span data-stu-id="05655-165">However, you can improve this view toobetter suit hello mobile browser.</span></span> <span data-ttu-id="05655-166">Par exemple, hello **Date** colonne est difficile à lire.</span><span class="sxs-lookup"><span data-stu-id="05655-166">For example, hello **Date** column is difficult to read.</span></span> <span data-ttu-id="05655-167">Plus loin dans le didacticiel de hello, vous allez modifier hello *AllTags* afficher toomake il adaptés aux appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="05655-167">Later in hello tutorial you'll change hello *AllTags* view toomake it mobile-friendly.</span></span>

## <span data-ttu-id="05655-168"><a name="bkmk_bootstrap"></a> Infrastructure CSS Bootstrap</span><span class="sxs-lookup"><span data-stu-id="05655-168"><a name="bkmk_bootstrap"></a> Bootstrap CSS Framework</span></span>
<span data-ttu-id="05655-169">Nouveauté de hello MVC 5 modèle est prise en charge d’amorçage intégrée.</span><span class="sxs-lookup"><span data-stu-id="05655-169">New in hello MVC 5 template is built-in Bootstrap support.</span></span> <span data-ttu-id="05655-170">Vous avez déjà vu comment il améliore immédiatement hello différentes vues de votre application.</span><span class="sxs-lookup"><span data-stu-id="05655-170">You have already seen how it immediately improves hello different views in your application.</span></span> <span data-ttu-id="05655-171">Par exemple, barre de navigation hello haut hello est réductible automatiquement lors de la largeur du navigateur hello est plus petite.</span><span class="sxs-lookup"><span data-stu-id="05655-171">For example, hello navigation bar at hello top is automatically collapsible when hello browser width is smaller.</span></span> <span data-ttu-id="05655-172">Sur le navigateur de bureau hello, essayez de redimensionner la fenêtre du navigateur hello et voir comment la barre de navigation hello modifie son apparence.</span><span class="sxs-lookup"><span data-stu-id="05655-172">On hello desktop browser, try resizing hello browser window and see how hello navigation bar changes its look and feel.</span></span> <span data-ttu-id="05655-173">Il s’agit de conception web réactive hello qui est intégrée à l’amorçage.</span><span class="sxs-lookup"><span data-stu-id="05655-173">This is hello responsive web design that is built into Bootstrap.</span></span>

<span data-ttu-id="05655-174">toosee comment hello Web app ressemble sans amorçage, ouvrez *application\_Démarrer\\BundleConfig.cs* et commentez les lignes hello contenant *bootstrap.js* et *bootstrap.css*.</span><span class="sxs-lookup"><span data-stu-id="05655-174">toosee how hello Web app would look without Bootstrap, open *App\_Start\\BundleConfig.cs* and comment out hello lines that contain *bootstrap.js* and *bootstrap.css*.</span></span> <span data-ttu-id="05655-175">Hello de code suivant montre hello deux dernières instructions Hello `RegisterBundles` méthode après modification de hello :</span><span class="sxs-lookup"><span data-stu-id="05655-175">hello following code shows hello last two statements of hello `RegisterBundles` method after hello change:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/bootstrap").Include(
              //"~/Scripts/bootstrap.js",
              "~/Scripts/respond.js"));

    bundles.Add(new StyleBundle("~/Content/css").Include(
              //"~/Content/bootstrap.css",
              "~/Content/site.css"));

<span data-ttu-id="05655-176">Appuyez sur `Ctrl+F5` application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="05655-176">Press `Ctrl+F5` toorun hello application.</span></span>

<span data-ttu-id="05655-177">Observez que la barre de navigation réductible hello est maintenant simplement une liste non triée ordinaire.</span><span class="sxs-lookup"><span data-stu-id="05655-177">Observe that hello collapsible navigation bar is now just an ordinary unordered list.</span></span> <span data-ttu-id="05655-178">Cliquez sur **Parcourir par balise** une nouvelle fois, puis cliquez sur **ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="05655-178">Click **Browse by tag** again, then click **ASP.NET**.</span></span>
<span data-ttu-id="05655-179">Dans la vue d’émulateur mobile hello, vous pouvez voir maintenant qu’il n’est plus monté de zoom de toohello écran, et vous devez faire défiler vers le côté en ordre toosee hello à droite de la table de hello.</span><span class="sxs-lookup"><span data-stu-id="05655-179">In hello mobile emulator view, you can see now that it is no longer zoom-fitted toohello screen, and you must scroll sideways in order toosee hello right side of hello table.</span></span>

![][SessionsByTagASP.NETNoBootstrap]

<span data-ttu-id="05655-180">Annuler vos modifications et actualiser hello navigateur mobile tooverify qui hello adaptés aux appareils mobiles affichage a été restaurée.</span><span class="sxs-lookup"><span data-stu-id="05655-180">Undo your changes and refresh hello mobile browser tooverify that hello mobile-friendly display has been restored.</span></span>

<span data-ttu-id="05655-181">Programme d’amorçage n’est pas spécifique tooASP.NET MVC 5, et vous pouvez tirer parti de ces fonctionnalités dans les applications web.</span><span class="sxs-lookup"><span data-stu-id="05655-181">Bootstrap is not specific tooASP.NET MVC 5, and you can take advantage of these features in any web application.</span></span> <span data-ttu-id="05655-182">Désormais, Bootstrap est intégré au modèle de projet ASP.NET MVC 5. Votre application web MVC 5 peut donc tirer parti de Bootstrap par défaut.</span><span class="sxs-lookup"><span data-stu-id="05655-182">But it is now built into the ASP.NET MVC 5 project template, so that your MVC 5 Web application can take advantage of Bootstrap by default.</span></span>

<span data-ttu-id="05655-183">Pour plus d’informations sur les données d’amorçage, consultez toothe [Bootstrap] [ BootstrapSite] site.</span><span class="sxs-lookup"><span data-stu-id="05655-183">For more information about Bootstrap, go toothe [Bootstrap][BootstrapSite] site.</span></span>

<span data-ttu-id="05655-184">Dans la section suivante de hello, vous verrez comment tooprovide des vues spécifiques du navigateur mobile.</span><span class="sxs-lookup"><span data-stu-id="05655-184">In hello next section you'll see how tooprovide mobile-browser specific views.</span></span>

## <span data-ttu-id="05655-185"><a name="bkmk_overrideviews"></a>Remplacer les vues hello, dispositions et les vues partielles</span><span class="sxs-lookup"><span data-stu-id="05655-185"><a name="bkmk_overrideviews"></a> Override hello Views, Layouts, and Partial Views</span></span>
<span data-ttu-id="05655-186">Vous pouvez remplacer toutes les vues (y compris les dispositions et les vues partielles) des navigateurs mobiles en général, mais aussi d’un navigateur mobile particulier ou encore d’un navigateur spécifique.</span><span class="sxs-lookup"><span data-stu-id="05655-186">You can override any view (including layouts and partial views) for mobile browsers in general, for an individual mobile browser, or for any specific browser.</span></span> <span data-ttu-id="05655-187">afficher les tooprovide mobiles spécifiques, vous pouvez copier un fichier de vue et ajouter *. Mobile* toohello nom du fichier.</span><span class="sxs-lookup"><span data-stu-id="05655-187">tooprovide a mobile-specific view, you can copy a view file and add *.Mobile* toohello file name.</span></span> <span data-ttu-id="05655-188">Par exemple, toocreate un mobile *Index* vue, vous pouvez copier *vues\\accueil\\Index.cshtml* à *vues\\accueil\\ Index.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="05655-188">For example, toocreate a mobile *Index* view, you can copy *Views\\Home\\Index.cshtml* to *Views\\Home\\Index.Mobile.cshtml*.</span></span>

<span data-ttu-id="05655-189">Dans cette section, vous allez créer un fichier de disposition mobile.</span><span class="sxs-lookup"><span data-stu-id="05655-189">In this section, you'll create a mobile-specific layout file.</span></span>

<span data-ttu-id="05655-190">toostart, copie *vues\\Shared\\\_Layout.cshtml* à *vues\\Shared\\\_Layout.Mobile.cshtml* .</span><span class="sxs-lookup"><span data-stu-id="05655-190">toostart, copy *Views\\Shared\\\_Layout.cshtml* to *Views\\Shared\\\_Layout.Mobile.cshtml*.</span></span> <span data-ttu-id="05655-191">Ouvrez  *\_Layout.Mobile.cshtml* et remplacez titre hello de **MVC5 Application** trop**MVC5 Application (Mobile)**.</span><span class="sxs-lookup"><span data-stu-id="05655-191">Open *\_Layout.Mobile.cshtml* and change hello title from **MVC5 Application** too**MVC5 Application (Mobile)**.</span></span>

<span data-ttu-id="05655-192">Dans chaque `Html.ActionLink` l’appel pour la barre de navigation hello, supprimez « Parcourir par » dans chaque lien *ActionLink*.</span><span class="sxs-lookup"><span data-stu-id="05655-192">In each `Html.ActionLink` call for hello navigation bar, remove "Browse by" in each link *ActionLink*.</span></span> <span data-ttu-id="05655-193">Hello de code suivant montre hello terminée `<ul class="nav navbar-nav">` balise du fichier de mise en page mobile hello.</span><span class="sxs-lookup"><span data-stu-id="05655-193">hello following code shows hello completed `<ul class="nav navbar-nav">` tag of hello mobile layout file.</span></span>

    <ul class="nav navbar-nav">
        <li>@Html.ActionLink("Home", "Index", "Home")</li>
        <li>@Html.ActionLink("Date", "AllDates", "Home")</li>
        <li>@Html.ActionLink("Speaker", "AllSpeakers", "Home")</li>
        <li>@Html.ActionLink("Tag", "AllTags", "Home")</li>
    </ul>

<span data-ttu-id="05655-194">Hello de copie *vues\\accueil\\AllTags.cshtml* le fichier *vues\\accueil\\AllTags.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="05655-194">Copy hello *Views\\Home\\AllTags.cshtml* file to *Views\\Home\\AllTags.Mobile.cshtml*.</span></span> <span data-ttu-id="05655-195">Ouvrir le nouveau fichier de hello et modifier le `<h2>` élément à partir de « Balises » trop « balises (M) » :</span><span class="sxs-lookup"><span data-stu-id="05655-195">Open hello new file and change the `<h2>` element from "Tags" too"Tags (M)":</span></span>

    <h2>Tags (M)</h2>

<span data-ttu-id="05655-196">Parcourir la page de balises toohello à l’aide d’un navigateur de bureau et à l’aide d’émulateur de navigateur mobile.</span><span class="sxs-lookup"><span data-stu-id="05655-196">Browse toohello tags page using a desktop browser and using mobile browser emulator.</span></span> <span data-ttu-id="05655-197">émulateur de navigateur mobile Hello affiche hello deux modifications (hello titre à partir de  *\_Layout.Mobile.cshtml* et titre hello à partir de *AllTags.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="05655-197">hello mobile browser emulator shows hello two changes you made (hello title from *\_Layout.Mobile.cshtml* and hello title from *AllTags.Mobile.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobile]

<span data-ttu-id="05655-198">En revanche, affichage du bureau hello n’a pas changé (avec un titre de  *\_Layout.cshtml* et *AllTags.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="05655-198">In contrast, hello desktop display has not changed (with titles from *\_Layout.cshtml* and *AllTags.cshtml*).</span></span>

![][AllTagsMobile_LayoutMobileDesktop]

## <span data-ttu-id="05655-199"><a name="bkmk_browserviews"></a> Création de vues spécifiques du navigateur</span><span class="sxs-lookup"><span data-stu-id="05655-199"><a name="bkmk_browserviews"></a> Create Browser-Specific Views</span></span>
<span data-ttu-id="05655-200">En outre toomobile-bureau spécifiques et des vues, vous pouvez créer des vues pour un navigateur individuel.</span><span class="sxs-lookup"><span data-stu-id="05655-200">In addition toomobile-specific and desktop-specific views, you can create views for an individual browser.</span></span> <span data-ttu-id="05655-201">Par exemple, vous pouvez créer des vues qui sont spécifiquement conçus pour hello iPhone ou un navigateur d’Android hello.</span><span class="sxs-lookup"><span data-stu-id="05655-201">For example, you can create views that are specifically for hello iPhone or hello Android browser.</span></span> <span data-ttu-id="05655-202">Dans cette section, vous allez créer une disposition pour le navigateur iPhone qui hello et une version iPhone Hello *AllTags* vue.</span><span class="sxs-lookup"><span data-stu-id="05655-202">In this section, you'll create a layout for hello iPhone browser and an iPhone version of hello *AllTags* view.</span></span>

<span data-ttu-id="05655-203">Ouvrez hello *Global.asax* et ajoutez hello suivant en bas de toohello de code de la `Application_Start` (méthode).</span><span class="sxs-lookup"><span data-stu-id="05655-203">Open hello *Global.asax* file and add hello following code toohello bottom of the `Application_Start` method.</span></span>

    DisplayModeProvider.Instance.Modes.Insert(0, new DefaultDisplayMode("iPhone")
    {
        ContextCondition = (context => context.GetOverriddenUserAgent().IndexOf
            ("iPhone", StringComparison.OrdinalIgnoreCase) >= 0)
    });

<span data-ttu-id="05655-204">Ce code définit un nouveau mode d’affichage appelé « iPhone », qui répondra à chaque demande entrante.</span><span class="sxs-lookup"><span data-stu-id="05655-204">This code defines a new display mode named "iPhone" that will be matched against each incoming request.</span></span> <span data-ttu-id="05655-205">Si la demande entrante de hello correspond à la condition que vous avez défini (autrement dit, si l’agent utilisateur de hello contient la chaîne de hello « iPhone »), ASP.NET MVC recherche pour les vues dont le nom contient le suffixe « iPhone ».</span><span class="sxs-lookup"><span data-stu-id="05655-205">If hello incoming request matches the condition you defined (that is, if hello user agent contains hello string "iPhone"), ASP.NET MVC will look for views whose name contains the "iPhone" suffix.</span></span>

> [!NOTE]
> <span data-ttu-id="05655-206">Lorsque Ajouter spécifiques au navigateur mobile modes d’affichage, telles que pour iPhone et Android, occuper que tooset hello du premier argument trop`0` toomake (insert haut hello de liste de hello) que ce mode de navigateur spécifiques hello est prioritaire sur modèle mobile de hello (*. Mobile.cshtml).</span><span class="sxs-lookup"><span data-stu-id="05655-206">When adding mobile browser-specific display modes, such as for iPhone and Android, be sure tooset hello first argument too`0` (insert at hello top of hello list) toomake sure that hello browser-specific mode takes precedence over hello mobile template (*.Mobile.cshtml).</span></span> <span data-ttu-id="05655-207">Si le modèle mobile de hello est haut hello de liste de hello au lieu de cela, il sera sélectionné sur votre mode d’affichage souhaité (hello première correspondance wins et modèle de mobile hello correspond à tous les navigateurs mobiles).</span><span class="sxs-lookup"><span data-stu-id="05655-207">If hello mobile template is at hello top of hello list instead, it will be selected over your intended display mode (hello first match wins, and hello mobile template matches all mobile browsers).</span></span> 
> 
> 

<span data-ttu-id="05655-208">Dans le code hello, avec le bouton droit `DefaultDisplayMode`, choisissez **résoudre**, puis choisissez `using System.Web.WebPages;`.</span><span class="sxs-lookup"><span data-stu-id="05655-208">In hello code, right-click `DefaultDisplayMode`, choose **Resolve**, and then choose `using System.Web.WebPages;`.</span></span> <span data-ttu-id="05655-209">Cette opération ajoute une référence toothe `System.Web.WebPages` espace de noms qui est l’emplacement où le `DisplayModeProvider` et `DefaultDisplayMode` les types sont définis.</span><span class="sxs-lookup"><span data-stu-id="05655-209">This adds a reference toothe `System.Web.WebPages` namespace, which is where the `DisplayModeProvider` and `DefaultDisplayMode` types are defined.</span></span>

![][ResolveDefaultDisplayMode]

<span data-ttu-id="05655-210">Vous pouvez également ajouter simplement manuellement hello suivant ligne toothe `using` section du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="05655-210">Alternatively, you can just manually add hello following line toothe `using` section of hello file.</span></span>

    using System.Web.WebPages;

<span data-ttu-id="05655-211">Enregistrer les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="05655-211">Save hello changes.</span></span> <span data-ttu-id="05655-212">Copiez le fichier *Views\\Shared\\\_Layout.Mobile.cshtml* vers *Views\\Shared\\\_Layout.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="05655-212">Copy the *Views\\Shared\\\_Layout.Mobile.cshtml* file to *Views\\Shared\\\_Layout.iPhone.cshtml*.</span></span> <span data-ttu-id="05655-213">Ouvrez le nouveau fichier de hello et modifiez titre hello à partir de `MVC5 Application (Mobile)` à `MVC5 Application (iPhone)`.</span><span class="sxs-lookup"><span data-stu-id="05655-213">Open hello new file and then change hello title from `MVC5 Application (Mobile)` to `MVC5 Application (iPhone)`.</span></span>

<span data-ttu-id="05655-214">Hello de copie *vues\\accueil\\AllTags.Mobile.cshtml* le fichier *vues\\accueil\\AllTags.iPhone.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="05655-214">Copy hello *Views\\Home\\AllTags.Mobile.cshtml* file to *Views\\Home\\AllTags.iPhone.cshtml*.</span></span> <span data-ttu-id="05655-215">Dans le nouveau fichier de hello, modifiez hello `<h2>` élément à partir de « balises (M) » » des balises (iPhone) ».</span><span class="sxs-lookup"><span data-stu-id="05655-215">In hello new file, change hello `<h2>` element from "Tags (M)" too"Tags (iPhone)".</span></span>

<span data-ttu-id="05655-216">Exécutez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="05655-216">Run hello application.</span></span> <span data-ttu-id="05655-217">Exécuter un émulateur navigateur mobile, assurez-vous que l’agent utilisateur qui lui est défini trop « iPhone », puis accédez toohello *AllTags* vue.</span><span class="sxs-lookup"><span data-stu-id="05655-217">Run a mobile browser emulator, make sure its user agent is set too"iPhone", and browse toohello *AllTags* view.</span></span> <span data-ttu-id="05655-218">Si vous utilisez un émulateur de hello dans les outils de développement Internet Explorer 11 F12, configurez les éléments suivants de toohello de l’émulation :</span><span class="sxs-lookup"><span data-stu-id="05655-218">If you are using hello emulator in Internet Explorer 11 F12 developer tools, configure emulation toohello following:</span></span>

* <span data-ttu-id="05655-219">Profil du navigateur = **Windows Phone**</span><span class="sxs-lookup"><span data-stu-id="05655-219">Browser profile = **Windows Phone**</span></span>
* <span data-ttu-id="05655-220">Chaîne d’agent utilisateur = **Custom**</span><span class="sxs-lookup"><span data-stu-id="05655-220">User agent string =  **Custom**</span></span>
* <span data-ttu-id="05655-221">Chaîne personnalisée = **Apple-iPhone5C1/1001.525**</span><span class="sxs-lookup"><span data-stu-id="05655-221">Custom string = **Apple-iPhone5C1/1001.525**</span></span>

<span data-ttu-id="05655-222">capture d’écran suivante Hello affiche hello *AllTags* vue dans l’émulateur dans les outils de développement Internet Explorer 11 F12 avec la chaîne d’agent utilisateur hello (il s’agit d’une chaîne d’agent utilisateur iPhone 5 C).</span><span class="sxs-lookup"><span data-stu-id="05655-222">hello following screenshot shows hello *AllTags* view rendered in the emulator in Internet Explorer 11 F12 developer tools with hello custom user agent string (this is an iPhone 5C user agent string).</span></span>

![][AllTagsIPhone_LayoutIPhone]

<span data-ttu-id="05655-223">Dans le navigateur d’appareil mobile hello, sélectionnez hello **haut-parleurs** lien.</span><span class="sxs-lookup"><span data-stu-id="05655-223">In hello mobile browser, select hello **Speakers** link.</span></span> <span data-ttu-id="05655-224">Car il n’est pas un affichage mobile (*AllSpeakers.Mobile.cshtml*), afficher des haut-parleurs par défaut hello (*AllSpeakers.cshtml*) est restitué à l’aide du mode mobile hello ( *\_ Layout.Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="05655-224">Because there's not a mobile view (*AllSpeakers.Mobile.cshtml*), hello default speakers view (*AllSpeakers.cshtml*) is rendered using hello mobile layout view (*\_Layout.Mobile.cshtml*).</span></span> <span data-ttu-id="05655-225">Comme indiqué ci-dessous, titre de hello **MVC5 Application (Mobile)** est défini dans  *\_Layout.Mobile.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="05655-225">As shown below, hello title **MVC5 Application (Mobile)** is defined in *\_Layout.Mobile.cshtml*.</span></span>

![][AllSpeakers_LayoutMobile]

<span data-ttu-id="05655-226">Vous pouvez désactiver globalement d’une vue de (non mobile) par défaut à partir de rendu à l’intérieur d’une disposition mobile en définissant `RequireConsistentDisplayMode` à `true` Bonjour *vues\\\_ViewStart.cshtml* fichier, comme suit :</span><span class="sxs-lookup"><span data-stu-id="05655-226">You can globally disable a default (non-mobile) view from rendering inside a mobile layout by setting `RequireConsistentDisplayMode` to `true` in hello *Views\\\_ViewStart.cshtml* file, like this:</span></span>

    @{
        Layout = "~/Views/Shared/_Layout.cshtml";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = true;
    }

<span data-ttu-id="05655-227">Lorsque `RequireConsistentDisplayMode` est défini trop`true`, disposition mobile de hello (*\_Layout.Mobile.cshtml*) est utilisé uniquement pour les périphériques mobiles (par exemple, lorsque le fichier est sous forme de hello  ***ViewName** . Mobile.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="05655-227">When `RequireConsistentDisplayMode` is set too`true`, hello mobile layout (*\_Layout.Mobile.cshtml*) is used only for mobile views (i.e. when the view file is of hello form ***ViewName**.Mobile.cshtml*).</span></span> <span data-ttu-id="05655-228">Vous souhaiterez peut-être tooset `RequireConsistentDisplayMode` trop`true` si votre mise en page mobile ne fonctionne pas correctement avec les vues non mobiles.</span><span class="sxs-lookup"><span data-stu-id="05655-228">You might want tooset `RequireConsistentDisplayMode` too`true` if your mobile layout doesn't work well with your non-mobile views.</span></span> <span data-ttu-id="05655-229">Hello capture d’écran ci-dessous montre comment hello *haut-parleurs* page restitue lorsque `RequireConsistentDisplayMode` est défini trop`true` (sans la chaîne hello « (Mobile) » Bonjour navigation barre haut hello).</span><span class="sxs-lookup"><span data-stu-id="05655-229">hello screenshot below shows how hello *Speakers* page renders when `RequireConsistentDisplayMode` is set too`true` (without hello string "(Mobile)" in hello navigational bar at hello top).</span></span>

![][AllSpeakers_LayoutMobileOverridden]

<span data-ttu-id="05655-230">Vous pouvez désactiver le mode d’affichage cohérent dans une vue spécifique en définissant `RequireConsistentDisplayMode` trop`false` dans le fichier de vue hello.</span><span class="sxs-lookup"><span data-stu-id="05655-230">You can disable consistent display mode in a specific view by setting `RequireConsistentDisplayMode` too`false` in hello view file.</span></span> <span data-ttu-id="05655-231">Le balisage suivant Bonjour *vues\\accueil\\AllSpeakers.cshtml* fichier définit `RequireConsistentDisplayMode` trop`false`:</span><span class="sxs-lookup"><span data-stu-id="05655-231">The following markup in hello *Views\\Home\\AllSpeakers.cshtml* file sets `RequireConsistentDisplayMode` too`false`:</span></span>

    @model IEnumerable<string>

    @{
        ViewBag.Title = "All speakers";
        DisplayModeProvider.Instance.RequireConsistentDisplayMode = false;
    }

<span data-ttu-id="05655-232">Dans cette section, nous avons vu comment toocreate dispositions mobiles, des vues et comment toocreate dispositions et les vues pour des périphériques spécifiques tels que hello iPhone.</span><span class="sxs-lookup"><span data-stu-id="05655-232">In this section we've seen how toocreate mobile layouts and views and how toocreate layouts and views for specific devices such as hello iPhone.</span></span>
<span data-ttu-id="05655-233">Toutefois, hello principal avantage du framework du programme d’amorçage CSS hello est la présentation interactive, ce qui signifie qu’une seule feuille de style peut être appliqué sur le bureau, téléphone et tablette navigateurs toocreate une apparence et convivialité cohérentes.</span><span class="sxs-lookup"><span data-stu-id="05655-233">However, hello main advantage of hello Bootstrap CSS framework is the responsive layout, which means that a single stylesheet can be applied across desktop, phone, and tablet browsers toocreate a consistent look and feel.</span></span> <span data-ttu-id="05655-234">Dans la section suivante de hello, vous verrez comment tooleverage amorcer toocreate adaptés aux appareils mobiles des vues.</span><span class="sxs-lookup"><span data-stu-id="05655-234">In hello next section you'll see how tooleverage Bootstrap toocreate mobile-friendly views.</span></span>

## <span data-ttu-id="05655-235"><a name="bkmk_Improvespeakerslist"></a>Améliorer hello haut-parleurs liste</span><span class="sxs-lookup"><span data-stu-id="05655-235"><a name="bkmk_Improvespeakerslist"></a> Improve hello Speakers List</span></span>
<span data-ttu-id="05655-236">Comme vous venez de voir, hello *haut-parleurs* vue est accessible en lecture, mais les liens hello sont petits et sont difficile tootap sur un appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="05655-236">As you just saw, hello *Speakers* view is readable, but hello links are small and are difficult tootap on a mobile device.</span></span> <span data-ttu-id="05655-237">Dans cette section, vous allez apporter hello *AllSpeakers* affichage adaptés aux appareils mobiles, qui affiche des liens volumineux, facile à tap et qui contient un tooquickly de zone de recherche trouvé haut-parleurs.</span><span class="sxs-lookup"><span data-stu-id="05655-237">In this section, you'll make hello *AllSpeakers* view mobile-friendly, which displays large, easy-to-tap links and contains a search box tooquickly find speakers.</span></span>

<span data-ttu-id="05655-238">Vous pouvez utiliser hello Bootstrap [groupe de liste liée] [ linked list group] style afin d’améliorer hello *haut-parleurs* vue.</span><span class="sxs-lookup"><span data-stu-id="05655-238">You can use hello Bootstrap [linked list group][linked list group] styling to improve hello *Speakers* view.</span></span> <span data-ttu-id="05655-239">Dans *vues\\accueil\\AllSpeakers.cshtml*, remplacez le contenu hello du fichier de Razor hello avec code hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="05655-239">In *Views\\Home\\AllSpeakers.cshtml*, replace hello contents of hello Razor file with hello code below.</span></span>

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

<span data-ttu-id="05655-240">Hello `class="list-group"` attribut Bonjour `<div>` balise s’applique le style de la liste d’amorçage et hello `class="input-group-item"` lien tooeach style d’élément de liste d’amorçage s’applique l’attribut.</span><span class="sxs-lookup"><span data-stu-id="05655-240">hello `class="list-group"` attribute in hello `<div>` tag applies the Bootstrap list styling, and hello `class="input-group-item"` attribute applies Bootstrap list item styling tooeach link.</span></span>

<span data-ttu-id="05655-241">Actualiser le navigateur d’appareil mobile hello.</span><span class="sxs-lookup"><span data-stu-id="05655-241">Refresh hello mobile browser.</span></span> <span data-ttu-id="05655-242">Hello mis à jour la vue ressemble :</span><span class="sxs-lookup"><span data-stu-id="05655-242">hello updated view looks like this:</span></span>

![][AllSpeakersFixed]

<span data-ttu-id="05655-243">Hello Bootstrap [groupe de liste liée] [ linked list group] style rend hello entier d’une zone pour chaque lien interactif, ce qui constitue une bien meilleure expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="05655-243">hello Bootstrap [linked list group][linked list group] styling makes hello entire box for each link clickable, which is a much better user experience.</span></span> <span data-ttu-id="05655-244">Basculer l’affichage du bureau toothe et observer hello apparence et convivialité cohérentes.</span><span class="sxs-lookup"><span data-stu-id="05655-244">Switch toothe desktop view and observe hello consistent look and feel.</span></span>

![][AllSpeakersFixedDesktop]

<span data-ttu-id="05655-245">Bien que la vue du navigateur mobile hello a été améliorée, il est difficile de naviguer hello longue liste de haut-parleurs.</span><span class="sxs-lookup"><span data-stu-id="05655-245">Although hello mobile browser view has improved, it's difficult to navigate hello long list of speakers.</span></span> <span data-ttu-id="05655-246">Bootstrap est dépourvu d'une fonction de filtre de recherche en natif. Il est possible d'en ajouter une à l'aide de quelques lignes de code.</span><span class="sxs-lookup"><span data-stu-id="05655-246">Bootstrap doesn't provide a search filter functionality out-of-the-box, but you can add it with a few lines of code.</span></span> <span data-ttu-id="05655-247">Vous allez tout d’abord ajouter une vue de toohello de zone de recherche, puis raccorder avec hello du code JavaScript pour la fonction de filtre hello.</span><span class="sxs-lookup"><span data-stu-id="05655-247">You will first add a search box toohello view, then hook up with hello JavaScript code for hello filter function.</span></span> <span data-ttu-id="05655-248">Dans *vues\\accueil\\AllSpeakers.cshtml*, ajoutez un \<formulaire\> balise juste après hello \<h2\> de balise, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="05655-248">In *Views\\Home\\AllSpeakers.cshtml*, add a \<form\> tag just after hello \<h2\> tag, as shown below:</span></span>

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

<span data-ttu-id="05655-249">Notez que hello `<form>` et `<input>` à la fois les balises ont hello amorçage styles appliqués toothem.</span><span class="sxs-lookup"><span data-stu-id="05655-249">Notice that hello `<form>` and `<input>` tags both have hello Bootstrap styles applied toothem.</span></span> <span data-ttu-id="05655-250">Hello `<span>` élément ajoute un démarrage [glyphicon] [ glyphicon] zone de recherche toothe.</span><span class="sxs-lookup"><span data-stu-id="05655-250">hello `<span>` element adds a Bootstrap [glyphicon][glyphicon] toothe search box.</span></span>

<span data-ttu-id="05655-251">Bonjour *Scripts* dossier, ajoutez un fichier JavaScript nommé *filter.js*.</span><span class="sxs-lookup"><span data-stu-id="05655-251">In hello *Scripts* folder, add a JavaScript file called *filter.js*.</span></span> <span data-ttu-id="05655-252">Ouvrir le fichier de hello et collez hello après le code dans celui-ci :</span><span class="sxs-lookup"><span data-stu-id="05655-252">Open hello file and paste hello following code into it:</span></span>

    $(function () {

        // reset hello search form when hello page loads
        $("form").each(function () {
            this.reset();
        });

        // wire up hello events toohello <input> element for search/filter
        $("input").bind("keyup change", function () {
            var searchtxt = this.value.toLowerCase();
            var items = $(".list-group-item");

            // show all speakers that begin with hello typed text and hide others
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

<span data-ttu-id="05655-253">Vous devez également tooinclude filter.js dans vos regroupements inscrits.</span><span class="sxs-lookup"><span data-stu-id="05655-253">You also need tooinclude filter.js in your registered bundles.</span></span> <span data-ttu-id="05655-254">Ouvrez *application\_Démarrer\\BundleConfig.cs* et modifier des groupes de première hello.</span><span class="sxs-lookup"><span data-stu-id="05655-254">Open *App\_Start\\BundleConfig.cs* and change hello first bundles.</span></span> <span data-ttu-id="05655-255">Modifier la première `bundles.Add` instruction (pour hello **jquery** offre groupée) tooinclude *Scripts\\filter.js*, comme suit :</span><span class="sxs-lookup"><span data-stu-id="05655-255">Change the first `bundles.Add` statement (for hello **jquery** bundle) tooinclude *Scripts\\filter.js*, as follows:</span></span>

     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                "~/Scripts/jquery-{version}.js",
                "~/Scripts/filter.js"));

<span data-ttu-id="05655-256">Hello **jquery** offre groupée est déjà rendue par défaut de hello  *\_disposition* vue.</span><span class="sxs-lookup"><span data-stu-id="05655-256">hello **jquery** bundle is already rendered by hello default *\_Layout* view.</span></span> <span data-ttu-id="05655-257">Une version ultérieure, vous pouvez utiliser hello du code JavaScript même tooapply les affichages de liste de filtre fonctionnalité tooother.</span><span class="sxs-lookup"><span data-stu-id="05655-257">Later, you can utilize hello same JavaScript code tooapply the filter functionality tooother list views.</span></span>

<span data-ttu-id="05655-258">Actualiser le navigateur d’appareil mobile hello et accédez toohello *AllSpeakers* vue.</span><span class="sxs-lookup"><span data-stu-id="05655-258">Refresh hello mobile browser and go toohello *AllSpeakers* view.</span></span> <span data-ttu-id="05655-259">Dans la zone de recherche, entrez « sc ».</span><span class="sxs-lookup"><span data-stu-id="05655-259">In the search box, type "sc".</span></span> <span data-ttu-id="05655-260">liste de haut-parleurs Hello doit maintenant être filtrée en fonction de chaîne de recherche tooyour.</span><span class="sxs-lookup"><span data-stu-id="05655-260">hello speakers list should now be filtered according tooyour search string.</span></span>

![][AllSpeakersFixedSearchBySC]

## <span data-ttu-id="05655-261"><a name="bkmk_improvetags"></a>Améliorer hello liste de balises</span><span class="sxs-lookup"><span data-stu-id="05655-261"><a name="bkmk_improvetags"></a> Improve hello Tags List</span></span>
<span data-ttu-id="05655-262">Comme hello *haut-parleurs* afficher, hello *balises* vue est accessible en lecture, mais les liens de hello sont petite et difficile tootap sur un appareil mobile.</span><span class="sxs-lookup"><span data-stu-id="05655-262">Like hello *Speakers* view, hello *Tags* view is readable, but hello links are small and difficult tootap on a mobile device.</span></span> <span data-ttu-id="05655-263">Vous pouvez corriger hello *balises* vue hello même moyen vous corrigez hello *haut-parleurs* afficher, si vous utilisez des modifications de code hello décrites précédemment, mais avec les éléments suivants de hello `Html.ActionLink` syntaxe de méthode dans  *Vues\\accueil\\AllTags.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="05655-263">You can fix hello *Tags* view hello same way you fix hello *Speakers* view, if you use hello code changes described earlier, but with hello following `Html.ActionLink` method syntax in *Views\\Home\\AllTags.cshtml*:</span></span>

    @Html.ActionLink(tag, 
                     "SessionsByTag", 
                     new { tag }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="05655-264">Hello actualiser la recherche du navigateur de bureau comme suit :</span><span class="sxs-lookup"><span data-stu-id="05655-264">hello refreshed desktop browser looks as follows:</span></span>

![][AllTagsFixedDesktop]

<span data-ttu-id="05655-265">Et hello actualisé navigateur mobile présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="05655-265">And hello refreshed mobile browser looks as follows:</span></span> 

![][AllTagsFixed]

> [!NOTE]
> <span data-ttu-id="05655-266">Si vous remarquez que cette mise en forme de liste d’origine hello est toujours présent dans hello navigateur mobile et vous demander quels styles d’amorçage nice tooyour s’est produit, il s’agit d’un artefact de votre antérieures action toocreate mobile des vues spécifiques.</span><span class="sxs-lookup"><span data-stu-id="05655-266">If you notice that hello original list formatting is still there in hello mobile browser and wonder what happened tooyour nice Bootstrap styling, this is an artifact of your earlier action toocreate mobile specific views.</span></span> <span data-ttu-id="05655-267">Toutefois, maintenant que vous utilisez hello Bootstrap CSS framework toocreate une conception réactive web, accédez de tête et supprimer ces affichages mobiles spécifiques et des vues de mise en page spécifiques à mobile hello.</span><span class="sxs-lookup"><span data-stu-id="05655-267">However, now that you are using hello Bootstrap CSS framework toocreate a responsive web design, go head and remove these mobile-specific views and hello mobile-specific layout views.</span></span> <span data-ttu-id="05655-268">Une fois que vous l’avez fait, hello de navigateur mobile actualisées affichera les styles d’amorçage hello.</span><span class="sxs-lookup"><span data-stu-id="05655-268">Once you have done so, hello refreshed mobile browser will show hello Bootstrap styling.</span></span>
> 
> 

## <span data-ttu-id="05655-269"><a name="bkmk_improvedates"></a>Améliorer hello liste de Dates</span><span class="sxs-lookup"><span data-stu-id="05655-269"><a name="bkmk_improvedates"></a> Improve hello Dates List</span></span>
<span data-ttu-id="05655-270">Vous pouvez améliorer hello *Dates* afficher comme amélioré de hello *haut-parleurs* et *balises* affiche si vous utilisez hello les modifications du code décrites précédemment, mais avec hello suivant `Html.ActionLink` syntaxe de méthode dans *vues\\accueil\\AllDates.cshtml*:</span><span class="sxs-lookup"><span data-stu-id="05655-270">You can improve hello *Dates* view like you improved hello *Speakers* and *Tags* views if you use hello code changes described earlier, but with hello following `Html.ActionLink` method syntax in *Views\\Home\\AllDates.cshtml*:</span></span>

    @Html.ActionLink(date.ToString("ddd, MMM dd, h:mm tt"), 
                     "SessionsByDate", 
                     new { date }, 
                     new { @class = "list-group-item" })

<span data-ttu-id="05655-271">La vue du navigateur mobile actualisé se présente ainsi :</span><span class="sxs-lookup"><span data-stu-id="05655-271">You will get a refreshed mobile browser view like this:</span></span>

![][AllDatesFixed]

<span data-ttu-id="05655-272">Vous pouvez encore améliorer hello *Dates* vue en organisant les valeurs de date-heure hello par date.</span><span class="sxs-lookup"><span data-stu-id="05655-272">You can further improve hello *Dates* view by organizing hello date-time values by date.</span></span> <span data-ttu-id="05655-273">Cela est possible avec hello Bootstrap [panneaux] [ panels] styles.</span><span class="sxs-lookup"><span data-stu-id="05655-273">This can be done with hello Bootstrap [panels][panels] styling.</span></span> <span data-ttu-id="05655-274">Remplacez le contenu hello Hello *vues\\accueil\\AllDates.cshtml* fichier avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="05655-274">Replace hello contents of hello *Views\\Home\\AllDates.cshtml* file with the following code:</span></span>

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

<span data-ttu-id="05655-275">Ce code crée un distinct `<div class="panel panel-primary">` balise pour chaque date distincte dans la liste de hello et utilise hello [groupe de liste liée] [ linked list group] pour différents liens comme avant.</span><span class="sxs-lookup"><span data-stu-id="05655-275">This code creates a separate `<div class="panel panel-primary">` tag for each distinct date in hello list, and uses hello [linked list group][linked list group] for the respective links as before.</span></span> <span data-ttu-id="05655-276">Voici un navigateur mobile hello il semble que lorsque ce code s’exécute :</span><span class="sxs-lookup"><span data-stu-id="05655-276">Here's what hello mobile browser looks like when this code runs:</span></span>

![][AllDatesFixed2]

<span data-ttu-id="05655-277">Navigateur de bureau toohello commutateur.</span><span class="sxs-lookup"><span data-stu-id="05655-277">Switch toohello desktop browser.</span></span> <span data-ttu-id="05655-278">Là encore, notez hello cohérent.</span><span class="sxs-lookup"><span data-stu-id="05655-278">Again, note hello consistent look.</span></span>

![][AllDatesFixed2Desktop]

## <span data-ttu-id="05655-279"><a name="bkmk_improvesessionstable"></a>Améliorer hello SessionsTable vue</span><span class="sxs-lookup"><span data-stu-id="05655-279"><a name="bkmk_improvesessionstable"></a> Improve hello SessionsTable View</span></span>
<span data-ttu-id="05655-280">Dans cette section, vous allez apporter hello *SessionsTable* afficher plus d’adaptés aux appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="05655-280">In this section, you'll make hello *SessionsTable* view more mobile-friendly.</span></span> <span data-ttu-id="05655-281">Cette modification n’est plus étendu hello dernières modifications apportées.</span><span class="sxs-lookup"><span data-stu-id="05655-281">This change is more extensive hello previous changes.</span></span>

<span data-ttu-id="05655-282">Dans le navigateur d’appareil mobile hello, appuyez sur hello **balise** bouton, puis entrez `asp` dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="05655-282">In hello mobile browser, tap hello **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="05655-283">Appuyez sur hello **ASP.NET** lien.</span><span class="sxs-lookup"><span data-stu-id="05655-283">Tap hello **ASP.NET** link.</span></span>

![][SessionsTableTagASP.NET]

<span data-ttu-id="05655-284">Comme vous pouvez le voir, affichage de hello est mise en forme en tant que table, qui est actuellement conçu toobe affichée dans le navigateur de bureau hello.</span><span class="sxs-lookup"><span data-stu-id="05655-284">As you can see, hello display is formatted as a table, which is currently designed toobe viewed in hello desktop browser.</span></span> <span data-ttu-id="05655-285">Toutefois, il est un peu difficile tooread sur un navigateur mobile.</span><span class="sxs-lookup"><span data-stu-id="05655-285">However, it's a little bit difficult tooread on a mobile browser.</span></span> <span data-ttu-id="05655-286">toofix, ouvrez *vues\\accueil\\SessionsTable.cshtml* puis remplacez le contenu hello du fichier par hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="05655-286">toofix this, open *Views\\Home\\SessionsTable.cshtml* and then replace hello contents of the file with hello following code:</span></span>

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

<span data-ttu-id="05655-287">code de Hello effectue les 3 tâches :</span><span class="sxs-lookup"><span data-stu-id="05655-287">hello code does 3 things:</span></span>

* <span data-ttu-id="05655-288">utilise hello Bootstrap [groupe de liste liée personnalisé] [ custom linked list group] tooformat hello verticalement, les informations de session afin que toutes ces informations sont accessibles en lecture sur un navigateur mobile (à l’aide de classes telles que liste groupe-élément-texte)</span><span class="sxs-lookup"><span data-stu-id="05655-288">uses hello Bootstrap [custom linked list group][custom linked list group] tooformat hello session information vertically, so that all this information is readable on a mobile browser (using classes such as list-group-item-text)</span></span>
* <span data-ttu-id="05655-289">s’applique hello [système de grille] [ grid system] toothe disposition, par conséquent, cette session hello les éléments de flux horizontalement dans le navigateur de bureau hello et verticalement dans un navigateur mobile de hello (à l’aide de la classe de hello col-md-4)</span><span class="sxs-lookup"><span data-stu-id="05655-289">applies hello [grid system][grid system] toothe layout, so that hello session items flow horizontally in hello desktop browser and vertically in hello mobile browser (using hello col-md-4 class)</span></span>
* <span data-ttu-id="05655-290">utilise hello [utilitaires réactives] [ responsive utilities] pour masquer les balises de session hello lorsqu’ils sont affichés dans un navigateur mobile de hello (à l’aide de la classe de xs masqué hello)</span><span class="sxs-lookup"><span data-stu-id="05655-290">uses hello [responsive utilities][responsive utilities] to hide hello session tags when viewed in hello mobile browser (using hello hidden-xs class)</span></span>

<span data-ttu-id="05655-291">Vous pouvez aussi appuyer sur une session titre lien toogo toohello respectifs.</span><span class="sxs-lookup"><span data-stu-id="05655-291">You can also tap a title link toogo toohello respective session.</span></span> <span data-ttu-id="05655-292">image Hello ci-dessous reflète les modifications de code hello.</span><span class="sxs-lookup"><span data-stu-id="05655-292">hello image below reflects hello code changes.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="05655-293">système de grille d’amorçage Hello que vous avez appliqués automatiquement organise les sessions verticalement dans le navigateur d’appareil mobile hello.</span><span class="sxs-lookup"><span data-stu-id="05655-293">hello Bootstrap grid system that you applied automatically arranges the sessions vertically in hello mobile browser.</span></span> <span data-ttu-id="05655-294">Notez également que les balises de hello ne sont pas affichées.</span><span class="sxs-lookup"><span data-stu-id="05655-294">Also, notice that hello tags are not shown.</span></span> <span data-ttu-id="05655-295">Navigateur de bureau toohello commutateur.</span><span class="sxs-lookup"><span data-stu-id="05655-295">Switch toohello desktop browser.</span></span>

![][SessionsTableFixedTagASP.NETDesktop]

<span data-ttu-id="05655-296">Dans le navigateur de bureau hello, notez que les balises hello sont maintenant affichées.</span><span class="sxs-lookup"><span data-stu-id="05655-296">In hello desktop browser, notice that hello tags are now displayed.</span></span> <span data-ttu-id="05655-297">En outre, vous pouvez voir que système de grille d’amorçage hello que vous appliqué organise les éléments de session de hello dans deux colonnes.</span><span class="sxs-lookup"><span data-stu-id="05655-297">Also, you can see that hello Bootstrap grid system you applied arranges hello session items in two columns.</span></span> <span data-ttu-id="05655-298">Si vous agrandissez le navigateur, vous verrez que le dispositif de hello change toothree colonnes.</span><span class="sxs-lookup"><span data-stu-id="05655-298">If you enlarge the browser, you will see that hello arrangement changes toothree columns.</span></span>

## <span data-ttu-id="05655-299"><a name="bkmk_improvesessionbycode"></a>Améliorer hello SessionByCode vue</span><span class="sxs-lookup"><span data-stu-id="05655-299"><a name="bkmk_improvesessionbycode"></a> Improve hello SessionByCode View</span></span>
<span data-ttu-id="05655-300">Enfin, vous allez résoudre hello *SessionByCode* afficher toomake il adaptés aux appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="05655-300">Finally, you'll fix hello *SessionByCode* view toomake it mobile-friendly.</span></span>

<span data-ttu-id="05655-301">Dans le navigateur d’appareil mobile hello, appuyez sur hello **balise** bouton, puis entrez `asp` dans la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="05655-301">In hello mobile browser, tap hello **Tag** button, then enter `asp` in the search box.</span></span>

![][AllTagsFixedSearchByASP]

<span data-ttu-id="05655-302">Appuyez sur hello **ASP.NET** lien.</span><span class="sxs-lookup"><span data-stu-id="05655-302">Tap hello **ASP.NET** link.</span></span> <span data-ttu-id="05655-303">Les sessions de balise ASP.NET hello sont affichées.</span><span class="sxs-lookup"><span data-stu-id="05655-303">Sessions for hello ASP.NET tag are displayed.</span></span>

![][FixedSessionsByTag]

<span data-ttu-id="05655-304">Choisissez hello **création d’une Application à Page unique avec ASP.NET et AngularJS** lien.</span><span class="sxs-lookup"><span data-stu-id="05655-304">Choose hello **Building a Single Page Application with ASP.NET and AngularJS** link.</span></span>

![][SessionByCode3-644]

<span data-ttu-id="05655-305">affichage du bureau Hello par défaut convient, mais vous pouvez améliorer hello aspect facilement à l’aide de certains composants de l’interface utilisateur graphique du programme d’amorçage.</span><span class="sxs-lookup"><span data-stu-id="05655-305">hello default desktop view is fine, but you can improve hello look easily by using some Bootstrap GUI components.</span></span>

<span data-ttu-id="05655-306">Ouvrez *vues\\accueil\\SessionByCode.cshtml* et remplacez les contenu hello hello suivant de balisage :</span><span class="sxs-lookup"><span data-stu-id="05655-306">Open *Views\\Home\\SessionByCode.cshtml* and replace hello contents with hello following markup:</span></span>

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

<span data-ttu-id="05655-307">balisage de nouveau Hello utilise des panneaux d’amorçage styles d’affichage mobile de tooimprove hello.</span><span class="sxs-lookup"><span data-stu-id="05655-307">hello new markup uses Bootstrap panels styling tooimprove hello mobile view.</span></span> 

<span data-ttu-id="05655-308">Actualiser le navigateur d’appareil mobile hello.</span><span class="sxs-lookup"><span data-stu-id="05655-308">Refresh hello mobile browser.</span></span> <span data-ttu-id="05655-309">Hello illustration suivante reflète les modifications de code hello que vous venez d’apporter :</span><span class="sxs-lookup"><span data-stu-id="05655-309">hello following image reflects hello code changes that you just made:</span></span>

![][SessionByCodeFixed3-644]

## <a name="wrap-up-and-review"></a><span data-ttu-id="05655-310">Conclusion</span><span class="sxs-lookup"><span data-stu-id="05655-310">Wrap Up and Review</span></span>
<span data-ttu-id="05655-311">Ce didacticiel vous a montré comment les applications Web toouse ASP.NET MVC 5 toodevelop adaptés aux appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="05655-311">This tutorial has shown you how toouse ASP.NET MVC 5 toodevelop mobile-friendly Web applications.</span></span> <span data-ttu-id="05655-312">Vous avez notamment vu les points suivants :</span><span class="sxs-lookup"><span data-stu-id="05655-312">These include:</span></span>

* <span data-ttu-id="05655-313">Déployer un tooan d’application ASP.NET MVC 5 application web App Service</span><span class="sxs-lookup"><span data-stu-id="05655-313">Deploy an ASP.NET MVC 5 application tooan App Service web app</span></span>
* <span data-ttu-id="05655-314">Utiliser la mise en page de démarrage toocreate web réactive dans votre application MVC 5</span><span class="sxs-lookup"><span data-stu-id="05655-314">Use Bootstrap toocreate responsive web layout in your MVC 5 application</span></span>
* <span data-ttu-id="05655-315">Remplacer la disposition, les vues, les vues partielles, de façon globale ou pour une vue spécifique</span><span class="sxs-lookup"><span data-stu-id="05655-315">Override layout, views, and partial views, both globally and for an individual view</span></span>
* <span data-ttu-id="05655-316">Contrôler la disposition et l’application de remplacement partiel à l’aide de la propriété `RequireConsistentDisplayMode`</span><span class="sxs-lookup"><span data-stu-id="05655-316">Control layout and partial override enforcement using the `RequireConsistentDisplayMode` property</span></span>
* <span data-ttu-id="05655-317">Créer des vues qui ciblent des navigateurs spécifiques, tels que navigateur iPhone qui hello</span><span class="sxs-lookup"><span data-stu-id="05655-317">Create views that target specific browsers, such as hello iPhone browser</span></span>
* <span data-ttu-id="05655-318">Appliquer des styles Bootstrap dans le code Razor</span><span class="sxs-lookup"><span data-stu-id="05655-318">Apply Bootstrap styling in Razor code</span></span>

## <a name="see-also"></a><span data-ttu-id="05655-319">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="05655-319">See Also</span></span>
* [<span data-ttu-id="05655-320">9 principes de base de la conception web réactive (en anglais)</span><span class="sxs-lookup"><span data-stu-id="05655-320">9 basic principles of responsive web design</span></span>](http://blog.froont.com/9-basic-principles-of-responsive-web-design/)
* <span data-ttu-id="05655-321">[Bootstrap][BootstrapSite]</span><span class="sxs-lookup"><span data-stu-id="05655-321">[Bootstrap][BootstrapSite]</span></span>
* <span data-ttu-id="05655-322">[Blog Bootstrap officiel (en anglais)][Official Bootstrap Blog]</span><span class="sxs-lookup"><span data-stu-id="05655-322">[Official Bootstrap Blog][Official Bootstrap Blog]</span></span>
* <span data-ttu-id="05655-323">[Tutoriel Bootstrap Twitter de Tutorial Republic (en anglais)][Twitter Bootstrap Tutorial from Tutorial Republic]</span><span class="sxs-lookup"><span data-stu-id="05655-323">[Twitter Bootstrap Tutorial from Tutorial Republic][Twitter Bootstrap Tutorial from Tutorial Republic]</span></span>
* <span data-ttu-id="05655-324">[Hello amorçage de laboratoire][hello Bootstrap Playground]</span><span class="sxs-lookup"><span data-stu-id="05655-324">[hello Bootstrap Playground][hello Bootstrap Playground]</span></span>
* <span data-ttu-id="05655-325">[Bonnes pratiques pour les applications web mobiles des recommandations W3C (en anglais)][W3C Recommendation Mobile Web Application Best Practices]</span><span class="sxs-lookup"><span data-stu-id="05655-325">[W3C Recommendation Mobile Web Application Best Practices][W3C Recommendation Mobile Web Application Best Practices]</span></span>
* <span data-ttu-id="05655-326">[Candidat à la recommandation du W3C concernant les requêtes de média (en anglais)][W3C Candidate Recommendation for media queries]</span><span class="sxs-lookup"><span data-stu-id="05655-326">[W3C Candidate Recommendation for media queries][W3C Candidate Recommendation for media queries]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="05655-327">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="05655-327">What's changed</span></span>
* <span data-ttu-id="05655-328">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="05655-328">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- Internal Links -->
[Deploy hello starter project tooan Azure web app]: #bkmk_DeployStarterProject
[Bootstrap CSS Framework]: #bkmk_bootstrap
[Override hello Views, Layouts, and Partial Views]: #bkmk_overrideviews
[Create Browser-Specific Views]:#bkmk_browserviews
[Improve hello Speakers List]: #bkmk_Improvespeakerslist
[Improve hello Tags List]: #bkmk_improvetags
[Improve hello Dates List]: #bkmk_improvedates
[Improve hello SessionsTable View]: #bkmk_improvesessionstable
[Improve hello SessionByCode View]: #bkmk_improvesessionbycode

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
[hello Bootstrap Playground]: http://www.bootply.com/
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

