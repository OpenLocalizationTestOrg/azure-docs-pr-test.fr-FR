---
title: "FEU d’aaaDeploy sur un ordinateur virtuel de Linux dans Azure | Documents Microsoft"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 2/21/2017
ms.author: juluk
ms.openlocfilehash: 42d887bb9f78becc02505e336be25fdaaf78df70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-lamp-stack-on-azure"></a><span data-ttu-id="b5afe-103">Déployer une pile LAMP dans Azure</span><span class="sxs-lookup"><span data-stu-id="b5afe-103">Deploy LAMP stack on Azure</span></span>
<span data-ttu-id="b5afe-104">Cet article vous guide tout au long de comment toodeploy un Apache web server, MySQL et PHP (pile de feu hello) sur Azure.</span><span class="sxs-lookup"><span data-stu-id="b5afe-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on Azure.</span></span> <span data-ttu-id="b5afe-105">Vous avez besoin d’un compte Azure ([obtenir une évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/)) et hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="b5afe-105">You need an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span> <span data-ttu-id="b5afe-106">Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b5afe-106">You can also perform these steps with hello [Azure CLI 1.0](create-lamp-stack-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="b5afe-107">Résumé des commandes rapides</span><span class="sxs-lookup"><span data-stu-id="b5afe-107">Quick command summary</span></span>

1. <span data-ttu-id="b5afe-108">Enregistrer et modifier hello [azuredeploy.parameters.json fichier](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) préférence tooyour sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="b5afe-108">Save and edit hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour preference on your local machine.</span></span>
2. <span data-ttu-id="b5afe-109">Exécutez hello suivant deux commandes toocreate un groupe de ressources et ensuite déployer votre modèle :</span><span class="sxs-lookup"><span data-stu-id="b5afe-109">Run hello following two commands toocreate a resource group and then deploy your template:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

### <a name="deploy-lamp-on-existing-vm"></a><span data-ttu-id="b5afe-110">Déploiement de LAMP sur une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="b5afe-110">Deploy LAMP on existing VM</span></span>
<span data-ttu-id="b5afe-111">suivant de Hello packages de mises à jour des commandes, puis installe Apache, MySQL et PHP :</span><span class="sxs-lookup"><span data-stu-id="b5afe-111">hello following commands updates packages, then installs Apache, MySQL, and PHP:</span></span>

```bash
sudo apt-get update
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

## <a name="deploy-lamp-on-new-vm-walkthrough"></a><span data-ttu-id="b5afe-112">Procédure pas à pas de déploiement de LAMP sur une nouvelle machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b5afe-112">Deploy LAMP on new VM walkthrough</span></span>

1. <span data-ttu-id="b5afe-113">Créer un groupe de ressources avec [création de groupe de az](/cli/azure/group#create) toocontain hello nouvelle machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="b5afe-113">Create a resource group with [az group create](/cli/azure/group#create) toocontain hello new VM:</span></span>

```azurecli
az group create -l westus -n myResourceGroup
```
<span data-ttu-id="b5afe-114">toocreate hello machine virtuelle proprement dite, vous pouvez utiliser un modèle Azure Resource Manager déjà écrite [ici sur GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span><span class="sxs-lookup"><span data-stu-id="b5afe-114">toocreate hello VM itself, you can use an already written Azure Resource Manager template found [here on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/lamp-app).</span></span>

2. <span data-ttu-id="b5afe-115">Enregistrer hello [azuredeploy.parameters.json fichier](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour les ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="b5afe-115">Save hello [azuredeploy.parameters.json file](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.parameters.json) tooyour local machine.</span></span>
3. <span data-ttu-id="b5afe-116">Modifier hello **azuredeploy.parameters.json** tooyour de fichier par défaut des entrées.</span><span class="sxs-lookup"><span data-stu-id="b5afe-116">Edit hello **azuredeploy.parameters.json** file tooyour preferred inputs.</span></span>
4. <span data-ttu-id="b5afe-117">Déployer le modèle hello avec [création du déploiement d’un groupe az] référençant hello téléchargé fichier json :</span><span class="sxs-lookup"><span data-stu-id="b5afe-117">Deploy hello template with [az group deployment create] referencing hello downloaded json file:</span></span>

```azurecli
az group deployment create -g myResourceGroup \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/lamp-app/azuredeploy.json \
    --parameters @filepathToParameters.json
```

<span data-ttu-id="b5afe-118">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="b5afe-118">hello output is similar toohello following example:</span></span>

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

<span data-ttu-id="b5afe-119">Vous avez maintenant créé une machine virtuelle Linux avec LAMP déjà installé.</span><span class="sxs-lookup"><span data-stu-id="b5afe-119">You have now created a Linux VM with LAMP already installed on it.</span></span> <span data-ttu-id="b5afe-120">Si vous le souhaitez, vous pouvez vérifier l’installation de hello en sautant trop bas[vérifier feu installé avec succès](#verify-lamp-successfully-installed).</span><span class="sxs-lookup"><span data-stu-id="b5afe-120">If you wish, you can verify hello install by jumping down too[Verify LAMP Successfully Installed](#verify-lamp-successfully-installed).</span></span>

## <a name="deploy-lamp-on-existing-vm-walkthrough"></a><span data-ttu-id="b5afe-121">Procédure pas à pas de déploiement de LAMP sur une machine virtuelle existante</span><span class="sxs-lookup"><span data-stu-id="b5afe-121">Deploy LAMP on existing VM walkthrough</span></span>
<span data-ttu-id="b5afe-122">Si vous avez besoin d’aide pour créer une VM Linux, vous pouvez head [toolearn ici comment toocreate un VM Linux](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span><span class="sxs-lookup"><span data-stu-id="b5afe-122">If you need help creating a Linux VM, you can head [here toolearn how toocreate a Linux VM](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-quick-create-cli).</span></span> <span data-ttu-id="b5afe-123">Ensuite, vous devez tooSSH dans hello Linux VM.</span><span class="sxs-lookup"><span data-stu-id="b5afe-123">Next, you need tooSSH into hello Linux VM.</span></span> <span data-ttu-id="b5afe-124">Si vous avez besoin d’aide sur la création d’une clé SSH, vous pouvez head [toolearn ici comment toocreate une clé SSH sur Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b5afe-124">If you need help with creating an SSH key, you can head [here toolearn how toocreate an SSH key on Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
<span data-ttu-id="b5afe-125">Si vous disposez déjà d’une clé SSH, continuez et ouvrez en ligne de commande une connexion SSH à votre machine virtuelle Linux avec `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="b5afe-125">If you have an SSH key already, go ahead and SSH from your command line into your Linux VM with `ssh azureuser@mypublicdns.westus.cloudapp.azure.com`.</span></span>

<span data-ttu-id="b5afe-126">Maintenant que vous utilisez dans votre VM Linux, nous pouvons guider dans l’installation de la pile de feu hello sur les distributions Debian.</span><span class="sxs-lookup"><span data-stu-id="b5afe-126">Now that you are working within your Linux VM, we can walk through installing hello LAMP stack on Debian-based distributions.</span></span> <span data-ttu-id="b5afe-127">les commandes exactes Hello peuvent différer pour les autres versions de Linux.</span><span class="sxs-lookup"><span data-stu-id="b5afe-127">hello exact commands might differ for other Linux distros.</span></span>

#### <a name="installing-on-debianubuntu"></a><span data-ttu-id="b5afe-128">Installation sur Debian/Ubuntu</span><span class="sxs-lookup"><span data-stu-id="b5afe-128">Installing on Debian/Ubuntu</span></span>
<span data-ttu-id="b5afe-129">Vous devez hello suivant des packages installés : `apache2`, `mysql-server`, `php5`, et `php5-mysql`.</span><span class="sxs-lookup"><span data-stu-id="b5afe-129">You need hello following packages installed: `apache2`, `mysql-server`, `php5`, and `php5-mysql`.</span></span> <span data-ttu-id="b5afe-130">Vous pouvez les installer directement à partir de ces packages ou à l’aide de Tasksel.</span><span class="sxs-lookup"><span data-stu-id="b5afe-130">You can install these packages by directly grabbing these packages or using Tasksel.</span></span>
<span data-ttu-id="b5afe-131">Avant d’installer, vous devez toodownload et mettre à jour les listes de package.</span><span class="sxs-lookup"><span data-stu-id="b5afe-131">Before installing you need toodownload and update package lists.</span></span>

```bash
sudo apt-get update
```

##### <a name="individual-packages"></a><span data-ttu-id="b5afe-132">Packages individuels</span><span class="sxs-lookup"><span data-stu-id="b5afe-132">Individual packages</span></span>
<span data-ttu-id="b5afe-133">Utilisation d’apt-get :</span><span class="sxs-lookup"><span data-stu-id="b5afe-133">Using apt-get:</span></span>

```bash
sudo apt-get install apache2 mysql-server php5 php5-mysql
```

##### <a name="using-tasksel"></a><span data-ttu-id="b5afe-134">Utilisation de Tasksel</span><span class="sxs-lookup"><span data-stu-id="b5afe-134">Using tasksel</span></span>
<span data-ttu-id="b5afe-135">Vous pouvez également télécharger Tasksel, un outil Debian/Ubuntu qui installe plusieurs packages connexes en tant que tâche coordonnée sur votre système.</span><span class="sxs-lookup"><span data-stu-id="b5afe-135">Alternatively you can download Tasksel, a Debian/Ubuntu tool that installs multiple related packages as a coordinated "task" onto your system.</span></span>

```bash
sudo apt-get install tasksel
sudo tasksel install lamp-server
```

<span data-ttu-id="b5afe-136">Après l’exécution d’une des options précédentes de hello, vous allez être invité à tooinstall ces packages et divers autres dépendances.</span><span class="sxs-lookup"><span data-stu-id="b5afe-136">After running either of hello previous options, you will be prompted tooinstall these packages and various other dependencies.</span></span> <span data-ttu-id="b5afe-137">tooset un mot de passe d’administration pour MySQL, appuyez sur « y », puis sur 'Entrée' toocontinue, suivez toutes les invites.</span><span class="sxs-lookup"><span data-stu-id="b5afe-137">tooset an administrative password for MySQL, press 'y' and then 'Enter' toocontinue, and follow any other prompts.</span></span> <span data-ttu-id="b5afe-138">Ce processus installe hello minimale requise PHP les extensions nécessitées toouse PHP avec MySQL.</span><span class="sxs-lookup"><span data-stu-id="b5afe-138">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![][1]

<span data-ttu-id="b5afe-139">Exécutez hello suivant commande toosee autres extensions PHP disponibles sous forme de packages :</span><span class="sxs-lookup"><span data-stu-id="b5afe-139">Run hello following command toosee other PHP extensions that are available as packages:</span></span>

```bash
apt-cache search php5
```

#### <a name="create-infophp-document"></a><span data-ttu-id="b5afe-140">Création d’un document info.php</span><span class="sxs-lookup"><span data-stu-id="b5afe-140">Create info.php document</span></span>
<span data-ttu-id="b5afe-141">Vous devez maintenant être en mesure de toocheck quelle version de PHP, MySQL et Apache vous avez via la ligne de commande hello en tapant `apache2 -v`, `mysql -v`, ou `php -v`.</span><span class="sxs-lookup"><span data-stu-id="b5afe-141">You should now be able toocheck what version of Apache, MySQL, and PHP you have through hello command line by typing `apache2 -v`, `mysql -v`, or `php -v`.</span></span>

<span data-ttu-id="b5afe-142">Si vous devez comme tootest en outre, vous pouvez créer un tooview de page PHP info rapide dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="b5afe-142">If you would like tootest further, you can create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="b5afe-143">Créez un fichier avec l’éditeur de texte Nano à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b5afe-143">Create a file with Nano text editor with this command:</span></span>

```bash
sudo nano /var/www/html/info.php
```

<span data-ttu-id="b5afe-144">Dans l’éditeur de texte hello GNU Nano, ajoutez hello lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="b5afe-144">Within hello GNU Nano text editor, add hello following lines:</span></span>

```php
<?php
phpinfo();
?>
```

<span data-ttu-id="b5afe-145">Ensuite, enregistrez et quittez l’éditeur de texte hello.</span><span class="sxs-lookup"><span data-stu-id="b5afe-145">Then save and exit hello text editor.</span></span>

<span data-ttu-id="b5afe-146">Redémarrez Apache avec cette commande pour que toutes les nouvelles installations prennent effet.</span><span class="sxs-lookup"><span data-stu-id="b5afe-146">Restart Apache with this command so all new installs take effect.</span></span>

```bash
sudo service apache2 restart
```

## <a name="verify-lamp-successfully-installed"></a><span data-ttu-id="b5afe-147">Vérification de l’installation correcte de LAMP</span><span class="sxs-lookup"><span data-stu-id="b5afe-147">Verify LAMP successfully installed</span></span>
<span data-ttu-id="b5afe-148">Vous pouvez maintenant vérifier vous avez créé en ouvrant un navigateur et allez toohttp://youruniqueDNS/info.php page des informations hello PHP.</span><span class="sxs-lookup"><span data-stu-id="b5afe-148">Now you can check hello PHP info page you created by opening a browser and going toohttp://youruniqueDNS/info.php.</span></span> <span data-ttu-id="b5afe-149">Il doit se présenter une image toothis similaire.</span><span class="sxs-lookup"><span data-stu-id="b5afe-149">It should look similar toothis image.</span></span>

![][2]

<span data-ttu-id="b5afe-150">Vous pouvez vérifier votre installation Apache en consultant hello Apache2 Ubuntu par défaut Page en accédant tooyou http://youruniqueDNS/.</span><span class="sxs-lookup"><span data-stu-id="b5afe-150">You can check your Apache installation by viewing hello Apache2 Ubuntu Default Page by going tooyou http://youruniqueDNS/.</span></span> <span data-ttu-id="b5afe-151">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="b5afe-151">hello output is similar toohello following example:</span></span>

![][3]

<span data-ttu-id="b5afe-152">Félicitations, vous avez configuré une pile LAMP sur votre machine virtuelle Azure !</span><span class="sxs-lookup"><span data-stu-id="b5afe-152">Congratulations, you have just setup a LAMP stack on your Azure VM!</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5afe-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b5afe-153">Next steps</span></span>
<span data-ttu-id="b5afe-154">Consultez hello documentation Ubuntu sur la pile de feu hello :</span><span class="sxs-lookup"><span data-stu-id="b5afe-154">Check out hello Ubuntu documentation on hello LAMP stack:</span></span>

* [<span data-ttu-id="b5afe-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span><span class="sxs-lookup"><span data-stu-id="b5afe-155">https://help.ubuntu.com/community/ApacheMySQLPHP</span></span>](https://help.ubuntu.com/community/ApacheMySQLPHP)

[1]: ./media/deploy-lamp-stack/configmysqlpassword-small.png
[2]: ./media/deploy-lamp-stack/phpsuccesspage.png
[3]: ./media/deploy-lamp-stack/apachesuccesspage.png
