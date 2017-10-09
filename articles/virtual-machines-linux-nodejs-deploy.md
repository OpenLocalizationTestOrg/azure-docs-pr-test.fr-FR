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
# <a name="deploy-a-nodejs-application-toolinux-virtual-machines-in-azure"></a>Déployer un tooLinux d’application Node.js Machines virtuelles dans Azure
Ce didacticiel montre comment tootake une application Node.js et déployer des machines virtuelles de tooLinux s’exécutant dans Azure. instructions Hello dans ce didacticiel peuvent être suivies sur n’importe quel système d’exploitation qui est capable d’exécuter Node.js.

Vous découvrirez comment effectuer les actions suivantes :

* Répliquer et cloner un référentiel GitHub contenant une application TODO simple.
* Créez et configurez deux ordinateurs virtuels de Linux dans l’application de hello toorun Azure ;
* Effectuer une itération sur une application hello en envoyant la machine virtuelle de mises à jour toohello web frontal.

> [!NOTE]
> toocomplete ce didacticiel, vous avez besoin d’un compte GitHub et un compte Microsoft Azure et hello capacité toouse Git à partir d’un ordinateur de développement.
> 
> Si vous n’avez pas de compte GitHub, vous pouvez vous inscrire [ici](https://github.com/join).
> 
> Si vous n’avez pas de compte [Microsoft Azure](https://azure.microsoft.com/), vous pouvez vous inscrire à un essai GRATUIT [ici](https://azure.microsoft.com/pricing/free-trial/). Cela va également vous guider hello inscription pour un [Account Microsoft](http://account.microsoft.com) si vous n’en avez pas déjà. Par ailleurs, si vous êtes abonné à Visual Studio, vous pouvez [activer vos avantages MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).
> 
> Si vous n’avez pas git sur votre machine de développement et que vous utilisez un ordinateur Macintosh ou Windows, installez git à partir d’ [ici](http://www.git-scm.com). Si vous utilisez Linux, installer git à l’aide de mécanisme de hello plus approprié, tel que `sudo apt-get install git`.
> 
> 

## <a name="forking-and-cloning-hello-todo-application"></a>Coexistence et clonage hello TODO Application
Hello application TODO utilisée par ce didacticiel implémente un serveur frontal web simple sur une instance de MongoDB qui conserve une liste de tâches. Une fois connectés tooGitHub, accédez [ici](https://github.com/stepro/node-todo) toofind hello application et effectuer un branchement à l’aide de lien de hello en haut à droite hello. Cette action doit créer un référentiel dans votre compte nommé *nom_compte*/node-todo.

À présent sur votre machine de développement, clonez ce référentiel :

    git clone https://github.com/accountname/node-todo.git

Nous utiliserons ce clone local du référentiel de hello un peu plus tard lors de la modification du code source de toohello.

## <a name="creating-and-configuring-hello-linux-virtual-machines"></a>Création et configuration hello les Machines virtuelles Linux
Azure prend totalement en charge le calcul brut à l’aide de machines virtuelles Linux. Cette partie de la montre de didacticiel hello comment vous pouvez facilement faire tourner les deux machines virtuelles de Linux et déployer toothem d’application TODO hello, en cours d’exécution hello du serveur web frontal sur l’un et hello instance MongoDB sur hello autres.

### <a name="creating-virtual-machines"></a>Création de machines virtuelles
toocreate de façon plus simple Hello une machine virtuelle dans Azure est toouse hello portail Azure. Cliquez sur [ici](https://portal.azure.com) toosign dans et lancez hello Azure Portal dans votre navigateur web. Une fois chargé hello portail Azure, effectuez hello comme suit :

* Cliquez sur hello « + nouveau » lier ;
* Sélectionner la catégorie « Calcul » de hello et choisissez « Ubuntu Server 14.04 LTS » ;
* Sélectionnez le modèle de déploiement « Gestionnaire de ressources » hello et cliquez sur « Créer » ;
* Renseignez les principes fondamentaux hello en suivant les recommandations suivantes :
  * Spécifiez un nom que vous pourrez facilement identifier plus tard.
  * Pour ce didacticiel, choisissez l’authentification par mot de passe.
  * Créez un groupe de ressources portant un nom identifiable.
* Pourquoi la taille de Machine virtuelle, « A1 Standard » est un choix raisonnable pour ce didacticiel.
* Pour les paramètres supplémentaires, vérifiez que le type de disque hello est « Standard » et accepter que tous les hello des valeurs par défaut restantes.
* Déclencher la création d’hello sur la page de résumé hello.

Effectuer hello ci-dessus traiter deux fois toocreate deux Linux virtuels, un pour hello web frontal et un pour l’instance de MongoDB hello. La création d’ordinateurs virtuels hello prendra environ 5 à 10 minutes.

### <a name="assigning-a-dns-entry-for-virtual-machines"></a>Affectation d’une entrée DNS pour les machines virtuelles
Les machines virtuelles créées dans Azure sont par défaut uniquement accessibles par le biais d’une adresse IP publique comme 1.2.3.4. Assurons-nous machines de hello plus facilement identifiables en leur attribuant des entrées DNS.

Une fois que le portail de hello indique que les machines virtuelles de hello ont été créés, cliquez sur lien des « Ordinateurs virtuels » hello dans la barre de navigation gauche hello et localiser vos ordinateurs. Pour chaque machine :

* Recherchez l’onglet d’Essentials hello et cliquez sur hello les adresse IP publique ;
* Dans la configuration d’adresse IP publique hello, affecter une étiquette de nom DNS et d’enregistrer.

portail de Hello garantit que vous spécifiez le nom hello est disponible. Après avoir enregistré la configuration de hello, vos ordinateurs virtuels auront des noms d’hôtes similaire trop`machinename.region.cloudapp.azure.com`.

### <a name="connecting-toohello-virtual-machines"></a>Connexion toohello Machines virtuelles
Lorsque vos machines virtuelles ont été configurés, ils ont été préconfigurés tooallow des connexions à distance via SSH. Il s’agit de mécanisme hello nous allons utiliser des machines virtuelles de hello tooconfigure. Si vous utilisez des fenêtres pour votre développement, vous devez tooget un client SSH si vous n’en avez pas déjà. Il est courant de choisir PuTTY, téléchargeable à partir d’ [ici](http://www.chiark.greenend.org.uk/~sgtatham/putty/). Les systèmes d’exploitation Macintosh et Linux sont fournis avec une version du protocole SSH préinstallée.

### <a name="configuring-hello-web-frontend-virtual-machine"></a>Configuration hello Machine virtuelle de serveur frontal Web
Ordinateur de serveur frontal web SSH toohello que vous avez créé à l’aide de PuTTY, ssh ligne de commande ou votre outil SSH autres préféré. S’affiche alors un message de bienvenue, suivi d’une invite de commandes.

Tout d’abord, vérifiez que git est installé ainsi que le nœud :

    sudo apt-get install -y git
    curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -
    sudo apt-get install -y nodejs

Serveur frontal web de l’application hello repose sur certains modules Node.js natifs, nous devons également ensemble essentiel de hello tooinstall des outils de génération :

    sudo apt-get install -y build-essential

Enfin, nous allons de l’installation d’une application Node.js appelée *indéfiniment*, ce qui contribue à toorun Node.js serveur d’applications :

    sudo npm install -g forever

Il s’agit de toutes les dépendances de hello nécessaires sur le serveur frontal de cette machine virtuelle toobe toorun en mesure de hello l’application web, nous allons donc obtenir cette exécution. toodo, nous allons créer tout d’abord un clone bare du référentiel GitHub de hello vous dupliquée précédemment afin que vous pouvez facilement publier des mises à jour toohello virtual machine (nous aborderons ce scénario de mise à jour plus tard) et puis cloner hello bare clone tooprovide une version de hello espace de stockage qui permettre être exécutée.

Démarrer à partir du répertoire de base (~) hello, exécutez hello suivant les commandes (en remplaçant *accountname* avec votre nom de compte d’utilisateur GitHub) :

    git clone --bare https://github.com/accountname/node-todo.git
    git clone node-todo.git

Maintenant, entrez le répertoire de nœud-todo hello et exécuter ces commandes :

    npm install
    forever start server.js

Hello serveur frontal de l’application web est en cours d’exécution, toutefois, il existe une étape supplémentaire avant que vous pouvez accéder à application hello depuis un navigateur web. machine virtuelle que vous avez créé Hello est protégé par une ressource Azure appelée un *groupe de sécurité réseau*, lequel a été créée pour vous lorsque vous avez approvisionné hello d’ordinateur virtuel. Actuellement, cette ressource autorise uniquement les demandes externes tooport toobe 22 routé toohello machine virtuelle, ce qui permet la communication SSH avec l’ordinateur de hello, mais rien d’autre. Par conséquent, Bonjour de tooview commande application TODO, qui est configuré toorun sur le port 8080, ce port doit également toobe ouvert.

Retour toohello portail Azure et hello complète comme suit :

* Cliquez sur « Groupes de ressources » dans la barre de navigation gauche hello ;
* Sélectionnez groupe de ressources hello qui contient votre machine virtuelle ;
* Dans hello obtenu la liste des ressources, sélectionnez le groupe de sécurité réseau hello (hello une par une icône de bouclier) ;
* Dans les propriétés de hello, choisissez « règles de sécurité de trafic entrant » ;
* Dans la barre d’outils de hello, cliquez sur « Ajouter » ;
* Fournissez un nom comme default-allow-todo.
* Définir le protocole de hello trop « TCP » ;
* Définir la plage de ports de destination hello trop « 8080 ; »
* Cliquez sur OK et attendre toobe de règle de sécurité hello créé.

Après avoir créé cette règle de sécurité, hello application de tâches est visible publiquement sur internet de hello et vous pouvez parcourir tooit, par exemple en utilisant une URL comme :

    http://machinename.region.cloudapp.azure.com:8080

Vous remarquerez que, bien que nous n’avons pas encore configuré la machine virtuelle de MongoDB hello, hello les application TODO apparaît toobe très fonctionnelle. Il s’agit, car le référentiel de code source hello est codé en dur toouse une instance MongoDB déjà déployée. Une fois que nous avons configuré la machine virtuelle de MongoDB hello, nous revenir en arrière et modifier, tooutilize de code source hello notre instance MongoDB privée à la place.

### <a name="configuring-hello-mongodb-virtual-machine"></a>Configuration hello MongoDB Virtual Machine
SSH toohello deuxième ordinateur que vous avez créé à l’aide de PuTTY, ssh ligne de commande ou votre outil SSH autres préféré. Lorsque vous voyez le message d’accueil hello et l’invite de commandes, installez MongoDB (ces instructions ont été effectuées à partir de [ici](https://docs.mongodb.org/master/tutorial/install-mongodb-on-ubuntu/)) :

    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927
    echo "deb http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list
    sudo apt-get update
    sudo apt-get install -y mongodb-org

Par défaut, MongoDB est configuré pour être uniquement accessible localement. Pour ce didacticiel, nous allons configurer MongoDB afin qu’il est accessible à partir de l’ordinateur virtuel de l’application hello. Dans un contexte sudo, ouvrir le fichier de /etc/mongod.conf hello et localiser hello `# network interfaces` section. Hello de modification `net.bindIp` configuration valeur trop`0.0.0.0`.

> [!NOTE]
> Cette configuration s’applique à des fins de hello de ce didacticiel uniquement. Il ne s’agit **pas** d’une pratique de sécurité recommandée et elle ne doit pas être utilisée dans les environnements de production.
> 
> 

Maintenant, vérifiez que hello MongoDB service a été démarré :

    sudo service mongod restart

MongoDB fonctionne sur le port 27017 par défaut. Par conséquent, Bonjour même façon qu’il est nécessaire de tooopen le port 8080 sur la machine virtuelle de hello web frontal, nous devons tooopen port 27017 sur l’ordinateur virtuel de MongoDB hello.

Retour toohello portail Azure et hello complète comme suit :

* Cliquez sur « Groupes de ressources » dans la barre de navigation gauche hello ;
* Sélectionnez groupe de ressources hello qui contient l’ordinateur virtuel de MongoDB hello ;
* Dans hello obtenu la liste des ressources, sélectionnez groupe de sécurité réseau hello (hello une par une icône de bouclier) avec hello que même nom que celui que vous avez donné de machine virtuelle de MongoDB toohello ;
* Dans les propriétés de hello, choisissez « règles de sécurité de trafic entrant » ;
* Dans la barre d’outils de hello, cliquez sur « Ajouter » ;
* Fournissez un nom comme default-allow-mongo.
* Définir le protocole de hello trop « TCP » ;
* Définir la plage de ports de destination hello trop « 27017 » ;
* Cliquez sur OK et attendre toobe de règle de sécurité hello créé.

## <a name="iterating-on-hello-todo-application"></a>Itération sur hello application de TODO
Jusqu'à présent, nous avons mis en service les ordinateurs virtuels Linux deux : celui qui exécute l’application hello serveur web frontal et l’autre qui exécute une instance de MongoDB. Mais il existe un problème : hello web frontal n’est pas utilise encore hello configuré MongoDB instance. Nous allons résoudre cela en mettant à jour hello web frontal code toouse une variable d’environnement au lieu d’une instance codé en dur.

### <a name="changing-hello-todo-application"></a>La modification d’application de hello TODO
Sur votre ordinateur de développement où vous avez cloné tout d’abord référentiel de nœud-todo hello, ouvrez hello `node-todo/config/database.js` dans votre éditeur favori et modifiez la valeur de codée en dur de hello comme valeur de l’url hello `mongodb://...` trop`process.env.MONGODB`.

Valider vos modifications et push toohello GitHub master :

    git commit -am "Get MongoDB instance from env"
    git push origin master

Malheureusement, cela ne publie pas machine virtuelle de hello modification toohello web frontal. Apportons quelques tooenable de machine virtuelle de toothat de modifications plus un mécanisme simple mais efficace pour la publication des mises à jour afin de pouvoir observer rapidement effet hello de modifications hello dans l’environnement d’exploitation hello.

### <a name="configuring-hello-web-frontend-virtual-machine"></a>Configuration hello Machine virtuelle de serveur frontal Web
Rappelez-vous que nous avons créé un clone bare du référentiel de nœud-todo hello précédemment sur l’ordinateur virtuel de hello web frontal. Il s’avère que cette action créé un nouveau Git distant toowhich modifications peuvent être appliquées. Toutefois, simplement en exécutant un push toothis à distance ne donne assez de modèle d’itération rapide hello que les développeurs cherchez lorsque vous travaillez sur leur code.

Ce que nous veut toodo en mesure de toobe est Vérifiez qu’en cas d’un référentiel distant de toohello par émission de données sur l’ordinateur virtuel de hello, application de tâches en cours d’exécution hello est automatiquement mis à jour. Heureusement, il s’agit de tooachieve facile avec git.

GIT expose un nombre de connexions qui sont appelés à des moments tooreact tooactions est effectuées sur le référentiel de hello. Elles sont spécifiées à l’aide de scripts de shell du référentiel hello `hooks` dossier. raccordement de Hello n’est plus applicable pour le scénario de mise à jour automatique hello est hello `post-update` événement.

Dans une machine virtuelle SSH session toohello web frontal, modifiez toohello `~/node-todo.git/hooks` répertoire et ajoutez hello tooa contenu nommé le fichier suivant `post-update` (en remplaçant `machinename` et `region` avec vos informations d’ordinateur virtuel MongoDB) :

    #!/bin/bash

    forever stopall
    unset 'GIT_DIR'
    export MONGODB="mongodb://machinename.region.cloudapp.azure.com:27017/tododb"
    cd ~/node-todo && git fetch origin && git pull origin master && npm install && forever start ~/node-todo/server.js
    exec git update-server-info

Vérifiez que ce fichier est exécutable en exécutant hello de commande suivante :

    chmod 755 post-update

Ce script vérifie qu’application serveur en cours de hello est arrêtée, code hello dans le référentiel cloné de hello est toohello mis à jour plus récentes, toutes les dépendances de mise à jour sont satisfaites, et hello serveur est redémarré. Cela garantit également que cet environnement hello a été configuré en vue de la réception de notre première mise à jour tooget hello MongoDB instance de l’application à partir d’une variable d’environnement.

### <a name="configuring-your-development-machine"></a>Configuration de votre machine de développement
Maintenant nous allons obtenir votre ordinateur de développement raccordée d’ordinateur virtuel de toohello web frontal. Il s’agit aussi simple que l’ajout de référentiel de bare hello sur l’ordinateur virtuel de hello un distant. Exécuter cet exemple hello suivant toodo de commande (en remplaçant *utilisateur* avec votre nom de connexion de machine virtuelle de serveur frontal web et *machinename* et *région* le cas échéant) :

    git remote add azure user@machinename.region.cloudapp.azure.com:node-todo.git

C’est tout en exécutant un push tooenable nécessaire ou la publication en vigueur, modifie l’ordinateur virtuel de toohello web frontal.

### <a name="publishing-updates"></a>Publication des mises à jour
Nous allons publier hello une modification qui a été effectuée jusqu'à présent afin que l’application hello utilisera sa propre instance MongoDB :

    git push azure master

Vous devez voir toothis similaire de sortie :

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

Une fois cette commande terminée, essayez d’actualiser l’application hello dans un navigateur web. Vous devez être en mesure de toosee que liste de tâches hello présentée ici est vide et n’est plus liée toohello partagé déployé MongoDB instance.

didacticiel de hello toocomplete, nous allons modifier un autre, plus visible. Sur votre ordinateur de développement, ouvrez le fichier de node-todo/public/index.html de hello à l’aide de votre éditeur favori. Localiser l’en-tête de jumbotron hello et modifier le titre hello à partir de « Je suis un Todo-aholic » trop « je ne suis un Todo-aholic sur Azure ! ».

Maintenant procédons à la validation :

    git commit -am "Azurify hello title"

Cette fois, nous allons publier hello modification tooAzure avant d’en exécutant un push du référentiel GitHub tooback toohello :

    git push azure master

Une fois cette commande exécutée, l’actualisation hello web page et vous modifications seront visibles hello. Dans la mesure où elles apparaîtront correctement, push hello modification toohello arrière origine distant : 

    git push origin master

## <a name="next-steps"></a>Étapes suivantes
Cet article a montré comment tootake une application Node.js et déployer des machines virtuelles de tooLinux s’exécutant dans Azure. toolearn en savoir plus sur les ordinateurs virtuels Linux dans Azure, consultez [tooLinux Introduction sur Azure](/documentation/articles/virtual-machines-linux-introduction/).

Pour plus d’informations sur les applications Node.js toodevelop sur Azure, consultez hello [centre de développement Node.js](/develop/nodejs/).

