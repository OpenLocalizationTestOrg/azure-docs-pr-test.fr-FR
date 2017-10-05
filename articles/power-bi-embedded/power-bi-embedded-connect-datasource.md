---
title: "Microsoft Power BI Embedded - Connexion à une source de données"
description: "Power BI Embedded, se connecter aux sources de données"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 9f614bbc63eae788aa52132c8f0e42ad8963559a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-a-data-source"></a>Se connecter à une source de données
Avec **Power BI Embedded**, vous pouvez incorporer des rapports dans votre propore application. Lorsque vous incorporez un rapport Power BI dans votre application, celui-ci se connecte aux données sous-jacentes par **importation** d’une copie des données ou par **connexion directe** à la source de données via **DirectQuery**.

Voici les différences entre l’**importation** et l’utilisation de **DirectQuery**.

| Importer | DirectQuery |
| --- | --- |
| Les tables, colonnes *et données* sont importées ou copiées dans le jeu de données du rapport. Pour voir les modifications apportées aux données sous-jacentes, vous devez actualiser ou réimporter un jeu de données à jour et complet. |Seules les *tables et colonnes* sont importées ou copiées dans le jeu de données du rapport. Vous visualisez toujours les données les plus récentes. |

Power BI Embedded vous permet d’utiliser DirectQuery avec des sources de données cloud mais pas des sources de données locales, pour l’instant.

> [!NOTE]
> La passerelle de données locale n’est pas prise en charge avec Power BI Embedded pour l’instant. Cela signifie que vous ne pouvez pas utiliser DirectQuery avec des sources de données locales.

## <a name="supported-data-sources"></a>Sources de données prises en charge

**DirectQuery**
* Base de données SQL Azure
* Azure SQL Data Warehouse

**Importationation**

Vous pouvez importer à l’aide de toutes les sources de données disponibles dans Power BI Desktop. Vous ne pourrez **pas** actualiser ces données dans Power BI Embedded. Vous devrez télécharger les modifications apportées à votre fichier PBIX dans Power BI Embedded. Cela est dû à l’absence de passerelle disponible. 

## <a name="benefits-of-using-directquery"></a>Avantages de l'utilisation de DirectQuery
Il existe deux grands avantages à utiliser **DirectQuery**:

* **DirectQuery** vous permet de créer des visualisations sur des jeux de données très volumineux, là où il serait impossible d’importer d’abord toutes les données.
* La modification des données sous-jacentes peut nécessiter une actualisation des données, et pour certains rapports, l’affichage des données en cours peut nécessiter des transferts de données volumineux, empêchant la réimportation des données. En revanche, les rapports **DirectQuery** utilisent toujours les données actuelles.

## <a name="limitations-of-directquery"></a>Limitations de DirectQuery
   Il existe quelques limitations à l’utilisation de **DirectQuery**:

* Toutes les tables doivent provenir d'une même base de données.
* Si la requête est trop complexe, une erreur se produit. Pour corriger l'erreur, vous devez refactoriser la requête afin de la simplifier. Si la requête doit être complexe, vous devez importer les données au lieu d’utiliser **DirectQuery**.
* Le filtrage de la relation s’effectue dans un seul sens, et non dans les deux sens.
* Vous ne pouvez pas modifier le type de données d'une colonne.
* Par défaut, les limitations s’appliquent aux expressions DAX autorisées dans les mesures. Voir [DirectQuery et mesures](#measures).

<a name="measures"/>

## <a name="directquery-and-measures"></a>DirectQuery et mesures
Pour garantir que les requêtes envoyées à la source de données sous-jacente sont suffisamment performantes, des limitations s’appliquent aux mesures. Lorsque vous utilisez **Power BI Desktop**, les utilisateurs avancés peuvent contourner cette limitation en choisissant **Fichier > Options et paramètres > Options**. Dans la boîte de dialogue **Options**, choisissez **DirectQuery**, puis sélectionnez l’option **Autoriser des mesures sans restriction en mode DirectQuery**. Lorsque cette option est sélectionnée, toute expression DAX valide pour une mesure peut être utilisée. Cependant, les utilisateurs doivent être conscients que certaines expressions qui fonctionnent très bien lorsque les données sont importées peuvent entraîner des requêtes très lentes vers la source principale en mode **DirectQuery** . 

## <a name="see-also"></a>Voir aussi
* [Prise en main de Microsoft Power BI Embedded](power-bi-embedded-get-started.md)
* [Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

Des questions ? [Essayer la communauté Power BI](http://community.powerbi.com/)

