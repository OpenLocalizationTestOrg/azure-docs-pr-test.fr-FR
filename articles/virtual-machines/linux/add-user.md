---
title: aaaAdd un tooa utilisateur VM Linux sur Azure | Documents Microsoft
description: Ajouter un tooa utilisateur Linux VM sur Azure.
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: eed050154adf0cbed2c168e7aa675bd3ded85fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-user-tooan-azure-vm"></a><span data-ttu-id="1aa33-103">Ajouter une machine virtuelle Azure de tooan utilisateur</span><span class="sxs-lookup"><span data-stu-id="1aa33-103">Add a user tooan Azure VM</span></span>
<span data-ttu-id="1aa33-104">Une des tâches de premier hello sur n’importe quel VM Linux nouvelle est toocreate un nouvel utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1aa33-104">One of hello first tasks on any new Linux VM is toocreate a new user.</span></span>  <span data-ttu-id="1aa33-105">Dans cet article, nous Apprenez à créer un compte d’utilisateur sudo, le paramètre hello un mot de passe, ajouter des clés publiques SSH et enfin utiliser `visudo` sudo tooallow sans mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1aa33-105">In this article, we walk through creating a sudo user account, setting hello password, adding SSH Public Keys, and finally use `visudo` tooallow sudo without a password.</span></span>

