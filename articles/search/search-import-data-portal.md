---
title: "données aaaImport dans Azure Search dans le portail de hello | Documents Microsoft"
description: "Utilisez hello Azure recherche Assistant Importer des données dans le portail Azure de hello toocrawl données Azure à partir de la base de données NoSQL Azure Cosmos, stockage Blob, le stockage de table, de la base de données SQL et SQL Server sur des machines virtuelles Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: Azure Portal
ms.assetid: f40fe07a-0536-485d-8dfa-8226eb72e2cd
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 00b0e59594560c0cdaea748df196518e9fba3834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-tooazure-search-using-hello-portal"></a>Importer des données tooAzure recherche à l’aide du portail de hello
Hello portail Azure fournit un **importer des données** Assistant sur le tableau de bord hello Azure Search pour charger les données dans un index. 

  ![Importer des données sur la barre de commandes hello][1]

En interne, Assistant de hello configure et appelle une *indexeur*, automatisation des différentes étapes du processus d’indexation de hello : 

* Connecter la source de données externe tooan Bonjour même abonnement Azure
* Générer un schéma d’index modifiable basé sur la structure de données source hello
* Charger des documents JSON dans un index à l’aide d’un ensemble de lignes récupérée à partir de la source de données hello

Vous pouvez tester ce workflow à l’aide d’exemples de données dans Azure Cosmos DB. Visitez [prise en main Azure Search Bonjour Azure Portal](search-get-started-portal.md) pour obtenir des instructions.

> [!NOTE]
> Vous pouvez lancer hello **importer des données** Assistant à partir de toosimplify de tableau de bord de base de données Azure Cosmos hello l’indexation pour cette source de données. Dans la navigation de gauche, accédez trop**Collections** > **ajouter Azure Search** tooget a démarré.

## <a name="data-sources-supported-by-hello-import-data-wizard"></a>Sources de données pris en charge par hello Assistant Importation de données
Assistant Importer des données de Hello prend en charge hello les sources de données suivantes : 

* Base de données SQL Azure
* Données relationnelles SQL Server sur une machine virtuelle Azure
* Azure Cosmos DB
* Stockage d'objets blob Azure
* Stockage de tables Azure

Un jeu de données aplati est requis. Vous pouvez uniquement effectuer vos importations à partir d’une seule table, vue de base de données ou structure de données équivalente. Vous devez créer cette structure de données avant d’exécuter l’Assistant de hello.

## <a name="connect-tooyour-data"></a>Se connecter aux données tooyour
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) et tableau de bord de service hello ouvert. Vous pouvez cliquer sur **davantage de services** dans hello saut barre toosearch existant « services recherche » dans l’abonnement actif de hello. 
2. Cliquez sur **importer des données** sur le panneau d’importer des données tooslide hello ouvrir de la barre de commandes hello.  
3. Cliquez sur **se connecter aux données tooyour** toospecify une définition de source de données utilisée par un indexeur. Pour les sources de données intra-subscription, hello Assistant peut généralement détecter et lire les informations de connexion, en réduisant les exigences de configuration globales.

|  |  |
| --- | --- |
| **Source de données existante** |Si des indexeurs sont déjà définis dans votre service de recherche, vous pouvez sélectionner une définition de source de données existante pour une autre importation. |
| **Azure SQL Database** |Nom du service, les informations d’identification pour un utilisateur de base de données avec l’autorisation de lecture et un nom de base de données peuvent être spécifiés sur la page de hello ou via une chaîne de connexion ADO.NET. Choisissez tooview d’option de chaîne de connexion hello ou personnaliser les propriétés. <br/><br/>Hello table ou une vue qui fournit l’ensemble de lignes hello doit être spécifié sur la page de hello. Cette option apparaît une fois la connexion de hello réussit, ce qui donne une liste déroulante afin que vous pouvez effectuer une sélection. |
| **SQL Server dans les machines virtuelles Azure** |Spécifiez un nom de service complet, un ID d’utilisateur et un mot de passe, ainsi qu’une base de données pour la chaîne de connexion. toouse cette source de données, vous devez avoir préalablement installé un certificat dans le magasin local hello qui chiffre les connexion hello. Pour obtenir des instructions, consultez [tooAzure de connexion SQL VM recherche](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md). <br/><br/>Hello table ou une vue qui fournit l’ensemble de lignes hello doit être spécifié sur la page de hello. Cette option apparaît une fois la connexion de hello réussit, ce qui donne une liste déroulante afin que vous pouvez effectuer une sélection. |
| **Azure Cosmos DB** |Elles incluent collection, base de données et compte de hello. Tous les documents dans la collection de hello seront inclus dans les index hello. Vous pouvez définir une requête tooflatten ou filtrer l’ensemble de lignes hello ou toodetect modifié des documents pour les opérations d’actualisation des données suivantes. |
| **Stockage Blob Azure** |Conditions préalables incluent le compte de stockage hello et un conteneur. Si vous le souhaitez, si les noms d’objets blob suivent une convention d’affectation de noms virtuelle à des fins de regroupement, vous pouvez spécifier la partie de répertoire virtuel hello du nom de hello en tant que dossier sous le conteneur. Consultez la page [Indexation de Stockage Blob](search-howto-indexing-azure-blob-storage.md) pour plus d’informations. |
| **Stockage de tables Azure** |Elles incluent compte de stockage hello et un nom de table. Si vous le souhaitez, vous pouvez spécifier une requête de tooretrieve un sous-ensemble de tables de hello. Consultez la page [Indexation de Stockage Table](search-howto-indexing-azure-tables.md) pour plus d’informations. |

