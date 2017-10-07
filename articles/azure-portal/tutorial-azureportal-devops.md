---
title: "Didacticiel : DevOps hello portail Azure | Documents Microsoft"
description: "En savoir plus hello différents flux de travail DevOps Bonjour portail Azure."
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: 4c32dbbd4e4b1c3809ef4b01e1496e350183ebde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-devops-with-hello-azure-portal"></a><span data-ttu-id="0330d-103">Didacticiel : DevOps hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="0330d-103">Tutorial: DevOps with hello Azure Portal</span></span>
<span data-ttu-id="0330d-104">Hello plateforme Azure est plein de flux de travail flexible DevOps.</span><span class="sxs-lookup"><span data-stu-id="0330d-104">hello Azure platform is full of flexible DevOps workflows.</span></span> <span data-ttu-id="0330d-105">Dans ce didacticiel, vous découvrez comment tooleverage les fonctionnalités de hello de toodevelop du portail Azure hello, tester, déployer, résoudre les problèmes, surveiller et gérer des applications en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0330d-105">In this tutorial, you learn how tooleverage hello capabilities of hello Azure Portal toodevelop, test, deploy, troubleshoot, monitor, and manage running applications.</span></span> <span data-ttu-id="0330d-106">Ce didacticiel se concentre sur les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="0330d-106">This tutorial focuses on hello following:</span></span>

