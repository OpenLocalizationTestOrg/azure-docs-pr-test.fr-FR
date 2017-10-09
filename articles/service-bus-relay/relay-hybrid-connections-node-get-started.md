---
title: "aaaGet a démarré avec des connexions hybrides relais dans le nœud | Documents Microsoft"
description: "Écrivez une application console Node.js pour les connexions hybrides Azure Relay."
services: service-bus-relay
documentationcenter: node
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e44e4867-3cf3-46be-8f8a-7671e2013bc4
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: node
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 235548399570074f7fd160fec28de8d3633625c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a>Prise en main des connexions hybrides Relay

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

Ce didacticiel fournit une introduction trop[connexions hybrides de relais Azure](relay-what-is-it.md#hybrid-connections)et montre comment toouse Node.js toocreate une application cliente qui envoie les messages d’application écouteur tooa correspondant. 

## <a name="what-will-be-accomplished"></a>Les opérations que nous allons effectuer

Étant donné que les connexions hybrides nécessitent un client et un serveur, vous allez créer deux applications console dans ce tutoriel. Voici les étapes hello :

1. Créer un espace de noms de relais, à l’aide de hello portail Azure.
2. Créer une connexion hybride, à l’aide de hello portail Azure.
3. Écrire des messages de console application tooreceive un serveur.
4. Écrire un client toosend les messages d’application console.

## <a name="prerequisites"></a>Composants requis

1. [Node.js](https://nodejs.org/en/).
2. Un abonnement Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Créer un espace de noms à l’aide de hello portail Azure

Si vous disposez déjà d’un espace de noms de relais créé, passez toohello [créer une connexion hybride à l’aide de hello portail Azure](#2-create-a-hybrid-connection-using-the-azure-portal) section.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Créez une connexion hybride à l’aide de hello portail Azure

Si vous avez déjà une connexion hybride créée, passez toohello [créer une application serveur](#3-create-a-server-application-listener) section.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Créer une application de serveur (récepteur)

toolisten et recevoir des messages à partir de hello relais, nous écrirons une application de console Node.js.

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. Créer une application cliente (expéditeur)

toosend messages toohello relais, nous écrirons une application de console Node.js.

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Exécuter des applications de hello

1. Exécutez l’application de serveur hello : à partir d’un type d’invite de commande Node.js `node listener.js`.
2. Exécutez l’application cliente de hello : à partir d’un type d’invite de commande Node.js `node sender.js`et entrez du texte.
3. Vérifiez que serveur hello application console sorties hello texte qui a été entré dans l’application cliente de hello.

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

Vous avez créé une application de connexions hybrides complète avec Node.js : félicitations !

## <a name="next-steps"></a>Étapes suivantes :

* [FAQ Relay](relay-faq.md)
* [Créer un espace de noms](relay-create-namespace-portal.md)
* [Prise en main de .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Prise en main de Node](relay-hybrid-connections-node-get-started.md)

