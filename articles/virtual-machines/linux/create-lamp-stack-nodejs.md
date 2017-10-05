---
title: "Déployer LAMP sur une machine virtuelle Linux avec Azure CLI 1.0 | Microsoft Docs"
description: "Découvrez comment installer la pile LAMP sur une machine virtuelle Linux dans Azure"
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
ms.openlocfilehash: feba2fb20d1831e92358ff5d1b4c9589d63d28dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-lamp-stack-with-the-azure-cli-10"></a><span data-ttu-id="f0e22-103">Déployer la pile LAMP avec Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="f0e22-103">Deploy LAMP stack with the Azure CLI 1.0</span></span>
<span data-ttu-id="f0e22-104">Cet article vous guide à travers le déploiement d’un serveur web Apache, de MySQL et de PHP (la pile LAMP) sur Azure.</span><span class="sxs-lookup"><span data-stu-id="f0e22-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on Azure.</span></span> <span data-ttu-id="f0e22-105">Vous aurez besoin d’un compte Azure ([obtenir un essai gratuit](https://azure.microsoft.com/pricing/free-trial/)) et de [l’interface de ligne de commande Azure](../../cli-install-nodejs.md) [connectée à votre compte Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="f0e22-105">You need an Azure Account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and the [Azure CLI](../../cli-install-nodejs.md) that is [connected to your Azure account](../../xplat-cli-connect.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="f0e22-106">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="f0e22-106">CLI versions to complete the task</span></span>
<span data-ttu-id="f0e22-107">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="f0e22-107">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="f0e22-108">[Azure CLI 1.0] : notre interface de ligne de commande pour les modèles de déploiement Classic et Resource Manager (cet article)</span><span class="sxs-lookup"><span data-stu-id="f0e22-108">[Azure CLI 1.0] – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="f0e22-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) : notre interface de ligne de commande nouvelle génération pour le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f0e22-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

```
# One command to create a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* <span data-ttu-id="f0e22-110">Déploiement de LAMP sur une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="f0e22-110">Deploy LAMP on existing VM</span></span>

```
# Two commands: one updates packages, the other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="f0e22-111">Procédure pas à pas de déploiement de LAMP sur une nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f0e22-111">Deploy LAMP on new VM walkthrough</span></span>
<span data-ttu-id="f0e22-112">Vous pouvez commencer par créer un [groupe de ressources](../../azure-resource-manager/resource-group-overview.md) qui contient la nouvelle machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="f0e22-112">You can start by creating a [resource group](../../azure-resource-manager/resource-group-overview.md) that will contain the new VM:</span></span>

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

