---
title: "Envoyer des événements vers Azure Event Hubs avec C | Microsoft Docs"
description: "Envoyer des événements vers Azure Event Hubs avec C"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: c
ms.devlang: csharp
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a615ee39b6c3731cc7df366e9fabeed5219a71b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="send-events-to-azure-event-hubs-using-c"></a><span data-ttu-id="43a81-103">Envoyer des événements vers Azure Event Hubs avec C</span><span class="sxs-lookup"><span data-stu-id="43a81-103">Send events to Azure Event Hubs using C</span></span>

## <a name="introduction"></a><span data-ttu-id="43a81-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="43a81-104">Introduction</span></span>
<span data-ttu-id="43a81-105">Les concentrateurs d’événements représentent un système d’ingestion à l’extensibilité élevée en mesure d’absorber des millions d’événements par seconde, ce qui permet à une application de traiter et d’analyser les quantités énormes de données produites par vos périphériques connectés et vos applications.</span><span class="sxs-lookup"><span data-stu-id="43a81-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="43a81-106">Une fois collectées dans un concentrateur d’événements, les données peuvent être transformées et stockées à l’aide de n’importe quel fournisseur d’analyses en temps réel ou d’un cluster de stockage.</span><span class="sxs-lookup"><span data-stu-id="43a81-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="43a81-107">Pour plus d’informations, consultez la [Vue d’ensemble des concentrateurs d’événements][Vue d’ensemble des concentrateurs d’événements].</span><span class="sxs-lookup"><span data-stu-id="43a81-107">For more information, please see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="43a81-108">Dans ce didacticiel, vous allez apprendre à envoyer des événements à un Event Hub à l’aide d’une application console en C. Pour recevoir des événements, cliquez sur le langage de réception approprié dans la table des matières de gauche.</span><span class="sxs-lookup"><span data-stu-id="43a81-108">In this tutorial, you will learn how to send events to an event hub using a console application in C. To receive events, click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="43a81-109">Pour réaliser ce didacticiel, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="43a81-109">To complete this tutorial, you will need the following:</span></span>

