---
title: "Déployer LEMP sur une machine virtuelle Linux dans Azure | Microsoft Docs"
description: Didacticiel - Installer la pile LEMP sur une machine virtuelle Linux dans Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: 653af144eb12cacf955f96a5442efd73add38e88
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a><span data-ttu-id="a49b9-103">Installer un serveur web LEMP sur une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="a49b9-103">Install a LEMP web server on an Azure VM</span></span>
<span data-ttu-id="a49b9-104">Cet article vous guide à travers le déploiement d’un serveur web NGINX, de celui de MySQL et de PHP (la pile LEMP) sur une machine virtuelle Ubuntu dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a49b9-104">This article walks you through how to deploy an NGINX web server, MySQL, and PHP (the LEMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="a49b9-105">Pouvant également être installée dans Azure, la pile LEMP est une alternative à la très répandue [pile LAMP](tutorial-lamp-stack.md).</span><span class="sxs-lookup"><span data-stu-id="a49b9-105">The LEMP stack is an alternative to the popular [LAMP stack](tutorial-lamp-stack.md), which you can also install in Azure.</span></span> <span data-ttu-id="a49b9-106">Pour voir le serveur LEMP fonctionner, vous pouvez éventuellement installer et configurer un site WordPress.</span><span class="sxs-lookup"><span data-stu-id="a49b9-106">To see the LEMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="a49b9-107">Ce didacticiel vous explique comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a49b9-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a49b9-108">Créer une machine virtuelle Ubuntu (la lettre « L » dans la pile LEMP)</span><span class="sxs-lookup"><span data-stu-id="a49b9-108">Create an Ubuntu VM (the 'L' in the LEMP stack)</span></span>
> * <span data-ttu-id="a49b9-109">Ouvrez le port 80 pour le trafic web</span><span class="sxs-lookup"><span data-stu-id="a49b9-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="a49b9-110">Installer NGINX, MySQL et PHP</span><span class="sxs-lookup"><span data-stu-id="a49b9-110">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="a49b9-111">Vérifier l’installation et la configuration</span><span class="sxs-lookup"><span data-stu-id="a49b9-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="a49b9-112">Installer WordPress sur le serveur LEMP</span><span class="sxs-lookup"><span data-stu-id="a49b9-112">Install WordPress on the LEMP server</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a49b9-113">Si vous choisissez d’installer et d’utiliser l’interface de ligne de commande localement, vous devez exécuter Azure CLI version 2.0.4 ou une version ultérieure pour poursuivre la procédure décrite dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="a49b9-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a49b9-114">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="a49b9-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="a49b9-115">Si vous devez installer ou mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a49b9-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a><span data-ttu-id="a49b9-116">Installer NGINX, MySQL et PHP</span><span class="sxs-lookup"><span data-stu-id="a49b9-116">Install NGINX, MySQL, and PHP</span></span>

<span data-ttu-id="a49b9-117">Exécutez la commande suivante pour mettre à jour les sources de package Ubuntu et installer NGINX, MySQL et PHP.</span><span class="sxs-lookup"><span data-stu-id="a49b9-117">Run the following command to update Ubuntu package sources and install NGINX, MySQL, and PHP.</span></span> 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

