---
title: "Désactiver les mots de passe SSH sur votre machine virtuelle Linux en configurant SSHD | Microsoft Docs"
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
ms.openlocfilehash: dc45a1cdce29cef061acc5c7e5b15d9d89265cd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="disable-ssh-passwords-on-your-linux-vm-by-configuring-sshd"></a><span data-ttu-id="124ae-103">Désactiver les mots de passe SSH sur votre machine virtuelle Linux en configurant SSHD</span><span class="sxs-lookup"><span data-stu-id="124ae-103">Disable SSH passwords on your Linux VM by configuring SSHD</span></span>
<span data-ttu-id="124ae-104">Cet article traite du verrouillage de la sécurité de connexion de votre machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="124ae-104">This article focuses on how to lock down the login security of your Linux VM.</span></span>  <span data-ttu-id="124ae-105">Dès que le port SSH 22 est ouvert, les robots tentent de se connecter en devinant le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="124ae-105">As soon as the SSH port 22 is opened to the world bots start trying to login by guessing passwords.</span></span>  <span data-ttu-id="124ae-106">Cet article décrit comment désactiver les connexions par mot de passe sur SSH.</span><span class="sxs-lookup"><span data-stu-id="124ae-106">What we will do in this article is disable password logins over SSH.</span></span>  <span data-ttu-id="124ae-107">En supprimant complètement la possibilité d’utiliser des mots de passe, nous protégeons la machine virtuelle Linux contre ce type d’attaque par force brute.</span><span class="sxs-lookup"><span data-stu-id="124ae-107">By completely removing the ability to use passwords we protect the Linux VM from this type of brute force attack.</span></span>  <span data-ttu-id="124ae-108">L’avantage supplémentaire est que nous configurons le SSHD Linux pour qu’il n’autorise que les connexions via des clés publiques et privées SSH, qui est de loin la méthode la plus sûre pour se connecter à Linux.</span><span class="sxs-lookup"><span data-stu-id="124ae-108">The added bonus is we will configure Linux SSHD to only allow logins via SSH public & private keys, by far the most secure way to login to Linux.</span></span>  <span data-ttu-id="124ae-109">Le nombre des différentes combinaisons possibles permettant de deviner la clé privée est immense et par conséquent décourage les robots de seulement essayer d’attaquer les clés SSH par force brute.</span><span class="sxs-lookup"><span data-stu-id="124ae-109">The possible combinations of it would require to guess the private key is immense and therefore discourages bots from even bothering to try to brute force SSH keys.</span></span>

## <a name="goals"></a><span data-ttu-id="124ae-110">Objectifs</span><span class="sxs-lookup"><span data-stu-id="124ae-110">Goals</span></span>
* <span data-ttu-id="124ae-111">Configurer SSHD pour interdire ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="124ae-111">Configure SSHD to disallow:</span></span>
  * <span data-ttu-id="124ae-112">Connexions par mot de passe</span><span class="sxs-lookup"><span data-stu-id="124ae-112">Password logins</span></span>
  * <span data-ttu-id="124ae-113">Connexion de l’utilisateur racine</span><span class="sxs-lookup"><span data-stu-id="124ae-113">Root user login</span></span>
  * <span data-ttu-id="124ae-114">Authentification par stimulation/réponse</span><span class="sxs-lookup"><span data-stu-id="124ae-114">Challenge-response authentication</span></span>
* <span data-ttu-id="124ae-115">Configurer SSHD pour autoriser ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="124ae-115">Configure SSHD to allow:</span></span>
  * <span data-ttu-id="124ae-116">Uniquement les connexions par clés SSH</span><span class="sxs-lookup"><span data-stu-id="124ae-116">only SSH key logins</span></span>
* <span data-ttu-id="124ae-117">Redémarrage de SSHD quand la session est encore ouverte</span><span class="sxs-lookup"><span data-stu-id="124ae-117">Restart SSHD while still logged in</span></span>
* <span data-ttu-id="124ae-118">Test de la nouvelle configuration SSHD</span><span class="sxs-lookup"><span data-stu-id="124ae-118">Test the new SSHD configuration</span></span>

