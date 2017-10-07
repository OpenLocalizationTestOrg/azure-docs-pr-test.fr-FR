---
title: aaaAzure relais FAQ | Documents Microsoft
description: "Obtenir toosome réponses questions fréquemment posées sur Azure relais."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 886d2c7f-838f-4938-bd23-466662fb1c8e
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: ab14431e27df43287940e7d12ea37e4093638d21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-faqs"></a>FAQ sur Azure Relay

Cet article contient les réponses à certaines questions fréquemment posées sur [Azure Relay](https://azure.microsoft.com/services/service-bus/). Pour des informations générales concernant la tarification et le support d’Azure, voir [Forum Aux Questions sur le support technique Azure](http://go.microsoft.com/fwlink/?LinkID=185083).

## <a name="general-questions"></a>Questions générales
### <a name="what-is-azure-relay"></a>Qu’est-ce qu’Azure Relay ?
Hello [service de relais d’Azure](relay-what-is-it.md) facilite vos applications hybrides en vous aidant à en toute sécurité les services exposent qui résident dans un cloud public de toohello réseau d’une entreprise. Vous pouvez exposer des services de hello sans ouvrir de connexion de pare-feu et sans nécessiter d’infrastructure de réseau d’entreprise tooa modifications contraignant.

### <a name="what-is-a-relay-namespace"></a>Qu’est-ce qu’un espace de noms Relay ?
A [espace de noms](relay-create-namespace-portal.md) est un conteneur d’étendue que vous pouvez utiliser tooaddress ressources de relais au sein de votre application. Vous devez créer un relais de toouse espace de noms. Il s’agit d’une des hello premières étapes de mise en route.

### <a name="what-happened-tooservice-bus-relay-service"></a>Le service de relais du Bus de tooService s’est produit ?
Hello précédemment appelé service de relais Service Bus est désormais appelée relais de WCF. Vous pouvez continuer toouse ce service comme d’habitude. fonctionnalité des connexions hybrides Hello est une version mise à jour d’un service qui est été transplanter à partir d’Azure BizTalk Services. Relais de WCF et les connexions hybrides continuent toobe pris en charge.

## <a name="pricing"></a>Tarification
Cela permet de situer section certaines questions fréquemment posées sur hello relais structure de prix. Pour des informations sur tarification générale d’Azure, voir le [Forum Aux Questions sur le support technique Azure](http://go.microsoft.com/fwlink/?LinkID=185083). Pour des informations complètes sur la tarification de Relay, voir [Détails de la tarification de Service Bus][Pricing overview].

### <a name="how-do-you-charge-for-hybrid-connections-and-wcf-relay"></a>Comment sont facturés les services Connexions hybrides et Relais WCF ?
Pour plus d’informations sur la tarification de relais, consultez hello [connexions hybrides et les relais de WCF] [ Pricing overview] table sur la page Détails de tarification Service Bus hello. En outre toohello prix indiquées sur cette page, vous êtes facturé pour les transferts de données associés pour les sorties en dehors du centre de données hello dans lequel votre application est approvisionnée.

### <a name="how-am-i-billed-for-hybrid-connections"></a>Comment est facturé le service Connexions hybrides ?
Voici trois exemples de scénarios facturation pour les Connexions hybrides :

*   Scénario 1 :
    *   Vous avez un écouteur unique, telles qu’une instance du Gestionnaire de connexions hybrides installé et en cours d’exécution en continu pour les mois entier hello de hello.
    *   Vous envoyer des 3 Go de données via la connexion hello mois hello. 
    *   Le total des frais s’élève à 5 $.
*   Scénario 2 :
    *   Vous avez un écouteur unique, telles qu’une instance du Gestionnaire de connexions hybrides installé et en cours d’exécution en continu pour les mois entier hello de hello.
    *   Vous envoyer des 10 Go de données via la connexion hello mois hello.
    *   Le total des frais s’élève à 7,50 $. 5 $ pour la connexion de hello et 5 premiers Go + 2,50 $ pour hello supplémentaire 5 Go de données.
*   Scénario 3 :
    *   Vous avez deux instances, A et B, Hello Gestionnaire de connexions hybrides installé et en cours d’exécution en continu pour les mois entier hello.
    *   Vous envoyez des 3 Go de données via la connexion A mois hello.
    *   Vous envoyez 6 Go de données via la connexion B au cours des mois de hello.
    *   Le total des frais s’élève à 10,50 $. Qui est de 5 $ pour la connexion A + 5 $ pour connexion B + 0,50 $ (par gigaoctet de sixième hello sur connexion B).

Notez que les prix hello utilisés dans les exemples hello ne s’appliquent uniquement pendant la période d’évaluation hello connexions hybrides. Les prix sont toochange sujet à la disponibilité générale de connexions hybrides.

### <a name="how-are-hours-calculated-for-relay"></a>Comment les heures sont-elles calculées pour Relay ?

Relais WCF est disponible uniquement dans les espaces de noms de niveau Standard. Autrement, les tarifs et [quotas de connexion](../service-bus-messaging/service-bus-quotas.md) applicables aux relais restent inchangés. Cela signifie que le relais continuer toobe facturés en fonction du nombre de hello de messages (pas pour les opérations) et heures de relais. Pour plus d’informations, consultez hello [« Connexions hybrides et relais de WCF »](https://azure.microsoft.com/pricing/details/service-bus/) table sur la page de détails de tarification de hello.

### <a name="what-if-i-have-more-than-one-listener-connected-tooa-specific-relay"></a>Que se passe-t-il si j’ai relais spécifique de plus d’un écouteur tooa connectés ?
Dans certains cas, un relais peut avoir plusieurs écouteurs connectés. Un relais est considéré comme ouvert lorsqu’au moins un écouteur de relais est tooit connecté. Ajout des résultats de relais ouvert tooan écouteurs dans heures de relais supplémentaires. nombre de Hello du relais expéditeurs (les clients qui appellent ou envoyer des messages toorelays) qui sont connectés tooa relais n’affecte pas de calcul hello des heures de relais.

### <a name="how-is-hello-messages-meter-calculated-for-wcf-relays"></a>Comment le compteur de messages hello est calculée pour les relais de WCF ?
(**Cela s’applique uniquement les relais tooWCF. Les messages sont gratuits pour les Connexions hybrides.** )

En règle générale, les messages facturables pour les relais sont calculés à l’aide de hello même méthode qui est utilisée pour répartie des entités (files d’attente, rubriques et abonnements), décrites précédemment. Toutefois, il existe des différences importantes.

Envoi d’un relais de Service Bus tooa message est traité comme un « « complète » par le biais d’envoi écouteur de relais toohello qui reçoit le message de type hello. Il n’est pas traité comme un envoi opération toohello Service Bus relay, suivi d’un écouteur de relais toohello remise. Un appel de service de style de demande-réponse (du haut too64 Ko) sur les résultats d’un écouteur de relais deux messages facturables : un message facturable pour la demande de hello et un message facturable pour la réponse de hello (en supposant que la réponse de hello est également de 64 Ko ou plus petit). Cela est différent de celui à l’aide d’un toomediate de file d’attente entre un client et un service. Si vous utilisez un toomediate de file d’attente entre un client et un service, hello même modèle de demande-réponse requiert une demande envoi toohello file d’attente, suivi par une retrait/livraison du service toohello de file d’attente hello. Cela est suivi d’une file d’attente de réponse envoi tooanother et une remise de retrait/à partir de ce client toohello de file d’attente. À l’aide de hello même taille hypothèses tout au long (haut too64 Ko), hello induite par les résultats de modèle de file d’attente des messages facturables 4. Vous serez facturé pour deux fois le numéro de hello Hello tooimplement de messages que même modèle que vous effectuer à l’aide de relais. Bien entendu, il existe avantages toousing les files d’attente tooachieve ce modèle, telles que la durabilité et nivellement de charge. Ces avantages peuvent justifier les coûts supplémentaires hello.

Les relais ouverts à l’aide de hello **netTCPRelay** liaison WCF traitent les messages non pas en tant que messages individuels, mais en tant que flux de données transitant via le système de hello. Lorsque vous utilisez cette liaison, hello expéditeur et récepteur suffit de visibilité de la trame hello de hello des messages envoyés et reçus. Pour les relais qui utilisent hello **netTCPRelay** de liaison, toutes les données est traité comme un flux pour le calcul de messages facturables. Dans ce cas, Service Bus calcule la quantité totale de hello de données envoyées ou reçues via chaque relais individuel sur une base de 5 minutes. Ensuite, il divise cette quantité totale de données par nombre de hello toodetermine 64 Ko de messages facturables pour ce relais pendant cette période de temps.

## <a name="quotas"></a>Quotas
| Nom du quota | Scope | Type | Comportement en cas de dépassement | Valeur |
| --- | --- | --- | --- | --- |
| Écouteurs simultanés sur un relais |Entité |statique |Les prochaines requêtes de connexions supplémentaires sont rejetées et une exception est reçue par hello appeler du code. |25 |
| Écouteurs Relay simultanés |Pour tout le système |statique |Les prochaines requêtes de connexions supplémentaires sont rejetées et une exception est reçue par hello appeler du code. |2 000 |
| Connexions Relay simultanées pour tous les points de terminaison Relay dans un espace de noms de service |Pour tout le système |Statique |- |5 000 |
| Points de terminaison Relay par espace de noms de service |Pour tout le système |Statique |- |10 000 |
| Taille de message pour les relais [NetOnewayRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.netonewayrelaybinding.aspx) et [NetEventRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.neteventrelaybinding.aspx) |Pour tout le système |statique |Les messages entrants qui dépassent ces quotas sont rejetées et une exception est reçue par hello appeler du code. |64 Ko |
| Taille de message pour les relais [HttpRelayTransportBindingElement](https://msdn.microsoft.com/library/microsoft.servicebus.httprelaytransportbindingelement.aspx) et [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) |Pour tout le système |Statique |- |Illimité |

### <a name="does-relay-have-any-usage-quotas"></a>Relay a-t-il des quotas d’utilisation ?
Par défaut, pour n’importe quel service cloud, Microsoft définit un quota d’utilisation agrégée mensuel qui est calculé avec tous les abonnements d’un client. Nous sommes conscients que vos besoins peuvent parfois dépasser ces limites. Vous pouvez contacter le service clientèle à tout moment pour nous faire part de vos besoins afin que nous puissions ajuster ces limites de manière appropriée. Bus des services, les quotas d’utilisation de hello sont les suivantes :

* 5 milliards de messages
* 2 millions d’heures de relais

Bien que nous nous réservons toodisable de droite hello un compte qui dépasse son quota d’utilisation mensuelle, nous fournissons notification par courrier électronique, et nous faisons client hello de toocontact plusieurs tentatives avant d’effectuer une action. Les clients qui dépassent ces quotas restent responsables de frais de dépassement occasionnés.

### <a name="naming-restrictions"></a>Restrictions concernant l’attribution de noms
Le nom de l’espace de noms du relais doit compter de 6 à 50 caractères.

## <a name="subscription-and-namespace-management"></a>Gestion des abonnements et des espaces de noms
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>Comment migrer un espace de noms de tooanother abonnement Azure ?

toomove un espace de noms à partir d’un abonnement de tooanother abonnement Azure, vous pouvez soit hello utilisation [portail Azure](https://portal.azure.com) ou utiliser les commandes PowerShell. toomove un abonnement de tooanother d’espace de noms, espace de noms hello doit être déjà active. utilisateur Hello commandes hello en cours d’exécution doit être un utilisateur d’administrateur sur les deux abonnements source et cible de hello.

#### <a name="azure-portal"></a>Portail Azure

toouse hello espaces de noms Azure toomigrate portail Azure relais de l’abonnement de tooanother un abonnement, consultez [déplacer des ressources tooa nouveau groupe de ressources ou d’un abonnement](../azure-resource-manager/resource-group-move-resources.md#use-portal). 

#### <a name="powershell"></a>PowerShell

toomove de PowerShell toouse un espace de noms de l’abonnement de tooanother un abonnement Azure, hello utilisation suivant la séquence de commandes. tooexecute cette opération, espace de noms hello doit déjà être actif et utilisateur hello exécutant des commandes PowerShell de hello doit être un administrateur sur les deux abonnements source et cible de hello.

```powershell
# Create a new resource group in hello target subscription.
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move hello namespace from hello source subscription toohello target subscription.
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="troubleshooting"></a>Résolution des problèmes
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-relay-apis-and-suggested-actions-you-can-take"></a>Quelles sont les exceptions hello générés par l’API de relais d’Azure et vous pouvez effectuer des actions suggérées ?
Pour obtenir une description des exceptions courantes et des actions suggérées, voir [Exceptions Relay][Relay exceptions].

### <a name="what-is-a-shared-access-signature-and-which-languages-can-i-use-toogenerate-a-signature"></a>Quelle est la signature d’accès partagé, et quelles langues puis-je utiliser toogenerate une signature ?
Les signatures d’accès partagé (SAP) sont des mécanismes d’authentification basés sur des hachages sécurisés SHA-256 ou des URI. Pour plus d’informations sur comment toogenerate vos propres signatures dans le nœud, PHP, Java, C et c#, consultez [authentification Service Bus avec des signatures d’accès partagé][Shared Access Signatures].

### <a name="is-it-possible-toowhitelist-relay-endpoints"></a>Il est possible toowhitelist points de terminaison de relais ?
Oui. client de relais Hello établit des connexions service de relais d’Azure toohello en utilisant des noms de domaine complet. Cela permet aux clients d’ajouter une entrée pour `*.servicebus.windows.net` sur les pare-feu qui prennent en charge la mise en liste verte de DNS.

## <a name="next-steps"></a>Étapes suivantes
* [Créer un espace de noms](relay-create-namespace-portal.md)
* [Prise en main de .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Prise en main de Node](relay-hybrid-connections-node-get-started.md)

[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Relay exceptions]: relay-exceptions.md
[Shared access signatures]: ../service-bus-messaging/service-bus-sas.md