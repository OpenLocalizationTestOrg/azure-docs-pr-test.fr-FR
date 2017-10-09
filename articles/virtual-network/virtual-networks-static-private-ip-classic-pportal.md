---
title: "les adresses IP privées aaaConfigure pour les machines virtuelles (classiques) - portail Azure | Documents Microsoft"
description: "Découvrez comment les adresses IP privées tooconfigure pour les machines virtuelles (classiques) à l’aide de hello portail Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a>Configurer des adresses IP privées pour une machine virtuelle (classique) à l’aide de hello portail Azure

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Cet article décrit le modèle de déploiement classique hello. Vous pouvez également [gérer une adresse IP privée statique dans le modèle de déploiement du Gestionnaire de ressources hello](virtual-networks-static-private-ip-arm-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

étapes d’exemple Hello ci-dessous s’attendre à un environnement simple déjà créé. Si vous souhaitez que les étapes de hello toorun car elles sont affichées dans ce document, tout d’abord créer d’environnement de test hello décrit dans [créer un réseau virtuel](virtual-networks-create-vnet-classic-pportal.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Comment toospecify une adresse IP privée statique d’adresses lorsque vous créez une machine virtuelle
toocreate un ordinateur virtuel nommé *DNS01* Bonjour *frontal* sous-réseau d’un réseau virtuel nommé *TestVNet* avec une adresse IP privée statique de *192.168.1.101*, Suivez les étapes de hello ci-dessous :

1. À partir d’un navigateur, accédez à toohttp://portal.azure.com et, si nécessaire, connectez-vous avec votre compte Azure.
2. Cliquez sur **nouveau** > **de calcul** > **Windows Server 2012 R2 Datacenter**, notez que hello **sélectionner un modèle de déploiement** liste déjà indique **classique**, puis cliquez sur **créer**.
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. Bonjour **créer un ordinateur virtuel** panneau, entrez le nom hello de hello toobe de machine virtuelle créée (*DNS01* dans notre scénario), hello compte d’administrateur local et le mot de passe.
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. Cliquez sur **Configuration facultative** > **Réseau** > **Réseau virtuel**, puis sur **TestVNet**. Si **TestVNet** n’est pas disponible, assurez-vous que vous utilisez hello *du centre des États-Unis* emplacement et vous avez créé l’environnement de test de hello décrit au début de hello de cet article.
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. Bonjour **réseau** panneau, vérifiez le sous-réseau hello qu’actuellement sélectionné est *frontal*, puis cliquez sur **des adresses IP**, sous **l’attributiond’adressesIP** cliquez sur **statique**, puis entrez *192.168.1.101* pour **adresse IP** comme indiqué ci-dessous.
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. Cliquez sur **OK** Bonjour **des adresses IP** panneau, puis cliquez sur **OK** Bonjour **réseau** panneau, puis cliquez sur **OK**Bonjour **configuration facultative** panneau.
7. Bonjour **créer un ordinateur virtuel** panneau, cliquez sur **créer**. Avis hello vignette ci-dessous affichée dans votre tableau de bord.
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Comment informations pour une machine virtuelle d’adresse IP privée statique de tooretrieve
tooview hello statique privées informations d’adresse IP pour hello machine virtuelle créée avec les étapes de hello ci-dessus, exécutez les étapes de hello ci-dessous.

1. À partir du portail d’Azure Azure hello, cliquez sur **parcourir tous les** > **machines virtuelles (classiques)** > **DNS01**  >   **Tous les paramètres** > **des adresses IP** et notez hello attribution d’adresses IP et l’adresse IP, comme indiqué ci-dessous.
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Comment tooremove une privée d’adresses IP statiques à partir d’une machine virtuelle
tooremove hello adresse IP privée statique à partir de hello machine virtuelle créée ci-dessus, suivez les étapes de hello ci-dessous.

1. À partir de hello **des adresses IP** panneau illustrée ci-dessus, cliquez sur **dynamique** toohello à droite de **attribution d’adresses IP**, puis cliquez sur **enregistrer**, puis Cliquez sur **Oui**.
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Comment tooadd une adresse IP privée statique d’adresses tooan existant de machine virtuelle
tooadd un toohello d’adresse IP privée statique machine virtuelle créée à l’aide des étapes de hello ci-dessus, suivez les étapes de hello ci-dessous :

1. À partir de hello **des adresses IP** panneau illustrée ci-dessus, cliquez sur **statique** toohello à droite de **l’attribution d’adresses IP**.
2. Tapez *192.168.1.101* pour **Adresse IP**, puis cliquez sur **Enregistrer** et sur **Oui**.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur les [adresses IP publiques réservées](virtual-networks-reserved-public-ip.md) .
* En savoir plus sur les [adresses IP publiques de niveau d’instance](virtual-networks-instance-level-public-ip.md) .
* Consultez hello [API REST de IP réservée](https://msdn.microsoft.com/library/azure/dn722420.aspx).

