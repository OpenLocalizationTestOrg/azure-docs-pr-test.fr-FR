---
title: Configuration de DHCPv6 pour les machines virtuelles Linux | Microsoft Docs
description: Configurer DHCPv6 pour la machines virtuelles Linux
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
ms.openlocfilehash: 5c591e7f1838c86ca74caea9dd3a5e8f874fd8a7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-dhcpv6-for-linux-vms"></a><span data-ttu-id="4f2f7-104">Configuration de DHCPv6 pour les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="4f2f7-104">Configuring DHCPv6 for Linux VMs</span></span>

<span data-ttu-id="4f2f7-105">Certaines des images de machines virtuelles Linux de la Place de marché Microsoft Azure ne présentent pas de configuration DHCPv6 par défaut.</span><span class="sxs-lookup"><span data-stu-id="4f2f7-105">Some of the Linux virtual machine images in the Azure Marketplace do not have DHCPv6 configured by default.</span></span> <span data-ttu-id="4f2f7-106">Pour prendre en charge IPv6, DHCPv6 doit être configuré dans la distribution du système d’exploitation Linux que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="4f2f7-106">To support IPv6, DHCPv6 must be configured in within the Linux OS distribution that you are using.</span></span> <span data-ttu-id="4f2f7-107">Différentes distributions Linux présentent des méthodes de configuration de DHCPv6 distinctes, car elles utilisent des packages non identiques.</span><span class="sxs-lookup"><span data-stu-id="4f2f7-107">Different Linux distributions have different ways of configuring DHCPv6 because they use different packages.</span></span>

> [!NOTE]
> <span data-ttu-id="4f2f7-108">Les images SUSE Linux et CoreOS récentes de la Place de marché Azure ont été préconfigurées avec DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="4f2f7-108">Recent SUSE Linux and CoreOS images in the Azure Marketplace have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="4f2f7-109">Aucune modification supplémentaire n’est requise pour l’utilisation de ces images.</span><span class="sxs-lookup"><span data-stu-id="4f2f7-109">No additional changes are required when using those images.</span></span>

<span data-ttu-id="4f2f7-110">Ce document vous explique comment activer DHCPv6 pour que votre machine virtuelle Linux obtienne une adresse IPv6.</span><span class="sxs-lookup"><span data-stu-id="4f2f7-110">This document describes how to enable DHCPv6 so that your Linux virtual machine obtains an IPv6 address.</span></span>

> [!WARNING]
> <span data-ttu-id="4f2f7-111">Une modification incorrecte des fichiers de configuration réseau peuvent vous faire perdre l’accès du réseau à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4f2f7-111">Improperly editing network configuration files can cause you to lose network access to your VM.</span></span> <span data-ttu-id="4f2f7-112">Nous vous recommandons de tester vos modifications de configuration sur des systèmes hors production.</span><span class="sxs-lookup"><span data-stu-id="4f2f7-112">We recommended that you test your configuration changes on non-production systems.</span></span> <span data-ttu-id="4f2f7-113">Les instructions de cet article ont été testées sur les dernières versions des images Linux dans la Place de marché Azure.</span><span class="sxs-lookup"><span data-stu-id="4f2f7-113">The instructions in this article have been tested on the latest versions of the Linux images in the Azure Marketplace.</span></span> <span data-ttu-id="4f2f7-114">Consultez la documentation de votre version spécifique de Linux pour obtenir des instructions plus détaillées.</span><span class="sxs-lookup"><span data-stu-id="4f2f7-114">Consult the documentation for your specific version of Linux for more detailed instructions.</span></span>

## <a name="ubuntu"></a><span data-ttu-id="4f2f7-115">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4f2f7-115">Ubuntu</span></span>

