---
title: "Didacticiel : Opérations de développement avec le portail Azure | Microsoft Docs"
description: "Découvrez les divers flux de travail DevOps dans le portail Azure."
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
ms.openlocfilehash: eec7d1402bdea4e5433c473dd713eed23aa80464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-devops-with-the-azure-portal"></a><span data-ttu-id="838e8-103">Didacticiel : Opérations de développement avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="838e8-103">Tutorial: DevOps with the Azure Portal</span></span>
<span data-ttu-id="838e8-104">La plateforme Azure regorge de flux de travail DevOps flexibles.</span><span class="sxs-lookup"><span data-stu-id="838e8-104">The Azure platform is full of flexible DevOps workflows.</span></span> <span data-ttu-id="838e8-105">Dans ce didacticiel, vous apprendrez à exploiter les fonctionnalités du portail Azure pour développer, tester, déployer, dépanner, analyser et gérer les applications en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="838e8-105">In this tutorial, you learn how to leverage the capabilities of the Azure Portal to develop, test, deploy, troubleshoot, monitor, and manage running applications.</span></span> <span data-ttu-id="838e8-106">Ce didacticiel se concentre sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="838e8-106">This tutorial focuses on the following:</span></span>

1. <span data-ttu-id="838e8-107">Création d’une application web et possibilité de déploiement continu</span><span class="sxs-lookup"><span data-stu-id="838e8-107">Creating a web app and enabling continuous deployment</span></span>
2. <span data-ttu-id="838e8-108">Développement et test d’une application</span><span class="sxs-lookup"><span data-stu-id="838e8-108">Develop and test an app</span></span>
3. <span data-ttu-id="838e8-109">Surveillance et dépannage d’une application</span><span class="sxs-lookup"><span data-stu-id="838e8-109">Monitoring and Troubleshooting an app</span></span>
4. <span data-ttu-id="838e8-110">Tâches de gestion des applications générales</span><span class="sxs-lookup"><span data-stu-id="838e8-110">General application management tasks</span></span>

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a><span data-ttu-id="838e8-111">Création d’une application web et possibilité de déploiement continu</span><span class="sxs-lookup"><span data-stu-id="838e8-111">Creating a web app and enabling continuous deployment</span></span>
<span data-ttu-id="838e8-112">Créez une application web avec [Azure App Service](https://azure.microsoft.com/services/app-service/), et utilisez-la pour la suite de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="838e8-112">Create a Web app with [Azure App Service](https://azure.microsoft.com/services/app-service/), which you’ll use in the rest of this tutorial.</span></span> <span data-ttu-id="838e8-113">Vous allez d’abord activer le déploiement continu à partir de votre référentiel de code source dans notre environnement Azure en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="838e8-113">You’ll initially enable continuous deployment from your source code repository into our running Azure environment.</span></span>

1. <span data-ttu-id="838e8-114">Se connecter au portail Azure</span><span class="sxs-lookup"><span data-stu-id="838e8-114">Sign into the Azure Portal</span></span>
2. <span data-ttu-id="838e8-115">Choisissez **App Services** &gt; **Add icon** (Ajouter une icône) et entrez un nom, choisissez votre abonnement, puis créez un groupe de ressources en guise de conteneur du service.</span><span class="sxs-lookup"><span data-stu-id="838e8-115">Choose **App Services** &gt; **Add icon** and enter a name, choose your subscription, and create a new resource group to serve as the container for the service.</span></span>
   
   <span data-ttu-id="838e8-116">Les groupes de ressources vous permettent de gérer différents aspects de la solution, telles que la facturation, les déploiements et l’analyse, le tout grâce à un groupe unique via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="838e8-116">Resource groups allow you to manage various aspects of the solution such as billing, deployments and monitoring all as a single group via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>
   
   ![image1][image1]
3. <span data-ttu-id="838e8-118">Après quelques instants, votre App Service est créé.</span><span class="sxs-lookup"><span data-stu-id="838e8-118">After a few moments, your app service is created.</span></span> <span data-ttu-id="838e8-119">Prenez quelques minutes pour explorer les différentes options de menu du service dans le portail.</span><span class="sxs-lookup"><span data-stu-id="838e8-119">Take a few minutes to explore the various menu options for the service in the portal.</span></span>
   
   ![image2][image2]    
4. <span data-ttu-id="838e8-121">Cliquez sur l'URL.</span><span class="sxs-lookup"><span data-stu-id="838e8-121">Click the URL.</span></span> <span data-ttu-id="838e8-122">Notez les divers outils et référentiels disponibles.</span><span class="sxs-lookup"><span data-stu-id="838e8-122">Notice the variety of available choices for tools and repositories.</span></span> <span data-ttu-id="838e8-123">Vous pouvez également utiliser les langages et infrastructures de votre choix, notamment .NET, Java et Ruby.</span><span class="sxs-lookup"><span data-stu-id="838e8-123">You can also use the languages and frameworks of your choice including .NET, Java, and Ruby.</span></span>
   
   ![image3][image3]    
5. <span data-ttu-id="838e8-125">Le portail Azure simplifie le déploiement continu, en le limitant à quelques étapes simples.</span><span class="sxs-lookup"><span data-stu-id="838e8-125">The Azure portal makes continuous deployment an easy process that involves only a few simple steps.</span></span> <span data-ttu-id="838e8-126">Dans le portail Azure, choisissez les paramètres en utilisant l’icône de l’App Service que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="838e8-126">In the Azure portal, choose settings from the icon for the app service you just created.</span></span>
   
   ![image4][image4]
   
   <span data-ttu-id="838e8-128">Dans le panneau qui s’ouvre sur la droite, accédez à la section de publication.</span><span class="sxs-lookup"><span data-stu-id="838e8-128">From the blade that opens on the right, scroll to the publishing section.</span></span>
   
   ![image5][image5]
6. <span data-ttu-id="838e8-130">Ensuite, configurez certains paramètres pour activer le déploiement continu pour l’application.</span><span class="sxs-lookup"><span data-stu-id="838e8-130">Next, configure some settings to enable continuous deployment for the app.</span></span> <span data-ttu-id="838e8-131">Cliquez sur Source du déploiement, puis sur Choisir la source.</span><span class="sxs-lookup"><span data-stu-id="838e8-131">Click Deployment Source and then click Choose Source.</span></span> <span data-ttu-id="838e8-132">Notez les diverses sources de référentiel disponibles.</span><span class="sxs-lookup"><span data-stu-id="838e8-132">Notice the variety of options you have for repository sources.</span></span>
   
   ![image6][image6]
7. <span data-ttu-id="838e8-134">Pour cet exemple, sélectionnez GitHub.</span><span class="sxs-lookup"><span data-stu-id="838e8-134">For this example choose GitHub.</span></span> <span data-ttu-id="838e8-135">Vous pouvez également choisir le référentiel de votre choix et configurer les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="838e8-135">Optionally choose the repository of your choice and setup the authorization credentials.</span></span>
   
   ![image7][image7]
8. <span data-ttu-id="838e8-137">Après la configuration des autorisations pour votre référentiel, vous pouvez choisir un projet et une branche à déployer.</span><span class="sxs-lookup"><span data-stu-id="838e8-137">After authorization to your repository, you can then choose a project and branch you wish to deploy.</span></span> <span data-ttu-id="838e8-138">Plusieurs exemples fictifs sont répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="838e8-138">There are several fictitious sample examples listed below.</span></span>
   
   ![image8][image8]
9. <span data-ttu-id="838e8-140">Une fois votre projet et votre branche choisis, cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="838e8-140">Once you choose your project and branch, click ok.</span></span> <span data-ttu-id="838e8-141">Des notifications de déploiement doivent commencer à apparaître.</span><span class="sxs-lookup"><span data-stu-id="838e8-141">You should start to see notifications of a deployment.</span></span>
   
   ![image9][image9]
10. <span data-ttu-id="838e8-143">Revenez à GitHub pour voir le webhook qui a été créé afin d’intégrer le référentiel de contrôle du code source à Azure.</span><span class="sxs-lookup"><span data-stu-id="838e8-143">Navigate back to GitHub to see the webhook that was created to integrate the source control repo with Azure.</span></span> <span data-ttu-id="838e8-144">Le portail Azure permet l’intégration à GitHub en seulement quelques étapes simples.</span><span class="sxs-lookup"><span data-stu-id="838e8-144">The Azure Portal enables integration with GitHub with only a few simple steps.</span></span>
    
    ![image10][image10]
11. <span data-ttu-id="838e8-146">Pour illustrer le déploiement continu, ajoutez rapidement du contenu dans le référentiel.</span><span class="sxs-lookup"><span data-stu-id="838e8-146">To demonstrate continuous deployment, you quickly add some content to the repository.</span></span> <span data-ttu-id="838e8-147">Pour obtenir un exemple simple, ajoutez un exemple de fichier texte à un référentiel GitHub.</span><span class="sxs-lookup"><span data-stu-id="838e8-147">For a simple example, add a sample text file to a GitHub repo.</span></span> <span data-ttu-id="838e8-148">Vous pouvez utiliser .NET, Ruby, Python ou un autre type d’application avec l’App Service.</span><span class="sxs-lookup"><span data-stu-id="838e8-148">You are free to use .NET, Ruby, Python, or some other type of application with App Service.</span></span> <span data-ttu-id="838e8-149">N’hésitez pas à ajouter un fichier texte ou une application ASP.NET MVC, Java ou Ruby au référentiel de votre choix.</span><span class="sxs-lookup"><span data-stu-id="838e8-149">Feel free to add a text file, ASP.NET MVC, Java, or Ruby application to the repo of your choice.</span></span>
    
    ![image11][image11]
12. <span data-ttu-id="838e8-151">Après avoir effectué des modifications dans votre référentiel, le démarrage d’un nouveau déploiement est signalé dans la zone de notification du portail.</span><span class="sxs-lookup"><span data-stu-id="838e8-151">After committing changes to your repository, you see a new deployment initiate in the portal notifications area.</span></span> <span data-ttu-id="838e8-152">Si vous ne voyez aucune modification rapidement après leur validation dans votre référentiel, cliquez sur Synchroniser.</span><span class="sxs-lookup"><span data-stu-id="838e8-152">Click Sync if you do not quickly see changes after committing to your repository.</span></span>
    
    ![image12][image12]
13. <span data-ttu-id="838e8-154">À ce stade, si vous essayez de charger la page pour l’App Service, il se peut que vous receviez une erreur 403.</span><span class="sxs-lookup"><span data-stu-id="838e8-154">At this point, if you try and load the page for the app service, you may receive a 403 error.</span></span> <span data-ttu-id="838e8-155">Dans cet exemple, elle apparaît car il n’existe aucune configuration de document par défaut pour la page, telle qu’un fichier index.htm ou default.html.</span><span class="sxs-lookup"><span data-stu-id="838e8-155">In this example, it is because there is no typical default document setup for the page such as a file like index.htm or default.html.</span></span> <span data-ttu-id="838e8-156">Vous pouvez résoudre rapidement ce problème à l’aide des outils du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="838e8-156">You can quickly remedy this with the tooling in the Azure Portal.</span></span>  <span data-ttu-id="838e8-157">Dans le portail Azure, choisissez Paramètres &gt; Paramètres de l’application.</span><span class="sxs-lookup"><span data-stu-id="838e8-157">In the Azure Portal choose Settings &gt; Application Settings.</span></span>
    
     ![image13][image13]
14. <span data-ttu-id="838e8-159">Un panneau regroupant les paramètres de l’application s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="838e8-159">A blade opens for application settings.</span></span> <span data-ttu-id="838e8-160">Entrez le nom de la page « SamplePage.html » et cliquez sur Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="838e8-160">Enter the name of the page “SamplePage.html” and click Save.</span></span> <span data-ttu-id="838e8-161">Prenez quelques minutes pour explorer les autres paramètres.</span><span class="sxs-lookup"><span data-stu-id="838e8-161">Take a few minutes to explore the other settings.</span></span>
    
    ![image14][image14]
15. <span data-ttu-id="838e8-163">Vous pouvez actualiser l’URL de votre navigateur afin d’être sûr de voir les modifications attendues.</span><span class="sxs-lookup"><span data-stu-id="838e8-163">Optionally refresh your browser URL to ensure you see the expected changes.</span></span> <span data-ttu-id="838e8-164">Dans ce cas, un texte simple remplit désormais la page.</span><span class="sxs-lookup"><span data-stu-id="838e8-164">In this case, there is some simple text now populating the page.</span></span> <span data-ttu-id="838e8-165">Chaque modification supplémentaire apportée au référentiel entraîne un déploiement automatique.</span><span class="sxs-lookup"><span data-stu-id="838e8-165">Each additional change to the repository would result in a new automatic deployment.</span></span>
    
    ![image15][image15]
    
    <span data-ttu-id="838e8-167">L’activation du déploiement continu avec le portail Azure est une procédure simple.</span><span class="sxs-lookup"><span data-stu-id="838e8-167">Enabling continuous deployment with the Azure Portal is an easy experience.</span></span> <span data-ttu-id="838e8-168">Vous pouvez également créer des pipelines de publication plus complexes et utiliser de nombreuses autres techniques avec contrôle de code source existant et systèmes d’intégration continue à déployer sur Azure, par exemple en exploitant les systèmes de gestion automatisée de la création et de la publication.</span><span class="sxs-lookup"><span data-stu-id="838e8-168">You can also build more complex release pipelines and use many other techniques with existing source control and continuous integration systems to deploy to Azure, such as leveraging automated build and release management systems.</span></span>

## <a name="develop-and-test-an-app"></a><span data-ttu-id="838e8-169">Développement et test d’une application</span><span class="sxs-lookup"><span data-stu-id="838e8-169">Develop and test an app</span></span>
<span data-ttu-id="838e8-170">Ensuite, apportez des modifications à la base de code et déployez-les rapidement.</span><span class="sxs-lookup"><span data-stu-id="838e8-170">Next, make some changes to the code base and rapidly deploy those changes.</span></span> <span data-ttu-id="838e8-171">Vous configurerez également des tests de performance pour l’application web.</span><span class="sxs-lookup"><span data-stu-id="838e8-171">You will also setup up some performance testing for the Web app.</span></span>

1. <span data-ttu-id="838e8-172">Dans le portail Azure, sélectionnez App Services dans le volet de navigation, puis recherchez votre App Service.</span><span class="sxs-lookup"><span data-stu-id="838e8-172">In the Azure Portal choose App Services from the navigation pane, and locate your App Service.</span></span>
   
   ![image16][image16]
2. <span data-ttu-id="838e8-174">Cliquez sur Outils</span><span class="sxs-lookup"><span data-stu-id="838e8-174">Click Tools</span></span>
   
   ![image17][image17]
3. <span data-ttu-id="838e8-176">Remarquez la catégorie Développer sous Outils.</span><span class="sxs-lookup"><span data-stu-id="838e8-176">Notice the develop category under Tools.</span></span> <span data-ttu-id="838e8-177">Cette catégorie inclut plusieurs outils utiles qui nous permettront de travailler avec des applications sans quitter le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="838e8-177">There are several useful tools here that allow us to work with apps without leaving the Azure Portal.</span></span> <span data-ttu-id="838e8-178">Cliquez sur Console.</span><span class="sxs-lookup"><span data-stu-id="838e8-178">Click on Console.</span></span>
   
   ![image18][image18]
4. <span data-ttu-id="838e8-180">Dans la fenêtre de console, vous pouvez émettre des commandes en direct pour votre application.</span><span class="sxs-lookup"><span data-stu-id="838e8-180">In the console window, you can issue live commands for your app.</span></span> <span data-ttu-id="838e8-181">Tapez la commande dir et appuyez sur Entrée.</span><span class="sxs-lookup"><span data-stu-id="838e8-181">Type the dir command and hit enter.</span></span> <span data-ttu-id="838e8-182">Notez que les commandes nécessitant des privilèges élevés ne fonctionnent pas.</span><span class="sxs-lookup"><span data-stu-id="838e8-182">Note that commands requiring elevated privileges do not work.</span></span>
   
   ![image19][image19]
5. <span data-ttu-id="838e8-184">Revenez à la catégorie Développer et choisissez Visual Studio Online.</span><span class="sxs-lookup"><span data-stu-id="838e8-184">Move back to the Develop category and choose Visual Studio Online.</span></span> <span data-ttu-id="838e8-185">Remarque : Visual Studio Online devient Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="838e8-185">Note: Visual Studio Online is now named Visual Studio Team Services.</span></span>
   
   ![image20][image20]
6. <span data-ttu-id="838e8-187">Passez à la fonctionnalité d’édition dans le navigateur de votre application.</span><span class="sxs-lookup"><span data-stu-id="838e8-187">Toggle on the in-browser editing experience for your App.</span></span>
   
   ![image21][image21]
7. <span data-ttu-id="838e8-189">Une extension web pour votre application s’installe.</span><span class="sxs-lookup"><span data-stu-id="838e8-189">A web extension installs for your app.</span></span> <span data-ttu-id="838e8-190">Les extensions permettent d’ajouter rapidement et facilement des fonctionnalités aux applications dans Azure.</span><span class="sxs-lookup"><span data-stu-id="838e8-190">Extensions quickly and easily add functionality to apps in Azure.</span></span> <span data-ttu-id="838e8-191">Découvrez certains autres types d’extension disponibles dans la capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="838e8-191">Notice some of the other extension types available in the screenshot below.</span></span>
   
   ![image22][image22]
8. <span data-ttu-id="838e8-193">Une fois que l’extension Visual Studio Online est installée, cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="838e8-193">Once the Visual Studio Online extension installs, click Go.</span></span>
   
   ![image23][image23]
9. <span data-ttu-id="838e8-195">Un onglet de navigateur s’ouvre pour afficher un IDE de développement directement dans le navigateur.</span><span class="sxs-lookup"><span data-stu-id="838e8-195">A browser tab opens where you see a development IDE directly in the browser.</span></span> <span data-ttu-id="838e8-196">Veuillez noter que l’exemple ci-dessous utilise Chrome.</span><span class="sxs-lookup"><span data-stu-id="838e8-196">Notice the experience below is in Chrome.</span></span>
   
   ![image24][image24]
10. <span data-ttu-id="838e8-198">Vous pouvez effectuer plusieurs activités telles que la modification de fichiers, l’ajout de fichiers et dossiers, et le téléchargement de contenu à partir du site en activité.</span><span class="sxs-lookup"><span data-stu-id="838e8-198">You can perform several activities such as edit files, add files and folders, and download content from the live site.</span></span> <span data-ttu-id="838e8-199">Apportez une modification rapide au fichier SamplePage.html.</span><span class="sxs-lookup"><span data-stu-id="838e8-199">Make a quick edit to the SamplePage.html file.</span></span>
    
    ![image25][image25]
11. <span data-ttu-id="838e8-201">Dans quelques instants, les modifications seront automatiquement enregistrées.</span><span class="sxs-lookup"><span data-stu-id="838e8-201">In a few moments, the changes are automatically saved.</span></span> <span data-ttu-id="838e8-202">Si vous revenez à la page, vous pourrez voir les modifications.</span><span class="sxs-lookup"><span data-stu-id="838e8-202">If you navigate back to the page, you can see the changes.</span></span> <span data-ttu-id="838e8-203">Gardez à l’esprit que les modifications en direct ne sont généralement pas appropriées pour les environnements de production.</span><span class="sxs-lookup"><span data-stu-id="838e8-203">Keep in mind live edits like these are most likely not suitable for production environments.</span></span> <span data-ttu-id="838e8-204">Toutefois, les outils facilitent largement la modification rapide des environnements de développement et de test.</span><span class="sxs-lookup"><span data-stu-id="838e8-204">However, the tools make it very easy to make quick changes for dev and test environments.</span></span>
    
    ![image26][image26]
    
    ![image27][image27]
12. <span data-ttu-id="838e8-207">Revenez au panneau Outils et, sous la catégorie Développer, cliquez sur Test de performance.</span><span class="sxs-lookup"><span data-stu-id="838e8-207">Move back to the tools blade and under the Develop category, click on Performance Test.</span></span>
    
    ![image28][image28]
13. <span data-ttu-id="838e8-209">Vous devez définir un compte Team Services.</span><span class="sxs-lookup"><span data-stu-id="838e8-209">You need to set a team services account.</span></span> <span data-ttu-id="838e8-210">Pour plus d’informations, consultez la page [Créer un compte Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span><span class="sxs-lookup"><span data-stu-id="838e8-210">See here for more details: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)</span></span>
14. <span data-ttu-id="838e8-211">Cliquez sur Nouveau pour créer un test de performance.</span><span class="sxs-lookup"><span data-stu-id="838e8-211">Click on New to create a performance test.</span></span>
    
    ![image29][image29]
    
    <span data-ttu-id="838e8-213">Configurez les différentes valeurs, puis cliquez sur Exécuter le test en bas de la boîte de dialogue pour lancer un test de performance.</span><span class="sxs-lookup"><span data-stu-id="838e8-213">Configure the various values and click Run Test at the bottom of the dialogue to initiate a performance test.</span></span>
    
    ![image30][image30]
    
    ![image31][image31]
15. <span data-ttu-id="838e8-216">Une fois le test démarré, vous pouvez surveiller l’état.</span><span class="sxs-lookup"><span data-stu-id="838e8-216">Once the test starts running, you can monitor the state.</span></span>
    
    ![image32][image32]
    
    <span data-ttu-id="838e8-218">Lorsque le test est terminé, cliquez sur le résultat pour afficher plus de détails.</span><span class="sxs-lookup"><span data-stu-id="838e8-218">Once the test finishes, clicking on the result shows more details.</span></span>
    
    ![image33][image33]
16. <span data-ttu-id="838e8-220">Dans cet exemple, vous avez créé une courte série de tests. La quantité de données à analyser est donc limitée, mais vous pouvez voir différentes mesures et réexécuter votre test à partir de cette vue.</span><span class="sxs-lookup"><span data-stu-id="838e8-220">In this example, you created a small test run, so there is limited data to analyze, but you can see various metrics as well as rerun your test from this view.</span></span> <span data-ttu-id="838e8-221">Le portail Azure facilite la création, l’exécution et l’analyse des tests de performance web.</span><span class="sxs-lookup"><span data-stu-id="838e8-221">The Azure Portal makes creating, executing, and analyzing web performance tests an easy process.</span></span> <span data-ttu-id="838e8-222">Les captures d’écran ci-dessous présentent les données de performances.</span><span class="sxs-lookup"><span data-stu-id="838e8-222">The screenshots below display the performance data.</span></span>
    
    ![image34][image34]
    
    ![image35][image35]
    
    ![image36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a><span data-ttu-id="838e8-226">Surveillance et dépannage d’une application</span><span class="sxs-lookup"><span data-stu-id="838e8-226">Monitoring and troubleshooting an app</span></span>
<span data-ttu-id="838e8-227">Azure fournit de nombreuses fonctionnalités de surveillance et de dépannage pour les applications en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="838e8-227">Azure provides many capabilities for monitoring and troubleshooting running applications.</span></span>

1. <span data-ttu-id="838e8-228">Dans le portail Azure de votre application web, sélectionnez Outils.</span><span class="sxs-lookup"><span data-stu-id="838e8-228">In the Azure Portal for our Web app choose Tools.</span></span>
   
   ![image37][image37]
2. <span data-ttu-id="838e8-230">Sous la catégorie Dépannage, notez les différents choix d’utilisation des outils pour résoudre les problèmes potentiels avec une application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="838e8-230">Under the Troubleshoot category, notice the various choices for using tools to troubleshoot potential issues with a running app.</span></span> <span data-ttu-id="838e8-231">Vous pouvez par exemple analyser le trafic HTTP en direct, activer la réparation spontanée, afficher les journaux et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="838e8-231">You can do things like monitor Live HTTP traffic, enable self-healing, view logs, and more.</span></span>
   
   ![image38][image38]
3. <span data-ttu-id="838e8-233">Sélectionnez Métriques du site pour obtenir rapidement une vue de certains codes HTTP.</span><span class="sxs-lookup"><span data-stu-id="838e8-233">Choose Site Metrics to quickly get a view of some HTTP codes.</span></span>
   
   ![image39][image39]
4. <span data-ttu-id="838e8-235">Sélectionnez Diagnostics en tant que service.</span><span class="sxs-lookup"><span data-stu-id="838e8-235">Choose Diagnostics as a Service.</span></span> <span data-ttu-id="838e8-236">Choisissez votre type d’application, puis sélectionnez Exécuter.</span><span class="sxs-lookup"><span data-stu-id="838e8-236">Choose your application type, then choose Run.</span></span>
   
   ![image40][image40]
   
   <span data-ttu-id="838e8-238">La collecte commence.</span><span class="sxs-lookup"><span data-stu-id="838e8-238">A collection begins.</span></span>
   
   ![image41][image41]
5. <span data-ttu-id="838e8-240">Vous pouvez choisir le journal approprié pour diagnostiquer les problèmes potentiels.</span><span class="sxs-lookup"><span data-stu-id="838e8-240">You may choose the appropriate log to diagnose potential issues.</span></span> <span data-ttu-id="838e8-241">Vous devez activer la journalisation pour voir toutes les options de données disponibles, comme les journaux HTTP.</span><span class="sxs-lookup"><span data-stu-id="838e8-241">You need to enable logging to see all of the available data options such as HTTP Logs.</span></span>
   
   ![image42][image42]
   
   <span data-ttu-id="838e8-243">En cliquant sur le fichier de vidage de la mémoire, vous pouvez télécharger et analyser un rapport d’analyse DebugDiag pour détecter les problèmes potentiels.</span><span class="sxs-lookup"><span data-stu-id="838e8-243">By clicking on the Memory Dump file you can download and analyze a DebugDiag analysis report to help find potential issues.</span></span>
   
   ![image43][image43]
6. <span data-ttu-id="838e8-245">Pour afficher davantage de données, vous devez activer la journalisation supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="838e8-245">To view more data, you need to enable additional logging.</span></span> <span data-ttu-id="838e8-246">Dans le portail Azure, accédez à l’application web et sélectionnez Paramètres.</span><span class="sxs-lookup"><span data-stu-id="838e8-246">In the Azure Portal, navigate to the Web app and choose Settings.</span></span>
   
   ![image44][image44]
7. <span data-ttu-id="838e8-248">Accédez à la catégorie Fonctionnalités, puis choisissez Journaux de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="838e8-248">Scroll down to the features category, and choose Diagnostic logs.</span></span>
   
      ![image45][image45]
8. <span data-ttu-id="838e8-250">Notez les différentes options de journalisation.</span><span class="sxs-lookup"><span data-stu-id="838e8-250">Notice the various options for logging.</span></span> <span data-ttu-id="838e8-251">Activez la journalisation du serveur web et cliquez sur Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="838e8-251">Toggle on Web server logging and click save.</span></span>
   
   ![image46][image46]
9. <span data-ttu-id="838e8-253">Revenez à la zone des outils de l’application et sélectionnez Diagnostics en tant que service, puis cliquez sur Exécuter pour exécuter de nouveau la collecte de données.</span><span class="sxs-lookup"><span data-stu-id="838e8-253">Move back to the tools area for the app and choose Diagnostics as a service and click Run to rerun the data collection.</span></span>
   
   ![image47][image47]
10. <span data-ttu-id="838e8-255">Lorsque le paramètre de journalisation HTTP est activé, vous voyez les données collectées pour les journaux HTTP.</span><span class="sxs-lookup"><span data-stu-id="838e8-255">With the HTTP logging setting enabled, you now see data collected for HTTP Logs.</span></span>
    
    ![image48][image48]
11. <span data-ttu-id="838e8-257">En cliquant sur le journal des fichiers HTML, vous générez un rapport complet basé sur navigateur, pour un examen approfondi.</span><span class="sxs-lookup"><span data-stu-id="838e8-257">By clicking the HTML file log, you produce a rich browser-based report for further investigation.</span></span>
    
    ![image49][image49]
12. <span data-ttu-id="838e8-259">Revenez à la section Outils dans le portail Azure de l’application.</span><span class="sxs-lookup"><span data-stu-id="838e8-259">Move back to the tools section in the Azure Portal for the app.</span></span> <span data-ttu-id="838e8-260">Accédez à la section Outils et choisissez Explorateur de processus.</span><span class="sxs-lookup"><span data-stu-id="838e8-260">Scroll to the Tools section and choose Process Explorer.</span></span>
    
    ![image50][image50]
13. <span data-ttu-id="838e8-262">En choisissant Explorateur de processus, vous pouvez afficher plus d’informations sur les processus en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="838e8-262">By choosing Process Explorer, you can view details about running processes.</span></span> <span data-ttu-id="838e8-263">Comme indiqué ci-dessous, vous pouvez explorer les processus, et même les interrompre, à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="838e8-263">Notice below you can drill into processes and even kill processes all from the Azure Portal.</span></span>
    
    ![image51][image51]
    
    ![image52][image52]
14. <span data-ttu-id="838e8-266">Revenez au panneau Paramètres, sur la gauche.</span><span class="sxs-lookup"><span data-stu-id="838e8-266">Move back to the Settings blade on the left.</span></span> <span data-ttu-id="838e8-267">Cliquez sur Nouvelle demande de support.</span><span class="sxs-lookup"><span data-stu-id="838e8-267">Click New support request.</span></span>
    
    ![image53][image53]
15. <span data-ttu-id="838e8-269">Dans le panneau de droite, vous pouvez fournir des informations sur les problèmes, saisir des coordonnées et télécharger des données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="838e8-269">From the blade on the right, you can fill out details about the issues, enter contact information, and even upload diagnostic data.</span></span> <span data-ttu-id="838e8-270">Le portail Azure facilite la collaboration avec le support Microsoft.</span><span class="sxs-lookup"><span data-stu-id="838e8-270">The Azure Portal enables working with Microsoft support a seamless experience.</span></span>
    
    ![image54][image54]
    
    ![image55][image55]
    
    <span data-ttu-id="838e8-273">Le portail Azure contribue à offrir une utilisation puissante et familière des outils, afin de contrôler et de dépanner nos applications en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="838e8-273">The Azure Portal helps provide powerful and familiar tooling experiences to help monitor and troubleshoot our running applications.</span></span> <span data-ttu-id="838e8-274">Vous pouvez également prendre rapidement des mesures en effectuant des tâches telles que le recyclage des processus, l’activation et la désactivation de différentes collectes de données, et même l’intégration au support professionnel Microsoft.</span><span class="sxs-lookup"><span data-stu-id="838e8-274">You are also able to take action quickly by performing tasks such as recycling processes, enabling and disabling various data collections, and even integrating with Microsoft professional support.</span></span>

## <a name="general-application-management"></a><span data-ttu-id="838e8-275">Gestion des applications générales</span><span class="sxs-lookup"><span data-stu-id="838e8-275">General Application Management</span></span>
<span data-ttu-id="838e8-276">Lorsque vous gérez des applications, vous devez souvent effectuer de nombreuses tâches, telles que la configuration des stratégies de sauvegarde, l’implémentation et la gestion des fournisseurs d’identité, et la configuration des contrôles d’accès basés sur les rôles.</span><span class="sxs-lookup"><span data-stu-id="838e8-276">When managing applications, you often need to perform a broad variety of activities such as configuring backup strategies, implementing and managing identity providers, and configuring Role-based access control.</span></span> <span data-ttu-id="838e8-277">Comme pour les autres expériences DevOps, la plateforme Azure intègre ces tâches directement dans le portail.</span><span class="sxs-lookup"><span data-stu-id="838e8-277">As with the other DevOps experiences, the Azure platform integrates these tasks directly into the portal.</span></span>

1. <span data-ttu-id="838e8-278">Afin de protéger l’application web contre les pertes de données, vous devez configurer des sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="838e8-278">To ensure you are keeping the Web App safe from data loss you need to configure backups.</span></span> <span data-ttu-id="838e8-279">Accédez à la zone Paramètres de votre application web.</span><span class="sxs-lookup"><span data-stu-id="838e8-279">Navigate to the Settings area for your Web app.</span></span>
   
   ![image56][image56]
2. <span data-ttu-id="838e8-281">Dans le panneau de droite, accédez à la catégorie Fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="838e8-281">In the blade on the right, scroll down to the Features category.</span></span>
   
    ![image57][image57]
3. <span data-ttu-id="838e8-283">Choisissez Sauvegardes ; un panneau s’ouvre sur la droite.</span><span class="sxs-lookup"><span data-stu-id="838e8-283">Choose Backups; a blade opens on the right.</span></span>
   
   ![image58][image58]
4. <span data-ttu-id="838e8-285">Cliquez sur Configurer, puis choisissez un compte de stockage dans le panneau de droite.</span><span class="sxs-lookup"><span data-stu-id="838e8-285">Click Configure, choose a storage account from the blade on the right.</span></span>
   
   ![image59][image59]
5. <span data-ttu-id="838e8-287">Maintenant, créez et choisissez un conteneur de stockage pour stocker vos sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="838e8-287">Now create and choose a storage container to hold your backups.</span></span> <span data-ttu-id="838e8-288">Cliquez sur l’option Créer figurant en bas du panneau.</span><span class="sxs-lookup"><span data-stu-id="838e8-288">Click create at the bottom of the blade.</span></span> <span data-ttu-id="838e8-289">Sélectionnez ensuite le conteneur.</span><span class="sxs-lookup"><span data-stu-id="838e8-289">Then select the container.</span></span>
   
   ![image60][image60]
6. <span data-ttu-id="838e8-291">Une fois que vous avez choisi le conteneur, vous pouvez configurer des planifications, ainsi que des sauvegardes de configuration pour vos bases de données.</span><span class="sxs-lookup"><span data-stu-id="838e8-291">Once you have chosen the container, you can configure schedules, as well as setup backups for your databases.</span></span> <span data-ttu-id="838e8-292">Pour ce scénario, cliquez sur l’icône Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="838e8-292">For this scenario, click the save icon.</span></span>
   
    ![image61][image61]
7. <span data-ttu-id="838e8-294">Après l’enregistrement, revenez à Sauvegardes dans le panneau de gauche.</span><span class="sxs-lookup"><span data-stu-id="838e8-294">After saving, scroll back to the blade on the left for Backups.</span></span> <span data-ttu-id="838e8-295">Cliquez sur Sauvegarder maintenant pour sauvegarder l’application.</span><span class="sxs-lookup"><span data-stu-id="838e8-295">Click Backup Now to back the application.</span></span>
   
    ![image62][image62]
8. <span data-ttu-id="838e8-297">Dans quelques instants, vous verrez qu’une sauvegarde a été créée.</span><span class="sxs-lookup"><span data-stu-id="838e8-297">In a few moments, you see a backup created.</span></span> <span data-ttu-id="838e8-298">Notez la présence de l’option Restaurer maintenant sur la capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="838e8-298">Notice the Restore Now option on the screen-shot below.</span></span>
   
    ![image63][image63]
9. <span data-ttu-id="838e8-300">Cliquez sur Restaurer maintenant et examinez les options dans le panneau de droite.</span><span class="sxs-lookup"><span data-stu-id="838e8-300">Click on Restore Now and examine the options to the blade on the right.</span></span> <span data-ttu-id="838e8-301">Vous pouvez choisir une sauvegarde appropriée et facilement restaurer un état antérieur si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="838e8-301">You can choose an appropriate backup and easily restore to an earlier state as necessary.</span></span> <span data-ttu-id="838e8-302">Le portail Azure nous a permis de facilement mettre en place une stratégie simple de récupération d’urgence pour l’application.</span><span class="sxs-lookup"><span data-stu-id="838e8-302">The Azure portal has helped us easily enable a simple disaster recovery strategy for the app.</span></span>
   
    ![image64][image64]
10. <span data-ttu-id="838e8-304">Revenez au panneau Paramètres sur la gauche. Sous Fonctionnalités, choisissez Authentification/autorisation.</span><span class="sxs-lookup"><span data-stu-id="838e8-304">Move back to the Settings blade on the left, and under Features and choose Authentication/Authorization.</span></span>
    
     ![image65][image65]
11. <span data-ttu-id="838e8-306">Dans le panneau de droite, choisissez Authentification App Service.</span><span class="sxs-lookup"><span data-stu-id="838e8-306">In the blade on the right choose App Service Authentication.</span></span> <span data-ttu-id="838e8-307">Notez les diverses options que vous pouvez configurer avec les fournisseurs les plus courants.</span><span class="sxs-lookup"><span data-stu-id="838e8-307">Notice the variety of options you can configure with popular providers.</span></span>
    
     ![image66][image66]
12. <span data-ttu-id="838e8-309">Sélectionnez le fournisseur de votre choix et notez les options pour l’étendue.</span><span class="sxs-lookup"><span data-stu-id="838e8-309">Choose the provider of your choice and notice the options for the scope.</span></span> <span data-ttu-id="838e8-310">Vous pouvez fournir un ID d’application et une question secrète, et activer rapidement l’authentification Facebook pour l’application.</span><span class="sxs-lookup"><span data-stu-id="838e8-310">You can provide an App ID and App Secret and quickly enable Facebook authentication for the app.</span></span> <span data-ttu-id="838e8-311">Le portail Azure offre une solution d’authentification clé en main pour les applications.</span><span class="sxs-lookup"><span data-stu-id="838e8-311">The Azure Portal enables authentication as a turnkey solution for apps.</span></span>
    
     ![image67][image67]
13. <span data-ttu-id="838e8-313">Revenez au panneau Paramètres et choisissez Utilisateurs dans la catégorie Gestion des ressources.</span><span class="sxs-lookup"><span data-stu-id="838e8-313">Move back to the Settings blade and choose Users under the Resource Management category.</span></span>
    
     ![image68][image68]
14. <span data-ttu-id="838e8-315">Dans le panneau de droite, examinez les diverses options permettant d’ajouter des utilisateurs et des rôles.</span><span class="sxs-lookup"><span data-stu-id="838e8-315">In the blade on the right examine the various options for adding roles and users.</span></span> <span data-ttu-id="838e8-316">Le portail Azure vous permet de contrôler facilement le contrôle d’accès en fonction du rôle (RBAC) pour l’application.</span><span class="sxs-lookup"><span data-stu-id="838e8-316">The Azure Portal lets you easily control RBAC (Role-based access control) for the application.</span></span>
    
     ![image69][image69]

## <a name="summary"></a><span data-ttu-id="838e8-318">Résumé</span><span class="sxs-lookup"><span data-stu-id="838e8-318">Summary</span></span>
<span data-ttu-id="838e8-319">Ce didacticiel a présenté succinctement la puissance de la plateforme Azure, qui passe par l’activation rapide d’un déploiement continu pour une application web, la réalisation de diverses activités de développement et de test, l’analyse et le dépannage des applications en activité et enfin la gestion des stratégies clés telles que la récupération d’urgence, l’identification et le contrôle d’accès en fonction du rôle.</span><span class="sxs-lookup"><span data-stu-id="838e8-319">This tutorial demonstrated some of the power with the Azure platform by quickly enabling continuous deployment for a web app, performing various development and testing activities, monitoring and troubleshooting a live app, and finally managing key strategies such as disaster recovery, identity, and role-based access control.</span></span> <span data-ttu-id="838e8-320">La plateforme Azure offre une expérience intégrée pour ces flux de travail DevOps. Vous pouvez ainsi travailler efficacement de manière appropriée à la tâche en cours.</span><span class="sxs-lookup"><span data-stu-id="838e8-320">The Azure platform enables an integrated experience for these DevOps workflows, and you can work efficiently by staying in context for the task at hand.</span></span>

## <a name="next-steps"></a><span data-ttu-id="838e8-321">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="838e8-321">Next steps</span></span>
* <span data-ttu-id="838e8-322">Azure Resource Manager est important pour permettre les opérations de développement sur la plateforme Azure.</span><span class="sxs-lookup"><span data-stu-id="838e8-322">Azure Resource Manager is important for enabling DevOps on the Azure platform.</span></span>  <span data-ttu-id="838e8-323">Pour en savoir plus, consultez la page [Vue d’ensemble d’Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="838e8-323">To learn more visit [Azure Resource Manager overview](../azure-resource-manager/resource-group-overview.md).</span></span>
* <span data-ttu-id="838e8-324">Pour en savoir plus sur le déploiement d’Azure App Service, consultez la page [Déploiement de votre application dans Azure App Service](../app-service-web/web-sites-deploy.md)</span><span class="sxs-lookup"><span data-stu-id="838e8-324">To learn more about Azure App Service deployment visit [Deploy your app to Azure App Service](../app-service-web/web-sites-deploy.md)</span></span>

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
