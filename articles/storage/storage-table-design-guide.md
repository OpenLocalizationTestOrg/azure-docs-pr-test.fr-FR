---
title: "Guide de conception de Table de stockage d’aaaAzure | Documents Microsoft"
description: "Concevoir des tables évolutives et performantes dans le stockage de tables Azure"
services: storage
documentationcenter: na
author: jasonnewyork
manager: tadb
editor: tysonn
ms.assetid: 8e228b0c-2998-4462-8101-9f16517393ca
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 02/28/2017
ms.author: jahogg
ms.openlocfilehash: bbac5e83fe994c1ba1408dd43367fbcfca6a2148
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-table-design-guide-designing-scalable-and-performant-tables"></a>Guide de conception de table Azure Storage : conception de tables évolutives et performantes
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

toodesign évolutive et performantes tables, vous devez considérer plusieurs facteurs tels que les performances, d’évolutivité et de coût. Si vous avez précédemment conçu des schémas pour les bases de données relationnelles, ces considérations sera tooyou familier, mais s’il existe des similarités entre le modèle de stockage de service de Table Azure hello et des modèles relationnels, sont également nombreux important différences. Ces différences conduisent généralement toovery différentes conceptions qui semblent toosomeone contre-intuitif ou de mauvaise familiariser avec les bases de données relationnelles, mais qui faites idée si vous concevez pour un magasin de clé/valeur NoSQL comme hello service Table Azure. La plupart des différences de votre conception reflète hello fait que service de Table hello applications à l’échelle de cloud conçue toosupport qui peuvent contenir des milliards d’entités (lignes dans la terminologie de base de données relationnelle) de données ou pour les jeux de données qui doit prendre en charge très élevée volumes de transactions : par conséquent, vous devez toothink différemment sur la manière dont vous stockez vos données et comprendre le fonctionne de hello service de Table. Un magasin de données NoSQL conçu peut activer tooscale de votre solution plus loin (et à moindre coût) à une solution qui utilise une base de données relationnelle. Ce guide fournit une aide relative à ces sujets.  

## <a name="about-hello-azure-table-service"></a>À propos de hello service Table Azure
Cette section présente certaines des fonctionnalités clés hello du service de Table hello qui sont particulièrement pertinentes toodesigning des performances et évolutivité. Si vous êtes tooAzure nouveau stockage et hello service de Table, lisez d’abord [Introduction tooMicrosoft Azure Storage](storage-introduction.md) et [prise en main Azure Table Storage à l’aide de .NET](storage-dotnet-how-to-use-tables.md) avant de lire le reste de hello de article. Bien que hello de ce guide porte sur hello service de Table, elle inclut une discussion de hello file d’attente Azure et les services Blob, et comment vous pouvez les utiliser en même temps que le service de Table dans une solution de hello.  

Qu’est le service de Table hello ? Comme vous pouvez vous attendre à partir du nom de hello, hello service de Table utilise un toostore de données sous forme de tableau. Dans la terminologie hello, chaque ligne de table de hello représente une entité et magasin de colonnes hello hello diverses propriétés de cette entité. Chaque entité a une paire de clés toouniquely identifier, et une colonne timestamp que hello service de Table utilise tootrack lors de la mise à jour d’entité de hello (cela se produit automatiquement et vous ne peut pas remplacer manuellement de hello timestamp avec une valeur arbitraire). Hello service de Table utilise cet horodatage de dernière modification (LMT) toomanage l’accès concurrentiel optimiste.  

> [!NOTE]
> opérations d’API REST service Hello Table retournent également un **ETag** valeur dérive d’horodatage de dernière modification de hello (LMT). Dans ce document, nous allons utiliser hello conditions ETag et LMT indifféremment car ils font référence toohello même les données sous-jacentes.  
> 
> 

Hello suivant montre un toostore de conception de table simple entités employee et department. La plupart des exemples hello figurant plus loin dans ce guide sont basées sur cette conception simple.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td>Marketing</td>
<td>00001</td>
<td>2014-08-22T00:50:32Z</td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td>Don</td>
<td>Hall</td>
<td>34</td>
<td>donh@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>Marketing</td>
<td>00002</td>
<td>2014-08-22T00:50:34Z</td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td>Jun</td>
<td>Cao</td>
<td>47</td>
<td>junc@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td>Marketing</td>
<td>Département</td>
<td>2014-08-22T00:50:30Z</td>
<td>
<table>
<tr>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>Marketing</td>
<td>153</td>
</tr>
</table>
</td>
</tr>
<tr>
<td>Sales</td>
<td>00010</td>
<td>2014-08-22T00:50:44Z</td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td>Ken</td>
<td>Kwok</td>
<td>23</td>
<td>kenk@contoso.com</td>
</tr>
</table>
</td>
</tr>
</table>


Jusqu'à présent, cela ressemble très similaire tooa table dans une base de données relationnelle avec les différences clés hello en cours hello colonnes obligatoires, et hello capacité toostore plusieurs types d’entités Bonjour même table. En outre, chacun des hello propriétés définies par l’utilisateur comme **FirstName** ou **âge** a un type de données, comme integer ou string, simplement comme une colonne dans une base de données relationnelle. Bien que, contrairement à une base de données relationnelle, nature de sans schéma hello Hello moyens de service de Table qui a une propriété n’a pas besoin hello même type de données sur chaque entité. toostore des types de données complexes dans une seule propriété, vous devez utiliser un format sérialisé comme JSON ou XML. Pour plus d’informations sur les types de données de service telles que la prise en charge de table hello, les plages de dates prise en charge, les règles d’affectation de noms et contraintes de taille, consultez [hello de présentation des modèle de données de Service de Table](http://msdn.microsoft.com/library/azure/dd179338.aspx).

Comme vous le verrez, votre choix de **PartitionKey** et **RowKey** est la conception de la table toogood fondamentaux. Toutes les entités stockées dans une table doivent avoir une combinaison unique de **PartitionKey** et **RowKey**. Comme avec les clés dans une table de base de données relationnelle, hello **PartitionKey** et **RowKey** les valeurs sont indexée toocreate un index cluster qui permet la recherche rapide ; Toutefois, hello service de Table ne crée aucun les index secondaires afin qu’ils soient hello que deux des propriétés indexées (certains schémas hello décrites plus loin montrent comment vous pouvez contourner cette limitation apparente).  

Un tableau est constitué d’une ou plusieurs partitions, et comme vous le verrez, nombreux hello vous apportez va être autour adaptée des décisions de conception **PartitionKey** et **RowKey** toooptimize votre solution. En guise de solution, vous pouvez utiliser une seule table contenant toutes vos entités organisées en partitions, mais généralement, une solution possède plusieurs tables. Tables vous aident à toologically organiser vos entités, vous aident à gérer l’accès à des données toohello à l’aide des listes de contrôle d’accès, et vous pouvez supprimer une table entière à l’aide d’une opération de stockage unique.  

