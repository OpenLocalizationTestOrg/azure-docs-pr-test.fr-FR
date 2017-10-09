---
title: "aaaOverview de capturer les concentrateurs d’événements Azure | Documents Microsoft"
description: "Capturer les données de télémétrie avec Event Hubs Capture"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e53cdeea-8a6a-474e-9f96-59d43c0e8562
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: sethm;darosa
ms.openlocfilehash: 0238cae712a0ed7bdf3e87ee93a069a553cb65df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-event-hubs-capture"></a>Azure Event Hubs Capture

Capturer les concentrateurs d’événements Azure vous permet de hello de remise tooautomatically diffusion en continu des données dans des concentrateurs d’événements tooan [le stockage Blob Azure](https://azure.microsoft.com/services/storage/blobs/) ou [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) compte de votre choix, par hello une plus grande flexibilité spécifier un intervalle de temps ou de taille. Configuration de Capture est rapide, il n’existe aucune toorun les coûts administratifs et il met à l’échelle automatiquement avec les concentrateurs d’événements [unités de débit](event-hubs-features.md#capacity). Capturer des concentrateurs d’événements est tooload moyen plus simple de hello, diffusion en continu des données dans Azure et vous permet de toofocus sur le traitement des données plutôt que sur la capture de données.

Capturer des concentrateurs d’événements vous permet de tooprocess en temps réel et en fonction de traitement par lots des pipelines sur hello même flux. Cela vous permet de créer des solutions capables d’évoluer avec vos besoins au fil du temps. Si vous créez des systèmes lot aujourd'hui avec un œil vers un traitement ultérieur en temps réel ou si vous souhaitez tooadd une solution en temps réel efficace de chemin d’accès à froid tooan existante, capturer des concentrateurs d’événements rend l’utilisation de la diffusion en continu de données plus facilement.

## <a name="how-event-hubs-capture-works"></a>Fonctionnement d’Azure Event Hubs Capture

Event Hubs est une mémoire tampon de rétention de temps durable pour l’entrée de données de télémétrie, journal de distribuées tooa similaire. tooscaling de clé Hello dans les concentrateurs d’événements est hello [modèle de consommateur partitionné](event-hubs-features.md#partitions). Chaque partition est un segment de données indépendant, et est utilisée de manière indépendante. Au fil du temps de que ces données soient hors tension, selon la période de rétention configurable hello. Par conséquent, un hub d’événements donné n’est jamais « saturé ».

Capturer des concentrateurs d’événements permet de vous toospecify votre propre compte de stockage d’objets Blob Azure et un conteneur ou un compte Azure Data Lake Store, qui sont des données hello capturée toostore utilisé. Ces comptes peuvent être Bonjour même région que votre concentrateur d’événements ou dans une autre région, ajout d’une grande souplesse toohello de fonctionnalité de Capture des concentrateurs d’événements hello.

Les données capturées sont écrites au format [Apache Avro][Apache Avro] : un format compact, rapide et binaire qui fournit des structures de données riches avec un schéma inclus. Ce format est largement utilisé dans Azure Data Factory écosystème de Hadoop hello et Analytique de flux de données. Vous trouverez plus d’informations sur l’utilisation d’Avro plus loin dans cet article.

### <a name="capture-windowing"></a>Fenêtrage de Capture

Vous tooset d’une capture de fenêtre toocontrol permet de capturer des concentrateurs d’événements. Cette fenêtre est une taille minimale et la configuration de l’heure avec une « premier wins stratégie, « ce qui signifie que qui hello les causes première déclencheur a rencontré une opération de capture. Si vous avez un quinze minutes, 100 Mo fenêtre de capture et envoyer 1 Mo par seconde, les déclencheurs de fenêtre de taille hello avant la fenêtre de temps hello. Chaque partition indépendamment de capture et écrit un objet blob de bloc terminé lors de la capture, hello nommé pour le moment hello à quels hello intervalle de capture a été rencontrée. convention d’affectation de noms de stockage Hello est comme suit :

```
[namespace]/[event hub]/[partition]/[YYYY]/[MM]/[DD]/[HH]/[mm]/[ss]
```

### <a name="scaling-toothroughput-units"></a>Mise à l’échelle des unités de toothroughput

Le trafic Event Hubs est contrôlé par les [unités de débit](event-hubs-features.md#capacity). Une unité de débit autorise 1 Mo/s ou 1 000 événements par seconde d’entrée et 2 000 événements par seconde de sortie. Les concentrateurs d’événements Standard peuvent être configurés avec 1 à 20 unités de débit, et vous pouvez en acheter d’autres en soumettant une [demande de support][support request] d’augmentation de quota. L’utilisation au-delà des unités de débit que vous avez achetées est limitée. Capturer des concentrateurs d’événements de copie les données directement à partir de stockage de concentrateurs d’événements interne hello, en ignorant les quotas de sortie unité de débit et de l’enregistrement de votre sortie pour les autres lecteurs de traitement, telles que les flux de données Analytique ou Spark.

Une fois configuré, Event Hubs Capture s’exécute automatiquement lorsque vous envoyez votre premier événement et continue de s’exécuter. toomake de votre tooknow de traitement en aval hello processus fonctionne, les concentrateurs d’événements écrit les fichiers vides lorsqu’il n’existe aucune donnée. Ce processus fournit une cadence prévisible et un marqueur qui peuvent alimenter vos processeurs de traitement par lots.

## <a name="setting-up-event-hubs-capture"></a>Configuration de l’outil Event Hubs Capture

Vous pouvez configurer la Capture au moment de la création du hub d’événements hello à l’aide de hello [portail Azure](https://portal.azure.com), ou à l’aide de modèles Azure Resource Manager. Pour plus d’informations, consultez hello suivant des articles :

- [Activer la Capture de concentrateurs d’événements à l’aide de hello portail Azure](event-hubs-capture-enable-through-portal.md)
- [Créer un espace de noms Event Hubs avec un concentrateur d’événements et activer Capture à l’aide d’un modèle Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub-enable-capture.md)

## <a name="exploring-hello-captured-files-and-working-with-avro"></a>Exploration des fichiers de hello capturée et l’utilisation de Avro

Capturer des concentrateurs d’événements crée des fichiers au format Avro, tel que spécifié dans la fenêtre de temps hello configuré. Vous pouvez afficher ces fichiers à l’aide de n’importe quel outil tel que [l’Explorateur de stockage Azure][Azure Storage Explorer]. Vous pouvez télécharger hello fichiers localement toowork sur ces derniers.

fichiers Hello produites par la Capture des concentrateurs d’événements ont hello suivant du schéma Avro :

![][3]

Un moyen simple tooexplore Avro des fichiers est à l’aide de hello [Avro outils] [ Avro Tools] jar d’Apache. Après avoir téléchargé ce fichier jar, vous pouvez voir le schéma hello d’un fichier Avro spécifique en exécutant hello de commande suivante :

```
java -jar avro-tools-1.8.2.jar getschema <name of capture file>
```

Cette commande renvoie

```
{

    "type":"record",
    "name":"EventData",
    "namespace":"Microsoft.ServiceBus.Messaging",
    "fields":[
                 {"name":"SequenceNumber","type":"long"},
                 {"name":"Offset","type":"string"},
                 {"name":"EnqueuedTimeUtc","type":"string"},
                 {"name":"SystemProperties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Properties","type":{"type":"map","values":["long","double","string","bytes"]}},
                 {"name":"Body","type":["null","bytes"]}
             ]
}
```

Vous pouvez également utiliser le format tooJSON fichier Avro outils tooconvert hello et effectuer d’autres traitements.

tooperform plus avancé du traitement, téléchargement et installer Avro votre choix de la plateforme. Au moment de hello de rédaction de cet article, les implémentations sont disponibles pour C, C++, C\#, Java, NodeJS, Perl, PHP, Python et Ruby.

Apache Avro propose des guides de mise en route complets pour [Java][Java] et [Python][Python]. Vous pouvez également lire hello [mise en route avec la Capture des concentrateurs d’événements](event-hubs-capture-python.md) l’article.

## <a name="how-event-hubs-capture-is-charged"></a>Chargement d’Azure Event Hubs Capture

Capturer des concentrateurs d’événements est limitée de même les unités toothroughput : comme un tarif horaire. frais de Hello sont nombre toohello directement proportionnelle d’unités de débit achetées pour l’espace de noms hello. Comme unités de débit augmentent et diminuent, compteurs de capturer des concentrateurs d’événements augmentent et diminuent les tooprovide correspondance des performances. compteurs de Hello se produisent en tandem. Pour plus d’informations sur les prix appliqués, consultez [Tarification d’Event Hubs](https://azure.microsoft.com/pricing/details/event-hubs/). 

## <a name="next-steps"></a>Étapes suivantes

Capturer des concentrateurs d’événements est hello plus simple des tooget données dans Azure. À l’aide d’Azure Data Lake, d’Azure Data Factory et d’Azure HDInsight, vous pouvez effectuer un traitement par lots, ainsi que d’autres analyses en utilisant des outils et des plateformes de votre choix, à l’échelle requise.

Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :

* [Bien démarrer avec l’envoi et la réception d’événements](event-hubs-dotnet-framework-getstarted-send.md)
* Un [exemple d'application complet qui utilise des hubs d’événements][sample application that uses Event Hubs]
* [Vue d’ensemble des hubs d’événements][Event Hubs overview]

[Apache Avro]: http://avro.apache.org/
[support request]: https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade
[Azure Storage Explorer]: http://azurestorageexplorer.codeplex.com/
[3]: ./media/event-hubs-capture-overview/event-hubs-capture3.png
[Avro Tools]: http://www-us.apache.org/dist/avro/avro-1.8.2/java/avro-tools-1.8.2.jar
[Java]: http://avro.apache.org/docs/current/gettingstartedjava.html
[Python]: http://avro.apache.org/docs/current/gettingstartedpython.html
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[sample application that uses Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-286fd097
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
