---
title: "aaaBuild des applications mobiles avec Xamarin et de la base de données Azure Cosmos | Documents Microsoft"
description: "Didacticiel qui permet de créer une application Xamarin iOS, Android ou Forms à l’aide d’Azure Cosmos DB. Azure Cosmos DB est une base de données cloud, mondiale et rapide, pour les applications mobiles."
services: cosmos-db
documentationcenter: .net
author: arramac
manager: monicar
editor: 
ms.assetid: ff97881a-b41a-499d-b7ab-4f394df0e153
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: arramac
ms.openlocfilehash: 362a0e239a61e1309e1cf720c23151760952cf69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-mobile-applications-with-xamarin-and-azure-cosmos-db"></a>Créer des applications mobiles avec Xamarin et Azure Cosmos DB
Des applications mobiles plus besoin de données toostore dans le cloud de hello et base de données Azure Cosmos est une base de données de cloud pour les applications mobiles. Elle a tout ce dont un développeur mobile a besoin. Il s’agit d’une base de données en tant que service, entièrement gérée, qui évolue en fonction de la demande. Il peut mettre votre application tooyour de données de façon transparente, chaque fois que vos utilisateurs se trouvent monde hello. À l’aide de hello [Kit de développement logiciel Azure Cosmos DB .NET Core](documentdb-sdk-dotnet-core.md), vous pouvez activer toointeract des applications mobiles Xamarin directement avec Azure Cosmos DB, sans une couche intermédiaire.

Dans cet article, nous proposons un didacticiel pour la création d’applications mobiles avec Xamarin et Azure Cosmos DB. Vous pouvez trouver le code source complet hello pour le didacticiel hello [Xamarin et la base de données Azure Cosmos sur GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin), y compris la manière toomanage utilisateurs et des autorisations.

## <a name="azure-cosmos-db-capabilities-for-mobile-apps"></a>Fonctionnalités d’Azure Cosmos DB pour les applications mobiles
Base de données Azure Cosmos fournit hello suivant des fonctionnalités clés pour les développeurs d’applications mobiles :

![Fonctionnalités d’Azure Cosmos DB pour les applications mobiles](media/mobile-apps-with-xamarin/documentdb-for-mobile.png)