## <a name="introduction"></a><span data-ttu-id="124ae-119">Introduction</span><span class="sxs-lookup"><span data-stu-id="124ae-119">Introduction</span></span>
[<span data-ttu-id="124ae-120">Définition de SSH</span><span class="sxs-lookup"><span data-stu-id="124ae-120">SSH defined</span></span>](https://en.wikipedia.org/wiki/Secure_Shell)

<span data-ttu-id="124ae-121">SSHD est le serveur SSH qui s’exécute sur la machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="124ae-121">SSHD is the SSH Server that runs on the Linux VM.</span></span>  <span data-ttu-id="124ae-122">SSH est un client qui s’exécute à partir d’un interpréteur de commandes sur votre poste de travail MacBook ou Linux.</span><span class="sxs-lookup"><span data-stu-id="124ae-122">SSH is a client that runs from a shell on your MacBook or Linux workstation.</span></span>  <span data-ttu-id="124ae-123">SSH est également le protocole utilisé pour sécuriser et chiffrer les communications entre votre poste de travail et la machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="124ae-123">SSH is also the protocol used to secure and encrypt the communication between your workstation and the Linux VM.</span></span>

<span data-ttu-id="124ae-124">Dans le cadre de cet article, il est très important que la connexion à votre machine virtuelle Linux soit ouverte durant toutes les étapes.</span><span class="sxs-lookup"><span data-stu-id="124ae-124">For this article it is very important to keep one login to your Linux VM open for the entire walk through.</span></span>  <span data-ttu-id="124ae-125">Pour cette raison, nous allons ouvrir deux terminaux et exécuter SSH vers la machine virtuelle Linux à partir de chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="124ae-125">For this reason we will open two terminals and SSH to the Linux VM from both of them.</span></span>  <span data-ttu-id="124ae-126">Nous utilisons le premier terminal pour modifier le fichier de configuration SSHD et redémarrer le service SSHD.</span><span class="sxs-lookup"><span data-stu-id="124ae-126">We will use the first terminal to make the changes to SSHDs configuration file and restart the SSHD service.</span></span>  <span data-ttu-id="124ae-127">Nous utilisons le deuxième terminal pour tester ces modifications une fois que le service est redémarré.</span><span class="sxs-lookup"><span data-stu-id="124ae-127">We will use the second terminal to test those changes once the service is restarted.</span></span>  <span data-ttu-id="124ae-128">Étant donné que nous désactivons les mots de passe SSH et que nous nous appuyons uniquement sur les clés SSH, si ces dernières sont incorrectes et que vous fermez la connexion à la machine virtuelle, celle-ci sera définitivement verrouillée et personne ne pourra se connecter à moins de la supprimer et de la recréer.</span><span class="sxs-lookup"><span data-stu-id="124ae-128">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close the connection to the VM, the VM will be permanently locked and no one will be able to login to it requiring it to be deleted and recreated.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="124ae-129">Composants requis</span><span class="sxs-lookup"><span data-stu-id="124ae-129">Prerequisites</span></span>
* [<span data-ttu-id="124ae-130">Créer des clés SSH sur Linux et Mac pour les machines virtuelles Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="124ae-130">Create SSH keys on Linux and Mac for Linux VMs in Azure</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* <span data-ttu-id="124ae-131">Compte Azure</span><span class="sxs-lookup"><span data-stu-id="124ae-131">Azure account</span></span>
  * [<span data-ttu-id="124ae-132">Version d’évaluation gratuite</span><span class="sxs-lookup"><span data-stu-id="124ae-132">free trial signup</span></span>](https://azure.microsoft.com/pricing/free-trial/)
  * [<span data-ttu-id="124ae-133">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="124ae-133">Azure portal</span></span>](http://portal.azure.com)
* <span data-ttu-id="124ae-134">Machine virtuelle Linux s’exécutant sur Azure</span><span class="sxs-lookup"><span data-stu-id="124ae-134">Linux VM running on azure</span></span>
* <span data-ttu-id="124ae-135">Paire de clés publique et privée SSH dans `~/.ssh/`</span><span class="sxs-lookup"><span data-stu-id="124ae-135">SSH public & private key pair in `~/.ssh/`</span></span>
* <span data-ttu-id="124ae-136">Clé publique SSH dans `~/.ssh/authorized_keys` sur la machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="124ae-136">SSH public key in `~/.ssh/authorized_keys` on the Linux VM</span></span>
* <span data-ttu-id="124ae-137">Droits sudo sur la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="124ae-137">Sudo rights on the VM</span></span>
* <span data-ttu-id="124ae-138">Port 22 ouvert</span><span class="sxs-lookup"><span data-stu-id="124ae-138">Port 22 open</span></span>

## <a name="quick-commands"></a><span data-ttu-id="124ae-139">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="124ae-139">Quick Commands</span></span>
<span data-ttu-id="124ae-140">*Les administrateurs Linux chevronnés souhaitant uniquement la version TLDR commencent ici.  Les utilisateurs qui souhaitent une explication détaillée et une procédure pas à pas peuvent ignorer cette section.*</span><span class="sxs-lookup"><span data-stu-id="124ae-140">*Seasoned Linux Admins who just want the TLDR version start here.  For everyone else that wants the detailed explanation and walk through skip this section.*</span></span>

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="124ae-141">Modifiez le fichier de configuration comme suit :</span><span class="sxs-lookup"><span data-stu-id="124ae-141">Edit the config file as follows:</span></span>

```sh
# Change PasswordAuthentication to this:
PasswordAuthentication no

# Change PubkeyAuthentication to this:
PubkeyAuthentication yes

# Change PermitRootLogin to this:
PermitRootLogin no

# Change ChallengeResponseAuthentication to this:
ChallengeResponseAuthentication no
```

<span data-ttu-id="124ae-142">Redémarrez le service SSHD.</span><span class="sxs-lookup"><span data-stu-id="124ae-142">Restart the SSHD service.</span></span> <span data-ttu-id="124ae-143">Sur les distributions basées sur Debian :</span><span class="sxs-lookup"><span data-stu-id="124ae-143">On Debian-based distros:</span></span>

```bash
sudo service ssh restart
```

<span data-ttu-id="124ae-144">Sur les distributions basées sur Red Hat :</span><span class="sxs-lookup"><span data-stu-id="124ae-144">On Red Hat-based distros:</span></span>

```bash
sudo service sshd restart
```

## <a name="detailed-walk-through"></a><span data-ttu-id="124ae-145">Procédure pas à pas détaillée</span><span class="sxs-lookup"><span data-stu-id="124ae-145">Detailed Walk Through</span></span>
<span data-ttu-id="124ae-146">Connexion à la machine virtuelle Linux sur le terminal 1 (T1).</span><span class="sxs-lookup"><span data-stu-id="124ae-146">Login to the Linux VM on terminal 1 (T1).</span></span>  <span data-ttu-id="124ae-147">Connexion à la machine virtuelle Linux sur le terminal 2 (T2).</span><span class="sxs-lookup"><span data-stu-id="124ae-147">Login to the Linux VM on terminal 2 (T2).</span></span>

<span data-ttu-id="124ae-148">Dans T2, nous modifions le fichier de configuration SSHD.</span><span class="sxs-lookup"><span data-stu-id="124ae-148">On T2 we are going to edit the SSHD configuration file.</span></span>  

```bash
sudo vim /etc/ssh/sshd_config
```

<span data-ttu-id="124ae-149">Ensuite, nous modifions seulement les paramètres pour désactiver les mots de passe et activer les connexions par clé SSH.</span><span class="sxs-lookup"><span data-stu-id="124ae-149">From here we will edit just the settings to disable passwords and enable SSH key logins.</span></span>  <span data-ttu-id="124ae-150">Vous pouvez rechercher et modifier de nombreux paramètres dans ce fichier pour sécuriser Linux et SSH selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="124ae-150">There are many settings in this file that you should research and change to make Linux & SSH as secure as you need.</span></span>

#### <a name="disable-password-logins"></a><span data-ttu-id="124ae-151">Désactiver les connexions par mot de passe</span><span class="sxs-lookup"><span data-stu-id="124ae-151">Disable Password logins</span></span>

```sh
# Change PasswordAuthentication to this:
PasswordAuthentication no
```

#### <a name="enable-public-key-authentication"></a><span data-ttu-id="124ae-152">Activer l’authentification par clé publique</span><span class="sxs-lookup"><span data-stu-id="124ae-152">Enable Public Key Authentication</span></span>

```sh
# Change PubkeyAuthentication to this:
PubkeyAuthentication yes
```

#### <a name="disable-root-login"></a><span data-ttu-id="124ae-153">Désactiver la connexion racine</span><span class="sxs-lookup"><span data-stu-id="124ae-153">Disable Root Login</span></span>

```sh
# Change PermitRootLogin to this:
PermitRootLogin no
```

#### <a name="disable-challenge-response-authentication"></a><span data-ttu-id="124ae-154">Désactiver l’authentification par stimulation/réponse</span><span class="sxs-lookup"><span data-stu-id="124ae-154">Disable Challenge-response Authentication</span></span>
```sh
# Change ChallengeResponseAuthentication to this:
ChallengeResponseAuthentication no
```

### <a name="restart-sshd"></a><span data-ttu-id="124ae-155">Redémarrer SSHD</span><span class="sxs-lookup"><span data-stu-id="124ae-155">Restart SSHD</span></span>
<span data-ttu-id="124ae-156">Dans l’interpréteur de commandes de T1, vérifiez que vous êtes toujours connecté.</span><span class="sxs-lookup"><span data-stu-id="124ae-156">From the T1 shell verify that you are still logged in.</span></span>  <span data-ttu-id="124ae-157">Cela est essentiel pour continuer à avoir accès à votre machine virtuelle si vos clés SSH ne sont pas correctes, car les mots de passe sont désormais désactivés.</span><span class="sxs-lookup"><span data-stu-id="124ae-157">This is critical so you do not get locked out of your VM if your SSH keys are not correct since passwords are now disabled.</span></span>  <span data-ttu-id="124ae-158">Si des paramètres sont incorrects sur votre machine virtuelle Linux, vous pouvez corriger sshd_config à partir de T1, car vous êtes toujours connecté et que SSH maintient la connexion active pendant le redémarrage du service SSHD.</span><span class="sxs-lookup"><span data-stu-id="124ae-158">If any setting are incorrect on your Linux VM you can use T1 to fix sshd_config as you will still be logged in and SSH will keep the connection alive during the SSHD service restart.</span></span>

<span data-ttu-id="124ae-159">À partir de T2, effectuez l’exécution :</span><span class="sxs-lookup"><span data-stu-id="124ae-159">From T2 run:</span></span>

##### <a name="on-the-debian-family"></a><span data-ttu-id="124ae-160">Pour la famille Debian</span><span class="sxs-lookup"><span data-stu-id="124ae-160">On the Debian Family</span></span>
```bash
sudo service ssh restart
```

##### <a name="on-the-redhat-family"></a><span data-ttu-id="124ae-161">Pour la famille RedHat</span><span class="sxs-lookup"><span data-stu-id="124ae-161">On the RedHat Family</span></span>
```bash
sudo service sshd restart
```

<span data-ttu-id="124ae-162">Les mots de passe sont désormais désactivés sur votre machine virtuelle, ce qui la protège contre les tentatives d’attaque par force brute des connexions par mot de passe.</span><span class="sxs-lookup"><span data-stu-id="124ae-162">Passwords are now disabled on your VM protecting it from brute force password login attempts.</span></span>  <span data-ttu-id="124ae-163">Quand seules les clés SSH sont autorisées, vous pouvez vous connecter de façon plus rapide et beaucoup plus sûre.</span><span class="sxs-lookup"><span data-stu-id="124ae-163">With only SSH Keys allowed you will be able to login faster and much more secure.</span></span>

