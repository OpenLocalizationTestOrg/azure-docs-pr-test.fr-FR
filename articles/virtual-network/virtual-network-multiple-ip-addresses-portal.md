---
title: "Plusieurs adresses IP pour les machines virtuelles Azure - Portail | Microsoft Docs"
description: "Affecter plusieurs adresses IP à une machine virtuelle à l’aide du portail Azure | Resource Manager"
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
ms.openlocfilehash: d264bd47d76db8015a64f09248c57c94572e2693
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-the-azure-portal"></a>Affecter plusieurs adresses IP à une machine virtuelle à l’aide du portail Azure

>[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]
>
Cet article explique comment créer une machine virtuelle dans le modèle de déploiement Azure Resource Manager à l’aide du portail Azure. Il n’est pas possible d’affecter plusieurs adresses IP à des ressources créées à l’aide du modèle de déploiement classique. Pour en savoir plus sur les modèles de déploiement Azure, voir [Comprendre les modèles de déploiement](../resource-manager-deployment-model.md).

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Créer une machine virtuelle avec plusieurs adresses IP

Si vous souhaitez créer une machine virtuelle avec plusieurs adresses IP ou une adresse IP privée statique, vous devez utiliser PowerShell ou l’interface Azure CLI. Pour savoir comment procéder, cliquez sur l’option relative à PowerShell ou à Azure CLI dans la zone située en haut de cet article. Vous pouvez utiliser le portail pour créer une machine virtuelle avec une seule adresse IP publique statique et (éventuellement) une seule adresse IP publique. Pour cela, suivez les étapes décrites dans l’article [Créer votre première machine virtuelle Windows dans le portail Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md) ou [Création d’une machine virtuelle Linux sur Azure à l’aide du portail](../virtual-machines/linux/quick-create-portal.md). Une fois la machine virtuelle créée, vous pouvez modifier les types d’adresse IP de dynamique à statique et ajouter d’autres adresses à l’aide du portail, en suivant les étapes de la section [Ajouter des adresses IP à une machine virtuelle](#add) du présent article.

## <a name="add"></a>Ajouter des adresses IP à une machine virtuelle

Vous pouvez ajouter des adresses IP privées et publiques à une carte réseau en suivant les étapes décrites ci-après. Les exemples fournis dans les sections suivantes supposent que vous disposez déjà d’une machine virtuelle avec les trois configurations IP décrites dans le [scénario](#Scenario) de cet article, mais ce n’est pas une condition obligatoire.

### <a name="coreadd"></a>Étapes de base

1. Accédez au portail Azure en saisissant l’adresse https://portal.azure.com. Connectez-vous, si nécessaire.
2. Dans le portail, cliquez sur **Plus de services**, puis saisissez *Machines virtuelles* dans la zone de filtre et cliquez sur **Machines virtuelles**.
3. Dans le panneau **Machines virtuelles**, cliquez sur la machine virtuelle à laquelle ajouter des adresses IP. Dans le panneau qui s’affiche, cliquez sur **Interfaces réseau** et sélectionnez l’interface réseau à laquelle ajouter les adresses IP. Dans l’exemple illustré dans l’image suivante, la carte réseau nommée *myNIC* associée à la machine virtuelle *myVM* est sélectionnée :

    ![Interface réseau](./media/virtual-network-multiple-ip-addresses-portal/figure1.png)

4. Dans le panneau affichant la carte réseau que vous avez sélectionnée, cliquez sur **Configurations IP**.

Effectuez les étapes décrites dans l’une des sections qui suivent, selon le type d’adresse IP que vous souhaitez ajouter.

### <a name="add-a-private-ip-address"></a>**Ajouter une adresse IP privée**

Procédez comme suit pour ajouter une nouvelle adresse IP privée :

1. Suivez les étapes de la section [Étapes de base](#coreadd) du présent article.
2. Cliquez sur **Ajouter**. Dans le panneau **Ajouter une configuration IP** qui s’affiche, créez une configuration IP appelée *IPConfig-4*, en lui associant l’adresse *10.0.0.7* à titre d’adresse IP privée *statique*, puis cliquez sur **OK**.

    > [!NOTE]
    > Lorsque vous ajoutez une adresse IP statique, vous devez spécifier une adresse valide, non utilisée, sur le sous-réseau auquel la carte réseau est connectée. Si l’adresse IP que vous sélectionnez n’est pas disponible, le portail lui associe une croix et vous devez en choisir une autre.

3. Lorsque vous cliquez sur OK, le panneau se ferme et la liste des nouvelles configurations IP s’affiche. Cliquez sur **OK** pour fermer le panneau **Ajouter une configuration IP**.
4. Vous pouvez cliquer sur **Ajouter** pour ajouter des configurations IP supplémentaires, ou fermer tous les panneaux ouverts pour terminer l’ajout d’adresses IP.
5. Ajoutez les adresses IP privées dans le système d’exploitation de la machine virtuelle en suivant les étapes relatives à ce système décrites dans la section [Ajouter des adresses IP à un système d’exploitation de machine virtuelle](#os-config) du présent article.

### <a name="add-a-public-ip-address"></a>Ajouter une adresse IP publique

Vous ajoutez une adresse IP publique en associant une ressource d’adresse IP publique à une configuration IP nouvelle ou existante.

> [!NOTE]
> Les adresses IP publiques ont un coût nominal. Pour en savoir plus, lisez la page [Tarification des adresses IP](https://azure.microsoft.com/pricing/details/ip-addresses) . Il existe une limite au nombre d’adresses IP publiques qui peuvent être utilisées dans un abonnement. Pour plus d’informations sur les limites, voir [Limites d’Azure](../azure-subscription-service-limits.md#networking-limits).
> 

### <a name="create-public-ip"></a>Créer une ressource d’adresse IP publique

Une adresse IP publique correspond à un paramètre de configuration d’une ressource d’adresse IP publique. Si vous disposez d’une ressource d’adresse IP publique qui n’est pas actuellement associée à une configuration IP, effectuez cette opération en ignorant la procédure ci-après, et appliquez les étapes décrites dans l’une des sections qui suivent, le cas échéant. Si aucune ressource d’adresse IP publique n’est disponible, procédez comme suit pour en créer une :

1. Accédez au portail Azure en saisissant l’adresse https://portal.azure.com. Connectez-vous, si nécessaire.
3. Dans le portail, cliquez sur **Nouveau** > **Mise en réseau** > **Adresse IP publique**.
4. Dans le panneau **Créer une adresse IP publique** qui s’affiche, indiquez un nom dans le champ **Nom**, sélectionnez une valeur dans les champs **Affectation d’adresses IP**, **Abonnement**, **Groupe de ressources** et **Emplacement**, puis cliquez sur **Créer**, comme indiqué dans l’image suivante :

    ![Créer une ressource d’adresse IP publique](./media/virtual-network-multiple-ip-addresses-portal/figure5.png)

5. Effectuez les étapes décrites dans l’une des sections qui suivent pour associer la ressource d’adresse IP publique à une configuration IP.

#### <a name="associate-the-public-ip-address-resource-to-a-new-ip-configuration"></a>Associer la ressource d’adresse IP publique à une nouvelle configuration IP

1. Suivez les étapes de la section [Étapes de base](#coreadd) du présent article.
2. Cliquez sur **Ajouter**. Dans le panneau **Ajouter une configuration IP** qui s’affiche, créez une configuration IP nommée *IPConfig-4*. Activez la case à cocher **Adresse IP publique** et choisissez une ressource d’adresse IP publique disponible dans le panneau **Choisir une adresse IP publique** qui s’affiche.

    Une fois que vous avez sélectionné la ressource d’adresse IP publique, cliquez sur **OK**. Le panneau se ferme. Le cas échéant, vous pouvez créer une adresse IP publique en suivant la procédure de la section [Créer une ressource d’adresse IP publique](#create-public-ip) du présent article. 

3. Passez en revue la nouvelle configuration IP. Même si aucune adresse IP privée n’a été explicitement affectée, une adresse de ce type a été automatiquement affectée à la configuration IP, car toutes les configurations IP doivent avoir une adresse IP privée.
4. Vous pouvez cliquer sur **Ajouter** pour ajouter des configurations IP supplémentaires, ou fermer tous les panneaux ouverts pour terminer l’ajout d’adresses IP.
5. Ajoutez l’adresse IP privée dans le système d’exploitation de la machine virtuelle en suivant les étapes relatives à ce système décrites dans la section [Ajouter des adresses IP à un système d’exploitation de machine virtuelle](#os-config) du présent article. N’ajoutez pas l’adresse IP publique dans le système d’exploitation.

#### <a name="associate-the-public-ip-address-resource-to-an-existing-ip-configuration"></a>Associer la ressource d’adresse IP publique à une configuration IP existante

1. Suivez les étapes de la section [Étapes de base](#coreadd) du présent article.
2. Cliquez sur la configuration IP à laquelle vous souhaitez ajouter la ressource d’adresse IP publique.
3. Dans le panneau IPConfig qui s’affiche, cliquez sur **Adresse IP**.
4. Dans le panneau **Choisir une adresse IP publique** qui apparaît, sélectionnez une adresse IP publique.
5. Cliquez sur **Enregistrer** : les panneaux se ferment. Le cas échéant, vous pouvez créer une adresse IP publique en suivant la procédure de la section [Créer une ressource d’adresse IP publique](#create-public-ip) du présent article.
3. Passez en revue la nouvelle configuration IP.
4. Vous pouvez cliquer sur **Ajouter** pour ajouter des configurations IP supplémentaires, ou fermer tous les panneaux ouverts pour terminer l’ajout d’adresses IP. N’ajoutez pas l’adresse IP publique dans le système d’exploitation.


[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