1. <span data-ttu-id="0330d-107">Création d’une application web et possibilité de déploiement continu</span><span class="sxs-lookup"><span data-stu-id="0330d-107">Creating a web app and enabling continuous deployment</span></span>
2. <span data-ttu-id="0330d-108">Développement et test d’une application</span><span class="sxs-lookup"><span data-stu-id="0330d-108">Develop and test an app</span></span>
3. <span data-ttu-id="0330d-109">Surveillance et dépannage d’une application</span><span class="sxs-lookup"><span data-stu-id="0330d-109">Monitoring and Troubleshooting an app</span></span>
4. <span data-ttu-id="0330d-110">Tâches de gestion des applications générales</span><span class="sxs-lookup"><span data-stu-id="0330d-110">General application management tasks</span></span>

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a><span data-ttu-id="0330d-111">Création d’une application web et possibilité de déploiement continu</span><span class="sxs-lookup"><span data-stu-id="0330d-111">Creating a web app and enabling continuous deployment</span></span>
<span data-ttu-id="0330d-112">Créer une application Web avec [Azure App Service](https://azure.microsoft.com/services/app-service/), que vous allez utiliser dans le reste de hello de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="0330d-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in hello rest of this tutorial.</span></span> <span data-ttu-id="0330d-113">Vous allez d’abord activer le déploiement continu à partir de votre référentiel de code source dans notre environnement Azure en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0330d-113">You’ll initially enable continuous deployment from your source code repository into our running Azure environment.</span></span>

1. <span data-ttu-id="0330d-114">Connectez-vous à hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="0330d-114">Sign into hello Azure Portal</span></span>
2. <span data-ttu-id="0330d-115">Choisissez **des Services d’application** &gt; **icône Ajouter** et entrez un nom, choisissez votre abonnement et créer un nouveau tooserve de groupe de ressources en tant que conteneur hello pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group tooserve as hello container for hello service.</span></span>
   
   <span data-ttu-id="0330d-116">Les groupes de ressources permettent de toomanage différents aspects de la solution hello telles que la facturation, déploiements et de surveillance sous la forme d’un seul groupe via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0330d-116">Resource groups allow you toomanage various aspects of hello solution such as billing, deployments and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>
   
   ![image1][image1]
3. <span data-ttu-id="0330d-118">Après quelques instants, votre App Service est créé.</span><span class="sxs-lookup"><span data-stu-id="0330d-118">After a few moments, your app service is created.</span></span> <span data-ttu-id="0330d-119">Prendre des différentes options de menu pour le service de hello hello de tooexplore quelques minutes dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-119">Take a few minutes tooexplore hello various menu options for hello service in hello portal.</span></span>
   
   ![image2][image2]    
4. <span data-ttu-id="0330d-121">Cliquez sur les URL hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-121">Click hello URL.</span></span> <span data-ttu-id="0330d-122">Notez les diverses options disponibles pour les outils et des référentiels hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-122">Notice hello variety of available choices for tools and repositories.</span></span> <span data-ttu-id="0330d-123">Vous pouvez également utiliser des langages de hello et infrastructures de votre choix, y compris .NET, Java et Ruby.</span><span class="sxs-lookup"><span data-stu-id="0330d-123">You can also use hello languages and frameworks of your choice including .NET, Java, and Ruby.</span></span>
   
   ![image3][image3]    
5. <span data-ttu-id="0330d-125">Hello portail Azure permet un déploiement continu un processus simple qui implique quelques étapes simples.</span><span class="sxs-lookup"><span data-stu-id="0330d-125">hello Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span></span> <span data-ttu-id="0330d-126">Bonjour portail Azure, choisissez les paramètres à partir de l’icône hello pour le service d’application hello que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="0330d-126">In hello Azure portal, choose settings from hello icon for hello app service you just created.</span></span>
   
   ![image4][image4]
   
   <span data-ttu-id="0330d-128">À partir du panneau hello qui s’ouvre sur hello droite, faites défiler toohello section de la publication.</span><span class="sxs-lookup"><span data-stu-id="0330d-128">From hello blade that opens on hello right, scroll toohello publishing section.</span></span>
   
   ![image5][image5]
6. <span data-ttu-id="0330d-130">Ensuite, configurez certains paramètres tooenable un déploiement continu pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-130">Next, configure some settings tooenable continuous deployment for hello app.</span></span> <span data-ttu-id="0330d-131">Cliquez sur Source du déploiement, puis sur Choisir la source.</span><span class="sxs-lookup"><span data-stu-id="0330d-131">Click Deployment Source and then click Choose Source.</span></span> <span data-ttu-id="0330d-132">Notez les diverses hello des options pour les sources de référentiel.</span><span class="sxs-lookup"><span data-stu-id="0330d-132">Notice hello variety of options you have for repository sources.</span></span>
   
   ![image6][image6]
7. <span data-ttu-id="0330d-134">Pour cet exemple, sélectionnez GitHub.</span><span class="sxs-lookup"><span data-stu-id="0330d-134">For this example choose GitHub.</span></span> <span data-ttu-id="0330d-135">Éventuellement, choisissez hello le référentiel de votre choix et configurer les informations d’identification d’autorisation de hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-135">Optionally choose hello repository of your choice and setup hello authorization credentials.</span></span>
   
   ![image7][image7]
8. <span data-ttu-id="0330d-137">Après le référentiel de tooyour d’autorisation, vous pouvez ensuite choisir un projet et la branche que vous souhaitez toodeploy.</span><span class="sxs-lookup"><span data-stu-id="0330d-137">After authorization tooyour repository, you can then choose a project and branch you wish toodeploy.</span></span> <span data-ttu-id="0330d-138">Plusieurs exemples fictifs sont répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0330d-138">There are several fictitious sample examples listed below.</span></span>
   
   ![image8][image8]
9. <span data-ttu-id="0330d-140">Une fois votre projet et votre branche choisis, cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="0330d-140">Once you choose your project and branch, click ok.</span></span> <span data-ttu-id="0330d-141">Vous devez commencer toosee des notifications d’un déploiement.</span><span class="sxs-lookup"><span data-stu-id="0330d-141">You should start toosee notifications of a deployment.</span></span>
   
   ![image9][image9]
10. <span data-ttu-id="0330d-143">Accédez tooGitHub arrière toosee hello webhook qui a été créé le référentiel de contrôle de source de hello toointegrate avec Azure.</span><span class="sxs-lookup"><span data-stu-id="0330d-143">Navigate back tooGitHub toosee hello webhook that was created toointegrate hello source control repo with Azure.</span></span> <span data-ttu-id="0330d-144">Hello portail Azure permet l’intégration avec GitHub avec seulement quelques étapes simples.</span><span class="sxs-lookup"><span data-stu-id="0330d-144">hello Azure Portal enables integration with GitHub with only a few simple steps.</span></span>
    
    ![image10][image10]
11. <span data-ttu-id="0330d-146">toodemonstrate le déploiement continu, vous ajouter rapidement certains référentiel de contenu toohello.</span><span class="sxs-lookup"><span data-stu-id="0330d-146">toodemonstrate continuous deployment, you quickly add some content toohello repository.</span></span> <span data-ttu-id="0330d-147">Pour obtenir un exemple simple, ajoutez un référentiel GitHub d’exemples texte fichier tooa.</span><span class="sxs-lookup"><span data-stu-id="0330d-147">For a simple example, add a sample text file tooa GitHub repo.</span></span> <span data-ttu-id="0330d-148">Vous êtes libre toouse .NET, Ruby, Python ou un autre type d’application à l’aide du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="0330d-148">You are free toouse .NET, Ruby, Python, or some other type of application with App Service.</span></span> <span data-ttu-id="0330d-149">Pensez libre tooadd un fichier texte, référentiel de toohello application ASP.NET MVC, Java ou Ruby de votre choix.</span><span class="sxs-lookup"><span data-stu-id="0330d-149">Feel free tooadd a text file, ASP.NET MVC, Java, or Ruby application toohello repo of your choice.</span></span>
    
    ![image11][image11]
12. <span data-ttu-id="0330d-151">Après avoir validé le référentiel de tooyour de modifications, vous voyez un nouveau déploiement lancer dans la zone de notification de portail de hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-151">After committing changes tooyour repository, you see a new deployment initiate in hello portal notifications area.</span></span> <span data-ttu-id="0330d-152">Si vous ne voyez pas rapidement modifications après avoir validé tooyour référentiel, cliquez sur Synchroniser.</span><span class="sxs-lookup"><span data-stu-id="0330d-152">Click Sync if you do not quickly see changes after committing tooyour repository.</span></span>
    
    ![image12][image12]
13. <span data-ttu-id="0330d-154">À ce stade, si vous essayez de chargez la page hello pour le service de l’application hello, vous pouvez recevoir une erreur 403.</span><span class="sxs-lookup"><span data-stu-id="0330d-154">At this point, if you try and load hello page for hello app service, you may receive a 403 error.</span></span> <span data-ttu-id="0330d-155">Dans cet exemple, il est, car il n’existe aucune configuration de document par défaut pour la page hello tel qu’un fichier comme index.htm ou default.html.</span><span class="sxs-lookup"><span data-stu-id="0330d-155">In this example, it is because there is no typical default document setup for hello page such as a file like index.htm or default.html.</span></span> <span data-ttu-id="0330d-156">Vous pouvez y remédier rapidement avec hello pour les outils Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0330d-156">You can quickly remedy this with hello tooling in hello Azure Portal.</span></span>  <span data-ttu-id="0330d-157">Bonjour portail Azure, choisissez les paramètres &gt; paramètres de l’Application.</span><span class="sxs-lookup"><span data-stu-id="0330d-157">In hello Azure Portal choose Settings &gt; Application Settings.</span></span>
    
     ![image13][image13]
14. <span data-ttu-id="0330d-159">Un panneau regroupant les paramètres de l’application s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="0330d-159">A blade opens for application settings.</span></span> <span data-ttu-id="0330d-160">Entrez le nom hello de page de hello « SamplePage.html » et cliquez sur Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="0330d-160">Enter hello name of hello page “SamplePage.html” and click Save.</span></span> <span data-ttu-id="0330d-161">Prendre des autres paramètres hello de tooexplore quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="0330d-161">Take a few minutes tooexplore hello other settings.</span></span>
    
    ![image14][image14]
15. <span data-ttu-id="0330d-163">Si vous le souhaitez actualiser votre tooensure URL de navigateur vous voyez les modifications hello attendu.</span><span class="sxs-lookup"><span data-stu-id="0330d-163">Optionally refresh your browser URL tooensure you see hello expected changes.</span></span> <span data-ttu-id="0330d-164">Dans ce cas, il est de texte simple maintenant remplissage page de hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-164">In this case, there is some simple text now populating hello page.</span></span> <span data-ttu-id="0330d-165">Chaque référentiel toohello de modification supplémentaire se traduirait par un nouveau déploiement automatique.</span><span class="sxs-lookup"><span data-stu-id="0330d-165">Each additional change toohello repository would result in a new automatic deployment.</span></span>
    
    ![image15][image15]
    
    <span data-ttu-id="0330d-167">L’activation d’un déploiement continu avec hello portail Azure est une expérience simple.</span><span class="sxs-lookup"><span data-stu-id="0330d-167">Enabling continuous deployment with hello Azure Portal is an easy experience.</span></span> <span data-ttu-id="0330d-168">Vous pouvez également générer des pipelines de version plus complexes et utiliser de nombreuses autres techniques avec contrôle de code source existant et d’intégration continue systèmes toodeploy tooAzure, telles que tirant parti de génération automatisé et les systèmes de gestion de version.</span><span class="sxs-lookup"><span data-stu-id="0330d-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems toodeploy tooAzure, such as leveraging automated build and release management systems.</span></span>

## <a name="develop-and-test-an-app"></a><span data-ttu-id="0330d-169">Développement et test d’une application</span><span class="sxs-lookup"><span data-stu-id="0330d-169">Develop and test an app</span></span>
<span data-ttu-id="0330d-170">Ensuite, modifiez toohello code base et déployer rapidement ces modifications.</span><span class="sxs-lookup"><span data-stu-id="0330d-170">Next, make some changes toohello code base and rapidly deploy those changes.</span></span> <span data-ttu-id="0330d-171">Vous serez également configurer certains tests de performances pour l’application Web hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-171">You will also setup up some performance testing for hello Web app.</span></span>

1. <span data-ttu-id="0330d-172">Bonjour Azure Portal choisir les Services d’application à partir du volet de navigation hello et recherchez votre application de Service.</span><span class="sxs-lookup"><span data-stu-id="0330d-172">In hello Azure Portal choose App Services from hello navigation pane, and locate your App Service.</span></span>
   
   ![image16][image16]
2. <span data-ttu-id="0330d-174">Cliquez sur Outils</span><span class="sxs-lookup"><span data-stu-id="0330d-174">Click Tools</span></span>
   
   ![image17][image17]
3. <span data-ttu-id="0330d-176">Notez que hello catégorie sous Outils de développement.</span><span class="sxs-lookup"><span data-stu-id="0330d-176">Notice hello develop category under Tools.</span></span> <span data-ttu-id="0330d-177">Il existe plusieurs outils utiles ici qui nous permettent de toowork avec les applications sans quitter hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0330d-177">There are several useful tools here that allow us toowork with apps without leaving hello Azure Portal.</span></span> <span data-ttu-id="0330d-178">Cliquez sur Console.</span><span class="sxs-lookup"><span data-stu-id="0330d-178">Click on Console.</span></span>
   
   ![image18][image18]
4. <span data-ttu-id="0330d-180">Dans la fenêtre de console hello, vous pouvez émettre des commandes actives pour votre application.</span><span class="sxs-lookup"><span data-stu-id="0330d-180">In hello console window, you can issue live commands for your app.</span></span> <span data-ttu-id="0330d-181">Commande de type hello dir et appuyez sur entrer.</span><span class="sxs-lookup"><span data-stu-id="0330d-181">Type hello dir command and hit enter.</span></span> <span data-ttu-id="0330d-182">Notez que les commandes nécessitant des privilèges élevés ne fonctionnent pas.</span><span class="sxs-lookup"><span data-stu-id="0330d-182">Note that commands requiring elevated privileges do not work.</span></span>
   
   ![image19][image19]
5. <span data-ttu-id="0330d-184">Replacer toohello développer catégorie et choisissez Visual Studio Online.</span><span class="sxs-lookup"><span data-stu-id="0330d-184">Move back toohello Develop category and choose Visual Studio Online.</span></span> <span data-ttu-id="0330d-185">Remarque : Visual Studio Online devient Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="0330d-185">Note: Visual Studio Online is now named Visual Studio Team Services.</span></span>
   
   ![image20][image20]
6. <span data-ttu-id="0330d-187">Basculer sur l’expérience d’édition dans le navigateur hello pour votre application.</span><span class="sxs-lookup"><span data-stu-id="0330d-187">Toggle on hello in-browser editing experience for your App.</span></span>
   
   ![image21][image21]
7. <span data-ttu-id="0330d-189">Une extension web pour votre application s’installe.</span><span class="sxs-lookup"><span data-stu-id="0330d-189">A web extension installs for your app.</span></span> <span data-ttu-id="0330d-190">Extensions rapidement et facilement ajoutent des fonctionnalités tooapps dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0330d-190">Extensions quickly and easily add functionality tooapps in Azure.</span></span> <span data-ttu-id="0330d-191">Notez que certaines des hello autres types d’extensions disponibles dans la capture d’écran hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0330d-191">Notice some of hello other extension types available in hello screenshot below.</span></span>
   
   ![image22][image22]
8. <span data-ttu-id="0330d-193">Une fois que hello extension Visual Studio Online est installé, cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="0330d-193">Once hello Visual Studio Online extension installs, click Go.</span></span>
   
   ![image23][image23]
9. <span data-ttu-id="0330d-195">Un navigateur onglet s’ouvre dans lequel vous consultez un développement IDE directement dans le navigateur de hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-195">A browser tab opens where you see a development IDE directly in hello browser.</span></span> <span data-ttu-id="0330d-196">Avis hello ci-dessous bénéficie dans Chrome.</span><span class="sxs-lookup"><span data-stu-id="0330d-196">Notice hello experience below is in Chrome.</span></span>
   
   ![image24][image24]
10. <span data-ttu-id="0330d-198">Vous pouvez effectuer plusieurs activités telles que les fichiers de la modifier, ajouter des fichiers et des dossiers et télécharger le contenu à partir du site en ligne hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-198">You can perform several activities such as edit files, add files and folders, and download content from hello live site.</span></span> <span data-ttu-id="0330d-199">Créez un fichier de SamplePage.html toohello édition rapide.</span><span class="sxs-lookup"><span data-stu-id="0330d-199">Make a quick edit toohello SamplePage.html file.</span></span>
    
    ![image25][image25]
11. <span data-ttu-id="0330d-201">Dans quelques instants, hello modifications sont automatiquement enregistrées.</span><span class="sxs-lookup"><span data-stu-id="0330d-201">In a few moments, hello changes are automatically saved.</span></span> <span data-ttu-id="0330d-202">Si vous accédez toohello arrière page, vous pouvez voir les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-202">If you navigate back toohello page, you can see hello changes.</span></span> <span data-ttu-id="0330d-203">Gardez à l’esprit que les modifications en direct ne sont généralement pas appropriées pour les environnements de production.</span><span class="sxs-lookup"><span data-stu-id="0330d-203">Keep in mind live edits like these are most likely not suitable for production environments.</span></span> <span data-ttu-id="0330d-204">Toutefois, les outils de hello rendent toomake très facile de rapides modifications pour le développement et les environnements de test.</span><span class="sxs-lookup"><span data-stu-id="0330d-204">However, hello tools make it very easy toomake quick changes for dev and test environments.</span></span>
    
    ![image26][image26]
    
    ![image27][image27]
12. <span data-ttu-id="0330d-207">Replacez le panneau d’outils toohello et sous la catégorie de développer hello, cliquez sur le Test de performances.</span><span class="sxs-lookup"><span data-stu-id="0330d-207">Move back toohello tools blade and under hello Develop category, click on Performance Test.</span></span>
    
    ![image28][image28]
13. <span data-ttu-id="0330d-209">Vous devez tooset un compte de services d’équipe.</span><span class="sxs-lookup"><span data-stu-id="0330d-209">You need tooset a team services account.</span></span> <span data-ttu-id="0330d-210">Pour plus d’informations, consultez la page [Créer un compte Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span><span class="sxs-lookup"><span data-stu-id="0330d-210">See here for more details: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span></span>
14. <span data-ttu-id="0330d-211">Cliquez sur Nouveau toocreate un test de performances.</span><span class="sxs-lookup"><span data-stu-id="0330d-211">Click on New toocreate a performance test.</span></span>
    
    ![image29][image29]
    
    <span data-ttu-id="0330d-213">Configurer hello différentes valeurs et cliquez sur Exécuter le Test bas hello hello boîte de dialogue tooinitiate un test de performances.</span><span class="sxs-lookup"><span data-stu-id="0330d-213">Configure hello various values and click Run Test at hello bottom of hello dialogue tooinitiate a performance test.</span></span>
    
    ![image30][image30]
    
    ![image31][image31]
15. <span data-ttu-id="0330d-216">Une fois le test de hello démarre l’exécution, vous pouvez surveiller l’état de hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-216">Once hello test starts running, you can monitor hello state.</span></span>
    
    ![image32][image32]
    
    <span data-ttu-id="0330d-218">Une fois le test de hello terminée, en cliquant sur le résultat de hello affiche plus de détails.</span><span class="sxs-lookup"><span data-stu-id="0330d-218">Once hello test finishes, clicking on hello result shows more details.</span></span>
    
    ![image33][image33]
16. <span data-ttu-id="0330d-220">Dans cet exemple, vous avez créé une petite série de tests, donc il est tooanalyze de données limité, mais vous pouvez consultez diverses mesures ainsi que réexécutez votre test à partir de cette vue.</span><span class="sxs-lookup"><span data-stu-id="0330d-220">In this example, you created a small test run, so there is limited data tooanalyze, but you can see various metrics as well as rerun your test from this view.</span></span> <span data-ttu-id="0330d-221">Hello portail Azure facilite la création, l’exécution et analyse des tests de performances web un processus simple.</span><span class="sxs-lookup"><span data-stu-id="0330d-221">hello Azure Portal makes creating, executing, and analyzing web performance tests an easy process.</span></span> <span data-ttu-id="0330d-222">Hello captures d’écran ci-dessous affichent les données de performances de hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-222">hello screenshots below display hello performance data.</span></span>
    
    ![image34][image34]
    
    ![image35][image35]
    
    ![image36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a><span data-ttu-id="0330d-226">Surveillance et dépannage d’une application</span><span class="sxs-lookup"><span data-stu-id="0330d-226">Monitoring and troubleshooting an app</span></span>
<span data-ttu-id="0330d-227">Azure fournit de nombreuses fonctionnalités de surveillance et de dépannage pour les applications en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0330d-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span></span>

1. <span data-ttu-id="0330d-228">Bonjour portail Azure pour notre application Web, sélectionnez Outils.</span><span class="sxs-lookup"><span data-stu-id="0330d-228">In hello Azure Portal for our Web app choose Tools.</span></span>
   
   ![image37][image37]
2. <span data-ttu-id="0330d-230">Sous catégorie de résolution des problèmes de hello, notez hello différentes options pour l’utilisation des problèmes potentiels d’outils tootroubleshoot avec une application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0330d-230">Under hello Troubleshoot category, notice hello various choices for using tools tootroubleshoot potential issues with a running app.</span></span> <span data-ttu-id="0330d-231">Vous pouvez par exemple analyser le trafic HTTP en direct, activer la réparation spontanée, afficher les journaux et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="0330d-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span></span>
   
   ![image38][image38]
3. <span data-ttu-id="0330d-233">Choisissez l’affichage de certains codes HTTP get tooquickly de métriques d’un Site.</span><span class="sxs-lookup"><span data-stu-id="0330d-233">Choose Site Metrics tooquickly get a view of some HTTP codes.</span></span>
   
   ![image39][image39]
4. <span data-ttu-id="0330d-235">Sélectionnez Diagnostics en tant que service.</span><span class="sxs-lookup"><span data-stu-id="0330d-235">Choose Diagnostics as a Service.</span></span> <span data-ttu-id="0330d-236">Choisissez votre type d’application, puis sélectionnez Exécuter.</span><span class="sxs-lookup"><span data-stu-id="0330d-236">Choose your application type, then choose Run.</span></span>
   
   ![image40][image40]
   
   <span data-ttu-id="0330d-238">La collecte commence.</span><span class="sxs-lookup"><span data-stu-id="0330d-238">A collection begins.</span></span>
   
   ![image41][image41]
5. <span data-ttu-id="0330d-240">Vous pouvez choisir les problèmes potentiels de hello journal approprié toodiagnose.</span><span class="sxs-lookup"><span data-stu-id="0330d-240">You may choose hello appropriate log toodiagnose potential issues.</span></span> <span data-ttu-id="0330d-241">Vous devez toosee de journalisation tooenable toutes les données disponibles hello options telles que les journaux HTTP.</span><span class="sxs-lookup"><span data-stu-id="0330d-241">You need tooenable logging toosee all of hello available data options such as HTTP Logs.</span></span>
   
   ![image42][image42]
   
   <span data-ttu-id="0330d-243">En cliquant sur le fichier d’image mémoire hello vous pouvez télécharger et analyser un DebugDiag toohelp de rapports d’analyse recherche les problèmes potentiels.</span><span class="sxs-lookup"><span data-stu-id="0330d-243">By clicking on hello Memory Dump file you can download and analyze a DebugDiag analysis report toohelp find potential issues.</span></span>
   
   ![image43][image43]
6. <span data-ttu-id="0330d-245">tooview plus de données, vous devez tooenable la journalisation supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="0330d-245">tooview more data, you need tooenable additional logging.</span></span> <span data-ttu-id="0330d-246">Bonjour portail Azure, accédez toohello Web app et choisissez les paramètres.</span><span class="sxs-lookup"><span data-stu-id="0330d-246">In hello Azure Portal, navigate toohello Web app and choose Settings.</span></span>
   
   ![image44][image44]
7. <span data-ttu-id="0330d-248">Faites défiler la liste des catégories de fonctionnalités toohello et choisissez les journaux de Diagnostic.</span><span class="sxs-lookup"><span data-stu-id="0330d-248">Scroll down toohello features category, and choose Diagnostic logs.</span></span>
   
      ![image45][image45]
8. <span data-ttu-id="0330d-250">Notez que hello diverses options pour la journalisation.</span><span class="sxs-lookup"><span data-stu-id="0330d-250">Notice hello various options for logging.</span></span> <span data-ttu-id="0330d-251">Activez la journalisation du serveur web et cliquez sur Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="0330d-251">Toggle on Web server logging and click save.</span></span>
   
   ![image46][image46]
9. <span data-ttu-id="0330d-253">Replacer la zone d’outils toohello pour l’application hello et choisissez Diagnostics en tant que service et cliquez sur Exécuter toorerun hello la collecte de données.</span><span class="sxs-lookup"><span data-stu-id="0330d-253">Move back toohello tools area for hello app and choose Diagnostics as a service and click Run toorerun hello data collection.</span></span>
   
   ![image47][image47]
10. <span data-ttu-id="0330d-255">Avec le paramètre d’enregistrement hello HTTP activé, vous voyez maintenant les données collectées pour les journaux HTTP.</span><span class="sxs-lookup"><span data-stu-id="0330d-255">With hello HTTP logging setting enabled, you now see data collected for HTTP Logs.</span></span>
    
    ![image48][image48]
11. <span data-ttu-id="0330d-257">En cliquant sur le fichier journal de hello HTML, vous produire un rapport basé sur le navigateur rich pour un examen approfondi.</span><span class="sxs-lookup"><span data-stu-id="0330d-257">By clicking hello HTML file log, you produce a rich browser-based report for further investigation.</span></span>
    
    ![image49][image49]
12. <span data-ttu-id="0330d-259">Replacer dans la section Outils toohello hello portail Azure pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-259">Move back toohello tools section in hello Azure Portal for hello app.</span></span> <span data-ttu-id="0330d-260">Faites défiler la section des outils toohello et choisissez Explorateur de processus.</span><span class="sxs-lookup"><span data-stu-id="0330d-260">Scroll toohello Tools section and choose Process Explorer.</span></span>
    
    ![image50][image50]
13. <span data-ttu-id="0330d-262">En choisissant Explorateur de processus, vous pouvez afficher plus d’informations sur les processus en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0330d-262">By choosing Process Explorer, you can view details about running processes.</span></span> <span data-ttu-id="0330d-263">Notez ci-dessous vous permettre Explorer le processus et même supprimer des processus à partir d’hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0330d-263">Notice below you can drill into processes and even kill processes all from hello Azure Portal.</span></span>
    
    ![image51][image51]
    
    ![image52][image52]
14. <span data-ttu-id="0330d-266">Replacez le panneau des paramètres toohello sur hello gauche.</span><span class="sxs-lookup"><span data-stu-id="0330d-266">Move back toohello Settings blade on hello left.</span></span> <span data-ttu-id="0330d-267">Cliquez sur Nouvelle demande de support.</span><span class="sxs-lookup"><span data-stu-id="0330d-267">Click New support request.</span></span>
    
    ![image53][image53]
15. <span data-ttu-id="0330d-269">À partir du panneau hello sur hello droite, vous pouvez remplir des détails sur les problèmes de hello, entrez les informations de contact et même télécharger des données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="0330d-269">From hello blade on hello right, you can fill out details about hello issues, enter contact information, and even upload diagnostic data.</span></span> <span data-ttu-id="0330d-270">Hello portail Azure permet de travailler avec prise en charge de Microsoft, une expérience transparente.</span><span class="sxs-lookup"><span data-stu-id="0330d-270">hello Azure Portal enables working with Microsoft support a seamless experience.</span></span>
    
    ![image54][image54]
    
    ![image55][image55]
    
    <span data-ttu-id="0330d-273">Hello portail Azure permet de fournir performante et familière pour les outils expériences toohelp moniteur et résoudre les problèmes de nos applications en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0330d-273">hello Azure Portal helps provide powerful and familiar tooling experiences toohelp monitor and troubleshoot our running applications.</span></span> <span data-ttu-id="0330d-274">Vous êtes également en mesure de tootake action rapidement en effectuant des tâches telles que le recyclage des processus, l’activation et désactivation des différentes collections de données et l’intégration de même avec prise en charge du professionnel de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0330d-274">You are also able tootake action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span></span>

## <a name="general-application-management"></a><span data-ttu-id="0330d-275">Gestion des applications générales</span><span class="sxs-lookup"><span data-stu-id="0330d-275">General Application Management</span></span>
<span data-ttu-id="0330d-276">Lors de la gestion des applications, vous devez souvent tooperform un vaste éventail d’activités telles que la configuration des stratégies de sauvegarde, l’implémentation et la gestion des fournisseurs d’identité et configurer le contrôle d’accès en fonction du rôle.</span><span class="sxs-lookup"><span data-stu-id="0330d-276">When managing applications, you often need tooperform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span></span> <span data-ttu-id="0330d-277">Comme avec hello autres expériences DevOps, hello plateforme Azure s’intègre à ces tâches directement dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-277">As with hello other DevOps experiences, hello Azure platform integrates these tasks directly into hello portal.</span></span>

1. <span data-ttu-id="0330d-278">tooensure vous conservez hello Web application protégée contre la perte de données, vous devez le tooconfigure sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="0330d-278">tooensure you are keeping hello Web App safe from data loss you need tooconfigure backups.</span></span> <span data-ttu-id="0330d-279">Accédez à zone de paramètres toohello pour votre application Web.</span><span class="sxs-lookup"><span data-stu-id="0330d-279">Navigate toohello Settings area for your Web app.</span></span>
   
   ![image56][image56]
2. <span data-ttu-id="0330d-281">Dans le panneau hello sur hello droite, faites défiler catégorie de fonctions toohello.</span><span class="sxs-lookup"><span data-stu-id="0330d-281">In hello blade on hello right, scroll down toohello Features category.</span></span>
   
    ![image57][image57]
3. <span data-ttu-id="0330d-283">Choisissez les sauvegardes ; un panneau s’ouvre sur la droite de hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-283">Choose Backups; a blade opens on hello right.</span></span>
   
   ![image58][image58]
4. <span data-ttu-id="0330d-285">Cliquez sur Configurer, choisissez un compte de stockage panneau hello sur hello droite.</span><span class="sxs-lookup"><span data-stu-id="0330d-285">Click Configure, choose a storage account from hello blade on hello right.</span></span>
   
   ![image59][image59]
5. <span data-ttu-id="0330d-287">Maintenant, créez et choisissez une toohold de conteneur de stockage de vos sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="0330d-287">Now create and choose a storage container toohold your backups.</span></span> <span data-ttu-id="0330d-288">Cliquez sur Créer en bas de hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-288">Click create at hello bottom of hello blade.</span></span> <span data-ttu-id="0330d-289">Puis sélectionnez le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-289">Then select hello container.</span></span>
   
   ![image60][image60]
6. <span data-ttu-id="0330d-291">Une fois que vous avez choisi le conteneur de hello, vous pouvez configurer des planifications, ainsi que les sauvegardes le programme d’installation pour vos bases de données.</span><span class="sxs-lookup"><span data-stu-id="0330d-291">Once you have chosen hello container, you can configure schedules, as well as setup backups for your databases.</span></span> <span data-ttu-id="0330d-292">Pour ce scénario, cliquez sur hello icône d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="0330d-292">For this scenario, click hello save icon.</span></span>
   
    ![image61][image61]
7. <span data-ttu-id="0330d-294">Après l’enregistrement, faites défiler panneau toohello arrière sur la gauche de hello pour les sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="0330d-294">After saving, scroll back toohello blade on hello left for Backups.</span></span> <span data-ttu-id="0330d-295">Cliquez sur Sauvegarder maintenant les application hello tooback.</span><span class="sxs-lookup"><span data-stu-id="0330d-295">Click Backup Now tooback hello application.</span></span>
   
    ![image62][image62]
8. <span data-ttu-id="0330d-297">Dans quelques instants, vous verrez qu’une sauvegarde a été créée.</span><span class="sxs-lookup"><span data-stu-id="0330d-297">In a few moments, you see a backup created.</span></span> <span data-ttu-id="0330d-298">Hello avis restaurer maintenant une option sur hello capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0330d-298">Notice hello Restore Now option on hello screen-shot below.</span></span>
   
    ![image63][image63]
9. <span data-ttu-id="0330d-300">Cliquez sur Restaurer maintenant et examinez le panneau de toohello options hello sur hello droite.</span><span class="sxs-lookup"><span data-stu-id="0330d-300">Click on Restore Now and examine hello options toohello blade on hello right.</span></span> <span data-ttu-id="0330d-301">Vous pouvez choisir qu'une sauvegarde appropriée et facilement tooan de restauration précédemment d’état en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="0330d-301">You can choose an appropriate backup and easily restore tooan earlier state as necessary.</span></span> <span data-ttu-id="0330d-302">Hello portail Azure nous a aidés à facilement activer une stratégie de récupération d’urgence simple pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-302">hello Azure portal has helped us easily enable a simple disaster recovery strategy for hello app.</span></span>
   
    ![image64][image64]
10. <span data-ttu-id="0330d-304">Déplacer Panneau de paramètres toohello sur hello gauche et sous fonctionnalités et choisissez l’authentification ou d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="0330d-304">Move back toohello Settings blade on hello left, and under Features and choose Authentication/Authorization.</span></span>
    
     ![image65][image65]
11. <span data-ttu-id="0330d-306">Dans le panneau hello sur hello droit, choisissez l’authentification du Service application.</span><span class="sxs-lookup"><span data-stu-id="0330d-306">In hello blade on hello right choose App Service Authentication.</span></span> <span data-ttu-id="0330d-307">Notez que hello de diverses options que vous pouvez configurer avec les fournisseurs populaires.</span><span class="sxs-lookup"><span data-stu-id="0330d-307">Notice hello variety of options you can configure with popular providers.</span></span>
    
     ![image66][image66]
12. <span data-ttu-id="0330d-309">Choisissez fournisseur hello de votre choix et notez les options hello pour l’étendue de hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-309">Choose hello provider of your choice and notice hello options for hello scope.</span></span> <span data-ttu-id="0330d-310">Vous pouvez fournir un ID d’application et le code Secret et rapidement activer l’authentification Facebook pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for hello app.</span></span> <span data-ttu-id="0330d-311">Hello portail Azure Active l’authentification en tant qu’une solution clé en main pour les applications.</span><span class="sxs-lookup"><span data-stu-id="0330d-311">hello Azure Portal enables authentication as a turnkey solution for apps.</span></span>
    
     ![image67][image67]
13. <span data-ttu-id="0330d-313">Replacez le panneau des paramètres toohello et choisir des utilisateurs sous la catégorie de gestion des ressources hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-313">Move back toohello Settings blade and choose Users under hello Resource Management category.</span></span>
    
     ![image68][image68]
14. <span data-ttu-id="0330d-315">Dans le panneau hello sur hello droite examiner hello diverses options pour l’ajout de rôles et les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0330d-315">In hello blade on hello right examine hello various options for adding roles and users.</span></span> <span data-ttu-id="0330d-316">Hello portail Azure vous permet de facilement contrôler RBAC (contrôle d’accès basé sur les rôles) pour une application hello.</span><span class="sxs-lookup"><span data-stu-id="0330d-316">hello Azure Portal lets you easily control RBAC (Role-based access control) for hello application.</span></span>
    
     ![image69][image69]

## <a name="summary"></a><span data-ttu-id="0330d-318">Résumé</span><span class="sxs-lookup"><span data-stu-id="0330d-318">Summary</span></span>
<span data-ttu-id="0330d-319">Ce didacticiel présentés ici puissance hello avec hello plateforme Azure rapidement l’activation de déploiement continu pour une application web, développement différents et activités de test, analyse et résolution des problèmes d’une application en temps réel et enfin la gestion de clé stratégies telles que la récupération d’urgence, d’identité et contrôle d’accès en fonction du rôle.</span><span class="sxs-lookup"><span data-stu-id="0330d-319">This tutorial demonstrated some of hello power with hello Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span></span> <span data-ttu-id="0330d-320">Hello plateforme Azure permet une expérience intégrée pour ces flux de travail DevOps et travailler efficacement, en restant dans le contexte pour la tâche hello en cours.</span><span class="sxs-lookup"><span data-stu-id="0330d-320">hello Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for hello task at hand.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0330d-321">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0330d-321">Next steps</span></span>
* <span data-ttu-id="0330d-322">Le Gestionnaire de ressources Azure est important pour l’activation de DevOps sur hello plateforme Azure.</span><span class="sxs-lookup"><span data-stu-id="0330d-322">Azure Resource Manager is important for enabling DevOps on hello Azure platform.</span></span>  <span data-ttu-id="0330d-323">toolearn plus visitez [vue d’ensemble du Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0330d-323">toolearn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="0330d-324">toolearn plus sur le déploiement du Service d’applications Azure, visitez [déployer votre tooAzure d’application du Service d’applications](../app-service-web/web-sites-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="0330d-324">toolearn more about Azure App Service deployment visit [Deploy your app tooAzure App Service](../app-service-web/web-sites-deploy.md)</span></span>

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
