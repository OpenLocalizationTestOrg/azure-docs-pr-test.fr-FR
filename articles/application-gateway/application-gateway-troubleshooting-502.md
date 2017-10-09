---
title: erreurs de Azure Application passerelle passerelle incorrecte (502) aaaTroubleshoot | Documents Microsoft
description: "Découvrez comment les erreurs tootroubleshoot 502 de passerelle d’Application"
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a>Résolution des erreurs de passerelle incorrecte dans Application Gateway

Découvrez comment les erreurs (502) passerelle incorrecte de tootroubleshoot reçu lors de l’utilisation de passerelle d’application.

## <a name="overview"></a>Vue d'ensemble

Après avoir configuré une passerelle d’application, une des erreurs hello que les utilisateurs peuvent rencontrer est « Erreur de serveur : 502 - serveur Web a reçu une réponse non valide en tant que passerelle ou proxy ». Cette erreur peut se produire en raison de toohello suivant raisons principales :

* Le [pool principal d’Azure Application Gateway n’est pas configuré ou est vide](#empty-backendaddresspool).
* Aucun des machines virtuelles de hello ou des instances dans [ensemble d’échelle de machine virtuelle sont intègres](#unhealthy-instances-in-backendaddresspool).
* Machines virtuelles ou des instances de l’ensemble d’échelle de machine virtuelle principale sont [sonde d’intégrité de par défaut ne répond pas toohello](#problems-with-default-health-probe.md).
* [Configuration non valide ou incorrecte des sondes d’intégrité personnalisées](#problems-with-custom-health-probe.md).
* [Problèmes de connectivité ou d’expiration](#request-time-out) des requêtes d’utilisateur.

## <a name="empty-backendaddresspool"></a>Pool d’adresses principal vide

### <a name="cause"></a>Cause :

Si hello passerelle d’Application n’a pas de machines virtuelles ou ensemble d’échelle de machine virtuelle configurée dans un pool d’adresses de serveur principal hello, il ne peut pas acheminer une demande du client et lève une erreur de passerelle incorrecte.

### <a name="solution"></a>Solution

Assurez-vous que le pool d’adresses principal hello n’est pas vide. Vous pouvez pour cela utiliser PowerShell, l’interface de ligne de commande ou le portail.

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

sortie de Hello de hello précédant l’applet de commande doit contenir un pool d’adresses de serveur principal non vide. Dans l’exemple suivant, la commande retourne deux pools configurés avec un nom de domaine complet ou des adresses IP pour les machines virtuelles de serveur principal. Hello état de configuration de hello BackendAddressPool doit être 'Succeeded'.

BackendAddressPoolsText :

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a>Instances non intègres dans BackendAddressPool

### <a name="cause"></a>Cause :

Si toutes les instances de hello de BackendAddressPool sont défectueux, passerelle d’Application n’ont pas de toute demande d’utilisateur principal tooroute à. Cela peut également être le cas de hello lorsque les instances de serveur principal sont sains, mais n’ont pas d’application hello requis déployée.

### <a name="solution"></a>Solution

Assurez-vous que les instances de hello sont intègres, application hello est correctement configurée. Vérifiez si les instances de serveur principal de hello sont toorespond en mesure de commande ping tooa à partir d’une autre machine virtuelle dans hello même réseau virtuel. Si configuré avec un point de terminaison public, assurez-vous que l’application web navigateur demande toohello est utilisable.

## <a name="problems-with-default-health-probe"></a>Problèmes avec la sonde d’intégrité par défaut

### <a name="cause"></a>Cause :

502 erreurs peuvent également être fréquentes indicateurs hello sonde d’intégrité par défaut est tooreach n’a pas pu machines virtuelles du serveur principal. Lorsqu’une instance de la passerelle d’Application est configurée, il configure automatiquement un tooeach de sonde d’intégrité par défaut BackendAddressPool à l’aide des propriétés de hello BackendHttpSetting. Aucun utilisateur d’entrée est obligatoire tooset cette sonde. Plus précisément, lorsqu’une règle d’équilibrage de charge est configurée, une association est établie entre BackendHttpSetting et BackendAddressPool. Une sonde est configurée pour chacune de ces associations lance la passerelle d’Application une instance de tooeach de connexion de contrôle d’intégrité réguliers dans hello BackendAddressPool port hello spécifié dans l’élément de BackendHttpSetting hello. Tableau suivant répertorie les valeurs hello associés de sonde de contrôle d’intégrité par défaut hello.

| Propriétés de la sonde | Valeur | Description |
| --- | --- | --- |
| URL de sonde |http://127.0.0.1/ |Chemin d'accès de l'URL |
| Intervalle |30 |Intervalle d’analyse en secondes |
| Délai d’attente |30 |Délai d’expiration de l’analyse en secondes |
| Seuil de défaillance sur le plan de l’intégrité |3 |Nombre de tentatives d’analyse serveur principal de Hello est marquée vers le bas après que le nombre d’échecs de sonde consécutifs hello a atteint le seuil de défaillance hello. |

### <a name="solution"></a>Solution

* Assurez-vous qu’un site par défaut est configuré et qu’il écoute sur le port 127.0.0.1.
* Si BackendHttpSetting spécifie un port autre que 80, le site par défaut de hello doit être toolisten configuré sur ce port.
* Hello appel toohttp://127.0.0.1:port doit retourner un code de résultat HTTP 200. Cela doit être retourné dans le délai d’attente de 30 secondes hello.
* Assurez-vous que le port configuré est ouvert et qu’il n’y a aucune règles de pare-feu ou les groupes de sécurité réseau Azure, qui bloquent le trafic entrant ou sortant sur le port hello configuré.
* Si les machines virtuelles Azure classiques ou le Service Cloud est utilisé avec le nom de domaine complet ou l’adresse IP publique, vérifiez hello correspondantes [point de terminaison](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) est ouvert.
* Si hello machine virtuelle est configurée via le Gestionnaire de ressources Azure et se trouve en dehors de hello réseau virtuel où la passerelle d’Application est déployée, [groupe de sécurité réseau](../virtual-network/virtual-networks-nsg.md) doit être configuré accès tooallow sur hello souhaité de port.

## <a name="problems-with-custom-health-probe"></a>Problèmes avec la sonde d’intégrité personnalisée

### <a name="cause"></a>Cause :

Sondes d’intégrité personnalisés permettent de tester le comportement par défaut de toohello davantage de flexibilité. Lorsque vous utilisez des sondes personnalisés, les utilisateurs peuvent configurer intervalle d’analyse hello, l’URL de hello et tootest de chemin d’accès et combien tooaccept d’échecs de réponse avant de marquer l’instance du pool de back-end hello comme étant défectueux. Hello propriétés supplémentaires suivantes est ajoutée.

| Propriétés de la sonde | Description |
| --- | --- |
| Nom |Nom de la sonde de hello. Ce nom est sonde de toohello toorefer utilisés dans les paramètres HTTP du serveur principal. |
| Protocole |Protocole utilisé sonde de hello toosend. Sonde de Hello utilise le protocole de hello définie dans les paramètres HTTP hello principal |
| Host |Hôte toosend hello de sonde à nom. S’applique uniquement lorsque plusieurs sites sont configurés sur Application Gateway. Ce nom est différent du nom d’hôte de la machine virtuelle. |
| Chemin |Chemin d’accès relatif de sonde de hello. chemin d’accès valide de Hello commence à partir de '/'. Sonde de Hello est envoyé trop\<protocole\>://\<hôte\>:\<port\>\<chemin d’accès\> |
| Intervalle |Intervalle d’analyse en secondes. Il s’agit d’intervalle de temps hello entre deux analyses consécutives. |
| Délai d’attente |Délai d’expiration de l’analyse en secondes. Si une réponse valide n’est pas reçue dans ce délai, la sonde de hello est marquée comme ayant échoué. |
| Seuil de défaillance sur le plan de l’intégrité |Nombre de tentatives d’analyse serveur principal de Hello est marquée vers le bas après que le nombre d’échecs de sonde consécutifs hello a atteint le seuil de défaillance hello. |

### <a name="solution"></a>Solution

Valider ce hello que sonde d’intégrité personnalisé est correctement configuré en tant que hello tableau précédent. En outre toohello précédente étapes de dépannage Vérifiez également les hello qui suit :

* Vérifiez cette sonde hello est spécifié correctement conformément à hello [guide](application-gateway-create-probe-ps.md).
* Si la passerelle d’Application est configurée pour un site unique, par hello de valeur par défaut hôte nom doit être spécifié sous la forme '127.0.0.1', à moins que sinon configurés dans une sonde personnalisée.
* Vérifiez qu’un appel toohttp : / /\<hôte\>:\<port\>\<chemin d’accès\> retourne un code de résultat HTTP 200.
* Assurez-vous que l’intervalle, délai d’expiration et UnhealtyThreshold sont dans une plage acceptable hello.
* Si à l’aide de HTTPS sonde, assurez-vous que ce serveur principal de hello ne nécessite pas SNI en configurant un certificat de secours sur le serveur principal de hello lui-même. 
* Assurez-vous que l’intervalle de délai d’attente et UnhealtyThreshold sont dans une plage acceptable hello.

## <a name="request-time-out"></a>Délai d’expiration de la demande

### <a name="cause"></a>Cause :

Lors de la réception d’une demande de l’utilisateur, passerelle d’Application s’applique hello configuré règles toohello demande et l’achemine instance du pool de back-end tooa. Il attend un intervalle de temps de réponse à partir de l’instance de serveur principal hello configurable. Par défaut, cet intervalle est de **30 secondes**. Si Application Gateway ne reçoit pas de réponse de l’application principale dans cet intervalle, la demande de l’utilisateur renverra une erreur 502.

### <a name="solution"></a>Solution

Passerelle d’application permet aux utilisateurs tooconfigure ce paramètre via BackendHttpSetting, ce qui peut être ensuite appliqués toodifferent pools. Les pools de serveurs principaux peuvent avoir des paramètres BackendHttpSetting différents et, par conséquent, des délais d’attente différents.

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a>Étapes suivantes

Si hello étapes précédentes ne résolvent pas hello problème, ouvrez un [ticket de support](https://azure.microsoft.com/support/options/).

