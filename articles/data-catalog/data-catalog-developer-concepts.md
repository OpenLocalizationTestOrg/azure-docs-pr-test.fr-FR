---
title: "concepts de développement de catalogue aaaData | Documents Microsoft"
description: "Concepts clés de présentation toohello dans le modèle conceptuel d’Azure Data Catalog, tel qu’exposé via hello API REST de catalogue."
services: data-catalog
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
tags: 
ms.assetid: 89de9137-a0a4-40d1-9f8d-625acad31619
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: d0b1628ff6c31458cb650efef852244f0c139b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-developer-concepts"></a>Concepts de développeur Azure Data Catalog
**Microsoft Azure Data Catalog** est un service cloud entièrement géré qui fournit des fonctionnalités de détection de source de données et de métadonnées de source de données de crowdsourcing. Les développeurs peuvent utiliser le service hello via son API REST. Présentation des concepts hello implémentées dans le service hello sont importante pour les développeurs toosuccessfully intégrer **Azure Data Catalog**.

## <a name="key-concepts"></a>Concepts clés
Hello **Azure Data Catalog** modèle conceptuel est basé sur quatre concepts clés : hello **catalogue**, **utilisateurs**, **actifs**et **Annotations**.

![concept][1]

*Figure 1 : modèle conceptuel simplifié d’Azure Data Catalog*

### <a name="catalog"></a>Catalogue
A **catalogue** est le conteneur de niveau supérieur hello pour tous les hello une organisation stocke des métadonnées. Chaque compte Azure ne peut avoir qu’un **catalogue** . Les catalogues sont lié tooan abonnement Azure, mais un seul **catalogue** peuvent être créés pour n’importe quel compte Azure donné, même si un compte peut avoir plusieurs abonnements.

Un catalogue contient des **utilisateurs** et des **ressources**.

### <a name="users"></a>Utilisateurs
Les utilisateurs sont des entités de sécurité qui ont des autorisations tooperform actions (recherche de catalogue de hello, ajouter, modifier ou supprimer des éléments, etc.) dans le catalogue de hello.

Un utilisateur peut avoir plusieurs rôles différents. Pour plus d’informations sur les rôles, consultez la section de hello rôles et d’autorisation.

Des utilisateurs individuels et des groupes de sécurité peuvent être ajoutés.

Azure Data Catalog utilise Azure Active Directory pour la gestion des identités et des accès. Chaque utilisateur de catalogue doit être un membre de hello Active Directory pour le compte de hello.

### <a name="assets"></a>Éléments multimédias
Un **catalogue** contient des ressources de données . **Ressources** hello l’unité de granularité gérée par le catalogue de hello.

la granularité d’un élément multimédia Hello varie par source de données. Pour SQL Server ou une base de données Oracle, une ressource peut être une table ou un affichage. Pour SQL Server Analysis Services, une ressource peut être une mesure, une dimension ou un indicateur de performance clé (KPI). Pour SQL Server Reporting Services, une ressource est un rapport.

Un **Asset** est hello la chose que vous ajoutez ou supprimez d’un catalogue. Il s’agit unité hello du résultat que vous récupérez des **recherche**.

Une **ressource** est constituée de son nom, de son emplacement et de son type ainsi que d’annotations apportant une description supplémentaire.

### <a name="annotations"></a>annotations
Les annotations sont des éléments qui représentent des métadonnées sur les ressources.

Les annotations sont, par exemple, des descriptions, des balises, un schéma, une documentation, etc. Une liste complète des types d’élément multimédia hello et annotation sont Bonjour section relative au modèle objet d’élément multimédia.

## <a name="crowdsourcing-annotations-and-user-perspective-multiplicity-of-opinion"></a>Annotations de crowdsourcing et perspective de l'utilisateur (multiplicité d'opinions)
Un aspect clé d’Azure Data Catalog est comment il prend en charge marketing participatif de hello de métadonnées dans le système de hello. Tooa opposés wiki approche – où il existe un seul avis et hello dernier à écrire gagne, modèle d’Azure Data Catalog hello qui permet plusieurs avis toolive côte à côte dans le système de hello.

Cette approche reflète hello réel des données d’entreprise où les utilisateurs peuvent avoir différentes perspectives sur un élément multimédia donné :

* Un administrateur de base de données peut fournir des informations sur les contrats de niveau de service ou la fenêtre de traitement disponibles hello pour les opérations en bloc ETL
* Un gestionnaire de données peut fournir des informations sur l’élément multimédia de hello entreprise processus toowhich hello, ou de classifications hello hello entreprise a appliqué tooit
* Un analyste financier peut fournir des informations sur l’utilisation des données de hello lors des tâches de création de rapports de fin de période

toosupport cet exemple, chaque utilisateur – hello DBA, Gestionnaire de données hello et analyste de hello – peut ajouter une description tooa table qui a été inscrit dans le catalogue de hello. Toutes les descriptions sont conservées dans le système de hello, et dans le portail d’Azure Data Catalog hello toutes les descriptions sont affichées.

