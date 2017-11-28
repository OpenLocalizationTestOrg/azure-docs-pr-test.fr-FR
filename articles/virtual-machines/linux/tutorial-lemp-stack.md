---
title: aaaDeploy LEMP sur un ordinateur virtuel de Linux dans Azure | Documents Microsoft
description: Didacticiel - pile LEMP installation hello un VM Linux dans Azure
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
ms.openlocfilehash: d8f9d84c5e9c0df4e9e985c10fe10f63a2f88214
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a><span data-ttu-id="c8c62-103">Installer un serveur web LEMP sur une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="c8c62-103">Install a LEMP web server on an Azure VM</span></span>
<span data-ttu-id="c8c62-104">Cet article vous guide tout au long de comment toodeploy un NGINX web server, MySQL et PHP (hello LEMP de pile) sur un VM Ubuntu dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c8c62-104">This article walks you through how toodeploy an NGINX web server, MySQL, and PHP (hello LEMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="c8c62-105">pile LEMP Hello est un autre toohello populaires [pile LAMP](tutorial-lamp-stack.md), que vous pouvez également installer dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c8c62-105">hello LEMP stack is an alternative toohello popular [LAMP stack](tutorial-lamp-stack.md), which you can also install in Azure.</span></span> <span data-ttu-id="c8c62-106">serveur LEMP toosee hello dans action, vous pouvez éventuellement installer et configurer un site WordPress.</span><span class="sxs-lookup"><span data-stu-id="c8c62-106">toosee hello LEMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="c8c62-107">Ce didacticiel vous explique comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c8c62-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c8c62-108">Créer une VM Ubuntu (hello « L » dans la pile LEMP hello)</span><span class="sxs-lookup"><span data-stu-id="c8c62-108">Create an Ubuntu VM (hello 'L' in hello LEMP stack)</span></span>
> * <span data-ttu-id="c8c62-109">Ouvrez le port 80 pour le trafic web</span><span class="sxs-lookup"><span data-stu-id="c8c62-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="c8c62-110">Installer NGINX, MySQL et PHP</span><span class="sxs-lookup"><span data-stu-id="c8c62-110">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="c8c62-111">Vérifier l’installation et la configuration</span><span class="sxs-lookup"><span data-stu-id="c8c62-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="c8c62-112">Installation de WordPress sur le serveur LEMP hello</span><span class="sxs-lookup"><span data-stu-id="c8c62-112">Install WordPress on hello LEMP server</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c8c62-113">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c8c62-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="c8c62-114">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="c8c62-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c8c62-115">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c8c62-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a><span data-ttu-id="c8c62-116">Installer NGINX, MySQL et PHP</span><span class="sxs-lookup"><span data-stu-id="c8c62-116">Install NGINX, MySQL, and PHP</span></span>

<span data-ttu-id="c8c62-117">Exécutez hello commande tooupdate Ubuntu package sources suivantes et installer NGINX, MySQL et PHP.</span><span class="sxs-lookup"><span data-stu-id="c8c62-117">Run hello following command tooupdate Ubuntu package sources and install NGINX, MySQL, and PHP.</span></span> 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

