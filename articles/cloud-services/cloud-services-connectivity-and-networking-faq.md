---
title: "problèmes de mise en réseau et aaaConnectivity pour le Forum aux questions de Microsoft Azure Cloud Services | Documents Microsoft"
description: "Cet article répertorie les hello questions fréquemment posées sur la mise en réseau pour les Services de Cloud de Microsoft Azure et de connectivité."
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: e725dbbf585a76807362c59299d0a31f511afd3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connectivity-and-networking-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a>Problèmes de connectivité et de mise en réseau pour Azure Cloud Services : questions fréquentes (FAQ)

Cet article comprend des questions fréquentes sur les problèmes de connectivité et de mise en réseau pour [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services). Vous pouvez également consulter hello [page de taille de machine virtuelle de Services Cloud](cloud-services-sizes-specs.md) pour les informations de taille.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-cant-reserve-an-ip-in-a-multi-vip-cloud-service"></a>Impossible de réserver une adresse IP dans un service cloud à plusieurs adresses IP virtuelles
Tout d’abord, assurez-vous que cette instance de machine virtuelle hello que vous essayez tooreserve hello IP est activée. En second lieu, assurez-vous que vous utilisez des adresses IP réservées pour les deux hello déploiements intermédiaire et de production. **Ne le faites pas** modifier les paramètres de hello pendant le déploiement de hello est mise à niveau.

## <a name="how-do-i-remote-desktop-when-i-have-an-nsg"></a>Comment établir un Bureau à distance lorsque je possède un groupe de sécurité réseau ?
Ajouter des règles toohello groupe de sécurité réseau qui autorisent le trafic sur les ports **3389** et **20000**.  Bureau à distance utilise le port **3389**.  Les instances de Service cloud sont à charge équilibrée, donc vous ne pouvez pas contrôler directement le tooconnect d’instance pour.  Hello *RemoteForwarder* et *RemoteAccess* agents gérer le trafic RDP et hello client toosend un cookie RDP et de spécifier un tooconnect instance individuelle pour.  Hello *RemoteForwarder* et *RemoteAccess* agents nécessitent ce port **20000** être ouvert, ce qui peut être bloqué si vous disposez d’un groupe de sécurité réseau.

## <a name="can-i-ping-a-cloud-service"></a>Est-il possible d’effectuer un test ping sur un service cloud ?

Non, ne pas à l’aide de hello normal « ping » / protocole ICMP. Hello protocole ICMP n’est pas autorisé via l’équilibrage de charge Azure hello.

tootest connectivité, nous vous recommandons d’effectuer un test ping du port. Alors que Ping.exe utilise ICMP, autres outils, tels que PSPing, Nmap et telnet autorise le port TCP spécifique de tootest connectivité tooa.

Pour plus d’informations, consultez [utiliser pings de port ICMP tootest connectivité de la machine virtuelle Azure au lieu de](https://blogs.msdn.microsoft.com/mast/2014/06/22/use-port-pings-instead-of-icmp-to-test-azure-vm-connectivity/).

## <a name="how-do-i-prevent-receiving-thousands-of-hits-from-unknown-ip-addresses-that-indicate-some-sort-of-malicious-attack-toohello-cloud-service"></a>Comment empêcher la réception des milliers d’accès d’adresses IP inconnues qui indiquent une sorte d’attaque malveillante toohello de service cloud ?
Azure implémente un tooprotect de sécurité réseau MULTICOUCHE ses services de plateforme attaques distribuées par déni de service (distribué DDoS). Hello système de défense Azure DDoS fait partie d’analyse processus continu d’Azure, qui est améliorée en permanence et de test d’intrusion. Ce système de défense DDoS est conçu toowithstand attaques non seulement à partir de hello en dehors de, mais également d’autres clients Azure. Pour plus d’informations, consultez [Sécurité réseau Microsoft Azure](http://download.microsoft.com/download/C/A/3/CA3FC5C0-ECE0-4F87-BF4B-D74064A00846/AzureNetworkSecurity_v3_Feb2015.pdf).

Vous pouvez également créer un bloc de tooselectively de tâche de démarrage des adresses IP spécifiques. Pour plus d’informations, consultez [Bloquer une adresse IP spécifique](cloud-services-startup-tasks-common.md#block-a-specific-ip-address).

## <a name="when-i-try-toordp-toomy-cloud-service-instance-i-get-hello-message-hello-user-account-has-expired"></a>Lors de l’instance de service cloud tooRDP toomy, j’obtiens le message de type hello, « compte d’utilisateur hello a expiré. »
Vous pouvez obtenir le message d’erreur hello « ce compte d’utilisateur a expiré » lorsque vous contournez hello date d’expiration est configuré dans les paramètres RDP. Vous pouvez modifier la date d’expiration de hello à partir du portail de hello en procédant comme suit :
1. Connectez-vous toohello Console de gestion Azure (https://manage.windowsazure.com), accédez tooyour le service cloud, puis sélectionnez hello **configurer** onglet.
2. Sélectionnez **Accès distant**.
3. Modifier date de « Expire sur » hello, puis enregistrez la configuration de hello.

Vous devez maintenant être en mesure de tooRDP tooyour machine.

## <a name="why-is-loadbalancer-not-balancing-traffic-equally"></a>Pourquoi le service LoadBalancer n’équilibre-t-il pas équitablement le trafic ?
Pour plus d’informations sur le fonctionnement interne de l’équilibreur de charge, consultez [Azure Load Balancer new distribution mode](https://azure.microsoft.com/blog/azure-load-balancer-new-distribution-mode/) (Nouveau mode de distribution d’Azure Load Balancer).

algorithme de distribution Hello utilisé est un 5-tuple (IP, port source, source destination IP, port de destination, type de protocole) des serveurs toomap trafic tooavailable de hachage. Il fournit l’adhérence uniquement dans une session de transport. Les paquets hello même session TCP ou UDP sera dirigé toohello même centre de données IP (DIP) de l’instance derrière le point de terminaison à charge équilibrée hello. Lorsque hello client ferme et rouvre les connexion hello ou démarre une nouvelle session à partir de la même adresse IP source, port source de hello change et provoque l’hello trafic toogo tooa DIP point de terminaison différent de hello.
