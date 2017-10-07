---
title: aaaUse Azure Data Factory et SQL Data Warehouse | Documents Microsoft
description: "Conseils sur l’utilisation de Microsoft Azure Data Factory avec Microsoft Azure SQL Data Warehouse, dans le cadre du développement de solutions."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 492de762-c7a2-4cdb-943f-3135230e94f1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d40a547830f9681504253d39ae3066800a955c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a>Utiliser Azure Data Factory avec SQL Data Warehouse
Azure Data Factory fournit une méthode entièrement gérée pour orchestrer le transfert hello de données et de l’exécution de procédures stockées sur SQL Data Warehouse.  Cela vous permettra de toomore facilement configuration et planification extraire de transformation et chargement (ETL) des procédures complexes avec l’entrepôt de données SQL. Pour obtenir une présentation plus complète de Azure Data Factory, consultez hello [documentation d’Azure Data Factory][Azure Data Factory documentation].

## <a name="data-movement"></a>Déplacement des données
Azure Data Factory permet le déplacement des données entre des sources locales, mais également entre divers services Microsoft Azure.  Une intégration globale actuelle avec Azure Data Factory prend en charge tooand de déplacement des données à partir de hello emplacements suivants :

* Stockage des objets blob
* Base de données SQL Azure
* SQL Server local
* SQL Server sur IaaS

Pour plus d’informations sur comment tooset les données d’une activité de copie, consultez [copier des données avec Azure Data Factory][Copy data with Azure Data Factory]

## <a name="stored-procedures"></a>Procédures stockées
 Bonjour même façon qu’il peut être utilisé tooschedule de transfert de données peut d’Azure Data Factory être exécution de hello tooorchestrate utilisé des procédures stockées.  Ainsi, plus complexe toobe pipelines créé et étend capacité tooleverage hello une puissance de calcul la fabrique de données Azure de l’entrepôt de données SQL.

## <a name="next-steps"></a>Étapes suivantes
Pour une vue d’ensemble de l’intégration, consultez [Vue d’ensemble sur l’intégration de SQL Data Warehouse][SQL Data Warehouse integration overview].
Pour obtenir des conseils supplémentaires en matière de développement, consultez l’article [Vue d’ensemble sur le développement SQL Data Warehouse][SQL Data Warehouse development overview].

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

