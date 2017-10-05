---
title: "Utiliser des modèles Azure pour créer HDInsight et Data Lake Store | Microsoft Docs"
description: "Utiliser des modèles Azure Resource Manager pour créer et utiliser les clusters HDInsight avec Azure Data Lake Store"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: 6f43423096f0e74f41afea275e4ec9801dc2cea5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="44a0e-103">Créer un cluster HDInsight avec Data Lake Store à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="44a0e-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="44a0e-104">Utilisation du portail</span><span class="sxs-lookup"><span data-stu-id="44a0e-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="44a0e-105">Utilisation de PowerShell (pour le stockage par défaut)</span><span class="sxs-lookup"><span data-stu-id="44a0e-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="44a0e-106">Utilisation de PowerShell (pour le stockage supplémentaire)</span><span class="sxs-lookup"><span data-stu-id="44a0e-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="44a0e-107">Utilisation du gestionnaire des ressources</span><span class="sxs-lookup"><span data-stu-id="44a0e-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="44a0e-108">Apprenez à utiliser Azure PowerShell pour configurer un cluster HDInsight avec Azure Data Lake Store **comme stockage supplémentaire**.</span><span class="sxs-lookup"><span data-stu-id="44a0e-108">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="44a0e-109">Pour les types de clusters pris en charge, Data Lake Store est utilisé comme compte de stockage par défaut ou supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="44a0e-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="44a0e-110">Lorsque Data Lake Store est utilisé comme espace de stockage supplémentaire, le compte de stockage par défaut pour les clusters est toujours Azure Storage Blob (WABS), et les fichiers associés au cluster (par exemple, les journaux, etc.) sont écrits dans le stockage par défaut, tandis que les données que vous souhaitez traiter peuvent être stockées dans un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="44a0e-110">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="44a0e-111">L’utilisation de Data Lake Store en tant que compte de stockage supplémentaire n’affecte pas les performances ni la capacité de lecture/écriture sur le stockage à partir du cluster.</span><span class="sxs-lookup"><span data-stu-id="44a0e-111">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="44a0e-112">Utilisation de Data Lake Store pour le stockage de cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="44a0e-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="44a0e-113">Voici quelques considérations importantes pour l’utilisation de HDInsight avec Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="44a0e-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="44a0e-114">L’option permettant de créer des clusters HDInsight avec accès au Data Lake Store comme stockage par défaut est disponible si vous utilisez HDInsight version 3.5 ou 3.6.</span><span class="sxs-lookup"><span data-stu-id="44a0e-114">Option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="44a0e-115">L’option permettant de créer des clusters HDInsight avec accès au Data Lake Store comme stockage supplémentaire est disponible si vous utilisez HDInsight versions 3.2, 3.4, 3.5 et 3.6.</span><span class="sxs-lookup"><span data-stu-id="44a0e-115">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="44a0e-116">Dans cet article, nous approvisionnons un cluster Hadoop avec Data Lake Store comme stockage supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="44a0e-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="44a0e-117">Pour obtenir des instructions sur la création d’un cluster Hadoop avec Data Lake Store comme stockage par défaut, consultez la rubrique [Créer un cluster HDInsight avec Data Lake Store à l'aide du portail Azure](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="44a0e-117">For instructions on how to create a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44a0e-118">Composants requis</span><span class="sxs-lookup"><span data-stu-id="44a0e-118">Prerequisites</span></span>
<span data-ttu-id="44a0e-119">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="44a0e-119">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="44a0e-120">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="44a0e-120">**An Azure subscription**.</span></span> <span data-ttu-id="44a0e-121">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44a0e-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="44a0e-122">**Azure PowerShell 1.0 ou version ultérieure**.</span><span class="sxs-lookup"><span data-stu-id="44a0e-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="44a0e-123">Consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="44a0e-123">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="44a0e-124">**Principal du service Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44a0e-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="44a0e-125">Les étapes de ce didacticiel indiquent comment créer un principal du service dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44a0e-125">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span></span> <span data-ttu-id="44a0e-126">Toutefois, vous devez être administrateur Azure AD pour pouvoir créer un principal du service.</span><span class="sxs-lookup"><span data-stu-id="44a0e-126">However, you must be an Azure AD administrator to be able to create a service principal.</span></span> <span data-ttu-id="44a0e-127">Si vous êtes administrateur Azure AD, vous pouvez ignorer ce prérequis et poursuivre le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="44a0e-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    <span data-ttu-id="44a0e-128">**Si vous n’êtes pas administrateur Azure AD**, vous ne pouvez pas effectuer les étapes nécessaires à la création d’un principal du service.</span><span class="sxs-lookup"><span data-stu-id="44a0e-128">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span></span> <span data-ttu-id="44a0e-129">Dans ce cas, votre administrateur Azure AD doit d’abord créer un principal du service. Vous pourrez ensuite créer un cluster HDInsight avec Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="44a0e-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="44a0e-130">En outre, le principal du service doit être créé à l’aide d’un certificat, comme décrit dans [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) (Créer un principal du service avec certificat).</span><span class="sxs-lookup"><span data-stu-id="44a0e-130">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="44a0e-131">Créer un cluster HDInsight avec Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="44a0e-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="44a0e-132">Le modèle Resource Manager et les prérequis pour l’utiliser sont disponibles sur GitHub à la page [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage) (Déployer un cluster HDInsight Linux avec un nouveau compte Data Lake Store).</span><span class="sxs-lookup"><span data-stu-id="44a0e-132">The Resource Manager template, and the prerequisites for using the template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="44a0e-133">Suivez les instructions de ce lien pour créer un cluster HDInsight avec Azure Data Lake Store comme stockage supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="44a0e-133">Follow the instructions provided at this link to create an HDInsight cluster with Azure Data Lake Store as the additional storage.</span></span>

