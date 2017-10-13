---
title: "Optimiser le débit du réseau des machines virtuelles | Microsoft Docs"
description: "Découvrez comment optimiser le débit du réseau des machines virtuelles Azure."
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
ms.openlocfilehash: 914747983d4d974810836be66d6c6af343f58b60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a>Optimiser le débit du réseau des machines virtuelles Azure

Les machines virtuelles Azure disposent de paramètres réseau par défaut qui peuvent être davantage optimisés pour le débit du réseau. Cet article décrit comment optimiser le débit du réseau pour les machines virtuelles Microsoft Azure Windows et Linux, notamment les distributions majeures telles que Ubuntu, CentOS et Red Hat.

## <a name="windows-vm"></a>Machine virtuelle Windows

Si votre machine virtuelle Windows est compatible avec la [mise en réseau accélérée](virtual-network-create-vm-accelerated-networking.md), l’activation de cette fonctionnalité constitue la configuration optimale pour le débit. Pour toutes les autres machines virtuelles Windows, l’utilisation de la mise à l’échelle côté réception (RSS) peut permettre d’atteindre un débit maximal supérieur à celui d’une machine virtuelle sans RSS. La mise à l’échelle côté réception (RSS) peut être désactivée par défaut sur une machine virtuelle Windows. Effectuez les étapes suivantes pour déterminer si la mise à l’échelle côté réception (RSS) est activée et, si nécessaire, pour l’activer.

1. Entrez la commande PowerShell `Get-NetAdapterRss` pour savoir si la mise à l’échelle côté réception (RSS) est activée sur une carte réseau. Dans l’exemple de sortie suivant retourné par `Get-NetAdapterRss`, la mise à l’échelle côté réception (RSS) n’est pas activée.

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. Entrez la commande suivante pour activer la mise à l’échelle côté réception (RSS) :

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    La commande précédente n’a pas de sortie. La commande a modifié les paramètres de la carte réseau, entraînant une perte temporaire de la connectivité pendant environ une minute. Une boîte de dialogue de reconnexion s’affiche lors de la perte de connectivité. En général, la connectivité est rétablie après la troisième tentative.
3. Vérifiez que la mise à l’échelle côté réception (RSS) est activée sur la machine virtuelle en entrant de nouveau la commande `Get-NetAdapterRss`. Si l’opération réussit, l’exemple de sortie suivant est retourné :

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a>Machine virtuelle Linux

La mise à l’échelle côté réception (RSS) est toujours activée par défaut sur une machine virtuelle Azure Linux. Les noyaux Linux publiés depuis janvier 2017 incluent de nouvelles options d’optimisation du réseau qui permettent à une machine virtuelle Linux d’obtenir un débit réseau plus élevé.

### <a name="ubuntu"></a>Ubuntu

Pour bénéficier de l’optimisation, mettez tout d’abord à jour vers la version la plus récente, à compter de juin 2017, qui est :
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
Une fois la mise à jour terminée, entrez les commandes suivantes pour obtenir le noyau le plus récent :

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
> Ce noyau de la préversion Azure Linux peut ne pas offrir les mêmes niveaux de disponibilité et de fiabilité que les noyaux et images de la Place de marché qui se trouvent dans la version mise à la disposition générale. La fonctionnalité n’est pas prise en charge, est susceptible de disposer de possibilités limitées et peut ne pas être aussi fiable que le noyau par défaut. N’utilisez pas ce noyau pour les charges de travail de production.

Des performances significatives en termes de débit peuvent être atteintes en installant le noyau Azure Linux proposé. Pour tester ce noyau, ajoutez cette ligne à /etc/apt/sources.list.

```bash
#add this to the end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

Exécutez ensuite ces commandes en tant qu’utilisateur racine.
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a>CentOS

Pour bénéficier de l’optimisation, mettez tout d’abord à jour vers la version la plus récente, à compter de juillet 2017, qui est :
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
Une fois la mise à jour terminée, installez les Services d’intégration Linux (LIS) les plus récents.
L’optimisation du débit est incluse dans les LIS, à partir de la version 4.2.2-2. Entrez les commandes suivantes pour installer LIS :

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a>Red Hat

Pour bénéficier de l’optimisation, mettez tout d’abord à jour vers la version la plus récente, à compter de juillet 2017, qui est :
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
Une fois la mise à jour terminée, installez les Services d’intégration Linux (LIS) les plus récents.
L’optimisation du débit est incluse dans les LIS, à partir de la version 4.2. Entrez les commandes suivantes pour télécharger et installer les LIS :

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

Apprenez-en plus sur les Services d’intégration Linux version 4.2 pour Hyper-V en consultant la [page de téléchargement](https://www.microsoft.com/download/details.aspx?id=55106).

## <a name="next-steps"></a>Étapes suivantes
* À présent que la machine virtuelle est optimisée, voyez le résultat avec le [Test de bande passante/débit de machine virtuelle](virtual-network-bandwidth-testing.md) pour votre scénario.
* En savoir plus avec le [FAQ sur les réseaux virtuels Azure](virtual-networks-faq.md)
