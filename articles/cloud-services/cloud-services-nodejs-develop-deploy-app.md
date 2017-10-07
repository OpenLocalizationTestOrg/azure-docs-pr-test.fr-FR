---
title: aaaNode.js Getting Started Guide | Documents Microsoft
description: "Découvrez comment toocreate un Node.js simple application web et service de cloud Azure tooan le déployer."
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
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a><span data-ttu-id="3dc9b-103">Créer et déployer un tooan d’application Node.js Azure Cloud Service</span><span class="sxs-lookup"><span data-stu-id="3dc9b-103">Build and deploy a Node.js application tooan Azure Cloud Service</span></span>

<span data-ttu-id="3dc9b-104">Ce didacticiel montre comment toocreate un Node.js simple application qui s’exécute dans un Service Cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-104">This tutorial shows how toocreate a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="3dc9b-105">Services de cloud computing sont les blocs de construction de hello d’applications cloud évolutives dans Azure.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-105">Cloud Services are hello building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="3dc9b-106">Elles permettent de séparation de hello et gestion indépendante et montée en puissance parallèle de serveurs frontaux et principaux composants de votre application.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-106">They allow hello separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="3dc9b-107">Cloud Services héberge de façon fiable chaque rôle sur une machine virtuelle dédiée.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="3dc9b-108">Pour plus d’informations sur les Services de cloud computing et leurs particularités tooAzure sites Web et les machines virtuelles, consultez [comparaison de sites Web Azure, Services de cloud computing et Machines virtuelles].</span><span class="sxs-lookup"><span data-stu-id="3dc9b-108">For more information on Cloud Services, and how they compare tooAzure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="3dc9b-109">Recherchez toobuild un site Web simple ?</span><span class="sxs-lookup"><span data-stu-id="3dc9b-109">Looking toobuild a simple website?</span></span> <span data-ttu-id="3dc9b-110">Si votre scénario ne comporte qu’un simple composant frontal web, envisagez d’[utiliser une application web légère].</span><span class="sxs-lookup"><span data-stu-id="3dc9b-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="3dc9b-111">Vous pouvez facilement mettre à niveau tooa Service de cloud computing que votre application web se développe et l’évolution de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-111">You can easily upgrade tooa Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="3dc9b-112">Dans ce didacticiel, vous allez créer une application Web simple, hébergée dans un rôle Web.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="3dc9b-113">Vous serez utiliser, hello calcul émulateur tootest votre application localement, puis déployez-la à l’aide des outils de ligne de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-113">You will use hello compute emulator tootest your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="3dc9b-114">application Hello est une application « hello world » simple :</span><span class="sxs-lookup"><span data-stu-id="3dc9b-114">hello application is a simple "hello world" application:</span></span>

