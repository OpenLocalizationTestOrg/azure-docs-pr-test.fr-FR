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
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="a3878-103">Tirer parti d’autres services avec SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a3878-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="a3878-104">En outre les fonctionnalités de base de tooits, entrepôt de données SQL permet aux utilisateurs tooleverage nombreux hello autres services dans Azure à ses côtés.</span><span class="sxs-lookup"><span data-stu-id="a3878-104">In addition tooits core functionality, SQL Data Warehouse enables users tooleverage many of hello other services in Azure alongside it.</span></span>  <span data-ttu-id="a3878-105">Plus précisément, nous avons pris actuellement les étapes toodeeply intégrer suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="a3878-105">Specifically, we have currently taken steps toodeeply integrate with hello following:</span></span>

* <span data-ttu-id="a3878-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="a3878-106">Power BI</span></span>
* <span data-ttu-id="a3878-107">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a3878-107">Azure Data Factory</span></span>
* <span data-ttu-id="a3878-108">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a3878-108">Azure Machine Learning</span></span>
* <span data-ttu-id="a3878-109">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a3878-109">Azure Stream Analytics</span></span>

<span data-ttu-id="a3878-110">Nous travaillons tooconnect avec davantage de services entre hello écosystème Azure.</span><span class="sxs-lookup"><span data-stu-id="a3878-110">We are working tooconnect with more services across hello Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="a3878-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="a3878-111">Power BI</span></span>
<span data-ttu-id="a3878-112">Intégration de Power BI vous permet de puissance de calcul hello tooleverage de l’entrepôt de données SQL avec la création de rapports dynamiques hello et visualisation de Power BI.</span><span class="sxs-lookup"><span data-stu-id="a3878-112">Power BI integration allows you tooleverage hello compute power of SQL Data Warehouse with hello dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="a3878-113">L’intégration de Power BI inclut actuellement les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a3878-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="a3878-114">**Connexion directe**: une connexion plus avancée avec un menu déroulant logique dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a3878-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="a3878-115">Ainsi, les analyses sont plus rapides à une plus grande échelle.</span><span class="sxs-lookup"><span data-stu-id="a3878-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="a3878-116">**Ouvrir dans Power BI**: bouton de « Ouvrir dans Power BI » hello passe instance informations tooPower BI, ce qui permet une connexion plus transparente.</span><span class="sxs-lookup"><span data-stu-id="a3878-116">**Open in Power BI**: hello 'Open in Power BI' button passes instance information tooPower BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="a3878-117">Consultez [intégrer avec Power BI](sql-data-warehouse-integrate-power-bi.md) ou hello [documentation de Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a3878-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or hello [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="a3878-118">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a3878-118">Azure Data Factory</span></span>
<span data-ttu-id="a3878-119">Azure Data Factory permet aux utilisateurs un toocreate plateforme managée que complexes d’extraction et chargement de pipelines.</span><span class="sxs-lookup"><span data-stu-id="a3878-119">Azure Data Factory gives users a managed platform toocreate complex Extract-Load pipelines.</span></span>  <span data-ttu-id="a3878-120">Intégration de SQL Data Warehouse avec Azure Data Factory inclut des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="a3878-120">SQL Data Warehouse's integration with Azure Data Factory includes hello following:</span></span>

* <span data-ttu-id="a3878-121">**Procédures stockées**: orchestrer des procédures stockées sur SQL Data Warehouse exécution hello.</span><span class="sxs-lookup"><span data-stu-id="a3878-121">**Stored Procedures**: Orchestrate hello execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="a3878-122">**Copie**: données de toomove utilisation ADF dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a3878-122">**Copy**: Use ADF toomove data into SQL Data Warehouse.</span></span>  <span data-ttu-id="a3878-123">Cette opération peut utiliser le mécanisme de déplacement des données standard de définition d’application ou PolyBase sous hello couvre.</span><span class="sxs-lookup"><span data-stu-id="a3878-123">This operation can use ADF's standard data movement mechanism or PolyBase under hello covers.</span></span> 

<span data-ttu-id="a3878-124">Consultez [intégrer à Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) ou hello [documentation d’Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a3878-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="a3878-125">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a3878-125">Azure Machine Learning</span></span>
<span data-ttu-id="a3878-126">Azure Machine Learning est un service entièrement géré analytique qui permet aux utilisateurs des modèles complexes toocreate tirant parti d’un grand ensemble d’outils prédictives.</span><span class="sxs-lookup"><span data-stu-id="a3878-126">Azure Machine Learning is a fully managed analytics service which allows users toocreate intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="a3878-127">Entrepôt de données SQL est pris en charge comme une source et la destination de ces modèles avec hello suivant de fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="a3878-127">SQL Data Warehouse is supported as both a source and destination for these models with hello following functionality:</span></span>

* <span data-ttu-id="a3878-128">**Lire les données :** pilotez des modèles à l’échelle à l’aide de T-SQL dans SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a3878-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="a3878-129">**Écriture de données :** de valider les modifications à partir de n’importe quel modèle sauvegarder tooSQL l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="a3878-129">**Write Data:** Commit changes from any model back tooSQL Data Warehouse.</span></span>

<span data-ttu-id="a3878-130">Consultez [intégrer à Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) ou hello [documentation d’Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a3878-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or hello [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="a3878-131">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a3878-131">Azure Stream Analytics</span></span>
<span data-ttu-id="a3878-132">Azure Stream Analytics est une infrastructure complexe, entièrement gérée pour le traitement et l’utilisation des données d’événement générées à partir d’Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="a3878-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="a3878-133">Intégration à SQL Data Warehouse permet de diffusion en continu traitées efficacement des données toobe et stockées en même temps que l’activation plus approfondie des données relationnelles, plus analyse avancée.</span><span class="sxs-lookup"><span data-stu-id="a3878-133">Integration with SQL Data Warehouse allows for streaming data toobe effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="a3878-134">**Sortie de tâche :** travaux de sortie d’envoi à partir de flux de données Analytique directement tooSQL l’entrepôt de données.</span><span class="sxs-lookup"><span data-stu-id="a3878-134">**Job Output:** Send output from Stream Analytics jobs directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="a3878-135">Consultez [intégrer à Azure flux Analytique](sql-data-warehouse-integrate-azure-stream-analytics.md) ou hello [documentation d’Azure Stream Analytique](https://azure.microsoft.com/documentation/services/stream-analytics/) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="a3878-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or hello [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

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