## <a name="customize-target-index"></a>Personnaliser l’index cible
Un index préliminaire est généralement déduit de hello le jeu de données. Ajouter, modifier ou supprimer un schéma de champs toocomplete hello. En outre, définir les attributs à toodetermine au niveau du champ hello ses comportements de recherche suivantes.

1. Dans **index cible de personnaliser**, spécifiez le nom de hello et un **clé** toouniquely utilisé identifier chaque document. Hello clé doit être une chaîne. Si les valeurs de champ sont des espaces ou des tirets être sûr tooset options avancées dans **importer vos données** toosuppress hello contrôle de validation pour ces caractères.
2. Passez en revue et réviser hello restant de champs. Le nom et le type de champ sont généralement renseignés automatiquement. Vous pouvez modifier le type de données hello jusqu'à ce que les index hello est créé. Si vous souhaitez le modifier par la suite, vous devrez alors le régénérer.
3. Définissez les attributs d’index de chaque champ :
   
   * Récupérable retourne hello champ dans les résultats de la recherche.
   * Filterable permet hello toobe de champ référencé dans les expressions de filtre.
   * Triable permet hello toobe de champ utilisé dans un tri.
   * Facetable permet de champ hello pour la navigation par facettes.
   * « Possibilité de recherche » permet une recherche en texte intégral.
4. Cliquez sur hello **analyseur** onglet si vous voulez toospecify un analyseur de langue au niveau du champ hello. Seuls les analyseurs de langage peuvent être spécifiés pour l’instant. L’utilisation d’un analyseur personnalisé ou d’un analyseur non dédié au langage, comme Keyword, Pattern, etc., nécessite du code.
   
   * Cliquez sur **Searchable** toodesignate recherche en texte intégral de recherche sur le champ de hello et activez les liste de hello Analyseur de liste déroulante.
   * Choisissez un analyseur hello souhaité. Pour plus d’informations, voir [Création d’une définition d’index de document dans plusieurs langues dans Azure Search](search-language-support.md).
5. Cliquez sur hello **suggestions** tooenable les suggestions de requête type-ahead sur les champs sélectionnés.

## <a name="import-your-data"></a>Importer vos données
1. Dans **importer vos données**, fournissez un nom pour l’indexeur de hello. Rappelez-vous ce produit hello Assistant hello importer des données est un indexeur. Ultérieurement, si vous souhaitez tooview ou le modifiez, vous devez le sélectionner à partir du portail de hello plutôt qu’en réexécutant l’Assistant de hello. 
2. Spécifier la planification hello, qui est basée sur fuseau horaire régional de hello, dans lequel le service de hello est approvisionnée.
3. Définir les seuils de toospecify des options avancées sur l’indexation si puisse continuer si un document est supprimé. En outre, vous pouvez spécifier si **clé** les champs sont autorisés toocontain espaces et des barres obliques.  
4. Cliquez sur **OK** toocreate hello index et importer des données de hello.

Vous pouvez surveiller l’indexation dans le portail de hello. Comme les documents sont chargées, nombre de documents hello augmente pour index hello que vous avez défini. Parfois, il prend quelques minutes pour toopick de page du portail hello des mises à jour de la plus récente hello.

index de Hello est prêt tooquery dès que tous les documents hello sont chargés.

## <a name="query-an-index-using-search-explorer"></a>Interrogation d’un index à l’aide de l’Explorateur de recherche

portail de Hello inclut **rechercher dans l’Explorateur** afin que vous pouvez interroger un index sans avoir toowrite n’importe quel code. Vous pouvez utiliser l’[Explorateur de recherche](search-explorer.md) sur n’importe quel index.

expérience de recherche Hello est basée sur les paramètres par défaut, par exemple hello [syntaxe simple](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) et la valeur par défaut [paramètre de requête searchMode (https://docs.microsoft.com/rest/api/searchservice/search-documents). 

Résultats sont retournés au format JSON, dans un format détaillé, afin que vous pouvez inspecter la totalité du document hello.

## <a name="edit-an-existing-indexer"></a>Modification d’un indexeur existant
Comme indiqué, Assistant Importation de données hello crée un **indexeur**, que vous pouvez modifier en tant qu’une construction autonome dans le portail de hello.

Dans le tableau de bord du service hello, double-cliquez sur hello indexeur vignette tooslide une liste de tous les indexeurs créé pour votre abonnement. Double-cliquez sur un des hello indexeurs toorun, modifier ou supprimer. Vous pouvez remplacer l’index de hello existant par un autre, modifiez la source de données hello et définir les options de seuils d’erreur lors de l’indexation.

## <a name="edit-an-existing-index"></a>Modification d’un index existant
Assistant Hello également créé un **index**. Dans Azure Search, index tooan de mises à jour structurelle nécessitent une reconstruction de cet index. Une régénération implique la suppression des index de hello, recréation d’index hello à l’aide d’un schéma modifié hello les modifications souhaitées et recharger les données. Les mises à jour structurelles incluent la modification d’un type de données et le renommage ou la suppression d’un champ.

L’ajout d’un nouveau champ, la modification des profils de score, la modification des générateurs de suggestions ou la modification des analyseurs de langue ne nécessitent pas de reconstruction. Consultez la page [Mettre à jour l’index](https://msdn.microsoft.com/library/azure/dn800964.aspx) pour plus de détails.


## <a name="next-steps"></a>Étapes suivantes
Passez en revue ces toolearn des liens plus à propos des indexeurs :

* [Indexation d’Azure SQL Database](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Indexation d’Azure Cosmos DB](search-howto-index-documentdb.md)
* [Indexation de Stockage Blob](search-howto-indexing-azure-blob-storage.md)
* [Indexation de Stockage Table](search-howto-indexing-azure-tables.md)

<!--Image references-->
[1]: ./media/search-import-data-portal/search-import-data-command.png