Ce modèle est appliqué toomost d’éléments hello dans le modèle d’objet hello, pour les types d’objet dans la charge utile JSON de hello sont souvent des tableaux pour les propriétés où vous pouvez vous attendre un singleton.

Par exemple, sous l’élément multimédia de hello racine est un tableau d’objets de description. propriété de tableau Hello est nommée « Description ». Un objet description possède une propriété : description. modèle de Hello est que chaque utilisateur de la description des types Obtient un objet de description créé pour la valeur hello fournie par l’utilisateur de hello.

Hello UX peut alors choisir comment toodisplay hello combinaison. Il existe trois modèles d'affichage différents.

* modèle le plus simple Hello est « All ». Dans ce modèle, tous les objets de hello sont affichés dans une liste. portail d’Azure Data Catalog Hello UX utilise ce modèle pour la description.
* Un autre modèle est « Fusionner ». Dans ce modèle, toutes les valeurs hello émanant de différents utilisateurs de hello sont fusionnées, doublons supprimés. Propriétés de balises et les experts hello sont des exemples de ce modèle dans le portail d’Azure Data Catalog hello UX.
* Un troisième modèle est la « règle de Thomas ». Dans ce modèle, uniquement hello dernière valeur tapée dans est affichée. Le nom convivial est un exemple de ce modèle.

## <a name="asset-object-model"></a>Modèle d'objet de ressource
Introduit dans la section des Concepts clés hello, hello **Azure Data Catalog** modèle objet inclut des éléments qui peuvent être actifs ou l’annotation. Les éléments ont des propriétés, qui peuvent être facultatives ou obligatoires. Certaines propriétés s’appliquent à des éléments tooall. Certaines propriétés s’appliquent tooall actifs. Certaines propriétés s’appliquent uniquement les types d’élément multimédia toospecific.

### <a name="system-properties"></a>Propriétés système
<table><tr><td><b>Nom de la propriété</b></td><td><b>Type de données</b></td><td><b>Commentaires</b></td></tr><tr><td>timestamp</td><td>DateTime</td><td>Hello dernier temps hello de l’élément a été modifié. Ce champ est généré par le serveur de hello lorsqu’un élément est inséré ou chaque fois qu’un élément est mis à jour. Hello valeur de cette propriété est ignorée sur l’entrée d’opérations de publication.</td></tr><tr><td>id</td><td>Uri</td><td>Url absolue de l’élément hello (en lecture seule). Il s’agit de hello URI adressable unique pour l’élément de hello.  Hello valeur de cette propriété est ignorée sur l’entrée d’opérations de publication.</td></tr><tr><td>type</td><td>String</td><td>type Hello de hello (en lecture seule).</td></tr><tr><td>etag</td><td>String</td><td>Une version de toohello chaîne correspondante d’élément hello qui peut être utilisé pour le contrôle d’accès concurrentiel optimiste lors de l’exécution d’opérations qui mettent à jour des éléments de catalogue de hello. « * » peut être utilisé toomatch n’importe quelle valeur.</td></tr></table>

### <a name="common-properties"></a>Propriétés communes
Ces propriétés s’appliquent les types d’élément multimédia tooall racine et de tous les types d’annotation.

<table>
<tr><td><b>Nom de la propriété</b></td><td><b>Type de données</b></td><td><b>Commentaires</b></td></tr>
<tr><td>fromSourceSystem</td><td>Boolean</td><td>Indique si les données de l’élément sont dérivées d’un système source (tel que Base de données SQL Server, Base de données Oracle) ou créées par un utilisateur.</td></tr>
</table>

### <a name="common-root-properties"></a>Propriétés de racine communes
<p>
Ces propriétés s’appliquent des types d’élément multimédia tooall racine.

<table><tr><td><b>Nom de la propriété</b></td><td><b>Type de données</b></td><td><b>Commentaires</b></td></tr><tr><td>name</td><td>String</td><td>Un nom dérivé des informations sur l’emplacement source données hello</td></tr><tr><td>dsl</td><td>DataSourceLocation</td><td>Décrit la source de données hello de manière unique et est un des identificateurs hello pour un composant de hello. (Voir la section identité double).  structure Hello de hello dsl varie selon le protocole de hello et type de source.</td></tr><tr><td>dataSource</td><td>DataSourceInfo</td><td>Plus de détails sur le type hello d’actif.</td></tr><tr><td>lastRegisteredBy</td><td>SecurityPrincipal</td><td>Décrit un utilisateur hello qui se sont récemment inscrits cet élément multimédia.  Contient l’id unique de hello pour l’utilisateur hello (hello upn) et un nom d’affichage (lastName et firstName).</td></tr><tr><td>containerId</td><td>String</td><td>ID de ressource de conteneur hello pour la source de données hello. Cette propriété n’est pas prise en charge pour le type de conteneur de hello.</td></tr></table>

### <a name="common-non-singleton-annotation-properties"></a>Propriétés d’annotation non singleton courantes
Ces propriétés s’appliquent les types non singleton annotation tooall (annotations, ce qui permettait toobe multiples par asset).

