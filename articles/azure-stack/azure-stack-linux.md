---
title: "Invités aaaLinux sur la pile de Azure | Documents Microsoft"
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
ms.openlocfilehash: 225bed7d630b676ca760add25731e347516b5bf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-linux-virtual-machines-on-azure-stack"></a>Déployer des machines virtuelles Linux sur Azure Stack
Vous pouvez déployer des ordinateurs virtuels Linux sur hello Kit de développement de pile Azure en ajoutant une image Linux hello Azure Marketplace de pile. Plusieurs fournisseurs Linux proposent des images qui peuvent être ajoutées à un Kit de développement Azure Stack, mais vous pouvez aussi générer votre propre image.

## <a name="download-an-image"></a>Télécharger une image
1. Télécharger et extraire une image de la pile compatibles Azure hello suivant liens ou préparer votre propre :
   
   * [Bitnami](https://bitnami.com/azure-stack)
   * [CentOS](http://olstacks.cloudapp.net/latest/)
   * [CoreOS](https://stable.release.core-os.net/amd64-usr/current/coreos_production_azure_image.vhd.bz2)
   * [SuSE](https://download.suse.com/Download?buildid=VCFi7y7MsFQ~)
   * [Ubuntu 14.04 LTS](https://partner-images.canonical.com/azure/azure_stack/) / [Ubuntu 16.04 LTS](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)
2. Extraire l’image du disque dur virtuel hello si nécessaire et [ajouter hello image toohello Marketplace](azure-stack-add-vm-image.md). Vérifiez que hello `OSType` paramètre est défini trop`Linux`.
3. Une fois que vous avez ajouté hello image toohello Marketplace, un élément de Marketplace est créé et vous pouvez déployer une machine virtuelle Linux.

## <a name="prepare-your-own-image"></a>Préparer votre propre image
1. Préparez votre propre image de Linux à l’aide de hello suivant les instructions :
   
   * [Distributions CentOS](../virtual-machines/linux/create-upload-centos.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Debian Linux](../virtual-machines/linux/debian-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Oracle Linux](../virtual-machines/linux/oracle-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Red Hat Enterprise Linux](../virtual-machines/linux/redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [SLES et openSUSE](../virtual-machines/linux/suse-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
   * [Ubuntu](../virtual-machines/linux/create-upload-ubuntu.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. Téléchargez et installez hello [Linux Agent Azure](https://github.com/Azure/WALinuxAgent/)
   
    Hello version de le Linux Agent Azure 2.1.3 ou supérieure est requise tooprovision votre VM Linux sur Azure pile. La plupart des distributions hello répertoriées ci-dessus déjà comprennent cette version de l’agent de hello ou supérieure sous forme de package dans leurs référentiels (généralement appelé `WALinuxAgent` ou `walinuxagent`). Toutefois, si hello version du package de l’agent Windows Azure hello est inférieur à 2.1.3 (2.0.18 ou inférieur), vous devez installer manuellement l’agent de hello. version de Hello installé peut être déterminée à partir du nom du package hello ou en exécutant `/usr/sbin/waagent -version` sur hello machine virtuelle.
   
    Suivez les instructions de hello sous l’agent Azure Linux de hello tooinstall manuellement :
   
   * Commencez par télécharger hello dernière Azure agent Linux à partir de [GitHub](https://github.com/Azure/WALinuxAgent/releases), exemple :
     
            # wget https://github.com/Azure/WALinuxAgent/archive/v2.2.0.tar.gz
   * Décompresser hello agent Azure :
     
            # tar -vzxf v2.2.0.tar.gz
   * Installez python-setuptools :
     
        **Debian / Ubuntu**
     
            # sudo apt-get update
            # sudo apt-get install python-setuptools
     
        **Ubuntu 16.04+**
     
            # sudo apt-get install python3-setuptools
     
        **RHEL / CentOS / Oracle Linux**
     
            # sudo yum install python-setuptools
   * Installez hello agent Azure :
     
            # cd WALinuxAgent-2.2.0
            # sudo python setup.py install --register-service
     
     Systèmes avec Python 2.x et 3.x installé Python côte à côte doivent hello toorun commande suivante :
     
         sudo python3 setup.py install --register-service
     Pour plus d’informations, consultez hello Linux Agent Azure [Lisez-moi](https://github.com/Azure/WALinuxAgent/blob/master/README.md).
3. [Ajouter l’image de hello toohello Marketplace](azure-stack-add-vm-image.md). Vérifiez que hello `OSType` paramètre est défini trop`Linux`.
4. Une fois que vous avez ajouté hello image toohello Marketplace, un élément de Marketplace est créé et vous pouvez déployer une machine virtuelle Linux.

## <a name="next-steps"></a>Étapes suivantes
[Forum aux questions sur Azure Stack](azure-stack-faq.md)

