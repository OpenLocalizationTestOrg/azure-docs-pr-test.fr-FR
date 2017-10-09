---
title: "vue d’ensemble des fonctionnalités aaaAzure concentrateurs d’événements | Documents Microsoft"
description: "Vue d’ensemble et détails sur les fonctionnalités des concentrateurs d’événements"
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 8094e48abc8455ed725d4d5d3f9895f431441e2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-features-overview"></a>Vue d’ensemble des fonctionnalités des concentrateurs d’événements

Azure Event Hubs est un service évolutif de traitement d’événements qui ingère et traite de gros volumes de données et d’événements avec une faible latence et une haute fiabilité. Consultez [quel est le service Event Hubs ?](event-hubs-what-is-event-hubs.md) pour une vue d’ensemble du service de hello.

Cet article s’appuie sur les informations de hello Bonjour [vue d’ensemble](event-hubs-what-is-event-hubs.md)et fournit des détails techniques et de mise en œuvre sur les fonctionnalités et composants de concentrateurs d’événements.

## <a name="event-publishers"></a>Éditeurs d'événements

Une entité qui envoie le concentrateur d’événements de données tooan est producteur d’événement, ou *Éditeur d’événements*. Les éditeurs d’événements peuvent publier des événements à l’aide du protocole HTTPS ou AMQP 1.0. Les éditeurs d’événements utilisez un tooidentify de jeton de Signature d’accès partagé (SAS) eux-mêmes tooan concentrateur d’événements et peuvent avoir une identité unique ou un jeton SAP commun.

### <a name="publishing-an-event"></a>Publication d'un événement

Vous pouvez publier un événement avec AMQP 1.0 ou HTTPS. Fournit des concentrateurs d’événements [les classes et les bibliothèques clientes](event-hubs-dotnet-framework-api-overview.md) pour la publication de concentrateur d’événements événements tooan à partir de clients .NET. Pour les autres runtimes et plateformes, vous pouvez utiliser n'importe quel client AMQP 1.0, comme [Apache Qpid](http://qpid.apache.org/). Vous pouvez publier les événements individuellement ou par lots. Une publication unique (instance de données d’événement) a une limite de 256 Ko, qu’il s’agisse d’un événement unique ou d’un lot. La publication d'événements plus volumineux que ce seuil entraîne une erreur. Il est recommandé pour toobe de serveurs de publication sans se préoccuper de partitions dans le concentrateur d’événements hello et tooonly spécifier un *clé de partition* (introduit dans la section suivante de hello), ou leur identité via leur jeton SAP.

Hello choix toouse AMQP ou HTTPS est le scénario d’utilisation de toohello spécifique. Le protocole AMQP requiert l’établissement d’un socket bidirectionnel persistant hello dans la sécurité au niveau des tootransport addition (TLS) ou SSL/TLS. AMQP a des coûts de réseau plus élevés lors de l’initialisation de session de hello, toutefois, HTTPS requiert traitement SSL supplémentaire pour chaque demande. Par ailleurs, AMQP propose des performances plus élevées pour les éditeurs courants.

![Event Hubs](./media/event-hubs-features/partition_keys.png)

Concentrateurs d’événements permet de s’assurer que tous les événements qui partage une valeur de clé de partition sont remis dans l’ordre et toohello que même partition. Si les clés de partition sont utilisées avec les stratégies de serveur de publication, puis hello identité du serveur de publication hello et valeur hello de clé de partition hello doit correspondre. Sinon, une erreur se produit.

### <a name="publisher-policy"></a>Stratégie de l'éditeur

Event Hubs permet un contrôle granulaire sur les éditeurs d'événements par le biais des *stratégies d'éditeur*. Stratégies d’éditeur sont des fonctionnalités d’exécution conçues toofacilitate grand nombre d’éditeurs d’événements indépendant. Avec les stratégies du serveur de publication, chaque serveur de publication utilise son propre identificateur lors de la publication du concentrateur d’événements événements tooan, à l’aide de hello suivant mécanisme :

```
//[my namespace].servicebus.windows.net/[event hub name]/publishers/[my publisher name]
```

Vous n’avez pas les noms d’éditeurs toocreate avance, mais il doit correspondre au jeton SAS de hello utilisé lors de la publication d’un événement, dans les identités des éditeurs indépendants tooensure ordre. Lorsque vous utilisez des stratégies d’éditeur, hello **PartitionKey** a la valeur toohello nom de l’éditeur. toowork correctement, ces valeurs doivent correspondre.

## <a name="capture"></a>Capture

