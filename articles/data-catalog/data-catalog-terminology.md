---
title: "aaaAzure la terminologie du catalogue de données | Documents Microsoft"
description: "Cet article fournit une présentation tooconcepts et termes utilisés dans la documentation d’Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6fec74d9-4a3c-4b4b-88ba-cad5ad143331
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: b5f071db4f62c914d2c1cdef9aa686b18d5297d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-terminology"></a>Terminologie d’Azure Data Catalog
## <a name="catalog"></a>Catalogue
Bonjour Azure Data Catalog est un référentiel de métadonnées basé sur le cloud dans lequel les données sources et ressources de données peuvent être inscrits. catalogue de Hello sert à un emplacement de stockage central pour les métadonnées structurelles extraites de sources de données et métadonnées descriptives ajoutées par les utilisateurs.

## <a name="data-source"></a>Source de données
Une source de données est un système ou un conteneur qui gère des ressources de données. Exemples : les bases de données SQL Server, les bases de données Oracle, les bases de données SQL Server Analysis Services (tabulaires ou multidimensionnelles) et les serveurs SQL Server Reporting Services.

## <a name="data-asset"></a>Ressource de données
Ressources de données sont des objets contenus dans les sources de données qui peuvent être enregistrés avec le catalogue de hello. Exemples : les tables et les vues SQL Server, les tables et les vues Oracle, les mesures SQL Server Analysis Services, les dimensions et les indicateurs clés de performance, et les rapports SQL Server Reporting Services.

## <a name="data-asset-location"></a>Emplacement des ressources de données
emplacement hello d’une source de données ou d’un élément de données, qui peut être utilisé tooconnect toohello stocke Hello catalogue source à l’aide d’une application cliente. format de Hello et les détails de l’emplacement de hello varient selon le type de source de données hello. Une table SQL Server peut être, par exemple, identifiée par quatre éléments : le nom du serveur, le nom de la base de données, le nom du schéma et le nom de l'objet, alors qu’un rapport SQL Server Reporting Services peut être identifié par son URL.

## <a name="structural-metadata"></a>Métadonnée structurelle
Les métadonnées structurelles sont hello extraites d’une source de données qui décrit la structure de hello d’une ressource de données. Cela inclut hello actifs emplacement, son nom d’objet et de type et les caractéristiques supplémentaires spécifiques au type. Par exemple, les métadonnées structurelles de hello pour les tables et vues incluent les noms hello et types de données des colonnes de l’objet hello.

