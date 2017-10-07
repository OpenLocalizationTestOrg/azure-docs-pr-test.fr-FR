---
title: "déploiement d’ordinateur virtuel aaaAzure avec Chef | Documents Microsoft"
description: "Découvrez comment toouse Chef toodo automatisé déploiement d’ordinateurs virtuels et de configuration sur Microsoft Azure"
services: virtual-machines-windows
documentationcenter: 
author: diegoviso
manager: timlt
tags: azure-service-management,azure-resource-manager
editor: 
ms.assetid: 0b82ca70-89ed-496d-bb49-c04ae59b4523
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: diviso
ms.openlocfilehash: c5ea98c673b2ee75dd4cedf27e50330af05230d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automating-azure-virtual-machine-deployment-with-chef"></a><span data-ttu-id="24725-103">Automatisation du déploiement de machine virtuelle Azure avec Chef</span><span class="sxs-lookup"><span data-stu-id="24725-103">Automating Azure virtual machine deployment with Chef</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="24725-104">Chef est un excellent outil d’automatisation et de fourniture des configurations d’état souhaitées.</span><span class="sxs-lookup"><span data-stu-id="24725-104">Chef is a great tool for delivering automation and desired state configurations.</span></span>

<span data-ttu-id="24725-105">Avec notre dernière version de l’api du cloud, Chef fournit une intégration transparente avec Azure, ce qui vous hello tooprovision de capacité et déployer des États de configuration via une commande unique.</span><span class="sxs-lookup"><span data-stu-id="24725-105">With our latest cloud-api release, Chef provides seamless integration with Azure, giving you hello ability tooprovision and deploy configuration states through a single command.</span></span>

<span data-ttu-id="24725-106">Dans cet article, vous allez apprendre comment tooset de votre tooprovision d’environnement Chef Azure virtual machines et vous guide dans la création d’une stratégie ou un « Livre de recettes » et puis de déployer cette tooan cookbook machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="24725-106">In this article, I’ll show you how tooset up your Chef environment tooprovision Azure virtual machines and walk you through creating a policy or “CookBook” and then deploying this cookbook tooan Azure virtual machine.</span></span>

<span data-ttu-id="24725-107">Commençons !</span><span class="sxs-lookup"><span data-stu-id="24725-107">Let’s begin!</span></span>

## <a name="chef-basics"></a><span data-ttu-id="24725-108">Principes fondamentaux de Chef</span><span class="sxs-lookup"><span data-stu-id="24725-108">Chef basics</span></span>
<span data-ttu-id="24725-109">Avant de commencer, je vous suggère de que vous passez en revue les concepts de base hello du Chef.</span><span class="sxs-lookup"><span data-stu-id="24725-109">Before you begin, I suggest you review hello basic concepts of Chef.</span></span> <span data-ttu-id="24725-110">Des éléments très intéressants sont disponibles <a href="http://www.chef.io/chef" target="_blank">ici</a> et nous vous recommandons de les passer en revue avant de suivre ce guide.</span><span class="sxs-lookup"><span data-stu-id="24725-110">There is great material <a href="http://www.chef.io/chef" target="_blank">here</a> and I recommend you have a quick read before you attempt this walkthrough.</span></span> <span data-ttu-id="24725-111">J’ai toutefois récapitulent les principes de base hello avant de commencer.</span><span class="sxs-lookup"><span data-stu-id="24725-111">I will however recap hello basics before we get started.</span></span>

<span data-ttu-id="24725-112">Hello suivant schéma décrit l’architecture de Chef hello globale.</span><span class="sxs-lookup"><span data-stu-id="24725-112">hello following diagram depicts hello high-level Chef architecture.</span></span>

![][2]

<span data-ttu-id="24725-113">Chef présente trois principaux composants architecturaux : le serveur Chef, le client Chef (nœud) et la station de travail Chef.</span><span class="sxs-lookup"><span data-stu-id="24725-113">Chef has three main architectural components: Chef Server, Chef Client (node), and Chef Workstation.</span></span>

