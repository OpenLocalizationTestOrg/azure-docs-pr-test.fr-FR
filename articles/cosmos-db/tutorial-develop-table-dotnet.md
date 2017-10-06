---
title: "Azure Cosmos DB : Développer avec hello API de Table dans .NET | Documents Microsoft"
description: "Découvrez comment toodevelop avec l’API de Table Azure Cosmos DB à l’aide de .NET"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a>Azure Cosmos DB : Développer avec hello dans .NET, les API de Table

Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale. Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur.

Ce didacticiel couvre hello tâches suivantes : 

> [!div class="checklist"] 
> * Création d’un compte Azure Cosmos DB 
> * Activer la fonctionnalité dans le fichier app.config hello 
> * Créer une table à l’aide de hello [API Table](table-introduction.md) (version préliminaire)
> * Ajouter une table de tooa d’entité 
> * Insertion d’un lot d’entités 
> * Extraction d'une seule entité 
> * Interrogation d’entités à l’aide d’index secondaires automatiques 
> * Remplacement d’une entité 
> * Suppression d’une entité 
> * Suppression d’une table
 
## <a name="tables-in-azure-cosmos-db"></a>Tables dans Azure Cosmos DB 

Base de données Azure Cosmos fournit hello [Table API](table-introduction.md) (aperçu) pour les applications qui ont besoin d’un magasin clé-valeur avec une conception sans schéma. [Stockage de Table Azure](../storage/common/storage-introduction.md) kits de développement logiciel et les API REST peuvent être toowork utilisé avec la base de données Azure Cosmos. Vous pouvez utiliser des tables de base de données Azure Cosmos toocreate aux exigences de débit élevé. Azure Cosmos DB prend en charge les tables optimisées en débit (appelées de façon informelle « tables premium »), actuellement en préversion publique. 

Vous pouvez continuer toouse stockage Azure Table pour les tables de stockage et réduire les besoins de débit. Base de données Azure Cosmos introduira prise en charge pour les tables de stockage optimisé dans une prochaine mise à jour et nouveaux et existants Table Azure en toute transparence les comptes de stockage sera mis à niveau tooAzure Cosmos DB.

Si vous utilisez actuellement le stockage de Table Azure, vous bénéficiez hello avantages avec l’aperçu de la « table premium » hello suivants :

