---
titre : aaa « didacticiel : créer votre premier index Azure Search dans le portail de hello | Description de Microsoft Docs » : Bonjour portail Azure, utilisez prédéfinies toogenerate de données exemple un index. Explorez la recherche en texte intégral, les filtres, les facettes, la recherche partielle, la recherche géographique, et bien davantage.
Services : rechercher documentationcenter : '' auteur : HeidiSteen manager : jhubbard éditeur : '' balises : portail d’azure

MS.AssetId : 21adc351-69bb-4a39-bc59-598c60c8f958 ms.service : recherche ms.devlang : na ms.workload : recherche ms.topic : hero-article ms.tgt_pltfrm : na ms.date : 26/06/2017 ms.author : heidist

---
# <a name="tutorial-create-your-first-azure-search-index-in-hello-portal"></a>Didacticiel : Créer votre premier index Azure Search dans le portail de hello

Bonjour portail Azure, démarrer avec un tooquickly de jeu de données exemple prédéfinis générer un index à l’aide de hello **importer des données** Assistant. Explorez la recherche en texte intégral, les filtres, les facettes, la recherche partielle et la recherche géographique avec **l’Explorateur de recherche**.  

Cette présentation dénuée de code est destinée à vous familiariser avec les données prédéfinies pour vous permettre d’écrire immédiatement des requêtes intéressantes. Bien que les outils du portail ne puissent pas se substituer au code, ils se révèlent utiles pour les tâches suivantes :

+ Acquisition d’une expérience pratique en un minimum de temps
+ Création d’un prototype d’index avant l’écriture du code dans l’Assistant **Importer des données**
+ Test des requêtes et de la syntaxe de l’analyseur dans **l’Explorateur de recherche**
+ Afficher un existant tooyour publié le service d’indexation et de rechercher des ses attributs.

**Durée estimée :** 15 minutes environ, mais davantage de temps si une inscription à un compte ou à un service est également requise. 

Vous pouvez également prendre à l’aide un [basée sur le code de présentation tooprogramming Azure Search dans .NET](search-howto-dotnet-sdk.md).

## <a name="prerequisites"></a>Composants requis

Ce didacticiel repose sur le principe que vous disposez [d’un abonnement Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) et du [service Recherche Azure](search-create-service-portal.md). 