[Capturer des concentrateurs d’événements](event-hubs-capture-overview.md) vous tooautomatically hello de capture de diffusion en continu des données dans des concentrateurs d’événements et enregistrez-le tooyour les choix d’un compte de stockage d’objets Blob ou d’un compte de Service de LAC de données Azure. Vous pouvez activer la Capture de hello portail Azure et spécifiez une taille minimale et la capture de temps fenêtre tooperform hello. À l’aide de capturer des concentrateurs d’événements, vous spécifiez votre propre compte de stockage d’objets Blob Azure et d’un conteneur, ou compte de Service de LAC de données Azure, qui est utilisé toostore hello les données capturées. Les données capturées sont écrit au format de Apache Avro hello.

## <a name="partitions"></a>Partitions

Concentrateurs d’événements fournit le message de diffusion en continu via un modèle de consommateur partitionné où chaque consommateur lit uniquement un sous-ensemble spécifique, ou une partition, du flux de messages hello. Ce modèle permet la mise à l’échelle horizontale pour le traitement des événements et fournit d’autres fonctionnalités de flux qui ne sont pas disponibles dans les rubriques et les files d’attente.

Une partition est une séquence ordonnée d’événements qui est conservée dans un concentrateur d’événements. Comme les événements plus récents arrivent, ils sont ajoutés fin toohello de cette séquence. Une partition peut être considérée comme un « journal de validation ».

![Event Hubs](./media/event-hubs-features/partition.png)

Concentrateurs d’événements conserve les données pendant une période de rétention configurée qui s’appliquent à toutes les partitions dans le concentrateur d’événements hello. Les événements expirent selon une base temporelle. Vous ne pouvez pas les supprimer explicitement. Comme les partitions sont indépendantes et contiennent leur propre séquence de données, elles évoluent souvent à des vitesses différentes.

![Event Hubs](./media/event-hubs-features/multiple_partitions.png)

nombre de Hello de partitions est spécifié lors de la création et doit être comprise entre 2 et 32. nombre de partitions Hello n’est pas modifiable, vous devez envisager la mise à l’échelle à long terme lors de la définition du nombre de partitions. Les partitions sont un mécanisme d’organisation de données qui se rapporte toohello de parallélisme en aval requis dans les applications consommatrices. Hello nombre de partitions dans un concentrateur d’événements sont directement liées toohello nombre de lecteurs simultanés souhaitées toohave. Vous pouvez augmenter le nombre de hello de partitions au-delà de 32 à contacter l’équipe de concentrateurs d’événements hello.

