---
title: "aaaConfigure un réseau virtuel dans Azure DevTest Labs | Documents Microsoft"
description: "Découvrez comment tooconfigure un réseau virtuel existant et un sous-réseau et les utiliser dans une machine virtuelle avec Azure DevTest Labs"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 6cda99c2-b87e-4047-90a0-5df10d8e9e14
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: a11ce8315e3c540e44aeacc9c5ee3dde014d4621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-in-azure-devtest-labs"></a>Configuration d’un réseau virtuel dans Azure DevTest Labs
Comme expliqué dans l’article hello, [ajouter une machine virtuelle avec lab de tooa artefacts](devtest-lab-add-vm-with-artifacts.md), lorsque vous créez une machine virtuelle dans un laboratoire, vous pouvez spécifier un réseau virtuel configuré. Un scénario pour cette opération est que si vous avez besoin de tooaccess vos ressources réseau d’entreprise à partir de vos machines virtuelles à l’aide de hello réseau virtuel qui a été configuré avec ExpressRoute ou VPN de site à site. Hello sections suivantes illustrent comment tooadd votre réseau virtuel existant dans les paramètres de réseau virtuel d’un laboratoire afin qu’il soit toochoose disponible lors de la création de machines virtuelles.

## <a name="configure-a-virtual-network-for-a-lab-using-hello-azure-portal"></a>Configurer un réseau virtuel pour un laboratoire à l’aide de hello portail Azure
Hello étapes suivantes vous guident tout ajout d’un laboratoire de tooa réseau (et de sous-réseau) virtuel existant afin qu’il peut être utilisé lors de la création d’une machine virtuelle Bonjour même laboratoire. 

1. Connectez-vous à toohello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Sélectionnez **plus Services**, puis sélectionnez **DevTest Labs** à partir de la liste de hello.
3. Dans liste hello labs, sélectionnez lab souhaité de hello. 
4. Dans le panneau de hello lab, sélectionnez **Configuration**.
5. Sur du laboratoire hello **Configuration** panneau, sélectionnez **réseaux virtuels**.
6. Sur hello **réseaux virtuels** panneau, vous voyez une liste de réseaux virtuels configurés pour pratiques hello ainsi que de réseau virtuel hello par défaut qui est créé pour votre laboratoire. 
7. Sélectionnez **Ajouter**.
   
    ![Ajouter un laboratoire tooyour de réseau virtuel existant](./media/devtest-lab-configure-vnet/lab-settings-vnet-add.png)
8. Sur hello **réseau virtuel** panneau, sélectionnez **[réseau virtuel]**.
   
    ![Sélection d’un réseau virtuel existant](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet1.png)
9. Sur hello **réseau virtuel de choisir** panneau, le réseau virtuel auquel vous souhaitez hello select. panneau Hello affiche tous les réseaux virtuels hello qui sont sous hello même région dans l’abonnement hello comme lab de hello.  
10. Après avoir sélectionné un réseau virtuel, vous êtes renvoyé toohello **réseau virtuel** cliquez sur le sous-réseau hello dans liste hello bas hello du Panneau de hello.

    ![Liste des sous-réseaux](./media/devtest-lab-configure-vnet/lab-settings-vnets-vnet2.png)
    
    Panneau de sous-réseau d’atelier Hello s’affiche.

    ![Panneau Lab Subnet (Sous-réseau de laboratoire)](./media/devtest-lab-configure-vnet/lab-subnet.png)

11. Spécifiez un **nom de sous-réseau de laboratoire**.
12. tooallow un toobe de sous-réseau utilisé dans le laboratoire de la création d’ordinateurs virtuels, sélectionnez **utilisé dans la création de la machine virtuelle**.
13. tooenable un [partagé d’adresse IP publique](devtest-lab-shared-ip.md), sélectionnez **activer partagée d’adresse IP publique**.
14. les adresses IP publiques tooallow dans un sous-réseau, sélectionnez **permettre la création d’IP publique**.
15. Bonjour **virtuels Maximum par utilisateur** indiquez hello maximales machines virtuelles par utilisateur pour chaque sous-réseau. Si vous souhaitez un nombre illimité de machines virtuelles, laissez ce champ vide.
16. Sélectionnez **OK** Panneau de sous-réseau de l’atelier tooclose hello.
17. Sélectionnez **enregistrer** Panneau de réseau virtuel tooclose hello.
18. Maintenant que hello réseau virtuel est configuré, il peut être sélectionné lors de la création d’une machine virtuelle. 
    toosee comment toocreate une machine virtuelle et spécifier un réseau virtuel, consultez l’article toohello [ajouter une machine virtuelle avec lab de tooa artefacts](devtest-lab-add-vm-with-artifacts.md). 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a>Étapes suivantes
Lorsque vous avez ajouté hello souhaité lab tooyour de réseau virtuel, étape suivante de hello est trop[ajouter un laboratoire tooyour de machine virtuelle](devtest-lab-add-vm-with-artifacts.md).

