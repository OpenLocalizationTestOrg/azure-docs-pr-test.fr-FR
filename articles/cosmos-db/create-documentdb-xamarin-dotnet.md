---
title: "Azure Cosmos DB : créer une application web avec authentification Xamarin et Facebook | Microsoft Docs"
description: "Présente un exemple de code .NET que vous pouvez utiliser tooconnect tooand interroger la base de données Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a>Azure Cosmos DB : créer une application web avec authentification .NET, Xamarin et Facebook

Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale. Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur. 

Ce démarrage rapide montre comment toocreate un compte de base de données Azure Cosmos, base de données du document et à l’aide de la collection hello portail Azure. Vous allez ensuite générer et déployer une application web de liste todo repose sur hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), [Xamarin](https://www.xamarin.com/)et du moteur d’autorisation de base de données Azure Cosmos hello. application web de liste de tâches Hello implémente un modèle de données par l’utilisateur qui permet de toologin les utilisateurs à l’aide de Facebook Auth et gérer leurs propres éléments toodo.

## <a name="prerequisites"></a>Composants requis

Si vous n’avez pas encore Visual Studio 2017 installé, vous pouvez télécharger et utiliser hello **libre** [2017 de Visual Studio Community Edition](https://www.visualstudio.com/downloads/). Assurez-vous que vous activez **le développement Azure** pendant l’installation de Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Création d'un compte de base de données

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Ajouter une collection

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Exemple d’application hello de cloner

Maintenant, nous allons une API DocumentDB le clonage d’application à partir de github, définir la chaîne de connexion hello et exécutez-le. Vous allez voir combien il est facile toowork avec des données par programme. 

1. Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `cd` répertoire de travail tooa.  

2. Exécutez hello suivant le dépôt d’exemples de commande tooclone hello. 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. Ouvrez ensuite le fichier de DocumentDBTodo.sln hello à partir du dossier samples/xamarin/UserItems/xamarin.forms hello dans Visual Studio. 

## <a name="review-hello-code"></a>Réviser le code hello

code Hello dans le dossier de Xamarin hello contient :

* L’application Xamarin. application Hello stocke des éléments de tâche de l’utilisateur hello dans une collection partitionnée nommée UserItems.
* L’API du répartiteur de jetons de ressource. Une ressource de base de données Azure Cosmos toobroker API Web ASP.NET simple des jetons toohello les utilisateurs de l’application hello connecté. Les jetons de ressource sont des jetons d’accès de courte durée de vie qui apportent une application hello hello accès toohello est enregistré dans les données de l’utilisateur.

Hello d’authentification et flux de données est illustré dans le diagramme hello ci-dessous.

* Hello UserItems collection est créée avec la clé de partition hello ' / nom d’utilisateur ». Si vous indiquez une clé de partition pour une collection de base de données Azure Cosmos tooscale indéfiniment en tant que nombre hello des utilisateurs et des éléments augmente.
* application Xamarin de Hello permet toologin utilisateurs avec les informations d’identification de Facebook.
* application Xamarin de Hello utilise tooauthenticate de jeton accès Facebook avec l’API ResourceTokenBroker
* broker de jeton de ressource Hello API authentifie la demande de hello à l’aide de la fonctionnalité d’authentification de Service d’application et demande un jeton de ressource de base de données Azure Cosmos avec des documents de tooall d’accès en lecture/écriture partage la clé de partition de l’utilisateur authentifié hello.
* Broker de jeton de ressource retourne hello ressource toohello jeton client application.
* application Hello accède à des éléments de tâche de l’utilisateur hello à l’aide du jeton de ressource hello.

![Application To-Do avec des exemples de données](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a>Mise à jour de votre chaîne de connexion

Revenez toohello tooget portail Azure vos informations de chaîne de connexion et le copier dans une application hello.

1. Bonjour [portail Azure](http://portal.azure.com/), dans votre base de données de Cosmos Azure account, Bonjour barre de navigation gauche, cliquez sur **clés**, puis cliquez sur **en lecture-écriture clés**. Vous allez utiliser les boutons de copier hello sur droite hello Hello de toocopy écran hello URI et la clé primaire dans le fichier Web.config de hello dans l’étape suivante de hello.

    ![Afficher et copier une clé d’accès dans hello portail Azure, le panneau de clés](./media/create-documentdb-xamarin-dotnet/keys.png)

2. Dans Visual Studio 2017, ouvrez le fichier Web.config de hello dans le dossier d’azure-documentdb-dotnet/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker hello. 

3. Copier la valeur de l’URI à partir du portail hello (à l’aide du bouton de copie hello) et le rendre hello valeur accountUrl hello dans le fichier Web.config. 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. Copiez la valeur de clé primaire à partir du portail de hello, puis rendre hello valeur accountKey hello dans Web.congif. 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

Vous avez maintenant d’une mise à jour de votre application avec toutes informations hello lui toocommunicate avec la base de données Azure Cosmos. 

## <a name="build-and-deploy-hello-web-app"></a>Générer et déployer l’application web de hello

1. Bonjour portail Azure, créer un Service d’applications du site Web toohost hello ressource jeton broker API.
2. Dans hello portail Azure, ouvrez le panneau des paramètres de l’application hello hello ressource jeton du service broker de site Web. Renseignez hello suivant les paramètres de l’application :

    * accountUrl - URL du compte de base de données Azure Cosmos hello à partir de l’onglet de clés hello de votre compte de base de données Azure Cosmos.
    * accountKey - clé de principale de compte de base de données Azure Cosmos hello à partir de l’onglet de clés hello de votre compte de base de données Azure Cosmos.
    * databaseId et collectionId de la base de données et de la collection créées

3. Hello tooyour de solution ResourceTokenBroker créé le site Web de publication.

4. Ouvrez le projet de Xamarin hello et accédez tooTodoItemManager.cs. Renseignez hello accountURL, collectionId, databaseId, ainsi que resourceTokenBrokerURL comme url de base https hello pour le site Web Service Broker pour les jetons de ressource hello.

5. Hello complète [comment tooconfigure votre compte de connexion du Service d’applications application toouse Facebook](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md) toosetup didacticiel l’authentification Facebook et configurer le site Web de ResourceTokenBroker hello.

    Exécutez l’application Xamarin de hello.

## <a name="review-slas-in-hello-azure-portal"></a>Passez en revue les SLA dans hello portail Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Supprimer des ressources

Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit : 

1. À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous venez de créer. 
2. Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.

## <a name="next-steps"></a>Étapes suivantes

Ce guide de démarrage rapide, vous avez appris comment toocreate un compte de base de données Azure Cosmos, créer une collection à l’aide de hello Explorateur de données, générer et déployer une application Xamarin. Vous pouvez maintenant importer les comptes de Cosmos DB tooyour des données supplémentaires. 

> [!div class="nextstepaction"]
> [Importer des données dans Azure Cosmos DB](import-data.md)
