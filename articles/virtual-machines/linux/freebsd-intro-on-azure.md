---
title: tooFreeBSD aaaIntroduction sur Azure | Documents Microsoft
description: "Apprenez à utiliser des machines virtuelles FreeBSD sur Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: 43ba7a70ed21e7fb8b331f4a26db0426e098c4aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a><span data-ttu-id="9ea2e-103">TooFreeBSD introduction sur Azure</span><span class="sxs-lookup"><span data-stu-id="9ea2e-103">Introduction tooFreeBSD on Azure</span></span>
<span data-ttu-id="9ea2e-104">Cette rubrique offre une vue d’ensemble de l’exécution d’une machine virtuelle FreeBSD dans Azure.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="9ea2e-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9ea2e-105">Overview</span></span>
<span data-ttu-id="9ea2e-106">FreeBSD pour Microsoft Azure est qu'un système d’exploitation avancé utilisé toopower les serveurs modernes, les ordinateurs de bureau et les plateformes incorporés.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-106">FreeBSD for Microsoft Azure is an advanced computer operating system used toopower modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="9ea2e-107">Microsoft Corporation est disposition des images de FreeBSD sur Azure avec hello [Agent invité d’ordinateur virtuel Azure](https://github.com/Azure/WALinuxAgent/) préconfiguré.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-107">Microsoft Corporation is making images of FreeBSD available on Azure with hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="9ea2e-108">Actuellement, hello versions FreeBSD suivantes sont proposées en tant qu’images par Microsoft :</span><span class="sxs-lookup"><span data-stu-id="9ea2e-108">Currently, hello following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="9ea2e-109">FreeBSD 10.3-RELEASE</span><span class="sxs-lookup"><span data-stu-id="9ea2e-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="9ea2e-110">FreeBSD 11.0-RELEASE</span><span class="sxs-lookup"><span data-stu-id="9ea2e-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="9ea2e-111">Hello est chargé pour la communication entre hello FreeBSD VM et hello tissu Azure pour les opérations telles que l’approvisionnement hello VM sur la première utilisation (nom d’utilisateur, mot de passe ou clé SSH, nom d’hôte, etc.) et l’activation des fonctionnalités pour les extensions de machine virtuelle sélectives.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-111">hello agent is responsible for communication between hello FreeBSD VM and hello Azure fabric for operations such as provisioning hello VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="9ea2e-112">Comme pour les versions futures de FreeBSD, stratégie de hello est toostay en cours et rendre hello dernières versions disponibles peu de temps après leur publication par l’équipe d’ingénierie hello FreeBSD version.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-112">As for future versions of FreeBSD, hello strategy is toostay current and make hello latest releases available shortly after they are published by hello FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="9ea2e-113">Déploiement d’une machine virtuelle FreeBSD</span><span class="sxs-lookup"><span data-stu-id="9ea2e-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="9ea2e-114">Déploiement d’un ordinateur virtuel de FreeBSD est un processus simple à l’aide d’une image à partir de Bonjour Azure Marketplace de hello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="9ea2e-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from hello Azure Marketplace from hello Azure portal:</span></span>

