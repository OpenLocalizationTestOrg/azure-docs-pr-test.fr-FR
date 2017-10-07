---
title: "prise en charge du Gestionnaire de ressources pour l’équilibrage de charge d’aaaAzure | Documents Microsoft"
description: "Utilisation de Powershell pour l’équilibrage de charge avec Azure Resource Manager. Utilisation de modèles pour l'équilibrage de charge"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3c02d9382de00fefe6af8f4f8a2b7b62b344f285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a>Utilisation de la prise en charge d’Azure Resource Manager pour l’équilibrage de charge Azure

Le Gestionnaire de ressources Azure est un framework de gestion préférés hello pour les services dans Azure. Azure Load Balancer peut être géré à l’aide des outils et des API basés sur Azure Resource Manager.

## <a name="concepts"></a>Concepts

Avec le Gestionnaire de ressources, équilibrage de charge Azure contient hello suivant des ressources enfants :

* Configuration d’une adresse IP frontale : un équilibreur de charge peut inclure une ou plusieurs adresses IP frontales, également appelées « adresses IP virtuelles ». Ces adresses IP servent d’entrée pour le trafic de hello.
* Pool d’adresses principal, il s’agit des adresses IP associées machine virtuelle de hello Interface de carte réseau (NIC) toowhich charge sera distribué.
* Règles d’équilibrage de charge – une propriété de règle mappe une adresse IP donnée frontal et le port jeu tooa de combinaison d’adresses IP de serveur principal et combinaison de port. Un même équilibreur de charge peut avoir plusieurs règles d’équilibrage de charge. Chaque règle est une combinaison d’une adresse IP et d’un port frontaux et d’une adresse IP et d’un port principaux associés aux machines virtuelles.
* Sondes – sondes activer vous tookeep suivi d’intégrité hello des instances de machine virtuelle. Si une sonde d’intégrité échoue, instance de machine virtuelle hello est automatiquement mis hors rotation.
* Des règles NAT de trafic entrant – définissant les règles NAT hello entrant qui traversent hello frontal IP et adresse IP de fin toohello distribuée précédent.

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a>Modèles de démarrage rapide

Le Gestionnaire de ressources Azure vous permet de tooprovision vos applications à l’aide d’un modèle déclaratif. Dans un modèle unique, vous pouvez déployer plusieurs services ainsi que leurs dépendances. Vous utilisez hello même modèle toorepeatedly déployer votre application au cours de chaque étape du cycle de vie application hello.

Les modèles peuvent inclure des définitions de machines virtuelles, de réseaux virtuels, de groupes à haute disponibilité, d’interfaces réseau (NIC), de comptes de stockage, d’équilibreurs de charge, de groupes de sécurité réseau et d’adresses IP publiques. Avec des modèles, vous pouvez créer tout ce dont vous avez besoin pour une application complexe. fichier de modèle Hello peut être vérifiée dans le système de gestion de contenu pour le contrôle de version et de collaboration.

[En savoir plus sur les modèles](../azure-resource-manager/resource-manager-template-walkthrough.md)

[En savoir plus sur les ressources de réseau](../virtual-network/resource-groups-networking.md)

Des modèles de démarrage rapide utilisant Azure Load Balancer se trouvent dans un [référentiel GitHub](https://github.com/Azure/azure-quickstart-templates) qui héberge un ensemble de modèles générés par la communauté.

Exemples de modèles :

* [2 machines virtuelles dans un équilibrage de charge et les règles d'équilibrage de charge](http://go.microsoft.com/fwlink/?LinkId=544799)
* [2 machines virtuelles dans un réseau virtuel avec un équilibrage de charge interne et les règles d’équilibrage de charge](http://go.microsoft.com/fwlink/?LinkId=544800)
* [2 machines virtuelles dans un équilibreur de charge et configurer des règles NAT sur hello équilibrage de charge](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a>Configuration de l'équilibrage de charge Azure avec PowerShell ou la CLI

Prise en main des applets de commande, des outils de ligne de commande et des API REST Azure Resource Manager

* [Applets de commande de mise en réseau Azure](https://msdn.microsoft.com/library/azure/mt163510.aspx) peut être utilisé toocreate un équilibreur de charge.
* [Comment toocreate un équilibreur de charge à l’aide du Gestionnaire de ressources Azure](load-balancer-get-started-ilb-arm-ps.md)
* [À l’aide de hello CLI d’Azure avec la gestion des ressources Azure](../xplat-cli-azure-resource-manager.md)
* [API REST de l'équilibrage de charge](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez également [commencer par créer un équilibrage de charge avec accès par Internet](load-balancer-get-started-internet-arm-ps.md) et configurer le type de [mode de distribution](load-balancer-distribution-mode.md) pour un comportement spécifique de trafic réseau d’équilibrage de charge.

Découvrez comment toomanage [les paramètres de délai d’expiration TCP pour un équilibrage de charge des temps d’inactivité](load-balancer-tcp-idle-timeout.md). Ceci est important lorsque votre application doit tookeep connexions actives pour les serveurs situés derrière un équilibreur de charge.
