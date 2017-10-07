---
title: aaaService Bus avec .NET et AMQP 1.0 | Documents Microsoft
description: "Utilisation d’Azure Service Bus à partir de .NET avec AMQP"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 332bcb13-e287-4715-99ee-3d7d97396487
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: sethm
ms.openlocfilehash: d8b40f92ba29058951556fa3db1adcf9383ee69f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-service-bus-from-net-with-amqp-10"></a>Utilisation de Service Bus à partir de .NET avec AMQP 1.0

## <a name="downloading-hello-service-bus-sdk"></a>Hello durant le téléchargement du Kit de développement logiciel de Service Bus

Prise en charge d’AMQP 1.0 est disponible dans hello Kit de développement logiciel Service Bus version 2.1 ou ultérieure. Vous pouvez vous assurer version la plus récente hello en téléchargeant les bits de Service Bus hello de [NuGet][NuGet].

## <a name="configuring-net-applications-toouse-amqp-10"></a>Configuration de .NET applications toouse AMQP 1.0

Par défaut, la bibliothèque cliente de hello .NET Service Bus communique avec les hello Service service Bus à l’aide d’un protocole SOAP dédié. toouse AMQP 1.0 au lieu de protocole par défaut de hello nécessite une configuration explicite sur la chaîne de connexion de Service Bus hello, comme décrit dans la section suivante de hello. À l'exception de cette modification, le code de l'application reste inchangé lors de l'utilisation d'AMQP 1.0.

