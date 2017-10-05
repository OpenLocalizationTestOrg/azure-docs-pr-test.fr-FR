---
title: "Automatisation du déploiement d’application avec des extensions de machine virtuelle | Microsoft Docs"
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
ms.openlocfilehash: 2f972fef75aa8e13af7dab908c2b0e2ec28f1324
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-linux-vms"></a><span data-ttu-id="a589b-103">Déploiement d’applications avec des modèles Azure Resource Manager pour les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="a589b-103">Application deployment with Azure Resource Manager templates for Linux VMs</span></span>

<span data-ttu-id="a589b-104">Une fois que toutes les exigences infrastructurelles d’Azure sont identifiées et converties en un modèle de déploiement, le déploiement de l’application réelle doit être effectué.</span><span class="sxs-lookup"><span data-stu-id="a589b-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, the actual application deployment needs to be addressed.</span></span> <span data-ttu-id="a589b-105">Le déploiement de l’application fait ici référence à l’installation des fichiers binaires de l’application réelle sur les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="a589b-105">Application deployment here is referring to installing the actual application binaries onto Azure resources.</span></span> <span data-ttu-id="a589b-106">Pour l’exemple du Store musique, .NET Core, NGINX et Superviseur doivent être installés et configurés sur chaque machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a589b-106">For the Music Store sample, .Net Core, NGINX, and Supervisor need to be installed and configured on each virtual machine.</span></span> <span data-ttu-id="a589b-107">Les fichiers binaires du Store musique doivent être installés sur la machine virtuelle, et la base de données du Store musique doit avoir été créée au préalable.</span><span class="sxs-lookup"><span data-stu-id="a589b-107">The Music Store binaries need to be installed onto the virtual machine, and the Music Store database pre-created.</span></span>