![Un navigateur web affichage page web de Hello World hello][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="3dc9b-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3dc9b-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="3dc9b-117">Ce didacticiel utilise Azure PowerShell, qui nécessite Windows.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="3dc9b-118">Installez et configurez [Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="3dc9b-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="3dc9b-119">Téléchargez et installez hello [Azure SDK pour .NET 2.7].</span><span class="sxs-lookup"><span data-stu-id="3dc9b-119">Download and install hello [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="3dc9b-120">Bonjour, installer le programme d’installation, sélectionnez :</span><span class="sxs-lookup"><span data-stu-id="3dc9b-120">In hello install setup, select:</span></span>
  * <span data-ttu-id="3dc9b-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="3dc9b-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="3dc9b-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="3dc9b-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="3dc9b-123">Créer un projet Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="3dc9b-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="3dc9b-124">Effectuez hello suivant de tâches toocreate un nouveau projet de Service Cloud Azure, ainsi que la structure de Node.js base :</span><span class="sxs-lookup"><span data-stu-id="3dc9b-124">Perform hello following tasks toocreate a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="3dc9b-125">Exécutez **Windows PowerShell** en tant qu’administrateur ; à partir de hello **Menu Démarrer** ou **écran d’accueil de**, recherchez **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-125">Run **Windows PowerShell** as Administrator; from hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="3dc9b-126">[Se connecter à PowerShell] tooyour abonnement.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-126">[Connect PowerShell] tooyour subscription.</span></span>
3. <span data-ttu-id="3dc9b-127">Entrez hello suivant le projet hello toocreate PowerShell applet de commande toocreate :</span><span class="sxs-lookup"><span data-stu-id="3dc9b-127">Enter hello following PowerShell cmdlet toocreate toocreate hello project:</span></span>

        New-AzureServiceProject helloworld

    ![résultat de Hello de commande de helloworld hello New-AzureService][hello result of hello New-AzureService helloworld command]

    <span data-ttu-id="3dc9b-129">Hello **New-AzureServiceProject** applet de commande génère une structure de base pour la publication d’un tooa d’application Node.js Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-129">hello **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application tooa Cloud Service.</span></span> <span data-ttu-id="3dc9b-130">Il contient les fichiers de configuration nécessaires à la publication tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-130">It contains configuration files necessary for publishing tooAzure.</span></span> <span data-ttu-id="3dc9b-131">applet de commande Hello change également votre répertoire toohello répertoire de travail hello service.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-131">hello cmdlet also changes your working directory toohello directory for hello service.</span></span>

    <span data-ttu-id="3dc9b-132">applet de commande Hello crée hello fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="3dc9b-132">hello cmdlet creates hello following files:</span></span>

   * <span data-ttu-id="3dc9b-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** et **ServiceDefinition.csdef** sont des fichiers propres à Azure, nécessaires à la publication de votre application.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="3dc9b-134">Pour plus d'informations, consultez la page [Présentation de la création d'un service hébergé pour Azure].</span><span class="sxs-lookup"><span data-stu-id="3dc9b-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="3dc9b-135">**deploymentSettings.json**: stocke les paramètres locaux qui sont utilisés par hello applets de commande de déploiement Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-135">**deploymentSettings.json**: Stores local settings that are used by hello Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="3dc9b-136">Entrez hello suivant commande tooadd un nouveau rôle web :</span><span class="sxs-lookup"><span data-stu-id="3dc9b-136">Enter hello following command tooadd a new web role:</span></span>

       Add-AzureNodeWebRole

   ![sortie Hello Hello Add-AzureNodeWebRole commande][hello output of hello Add-AzureNodeWebRole command]

   <span data-ttu-id="3dc9b-138">Hello **Add-AzureNodeWebRole** applet de commande crée une application Node.js base.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-138">hello **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="3dc9b-139">Il modifie également hello **.csfg** et **.csdef** fichiers tooadd les entrées de configuration pour le nouveau rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-139">It also modifies hello **.csfg** and **.csdef** files tooadd configuration entries for hello new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3dc9b-140">Si vous ne spécifiez pas de nom de rôle, un nom par défaut est utilisé.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="3dc9b-141">Vous pouvez fournir un nom en tant que paramètre d’applet de commande premier hello :`Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="3dc9b-141">You can provide a name as hello first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="3dc9b-142">application de Node.js Hello est définie dans le fichier de hello **server.js**, situé dans le répertoire hello pour le rôle web de hello (**WebRole1** par défaut).</span><span class="sxs-lookup"><span data-stu-id="3dc9b-142">hello Node.js app is defined in hello file **server.js**, located in hello directory for hello web role (**WebRole1** by default).</span></span> <span data-ttu-id="3dc9b-143">Voici le code de hello :</span><span class="sxs-lookup"><span data-stu-id="3dc9b-143">Here is hello code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="3dc9b-144">Ce code est essentiellement les hello identique hello « Hello World » exemple sur hello [nodejs.org] site Web, sauf qu’elle utilise le numéro de port hello affecté par l’environnement de cloud hello.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-144">This code is essentially hello same as hello "Hello World" sample on hello [nodejs.org] website, except it uses hello port number assigned by hello cloud environment.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="3dc9b-145">Déployer hello application tooAzure</span><span class="sxs-lookup"><span data-stu-id="3dc9b-145">Deploy hello application tooAzure</span></span>

> [!NOTE]
> <span data-ttu-id="3dc9b-146">toocomplete ce didacticiel, vous avez besoin d’un compte Azure.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-146">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="3dc9b-147">Vous pouvez [activer les avantages de votre abonnement MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) ou [vous inscrire pour un compte gratuit](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span><span class="sxs-lookup"><span data-stu-id="3dc9b-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-hello-azure-publishing-settings"></a><span data-ttu-id="3dc9b-148">Télécharger hello Azure paramètres de publication</span><span class="sxs-lookup"><span data-stu-id="3dc9b-148">Download hello Azure publishing settings</span></span>
<span data-ttu-id="3dc9b-149">toodeploy tooAzure de votre application, vous devez d’abord télécharger hello pour votre abonnement Azure, les paramètres de publication.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-149">toodeploy your application tooAzure, you must first download hello publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="3dc9b-150">Exécutez hello suivant l’applet de commande PowerShell de Azure :</span><span class="sxs-lookup"><span data-stu-id="3dc9b-150">Run hello following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="3dc9b-151">Ce processus utilisera votre navigateur toonavigate toohello page de téléchargement des paramètres de publication.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-151">This will use your browser toonavigate toohello publish settings download page.</span></span> <span data-ttu-id="3dc9b-152">Vous pouvez être invité à toolog avec un Account Microsoft.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-152">You may be prompted toolog in with a Microsoft Account.</span></span> <span data-ttu-id="3dc9b-153">Dans ce cas, utilisez le compte hello associé à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-153">If so, use hello account associated with your Azure subscription.</span></span>

   <span data-ttu-id="3dc9b-154">Vous pouvez accéder facilement à hello téléchargé profil tooa fichier emplacement d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-154">Save hello downloaded profile tooa file location you can easily access.</span></span>
2. <span data-ttu-id="3dc9b-155">Exécutez suivante hello de tooimport d’applet de commande profil que vous avez téléchargé de publication :</span><span class="sxs-lookup"><span data-stu-id="3dc9b-155">Run following cmdlet tooimport hello publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > <span data-ttu-id="3dc9b-156">Après l’importation hello paramètres de publication, envisagez de suppression hello de télécharger le fichier .publishSettings, car il contient des informations qui pourrait permettre à une personne tooaccess votre compte.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-156">After importing hello publish settings, consider deleting hello downloaded .publishSettings file, because it contains information that could allow someone tooaccess your account.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="3dc9b-157">Publier l’application hello</span><span class="sxs-lookup"><span data-stu-id="3dc9b-157">Publish hello application</span></span>
<span data-ttu-id="3dc9b-158">toopublish, exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="3dc9b-158">toopublish, run hello following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="3dc9b-159">**-ServiceName** Spécifie le nom hello pour le déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-159">**-ServiceName** specifies hello name for hello deployment.</span></span> <span data-ttu-id="3dc9b-160">Cela doit être un nom unique, sinon hello publier le processus échoue.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-160">This must be a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="3dc9b-161">Hello **Get-Date** commande s’attache à une chaîne de date/heure qui doit rendre le nom de hello unique.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-161">hello **Get-Date** command tacks on a date/time string that should make hello name unique.</span></span>
* <span data-ttu-id="3dc9b-162">**-Location** spécifie hello de centre de données qui sera hébergée dans application hello.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-162">**-Location** specifies hello datacenter that hello application will be hosted in.</span></span> <span data-ttu-id="3dc9b-163">toosee une liste des centres de données disponibles, utilisez hello **Get-AzureLocation** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-163">toosee a list of available datacenters, use hello **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="3dc9b-164">**-Lancer** ouvre une fenêtre de navigateur et navigue toohello hébergé service après le déploiement est terminé.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-164">**-Launch** opens a browser window and navigates toohello hosted service after deployment has completed.</span></span>

<span data-ttu-id="3dc9b-165">Une fois la publication effectuée, vous découvrez une réponse similaire toohello :</span><span class="sxs-lookup"><span data-stu-id="3dc9b-165">After publishing succeeds, you will see a response similar toohello following:</span></span>

![sortie Hello Hello Publish-AzureService commande][hello output of hello Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="3dc9b-167">Il peut prendre plusieurs minutes pour hello application toodeploy et sont disponible lors de la première publication.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-167">It can take several minutes for hello application toodeploy and become available when first published.</span></span>

<span data-ttu-id="3dc9b-168">Une fois le déploiement de hello est terminée, une fenêtre de navigateur vous ouvrez et accédez toohello le service cloud.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-168">Once hello deployment has completed, a browser window will open and navigate toohello cloud service.</span></span>

![Une fenêtre de navigateur affichant hello hello world page ; URL de Hello indique la page de hello est hébergé sur Azure.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

<span data-ttu-id="3dc9b-170">Votre application s'exécute maintenant sur Azure.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="3dc9b-171">Hello **AzureServiceProject de publication** applet de commande effectue hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="3dc9b-171">hello **Publish-AzureServiceProject** cmdlet performs hello following steps:</span></span>

1. <span data-ttu-id="3dc9b-172">Crée un toodeploy du package.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-172">Creates a package toodeploy.</span></span> <span data-ttu-id="3dc9b-173">Hello contient tous les fichiers hello dans votre dossier d’application.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-173">hello package contains all hello files in your application folder.</span></span>
2. <span data-ttu-id="3dc9b-174">Elle crée un **compte de stockage** , si celui-ci n'existe pas.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="3dc9b-175">Hello compte de stockage Azure est un package d’application hello toostore utilisés pendant le déploiement.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-175">hello Azure storage account is used toostore hello application package during deployment.</span></span> <span data-ttu-id="3dc9b-176">Vous pouvez supprimer en toute sécurité de compte de stockage hello après le déploiement.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-176">You can safely delete hello storage account after deployment is done.</span></span>
3. <span data-ttu-id="3dc9b-177">Elle crée un **service cloud** , si celui-ci n'existe pas.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="3dc9b-178">A **service de cloud computing** est conteneur hello dans lequel votre application est hébergée lorsqu’il est déployé tooAzure.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-178">A **cloud service** is hello container in which your application is hosted when it is deployed tooAzure.</span></span> <span data-ttu-id="3dc9b-179">Pour plus d'informations, consultez la page [Présentation de la création d'un service hébergé pour Azure].</span><span class="sxs-lookup"><span data-stu-id="3dc9b-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="3dc9b-180">Publie tooAzure de package de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-180">Publishes hello deployment package tooAzure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="3dc9b-181">Arrêt et suppression de votre application</span><span class="sxs-lookup"><span data-stu-id="3dc9b-181">Stopping and deleting your application</span></span>
<span data-ttu-id="3dc9b-182">Après avoir déployé votre application, vous souhaiterez peut-être toodisable il afin d’éviter des coûts supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-182">After deploying your application, you may want toodisable it so you can avoid extra costs.</span></span> <span data-ttu-id="3dc9b-183">Azure facture les instances de rôle Web par heure de serveur consommée.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="3dc9b-184">Heure du serveur est utilisée une fois que votre application est déployée, même si les instances de hello ne sont pas en cours d’exécution et état de hello s’est arrêté.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-184">Server time is consumed once your application is deployed, even if hello instances are not running and are in hello stopped state.</span></span>

1. <span data-ttu-id="3dc9b-185">Dans la fenêtre Windows PowerShell de hello, arrêter le déploiement de service hello créé dans la section précédente de hello avec hello suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="3dc9b-185">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="3dc9b-186">L’arrêt du service de hello peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-186">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="3dc9b-187">Lors de l’arrêt du service de hello, vous recevez un message indiquant qu’il s’est arrêtée.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-187">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![état Hello de commande hello Stop-AzureService][hello status of hello Stop-AzureService command]
2. <span data-ttu-id="3dc9b-189">service de hello toodelete, hello appel suivant l’applet de commande :</span><span class="sxs-lookup"><span data-stu-id="3dc9b-189">toodelete hello service, call hello following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="3dc9b-190">Lorsque vous y êtes invité, entrez **Y** service de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-190">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="3dc9b-191">Suppression du service de hello peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-191">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="3dc9b-192">Une fois que le service de hello a été supprimé, vous recevez un message indiquant que le service de hello a été supprimée.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-192">After hello service has been deleted you receive a message indicating that hello service was deleted.</span></span>

   ![état Hello de commande Remove-AzureService de hello][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="3dc9b-194">Suppression du service de hello ne supprime pas le compte de stockage hello qui a été créé lorsque hello service a été initialement publié, et vous continuerez toobe facturé en fonction de stockage utilisé.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-194">Deleting hello service does not delete hello storage account that was created when hello service was initially published, and you will continue toobe billed for storage used.</span></span> <span data-ttu-id="3dc9b-195">Si rien d’autre utilise le stockage de hello, vous souhaiterez peut-être toodelete il.</span><span class="sxs-lookup"><span data-stu-id="3dc9b-195">If nothing else is using hello storage, you may want toodelete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dc9b-196">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3dc9b-196">Next steps</span></span>
<span data-ttu-id="3dc9b-197">Pour plus d’informations, consultez hello [centre de développement Node.js].</span><span class="sxs-lookup"><span data-stu-id="3dc9b-197">For more information, see hello [Node.js Developer Center].</span></span>

<!-- URL List -->

[comparaison de sites Web Azure, Services de cloud computing et Machines virtuelles]: ../app-service-web/choose-web-site-cloud-service-vm.md
[utiliser une application web légère]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Azure SDK pour .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[Se connecter à PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Présentation de la création d'un service hébergé pour Azure]: https://azure.microsoft.com/documentation/services/cloud-services/
[centre de développement Node.js]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
