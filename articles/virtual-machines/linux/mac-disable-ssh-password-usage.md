---
title: les mots de passe SSH aaaDisable sur votre VM Linux en configurant SSHD | Documents Microsoft
description: "Sécurisez votre machine virtuelle Linux sur Azure en désactivant les connexions par mot de passe pour SSH."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: 
ms.assetid: 46137640-a7d2-40e5-a1e9-9effef7eb190
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/26/2016
ms.author: v-livech
ms.openlocfilehash: fb67b2f5b8b3bf2ba214858940b04f2ea9013fb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a><span data-ttu-id="4e11c-103">Désactiver les mots de passe SSH sur votre machine virtuelle Linux en configurant SSHD</span><span class="sxs-lookup"><span data-stu-id="4e11c-103">Disable SSH passwords on your Linux VM by configuring SSHD</span></span>
<span data-ttu-id="4e11c-104">Cet article se concentre sur la façon de toolock la sécurité de connexion hello de votre VM Linux.</span><span class="sxs-lookup"><span data-stu-id="4e11c-104">This article focuses on how toolock down hello login security of your Linux VM.</span></span>  <span data-ttu-id="4e11c-105">Dès que hello SSH port 22 est ouvert toohello world robots commencent la tentative de toologin par des mots de passe de déchiffrement.</span><span class="sxs-lookup"><span data-stu-id="4e11c-105">As soon as hello SSH port 22 is opened toohello world bots start trying toologin by guessing passwords.</span></span>  <span data-ttu-id="4e11c-106">Cet article décrit comment désactiver les connexions par mot de passe sur SSH.</span><span class="sxs-lookup"><span data-stu-id="4e11c-106">What we will do in this article is disable password logins over SSH.</span></span>  <span data-ttu-id="4e11c-107">Attaque par des mots de passe toouse nous protéger hello Linux VM à partir de ce type d’attaque en force supprimant complètement la possibilité de hello.</span><span class="sxs-lookup"><span data-stu-id="4e11c-107">By completely removing hello ability toouse passwords we protect hello Linux VM from this type of brute force attack.</span></span>  <span data-ttu-id="4e11c-108">Hello ajouté bonus est, nous allons configurer SSHD Linux tooonly autoriser les connexions via SSH les clés privés et publics, hello loin tooLinux de toologin de manière plus sécurisée.</span><span class="sxs-lookup"><span data-stu-id="4e11c-108">hello added bonus is we will configure Linux SSHD tooonly allow logins via SSH public & private keys, by far hello most secure way toologin tooLinux.</span></span>  <span data-ttu-id="4e11c-109">les combinaisons possibles Hello de celui-ci nécessiterait la clé privée de tooguess hello est considérable et par conséquent déconseille robots à partir de la même déranger tootry toobrute force SSH clés.</span><span class="sxs-lookup"><span data-stu-id="4e11c-109">hello possible combinations of it would require tooguess hello private key is immense and therefore discourages bots from even bothering tootry toobrute force SSH keys.</span></span>

## <a name="goals"></a><span data-ttu-id="4e11c-110">Objectifs</span><span class="sxs-lookup"><span data-stu-id="4e11c-110">Goals</span></span>
* <span data-ttu-id="4e11c-111">Configurer SSHD toodisallow :</span><span class="sxs-lookup"><span data-stu-id="4e11c-111">Configure SSHD toodisallow:</span></span>
  * <span data-ttu-id="4e11c-112">Connexions par mot de passe</span><span class="sxs-lookup"><span data-stu-id="4e11c-112">Password logins</span></span>
  * <span data-ttu-id="4e11c-113">Connexion de l’utilisateur racine</span><span class="sxs-lookup"><span data-stu-id="4e11c-113">Root user login</span></span>
  * <span data-ttu-id="4e11c-114">Authentification par stimulation/réponse</span><span class="sxs-lookup"><span data-stu-id="4e11c-114">Challenge-response authentication</span></span>
