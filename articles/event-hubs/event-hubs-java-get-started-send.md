---
title: "aaaSend événements tooAzure concentrateurs d’événements à l’aide de Java | Documents Microsoft"
description: "Commencer l’envoi des concentrateurs tooEvent à l’aide de Java"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: ec537b8849a0cb49855e76c0c0ef4093108fe83c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-java"></a>Envoyer des événements de concentrateurs d’événements tooAzure à l’aide de Java

## <a name="introduction"></a>Introduction
Concentrateurs d’événements est un système de réception hautement évolutives pouvant millions d’événements par seconde, l’activation d’un tooprocess de l’application de réception et analyser hello des quantités massives de données généré par vos périphériques connectés et les applications. Une fois collectées dans un concentrateur d’événements, les données peuvent être transformées et stockées à l’aide de n’importe quel fournisseur d’analyses en temps réel ou d’un cluster de stockage.

Pour plus d’informations, consultez hello [vue d’ensemble des concentrateurs d’événements][Event Hubs overview].

Ce didacticiel montre comment toosend concentrateur d’événements tooan d’événements à l’aide d’une application de console dans Java. événements de tooreceive à l’aide de la bibliothèque du processeur d’événements Java hôte hello, consultez [cet article](event-hubs-java-get-started-receive-eph.md), ou cliquez sur le langage de réception approprié hello dans la table de gauche hello du contenu.

Dans l’ordre toocomplete ce didacticiel, vous devez hello suivant :

* Un environnement de développement Java. Pour ce didacticiel, nous partons du principe que la solution utilisée est [Eclipse](https://www.eclipse.org/).
* Un compte Azure actif. <br/>Si vous ne possédez pas de compte, vous pouvez créer un compte gratuit en quelques minutes. Pour plus d'informations, consultez la page <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Version d'évaluation gratuite d'Azure</a>.

## <a name="send-messages-tooevent-hubs"></a>Envoyer des messages tooEvent concentrateurs
Hello Java la bibliothèque cliente pour le service Event Hubs est disponible pour une utilisation dans les projets Maven hello [référentiel Central de Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22). Vous pouvez faire référence à cette bibliothèque à l’aide de hello après la déclaration de dépendance à l’intérieur de votre fichier de projet Maven :    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

Pour différents types d’environnements de build, vous pouvez obtenir explicitement des fichiers JAR de hello dernière version publiée de hello [référentiel Central de Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).  

Pour un serveur de publication d’événement simple, importer hello *com.microsoft.azure.eventhubs* package pour les classes clientes de concentrateurs d’événements hello et hello *com.microsoft.azure.servicebus* le package pour ces classes d’utilitaire en tant qu’exceptions courantes qui sont partagées avec le client de messagerie Service Bus de Azure hello. 

Pourquoi suivant l’exemple, tout d’abord créer un projet pour une application console/shell Maven dans votre environnement de développement Java favori. Nom de classe hello `Send`.     

```java
import java.io.IOException;
import java.nio.charset.*;
import java.util.*;
import java.util.concurrent.ExecutionException;

import com.microsoft.azure.eventhubs.*;
import com.microsoft.azure.servicebus.*;

public class Send
{
    public static void main(String[] args) 
            throws ServiceBusException, ExecutionException, InterruptedException, IOException
    {
```

Remplacer les noms du hub hello espace de noms et des événements avec des valeurs hello utilisés lors de la création du concentrateur d’événements hello.

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

Ensuite, créez un événement unique en transformant une chaîne dans son encodage UTF-8 octets. Ensuite, créez une nouvelle instance de client de concentrateurs d’événements à partir de la chaîne de connexion hello et envoyer le message de type hello.   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :

* [Recevoir des événements à l’aide de hello EventProcessorHost](event-hubs-java-get-started-receive-eph.md)
* [Vue d’ensemble des hubs d’événements][Event Hubs overview]
* [Créer un concentrateur d’événements](event-hubs-create.md)
* [FAQ sur les hubs d'événements](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md