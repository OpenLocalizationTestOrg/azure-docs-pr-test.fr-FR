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
# <a name="deploy-a-lamp-app-using-hello-azure-customscript-extension-for-linux"></a><span data-ttu-id="3b31e-103">Déployer une application de feu à l’aide de hello CustomScript Extension de Azure pour Linux</span><span class="sxs-lookup"><span data-stu-id="3b31e-103">Deploy a LAMP app using hello Azure CustomScript Extension for Linux</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="3b31e-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3b31e-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3b31e-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="3b31e-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="3b31e-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="3b31e-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="3b31e-107">Pour plus d’informations sur le déploiement d’une pile LAMP à l’aide du modèle de gestionnaire de ressources hello, consultez [ici](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3b31e-107">For information about deploying a LAMP stack using hello Resource Manager model, see [here](../tutorial-lamp-stack.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="3b31e-108">Hello CustomScript Extension de Microsoft Azure pour Linux fournit un moyen toocustomize vos machines virtuelles (VM) en exécutant du code arbitraire écrit dans n’importe quel langage de script pris en charge par hello machine virtuelle (par exemple, Python et un interpréteur de commandes).</span><span class="sxs-lookup"><span data-stu-id="3b31e-108">hello Microsoft Azure CustomScript Extension for Linux provides a way toocustomize your virtual machines (VMs) by running arbitrary code written in any scripting language supported by hello VM (for example, Python, and Bash).</span></span> <span data-ttu-id="3b31e-109">Cela fournit un tooautomate de manière très flexible des ordinateurs de toomultiple de déploiement d’application.</span><span class="sxs-lookup"><span data-stu-id="3b31e-109">This provides a very flexible way tooautomate application deployment toomultiple machines.</span></span>

<span data-ttu-id="3b31e-110">Vous pouvez déployer hello CustomScript Extension à l’aide de hello portail Azure, Windows PowerShell ou hello Azure Interface de ligne (Azure).</span><span class="sxs-lookup"><span data-stu-id="3b31e-110">You can deploy hello CustomScript Extension using hello Azure portal, Windows PowerShell, or hello Azure Command-Line Interface (Azure CLI).</span></span>

<span data-ttu-id="3b31e-111">Dans cet article, nous allons utiliser hello CLI d’Azure toodeploy un tooan d’application simple feu Ubuntu VM créé à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="3b31e-111">In this article we'll use hello Azure CLI toodeploy a simple LAMP application tooan Ubuntu VM created using hello classic deployment model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b31e-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3b31e-112">Prerequisites</span></span>
<span data-ttu-id="3b31e-113">Pour l’exemple suivant, créez d’abord deux machines virtuelles Azure exécutant Ubuntu 14.04 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3b31e-113">For this example, first create two Azure VMs running Ubuntu 14.04 or later.</span></span> <span data-ttu-id="3b31e-114">Hello machines virtuelles sont appelées *script-vm* et *feu-vm*.</span><span class="sxs-lookup"><span data-stu-id="3b31e-114">hello VMs are called *script-vm* and *lamp-vm*.</span></span> <span data-ttu-id="3b31e-115">Utilisez des noms uniques lorsque vous créez des machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="3b31e-115">Use unique names when you create hello VMs.</span></span> <span data-ttu-id="3b31e-116">Un les commandes CLI utilisée toorun hello et l’autre application de feu hello toodeploy utilisé.</span><span class="sxs-lookup"><span data-stu-id="3b31e-116">One is used toorun hello CLI commands and one is used toodeploy hello LAMP app.</span></span>

<span data-ttu-id="3b31e-117">Vous devez également un compte de stockage Azure et une clé tooaccess informatique (vous pouvez obtenir cette information à partir de hello portail Azure).</span><span class="sxs-lookup"><span data-stu-id="3b31e-117">You also need an Azure Storage account and a key tooaccess it (you can get this from hello Azure portal).</span></span>

