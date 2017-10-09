---
title: "aaaSave recherches et code confidentiel des ressources de données dans Azure Data Catalog | Documents Microsoft"
description: "Tooarticle de façon à des fonctionnalités mise en surbrillance dans Azure Data Catalog pour enregistrer les sources de données et des ressources de données pour une utilisation ultérieure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0ad0a31d4b84782fed9d80acc2734912eecd6d74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a>Enregistrer des recherches et épingler des ressources de données dans Azure Data Catalog
## <a name="introduction"></a>Introduction
Azure Data Catalog fournit des fonctionnalités de détection des sources de données. Vous pouvez rapidement rechercher et filtrer les sources de données toolocate hello catalogue et comprendre leur rôle respectif, rend plus facile toofind hello bonnes données pour la tâche hello à portée de main.

Mais que se passe-t-il si vous devez tooregularly fonctionnent avec hello même données ? Et que se passe-t-il si d’autres utilisateurs contribuent régulièrement votre toohello de la base de connaissances mêmes sources de données dans le catalogue de hello ? Dans ces situations, ayant toorepeatedly problème hello même recherche peut être inefficace. C’est là que l’enregistrement des recherches et l’épinglage des ressources de données peuvent vous aider.

## <a name="saved-searches"></a>Recherches enregistrées
Dans Data Catalog, une recherche enregistrée est une définition de recherche réutilisable spécifique à un utilisateur. Vous pouvez définir une recherche (termes, balises et autres filtres), puis l’enregistrer. Vous pouvez réexécuter définition de recherche hello enregistré ultérieure tooreturn toutes les ressources de données qui correspondent aux critères de recherche.

### <a name="create-a-saved-search"></a>Créer une recherche enregistrée
toocreate une recherche enregistrée, procédez comme hello suivant :
1. Dans le portail Azure Data Catalog hello, Bonjour **recherche actuelle** fenêtre, cliquez sur **enregistrer**. 

    ![Bouton Enregistrer dans les paramètres Recherche actuelle](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. Entrez les critères de recherche hello que vous souhaitez tooreuse, puis cliquez sur **enregistrer**.

    ![Attribution d’un nom à la recherche enregistrée dans les paramètres Recherche actuelle](./media/data-catalog-how-to-save-pin/02-name.png)

3. Lorsque vous êtes invité, entrez un nom pour hello recherche enregistrée. Choisissez un nom qui est significatif et qui décrit les ressources de données hello qui seront retournées par la recherche de hello.

### <a name="manage-saved-searches"></a>Gérer les recherches enregistrées
Après avoir enregistré une ou plusieurs des recherches, une **recherches enregistrées** option s’affiche sous hello **recherche actuelle** boîte. Lors de la liste de hello est développée, toutes les recherches enregistrées sont affichées.

 ![Liste des recherches enregistrées](./media/data-catalog-how-to-save-pin/03-list.png)

Effectuez hello suivantes :

* tooexecute une recherche, sélectionnez une recherche enregistrée dans la liste de hello.

* tooview une liste d’options de gestion d’une recherche enregistrée, cliquez sur hello nom recherche toohello suivant de flèche vers le bas.

    ![Options de gestion des recherches enregistrées](./media/data-catalog-how-to-save-pin/04-managing.png)

* tooenter un nouveau nom pour la recherche de hello enregistré, sélectionnez **renommer**. définition de recherche Hello n’est pas modifiée.

* recherche de hello enregistré tooremove dans votre liste, sélectionnez **supprimer**, puis confirmez la suppression de hello.

* recherche de hello enregistré toomark en tant que la recherche par défaut, sélectionnez **enregistrer en tant que valeur par défaut**. Si vous effectuez une recherche « vide » à partir de la page d’accueil Azure Data Catalog hello, votre recherche par défaut est exécutée. En outre, hello recherche qui est marqué comme la recherche par défaut de hello est affiché en haut de hello de hello **recherches enregistrées** liste.

### <a name="organizational-saved-searches"></a>Recherches enregistrées organisationnelles
Tous les utilisateurs de votre organisation peuvent enregistrer des recherches pour leur propre usage. Les administrateurs de catalogue de données peuvent également enregistrer des recherches pour tous les utilisateurs au sein de l’organisation de hello. Lorsque les administrateurs enregistrement une recherche, elles apparaissent avec un **partage au sein de la société de hello** option. En sélectionnant cette hello de partages option enregistré de recherche pour tous les utilisateurs dans l’organisation de hello.

 ![Recherches enregistrées organisationnelles](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a>Ressources de données épinglées
Les recherches enregistrées vous permettent d’enregistrer et de réutiliser les définitions de recherche. ressources de données Hello qui sont retournées par les recherches de hello peuvent changer au fil du temps en tant que contenu hello de modification de catalogue hello. Quand vous épinglez des ressources de données, vous pouvez identifier de manière explicite toomake actifs de données spécifique les tooaccess plus facilement sans avoir besoin de toouse une recherche.

L’épinglage d’une ressource de données est simple. tooadd hello données asset tooyour épinglé la liste, cliquez simplement sur hello **code confidentiel** icône. icône de Hello s’affiche dans hello de vignette d’élément multimédia hello dans l’affichage en mosaïque hello et dans la colonne la plus à gauche de hello dans la vue de liste de hello dans le portail d’Azure Data Catalog hello.

![icône d’épingle Hello ressource de données](./media/data-catalog-how-to-save-pin/05-pinning.png)

Le désépinglage d’une ressource de données est tout aussi simple. Cliquez simplement sur hello **désépingler** paramètre de hello tootoggle icône pour un composant sélectionné de hello.

![icône de ressource de données Hello détacher](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="hello-my-assets-section"></a>Hello section de mes ressources
Hello Data Catalog, page d’accueil du portail inclut un **mes ressources** section qui affiche les ressources de l’utilisateur actuel de toohello qui vous intéresse. Cette section inclut à la fois les ressources épinglées et les recherches enregistrées.

![Hello section Mes actifs sur la page d’accueil hello](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a>Résumé
Azure Data Catalog offre des fonctionnalités qui le rendent plus facile toodiscover hello des sources de données que vous avez besoin, que vous et autres membres de l’organisation peuvent consacrer moins de temps et en plus de temps avec lui. Les recherches enregistrées et l’épinglage des ressources de données viennent s’ajouter à ces fonctionnalités pour que les utilisateurs puissent identifier facilement les sources de données qu’ils utilisent le plus souvent.
