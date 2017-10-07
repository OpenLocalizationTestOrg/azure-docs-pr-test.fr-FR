---
title: "aaaIntroduction tooAzure stockage de file d’attente | Documents Microsoft"
description: "Introduction tooAzure stockage de file d’attente"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: robinsh
ms.openlocfilehash: 669effedff7beedde8a119c350a2a70edafedcf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooqueues"></a>Introduction tooQueues

Stockage de file d’attente Azure est un service pour stocker un grand nombre de messages qui sont accessibles à partir de n’importe où dans le monde hello via des appels authentifiés à l’aide de HTTP ou HTTPS. Un message de la file d’attente unique peut être de taille too64 Ko, et une file d’attente peut contenir des millions de messages, des limites de capacité totale de toohello d’un compte de stockage.

## <a name="common-uses"></a>Utilisations courantes

Voici quelques utilisations courantes des files d’attente de stockage :

* Création d’une file d’attente de travail tooprocess asynchrone
* Transmission de messages à partir d’un rôle de travail Azure tooan rôle web Azure

## <a name="queue-service-concepts"></a>Concepts du service File d’attente

Hello service file d’attente contient hello suivant des composants :

![Concepts de File d’attente](./media/storage-queues-introduction/queue1.png)

* **Format d’URL :** files d’attente sont adressables hello suivant le format d’URL :   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    Hello suivant URL traite une file d’attente dans le diagramme de hello :  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **Compte de stockage :** tous accéder tooAzure stockage s’effectue via un compte de stockage. Pour plus d’informations sur la capacité du compte de stockage, consultez la page [Objectifs de performance et évolutivité du stockage Azure](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) .

* **File d’attente :** une file d’attente contient un ensemble de messages. Tous les messages doivent être dans une file d’attente. Notez que ce nom de file d’attente hello doit être en minuscule. Pour plus d'informations sur l’affectation de noms à des files d’attente, consultez [Affectation de noms pour les files d'attente et les métadonnées](https://msdn.microsoft.com/library/azure/dd179349.aspx).

* **Message :** un message, dans n’importe quel format, des too64 Ko. Hello durée maximale pendant laquelle un message peut rester dans la file d’attente hello est de sept jours.

## <a name="next-steps"></a>Étapes suivantes

* [Créer un compte de stockage](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [Bien démarrer avec les files d’attente en utilisant .NET](storage-dotnet-how-to-use-queues.md)
