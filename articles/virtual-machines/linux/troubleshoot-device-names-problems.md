---
title: "les noms des périphériques aaaLinux machine virtuelle sont modifiés dans Azure | Documents Microsoft"
description: "Explique hello pourquoi les noms des périphériques sont modifiés et fournissent des solutions pour résoudre ce problème."
services: virtual-machines-linux
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: 
ms.service: virtual-machines-linux
ms.topic: article
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 4d3a5853d61edd2c8e8b85ab69e5ed3b3bc00bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-linux-vm-device-names-are-changed"></a>Résolution des problèmes : les noms d’appareil des machines virtuelles Linux sont modifiés

Hello explique pourquoi les noms des périphériques sont modifiés après avoir redémarrer une machine virtuelle de Linux (VM), ou rattacher les disques hello. Il fournit également des solutions de hello pour résoudre ce problème.

## <a name="symptom"></a>Symptôme

Vous pouvez rencontrer les problèmes suivants lors de l’exécution des machines virtuelles Linux dans Microsoft Azure de hello.

- Hello VM échoue tooboot après un redémarrage.

- Si les disques de données sont détachées et rattachés, les noms de périphériques hello pour les disques sont modifiés.

- Les applications ou un scripts faisant référence à un disque par son nom d’appareil échouent. Vous trouverez ce hello nom du périphérique de disque de hello est modifiée.

## <a name="cause"></a>Cause :

Chemins d’accès de périphérique dans Linux ne sont pas garantis toobe cohérent entre les redémarrages. Les noms d’appareil se composent de numéros principaux (lettre) et secondaires.  Lorsque le pilote de périphérique de stockage de Linux hello détecte un nouveau périphérique, il assigne tooit de numéros de périphériques principaux et secondaires à partir de la plage de hello disponibles. Lorsqu’un périphérique est supprimé, hello numéros sont libéré toobe le réutiliser ultérieurement.

Hello dû hello analyse dans Linux planifiée par le sous-système SCSI hello se produit en mode asynchrone. Hello périphérique final chemin d’accès d’affectation de noms peut varier entre les redémarrages. 

## <a name="solution"></a>Solution

tooresolve ce problème, utilisez persistant d’affectation de noms. Il existe quatre méthodes toopersistent d’affectation de noms - par l’étiquette de système de fichiers, par uuid, par id et par chemin d’accès. Nous vous recommandons d’étiquette de système de fichiers hello et les méthodes de l’UUID pour les machines virtuelles Linux Azure. 

