---
title: "aaaGet main Analytique de LAC de données Azure à l’aide d’Azure PowerShell | Documents Microsoft"
description: "Utiliser Azure PowerShell toocreate un compte Analytique lac de données, créez une tâche Analytique lac de données à l’aide de U-SQL et envoi de la tâche de hello. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 8a4e901e-9656-4a60-90d0-d78ff2f00656
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: edmaca
ms.openlocfilehash: cb9b35352d1cc9a78337448b1d6835875a212e08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="4dab0-103">Prise en main d’Analytique Data Lake à l’aide d’Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4dab0-103">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="4dab0-104">Découvrez comment toouse Azure PowerShell toocreate Analytique de LAC de données Azure des comptes et puis soumettre et exécuter des travaux U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4dab0-104">Learn how toouse Azure PowerShell toocreate Azure Data Lake Analytics accounts and then submit and run U-SQL jobs.</span></span> <span data-ttu-id="4dab0-105">Pour plus d’informations sur Analytique Data Lake, consultez [Présentation d’Analytique Data Lake Azure](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4dab0-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4dab0-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4dab0-106">Prerequisites</span></span>

<span data-ttu-id="4dab0-107">Avant de commencer ce didacticiel, vous devez disposer de hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4dab0-107">Before you begin this tutorial, you must have hello following information:</span></span>

* <span data-ttu-id="4dab0-108">**Un compte Azure Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="4dab0-108">**An Azure Data Lake Analytics account**.</span></span> <span data-ttu-id="4dab0-109">Consultez [Prise en main de Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="4dab0-109">See [Get started with Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).</span></span>
* <span data-ttu-id="4dab0-110">**Un poste de travail sur lequel est installé Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="4dab0-110">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="4dab0-111">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4dab0-111">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="log-in-tooazure"></a><span data-ttu-id="4dab0-112">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="4dab0-112">Log in tooAzure</span></span>

<span data-ttu-id="4dab0-113">Ce didacticiel suppose que vous savez déjà utiliser Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4dab0-113">This tutorial assumes you are already familiar with using Azure PowerShell.</span></span> <span data-ttu-id="4dab0-114">En particulier, vous devez tooknow comment toolog dans tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4dab0-114">In particular, you need tooknow how toolog in tooAzure.</span></span> <span data-ttu-id="4dab0-115">Consultez hello [prise en main Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) si vous avez besoin d’aide.</span><span class="sxs-lookup"><span data-stu-id="4dab0-115">See hello [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) if you need help.</span></span>

<span data-ttu-id="4dab0-116">toolog avec un nom d’abonnement :</span><span class="sxs-lookup"><span data-stu-id="4dab0-116">toolog in with a subscription name:</span></span>

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

<span data-ttu-id="4dab0-117">Au lieu du nom de l’abonnement hello, vous pouvez également utiliser un toolog d’id d’abonnement dans :</span><span class="sxs-lookup"><span data-stu-id="4dab0-117">Instead of hello subscription name, you can also use a subscription id toolog in:</span></span>

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

<span data-ttu-id="4dab0-118">En cas de réussite, sortie hello de cette commande ressemble à hello suivant du texte :</span><span class="sxs-lookup"><span data-stu-id="4dab0-118">If  successful, hello output of this command looks like hello following text:</span></span>

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a><span data-ttu-id="4dab0-119">Préparation pour le didacticiel de hello</span><span class="sxs-lookup"><span data-stu-id="4dab0-119">Preparing for hello tutorial</span></span>

<span data-ttu-id="4dab0-120">extraits de code PowerShell Hello dans ce didacticiel utilisent ces informations à ces toostore de variables :</span><span class="sxs-lookup"><span data-stu-id="4dab0-120">hello PowerShell snippets in this tutorial use these variables toostore this information:</span></span>

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="4dab0-121">Obtenir des informations sur un compte Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4dab0-121">Get information about a Data Lake Analytics account</span></span>

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a><span data-ttu-id="4dab0-122">Envoyer un travail U-SQL</span><span class="sxs-lookup"><span data-stu-id="4dab0-122">Submit a U-SQL job</span></span>

<span data-ttu-id="4dab0-123">Créer un script de hello U-SQL toohold variable PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4dab0-123">Create a PowerShell variable toohold hello U-SQL script.</span></span>

```
$script = @"
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

"@
```

<span data-ttu-id="4dab0-124">Envoyer le script de hello.</span><span class="sxs-lookup"><span data-stu-id="4dab0-124">Submit hello script.</span></span>

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

<span data-ttu-id="4dab0-125">Vous pouvez également enregistrer le script de hello en tant que fichier et envoyer par hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4dab0-125">Alternatively, you could save hello script as a file and submit with hello following command:</span></span>

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


<span data-ttu-id="4dab0-126">Obtenir l’état de hello d’une tâche donnée.</span><span class="sxs-lookup"><span data-stu-id="4dab0-126">Get hello status of a specific job.</span></span> <span data-ttu-id="4dab0-127">Gardez à l’aide de cette applet de commande jusqu'à ce que vous voyiez hello travail est effectué.</span><span class="sxs-lookup"><span data-stu-id="4dab0-127">Keep using this cmdlet until you see hello job is done.</span></span>

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

<span data-ttu-id="4dab0-128">Au lieu d’appeler Get-AdlAnalyticsJob plusieurs fois jusqu'à ce que la tâche terminée, vous pouvez utiliser l’applet de commande Wait-AdlJob hello.</span><span class="sxs-lookup"><span data-stu-id="4dab0-128">Instead of calling Get-AdlAnalyticsJob over and over until a job finishes, you can use hello Wait-AdlJob cmdlet.</span></span>

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

<span data-ttu-id="4dab0-129">Téléchargez le fichier de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="4dab0-129">Download hello output file.</span></span>

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a><span data-ttu-id="4dab0-130">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4dab0-130">See also</span></span>
* <span data-ttu-id="4dab0-131">toosee hello même didacticiel à l’aide d’autres outils, cliquez sur les sélecteurs d’onglet hello haut hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="4dab0-131">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
* <span data-ttu-id="4dab0-132">toolearn U-SQL, consultez [prise en main langage lac de données Azure Analytique U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4dab0-132">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="4dab0-133">Pour les tâches de gestion, consultez [Gestion d’Azure Data Lake Analytics à l’aide du portail Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4dab0-133">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
