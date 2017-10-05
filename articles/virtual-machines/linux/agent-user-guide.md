---
title: "Vue d’ensemble de l’agent de machine virtuelle Linux Azure | Microsoft Docs"
description: "Apprenez à installer et à configurer l'agent Linux (waagent) pour gérer l'interaction de votre machine virtuelle avec le contrôleur de structure Azure."
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
ms.openlocfilehash: 486ad6bb148583a957fb82b7954ff94f853b12cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="understanding-and-using-the-azure-linux-agent"></a><span data-ttu-id="7d195-103">Présentation et utilisation de l’agent Linux Azure</span><span class="sxs-lookup"><span data-stu-id="7d195-103">Understanding and using the Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="7d195-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="7d195-104">Introduction</span></span>
<span data-ttu-id="7d195-105">L’agent Microsoft Azure Linux (waagent) gère l’approvisionnement de Linux et FreeBSD, ainsi que l’interaction des machines virtuelles avec le contrôleur de structure Azure.</span><span class="sxs-lookup"><span data-stu-id="7d195-105">The Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="7d195-106">Il offre les fonctionnalités suivantes pour les déploiements IaaS Linux et FreeBSD :</span><span class="sxs-lookup"><span data-stu-id="7d195-106">It provides the following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="7d195-107">Pour plus d’informations, consultez le fichier [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) de l’agent Linux Azure.</span><span class="sxs-lookup"><span data-stu-id="7d195-107">See the Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="7d195-108">**Approvisionnement d’image**</span><span class="sxs-lookup"><span data-stu-id="7d195-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="7d195-109">Création d'un compte d'utilisateur</span><span class="sxs-lookup"><span data-stu-id="7d195-109">Creation of a user account</span></span>
  * <span data-ttu-id="7d195-110">Configuration des types d'authentification SSH</span><span class="sxs-lookup"><span data-stu-id="7d195-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="7d195-111">Déploiement des clés publiques et des paires de clés SSH</span><span class="sxs-lookup"><span data-stu-id="7d195-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="7d195-112">Définition du nom d'hôte</span><span class="sxs-lookup"><span data-stu-id="7d195-112">Setting the host name</span></span>
  * <span data-ttu-id="7d195-113">Publication du nom d'hôte sur la plateforme DNS</span><span class="sxs-lookup"><span data-stu-id="7d195-113">Publishing the host name to the platform DNS</span></span>
  * <span data-ttu-id="7d195-114">Génération de rapports sur l'empreinte digitale de la clé d'hôte SSH destinés à la plateforme</span><span class="sxs-lookup"><span data-stu-id="7d195-114">Reporting SSH host key fingerprint to the platform</span></span>
  * <span data-ttu-id="7d195-115">Gestion du disque de ressources</span><span class="sxs-lookup"><span data-stu-id="7d195-115">Resource Disk Management</span></span>
  * <span data-ttu-id="7d195-116">Formatage et montage du disque de ressources</span><span class="sxs-lookup"><span data-stu-id="7d195-116">Formatting and mounting the resource disk</span></span>
  * <span data-ttu-id="7d195-117">Configuration de l'espace d'échange</span><span class="sxs-lookup"><span data-stu-id="7d195-117">Configuring swap space</span></span>
* <span data-ttu-id="7d195-118">**Mise en réseau**</span><span class="sxs-lookup"><span data-stu-id="7d195-118">**Networking**</span></span>
  
  * <span data-ttu-id="7d195-119">Gestion des itinéraires afin d'améliorer la compatibilité avec les serveurs DHCP de plateforme</span><span class="sxs-lookup"><span data-stu-id="7d195-119">Manages routes to improve compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="7d195-120">Garantie de la stabilité du nom de l'interface réseau</span><span class="sxs-lookup"><span data-stu-id="7d195-120">Ensures the stability of the network interface name</span></span>
* <span data-ttu-id="7d195-121">**Noyau**</span><span class="sxs-lookup"><span data-stu-id="7d195-121">**Kernel**</span></span>
  
  * <span data-ttu-id="7d195-122">Configure la topologie NUMA virtuelle (désactivée pour le noyau < à 2.6.37)</span><span class="sxs-lookup"><span data-stu-id="7d195-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="7d195-123">Consommation de l'entropie Hyper-V pour /dev/random</span><span class="sxs-lookup"><span data-stu-id="7d195-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="7d195-124">Configuration des délais d'expiration SCSI de l'appareil racine (qui peut être distant)</span><span class="sxs-lookup"><span data-stu-id="7d195-124">Configures SCSI timeouts for the root device (which could be remote)</span></span>
