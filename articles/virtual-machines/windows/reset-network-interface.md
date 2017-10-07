---
title: "interface réseau Windows Azure VM aaaHow tooreset | Documents Microsoft"
description: "Montre comment tooreset interface réseau pour la machine virtuelle de Windows Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: genlin
manager: willchen
editor: 
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: genli
ms.openlocfilehash: 1b653820927ef4c3bb8f384a7e752846a8be3da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-network-interface-for-azure-windows-vm"></a>Comment tooreset interface réseau pour la machine virtuelle de Windows Azure 

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Vous ne peut pas se connecter à tooMicrosoft Machine virtuelle de Windows Azure (VM) après la désactivation de la valeur par défaut de hello d’Interface réseau (NIC) ou manuellement définit une adresse IP statique pour la carte réseau de hello. Cet article explique comment tooreset hello interface réseau de l’ordinateur virtuel Windows Azure, qui résout le problème de connexion à distance hello.

[!INCLUDE [support-disclaimer](../../../includes/support-disclaimer.md)]
## <a name="reset-network-interface"></a>Réinitialiser l’interface réseau

### <a name="for-classic-vms"></a>Pour les machines virtuelles Classic

tooreset réseau de l’interface, procédez comme suit :

1.  Accédez toohello [portail Azure]( https://ms.portal.azure.com).
2.  Sélectionnez **Machines virtuelles (Classic)**.
3.  Sélectionnez hello affectées de Machine virtuelle.
4.  Sélectionnez **Adresses IP**.
5.  Si hello **l’attribution IP privé** n’est pas **statique**, modifiez-le trop**statique**.
6.  Hello de modification **adresse IP** tooanother adresse IP disponible dans hello sous-réseau.
7.  Sélectionnez Enregistrer.
8.  machine virtuelle de Hello redémarre tooinitialize hello nouveau NIC toohello système.
9.  Essayez tooRDP tooyour machine. En cas de réussite, vous pouvez modifier hello IP privé adresse arrière toohello d’origine si vous le souhaitez. Sinon, vous pouvez conserver cette adresse. 

### <a name="for-vms-deployed-in-resource-group-model"></a>Pour les machines virtuelles déployées dans le modèle de groupe de ressources

1.  Accédez toohello [portail Azure]( https://ms.portal.azure.com).
2.  Sélectionnez hello affectées de Machine virtuelle.
3.  Sélectionnez **Interfaces réseau**.
4.  Sélectionnez hello Qu'interface réseau associé à votre ordinateur
5.  Sélectionnez **Configurations IP**.
6.  Sélectionnez adresse IP de hello. 
7.  Si hello **l’attribution IP privé** n’est pas **statique**, modifiez-le trop**statique**.
8.  Hello de modification **adresse IP** tooanother adresse IP disponible dans hello sous-réseau.
9. machine virtuelle de Hello redémarre tooinitialize hello nouveau NIC toohello système.
10. Essayez tooRDP tooyour machine. En cas de réussite, vous pouvez modifier hello IP privé adresse arrière toohello d’origine si vous le souhaitez. Sinon, vous pouvez conserver cette adresse. 

## <a name="delete-hello-unavailable-nics"></a>Supprimer hello cartes réseau non disponible
Une fois que vous pouvez les ordinateur toohello Bureau à distance, vous devez supprimer le problème potentiel de hello anciennes cartes réseau tooavoid hello :

1.  Ouvrez le Gestionnaire de périphériques.
2.  Sélectionnez **Afficher** > **Afficher les périphériques cachés**.
3.  Sélectionnez **Adaptateurs réseau**. 
4.  Rechercher les cartes de hello nommés en tant que « Carte de réseau Microsoft Hyper-V ».
5.  Il se peut qu’un adaptateur non disponible apparaisse grisé. L’adaptateur hello d’avec le bouton droit, puis sélectionnez Désinstaller.

    ![image Hello Hello NIC](media/reset-network-interface/nicpage.png)

    > [!NOTE]
    > Désinstaller uniquement les adaptateurs indisponible hello qui portent le nom hello « Carte de réseau Microsoft Hyper-V ». Si vous désinstallez des hello autres adaptateurs masquées, elle peut entraîner des problèmes supplémentaires.
    >
    >

6.  À présent, tous les adaptateurs indisponibles ont normalement été nettoyés sur votre système.