<span data-ttu-id="c8c62-118">Vous êtes invité à tooinstall hello packages et autres dépendances.</span><span class="sxs-lookup"><span data-stu-id="c8c62-118">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="c8c62-119">Lorsque vous y êtes invité, définissez un mot de passe racine MySQL, puis sur [Entrée] toocontinue.</span><span class="sxs-lookup"><span data-stu-id="c8c62-119">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="c8c62-120">Suivez hello restant d’invites.</span><span class="sxs-lookup"><span data-stu-id="c8c62-120">Follow hello remaining prompts.</span></span> <span data-ttu-id="c8c62-121">Ce processus installe hello minimale requise PHP les extensions nécessitées toouse PHP avec MySQL.</span><span class="sxs-lookup"><span data-stu-id="c8c62-121">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![Page de mot de passe racine MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="c8c62-123">Vérifier l’installation et la configuration</span><span class="sxs-lookup"><span data-stu-id="c8c62-123">Verify installation and configuration</span></span>


### <a name="nginx"></a><span data-ttu-id="c8c62-124">NGINX</span><span class="sxs-lookup"><span data-stu-id="c8c62-124">NGINX</span></span>

<span data-ttu-id="c8c62-125">Vérifier la version de hello de NGINX avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c8c62-125">Check hello version of NGINX with hello following command:</span></span>
```bash
nginx -v
```

<span data-ttu-id="c8c62-126">Avec NGINX installés et le port 80 ouvrez tooyour machine virtuelle, de serveur web de hello désormais accessibles à partir de hello internet.</span><span class="sxs-lookup"><span data-stu-id="c8c62-126">With NGINX installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="c8c62-127">tooview hello NGINX page d’accueil, ouvrez un navigateur web et entrez les adresse IP publique hello Hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c8c62-127">tooview hello NGINX welcome page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="c8c62-128">Utilisez l’adresse IP publique de hello, vous avez utilisé tooSSH toohello machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="c8c62-128">Use hello public IP address you used tooSSH toohello VM:</span></span>

![Page par défaut de NGINX][3]


### <a name="mysql"></a><span data-ttu-id="c8c62-130">MySQL</span><span class="sxs-lookup"><span data-stu-id="c8c62-130">MySQL</span></span>

<span data-ttu-id="c8c62-131">Vérifiez la version hello de MySQL avec hello commande suivante (Notez majuscules de hello `V` paramètre) :</span><span class="sxs-lookup"><span data-stu-id="c8c62-131">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="c8c62-132">Nous vous recommandons d’exécuter hello après l’installation de hello sécurisé toohelp script de MySQL :</span><span class="sxs-lookup"><span data-stu-id="c8c62-132">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="c8c62-133">Entrez votre mot de passe racine MySQL et configurer les paramètres de sécurité hello pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="c8c62-133">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="c8c62-134">Si vous souhaitez toocreate une base de données MySQL, ajouter des utilisateurs, ou modifier les paramètres de configuration, tooMySQL de connexion :</span><span class="sxs-lookup"><span data-stu-id="c8c62-134">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="c8c62-135">Lorsque vous avez terminé, quittez hello mysql invite en tapant `\q`.</span><span class="sxs-lookup"><span data-stu-id="c8c62-135">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="c8c62-136">PHP</span><span class="sxs-lookup"><span data-stu-id="c8c62-136">PHP</span></span>

<span data-ttu-id="c8c62-137">Vérifier la version de hello de PHP avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c8c62-137">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="c8c62-138">Configurer hello de toouse NGINX Gestionnaire de processus FastCGI PHP (PHP-pouces).</span><span class="sxs-lookup"><span data-stu-id="c8c62-138">Configure NGINX toouse hello PHP FastCGI Process Manager (PHP-FPM).</span></span> <span data-ttu-id="c8c62-139">Exécutez hello suivant les commandes tooback serveur NGINX d’origine de hello bloquer le fichier de configuration et puis modifiez le fichier d’origine de hello dans un éditeur de votre choix :</span><span class="sxs-lookup"><span data-stu-id="c8c62-139">Run hello following commands tooback up hello original NGINX server block config file and then edit hello original file in an editor of your choice:</span></span>

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

<span data-ttu-id="c8c62-140">Dans l’éditeur de hello, remplacez le contenu de hello de `/etc/nginx/sites-available/default` avec les éléments suivants de hello.</span><span class="sxs-lookup"><span data-stu-id="c8c62-140">In hello editor, replace hello contents of `/etc/nginx/sites-available/default` with hello following.</span></span> <span data-ttu-id="c8c62-141">Consultez les commentaires hello pour une explication des paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="c8c62-141">See hello comments for explanation of hello settings.</span></span> <span data-ttu-id="c8c62-142">Remplacez hello adresse IP publique de votre machine virtuelle pour *yourPublicIPAddress*et laisser hello restant de paramètres.</span><span class="sxs-lookup"><span data-stu-id="c8c62-142">Substitute hello public IP address of your VM for *yourPublicIPAddress*, and leave hello remaining settings.</span></span> <span data-ttu-id="c8c62-143">Puis enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="c8c62-143">Then save hello file.</span></span>

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

<span data-ttu-id="c8c62-144">Vérifier la configuration de NGINX hello pour les erreurs de syntaxe :</span><span class="sxs-lookup"><span data-stu-id="c8c62-144">Check hello NGINX configuration for syntax errors:</span></span>

```bash
sudo nginx -t
```

<span data-ttu-id="c8c62-145">Si la syntaxe de hello est correcte, redémarrez NGINX avec hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c8c62-145">If hello syntax is correct, restart NGINX with hello following command:</span></span>

```bash
sudo service nginx restart
```

<span data-ttu-id="c8c62-146">Si vous souhaitez davantage de tootest, créez un tooview de page PHP info rapide dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="c8c62-146">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="c8c62-147">Hello commande suivante crée la page des informations hello PHP :</span><span class="sxs-lookup"><span data-stu-id="c8c62-147">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



<span data-ttu-id="c8c62-148">Vous pouvez maintenant vérifier page des informations de PHP hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="c8c62-148">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="c8c62-149">Ouvrez un navigateur et allez trop`http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="c8c62-149">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="c8c62-150">Remplacez hello adresse IP publique de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c8c62-150">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="c8c62-151">Il doit se présenter une image toothis similaire.</span><span class="sxs-lookup"><span data-stu-id="c8c62-151">It should look similar toothis image.</span></span>

![Page d’informations PHP][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a><span data-ttu-id="c8c62-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c8c62-153">Next steps</span></span>

<span data-ttu-id="c8c62-154">Dans ce didacticiel, vous avez déployé un serveur LEMP dans Azure.</span><span class="sxs-lookup"><span data-stu-id="c8c62-154">In this tutorial, you deployed a LEMP server in Azure.</span></span> <span data-ttu-id="c8c62-155">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="c8c62-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c8c62-156">Créer une machine virtuelle Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c8c62-156">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="c8c62-157">Ouvrez le port 80 pour le trafic web</span><span class="sxs-lookup"><span data-stu-id="c8c62-157">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="c8c62-158">Installer NGINX, MySQL et PHP</span><span class="sxs-lookup"><span data-stu-id="c8c62-158">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="c8c62-159">Vérifier l’installation et la configuration</span><span class="sxs-lookup"><span data-stu-id="c8c62-159">Verify installation and configuration</span></span>
> * <span data-ttu-id="c8c62-160">Installation de WordPress sur la pile LEMP hello</span><span class="sxs-lookup"><span data-stu-id="c8c62-160">Install WordPress on hello LEMP stack</span></span>

<span data-ttu-id="c8c62-161">Avancer toolearn de didacticiel suivant toohello comment toosecure les serveurs web avec les certificats SSL.</span><span class="sxs-lookup"><span data-stu-id="c8c62-161">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c8c62-162">Sécuriser un serveur web avec SSL</span><span class="sxs-lookup"><span data-stu-id="c8c62-162">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