- [<span data-ttu-id="9ea2e-115">10.3 FreeBSD sur hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="9ea2e-115">FreeBSD 10.3 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="9ea2e-116">11.0 FreeBSD sur hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="9ea2e-116">FreeBSD 11.0 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="9ea2e-117">Créer une machine virtuelle FreeBSD via Azure CLI 2.0 sur FreeBSD</span><span class="sxs-lookup"><span data-stu-id="9ea2e-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="9ea2e-118">Vous devez tout d’abord tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) bien que la commande suivante sur un ordinateur de FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-118">First you need tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="9ea2e-119">Si l’interpréteur de commandes n’est pas installé sur votre ordinateur FreeBSD, exécutez la commande avant l’installation de hello suivante.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-119">If bash is not installed on your FreeBSD machine, run following command before hello installation.</span></span> 

```bash
sudo pkg install bash
```

<span data-ttu-id="9ea2e-120">Si les python n’est pas installé sur votre ordinateur FreeBSD, exécutez suivant les commandes avant l’installation de hello.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-120">If python is not installed on your FreeBSD machine, run following commands before hello installation.</span></span> 

```bash
sudo pkg install python35
cd /usr/local/bin 
sudo rm /usr/local/bin/python 
sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="9ea2e-121">Pendant l’installation de hello, vous êtes invité `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-121">During hello installation, you are asked `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="9ea2e-122">Si vous répondez `y` et entrez `/etc/rc.conf` en tant que `a path tooan rc file tooupdate`, vous pouvez répondre à problème de hello `ERROR: [Errno 13] Permission denied`.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-122">If you answer `y` and enter `/etc/rc.conf` as `a path tooan rc file tooupdate`, you may meet hello problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="9ea2e-123">tooresolve ce problème, vous devez accorder hello écriture toocurrent droit sur le fichier de hello `etc/rc.conf`.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-123">tooresolve this problem, you should grant hello write right toocurrent user against hello file `etc/rc.conf`.</span></span>

<span data-ttu-id="9ea2e-124">Vous pouvez maintenant vous connecter à Azure et créer votre machine virtuelle FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="9ea2e-125">Vous trouverez ci-dessous un exemple toocreate une machine virtuelle 11.0 de FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-125">Below is an example toocreate a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="9ea2e-126">Vous pouvez également ajouter le paramètre hello `--public-ip-address-dns-name` avec un nom DNS globalement unique pour une adresse IP publique nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-126">You can also add hello parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
az login 
az group create --name myResourceGroup --location eastus
az vm create --name myFreeBSD11 \
    --resource-group myResourceGroup \
    --image MicrosoftOSTC:FreeBSD:11.0:latest \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="9ea2e-127">Vous pouvez ensuite vous connecter dans tooyour FreeBSD VM via l’adresse ip hello imprimé dans la sortie de hello d’au-dessus de déploiement.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-127">Then you can log in tooyour FreeBSD VM through hello ip address that printed in hello output of above deployment.</span></span> 

```bash
ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="9ea2e-128">Extension de machine virtuelle pour FreeBSD</span><span class="sxs-lookup"><span data-stu-id="9ea2e-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="9ea2e-129">Voici les extensions de machines virtuelles prises en charge par FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="9ea2e-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="9ea2e-130">VMAccess</span></span>
<span data-ttu-id="9ea2e-131">Hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension peut :</span><span class="sxs-lookup"><span data-stu-id="9ea2e-131">hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="9ea2e-132">Réinitialiser le mot de passe hello d’hello d’origine sudo.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-132">Reset hello password of hello original sudo user.</span></span>
* <span data-ttu-id="9ea2e-133">Créer un nouvel utilisateur de sudo avec mot de passe hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-133">Create a new sudo user with hello password specified.</span></span>
* <span data-ttu-id="9ea2e-134">Définissez la clé d’hôte public hello avec clé hello donné.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-134">Set hello public host key with hello key given.</span></span>
* <span data-ttu-id="9ea2e-135">Réinitialiser la clé d’hôte public hello fournie pendant l’approvisionnement si la clé d’hôte hello n’est pas fournie d’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-135">Reset hello public host key provided during VM provisioning if hello host key is not provided.</span></span>
* <span data-ttu-id="9ea2e-136">Ouvrez le port SSH hello (22) et de restauration hello sshd_config si reset_ssh a la valeur tootrue.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-136">Open hello SSH port (22) and restore hello sshd_config if reset_ssh is set tootrue.</span></span>
* <span data-ttu-id="9ea2e-137">Supprimer un utilisateur existant de hello.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-137">Remove hello existing user.</span></span>
* <span data-ttu-id="9ea2e-138">Vérifier les disques.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-138">Check disks.</span></span>
* <span data-ttu-id="9ea2e-139">Réparer un disque ajouté.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="9ea2e-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="9ea2e-140">CustomScript</span></span>
<span data-ttu-id="9ea2e-141">Hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension peut :</span><span class="sxs-lookup"><span data-stu-id="9ea2e-141">hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="9ea2e-142">Si fourni, télécharger les scripts de hello personnalisé de stockage Azure ou de stockage public externe (par exemple, GitHub).</span><span class="sxs-lookup"><span data-stu-id="9ea2e-142">If provided, download hello customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="9ea2e-143">Exécutez le script de point d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-143">Run hello entry point script.</span></span>
* <span data-ttu-id="9ea2e-144">Prendre en charge les commandes inline.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-144">Support inline commands.</span></span>
* <span data-ttu-id="9ea2e-145">Convertir automatiquement le saut de ligne Windows dans des scripts Shell et Python.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="9ea2e-146">Supprimer automatiquement les nomenclatures dans des scripts Shell et Python.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="9ea2e-147">Protéger les données sensibles dans CommandToExecute.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="9ea2e-148">La machine virtuelle FreeBSD prend uniquement en charge CustomScript version 1.x à ce stade.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="9ea2e-149">Authentification : noms d’utilisateurs, mots de passe et clés SSH</span><span class="sxs-lookup"><span data-stu-id="9ea2e-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="9ea2e-150">Lorsque vous créez une machine virtuelle de FreeBSD à l’aide de hello portail Azure, vous devez fournir un nom d’utilisateur, le mot de passe ou la clé publique SSH.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-150">When you're creating a FreeBSD virtual machine by using hello Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="9ea2e-151">Noms d’utilisateur pour le déploiement d’un ordinateur virtuel de FreeBSD sur Azure ne doivent pas correspondre à des noms des comptes système (UID < 100) déjà présentes dans l’ordinateur virtuel de hello (« root », par exemple).</span><span class="sxs-lookup"><span data-stu-id="9ea2e-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in hello virtual machine ("root", for example).</span></span>
<span data-ttu-id="9ea2e-152">Actuellement, seuls hello RSA de la clé SSH est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-152">Currently, only hello RSA SSH key is supported.</span></span> <span data-ttu-id="9ea2e-153">Une clé SSH multiligne doit commencer par `---- BEGIN SSH2 PUBLIC KEY ----` et se terminer par `---- END SSH2 PUBLIC KEY ----`.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="9ea2e-154">Obtention de privilèges de superutilisateur</span><span class="sxs-lookup"><span data-stu-id="9ea2e-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="9ea2e-155">compte d’utilisateur Hello est spécifié lors du déploiement d’instance de machine virtuelle sur Azure est un compte privilégié.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-155">hello user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="9ea2e-156">package de sudo Hello a été installé dans hello publié FreeBSD image.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-156">hello package of sudo was installed in hello published FreeBSD image.</span></span>
<span data-ttu-id="9ea2e-157">Une fois que vous êtes connecté via ce compte d’utilisateur, vous pouvez exécuter des commandes en tant que racine en utilisant la syntaxe de commande hello.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-157">After you're logged in through this user account, you can run commands as root by using hello command syntax.</span></span>

```
$ sudo <COMMAND>
```

<span data-ttu-id="9ea2e-158">Vous pouvez éventuellement obtenir un interpréteur de commandes root avec `sudo -s`.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="9ea2e-159">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="9ea2e-159">Known issues</span></span>
<span data-ttu-id="9ea2e-160">Hello [Agent invité d’ordinateur virtuel Azure](https://github.com/Azure/WALinuxAgent/) version 2.2.2 a un [problème connu] (https://github.com/Azure/WALinuxAgent/pull/517) qui provoque l’échec de disposition hello pour VM FreeBSD sur Azure.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-160">hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes hello provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="9ea2e-161">Hello correctif a été capturée par [Agent invité d’ordinateur virtuel Azure](https://github.com/Azure/WALinuxAgent/) version 2.2.3 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-161">hello fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9ea2e-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9ea2e-162">Next steps</span></span>
* <span data-ttu-id="9ea2e-163">Accédez trop[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate un VM FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="9ea2e-163">Go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate a FreeBSD VM.</span></span>
* <span data-ttu-id="9ea2e-164">Si vous souhaitez toobring vos propres tooAzure FreeBSD, reportez-vous trop[créer et charger un tooAzure FreeBSD VHD](classic/freebsd-create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="9ea2e-164">If you want toobring your own FreeBSD tooAzure, refer too[Create and upload a FreeBSD VHD tooAzure](classic/freebsd-create-upload-vhd.md).</span></span>
