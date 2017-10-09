---
title: "aaaMultiple VIP d’équilibrage de charge Azure | Documents Microsoft"
description: "Vue d’ensemble des adresses IP virtuelles multiples dans Azure Load Balancer"
services: load-balancer
documentationcenter: na
author: chkuhtz
manager: narayan
editor: 
ms.assetid: 748e50cd-3087-4c2e-a9e1-ac0ecce4f869
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2016
ms.author: chkuhtz
ms.openlocfilehash: e186e1248e7d187e7efd0668dc3244465ce3e156
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-vips-for-azure-load-balancer"></a>Adresses IP virtuelles multiples pour Azure Load Balancer

Équilibrage de charge Azure vous permet de services de solde tooload sur plusieurs ports, plusieurs adresses IP ou les deux. Vous pouvez utiliser des flux équilibre de charge publics et internes équilibrage définitions tooload sur un ensemble de machines virtuelles.

Cet article décrit les notions de base hello de cette possibilité, les concepts importants et les contraintes. Si vous envisagez uniquement tooexpose services sur une seule adresse IP, vous trouverez des instructions simplifiées pour [public](load-balancer-get-started-internet-portal.md) ou [interne](load-balancer-get-started-ilb-arm-portal.md) configurations d’équilibrage de charge. Ajout de plusieurs adresses IP virtuelles est la configuration de l’adresse IP virtuelle unique tooa incrémentielle. À l’aide des concepts de hello dans cet article, vous pouvez développer une configuration simplifiée à tout moment.

Lorsque vous définissez un équilibrage de charge Azure, une configuration frontale et une configuration principale sont connectées avec des règles. Sonde d’intégrité référencé par la règle de hello Hello est utilisé toodetermine nouveaux flux sont envoyées tooa nœud dans le pool principal d’hello. serveur frontal de Hello est défini par une IP virtuelle (VIP), qui est un objet de 3 tuples constitué d’une adresse IP (publique ou interne), un protocole de transport (TCP ou UDP) et un numéro de port. Une adresse DIP est qu'une adresse IP sur une carte de réseau virtuel Azure attaché tooa machine virtuelle dans le pool principal d’hello.

Hello tableau suivant contient quelques exemples de configuration de serveur frontal :

| Adresse IP virtuelle | Adresse IP | protocol | port |
| --- | --- | --- | --- |
| 1 |65.52.0.1 |TCP |80 |
| 2 |65.52.0.1 |TCP |*8080* |
| 3 |65.52.0.1 |*UDP* |80 |
| 4 |*65.52.0.2* |TCP |80 |

table de Hello montre quatre des serveurs frontaux différents. Les serveurs frontaux nº 1, 2 et 3 présentent une adresse IP virtuelle unique avec des règles multiples. Hello même adresse IP est utilisée mais hello port ou protocole est différent pour chaque serveur frontal. Les serveurs frontaux #1 et #4 constituent un exemple de plusieurs adresses IP virtuelles, dans laquelle hello même protocole de serveur frontal et le port sont réutilisées entre plusieurs adresses IP virtuelles.

L’équilibrage de charge Azure fournit une grande souplesse dans la définition des règles d’équilibrage de charge hello. Une règle déclare comment une adresse et un port sur le serveur frontal de hello adresse de destination de toohello mappé et le port sur hello principal. Ou non les ports du serveur principal sont réutilisés par ces règles dépend de type hello de règle de hello. Chaque type de règle présente des exigences spécifiques qui peuvent affecter la configuration de l’hôte et la conception de la sonde. Il existe deux types de règle :

1. réutilisation de la règle par défaut de Hello avec aucun port principal
2. règle d’adresse IP flottante Hello dans laquelle les ports du serveur principal sont réutilisées

L’équilibrage de charge Azure vous permet de toomix les deux types de règles sur hello même configuration d’équilibrage de charge. équilibrage de charge Hello peut les utiliser simultanément pour une machine virtuelle donnée, ou toute combinaison, tant que vous respectez des contraintes de la règle de hello hello. Le type de règle que vous choisissez dépend de la configuration requise de hello de votre application et hello la complexité de prendre en charge cette configuration. Vous devez évaluer quels types de règle conviennent le mieux à votre scénario.