- [Distribution mondiale](distribute-data-globally.md) clé en main avec multihébergement et [basculements automatiques et manuels](regional-failover.md)
- Prise en charge de l’indexation automatique indépendante du schéma par rapport à toutes les propriétés (« index secondaires »), et requêtes rapides 
- Prise en charge de la [mise à l’échelle indépendante du stockage et du débit](partition-data.md) pour autant de régions que nécessaire
- Prise en charge de [débit dédié par table](request-units.md) qui peut être monté en charge des centaines toomillions de demandes par seconde
- Prise en charge de [cinq niveaux de cohérence ajustables](consistency-levels.md) tootrade hors tension de la disponibilité, la latence et la cohérence selon les besoins de votre application
- disponibilité de 99,99 % au sein d’une seule région et capacité tooadd plusieurs régions pour augmenter la disponibilité et [SLA complète de pointe](https://azure.microsoft.com/support/legal/sla/cosmos-db/) sur la disponibilité générale
- Travailler avec le stockage Azure existant hello .NET SDK et aucune application de tooyour de modifications de code

Version préliminaire hello, prend en charge de la base de données Azure Cosmos hello API de Table à l’aide de hello du SDK .NET. Vous pouvez télécharger hello [aperçu de stockage Windows Azure SDK](https://aka.ms/premiumtablenuget) de NuGet, qui a hello mêmes classes et les signatures de méthode en tant que hello [SDK Azure Storage](https://www.nuget.org/packages/WindowsAzure.Storage), mais connectez-vous également les comptes de Cosmos DB tooAzure à l’aide de hello API de table.

toolearn savoir plus sur les tâches de stockage Azure Table complexes, consultez :

* [Introduction tooAzure Cosmos DB : API de Table](table-introduction.md)
* documentation de référence de service de Table pour plus d’informations sur les API disponibles de Hello [bibliothèque cliente de stockage pour la référence .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)

### <a name="about-this-tutorial"></a>À propos de ce didacticiel
Ce didacticiel est pour les développeurs qui sont familiarisés avec hello stockage de Table Azure SDK et sont que les fonctionnalités de premium hello toouse disponibles à l’aide de base de données Azure Cosmos. Il est basé sur [prise en main le stockage de Table Azure à l’aide de .NET](table-storage-how-to-use-dotnet.md) et montre comment parti tootake de fonctionnalités supplémentaires que les index secondaires, le débit approvisionné et hébergement multiple. Nous abordons la toouse hello toocreate portail Azure un compte de base de données Azure Cosmos, puis créer et déployer une application de la Table. Nous passons également en revue des exemples .NET pour la création et la suppression d’une table, et l’insertion, la mise à jour, la suppression et l’interrogation de données de table. 

Si vous n’avez pas encore Visual Studio 2017 installé, vous pouvez télécharger et utiliser hello **libre** [2017 de Visual Studio Community Edition](https://www.visualstudio.com/downloads/). Assurez-vous que vous activez **le développement Azure** pendant l’installation de Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Création d'un compte de base de données

Commençons par la création d’un compte de base de données Azure Cosmos Bonjour portail Azure.  

> [!TIP]
> * Possédez-vous un compte Azure Cosmos DB ? Dans ce cas, passez directement trop[configurer votre solution Visual Studio](#SetupVS).
> * Possédiez-vous un compte Azure DocumentDB ? Si votre compte est maintenant un compte de base de données Azure Cosmos, et que vous pouvez passer trop[configurer votre solution Visual Studio](#SetupVS).  
> * Si vous utilisez hello Azure Cosmos DB émulateur, suivez les étapes de hello à [Azure Cosmos DB émulateur](local-emulator.md) toosetup hello émulateur et passer trop[configurer votre Solution Visual Studio](#SetupVS).
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a>Exemple d’application hello de cloner

Maintenant nous allons cloner une application de la Table à partir de github, définissez la chaîne de connexion hello et exécutez-le.

1. Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `cd` répertoire de travail tooa.  

2. Exécutez hello suivant le dépôt d’exemples de commande tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. Ouvrez ensuite le fichier de solution de hello dans Visual Studio.

## <a name="update-your-connection-string"></a>Mise à jour de votre chaîne de connexion

Revenez toohello tooget portail Azure vos informations de chaîne de connexion et le copier dans une application hello.

1. Bonjour [portail Azure](http://portal.azure.com/), dans votre base de données de Cosmos Azure account, Bonjour barre de navigation gauche, cliquez sur **clés**, puis cliquez sur **en lecture-écriture clés**. Vous allez utiliser les boutons de copier hello sur droite hello hello écran toocopy hello de chaîne de connexion dans le fichier app.config de hello dans l’étape suivante de hello.

2. Dans Visual Studio, ouvrez le fichier app.config de hello. 

3. Copier la valeur de l’URI à partir du portail hello (à l’aide du bouton de copie hello) et le rendre hello la valeur de clé de compte hello dans app.config. Utilisez le nom de compte de hello créé précédemment pour le nom de compte dans le fichier app.config.
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> toouse cette application avec le stockage de Table Azure standard, vous devez de chaîne de connexion toochange hello dans `app.config file`. Utiliser le nom de compte hello en tant que nom de compte de la Table et la clé en tant que clé primaire de stockage Azure. <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a>Générez et déployez l’application hello
1. Dans Visual Studio, cliquez sur projet hello dans **l’Explorateur de solutions** puis cliquez sur **gérer les Packages NuGet**. 

2. Bonjour NuGet **Parcourir** , tapez ***WindowsAzure.Storage-PremiumTable***. Cochez la case **Inclure les préversions**.

3. À partir des résultats de hello, installez hello **WindowsAzure.Storage-PremiumTable** et choisissez la version préliminaire de hello `0.0.1-preview`. Cette action installe le package de stockage de Table Azure hello et toutes les dépendances.

4. Cliquez sur CTRL + F5 application hello de toorun. 

Vous pouvez maintenant revenir en arrière tooData Explorer et voir la requête, modifier et travailler avec ces données de table. 

> [!NOTE]
> toouse cette application avec un émulateur de base de données Azure Cosmos, simplement vous avez besoin de chaîne de connexion toochange hello dans `app.config file`. Utilisez hello sous la valeur de l’émulateur. <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a>Fonctionnalités d’Azure Cosmos DB
Base de données Azure Cosmos prend en charge un certain nombre de fonctionnalités qui ne sont pas disponibles dans hello API de stockage Azure Table. Hello nouvelles fonctionnalités peuvent être activées via les éléments suivants de hello `appSettings` valeurs de configuration. Nous n’avez pas introduit toutes les nouvelles signatures surcharges toohello aperçu ou SDK Azure Storage. Cela vous permet de tooconnect tooboth standard et premium tables et le travail avec d’autres services de stockage Azure, comme les objets BLOB et files d’attente. 


| Clé | Description |
| --- | --- |
| TableConnectionMode  | Azure Cosmos DB prend en charge deux modes de connectivité. Dans `Gateway` mode, les demandes sont toujours effectuées passerelle de base de données Azure Cosmos toohello, qu’il transfère toohello des partitions de données correspondante. Dans `Direct` mode de connectivité client de hello lit mappage hello de toopartitions de tables et les demandes sont effectuées directement sur les partitions de données. Nous vous recommandons de `Direct`, hello par défaut.  |
| TableConnectionProtocol | Azure Cosmos DB prend en charge deux protocoles de connexion : `Https` et `Tcp`. `Tcp`est la valeur par défaut hello et recommandé, car il est plus léger. |
| TablePreferredLocations | Liste séparée par des virgules des emplacements (de multihébergement) préférés pour les lectures. Chaque compte Azure Cosmos DB peut être associé à un nombre de régions compris entre un et plus de 30. Chaque instance de client peut spécifier un sous-ensemble de ces régions dans l’ordre de hello préféré pour les lectures de faible latence. les régions Hello doivent être nommées à l’aide de leurs [afficher les noms des](https://msdn.microsoft.com/library/azure/gg441293.aspx), par exemple, `West US`. Voir également [API multihébergement](tutorial-global-distribution-table.md).
| TableConsistencyLevel | Vous pouvez trouver un compromis entre latence, cohérence et disponibilité en choisissant l’un des cinq niveaux de cohérence bien définis disponibles : `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix` et `Eventual`. La valeur par défaut est `Session`. choix de Hello du niveau de cohérence rend une différence significative des performances dans les configurations de plusieurs régions. Pour plus d’informations, consultez [Niveaux de cohérence](consistency-levels.md). |
| TableThroughput | Débit réservé pour la table hello exprimée en unités de demande (RU) par seconde. Les tables uniques peuvent prendre en charge plusieurs centaines de millions de RU/s. Voir [Unités de requête](request-units.md). La valeur par défaut est `400`. |
| TableIndexingPolicy | Indexation cohérente et automatique de toutes les colonnes que contiennent les tables. | JSON chaîne conforme toohello une spécification de la stratégie d’indexation. Consultez [stratégie d’indexation](indexing-policies.md) toosee comment vous pouvez modifier des colonnes spécifiques d’indexation stratégie tooinclude/exclude. | Indexation automatique de toutes les propriétés (hachage pour les chaînes et plage pour les nombres). |
| TableQueryMaxItemCount | Configurer hello le nombre maximal d’éléments renvoyés par la requête de table dans un seul aller-retour. Valeur par défaut est `-1`, ce qui permet la base de données Azure Cosmos déterminer dynamiquement la valeur hello lors de l’exécution. |
| TableQueryEnableScan | Si la requête de hello ne peut pas utiliser des index de hello pour n’importe quel filtre, puis l’exécuter quand même via une analyse. La valeur par défaut est `false`.|
| TableQueryMaxDegreeOfParallelism | degré de Hello de parallélisme pour l’exécution d’une requête de partitions croisées. `0`est la série avec aucune pré-extraction, `1` est série avec la pré-récupération et les valeurs élevées hello accroître le taux de parallélisme. Valeur par défaut est `-1`, ce qui permet la base de données Azure Cosmos déterminer dynamiquement la valeur hello lors de l’exécution. |

valeur par défaut de toochange hello, ouvrez hello `app.config` fichier à partir de l’Explorateur de solutions dans Visual Studio. Ajouter du contenu hello Hello `<appSettings>` élément indiqué ci-dessous. Remplacez `account-name` avec nom hello de votre compte de stockage et `account-key` avec la clé d’accès de votre compte. 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

Nous allons effectuer une révision rapide de ce qui se passe dans l’application hello. Ouvrez hello `Program.cs` fichier et que vous recherchez que ces lignes de code créent hello de ressources de la Table. 

## <a name="create-hello-table-client"></a>Créer le client de table hello
Vous initialisez un `CloudTableClient` compte de table tooconnect toohello.

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
Ce client est initialisé à l’aide de hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, et `TablePreferredLocations` s’il est spécifié dans les paramètres de l’application hello des valeurs de configuration.
    
## <a name="create-a-table"></a>Création d’une table
Ensuite, vous créez une table à l’aide de `CloudTable`. Tables de base de données Azure Cosmos peuvent évoluer de manière indépendante en termes de débit et de stockage et le partitionnement est géré automatiquement par le service de hello. Azure Cosmos DB prend à la fois en charge une taille fixe et un nombre illimité de tables. Pour plus d’informations, consultez [Partitionnement dans Azure Cosmos DB](partition-data.md). 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

Il existe une différence importante dans la façon dont les tables sont créées. Azure Cosmos DB réserve le débit, contrairement au modèle du stockage Azure pour les transactions, basé sur la consommation. modèle de réservation Hello présente deux avantages principaux :

* Le débit est dédié/réservé, ce qui fait que vous n’êtes jamais limité si le taux de requêtes est inférieur ou égal à votre débit approvisionné.
* modèle de réservation Hello est plus [économique pour les charges de travail à nombre élevé de débit](key-value-store-cost.md)

Vous pouvez configurer un débit hello par défaut en configurant le paramètre hello pour `TableThroughput` en termes de RU (unités de demande) par seconde. 

Une lecture d’une entité de 1 Ko est normalisée en tant que 1 ur et autres opérations sont normalisée tooa fixé valeur RU en fonction de leur consommation de processeur, mémoire et e/s. En savoir plus sur les [Unités de requête dans Azure Cosmos DB](request-units.md).

> [!NOTE]
> Alors que le SDK le stockage de Table ne prend pas en charge la modification de débit, vous pouvez modifier le débit de hello instantanément à tout moment à l’aide de hello portail Azure ou CLI d’Azure.

Ensuite, nous guider lecture simple de hello et écrire des opérations à l’aide du stockage de Table Azure hello SDK. Ce didacticiel démontre les latences prévisibles faibles, de l’ordre de quelques millisecondes, et les requêtes rapides assurées par Azure Cosmos DB.

## <a name="add-an-entity-tooa-table"></a>Ajouter une table de tooa d’entité
Les entités dans le stockage Azure Table étendent à partir de hello `TableEntity` classe et doit avoir `PartitionKey` et `RowKey` propriétés. Voici un exemple de définition d’une entité de client.

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

Hello suivant extrait de code montre comment tooinsert une entité avec hello stockage Azure SDK. Base de données Azure Cosmos est conçu pour être garanti de faible latence à n’importe quelle échelle, entre Bonjour.

Fin des écritures < 15 ms à p99 et ms ~ 6 à p50 pour les applications en cours d’exécution hello même région que le compte de base de données Azure Cosmos de hello. Et cette durée compte fait hello qui écrit est toohello précédent client une fois qu’ils sont répliquées de manière synchrone, la validation de façon durable, et tout le contenu est indexé.

Hello API de la Table de base de données Azure Cosmos est en version préliminaire. Disponibilité générale, hello p99 de garanties de latence sont soutenues par SLA, comme d’autres API de base de données Azure Cosmos. 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a>Insertion d’un lot d’entités
Azure Table storage prend en charge une API d’opération de traitement par lots, qui vous permet de combiner des mises à jour, suppressions et insertions dans hello même opération de lot unique. Base de données Azure Cosmos n’a pas certaines des limitations de hello sur les API de lot hello en tant que stockage de Table Azure. Par exemple, vous pouvez effectuer plusieurs lectures dans un lot, vous pouvez effectuer plusieurs écritures toohello même entité au sein d’un lot, et il n’existe aucune limite sur 100 opérations par lot. 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a>Extraction d'une seule entité
Récupère (obtient) dans Cosmos base de données Azure complet < 10 ms à p99 et ~ 1 ms à p50 dans hello même région Azure. Vous pouvez ajouter autant compte tooyour de régions pour les lectures de faible latence et déployer tooread d’applications à partir de leur région (« multi-résidente ») en définissant `TablePreferredLocations`. 

Vous pouvez récupérer une entité unique à l’aide de hello suivant extrait de code :

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> Pour plus d’informations sur les API multihébergement, consultez [Développement avec plusieurs régions](tutorial-global-distribution-table.md).
>

## <a name="query-entities-using-automatic-secondary-indexes"></a>Interrogation d’entités à l’aide d’index secondaires automatiques
Tables peuvent être interrogées à l’aide de hello `TableQuery` classe. Azure Cosmos DB intègre un moteur de base de données optimisé pour l’écriture qui indexe automatiquement toutes les colonnes de votre table. L’indexation de base de données Azure Cosmos est tooschema agnostique. Par conséquent, même si votre schéma est différent entre les lignes, ou si le schéma de hello évolue au fil du temps, il est automatiquement indexé. Étant donné que la base de données Azure Cosmos prend en charge les index secondaires automatique, les requêtes par rapport à n’importe quelle propriété peuvent utiliser les index hello et pris en charge efficacement.

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

Dans l’aperçu, prend en charge la base de données Azure Cosmos hello même fonctionnalité comme stockage de Table Azure pour hello API de la Table de requête. Azure Cosmos DB prend également en charge le tri, les agrégats, les requêtes géospatiales, les hiérarchies et un large éventail de fonctions intégrées. Vous trouverez des fonctionnalités supplémentaires Hello Bonjour API de Table dans une mise à jour future du service. Pour une vue d’ensemble de ces fonctionnalités, consultez [Azure Cosmos DB query](documentdb-sql-query.md) (Requête dans Azure Cosmos DB). 

## <a name="replace-an-entity"></a>Remplacement d’une entité
tooupdate une entité, récupérer à partir du service de Table hello, modifier l’objet d’entité hello, puis enregistrez les modifications hello de nouveau service de Table toohello. Hello code suivant modifie un numéro de téléphone existant. 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
De même, vous pouvez effectuer des opérations `InsertOrMerge` ou `Merge`.  

## <a name="delete-an-entity"></a>Suppression d’une entité
Vous pouvez facilement supprimer une entité une fois que vous l’avez extrait à l’aide de hello même modèle indiqué pour la mise à jour une entité. Hello suivant code récupère et supprime une entité customer.

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a>Suppression d’une table
Enfin, hello, exemple de code suivant supprime une table à partir d’un compte de stockage. Vous pouvez supprimer et recréer une table immédiatement avec Azure Cosmos DB.

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a>Supprimer des ressources 

Si vous n’allez toocontinue toouse cette application, utilisez hello suivant toodelete suit toutes les ressources créées par ce didacticiel Bonjour portail Azure.   

1. À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé.  
2. Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**. 

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, nous avons abordé comment tooget démarrer à l’aide de la base de données Azure Cosmos hello API de Table, et vous avez effectué les éléments suivants de hello : 

> [!div class="checklist"] 
> * Créé un compte Azure Cosmos DB 
> * Fonctionnalité activée dans le fichier app.config hello 
> * Création d’une table 
> * Ajout d’un tableau de tooa entité 
> * Insertion d’un lot d’entités 
> * Extraction d’une seule entité 
> * Interrogation d’entités à l’aide d’index secondaires automatiques 
> * Remplacement d’une entité 
> * Suppression d’une entité 
> * Suppression d’une table  

Vous pouvez maintenant continuer le didacticiel suivant de toohello et en savoir plus sur l’interrogation des données de la table. 

> [!div class="nextstepaction"]
> [Requête avec hello API de Table](tutorial-query-table.md)
