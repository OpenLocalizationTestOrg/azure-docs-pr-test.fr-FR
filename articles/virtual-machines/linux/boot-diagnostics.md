---
title: aaaBoot des diagnostics pour les ordinateurs virtuels Linux dans Azure | Documentation de Microsoft
description: "Vue d’ensemble des fonctionnalités de débogage deux hello pour les ordinateurs virtuels Linux dans Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: Deland-Han
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: delhan
ms.openlocfilehash: d355d512de09d2f1d7a2718e3db3fb99c9dd9e24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-boot-diagnostics-tootroubleshoot-linux-virtual-machines-in-azure"></a>Comment toouse démarrer les ordinateurs virtuels Linux diagnostics tootroubleshoot dans Azure

La prise en charge de deux fonctionnalités de débogage est désormais disponible dans Azure : les supports de Console Output et Screenshot pour le modèle de déploiement Azure Virtual Machines Resource Manager. 

Lors de la prochaine tooAzure de votre propre image ou même initialisation d’une des images de plateforme hello, il peut y avoir plusieurs raisons pour lesquelles un ordinateur virtuel Obtient dans un état non démarrable. Activation de ces fonctionnalités vous tooeasily diagnostiquer et récupérer vos Machines virtuelles des échecs de démarrage.

Pour les Machines virtuelles Linux, vous pouvez facilement afficher sortie hello de votre journal de console à partir de hello portail :

![Portail Azure](./media/boot-diagnostics/screenshot1.png)
 
Toutefois, pour Windows et les ordinateurs virtuels Linux, Azure permet également de toosee une capture d’écran de hello machine virtuelle à partir de l’hyperviseur de hello :

![Error](./media/boot-diagnostics/screenshot2.png)

Ces deux fonctionnalités sont prises en charge par les Machines Virtuelles Azure dans toutes les régions. Tooappear de minutes too10 dans votre compte de stockage peuvent prendre note des captures d’écran et la sortie.

## <a name="common-boot-errors"></a>Erreurs de démarrage courantes

- [Problèmes de système de fichiers](https://blogs.msdn.microsoft.com/linuxonazure/2016/09/13/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes/)
- [Problèmes de noyau](https://blogs.msdn.microsoft.com/linuxonazure/2016/10/09/linux-recovery-manually-fixing-non-boot-issues-related-to-kernel-problems/)
- [Erreurs FSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/ )

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>Activer la fonction de diagnostic sur une nouvelle machine virtuelle
1. Lorsque vous créez une Machine virtuelle à partir de la version préliminaire du portail de hello, sélectionnez hello **Azure Resource Manager** à partir de la liste déroulante modèle de déploiement hello :
 
    ![Gestionnaire de ressources](./media/boot-diagnostics/screenshot3.jpg)

2. Configurer hello analyse option tooselect hello de stockage Azure où vous aimeriez tooplace ces fichiers de diagnostic.
 
    ![Créer une machine virtuelle](./media/boot-diagnostics/screenshot4.jpg)

3. Si vous déployez un modèle Azure Resource Manager, accédez de ressource d’ordinateur virtuel tooyour et ajouter la section de profil de diagnostics hello. N’oubliez pas d’en-tête de version de l’API de toouse hello « 2015-06-15 ».

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. profil de diagnostic Hello vous permet de compte de stockage hello tooselect où vous souhaitez tooput ces journaux.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

## <a name="update-an-existing-virtual-machine"></a>Mettre à jour une machine virtuelle existante

diagnostics de démarrage tooenable via le portail de hello, vous pouvez également mettre à jour un ordinateur virtuel existant via le portail de hello. Sélectionnez hello option Diagnostics de démarrage et les enregistrer. Redémarrez l’effet de tootake hello machine virtuelle.

![Mettre à jour une machine virtuelle existante](./media/boot-diagnostics/screenshot5.png)