Dans la version actuelle de hello, il existe quelques fonctionnalités de l’API qui ne sont pas pris en charge lors de l’utilisation d’AMQP. Ces fonctionnalités non prises en charge sont répertoriées plus loin dans la section de hello [non pris en charge des fonctionnalités, les restrictions et les différences de comportement](#unsupported-features-restrictions-and-behavioral-differences). Certaines des hello paramètres de configuration avancée ont également une signification différente lors de l’utilisation d’AMQP.

### <a name="configuration-using-appconfig"></a>Configuration à l’aide d’App.config

Il est recommandé pour les applications toouse hello App.config fichier toostore de configuration. Pour les applications de Service Bus, vous pouvez utiliser la chaîne de connexion de Service Bus App.config toostore hello. Voici un exemple de fichier App.config :

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <appSettings>
        <add key="Microsoft.ServiceBus.ConnectionString"
             value="Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp" />
    </appSettings>
</configuration>
```

Hello valeur Hello `Microsoft.ServiceBus.ConnectionString` paramètre est la chaîne de connexion de Service Bus hello est utilisé tooconfigure hello connexion tooService Bus. format de Hello est comme suit :

`Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[SAS key];TransportType=Amqp`

Où `[namespace]` et `SharedAccessKey` sont obtenues à partir de hello [portail Azure] [ Azure portal] lorsque vous créez un espace de noms Service Bus. Pour plus d’informations, consultez [créer un espace de noms Service Bus à l’aide de hello portail Azure][Create a Service Bus namespace using hello Azure portal].

Lors de l’utilisation d’AMQP, ajoutez la chaîne de connexion de hello avec `;TransportType=Amqp`. Cette notation fait en sorte que hello client bibliothèque toomake son tooService connexion Bus à l’aide d’AMQP 1.0.

## <a name="message-serialization"></a>Sérialisation de messages

Lorsque vous utilisez le protocole par défaut de hello, hello sérialisation par défaut de la bibliothèque cliente .NET hello est toouse hello [DataContractSerializer] [ DataContractSerializer] type tooserialize un [BrokeredMessage ] [ BrokeredMessage] instance pour le transport entre la bibliothèque cliente de hello et hello Service service Bus. Lorsque vous utilisez le mode de transport AMQP hello, bibliothèque hello du client utilise le système de type hello AMQP pour la sérialisation de hello [message réparti] [ BrokeredMessage] dans un message AMQP. Cette sérialisation permet hello message toobe reçu et interprété par une application de réception qui s’exécute potentiellement sur une plateforme différente, par exemple, une application Java qui utilise l’API JMS de hello tooaccess Service Bus.

Lorsque vous construisez un [BrokeredMessage] [ BrokeredMessage] instance, vous pouvez fournir un objet .NET en tant qu’un tooserve de constructeur toohello paramètre en tant que corps hello de message de type hello. Pour les objets qui peuvent être mappés tooAMQP des types primitifs, les corps de hello est sérialisé en types de données AMQP. Si l’objet de hello ne peut pas être mappé directement dans un type primitif AMQP ; Autrement dit, un type personnalisé défini par l’application hello, puis les objet hello est sérialisé à l’aide de hello [DataContractSerializer][DataContractSerializer], et les octets de hello sérialisé sont envoyés dans un message de données AMQP.

interopérabilité toofacilitate avec des clients non .NET, utilisez uniquement des types .NET qui peuvent être sérialisés directement en types AMQP pour les corps de hello du message de type hello. Hello tableau suivant détaille ces types et le système de type hello correspondant mappage toohello AMQP.

| Type d’objet de corps .NET | Type AMQP mappé | Type de section de corps AMQP |
| --- | --- | --- |
| valeur booléenne |booléenne |Valeur AMQP |
| byte |ubyte |Valeur AMQP |
| ushort |ushort |Valeur AMQP |
| uint |uint |Valeur AMQP |
| ulong |ulong |Valeur AMQP |
| sbyte |byte |Valeur AMQP |
| short |short |Valeur AMQP |
| int |int |Valeur AMQP |
| long |long |Valeur AMQP |
| float |float |Valeur AMQP |
| double |double |Valeur AMQP |
| décimal |decimal128 |Valeur AMQP |
| char |char |Valeur AMQP |
| DateTime |timestamp |Valeur AMQP |
| Guid |uuid |Valeur AMQP |
| byte[] |binaire |Valeur AMQP |
| string |string |Valeur AMQP |
| System.Collections.IList |list |Valeur AMQP : éléments contenus dans la collection de hello peuvent uniquement être ceux qui sont définis dans cette table. |
| System.Array |array |Valeur AMQP : éléments contenus dans la collection de hello peuvent uniquement être ceux qui sont définis dans cette table. |
| System.Collections.IDictionary |map |Valeur AMQP : éléments contenus dans la collection de hello peuvent uniquement être ceux qui sont définis dans cette table. Remarque : seules les clés de chaîne sont pris en charge. |
| Uri |Décrit la chaîne (voir hello tableau suivant) |Valeur AMQP |
| Datetimeoffset |Décrit le long (voir hello tableau suivant) |Valeur AMQP |
| TimeSpan |Décrit le long (voir hello) |Valeur AMQP |
| Stream |binaire |Données AMQP (peuvent être multiples). les sections de données Hello contiennent les octets bruts hello lire à partir de l’objet de flux hello. |
| Objet Other |binaire |Données AMQP (peuvent être multiples). Contient des données binaires hello sérialisé d’objet hello qui utilise hello DataContractSerializer ou un sérialiseur fourni par l’application hello. |

| Type .NET | Type décrit AMQP mappé | Remarques |
| --- | --- | --- |
| Uri |`<type name=”uri” class=restricted source=”string”> <descriptor name=”com.microsoft:uri” /></type>` |Uri.AbsoluteUri |
| Datetimeoffset |`<type name=”datetime-offset” class=restricted source=”long”> <descriptor name=”com.microsoft:datetime-offset” /></type>` |DateTimeOffset.UtcTicks |
| TimeSpan |`<type name=”timespan” class=restricted source=”long”> <descriptor name=”com.microsoft:timespan” /></type> ` |TimeSpan.Ticks |

## <a name="unsupported-features-restrictions-and-behavioral-differences"></a>Fonctionnalités non prises en charge, restrictions et différences de comportement

Hello suivant les fonctionnalités de hello les API .NET Service Bus n’est pas actuellement pris en charge lors de l’utilisation d’AMQP :

* Transactions
* Envoi via destination de transfert

Il existe également de petites différences de comportement hello Hello les API .NET Service Bus lors de l’utilisation d’AMQP, protocole de toohello comparés par défaut :

* Hello [OperationTimeout] [ OperationTimeout] propriété est ignorée.
* `MessageReceiver.Receive(TimeSpan.Zero)` est implémenté en tant que `MessageReceiver.Receive(TimeSpan.FromSeconds(10))`.
* Fin des messages par les jetons de verrou n’est possible par les récepteurs de messages hello initialement reçu les messages hello.

## <a name="controlling-amqp-protocol-settings"></a>Contrôle des paramètres de protocole AMQP

Hello [API .NET](/dotnet/api/) exposer plusieurs toocontrol hello du comportement des paramètres de hello protocole AMQP :

* **[MessageReceiver.PrefetchCount](/dotnet/api/microsoft.servicebus.messaging.messagereceiver.prefetchcount?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessageReceiver_PrefetchCount)**: contrôles hello crédit initial appliqué tooa lien. valeur par défaut Hello est 0.
* **[MessagingFactorySettings.AmqpTransportSettings.MaxFrameSize](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.maxframesize?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_MaxFrameSize)**: taille de trame AMQP maximale contrôles hello fournie durant la négociation hello à ouvrir la connexion. valeur par défaut Hello est 65 536 octets.
* **[MessagingFactorySettings.AmqpTransportSettings.BatchFlushInterval](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.batchflushinterval?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_BatchFlushInterval)**: si les transferts sont exécutables par lots, cette valeur détermine le délai maximal de hello pour envoyer des dispositions. Héritée par les expéditeurs/destinataires par défaut. Expéditeur/destinataire individuel peut remplacer une valeur par défaut de hello, qui est de 20 millisecondes.
* **[MessagingFactorySettings.AmqpTransportSettings.UseSslStreamSecurity](/dotnet/api/microsoft.servicebus.messaging.amqp.amqptransportsettings.usesslstreamsecurity?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_Amqp_AmqpTransportSettings_UseSslStreamSecurity)** : contrôle si les connexions AMQP sont établies via une connexion SSL. valeur par défaut Hello est **true**.

## <a name="next-steps"></a>Étapes suivantes

Prêt toolearn plus ? Visitez hello suivant liens :

* [Vue d’ensemble du protocole AMQP de Service Bus]
* [Prise en charge d’AMQP 1.0 dans les rubriques et files d’attente partitionnées Service Bus]
* [AMQP dans Service Bus pour Windows Server]

[Create a Service Bus namespace using hello Azure portal]: service-bus-create-namespace-portal.md
[DataContractSerializer]: https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage?view=azureservicebus-4.0.0
[Microsoft.ServiceBus.Messaging.MessagingFactory.AcceptMessageSession]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory.acceptmessagesession?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactory_AcceptMessageSession
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[NuGet]: http://nuget.org/packages/WindowsAzure.ServiceBus/
[Azure portal]: https://portal.azure.com
[Vue d’ensemble du protocole AMQP de Service Bus]: service-bus-amqp-overview.md
[Prise en charge d’AMQP 1.0 dans les rubriques et files d’attente partitionnées Service Bus]: service-bus-partitioned-queues-and-topics-amqp-overview.md
[AMQP dans Service Bus pour Windows Server]: https://msdn.microsoft.com/library/dn574799.aspx