<table>
<tr><td><b>Nom de la propriété</b></td><td><b>Type de données</b></td><td><b>Commentaires</b></td></tr>
<tr><td>key</td><td>String</td><td>Clé qui identifie de façon unique annotation hello dans la collection actuelle de hello spécifié par l’utilisateur. longueur de clé Hello ne peut pas dépasser 256 caractères.</td></tr>
</table>

### <a name="root-asset-types"></a>Types de ressources racines
Types de ressource racine sont les types qui représentent hello différents types de ressources de données qui peuvent être enregistrés dans le catalogue de hello. Pour chaque type de racine, il existe une vue, qui décrit l’actif et les annotations incluses dans la vue de hello. Nom de la vue doit être utilisé dans le segment d’url hello correspondant {view_name} lors de la publication d’un élément multimédia à l’aide des API REST.

<table><tr><td><b>Type de ressource (nom de la vue)</b></td><td><b>Propriétés supplémentaires</b></td><td><b>Type de données</b></td><td><b>Annotations autorisées</b></td><td><b>Commentaires</b></td></tr><tr><td>Table (« tables »)</td><td></td><td></td><td>Description<p>FriendlyName<p>Tag<p>Schéma<p>ColumnDescription<p>ColumnTag<p> Expert<p>VERSION PRÉLIMINAIRE<p>AccessInstruction<p>TableDataProfile<p>ColumnDataProfile<p>ColumnDataClassification<p>Documentation<p></td><td>Une table représente des données tabulaires.  Par exemple : une table SQL, un affichage SQL, une table tabulaire Analysis Services, une dimension multidimensionnelle Analysis Services, une table Oracle, etc.   </td></tr><tr><td>Mesures (« measures »)</td><td></td><td></td><td>Description<p>FriendlyName<p>Tag<p>Expert<p>AccessInstruction<p>Documentation<p></td><td>Ce type représente une mesure Analysis Services.</td></tr><tr><td></td><td>mesure</td><td>Colonne</td><td></td><td>Mesure hello décrivant de métadonnées</td></tr><tr><td></td><td>isCalculated </td><td>Boolean</td><td></td><td>Spécifie si les mesures hello sont calculée ou non.</td></tr><tr><td></td><td>measureGroup</td><td>Chaîne</td><td></td><td>Conteneur physique de mesure</td></tr><td>KPI (« kpis »)</td><td></td><td></td><td>Description<p>FriendlyName<p>Tag<p>Expert<p>AccessInstruction<p>Documentation</td><td></td></tr><tr><td></td><td>measureGroup</td><td>Chaîne</td><td></td><td>Conteneur physique de mesure</td></tr><tr><td></td><td>goalExpression</td><td>String</td><td></td><td>Une expression numérique MDX ou un calcul qui retourne la valeur cible hello hello indicateur de performance clé.</td></tr><tr><td></td><td>valueExpression</td><td>String</td><td></td><td>Expression numérique MDX qui retourne la valeur réelle de hello Hello indicateur de performance clé.</td></tr><tr><td></td><td>statusExpression</td><td>String</td><td></td><td>Une expression MDX qui représente l’état hello Hello indicateur de performance clé à un point spécifié dans le temps.</td></tr><tr><td></td><td>trendExpression</td><td>String</td><td></td><td>Une expression MDX qui prend la valeur hello hello KPI au fil du temps. Hello peut être n’importe quel critère de temps qui s’avère utile dans un contexte spécifique.</td>
<tr><td>Report (« reports »)</td><td></td><td></td><td>Description<p>FriendlyName<p>Tag<p>Expert<p>AccessInstruction<p>Documentation<p></td><td>Ce type représente un rapport SQL Server Reporting Services </td></tr><tr><td></td><td>assetCreatedDate</td><td>String</td><td></td><td></td></tr><tr><td></td><td>assetCreatedBy</td><td>Chaîne</td><td></td><td></td></tr><tr><td></td><td>assetModifiedDate</td><td>Chaîne</td><td></td><td></td></tr><tr><td></td><td>assetModifiedBy</td><td>Chaîne</td><td></td><td></td></tr><tr><td>Container (« containers »)</td><td></td><td></td><td>Description<p>FriendlyName<p>Tag<p>Expert<p>AccessInstruction<p>Documentation<p></td><td>Ce type représente un conteneur d'autres ressources telles qu'une base de données SQL, un conteneur d'objets Blob Azure ou un modèle Analysis Services.</td></tr></table>

### <a name="annotation-types"></a>Types d'annotation
Types d’annotation représentent des types de métadonnées qui peuvent être affectés à des types de tooother dans le catalogue de hello.

<table>
<tr><td><b>Type d’annotation (nom de la vue imbriqué)</b></td><td><b>Propriétés supplémentaires</b></td><td><b>Type de données</b></td><td><b>Commentaires</b></td></tr>

