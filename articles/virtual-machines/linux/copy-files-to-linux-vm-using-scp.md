---
title: "Déplacer des fichiers vers et depuis des machines virtuelles Linux Azure avec SCP | Microsoft Docs"
description: "Déplacez, en toute sécurité, des fichiers vers et depuis une machine virtuelle Linux dans Azure à l’aide de SCP et d’une paire de clés SSH."
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
ms.openlocfilehash: 736f7c11ec3de04f1ad52ee29d0a4c952c9b0545
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="move-files-to-and-from-a-linux-vm-using-scp"></a><span data-ttu-id="250d5-103">Déplacer des fichiers vers et depuis une machine virtuelle Linux à l’aide de SCP</span><span class="sxs-lookup"><span data-stu-id="250d5-103">Move files to and from a Linux VM using SCP</span></span>

<span data-ttu-id="250d5-104">Cet article explique comment déplacer des fichiers à partir de votre poste de travail vers une machine virtuelle Linux Azure ou à partir d’une machine virtuelle Linux Azure vers votre poste de travail, à l’aide de la copie sécurisée (SCP).</span><span class="sxs-lookup"><span data-stu-id="250d5-104">This article shows how to move files from your workstation up to an Azure Linux VM, or from an Azure Linux VM down to your workstation, using Secure Copy (SCP).</span></span> <span data-ttu-id="250d5-105">Le déplacement de fichiers entre votre poste de travail et une machine virtuelle Linux, de manière rapide et sécurisée, constitue une partie essentielle de la gestion de votre infrastructure Azure.</span><span class="sxs-lookup"><span data-stu-id="250d5-105">Moving files between your workstation and a Linux VM, quickly and securely, is critical for managing your Azure infrastructure.</span></span> 

