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
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a>Prise en main d’Analytique Data Lake à l’aide d’Azure PowerShell
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Découvrez comment toouse Azure PowerShell toocreate Analytique de LAC de données Azure des comptes et puis soumettre et exécuter des travaux U-SQL. Pour plus d’informations sur Analytique Data Lake, consultez [Présentation d’Analytique Data Lake Azure](data-lake-analytics-overview.md).

## <a name="prerequisites"></a>Composants requis

Avant de commencer ce didacticiel, vous devez disposer de hello informations suivantes :

* **Un compte Azure Data Lake Analytics**. Consultez [Prise en main de Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).
* **Un poste de travail sur lequel est installé Azure PowerShell**. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

Ce didacticiel suppose que vous savez déjà utiliser Azure PowerShell. En particulier, vous devez tooknow comment toolog dans tooAzure. Consultez hello [prise en main Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) si vous avez besoin d’aide.

toolog avec un nom d’abonnement :

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

Au lieu du nom de l’abonnement hello, vous pouvez également utiliser un toolog d’id d’abonnement dans :

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

En cas de réussite, sortie hello de cette commande ressemble à hello suivant du texte :

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a>Préparation pour le didacticiel de hello

extraits de code PowerShell Hello dans ce didacticiel utilisent ces informations à ces toostore de variables :

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a>Obtenir des informations sur un compte Data Lake Analytics

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a>Envoyer un travail U-SQL

Créer un script de hello U-SQL toohold variable PowerShell.

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

Envoyer le script de hello.

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

Vous pouvez également enregistrer le script de hello en tant que fichier et envoyer par hello de commande suivante :

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


Obtenir l’état de hello d’une tâche donnée. Gardez à l’aide de cette applet de commande jusqu'à ce que vous voyiez hello travail est effectué.

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

Au lieu d’appeler Get-AdlAnalyticsJob plusieurs fois jusqu'à ce que la tâche terminée, vous pouvez utiliser l’applet de commande Wait-AdlJob hello.

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

Téléchargez le fichier de sortie hello.

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a>Voir aussi
* toosee hello même didacticiel à l’aide d’autres outils, cliquez sur les sélecteurs d’onglet hello haut hello de page de hello.
* toolearn U-SQL, consultez [prise en main langage lac de données Azure Analytique U-SQL](data-lake-analytics-u-sql-get-started.md).
* Pour les tâches de gestion, consultez [Gestion d’Azure Data Lake Analytics à l’aide du portail Azure](data-lake-analytics-manage-use-portal.md).
