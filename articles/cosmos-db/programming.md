---
title: "programmation de JavaScript côté aaaServer pour la base de données Azure Cosmos | Documents Microsoft"
description: "Découvrez comment toowrite de base de données Azure Cosmos toouse procédures stockées, les déclencheurs de base de données et les fonctions définies par l’utilisateur (UDF) dans JavaScript. Obtenez notamment des conseils en matière de programmation de base de données."
keywords: "Déclencheurs de base de données, procédure stockée, procédure stockée, programme de base de données, sproc, documentdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: 
author: aliuy
manager: jhubbard
editor: mimig
ms.assetid: 0fba7ebd-a4fc-4253-a786-97f1354fbf17
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: andrl
ms.openlocfilehash: 5a011d1c4b0b5908d5de73607a1bc328ed1711d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-server-side-programming-stored-procedures-database-triggers-and-udfs"></a>Programmation Azure Cosmos DB côté serveur : procédures stockées, déclencheurs de base de données et fonctions définies par l’utilisateur
Découvrez comment l’exécution transactionnelle de JavaScript intégrée au langage d’Azure Cosmos DB permet aux développeurs d’écrire des **procédures stockées**, des **déclencheurs** et des **fonctions définies par l’utilisateur (FDU)** en mode natif dans une version [ECMAScript 2015](http://www.ecma-international.org/ecma-262/6.0/) pour JavaScript. Cela vous permet de logique d’application toowrite base de données programme qui peut être livrée et exécutée directement sur les partitions de stockage de base de données hello. 

Nous vous recommandons de mise en route démarrée par regarder hello suivant vidéo, où Andrew Liu fournit une brève introduction de tooCosmos de base de données modèle de programmation côté serveur de base de données. 

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-Demo-A-Quick-Intro-to-Azure-DocumentDBs-Server-Side-Javascript/player]
> 
> 

Ensuite, retourner toothis article, où vous allez apprendre toohello de réponses hello suivant questions :  

* Comment écrire une procédure stockée, un déclencheur ou une fonction définie par l'utilisateur à l'aide de JavaScript ?
* Comment Azure Cosmos DB offre-il une garantie ACID ?
* Comment les transactions fonctionnent-elles dans Azure Cosmos DB ?
* Qu'est-ce que les pré-déclencheurs et les post-déclencheurs, et comment procède-t-on pour leur écriture ?
* Comment enregistrer et exécuter une procédure stockée, un déclencheur ou une fonction définie par l'utilisateur sur la base de l'architecture REST avec HTTP ?
* Les kits de développement logiciel Cosmos DB toocreate disponible et exécutez et procédures stockées, déclencheurs, UDF ?

## <a name="introduction-toostored-procedure-and-udf-programming"></a>Introduction tooStored procédure et la programmation des UDF
Cette approche de *« JavaScript sous la forme d’un jour modern T-SQL »* évite aux développeurs d’application de la complexité hello des incompatibilités au niveau du système de type et les technologies de mappage relationnel objet. Elle comporte également plusieurs avantages intrinsèques qui peuvent être des applications riches toobuild utilisé :  

* **Logique procédurale :** JavaScript sous la forme d’un langage de programmation de haut niveau, fournit une interface riche et familière de tooexpress une logique métier. Vous pouvez effectuer des séquences de données toohello proche des opérations complexes.
* **Transactions atomiques :** Azure Cosmos DB garantit que les opérations de base de données effectuées dans un déclencheur ou une procédure stockée sont atomiques. Cela permet à une application de combiner des applications connexes en un seul lot de façon à ce que toutes réussissent ou qu’aucune ne réussisse. 
* **Performances :** hello fait que JSON est le système de type de langage Javascript toohello intrinsèquement mappé et est également permet à l’unité de stockage dans la base de données Cosmos hello pour un nombre d’optimisations de matérialisation différée de JSON documents dans la mémoire tampon de hello pool des rendre disponibles à la demande toohello l’exécution de code. Il existe des gains de performance plus associés avec l’envoi de journaux de base de données toohello de logique métier :
  
  * Traitement par lot - Les développeurs peuvent regrouper les opérations telles que les insertions et les envoyer en bloc. coût de la latence du trafic réseau Hello et des transactions distinctes hello magasin toocreate généraux sont considérablement réduites. 
  * Précompilation – Cosmos DB précompilation des procédures stockées, déclencheurs et définies par l’utilisateur (UDF) de fonctions tooavoid le coût de compilation JavaScript pour chaque appel. Hello surcharge de la création de code d’octet hello pour la logique procédurale de hello est amorti tooa présenter d’avantage.
  * Séquencement - De nombreuses opérations requièrent un effet secondaire (« déclencheur ») qui implique potentiellement d'effectuer une ou plusieurs opérations de stockage secondaires. À part l’atomicité, il est plus performant lorsque déplacées toohello server. 
* **Encapsulation :** les procédures stockées peuvent être logique toogroup utilisé dans un seul emplacement. Ceci présente deux avantages :
  * Il ajoute une couche d’abstraction sur les données brutes de hello, qui permet aux données architectes tooevolve leurs applications indépendamment à partir des données de hello. Cela est particulièrement avantageux lorsque les données de salutation sont sans schéma, en raison des hypothèses fragile toohello qui peuvent nécessiter une toobe intégrée application hello s’ils ont toodeal avec des données directement.  
  * Cette abstraction permet aux entreprises de sécuriser leurs données en rationalisant l’accès à partir de scripts de hello hello.  

Hello création et l’exécution des déclencheurs de base de données, d’une procédure stockée et d’opérateurs de requête personnalisée est pris en charge par le biais hello [API REST](/rest/api/documentdb/), [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio/releases), et [client SDK](documentdb-sdk-dotnet.md) sur de nombreuses plateformes, y compris .NET, Node.js et JavaScript.

