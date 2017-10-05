---
title: Prise en main des connexions hybrides Azure Relay dans .NET | Microsoft Docs
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
ms.openlocfilehash: 1af23bfd46dd7d3781505473f7c1d86e65ea9bc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a>Prise en main des connexions hybrides Relay
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

Ce tutoriel présente les [connexions hybrides Azure Relay](relay-what-is-it.md#hybrid-connections) et explique comment utiliser .NET pour créer une application cliente qui envoie des messages à une application d’écouteur correspondante. 

## <a name="what-will-be-accomplished"></a>Les opérations que nous allons effectuer
Étant donné que les connexions hybrides nécessitent un client et un serveur, le didacticiel crée deux applications de console. Voici la procédure à suivre :

1. Créer un espace de noms Relay à l’aide du portail Azure.
2. Créer une connexion hybride dans cet espace de noms, à l’aide du portail Azure.
3. Écrire une application de console (écouteur) de serveur pour recevoir des messages.
4. Écrire une application de console (expéditeur) de client pour envoyer des messages.

## <a name="prerequisites"></a>Composants requis

Voici les prérequis pour effectuer ce tutoriel :

1. [Visual Studio 2015 ou une version ultérieure](http://www.visualstudio.com). Les exemples de ce didacticiel utilisent Visual Studio 2017.
2. Un abonnement Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a>1. Créer un espace de noms à l’aide du Portail Azure
Si vous avez déjà créé un espace de noms Relay, passez à la section [Créer une connexion hybride à l’aide du portail Azure](#2-create-a-hybrid-connection-using-the-azure-portal).

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-the-azure-portal"></a>2. Créer une connexion hybride à l’aide du portail Azure
Si vous avez déjà créé une connexion hybride, passez à la section [Créer une application de serveur](#3-create-a-server-application-listener).

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Créer une application de serveur (récepteur)
Pour écouter et recevoir des messages à partir de Relay, nous allons écrire une application de console C# à l’aide de Visual Studio.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. Créer une application cliente (expéditeur)
Pour envoyer des messages à Relay, nous allons écrire une application de console C# à l’aide de Visual Studio.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-the-applications"></a>5. Exécution des applications
1. Exécutez l’application de serveur.
2. Exécutez l’application cliente et entrez du texte.
3. Vérifiez que la console d’application de serveur renvoie le texte entré dans l’application cliente.

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

Félicitations, vous avez créé une application de connexions hybrides de bout en bout.

## <a name="next-steps"></a>Étapes suivantes :
* [FAQ Relay](relay-faq.md)
* [Créer un espace de noms](relay-create-namespace-portal.md)
* [Prise en main de Node](relay-hybrid-connections-node-get-started.md)

