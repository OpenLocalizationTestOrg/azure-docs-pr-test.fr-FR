---
title: "aaaAzure Cosmos DB modèle de ressource et concepts | Documents Microsoft"
description: "En savoir plus sur le modèle hiérarchique de Azure Cosmos DB des bases de données, des collections, une fonction définie par l’utilisateur (UDF), des documents, des ressources de toomanage autorisations et plus."
keywords: "Modèle hiérarchique, cosmosdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: 
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: ef9d5c0c-0867-4317-bb1b-98e219799fd5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: anhoh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc3642232b86cc27901ebd97456c386829324632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-hierarchical-resource-model-and-core-concepts"></a>Concepts clés et modèle de ressource hiérarchiques Azure Cosmos DB
les entités de base de données qui gère de la base de données Azure Cosmos Hello sont visées tooas **ressources**. Chaque ressource est identifiée de manière unique par un URI logique. Vous pouvez interagir avec les ressources de hello à l’aide de verbes HTTP standard, les en-têtes de demande/réponse et les codes d’état. 

La lecture de cet article, vous serez hello en mesure de tooanswer suivant questions :

* Qu’est-ce que le modèle de ressource de Cosmos DB ?
* Quels sont le système défini des ressources en tant que ressources de toouser opposés défini ?
* Comment adresser une ressource ?
* Comment travailler avec des collections ?
* Comment utiliser les procédures stockées, les déclencheurs et les fonctions définies par l’utilisateur ?

## <a name="hierarchical-resource-model"></a>Modèle de ressource hiérarchique
Comme hello diagramme suivant illustre, hello DB Cosmos hiérarchique **modèle de ressource** se compose d’ensembles de ressources sous un compte de base de données, chaque adressable via un URI logique et stable. Un ensemble de ressources sera tooas auxquels un **flux** dans cet article. 

> [!NOTE]
> Base de données Cosmos Azure offre un protocole TCP hautement efficace qui se trouve également RESTful dans son modèle de communication, disponible via hello [API cliente DocumentDB .NET](documentdb-sdk-dotnet.md).
> 
> 

![Modèle de ressource hiérarchique Azure Cosmos DB][1]  
**Modèle de ressource hiérarchique**   

toostart utilisation des ressources, vous devez [créer un compte de base de données](create-documentdb-dotnet.md) à l’aide de votre abonnement Azure. Un compte de base de données se compose d’un ensemble de **bases de données**. Chacune d’elles contient plusieurs **collections** et chaque collection contient des **procédures stockées, des déclencheurs, des fonctions définies par l’utilisateur, des documents** et les **pièces jointes** associées. Une base de données a également associés **utilisateurs**, chacun avec un ensemble de **autorisations** tooaccess collections, procédures stockées, déclencheurs, UDF, documents ou des pièces jointes. Les bases de données, les utilisateurs, les autorisations et les collections sont des ressources définies par le système avec des schémas connus, tandis que les documents et les pièces jointes contiennent du contenu JSON arbitraire défini par l'utilisateur.  