Ce didacticiel utilise hello [SDK Node.js avec Q promesses](http://azure.github.io/azure-documentdb-node-q/) tooillustrate syntaxe et l’utilisation de procédures stockées, des déclencheurs et des UDF.   

## <a name="stored-procedures"></a>Procédures stockées
### <a name="example-write-a-simple-stored-procedure"></a>Exemple : Écriture d’une simple procédure stockée
Commençons par une simple procédure stockée qui renvoie une réponse « Hello World ».

    var helloWorldStoredProc = {
        id: "helloWorld",
        serverScript: function () {
            var context = getContext();
            var response = context.getResponse();

            response.setBody("Hello, World");
        }
    }


Les procédures stockées sont enregistrées par collection, et elles peuvent s'appliquer à tout document et toute pièce jointe figurant dans cette collection. Hello extrait de code suivant montre comment tooregister hello helloWorld procédure stockée avec une collection. 

    // register hello stored procedure
    var createdStoredProcedure;
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', helloWorldStoredProc)
        .then(function (response) {
            createdStoredProcedure = response.resource;
            console.log("Successfully created stored procedure");
        }, function (error) {
            console.log("Error", error);
        });


Une fois la procédure stockée hello est inscrit, nous pouvons exécuter par rapport à la collection de hello et lire hello les résultats au client de hello. 

    // execute hello stored procedure
    client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/helloWorld')
        .then(function (response) {
            console.log(response.result); // "Hello, World"
        }, function (err) {
            console.log("Error", error);
        });


objet de contexte Hello fournit l’accès tooall les opérations qui peuvent être effectuées sur le stockage de base de données Cosmos, ainsi que pour accéder aux objets de demande et de réponse toohello. Dans ce cas, nous avons utilisé hello objet tooset hello corps de réponse de réponse hello qui a été envoyé arrière toohello client. Pour plus d’informations, consultez toohello [JavaScript de base de données Azure Cosmos server documentation SDK](http://azure.github.io/azure-documentdb-js-server/).  

Nous développer cet exemple et ajouter plusieurs fonctionnalités de la base de données toohello de procédure stockée. Les procédures stockées peuvent créer, mettre à jour, lire, interroger et supprimer des documents et pièces jointes à l’intérieur de la collection de hello.    

### <a name="example-write-a-stored-procedure-toocreate-a-document"></a>Exemple : Écrire une procédure stockée de toocreate un document
extrait de code Hello suivant montre comment toouse hello toointeract d’objet de contexte avec des ressources de base de données Cosmos.

    var createDocumentStoredProc = {
        id: "createMyDocument",
        serverScript: function createMyDocument(documentToCreate) {
            var context = getContext();
            var collection = context.getCollection();

            var accepted = collection.createDocument(collection.getSelfLink(),
                  documentToCreate,
                  function (err, documentCreated) {
                      if (err) throw new Error('Error' + err.message);
                      context.getResponse().setBody(documentCreated.id)
                  });
            if (!accepted) return;
        }
    }


Cette procédure stockée accepte comme entrée documentToCreate, corps hello d’un toobe document créé dans la collection actuelle de hello. Toutes ces opérations sont asynchrones et dépendent de rappels de fonction JavaScript. fonction de rappel Hello possède deux paramètres, un pour l’objet d’erreur hello hello échoue et l’autre pour hello créé l’objet. À l’intérieur du rappel de hello, les utilisateurs peuvent gérer l’exception de hello ou lever une erreur. Si un rappel n’est pas fourni, et il existe une erreur, le runtime de base de données Azure Cosmos hello génère une erreur.   

Dans l’exemple hello ci-dessus, le rappel de hello génère une erreur en cas d’échec de l’opération de hello. Sinon, il définit les id hello Hello créé le document en tant que corps hello du client de toohello réponse hello. Voici la façon dont cette procédure stockée est exécutée avec des paramètres d'entrée.

    // register hello stored procedure
    client.createStoredProcedureAsync('dbs/testdb/colls/testColl', createDocumentStoredProc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;

            // run stored procedure toocreate a document
            var docToCreate = {
                id: "DocFromSproc",
                book: "hello Hitchhiker’s Guide toohello Galaxy",
                author: "Douglas Adams"
            };

            return client.executeStoredProcedureAsync('dbs/testdb/colls/testColl/sprocs/createMyDocument',
                  docToCreate);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response); // "DocFromSproc"
    }, function (error) {
        console.log("Error", error);
    });


Notez que cette procédure stockée peut tootake modifié un tableau d’instances de document en tant qu’entrée et créer les hello même stockée dans l’exécution de la procédure au lieu de réseau de plusieurs demandes toocreate d'entre eux individuellement. Cela peut être utilisé tooimplement un importateur en bloc efficace pour DB Cosmos (décrit plus loin dans ce didacticiel).   

exemple Hello décrit a montré comment toouse des procédures stockées. Nous allons aborder les déclencheurs et les fonctions définies par l’utilisateur (UDF) plus loin dans le didacticiel de hello.

## <a name="database-program-transactions"></a>Transactions de programme de base de données
Une transaction dans une base de données classique peut être définie comme étant une séquence d'opérations effectuées en tant qu'unité de travail logique unique. Chaque transaction offre des **garanties ACID**. ACID est un acronyme bien connu qui est l’abréviation de quatre propriétés : Atomicité, Cohérence, Isolation et Durabilité.  