Alors que les partitions sont identifiables et peuvent être envoyées toodirectly, envoyant directement tooa partition n’est pas recommandée. Au lieu de cela, vous pouvez utiliser des constructions de niveau supérieur, introduites dans hello [Éditeur d’événements](#event-publishers) et [capacité](#capacity) sections. 

Les partitions sont remplies avec une séquence de données d’événement qui contient le corps hello d’événement de hello, un sac défini par l’utilisateur et les métadonnées telles que son décalage dans la partition de hello et son numéro de séquence de flux hello.

Pour plus d’informations sur les partitions et les compromis de hello entre la disponibilité et la fiabilité, consultez hello [guide de programmation de concentrateurs d’événements](event-hubs-programming-guide.md#partition-key) et hello [disponibilité et la cohérence dans les concentrateurs d’événements](event-hubs-availability-and-consistency.md) article .

### <a name="partition-key"></a>Clé de partition

Vous pouvez utiliser un [clé de partition](event-hubs-programming-guide.md#partition-key) toomap des données d’événement entrant vers des partitions spécifiques à des fins de hello d’organisation des données. clé de partition Hello est une valeur fournie par l’expéditeur est passée dans un concentrateur d’événements. Elle est traitée via une fonction de hachage statique, ce qui crée l’attribution de partition hello. Si vous ne spécifiez aucune clé de partition lors de la publication d’un événement, une affectation de type tourniquet (round robin) est utilisée.

Éditeur d’événements Hello est uniquement informé de sa clé de partition, pas les événements de hello du toowhich hello partition sont publiés. Cette séparation de la clé et la partition isole expéditeur hello d’avoir tooknow trop sur le traitement en aval de hello. Un périphérique ou un utilisateur unique identité rend une bonne clé de partition, mais les autres attributs tels que geography peuvent également être utilisé toogroup événements associés dans une seule partition.

## <a name="sas-tokens"></a>Jetons SAS

Utilise des concentrateurs d’événements *Signatures d’accès partagé*, qui sont disponible au niveau du concentrateur hello espace de noms et des événements. Un jeton SAS est généré à partir d'une clé SAS. C'est un hachage SHA d'une URL, codé dans un format spécifique. À l’aide du nom hello de clé de hello (stratégie) et du jeton de hello, les concentrateurs d’événements peut régénérer le hachage de hello et ainsi s’authentifier l’expéditeur de hello. Normalement, les jetons SAS pour les éditeurs d’événements sont créés uniquement avec des privilèges **d’envoi** sur un concentrateur d’événements spécifique. Identification de l’éditeur introduite dans la stratégie d’éditeur hello, ce mécanisme d’URL de jeton SAS sert hello. Pour plus d’informations sur l’utilisation de SAS, consultez [Authentification par signature d’accès partagé avec Service Bus](../service-bus-messaging/service-bus-sas.md).

## <a name="event-consumers"></a>Consommateurs d'événements

Toute entité qui lit des données d’événement à partir d’un concentrateur d’événements est un *consommateur d’événements*. Tous les consommateurs de concentrateurs d’événements se connectent via une session de hello AMQP 1.0 et les événements sont remis via une session de hello dès qu’elles sont disponibles. client de Hello ne nécessite pas de toopoll pour la disponibilité des données.

### <a name="consumer-groups"></a>Groupes de consommateurs

le mécanisme de publication/abonnement Hello des concentrateurs d’événements est activé via *groupes de consommateurs*. Un groupe de consommateurs est une vue (état, position ou décalage) d’un concentrateur d’événements dans sa totalité. Groupes de consommateurs activer plusieurs applications consommatrices tooeach ont une vue distincte du flux d’événements hello et flux de hello tooread indépendamment à leur propre rythme et avec leurs propres décalages.

Dans un architecture de traitement de flux, chaque application en aval équivaut tooa du groupe de consommateurs. Si vous souhaitez que le stockage à long terme toolong de toowrite événements données, cette application d’enregistrement est un groupe de consommateurs. Le traitement des événements complexes est ensuite effectué par un autre groupe de consommateurs distinct. Vous ne pouvez accéder aux partitions que par le biais d'un groupe de consommateurs. Il peut y avoir au maximum 5 lecteurs simultanés sur une partition par groupe de consommateurs. Toutefois **il est recommandé de n’avoir qu’un seul récepteur actif sur une partition par groupe de consommateurs**. Un groupe de consommateurs par défaut est toujours dans un concentrateur d’événements, et vous pouvez créer des groupes de consommateurs too20 pour un concentrateur d’événements de niveau Standard.

Hello Voici des exemples de convention d’URI du groupe de consommateurs hello :

```http
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #1]
//[my namespace].servicebus.windows.net/[event hub name]/[Consumer Group #2]
```

Hello figure ci-dessous illustre l’architecture de traitement flux hello concentrateurs d’événements :

![Event Hubs](./media/event-hubs-features/event_hubs_architecture.png)

### <a name="stream-offsets"></a>Décalages du flux

Un *offset* position hello d’un événement dans une partition. Vous pouvez considérer un décalage comme un curseur côté client. décalage Hello est un octet de numérotation de l’événement de hello. Ce décalage permet un toospecify de consommateur (lecteur) d’événement un point dans le flux d’événements hello à partir duquel ils veulent toobegin la lecture des événements. Vous pouvez spécifier le décalage de hello comme un horodatage ou comme une valeur de décalage. Les clients sont responsables du stockage de leurs propres valeurs de décalage en dehors de hello service Event Hubs. Dans une partition, chaque événement inclut un décalage.

![Event Hubs](./media/event-hubs-features/partition_offset.png)

### <a name="checkpointing"></a>Points de contrôle

Les *points de contrôle* constituent un processus par lequel les lecteurs marquent ou valident leur position dans une séquence d’événements de partition. Points de contrôle incombe de hello du consommateur de hello et se produit sur une base par partition dans un groupe de consommateurs. Cette responsabilité signifie que pour chaque groupe de consommateurs, chaque lecteur de partition doit conserver une trace de sa position actuelle dans le flux d’événements hello et permet d’informer le service de hello quand il considère que les flux de données hello terminée.

Si un lecteur se déconnecte d’une partition, lorsqu’il reconnecte, il commence à lire au point de contrôle hello précédemment soumis par hello dernier lecteur de cette partition dans ce groupe de consommateurs. Lorsque le lecteur de hello se connecte, il transmet ce décalage toohello événement hub toospecify hello emplacement lequel toostart la lecture. De cette façon, vous pouvez utiliser des points de contrôle tooboth marquer des événements comme « terminé » par les applications en aval, et résilience tooprovide si un basculement entre des lecteurs en cours d’exécution sur des ordinateurs différents se produit. Il est possible de tooreturn tooolder données en spécifiant un décalage inférieur à partir de ce processus de vérification. Grâce à ce mécanisme, les points de contrôle permettent une résilience au basculement renforcée, mais également la relecture du flux d’événements.

### <a name="common-consumer-tasks"></a>Tâches courantes du consommateur

Tous les consommateurs Azure Event Hubs se connectent via une session AMQP 1.0, un canal de communication bidirectionnelle prenant en charge l’état. Chaque partition a une session AMQP 1.0 qui facilite le transport hello d’événements séparés par partition.

#### <a name="connect-tooa-partition"></a>Se connecter tooa partition

Lors de la connexion toopartitions, il est commun toouse pratique un bail de partitions de mécanisme toocoordinate reader connexions toospecific. De cette manière, il est possible pour chaque partition dans un consommateur groupe toohave qu’un seul lecteur actif. Points de contrôle, la location et la gestion des lecteurs sont simplifiées à l’aide de hello [EventProcessorHost](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost) classe pour les clients .NET. Hello processeur d’événements hôte est un agent de consommateur intelligent.

#### <a name="read-events"></a>Lire les événements

Une fois la session AMQP 1.0 et établir un lien est ouverte pour une partition spécifique, les événements sont remis toohello AMQP 1.0 client par hello service Event Hubs. Ce mécanisme de livraison permet un débit plus élevé et une latence plus faible par rapport aux mécanismes basés sur l'extraction, tels que HTTP GET. Comme les événements sont envoyés toohello client, chaque instance de données d’événement contient des métadonnées importantes telles que nombre hello offset et de la séquence qui sont utilisés toofacilitate des points de contrôle sur la séquence d’événements hello.

Données d’événement :
* Offset
* Numéro de séquence
* Corps
* Propriétés de l’utilisateur
* Propriétés système

Il est le décalage de hello toomanage responsabilité.

## <a name="capacity"></a>Capacity

Concentrateurs d’événements possède une architecture parallèle hautement extensible et il existe plusieurs facteurs clés tooconsider, lors du dimensionnement et de mise à l’échelle.

### <a name="throughput-units"></a>Unités de débit

capacité de débit Hello des concentrateurs d’événements est contrôlée par *unités de débit*. Les unités de débit sont des unités de capacité achetées préalablement. Une unité de débit inclut hello suivant de capacité :

* Entrée : des Mo too1 par seconde ou 1 000 événements par seconde (selon celle qui apparaît en premier)
* Sortie : des Mo too2 par seconde

Au-delà de la capacité de hello de hello acheté des unités de débit, l’entrée est limitée et un [ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) est retourné. Sortie ne produit pas d’exceptions de limitation, mais toujours limitée toohello une capacité de hello acheté des unités de débit. Si vous recevez des exceptions de vitesse de publication ou que vous attendez une sortie supérieure toosee, être toocheck que le nombre d’unités de débit que vous avez achetées pour l’espace de noms hello. Vous pouvez gérer des unités de débit sur hello **échelle** panneau d’espaces de noms hello Bonjour [portail Azure](https://portal.azure.com). Vous pouvez également gérer des unités de débit par programmation à l’aide de hello [API de concentrateurs d’événements](event-hubs-api-overview.md).

Les unités de débit sont facturées par heure et sont préalablement acquises. Une fois achetées, les unités de débit sont facturées au moins une heure. Too20 unités de débit peuvent être achetées pour un espace de noms de concentrateurs d’événements et sont partagées entre tous les concentrateurs d’événements dans l’espace de noms hello.

Plusieurs unités de débit peuvent être achetées dans les blocs de 20 unités de débit too100, en contactant le support Azure. Ensuite, vous pouvez également acheter des blocs de 100 unités de débit.

Nous vous recommandons d’équilibrer échelle optimale tooachieve partitions et les unités de débit. Une partition unique a une échelle maximale d'une unité de débit. Hello nombre d’unités de débit doit être inférieure ou égale nombre toohello de partitions dans un concentrateur d’événements.

Pour obtenir des informations de tarification détaillées des concentrateurs d’événements, consultez [Tarification des concentrateurs d’événements](https://azure.microsoft.com/pricing/details/event-hubs/).

## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur les concentrateurs d’événements, consultez hello suivant liens :

* Prise en main avec un [didacticiel des hubs d'événements][Event Hubs tutorial]
* [Guide de programmation de concentrateurs d’événements](event-hubs-programming-guide.md)
* [Disponibilité et cohérence dans Event Hubs](event-hubs-availability-and-consistency.md)
* [FAQ sur les hubs d'événements](event-hubs-faq.md)
* [Exemples de hubs d’événements][]

[Event Hubs tutorial]: event-hubs-dotnet-standard-getstarted-send.md
[Exemples de hubs d’événements]: https://github.com/Azure/azure-event-hubs/tree/master/samples