<span data-ttu-id="1aa33-106">Conditions préalables sont : [un compte Azure](https://azure.microsoft.com/pricing/free-trial/), [les clés publiques et privées SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), un groupe de ressources Azure hello CLI d’Azure installé et à l’aide de mode de gestionnaire de ressources tooAzure `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="1aa33-106">Prerequisites are: [an Azure account](https://azure.microsoft.com/pricing/free-trial/), [SSH public and private keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), an Azure resource group, and hello Azure CLI installed and switched tooAzure Resource Manager mode using `azure config mode arm`.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="1aa33-107">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="1aa33-107">Quick Commands</span></span>
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy hello SSH Public Key toohello new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers tooallow no password
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify hello SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="1aa33-108">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="1aa33-108">Detailed Walkthrough</span></span>
### <a name="introduction"></a><span data-ttu-id="1aa33-109">Introduction</span><span class="sxs-lookup"><span data-stu-id="1aa33-109">Introduction</span></span>
<span data-ttu-id="1aa33-110">L’une des tâches de premier et le plus courant hello avec un nouveau serveur est tooadd un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1aa33-110">One of hello first and most common task with a new server is tooadd a user account.</span></span>  <span data-ttu-id="1aa33-111">Connexions d’accès racine doivent être désactivées et compte de racine de hello lui-même ne doit pas être utilisé avec votre serveur Linux, sudo uniquement.</span><span class="sxs-lookup"><span data-stu-id="1aa33-111">Root logins should be disabled and hello root account itself should not be used with your Linux server, only sudo.</span></span>  <span data-ttu-id="1aa33-112">En donnant une escalade de verrous racine utilisateur des privilèges à l’aide de sudo elle hello tooadminister de manière appropriée et Linux.</span><span class="sxs-lookup"><span data-stu-id="1aa33-112">Giving a user root escalation privileges using sudo it hello proper way tooadminister and use Linux.</span></span>

<span data-ttu-id="1aa33-113">À l’aide de la commande hello `useradd` toohello de comptes d’utilisateur Linux VM, nous avons ajouté.</span><span class="sxs-lookup"><span data-stu-id="1aa33-113">Using hello command `useradd` we are adding user accounts toohello Linux VM.</span></span>  <span data-ttu-id="1aa33-114">L’exécution de `useradd` modifie `/etc/passwd`, `/etc/shadow`, `/etc/group` et `/etc/gshadow`.</span><span class="sxs-lookup"><span data-stu-id="1aa33-114">Running `useradd` modifies `/etc/passwd`, `/etc/shadow`, `/etc/group`, and `/etc/gshadow`.</span></span>  <span data-ttu-id="1aa33-115">Nous avons ajouté un indicateur de ligne de commande de toohello `useradd` commande tooalso ajouter hello toohello sudo bon groupe d’utilisateurs sur Linux.</span><span class="sxs-lookup"><span data-stu-id="1aa33-115">We are adding a command-line flag toohello `useradd` command tooalso add hello new user toohello proper sudo group on Linux.</span></span>  <span data-ttu-id="1aa33-116">Même thou `useradd` crée une entrée dans `/etc/passwd` il ne donne pas nouveau compte d’utilisateur hello un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1aa33-116">Even thou `useradd` creates an entry into `/etc/passwd` it does not give hello new user account a password.</span></span>  <span data-ttu-id="1aa33-117">Nous allons créer un mot de passe initial hello nouvel utilisateur à l’aide de hello simple `passwd` commande.</span><span class="sxs-lookup"><span data-stu-id="1aa33-117">We are creating an initial password for hello new user using hello simple `passwd` command.</span></span>  <span data-ttu-id="1aa33-118">dernière étape de Hello est toomodify hello sudo règles tooallow qui tooexecute les commandes utilisateur avec des privilèges sudo sans avoir à tooenter un mot de passe pour chaque commande.</span><span class="sxs-lookup"><span data-stu-id="1aa33-118">hello last step is toomodify hello sudo rules tooallow that user tooexecute commands with sudo privileges without having tooenter a password for every command.</span></span>  <span data-ttu-id="1aa33-119">Connexion à l’aide de la clé privée de hello présumée ce compte d’utilisateur est protégée contre les mauvais acteurs et allez un accès sudo tooallow sans mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1aa33-119">Logging in using hello Private key we are assuming that user account is safe from bad actors and are going tooallow sudo access without a password.</span></span>  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a><span data-ttu-id="1aa33-120">Ajout d’un tooan d’utilisateur unique sudo machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="1aa33-120">Adding a single sudo user tooan Azure VM</span></span>
<span data-ttu-id="1aa33-121">Ouvrez une session dans toohello machine virtuelle Azure à l’aide de clés SSH.</span><span class="sxs-lookup"><span data-stu-id="1aa33-121">Log in toohello Azure VM using SSH keys.</span></span>  <span data-ttu-id="1aa33-122">Si vous n’avez pas configuré un accès par clé publique SSH, commencez par lire entièrement l’article [Utilisation d’une authentification par clé publique avec Azure](http://link.to/article).</span><span class="sxs-lookup"><span data-stu-id="1aa33-122">If you have not setup SSH public key access, complete this article first [Using Public Key Authentication with Azure](http://link.to/article).</span></span>  

<span data-ttu-id="1aa33-123">Hello `useradd` commande termine hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="1aa33-123">hello `useradd` command completes hello following tasks:</span></span>

* <span data-ttu-id="1aa33-124">créer un compte d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="1aa33-124">create a new user account</span></span>
* <span data-ttu-id="1aa33-125">créer un groupe d’utilisateurs avec hello même nom</span><span class="sxs-lookup"><span data-stu-id="1aa33-125">create a new user group with hello same name</span></span>
* <span data-ttu-id="1aa33-126">Ajouter une entrée vide trop`/etc/passwd`</span><span class="sxs-lookup"><span data-stu-id="1aa33-126">add a blank entry too`/etc/passwd`</span></span>
* <span data-ttu-id="1aa33-127">Ajouter une entrée vide trop`/etc/gpasswd`</span><span class="sxs-lookup"><span data-stu-id="1aa33-127">add a blank entry too`/etc/gpasswd`</span></span>

<span data-ttu-id="1aa33-128">Hello `-G` indicateur de ligne de commande ajoute hello utilisateur compte toohello correcte d’un groupe Linux attribution de privilèges d’escalade de verrous de racine de nouveau compte d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="1aa33-128">hello `-G` command-line flag adds hello new user account toohello proper Linux group giving hello new user account root escalation privileges.</span></span>

#### <a name="add-hello-user"></a><span data-ttu-id="1aa33-129">Ajouter un utilisateur de hello</span><span class="sxs-lookup"><span data-stu-id="1aa33-129">Add hello user</span></span>
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a><span data-ttu-id="1aa33-130">Définir le mot de passe</span><span class="sxs-lookup"><span data-stu-id="1aa33-130">Set a password</span></span>
<span data-ttu-id="1aa33-131">Hello `useradd` commande hello crée et ajoute une entrée tooboth `/etc/passwd` et `/etc/gpasswd` mais ne définit ne pas réellement le mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="1aa33-131">hello `useradd` command creates hello user and adds an entry tooboth `/etc/passwd` and `/etc/gpasswd` but does not actually set hello password.</span></span>  <span data-ttu-id="1aa33-132">Hello mot de passe est ajouté toohello entrée à l’aide de hello `passwd` commande.</span><span class="sxs-lookup"><span data-stu-id="1aa33-132">hello password is added toohello entry using hello `passwd` command.</span></span>

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

<span data-ttu-id="1aa33-133">Nous disposons désormais d’un utilisateur avec des privilèges sudo sur un serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="1aa33-133">We now have a user with sudo privileges on hello server.</span></span>

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a><span data-ttu-id="1aa33-134">Ajoutez votre clé publique SSH toohello nouveau compte d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="1aa33-134">Add your SSH Public Key toohello new user account</span></span>
<span data-ttu-id="1aa33-135">À partir de votre ordinateur, utilisez hello `ssh-copy-id` avec le nouveau mot de passe hello.</span><span class="sxs-lookup"><span data-stu-id="1aa33-135">From your machine, use hello `ssh-copy-id` command with hello new password.</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a><span data-ttu-id="1aa33-136">Utilisation visudo tooallow sudo sans mot de passe</span><span class="sxs-lookup"><span data-stu-id="1aa33-136">Using visudo tooallow sudo usage without a password</span></span>
<span data-ttu-id="1aa33-137">À l’aide de `visudo` tooedit hello `/etc/sudoers` fichier ajoute plusieurs couches de protection contre la modification incorrecte de ce fichier important.</span><span class="sxs-lookup"><span data-stu-id="1aa33-137">Using `visudo` tooedit hello `/etc/sudoers` file adds a few layers of protection against incorrectly modifying this important file.</span></span>  <span data-ttu-id="1aa33-138">Lors de l’exécution `visudo`, hello `/etc/sudoers` fichier est verrouillé tooensure aucun autre utilisateur ne peut apporter des modifications pendant qu’il est activement en cours de modification.</span><span class="sxs-lookup"><span data-stu-id="1aa33-138">Upon executing `visudo`, hello `/etc/sudoers` file is locked tooensure no other user can make changes while it is actively being edited.</span></span>  <span data-ttu-id="1aa33-139">Hello `/etc/sudoers` le fichier est extrait également les erreurs par `visudo` lorsque vous essayez de toosave ou se fermer : Impossible d’enregistrer un fichier de programmes sudo rompue.</span><span class="sxs-lookup"><span data-stu-id="1aa33-139">hello `/etc/sudoers` file is also checked for mistakes by `visudo` when you attempt toosave or exit so you cannot save a broken sudoers file.</span></span>

<span data-ttu-id="1aa33-140">Nous avons déjà les utilisateurs de groupe par défaut correcte de hello pour un accès sudo.</span><span class="sxs-lookup"><span data-stu-id="1aa33-140">We already have users in hello correct default group for sudo access.</span></span>  <span data-ttu-id="1aa33-141">Nous allons maintenant tooenable ces groupes de sudo toouse sans mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1aa33-141">Now we are going tooenable those groups toouse sudo with no password.</span></span>

```bash
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-hello-user-ssh-keys-and-sudo"></a><span data-ttu-id="1aa33-142">Vérifiez les utilisateur hello, ssh clés et sudo</span><span class="sxs-lookup"><span data-stu-id="1aa33-142">Verify hello user, ssh keys, and sudo</span></span>
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