En bref, l’atomicité garantit que tout le travail hello effectué à l’intérieur d’une transaction est considéré comme une unité unique où soit sont validées ou none. Cohérence permet de s’assurer que les données de salutation sont toujours en bon état interne entre les transactions. Isolation garantit que deux transactions n’interfèrent avec d’autres : en général, la plupart des systèmes de fournissent plusieurs niveaux d’isolement qui peuvent être utilisés selon les besoins de l’application hello. Durabilité garantit que toute modification est validée dans la base de données hello sera toujours présente.   

Dans la base de données Cosmos, JavaScript est hébergé dans hello même espace mémoire en tant que base de données hello. Par conséquent, les demandes effectuées au sein des procédures stockées et les déclencheurs s’exécutent dans hello même étendue d’une session de base de données. Cela permet de Cosmos DB tooguarantee ACID pour toutes les opérations qui font partie d’un seul procédure stocké/déclencheur. Tenez compte de hello suit stocké la définition de la procédure :

    // JavaScript source code
    var exchangeItemsSproc = {
        id: "exchangeItems",
        serverScript: function (playerId1, playerId2) {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            var player1Document, player2Document;

            // query for players
            var filterQuery = 'SELECT * FROM Players p where p.id  = "' + playerId1 + '"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery, {},
                function (err, documents, responseOptions) {
                    if (err) throw new Error("Error" + err.message);

                    if (documents.length != 1) throw "Unable toofind both names";
                    player1Document = documents[0];

                    var filterQuery2 = 'SELECT * FROM Players p where p.id = "' + playerId2 + '"';
                    var accept2 = collection.queryDocuments(collection.getSelfLink(), filterQuery2, {},
                        function (err2, documents2, responseOptions2) {
                            if (err2) throw new Error("Error" + err2.message);
                            if (documents2.length != 1) throw "Unable toofind both names";
                            player2Document = documents2[0];
                            swapItems(player1Document, player2Document);
                            return;
                        });
                    if (!accept2) throw "Unable tooread player details, abort ";
                });

            if (!accept) throw "Unable tooread player details, abort ";

            // swap hello two players’ items
            function swapItems(player1, player2) {
                var player1ItemSave = player1.item;
                player1.item = player2.item;
                player2.item = player1ItemSave;

                var accept = collection.replaceDocument(player1._self, player1,
                    function (err, docReplaced) {
                        if (err) throw "Unable tooupdate player 1, abort ";

                        var accept2 = collection.replaceDocument(player2._self, player2,
                            function (err2, docReplaced2) {
                                if (err) throw "Unable tooupdate player 2, abort"
                            });

                        if (!accept2) throw "Unable tooupdate player 2, abort";
                    });

                if (!accept) throw "Unable tooupdate player 1, abort";
            }
        }
    }

    // register hello stored procedure in Node.js client
    client.createStoredProcedureAsync(collection._self, exchangeItemsSproc)
        .then(function (response) {
            var createdStoredProcedure = response.resource;
        }
    );

Cette procédure stockée utilise des transactions au sein d’un jeu application tootrade des éléments entre deux lecteurs en une seule opération. Hello stockées deux documents procédure tentatives tooread que chaque lecteur toohello correspondant ID passée en tant qu’argument. Si les deux documents de lecteur sont trouvés, puis procédure stockée hello met à jour les documents hello en échangeant leurs éléments. Si des erreurs se produisent le long de la façon de hello, elle lève une exception de JavaScript qui abandonne implicitement des transactions de hello.

Si hello procédure stockée hello de collection est inscrit sur est une collection de partition unique, documents de hello tooall étendue au sein de la collection de hello est hello transaction. Si la collection de hello est partitionnée, les procédures stockées sont exécutées dans la portée de transaction hello d’une clé de partition unique. Stockée de chaque exécution de la procédure doit comporter une valeur de clé de partition toohello étendue hello de la transaction doit s’exécuter sous. Pour plus d’informations, consultez [Partitionnement dans Azure Cosmos DB](partition-data.md).

### <a name="commit-and-rollback"></a>Validation et restauration
Les transactions sont intégrées de façon approfondie et native dans le modèle de programmation JavaScript d’Azure Cosmos DB. Dans une fonction JavaScript, toutes les opérations sont automatiquement encapsulées dans une transaction unique. Si hello JavaScript se termine sans qu’aucune exception, base de données toohello hello opérations sont validées. En effet, hello « instructions BEGIN TRANSACTION » et « COMMIT TRANSACTION » dans les bases de données relationnelles sont implicites dans la base de données Cosmos.  

S’il existe une exception est propagée à partir du script de hello, le runtime JavaScript Cosmos DB annule toute transaction de hello. Comme indiqué précédemment dans hello exemple, en levant une exception est équivalent effectivement tooa « ROLLBACK TRANSACTION » dans la base de données Cosmos.

### <a name="data-consistency"></a>Cohérence des données
Déclencheurs et procédures stockées sont toujours exécutées sur le réplica principal de hello du conteneur de base de données Azure Cosmos hello. Cela permet de s'assurer que les lectures à partir des procédures stockées offrent une cohérence forte. Les requêtes utilisant les fonctions définies par l’utilisateur peuvent être exécutées sur hello principal ou de n’importe quel réplica secondaire, mais nous nous assurons que toomeet hello demandée au niveau de cohérence en choisissant de réplica approprié de hello.

## <a name="bounded-execution"></a>Exécution limitée
Toutes les opérations de base de données Cosmos doivent se terminer dans le serveur hello spécifié durée du délai d’attente de la demande. Cette contrainte s’applique également à des fonctions de tooJavaScript (procédures stockées, déclencheurs et fonctions définies par l’utilisateur). Si une opération ne se termine pas avec ce délai, hello transaction est restaurée. Fonctions JavaScript doivent terminer délai hello ou implémenter une exécution toobatch/reprise de modèle en fonction de continuation.  