<span data-ttu-id="f0e22-113">Pour créer la machine virtuelle elle-même, vous pouvez utiliser un modèle Azure Resource Manager déjà écrit [ici sur GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="f0e22-113">To create the VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

<span data-ttu-id="f0e22-114">Vous devez voir une réponse invitant l’utilisateur à renseigner certaines informations :</span><span class="sxs-lookup"><span data-stu-id="f0e22-114">You should see a response prompting some more inputs:</span></span>

    info:    Executing command group deployment create
    info:    Supply values for the following parameters
    storageAccountNamePrefix: lampprefix
    location: westus
    adminUsername: someUsername
    adminPassword: somePassword
    mySqlPassword: somePassword
    dnsLabelPrefix: azlamptest
    info:    Initializing template configurations and parameters
    info:    Creating a deployment
    info:    Created template deployment "uniqueLampName"
    info:    Waiting for deployment to complete
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

<span data-ttu-id="f0e22-115">Vous avez maintenant créé une machine virtuelle Linux avec LAMP déjà installé.</span><span class="sxs-lookup"><span data-stu-id="f0e22-115">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="f0e22-116">Si vous le souhaitez, vous pouvez vérifier l’installation en accédant à la section [Vérification de l’installation correcte de LAMP](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="f0e22-116">If you wish, you can verify the install by jumping down to [Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="f0e22-117">Procédure pas à pas de déploiement de LAMP sur une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="f0e22-117">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="f0e22-118">Si vous avez besoin d’aide pour créer une machine virtuelle Linux, vous pouvez vous rendre [ici pour apprendre à créer une machine virtuelle Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f0e22-118">If you need help creating a Linux VM, you can head [here to learn how to create a Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="f0e22-119">Ensuite, vous devez intégrer SSH à la machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="f0e22-119">Next, you need to SSH into the Linux VM.</span></span> <span data-ttu-id="f0e22-120">Si vous avez besoin d’aide pour créer une clé SSH, vous pouvez vous rendre [ici pour apprendre à créer une clé SSH sous Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f0e22-120">If you need help with creating an SSH key, you can head [here to learn how to create an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="f0e22-121">Si vous disposez déjà d’une clé SSH, continuez et ouvrez en ligne de commande une connexion SSH à votre machine virtuelle Linux avec `ssh exampleUsername@exampleDNS`.</span><span class="sxs-lookup"><span data-stu-id="f0e22-121">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh exampleUsername@exampleDNS`.</span></span>

<span data-ttu-id="f0e22-122">Maintenant que vous travaillez dans votre machine virtuelle Linux, nous allons étudier l’installation de la pile LAMP sur des distributions Debian.</span><span class="sxs-lookup"><span data-stu-id="f0e22-122">Now that you are working within your Linux VM, we can walk through installing the LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="f0e22-123">Les commandes exactes peuvent varier pour les autres distributions Linux.</span><span class="sxs-lookup"><span data-stu-id="f0e22-123">The exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="f0e22-124">Installation sur Debian/Ubuntu</span><span class="sxs-lookup"><span data-stu-id="f0e22-124">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="f0e22-125">Les packages suivants doivent être installés : `apache2`, `mysql-server`, `php5` et `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="f0e22-125">You need the following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="f0e22-126">Vous pouvez les installer directement à partir de ces packages ou à l’aide de Tasksel.</span><span class="sxs-lookup"><span data-stu-id="f0e22-126">You can install these packages by directly grabbing these packages or using Tasksel.</span></span> <span data-ttu-id="f0e22-127">Les instructions pour les deux options figurent ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f0e22-127">Instructions for both options are listed below.</span></span>
<span data-ttu-id="f0e22-128">Avant de procéder à l’installation, vous devez télécharger et mettre à jour les listes de packages.</span><span class="sxs-lookup"><span data-stu-id="f0e22-128">Before installing you need to download and update package lists.</span></span>

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a><span data-ttu-id="f0e22-129">Packages individuels</span><span class="sxs-lookup"><span data-stu-id="f0e22-129">Individual packages</span></span>
<span data-ttu-id="f0e22-130">Utilisation d’apt-get :</span><span class="sxs-lookup"><span data-stu-id="f0e22-130">Using apt-get:</span></span>

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a><span data-ttu-id="f0e22-131">Utilisation de Tasksel</span><span class="sxs-lookup"><span data-stu-id="f0e22-131">Using tasksel</span></span>
<span data-ttu-id="f0e22-132">Vous pouvez également télécharger Tasksel, un outil Debian/Ubuntu qui installe plusieurs packages connexes en tant que tâche coordonnée sur votre système.</span><span class="sxs-lookup"><span data-stu-id="f0e22-132">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

<span data-ttu-id="f0e22-133">Après avoir exécuté l’une des options précédentes, vous serez invité à installer ces packages et d’autres dépendances.</span><span class="sxs-lookup"><span data-stu-id="f0e22-133">After running either of the previous options, you will be prompted to install these packages and various other dependencies.</span></span> <span data-ttu-id="f0e22-134">Appuyez sur « y » puis « Entrée » pour continuer et suivez les indications des invites pour définir un mot de passe d'administration pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="f0e22-134">Press 'y' and then 'Enter' to continue, and follow any other prompts to set an administrative password for MySQL.</span></span> <span data-ttu-id="f0e22-135">Cette action installe les extensions PHP minimales requises pour utiliser PHP avec MySQL.</span><span class="sxs-lookup"><span data-stu-id="f0e22-135">This installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="f0e22-136">Exécutez les commandes suivantes pour voir les autres extensions PHP disponibles sous forme de packages :</span><span class="sxs-lookup"><span data-stu-id="f0e22-136">Run the following command to see other PHP extensions that are available as packages:</span></span>

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a><span data-ttu-id="f0e22-137">Création d’un document info.php</span><span class="sxs-lookup"><span data-stu-id="f0e22-137">Create info.php document</span></span>
<span data-ttu-id="f0e22-138">Vous devez maintenant être en mesure de vérifier la version d’Apache, de MySQL et de PHP figurant dans la ligne de commande en tapant `apache2 -v`, `mysql -v` ou `php -v`.</span><span class="sxs-lookup"><span data-stu-id="f0e22-138">You should now be able to check what version of Apache, MySQL, and PHP you have through the command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="f0e22-139">Si vous souhaitez poursuivre le test, vous pouvez créer une page d’informations PHP rapide à afficher dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="f0e22-139">If you would like to test further, you can create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="f0e22-140">Créez un fichier avec l’éditeur de texte Nano à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f0e22-140">Create a file with Nano text editor with this command:</span></span>

    user@ubuntu$ sudo nano /var/www/html/info.php

<span data-ttu-id="f0e22-141">Dans l’éditeur de texte GNU Nano, ajoutez les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f0e22-141">Within the GNU Nano text editor, add the following lines:</span></span>

    <?php
    phpinfo();
    ?>

<span data-ttu-id="f0e22-142">Enregistrez ensuite votre travail et quittez l’éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="f0e22-142">Then save and exit the text editor.</span></span>

<span data-ttu-id="f0e22-143">Redémarrez Apache avec cette commande pour que toutes les nouvelles installations prennent effet.</span><span class="sxs-lookup"><span data-stu-id="f0e22-143">Restart Apache with this command so all new installs take effect.</span></span>

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="f0e22-144">Vérification de l’installation correcte de LAMP</span><span class="sxs-lookup"><span data-stu-id="f0e22-144">Verify LAMP successfully installed</span></span>
<span data-ttu-id="f0e22-145">Vous pouvez maintenant consulter la page d’informations PHP que vous avez créée en ouvrant un navigateur et en accédant à http://votreDNSunique/info.php.</span><span class="sxs-lookup"><span data-stu-id="f0e22-145">Now you can check the PHP info page you created by opening a browser and going to http://youruniqueDNS/info.php.</span></span> <span data-ttu-id="f0e22-146">Elle doit ressembler à cette image.</span><span class="sxs-lookup"><span data-stu-id="f0e22-146">It should look similar to this image.</span></span>

![][2]

<span data-ttu-id="f0e22-147">Vous pouvez vérifier votre installation Apache en consultant la page par défaut d’Ubuntu Apache2 en accédant à http://votreDNSunique/.</span><span class="sxs-lookup"><span data-stu-id="f0e22-147">You can check your Apache installation by viewing the Apache2 Ubuntu Default Page by going to you http://youruniqueDNS/.</span></span> <span data-ttu-id="f0e22-148">Les informations suivantes s’affichent, comme sur cette image.</span><span class="sxs-lookup"><span data-stu-id="f0e22-148">You should see something like this image.</span></span>

![][3]

<span data-ttu-id="f0e22-149">Félicitations, vous avez configuré une pile LAMP sur votre machine virtuelle Azure !</span><span class="sxs-lookup"><span data-stu-id="f0e22-149">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0e22-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f0e22-150">Next steps</span></span>
<span data-ttu-id="f0e22-151">Consultez la documentation Ubuntu sur la pile LAMP :</span><span class="sxs-lookup"><span data-stu-id="f0e22-151">Check out the Ubuntu documentation on the LAMP stack:</span></span>

* [<span data-ttu-id="f0e22-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="f0e22-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png