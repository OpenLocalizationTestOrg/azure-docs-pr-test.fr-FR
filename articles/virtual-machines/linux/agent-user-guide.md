---
title: "aaaAzure présentation de l’Agent de machine virtuelle Linux | Documents Microsoft"
description: "Découvrez comment tooinstall et configurer le Linux Agent (waagent) toomanage interaction de votre machine virtuelle avec le contrôleur de structure Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4e08c84d9205f4db7aae6fd1568ec1f15fba395c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-and-using-hello-azure-linux-agent"></a><span data-ttu-id="8326f-103">Présentation et utilisation hello Linux Agent Azure</span><span class="sxs-lookup"><span data-stu-id="8326f-103">Understanding and using hello Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="8326f-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="8326f-104">Introduction</span></span>
<span data-ttu-id="8326f-105">Hello Microsoft Azure Linux (waagent) géré par l’Agent Linux et FreeBSD approvisionnement et machine virtuelle interaction avec hello contrôleur de structure Azure.</span><span class="sxs-lookup"><span data-stu-id="8326f-105">hello Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with hello Azure Fabric Controller.</span></span> <span data-ttu-id="8326f-106">Il fournit hello suivant de fonctionnalités pour les déploiements de Linux et FreeBSD IaaS :</span><span class="sxs-lookup"><span data-stu-id="8326f-106">It provides hello following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="8326f-107">Consultez la rubrique hello Azure Linux agent [Lisez-moi](https://github.com/Azure/WALinuxAgent/blob/master/README.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="8326f-107">See hello Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="8326f-108">**Approvisionnement d’image**</span><span class="sxs-lookup"><span data-stu-id="8326f-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="8326f-109">Création d'un compte d'utilisateur</span><span class="sxs-lookup"><span data-stu-id="8326f-109">Creation of a user account</span></span>
  * <span data-ttu-id="8326f-110">Configuration des types d'authentification SSH</span><span class="sxs-lookup"><span data-stu-id="8326f-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="8326f-111">Déploiement des clés publiques et des paires de clés SSH</span><span class="sxs-lookup"><span data-stu-id="8326f-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="8326f-112">Nom du paramètre hello hôte</span><span class="sxs-lookup"><span data-stu-id="8326f-112">Setting hello host name</span></span>
  * <span data-ttu-id="8326f-113">Plateforme de publication hello hôte nom toohello DNS</span><span class="sxs-lookup"><span data-stu-id="8326f-113">Publishing hello host name toohello platform DNS</span></span>
  * <span data-ttu-id="8326f-114">Toohello plateforme de création de rapports SSH hôte clé empreinte digitale</span><span class="sxs-lookup"><span data-stu-id="8326f-114">Reporting SSH host key fingerprint toohello platform</span></span>
  * <span data-ttu-id="8326f-115">Gestion du disque de ressources</span><span class="sxs-lookup"><span data-stu-id="8326f-115">Resource Disk Management</span></span>
  * <span data-ttu-id="8326f-116">Mise en forme et le montage du disque de ressources hello</span><span class="sxs-lookup"><span data-stu-id="8326f-116">Formatting and mounting hello resource disk</span></span>
  * <span data-ttu-id="8326f-117">Configuration de l'espace d'échange</span><span class="sxs-lookup"><span data-stu-id="8326f-117">Configuring swap space</span></span>
* <span data-ttu-id="8326f-118">**Mise en réseau**</span><span class="sxs-lookup"><span data-stu-id="8326f-118">**Networking**</span></span>
  
  * <span data-ttu-id="8326f-119">Gère les itinéraires tooimprove la compatibilité avec les serveurs DHCP de plateforme</span><span class="sxs-lookup"><span data-stu-id="8326f-119">Manages routes tooimprove compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="8326f-120">Garantit la stabilité hello du nom de l’interface réseau hello</span><span class="sxs-lookup"><span data-stu-id="8326f-120">Ensures hello stability of hello network interface name</span></span>
* <span data-ttu-id="8326f-121">**Noyau**</span><span class="sxs-lookup"><span data-stu-id="8326f-121">**Kernel**</span></span>
  
  * <span data-ttu-id="8326f-122">Configure la topologie NUMA virtuelle (désactivée pour le noyau < à 2.6.37)</span><span class="sxs-lookup"><span data-stu-id="8326f-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="8326f-123">Consommation de l'entropie Hyper-V pour /dev/random</span><span class="sxs-lookup"><span data-stu-id="8326f-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="8326f-124">Configure les délais d’expiration SCSI pour appareil de racine hello (qui peut être à distance)</span><span class="sxs-lookup"><span data-stu-id="8326f-124">Configures SCSI timeouts for hello root device (which could be remote)</span></span>
* <span data-ttu-id="8326f-125">**Diagnostics**</span><span class="sxs-lookup"><span data-stu-id="8326f-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="8326f-126">Port de console redirection toohello série</span><span class="sxs-lookup"><span data-stu-id="8326f-126">Console redirection toohello serial port</span></span>
* <span data-ttu-id="8326f-127">**Déploiements SCVMM**</span><span class="sxs-lookup"><span data-stu-id="8326f-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="8326f-128">Détecte et amorce l’agent VMM de hello pour Linux lors de l’exécution dans un environnement de System Center Virtual Machine Manager 2012 R2</span><span class="sxs-lookup"><span data-stu-id="8326f-128">Detects and bootstraps hello VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="8326f-129">**Extension de machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="8326f-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="8326f-130">Injecter des composants créés par Microsoft et partenaires dans automation de logiciels et la configuration de tooenable Linux VM (IaaS)</span><span class="sxs-lookup"><span data-stu-id="8326f-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) tooenable software and configuration automation</span></span>
  * <span data-ttu-id="8326f-131">Implémentation de référence de l’extension de machine virtuelle à l’adresse [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="8326f-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="8326f-132">Communication</span><span class="sxs-lookup"><span data-stu-id="8326f-132">Communication</span></span>
<span data-ttu-id="8326f-133">Hello flux d’informations à partir de l’agent de hello plateforme toohello se produit via deux canaux :</span><span class="sxs-lookup"><span data-stu-id="8326f-133">hello information flow from hello platform toohello agent occurs via two channels:</span></span>

* <span data-ttu-id="8326f-134">Un DVD attaché au moment du démarrage pour les déploiements IaaS.</span><span class="sxs-lookup"><span data-stu-id="8326f-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="8326f-135">Ce DVD comprend un fichier de configuration conformes OVF qui inclut toutes les informations de configuration autre que les paires de clés hello réel SSH.</span><span class="sxs-lookup"><span data-stu-id="8326f-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than hello actual SSH keypairs.</span></span>
* <span data-ttu-id="8326f-136">Un point de terminaison TCP exposer une API REST utilisée tooobtain déploiement et configuration de la topologie.</span><span class="sxs-lookup"><span data-stu-id="8326f-136">A TCP endpoint exposing a REST API used tooobtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="8326f-137">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="8326f-137">Requirements</span></span>
<span data-ttu-id="8326f-138">Hello systèmes suivants ont été testées et sont connues toowork avec hello Linux Agent Azure :</span><span class="sxs-lookup"><span data-stu-id="8326f-138">hello following systems have been tested and are known toowork with hello Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="8326f-139">Cette liste peut différer de la liste officielle de hello des systèmes pris en charge sur hello plateforme Microsoft Azure, comme décrit ici : [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span><span class="sxs-lookup"><span data-stu-id="8326f-139">This list may differ from hello official list of supported systems on hello Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="8326f-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="8326f-140">CoreOS</span></span>
* <span data-ttu-id="8326f-141">CentOS 6.3+</span><span class="sxs-lookup"><span data-stu-id="8326f-141">CentOS 6.3+</span></span>
* <span data-ttu-id="8326f-142">Red Hat Enterprise Linux 6.7+</span><span class="sxs-lookup"><span data-stu-id="8326f-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="8326f-143">Debian 7.0+</span><span class="sxs-lookup"><span data-stu-id="8326f-143">Debian 7.0+</span></span>
* <span data-ttu-id="8326f-144">Ubuntu 12.04+</span><span class="sxs-lookup"><span data-stu-id="8326f-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="8326f-145">openSUSE 12.3+</span><span class="sxs-lookup"><span data-stu-id="8326f-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="8326f-146">SLES 11 SP3+</span><span class="sxs-lookup"><span data-stu-id="8326f-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="8326f-147">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="8326f-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="8326f-148">Autres systèmes pris en charge :</span><span class="sxs-lookup"><span data-stu-id="8326f-148">Other Supported Systems:</span></span>

* <span data-ttu-id="8326f-149">FreeBSD 10+ (agent Azure Linux v2.0.10+)</span><span class="sxs-lookup"><span data-stu-id="8326f-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="8326f-150">l’agent de Linux Hello dépend de certains packages de système dans l’ordre toofunction correctement :</span><span class="sxs-lookup"><span data-stu-id="8326f-150">hello Linux agent depends on some system packages in order toofunction properly:</span></span>

* <span data-ttu-id="8326f-151">Python 2.6+</span><span class="sxs-lookup"><span data-stu-id="8326f-151">Python 2.6+</span></span>
* <span data-ttu-id="8326f-152">OpenSSL 1.0+</span><span class="sxs-lookup"><span data-stu-id="8326f-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="8326f-153">OpenSSH 5.3+</span><span class="sxs-lookup"><span data-stu-id="8326f-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="8326f-154">Utilitaires de système de fichiers : sfdisk, fdisk, mkfs, séparés</span><span class="sxs-lookup"><span data-stu-id="8326f-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="8326f-155">Outils de mot de passe : chpasswd, sudo</span><span class="sxs-lookup"><span data-stu-id="8326f-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="8326f-156">Outils de traitement de texte : sed, grep</span><span class="sxs-lookup"><span data-stu-id="8326f-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="8326f-157">Outils réseau : ip-route</span><span class="sxs-lookup"><span data-stu-id="8326f-157">Network tools: ip-route</span></span>
* <span data-ttu-id="8326f-158">Prise en charge du noyau pour le montage de systèmes de fichiers UDF.</span><span class="sxs-lookup"><span data-stu-id="8326f-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="8326f-159">Installation</span><span class="sxs-lookup"><span data-stu-id="8326f-159">Installation</span></span>
<span data-ttu-id="8326f-160">Installation à l’aide d’un fichier RPM ou un package DEB à partir d’un référentiel de packages de distribution de votre est la méthode hello préféré de l’installation et la mise à niveau hello Linux Agent Azure.</span><span class="sxs-lookup"><span data-stu-id="8326f-160">Installation using an RPM or a DEB package from your distribution's package repository is hello preferred method of installing and upgrading hello Azure Linux Agent.</span></span> <span data-ttu-id="8326f-161">Tous les hello [approuvée des fournisseurs de distribution](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) intégrer leurs images et des référentiels du package de l’agent Azure Linux hello.</span><span class="sxs-lookup"><span data-stu-id="8326f-161">All hello [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate hello Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="8326f-162">Consultez la documentation du toohello Bonjour [référentiel Linux Agent Azure sur GitHub](https://github.com/Azure/WALinuxAgent) pour les options d’installation avancées, telles que l’installation à partir d’emplacements source ou toocustom ou de préfixes.</span><span class="sxs-lookup"><span data-stu-id="8326f-162">Refer toohello documentation in hello [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or toocustom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="8326f-163">Options de la ligne de commande</span><span class="sxs-lookup"><span data-stu-id="8326f-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="8326f-164">Indicateurs</span><span class="sxs-lookup"><span data-stu-id="8326f-164">Flags</span></span>
* <span data-ttu-id="8326f-165">verbose : accroît le niveau de détail de la commande spécifiée.</span><span class="sxs-lookup"><span data-stu-id="8326f-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="8326f-166">force : ignore la confirmation interactive de certaines commandes.</span><span class="sxs-lookup"><span data-stu-id="8326f-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="8326f-167">Commandes</span><span class="sxs-lookup"><span data-stu-id="8326f-167">Commands</span></span>
* <span data-ttu-id="8326f-168">aide : répertorie les commandes hello pris en charge et les indicateurs.</span><span class="sxs-lookup"><span data-stu-id="8326f-168">help: Lists hello supported commands and flags.</span></span>
* <span data-ttu-id="8326f-169">annulation du déploiement : tentative de système de hello tooclean et adapté à la reconfiguration.</span><span class="sxs-lookup"><span data-stu-id="8326f-169">deprovision: Attempt tooclean hello system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="8326f-170">Cette opération supprimé suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="8326f-170">This operation deleted hello following:</span></span>
  
  * <span data-ttu-id="8326f-171">Toutes les clés d’hôte SSH (si Provisioning.RegenerateSshHostKeyPair est « y » dans le fichier de configuration hello)</span><span class="sxs-lookup"><span data-stu-id="8326f-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="8326f-172">la configuration de Nameserver dans /etc/resolv.conf ;</span><span class="sxs-lookup"><span data-stu-id="8326f-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="8326f-173">Mot de passe racine à partir / etc/shadow (si Provisioning.DeleteRootPassword est « y » dans le fichier de configuration hello)</span><span class="sxs-lookup"><span data-stu-id="8326f-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in hello configuration file)</span></span>
  * <span data-ttu-id="8326f-174">les baux du client DHCP mis en cache.</span><span class="sxs-lookup"><span data-stu-id="8326f-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="8326f-175">Réinitialise héberge nom toolocalhost.localdomain</span><span class="sxs-lookup"><span data-stu-id="8326f-175">Resets host name toolocalhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="8326f-176">Mise hors service ne garantit pas que cette image hello est désactivée de toutes les informations sensibles et appropriée pour la redistribution.</span><span class="sxs-lookup"><span data-stu-id="8326f-176">Deprovisioning does not guarantee that hello image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="8326f-177">Annuler le déploiement + utilisateur : effectue tout sous - deprovision (ci-dessus) et également supprime hello dernier compte d’utilisateur configuré (obtenu à partir de /var/lib/waagent) et les données associées.</span><span class="sxs-lookup"><span data-stu-id="8326f-177">deprovision+user: Performs everything under -deprovision (above) and also deletes hello last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="8326f-178">Ce paramètre est utilisé pour annuler l'approvisionnement d'une image qui a été précédemment approvisionnée sur Azure en vue d'être capturée et réutilisée.</span><span class="sxs-lookup"><span data-stu-id="8326f-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="8326f-179">version : affiche la version de waagent hello</span><span class="sxs-lookup"><span data-stu-id="8326f-179">version: Displays hello version of waagent</span></span>
* <span data-ttu-id="8326f-180">serialconsole : Configure GRUB toomark ttyS0 (hello le premier port série) en tant que console de démarrage hello.</span><span class="sxs-lookup"><span data-stu-id="8326f-180">serialconsole: Configures GRUB toomark ttyS0 (hello first serial port) as hello boot console.</span></span> <span data-ttu-id="8326f-181">Cela garantit que les journaux du démarrage du noyau sont envoyés de port série toothe et sont accessibles pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="8326f-181">This ensures that kernel bootup logs are sent toothe serial port and made available for debugging.</span></span>
* <span data-ttu-id="8326f-182">démon : exécuté waagent comme une interaction de toomanage démon avec la plateforme de hello.</span><span class="sxs-lookup"><span data-stu-id="8326f-182">daemon: Run waagent as a daemon toomanage interaction with hello platform.</span></span> <span data-ttu-id="8326f-183">Cet argument est toowaagent spécifié dans le script d’initialisation waagent hello.</span><span class="sxs-lookup"><span data-stu-id="8326f-183">This argument is specified toowaagent in hello waagent init script.</span></span>
* <span data-ttu-id="8326f-184">start : exécute waagent en arrière-plan</span><span class="sxs-lookup"><span data-stu-id="8326f-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="8326f-185">Configuration</span><span class="sxs-lookup"><span data-stu-id="8326f-185">Configuration</span></span>
<span data-ttu-id="8326f-186">Un fichier de configuration (/ etc/waagent.conf) contrôles hello actions de waagent.</span><span class="sxs-lookup"><span data-stu-id="8326f-186">A configuration file (/etc/waagent.conf) controls hello actions of waagent.</span></span> <span data-ttu-id="8326f-187">Un exemple de fichier de configuration est affiché ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8326f-187">A sample configuration file is shown below:</span></span>

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

<span data-ttu-id="8326f-188">Hello que différentes options de configuration sont décrites en détail ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8326f-188">hello various configuration options are described in detail below.</span></span> <span data-ttu-id="8326f-189">Elles sont de trois types : Boolean, String ou Integer.</span><span class="sxs-lookup"><span data-stu-id="8326f-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="8326f-190">options de configuration booléenne de Hello peuvent être spécifiées en tant que « y » ou « n ».</span><span class="sxs-lookup"><span data-stu-id="8326f-190">hello Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="8326f-191">Bonjour mot clé spécial « None » peut être utilisé pour une chaîne type entrées de configuration comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8326f-191">hello special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="8326f-192">**Provisioning.Enabled :**</span><span class="sxs-lookup"><span data-stu-id="8326f-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="8326f-193">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="8326f-193">Type: Boolean</span></span>  
<span data-ttu-id="8326f-194">Par défaut : y</span><span class="sxs-lookup"><span data-stu-id="8326f-194">Default: y</span></span>

<span data-ttu-id="8326f-195">Cela permet de hello utilisateur tooenable ou désactiver hello configuration des fonctionnalités de l’agent de hello.</span><span class="sxs-lookup"><span data-stu-id="8326f-195">This allows hello user tooenable or disable hello provisioning functionality in hello agent.</span></span> <span data-ttu-id="8326f-196">Les valeurs valides sont « y » ou « n ».</span><span class="sxs-lookup"><span data-stu-id="8326f-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="8326f-197">Si la configuration est désactivée, clés d’hôte et d’utilisateur SSH dans l’image de hello sont conservés et toute configuration spécifiée Bonjour Azure API de configuration est ignorée.</span><span class="sxs-lookup"><span data-stu-id="8326f-197">If provisioning is disabled, SSH host and user keys in hello image are preserved and any configuration specified in hello Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="8326f-198">Hello `Provisioning.Enabled` trop « n » sur les Images de Cloud Ubuntu qui utilisent cloud-init pour la configuration de paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="8326f-198">hello `Provisioning.Enabled` parameter defaults too"n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="8326f-199">**Provisioning.DeleteRootPassword :**</span><span class="sxs-lookup"><span data-stu-id="8326f-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="8326f-200">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="8326f-200">Type: Boolean</span></span>  
<span data-ttu-id="8326f-201">Par défaut : n</span><span class="sxs-lookup"><span data-stu-id="8326f-201">Default: n</span></span>

<span data-ttu-id="8326f-202">Si set, mot de passe racine hello dans le fichier de clichés instantanés/etc/hello est effacé au cours de hello le processus d’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="8326f-202">If set, hello root password in hello /etc/shadow file is erased during hello provisioning process.</span></span>

<span data-ttu-id="8326f-203">**Provisioning.RegenerateSshHostKeyPair :**</span><span class="sxs-lookup"><span data-stu-id="8326f-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="8326f-204">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="8326f-204">Type: Boolean</span></span>  
<span data-ttu-id="8326f-205">Par défaut : y</span><span class="sxs-lookup"><span data-stu-id="8326f-205">Default: y</span></span>

<span data-ttu-id="8326f-206">Si l’ensemble, tous les SSH hôte paires de clés (ecdsa, dsa et rsa) est supprimé lors de hello processus à partir d’etc/ssh/de configuration.</span><span class="sxs-lookup"><span data-stu-id="8326f-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during hello provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="8326f-207">Une nouvelle paire de clés unique est générée.</span><span class="sxs-lookup"><span data-stu-id="8326f-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="8326f-208">le type de chiffrement Hello pour la nouvelle paire de clés de hello est configurable par hello Provisioning.SshHostKeyPairType entrée.</span><span class="sxs-lookup"><span data-stu-id="8326f-208">hello encryption type for hello fresh key pair is configurable by hello Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="8326f-209">Notez que certaines distributions recréera les paires de clés SSH pour les types de chiffrement manquant lorsque le démon SSH hello redémarre (par exemple, après un redémarrage).</span><span class="sxs-lookup"><span data-stu-id="8326f-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when hello SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="8326f-210">**Provisioning.SshHostKeyPairType :**</span><span class="sxs-lookup"><span data-stu-id="8326f-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="8326f-211">Type : string</span><span class="sxs-lookup"><span data-stu-id="8326f-211">Type: String</span></span>  
<span data-ttu-id="8326f-212">Par défaut : rsa</span><span class="sxs-lookup"><span data-stu-id="8326f-212">Default: rsa</span></span>

<span data-ttu-id="8326f-213">Type d’algorithme de chiffrement tooan est pris en charge par le démon SSH hello sur l’ordinateur virtuel de hello celle-ci peut être définie.</span><span class="sxs-lookup"><span data-stu-id="8326f-213">This can be set tooan encryption algorithm type that is supported by hello SSH daemon on hello virtual machine.</span></span> <span data-ttu-id="8326f-214">les valeurs Hello généralement prises en charge sont « rsa », « dsa » et « ecdsa ».</span><span class="sxs-lookup"><span data-stu-id="8326f-214">hello typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="8326f-215">Notez que « putty.exe » sur Windows ne prend pas en charge « ecdsa ».</span><span class="sxs-lookup"><span data-stu-id="8326f-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="8326f-216">Par conséquent, si vous envisagez de toouse putty.exe Windows tooconnect tooa déploiement Linux, utilisez « rsa » ou « dsa ».</span><span class="sxs-lookup"><span data-stu-id="8326f-216">So, if you intend toouse putty.exe on Windows tooconnect tooa Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="8326f-217">**Provisioning.MonitorHostName :**</span><span class="sxs-lookup"><span data-stu-id="8326f-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="8326f-218">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="8326f-218">Type: Boolean</span></span>  
<span data-ttu-id="8326f-219">Par défaut : y</span><span class="sxs-lookup"><span data-stu-id="8326f-219">Default: y</span></span>

<span data-ttu-id="8326f-220">Si défini, waagent analysez hello Linux virtual machine pour les modifications de nom d’hôte (tel que renvoyé par la commande de « hostname » hello) et mettre à jour automatiquement la configuration du réseau dans la modification de hello hello image tooreflect hello.</span><span class="sxs-lookup"><span data-stu-id="8326f-220">If set, waagent will monitor hello Linux virtual machine for hostname changes (as returned by hello "hostname" command) and automatically update hello networking configuration in hello image tooreflect hello change.</span></span> <span data-ttu-id="8326f-221">Dans le nom de l’ordre toopush hello modifier les serveurs DNS toohello, mise en réseau sera redémarré dans la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="8326f-221">In order toopush hello name change toohello DNS servers, networking will be restarted in hello virtual machine.</span></span> <span data-ttu-id="8326f-222">La connexion Internet est alors brièvement interrompue.</span><span class="sxs-lookup"><span data-stu-id="8326f-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="8326f-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="8326f-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="8326f-224">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="8326f-224">Type: Boolean</span></span>  
<span data-ttu-id="8326f-225">Par défaut : n</span><span class="sxs-lookup"><span data-stu-id="8326f-225">Default: n</span></span>

<span data-ttu-id="8326f-226">Si ce paramètre est défini, waagent décodera CustomData en Base64.</span><span class="sxs-lookup"><span data-stu-id="8326f-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="8326f-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="8326f-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="8326f-228">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="8326f-228">Type: Boolean</span></span>  
<span data-ttu-id="8326f-229">Par défaut : n</span><span class="sxs-lookup"><span data-stu-id="8326f-229">Default: n</span></span>

<span data-ttu-id="8326f-230">Si ce paramètre est défini, waagent exécute CustomData après l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="8326f-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="8326f-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="8326f-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="8326f-232">Type : chaîne</span><span class="sxs-lookup"><span data-stu-id="8326f-232">Type:String</span></span>  
<span data-ttu-id="8326f-233">Par défaut : 6</span><span class="sxs-lookup"><span data-stu-id="8326f-233">Default:6</span></span>

<span data-ttu-id="8326f-234">Algorithme utilisé par crypt lors de la génération du hachage de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="8326f-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="8326f-235">1 - MD5</span><span class="sxs-lookup"><span data-stu-id="8326f-235">1 - MD5</span></span>  
 <span data-ttu-id="8326f-236">2 a - Blowfish</span><span class="sxs-lookup"><span data-stu-id="8326f-236">2a - Blowfish</span></span>  
 <span data-ttu-id="8326f-237">5 - SHA-256</span><span class="sxs-lookup"><span data-stu-id="8326f-237">5 - SHA-256</span></span>  
 <span data-ttu-id="8326f-238">6 - SHA-512</span><span class="sxs-lookup"><span data-stu-id="8326f-238">6 - SHA-512</span></span>  

<span data-ttu-id="8326f-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="8326f-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="8326f-240">Type : chaîne</span><span class="sxs-lookup"><span data-stu-id="8326f-240">Type:String</span></span>  
<span data-ttu-id="8326f-241">Par défaut : 10</span><span class="sxs-lookup"><span data-stu-id="8326f-241">Default:10</span></span>

<span data-ttu-id="8326f-242">Longueur de la chaîne salt aléatoire utilisée lors de la génération du hachage de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="8326f-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="8326f-243">**ResourceDisk.Format :**</span><span class="sxs-lookup"><span data-stu-id="8326f-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="8326f-244">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="8326f-244">Type: Boolean</span></span>  
<span data-ttu-id="8326f-245">Par défaut : y</span><span class="sxs-lookup"><span data-stu-id="8326f-245">Default: y</span></span>

<span data-ttu-id="8326f-246">Si la valeur, disque de ressources hello fournie par la plateforme de hello sera formaté et monté par waagent si le type de système de fichiers hello demandé par l’utilisateur hello dans « ResourceDisk.Filesystem » n’est pas « ntfs ».</span><span class="sxs-lookup"><span data-stu-id="8326f-246">If set, hello resource disk provided by hello platform will be formatted and mounted by waagent if hello filesystem type requested by hello user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="8326f-247">Une partition unique de type Linux (83) sera disponible sur le disque de hello.</span><span class="sxs-lookup"><span data-stu-id="8326f-247">A single partition of type Linux (83) will be made available on hello disk.</span></span> <span data-ttu-id="8326f-248">Notez que cette partition n'est pas formatée si elle ne peut pas être correctement montée.</span><span class="sxs-lookup"><span data-stu-id="8326f-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="8326f-249">**ResourceDisk.Filesystem :**</span><span class="sxs-lookup"><span data-stu-id="8326f-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="8326f-250">Type : string</span><span class="sxs-lookup"><span data-stu-id="8326f-250">Type: String</span></span>  
<span data-ttu-id="8326f-251">Par défaut : ext4</span><span class="sxs-lookup"><span data-stu-id="8326f-251">Default: ext4</span></span>

<span data-ttu-id="8326f-252">Cela spécifie le type de système de fichiers hello pour le disque de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="8326f-252">This specifies hello filesystem type for hello resource disk.</span></span> <span data-ttu-id="8326f-253">Les valeurs prises en charge diffèrent selon la distribution Linux.</span><span class="sxs-lookup"><span data-stu-id="8326f-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="8326f-254">Si la chaîne de hello est X, puis mkfs. X doit être présent sur l’image de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="8326f-254">If hello string is X, then mkfs.X should be present on hello Linux image.</span></span> <span data-ttu-id="8326f-255">Les images SLES 11 doivent généralement utiliser « ext3 ».</span><span class="sxs-lookup"><span data-stu-id="8326f-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="8326f-256">Les images FreeBSD doivent utiliser « ufs2 » ici.</span><span class="sxs-lookup"><span data-stu-id="8326f-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="8326f-257">**ResourceDisk.MountPoint :**</span><span class="sxs-lookup"><span data-stu-id="8326f-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="8326f-258">Type : string</span><span class="sxs-lookup"><span data-stu-id="8326f-258">Type: String</span></span>  
<span data-ttu-id="8326f-259">Par défaut : /mnt/resource</span><span class="sxs-lookup"><span data-stu-id="8326f-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="8326f-260">Cela spécifie le chemin d’accès hello à laquelle le disque de ressources hello est monté.</span><span class="sxs-lookup"><span data-stu-id="8326f-260">This specifies hello path at which hello resource disk is mounted.</span></span> <span data-ttu-id="8326f-261">Notez que le disque ressource hello un *temporaire* disque et peut être vidé lorsque hello machine virtuelle est déprovisionnée.</span><span class="sxs-lookup"><span data-stu-id="8326f-261">Note that hello resource disk is a *temporary* disk, and might be emptied when hello VM is deprovisioned.</span></span>

<span data-ttu-id="8326f-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="8326f-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="8326f-263">Type : string</span><span class="sxs-lookup"><span data-stu-id="8326f-263">Type: String</span></span>  
<span data-ttu-id="8326f-264">Par défaut : aucun</span><span class="sxs-lookup"><span data-stu-id="8326f-264">Default: None</span></span>

<span data-ttu-id="8326f-265">Spécifie le disque montage options toobe passé toohello mount -o commande.</span><span class="sxs-lookup"><span data-stu-id="8326f-265">Specifies disk mount options toobe passed toohello mount -o command.</span></span> <span data-ttu-id="8326f-266">Les valeurs de cette liste sont séparées par des virgules, par exemple</span><span class="sxs-lookup"><span data-stu-id="8326f-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="8326f-267">'nodev,nosuid'.</span><span class="sxs-lookup"><span data-stu-id="8326f-267">'nodev,nosuid'.</span></span> <span data-ttu-id="8326f-268">Pour plus d’informations, consultez mount(8).</span><span class="sxs-lookup"><span data-stu-id="8326f-268">See mount(8) for details.</span></span>

<span data-ttu-id="8326f-269">**ResourceDisk.EnableSwap :**</span><span class="sxs-lookup"><span data-stu-id="8326f-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="8326f-270">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="8326f-270">Type: Boolean</span></span>  
<span data-ttu-id="8326f-271">Par défaut : n</span><span class="sxs-lookup"><span data-stu-id="8326f-271">Default: n</span></span>

<span data-ttu-id="8326f-272">Si défini, un fichier d’échange (/ fichier d’échange) est créé sur le disque de ressources hello et ajouté l’espace d’échange système toohello.</span><span class="sxs-lookup"><span data-stu-id="8326f-272">If set, a swap file (/swapfile) is created on hello resource disk and added toohello system swap space.</span></span>

<span data-ttu-id="8326f-273">**ResourceDisk.SwapSizeMB :**</span><span class="sxs-lookup"><span data-stu-id="8326f-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="8326f-274">Type : entier</span><span class="sxs-lookup"><span data-stu-id="8326f-274">Type: Integer</span></span>  
<span data-ttu-id="8326f-275">Par défaut : 0</span><span class="sxs-lookup"><span data-stu-id="8326f-275">Default: 0</span></span>

<span data-ttu-id="8326f-276">taille de Hello hello du fichier d’échange en mégaoctets.</span><span class="sxs-lookup"><span data-stu-id="8326f-276">hello size of hello swap file in megabytes.</span></span>

<span data-ttu-id="8326f-277">**Logs.Verbose :**</span><span class="sxs-lookup"><span data-stu-id="8326f-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="8326f-278">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="8326f-278">Type: Boolean</span></span>  
<span data-ttu-id="8326f-279">Par défaut : n</span><span class="sxs-lookup"><span data-stu-id="8326f-279">Default: n</span></span>

<span data-ttu-id="8326f-280">Si elle est définie, le niveau de détail du journal est optimisé.</span><span class="sxs-lookup"><span data-stu-id="8326f-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="8326f-281">Waagent journaux too/var/log/waagent.log et tire parti des fonctionnalités toorotate journaux de hello système logrotate.</span><span class="sxs-lookup"><span data-stu-id="8326f-281">Waagent logs too/var/log/waagent.log and leverages hello system logrotate functionality toorotate logs.</span></span>

<span data-ttu-id="8326f-282">**OS.EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="8326f-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="8326f-283">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="8326f-283">Type: Boolean</span></span>  
<span data-ttu-id="8326f-284">Par défaut : n</span><span class="sxs-lookup"><span data-stu-id="8326f-284">Default: n</span></span>

<span data-ttu-id="8326f-285">Si la valeur, hello agent essayez tooinstall et ensuite charger un pilote de noyau RDMA qui correspond à la version de hello du microprogramme hello sur hello matériel sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="8326f-285">If set, hello agent will attempt tooinstall and then load an RDMA kernel driver that matches hello version of hello firmware on hello underlying hardware.</span></span>

<span data-ttu-id="8326f-286">**OS.RootDeviceScsiTimeout :**</span><span class="sxs-lookup"><span data-stu-id="8326f-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="8326f-287">Type : entier</span><span class="sxs-lookup"><span data-stu-id="8326f-287">Type: Integer</span></span>  
<span data-ttu-id="8326f-288">Par défaut : 300</span><span class="sxs-lookup"><span data-stu-id="8326f-288">Default: 300</span></span>

<span data-ttu-id="8326f-289">Cela configure le délai d’attente de hello SCSI en secondes sur les lecteurs de disque et les données hello du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="8326f-289">This configures hello SCSI timeout in seconds on hello OS disk and data drives.</span></span> <span data-ttu-id="8326f-290">Si la valeur n’est pas définie, les valeurs par défaut sont utilisées par le système hello.</span><span class="sxs-lookup"><span data-stu-id="8326f-290">If not set, hello system defaults are used.</span></span>

<span data-ttu-id="8326f-291">**OS.OpensslPath :**</span><span class="sxs-lookup"><span data-stu-id="8326f-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="8326f-292">Type : string</span><span class="sxs-lookup"><span data-stu-id="8326f-292">Type: String</span></span>  
<span data-ttu-id="8326f-293">Par défaut : aucun</span><span class="sxs-lookup"><span data-stu-id="8326f-293">Default: None</span></span>

<span data-ttu-id="8326f-294">Cela peut être utilisé toospecify un chemin alternatif pour toouse binaire d’openssl hello pour les opérations de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="8326f-294">This can be used toospecify an alternate path for hello openssl binary toouse for cryptographic operations.</span></span>

<span data-ttu-id="8326f-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="8326f-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="8326f-296">Type : string</span><span class="sxs-lookup"><span data-stu-id="8326f-296">Type: String</span></span>  
<span data-ttu-id="8326f-297">Par défaut : aucun</span><span class="sxs-lookup"><span data-stu-id="8326f-297">Default: None</span></span>

<span data-ttu-id="8326f-298">Si, l’agent de hello utilisera ce proxy server tooaccess hello internet.</span><span class="sxs-lookup"><span data-stu-id="8326f-298">If set, hello agent will use this proxy server tooaccess hello internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="8326f-299">Images cloud Ubuntu</span><span class="sxs-lookup"><span data-stu-id="8326f-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="8326f-300">Notez que Ubuntu Cloud Images utilisent [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform nombreuses tâches de configuration qui seraient sinon gérés par hello Linux Agent Azure.</span><span class="sxs-lookup"><span data-stu-id="8326f-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) tooperform many configuration tasks that would otherwise be managed by hello Azure Linux Agent.</span></span>  <span data-ttu-id="8326f-301">Veuillez noter hello suivant différences :</span><span class="sxs-lookup"><span data-stu-id="8326f-301">Please note hello following differences:</span></span>

* <span data-ttu-id="8326f-302">**Provisioning.Enabled** trop « n » sur les Images de Cloud Ubuntu qui utilisent tooperform cloud-init des tâches de configuration par défaut.</span><span class="sxs-lookup"><span data-stu-id="8326f-302">**Provisioning.Enabled** defaults too"n" on Ubuntu Cloud Images that use cloud-init tooperform provisioning tasks.</span></span>
* <span data-ttu-id="8326f-303">Hello, paramètres de configuration suivants ont aucun effet sur Ubuntu Cloud Images qui utilisent cloud-init toomanage hello ressources disque et échange d’espace :</span><span class="sxs-lookup"><span data-stu-id="8326f-303">hello following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init toomanage hello resource disk and swap space:</span></span>
  
  * <span data-ttu-id="8326f-304">**ResourceDisk.Format**</span><span class="sxs-lookup"><span data-stu-id="8326f-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="8326f-305">**ResourceDisk.Filesystem**</span><span class="sxs-lookup"><span data-stu-id="8326f-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="8326f-306">**ResourceDisk.MountPoint**</span><span class="sxs-lookup"><span data-stu-id="8326f-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="8326f-307">**ResourceDisk.EnableSwap**</span><span class="sxs-lookup"><span data-stu-id="8326f-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="8326f-308">**ResourceDisk.SwapSizeMB**</span><span class="sxs-lookup"><span data-stu-id="8326f-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="8326f-309">Consultez hello après le point de montage de disque de ressources ressources tooconfigure hello et échange d’espace sur les Images de Cloud Ubuntu lors de la configuration :</span><span class="sxs-lookup"><span data-stu-id="8326f-309">Please see hello following resources tooconfigure hello resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="8326f-310">Wiki Ubuntu : Configurer les partitions d’échange</span><span class="sxs-lookup"><span data-stu-id="8326f-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="8326f-311">Injection de données personnalisées dans une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="8326f-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