Dans le développement de toosimplify commande stockées procédures et déclencheurs toohandle des limites de temps, toutes les fonctions sous l’objet de collection hello (pour créer, lire, remplacer et supprimer des documents et des pièces jointes) retournent une valeur booléenne qui représente si qui l’opération sera effectuée. Si cette valeur est false, cela indique que délai hello est sur tooexpire et que cette procédure hello doit encapsuler l’exécution des requêtes.  Opérations en file d’attente toohello préalable première opération de magasin non accepté est garanti que toocomplete si la procédure stockée hello est terminée dans le temps et ne pas en file d’attente d’autres requêtes.  

Les fonctions JavaScript sont également liées lors de la consommation de ressources. COSMOS DB réserve le débit par la collection en fonction de la taille de hello configuré d’un compte de base de données. Le débit est exprimé en unités normalisées de processeur, de mémoire et de consommation d'E/S, appelées unités de demande. Les fonctions JavaScript peuvent utiliser d’un grand nombre d’unités réservées dans un délai court et peuvent obtenir limitée si limite la collection hello est atteinte. Procédures stockées utilisant beaucoup de ressources peuvent également être disponibilité tooensure mis en quarantaine des opérations de base de données primitif.  

### <a name="example-bulk-importing-data-into-a-database-program"></a>Exemple : importation de données en bloc dans un programme de base de données
Voici un exemple d’une procédure stockée qui est écrit toobulk-importer des documents dans une collection. Remarque hello stockage l’exécution des procédures handles limitées en vérifiant hello booléen valeur de retour à partir de createDocument, et puis utilise hello le nombre de documents insérées dans chaque appel de la progression de tootrack et de reprise de la procédure stockée hello sur des lots.

    function bulkImport(docs) {
        var collection = getContext().getCollection();
        var collectionLink = collection.getSelfLink();

        // hello count of imported docs, also used as current doc index.
        var count = 0;

        // Validate input.
        if (!docs) throw new Error("hello array is undefined or null.");

        var docsLength = docs.length;
        if (docsLength == 0) {
            getContext().getResponse().setBody(0);
        }

        // Call hello create API toocreate a document.
        tryCreate(docs[count], callback);

        // Note that there are 2 exit conditions:
        // 1) hello createDocument request was not accepted. 
        //    In this case hello callback will not be called, we just call setBody and we are done.
        // 2) hello callback was called docs.length times.
        //    In this case all documents were created and we don’t need toocall tryCreate anymore. Just call setBody and we are done.
        function tryCreate(doc, callback) {
            var isAccepted = collection.createDocument(collectionLink, doc, callback);

            // If hello request was accepted, callback will be called.
            // Otherwise report current count back toohello client, 
            // which will call hello script again with remaining set of docs.
            if (!isAccepted) getContext().getResponse().setBody(count);
        }

        // This is called when collection.createDocument is done in order tooprocess hello result.
        function callback(err, doc, options) {
            if (err) throw err;

            // One more document has been inserted, increment hello count.
            count++;

            if (count >= docsLength) {
                // If we created all documents, we are done. Just set hello response.
                getContext().getResponse().setBody(count);
            } else {
                // Create next document.
                tryCreate(docs[count], callback);
            }
        }
    }