## <a name="descriptive-metadata"></a>Métadonnée descriptive
Métadonnées descriptives sont qui décrit l’objectif de hello ou l’intention d’une ressource de données. En général, les métadonnées descriptives sont ajoutée par les utilisateurs du catalogue à l’aide du portail d’Azure Data Catalog hello, mais il peut également être extrait à partir de la source de données hello lors de l’inscription. Par exemple, hello Azure Data Catalog d’inscription est extrait des descriptions de hello Description (propriété) dans SQL Server Analysis Services et SQL Server Reporting Services et de hello [ms_descriptiondepropriétéétendue](https://technet.microsoft.com/library/ms190243.aspx)dans les bases de données SQL Server, si ces propriétés ont été remplies avec des valeurs.

## <a name="request-access"></a>Demander l'accès
Métadonnées d’une ressource de données peuvent inclure des informations sur comment accéder à toorequest toohello données actif ou source de données. Ces informations sont présentées avec emplacement données hello et peuvent inclure un ou plusieurs des options suivantes de hello :

* adresse de messagerie Hello d’utilisateur de hello ou de l’équipe responsable de l’octroi de source de données access toohello.
* URL de Hello Hello documentées processus que les utilisateurs doivent accepter la source de données toohello toogain access.
* Hello l’URL d’un outil de gestion identité et accès (tel que Microsoft Identity Manager) qui peut être source de données toohello toogain utilisé access.
* Une entrée de texte libre qui décrit la façon dont les utilisateurs peuvent avoir la source de données access toohello.

## <a name="preview"></a>VERSION PRÉLIMINAIRE
Un aperçu dans Azure Data Catalog est un instantané des enregistrements too20 qui peuvent être extraites à partir de la source de données hello lors de l’inscription et stockées dans le catalogue de hello avec les métadonnées des ressources données hello. Aperçu de Hello peut aider les utilisateurs de découvrir une ressource de données est mieux comprennent sa fonction et l’objet. En d’autres termes, voir les exemples de données peut être plus importante que les voir uniquement les types de données et les noms de colonne hello.
Aperçus sont uniquement pris en charge pour les tables et vues et doivent être explicitement sélectionnés par l’utilisateur de hello lors de l’inscription.

## <a name="data-profile"></a>Profil de données
Un profil des données dans Azure Data Catalog est un instantané des métadonnées au niveau de la table et au niveau des colonnes sur une ressource de données enregistrés qui peut être extraites à partir de la source de données hello lors de l’inscription et stockée dans le catalogue de hello avec les métadonnées des ressources données hello. profilage des données Hello peut aider les utilisateurs de découvrir une ressource de données est mieux comprennent sa fonction et l’objet. Toopreviews similaires, les profils de données doit explicitement sélectionné par l’utilisateur de hello lors de l’inscription.

> [!NOTE]
> Extraction d’un profil de données peut être une opération coûteuse pour grandes tables et des vues, et peut considérablement augmenter hello durée tooregister une source de données.
>
>

## <a name="user-perspective"></a>Point de vue de l’utilisateur
Dans Azure Data Catalog, tout utilisateur peut fournir des métadonnées descriptives pour une ressource de données inscrite. Chaque utilisateur dispose d’une perspective distincte de données de hello et son utilisation. Par exemple, administrateur hello responsable d’un serveur peut fournir des détails de hello de son contrat de niveau de service (SLA) ou de fenêtres de sauvegarde ; un gestionnaire de données peut fournir des toodocumentation de liens pour les entreprises hello traite prend en charge des données hello ; et un analyste peut fournir une description en termes de hello qui sont les plus pertinents tooother analystes et qui peut être plus utile toothose les utilisateurs qui doivent toodiscover et comprennent les données de salutation.

Chacune de ces perspectives sont utiles, par nature, et dans Azure Data Catalog chaque utilisateur peut fournir des informations hello toothem significative, alors que tous les utilisateurs peuvent utiliser les données hello toounderstand informations et son objectif.

## <a name="expert"></a>Expert
Un expert est un utilisateur qui a été identifié comme une personne pouvant apporter son point de vue d’« expert » pour une ressource de données. Tout utilisateur peut s’ajouter lui-même ou ajouter un autre utilisateur en tant qu'expert pour une ressource. Qui est répertorié comme un expert n’implique pas des privilèges supplémentaires dans Azure Data Catalog ; Il permet aux utilisateurs tooeasily localiser ces perspectives sont probablement toobe utile lorsque vous parcourez les métadonnées d’un élément multimédia.

## <a name="owner"></a>Propriétaire
Un propriétaire est un utilisateur qui dispose de privilèges supplémentaires pour assurer la gestion d'une ressource de données d’Azure Data Catalog. Les utilisateurs peuvent s’approprier des ressources de données inscrites et les propriétaires peuvent ajouter d'autres utilisateurs en tant que copropriétaires. Pour plus d’informations, consultez [comment toomanage les ressources de données](data-catalog-how-to-manage.md)  

> [!NOTE]
> La propriété et la gestion sont uniquement disponibles dans hello Édition Standard d’Azure Data Catalog.
>
>

## <a name="registration"></a>Inscription
L’inscription est hello action consistant à extraire les métadonnées des ressources de données à partir d’une source de données et en le copiant service Azure Data Catalog de toohello. Les ressources de données qui ont été inscrites peuvent ensuite être annotées et découvertes.

## <a name="see-also"></a>Voir aussi
* [Présentation d’Azure Data Catalog](data-catalog-what-is-data-catalog.md) -Cet article fournit une vue d’ensemble de service Azure Data Catalog de hello, hello valeur qu'il fournit et il prend en charge des scénarios de hello.
* [Prise en main Azure Data Catalog](data-catalog-get-started.md) -cet article fournit un didacticiel de bout en bout illustrant comment toouse Azure du catalogue de données pour la détection de source de données.  
