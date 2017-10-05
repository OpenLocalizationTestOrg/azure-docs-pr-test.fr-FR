---
title: "Configurer SSHD sur des machines virtuelles Linux Azure | Microsoft Docs"
description: "Configurez SSHD pour les meilleures pratiques de sécurité et pour verrouiller SSH sur des machines virtuelles Linux Azure."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/21/2016
ms.author: v-livech
ms.openlocfilehash: 0195c385b00ab92b2b92ce8ff00983a0d91bf3a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a><span data-ttu-id="43bd3-103">Configurer SSHD sur des machines virtuelles Linux Azure</span><span class="sxs-lookup"><span data-stu-id="43bd3-103">Configure SSHD on Azure Linux VMs</span></span>

<span data-ttu-id="43bd3-104">Cet article explique comment verrouiller le serveur SSH sur Linux, mettre en œuvre les meilleures pratiques de sécurité et accélérer le processus de connexion SSH en utilisant des clés SSH plutôt que des mots de passe.</span><span class="sxs-lookup"><span data-stu-id="43bd3-104">This article shows how to lockdown the SSH Server on Linux, to provide best practices security and also to speed up the SSH login process by using SSH keys instead of passwords.</span></span>  <span data-ttu-id="43bd3-105">Pour renforcer le verrouillage de SSHD, nous allons désactiver la connexion de l’utilisateur racine, limiter les utilisateurs autorisés à se connecter via une liste de groupes approuvés, désactiver la version 1 du protocole SSH, définir un minimum de bits pour les clés et configurer la déconnexion automatique des utilisateurs inactifs.</span><span class="sxs-lookup"><span data-stu-id="43bd3-105">To further lockdown SSHD we are going to disable the root user from being able to login, limit the users that are allowed to login via an approved group list, disabling SSH protocol version 1, set a minimum key bit, and configure auto-logout of idle users.</span></span>  <span data-ttu-id="43bd3-106">Les éléments requis pour cet article sont les suivants : un compte Azure ([obtenir un essai gratuit](https://azure.microsoft.com/pricing/free-trial/)) et [des fichiers de clés SSH publiques et privées](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="43bd3-106">The requirements for this article are: an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="43bd3-107">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="43bd3-107">Quick Commands</span></span>

<span data-ttu-id="43bd3-108">Configurez `/etc/ssh/sshd_config` en utilisant les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="43bd3-108">Configure `/etc/ssh/sshd_config` with the following settings:</span></span>

### <a name="disable-password-logins"></a><span data-ttu-id="43bd3-109">Désactiver les connexions par mot de passe</span><span class="sxs-lookup"><span data-stu-id="43bd3-109">Disable password logins</span></span>

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-the-root-user"></a><span data-ttu-id="43bd3-110">Désactiver la connexion de l’utilisateur racine</span><span class="sxs-lookup"><span data-stu-id="43bd3-110">Disable login by the root user</span></span>

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a><span data-ttu-id="43bd3-111">Liste de groupes autorisés</span><span class="sxs-lookup"><span data-stu-id="43bd3-111">Allowed groups list</span></span>

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a><span data-ttu-id="43bd3-112">Liste d’utilisateurs autorisés</span><span class="sxs-lookup"><span data-stu-id="43bd3-112">Allowed users list</span></span>

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="43bd3-113">Désactiver la version 1 du protocole SSH</span><span class="sxs-lookup"><span data-stu-id="43bd3-113">Disable SSH protocol version 1</span></span>

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a><span data-ttu-id="43bd3-114">Minimum de bits pour les clés</span><span class="sxs-lookup"><span data-stu-id="43bd3-114">Minimum key bits</span></span>

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a><span data-ttu-id="43bd3-115">Déconnecter les utilisateurs inactifs</span><span class="sxs-lookup"><span data-stu-id="43bd3-115">Disconnect idle users</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="43bd3-116">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="43bd3-116">Detailed Walkthrough</span></span>

<span data-ttu-id="43bd3-117">SSHD est le serveur SSH qui s’exécute sur la machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="43bd3-117">SSHD is the SSH Server that runs on the Linux VM.</span></span>  <span data-ttu-id="43bd3-118">SSH est un client qui s’exécute à partir d’un interpréteur de commandes sur votre MacBook ou votre poste de travail Linux, ou à partir d’un script Bash sur Windows.</span><span class="sxs-lookup"><span data-stu-id="43bd3-118">SSH is a client that runs from a shell on your MacBook, Linux workstation, or from a Bash on Windows.</span></span>  <span data-ttu-id="43bd3-119">SSH est également le protocole utilisé pour sécuriser et chiffrer les communications entre votre poste de travail et la machine virtuelle Linux, ce qui fait également de SSH un VPN (réseau privé virtuel).</span><span class="sxs-lookup"><span data-stu-id="43bd3-119">SSH is also the protocol used to secure and encrypt the communication between your workstation and the Linux VM making SSH also a VPN (Virtual Private Network).</span></span>

<span data-ttu-id="43bd3-120">Dans le cadre de cet article, il est très important que la connexion à votre machine virtuelle Linux soit ouverte durant toutes les étapes.</span><span class="sxs-lookup"><span data-stu-id="43bd3-120">For this article, it is very important to keep one login to your Linux VM open for the entire walk-through.</span></span>  <span data-ttu-id="43bd3-121">Une fois une connexion SSH établie, la session reste ouverte tant que la fenêtre n’est pas fermée.</span><span class="sxs-lookup"><span data-stu-id="43bd3-121">Once an SSH connection is established, it remains as an open session as long as the window is not closed.</span></span>  <span data-ttu-id="43bd3-122">Le fait d’avoir un terminal connecté permet d’apporter des modifications au service SSHD en empêchant que l’accès soit bloqué si une modification entraîne une rupture.</span><span class="sxs-lookup"><span data-stu-id="43bd3-122">Having one terminal logged in, allows for changes to be made to the SSHD service without being locked out if a breaking change is made.</span></span>  <span data-ttu-id="43bd3-123">Si vous voyez toutefois votre accès à votre machine virtuelle Linux bloqué à cause d’une configuration SSHD rompue, Azure offre la possibilité de réinitialiser une configuration SSHD rompue à l’aide de [l’extension d’accès aux machines virtuelles Azure](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="43bd3-123">If you do get locked out of your Linux VM with a broken SSHD configuration, Azure offers the ability to reset a broken SSHD configuration with the [Azure VM Access Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="43bd3-124">Pour cette raison, nous ouvrons deux terminaux et établissons une connexion SSH avec la machine virtuelle Linux à partir de chacun d’eux.</span><span class="sxs-lookup"><span data-stu-id="43bd3-124">For this reason we open two terminals and SSH to the Linux VM from both of them.</span></span>  <span data-ttu-id="43bd3-125">Nous utilisons le premier terminal pour modifier le fichier de configuration SSHD et redémarrer le service SSHD.</span><span class="sxs-lookup"><span data-stu-id="43bd3-125">We use the first terminal to make the changes to SSHDs configuration file and restart the SSHD service.</span></span>  <span data-ttu-id="43bd3-126">Nous utilisons le deuxième terminal pour tester ces modifications une fois le service redémarré.</span><span class="sxs-lookup"><span data-stu-id="43bd3-126">We use the second terminal to test those changes once the service is restarted.</span></span>  <span data-ttu-id="43bd3-127">Étant donné que nous désactivons les mots de passe SSH et que nous nous appuyons uniquement sur les clés SSH, si ces dernières sont incorrectes et que vous fermez la connexion à la machine virtuelle, celle-ci sera définitivement verrouillée et personne ne pourra se connecter à moins de la supprimer et de la recréer.</span><span class="sxs-lookup"><span data-stu-id="43bd3-127">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close the connection to the VM, the VM will be permanently locked and no one will be able to login to it requiring it to be deleted and recreated.</span></span>

## <a name="disable-password-logins"></a><span data-ttu-id="43bd3-128">Désactiver les connexions par mot de passe</span><span class="sxs-lookup"><span data-stu-id="43bd3-128">Disable password logins</span></span>

<span data-ttu-id="43bd3-129">Le moyen le plus rapide pour sécuriser votre machine virtuelle Linux consiste à désactiver les connexions par mot de passe.</span><span class="sxs-lookup"><span data-stu-id="43bd3-129">The quickest way to secure you Linux VM is to disable password logins.</span></span>  <span data-ttu-id="43bd3-130">Si les connexions par mot de passe sont activées, les robots qui sillonnent le web essaieront immédiatement d’utiliser une attaque par force brute pour deviner le mot de passe de votre machine virtuelle Linux à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="43bd3-130">When password logins are enabled, bots crawling the web will immediately start attempting to brute force guess the password for your Linux VM using SSH.</span></span>  <span data-ttu-id="43bd3-131">Lorsque les connexions par mot de passe sont désactivées complètement, le serveur SSH ignorer toutes les tentatives de connexion par mot de passe.</span><span class="sxs-lookup"><span data-stu-id="43bd3-131">Disabling password logins completely, enables the SSH server to ignore all password login attempts.</span></span>

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-the-root-user"></a><span data-ttu-id="43bd3-132">Désactiver la connexion de l’utilisateur racine</span><span class="sxs-lookup"><span data-stu-id="43bd3-132">Disable login by the root user</span></span>

<span data-ttu-id="43bd3-133">Conformément aux meilleures pratiques applicables à Linux, l’utilisateur `root` ne doit jamais être connecté via SSH ou à l’aide de `sudo su`.</span><span class="sxs-lookup"><span data-stu-id="43bd3-133">Following Linux best practices, the `root` user should never be logged into over SSH or using `sudo su`.</span></span>  <span data-ttu-id="43bd3-134">Toutes les commandes nécessitant des autorisations de niveau racine doivent toujours être exécutées par le biais de la commande `sudo`, qui enregistre toutes les actions à des fins d’audit ultérieur.</span><span class="sxs-lookup"><span data-stu-id="43bd3-134">All commands needing root level permissions should always be run through the `sudo` command, which logs all actions for future auditing.</span></span>  <span data-ttu-id="43bd3-135">La désactivation de la connexion de l’utilisateur `root` via SSH est une étape des meilleures pratiques de sécurité permettant de s’assurer que seuls les utilisateurs autorisés sont en mesure d’établir une connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="43bd3-135">Disabling the `root` user from logging in via SSH is a security best practices step that ensures only authorized users are allowed to SSH.</span></span>

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a><span data-ttu-id="43bd3-136">Liste de groupes autorisés</span><span class="sxs-lookup"><span data-stu-id="43bd3-136">Allowed groups list</span></span>

<span data-ttu-id="43bd3-137">Le protocole SSH offre une méthode de restriction des utilisateurs et des groupes autorisés à se connecter via SSH.</span><span class="sxs-lookup"><span data-stu-id="43bd3-137">SSH offers a method of restricting users and group that are allowed or disallowed from logging in over SSH.</span></span>  <span data-ttu-id="43bd3-138">Cette fonctionnalité s’appuie sur des listes pour autoriser ou interdire l’accès à des utilisateurs et des groupes spécifiques.</span><span class="sxs-lookup"><span data-stu-id="43bd3-138">This feature uses lists to approve or deny specific users and groups from logging in.</span></span>  <span data-ttu-id="43bd3-139">La définition du groupe wheel sur la liste `AllowGroups` permet de restreindre les connexions approuvées via SSH aux comptes d’utilisateurs appartenant au groupe wheel.</span><span class="sxs-lookup"><span data-stu-id="43bd3-139">Setting the wheel group to the `AllowGroups` list restricts approved logins over SSH to just user accounts that are in the wheel group.</span></span>

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a><span data-ttu-id="43bd3-140">Liste d’utilisateurs autorisés</span><span class="sxs-lookup"><span data-stu-id="43bd3-140">Allowed users list</span></span>

<span data-ttu-id="43bd3-141">La restriction des connexions SSH à certains utilisateurs offre un moyen plus spécifique d’accomplir la même tâche que `AllowGroups`.</span><span class="sxs-lookup"><span data-stu-id="43bd3-141">Restricting SSH logins to just users is a more specific way to accomplish the same task that `AllowGroups` is.</span></span>  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="43bd3-142">Désactiver la version 1 du protocole SSH</span><span class="sxs-lookup"><span data-stu-id="43bd3-142">Disable SSH protocol version 1</span></span>

<span data-ttu-id="43bd3-143">La version 1 du protocole SSH n’est pas sécurisée et doit être désactivée.</span><span class="sxs-lookup"><span data-stu-id="43bd3-143">SSH protocol version 1 is insecure and should be disabled.</span></span>  <span data-ttu-id="43bd3-144">La version 2 du protocole SSH est la version actuelle. Elle offre un moyen sécurisé d’établir une connexion SSH avec votre serveur.</span><span class="sxs-lookup"><span data-stu-id="43bd3-144">SSH protocol version 2 is the current version that offers a secure way to SSH to your server.</span></span>  <span data-ttu-id="43bd3-145">La désactivation de la version 1 de SSH permet de refuser tout accès aux clients SSH qui tentent d’établir une connexion avec le serveur SSH à l’aide de cette version du protocole.</span><span class="sxs-lookup"><span data-stu-id="43bd3-145">Disabling SSH version 1 denies any SSH clients that are attempting to establish a connection with the SSH server using SSH version 1.</span></span>  <span data-ttu-id="43bd3-146">Seules les connexions faisant appel à la version 2 de SSH sont autorisées à négocier une connexion avec le serveur SSH.</span><span class="sxs-lookup"><span data-stu-id="43bd3-146">Only SSH version 2 connections are allowed to negotiate a connection with the SSH server.</span></span>

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a><span data-ttu-id="43bd3-147">Minimum de bits pour les clés</span><span class="sxs-lookup"><span data-stu-id="43bd3-147">Minimum key bits</span></span>

<span data-ttu-id="43bd3-148">Conformément aux meilleures pratiques de sécurité, les connexions SSH par mot de passe sont désactivées et seules les clés SSH peuvent être utilisées pour l’authentification auprès du serveur SSH.</span><span class="sxs-lookup"><span data-stu-id="43bd3-148">Following security best practices, password SSH logins are disabled and only SSH keys are allowed to be used to authenticate with the SSH server.</span></span>  <span data-ttu-id="43bd3-149">Ces clés SSH peuvent être créées à l’aide de clés de longueur différente, mesurées en bits.</span><span class="sxs-lookup"><span data-stu-id="43bd3-149">These SSH keys can be created using different length keys, measured in bits.</span></span>  <span data-ttu-id="43bd3-150">Selon les meilleures pratiques, une longueur de 2 048 bits constitue le niveau de sécurité minimal acceptable pour les clés.</span><span class="sxs-lookup"><span data-stu-id="43bd3-150">Best practices states that keys of 2048 bits in length are the minimum acceptable key strength.</span></span>  <span data-ttu-id="43bd3-151">Les clés de moins de 2 048 bits risquent en effet d’être déchiffrées.</span><span class="sxs-lookup"><span data-stu-id="43bd3-151">Keys of less than 2048 bits could theoretically be broken.</span></span>  <span data-ttu-id="43bd3-152">La définition de `ServerKeyBits` sur `2048` permet d’autoriser les connexions faisant appel à des clés d’au moins 2 048 bits et d’interdire les connexions qui utilisent des clés moins longues.</span><span class="sxs-lookup"><span data-stu-id="43bd3-152">Setting the `ServerKeyBits` to `2048` allows any connections using keys of 2048 bits or greater and deny connections of less than 2048 bits.</span></span>

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a><span data-ttu-id="43bd3-153">Déconnecter les utilisateurs inactifs</span><span class="sxs-lookup"><span data-stu-id="43bd3-153">Disconnect idle users</span></span>

<span data-ttu-id="43bd3-154">Le protocole SSH offre la possibilité de déconnecter les utilisateurs ayant une session ouverte qui sont restés inactifs pendant plus d’un certain nombre de secondes.</span><span class="sxs-lookup"><span data-stu-id="43bd3-154">SSH has the ability to disconnect users that have open connections that have remained idle for more than a set period of seconds.</span></span>  <span data-ttu-id="43bd3-155">Le fait de conserver les sessions ouvertes uniquement pour les utilisateurs actifs permet de limiter l’exposition de la machine virtuelle Linux.</span><span class="sxs-lookup"><span data-stu-id="43bd3-155">Keeping open sessions to only those users who are active limits the exposure of the Linux VM.</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a><span data-ttu-id="43bd3-156">Redémarrer SSHD</span><span class="sxs-lookup"><span data-stu-id="43bd3-156">Restart SSHD</span></span>

<span data-ttu-id="43bd3-157">Pour activer les paramètres de `/etc/ssh/sshd_config`, vous devez redémarrer le processus SSHD, ce qui entraîne le redémarrage du serveur SSH.</span><span class="sxs-lookup"><span data-stu-id="43bd3-157">To enable the settings in `/etc/ssh/sshd_config` restart the SSHD process which restarts the SSH server.</span></span>  <span data-ttu-id="43bd3-158">La fenêtre de terminal utilisée pour redémarrer le serveur SSH reste ouverte, empêchant la perte de la session SSH ouverte.</span><span class="sxs-lookup"><span data-stu-id="43bd3-158">The terminal window you use to restart the SSH server remain open without losing the open SSH session.</span></span>  <span data-ttu-id="43bd3-159">Pour tester les nouveaux paramètres du serveur SSH, utilisez une deuxième fenêtre de terminal ou un deuxième onglet.</span><span class="sxs-lookup"><span data-stu-id="43bd3-159">To test the new SSH server settings use a second terminal window or tab.</span></span>  <span data-ttu-id="43bd3-160">L’utilisation d’un terminal distinct pour tester la connexion SSH vous permet de revenir en arrière et d’apporter des modifications supplémentaires à `/etc/ssh/sshd_config` dans le premier terminal sans voir votre accès bloqué si une modification de la configuration SSHD entraîne une rupture.</span><span class="sxs-lookup"><span data-stu-id="43bd3-160">Using a separate terminal to test the SSH connection allows you to go back and make additional changes to the `/etc/ssh/sshd_config` in the first terminal, without being locked out by a breaking SSHD change.</span></span>  

### <a name="on-redhat-centos-and-fedora"></a><span data-ttu-id="43bd3-161">Sur Redhat, Centos et Fedora</span><span class="sxs-lookup"><span data-stu-id="43bd3-161">On Redhat, Centos and Fedora</span></span>

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a><span data-ttu-id="43bd3-162">Sur Debian et Ubuntu</span><span class="sxs-lookup"><span data-stu-id="43bd3-162">On Debian & Ubuntu</span></span>

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a><span data-ttu-id="43bd3-163">Réinitialiser SSHD à l’aide de la commande reset-access Azure</span><span class="sxs-lookup"><span data-stu-id="43bd3-163">Reset SSHD using Azure reset-access</span></span>

<span data-ttu-id="43bd3-164">Si votre accès est bloqué à cause d’une modification ayant entraîné une rupture de la configuration SSHD, vous pouvez utiliser l’extension d’accès aux machines virtuelles Azure pour rétablir la configuration SSHD d’origine.</span><span class="sxs-lookup"><span data-stu-id="43bd3-164">If you are locked out from a breaking change to the SSHD configuration you can use the Azure VM access-extension to reset the SSHD configuration back to the original configuration.</span></span>

<span data-ttu-id="43bd3-165">Remplacez les exemples de noms par vos propres noms.</span><span class="sxs-lookup"><span data-stu-id="43bd3-165">Replace any example names with your own.</span></span>

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a><span data-ttu-id="43bd3-166">Installer Fail2ban</span><span class="sxs-lookup"><span data-stu-id="43bd3-166">Install Fail2ban</span></span>

<span data-ttu-id="43bd3-167">Il est vivement recommandé d’installer et de configurer l’application open source Fail2ban, qui bloque les tentatives répétées de connexion à votre machine virtuelle Linux via SSH à l’aide d’une attaque par force brute.</span><span class="sxs-lookup"><span data-stu-id="43bd3-167">It is strongly recommended to install and setup the open source app Fail2ban, which blocks repeated attempts to login to your Linux VM over SSH using brute force.</span></span>  <span data-ttu-id="43bd3-168">Fail2ban enregistre les tentatives répétées de connexion via SSH ayant échoué, puis crée des règles de pare-feu pour bloquer l’adresse IP dont proviennent ces tentatives.</span><span class="sxs-lookup"><span data-stu-id="43bd3-168">Fail2ban logs repeated failed attempts to login over SSH and then creates firewall rules to block the IP address that the attempts are originating from.</span></span>

* [<span data-ttu-id="43bd3-169">Page d’accueil de Fail2ban</span><span class="sxs-lookup"><span data-stu-id="43bd3-169">Fail2ban homepage</span></span>](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a><span data-ttu-id="43bd3-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="43bd3-170">Next Steps</span></span>

<span data-ttu-id="43bd3-171">Maintenant que vous avez configuré et verrouillé le serveur SSH sur votre machine virtuelle Linux, vous pouvez suivre d’autres meilleures pratiques de sécurité.</span><span class="sxs-lookup"><span data-stu-id="43bd3-171">Now that you have configured and locked down the SSH server on your Linux VM there are additional security best practices you can follow.</span></span>  

* [<span data-ttu-id="43bd3-172">Gérer les utilisateurs, SSH et vérifier ou réparer les disques de machines virtuelles Azure Linux à l'aide de l’extension VMAccess</span><span class="sxs-lookup"><span data-stu-id="43bd3-172">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="43bd3-173">Chiffrer des disques sur une machine virtuelle Linux à l’aide de l’interface de ligne de commande Azure (CLI)</span><span class="sxs-lookup"><span data-stu-id="43bd3-173">Encrypt disks on a Linux VM using the Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="43bd3-174">Accès et sécurité dans les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="43bd3-174">Access and security in Azure Resource Manager templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
