---
title: "Résolution des problèmes de connectivité entre machines virtuelles Azure | Microsoft Docs"
description: "Découvrez comment résoudre les problèmes de connectivité entre machines virtuelles Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/25/2017
ms.author: genli
ms.openlocfilehash: fd0f25c07cb3f385d3e8480ce1e33dec1ae0a214
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a>Résolution des problèmes de connectivité entre machines virtuelles Azure

Vous pouvez rencontrer des problèmes de connectivité entre machines virtuelles Azure. Cet article fournit les étapes requises pour vous aider à résoudre ce problème. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a>Symptôme

Une machine virtuelle Azure ne peut pas se connecter à une autre machine virtuelle de Azure.

## <a name="troubleshooting-guidance"></a>Instructions pour la résolution des problèmes 

1. [Vérifiez si la carte réseau est mal configuré](#step-1-check-if-nic-is-misconfigured)
2. [Vérifiez si le trafic réseau est bloqué par le groupe de sécurité réseau ou UDR](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [Vérifiez si le trafic réseau est bloqué par un pare-feu de machine virtuelle](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [Vérifiez si une application ou un service de la machine virtuelle écoute sur le port](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [Vérifiez si le problème est causé par SNAT](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [Vérifiez si le trafic est bloqué par des ACL pour la machine virtuelle classique](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [Vérifiez si le point de terminaison est créé pour la machine virtuelle classique](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [Impossible de se connecter à un partage réseau de machine virtuelle](#step-8-unable-to-connect-to-a-vm-network-share)
9. [Connectivité de réseau virtuel entre réseaux virtuels](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a>Étapes de dépannage

Suivez ces étapes pour résoudre le problème. Vérifiez si le problème est résolu après chaque étape. 

### <a name="step-1-check-if-nic-is-misconfigured"></a>Étape 1 : Vérifier si la carte réseau est mal configuré

Suivez [comment réinitialiser l’interface réseau pour Windows Azure VM](../virtual-machines/windows/reset-network-interface.md). 

Si le problème se produit après la modification de l’interface réseau (NIC), procédez comme suit :

**Machines virtuelles mulit-NIC**

1. Ajoutez une carte réseau.
2. Résoudre les problèmes dans la carte réseau défectueux ou supprimer des mauvais NIC.  Puis readd la carte réseau.

Pour plus d’informations, consultez [Ajouter ou supprimer des cartes réseau de machines virtuelles](virtual-network-network-interface-vm.md).

**Machine virtuelle à carte réseau unique** 

- [Redéployez la machine virtuelle Windows.](../virtual-machines/windows/redeploy-to-new-node.md)
- [Redéployer la machine virtuelle Linux.](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a>Étape 2 : Vérifier si le trafic réseau est bloqué par le groupe de sécurité réseau ou UDR

Utiliser [Vérifiez que les flux IP de l’Observateur réseau](../network-watcher/network-watcher-ip-flow-verify-overview.md) et [l’enregistrement de flux de groupe de sécurité réseau](../network-watcher/network-watcher-nsg-flow-logging-overview.md) pour déterminer s’il existe un groupe de sécurité réseau ou un itinéraire défini par l’utilisateur qui interfère avec le flux de trafic.

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a>Étape 3 : Vérifier si le trafic réseau est bloqué par un pare-feu de machine virtuelle

Désactivez le pare-feu, puis testez le résultat. Si le problème est résolu, vérifiez les paramètres dans le pare-feu et activer de nouveau.

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-the-port"></a>Étape 4 : Vérifiez si une application ou un service de la machine virtuelle écoute sur le port

Vous pouvez utiliser une des méthodes suivantes pour vérifier si les Application de la machine virtuelle ou un Service est à l’écoute sur le port

- Exécutez les commandes suivantes pour vérifier si le serveur écoute sur ce port.

**Machine virtuelle Windows**

    netstat –ano

**Machine virtuelle Linux**

    netstat -l

- Exécutez le **Telnet** commande sur la machine virtuelle à elle-même pour tester le port. Si le test échoue, application ou service n’est pas configuré pour écouter sur le port.

### <a name="step-5-check-whether-the-problem-is-caused-by-snat"></a>Étape 5 : Vérifiez si le problème est causé par SNAT

Dans certains scénarios, l’ordinateur virtuel est placé derrière une solution d’équilibrer la charge qui a une dépendance sur les ressources en dehors d’Azure. Dans ces scénarios, si vous rencontrez des problèmes de connexion intermittents, le problème peut être dû à [l’épuisement du port SNAT](../load-balancer/load-balancer-outbound-connections.md). Pour résoudre ce problème, créez une adresse IP virtuelle (ou ILPIP pour classique) pour chaque ordinateur virtuel qui se trouve derrière l’équilibrage de charge et sécurisé avec le groupe de sécurité réseau ou de la liste ACL. 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm"></a>Étape 6 : Vérifiez si le trafic est bloqué par des ACL pour la machine virtuelle classique

Une liste ACL permet d’autoriser ou refuser le trafic de manière sélective pour un point de terminaison de machine virtuelle. Pour plus d’informations, consultez la page [Gestion de l’ACL sur un point de terminaison](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

### <a name="step-7-check-whether-the-endpoint-is-created-for-the-classic-vm"></a>Étape 7 : Vérifiez si le point de terminaison est créé pour la machine virtuelle classique

Tous les ordinateurs virtuels que vous créez dans Azure à l’aide du modèle de déploiement classique peuvent communiquer automatiquement via un canal réseau privé avec d’autres machines virtuelles dans le même service cloud ou d’un réseau virtuel. Toutefois, les ordinateurs sur d'autres réseaux virtuels requièrent des points de terminaison pour diriger le trafic réseau entrant vers une machine virtuelle. Pour plus d’informations, consultez [Configuration de points de terminaison](../virtual-machines/windows/classic/setup-endpoints.md).

### <a name="step-8-unable-to-connect-to-a-vm-network-share"></a>Étape 8 : Impossible de se connecter à un partage réseau de machine virtuelle

Si vous ne parvenez pas à se connecter à un partage réseau de machine virtuelle, le problème peut résulter de cartes d’interface réseau non disponibles dans la machine virtuelle. Pour supprimer les cartes réseau non disponibles, consultez [Supprimer les cartes réseau non disponibles](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)

### <a name="step-9-inter-vnet-connectivity"></a>Étape 9 : La connectivité réseau virtuel entre réseaux virtuels

Utiliser [Vérifiez que les flux IP de l’Observateur réseau](../network-watcher/network-watcher-ip-flow-verify-overview.md) et [l’enregistrement de flux de groupe de sécurité réseau](../network-watcher/network-watcher-nsg-flow-logging-overview.md) pour déterminer s’il existe un groupe de sécurité réseau ou un itinéraire défini par l’utilisateur qui interfère avec le flux de trafic. Vous pouvez également valider votre configuration de réseau virtuel Inter [ici](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).

### <a name="need-help-contact-support"></a>Vous avez besoin d’aide ? Contactez le support technique.
Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) pour obtenir une prise en charge rapide de votre problème.