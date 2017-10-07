---
title: "aaaMove fichiers tooand à partir d’ordinateurs virtuels Linux de Azure avec SCP | Documents Microsoft"
description: "Déplacer en toute sécurité les fichiers tooand à partir d’un VM Linux dans Azure en utilisant le SCP et une paire de clés SSH."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a><span data-ttu-id="feb1d-103">Déplacer les fichiers tooand à partir d’un VM Linux à l’aide de SCP</span><span class="sxs-lookup"><span data-stu-id="feb1d-103">Move files tooand from a Linux VM using SCP</span></span>

<span data-ttu-id="feb1d-104">Cet article explique comment toomove des fichiers à partir de votre station de travail des tooan machine virtuelle Linux de Azure, ou à partir d’un Azure machine virtuelle Linux vers le bas tooyour station de travail, à l’aide de la copie sécurisé (SCP).</span><span class="sxs-lookup"><span data-stu-id="feb1d-104">This article shows how toomove files from your workstation up tooan Azure Linux VM, or from an Azure Linux VM down tooyour workstation, using Secure Copy (SCP).</span></span> <span data-ttu-id="feb1d-105">Le déplacement de fichiers entre votre poste de travail et une machine virtuelle Linux, de manière rapide et sécurisée, constitue une partie essentielle de la gestion de votre infrastructure Azure.</span><span class="sxs-lookup"><span data-stu-id="feb1d-105">Moving files between your workstation and a Linux VM, quickly and securely, is critical for managing your Azure infrastructure.</span></span> 