| Ressource | Description |
| --- | --- |
| Compte de base de données |Le compte de base de données est associé à un jeu de bases de données et à une quantité fixe de stockage d’objets blob pour les pièces jointes. Vous pouvez créer un ou plusieurs comptes de base de données à l’aide de votre abonnement Azure. Pour plus d’informations, consultez notre [page de tarification](https://azure.microsoft.com/pricing/details/cosmos-db/). |
| Base de données |Une base de données est un conteneur logique de stockage de documents partitionné entre des collections. Elle sert également de conteneur pour les utilisateurs. |
| Utilisateur |espace de noms logique Hello pour fixer l’étendue des autorisations. |
| Autorisation |Un jeton d’autorisation associé à un utilisateur pour la ressource spécifique de tooa accès. |
| Collection |Une collection est un conteneur de documents JSON et hello associés logique d’application JavaScript. Une collection est une entité facturable, où hello [coût](performance-levels.md) est déterminé par le niveau de performance hello associé hello collection. Collections peut couvrir une ou plusieurs partitions/serveurs et peut évoluer toohandle quasi illimitée des volumes de stockage ou de débit. |
| Procédure stockée |Logique d’application écrite en JavaScript qui est inscrit auprès d’une collection et exécutée de façon transactionnelle au sein du moteur de base de données hello. |
| Déclencheur |Logique d'application écrite en JavaScript exécutée avant ou après une opération d'insertion, de remplacement ou de suppression. |
| Fonctions définies par l'utilisateur |Logique d'application écrite en JavaScript. UDF activer toomodel un opérateur de requête personnalisée et ainsi étendent le langage de requête API DocumentDB hello principal. |
| Document |Contenu JSON (arbitraire) défini par l'utilisateur. Par défaut, aucun schéma ne doit toobe défini ni index secondaire doivent-elles toobe fournies pour hello tous les documents ajoutés tooa collection. |
| Pièce jointe |Les pièces jointes sont des documents spéciaux contenant des références et les métadonnées associées pour un élément multimédia/objet blob externe. développeur de Hello peut choisir de blob de hello toohave géré par la base de données Cosmos ou stocker chez un fournisseur de service blob externes tels que OneDrive, Dropbox, etc.. |

## <a name="system-vs-user-defined-resources"></a>Ressources système ou ressources définies par l'utilisateur
Les ressources (telles que les comptes de base de données, les bases de données, les collections, les utilisateurs, les autorisations, les procédures stockées, les déclencheurs et les fonctions définies par l'utilisateur) ont toutes un schéma fixe et sont nommées « ressources système ». En revanche, les ressources telles que les documents et les pièces jointes n’ont aucune restriction sur le schéma de hello et sont des exemples de ressources de défini par l’utilisateur. Dans Cosmos DB, les ressources système et définies par l’utilisateur sont représentées et gérées en tant qu’éléments JSON standard. Toutes les ressources, système ou définies par l’utilisateur ont hello propriétés courantes suivantes.

> [!NOTE]
> Toutes les propriétés générées par le système dans une ressource ont comme préfixe un trait de soulignement (_) dans leur représentation JSON.
> 
> 

<table>
    <tbody>
        <tr>
            <td valign="top"><p><strong>Propriété</strong></p></td>
            <td valign="top"><p><strong>Définie par l’utilisateur ou générée par le système ?</strong></p></td>
            <td valign="top"><p><strong>Objectif</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>_rid</p></td>
            <td valign="top"><p>Générée par le système</p></td>
            <td valign="top"><p>Identificateur unique et hiérarchique de ressource de hello système généré</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_etag</p></td>
            <td valign="top"><p>Générée par le système</p></td>
            <td valign="top"><p>eTag de ressource hello requise pour le contrôle d’accès concurrentiel optimiste</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_ts</p></td>
            <td valign="top"><p>Générée par le système</p></td>
            <td valign="top"><p>Horodateur de la dernière mise à jour de ressource de hello</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_self</p></td>
            <td valign="top"><p>Générée par le système</p></td>
            <td valign="top"><p>URI adressable unique de la ressource de hello</p></td>
        </tr>
        <tr>
            <td valign="top"><p>id</p></td>
            <td valign="top"><p>Générée par le système</p></td>
            <td valign="top"><p>Nom unique de la ressource de hello défini par l’utilisateur (avec hello même partition valeur de clé). Si l’utilisateur de hello ne spécifie pas un id, un id sera générée par le système</p></td>
        </tr>
    </tbody>
</table>

### <a name="wire-representation-of-resources"></a>Représentation en réseau des ressources
COSMOS DB n’impose pas de toutes les extensions exclusives toohello standard ou spéciales encodages JSON ; il fonctionne avec des documents JSON conformes standards.  

### <a name="addressing-a-resource"></a>Adressage d'une ressource
Toutes les ressources sont adressables via des URI. Hello valeur Hello **_self** propriété d’une ressource représente hello URI relatif de la ressource de hello. Hello format Hello URI se compose de hello /\<flux\>/ segments de chemin d’accès de {_rid} :  

| Valeur de hello _self | Description |
| --- | --- |
| /dbs |Flux de bases de données sous un compte de base de données |
| /dbs/{dbName} |Base de données avec l’id correspondant hello valeur {dbName} |
| /dbs/{dbName}/colls/ |Flux de collections dans une base de données |
| /dbs/{dbName}/colls/{collName} |Collection avec l’id correspondant hello valeur {collName} |
| /dbs/{dbName}/colls/{collName}/docs |Flux de documents dans une collection |
| /dbs/{dbName}/colls/{collName}/docs/{docId} |Le document ayant l’id correspondant hello valeur {doc} |
| /dbs/{dbName}/users/ |Flux d'utilisateurs d'une base de données |
| /dbs/{dbName}/users/{userId} |Utilisateur avec l’id correspondant hello valeur {user} |
| /dbs/{dbName}/users/{userId}/permissions |Flux d'autorisations d'un utilisateur |
| /dbs/{dbName}/users/{userId}/permissions/{permissionId} |Autorisation avec l’id correspondant hello valeur {permission} |

Chaque ressource a un nom d’unique définie par l’utilisateur exposé via la propriété d’id hello. Remarque : pour les documents, si l’utilisateur de hello ne spécifie pas un id, nos kits de développement logiciel pris en charge génère automatiquement un id unique pour le document de hello. id de Hello est une chaîne définie par l’utilisateur, des caractères too256 qui est unique dans le contexte de hello d’une ressource parent spécifique. 

Chaque ressource a également un identificateur de ressource hiérarchique générée par le système (également désignée tooas un RID), qui est disponible via la propriété _rid de hello. Hello RID encode hello ensemble de la hiérarchie d’une ressource donnée, et il s’agit de qu'une représentation interne pratique utilisé tooenforce l’intégrité référentielle de façon distribuée. Hello RID est unique au sein d’un compte de base de données et il est utilisé en interne par la base de données Cosmos pour un routage efficace sans nécessiter de recherches de partition croisée. valeurs Hello hello _self et les propriétés de _rid hello sont des représentations de remplacement et canoniques d’une ressource. 

Hello API REST prise en charge l’adressage des ressources et le routage des demandes par id de hello et propriétés de _rid hello.

## <a name="database-accounts"></a>Comptes de base de données
Votre abonnement Azure vous permet d’approvisionner un ou plusieurs comptes de base de données Cosmos DB.

Vous pouvez créer et gérer les comptes de base de données Cosmos DB via hello portail Azure à [http://portal.azure.com/](https://portal.azure.com/). La création et la gestion d’un compte de base de données requièrent un accès administrateur et peuvent uniquement être effectuées avec votre abonnement Azure. 

### <a name="database-account-properties"></a>Propriétés des comptes de base de données
Dans le cadre de la configuration et la gestion d’un compte de base de données, vous pouvez configurer et lire hello propriétés suivantes :  

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Nom de la propriété</strong></p></td>
            <td valign="top"><p><strong>Description</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>Stratégie de cohérence</p></td>
            <td valign="top"><p>Définir ce niveau de cohérence de propriété tooconfigure hello par défaut pour toutes les collections hello sous votre compte de base de données. Vous pouvez remplacer le niveau de cohérence hello sur la base de chaque demande à l’aide d’en-tête de demande hello [x-ms-consistency-level]. <p><p>Notez que cette propriété s’applique uniquement toohello <i>ressources définies par l’utilisateur</i>. Toutes les ressources définies par le système sont configurés toosupport lectures/requêtes à forte cohérence.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Clés d’autorisation</p></td>
            <td valign="top"><p>Voici hello principal et secondaire clés principale et en lecture seule qui fournissent d’administration accéder tooall des ressources hello sous le compte de base de données hello.</p></td>
        </tr>
    </tbody>
</table>

Notez que dans Ajout tooprovisioning, configuration et la gestion de votre compte de base de données à partir de hello portail Azure, vous pouvez également programmer créer et gérer des comptes de base de données de base de données Cosmos à l’aide de hello [API REST de Azure Cosmos DB](/rest/api/documentdb/) en tant que Bien que [client SDK](documentdb-sdk-dotnet.md).  

## <a name="databases"></a>Bases de données
Une base de données de la base de données Cosmos est un conteneur logique d’un ou plusieurs collections et d’utilisateurs, comme indiqué dans hello suivant schéma. Vous pouvez créer n’importe quel nombre de bases de données sous un toooffer de sujet de compte de base de données Cosmos DB limites.  

![Compte de base de données et modèle hiérarchique de regroupements][2]  
**Une base de données est un conteneur logique d’utilisateurs et de collections**

Une base de données peut contenir un stockage de documents presque illimité partitionné dans des collections.

### <a name="elastic-scale-of-a-cosmos-db-database"></a>Évolutivité flexible d’une base de données Cosmos DB
Une base de données de la base de données Cosmos est élastique par défaut – allant de quelques toopetabytes Go de stockage de documents SSD sauvegardé et débit approvisionné. 

Contrairement à une base de données SGBDR traditionnel, une base de données dans la base de données Cosmos n’est pas étendue tooa un seul ordinateur. Avec Cosmos DB, comme la mise à l’échelle de votre application doit toogrow, vous pouvez créer d’autres collections, les bases de données ou les deux. En effet, plusieurs applications de Microsoft utilisent Cosmos DB à l’échelle du client en créant des bases de données Cosmos DB très volumineuses, contenant chacune des milliers de collections qui regroupent des téraoctets de stockage de documents. Vous pouvez augmenter ou réduire une base de données en ajoutant ou supprimant des collections toomeet spécifications de mise à l’échelle de votre application. 

Vous pouvez créer n’importe quel nombre de regroupements au sein d’une offre de toohello d’objet de base de données. Chaque collection a stockage SSD sauvegardé et débit approvisionné pour vous en fonction du niveau de performances sélectionnés hello.

Une base de données Cosmos DB est également un conteneur d’utilisateurs. Un utilisateur, à leur tour, est un espace de noms logique pour un jeu d’autorisations qui fournit les pièces jointes, documents et affinées toocollections d’accès et d’autorisation.  

Comme avec d’autres ressources dans le modèle de ressource de base de données Cosmos hello, bases de données peuvent être créés, remplacé, supprimer, lire ou énumérées facilement à l’aide soit hello [API REST](/rest/api/documentdb/) ou l’une des hello [client SDK](documentdb-sdk-dotnet.md). COSMOS DB garantit la cohérence forte pour la lecture ou l’interrogation des métadonnées hello d’une ressource de base de données. Suppression d’une base de données automatiquement garantit que vous ne peut pas accéder à une des collections de hello ou qu’il contient des utilisateurs.   

## <a name="collections"></a>Collections
Une collection Cosmos DB est un conteneur pour vos documents JSON. 

### <a name="elastic-ssd-backed-document-storage"></a>Stockage de documents SSD flexible
Une collection est intrinsèquement flexible : elle augmente ou diminue à mesure que vous ajoutez ou supprimez des documents. Les collections sont des ressources logiques. Elles peuvent s’étendre sur plusieurs partitions physiques ou serveurs. nombre de Hello de partitions dans une collection est déterminé par DB Cosmos en fonction de la taille de stockage hello et débit approvisionné de hello de votre collection. Chaque partition dans Azure Cosmos DB dispose d’une quantité fixe de stockage SSD associé. Elle est également répliquée pour offrir une haute disponibilité. Gestion des partitions est entièrement gérée par la base de données Azure Cosmos, et ne pas avoir un code complexe toowrite ou de gérer vos partitions. Les collections Cosmos DB sont **pratiquement illimitées** en termes de débit et de stockage. 

### <a name="automatic-indexing-of-collections"></a>Indexation automatique des collections
Cosmos DB est un véritable système de base de données sans schéma. Il ne pas supposer ou nécessitent un schéma pour les documents JSON hello. Lorsque vous ajoutez la collection de documents tooa, Cosmos DB les indexe automatiquement et sont disponibles pour vous tooquery. L’indexation automatique de documents sans schéma ou index secondaire est une fonctionnalité clé de Cosmos DB. Elle est rendue possible par des techniques offrant une maintenance d’index structurée par des journaux, sans verrouillage et optimisée pour l’écriture. Cosmos DB prend en charge des volumes soutenus d’écriture très rapides, tout en continuant de servir des requêtes cohérentes. Stockage de documents et les index sont utilisé toocalculate hello stockage est consommé par chaque collection. Vous pouvez contrôler hello stockage et les performances des compromis associés à l’indexation en configurant la stratégie d’indexation hello pour une collection. 

### <a name="configuring-hello-indexing-policy-of-a-collection"></a>Configuration de la stratégie d’indexation hello d’une collection
Hello indexation de stratégie de chaque collection vous permet de toomake performances et stockage des compromis associés à l’indexation. Hello options suivantes sont disponible tooyou dans le cadre de la configuration de l’indexation :  

* Choisissez si la collection de hello indexe automatiquement tous les documents hello ou non. Par défaut, tous les documents sont automatiquement indexés. Vous pouvez choisir tooturn désactiver l’indexation automatique et ajouter de manière sélective uniquement les index toohello des documents spécifiques. À l’inverse, vous pouvez choisir de façon sélective tooexclude uniquement des documents spécifiques. Vous pouvez y parvenir en définissant des toobe de propriété automatique hello true ou false sur indexingPolicy hello d’une collection, à l’aide d’en-tête de demande hello [x-ms-indexingdirective] lors de l’insertion, de remplacement ou de suppression d’un document.  
* Choisissez si tooinclude ou exclure des chemins spécifiques ou des modèles dans vos documents à partir de hello index. Vous pouvez y parvenir en paramètre includedPaths et excludedPaths sur indexingPolicy hello d’une collection respectivement. Vous pouvez également configurer hello stockage et les performances des compromis pour la plage et hachage de requêtes pour les modèles de chemin d’accès spécifique. 
* Choisissez entre des mises à jour d'index synchrones (cohérentes) ou asynchrones (différées). Par défaut, les index hello est mise à jour synchrone sur chaque insertion, de remplacer ou de suppression d’une collection de toohello du document. Ainsi, les requêtes hello toohonor hello même niveau de cohérence que celui de lectures de document hello. Bien que Cosmos DB est optimisé en écriture et prend en charge des volumes maintenus d’écritures de document, ainsi que la maintenance d’index synchrones et traiter les requêtes de cohérence, vous pouvez configurer certaine tooupdate collections leur index tardivement. Indexation différée améliore davantage les performances d’écriture hello et est idéale pour les scénarios d’ingestion en bloc pour les collections de lectures principalement.

stratégie d’indexation de Hello peut être modifié en exécutant une commande PUT sur la collection de hello. Cela peut être obtenue via hello [client SDK](documentdb-sdk-dotnet.md), hello [Azure Portal](https://portal.azure.com) ou hello [API REST](/rest/api/documentdb/).

### <a name="querying-a-collection"></a>Interrogation d'une collection
documents Hello au sein d’une collection peuvent avoir des schémas arbitraires et vous pouvez interroger des documents d’une collection sans fournir n’importe quel schéma ou un index secondaire dès le départ. Vous pouvez interroger la collection de hello à l’aide de hello [API de DocumentDB de base de données Azure Cosmos : référence de la syntaxe SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx), qui fournit des opérateurs spatiales, relationnelles et hiérarchiques riches et extensibilité via des UDFs JavaScript. Permet de grammaire JSON pour la modélisation des documents JSON en tant qu’arborescences avec étiquettes en tant que nœuds d’arbre hello. Cette capacité est exploitée par les techniques d’indexation automatique de l’API DocumentDB et par le dialecte SQL de l’API DocumentDB. Hello langage de requête DocumetDB API se compose de trois aspects principaux :   

1. Un petit ensemble d’opérations de requête qui mappent naturellement arborescence toohello, y compris les projections et les requêtes hiérarchiques. 
2. Un sous-ensemble d'opérations relationnelles incluant la composition, le filtrage, les projections, les agrégations et les jointures réflexives. 
3. Des fonctions définies par l'utilisateur JavaScript pures, qui fonctionnent avec (1) et (2).  

modèle de requête de base de données Cosmos Hello tentatives toostrike un équilibre entre les fonctionnalités, l’efficacité et la simplicité. en mode natif, moteur de base de données de base de données Cosmos Hello compile et exécute les instructions de requête SQL hello. Vous pouvez interroger une collection à l’aide de hello [API REST](/rest/api/documentdb/) ou l’une des hello [client SDK](documentdb-sdk-dotnet.md). Hello .NET SDK est fourni avec un fournisseur LINQ.

> [!TIP]
> Vous pouvez essayer de hello API DocumentDB et exécuter des requêtes SQL sur notre jeu de données Bonjour [Query Playground](https://www.documentdb.com/sql/demo).
> 
> 

## <a name="multi-document-transactions"></a>Transactions multi-documents
Transactions de base de données fournissent un modèle de programmation sûr et prévisible pour traiter les données de toohello de modifications simultanées. Dans le système SGBDR, logique métier de hello méthode traditionnelle toowrite est toowrite **des procédures stockées** et/ou **déclencheurs** et expédiez le serveur de base de données toohello pour l’exécution transactionnelle. Dans un système SGBDR, programmeur de l’application hello est toodeal requis avec les deux langages de programmation différents : 

* Hello (non transactionnelle) application langage de programmation (par exemple, JavaScript, Python, c#, Java, etc.)
* T-SQL, hello transactionnelle langage de programmation qui est exécuté en mode natif par base de données hello

En vertu de son engagement profond tooJavaScript et de JSON directement dans le moteur de base de données hello, Cosmos DB fournit un modèle de programmation intuitif pour JavaScript en cours d’exécution en fonction de la logique d’application directement sur des collections de hello en termes de procédures stockées et déclencheurs. Ainsi, les deux éléments suivants de hello :

* Contrôler la mise en œuvre efficace de l’accès concurrentiel, restauration automatique de l’indexation de graphiques d’objets JSON hello directement dans le moteur de base de données hello
* Exprimer naturellement les flux de contrôle, variable de portée, l’attribution et l’intégration de gestion des exceptions de primitives avec des transactions de base de données directement en termes de langage de programmation JavaScript hello

logique de JavaScript Hello inscrite à un niveau de la collection peut alors émettre des opérations de base de données sur des documents de hello Hello étant donné la collection. COSMOS DB implicitement hello encapsule que JavaScript en fonction des procédures stockées et déclencheurs au sein d’un ambiante les transactions ACID avec l’isolement d’instantané entre les documents dans une collection. Pendant son exécution, hello si hello JavaScript lève une exception, hello puis la totalité de la transaction est abandonnée. Bonjour modèle de programmation qui en résulte est très simple mais puissants. Les développeurs JavaScript obtiennent un modèle de programmation « durable » tout en continuant d'utiliser les constructions de langage et les primitives de bibliothèques qui leurs sont familières.   

Hello capacité tooexecute JavaScript directement dans la base de données hello moteur Bonjour même espace d’adressage comme pool de mémoires tampons hello performant et l’exécution transactionnelle des opérations de base de données par rapport aux documents de hello d’une collection. En outre, moteur de base de données de base de données Cosmos rend un toohello profond engagement JSON et JavaScript élimine toute impédance entre les systèmes de type hello d’application et de la base de données hello.   

Après avoir créé une collection, vous pouvez inscrire des procédures stockées, déclencheurs et UDF avec une collection à l’aide de hello [API REST](/rest/api/documentdb/) ou l’une des hello [client SDK](documentdb-sdk-dotnet.md). Après l'enregistrement, vous pouvez les référencer et les exécuter. Envisagez suivant de hello entièrement écrit dans JavaScript, code hello ci-dessous prend deux arguments (nom de livre et nom de l’auteur) de procédure stockée et crée un nouveau document, les requêtes pour un document et puis met à jour – toutes les tâches dans une transaction ACID implicite. À tout moment pendant l’exécution de hello, si une exception JavaScript est levée, toute transaction de hello est abandonnée.

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();        
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            {id: name, author: author},
            function(err, documentCreated) {
                if(err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function(err, matchingDocuments) {
                        if(err) throw new Error(err.message);

                        context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don’t need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);   
                        }
                    })
            })
    };

client de Hello peut « expédition » hello ci-dessus JavaScript logique toohello base de données pour l’exécution transactionnelle via HTTP POST. Pour plus d’informations sur l’utilisation de méthodes HTTP, consultez l’article [RESTful interactions with Azure Cosmos DB resources (Interactions RESTful avec les ressources Azure Cosmos DB)](https://msdn.microsoft.com/library/azure/mt622086.aspx). 

    client.createStoredProcedureAsync(collection._self, {id: "CRUDProc", body: businessLogic})
       .then(function(createdStoredProcedure) {
            return client.executeStoredProcedureAsync(createdStoredProcedure.resource._self,
                "NoSQL Distilled",
                "Martin Fowler");
        })
        .then(function(result) {
            console.log(result);
        },
        function(error) {
            console.log(error);
        });


Notez qu’étant donné que la base de données hello comprend naturellement JSON et JavaScript, il existe aucune incompatibilité de type de système sans « Mappage OR » ou magique de génération de code nécessaires.   

Déclencheurs et procédures stockées interagissent avec les documents dans une collection via un modèle d’objet bien défini, qui expose le contexte actuel de la collecte de hello hello et de la collection.  

Collections Bonjour API DocumentDB peuvent être créé, supprimés, lire ou énumérées facilement à l’aide soit hello [API REST](/rest/api/documentdb/) ou l’une des hello [client SDK](documentdb-sdk-dotnet.md). Hello API DocumentDB fournit toujours à forte cohérence pour la lecture ou l’interrogation des métadonnées hello d’une collection. Suppression d’un regroupement automatiquement garantit que vous ne peut pas accéder aux documents de hello, les pièces jointes, procédures stockées, déclencheurs et UDF qu’il contient.   

## <a name="stored-procedures-triggers-and-user-defined-functions-udf"></a>Procédures stockées, déclencheurs et fonctions définies par l’utilisateur
Comme décrit dans la section précédente de hello, vous pouvez écrire toorun de logique d’application directement dans une transaction à l’intérieur du moteur de base de données hello. logique de l’application Hello peut être entièrement écrit en JavaScript et peut être modélisée comme une procédure stockée, déclencheur ou un fichier UDF. Hello du code JavaScript au sein d’une procédure stockée ou un déclencheur peut insérer, remplacer, supprimer, des documents de lecture ou de la requête dans une collection. Sur hello autre part, hello JavaScript dans un fichier UDF ne peut pas insérer, remplacer ou supprimer des documents. UDF énumérer les documents hello du jeu de résultats d’une requête et produisent un autre jeu de résultats. Cosmos DB applique une gouvernance des ressources basée sur une réservation stricte aux architectures mutualisées. Chaque procédure stockée, déclencheur ou un fichier UDF Obtient un quantum fixe de toodo de ressources de système d’exploitation son travail. En outre, les procédures stockées, des déclencheurs ou des UDF ne peut pas lier les bibliothèques JavaScript externes et sur liste noire si elles dépassent les budgets de ressources hello allouées toothem. Vous pouvez inscrire, annuler l’inscription des procédures stockées, des déclencheurs ou des UDF avec une collection à l’aide de hello API REST.  Une fois enregistrés, ils sont précompilés et stockés en tant que codes d'octets et sont exécutés ultérieurement. Hello après section illustre comment vous pouvez utiliser hello Cosmos DB JavaScript SDK tooregister, exécuter et annuler l’inscription d’une procédure stockée, déclencheur et un fichier UDF. Hello SDK JavaScript est un simple wrapper sur hello [API REST](/rest/api/documentdb/). 

### <a name="registering-a-stored-procedure"></a>Enregistrement d'une procédure stockée
L'enregistrement d'une procédure stockée crée une ressource de procédure stockée dans une collection via HTTP POST.  

    var storedProc = {
        id: "validateAndCreate",
        body: function (documentToCreate) {
            documentToCreate.id = documentToCreate.id.toUpperCase();

            var collectionManager = getContext().getCollection();
            collectionManager.createDocument(collectionManager.getSelfLink(),
                documentToCreate,
                function(err, documentCreated) {
                    if(err) throw new Error('Error while creating document: ' + err.message;
                    getContext().getResponse().setBody('success - created ' + 
                            documentCreated.name);
                });
        }
    };

    client.createStoredProcedureAsync(collection._self, storedProc)
        .then(function (createdStoredProcedure) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-stored-procedure"></a>Exécution d'une procédure stockée
L’exécution d’une procédure stockée est effectuée en émettant une requête HTTP POST par rapport à une ressource de procédure stockée existante en passant les paramètres toohello procédure dans le corps de la demande hello.

    var inputDocument = {id : "document1", author: "G. G. Marquez"};
    client.executeStoredProcedureAsync(createdStoredProcedure.resource._self, inputDocument)
        .then(function(executionResult) {
            assert.equal(executionResult, "success - created DOCUMENT1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-stored-procedure"></a>Annulation de l'enregistrement d'une procédure stockée
Pour annuler l’enregistrement d’une procédure stockée, il suffit d’émettre une instruction HTTP DELETE sur une ressource de procédure stockée existante.   

    client.deleteStoredProcedureAsync(createdStoredProcedure.resource._self)
        .then(function (response) {
            return;
        }, function(error) {
            console.log("Error");
        });


### <a name="registering-a-pre-trigger"></a>Enregistrement d'un pré-déclencheur
L'enregistrement d'un déclencheur s'effectue en créant une ressource de déclencheur dans une collection via HTTP POST. Vous pouvez spécifier si déclencheur de hello est un antérieur ou un type de déclencheur et hello post d’opération peut être associée à (par exemple, créer, remplacer, supprimer ou tous).   

    var preTrigger = {
        id: "upperCaseId",
        body: function() {
                var item = getContext().getRequest().getBody();
                item.id = item.id.toUpperCase();
                getContext().getRequest().setBody(item);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.All
    }

    client.createTriggerAsync(collection._self, preTrigger)
        .then(function (createdPreTrigger) {
            console.log("Successfully created trigger");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-pre-trigger"></a>Exécution d'un pré-déclencheur
L’exécution d’un déclencheur est effectuée en spécifiant le nom hello d’un déclencheur existant au moment de hello d’émettre la demande POST ou PUT/suppression de hello d’une ressource de document via l’en-tête de demande hello.  

    client.createDocumentAsync(collection._self, { id: "doc1", key: "Love in hello Time of Cholera" }, { preTriggerInclude: "upperCaseId" })
        .then(function(createdDocument) {
            assert.equal(createdDocument.resource.id, "DOC1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-pre-trigger"></a>Annulation de l'enregistrement d'un pré-déclencheur
Pour annuler l’enregistrement d’un déclencheur, il suffit d’émettre une instruction HTTP DELETE sur une ressource de déclencheur existante.  

    client.deleteTriggerAsync(createdPreTrigger._self);
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

### <a name="registering-a-udf"></a>Enregistrement d'une fonction définie par l'utilisateur
L'enregistrement d'une fonction définie par l'utilisateur s'effectue en créant une ressource de fonction définie par l'utilisateur dans une collection via HTTP POST.  

    var udf = { 
        id: "mathSqrt",
        body: function(number) {
                return Math.sqrt(number);
        },
    };
    client.createUserDefinedFunctionAsync(collection._self, udf)
        .then(function (createdUdf) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-udf-as-part-of-hello-query"></a>L’exécution d’une UDF dans le cadre de la requête de hello
Un fichier UDF peut être spécifié dans le cadre de la requête SQL hello et est utilisé comme un cœur de hello moyen tooextend [langage de requête SQL hello API DocumentDB](https://msdn.microsoft.com/library/azure/dn782250.aspx).

    var filterQuery = "SELECT udf.mathSqrt(r.Age) AS sqrtAge FROM root r WHERE r.FirstName='John'";
    client.queryDocuments(collection._self, filterQuery).toArrayAsync();
        .then(function(queryResponse) {
            var queryResponseDocuments = queryResponse.feed;
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-udf"></a>Annulation de l'enregistrement d'une fonction définie par l'utilisateur
Pour annuler l’enregistrement d’une fonction définie par l’utilisateur, il suffit d’émettre une instruction HTTP DELETE sur une ressource de fonction définie par l’utilisateur existante.  

    client.deleteUserDefinedFunctionAsync(createdUdf._self)
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

Bien que des extraits de code hello ci-dessus a montré l’inscription de hello (POST), d’annulation d’inscription (PUT), liste/lecture (GET) et l’exécution (POST) via hello [SDK JavaScript](https://github.com/Azure/azure-documentdb-js), vous pouvez également utiliser hello [API REST](/rest/api/documentdb/) ou autres [client SDK](documentdb-sdk-dotnet.md). 

## <a name="documents"></a>Documents
Vous pouvez insérer, remplacer, supprimer, lire, énumérer et interroger arbitrairement des documents JSON dans une collection. COSMOS DB n’impose pas de n’importe quel schéma et ne nécessite pas d’index secondaires dans toosupport commande interrogation sur des documents dans une collection. taille maximale de Hello pour un document est 2 Mo.   

En étant un service de base de données véritablement ouvert, Cosmos DB n’invente pas de types de données spécialisés (par exemple, les valeurs de date et heure) ou d’encodage spécifique pour les documents JSON. Notez que Cosmos DB ne requiert pas de n’importe quel spéciaux JSON conventions toocodify hello des relations entre les divers documents ; Hello SQL syntaxe de base de données Cosmos fournit des opérateurs de requête très puissante de relationnelle et hiérarchique tooquery et projet des documents sans annotations spéciales ou des relations de toocodify nécessaire entre les documents à l’aide des propriétés distinctives.  

Comme avec toutes les autres ressources, vous pouvez créer des documents, remplacées, supprimé, lire, énumérées et interrogé facilement à l’aide des API REST ou des hello [client SDK](documentdb-sdk-dotnet.md). Suppression d’un document instantanément libère tooall correspondante de quota hello de pièces jointes de hello imbriqué. Hello en lecture au niveau de la cohérence des documents suit la règle de cohérence hello sur le compte de base de données hello. Vous pouvez remplacer cette stratégie en fonction de la demande, selon les besoins de cohérence des données de votre application. Lors de l’interrogation de documents, hello lire cohérence suit hello est définie sur la collection de hello de mode d’indexation. Pour « cohérent », il suit la règle de cohérence du compte hello. 

## <a name="attachments-and-media"></a>Pièces jointes et éléments multimédias
COSMOS DB vous permet de toostore binaire BLOB/média avec Cosmos DB (maximum de 2 Go par compte) ou tooyour multimédias à distance propre magasin. Il vous permet également métadonnées de hello toorepresent d’un support en termes d’un document spécial appelé pièce jointe. Une pièce jointe dans la base de données Cosmos est un document (JSON) spécial références hello multimédia/objet blob stocké ailleurs. Une pièce jointe est simplement un document spécial qui capture des métadonnées hello (emplacement, auteur, etc.) d’un support stocké dans un stockage à distance. 

Considérons une application de lecture social qui utilise des annotations manuscrites de toostore Cosmos de base de données et métadonnées, y compris les commentaires, met en surbrillance, signets, les évaluations, aime/goûts etc. associés pour un livre électronique d’un utilisateur donné.   

* Hello contenu du livre hello lui-même est stocké dans le stockage des supports hello soit disponible en tant que partie d’un compte de base de données de base de données Cosmos ou d’un magasin de support à distance. 
* Une application peut stocker chaque métadonnée de l'utilisateur dans un document distinct (par exemple, les métadonnées de Jean pour le livre1 sont stockées dans un document référencé par le chemin /colls/jean/docs/livre1). 
* Les pièces jointes pointant vers les pages de contenu toohello d’un livre donné d’un utilisateur sont stockés dans le document correspondant de hello /colls/joe/docs/book1/chapter1, par exemple, /colls/joe/docs/book1/chapter2 etc.. 

Notez que les exemples hello répertoriés ci-dessus utilisent la hiérarchie des ressources ID convivial tooconvey hello. Ressources accessibles via des API REST de hello via l’ID de ressource unique. 

Pour les supports hello qui est géré par la base de données Cosmos, propriété _media de hello de pièce jointe de hello référence media hello par son URI. COSMOS DB garantit media de collecter hello toogarbage lorsque toutes les références en suspens hello sont supprimés. COSMOS DB génère la pièce jointe de hello lorsque vous téléchargez de nouveau support de sauvegarde hello et renseigne automatiquement des hello _media toopoint toohello nouvellement ajoutée media. Si vous choisissez le support de hello toostore dans un magasin d’objets blob distants géré par vous (par exemple OneDrive, le stockage Azure, DropBox etc.), vous pouvez toujours utiliser le support de pièces jointes tooreference hello. Dans ce cas, vous serez créer vous-même les pièces jointes de hello et remplissez sa propriété _media.   

Comme avec toutes les autres ressources, les pièces jointes peuvent être créés, remplacé, supprimer, lire ou énumérées facilement à l’aide des API REST ou des clients de hello kits de développement logiciel. Comme des documents, hello lire le niveau de cohérence de pièces jointes suit la règle de cohérence hello sur le compte de base de données hello. Vous pouvez remplacer cette stratégie en fonction de la demande, selon les besoins de cohérence des données de votre application. Lors de l’interrogation pour les pièces jointes, hello lire cohérence suit hello est définie sur la collection de hello de mode d’indexation. Pour « cohérent », il suit la règle de cohérence du compte hello. 
 

## <a name="users"></a>Utilisateurs
Un utilisateur de Cosmos DB correspond à un espace de noms logique pour le regroupement des autorisations. Un utilisateur de base de données Cosmos peut-être correspondre tooa utilisateur dans un système de gestion d’identité ou un rôle d’application prédéfinie. Pour la base de données Cosmos, un utilisateur représente simplement un toogroup abstraction un jeu d’autorisations dans une base de données.   

Pour implémenter une architecture mutualisée dans votre application, vous pouvez créer des utilisateurs dans DB Cosmos correspondant utilisateurs réels de tooyour ou locataires hello de votre application. Vous pouvez ensuite créer des autorisations pour un utilisateur donné qui correspondent toohello le contrôle d’accès sur les différentes collections, documents, pièces jointes, etc..   

Comme vos applications ont besoin tooscale avec la croissance de l’utilisateur, vous pouvez adopter différentes méthodes tooshard vos données. Vous pouvez modéliser chacun de vos utilisateurs comme suit :   

* Chaque utilisateur est mappé à tooa de base de données.
* Chaque utilisateur est mappé à tooa collection. 
* Les documents correspondant aux utilisateurs de toomultiple accédez tooa dédiée de collection. 
* Les documents correspondant aux utilisateurs de toomultiple accédez jeu tooa de collections.   

Quel que soit le choix de la stratégie de partitionnement spécifique de hello, vous pouvez modéliser vos utilisateurs réels en tant qu’utilisateurs de base de données de la base de données Cosmos et associer des autorisations de granularité fine tooeach utilisateur.  

![Regroupements d’utilisateurs][3]  
**Stratégies de partitionnement et modélisation des utilisateurs**

Comme toutes les autres ressources, les utilisateurs de base de données Cosmos peuvent être créés, remplacé, supprimer, lire ou énumérées facilement à l’aide des API REST ou des clients de hello kits de développement logiciel. COSMOS DB fournit toujours à forte cohérence pour la lecture ou l’interrogation des métadonnées hello d’une ressource de l’utilisateur. Il est important de noter que la suppression d’un utilisateur automatiquement garantit que les autorisations hello qu’il contient ne peut pas accéder à. Même si hello Cosmos DB récupère quota hello d’autorisations de hello dans le cadre de l’utilisateur hello supprimé en arrière-plan de hello, les autorisations hello supprimé est instantanément à nouveau disponible pour vous toouse.  

## <a name="permissions"></a>Autorisations
Pour le contrôle des accès, les ressources telles que les comptes de base de données, les bases de données, les utilisateurs et les autorisations sont considérées comme des ressources d’ *administration* , car elles requièrent des privilèges d’administrateur. Sur hello autre part, y compris les collections hello, documents, pièces jointes, procédures stockées, déclencheurs, des ressources et UDF sont limitent sous une base de données et considérées comme *ressources d’application*. Correspondant toohello deux types de ressources et rôles hello y accéder (à savoir un administrateur de hello et utilisateur), le modèle d’autorisation de hello définit deux types de *clés d’accès*: *clé principale* et *clé de ressource*. clé principale de Hello fait partie d’un compte de base de données hello et est fournie toohello développeur (ou l’administrateur) qui est mise en service de compte de base de données hello. Cette clé principale intègre la sémantique de l’administrateur, dans la mesure où il peut être utilisé tooauthorize tooboth de l’accès d’administration et les ressources d’application. En revanche, une clé de ressource est une clé d’accès granulaires qui permet l’accès tooa *spécifique* ressource d’application. Par conséquent, il capture relation hello entre une base de données utilisateur hello et hello autorisations hello utilisateur dispose d’une ressource spécifique (par exemple, collection, document, pièce jointe, procédure stockée, déclencheur ou UDF).   

Hello tooobtain de façon uniquement qu'une clé de ressource est en créant une ressource d’autorisation sous un utilisateur donné. Notez que, dans l’ordre toocreate ou récupérer une autorisation, une clé principale doit être présentée dans l’en-tête d’autorisation hello. Une ressource autorisation lie un utilisateur de ressources, accès et hello hello. Après avoir créé une ressource d’autorisation, utilisateur de hello doit uniquement toopresent clé de ressource associée hello dans l’ordre toogain accès toohello ressource. Par conséquent, une clé de ressource peut être considérée comme une représentation logique et compacte de ressource d’autorisation hello.  

Comme avec toutes les autres ressources, autorisations dans la base de données Cosmos peuvent être créées, remplacé, supprimer, lire ou énumérées facilement à l’aide des API REST ou des clients de hello kits de développement logiciel. COSMOS DB fournit toujours à forte cohérence pour la lecture ou l’interrogation des métadonnées hello d’une autorisation. 

## <a name="next-steps"></a>Étapes suivantes
Pour en savoir plus sur l’utilisation des ressources avec des commandes HTTP, consultez l’article [RESTful interactions with Cosmos DB resources (Interactions RESTful avec les ressources Cosmos DB)](https://msdn.microsoft.com/library/azure/mt622086.aspx).

[1]: media/documentdb-resources/resources1.png
[2]: media/documentdb-resources/resources2.png
[3]: media/documentdb-resources/resources3.png