<span data-ttu-id="24725-114">Hello serveur Chef est le point de gestion et il existe deux options pour le serveur Chef de hello : une solution hébergée ou une solution sur site.</span><span class="sxs-lookup"><span data-stu-id="24725-114">hello Chef Server is our management point and there are two options for hello Chef Server: a hosted solution or an on-premises solution.</span></span> <span data-ttu-id="24725-115">Nous allons utiliser une solution hébergée.</span><span class="sxs-lookup"><span data-stu-id="24725-115">We will be using a hosted solution.</span></span>

<span data-ttu-id="24725-116">Client Hello Chef (nœud) est l’agent hello qui se trouve sur les serveurs hello que vous gérez.</span><span class="sxs-lookup"><span data-stu-id="24725-116">hello Chef Client (node) is hello agent that sits on hello servers you are managing.</span></span>

<span data-ttu-id="24725-117">Hello station de travail Chef est notre station de travail administration, où nous créer notre stratégie et exécuter des commandes de gestion de notre.</span><span class="sxs-lookup"><span data-stu-id="24725-117">hello Chef Workstation is our admin workstation where we create our policies and execute our management commands.</span></span> <span data-ttu-id="24725-118">Nous exécutons hello **knife** de commande à partir de la station de travail Chef toomanage de hello notre infrastructure.</span><span class="sxs-lookup"><span data-stu-id="24725-118">We run hello **knife** command from hello Chef Workstation toomanage our infrastructure.</span></span>

<span data-ttu-id="24725-119">Il est également hello concept de « Cuisine » et « Recettes ».</span><span class="sxs-lookup"><span data-stu-id="24725-119">There is also hello concept of “Cookbooks” and “Recipes”.</span></span> <span data-ttu-id="24725-120">Ceux-ci sont effectivement des stratégies hello nous définir et appliquer des serveurs de tooour.</span><span class="sxs-lookup"><span data-stu-id="24725-120">These are effectively hello policies we define and apply tooour servers.</span></span>

## <a name="preparing-hello-workstation"></a><span data-ttu-id="24725-121">Préparation de la station de travail hello</span><span class="sxs-lookup"><span data-stu-id="24725-121">Preparing hello workstation</span></span>
<span data-ttu-id="24725-122">Tout d’abord, vous permet de station de travail de préparation hello.</span><span class="sxs-lookup"><span data-stu-id="24725-122">First, lets prep hello workstation.</span></span> <span data-ttu-id="24725-123">J’utilise une station de travail Windows standard.</span><span class="sxs-lookup"><span data-stu-id="24725-123">I’m using a standard Windows workstation.</span></span> <span data-ttu-id="24725-124">Nous devons toocreate un toostore directory nos fichiers de configuration et les livres de cuisine.</span><span class="sxs-lookup"><span data-stu-id="24725-124">We need toocreate a directory toostore our config files and cookbooks.</span></span>

<span data-ttu-id="24725-125">Commencez par créer un répertoire appelé C:\chef.</span><span class="sxs-lookup"><span data-stu-id="24725-125">First create a directory called C:\chef.</span></span>

<span data-ttu-id="24725-126">Créez ensuite un second répertoire appelé c:\chef\cookbooks.</span><span class="sxs-lookup"><span data-stu-id="24725-126">Then create a second directory called c:\chef\cookbooks.</span></span>

<span data-ttu-id="24725-127">Nous devons maintenant toodownload notre fichier paramètres Azure pour Chef puisse communiquer avec notre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="24725-127">We now need toodownload our Azure settings file so Chef can communicate with our Azure subscription.</span></span>