<tr><td>Description (« descriptions »)</td><td></td><td></td><td>Cette propriété contient une description de la ressource. Chaque utilisateur du système de hello permettre ajouter leur propre description.  Uniquement cet utilisateur peut modifier l’objet de Description hello.  (Les propriétaires actifs et les administrateurs peuvent supprimer l’objet de Description hello mais pas le modifier). système de Hello conserve séparément les descriptions des utilisateurs.  Par conséquent il est un tableau des descriptions de chaque élément multimédia (un pour chaque utilisateur qui a contribué à leurs connaissances sur asset hello, dans toopossibly d’addition qui contient des informations dérivée de la source de données hello).</td></tr>
<tr><td></td><td>description</td><td>string</td><td>Une brève description (lignes 2-3) de l’élément multimédia de hello</td></tr>

<tr><td>Tag (« tags »)</td><td></td><td></td><td>Cette propriété définit une balise pour une ressource. Chaque utilisateur du système de hello peut ajouter plusieurs balises pour un élément multimédia.  Hello uniquement les utilisateur qui a créé les objets de balise puisse les modifier.  (Les propriétaires actifs et les administrateurs peuvent supprimer l’objet de balise hello mais pas le modifier). système de Hello conserve les balises d’utilisateurs séparément.  Il y a donc un tableau d’objets Tag sur chaque ressource.</td></tr>
<tr><td></td><td>tag</td><td>string</td><td>Un balise décrivant hello élément multimédia.</td></tr>

<tr><td>FriendlyName (« friendlyName »)</td><td></td><td></td><td>Cette propriété contient un nom convivial pour une ressource. FriendlyName est une annotation singleton - FriendlyName qu’une seule peut être ajouté tooan actif.  Hello uniquement les utilisateur qui a créé l’objet de FriendlyName peut la modifier. (Les propriétaires actifs et les administrateurs peuvent supprimer hello FriendlyName objet mais pas le modifier). système de Hello tient à jour les noms d’utilisateurs convivial séparément.</td></tr>
<tr><td></td><td>friendlyName</td><td>string</td><td>Un nom convivial de l’élément multimédia de hello.</td></tr>

<tr><td>Schema (« schema »)</td><td></td><td></td><td>Hello schéma décrit la structure hello de données de hello.  Il répertorie les noms d’attribut (colonne, attribut de champ, etc.) hello, ainsi d’autres métadonnées des types.  Cette information est dérivée à partir de la source de données hello.  Le schéma est une annotation singleton ; il n’est possible d’ajouter qu’un seul schéma pour une ressource.</td></tr>
<tr><td></td><td>colonnes</td><td>Column[]</td><td>Un tableau d'objets de colonne. Elles décrivent les colonnes hello avec des informations dérivées de la source de données hello.</td></tr>

<tr><td>ColumnDescription (« columnDescriptions »)</td><td></td><td></td><td>Cette propriété contient une description de la colonne.  Chaque utilisateur du système de hello permettre ajouter leurs propres descriptions pour plusieurs colonnes (au plus une par colonne). Uniquement les utilisateurs hello qui a créé les objets ColumnDescription peuvent les modifier.  (Les propriétaires actifs et les administrateurs peuvent supprimer hello ColumnDescription objet mais pas le modifier). système de Hello conserve les descriptions des colonnes de ces utilisateur séparément.  Par conséquent, il est un tableau d’objets ColumnDescription sur chaque élément multimédia (une par colonne pour chaque utilisateur qui a contribué à leurs connaissances sur la colonne de hello en outre toopossibly qui contient des informations dérivées de source de données hello).  Hello ColumnDescription est faiblement lié toohello schéma afin qu’il puisse obtenir synchronisé. Hello ColumnDescription peut décrire une colonne qui n’existe plus dans le schéma de hello.  C’est description de tookeep toohello writer et schéma de synchronisation.  source de données Hello peut-être également des informations de description des colonnes et sont des objets ColumnDescription supplémentaires qui sont créés lorsque vous exécutez l’outil de hello.</td></tr>
<tr><td></td><td>columnName</td><td>String</td><td>nom Hello de colonne hello à que cette description fait référence.</td></tr>
<tr><td></td><td>description</td><td>String</td><td>une brève description (lignes 2-3) de la colonne de hello.</td></tr>

<tr><td>ColumnTag (« columnTags »)</td><td></td><td></td><td>Cette propriété contient une balise pour une colonne. Chaque utilisateur du système de hello peut ajouter plusieurs balises pour une colonne donnée et pouvez ajouter des balises pour plusieurs colonnes. Uniquement les utilisateurs hello qui a créé les objets ColumnTag peuvent les modifier. (Les propriétaires actifs et les administrateurs peuvent supprimer hello ColumnTag objet mais pas le modifier). système de Hello conserve les étiquettes de colonne ces utilisateurs séparément.  Il y a donc un tableau d’objets ColumnTag sur chaque ressource.  Hello ColumnTag est toohello faiblement lié schéma afin qu’il puisse obtenir synchronisé. Hello ColumnTag peut décrire une colonne qui n’existe plus dans le schéma de hello.  Il est d’étiquette de colonne tookeep toohello writer et schéma de synchronisation.</td></tr>
<tr><td></td><td>columnName</td><td>String</td><td>nom Hello de colonne hello à que cette balise fait référence.</td></tr>
<tr><td></td><td>tag</td><td>String</td><td>Une colonne hello décrivant de balise.</td></tr>

