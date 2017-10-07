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
# <a name="send-events-tooazure-event-hubs-using-java"></a><span data-ttu-id="c0c15-103">Envoyer des événements de concentrateurs d’événements tooAzure à l’aide de Java</span><span class="sxs-lookup"><span data-stu-id="c0c15-103">Send events tooAzure Event Hubs using Java</span></span>

## <a name="introduction"></a><span data-ttu-id="c0c15-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="c0c15-104">Introduction</span></span>
<span data-ttu-id="c0c15-105">Concentrateurs d’événements est un système de réception hautement évolutives pouvant millions d’événements par seconde, l’activation d’un tooprocess de l’application de réception et analyser hello des quantités massives de données généré par vos périphériques connectés et les applications.</span><span class="sxs-lookup"><span data-stu-id="c0c15-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="c0c15-106">Une fois collectées dans un concentrateur d’événements, les données peuvent être transformées et stockées à l’aide de n’importe quel fournisseur d’analyses en temps réel ou d’un cluster de stockage.</span><span class="sxs-lookup"><span data-stu-id="c0c15-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="c0c15-107">Pour plus d’informations, consultez hello [vue d’ensemble des concentrateurs d’événements][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="c0c15-107">For more information, see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="c0c15-108">Ce didacticiel montre comment toosend concentrateur d’événements tooan d’événements à l’aide d’une application de console dans Java.</span><span class="sxs-lookup"><span data-stu-id="c0c15-108">This tutorial shows how toosend events tooan event hub by using a console application in Java.</span></span> <span data-ttu-id="c0c15-109">événements de tooreceive à l’aide de la bibliothèque du processeur d’événements Java hôte hello, consultez [cet article](event-hubs-java-get-started-receive-eph.md), ou cliquez sur le langage de réception approprié hello dans la table de gauche hello du contenu.</span><span class="sxs-lookup"><span data-stu-id="c0c15-109">tooreceive events using hello Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="c0c15-110">Dans l’ordre toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="c0c15-110">In order toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="c0c15-111">Un environnement de développement Java.</span><span class="sxs-lookup"><span data-stu-id="c0c15-111">A Java development environment.</span></span> <span data-ttu-id="c0c15-112">Pour ce didacticiel, nous partons du principe que la solution utilisée est [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="c0c15-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="c0c15-113">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="c0c15-113">An active Azure account.</span></span> <br/><span data-ttu-id="c0c15-114">Si vous ne possédez pas de compte, vous pouvez créer un compte gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="c0c15-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="c0c15-115">Pour plus d'informations, consultez la page <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Version d'évaluation gratuite d'Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="c0c15-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="c0c15-116">Envoyer des messages tooEvent concentrateurs</span><span class="sxs-lookup"><span data-stu-id="c0c15-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="c0c15-117">Hello Java la bibliothèque cliente pour le service Event Hubs est disponible pour une utilisation dans les projets Maven hello [référentiel Central de Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="c0c15-117">hello Java client library for Event Hubs is available for use in Maven projects from hello [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span> <span data-ttu-id="c0c15-118">Vous pouvez faire référence à cette bibliothèque à l’aide de hello après la déclaration de dépendance à l’intérieur de votre fichier de projet Maven :</span><span class="sxs-lookup"><span data-stu-id="c0c15-118">You can reference this library using hello following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

<span data-ttu-id="c0c15-119">Pour différents types d’environnements de build, vous pouvez obtenir explicitement des fichiers JAR de hello dernière version publiée de hello [référentiel Central de Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="c0c15-119">For different types of build environments, you can explicitly obtain hello latest released JAR files from hello [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span>  

<span data-ttu-id="c0c15-120">Pour un serveur de publication d’événement simple, importer hello *com.microsoft.azure.eventhubs* package pour les classes clientes de concentrateurs d’événements hello et hello *com.microsoft.azure.servicebus* le package pour ces classes d’utilitaire en tant qu’exceptions courantes qui sont partagées avec le client de messagerie Service Bus de Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c0c15-120">For a simple event publisher, import hello *com.microsoft.azure.eventhubs* package for hello Event Hubs client classes and hello *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with hello Azure Service Bus messaging client.</span></span> 

<span data-ttu-id="c0c15-121">Pourquoi suivant l’exemple, tout d’abord créer un projet pour une application console/shell Maven dans votre environnement de développement Java favori.</span><span class="sxs-lookup"><span data-stu-id="c0c15-121">For hello following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="c0c15-122">Nom de classe hello `Send`.</span><span class="sxs-lookup"><span data-stu-id="c0c15-122">Name hello class `Send`.</span></span>     

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

<span data-ttu-id="c0c15-123">Remplacer les noms du hub hello espace de noms et des événements avec des valeurs hello utilisés lors de la création du concentrateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="c0c15-123">Replace hello namespace and event hub names with hello values used when you created hello event hub.</span></span>

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

<span data-ttu-id="c0c15-124">Ensuite, créez un événement unique en transformant une chaîne dans son encodage UTF-8 octets.</span><span class="sxs-lookup"><span data-stu-id="c0c15-124">Then, create a singular event by transforming a string into its UTF-8 byte encoding.</span></span> <span data-ttu-id="c0c15-125">Ensuite, créez une nouvelle instance de client de concentrateurs d’événements à partir de la chaîne de connexion hello et envoyer le message de type hello.</span><span class="sxs-lookup"><span data-stu-id="c0c15-125">Then, create a new Event Hubs client instance from hello connection string and send hello message.</span></span>   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a><span data-ttu-id="c0c15-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c0c15-126">Next steps</span></span>
<span data-ttu-id="c0c15-127">Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="c0c15-127">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="c0c15-128">Recevoir des événements à l’aide de hello EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="c0c15-128">Receive events using hello EventProcessorHost</span></span>](event-hubs-java-get-started-receive-eph.md)
* <span data-ttu-id="c0c15-129">[Vue d’ensemble des hubs d’événements][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="c0c15-129">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="c0c15-130">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="c0c15-130">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="c0c15-131">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="c0c15-131">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md