<span data-ttu-id="250d5-106">Pour cet article, vous avez besoin d’une machine virtuelle Linux déployée dans Azure à l’aide de [fichiers de clés publiques et privées SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="250d5-106">For this article, you need a Linux VM deployed in Azure using [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="250d5-107">Vous avez également besoin d’un client SCP pour votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="250d5-107">You also need an SCP client for your local computer.</span></span> <span data-ttu-id="250d5-108">Celui-ci est construit par-dessus SSH et inclus dans l’interpréteur de commandes Bash par défaut de la plupart des ordinateurs Mac et Linux et dans certains interpréteurs de commandes Windows.</span><span class="sxs-lookup"><span data-stu-id="250d5-108">It is built on top of SSH and included in the default Bash shell of most Linux and Mac computers and some Windows shells.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="250d5-109">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="250d5-109">Quick commands</span></span>

<span data-ttu-id="250d5-110">Copier un fichier vers la machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="250d5-110">Copy a file up to the Linux VM</span></span>

```bash
scp file azureuser@azurehost:directory/targetfile
```

<span data-ttu-id="250d5-111">Copier un fichier à partir de la machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="250d5-111">Copy a file down from the Linux VM</span></span>

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="250d5-112">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="250d5-112">Detailed walkthrough</span></span>

<span data-ttu-id="250d5-113">Par exemple, nous déplaçons un fichier de configuration Azure vers une machine virtuelle Linux et nous extrayons un répertoire de fichiers journaux, en utilisant à la fois SCP et des clés SSH.</span><span class="sxs-lookup"><span data-stu-id="250d5-113">As examples, we move an Azure configuration file up to a Linux VM and pull down a log file directory, both using SCP and SSH keys.</span></span>   

## <a name="ssh-key-pair-authentication"></a><span data-ttu-id="250d5-114">Authentification avec une paire de clés SSH</span><span class="sxs-lookup"><span data-stu-id="250d5-114">SSH key pair authentication</span></span>

<span data-ttu-id="250d5-115">SCP utilise SSH pour la couche de transport.</span><span class="sxs-lookup"><span data-stu-id="250d5-115">SCP uses SSH for the transport layer.</span></span> <span data-ttu-id="250d5-116">SSH gère l’authentification sur l’hôte de destination, puis déplace le fichier dans un tunnel chiffré fourni par défaut avec SSH.</span><span class="sxs-lookup"><span data-stu-id="250d5-116">SSH handles the authentication on the destination host, and it moves the file in an encrypted tunnel provided by default with SSH.</span></span> <span data-ttu-id="250d5-117">Pour l’authentification SSH, des noms d’utilisateur et des mots de passe peuvent être utilisés.</span><span class="sxs-lookup"><span data-stu-id="250d5-117">For SSH authentication, usernames and passwords can be used.</span></span> <span data-ttu-id="250d5-118">Toutefois, l’authentification par clé publique et privée SSH est recommandée en tant que meilleure pratique de sécurité.</span><span class="sxs-lookup"><span data-stu-id="250d5-118">However, SSH public and private key authentication are recommended as a security best practice.</span></span> <span data-ttu-id="250d5-119">Une fois que SSH a authentifié la connexion, SCP commence à copier le fichier.</span><span class="sxs-lookup"><span data-stu-id="250d5-119">Once SSH has authenticated the connection, SCP then begins copying the file.</span></span> <span data-ttu-id="250d5-120">À l’aide d’une valeur `~/.ssh/config` correctement configurée et de clés publiques et privées SSH, la connexion SCP peut être établie simplement à l’aide d’un nom de serveur (ou d’une adresse IP).</span><span class="sxs-lookup"><span data-stu-id="250d5-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, the SCP connection can be established by just using a server name (or IP address).</span></span> <span data-ttu-id="250d5-121">Si vous n’avez qu’une seule clé SSH, SCP la recherche dans le répertoire `~/.ssh/` et l’utilise par défaut pour se connecter à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="250d5-121">If you only have one SSH key, SCP looks for it in the `~/.ssh/` directory, and uses it by default to log in to the VM.</span></span>

<span data-ttu-id="250d5-122">Pour plus d’informations sur la configuration de votre `~/.ssh/config` et les clés publiques et privées SSH, consultez [Créer des clés SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="250d5-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, see [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="scp-a-file-to-a-linux-vm"></a><span data-ttu-id="250d5-123">Copie sécurisée (SCP) d’un fichier vers une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="250d5-123">SCP a file to a Linux VM</span></span>

<span data-ttu-id="250d5-124">Pour le premier exemple, nous copions un fichier de configuration Azure vers une machine virtuelle Linux qui est utilisée pour déployer l’automatisation.</span><span class="sxs-lookup"><span data-stu-id="250d5-124">For the first example, we copy an Azure configuration file up to a Linux VM that is used to deploy automation.</span></span> <span data-ttu-id="250d5-125">Étant donné que ce fichier contient des informations d’identification d’API Azure, notamment des secrets, sa sécurité est importante.</span><span class="sxs-lookup"><span data-stu-id="250d5-125">Because this file contains Azure API credentials, which include secrets, security is important.</span></span> <span data-ttu-id="250d5-126">Le tunnel chiffré fourni par SSH protège le contenu du fichier.</span><span class="sxs-lookup"><span data-stu-id="250d5-126">The encrypted tunnel provided by SSH protects the contents of the file.</span></span>

<span data-ttu-id="250d5-127">La commande suivante copie le fichier local *.azure/config* vers une machine virtuelle Azure avec le nom de domaine complet *myserver.eastus.cloudapp.azure.com*. Le nom d’utilisateur administrateur sur la machine virtuelle Azure est *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="250d5-127">The following command copies the local *.azure/config* file to an Azure VM with FQDN *myserver.eastus.cloudapp.azure.com*. The admin user name on the Azure VM is *azureuser*.</span></span> <span data-ttu-id="250d5-128">Le fichier est ciblé dans le répertoire */home/azureuser/*.</span><span class="sxs-lookup"><span data-stu-id="250d5-128">The file is targeted to the */home/azureuser/* directory.</span></span> <span data-ttu-id="250d5-129">Substituez vos propres valeurs dans cette commande.</span><span class="sxs-lookup"><span data-stu-id="250d5-129">Substitute your own values in this command.</span></span>

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a><span data-ttu-id="250d5-130">Copie sécurisée (SCP) d’un répertoire à partir d’une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="250d5-130">SCP a directory from a Linux VM</span></span>

<span data-ttu-id="250d5-131">Pour cet exemple, nous copions un répertoire de fichiers journaux à partir de la machine virtuelle Linux sur votre poste de travail.</span><span class="sxs-lookup"><span data-stu-id="250d5-131">For this example, we copy a directory of log files from the Linux VM down to your workstation.</span></span> <span data-ttu-id="250d5-132">Un fichier journal est susceptible de contenir des données sensibles ou secrètes.</span><span class="sxs-lookup"><span data-stu-id="250d5-132">A log file may or may not contain sensitive or secret data.</span></span> <span data-ttu-id="250d5-133">Toutefois, l’utilisation de SCP garantit que le contenu des fichiers journaux est chiffré.</span><span class="sxs-lookup"><span data-stu-id="250d5-133">However, using SCP ensures the contents of the log files are encrypted.</span></span> <span data-ttu-id="250d5-134">L’utilisation de SCP pour transférer les fichiers constitue le moyen le plus simple de copier le répertoire et les fichiers journaux sur votre poste de travail tout en assurant leur sécurité.</span><span class="sxs-lookup"><span data-stu-id="250d5-134">Using SCP to transfer the files is the easiest way to get the log directory and files down to your workstation while also being secure.</span></span>

<span data-ttu-id="250d5-135">La commande suivante copie les fichiers contenus dans le répertoire */home/azureuser/logs/* sur la machine virtuelle Azure dans le répertoire/tmp local :</span><span class="sxs-lookup"><span data-stu-id="250d5-135">The following command copies files in the */home/azureuser/logs/* directory on the Azure VM to the local /tmp directory:</span></span>

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

<span data-ttu-id="250d5-136">L’indicateur de l’interface de ligne de commande `-r` indique à SCP de copier de manière récursive les fichiers et les répertoires à partir du point du répertoire indiqué dans la commande.</span><span class="sxs-lookup"><span data-stu-id="250d5-136">The `-r` cli flag instructs SCP to recursively copy the files and directories from the point of the directory listed in the command.</span></span>  <span data-ttu-id="250d5-137">Notez également que la syntaxe de ligne de commande est similaire à une commande de copie `cp`.</span><span class="sxs-lookup"><span data-stu-id="250d5-137">Also notice that the command-line syntax is similar to a `cp` copy command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="250d5-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="250d5-138">Next steps</span></span>

* [<span data-ttu-id="250d5-139">Gérer les utilisateurs, SSH et vérifier ou réparer les disques de machines virtuelles Azure Linux à l'aide de l’extension VMAccess</span><span class="sxs-lookup"><span data-stu-id="250d5-139">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)