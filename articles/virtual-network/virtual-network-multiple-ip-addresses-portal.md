---
title: aaaMultiple des adresses IP pour les machines virtuelles - portail | Documents Microsoft
description: "Découvrez comment tooassign des adresses IP multiples à l’aide de machine virtuelle tooa hello portail Azure | Gestionnaire de ressources."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 3a8cae97-3bed-430d-91b3-274696d91e34
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/30/2016
ms.author: annahar
ms.openlocfilehash: 34075766ac68c8de38c258a4d70e35881f28bb0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-portal"></a>Assigner plusieurs ordinateurs de toovirtual d’adresses IP à l’aide de hello portail Azure

>[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]
>
Cet article explique comment toocreate un ordinateur virtuel (VM) l’utilisation de modèle de déploiement Azure Resource Manager hello hello portail Azure. Tooresources créé via le modèle de déploiement classique hello ne peut pas être assignés à plusieurs adresses IP. toolearn plus d’informations sur les modèles de déploiement Azure, lisez hello [comprendre les modèles de déploiement](../resource-manager-deployment-model.md) l’article.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Créer une machine virtuelle avec plusieurs adresses IP

Si vous souhaitez toocreate une machine virtuelle avec plusieurs adresses IP ou une adresse IP privée statique, vous devez le créer à l’aide de PowerShell ou hello CLI d’Azure. Cliquez comment hello PowerShell ou options CLI haut hello toolearn de cet article. Vous pouvez créer une machine virtuelle avec une seule adresse IP privée dynamique et (éventuellement) une seule adresse IP publique à l’aide du portail de hello en suivant les étapes de hello Bonjour [créer une machine virtuelle Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) ou [créer un VM Linux](../virtual-machines/linux/quick-create-portal.md) articles. Après avoir créé la machine virtuelle de hello, vous pouvez modifier le type d’adresse IP hello de toostatic dynamique et ajouter des adresses IP supplémentaires à l’aide du portail de hello en suivant les étapes dans hello [ajouter une adresse IP adresses tooa VM](#add) section de cet article.

## <a name="add"></a>Ajouter tooa d’adresses IP virtuelle

Vous pouvez ajouter privé et public tooa adresses IP réseau en effectuant les étapes hello qui suivent. Bonjour Bonjour les sections suivantes supposent que vous avez déjà une machine virtuelle avec des configurations IP hello trois décrites dans hello [scénario](#Scenario) dans cet article, mais il n’est pas nécessaire de procéder.

### <a name="coreadd"></a>Étapes de base

1. Parcourir toohello portail Azure à https://portal.azure.com et connectez-vous, si nécessaire.
2. Dans le portail de hello, cliquez sur **davantage de services** > type *virtuels* dans hello zone de filtre, puis cliquez sur **machines virtuelles**.
3. Bonjour **virtuels** panneau, cliquez sur hello machine virtuelle que vous souhaitez tooadd IP adresses. Cliquez sur **interfaces réseau** dans Panneau de machine virtuelle hello qui s’affiche et puis sélectionnez hello réseau interface que vous souhaitez tooadd hello IP adresses. Dans l’exemple hello hello suivant image, hello carte réseau nommée *myNIC* de hello ordinateur virtuel nommé *myVM* est sélectionnée :

    ![Interface réseau](./media/virtual-network-multiple-ip-addresses-portal/figure1.png)

4. Dans hello panneau qui s’affiche pour hello carte réseau que vous avez sélectionné, cliquez sur **configurations IP**.

Hello terminé les étapes de l’une des sections hello qui suivent, en fonction de type hello d’adresse IP vous tooadd.

### <a name="add-a-private-ip-address"></a>**Ajouter une adresse IP privée**

Terminer hello suivant les étapes tooadd une nouvelle adresse IP privée :

1. Hello terminé les étapes Bonjour [étapes de base](#coreadd) section de cet article.
2. Cliquez sur **Add**. Bonjour **configuration d’ajouter une adresse IP** panneau qui s’affiche, créez une configuration IP nommée *4-IPConfig* avec *10.0.0.7* comme un *statique* IP privée d’adresses, puis cliquez sur **OK**.

    > [!NOTE]
    > Lorsque vous ajoutez une adresse IP statique, vous devez spécifier une adresse valide inutilisée sur hello de sous-réseau hello à que carte réseau est connectée. Si l’adresse hello choisie n’est pas disponible, portail de hello affiche un X pour l’adresse IP de hello et vous devez tooselect une autre.

3. Une fois que vous cliquez sur OK, panneau de hello se ferme et vous verrez une nouvelle configuration d’IP hello répertoriée. Cliquez sur **OK** tooclose hello **configuration d’ajouter une adresse IP** panneau.
4. Vous pouvez cliquer sur **ajouter** tooadd des configurations IP supplémentaires, ou fermez toutes les adresses IP Ajout de lames toofinish.
5. Système d’exploitation de l’ordinateur virtuel toohello les adresses IP privée de hello ajouter en procédant comme hello pour votre système d’exploitation Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article.

### <a name="add-a-public-ip-address"></a>Ajouter une adresse IP publique

Une adresse IP publique est ajoutée en associant un tooeither de ressource d’adresse IP publique, une nouvelle configuration IP ou une configuration IP existante.

> [!NOTE]
> Les adresses IP publiques ont un coût nominal. toolearn en savoir plus sur le protocole IP adresse tarification, lire hello [tarification d’adresse IP](https://azure.microsoft.com/pricing/details/ip-addresses) page. Il existe un toohello limiter le nombre d’adresses IP publiques qui peut être utilisé dans un abonnement. toolearn plus d’informations sur les limites de hello, lire hello [Azure limite](../azure-subscription-service-limits.md#networking-limits) l’article.
> 

### <a name="create-public-ip"></a>Créer une ressource d’adresse IP publique

Une adresse IP publique correspond à un paramètre de configuration d’une ressource d’adresse IP publique. Si vous avez une ressource d’adresse IP publique qui n’est pas tooan actuellement associé IP configuration de configuration IP de tooan tooassociate, ignorer des hello comme suit et effectuer des étapes de hello dans une des sections hello qui suivent, dont vous avez besoin. Si vous n’avez pas une ressource d’adresse IP publique disponible, terminez hello suivant toocreate étapes une :

1. Parcourir toohello portail Azure à https://portal.azure.com et connectez-vous, si nécessaire.
3. Dans le portail de hello, cliquez sur **nouveau** > **réseau** > **adresse IP publique**.
4. Bonjour **créer une adresse IP publique** panneau qui s’affiche, entrez un **nom**, sélectionnez un **l’attribution d’adresses IP** type, un **abonnement**, un **Groupe de ressources**et un **emplacement**, puis cliquez sur **créer**, comme indiqué dans hello illustration suivante :

    ![Créer une ressource d’adresse IP publique](./media/virtual-network-multiple-ip-addresses-portal/figure5.png)

5. Hello terminé les étapes dans une des sections hello qui suivent tooassociate hello publique ressource tooan IP configuration d’adresse IP.

#### <a name="associate-hello-public-ip-address-resource-tooa-new-ip-configuration"></a>Associer hello publique ressource tooa nouveau IP configuration d’adresse IP

1. Hello terminé les étapes Bonjour [étapes de base](#coreadd) section de cet article.
2. Cliquez sur **Add**. Bonjour **configuration d’ajouter une adresse IP** panneau qui s’affiche, créez une configuration IP nommée *IPConfig-4*. Activer hello **adresse IP publique** et sélectionnez une existante, disponible publique ressource d’adresse IP à partir de hello **choisir une adresse IP publique** panneau s’affiche.

    Une fois que vous avez sélectionné la ressource d’adresse IP publique hello, cliquez sur **OK** et panneau de hello va se fermer. Si vous n’avez pas une adresse IP publique existante, vous pouvez en créer un en procédant comme hello Bonjour [créer une ressource d’adresse IP publique](#create-public-ip) section de cet article. 

3. Révision hello nouveau la configuration IP. Même si une adresse IP privée n’a pas été explicitement affectée, un a été attribué automatiquement la configuration IP de toohello, car toutes les configurations IP doivent avoir une adresse IP privée.
4. Vous pouvez cliquer sur **ajouter** tooadd des configurations IP supplémentaires, ou fermez toutes les adresses IP Ajout de lames toofinish.
5. Ajouter un système de d’exploitation de hello privé IP adresse toohello machine virtuelle en effectuant les étapes hello pour votre système d’exploitation Bonjour [ajouter une adresse IP traite le système d’exploitation de l’ordinateur virtuel tooa](#os-config) section de cet article. N’ajoutez pas hello publique IP adresse toohello système d’exploitation.

#### <a name="associate-hello-public-ip-address-resource-tooan-existing-ip-configuration"></a>Associer hello publique ressource tooan existant IP configuration d’adresse IP

1. Hello terminé les étapes Bonjour [étapes de base](#coreadd) section de cet article.
2. Cliquez sur configuration IP de hello souhaité tooadd hello publique ressource d’adresse IP à.
3. Dans le panneau de IPConfig hello qui s’affiche, cliquez sur **adresse IP**.
4. Bonjour **choisir une adresse IP publique** panneau qui s’affiche, sélectionnez une adresse IP publique.
5. Cliquez sur **enregistrer** et panneaux de hello va se fermer. Si vous n’avez pas une adresse IP publique existante, vous pouvez en créer un en procédant comme hello Bonjour [créer une ressource d’adresse IP publique](#create-public-ip) section de cet article.
3. Révision hello nouveau la configuration IP.
4. Vous pouvez cliquer sur **ajouter** tooadd des configurations IP supplémentaires, ou fermez toutes les adresses IP Ajout de lames toofinish. N’ajoutez pas hello publique IP adresse toohello système d’exploitation.


[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
