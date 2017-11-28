---
title: "aaaGet démarré avec Analytique de LAC de données Azure à l’aide du portail Azure | Documents Microsoft"
description: "Découvrez comment toouse hello toocreate portail Azure un compte Analytique lac de données, créez une tâche Analytique lac de données à l’aide de U-SQL et envoi de la tâche de hello. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a><span data-ttu-id="e54e2-103">Prise en main d’Azure Data Lake Analytics à l’aide du Portail Azure</span><span class="sxs-lookup"><span data-stu-id="e54e2-103">Get started with Azure Data Lake Analytics using Azure portal</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="e54e2-104">Découvrez comment toouse hello Azure toocreate portail des comptes Analytique de LAC de données Azure, définir des travaux dans [U-SQL](data-lake-analytics-u-sql-get-started.md)et soumettre le service de données Lake Analytique toohello travaux.</span><span class="sxs-lookup"><span data-stu-id="e54e2-104">Learn how toouse hello Azure portal toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="e54e2-105">Pour plus d’informations sur Analytique Data Lake, consultez [Présentation d’Analytique Data Lake Azure](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e54e2-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e54e2-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e54e2-106">Prerequisites</span></span>

<span data-ttu-id="e54e2-107">Avant de commencer ce didacticiel, vous devez disposer d’un **abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="e54e2-107">Before you begin this tutorial, you must have an **Azure subscription**.</span></span> <span data-ttu-id="e54e2-108">Consultez la rubrique [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e54e2-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="e54e2-109">Créer un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="e54e2-109">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="e54e2-110">Maintenant, vous allez créer un Analytique lac de données et un magasin Data Lake Store compte hello même temps.</span><span class="sxs-lookup"><span data-stu-id="e54e2-110">Now, you will create a Data Lake Analytics and a Data Lake Store account at hello same time.</span></span>  <span data-ttu-id="e54e2-111">Cette étape est simple et seulement prend environ 60 secondes toofinish.</span><span class="sxs-lookup"><span data-stu-id="e54e2-111">This step is simple and only takes about 60 seconds toofinish.</span></span>

1. <span data-ttu-id="e54e2-112">Ouverture de session toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e54e2-112">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e54e2-113">Cliquez sur **Nouveau** >  **Données + analyse** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="e54e2-113">Click **New** >  **Data + Analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="e54e2-114">Sélectionnez les valeurs de hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e54e2-114">Select values for hello following items:</span></span>
   * <span data-ttu-id="e54e2-115">**Nom** : donnez un nom à votre compte Data Lake Analytics (utilisez uniquement des lettres minuscules et des chiffres).</span><span class="sxs-lookup"><span data-stu-id="e54e2-115">**Name**: Name your Data Lake Analytics account (Only lower case letters and numbers allowed).</span></span>
   * <span data-ttu-id="e54e2-116">**Abonnement**: choisissez hello abonnement Azure utilisé pour le compte de l’Analytique de hello.</span><span class="sxs-lookup"><span data-stu-id="e54e2-116">**Subscription**: Choose hello Azure subscription used for hello Analytics account.</span></span>
   * <span data-ttu-id="e54e2-117">**Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="e54e2-117">**Resource Group**.</span></span> <span data-ttu-id="e54e2-118">Sélectionnez un groupe de ressources Azure existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="e54e2-118">Select an existing Azure Resource Group or create a new one.</span></span>
   * <span data-ttu-id="e54e2-119">**Emplacement**.</span><span class="sxs-lookup"><span data-stu-id="e54e2-119">**Location**.</span></span> <span data-ttu-id="e54e2-120">Sélectionnez un centre de données Azure pour compte Analytique lac de données de hello.</span><span class="sxs-lookup"><span data-stu-id="e54e2-120">Select an Azure data center for hello Data Lake Analytics account.</span></span>
   * <span data-ttu-id="e54e2-121">**Data Lake Store**: suivez hello instruction toocreate un nouveau compte Data Lake Store, ou sélectionnez-en un existant.</span><span class="sxs-lookup"><span data-stu-id="e54e2-121">**Data Lake Store**: Follow hello instruction toocreate a new Data Lake Store account, or select an existing one.</span></span> 
4. <span data-ttu-id="e54e2-122">Si vous le souhaitez, sélectionnez un niveau tarifaire pour votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="e54e2-122">Optionally, select a pricing tier for your Data Lake Analytics account.</span></span>
5. <span data-ttu-id="e54e2-123">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e54e2-123">Click **Create**.</span></span> 


## <a name="your-first-u-sql-script"></a><span data-ttu-id="e54e2-124">Votre premier script U-SQL</span><span class="sxs-lookup"><span data-stu-id="e54e2-124">Your first U-SQL script</span></span>

<span data-ttu-id="e54e2-125">Hello suivant le texte est un script U-SQL très simple.</span><span class="sxs-lookup"><span data-stu-id="e54e2-125">hello following text is a very simple U-SQL script.</span></span> <span data-ttu-id="e54e2-126">Il se définissent un jeu de données petit script de hello, puis écrivez ce jeu de données sortantes Data Lake Store toohello par défaut comme un fichier appelé `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="e54e2-126">All it does is define a small dataset within hello script and then write that dataset out toohello default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="e54e2-127">Envoyer un travail U-SQL</span><span class="sxs-lookup"><span data-stu-id="e54e2-127">Submit a U-SQL job</span></span>

1. <span data-ttu-id="e54e2-128">À partir de hello compte d’Analytique lac de données, cliquez sur **nouveau travail**.</span><span class="sxs-lookup"><span data-stu-id="e54e2-128">From hello Data Lake Analytics account, click **New Job**.</span></span>
2. <span data-ttu-id="e54e2-129">Collez le texte hello Hello script U-SQL ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="e54e2-129">Paste in hello text of hello U-SQL script shown above.</span></span> 
3. <span data-ttu-id="e54e2-130">Cliquez sur **Envoyer le travail**.</span><span class="sxs-lookup"><span data-stu-id="e54e2-130">Click **Submit Job**.</span></span>   
4. <span data-ttu-id="e54e2-131">Patientez jusqu'à ce que les changements d’état de tâche de hello trop**Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="e54e2-131">Wait until hello job status changes too**Succeeded**.</span></span>
5. <span data-ttu-id="e54e2-132">En cas d’échec de la tâche de hello, consultez [moniteur et résoudre les problèmes de travaux d’Analytique lac de données](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="e54e2-132">If hello job failed, see [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>
6. <span data-ttu-id="e54e2-133">Cliquez sur hello **sortie** onglet, puis cliquez sur `data.csv`.</span><span class="sxs-lookup"><span data-stu-id="e54e2-133">Click hello **Output** tab, and then click `data.csv`.</span></span> 

## <a name="see-also"></a><span data-ttu-id="e54e2-134">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="e54e2-134">See also</span></span>

* <span data-ttu-id="e54e2-135">tooget en main le développement d’applications SQL-U, consultez [scripts développer U-SQL à l’aide de Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e54e2-135">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="e54e2-136">toolearn U-SQL, consultez [prise en main langage lac de données Azure Analytique U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e54e2-136">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="e54e2-137">Pour les tâches de gestion, consultez [Gestion d’Azure Data Lake Analytics à l’aide du portail Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e54e2-137">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
