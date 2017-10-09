---
title: aaaConfiguring DHCPv6 pour les machines virtuelles Linux | Documents Microsoft
description: Comment tooconfigure DHCPv6 pour les machines virtuelles Linux.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "IPv6, équilibreur de charge azure, double pile, adresse ip publique, ipv6 natif, mobile, iot"
ms.assetid: b32719b6-00e8-4cd0-ba7f-e60e8146084b
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: abd5a98c3496b189946f59bab1d9c20dcd0aa2c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="6d912-104">Configuration de DHCPv6 pour les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="6d912-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="6d912-105">Certaines des images de machine virtuelle Linux hello Bonjour Azure Marketplace inutile DHCPv6 configuré par défaut.</span><span class="sxs-lookup"><span data-stu-id="6d912-105">Some of hello Linux virtual machine images in hello Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="6d912-106">toosupport IPv6, DHCPv6 doit être configuré au sein de la distribution du système d’exploitation Linux hello que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="6d912-106">toosupport IPv6, DHCPv6 must be configured in within hello Linux OS distribution that you are using.</span></span> <span data-ttu-id="6d912-107">Différentes distributions Linux présentent des méthodes de configuration de DHCPv6 distinctes, car elles utilisent des packages non identiques.</span><span class="sxs-lookup"><span data-stu-id="6d912-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="6d912-108">Les images SUSE Linux et CoreOS récentes Bonjour Azure Marketplace ont été préconfigurées avec DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="6d912-108">Recent SUSE Linux and CoreOS images in hello Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="6d912-109">Aucune modification supplémentaire n’est requise pour l’utilisation de ces images.</span><span class="sxs-lookup"><span data-stu-id="6d912-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="6d912-110">Ce document décrit comment tooenable DHCPv6 afin que votre machine virtuelle de Linux obtienne une adresse IPv6.</span><span class="sxs-lookup"><span data-stu-id="6d912-110">This document describes how tooenable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="6d912-111">Modification incorrecte des fichiers de configuration de réseau risque de vous toolose réseau accès tooyour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6d912-111">Improperly editing network configuration files can cause you toolose network access tooyour VM.</span></span> <span data-ttu-id="6d912-112">Nous vous recommandons de tester vos modifications de configuration sur des systèmes hors production.</span><span class="sxs-lookup"><span data-stu-id="6d912-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="6d912-113">instructions Hello dans cet article ont été testées sur hello dernières versions des images de Linux hello Bonjour Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="6d912-113">hello instructions in this article have been tested on hello latest versions of hello Linux images in hello Azure Marketplace.</span></span> <span data-ttu-id="6d912-114">Consultez la documentation de hello spécifique à votre version de Linux pour obtenir des instructions plus détaillées.</span><span class="sxs-lookup"><span data-stu-id="6d912-114">Consult hello documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="6d912-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="6d912-115">Ubuntu</span></span>

1. <span data-ttu-id="6d912-116">Modifier le fichier de hello `/etc/dhcp/dhclient6.conf` et ajoutez hello ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="6d912-116">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="6d912-117">Modifier la configuration de réseau de hello pour l’interface d’eth0 hello avec hello configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="6d912-117">Edit hello network configuration for hello eth0 interface with hello following configuration:</span></span>

   * <span data-ttu-id="6d912-118">Sur **Ubuntu 12.04 et 14.04**, modifiez le fichier de hello`/etc/network/interfaces.d/eth0.cfg`</span><span class="sxs-lookup"><span data-stu-id="6d912-118">On **Ubuntu 12.04 and 14.04**, edit hello file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="6d912-119">Sur **Ubuntu 16.04**, modifiez le fichier de hello`/etc/network/interfaces.d/50-cloud-init.cfg`</span><span class="sxs-lookup"><span data-stu-id="6d912-119">On **Ubuntu 16.04**, edit hello file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="6d912-120">Renouvelez l’adresse IPv6 :</span><span class="sxs-lookup"><span data-stu-id="6d912-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="6d912-121">Debian</span><span class="sxs-lookup"><span data-stu-id="6d912-121">Debian</span></span>

