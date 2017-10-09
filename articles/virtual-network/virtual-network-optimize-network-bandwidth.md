---
title: "débit de réseau de machine virtuelle aaaOptimize | Documents Microsoft"
description: "Découvrez comment toooptimize machine virtuelle Azure débit du réseau."
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: a5cff2d0ab6e3553c3f90d99629521a431477de0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a>Optimiser le débit du réseau des machines virtuelles Azure

Les machines virtuelles Azure disposent de paramètres réseau par défaut qui peuvent être davantage optimisés pour le débit du réseau. Cet article décrit comment toooptimize débit du réseau pour Windows Azure de Microsoft et les machines virtuelles Linux, y compris les distributions majeures telles que Ubuntu, CentOS et Red Hat.

## <a name="windows-vm"></a>Machine virtuelle Windows

Si votre machine virtuelle Windows est prise en charge avec [Accelerated réseau](virtual-network-create-vm-accelerated-networking.md), l’activation de cette fonctionnalité serait la configuration optimale de hello pour le débit. Pour toutes les autres machines virtuelles Windows, l’utilisation de la mise à l’échelle côté réception (RSS) peut permettre d’atteindre un débit maximal supérieur à celui d’une machine virtuelle sans RSS. La mise à l’échelle côté réception (RSS) peut être désactivée par défaut sur une machine virtuelle Windows. Terminer hello suivant les étapes toodetermine si RSS est activé et tooenable si elle est désactivée.

1. Entrez hello `Get-NetAdapterRss` toosee de commande PowerShell si RSS est activé pour une carte réseau. Bonjour suivant l’exemple de sortie retourné par hello `Get-NetAdapterRss`, RSS n’est pas activé.

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. Entrez hello suivant commande tooenable RSS :

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    commande précédente Hello n’a pas une sortie. commande Hello modifié des paramètres de carte réseau, à l’origine de la perte de connectivité temporaire d’une minute environ. Une boîte de dialogue Nouvelle connexion en cours s’affiche lors de la perte de connectivité hello. En général la connectivité est rétablie après une tentative de tiers hello.
3. Vérifiez que RSS est activé dans la machine virtuelle de hello en entrant hello `Get-NetAdapterRss` réexécutez la commande. En cas de réussite, hello suivant l’exemple de sortie est retournée :

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a>Machine virtuelle Linux

La mise à l’échelle côté réception (RSS) est toujours activée par défaut sur une machine virtuelle Azure Linux. Noyaux Linux publiées depuis janvier 2017 incluent de nouvelles options d’optimisation de réseau qui permettent un débit plus élevé du réseau tooachieve Linux VM.

### <a name="ubuntu"></a>Ubuntu

Dans l’optimisation de l’ordre tooget hello, tout d’abord mettre à jour version toohello dernières pris en charge, à compter de juin 2017, qui est :
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
Une fois la mise à jour hello est terminée, entrez hello suivant du noyau de commandes tooget hello plus récent :

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

Commande facultative :

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a>Noyau de la préversion Ubuntu Azure
> [!WARNING]
> Cette version d’évaluation Azure Linux noyau ne peut pas avoir hello même niveau de disponibilité et la fiabilité en tant qu’images de Marketplace et noyaux qui sont en général version en disponibilité. fonctionnalité de Hello n’est pas pris en charge peut-être avoir limitées des fonctionnalités et ne peut pas être aussi fiable que le noyau de hello par défaut. N’utilisez pas ce noyau pour les charges de travail de production.

Performances de débit significative possible en installant hello proposé noyau Azure Linux. tootry ce noyau, ajoutez cette ligne de too/etc/apt/sources.list

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

Exécutez ensuite ces commandes en tant qu’utilisateur racine.
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a>CentOS

Dans l’optimisation de l’ordre tooget hello, tout d’abord mettre à jour version toohello dernières pris en charge, à compter de juillet 2017, qui est :
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
Une fois la mise à jour hello est terminée, installation Bonjour derniers Services d’intégration Linux (LIS).
optimisation de débit Hello est LIS, en commençant à partir de 4.2.2-2. Entrez hello suivant de commandes tooinstall LIS :

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a>Red Hat

Dans l’optimisation de l’ordre tooget hello, tout d’abord mettre à jour version toohello dernières pris en charge, à compter de juillet 2017, qui est :
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
Une fois la mise à jour hello est terminée, installation Bonjour derniers Services d’intégration Linux (LIS).
optimisation de débit Hello est LIS, en commençant à partir de 4.2. Entrez hello suivant toodownload de commandes et installer LIS :

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

En savoir plus sur Linux Integration Services Version 4.2 pour Hyper-V en consultant hello [page de téléchargement](https://www.microsoft.com/download/details.aspx?id=55106).

## <a name="next-steps"></a>Étapes suivantes
* Maintenant que hello machine virtuelle est optimisée, consultez résultat hello avec [la bande passante ou de débit test Azure VM](virtual-network-bandwidth-testing.md) pour votre scénario.
* En savoir plus avec le [FAQ sur les réseaux virtuels Azure](virtual-networks-faq.md)