<!--Download your publish settings from [here](https://manage.windowsazure.com/publishsettings/).-->
<span data-ttu-id="24725-128">Télécharger vos paramètres à l’aide de hello PowerShell Azure de publication [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) commande.</span><span class="sxs-lookup"><span data-stu-id="24725-128">Download your publish settings using hello PowerShell Azure [Get-AzurePublishSettingsFile](https://docs.microsoft.com/en-us/powershell/module/azure/get-azurepublishsettingsfile?view=azuresmps-4.0.0) command.</span></span> 

<span data-ttu-id="24725-129">Enregistrer hello publier le fichier de paramètres dans C:\chef.</span><span class="sxs-lookup"><span data-stu-id="24725-129">Save hello publish settings file in C:\chef.</span></span>

## <a name="creating-a-managed-chef-account"></a><span data-ttu-id="24725-130">Création d’un compte Chef géré</span><span class="sxs-lookup"><span data-stu-id="24725-130">Creating a managed Chef account</span></span>
<span data-ttu-id="24725-131">Inscrivez-vous à un compte Chef hébergé [ici](https://manage.chef.io/signup).</span><span class="sxs-lookup"><span data-stu-id="24725-131">Sign up for a hosted Chef account [here](https://manage.chef.io/signup).</span></span>

<span data-ttu-id="24725-132">Au cours du processus d’inscription de hello, vous serez invité à toocreate une nouvelle organisation.</span><span class="sxs-lookup"><span data-stu-id="24725-132">During hello signup process, you will be asked toocreate a new organization.</span></span>

![][3]

<span data-ttu-id="24725-133">Une fois que votre organisation est créé, téléchargez hello starter kit.</span><span class="sxs-lookup"><span data-stu-id="24725-133">Once your organization is created, download hello starter kit.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="24725-134">Si vous recevez un message vous avertissant que vos clés sont réinitialisées, il est OK tooproceed que nous ne disposons d’aucune infrastructure existante comme encore configuré.</span><span class="sxs-lookup"><span data-stu-id="24725-134">If you receive a prompt warning you that your keys will be reset, it’s ok tooproceed as we have no existing infrastructure configured as yet.</span></span>
> 
> 

<span data-ttu-id="24725-135">Le fichier zip du starter kit comprend vos clés et fichiers de configuration d’organisation.</span><span class="sxs-lookup"><span data-stu-id="24725-135">This starter kit zip file contains your organization config files and keys.</span></span>

## <a name="configuring-hello-chef-workstation"></a><span data-ttu-id="24725-136">Configuration de station de travail Chef hello</span><span class="sxs-lookup"><span data-stu-id="24725-136">Configuring hello Chef workstation</span></span>
<span data-ttu-id="24725-137">Extraire le contenu de hello de hello chef-starter.zip tooC:\chef.</span><span class="sxs-lookup"><span data-stu-id="24725-137">Extract hello content of hello chef-starter.zip tooC:\chef.</span></span>

<span data-ttu-id="24725-138">Copiez tous les fichiers sous starter\chef-chef-repo\.chef tooyour c:\chef active.</span><span class="sxs-lookup"><span data-stu-id="24725-138">Copy all files under chef-starter\chef-repo\.chef tooyour c:\chef directory.</span></span>

<span data-ttu-id="24725-139">Votre annuaire doit maintenant ressembler à hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="24725-139">Your directory should now look something like hello following example.</span></span>

![][5]

<span data-ttu-id="24725-140">Vous devez maintenant avoir quatre fichiers notamment racine hello c:\chef hello fichier publication Azure.</span><span class="sxs-lookup"><span data-stu-id="24725-140">You should now have four files including hello Azure publishing file in hello root of c:\chef.</span></span>

<span data-ttu-id="24725-141">fichiers PEM de Hello contient votre organisation et l’administration des clés privées pour la communication pendant que le fichier knife.rb de hello contient votre configuration couteau.</span><span class="sxs-lookup"><span data-stu-id="24725-141">hello PEM files contain your organization and admin private keys for communication while hello knife.rb file contains your knife configuration.</span></span> <span data-ttu-id="24725-142">Nous avons besoin tooedit hello knife.rb fichier.</span><span class="sxs-lookup"><span data-stu-id="24725-142">We will need tooedit hello knife.rb file.</span></span>

<span data-ttu-id="24725-143">Ouvrir le fichier de hello dans l’éditeur de votre choix et modifiez hello « cookbook_path » en supprimant les hello /... / à partir du chemin d’accès de hello afin qu’elle apparaisse comme le montre l’illustration suivante.</span><span class="sxs-lookup"><span data-stu-id="24725-143">Open hello file in your editor of choice and modify hello “cookbook_path” by removing hello /../ from hello path so it appears as shown next.</span></span>

    cookbook_path  ["#{current_dir}/cookbooks"]

<span data-ttu-id="24725-144">Ajoutez également réfléchissante nom hello de votre Azure de la ligne suivante de hello publier le fichier de paramètres.</span><span class="sxs-lookup"><span data-stu-id="24725-144">Also add hello following line reflecting hello name of your Azure publish settings file.</span></span>

    knife[:azure_publish_settings_file] = "yourfilename.publishsettings"

<span data-ttu-id="24725-145">Votre fichier knife.rb doit maintenant ressembler toohello similaire, l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="24725-145">Your knife.rb file should now look similar toohello following example.</span></span>

![][6]

<span data-ttu-id="24725-146">Ces lignes garantit que couteau référence active de livres de cuisine hello sous c:\chef\cookbooks et qu’il utilise également le fichier de paramètres de publication Azure lors des opérations de Azure.</span><span class="sxs-lookup"><span data-stu-id="24725-146">These lines will ensure that Knife references hello cookbooks directory under c:\chef\cookbooks, and also uses our Azure Publish Settings file during Azure operations.</span></span>

## <a name="installing-hello-chef-development-kit"></a><span data-ttu-id="24725-147">Lors de l’installation hello Chef Development Kit</span><span class="sxs-lookup"><span data-stu-id="24725-147">Installing hello Chef Development Kit</span></span>
<span data-ttu-id="24725-148">Suivant [Téléchargez et installez](http://downloads.getchef.com/chef-dk/windows) hello tooset ChefDK (Chef Development Kit) de votre station de travail Chef.</span><span class="sxs-lookup"><span data-stu-id="24725-148">Next [download and install](http://downloads.getchef.com/chef-dk/windows) hello ChefDK (Chef Development Kit) tooset up your Chef Workstation.</span></span>

![][7]

<span data-ttu-id="24725-149">Installer dans l’emplacement par défaut hello c:\opscode.</span><span class="sxs-lookup"><span data-stu-id="24725-149">Install in hello default location of c:\opscode.</span></span> <span data-ttu-id="24725-150">Cette opération prendra environ 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="24725-150">This install will take around 10 minutes.</span></span>

<span data-ttu-id="24725-151">Vérifiez que votre variable PATH comprend les entrées de C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;C:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span><span class="sxs-lookup"><span data-stu-id="24725-151">Confirm your PATH variable contains entries for C:\opscode\chefdk\bin;C:\opscode\chefdk\embedded\bin;c:\users\yourusername\.chefdk\gem\ruby\2.0.0\bin</span></span>

<span data-ttu-id="24725-152">S’ils sont absents, assurez-vous de les ajouter !</span><span class="sxs-lookup"><span data-stu-id="24725-152">If they are not there, make sure you add these paths!</span></span>

<span data-ttu-id="24725-153">*Remarque hello ordre de hello chemin d’accès est IMPORTANT !*</span><span class="sxs-lookup"><span data-stu-id="24725-153">*NOTE hello ORDER OF hello PATH IS IMPORTANT!*</span></span> <span data-ttu-id="24725-154">Si les chemins opscode ne sont pas dans l’ordre correct de hello que vous rencontrez des problèmes.</span><span class="sxs-lookup"><span data-stu-id="24725-154">If your opscode paths are not in hello correct order you will have issues.</span></span>

<span data-ttu-id="24725-155">Redémarrez votre station de travail avant de continuer.</span><span class="sxs-lookup"><span data-stu-id="24725-155">Reboot your workstation before you continue.</span></span>

<span data-ttu-id="24725-156">Ensuite, nous allons installer extension d’Azure Knife hello.</span><span class="sxs-lookup"><span data-stu-id="24725-156">Next, we will install hello Knife Azure extension.</span></span> <span data-ttu-id="24725-157">Cela fournit couteau hello « Plug-in Azure ».</span><span class="sxs-lookup"><span data-stu-id="24725-157">This provides Knife with hello “Azure Plugin”.</span></span>

<span data-ttu-id="24725-158">Exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="24725-158">Run hello following command.</span></span>

    chef gem install knife-azure ––pre

> [!NOTE]
> <span data-ttu-id="24725-159">argument de pre-Hello garantit que vous recevez la dernière version RC hello Hello plug-in Azure Knife qui fournit l’accès toohello dernier jeu d’API.</span><span class="sxs-lookup"><span data-stu-id="24725-159">hello –pre argument ensures you are receiving hello latest RC version of hello Knife Azure Plugin which provides access toohello latest set of APIs.</span></span>
> 
> 

<span data-ttu-id="24725-160">Il est probable qu’un nombre de dépendances sera également installé à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="24725-160">It’s likely that a number of dependencies will also be installed at hello same time.</span></span>

![][8]

<span data-ttu-id="24725-161">tooensure que tout est configuré correctement, hello exécution commande suivante.</span><span class="sxs-lookup"><span data-stu-id="24725-161">tooensure everything is configured correctly, run hello following command.</span></span>

    knife azure image list

<span data-ttu-id="24725-162">Si tout est configuré correctement, vous verrez une liste d’images Azure disponibles défiler.</span><span class="sxs-lookup"><span data-stu-id="24725-162">If everything is configured correctly, you will see a list of available Azure images scroll through.</span></span>

<span data-ttu-id="24725-163">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="24725-163">Congratulations.</span></span> <span data-ttu-id="24725-164">station de travail Hello est configurée.</span><span class="sxs-lookup"><span data-stu-id="24725-164">hello workstation is set up!</span></span>

## <a name="creating-a-cookbook"></a><span data-ttu-id="24725-165">Création d’un livre de recettes</span><span class="sxs-lookup"><span data-stu-id="24725-165">Creating a Cookbook</span></span>
<span data-ttu-id="24725-166">Un livre de recettes est utilisé par le Chef toodefine un ensemble de commandes que vous souhaitez tooexecute sur votre client géré.</span><span class="sxs-lookup"><span data-stu-id="24725-166">A Cookbook is used by Chef toodefine a set of commands that you wish tooexecute on your managed client.</span></span> <span data-ttu-id="24725-167">Création d’un livre de recettes est simple et nous utilisons hello **chef générer cookbook** commande toogenerate notre modèle livre de recettes.</span><span class="sxs-lookup"><span data-stu-id="24725-167">Creating a Cookbook is straightforward and we use hello **chef generate cookbook** command toogenerate our Cookbook template.</span></span> <span data-ttu-id="24725-168">Nous appellerons notre livre de recettes webserver, étant donné que je souhaite disposer d’une stratégie qui déploie IIS automatiquement.</span><span class="sxs-lookup"><span data-stu-id="24725-168">I will be calling my Cookbook web server as I would like a policy that automatically deploys IIS.</span></span>

<span data-ttu-id="24725-169">Dans le répertoire C:\Chef exécuter hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="24725-169">Under your C:\Chef directory run hello following command.</span></span>

    chef generate cookbook webserver

<span data-ttu-id="24725-170">Cette opération génère un ensemble de fichiers sous le répertoire hello C:\Chef\cookbooks\webserver.</span><span class="sxs-lookup"><span data-stu-id="24725-170">This will generate a set of files under hello directory C:\Chef\cookbooks\webserver.</span></span> <span data-ttu-id="24725-171">Nous avons maintenant besoin toodefine hello de commandes que nous souhaitons notre tooexecute de client Chef sur notre machine virtuelle gérée.</span><span class="sxs-lookup"><span data-stu-id="24725-171">We now need toodefine hello set of commands we would like our Chef client tooexecute on our managed virtual machine.</span></span>

<span data-ttu-id="24725-172">commandes Hello sont stockés dans hello fichier default.rb.</span><span class="sxs-lookup"><span data-stu-id="24725-172">hello commands are stored in hello file default.rb.</span></span> <span data-ttu-id="24725-173">Dans ce fichier, je vais définissant un ensemble de commandes qui installe les services IIS, démarre IIS et copie un dossier wwwroot toohello modèle.</span><span class="sxs-lookup"><span data-stu-id="24725-173">In this file, I’ll be defining a set of commands that installs IIS, starts IIS and copies a template file toohello wwwroot folder.</span></span>

<span data-ttu-id="24725-174">Modifier le fichier de C:\chef\cookbooks\webserver\recipes\default.rb hello et ajouter les lignes suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="24725-174">Modify hello C:\chef\cookbooks\webserver\recipes\default.rb file and add hello following lines.</span></span>

    powershell_script 'Install IIS' do
         action :run
         code 'add-windowsfeature Web-Server'
    end

    service 'w3svc' do
         action [ :enable, :start ]
    end

    template 'c:\inetpub\wwwroot\Default.htm' do
         source 'Default.htm.erb'
         rights :read, 'Everyone'
    end

<span data-ttu-id="24725-175">Enregistrez le fichier de hello une fois que vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="24725-175">Save hello file once you are done.</span></span>

## <a name="creating-a-template"></a><span data-ttu-id="24725-176">Création d’un modèle</span><span class="sxs-lookup"><span data-stu-id="24725-176">Creating a template</span></span>
<span data-ttu-id="24725-177">Comme mentionné précédemment, nous devons toogenerate un fichier de modèle qui sera utilisé en tant que notre page default.html.</span><span class="sxs-lookup"><span data-stu-id="24725-177">As we mentioned previously, we need toogenerate a template file which will be used as our default.html page.</span></span>

<span data-ttu-id="24725-178">Exécutez hello suivant le modèle de commande toogenerate hello.</span><span class="sxs-lookup"><span data-stu-id="24725-178">Run hello following command toogenerate hello template.</span></span>

    chef generate template webserver Default.htm

<span data-ttu-id="24725-179">Maintenant accédez toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb fichier.</span><span class="sxs-lookup"><span data-stu-id="24725-179">Now navigate toohello C:\chef\cookbooks\webserver\templates\default\Default.htm.erb file.</span></span> <span data-ttu-id="24725-180">Modifier le fichier de hello en ajoutant du code HTML « Hello World » simple, puis enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="24725-180">Edit hello file by adding some simple “Hello World” HTML code, and then save hello file.</span></span>

## <a name="upload-hello-cookbook-toohello-chef-server"></a><span data-ttu-id="24725-181">Télécharger hello Cookbook toohello serveur Chef</span><span class="sxs-lookup"><span data-stu-id="24725-181">Upload hello Cookbook toohello Chef Server</span></span>
<span data-ttu-id="24725-182">Dans cette étape, nous allons prendre une copie de hello Cookbook que nous avons créé sur la machine locale et de les télécharger toohello le serveur Chef hébergé.</span><span class="sxs-lookup"><span data-stu-id="24725-182">In this step, we are taking a copy of hello Cookbook that we have created on our local machine and uploading it toohello Chef Hosted Server.</span></span> <span data-ttu-id="24725-183">Une fois téléchargé, hello Cookbook apparaîtra sous hello **stratégie** onglet.</span><span class="sxs-lookup"><span data-stu-id="24725-183">Once uploaded, hello Cookbook will appear under hello **Policy** tab.</span></span>

    knife cookbook upload webserver

![][9]

## <a name="deploy-a-virtual-machine-with-knife-azure"></a><span data-ttu-id="24725-184">Déployer une machine virtuelle avec Knife Azure</span><span class="sxs-lookup"><span data-stu-id="24725-184">Deploy a virtual machine with Knife Azure</span></span>
<span data-ttu-id="24725-185">Maintenant nous déployer une machine virtuelle Azure et appliquer hello Cookbook « Serveur Web » qui va installer notre page de web IIS web service et la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="24725-185">We will now deploy an Azure virtual machine and apply hello “Webserver” Cookbook which will install our IIS web service and default web page.</span></span>

<span data-ttu-id="24725-186">Dans l’ordre toodo cela, utilisez hello **knife azure serveur créer** commande.</span><span class="sxs-lookup"><span data-stu-id="24725-186">In order toodo this, use hello **knife azure server create** command.</span></span>

<span data-ttu-id="24725-187">Suis exemple de commande hello s’affiche ensuite.</span><span class="sxs-lookup"><span data-stu-id="24725-187">Am example of hello command appears next.</span></span>

    knife azure server create --azure-dns-name 'diegotest01' --azure-vm-name 'testserver01' --azure-vm-size 'Small' --azure-storage-account 'portalvhdsxxxx' --bootstrap-protocol 'cloud-api' --azure-source-image 'a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-Datacenter-201411.01-en.us-127GB.vhd' --azure-service-location 'Southeast Asia' --winrm-user azureuser --winrm-password 'myPassword123' --tcp-endpoints 80,3389 --r 'recipe[webserver]'

<span data-ttu-id="24725-188">paramètres de Hello sont explicites.</span><span class="sxs-lookup"><span data-stu-id="24725-188">hello parameters are self-explanatory.</span></span> <span data-ttu-id="24725-189">Remplacez vos variables particulières et exécutez.</span><span class="sxs-lookup"><span data-stu-id="24725-189">Substitute your particular variables and run.</span></span>

> [!NOTE]
> <span data-ttu-id="24725-190">Via la ligne de commande hello Bonjour, je suis également automatisation mes règles de filtre de point de terminaison réseau à l’aide du paramètre – tcp-points de terminaison de hello.</span><span class="sxs-lookup"><span data-stu-id="24725-190">Through hello hello command line, I’m also automating my endpoint network filter rules by using hello –tcp-endpoints parameter.</span></span> <span data-ttu-id="24725-191">J’ai ouvert les ports 80 et 3389 tooprovide accès toomy web page et session RDP.</span><span class="sxs-lookup"><span data-stu-id="24725-191">I’ve opened up ports 80 and 3389 tooprovide access toomy web page and RDP session.</span></span>
> 
> 

<span data-ttu-id="24725-192">Une fois que vous exécutez la commande hello, accédez toohello Azure portal et vous verrez votre ordinateur commencer tooprovision.</span><span class="sxs-lookup"><span data-stu-id="24725-192">Once you run hello command, go toohello Azure portal and you will see your machine begin tooprovision.</span></span>

![][13]

<span data-ttu-id="24725-193">invite de commandes Hello s’affiche ensuite.</span><span class="sxs-lookup"><span data-stu-id="24725-193">hello command prompt appears next.</span></span>

![][10]

<span data-ttu-id="24725-194">Une fois le déploiement de hello est terminé, nous devons être service web de toohello tooconnect en mesure de via le port 80 comme nous avions ouvert le port de hello lorsque nous avons fourni la machine virtuelle hello hello les commandes Knife Azure.</span><span class="sxs-lookup"><span data-stu-id="24725-194">Once hello deployment is complete, we should be able tooconnect toohello web service over port 80 as we had opened hello port when we provisioned hello virtual machine with hello Knife Azure command.</span></span> <span data-ttu-id="24725-195">Comme cet ordinateur virtuel est hello une machine virtuelle uniquement dans le service cloud, je le connecterai avec l’url du service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="24725-195">As this virtual machine is hello only virtual machine in my cloud service, I’ll connect it with hello cloud service url.</span></span>

![][11]

<span data-ttu-id="24725-196">Comme vous pouvez le voir, le code html est créatif.</span><span class="sxs-lookup"><span data-stu-id="24725-196">As you can see, I got creative with my HTML code.</span></span>

<span data-ttu-id="24725-197">N’oubliez pas que nous pouvons également connecter via une session RDP à partir de hello portail Azure via le port 3389.</span><span class="sxs-lookup"><span data-stu-id="24725-197">Don’t forget we can also connect through an RDP session from hello Azure portal via port 3389.</span></span>

<span data-ttu-id="24725-198">Nous espérons que cela a été utile !</span><span class="sxs-lookup"><span data-stu-id="24725-198">I hope this has been helpful!</span></span> <span data-ttu-id="24725-199">Démarrez votre voyage vers l’Infrastructure en tant que code avec Azure dès aujourd’hui !</span><span class="sxs-lookup"><span data-stu-id="24725-199">Go  and start your infrastructure as code journey with Azure today!</span></span>

<!--Image references-->
[2]: media/chef-automation/2.png
[3]: media/chef-automation/3.png
[4]: media/chef-automation/4.png
[5]: media/chef-automation/5.png
[6]: media/chef-automation/6.png
[7]: media/chef-automation/7.png
[8]: media/chef-automation/8.png
[9]: media/chef-automation/9.png
[10]: media/chef-automation/10.png
[11]: media/chef-automation/11.png
[13]: media/chef-automation/13.png


<!--Link references-->
