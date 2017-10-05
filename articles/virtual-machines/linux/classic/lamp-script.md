---
title: "Utilisation de l’extension de script personnalisé sur une machine virtuelle Linux | Microsoft Docs"
description: "Apprenez à utiliser l’extension de script personnalisé Azure pour déployer des applications sur des machines virtuelles Linux dans Azure, créées à l’aide du modèle de déploiement classique."
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
ms.openlocfilehash: cb1fc9a44dc9e57d9cc9f1c546ad937d67e63c2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-a-lamp-app-using-the-azure-customscript-extension-for-linux"></a><span data-ttu-id="7118d-103">Déployer une application LAMP à l’aide de l’extension CustomScript Azure pour Linux</span><span class="sxs-lookup"><span data-stu-id="7118d-103">Deploy a LAMP app using the Azure CustomScript Extension for Linux</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="7118d-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7118d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7118d-105">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="7118d-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="7118d-106">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7118d-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="7118d-107">Pour plus d’informations sur le déploiement d’une pile LAMP à l’aide du modèle Resource Manager, suivez [ce lien](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7118d-107">For information about deploying a LAMP stack using the Resource Manager model, see [here](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="7118d-108">L’extension CustomScript Microsoft Azure pour Linux vous permet de personnaliser vos machines virtuelles en exécutant du code arbitraire écrit dans n’importe quel langage de script pris en charge par la machine virtuelle (par exemple Python et Bash).</span><span class="sxs-lookup"><span data-stu-id="7118d-108">The Microsoft Azure CustomScript Extension for Linux provides a way to customize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by the VM (for example, Python, and Bash).</span></span> <span data-ttu-id="7118d-109">Cela fournit un moyen très souple pour automatiser le déploiement d'application sur plusieurs machines.</span><span class="sxs-lookup"><span data-stu-id="7118d-109">This provides a very flexible way to automate application deployment to multiple machines.</span></span>

<span data-ttu-id="7118d-110">Vous pouvez déployer l’extension CustomScript à l’aide du Portail Azure, de Windows PowerShell ou de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="7118d-110">You can deploy the CustomScript Extension using the Azure portal, Windows PowerShell, or the Azure Command-Line Interface (Azure CLI).</span></span>

<span data-ttu-id="7118d-111">Dans cet article, nous allons utiliser l’interface de ligne de commande Azure pour déployer une machine virtuelle Ubuntu créée à l’aide du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="7118d-111">In this article we'll use the Azure CLI to deploy a simple LAMP application to an Ubuntu VM created using the classic deployment model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7118d-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7118d-112">Prerequisites</span></span>
<span data-ttu-id="7118d-113">Pour l’exemple suivant, créez d’abord deux machines virtuelles Azure exécutant Ubuntu 14.04 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7118d-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span></span> <span data-ttu-id="7118d-114">Ces machines virtuelles sont appelées *script-vm* et *lamp-vm*.</span><span class="sxs-lookup"><span data-stu-id="7118d-114">The VMs are called *script-vm* and *lamp-vm*.</span></span> <span data-ttu-id="7118d-115">Utilisez des noms uniques lorsque vous créez les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="7118d-115">Use unique names when you create the VMs.</span></span> <span data-ttu-id="7118d-116">L’une d’elles sert à exécuter les commandes de l’interface de ligne de commande, tandis que l’autre accueille l’application LAMP déployée.</span><span class="sxs-lookup"><span data-stu-id="7118d-116">One is used to run the CLI commands and one is used to deploy the LAMP app.</span></span>

<span data-ttu-id="7118d-117">Vous avez également besoin d’un compte Stockage Azure et d’une clé pour accéder à celui-ci (vous pouvez l’obtenir sur le Portail Azure).</span><span class="sxs-lookup"><span data-stu-id="7118d-117">You also need an Azure Storage account and a key to access it (you can get this from the Azure portal).</span></span>

<span data-ttu-id="7118d-118">Si vous avez besoin d’aide pour créer des machines virtuelles Linux sur Azure, reportez-vous à [Création d’une machine virtuelle exécutant Linux](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="7118d-118">If you need help creating Linux VMs on Azure refer to [Create a Virtual Machine Running Linux](createportal.md).</span></span>

<span data-ttu-id="7118d-119">Les commandes d’installation sont adaptées pour Ubuntu, mais vous pouvez adapter l’installation à n’importe quelle distribution Linux prise en charge.</span><span class="sxs-lookup"><span data-stu-id="7118d-119">The install commands assume Ubuntu, but you can adapt the installation for any supported Linux distro.</span></span>

<span data-ttu-id="7118d-120">La machine virtuelle script-vm doit disposer de l’interface de ligne de commande Azure, ainsi que d’une connexion opérationnelle à Azure.</span><span class="sxs-lookup"><span data-stu-id="7118d-120">The script-vm VM needs to have Azure CLI installed, with a working connection to Azure.</span></span> <span data-ttu-id="7118d-121">Pour obtenir de l’aide à ce sujet, reportez-vous à [Installation et configuration de l’interface de ligne de commande Microsoft Azure](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="7118d-121">For help with this refer to [Install and Configure the Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span>

## <a name="upload-a-script"></a><span data-ttu-id="7118d-122">Télécharger un script</span><span class="sxs-lookup"><span data-stu-id="7118d-122">Upload a script</span></span>
<span data-ttu-id="7118d-123">Nous allons utiliser l’extension de script personnalisé pour exécuter un script sur une machine virtuelle distante pour installer la pile LAMP et créer une page PHP.</span><span class="sxs-lookup"><span data-stu-id="7118d-123">We'll use the CustomScript Extension to run a script on a remote VM to install the LAMP stack and create a PHP page.</span></span> <span data-ttu-id="7118d-124">Pour accéder au script depuis n'importe où, nous allons le télécharger sous la forme d'un objet blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7118d-124">In order to access the script from anywhere we'll upload it as an Azure blob.</span></span>

### <a name="script-overview"></a><span data-ttu-id="7118d-125">Vue d’ensemble du script</span><span class="sxs-lookup"><span data-stu-id="7118d-125">Script overview</span></span>
<span data-ttu-id="7118d-126">L’exemple de script installe une pile LAMP sur Ubuntu (y compris la configuration d’une installation sans assistance de MySQL), écrit un simple fichier PHP et démarre Apache.</span><span class="sxs-lookup"><span data-stu-id="7118d-126">The script example installs a LAMP stack to Ubuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span></span>

    #!/bin/bash
    # set up a silent install of MySQL
    dbpass="mySQLPassw0rd"

    export DEBIAN_FRONTEND=noninteractive
    echo mysql-server-5.6 mysql-server/root_password password $dbpass | debconf-set-selections
    echo mysql-server-5.6 mysql-server/root_password_again password $dbpass | debconf-set-selections

    # install the LAMP stack
    apt-get -y install apache2 mysql-server php5 php5-mysql  

    # write some PHP
    echo \<center\>\<h1\>My Demo App\</h1\>\<br/\>\</center\> > /var/www/html/phpinfo.php
    echo \<\?php phpinfo\(\)\; \?\> >> /var/www/html/phpinfo.php

    # restart Apache
    apachectl restart

### <a name="upload-script"></a><span data-ttu-id="7118d-127">Télécharger le script</span><span class="sxs-lookup"><span data-stu-id="7118d-127">Upload script</span></span>
<span data-ttu-id="7118d-128">Enregistrez le script en tant que fichier texte, par exemple *install_lamp.sh*, puis téléchargez-le vers le service de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="7118d-128">Save the script as a text file, for example *install_lamp.sh*, and then upload it to Azure Storage.</span></span> <span data-ttu-id="7118d-129">Vous pouvez le faire facilement avec l’interface de ligne de commande Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7118d-129">You can do this easily with Azure CLI.</span></span> <span data-ttu-id="7118d-130">L'exemple suivant télécharge le fichier dans un conteneur de stockage nommé « scripts ».</span><span class="sxs-lookup"><span data-stu-id="7118d-130">The following example uploads the file to a storage container named "scripts".</span></span> <span data-ttu-id="7118d-131">Si le conteneur n'existe pas, vous devez d'abord le créer.</span><span class="sxs-lookup"><span data-stu-id="7118d-131">If the container doesn't exist you'll need to create it first.</span></span>

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

<span data-ttu-id="7118d-132">Créez également un fichier JSON qui décrit comment télécharger le script à partir d’Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7118d-132">Also create a JSON file that describes how to download the script from Azure Storage.</span></span> <span data-ttu-id="7118d-133">Enregistrez-le sous la forme *public_config.json* (en remplaçant « mystorage » par le nom de votre compte de stockage) :</span><span class="sxs-lookup"><span data-stu-id="7118d-133">Save this as *public_config.json* (replacing "mystorage" with the name of your storage account):</span></span>

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-the-extension"></a><span data-ttu-id="7118d-134">Déployer l’extension</span><span class="sxs-lookup"><span data-stu-id="7118d-134">Deploy the extension</span></span>
<span data-ttu-id="7118d-135">Vous pouvez maintenant utiliser la commande suivante pour déployer l’extension CustomScript Linux sur la machine virtuelle distante à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="7118d-135">Now you can use the next command to deploy the Linux CustomScript Extension to the remote VM using the Azure CLI.</span></span>

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

<span data-ttu-id="7118d-136">La commande précédente télécharge et exécute le script *install_lamp.sh* sur la machine virtuelle appelée *lamp-vm*.</span><span class="sxs-lookup"><span data-stu-id="7118d-136">The previous command downloads and runs the *install_lamp.sh* script on the VM called *lamp-vm*.</span></span>

<span data-ttu-id="7118d-137">Étant donné que l’application comprend un serveur web, n’oubliez pas d’ouvrir un port d’écoute HTTP sur la machine virtuelle distante avec la commande qui suit.</span><span class="sxs-lookup"><span data-stu-id="7118d-137">Since the app includes a web server, remember to open an HTTP listening port on the remote VM with the next command.</span></span>

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="7118d-138">Surveillance et dépannage</span><span class="sxs-lookup"><span data-stu-id="7118d-138">Monitoring and troubleshooting</span></span>
<span data-ttu-id="7118d-139">Vous pouvez vérifier l’exécution du script personnalisé en examinant le fichier journal sur la machine virtuelle distante.</span><span class="sxs-lookup"><span data-stu-id="7118d-139">You can check on how well the custom script runs by looking at the log file on the remote VM.</span></span> <span data-ttu-id="7118d-140">Établissez une connexion SSH à *lamp-vm* , puis affichez la dernière partie du fichier journal avec la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="7118d-140">SSH to *lamp-vm* and tail the log file with the next command.</span></span>

    cd /var/log/azure/customscript
    tail -f handler.log

<span data-ttu-id="7118d-141">Après avoir exécuté l’extension CustomScript, vous pouvez accéder à la page PHP que vous avez créée pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="7118d-141">After you run the CustomScript Extension, you can browse to the PHP page you created for information.</span></span> <span data-ttu-id="7118d-142">La page PHP pour l’exemple de cet article est *http://lamp-vm.cloudapp.net/phpinfo.php*.</span><span class="sxs-lookup"><span data-stu-id="7118d-142">The PHP page for the example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7118d-143">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="7118d-143">Additional resources</span></span>
<span data-ttu-id="7118d-144">Vous pouvez utiliser les mêmes étapes de base pour déployer des applications plus complexes.</span><span class="sxs-lookup"><span data-stu-id="7118d-144">You can use the same basic steps to deploy more complex apps.</span></span> <span data-ttu-id="7118d-145">Dans cet exemple, le script d'installation a été enregistré en tant qu'objet blob public dans Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="7118d-145">In this example the install script was saved as a public blob in Azure Storage.</span></span> <span data-ttu-id="7118d-146">Une option plus sécurisée consisterait à stocker le script d’installation sous la forme d’un objet blob sécurisé avec une [signature d’accès sécurisé](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span><span class="sxs-lookup"><span data-stu-id="7118d-146">A more secure option would be to store the install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span></span>

<span data-ttu-id="7118d-147">Voici quelques ressources supplémentaires pour l’interface de ligne de commande Azure, Linux et l’extension CustomScript.</span><span class="sxs-lookup"><span data-stu-id="7118d-147">Additional resources for Azure CLI, Linux and the CustomScript Extension are listed next.</span></span>

[<span data-ttu-id="7118d-148">Automatiser les tâches de personnalisation de machine virtuelle Linux à l’aide de l’extension CustomScript</span><span class="sxs-lookup"><span data-stu-id="7118d-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span></span>](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[<span data-ttu-id="7118d-149">Extensions Linux Azure (GitHub)</span><span class="sxs-lookup"><span data-stu-id="7118d-149">Azure Linux Extensions (GitHub)</span></span>](https://github.com/Azure/azure-linux-extensions)