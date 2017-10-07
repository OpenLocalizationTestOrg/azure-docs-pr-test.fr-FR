---
title: "état d’analyse et les sondes d’équilibrage d’aaaLoad personnalisés | Documents Microsoft"
description: "Découvrez comment des sondes toouse personnalisé pour les instances de toomonitor d’équilibrage de charge Azure derrière un équilibreur de charge"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 46b152c5-6a27-4bfc-bea3-05de9ce06a57
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3dfcfcd2d5cffa58b160cb38d63acffbd997d452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-load-balancer-probes"></a>Comprendre les sondes de l’équilibrage de charge

Équilibrage de charge Azure offre d’intégrité hello capacité toomonitor hello des instances de serveur à l’aide de sondes. Lorsqu’une sonde échoue toorespond, équilibrage de charge cesse d’envoyer des instance non intègre de nouvelles connexions toohello. les connexions existantes Hello ne sont pas affectées, et les nouvelles connexions sont envoyées toohealthy instances.

Les rôles de service cloud (rôles de travail et rôles Web) utilisent un agent invité pour la surveillance par sonde. Des sondes personnalisées TCP ou HTTP doivent être configurées quand vous utilisez des machines virtuelles derrière un équilibreur de charge.

## <a name="understand-probe-count-and-timeout"></a>Présentation du nombre et du délai d’expiration des sondes

Le comportement des sondes dépend des éléments suivants :

* nombre de Hello de sondes réussies qui autorisent une toobe instance étiqueté comme étant en service.
* nombre de Hello de sondes ayant échouées qui provoquent une toobe instance étiqueté comme étant hors service.

valeur du délai d’expiration et la fréquence du Hello définie dans SuccessFailCount déterminer si une instance est confirmé toobe en cours d’exécution ou ne pas en cours d’exécution. Bonjour portail Azure, délai d’attente hello a la valeur tootwo hello valeur de fréquence de hello.

configuration de sonde Hello de toutes les instances d’équilibrage de la charge pour un point de terminaison (autrement dit, un jeu d’équilibrage) doit être hello identiques. Cela signifie que vous ne pouvez avoir une configuration de la sonde différents pour chaque instance de rôle ou de la machine virtuelle dans hello même service hébergé par une combinaison de point de terminaison particulier. Par exemple, chaque instance doit avoir des délais d’expiration et des ports locaux identiques.

> [!IMPORTANT]
> Une sonde d’équilibrage de charge utilise l’adresse IP de hello 168.63.129.16. Cette adresse IP publique facilite les ressources de la plateforme communication toointernal pour hello mettre-your-propriétaire-IP scénario de réseau virtuel Azure. Hello public l’adresse IP virtuelle 168.63.129.16 est utilisé dans toutes les régions et ne change pas. Nous vous conseillons d’autoriser cette adresse IP dans toutes les stratégies de pare-feu local. Elle ne doit pas être considérée comme un risque de sécurité car uniquement hello interne plateforme Azure peut obtenir un message à partir de cette adresse. Si vous ne le faites pas, il y aura un comportement inattendu dans de nombreux scénarios, telles que la configuration de hello même plage d’adresses IP 168.63.129.16 et avoir dupliqué des adresses IP.

## <a name="learn-about-hello-types-of-probes"></a>En savoir plus sur les types d’analyses par sondage hello

### <a name="guest-agent-probe"></a>Sonde d’agent invité

Cette sonde est disponible pour Azure Cloud Services uniquement. Équilibrage de charge utilise l’agent invité de hello hello virtual machine, puis écoute et répond avec une réponse HTTP 200 OK uniquement lorsque hello instance est prête hello (autrement dit, pas dans un autre état comme occupé, le recyclage ou l’arrêt).

