---
title: aaaHost Ruby sur le site Web de Rails sur un VM Linux | Documents Microsoft
description: "Configuration et hébergement d'un Ruby sur le site web de Rails dans Azure en utilisant une machine virtuelle Linux."
services: virtual-machines-linux
documentationcenter: ruby
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: aad32685-3550-4bff-9c73-beb8d70b3291
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: ruby
ms.topic: article
ms.date: 06/27/2017
ms.author: robmcm
ms.openlocfilehash: c545c24fc6c89497854bbe55a6d0d1d0b072c386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a><span data-ttu-id="c89bc-103">Application Web Ruby on Rails sur une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="c89bc-103">Ruby on Rails Web application on an Azure VM</span></span>
<span data-ttu-id="c89bc-104">Ce didacticiel montre comment toohost Ruby sur le site Web de Rails sur Azure à l’aide d’une machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="c89bc-104">This tutorial shows how toohost a Ruby on Rails website on Azure using a Linux virtual machine.</span></span>  

<span data-ttu-id="c89bc-105">Ce didacticiel a été validé à l’aide d’Ubuntu Server 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="c89bc-105">This tutorial was validated using Ubuntu Server 14.04 LTS.</span></span> <span data-ttu-id="c89bc-106">Si vous utilisez une autre distribution Linux, vous devrez peut-être toomodify hello étapes tooinstall Rails.</span><span class="sxs-lookup"><span data-stu-id="c89bc-106">If you use a different Linux distribution, you might need toomodify hello steps tooinstall Rails.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c89bc-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c89bc-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="c89bc-108">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="c89bc-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="c89bc-109">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="c89bc-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
>
>

## <a name="create-an-azure-vm"></a><span data-ttu-id="c89bc-110">Création d’une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="c89bc-110">Create an Azure VM</span></span>
<span data-ttu-id="c89bc-111">Commencez par créer une machine virtuelle Azure avec une image Linux.</span><span class="sxs-lookup"><span data-stu-id="c89bc-111">Start by creating an Azure VM with a Linux image.</span></span>

<span data-ttu-id="c89bc-112">toocreate hello de machine virtuelle, vous pouvez utiliser hello portail Azure ou hello Azure Interface de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="c89bc-112">toocreate hello VM, you can use hello Azure portal or hello Azure Command-Line Interface (CLI).</span></span>