## <a id="trigger"></a> Déclencheurs de base de données
### <a name="database-pre-triggers"></a>Pré-déclencheurs de base de données
Azure Cosmos DB fournit des déclencheurs qui sont exécutés ou déclenchés par une opération sur un document. Par exemple, vous pouvez spécifier un déclencheur avant lorsque vous créez un document – ce déclencheur préliminaire s’exécutera avant la création de document de hello. Hello Voici un exemple de comment pré-déclencheurs peuvent être des propriétés de hello toovalidate utilisées d’un document qui est en cours de création :

    var validateDocumentContentsTrigger = {
        id: "validateDocumentContents",
        serverScript: function validate() {
            var context = getContext();
            var request = context.getRequest();

            // document toobe created in hello current operation
            var documentToCreate = request.getBody();

            // validate properties
            if (!("timestamp" in documentToCreate)) {
                var ts = new Date();
                documentToCreate["my timestamp"] = ts.getTime();
            }

            // update hello document that will be created
            request.setBody(documentToCreate);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.Create
    }


Et hello code d’inscription côté client Node.js correspondant pour le déclencheur de hello :

    // register pre-trigger
    client.createTriggerAsync(collection.self, validateDocumentContentsTrigger)
        .then(function (response) {
            console.log("Created", response.resource);
            var docToCreate = {
                id: "DocWithTrigger",
                event: "Error",
                source: "Network outage"
            };

            // run trigger while creating above document 
            var options = { preTriggerInclude: "validateDocumentContents" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function (error) {
            console.log("Error", error);
        })
    .then(function (response) {
        console.log(response.resource); // document with timestamp property added
    }, function (error) {
        console.log("Error", error);
    });


Les pré-déclencheurs ne peuvent pas avoir de paramètres en entrée. objet de demande Hello peut être le message de demande utilisé toomanipulate hello associé hello opération. Ici, déclencheur avant de hello est en cours d’exécution avec la création d’un document hello et corps du message de demande hello contient hello document toobe est créé au format JSON.   

Lorsque les déclencheurs sont enregistrées, les utilisateurs peuvent spécifier des opérations de hello, il peut s’exécuter avec. Ce déclencheur a été créé avec TriggerOperation.Create, ce qui signifie que suivant de hello n’est pas autorisée.

    var options = { preTriggerInclude: "validateDocumentContents" };

    client.replaceDocumentAsync(docToReplace.self,
                  newDocBody, options)
    .then(function (response) {
        console.log(response.resource);
    }, function (error) {
        console.log("Error", error);
    });

    // Fails, can’t use a create trigger in a replace operation

### <a name="database-post-triggers"></a>Post-déclencheurs de base de données
Les post-déclencheurs, comme les pré-déclencheurs, sont associés à une opération dans un document et n'acceptent pas de paramètres en entrée. Ils ne s’exécutent **après** opération de hello est terminée et ont accès toohello réponse message qui est envoyé toohello client.   

Hello, l’exemple suivant montre les post-déclencheurs en action :

    var updateMetadataTrigger = {
        id: "updateMetadata",
        serverScript: function updateMetadata() {
            var context = getContext();
            var collection = context.getCollection();
            var response = context.getResponse();

            // document that was created
            var createdDocument = response.getBody();

            // query for metadata document
            var filterQuery = 'SELECT * FROM root r WHERE r.id = "_metadata"';
            var accept = collection.queryDocuments(collection.getSelfLink(), filterQuery,
                updateMetadataCallback);
            if(!accept) throw "Unable tooupdate metadata, abort";

            function updateMetadataCallback(err, documents, responseOptions) {
                if(err) throw new Error("Error" + err.message);
                         if(documents.length != 1) throw 'Unable toofind metadata document';

                         var metadataDocument = documents[0];

                         // update metadata
                         metadataDocument.createdDocuments += 1;
                         metadataDocument.createdNames += " " + createdDocument.id;
                         var accept = collection.replaceDocument(metadataDocument._self,
                               metadataDocument, function(err, docReplaced) {
                                      if(err) throw "Unable tooupdate metadata, abort";
                               });
                         if(!accept) throw "Unable tooupdate metadata, abort";
                         return;                    
            }                                                                                            
        },
        triggerType: TriggerType.Post,
        triggerOperation: TriggerOperation.All
    }


déclencheur de Hello peut être inscrit comme indiqué dans hello suivant l’exemple.

    // register post-trigger
    client.createTriggerAsync('dbs/testdb/colls/testColl', updateMetadataTrigger)
        .then(function(createdTrigger) { 
            var docToCreate = { 
                name: "artist_profile_1023",
                artist: "hello Band",
                albums: ["Hellujah", "Rotators", "Spinning Top"]
            };

            // run trigger while creating above document 
            var options = { postTriggerInclude: "updateMetadata" };

            return client.createDocumentAsync(collection.self,
                  docToCreate, options);
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });


Ce déclencheur interroge pour le document de métadonnées hello et met à jour avec des détails sur le document de hello nouvellement créé.  

Une chose importante toonote est hello **transactionnelle** l’exécution des déclencheurs dans la base de données Cosmos. Ce déclencheur après s’exécute en tant que partie de hello même transaction que la création de hello hello document d’origine. Par conséquent, si nous lève une exception à partir de post-déclencheur de hello (par exemple si nous sommes le document de métadonnées hello tooupdate impossible), toute transaction de hello échouera et être restaurée. Aucun document n'est créé et une exception est renvoyée.  

## <a id="udf"></a>Fonctions définies par l’utilisateur
Fonctions définies par l’utilisateur (UDF) sont la grammaire du langage de requête utilisé tooextend hello DocumentDB API SQL et implémentent la logique métier personnalisée. Elles peuvent uniquement être appelées à partir de requêtes. Ils n’ont pas d’objet de contexte d’accès toohello et sont censées toobe utilisé en tant que calcul seule JavaScript. Par conséquent, l’UDF peuvent être exécuté sur les réplicas secondaires de hello Cosmos DB service.  

Hello exemple suivant crée un fichier UDF toocalculate impôt basée sur les taux de différents supports de revenu et utilise alors à l’intérieur d’une requête toofind toutes les personnes qui les taxes payant plus de 20 000 $.

    var taxUdf = {
        id: "tax",
        serverScript: function tax(income) {

            if(income == undefined) 
                throw 'no input';

            if (income < 1000) 
                return income * 0.1;
            else if (income < 10000) 
                return income * 0.2;
            else
                return income * 0.4;
        }
    }


Hello UDF peut ensuite être utilisé dans les requêtes comme Bonjour suivant l’exemple :

    // register UDF
    client.createUserDefinedFunctionAsync('dbs/testdb/colls/testColl', taxUdf)
        .then(function(response) { 
            console.log("Created", response.resource);

            var query = 'SELECT * FROM TaxPayers t WHERE udf.tax(t.income) > 20000'; 
            return client.queryDocuments('dbs/testdb/colls/testColl',
                   query).toArrayAsync();
        }, function(error) {
            console.log("Error" , error);
        })
    .then(function(response) {
        var documents = response.feed;
        console.log(response.resource); 
    }, function(error) {
        console.log("Error" , error);
    });

## <a name="javascript-language-integrated-query-api"></a>API de requête intégrée au langage JavaScript
En outre tooissuing les requêtes à l’aide de la grammaire SQL de DocumentDB, hello Kit de développement logiciel côté serveur vous permet de requêtes tooperform optimisé à l’aide d’une interface JavaScript fluent sans aucune connaissance de SQL. requête de JavaScript Hello QU'API vous permet de requêtes de build tooprogrammatically en passant des fonctions de prédicat dans une fonction enchaînée appelle, avec un tooECMAScript5 familiers syntaxe intégrés du tableau et les bibliothèques JavaScript comme lodash. Les requêtes sont analysées par hello JavaScript runtime toobe exécutée efficacement les indices de DB Azure Cosmos.

> [!NOTE]
> `__`(trait de soulignement double) est un alias trop`getContext().getCollection()`.
> <br/>
> En d’autres termes, vous pouvez utiliser `__` ou `getContext().getCollection()` tooaccess hello API de requête de JavaScript.
> 
> 

Les fonctions prises en charge sont les suivantes :

<ul>
<li>
<b>chain() ... .value([callback] [, options])</b>
<ul>
<li>
Commence un appel chaîné qui doit se terminer par value().
</li>
</ul>
</li>
<li>
<b>filter(predicateFunction [, options] [, callback])</b>
<ul>
<li>
Filtre hello d’entrée à l’aide d’une fonction de prédicat qui retourne la valeur true/false dans l’ordre toofilter documents d’entrée/sortie dans le jeu résultant de hello. Ce comportement similaire tooa clause WHERE dans SQL.
</li>
</ul>
</li>
<li>
<b>map(transformationFunction [, options] [, callback])</b>
<ul>
<li>
Applique une projection d’une fonction de transformation qui mappe chaque élément d’entrée tooa JavaScript objet ou une valeur. Cela a un comportement similaire clause SELECT tooa dans SQL.
</li>
</ul>
</li>
<li>
<b>pluck([propertyName] [, options] [, callback])</b>
<ul>
<li>
Il s’agit d’un raccourci pour une carte qui extrait la valeur hello d’une propriété unique de chaque élément d’entrée.
</li>
</ul>
</li>
<li>
<b>flatten([isShallow] [, options] [, callback])</b>
<ul>
<li>
Combine et aplatissement des tableaux à partir de chaque élément d’entrée dans un tableau à une seule tooa. Le système de comporte tooSelectMany similaires dans LINQ.
</li>
</ul>
</li>
<li>
<b>sortBy([predicate] [, options] [, callback])</b>
<ul>
<li>
Générer un nouvel ensemble de documents en triant les documents hello dans le flux de document d’entrée hello croissant à l’aide de hello fonction de prédicat. Cela a un comportement similaire tooa clause ORDER BY dans SQL.
</li>
</ul>
</li>
<li>
<b>sortByDescending([predicate] [, options] [, callback])</b>
<ul>
<li>
Générer un nouvel ensemble de documents en triant les documents hello dans le flux de document d’entrée hello décroissant à l’aide de hello fonction de prédicat. Cela a un comportement similaire clause ORDER BY x DESC de tooa dans SQL.
</li>
</ul>
</li>
</ul>


Lorsque inclus dans des fonctions de prédicat ou sélecteur, hello constructions JavaScript suivantes obtenir automatiquement optimisé toorun directement sur l’index de base de données Azure Cosmos :

* Opérateurs simples : = + - * / % | ^ &amp; == != === !=== &lt; &gt; &lt;= &gt;= || &amp;&amp; &lt;&lt; &gt;&gt; &gt;&gt;&gt;! ~
* Littéraux, y compris le littéral d’objet hello : {}
* var, return

Hello construit du code JavaScript suivant n’a pas obtenir optimisée pour les index de base de données Azure Cosmos de :

* Flux de contrôle (par exemple, if, for, while)
* Appels de fonction

Pour plus d’informations, voir [JSDocs côté serveur](http://azure.github.io/azure-documentdb-js-server/).

### <a name="example-write-a-stored-procedure-using-hello-javascript-query-api"></a>Exemple : Écrire une procédure stockée à l’aide des API de requête hello JavaScript
Hello suivant l’exemple de code est un exemple d’utilisation de la hello API de requête de JavaScript dans le contexte hello d’une procédure stockée. Insère un document donné par le paramètre d’entrée, Hello procédure stockée et met à jour d’un document de métadonnées, à l’aide de hello `__.filter()` méthode, avec minSize, maxSize et totalSize en fonction de propriété de taille du document d’entrée hello.

    /**
     * Insert actual doc and update metadata doc: minSize, maxSize, totalSize based on doc.size.
     */
    function insertDocumentAndUpdateMetadata(doc) {
      // HTTP error codes sent tooour callback funciton by DocDB server.
      var ErrorCode = {
        RETRY_WITH: 449,
      }

      var isAccepted = __.createDocument(__.getSelfLink(), doc, {}, function(err, doc, options) {
        if (err) throw err;

        // Check hello doc (ignore docs with invalid/zero size and metaDoc itself) and call updateMetadata.
        if (!doc.isMetadata && doc.size > 0) {
          // Get hello meta document. We keep it in hello same collection. it's hello only doc that has .isMetadata = true.
          var result = __.filter(function(x) {
            return x.isMetadata === true
          }, function(err, feed, options) {
            if (err) throw err;

            // We assume that metadata doc was pre-created and must exist when this script is called.
            if (!feed || !feed.length) throw new Error("Failed toofind hello metadata document.");

            // hello metadata document.
            var metaDoc = feed[0];

            // Update metaDoc.minSize:
            // for 1st document use doc.Size, for all hello rest see if it's less than last min.
            if (metaDoc.minSize == 0) metaDoc.minSize = doc.size;
            else metaDoc.minSize = Math.min(metaDoc.minSize, doc.size);

            // Update metaDoc.maxSize.
            metaDoc.maxSize = Math.max(metaDoc.maxSize, doc.size);

            // Update metaDoc.totalSize.
            metaDoc.totalSize += doc.size;

            // Update/replace hello metadata document in hello store.
            var isAccepted = __.replaceDocument(metaDoc._self, metaDoc, function(err) {
              if (err) throw err;
              // Note: in case concurrent updates causes conflict with ErrorCode.RETRY_WITH, we can't read hello meta again 
              //       and update again because due tooSnapshot isolation we will read same exact version (we are in same transaction).
              //       We have tootake care of that on hello client side.
            });
            if (!isAccepted) throw new Error("replaceDocument(metaDoc) returned false.");
          });
          if (!result.isAccepted) throw new Error("filter for metaDoc returned false.");
        }
      });
      if (!isAccepted) throw new Error("createDocument(actual doc) returned false.");
    }

## <a name="sql-toojavascript-cheat-sheet"></a>Aide-mémoire de tooJavascript SQL
Hello tableau suivant présente les différentes requêtes SQL et les requêtes de JavaScript correspondantes hello.

Comme pour les requêtes SQL, les clés de propriété de document (par exemple, `doc.id`) respectent la casse.

|SQL| API de requête JavaScript|Description ci-dessous|
|---|---|---|
|SELECT *<br>FROM docs| __.map(function(doc) { <br>&nbsp;&nbsp;&nbsp;&nbsp;return doc;<br>});|1|
|SELECT docs.id, docs.message AS msg, docs.actions <br>FROM docs|__.map(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;return {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;id: doc.id,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;msg: doc.message,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;actions:doc.actions<br>&nbsp;&nbsp;&nbsp;&nbsp;};<br>});|2|
|SELECT *<br>FROM docs<br>WHERE docs.id="X998_Y998"|__.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;return doc.id ==="X998_Y998";<br>});|3|
|SELECT *<br>FROM docs<br>WHERE ARRAY_CONTAINS(docs.Tags, 123)|__.filter(function(x) {<br>&nbsp;&nbsp;&nbsp;&nbsp;return x.Tags &amp;&amp; x.Tags.indexOf(123) &gt; -1;<br>});|4|
|SELECT docs.id, docs.message AS msg<br>FROM docs<br>WHERE docs.id="X998_Y998"|__.chain()<br>&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;return doc.id ==="X998_Y998";<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.map(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;return {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;id: doc.id,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;msg: doc.message<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;};<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>.value();|5|
|SELECT VALUE tag<br>FROM docs<br>JOIN tag IN docs.Tags<br>ORDER BY docs._ts|__.chain()<br>&nbsp;&nbsp;&nbsp;&nbsp;.filter(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;return doc.Tags &amp;&amp; Array.isArray(doc.Tags);<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.sortBy(function(doc) {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  &nbsp;return doc._ts;<br>&nbsp;&nbsp;&nbsp;&nbsp;})<br>&nbsp;&nbsp;&nbsp;&nbsp;.pluck("Tags")<br>&nbsp;&nbsp;&nbsp;&nbsp;.flatten()<br>&nbsp;&nbsp;&nbsp;&nbsp;.value()|6|

Hello descriptions suivantes expliquent chaque requête de table hello ci-dessus.
1. Renvoie tous les documents (paginés avec jeton de continuation) tels quels.
2. Projets hello id, le message (alias toomsg) et l’action à partir de tous les documents.
3. Requêtes pour les documents avec le prédicat de hello : id = « X998_Y998 ».
4. Requêtes pour les documents qui ont une propriété de balises et de balises est un tableau qui contient la valeur de hello 123.
5. Requêtes pour les documents avec un prédicat, id = « X998_Y998 » et l’id de hello puis projets et de message (alias toomsg).
6. Les filtres pour les documents qui ont une propriété de tableau, les balises, et trie les documents qui en résultent hello par la propriété du système hello _ts timestamp et projette ensuite + aplatit le tableau de balises hello.


## <a name="runtime-support"></a>Prise en charge du runtime
[API du côté serveur JavaScript pour DocumentDB](http://azure.github.io/azure-documentdb-js-server/) hello prend en charge la plupart des hello grand public des fonctionnalités de langage JavaScript standard par [ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm).

### <a name="security"></a>Sécurité
JavaScript des procédures stockées et déclencheurs sont sandbox afin que les effets de hello d’un script ne pas renvoyer les toohello autres sans passer par le biais d’isolation des transactions hello instantané au niveau de base de données hello. environnements d’exécution Hello regroupées sont nettoyés du contexte de hello après chaque exécution. Par conséquent, elles sont garanties toobe sans échec de toutes les effets secondaires involontaires entre eux.

### <a name="pre-compilation"></a>Précompilation
Les procédures stockées, déclencheurs et des UDF sont format du code précompilé implicitement toohello octets dans le coût de compilation de commande tooavoid lors de chaque appel du script hello. Cela permet de s'assurer que les appels de procédures stockées sont rapides et présentent un encombrement réduit.

## <a name="client-sdk-support"></a>Prise en charge du kit SDK client
En outre toohello API DocumentDB pour [Node.js](documentdb-sdk-node.md) client, la base de données Azure Cosmos a [.NET](documentdb-sdk-dotnet.md), [.NET Core](documentdb-sdk-dotnet-core.md), [Java](documentdb-sdk-java.md), [ JavaScript](http://azure.github.io/azure-documentdb-js/), et [kits de développement logiciel Python](documentdb-sdk-python.md) pour hello API DocumentDB. Les procédures stockées, les déclencheurs et les fonctions définies par l'utilisateur peuvent être créés et exécutés au moyen de l'un de ces kits SDK également. Hello suivant montre l’exemple de comment toocreate et exécuter une procédure stockée à l’aide du client de .NET hello. Notez comment hello .NET sont passés dans hello procédure stockée au format JSON et lire.

    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    

                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }

                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };

    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;

    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "sproc"), document, 1920);


Cet exemple montre comment toouse hello [DocumentDB .NET API](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) toocreate un déclencheur préalable et créer un document avec déclencheur hello activé. 

    Trigger preTrigger = new Trigger()
    {
        Id = "CapitalizeName",
        Body = @"function() {
            var item = getContext().getRequest().getBody();
            item.id = item.id.toUpperCase();
            getContext().getRequest().setBody(item);
        }",
        TriggerOperation = TriggerOperation.Create,
        TriggerType = TriggerType.Pre
    };

    Document createdItem = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), new Document { Id = "documentdb" },
        new RequestOptions
        {
            PreTriggerInclude = new List<string> { "CapitalizeName" },
        });


