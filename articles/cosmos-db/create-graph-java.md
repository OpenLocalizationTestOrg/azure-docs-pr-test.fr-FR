---
title: "aaaCreate une base de données du graphique de base de données Azure Cosmos avec Java | Documents Microsoft"
description: "Présente une Java le code exemple, vous pouvez utiliser un graphique des données tooconnect tooand requête dans la base de données Azure Cosmos à l’aide de GREMLINE."
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/24/2017
ms.author: denlee
ms.openlocfilehash: 595c0fb108f3dbe8c83674f0c9c4b0cdd3ab4c95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-graph-database-using-java-and-hello-azure-portal"></a>Base de données Cosmos Azure : Créer une base de données de graphique à l’aide de Java et hello portail Azure

Azure Cosmos DB est le service de base de données multi-modèle de Microsoft distribué à l’échelle mondiale. Vous pouvez rapidement créer et interroger des bases de données de graphique, qui bénéficient de distribution globale de hello et des fonctionnalités de mise à l’échelle horizontale au cœur de hello de base de données Azure Cosmos document et clé/valeur. 

Ce démarrage rapide crée un graphique à l’aide de la base de données hello outils portails Azure pour la base de données Azure Cosmos. Ce démarrage rapide montre comment tooquickly créer une application de console Java à l’aide d’une base de données de graphique à l’aide de systèmes d’exploitation hello [GREMLINE Java](https://mvnrepository.com/artifact/org.apache.tinkerpop/gremlin-driver) pilote. instructions Hello dans ce démarrage rapide peuvent être suivies sur n’importe quel système d’exploitation qui est capable d’exécuter Java. Ce démarrage rapide permet familiarise avec la création et modification des ressources du graphique dans hello l’interface utilisateur ou par programme, selon ce qui est votre préférence. 

## <a name="prerequisites"></a>Composants requis

* [Java Development Kit (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * Sur Ubuntu, exécutez `apt-get install default-jdk` tooinstall hello JDK.
    * Être tooset vraiment hello JAVA_HOME variable toopoint toohello dossier d’environnement sur lequel hello JDK est installé.
* [Téléchargement](http://maven.apache.org/download.cgi) et [installation](http://maven.apache.org/install.html) d’une archive binaire [Maven](http://maven.apache.org/)
    * Sur Ubuntu, vous pouvez exécuter `apt-get install maven` tooinstall Maven.
* [Git](https://www.git-scm.com/)
    * Sur Ubuntu, vous pouvez exécuter `sudo apt-get install git` tooinstall Git.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Création d'un compte de base de données

Avant de pouvoir créer une base de données du graphique, vous devez toocreate un compte de base de données GREMLINE (graphique) avec la base de données Azure Cosmos.

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Ajout d’un graphique

Vous pouvez maintenant utiliser outil Explorateur de données de hello Bonjour toocreate portail Azure une base de données de graphique. 

1. Bonjour portail Azure, dans le menu de navigation gauche hello, cliquez sur **Explorateur de données (version préliminaire)**. 
2. Bonjour **Explorateur de données (version préliminaire)** panneau, cliquez sur **nouveau graphique**, puis renseignez page hello à l’aide de hello informations suivantes :

    ![Explorateur de données Bonjour portail Azure](./media/create-graph-java/azure-cosmosdb-data-explorer.png)

    Paramètre|Valeur suggérée|Description
    ---|---|---
    ID de base de données|sample-database|ID de Hello pour votre nouvelle base de données. Les noms de base de données doivent inclure entre 1 et 255 caractères et ne peuvent pas contenir `/ \ # ?` ni d’espace de fin.
    ID du graphique|sample-graph|ID de Hello pour votre nouveau graphique. Les noms de graphique ont hello même caractère spécifications en tant qu’ID de base de données.
    Capacité de stockage| 10 Go|Laissez la valeur par défaut de hello. Il s’agit de la capacité de stockage hello de base de données hello.
    Throughput|400 unités de requête|Laissez la valeur par défaut de hello. Vous pouvez monter le débit hello ultérieurement si vous souhaitez une latence tooreduce.
    Clé de partition|Laisser vide|Clé de partition hello pour objectif de hello de ce démarrage rapide, laissez vide.

3. Une fois le formulaire de hello est rempli, cliquez sur **OK**.

## <a name="clone-hello-sample-application"></a>Exemple d’application hello de cloner

Maintenant nous allons cloner une application graphique à partir de github, définissez la chaîne de connexion hello et exécutez-le. Vous voyez combien il est facile toowork avec des données par programme. 

1. Ouvrez une fenêtre de Terminal Server git, telles que l’interpréteur de commandes git, et `cd` répertoire de travail tooa.  

2. Exécutez hello suivant le dépôt d’exemples de commande tooclone hello. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-java-getting-started.git
    ```

## <a name="review-hello-code"></a>Réviser le code hello

Nous allons effectuer une révision rapide de ce qui se passe dans l’application hello. Ouvrez hello `Program.java` de fichiers à partir du dossier \src\GetStarted hello et recherchez ces lignes de code. 

* Hello GREMLINE `Client` est initialisé à partir de la configuration de hello dans `src/remote.yaml`.

    ```java
    cluster = Cluster.build(new File("src/remote.yaml")).create();
    ...
    client = cluster.connect();
    ```

* Une série d’étapes de GREMLINE sont exécutées à l’aide de hello `client.submit` (méthode).

    ```java
    ResultSet results = client.submit(gremlin);

    CompletableFuture<List<Result>> completableFutureResults = results.all();
    List<Result> resultList = completableFutureResults.get();

    for (Result result : resultList) {
        System.out.println(result.toString());
    }
    ```

## <a name="update-your-connection-string"></a>Mise à jour de votre chaîne de connexion

1. Fichier de src/remote.yaml hello ouvert. 

3. Renseignez vos *hôtes*, *nom d’utilisateur*, et *mot de passe* valeurs hello src/remote.yaml fichier. autres paramètres de hello Hello n’avez pas besoin de toobe modifié.

    Paramètre|Valeur suggérée|Description
    ---|---|---
    Hôtes|[***.graphs.azure.com]|Consultez ce tableau de la capture d’écran hello. Cette valeur est la valeur de l’URI de GREMLINE hello sur la page de vue d’ensemble de hello Hello portail Azure, entre crochets, suivi d’un hello : 443 / supprimé.<br><br>Cette valeur peut également être récupérée à partir de l’onglet de clés hello, à l’aide de la valeur de l’URI hello en supprimant https://, la modification de documents toographs et suppression de fin hello : 443 /.
    Nom d’utilisateur|/dbs/sample-database/colls/sample-graph|Hello ressource sous forme de hello `/dbs/<db>/colls/<coll>` où `<db>` est votre nom de base de données existant et `<coll>` est votre nom existant de la collection.
    Mot de passe|*Votre clé principale primaire*|Consultez ce tableau de la capture d’écran hello deuxième. Cette valeur est la clé primaire, que vous pouvez récupérer à partir de la page de clés hello Hello portail Azure, dans la zone de clé primaire hello. Copier la valeur hello à l’aide du bouton de copie hello sur droite hello de zone de hello.

    Pour la valeur d’hôtes hello, copiez hello **GREMLINE URI** valeur hello **vue d’ensemble** page. S’il est vide, consultez les instructions de hello dans ligne hello hôtes hello précédant la table sur la création de hello GREMLINE URI à partir du Panneau de clés hello.
![Valeur d’URI de GREMLINE hello afficher et copier sur la page de vue d’ensemble de hello Bonjour portail Azure](./media/create-graph-java/gremlin-uri.png)

    Pourquoi la valeur de mot de passe, copiez hello **clé primaire** de hello **clés** panneau : ![afficher et copier les clés de votre clé primaire Bonjour portail Azure, page](./media/create-graph-java/keys.png)

## <a name="run-hello-console-app"></a>Exécutez l’application de console hello

1. Dans la fenêtre de terminal git hello, `cd` dossier azure-cosmos-db-graph-java-getting-started de toohello.

2. Dans la fenêtre de terminal git hello, tapez `mvn package` tooinstall hello requis packages Java.

3. Dans la fenêtre de terminal git hello, exécutez `mvn exec:java -D exec.mainClass=GetStarted.Program` dans hello toostart de la fenêtre de terminal de votre application Java.

fenêtre de terminal Hello affiche les sommets hello ajoutés toohello graphique. Une fois que la fin du programme de hello basculer arrière toohello portail Azure dans votre navigateur internet. 

<a id="add-sample-data"></a>
## <a name="review-and-add-sample-data"></a>Examiner et ajouter des exemples de données

Vous pouvez maintenant revenir en arrière tooData Explorer et consultez les sommets hello ajouté toohello graphique et ajouter des points de données supplémentaires.

1. Dans l’Explorateur de données, développez hello **base de données exemple**/**exemple de graphique**, cliquez sur **graphique**, puis cliquez sur **appliquer le filtre**. 

   ![Créer des documents dans l’Explorateur de données Bonjour portail Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-expanded.png)

2. Bonjour **résultats** liste, notez hello nouveaux utilisateurs ajoutés toohello graphique. Sélectionnez **ben** et notez qu’il s’est connecté toorobin. Vous pouvez déplacer les sommets hello sur l’Explorateur graphique hello, effectuer un zoom avant et arrière et développez taille hello de surface de l’Explorateur graphique hello. 

   ![Nouvelle sommets dans graphique hello hello portail Azure dans l’Explorateur de données](./media/create-graph-java/azure-cosmosdb-graph-explorer-new.png)

3. Nous allons ajouter quelques nouveau utilisateurs toohello graphique à l’aide de hello Explorateur de données. Cliquez sur hello **nouveau sommet** graphique tooyour des données tooadd du bouton.

   ![Créer des documents dans l’Explorateur de données Bonjour portail Azure](./media/create-graph-java/azure-cosmosdb-data-explorer-new-vertex.png)

4. Entrez une étiquette de *personne* puis entrez hello suivante, clés et valeurs toocreate hello premier vertex dans le graphique de hello. Notez que vous pouvez créer des propriétés uniques pour chaque personne dans votre graphique. Clé d’identification uniquement hello est requis.

    key|value|Remarques
    ----|----|----
    id|ashley|Identificateur unique de Hello pour les vertex hello. Si vous ne spécifiez aucun id, le système en génère un pour vous.
    gender|female| 
    tech | java | 

    > [!NOTE]
    > Dans ce guide de démarrage rapide, nous créons une collection non partitionnée. Toutefois, si vous créez une collection partitionnée par spécification d’une clé de partition pendant la création de la collection hello, vous devez clé de partition tooinclude hello en tant que clé dans chaque nouveau sommet. 

5. Cliquez sur **OK**. Vous devrez peut-être tooexpand votre écran toosee **OK** sous hello écran hello.

6. Cliquez de nouveau sur **New Vertex (Nouveau vertex)** et ajoutez un nouvel utilisateur supplémentaire. Entrez une étiquette de *personne* puis entrez les éléments suivants de hello clés et valeurs :

    key|value|Remarques
    ----|----|----
    id|rakesh|Identificateur unique de Hello pour les vertex hello. Si vous ne spécifiez aucun id, le système en génère un pour vous.
    gender|male| 
    school|MIT| 

7. Cliquez sur **OK**. 

8. Cliquez sur **appliquer le filtre** avec la valeur par défaut hello `g.V()` filtre. Tous les utilisateurs de hello affichent désormais Bonjour **résultats** liste. Lorsque vous ajoutez davantage de données, vous pouvez utiliser des filtres toolimit vos résultats. Par défaut, l’Explorateur de données utilise `g.V()` tooretrieve tous les sommets dans un graphique, mais vous peuvent modifier ce tooa différents [requête graph](tutorial-query-graph.md), tel que `g.V().count()`, tooreturn un nombre de tous les sommets hello dans graph hello au format JSON.

9. À présent, nous pouvons connecter rakesh et ashley. Vérifiez **Alice** activée dans hello **résultats** liste, puis cliquez sur bouton de modification hello suivant trop**cibles** en bas à droite. Vous devrez peut-être toowiden votre hello toosee de fenêtre **propriétés** zone.

   ![Modifier la cible d’un sommet dans un graphique hello](./media/create-graph-java/azure-cosmosdb-data-explorer-edit-target.png)

10. Bonjour **cible** zone *rakesh*et Bonjour **étiquette du bord** zone *sait*, puis cliquez sur la case à cocher hello.

   ![Ajouter une connexion entre ashley et rakesh dans l’Explorateur de données](./media/create-graph-java/azure-cosmosdb-data-explorer-set-target.png)

11. Sélectionnez à présent **rakesh** à partir de la liste des résultats hello et voir qu’Alice et rakesh sont connectés. 

   ![Deux vertex connectés dans l’Explorateur de données](./media/create-graph-java/azure-cosmosdb-graph-explorer.png)

    Vous pouvez également utiliser les procédures de toocreate stockée Explorateur de données, UDF et déclencheurs tooperform ainsi la logique métier côté serveur en tant que le débit de l’échelle. Explorateur de données expose l’ensemble du hello intégrées par programmation l’accès aux données disponibles dans l’API de hello, mais il fournit des données un accès facile tooyour hello portail Azure.



## <a name="review-slas-in-hello-azure-portal"></a>Passez en revue les SLA dans hello portail Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Supprimer des ressources

Si vous n’allez toocontinue toouse cette application, supprimez toutes les ressources créées par ce démarrage rapide Bonjour portail Azure par hello comme suit : 

1. À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur nom hello de ressource hello vous avez créé. 
2. Dans la page de votre groupe de ressources, cliquez sur **supprimer**, tapez nom hello de hello ressources toodelete dans la zone de texte hello, puis cliquez sur **supprimer**.

## <a name="next-steps"></a>Étapes suivantes

Ce guide de démarrage rapide, vous avez appris comment toocreate un compte de base de données Azure Cosmos, créer un graphique à l’aide de hello Explorateur de données et exécuter une application. Vous pouvez maintenant générer des requêtes plus complexes et implémenter une logique de traversée de graphique puissante, à l’aide de Gremlin. 

> [!div class="nextstepaction"]
> [Interroger à l’aide de Gremlin](tutorial-query-graph.md)