### <a name="azure-portal"></a><span data-ttu-id="c89bc-113">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="c89bc-113">Azure portal</span></span>
1. <span data-ttu-id="c89bc-114">L’authentification à hello [portail Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="c89bc-114">Sign into hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="c89bc-115">Cliquez sur **nouveau**, puis tapez « Ubuntu Server 14.04 » dans la zone de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="c89bc-115">Click **New**, then type "Ubuntu Server 14.04" in hello search box.</span></span> <span data-ttu-id="c89bc-116">Cliquez sur entrée hello retournée par la recherche de hello.</span><span class="sxs-lookup"><span data-stu-id="c89bc-116">Click hello entry returned by hello search.</span></span> <span data-ttu-id="c89bc-117">Pour le modèle de déploiement hello, sélectionnez **classique**, puis cliquez sur « Créer ».</span><span class="sxs-lookup"><span data-stu-id="c89bc-117">For hello deployment model, select **Classic**, then click "Create".</span></span>
3. <span data-ttu-id="c89bc-118">Dans le panneau des principes de base hello, fournir des valeurs pour les champs hello requis : nom (pour hello machine virtuelle), nom d’utilisateur, type d’authentification et les informations d’identification correspondantes hello, abonnement Azure, groupe de ressources et l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="c89bc-118">In hello Basics blade, supply values for hello required fields: Name (for hello VM), User name, Authentication type and hello corresponding credentials, Azure subscription, Resource group, and Location.</span></span>

   ![Create a new Ubuntu Image](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. <span data-ttu-id="c89bc-120">Après la configuration de machine virtuelle de hello, cliquez sur le nom d’ordinateur virtuel hello, puis cliquez sur **points de terminaison** Bonjour **paramètres** catégorie.</span><span class="sxs-lookup"><span data-stu-id="c89bc-120">After hello VM is provisioned, click on hello VM name, and click **Endpoints** in hello **Settings** category.</span></span> <span data-ttu-id="c89bc-121">Trouver le point de terminaison hello SSH, répertorié sous **autonome**.</span><span class="sxs-lookup"><span data-stu-id="c89bc-121">Find hello SSH endpoint, listed under **Standalone**.</span></span>

   ![Point de terminaison par défaut.](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a><span data-ttu-id="c89bc-123">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="c89bc-123">Azure CLI</span></span>
<span data-ttu-id="c89bc-124">Suivez les étapes de hello dans [créer une Machine virtuelle exécutant Linux][vm-instructions].</span><span class="sxs-lookup"><span data-stu-id="c89bc-124">Follow hello steps in [Create a Virtual Machine Running Linux][vm-instructions].</span></span>

<span data-ttu-id="c89bc-125">Après la configuration de machine virtuelle de hello, vous pouvez obtenir le point de terminaison SSH hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c89bc-125">After hello VM is provisioned, you can get hello SSH endpoint by running hello following command:</span></span>

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a><span data-ttu-id="c89bc-126">installation de Ruby sur Rails</span><span class="sxs-lookup"><span data-stu-id="c89bc-126">Install Ruby on Rails</span></span>
1. <span data-ttu-id="c89bc-127">Utiliser SSH tooconnect toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c89bc-127">Use SSH tooconnect toohello VM.</span></span>
2. <span data-ttu-id="c89bc-128">À partir de la session SSH hello, utilisez hello suivant de commandes tooinstall Ruby de hello machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="c89bc-128">From hello SSH session, use hello following commands tooinstall Ruby on hello VM:</span></span>

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    <span data-ttu-id="c89bc-129">installation de Hello peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="c89bc-129">hello installation may take a few minutes.</span></span> <span data-ttu-id="c89bc-130">Lorsqu’elle est terminée, utilisez hello suivant tooverify commande que Ruby est installé :</span><span class="sxs-lookup"><span data-stu-id="c89bc-130">When it completes, use hello following command tooverify that Ruby is installed:</span></span>

        ruby -v

3. <span data-ttu-id="c89bc-131">Suivant de hello utilisation de commandes de Rails de tooinstall :</span><span class="sxs-lookup"><span data-stu-id="c89bc-131">Use hello following command tooinstall Rails:</span></span>

        sudo gem install rails --no-rdoc --no-ri -V

    <span data-ttu-id="c89bc-132">Utilisez hello--non-rdoc et--tooskip non-ri indicateurs installation de la documentation de hello, qui est plus rapide.</span><span class="sxs-lookup"><span data-stu-id="c89bc-132">Use hello --no-rdoc and --no-ri flags tooskip installing hello documentation, which is faster.</span></span>
    <span data-ttu-id="c89bc-133">Cette commande probablement prendra un certain temps tooexecute, afin de l’ajout de hello -V Affiche des informations sur la progression de l’installation hello.</span><span class="sxs-lookup"><span data-stu-id="c89bc-133">This command will likely take a long time tooexecute, so adding hello -V will display information about hello installation progress.</span></span>

## <a name="create-and-run-an-app"></a><span data-ttu-id="c89bc-134">Création et exécution d’une application</span><span class="sxs-lookup"><span data-stu-id="c89bc-134">Create and run an app</span></span>
<span data-ttu-id="c89bc-135">Toujours connecté via une connexion SSH, exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="c89bc-135">While still logged in via SSH, run hello following commands:</span></span>

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

<span data-ttu-id="c89bc-136">Hello [nouveau](http://guides.rubyonrails.org/command_line.html#rails-new) commande crée une nouvelle application de quadrillage.</span><span class="sxs-lookup"><span data-stu-id="c89bc-136">hello [new](http://guides.rubyonrails.org/command_line.html#rails-new) command creates a new Rails app.</span></span> <span data-ttu-id="c89bc-137">Hello [server](http://guides.rubyonrails.org/command_line.html#rails-server) commande démarre hello WEBrick au serveur web qui est fourni avec les Rails.</span><span class="sxs-lookup"><span data-stu-id="c89bc-137">hello [server](http://guides.rubyonrails.org/command_line.html#rails-server) command starts hello WEBrick web server that comes with Rails.</span></span> <span data-ttu-id="c89bc-138">(Pour la production, vous souhaiterez probablement toouse un autre serveur, telles que licorne ou passagers.)</span><span class="sxs-lookup"><span data-stu-id="c89bc-138">(For production use, you would probably want toouse a different server, such as Unicorn or Passenger.)</span></span>

<span data-ttu-id="c89bc-139">Vous devez voir s’afficher sortie similaire toohello.</span><span class="sxs-lookup"><span data-stu-id="c89bc-139">You should see output similar toohello following.</span></span>

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a><span data-ttu-id="c89bc-140">Ajout d’un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="c89bc-140">Add an endpoint</span></span>
1. <span data-ttu-id="c89bc-141">Accédez toohello [Azure portal] [https://portal.azure.com] et sélectionnez votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c89bc-141">Go toohello [Azure portal][https://portal.azure.com] and select your VM.</span></span>

2. <span data-ttu-id="c89bc-142">Sélectionnez **points de terminaison** Bonjour **paramètres** le long de la page de hello hello bord gauche.</span><span class="sxs-lookup"><span data-stu-id="c89bc-142">Select **ENDPOINTS** in hello **Settings** along hello left edge hello page.</span></span>

3. <span data-ttu-id="c89bc-143">Cliquez sur **ajouter** en hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="c89bc-143">Click **ADD** at hello top of hello page.</span></span>

4. <span data-ttu-id="c89bc-144">Bonjour **ajouter le point de terminaison** boîte de dialogue, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c89bc-144">In hello **Add endpoint** dialog page, enter hello following information:</span></span>

   * <span data-ttu-id="c89bc-145">**Nom** : HTTP</span><span class="sxs-lookup"><span data-stu-id="c89bc-145">**Name**: HTTP</span></span>
   * <span data-ttu-id="c89bc-146">**Protocole**: TCP</span><span class="sxs-lookup"><span data-stu-id="c89bc-146">**Protocol**: TCP</span></span>
   * <span data-ttu-id="c89bc-147">**Port public** : 80</span><span class="sxs-lookup"><span data-stu-id="c89bc-147">**Public port**: 80</span></span>
   * <span data-ttu-id="c89bc-148">**Port privé** : 3000</span><span class="sxs-lookup"><span data-stu-id="c89bc-148">**Private port**: 3000</span></span>
   * <span data-ttu-id="c89bc-149">**Adresse PI flottante** : Désactivée</span><span class="sxs-lookup"><span data-stu-id="c89bc-149">**Floating PI address**: Disabled</span></span>
   * <span data-ttu-id="c89bc-150">**Liste de contrôle d’accès - ordre**: 1001, ou une autre valeur qui définit la priorité de hello de cette règle d’accès.</span><span class="sxs-lookup"><span data-stu-id="c89bc-150">**Access control list - Order**: 1001, or another value that sets hello priority of this access rule.</span></span>
   * <span data-ttu-id="c89bc-151">**Liste de contrôle d’accès - nom** : allowHTTP</span><span class="sxs-lookup"><span data-stu-id="c89bc-151">**Access control list - Name**: allowHTTP</span></span>
   * <span data-ttu-id="c89bc-152">**Liste de contrôle d’accès - Action** : autoriser</span><span class="sxs-lookup"><span data-stu-id="c89bc-152">**Access control list - Action**: permit</span></span>
   * <span data-ttu-id="c89bc-153">**Liste de contrôle d’accès - sous-réseau distant** : 1.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="c89bc-153">**Access control list - Remote subnet**: 1.0.0.0/16</span></span>

     <span data-ttu-id="c89bc-154">Ce point de terminaison a un port public 80 qui achemine le trafic toohello port privé (3000), où hello Rails serveur écoute.</span><span class="sxs-lookup"><span data-stu-id="c89bc-154">This endpoint  has a public port of 80 that will route traffic toohello private port of 3000, where hello Rails server is listening.</span></span> <span data-ttu-id="c89bc-155">règle de liste de contrôle Hello accès permet de trafic public sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="c89bc-155">hello access control list rule allows public traffic on port 80.</span></span>

     ![new-endpoint](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. <span data-ttu-id="c89bc-157">Cliquez sur le point de terminaison toosave OK hello.</span><span class="sxs-lookup"><span data-stu-id="c89bc-157">Click OK toosave hello endpoint.</span></span>

6. <span data-ttu-id="c89bc-158">Un message doit apparaître indiquant **Enregistrement du point de terminaison de la machine virtuelle**.</span><span class="sxs-lookup"><span data-stu-id="c89bc-158">A message should appear that states **Saving virtual machine endpoint**.</span></span> <span data-ttu-id="c89bc-159">Une fois ce message disparaît, le point de terminaison hello est actif.</span><span class="sxs-lookup"><span data-stu-id="c89bc-159">Once this message disappears, hello endpoint is active.</span></span> <span data-ttu-id="c89bc-160">Vous pouvez maintenant tester votre application en parcourant le nom DNS de toohello de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c89bc-160">You may now test your application by navigating toohello DNS name of your virtual machine.</span></span> <span data-ttu-id="c89bc-161">site Web de Hello doit apparaître comme toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="c89bc-161">hello website should appear similar toohello following:</span></span>

    ![page rails par défaut][default-rails-cloud]

## <a name="next-steps"></a><span data-ttu-id="c89bc-163">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c89bc-163">Next steps</span></span>
<span data-ttu-id="c89bc-164">Dans ce didacticiel, vous avez effectué la plupart des étapes de hello manuellement.</span><span class="sxs-lookup"><span data-stu-id="c89bc-164">In this tutorial, you did most of hello steps manually.</span></span> <span data-ttu-id="c89bc-165">Dans un environnement de production, vous écrivez votre application sur un ordinateur de développement et déployez-le toohello machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="c89bc-165">In a production environment, you would write your app on a development machine and deploy it toohello Azure VM.</span></span> <span data-ttu-id="c89bc-166">En outre, la plupart des environnements de production hébergent application de quadrillage hello conjointement avec un autre processus serveur tels que Apache ou NginX, qui gère demande des instances de routage toomultiple d’application de quadrillage hello et servant de ressources statiques.</span><span class="sxs-lookup"><span data-stu-id="c89bc-166">Also, most production environments host hello Rails application in conjunction with another server process such as Apache or NginX, which handles request routing toomultiple instances of hello Rails application and serving static resources.</span></span> <span data-ttu-id="c89bc-167">Pour plus d’informations, consultez http://rubyonrails.org/deploy/.</span><span class="sxs-lookup"><span data-stu-id="c89bc-167">For more information, see http://rubyonrails.org/deploy/.</span></span>

<span data-ttu-id="c89bc-168">toolearn en savoir plus sur Ruby on Rails, visitez hello [Ruby sur les Rails Guides][rails-guides].</span><span class="sxs-lookup"><span data-stu-id="c89bc-168">toolearn more about Ruby on Rails, visit hello [Ruby on Rails Guides][rails-guides].</span></span>

<span data-ttu-id="c89bc-169">toouse des services Azure à partir de votre application Ruby, consultez :</span><span class="sxs-lookup"><span data-stu-id="c89bc-169">toouse Azure services from your Ruby application, see:</span></span>

* <span data-ttu-id="c89bc-170">[Utilisation du stockage d’objets blob à partir de Ruby][blobs]</span><span class="sxs-lookup"><span data-stu-id="c89bc-170">[Store unstructured data using blobs][blobs]</span></span>
* <span data-ttu-id="c89bc-171">[Utilisation du stockage de tables à partir de Ruby][tables]</span><span class="sxs-lookup"><span data-stu-id="c89bc-171">[Store key/value pairs using tables][tables]</span></span>
* <span data-ttu-id="c89bc-172">[Traiter du contenu de la bande passante élevée avec hello Content Delivery Network][cdn-howto]</span><span class="sxs-lookup"><span data-stu-id="c89bc-172">[Serve high bandwidth content with hello Content Delivery Network][cdn-howto]</span></span>

<!-- WA.com links -->
[blobs]:../../../storage/blobs/storage-ruby-how-to-use-blob-storage.md
[cdn-howto]:https://azure.microsoft.com/develop/ruby/app-services/
[tables]:../../../cosmos-db/table-storage-how-to-use-ruby.md
[vm-instructions]:createportal.md

<!-- External Links -->
[rails-guides]:http://guides.rubyonrails.org/
[sqlite3]:http://www.sqlite.org/

<!-- Images -->

[default-rails-cloud]:./media/virtual-machines-linux-classic-ruby-rails-web-app/basicrailscloud.png
[vmlist]:./media/virtual-machines-linux-classic-ruby-rails-web-app/vmlist.png
[endpoints]:./media/virtual-machines-linux-classic-ruby-rails-web-app/endpoints.png
[new-endpoint]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint.png
[new-endpoint1]:./media/virtual-machines-linux-classic-ruby-rails-web-app/newendpoint1.png
