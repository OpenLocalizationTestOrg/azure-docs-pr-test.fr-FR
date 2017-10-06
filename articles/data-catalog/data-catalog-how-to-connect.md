---
title: sources de toodata aaaHow tooconnect | Documents Microsoft
description: "Tooarticle de la mise en surbrillance le mode de détection de tooconnect toodata sources avec Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 4e6b27a5-cf75-4012-b88c-333c1fe638e8
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 01d659510c8e67c1238ed488f4eebf511aab7217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-toodata-sources"></a>Comment tooconnect toodata sources
## <a name="introduction"></a>Introduction
**Microsoft Azure Data Catalog** est un service cloud entièrement géré qui sert de système d'inscription et de détection des sources de données d'entreprise. En d’autres termes, **Azure Data Catalog** est tout sur aidant les utilisateurs à découvrir, comprendre et utiliser des sources de données, et aider les organisations tooget plus la valeur à partir de leurs données. Un aspect clé de ce scénario utilise hello source de données : une fois qu’un utilisateur découvre une données et comprend son objectif, étape suivante de hello est source de données de toohello de tooconnect tooput toouse de ses données.

## <a name="data-source-locations"></a>Emplacements des sources de données
Lors de l’enregistrement de source de données, **Azure Data Catalog** reçoit des métadonnées sur la source de données hello. Ces métadonnées incluent des détails hello d’emplacement de la source de données hello. Détails de Hello d’emplacement de hello varie à partir de la source de données source toodata, mais il contient toujours hello informations nécessaires tooconnect. Par exemple, emplacement hello pour une table SQL Server inclut les nom hello du serveur, nom de la base de données, nom de schéma et nom de la table, alors que l’emplacement du hello pour un rapport SQL Server Reporting Services inclut le nom du serveur hello et rapport de toohello hello chemin d’accès. Autres types de sources de données aura des emplacements qui reflètent la structure de hello et des capacités du système source de hello.

## <a name="integrated-client-tools"></a>Outils clients intégrés
source de données du tooa tooconnect de la façon la plus simple Hello est toouse hello « ouvrir dans... » menu Bonjour **Azure Data Catalog** portal. Ce menu affiche une liste des options de connexion actifs de données sélectionnée toohello.
Lorsque vous utilisez l’affichage en mosaïque hello par défaut, ce menu est disponible sur hello chaque mosaïque.

 ![Ouverture d’une table SQL Server dans Excel à partir de la vignette d’élément multimédia hello données](./media/data-catalog-how-to-connect/data-catalog-how-to-connect1.png)

Lors de l’affichage de liste hello, hello est disponible dans le volet de recherche hello haut hello de fenêtre du portail hello.

 ![Ouverture d’un rapport SQL Server Reporting Services dans le Gestionnaire de rapports à partir de la barre de recherche hello](./media/data-catalog-how-to-connect/data-catalog-how-to-connect2.png)

## <a name="supported-client-applications"></a>Applications clientes prises en charge
Lorsque vous utilisez hello « ouvrir dans... » menu pour les données sources dans le portail d’Azure Data Catalog hello, application de hello client approprié doit être installée sur l’ordinateur client de hello.

| Ouvrir dans l’application | Extension de fichier/protocole | Versions d’application prises en charge |
| --- | --- | --- |
| Excel |.odc |Excel 2010 ou version ultérieure |
| Excel (1 000 premiers) |.odc |Excel 2010 ou version ultérieure |
| Power Query |.xlsx |Excel 2016 ou Excel 2010 ou Excel 2013 avec hello Power Query pour Excel installé |
| Power BI Desktop |.pbix |Power BI Desktop juillet 2016 ou version ultérieure |
| SQL Server Data Tools |vsweb:// |Visual Studio 2013 Update 4 ou version ultérieure avec les outils SQL Server installés |
| Gestionnaire de rapports |http:// |Voir la [configuration de navigateur requise pour SQL Server Reporting Services](https://technet.microsoft.com/en-us/library/ms156511.aspx) |

## <a name="your-data-your-tools"></a>Vos données, vos outils
options de Hello disponibles dans le menu de hello dépendent de type hello de ressource de données actuellement sélectionnée. Bien entendu, les outils possibles seront incluses dans hello « ouvrir dans... » menu, mais il est encore facile tooconnect toohello data source à l’aide de n’importe quel outil client. Lorsqu’une ressource de données est sélectionnée dans hello **Azure Data Catalog** portail, emplacement complet de hello est affiché dans le volet de propriétés hello.

 ![Informations de connexion pour une table SQL Server](./media/data-catalog-how-to-connect/data-catalog-how-to-connect3.png)

les informations de connexion Hello détails seront différents de type de source de toodata de type de source de données, mais les informations hello inclus dans le portail de hello vous donneront tout ce dont vous avez besoin de source de données tooconnect toohello dans n’importe quel outil client. Les utilisateurs peuvent copier les détails de la connexion hello pour les sources de données hello qui ils ont découverts à l’aide de **Azure Data Catalog**, leur permettant ainsi de toowork avec des données hello dans leur outil de choix.

## <a name="connecting-and-data-source-permissions"></a>Connexion et autorisations de sources de données
Bien que **Azure Data Catalog** rend les sources de données access détectable, toohello les données proprement dite restent sous contrôle de code hello du propriétaire hello de la source de données ou administrateur. Détection d’une source de données dans **Azure Data Catalog** ne donne pas un utilisateur les autorisations tooaccess hello source de données.

toomake plus facile pour les utilisateurs de découvrir les données source mais n’ont pas d’autorisation tooaccess ses données, les utilisateurs peuvent fournir des informations Bonjour propriété de demande d’accès lors de l’annotation d’une source de données. Les informations fournies ici, notamment des liens toohello a ou le point de contact pour obtenir un accès aux sources de données – sont présentées en même temps que les informations d’emplacement hello données source dans le portail de hello.

 ![Informations de connexion avec fourniture des instructions d’accès de requête](./media/data-catalog-how-to-connect/data-catalog-how-to-connect4.png)

## <a name="summary"></a>Résumé
Inscription d’une source de données avec **Azure Data Catalog** identifiables que les données en copiant les métadonnées structurelles et descriptive à partir de la source de données hello dans hello service du catalogue. Une fois qu’une source de données a été enregistrée et découverts, les utilisateurs peuvent se connecter à source de données toohello de hello **Azure Data Catalog** portail « ouvrir dans... » » ou à l’aide des outils de données de leur choix.

## <a name="see-also"></a>Voir aussi
* [Prise en main Azure Data Catalog](data-catalog-get-started.md) didacticiel pour plus d’informations détaillées sur la façon tooconnect toodata sources.