Pour plus d’informations, consultez [configuration hello définition du fichier de service (csdef) pour les sondes d’intégrité](https://msdn.microsoft.com/library/azure/ee758710.aspx) ou [prise en main la création d’un équilibrage de charge connecté à Internet pour les services de cloud computing](load-balancer-get-started-internet-classic-cloud.md#check-load-balancer-health-status-for-cloud-services).

### <a name="what-makes-a-guest-agent-probe-mark-an-instance-as-unhealthy"></a>Dans quelles conditions une sonde d’agent invité marque-t-elle une instance comme étant défectueuse ?

Si l’agent invité de hello échoue toorespond avec HTTP 200 OK, les marques de programme d’équilibrage de charge hello hello instance ne répond pas et cesse d’envoyer l’instance toothat de trafic. équilibrage de charge Hello continue d’instance de hello tooping. Si l’agent invité de hello répond avec un HTTP 200, équilibrage de charge hello envoie à nouveau l’instance de toothat le trafic.

Lorsque vous utilisez un rôle web, code de site Web hello s’exécute généralement dans w3wp.exe, ce qui n’est pas analysé par hello tissu Azure ou l’agent invité. Cela signifie que les échecs dans w3wp.exe (par exemple, les réponses HTTP 500) ne sera pas l’agent invité de toohello signalé et équilibrage de charge hello ne prendra qu’une instance hors rotation.

### <a name="http-custom-probe"></a>Sonde HTTP personnalisée

Sonde d’équilibrage de charge HTTP personnalisée Hello remplace hello par défaut invité sonde de l’agent, ce qui signifie que vous pouvez créer votre propre logique personnalisée toodetermine hello la santé de l’instance de rôle hello. équilibrage de charge Hello les tests de votre point de terminaison toutes les 15 secondes, par défaut. instance de Hello est considéré comme toobe dans rotation d’équilibrage de charge hello s’il répond avec un HTTP 200 dans hello délai imparti (31 secondes par défaut).

Cela peut être utile si vous souhaitez tooimplement vos propres instances de tooremove logique à partir de la rotation d’équilibrage de charge. Par exemple, vous pouvez décider tooremove une instance si elle est supérieure à 90 % de l’UC et retourne un état autre que 200. Si vous avez des rôles web qui utilisent w3wp.exe, cela signifie également vous obtenez automatique d’analyse de votre site Web, car les défaillances dans votre code de site Web retourne une sonde d’équilibrage de charge non-200 état toohello.

> [!NOTE]
> Sonde de Hello HTTP personnalisé prend en charge les chemins d’accès relatifs et le protocole HTTP uniquement. HTTPS n’est pas pris en charge.

### <a name="what-makes-an-http-custom-probe-mark-an-instance-as-unhealthy"></a>Dans quelles conditions une sonde HTTP personnalisée marque-t-elle une instance comme étant défectueuse ?

* Hello application HTTP renvoie un code de réponse HTTP autre que 200 (par exemple, 403, 404 ou 500). Il s’agit d’un accusé de réception positif hello application instance doit être mises hors service immédiatement.
* serveur de Hello HTTP ne répond pas du tout après le délai d’attente hello. Selon la valeur de délai d’attente de hello est défini, cela peut signifier que sonde plusieurs demandes go sans réponse avant de sonde de hello est marqué comme inactif (autrement dit, avant de SuccessFailCount sondes sont envoyés).
* serveur de Hello ferme la connexion hello via une réinitialisation TCP.

### <a name="tcp-custom-probe"></a>Sonde TCP personnalisée

TCP sondes établir une connexion en effectuant une négociation triple avec le port de hello défini.

### <a name="what-makes-a-tcp-custom-probe-mark-an-instance-as-unhealthy"></a>Dans quelles conditions une sonde TCP personnalisée marque-t-elle une instance comme étant défectueuse ?

* serveur TCP Hello ne répond pas du tout après le délai d’attente hello. Les demandes qui ont été configuré toogo sans réponse avant de marquer la sonde hello ne pas en cours d’exécution lorsque sonde de hello comme étant ne pas en cours d’exécution dépend de nombre hello de sonde ayant échoué.
* Sonde de Hello reçoit un réinitialisation à partir de l’instance de rôle hello TCP.

Pour plus d’informations sur la configuration d’une sonde d’intégrité HTTP ou d’une sonde TCP, consultez [Création d’un équilibreur de charge accessible sur Internet dans Resource Manager à l’aide de PowerShell](load-balancer-get-started-internet-arm-ps.md).

## <a name="add-healthy-instances-back-into-load-balancer-rotation"></a>Rajouter des instances saines à la rotation d’équilibrage de charge

Les sondes HTTP et TCP sont considérés comme intègres et marquer l’instance de rôle hello comme sain lorsque :

* équilibrage de charge Hello Obtient une sonde positif hello première heure hello que machine virtuelle démarre.
* numéro d’Hello SuccessFailCount (décrit précédemment) définit la valeur hello de sondes réussies sont l’instance de rôle requis toomark hello intègre. Si une instance de rôle a été supprimée, nombre hello de sondes de réussite, successives égale ou supérieure à valeur hello d’instance de rôle SuccessFailCount toomark hello en cours d’exécution.

> [!NOTE]
> Si la santé d’une instance de rôle hello fluctue, équilibrage de charge hello attend plus longtemps avant de mettre l’instance de rôle hello en état d’intégrité hello. Cela est réalisé via Stratégie tooprotect hello infrastructure d’utilisateurs et hello.

## <a name="use-log-analytics-for-load-balancer"></a>Utiliser l’analytique des journaux pour l’équilibreur de charge

Vous pouvez utiliser [journal analytique pour l’équilibrage de charge](load-balancer-monitor-log.md) toocheck hello sonde d’intégrité état et la sonde de nombre. Journalisation sont utilisables avec les statistiques tooprovide Power BI ou Azure Operational Insights sur l’état de contrôle d’intégrité d’équilibrage de charge.
