---
title: "aaaDeploy un tooLinux d’application Node.js Machines virtuelles dans Azure"
description: "Découvrez comment toodeploy un Node.js ordinateurs virtuels tooLinux d’application dans Azure."
services: 
documentationcenter: nodejs
author: stepro
manager: dmitryr
editor: 
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: /azure
ms.assetid: 857a812d-c73e-4af7-a985-2d0baf8b6f71
ms.service: multiple
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2016
ms.author: stephpr
ms.openlocfilehash: e876c8170a06f102f7f32ec7cb930b876647a707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a><span data-ttu-id="ebfb1-103">Déployer un tooLinux d’application Node.js Machines virtuelles dans Azure</span><span class="sxs-lookup"><span data-stu-id="ebfb1-103">Deploy a Node.js application tooLinux Virtual Machines in Azure</span></span>
<span data-ttu-id="ebfb1-104">Ce didacticiel montre comment tootake une application Node.js et déployer des machines virtuelles de tooLinux s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-104">This tutorial shows how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="ebfb1-105">instructions Hello dans ce didacticiel peuvent être suivies sur n’importe quel système d’exploitation qui est capable d’exécuter Node.js.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-105">hello instructions in this tutorial can be followed on any operating system that is capable of running Node.js.</span></span>

<span data-ttu-id="ebfb1-106">Vous découvrirez comment effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-106">You'll learn how to:</span></span>

* <span data-ttu-id="ebfb1-107">Répliquer et cloner un référentiel GitHub contenant une application TODO simple.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-107">Fork and clone a GitHub repository containing a simple TODO application;</span></span>
* <span data-ttu-id="ebfb1-108">Créez et configurez deux ordinateurs virtuels de Linux dans l’application de hello toorun Azure ;</span><span class="sxs-lookup"><span data-stu-id="ebfb1-108">Create and configure two Linux virtual machines in Azure toorun hello application;</span></span>
* <span data-ttu-id="ebfb1-109">Effectuer une itération sur une application hello en envoyant la machine virtuelle de mises à jour toohello web frontal.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-109">Iterate on hello application by pushing updates toohello web frontend virtual machine.</span></span>

