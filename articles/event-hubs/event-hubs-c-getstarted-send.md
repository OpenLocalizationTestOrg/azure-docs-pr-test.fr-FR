---
title: "aaaSend événements tooAzure concentrateurs d’événements à l’aide de C | Documents Microsoft"
description: "Envoyer des événements de concentrateurs d’événements tooAzure à l’aide de C"
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
ms.openlocfilehash: bb53300c070debb4a3658a38df9d3966f08e81ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-c"></a><span data-ttu-id="b8e15-103">Envoyer des événements de concentrateurs d’événements tooAzure à l’aide de C</span><span class="sxs-lookup"><span data-stu-id="b8e15-103">Send events tooAzure Event Hubs using C</span></span>

## <a name="introduction"></a><span data-ttu-id="b8e15-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="b8e15-104">Introduction</span></span>
<span data-ttu-id="b8e15-105">Concentrateurs d’événements est un système de réception hautement évolutives pouvant millions d’événements par seconde, l’activation d’un tooprocess de l’application de réception et analyser hello des quantités massives de données généré par vos périphériques connectés et les applications.</span><span class="sxs-lookup"><span data-stu-id="b8e15-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="b8e15-106">Une fois collectées dans un concentrateur d’événements, les données peuvent être transformées et stockées à l’aide de n’importe quel fournisseur d’analyses en temps réel ou d’un cluster de stockage.</span><span class="sxs-lookup"><span data-stu-id="b8e15-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="b8e15-107">Pour plus d’informations, consultez hello [vue d’ensemble des concentrateurs d’événements] [vue d’ensemble des concentrateurs d’événements].</span><span class="sxs-lookup"><span data-stu-id="b8e15-107">For more information, please see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="b8e15-108">Dans ce didacticiel, vous allez apprendre comment concentrateur d’événements toosend événements tooan à l’aide d’une application console dans tooreceive c. les événements, cliquez sur hello réception langue dans la table de gauche hello du contenu.</span><span class="sxs-lookup"><span data-stu-id="b8e15-108">In this tutorial, you will learn how toosend events tooan event hub using a console application in C. tooreceive events, click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="b8e15-109">toocomplete ce didacticiel, vous devez hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b8e15-109">toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="b8e15-110">Un environnement de développement en C.</span><span class="sxs-lookup"><span data-stu-id="b8e15-110">A C development environment.</span></span> <span data-ttu-id="b8e15-111">Pour ce didacticiel, nous allons supposer la pile de gcc hello sur une machine virtuelle Linux de Azure avec Ubuntu 14.04.</span><span class="sxs-lookup"><span data-stu-id="b8e15-111">For this tutorial, we will assume hello gcc stack on an Azure Linux VM with Ubuntu 14.04.</span></span>
* <span data-ttu-id="b8e15-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="b8e15-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span></span>
* <span data-ttu-id="b8e15-113">Un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="b8e15-113">An active Azure account.</span></span> <span data-ttu-id="b8e15-114">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="b8e15-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b8e15-115">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b8e15-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="b8e15-116">Envoyer des messages tooEvent concentrateurs</span><span class="sxs-lookup"><span data-stu-id="b8e15-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="b8e15-117">Dans cette section, nous écrivons un concentrateur d’événements C application toosend événements tooyour.</span><span class="sxs-lookup"><span data-stu-id="b8e15-117">In this section we write a C app toosend events tooyour event hub.</span></span> <span data-ttu-id="b8e15-118">Hello de code utilise la bibliothèque de Proton AMQP hello de hello [projet Apache Qpid](http://qpid.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="b8e15-118">hello code uses hello Proton AMQP library from hello [Apache Qpid project](http://qpid.apache.org/).</span></span> <span data-ttu-id="b8e15-119">Il s’agit files d’attente de Service Bus toousing analogue et rubriques avec AMQP c comme [ici](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span><span class="sxs-lookup"><span data-stu-id="b8e15-119">This is analogous toousing Service Bus queues and topics with AMQP from C as shown [here](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span></span> <span data-ttu-id="b8e15-120">Pour plus d’informations, consultez la [documentation Qpid Proton](http://qpid.apache.org/proton/index.html).</span><span class="sxs-lookup"><span data-stu-id="b8e15-120">For more information, see [Qpid Proton documentation](http://qpid.apache.org/proton/index.html).</span></span>

