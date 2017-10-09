---
title: aaaWhat de nouveau dans Azure Data Catalog | Documents Microsoft
description: "Cet article fournit qu'une vue d’ensemble des nouvelles fonctionnalités ajoutées tooAzure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 1201f8d4-6f26-4182-af3f-91e758a12303
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/22/2017
ms.author: maroche
ms.openlocfilehash: f60130487ece39e110446b68544945089d2ab37e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="whats-new-in-azure-data-catalog"></a>Nouveautés d'Azure Data Catalog
Met à jour trop**Azure Data Catalog** sont publiées régulièrement. Comme certaines versions portent sur les fonctionnalités du service principal, toutes les versions ne contiennent pas nécessairement de nouvelles fonctionnalités orientées utilisateur. Cette page présente un nouveau service de Azure Data Catalog toohello ajouté des fonctionnalités de direction de l’utilisateur.

## <a name="whats-new-for-august-2017"></a>Nouveautés d’août 2017 
À compter d’août 2017, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :

*   Un nouvel échantillon de développeur est disponible pour la création et la gestion des métadonnées de relation à l’aide de hello API REST de catalogue de données. Hello *importer des informations sur les relations dans le catalogue de données* exemple est disponible sur hello [page d’exemples de code de catalogue de données](https://azure.microsoft.com/resources/samples/?service=data-catalog&sort=0). 
* Prise en charge pour l’extraction joindre des métadonnées de relation à partir de sources de données Teradata lors de l’enregistrement des tables connexes à l’aide d’outil de l’enregistrement de source de données hello.
* Prend en charge pour la fonction table SQL Server (TVF) objets lors de l’inscription des sources de données SQL Server à l’aide d’outil de l’enregistrement de source de données hello.
* Plusieurs mises à jour perfectionnements tooincrease hello performance et facilité d’utilisation du portail du catalogue de données hello.

## <a name="whats-new-for-july-2017"></a>Nouveautés de juillet 2017 
À compter de juillet 2017, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :
*   Prise en charge d’un contrôle plus précis des opérations de métadonnées autorisées, notamment :
    - Les administrateurs de catalogue peuvent limiter les balises de toocontribute de capacité des utilisateurs et des métadonnées connexes toohello catalogue, l’activation du catalogue de toohello d’accès en lecture seule.
    - Les administrateurs de catalogue peuvent limiter des capacité tooregister nouvelles sources de données utilisateurs dans le catalogue de hello.
    - Les administrateurs de catalogue peuvent limiter des capacité tootake la propriété utilisateurs de métadonnées des ressources de données dans le catalogue de hello.
    - Les autorisations peuvent être accordées utilisateurs afin de faciliter la gestion des autorisations et des groupes de sécurité Active Directory tooAzure.
* Prise en charge pour les relations entre les ressources de données inscrit et découverte actifs de données connexes dans le portail du catalogue de données hello, y compris :
    - Extraction des métadonnées de relation à partir de MySQL, Oracle et SQL Server (y compris la base de données SQL Azure) lors de l’utilisation des sources de données hello outil de l’enregistrement de source de données catalogue de données.
    - Découverte des données connexes lors de l’affichage des métadonnées des ressources dans le portail du catalogue de données hello.
    - Opérations toodefine, découvrir et gérer les relations entre les ressources de données à l’aide de hello API REST de catalogue de données.

Pour plus d’informations sur la gestion des autorisations dans le catalogue de données, consultez [comment toosecure accéder aux ressources de catalogue et les données toodata](data-catalog-how-to-secure-catalog.md).
Pour plus d’informations sur les relations dans le catalogue de données, consultez [comment tooview associés à des ressources de données dans Azure Data Catalog](data-catalog-how-to-view-related-data-assets.md).

## <a name="whats-new-for-june-2017"></a>Nouveautés de juin 2017 
À compter de juin 2017, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :
*   Prise en charge des sources de données Sybase, Apache Cassandra et MongoDB. Les utilisateurs peuvent désormais inscrire et découvrir les bases de données et tables Cassandra et MongoDB, ainsi que les bases de données, tables et vues Sybase.

> [!NOTE]
> Lorsque l’inscription MongoDB et Cassandra tables qui incluent des colonnes avec des types de données complexes telles que les enregistrements et les tableaux, ces colonnes ne pas être inclus dans les métadonnées de hello ajouté tooData catalogue.

## <a name="whats-new-for-may-2017"></a>Nouveautés de mai 2017 
À compter de mai 2017, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :
*   Un nouvel échantillon de développeur est disponible pour l’importation en bloc hello de termes de glossaire métier. exemple d’importation en bloc de glossaire Hello est disponible sur hello [page d’exemples de données catalogue développeur](https://docs.microsoft.com/azure/data-catalog/data-catalog-samples). 
*   Prise en charge pour la modification des informations de connexion ODBC dans le portail d’Azure Data Catalog hello. Les propriétaires de données actif et les administrateurs de catalogue de données peuvent désormais modifier les informations de connexion hello pour des sources de données ODBC sans avoir besoin de sources de données dans le Registre toore hello.
*   Prise en charge des URL interactives dans les définitions et les descriptions du glossaire métier. Lorsque les URL sont inclus dans les propriétés de description et la définition de hello pour les termes de glossaire métier, hello URL seront affichera en tant que liens hypertexte dans le portail du catalogue de données hello.
*   Prise en charge pour l’affichage expert nomme tooexpert en outre les adresses de messagerie. Lorsque vous affichez les experts de propriétés hello pour une ressource de données dans le portail du catalogue de données hello, nom complet de l’expert hello d’Azure Active Directory s’affichera dans l’info-bulle hello.

## <a name="whats-new-for-april-2017"></a>Nouveautés d’avril 2017 
À compter d’avril 2017, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :
*   Prise en charge des sources de données ODBC. Les utilisateurs peuvent désormais inscrire et découvrir les bases de données ODBC, les tables et vues à l’aide d’outil d’inscription de hello catalogue de données données source.

## <a name="whats-new-for-march-2017"></a>Nouveautés de mars 2017 
À partir de mars 2017, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :
*   Prise en charge de l’utilisation des groupes de sécurité AAD pour les administrateurs de Data Catalog.
*   Azure Data Catalog est maintenant disponible dans une nouvelle région Azure. Les clients peuvent configurer hello Azure Data Catalog dans hello ouest des États-Unis région, dans Ajout tooEast des États-Unis, ouest des États-Unis, Europe de l’ouest et est de l’Australie, Europe du Nord et Asie du Sud-est. Pour plus d’informations, consultez l’article [Régions Azure](https://azure.microsoft.com/regions/).

## <a name="whats-new-for-february-2017"></a>Nouveautés de février 2017 
À compter de février 2017, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :
*   Prise en charge pour les paramètres avancés dans outil d’enregistrement de source de données de catalogue de données hello. Les utilisateurs peuvent spécifier des valeurs de délai d’expiration des commandes lors de l’inscription de sources de données volumineuses.
*   Prise en charge des sources de données FTP et PostgreSQL. Les utilisateurs peuvent désormais inscrire et découvrir des fichiers et des répertoires FT, ainsi que les bases de données, tables et vues PostgreSQL.

## <a name="whats-new-for-january-2017"></a>Nouveautés de janvier 2017 
À compter de janvier 2017, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :
*   Azure Data Catalog est désormais conforme à [CSA STAR](https://www.microsoft.com/trustcenter/compliance/csa-star-certification).
*   Intégration à [Obtenir et transformer dans Excel 2016 et Power Query pour Excel](https://support.office.com/article/Introduction-to-Microsoft-Power-Query-for-Excel-6E92E2F4-2079-4E1F-BAD5-89F6269CD605). Les utilisateurs Excel peuvent partager et détecter des requêtes à l’aide d’Azure Data Catalog à partir d’Excel. Cette fonctionnalité est disponible toousers dont les licences Power BI Pro.

## <a name="whats-new-for-december-2016"></a>Nouveautés de décembre 2016
À compter de 2016 de décembre, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :
*   Azure Data Catalog est désormais conforme à [HIPAA](https://www.microsoft.com/trustcenter/Compliance/HIPAA) et aux [Clauses modèles de l’UE](https://www.microsoft.com/TrustCenter/Compliance/EU-Model-Clauses).
*   Prise en charge de la modification des informations de connexion des sources de données. Les propriétaires de données actif et les administrateurs de catalogue de données peuvent maintenant modifier les informations de connexion hello pour les sources de données enregistré sans avoir besoin de sources de données dans le Registre toore hello.
*   Prise en charge des sources de données Salesforce.com. Les utilisateurs peuvent désormais inscrire et découvrir les objets Salesforce.


## <a name="whats-new-for-november-2016"></a>Nouveautés de novembre 2016
À compter de novembre 2016, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :
*   Azure Data Catalog est désormais conforme aux normes [ISO/IEC 27001](https://www.microsoft.com/trustcenter/compliance/iso-iec-27001) et [ISO/IEC 27018](https://www.microsoft.com/TrustCenter/Compliance/iso-iec-27018).
*   Prise en charge pour l’inscription manuelle hello de sources de données ODBC à l’aide du portail de catalogue de données hello et l’API REST.

## <a name="whats-new-for-september-2016"></a>Nouveautés de septembre 2016
À compter de septembre 2016, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :

* Prise en charge des sources de données IBM DB2. Les utilisateurs peuvent désormais inscrire et découvrir les bases de données, tables et vues DB2.
* Prise en charge des sources de données Azure Cosmos DB. Les utilisateurs peuvent désormais inscrire et découvrir les bases de données et collections Cosmos DB.
* Prise en charge pour la personnalisation du nom du catalogue dans le portail du catalogue de données hello hello. Les administrateurs de catalogue peuvent maintenant fournir du texte s’affiche dans le titre du portail hello, telles que nom de l’organisation hello.

## <a name="whats-new-for-august-2016"></a>Nouveautés d’août 2016
À compter d’août 2016, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :

* Améliorations de l’inscription des sources de données SQL Server Master Data Services (MDS). Les utilisateurs peuvent maintenant inclure des profils de données et les versions préliminaires lors de l’inscription d’entités MDS à l’aide d’outil d’inscription de hello catalogue de données données source.
* Prise en charge des recherches enregistrées de l’organisation définies par l’administrateur. Lorsque vous enregistrez une recherche dans le portail du catalogue de données hello, les administrateurs de catalogue de données peuvent maintenant choisir toosave recherches pour une utilisation personnelle ou pour tous les utilisateurs du catalogue. Les recherches enregistrées de l’organisation sont partagées avec tous les utilisateurs du catalogue et peuvent servir de points de départ standardisés pour la détection des sources de données.
* Affichage des propriétés dans le portail du catalogue de données hello toohello des mises à jour. Toutes les propriétés de ressource de données sont maintenant affichées et gérés dans un tooprovide volet unique, redimensionnables, une expérience plus cohérente et détectable.

## <a name="whats-new-for-july-2016"></a>Nouveautés de juillet 2016
À compter de juillet 2016, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :

* Prise en charge des sources de données SQL Server Master Data Services (MDS). Les utilisateurs peuvent désormais inscrire et découvrir les entités et les modèles MDS.
* Prise en charge des procédures SQL Server stockées. Les utilisateurs peuvent désormais inscrire et découvrir les objets des procédures stockées dans les sources de données SQL Server.
* Prise en charge de langues supplémentaires dans le portail d’Azure Data Catalog hello et outil d’inscription source hello données, pour un total de 18 langues prises en charge. Hello expérience utilisateur d’Azure Data Catalog est localisé en fonction des préférences de langue hello définie dans Windows ou dans le navigateur web de hello.
* Les mises à jour et affinement de hello Data Catalog portail page d’accueil, y compris les améliorations des performances et une expérience utilisateur rationalisée.

## <a name="whats-new-for-june-2016"></a>Nouveautés de juin 2016
Depuis juin 2016, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :

* Prise en charge pour le redimensionnement des colonnes dans la vue de liste hello lors de la découverte des ressources de données dans le portail du catalogue de données hello. Les utilisateurs peuvent redimensionner maintenant toomore des colonnes individuelles à lire facilement asset longue des métadonnées telles que les balises et les descriptions.
* Menu « Ouvrir dans » de toohello a été ajouté à Power Query pour Excel, dans le portail du catalogue de données hello. Les utilisateurs peuvent désormais ouvrir les sources de données pris en charge dans Excel 2016 ou dans Excel 2010 et Excel 2013 avec hello [Power Query pour Excel](https://support.office.com/article/Introduction-to-Microsoft-Power-Query-for-Excel-6E92E2F4-2079-4E1F-BAD5-89F6269CD605) complément installé.
* Prise en charge des sources de données de stockage de tables Azure. Les utilisateurs peuvent désormais inscrire et découvrir des objets de table dans les sources de données Stockage Azure.

## <a name="whats-new-for-may-2016"></a>Nouveautés de mai 2016
À compter de mai 2016, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :

* Un glossaire métier qui permet aux administrateurs de catalogue toodefine business termes et les hiérarchies toocreate un vocabulaire métier commun. Les utilisateurs peuvent la balise actifs de données enregistré avec toomake de termes de glossaire il toodiscover plus facile et comprendre le contenu de hello du catalogue de hello. Pour plus d’informations, consultez [comment tooset des hello glossaire métier pour baliser les régie](data-catalog-how-to-business-glossary.md)  
* Améliorations toohello glossaire métier de catalogue de données qui permet aux utilisateurs tooupdate plusieurs termes de glossaire en une seule opération. Les utilisateurs peuvent sélectionner plusieurs hello tooedit de termes champs qui suivent :
  * Terme parent : hello utilisateur sélectionne un nouveau terme parent et tous les termes sélectionnés sont des enfants de toobe mis à jour du terme parent de hello sélectionné. Si hello sélectionnés ont tous des termes hello même parent, puis parent est indiqué dans la zone de texte hello, sinon le champ de terme parent hello est tooblank de jeu.   
  * Les balises et les parties prenantes : les utilisateurs peuvent ajouter et supprimer des balises et les parties prenantes de plusieurs termes de glossaire à l’aide de la même expérience de hello balisage plusieurs ressources de données.

> [!NOTE]
> glossaire métier de Hello est uniquement disponible dans hello Édition Standard d’Azure Data Catalog. Hello édition gratuite ne fournit pas certaines fonctionnalités d’étiquetage régi ou un glossaire métier.

## <a name="whats-new-for-march-2016"></a>Nouveautés de mars 2016
Mars 2016, hello suivant les fonctionnalités ont été ajoutée tooAzure données catalogue : g :

* Un consolidée API REST point de terminaison pour accéder par programme aux fonctionnalités de recherche hello et fonctions de gestion des ressources de catalogue de hello service Azure Data Catalog. Ce point de terminaison d’API de recherche et ce point de terminaison d’API de catalogue étaient déconseillés et ne sont plus disponibles depuis le 21 mars 2016. Il n’y a aucune modification sémantique toohello Hello API. URI de point de terminaison hello uniquement modifié. Pour plus d’informations, consultez hello [référence API REST de catalogue de données Azure](https://msdn.microsoft.com/library/azure/mt267595.aspx). Pour des exemples d’API, consultez [Exemples de développement Azure Data Catalog](data-catalog-samples.md).

## <a name="whats-new-for-february-2016"></a>Nouveautés de février 2016
À compter de février 2016, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :

* Sélection d’une source de données qui vient d’être repensé rencontrer dans l’outil d’inscription de hello Azure Data Catalog données source. Hello outil d’enregistrement de source de données a été mis à jour toomake informatique plus facile vous toolocate et sélectionnez à partir de sources de données hello pris en charge par Azure Data Catalog.
* Prise en charge de 10 langues supplémentaires dans le portail d’Azure Data Catalog hello et outil de l’enregistrement de source de données hello. En outre tooEnglish, hello expérience d’Azure Data Catalog est désormais disponible en allemand, espagnol, Français, italien, japonais, coréen, portugais (Brésil), russe, chinois simplifié et chinois traditionnel. Bonjour Azure Data Catalog, expérience utilisateur est localisé en fonction des préférences de langue de hello définie dans Windows ou dans le navigateur web de l’utilisateur hello.
* Prise en charge de la géo-réplication des données Azure Data Catalog pour garantir la continuité de l’activité et la récupération d’urgence. Tout contenu de Azure Data Catalog, y compris source crowdsourced et les métadonnées des annotations de données, est désormais répliqué entre deux régions Azure à aucun toocustomers coût supplémentaire. Hello régions Azure sont déjà associées, au moins 500 miles écart et suivez les mappage hello comme décrit dans [entreprise la continuité des activités et récupération d’urgence (BCDR) : les régions Azure associées](../best-practices-availability-paired-regions.md).
* Prise en charge pour la modification de hello abonnement Azure utilisé par Azure Data Catalog. Azure Data Catalog les administrateurs peuvent utiliser page de paramètres hello dans hello Azure Data Catalog tooselect portail un autre abonnement Azure pour la facturation.

## <a name="whats-new-for-january-2016"></a>Nouveautés de janvier 2016
À compter de janvier 2016, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :

* Prise en charge de l’inscription manuelle de sources de données supplémentaires. Vous pouvez maintenant utiliser « Créer une entrée manuelle » dans le portail d’Azure Data Catalog hello, ou hello de tooregister d’API REST de Azure données catalogue hello les sources de données suivantes :
  * OData : fonction, jeu d’entités et conteneur d’entités
  * HTTP : fichier, point de terminaison, rapport et site
  * Système de fichiers : fichier
  * SharePoint : liste
  * FTP : fichier et répertoire
  * Salesforce.com : objet
  * DB2 : table, vue et base de données
  * PostgreSQL : table, vue et base de données
* Prise en charge de la fonction « Ouvrir dans SQL Server Data Tools » pour les sources de données SQL Server (y compris Base de données SQL Azure et Azure SQL Data Warehouse).  
* Prise en charge de l’inscription et de la découverte des vues et packages SAP HANA. Vous pouvez enregistrer des données SAP HANA sources à l’aide des données de catalogue de données Azure hello de source de l’outil d’inscription et pouvant annoter et découvrir des sources de données SAP HANA à l’aide du portail d’Azure Data Catalog hello.
* Hello toopin de capacité et détacher des ressources de données dans le portail d’Azure Data Catalog hello. Vous pouvez choisir toopin données actifs toomake les toorediscover plus facile et la réutilisation.
* Une page d’accueil qui vient d’être repensée dans le portail d’Azure Data Catalog hello. nouvelle page d’accueil Hello inclut idée hello utilisateurs activité en cours - y compris les ressources récemment publiées, épinglé actifs et les recherches enregistrées - et un aperçu de l’activité hello Bonjour catalogue en un ensemble.
* Prise en charge pour les paramètres utilisateur persistante dans le portail d’Azure Data Catalog hello. Paramètres de l’expérience utilisateur - affichage de grille ou de mosaïque, y compris, hello du nombre de résultats par page et d’accès ou de désactiver la mise en surbrillance - sont conservées entre les sessions de l’utilisateur.
* Azure Data Catalog est maintenant disponible dans deux nouvelles régions Azure. Les clients peuvent configurer hello Azure Data Catalog dans hello Europe du Nord et Asie du Sud-est régions, en plus tooEast des États-Unis, ouest des États-Unis, Europe de l’ouest et est de l’Australie. Pour plus d’informations, consultez l’article [Régions Azure](https://azure.microsoft.com/regions/).

> [!NOTE]
> « Ouvrir dans SQL Server Data Tools » requiert Visual Studio 2013 avec Update 4 et les outils SQL Server toobe installé. tooinstall hello dernière version de SQL Server Data Tools, visitez [télécharger SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).


## <a name="whats-new-for-december-2015"></a>Nouveautés de décembre 2015
Depuis décembre 2015, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :

* Prise en charge de profils de données pour les sources de données Azure SQL Data Warehouse. Lorsque vous inscrivez des vues et les tables de l’entrepôt de données SQL Azure, les utilisateurs peuvent choisir les métriques de profil des données tooinclude avec des métadonnées hello extraites à partir de la source de données hello.
* Prise en charge de l’inscription et de la découverte des bases de données et des objets MySQL. Les utilisateurs peuvent inscrire MySQL sources de données à l’aide des données de catalogue de données Azure hello de source de l’outil d’inscription et pouvant annoter et découvrir des sources de données MySQL à l’aide du portail d’Azure Data Catalog hello.
* Prise en charge de l’authentification SPNEGO et Windows pour les sources de données Teradata. Lorsque vous inscrivez Teradata tables et les vues, les utilisateurs peuvent choisir tooTeradata tooconnect à l’aide de l’authentification SPNEGO et Windows et LDAP et TD2.
* Prise en charge des sources de données Azure Data Lake Store. Les utilisateurs peuvent désormais inscrire et découvrir des sources de données Azure Data Lake Store à l’aide d'Azure Data Catalog.
* Prise en charge pour spécifier manuellement les paramètres du proxy réseau dans l’outil d’inscription de hello Azure Data Catalog données source. Les utilisateurs peuvent sélectionner « Modifier les paramètres de proxy » à partir de la page d’accueil de l’outil hello et peuvent spécifier utilisé par l’outil de hello du toobe d’adresse et le port de proxy hello.

## <a name="whats-new-for-november-2015"></a>Nouveautés de novembre 2015
À compter de novembre 2015, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :

* Hello capacité tooview et copiez les chaînes de connexion à partir de portail d’Azure Data Catalog hello pour SQL Server (y compris la base de données SQL Azure) et sources de données Oracle. Les utilisateurs peuvent cliquer le lien « Afficher les chaînes de connexion » dans les informations de connexion hello pour un serveur SQL Server ou de table, vue ou la base de données, toosee hello chaînes de connexion Oracle utilisé la source de données tooconnect toohello. Les chaînes de connexion ADO.NET, ODBC, OLEDB et JDBC sont fournies pour les sources de données SQL Server. Les chaînes de connexion ODBC et OLEDB sont fournies pour les sources de données Oracle.
* Prise en charge de l’inclusion des profils de données lors de l’inscription des tables et vues Teradata.
* Prise en charge de la fonction « Ouvrir dans Power BI Desktop » pour les sources SQL Server (notamment Azure SQL Database et Azure SQL Data Warehouse), SQL Server Analysis Services, Azure Storage et HDFS.  
* Prise en charge de l’authentification LDAP pour les sources de données Teradata. Lorsque vous inscrivez Teradata tables et les vues, les utilisateurs peuvent choisir tooTeradata tooconnect à l’aide de LDAP et l’authentification TD2.
* Prise en charge de « Ouvrir dans Excel » pour les sources de données Teradata.
* Prise en charge de termes de recherche récente dans le portail d’Azure Data Catalog hello. Lors de la recherche dans le portail de hello, les utilisateurs peuvent sélectionner à partir d’expérience de découverte recherche récemment utilisés termes tooaccelerate hello.
* Prise en charge de l’aperçu des sources de données Teradata. Lors de l’inscription Teradata tables et les vues, les utilisateurs peuvent choisir les enregistrements de capture instantanée tooinclude avec des métadonnées hello extraites à partir de la source de données hello.
* Prise en charge de la commande « Ouvrir avec Excel » pour les sources de données Azure SQL Data Warehouse.
* Prise en charge de la définition et la modification des schémas de niveau colonne pour les ressources de données inscrites. Après la création d’une ressource de données à l’aide du portail d’Azure Data Catalog hello manuellement, les utilisateurs peuvent ajouter des définitions de colonne dans les propriétés de ressource données hello.
* Prise en charge pour les requêtes de « a » lors de la recherche d’Azure Data Catalog, détection de hello tooenable inscrit de ressources de données qui possèdent des métadonnées spécifiques. La syntaxe des requêtes Azure Data Catalog comprend à présent les éléments suivants :

| Syntaxe de requête | Objectif |
| --- | --- |
| `has:previews` |Recherche les ressources de données qui comprennent une version préliminaire |
| `has:documentation` |Recherche les ressources de données pour lesquelles une documentation a été fournie |
| `has:tableDataProfiles` |Recherche des ressources de données avec des informations de profil des données de niveau table |
| `has:columnsDataProfiles` |Recherche des ressources de données avec des informations de profil des données de niveau colonne |


> [!NOTE]
> « Ouvrir dans Power BI Desktop » requiert une version de hello Power BI Desktop application toobe est installé. Si vous rencontrez des problèmes ou erreurs à l’aide de cette fonctionnalité, vérifiez que vous avez hello dernière version de Power BI Desktop à partir de [PowerBI.com](https://powerbi.com).


## <a name="whats-new-for-october-2015"></a>Nouveautés d’octobre 2015
Depuis octobre 2015, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :

* Prise en charge de chiffrement au repos d'aperçus et de profils de données pour des sources de données enregistrées. Azure Data Catalog chiffre en toute transparence des enregistrements de version préliminaire et inscrits avec le service de hello, sans recourir à de gestion de clés par les administrateurs de catalogue de sources de données de profils de données.
* Prise en charge des sources de données Teradata. Les utilisateurs peuvent désormais inscrire et découvrir des tables et vues Teradata.
* Prise en charge de sources de données Hive locales. Les utilisateurs peuvent désormais inscrire et détecter des tables Hive pour Apache Hive dans Hadoop sur des sources de données locales.
* Prise en charge des recherches enregistrées dans le portail d’Azure Data Catalog hello. Les utilisateurs peuvent enregistrer des termes de recherche et tooeasily des sélections de filtre répéter des recherches précédentes et définir des vues utiles de contenu de ce catalogue hello. L’utilisateur peut également définir une recherche enregistrée comme recherche par défaut. Lorsqu’un utilisateur clique sur l’icône de recherche hello « Loupe » à partir de la page accueil du portail Azure Data Catalog hello ou à partir de la page « getting started » de hello, hello passe directement toohello marquée comme valeur par défaut de recherche enregistrée.
* Prise en charge pour la documentation de texte enrichi pour les données des ressources et les conteneurs dans le portail d’Azure Data Catalog hello. Les utilisateurs peuvent désormais fournir une documentation pour les données telles que les tableaux, les vues et les rapports, ainsi que pour les conteneurs tels que les bases de données et les modèles, pour les scénarios où les balises et les descriptions ne sont pas suffisantes.
* Prise en charge de l'enregistrement manuel de types de sources de données connus. Les utilisateurs peuvent entrer manuellement les informations de source de données à l’aide du portail d’Azure Data Catalog hello pour tous les types de source de données pris en charge par Azure Data Catalog.
* Prise en charge de l’autorisation des  groupes de sécurité Azure Active Directory. Les administrateurs de catalogue peuvent activer des accès toosecurity groupes de catalogues, les comptes d’utilisateur, rendant tooAzure d’accès plus facile toomanage Data Catalog.
* Prise en charge pour l’ouverture des sources de données Hive dans Excel à partir du portail d’Azure Data Catalog hello.

> [!NOTE]
> Pour la version actuelle de hello, seule l’authentification Teradata TD2 est pris en charge. D’autres mécanismes d’authentification seront pris en charge dans les futures versions.

> [!NOTE]
> toouse la fonctionnalité de « Ouvrir dans Excel » hello pour les sources de données Hive, les utilisateurs doivent avoir hello pilote ODBC installé pour la ruche.

## <a name="whats-new-for-september-2015"></a>Nouveautés de septembre 2015
À compter de septembre 2015, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :

* Prise en charge de l’inclusion des profils de données lors de l’inscription des sources de données Hive.
* Prise en charge pour la détection par programme des hello API de catalogue, facilitant ainsi pour toointegrate d’applications avec Azure Data Catalog.
* Un nouveau « getting started » source de données dans le portail d’Azure Data Catalog hello expérience de découverte. Lorsque les utilisateurs entrent une page de « découvrir » hello du portail d’Azure Data Catalog hello sans entrer un terme de recherche, ils sont présentés avec une vue d’ensemble du contenu du catalogue hello, y compris les balises de hello plus fréquemment utilisé, experts, types de sources de données et les types d’objets.
* Prise en charge de l’inscription et de la découverte des bases de données et des objets Azure SQL Data Warehouse. Pour plus d’informations sur Azure SQL Data Warehouse, consultez [SQL Data Warehouse](https://azure.microsoft.com/services/sql-data-warehouse/).
* Prise en charge de l’inscription et de la découverte des modèles SQL Server Analysis Services et des serveurs SQL Server Reporting Services en tant que conteneurs. Lors de l’inscription des objets SSAS et SSRS, Azure Data Catalog crée une entrée pour le modèle SSAS hello et le serveur SSRS et pour les rapports hello et d’autres objets. les conteneurs Hello peuvent être détectés et annoté à l’aide du portail d’Azure Data Catalog hello. Les utilisateurs peuvent également rechercher et filtrer hello contenu d’un modèle de serveur dans toosearching d’ajout et de filtrage du contenu hello du catalogue de hello.
* Prise en charge de l’inscription et de la détection d’objets SQL Server Analysis Services via HTTP/HTTPS. Les utilisateurs peuvent maintenant connecter les serveurs de tooSSAS à l’aide d’une URL (par exemple, https://servername/olap/msmdpump.dll) au lieu d’un nom de serveur et peuvent utiliser l’authentification de base et les connexions anonymes à l’authentification tooWindows Ajout. Pour plus d’informations sur les tooSSAS des connexions HTTP/HTTPS, consultez [configurer l’accès HTTP tooAnalysis Services](https://msdn.microsoft.com/library/gg492140.aspx).
* Prise en charge de sources de données Hive sur HDInsight. Les utilisateurs peuvent désormais inscrire et détecter des tables Hive pour Apache Hive dans Hadoop sur des sources de données HDInsight. Pour plus d’informations sur la ruche sur HDInsight, consultez hello [centre de documentation HDInsight](../hdinsight/hdinsight-use-hive.md).
* Prise en charge de l’inscription et de la détection de bases de données Oracle et de clusters HDFS en tant que conteneurs. Lors de l’enregistrement des tables Oracle et de vues ou de HDFS, Azure Data Catalog crée une entrée pour la base de données hello, les tables et vues. base de données Hello peut être détecté et annoté à l’aide du portail d’Azure Data Catalog hello. Les utilisateurs peuvent également rechercher et filtrer hello du contenu d’une base de données ou de cluster en outre toosearching et le filtrage de contenu hello du catalogue de hello.
* Prise en charge de l'enregistrement manuel de types de sources de données inconnus. Les utilisateurs peuvent entrer manuellement les informations de source de données à l’aide du portail d’Azure Data Catalog hello, afin que les sources de données ne sont pas explicitement prises en charge par hello outil d’enregistrement de source de données peut être annoté et découverts.
* Prise en charge de l'enregistrement et de la découverte des bases de données SQL Server en tant que conteneurs. Lorsque vous inscrivez des vues et des tables SQL Server, Azure Data Catalog crée une entrée pour la base de données hello, les tables et vues. base de données Hello peut être détecté et annoté à l’aide du portail d’Azure Data Catalog hello. Les utilisateurs peuvent également rechercher et filtrer contenu hello d’une base de données toosearching d’addition et de filtrage contenu hello du catalogue de hello.

> [!NOTE]
> SSAS et SSRS des objets qui ont été toohello préalable inscrit version 18 septembre doivent être réinscrit à l’aide d’outil de l’enregistrement de source de données hello avant hello modèle ou serveur entrée est ajoutée toohello catalogue. Nouvelle inscription d’une source de données n’affecte pas toutes les annotations qui ont été ajoutées par les utilisateurs dans le portail d’Azure Data Catalog hello.

> [!NOTE]
> Tables Oracle, des vues et des fichiers HDFS et des répertoires qui ont été toohello préalable inscrit version 11 septembre doivent être réinscrit à l’aide d’outil de l’enregistrement de source de données hello avant hello entrée de base de données ou de cluster est ajoutée toohello catalogue. Nouvelle inscription d’une source de données n’affecte pas toutes les annotations qui ont été ajoutées par les utilisateurs dans le portail d’Azure Data Catalog hello.

> [!NOTE]
> Tables SQL Server et les vues qui ont été toohello préalable inscrit version septembre 4 doivent être inscrit de nouveau à l’aide d’outil de l’enregistrement de source de données hello avant l’ajout d’entrée de base de données hello toohello catalogue. Nouvelle inscription d’une source de données n’affecte pas toutes les annotations qui ont été ajoutées par les utilisateurs dans le portail d’Azure Data Catalog hello.

## <a name="whats-new-for-august-2015"></a>Nouveautés d’août 2015
Depuis août 2015, hello suivant les fonctionnalités ont été ajoutée tooAzure catalogue de données :

* Prise en charge du profilage des données pour les sources de données SQL Server et Oracle. Lorsque vous inscrivez des vues et les tables SQL Server et Oracle, les utilisateurs peuvent choisir les informations de profil des données tooinclude pour les objets hello en cours d’inscription. profilage des données Hello inclut les statistiques au niveau objet et au niveau des colonnes.
* Prise en charge des sources de données HDFS Hadoop. Les utilisateurs peuvent désormais s'inscrire et découvrir les fichiers et répertoires HFDFS.
* Prise en charge de la fourniture d’informations de demande d’accès pour les sources de données inscrites. Pour toute ressource de données enregistré, les utilisateurs peuvent fournir maintenant des instructions pour demander l’accès, y compris des liens de messagerie ou URL, tooeasily intégrer avec des processus et des outils existants.
* Info-bulles pour les étiquettes et les experts, toomake il toodiscover plus facilement ce que les utilisateurs ont fourni les métadonnées pour les ressources de données enregistré.
* Nous avons ajouté un nouveau « Utilisateur » bouton et menu tooour barre de navigation supérieure. Ce menu permet à utilisateur de hello consultez toolog du compte utilisé hello sur tooAzure Data Catalog et toosign out si vous le souhaitez. Ce menu affiche également le nom du catalogue hello, qui est utile toodevelopers à l’aide de hello API REST du catalogue de données Azure.
* Édition standard uniquement : Lorsque vous ajoutez des ressources de toodata propriétaires, Azure Data Catalog prend désormais en charge les comptes d’utilisateurs et groupes de sécurité en tant que propriétaires. tooadd un groupe de sécurité en tant que propriétaire pour les ressources de données sélectionnée, vous pouvez entrer nom complet du groupe de deux hello ou adresse de messagerie du groupe hello UPN, le cas échéant.
* Prise en charge des sources de données de stockage d’objets blob Azure. Les utilisateurs peuvent désormais s’inscrire et découvrir des objets blob Azure Storage et des répertoires.

