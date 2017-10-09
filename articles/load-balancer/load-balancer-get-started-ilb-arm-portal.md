---
title: "aaaCreate un équilibreur de charge interne - portail Azure | Documents Microsoft"
description: "Découvrez comment toocreate un interne l’équilibrage de charge dans le Gestionnaire de ressources à l’aide de hello portail Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ac14fb9-8d14-4892-bfe6-8bc74c48ae2c
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 80124217a84857b542eb41cb814ec97234176dd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-in-hello-azure-portal"></a>Créer un équilibreur de charge interne Bonjour portail Azure

> [!div class="op_single_selector"]
> * [portail Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [Interface de ligne de commande Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Modèle](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).  Cet article couvre l’utilisation de modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu de hello [modèle de déploiement classique](load-balancer-get-started-ilb-classic-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="get-started-creating-an-internal-load-balancer-using-azure-portal"></a>Prise en main de la création d’un équilibreur de charge interne avec le portail Azure

Utilisez hello suivant les étapes toocreate un équilibreur de charge interne dans hello portail Azure.

1. Ouvrez un navigateur, accédez toohello [portail Azure](http://portal.azure.com)et connectez-vous avec votre compte Azure.
2. Hello du côté supérieur gauche de l’écran hello, cliquez sur **nouveau** > **réseau** > **équilibrage de charge**.
3. Bonjour **équilibrage de charge créer** panneau, entrez un **nom** pour votre équilibreur de charge.
4. Sous **Schéma**, cliquez sur **Interne**.
5. Cliquez sur **réseau virtuel**, et puis sélectionnez hello réseau virtuel où vous souhaitez l’équilibrage de charge toocreate hello.

   > [!NOTE]
   > Si vous ne voyez pas le réseau virtuel de hello à toouse, vérifiez hello **emplacement** vous utilisez pour l’équilibrage de charge hello et modifiez-le en conséquence.

6. Cliquez sur **sous-réseau**, puis sélectionnez le sous-réseau hello où vous souhaitez l’équilibrage de charge toocreate hello.
7. Sous **l’attribution d’adresses IP**, cliquez sur **dynamique** ou **statique**, selon que vous souhaitez adresse hello pour hello charge équilibrage toobe fixe (statique) ou non.

   > [!NOTE]
   > Si vous sélectionnez toouse une adresse IP statique, vous devez tooprovide une adresse pour l’équilibrage de charge hello.

8. Sous **groupe de ressources** spécifier nom hello d’un nouveau groupe de ressources pour l’équilibrage de charge hello, ou cliquez sur **sélectionnez existante** et sélectionnez un groupe de ressources existant.
9. Cliquez sur **Créer**.

## <a name="configure-load-balancing-rules"></a>Configuration des règles d’équilibrage de la charge

Après hello création de l’équilibrage de charge, accédez tooconfigure de ressource de programme d’équilibrage de charge toohello il.
Vous devez tooconfigure tout d’abord un pool d’adresses de serveur principal et d’une sonde avant de configurer une règle d’équilibrage de charge.

### <a name="step-1-configure-a-back-end-pool"></a>Étape 1 : Configurer un pool principal

1. Bonjour portail Azure, cliquez sur **Parcourir** > **équilibrages de charge**, puis cliquez sur équilibrage de charge hello vous avez créé précédemment.
2. Bonjour **paramètres** panneau, cliquez sur **pools principaux**.
3. Bonjour **pools d’adresses principaux** panneau, cliquez sur **ajouter**.
4. Bonjour **ajouter le pool principal** panneau, entrez un **nom** de pool hello du serveur principal, puis cliquez sur **OK**.

### <a name="step-2-configure-a-probe"></a>Étape 2 : Configurer une sonde

1. Bonjour portail Azure, cliquez sur **Parcourir** > **équilibrages de charge**, puis cliquez sur équilibrage de charge hello vous avez créé précédemment.
2. Bonjour **paramètres** panneau, cliquez sur **sondes**.
3. Bonjour **sondes** panneau, cliquez sur **ajouter**.
4. Bonjour **ajouter sonde** panneau, entrez un **nom** pour la sonde de hello.
5. Sous **Protocole**, sélectionnez **HTTP** (pour les sites web) ou **TCP** (pour les autres applications basées sur TCP).
6. Sous **Port**, spécifiez hello port toouse lors de l’accès de sonde de hello.
7. Sous **chemin d’accès** (pour HTTP sondes uniquement), spécifiez toouse de chemin d’accès hello comme une sonde.
8. Sous **intervalle** spécifier la fréquence à laquelle tooprobe hello application.
9. Sous **seuil défaillance**, spécifiez le nombre de tentatives doivent échouer avant que la machine virtuelle de serveur principal hello est marqué comme étant défectueux.
10. Cliquez sur **OK** toocreate sonde.

### <a name="step-3-configure-load-balancing-rules"></a>Étape 3 : Configurer les règles d’équilibrage de charge

1. Bonjour portail Azure, cliquez sur **Parcourir** > **équilibrages de charge**, puis cliquez sur équilibrage de charge hello vous avez créé précédemment.
2. Bonjour **paramètres** panneau, cliquez sur **règles d’équilibrage de charge**.
3. Bonjour **règles d’équilibrage de charge** panneau, cliquez sur **ajouter**.
4. Bonjour **règle d’équilibrage ajouter** panneau, entrez un **nom** pour la règle de hello.
5. Sous **Protocole**, sélectionnez **HTTP** (pour les sites web) ou **TCP** (pour les autres applications basées sur TCP).
6. Sous **Port**, spécifiez les clients du port hello connectent à équilibrage de charge tooin hello.
7. Sous **port principal**, spécifiez hello port toobe est utilisé dans le pool principal hello (en règle générale, port d’équilibrage de charge hello et port du serveur principal hello sont hello même).
8. Sous **pool principal**, sélectionnez hello principal pool que vous avez créé précédemment.
9. Sous **persistance de Session**, sélectionnez la façon dont vous souhaitez que les sessions toopersist.
10. Sous **délai d’inactivité (minutes)**, spécifiez le délai d’inactivité de hello.
11. Sous **Adresse IP flottante (retour serveur direct)**, cliquez sur **Désactivé** ou **Activé**.
12. Cliquez sur **OK**.

## <a name="next-steps"></a>Étapes suivantes

[Configuration d'un mode de distribution d'équilibrage de charge](load-balancer-distribution-mode.md)

[Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)

