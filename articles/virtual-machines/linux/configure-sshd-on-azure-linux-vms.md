---
title: aaaConfigure SSHD sur des Machines virtuelles Azure Linux | Documents Microsoft
description: "Configurer SSHD pour toolockdown SSH tooAzure les ordinateurs virtuels Linux et les meilleures pratiques de sécurité."
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
ms.openlocfilehash: c2361be7199a24b129c06acfc899dd32f6e1d6fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-sshd-on-azure-linux-vms"></a><span data-ttu-id="a7944-103">Configurer SSHD sur des machines virtuelles Linux Azure</span><span class="sxs-lookup"><span data-stu-id="a7944-103">Configure SSHD on Azure Linux VMs</span></span>

<span data-ttu-id="a7944-104">Cet article explique comment toolockdown hello serveur SSH sur Linux, tooprovide méthodes recommandées la sécurité et toospeed des processus de connexion SSH hello également à l’aide de clés SSH à la place des mots de passe.</span><span class="sxs-lookup"><span data-stu-id="a7944-104">This article shows how toolockdown hello SSH Server on Linux, tooprovide best practices security and also toospeed up hello SSH login process by using SSH keys instead of passwords.</span></span>  <span data-ttu-id="a7944-105">toofurther lockdown SSHD, nous allons utilisateur racine de hello toodisable d’être en mesure de toologin, limiter les utilisateurs hello autorisés toologin via une liste des groupes approuvés, la désactivation de la version 1 du protocole SSH, un bit de clé minimale et configurer avant déconnexion automatique des utilisateurs inactifs.</span><span class="sxs-lookup"><span data-stu-id="a7944-105">toofurther lockdown SSHD we are going toodisable hello root user from being able toologin, limit hello users that are allowed toologin via an approved group list, disabling SSH protocol version 1, set a minimum key bit, and configure auto-logout of idle users.</span></span>  <span data-ttu-id="a7944-106">configuration requise de Hello pour cet article est : un compte Azure ([obtenir une évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/)) et [fichiers clés SSH publique et privée](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a7944-106">hello requirements for this article are: an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)) and [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="quick-commands"></a><span data-ttu-id="a7944-107">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="a7944-107">Quick Commands</span></span>

<span data-ttu-id="a7944-108">Configurer `/etc/ssh/sshd_config` avec hello suivant les paramètres :</span><span class="sxs-lookup"><span data-stu-id="a7944-108">Configure `/etc/ssh/sshd_config` with hello following settings:</span></span>

### <a name="disable-password-logins"></a><span data-ttu-id="a7944-109">Désactiver les connexions par mot de passe</span><span class="sxs-lookup"><span data-stu-id="a7944-109">Disable password logins</span></span>

```bash
PasswordAuthentication no
```

### <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="a7944-110">Désactiver la connexion à l’utilisateur racine de hello</span><span class="sxs-lookup"><span data-stu-id="a7944-110">Disable login by hello root user</span></span>

```bash
PermitRootLogin no
```

### <a name="allowed-groups-list"></a><span data-ttu-id="a7944-111">Liste de groupes autorisés</span><span class="sxs-lookup"><span data-stu-id="a7944-111">Allowed groups list</span></span>

```bash
AllowGroups wheel
```

### <a name="allowed-users-list"></a><span data-ttu-id="a7944-112">Liste d’utilisateurs autorisés</span><span class="sxs-lookup"><span data-stu-id="a7944-112">Allowed users list</span></span>

```bash
AllowUsers ahmet ralph
```

### <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="a7944-113">Désactiver la version 1 du protocole SSH</span><span class="sxs-lookup"><span data-stu-id="a7944-113">Disable SSH protocol version 1</span></span>

```bash
Protocol 2
```

### <a name="minimum-key-bits"></a><span data-ttu-id="a7944-114">Minimum de bits pour les clés</span><span class="sxs-lookup"><span data-stu-id="a7944-114">Minimum key bits</span></span>

```bash
ServerKeyBits 2048
```

### <a name="disconnect-idle-users"></a><span data-ttu-id="a7944-115">Déconnecter les utilisateurs inactifs</span><span class="sxs-lookup"><span data-stu-id="a7944-115">Disconnect idle users</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="a7944-116">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="a7944-116">Detailed Walkthrough</span></span>

<span data-ttu-id="a7944-117">SSHD est hello serveur SSH qui s’exécute sur hello Linux VM.</span><span class="sxs-lookup"><span data-stu-id="a7944-117">SSHD is hello SSH Server that runs on hello Linux VM.</span></span>  <span data-ttu-id="a7944-118">SSH est un client qui s’exécute à partir d’un interpréteur de commandes sur votre MacBook ou votre poste de travail Linux, ou à partir d’un script Bash sur Windows.</span><span class="sxs-lookup"><span data-stu-id="a7944-118">SSH is a client that runs from a shell on your MacBook, Linux workstation, or from a Bash on Windows.</span></span>  <span data-ttu-id="a7944-119">SSH est également hello protocole utilisé toosecure et chiffrer la communication hello entre votre station de travail et les hello VM Linux qui SSH effectue également un réseau VPN (Virtual Private Network).</span><span class="sxs-lookup"><span data-stu-id="a7944-119">SSH is also hello protocol used toosecure and encrypt hello communication between your workstation and hello Linux VM making SSH also a VPN (Virtual Private Network).</span></span>

<span data-ttu-id="a7944-120">Pour cet article, il est tooyour d’une seule connexion tookeep très important Linux VM ouvrir pour la procédure pas à pas ensemble hello.</span><span class="sxs-lookup"><span data-stu-id="a7944-120">For this article, it is very important tookeep one login tooyour Linux VM open for hello entire walk-through.</span></span>  <span data-ttu-id="a7944-121">Une fois qu’une connexion SSH est établie, il reste comme une session ouverte tant que fenêtre hello n’est pas fermée.</span><span class="sxs-lookup"><span data-stu-id="a7944-121">Once an SSH connection is established, it remains as an open session as long as hello window is not closed.</span></span>  <span data-ttu-id="a7944-122">Ayant un terminal connecté, permet de modifications toobe apportée toohello SSHD service sans être verrouillé si une modification avec rupture est effectuée.</span><span class="sxs-lookup"><span data-stu-id="a7944-122">Having one terminal logged in, allows for changes toobe made toohello SSHD service without being locked out if a breaking change is made.</span></span>  <span data-ttu-id="a7944-123">Si vous effectuez l’être verrouillés hors de votre VM Linux avec une configuration SSHD rompue, Azure offre une configuration SSHD interrompue avec hello hello capacité tooreset [Extension d’accès Azure VM](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a7944-123">If you do get locked out of your Linux VM with a broken SSHD configuration, Azure offers hello ability tooreset a broken SSHD configuration with hello [Azure VM Access Extension](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="a7944-124">Pour cette raison, nous allons ouvrir deux terminaux et SSH toohello Linux VM à partir des deux d'entre eux.</span><span class="sxs-lookup"><span data-stu-id="a7944-124">For this reason we open two terminals and SSH toohello Linux VM from both of them.</span></span>  <span data-ttu-id="a7944-125">Nous utiliser hello premier toomake terminal hello modifications tooSSHDs fichier de configuration et redémarrez le service SSHD hello.</span><span class="sxs-lookup"><span data-stu-id="a7944-125">We use hello first terminal toomake hello changes tooSSHDs configuration file and restart hello SSHD service.</span></span>  <span data-ttu-id="a7944-126">Nous utilisons tootest terminal deuxième hello celles modifie une fois le redémarrage du service hello.</span><span class="sxs-lookup"><span data-stu-id="a7944-126">We use hello second terminal tootest those changes once hello service is restarted.</span></span>  <span data-ttu-id="a7944-127">Étant donné que nous allons la désactivation des mots de passe SSH et partie de confiance strictement sur les clés SSH, si vos clés SSH ne sont pas corrects et que vous fermez hello connexion toohello machine virtuelle, hello machine virtuelle seront définitivement verrouillé et aucun sera tooit toologin en mesure de rendre obligatoire toobe supprimé et recréé.</span><span class="sxs-lookup"><span data-stu-id="a7944-127">Because we are disabling SSH passwords and relying strictly on SSH keys, if your SSH keys are not correct and you close hello connection toohello VM, hello VM will be permanently locked and no one will be able toologin tooit requiring it toobe deleted and recreated.</span></span>

## <a name="disable-password-logins"></a><span data-ttu-id="a7944-128">Désactiver les connexions par mot de passe</span><span class="sxs-lookup"><span data-stu-id="a7944-128">Disable password logins</span></span>

<span data-ttu-id="a7944-129">Hello toosecure de manière plus rapide vous Linux VM est toodisable les connexions de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="a7944-129">hello quickest way toosecure you Linux VM is toodisable password logins.</span></span>  <span data-ttu-id="a7944-130">Lorsque les connexions de mot de passe sont activées, robots web de hello l’analyse démarre immédiatement la tentative de toobrute force mot de passe estimation hello pour votre VM Linux à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="a7944-130">When password logins are enabled, bots crawling hello web will immediately start attempting toobrute force guess hello password for your Linux VM using SSH.</span></span>  <span data-ttu-id="a7944-131">Désactive les connexions de mot de passe complètement, permet de hello SSH server tooignore toutes les tentatives de connexion de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="a7944-131">Disabling password logins completely, enables hello SSH server tooignore all password login attempts.</span></span>

```bash
PasswordAuthentication no
```

## <a name="disable-login-by-hello-root-user"></a><span data-ttu-id="a7944-132">Désactiver la connexion à l’utilisateur racine de hello</span><span class="sxs-lookup"><span data-stu-id="a7944-132">Disable login by hello root user</span></span>

<span data-ttu-id="a7944-133">Suivant les recommandations Linux, hello `root` utilisateur ne doit jamais être connecté à via SSH ou à l’aide de `sudo su`.</span><span class="sxs-lookup"><span data-stu-id="a7944-133">Following Linux best practices, hello `root` user should never be logged into over SSH or using `sudo su`.</span></span>  <span data-ttu-id="a7944-134">Toutes les commandes nécessitant des autorisations au niveau racine doivent toujours être exécutées par le biais hello `sudo` commande, qui enregistre toutes les actions d’audit ultérieur.</span><span class="sxs-lookup"><span data-stu-id="a7944-134">All commands needing root level permissions should always be run through hello `sudo` command, which logs all actions for future auditing.</span></span>  <span data-ttu-id="a7944-135">Désactivation hello `root` utilisateur de se connecter via une connexion SSH est une étape sécurité meilleures pratiques de qui permet de s’assurer seulement les utilisateurs autorisés peuvent tooSSH.</span><span class="sxs-lookup"><span data-stu-id="a7944-135">Disabling hello `root` user from logging in via SSH is a security best practices step that ensures only authorized users are allowed tooSSH.</span></span>

```bash
PermitRootLogin no
```

## <a name="allowed-groups-list"></a><span data-ttu-id="a7944-136">Liste de groupes autorisés</span><span class="sxs-lookup"><span data-stu-id="a7944-136">Allowed groups list</span></span>

<span data-ttu-id="a7944-137">Le protocole SSH offre une méthode de restriction des utilisateurs et des groupes autorisés à se connecter via SSH.</span><span class="sxs-lookup"><span data-stu-id="a7944-137">SSH offers a method of restricting users and group that are allowed or disallowed from logging in over SSH.</span></span>  <span data-ttu-id="a7944-138">Cette fonctionnalité utilise des listes tooapprove ou refuser des utilisateurs et groupes spécifiques de se connecter.</span><span class="sxs-lookup"><span data-stu-id="a7944-138">This feature uses lists tooapprove or deny specific users and groups from logging in.</span></span>  <span data-ttu-id="a7944-139">Paramètre hello roue groupe toohello `AllowGroups` liste limite les connexions approuvées sur les comptes d’utilisateur SSH toojust qui se trouvent dans le groupe de roulette hello.</span><span class="sxs-lookup"><span data-stu-id="a7944-139">Setting hello wheel group toohello `AllowGroups` list restricts approved logins over SSH toojust user accounts that are in hello wheel group.</span></span>

```bash
AllowGroups wheel
```

## <a name="allowed-users-list"></a><span data-ttu-id="a7944-140">Liste d’utilisateurs autorisés</span><span class="sxs-lookup"><span data-stu-id="a7944-140">Allowed users list</span></span>

<span data-ttu-id="a7944-141">Limiter les utilisateurs toojust de connexions SSH est une façon plus spécifique tooaccomplish hello même tâche que `AllowGroups` est.</span><span class="sxs-lookup"><span data-stu-id="a7944-141">Restricting SSH logins toojust users is a more specific way tooaccomplish hello same task that `AllowGroups` is.</span></span>  

```bash
AllowUsers ahmet ralph
```

## <a name="disable-ssh-protocol-version-1"></a><span data-ttu-id="a7944-142">Désactiver la version 1 du protocole SSH</span><span class="sxs-lookup"><span data-stu-id="a7944-142">Disable SSH protocol version 1</span></span>

<span data-ttu-id="a7944-143">La version 1 du protocole SSH n’est pas sécurisée et doit être désactivée.</span><span class="sxs-lookup"><span data-stu-id="a7944-143">SSH protocol version 1 is insecure and should be disabled.</span></span>  <span data-ttu-id="a7944-144">Version 2 du protocole SSH est la version actuelle hello qui offre un serveur de tooyour de tooSSH de manière sécurisée.</span><span class="sxs-lookup"><span data-stu-id="a7944-144">SSH protocol version 2 is hello current version that offers a secure way tooSSH tooyour server.</span></span>  <span data-ttu-id="a7944-145">La désactivation de la version 1 de SSH refuse à tous les clients SSH qui tentent de tooestablish une connexion avec le serveur SSH hello à l’aide de la version 1 de SSH.</span><span class="sxs-lookup"><span data-stu-id="a7944-145">Disabling SSH version 1 denies any SSH clients that are attempting tooestablish a connection with hello SSH server using SSH version 1.</span></span>  <span data-ttu-id="a7944-146">Seules les connexions SSH version 2 sont autorisées toonegotiate une connexion avec le serveur SSH hello.</span><span class="sxs-lookup"><span data-stu-id="a7944-146">Only SSH version 2 connections are allowed toonegotiate a connection with hello SSH server.</span></span>

```bash
Protocol 2
```

## <a name="minimum-key-bits"></a><span data-ttu-id="a7944-147">Minimum de bits pour les clés</span><span class="sxs-lookup"><span data-stu-id="a7944-147">Minimum key bits</span></span>

<span data-ttu-id="a7944-148">Meilleures pratiques de sécurité, connexions SSH de mot de passe sont désactivées, et seules les clés SSH sont autorisées toobe utilisé tooauthenticate avec serveur SSH de hello.</span><span class="sxs-lookup"><span data-stu-id="a7944-148">Following security best practices, password SSH logins are disabled and only SSH keys are allowed toobe used tooauthenticate with hello SSH server.</span></span>  <span data-ttu-id="a7944-149">Ces clés SSH peuvent être créées à l’aide de clés de longueur différente, mesurées en bits.</span><span class="sxs-lookup"><span data-stu-id="a7944-149">These SSH keys can be created using different length keys, measured in bits.</span></span>  <span data-ttu-id="a7944-150">Meilleures pratiques que les clés de longueur de 2 048 bits sont hello minimale acceptable puissance de la clé des États.</span><span class="sxs-lookup"><span data-stu-id="a7944-150">Best practices states that keys of 2048 bits in length are hello minimum acceptable key strength.</span></span>  <span data-ttu-id="a7944-151">Les clés de moins de 2 048 bits risquent en effet d’être déchiffrées.</span><span class="sxs-lookup"><span data-stu-id="a7944-151">Keys of less than 2048 bits could theoretically be broken.</span></span>  <span data-ttu-id="a7944-152">Hello du paramètre `ServerKeyBits` trop`2048` autorise toutes les connexions à l’aide de clés de 2 048 bits ou supérieur et refuser les connexions de moins de 2 048 bits.</span><span class="sxs-lookup"><span data-stu-id="a7944-152">Setting hello `ServerKeyBits` too`2048` allows any connections using keys of 2048 bits or greater and deny connections of less than 2048 bits.</span></span>

```bash
ServerKeyBits 2048
```

## <a name="disconnect-idle-users"></a><span data-ttu-id="a7944-153">Déconnecter les utilisateurs inactifs</span><span class="sxs-lookup"><span data-stu-id="a7944-153">Disconnect idle users</span></span>

<span data-ttu-id="a7944-154">SSH a hello capacité toodisconnect utilisateurs qui ont des connexions ouvertes qui sont restées inactives au-delà d’une durée de secondes.</span><span class="sxs-lookup"><span data-stu-id="a7944-154">SSH has hello ability toodisconnect users that have open connections that have remained idle for more than a set period of seconds.</span></span>  <span data-ttu-id="a7944-155">Conservation des sessions ouvertes tooonly aux utilisateurs exposition de hello limites active de hello Linux VM.</span><span class="sxs-lookup"><span data-stu-id="a7944-155">Keeping open sessions tooonly those users who are active limits hello exposure of hello Linux VM.</span></span>

```bash
ClientAliveInterval 300
ClientAliveCountMax 0
```

## <a name="restart-sshd"></a><span data-ttu-id="a7944-156">Redémarrer SSHD</span><span class="sxs-lookup"><span data-stu-id="a7944-156">Restart SSHD</span></span>

<span data-ttu-id="a7944-157">paramètres de hello tooenable dans `/etc/ssh/sshd_config` redémarrer les processus SSHD hello qui redémarre le serveur SSH de hello.</span><span class="sxs-lookup"><span data-stu-id="a7944-157">tooenable hello settings in `/etc/ssh/sshd_config` restart hello SSHD process which restarts hello SSH server.</span></span>  <span data-ttu-id="a7944-158">fenêtre de terminal Hello vous utilisez toorestart hello SSH server restent ouverts sans perdre d’ouverture de session SSH hello.</span><span class="sxs-lookup"><span data-stu-id="a7944-158">hello terminal window you use toorestart hello SSH server remain open without losing hello open SSH session.</span></span>  <span data-ttu-id="a7944-159">paramètres du serveur SSH nouvelle tootest hello utilisent une deuxième fenêtre de terminal ou un onglet.  À l’aide d’un Bonjour tootest terminal distincte connexion SSH vous permet de toogo précédent et rendre des modifications supplémentaires toohello `/etc/ssh/sshd_config` dans hello premier terminal, sans être verrouillé par une modification avec rupture SSHD.</span><span class="sxs-lookup"><span data-stu-id="a7944-159">tootest hello new SSH server settings use a second terminal window or tab.  Using a separate terminal tootest hello SSH connection allows you toogo back and make additional changes toohello `/etc/ssh/sshd_config` in hello first terminal, without being locked out by a breaking SSHD change.</span></span>  

### <a name="on-redhat-centos-and-fedora"></a><span data-ttu-id="a7944-160">Sur Redhat, Centos et Fedora</span><span class="sxs-lookup"><span data-stu-id="a7944-160">On Redhat, Centos and Fedora</span></span>

```bash
service sshd restart
```

### <a name="on-debian--ubuntu"></a><span data-ttu-id="a7944-161">Sur Debian et Ubuntu</span><span class="sxs-lookup"><span data-stu-id="a7944-161">On Debian & Ubuntu</span></span>

```bash
service ssh restart
```

## <a name="reset-sshd-using-azure-reset-access"></a><span data-ttu-id="a7944-162">Réinitialiser SSHD à l’aide de la commande reset-access Azure</span><span class="sxs-lookup"><span data-stu-id="a7944-162">Reset SSHD using Azure reset-access</span></span>

<span data-ttu-id="a7944-163">Si vous êtes bloqué d’une configuration de SSHD de toohello de modification avec rupture, vous pouvez utiliser hello extension d’accès Azure VM tooreset hello SSHD configuration arrière toohello configuration d’origine.</span><span class="sxs-lookup"><span data-stu-id="a7944-163">If you are locked out from a breaking change toohello SSHD configuration you can use hello Azure VM access-extension tooreset hello SSHD configuration back toohello original configuration.</span></span>

<span data-ttu-id="a7944-164">Remplacez les exemples de noms par vos propres noms.</span><span class="sxs-lookup"><span data-stu-id="a7944-164">Replace any example names with your own.</span></span>

```azurecli
azure vm reset-access \
--resource-group myResourceGroup \
--name myVM \
--reset-ssh
```

## <a name="install-fail2ban"></a><span data-ttu-id="a7944-165">Installer Fail2ban</span><span class="sxs-lookup"><span data-stu-id="a7944-165">Install Fail2ban</span></span>

<span data-ttu-id="a7944-166">Il est fortement recommandé tooinstall et le programme d’installation open source application hello Fail2ban, les blocs répété tentatives toologin tooyour Linux VM via SSH à l’aide de force brute.</span><span class="sxs-lookup"><span data-stu-id="a7944-166">It is strongly recommended tooinstall and setup hello open source app Fail2ban, which blocks repeated attempts toologin tooyour Linux VM over SSH using brute force.</span></span>  <span data-ttu-id="a7944-167">Les journaux de Fail2ban répétées basculé tentatives toologin SSH et crée ensuite des règles de pare-feu tooblock hello l’adresse IP provenant de tentatives de hello.</span><span class="sxs-lookup"><span data-stu-id="a7944-167">Fail2ban logs repeated failed attempts toologin over SSH and then creates firewall rules tooblock hello IP address that hello attempts are originating from.</span></span>

* [<span data-ttu-id="a7944-168">Page d’accueil de Fail2ban</span><span class="sxs-lookup"><span data-stu-id="a7944-168">Fail2ban homepage</span></span>](http://www.fail2ban.org/wiki/index.php/Main_Page)

## <a name="next-steps"></a><span data-ttu-id="a7944-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a7944-169">Next Steps</span></span>

<span data-ttu-id="a7944-170">Maintenant que vous avez configuré et verrouillé de serveur SSH de hello sur votre VM Linux il existe des meilleures pratiques de la sécurité supplémentaire que vous pouvez suivre.</span><span class="sxs-lookup"><span data-stu-id="a7944-170">Now that you have configured and locked down hello SSH server on your Linux VM there are additional security best practices you can follow.</span></span>  

* [<span data-ttu-id="a7944-171">Gérer les utilisateurs, SSH et vérification ou de réparation des disques sur les machines virtuelles Azure Linux à l’aide de bienvenue de le VMAccess Extension</span><span class="sxs-lookup"><span data-stu-id="a7944-171">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="a7944-172">Chiffrer les disques sur un VM Linux à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="a7944-172">Encrypt disks on a Linux VM using hello Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

* [<span data-ttu-id="a7944-173">Accès et sécurité dans les modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a7944-173">Access and security in Azure Resource Manager templates</span></span>](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