Si vous ne souhaitez pas immédiatement tooprovision un service, vous pouvez regarder une démonstration de 6 minutes de hello les étapes de ce didacticiel, commençant au environ trois minutes en cela [vidéo de présentation de la recherche Azure](https://channel9.msdn.com/Events/Connect/2016/138).

## <a name="find-your-service"></a>Recherche de votre service
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Ouvrez le tableau de bord du service de hello de votre service Azure Search. Si vous n’avez pas épingler du tableau de bord hello service vignette tooyour, vous pouvez trouver votre service de cette façon : 
   
   * Bonjour Jumpbar, cliquez sur **davantage de services** bas hello hello gauche du volet de navigation.
   * Dans la zone de recherche de hello, tapez *recherche* tooget une liste de recherche des services pour votre abonnement. Votre service doit apparaître dans la liste de hello. 

## <a name="check-for-space"></a>Vérifier l’espace disponible
De nombreux clients démarrent avec le service gratuit de hello. Cette version est limitée toothree index, trois sources de données et trois indexeurs. Avant de commencer, assurez-vous de disposer d’assez d’espace pour stocker des éléments supplémentaires. Ce didacticiel crée une occurrence de chaque objet. 

> [!TIP] 
> Vignettes de tableau de bord de service hello affichent le nombre des index, indexeurs et sources de données déjà. vignette d’indexeur Hello affiche les indicateurs de réussite et d’échec. Cliquez sur hello vignette tooview hello indexeur count. 
>
> ![Vignettes Indexeurs et Sources de données][1]
>

## <a name="create-index"></a> Créer un index et charger des données
Les requêtes de recherche se répètent sur un *index* contenant les données de recherche, les métadonnées et les constructions utilisées pour l’optimisation de certains comportements de recherche.

tookeep cette tâche est basée sur le portail, nous utilisons un jeu de données exemple intégré qui peut être analysé à l’aide d’un indexeur via hello **importer des données** Assistant. 

#### <a name="step-1-start-hello-import-data-wizard"></a>Étape 1 : Démarrer l’Assistant Importation de données hello
1. Dans votre tableau de bord de service Azure Search, cliquez sur **importer des données** dans toostart de barre de commandes hello un Assistant qui crée et remplit un index.
   
    ![Commande Importer des données][2]

2. Dans l’Assistant de hello, cliquez sur **Source de données** > **exemples** > **realestate-us-sample**. Cette source de données est préconfigurée avec un nom, un type et des informations de connexion. Une fois créée, elle devient une « source de données existante » qui peut être réutilisée dans d’autres opérations d’importation.

    ![Sélection d’un exemple de jeu de données][9]

3. Cliquez sur **OK** toouse il.

#### <a name="step-2-define-hello-index"></a>Étape 2 : Définir des index de hello
Création d’un index est généralement manuelle et basée sur le code, mais les Assistant hello peuvent générer un index pour n’importe quelle source de données qu’il peut analyser. Au minimum, un index requiert un nom et une collection de champs, avec un champ marqué comme hello toouniquely clé de document identifier chaque document.

Les champs comportent des types de données et des attributs. cases à cocher Hello haut hello sont *attributs d’index* contrôle de l’utilisation du champ de hello. 

* **Récupérable** signifie que le champ s’affiche dans la liste des résultats de recherche. En décochant cette case, vous pouvez marquer des champs individuels comme hors limites pour les résultats de recherche, par exemple lorsqu’un champ est utilisé uniquement dans les expressions de filtre. 
* Les options **Filtrable**, **Triable** et **À choix multiples** déterminent si le champ peut être utilisé dans un filtre, un tri ou une structure de navigation à facettes. 
* **Possibilité de recherche** signifie que le champ est inclus dans la recherche en texte intégral. Les chaînes sont utilisables dans une recherche. Les champs numériques et booléens sont souvent marqués comme ne pouvant pas faire l’objet d’une recherche. 

Par défaut, Assistant de hello analyse source de données hello pour les identificateurs uniques en tant que base hello du champ de clé hello. Les chaînes sont dotées d’attributs les définissant comme récupérables et utilisables dans une recherche. Les entiers présentent des attributs les définissant comme récupérables, filtrables, triables et à choix multiples.

  ![Index généré pour la source realestate][3]

Cliquez sur **OK** index de hello toocreate.

#### <a name="step-3-define-hello-indexer"></a>Étape 3 : Définir l’indexeur de hello
Toujours en hello **importer des données** Assistant, cliquez sur **indexeur** > **nom**, puis tapez un nom pour l’indexeur de hello. 

Cet objet définit un processus exécutable. Vous pouvez placer il sur une planification périodique, mais pour indexeur du toorun hello option maintenant utiliser hello par défaut une fois, immédiatement, lorsque vous cliquez sur **OK**.  

  ![Indexeur de la source realestate][8]

## <a name="check-progress"></a>Vérification de la progression
toomonitor importer revenir en arrière toohello tableau de bord de service, faites défiler la liste et double-cliquez sur hello **indexeurs** liste des indexeurs mosaïques tooopen hello. Vous devez voir indexeur hello nouvellement créé dans la liste hello, avec l’état indiquant « en cours » ou en cas de réussite, en même temps que le nombre de hello de documents indexés.

   ![Message de progression de l’indexeur][4]

## <a name="query-index"></a>Index de requête hello
Vous disposez maintenant d’un index de recherche est tooquery prêt. **Rechercher dans l’Explorateur** est un outil de requête construit dans le portail de hello. Il comporte une zone de recherche qui vous permet de vérifier si les résultats de la recherche répondent à vos attentes. 

> [!TIP]
> Bonjour [vidéo de présentation de la recherche Azure](https://channel9.msdn.com/Events/Connect/2016/138), hello suivant étapes est illustrée à 6m08s dans la vidéo de hello.
>

1. Cliquez sur **rechercher dans l’Explorateur** sur la barre de commandes hello.

   ![Commande Explorateur de recherche][5]

2. Cliquez sur **index de modification** sur hello barre de commandes tooswitch trop*realestate-us-sample*.

   ![Commandes d’index et d’API][6]

3. Cliquez sur **version de l’API Set** sur toosee de barre de commandes hello qui reste API sont disponibles. Afficher un aperçu des API vous donnent qu'accès fonctionnalités toonew pas encore généralement publiées. Pour les requêtes de hello ci-dessous, utilisez version généralement disponible de hello (01-09-2016), sauf sur indication. 

    > [!NOTE]
    > [API REST de Azure Search](https://docs.microsoft.com/rest/api/searchservice/search-documents) et hello [bibliothèque .NET](search-howto-dotnet-sdk.md#core-scenarios) entièrement équivalentes, mais **rechercher dans l’Explorateur** est toohandle équipés uniquement les appels REST. Elle accepte la syntaxe pour les deux [syntaxe de requête simple](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) et [complète l’Analyseur de requêtes Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), ainsi que tous les hello des paramètres de recherche disponibles dans [recherche dans le Document](https://docs.microsoft.com/rest/api/searchservice/search-documents) operations.
    > 

4. Dans la barre de recherche de hello, entrez les chaînes de requête hello ci-dessous et cliquez sur **recherche**.

  ![Exemple de requête de recherche][7]

**`search=seattle`**

+ Hello `search` paramètre est utilisé tooinput une recherche par mot clé pour la recherche en texte intégral, dans ce cas, retournant des listes de l’état de ROI County, Washington, contenant *Seattle* dans n’importe quel champ de recherche dans le document de hello. 

+ **Rechercher dans l’Explorateur** retourne des résultats au format JSON, qui est tooread verbose et difficile si les documents ont une structure dense. En fonction de vos documents, vous devrez peut-être code toowrite rechercher des éléments importants de résultats tooextract qui handles. 

+ Les documents sont composées de tous les champs marqués comme récupérables dans les index hello. Cliquez sur les attributs d’index tooview dans le portail hello, *realestate-us-sample* Bonjour **index** vignette.

**`search=seattle&$count=true&$top=100`**

+ Hello `&` symbole est utilisé tooappend des paramètres, qui peuvent être spécifiées dans n’importe quel ordre. 

+  Hello `$count=true` paramètre retourne le nombre de somme hello de tous les documents renvoyés. Vous pouvez vérifier les requêtes de filtre en surveillant les modifications signalées par `$count=true`. 

+ Hello `$top=100` hello retourne la plus élevée classés 100 documents hors hello total. Par défaut, Azure Search retourne hello 50 premières meilleures correspondances. Vous pouvez augmenter ou diminuer la quantité hello via `$top`.

**`search=*&facet=city&$top=2`**

+ `search=*` est une recherche vide. Les recherches vides portent sur tous les éléments. Une des raisons pour soumettre une requête vide est trop filtrer ou facette sur l’ensemble complet de hello de documents. Par exemple, vous souhaitez un tooconsist de structure de navigation des facettes de toutes les villes dans les index hello.

+  `facet`Retourne une navigation de la structure que vous pouvez passer le contrôle d’interface utilisateur tooa. Il renvoie des catégories ainsi qu’un nombre. Dans ce cas, les catégories sont basées sur le nombre de hello des villes. Le service Recherche Azure ne propose aucune fonction d’agrégation, mais vous pouvez bénéficier d’une fonction quasiment comparable par le biais du paramètre `facet`, qui renvoie un nombre de documents dans chaque catégorie.

+ `$top=2`Rétablit les deux documents, qui illustre que vous pouvez utiliser `top` tooboth réduire ou augmenter les résultats.

**`search=seattle&facet=beds`**

+ Cette requête définit une facette correspondant au nombre de chambres dans une recherche de texte portant sur *Seattle*. `"beds"`peut être spécifiée comme une facette, car le champ de hello est marqué comme récupérables, filtrable et facetable dans l’index de hello et hello de valeurs contient (numérique, 1 à 5), conviennent pour le classement des annonces en groupes (annonces avec 3 chambres, 4 chambres). 

+ Seuls les champs filtrables peuvent être désignés comme étant à facettes. Seuls les champs récupérables peuvent être retournées dans les résultats de hello.

**`search=seattle&$filter=beds gt 3`**

+ Hello `filter` paramètre renvoie les résultats correspondant aux critères de hello vous avez fourni. Dans ce cas précis, la recherche renvoie les entrées présentant un nombre de chambres supérieur à 3. 

+ La syntaxe de filtre est une construction OData. Pour plus d’informations, consultez l’article [Filter OData syntax](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) (Syntaxe d’expression de filtre OData).

**`search=granite countertops&highlight=description`**

+ Mise en surbrillance fait référence tooformatting sur du texte correspondant mot clé hello, étant donné les correspondances se trouvent dans un champ spécifique. Si votre terme de recherche est profondément enfouie dans une description, vous pouvez ajouter d’atteinte toomake mise en surbrillance il toospot plus facile. Dans ce cas, hello mis en forme une expression `"granite countertops"` est plus facile toosee dans le champ de description hello.

**`search=mice&highlight=description`**

+ La recherche en texte intégral recherche les formes d’un mot qui présentent une sémantique similaire. Dans ce cas, les résultats de recherche contiennent un texte mis en surbrillance pour « mouse » pour les particuliers qui ont infestation de la souris, dans la recherche par mot clé réponse tooa sur « souris ». Formes différentes du même mot peut apparaître dans les résultats en raison d’une analyse linguistique de hello. 

+ Le service Recherche Azure prend en charge 56 analyseurs Lucene et Microsoft. Hello utilisée par défaut Azure Search est un analyseur Lucene standard de hello. 

**`search=samamish`**

+ Les mots mal orthographiés, comme 'samamish' pour le plateau de Samammish hello Bonjour région de Seattle, échouent tooreturn des correspondances de recherche classique. toohandle les fautes d’orthographe, vous pouvez utiliser une recherche floue, décrite dans l’exemple suivant de hello.

**`search=samamish~&queryType=full`**

+ La recherche floue est activée lorsque vous spécifiez hello `~` de symboles et d’utiliser l’Analyseur de requête complète hello, qui interprète et analyse correctement hello `~` syntaxe. 

+ Recherche floue n’est disponible lorsque vous y consentez Analyseur de requête complète hello, qui se produit lorsque vous définissez `queryType=full`. Pour plus d’informations sur les scénarios de requête activées par l’Analyseur de requête complète hello, consultez [syntaxe de requête Lucene dans Azure Search](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search).

+ Lorsque `queryType` est n’est pas spécifié, l’Analyseur de requête simple hello par défaut est utilisé. Analyseur de requête simple Hello est plus rapide, mais si vous avez besoin de recherche floue, les expressions régulières, recherche de proximité ou autres types de requêtes avancées, vous devrez la syntaxe complète de hello. 

**`search=*&$count=true&$filter=geo.distance(location,geography'POINT(-122.121513 47.673988)') le 5`**

+ Geospatial recherche est prise en charge par le biais hello [edm. Type de données GeographyPoint](https://docs.microsoft.com/rest/api/searchservice/supported-data-types) sur un champ qui contient les coordonnées. La recherche géographique est un type de filtre, spécifié dans l’article [Filter OData syntax](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) (Syntaxe d’expression de filtre OData). 

+ exemple de requête Hello filtre tous les résultats pour les données positionnelles, où les résultats sont moins de 5 kilomètres depuis un point donné (spécifié en tant que coordonnées de latitude et longitude). En ajoutant `$count`, vous pouvez voir le nombre de résultats est retourné lorsque vous modifiez la distance hello ou coordonnées de hello. 

+ La recherche géographique est utile si votre application de recherche dispose d’une fonctionnalité « rechercher à proximité » ou qu’elle utilise la navigation dans les cartes. Toutefois, cette fonction de recherche n’est pas disponible en texte intégral. Si vous avez des besoins des utilisateurs pour la recherche sur une ville ou le pays par nom, ajouter des champs contenant des noms de ville ou de pays, dans toocoordinates d’addition.

## <a name="next-steps"></a>Étapes suivantes

+ Modifiez un des objets hello que vous venez de créer. Après une exécution de l’Assistant de hello vous pouvez revenir en arrière et afficher ou modifier les composants individuels : source de données, l’indexeur ou index. Certaines modifications, par exemple hello la modification du type de données du champ hello, ne sont pas autorisées sur les index hello, mais la plupart des propriétés et les paramètres sont modifiables.

  tooview des composants individuels, cliquez sur hello **Index**, **indexeur**, ou **des Sources de données** vignettes sur votre tableau de bord toodisplay une liste des objets existants. toolearn en savoir plus sur les modifications d’index qui ne nécessitent pas une reconstruction, consultez [Index (API REST de Azure Search) de la mise à jour](https://docs.microsoft.com/rest/api/searchservice/update-index).

+ Essayez les outils de hello et étapes avec d’autres sources de données. Hello, exemple de dataset `realestate-us-sample`, provient d’une base de données SQL Azure Azure Search peut analyser. Outre Azure SQL Database, le service Recherche Azure peut analyser et déduire un index à partir de structures de données plates de Stockage Table Azure, de Stockage Blob, de SQL Server sur une machine virtuelle Azure et d’Azure Cosmos DB. Toutes ces sources de données sont pris en charge dans l’Assistant de hello. Dans le code, vous pouvez facilement remplir un index à l’aide d’un *indexeur*.

+ Toutes les autres sources de données de non-indexeur sont pris en charge via un modèle d’émission, où votre code exécute un push de nouvelles et modifiées des ensembles de lignes dans l’index de tooyour JSON. Pour plus d’informations, consultez l’article [Add, update, or delete documents in Azure Search](https://docs.microsoft.com/rest/api/searchservice/addupdate-or-delete-documents) (Ajouter, mettre à jour ou supprimer des documents dans le service Recherche Azure).

Pour plus d’informations sur les autres fonctionnalités mentionnées dans cet article, sélectionnez les liens suivants :

* [Présentation des indexeurs](search-indexer-overview.md)
* [Créer des Index (y compris une explication détaillée des attributs d’index hello)](https://docs.microsoft.com/rest/api/searchservice/create-index)
* [Explorateur de recherche](search-explorer.md)
* [Rechercher des Documents (comprend des exemples de syntaxe de requête)](https://docs.microsoft.com/rest/api/searchservice/search-documents)


<!--Image references-->
[1]: ./media/search-get-started-portal/tiles-indexers-datasources2.png
[2]: ./media/search-get-started-portal/import-data-cmd2.png
[3]: ./media/search-get-started-portal/realestateindex2.png
[4]: ./media/search-get-started-portal/indexers-inprogress2.png
[5]: ./media/search-get-started-portal/search-explorer-cmd2.png
[6]: ./media/search-get-started-portal/search-explorer-changeindex-se2.png
[7]: ./media/search-get-started-portal/search-explorer-query2.png
[8]: ./media/search-get-started-portal/realestate-indexer2.png
[9]: ./media/search-get-started-portal/import-datasource-sample2.png