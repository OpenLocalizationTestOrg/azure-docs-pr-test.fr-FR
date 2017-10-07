---
title: "les adresses IP privées aaaConfigure pour les machines virtuelles - portail Azure | Documents Microsoft"
description: "Découvrez comment les adresses IP privées tooconfigure pour les ordinateurs virtuels à l’aide de hello portail Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a>Configurer des adresses IP privées pour un ordinateur virtuel à l’aide de hello portail Azure

> [!div class="op_single_selector"]
> * [Portail Azure](virtual-networks-static-private-ip-arm-pportal.md)
> * [PowerShell](virtual-networks-static-private-ip-arm-ps.md)
> * [interface de ligne de commande Azure](virtual-networks-static-private-ip-arm-cli.md)
> * [Portail Azure (classique)](virtual-networks-static-private-ip-classic-pportal.md)
> * [PowerShell (classique)](virtual-networks-static-private-ip-classic-ps.md)
> * [Interface de ligne de commande Azure (classique)](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello. Vous pouvez également [gérer une adresse IP privée statique dans le modèle de déploiement classique hello](virtual-networks-static-private-ip-classic-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

étapes d’exemple Hello ci-dessous s’attendre à un environnement simple déjà créé. Si vous souhaitez que les étapes de hello toorun car elles sont affichées dans ce document, tout d’abord créer d’environnement de test hello décrit dans [créer un réseau virtuel](virtual-networks-create-vnet-arm-pportal.md).

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a>Comment les adresses toocreate une machine virtuelle pour tester l’adresse IP privée statique
Impossible de définir une adresse IP privée statique lors de la création de hello d’une machine virtuelle en mode de déploiement du Gestionnaire de ressources hello à l’aide de hello portail Azure. Vous devez d’abord créer hello VM, quantité définie son toobe IP privée statique.

toocreate un ordinateur virtuel nommé *DNS01* Bonjour *frontal* sous-réseau d’un réseau virtuel nommé *TestVNet*, suivez les étapes de hello ci-dessous.

1. À partir d’un navigateur, accédez à toohttp://portal.azure.com et, si nécessaire, connectez-vous avec votre compte Azure.
2. Cliquez sur **nouveau** > **de calcul** > **Windows Server 2012 R2 Datacenter**, notez que hello **sélectionner un modèle de déploiement** liste déjà indique **le Gestionnaire de ressources**, puis cliquez sur **créer**, comme indiqué dans la figure ci-dessous hello.
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. Bonjour **notions de base** panneau, entrez le nom hello de hello toobe de machine virtuelle créée (*DNS01* dans notre scénario), hello compte d’administrateur local et le mot de passe, comme indiqué dans la figure ci-dessous hello.
   
    ![Panneau Informations de base](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. Vérifiez que hello **emplacement** sélectionné est *du centre des États-Unis*, puis cliquez sur **sélectionnez existante** sous **groupe de ressources**, puis cliquez sur **Groupe de ressources** , puis cliquez sur *TestRG*, puis cliquez sur **OK**.
   
    ![Panneau Informations de base](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. Bonjour **choisir une taille** panneau, sélectionnez **A1 Standard**, puis cliquez sur **sélectionnez**.
   
    ![Panneau Choisir une taille](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. Dans le **paramètres** panneau, assurez-vous de hello que propriétés suivantes sont définies sont définis avec des valeurs hello ci-dessous, puis cliquez sur **OK**.
   
    -**Compte de stockage**: *vnetstorage*
   
   * **Réseau**: *TestVNet*
   * **Sous-réseau**: *FrontEnd*
     
     ![Panneau Choisir une taille](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. Bonjour **Résumé** panneau, cliquez sur **OK**. Avis hello vignette ci-dessous affichée dans votre tableau de bord.
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Comment informations pour une machine virtuelle d’adresse IP privée statique de tooretrieve
tooview hello statique privées informations d’adresse IP pour hello machine virtuelle créée avec les étapes de hello ci-dessus, exécutez les étapes de hello ci-dessous.

1. À partir du portail d’Azure Azure hello, cliquez sur **parcourir tous les** > **virtuels** > **DNS01** > **toutes les paramètres** > **interfaces réseau** , puis cliquez sur l’interface réseau uniquement hello répertorié.
   
    ![Déploiement d’une vignette de machine virtuelle](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. Bonjour **interface réseau** panneau, cliquez sur **tous les paramètres** > **des adresses IP** et avis hello **affectation** et **Adresse IP** valeurs.
   
    ![Déploiement d’une vignette de machine virtuelle](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Comment tooadd une adresse IP privée statique d’adresses tooan existant de machine virtuelle
tooadd un toohello d’adresse IP privée statique machine virtuelle créée à l’aide des étapes de hello ci-dessus, suivez les étapes de hello ci-dessous :

1. À partir de hello **des adresses IP** panneau illustrée ci-dessus, cliquez sur **statique** sous **affectation**.
2. Tapez *192.168.1.101* dans **Adresse IP**, puis cliquez sur **Enregistrer**.
   
    ![Création d'une machine virtuelle dans le portail Azure](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> Si, après avoir en cliquant sur **enregistrer** vous remarquez que l’attribution hello est toujours définie trop**dynamique**, cela signifie qu’adresse hello vous avez tapé est déjà en cours d’utilisation. Essayez une autre adresse IP.
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Comment tooremove une privée d’adresses IP statiques à partir d’une machine virtuelle
tooremove hello adresse IP privée statique à partir de hello machine virtuelle créée ci-dessus, effectuez hello suivant l’étape :

À partir de hello **des adresses IP** panneau illustrée ci-dessus, cliquez sur **dynamique** sous **affectation**, puis cliquez sur **enregistrer**.

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur les [adresses IP publiques réservées](virtual-networks-reserved-public-ip.md) .
* En savoir plus sur les [adresses IP publiques de niveau d’instance](virtual-networks-instance-level-public-ip.md) .
* Consultez hello [API REST de IP réservée](https://msdn.microsoft.com/library/azure/dn722420.aspx).