1. <span data-ttu-id="b8e15-121">À partir de hello [page Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html), suivez hello instructions tooinstall Qpid Proton, selon votre environnement.</span><span class="sxs-lookup"><span data-stu-id="b8e15-121">From hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html), follow hello instructions tooinstall Qpid Proton, depending on your environment.</span></span>
2. <span data-ttu-id="b8e15-122">toocompile hello bibliothèque Proton, installez hello suivant des packages :</span><span class="sxs-lookup"><span data-stu-id="b8e15-122">toocompile hello Proton library, install hello following packages:</span></span>
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. <span data-ttu-id="b8e15-123">Télécharger hello [bibliothèque Qpid Proton](http://qpid.apache.org/proton/index.html)et l’extraire, par exemple :</span><span class="sxs-lookup"><span data-stu-id="b8e15-123">Download hello [Qpid Proton library](http://qpid.apache.org/proton/index.html), and extract it, e.g.:</span></span>
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. <span data-ttu-id="b8e15-124">Créez un répertoire de build, compilez-le et installez-le :</span><span class="sxs-lookup"><span data-stu-id="b8e15-124">Create a build directory, compile and install:</span></span>
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. <span data-ttu-id="b8e15-125">Dans votre répertoire de travail, créez un nouveau fichier appelé **sender.c** avec hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="b8e15-125">In your work directory, create a new file called **sender.c** with hello following code.</span></span> <span data-ttu-id="b8e15-126">N’oubliez pas de valeur de hello toosubstitute pour votre nom de hub d’événements et le nom de l’espace de noms.</span><span class="sxs-lookup"><span data-stu-id="b8e15-126">Remember toosubstitute hello value for your event hub name and namespace name.</span></span> <span data-ttu-id="b8e15-127">Vous devez également remplacer une version codée URL de clé hello hello **SendRule** créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="b8e15-127">You must also substitute a URL-encoded version of hello key for hello **SendRule** created earlier.</span></span> <span data-ttu-id="b8e15-128">Vous pouvez la coder par URL [ici](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="b8e15-128">You can URL-encode it [here](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
   
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
        printf("Press Ctrl-C toostop hello sender process\n");
   
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
6. <span data-ttu-id="b8e15-129">Compilez le fichier de hello, en supposant que **gcc**:</span><span class="sxs-lookup"><span data-stu-id="b8e15-129">Compile hello file, assuming **gcc**:</span></span>
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > <span data-ttu-id="b8e15-130">Dans ce code, nous utilisons une fenêtre sortante 1 tooforce de message d’appel sortant dès que possible.</span><span class="sxs-lookup"><span data-stu-id="b8e15-130">In this code, we use an outgoing window of 1 tooforce hello messages out as soon as possible.</span></span> <span data-ttu-id="b8e15-131">En général, votre application doit essayer de débit de tooincrease toobatch messages.</span><span class="sxs-lookup"><span data-stu-id="b8e15-131">In general, your application should try toobatch messages tooincrease throughput.</span></span> <span data-ttu-id="b8e15-132">Consultez hello [page Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html) pour plus d’informations sur la façon dont toouse hello bibliothèque Qpid Proton dans cette section et autres environnements et de plateformes dont les liaisons sont fournis (actuellement Perl, PHP, Python et Ruby).</span><span class="sxs-lookup"><span data-stu-id="b8e15-132">See hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html) for information about how toouse hello Qpid Proton library in this and other environments, and from platforms for which bindings are provided (currently Perl, PHP, Python, and Ruby).</span></span>


## <a name="next-steps"></a><span data-ttu-id="b8e15-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b8e15-133">Next steps</span></span>
<span data-ttu-id="b8e15-134">Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :</span><span class="sxs-lookup"><span data-stu-id="b8e15-134">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="b8e15-135">Vue d’ensemble des hubs d’événements</span><span class="sxs-lookup"><span data-stu-id="b8e15-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md
)
* [<span data-ttu-id="b8e15-136">Créer un concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="b8e15-136">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="b8e15-137">FAQ sur les hubs d'événements</span><span class="sxs-lookup"><span data-stu-id="b8e15-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