<tr><td>Expert (« experts »)</td><td></td><td></td><td>Cette propriété contient un utilisateur qui est considéré comme un expert dans le jeu de données hello. opinions(descriptions) bulles toohello haut experts Hello de hello UX la liste des descriptions. Chaque utilisateur peut spécifier ses propres experts. Uniquement cet utilisateur peut modifier l’objet d’experts hello. (Les propriétaires actifs et les administrateurs peuvent supprimer les objets Expert hello mais pas le modifier).</td></tr>
<tr><td></td><td>expert</td><td>SecurityPrincipal</td><td></td></tr>

<tr><td>Preview (« previews »)</td><td></td><td></td><td>Aperçu de Hello contient un instantané de hello top 20 lignes de données pour un composant de hello. L’aperçu n’est utile que pour certains types de ressources (c’est à dire qu’il est pertinent pour Table, mais pas pour Measure).</td></tr>
<tr><td></td><td>preview</td><td>object[]</td><td>Tableau d'objets qui représentent une colonne.  Chaque objet possède une propriété de mappage de colonne tooa avec une valeur pour cette colonne pour la ligne de hello.</td></tr>

<tr><td>AccessInstruction (« accessInstructions »)</td><td></td><td></td><td></td></tr>
<tr><td></td><td>mimeType</td><td>string</td><td>type de contenu de hello Hello mime.</td></tr>
<tr><td></td><td>Contenu</td><td>string</td><td>instructions Hello permettant tooget accéder à des ressources de données toothis. contenu de Hello peut être une URL, une adresse de messagerie ou un ensemble d’instructions.</td></tr>

<tr><td>TableDataProfile (« tableDataProfiles »)</td><td></td><td></td><td></td></tr>
<tr><td></td><td>numberOfRows</td></td><td>int</td><td>nombre de Hello de lignes dans le jeu de données hello</td></tr>
<tr><td></td><td>size</td><td>long</td><td>taille de Hello en octets hello du jeu de données.  </td></tr>
<tr><td></td><td>schemaModifiedTime</td><td>string</td><td>schéma de hello Hello dernière heure a été modifiée.</td></tr>
<tr><td></td><td>dataModifiedTime</td><td>string</td><td>jeu de données Hello dernière heure hello a été modifié (données a été ajoutées, modifiée ou supprimer)</td></tr>

<tr><td>ColumnsDataProfile (« columnsDataProfiles »)</td><td></td><td></td><td></td></tr>
<tr><td></td><td>colonnes</td></td><td>ColumnDataProfile[]</td><td>Tableau de profils de données de colonne.</td></tr>

<tr><td>ColumnDataClassification (« columnDataClassifications »)</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columnName</td><td>String</td><td>nom Hello de colonne hello à que cette classification se rapporte.</td></tr>
<tr><td></td><td>classification ;</td><td>String</td><td>classification de Hello de données hello dans cette colonne.</td></tr>

<tr><td>Documentation (« documentation »)</td><td></td><td></td><td>Une seule documentation peut être associée à une ressource donnée.</td></tr>
<tr><td></td><td>mimeType</td><td>string</td><td>type de contenu de hello Hello mime.</td></tr>
<tr><td></td><td>Contenu</td><td>string</td><td>contenu de documentation Hello.</td></tr>

</table>

### <a name="common-types"></a>Types courants
Les types courants peuvent être utilisés comme types de hello pour les propriétés, mais ne sont pas des éléments.

<table>
<tr><td><b>Type courant</b></td><td><b>Propriétés</b></td><td><b>Type de données</b></td><td><b>Commentaires</b></td></tr>
<tr><td>DataSourceInfo</td><td></td><td></td><td></td></tr>
<tr><td></td><td>sourceType</td><td>string</td><td>Décrit le type hello de source de données.  Par exemple : SQL Server, base de données Oracle, etc.  </td></tr>
<tr><td></td><td>objectType</td><td>string</td><td>Décrit le type hello d’objet dans la source de données hello. Par exemple : table, affichage pour SQL Server.</td></tr>

<tr><td>DataSourceLocation</td><td></td><td></td><td></td></tr>
<tr><td></td><td>protocol</td><td>string</td><td>Obligatoire. Décrit un toocommunicate de protocole utilisé avec la source de données hello. Par exemple : « tds » pour SQl Server, « oracle » pour Oracle, etc. Consultez trop[spécification de référence - DSL Structure de source de données](data-catalog-dsr.md) pour la liste hello des protocoles actuellement pris en charge.</td></tr>
<tr><td></td><td>address</td><td>Dictionnaire<string, object></td><td>Obligatoire. Adresse est un ensemble de données toohello spécifique qui est la source de données utilisé tooidentify hello référencée. données d’adresse Hello portée tooa protocole particulier, ce qui signifie qu’il est sans signification sans connaître le protocole de hello.</td></tr>
<tr><td></td><td>authentication</td><td>string</td><td>facultatif. schéma d’authentification Hello utilisé toocommunicate avec la source de données hello. Par exemple : windows, oauth, etc.</td></tr>
<tr><td></td><td>connectionProperties</td><td>Dictionnaire<string, object></td><td>facultatif. Informations supplémentaires sur la source de données tooconnect tooa.</td></tr>