* <span data-ttu-id="7d195-125">**Diagnostics**</span><span class="sxs-lookup"><span data-stu-id="7d195-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="7d195-126">Redirection de la console vers le port série</span><span class="sxs-lookup"><span data-stu-id="7d195-126">Console redirection to the serial port</span></span>
* <span data-ttu-id="7d195-127">**Déploiements SCVMM**</span><span class="sxs-lookup"><span data-stu-id="7d195-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="7d195-128">Détection et amorçage de l'agent VMM pour Linux lors de l'exécution dans un environnement System Center Virtual Machine Manager 2012 R2</span><span class="sxs-lookup"><span data-stu-id="7d195-128">Detects and bootstraps the VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="7d195-129">**Extension de machine virtuelle**</span><span class="sxs-lookup"><span data-stu-id="7d195-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="7d195-130">Injection de composants créés par Microsoft et ses partenaires dans la machine virtuelle Linux pour activer les logiciels et l’automatisation de la configuration</span><span class="sxs-lookup"><span data-stu-id="7d195-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) to enable software and configuration automation</span></span>
  * <span data-ttu-id="7d195-131">Implémentation de référence de l’extension de machine virtuelle à l’adresse [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="7d195-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="7d195-132">Communication</span><span class="sxs-lookup"><span data-stu-id="7d195-132">Communication</span></span>
<span data-ttu-id="7d195-133">Le flux d'informations de la plateforme à l'agent se produit via deux canaux :</span><span class="sxs-lookup"><span data-stu-id="7d195-133">The information flow from the platform to the agent occurs via two channels:</span></span>

* <span data-ttu-id="7d195-134">Un DVD attaché au moment du démarrage pour les déploiements IaaS.</span><span class="sxs-lookup"><span data-stu-id="7d195-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="7d195-135">Ce DVD comprend un fichier de configuration compatible OVF qui inclut toutes les informations d'approvisionnement différentes des paires de clés SSH réelles.</span><span class="sxs-lookup"><span data-stu-id="7d195-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than the actual SSH keypairs.</span></span>
* <span data-ttu-id="7d195-136">Un point de terminaison TCP qui expose une API REST utilisée pour obtenir la configuration du déploiement et de la topologie.</span><span class="sxs-lookup"><span data-stu-id="7d195-136">A TCP endpoint exposing a REST API used to obtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="7d195-137">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="7d195-137">Requirements</span></span>
<span data-ttu-id="7d195-138">Les systèmes suivants ont été testés et fonctionnent avec l’agent Linux Azure :</span><span class="sxs-lookup"><span data-stu-id="7d195-138">The following systems have been tested and are known to work with the Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="7d195-139">Notez que cette liste peut être différente de la liste officielle des systèmes pris en charge sur la plateforme Microsoft Azure, disponible ici : [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span><span class="sxs-lookup"><span data-stu-id="7d195-139">This list may differ from the official list of supported systems on the Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="7d195-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="7d195-140">CoreOS</span></span>
* <span data-ttu-id="7d195-141">CentOS 6.3+</span><span class="sxs-lookup"><span data-stu-id="7d195-141">CentOS 6.3+</span></span>
* <span data-ttu-id="7d195-142">Red Hat Enterprise Linux 6.7+</span><span class="sxs-lookup"><span data-stu-id="7d195-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="7d195-143">Debian 7.0+</span><span class="sxs-lookup"><span data-stu-id="7d195-143">Debian 7.0+</span></span>
* <span data-ttu-id="7d195-144">Ubuntu 12.04+</span><span class="sxs-lookup"><span data-stu-id="7d195-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="7d195-145">openSUSE 12.3+</span><span class="sxs-lookup"><span data-stu-id="7d195-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="7d195-146">SLES 11 SP3+</span><span class="sxs-lookup"><span data-stu-id="7d195-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="7d195-147">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="7d195-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="7d195-148">Autres systèmes pris en charge :</span><span class="sxs-lookup"><span data-stu-id="7d195-148">Other Supported Systems:</span></span>

* <span data-ttu-id="7d195-149">FreeBSD 10+ (agent Azure Linux v2.0.10+)</span><span class="sxs-lookup"><span data-stu-id="7d195-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="7d195-150">L’agent Linux repose sur certains packages système pour fonctionner correctement :</span><span class="sxs-lookup"><span data-stu-id="7d195-150">The Linux agent depends on some system packages in order to function properly:</span></span>

* <span data-ttu-id="7d195-151">Python 2.6+</span><span class="sxs-lookup"><span data-stu-id="7d195-151">Python 2.6+</span></span>
* <span data-ttu-id="7d195-152">OpenSSL 1.0+</span><span class="sxs-lookup"><span data-stu-id="7d195-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="7d195-153">OpenSSH 5.3+</span><span class="sxs-lookup"><span data-stu-id="7d195-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="7d195-154">Utilitaires de système de fichiers : sfdisk, fdisk, mkfs, séparés</span><span class="sxs-lookup"><span data-stu-id="7d195-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="7d195-155">Outils de mot de passe : chpasswd, sudo</span><span class="sxs-lookup"><span data-stu-id="7d195-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="7d195-156">Outils de traitement de texte : sed, grep</span><span class="sxs-lookup"><span data-stu-id="7d195-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="7d195-157">Outils réseau : ip-route</span><span class="sxs-lookup"><span data-stu-id="7d195-157">Network tools: ip-route</span></span>
* <span data-ttu-id="7d195-158">Prise en charge du noyau pour le montage de systèmes de fichiers UDF.</span><span class="sxs-lookup"><span data-stu-id="7d195-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="7d195-159">Installation</span><span class="sxs-lookup"><span data-stu-id="7d195-159">Installation</span></span>
<span data-ttu-id="7d195-160">L’installation à l’aide d’un package RPM ou DEB à partir de votre référentiel de packages de distribution est la méthode privilégiée pour installer et mettre à niveau l’agent Microsoft Linux Azure.</span><span class="sxs-lookup"><span data-stu-id="7d195-160">Installation using an RPM or a DEB package from your distribution's package repository is the preferred method of installing and upgrading the Azure Linux Agent.</span></span> <span data-ttu-id="7d195-161">Tous les [fournisseurs de distribution approuvés](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) intègrent l’agent Azure Linux dans leurs images et référentiels.</span><span class="sxs-lookup"><span data-stu-id="7d195-161">All the [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate the Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="7d195-162">Consultez la documentation dans le [référentiel de l’agent Linux Azure sur GitHub](https://github.com/Azure/WALinuxAgent) pour connaître les options d’installation avancées, telles que les préfixes et l’installation à partir d’une source ou dans des emplacements personnalisés.</span><span class="sxs-lookup"><span data-stu-id="7d195-162">Refer to the documentation in the [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or to custom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="7d195-163">Options de la ligne de commande</span><span class="sxs-lookup"><span data-stu-id="7d195-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="7d195-164">Indicateurs</span><span class="sxs-lookup"><span data-stu-id="7d195-164">Flags</span></span>
* <span data-ttu-id="7d195-165">verbose : accroît le niveau de détail de la commande spécifiée.</span><span class="sxs-lookup"><span data-stu-id="7d195-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="7d195-166">force : ignore la confirmation interactive de certaines commandes.</span><span class="sxs-lookup"><span data-stu-id="7d195-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="7d195-167">Commandes</span><span class="sxs-lookup"><span data-stu-id="7d195-167">Commands</span></span>
* <span data-ttu-id="7d195-168">help : répertorie les commandes et les indicateurs pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7d195-168">help: Lists the supported commands and flags.</span></span>
* <span data-ttu-id="7d195-169">deprovision : essaie de nettoyer le système et de le préparer pour le réapprovisionnement.</span><span class="sxs-lookup"><span data-stu-id="7d195-169">deprovision: Attempt to clean the system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="7d195-170">Cette opération supprime les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="7d195-170">This operation deleted the following:</span></span>
  
  * <span data-ttu-id="7d195-171">toutes les clés de l'hôte SSH (si Provisioning.RegenerateSshHostKeyPair a la valeur « y » dans le fichier de configuration) ;</span><span class="sxs-lookup"><span data-stu-id="7d195-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in the configuration file)</span></span>
  * <span data-ttu-id="7d195-172">la configuration de Nameserver dans /etc/resolv.conf ;</span><span class="sxs-lookup"><span data-stu-id="7d195-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="7d195-173">le mot de passe racine de /etc/shadow (si Provisioning.DeleteRootPassword a la valeur « y » dans le fichier de configuration) ;</span><span class="sxs-lookup"><span data-stu-id="7d195-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in the configuration file)</span></span>
  * <span data-ttu-id="7d195-174">les baux du client DHCP mis en cache.</span><span class="sxs-lookup"><span data-stu-id="7d195-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="7d195-175">Réinitialise le nom d’hôte sur localhost.localdomain.</span><span class="sxs-lookup"><span data-stu-id="7d195-175">Resets host name to localhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="7d195-176">L’annulation de l’approvisionnement ne garantit pas que l’image est exempte de toute information sensible et qu’elle convient à la redistribution.</span><span class="sxs-lookup"><span data-stu-id="7d195-176">Deprovisioning does not guarantee that the image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="7d195-177">deprovision+user : effectue tout ce qui est décrit sous -deprovision (ci-dessus) et supprime également le dernier compte d’utilisateur approvisionné (obtenu à partir de /var/lib/waagent) et les données associées.</span><span class="sxs-lookup"><span data-stu-id="7d195-177">deprovision+user: Performs everything under -deprovision (above) and also deletes the last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="7d195-178">Ce paramètre est utilisé pour annuler l'approvisionnement d'une image qui a été précédemment approvisionnée sur Azure en vue d'être capturée et réutilisée.</span><span class="sxs-lookup"><span data-stu-id="7d195-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="7d195-179">version : affiche la version de waagent.</span><span class="sxs-lookup"><span data-stu-id="7d195-179">version: Displays the version of waagent</span></span>
* <span data-ttu-id="7d195-180">serialconsole : configure GRUB pour marquer ttyS0 (premier port série) en tant que console de démarrage.</span><span class="sxs-lookup"><span data-stu-id="7d195-180">serialconsole: Configures GRUB to mark ttyS0 (the first serial port) as the boot console.</span></span> <span data-ttu-id="7d195-181">Les journaux de démarrage du noyau sont ainsi envoyés au port série et sont prêts à être débogués.</span><span class="sxs-lookup"><span data-stu-id="7d195-181">This ensures that kernel bootup logs are sent to the serial port and made available for debugging.</span></span>
* <span data-ttu-id="7d195-182">daemon : exécute waagent en tant que démon afin de gérer l’interaction avec la plateforme.</span><span class="sxs-lookup"><span data-stu-id="7d195-182">daemon: Run waagent as a daemon to manage interaction with the platform.</span></span> <span data-ttu-id="7d195-183">Cet argument est spécifié à waagent dans le script waagent init.</span><span class="sxs-lookup"><span data-stu-id="7d195-183">This argument is specified to waagent in the waagent init script.</span></span>
* <span data-ttu-id="7d195-184">start : exécute waagent en arrière-plan</span><span class="sxs-lookup"><span data-stu-id="7d195-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="7d195-185">Configuration</span><span class="sxs-lookup"><span data-stu-id="7d195-185">Configuration</span></span>
<span data-ttu-id="7d195-186">Un fichier de configuration (/etc/waagent.conf) contrôle les actions de waagent.</span><span class="sxs-lookup"><span data-stu-id="7d195-186">A configuration file (/etc/waagent.conf) controls the actions of waagent.</span></span> <span data-ttu-id="7d195-187">Un exemple de fichier de configuration est affiché ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="7d195-187">A sample configuration file is shown below:</span></span>

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

<span data-ttu-id="7d195-188">Les diverses options de configuration sont décrites de manière détaillée ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7d195-188">The various configuration options are described in detail below.</span></span> <span data-ttu-id="7d195-189">Elles sont de trois types : Boolean, String ou Integer.</span><span class="sxs-lookup"><span data-stu-id="7d195-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="7d195-190">Les options de configuration Boolean peuvent être spécifiées à l'aide de « y » (oui) ou « n » (non).</span><span class="sxs-lookup"><span data-stu-id="7d195-190">The Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="7d195-191">Le mot clé « None » (Aucun) peut être utilisé dans le cas de certaines entrées de type chaîne comme décrit ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7d195-191">The special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="7d195-192">**Provisioning.Enabled :**</span><span class="sxs-lookup"><span data-stu-id="7d195-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="7d195-193">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="7d195-193">Type: Boolean</span></span>  
<span data-ttu-id="7d195-194">Par défaut : y</span><span class="sxs-lookup"><span data-stu-id="7d195-194">Default: y</span></span>

<span data-ttu-id="7d195-195">L'utilisateur peut activer ou désactiver la fonctionnalité d'approvisionnement dans l'agent.</span><span class="sxs-lookup"><span data-stu-id="7d195-195">This allows the user to enable or disable the provisioning functionality in the agent.</span></span> <span data-ttu-id="7d195-196">Les valeurs valides sont « y » ou « n ».</span><span class="sxs-lookup"><span data-stu-id="7d195-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="7d195-197">Si l'approvisionnement est désactivé, les clés d'utilisateur et d'hôte SSH dans l'image sont conservées et toute configuration spécifiée dans l'API d'approvisionnement Azure est ignorée.</span><span class="sxs-lookup"><span data-stu-id="7d195-197">If provisioning is disabled, SSH host and user keys in the image are preserved and any configuration specified in the Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="7d195-198">La valeur par défaut du paramètre `Provisioning.Enabled` est « n » dans les images cloud Ubuntu qui utilisent cloud-init pour l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="7d195-198">The `Provisioning.Enabled` parameter defaults to "n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="7d195-199">**Provisioning.DeleteRootPassword :**</span><span class="sxs-lookup"><span data-stu-id="7d195-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="7d195-200">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="7d195-200">Type: Boolean</span></span>  
<span data-ttu-id="7d195-201">Par défaut : n</span><span class="sxs-lookup"><span data-stu-id="7d195-201">Default: n</span></span>

<span data-ttu-id="7d195-202">Si elle est définie, le mot de passe racine dans le fichier /etc/shadow est effacé au cours du processus d'approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="7d195-202">If set, the root password in the /etc/shadow file is erased during the provisioning process.</span></span>

<span data-ttu-id="7d195-203">**Provisioning.RegenerateSshHostKeyPair :**</span><span class="sxs-lookup"><span data-stu-id="7d195-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="7d195-204">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="7d195-204">Type: Boolean</span></span>  
<span data-ttu-id="7d195-205">Par défaut : y</span><span class="sxs-lookup"><span data-stu-id="7d195-205">Default: y</span></span>

<span data-ttu-id="7d195-206">Si elle est définie, toutes les paires de clés d'hôte SSH (ecdsa, dsa et rsa) sont supprimées de /etc/ssh/ au cours du processus d'approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="7d195-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during the provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="7d195-207">Une nouvelle paire de clés unique est générée.</span><span class="sxs-lookup"><span data-stu-id="7d195-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="7d195-208">L'entrée Provisioning.SshHostKeyPairType peut configurer le type de chiffrement pour la nouvelle paire de clés.</span><span class="sxs-lookup"><span data-stu-id="7d195-208">The encryption type for the fresh key pair is configurable by the Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="7d195-209">Veuillez noter que certaines distributions créent à nouveau les paires de clés SSH pour tout type de chiffrement manquant au redémarrage du démon SSH.</span><span class="sxs-lookup"><span data-stu-id="7d195-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when the SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="7d195-210">**Provisioning.SshHostKeyPairType :**</span><span class="sxs-lookup"><span data-stu-id="7d195-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="7d195-211">Type : string</span><span class="sxs-lookup"><span data-stu-id="7d195-211">Type: String</span></span>  
<span data-ttu-id="7d195-212">Par défaut : rsa</span><span class="sxs-lookup"><span data-stu-id="7d195-212">Default: rsa</span></span>

<span data-ttu-id="7d195-213">Un type d'algorithme de chiffrement qui est pris en charge par le démon SSH sur la machine virtuelle peut être défini.</span><span class="sxs-lookup"><span data-stu-id="7d195-213">This can be set to an encryption algorithm type that is supported by the SSH daemon on the virtual machine.</span></span> <span data-ttu-id="7d195-214">Les valeurs généralement prises en charge sont « rsa », « dsa » et « ecdsa ».</span><span class="sxs-lookup"><span data-stu-id="7d195-214">The typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="7d195-215">Notez que « putty.exe » sur Windows ne prend pas en charge « ecdsa ».</span><span class="sxs-lookup"><span data-stu-id="7d195-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="7d195-216">Si vous envisagez d'utiliser putty.exe sur Windows pour établir une connexion sur un déploiement Linux, veuillez utiliser « rsa » ou « dsa ».</span><span class="sxs-lookup"><span data-stu-id="7d195-216">So, if you intend to use putty.exe on Windows to connect to a Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="7d195-217">**Provisioning.MonitorHostName :**</span><span class="sxs-lookup"><span data-stu-id="7d195-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="7d195-218">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="7d195-218">Type: Boolean</span></span>  
<span data-ttu-id="7d195-219">Par défaut : y</span><span class="sxs-lookup"><span data-stu-id="7d195-219">Default: y</span></span>

<span data-ttu-id="7d195-220">Si elle est définie, waagent surveille la machine virtuelle Linux en vue de détecter des modifications de nom d'hôte (comme renvoyé par la commande « hostname ») et met automatiquement à jour la configuration de mise en réseau dans l'image afin de refléter la modification.</span><span class="sxs-lookup"><span data-stu-id="7d195-220">If set, waagent will monitor the Linux virtual machine for hostname changes (as returned by the "hostname" command) and automatically update the networking configuration in the image to reflect the change.</span></span> <span data-ttu-id="7d195-221">Afin de transmettre la modification de nom aux serveurs DNS, la mise en réseau est redémarrée sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7d195-221">In order to push the name change to the DNS servers, networking will be restarted in the virtual machine.</span></span> <span data-ttu-id="7d195-222">La connexion Internet est alors brièvement interrompue.</span><span class="sxs-lookup"><span data-stu-id="7d195-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="7d195-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="7d195-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="7d195-224">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="7d195-224">Type: Boolean</span></span>  
<span data-ttu-id="7d195-225">Par défaut : n</span><span class="sxs-lookup"><span data-stu-id="7d195-225">Default: n</span></span>

<span data-ttu-id="7d195-226">Si ce paramètre est défini, waagent décodera CustomData en Base64.</span><span class="sxs-lookup"><span data-stu-id="7d195-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="7d195-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="7d195-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="7d195-228">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="7d195-228">Type: Boolean</span></span>  
<span data-ttu-id="7d195-229">Par défaut : n</span><span class="sxs-lookup"><span data-stu-id="7d195-229">Default: n</span></span>

<span data-ttu-id="7d195-230">Si ce paramètre est défini, waagent exécute CustomData après l’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="7d195-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="7d195-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="7d195-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="7d195-232">Type : chaîne</span><span class="sxs-lookup"><span data-stu-id="7d195-232">Type:String</span></span>  
<span data-ttu-id="7d195-233">Par défaut : 6</span><span class="sxs-lookup"><span data-stu-id="7d195-233">Default:6</span></span>

<span data-ttu-id="7d195-234">Algorithme utilisé par crypt lors de la génération du hachage de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7d195-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="7d195-235">1 - MD5</span><span class="sxs-lookup"><span data-stu-id="7d195-235">1 - MD5</span></span>  
 <span data-ttu-id="7d195-236">2 a - Blowfish</span><span class="sxs-lookup"><span data-stu-id="7d195-236">2a - Blowfish</span></span>  
 <span data-ttu-id="7d195-237">5 - SHA-256</span><span class="sxs-lookup"><span data-stu-id="7d195-237">5 - SHA-256</span></span>  
 <span data-ttu-id="7d195-238">6 - SHA-512</span><span class="sxs-lookup"><span data-stu-id="7d195-238">6 - SHA-512</span></span>  

<span data-ttu-id="7d195-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="7d195-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="7d195-240">Type : chaîne</span><span class="sxs-lookup"><span data-stu-id="7d195-240">Type:String</span></span>  
<span data-ttu-id="7d195-241">Par défaut : 10</span><span class="sxs-lookup"><span data-stu-id="7d195-241">Default:10</span></span>

<span data-ttu-id="7d195-242">Longueur de la chaîne salt aléatoire utilisée lors de la génération du hachage de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7d195-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="7d195-243">**ResourceDisk.Format :**</span><span class="sxs-lookup"><span data-stu-id="7d195-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="7d195-244">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="7d195-244">Type: Boolean</span></span>  
<span data-ttu-id="7d195-245">Par défaut : y</span><span class="sxs-lookup"><span data-stu-id="7d195-245">Default: y</span></span>

<span data-ttu-id="7d195-246">Si elle est définie, le disque de ressources fourni par la plateforme est formaté et monté par waagent si le type de système de fichiers demandé par l'utilisateur dans « ResourceDisk.Filesystem » est différent de « ntfs ».</span><span class="sxs-lookup"><span data-stu-id="7d195-246">If set, the resource disk provided by the platform will be formatted and mounted by waagent if the filesystem type requested by the user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="7d195-247">Une partition unique de type Linux (83) est mise à la disposition sur le disque.</span><span class="sxs-lookup"><span data-stu-id="7d195-247">A single partition of type Linux (83) will be made available on the disk.</span></span> <span data-ttu-id="7d195-248">Notez que cette partition n'est pas formatée si elle ne peut pas être correctement montée.</span><span class="sxs-lookup"><span data-stu-id="7d195-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="7d195-249">**ResourceDisk.Filesystem :**</span><span class="sxs-lookup"><span data-stu-id="7d195-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="7d195-250">Type : string</span><span class="sxs-lookup"><span data-stu-id="7d195-250">Type: String</span></span>  
<span data-ttu-id="7d195-251">Par défaut : ext4</span><span class="sxs-lookup"><span data-stu-id="7d195-251">Default: ext4</span></span>

<span data-ttu-id="7d195-252">Cette commande spécifie le type de système de fichiers pour le disque de ressources.</span><span class="sxs-lookup"><span data-stu-id="7d195-252">This specifies the filesystem type for the resource disk.</span></span> <span data-ttu-id="7d195-253">Les valeurs prises en charge diffèrent selon la distribution Linux.</span><span class="sxs-lookup"><span data-stu-id="7d195-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="7d195-254">Si la chaîne est X, mkfs.X doit être présent sur l'image Linux.</span><span class="sxs-lookup"><span data-stu-id="7d195-254">If the string is X, then mkfs.X should be present on the Linux image.</span></span> <span data-ttu-id="7d195-255">Les images SLES 11 doivent généralement utiliser « ext3 ».</span><span class="sxs-lookup"><span data-stu-id="7d195-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="7d195-256">Les images FreeBSD doivent utiliser « ufs2 » ici.</span><span class="sxs-lookup"><span data-stu-id="7d195-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="7d195-257">**ResourceDisk.MountPoint :**</span><span class="sxs-lookup"><span data-stu-id="7d195-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="7d195-258">Type : string</span><span class="sxs-lookup"><span data-stu-id="7d195-258">Type: String</span></span>  
<span data-ttu-id="7d195-259">Par défaut : /mnt/resource</span><span class="sxs-lookup"><span data-stu-id="7d195-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="7d195-260">Cette commande spécifie le chemin où le disque de ressources est monté.</span><span class="sxs-lookup"><span data-stu-id="7d195-260">This specifies the path at which the resource disk is mounted.</span></span> <span data-ttu-id="7d195-261">Notez que le disque de ressources est un disque *temporaire* et qu'il peut être vidé lors de l'annulation de l'approvisionnement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="7d195-261">Note that the resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span>

<span data-ttu-id="7d195-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="7d195-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="7d195-263">Type : string</span><span class="sxs-lookup"><span data-stu-id="7d195-263">Type: String</span></span>  
<span data-ttu-id="7d195-264">Par défaut : aucun</span><span class="sxs-lookup"><span data-stu-id="7d195-264">Default: None</span></span>

<span data-ttu-id="7d195-265">Spécifie les options de montage de disque à transmettre à la commande mount -o.</span><span class="sxs-lookup"><span data-stu-id="7d195-265">Specifies disk mount options to be passed to the mount -o command.</span></span> <span data-ttu-id="7d195-266">Les valeurs de cette liste sont séparées par des virgules, par exemple</span><span class="sxs-lookup"><span data-stu-id="7d195-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="7d195-267">'nodev,nosuid'.</span><span class="sxs-lookup"><span data-stu-id="7d195-267">'nodev,nosuid'.</span></span> <span data-ttu-id="7d195-268">Pour plus d’informations, consultez mount(8).</span><span class="sxs-lookup"><span data-stu-id="7d195-268">See mount(8) for details.</span></span>

<span data-ttu-id="7d195-269">**ResourceDisk.EnableSwap :**</span><span class="sxs-lookup"><span data-stu-id="7d195-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="7d195-270">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="7d195-270">Type: Boolean</span></span>  
<span data-ttu-id="7d195-271">Par défaut : n</span><span class="sxs-lookup"><span data-stu-id="7d195-271">Default: n</span></span>

<span data-ttu-id="7d195-272">Si elle est définie, un fichier d'échange (/swapfile) est créé sur le disque de ressources et est ajouté à l'espace d'échange système.</span><span class="sxs-lookup"><span data-stu-id="7d195-272">If set, a swap file (/swapfile) is created on the resource disk and added to the system swap space.</span></span>

<span data-ttu-id="7d195-273">**ResourceDisk.SwapSizeMB :**</span><span class="sxs-lookup"><span data-stu-id="7d195-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="7d195-274">Type : entier</span><span class="sxs-lookup"><span data-stu-id="7d195-274">Type: Integer</span></span>  
<span data-ttu-id="7d195-275">Par défaut : 0</span><span class="sxs-lookup"><span data-stu-id="7d195-275">Default: 0</span></span>

<span data-ttu-id="7d195-276">Taille du fichier d'échange en mégaoctets.</span><span class="sxs-lookup"><span data-stu-id="7d195-276">The size of the swap file in megabytes.</span></span>

<span data-ttu-id="7d195-277">**Logs.Verbose :**</span><span class="sxs-lookup"><span data-stu-id="7d195-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="7d195-278">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="7d195-278">Type: Boolean</span></span>  
<span data-ttu-id="7d195-279">Par défaut : n</span><span class="sxs-lookup"><span data-stu-id="7d195-279">Default: n</span></span>

<span data-ttu-id="7d195-280">Si elle est définie, le niveau de détail du journal est optimisé.</span><span class="sxs-lookup"><span data-stu-id="7d195-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="7d195-281">Waagent enregistre dans /var/log/waagent.log et exploite la fonctionnalité logrotate du système pour faire tourner les journaux.</span><span class="sxs-lookup"><span data-stu-id="7d195-281">Waagent logs to /var/log/waagent.log and leverages the system logrotate functionality to rotate logs.</span></span>

<span data-ttu-id="7d195-282">**OS.EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="7d195-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="7d195-283">Type : booléen</span><span class="sxs-lookup"><span data-stu-id="7d195-283">Type: Boolean</span></span>  
<span data-ttu-id="7d195-284">Par défaut : n</span><span class="sxs-lookup"><span data-stu-id="7d195-284">Default: n</span></span>

<span data-ttu-id="7d195-285">Si ce paramètre est défini, l’agent tente de s’installer, puis charge un pilote de noyau RDMA qui correspond à la version du microprogramme sur le matériel sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="7d195-285">If set, the agent will attempt to install and then load an RDMA kernel driver that matches the version of the firmware on the underlying hardware.</span></span>

<span data-ttu-id="7d195-286">**OS.RootDeviceScsiTimeout :**</span><span class="sxs-lookup"><span data-stu-id="7d195-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="7d195-287">Type : entier</span><span class="sxs-lookup"><span data-stu-id="7d195-287">Type: Integer</span></span>  
<span data-ttu-id="7d195-288">Par défaut : 300</span><span class="sxs-lookup"><span data-stu-id="7d195-288">Default: 300</span></span>

<span data-ttu-id="7d195-289">Le délai d'expiration SCSI est configuré en secondes sur le disque du système d'exploitation et les lecteurs de données.</span><span class="sxs-lookup"><span data-stu-id="7d195-289">This configures the SCSI timeout in seconds on the OS disk and data drives.</span></span> <span data-ttu-id="7d195-290">Si elle n'est pas définie, les valeurs par défaut du système sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="7d195-290">If not set, the system defaults are used.</span></span>

<span data-ttu-id="7d195-291">**OS.OpensslPath :**</span><span class="sxs-lookup"><span data-stu-id="7d195-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="7d195-292">Type : string</span><span class="sxs-lookup"><span data-stu-id="7d195-292">Type: String</span></span>  
<span data-ttu-id="7d195-293">Par défaut : aucun</span><span class="sxs-lookup"><span data-stu-id="7d195-293">Default: None</span></span>

<span data-ttu-id="7d195-294">Cette commande sert à spécifier un autre chemin pour les données binaires openssl à utiliser pour les opérations de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="7d195-294">This can be used to specify an alternate path for the openssl binary to use for cryptographic operations.</span></span>

<span data-ttu-id="7d195-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="7d195-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="7d195-296">Type : string</span><span class="sxs-lookup"><span data-stu-id="7d195-296">Type: String</span></span>  
<span data-ttu-id="7d195-297">Par défaut : aucun</span><span class="sxs-lookup"><span data-stu-id="7d195-297">Default: None</span></span>

<span data-ttu-id="7d195-298">Si ce paramètre est défini, l’agent utilisera ce serveur proxy pour accéder à internet.</span><span class="sxs-lookup"><span data-stu-id="7d195-298">If set, the agent will use this proxy server to access the internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="7d195-299">Images cloud Ubuntu</span><span class="sxs-lookup"><span data-stu-id="7d195-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="7d195-300">Notez que les images cloud Ubuntu utilisent [Cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) pour exécuter les tâches de configuration qui pourraient être gérées par l’agent Linux Azure.</span><span class="sxs-lookup"><span data-stu-id="7d195-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) to perform many configuration tasks that would otherwise be managed by the Azure Linux Agent.</span></span>  <span data-ttu-id="7d195-301">Notez les différences suivantes :</span><span class="sxs-lookup"><span data-stu-id="7d195-301">Please note the following differences:</span></span>

