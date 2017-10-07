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
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="2550c-103">Déploiement d’applications avec des modèles Azure Resource Manager pour les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="2550c-103">Application deployment with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="2550c-104">Une fois que toutes les exigences d’infrastructures Azure ont été identifiés et de traduire un modèle de déploiement, déploiement d’application réelle hello doit toobe adressé.</span><span class="sxs-lookup"><span data-stu-id="2550c-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, hello actual application deployment needs toobe addressed.</span></span> <span data-ttu-id="2550c-105">Déploiement d’application fait référence des fichiers binaires d’application réelle de hello tooinstalling sur les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="2550c-105">Application deployment here is referring tooinstalling hello actual application binaries onto Azure resources.</span></span> <span data-ttu-id="2550c-106">Pour un exemple de magasin de musique hello, .net Core, NGINX et superviseur doivent toobe installé et configuré sur chaque ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="2550c-106">For hello Music Store sample, .Net Core, NGINX, and Supervisor need toobe installed and configured on each virtual machine.</span></span> <span data-ttu-id="2550c-107">Bonjour magasin de musique binaires doivent toobe installé sur l’ordinateur virtuel de hello et hello de base de données du magasin de musique créé au préalable.</span><span class="sxs-lookup"><span data-stu-id="2550c-107">hello Music Store binaries need toobe installed onto hello virtual machine, and hello Music Store database pre-created.</span></span>

<span data-ttu-id="2550c-108">Ce document décrit en détail comment extensions de Machine virtuelle peuvent automatiser la configuration et déploiement tooAzure ordinateurs virtuels d’application.</span><span class="sxs-lookup"><span data-stu-id="2550c-108">This document details how Virtual Machine extensions can automate application deployment and configuration tooAzure virtual machines.</span></span> <span data-ttu-id="2550c-109">Toutes les dépendances et configurations uniques sont en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="2550c-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="2550c-110">Pour une expérience optimale de hello, préalable déployer une instance de hello solution tooyour abonnement Azure et de travail en même temps que le modèle de gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2550c-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="2550c-111">modèle complète de Hello se trouve ici : [déploiement du magasin de musique sur Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="2550c-111">hello complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="2550c-112">Script de configuration</span><span class="sxs-lookup"><span data-stu-id="2550c-112">Configuration script</span></span>
<span data-ttu-id="2550c-113">Extensions de Machine virtuelle sont des programmes spécialisés qui s’exécutent sur l’automatisation de machines virtuelles tooprovide configuration.</span><span class="sxs-lookup"><span data-stu-id="2550c-113">Virtual Machine extensions are specialized programs that execute against virtual machines tooprovide configuration automation.</span></span> <span data-ttu-id="2550c-114">Les extensions sont disponibles pour de nombreux objectifs spécifiques tels que la protection contre les virus, la configuration de la journalisation et la configuration de Docker.</span><span class="sxs-lookup"><span data-stu-id="2550c-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="2550c-115">Une extension de script personnalisé peut être utilisé toorun un script sur un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="2550c-115">A custom script extension can be used toorun any script against a virtual machine.</span></span> <span data-ttu-id="2550c-116">Exemple de magasin de musique hello, il est les machines virtuelles de toohello script personnalisé extension tooconfigure hello Ubuntu et installer l’application de magasin de musique hello.</span><span class="sxs-lookup"><span data-stu-id="2550c-116">With hello Music Store sample, it is up toohello custom script extension tooconfigure hello Ubuntu virtual machines and install hello Music Store application.</span></span> 

