---
title: "didacticiel de développement d’application aaaJava à l’aide de la base de données Azure Cosmos | Documents Microsoft"
description: "Ce didacticiel de l’application web Java vous montre comment toouse hello de base de données Azure Cosmos hello API DocumentDB toostore et accéder aux données à partir d’une application Java hébergée sur des sites Web Azure."
keywords: "Développement d’applications, didacticiel de base de données, application java, didacticiel de l’application web java, documentdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: java
author: dennyglee
manager: jhubbard
editor: mimig
ms.assetid: 0867a4a2-4bf5-4898-a1f4-44e3868f8725
ms.service: cosmos-db
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 08/22/2017
ms.author: denlee
ms.openlocfilehash: e073de23beb0037ee1e37b48a69e8fe7cdc3fc1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-web-application-using-azure-cosmos-db-and-hello-documentdb-api"></a>Créer une application web de Java à l’aide de la base de données Azure Cosmos et hello API DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.JS](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Ce didacticiel de l’application web Java vous montre comment toouse hello [base de données Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) service toostore et accéder aux données à partir d’une application Java hébergée sur Azure App Service Web Apps. Dans cette rubrique, vous allez apprendre à :

* Comment toobuild une application Java Server Pages (JSP) de base dans Eclipse.
* Comment toowork avec hello Azure Cosmos DB service à l’aide de hello [Kit de développement Java Azure Cosmos DB](https://github.com/Azure/azure-documentdb-java).

Ce didacticiel d’application Java vous montre des tâches d’application de gestion des tâches toocreate sur le web qui permet de marquer, récupérer et vous toocreate comme étant exécutée, comme indiqué dans hello suivant l’image. Chacune des tâches hello dans la liste de tâches hello sont stockés sous forme de documents JSON dans la base de données Azure Cosmos.

![Application Java My ToDo List](./media/documentdb-java-application/image1.png)

> [!TIP]
> Ce didacticiel de développement d’applications part du principe que vous avez déjà utilisé Java. Si vous êtes tooJava nouveau ou hello [outils requis](#Prerequisites), nous vous recommandons de télécharger hello complète [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) projet à partir de GitHub et de la création à l’aide de [hello instructions à fin hello de ce l’article](#GetProject). Une fois que vous avez créé, vous pouvez consulter les informations de toogain d’article hello sur le code hello dans le contexte de hello du projet de hello.  
> 
> 

## <a id="Prerequisites"></a>Conditions préalables à l’exécution de ce didacticiel d’application web Java
Avant de commencer ce didacticiel de développement d’application, vous devez disposer de hello :

* Un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure](https://azure.microsoft.com/pricing/free-trial/).

    OU

    Une installation locale de hello [Azure Cosmos DB émulateur](local-emulator.md).
* [Kit de développement logiciel Java (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
* [Environnement de développement intégré (IDE) Eclipse pour développeurs Java EE.](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunasr1)
* [Un site web Azure avec un environnement d’exécution Java (Tomcat ou Jetty, par exemple) activé.](../app-service-web/web-sites-java-get-started.md)

Si vous installez ces outils pour hello première fois, coreservlets.com fournit une vue d’ensemble du processus d’installation hello dans la section de démarrage rapide de hello de leurs [didacticiel : installation TomCat7 et son utilisation avec Eclipse](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html) l’article.

## <a id="CreateDB"></a>Étape 1 : création d’un compte Azure Cosmos DB
Commençons par créer un compte Azure Cosmos DB. Si vous déjà disposez d’un compte ou si vous utilisez hello Azure Cosmos DB émulateur pour ce didacticiel, vous pouvez ignorer trop[étape 2 : créer l’application de Java JSP hello](#CreateJSP).

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

## <a id="CreateJSP"></a>Étape 2 : Créer l’application de Java JSP hello
hello toocreate application JSP :

1. Tout d'abord, nous allons commencer par la création d'un projet Java. Démarrez Eclipse, puis cliquez sur **File** (Fichier), sur **New** (Nouveau), puis sur **Dynamic Web Project** (Projet web dynamique). Si vous ne voyez pas **projet Web dynamique** répertorié sous forme de projet disponible, procédez comme hello suivant : cliquez sur **fichier**, cliquez sur **nouveau**, cliquez sur **projet**..., développez **Web**, cliquez sur **projet Web dynamique**, puis cliquez sur **suivant**.
   
    ![Développement d’applications Java JSP](./media/documentdb-java-application/image10.png)
2. Entrez un nom de projet Bonjour **nom du projet** zone et Bonjour **Runtime cible** menu déroulant, sélectionnez éventuellement une valeur (par exemple, Apache Tomcat v7.0), puis cliquez sur **Terminer**. Sélection d’un runtime cible permet de vous toorun votre projet localement par le biais d’Eclipse.
3. Dans Eclipse, dans la vue de l’Explorateur de projets hello, développez votre projet. Cliquez avec le bouton droit sur **WebContent**, cliquez sur **New (Nouveau)**, puis sur **JSP File (Fichier JSP)**.
4. Bonjour **nouveau fichier JSP** boîte de dialogue, le nom de fichier hello **index.jsp**. Conservez le dossier parent hello **WebContent**, comme indiqué dans hello après l’illustration, puis cliquez sur **suivant**.
   
    ![Création d’un fichier JSP - Didacticiel d’application web Java](./media/documentdb-java-application/image11.png)
5. Bonjour **sélectionner un modèle JSP** boîte de dialogue, à des fins de hello de ce didacticiel, sélectionnez **nouveau fichier JSP (html)**, puis cliquez sur **Terminer**.
6. Lorsque le fichier de hello index.jsp s’ouvre dans Eclipse, ajoutez le texte toodisplay **Hello World !** dans hello existant <body> élément. Votre mise à jour <body> contenu doit ressembler à hello suivant de code :
   
        <body>
            <% out.println("Hello World!"); %>
        </body>
7. Enregistrez le fichier index.jsp de hello.
8. Si vous définissez un runtime cible à l’étape 2, vous pouvez cliquer sur **projet** , puis **exécuter** toorun localement votre application JSP :
   
    ![Hello World – Didacticiel d’application Java](./media/documentdb-java-application/image12.png)

## <a id="InstallSDK"></a>Étape 3 : Installer hello DocumentDB Java SDK
Bonjour toopull de façon plus simple de hello DocumentDB Java SDK et ses dépendances est via [Apache Maven](http://maven.apache.org/).

toodo, vous devez tooconvert votre projet de maven tooa en effectuant hello comme suit :

1. Avec le bouton droit de votre projet dans l’Explorateur de projets de hello, cliquez sur **configurer**, cliquez sur **convertir tooMaven projet**.
2. Bonjour **créer nouveau POM** fenêtre, acceptez les valeurs par défaut hello et cliquez sur **Terminer**.
3. Dans **Explorateur de projets**, ouvrez fichier pom.xml de hello.
4. Sur hello **dépendances** onglet hello **dépendances** volet, cliquez sur **ajouter**.
5. Bonjour **sélectionner une dépendance** fenêtre, hello suivant :
   
   * Bonjour **Id de groupe** , entrez com.microsoft.azure.
   * Bonjour **Id d’artefact** , entrez azure documentdb.
   * Bonjour **Version** , entrez 1.5.1.
     
   ![Installation du Kit de développement logiciel (SDK) d’applications Java DocumentDB](./media/documentdb-java-application/image13.png)
     
   * Ou ajouter une dépendance de hello XML pour l’Id de groupe et l’Id d’artefact directement toohello pom.xml via un éditeur de texte :
     
        <dependency><groupId>com.microsoft.azure</groupId><artifactId>azure-documentdb</artifactId><version>1.9.1</version></dependency>
6. Cliquez sur **OK** et Maven installera hello DocumentDB Java SDK.
7. Enregistrez le fichier de pom.xml hello.

## <a id="UseService"></a>Étape 4 : À l’aide de service de base de données Azure Cosmos hello dans une application Java
1. Tout d’abord, nous allons définir objet TodoItem de hello dans TodoItem.java :
   
        @Data
        @Builder
        public class TodoItem {
            private String category;
            private boolean complete;
            private String id;
            private String name;
        }
   
    Dans ce projet, nous utilisons [Lombok du projet](http://projectlombok.org/) toogenerate hello constructeur, accesseurs Get, Set et un générateur. Ou bien, vous pouvez écrire ce code manuellement ou laisser hello IDE sa génération.
2. service de base de données Azure Cosmos tooinvoke hello, vous devez instancier un nouvel **DocumentClient**. En règle générale, il s’agit des meilleures tooreuse hello **DocumentClient** - plutôt que de construire un nouveau client pour chaque demande ultérieure. Nous pouvons réutiliser client de hello en encapsulant client hello dans un **DocumentClientFactory**. Dans DocumentClientFactory.java, vous devez vous avez enregistré le Presse-papiers tooyour dans valeur d’URI et la clé primaire de hello toopaste [étape 1](#CreateDB). Remplacez [YOUR\_ENDPOINT\_HERE] par l’URI et [YOUR\_KEY\_HERE] par votre CLÉ PRIMAIRE.
   
        private static final String HOST = "[YOUR_ENDPOINT_HERE]";
        private static final String MASTER_KEY = "[YOUR_KEY_HERE]";
   
        private static DocumentClient documentClient = new DocumentClient(HOST, MASTER_KEY,
                        ConnectionPolicy.GetDefault(), ConsistencyLevel.Session);
   
        public static DocumentClient getDocumentClient() {
            return documentClient;
        }
3. Maintenant nous allons créer un tooabstract objet d’accès aux données (DAO) conserver notre tooAzure d’éléments ToDo Cosmos DB.
   
    Commander les éléments de tâche toosave tooa collection, hello client a besoin de tooknow le toopersist collecte et de la base de données trop (référencé par Self-Link). En règle générale, il s’agit de collecte lorsque cela est possible et base de données de meilleure toocache hello toohello base de données des allers-retours supplémentaires tooavoid.
   
    Hello de code suivant illustre comment tooretrieve notre base de données et de la collection, si elle existe, ou créez-en un nouveau si elle n’existe pas :
   
        public class DocDbDao implements TodoDao {
            // hello name of our database.
            private static final String DATABASE_ID = "TodoDB";
   
            // hello name of our collection.
            private static final String COLLECTION_ID = "TodoCollection";
   
            // hello Azure Cosmos DB Client
            private static DocumentClient documentClient = DocumentClientFactory
                    .getDocumentClient();
   
            // Cache for hello database object, so we don't have tooquery for it to
            // retrieve self links.
            private static Database databaseCache;
   
            // Cache for hello collection object, so we don't have tooquery for it to
            // retrieve self links.
            private static DocumentCollection collectionCache;
   
            private Database getTodoDatabase() {
                if (databaseCache == null) {
                    // Get hello database if it exists
                    List<Database> databaseList = documentClient
                            .queryDatabases(
                                    "SELECT * FROM root r WHERE r.id='" + DATABASE_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (databaseList.size() > 0) {
                        // Cache hello database object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        databaseCache = databaseList.get(0);
                    } else {
                        // Create hello database if it doesn't exist.
                        try {
                            Database databaseDefinition = new Database();
                            databaseDefinition.setId(DATABASE_ID);
   
                            databaseCache = documentClient.createDatabase(
                                    databaseDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return databaseCache;
            }
   
            private DocumentCollection getTodoCollection() {
                if (collectionCache == null) {
                    // Get hello collection if it exists.
                    List<DocumentCollection> collectionList = documentClient
                            .queryCollections(
                                    getTodoDatabase().getSelfLink(),
                                    "SELECT * FROM root r WHERE r.id='" + COLLECTION_ID
                                            + "'", null).getQueryIterable().toList();
   
                    if (collectionList.size() > 0) {
                        // Cache hello collection object so we won't have tooquery for it
                        // later tooretrieve hello selfLink.
                        collectionCache = collectionList.get(0);
                    } else {
                        // Create hello collection if it doesn't exist.
                        try {
                            DocumentCollection collectionDefinition = new DocumentCollection();
                            collectionDefinition.setId(COLLECTION_ID);
   
                            collectionCache = documentClient.createCollection(
                                    getTodoDatabase().getSelfLink(),
                                    collectionDefinition, null).getResource();
                        } catch (DocumentClientException e) {
                            // TODO: Something has gone terribly wrong - hello app wasn't
                            // able tooquery or create hello collection.
                            // Verify your connection, endpoint, and key.
                            e.printStackTrace();
                        }
                    }
                }
   
                return collectionCache;
            }
        }
4. étape suivante de Hello est toowrite certaines hello toopersist de code TodoItems dans toohello collection. Dans cet exemple, nous allons utiliser [Gson](https://code.google.com/p/google-gson/) tooserialize et désérialiser des documents tooJSON TodoItem brut objets Java ancien (POJO).
   
        // We'll use Gson for POJO <=> JSON serialization for this example.
        private static Gson gson = new Gson();
   
        @Override
        public TodoItem createTodoItem(TodoItem todoItem) {
            // Serialize hello TodoItem as a JSON Document.
            Document todoItemDocument = new Document(gson.toJson(todoItem));
   
            // Annotate hello document as a TodoItem for retrieval (so that we can
            // store multiple entity types in hello collection).
            todoItemDocument.set("entityType", "todoItem");
   
            try {
                // Persist hello document using hello DocumentClient.
                todoItemDocument = documentClient.createDocument(
                        getTodoCollection().getSelfLink(), todoItemDocument, null,
                        false).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
5. De même que les collections et les bases de données Azure Cosmos DB, les documents sont référencés par des liens réflexifs. Hello suivant permet de fonction d’assistance que nous récupérer les documents par un autre attribut (par exemple, « id ») au lieu de l’élément Self-link :
   
        private Document getDocumentById(String id) {
            // Retrieve hello document using hello DocumentClient.
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.id='" + id + "'", null)
                    .getQueryIterable().toList();
   
            if (documentList.size() > 0) {
                return documentList.get(0);
            } else {
                return null;
            }
        }
6. Nous pouvons utiliser la méthode d’assistance de hello dans l’étape 5 tooretrieve un document TodoItem JSON par id et de le désérialiser tooa POJO :
   
        @Override
        public TodoItem readTodoItem(String id) {
            // Retrieve hello document by id using our helper method.
            Document todoItemDocument = getDocumentById(id);
   
            if (todoItemDocument != null) {
                // De-serialize hello document in tooa TodoItem.
                return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
            } else {
                return null;
            }
        }
7. Nous pouvons également utiliser hello DocumentClient tooget une collection ou une liste de TodoItems à l’aide de SQL de DocumentDB :
   
        @Override
        public List<TodoItem> readTodoItems() {
            List<TodoItem> todoItems = new ArrayList<TodoItem>();
   
            // Retrieve hello TodoItem documents
            List<Document> documentList = documentClient
                    .queryDocuments(getTodoCollection().getSelfLink(),
                            "SELECT * FROM root r WHERE r.entityType = 'todoItem'",
                            null).getQueryIterable().toList();
   
            // De-serialize hello documents in tooTodoItems.
            for (Document todoItemDocument : documentList) {
                todoItems.add(gson.fromJson(todoItemDocument.toString(),
                        TodoItem.class));
            }
   
            return todoItems;
        }
8. Il existe de nombreuses façons tooupdate un document avec hello DocumentClient. Dans notre application de liste Todo, nous souhaitons tootoggle en mesure de toobe si un objet TodoItem est terminé. Cela peut être obtenue en mettant à jour d’attribut de « terminée » hello dans le document de hello :
   
        @Override
        public TodoItem updateTodoItem(String id, boolean isComplete) {
            // Retrieve hello document from hello database
            Document todoItemDocument = getDocumentById(id);
   
            // You can update hello document as a JSON document directly.
            // For more complex operations - you could de-serialize hello document in
            // tooa POJO, update hello POJO, and then re-serialize hello POJO back in to
            // a document.
            todoItemDocument.set("complete", isComplete);
   
            try {
                // Persist/replace hello updated document.
                todoItemDocument = documentClient.replaceDocument(todoItemDocument,
                        null).getResource();
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return null;
            }
   
            return gson.fromJson(todoItemDocument.toString(), TodoItem.class);
        }
9. Enfin, nous souhaitons hello capacité toodelete un TodoItem de notre liste. toodo, nous pouvons utiliser la méthode d’assistance de hello nous a écrit précédemment tooretrieve hello Self-link et alors indiquer au hello client toodelete il :
   
        @Override
        public boolean deleteTodoItem(String id) {
            // Azure Cosmos DB refers toodocuments by self link rather than id.
   
            // Query for hello document tooretrieve hello self link.
            Document todoItemDocument = getDocumentById(id);
   
            try {
                // Delete hello document by self link.
                documentClient.deleteDocument(todoItemDocument.getSelfLink(), null);
            } catch (DocumentClientException e) {
                e.printStackTrace();
                return false;
            }
   
            return true;
        }

## <a id="Wire"></a>Étape 5 : Ensemble reste hello Hello du projet de développement d’applications Java de câblage
Maintenant que nous avons terminé fun de hello bits - tout ce qui reste est toobuild une interface utilisateur rapide et le connecter tooour DAO.

1. Tout d’abord, nous pouvons commencer à la création d’un contrôleur toocall notre DAO :
   
        public class TodoItemController {
            public static TodoItemController getInstance() {
                if (todoItemController == null) {
                    todoItemController = new TodoItemController(TodoDaoFactory.getDao());
                }
                return todoItemController;
            }
   
            private static TodoItemController todoItemController;
   
            private final TodoDao todoDao;
   
            TodoItemController(TodoDao todoDao) {
                this.todoDao = todoDao;
            }
   
            public TodoItem createTodoItem(@NonNull String name,
                    @NonNull String category, boolean isComplete) {
                TodoItem todoItem = TodoItem.builder().name(name).category(category)
                        .complete(isComplete).build();
                return todoDao.createTodoItem(todoItem);
            }
   
            public boolean deleteTodoItem(@NonNull String id) {
                return todoDao.deleteTodoItem(id);
            }
   
            public TodoItem getTodoItemById(@NonNull String id) {
                return todoDao.readTodoItem(id);
            }
   
            public List<TodoItem> getTodoItems() {
                return todoDao.readTodoItems();
            }
   
            public TodoItem updateTodoItem(@NonNull String id, boolean isComplete) {
                return todoDao.updateTodoItem(id, isComplete);
            }
        }
   
    Dans une application plus complexe, le contrôleur de hello peut héberger la logique métier complexe par-dessus hello DAO.
2. Ensuite, nous allons créer un contrôleur de servlet tooroute HTTP demandes toohello :
   
        public class TodoServlet extends HttpServlet {
            // API Keys
            public static final String API_METHOD = "method";
   
            // API Methods
            public static final String CREATE_TODO_ITEM = "createTodoItem";
            public static final String GET_TODO_ITEMS = "getTodoItems";
            public static final String UPDATE_TODO_ITEM = "updateTodoItem";
   
            // API Parameters
            public static final String TODO_ITEM_ID = "todoItemId";
            public static final String TODO_ITEM_NAME = "todoItemName";
            public static final String TODO_ITEM_CATEGORY = "todoItemCategory";
            public static final String TODO_ITEM_COMPLETE = "todoItemComplete";
   
            public static final String MESSAGE_ERROR_INVALID_METHOD = "{'error': 'Invalid method'}";
   
            private static final long serialVersionUID = 1L;
            private static final Gson gson = new Gson();
   
            @Override
            protected void doGet(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
   
                String apiResponse = MESSAGE_ERROR_INVALID_METHOD;
   
                TodoItemController todoItemController = TodoItemController
                        .getInstance();
   
                String id = request.getParameter(TODO_ITEM_ID);
                String name = request.getParameter(TODO_ITEM_NAME);
                String category = request.getParameter(TODO_ITEM_CATEGORY);
                boolean isComplete = StringUtils.equalsIgnoreCase("true",
                        request.getParameter(TODO_ITEM_COMPLETE)) ? true : false;
   
                switch (request.getParameter(API_METHOD)) {
                case CREATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.createTodoItem(name,
                            category, isComplete));
                    break;
                case GET_TODO_ITEMS:
                    apiResponse = gson.toJson(todoItemController.getTodoItems());
                    break;
                case UPDATE_TODO_ITEM:
                    apiResponse = gson.toJson(todoItemController.updateTodoItem(id,
                            isComplete));
                    break;
                default:
                    break;
                }
   
                response.getWriter().println(apiResponse);
            }
   
            @Override
            protected void doPost(HttpServletRequest request,
                    HttpServletResponse response) throws ServletException, IOException {
                doGet(request, response);
            }
        }
3. Nous avons besoin d’un utilisateur de toohello toodisplay interface web utilisateur. Nous allons réécrire hello index.jsp créée précédemment :
    ```html
        <html>
        <head>
          <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
          <meta http-equiv="X-UA-Compatible" content="IE=edge;" />
          <title>Azure Cosmos DB Java Sample</title>
   
          <!-- Bootstrap -->
          <link href="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css" rel="stylesheet">
   
          <style>
            /* Add padding toobody for fixed nav bar */
            body {
              padding-top: 50px;
            }
          </style>
        </head>
        <body>
          <!-- Nav Bar -->
          <div class="navbar navbar-inverse navbar-fixed-top" role="navigation">
            <div class="container">
              <div class="navbar-header">
                <a class="navbar-brand" href="#">My Tasks</a>
              </div>
            </div>
          </div>
   
          <!-- Body -->
          <div class="container">
            <h1>My ToDo List</h1>
   
            <hr/>
   
            <!-- hello ToDo List -->
            <div class = "todoList">
              <table class="table table-bordered table-striped" id="todoItems">
                <thead>
                  <tr>
                    <th>Name</th>
                    <th>Category</th>
                    <th>Complete</th>
                  </tr>
                </thead>
                <tbody>
                </tbody>
              </table>
   
              <!-- Update Button -->
              <div class="todoUpdatePanel">
                <form class="form-horizontal" role="form">
                  <button type="button" class="btn btn-primary">Update Tasks</button>
                </form>
              </div>
   
            </div>
   
            <hr/>
   
            <!-- Item Input Form -->
            <div class="todoForm">
              <form class="form-horizontal" role="form">
                <div class="form-group">
                  <label for="inputItemName" class="col-sm-2">Task Name</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemName" placeholder="Enter name">
                  </div>
                </div>
   
                <div class="form-group">
                  <label for="inputItemCategory" class="col-sm-2">Task Category</label>
                  <div class="col-sm-10">
                    <input type="text" class="form-control" id="inputItemCategory" placeholder="Enter category">
                  </div>
                </div>
   
                <button type="button" class="btn btn-primary">Add Task</button>
              </form>
            </div>
   
          </div>
   
          <!-- Placed at hello end of hello document so hello pages load faster -->
          <script src="//ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js"></script>
          <script src="//ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js"></script>
          <script src="assets/todo.js"></script>
        </body>
        </html>
    ```
4. Et enfin, écrire une interface utilisateur de côté client JavaScript tootie hello web et hello servlet ensemble :
   
        var todoApp = {
          /*
           * API methods toocall Java backend.
           */
          apiEndpoint: "api",
   
          createTodoItem: function(name, category, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "createTodoItem",
                "todoItemName": name,
                "todoItemCategory": category,
                "todoItemComplete": isComplete
              },
              function(data) {
                var todoItem = data;
                todoApp.addTodoItemToTable(todoItem.id, todoItem.name, todoItem.category, todoItem.complete);
              },
              "json");
          },
   
          getTodoItems: function() {
            $.post(todoApp.apiEndpoint, {
                "method": "getTodoItems"
              },
              function(data) {
                var todoItemArr = data;
                $.each(todoItemArr, function(index, value) {
                  todoApp.addTodoItemToTable(value.id, value.name, value.category, value.complete);
                });
              },
              "json");
          },
   
          updateTodoItem: function(id, isComplete) {
            $.post(todoApp.apiEndpoint, {
                "method": "updateTodoItem",
                "todoItemId": id,
                "todoItemComplete": isComplete
              },
              function(data) {},
              "json");
          },
   
          /*
           * UI Methods
           */
          addTodoItemToTable: function(id, name, category, isComplete) {
            var rowColor = isComplete ? "active" : "warning";
   
            todoApp.ui_table().append($("<tr>")
              .append($("<td>").text(name))
              .append($("<td>").text(category))
              .append($("<td>")
                .append($("<input>")
                  .attr("type", "checkbox")
                  .attr("id", id)
                  .attr("checked", isComplete)
                  .attr("class", "isComplete")
                ))
              .addClass(rowColor)
            );
          },
   
          /*
           * UI Bindings
           */
          bindCreateButton: function() {
            todoApp.ui_createButton().click(function() {
              todoApp.createTodoItem(todoApp.ui_createNameInput().val(), todoApp.ui_createCategoryInput().val(), false);
              todoApp.ui_createNameInput().val("");
              todoApp.ui_createCategoryInput().val("");
            });
          },
   
          bindUpdateButton: function() {
            todoApp.ui_updateButton().click(function() {
              // Disable button temporarily.
              var myButton = $(this);
              var originalText = myButton.text();
              $(this).text("Updating...");
              $(this).prop("disabled", true);
   
              // Call api tooupdate todo items.
              $.each(todoApp.ui_updateId(), function(index, value) {
                todoApp.updateTodoItem(value.name, value.value);
                $(value).remove();
              });
   
              // Re-enable button.
              setTimeout(function() {
                myButton.prop("disabled", false);
                myButton.text(originalText);
              }, 500);
            });
          },
   
          bindUpdateCheckboxes: function() {
            todoApp.ui_table().on("click", ".isComplete", function(event) {
              var checkboxElement = $(event.currentTarget);
              var rowElement = $(event.currentTarget).parents('tr');
              var id = checkboxElement.attr('id');
              var isComplete = checkboxElement.is(':checked');
   
              // Toggle table row color
              if (isComplete) {
                rowElement.addClass("active");
                rowElement.removeClass("warning");
              } else {
                rowElement.removeClass("active");
                rowElement.addClass("warning");
              }
   
              // Update hidden inputs for update panel.
              todoApp.ui_updateForm().children("input[name='" + id + "']").remove();
   
              todoApp.ui_updateForm().append($("<input>")
                .attr("type", "hidden")
                .attr("class", "updateComplete")
                .attr("name", id)
                .attr("value", isComplete));
   
            });
          },
   
          /*
           * UI Elements
           */
          ui_createNameInput: function() {
            return $(".todoForm #inputItemName");
          },
   
          ui_createCategoryInput: function() {
            return $(".todoForm #inputItemCategory");
          },
   
          ui_createButton: function() {
            return $(".todoForm button");
          },
   
          ui_table: function() {
            return $(".todoList table tbody");
          },
   
          ui_updateButton: function() {
            return $(".todoUpdatePanel button");
          },
   
          ui_updateForm: function() {
            return $(".todoUpdatePanel form");
          },
   
          ui_updateId: function() {
            return $(".todoUpdatePanel .updateComplete");
          },
   
          /*
           * Install hello TodoApp
           */
          install: function() {
            todoApp.bindCreateButton();
            todoApp.bindUpdateButton();
            todoApp.bindUpdateCheckboxes();
   
            todoApp.getTodoItems();
          }
        };
   
        $(document).ready(function() {
          todoApp.install();
        });
5. Génial ! Tout ce qui reste est maintenant application hello de tootest. Exécuter des application hello localement et ajouter des éléments de tâche en remplissant la catégorie et le nom de l’élément hello en cliquant sur **ajouter une tâche**.
6. Une fois que l’élément de hello s’affiche, vous pouvez mettre à jour si elle est terminée en activant la case à cocher hello en cliquant sur **mettre à jour les tâches**.

## <a id="Deploy"></a>Étape 6 : Déployer votre tooAzure d’application Java Sites Web
Les Sites Web Azure permettent de déployer facilement des applications Java en les exportant sous forme de fichiers WAR et en les chargeant par le biais du contrôle de code source (GIT, par exemple) ou par FTP.

1. tooexport votre application sous forme de fichier WAR, avec le bouton droit sur votre projet dans **Explorateur de projets**, cliquez sur **exporter**, puis cliquez sur **le fichier WAR**.
2. Bonjour **WAR exporter** fenêtre, hello suivant :
   
   * Dans la zone de projet Web hello, entrez exemple azure-documentdb-java.
   * Dans la zone de Destination hello, choisissez un fichier WAR de destination toosave hello.
   * Cliquez sur **Terminer**.
3. Maintenant que vous avez un fichier WAR dans main, vous pouvez simplement télécharger tooyour Site Web Azure **webapps** active. Pour obtenir des instructions sur le téléchargement du fichier de hello, consultez [ajouter un tooAzure d’application Java App Service Web Apps](../app-service-web/web-sites-java-add-app.md).
   
    Une fois le fichier WAR hello toohello téléchargé WebApp active, l’environnement d’exécution hello détectera que vous l’avez ajouté et chargez automatiquement.
4. tooview votre produit fini, accédez toohttp://YOUR\_SITE\_NAME.azurewebsites.net/azure-java-sample/ et commencez à ajouter vos tâches !

## <a id="GetProject"></a>Obtenir le projet de hello à partir de GitHub
Tous les exemples hello dans ce didacticiel sont inclus dans hello [todo](https://github.com/Azure-Samples/documentdb-java-todo-app) projet sur GitHub. projet de todo tooimport hello dans Eclipse, assurez-vous d’avoir les logiciels hello et les ressources répertoriées dans hello [conditions préalables](#Prerequisites) section, puis hello suivant :

1. Installez [Project Lombok](http://projectlombok.org/). Lombok est utilisé toogenerate constructeurs, accesseurs Get, SET dans le projet de hello. Une fois que vous avez téléchargé le fichier de lombok.jar hello, double-cliquez dessus tooinstall il ou installez-le à partir de la ligne de commande hello.
2. Si Eclipse est ouvert, fermez-le et redémarrez-le tooload Lombok.
3. Dans Eclipse, sur hello **fichier** menu, cliquez sur **importation**.
4. Bonjour **importation** fenêtre, cliquez sur **Git**, cliquez sur **projets à partir de Git**, puis cliquez sur **suivant**.
5. Sur hello **sélectionner une Source de référentiel** , cliquez sur **Clone URI**.
6. Sur hello **référentiel de code Source Git** écran, Bonjour **URI** zone, entrez https://github.com/Azure-Samples/java-todo-app.git, puis cliquez sur **suivant**.
7. Sur hello **sélection de la branche** écran, vérifiez que **master** est sélectionné, puis cliquez sur **suivant**.
8. Sur hello **Local de Destination** , cliquez sur **Parcourir** tooselect un dossier dans lequel les référentiel hello peuvent être copiés, puis cliquez sur **suivant**.
9. Sur hello **sélectionner un toouse de l’Assistant pour importer des projets** écran, vérifiez que **importer des projets existants** est sélectionné, puis cliquez sur **suivant**.
10. Sur hello **importation projets** écran, désélectionnez hello **DocumentDB** de projet, puis cliquez sur **Terminer**. projet de DocumentDB Hello contient hello Azure Cosmos DB Java SDK, nous allons ajouter en tant que dépendance à la place.
11. Dans **Explorateur de projets**, accédez tooazure-documentdb-java-sample\src\com.microsoft.azure.documentdb.sample.dao\DocumentClientFactory.java et remplacer des valeurs d’hôte et MASTER_KEY hello avec hello URI et une clé primaire pour votre compte de base de données Azure Cosmos, puis enregistrer le fichier hello. Pour plus d'informations, consultez l'[Étape 1. Créez un compte de base de données Azure Cosmos DB](#CreateDB).
12. Dans **Explorateur de projets**, cliquez avec le bouton droit sur hello **documentdb azure-exemple java**, cliquez sur **générer le chemin d’accès**, puis cliquez sur **configurer Build chemin d’accès**.
13. Sur hello **chemin d’accès de Build Java** de l’écran, dans le volet droit de hello, sélectionnez hello **bibliothèques** onglet, puis cliquez sur **ajouter le fichiers JAR externe**. Accédez emplacement toohello du fichier de lombok.jar hello, puis cliquez sur **ouvrir**, puis cliquez sur **OK**.
14. Hello d’utilisation étape 12 tooopen **propriétés** à nouveau, fenêtre, puis dans le volet gauche de hello cliquez sur **ciblée des Runtimes**.
15. Sur hello **ciblée des Runtimes** , cliquez sur **nouveau**, sélectionnez **Apache Tomcat v7.0**, puis cliquez sur **OK**.
16. Hello de tooopen utilisation étape 12 **propriétés** fenêtre à nouveau, puis dans le volet gauche de hello cliquez sur **facettes de projet**.
17. Sur hello **projet facettes** écran, sélectionnez **Module Web dynamique** et **Java**, puis cliquez sur **OK**.
18. Sur hello **serveurs** onglet bas hello écran hello, avec le bouton droit **Tomcat v7.0 serveur à localhost** puis cliquez sur **ajouter et supprimer des**.
19. Sur hello **ajouter et supprimer des** fenêtre, déplacer **documentdb azure-exemple java** toohello **configuré** zone, puis cliquez sur **Terminer**.
20. Bonjour **serveurs** droit **Tomcat v7.0 serveur à localhost**, puis cliquez sur **redémarrer**.
21. Dans un navigateur, accédez à toohttp://localhost:8080 / documentdb azure-exemple java / et commencer à ajouter la liste des tâches tooyour. Notez que si vous avez modifié les valeurs de port par défaut, modifiez la valeur de toohello de 8080 que vous avez sélectionné.
22. reportez-vous à votre projet de tooan les site web Azure, toodeploy [étape 6. Déployer votre application de tooAzure Sites Web](#Deploy).

[1]: media/documentdb-java-application/keys.png
