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
# <a name="ruby-on-rails-web-application-on-an-azure-vm"></a>Application Web Ruby on Rails sur une machine virtuelle Azure
Ce didacticiel montre comment toohost Ruby sur le site Web de Rails sur Azure à l’aide d’une machine virtuelle Linux.  

Ce didacticiel a été validé à l’aide d’Ubuntu Server 14.04 LTS. Si vous utilisez une autre distribution Linux, vous devrez peut-être toomodify hello étapes tooinstall Rails.

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../../../azure-resource-manager/resource-manager-deployment-model.md).  Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.
>
>

## <a name="create-an-azure-vm"></a>Création d’une machine virtuelle Azure
Commencez par créer une machine virtuelle Azure avec une image Linux.

toocreate hello de machine virtuelle, vous pouvez utiliser hello portail Azure ou hello Azure Interface de ligne de commande (CLI).

### <a name="azure-portal"></a>Portail Azure
1. L’authentification à hello [portail Azure](https://portal.azure.com)
2. Cliquez sur **nouveau**, puis tapez « Ubuntu Server 14.04 » dans la zone de recherche hello. Cliquez sur entrée hello retournée par la recherche de hello. Pour le modèle de déploiement hello, sélectionnez **classique**, puis cliquez sur « Créer ».
3. Dans le panneau des principes de base hello, fournir des valeurs pour les champs hello requis : nom (pour hello machine virtuelle), nom d’utilisateur, type d’authentification et les informations d’identification correspondantes hello, abonnement Azure, groupe de ressources et l’emplacement.

   ![Create a new Ubuntu Image](./media/virtual-machines-linux-classic-ruby-rails-web-app/createvm.png)

4. Après la configuration de machine virtuelle de hello, cliquez sur le nom d’ordinateur virtuel hello, puis cliquez sur **points de terminaison** Bonjour **paramètres** catégorie. Trouver le point de terminaison hello SSH, répertorié sous **autonome**.

   ![Point de terminaison par défaut.](./media/virtual-machines-linux-classic-ruby-rails-web-app/endpointsnewportal.png)

### <a name="azure-cli"></a>Interface de ligne de commande Azure
Suivez les étapes de hello dans [créer une Machine virtuelle exécutant Linux][vm-instructions].

Après la configuration de machine virtuelle de hello, vous pouvez obtenir le point de terminaison SSH hello en exécutant hello de commande suivante :

    azure vm endpoint list <vm-name>  

## <a name="install-ruby-on-rails"></a>installation de Ruby sur Rails
1. Utiliser SSH tooconnect toohello machine virtuelle.
2. À partir de la session SSH hello, utilisez hello suivant de commandes tooinstall Ruby de hello machine virtuelle :

        sudo apt-get update -y
        sudo apt-get upgrade -y

        sudo apt-add-repository ppa:brightbox/ruby-ng
        sudo apt-get update
        sudo apt-get install ruby2.4

        > [!TIP]
        > hello brightbox repository contains hello current Ruby distribution.

    installation de Hello peut prendre quelques minutes. Lorsqu’elle est terminée, utilisez hello suivant tooverify commande que Ruby est installé :

        ruby -v

3. Suivant de hello utilisation de commandes de Rails de tooinstall :

        sudo gem install rails --no-rdoc --no-ri -V

    Utilisez hello--non-rdoc et--tooskip non-ri indicateurs installation de la documentation de hello, qui est plus rapide.
    Cette commande probablement prendra un certain temps tooexecute, afin de l’ajout de hello -V Affiche des informations sur la progression de l’installation hello.

## <a name="create-and-run-an-app"></a>Création et exécution d’une application
Toujours connecté via une connexion SSH, exécutez hello suivant de commandes :

    rails new myapp
    cd myapp
    rails server -b 0.0.0.0 -p 3000

Hello [nouveau](http://guides.rubyonrails.org/command_line.html#rails-new) commande crée une nouvelle application de quadrillage. Hello [server](http://guides.rubyonrails.org/command_line.html#rails-server) commande démarre hello WEBrick au serveur web qui est fourni avec les Rails. (Pour la production, vous souhaiterez probablement toouse un autre serveur, telles que licorne ou passagers.)

Vous devez voir s’afficher sortie similaire toohello.

    => Booting WEBrick
    => Rails 4.2.1 application starting in development on http://0.0.0.0:3000
    => Run `rails server -h` for more startup options
    => Ctrl-C tooshutdown server
    [2015-06-09 23:34:23] INFO  WEBrick 1.3.1
    [2015-06-09 23:34:23] INFO  ruby 1.9.3 (2013-11-22) [x86_64-linux]
    [2015-06-09 23:34:23] INFO  WEBrick::HTTPServer#start: pid=27766 port=3000

## <a name="add-an-endpoint"></a>Ajout d’un point de terminaison
1. Accédez toohello [Azure portal] [https://portal.azure.com] et sélectionnez votre machine virtuelle.

2. Sélectionnez **points de terminaison** Bonjour **paramètres** le long de la page de hello hello bord gauche.

3. Cliquez sur **ajouter** en hello haut hello.

4. Bonjour **ajouter le point de terminaison** boîte de dialogue, entrez hello informations suivantes :

   * **Nom** : HTTP
   * **Protocole**: TCP
   * **Port public** : 80
   * **Port privé** : 3000
   * **Adresse PI flottante** : Désactivée
   * **Liste de contrôle d’accès - ordre**: 1001, ou une autre valeur qui définit la priorité de hello de cette règle d’accès.
   * **Liste de contrôle d’accès - nom** : allowHTTP
   * **Liste de contrôle d’accès - Action** : autoriser
   * **Liste de contrôle d’accès - sous-réseau distant** : 1.0.0.0/16

     Ce point de terminaison a un port public 80 qui achemine le trafic toohello port privé (3000), où hello Rails serveur écoute. règle de liste de contrôle Hello accès permet de trafic public sur le port 80.

     ![new-endpoint](./media/virtual-machines-linux-classic-ruby-rails-web-app/createendpoint.png)

5. Cliquez sur le point de terminaison toosave OK hello.

6. Un message doit apparaître indiquant **Enregistrement du point de terminaison de la machine virtuelle**. Une fois ce message disparaît, le point de terminaison hello est actif. Vous pouvez maintenant tester votre application en parcourant le nom DNS de toohello de votre machine virtuelle. site Web de Hello doit apparaître comme toohello suivantes :

    ![page rails par défaut][default-rails-cloud]

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez effectué la plupart des étapes de hello manuellement. Dans un environnement de production, vous écrivez votre application sur un ordinateur de développement et déployez-le toohello machine virtuelle Azure. En outre, la plupart des environnements de production hébergent application de quadrillage hello conjointement avec un autre processus serveur tels que Apache ou NginX, qui gère demande des instances de routage toomultiple d’application de quadrillage hello et servant de ressources statiques. Pour plus d’informations, consultez http://rubyonrails.org/deploy/.

toolearn en savoir plus sur Ruby on Rails, visitez hello [Ruby sur les Rails Guides][rails-guides].

toouse des services Azure à partir de votre application Ruby, consultez :

* [Utilisation du stockage d’objets blob à partir de Ruby][blobs]
* [Utilisation du stockage de tables à partir de Ruby][tables]
* [Traiter du contenu de la bande passante élevée avec hello Content Delivery Network][cdn-howto]

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
