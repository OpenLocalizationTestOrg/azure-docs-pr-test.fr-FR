---
title: "aaaTroubleshoot équilibrage de charge Azure | Documents Microsoft"
description: "Résoudre les problèmes connus liés à Azure Load Balancer"
services: load-balancer
documentationcenter: na
author: RamanDhillon
manager: timlt
editor: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/10/2017
ms.author: kumud
ms.openlocfilehash: 56b73fcbf0bbf18cedfd113a280cfafa2a3dc9f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-load-balancer"></a>Résoudre les problèmes liés à Azure Load Balancer

Cette page contient des informations de résolution des problèmes liés aux questions courantes relatives à Azure Load Balancer. Lors de la connectivité d’équilibrage de charge de hello n’est pas disponible, les symptômes les plus courants hello sont les suivantes : 
- Machines virtuelles derrière un équilibreur de charge ne répondent pas toohealth sondes de hello 
- Machines virtuelles derrière un équilibreur de charge de hello ne répondent pas toohello du trafic sur le port hello configuré

## <a name="symptom-vms-behind-hello-load-balancer-are-not-responding-toohealth-probes"></a>Symptôme : les machines virtuelles derrière un équilibreur de charge de hello ne répondent pas toohealth sondes
Pour hello tooparticipate de serveurs principaux dans le jeu d’équilibrage de charge de hello, ils doivent passer hello sonde vérification. Pour plus d’informations sur les sondes d’intégrité, consultez la page [Comprendre les sondes de l’équilibrage de charge](load-balancer-custom-probe-overview.md). 

pool principal d’équilibreur de charge Hello machines virtuelles ne répond pas toohello sondes tooany échéance Hello suivant raisons : 
- Une machine virtuelle du pool principal de l’équilibreur de charge est défectueuse 
- Machine virtuelle n’écoute pas sur le port de la sonde hello pool principal d’équilibreurs de charge 
- Un pare-feu ou un groupe de sécurité réseau bloque port hello hello pool principal d’équilibreur de charge machines virtuelles 
- Autres erreurs de configuration de l’équilibreur de charge

### <a name="cause-1-load-balancer-backend-pool-vm-is-unhealthy"></a>Cause 1 : une machine virtuelle du pool principal de l’équilibreur de charge est défectueuse 

**Validation et résolution**

tooresolve ce problème, connectez-vous à toohello participant à des machines virtuelles et vérifiez si hello état des ordinateurs virtuels est sain et peut répondre trop**PsPing** ou **TCPing** à partir d’une autre machine virtuelle dans le pool de hello. Si hello machine virtuelle est défectueux ou Impossible toorespond toohello sonde, vous devez résoudre le problème de hello et obtenir hello VM sauvegarder l’état intègre tooa avant de pouvoir faire partie de l’équilibrage de charge.

### <a name="cause-2-load-balancer-backend-pool-vm-is-not-listening-on-hello-probe-port"></a>Cause 2 : Le pool principal d’équilibreur de charge machine virtuelle n’écoute pas sur le port de la sonde hello
Si hello machine virtuelle est intègre, mais ne répond pas toohello sonde, une des raisons peut-être que port de la sonde hello n’est pas ouvert sur hello participant à la machine virtuelle, ou hello VM n’est pas à l’écoute sur ce port.

**Validation et résolution**

1. Le journal dans le back-end toohello machine virtuelle. 
2. Ouvrez une invite de commandes et exécutez hello suivant toovalidate de commande est une application qui écoute sur le port de la sonde hello :   
            netstat -an
3. Si l’état du port hello n’est pas répertorié comme **écoute**, configurer le port approprié de hello. 
4. Vous pouvez également sélectionner un autre port, qui indique **ÉCOUTE**, et mettre à jour en conséquence la configuration de l’équilibreur de charge.              

###<a name="cause-3-firewall-or-a-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vms"></a>Cause 3 : Un pare-feu ou un groupe de sécurité réseau bloque port hello sur le pool principal équilibreurs de charge hello machines virtuelles  
Si le pare-feu hello sur hello que VM bloque port de la sonde hello ou un ou plusieurs groupes de sécurité réseau configurés sur le sous-réseau de hello ou hello machine virtuelle, n’autorise pas de port de hello sonde tooreach hello, hello machine virtuelle est sonde de contrôle d’intégrité toohello toorespond impossible.          

**Validation et résolution**

