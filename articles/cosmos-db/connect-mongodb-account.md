---
title: "chaîne de connexion aaaMongoDB pour un compte de base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment tooconnect votre tooan d’application MongoDB Azure Cosmos DB compte à l’aide d’une chaîne de connexion MongoDB."
keywords: "chaîne de connexion mongodb"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a>Se connecter à un tooAzure d’application MongoDB Cosmos DB
Découvrez comment tooconnect votre tooan d’application MongoDB Azure Cosmos DB compte à l’aide d’une chaîne de connexion MongoDB. Vous pouvez ensuite utiliser une base de données de la base de données Azure Cosmos en tant que données de hello stocker pour votre application MongoDB. 

Ce didacticiel fournit des informations de chaîne de connexion tooretrieve deux façons :

- [Hello quick start (méthode)](#QuickstartConnection), pour une utilisation avec les pilotes .NET, Node.js, MongoDB Shell, Java et Python
- [Hello de méthode de chaîne de connexion personnalisée](#GetCustomConnection), pour une utilisation avec d’autres pilotes

## <a name="prerequisites"></a>Composants requis

- Un compte Azure. Si vous ne possédez pas de compte Azure, vous pouvez créer un [compte Azure gratuit](https://azure.microsoft.com/free/) dès maintenant. 
- Un compte Azure Cosmos DB. Pour obtenir des instructions, consultez [créer une application web de MongoDB API avec .NET et hello Azure portal](create-mongodb-dotnet.md).

## <a id="QuickstartConnection"></a>Obtenir la chaîne de connexion MongoDB hello à l’aide de démarrage rapide de hello
1. Dans un navigateur Internet, connectez-vous toohello [portail Azure](https://portal.azure.com).
2. Bonjour **base de données Azure Cosmos** panneau, sélectionnez hello des API pour MongoDB compte. 
3. Dans le volet gauche de hello du Panneau de compte hello, cliquez sur **démarrage rapide**. 
4. Choisissez votre plateforme (**.NET**, **Node.js**, **MongoDB Shell**, **Java** ou **Python**). Si votre pilote ou outil n’est pas répertorié, ne vous inquiétez pas, nous développons en permanence de nouveaux extraits de code de connexion. Veuillez commenter ci-dessous vous aimeriez toosee. toolearn comment toocraft votre propre connexion, lecture [obtenir des informations de chaîne de connexion du compte hello](#GetCustomConnection).
5. Copiez et collez l’extrait de code hello dans votre application MongoDB.

    ![Panneau Démarrage rapide](./media/connect-mongodb-account/QuickStartBlade.png)

## <a id="GetCustomConnection"></a>Obtenir toocustomize de chaîne de connexion de MongoDB hello
1. Dans un navigateur Internet, connectez-vous toohello [portail Azure](https://portal.azure.com).
2. Bonjour **base de données Azure Cosmos** panneau, sélectionnez hello des API pour MongoDB compte. 
3. Dans le volet gauche de hello du Panneau de compte hello, cliquez sur **chaîne de connexion**. 
4. Hello **chaîne de connexion** panneau s’ouvre. Il a toohello compte de tous les hello informations tooconnect nécessaires à l’aide d’un pilote pour MongoDB, y compris une chaîne de connexion prédéfini.

    ![Panneau Chaîne de connexion](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a>Exigences relatives à la chaîne de connexion
> [!Important]
> Azure Cosmos DB obéit à des normes et à des exigences strictes en matière de sécurité. Les comptes Azure Cosmos DB requièrent une authentification et une communication sécurisée via *SSL*. 
>
>

Base de données Azure Cosmos prend en charge hello MongoDB connexion chaîne URI format standard, avec quelques exigences spécifiques : comptes de base de données Azure Cosmos requièrent l’authentification et communication sécurisée via SSL. Par conséquent, le format de chaîne de connexion hello est :

    mongodb://username:password@host:port/[database]?ssl=true

les valeurs de cette chaîne Hello sont disponibles dans hello **chaîne de connexion** panneau présentée précédemment :

* Nom d’utilisateur (obligatoire) : nom du compte Azure Cosmos DB.
* Mot de passe (obligatoire) : mot de passe du compte Azure Cosmos DB.
* Hôte (obligatoire) : nom de domaine complet de hello compte de base de données Azure Cosmos.
* Port (obligatoire) : 10255.
* Base de données (facultatif) : base de données hello hello connexion utilise. Si aucune base de données n’est fourni, la base de données par défaut hello est « test ».
* ssl = true (obligatoire)

Par exemple, considérez compte hello hello **chaîne de connexion** panneau. Exemple de chaîne de connexion valide :

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[utiliser MongoChef](mongodb-mongochef.md) avec une API de base de données Azure Cosmos pour MongoDB compte.
* Explorer les API de base de données Azure Cosmos de hello pour MongoDB en consultant [exemples](mongodb-samples.md).