Et hello l’exemple suivant montre comment toocreate un utilisateur défini (fonction) (UDF) et l’utiliser dans un [requête DocumentDB API SQL](documentdb-sql-query.md).

    UserDefinedFunction function = new UserDefinedFunction()
    {
        Id = "LOWER",
        Body = @"function(input) 
        {
            return input.toLowerCase();
        }"
    };

    foreach (Book book in client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        "SELECT * FROM Books b WHERE udf.LOWER(b.Title) = 'war and peace'"))
    {
        Console.WriteLine("Read {0} from query", book);
    }

## <a name="rest-api"></a>API REST
Toutes les opérations Azure Cosmos DB peuvent être effectuées sur la base de l’architecture REST. Les procédures stockées, les déclencheurs et les fonctions définies par l'utilisateur peuvent être enregistrés dans une collection au moyen de HTTP POST. Hello Voici un exemple d’une procédure stockée de tooregister :

    POST https://<url>/sprocs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT


    var x = {
      "name": "createAndAddProperty",
      "body": function (docToCreate, addedPropertyName, addedPropertyValue) {
                var collectionManager = getContext().getCollection();
                collectionManager.createDocument(
                    collectionManager.getSelfLink(),
                    docToCreate,
                    function(err, docCreated) {
                      if(err) throw new Error('Error:  ' + err.message);
                      docCreated[addedPropertyName] = addedPropertyValue;
                      getContext().getResponse().setBody(docCreated);
                    });
            }
    }


