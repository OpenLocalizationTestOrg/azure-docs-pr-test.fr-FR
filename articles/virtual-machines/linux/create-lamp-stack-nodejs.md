---
title: "FEU d’aaaDeploy sur une machine virtuelle Linux hello Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment tooinstall hello feu de pile sur un VM Linux dans Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jluk
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: NA
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: e78a82d388ce68710933b9b673aa1b2460bdbb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a>Déployer la pile LAMP avec hello Azure CLI 1.0
Cet article vous guide tout au long de comment toodeploy un Apache web server, MySQL et PHP (pile de feu hello) sur Azure. Vous avez besoin d’un compte Azure ([obtenir une évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/)) et hello [CLI d’Azure](../../cli-install-nodejs.md) qui est [connecté tooyour compte Azure](../../xplat-cli-connect.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Tâche de hello CLI versions toocomplete
Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :

- [Azure CLI 1.0] – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)
- [Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* Déploiement de LAMP sur une machine virtuelle existante

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a>Procédure pas à pas de déploiement de LAMP sur une nouvelle machine virtuelle
Vous pouvez commencer par créer un [groupe de ressources](../../azure-resource-manager/resource-group-overview.md) qui contiendra hello nouvelle machine virtuelle :

    $ azure group create uniqueResourceGroup westus
    info:    Executing command group create
    info:    Getting resource group uniqueResourceGroup
    info:    Creating resource group uniqueResourceGroup
    info:    Created resource group uniqueResourceGroup
    data:    Id:                  /subscriptions/########-####-####-####-############/resourceGroups/uniqueResourceGroup
    data:    Name:                uniqueResourceGroup
    data:    Location:            westus
    data:    Provisioning State:  Succeeded
    data:    Tags: null
    data:
    info:    group create command OK

toocreate hello machine virtuelle proprement dite, vous pouvez utiliser un modèle Azure Resource Manager déjà écrite [ici sur GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

Vous devez voir une réponse invitant l’utilisateur à renseigner certaines informations :

    info:    Executing command group deployment create
    info:    Supply values for hello following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment toocomplete
    data:    DeploymentName     : uniqueLampName
    data:    ResourceGroupName  : uniqueResourceGroup
    data:    ProvisioningState  : Succeeded
    data:    Timestamp          :
    data:    Mode               : Incremental
    data:    CorrelationId      : d51bbf3c-88f1-4cf3-a8b3-942c6925f381
    data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
    data:    ContentVersion     : 1.0.0.0
    data:    DeploymentParameters :
    data:    Name                      Type          Value
    data:    ------------------------  ------------  -----------
    data:    storageAccountNamePrefix  String        lampprefix
    data:    location                  String        westus
    data:    adminUsername             String        someUsername
    data:    adminPassword             SecureString  undefined
    data:    mySqlPassword             SecureString  undefined
    data:    dnsLabelPrefix            String        azlamptest
    data:    ubuntuOSVersion           String        14.04.2-LTS
    info:    group deployment create command OK

Vous avez maintenant créé une machine virtuelle Linux avec LAMP déjà installé. Si vous le souhaitez, vous pouvez vérifier l’installation de hello en sautant trop bas[vérifier feu installé avec succès](#verify-lamp-successfully-installed).

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a>Procédure pas à pas de déploiement de LAMP sur une machine virtuelle existante
Si vous avez besoin d’aide pour créer une VM Linux, vous pouvez head [toolearn ici comment toocreate un VM Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Ensuite, vous devez tooSSH dans hello Linux VM. Si vous avez besoin d’aide sur la création d’une clé SSH, vous pouvez head [toolearn ici comment toocreate une clé SSH sur Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
Si vous disposez déjà d’une clé SSH, continuez et ouvrez en ligne de commande une connexion SSH à votre machine virtuelle Linux avec `ssh exampleUsername@exampleDNS`.

Maintenant que vous utilisez dans votre VM Linux, nous pouvons guider dans l’installation de la pile de feu hello sur les distributions Debian. les commandes exactes Hello peuvent différer pour les autres versions de Linux.

#### <a name="installing-on-debianubuntu"></a>Installation sur Debian/Ubuntu
Vous devez hello suivant des packages installés : `apache2`, `mysql-server`, `php5`, et `php5-mysql`. Vous pouvez les installer directement à partir de ces packages ou à l’aide de Tasksel. Les instructions pour les deux options figurent ci-dessous.
Avant d’installer, vous devez toodownload et mettre à jour les listes de package.

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a>Packages individuels
Utilisation d’apt-get :

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a>Utilisation de Tasksel
Vous pouvez également télécharger Tasksel, un outil Debian/Ubuntu qui installe plusieurs packages connexes en tant que tâche coordonnée sur votre système.

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

Après l’exécution d’une des options précédentes de hello, vous allez être invité à tooinstall ces packages et divers autres dépendances. Appuyez sur « y », puis sur 'Entrée' toocontinue et suivez les autres tooset demande un mot de passe d’administration pour MySQL. Cette commande installe hello minimale requise PHP les extensions nécessitées toouse PHP avec MySQL. 

![][1]

Exécutez hello suivant commande toosee autres extensions PHP disponibles sous forme de packages :

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a>Création d’un document info.php
Vous devez maintenant être en mesure de toocheck quelle version de PHP, MySQL et Apache vous avez via la ligne de commande hello en tapant `apache2 -v`, `mysql -v`, ou `php -v`.

Si vous devez comme tootest en outre, vous pouvez créer un tooview de page PHP info rapide dans un navigateur. Créez un fichier avec l’éditeur de texte Nano à l’aide de la commande suivante :

    user@ubuntu$ sudo nano /var/www/html/info.php

Dans l’éditeur de texte hello GNU Nano, ajoutez hello lignes suivantes :

    <?php
    phpinfo();
    ?>

Ensuite, enregistrez et quittez l’éditeur de texte hello.

Redémarrez Apache avec cette commande pour que toutes les nouvelles installations prennent effet.

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a>Vérification de l’installation correcte de LAMP
Vous pouvez maintenant vérifier vous avez créé en ouvrant un navigateur et allez toohttp://youruniqueDNS/info.php page des informations hello PHP. Il doit se présenter une image toothis similaire.

![][2]

Vous pouvez vérifier votre installation Apache en consultant hello Apache2 Ubuntu par défaut Page en accédant tooyou http://youruniqueDNS/. Les informations suivantes s’affichent, comme sur cette image.

![][3]

Félicitations, vous avez configuré une pile LAMP sur votre machine virtuelle Azure !

## <a name="next-steps"></a>Étapes suivantes
Consultez hello documentation Ubuntu sur la pile de feu hello :

* [https://help.ubuntu.com/community/ApacheMySQLPHP](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png