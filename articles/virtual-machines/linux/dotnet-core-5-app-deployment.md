---
title: "aaaAutomating déploiement d’applications avec les Extensions de Machine virtuelle | Documents Microsoft"
description: Didacticiel sur DotNet Core pour les machines virtuelles Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 9fc8b1ba-60f5-410b-8190-9f1ff885e50e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 38a02a4271d6b9ba02a473a51794a7bd90ca3a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a>Déploiement d’applications avec des modèles Azure Resource Manager pour les machines virtuelles Linux

Une fois que toutes les exigences d’infrastructures Azure ont été identifiés et de traduire un modèle de déploiement, déploiement d’application réelle hello doit toobe adressé. Déploiement d’application fait référence des fichiers binaires d’application réelle de hello tooinstalling sur les ressources Azure. Pour un exemple de magasin de musique hello, .net Core, NGINX et superviseur doivent toobe installé et configuré sur chaque ordinateur virtuel. Bonjour magasin de musique binaires doivent toobe installé sur l’ordinateur virtuel de hello et hello de base de données du magasin de musique créé au préalable.

Ce document décrit en détail comment extensions de Machine virtuelle peuvent automatiser la configuration et déploiement tooAzure ordinateurs virtuels d’application. Toutes les dépendances et configurations uniques sont en surbrillance. Pour une expérience optimale de hello, préalable déployer une instance de hello solution tooyour abonnement Azure et de travail en même temps que le modèle de gestionnaire de ressources Azure hello. modèle complète de Hello se trouve ici : [déploiement du magasin de musique sur Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

## <a name="configuration-script"></a>Script de configuration
Extensions de Machine virtuelle sont des programmes spécialisés qui s’exécutent sur l’automatisation de machines virtuelles tooprovide configuration. Les extensions sont disponibles pour de nombreux objectifs spécifiques tels que la protection contre les virus, la configuration de la journalisation et la configuration de Docker. Une extension de script personnalisé peut être utilisé toorun un script sur un ordinateur virtuel. Exemple de magasin de musique hello, il est les machines virtuelles de toohello script personnalisé extension tooconfigure hello Ubuntu et installer l’application de magasin de musique hello. 

Avant indiquant comment les extensions de machine virtuelle sont déclarées dans un modèle Azure Resource Manager, examinez le script hello qui est exécuté. Ce script configure la machine virtuelle d’Ubuntu Bonjour Bonjour toohost application de magasin de musique. Lors de l’exécution, le script de hello installe les logiciels requis de tous les installer l’application de magasin de musique hello à partir du contrôle de code source et préparer hello de base de données. 

application de base toolearn en savoir plus sur l’hébergement de .net sur Linux, consultez [environnement de production de publication tooa Linux](https://docs.asp.net/en/latest/publishing/linuxproduction.html).

> Cet exemple ne sert qu’à des fins de démonstration.
> 
> 

```bash
#!/bin/bash

# install dotnet core
sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'
sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
sudo apt-get update
sudo apt-get install -y dotnet-dev-1.0.0-preview2-003121

# download application
sudo wget https://raw.github.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/music-store-azure-demo-pub.tar /
sudo mkdir /opt/music
sudo tar -xf music-store-azure-demo-pub.tar -C /opt/music

# install nginx, update config file
sudo apt-get install -y nginx
sudo service nginx start
sudo touch /etc/nginx/sites-available/default
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/nginx-config/default -O /etc/nginx/sites-available/default
sudo cp /opt/music/nginx-config/default /etc/nginx/sites-available/
sudo nginx -s reload

# update and secure music config file
sed -i "s/<replaceserver>/$1/g" /opt/music/config.json
sed -i "s/<replaceuser>/$2/g" /opt/music/config.json
sed -i "s/<replacepass>/$3/g" /opt/music/config.json
sudo chown $2 /opt/music/config.json
sudo chmod 0400 /opt/music/config.json

# config supervisor
sudo apt-get install -y supervisor
sudo touch /etc/supervisor/conf.d/music.conf
sudo wget https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/music-app/supervisor/music.conf -O /etc/supervisor/conf.d/music.conf
sudo service supervisor stop
sudo service supervisor start

# pre-create music store database
/usr/bin/dotnet /opt/music/MusicStore.dll &
```

## <a name="vm-script-extension"></a>Extension de script de machine virtuelle
Extensions de machine virtuelle peut être exécutées sur un ordinateur virtuel au moment de la génération en incluant la ressource d’extension hello dans le modèle de gestionnaire de ressources Azure hello. extension de Hello peut être ajoutée avec l’Assistant de Visual Studio ajouter une ressource hello, ou en insérant un JSON valide dans le modèle de hello. Hello ressource d’Extension de Script est imbriquée dans hello ressource d’ordinateur virtuel ; Ceci peut être observé dans hello l’exemple suivant.

Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [Extension de Script de machine virtuelle](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359). 

Notez dans hello ci-dessous JSON qui hello script est stocké dans GitHub. Ce script pourrait également être stocké dans Stockage Blob Azure. Modèles Azure Resource Manager permettent également, tooconstructed de chaîne de l’exécution de script hello telles que les valeurs de paramètres de modèle peuvent être utilisées en tant que paramètres pour l’exécution du script. Dans ce cas les données sont fournies lors du déploiement de modèles de hello, et ces valeurs peuvent ensuite être utilisées lors de l’exécution du script de hello.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

Pour plus d’informations sur l’utilisation d’extension de script personnalisé hello, consultez [extensions de script personnalisé avec les modèles de gestionnaire de ressources](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="next-step"></a>Étape suivante
<hr>

[Découvrir d’autres modèles Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates)

