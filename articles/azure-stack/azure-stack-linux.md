---
title: "Invités Linux sur Azure Stack | Microsoft Docs"
description: "Découvrez comment créer des machines virtuelles Linux sur Azure Stack."
services: azure-stack
documentationcenter: 
author: anjayajodha
manager: byronr
editor: 
ms.assetid: d2155c59-902e-4f63-ac58-d19e6a765380
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: anajod
ms.openlocfilehash: 935cd31c4b38262b7e42271574a8a221377a3cec
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-linux-virtual-machines-on-azure-stack"></a>Déployer des machines virtuelles Linux sur Azure Stack
Vous pouvez déployer des machines virtuelles Linux sur le Kit de développement Azure Stack en ajoutant une image Linux dans la Place de Marché Azure Stack. Plusieurs fournisseurs Linux proposent des images qui peuvent être ajoutées à un Kit de développement Azure Stack, mais vous pouvez aussi générer votre propre image.

## <a name="download-an-image"></a>Télécharger une image
1. Téléchargez et extrayez une image compatible avec Azure Stack à partir des liens suivants, ou préparez votre propre image :
   
   * [Bitnami](https://bitnami.com/azure-stack)
   * [CentOS](http://olstacks.cloudapp.net/latest/)
   * [CoreOS](https://stable.release.core-os.net/amd64-usr/current/coreos_production_azure_image.vhd.bz2)
   * [SuSE](https://download.suse.com/Download?buildid=VCFi7y7MsFQ~)
   * [Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)
2. Extrayez le disque dur virtuel d’image si nécessaire et [ajoutez l’image à la Place de Marché](azure-stack-add-vm-image.md). Vérifiez que le paramètre `OSType` a la valeur `Linux`.
3. Une fois que vous avez ajouté l’image à la Place de Marché, un élément de Place de Marché est créé et vous pouvez déployer une machine virtuelle Linux.

## <a name="prepare-your-own-image"></a>Préparer votre propre image
1. Préparez votre propre image Linux en appliquant l’une des instructions suivantes :
   
   * [Distributions CentOS](../virtual-machines/linux/create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Debian Linux](../virtual-machines/linux/debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Oracle Linux](../virtual-machines/linux/oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Red Hat Enterprise Linux](../virtual-machines/linux/redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [SLES et openSUSE](../virtual-machines/linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Ubuntu](../virtual-machines/linux/create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. Téléchargez et installez l’[agent Linux Azure](https://github.com/Azure/WALinuxAgent/)
   
    L’agent Linux Azure version 2.1.3 ou ultérieure est nécessaire pour approvisionner votre machine virtuelle Linux sur Azure Stack. La plupart des distributions répertoriées ci-dessus incluent déjà cette version de l’agent ou une version ultérieure en tant que package dans leurs dépôts (généralement nommé `WALinuxAgent` ou `walinuxagent`). Toutefois, si la version du package de l’agent Azure est inférieure à la version 2.1.3 (autrement dit, 2.0.18 ou inférieure), vous devez installer l’agent manuellement. Vous pouvez déterminer la version installée à partir du nom de package ou en exécutant `/usr/sbin/waagent -version` sur la machine virtuelle.
   
    Pour installer l’agent Linux Azure manuellement, suivez les instructions ci-dessous :
   
   * Commencez par télécharger l’agent Linux Azure le plus récent à partir de [GitHub](https://github.com/Azure/WALinuxAgent/releases), par exemple :
     
            # wget https://github.com/Azure/WALinuxAgent/archive/v2.2.0.tar.gz
   * Décompressez l’agent Azure :
     
            # tar -vzxf v2.2.0.tar.gz
   * Installez python-setuptools :
     
        **Debian / Ubuntu**
     
            # sudo apt-get update
            # sudo apt-get install python-setuptools
     
        **Ubuntu 16.04+**
     
            # sudo apt-get install python3-setuptools
     
        **RHEL / CentOS / Oracle Linux**
     
            # sudo yum install python-setuptools
   * Installez l’agent Azure :
     
            # cd WALinuxAgent-2.2.0
            # sudo python setup.py install --register-service
     
     Les systèmes sur lesquels Python 2.x et Python 3.x sont installés côte à côte devront peut-être exécuter la commande suivante :
     
         sudo python3 setup.py install --register-service
     Pour plus d’informations, consultez le [fichier LISEZMOI](https://github.com/Azure/WALinuxAgent/blob/master/README.md) de l’agent Linux Azure.
3. [Ajoutez l’image à la Place de Marché](azure-stack-add-vm-image.md). Vérifiez que le paramètre `OSType` a la valeur `Linux`.
4. Une fois que vous avez ajouté l’image à la Place de Marché, un élément de Place de Marché est créé et vous pouvez déployer une machine virtuelle Linux.

## <a name="next-steps"></a>Étapes suivantes
[Forum aux questions sur Azure Stack](azure-stack-faq.md)

