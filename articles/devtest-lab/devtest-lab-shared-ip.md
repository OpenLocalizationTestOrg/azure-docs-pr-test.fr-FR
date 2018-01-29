---
title: "Comprendre les adresses IP partagées dans Azure DevTest Labs | Microsoft Docs"
description: "Découvrez comment Azure DevTest Labs utilise les adresses IP partagées afin de limiter les adresses IP publiques requises pour accéder aux machines virtuelles de votre laboratoire."
services: devtest-lab
documentationcenter: na
author: craigcaseyMSFT
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: v-craic
ms.openlocfilehash: 921db397a9a30a102d47d5e6c379e98daba6e5c5
ms.sourcegitcommit: 85012dbead7879f1f6c2965daa61302eb78bd366
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/02/2018
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a>Comprendre les adresses IP partagées dans Azure DevTest Labs

Azure DevTest Labs permet aux machines virtuelles de laboratoire de partager la même adresse IP publique afin de limiter le nombre d’adresses IP publiques requises pour accéder aux machines virtuelles de votre laboratoire individuel.  Cet article décrit le fonctionnement des adresses IP partagées et les options de configuration qui leur sont associées.

## <a name="shared-ip-setting"></a>Paramètre d’adresse IP partagée

Lorsque vous créez un laboratoire, il se trouve dans un sous-réseau de réseau virtuel.  Par défaut, ce sous-réseau est créé avec le paramètre **Enable shared public IP** (Activer l’adresse IP publique partagée) défini sur *Oui*.  Cette configuration crée une adresse IP publique pour le sous-réseau dans son ensemble.  Pour plus d’informations sur la configuration des réseaux virtuels et des sous-réseaux, consultez [Configurer un réseau virtuel dans Azure DevTest Labs](devtest-lab-configure-vnet.md).

![Nouveau sous-réseau de laboratoire](media/devtest-lab-shared-ip/lab-subnet.png)

Pour les laboratoires existants, vous pouvez activer cette option en sélectionnant **Configuration et stratégies > réseaux virtuels**. Puis, sélectionnez un réseau virtuel dans la liste et choisissez **ACTIVER L’ADRESSE IP PUBLIQUE PARTAGÉE** pour un sous-réseau sélectionné. Vous pouvez également désactiver cette option dans un laboratoire si vous ne souhaitez pas partager une adresse IP publique entre les machines virtuelles du laboratoire.

Les machines virtuelles créées dans ce laboratoire utilisent par défaut une adresse IP partagée.  Lorsque vous créez la machine virtuelle, ce paramètre peut être observé dans le panneau **Paramètres avancés** sous **Configuration de l’adresse IP**.

![Nouvelle machine virtuelle](media/devtest-lab-shared-ip/new-vm.png)

- **Partagé :** toutes les machines virtuelles créées en mode **Partagé** sont placées dans un groupe de ressources (GR). Une seule adresse IP est affectée à ce GR et toutes les machines virtuelles de ce GR utilisent cette adresse IP.
- **Public :** chaque machine virtuelle que vous créez possède sa propre adresse IP et est créée dans son propre groupe de ressources.
- **Privé :** chaque machine virtuelle que vous créez utilise une adresse IP privée. Vous ne pourrez pas vous connecter directement à cette machine virtuelle depuis Internet avec le bureau à distance.

Chaque fois qu’une machine virtuelle dotée une adresse IP partagée activée est ajoutée au sous-réseau, DevTest Labs ajoute automatiquement la machine virtuelle à un équilibreur de charge et attribue un numéro de port TCP à l’adresse IP publique, pour le transfert vers le port RDP sur la machine virtuelle.  

## <a name="using-the-shared-ip"></a>Utilisation de l’adresse IP partagée

- **Utilisateurs Linux :** SSH vers la machine virtuelle à l’aide de l’adresse IP ou du nom de domaine complet, suivis du signe deux-points et du port. Par exemple, dans l’image ci-dessous, l’adresse RDP pour se connecter à la machine virtuelle est `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.

  ![Exemple de machine virtuelle](media/devtest-lab-shared-ip/vm-info.png)

- **Utilisateurs Windows :** sélectionnez **Se connecter** sur le portail Azure pour télécharger un fichier RDP préconfiguré et accéder à la machine virtuelle.

## <a name="next-steps"></a>étapes suivantes

* [Définir des stratégies de laboratoire dans Azure DevTest Labs](devtest-lab-set-lab-policy.md)
* [Configuration d’un réseau virtuel dans Azure DevTest Labs](devtest-lab-configure-vnet.md)