La plupart des distributions fournissent également soit hello **nofail** ou **nobootwait** fstab options. Ces options permettent une tooboot système même en cas de disque de hello toomount au démarrage. Consultez la documentation de la distribution hello pour plus d’informations sur ces paramètres. Pour plus d’informations sur comment tooconfigure un toouse Linux VM un UUID lorsque vous ajoutez un disque de données, consultez [connecter toohello nouveau disque Linux VM toomount hello](add-disk.md#connect-to-the-linux-vm-to-mount-the-new-disk). 

Lorsque l’agent de hello Azure Linux est installé sur une machine virtuelle, il utilise Udev règles tooconstruct un ensemble de liens symboliques sous **/dev/disk/azure**. Ces règles Udev peuvent être utilisées par les applications et les disques tooidentify scripts sont attaché toohello machine virtuelle, leur type, hello numéro d’unité logique.

## <a name="more-information"></a>Plus d’informations

### <a name="identify-disk-luns"></a>Identifier les numéros d’unité logique des disques

Une application peut utiliser des numéros d’unités logiques toofind tous les disques de hello attaché et créer des liens symboliques. l’agent Azure Linux de Hello inclut désormais les règles d’uDev pour configurer des liens symboliques à partir d’une unité de toohello numéro d’unité logique, procédez comme suit :

    $ tree /dev/disk/azure

    /dev/disk/azure
    ├── resource -> ../../sdb
    ├── resource-part1 -> ../../sdb1
    ├── root -> ../../sda
    ├── root-part1 -> ../../sda1
    └── scsi1
        ├── lun0 -> ../../../sdc
        ├── lun0-part1 -> ../../../sdc1
        ├── lun1 -> ../../../sdd
        ├── lun1-part1 -> ../../../sdd1
        ├── lun1-part2 -> ../../../sdd2
        └── lun1-part3 -> ../../../sdd3                                    
                                 

Numéro d’unité logique peut également être récupérée à partir Bonjour Linux invité à l’aide de lsscsi ou un outil similaire comme suit.

       $ sudo lsscsi

      [1:0:0:0] cd/dvd Msft Virtual CD/ROM 1.0 /dev/sr0

      [2:0:0:0] disk Msft Virtual Disk 1.0 /dev/sda

      [3:0:1:0] disk Msft Virtual Disk 1.0 /dev/sdb

      [5:0:0:0] disk Msft Virtual Disk 1.0 /dev/sdc

      [5:0:0:1] disk Msft Virtual Disk 1.0 /dev/sdd

Ces informations de numéro d’unité logique invité peuvent être utilisées à l’abonnement Azure métadonnées tooidentify hello emplacement dans le stockage Azure hello disque dur virtuel qui stocke les données de partition hello. Par exemple, utilisez hello az cli :

    $ az vm show --resource-group testVM --name testVM | jq -r .storageProfile.dataDisks                                        
    [                                                                                                                                                                  
    {                                                                                                                                                                  
    "caching": "None",                                                                                                                                              
      "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 1023,                                                                                                                                             
      "image": null,                                                                                                                                                   
    "lun": 0,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-114353",                                                                                                                    
    "vhd": {                                                                                                                                                          
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-114353.vhd"                                                       
    }                                                                                                                                                              
    },                                                                                                                                                                
    {                                                                                                                                                                   
    "caching": "None",                                                                                                                                               
    "createOption": "empty",                                                                                                                                         
    "diskSizeGb": 512,                                                                                                                                              
    "image": null,                                                                                                                                                   
    "lun": 1,                                                                                                                                                        
    "managedDisk": null,                                                                                                                                             
    "name": "testVM-20170619-121516",                                                                                                                    
    "vhd": {                                                                                                                                                           
      "uri": "https://testVM.blob.core.windows.net/vhd/testVM-20170619-121516.vhd"                                                       
      }                                                                                                                                                             
      }                                                                                                                                                             
    ]

### <a name="discover-filesystem-uuids-by-using-blkid"></a>Découvrir les UUID de système de fichiers à l’aide de l’utilitaire blkid

Un script ou une application peut lire la sortie hello du blkid ou autres sources similaires et construire des liens symboliques dans **dev** à utiliser. sortie de Hello affiche hello UUID de tous les disques attachés toohello machine virtuelle et hello appareil fichier toowhich elles sont associées :

    $ sudo blkid -s UUID

    /dev/sr0: UUID="120B021372645f72"
    /dev/sda1: UUID="52c6959b-79b0-4bdd-8ed6-71e0ba782fb4"
    /dev/sdb1: UUID="176250df-9c7c-436f-94e4-d13f9bdea744"
    /dev/sdc1: UUID="b0048738-4ecc-4837-9793-49ce296d2692"

règles d’udev Hello waagent construire un ensemble de liens symboliques sous **/dev/disk/azure**:


    $ ls -l /dev/disk/azure

    total 0
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 resource -> ../../sdb
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 resource-part1 -> ../../sdb1
    lrwxrwxrwx 1 root root  9 Jun  2 23:17 root -> ../../sda
    lrwxrwxrwx 1 root root 10 Jun  2 23:17 root-part1 -> ../../sda1


application Hello peut utiliser ces informations identifier le périphérique de disque de démarrage hello et le disque de la ressource (éphémère) hello. Dans Azure, les applications doivent faire référence trop**/dev/disk/azure/root-part1** ou **/dev/disk/azure-resource-part1** toodiscover ces partitions.

S’il existe des partitions supplémentaires à partir de la liste du blkid hello, ils se trouvent sur un disque de données. Applications hello UUID pour ces partitions et vous utilisez un chemin d’accès comme hello sous nom du périphérique toodiscover hello lors de l’exécution :

    $ ls -l /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692

    lrwxrwxrwx 1 root root 10 Jun 19 15:57 /dev/disk/by-uuid/b0048738-4ecc-4837-9793-49ce296d2692 -> ../../sdc1

    
### <a name="get-hello-latest-azure-storage-rules"></a>Obtenir des règles de stockage Azure hello plus récente

toohello dernières règles de stockage Azure, exécutez th suivant de commandes :

    # sudo curl -o /etc/udev/rules.d/66-azure-storage.rules https://raw.githubusercontent.com/Azure/WALinuxAgent/master/config/66-azure-storage.rules
    # sudo udevadm trigger --subsystem-match=block


Pour plus d’informations, consultez hello suivant des articles :

- [Ubuntu: Using UUID](https://help.ubuntu.com/community/UsingUUID) (Utilisation des UUID)

- [Red Hat: Persistent Naming](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Storage_Administration_Guide/persistent_naming.html) (Attribution de noms persistants)

- [Linux: What UUIDs can do for you](https://www.linux.com/news/what-uuids-can-do-you) (Ce que les UUID peuvent faire pour vous)

- [UDev : Introduction tooDevice Management dans le système moderne Linux](https://www.linux.com/news/udev-introduction-device-management-modern-linux-system)