* <span data-ttu-id="43a81-110">Un environnement de développement en C.</span><span class="sxs-lookup"><span data-stu-id="43a81-110">A C development environment.</span></span> <span data-ttu-id="43a81-111">Pour ce didacticiel, nous partirons du principe que la pile GCC est sur une machine virtuelle Linux Azure dotée du système d’exploitation Ubuntu 14.04.</span><span class="sxs-lookup"><span data-stu-id="43a81-111">For this tutorial, we will assume the gcc stack on an Azure Linux VM with Ubuntu 14.04.</span></span>
* <span data-ttu-id="43a81-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="43a81-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span></span>
* <span data-ttu-id="43a81-113">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="43a81-113">An active Azure account.</span></span> <span data-ttu-id="43a81-114">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="43a81-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="43a81-115">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="43a81-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="send-messages-to-event-hubs"></a><span data-ttu-id="43a81-116">Envoi de messages vers Event Hubs</span><span class="sxs-lookup"><span data-stu-id="43a81-116">Send messages to Event Hubs</span></span>
<span data-ttu-id="43a81-117">Dans cette section, nous allons écrire une application en C pour envoyer des événements à votre concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="43a81-117">In this section we write a C app to send events to your event hub.</span></span> <span data-ttu-id="43a81-118">Le code utilise la bibliothèque Proton AMQP du [projet Apache Qpid](http://qpid.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="43a81-118">The code uses the Proton AMQP library from the [Apache Qpid project](http://qpid.apache.org/).</span></span> <span data-ttu-id="43a81-119">Cette approche est similaire à l’utilisation des rubriques et des files d’attente Service Bus avec AMQP en partant du langage C comme indiqué [ici](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span><span class="sxs-lookup"><span data-stu-id="43a81-119">This is analogous to using Service Bus queues and topics with AMQP from C as shown [here](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span></span> <span data-ttu-id="43a81-120">Pour plus d’informations, consultez la [documentation Qpid Proton](http://qpid.apache.org/proton/index.html).</span><span class="sxs-lookup"><span data-stu-id="43a81-120">For more information, see [Qpid Proton documentation](http://qpid.apache.org/proton/index.html).</span></span>

1. <span data-ttu-id="43a81-121">Dans la [page Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html), suivez les instructions d’installation de Qpid Proton correspondant à votre environnement.</span><span class="sxs-lookup"><span data-stu-id="43a81-121">From the [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html), follow the instructions to install Qpid Proton, depending on your environment.</span></span>
2. <span data-ttu-id="43a81-122">Pour compiler la bibliothèque Proton, installez les packages suivants :</span><span class="sxs-lookup"><span data-stu-id="43a81-122">To compile the Proton library, install the following packages:</span></span>
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. <span data-ttu-id="43a81-123">Téléchargez la [bibliothèque Qpid Proton](http://qpid.apache.org/proton/index.html) et effectuez son extraction, par exemple :</span><span class="sxs-lookup"><span data-stu-id="43a81-123">Download the [Qpid Proton library](http://qpid.apache.org/proton/index.html), and extract it, e.g.:</span></span>
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. <span data-ttu-id="43a81-124">Créez un répertoire de build, compilez-le et installez-le :</span><span class="sxs-lookup"><span data-stu-id="43a81-124">Create a build directory, compile and install:</span></span>
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. <span data-ttu-id="43a81-125">Dans le répertoire de travail, créez un fichier nommé **sender.c** avec le code suivant.</span><span class="sxs-lookup"><span data-stu-id="43a81-125">In your work directory, create a new file called **sender.c** with the following code.</span></span> <span data-ttu-id="43a81-126">N’oubliez pas de remplacer la valeur du nom de votre concentrateur d’événements et du nom de votre espace de noms.</span><span class="sxs-lookup"><span data-stu-id="43a81-126">Remember to substitute the value for your event hub name and namespace name.</span></span> <span data-ttu-id="43a81-127">Vous devez également remplacer une version codée URL de la clé pour le **SendRule** précédemment créé.</span><span class="sxs-lookup"><span data-stu-id="43a81-127">You must also substitute a URL-encoded version of the key for the **SendRule** created earlier.</span></span> <span data-ttu-id="43a81-128">Vous pouvez la coder par URL [ici](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="43a81-128">You can URL-encode it [here](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
   
    ```c
    #include "proton/message.h"
    #include "proton/messenger.h"
   
    #include <getopt.h>
    #include <proton/util.h>
    #include <sys/time.h>
    #include <stddef.h>
    #include <stdio.h>
    #include <string.h>
    #include <unistd.h>
    #include <stdlib.h>
   
    #define check(messenger)                                                     
      {                                                                          
        if(pn_messenger_errno(messenger))                                        
        {                                                                        
          printf("check\n");                                                     
          die(__FILE__, __LINE__, pn_error_text(pn_messenger_error(messenger))); 
        }                                                                        
      }  
   
    pn_timestamp_t time_now(void)
    {
      struct timeval now;
      if (gettimeofday(&now, NULL)) pn_fatal("gettimeofday failed\n");
      return ((pn_timestamp_t)now.tv_sec) * 1000 + (now.tv_usec / 1000);
    }  
   
    void die(const char *file, int line, const char *message)
    {
      printf("Dead\n");
      fprintf(stderr, "%s:%i: %s\n", file, line, message);
      exit(1);
    }
   
    int sendMessage(pn_messenger_t * messenger) {
        char * address = (char *) "amqps://SendRule:{Send Rule key}@{namespace name}.servicebus.windows.net/{event hub name}";
        char * msgtext = (char *) "Hello from C!";
   
        pn_message_t * message;
        pn_data_t * body;
        message = pn_message();
   
        pn_message_set_address(message, address);
        pn_message_set_content_type(message, (char*) "application/octect-stream");
        pn_message_set_inferred(message, true);
   
        body = pn_message_body(message);
        pn_data_put_binary(body, pn_bytes(strlen(msgtext), msgtext));
   
        pn_messenger_put(messenger, message);
        check(messenger);
        pn_messenger_send(messenger, 1);
        check(messenger);
   
        pn_message_free(message);
    }
   
    int main(int argc, char** argv) {
        printf("Press Ctrl-C to stop the sender process\n");
   
        pn_messenger_t *messenger = pn_messenger(NULL);
        pn_messenger_set_outgoing_window(messenger, 1);
        pn_messenger_start(messenger);
   
        while(true) {
            sendMessage(messenger);
            printf("Sent message\n");
            sleep(1);
        }
   
        // release messenger resources
        pn_messenger_stop(messenger);
        pn_messenger_free(messenger);
   
        return 0;
    }
    ```
6. <span data-ttu-id="43a81-129">Compilez le fichier (en supposant que **gcc**est défini) :</span><span class="sxs-lookup"><span data-stu-id="43a81-129">Compile the file, assuming **gcc**:</span></span>
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > <span data-ttu-id="43a81-130">Dans ce code, nous utilisons une fenêtre sortante de 1 pour forcer l’envoi des messages dès que possible.</span><span class="sxs-lookup"><span data-stu-id="43a81-130">In this code, we use an outgoing window of 1 to force the messages out as soon as possible.</span></span> <span data-ttu-id="43a81-131">En général, votre application doit essayer d’envoyer les messages par lot pour augmenter le débit.</span><span class="sxs-lookup"><span data-stu-id="43a81-131">In general, your application should try to batch messages to increase throughput.</span></span> <span data-ttu-id="43a81-132">Consultez la [page Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html) pour plus d’informations sur l’utilisation de la bibliothèque Qpid Proton dans l’ensemble des environnements et à partir des plateformes pour lesquelles des liaisons sont fournies (actuellement Perl, PHP, Python et Ruby).</span><span class="sxs-lookup"><span data-stu-id="43a81-132">See the [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html) for information about how to use the Qpid Proton library in this and other environments, and from platforms for which bindings are provided (currently Perl, PHP, Python, and Ruby).</span></span>


## <a name="next-steps"></a><span data-ttu-id="43a81-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="43a81-133">Next steps</span></span>
<span data-ttu-id="43a81-134">Vous pouvez en apprendre plus sur Event Hubs en consultant les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="43a81-134">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="43a81-135">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="43a81-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md
)
* [<span data-ttu-id="43a81-136">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="43a81-136">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="43a81-137">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="43a81-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