<span data-ttu-id="feb1d-106">Pour cet article, vous avez besoin d’une machine virtuelle Linux déployée dans Azure à l’aide de [fichiers de clés publiques et privées SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="feb1d-106">For this article, you need a Linux VM deployed in Azure using [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="feb1d-107">Vous avez également besoin d’un client SCP pour votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="feb1d-107">You also need an SCP client for your local computer.</span></span> <span data-ttu-id="feb1d-108">Il est construit par-dessus SSH et inclus dans l’interpréteur de commandes Bash hello par défaut de la plupart des ordinateurs Mac et Linux et certains interpréteurs de commandes Windows.</span><span class="sxs-lookup"><span data-stu-id="feb1d-108">It is built on top of SSH and included in hello default Bash shell of most Linux and Mac computers and some Windows shells.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="feb1d-109">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="feb1d-109">Quick commands</span></span>

<span data-ttu-id="feb1d-110">Copier un fichier de configuration toohello Linux VM</span><span class="sxs-lookup"><span data-stu-id="feb1d-110">Copy a file up toohello Linux VM</span></span>

```bash
scp file azureuser@azurehost:directory/targetfile
```

<span data-ttu-id="feb1d-111">Copier un fichier vers le bas à partir de hello Linux VM</span><span class="sxs-lookup"><span data-stu-id="feb1d-111">Copy a file down from hello Linux VM</span></span>

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="feb1d-112">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="feb1d-112">Detailed walkthrough</span></span>

<span data-ttu-id="feb1d-113">Par exemple, nous déplacer un fichier de configuration Azure des tooa Linux VM et par extraction vers le bas un répertoire du fichier journal, à la fois à l’aide de clés CSP et SSH.</span><span class="sxs-lookup"><span data-stu-id="feb1d-113">As examples, we move an Azure configuration file up tooa Linux VM and pull down a log file directory, both using SCP and SSH keys.</span></span>   

## <a name="ssh-key-pair-authentication"></a><span data-ttu-id="feb1d-114">Authentification avec une paire de clés SSH</span><span class="sxs-lookup"><span data-stu-id="feb1d-114">SSH key pair authentication</span></span>

<span data-ttu-id="feb1d-115">SCP utilise SSH pour la couche de transport hello.</span><span class="sxs-lookup"><span data-stu-id="feb1d-115">SCP uses SSH for hello transport layer.</span></span> <span data-ttu-id="feb1d-116">L’authentification sur l’hôte de destination hello hello SSH handles, et il transfère des fichiers hello dans un tunnel chiffré fourni par défaut avec SSH.</span><span class="sxs-lookup"><span data-stu-id="feb1d-116">SSH handles hello authentication on hello destination host, and it moves hello file in an encrypted tunnel provided by default with SSH.</span></span> <span data-ttu-id="feb1d-117">Pour l’authentification SSH, des noms d’utilisateur et des mots de passe peuvent être utilisés.</span><span class="sxs-lookup"><span data-stu-id="feb1d-117">For SSH authentication, usernames and passwords can be used.</span></span> <span data-ttu-id="feb1d-118">Toutefois, l’authentification par clé publique et privée SSH est recommandée en tant que meilleure pratique de sécurité.</span><span class="sxs-lookup"><span data-stu-id="feb1d-118">However, SSH public and private key authentication are recommended as a security best practice.</span></span> <span data-ttu-id="feb1d-119">Une fois que SSH a authentifié les connexion hello, SCP commence alors la copie du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="feb1d-119">Once SSH has authenticated hello connection, SCP then begins copying hello file.</span></span> <span data-ttu-id="feb1d-120">À l’aide d’un correctement configuré `~/.ssh/config` et SSH clés publiques et privées, connexion de hello SCP peuvent être établies en utilisant un nom de serveur (ou adresse IP).</span><span class="sxs-lookup"><span data-stu-id="feb1d-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, hello SCP connection can be established by just using a server name (or IP address).</span></span> <span data-ttu-id="feb1d-121">Si vous avez uniquement une clé SSH, SCP cherche dans hello `~/.ssh/` active et l’utilise en toolog par défaut dans toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="feb1d-121">If you only have one SSH key, SCP looks for it in hello `~/.ssh/` directory, and uses it by default toolog in toohello VM.</span></span>

<span data-ttu-id="feb1d-122">Pour plus d’informations sur la configuration de votre `~/.ssh/config` et les clés publiques et privées SSH, consultez [Créer des clés SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="feb1d-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, see [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="scp-a-file-tooa-linux-vm"></a><span data-ttu-id="feb1d-123">SCP un tooa fichier Linux VM</span><span class="sxs-lookup"><span data-stu-id="feb1d-123">SCP a file tooa Linux VM</span></span>

<span data-ttu-id="feb1d-124">Pour le premier exemple de hello, nous copions un fichier de configuration Azure des tooa VM Linux qui est utilisé toodeploy automation.</span><span class="sxs-lookup"><span data-stu-id="feb1d-124">For hello first example, we copy an Azure configuration file up tooa Linux VM that is used toodeploy automation.</span></span> <span data-ttu-id="feb1d-125">Étant donné que ce fichier contient des informations d’identification d’API Azure, notamment des secrets, sa sécurité est importante.</span><span class="sxs-lookup"><span data-stu-id="feb1d-125">Because this file contains Azure API credentials, which include secrets, security is important.</span></span> <span data-ttu-id="feb1d-126">tunnel chiffré de Hello fournie par SSH protège le contenu hello du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="feb1d-126">hello encrypted tunnel provided by SSH protects hello contents of hello file.</span></span>

<span data-ttu-id="feb1d-127">Hello après la commande copies hello local *.azure/config* tooan machine virtuelle Azure avec le nom de domaine complet du fichier *myserver.eastus.cloudapp.azure.com*. nom d’utilisateur admin hello sur hello machine virtuelle Azure est *azureuser* .</span><span class="sxs-lookup"><span data-stu-id="feb1d-127">hello following command copies hello local *.azure/config* file tooan Azure VM with FQDN *myserver.eastus.cloudapp.azure.com*. hello admin user name on hello Azure VM is *azureuser*.</span></span> <span data-ttu-id="feb1d-128">fichier Hello est ciblé toohello */home/azureuser/* active.</span><span class="sxs-lookup"><span data-stu-id="feb1d-128">hello file is targeted toohello */home/azureuser/* directory.</span></span> <span data-ttu-id="feb1d-129">Substituez vos propres valeurs dans cette commande.</span><span class="sxs-lookup"><span data-stu-id="feb1d-129">Substitute your own values in this command.</span></span>

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a><span data-ttu-id="feb1d-130">Copie sécurisée (SCP) d’un répertoire à partir d’une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="feb1d-130">SCP a directory from a Linux VM</span></span>

<span data-ttu-id="feb1d-131">Pour cet exemple, nous copions un répertoire de fichiers journaux à partir de hello Linux VM tooyour la station de travail vers le bas.</span><span class="sxs-lookup"><span data-stu-id="feb1d-131">For this example, we copy a directory of log files from hello Linux VM down tooyour workstation.</span></span> <span data-ttu-id="feb1d-132">Un fichier journal est susceptible de contenir des données sensibles ou secrètes.</span><span class="sxs-lookup"><span data-stu-id="feb1d-132">A log file may or may not contain sensitive or secret data.</span></span> <span data-ttu-id="feb1d-133">Toutefois, à l’aide de SCP garantit le contenu des fichiers de journaux hello hello est crypté.</span><span class="sxs-lookup"><span data-stu-id="feb1d-133">However, using SCP ensures hello contents of hello log files are encrypted.</span></span> <span data-ttu-id="feb1d-134">L’utilisation de fichiers de SCP tootransfer hello est tooget de façon plus simple de hello hello du répertoire des journaux et des fichiers vers le bas de station de travail tooyour tout en étant sécurisée.</span><span class="sxs-lookup"><span data-stu-id="feb1d-134">Using SCP tootransfer hello files is hello easiest way tooget hello log directory and files down tooyour workstation while also being secure.</span></span>

<span data-ttu-id="feb1d-135">Hello commande suivante copie les fichiers Bonjour */home/azureuser/journaux/* répertoire répertoire /tmp local de hello Azure VM toohello :</span><span class="sxs-lookup"><span data-stu-id="feb1d-135">hello following command copies files in hello */home/azureuser/logs/* directory on hello Azure VM toohello local /tmp directory:</span></span>

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

<span data-ttu-id="feb1d-136">Hello `-r` cli indicateur indique SCP toorecursively copier hello les fichiers et répertoires à partir du point de hello du répertoire hello répertorié dans la commande hello.</span><span class="sxs-lookup"><span data-stu-id="feb1d-136">hello `-r` cli flag instructs SCP toorecursively copy hello files and directories from hello point of hello directory listed in hello command.</span></span>  <span data-ttu-id="feb1d-137">Notez que la syntaxe de ligne de commande de hello est également semblable tooa `cp` copier la commande.</span><span class="sxs-lookup"><span data-stu-id="feb1d-137">Also notice that hello command-line syntax is similar tooa `cp` copy command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="feb1d-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="feb1d-138">Next steps</span></span>

* [<span data-ttu-id="feb1d-139">Gérer les utilisateurs, SSH et vérification ou de réparation des disques sur les machines virtuelles Azure Linux à l’aide de bienvenue de le VMAccess Extension</span><span class="sxs-lookup"><span data-stu-id="feb1d-139">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
