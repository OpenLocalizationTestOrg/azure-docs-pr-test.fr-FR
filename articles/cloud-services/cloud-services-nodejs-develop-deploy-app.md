---
title: Guide de mise en route Node.js | Microsoft Docs
description: "Apprenez à créer une application web Node.js simple et à la déployer vers un service cloud Azure."
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 980643f35c78bbae7b1b12336331ca15ad4fb89b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="build-and-deploy-a-nodejs-application-to-an-azure-cloud-service"></a><span data-ttu-id="8995e-103">Création et déploiement d'une application Node.js dans Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="8995e-103">Build and deploy a Node.js application to an Azure Cloud Service</span></span>

<span data-ttu-id="8995e-104">Ce didacticiel explique comment créer une application Node.js simple s’exécutant dans Azure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="8995e-104">This tutorial shows how to create a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="8995e-105">Les services Cloud Services sont des composantes des applications cloud extensibles dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8995e-105">Cloud Services are the building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="8995e-106">Ils permettent de séparer, de gérer et d'étendre de façon indépendante le composant frontal et le composant principal de votre application.</span><span class="sxs-lookup"><span data-stu-id="8995e-106">They allow the separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="8995e-107">Cloud Services héberge de façon fiable chaque rôle sur une machine virtuelle dédiée.</span><span class="sxs-lookup"><span data-stu-id="8995e-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="8995e-108">Pour plus d'informations sur les services cloud et pour connaître les différences avec les sites Web Azure et les machines virtuelles, consultez la page [Comparaison des sites Web Azure, des services cloud et des machines virtuelles].</span><span class="sxs-lookup"><span data-stu-id="8995e-108">For more information on Cloud Services, and how they compare to Azure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="8995e-109">Vous voulez créer un simple site Web ?</span><span class="sxs-lookup"><span data-stu-id="8995e-109">Looking to build a simple website?</span></span> <span data-ttu-id="8995e-110">Si votre scénario ne comporte qu’un simple composant frontal web, envisagez d’[utiliser une application web légère].</span><span class="sxs-lookup"><span data-stu-id="8995e-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="8995e-111">Vous pouvez facilement mettre à niveau vers un service cloud en fonction du développement de votre application et de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="8995e-111">You can easily upgrade to a Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="8995e-112">Dans ce didacticiel, vous allez créer une application Web simple, hébergée dans un rôle Web.</span><span class="sxs-lookup"><span data-stu-id="8995e-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="8995e-113">Vous utiliserez l’émulateur de calcul pour tester votre application localement, puis déploierez cette dernière à l’aide d’outils en ligne de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8995e-113">You will use the compute emulator to test your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="8995e-114">Il s’agit d’une application « hello world » simple :</span><span class="sxs-lookup"><span data-stu-id="8995e-114">The application is a simple "hello world" application:</span></span>

