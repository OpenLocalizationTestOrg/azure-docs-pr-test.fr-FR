---
title: "équilibrage de charge aaaCreate une côté Internet - portail Azure classic | Documents Microsoft"
description: "Découvrez comment toocreate un équilibrage de charge exposés à Internet à l’aide de modèle de déploiement classique hello portail Azure classic"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: fa3e93c0-968a-472d-a17c-65665c050db2
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 27b0d5af6e7b493fa94a9dfbfa260483ae95a2fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-classic-portal"></a>Commencer à créer un Internet faisant face à l’équilibrage de charge (classiques) Bonjour portail Azure classic

> [!div class="op_single_selector"]
> * [portail Azure Classic](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [Interface de ligne de commande Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Azure Cloud Services](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Avant d’utiliser des ressources Azure, il est important toounderstand que Azure dispose actuellement de deux modèles de déploiement : le Gestionnaire de ressources Azure et classique. Veillez à bien comprendre les [modèles et outils de déploiement](../azure-classic-rm.md) avant d’utiliser une ressource Azure. Vous pouvez afficher la documentation hello pour différents outils en cliquant sur les onglets hello haut hello de cet article. Cet article décrit le modèle de déploiement classique hello. Vous pouvez également [apprendre comment toocreate une connecté à Internet l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-an-internet-facing-load-balancer-for-virtual-machines"></a>Configurer un équilibrage de charge accessible sur Internet pour les machines virtuelles

Dans l’ordre tooload équilibrer le trafic réseau à partir de hello Internet entre les machines virtuelles de hello d’un service cloud, vous devez créer un jeu d’équilibrage de charge. Cette procédure suppose que vous avez déjà créé des machines virtuelles de hello et qu’ils sont tous dans hello même service cloud.

**tooconfigure un jeu d’équilibrage de la charge pour les machines virtuelles**

1. Bonjour portail Azure classic, cliquez sur **virtuels**, puis cliquez sur nom hello d’un ordinateur virtuel dans le jeu d’équilibrage de charge hello.
2. Cliquez sur **Points de terminaison**, puis sur **Ajouter**.
3. Sur hello **ajouter un ordinateur virtuel de tooa point de terminaison** , cliquez sur la flèche vers la droite hello.
4. Sur hello **spécifier les détails de hello du point de terminaison hello** page :

   * Dans **nom**, tapez un nom pour le point de terminaison hello ou sélectionnez nom de hello dans la liste hello des points de terminaison prédéfinis pour les protocoles communs.
   * Dans **protocole**, sélectionnez le protocole hello requis par type hello du point de terminaison, TCP ou UDP, en fonction des besoins.
   * Dans **les ports Public et privé**, tapez les numéros de port hello souhaité hello toouse de machine virtuelle, en fonction des besoins. Vous pouvez utiliser un port privé hello et les règles de pare-feu sur le trafic tooredirect de machine virtuelle hello d’une manière qui convient à votre application. un port privé Hello peut être hello identique au port public de hello. Par exemple, pour un point de terminaison pour le trafic web (HTTP), vous pouvez affecter 80 tooboth hello publiques et privées voies.

5. Sélectionnez **créer un jeu d’équilibrage de la charge**, puis cliquez sur la flèche vers la droite hello.
6. Sur hello **configurer le jeu d’équilibrage de charge hello** page, tapez un nom pour le jeu d’équilibrage de charge hello, puis assigner des valeurs hello pour le comportement de sonde de hello équilibrage de charge Azure. Hello équilibreur de charge utilise des sondes toodetermine si virtuels hello dans le jeu d’équilibrage de charge hello sont tooreceive disponibles du trafic entrant.
7. Cliquez sur hello coche toocreate hello équilibrée point de terminaison. Vous verrez **Oui** Bonjour **nom de jeu d’équilibrage de charge** colonne Hello **points de terminaison** page pour la machine virtuelle de hello.
8. Dans le portail de hello, cliquez sur **virtuels**, cliquez sur le nom hello d’un ordinateur virtuel supplémentaire dans le jeu d’équilibrage de charge hello **points de terminaison**, puis cliquez sur **ajouter**.
9. Sur hello **ajouter un ordinateur virtuel de tooa point de terminaison** , cliquez sur **ajouter le jeu d’équilibrage de charge existant point de terminaison tooan**, sélectionnez nom hello du jeu d’équilibrage de charge hello, puis cliquez sur la flèche vers la droite hello.
10. Sur hello **spécifier les détails de hello du point de terminaison hello** page, tapez un nom pour le point de terminaison hello, puis cliquez sur la case à cocher hello.

Pour hello autres machines virtuelles dans le jeu d’équilibrage de charge hello, répétez les étapes 8 à 10.

## <a name="next-steps"></a>Étapes suivantes

[Prise en main de la configuration d’un équilibrage de charge interne](load-balancer-get-started-ilb-arm-ps.md)

[Configuration d'un mode de distribution d'équilibrage de charge](load-balancer-distribution-mode.md)

[Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)