* <span data-ttu-id="4e11c-115">Configurer SSHD tooallow :</span><span class="sxs-lookup"><span data-stu-id="4e11c-115">Configure SSHD tooallow:</span></span>
  * <span data-ttu-id="4e11c-116">Uniquement les connexions par clés SSH</span><span class="sxs-lookup"><span data-stu-id="4e11c-116">only SSH key logins</span></span>
* <span data-ttu-id="4e11c-117">Redémarrage de SSHD quand la session est encore ouverte</span><span class="sxs-lookup"><span data-stu-id="4e11c-117">Restart SSHD while still logged in</span></span>
* <span data-ttu-id="4e11c-118">Configuration de test hello nouvelle SSHD</span><span class="sxs-lookup"><span data-stu-id="4e11c-118">Test hello new SSHD configuration</span></span>

## <a name="introduction"></a><span data-ttu-id="4e11c-119">Introduction</span><span class="sxs-lookup"><span data-stu-id="4e11c-119">Introduction</span></span>
[<span data-ttu-id="4e11c-120">Définition de SSH</span><span class="sxs-lookup"><span data-stu-id="4e11c-120">SSH defined</span></span>](https://en.wikipedia.org/wiki/Secure_Shell)

<span data-ttu-id="4e11c-121">SSHD est hello serveur SSH qui s’exécute sur hello Linux VM.</span><span class="sxs-lookup"><span data-stu-id="4e11c-121">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="4e11c-122">SSH est un client qui s’exécute à partir d’un interpréteur de commandes sur votre poste de travail MacBook ou Linux.</span><span class="sxs-lookup"><span data-stu-id="4e11c-122">SSH is a client that runs from a shell on your MacBook or Linux workstation.</span></span>  <span data-ttu-id="4e11c-123">SSH est également hello protocole utilisé toosecure et chiffrer la communication hello entre votre station de travail et les hello Linux VM.</span><span class="sxs-lookup"><span data-stu-id="4e11c-123">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM.</span></span>

<span data-ttu-id="4e11c-124">Pour cet article, il est très important tookeep une connexion tooyour est VM Linux ouvert pour l’ensemble de hello guident.</span><span class="sxs-lookup"><span data-stu-id="4e11c-124">For this article it is very important tookeep one login tooyour Linux VM open for hello entire walk through.</span></span>  <span data-ttu-id="4e11c-125">Pour cette raison, nous allons ouvrir deux terminaux et SSH toohello Linux VM à partir des deux d'entre eux.</span><span class="sxs-lookup"><span data-stu-id="4e11c-125">For this reason we will open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="4e11c-126">Nous utilise hello premier toomake terminal hello modifications tooSSHDs fichier de configuration et redémarrez le service SSHD hello.</span><span class="sxs-lookup"><span data-stu-id="4e11c-126">We will use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="4e11c-127">Nous allons utiliser hello tootest terminal deuxième celles modifie une fois le redémarrage du service hello.</span><span class="sxs-lookup"><span data-stu-id="4e11c-127">We will use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="4e11c-128">Étant donné que nous allons la désactivation des mots de passe SSH et partie de confiance strictement sur les clés SSH, si vos clés SSH ne sont pas corrects et que vous fermez hello connexion toohello machine virtuelle, hello machine virtuelle seront définitivement verrouillé et aucun sera tooit toologin en mesure de rendre obligatoire toobe supprimé et recréé.</span><span class="sxs-lookup"><span data-stu-id="4e11c-128">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e11c-129">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4e11c-129">Prerequisites</span></span>
* [<span data-ttu-id="4e11c-130">Créer des clés SSH sur Linux et Mac pour les machines virtuelles Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="4e11c-130">Create SSH keys on Linux and Mac for Linux VMs in Azure</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="4e11c-131">Compte Azure</span><span class="sxs-lookup"><span data-stu-id="4e11c-131">Azure account</span></span>
  * [<span data-ttu-id="4e11c-132">Version d’évaluation gratuite</span><span class="sxs-lookup"><span data-stu-id="4e11c-132">free trial signup</span></span>](https://azure.microsoft.com/pricing/free-trial/)
  * [<span data-ttu-id="4e11c-133">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="4e11c-133">Azure portal</span></span>](http://portal.azure.com)
* <span data-ttu-id="4e11c-134">Machine virtuelle Linux s’exécutant sur Azure</span><span class="sxs-lookup"><span data-stu-id="4e11c-134">Linux VM running on azure</span></span>
* <span data-ttu-id="4e11c-135">Paire de clés publique et privée SSH dans `~/.ssh/`</span><span class="sxs-lookup"><span data-stu-id="4e11c-135">SSH public & private key pair in `~/.ssh/`</span></span>
* <span data-ttu-id="4e11c-136">Dans la clé publique SSH `~/.ssh/authorized_keys` sur hello Linux VM</span><span class="sxs-lookup"><span data-stu-id="4e11c-136">SSH public key in `~/.ssh/authorized_keys` on hello Linux VM</span></span>
* <span data-ttu-id="4e11c-137">Droits de sudo sur hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="4e11c-137">Sudo rights on hello VM</span></span>
* <span data-ttu-id="4e11c-138">Port 22 ouvert</span><span class="sxs-lookup"><span data-stu-id="4e11c-138">Port 22 open</span></span>

## <a name="quick-commands"></a><span data-ttu-id="4e11c-139">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="4e11c-139">Quick Commands</span></span>
<span data-ttu-id="4e11c-140">*Les administrateurs Linux expérimentés souhaitant simplement de la version TLDR hello, commencez ici.  Pour tout le monde afin de pouvoir hello explication détaillée et procédure pas à pas ignorer cette section.*</span><span class="sxs-lookup"><span data-stu-id="4e11c-140">*Seasoned Linux Admins who just want hello TLDR version start here.  For everyone else that wants hello detailed explanation and walk through skip this section.*</span></span>

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="4e11c-141">Modifiez le fichier de configuration hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4e11c-141">Edit hello config file as follows:</span></span>

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no

# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes

# Change PermitRootLogin toothis:
PermitRootLogin no

# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

<span data-ttu-id="4e11c-142">Redémarrez le service SSHD hello.</span><span class="sxs-lookup"><span data-stu-id="4e11c-142">Restart hello SSHD service.</span></span> <span data-ttu-id="4e11c-143">Sur les distributions basées sur Debian :</span><span class="sxs-lookup"><span data-stu-id="4e11c-143">On Debian-based distros:</span></span>

```bash
sudo service ssh restart
```

<span data-ttu-id="4e11c-144">Sur les distributions basées sur Red Hat :</span><span class="sxs-lookup"><span data-stu-id="4e11c-144">On Red Hat-based distros:</span></span>

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a><span data-ttu-id="4e11c-145">Procédure pas à pas détaillée</span><span class="sxs-lookup"><span data-stu-id="4e11c-145">Detailed Walk Through</span></span>
<span data-ttu-id="4e11c-146">Connexion toohello Linux VM sur terminal 1 (T1).</span><span class="sxs-lookup"><span data-stu-id="4e11c-146">Login toohello Linux VM on terminal 1 (T1).</span></span>  <span data-ttu-id="4e11c-147">Connexion toohello Linux VM sur 2 terminal (T2).</span><span class="sxs-lookup"><span data-stu-id="4e11c-147">Login toohello Linux VM on terminal 2 (T2).</span></span>

<span data-ttu-id="4e11c-148">Dans T2, nous allons fichier de configuration SSHD tooedit hello.</span><span class="sxs-lookup"><span data-stu-id="4e11c-148">On T2 we are going tooedit hello SSHD configuration file.</span></span>  

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="4e11c-149">À partir d’ici, nous modifier simplement hello paramètres toodisable des mots de passe et activer les connexions de clé SSH.</span><span class="sxs-lookup"><span data-stu-id="4e11c-149">From here we will edit just hello settings toodisable passwords and enable SSH key logins.</span></span>  <span data-ttu-id="4e11c-150">Il existe de nombreux paramètres dans ce fichier que vous devez rechercher et modifier toomake Linux & SSH aussi sécurisée que nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4e11c-150">There are many settings in this file that you should research and change toomake Linux & SSH as secure as you need.</span></span>

#### <a name="disable-password-logins"></a><span data-ttu-id="4e11c-151">Désactiver les connexions par mot de passe</span><span class="sxs-lookup"><span data-stu-id="4e11c-151">Disable Password logins</span></span>

```sh
# Change PasswordAuthentication toothis:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a><span data-ttu-id="4e11c-152">Activer l’authentification par clé publique</span><span class="sxs-lookup"><span data-stu-id="4e11c-152">Enable Public Key Authentication</span></span>

```sh
# Change PubkeyAuthentication toothis:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a><span data-ttu-id="4e11c-153">Désactiver la connexion racine</span><span class="sxs-lookup"><span data-stu-id="4e11c-153">Disable Root Login</span></span>

```sh
# Change PermitRootLogin toothis:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a><span data-ttu-id="4e11c-154">Désactiver l’authentification par stimulation/réponse</span><span class="sxs-lookup"><span data-stu-id="4e11c-154">Disable Challenge-response Authentication</span></span>
```sh
# Change ChallengeResponseAuthentication toothis:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a><span data-ttu-id="4e11c-155">Redémarrer SSHD</span><span class="sxs-lookup"><span data-stu-id="4e11c-155">Restart SSHD</span></span>
<span data-ttu-id="4e11c-156">À partir de l’interpréteur de commandes hello T1, vérifiez que vous êtes toujours connecté.</span><span class="sxs-lookup"><span data-stu-id="4e11c-156">From hello T1 shell verify that you are still logged in.</span></span>  <span data-ttu-id="4e11c-157">Cela est essentiel pour continuer à avoir accès à votre machine virtuelle si vos clés SSH ne sont pas correctes, car les mots de passe sont désormais désactivés.</span><span class="sxs-lookup"><span data-stu-id="4e11c-157">This is critical so you do not get locked out of your VM if your SSH keys are not correct since passwords are now disabled.</span></span>  <span data-ttu-id="4e11c-158">Si les paramètres sont incorrects sur votre VM Linux vous pouvez utiliser T1 toofix sshd_config, vous êtes toujours connecté et SSH conservera les connexion hello actif pendant hello les service SSHD redémarrer.</span><span class="sxs-lookup"><span data-stu-id="4e11c-158">If any setting are incorrect on your Linux VM you can use T1 toofix sshd_config as you will still be logged in and SSH will keep hello connection alive during hello SSHD service restart.</span></span>

<span data-ttu-id="4e11c-159">À partir de T2, effectuez l’exécution :</span><span class="sxs-lookup"><span data-stu-id="4e11c-159">From T2 run:</span></span>

##### <a name="on-hello-debian-family"></a><span data-ttu-id="4e11c-160">Sur hello Debian famille</span><span class="sxs-lookup"><span data-stu-id="4e11c-160">On hello Debian Family</span></span>
```bash
sudo service ssh restart
```

##### <a name="on-hello-redhat-family"></a><span data-ttu-id="4e11c-161">Sur hello RedHat famille</span><span class="sxs-lookup"><span data-stu-id="4e11c-161">On hello RedHat Family</span></span>
```bash
sudo service sshd restart
```

<span data-ttu-id="4e11c-162">Les mots de passe sont désormais désactivés sur votre machine virtuelle, ce qui la protège contre les tentatives d’attaque par force brute des connexions par mot de passe.</span><span class="sxs-lookup"><span data-stu-id="4e11c-162">Passwords are now disabled on your VM protecting it from brute force password login attempts.</span></span>  <span data-ttu-id="4e11c-163">Avec uniquement SSH clés autorisée, vous serez en mesure de toologin plus rapide et plus sûre.</span><span class="sxs-lookup"><span data-stu-id="4e11c-163">With only SSH Keys allowed you will be able toologin faster and much more secure.</span></span>

