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
# <a name="configuring-dhcpv6-for-linux-vms"></a>Configuration de DHCPv6 pour les machines virtuelles Linux

Certaines des images de machine virtuelle Linux hello Bonjour Azure Marketplace inutile DHCPv6 configuré par défaut. toosupport IPv6, DHCPv6 doit être configuré au sein de la distribution du système d’exploitation Linux hello que vous utilisez. Différentes distributions Linux présentent des méthodes de configuration de DHCPv6 distinctes, car elles utilisent des packages non identiques.

> [!NOTE]
> Les images SUSE Linux et CoreOS récentes Bonjour Azure Marketplace ont été préconfigurées avec DHCPv6. Aucune modification supplémentaire n’est requise pour l’utilisation de ces images.

Ce document décrit comment tooenable DHCPv6 afin que votre machine virtuelle de Linux obtienne une adresse IPv6.

> [!WARNING]
> Modification incorrecte des fichiers de configuration de réseau risque de vous toolose réseau accès tooyour machine virtuelle. Nous vous recommandons de tester vos modifications de configuration sur des systèmes hors production. instructions Hello dans cet article ont été testées sur hello dernières versions des images de Linux hello Bonjour Azure Marketplace. Consultez la documentation de hello spécifique à votre version de Linux pour obtenir des instructions plus détaillées.

## <a name="ubuntu"></a>Ubuntu

1. Modifier le fichier de hello `/etc/dhcp/dhclient6.conf` et ajoutez hello ligne suivante :

        timeout 10;

2. Modifier la configuration de réseau de hello pour l’interface d’eth0 hello avec hello configuration suivante :

   * Sur **Ubuntu 12.04 et 14.04**, modifiez le fichier de hello`/etc/network/interfaces.d/eth0.cfg`
   * Sur **Ubuntu 16.04**, modifiez le fichier de hello`/etc/network/interfaces.d/50-cloud-init.cfg`

         iface eth0 inet6 auto
             up sleep 5
             up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. Renouvelez l’adresse IPv6 :

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="debian"></a>Debian

1. Modifier le fichier de hello `/etc/dhcp/dhclient6.conf` et ajoutez hello ligne suivante :

        timeout 10;

2. Modifier le fichier de hello `/etc/network/interfaces` et ajoutez hello configuration suivante :

        iface eth0 inet6 auto
            up sleep 5
            up dhclient -1 -6 -cf /etc/dhcp/dhclient6.conf -lf /var/lib/dhcp/dhclient6.eth0.leases -v eth0 || true

3. Renouvelez l’adresse IPv6 :

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="rhel--centos--oracle-linux"></a>RHEL / CentOS / Oracle Linux

1. Modifier le fichier de hello `/etc/sysconfig/network` et ajoutez hello suivant paramètre :

        NETWORKING_IPV6=yes

2. Modifier le fichier de hello `/etc/sysconfig/network-scripts/ifcfg-eth0` et ajoutez hello deux paramètres suivants :

        IPV6INIT=yes
        DHCPV6C=yes

3. Renouvelez l’adresse IPv6 :

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-11--opensuse-13"></a>SLES 11 et openSUSE 13

Les images SLES et openSUSE récentes d’Azure ont été préconfigurées avec DHCPv6. Aucune modification supplémentaire n’est requise pour l’utilisation de ces images. Si vous avez une machine virtuelle basée sur une image SUSE antérieure ou personnalisée, utilisez hello comme suit :

1. Installer hello `dhcp-client` du package, si nécessaire :

    ```bash
    sudo zypper install dhcp-client
    ```

2. Modifier le fichier de hello `/etc/sysconfig/network/ifcfg-eth0` et ajoutez hello suivant paramètre :

        DHCLIENT6_MODE='managed'

3. Renouveler l’adresse de hello IPv6 :

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="sles-12-and-opensuse-leap"></a>SLES 12 et openSUSE Leap

Les images SLES et openSUSE récentes d’Azure ont été préconfigurées avec DHCPv6. Aucune modification supplémentaire n’est requise pour l’utilisation de ces images. Si vous avez une machine virtuelle basée sur une image SUSE antérieure ou personnalisée, utilisez hello comme suit :

1. Modifier le fichier de hello `/etc/sysconfig/network/ifcfg-eth0` et remplacer ce paramètre

        #BOOTPROTO='dhcp4'

    avec hello valeur suivante :

        BOOTPROTO='dhcp'

2. Ajouter hello suit le paramètre trop`/etc/sysconfig/network/ifcfg-eth0`:

        DHCLIENT6_MODE='managed'

3. Renouveler l’adresse de hello IPv6 :

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

## <a name="coreos"></a>CoreOS

Les images CoreOS récentes d’Azure ont été préconfigurées avec DHCPv6. Aucune modification supplémentaire n’est requise pour l’utilisation de ces images. Si vous avez une machine virtuelle basée sur une image CoreOS antérieure ou personnalisée, utilisez hello comme suit :

1. Modifier le fichier de hello`/etc/systemd/network/10_dhcp.network`

        [Match]
        eth0

        [Network]
        DHCP=ipv6

2. Renouveler l’adresse de hello IPv6 :

    ```bash
    sudo systemctl restart systemd-networkd
    ```