Hello procédure stockée est enregistrée en exécutant une demande POST sur hello URI dbs/testdb/colls/testColl/procédures stockées contenant hello corps hello toocreate de procédure stockée. Les déclencheurs et les fonctions définies par l'utilisateur peuvent être inscrits de la même façon en émettant une demande POST sur /triggers et /udfs respectivement.
Cette procédure stockée peut ensuite être exécutée en émettant une demande POST sur son lien de ressource :

    POST https://<url>/sprocs/<sproc> HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:20 GMT


    [ { "name": "TestDocument", "book": "Autumn of hello Patriarch"}, "Price", 200 ]


Ici, la procédure stockée de toohello d’entrée de hello est passé dans le corps de la demande hello. Notez que l’entrée de hello est passée comme un tableau JSON des paramètres d’entrée. Hello stockées procédure prend hello la première entrée sous la forme d’un document qui est un corps de réponse. réponse Hello que nous de réception est la suivante :

    HTTP/1.1 200 OK

    { 
      name: 'TestDocument',
      book: ‘Autumn of hello Patriarch’,
      id: ‘V7tQANV3rAkDAAAAAAAAAA==‘,
      ts: 1407830727,
      self: ‘dbs/V7tQAA==/colls/V7tQANV3rAk=/docs/V7tQANV3rAkDAAAAAAAAAA==/’,
      etag: ‘6c006596-0000-0000-0000-53e9cac70000’,
      attachments: ‘attachments/’,
      Price: 200
    }


