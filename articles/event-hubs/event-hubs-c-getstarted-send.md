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
# <a name="send-events-tooazure-event-hubs-using-c"></a>Envoyer des événements de concentrateurs d’événements tooAzure à l’aide de C

## <a name="introduction"></a>Introduction
Concentrateurs d’événements est un système de réception hautement évolutives pouvant millions d’événements par seconde, l’activation d’un tooprocess de l’application de réception et analyser hello des quantités massives de données généré par vos périphériques connectés et les applications. Une fois collectées dans un concentrateur d’événements, les données peuvent être transformées et stockées à l’aide de n’importe quel fournisseur d’analyses en temps réel ou d’un cluster de stockage.

Pour plus d’informations, consultez hello [vue d’ensemble des concentrateurs d’événements] [vue d’ensemble des concentrateurs d’événements].

Dans ce didacticiel, vous allez apprendre comment concentrateur d’événements toosend événements tooan à l’aide d’une application console dans tooreceive c. les événements, cliquez sur hello réception langue dans la table de gauche hello du contenu.

toocomplete ce didacticiel, vous devez hello suivant :

* Un environnement de développement en C. Pour ce didacticiel, nous allons supposer la pile de gcc hello sur une machine virtuelle Linux de Azure avec Ubuntu 14.04.
* [Microsoft Visual Studio](https://www.visualstudio.com/).
* Un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="send-messages-tooevent-hubs"></a>Envoyer des messages tooEvent concentrateurs
Dans cette section, nous écrivons un concentrateur d’événements C application toosend événements tooyour. Hello de code utilise la bibliothèque de Proton AMQP hello de hello [projet Apache Qpid](http://qpid.apache.org/). Il s’agit files d’attente de Service Bus toousing analogue et rubriques avec AMQP c comme [ici](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504). Pour plus d’informations, consultez la [documentation Qpid Proton](http://qpid.apache.org/proton/index.html).

1. À partir de hello [page Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html), suivez hello instructions tooinstall Qpid Proton, selon votre environnement.
2. toocompile hello bibliothèque Proton, installez hello suivant des packages :
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. Télécharger hello [bibliothèque Qpid Proton](http://qpid.apache.org/proton/index.html)et l’extraire, par exemple :
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. Créez un répertoire de build, compilez-le et installez-le :
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. Dans votre répertoire de travail, créez un nouveau fichier appelé **sender.c** avec hello suivant de code. N’oubliez pas de valeur de hello toosubstitute pour votre nom de hub d’événements et le nom de l’espace de noms. Vous devez également remplacer une version codée URL de clé hello hello **SendRule** créé précédemment. Vous pouvez la coder par URL [ici](http://www.w3schools.com/tags/ref_urlencode.asp).
   
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
6. Compilez le fichier de hello, en supposant que **gcc**:
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > Dans ce code, nous utilisons une fenêtre sortante 1 tooforce de message d’appel sortant dès que possible. En général, votre application doit essayer de débit de tooincrease toobatch messages. Consultez hello [page Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html) pour plus d’informations sur la façon dont toouse hello bibliothèque Qpid Proton dans cette section et autres environnements et de plateformes dont les liaisons sont fournis (actuellement Perl, PHP, Python et Ruby).


## <a name="next-steps"></a>Étapes suivantes
Vous pouvez plus d’informations sur les concentrateurs d’événements en visitant hello suivant liens :

* [Vue d’ensemble des hubs d’événements](event-hubs-what-is-event-hubs.md
)
* [Créer un concentrateur d’événements](event-hubs-create.md)
* [FAQ sur les hubs d'événements](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