* Requêtes riches sur des données sans schéma. Azure Cosmos DB stocke les données sous la forme de documents JSON sans schéma dans des collections hétérogènes. Il offre [requêtes riches et rapides](documentdb-sql-query.md) sans hello devez tooworry sur les schémas ou les index.
* Débit rapide. Il ne prend que quelques millisecondes tooread et écrire des documents avec la base de données Azure Cosmos. Les développeurs peuvent spécifier le débit hello que dont ils ont besoin et base de données Azure Cosmos l’honore avec les contrats SLA de 99,99 %.
* Mise à l’échelle illimitée. Vos collections Azure Cosmos DB [augmentent à mesure que votre application grandit](partition-data.md). Vous pouvez commencer par des données de petite taille et un débit réduit, soit quelques centaines de requêtes par seconde. Vos collections peuvent atteindre toopetabytes de données et de débit arbitrairement volumineux avec des centaines de millions de demandes par seconde.
* Distribution globale. Application mobile, les utilisateurs se trouvent sur hello traverser, souvent Bonjour. Azure Cosmos DB est une [base de données mondialement distribuée](distribute-data-globally.md). Cliquez sur hello carte toomake vos utilisateurs tooyour accessible de données.
* Autorisation riche intégrée. Avec Azure Cosmos DB, vous implémentez facilement des modèles très répandus, comme les [données par utilisateur](https://aka.ms/documentdb-xamarin-todouser) ou les données partagées par plusieurs utilisateurs, sans recourir à un code d’autorisation complexe personnalisé.
* Requêtes géospatiales. Beaucoup d’applications mobiles proposent aujourd’hui des expériences géocontextuelles. Avec prise en charge de première classe pour [geospatial types](geospatial.md), base de données Azure Cosmos facilite le création ces tooaccomplish facilement des expériences.
* Pièces jointes binaires. Vos données d’application comprennent souvent des blobs binaires. Prise en charge native pour les pièces jointes rend plus facile toouse de base de données Azure Cosmos en tant qu’un guichet unique pour vos données d’application.

## <a name="azure-cosmos-db-and-xamarin-tutorial"></a>Didacticiel Azure Cosmos DB et Xamarin
Hello suivant le didacticiel montre comment toobuild une application mobile à l’aide de Xamarin et la base de données Azure Cosmos. Vous pouvez trouver le code source complet hello pour le didacticiel hello [Xamarin et la base de données Azure Cosmos sur GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin).

### <a name="get-started"></a>Prise en main
Il est facile tooget démarré avec la base de données Azure Cosmos. Accédez toohello portail Azure et créer un nouveau compte de base de données Azure Cosmos. Cliquez sur hello **démarrage rapide** onglet. Téléchargement Xamarin Forms action liste exemple hello qui est déjà connecté compte de base de données Azure Cosmos tooyour. 

![Démarrage rapide d’Azure Cosmos DB pour les applications mobiles](media/mobile-apps-with-xamarin/cosmos-db-quickstart.png)

Ou si vous avez une application Xamarin existante, vous pouvez ajouter hello [package NuGet de base de données Azure Cosmos](documentdb-sdk-dotnet-core.md). Azure Cosmos DB prend en charge les bibliothèques partagées Xamarin.IOS, Xamarin.Android et Xamarin Forms.

### <a name="work-with-data"></a>Utilisation des données
Vos enregistrements de données sont stockés dans Azure Cosmos DB sous la forme de documents JSON sans schéma dans des collections hétérogènes. Vous pouvez stocker des documents avec des structures différentes dans hello même collection :

```cs
    var result = await client.CreateDocumentAsync(collectionLink, todoItem);
```

Dans vos projets Xamarin, vous pouvez utiliser des requêtes intégrées au langage sur des données sans schéma :

```cs
    var query = await client.CreateDocumentQuery<ToDoItem>(collectionLink)
                    .Where(todoItem => todoItem.Complete == false)
                    .AsDocumentQuery();

    Items = new List<TodoItem>();
    while (query.HasMoreResults) {
        Items.AddRange(await query.ExecuteNextAsync<TodoItem>());
    }
```
### <a name="add-users"></a>Ajouter des utilisateurs
Comme de nombreuses obtenir des exemples démarrées, exemple de base de données Azure Cosmos hello téléchargé authentifie toohello service à l’aide d’un codé en dur de la clé principale dans le code de l’application hello. Cette valeur par défaut n’est pas recommandé pour une application que vous avez l’intention de votre émulateur local toorun n’importe où, à l’exception. Si un utilisateur non autorisé obtenu la clé principale de hello, toutes les données hello sur votre compte de base de données Azure Cosmos pourrait être compromises. Au lieu de cela, vous souhaitez que votre tooaccess application hello uniquement les enregistrements pour l’utilisateur connecté hello. Base de données Cosmos Azure permet aux développeurs de toogrant application lecture ou lecture/écriture collection tooa d’autorisations, un ensemble de documents regroupées par une clé de partition ou un document spécifique. 

Suivez ces étapes toomodify hello action liste application tooa action multi-utilisateur liste d’applications : 

  1. Ajouter l’application tooyour de connexion à l’aide de Facebook, Active Directory ou tout autre fournisseur.

  2. Créer une collection Azure Cosmos DB UserItems avec **/userId** en tant que clé de partition hello. Spécification de clé de partition hello pour votre collection permet à l’infini tooscale de la base de données Azure Cosmos en tant que nombre hello d’utilisateurs de votre application augmente, tout en continuant de requêtes rapide de toooffer.

  3. Ajoutez Azure Cosmos DB Ressource Token Broker. Cette API Web simple authentifie les utilisateurs et émet des jetons de courte durée de vie toosigned les utilisateurs avec accès uniquement les documents toohello au sein de leur partition. Dans cet exemple, nous hébergeons Resource Token Broker dans App Service.

  4. Modifier hello application tooauthenticate tooResource Broker jeton avec Facebook et demander des jetons de ressource hello pour hello Facebook utilisateurs connectés. Vous pouvez ensuite accéder à leurs données Bonjour UserItems collection.  

Un exemple de code complet de ce modèle est disponible sur [Resource Token Broker sur GitHub](http://aka.ms/documentdb-xamarin-todouser). Ce diagramme illustre les solutions hello :

![Utilisateurs d’Azure Cosmos DB et répartiteur d’autorisations](media/mobile-apps-with-xamarin/documentdb-resource-token-broker.png)

Si vous souhaitez que deux utilisateurs toohave accès toohello même liste de tâches, vous pouvez ajouter le jeton d’accès toohello des autorisations supplémentaires dans Service Broker jeton de ressource.

### <a name="scale-on-demand"></a>Mise à l’échelle à la demande
Azure Cosmos DB est une base de données gérée en tant que service. À mesure que votre base d’utilisateurs augmente, vous n’avez pas besoin tooworry sur la configuration des machines virtuelles ou d’accroître les cœurs. Il vous suffit de tootell base de données Azure Cosmos est le nombre d’opérations par seconde (débit) que votre application a besoin. Vous pouvez spécifier le débit hello via hello **échelle** onglet à l’aide d’une mesure du débit appelé unités de demande (RUs) par seconde. Par exemple, une opération de lecture d’un document de 1 Ko nécessite 1 RU. Vous pouvez également ajouter des alertes toohello **débit** toomonitor métrique hello croissance du trafic et modifier par programmation le débit hello déclencher les alertes.

![Débit de mise à l’échelle d’Azure Cosmos DB à la demande](media/mobile-apps-with-xamarin/cosmos-db-xamarin-scale.png)

### <a name="go-planet-scale"></a>Développement à l’échelle de la planète
Comme votre popularité gains d’application, vous pourrez obtenir les utilisateurs monde hello. Ou peut-être toobe préparé pour les événements imprévus. Accédez toohello portail Azure et ouvrez votre compte de base de données Azure Cosmos. Cliquez sur hello carte toomake vos données tooany répliquer en continu de régions sur Bonjour. Grâce à cette fonctionnalité, vos données sont disponibles où que se trouvent vos utilisateurs. Vous pouvez également ajouter toobe de stratégies de basculement préparé pour les plans d’urgence.

![Mise à l’échelle d’Azure Cosmos DB dans différentes régions géographiques](media/mobile-apps-with-xamarin/cosmos-db-xamarin-replicate.png)

Félicitations ! Vous les solutions hello s’est terminé et que vous avez une application mobile avec Xamarin et de la base de données Azure Cosmos. Suivez les applications Cordova toobuild étapes similaires à l’aide de hello Azure Cosmos DB JavaScript SDK et des applications iOS/Android natives à l’aide des API REST de Azure Cosmos DB.

## <a name="next-steps"></a>Étapes suivantes
* Afficher le code source de hello pour [Xamarin et la base de données Azure Cosmos sur GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin).
* Télécharger hello [Azure Cosmos DB .NET Core SDK](documentdb-sdk-dotnet-core.md).
* Consultez davantage d’exemples de code pour les [applications .NET](documentdb-dotnet-samples.md).
* Découvrez plus en détail les [riches fonctionnalités d’interrogation d’Azure Cosmos DB](documentdb-sql-query.md).
* Découvrez plus en détail la [prise en charge géospatiale dans Azure Cosmos DB](geospatial.md).