1. <span data-ttu-id="4f2f7-116">Modifiez le fichier `/etc/dhcp/dhclient6.conf` , puis ajoutez la ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="4f2f7-116">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="4f2f7-117">Modifiez la configuration du réseau pour l’interface eth0, selon la méthode suivante :</span><span class="sxs-lookup"><span data-stu-id="4f2f7-117">Edit the network configuration for the eth0 interface with the following configuration:</span></span>

   * <span data-ttu-id="4f2f7-118">Sur **Ubuntu 12.04 et 14.04**, modifiez le fichier `/etc/network/interfaces.d/eth0.cfg`.</span><span class="sxs-lookup"><span data-stu-id="4f2f7-118">On **Ubuntu 12.04 and 14.04**, edit the file `/etc/network/interfaces.d/eth0.cfg`</span></span>
   * <span data-ttu-id="4f2f7-119">Sur **Ubuntu 16.04**, modifiez le fichier `/etc/network/interfaces.d/50-cloud-init.cfg`.</span><span class="sxs-lookup"><span data-stu-id="4f2f7-119">On **Ubuntu 16.04**, edit the file `/etc/network/interfaces.d/50-cloud-init.cfg`</span></span>

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="4f2f7-120">Renouvelez l’adresse IPv6 :</span><span class="sxs-lookup"><span data-stu-id="4f2f7-120">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a><span data-ttu-id="4f2f7-121">Debian</span><span class="sxs-lookup"><span data-stu-id="4f2f7-121">Debian</span></span>

1. <span data-ttu-id="4f2f7-122">Modifiez le fichier `/etc/dhcp/dhclient6.conf` , puis ajoutez la ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="4f2f7-122">Edit the file `/etc/dhcp/dhclient6.conf` and add the following line:</span></span>

        timeout 10;

2. <span data-ttu-id="4f2f7-123">Modifiez le fichier `/etc/network/interfaces` , puis ajoutez la configuration suivante :</span><span class="sxs-lookup"><span data-stu-id="4f2f7-123">Edit the file `/etc/network/interfaces` and add the following configuration:</span></span>

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. <span data-ttu-id="4f2f7-124">Renouvelez l’adresse IPv6 :</span><span class="sxs-lookup"><span data-stu-id="4f2f7-124">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a><span data-ttu-id="4f2f7-125">RHEL / CentOS / Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="4f2f7-125">RHEL / CentOS / Oracle Linux</span></span>

1. <span data-ttu-id="4f2f7-126">Modifiez le fichier `/etc/sysconfig/network` , puis ajoutez le paramètre suivant :</span><span class="sxs-lookup"><span data-stu-id="4f2f7-126">Edit the file `/etc/sysconfig/network` and add the following parameter:</span></span>

        NETWORKING_IPV6=yes

2. <span data-ttu-id="4f2f7-127">Modifiez le fichier `/etc/sysconfig/network-scripts/ifcfg-eth0` , puis ajoutez les deux paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="4f2f7-127">Edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following two parameters:</span></span>

        IPV6INIT=yes
        DHCPV6C=yes

3. <span data-ttu-id="4f2f7-128">Renouvelez l’adresse IPv6 :</span><span class="sxs-lookup"><span data-stu-id="4f2f7-128">Renew IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a><span data-ttu-id="4f2f7-129">SLES 11 et openSUSE 13</span><span class="sxs-lookup"><span data-stu-id="4f2f7-129">SLES 11 & openSUSE 13</span></span>

<span data-ttu-id="4f2f7-130">Les images SLES et openSUSE récentes d’Azure ont été préconfigurées avec DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="4f2f7-130">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="4f2f7-131">Aucune modification supplémentaire n’est requise pour l’utilisation de ces images.</span><span class="sxs-lookup"><span data-stu-id="4f2f7-131">No additional changes are required when using those images.</span></span> <span data-ttu-id="4f2f7-132">Si vous possédez une machine virtuelle basée sur une image SUSE plus ancienne ou personnalisée, appliquez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4f2f7-132">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="4f2f7-133">Installez le package `dhcp-client` , si nécessaire :</span><span class="sxs-lookup"><span data-stu-id="4f2f7-133">Install the `dhcp-client` package, if needed:</span></span>

    ```bash
    sudo zypper install dhcp-client
    ```