1. <span data-ttu-id="6d912-122">Modifier le fichier de hello `/etc/dhcp/dhclient6.conf` et ajoutez hello ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="6d912-122">Edit hello file `/etc/dhcp/dhclient6.conf` and add hello following line:</span></span>

        timeout 10;

2. <span data-ttu-id="6d912-123">Modifier le fichier de hello `/etc/network/interfaces` et ajoutez hello configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="6d912-123">Edit hello file `/etc/network/interfaces` and add hello following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="6d912-124">Renouvelez l’adresse IPv6 :</span><span class="sxs-lookup"><span data-stu-id="6d912-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="6d912-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="6d912-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="6d912-126">Modifier le fichier de hello `/etc/sysconfig/network` et ajoutez hello suivant paramètre :</span><span class="sxs-lookup"><span data-stu-id="6d912-126">Edit hello file `/etc/sysconfig/network` and add hello following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="6d912-127">Modifier le fichier de hello `/etc/sysconfig/network-scripts/ifcfg-eth0` et ajoutez hello deux paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="6d912-127">Edit hello file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add hello following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="6d912-128">Renouvelez l’adresse IPv6 :</span><span class="sxs-lookup"><span data-stu-id="6d912-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="6d912-129">SLES 11 et openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="6d912-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="6d912-130">Les images SLES et openSUSE récentes d’Azure ont été préconfigurées avec DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="6d912-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="6d912-131">Aucune modification supplémentaire n’est requise pour l’utilisation de ces images.</span><span class="sxs-lookup"><span data-stu-id="6d912-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="6d912-132">Si vous avez une machine virtuelle basée sur une image SUSE antérieure ou personnalisée, utilisez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6d912-132">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="6d912-133">Installer hello `dhcp-client` du package, si nécessaire :</span><span class="sxs-lookup"><span data-stu-id="6d912-133">Install hello `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="6d912-134">Modifier le fichier de hello `/etc/sysconfig/network/ifcfg-eth0` et ajoutez hello suivant paramètre :</span><span class="sxs-lookup"><span data-stu-id="6d912-134">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and add hello following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="6d912-135">Renouveler l’adresse de hello IPv6 :</span><span class="sxs-lookup"><span data-stu-id="6d912-135">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="6d912-136">SLES 12 et openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="6d912-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="6d912-137">Les images SLES et openSUSE récentes d’Azure ont été préconfigurées avec DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="6d912-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="6d912-138">Aucune modification supplémentaire n’est requise pour l’utilisation de ces images.</span><span class="sxs-lookup"><span data-stu-id="6d912-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="6d912-139">Si vous avez une machine virtuelle basée sur une image SUSE antérieure ou personnalisée, utilisez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6d912-139">If you have a VM based on an older or custom SUSE image, use hello following steps:</span></span>

1. <span data-ttu-id="6d912-140">Modifier le fichier de hello `/etc/sysconfig/network/ifcfg-eth0` et remplacer ce paramètre</span><span class="sxs-lookup"><span data-stu-id="6d912-140">Edit hello file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="6d912-141">avec hello valeur suivante :</span><span class="sxs-lookup"><span data-stu-id="6d912-141">with hello following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="6d912-142">Ajouter hello suit le paramètre trop`/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="6d912-142">Add hello following parameter too`/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="6d912-143">Renouveler l’adresse de hello IPv6 :</span><span class="sxs-lookup"><span data-stu-id="6d912-143">Renew hello IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="6d912-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="6d912-144">CoreOS</span></span>

<span data-ttu-id="6d912-145">Les images CoreOS récentes d’Azure ont été préconfigurées avec DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="6d912-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="6d912-146">Aucune modification supplémentaire n’est requise pour l’utilisation de ces images.</span><span class="sxs-lookup"><span data-stu-id="6d912-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="6d912-147">Si vous avez une machine virtuelle basée sur une image CoreOS antérieure ou personnalisée, utilisez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6d912-147">If you have a VM based on an older or custom CoreOS image, use hello following steps:</span></span>

1. <span data-ttu-id="6d912-148">Modifier le fichier de hello`/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="6d912-148">Edit hello file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="6d912-149">Renouveler l’adresse de hello IPv6 :</span><span class="sxs-lookup"><span data-stu-id="6d912-149">Renew hello IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