<tr><td>SecurityPrincipal</td><td></td><td></td><td>Hello principal n’effectue aucune validation des propriétés fournies par rapport à AAD lors de la publication.</td></tr>
<tr><td></td><td>upn</td><td>string</td><td>Adresse de messagerie unique de l'utilisateur. Doit être spécifié si objectId n’est pas fourni, ou dans le contexte de hello de propriété « lastRegisteredBy », sinon facultative.</td></tr>
<tr><td></td><td>objectId</td><td>Guid</td><td>Identité AAD du groupe d’utilisateurs ou de sécurité. facultatif. Doit être spécifié si UPN n’est pas fourni ; sinon, facultatif.</td></tr>
<tr><td></td><td>firstName</td><td>string</td><td>Prénom de l'utilisateur (à des fins d'affichage). facultatif. Valide uniquement dans le contexte hello de propriété de « lastRegisteredBy ». Ne peut pas être spécifié lors de la fourniture du principal de sécurité pour « roles », « permissions » et « experts ».</td></tr>
<tr><td></td><td>lastName</td><td>string</td><td>Nom de l'utilisateur (à des fins d'affichage). facultatif. Valide uniquement dans le contexte hello de propriété de « lastRegisteredBy ». Ne peut pas être spécifié lors de la fourniture du principal de sécurité pour « roles », « permissions » et « experts ».</td></tr>

<tr><td>Colonne</td><td></td><td></td><td></td></tr>
<tr><td></td><td>name</td><td>string</td><td>Nom de colonne de hello ou un attribut.</td></tr>
<tr><td></td><td>type</td><td>string</td><td>type de données de colonne de hello ou un attribut. les types autorisés Hello dépendent sourceType de données de ressource de hello.  Seul un sous-ensemble des types est pris en charge.</td></tr>
<tr><td></td><td>maxLength</td><td>int</td><td>Hello maximum autorisé pour la colonne de hello ou un attribut. Dérivé de la source de données. Seuls les types de source toosome applicable.</td></tr>
<tr><td></td><td>precision</td><td>byte</td><td>précision Hello pour hello colonne ou l’attribut. Dérivé de la source de données. Seuls les types de source toosome applicable.</td></tr>
<tr><td></td><td>isNullable</td><td>Boolean</td><td>Indique si la colonne de hello est autorisée à toohave une valeur null ou non. Dérivé de la source de données. Seuls les types de source toosome applicable.</td></tr>
<tr><td></td><td>expression</td><td>string</td><td>Si la valeur de hello est une colonne calculée, ce champ contient expression hello correspondant à la valeur de hello. Dérivé de la source de données. Seuls les types de source toosome applicable.</td></tr>

<tr><td>ColumnDataProfile</td><td></td><td></td><td></td></tr>
<tr><td></td><td>columnName </td><td>string</td><td>nom de colonne de hello de Hello</td></tr>
<tr><td></td><td>type </td><td>string</td><td>type Hello de colonne de hello</td></tr>
<tr><td></td><td>Min </td><td>string</td><td>valeur minimale de Hello hello jeu de données</td></tr>
<tr><td></td><td>max </td><td>string</td><td>valeur maximale de Hello hello jeu de données</td></tr>
<tr><td></td><td>avg </td><td>double</td><td>valeur moyenne de Hello hello jeu de données</td></tr>
<tr><td></td><td>stdev </td><td>double</td><td>écart type Hello pour le jeu de données hello</td></tr>
<tr><td></td><td>nullCount </td><td>int</td><td>nombre de valeurs null dans le jeu de données hello de Hello</td></tr>
<tr><td></td><td>distinctCount  </td><td>int</td><td>nombre de valeurs distinctes dans le jeu de données hello de Hello</td></tr>


</table>

## <a name="asset-identity"></a>Identité des ressources
Azure Data Catalog utilise « protocol » et les propriétés d’identité à partir de hello « address » sac de propriétés de hello datasourcelocation est « dsl » propriété toogenerate identité de l’élément multimédia hello, qui est utilisé tooaddress hello actif à l’intérieur de hello catalogue.
Par exemple, protocole de « tds » hello a des propriétés d’identité « server », « database », « schema » et « objet ». combinaisons de Hello du protocole de hello et de propriétés d’identité hello sont identité de hello toogenerate utilisé Hello Asset de Table SQL Server.
Azure Data Catalog propose plusieurs protocoles de source de données intégrés qui sont répertoriés dans [Spécification de référence de la source de données - Structure DSL](data-catalog-dsr.md).
Hello ensemble de protocoles pris en charge peut être étendue par programme (consultez la référence d’API REST de catalogue tooData). Les administrateurs de hello catalogue peuvent enregistrer des protocoles de source de données personnalisé. Hello tableau suivant décrit les propriétés nécessaires de hello tooregister un protocole personnalisé.

