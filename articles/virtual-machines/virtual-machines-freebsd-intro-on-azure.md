---
title: "Présentation FreeBSD dans Azure | Microsoft Docs"
description: "Apprenez à utiliser des machines virtuelles FreeBSD sur Azure"
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: d0fc5de34f7d9e5a607495eb97d9e35dc9eb21f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-freebsd-on-azure"></a><span data-ttu-id="6c408-103">Présentation de FreeBSD sur Azure</span><span class="sxs-lookup"><span data-stu-id="6c408-103">Introduction to FreeBSD on Azure</span></span>
<span data-ttu-id="6c408-104">Cette rubrique offre une vue d’ensemble de l’exécution d’une machine virtuelle FreeBSD dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6c408-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="6c408-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6c408-105">Overview</span></span>
<span data-ttu-id="6c408-106">FreeBSD pour Microsoft Azure est un système d’exploitation informatique avancé utilisé sur les serveurs, ordinateurs de bureau et plateformes intégrées modernes.</span><span class="sxs-lookup"><span data-stu-id="6c408-106">FreeBSD for Microsoft Azure is an advanced computer operating system used to power modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="6c408-107">Microsoft Corporation rend disponibles des images de FreeBSD sur Azure avec [l’Agent invité de machine virtuelle Azure](https://github.com/Azure/WALinuxAgent/) préconfiguré.</span><span class="sxs-lookup"><span data-stu-id="6c408-107">Microsoft Corporation is making images of FreeBSD available on Azure with the [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="6c408-108">Actuellement, les versions FreeBSD suivantes sont proposées sous forme d’images par Microsoft :</span><span class="sxs-lookup"><span data-stu-id="6c408-108">Currently, the following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="6c408-109">FreeBSD 10.3-RELEASE</span><span class="sxs-lookup"><span data-stu-id="6c408-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="6c408-110">FreeBSD 11.0-RELEASE</span><span class="sxs-lookup"><span data-stu-id="6c408-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="6c408-111">L’agent est responsable de la communication entre la machine virtuelle FreeBSD et Azure Fabric pour les opérations telles que l’approvisionnement de la machine virtuelle à la première utilisation (nom d’utilisateur, mot de passe ou clé SSH, nom d’hôte, etc.) et l’activation de fonctionnalités pour certaines extensions de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6c408-111">The agent is responsible for communication between the FreeBSD VM and the Azure fabric for operations such as provisioning the VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="6c408-112">Comme pour les versions futures de FreeBSD, la stratégie consiste à rester à jour et à rendre disponibles les dernières versions dès qu’elles sont publiées par l’équipe d’ingénieurs de lancement de FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="6c408-112">As for future versions of FreeBSD, the strategy is to stay current and make the latest releases available shortly after they are published by the FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="6c408-113">Déploiement d’une machine virtuelle FreeBSD</span><span class="sxs-lookup"><span data-stu-id="6c408-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="6c408-114">Le déploiement d’une machine virtuelle FreeBSD est un processus simple qui utilise une image provenant de la Place de marché ’Azure sur le portail Azure :</span><span class="sxs-lookup"><span data-stu-id="6c408-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from the Azure Marketplace from the Azure portal:</span></span>

- [<span data-ttu-id="6c408-115">FreeBSD 10.3 sur Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="6c408-115">FreeBSD 10.3 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="6c408-116">FreeBSD 11.0 sur Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="6c408-116">FreeBSD 11.0 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="6c408-117">Créer une machine virtuelle FreeBSD via Azure CLI 2.0 sur FreeBSD</span><span class="sxs-lookup"><span data-stu-id="6c408-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="6c408-118">Vous devez d’abord installer [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) via la commande suivante sur un ordinateur FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="6c408-118">First you need to install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
    curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="6c408-119">Si l’interpréteur de commandes n’est pas installé sur votre ordinateur FreeBSD, exécutez la commande suivante avant l’installation.</span><span class="sxs-lookup"><span data-stu-id="6c408-119">If bash is not installed on your FreeBSD machine, run following command before the installation.</span></span> 

```
    sudo pkg install bash
```

<span data-ttu-id="6c408-120">Si python n’est pas installé sur votre ordinateur FreeBSD, exécutez les commandes suivantes avant l’installation.</span><span class="sxs-lookup"><span data-stu-id="6c408-120">If python is not installed on your FreeBSD machine, run following commands before the installation.</span></span> 

```
    sudo pkg install python35
    cd /usr/local/bin 
    sudo rm /usr/local/bin/python 
    sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="6c408-121">Pendant l’installation, vous devez répondre à la question suivante : `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span><span class="sxs-lookup"><span data-stu-id="6c408-121">During the installation, you are asked `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="6c408-122">Si vous répondez `y` et que vous entrez `/etc/rc.conf` comme `a path to an rc file to update`, vous pouvez rencontrer le problème suivant : `ERROR: [Errno 13] Permission denied`.</span><span class="sxs-lookup"><span data-stu-id="6c408-122">If you answer `y` and enter `/etc/rc.conf` as `a path to an rc file to update`, you may meet the problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="6c408-123">Pour résoudre ce problème, vous devez accorder le droit d’écriture à l’utilisateur actif pour le fichier `etc/rc.conf`.</span><span class="sxs-lookup"><span data-stu-id="6c408-123">To resolve this problem, you should grant the write right to current user against the file `etc/rc.conf`.</span></span>

<span data-ttu-id="6c408-124">Vous pouvez maintenant vous connecter à Azure et créer votre machine virtuelle FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="6c408-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="6c408-125">Voici un exemple de création d’une machine virtuelle FreeBSD 11.0.</span><span class="sxs-lookup"><span data-stu-id="6c408-125">Below is an example to create a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="6c408-126">Vous pouvez également ajouter le paramètre `--public-ip-address-dns-name` avec un nom DNS global unique pour une adresse IP publique nouvellement créée.</span><span class="sxs-lookup"><span data-stu-id="6c408-126">You can also add the parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
    az login 
    az group create -n myResourceGroup -l westus az vm create -n myFreeBSD11 -g myResourceGroup --image MicrosoftOSTC:FreeBSD:11.0:latest --admin-username azureuser --ssh-key-value /etc/ssh/ssh_host_rsa_key.pub 
```

<span data-ttu-id="6c408-127">Vous pouvez ensuite vous connecter à votre machine virtuelle FreeBSD via l’adresse IP qui figure dans la sortie du déploiement ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="6c408-127">Then you can log in to your FreeBSD VM through the ip address that printed in the output of above deployment.</span></span> 

```bash
    ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="6c408-128">Extension de machine virtuelle pour FreeBSD</span><span class="sxs-lookup"><span data-stu-id="6c408-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="6c408-129">Voici les extensions de machines virtuelles prises en charge par FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="6c408-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="6c408-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="6c408-130">VMAccess</span></span>
<span data-ttu-id="6c408-131">L’extension [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) peut :</span><span class="sxs-lookup"><span data-stu-id="6c408-131">The [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="6c408-132">Réinitialiser le mot de passe de l’utilisateur sudo d’origine.</span><span class="sxs-lookup"><span data-stu-id="6c408-132">Reset the password of the original sudo user.</span></span>
* <span data-ttu-id="6c408-133">Créer un nouvel utilisateur sudo avec le mot de passe spécifié.</span><span class="sxs-lookup"><span data-stu-id="6c408-133">Create a new sudo user with the password specified.</span></span>
* <span data-ttu-id="6c408-134">Définir une clé hôte publique donnée.</span><span class="sxs-lookup"><span data-stu-id="6c408-134">Set the public host key with the key given.</span></span>
* <span data-ttu-id="6c408-135">Réinitialiser la clé hôte publique fournie pendant l’approvisionnement de la machine virtuelle si la clé hôte n’est pas fournie.</span><span class="sxs-lookup"><span data-stu-id="6c408-135">Reset the public host key provided during VM provisioning if the host key is not provided.</span></span>
* <span data-ttu-id="6c408-136">Ouvrir le port SSH (22) et restaurer sshd_config si reset_ssh a la valeur True.</span><span class="sxs-lookup"><span data-stu-id="6c408-136">Open the SSH port (22) and restore the sshd_config if reset_ssh is set to true.</span></span>
* <span data-ttu-id="6c408-137">Supprimer l’utilisateur existant.</span><span class="sxs-lookup"><span data-stu-id="6c408-137">Remove the existing user.</span></span>
* <span data-ttu-id="6c408-138">Vérifier les disques.</span><span class="sxs-lookup"><span data-stu-id="6c408-138">Check disks.</span></span>
* <span data-ttu-id="6c408-139">Réparer un disque ajouté.</span><span class="sxs-lookup"><span data-stu-id="6c408-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="6c408-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="6c408-140">CustomScript</span></span>
<span data-ttu-id="6c408-141">L’extension [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) peut :</span><span class="sxs-lookup"><span data-stu-id="6c408-141">The [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="6c408-142">Télécharger les scripts personnalisés dans le stockage Azure ou un stockage public externe (par exemple, GitHub) s’ils sont fournis.</span><span class="sxs-lookup"><span data-stu-id="6c408-142">If provided, download the customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="6c408-143">Exécuter le script de point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="6c408-143">Run the entry point script.</span></span>
* <span data-ttu-id="6c408-144">Prendre en charge les commandes inline.</span><span class="sxs-lookup"><span data-stu-id="6c408-144">Support inline commands.</span></span>
* <span data-ttu-id="6c408-145">Convertir automatiquement le saut de ligne Windows dans des scripts Shell et Python.</span><span class="sxs-lookup"><span data-stu-id="6c408-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="6c408-146">Supprimer automatiquement les nomenclatures dans des scripts Shell et Python.</span><span class="sxs-lookup"><span data-stu-id="6c408-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="6c408-147">Protéger les données sensibles dans CommandToExecute.</span><span class="sxs-lookup"><span data-stu-id="6c408-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="6c408-148">La machine virtuelle FreeBSD prend uniquement en charge CustomScript version 1.x à ce stade.</span><span class="sxs-lookup"><span data-stu-id="6c408-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="6c408-149">Authentification : noms d’utilisateurs, mots de passe et clés SSH</span><span class="sxs-lookup"><span data-stu-id="6c408-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="6c408-150">Lorsque vous créez une machine virtuelle FreeBSD avec le Portail Azure, vous devez fournir un nom d’utilisateur, un mot de passe ou une clé publique SSH.</span><span class="sxs-lookup"><span data-stu-id="6c408-150">When you're creating a FreeBSD virtual machine by using the Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="6c408-151">Le nom d’utilisateur pour le déploiement d’une machine virtuelle FreeBSD sur Azure ne doit pas correspondre au nom des comptes système (UID < 100) déjà présents sur la machine virtuelle (« root », par exemple).</span><span class="sxs-lookup"><span data-stu-id="6c408-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in the virtual machine ("root", for example).</span></span>
<span data-ttu-id="6c408-152">Actuellement, seule la règle RSA SSH est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="6c408-152">Currently, only the RSA SSH key is supported.</span></span> <span data-ttu-id="6c408-153">Une clé SSH multiligne doit commencer par `---- BEGIN SSH2 PUBLIC KEY ----` et se terminer par `---- END SSH2 PUBLIC KEY ----`.</span><span class="sxs-lookup"><span data-stu-id="6c408-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="6c408-154">Obtention de privilèges de superutilisateur</span><span class="sxs-lookup"><span data-stu-id="6c408-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="6c408-155">Le compte utilisateur qui est spécifié pendant le déploiement de l'instance de machine virtuelle dans Azure est un compte privilégié.</span><span class="sxs-lookup"><span data-stu-id="6c408-155">The user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="6c408-156">Le package de « sudo » a été installé dans l’image FreeBSD publiée.</span><span class="sxs-lookup"><span data-stu-id="6c408-156">The package of sudo was installed in the published FreeBSD image.</span></span>
<span data-ttu-id="6c408-157">Une fois connecté avec ce compte utilisateur, vous pouvez exécuter les commandes en tant que root avec la syntaxe de commande.</span><span class="sxs-lookup"><span data-stu-id="6c408-157">After you're logged in through this user account, you can run commands as root by using the command syntax.</span></span>

```
    $ sudo <COMMAND>
```

<span data-ttu-id="6c408-158">Vous pouvez éventuellement obtenir un interpréteur de commandes root avec `sudo -s`.</span><span class="sxs-lookup"><span data-stu-id="6c408-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="6c408-159">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="6c408-159">Known issues</span></span>
<span data-ttu-id="6c408-160">L’[Agent invité de machine virtuelle Azure](https://github.com/Azure/WALinuxAgent/) version 2.2.2 présente un problème [connu] (https://github.com/Azure/WALinuxAgent/pull/517) qui provoque l’échec de l’approvisionnement pour la machine virtuelle FreeBSD sur Azure.</span><span class="sxs-lookup"><span data-stu-id="6c408-160">The [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes the provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="6c408-161">Le correctif a été capturé par l’[Agent invité de machine virtuelle Azure](https://github.com/Azure/WALinuxAgent/) 2.2.3 et versions ultérieures.</span><span class="sxs-lookup"><span data-stu-id="6c408-161">The fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6c408-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6c408-162">Next steps</span></span>
* <span data-ttu-id="6c408-163">Accédez à [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) pour créer une machine virtuelle FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="6c408-163">Go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) to create a FreeBSD VM.</span></span>
* <span data-ttu-id="6c408-164">Si vous souhaitez utiliser votre propre FreeBSD dans Azure, consultez [Créer et charger un VHD FreeBSD dans Azure](linux/classic/freebsd-create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="6c408-164">If you want to bring your own FreeBSD to Azure, refer to [Create and upload a FreeBSD VHD to Azure](linux/classic/freebsd-create-upload-vhd.md).</span></span>
