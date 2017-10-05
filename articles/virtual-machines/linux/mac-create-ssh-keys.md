---
title: "Créer et utiliser une paire de clés SSH pour les machines virtuelles Linux dans Azure | Microsoft Docs"
description: "Comment créer et utiliser une paire de clés publique et privée SSH pour les machines virtuelles Linux dans Azure afin d’améliorer la sécurité du processus d’authentification."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: iainfou
ms.openlocfilehash: 0fb71d2ffe533afba6e1e527b727a7b085e7da14
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-create-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a><span data-ttu-id="f9615-103">Comment créer et utiliser une paire de clés publique et privée SSHpour les machines virtuelles Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="f9615-103">How to create and use an SSH public and private key pair for Linux VMs in Azure</span></span>
<span data-ttu-id="f9615-104">Avec une paire de clés SSH (secure shell), vous pouvez créer des machines virtuelles sur Azure qui utilisent par défaut des clés SSH pour l’authentification, éliminant ainsi la nécessité de recourir aux mots de passe pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="f9615-104">With a secure shell (SSH) key pair, you can create virtual machines (VMs) in Azure that use SSH keys for authentication, eliminating the need for passwords to log in.</span></span> <span data-ttu-id="f9615-105">Cet article vous indique comment générer et utiliser rapidement une paire de clés publique et privée SSH RSA de version de protocole 2 pour des machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="f9615-105">This article shows you how to quickly generate and use an SSH protocol version 2 RSA public and private key file pair for Linux VMs.</span></span> <span data-ttu-id="f9615-106">Pour accéder à une procédure plus détaillée et à des exemples supplémentaires, consultez la [procédure détaillée de création de paires de clés SSH et de certificats](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="f9615-106">For more detailed steps and additional examples, see [detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

## <a name="create-an-ssh-key-pair"></a><span data-ttu-id="f9615-107">Création d’une paire de clés SSH</span><span class="sxs-lookup"><span data-stu-id="f9615-107">Create an SSH key pair</span></span>
<span data-ttu-id="f9615-108">Utilisez la commande `ssh-keygen` pour créer des fichiers de clés publique et privée SSH qui, par défaut, sont créés dans le répertoire `~/.ssh`, mais vous pouvez spécifier un autre emplacement et une phrase secrète supplémentaire (un mot de passe permettant d’accéder au fichier de clé privée) lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="f9615-108">Use the `ssh-keygen` command to create SSH public and private key files that are by default created in the `~/.ssh` directory, but you can specify a different location and additional passphrase (a password to access the private key file) when prompted.</span></span> <span data-ttu-id="f9615-109">Exécutez la commande suivante à partir d’un shell Bash et répondez aux invites avec vos propres informations.</span><span class="sxs-lookup"><span data-stu-id="f9615-109">Run the following command from a Bash shell, answering the prompts with your own information.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-the-ssh-key-pair"></a><span data-ttu-id="f9615-110">Utilisation de la paire de clés SSH</span><span class="sxs-lookup"><span data-stu-id="f9615-110">Use the SSH key pair</span></span>
<span data-ttu-id="f9615-111">La clé publique que vous placez sur votre machine virtuelle Linux dans Azure est stockée par défaut dans `~/.ssh/id_rsa.pub`, sauf si vous avez modifié l’emplacement au moment de sa création.</span><span class="sxs-lookup"><span data-stu-id="f9615-111">The public key that you place on your Linux VM in Azure is by default stored in `~/.ssh/id_rsa.pub`, unless you changed the location when you created them.</span></span> <span data-ttu-id="f9615-112">Si vous utilisez [Azure CLI 2.0](/cli/azure) pour créer votre machine virtuelle, spécifiez l’emplacement de cette clé publique lorsque vous utilisez la commande [az vm create](/cli/azure/vm#create) avec l’option `--ssh-key-path`.</span><span class="sxs-lookup"><span data-stu-id="f9615-112">If you use the [Azure CLI 2.0](/cli/azure) to create your VM, specify the location of this public key when you use the [az vm create](/cli/azure/vm#create) with the `--ssh-key-path` option.</span></span> <span data-ttu-id="f9615-113">Si vous copiez et collez le contenu du fichier de clé publique pour l’utiliser dans le portail Azure ou dans un modèle Resource Manager, veillez à ne pas copier pas les espaces blancs supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="f9615-113">If you copy and paste the contents of the public key file to use in the Azure portal or a Resource Manager template, make sure you don't copy any additional whitespace.</span></span> <span data-ttu-id="f9615-114">Par exemple, si vous utilisez OS X, vous pouvez diriger le fichier de clé publique (par défaut, **~/.ssh/id_rsa.pub**) sur **pbcopy** pour en copier le contenu (d’autres programmes Linux, par exemple `xclip`, peuvent être utilisés à cette fin).</span><span class="sxs-lookup"><span data-stu-id="f9615-114">For example, if you use OS X, you can pipe the public key file (by default, **~/.ssh/id_rsa.pub**) to **pbcopy** to copy the contents (there are other Linux programs that do the same thing, such as `xclip`).</span></span>

<span data-ttu-id="f9615-115">Si vous n’êtes pas familiarisé avec les clés publiques SSH, vous pouvez voir votre clé publique en exécutant `cat` comme suit, en remplaçant `~/.ssh/id_rsa.pub` par l’emplacement de votre propre fichier de clé publique :</span><span class="sxs-lookup"><span data-stu-id="f9615-115">If you're not familiar with SSH public keys, you can see your public key by running `cat` as follows, replacing `~/.ssh/id_rsa.pub` with your own public key file location:</span></span>

```bash
cat ~/.ssh/id_rsa.pub
```

<span data-ttu-id="f9615-116">Avec la clé publique sur votre machine virtuelle Azure, appliquez le protocole SSH sur votre machine virtuelle à l’aide de l’adresse IP ou du nom DNS de votre machine virtuelle (n’oubliez pas de remplacer `azureuser` et `myvm.westus.cloudapp.azure.com` ci-dessous par le nom d’utilisateur administrateur et par le nom de domaine complet, ou par l’adresse IP) :</span><span class="sxs-lookup"><span data-stu-id="f9615-116">With the public key on your Azure VM, SSH to your VM using the IP address or DNS name of your VM (remember to replace `azureuser` and `myvm.westus.cloudapp.azure.com` below with the admin username and the fully qualified domain name -- or IP address):</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="f9615-117">Si vous avez fourni un mot de passe lorsque vous avez créé votre paire de clés, saisissez-le lorsque vous y êtes invité pendant le processus de connexion.</span><span class="sxs-lookup"><span data-stu-id="f9615-117">If you provided a passphrase when you created your key pair, enter the passphrase when prompted during the login process.</span></span> <span data-ttu-id="f9615-118">(Le serveur est ajouté à votre dossier `~/.ssh/known_hosts` et vous n’avez pas à vous connecter à nouveau tant que la clé publique sur votre machine virtuelle Azure n’est pas modifiée ou que le nom de serveur n’est pas supprimé du dossier `~/.ssh/known_hosts`.)</span><span class="sxs-lookup"><span data-stu-id="f9615-118">(The server is added to your `~/.ssh/known_hosts` folder, and you won't be asked to connect again until the public key on your Azure VM changes or the server name is removed from `~/.ssh/known_hosts`.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9615-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f9615-119">Next steps</span></span>

<span data-ttu-id="f9615-120">Les machines virtuelles créées à l’aide de clés SSH sont par défaut configurées avec les mots de passe désactivés, ce qui rend les tentatives de déchiffrement par force brute bien plus coûteuses et par conséquent difficiles.</span><span class="sxs-lookup"><span data-stu-id="f9615-120">VMs created using SSH keys are by default configured with passwords disabled, to make brute-forced guessing attempts vastly more expensive and therefore difficult.</span></span> <span data-ttu-id="f9615-121">Cette rubrique décrit la création d’une simple paire de clés SSH dans le cadre d’une utilisation rapide.</span><span class="sxs-lookup"><span data-stu-id="f9615-121">This topic describes creating a simple SSH key pair for quick usage.</span></span> <span data-ttu-id="f9615-122">Si vous avez besoin d’assistance lors de la création de votre paire de clés SSH ou si vous avez besoin de certificats supplémentaires, consultez [les étapes détaillées pour créer des paires de clés SSH et des certificats](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="f9615-122">If you need more assistance in creating your SSH key pair or require additional certificates, see [Detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

<span data-ttu-id="f9615-123">Vous pouvez créer des machines virtuelles qui utilisent votre paire de clés SSH à l’aide du portail Azure, de l’interface de ligne de commande et de modèles :</span><span class="sxs-lookup"><span data-stu-id="f9615-123">You can create VMs that use your SSH key pair using the Azure portal, CLI, and templates:</span></span>

* [<span data-ttu-id="f9615-124">Créer une machine virtuelle Linux à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="f9615-124">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f9615-125">Création d’une machine virtuelle Linux à l’aide de l’interface Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f9615-125">Create a secure Linux VM using the Azure CLI 2.0)</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="f9615-126">Créer une machine virtuelle Linux sécurisée à l’aide d’un modèle Azure</span><span class="sxs-lookup"><span data-stu-id="f9615-126">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