### <a name="custom-data-source-protocol-specification"></a>Caractéristiques d’un protocole de source de données personnalisé
<table>
<tr><td><b>Type</b></td><td><b>Propriétés</b></td><td><b>Type de données</b></td><td><b>Commentaires</b></td></tr>

<tr><td>DataSourceProtocol</td><td></td><td></td><td></td></tr>
<tr><td></td><td>namespace</td><td>string</td><td>espace de noms Hello du protocole de hello. Namespace doit être de 1 too255 caractères, contenir une ou plusieurs parties non vide séparées par un point (.). Chaque partie doit être comprise entre 1 too255 caractères, commencer par une lettre et contenir uniquement des lettres et des chiffres.</td></tr>
<tr><td></td><td>name</td><td>string</td><td>nom Hello du protocole de hello. Nom doit être comprise entre 1 too255 caractères, commencer par une lettre et contenir uniquement des lettres, des chiffres et hello tiret (-).</td></tr>
<tr><td></td><td>identityProperties</td><td>DataSourceProtocolIdentityProperty[]</td><td>Liste des propriétés d’identité ; doit contenir au moins une propriété, mais pas plus de 20. Par exemple : « server », « database », « schema », « objet » est des propriétés d’identité du protocole de « tds » hello.</td></tr>
<tr><td></td><td>identitySets</td><td>DataSourceProtocolIdentitySet[]</td><td>Liste de jeux d’identité. Définit des ensembles de propriétés d’identité qui représentent l’identité valide d’une ressource. Doit contenir au moins un jeu, mais pas plus de 20. Par exemple : {« server », « database », « schema » et « object »} est un jeu d’identité pour le protocole « tds », qui définit l’identité d’une ressource de table SQL Server.</td></tr>

<tr><td>DataSourceProtocolIdentityProperty</td><td></td><td></td><td></td></tr>
<tr><td></td><td>name</td><td>string</td><td>nom de Hello de propriété de hello. Nom doit être comprise entre 1 too100 caractères, commencent par une lettre et peut contenir que des lettres et des chiffres.</td></tr>
<tr><td></td><td>type</td><td>string</td><td>type de Hello de propriété de hello. Les valeurs prises en charge sont les suivantes : « bool, « boolean », « byte », « guid », « int », « integer », « long », « string », « url »</td></tr>
<tr><td></td><td>ignoreCase</td><td>bool</td><td>Indique si la casse doit être ignorée lors de l’utilisation de valeur de la propriété. Ne peut être spécifié que pour les propriétés de type « string ». La valeur par défaut est false.</td></tr>
<tr><td></td><td>urlPathSegmentsIgnoreCase</td><td>bool[]</td><td>Indique si la casse doit être ignorée pour chaque segment de chemin d’accès d’url hello. Ne peut être spécifié que pour les propriétés de type « url ». La valeur par défaut est [false].</td></tr>

<tr><td>DataSourceProtocolIdentitySet</td><td></td><td></td><td></td></tr>
<tr><td></td><td>name</td><td>string</td><td>nom Hello d’ensemble d’identités hello.</td></tr>
<tr><td></td><td>properties</td><td>string[]</td><td>liste de Hello des propriétés d’identité inclus dans cette identité définie. Elle ne peut pas contenir de doublons. Chaque propriété référencée par un ensemble d’identités doit être définie dans la liste hello de « identityProperties » du protocole de hello.</td></tr>

</table>

## <a name="roles-and-authorization"></a>Rôles et autorisations
Microsoft Azure Data Catalog offre des fonctionnalités d'autorisation pour les opérations CRUD sur les ressources et les annotations.

## <a name="key-concepts"></a>Concepts clés
Bonjour Azure Data Catalog utilise deux mécanismes d’autorisation :

* Autorisation par rôle
* Autorisation basée sur les autorisations

### <a name="roles"></a>contrôleur
Il existe trois rôles : **administrateur**, **propriétaire** et **collaborateur**.  Chaque rôle dispose de son étendue et les droits qui sont résumés dans hello tableau suivant.

<table><tr><td><b>Rôle</b></td><td><b>Portée</b></td><td><b>Droits</b></td></tr><tr><td>Administrateur</td><td>Catalogue (tous les actifs/annotations Bonjour catalogue)</td><td>Lecture Suppression ViewRoles

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>Propriétaire</td><td>Chaque ressource (élément racine)</td><td>Lecture Suppression ViewRoles

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>Collaborateur</td><td>Chaque ressource et annotation</td><td>Mise à jour en lecture supprimer ViewRoles Remarque : tous les droits de hello sont considérés comme révoqués si hello en lecture à droite d’élément de hello est révoquée pour hello contributeur</td></tr></table>

