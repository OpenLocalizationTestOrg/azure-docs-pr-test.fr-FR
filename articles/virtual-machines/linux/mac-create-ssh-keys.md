---
title: "paire de clés aaaCreate et utilisez un SSH pour les machines virtuelles Linux dans Azure | Documents Microsoft"
description: "Comment toocreate et utilisez une paire de clés SSH publique et privée pour les machines virtuelles Linux dans Azure tooimprove hello sécurité hello processus d’authentification."
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
ms.openlocfilehash: 7fb94841d34d5bc006f3134adf91102ddce5f174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a><span data-ttu-id="d2e9a-103">Comment toocreate et utiliser une clé publique et privée de SSH paire pour les machines virtuelles Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="d2e9a-103">How toocreate and use an SSH public and private key pair for Linux VMs in Azure</span></span>
<span data-ttu-id="d2e9a-104">Avec une paire de clés SSH (secure shell), vous pouvez créer des machines virtuelles (VM) dans Azure qui utilisent des clés SSH pour l’authentification, hello inutile toolog des mots de passe dans.</span><span class="sxs-lookup"><span data-stu-id="d2e9a-104">With a secure shell (SSH) key pair, you can create virtual machines (VMs) in Azure that use SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="d2e9a-105">Cet article vous explique comment tooquickly générer et utiliser une paire de fichier de clé publique et privée RSA de SSH protocol version 2 pour les machines virtuelles Linux.</span><span class="sxs-lookup"><span data-stu-id="d2e9a-105">This article shows you how tooquickly generate and use an SSH protocol version 2 RSA public and private key file pair for Linux VMs.</span></span> <span data-ttu-id="d2e9a-106">Pour plus d’étapes et des exemples supplémentaires, consultez [détaillée des paires de clés SSH toocreate étapes et les certificats](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="d2e9a-106">For more detailed steps and additional examples, see [detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

## <a name="create-an-ssh-key-pair"></a><span data-ttu-id="d2e9a-107">Création d’une paire de clés SSH</span><span class="sxs-lookup"><span data-stu-id="d2e9a-107">Create an SSH key pair</span></span>
<span data-ttu-id="d2e9a-108">Hello d’utilisation `ssh-keygen` fichiers de commandes toocreate SSH publiques et privées clés par défaut créé dans hello `~/.ssh` active, mais vous pouvez spécifier un autre emplacement et le mot de passe supplémentaire (un mot de passe tooaccess hello fichier de clé privée) lors de la vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="d2e9a-108">Use hello `ssh-keygen` command toocreate SSH public and private key files that are by default created in hello `~/.ssh` directory, but you can specify a different location and additional passphrase (a password tooaccess hello private key file) when prompted.</span></span> <span data-ttu-id="d2e9a-109">Exécutez hello commande suivante à partir d’un interpréteur de commandes Bash, répondre aux invites hello avec vos propres informations.</span><span class="sxs-lookup"><span data-stu-id="d2e9a-109">Run hello following command from a Bash shell, answering hello prompts with your own information.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a><span data-ttu-id="d2e9a-110">Utilisez la paire de clés SSH hello</span><span class="sxs-lookup"><span data-stu-id="d2e9a-110">Use hello SSH key pair</span></span>
<span data-ttu-id="d2e9a-111">clé publique Hello que vous placez sur votre VM Linux dans Azure est stocké par défaut dans `~/.ssh/id_rsa.pub`, sauf si vous avez modifié les emplacement hello lorsque vous les avez créés.</span><span class="sxs-lookup"><span data-stu-id="d2e9a-111">hello public key that you place on your Linux VM in Azure is by default stored in `~/.ssh/id_rsa.pub`, unless you changed hello location when you created them.</span></span> <span data-ttu-id="d2e9a-112">Si vous utilisez hello [Azure CLI 2.0](/cli/azure) toocreate votre machine virtuelle, spécifiez l’emplacement hello de cette clé publique lorsque vous utilisez hello [az vm créer](/cli/azure/vm#create) avec hello `--ssh-key-path` option.</span><span class="sxs-lookup"><span data-stu-id="d2e9a-112">If you use hello [Azure CLI 2.0](/cli/azure) toocreate your VM, specify hello location of this public key when you use hello [az vm create](/cli/azure/vm#create) with hello `--ssh-key-path` option.</span></span> <span data-ttu-id="d2e9a-113">Si vous copiez et collez contenu hello de toouse du fichier de clé publique hello hello portail Azure ou d’un modèle de gestionnaire de ressources, assurez-vous que vous ne copiez pas les espaces blancs supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="d2e9a-113">If you copy and paste hello contents of hello public key file toouse in hello Azure portal or a Resource Manager template, make sure you don't copy any additional whitespace.</span></span> <span data-ttu-id="d2e9a-114">Par exemple, si vous utilisez OS X, vous pouvez diriger le fichier de clé publique hello (par défaut, **~/.ssh/id_rsa.pub**) trop**pbcopy** toocopy contenu de hello (des autres programmes Linux hello même chose, tel que `xclip`).</span><span class="sxs-lookup"><span data-stu-id="d2e9a-114">For example, if you use OS X, you can pipe hello public key file (by default, **~/.ssh/id_rsa.pub**) too**pbcopy** toocopy hello contents (there are other Linux programs that do hello same thing, such as `xclip`).</span></span>

<span data-ttu-id="d2e9a-115">Si vous n’êtes pas familiarisé avec les clés publiques SSH, vous pouvez voir votre clé publique en exécutant `cat` comme suit, en remplaçant `~/.ssh/id_rsa.pub` par l’emplacement de votre propre fichier de clé publique :</span><span class="sxs-lookup"><span data-stu-id="d2e9a-115">If you're not familiar with SSH public keys, you can see your public key by running `cat` as follows, replacing `~/.ssh/id_rsa.pub` with your own public key file location:</span></span>

```bash
cat ~/.ssh/id_rsa.pub
```

<span data-ttu-id="d2e9a-116">Avec la clé publique de hello sur votre machine virtuelle Azure, à l’aide de SSH tooyour VM hello adresse IP ou nom DNS de votre machine virtuelle (n’oubliez pas de tooreplace `azureuser` et `myvm.westus.cloudapp.azure.com` ci-dessous avec le nom d’utilisateur de hello administrateur ou une adresse IP et nom de domaine complet de hello--adresse) :</span><span class="sxs-lookup"><span data-stu-id="d2e9a-116">With hello public key on your Azure VM, SSH tooyour VM using hello IP address or DNS name of your VM (remember tooreplace `azureuser` and `myvm.westus.cloudapp.azure.com` below with hello admin username and hello fully qualified domain name -- or IP address):</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="d2e9a-117">Si vous avez fourni un mot de passe lorsque vous avez créé votre paire de clés, entrez la phrase secrète de hello lorsque vous y êtes invité au cours du processus de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="d2e9a-117">If you provided a passphrase when you created your key pair, enter hello passphrase when prompted during hello login process.</span></span> <span data-ttu-id="d2e9a-118">(serveur de hello est ajouté tooyour `~/.ssh/known_hosts` dossier et que vous ne vous demandera tooconnect à nouveau jusqu'à ce que la clé publique de hello sur vos modifications de la machine virtuelle Azure ou le nom du serveur hello est supprimé de `~/.ssh/known_hosts`.)</span><span class="sxs-lookup"><span data-stu-id="d2e9a-118">(hello server is added tooyour `~/.ssh/known_hosts` folder, and you won't be asked tooconnect again until hello public key on your Azure VM changes or hello server name is removed from `~/.ssh/known_hosts`.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d2e9a-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d2e9a-119">Next steps</span></span>

<span data-ttu-id="d2e9a-120">Machines virtuelles créées à l’aide de clés SSH sont par défaut configuré avec des mots de passe désactivés, toomake cassée estimation tente considérablement plus coûteux et par conséquent difficile.</span><span class="sxs-lookup"><span data-stu-id="d2e9a-120">VMs created using SSH keys are by default configured with passwords disabled, toomake brute-forced guessing attempts vastly more expensive and therefore difficult.</span></span> <span data-ttu-id="d2e9a-121">Cette rubrique décrit la création d’une simple paire de clés SSH dans le cadre d’une utilisation rapide.</span><span class="sxs-lookup"><span data-stu-id="d2e9a-121">This topic describes creating a simple SSH key pair for quick usage.</span></span> <span data-ttu-id="d2e9a-122">Si vous avez besoin d’assistance pour la création de votre paire de clés SSH ou exiger des certificats supplémentaires, consultez [détaillée des paires de clés SSH toocreate étapes et les certificats](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="d2e9a-122">If you need more assistance in creating your SSH key pair or require additional certificates, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

<span data-ttu-id="d2e9a-123">Vous pouvez créer des ordinateurs virtuels qui utilisent votre paire de clés SSH à l’aide de hello portail Azure, CLI et les modèles :</span><span class="sxs-lookup"><span data-stu-id="d2e9a-123">You can create VMs that use your SSH key pair using hello Azure portal, CLI, and templates:</span></span>

* [<span data-ttu-id="d2e9a-124">Créer une VM Linux sécurisé à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="d2e9a-124">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="d2e9a-125">Créer une VM Linux sécurisé à l’aide de hello Azure CLI 2.0)</span><span class="sxs-lookup"><span data-stu-id="d2e9a-125">Create a secure Linux VM using hello Azure CLI 2.0)</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="d2e9a-126">Créer une machine virtuelle Linux sécurisée à l’aide d’un modèle Azure</span><span class="sxs-lookup"><span data-stu-id="d2e9a-126">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
