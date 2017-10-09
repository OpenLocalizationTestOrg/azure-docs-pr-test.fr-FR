---
title: "aaaUse PowerShell tooget main d’Azure Data Lake Store | Documents Microsoft"
description: "Utiliser Azure PowerShell toocreate un compte Data Lake Store et effectuer des opérations de base"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 9c958bfd63e412ec0b0a4113a149f61aee026bc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a>Prise en main d'Azure Data Lake Store avec Azure PowerShell
> [!div class="op_single_selector"]
> * [Portail](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Kit SDK .NET](data-lake-store-get-started-net-sdk.md)
> * [Kit SDK Java](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.JS](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Découvrez comment toouse Azure PowerShell toocreate stocker une Azure Data Lake compte et effectuer des opérations de base telles que la création de dossiers, téléchargent et téléchargement les fichiers de données, supprimez votre compte, un etc.. Pour plus d’informations sur Data Lake Store, consultez [Vue d’ensemble de Data Lake Store](data-lake-store-overview.md).

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez disposer de hello :

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 ou version ultérieure**. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

## <a name="authentication"></a>Authentification
Cet article utilise une approche plus simple de l’authentification avec Data Lake Store où vous êtes invité à tooenter vos informations d’identification de compte Azure. Hello accès niveau tooData Lake Store compte de système de fichiers et est ensuite régie par niveau d’accès hello Hello à l’utilisateur connecté. Toutefois, il existe d’autres approches en tant que bien tooauthenticate avec Data Lake Store, qui sont **l’authentification de l’utilisateur final** ou **l’authentification de service**. Pour plus d’informations sur la façon d’et tooauthenticate, consultez [l’authentification de l’utilisateur final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [l’authentification de service](data-lake-store-authenticate-using-active-directory.md).

## <a name="create-an-azure-data-lake-store-account"></a>Créer un compte Azure Data Lake Store
1. À partir de votre bureau, ouvrez une nouvelle fenêtre de Windows PowerShell et entrez hello suivant toolog extrait dans tooyour compte Azure, définissez hello abonnement et hello Data Lake Store fournisseur. Toolog demandée, assurez-vous que vous connectez en tant qu’un des admininistrators/propriétaire de l’abonnement hello :

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. Un compte Azure Data Lake Store est associé à un groupe de ressources Azure. Commencez par créer un groupe de ressources Azure.

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    ![Créer un groupe de ressources Azure](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Créer un groupe de ressources Azure")
3. Créer un compte Azure Data Lake Store. nom Hello que vous spécifiez doit uniquement contenir des lettres minuscules et chiffres.

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    ![Créer un compte Azure Data Lake Store](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Créer un compte Azure Data Lake Store")
4. Vérifiez que le compte de hello a été créé.

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    Hello pour cela doit être de sortie **True**.

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a>Créer des structures de répertoires dans votre Azure Data Lake Store
Vous pouvez créer des répertoires sous votre toomanage de compte Azure Data Lake Store et stocker des données.

1. Spécifiez un répertoire racine.

        $myrootdir = "/"
2. Créer un nouveau répertoire nommé **mynewdirectory** sous la racine spécifiée de hello.

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. Vérifiez que ce répertoire hello est créé avec succès.

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    Il doit afficher une sortie semblable à hello suivante :

    ![Vérifier le répertoire](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Vérifier le répertoire")

## <a name="upload-data-tooyour-azure-data-lake-store"></a>Télécharger des données tooyour Azure Data Lake Store
Vous pouvez télécharger votre tooData de data Lake Store directement dans le répertoire de niveau ou tooa de racine hello que vous avez créé dans le compte de hello. Hello d’extraits de code ci-dessous montrent comment tooupload un répertoire toohello de données exemple (**mynewdirectory**) vous avez créé dans la section précédente de hello.

Si vous recherchez des tooupload de données d’exemple, vous pouvez obtenir hello **Ambulance données** dossier hello [référentiel Git de LAC de données Azure](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData). Télécharger le fichier de hello et stockez-le dans un répertoire local sur votre ordinateur, telles que C:\sampledata\.

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a>Renommer, télécharger et supprimer des données de votre Data Lake Store
toorename un fichier, utilisez hello de commande suivante :

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

toodownload un fichier, utilisez hello de commande suivante :

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

toodelete un fichier, utilisez hello de commande suivante :

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

Lorsque vous y êtes invité, entrez **Y** élément hello de toodelete. Si vous avez plusieurs fichiers toodelete, vous pouvez fournir tous les chemins d’accès de hello séparés par des virgules.

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a>Supprimer votre compte Azure Data Lake Store
Utilisez hello suivant commande toodelete votre compte Data Lake Store.

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

Lorsque vous y êtes invité, entrez **Y** compte de hello toodelete.

## <a name="performance-guidance-while-using-powershell"></a>Guide des performances lors de l’utilisation de PowerShell

Voici les paramètres importants qui peuvent être analysées tooget hello meilleures performances lors de l’utilisation de PowerShell toowork avec Data Lake Store hello :

| Propriété            | Default | Description |
|---------------------|---------|-------------|
| PerFileThreadCount  | 10      | Ce paramètre vous permet de nombre de hello toochoose de threads parallèles pour le chargement ou téléchargement de chaque fichier. Ce nombre représente hello nombre max. de threads qui peut être alloués par fichier, mais vous risquez d’obtenir moins de threads en fonction de votre scénario (par exemple, si vous téléchargez un fichier de 1 Ko, vous obtiendrez un thread même si vous demander de 20 threads).  |
| ConcurrentFileCount | 10      | Ce paramètre est spécifique au chargement ou au téléchargement des dossiers. Ce paramètre détermine le nombre hello des fichiers simultanées qui peuvent être téléchargés ou téléchargé. Ce nombre représente le nombre maximal de hello des fichiers simultanées qui peuvent être téléchargés ou téléchargé en même temps, mais vous risquez d’obtenir moins d’accès concurrentiel en fonction de votre scénario (par exemple, si vous téléchargez les deux fichiers, vous obtiendrez deux téléchargements de fichier simultanées même si vous demandez 15). |

**Exemple**

Cette commande télécharge les fichiers de disque local de l’utilisateur d’Azure Data Lake Store toohello à l’aide de 20 threads par fichier et 100 fichiers simultanées.

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-hello-value-tooset-for-these-parameters"></a>Comment déterminer les tooset de valeur hello pour ces paramètres ?

Voici quelques conseils à suivre.

* **Étape 1 : Déterminer le nombre total de threads de hello** -vous devez commencer par le calcul toouse de nombre total de threads hello. En règle générale, vous devez utiliser 6 threads pour chaque noyau physique.

        Total thread count = total physical cores * 6

    **Exemple**

    En supposant que Hello PowerShell sont en cours d’exécution des commandes à partir d’une machine virtuelle D14 qui possède 16 cœurs

        Total thread count = 16 cores * 6 = 96 threads


* **Étape 2 : Calculer PerFileThreadCount** -nous calculons notre PerFileThreadCount en fonction de taille hello des fichiers de hello. Pour les fichiers inférieures à 2,5 Go, n’est pas toochange besoin de ce paramètre car hello comme valeur par défaut 10 est suffisante. Pour les fichiers de plus de 2,5 Go, vous devez utiliser 10 threads base hello pour hello première 2,5 Go et ajouter 1 thread de chaque augmentation de 256 Mo supplémentaires pour une taille de fichier. Si vous copiez un dossier contenant différentes tailles de fichiers, envisagez de regrouper ces fichiers par tailles similaires. Les différentes tailles de fichiers ne permettent pas d’obtenir des performances optimales. Si cela est possible toogroup les tailles de fichiers similaires, vous devez définir PerFileThreadCount selon la taille de fichier maximale hello.

        PerFileThreadCount = 10 threads for hello first 2.5GB + 1 thread for each additional 256MB increase in file size

    **Exemple**

    En supposant que vous avez 100 fichiers allant de 1 Go too10GB, nous utilisons hello 10 Go comme hello plus grande taille de l’équation, ce qui indiquerait hello suivante du fichier.

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* **Étape 3 : Calculer ConcurrentFilecount** -utiliser le nombre total de threads hello et PerFileThreadCount toocalculate ConcurrentFileCount selon hello suivant l’équation.

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    **Exemple**

    Selon les valeurs de l’exemple hello que nous avons utilisé

        96 = 40 * ConcurrentFileCount

    Par conséquent, **ConcurrentFileCount** est **2.4**, ce qui nous pouvons arrondir trop**2**.

### <a name="further-tuning"></a>Paramétrage supplémentaire

Vous pouvez avoir besoin de davantage de paramétrage, car il existe une plage de toowork de tailles de fichier avec. Hello au-dessus de calcul fonctionne bien si toutes ou la plupart des fichiers de hello est la plage de 10 Go toohello et que le plus proche. Par contre, s’il y a beaucoup de tailles de fichiers différentes et que la plupart des fichiers sont parmi les plus petits, vous pouvez réduire PerFileThreadCount. En réduisant hello PerFileThreadCount, nous pouvons augmenter ConcurrentFileCount. Par conséquent, si nous partons du principe que la plupart de ses fichiers est plus petite dans la plage de 5 Go hello, nous pouvons refaire la notre calcul :

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

Par conséquent, **ConcurrentFileCount** sera désormais 96/20, ce qui est 4.8, arrondie trop**4**.

Vous pouvez continuer tootune ces paramètres en modifiant hello **PerFileThreadCount** haut et bas en fonction de distribution hello votre de tailles de fichier.

### <a name="limitation"></a>Limitation

* **Nombre de fichiers est inférieure à ConcurrentFileCount**: si le nombre de hello de fichiers que vous chargez est inférieure à hello **ConcurrentFileCount** que vous avez calculé, puis vous devez réduire  **ConcurrentFileCount** nombre égal toohello de toobe de fichiers. Vous pouvez utiliser n’importe quel tooincrease de threads restants **PerFileThreadCount**.

* **Trop de threads**: Si vous augmentez le thread trop sans augmenter la taille de votre cluster, vous courez risque hello de dégradation des performances. Il peut y avoir des problèmes de contention lors du basculement de contexte sur hello du processeur.

* **Concurrence insuffisante**: si la concurrence de hello n’est pas suffisante, puis votre cluster est peut-être trop faible. Vous pouvez augmenter le nombre de hello de nœuds dans votre cluster qui vous donne plus de concurrence.

* **Erreurs de limitation** : il se peut que vous rencontriez des erreurs de limitation si le nombre d’accès concurrentiels est trop élevé. Si vous rencontrez le problème de limitation, vous devez réduire d’accès concurrentiel hello ou nous contacter.

## <a name="next-steps"></a>Étapes suivantes
* [Sécuriser les données dans Data Lake Store](data-lake-store-secure-data.md)
* [Utiliser Azure Data Lake Analytics avec Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Utiliser Azure HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

