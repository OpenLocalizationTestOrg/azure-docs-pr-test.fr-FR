---
title: "aaaDeploy 3 nœuds Deis cluster | Documents Microsoft"
description: "Cet article décrit comment toocreate Deis 3 nœuds clusters sur Azure à l’aide d’un modèle Azure Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a>Déployer et configurer un cluster Deis à 3 nœuds dans Azure
Cet article vous détaille l’approvisionnement d’un cluster [Deis](http://deis.io/) sur Azure. Elle couvre toutes les étapes de hello de création toodeploying des certificats nécessaires hello et un exemple de mise à l’échelle **accédez** application sur le cluster qui vient d’être mis en service de hello.

Hello diagramme suivant illustre architecture hello du système de hello déployé. Un administrateur système gère à l’aide du cluster hello Deis des outils tels que **deis** et **deisctl**. Les connexions sont établies via un équilibrage de charge Azure, qui transfère les nœuds de cluster de hello tooone de connexions hello du membre de hello. accès des clients Hello des applications via l’équilibrage de charge hello également déployées. Dans ce cas, équilibrage de charge hello transfère hello trafic tooa Deis maillage du routeur, qui achemine davantage de conteneurs Docker de trafic toocorresponding hébergés sur le cluster de hello.

  ![Diagramme d’architecture du cluster Deis déployé](./media/deis-cluster/architecture-overview.png)

Dans toorun ordre via hello comme suit, vous devez :

* Un abonnement Azure actif. Si vous n’en avez pas, vous pouvez obtenir une version d’essai sur [azure.com](https://azure.microsoft.com/).
* Un travail ou des groupes de ressources Azure scolaire id toouse. Si vous avez un compte personnel et un journal avec un id Microsoft, vous devez trop[créer un id de travail de votre personnel une](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Soit--selon votre système d’exploitation du client--hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) ou hello [CLI d’Azure pour Mac, Linux et Windows](../../cli-install-nodejs.md).
* [OpenSSL](https://www.openssl.org/). OpenSSL est utilisé toogenerate hello les certificats nécessaires.
* Un client Git, comme [Git Bash](https://git-scm.com/).
* tootest hello exemple d’application, vous devez également un serveur DNS. Vous pouvez utiliser les serveurs ou services DNS qui prennent en charge les enregistrements DNS de caractères génériques A Record.
* Un ordinateur toorun Deis des outils clients. Vous pouvez utiliser un ordinateur local ou une machine virtuelle. Vous pouvez exécuter ces outils sur presque n’importe quel distribution Linux, mais Ubuntu utilisent hello instructions suivantes.

## <a name="provision-hello-cluster"></a>Cluster hello de disposition
Dans cette section, vous allez utiliser un [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) modèle à partir du référentiel open source de hello [modèles de démarrage rapide azure](https://github.com/Azure/azure-quickstart-templates). Tout d’abord, vous allez copier vers le bas du modèle de hello. Ensuite, créez une paire de clés SSH à des fins d’authentification. Ensuite, configurez le nouvel identifiant de votre cluster. Et enfin, vous allez utiliser le script de Shell hello ou le cluster hello tooprovision hello PowerShell script.

1. Référentiel de hello clone : [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. Atteindre le dossier de modèles toohello :
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. Créez une paire de clés SSH à l’aide de l’outil ssh-keygen :
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. Générer un certificat à l’aide de hello au-dessus de clé privée :
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. Accédez trop[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate un nouveau jeton de cluster, qui ressemble à quelque chose comme :
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   Chaque cluster CoreOS doit toohave un jeton unique à partir de ce service gratuit. Pour plus d’informations, voir la [documentation CoreOS](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) .
6. Modifier hello **cloud-config.yaml** fichier existant de hello tooreplace **découverte** jeton avec le nouveau jeton d’hello :
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. Modifier hello **azuredeploy-parameters.json** fichier : certificat hello ouvrir créé à l’étape 4 dans un éditeur de texte. Copiez tout le texte entre `----BEGIN CERTIFICATE-----` et `-----END CERTIFICATE-----` dans hello **sshKeyData** paramètre (vous devez tooremove tous les caractères de saut de ligne).
8. Modifier hello **newStorageAccountName** paramètre. Il s’agit de compte de stockage hello pour les disques de machine virtuelle du système d’exploitation. Nom de ce compte a toobe global unique.
9. Modifier hello **publicDomainName** paramètre. Cela va faire partie du nom DNS de hello associé hello charge équilibrage adresse IP publique. Hello FQDN final auront hello format de *[valeur de ce paramètre]*. *[Région]* . cloudapp.azure.com. Par exemple, si vous spécifiez le nom de hello en tant que deishbai32, et groupe de ressources hello est la région ouest des États-Unis toohello déployé, puis hello final équilibrage de charge de nom de domaine complet tooyour sera deishbai32.westus.cloudapp.azure.com.
10. Enregistrez le fichier de paramètres hello. Et ensuite, vous pouvez configurer cluster hello à l’aide d’Azure PowerShell :
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    ou de la CLI Azure :
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. Une fois le groupe de ressources hello est configuré, vous pouvez voir toutes les ressources hello dans le groupe de hello sur le portail Azure classic. Comme indiqué dans hello suivant hello capture d’écran, groupe de ressources contient un réseau virtuel avec trois machines virtuelles, qui sont jointes toohello même groupe à haute disponibilité. groupe de Hello contient également un équilibreur de charge, ce qui a une adresse IP publique associée.
    
    ![Hello configuré le groupe de ressources sur le portail Azure classic](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a>Installer le client de hello
Vous devez **deisctl** toocontrol votre Deis de cluster. Deisctl est installé automatiquement dans tous les nœuds de cluster hello, mais il est un deisctl toouse de bonnes pratiques sur un ordinateur d’administration distinct. En outre, étant donné que tous les nœuds sont configurés avec uniquement des adresses IP privées, vous devez toouse SSH tunneling via l’équilibrage de charge hello, qui a une adresse IP publique, ordinateurs de nœud tooconnect toohello. Hello Voici étapes hello paramétrant deisctl sur un ordinateur virtuel ou Ubuntu physique distinct.

1. Installez deisctl:mkdir deis.
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. Ajoutez votre agent toossh de clé privée :
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. Configurez deisctl :
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

Hello modèle définit les règles NAT entrantes qui mappent 2223 tooinstance 1, 2224 tooinstance 2 et 2225 tooinstance 3. Cela procure une redondance pour l’outil de deisctl hello. Vous pouvez examiner ces règles sur le portail Azure Classic :

![Règles NAT sur l’équilibrage de charge hello](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> Actuellement le modèle de hello prend uniquement en charge les clusters à 3 nœuds. En effet, la définition des règles NAT des modèles Azure Resource Manager présente une limitation : elle ne prend pas en charge la syntaxe de boucle.
> 
> 

## <a name="install-and-start-hello-deis-platform"></a>Installez et démarrez hello Deis de plate-forme
Vous pouvez désormais utiliser deisctl tooinstall et démarrer hello Deis plateforme :

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> Plateforme de hello départ prend un certain temps (jusqu'à 10 minutes). En particulier, le démarrage du service de générateur hello peut prendre un certain temps. Et parfois, il prend quelques tentatives toosucceed : si l’opération de hello semble toohang, essayez de taper `ctrl+c` exécution toobreak de commande hello, puis réessayez.
> 
> 

Vous pouvez utiliser `deisctl list` tooverify si tous les services sont en cours d’exécution :

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

Félicitations ! Votre nouveau cluster Deis est opérationnel sur Azure. Ensuite, nous allons déployer un cluster de hello Go application toosee dans l’action de l’exemple.

## <a name="deploy-and-scale-a-hello-world-application"></a>Déployer et mettre à l’échelle une application Hello World
Hello étapes suivantes montrent comment toodeploy « Hello World » accédez cluster toohello d’application. étapes de Hello sont basées sur [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).

1. Pour hello routage maillage toowork correctement, vous devez toohave un enregistrement générique A pour votre domaine pointe toohello adresse IP publique de l’équilibrage de charge hello. Hello capture d’écran suivante affiche hello un enregistrement d’un enregistrement de domaine exemple sur GoDaddy :
   
    ![Enregistrement « A Record » GoDaddy](./media/deis-cluster/go-daddy.png)
   
   <p />
2. Installez l’outil deis :
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. Créer une clé SSH, puis ajoutez hello tooGitHub de clé publique (bien entendu, vous pouvez également réutiliser vos clés existantes). toocreate une nouvelle paire de clés SSH, utilisez :
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. Ajoutez id_rsa.pub ou hello de clé publique de votre choix, tooGitHub. Pour cela, à l’aide de hello ajouter SSH bouton clé dans l’écran de configuration de clés SSH :
   
   ![Clé GitHub](./media/deis-cluster/github-key.png)
   
   <p />
5. Enregistrez un nouvel utilisateur :
   
        deis register http://deis.[your domain]
   <p />
6. Ajoutez la clé SSH hello :
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. Créez une application.
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p />
8.push de git Hello déclenchera Docker images toobe généré et déployé, qui prendra quelques minutes. À partir de mon expérience, occasionnellement, étape 10 (référentiel de push image tooprivate) peut se bloquer. Dans ce cas, vous pouvez arrêter le processus de hello, à l’aide de remove hello application ' deis applications : détruire : un <application name> ` tooremove hello application and try again. You can use `deis apps:list' toofind nom hello de votre application. Si tout fonctionne, vous devez voir quelque chose comme suit hello à fin hello de sorties de commandes :
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. Vérifiez si l’application hello fonctionne :
   
        curl -S http://[your application name].[your domain]
   Ce qui suit doit s’afficher :
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. Mettre à l’échelle too3 instances de l’application hello :
    
        deis scale cmd=3
    <p />
11. Si vous le souhaitez, vous pouvez utiliser deis Infos tooexamine détails de votre application. Hello sorties suivantes sont mon déploiement d’application :
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a>Étapes suivantes
Cet article vous parcouru toutes les tooprovision d’étapes hello Deis un nouveau cluster sur Azure à l’aide d’un modèle Azure Resource Manager. modèle de Hello prend en charge la redondance dans les connexions, ainsi que pour les applications déployées d’équilibrage de charge des outils. modèle de Hello évite également à l’aide d’adresses IP publiques sur les nœuds membres, qui enregistre des précieuses ressources IP publics et fournit un environnement plus sécurisé d’applications toohost. toolearn, voir hello suivant des articles :

[Présentation d’Azure Resource Manager][resource-group-overview]  
[Comment toouse hello CLI d’Azure][azure-command-line-tools]  
[Utilisation d’Azure PowerShell avec Azure Resource Manager][powershell-azure-resource-manager]  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