### <a name="table-partitions"></a>Partitions de table
nom du compte Hello, nom de la table et **PartitionKey** ensemble identifier partition hello au sein du service de stockage hello où le service de table hello stocke les entités hello. Ainsi que faisant partie du modèle pour les entités d’adressage de hello, partitions de définissent une étendue pour les transactions (consultez [Transactions de groupe d’entités](#entity-group-transactions) ci-dessous) et écran hello de comment le service de table hello évolue. Pour plus d’informations sur les partitions, consultez [Objectifs d’évolutivité et de performances d’Azure Storage](storage-scalability-targets.md).  

Bonjour service de Table, un nœud individuel services ou plus effectuer des partitions et hello service échelles dynamiquement à l’équilibrage de charge des partitions sur les nœuds. Si un nœud est sous charge, le service de table hello peut *fractionner* plage hello de partitions traitées par ce nœud sur différents nœuds ; lors de la réduction du trafic, le service de hello peut *fusion* allant de la partition de hello nœuds silencieux sur un seul nœud.  

Pour plus d’informations sur hello détails internes de hello service de Table et notamment comment le service de hello gère les partitions, consultez les livre hello [Microsoft Azure Storage : A hautement disponible Service de stockage Cloud à forte cohérence](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).  

### <a name="entity-group-transactions"></a>Transactions de groupe d’entités
Bonjour service de Table, Transactions de groupe d’entités (EGTs) sont mécanisme intégré uniquement de hello pour effectuer des mises à jour atomiques entre plusieurs entités. EGTs sont également référencé tooas *par lots de transactions* dans certains documents. EGTs peut uniquement fonctionner sur des entités stockées dans hello même partition (partage hello même clé de partition dans une table donnée), de sorte que chaque fois que vous devez le comportement transactionnel atomique entre plusieurs entités vous devez tooensure ces entités sont Bonjour même partition. Il s’agit souvent une raison de conserver plusieurs types d’entités Bonjour même table (et de partition) et non à l’aide de plusieurs tables pour les différents types d’entité. Une seule EGT peut traiter jusqu'à 100 entités.  Si vous envoyez plusieurs EGTs simultanées pour son traitement est important tooensure ces EGTs ne fonctionnent pas sur les entités qui sont communes à EGTs comme dans le cas contraire le traitement peut être différé.

EGTs présentent également un compromis potentiel pour vous tooevaluate dans votre conception : l’utilisation de plusieurs partitions augmente l’évolutivité de hello de votre application, car Azure dispose de davantage d’occasions de requêtes sur les nœuds d’équilibrage de charge, mais cela peut limiter hello capacité de votre application tooperform atomique des transactions et maintenir la cohérence forte pour vos données. En outre, il existe des objectifs d’évolutivité spécifique au niveau de hello d’une partition qui peut limiter le débit des transactions, vous pouvez vous attendre pour un seul nœud hello : pour plus d’informations sur les objectifs d’évolutivité hello pour les comptes de stockage Azure et de la table de hello service, consultez [évolutivité du stockage Azure et les objectifs de performances](storage-scalability-targets.md). Discutez des différentes sections ultérieures de ce guide de conception des stratégies qui vous aident à gérer les compromis de telles que celle-ci et discutez de la meilleure façon toochoose votre clé de partition basés sur les conditions spécifiques de hello de votre application cliente.  

### <a name="capacity-considerations"></a>Considérations relatives à la capacité
Hello tableau suivant récapitule certaines des toobe de valeurs de clé hello connaître lorsque vous concevez une solution de service de Table :  

| Capacité totale d'un compte de stockage Azure | 500 To |
| --- | --- |
| Nombre de tables dans un compte de stockage Azure |Limité uniquement par la capacité de hello hello du compte de stockage |
| Nombre de partitions dans une table |Limité uniquement par la capacité de hello hello du compte de stockage |
| Nombre d'entités dans une partition |Limité uniquement par la capacité de hello hello du compte de stockage |
| Taille d'une entité individuelle |Configurer Mo too1 avec un maximum de 255 propriétés (y compris hello **PartitionKey**, **RowKey**, et **Timestamp**) |
| Taille de hello **PartitionKey** |Une chaîne de taille too1 Ko |
| Taille de hello **RowKey** |Une chaîne de taille too1 Ko |
| Taille d'une transaction ETG |Une transaction peut inclure au plus 100 entités et la charge utile de hello doit être inférieure à 4 Mo. Une transaction EGT ne peut mettre à jour une entité qu'une seule fois. |

Pour plus d’informations, consultez [hello de présentation des modèle de données de Service de Table](http://msdn.microsoft.com/library/azure/dd179338.aspx).  

### <a name="cost-considerations"></a>Considérations relatives au coût
Stockage de table est relativement peu coûteux, mais vous devez inclure les estimations de coût pour les deux quantité capacité hello et l’utilisation de transactions dans le cadre de votre version d’évaluation d’une solution qui utilise le service de Table hello. Toutefois, dans de nombreux scénarios, le stockage des données dénormalisées ou en double dans hello tooimprove de commande performance ou l’évolutivité de votre solution est un tootake approche valide. Pour plus d’informations sur la tarification, consultez la page [Tarification Azure Storage](https://azure.microsoft.com/pricing/details/storage/).  

## <a name="guidelines-for-table-design"></a>Conseils pour la conception de table
Ces listes résument certaines des recommandations principales de hello que vous gardez à l’esprit lorsque vous concevez vos tables, de ce guide puisse les traiter dans plus en détail plus loin dans. Ces instructions sont très différentes de recommandations hello que vous devrez généralement effectuer pour la conception de base de données relationnelle.  

Conception de votre toobe de solution de service de Table *lire* efficace :

* ***Pensez votre conception pour l’interrogation dans des applications à lecture intensive.*** Lorsque vous concevez vos tables, pensez aux requêtes hello (surtout latence de hello ceux qui sont sensibles) que vous allez exécuter avant de définir comment mettre à jour vos entités. Cela permet généralement d’élaborer une solution efficace et performante.  
* ***Spécifiez les valeurs de PartitionKey et de RowKey dans vos requêtes.*** *Point de requêtes* tel qu’il s’agit des requêtes de service de table hello plus efficaces.  
* ***Envisagez de stocker des copies dupliquées des entités.*** Stockage de table est bon marché vous devez donc le stockage hello même entité plusieurs fois (avec des clés différentes) tooenable des requêtes plus efficaces.  
* ***Envisagez de dénormaliser vos données.*** Le stockage de tables est bon marché. Nous vous recommandons donc d’envisager la dénormalisation de vos données. Par exemple, stocker les entités résumées afin que les requêtes pour les données d’agrégation doivent uniquement tooaccess une seule entité.  
* ***Utilisez des valeurs de clé composées.*** Hello uniquement les clés que vous avez sont **PartitionKey** et **RowKey**. Par exemple, utilisez tooentities de chemins d’accès composés de valeurs de clé tooenable autre accès à clé.  
* ***Utilisez la projection de requête.*** Vous pouvez réduire la quantité hello de données que vous transférez réseau hello à l’aide de requêtes qui sélectionnent uniquement les champs hello que nécessaires.  

Conception de votre toobe de solution de service de Table *écrire* efficace :  

* ***Ne créez pas de partitions à chaud.*** Choisissez les touches qui vous permettent de toospread vos demandes sur plusieurs partitions à tout moment.  
* ***Évitez les pics de trafic.*** Le trafic de hello lever un délai raisonnable et éviter des pics de trafic.
* ***Ne créez pas nécessairement une table distincte pour chaque type d’entité.*** Lorsque vous avez besoin des transactions atomiques sur les types d’entité, vous pouvez stocker ces plusieurs types d’entités dans hello même partition Bonjour même table.
* ***Considérez que vous devez obtenir un débit maximal hello.*** Vous devez être conscient des objectifs d’évolutivité hello pour hello service de Table et vous assurer que votre conception n’entraîne pas vous tooexceed les.  

En lisant ce guide, vous rencontrerez des exemples mettant ces principes en pratique.  

## <a name="design-for-querying"></a>Conception pour l'interrogation
Les solutions de service de table peuvent être lus beaucoup, beaucoup d’écriture ou une combinaison de hello deux. Cette section se concentre sur toobear de choses hello à l’esprit lorsque vous concevez votre toosupport du service de Table efficacement des opérations de lecture. En règle générale, une conception qui prend en charge les opérations de lecture de manière efficace le sera également pour des opérations d'écriture. Toutefois, il existe des considérations supplémentaires toobear à l’esprit lors de la conception toosupport opérations d’écriture, décrites dans la section suivante de hello, [conception pour la modification de données](#design-for-data-modification).

Un bon point de départ pour concevoir votre tooenable de solution de service de Table vous tooread des données efficacement sont tooask « les requêtes seront mes données hello application besoin tooexecute tooretrieve dont il a besoin de hello service de Table ? »  

> [!NOTE]
> Hello service de Table, il est important de tooget hello design correct au préalable, car il est difficile et coûteuse toochange plus tard. Par exemple, dans une base de données relationnelle, il est souvent tooaddress possibles des problèmes de performances en ajoutant simplement indexe tooan de base de données existante : il n’est pas une option avec hello service de Table.  
> 
> 

Cette section se concentre sur les problèmes clés hello que lorsque vous concevez vos tables pour les requêtes à traiter. Hello rubriques de cette section sont les suivantes :

* [Impact de votre choix de PartitionKey et RowKey sur les performances des requêtes](#how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance)
* [Choix d’une PartitionKey appropriée](#choosing-an-appropriate-partitionkey)
* [Optimisation des requêtes pour hello service de Table](#optimizing-queries-for-the-table-service)
* [Tri des données dans hello service de Table](#sorting-data-in-the-table-service)

### <a name="how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance"></a>Impact de votre choix de PartitionKey et RowKey sur les performances des requêtes
Hello exemples suivants supposent service de table hello stocke les entités employé par hello suivant structure (la plupart des exemples de hello omettre hello **Timestamp** propriété par souci de clarté) :  

| *Nom de la colonne* | *Type de données* |
| --- | --- |
| **PartitionKey** (nom du service) |String |
| **RowKey** (ID d’employé) |String |
| **FirstName** |String |
| **LastName** |String |
| **Age** |Integer |
| **EmailAddress** |String |

Hello section antérieure [vue d’ensemble du service Table Azure](#overview) décrit quelques-unes des fonctionnalités clés hello Hello service Table Azure qui ont un impact direct sur la conception de la requête. Sont ainsi hello suivant les recommandations générales pour concevoir des requêtes de service de Table. Notez que la syntaxe du filtre hello utilisé dans les exemples hello ci-dessous est à partir du service de Table hello API REST, pour plus d’informations, consultez [interroger des entités](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

* A ***requête de Point de*** toouse recherche plus efficace de hello, est recommandée toobe utilisé pour les recherches de haut volume ou de recherches nécessitant une latence la plus faible. Une telle requête peut utiliser hello index toolocate une entité individuelle très efficacement en spécifiant les deux hello **PartitionKey** et **RowKey** valeurs. Par exemple : $filter=(PartitionKey eq ’Sales’) and (RowKey eq ’2’)  
* Deuxième est un ***requête de plage*** qui utilise hello **PartitionKey** et les filtres d’une plage de **RowKey** valeurs tooreturn plusieurs entités. Hello **PartitionKey** valeur identifie une partition spécifique et hello **RowKey** valeurs identifient un sous-ensemble d’entités hello dans cette partition. Par exemple : $filter=PartitionKey eq ’Sales’ and RowKey ge ’S’ and RowKey lt ’T’  
* Troisième optimale est un ***Partition analyse*** qui utilise hello **PartitionKey** et filtres sur une autre propriété non-clé et qui peuvent retourner plusieurs entités. Hello **PartitionKey** valeur identifie une partition spécifique, et sélectionnez pour un sous-ensemble d’entités hello dans cette partition de valeurs de propriété de hello. Par exemple : $filter=PartitionKey eq ’Sales’ and LastName eq ’Smith’  
* A ***Table Scan*** n’inclut pas de hello **PartitionKey** et s’avère particulièrement inefficace parce qu’il recherche toutes les partitions hello qui composent la table à son tour pour toutes les entités correspondantes. Il effectue une analyse de table, quelle que soit ou non votre filtre utilise hello **RowKey**. Par exemple : $filter=LastName eq ’Jones’  
* Les requêtes qui retournent plusieurs entités les retournent triées dans l’ordre de la **PartitionKey** et de la **RowKey**. tooavoid avoir recours les entités hello dans le client de hello, choisissez un **RowKey** qui définit l’ordre de tri hello plus courantes.  

Notez que l’utilisation une «**ou**» toospecify un filtre basé sur **RowKey** les valeurs des résultats dans une analyse de la partition et n’est pas traité comme une requête de plage. Par conséquent, vous devez éviter les requêtes qui utilisent des filtres comme : $filter=PartitionKey eq ’Sales’ and (RowKey eq ’121’ or RowKey eq ’322’)  

Pour obtenir des exemples de code côté client qui utilisent des requêtes efficaces hello bibliothèque cliente de stockage tooexecute, consultez :  

* [Exécution d’une requête de point à l’aide de la bibliothèque cliente de stockage de hello](#executing-a-point-query-using-the-storage-client-library)
* [Récupération de plusieurs entités à l’aide de LINQ](#retrieving-multiple-entities-using-linq)
* [Projection côté serveur](#server-side-projection)  

Pour obtenir des exemples de code côté client qui peut gérer l’entité plusieurs types stockés dans hello même table, consultez :  

* [Utilisation des types d’entités hétérogènes](#working-with-heterogeneous-entity-types)  

### <a name="choosing-an-appropriate-partitionkey"></a>Choix d’une PartitionKey appropriée
Votre choix de **PartitionKey** doit équilibrer utiliser hello besoin tooenables hello EGTs (cohérence tooensure) hello exigence toodistribute vos entités sur plusieurs partitions (tooensure une solution évolutive).  

Une des extrémités, vous pouvez stocker toutes vos entités dans une seule partition, mais cela peut limiter l’évolutivité hello de votre solution et empêche le service de table hello ne soient pas en mesure de tooload-équilibrer les demandes. À hello inverse, vous pouvez stocker une entité par partition, qui est hautement évolutif et qui permet de tooload-équilibrer les demandes de hello table service, mais qui vous empêchent d’à l’aide de transactions de groupe d’entités.  

Idéale **PartitionKey** est celui qui vous permet de toouse des requêtes efficaces et qui est suffisamment partitions tooensure votre solution est évolutif. En règle générale, vous trouverez que vos entités auront une propriété appropriée qui les distribue sur des partitions suffisantes.

> [!NOTE]
> Par exemple, dans un système qui stocke des informations sur des utilisateurs ou des employés, l’ID utilisateur peut être une bonne PartitionKey. Vous pouvez avoir plusieurs entités qui utilisent un nom d’utilisateur donné en tant que clé de partition hello. Les différentes entités qui stockent des données relatives à un utilisateur sont regroupées en une seule partition et sont ainsi accessibles via des transactions de groupe d’entités, tout en étant hautement évolutives.
> 
> 

Il existe des considérations supplémentaires de votre choix de **PartitionKey** liés toohow vous insérer, mettre à jour et supprimer des entités : consultez la section de hello [conception pour la modification de données](#design-for-data-modification) ci-dessous.  

### <a name="optimizing-queries-for-hello-table-service"></a>Optimisation des requêtes pour hello service de Table
service de Table de Hello indexe automatiquement vos entités à l’aide de hello **PartitionKey** et **RowKey** valeurs dans un index cluster unique, hello donc raison que les requêtes univoques sont hello toouse plus efficace . Toutefois, il n’existe pas d’index autre que celui sur l’index ordonné en clusters hello hello **PartitionKey** et **RowKey**.

De nombreuses conceptions doivent répondre aux recherche tooenable de spécifications d’entités en fonction de plusieurs critères. Par exemple, la localisation des entités relatives aux employés (employee) en fonction de leurs adresses de messagerie électronique, de leur ID employé ou de leur nom. Hello suivants de modèles dans la section de hello [les modèles de conception de Table](#table-design-patterns) résoudre ces types de spécifications et décrivent les façons de contourner les faits hello que service de Table hello ne fournit pas d’index secondaires :  

* [Modèle d’index secondaire intra-partition](#intra-partition-secondary-index-pattern) -stocker plusieurs copies de chaque entité à l’aide de différents **RowKey** valeurs (Bonjour même partition) tooenable des recherches rapides et efficaces et tri de substitution à l’aide des commandes autre **RowKey** valeurs.  
* [Modèle de partition entre les index secondaires](#inter-partition-secondary-index-pattern) - stocker plusieurs copies de chaque entité à l’aide de différentes valeurs de RowKey dans des partitions distinctes ou dans des tables distinctes tooenable rapide et des recherches efficaces et tri de substitution des commandes à l’aide de différents **RowKey** valeurs.  
* [Modèle d’entités index](#index-entities-pattern) -conserver les index entités tooenable recherches efficaces qui retournent les listes des entités.  

### <a name="sorting-data-in-hello-table-service"></a>Tri des données dans hello service de Table
Hello service de Table retourne des entités triées dans l’ordre croissant selon **PartitionKey** puis **RowKey**. Ces clés sont des valeurs de chaîne et tooensure trier les valeurs numériques correctement, vous devez les convertir tooa fixée longueur et les remplir avec des zéros. Par exemple, si hello valeur d’id employé vous servir hello **RowKey** est une valeur entière, vous devez convertir les id d’employé **123** trop**00000123**.  

De nombreuses applications ont des exigences toouse données triées dans des ordres différents : par exemple, le tri employés par nom ou par date de jointure. Hello suivants de modèles dans la section de hello [les modèles de conception de Table](#table-design-patterns) adresse la façon dont les ordres de tri de tooalternate pour vos entités :  

* [Modèle d’index secondaire intra-partition](#intra-partition-secondary-index-pattern) -stocker plusieurs copies de chaque entité à l’aide de différentes valeurs de RowKey (Bonjour même partition) tooenable des recherches rapides et efficaces et tri de substitution des commandes à l’aide de différentes valeurs de RowKey.  
* [Modèle de partition entre les index secondaires](#inter-partition-secondary-index-pattern) - stocker plusieurs copies de chaque entité à l’aide de différentes valeurs de RowKey dans des partitions distinctes dans des tables distinctes tooenable rapide et des recherches efficaces et tri de substitution des commandes à l’aide de différents RowKey valeurs.
* [Le modèle de la fin du journal](#log-tail-pattern) -récupérer hello  *n*  entités la plus récemment ajoutée tooa partition à l’aide un **RowKey** valeur trie inverse de date et l’ordre chronologique.  

## <a name="design-for-data-modification"></a>Conception pour la modification de données
Cette section se concentre sur les considérations de conception hello pour l’optimisation des insertions, mises à jour et les supprime. Dans certains cas, vous devez tooevaluate les compromis de hello entre conceptions optimiser pour l’interrogation de conceptions optimiser pour la modification des données comme vous le feriez dans les conceptions de bases de données relationnelles (bien que les techniques de hello de gestion hello conception compromis sont différents dans une base de données relationnelle). Hello section [les modèles de conception de Table](#table-design-patterns) décrit certains modèles de conception détaillées pour hello service de Table et met en évidence certaines ces compromis. En pratique, vous constaterez que les nombreuses conceptions optimisées pour l'interrogation des entités fonctionnent aussi bien pour la modification des entités.  

### <a name="optimizing-hello-performance-of-insert-update-and-delete-operations"></a>Optimisation des performances de hello de l’instruction insert, update et delete opérations
tooupdate ou supprimer une entité, vous devez être en mesure de tooidentify à l’aide de hello **PartitionKey** et **RowKey** valeurs. À cet égard, votre choix de **PartitionKey** et **RowKey** pour la modification des entités doit suivre similaire critères tooyour choix toosupport point de requêtes, car vous souhaitez que les entités tooidentify en tant que plus efficacement possible. Vous ne souhaitez pas toouse un inefficace partition ou une table analyse toolocate une entité Bonjour de toodiscover commande **PartitionKey** et **RowKey** valeurs, vous devez tooupdate ou la supprimer.  

Hello suivants de modèles dans la section de hello [les modèles de conception de Table](#table-design-patterns) adresse optimisation des performances hello ou votre insertion, la mise à jour et supprimer des opérations :  

* [Un volume élevé supprimer modèle](#high-volume-delete-pattern) -suppression de hello activation d’un volume élevé d’entités en stockant toutes les entités hello pour suppression simultanée dans leur propre table distincte ; vous supprimer des entités de hello en supprimant la table de hello.  
* [Modèle de série de données](#data-series-pattern) -série de données complète de magasin seule entité toominimize hello de plusieurs demandes.  
* [Modèle d’entités large](#wide-entities-pattern) -utiliser des entités logiques plusieurs entités physiques toostore avec plus de 252 propriétés.  
* [Modèle d’entités volumineux](#large-entities-pattern) -utiliser blob stockage toostore grande des valeurs.  

### <a name="ensuring-consistency-in-your-stored-entities"></a>Vérification de la cohérence de vos entités stockées
Hello autre facteur clé qui influencent votre choix de clés pour l’optimisation des modifications de données est la cohérence tooensure à l’aide de transactions atomiques. Vous ne pouvez utiliser un toooperate EGT sur les entités stockées dans hello même partition.  

Hello suivants de modèles dans la section de hello [les modèles de conception de Table](#table-design-patterns) la gestion de la cohérence des adresses :  

* [Modèle d’index secondaire intra-partition](#intra-partition-secondary-index-pattern) -stocker plusieurs copies de chaque entité à l’aide de différents **RowKey** valeurs (Bonjour même partition) tooenable des recherches rapides et efficaces et tri de substitution à l’aide des commandes autre **RowKey** valeurs.  
* [Modèle de partition entre les index secondaires](#inter-partition-secondary-index-pattern) - stocker plusieurs copies de chaque entité à l’aide de différentes valeurs de RowKey dans des partitions distinctes ou dans des tables distinctes tooenable rapide et des recherches efficaces et tri de substitution des commandes à l’aide de différents **RowKey** valeurs.  
* [Modèle de transactions cohérentes](#eventually-consistent-transactions-pattern) : permet de conserver un comportement cohérent entre les limites de partition ou les limites du système de stockage à l’aide des files d’attente Azure.
* [Modèle d’entités index](#index-entities-pattern) -conserver les index entités tooenable recherches efficaces qui retournent les listes des entités.  
* [Modèle de dénormalisation](#denormalization-pattern) -combiner reliés de données dans une seule entité tooenable tooretrieve tous hello des données que vous avez besoin d’une requête de point unique.  
* [Modèle de série de données](#data-series-pattern) -série de données complète de magasin seule entité toominimize hello de plusieurs demandes.  

Pour plus d’informations sur les transactions de groupe d’entités, consultez la section de hello [Transactions de groupe d’entités](#entity-group-transactions).  

### <a name="ensuring-your-design-for-efficient-modifications-facilitates-efficient-queries"></a>Garantie que votre conception visant à effectuer des modifications efficaces facilite les requêtes efficaces
Dans de nombreux cas, une conception pour les résultats de requêtes efficace dans modifications efficace, mais vous devez évaluez toujours s’il s’agit de cas hello pour votre scénario spécifique. Certains schémas hello dans la section de hello [les modèles de conception de Table](#table-design-patterns) explicitement évaluer les compromis entre l’interrogation et la modification des entités, et vous devez toujours prendre en compte hello quantité, pour chaque type d’opération.  

Hello suivants de modèles dans la section de hello [les modèles de conception de Table](#table-design-patterns) compromis entre la conception de requêtes efficaces et de conception pour la modification de données efficace d’adresses :  

* [Modèle clé composé](#compound-key-pattern) -utilisez composé **RowKey** valeurs tooenable un toolookup client liés de données avec une requête de point unique.  
* [Le modèle de la fin du journal](#log-tail-pattern) -récupérer hello  *n*  entités la plus récemment ajoutée tooa partition à l’aide un **RowKey** valeur trie inverse de date et l’ordre chronologique.  

## <a name="encrypting-table-data"></a>Chiffrement de données de table
Hello bibliothèque cliente de stockage de Azure .NET prend en charge le chiffrement des propriétés d’entité de chaîne pour l’insertion d’opérations et de remplacement. chaînes de Hello chiffrée sont stockées sur le service de hello en tant que propriétés binaires, et elles sont converties en arrière toostrings après le déchiffrement.    

Pour les tables, en outre toohello de stratégie de chiffrement, les utilisateurs doivent spécifier hello propriétés toobe est chiffré. Pour ce faire, il faut spécifier un attribut EncryptProperty \(pour les entités POCO qui dérivent de TableEntity) ou un programme de résolution de chiffrement dans les options de requête. Un programme de résolution de chiffrement est un délégué qui prend une clé de partition, une clé de ligne et un nom de propriété, puis renvoie une valeur booléenne indiquant si cette propriété doit être chiffrée. Au cours du chiffrement, bibliothèque cliente de hello utilisera cette toodecide informations si une propriété doit être chiffrée lors de l’écriture toohello câble. délégué de Hello prévoit également de la possibilité de hello de logique autour de la façon dont les propriétés sont cryptées. (Par exemple, si X, alors chiffrer la propriété A ; sinon chiffrer les propriétés A et B.) Notez qu’il est tooprovide n’est pas nécessaire de ces informations lors de la lecture ou l’interrogation des entités.

Notez que la fusion n’est pas prise en charge pour le moment. Dans la mesure où un sous-ensemble de propriétés aient été crypté précédemment à l’aide d’une autre clé, simplement la fusion de nouvelles propriétés de hello et mise à jour des métadonnées de hello entraîne une perte de données. La fusion soit nécessite un service supplémentaire appels entité de tooread hello existant à partir du service de hello, ou à l’aide d’une nouvelle clé par propriété, qui ne conviennent pas pour des raisons de performances.     

Pour plus d’informations sur le chiffrement des données de table, consultez [Chiffrement côté client et coffre de clés Azure pour Microsoft Azure Storage](storage-client-side-encryption.md).  

## <a name="modelling-relationships"></a>Modélisation des relations
Création de modèles de domaine est une étape clée dans la conception de hello des systèmes complexes. En règle générale, vous hello modélisation des processus tooidentify entités et relations hello entre eux, comme un moyen toounderstand hello du domaine d’entreprise informent conception hello de votre système. Cette section se concentre sur la façon dont vous pouvez traduire certains des types hello communs relation trouvés dans toodesigns de modèles de domaine pour hello service de Table. processus de Hello de mappage à partir d’un logique tooa de modèle de données physique en fonction-modèle de données NoSQL est très différente de celle utilisée lors de la conception d’une base de données relationnelle. Conception de bases de données relationnelles suppose généralement un processus de normalisation de données optimisé pour minimiser la redondance – et une fonctionnalité de requête déclarative qui résumés hello la mise en œuvre du fonctionne de la base de données hello.  

### <a name="one-to-many-relationships"></a>Relations un-à-plusieurs
Les relations un-à-plusieurs entre des objets de domaine d'entreprise se produisent très fréquemment : par exemple, un service a de nombreux employés. Il existe plusieurs relations de type un-à-plusieurs façons tooimplement Bonjour service de Table chaque avec leurs avantages et inconvénients qui peuvent être pertinentes toohello scénario en particulier.  

Considérez l’exemple hello d’une grande entreprise multinationale avec des dizaines de milliers de services et les entités employé où chaque service a de nombreux employés et chaque employé comme associée à un service spécifique. Une approche consiste à service distincts de toostore et entités employé telles que celles-ci :  

![][1]

Cet exemple montre une relation un-à-plusieurs implicite entre types hello selon hello **PartitionKey** valeur. Chaque service peut avoir de nombreux employés.  

Cet exemple montre également une entité de service et ses entités employé dans hello même partition. Vous pouvez choisir toouse différentes partitions, les tables ou même des comptes de stockage pour hello différents types d’entité.  

Une autre approche est toodenormalize vos entités employé uniquement données et le magasin avec des données dénormalisées département, comme indiqué dans hello l’exemple suivant. Dans ce scénario particulier, cette approche dénormalisée peut-être pas hello meilleures si vous avez un besoin toobe toochange en mesure de hello les détails d’un gestionnaire de service car toodo cela vous devez tooupdate chaque employé dans le service de hello.  

![][2]

Pour plus d’informations, consultez hello [modèle de dénormalisation](#denormalization-pattern) plus loin dans ce guide.  

Hello tableau suivant résume les avantages et inconvénients de chacune des approches hello présentées ci-dessus pour le stockage des employés et des entités de service qui ont une relation un-à-plusieurs hello. Vous devez également envisager la fréquence à laquelle tooperform diverses opérations : il peut être acceptable toohave une conception qui inclut une opération coûteuse, si cette opération ne se produit que rarement.  

<table>
<tr>
<th>Approche</th>
<th>Avantages</th>
<th>Inconvénients</th>
</tr>
<tr>
<td>Séparation des types d'entités, même partition, même table</td>
<td>
<ul>
<li>Vous pouvez mettre à jour une entité de service en une seule opération.</li>
<li>Vous pouvez utiliser une cohérence de toomaintain EGT si vous disposez d’une exigence toomodify une entité de service chaque fois que vous mise à jour/insertion/suppression une entité employee. Par exemple, si vous conservez un nombre d'employés de service pour chaque service.</li>
</ul>
</td>
<td>
<ul>
<li>Vous devrez peut-être tooretrieve un employé et une entité de service pour certaines activités de client.</li>
<li>Opérations de stockage produisent dans hello même partition. Si les volumes de transactions sont élevés, cela peut entraîner une zone sensible.</li>
<li>Vous ne pouvez pas déplacer un employé tooa nouveau service à l’aide d’un EGT.</li>
</ul>
</td>
</tr>
<tr>
<td>Types d'entités distincts, différentes partitions ou différentes tables ou différents comptes de stockage</td>
<td>
<ul>
<li>Vous pouvez mettre à jour une entité de service ou une entité d'employé avec une seule opération.</li>
<li>Au niveau des volumes élevés de transactions, cela peut aider à charge de hello réparti sur plusieurs partitions.</li>
</ul>
</td>
<td>
<ul>
<li>Vous devrez peut-être tooretrieve un employé et une entité de service pour certaines activités de client.</li>
<li>Vous ne pouvez pas utiliser EGTs toomaintain cohérence lorsque vous mise à jour/insertion/suppression un employé et mise à jour un service. Par exemple, la mise à jour d'un nombre d'employés dans une entité de service.</li>
<li>Vous ne pouvez pas déplacer un employé tooa nouveau service à l’aide d’un EGT.</li>
</ul>
</td>
</tr>
<tr>
<td>Dénormaliser en type d'entité unique</td>
<td>
<ul>
<li>Vous pouvez récupérer toutes les informations de hello que vous avez besoin d’une demande unique.</li>
</ul>
</td>
<td>
<ul>
<li>Il peut être coûteuse toomaintain cohérence si vous avez besoin des informations de service tooupdate (cela nécessiterait vous tooupdate tous les employés hello dans un service).</li>
</ul>
</td>
</tr>
</table>

Comment vous choisir entre ces options et les professionnels de l’hello et les inconvénients sont plus importantes, dépend de vos scénarios d’application spécifique. Par exemple, la fréquence à laquelle vous modifiez des entités de service ; toutes vos requêtes employé doivent-elles hello départemental des informations supplémentaires ; Comment fermer vous sont les limites d’extensibilité toohello sur vos partitions ou votre compte de stockage ?  

### <a name="one-to-one-relationships"></a>Relations un à un
Les modèles de domaines peuvent inclure des relations un à un entre les entités. Si vous devez tooimplement une relation un à un Bonjour service de Table, vous devez également choisir comment toolink hello deux entités associées lorsque vous avez besoin de tooretrieve tous les deux. Ce lien peut être implicite, selon une convention de valeurs de clés hello ou explicite en stockant un lien sous forme de hello de **PartitionKey** et **RowKey** entité de valeurs dans chaque tooits entité liée. Pour en savoir plus sur si vous devez stocker hello des entités connexes dans hello même partition, consultez la section de hello [un-à-plusieurs relations](#one-to-many-relationships).  

Notez qu’il existe également des considérations sur l’implémentation qui peuvent représenter des relations tooimplement hello service de Table :  

* Gestion des entités volumineuses (pour plus d’informations, consultez [Modèle d’entités volumineuses](#large-entities-pattern))  
* L’implémentation de contrôles d’accès (pour plus d’informations, consultez [Contrôle d’accès avec des signatures d’accès partagé](#controlling-access-with-shared-access-signatures))  

### <a name="join-in-hello-client"></a>Jointure dans le client de hello
Bien qu’il existe des relations de façons toomodel Bonjour service de Table, vous que deux raisons principales hello pour l’utilisation du service de Table hello sont l’évolutivité et les performances ne devez pas oublier. Si vous trouvez que sont de modélisation plusieurs relations de compromettre les performances hello et l’évolutivité de votre solution, se poser que si elle est nécessaire toobuild tous hello dans votre conception de la table des relations de données. Vous pouvez en mesure de toosimplify hello Design et améliorer les performances de votre solution et l’extensibilité de hello si vous laissez votre application cliente pour effectuer toutes les jointures nécessaires.  

Par exemple, si vous avez des tables de petite taille qui contiennent des données qui ne changent pas souvent, vous pouvez extraire ces données qu’une seule fois et mettre en cache sur le client de hello. Cela permet d’éviter les allers et retours répétées tooretrieve hello des mêmes données. Dans les exemples hello que nous avons abordé dans ce guide, hello ensemble de services dans une petite entreprise est probablement toobe petit et modification rarement rend un bon candidat pour l’application cliente peut télécharger une fois les données et le cache en tant que données de recherche.  

### <a name="inheritance-relationships"></a>Relations d'héritage
Si votre application cliente utilise un ensemble de classes faisant partie d’un entités toorepresent relation d’héritage, vous pouvez facilement conserver ces entités Bonjour service de Table. Par exemple, vous disposez hello suivant l’ensemble de classes définies dans votre application cliente où **personne** est une classe abstraite.

![][3]

Vous pouvez conserver les instances de deux classes concrètes hello Bonjour service de Table à l’aide d’une seule table de personne à l’aide des entités dans ressemblant à ceci :  

![][4]

Pour plus d’informations sur l’utilisation de plusieurs types d’entités dans la même table dans le code client de hello, consultez la section de hello [utilisation des types d’entités hétérogènes](#working-with-heterogeneous-entity-types) plus loin dans ce guide. Cela fournit des exemples de la façon dont toorecognize hello type d’entité dans le code client.  

## <a name="table-design-patterns"></a>Modèles de conception de table
Dans les sections précédentes, vous avez vu certaines des descriptions détaillées sur comment toooptimize votre table de conception pour les deux la récupération des données d’entité à l’aide de requêtes et d’insertion, de mise à jour et de suppression des données d’entité. Cette section décrit certains modèles appropriés pour une utilisation avec des solutions de service de Table. En outre, vous verrez comment vous pouvez pratiquement résoudre certains problèmes de hello et compromis générées précédemment dans ce guide. Hello diagramme suivant résume les relations entre différents modèles d’hello hello :  

![][5]

mappage de modèle Hello ci-dessus met en évidence des relations entre des modèles (bleus) et anti-modèles (orange) qui sont décrits dans ce guide. Il existe bien sûr bien d'autres modèles qui méritent votre attention. Par exemple, un des principaux scénarios de hello pour Service de Table est toouse hello [modèle de vue matérialisée](https://msdn.microsoft.com/library/azure/dn589782.aspx) de hello [répartition de responsabilité requête commande (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx) modèle.  

### <a name="intra-partition-secondary-index-pattern"></a>Modèle d’index secondaire intra-partition
Stocker plusieurs copies de chaque entité à l’aide de différents **RowKey** valeurs (Bonjour même partition) tooenable des recherches rapides et efficaces et tri de substitution des commandes à l’aide de différents **RowKey** valeurs. La cohérence des mises à jour entre les copies peut être assurée à l’aide d’une EGT.  

#### <a name="context-and-problem"></a>Contexte et problème
Hello service de Table indexe automatiquement des entités à l’aide de hello **PartitionKey** et **RowKey** valeurs. Cela permet une tooretrieve d’application client à une entité efficacement à l’aide de ces valeurs. Par exemple, à l’aide de la structure de la table hello illustré ci-dessous, une application cliente peut utiliser un tooretrieve requête de point d’une entité de l’employé individuel en utilisant le nom du service informatique hello et id d’employé hello (hello **PartitionKey** et  **RowKey** valeurs). Un client peut également récupérer des entités, triées par ID d'employé au sein de chaque service.

![][6]

Si vous voulez également toofind en mesure de toobe une entité employee en fonction de valeur hello d’une autre propriété, telles que l’adresse de messagerie, vous devez utiliser un toofind d’analyse partition moins efficace une correspondance. Il s’agit, car le service de table hello ne fournit pas d’index secondaires. En outre, il n’existe aucune option toorequest une liste d’employés triés dans un ordre différent de celui **RowKey** ordre.  

#### <a name="solution"></a>Solution
toowork autour d’un manque de hello d’index secondaires, vous pouvez stocker plusieurs copies de chaque entité avec chaque copie à l’aide d’une autre **RowKey** valeur. Si vous stockez une entité avec les structures hello illustrés ci-dessous, vous pouvez récupérer efficacement des entités employee en fonction de l’id de courrier électronique adresse ou de l’employé. Hello des valeurs de préfixe de hello **RowKey**, « empid_ » et « email_ » permettent tooquery pour un seul employé ou une plage d’employés à l’aide d’une plage d’adresses de messagerie ou l’ID d’employé.  

![][7]

Hello suivant deux critères de filtre (une recherche par id d’employé et une recherche par adresse de messagerie), tous deux spécifient des requêtes de point de :  

* $filter=(PartitionKey eq ’Sales’) and (RowKey eq ’empid_000223’)  
* $filter=(PartitionKey eq 'Sales') and (RowKey eq email_jonesj@contoso.com  

Si vous interrogez pour une plage d’entités de l’employé, vous pouvez spécifier une plage triée dans l’ordre des id employé, ou une plage triée dans l’ordre d’adresse de messagerie en interrogeant des entités avec le préfixe approprié de hello Bonjour **RowKey**.  

* l’utilisation de tous les employés hello dans le service des ventes hello avec un id d’employé dans hello plage 000100 too000199 toofind : $filter = (PartitionKey eq 'Sales') et (RowKey ge 'empid_000100') et (le RowKey 'empid_000199')  
* toofind tous hello employés du département des ventes hello avec une adresse de messagerie commençant par hello lettre « a » utilisation : $filter = (PartitionKey eq 'Sales') et (RowKey ge 'email_a') et (RowKey lt 'email_b')  
  
  Notez que la syntaxe du filtre hello utilisé dans les exemples hello ci-dessus est hello service de Table API REST, pour plus d’informations, consultez [interroger des entités](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

#### <a name="issues-and-considerations"></a>Problèmes et considérations
Prendre en compte les points suivants lorsque vous décidez de hello comment tooimplement ce modèle :  

* Stockage de table étant relativement peu coûteux toouse hello coût des frais de stockage des données en double ne doit pas être une préoccupation majeure. Toutefois, vous devez toujours évaluée coût hello de votre conception en fonction de vos besoins de stockage et ajouter uniquement des entités en double toosupport hello requêtes que votre application cliente s’exécute.  
* Entités d’index secondaire hello sont stockées dans hello même partition en tant qu’entités d’origine de hello, vous devez vous assurer que vous ne dépassez pas les objectifs d’évolutivité hello pour une partition individuelle.  
* Vous pouvez conserver vos entités en double cohérents entre eux à l’aide de EGTs tooupdate hello deux des copies de l’entité de hello atomiquement. Cela implique que vous devez stocker toutes les copies d’une entité dans hello même partition. Pour plus d’informations, consultez la section de hello [à l’aide de Transactions de groupe d’entités](#entity-group-transactions).  
* valeur utilisée pour hello de Hello **RowKey** doit être unique pour chaque entité. Nous vous conseillons d'utiliser des valeurs de clé composée.  
* Remplissage des valeurs numériques dans hello **RowKey** (par exemple, id d’employé hello 000223), permet de corriger le tri et de filtrage en fonction des limites supérieures et inférieures.  
* Vous ne devez pas nécessairement tooduplicate toutes les propriétés de hello de votre entité. Par exemple, si hello requêtes envoyer par courrier électronique des entités hello de recherche à l’aide de hello adressent Bonjour **RowKey** ont jamais besoin d’âge de l’employé hello, ces entités peut avoir hello suivant structure :

![][8]

* Il est généralement préférable de doublons toostore et vous assurer que vous pouvez récupérer toutes les données hello vous avez besoin d’une seule requête, à toouse une requête toolocate une entité et un autre toolookup hello données requises.  

#### <a name="when-toouse-this-pattern"></a>Lorsque toouse ce modèle
Utilisez ce modèle lorsque votre application cliente doit tooretrieve les entités à l’aide d’une variété de clés différentes, lorsque votre client nécessite des entités tooretrieve dans différents ordres de tri, et où vous pouvez identifier chaque entité à une série de valeurs uniques. Toutefois, vous devez être sûr de ne pas dépasser les limites d’extensibilité hello partition lorsque vous effectuez des recherches d’entité à l’aide de la hello différents **RowKey** valeurs.  

#### <a name="related-patterns-and-guidance"></a>Conseils et modèles connexes
Hello suivantes des modèles et des instructions peuvent également être intéressant lorsque vous implémentez ce modèle :  

* [Modèle d’index secondaire entre les partitions](#inter-partition-secondary-index-pattern)
* [Modèle de clé composée](#compound-key-pattern)
* [Transactions de groupe d’entités](#entity-group-transactions)
* [Utilisation des types d’entités hétérogènes](#working-with-heterogeneous-entity-types)

### <a name="inter-partition-secondary-index-pattern"></a>Modèle d’index secondaire entre les partitions
Stocker plusieurs copies de chaque entité à l’aide de différents **RowKey** valeurs dans des partitions distinctes ou dans les recherches des tables distinctes tooenable rapides et efficaces et ordres de tri secondaires à l’aide de différents **RowKey**valeurs.  

#### <a name="context-and-problem"></a>Contexte et problème
Hello service de Table indexe automatiquement des entités à l’aide de hello **PartitionKey** et **RowKey** valeurs. Cela permet une tooretrieve d’application client à une entité efficacement à l’aide de ces valeurs. Par exemple, à l’aide de la structure de la table hello illustré ci-dessous, une application cliente peut utiliser un tooretrieve requête de point d’une entité de l’employé individuel en utilisant le nom du service informatique hello et id d’employé hello (hello **PartitionKey** et  **RowKey** valeurs). Un client peut également récupérer des entités, triées par ID d'employé au sein de chaque service.  

![][9]

Si vous voulez également toofind en mesure de toobe une entité employee en fonction de valeur hello d’une autre propriété, telles que l’adresse de messagerie, vous devez utiliser un toofind d’analyse partition moins efficace une correspondance. Il s’agit, car le service de table hello ne fournit pas d’index secondaires. En outre, il n’existe aucune option toorequest une liste d’employés triés dans un ordre différent de celui **RowKey** ordre.  

Vous comptez un volume très élevé de transactions par rapport à ces entités et que vous souhaitez risque de hello toominimize Hello limitation votre client de service de Table.  

#### <a name="solution"></a>Solution
toowork autour d’un manque de hello d’index secondaires, vous pouvez stocker plusieurs copies de chaque entité avec chaque copie à l’aide de différents **PartitionKey** et **RowKey** valeurs. Si vous stockez une entité avec les structures hello illustrés ci-dessous, vous pouvez récupérer efficacement des entités employee en fonction de l’id de courrier électronique adresse ou de l’employé. Hello des valeurs de préfixe de hello **PartitionKey**, « empid_ » et « email_ » permettent de tooidentify qui index que vous souhaitez toouse pour une requête.  

![][10]

Hello suivant deux critères de filtre (une recherche par id d’employé et une recherche par adresse de messagerie), tous deux spécifient des requêtes de point de :  

* $filter=(PartitionKey eq ’empid_Sales’) and (RowKey eq ’000223’)
* $filter=(PartitionKey eq ’email_Sales’) and (RowKey eq jonesj@contoso.com  

Si vous interrogez pour une plage d’entités de l’employé, vous pouvez spécifier une plage triée dans l’ordre des id employé, ou une plage triée dans l’ordre d’adresse de messagerie en interrogeant des entités avec le préfixe approprié de hello Bonjour **RowKey**.  

* toofind tous hello employés dans hello service des ventes avec un id d’employé dans la plage de hello **000100** trop**000199** triées en cours d’utilisation d’order id employé : $filter = (PartitionKey eq ' empid_Sales') et (RowKey ge ' 000100') et (le RowKey '000199')  
* toofind tous les employés hello dans le service des ventes hello avec une adresse de messagerie qui commence par « a » dans Utilisation de commande d’adresse de messagerie : $filter = (PartitionKey eq ' email_Sales') et (RowKey ge 'a') et (RowKey lt 'b')  

Notez que la syntaxe du filtre hello utilisé dans les exemples hello ci-dessus est hello service de Table API REST, pour plus d’informations, consultez [interroger des entités](http://msdn.microsoft.com/library/azure/dd179421.aspx).  

#### <a name="issues-and-considerations"></a>Problèmes et considérations
Prendre en compte les points suivants lorsque vous décidez de hello comment tooimplement ce modèle :  

* Vous pouvez conserver vos entités en double cohérente entre eux à l’aide de hello [modèle de transactions cohérente](#eventually-consistent-transactions-pattern) entités de toomaintain hello index primaires et secondaires.  
* Stockage de table étant relativement peu coûteux toouse hello coût des frais de stockage des données en double ne doit pas être une préoccupation majeure. Toutefois, vous devez toujours évaluée coût hello de votre conception en fonction de vos besoins de stockage et ajouter uniquement des entités en double toosupport hello requêtes que votre application cliente s’exécute.  
* valeur utilisée pour hello de Hello **RowKey** doit être unique pour chaque entité. Nous vous conseillons d'utiliser des valeurs de clé composée.  
* Remplissage des valeurs numériques dans hello **RowKey** (par exemple, id d’employé hello 000223), permet de corriger le tri et de filtrage en fonction des limites supérieures et inférieures.  
* Vous ne devez pas nécessairement tooduplicate toutes les propriétés de hello de votre entité. Par exemple, si hello requêtes envoyer par courrier électronique des entités hello de recherche à l’aide de hello adressent Bonjour **RowKey** ont jamais besoin d’âge de l’employé hello, ces entités peut avoir hello suivant structure :
  
  ![][11]
* Il est généralement une meilleure toostore des données en double et vous assurer que vous pouvez récupérer toutes les données hello que vous avez besoin d’une requête unique que toolocate d’une requête toouse une entité à l’aide de hello index secondaire et un autre toolookup hello les données requises dans les index primaire hello.  

#### <a name="when-toouse-this-pattern"></a>Lorsque toouse ce modèle
Utilisez ce modèle lorsque votre application cliente doit tooretrieve les entités à l’aide d’une variété de clés différentes, lorsque votre client nécessite des entités tooretrieve dans différents ordres de tri, et où vous pouvez identifier chaque entité à une série de valeurs uniques. Utilisez ce modèle lorsque vous souhaitez tooavoid dépassement des limites de l’évolutivité de partition hello lorsque vous effectuez des recherches d’entité à l’aide de la hello différents **RowKey** valeurs.  

#### <a name="related-patterns-and-guidance"></a>Conseils et modèles connexes
Hello suivantes des modèles et des instructions peuvent également être intéressant lorsque vous implémentez ce modèle :  

* [Modèle de transactions cohérentes](#eventually-consistent-transactions-pattern)  
* [Modèle d’index secondaire intra-partition](#intra-partition-secondary-index-pattern)  
* [Modèle de clé composée](#compound-key-pattern)  
* [Transactions de groupe d’entités](#entity-group-transactions)  
* [Utilisation des types d’entités hétérogènes](#working-with-heterogeneous-entity-types)  

### <a name="eventually-consistent-transactions-pattern"></a>Modèle de transactions cohérentes
Permet de conserver un comportement cohérent entre les limites de partition ou les limites du système de stockage à l'aide des files d'attente Azure.  

#### <a name="context-and-problem"></a>Contexte et problème
EGTs activer les transactions atomiques entre plusieurs entités qui partagent hello même clé de partition. Pour des raisons d’évolutivité et des performances, vous pouvez décider d’entités toostore qui ont des exigences de cohérence dans des partitions distinctes ou dans un système de stockage distincts : dans ce scénario, vous ne pouvez pas utiliser EGTs toomaintain cohérence. Par exemple, peut avoir une cohérence éventuelle de toomaintain exigence entre :  

* Entités stockées dans deux partitions différentes dans la même table, dans des tables différentes, dans différents comptes de stockage de hello.  
* Une entité stockées Bonjour service de Table et un objet blob dans hello service Blob.  
* Une entité est stockée dans le service de Table hello et un fichier dans un système de fichiers.  
* Une entité stocker Bonjour service de Table encore indexées à l’aide du service Azure Search de hello.  

#### <a name="solution"></a>Solution
À l'aide des files d'attente Azure, vous pouvez implémenter une solution cohérente entre plusieurs partitions ou systèmes de stockage.
tooillustrate cette approche, vous possédez une exigence toobe tooarchive en mesure d’anciennes employé entités. Les anciennes entités d'employés sont rarement interrogées et doivent être exclues de toutes les activités impliquant des employés actuels. tooimplement cette exigence, vous stockez les employés actifs dans hello **actuel** table et les anciens employés Bonjour **Archive** table. L’archivage d’un employé nécessite que vous toodelete entité hello hello **actuel** de table et ajouter hello entité toohello **Archive** table, mais vous ne pouvez pas utiliser un tooperform EGT ces deux opérations. risque de hello tooavoid qu’une défaillance, une entité tooappear dans les deux ou aucune des tables, l’opération d’archivage hello doit être cohérente. Hello diagramme de séquence suivant décrit les étapes de hello dans cette opération. Informations supplémentaires sont disponibles pour les chemins d’accès de l’exception suivante du texte hello.  

![][12]

Un client lance une opération d’archivage hello en plaçant un message dans une file d’attente Azure, dans cet employé de tooarchive exemple #456. Un rôle de travail interroge la file d’attente hello pour les nouveaux messages ; Lorsqu’il trouve un, il lit le message de type hello et laisse une copie masquée sur la file d’attente hello. rôle de travail Hello extrait ensuite une copie de l’entité de hello hello **actuel** table, insère une copie Bonjour **Archive** table, puis hello suppressions d’origine à partir de hello **actuel**table. Enfin, s’il n’y a aucuns erreurs des étapes précédentes de hello, rôle de travail hello supprime message de type hello masqué à partir de la file d’attente hello.  

Dans cet exemple, l’étape 4 insère employé de hello hello **Archive** table. Il peut ajouter hello employé tooa objet blob dans hello service Blob ou un fichier dans un système de fichiers.  

#### <a name="recovering-from-failures"></a>Récupération après échec
Il est important que hello opérations dans les étapes **4** et **5** doit être *idempotent* au cas où l’opération d’archivage hello toorestart a besoin de rôle de travail hello. Si vous utilisez le service de Table hello, de l’étape **4** vous devez utiliser une opération « Insérer ou remplacer » ; pour l’étape **5** vous devez utiliser un « supprimer si existe « opération dans la bibliothèque cliente de hello que vous utilisez. Si vous utilisez un autre système de stockage, vous devez utiliser une opération idempotent appropriée.  

Si le rôle de travail hello ne termine jamais étape **6**, puis une fois que vous continuez à recevoir un message de type hello du délai d’attente sur la file d’attente hello préparer pour hello travail rôle tootry tooreprocess. rôle de travail Hello peut vérifier le nombre de fois où un message sur la file d’attente hello a été lu et, si nécessaire, indicateur, il est un message « incohérent » un examen plus approfondi en l’envoyant tooa séparer la file d’attente. Pour plus d’informations sur la lecture de messages de la file d’attente et la vérification hello dequeue count, consultez [Get Messages](https://msdn.microsoft.com/library/azure/dd179474.aspx).  

Certaines erreurs à partir des services de Table et de la file d’attente hello sont des erreurs temporaires et votre application cliente doit inclure toohandle logique de nouvelle tentative approprié les.  

#### <a name="issues-and-considerations"></a>Problèmes et considérations
Prendre en compte les points suivants lorsque vous décidez de hello comment tooimplement ce modèle :  

* Cette solution ne fournit pas d'isolation des transactions. Par exemple, un client peut lire hello **actuel** et **Archive** tables lorsque le rôle de travail hello s’est produit entre les étapes **4** et **5**et consultez un vue incohérente des données de hello. Notez que les données de salutation sera cohérentes par la suite.  
* Il se peut que vous devez vous assurer que les étapes 4 et 5 sont idempotents dans cohérence éventuelle tooensure de commande.  
* Vous pouvez adapter la solution de hello à l’aide de plusieurs files d’attente et les instances de rôle de travail.  

#### <a name="when-toouse-this-pattern"></a>Lorsque toouse ce modèle
Utilisez ce modèle lorsque vous souhaitez que la cohérence éventuelle de tooguarantee entre des entités qui existent dans différentes partitions ou tables. Vous pouvez étendre cette cohérence éventuelle tooensure de modèle pour les opérations sur le service de Table hello et service d’objets Blob hello et autres sources de données non - Azure Storage comme système de fichiers de base de données ou hello.  

#### <a name="related-patterns-and-guidance"></a>Conseils et modèles connexes
Hello suivantes des modèles et des instructions peuvent également être intéressant lorsque vous implémentez ce modèle :  

* [Transactions de groupe d’entités](#entity-group-transactions)  
* [Fusion ou remplacement](#merge-or-replace)  

> [!NOTE]
> Si l’isolation des transactions est importante tooyour solution, vous devez envisager de reconcevoir votre tooenable de tables vous toouse EGTs.  
> 
> 

### <a name="index-entities-pattern"></a>Modèle d’entités d’index
Mettre à jour les index entités tooenable recherches efficaces qui retournent les listes des entités.  

#### <a name="context-and-problem"></a>Contexte et problème
Hello service de Table indexe automatiquement des entités à l’aide de hello **PartitionKey** et **RowKey** valeurs. Cela permet une tooretrieve d’application client une entité efficacement à l’aide d’une requête de point. Par exemple, à l’aide de la structure de la table hello illustré ci-dessous, une application cliente peut récupérer une entité employee individuels en utilisant le nom du service informatique hello et id d’employé hello (hello **PartitionKey** et **RowKey** ).  

![][13]

Si vous voulez également tooretrieve en mesure de toobe une liste des entités de l’employé en fonction de la valeur hello d’une autre propriété non uniques, telles que son nom, vous devez utiliser une partition moins efficace analyse toofind correspondances au lieu d’utiliser un index toolook les configurer directement. Il s’agit, car le service de table hello ne fournit pas d’index secondaires.  

#### <a name="solution"></a>Solution
recherche de tooenable par nom avec structure d’entité hello illustrée ci-dessus, vous devez gérer des listes d’ID d’employé. Si vous souhaitez que les entités tooretrieve hello employé avec un nom donné, tels que Jones, vous devez d’abord localiser liste hello des ID d’employés pour les employés Jones comme leur nom et puis d’extraire ces entités employé. Il existe trois options principales pour le stockage des listes hello d’ID d’employé :  

* Le stockage d'objets blob.  
* Créer des entités de l’index dans hello même partition en tant qu’entités d’employé hello.  
* La création d'entités d'index dans une table ou une partition séparée.  

<u>Méthode nº 1 : stockage d’objets blob</u>  

Pour la première option de hello, vous créez un objet blob pour chaque nom unique et chaque magasin d’objets blob une liste de hello **PartitionKey** (service) et **RowKey** valeurs (id d’employé) pour les employés qui ont ce dernier. nom. Lorsque vous ajoutez ou supprimez un employé, vous devez vous assurer que contenu hello du blob pertinentes de hello est cohérent avec les entités d’employé hello.  

<u>Option #2 :</u> entités Create index hello même partition  

Pour la deuxième option de hello, utilisez les entités index qui stockent les données suivantes de hello :  

![][14]

Hello **EmployeeIDs** propriété contient une liste des ID d’employés pour les employés avec nom hello stockée Bonjour **RowKey**.  

Hello étapes suivantes décrivent les processus hello que vous devez suivre lorsque vous ajoutez un nouvel employé si vous utilisez la deuxième option de hello. Dans cet exemple, nous ajoutons un employé avec l’Id 000152 et un nom de famille Jones dans le service des ventes hello :  

1. Récupérer l’entité d’index hello avec un **PartitionKey** de valeur « Ventes » et hello **RowKey** valeur « Jones ». Enregistrez hello ETag de toouse de cette entité à l’étape 2.  
2. Créer une transaction de groupe d’entités (autrement dit, une opération de traitement par lots) qui insère l’entité employee hello (**PartitionKey** valeur « Ventes » et **RowKey** valeur « 000152 »), et les mises à jour hello entité d’index ( **PartitionKey** valeur « Ventes » et **RowKey** valeur « Jones ») en ajoutant hello nouvelle employee id toohello liste hello EmployeeIDs champ. Pour plus d’informations sur les transactions de groupe d’entités, consultez [Transactions de groupe d’entités](#entity-group-transactions).  
3. Si la transaction de groupe d’entités hello échoue en raison d’une erreur d’accès concurrentiel optimiste (quelqu'un d’autre a modifié uniquement l’entité d’index hello), vous devez toostart sur à l’étape 1 à nouveau.  

Vous pouvez utiliser un toodeleting approche similaire employé si vous utilisez la deuxième option de hello. La modification du nom d’un employé est légèrement plus complexe, car vous devez tooexecute une transaction de groupe d’entités qui met à jour les trois entités : hello entité employee, hello index pour nom ancienne hello et hello index pour hello nouveau nom. Vous devez extraire chaque entité avant d’apporter toutes les modifications dans l’ordre des valeurs d’ETag hello tooretrieve que vous pouvez ensuite utiliser les mises à jour de hello tooperform à l’aide de l’accès concurrentiel optimiste.  

Hello étapes suivantes décrivent les processus hello que vous devez suivre lorsque vous avez besoin de toolook de tous les employés hello avec un nom donné dans un service si vous utilisez la deuxième option de hello. Dans cet exemple, nous recherchons les tous les employés hello avec le nom de famille Jones dans le service des ventes hello :  

1. Récupérer l’entité d’index hello avec un **PartitionKey** de valeur « Ventes » et hello **RowKey** valeur « Jones ».  
2. Analyser la liste hello des identificateurs dans le champ de EmployeeIDs hello des employés.  
3. Si vous avez besoin des informations supplémentaires sur chacun de ces employés (par exemple, leurs adresses de messagerie), extraire chacune des entités d’employé hello à l’aide de **PartitionKey** valeur « Ventes » et **RowKey** les valeurs à partir de liste Hello d’employés obtenu à l’étape 2.  

<u>Méthode nº 3 :</u> création d’entités d’index dans une table ou une partition séparée  

Pour la troisième option de hello, utilisez les entités index qui stockent les données suivantes de hello :  

![][15]

Hello **EmployeeIDs** propriété contient une liste des ID d’employés pour les employés avec nom hello stockée Bonjour **RowKey**.  

Avec l’option de tiers hello, vous ne pouvez pas utiliser EGTs toomaintain cohérence hello index entités étant dans une partition distincte à partir des entités employé hello. Vous devez vous assurer que les entités index hello cohérentes avec les entités d’employé hello.  

#### <a name="issues-and-considerations"></a>Problèmes et considérations
Prendre en compte les points suivants lorsque vous décidez de hello comment tooimplement ce modèle :  

* Cette solution requiert tooretrieve au moins deux requêtes correspondance entités : un tooquery hello index liste les entités tooobtain hello de **RowKey** de valeurs et interroge ensuite tooretrieve chaque entité dans la liste de hello.  
* Étant donné qu’une entité individuelle a une taille maximale de 1 Mo, option #2 et l’option #3 dans la solution de hello supposent que liste hello des ID d’employés pour n’importe quel nom donné n’est jamais supérieure à 1 Mo. Si la liste hello d’ID d’employé est probablement toobe supérieur à 1 Mo, utiliser l’option #1 et stocker des données d’index hello dans le stockage blob.  
* Si vous utilisez l’option #2 (à l’aide de EGTs toohandle Ajout et suppression des employés et la modification du nom d’un employé) vous devez déterminer si le volume hello de transactions s’approche des limites d’extensibilité hello dans une partition donnée. Si c’est le cas de hello, vous devez envisager une solution cohérente (option #1 ou #3) qui utilise la mise à jour de files d’attente toohandle hello demande et permet de vous toostore vos entités de l’index dans une partition distincte à partir des entités employé hello.  
* Option #2 dans cette solution suppose que vous souhaitez toolook par nom de famille dans un service : par exemple, vous souhaitez tooretrieve une liste d’employés avec un nom de famille Jones dans le service des ventes hello. Si vous souhaitez toobe les toolook en mesure de configurer tous les employés hello avec un nom de famille Jones dans toute l’organisation hello, utilisez l’option #1 ou #3.
* Vous pouvez implémenter une solution basée sur la file d’attente qui assure la cohérence éventuelle (voir hello [modèle de transactions cohérente](#eventually-consistent-transactions-pattern) pour plus d’informations).  

#### <a name="when-toouse-this-pattern"></a>Lorsque toouse ce modèle
Utilisez ce modèle lorsque vous souhaitez toolookup un ensemble d’entités qui partagent toutes une valeur de propriété courantes, telles que tous les employés dont le nom de famille hello Jones.  

#### <a name="related-patterns-and-guidance"></a>Conseils et modèles connexes
Hello suivantes des modèles et des instructions peuvent également être intéressant lorsque vous implémentez ce modèle :  

* [Modèle de clé composée](#compound-key-pattern)  
* [Modèle de transactions cohérentes](#eventually-consistent-transactions-pattern)  
* [Transactions de groupe d’entités](#entity-group-transactions)  
* [Utilisation des types d’entités hétérogènes](#working-with-heterogeneous-entity-types)  

### <a name="denormalization-pattern"></a>Modèle de dénormalisation
Combiner des données connexes dans une seule entité de tooenable tooretrieve tous hello des données que vous avez besoin d’une requête de point unique.  

#### <a name="context-and-problem"></a>Contexte et problème
Dans une base de données relationnelle, vous normalisez généralement la déduplication des données tooremove résultant dans les requêtes qui extraient des données provenant de plusieurs tables. Si vous normalisez vos données dans des tables Azure, vous devez vous plusieurs allers-retours de hello client toohello server tooretrieve vos données connexes. Par exemple, avec la structure de la table hello illustré ci-dessous, vous avez besoin de deux arrondir allers-retours tooretrieve hello plus d’informations pour un service : une toofetch entité du service hello qui inclut l’id du Gestionnaire de hello et détails d’un autre demande toofetch hello du gestionnaire un employé entité.  

![][16]

#### <a name="solution"></a>Solution
Au lieu de stocker les données de salutation dans deux entités distinctes, dénormaliser les données hello et conserver une copie de détails du Gestionnaire de hello dans entité du service hello. Par exemple :  

![][17]

Avec les entités de service stockées avec ces propriétés, vous pouvez maintenant récupérer tous les détails de hello que vous avez besoin sur un service à l’aide d’une requête de point.  

#### <a name="issues-and-considerations"></a>Problèmes et considérations
Prendre en compte les points suivants lorsque vous décidez de hello comment tooimplement ce modèle :  

* Des coûts réels sont associés au stockage des données à deux reprises. amélioration des performances (résultant de service de stockage moins demandes toohello) généralement Hello compense marginal augmentation des coûts de stockage hello (et ce coût est décalé partiellement par une réduction de nombre hello de transactions vous avez besoin des détails de hello toofetch d’un service).  
* Vous devez maintenir la cohérence de hello de hello deux entités qui stockent des informations sur les gestionnaires. Vous pouvez gérer des problème de cohérence hello à l’aide de EGTs tooupdate plusieurs entités dans une seule transaction atomique : dans ce cas, hello service et hello employé pour le Gestionnaire de service hello sont stockés dans hello même partition.  

#### <a name="when-toouse-this-pattern"></a>Lorsque toouse ce modèle
Utilisez ce modèle lorsque vous devez fréquemment toolook les informations associées. Ce modèle réduit le nombre hello de votre client doit faire des données de hello tooretrieve qu'il nécessite des requêtes.  

#### <a name="related-patterns-and-guidance"></a>Conseils et modèles connexes
Hello suivantes des modèles et des instructions peuvent également être intéressant lorsque vous implémentez ce modèle :  

* [Modèle de clé composée](#compound-key-pattern)  
* [Transactions de groupe d’entités](#entity-group-transactions)  
* [Utilisation des types d’entités hétérogènes](#working-with-heterogeneous-entity-types)

### <a name="compound-key-pattern"></a>Modèle de clé composée
Utilisez composé **RowKey** valeurs tooenable un toolookup client liés de données avec une requête de point unique.  

#### <a name="context-and-problem"></a>Contexte et problème
Dans une base de données relationnelle, il est toouse naturel des jointures dans les requêtes tooreturn connexes du client toohello de données dans une requête unique. Par exemple, vous pouvez utiliser hello employee id toolook la liste des entités connexes qui contiennent des performances et de consulter les données pour cet employé.  

Supposons que vous stockez des entités employee hello service de Table à l’aide de hello suivant structure :  

![][18]

Vous devez également toostore des données historiques relatives tooreviews et performances de chaque employé de hello année a travaillé pour votre organisation et vous devez tooaccess en mesure de toobe ces informations par année. Une option est toocreate une autre table qui stocke les entités avec hello suivant structure :  

![][19]

Notez que cette approche que vous pouvez décider tooduplicate certaines informations (par exemple, prénom et nom) de hello nouvelle entité tooenable vous tooretrieve vos données grâce à une demande unique. Toutefois, vous ne peut pas assurer la cohérence forte, car vous ne pouvez pas utiliser un EGT tooupdate hello deux entités atomiquement.  

#### <a name="solution"></a>Solution
Stocker un nouveau type d’entité dans votre table d’origine à l’aide des entités avec hello suivant structure :  

![][20]

Notez comment hello **RowKey** est maintenant une clé composée constituée par id d’employé hello et année hello de données de révision hello qui vous permet de tooretrieve hello des performances de l’employé et passez en revue les données avec une demande unique pour une entité unique.  

Hello, l’exemple suivant indique comment vous pouvez récupérer toutes les données de révision hello pour un employé donné (par exemple, employé 000123 dans le service des ventes hello) :  

$filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000123') and (RowKey lt 'empid_000124')&$select=RowKey,Manager Rating,Peer Rating,Comments  

#### <a name="issues-and-considerations"></a>Problèmes et considérations
Prendre en compte les points suivants lorsque vous décidez de hello comment tooimplement ce modèle :  

* Vous devez utiliser un caractère de séparation appropriés qui le rend facile tooparse hello **RowKey** valeur : par exemple, **000123_2012**.  
* Vous stockez également cette entité Bonjour même partition en tant que d’autres entités qui contiennent des données associées pour hello même employé, ce qui signifie que vous pouvez utiliser la cohérence forte EGTs toomaintain.
* Vous devez envisager la fréquence à laquelle vous interroge hello données toodetermine si ce modèle est approprié.  Par exemple, si vous accédez à hello rarement des données de révision et hello de données principal employé souvent que vous devez les conserver en tant qu’entités distinctes.  

#### <a name="when-toouse-this-pattern"></a>Lorsque toouse ce modèle
Utilisez ce modèle lorsque vous avez besoin de toostore une ou plusieurs des entités connexes que vous interrogez fréquemment.  

#### <a name="related-patterns-and-guidance"></a>Conseils et modèles connexes
Hello suivantes des modèles et des instructions peuvent également être intéressant lorsque vous implémentez ce modèle :  

* [Transactions de groupe d’entités](#entity-group-transactions)  
* [Utilisation des types d’entités hétérogènes](#working-with-heterogeneous-entity-types)  
* [Modèle de transactions cohérentes](#eventually-consistent-transactions-pattern)  

### <a name="log-tail-pattern"></a>Modèle de fin de journal
Récupérer hello  *n*  entités la plus récemment ajoutée tooa partition en utilisant un **RowKey** valeur trie inverse de date et l’ordre chronologique.  

#### <a name="context-and-problem"></a>Contexte et problème
Une exigence courante est d’être en mesure de tooretrieve entités hello plus récemment créé, par exemple hello dix dernières notes de frais soumises par un employé. Prise en charge des requêtes de table un **$top** hello de tooreturn d’opération de requête tout d’abord  *n*  entités à partir d’un ensemble : il n’existe aucune requête équivalente tooreturn hello dernière n entités d’opération dans un jeu.  

#### <a name="solution"></a>Solution
Les entités de hello Store à l’aide un **RowKey** que naturellement trie dans l’ordre inverse date/heure commande à l’aide d’entrée la plus récente hello est toujours hello dans le tableau de hello.  

Par exemple, tooretrieve en mesure de toobe hello dix dernières notes de frais soumises par un employé, vous pouvez utiliser une valeur de graduation inverse hello dérivée de date/heure actuelle. Hello exemple de code c# suivant montre une façon toocreate une valeur « inversé graduations » approprié pour un **RowKey** qui effectue le tri de toohello plus récente de hello plus ancienne :  

`string invertedTicks = string.Format("{0:D19}", DateTime.MaxValue.Ticks - DateTime.UtcNow.Ticks);`  

Vous pouvez revenir durée toohello date à l’aide de hello suivant de code :  

`DateTime dt = new DateTime(DateTime.MaxValue.Ticks - Int64.Parse(invertedTicks));`  

requête de table Hello ressemble à ceci :  

`https://myaccount.table.core.windows.net/EmployeeExpense(PartitionKey='empid')?$top=10`  

#### <a name="issues-and-considerations"></a>Problèmes et considérations
Prendre en compte les points suivants lorsque vous décidez de hello comment tooimplement ce modèle :  

* Vous devez faire précéder valeur des graduations inverse hello avec des zéros non significatifs trie de valeur de chaîne hello tooensure comme prévu.  
* Vous devez être conscient des objectifs d’évolutivité hello au niveau hello d’une partition. Veillez à ne pas créer des partitions de zone sensible.  

#### <a name="when-toouse-this-pattern"></a>Lorsque toouse ce modèle
Utilisez ce modèle lorsque vous avez besoin d’entités tooaccess dans l’ordre de date/heure inverse ou lorsque vous devez tooaccess hello plus récemment ajouté des entités.  

#### <a name="related-patterns-and-guidance"></a>Conseils et modèles connexes
Hello suivantes des modèles et des instructions peuvent également être intéressant lorsque vous implémentez ce modèle :  

* [Ajouter un anti-modèle ou un préfixe d’anti-modèle](#prepend-append-anti-pattern)  
* [Récupération des entités](#retrieving-entities)  

### <a name="high-volume-delete-pattern"></a>Modèle de suppression de volume élevé
Activer la suppression d’un volume élevé d’entités hello en stockant toutes les entités hello pour suppression simultanée dans leur propre table distincte ; vous supprimez des entités de hello en supprimant la table de hello.  

#### <a name="context-and-problem"></a>Contexte et problème
De nombreuses applications supprimer les anciennes données qui n’a plus besoin application de client toobe tooa disponibles, ou cette application hello a archivé le support de stockage tooanother. Vous identifiez généralement ces données à une date : par exemple, vous avez des enregistrements toodelete a besoin de toutes les demandes de connexion qui ont plus de 60 jours.  

Une conception possible est toouse hello horodatage de la demande de connexion hello Bonjour **RowKey**:  

![][21]

Cette approche évite les zones réactives de partition, car l’application hello peut insérer et supprimer des entités de connexion pour chaque utilisateur dans une partition distincte. Toutefois, cette approche peut s’avérer onéreuse beaucoup de temps si vous avez un grand nombre d’entités, car vous devez tout d’abord tooperform une analyse de table dans l’ordre tooidentify tous les toodelete d’entités hello et vous devez le supprimer chaque entité ancien. Notez que vous pouvez réduire le nombre hello d’allers-retours toohello serveur requis toodelete hello anciennes entités par le traitement par lots de plusieurs demandes de suppression dans EGTs.  

#### <a name="solution"></a>Solution
Utilisez une table distincte pour chaque jour de tentative de connexion. Vous pouvez utiliser la conception d’entité hello ci-dessus tooavoid hotspots lorsque vous insérez des entités, et la suppression des anciennes entités est maintenant simplement une question de la suppression d’une table de tous les jours (une seule opération de stockage) au lieu de la recherche et la suppression des milliers de entités de connexion individuelle tous les jours.  

#### <a name="issues-and-considerations"></a>Problèmes et considérations
Prendre en compte les points suivants lorsque vous décidez de hello comment tooimplement ce modèle :  

* Votre conception prend en charge les autres méthodes que votre application utilisera les données de salutation telles que la recherche des entités spécifiques, en liaison avec d’autres données, ou générer des informations d’agrégation ?  
* Votre conception évite-t-elle les zones sensibles lorsque vous insérez de nouvelles entités ?  
* Attendez un délai, si vous souhaitez tooreuse hello même nom de la table après sa suppression. Il s’agit d’une meilleure tooalways utiliser des noms de table unique.  
* Prévoyez une limitation lorsque vous utilisez tout d’abord une nouvelle table tandis que hello service de Table apprend les modèles d’accès hello et distribue les partitions de hello entre les nœuds. Vous devez envisager la fréquence à laquelle vous avez besoin de toocreate nouvelles tables.  

#### <a name="when-toouse-this-pattern"></a>Lorsque toouse ce modèle
Utilisez ce modèle lorsque vous avez un grand nombre d’entités que vous devez supprimer à hello même temps.  

#### <a name="related-patterns-and-guidance"></a>Conseils et modèles connexes
Hello suivantes des modèles et des instructions peuvent également être intéressant lorsque vous implémentez ce modèle :  

* [Transactions de groupe d’entités](#entity-group-transactions)
* [Modification des entités](#modifying-entities)  

### <a name="data-series-pattern"></a>Modèle de série de données
Série de données complète de magasin seule entité toominimize hello de plusieurs demandes.  

#### <a name="context-and-problem"></a>Contexte et problème
Un scénario courant consiste pour une application toostore une série de données qu’elle nécessite généralement tooretrieve tous en même temps. Par exemple, votre application peut enregistrer les messages de messagerie instantanée combien chaque employé envoie toutes les heures et ensuite utiliser cette tooplot informations envoyée par chaque utilisateur sur le nombre de messages hello 24 heures précédentes. Un modèle peut être toostore des 24 entités pour chaque employé :  

![][22]

Grâce à cette conception, vous pouvez facilement localiser et hello entité tooupdate de mettre à jour pour chaque employé chaque fois que la valeur du nombre de messages hello tooupdate a besoin d’application hello. Toutefois, tooretrieve hello informations tooplot un graphique de l’activité hello de hello 24 heures précédentes, vous devez récupérer des 24 entités.  

#### <a name="solution"></a>Solution
Utilisez hello suivant de modèle avec un nombre de messages hello toostore propriété distinct pour chaque heure :  

![][23]

Grâce à cette conception, vous pouvez utiliser un nombre de messages de fusion opération tooupdate hello pour un employé pour une heure spécifique. Maintenant, vous pouvez récupérer toutes les informations de hello vous avez besoin de graphique de hello tooplot à l’aide d’une requête pour une entité unique.  

#### <a name="issues-and-considerations"></a>Problèmes et considérations
Prendre en compte les points suivants lorsque vous décidez de hello comment tooimplement ce modèle :  

* Si votre série de données complète n’est pas adaptée à une seule entité (une entité peut avoir des propriétés de too252), utilisez un autre magasin de données comme un objet blob.  
* Si vous avez plusieurs clients simultanément mise à jour d’une entité, vous devez toouse hello **ETag** tooimplement l’accès concurrentiel optimiste. Si vous avez de nombreux clients, vous pouvez rencontrer une contention élevée.  

#### <a name="when-toouse-this-pattern"></a>Lorsque toouse ce modèle
Utilisez ce modèle lorsque vous avez besoin de tooupdate et récupérer une série de données associée à une entité individuelle.  

#### <a name="related-patterns-and-guidance"></a>Conseils et modèles connexes
Hello suivantes des modèles et des instructions peuvent également être intéressant lorsque vous implémentez ce modèle :  

* [Modèle d'entités volumineuses](#large-entities-pattern)  
* [Fusion ou remplacement](#merge-or-replace)  
* [Modèle de transactions cohérente](#eventually-consistent-transactions-pattern) (si vous stockez des séries de données hello dans un objet blob)  

### <a name="wide-entities-pattern"></a>Modèle d’entités larges
Utiliser des entités logiques plusieurs entités physiques toostore avec plus de 252 propriétés.  

#### <a name="context-and-problem"></a>Contexte et problème
Une entité individuelle peut avoir des propriétés, pas plus de 252 (à l’exception des propriétés du système obligatoire hello) et ne peut pas stocker plus de 1 Mo de données au total. Dans une base de données relationnelle, vous obtiendrez en général arrondit les limites de taille hello d’une ligne par ajout d’une nouvelle table et application d’une relation 1 à 1 entre eux.  

#### <a name="solution"></a>Solution
À l’aide du service de Table hello, vous pouvez stocker plusieurs entités toorepresent un objet unique grandes entreprises avec plus de 252 propriétés. Par exemple, si vous souhaitez toostore nombre hello de messages de messagerie instantanée envoyées par chaque employé pour hello cours des 365 derniers jours, vous pouvez utiliser hello suivant le modèle qui utilise deux entités avec des schémas différents :  

![][24]

Si vous avez besoin de toomake une modification qui nécessite la mise à jour à la fois tookeep entités les synchronisés entre eux, vous pouvez utiliser un EGT. Sinon, vous pouvez utiliser un nombre de messages de fusion unique opération tooupdate hello pour un jour spécifique. tooretrieve tous hello des données pour un employé individuel, vous devez récupérer les deux entités, vous pouvez faire avec deux demandes efficace qui utilisent à la fois un **PartitionKey** et un **RowKey** valeur.  

#### <a name="issues-and-considerations"></a>Problèmes et considérations
Prendre en compte les points suivants lorsque vous décidez de hello comment tooimplement ce modèle :  

* La récupération d’une entité logique complète implique au moins deux transactions de stockage : entité physique d’un tooretrieve chaque.  

#### <a name="when-toouse-this-pattern"></a>Lorsque toouse ce modèle
Utilisez ce modèle lorsque le service de Table besoin toostore les entités dont la taille ou le nombre de propriétés dépasse les limites de hello pour une entité individuelle dans hello.  

#### <a name="related-patterns-and-guidance"></a>Conseils et modèles connexes
Hello suivantes des modèles et des instructions peuvent également être intéressant lorsque vous implémentez ce modèle :  

* [Transactions de groupe d’entités](#entity-group-transactions)
* [Fusion ou remplacement](#merge-or-replace)

### <a name="large-entities-pattern"></a>Modèle d’entités volumineuses
Utiliser les valeurs de propriété volumineux de toostore de stockage blob.  

#### <a name="context-and-problem"></a>Contexte et problème
Une entité individuelle ne peut pas stocker plus de 1 Mo de données au total. Si une ou plusieurs des propriétés de stockent des valeurs qui provoquent de taille totale de hello de votre entité de tooexceed cette valeur, vous ne peut pas stocker l’entité toute entière de hello Bonjour service de Table.  

#### <a name="solution"></a>Solution
Si votre entité dépasse 1 Mo la taille, car une ou plusieurs propriétés contiennent une grande quantité de données, vous pouvez stocker des données dans hello service Blob et adresse hello d’objet blob de hello puis à stocker dans une propriété d’entité de hello. Par exemple, vous pouvez stocker des photos hello d’un employé dans le stockage blob et stocker des photos toohello lien Bonjour **Photo** propriété de votre entité employee :  

![][25]

#### <a name="issues-and-considerations"></a>Problèmes et considérations
Prendre en compte les points suivants lorsque vous décidez de hello comment tooimplement ce modèle :  

* toomaintain la cohérence éventuelle entre entité hello Bonjour service de Table et les données de hello Bonjour service Blob, utilisez hello [modèle de transactions cohérente](#eventually-consistent-transactions-pattern) toomaintain vos entités.
* La récupération d’une entité complète implique au moins deux transactions de stockage : une entité de hello tooretrieve et un tooretrieve hello des données blob.  

#### <a name="when-toouse-this-pattern"></a>Lorsque toouse ce modèle
Utilisez ce modèle lorsque vous avez besoin d’entités toostore dont la taille dépasse les limites de hello pour une entité individuelle dans le service de Table hello.  

#### <a name="related-patterns-and-guidance"></a>Conseils et modèles connexes
Hello suivantes des modèles et des instructions peuvent également être intéressant lorsque vous implémentez ce modèle :  

* [Modèle de transactions cohérentes](#eventually-consistent-transactions-pattern)  
* [Modèle d’entités larges](#wide-entities-pattern)

<a name="prepend-append-anti-pattern"></a>

### <a name="prependappend-anti-pattern"></a>Ajouter un anti-modèle ou un préfixe d'anti-modèle
Augmenter l’évolutivité lorsque vous avez un nombre important d’insertions en répartissant les insertions de hello sur plusieurs partitions.  

#### <a name="context-and-problem"></a>Contexte et problème
Ajoutant au début ou de l’ajout des entités de tooyour stockée d’entités en général des résultats dans une application hello Ajout de nouvelles entités toohello tout d’abord ou la dernière partition d’une séquence de partitions. Dans ce cas, toutes les insertions hello à un moment donné sont se produisent dans la même partition, la création d’un point d’accès qui empêche l’équilibrage de charge de service de table hello insère entre plusieurs nœuds de hello et éventuellement à l’origine de votre l’évolutivité des applications toohit hello cibles pour la partition. Par exemple, si vous avez une application d’accès réseau de journaux et les ressources par les employés, peut entraîner une structure d’entité comme indiqué ci-dessous hello partition de heure actuelle devenir une zone réactive si volume hello de transactions atteint cible d’évolutivité hello pour une partition individuelle :  

![][26]

#### <a name="solution"></a>Solution
Hello structure autre entité suivante permet d’éviter une zone réactive de n’importe quelle partition particulière en tant qu’événements de journaux d’application hello :  

![][27]

Notez avec cet exemple, comment les deux hello **PartitionKey** et **RowKey** sont des clés composées. Hello **PartitionKey** utilise le service de hello et journalisation de hello employee id toodistribute sur plusieurs partitions.  

#### <a name="issues-and-considerations"></a>Problèmes et considérations
Prendre en compte les points suivants lorsque vous décidez de hello comment tooimplement ce modèle :  

* Permet de votre application cliente a hello autre structure de clés qui vous évite de créer des partitions à chaud lors des insertions efficacement en charge les requêtes hello ?  
* Votre volume escompté des transactions signifie que vous tooreach susceptible d’objectifs d’évolutivité hello pour une partition individuelle et être limitée par le service de stockage hello ?  

#### <a name="when-toouse-this-pattern"></a>Lorsque toouse ce modèle
Évitez anti-modèle ajouter/ajouter hello lorsque votre volume de transactions est probablement tooresult de limitation par le service de stockage hello lorsque vous accédez à une partition à chaud.  

#### <a name="related-patterns-and-guidance"></a>Conseils et modèles connexes
Hello suivantes des modèles et des instructions peuvent également être intéressant lorsque vous implémentez ce modèle :  

* [Modèle de clé composée](#compound-key-pattern)  
* [Modèle de fin de journal](#log-tail-pattern)  
* [Modification des entités](#modifying-entities)  

### <a name="log-data-anti-pattern"></a>Journalisation de l'anti-modèle de données
En règle générale, vous devez utiliser hello service Blob au lieu de hello données du journal toostore Table service.  

#### <a name="context-and-problem"></a>Contexte et problème
Cas d’utilisation commun pour les données de journal sont tooretrieve une sélection d’entrées de journal pour une plage de date/heure spécifique : par exemple, vous souhaitez toofind tous hello erreur et messages critiques que votre application connectée entre 15:04 et 15:06 à une date spécifique. Vous ne souhaitez pas toouse hello date et heure hello message toodetermine hello partition des journaux vous enregistrez le journal des entités à : que les résultats dans une partition à chaud, car le partagent à un moment donné, toutes les entités de journal hello hello même **PartitionKey** valeur (consultez la section de hello [ajoutez/ajouter l’anti-modèle](#prepend-append-anti-pattern)). Par exemple, hello suivant le schéma de l’entité pour un message du journal des résultats dans une partition à chaud comme application hello écrit les messages du journal partition toohello pour hello date et heure :  

![][28]

Dans cet exemple, hello **RowKey** inclut hello date et heure tooensure de message de journal hello que les messages du journal sont stockés triées par ordre de date/heure et un id de message au cas où plusieurs messages de journal partagent hello mêmes date et heure.  

Une autre approche consiste à toouse un **PartitionKey** qui garantit que l’application hello écrit des messages dans une plage de partitions. Par exemple, si la source hello du message de journal hello fournit un toodistribute moyen des messages entre ces partitions, vous pouvez utiliser hello suivant le schéma de l’entité :  

![][29]

Toutefois, le problème hello avec ce schéma est que tooretrieve tous hello des messages de journal pour un intervalle de temps spécifique, vous devez rechercher chaque partition dans la table de hello.

#### <a name="solution"></a>Solution
Hello précédente section hello en surbrillance d’un problème de la tentative de toouse hello des entrées de journal de Table service toostore et deux satisfaisante suggéré, conçoit. Une solution conduite tooa de partition à chaud avec risque de hello de performances de l’écriture de messages de journal ; Hello autre solution a entraîné médiocrité des performances en raison de hello exigence tooscan chaque partition dans les messages de journal hello table tooretrieve pour un intervalle de temps spécifique. Stockage d’objets BLOB offre une meilleure solution pour ce type de scénario et Voici comment Azure stockage Analytique magasins hello données de journalisation.  

Cette section décrit comment Analytique de stockage stocke des données de journal dans le stockage d’objets blob en guise d’illustration de ces données toostoring approche qui généralement d’une requête par plage.  

Storage Analytics stocke les messages de journalisation dans un format délimité dans plusieurs objets blob. format délimité de Hello facilite pour un client de données d’application tooparse hello dans le message du journal hello.  

Stockage Analytique utilise une convention d’affectation de noms pour les objets BLOB qui vous permet de toolocate hello blob (ou des objets BLOB) qui contiennent des messages de journal hello que vous recherchez. Par exemple, un objet blob nommé « queue/2014/07/31/1800/000001.log » contient des messages du journal qui concernent le service de file d’attente toohello heure hello en commençant à 18:00 31 juillet 2014. Hello « 000001 » indique qu’il s’agit du journal première hello pour cette période. Analytique de stockage enregistre également les horodatages hello Hello premier et dernier journal des messages stockés dans le fichier de hello dans le cadre des métadonnées d’objet blob hello. Hello API pour permet de stockage d’objets blob vous recherchez des objets BLOB dans un conteneur selon un préfixe de nom : toolocate tous les objets BLOB hello qui contiennent la file d’attente les données du journal pour les heures hello en commençant à 18:00, vous pouvez utiliser hello préfixe « file d’attente/2014/07/31/1800. »  

Stockage Analytique met en mémoire tampon des messages de journal en interne et met à jour périodiquement les blob approprié hello ou crée un nouveau avec le dernier lot de hello des entrées de journal. Cela réduit le nombre de hello d’écritures, il doit effectuer toohello service d’objets blob.  

Si vous implémentez une solution similaire dans votre propre application, vous devez considérer comment toomanage hello compromis entre la fiabilité (écriture de chaque stockage tooblob de journal d’entrée lors de sa réalisation) et de coût et d’évolutivité (mise en mémoire tampon des mises à jour dans votre application et les écrire tooblob stockage dans des lots).  

#### <a name="issues-and-considerations"></a>Problèmes et considérations
Tenez compte des points suivants lorsque vous décidez comment toostore enregistrer les données de hello :  

* Si vous créez une conception de table qui évite les partitions sensibles potentielles, il est possible que l'accès aux données de journalisation ne soit pas très efficace.  
* tooprocess les données du journal, un client doit souvent tooload nombre d’enregistrements.  
* Bien que les données de journalisation soient souvent structurées, le stockage d'objets blob peut être une meilleure solution.  

### <a name="implementation-considerations"></a>Considérations relatives à l'implémentation
Cette section décrit certaines des toobear de considérations hello à l’esprit lorsque vous implémentez les modèles hello décrits dans les sections précédentes hello. La plupart de cette section utilise des exemples écrits en c# qui utilisent la bibliothèque cliente de stockage (version 4.3.0 lors de l’écriture hello) de hello.  

### <a name="retrieving-entities"></a>Récupération des entités
Comme indiqué dans la section de hello [conception pour l’interrogation](#design-for-querying), requête plus efficace de hello est une requête de point. Toutefois, dans certains cas vous devrez peut-être tooretrieve plusieurs entités. Cette section décrit certaines entités de tooretrieving approches courantes à l’aide de la bibliothèque cliente de stockage de hello.  

#### <a name="executing-a-point-query-using-hello-storage-client-library"></a>Exécution d’une requête de point à l’aide de la bibliothèque cliente de stockage de hello
tooexecute de façon plus simple Hello une requête de point est toouse hello **récupérer** opération de table comme indiqué dans hello suivant extrait de code c# qui Récupère une entité avec une **PartitionKey** de valeur « ventes » et un  **RowKey** de valeur « 212 » :  

```csharp
TableOperation retrieveOperation = TableOperation.Retrieve<EmployeeEntity>("Sales", "212");
var retrieveResult = employeeTable.Execute(retrieveOperation);
if (retrieveResult.Result != null)
{
    EmployeeEntity employee = (EmployeeEntity)retrieveResult.Result;
    ...
}  
```

Notez la façon dont cet exemple attend les entités hello il récupère toobe de type **EmployeeEntity**.  

#### <a name="retrieving-multiple-entities-using-linq"></a>Récupération de plusieurs entités à l’aide de LINQ
Vous pouvez extraire plusieurs entités à l’aide de LINQ avec la bibliothèque cliente de stockage et en spécifiant une requête avec une clause **where** . tooavoid une analyse de table, vous devez toujours inclure hello **PartitionKey** valeur Bonjour où clause et si possible hello **RowKey** tooavoid les analyses de table et de partition de valeur. Hello service table prend en charge un ensemble limité de toouse de (supérieur à, supérieur ou égal à, inférieur à, inférieur ou égal, égal et n’est pas égal) d’opérateurs de comparaison dans hello où clause. Hello extrait de code c# suivant recherche tous les employés hello dont le nom commence par « B » (en supposant que hello **RowKey** magasins hello nom) dans le service commercial hello (en supposant que hello **PartitionKey** magasins hello nom du service) :  

```csharp
TableQuery<EmployeeEntity> employeeQuery = employeeTable.CreateQuery<EmployeeEntity>();
var query = (from employee in employeeQuery
            where employee.PartitionKey == "Sales" &&
            employee.RowKey.CompareTo("B") >= 0 &&
            employee.RowKey.CompareTo("C") < 0
            select employee).AsTableQuery();
var employees = query.Execute();  
```

Notez la façon dont les requêtes hello spécifie à la fois un **RowKey** et un **PartitionKey** tooensure de meilleur performances.  

Hello exemple de code suivant montre une fonctionnalité équivalente à l’aide des API fluent de hello (pour plus d’informations sur l’API fluent en général, consultez [meilleures pratiques pour la conception d’une API Fluent](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)) :  

```csharp
TableQuery<EmployeeEntity> employeeQuery = new TableQuery<EmployeeEntity>().Where(
    TableQuery.CombineFilters(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition(
    "PartitionKey", QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.GenerateFilterCondition(
    "RowKey", QueryComparisons.GreaterThanOrEqual, "B")
),
TableOperators.And,
TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "C")
    )
);
var employees = employeeTable.ExecuteQuery(employeeQuery);  
```

> [!NOTE]
> exemple Hello imbrique plusieurs **CombineFilters** tooinclude de méthodes hello trois conditions de filtre.  
> 
> 

#### <a name="retrieving-large-numbers-of-entities-from-a-query"></a>Récupération d'un grand nombre d'entités à partir d'une requête
Une requête optimale renvoie une entité individuelle basée sur une valeur de **PartitionKey** et une valeur de **RowKey**. Toutefois, dans certains scénarios vous avez peut-être un tooreturn exigence d’entités à partir de hello même partition ou même à partir de plusieurs partitions.  

Vous devez toujours entièrement tester les performances de hello de votre application dans de tels scénarios.  

Une requête sur le service de table hello peut renvoyer un maximum de 1 000 entités à la fois et peut s’exécuter pendant un maximum de cinq secondes. Si le jeu de résultats hello contient plus de 1 000 entités, si la requête de hello ne s’est pas terminée dans les cinq secondes, ou si la requête de hello dépasse la limite de partition hello, hello service Table renvoie un tooenable de jeton de continuation hello messages hello du client application toorequest ensemble suivant d’entités. Pour plus d’informations sur la façon dont fonctionnent les jetons de continuation, consultez [Délai de requête et pagination](http://msdn.microsoft.com/library/azure/dd135718.aspx).  

Si vous utilisez hello bibliothèque cliente de stockage, il peut gérer automatiquement les jetons de continuation pour vous qu’elle retourne des entités à partir de hello service de Table. Hello c# exemple de code suivant à l’aide de hello bibliothèque cliente de stockage automatiquement gère les jetons de continuation si le service de table hello les retourne dans une réponse :  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

var employees = employeeTable.ExecuteQuery(employeeQuery);
foreach (var emp in employees)
{
        ...
}  
```

Hello suivant de code c# gère les jetons de continuation explicitement :  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

TableContinuationToken continuationToken = null;

do
{
        var employees = employeeTable.ExecuteQuerySegmented(
        employeeQuery, continuationToken);
    foreach (var emp in employees)
    {
    ...
    }
    continuationToken = employees.ContinuationToken;
} while (continuationToken != null);  
```

À l’aide de jetons de continuation explicitement, vous pouvez contrôler quand votre application récupère le segment suivant de hello de données. Par exemple, si votre application cliente Active toopage les utilisateurs par le biais des entités hello stockées dans une table, un utilisateur peut décider pas toopage via toutes les entités hello hello requête extrait votre application uniquement utiliserait un Bonjour tooretrieve de jeton de continuation suivant segment lors de l’utilisateur de hello a fini de pagination de toutes les entités hello dans le segment actuel de hello. Cette approche présente plusieurs avantages :  

* Il vous permet de durée hello toolimit tooretrieve de données à partir de hello service de Table et que vous déplacez réseau hello.  
* Il permet de vous tooperform e/s asynchrone dans .NET.  
* Il vous permet le stockage de jeton toopersistent tooserialize hello continuation pour pouvoir continuer dans les cas de hello d’incident d’application.  

> [!NOTE]
> En général, un jeton de liaison retourne un segment contenant 1 000 entités, bien qu'il puisse y en avoir moins. C’est également hello cas si vous limitez le nombre de hello d’une requête retourne à l’aide des entrées **prendre** tooreturn hello première n entités qui correspondent à vos critères de recherche : service de table hello peut retourner un segment contenant moins de n entités le long avec un tooenable de jeton de continuation vous tooretrieve hello autres entités.  
> 
> 

Hello code c# suivant montre comment le nombre de hello toomodify d’entités retournées à l’intérieur d’un segment :  

```csharp
employeeQuery.TakeCount = 50;  
```

#### <a name="server-side-projection"></a>Projection côté serveur
Une seule entité too255 propriétés et d’être up too1 Mo. Lorsque vous interrogez la table de hello et récupérer des entités, vous devrez peut-être pas toutes les propriétés de hello et peut éviter le transfert de données inutilement (toohelp réduire la latence et coût). Vous pouvez utiliser les propriétés de hello simplement de tootransfer de projection du côté serveur, que vous avez besoin. Bonjour exemple suivant est extrait simplement hello **messagerie** propriété (avec **PartitionKey**, **RowKey**, **Timestamp**et  **ETag**) à partir des entités hello sélectionnées par la requête de hello.  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
List<string> columns = new List<string>() { "Email" };
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter).Select(columns);

var entities = employeeTable.ExecuteQuery(employeeQuery);
foreach (var e in entities)
{
        Console.WriteLine("RowKey: {0}, EmployeeEmail: {1}", e.RowKey, e.Email);
}  
```

Notez comment hello **RowKey** valeur est disponible même si elle ne figurait pas dans la liste hello des propriétés tooretrieve.  

### <a name="modifying-entities"></a>Modification des entités
Hello bibliothèque cliente de stockage permet toomodify vos entités stockées dans le service de table hello par l’insertion, la suppression et la mise à jour des entités. Vous pouvez utiliser EGTs toobatch plusieurs insert, update et delete opérations nombre de hello tooreduce ensemble d’allers-retours requis et améliorer les performances de hello de votre solution.  

Notez que les exceptions levées lorsque hello bibliothèque cliente de stockage s’exécute en général un EGT incluent des index hello d’entité hello hello lot toofail à l’origine. Cela est utile lorsque vous déboguez du code qui utilise des EGT.  

Nous vous conseillons de réfléchir également à la façon dont votre conception affecte la méthode de votre application cliente pour gérer les opérations d'accès concurrentiel et de mises à jour.  

#### <a name="managing-concurrency"></a>Gérer l'accès concurrentiel
Par défaut, le service de table hello implémente optimiste de contrôle d’accès concurrentiel au niveau de hello d’entités individuelles pour **insérer**, **fusion**, et **supprimer** opérations, Bien qu’il soit possible pour un Bonjour tooforce de client de service toobypass table ces vérifications. Pour plus d’informations sur la manière dont service de table hello gère l’accès concurrentiel, consultez [la gestion de l’accès concurrentiel dans Microsoft Azure Storage](storage-concurrency.md).  

#### <a name="merge-or-replace"></a>Fusion ou remplacement
Hello **remplacer** méthode Hello **TableOperation** classe remplace toujours l’entité complète de hello Bonjour service de Table. Si vous n’incluez pas une propriété dans la demande hello lorsque cette propriété existe dans l’entité de stockée hello, demande de hello supprime que la propriété à partir de hello stockées entité. Sauf si vous souhaitez tooremove une propriété explicitement à partir d’une entité stockée, vous devez inclure chaque propriété dans la demande hello.  

Vous pouvez utiliser hello **fusion** méthode Hello **TableOperation** classe tooreduce hello quantité des données que vous envoyez service de Table toohello lorsque vous souhaitez tooupdate une entité. Hello **fusion** méthode remplace toutes les propriétés de l’entité de hello stockée avec les valeurs de propriété d’entité hello inclus dans la demande de hello, mais laisse intactes toutes les propriétés de hello stockées entité qui ne sont pas inclus dans la demande hello. Cela est utile si vous avez entités volumineuses, il vous suffit de tooupdate un petit nombre de propriétés dans une demande.  

> [!NOTE]
> Hello **remplacer** et **fusion** méthodes échouent si hello entité n’existe pas. En guise d’alternative, vous pouvez utiliser hello **InsertOrReplace** et **InsertOrMerge** des méthodes qui créent une nouvelle entité si elle n’existe pas.  
> 
> 

### <a name="working-with-heterogeneous-entity-types"></a>Utilisation des types d’entités hétérogènes
Hello service de Table est un *sans schéma* magasin de tables qui signifie qu’une seule table peut stocker des entités de plusieurs types en fournissant une grande souplesse dans votre conception. Hello exemple suivant illustre une table qui stocke les entités de service et de l’employé :  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

Notez que chaque entité doit toujours avoir les valeurs **PartitionKey**, **RowKey** et **Timestamp**, mais elle peut aussi avoir n’importe quel ensemble de propriétés. En outre, aucune est tooindicate hello de type d’une entité, sauf si vous choisissez toostore ces informations quelque part. Il existe deux options pour identifier le type d’entité hello :  

* Ajouter toohello de type d’entité hello **RowKey** (ou éventuellement hello **PartitionKey**). Par exemple, **EMPLOYEE_000123** ou **DEPARTMENT_SALES** en tant que valeurs de **RowKey**.  
* Utilisez un type d’entité propriété distinct toorecord hello comme indiqué dans le tableau hello ci-dessous.  

<table>
<tr>
<th>PartitionKey</th>
<th>RowKey</th>
<th>Timestamp</th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EventType</th>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td>Employee</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EntityType</th>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td>Employee</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EventType</th>
<th>DepartmentName</th>
<th>EmployeeCount</th>
</tr>
<tr>
<td>department</td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th>EventType</th>
<th>FirstName</th>
<th>LastName</th>
<th>Age</th>
<th>Email</th>
</tr>
<tr>
<td>Employee</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

première option Hello, ajoutant hello entité type toohello **RowKey**, est utile s’il existe un risque que les deux entités de types différents peuvent avoir hello même valeur de clé. Il regroupe également des entités de hello même type ensemble dans la partition de hello.  

Hello techniques présentées dans cette section sont particulièrement toohello discussion [des relations d’héritage](#inheritance-relationships) plus haut dans ce guide dans la section de hello [modélisation relations](#modelling-relationships).  

> [!NOTE]
> Vous devez envisager d’inclure un numéro de version dans hello entité type valeur tooenable client applications tooevolve POCO des objets et travailler avec des versions différentes.  
> 
> 

Hello reste de cette section décrit certaines des fonctionnalités hello Bonjour bibliothèque cliente de stockage qui facilitent l’utilisation de plusieurs types d’entités Bonjour, même table.  

#### <a name="retrieving-heterogeneous-entity-types"></a>Récupération de types d'entités hétérogènes
Si vous utilisez hello bibliothèque cliente de stockage, vous avez trois options pour travailler avec plusieurs types d’entités.  

Si vous connaissez le type hello d’entité hello stockée avec un spécifique **RowKey** et **PartitionKey** valeurs, vous pouvez spécifier le type d’entité hello lorsque vous récupérez une entité de hello comme indiqué dans les exemples hello deux précédents pour récupérer les entités de type **EmployeeEntity**: [l’exécution d’une requête de point à l’aide de la bibliothèque cliente de stockage de hello](#executing-a-point-query-using-the-storage-client-library) et [la récupération de plusieurs entités à l’aide de LINQ](#retrieving-multiple-entities-using-linq).  

deuxième option de Hello est toouse hello **DynamicTableEntity** type (un sac de propriétés) au lieu d’un type d’entité POCO concrète (cette option peut également améliorer les performances, car il n’existe aucun besoin tooserialize et désérialiser les entités hello trop. Types de réseau). Hello suivant le code c# potentiellement récupère plusieurs entités de différents types de table de hello, mais retourne toutes les entités en tant que **DynamicTableEntity** instances. Il utilise ensuite hello **EntityType** type hello toodetermine de chaque entité :  

```csharp
string filter = TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("PartitionKey",
    QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("RowKey",
                    QueryComparisons.GreaterThanOrEqual, "B"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey",
        QueryComparisons.LessThan, "F")
    )
);
TableQuery<DynamicTableEntity> entityQuery =
    new TableQuery<DynamicTableEntity>().Where(filter);
var employees = employeeTable.ExecuteQuery(entityQuery);

IEnumerable<DynamicTableEntity> entities = employeeTable.ExecuteQuery(entityQuery);
foreach (var e in entities)
{
EntityProperty entityTypeProperty;
if (e.Properties.TryGetValue("EntityType", out entityTypeProperty))
{
    if (entityTypeProperty.StringValue == "Employee")
    {
        // Use entityTypeProperty, RowKey, PartitionKey, Etag, and Timestamp
        }
    }
}  
```

Notez que tooretrieve autres propriétés que vous devez utiliser hello **TryGetValue** méthode sur hello **propriétés** propriété Hello **DynamicTableEntity** classe.  

Une troisième option est toocombine à l’aide de hello **DynamicTableEntity** type et un **EntityResolver** instance. Cela vous permet de tooresolve toomultiple POCO types Bonjour même requête. Dans cet exemple, hello **EntityResolver** délégué à l’aide de hello **EntityType** toodistinguish de propriété entre types hello deux d’entité qui hello requête retourne. Hello **résoudre** méthode utilise hello **résolveur** déléguer tooresolve **DynamicTableEntity** trop d’instances**TableEntity** instances.  

```csharp
EntityResolver<TableEntity> resolver = (pk, rk, ts, props, etag) =>
{

        TableEntity resolvedEntity = null;
        if (props["EntityType"].StringValue == "Department")
        {
        resolvedEntity = new DepartmentEntity();
        }
        else if (props["EntityType"].StringValue == "Employee")
        {
        resolvedEntity = new EmployeeEntity();
        }
        else throw new ArgumentException("Unrecognized entity", "props");

        resolvedEntity.PartitionKey = pk;
        resolvedEntity.RowKey = rk;
        resolvedEntity.Timestamp = ts;
        resolvedEntity.ETag = etag;
        resolvedEntity.ReadEntity(props, null);
        return resolvedEntity;
};

string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<DynamicTableEntity> entityQuery =
        new TableQuery<DynamicTableEntity>().Where(filter);

var entities = employeeTable.ExecuteQuery(entityQuery, resolver);
foreach (var e in entities)
{
        if (e is DepartmentEntity)
        {
    ...
        }
        if (e is EmployeeEntity)
        {
    ...
        }
}  
```

#### <a name="modifying-heterogeneous-entity-types"></a>Modification des types d'entités hétérogènes
Il est inutile type hello de tooknow d’une entité de toodelete vous savez toujours de type hello d’une entité lorsque vous insérez. Toutefois, vous pouvez utiliser **DynamicTableEntity** tooupdate une entité de type sans connaître son type et sans l’aide d’une classe d’entité POCO. Hello exemple de code suivant récupère une entité unique et vérifie hello **EmployeeCount** propriété existe avant la mise à jour.  

```csharp
TableResult result =
        employeeTable.Execute(TableOperation.Retrieve(partitionKey, rowKey));
DynamicTableEntity department = (DynamicTableEntity)result.Result;

EntityProperty countProperty;

if (!department.Properties.TryGetValue("EmployeeCount", out countProperty))
{
        throw new
        InvalidOperationException("Invalid entity, EmployeeCount property not found.");
}
countProperty.Int32Value += 1;
employeeTable.Execute(TableOperation.Merge(department));  
```

### <a name="controlling-access-with-shared-access-signatures"></a>Contrôle d’accès avec des signatures d’accès partagé
Vous pouvez utiliser la Signature d’accès partagé (SAS) jetons tooenable client applications toomodify (et interroger) les entités de table directement sans tooauthenticate besoin de hello directement avec le service de table hello. En règle générale, il existe des trois principaux avantages toousing SAP dans votre application :  

* Vous n’avez pas besoin de toodistribute votre stockage compte tooan clé de plateforme sécurisée (par exemple, un appareil mobile) dans l’ordre tooallow tooaccess de cet appareil et modifier des entités Bonjour service de Table.  
* Vous pouvez décharger certaines tâches de travail de hello ce site web et exécutent des rôles de travail dans la gestion de vos appareils de tooclient des entités telles que les ordinateurs des utilisateurs finaux et les appareils mobiles.  
* Vous pouvez affecter une contrainte et temps limité d’ensemble du client de tooa autorisations (par exemple, pour autoriser l’accès en lecture seule toospecific ressources).  

Pour plus d’informations sur l’utilisation de jetons SAP avec hello service de Table, consultez [à l’aide de Signatures SAP (accès partagé)](storage-dotnet-shared-access-signature-part-1.md).  

Toutefois, vous devez toujours générer des jetons SAP hello qui accordent un client application toohello entités hello service de table : vous devez le faire dans un environnement qui a sécuriser l’accès aux clés de compte de stockage tooyour. En règle générale, vous utilisez un web ou travail rôle toogenerate hello SAS des jetons et remettre les applications clientes toohello qui doivent accéder à des entités de tooyour. Car il existe toujours une surcharge impliquées dans la génération et de distribution tooclients de jetons SAS, vous devez envisager la meilleure façon tooreduce cette surcharge, surtout dans les scénarios de haut volume.  

Il est possible de toogenerate un jeton SAP qu’accorde accéder au sous-ensemble tooa d’entités hello dans une table. Par défaut, vous créez un jeton SAP pour une table entière, mais il est également possible de toospecify que tooeither d’accès de jeton grant hello SAS une plage de **PartitionKey** valeurs ou une plage de **PartitionKey** et  **RowKey** valeurs. Vous pouvez choisir toogenerate jetons SAP pour les utilisateurs individuels de votre système de telle sorte que chaque jeton d’utilisateur SAP ne lui permet d’accéder tootheir des entités propre Bonjour service de table.  

### <a name="asynchronous-and-parallel-operations"></a>Opérations asynchrones et parallèles
Si vous effectuez la diffusion de vos demandes sur plusieurs partitions, vous pouvez améliorer le débit et la réactivité du client en utilisant des requêtes asynchrones ou parallèles.
Par exemple, vous pouvez avoir plusieurs instances de rôle de travail accédant à vos tables en parallèle. Vous pouvez disposer de rôles de travail individuels responsables des ensembles particuliers de partitions, ou tout simplement avoir plusieurs instances de rôle de travail, chaque tooaccess en mesure de tous les hello partitions dans une table.  

Dans une instance cliente, vous pouvez améliorer le débit en exécutant des opérations de stockage en mode asynchrone. Hello bibliothèque cliente de stockage permet de modifications et toowrite facilement des requêtes asynchrones. Par exemple, vous pouvez commencer avec une méthode synchrone hello qui Récupère toutes les entités hello dans une partition comme indiqué dans hello suivant de code c# :  

```csharp
private static void ManyEntitiesQuery(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

        TableContinuationToken continuationToken = null;

        do
        {
        var employees = employeeTable.ExecuteQuerySegmented(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
    {
        ...
    }
        continuationToken = employees.ContinuationToken;
        } while (continuationToken != null);
}  
```

Vous pouvez facilement modifier ce code pour cette requête hello s’exécute de façon asynchrone, comme suit :  

```csharp
private static async Task ManyEntitiesQueryAsync(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);
        TableContinuationToken continuationToken = null;

        do
        {
        var employees = await employeeTable.ExecuteQuerySegmentedAsync(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
        {
            ...
        }
        continuationToken = employees.ContinuationToken;
            } while (continuationToken != null);
}  
```

Dans cet exemple asynchrone, vous pouvez voir les suivant hello change à partir de la version synchrone de hello :  

* signature de méthode Hello inclut désormais hello **async** modificateur et retourne un **tâche** instance.  
* Au lieu de l’appel hello **ExecuteSegmented** tooretrieve résultats de la méthode, hello méthode maintenant les appels hello **ExecuteSegmentedAsync** hello (méthode) et utilise **await** modificateur tooretrieve résultats de façon asynchrone.  

application cliente de Hello peut appeler cette méthode plusieurs fois (avec des valeurs différentes pour hello **service** paramètre), et chaque requête est exécutée sur un thread distinct.  

Notez qu’il n’existe aucune version asynchrone de hello **Execute** méthode Bonjour **TableQuery** classe car hello **IEnumerable** interface ne prend pas en charge asynchrone énumération.  

Vous pouvez également insérer, mettre à jour et supprimer des entités de façon asynchrone. Hello exemple c# suivant montre une méthode simple et synchrone de tooinsert ou remplace une entité employee :  

```csharp
private static void SimpleEmployeeUpsert(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = employeeTable
        .Execute(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

Vous pouvez facilement modifier ce code afin que la mise à jour hello s’exécute de façon asynchrone, comme suit :  

```csharp
private static async Task SimpleEmployeeUpsertAsync(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = await employeeTable
        .ExecuteAsync(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

Dans cet exemple asynchrone, vous pouvez voir les suivant hello change à partir de la version synchrone de hello :  

* signature de méthode Hello inclut désormais hello **async** modificateur et retourne un **tâche** instance.  
* Au lieu de l’appel hello **Execute** entité de méthode tooupdate hello, hello méthode maintenant les appels hello **ExecuteAsync** hello (méthode) et utilise **await** modificateur tooretrieve résultats de façon asynchrone.  

application cliente de Hello peut appeler plusieurs méthodes asynchrones, telle que celle-ci, et chaque appel de méthode s’exécute sur un thread distinct.  

### <a name="credits"></a>Crédits
Nous aimerions hello toothank suit les membres de l’équipe Azure pour leurs contributions de hello : Dominic Betts, Jason Hogg, Jean Ghanem, Jai Haridas, Jeff Irwin, Vamshidhar Kommineni, Vinay Shah et Serdar Ozler ainsi que Tom Hollander de DX de Microsoft. 

Nous aimerions également hello toothank suivant du MVP Microsoft pour leurs commentaires précieux à Microsoft pendant les cycles de révision : Igor Papirov et Edward Bakker.

[1]: ./media/storage-table-design-guide/storage-table-design-IMAGE01.png
[2]: ./media/storage-table-design-guide/storage-table-design-IMAGE02.png
[3]: ./media/storage-table-design-guide/storage-table-design-IMAGE03.png
[4]: ./media/storage-table-design-guide/storage-table-design-IMAGE04.png
[5]: ./media/storage-table-design-guide/storage-table-design-IMAGE05.png
[6]: ./media/storage-table-design-guide/storage-table-design-IMAGE06.png
[7]: ./media/storage-table-design-guide/storage-table-design-IMAGE07.png
[8]: ./media/storage-table-design-guide/storage-table-design-IMAGE08.png
[9]: ./media/storage-table-design-guide/storage-table-design-IMAGE09.png
[10]: ./media/storage-table-design-guide/storage-table-design-IMAGE10.png
[11]: ./media/storage-table-design-guide/storage-table-design-IMAGE11.png
[12]: ./media/storage-table-design-guide/storage-table-design-IMAGE12.png
[13]: ./media/storage-table-design-guide/storage-table-design-IMAGE13.png
[14]: ./media/storage-table-design-guide/storage-table-design-IMAGE14.png
[15]: ./media/storage-table-design-guide/storage-table-design-IMAGE15.png
[16]: ./media/storage-table-design-guide/storage-table-design-IMAGE16.png
[17]: ./media/storage-table-design-guide/storage-table-design-IMAGE17.png
[18]: ./media/storage-table-design-guide/storage-table-design-IMAGE18.png
[19]: ./media/storage-table-design-guide/storage-table-design-IMAGE19.png
[20]: ./media/storage-table-design-guide/storage-table-design-IMAGE20.png
[21]: ./media/storage-table-design-guide/storage-table-design-IMAGE21.png
[22]: ./media/storage-table-design-guide/storage-table-design-IMAGE22.png
[23]: ./media/storage-table-design-guide/storage-table-design-IMAGE23.png
[24]: ./media/storage-table-design-guide/storage-table-design-IMAGE24.png
[25]: ./media/storage-table-design-guide/storage-table-design-IMAGE25.png
[26]: ./media/storage-table-design-guide/storage-table-design-IMAGE26.png
[27]: ./media/storage-table-design-guide/storage-table-design-IMAGE27.png
[28]: ./media/storage-table-design-guide/storage-table-design-IMAGE28.png
[29]: ./media/storage-table-design-guide/storage-table-design-IMAGE29.png

