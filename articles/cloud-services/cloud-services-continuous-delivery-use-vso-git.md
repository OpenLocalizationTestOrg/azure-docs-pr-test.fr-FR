---
title: Livraison continue avec Git et Visual Studio Team Services dans Azure | Microsoft Docs
description: "Découvrez comment configurer vos projets d'équipe Visual Studio Team Services afin d’utiliser Git pour les générer et les déployer automatiquement vers la fonctionnalité Web App d’Azure App Service ou des Cloud Services."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: f4f5f231536bc381d17898ff2c592be821168a65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="43848-103">Diffusion continue sur Azure au moyen de Visual Studio Team Services et Git</span><span class="sxs-lookup"><span data-stu-id="43848-103">Continuous delivery to Azure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="43848-104">Vous pouvez utiliser des projets d'équipe Visual Studio Team Services pour héberger un référentiel Git pour votre code source, et pour les créer et déployer automatiquement dans des applications Web ou des Cloud Services Azure lorsque vous placez une validation dans le référentiel.</span><span class="sxs-lookup"><span data-stu-id="43848-104">You can use Visual Studio Team Services team projects to host a Git repository for your source code, and automatically build and deploy to Azure web apps or cloud services whenever you push a commit to the repository.</span></span>

<span data-ttu-id="43848-105">Visual Studio 2013 et le Kit de développement logiciel (SDK) Azure doivent être installés sur votre système.</span><span class="sxs-lookup"><span data-stu-id="43848-105">You'll need Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="43848-106">Si Visual Studio 2013 n'est pas déjà installé, téléchargez-le en choisissant le lien **Test gratuit de Visual Studio** sur [www.visualstudio.com](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="43848-106">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="43848-107">Pour installer le Kit de développement logiciel (SDK) Azure, cliquez [ici](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="43848-107">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="43848-108">Vous avez besoin d’un compte Visual Studio Team Services pour suivre ce didacticiel : vous pouvez [ouvrir un compte Visual Studio Team Services gratuit](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="43848-108">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="43848-109">Pour configurer un service cloud permettant de générer et de déployer automatiquement sur Azure au moyen de Visual Studio Team Services, suivez ces étapes.</span><span class="sxs-lookup"><span data-stu-id="43848-109">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="43848-110">1 : Création d'un référentiel Git</span><span class="sxs-lookup"><span data-stu-id="43848-110">1: Create a Git repository</span></span>
1. <span data-ttu-id="43848-111">Si vous ne disposez pas de compte Visual Studio Team Services, vous pouvez en obtenir un [ici](http://go.microsoft.com/fwlink/?LinkId=397665).</span><span class="sxs-lookup"><span data-stu-id="43848-111">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="43848-112">Lorsque vous créez un projet d'équipe, choisissez Git comme système de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="43848-112">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="43848-113">Suivez les instructions de connexion de Visual Studio à votre projet d'équipe.</span><span class="sxs-lookup"><span data-stu-id="43848-113">Follow the instructions to connect Visual Studio to your team project.</span></span>
2. <span data-ttu-id="43848-114">Dans **Team Explorer**, sélectionnez le lien **Cloner ce référentiel**.</span><span class="sxs-lookup"><span data-stu-id="43848-114">In **Team Explorer**, choose the **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="43848-115">Indiquez l’emplacement de la copie locale, puis sélectionnez le bouton **Cloner** .</span><span class="sxs-lookup"><span data-stu-id="43848-115">Specify the location of the local copy and then choose the **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-to-the-repository"></a><span data-ttu-id="43848-116">2 : Création d'un projet et validation dans le référentiel</span><span class="sxs-lookup"><span data-stu-id="43848-116">2: Create a project and commit it to the repository</span></span>
1. <span data-ttu-id="43848-117">Dans la section **Solutions** de **Team Explorer**, sélectionnez le lien **Nouveau** pour créer un projet dans le référentiel local.</span><span class="sxs-lookup"><span data-stu-id="43848-117">In **Team Explorer**, in the **Solutions** section, choose the **New** link to create a new project in the local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="43848-118">Vous pouvez déployer une application Web ou un service cloud (application Azure) en suivant les étapes de cette procédure.</span><span class="sxs-lookup"><span data-stu-id="43848-118">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span> <span data-ttu-id="43848-119">Créez un projet de service cloud Azure ou un projet MVC ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="43848-119">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="43848-120">Assurez-vous que le projet cible le .NET Framework 4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="43848-120">Make sure that the project targets the .NET Framework 4 or later.</span></span> <span data-ttu-id="43848-121">Si vous créez un projet de service cloud, ajoutez un rôle web ASP.NET MVC et un rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="43848-121">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="43848-122">Si vous voulez créer une application web, choisissez le modèle de projet **Application web ASP.NET**, puis sélectionnez **MVC**.</span><span class="sxs-lookup"><span data-stu-id="43848-122">If you want to create a web app, choose the **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="43848-123">Pour plus d’informations, consultez la rubrique [Création d’une application web ASP.NET dans Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) .</span><span class="sxs-lookup"><span data-stu-id="43848-123">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="43848-124">Ouvrez le menu contextuel de la solution et choisissez **Valider**.</span><span class="sxs-lookup"><span data-stu-id="43848-124">Open the shortcut menu for the solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="43848-125">Si vous utilisez Git dans Visual Studio Team Services pour la première fois, vous devez fournir des informations pour vous identifier dans Git.</span><span class="sxs-lookup"><span data-stu-id="43848-125">If this is the first time you've used Git in Visual Studio Team Services, you'll need to provide some information to identify yourself in Git.</span></span> <span data-ttu-id="43848-126">Dans la zone **Modifications en attente** de **Team Explorer**, entrez votre nom d’utilisateur et votre adresse de messagerie.</span><span class="sxs-lookup"><span data-stu-id="43848-126">In the **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="43848-127">Entrez un commentaire pour la validation, puis sélectionnez le bouton **Valider** .</span><span class="sxs-lookup"><span data-stu-id="43848-127">Enter a comment for the commit and then choose the **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="43848-128">Notez les options à inclure ou exclure quand vous archivez des modifications spécifiques.</span><span class="sxs-lookup"><span data-stu-id="43848-128">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="43848-129">Si les modifications voulues sont exclues, choisissez **Tout inclure**.</span><span class="sxs-lookup"><span data-stu-id="43848-129">If the changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="43848-130">Vous avez maintenant validé les modifications dans votre copie locale du référentiel.</span><span class="sxs-lookup"><span data-stu-id="43848-130">You've now committed the changes in your local copy of the repository.</span></span> <span data-ttu-id="43848-131">Synchronisez ensuite ces modifications avec le serveur en choisissant le lien **Synchronisation** .</span><span class="sxs-lookup"><span data-stu-id="43848-131">Next, sync those changes with the server by choosing the **Sync** link.</span></span>

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="43848-132">3 : Connexion du projet à Azure</span><span class="sxs-lookup"><span data-stu-id="43848-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="43848-133">Vous avez maintenant un référentiel Git dans Visual Studio Team Services contenant du code source : vous êtes prêt à connecter votre référentiel Git à Azure.</span><span class="sxs-lookup"><span data-stu-id="43848-133">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready to connect your git repository to Azure.</span></span>  <span data-ttu-id="43848-134">Dans le [portail Azure Classic](http://go.microsoft.com/fwlink/?LinkID=213885), sélectionnez votre service cloud ou application web, ou créez-en un en sélectionnant l’icône + en bas à gauche et en choisissant **Service cloud** ou **Application web**, puis **Création rapide**.</span><span class="sxs-lookup"><span data-stu-id="43848-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the + icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="43848-135">Pour les Cloud Services, sélectionnez le lien **Configurer la publication avec Visual Studio Team Services** .</span><span class="sxs-lookup"><span data-stu-id="43848-135">For cloud services, choose the **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="43848-136">Pour les applications web, cliquez sur le lien **Configurer le déploiement à partir du contrôle de code source** .</span><span class="sxs-lookup"><span data-stu-id="43848-136">For web apps, choose the **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="43848-137">Dans l'Assistant, tapez le nom de votre compte Visual Studio Team Services dans la zone de texte et choisissez le lien **Autoriser maintenant** .</span><span class="sxs-lookup"><span data-stu-id="43848-137">In the wizard, type the name of your Visual Studio Team Services account in the textbox and choose the **Authorize Now** link.</span></span> <span data-ttu-id="43848-138">Vous serez peut-être invité à vous connecter.</span><span class="sxs-lookup"><span data-stu-id="43848-138">You might be asked to sign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="43848-139">Dans la boîte de dialogue contextuelle **Demande de connexion**, sélectionnez **Accepter** pour autoriser Azure à configurer votre projet d’équipe dans Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="43848-139">In the **Connection Request** pop-up dialog, choose **Accept** to authorize Azure to configure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="43848-140">Si la procédure d’autorisation réussit, une zone déroulante affiche la liste de vos projets d’équipe Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="43848-140">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="43848-141">Sélectionnez le nom du projet d'équipe que vous avez créé aux étapes précédentes et choisissez la coche de l'Assistant.</span><span class="sxs-lookup"><span data-stu-id="43848-141">Select the name of team project that you created in the previous steps, and choose the wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="43848-142">La prochaine fois que vous placerez une validation dans votre référentiel, Visual Studio Team Services génèrera et déploiera votre projet dans Azure.</span><span class="sxs-lookup"><span data-stu-id="43848-142">The next time you push a commit to your repository, Visual Studio Team Services will build and deploy your project to Azure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="43848-143">4 : Déclenchement d'une régénération et redéploiement de votre projet</span><span class="sxs-lookup"><span data-stu-id="43848-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="43848-144">Dans Visual Studio, ouvrez un fichier et modifiez-le.</span><span class="sxs-lookup"><span data-stu-id="43848-144">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="43848-145">Par exemple, modifiez le fichier `_Layout.cshtml` sous le dossier Views\\Shared dans un rôle Web MVC.</span><span class="sxs-lookup"><span data-stu-id="43848-145">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="43848-146">Modifiez le texte du pied de page du site et enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="43848-146">Edit the footer text for the site and save the file.</span></span>
   
    ![][18]
3. <span data-ttu-id="43848-147">Dans l’**Explorateur de solutions**, ouvrez le menu contextuel du nœud de la solution, du nœud du projet ou du fichier que vous avez modifié, puis sélectionnez **Valider**.</span><span class="sxs-lookup"><span data-stu-id="43848-147">In **Solution Explorer**, open the shortcut menu for the solution node, project node, or the file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="43848-148">Tapez un commentaire et sélectionnez **Valider**.</span><span class="sxs-lookup"><span data-stu-id="43848-148">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="43848-149">Sélectionnez le lien **Synchronisation** .</span><span class="sxs-lookup"><span data-stu-id="43848-149">Choose the **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="43848-150">Sélectionnez le lien **Pousser** pour placer votre validation dans le référentiel dans Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="43848-150">Choose the **Push** link to push your commit to the repository in Visual Studio Team Services.</span></span> <span data-ttu-id="43848-151">(Vous pouvez également utiliser le bouton **Synchronisation** pour copier vos validations dans le référentiel.</span><span class="sxs-lookup"><span data-stu-id="43848-151">(You can also use the **Sync** button to copy your commits to the repository.</span></span> <span data-ttu-id="43848-152">La différence est que **Synchronisation** extrait également les dernières modifications du référentiel).</span><span class="sxs-lookup"><span data-stu-id="43848-152">The difference is that **Sync** also pulls the latest changes from the repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="43848-153">Choisissez le bouton **Accueil** pour revenir à la page d’accueil de **Team Explorer**.</span><span class="sxs-lookup"><span data-stu-id="43848-153">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="43848-154">Choisissez **Builds** pour afficher les builds en cours.</span><span class="sxs-lookup"><span data-stu-id="43848-154">Choose **Builds** to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="43848-155">**Team Explorer** indique qu’une build est disponible pour archivage.</span><span class="sxs-lookup"><span data-stu-id="43848-155">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="43848-156">Double-cliquez sur le nom de la build en cours pour afficher un journal détaillé de la génération.</span><span class="sxs-lookup"><span data-stu-id="43848-156">To view a detailed log as the build progresses, double-click the name of the build in progress.</span></span>
10. <span data-ttu-id="43848-157">Pendant la création de la build, examinez la définition de build créée lorsque vous avez utilisé l'Assistant pour la liaison à Azure.</span><span class="sxs-lookup"><span data-stu-id="43848-157">While the build is in-progress, take a look at the build definition that was created when you used the wizard to link to Azure.</span></span>  <span data-ttu-id="43848-158">Ouvrez le menu contextuel de la définition de build et choisissez **Modifier la définition de build**.</span><span class="sxs-lookup"><span data-stu-id="43848-158">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="43848-159">Sous l’onglet **Déclencher** , vous allez voir que la définition de build prévoit par défaut un processus de génération pour chaque archivage.</span><span class="sxs-lookup"><span data-stu-id="43848-159">In the **Trigger** tab, you will see that the build definition is set to build on every check-in, by default.</span></span> <span data-ttu-id="43848-160">(Pour un service cloud, Visual Studio Team Services génère et déploie automatiquement la branche principale dans l'environnement intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="43848-160">(For a cloud service, Visual Studio Team Services builds and deploys the master branch to the staging environment automatically.</span></span> <span data-ttu-id="43848-161">Vous devez quand même effectuer une opération manuelle pour le déploiement dans le site Web en activité.</span><span class="sxs-lookup"><span data-stu-id="43848-161">You still have to do a manual step to deploy to the live site.</span></span> <span data-ttu-id="43848-162">Pour une application web qui ne comporte pas d’environnement intermédiaire, elle déploie la branche principale directement dans le site en activité.</span><span class="sxs-lookup"><span data-stu-id="43848-162">For a web app that doesn't have staging environment, it deploys the master branch directly to the live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="43848-163">Sous l’onglet **Processus** , vous pouvez voir que l’environnement de déploiement est défini sur le nom de votre service cloud ou application web.</span><span class="sxs-lookup"><span data-stu-id="43848-163">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="43848-164">Spécifiez des valeurs pour les propriétés si vous souhaitez d'autres valeurs que celles par défaut.</span><span class="sxs-lookup"><span data-stu-id="43848-164">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="43848-165">Les propriétés de publication dans Azure se trouvent dans la section **Déploiement** ; vous devrez peut-être configurer également les paramètres MSBuild.</span><span class="sxs-lookup"><span data-stu-id="43848-165">The properties for Azure publishing are in the **Deployment** section, and you might also need to set MSBuild parameters.</span></span> <span data-ttu-id="43848-166">Exemple : dans un projet de service cloud, pour spécifier la configuration d’un autre service que « Cloud », configurez les paramètres MSbuild avec `/p:TargetProfile=[YourProfile]` où *[YourProfile]* correspond à un fichier de configuration de service avec un nom tel que ServiceConfiguration.*YourProfile*.cscfg.</span><span class="sxs-lookup"><span data-stu-id="43848-166">For example, in a cloud service project, to specify a service configuration other than "Cloud", set the MSbuild parameters to `/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="43848-167">Le tableau suivant présente les propriétés disponibles dans la section **Déploiement** :</span><span class="sxs-lookup"><span data-stu-id="43848-167">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="43848-168">Propriété</span><span class="sxs-lookup"><span data-stu-id="43848-168">Property</span></span> | <span data-ttu-id="43848-169">Valeur par défaut</span><span class="sxs-lookup"><span data-stu-id="43848-169">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="43848-170">Autoriser les certificats non approuvés</span><span class="sxs-lookup"><span data-stu-id="43848-170">Allow Untrusted Certificates</span></span> |<span data-ttu-id="43848-171">Si cette propriété a la valeur false, des certificats SSL doivent être signés par une autorité racine.</span><span class="sxs-lookup"><span data-stu-id="43848-171">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="43848-172">Autoriser la mise à niveau</span><span class="sxs-lookup"><span data-stu-id="43848-172">Allow Upgrade</span></span> |<span data-ttu-id="43848-173">Permet au déploiement de mettre à jour un déploiement existant au lieu d'en créer un.</span><span class="sxs-lookup"><span data-stu-id="43848-173">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="43848-174">Conserve l'adresse IP.</span><span class="sxs-lookup"><span data-stu-id="43848-174">Preserves the IP address.</span></span> |
    | <span data-ttu-id="43848-175">Ne pas supprimer</span><span class="sxs-lookup"><span data-stu-id="43848-175">Do Not Delete</span></span> |<span data-ttu-id="43848-176">Si cette propriété a la valeur true, ne remplacez pas un déploiement sans rapport (la mise à niveau est autorisée).</span><span class="sxs-lookup"><span data-stu-id="43848-176">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="43848-177">Chemin d'accès des paramètres de déploiement</span><span class="sxs-lookup"><span data-stu-id="43848-177">Path to Deployment Settings</span></span> |<span data-ttu-id="43848-178">Chemin d’accès à votre fichier .pubxml pour un site Web, relatif au dossier racine du référentiel.</span><span class="sxs-lookup"><span data-stu-id="43848-178">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="43848-179">Ignorée pour les services cloud.</span><span class="sxs-lookup"><span data-stu-id="43848-179">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="43848-180">Environnement de déploiement SharePoint</span><span class="sxs-lookup"><span data-stu-id="43848-180">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="43848-181">Identique au nom du service.</span><span class="sxs-lookup"><span data-stu-id="43848-181">The same as the service name.</span></span> |
    | <span data-ttu-id="43848-182">Environnement de déploiement Azure</span><span class="sxs-lookup"><span data-stu-id="43848-182">Azure Deployment Environment</span></span> |<span data-ttu-id="43848-183">Nom de l’application web ou du service cloud</span><span class="sxs-lookup"><span data-stu-id="43848-183">The web app or cloud service name.</span></span> |
14. <span data-ttu-id="43848-184">À ce stade, la création de la build doit être terminée.</span><span class="sxs-lookup"><span data-stu-id="43848-184">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="43848-185">Si vous double-cliquez sur le nom de la build, Visual Studio affiche un **Résumé de la build**, y compris tous les résultats de test provenant de projets de test unitaires associés.</span><span class="sxs-lookup"><span data-stu-id="43848-185">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="43848-186">Dans le [portail Azure Classic](http://go.microsoft.com/fwlink/?LinkID=213885), vous pouvez afficher le déploiement associé sous l’onglet **Déploiements** quand l’environnement intermédiaire est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="43848-186">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="43848-187">Accédez à l'URL de votre site.</span><span class="sxs-lookup"><span data-stu-id="43848-187">Browse to your site's URL.</span></span> <span data-ttu-id="43848-188">Pour une application web, sélectionnez simplement le bouton **Parcourir** dans le portail.</span><span class="sxs-lookup"><span data-stu-id="43848-188">For a web app, just choose  the **Browse** button in the portal.</span></span> <span data-ttu-id="43848-189">Dans le cas d’un service cloud, choisissez l’URL dans la section **Aperçu rapide** de la page **Tableau de bord** représentant l’environnement intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="43848-189">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment.</span></span>
    
    <span data-ttu-id="43848-190">Les déploiements résultant de l'intégration continue de services cloud sont publiés dans l'environnement intermédiaire par défaut.</span><span class="sxs-lookup"><span data-stu-id="43848-190">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="43848-191">Vous pouvez changer cela en définissant la propriété **Environnement du service cloud de substitution** sur **Production**.</span><span class="sxs-lookup"><span data-stu-id="43848-191">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="43848-192">Cet écran indique où se trouve l’URL du site dans la page du tableau de bord du service cloud.</span><span class="sxs-lookup"><span data-stu-id="43848-192">Here's where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="43848-193">Un nouvel onglet de navigateur apparaît pour afficher votre site en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="43848-193">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="43848-194">Si vous apportez d'autres modifications à votre projet, vous déclenchez d'autres builds et vous accumulez plusieurs déploiements.</span><span class="sxs-lookup"><span data-stu-id="43848-194">If you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="43848-195">Le plus récent est marqué comme Actif.</span><span class="sxs-lookup"><span data-stu-id="43848-195">The latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="43848-196">5 : Redéploiement d'une build antérieure</span><span class="sxs-lookup"><span data-stu-id="43848-196">5: Redeploy an earlier build</span></span>
<span data-ttu-id="43848-197">Cette étape est facultative.</span><span class="sxs-lookup"><span data-stu-id="43848-197">This step is optional.</span></span> <span data-ttu-id="43848-198">Dans le portail Azure Classic, choisissez un déploiement antérieur et sélectionnez **Redéployer** pour revenir à un archivage antérieur de votre site.</span><span class="sxs-lookup"><span data-stu-id="43848-198">In the Azure classic portal, choose an earlier deployment and choose **Redeploy** to rewind your site to an earlier check-in.</span></span> <span data-ttu-id="43848-199">Notez que cela déclenche une nouvelle génération dans TFS et crée une entrée dans l’historique de votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="43848-199">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="43848-200">6 : Modification du déploiement de production</span><span class="sxs-lookup"><span data-stu-id="43848-200">6: Change the Production deployment</span></span>
<span data-ttu-id="43848-201">Une fois que vous êtes prêt, vous pouvez promouvoir l’environnement intermédiaire en environnement de production en sélectionnant **Basculer** dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="43848-201">When you are ready, you can promote the Staging environment to the Production environment by choosing **Swap** in the Azure classic portal.</span></span> <span data-ttu-id="43848-202">L'environnement intermédiaire récemment déployé passe à l'état de production et l'environnement de production précédent, le cas échéant, devient un environnement intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="43848-202">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="43848-203">Le déploiement actif peut être différent pour les environnements de production et intermédiaire, mais l'historique de déploiement des builds récentes est identique quel que soit l'environnement.</span><span class="sxs-lookup"><span data-stu-id="43848-203">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="43848-204">7 : Déploiement à partir d’une branche en cours d’utilisation</span><span class="sxs-lookup"><span data-stu-id="43848-204">7: Deploy from a working branch.</span></span>
<span data-ttu-id="43848-205">Lorsque vous utilisez Git, vous apportez généralement des modifications à une branche en cours d'utilisation et les intégrez dans une branche principale lorsque votre déploiement est terminé.</span><span class="sxs-lookup"><span data-stu-id="43848-205">When you use Git, you usually make changes in a working branch and integrate into the master branch when your development reaches a finished state.</span></span> <span data-ttu-id="43848-206">Pendant la phase de déploiement d'un projet, vous pouvez générer et déployer la branche en cours d'utilisation dans Azure.</span><span class="sxs-lookup"><span data-stu-id="43848-206">During the development phase of a project, you'll want to build and deploy the working branch to Azure.</span></span>

1. <span data-ttu-id="43848-207">Dans **Team Explorer**, sélectionnez le bouton **Accueil**, puis le bouton **Branches**.</span><span class="sxs-lookup"><span data-stu-id="43848-207">In **Team Explorer**, choose the **Home** button and then choose the **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="43848-208">Sélectionnez le lien **Nouvelle branche** .</span><span class="sxs-lookup"><span data-stu-id="43848-208">Choose the **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="43848-209">Entrez le nom d’une branche (ex. « Utilisation en cours ») et sélectionnez **Créer une branche**.</span><span class="sxs-lookup"><span data-stu-id="43848-209">Enter the name of the branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="43848-210">pour créer une branche locale.</span><span class="sxs-lookup"><span data-stu-id="43848-210">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="43848-211">Publiez la branche.</span><span class="sxs-lookup"><span data-stu-id="43848-211">Publish the branch.</span></span> <span data-ttu-id="43848-212">Sélectionnez le nom de la branche dans **Branches non publiées**, puis **Publier**.</span><span class="sxs-lookup"><span data-stu-id="43848-212">Choose the branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="43848-213">Par défaut, seules les modifications apportées à la branche principale déclenchent une génération continue.</span><span class="sxs-lookup"><span data-stu-id="43848-213">By default, only changes to the master branch trigger a continuous build.</span></span> <span data-ttu-id="43848-214">Pour configurer une génération continue pour une branche en cours d’utilisation, sélectionnez la page **Builds** dans **Team Explorer** et sélectionnez **Modifier la définition de build**.</span><span class="sxs-lookup"><span data-stu-id="43848-214">To set up continuous build for a working branch, choose the **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="43848-215">Ouvrez l'onglet **Paramètres de la source** .</span><span class="sxs-lookup"><span data-stu-id="43848-215">Open the **Source Settings** tab.</span></span> <span data-ttu-id="43848-216">Sous **Branches surveillées pour l’intégration et la génération continue**, sélectionnez **Cliquez ici pour ajouter une ligne**.</span><span class="sxs-lookup"><span data-stu-id="43848-216">Under **Monitored branches for continuous integration and build**, choose **Click here to add a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="43848-217">Spécifiez la branche que vous avez créée (par ex. refs/heads/working).</span><span class="sxs-lookup"><span data-stu-id="43848-217">Specify the branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="43848-218">Modifiez le code, ouvrez le menu contextuel du fichier modifié et sélectionnez **Valider**.</span><span class="sxs-lookup"><span data-stu-id="43848-218">Make a change in the code, open the shortcut menu for the changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="43848-219">Sélectionnez le lien **Validations non synchronisées**, puis le bouton **Synchronisation** ou le lien **Pousser** pour copier les modifications dans la copie de la branche en cours d’utilisation dans Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="43848-219">Choose the **Unsynced Commits** link, and choose  the **Sync** button or the **Push** link to copy the changes to the copy of the working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="43848-220">Accédez à la vue **Builds** et recherchez la build qui vient d'être déclenchée pour la branche en cours d'utilisation.</span><span class="sxs-lookup"><span data-stu-id="43848-220">Navigate to the **Builds** view and find the build that just got triggered for the working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43848-221">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="43848-221">Next steps</span></span>
<span data-ttu-id="43848-222">Pour obtenir des conseils supplémentaires sur l’utilisation de Git avec Visual Studio Team Services, consultez la page [Développer et partager votre code dans Git à l’aide de Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) ; pour en savoir plus sur l’utilisation d’un référentiel Git qui n’est pas géré par Visual Studio Team Services pour la publication dans Azure, consultez la page [Déploiement continu à l’aide de Git dans Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="43848-222">To learn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services to publish to Azure, see [Continuous Deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="43848-223">Pour en savoir plus sur Visual Studio Team Services, consultez [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="43848-223">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