<span data-ttu-id="3b31e-118">Si vous avez besoin d’aide pour créer des machines virtuelles Linux sur Azure, consultez trop[créer une Machine virtuelle exécutant Linux](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="3b31e-118">If you need help creating Linux VMs on Azure refer too[Create a Virtual Machine Running Linux](createportal.md).</span></span>

<span data-ttu-id="3b31e-119">commandes d’installation Hello supposent Ubuntu, mais vous pouvez adapter les installation hello pour tout pris en charge la distribution de Linux.</span><span class="sxs-lookup"><span data-stu-id="3b31e-119">hello install commands assume Ubuntu, but you can adapt hello installation for any supported Linux distro.</span></span>

<span data-ttu-id="3b31e-120">Hello machine virtuelle de script-vm doit toohave que CLI d’Azure installé, avec un tooAzure de connexion du travail.</span><span class="sxs-lookup"><span data-stu-id="3b31e-120">hello script-vm VM needs toohave Azure CLI installed, with a working connection tooAzure.</span></span> <span data-ttu-id="3b31e-121">Pour plus d’informations, consultez trop[installer et configurer hello Interface de ligne de commande Azure](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3b31e-121">For help with this refer too[Install and Configure hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span>

## <a name="upload-a-script"></a><span data-ttu-id="3b31e-122">Télécharger un script</span><span class="sxs-lookup"><span data-stu-id="3b31e-122">Upload a script</span></span>
<span data-ttu-id="3b31e-123">Nous allons utiliser hello CustomScript Extension toorun un script sur une pile de feu VM tooinstall hello à distance et créer une page PHP.</span><span class="sxs-lookup"><span data-stu-id="3b31e-123">We'll use hello CustomScript Extension toorun a script on a remote VM tooinstall hello LAMP stack and create a PHP page.</span></span> <span data-ttu-id="3b31e-124">Dans le script de hello ordre tooaccess depuis n’importe où nous allons télécharger sous la forme d’un objet blob Azure.</span><span class="sxs-lookup"><span data-stu-id="3b31e-124">In order tooaccess hello script from anywhere we'll upload it as an Azure blob.</span></span>

### <a name="script-overview"></a><span data-ttu-id="3b31e-125">Vue d’ensemble du script</span><span class="sxs-lookup"><span data-stu-id="3b31e-125">Script overview</span></span>
<span data-ttu-id="3b31e-126">exemple de script Hello installe un tooUbuntu de pile LAMP (y compris la configuration d’une installation silencieuse de MySQL), écrit un simple fichier PHP et démarre Apache.</span><span class="sxs-lookup"><span data-stu-id="3b31e-126">hello script example installs a LAMP stack tooUbuntu (including setting up a silent install of MySQL), writes a simple PHP file, and starts Apache.</span></span>

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

### <a name="upload-script"></a><span data-ttu-id="3b31e-127">Télécharger le script</span><span class="sxs-lookup"><span data-stu-id="3b31e-127">Upload script</span></span>
<span data-ttu-id="3b31e-128">Enregistrer le script de hello dans un fichier texte, par exemple *install_lamp.sh*, puis téléchargez tooAzure stockage.</span><span class="sxs-lookup"><span data-stu-id="3b31e-128">Save hello script as a text file, for example *install_lamp.sh*, and then upload it tooAzure Storage.</span></span> <span data-ttu-id="3b31e-129">Vous pouvez le faire facilement avec l’interface de ligne de commande Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3b31e-129">You can do this easily with Azure CLI.</span></span> <span data-ttu-id="3b31e-130">Hello exemple suivant télécharge conteneur de stockage hello fichier tooa nommé « scripts ».</span><span class="sxs-lookup"><span data-stu-id="3b31e-130">hello following example uploads hello file tooa storage container named "scripts".</span></span> <span data-ttu-id="3b31e-131">Si le conteneur de hello n’existe pas, vous devez toocreate il premier.</span><span class="sxs-lookup"><span data-stu-id="3b31e-131">If hello container doesn't exist you'll need toocreate it first.</span></span>

    azure storage blob upload -a <yourStorageAccountName> -k <yourStorageKey> --container scripts ./install_lamp.sh

<span data-ttu-id="3b31e-132">Également créer un fichier JSON qui décrit comment toodownload hello script depuis le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3b31e-132">Also create a JSON file that describes how toodownload hello script from Azure Storage.</span></span> <span data-ttu-id="3b31e-133">Enregistrez-la en tant que *public_config.json* (en remplaçant « mystorage » avec le nom de hello de votre compte de stockage) :</span><span class="sxs-lookup"><span data-stu-id="3b31e-133">Save this as *public_config.json* (replacing "mystorage" with hello name of your storage account):</span></span>

    {"fileUris":["https://mystorage.blob.core.windows.net/scripts/install_lamp.sh"], "commandToExecute":"sh install_lamp.sh" }


## <a name="deploy-hello-extension"></a><span data-ttu-id="3b31e-134">Déployer l’extension de hello</span><span class="sxs-lookup"><span data-stu-id="3b31e-134">Deploy hello extension</span></span>
<span data-ttu-id="3b31e-135">Vous pouvez désormais utiliser hello suivant commande toodeploy hello Linux CustomScript Extension toohello à distance à l’aide de la machine virtuelle hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="3b31e-135">Now you can use hello next command toodeploy hello Linux CustomScript Extension toohello remote VM using hello Azure CLI.</span></span>

    azure vm extension set -c "./public_config.json" lamp-vm CustomScript Microsoft.Azure.Extensions 2.0

<span data-ttu-id="3b31e-136">commande précédente Hello télécharge et exécute hello *install_lamp.sh* script sur hello VM appelé *feu-vm*.</span><span class="sxs-lookup"><span data-stu-id="3b31e-136">hello previous command downloads and runs hello *install_lamp.sh* script on hello VM called *lamp-vm*.</span></span>

<span data-ttu-id="3b31e-137">Étant donné que l’application hello inclut un serveur web, n’oubliez pas de port d’écoute tooopen HTTP sur hello VM à distance avec la commande suivante hello.</span><span class="sxs-lookup"><span data-stu-id="3b31e-137">Since hello app includes a web server, remember tooopen an HTTP listening port on hello remote VM with hello next command.</span></span>

    azure vm endpoint create -n Apache -o tcp lamp-vm 80 80

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="3b31e-138">Surveillance et dépannage</span><span class="sxs-lookup"><span data-stu-id="3b31e-138">Monitoring and troubleshooting</span></span>
<span data-ttu-id="3b31e-139">Vous pouvez vérifier dans degré hello s’exécute de script personnalisé en le recherchant dans le fichier journal de hello sur hello VM à distance.</span><span class="sxs-lookup"><span data-stu-id="3b31e-139">You can check on how well hello custom script runs by looking at hello log file on hello remote VM.</span></span> <span data-ttu-id="3b31e-140">SSH trop*feu-vm* et la fin du fichier de journal hello avec la commande suivante hello.</span><span class="sxs-lookup"><span data-stu-id="3b31e-140">SSH too*lamp-vm* and tail hello log file with hello next command.</span></span>

    cd /var/log/azure/customscript
    tail -f handler.log

<span data-ttu-id="3b31e-141">Après avoir exécuté hello CustomScript Extension, vous pouvez parcourir la page PHP toohello que vous avez créé pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="3b31e-141">After you run hello CustomScript Extension, you can browse toohello PHP page you created for information.</span></span> <span data-ttu-id="3b31e-142">Hello PHP page par exemple hello dans cet article est *http://lamp-vm.cloudapp.net/phpinfo.php*.</span><span class="sxs-lookup"><span data-stu-id="3b31e-142">hello PHP page for hello example in this article is *http://lamp-vm.cloudapp.net/phpinfo.php*.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3b31e-143">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="3b31e-143">Additional resources</span></span>
<span data-ttu-id="3b31e-144">Vous pouvez utiliser hello même toodeploy d’étapes de base des applications plus complexes.</span><span class="sxs-lookup"><span data-stu-id="3b31e-144">You can use hello same basic steps toodeploy more complex apps.</span></span> <span data-ttu-id="3b31e-145">Dans cet exemple de script d’installation hello a été enregistré comme un objet blob public dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="3b31e-145">In this example hello install script was saved as a public blob in Azure Storage.</span></span> <span data-ttu-id="3b31e-146">Une option plus sécurisée serait le script d’installation toostore hello en tant qu’objet blob sécurisé avec un [Signature d’accès sécurisé](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span><span class="sxs-lookup"><span data-stu-id="3b31e-146">A more secure option would be toostore hello install script as a secure blob with a [Secure Access Signature](https://msdn.microsoft.com/library/azure/ee395415.aspx) (SAS).</span></span>

<span data-ttu-id="3b31e-147">Ressources supplémentaires pour CLI d’Azure, Linux et hello CustomScript Extension sont décrits ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3b31e-147">Additional resources for Azure CLI, Linux and hello CustomScript Extension are listed next.</span></span>

[<span data-ttu-id="3b31e-148">Automatiser les tâches de personnalisation de machine virtuelle Linux à l’aide de l’extension CustomScript</span><span class="sxs-lookup"><span data-stu-id="3b31e-148">Automate Linux VM Customization Tasks Using CustomScript Extension</span></span>](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)

[<span data-ttu-id="3b31e-149">Extensions Linux Azure (GitHub)</span><span class="sxs-lookup"><span data-stu-id="3b31e-149">Azure Linux Extensions (GitHub)</span></span>](https://github.com/Azure/azure-linux-extensions)