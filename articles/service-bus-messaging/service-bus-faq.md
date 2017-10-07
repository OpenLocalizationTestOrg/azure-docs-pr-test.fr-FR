---
title: aaaAzure Service Bus, Forum aux questions (FAQ) | Documents Microsoft
description: "Répond à certaines questions fréquemment posées sur Azure Service Bus."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: cc75786d-3448-4f79-9fec-eef56c0027ba
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 71fe9eac46647a3e4026dbcaf2196984dd4b6a44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-faq"></a>FAQ Service Bus
Cet article répond à certaines questions fréquemment posées sur Microsoft Azure Service Bus. Vous pouvez aussi visiter hello [Forum aux questions sur Azure prend en charge](http://go.microsoft.com/fwlink/?LinkID=185083) pour plus d’informations de tarification et la prise en charge Azure.

## <a name="general-questions-about-azure-service-bus"></a>Questions générales sur Azure Service Bus
### <a name="what-is-azure-service-bus"></a>Qu’est-ce qu’Azure Service Bus ?
[Azure Service Bus](service-bus-messaging-overview.md) est une plateforme cloud messagerie asynchrone qui vous permet de toosend des données entre les systèmes découplées. Microsoft propose cette fonctionnalité en tant que service, ce qui signifie que vous n’avez pas toohost votre propre matériel dans l’ordre toouse il.

### <a name="what-is-a-service-bus-namespace"></a>Présentation des espaces de noms Service Bus
Un [espace de nom](service-bus-create-namespace-portal.md) fournit un conteneur d’étendue pour l’adressage des ressources Service Bus au sein de votre application. Créer un est nécessaire toouse Service Bus et à l’un des hello premières étapes de mise en route.

### <a name="what-is-an-azure-service-bus-queue"></a>Présentation des files d’attente Azure Service Bus
Une [file d’attente Service Bus](service-bus-queues-topics-subscriptions.md) est une entité dans laquelle les messages sont stockés. Les files d’attente sont particulièrement utiles lorsque vous avez plusieurs applications ou plusieurs parties d’une application distribuée qui doivent toocommunicate entre eux. file d’attente Hello est Centre de distribution tooa similaire dans la mesure où plusieurs produits (messages) sont reçus, puis envoyées à partir de cet emplacement.

### <a name="what-are-azure-service-bus-topics-and-subscriptions"></a>Présentation des rubriques et des abonnements Azure Service Bus
Une rubrique peut être visualisée comme une file d’attente. En cas d’utilisation de plusieurs abonnements, elle devient un modèle de messagerie plus riche ; plus simplement, il s’agit d’un outil de communication de type un-à-plusieurs. Ce modèle de publication/abonnement (ou *pub/sub*) permet à une application qui envoie une rubrique de message de tooa avec plusieurs abonnements toohave qu’un message reçu par plusieurs applications.

### <a name="what-is-a-partitioned-entity"></a>Présentation des entités partitionnées
Une file d’attente ou une rubrique classique est gérée par un seul courtier de messages et stockée dans une seule banque de messagerie. Les [files d’attente et rubriques partitionnées](service-bus-partitioning.md) sont gérées par plusieurs courtiers de messages et stockées dans plusieurs banques de messagerie. Cela signifie que hello le débit global d’une file d’attente partitionnée ou une rubrique n’est plus limitée par des performances d’un seul broker ou de la banque de messages hello. En outre, la panne temporaire d’une banque de messagerie ne rend pas une rubrique ou une file d’attente partitionnée indisponible.

Notez que le classement n’est pas garanti lors de l’utilisation d’entités partitionnées. Dans l’événement hello qu’une partition n’est pas disponible, vous pouvez toujours envoyer et recevoir des messages de hello autres partitions.

## <a name="best-practices"></a>Meilleures pratiques
### <a name="what-are-some-azure-service-bus-best-practices"></a>Présentation des meilleures pratiques Azure Service Bus
* [Meilleures pratiques pour les améliorations des performances à l’aide du Service Bus] [ Best practices for performance improvements using Service Bus] : cet article décrit comment les messages toooptimize performances lors de l’échange.

### <a name="what-should-i-know-before-creating-entities"></a>Quelles sont les informations à connaître pour pouvoir créer des entités ?
Hello propriétés d’une file d’attente et les rubrique suivantes est immuable. Veuillez en tenir compte lorsque vous configurez vos entités, dans la mesure où elles ne peuvent pas être modifiées sans créer une nouvelle entité de remplacement.

* Taille
* Partitionnement
* Sessions
* Détection des doublons
* Entité rapide

## <a name="pricing"></a>Tarification
Cette section répond à certaines questions fréquemment posées sur la structure de prix hello Service Bus.

Hello [Service Bus tarification et facturation](service-bus-pricing-billing.md) article explique les paramètres de facturation hello dans Service Bus et pour plus d’informations sur les options de tarification de Service Bus, consultez [détails de la tarification de Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).

Vous pouvez aussi visiter hello [FAQ sur la prise en charge Azure](http://go.microsoft.com/fwlink/?LinkID=185083) pour Azure général informations de tarification. 

### <a name="how-do-you-charge-for-service-bus"></a>Quel est le coût de Service Bus ?
Pour obtenir toutes les informations sur la tarification de Service Bus, consultez les [détails sur la tarification de Service Bus][Pricing overview]. En outre toohello prix indiqué, vous êtes facturé pour les transferts de données associés pour les sorties en dehors du centre de données hello dans lequel votre application est approvisionnée.

### <a name="what-usage-of-service-bus-is-subject-toodata-transfer-what-is-not"></a>Quelle utilisation de Service Bus est un transfert de toodata sujet ? Laquelle ne l’est pas ?
Les transferts de données au sein d’une région Azure donnée sont effectués gratuitement, de même que les transferts de données entrants. Transfert de données en dehors d’une région est frais tooegress de sujet qui se trouve [ici](https://azure.microsoft.com/pricing/details/bandwidth/).

### <a name="does-service-bus-charge-for-storage"></a>Service Bus facture-t-il le stockage ?
Non, Service Bus ne facture pas le stockage ? Toutefois, il est une quota limite hello quantité maximale de données qui peuvent être conservées par file d’attente/rubrique. Consultez la question fréquemment posée suivante de hello.

## <a name="quotas"></a>Quotas

Pour obtenir la liste de quotas et limites de Service Bus, consultez hello [vue d’ensemble des quotas de Service Bus][Quotas overview].

### <a name="does-service-bus-have-any-usage-quotas"></a>Service Bus fixe-t-il des quotas d’utilisation ?
Par défaut, pour n’importe quel service cloud, Microsoft définit un quota d’utilisation agrégée mensuel calculé avec tous les abonnements d’un client. Nous savons que vous pouvez avoir des besoins dépassant ces limites, veuillez contacter le service clientèle à tout moment pour que nous puissions déterminer vos besoins et ajuster ces limites en conséquence. Bus des services, le quota d’utilisation de hello est 5 milliards de messages par mois.

Pendant que nous réservons toodisable de droite hello un compte client qui a dépassé son quota d’utilisation d’un mois donné, nous seront avertis par courrier électronique et plusieurs tentatives toocontact un client avant d’effectuer une action. Les clients qui dépassent ces quotas seront toujours responsables des frais qui dépassent les quotas hello.

Comme avec d’autres services sur Azure, Service Bus applique un ensemble de tooensure de quotas spécifiques qu’il existe une utilisation juste des ressources. Vous trouverez plus d’informations sur ces quotas Bonjour [vue d’ensemble des quotas de Service Bus][Quotas overview].

## <a name="troubleshooting"></a>Résolution des problèmes
### <a name="what-are-some-of-hello-exceptions-generated-by-azure-service-bus-apis-and-their-suggested-actions"></a>Quelles sont les exceptions hello générées par l’API Azure Service Bus et de leurs actions suggérées ?
Pour obtenir la liste des exceptions Service Bus potentielles, consultez la page [Vue d’ensemble des exceptions][Exceptions overview].

### <a name="what-is-a-shared-access-signature-and-which-languages-support-generating-a-signature"></a>Qu’est-ce qu’une signature d’accès partagé et quels langages prennent en charge la génération d’une signature ?
Les signatures d’accès partagé sont un mécanisme d’authentification basé sur des hachages sécurisés SHA-256 ou des URI. Pour plus d’informations sur la façon toogenerate vos propres signatures dans le nœud, PHP, Java et C\#, consultez hello [Signatures d’accès partagé] [ Shared Access Signatures] l’article.

## <a name="subscription-and-namespace-management"></a>Gestion des abonnements et des espaces de noms
### <a name="how-do-i-migrate-a-namespace-tooanother-azure-subscription"></a>Comment migrer un espace de noms de tooanother abonnement Azure ?

Vous pouvez déplacer un espace de noms à partir d’un abonnement Azure tooanother, à l’aide soit hello [portail Azure](https://portal.azure.com) ou de commandes PowerShell. Dans l’opération de tri tooexecute hello, espace de noms hello doit déjà être actif. utilisateur Hello l’exécution de commandes hello doit être administrateur sur les deux sources hello et cibler des abonnements.

#### <a name="portal"></a>Portail

toouse hello abonnement de tooanother espaces de noms du Service Bus toomigrate portail Azure, suivez les instructions de hello [ici](../azure-resource-manager/resource-group-move-resources.md#use-portal). 

#### <a name="powershell"></a>PowerShell

Hello séquence suivante de commandes PowerShell déplace un espace de noms à partir d’un abonnement Azure tooanother. tooexecute cette opération, espace de noms hello doit déjà être actif et utilisateur hello exécutant des commandes PowerShell de hello doit être un administrateur sur les deux abonnements source et cible de hello.

```powershell
# Create a new resource group in target subscription
Select-AzureRmSubscription -SubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff'
New-AzureRmResourceGroup -Name 'targetRG' -Location 'East US'

# Move namespace from source subscription tootarget subscription
Select-AzureRmSubscription -SubscriptionId 'aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa'
$res = Find-AzureRmResource -ResourceNameContains mynamespace -ResourceType 'Microsoft.ServiceBus/namespaces'
Move-AzureRmResource -DestinationResourceGroupName 'targetRG' -DestinationSubscriptionId 'ffffffff-ffff-ffff-ffff-ffffffffffff' -ResourceId $res.ResourceId
```

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur le Bus des services, consultez hello rubriques suivantes.

* [Présentation d’Azure Service Bus Premium (billet de blog)](http://azure.microsoft.com/blog/introducing-azure-service-bus-premium-messaging/)
* [Présentation d’Azure Service Bus Premium (Channel9)](https://channel9.msdn.com/Blogs/Subscribe/Introducing-Azure-Service-Bus-Premium-Messaging)
* [Vue d’ensemble de Service Bus](service-bus-messaging-overview.md)
* [Présentation de l'architecture d'Azure Service Bus](service-bus-fundamentals-hybrid-solutions.md)
* [Prise en main des files d’attente Service Bus](service-bus-dotnet-get-started-with-queues.md)

[Best practices for performance improvements using Service Bus]: service-bus-performance-improvements.md
[Best practices for insulating applications against Service Bus outages and disasters]: service-bus-outages-disasters.md
[Pricing overview]: https://azure.microsoft.com/pricing/details/service-bus/
[Quotas overview]: service-bus-quotas.md
[Exceptions overview]: service-bus-messaging-exceptions.md
[Shared Access Signatures]: service-bus-sas.md