<span data-ttu-id="a49b9-118">Vous êtes invité à installer les packages et les autres dépendances.</span><span class="sxs-lookup"><span data-stu-id="a49b9-118">You are prompted to install the packages and other dependencies.</span></span> <span data-ttu-id="a49b9-119">Lorsque vous y êtes invité, définissez un mot de passe racine pour MySQL, puis [Entrée] pour continuer.</span><span class="sxs-lookup"><span data-stu-id="a49b9-119">When prompted, set a root password for MySQL, and then [Enter] to continue.</span></span> <span data-ttu-id="a49b9-120">Suivez les invites restantes.</span><span class="sxs-lookup"><span data-stu-id="a49b9-120">Follow the remaining prompts.</span></span> <span data-ttu-id="a49b9-121">Ce processus installe les extensions PHP minimales requises pour utiliser PHP avec MySQL.</span><span class="sxs-lookup"><span data-stu-id="a49b9-121">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![Page de mot de passe racine MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="a49b9-123">Vérifier l’installation et la configuration</span><span class="sxs-lookup"><span data-stu-id="a49b9-123">Verify installation and configuration</span></span>


### <a name="nginx"></a><span data-ttu-id="a49b9-124">NGINX</span><span class="sxs-lookup"><span data-stu-id="a49b9-124">NGINX</span></span>

<span data-ttu-id="a49b9-125">Vérifiez la version de NGINX à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a49b9-125">Check the version of NGINX with the following command:</span></span>
```bash
nginx -v
```

<span data-ttu-id="a49b9-126">Avec NGINX installé et le port 80 ouvert sur votre machine virtuelle, le serveur web est désormais accessible à partir d’internet.</span><span class="sxs-lookup"><span data-stu-id="a49b9-126">With NGINX installed, and port 80 open to your VM, the web server can now be accessed from the internet.</span></span> <span data-ttu-id="a49b9-127">Pour afficher la page d’accueil de NGINX, ouvrez un navigateur web et entrez l’adresse IP publique de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a49b9-127">To view the NGINX welcome page, open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="a49b9-128">Utilisez l’adresse IP publique dont vous vous êtes servi pour vous connecter par SSH à la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="a49b9-128">Use the public IP address you used to SSH to the VM:</span></span>

![Page par défaut de NGINX][3]


### <a name="mysql"></a><span data-ttu-id="a49b9-130">MySQL</span><span class="sxs-lookup"><span data-stu-id="a49b9-130">MySQL</span></span>

<span data-ttu-id="a49b9-131">Vérifiez la version de MySQL avec la commande suivante (remarquez le paramètre `V` avec une majuscule) :</span><span class="sxs-lookup"><span data-stu-id="a49b9-131">Check the version of MySQL with the following command (note the capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="a49b9-132">Nous vous recommandons d’exécuter le script suivant pour vous aider à sécuriser l’installation de MySQL :</span><span class="sxs-lookup"><span data-stu-id="a49b9-132">We recommend running the following script to help secure the installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="a49b9-133">Entrez votre mot de passe racine MySQL et configurez les paramètres de sécurité pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="a49b9-133">Enter your MySQL root password, and configure the security settings for your environment.</span></span>

<span data-ttu-id="a49b9-134">Si vous souhaitez créer une base de données MySQL, ajoutez des utilisateurs ou changez les paramètres de configuration, puis connectez-vous à MySQL :</span><span class="sxs-lookup"><span data-stu-id="a49b9-134">If you want to create a MySQL database, add users, or change configuration settings, login to MySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="a49b9-135">Lorsque vous avez terminé, quittez l’invite de mysql en tapant `\q`.</span><span class="sxs-lookup"><span data-stu-id="a49b9-135">When done, exit the mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="a49b9-136">PHP</span><span class="sxs-lookup"><span data-stu-id="a49b9-136">PHP</span></span>

<span data-ttu-id="a49b9-137">Vérifiez la version de PHP avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a49b9-137">Check the version of PHP with the following command:</span></span>

```bash
php -v
```

<span data-ttu-id="a49b9-138">Configurez NGINX pour utiliser l’interface PHP-FPM (PHP FastCGI Process Manager).</span><span class="sxs-lookup"><span data-stu-id="a49b9-138">Configure NGINX to use the PHP FastCGI Process Manager (PHP-FPM).</span></span> <span data-ttu-id="a49b9-139">Exécutez les commandes suivantes pour sauvegarder le fichier de configuration du bloc serveur NGINX d’origine et modifier ensuite le fichier original dans l’éditeur de votre choix :</span><span class="sxs-lookup"><span data-stu-id="a49b9-139">Run the following commands to back up the original NGINX server block config file and then edit the original file in an editor of your choice:</span></span>

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

<span data-ttu-id="a49b9-140">Dans l’éditeur, remplacez le contenu de `/etc/nginx/sites-available/default` par ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="a49b9-140">In the editor, replace the contents of `/etc/nginx/sites-available/default` with the following.</span></span> <span data-ttu-id="a49b9-141">Consultez les commentaires pour lire une explication sur les paramètres.</span><span class="sxs-lookup"><span data-stu-id="a49b9-141">See the comments for explanation of the settings.</span></span> <span data-ttu-id="a49b9-142">Remplacez l’adresse IP publique de votre machine virtuelle par *yourPublicIPAddress* (votre adresse IP publique) et conservez les autres paramètres.</span><span class="sxs-lookup"><span data-stu-id="a49b9-142">Substitute the public IP address of your VM for *yourPublicIPAddress*, and leave the remaining settings.</span></span> <span data-ttu-id="a49b9-143">Puis enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="a49b9-143">Then save the file.</span></span>

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    # Homepage of website is index.php
    index index.php;

    server_name yourPublicIPAddress;

    location / {
        try_files $uri $uri/ =404;
    }

    # Include FastCGI configuration for NGINX
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }
}
```

<span data-ttu-id="a49b9-144">Vérifiez la configuration de NGINX à la recherche d’erreurs de syntaxe :</span><span class="sxs-lookup"><span data-stu-id="a49b9-144">Check the NGINX configuration for syntax errors:</span></span>

```bash
sudo nginx -t
```

<span data-ttu-id="a49b9-145">Si la syntaxe est correcte, redémarrez NGINX avec la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a49b9-145">If the syntax is correct, restart NGINX with the following command:</span></span>

```bash
sudo service nginx restart
```

<span data-ttu-id="a49b9-146">Si vous voulez poursuivre le test, créez une page d’informations PHP rapide pour l’afficher dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="a49b9-146">If you want to test further, create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="a49b9-147">La commande suivante crée la page d’informations PHP :</span><span class="sxs-lookup"><span data-stu-id="a49b9-147">The following command creates the PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



<span data-ttu-id="a49b9-148">À présent, vous pouvez vérifier la page d’informations PHP que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="a49b9-148">Now you can check the PHP info page you created.</span></span> <span data-ttu-id="a49b9-149">Ouvrez un navigateur web et accédez à `http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="a49b9-149">Open a browser and go to `http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="a49b9-150">Remplacez l’adresse IP publique de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a49b9-150">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="a49b9-151">Elle doit ressembler à cette image.</span><span class="sxs-lookup"><span data-stu-id="a49b9-151">It should look similar to this image.</span></span>

![Page d’informations PHP][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a><span data-ttu-id="a49b9-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a49b9-153">Next steps</span></span>

<span data-ttu-id="a49b9-154">Dans ce didacticiel, vous avez déployé un serveur LEMP dans Azure.</span><span class="sxs-lookup"><span data-stu-id="a49b9-154">In this tutorial, you deployed a LEMP server in Azure.</span></span> <span data-ttu-id="a49b9-155">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="a49b9-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a49b9-156">Créer une machine virtuelle Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a49b9-156">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="a49b9-157">Ouvrez le port 80 pour le trafic web</span><span class="sxs-lookup"><span data-stu-id="a49b9-157">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="a49b9-158">Installer NGINX, MySQL et PHP</span><span class="sxs-lookup"><span data-stu-id="a49b9-158">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="a49b9-159">Vérifier l’installation et la configuration</span><span class="sxs-lookup"><span data-stu-id="a49b9-159">Verify installation and configuration</span></span>
> * <span data-ttu-id="a49b9-160">Installer WordPress sur la pile LEMP</span><span class="sxs-lookup"><span data-stu-id="a49b9-160">Install WordPress on the LEMP stack</span></span>

<span data-ttu-id="a49b9-161">Passez au didacticiel suivant pour savoir comment mieux protéger les serveurs SSL à l’aide des certificats SSL.</span><span class="sxs-lookup"><span data-stu-id="a49b9-161">Advance to the next tutorial to learn how to secure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a49b9-162">Sécuriser un serveur web avec SSL</span><span class="sxs-lookup"><span data-stu-id="a49b9-162">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