* <span data-ttu-id="7d195-302">**Provisioning.Enabled** est défini par défaut sur n sur les images cloud Ubuntu utilisant Cloud-init pour exécuter les tâches d’approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="7d195-302">**Provisioning.Enabled** defaults to "n" on Ubuntu Cloud Images that use cloud-init to perform provisioning tasks.</span></span>
* <span data-ttu-id="7d195-303">Les paramètres de configuration suivants n’ont aucun effet sur les images cloud Ubuntu utilisant Cloud-init pour gérer le disque de ressources et l’espace d’échange :</span><span class="sxs-lookup"><span data-stu-id="7d195-303">The following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init to manage the resource disk and swap space:</span></span>
  
  * <span data-ttu-id="7d195-304">**ResourceDisk.Format**</span><span class="sxs-lookup"><span data-stu-id="7d195-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="7d195-305">**ResourceDisk.Filesystem**</span><span class="sxs-lookup"><span data-stu-id="7d195-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="7d195-306">**ResourceDisk.MountPoint**</span><span class="sxs-lookup"><span data-stu-id="7d195-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="7d195-307">**ResourceDisk.EnableSwap**</span><span class="sxs-lookup"><span data-stu-id="7d195-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="7d195-308">**ResourceDisk.SwapSizeMB**</span><span class="sxs-lookup"><span data-stu-id="7d195-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="7d195-309">Consultez les ressources suivantes pour configurer le point de montage du disque de ressources et l’espace d’échange sur les images cloud Ubuntu durant l’approvisionnement :</span><span class="sxs-lookup"><span data-stu-id="7d195-309">Please see the following resources to configure the resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="7d195-310">Wiki Ubuntu : Configurer les partitions d’échange</span><span class="sxs-lookup"><span data-stu-id="7d195-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="7d195-311">Injection de données personnalisées dans une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="7d195-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