<span data-ttu-id="44a0e-134">Les instructions du lien mentionné ci-dessus requièrent PowerShell.</span><span class="sxs-lookup"><span data-stu-id="44a0e-134">The instructions at the link mentioned above require PowerShell.</span></span> <span data-ttu-id="44a0e-135">Avant de commencer à suivre ces instructions, vérifiez que vous vous connectez à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="44a0e-135">Before you start with those instructions, make sure you log in to your Azure account.</span></span> <span data-ttu-id="44a0e-136">Sur votre bureau, ouvrez une nouvelle fenêtre Azure PowerShell et entrez les extraits de code suivants.</span><span class="sxs-lookup"><span data-stu-id="44a0e-136">From your desktop, open a new Azure PowerShell window, and enter the following snippets.</span></span> <span data-ttu-id="44a0e-137">Lorsque vous êtes invité à vous connecter, vérifiez que vous vous connectez en tant qu’administrateur/propriétaire de l’abonnement :</span><span class="sxs-lookup"><span data-stu-id="44a0e-137">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span></span>

```
# Log in to your Azure account
Login-AzureRmAccount

# List all the subscriptions associated to your account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-to-the-azure-data-lake-store"></a><span data-ttu-id="44a0e-138">Charger des exemples de données sur l’Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="44a0e-138">Upload sample data to the Azure Data Lake Store</span></span>
<span data-ttu-id="44a0e-139">Le modèle Resource Manager crée un compte Data Lake Store et l’associe au cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="44a0e-139">The Resource Manager template creates a new Data Lake Store account and associates it with the HDInsight cluster.</span></span> <span data-ttu-id="44a0e-140">Vous devez charger des exemples de données sur le Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="44a0e-140">You must now upload some sample data to the Data Lake Store.</span></span> <span data-ttu-id="44a0e-141">Vous aurez besoin de ces données plus tard dans ce didacticiel, pour exécuter des tâches à partir d’un cluster HDInsight ayant accès au Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="44a0e-141">You'll need this data later in the tutorial to run jobs from an HDInsight cluster that access data in the Data Lake Store.</span></span> <span data-ttu-id="44a0e-142">Pour plus d’informations sur le chargement de données, consultez [Upload a file to your Data Lake Store](data-lake-store-get-started-portal.md#uploaddata) (Charger un fichier sur votre Data Lake Store).</span><span class="sxs-lookup"><span data-stu-id="44a0e-142">For instructions on how to upload data, see [Upload a file to your Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="44a0e-143">Si vous recherchez des exemples de données à charger, vous pouvez récupérer le dossier **Données Ambulance** dans le [dépôt Git Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="44a0e-143">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-the-sample-data"></a><span data-ttu-id="44a0e-144">Définir les ACL appropriées sur les exemples de données</span><span class="sxs-lookup"><span data-stu-id="44a0e-144">Set relevant ACLs on the sample data</span></span>
<span data-ttu-id="44a0e-145">Pour que les exemples de données que vous chargez soient accessibles à partir du cluster HDInsight, vous devez vérifier que l’application Azure AD qui est utilisée pour établir l’identité entre le cluster HDInsight et Data Lake Store a accès au fichier/dossier auquel vous essayez d’accéder.</span><span class="sxs-lookup"><span data-stu-id="44a0e-145">To make sure the sample data you upload is accessible from the HDInsight cluster, you must ensure that the Azure AD application that is used to establish identity between the HDInsight cluster and Data Lake Store has access to the file/folder you are trying to access.</span></span> <span data-ttu-id="44a0e-146">Pour ce faire, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="44a0e-146">To do this, perform the following steps.</span></span>

1. <span data-ttu-id="44a0e-147">Recherchez le nom de l’application Azure AD qui est associée au cluster HDInsight et au Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="44a0e-147">Find the name of the Azure AD application that is associated with HDInsight cluster and the Data Lake Store.</span></span> <span data-ttu-id="44a0e-148">Pour ce faire, vous pouvez ouvrir le panneau du cluster HDInsight que vous avez créé à l’aide du modèle Resource Manager, cliquer sur l’onglet **Identité AAD de cluster** et rechercher la valeur de **Nom d’affichage du principal du service**.</span><span class="sxs-lookup"><span data-stu-id="44a0e-148">One way to look for the name is to open the HDInsight cluster blade that you created using the Resource Manager template, click the **Cluster AAD Identity** tab, and look for the value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="44a0e-149">À présent, fournissez un accès à cette application Azure AD sur le fichier/dossier auquel vous souhaitez accéder à partir du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="44a0e-149">Now, provide access to this Azure AD application on the file/folder that you want to access from the HDInsight cluster.</span></span> <span data-ttu-id="44a0e-150">Pour définir les ACL adéquates sur le fichier/dossier dans Data Lake Store, consultez [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions) (Sécurisation des données dans Data Lake Store).</span><span class="sxs-lookup"><span data-stu-id="44a0e-150">To set the right ACLs on the file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a><span data-ttu-id="44a0e-151">Exécuter des tâches de test sur le cluster HDInsight pour utiliser Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="44a0e-151">Run test jobs on the HDInsight cluster to use the Data Lake Store</span></span>
<span data-ttu-id="44a0e-152">Après avoir configuré un cluster HDInsight, vous pouvez exécuter des tâches de test sur le cluster pour vérifier que le cluster HDInsight peut accéder à Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="44a0e-152">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="44a0e-153">Pour ce faire, nous allons exécuter un exemple de tâche Hive qui crée une table avec les exemples de données que vous avez téléchargés précédemment dans votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="44a0e-153">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span></span>

<span data-ttu-id="44a0e-154">Dans cette section, vous allez utiliser SSH dans un cluster HDInsight Linux et exécuter l’exemple de requête Hive.</span><span class="sxs-lookup"><span data-stu-id="44a0e-154">In this section you will SSH into an HDInsight Linux cluster and run the a sample Hive query.</span></span> <span data-ttu-id="44a0e-155">Si vous utilisez un client Windows, nous vous recommandons d’utiliser **PuTTY**, qui peut être téléchargé à partir de [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="44a0e-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="44a0e-156">Pour plus d’informations sur l’utilisation de PuTTY, consultez la rubrique [Utilisation de SSH avec Hadoop Linux dans HDInsight à partir de Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="44a0e-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="44a0e-157">Une fois connecté, démarrez l'interface de ligne de commande Hive à l'aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="44a0e-157">Once connected, start the Hive CLI by using the following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="44a0e-158">À l’aide de l’interface CLI, entrez les instructions suivantes pour créer une table nommée **vehicles** en utilisant les exemples de données dans Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="44a0e-158">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="44a0e-159">Le résultat doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="44a0e-159">You should see an output similar to the following:</span></span>

   ```
   1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
   1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
   1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
   1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
   1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
   1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
   1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
   1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
   1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
   1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="44a0e-160">Accéder à Data Lake Store avec les commandes HDFS</span><span class="sxs-lookup"><span data-stu-id="44a0e-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="44a0e-161">Une fois que vous avez configuré le cluster HDInsight pour qu'il utilise Data Lake Store, vous pouvez utiliser les commandes de l'interpréteur de commandes HDFS pour accéder au magasin.</span><span class="sxs-lookup"><span data-stu-id="44a0e-161">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span></span>