> [!NOTE]
> **Lecture**, **mise à jour**, **supprimer**, **ViewRoles** droits sont applicables tooany élément (actif ou annotation) lors de la **TakeOwnership**, **ChangeOwnership**, **ChangeVisibility**, **ViewPermissions** sont uniquement les actifs de racine toohello applicable.
> 
> **Supprimer** droite s’applique tooan élément et tous les sous-éléments ou élément unique qu’il contient. Par exemple, la suppression d’une ressource supprime également toutes les annotations pour cette ressource.
> 
> 

### <a name="permissions"></a>Autorisations
L'autorisation est une liste d'entrées de contrôle d'accès. Chaque entrée de contrôle d’accès affecte l’ensemble de l’entité de sécurité tooa droits. Autorisations peuvent uniquement être spécifiées sur un élément multimédia (autrement dit, les éléments racine) et s’appliquent toohello actif et les sous-éléments.

Au cours de hello **Azure Data Catalog** aperçu uniquement **en lecture** droite est prise en charge de la visibilité toorestrict hello autorisations liste tooenable scénario d’un élément multimédia.

Par défaut, tout utilisateur authentifié a **en lecture** avec le bouton droit pour n’importe quel élément dans le catalogue de hello, sauf si la visibilité est restreinte ensemble toohello des principaux dans les autorisations hello.

## <a name="rest-api"></a>API REST
**PUT** et **POST** l’élément d’affichage des demandes peut être utilisé toocontrol rôles et autorisations : dans la charge utile tooitem de plus, les deux propriétés système peuvent être spécifiées **rôles** et  **autorisations**.

> [!NOTE]
> **autorisations** uniquement les éléments racine tooa applicable.
> 
> **Propriétaire** élément de rôle s’applique seulement tooa racine.
> 
> Par défaut, lorsqu’un élément est créé dans le catalogue de hello son **collaborateur** a la valeur toohello des utilisateur actuellement authentifié. Si l’élément doit être mis à jour par tout le monde, **collaborateur** doit être défini trop&lt;tout le monde&gt; principal de sécurité spécial dans hello **rôles** propriété lorsque l’élément est d’abord publié () consultez le toohello l’exemple suivant). **Collaborateur** ne peut pas être modifié et reste identique hello pendant la durée de vie d’un élément (même **administrateur** ou **propriétaire** n’a pas hello de droite toochange hello  **Collaborateur**). Hello la seule valeur prise en charge pour le paramètre explicite de hello Hello **collaborateur** est &lt;tout le monde&gt;: **collaborateur** peut être uniquement un utilisateur qui a créé un élément ou &lt; Tout le monde&gt;.
> 
> 

### <a name="examples"></a>Exemples
**Définir le collaborateur trop&lt;tout le monde&gt; lors de la publication d’un élément.**
Le principal de sécurité spécial &lt;Everyone&gt; a l’objectId « 00000000-0000-0000-0000-000000000201 ».
  **POST** https://api.azuredatacatalog.com/catalogs/default/views/tables/?api-version=2016-03-30

> [!NOTE]
> Certaines implémentations du client HTTP peuvent automatiquement émettre à nouveau les demandes tooa de réponse 302 à partir du serveur de hello, mais généralement supprimer les en-têtes d’autorisation à partir de la demande de hello. L’en-tête d’autorisation hello étant requis toomake demandes tooAzure catalogue de données, vous devez vous assurer l’en-tête d’autorisation hello est encore fourni lors de la relance d’un emplacement de redirection de tooa de demande spécifié par Azure Data Catalog. Hello exemple de code suivant montre à l’aide de l’objet hello HttpWebRequest de .NET.
> 
> 

**Corps**

    {
        "roles": [
            {
                "role": "Contributor",
                "members": [
                    {
                        "objectId": "00000000-0000-0000-0000-000000000201"
                    }
                ]
            }
        ]
    }

  **Attribution des propriétaires et restriction de la visibilité pour un élément racine existant** : **PUT** https://api.azuredatacatalog.com/catalogs/default/views/tables/042297b0...1be45ecd462a?api-version=2016-03-30

    {
        "roles": [
            {
                "role": "Owner",
                "members": [
                    {
                        "objectId": "c4159539-846a-45af-bdfb-58efd3772b43",
                        "upn": "user1@contoso.com"
                    },
                    {
                        "objectId": "fdabd95b-7c56-47d6-a6ba-a7c5f264533f",
                        "upn": "user2@contoso.com"
                    }
                ]
            }
        ],
        "permissions": [
            {
                "principal": {
                    "objectId": "27b9a0eb-bb71-4297-9f1f-c462dab7192a",
                    "upn": "user3@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            },
            {
                "principal": {
                    "objectId": "4c8bc8ce-225c-4fcf-b09a-047030baab31",
                    "upn": "user4@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            }
        ]
    }

> [!NOTE]
> Dans PUT il n’est pas nécessaire de toospecify une charge utile d’élément dans le corps de hello : PUT peut être utilisé tooupdate des rôles simplement et/ou les autorisations.
> 
> 

<!--Image references-->
[1]: ./media/data-catalog-developer-concepts/concept2.png
