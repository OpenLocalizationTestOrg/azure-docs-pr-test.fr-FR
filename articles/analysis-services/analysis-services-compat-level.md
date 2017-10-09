---
title: "niveau de compatibilité de modèle aaaData dans Azure Analysis Services | Documents Microsoft"
description: "Présentation du niveau de compatibilité des modèles de données tabulaires."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/16/2017
ms.author: owend
ms.openlocfilehash: bfaf0c60666729d1e6e0baf082c046ea9faa4e86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a><span data-ttu-id="0e890-103">Niveau de compatibilité pour les modèles tabulaires Analysis Services</span><span class="sxs-lookup"><span data-stu-id="0e890-103">Compatibility level for Analysis Services tabular models</span></span>

<span data-ttu-id="0e890-104">*Niveau de compatibilité* fait référence à des comportements spécifiques aux toorelease dans Analysis Services moteur de hello.</span><span class="sxs-lookup"><span data-stu-id="0e890-104">*Compatibility level* refers toorelease-specific behaviors in hello Analysis Services engine.</span></span> <span data-ttu-id="0e890-105">Niveau de compatibilité toohello modifications qu’il coïncide avec les versions principales de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0e890-105">Changes toohello compatibility level typically coincide with major releases of SQL Server.</span></span> <span data-ttu-id="0e890-106">Ces modifications sont également implémentées dans parité de toomaintain Azure Analysis Services entre les deux plateformes.</span><span class="sxs-lookup"><span data-stu-id="0e890-106">These changes are also implemented in Azure Analysis Services toomaintain parity between both platforms.</span></span> <span data-ttu-id="0e890-107">Les modifications du niveau de compatibilité affectent également les fonctionnalités disponibles dans vos modèles tabulaires.</span><span class="sxs-lookup"><span data-stu-id="0e890-107">Compatibility level changes also affect features available in your tabular models.</span></span> <span data-ttu-id="0e890-108">Par exemple, DirectQuery et les métadonnées de l’objet sous forme de tableau ont des implémentations différentes en fonction du niveau de compatibilité hello.</span><span class="sxs-lookup"><span data-stu-id="0e890-108">For example, DirectQuery and tabular object metadata have different implementations depending on hello compatibility level.</span></span> 

<span data-ttu-id="0e890-109">Azure Analysis Services prend en charge les niveaux de compatibilité hello 1200 et 1400 les modèles tabulaires.</span><span class="sxs-lookup"><span data-stu-id="0e890-109">Azure Analysis Services supports tabular models at hello 1200 and 1400 compatibility levels.</span></span>

<span data-ttu-id="0e890-110">niveau de compatibilité plus récent Hello est 1400.</span><span class="sxs-lookup"><span data-stu-id="0e890-110">hello latest compatibility level is 1400.</span></span> <span data-ttu-id="0e890-111">Ce niveau coïncide avec SQL Server 2017 Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="0e890-111">This level coincides with SQL Server 2017 Analysis Services.</span></span> <span data-ttu-id="0e890-112">Principales fonctionnalités hello 1400 au niveau de compatibilité sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="0e890-112">Major features in hello 1400 compatibility level include:</span></span>

*  <span data-ttu-id="0e890-113">Nouvelle infrastructure pour la connectivité de données et l’importation dans les modèles tabulaires avec prise en charge des API TOM et des scripts TMSL.</span><span class="sxs-lookup"><span data-stu-id="0e890-113">New infrastructure for data connectivity and import into tabular models with support for TOM APIs and TMSL scripting.</span></span> <span data-ttu-id="0e890-114">Cette nouvelle fonctionnalité permet la prise en charge de sources de données supplémentaires, comme le stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="0e890-114">This new feature enables support for additional data sources such as Azure Blob storage.</span></span>
*  <span data-ttu-id="0e890-115">Fonctionnalités de transformation de données et de mashup des données à l’aide d’expressions Obtenir les données et M.</span><span class="sxs-lookup"><span data-stu-id="0e890-115">Data transformation and data mashup capabilities by using Get Data and M expressions.</span></span>
*  <span data-ttu-id="0e890-116">Les mesures prennent en charge une propriété Lignes de détails avec une expression DAX.</span><span class="sxs-lookup"><span data-stu-id="0e890-116">Measures support a Detail Rows property with a DAX expression.</span></span> <span data-ttu-id="0e890-117">Cette propriété Active les outils clients tels que toodrill Microsoft Excel toodetailed des données à partir d’un rapport.</span><span class="sxs-lookup"><span data-stu-id="0e890-117">This property enables client tools like Microsoft Excel toodrill down toodetailed data from an aggregated report.</span></span> <span data-ttu-id="0e890-118">Par exemple, lorsque les utilisateurs consultent le total des ventes pour une région ou le mois, ils peuvent afficher les détails de la commande hello associé.</span><span class="sxs-lookup"><span data-stu-id="0e890-118">For example, when users view total sales for a region and month, they can view hello associated order details.</span></span> 
*  <span data-ttu-id="0e890-119">Sécurité au niveau de l’objet de table et de colonne noms en outre toohello des données au sein de celles-ci.</span><span class="sxs-lookup"><span data-stu-id="0e890-119">Object-level security for table and column names, in addition toohello data within them.</span></span>
*  <span data-ttu-id="0e890-120">Prise en charge améliorée des hiérarchies déséquilibrées.</span><span class="sxs-lookup"><span data-stu-id="0e890-120">Enhanced support for ragged hierarchies.</span></span>
*  <span data-ttu-id="0e890-121">Amélioration des performances et de la surveillance.</span><span class="sxs-lookup"><span data-stu-id="0e890-121">Performance and monitoring improvements.</span></span>
  
