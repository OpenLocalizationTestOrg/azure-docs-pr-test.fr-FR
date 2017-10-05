---
title: "Envoyer des événements vers Azure Event Hubs avec Java | Microsoft Docs"
description: "Prise en main de l’envoi vers Event Hubs avec Java"
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
ms.openlocfilehash: b31771001989e20b88bc8d7bca1afceb58ec197c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="send-events-to-azure-event-hubs-using-java"></a><span data-ttu-id="a7a3f-103">Envoyer des événements vers Azure Event Hubs avec Java</span><span class="sxs-lookup"><span data-stu-id="a7a3f-103">Send events to Azure Event Hubs using Java</span></span>

## <a name="introduction"></a><span data-ttu-id="a7a3f-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="a7a3f-104">Introduction</span></span>
<span data-ttu-id="a7a3f-105">Les concentrateurs d’événements représentent un système d’ingestion à l’extensibilité élevée en mesure d’absorber des millions d’événements par seconde, ce qui permet à une application de traiter et d’analyser les quantités énormes de données produites par vos périphériques connectés et vos applications.</span><span class="sxs-lookup"><span data-stu-id="a7a3f-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="a7a3f-106">Une fois collectées dans un concentrateur d’événements, les données peuvent être transformées et stockées à l’aide de n’importe quel fournisseur d’analyses en temps réel ou d’un cluster de stockage.</span><span class="sxs-lookup"><span data-stu-id="a7a3f-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="a7a3f-107">Pour plus d’informations, consultez la section [Vue d’ensemble d’Event Hubs][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="a7a3f-107">For more information, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="a7a3f-108">Ce didacticiel explique comment envoyer des événements vers un concentrateur d’événements à l’aide d’une application console en Java.</span><span class="sxs-lookup"><span data-stu-id="a7a3f-108">This tutorial shows how to send events to an event hub by using a console application in Java.</span></span> <span data-ttu-id="a7a3f-109">Pour recevoir des événements avec le processeur d’événements Java, consultez [cet article](event-hubs-java-get-started-receive-eph.md) ou cliquez sur le langage de réception approprié dans le sommaire à gauche.</span><span class="sxs-lookup"><span data-stu-id="a7a3f-109">To receive events using the Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="a7a3f-110">Pour effectuer ce didacticiel, vous devrez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a7a3f-110">In order to complete this tutorial, you will need the following:</span></span>

* <span data-ttu-id="a7a3f-111">Un environnement de développement Java.</span><span class="sxs-lookup"><span data-stu-id="a7a3f-111">A Java development environment.</span></span> <span data-ttu-id="a7a3f-112">Pour ce didacticiel, nous partons du principe que la solution utilisée est [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="a7a3f-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="a7a3f-113">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="a7a3f-113">An active Azure account.</span></span> <br/><span data-ttu-id="a7a3f-114">Si vous ne possédez pas de compte, vous pouvez créer un compte gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="a7a3f-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="a7a3f-115">Pour plus d'informations, consultez la page <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Version d'évaluation gratuite d'Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="a7a3f-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="send-messages-to-event-hubs"></a><span data-ttu-id="a7a3f-116">Envoi de messages vers Event Hubs</span><span class="sxs-lookup"><span data-stu-id="a7a3f-116">Send messages to Event Hubs</span></span>
<span data-ttu-id="a7a3f-117">La bibliothèque cliente de Java pour les concentrateurs d’événements peut être utilisée dans les projets Maven à partir du [référentiel central Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="a7a3f-117">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span> <span data-ttu-id="a7a3f-118">Vous pouvez référencer cette bibliothèque à l’aide de la déclaration de dépendance suivante au sein de votre fichier de projet Maven :</span><span class="sxs-lookup"><span data-stu-id="a7a3f-118">You can reference this library using the following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

<span data-ttu-id="a7a3f-119">Pour différents types d’environnements de génération, vous pouvez obtenir explicitement les fichiers JAR les plus récents à partir du [référentiel central Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="a7a3f-119">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span>  

<span data-ttu-id="a7a3f-120">Pour un éditeur d’événements simple, importez le package *com.microsoft.azure.eventhubs* pour les classes clientes Event Hubs et le package *com.microsoft.azure.servicebus* pour les classes utilitaires, telles que les exceptions courantes qui sont partagées avec le client de messagerie Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a7a3f-120">For a simple event publisher, import the *com.microsoft.azure.eventhubs* package for the Event Hubs client classes and the *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with the Azure Service Bus messaging client.</span></span> 

<span data-ttu-id="a7a3f-121">Pour l’exemple suivant, créez tout d’abord un nouveau projet Maven pour une application de console/shell dans votre environnement de développement Java favori.</span><span class="sxs-lookup"><span data-stu-id="a7a3f-121">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="a7a3f-122">Nommez la classe `Send`.</span><span class="sxs-lookup"><span data-stu-id="a7a3f-122">Name the class `Send`.</span></span>     

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

<span data-ttu-id="a7a3f-123">Remplacez l’espace de noms et les noms du concentrateur d’événements par les valeurs utilisées lorsque vous avez créé le concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="a7a3f-123">Replace the namespace and event hub names with the values used when you created the event hub.</span></span>

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

<span data-ttu-id="a7a3f-124">Ensuite, créez un événement unique en transformant une chaîne dans son encodage UTF-8 octets.</span><span class="sxs-lookup"><span data-stu-id="a7a3f-124">Then, create a singular event by transforming a string into its UTF-8 byte encoding.</span></span> <span data-ttu-id="a7a3f-125">Enfin, créez une nouvelle instance cliente Event Hubs à partir de la chaîne de connexion et envoyez le message.</span><span class="sxs-lookup"><span data-stu-id="a7a3f-125">Then, create a new Event Hubs client instance from the connection string and send the message.</span></span>   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a><span data-ttu-id="a7a3f-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a7a3f-126">Next steps</span></span>
<span data-ttu-id="a7a3f-127">Vous pouvez en apprendre plus sur Event Hubs en consultant les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="a7a3f-127">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="a7a3f-128">Recevoir des événements avec EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="a7a3f-128">Receive events using the EventProcessorHost</span></span>](event-hubs-java-get-started-receive-eph.md)
* <span data-ttu-id="a7a3f-129">[Vue d’ensemble des hubs d’événements][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="a7a3f-129">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="a7a3f-130">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="a7a3f-130">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="a7a3f-131">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="a7a3f-131">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md