* Si le pare-feu hello est activé, vérifiez s’il est configuré port de la sonde tooallow hello. Si ce n’est pas le cas, configurez le trafic de hello pare-feu tooallow sur le port de la sonde hello et testez à nouveau. 
* À partir de la liste de hello des groupes de sécurité réseau, vérifiez si le trafic entrant ou sortant hello sur le port de la sonde hello interférence. 
* En outre, vérifiez si un **Deny All** groupes de sécurité réseau de règle sur hello NIC de machine virtuelle de hello ou hello sous-réseau qui a une priorité plus élevée que la règle par défaut hello qui permet à trafic et des sondes d’équilibrage de charge (groupes de sécurité réseau doivent autoriser IP d’équilibrage de charge de 168.63.129.16). 
* Si une de ces règles bloquent le trafic de sonde hello, supprimer et reconfigurer le trafic de sondes hello règles tooallow hello.  
* Testez si hello machine virtuelle a démarré maintenant répondre le contrôle d’intégrité toohello sondes. 

### <a name="cause-4-other-misconfigurations-in-load-balancer"></a>Cause 4 : autres erreurs de configuration de l’équilibreur de charge
Si tous les hello causes précédents semblent toobe validé et résolus correctement et le serveur principal de hello VM toujours ne pas répondre toohello sonde de contrôle d’intégrité, puis manuellement tester la connectivité et collecter une connectivité de hello toounderstand traces.

**Validation et résolution**

* Utilisez **Psping** parmi hello autres machines virtuelles dans hello réponse de port de réseau virtuel tootest hello sonde (exemple :.\psping.exe -t 10.0.0.4:3389) et enregistrez les résultats. 
* Utilisez **TCPing** parmi hello autres machines virtuelles dans hello réponse de port de réseau virtuel tootest hello sonde (exemple :.\tcping.exe 10.0.0.4 3389) et enregistrez les résultats. 
* Si aucune réponse n’est reçue dans ces tests ping,
    - Exécuter un simultanées Netsh trace sur le pool principal de cible hello machine virtuelle et une autre machine virtuelle de test à partir de hello même réseau virtuel. Maintenant, exécutez un test PsPing pendant un certain temps, collecter des traces réseau, puis arrêter le test de hello. 
    - Analyser la capture de réseau hello et s’il existe deux requête ping de toohello connexes paquets entrants et sortants. 
        - Si aucun les paquets entrants ne sont observées sur le pool principal d’hello machine virtuelle, il est potentiellement un groupe de sécurité réseau ou UDR mauvaise configuration bloquer hello le trafic. 
        - Si aucun les paquets sortants ne sont observées sur le pool principal d’hello VM, hello machine virtuelle doit toobe activée pour tous les problèmes non liées (par eample, port de la sonde Application blocage hello). 
    - Vérifier si les paquets hello sonde sont destination tooanother forcé (probablement via les paramètres de UDR) avant d’atteindre l’équilibrage de charge hello. Cela peut entraîner hello trafic toonever portée hello principal machine virtuelle. 
