---
title: "Prise en main d’Azure Data Lake Analytics à l’aide du portail Azure | Microsoft Docs"
description: "Découvrez comment utiliser le portail Azure pour créer un compte Data Lake Analytics, créer un travail Data Lake Analytics avec U-SQL et envoyer le travail. "
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
ms.openlocfilehash: 2722a2d72ed90ea0005362563ecaee30750c040a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a><span data-ttu-id="9bf66-103">Prise en main d’Azure Data Lake Analytics à l’aide du Portail Azure</span><span class="sxs-lookup"><span data-stu-id="9bf66-103">Get started with Azure Data Lake Analytics using Azure portal</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="9bf66-104">Découvrez comment utiliser le portail Azure pour créer des comptes Azure Data Lake Analytics, définir des travaux dans [U-SQL](data-lake-analytics-u-sql-get-started.md) et envoyer des travaux au service Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="9bf66-104">Learn how to use the Azure portal to create Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to the Data Lake Analytics service.</span></span> <span data-ttu-id="9bf66-105">Pour plus d’informations sur Analytique Data Lake, consultez [Présentation d’Analytique Data Lake Azure](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9bf66-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bf66-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="9bf66-106">Prerequisites</span></span>

<span data-ttu-id="9bf66-107">Avant de commencer ce didacticiel, vous devez disposer d’un **abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="9bf66-107">Before you begin this tutorial, you must have an **Azure subscription**.</span></span> <span data-ttu-id="9bf66-108">Consultez la rubrique [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9bf66-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="9bf66-109">Créer un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="9bf66-109">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="9bf66-110">À présent, vous allez créer un compte Data Lake Analytics et un compte Data Lake Store simultanément.</span><span class="sxs-lookup"><span data-stu-id="9bf66-110">Now, you will create a Data Lake Analytics and a Data Lake Store account at the same time.</span></span>  <span data-ttu-id="9bf66-111">Cette étape est simple et ne prend qu’environ 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="9bf66-111">This step is simple and only takes about 60 seconds to finish.</span></span>

1. <span data-ttu-id="9bf66-112">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9bf66-112">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9bf66-113">Cliquez sur **Nouveau** >  **Données + analyse** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="9bf66-113">Click **New** >  **Data + Analytics** > **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="9bf66-114">Sélectionnez des valeurs pour les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="9bf66-114">Select values for the following items:</span></span>
   * <span data-ttu-id="9bf66-115">**Nom** : donnez un nom à votre compte Data Lake Analytics (utilisez uniquement des lettres minuscules et des chiffres).</span><span class="sxs-lookup"><span data-stu-id="9bf66-115">**Name**: Name your Data Lake Analytics account (Only lower case letters and numbers allowed).</span></span>
   * <span data-ttu-id="9bf66-116">**Abonnement**: choisissez l’abonnement Azure utilisé pour le compte Analytics.</span><span class="sxs-lookup"><span data-stu-id="9bf66-116">**Subscription**: Choose the Azure subscription used for the Analytics account.</span></span>
   * <span data-ttu-id="9bf66-117">**Groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="9bf66-117">**Resource Group**.</span></span> <span data-ttu-id="9bf66-118">Sélectionnez un groupe de ressources Azure existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="9bf66-118">Select an existing Azure Resource Group or create a new one.</span></span>
   * <span data-ttu-id="9bf66-119">**Emplacement**.</span><span class="sxs-lookup"><span data-stu-id="9bf66-119">**Location**.</span></span> <span data-ttu-id="9bf66-120">Sélectionnez un centre de données Azure pour le compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="9bf66-120">Select an Azure data center for the Data Lake Analytics account.</span></span>
   * <span data-ttu-id="9bf66-121">**Data Lake Store** : suivez les instructions pour créer un compte Data Lake Store ou sélectionnez un compte existant.</span><span class="sxs-lookup"><span data-stu-id="9bf66-121">**Data Lake Store**: Follow the instruction to create a new Data Lake Store account, or select an existing one.</span></span> 
4. <span data-ttu-id="9bf66-122">Si vous le souhaitez, sélectionnez un niveau tarifaire pour votre compte Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="9bf66-122">Optionally, select a pricing tier for your Data Lake Analytics account.</span></span>
5. <span data-ttu-id="9bf66-123">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="9bf66-123">Click **Create**.</span></span> 


## <a name="your-first-u-sql-script"></a><span data-ttu-id="9bf66-124">Votre premier script U-SQL</span><span class="sxs-lookup"><span data-stu-id="9bf66-124">Your first U-SQL script</span></span>

<span data-ttu-id="9bf66-125">Le texte suivant est un script U-SQL très simple.</span><span class="sxs-lookup"><span data-stu-id="9bf66-125">The following text is a very simple U-SQL script.</span></span> <span data-ttu-id="9bf66-126">Il ne fait que définir un petit jeu de données dans le script puis de l’écrire dans le Data Lake Store par défaut comme un fichier appelé `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="9bf66-126">All it does is define a small dataset within the script and then write that dataset out to the default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="9bf66-127">Envoyer un travail U-SQL</span><span class="sxs-lookup"><span data-stu-id="9bf66-127">Submit a U-SQL job</span></span>

1. <span data-ttu-id="9bf66-128">À partir du compte Data Lake Analytics, cliquez sur **Nouveau travail**.</span><span class="sxs-lookup"><span data-stu-id="9bf66-128">From the Data Lake Analytics account, click **New Job**.</span></span>
2. <span data-ttu-id="9bf66-129">Collez le texte du script U-SQL ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="9bf66-129">Paste in the text of the U-SQL script shown above.</span></span> 
3. <span data-ttu-id="9bf66-130">Cliquez sur **Envoyer le travail**.</span><span class="sxs-lookup"><span data-stu-id="9bf66-130">Click **Submit Job**.</span></span>   
4. <span data-ttu-id="9bf66-131">Attendez que l’état du travail passe à **Réussi**.</span><span class="sxs-lookup"><span data-stu-id="9bf66-131">Wait until the job status changes to **Succeeded**.</span></span>
5. <span data-ttu-id="9bf66-132">Si le travail échoue, consultez [Analyser et dépanner les travaux Data Lake Analytics](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="9bf66-132">If the job failed, see [Monitor and troubleshoot Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>
6. <span data-ttu-id="9bf66-133">Cliquez sur l’onglet **Sortie**, puis sur `data.csv`.</span><span class="sxs-lookup"><span data-stu-id="9bf66-133">Click the **Output** tab, and then click `data.csv`.</span></span> 

## <a name="see-also"></a><span data-ttu-id="9bf66-134">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9bf66-134">See also</span></span>

* <span data-ttu-id="9bf66-135">Pour commencer à développer des applications U-SQL, consultez [Développer des scripts U-SQL avec Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9bf66-135">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="9bf66-136">Pour connaître U-SQL, voir [Prise en main du langage U-SQL d’Analytique Data Lake Azure](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9bf66-136">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="9bf66-137">Pour les tâches de gestion, consultez [Gestion d’Azure Data Lake Analytics à l’aide du portail Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9bf66-137">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