2. <span data-ttu-id="4f2f7-134">Modifiez le fichier `/etc/sysconfig/network/ifcfg-eth0` , puis ajoutez le paramètre suivant :</span><span class="sxs-lookup"><span data-stu-id="4f2f7-134">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and add the following parameter:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="4f2f7-135">Renouvelez l’adresse IPv6 :</span><span class="sxs-lookup"><span data-stu-id="4f2f7-135">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a><span data-ttu-id="4f2f7-136">SLES 12 et openSUSE Leap</span><span class="sxs-lookup"><span data-stu-id="4f2f7-136">SLES 12 and openSUSE Leap</span></span>

<span data-ttu-id="4f2f7-137">Les images SLES et openSUSE récentes d’Azure ont été préconfigurées avec DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="4f2f7-137">Recent SLES and openSUSE images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="4f2f7-138">Aucune modification supplémentaire n’est requise pour l’utilisation de ces images.</span><span class="sxs-lookup"><span data-stu-id="4f2f7-138">No additional changes are required when using those images.</span></span> <span data-ttu-id="4f2f7-139">Si vous possédez une machine virtuelle basée sur une image SUSE plus ancienne ou personnalisée, appliquez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4f2f7-139">If you have a VM based on an older or custom SUSE image, use the following steps:</span></span>

1. <span data-ttu-id="4f2f7-140">Modifiez le fichier `/etc/sysconfig/network/ifcfg-eth0` , puis remplacez ce paramètre</span><span class="sxs-lookup"><span data-stu-id="4f2f7-140">Edit the file `/etc/sysconfig/network/ifcfg-eth0` and replace this parameter</span></span>

        #BOOTPROTO='dhcp4'

    <span data-ttu-id="4f2f7-141">avec la valeur suivante :</span><span class="sxs-lookup"><span data-stu-id="4f2f7-141">with the following value:</span></span>

        BOOTPROTO='dhcp'

2. <span data-ttu-id="4f2f7-142">Ajoutez le paramètre suivant à `/etc/sysconfig/network/ifcfg-eth0`:</span><span class="sxs-lookup"><span data-stu-id="4f2f7-142">Add the following parameter to `/etc/sysconfig/network/ifcfg-eth0`:</span></span>

        DHCLIENT6_MODE='managed'

3. <span data-ttu-id="4f2f7-143">Renouvelez l’adresse IPv6 :</span><span class="sxs-lookup"><span data-stu-id="4f2f7-143">Renew the IPv6 address:</span></span>

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a><span data-ttu-id="4f2f7-144">CoreOS</span><span class="sxs-lookup"><span data-stu-id="4f2f7-144">CoreOS</span></span>

<span data-ttu-id="4f2f7-145">Les images CoreOS récentes d’Azure ont été préconfigurées avec DHCPv6.</span><span class="sxs-lookup"><span data-stu-id="4f2f7-145">Recent CoreOS images in Azure have been pre-configured with DHCPv6.</span></span> <span data-ttu-id="4f2f7-146">Aucune modification supplémentaire n’est requise pour l’utilisation de ces images.</span><span class="sxs-lookup"><span data-stu-id="4f2f7-146">No additional changes are required when using those images.</span></span> <span data-ttu-id="4f2f7-147">Si vous possédez une machine virtuelle basée sur une image CoreOS ancienne ou personnalisée, appliquez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4f2f7-147">If you have a VM based on an older or custom CoreOS image, use the following steps:</span></span>

1. <span data-ttu-id="4f2f7-148">Modifiez le fichier `/etc/systemd/network/10_dhcp.network`</span><span class="sxs-lookup"><span data-stu-id="4f2f7-148">Edit the file `/etc/systemd/network/10_dhcp.network`</span></span>

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. <span data-ttu-id="4f2f7-149">Renouvelez l’adresse IPv6 :</span><span class="sxs-lookup"><span data-stu-id="4f2f7-149">Renew the IPv6 address:</span></span>

    ```bash
    sudo systemctl restart systemd-networkd
    ```