![Navigateur Web avec la page Web Hello World][A web browser displaying the Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="8995e-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8995e-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="8995e-117">Ce didacticiel utilise Azure PowerShell, qui nécessite Windows.</span><span class="sxs-lookup"><span data-stu-id="8995e-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="8995e-118">Installez et configurez [Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="8995e-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="8995e-119">Téléchargez et installez le [Kit de développement logiciel (SDK) Azure pour .NET 2.7].</span><span class="sxs-lookup"><span data-stu-id="8995e-119">Download and install the [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="8995e-120">Dans le programme d'installation, sélectionnez :</span><span class="sxs-lookup"><span data-stu-id="8995e-120">In the install setup, select:</span></span>
  * <span data-ttu-id="8995e-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="8995e-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="8995e-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="8995e-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="8995e-123">Créer un projet Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="8995e-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="8995e-124">Effectuez les tâches suivantes pour créer un projet Azure Cloud Services, avec la structure Node.js de base :</span><span class="sxs-lookup"><span data-stu-id="8995e-124">Perform the following tasks to create a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="8995e-125">Exécutez **Windows PowerShell** en tant qu’administrateur ; à partir du **menu Démarrer** ou de l’**écran d’accueil**, recherchez **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="8995e-125">Run **Windows PowerShell** as Administrator; from the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="8995e-126">[Connectez PowerShell] à votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="8995e-126">[Connect PowerShell] to your subscription.</span></span>
3. <span data-ttu-id="8995e-127">Entrez l’applet de commande PowerShell suivante pour créer le projet :</span><span class="sxs-lookup"><span data-stu-id="8995e-127">Enter the following PowerShell cmdlet to create to create the project:</span></span>

        New-AzureServiceProject helloworld

    ![Le résultat de la nouvelle commande helloworld New-AzureService][The result of the New-AzureService helloworld command]

    <span data-ttu-id="8995e-129">La cmdlet **New-AzureServiceProject** génère une structure de base pour publier une application Node.js dans un service cloud.</span><span class="sxs-lookup"><span data-stu-id="8995e-129">The **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application to a Cloud Service.</span></span> <span data-ttu-id="8995e-130">Elle contient les fichiers de configuration nécessaires à la publication sur Azure.</span><span class="sxs-lookup"><span data-stu-id="8995e-130">It contains configuration files necessary for publishing to Azure.</span></span> <span data-ttu-id="8995e-131">La cmdlet change aussi votre répertoire de travail et le remplace par le répertoire du service.</span><span class="sxs-lookup"><span data-stu-id="8995e-131">The cmdlet also changes your working directory to the directory for the service.</span></span>

    <span data-ttu-id="8995e-132">L’applet de commande crée les fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="8995e-132">The cmdlet creates the following files:</span></span>

   * <span data-ttu-id="8995e-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** et **ServiceDefinition.csdef** sont des fichiers propres à Azure, nécessaires à la publication de votre application.</span><span class="sxs-lookup"><span data-stu-id="8995e-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="8995e-134">Pour plus d'informations, consultez la page [Présentation de la création d'un service hébergé pour Azure].</span><span class="sxs-lookup"><span data-stu-id="8995e-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="8995e-135">**deploymentSettings.json**stocke les paramètres locaux utilisés par les cmdlets de déploiement Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8995e-135">**deploymentSettings.json**: Stores local settings that are used by the Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="8995e-136">Entrez la commande suivante pour ajouter un nouveau rôle Web :</span><span class="sxs-lookup"><span data-stu-id="8995e-136">Enter the following command to add a new web role:</span></span>

       Add-AzureNodeWebRole

   ![Résultat de la commande Add-AzureNodeWebRole][The output of the Add-AzureNodeWebRole command]

   <span data-ttu-id="8995e-138">La cmdlet **Add-AzureNodeWebRole** crée une application Node.js de base.</span><span class="sxs-lookup"><span data-stu-id="8995e-138">The **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="8995e-139">Elle modifie également les fichiers **.csfg** et **.csdef** afin d’ajouter des entrées de configuration pour le nouveau rôle.</span><span class="sxs-lookup"><span data-stu-id="8995e-139">It also modifies the **.csfg** and **.csdef** files to add configuration entries for the new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8995e-140">Si vous ne spécifiez pas de nom de rôle, un nom par défaut est utilisé.</span><span class="sxs-lookup"><span data-stu-id="8995e-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="8995e-141">Vous pouvez indiquer un nom comme premier paramètre de la cmdlet : `Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="8995e-141">You can provide a name as the first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="8995e-142">L’application Node.js est définie dans le fichier **server.js**, situé dans le répertoire du rôle web (**WebRole1** par défaut).</span><span class="sxs-lookup"><span data-stu-id="8995e-142">The Node.js app is defined in the file **server.js**, located in the directory for the web role (**WebRole1** by default).</span></span> <span data-ttu-id="8995e-143">Voici le code :</span><span class="sxs-lookup"><span data-stu-id="8995e-143">Here is the code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="8995e-144">Ce code est essentiellement identique à l’exemple « Hello World » sur le site web [nodejs.org] , sauf qu’il utilise le numéro de port attribué par l’environnement de cloud.</span><span class="sxs-lookup"><span data-stu-id="8995e-144">This code is essentially the same as the "Hello World" sample on the [nodejs.org] website, except it uses the port number assigned by the cloud environment.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="8995e-145">Déploiement de l'application dans Azure</span><span class="sxs-lookup"><span data-stu-id="8995e-145">Deploy the application to Azure</span></span>

> [!NOTE]
> <span data-ttu-id="8995e-146">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="8995e-146">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="8995e-147">Vous pouvez [activer les avantages de votre abonnement MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) ou [vous inscrire pour un compte gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span><span class="sxs-lookup"><span data-stu-id="8995e-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-the-azure-publishing-settings"></a><span data-ttu-id="8995e-148">Télécharger les paramètres de publication Azure</span><span class="sxs-lookup"><span data-stu-id="8995e-148">Download the Azure publishing settings</span></span>
<span data-ttu-id="8995e-149">Pour déployer votre application sur Azure, vous devez télécharger les paramètres de publication de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="8995e-149">To deploy your application to Azure, you must first download the publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="8995e-150">Exécutez l’applet de commande Azure PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="8995e-150">Run the following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="8995e-151">Ceci utilise votre navigateur pour accéder à la page de téléchargement des paramètres de publication.</span><span class="sxs-lookup"><span data-stu-id="8995e-151">This will use your browser to navigate to the publish settings download page.</span></span> <span data-ttu-id="8995e-152">Il est possible que vous soyez invité à vous connecter avec un compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8995e-152">You may be prompted to log in with a Microsoft Account.</span></span> <span data-ttu-id="8995e-153">Si c’est le cas, utilisez le compte associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="8995e-153">If so, use the account associated with your Azure subscription.</span></span>

   <span data-ttu-id="8995e-154">Enregistrez le profil téléchargé dans un emplacement auquel vous pouvez accéder facilement.</span><span class="sxs-lookup"><span data-stu-id="8995e-154">Save the downloaded profile to a file location you can easily access.</span></span>
2. <span data-ttu-id="8995e-155">Exécutez l’applet de commande suivante pour importer le profil de publication que vous avez téléchargé :</span><span class="sxs-lookup"><span data-stu-id="8995e-155">Run following cmdlet to import the publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path to file]

    > [!NOTE]
    > <span data-ttu-id="8995e-156">Après l’importation des paramètres de publication, pensez à supprimer le fichier .publishSettings téléchargé, car il contient des informations qui pourraient permettre à d’autres personnes d’accéder à votre compte.</span><span class="sxs-lookup"><span data-stu-id="8995e-156">After importing the publish settings, consider deleting the downloaded .publishSettings file, because it contains information that could allow someone to access your account.</span></span>

### <a name="publish-the-application"></a><span data-ttu-id="8995e-157">Publication de l'application</span><span class="sxs-lookup"><span data-stu-id="8995e-157">Publish the application</span></span>
<span data-ttu-id="8995e-158">Pour publier, exécutez les commande suivantes :</span><span class="sxs-lookup"><span data-stu-id="8995e-158">To publish, run the following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="8995e-159">**-ServiceName** indique le nom du déploiement.</span><span class="sxs-lookup"><span data-stu-id="8995e-159">**-ServiceName** specifies the name for the deployment.</span></span> <span data-ttu-id="8995e-160">Ce nom doit être unique, sans quoi le processus de publication échouera.</span><span class="sxs-lookup"><span data-stu-id="8995e-160">This must be a unique name, otherwise the publish process will fail.</span></span> <span data-ttu-id="8995e-161">La commande **Get-Date** s'attache à une chaîne de date et d'heure qui doit rendre le nom unique.</span><span class="sxs-lookup"><span data-stu-id="8995e-161">The **Get-Date** command tacks on a date/time string that should make the name unique.</span></span>
* <span data-ttu-id="8995e-162">**-Emplacement** indique le centre de données dans lequel l'application sera hébergée.</span><span class="sxs-lookup"><span data-stu-id="8995e-162">**-Location** specifies the datacenter that the application will be hosted in.</span></span> <span data-ttu-id="8995e-163">Pour afficher une liste des centres de données disponibles, utilisez la cmdlet **Get-AzureLocation** .</span><span class="sxs-lookup"><span data-stu-id="8995e-163">To see a list of available datacenters, use the **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="8995e-164">**-Launch** ouvre une fenêtre de navigateur et accède au service hébergé une fois le déploiement terminé.</span><span class="sxs-lookup"><span data-stu-id="8995e-164">**-Launch** opens a browser window and navigates to the hosted service after deployment has completed.</span></span>

<span data-ttu-id="8995e-165">Une fois la publication effectuée, vous devez obtenir une réponse semblable à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="8995e-165">After publishing succeeds, you will see a response similar to the following:</span></span>

![Résultat de la commande Publish-AzureService][The output of the Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="8995e-167">Il peut s’écouler plusieurs minutes avant que l’application soit déployée et disponible lors de la première publication.</span><span class="sxs-lookup"><span data-stu-id="8995e-167">It can take several minutes for the application to deploy and become available when first published.</span></span>

<span data-ttu-id="8995e-168">Une fois le déploiement terminé, une fenêtre de navigateur s'ouvre et accède au service cloud.</span><span class="sxs-lookup"><span data-stu-id="8995e-168">Once the deployment has completed, a browser window will open and navigate to the cloud service.</span></span>

![Fenêtre de navigateur affichant la page Hello World ; l’URL indique que la page est hébergée sur Azure.][A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.]

<span data-ttu-id="8995e-170">Votre application s'exécute maintenant sur Azure.</span><span class="sxs-lookup"><span data-stu-id="8995e-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="8995e-171">La cmdlet **Publish-AzureServiceProject** effectue les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8995e-171">The **Publish-AzureServiceProject** cmdlet performs the following steps:</span></span>

1. <span data-ttu-id="8995e-172">Elle crée un package à déployer.</span><span class="sxs-lookup"><span data-stu-id="8995e-172">Creates a package to deploy.</span></span> <span data-ttu-id="8995e-173">Ce package contient tous les fichiers de votre dossier d’application.</span><span class="sxs-lookup"><span data-stu-id="8995e-173">The package contains all the files in your application folder.</span></span>
2. <span data-ttu-id="8995e-174">Elle crée un **compte de stockage** , si celui-ci n'existe pas.</span><span class="sxs-lookup"><span data-stu-id="8995e-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="8995e-175">Le compte de stockage Azure permet de stocker le package de l'application au cours du déploiement.</span><span class="sxs-lookup"><span data-stu-id="8995e-175">The Azure storage account is used to store the application package during deployment.</span></span> <span data-ttu-id="8995e-176">Vous pouvez supprimer en toute sécurité le compte de stockage une fois le déploiement terminé.</span><span class="sxs-lookup"><span data-stu-id="8995e-176">You can safely delete the storage account after deployment is done.</span></span>
3. <span data-ttu-id="8995e-177">Elle crée un **service cloud** , si celui-ci n'existe pas.</span><span class="sxs-lookup"><span data-stu-id="8995e-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="8995e-178">Le **service cloud** est le conteneur dans lequel votre application est hébergée lorsqu'elle est déployée sur Azure.</span><span class="sxs-lookup"><span data-stu-id="8995e-178">A **cloud service** is the container in which your application is hosted when it is deployed to Azure.</span></span> <span data-ttu-id="8995e-179">Pour plus d'informations, consultez la page [Présentation de la création d'un service hébergé pour Azure].</span><span class="sxs-lookup"><span data-stu-id="8995e-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="8995e-180">Elle publie le package de déploiement sur Azure.</span><span class="sxs-lookup"><span data-stu-id="8995e-180">Publishes the deployment package to Azure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="8995e-181">Arrêt et suppression de votre application</span><span class="sxs-lookup"><span data-stu-id="8995e-181">Stopping and deleting your application</span></span>
<span data-ttu-id="8995e-182">Après avoir déployé votre application, vous pouvez la désactiver afin de vous éviter des coûts supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="8995e-182">After deploying your application, you may want to disable it so you can avoid extra costs.</span></span> <span data-ttu-id="8995e-183">Azure facture les instances de rôle Web par heure de serveur consommée.</span><span class="sxs-lookup"><span data-stu-id="8995e-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="8995e-184">Une fois votre application déployée, elle consomme du temps de serveur, même si les instances ne sont pas exécutées et sont arrêtées.</span><span class="sxs-lookup"><span data-stu-id="8995e-184">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

1. <span data-ttu-id="8995e-185">Dans la fenêtre Windows PowerShell, arrêtez le déploiement du service créé dans la section précédente à l'aide de la cmdlet suivante :</span><span class="sxs-lookup"><span data-stu-id="8995e-185">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="8995e-186">L'arrêt du service peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="8995e-186">Stopping the service may take several minutes.</span></span> <span data-ttu-id="8995e-187">Une fois le service arrêté, vous recevez un message confirmant l'arrêt du service.</span><span class="sxs-lookup"><span data-stu-id="8995e-187">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![État de la commande Stop-AzureService.][The status of the Stop-AzureService command]
2. <span data-ttu-id="8995e-189">Pour supprimer le service, utilisez la cmdlet suivante :</span><span class="sxs-lookup"><span data-stu-id="8995e-189">To delete the service, call the following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="8995e-190">Lorsque vous y êtes invité, entrez **Y** pour supprimer le service.</span><span class="sxs-lookup"><span data-stu-id="8995e-190">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="8995e-191">La suppression du service peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="8995e-191">Deleting the service may take several minutes.</span></span> <span data-ttu-id="8995e-192">Une fois le service supprimé, vous recevez un message confirmant la suppression du service.</span><span class="sxs-lookup"><span data-stu-id="8995e-192">After the service has been deleted you receive a message indicating that the service was deleted.</span></span>

   ![État de la commande Remove-AzureService][The status of the Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="8995e-194">La suppression du service ne supprime pas le compte de stockage qui a été créé lors de la publication initiale du service. Le stockage utilisé continuera à vous être facturé.</span><span class="sxs-lookup"><span data-stu-id="8995e-194">Deleting the service does not delete the storage account that was created when the service was initially published, and you will continue to be billed for storage used.</span></span> <span data-ttu-id="8995e-195">Si aucun autre élément n’utilise le stockage, il peut être préférable de le supprimer.</span><span class="sxs-lookup"><span data-stu-id="8995e-195">If nothing else is using the storage, you may want to delete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8995e-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8995e-196">Next steps</span></span>
<span data-ttu-id="8995e-197">Pour plus d’informations, consultez le [Centre pour développeurs Node.js].</span><span class="sxs-lookup"><span data-stu-id="8995e-197">For more information, see the [Node.js Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="8995e-198">[Comparaison des sites Web Azure, des services cloud et des machines virtuelles]: ../app-service-web/choose-web-site-cloud-service-vm.md</span><span class="sxs-lookup"><span data-stu-id="8995e-198">[Azure Websites, Cloud Services and Virtual Machines comparison]: ../app-service-web/choose-web-site-cloud-service-vm.md</span></span>
<span data-ttu-id="8995e-199">[utiliser une application web légère]: ../app-service-web/app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="8995e-199">[using a lightweight web app]: ../app-service-web/app-service-web-get-started-nodejs.md</span></span>
<span data-ttu-id="8995e-200">[Azure PowerShell]: /powershell/azureps-cmdlets-docs</span><span class="sxs-lookup"><span data-stu-id="8995e-200">[Azure Powershell]: /powershell/azureps-cmdlets-docs</span></span>
<span data-ttu-id="8995e-201">[Kit de développement logiciel (SDK) Azure pour .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178</span><span class="sxs-lookup"><span data-stu-id="8995e-201">[Azure SDK for .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178</span></span>
<span data-ttu-id="8995e-202">[Connectez PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect</span><span class="sxs-lookup"><span data-stu-id="8995e-202">[Connect PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect</span></span>
<span data-ttu-id="8995e-203">[nodejs.org]: http://nodejs.org/</span><span class="sxs-lookup"><span data-stu-id="8995e-203">[nodejs.org]: http://nodejs.org/</span></span>
<span data-ttu-id="8995e-204">[Présentation de la création d'un service hébergé pour Azure]: https://azure.microsoft.com/documentation/services/cloud-services/</span><span class="sxs-lookup"><span data-stu-id="8995e-204">[Overview of Creating a Hosted Service for Azure]: https://azure.microsoft.com/documentation/services/cloud-services/</span></span>
<span data-ttu-id="8995e-205">[Centre pour développeurs Node.js]: https://azure.microsoft.com/develop/nodejs/</span><span class="sxs-lookup"><span data-stu-id="8995e-205">[Node.js Developer Center]: https://azure.microsoft.com/develop/nodejs/</span></span>

<!-- IMG List -->

[The result of the New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[The output of the Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying the Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[The output of the Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[The status of the Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[The status of the Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
