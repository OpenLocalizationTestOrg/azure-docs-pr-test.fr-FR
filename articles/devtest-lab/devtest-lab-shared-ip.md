---
title: "aaaUnderstand partagé des adresses IP dans Azure DevTest Labs | Documents Microsoft"
description: "Découvrez comment Azure DevTest Labs utilise partagé IP adresses toominimize hello publique IP adresses requis tooaccess votre laboratoire de machines virtuelles."
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a>Comprendre les adresses IP partagées dans Azure DevTest Labs

Lab de permet de Azure DevTest Labs partage des machines virtuelles hello publique IP adresse toominimize hello autant de public tooaccess de requis d’adresses IP de votre laboratoire des machines virtuelles.  Cet article décrit le fonctionnement des adresses IP partagées et les options de configuration qui leur sont associées.

## <a name="shared-ip-setting"></a>Paramètre d’adresse IP partagée

Lorsque vous créez un laboratoire, il se trouve dans un sous-réseau de réseau virtuel.  Par défaut, ce sous-réseau est créé avec **activer partagée d’adresse IP publique** défini trop*Oui*.  Cette configuration crée une adresse IP publique pour le sous-réseau en entier hello.  Pour plus d’informations sur la configuration des réseaux virtuels et des sous-réseaux, consultez [Configurer un réseau virtuel dans Azure DevTest Labs](devtest-lab-configure-vnet.md).

![Nouveau sous-réseau de laboratoire](media/devtest-lab-shared-ip/lab-subnet.png)

Pour les laboratoires existants, vous pouvez activer cette option en sélectionnant **Configuration et stratégies > réseaux virtuels**. Ensuite, sélectionnez un réseau virtuel à partir de la liste de hello et choisissez **activer partagé adresse IP publique** pour un sous-réseau sélectionné. Vous pouvez également désactiver cette option dans un laboratoire si vous ne souhaitez pas tooshare une adresse IP publique entre les ordinateurs virtuels de lab.

Les ordinateurs virtuels créés dans cette toousing par défaut de laboratoire une adresse IP partagée.  Lorsque vous créez hello machine virtuelle, ce paramètre peut être observé dans hello **paramètres avancés** panneau sous **configuration d’adresse IP**.

![Nouvelle machine virtuelle](media/devtest-lab-shared-ip/new-vm.png)

- **Partagé :** toutes les machines virtuelles créées en mode **Partagé** sont placées dans un groupe de ressources (GR). Une seule adresse IP est affectée pour ce groupe de routage et de toutes les machines virtuelles dans hello RG utilisera cette adresse IP.
- **Public :** chaque machine virtuelle que vous créez possède sa propre adresse IP et est créée dans son propre groupe de ressources.
- **Privé :** chaque machine virtuelle que vous créez utilise une adresse IP privée. Vous ne serez pas en mesure de tooconnect toothis machine virtuelle directement à partir de hello internet avec le Bureau à distance.

Chaque fois qu’une machine virtuelle avec l’adresse IP partagée activée est ajoutée toohello sous-réseau, DevTest Labs ajoute l’équilibrage de charge hello VM tooa automatiquement et affecte un numéro de port TCP sur l’adresse IP publique hello transfert toohello port RDP sur hello machine virtuelle.  

## <a name="using-hello-shared-ip"></a>À l’aide de hello partagé IP

- **Les utilisateurs Linux :** SSH toohello machine virtuelle en utilisant l’adresse IP de hello ou nom de domaine complet, suivie du signe deux-points, suivi de port de hello. Par exemple, dans l’image hello ci-dessous, hello RDP adresses toohello tooconnect machine virtuelle est `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.

  ![Exemple de machine virtuelle](media/devtest-lab-shared-ip/vm-info.png)

- **Les utilisateurs Windows :** hello sélectionnez **Connect** bouton un fichier RDP préconfiguré hello toodownload portail Azure et accéder hello machine virtuelle.

## <a name="next-steps"></a>Étapes suivantes

* [Définir des stratégies de laboratoire dans Azure DevTest Labs](devtest-lab-set-lab-policy.md)
* [Configuration d’un réseau virtuel dans Azure DevTest Labs](devtest-lab-configure-vnet.md)





