---
title: "les scripts aaaDevelop U-SQL à l’aide de Data Lake Tools pour Visual Studio | Documents Microsoft"
description: "Découvrez comment tooinstall Data Lake Tools pour Visual Studio et les scripts U-SQL toodevelop et de test."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/28/2017
ms.author: saveenr, yanacai
ms.openlocfilehash: 7a0c02c275b8cefecbe784ba63969cbf24a150d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a><span data-ttu-id="d6092-103">Développer des scripts U-SQL à l’aide des outils Data Lake pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d6092-103">Develop U-SQL scripts by using Data Lake Tools for Visual Studio</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


<span data-ttu-id="d6092-104">Découvrez comment toouse Visual Studio toocreate Analytique de LAC de données Azure des comptes, définir des travaux dans [U-SQL](data-lake-analytics-u-sql-get-started.md)et soumettre le service de données Lake Analytique toohello travaux.</span><span class="sxs-lookup"><span data-stu-id="d6092-104">Learn how toouse Visual Studio toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="d6092-105">Pour plus d’informations sur Analytique Data Lake, consultez [Présentation d’Analytique Data Lake Azure](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d6092-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d6092-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d6092-106">Prerequisites</span></span>

* <span data-ttu-id="d6092-107">**Visual Studio** : toutes les éditions sauf Express sont prises en charge.</span><span class="sxs-lookup"><span data-stu-id="d6092-107">**Visual Studio**: All editions except Express are supported.</span></span>
    * <span data-ttu-id="d6092-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="d6092-108">Visual Studio 2017</span></span>
    * <span data-ttu-id="d6092-109">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="d6092-109">Visual Studio 2015</span></span>
    * <span data-ttu-id="d6092-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="d6092-110">Visual Studio 2013</span></span>
* <span data-ttu-id="d6092-111">**Kit SDK Microsoft Azure pour .NET** version 2.7.1 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d6092-111">**Microsoft Azure SDK for .NET** version 2.7.1 or later.</span></span>  <span data-ttu-id="d6092-112">Installez-le à l’aide de hello [le programme d’installation de Web platform](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="d6092-112">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="d6092-113">Un compte**Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d6092-113">A **Data Lake Analytics** account.</span></span> <span data-ttu-id="d6092-114">toocreate un compte, consultez [prise en main Analytique de LAC de données Azure à l’aide du portail Azure](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d6092-114">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="install-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="d6092-115">Installer Azure Data Lake Tools pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d6092-115">Install Azure Data Lake Tools for Visual Studio</span></span> 

<span data-ttu-id="d6092-116">Téléchargez et installez Azure Data Lake Tools pour Visual Studio [à partir du centre de téléchargement de hello](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="d6092-116">Download and install Azure Data Lake Tools for Visual Studio [from hello Download Center](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="d6092-117">Après l’installation, notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="d6092-117">After installation, note that:</span></span>
* <span data-ttu-id="d6092-118">Hello **l’Explorateur de serveurs** > **Azure** nœud contient un **Analytique lac de données** nœud.</span><span class="sxs-lookup"><span data-stu-id="d6092-118">hello **Server Explorer** > **Azure** node contains a **Data Lake Analytics** node.</span></span> 
* <span data-ttu-id="d6092-119">Hello **outils** menu a un **Data Lake** élément.</span><span class="sxs-lookup"><span data-stu-id="d6092-119">hello **Tools** menu has a **Data Lake** item.</span></span>

## <a name="connect-tooan-azure-data-lake-analytics-account"></a><span data-ttu-id="d6092-120">Tooan Analytique de LAC de données Azure compte de connexion</span><span class="sxs-lookup"><span data-stu-id="d6092-120">Connect tooan Azure Data Lake Analytics account</span></span>

1. <span data-ttu-id="d6092-121">Ouvrez Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d6092-121">Open Visual Studio.</span></span>
2. <span data-ttu-id="d6092-122">Ouvrez l’Explorateur de serveurs en sélectionnant **Afficher** > **Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="d6092-122">Open Server Explorer by selecting **View** > **Server Explorer**.</span></span>
3. <span data-ttu-id="d6092-123">Cliquez avec le bouton droit sur **Azure**.</span><span class="sxs-lookup"><span data-stu-id="d6092-123">Right-click **Azure**.</span></span> <span data-ttu-id="d6092-124">Puis sélectionnez **connecter tooMicrosoft abonnement Azure** et suivez les instructions de hello.</span><span class="sxs-lookup"><span data-stu-id="d6092-124">Then select **Connect tooMicrosoft Azure Subscription** and follow hello instructions.</span></span>
4. <span data-ttu-id="d6092-125">Dans l’Explorateur de serveurs, sélectionnez **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d6092-125">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> <span data-ttu-id="d6092-126">Une liste des comptes Data Lake Analytics s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d6092-126">You see a list of your Data Lake Analytics accounts.</span></span>


## <a name="write-your-first-u-sql-script"></a><span data-ttu-id="d6092-127">Rédiger son premier script U-SQL</span><span class="sxs-lookup"><span data-stu-id="d6092-127">Write your first U-SQL script</span></span>

<span data-ttu-id="d6092-128">Hello suivant le texte est un simple script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d6092-128">hello following text is a simple U-SQL script.</span></span> <span data-ttu-id="d6092-129">Il définit un petit jeu de données et les écritures Data Lake Store dataset toohello par défaut comme un fichier appelé `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="d6092-129">It defines a small dataset and writes that dataset toohello default Data Lake Store as a file called `/data.csv`.</span></span>

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

### <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="d6092-130">Envoyer le travail Analytique Data Lake</span><span class="sxs-lookup"><span data-stu-id="d6092-130">Submit a Data Lake Analytics job</span></span>

1. <span data-ttu-id="d6092-131">Sélectionnez **Fichier** > **Nouveau** > **Projet**.</span><span class="sxs-lookup"><span data-stu-id="d6092-131">Select **File** > **New** > **Project**.</span></span>

2. <span data-ttu-id="d6092-132">Sélectionnez hello **U-SQL projet** , puis tapez **OK**.</span><span class="sxs-lookup"><span data-stu-id="d6092-132">Select hello **U-SQL Project** type, and then click **OK**.</span></span> <span data-ttu-id="d6092-133">Visual Studio crée une solution avec un fichier **Script.usql**.</span><span class="sxs-lookup"><span data-stu-id="d6092-133">Visual Studio creates a solution with a **Script.usql** file.</span></span>

3. <span data-ttu-id="d6092-134">Coller le script précédent de hello dans hello **Script.usql** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="d6092-134">Paste hello previous script into hello **Script.usql** window.</span></span>

4. <span data-ttu-id="d6092-135">Dans le coin supérieur gauche de hello Hello **Script.usql** fenêtre, spécifiez hello Analytique lac de données compte.</span><span class="sxs-lookup"><span data-stu-id="d6092-135">In hello upper-left corner of hello **Script.usql** window, specify hello Data Lake Analytics account.</span></span>

    ![Soumettre un projet U-SQL Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. <span data-ttu-id="d6092-137">Dans le coin supérieur gauche de hello Hello **Script.usql** fenêtre, sélectionnez **Submit**.</span><span class="sxs-lookup"><span data-stu-id="d6092-137">In hello upper-left corner of hello **Script.usql** window, select **Submit**.</span></span>
6. <span data-ttu-id="d6092-138">Vérifiez que hello **Analytique compte**, puis sélectionnez **Submit**.</span><span class="sxs-lookup"><span data-stu-id="d6092-138">Verify hello **Analytics Account**, and then select **Submit**.</span></span> <span data-ttu-id="d6092-139">Résultats de la soumission sont disponibles dans hello Data Lake Tools pour Visual Studio résultats après que l’envoi de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="d6092-139">Submission results are available in hello Data Lake Tools for Visual Studio Results after hello submission is complete.</span></span>

    ![Soumettre un projet U-SQL Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. <span data-ttu-id="d6092-141">toosee hello dernier travail état et l’actualisation hello écran, cliquez sur **Actualiser**.</span><span class="sxs-lookup"><span data-stu-id="d6092-141">toosee hello latest job status and refresh hello screen, click **Refresh**.</span></span> <span data-ttu-id="d6092-142">Lors de la réussite du travail de hello, il affiche hello **travail graphique**, **des opérations de métadonnées**, **historique de l’état**, et **Diagnostics**:</span><span class="sxs-lookup"><span data-stu-id="d6092-142">When hello job succeeds, it shows hello **Job Graph**, **MetaData Operations**, **State History**, and **Diagnostics**:</span></span>

    ![Graphique des performances du travail U-SQL Visual Studio Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * <span data-ttu-id="d6092-144">**Résumé du travail** affiche hello résumé du travail de hello.</span><span class="sxs-lookup"><span data-stu-id="d6092-144">**Job Summary** shows hello summary of hello job.</span></span>   
   * <span data-ttu-id="d6092-145">**Détails de la tâche** affiche des informations plus spécifiques sur la tâche hello, y compris le script de hello, des ressources et des sommets.</span><span class="sxs-lookup"><span data-stu-id="d6092-145">**Job Details** shows more specific information about hello job, including hello script, resources, and vertices.</span></span>
   * <span data-ttu-id="d6092-146">**Graphique de travail** visualise progression hello de hello.</span><span class="sxs-lookup"><span data-stu-id="d6092-146">**Job Graph** visualizes hello progress of hello job.</span></span>
   * <span data-ttu-id="d6092-147">**Opérations de métadonnées** montre toutes les actions hello qui ont été effectuées sur le catalogue de hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d6092-147">**MetaData Operations** shows all hello actions that were taken on hello U-SQL catalog.</span></span>
   * <span data-ttu-id="d6092-148">**Données** affiche toutes les entrées de hello et sorties.</span><span class="sxs-lookup"><span data-stu-id="d6092-148">**Data** shows all hello inputs and outputs.</span></span>
   * <span data-ttu-id="d6092-149">**Diagnostics** fournit une analyse avancée pour l’optimisation des performances et de l’exécution des travaux.</span><span class="sxs-lookup"><span data-stu-id="d6092-149">**Diagnostics** provides an advanced analysis for job execution and performance optimization.</span></span>

### <a name="toocheck-job-state"></a><span data-ttu-id="d6092-150">état de la tâche toocheck</span><span class="sxs-lookup"><span data-stu-id="d6092-150">toocheck job state</span></span>

1. <span data-ttu-id="d6092-151">Dans l’Explorateur de serveurs, sélectionnez **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="d6092-151">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> 
2. <span data-ttu-id="d6092-152">Développez le nom du compte hello Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="d6092-152">Expand hello Data Lake Analytics account name.</span></span>
3. <span data-ttu-id="d6092-153">Double-cliquez sur **Travaux**.</span><span class="sxs-lookup"><span data-stu-id="d6092-153">Double-click **Jobs**.</span></span>
4. <span data-ttu-id="d6092-154">Sélectionnez la tâche hello que vous avez déjà envoyé.</span><span class="sxs-lookup"><span data-stu-id="d6092-154">Select hello job that you previously submitted.</span></span>

### <a name="toosee-hello-output-of-a-job"></a><span data-ttu-id="d6092-155">sortie de hello toosee d’une tâche</span><span class="sxs-lookup"><span data-stu-id="d6092-155">toosee hello output of a job</span></span>

1. <span data-ttu-id="d6092-156">Dans l’Explorateur de serveurs, parcourir le travail toohello que vous avez envoyé.</span><span class="sxs-lookup"><span data-stu-id="d6092-156">In Server Explorer, browse toohello job you submitted.</span></span>
2. <span data-ttu-id="d6092-157">Cliquez sur hello **données** onglet.</span><span class="sxs-lookup"><span data-stu-id="d6092-157">Click hello **Data** tab.</span></span>
3. <span data-ttu-id="d6092-158">Bonjour **de sorties de travail** onglet, sélectionnez hello `"/data.csv"` fichier.</span><span class="sxs-lookup"><span data-stu-id="d6092-158">In hello **Job Outputs** tab, select hello `"/data.csv"` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6092-159">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d6092-159">Next steps</span></span>

* [<span data-ttu-id="d6092-160">Run U-SQL scripts on your own workstation for testing and debugging (Exécuter des scripts U-SQL sur votre station de travail pour les tests et le débogage)</span><span class="sxs-lookup"><span data-stu-id="d6092-160">Run U-SQL scripts on your own workstation for testing and debugging</span></span>](data-lake-analytics-data-lake-tools-local-run.md)
* [<span data-ttu-id="d6092-161">Débogage de travaux U-SQL</span><span class="sxs-lookup"><span data-stu-id="d6092-161">Debug C# code in U-SQL jobs</span></span>](data-lake-analytics-debug-u-sql-jobs.md)
* [<span data-ttu-id="d6092-162">Utilisez hello Azure Data Lake Tools pour Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d6092-162">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