<span data-ttu-id="a589b-108">Ce document décrit en détail comment des extensions de machine virtuelle peuvent automatiser le déploiement et la configuration d’applications sur des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="a589b-108">This document details how Virtual Machine extensions can automate application deployment and configuration to Azure virtual machines.</span></span> <span data-ttu-id="a589b-109">Toutes les dépendances et configurations uniques sont en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="a589b-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="a589b-110">Pour optimiser l’expérience, prédéployez une instance de la solution sur votre abonnement Azure et travaillez avec le modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a589b-110">For the best experience, pre-deploy an instance of the solution to your Azure subscription and work along with the Azure Resource Manager template.</span></span> <span data-ttu-id="a589b-111">Pour le modèle complet, consultez [Déploiement du Store musique sur Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="a589b-111">The complete template can be found here – [Music Store Deployment on Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="a589b-112">Script de configuration</span><span class="sxs-lookup"><span data-stu-id="a589b-112">Configuration script</span></span>
<span data-ttu-id="a589b-113">Les extensions de machine virtuelle sont des programmes spécialisés qui s’exécutent sur des machines virtuelles pour automatiser la configuration.</span><span class="sxs-lookup"><span data-stu-id="a589b-113">Virtual Machine extensions are specialized programs that execute against virtual machines to provide configuration automation.</span></span> <span data-ttu-id="a589b-114">Les extensions sont disponibles pour de nombreux objectifs spécifiques tels que la protection contre les virus, la configuration de la journalisation et la configuration de Docker.</span><span class="sxs-lookup"><span data-stu-id="a589b-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="a589b-115">Une extension de script personnalisé peut être utilisée pour exécuter un script sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a589b-115">A custom script extension can be used to run any script against a virtual machine.</span></span> <span data-ttu-id="a589b-116">Avec l’exemple du Store musique, l’extension de script personnalisé doit configurer les machines virtuelles Ubuntu et installer l’application du Store musique.</span><span class="sxs-lookup"><span data-stu-id="a589b-116">With the Music Store sample, it is up to the custom script extension to configure the Ubuntu virtual machines and install the Music Store application.</span></span> 

<span data-ttu-id="a589b-117">Avant de détailler la manière dont les extensions de machine virtuelle sont déclarées dans un modèle Azure Resource Manager, examinez le script exécuté.</span><span class="sxs-lookup"><span data-stu-id="a589b-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine the script that is run.</span></span> <span data-ttu-id="a589b-118">Celui-ci configure la machine virtuelle Linux Ubuntu pour héberger l’application du Store musique.</span><span class="sxs-lookup"><span data-stu-id="a589b-118">This script configures the Ubuntu virtual machine to host the Music Store application.</span></span> <span data-ttu-id="a589b-119">Lors de son exécution, le script installe tous les logiciels nécessaires, installe l’application du Store musique à partir du contrôle de code source et prépare la base de données.</span><span class="sxs-lookup"><span data-stu-id="a589b-119">When run, the script installs all needed software, install the Music store application from source control, and prepare the database.</span></span> 

<span data-ttu-id="a589b-120">Pour plus d’informations sur l’hébergement d’une application .NET Core sur Linux, consultez [Publier dans un environnement de production Linux](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span><span class="sxs-lookup"><span data-stu-id="a589b-120">To learn more about hosting a .Net Core application on Linux, see [Publish to a Linux production environment](https://docs.asp.net/en/latest/publishing/linuxproduction.html).</span></span>

> <span data-ttu-id="a589b-121">Cet exemple ne sert qu’à des fins de démonstration.</span><span class="sxs-lookup"><span data-stu-id="a589b-121">This sample is for demonstration purposes.</span></span>
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

## <a name="vm-script-extension"></a><span data-ttu-id="a589b-122">Extension de script de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="a589b-122">VM Script Extension</span></span>
<span data-ttu-id="a589b-123">Les extensions de machine virtuelle peuvent être exécutées sur une machine virtuelle au moment de sa génération en incluant la ressource d’extension dans le modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a589b-123">VM Extensions can be run against a virtual machine at build time by including the extension resource in the Azure Resource Manager template.</span></span> <span data-ttu-id="a589b-124">L’extension peut être ajoutée avec l’Assistant Ajouter une ressource de Visual Studio, ou en insérant un JSON valide dans le modèle.</span><span class="sxs-lookup"><span data-stu-id="a589b-124">The extension can be added with the Visual Studio Add Resource wizard, or by inserting valid JSON into the template.</span></span> <span data-ttu-id="a589b-125">La ressource d’extension de script est imbriquée dans la ressource de machine virtuelle, comme le montre l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="a589b-125">The Script Extension resource is nested inside the Virtual Machine resource; this can be seen in the following example.</span></span>

<span data-ttu-id="a589b-126">Pour voir l’exemple JSON dans le modèle Resource Manager, suivez ce lien : [Extension de script de machine virtuelle](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span><span class="sxs-lookup"><span data-stu-id="a589b-126">Follow this link to see the JSON sample within the Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L359).</span></span> 

<span data-ttu-id="a589b-127">Notez que, dans le JSON ci-dessous, le script est stocké dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="a589b-127">Notice in the below JSON that the script is stored in GitHub.</span></span> <span data-ttu-id="a589b-128">Ce script pourrait également être stocké dans Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="a589b-128">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="a589b-129">De même, les modèles Azure Resource Manager permettent de construire la chaîne d’exécution du script de façon à ce que les valeurs des paramètres du modèle puissent être utilisées en tant que paramètres pour l’exécution du script.</span><span class="sxs-lookup"><span data-stu-id="a589b-129">Also, Azure Resource Manager templates allow the script execution string to constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="a589b-130">Dans ce cas, des données sont fournies lors du déploiement des modèles et ces valeurs peuvent ensuite être utilisées lors de l’exécution du script.</span><span class="sxs-lookup"><span data-stu-id="a589b-130">In this case data is provided when deploying the templates, and these values can then be used when executing the script.</span></span>

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

<span data-ttu-id="a589b-131">Pour plus d’informations sur l’utilisation des extensions de script personnalisé, consultez [Extensions de script personnalisé avec des modèles Resource Manager](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a589b-131">For more information on using the custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="a589b-132">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="a589b-132">Next Step</span></span>
<hr>

[<span data-ttu-id="a589b-133">Découvrir d’autres modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a589b-133">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