Contrairement aux procédures stockées, les déclencheurs ne peuvent pas être exécutés directement. À la place, ils sont exécutés au sein d'une opération dans un document. Nous pouvons spécifier hello déclencheurs toorun avec une demande à l’aide d’en-têtes HTTP. Hello Voici demande toocreate un document.

    POST https://<url>/docs/ HTTP/1.1
    authorization: <<auth>>
    x-ms-date: Thu, 07 Aug 2014 03:43:10 GMT
    x-ms-documentdb-pre-trigger-include: validateDocumentContents 
    x-ms-documentdb-post-trigger-include: bookCreationPostTrigger


    {
       "name": "newDocument",
       “title”: “hello Wizard of Oz”,
       “author”: “Frank Baum”,
       “pages”: 92
    }


Ici, toobe de déclencheur préliminaire hello exécuter avec la demande de hello est spécifié dans l’en-tête de x-ms-documentdb-pre-trigger-include de hello. En conséquence, tous les déclencheurs après figurent dans l’en-tête de x-ms-documentdb-post-trigger-include hello. Notez que les pré- et post-déclencheurs peuvent tous deux être spécifiés pour une demande donnée.

## <a name="sample-code"></a>Exemple de code
Vous trouverez d’autres exemples de code côté serveur (notamment [bulk-delete](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/bulkDelete.js) et [update](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples/stored-procedures/update.js)) dans notre [référentiel GitHub](https://github.com/Azure/azure-documentdb-js-server/tree/master/samples).

Vous souhaitez tooshare votre procédure stockée impressionnant ? Envoyez-nous une requête d’extraction ! 

## <a name="next-steps"></a>Étapes suivantes
Une fois que vous avez une ou plusieurs procédures stockées, déclencheurs et fonctions définies par l’utilisateur créées, vous pouvez les charger et les afficher dans hello portail Azure à l’aide de l’Explorateur de données.

Vous pouvez également trouver des éléments suivants de hello références et ressources utiles dans votre chemin d’accès toolearn plus en détail la programmation côté serveur de base de données Azure Cosmos :

* [Kits SDK Azure Cosmos DB](documentdb-sdk-dotnet.md)
* [Studio DocumentDB](https://github.com/mingaliu/DocumentDBStudio/releases)
* [JSON](http://www.json.org/) 
* [JavaScript ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
* [Extensibilité de la base de données sécurisée et portable](http://dl.acm.org/citation.cfm?id=276339) 
* [Architecture de base de données orientée services](http://dl.acm.org/citation.cfm?id=1066267&coll=Portal&dl=GUIDE) 
* [Hébergement hello Runtime .NET dans Microsoft SQL server](http://dl.acm.org/citation.cfm?id=1007669)