* Modifier le type de sonde hello (par exemple, HTTP tooTCP) et configurer le port correspondant de hello dans les listes ACL des groupes de sécurité réseau et pare-feu toovalidate si hello problème avec la configuration de hello de réponse de sonde. Pour plus d’informations sur la configuration de la sonde d’intégrité, consultez la page [Endpoint Load Balancing health probe configuration (Configuration d’une sonde d’intégrité pour l’équilibrage de charge des points de terminaison)](https://blogs.msdn.microsoft.com/mast/2016/01/26/endpoint-load-balancing-heath-probe-configuration-details/).

## <a name="symptom-vms-behind-load-balancer-are-not-responding-tootraffic-on-hello-configured-data-port"></a>Symptôme : les machines virtuelles derrière un équilibreur de charge ne répondent pas tootraffic sur le port de données hello configuré

Si un pool principal d’ordinateur virtuel est répertorié comme sain et répond toohello les sondes d’intégrité, mais ne participe pas toujours à l’équilibrage de charge de hello ou ne répond pas toohello le trafic des données, il peut être dû tooany Hello suivant raisons : 
* Pool principal d’équilibrage de la que machine virtuelle n’est pas à l’écoute sur le port de données hello de charge 
* Groupe de sécurité réseau bloque le port hello hello pool principal d’équilibreur de charge machine virtuelle  
* Équilibrage de charge à partir de l’accès à hello hello même machine virtuelle et la carte réseau 
* L’accès à hello Internet VIP d’équilibrage de charge à partir de hello participant à la machine virtuelle pool principal d’équilibreur de charge 

### <a name="cause-1-load-balancer-backend-pool-vm-is-not-listening-on-hello-data-port"></a>Cause 1 : Le pool principal d’équilibreur de charge VM n’écoute pas sur le port de données hello 
Si une machine virtuelle ne répond pas toohello le trafic des données, il est peut-être parce que port cible de hello n’est pas ouvert sur hello participant à la machine virtuelle ou hello VM n’est pas à l’écoute sur ce port. 

**Validation et résolution**

1. Le journal dans le back-end toohello machine virtuelle. 
2. Ouvrez une invite de commandes et exécutez hello suivant toovalidate de commande est une application qui écoute sur le port de données hello :  
            netstat -an 
3. Si le port de hello n’est pas répertorié avec l’état « Écoute », de configurer le port d’écoute approprié de hello 
4. Si le port de hello est marqué comme à l’écoute, puis vérifiez application cible de hello sur ce port pour les problèmes possibles. 

### <a name="cause-2-network-security-group-is-blocking-hello-port-on-hello-load-balancer-backend-pool-vm"></a>Cause 2 : Groupe de sécurité réseau bloque port hello hello pool principal d’équilibreur de charge machine virtuelle  

Si un ou plusieurs groupes de sécurité configurés sur le sous-réseau de hello ou hello machine virtuelle du réseau, bloque hello l’adresse IP source ou le port, puis hello machine virtuelle est toorespond impossible.

* Liste des groupes de sécurité réseau hello configurés sur le back-end hello machine virtuelle. Pour plus d'informations, consultez les pages suivantes :
    -  [Gérer les groupes de sécurité réseau à l’aide de hello portail](../virtual-network/virtual-network-manage-nsg-arm-portal.md)
    -  [Gérer des groupes de sécurité réseau à l’aide de PowerShell](../virtual-network/virtual-network-manage-nsg-arm-ps.md)
* À partir de la liste de hello des groupes de sécurité réseau, vérifiez si :
    - le trafic entrant ou sortant Hello sur le port de données hello a interférence. 
    - un **Deny All** règle de groupe de sécurité réseau sur hello carte réseau du sous-réseau de machine virtuelle ou hello hello qui a une priorité plus élevée à cette règle par défaut hello qui permet des sondes d’équilibrage de charge et le trafic (groupes de sécurité réseau doivent autoriser IP d’équilibrage de charge de 168.63.129.16, qui est le port de la sonde) 
* Si une des règles de hello bloquent le trafic de hello, supprimer et reconfigurer ces le trafic de données règles tooallow hello.  
* Testez si hello machine virtuelle a démarré maintenant les sondes d’intégrité de toohello toorespond.

### <a name="cause-3-accessing-hello-load-balancer-from-hello-same-vm-and-network-interface"></a>Cause 3 : L’accès à hello équilibrage de charge à partir de hello même interface de machine virtuelle et réseau 

Si votre application hébergée dans le service principal hello machine virtuelle d’un équilibreur de charge essaie tooaccess une autre application hébergée dans hello principal même machine virtuelle sur hello même Interface réseau, il correspond à un scénario non pris en charge et échouera. 

**Résolution** vous pouvez résoudre ce problème via l’une des méthodes suivantes de hello :
* Configurez des machines virtuelles du pool principal distinctes par application. 
* Configurer application hello dans les deux machines virtuelles de carte réseau pour chaque application a été à l’aide de sa propre interface réseau et l’adresse IP. 

### <a name="cause-4-accessing-hello-internal-load-balancer-vip-from-hello-participating-load-balancer-backend-pool-vm"></a>Cause 4 : Accédez à hello VIP d’équilibrage de charge interne depuis hello participant à la machine virtuelle pool principal d’équilibreur de charge

Si une adresse IP virtuelle d’équilibrage de charge interne est configuré à l’intérieur d’un réseau virtuel, et tente d’un des principaux de participant hello machines virtuelles tooaccess hello interne VIP d’équilibrage de charge, qui entraîne l’échec. Ce scénario n’est pas pris en charge.
**Résolution** évaluer la passerelle d’Application ou d’autres toosupport proxy (par exemple, nginx ou haproxy) ce type de scénario. Pour plus d’informations sur Application Gateway, consultez la page [Vue d’ensemble de la passerelle Application Gateway](../application-gateway/application-gateway-introduction.md).

## <a name="additional-network-captures"></a>Captures de réseau supplémentaires
Si vous décidez de tooopen un cas de support, collecter hello suivant des informations pour une résolution plus rapide. Choisissez un Bonjour tooperform de machine virtuelle unique principal suite de tests :
- Utiliser Psping à partir d’un des principaux hello machines virtuelles au sein de la réponse de port de réseau virtuel tootest hello sonde de hello (exemple : psping 10.0.0.4:3389) et enregistrez les résultats. 
- Utilisez TCPing à partir d’un des principaux hello machines virtuelles au sein de la réponse de port de réseau virtuel tootest hello sonde de hello (exemple : psping 10.0.0.4:3389) et enregistrez les résultats.
- Si aucune réponse n’est reçu dans ces tests ping, exécuter une trace Netsh simultanée sur hello principal VM et hello machine virtuelle de test de réseau virtuel alors que vous exécutez PsPing puis arrêtez hello Netsh trace. 
  
## <a name="next-steps"></a>Étapes suivantes

Si hello étapes précédentes ne résolvent pas hello problème, ouvrez un [ticket de support](https://azure.microsoft.com/support/options/).