<span data-ttu-id="44a0e-162">Dans cette section, vous allez utiliser SSH dans un cluster HDInsight Linux et exécuter les commandes HDFS.</span><span class="sxs-lookup"><span data-stu-id="44a0e-162">In this section you will SSH into an HDInsight Linux cluster and run the HDFS commands.</span></span> <span data-ttu-id="44a0e-163">Si vous utilisez un client Windows, nous vous recommandons d’utiliser **PuTTY**, qui peut être téléchargé à partir de [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="44a0e-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="44a0e-164">Pour plus d’informations sur l’utilisation de PuTTY, consultez la rubrique [Utilisation de SSH avec Hadoop Linux dans HDInsight à partir de Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="44a0e-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="44a0e-165">Une fois connecté, utilisez la commande du système de fichiers HDFS suivante pour répertorier les fichiers dans le Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="44a0e-165">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="44a0e-166">Le fichier que vous avez téléchargé dans Data Lake Store doit y figurer.</span><span class="sxs-lookup"><span data-stu-id="44a0e-166">This should list the file that you uploaded earlier to the Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="44a0e-167">Vous pouvez également utiliser la commande `hdfs dfs -put` pour charger des fichiers dans Data Lake Store, puis utiliser `hdfs dfs -ls` pour vérifier si les fichiers ont été chargés avec succès.</span><span class="sxs-lookup"><span data-stu-id="44a0e-167">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="44a0e-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="44a0e-168">Next steps</span></span>
* [<span data-ttu-id="44a0e-169">Copier des données d’objets blob Stockage Azure vers Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="44a0e-169">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