> [!NOTE]
> <span data-ttu-id="ebfb1-110">toocomplete ce didacticiel, vous avez besoin d’un compte GitHub et un compte Microsoft Azure et hello capacité toouse Git à partir d’un ordinateur de développement.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-110">toocomplete this tutorial, you need a GitHub account and a Microsoft Azure account, and hello ability toouse Git from a development machine.</span></span>
> 
> <span data-ttu-id="ebfb1-111">Si vous n’avez pas de compte GitHub, vous pouvez vous inscrire [ici](https://github.com/join).</span><span class="sxs-lookup"><span data-stu-id="ebfb1-111">If you don't have a GitHub account, you can sign up [here](https://github.com/join).</span></span>
> 
> <span data-ttu-id="ebfb1-112">Si vous n’avez pas de compte [Microsoft Azure](https://azure.microsoft.com/), vous pouvez vous inscrire à un essai GRATUIT [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ebfb1-112">If you don't have a [Microsoft Azure](https://azure.microsoft.com/) account, you can sign up for a FREE trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="ebfb1-113">Cela va également vous guider hello inscription pour un [Account Microsoft](http://account.microsoft.com) si vous n’en avez pas déjà.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-113">This will also lead you through hello sign up process for a [Microsoft Account](http://account.microsoft.com) if you do not already have one.</span></span> <span data-ttu-id="ebfb1-114">Par ailleurs, si vous êtes abonné à Visual Studio, vous pouvez [activer vos avantages MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="ebfb1-114">Alternatively, if you are a Visual Studio subscriber, you can [activate your MSDN benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>
> 
> <span data-ttu-id="ebfb1-115">Si vous n’avez pas git sur votre machine de développement et que vous utilisez un ordinateur Macintosh ou Windows, installez git à partir d’ [ici](http://www.git-scm.com).</span><span class="sxs-lookup"><span data-stu-id="ebfb1-115">If you do not have git on your development machine, then if you are using a Macintosh or Windows machine, install git from [here](http://www.git-scm.com).</span></span> <span data-ttu-id="ebfb1-116">Si vous utilisez Linux, installer git à l’aide de mécanisme de hello plus approprié, tel que `sudo apt-get install git`.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-116">If you are using Linux, install git using hello mechanism most appropriate for you, such as `sudo apt-get install git`.</span></span>
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a><span data-ttu-id="ebfb1-117">Coexistence et clonage hello TODO Application</span><span class="sxs-lookup"><span data-stu-id="ebfb1-117">Forking and Cloning hello TODO Application</span></span>
<span data-ttu-id="ebfb1-118">Hello application TODO utilisée par ce didacticiel implémente un serveur frontal web simple sur une instance de MongoDB qui conserve une liste de tâches.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-118">hello TODO application used by this tutorial implements a simple web frontend over a MongoDB instance that keeps track of a TODO list.</span></span> <span data-ttu-id="ebfb1-119">Une fois connectés tooGitHub, accédez [ici](https://github.com/stepro/node-todo) toofind hello application et effectuer un branchement à l’aide de lien de hello en haut à droite hello.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-119">After signing in tooGitHub, go [here](https://github.com/stepro/node-todo) toofind hello application and fork it using hello link in hello top right.</span></span> <span data-ttu-id="ebfb1-120">Cette action doit créer un référentiel dans votre compte nommé *nom_compte*/node-todo.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-120">This should create a repository in your account named *accountname*/node-todo.</span></span>

<span data-ttu-id="ebfb1-121">À présent sur votre machine de développement, clonez ce référentiel :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-121">Now on your development machine, clone this repository:</span></span>

    git clone https://github.com/accountname/node-todo.git

<span data-ttu-id="ebfb1-122">Nous utiliserons ce clone local du référentiel de hello un peu plus tard lors de la modification du code source de toohello.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-122">We'll use this local clone of hello repository a little later when making changes toohello source code.</span></span>

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a><span data-ttu-id="ebfb1-123">Création et configuration hello les Machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="ebfb1-123">Creating and Configuring hello Linux Virtual Machines</span></span>
<span data-ttu-id="ebfb1-124">Azure prend totalement en charge le calcul brut à l’aide de machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-124">Azure has great support for raw compute using Linux virtual machines.</span></span> <span data-ttu-id="ebfb1-125">Cette partie de la montre de didacticiel hello comment vous pouvez facilement faire tourner les deux machines virtuelles de Linux et déployer toothem d’application TODO hello, en cours d’exécution hello du serveur web frontal sur l’un et hello instance MongoDB sur hello autres.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-125">This part of hello tutorial shows how you can easily spin up two Linux virtual machines and deploy hello TODO application toothem, running hello web frontend on one and hello MongoDB instance on hello other.</span></span>

### <a name="creating-virtual-machines"></a><span data-ttu-id="ebfb1-126">Création de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="ebfb1-126">Creating Virtual Machines</span></span>
<span data-ttu-id="ebfb1-127">toocreate de façon plus simple Hello une machine virtuelle dans Azure est toouse hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-127">hello easiest way toocreate a new virtual machine in Azure is toouse hello Azure Portal.</span></span> <span data-ttu-id="ebfb1-128">Cliquez sur [ici](https://portal.azure.com) toosign dans et lancez hello Azure Portal dans votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-128">Click [here](https://portal.azure.com) toosign in and launch hello Azure Portal in your web browser.</span></span> <span data-ttu-id="ebfb1-129">Une fois chargé hello portail Azure, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-129">Once hello Azure Portal has loaded, complete hello following steps:</span></span>

* <span data-ttu-id="ebfb1-130">Cliquez sur hello « + nouveau » lier ;</span><span class="sxs-lookup"><span data-stu-id="ebfb1-130">Click hello "+ New" link;</span></span>
* <span data-ttu-id="ebfb1-131">Sélectionner la catégorie « Calcul » de hello et choisissez « Ubuntu Server 14.04 LTS » ;</span><span class="sxs-lookup"><span data-stu-id="ebfb1-131">Pick hello "Compute" category and choose "Ubuntu Server 14.04 LTS";</span></span>
* <span data-ttu-id="ebfb1-132">Sélectionnez le modèle de déploiement « Gestionnaire de ressources » hello et cliquez sur « Créer » ;</span><span class="sxs-lookup"><span data-stu-id="ebfb1-132">Select hello "Resource Manager" deployment model and click "Create";</span></span>
* <span data-ttu-id="ebfb1-133">Renseignez les principes fondamentaux hello en suivant les recommandations suivantes :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-133">Fill in hello basics following these guidelines:</span></span>
  * <span data-ttu-id="ebfb1-134">Spécifiez un nom que vous pourrez facilement identifier plus tard.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-134">Specify a name you can easily identify later;</span></span>
  * <span data-ttu-id="ebfb1-135">Pour ce didacticiel, choisissez l’authentification par mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-135">For this tutorial, choose Password authentication;</span></span>
  * <span data-ttu-id="ebfb1-136">Créez un groupe de ressources portant un nom identifiable.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-136">Create a new resource group with an identifiable name.</span></span>
* <span data-ttu-id="ebfb1-137">Pourquoi la taille de Machine virtuelle, « A1 Standard » est un choix raisonnable pour ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-137">For hello Virtual Machine size, "A1 Standard" is a reasonable choice for this tutorial.</span></span>
* <span data-ttu-id="ebfb1-138">Pour les paramètres supplémentaires, vérifiez que le type de disque hello est « Standard » et accepter que tous les hello des valeurs par défaut restantes.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-138">For additional settings, ensure hello disk type is "Standard" and accept all hello remaining defaults.</span></span>
* <span data-ttu-id="ebfb1-139">Déclencher la création d’hello sur la page de résumé hello.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-139">Kick off hello creation on hello summary page.</span></span>

<span data-ttu-id="ebfb1-140">Effectuer hello ci-dessus traiter deux fois toocreate deux Linux virtuels, un pour hello web frontal et un pour l’instance de MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-140">Perform hello above process twice toocreate two Linux virtual machines, one for hello web frontend and one for hello MongoDB instance.</span></span> <span data-ttu-id="ebfb1-141">La création d’ordinateurs virtuels hello prendra environ 5 à 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-141">Creation of hello virtual machines will take about 5-10 minutes.</span></span>

### <a name="assigning-a-dns-entry-for-virtual-machines"></a><span data-ttu-id="ebfb1-142">Affectation d’une entrée DNS pour les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="ebfb1-142">Assigning a DNS entry for Virtual Machines</span></span>
<span data-ttu-id="ebfb1-143">Les machines virtuelles créées dans Azure sont par défaut uniquement accessibles par le biais d’une adresse IP publique comme 1.2.3.4.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-143">Virtual machines created in Azure are by default only accessible through a public IP address like 1.2.3.4.</span></span> <span data-ttu-id="ebfb1-144">Assurons-nous machines de hello plus facilement identifiables en leur attribuant des entrées DNS.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-144">Let's make hello machines more easily identifiable by assigning them DNS entries.</span></span>

<span data-ttu-id="ebfb1-145">Une fois que le portail de hello indique que les machines virtuelles de hello ont été créés, cliquez sur lien des « Ordinateurs virtuels » hello dans la barre de navigation gauche hello et localiser vos ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-145">Once hello portal indicates that hello virtual machines have been created, click on hello "Virtual machines" link in hello left navbar and locate your machines.</span></span> <span data-ttu-id="ebfb1-146">Pour chaque machine :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-146">For each machine:</span></span>

* <span data-ttu-id="ebfb1-147">Recherchez l’onglet d’Essentials hello et cliquez sur hello les adresse IP publique ;</span><span class="sxs-lookup"><span data-stu-id="ebfb1-147">Locate hello Essentials tab and click on hello Public IP Address;</span></span>
* <span data-ttu-id="ebfb1-148">Dans la configuration d’adresse IP publique hello, affecter une étiquette de nom DNS et d’enregistrer.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-148">In hello public IP address configuration, assign a DNS name label and save.</span></span>

<span data-ttu-id="ebfb1-149">portail de Hello garantit que vous spécifiez le nom hello est disponible.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-149">hello portal will ensure that hello name you specify is available.</span></span> <span data-ttu-id="ebfb1-150">Après avoir enregistré la configuration de hello, vos ordinateurs virtuels auront des noms d’hôtes similaire trop`machinename.region.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-150">After saving hello configuration, your virtual machines will have host names similar too`machinename.region.cloudapp.azure.com`.</span></span>

### <a name="connecting-toohello-virtual-machines"></a><span data-ttu-id="ebfb1-151">Connexion toohello Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="ebfb1-151">Connecting toohello Virtual Machines</span></span>
<span data-ttu-id="ebfb1-152">Lorsque vos machines virtuelles ont été configurés, ils ont été préconfigurés tooallow des connexions à distance via SSH.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-152">When your virtual machines were provisioned, they were pre-configured tooallow remote connections over SSH.</span></span> <span data-ttu-id="ebfb1-153">Il s’agit de mécanisme hello nous allons utiliser des machines virtuelles de hello tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-153">This is hello mechanism we will use tooconfigure hello virtual machines.</span></span> <span data-ttu-id="ebfb1-154">Si vous utilisez des fenêtres pour votre développement, vous devez tooget un client SSH si vous n’en avez pas déjà.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-154">If you are using Windows for your development, you will need tooget an SSH client if you do not already have one.</span></span> <span data-ttu-id="ebfb1-155">Il est courant de choisir PuTTY, téléchargeable à partir d’ [ici](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span><span class="sxs-lookup"><span data-stu-id="ebfb1-155">A common choice here is PuTTY, which can be downloaded from [here](http://www.chiark.greenend.org.uk/~sgtatham/putty/).</span></span> <span data-ttu-id="ebfb1-156">Les systèmes d’exploitation Macintosh et Linux sont fournis avec une version du protocole SSH préinstallée.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-156">Macintosh and Linux OSes come with a version of SSH pre-installed.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="ebfb1-157">Configuration hello Machine virtuelle de serveur frontal Web</span><span class="sxs-lookup"><span data-stu-id="ebfb1-157">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="ebfb1-158">Ordinateur de serveur frontal web SSH toohello que vous avez créé à l’aide de PuTTY, ssh ligne de commande ou votre outil SSH autres préféré.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-158">SSH toohello web frontend machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="ebfb1-159">S’affiche alors un message de bienvenue, suivi d’une invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-159">You should see a welcome message followed by a command prompt.</span></span>

<span data-ttu-id="ebfb1-160">Tout d’abord, vérifiez que git est installé ainsi que le nœud :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-160">First, let's make sure that git and node are both installed:</span></span>

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

<span data-ttu-id="ebfb1-161">Serveur frontal web de l’application hello repose sur certains modules Node.js natifs, nous devons également ensemble essentiel de hello tooinstall des outils de génération :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-161">Since hello application's web frontend relies on some native Node.js modules, we also need tooinstall hello essential set of build tools:</span></span>

    sudo apt-get install -y build-essential

<span data-ttu-id="ebfb1-162">Enfin, nous allons de l’installation d’une application Node.js appelée *indéfiniment*, ce qui contribue à toorun Node.js serveur d’applications :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-162">Finally, let's install a Node.js application called *forever*, which helps toorun Node.js server applications:</span></span>

    sudo npm install -g forever

<span data-ttu-id="ebfb1-163">Il s’agit de toutes les dépendances de hello nécessaires sur le serveur frontal de cette machine virtuelle toobe toorun en mesure de hello l’application web, nous allons donc obtenir cette exécution.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-163">These are all hello dependencies needed on this virtual machine toobe able toorun hello application's web frontend, so let's get that running.</span></span> <span data-ttu-id="ebfb1-164">toodo, nous allons créer tout d’abord un clone bare du référentiel GitHub de hello vous dupliquée précédemment afin que vous pouvez facilement publier des mises à jour toohello virtual machine (nous aborderons ce scénario de mise à jour plus tard) et puis cloner hello bare clone tooprovide une version de hello espace de stockage qui permettre être exécutée.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-164">toodo this, we will first create a bare clone of hello GitHub repository you previously forked so that you can easily publish updates toohello virtual machine (we'll cover this update scenario later), and then clone hello bare clone tooprovide a version of hello repository that can actually be executed.</span></span>

<span data-ttu-id="ebfb1-165">Démarrer à partir du répertoire de base (~) hello, exécutez hello suivant les commandes (en remplaçant *accountname* avec votre nom de compte d’utilisateur GitHub) :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-165">Starting from hello home (~) directory, run hello following commands (replacing *accountname* with your GitHub user account name):</span></span>

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

<span data-ttu-id="ebfb1-166">Maintenant, entrez le répertoire de nœud-todo hello et exécuter ces commandes :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-166">Now enter hello node-todo directory and run these commands:</span></span>

    npm install
    forever start server.js

<span data-ttu-id="ebfb1-167">Hello serveur frontal de l’application web est en cours d’exécution, toutefois, il existe une étape supplémentaire avant que vous pouvez accéder à application hello depuis un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-167">hello application's web frontend is now running, however there is one more step before you can access hello application from a web browser.</span></span> <span data-ttu-id="ebfb1-168">machine virtuelle que vous avez créé Hello est protégé par une ressource Azure appelée un *groupe de sécurité réseau*, lequel a été créée pour vous lorsque vous avez approvisionné hello d’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-168">hello virtual machine you created is protected by an Azure resource called a *network security group*, which was created for you when you provisioned hello virtual machine.</span></span> <span data-ttu-id="ebfb1-169">Actuellement, cette ressource autorise uniquement les demandes externes tooport toobe 22 routé toohello machine virtuelle, ce qui permet la communication SSH avec l’ordinateur de hello, mais rien d’autre.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-169">Currently, this resource only allows external requests tooport 22 toobe routed toohello virtual machine, which enables SSH communication with hello machine but nothing else.</span></span> <span data-ttu-id="ebfb1-170">Par conséquent, Bonjour de tooview commande application TODO, qui est configuré toorun sur le port 8080, ce port doit également toobe ouvert.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-170">So in order tooview hello TODO application, which is configured toorun on port 8080, this port also needs toobe opened up.</span></span>

<span data-ttu-id="ebfb1-171">Retour toohello portail Azure et hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-171">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="ebfb1-172">Cliquez sur « Groupes de ressources » dans la barre de navigation gauche hello ;</span><span class="sxs-lookup"><span data-stu-id="ebfb1-172">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="ebfb1-173">Sélectionnez groupe de ressources hello qui contient votre machine virtuelle ;</span><span class="sxs-lookup"><span data-stu-id="ebfb1-173">Select hello resource group that contains your virtual machine;</span></span>
* <span data-ttu-id="ebfb1-174">Dans hello obtenu la liste des ressources, sélectionnez le groupe de sécurité réseau hello (hello une par une icône de bouclier) ;</span><span class="sxs-lookup"><span data-stu-id="ebfb1-174">In hello resulting list of resources, select hello network security group (hello one with a shield icon);</span></span>
* <span data-ttu-id="ebfb1-175">Dans les propriétés de hello, choisissez « règles de sécurité de trafic entrant » ;</span><span class="sxs-lookup"><span data-stu-id="ebfb1-175">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="ebfb1-176">Dans la barre d’outils de hello, cliquez sur « Ajouter » ;</span><span class="sxs-lookup"><span data-stu-id="ebfb1-176">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="ebfb1-177">Fournissez un nom comme default-allow-todo.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-177">Provide a name like "default-allow-todo";</span></span>
* <span data-ttu-id="ebfb1-178">Définir le protocole de hello trop « TCP » ;</span><span class="sxs-lookup"><span data-stu-id="ebfb1-178">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="ebfb1-179">Définir la plage de ports de destination hello trop « 8080 ; »</span><span class="sxs-lookup"><span data-stu-id="ebfb1-179">Set hello destination port range too"8080";</span></span>
* <span data-ttu-id="ebfb1-180">Cliquez sur OK et attendre toobe de règle de sécurité hello créé.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-180">Click OK and wait for hello security rule toobe created.</span></span>

<span data-ttu-id="ebfb1-181">Après avoir créé cette règle de sécurité, hello application de tâches est visible publiquement sur internet de hello et vous pouvez parcourir tooit, par exemple en utilisant une URL comme :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-181">After creating this security rule, hello TODO application is publically visible on hello internet and you can browse tooit, for instance using a URL such as:</span></span>

    http://machinename.region.cloudapp.azure.com:8080

<span data-ttu-id="ebfb1-182">Vous remarquerez que, bien que nous n’avons pas encore configuré la machine virtuelle de MongoDB hello, hello les application TODO apparaît toobe très fonctionnelle.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-182">You will notice that even though we have not yet configured hello MongoDB virtual machine, hello TODO application appears toobe quite functional.</span></span> <span data-ttu-id="ebfb1-183">Il s’agit, car le référentiel de code source hello est codé en dur toouse une instance MongoDB déjà déployée.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-183">This is because hello source repository is hardcoded toouse a pre-deployed MongoDB instance.</span></span> <span data-ttu-id="ebfb1-184">Une fois que nous avons configuré la machine virtuelle de MongoDB hello, nous revenir en arrière et modifier, tooutilize de code source hello notre instance MongoDB privée à la place.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-184">Once we have configured hello MongoDB virtual machine, we will go back and change hello source code tooutilize our private MongoDB instance instead.</span></span>

### <a name="configuring-hello-mongodb-virtual-machine"></a><span data-ttu-id="ebfb1-185">Configuration hello MongoDB Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="ebfb1-185">Configuring hello MongoDB Virtual Machine</span></span>
<span data-ttu-id="ebfb1-186">SSH toohello deuxième ordinateur que vous avez créé à l’aide de PuTTY, ssh ligne de commande ou votre outil SSH autres préféré.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-186">SSH toohello second machine you created using PuTTY, ssh command line or your other favorite SSH tool.</span></span> <span data-ttu-id="ebfb1-187">Lorsque vous voyez le message d’accueil hello et l’invite de commandes, installez MongoDB (ces instructions ont été effectuées à partir de [ici](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)) :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-187">After seeing hello welcome message and command prompt, install MongoDB (these instructions were taken from [here](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)):</span></span>

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

<span data-ttu-id="ebfb1-188">Par défaut, MongoDB est configuré pour être uniquement accessible localement.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-188">By default, MongoDB is configured so it can only be accessed locally.</span></span> <span data-ttu-id="ebfb1-189">Pour ce didacticiel, nous allons configurer MongoDB afin qu’il est accessible à partir de l’ordinateur virtuel de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-189">For this tutorial, we will configure MongoDB so it can be accessed from hello application's virtual machine.</span></span> <span data-ttu-id="ebfb1-190">Dans un contexte sudo, ouvrir le fichier de /etc/mongod.conf hello et localiser hello `# network interfaces` section.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-190">In a sudo context, open hello /etc/mongod.conf file and locate hello `# network interfaces` section.</span></span> <span data-ttu-id="ebfb1-191">Hello de modification `net.bindIp` configuration valeur trop`0.0.0.0`.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-191">Change hello `net.bindIp` configuration value too`0.0.0.0`.</span></span>

> [!NOTE]
> <span data-ttu-id="ebfb1-192">Cette configuration s’applique à des fins de hello de ce didacticiel uniquement.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-192">This configuration is for hello purposes of this tutorial only.</span></span> <span data-ttu-id="ebfb1-193">Il ne s’agit **pas** d’une pratique de sécurité recommandée et elle ne doit pas être utilisée dans les environnements de production.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-193">It is **NOT** a recommended security practice and should not be used in production environments.</span></span>
> 
> 

<span data-ttu-id="ebfb1-194">Maintenant, vérifiez que hello MongoDB service a été démarré :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-194">Now ensure hello MongoDB service has been started:</span></span>

    sudo service mongod restart

<span data-ttu-id="ebfb1-195">MongoDB fonctionne sur le port 27017 par défaut.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-195">MongoDB operates over port 27017 by default.</span></span> <span data-ttu-id="ebfb1-196">Par conséquent, Bonjour même façon qu’il est nécessaire de tooopen le port 8080 sur la machine virtuelle de hello web frontal, nous devons tooopen port 27017 sur l’ordinateur virtuel de MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-196">So, in hello same way that we needed tooopen port 8080 on hello web frontend virtual machine, we need tooopen port 27017 on hello MongoDB virtual machine.</span></span>

<span data-ttu-id="ebfb1-197">Retour toohello portail Azure et hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-197">Return toohello Azure Portal and complete hello following steps:</span></span>

* <span data-ttu-id="ebfb1-198">Cliquez sur « Groupes de ressources » dans la barre de navigation gauche hello ;</span><span class="sxs-lookup"><span data-stu-id="ebfb1-198">Click on "Resource groups" in hello left navbar;</span></span>
* <span data-ttu-id="ebfb1-199">Sélectionnez groupe de ressources hello qui contient l’ordinateur virtuel de MongoDB hello ;</span><span class="sxs-lookup"><span data-stu-id="ebfb1-199">Select hello resource group that contains hello MongoDB virtual machine;</span></span>
* <span data-ttu-id="ebfb1-200">Dans hello obtenu la liste des ressources, sélectionnez groupe de sécurité réseau hello (hello une par une icône de bouclier) avec hello que même nom que celui que vous avez donné de machine virtuelle de MongoDB toohello ;</span><span class="sxs-lookup"><span data-stu-id="ebfb1-200">In hello resulting list of resources, select hello network security group (hello one with a shield icon) with hello same name that you gave toohello MongoDB virtual machine;</span></span>
* <span data-ttu-id="ebfb1-201">Dans les propriétés de hello, choisissez « règles de sécurité de trafic entrant » ;</span><span class="sxs-lookup"><span data-stu-id="ebfb1-201">In hello properties, choose "Inbound security rules";</span></span>
* <span data-ttu-id="ebfb1-202">Dans la barre d’outils de hello, cliquez sur « Ajouter » ;</span><span class="sxs-lookup"><span data-stu-id="ebfb1-202">In hello toolbar, click "Add";</span></span>
* <span data-ttu-id="ebfb1-203">Fournissez un nom comme default-allow-mongo.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-203">Provide a name like "default-allow-mongo";</span></span>
* <span data-ttu-id="ebfb1-204">Définir le protocole de hello trop « TCP » ;</span><span class="sxs-lookup"><span data-stu-id="ebfb1-204">Set hello protocol too"TCP";</span></span>
* <span data-ttu-id="ebfb1-205">Définir la plage de ports de destination hello trop « 27017 » ;</span><span class="sxs-lookup"><span data-stu-id="ebfb1-205">Set hello destination port range too"27017";</span></span>
* <span data-ttu-id="ebfb1-206">Cliquez sur OK et attendre toobe de règle de sécurité hello créé.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-206">Click OK and wait for hello security rule toobe created.</span></span>

## <a name="iterating-on-hello-todo-application"></a><span data-ttu-id="ebfb1-207">Itération sur hello application de TODO</span><span class="sxs-lookup"><span data-stu-id="ebfb1-207">Iterating on hello TODO application</span></span>
<span data-ttu-id="ebfb1-208">Jusqu'à présent, nous avons mis en service les ordinateurs virtuels Linux deux : celui qui exécute l’application hello serveur web frontal et l’autre qui exécute une instance de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-208">So far, we have provisioned two Linux virtual machines: one that is running hello application's web frontend and one that is running a MongoDB instance.</span></span> <span data-ttu-id="ebfb1-209">Mais il existe un problème : hello web frontal n’est pas utilise encore hello configuré MongoDB instance.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-209">But there is a problem - hello web frontend isn't actually using hello provisioned MongoDB instance yet.</span></span> <span data-ttu-id="ebfb1-210">Nous allons résoudre cela en mettant à jour hello web frontal code toouse une variable d’environnement au lieu d’une instance codé en dur.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-210">Let's fix that by updating hello web frontend code toouse an environment variable instead of a hard-coded instance.</span></span>

### <a name="changing-hello-todo-application"></a><span data-ttu-id="ebfb1-211">La modification d’application de hello TODO</span><span class="sxs-lookup"><span data-stu-id="ebfb1-211">Changing hello TODO application</span></span>
<span data-ttu-id="ebfb1-212">Sur votre ordinateur de développement où vous avez cloné tout d’abord référentiel de nœud-todo hello, ouvrez hello `node-todo/config/database.js` dans votre éditeur favori et modifiez la valeur de codée en dur de hello comme valeur de l’url hello `mongodb://...` trop`process.env.MONGODB`.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-212">On your development machine where you first cloned hello node-todo repository, open hello `node-todo/config/database.js` file in your favorite editor and change hello url value from hello hard-coded value like `mongodb://...` too`process.env.MONGODB`.</span></span>

<span data-ttu-id="ebfb1-213">Valider vos modifications et push toohello GitHub master :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-213">Commit your changes and push toohello GitHub master:</span></span>

    git commit -am "Get MongoDB instance from env"
    git push origin master

<span data-ttu-id="ebfb1-214">Malheureusement, cela ne publie pas machine virtuelle de hello modification toohello web frontal.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-214">Unfortunately, this doesn't publish hello change toohello web frontend virtual machine.</span></span> <span data-ttu-id="ebfb1-215">Apportons quelques tooenable de machine virtuelle de toothat de modifications plus un mécanisme simple mais efficace pour la publication des mises à jour afin de pouvoir observer rapidement effet hello de modifications hello dans l’environnement d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-215">Let's make a few more changes toothat virtual machine tooenable a simple but effective mechanism for publishing updates so you can quickly observe hello effect of hello changes in hello live environment.</span></span>

### <a name="configuring-hello-web-frontend-virtual-machine"></a><span data-ttu-id="ebfb1-216">Configuration hello Machine virtuelle de serveur frontal Web</span><span class="sxs-lookup"><span data-stu-id="ebfb1-216">Configuring hello Web Frontend Virtual Machine</span></span>
<span data-ttu-id="ebfb1-217">Rappelez-vous que nous avons créé un clone bare du référentiel de nœud-todo hello précédemment sur l’ordinateur virtuel de hello web frontal.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-217">Recall that we previously created a bare clone of hello node-todo repository on hello web frontend virtual machine.</span></span> <span data-ttu-id="ebfb1-218">Il s’avère que cette action créé un nouveau Git distant toowhich modifications peuvent être appliquées.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-218">It turns out that this action created a new Git remote toowhich changes can be pushed.</span></span> <span data-ttu-id="ebfb1-219">Toutefois, simplement en exécutant un push toothis à distance ne donne assez de modèle d’itération rapide hello que les développeurs cherchez lorsque vous travaillez sur leur code.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-219">However, simply pushing toothis remote doesn't quite give hello rapid iteration model that developers are looking for when working on their code.</span></span>

<span data-ttu-id="ebfb1-220">Ce que nous veut toodo en mesure de toobe est Vérifiez qu’en cas d’un référentiel distant de toohello par émission de données sur l’ordinateur virtuel de hello, application de tâches en cours d’exécution hello est automatiquement mis à jour.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-220">What we would like toobe able toodo is ensure that when a push toohello remote repository on hello virtual machine occurs, hello running TODO application is automatically updated.</span></span> <span data-ttu-id="ebfb1-221">Heureusement, il s’agit de tooachieve facile avec git.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-221">Fortunately, this is easy tooachieve with git.</span></span>

<span data-ttu-id="ebfb1-222">GIT expose un nombre de connexions qui sont appelés à des moments tooreact tooactions est effectuées sur le référentiel de hello.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-222">Git exposes a number of hooks that are called at particular times tooreact tooactions taken on hello repository.</span></span> <span data-ttu-id="ebfb1-223">Elles sont spécifiées à l’aide de scripts de shell du référentiel hello `hooks` dossier.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-223">These are specified using shell scripts in hello repository's `hooks` folder.</span></span> <span data-ttu-id="ebfb1-224">raccordement de Hello n’est plus applicable pour le scénario de mise à jour automatique hello est hello `post-update` événement.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-224">hello hook that is most applicable for hello auto-update scenario is hello `post-update` event.</span></span>

<span data-ttu-id="ebfb1-225">Dans une machine virtuelle SSH session toohello web frontal, modifiez toohello `~/node-todo.git/hooks` répertoire et ajoutez hello tooa contenu nommé le fichier suivant `post-update` (en remplaçant `machinename` et `region` avec vos informations d’ordinateur virtuel MongoDB) :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-225">In a SSH session toohello web frontend virtual machine, change toohello `~/node-todo.git/hooks` directory and add hello following content tooa file named `post-update` (replacing `machinename` and `region` with your MongoDB virtual machine information):</span></span>

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

<span data-ttu-id="ebfb1-226">Vérifiez que ce fichier est exécutable en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-226">Ensure this file is executable by running hello following command:</span></span>

    chmod 755 post-update

<span data-ttu-id="ebfb1-227">Ce script vérifie qu’application serveur en cours de hello est arrêtée, code hello dans le référentiel cloné de hello est toohello mis à jour plus récentes, toutes les dépendances de mise à jour sont satisfaites, et hello serveur est redémarré.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-227">This script ensures that hello current server application is stopped, hello code in hello cloned repository is updated toohello latest, any updated dependencies are satisfied, and hello server is restarted.</span></span> <span data-ttu-id="ebfb1-228">Cela garantit également que cet environnement hello a été configuré en vue de la réception de notre première mise à jour tooget hello MongoDB instance de l’application à partir d’une variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-228">It also ensures that hello environment has been configured in preparation for receiving our first application update tooget hello MongoDB instance from an environment variable.</span></span>

### <a name="configuring-your-development-machine"></a><span data-ttu-id="ebfb1-229">Configuration de votre machine de développement</span><span class="sxs-lookup"><span data-stu-id="ebfb1-229">Configuring your Development Machine</span></span>
<span data-ttu-id="ebfb1-230">Maintenant nous allons obtenir votre ordinateur de développement raccordée d’ordinateur virtuel de toohello web frontal.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-230">Now let's get your development machine hooked up toohello web frontend virtual machine.</span></span> <span data-ttu-id="ebfb1-231">Il s’agit aussi simple que l’ajout de référentiel de bare hello sur l’ordinateur virtuel de hello un distant.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-231">This is as simple as adding hello bare repository on hello virtual machine as a remote.</span></span> <span data-ttu-id="ebfb1-232">Exécuter cet exemple hello suivant toodo de commande (en remplaçant *utilisateur* avec votre nom de connexion de machine virtuelle de serveur frontal web et *machinename* et *région* le cas échéant) :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-232">Run hello following command toodo this (replacing *user* with your web frontend virtual machine login name and *machinename* and *region* as appropriate):</span></span>

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

<span data-ttu-id="ebfb1-233">C’est tout en exécutant un push tooenable nécessaire ou la publication en vigueur, modifie l’ordinateur virtuel de toohello web frontal.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-233">This is all that is needed tooenable pushing, or in effect publishing, changes toohello web frontend virtual machine.</span></span>

### <a name="publishing-updates"></a><span data-ttu-id="ebfb1-234">Publication des mises à jour</span><span class="sxs-lookup"><span data-stu-id="ebfb1-234">Publishing Updates</span></span>
<span data-ttu-id="ebfb1-235">Nous allons publier hello une modification qui a été effectuée jusqu'à présent afin que l’application hello utilisera sa propre instance MongoDB :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-235">Let's publish hello one change that has been made so far so that hello application will use our own MongoDB instance:</span></span>

    git push azure master

<span data-ttu-id="ebfb1-236">Vous devez voir toothis similaire de sortie :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-236">You should see output similar toothis:</span></span>

    Counting objects: 4, done.
    Delta compression using up too4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 406 bytes | 0 bytes/s, done.
    Total 4 (delta 1), reused 0 (delta 0)
    remote: info:    Forever stopped processes:
    remote: data:        uid  command         script    forever pid  id logfile                         uptime
    remote: data:    [0] 0Lyh /usr/bin/nodejs server.js 9064    9301    /home/username/.forever/0Lyh.log 0:0:3:17.487
    remote: From /home/username/node-todo
    remote:    5f31fd7..5bc7be5  master     -> origin/master
    remote: From /home/username/node-todo
    remote:  * branch            master     -> FETCH_HEAD
    remote: Updating 5f31fd7..5bc7be5
    remote: Fast-forward
    remote:  config/database.js | 2 +-
    remote:  1 file changed, 1 insertion(+), 1 deletion(-)
    remote: npm WARN package.json node-todo@0.0.0 No repository field.
    remote: npm WARN package.json node-todo@0.0.0 No license field.
    remote: warn:    --minUptime not set. Defaulting to: 1000ms
    remote: warn:    --spinSleepTime not set. Your script will exit if it does not stay up for at least 1000ms
    remote: info:    Forever processing file: /home/username/node-todo/server.js
    toousername@machinename.region.cloudapp.azure.com:node-todo.git
    5f31fd7..5bc7be5  master -> master

<span data-ttu-id="ebfb1-237">Une fois cette commande terminée, essayez d’actualiser l’application hello dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-237">After this command completes, try refreshing hello application in a web browser.</span></span> <span data-ttu-id="ebfb1-238">Vous devez être en mesure de toosee que liste de tâches hello présentée ici est vide et n’est plus liée toohello partagé déployé MongoDB instance.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-238">You should be able toosee that hello TODO list presented here is empty and no longer tied toohello shared deployed MongoDB instance.</span></span>

<span data-ttu-id="ebfb1-239">didacticiel de hello toocomplete, nous allons modifier un autre, plus visible.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-239">toocomplete hello tutorial, let's make another, more visible change.</span></span> <span data-ttu-id="ebfb1-240">Sur votre ordinateur de développement, ouvrez le fichier de node-todo/public/index.html de hello à l’aide de votre éditeur favori.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-240">On your development machine, open hello node-todo/public/index.html file using your favorite editor.</span></span> <span data-ttu-id="ebfb1-241">Localiser l’en-tête de jumbotron hello et modifier le titre hello à partir de « Je suis un Todo-aholic » trop « je ne suis un Todo-aholic sur Azure ! ».</span><span class="sxs-lookup"><span data-stu-id="ebfb1-241">Locate hello jumbotron header and change  hello title from "I'm a Todo-aholic" too"I'm a Todo-aholic on Azure!".</span></span>

<span data-ttu-id="ebfb1-242">Maintenant procédons à la validation :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-242">Now let's commit:</span></span>

    git commit -am "Azurify hello title"

<span data-ttu-id="ebfb1-243">Cette fois, nous allons publier hello modification tooAzure avant d’en exécutant un push du référentiel GitHub tooback toohello :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-243">This time, let's publish hello change tooAzure before pushing it tooback toohello GitHub repo:</span></span>

    git push azure master

<span data-ttu-id="ebfb1-244">Une fois cette commande exécutée, l’actualisation hello web page et vous modifications seront visibles hello.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-244">Once this command completes, refresh hello web page and you will see hello changes.</span></span> <span data-ttu-id="ebfb1-245">Dans la mesure où elles apparaîtront correctement, push hello modification toohello arrière origine distant :</span><span class="sxs-lookup"><span data-stu-id="ebfb1-245">Since they look good, push hello change back toohello origin remote:</span></span> 

    git push origin master

## <a name="next-steps"></a><span data-ttu-id="ebfb1-246">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ebfb1-246">Next Steps</span></span>
<span data-ttu-id="ebfb1-247">Cet article a montré comment tootake une application Node.js et déployer des machines virtuelles de tooLinux s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="ebfb1-247">This article showed how tootake a Node.js application and deploy it tooLinux virtual machines running in Azure.</span></span> <span data-ttu-id="ebfb1-248">toolearn en savoir plus sur les ordinateurs virtuels Linux dans Azure, consultez [tooLinux Introduction sur Azure](/documentation/articles/virtual-machines-linux-introduction/).</span><span class="sxs-lookup"><span data-stu-id="ebfb1-248">toolearn more about Linux virtual machines in Azure, see [Introduction tooLinux on Azure](/documentation/articles/virtual-machines-linux-introduction/).</span></span>

<span data-ttu-id="ebfb1-249">Pour plus d’informations sur les applications Node.js toodevelop sur Azure, consultez hello [centre de développement Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="ebfb1-249">For more information about how toodevelop Node.js applications on Azure, see hello [Node.js Developer Center](/develop/nodejs/).</span></span>

