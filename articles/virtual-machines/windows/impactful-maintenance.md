---
title: maintenance aaaImpactful pour les machines virtuelles Windows dans Azure | Documents Microsoft
description: Maintenance affectant les machines virtuelles Windows
services: virtual-machines-windows
documentationcenter: 
author: zivr
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: zivr
ms.openlocfilehash: 98afaea0fdca796177e075b33615b03f1e7a0fdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="impactful-maintenance-for-virtual-machines"></a>Maintenance affectant les machines virtuelles

Il existe quelques cas où vos machines virtuelles sont redémarrés en raison de toohello de maintenance tooplanned sous-jacent d’infrastructure. Sa disponibilité toothe impact non négligeable de vos machines virtuelles hébergées dans Azure, hello suivantes sont désormais disponibles pour vous toouse :

-   Notification envoyée au moins 30 jours avant l’impact de hello.

-   Fenêtres de maintenance visibilité toohello par chaque ordinateur virtuel.

-   Flexibilité et contrôle dans la définition de l’heure exacte de hello pour avoir un impact sur vos machines virtuelles de la maintenance.

La maintenance dans Microsoft Azure est planifiée en itérations. Itérations initiales ont la plus petite portée ordre tooreduce hello les risques impliqués dans le déploiement de fonctionnalités et les nouveaux correctifs. Itérations ultérieures peuvent être réparties entre plusieurs régions (jamais de hello même paire de région). Une machine virtuelle est incluse dans une itération de maintenance unique. Si une itération est abandonnée, les machines virtuelles restantes sont incluses dans une future itération.

itération de la maintenance planifiée Hello comprend deux phases : fenêtre de Maintenance Pre-emptive et une fenêtre de Maintenance planifiée.

Hello **fenêtre de Maintenance Pre-emptive** assure la maintenance de hello hello flexibilité tooinitiate sur vos machines virtuelles. En procédant ainsi, vous pouvez déterminer si vos machines virtuelles sont affectés, hello de séquence de mise à jour hello et durée hello entre chaque machine virtuelle en cours de maintenance. Vous pouvez interroger les toosee de chaque machine virtuelle si elle est planifiée pour la maintenance et vérifier les résultats hello de votre dernière demande de maintenance initié.

Hello **fenêtre de Maintenance planifiée** est lorsque Azure a planifié vos machines virtuelles pour la maintenance de hello. Au cours de cette fenêtre de temps, ce qui suit la fenêtre de maintenance préventive, vous pouvez tout de même interroger hello fenêtre de maintenance, mais n’est plus maintenance de hello tooorchestrate en mesure de.

## <a name="availability-considerations-during-planned-maintenance"></a>Considérations relatives à la disponibilité lors de la maintenance planifiée 

### <a name="paired-regions"></a>Régions jumelées

