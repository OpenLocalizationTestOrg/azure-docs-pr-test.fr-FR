---
title: "FEU d’aaaDeploy sur un ordinateur virtuel de Linux dans Azure | Documents Microsoft"
description: Didacticiel - pile LAMP installation hello un VM Linux dans Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: a3d0ecb3277f15bd0a2fdc0d85b738a760e68865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a><span data-ttu-id="af57a-103">Installer un serveur web LAMP sur une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="af57a-103">Install a LAMP web server on an Azure VM</span></span>
<span data-ttu-id="af57a-104">Cet article vous guide tout au long de comment toodeploy un Apache web server, MySQL et PHP (pile de feu hello) sur un VM Ubuntu dans Azure.</span><span class="sxs-lookup"><span data-stu-id="af57a-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="af57a-105">Si vous préférez le serveur de web NGINX hello, consultez hello [pile LEMP](tutorial-lemp-stack.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="af57a-105">If you prefer hello NGINX web server, see hello [LEMP stack](tutorial-lemp-stack.md) tutorial.</span></span> <span data-ttu-id="af57a-106">serveur de feu toosee hello dans action, vous pouvez éventuellement installer et configurer un site WordPress.</span><span class="sxs-lookup"><span data-stu-id="af57a-106">toosee hello LAMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="af57a-107">Ce didacticiel vous explique comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="af57a-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="af57a-108">Créer une VM Ubuntu (hello « L » dans la pile de feu hello)</span><span class="sxs-lookup"><span data-stu-id="af57a-108">Create an Ubuntu VM (hello 'L' in hello LAMP stack)</span></span>
> * <span data-ttu-id="af57a-109">Ouvrez le port 80 pour le trafic web</span><span class="sxs-lookup"><span data-stu-id="af57a-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="af57a-110">Installer Apache, MySQL et PHP</span><span class="sxs-lookup"><span data-stu-id="af57a-110">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="af57a-111">Vérifier l’installation et la configuration</span><span class="sxs-lookup"><span data-stu-id="af57a-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="af57a-112">Installation de WordPress sur le serveur de feu hello</span><span class="sxs-lookup"><span data-stu-id="af57a-112">Install WordPress on hello LAMP server</span></span>


