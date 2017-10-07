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
# <a name="deploy-lamp-stack-with-hello-azure-cli-10"></a><span data-ttu-id="638f6-103">Déployer la pile LAMP avec hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="638f6-103">Deploy LAMP stack with hello Azure CLI 1.0</span></span>
<span data-ttu-id="638f6-104">Cet article vous guide tout au long de comment toodeploy un Apache web server, MySQL et PHP (pile de feu hello) sur Azure.</span><span class="sxs-lookup"><span data-stu-id="638f6-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="638f6-105">Vous avez besoin d’un compte Azure ([obtenir une évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/)) et hello [CLI d’Azure](../../cli-install-nodejs.md) qui est [connecté tooyour compte Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="638f6-105">You need an Azure Account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI](../../cli-install-nodejs.md) that is [connected tooyour Azure account](../../xplat-cli-connect.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="638f6-106">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="638f6-106">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="638f6-107">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="638f6-107">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="638f6-108">[Azure CLI 1.0] – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="638f6-108">[Azure CLI 1.0] – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="638f6-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="638f6-109">[Azure CLI 2.0](create-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

```
# One command toocreate a resource group holding a VM with LAMP already on it
$ azure group create -n uniqueResourceGroup -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json
```

* <span data-ttu-id="638f6-110">Déploiement de LAMP sur une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="638f6-110">Deploy LAMP on existing VM</span></span>

```
# Two commands: one updates packages, hello other installs Apache, MySQL, and PHP
user@ubuntu$ sudo apt-get update
user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="638f6-111">Procédure pas à pas de déploiement de LAMP sur une nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="638f6-111">Deploy LAMP on new VM walkthrough</span></span>
<span data-ttu-id="638f6-112">Vous pouvez commencer par créer un [groupe de ressources](../../azure-resource-manager/resource-group-overview.md) qui contiendra hello nouvelle machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="638f6-112">You can start by creating a [resource group](../../azure-resource-manager/resource-group-overview.md) that will contain hello new VM:</span></span>

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

<span data-ttu-id="638f6-113">toocreate hello machine virtuelle proprement dite, vous pouvez utiliser un modèle Azure Resource Manager déjà écrite [ici sur GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="638f6-113">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

    $ azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json uniqueResourceGroup uniqueLampName

<span data-ttu-id="638f6-114">Vous devez voir une réponse invitant l’utilisateur à renseigner certaines informations :</span><span class="sxs-lookup"><span data-stu-id="638f6-114">You should see a response prompting some more inputs:</span></span>

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

<span data-ttu-id="638f6-115">Vous avez maintenant créé une machine virtuelle Linux avec LAMP déjà installé.</span><span class="sxs-lookup"><span data-stu-id="638f6-115">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="638f6-116">Si vous le souhaitez, vous pouvez vérifier l’installation de hello en sautant trop bas[vérifier feu installé avec succès](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="638f6-116">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="638f6-117">Procédure pas à pas de déploiement de LAMP sur une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="638f6-117">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="638f6-118">Si vous avez besoin d’aide pour créer une VM Linux, vous pouvez head [toolearn ici comment toocreate un VM Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="638f6-118">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="638f6-119">Ensuite, vous devez tooSSH dans hello Linux VM.</span><span class="sxs-lookup"><span data-stu-id="638f6-119">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="638f6-120">Si vous avez besoin d’aide sur la création d’une clé SSH, vous pouvez head [toolearn ici comment toocreate une clé SSH sur Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="638f6-120">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="638f6-121">Si vous disposez déjà d’une clé SSH, continuez et ouvrez en ligne de commande une connexion SSH à votre machine virtuelle Linux avec `ssh exampleUsername@exampleDNS`.</span><span class="sxs-lookup"><span data-stu-id="638f6-121">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh exampleUsername@exampleDNS`.</span></span>

<span data-ttu-id="638f6-122">Maintenant que vous utilisez dans votre VM Linux, nous pouvons guider dans l’installation de la pile de feu hello sur les distributions Debian.</span><span class="sxs-lookup"><span data-stu-id="638f6-122">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="638f6-123">les commandes exactes Hello peuvent différer pour les autres versions de Linux.</span><span class="sxs-lookup"><span data-stu-id="638f6-123">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="638f6-124">Installation sur Debian/Ubuntu</span><span class="sxs-lookup"><span data-stu-id="638f6-124">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="638f6-125">Vous devez hello suivant des packages installés : `apache2`, `mysql-server`, `php5`, et `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="638f6-125">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="638f6-126">Vous pouvez les installer directement à partir de ces packages ou à l’aide de Tasksel.</span><span class="sxs-lookup"><span data-stu-id="638f6-126">You can install these packages by directly grabbing these packages or using Tasksel.</span></span> <span data-ttu-id="638f6-127">Les instructions pour les deux options figurent ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="638f6-127">Instructions for both options are listed below.</span></span>
<span data-ttu-id="638f6-128">Avant d’installer, vous devez toodownload et mettre à jour les listes de package.</span><span class="sxs-lookup"><span data-stu-id="638f6-128">Before installing you need toodownload and update package lists.</span></span>

    user@ubuntu$ sudo apt-get update

##### <a name="individual-packages"></a><span data-ttu-id="638f6-129">Packages individuels</span><span class="sxs-lookup"><span data-stu-id="638f6-129">Individual packages</span></span>
<span data-ttu-id="638f6-130">Utilisation d’apt-get :</span><span class="sxs-lookup"><span data-stu-id="638f6-130">Using apt-get:</span></span>

    user@ubuntu$ sudo apt-get install apache2 mysql-server php5 php5-mysql

##### <a name="using-tasksel"></a><span data-ttu-id="638f6-131">Utilisation de Tasksel</span><span class="sxs-lookup"><span data-stu-id="638f6-131">Using tasksel</span></span>
<span data-ttu-id="638f6-132">Vous pouvez également télécharger Tasksel, un outil Debian/Ubuntu qui installe plusieurs packages connexes en tant que tâche coordonnée sur votre système.</span><span class="sxs-lookup"><span data-stu-id="638f6-132">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

    user@ubuntu$ sudo apt-get install tasksel
    user@ubuntu$ sudo tasksel install lamp-server

<span data-ttu-id="638f6-133">Après l’exécution d’une des options précédentes de hello, vous allez être invité à tooinstall ces packages et divers autres dépendances.</span><span class="sxs-lookup"><span data-stu-id="638f6-133">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="638f6-134">Appuyez sur « y », puis sur 'Entrée' toocontinue et suivez les autres tooset demande un mot de passe d’administration pour MySQL.</span><span class="sxs-lookup"><span data-stu-id="638f6-134">Press 'y' and then 'Enter' toocontinue, and follow any other prompts tooset an administrative password for MySQL.</span></span> <span data-ttu-id="638f6-135">Cette commande installe hello minimale requise PHP les extensions nécessitées toouse PHP avec MySQL.</span><span class="sxs-lookup"><span data-stu-id="638f6-135">This installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="638f6-136">Exécutez hello suivant commande toosee autres extensions PHP disponibles sous forme de packages :</span><span class="sxs-lookup"><span data-stu-id="638f6-136">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

    user@ubuntu$ apt-cache search php5


#### <a name="create-infophp-document"></a><span data-ttu-id="638f6-137">Création d’un document info.php</span><span class="sxs-lookup"><span data-stu-id="638f6-137">Create info.php document</span></span>
<span data-ttu-id="638f6-138">Vous devez maintenant être en mesure de toocheck quelle version de PHP, MySQL et Apache vous avez via la ligne de commande hello en tapant `apache2 -v`, `mysql -v`, ou `php -v`.</span><span class="sxs-lookup"><span data-stu-id="638f6-138">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="638f6-139">Si vous devez comme tootest en outre, vous pouvez créer un tooview de page PHP info rapide dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="638f6-139">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="638f6-140">Créez un fichier avec l’éditeur de texte Nano à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="638f6-140">Create a file with Nano text editor with this command:</span></span>

    user@ubuntu$ sudo nano /var/www/html/info.php

<span data-ttu-id="638f6-141">Dans l’éditeur de texte hello GNU Nano, ajoutez hello lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="638f6-141">Within hello GNU Nano text editor, add hello following lines:</span></span>

    <?php
    phpinfo();
    ?>

<span data-ttu-id="638f6-142">Ensuite, enregistrez et quittez l’éditeur de texte hello.</span><span class="sxs-lookup"><span data-stu-id="638f6-142">Then save and exit hello text editor.</span></span>

<span data-ttu-id="638f6-143">Redémarrez Apache avec cette commande pour que toutes les nouvelles installations prennent effet.</span><span class="sxs-lookup"><span data-stu-id="638f6-143">Restart Apache with this command so all new installs take effect.</span></span>

    user@ubuntu$ sudo service apache2 restart

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="638f6-144">Vérification de l’installation correcte de LAMP</span><span class="sxs-lookup"><span data-stu-id="638f6-144">Verify LAMP successfully installed</span></span>
<span data-ttu-id="638f6-145">Vous pouvez maintenant vérifier vous avez créé en ouvrant un navigateur et allez toohttp://youruniqueDNS/info.php page des informations hello PHP.</span><span class="sxs-lookup"><span data-stu-id="638f6-145">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="638f6-146">Il doit se présenter une image toothis similaire.</span><span class="sxs-lookup"><span data-stu-id="638f6-146">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="638f6-147">Vous pouvez vérifier votre installation Apache en consultant hello Apache2 Ubuntu par défaut Page en accédant tooyou http://youruniqueDNS/.</span><span class="sxs-lookup"><span data-stu-id="638f6-147">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="638f6-148">Les informations suivantes s’affichent, comme sur cette image.</span><span class="sxs-lookup"><span data-stu-id="638f6-148">You should see something like this image.</span></span>

![][3]

<span data-ttu-id="638f6-149">Félicitations, vous avez configuré une pile LAMP sur votre machine virtuelle Azure !</span><span class="sxs-lookup"><span data-stu-id="638f6-149">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="638f6-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="638f6-150">Next steps</span></span>
<span data-ttu-id="638f6-151">Consultez hello documentation Ubuntu sur la pile de feu hello :</span><span class="sxs-lookup"><span data-stu-id="638f6-151">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="638f6-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="638f6-152">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png