Nous explorons davantage ces scénarios en commençant par le comportement par défaut de hello.

## <a name="rule-type-1-no-backend-port-reuse"></a>Type de règle nº 1 : pas de réutilisation des ports principaux

![Illustration d’adresses IP multiples](./media/load-balancer-multivip-overview/load-balancer-multivip.png)

Dans ce scénario, hello frontal adresses IP virtuelles sont configurées comme suit :

| Adresse IP virtuelle | Adresse IP | protocol | port |
| --- | --- | --- | --- |
| ![Adresse IP virtuelle](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![Adresse IP virtuelle](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

Hello DIP est destination hello hello flux entrant. Dans le pool principal d’hello, chaque machine virtuelle expose service hello souhaité sur un port unique sur une adresse DIP. Ce service est associé à frontal hello via une définition de règle.

Nous définissons deux règles :

| Règle | Mapper le serveur frontal | toobackend pool |
| --- | --- | --- |
| 1 |![Adresse IP virtuelle](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![Serveur principal](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP1:80, ![Serveur principal](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) DIP2:80 |
| 2 |![Adresse IP virtuelle](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![Serveur principal](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP1:81, ![Serveur principal](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) DIP2:81 |

mappage complet de Hello dans l’équilibrage de charge Azure est désormais comme suit :

| Règle | Adresse IP virtuelle | protocol | port | Destination | port |
| --- | --- | --- | --- | --- | --- |
| ![Règle](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |Adresse IP dédiée |80 |
| ![Règle](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |Adresse IP dédiée |81 |

Chaque règle doit produire un flux avec une combinaison unique d’adresse IP de destination et de port de destination. Par le port de destination hello variables du flux de hello, plusieurs règles peuvent offrir flux toohello DIP même sur des ports différents.

Sondes d’intégrité sont toujours dirigée toohello DIP d’une machine virtuelle. Vous devez vous assurer vous que votre analyse reflète intégrité hello hello machine virtuelle.

## <a name="rule-type-2-backend-port-reuse-by-using-floating-ip"></a>Type de règle nº 2 : réutilisation des ports principaux à l’aide d’une adresse IP flottante

Équilibrage de charge Azure souplesse hello port de serveur frontal hello tooreuse entre plusieurs adresses IP virtuelles, quelle que soit le type de règle hello utilisé. En outre, certains scénarios d’application préfèrent ou requièrent des hello même port toobe utilisé par plusieurs instances d’application sur une seule machine virtuelle dans le pool principal d’hello. Des exemples courants de réutilisation de port incluent le clustering pour la haute disponibilité, les appliances réseau virtuelles, ainsi que l’exposition de plusieurs points de terminaison TLS sans nouveau chiffrement.

Si vous souhaitez le port principal de hello tooreuse entre plusieurs règles, vous devez activer IP flottante dans la définition de règle hello.

L’adresse IP flottante est une partie de ce que l’on appelle le « retour direct du serveur » (DSR). Le DSR se compose de deux éléments : une topologie de flux et un schéma de mappage d’adresses IP. Du point de vue de la plate-forme, Azure Load Balancer fonctionne toujours dans une topologie de flux DSR, que l’adresse IP flottante soit activée ou non. Cela signifie que hello sortant partie d’un flux est toujours correctement réécrite tooflow toohello directement arrière origine.

Avec le type de règle par défaut hello, Azure expose une schéma de mappage d’adresse IP pour faciliter l’utilisation d’équilibrage de charge traditionnelle. L’activation d’adresse IP flottante modifie tooallow de schéma de mappage d’adresses IP hello pour une flexibilité supplémentaire comme expliqué ci-dessous.

Hello suivant le diagramme illustre cette configuration :

![Illustration d’adresses IP multiples](./media/load-balancer-multivip-overview/load-balancer-multivip-dsr.png)

Pour ce scénario, chaque machine virtuelle dans le pool principal d’hello a trois interfaces réseau :

* DIP : une carte réseau virtuelle associée hello VM (configuration IP de ressource des cartes réseau de Azure)
* VIP1 : interface de bouclage du SE invité qui est configurée avec l’adresse IP de VIP1
* VIP2 : interface de bouclage du SE invité qui est configurée avec l’adresse IP de VIP2

> [!IMPORTANT]
> configuration de Hello des interfaces logiques de hello est effectuée au sein du système d’exploitation invité de hello. Cette configuration n’est pas exécutée ou gérée par Azure. Sans cette configuration, les règles de hello ne fonctionnera pas. Définitions de sonde d’intégrité utilisent hello DIP Hello VM plutôt que hello VIP logique. Par conséquent, votre service doit fournir des réponses de la sonde sur un port d’adresse DIP qui reflètent l’état hello hello du service de proposé sur l’adresse IP virtuelle de la logique hello.

Supposons que hello même configuration de serveur frontal comme dans le scénario précédent de hello :

| Adresse IP virtuelle | Adresse IP | protocol | port |
| --- | --- | --- | --- |
| ![Adresse IP virtuelle](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |
| ![Adresse IP virtuelle](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |*65.52.0.2* |TCP |80 |

Nous définissons deux règles :

| Règle | Mapper le serveur frontal | toobackend pool |
| --- | --- | --- |
| 1 |![Règle](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 |![Serveur principal](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) VIP1:80 (dans les machines virtuelles 1 et 2) |
| 2 |![Règle](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 |![Serveur principal](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) VIP2:80 (dans les machines virtuelles 1 et 2) |

Hello tableau suivant montre le mappage complet de hello dans l’équilibrage de charge hello :

| Règle | Adresse IP virtuelle | protocol | port | Destination | port |
| --- | --- | --- | --- | --- | --- |
| ![Adresse IP virtuelle](./media/load-balancer-multivip-overview/load-balancer-rule-green.png) 1 |65.52.0.1 |TCP |80 |Identique à l’adresse IP virtuelle (65.52.0.1) |Identique à l’adresse IP virtuelle (80) |
| ![Adresse IP virtuelle](./media/load-balancer-multivip-overview/load-balancer-rule-purple.png) 2 |65.52.0.2 |TCP |80 |Identique à l’adresse IP virtuelle (65.52.0.2) |Identique à l’adresse IP virtuelle (80) |

destination de Hello hello flux entrant est adresse hello VIP sur l’interface de boucle hello hello machine virtuelle. Chaque règle doit produire un flux avec une combinaison unique d’adresse IP de destination et de port de destination. Par différents hello adresse IP de destination du flux de hello, la réutilisation de port est possible sur hello même machine virtuelle. Votre service est équilibrage de charge toohello exposé en le liant toohello de VIP adresse IP et port de l’interface de bouclage respectifs hello.

Notez que cet exemple ne modifie pas le port de destination hello. Bien qu’il s’agit d’un scénario de l’adresse IP flottante, équilibrage de charge Azure prend également en charge définition d’un port de destination de règle toorewrite hello principal et le toomake il diffère de port de destination du serveur frontal hello.

Hello, type de règle d’adresse IP flottante est foundation hello des différents modèles de configuration d’équilibrage de charge. Un exemple qui est actuellement disponible est hello [SQL AlwaysOn avec plusieurs écouteurs](../virtual-machines/windows/sql/virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md) configuration. Au fil du temps, nous documenterons un plus grand nombre de ces scénarios.

## <a name="limitations"></a>Limitations

* Les configurations d’adresses IP virtuelles multiples sont uniquement prises en charge avec les machines virtuelles IaaS.
* Règle d’adresse IP flottante hello, votre application doit utiliser hello DIP pour les flux sortants. Si votre application lie l’adresse IP virtuelle de toohello configuré sur l’interface de bouclage hello dans le système d’exploitation invité de hello, puis SNAT n’est pas flux sortant de hello toorewrite disponibles et les flux hello échoue.
* Les adresses IP publiques ont une incidence sur la facturation. Pour plus d’informations, voir la page [Tarification des adresses IP](https://azure.microsoft.com/pricing/details/ip-addresses/)
* Des limites d’abonnement s’appliquent. Pour plus d’informations, voir les [limites de service](../azure-subscription-service-limits.md#networking-limits) .
