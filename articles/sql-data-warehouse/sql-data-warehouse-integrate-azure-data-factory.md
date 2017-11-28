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
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a><span data-ttu-id="759a6-103">Utiliser Azure Data Factory avec SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="759a6-103">Use Azure Data Factory with SQL Data Warehouse</span></span>
<span data-ttu-id="759a6-104">Azure Data Factory fournit une méthode entièrement gérée pour orchestrer le transfert hello de données et de l’exécution de procédures stockées sur SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="759a6-104">Azure Data Factory provides a fully managed method for orchestrating hello transfer of data and execution of stored procedures on SQL Data Warehouse.</span></span>  <span data-ttu-id="759a6-105">Cela vous permettra de toomore facilement configuration et planification extraire de transformation et chargement (ETL) des procédures complexes avec l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="759a6-105">This will allow you toomore easily set-up and schedule complex Extract Transform and Load (ETL) procedures with SQL Data Warehouse.</span></span> <span data-ttu-id="759a6-106">Pour obtenir une présentation plus complète de Azure Data Factory, consultez hello [documentation d’Azure Data Factory][Azure Data Factory documentation].</span><span class="sxs-lookup"><span data-stu-id="759a6-106">For a more complete overview of Azure Data Factory, see hello [Azure Data Factory documentation][Azure Data Factory documentation].</span></span>

## <a name="data-movement"></a><span data-ttu-id="759a6-107">Déplacement des données</span><span class="sxs-lookup"><span data-stu-id="759a6-107">Data Movement</span></span>
<span data-ttu-id="759a6-108">Azure Data Factory permet le déplacement des données entre des sources locales, mais également entre divers services Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="759a6-108">Azure Data Factory enables data movement between both on-premises sources and different Azure services.</span></span>  <span data-ttu-id="759a6-109">Une intégration globale actuelle avec Azure Data Factory prend en charge tooand de déplacement des données à partir de hello emplacements suivants :</span><span class="sxs-lookup"><span data-stu-id="759a6-109">Overall, current integration with Azure Data Factory supports data movement tooand from hello following locations:</span></span>

* <span data-ttu-id="759a6-110">Stockage des objets blob</span><span class="sxs-lookup"><span data-stu-id="759a6-110">Azure blob storage</span></span>
* <span data-ttu-id="759a6-111">Base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="759a6-111">Azure SQL Database</span></span>
* <span data-ttu-id="759a6-112">SQL Server local</span><span class="sxs-lookup"><span data-stu-id="759a6-112">On-premises SQL Server</span></span>
* <span data-ttu-id="759a6-113">SQL Server sur IaaS</span><span class="sxs-lookup"><span data-stu-id="759a6-113">SQL Server on IaaS</span></span>

<span data-ttu-id="759a6-114">Pour plus d’informations sur comment tooset les données d’une activité de copie, consultez [copier des données avec Azure Data Factory][Copy data with Azure Data Factory]</span><span class="sxs-lookup"><span data-stu-id="759a6-114">For information on how tooset up a data copy activity see [Copy data with Azure Data Factory][Copy data with Azure Data Factory]</span></span>

## <a name="stored-procedures"></a><span data-ttu-id="759a6-115">Procédures stockées</span><span class="sxs-lookup"><span data-stu-id="759a6-115">Stored Procedures</span></span>
 <span data-ttu-id="759a6-116">Bonjour même façon qu’il peut être utilisé tooschedule de transfert de données peut d’Azure Data Factory être exécution de hello tooorchestrate utilisé des procédures stockées.</span><span class="sxs-lookup"><span data-stu-id="759a6-116">In hello same way it can be used tooschedule data transfer, Azure Data Factory can also be used tooorchestrate hello execution of stored procedures.</span></span>  <span data-ttu-id="759a6-117">Ainsi, plus complexe toobe pipelines créé et étend capacité tooleverage hello une puissance de calcul la fabrique de données Azure de l’entrepôt de données SQL.</span><span class="sxs-lookup"><span data-stu-id="759a6-117">This allows more complex pipelines toobe created and extends Azure Data Factory's ability tooleverage hello computational power of SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="759a6-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="759a6-118">Next steps</span></span>
<span data-ttu-id="759a6-119">Pour une vue d’ensemble de l’intégration, consultez [Vue d’ensemble sur l’intégration de SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="759a6-119">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>
<span data-ttu-id="759a6-120">Pour obtenir des conseils supplémentaires en matière de développement, consultez l’article [Vue d’ensemble sur le développement SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="759a6-120">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

