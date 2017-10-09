---
title: "aaaMicrosoft Power BI Embedded - source de données tooa connexion"
description: Power BI Embedded, connecter des sources de toodata
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
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a>Connectez la source de données tooa
Avec **Power BI Embedded**, vous pouvez incorporer des rapports dans votre propore application. Lorsque vous incorporez un rapport Power BI dans votre application, les rapports hello connecte toohello sous-jacente des données par **importation** une copie de données de hello ou par **connexion directe** à l’aide de source de données toohello  **DirectQuery**.

Voici hello les différences entre l’utilisation de **importation** et **DirectQuery**.

| Importer | DirectQuery |
| --- | --- |
| Tables, colonnes, *et données* sont importées ou copiées dans le jeu de données du rapport hello. toosee modifie les données sous-jacentes toohello s’est produite, vous devez actualiser ou importez, à nouveau un dataset complet, en cours. |Uniquement *tables et colonnes* sont importées ou copiées dans le jeu de données du rapport hello. Vous toujours Affichez les données les plus récentes hello. |

Power BI Embedded vous permet d’utiliser DirectQuery avec des sources de données cloud mais pas des sources de données locales, pour l’instant.

> [!NOTE]
> Hello passerelle de données locale n'est pas pris en charge avec Power BI incorporé pour l’instant. Cela signifie que vous ne pouvez pas utiliser DirectQuery avec des sources de données locales.

## <a name="supported-data-sources"></a>Sources de données prises en charge

**DirectQuery**
* Base de données SQL Azure
* Azure SQL Data Warehouse

**Importationation**

Vous pouvez importer à l’aide de toutes les sources de données disponibles hello dans Power BI Desktop. Vous allez **pas** être en mesure de toorefresh ces données dans Power BI Embedded. Vous devez les modifications tooupload tooyour PBIX tooPower BI incorporée du fichier. Il s’agit en raison de la passerelle disponible de toono. 

## <a name="benefits-of-using-directquery"></a>Avantages de l'utilisation de DirectQuery
Il existe deux grands avantages à utiliser **DirectQuery**:

* **DirectQuery** vous permet de créer des visualisations sur des jeux de données très volumineux, où il sinon serait irréalisable toofirst importation tous hello des données.
* Modification des données sous-jacentes peuvent exiger une actualisation des données et pour certains rapports, hello doivent toodisplay les données actuelles nécessite des transferts de données volumineux, effectuer une nouvelle importation des données irréalisable. En revanche, les rapports **DirectQuery** utilisent toujours les données actuelles.

## <a name="limitations-of-directquery"></a>Limitations de DirectQuery
   Il existe quelques limitations toousing **DirectQuery**:

* Toutes les tables doivent provenir d'une même base de données.
* Si la requête de hello est trop complexe, une erreur se produit. Erreur de hello tooremedy, vous devez refactoriser les requête hello afin qu’il soit moins complexe. Si la requête de hello doit être complexe, vous devez tooimport les données de salutation au lieu d’utiliser **DirectQuery**.
* Filtrage de la relation est limité tooa direction à sens unique, plutôt que les deux sens.
* Vous ne pouvez pas modifier le type de données hello d’une colonne.
* Par défaut, les limitations s’appliquent aux expressions DAX autorisées dans les mesures. Voir [DirectQuery et mesures](#measures).

<a name="measures"/>

## <a name="directquery-and-measures"></a>DirectQuery et mesures
requêtes tooensure envoyés toohello source de données sous-jacente des performances acceptables, les limitations sont imposées aux mesures. Lorsque vous utilisez **Power BI Desktop**avancées les utilisateurs peuvent choisir toobypass cette limitation en choisissant **fichier > Options et paramètres > Options**. Bonjour **Options** boîte de dialogue, choisissez **DirectQuery**, puis sélectionnez l’option de hello **autoriser des mesures sans restriction en mode DirectQuery**. Lorsque cette option est sélectionnée, toute expression DAX valide pour une mesure peut être utilisée. Les utilisateurs doivent connaître ; Toutefois, que certaines expressions qui fonctionnent très bien lors de l’importation de données de salutation peut entraîner des requêtes très lentes toohello principal dans la source **DirectQuery** mode. 

## <a name="see-also"></a>Voir aussi
* [Prise en main de Microsoft Power BI Embedded](power-bi-embedded-get-started.md)
* [Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

Des questions ? [Essayez de hello Communauté Power BI](http://community.powerbi.com/)

