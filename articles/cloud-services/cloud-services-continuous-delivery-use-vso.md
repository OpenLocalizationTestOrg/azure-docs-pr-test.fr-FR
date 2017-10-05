---
title: Livraison continue avec Visual Studio Team Services dans Azure | Microsoft Docs
description: "Découvrez comment configurer vos projets d'équipe Visual Studio Team Services afin de les générer et de les déployer automatiquement vers la fonctionnalité Web App d’Azure App Service ou des Cloud Services."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: d80ce63eb7ddfd7c45726be887a772f9a7594b28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services"></a><span data-ttu-id="9b90f-103">Diffusion continue sur Azure au moyen de Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="9b90f-103">Continuous delivery to Azure using Visual Studio Team Services</span></span>
<span data-ttu-id="9b90f-104">Vous pouvez configurer vos projets Visual Studio Team Services afin de les générer et de les déployer automatiquement sur des applications Web Azure ou des Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="9b90f-104">You can configure your Visual Studio Team Services team projects to automatically build and deploy to Azure web apps or cloud services.</span></span>  <span data-ttu-id="9b90f-105">(Pour plus d'informations sur la procédure à suivre pour configurer un système de génération et de déploiement continus au moyen d'un serveur TFS *local* , consultez la rubrique [Remise continue pour Cloud Services dans Azure](cloud-services-dotnet-continuous-delivery.md).)</span><span class="sxs-lookup"><span data-stu-id="9b90f-105">(For information on how to set up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="9b90f-106">Ce didacticiel part du principe que vous avez déjà installé Visual Studio 2013 et le Kit de développement logiciel (SDK) Azure sur votre système.</span><span class="sxs-lookup"><span data-stu-id="9b90f-106">This tutorial assumes you have Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="9b90f-107">Si Visual Studio 2013 n'est pas déjà installé, téléchargez-le en choisissant le lien **Test gratuit de Visual Studio** sur [www.visualstudio.com](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="9b90f-107">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="9b90f-108">Pour installer le Kit de développement logiciel (SDK) Azure, cliquez [ici](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="9b90f-108">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="9b90f-109">Vous avez besoin d’un compte Visual Studio Team Services pour suivre ce didacticiel : vous pouvez [ouvrir un compte Visual Studio Team Services gratuit](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="9b90f-109">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="9b90f-110">Pour configurer un service cloud permettant de générer et de déployer automatiquement sur Azure au moyen de Visual Studio Team Services, suivez ces étapes.</span><span class="sxs-lookup"><span data-stu-id="9b90f-110">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="9b90f-111">1 : Création d'un projet d'équipe</span><span class="sxs-lookup"><span data-stu-id="9b90f-111">1: Create a team project</span></span>
<span data-ttu-id="9b90f-112">Suivez les instructions disponibles [ici](http://go.microsoft.com/fwlink/?LinkId=512980) pour créer votre projet d'équipe et l'associer à Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9b90f-112">Follow the instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) to create your team project and link it to Visual Studio.</span></span> <span data-ttu-id="9b90f-113">Cette procédure pas à pas part du principe que vous utilisez TFVC (Team Foundation Version Control) en tant que solution de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="9b90f-113">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="9b90f-114">Si vous souhaitez utiliser Git pour le contrôle de version, consultez [la version Git de cette procédure pas à pas](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span><span class="sxs-lookup"><span data-stu-id="9b90f-114">If you want to use Git for version control, see [the Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-to-source-control"></a><span data-ttu-id="9b90f-115">2 : Archivage d'un projet dans le contrôle de code source</span><span class="sxs-lookup"><span data-stu-id="9b90f-115">2: Check in a project to source control</span></span>
1. <span data-ttu-id="9b90f-116">Dans Visual Studio, ouvrez la solution à déployer, ou créez-en une.</span><span class="sxs-lookup"><span data-stu-id="9b90f-116">In Visual Studio, open the solution you want to deploy, or create a new one.</span></span>
   <span data-ttu-id="9b90f-117">Vous pouvez déployer une application Web ou un service cloud (application Azure) en suivant les étapes de cette procédure.</span><span class="sxs-lookup"><span data-stu-id="9b90f-117">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span>
   <span data-ttu-id="9b90f-118">Si vous voulez créer une solution, créez un projet de service cloud Azure ou ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="9b90f-118">If you want to create a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="9b90f-119">Vérifiez que le projet cible .NET Framework 4 ou 4.5, et si vous créez un projet de service cloud, ajoutez un rôle Web ASP.NET MVC et un rôle de travail, et choisissez Application Internet pour le rôle Web.</span><span class="sxs-lookup"><span data-stu-id="9b90f-119">Make sure that the project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for the web role.</span></span> <span data-ttu-id="9b90f-120">Lorsque vous y êtes invité, choisissez **Application Internet**.</span><span class="sxs-lookup"><span data-stu-id="9b90f-120">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="9b90f-121">Si vous voulez créer une application Web, choisissez le modèle de projet Application Web ASP.NET, puis sélectionnez MVC.</span><span class="sxs-lookup"><span data-stu-id="9b90f-121">If you want to create a web app, choose the ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="9b90f-122">Consultez la rubrique [Création d’une application Web ASP.NET dans Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9b90f-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9b90f-123">Actuellement, Visual Studio Team Services ne prend en charge que les déploiements CI des applications web Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9b90f-123">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="9b90f-124">Les projets de site web n’entrent pas dans ce cadre.</span><span class="sxs-lookup"><span data-stu-id="9b90f-124">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="9b90f-125">Ouvrez le menu contextuel pour la solution et sélectionnez **Ajouter la solution au contrôle de code source**.</span><span class="sxs-lookup"><span data-stu-id="9b90f-125">Open the context menu for the solution, and choose **Add Solution to Source Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="9b90f-126">Acceptez ou modifiez les valeurs par défaut et choisissez le bouton **OK** .</span><span class="sxs-lookup"><span data-stu-id="9b90f-126">Accept or change the defaults and choose the **OK** button.</span></span> <span data-ttu-id="9b90f-127">Au terme du processus, les icônes du contrôle de code source apparaissent dans l' **Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="9b90f-127">Once the process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="9b90f-128">Ouvrez le menu contextuel de la solution et choisissez **Archiver**.</span><span class="sxs-lookup"><span data-stu-id="9b90f-128">Open the shortcut menu for the solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="9b90f-129">Dans la zone **Modifications en attente** de **Team Explorer**, tapez un commentaire pour l’archivage et choisissez le bouton **Archiver**.</span><span class="sxs-lookup"><span data-stu-id="9b90f-129">In the **Pending Changes** area of **Team Explorer**, type a comment for the check-in and choose the **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="9b90f-130">Notez les options à inclure ou exclure quand vous archivez des modifications spécifiques.</span><span class="sxs-lookup"><span data-stu-id="9b90f-130">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="9b90f-131">Si des modifications voulues sont exclues, choisissez le lien **Tout inclure** .</span><span class="sxs-lookup"><span data-stu-id="9b90f-131">If desired changes are excluded, choose the **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="9b90f-132">3 : Connexion du projet à Azure</span><span class="sxs-lookup"><span data-stu-id="9b90f-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="9b90f-133">Maintenant que vous disposez d’un projet d’équipe Visual Studio Team Services contenant du code source, vous êtes prêt à connecter votre projet d’équipe à Azure.</span><span class="sxs-lookup"><span data-stu-id="9b90f-133">Now that you have a VS Team Services team project with some source code in it, you are ready to connect your team project to Azure.</span></span>  <span data-ttu-id="9b90f-134">Dans le [portail Azure Classic](http://go.microsoft.com/fwlink/?LinkID=213885), sélectionnez votre service cloud ou application web, ou créez-en un en sélectionnant l’icône **+** en bas à gauche et en choisissant **Service cloud** ou **Application web**, puis **Création rapide**.</span><span class="sxs-lookup"><span data-stu-id="9b90f-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the **+** icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="9b90f-135">Choisissez le lien **Configurer la publication avec Visual Studio Team Services** .</span><span class="sxs-lookup"><span data-stu-id="9b90f-135">Choose the **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="9b90f-136">Dans l'Assistant, tapez le nom de votre compte Visual Studio Team Services dans la zone de texte et cliquez sur le lien **Autoriser maintenant** .</span><span class="sxs-lookup"><span data-stu-id="9b90f-136">In the wizard, type the name of your Visual Studio Team Services account in the textbox and click the **Authorize Now** link.</span></span> <span data-ttu-id="9b90f-137">Vous serez peut-être invité à vous connecter.</span><span class="sxs-lookup"><span data-stu-id="9b90f-137">You might be asked to sign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="9b90f-138">Dans la boîte de dialogue contextuelle **Demande de connexion**, choisissez le bouton **Accepter** pour autoriser Azure à configurer votre projet d’équipe dans Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="9b90f-138">In the **Connection Request** pop-up dialog, choose the **Accept** button to authorize Azure to configure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="9b90f-139">Si le processus d'autorisation aboutit, une zone déroulante affiche une liste de vos projets Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="9b90f-139">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="9b90f-140">Choisissez le nom du projet d’équipe que vous avez créé aux étapes précédentes et choisissez la coche de l’Assistant.</span><span class="sxs-lookup"><span data-stu-id="9b90f-140">Choose  the name of team project that you created in the previous steps, and then choose the wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="9b90f-141">Une fois votre projet lié, des instructions s'affichent pour vous permettre d'archiver les modifications dans votre projet d'équipe Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="9b90f-141">After your project is linked, you will see some instructions for checking in changes to your Visual Studio Team Services team project.</span></span>  <span data-ttu-id="9b90f-142">Lors du prochain archivage, Visual Studio Team Services générera et déploiera votre projet sur Azure.</span><span class="sxs-lookup"><span data-stu-id="9b90f-142">On your next check-in, Visual Studio Team Services will build and deploy your project to Azure.</span></span>  <span data-ttu-id="9b90f-143">Essayez maintenant en cliquant sur le lien **Archiver depuis Visual Studio**, puis sur le lien **Lancer Visual Studio** (ou le bouton **Visual Studio** équivalent en bas de l’écran du portail).</span><span class="sxs-lookup"><span data-stu-id="9b90f-143">Try this now by clicking the **Check In from Visual Studio** link, and then the **Launch Visual Studio** link (or the equivalent **Visual Studio** button at the bottom of the portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="9b90f-144">4 : Déclenchement d'une régénération et redéploiement de votre projet</span><span class="sxs-lookup"><span data-stu-id="9b90f-144">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="9b90f-145">Dans Visual Studio **Team Explorer**, choisissez le lien **Explorateur du contrôle de code source**.</span><span class="sxs-lookup"><span data-stu-id="9b90f-145">In Visual Studio's **Team Explorer**, choose the **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="9b90f-146">Accédez à votre fichier solution et ouvrez-le.</span><span class="sxs-lookup"><span data-stu-id="9b90f-146">Navigate to your solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="9b90f-147">Dans l' **Explorateur de solutions**, ouvrez un fichier et modifiez-le.</span><span class="sxs-lookup"><span data-stu-id="9b90f-147">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="9b90f-148">Par exemple, modifiez le fichier `_Layout.cshtml` sous le dossier Views\\Shared dans un rôle Web MVC.</span><span class="sxs-lookup"><span data-stu-id="9b90f-148">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="9b90f-149">Modifiez le logo du site et appuyez sur **Ctrl+S** pour enregistrer le fichier.</span><span class="sxs-lookup"><span data-stu-id="9b90f-149">Edit the logo for the site and choose **Ctrl+S** to save the file.</span></span>
   
    ![][18]
5. <span data-ttu-id="9b90f-150">Dans **Team Explorer**, choisissez le lien **Modifications en attente**.</span><span class="sxs-lookup"><span data-stu-id="9b90f-150">In **Team Explorer**, choose the **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="9b90f-151">Entrez un commentaire et choisissez le bouton **Archiver** .</span><span class="sxs-lookup"><span data-stu-id="9b90f-151">Enter a comment and then choose the **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="9b90f-152">Choisissez le bouton **Accueil** pour revenir à la page d’accueil de **Team Explorer**.</span><span class="sxs-lookup"><span data-stu-id="9b90f-152">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="9b90f-153">Choisissez le lien **Builds** pour afficher les builds en cours.</span><span class="sxs-lookup"><span data-stu-id="9b90f-153">Choose the **Builds** link to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="9b90f-154">**Team Explorer** indique qu’une build est disponible pour archivage.</span><span class="sxs-lookup"><span data-stu-id="9b90f-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="9b90f-155">Double-cliquez sur le nom de la build en cours pour afficher un journal détaillé lors du processus de génération.</span><span class="sxs-lookup"><span data-stu-id="9b90f-155">Double-click the name of the build in progress to view a detailed log as the build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="9b90f-156">Pendant la création de la build, examinez la définition de build qui a été créée lorsque vous avez lié TFS à Azure au moyen de l'Assistant.</span><span class="sxs-lookup"><span data-stu-id="9b90f-156">While the build is in-progress, take a look at the build definition that was created when you linked TFS to Azure by using the wizard.</span></span>  <span data-ttu-id="9b90f-157">Ouvrez le menu contextuel de la définition de build et choisissez **Modifier la définition de build**.</span><span class="sxs-lookup"><span data-stu-id="9b90f-157">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="9b90f-158">Dans l’onglet **Déclencher** , vous allez voir que la définition de build prévoit par défaut un processus de génération pour chaque archivage.</span><span class="sxs-lookup"><span data-stu-id="9b90f-158">In the **Trigger** tab, you will see that the build definition is set to build on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="9b90f-159">Dans l'onglet **Processus** , vous pouvez voir que l'environnement de déploiement est défini sur le nom de votre service cloud ou application Web.</span><span class="sxs-lookup"><span data-stu-id="9b90f-159">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span> <span data-ttu-id="9b90f-160">Si vous utilisez des applications Web, les propriétés affichées seront différentes de celles figurant ici.</span><span class="sxs-lookup"><span data-stu-id="9b90f-160">If you are working with web apps, the properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="9b90f-161">Spécifiez des valeurs pour les propriétés si vous souhaitez d'autres valeurs que celles par défaut.</span><span class="sxs-lookup"><span data-stu-id="9b90f-161">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="9b90f-162">Les propriétés pour la publication Azure se trouvent dans la section **Déploiement** .</span><span class="sxs-lookup"><span data-stu-id="9b90f-162">The properties for Azure publishing are in the **Deployment** section.</span></span>
    
     <span data-ttu-id="9b90f-163">Le tableau suivant présente les propriétés disponibles dans la section **Déploiement** :</span><span class="sxs-lookup"><span data-stu-id="9b90f-163">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="9b90f-164">Propriété</span><span class="sxs-lookup"><span data-stu-id="9b90f-164">Property</span></span> | <span data-ttu-id="9b90f-165">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="9b90f-165">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="9b90f-166">Autoriser les certificats non approuvés</span><span class="sxs-lookup"><span data-stu-id="9b90f-166">Allow Untrusted Certificates</span></span> |<span data-ttu-id="9b90f-167">Si cette propriété a la valeur false, des certificats SSL doivent être signés par une autorité racine.</span><span class="sxs-lookup"><span data-stu-id="9b90f-167">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="9b90f-168">Autoriser la mise à niveau</span><span class="sxs-lookup"><span data-stu-id="9b90f-168">Allow Upgrade</span></span> |<span data-ttu-id="9b90f-169">Permet au déploiement de mettre à jour un déploiement existant au lieu d'en créer un.</span><span class="sxs-lookup"><span data-stu-id="9b90f-169">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="9b90f-170">Conserve l'adresse IP.</span><span class="sxs-lookup"><span data-stu-id="9b90f-170">Preserves the IP address.</span></span> |
    | <span data-ttu-id="9b90f-171">Ne pas supprimer</span><span class="sxs-lookup"><span data-stu-id="9b90f-171">Do Not Delete</span></span> |<span data-ttu-id="9b90f-172">Si cette propriété a la valeur true, ne remplacez pas un déploiement sans rapport (la mise à niveau est autorisée).</span><span class="sxs-lookup"><span data-stu-id="9b90f-172">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="9b90f-173">Chemin d'accès des paramètres de déploiement</span><span class="sxs-lookup"><span data-stu-id="9b90f-173">Path to Deployment Settings</span></span> |<span data-ttu-id="9b90f-174">Chemin d’accès à votre fichier .pubxml pour un site Web, relatif au dossier racine du référentiel.</span><span class="sxs-lookup"><span data-stu-id="9b90f-174">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="9b90f-175">Ignorée pour les services cloud.</span><span class="sxs-lookup"><span data-stu-id="9b90f-175">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="9b90f-176">Environnement de déploiement SharePoint</span><span class="sxs-lookup"><span data-stu-id="9b90f-176">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="9b90f-177">Identique au nom du service.</span><span class="sxs-lookup"><span data-stu-id="9b90f-177">The same as the service name.</span></span> |
    | <span data-ttu-id="9b90f-178">Environnement de déploiement Azure</span><span class="sxs-lookup"><span data-stu-id="9b90f-178">Azure Deployment Environment</span></span> |<span data-ttu-id="9b90f-179">Nom de l'application Web ou du service cloud.</span><span class="sxs-lookup"><span data-stu-id="9b90f-179">The web app or cloud service name.</span></span> |
12. <span data-ttu-id="9b90f-180">Si vous utilisez plusieurs configurations de service (fichiers .cscfg), vous pouvez spécifier la configuration du service désiré dans le paramètre **Build, Advanced, MSBuild arguments** .</span><span class="sxs-lookup"><span data-stu-id="9b90f-180">If you are using multiple service configurations (.cscfg files), you can specify the desired service configuration in the **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="9b90f-181">Par exemple, pour utiliser ServiceConfiguration.Test.cscfg, définissez l'option de ligne d'argument MSBuild `/p:TargetProfile=Test`.</span><span class="sxs-lookup"><span data-stu-id="9b90f-181">For example, to use ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="9b90f-182">À ce stade, la création de la build doit être terminée.</span><span class="sxs-lookup"><span data-stu-id="9b90f-182">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="9b90f-183">Si vous double-cliquez sur le nom de la build, Visual Studio affiche un **Résumé de la build**, y compris tous les résultats de test provenant de projets de test unitaires associés.</span><span class="sxs-lookup"><span data-stu-id="9b90f-183">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="9b90f-184">Dans le [portail Azure Classic](http://go.microsoft.com/fwlink/?LinkID=213885), vous pouvez afficher le déploiement associé sous l’onglet **Déploiements** quand l’environnement intermédiaire est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="9b90f-184">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="9b90f-185">Accédez à l'URL de votre site.</span><span class="sxs-lookup"><span data-stu-id="9b90f-185">Browse to your site's URL.</span></span> <span data-ttu-id="9b90f-186">Dans le cas d'une application Web, cliquez simplement sur le bouton **Parcourir** dans la barre de commandes.</span><span class="sxs-lookup"><span data-stu-id="9b90f-186">For a web app, just click the **Browse** button on the command bar.</span></span> <span data-ttu-id="9b90f-187">Dans le cas d’un service cloud, choisissez l’URL dans la section **Aperçu rapide** de la page **Tableau de bord** représentant l’environnement intermédiaire d’un service cloud.</span><span class="sxs-lookup"><span data-stu-id="9b90f-187">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment for a cloud service.</span></span> <span data-ttu-id="9b90f-188">Les déploiements résultant de l'intégration continue de services cloud sont publiés dans l'environnement intermédiaire par défaut.</span><span class="sxs-lookup"><span data-stu-id="9b90f-188">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="9b90f-189">Vous pouvez changer cela en définissant la propriété **Environnement du service cloud de substitution** sur **Production**.</span><span class="sxs-lookup"><span data-stu-id="9b90f-189">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="9b90f-190">Cet écran indique où se trouve l'URL de site dans la page de tableau de bord du service cloud.</span><span class="sxs-lookup"><span data-stu-id="9b90f-190">This screenshot shows where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="9b90f-191">Un nouvel onglet de navigateur apparaît pour afficher votre site en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="9b90f-191">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="9b90f-192">Pour les services cloud, si vous apportez d'autres modifications à votre projet, vous déclenchez d'autres builds et vous accumulez plusieurs déploiements.</span><span class="sxs-lookup"><span data-stu-id="9b90f-192">For cloud services, if you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="9b90f-193">Le plus récent est marqué comme étant actif.</span><span class="sxs-lookup"><span data-stu-id="9b90f-193">The latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="9b90f-194">5 : Redéploiement d'une build antérieure</span><span class="sxs-lookup"><span data-stu-id="9b90f-194">5: Redeploy an earlier build</span></span>
<span data-ttu-id="9b90f-195">Cette étape (facultative) s'applique aux services cloud.</span><span class="sxs-lookup"><span data-stu-id="9b90f-195">This step applies to cloud services and is optional.</span></span> <span data-ttu-id="9b90f-196">Dans le portail Azure Classic, choisissez un déploiement antérieur et cliquez sur le bouton **Redéployer** pour revenir à un archivage antérieur de votre site.</span><span class="sxs-lookup"><span data-stu-id="9b90f-196">In the Azure classic portal, choose an earlier deployment and then choose the **Redeploy** button to rewind your site to an earlier check-in.</span></span>  <span data-ttu-id="9b90f-197">Notez que cela déclenche une nouvelle génération dans TFS et crée une entrée dans l’historique de votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="9b90f-197">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="9b90f-198">6 : Modification du déploiement de production</span><span class="sxs-lookup"><span data-stu-id="9b90f-198">6: Change the Production deployment</span></span>
<span data-ttu-id="9b90f-199">Cette étape s'applique uniquement aux services cloud, pas aux applications Web.</span><span class="sxs-lookup"><span data-stu-id="9b90f-199">This step applies only to cloud services, not web apps.</span></span> <span data-ttu-id="9b90f-200">Une fois que vous êtes prêt, vous pouvez promouvoir l'environnement intermédiaire en environnement de production en choisissant le bouton **Swap** dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="9b90f-200">When you are ready, you can promote the Staging environment to the production environment by choosing the **Swap** button in the Azure classic portal.</span></span> <span data-ttu-id="9b90f-201">L'environnement intermédiaire récemment déployé passe à l'état de production et l'environnement de production précédent, le cas échéant, devient un environnement intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="9b90f-201">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="9b90f-202">Le déploiement actif peut être différent pour les environnements de production et intermédiaire, mais l'historique de déploiement des builds récentes est identique quel que soit l'environnement.</span><span class="sxs-lookup"><span data-stu-id="9b90f-202">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="9b90f-203">7 : Exécution de tests unitaires</span><span class="sxs-lookup"><span data-stu-id="9b90f-203">7: Run unit tests</span></span>
<span data-ttu-id="9b90f-204">Cette étape s'applique uniquement aux applications Web, et non aux services cloud.</span><span class="sxs-lookup"><span data-stu-id="9b90f-204">This step applies only to web apps, not cloud services.</span></span> <span data-ttu-id="9b90f-205">Pour mettre en place un « portail de qualité » dans votre déploiement, vous pouvez exécuter des tests unitaires. S'ils échouent, vous pouvez interrompre le déploiement.</span><span class="sxs-lookup"><span data-stu-id="9b90f-205">To put a quality gate on your deployment, you can run unit tests and if they fail, you can stop the deployment.</span></span>

1. <span data-ttu-id="9b90f-206">Dans Visual Studio, ajoutez un projet de test unitaire.</span><span class="sxs-lookup"><span data-stu-id="9b90f-206">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="9b90f-207">Ajoutez les références de projet au projet que vous souhaitez tester.</span><span class="sxs-lookup"><span data-stu-id="9b90f-207">Add project references to the project you want to test.</span></span>
   
   ![][40]
3. <span data-ttu-id="9b90f-208">Ajoutez quelques tests unitaires.</span><span class="sxs-lookup"><span data-stu-id="9b90f-208">Add some unit tests.</span></span> <span data-ttu-id="9b90f-209">Pour commencer, essayez de réaliser un faux test qui réussira toujours.</span><span class="sxs-lookup"><span data-stu-id="9b90f-209">To get started, try a dummy test that will always pass.</span></span>
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. <span data-ttu-id="9b90f-210">Modifiez la définition de la build, choisissez l’onglet **Processus** et étendez le nœud de **test**.</span><span class="sxs-lookup"><span data-stu-id="9b90f-210">Edit the build definition, choose the **Process** tab, and expand the **Test** node.</span></span>
5. <span data-ttu-id="9b90f-211">Définissez le paramètre **Fail build on test failure** sur True.</span><span class="sxs-lookup"><span data-stu-id="9b90f-211">Set the **Fail build on test failure** to True.</span></span> <span data-ttu-id="9b90f-212">Cela signifie que le déploiement ne sera pas réalisé à moins que le test ne réussisse.</span><span class="sxs-lookup"><span data-stu-id="9b90f-212">This means that the deployment won't occur unless the tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="9b90f-213">Placez une nouvelle build dans la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="9b90f-213">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="9b90f-214">Pendant que la build est en cours de traitement, suivez sa progression.</span><span class="sxs-lookup"><span data-stu-id="9b90f-214">While the build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="9b90f-215">Lorsque la build est terminée, consultez les résultats de test.</span><span class="sxs-lookup"><span data-stu-id="9b90f-215">When the build is done, check the test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="9b90f-216">Essayez de créer un nouveau test qui échouera.</span><span class="sxs-lookup"><span data-stu-id="9b90f-216">Try creating a test that will fail.</span></span> <span data-ttu-id="9b90f-217">Ajoutez un nouveau test en copiant le premier, en le renommant et en plaçant en commentaire la ligne de code indiquant que NotImplementedException est une exception attendue.</span><span class="sxs-lookup"><span data-stu-id="9b90f-217">Add a new test by copying the first one, rename it, and comment out the line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="9b90f-218">Archivez le changement pour mettre une nouvelle build dans la file d'attente.</span><span class="sxs-lookup"><span data-stu-id="9b90f-218">Check in the change to queue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="9b90f-219">Consultez les résultats du test pour obtenir des détails sur l'échec.</span><span class="sxs-lookup"><span data-stu-id="9b90f-219">View the test results to see details about the failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="9b90f-220">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9b90f-220">Next steps</span></span>
<span data-ttu-id="9b90f-221">Pour en savoir plus sur le test unitaire dans Visual Studio Team Services, consultez [Exécuter des tests unitaires dans votre build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span><span class="sxs-lookup"><span data-stu-id="9b90f-221">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="9b90f-222">Si vous utilisez Git, consultez les rubriques [Partager votre code dans Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) et [Déploiement continu vers Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="9b90f-222">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="9b90f-223">Pour en savoir plus sur Visual Studio Team Services, consultez [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="9b90f-223">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