<span data-ttu-id="2550c-117">Avant indiquant comment les extensions de machine virtuelle sont déclarées dans un modèle Azure Resource Manager, examinez le script hello qui est exécuté.</span><span class="sxs-lookup"><span data-stu-id="2550c-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine hello script that is run.</span></span> <span data-ttu-id="2550c-118">Ce script configure la machine virtuelle d’Ubuntu Bonjour Bonjour toohost application de magasin de musique.</span><span class="sxs-lookup"><span data-stu-id="2550c-118">This script configures hello Ubuntu virtual machine toohost hello Music Store application.</span></span> <span data-ttu-id="2550c-119">Lors de l’exécution, le script de hello installe les logiciels requis de tous les installer l’application de magasin de musique hello à partir du contrôle de code source et préparer hello de base de données.</span><span class="sxs-lookup"><span data-stu-id="2550c-119">When run, hello script installs all needed software, install hello Music store application from source control, and prepare hello database.</span></span> 

<span data-ttu-id="2550c-120">application de base toolearn en savoir plus sur l’hébergement de .net sur Linux, consultez [environnement de production de publication tooa Linux](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span><span class="sxs-lookup"><span data-stu-id="2550c-120">toolearn more about hosting a .Net Core application on Linux, see [Publish tooa Linux production environment](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span></span>

> <span data-ttu-id="2550c-121">Cet exemple ne sert qu’à des fins de démonstration.</span><span class="sxs-lookup"><span data-stu-id="2550c-121">This sample is for demonstration purposes.</span></span>
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

## <a name="vm-script-extension"></a><span data-ttu-id="2550c-122">Extension de script de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="2550c-122">VM Script Extension</span></span>
<span data-ttu-id="2550c-123">Extensions de machine virtuelle peut être exécutées sur un ordinateur virtuel au moment de la génération en incluant la ressource d’extension hello dans le modèle de gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2550c-123">VM Extensions can be run against a virtual machine at build time by including hello extension resource in hello Azure Resource Manager template.</span></span> <span data-ttu-id="2550c-124">extension de Hello peut être ajoutée avec l’Assistant de Visual Studio ajouter une ressource hello, ou en insérant un JSON valide dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="2550c-124">hello extension can be added with hello Visual Studio Add Resource wizard, or by inserting valid JSON into hello template.</span></span> <span data-ttu-id="2550c-125">Hello ressource d’Extension de Script est imbriquée dans hello ressource d’ordinateur virtuel ; Ceci peut être observé dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="2550c-125">hello Script Extension resource is nested inside hello Virtual Machine resource; this can be seen in hello following example.</span></span>

<span data-ttu-id="2550c-126">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [Extension de Script de machine virtuelle](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span><span class="sxs-lookup"><span data-stu-id="2550c-126">Follow this link toosee hello JSON sample within hello Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span></span> 

<span data-ttu-id="2550c-127">Notez dans hello ci-dessous JSON qui hello script est stocké dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="2550c-127">Notice in hello below JSON that hello script is stored in GitHub.</span></span> <span data-ttu-id="2550c-128">Ce script pourrait également être stocké dans Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="2550c-128">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="2550c-129">Modèles Azure Resource Manager permettent également, tooconstructed de chaîne de l’exécution de script hello telles que les valeurs de paramètres de modèle peuvent être utilisées en tant que paramètres pour l’exécution du script.</span><span class="sxs-lookup"><span data-stu-id="2550c-129">Also, Azure Resource Manager templates allow hello script execution string tooconstructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="2550c-130">Dans ce cas les données sont fournies lors du déploiement de modèles de hello, et ces valeurs peuvent ensuite être utilisées lors de l’exécution du script de hello.</span><span class="sxs-lookup"><span data-stu-id="2550c-130">In this case data is provided when deploying hello templates, and these values can then be used when executing hello script.</span></span>

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

<span data-ttu-id="2550c-131">Pour plus d’informations sur l’utilisation d’extension de script personnalisé hello, consultez [extensions de script personnalisé avec les modèles de gestionnaire de ressources](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2550c-131">For more information on using hello custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="2550c-132">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="2550c-132">Next Step</span></span>
<hr>

[<span data-ttu-id="2550c-133">Découvrir d’autres modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2550c-133">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