## <a name="set-compatibility-level"></a><span data-ttu-id="0e890-122">Définir le niveau de compatibilité</span><span class="sxs-lookup"><span data-stu-id="0e890-122">Set compatibility level</span></span> 
 <span data-ttu-id="0e890-123">Lorsque vous créez un nouveau projet de modèle tabulaire dans SSDT, vous pouvez spécifier le niveau de compatibilité hello sur hello **Générateur de modèles tabulaires** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0e890-123">When creating a new tabular model project in SSDT, you can specify hello compatibility level on hello **Tabular model designer** dialog.</span></span> 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 <span data-ttu-id="0e890-125">Si vous sélectionnez hello **ne plus afficher ce message** option, tous les projets suivants utilisent niveau de compatibilité de hello vous avez spécifié comme valeur par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="0e890-125">If you select hello **Do not show this message again** option, all subsequent projects use hello compatibility level you specified as hello default.</span></span> <span data-ttu-id="0e890-126">Vous pouvez modifier le niveau de compatibilité par défaut hello dans SSDT sous **outils** > **Options**.</span><span class="sxs-lookup"><span data-stu-id="0e890-126">You can change hello default compatibility level in SSDT in **Tools** > **Options**.</span></span>  
  
 <span data-ttu-id="0e890-127">tooupgrade un projet de modèle tabulaire existant dans SSDT, jeu hello **le niveau de compatibilité** propriété hello modèle **propriétés** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="0e890-127">tooupgrade an existing tabular model project in SSDT, set  hello **Compatibility Level** property in hello model **Properties** window.</span></span> <span data-ttu-id="0e890-128">Gardez à l’esprit, la mise à niveau le niveau de compatibilité hello est irréversible.</span><span class="sxs-lookup"><span data-stu-id="0e890-128">Keep in-mind, upgrading hello compatibility level is irreversible.</span></span>
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a><span data-ttu-id="0e890-129">Vérifier le niveau de compatibilité d’une base de données de modèles tabulaires dans SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="0e890-129">Check compatibility level for a tabular model database in SQL Server Management Studio</span></span> 
 <span data-ttu-id="0e890-130">Dans SSMS, cliquez sur le nom de base de données hello > **propriétés** > **le niveau de compatibilité**.</span><span class="sxs-lookup"><span data-stu-id="0e890-130">In SSMS, right-click hello database name > **Properties** > **Compatibility Level**.</span></span>  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a><span data-ttu-id="0e890-131">Vérifier le niveau de compatibilité pris en charge pour un serveur dans SSMS</span><span class="sxs-lookup"><span data-stu-id="0e890-131">Check supported compatibility level for a server in SSMS</span></span>  
 <span data-ttu-id="0e890-132">Dans SSMS, cliquez sur le nom du serveur hello > **propriétés** > **pris en charge un niveau de compatibilité**.</span><span class="sxs-lookup"><span data-stu-id="0e890-132">In SSMS, right-click hello server name>  **Properties** > **Supported Compatibility Level**.</span></span>  
  
 <span data-ttu-id="0e890-133">Cette propriété spécifie hello plus haut niveau de compatibilité d’une base de données qui s’exécutent sur serveur hello (à l’exception de la version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="0e890-133">This property specifies hello highest compatibility level of a database that will run on hello server (excluding preview).</span></span> <span data-ttu-id="0e890-134">Hello pris en charge le niveau de compatibilité ne peut pas être modifié.</span><span class="sxs-lookup"><span data-stu-id="0e890-134">hello supported compatibility level cannot be changed.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="0e890-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0e890-135">Next steps</span></span>
  <span data-ttu-id="0e890-136">[Créer un modèle dans le portail Azure](analysis-services-create-model-portal.md) </span><span class="sxs-lookup"><span data-stu-id="0e890-136">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span></span>  
  [<span data-ttu-id="0e890-137">Gérer Analysis Services</span><span class="sxs-lookup"><span data-stu-id="0e890-137">Manage Analysis Services</span></span>](analysis-services-manage.md)  