Chaque région Azure est associée à une autre région de hello même geography, créant ainsi une paire régionale. Lors de l’exécution de maintenance, Azure met à jour uniquement les instances de Machine virtuelle hello dans une région de la paire. Par exemple, lors de la mise à jour hello ordinateurs virtuels de l’Amérique du Nord, Azure ne mettra pas à jour les Machines virtuelles dans l’Amérique du Sud à hello même temps. La mise à jour est planifiée à un autre moment, en activant le basculement ou l’équilibrage de charge entre les régions. Toutefois, autres régions comme Europe du Nord peut être en cours de maintenance à hello même temps que les États-Unis.
En savoir plus sur les [paires de régions Azure](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="single-instance-vms-vs-availability-set-or-vm-scale-set"></a>Machines virtuelles à instance unique et groupe à haute disponibilité ou groupe de machines virtuelles identiques

Lors du déploiement d’une charge de travail à l’aide de machines virtuelles dans Azure, vous pouvez créer hello machines virtuelles au sein d’un groupe à haute disponibilité dans l’application tooyour de commandes tooprovide haute disponibilité. Dans une telle configuration, vous avez la garantie qu’au moins une des machines virtuelles sera disponible pendant une panne ou un événement de maintenance.

Au sein d’un ensemble de disponibilité, des ordinateurs virtuels individuels sont réparties sur les domaines de mise à jour too20. Lors de la maintenance planifiée, un seul domaine de mise à jour est affecté à un moment donné. commande Hello de domaines de mise à jour un impact sur les ne peut pas procèdent de manière séquentielle pendant les maintenances planifiées. Pour unique une instance de machines virtuelles (n’appartenant pas à haute disponibilité), il n’existe aucun moyen toopredict ou déterminer quel et le nombre de machines virtuelles sont affectés ensemble.

Machines virtuelles identiques sont une ressource de calcul Azure qui vous permet de toodeploy et gérer un ensemble de machines virtuelles identiques en tant qu’une seule ressource.
ensemble d’échelle Hello fournit des garanties similaires tooan groupe à haute disponibilité dans le formulaire de domaines de mise à jour. 

Pour plus d’informations sur la configuration de vos ordinateurs virtuels pour la haute disponibilité, consultez [ *administrer la disponibilité de vos machines virtuelles de Windows hello des*](../linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="scheduled-events"></a>Événements planifiés

Metadata Service Azure vous permet de toodiscover d’informations sur votre Machine virtuelle hébergée dans Azure. Les événements, une des catégories hello exposée, des informations concernant les événements à venir surfaces planifiés (par exemple, redémarrez) afin que votre application peut préparer et limiter interruption.

Pour plus d’informations sur les événements planifiés, consultez trop[Service de métadonnées Azure - événements planifiés](../virtual-machines-scheduled-events.md).

## <a name="maintenance-discovery-and-notifications"></a>Notifications et détection de maintenance

Planification de maintenance est toocustomers visibles au niveau de hello d’ordinateurs virtuels individuels. Vous pouvez utiliser Azure portal, tooquery API, PowerShell ou CLI pour les fenêtres de maintenance préventive et planifiée. En outre, attendre à recevoir une notification (messagerie) en cas de hello où un (ou plus) de vos ordinateurs virtuels sont affectés au cours du processus de hello.

Les phases de maintenance préemptive et planifiée commencent par une notification. Attendez tooreceive une seule notification par abonnement Azure. notification de Hello est envoyée à l’abonnement toohello admin et co-admin par défaut. Vous pouvez également configurer audience hello pour la notification de maintenance.

### <a name="view-hello-maintenance-window-in-hello-portal"></a>Afficher hello fenêtre de Maintenance dans le portail de hello 

Vous pouvez utiliser hello portail Azure et rechercher des machines virtuelles de la maintenance planifiées.

1.  Se connecter toohello portail Azure.

2.  Cliquez sur et ouvrez hello **virtuels** panneau.

3.  Cliquez sur hello **colonnes** liste hello tooopen de toochoose de colonnes disponibles à partir de

4.  Sélectionnez et ajoutez hello **fenêtre de Maintenance** colonnes. Machines virtuelles qui sont planifiées pour la maintenance ont des fenêtres de maintenance hello exposés. Une fois la maintenance terminée ou abandonnée, la fenêtre de maintenance n’est plus présentée.

### <a name="query-maintenance-details-using-hello-azure-api"></a>Détails de maintenance de requête à l’aide de hello API Azure

Hello d’utilisation [obtenir des informations sur les ordinateurs virtuels API](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) et recherchez hello vue toodiscover hello maintenance détails de l’instance sur une machine virtuelle individuelle. réponse de Hello inclut hello suivant d’éléments :

  - isCustomerInitiatedMaintenanceAllowed : indique si vous pouvez désormais lancer préemptive redéployer sur hello machine virtuelle.

  - preMaintenanceWindowStartTime : hello heure de début de la fenêtre de maintenance préventive hello.

  - preMaintenanceWindowEndTime : hello heure de fin de la fenêtre de maintenance préventive hello. Après cette heure, vous ne pourra plus être maintenance en mesure de tooinitiate sur cet ordinateur virtuel.
    
  - maintenanceWindowStartTime : hello heure de début de fenêtre de maintenance planifiée hello lorsque votre machine virtuelle sont affectés.

  - maintenanceWindowEndTime : hello heure de fin de la fenêtre de maintenance planifiée hello.
  
  - lastOperationResultCode : hello les résultats de votre dernière opération de redéploiement de la Maintenance.
 
  - lastOperationMessage : résultat de hello décrivant de votre dernière opération de redéploiement de la Maintenance du Message.

## <a name="pre-emptive-redeploy"></a>Redéploiement préemptif

Action de redéployer préemptives fournit hello flexibilité toocontrol hello heure maintenance VMs tooyour appliqué dans Azure. Maintenance planifiée commence par une fenêtre de maintenance préventive où vous pouvez décider à l’heure exacte de hello pour chacun de vos toobe de machines virtuelles redémarré. Cette fonctionnalité est notamment utile dans les cas d’utilisation suivants :

-   Maintenance besoin toobe coordonné avec le client de fin hello.

-   fenêtre de maintenance planifiée Hello proposé par Azure n’est pas suffisant.
    Cela peut être que fenêtre hello produit toobe hello le temps de la semaine, ou il est trop long.

-   Pour plusieurs instances ou les applications multiniveau, vous avez besoin de suffisamment de temps entre les deux machines virtuelles ou d’une certaine toofollow de séquence.

Lorsque vous appelez pour redéployer préemptive sur une machine virtuelle, il déplace hello VM tooan déjà mis à jour du nœud et ensuite l’alimente, en conservant toutes vos options de configuration et les ressources associées. Ainsi, le disque temporaire de hello est perdu et associé à des adresses IP dynamiques interface réseau virtuelle sont mises à jour.

Le redéploiement préemptif est activé une fois par machine virtuelle. S’il existe une erreur pendant le processus de hello, hello opération est abandonnée, hello VM n’est pas affecté et il est exclu de l’itération de maintenance hello planifié. Vous être contacté en une date ultérieure, avec une planification et proposé une nouvelle opportunité tooschedule et séquence hello impact sur vos machines virtuelles.