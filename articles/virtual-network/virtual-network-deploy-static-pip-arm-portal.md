---
title: aaaCreate une machine virtuelle avec une adresse IP publique statique - portail Azure | Documents Microsoft
description: "Découvrez comment toocreate une machine virtuelle avec un statique publique adresse IP via hello portail Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74d2132785f06148757409ee0a44b98d1e4b98e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a>Créer une machine virtuelle avec une adresse IP publique statique à l’aide de hello portail Azure

> [!div class="op_single_selector"]
> * [Portail Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Interface de ligne de commande Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [Modèle](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (classique)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu du modèle de déploiement classique hello.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a>Créer une machine virtuelle avec une adresse IP publique statique

toocreate une machine virtuelle avec une adresse IP publique statique d’adresses Bonjour portail Azure, hello complète comme suit :

1. À partir d’un navigateur, accédez à toohello [portail Azure](https://portal.azure.com) et, si nécessaire, connectez-vous à votre compte Azure.
2. Dans hello coin supérieur gauche du portail de hello, cliquez sur **nouveau**>>**de calcul**>**Windows Server 2012 R2 Datacenter**.
3. Bonjour **sélectionner un modèle de déploiement** , sélectionnez **le Gestionnaire de ressources** et cliquez sur **créer**.
4. Bonjour **notions de base** panneau, entrez les informations sur les ordinateurs virtuels hello comme indiqué ci-dessous, puis cliquez sur **OK**.
   
    ![Portail Azure - De base](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. Bonjour **choisir une taille** panneau, cliquez sur **A1 Standard** comme indiqué ci-dessous, puis cliquez sur **sélectionnez**.
   
    ![Portail Azure - Choisir une taille](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. Bonjour **paramètres** panneau, cliquez sur **adresse IP publique**, puis Bonjour **créer une adresse IP publique** panneau, sous **affectation**, cliquez sur **Statique** comme indiqué ci-dessous. Cliquez ensuite sur **OK**.
   
    ![Portail Azure - Créer une adresse IP publique](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. Bonjour **paramètres** panneau, cliquez sur **OK**.
8. Hello de révision **Résumé** panneau, comme illustré ci-dessous, puis cliquez sur **OK**.
   
    ![Portail Azure - Créer une adresse IP publique](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. Notez la nouvelle vignette de hello dans votre tableau de bord.
   
    ![Portail Azure - Créer une adresse IP publique](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. Une fois créé, hello VM hello **paramètres** panneau s’affichera comme indiqué ci-dessous
    
    ![Portail Azure - Créer une adresse IP publique](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

