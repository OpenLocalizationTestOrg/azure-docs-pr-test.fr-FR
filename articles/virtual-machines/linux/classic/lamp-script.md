---
title: aaaUse hello CustomScript Extension sur un VM Linux | Documents Microsoft
description: "Découvrez comment toouse hello CustomScript extension toodeploy les applications sur des Machines virtuelles Linux dans Azure créé à l’aide du modèle de déploiement classique hello."
editor: tysonn
manager: timlt
documentationcenter: 
services: virtual-machines-linux
author: gbowerman
tags: azure-service-management
ms.assetid: e535241d-feca-4412-b07a-67c936ba88a0
ms.service: virtual-machines-linux
ms.workload: multiple
ms.tgt_pltfrm: linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: guybo
ms.openlocfilehash: 864a586e70093eefbabc065a3c05e1cf9e315704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a>Déployer une application de feu à l’aide de hello CustomScript Extension de Azure pour Linux
> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello. Pour plus d’informations sur le déploiement d’une pile LAMP à l’aide du modèle de gestionnaire de ressources hello, consultez [ici](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Hello CustomScript Extension de Microsoft Azure pour Linux fournit un moyen toocustomize vos machines virtuelles (VM) en exécutant du code arbitraire écrit dans n’importe quel langage de script pris en charge par hello machine virtuelle (par exemple, Python et un interpréteur de commandes). Cela fournit un tooautomate de manière très flexible des ordinateurs de toomultiple de déploiement d’application.

Vous pouvez déployer hello CustomScript Extension à l’aide de hello portail Azure, Windows PowerShell ou hello Azure Interface de ligne (Azure).

Dans cet article, nous allons utiliser hello CLI d’Azure toodeploy un tooan d’application simple feu Ubuntu VM créé à l’aide du modèle de déploiement classique hello.

## <a name="prerequisites"></a>Composants requis
Pour l’exemple suivant, créez d’abord deux machines virtuelles Azure exécutant Ubuntu 14.04 ou version ultérieure. Hello machines virtuelles sont appelées *script-vm* et *feu-vm*. Utilisez des noms uniques lorsque vous créez des machines virtuelles de hello. Un les commandes CLI utilisée toorun hello et l’autre application de feu hello toodeploy utilisé.

Vous devez également un compte de stockage Azure et une clé tooaccess informatique (vous pouvez obtenir cette information à partir de hello portail Azure).

Si vous avez besoin d’aide pour créer des machines virtuelles Linux sur Azure, consultez trop[créer une Machine virtuelle exécutant Linux](createportal.md).

commandes d’installation Hello supposent Ubuntu, mais vous pouvez adapter les installation hello pour tout pris en charge la distribution de Linux.

Hello machine virtuelle de script-vm doit toohave que CLI d’Azure installé, avec un tooAzure de connexion du travail. Pour plus d’informations, consultez trop[installer et configurer hello Interface de ligne de commande Azure](../../../cli-install-nodejs.md).

## <a name="upload-a-script"></a>Télécharger un script
Nous allons utiliser hello CustomScript Extension toorun un script sur une pile de feu VM tooinstall hello à distance et créer une page PHP. Dans le script de hello ordre tooaccess depuis n’importe où nous allons télécharger sous la forme d’un objet blob Azure.

### <a name="script-overview"></a>Vue d’ensemble du script
exemple de script Hello installe un tooUbuntu de pile LAMP (y compris la configuration d’une installation silencieuse de MySQL), écrit un simple fichier PHP et démarre Apache.

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install hello LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a>Télécharger le script
Enregistrer le script de hello dans un fichier texte, par exemple *install_lamp.sh*, puis téléchargez tooAzure stockage. Vous pouvez le faire facilement avec l’interface de ligne de commande Microsoft Azure. Hello exemple suivant télécharge conteneur de stockage hello fichier tooa nommé « scripts ». Si le conteneur de hello n’existe pas, vous devez toocreate il premier.

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

Également créer un fichier JSON qui décrit comment toodownload hello script depuis le stockage Azure. Enregistrez-la en tant que *public_config.json* (en remplaçant « mystorage » avec le nom de hello de votre compte de stockage) :

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a>Déployer l’extension de hello
Vous pouvez désormais utiliser hello suivant commande toodeploy hello Linux CustomScript Extension toohello à distance à l’aide de la machine virtuelle hello CLI d’Azure.

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

commande précédente Hello télécharge et exécute hello *install_lamp.sh* script sur hello VM appelé *feu-vm*.

Étant donné que l’application hello inclut un serveur web, n’oubliez pas de port d’écoute tooopen HTTP sur hello VM à distance avec la commande suivante hello.

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a>Surveillance et dépannage
Vous pouvez vérifier dans degré hello s’exécute de script personnalisé en le recherchant dans le fichier journal de hello sur hello VM à distance. SSH trop*feu-vm* et la fin du fichier de journal hello avec la commande suivante hello.

    cd /var/log/azure/customscript
    tail -f handler.log

Après avoir exécuté hello CustomScript Extension, vous pouvez parcourir la page PHP toohello que vous avez créé pour plus d’informations. Hello PHP page par exemple hello dans cet article est *http://lamp-vm.cloudapp.net/phpinfo.php*.

## <a name="additional-resources"></a>Ressources supplémentaires
Vous pouvez utiliser hello même toodeploy d’étapes de base des applications plus complexes. Dans cet exemple de script d’installation hello a été enregistré comme un objet blob public dans le stockage Azure. Une option plus sécurisée serait le script d’installation toostore hello en tant qu’objet blob sécurisé avec un [Signature d’accès sécurisé](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).

Ressources supplémentaires pour CLI d’Azure, Linux et hello CustomScript Extension sont décrits ci-dessous.

[Automatiser les tâches de personnalisation de machine virtuelle Linux à l’aide de l’extension CustomScript](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[Extensions Linux Azure (GitHub)](https://github.com/Azure/azure-linux-extensions)