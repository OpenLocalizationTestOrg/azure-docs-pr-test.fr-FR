---
title: "aaaTroubleshooting des problèmes de connectivité entre machines virtuelles Azure | Documents Microsoft"
description: "Découvrez comment tooTroubleshoot hello des problèmes de connectivité entre machines virtuelles Azure."
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
ms.openlocfilehash: ee0819178dcbee2bf529a495758e6c33f49e085e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-connectivity-problems-between-azure-vms"></a>Résolution des problèmes de connectivité entre machines virtuelles Azure

Vous pouvez rencontrer des problèmes de connectivité entre machines virtuelles Azure. Cet article fournit la résolution des problèmes étapes toohelp vous résolvez ce problème. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="symptom"></a>Symptôme

Une machine virtuelle Azure ne peut pas se connecter à tooanother machine virtuelle Azure.

## <a name="troubleshooting-guidance"></a>Instructions pour la résolution des problèmes 

1. [Vérifiez si la carte réseau est mal configuré](#step-1-check-if-nic-is-misconfigured)
2. [Vérifiez si le trafic réseau est bloqué par le groupe de sécurité réseau ou UDR](#step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr)
3. [Vérifiez si le trafic réseau est bloqué par un pare-feu de machine virtuelle](#step-3-check-if-network-traffic-is-blocked-by-vm-firewall)
4. [Vérifiez si l’option application de la machine virtuelle ou un service écoute sur le port de hello](#step-4-check-whether-vm-app-or-service-is-listening-on-the-port)
5. [Vérifiez si le problème de hello est causée par SNAT](#step-5-check-whether-the-problem-is-caused-by-snat)
6. [Vérifiez si le trafic est bloqué par des listes ACL pour hello VM classique](#step-6-check-whether-traffic-is-blocked-by-acls-for-the-classic-vm)
7. [Vérifiez si le point de terminaison hello est créé pour hello VM classique](#step-7-check-whether-the-endpoint-is-created-for-the-classic-vm)
8. [Partage de réseau de machine virtuelle tooa tooconnect Impossible](#step-8-unable-to-connect-to-a-vm-network-share)
9. [Connectivité de réseau virtuel entre réseaux virtuels](#step-9-inter-vnet-connectivity)

## <a name="troubleshooting-steps"></a>Étapes de dépannage

Suivez ces problèmes de hello tootroubleshoot étapes. Vérifiez si le problème de hello est résolu après chaque étape. 

### <a name="step-1-check-if-nic-is-misconfigured"></a>Étape 1 : Vérifier si la carte réseau est mal configuré

Suivez [comment tooreset interface réseau pour Windows Azure VM](../virtual-machines/windows/reset-network-interface.md). 

Si le problème de hello se produit après avoir modifié l’interface de réseau hello (NIC), procédez comme suit :

**Machines virtuelles mulit-NIC**

1. Ajoutez une carte réseau.
2. Résoudre les problèmes de hello dans hello incorrect supprimer ou carte réseau défectueux carte réseau.  Puis readd NIC de hello.

Pour plus d’informations, consultez [ajouter réseau interfaces tooor supprimer des machines virtuelles](virtual-network-network-interface-vm.md).

**Machine virtuelle à carte réseau unique** 

- [Redéployez la machine virtuelle Windows.](../virtual-machines/windows/redeploy-to-new-node.md)
- [Redéployer la machine virtuelle Linux.](../virtual-machines/linux/redeploy-to-new-node.md)

### <a name="step-2-check-if-network-traffic-is-blocked-by-nsg-or-udr"></a>Étape 2 : Vérifier si le trafic réseau est bloqué par le groupe de sécurité réseau ou UDR

Utiliser [Vérifiez que les flux IP de l’Observateur réseau](../network-watcher/network-watcher-ip-flow-verify-overview.md) et [l’enregistrement de flux de groupe de sécurité réseau](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify s’il existe un groupe de sécurité réseau ou un itinéraire défini par l’utilisateur qui interfère avec le flux de trafic.

### <a name="step-3-check-if-network-traffic-is-blocked-by-vm-firewall"></a>Étape 3 : Vérifier si le trafic réseau est bloqué par un pare-feu de machine virtuelle

Désactiver le pare-feu hello et testez les résultats hello. Si hello problème est résolu, vérifiez les paramètres de hello dans le pare-feu hello et réactiver.

### <a name="step-4-check-whether-vm-app-or-service-is-listening-on-hello-port"></a>Étape 4 : Vérifier si l’option application de la machine virtuelle ou un service écoute sur le port de hello

Vous pouvez utiliser une des hello suivant les méthodes toocheck si l’Application de la machine virtuelle ou un Service écoute sur le port de hello

- Exécutez hello suivant de commandes toocheck si hello serveur écoute sur ce port.

**Machine virtuelle Windows**

    netstat –ano

**Machine virtuelle Linux**

    netstat -l

- Exécutez hello **Telnet** commande hello port de machine virtuelle tooitself tootest hello. En cas de test de hello, application ou service n’est pas toolisten configuré sur le port hello.

### <a name="step-5-check-whether-hello-problem-is-caused-by-snat"></a>Étape 5 : Vérifier si le problème de hello est causée par SNAT

Dans certains scénarios, hello machine virtuelle est placé derrière une solution d’équilibrer la charge qui a une dépendance sur les ressources en dehors d’Azure. Dans ces scénarios, si vous rencontrez des problèmes de connexion intermittents, hello problème peut être dû [épuisement du port SNAT](../load-balancer/load-balancer-outbound-connections.md). problème de hello tooresolve, créer une adresse IP virtuelle (ou ILPIP pour classique) pour chaque ordinateur virtuel qui est derrière un équilibreur de charge hello et sécurisé avec le groupe de sécurité réseau ou de la liste ACL. 

### <a name="step-6-check-whether-traffic-is-blocked-by-acls-for-hello-classic-vm"></a>Étape 6 : Vérification si le trafic est bloqué par des listes ACL pour hello VM classique

Une liste ACL fournit hello capacité tooselectively autoriser ou refuser le trafic pour un point de terminaison de machine virtuelle. Pour plus d’informations, consultez [gérer hello ACL sur un point de terminaison](../virtual-machines/windows/classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

### <a name="step-7-check-whether-hello-endpoint-is-created-for-hello-classic-vm"></a>Étape 7 : Vérification si le point de terminaison hello est créé pour hello VM classique

Tous les ordinateurs virtuels que vous créez dans Azure à l’aide du modèle de déploiement classique hello peuvent communiquer automatiquement via un canal réseau privé avec d’autres ordinateurs virtuels de hello que même service ou de réseau virtuel de cloud. Toutefois, les ordinateurs sur d’autres réseaux virtuels nécessitent des points de terminaison toodirect hello réseau entrant trafic tooa machine virtuelle. Pour plus d’informations, consultez [comment tooset des points de terminaison](../virtual-machines/windows/classic/setup-endpoints.md).

### <a name="step-8-unable-tooconnect-tooa-vm-network-share"></a>Étape 8 : Le partage réseau VM Impossible de tooconnect tooa

Si vous êtes le partage de réseau de machine virtuelle tooa tooconnect impossible, problème de hello peut résulter de cartes d’interface réseau non disponibles dans hello machine virtuelle. toodelete hello indisponible cartes réseau, consultez [comment toodelete hello cartes réseau non disponible](../virtual-machines/windows/reset-network-interface.md#delete-the-unavailable-nics)

### <a name="step-9-inter-vnet-connectivity"></a>Étape 9 : La connectivité réseau virtuel entre réseaux virtuels

Utiliser [Vérifiez que les flux IP de l’Observateur réseau](../network-watcher/network-watcher-ip-flow-verify-overview.md) et [l’enregistrement de flux de groupe de sécurité réseau](../network-watcher/network-watcher-nsg-flow-logging-overview.md) tooidentify s’il existe un groupe de sécurité réseau ou un itinéraire défini par l’utilisateur qui interfère avec le flux de trafic. Vous pouvez également valider votre configuration de réseau virtuel Inter [ici](https://support.microsoft.com/en-us/help/4032151/configuring-and-validating-vnet-or-vpn-connections).

### <a name="need-help-contact-support"></a>Vous avez besoin d’aide ? Contactez le support technique.
Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.
