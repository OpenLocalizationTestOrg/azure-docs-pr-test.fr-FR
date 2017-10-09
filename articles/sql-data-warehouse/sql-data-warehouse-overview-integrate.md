---
title: "aaaBuild des solutions intégrées avec l’entrepôt de données SQL | Documents Microsoft"
description: "Outils et partenaires proposant des solutions s’intégrant avec SQL Data Warehouse. "
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: e2dc8f3f-10e3-4589-a4e2-50c67dfcf67f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: c8a4202dd84305bea4e4c2faf0e4791d026e794f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a>Tirer parti d’autres services avec SQL Data Warehouse
En outre les fonctionnalités de base de tooits, entrepôt de données SQL permet aux utilisateurs tooleverage nombreux hello autres services dans Azure à ses côtés.  Plus précisément, nous avons pris actuellement les étapes toodeeply intégrer suivant de hello :

* Power BI
* Azure Data Factory
* Azure Machine Learning
* Azure Stream Analytics

Nous travaillons tooconnect avec davantage de services entre hello écosystème Azure.

## <a name="power-bi"></a>Power BI
Intégration de Power BI vous permet de puissance de calcul hello tooleverage de l’entrepôt de données SQL avec la création de rapports dynamiques hello et visualisation de Power BI. L’intégration de Power BI inclut actuellement les éléments suivants :

* **Connexion directe**: une connexion plus avancée avec un menu déroulant logique dans SQL Data Warehouse.  Ainsi, les analyses sont plus rapides à une plus grande échelle.
* **Ouvrir dans Power BI**: bouton de « Ouvrir dans Power BI » hello passe instance informations tooPower BI, ce qui permet une connexion plus transparente.

Consultez [intégrer avec Power BI](sql-data-warehouse-integrate-power-bi.md) ou hello [documentation de Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) pour plus d’informations.

## <a name="azure-data-factory"></a>Azure Data Factory
Azure Data Factory permet aux utilisateurs un toocreate plateforme managée que complexes d’extraction et chargement de pipelines.  Intégration de SQL Data Warehouse avec Azure Data Factory inclut des éléments suivants de hello :

* **Procédures stockées**: orchestrer des procédures stockées sur SQL Data Warehouse exécution hello.
* **Copie**: données de toomove utilisation ADF dans SQL Data Warehouse.  Cette opération peut utiliser le mécanisme de déplacement des données standard de définition d’application ou PolyBase sous hello couvre. 

Consultez [intégrer à Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) ou hello [documentation d’Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) pour plus d’informations.

## <a name="azure-machine-learning"></a>Azure Machine Learning
Azure Machine Learning est un service entièrement géré analytique qui permet aux utilisateurs des modèles complexes toocreate tirant parti d’un grand ensemble d’outils prédictives.  Entrepôt de données SQL est pris en charge comme une source et la destination de ces modèles avec hello suivant de fonctionnalités :

* **Lire les données :** pilotez des modèles à l’échelle à l’aide de T-SQL dans SQL Data Warehouse.
* **Écriture de données :** de valider les modifications à partir de n’importe quel modèle sauvegarder tooSQL l’entrepôt de données.

Consultez [intégrer à Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) ou hello [documentation d’Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) pour plus d’informations.

## <a name="azure-stream-analytics"></a>Azure Stream Analytics
Azure Stream Analytics est une infrastructure complexe, entièrement gérée pour le traitement et l’utilisation des données d’événement générées à partir d’Azure Event Hubs.  Intégration à SQL Data Warehouse permet de diffusion en continu traitées efficacement des données toobe et stockées en même temps que l’activation plus approfondie des données relationnelles, plus analyse avancée.  

* **Sortie de tâche :** travaux de sortie d’envoi à partir de flux de données Analytique directement tooSQL l’entrepôt de données.

Consultez [intégrer à Azure flux Analytique](sql-data-warehouse-integrate-azure-stream-analytics.md) ou hello [documentation d’Azure Stream Analytique](https://azure.microsoft.com/documentation/services/stream-analytics/) pour plus d’informations.

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop/

[Azure Data Factory]: sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: sql-data-warehouse-integrate-power-bi.md
[Partners]: sql-data-warehouse-partner-business-intelligence.md

<!--MSDN references-->

<!--Other Web references-->
