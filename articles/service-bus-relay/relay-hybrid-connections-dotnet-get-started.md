---
title: "aaaGet a démarré avec des connexions hybrides relais dans .NET | Documents Microsoft"
description: "Écrivez une application console C# pour les connexions hybrides Azure Relay."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d1386900-b942-4abf-acfc-38d2ef826253
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 1e4af28e7cd4393c8ca965a149a0b83ebcc44f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a>Prise en main des connexions hybrides Relay
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

Ce didacticiel fournit une introduction trop[connexions hybrides de relais Azure](relay-what-is-it.md#hybrid-connections)et montre comment toouse .NET toocreate une application cliente qui envoie les messages d’application écouteur tooa correspondant. 

## <a name="what-will-be-accomplished"></a>Les opérations que nous allons effectuer
Étant donné que les connexions hybrides requiert un client et un composant serveur, didacticiel de hello crée deux applications console. Voici les étapes hello :

1. Créer un espace de noms de relais, à l’aide de hello portail Azure.
2. Dans cet espace de noms, à l’aide de hello portail Azure, créez une connexion hybride.
3. Écrire des messages tooreceive d’application une console de serveur (récepteur).
4. Écrire des messages d’application toosend une console client (expéditeur).

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel, vous devez hello suivant des conditions préalables :

1. [Visual Studio 2015 ou une version ultérieure](http://www.visualstudio.com). exemples de Hello dans ce didacticiel utilisent Visual Studio 2017.
2. Un abonnement Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Créer un espace de noms à l’aide de hello portail Azure
Si vous avez déjà créé un espace de noms de relais, raccourcis toohello [créer une connexion hybride à l’aide de hello portail Azure](#2-create-a-hybrid-connection-using-the-azure-portal) section.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Créez une connexion hybride à l’aide de hello portail Azure
Si vous avez déjà créé une connexion hybride, raccourcis toohello [créer une application serveur](#3-create-a-server-application-listener) section.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Créer une application de serveur (récepteur)
toolisten et recevoir des messages à partir de hello relais, nous écrirons une application console c# à l’aide de Visual Studio.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. Créer une application cliente (expéditeur)
toohello de messages toosend de relais, nous écrirons une application console c# à l’aide de Visual Studio.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Exécuter des applications de hello
1. Exécutez l’application de serveur hello.
2. Exécutez l’application cliente de hello et saisir du texte.
3. Vérifiez que serveur hello application console sorties hello texte qui a été entré dans l’application cliente de hello.

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

Félicitations, vous avez créé une application de connexions hybrides de bout en bout.

## <a name="next-steps"></a>Étapes suivantes :
* [FAQ Relay](relay-faq.md)
* [Créer un espace de noms](relay-create-namespace-portal.md)
* [Prise en main de Node](relay-hybrid-connections-node-get-started.md)