<span data-ttu-id="af57a-113">Pour plus d’informations sur la pile de feu hello, notamment des recommandations pour un environnement de production, consultez hello [Ubuntu documentation](https://help.ubuntu.com/community/ApacheMySQLPHP).</span><span class="sxs-lookup"><span data-stu-id="af57a-113">For more on hello LAMP stack, including recommendations for a production environment, see hello [Ubuntu documentation](https://help.ubuntu.com/community/ApacheMySQLPHP).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="af57a-114">Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="af57a-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="af57a-115">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="af57a-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="af57a-116">Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="af57a-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a><span data-ttu-id="af57a-117">Installer Apache, MySQL et PHP</span><span class="sxs-lookup"><span data-stu-id="af57a-117">Install Apache, MySQL, and PHP</span></span>

<span data-ttu-id="af57a-118">Exécutez hello commande tooupdate Ubuntu package sources suivantes et installer PHP, MySQL et Apache.</span><span class="sxs-lookup"><span data-stu-id="af57a-118">Run hello following command tooupdate Ubuntu package sources and install Apache, MySQL, and PHP.</span></span> <span data-ttu-id="af57a-119">Notez hello du point d’insertion (^) à fin hello de commande hello.</span><span class="sxs-lookup"><span data-stu-id="af57a-119">Note hello caret (^) at hello end of hello command.</span></span>


```bash
sudo apt update && sudo apt install lamp-server^
```



<span data-ttu-id="af57a-120">Vous êtes invité à tooinstall hello packages et autres dépendances.</span><span class="sxs-lookup"><span data-stu-id="af57a-120">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="af57a-121">Lorsque vous y êtes invité, définissez un mot de passe racine MySQL, puis sur [Entrée] toocontinue.</span><span class="sxs-lookup"><span data-stu-id="af57a-121">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="af57a-122">Suivez hello restant d’invites.</span><span class="sxs-lookup"><span data-stu-id="af57a-122">Follow hello remaining prompts.</span></span> <span data-ttu-id="af57a-123">Ce processus installe hello minimale requise PHP les extensions nécessitées toouse PHP avec MySQL.</span><span class="sxs-lookup"><span data-stu-id="af57a-123">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![Page de mot de passe racine MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="af57a-125">Vérifier l’installation et la configuration</span><span class="sxs-lookup"><span data-stu-id="af57a-125">Verify installation and configuration</span></span>


### <a name="apache"></a><span data-ttu-id="af57a-126">Apache</span><span class="sxs-lookup"><span data-stu-id="af57a-126">Apache</span></span>

<span data-ttu-id="af57a-127">Vérifier la version de hello d’Apache avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="af57a-127">Check hello version of Apache with hello following command:</span></span>
```bash
apache2 -v
```

<span data-ttu-id="af57a-128">Avec Apache installés et le port 80 ouvrez tooyour machine virtuelle, de serveur web de hello désormais accessibles à partir de hello internet.</span><span class="sxs-lookup"><span data-stu-id="af57a-128">With Apache installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="af57a-129">tooview hello Apache2 Ubuntu par défaut Page, ouvrez un navigateur web et entrez les adresse IP publique hello Hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="af57a-129">tooview hello Apache2 Ubuntu Default Page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="af57a-130">Utilisez l’adresse IP publique de hello, vous avez utilisé tooSSH toohello machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="af57a-130">Use hello public IP address you used tooSSH toohello VM:</span></span>

![Page par défaut d’Apache][3]


### <a name="mysql"></a><span data-ttu-id="af57a-132">MySQL</span><span class="sxs-lookup"><span data-stu-id="af57a-132">MySQL</span></span>

<span data-ttu-id="af57a-133">Vérifiez la version hello de MySQL avec hello commande suivante (Notez majuscules de hello `V` paramètre) :</span><span class="sxs-lookup"><span data-stu-id="af57a-133">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="af57a-134">Nous vous recommandons d’exécuter hello après l’installation de hello sécurisé toohelp script de MySQL :</span><span class="sxs-lookup"><span data-stu-id="af57a-134">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="af57a-135">Entrez votre mot de passe racine MySQL et configurer les paramètres de sécurité hello pour votre environnement.</span><span class="sxs-lookup"><span data-stu-id="af57a-135">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="af57a-136">Si vous souhaitez toocreate une base de données MySQL, ajouter des utilisateurs, ou modifier les paramètres de configuration, tooMySQL de connexion :</span><span class="sxs-lookup"><span data-stu-id="af57a-136">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="af57a-137">Lorsque vous avez terminé, quittez hello mysql invite en tapant `\q`.</span><span class="sxs-lookup"><span data-stu-id="af57a-137">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="af57a-138">PHP</span><span class="sxs-lookup"><span data-stu-id="af57a-138">PHP</span></span>

<span data-ttu-id="af57a-139">Vérifier la version de hello de PHP avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="af57a-139">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="af57a-140">Si vous souhaitez davantage de tootest, créez un tooview de page PHP info rapide dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="af57a-140">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="af57a-141">Hello commande suivante crée la page des informations hello PHP :</span><span class="sxs-lookup"><span data-stu-id="af57a-141">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

<span data-ttu-id="af57a-142">Vous pouvez maintenant vérifier page des informations de PHP hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="af57a-142">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="af57a-143">Ouvrez un navigateur et allez trop`http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="af57a-143">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="af57a-144">Remplacez hello adresse IP publique de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="af57a-144">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="af57a-145">Il doit se présenter une image toothis similaire.</span><span class="sxs-lookup"><span data-stu-id="af57a-145">It should look similar toothis image.</span></span>

![Page d’informations PHP][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a><span data-ttu-id="af57a-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="af57a-147">Next steps</span></span>

<span data-ttu-id="af57a-148">Dans ce didacticiel, vous avez déployé un serveur LAMP dans Azure.</span><span class="sxs-lookup"><span data-stu-id="af57a-148">In this tutorial, you deployed a LAMP server in Azure.</span></span> <span data-ttu-id="af57a-149">Vous avez appris à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="af57a-149">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="af57a-150">Créer une machine virtuelle Ubuntu</span><span class="sxs-lookup"><span data-stu-id="af57a-150">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="af57a-151">Ouvrez le port 80 pour le trafic web</span><span class="sxs-lookup"><span data-stu-id="af57a-151">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="af57a-152">Installer Apache, MySQL et PHP</span><span class="sxs-lookup"><span data-stu-id="af57a-152">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="af57a-153">Vérifier l’installation et la configuration</span><span class="sxs-lookup"><span data-stu-id="af57a-153">Verify installation and configuration</span></span>
> * <span data-ttu-id="af57a-154">Installation de WordPress sur le serveur de feu hello</span><span class="sxs-lookup"><span data-stu-id="af57a-154">Install WordPress on hello LAMP server</span></span>

<span data-ttu-id="af57a-155">Avancer toolearn de didacticiel suivant toohello comment toosecure les serveurs web avec les certificats SSL.</span><span class="sxs-lookup"><span data-stu-id="af57a-155">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="af57a-156">Sécuriser un serveur web avec SSL</span><span class="sxs-lookup"><span data-stu-id="af57a-156">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png