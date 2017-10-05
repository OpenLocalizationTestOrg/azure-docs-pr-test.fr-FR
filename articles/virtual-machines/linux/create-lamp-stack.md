---
title: "Déployer LAMP sur une machine virtuelle Linux dans Azure | Microsoft Docs"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: ad69876bfbeba5f948a81e5c48c659fdf2265ae2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-lamp-stack-on-azure"></a><span data-ttu-id="9958f-103">Déployer une pile LAMP dans Azure</span><span class="sxs-lookup"><span data-stu-id="9958f-103">Deploy LAMP stack on Azure</span></span>
<span data-ttu-id="9958f-104">Cet article vous guide à travers le déploiement d’un serveur web Apache, de MySQL et de PHP (la pile LAMP) sur Azure.</span><span class="sxs-lookup"><span data-stu-id="9958f-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on Azure.</span></span> <span data-ttu-id="9958f-105">Vous avez besoin d’un compte Azure ([obtenir un essai gratuit](https://azure.microsoft.com/pricing/free-trial/)) et [d’Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="9958f-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and the [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="9958f-106">Vous pouvez également suivre ces étapes avec [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9958f-106">You can also perform these steps with the [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="9958f-107">Résumé des commandes rapides</span><span class="sxs-lookup"><span data-stu-id="9958f-107">Quick command summary</span></span>

1. <span data-ttu-id="9958f-108">Enregistrez et modifiez le [fichier azuredeploy.parameters.json](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) à votre convenance sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="9958f-108">Save and edit the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your preference on your local machine.</span></span>
2. <span data-ttu-id="9958f-109">Exécutez les deux commandes suivantes pour créer un groupe de ressources, puis déployez votre modèle :</span><span class="sxs-lookup"><span data-stu-id="9958f-109">Run the following two commands to create a resource group and then deploy your template:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a><span data-ttu-id="9958f-110">Déploiement de LAMP sur une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="9958f-110">Deploy LAMP on existing VM</span></span>
<span data-ttu-id="9958f-111">Les commandes suivantes mettent à jour les packages, puis installent Apache, MySQL et PHP :</span><span class="sxs-lookup"><span data-stu-id="9958f-111">The following commands updates packages, then installs Apache, MySQL, and PHP:</span></span>

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="9958f-112">Procédure pas à pas de déploiement de LAMP sur une nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="9958f-112">Deploy LAMP on new VM walkthrough</span></span>

1. <span data-ttu-id="9958f-113">Avec la commande [az group create](/cli/azure/group#create), créez un groupe de ressources qui contiendra la nouvelle machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="9958f-113">Create a resource group with [az group create](/cli/azure/group#create) to contain the new VM:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
```
<span data-ttu-id="9958f-114">Pour créer la machine virtuelle elle-même, vous pouvez utiliser un modèle Azure Resource Manager déjà écrit [ici sur GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="9958f-114">To create the VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

2. <span data-ttu-id="9958f-115">Enregistrez le [fichier azuredeploy.parameters.json](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="9958f-115">Save the [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) to your local machine.</span></span>
3. <span data-ttu-id="9958f-116">Modifiez le fichier **azuredeploy.parameters.json** en insérant les entrées de votre choix.</span><span class="sxs-lookup"><span data-stu-id="9958f-116">Edit the **azuredeploy.parameters.json** file to your preferred inputs.</span></span>
4. <span data-ttu-id="9958f-117">Déployez le modèle avec [az group deployment create] en faisant référence au fichier JSON téléchargé :</span><span class="sxs-lookup"><span data-stu-id="9958f-117">Deploy the template with [az group deployment create] referencing the downloaded json file:</span></span>

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

<span data-ttu-id="9958f-118">Le résultat ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9958f-118">The output is similar to the following example:</span></span>

```json
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup/providers/Microsoft.Resources/deployments/azuredeploy",
"name": "azuredeploy",
"properties": {
    "correlationId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
    "debugSetting": null,
}
...
"provisioningState": "Succeeded",
"template": null,
"templateLink": {
    "contentVersion": "1.0.0.0",
    "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json"
    },
    "timestamp": "2017-02-22T00:05:51.860411+00:00"
},
"resourceGroup": "myResourceGroup"
}
```

<span data-ttu-id="9958f-119">Vous avez maintenant créé une machine virtuelle Linux avec LAMP déjà installé.</span><span class="sxs-lookup"><span data-stu-id="9958f-119">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="9958f-120">Si vous le souhaitez, vous pouvez vérifier l’installation en accédant à la section [Vérification de l’installation correcte de LAMP](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="9958f-120">If you wish, you can verify the install by jumping down to [Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="9958f-121">Procédure pas à pas de déploiement de LAMP sur une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="9958f-121">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="9958f-122">Si vous avez besoin d’aide pour créer une machine virtuelle Linux, vous pouvez vous rendre [ici pour apprendre à créer une machine virtuelle Linux](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span><span class="sxs-lookup"><span data-stu-id="9958f-122">If you need help creating a Linux VM, you can head [here to learn how to create a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span></span> <span data-ttu-id="9958f-123">Ensuite, vous devez intégrer SSH à la machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="9958f-123">Next, you need to SSH into the Linux VM.</span></span> <span data-ttu-id="9958f-124">Si vous avez besoin d’aide pour créer une clé SSH, vous pouvez vous rendre [ici pour apprendre à créer une clé SSH sous Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9958f-124">If you need help with creating an SSH key, you can head [here to learn how to create an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="9958f-125">Si vous disposez déjà d’une clé SSH, continuez et ouvrez en ligne de commande une connexion SSH à votre machine virtuelle Linux avec `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="9958f-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="9958f-126">Maintenant que vous travaillez dans votre machine virtuelle Linux, nous allons étudier l’installation de la pile LAMP sur des distributions Debian.</span><span class="sxs-lookup"><span data-stu-id="9958f-126">Now that you are working within your Linux VM, we can walk through installing the LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="9958f-127">Les commandes exactes peuvent varier pour les autres distributions Linux.</span><span class="sxs-lookup"><span data-stu-id="9958f-127">The exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="9958f-128">Installation sur Debian/Ubuntu</span><span class="sxs-lookup"><span data-stu-id="9958f-128">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="9958f-129">Les packages suivants doivent être installés : `apache2`, `mysql-server`, `php5` et `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="9958f-129">You need the following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="9958f-130">Vous pouvez les installer directement à partir de ces packages ou à l’aide de Tasksel.</span><span class="sxs-lookup"><span data-stu-id="9958f-130">You can install these packages by directly grabbing these packages or using Tasksel.</span></span>
<span data-ttu-id="9958f-131">Avant de procéder à l’installation, vous devez télécharger et mettre à jour les listes de packages.</span><span class="sxs-lookup"><span data-stu-id="9958f-131">Before installing you need to download and update package lists.</span></span>

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a><span data-ttu-id="9958f-132">Packages individuels</span><span class="sxs-lookup"><span data-stu-id="9958f-132">Individual packages</span></span>
<span data-ttu-id="9958f-133">Utilisation d’apt-get :</span><span class="sxs-lookup"><span data-stu-id="9958f-133">Using apt-get:</span></span>

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a><span data-ttu-id="9958f-134">Utilisation de Tasksel</span><span class="sxs-lookup"><span data-stu-id="9958f-134">Using tasksel</span></span>
<span data-ttu-id="9958f-135">Vous pouvez également télécharger Tasksel, un outil Debian/Ubuntu qui installe plusieurs packages connexes en tant que tâche coordonnée sur votre système.</span><span class="sxs-lookup"><span data-stu-id="9958f-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

<span data-ttu-id="9958f-136">Après avoir exécuté l’une des options précédentes, vous serez invité à installer ces packages et d’autres dépendances.</span><span class="sxs-lookup"><span data-stu-id="9958f-136">After running either of the previous options, you will be prompted to install these packages and various other dependencies.</span></span> <span data-ttu-id="9958f-137">Pour définir un mot de passe d’administration pour MySQL, appuyez sur « y » puis « Entrée » pour continuer et suivez les indications des invites.</span><span class="sxs-lookup"><span data-stu-id="9958f-137">To set an administrative password for MySQL, press 'y' and then 'Enter' to continue, and follow any other prompts.</span></span> <span data-ttu-id="9958f-138">Ce processus installe les extensions PHP minimales requises pour utiliser PHP avec MySQL.</span><span class="sxs-lookup"><span data-stu-id="9958f-138">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="9958f-139">Exécutez les commandes suivantes pour voir les autres extensions PHP disponibles sous forme de packages :</span><span class="sxs-lookup"><span data-stu-id="9958f-139">Run the following command to see other PHP extensions that are available as packages:</span></span>

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a><span data-ttu-id="9958f-140">Création d’un document info.php</span><span class="sxs-lookup"><span data-stu-id="9958f-140">Create info.php document</span></span>
<span data-ttu-id="9958f-141">Vous devez maintenant être en mesure de vérifier la version d’Apache, de MySQL et de PHP figurant dans la ligne de commande en tapant `apache2 -v`, `mysql -v` ou `php -v`.</span><span class="sxs-lookup"><span data-stu-id="9958f-141">You should now be able to check what version of Apache, MySQL, and PHP you have through the command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="9958f-142">Si vous souhaitez poursuivre le test, vous pouvez créer une page d’informations PHP rapide à afficher dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="9958f-142">If you would like to test further, you can create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="9958f-143">Créez un fichier avec l’éditeur de texte Nano à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9958f-143">Create a file with Nano text editor with this command:</span></span>

```bash
sudo nano /var/www/html/info.php
```

<span data-ttu-id="9958f-144">Dans l’éditeur de texte GNU Nano, ajoutez les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9958f-144">Within the GNU Nano text editor, add the following lines:</span></span>

```php
<?php
phpinfo();
?>
```

<span data-ttu-id="9958f-145">Enregistrez ensuite votre travail et quittez l’éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="9958f-145">Then save and exit the text editor.</span></span>

<span data-ttu-id="9958f-146">Redémarrez Apache avec cette commande pour que toutes les nouvelles installations prennent effet.</span><span class="sxs-lookup"><span data-stu-id="9958f-146">Restart Apache with this command so all new installs take effect.</span></span>

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="9958f-147">Vérification de l’installation correcte de LAMP</span><span class="sxs-lookup"><span data-stu-id="9958f-147">Verify LAMP successfully installed</span></span>
<span data-ttu-id="9958f-148">Vous pouvez maintenant consulter la page d’informations PHP que vous avez créée en ouvrant un navigateur et en accédant à http://votreDNSunique/info.php.</span><span class="sxs-lookup"><span data-stu-id="9958f-148">Now you can check the PHP info page you created by opening a browser and going to http://youruniqueDNS/info.php.</span></span> <span data-ttu-id="9958f-149">Elle doit ressembler à cette image.</span><span class="sxs-lookup"><span data-stu-id="9958f-149">It should look similar to this image.</span></span>

![][2]

<span data-ttu-id="9958f-150">Vous pouvez vérifier votre installation Apache en consultant la page par défaut d’Ubuntu Apache2 en accédant à http://votreDNSunique/.</span><span class="sxs-lookup"><span data-stu-id="9958f-150">You can check your Apache installation by viewing the Apache2 Ubuntu Default Page by going to you http://youruniqueDNS/.</span></span> <span data-ttu-id="9958f-151">Le résultat ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9958f-151">The output is similar to the following example:</span></span>

![][3]

<span data-ttu-id="9958f-152">Félicitations, vous avez configuré une pile LAMP sur votre machine virtuelle Azure !</span><span class="sxs-lookup"><span data-stu-id="9958f-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="9958f-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9958f-153">Next steps</span></span>
<span data-ttu-id="9958f-154">Consultez la documentation Ubuntu sur la pile LAMP :</span><span class="sxs-lookup"><span data-stu-id="9958f-154">Check out the Ubuntu documentation on the LAMP stack:</span></span>

* [<span data-ttu-id="9958f-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="9958f-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
