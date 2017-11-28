---
title: "aaaUse modèles Azure toocreate HDInsight et Data Lake Store | Documents Microsoft"
description: "Utilisez toocreate de modèles Azure Resource Manager et clusters HDInsight avec Azure Data Lake Store"
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
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a><span data-ttu-id="fbbf5-103">Créer un cluster HDInsight avec Data Lake Store à l’aide d’un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fbbf5-103">Create an HDInsight cluster with Data Lake Store using Azure Resource Manager template</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fbbf5-104">Utilisation du portail</span><span class="sxs-lookup"><span data-stu-id="fbbf5-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="fbbf5-105">Utilisation de PowerShell (pour le stockage par défaut)</span><span class="sxs-lookup"><span data-stu-id="fbbf5-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="fbbf5-106">Utilisation de PowerShell (pour le stockage supplémentaire)</span><span class="sxs-lookup"><span data-stu-id="fbbf5-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="fbbf5-107">Utilisation du gestionnaire des ressources</span><span class="sxs-lookup"><span data-stu-id="fbbf5-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="fbbf5-108">Découvrez comment toouse Azure PowerShell tooconfigure un HDInsight de cluster avec Azure Data Lake Store **en tant que stockage supplémentaire**.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span>

<span data-ttu-id="fbbf5-109">Pour les types de clusters pris en charge, Data Lake Store est utilisé comme compte de stockage par défaut ou supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-109">For supported cluster types, Data Lake Store be used as an default storage or additional storage account.</span></span> <span data-ttu-id="fbbf5-110">Lorsque Data Lake Store est utilisé comme espace de stockage supplémentaire, compte de stockage par défaut hello pour les clusters de hello sera toujours les objets BLOB de stockage Azure (WASB) et fichiers hello cluster (par exemple, les journaux, etc.) sont toujours enregistrées toohello du stockage par défaut, lors des données hello que vous avez choix tooprocess peuvent être stockées dans un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-110">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="fbbf5-111">À l’aide de Data Lake Store en tant qu’un compte de stockage supplémentaires n’affecte pas les performances ou le stockage de toohello hello capacité tooread/écriture à partir du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-111">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="fbbf5-112">Utilisation de Data Lake Store pour le stockage de cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="fbbf5-112">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="fbbf5-113">Voici quelques considérations importantes pour l’utilisation de HDInsight avec Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="fbbf5-113">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="fbbf5-114">Clusters de HDInsight option toocreate avec un accès tooData Lake Store en tant que stockage de la valeur par défaut est disponible pour HDInsight version 3.5 et 3.6.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-114">Option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="fbbf5-115">Clusters de HDInsight option toocreate avec un accès tooData Lake Store en tant que stockage supplémentaire est disponible pour les versions 3.2, 3.4, 3.5 et 3.6 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-115">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="fbbf5-116">Dans cet article, nous approvisionnons un cluster Hadoop avec Data Lake Store comme stockage supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-116">In this article, we provision a Hadoop cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="fbbf5-117">Pour savoir comment toocreate un Hadoop cluster avec Data Lake Store en tant que stockage par défaut, consultez [créer un cluster HDInsight à l’aide du portail Azure Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fbbf5-117">For instructions on how toocreate a Hadoop cluster with Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbbf5-118">Composants requis</span><span class="sxs-lookup"><span data-stu-id="fbbf5-118">Prerequisites</span></span>
<span data-ttu-id="fbbf5-119">Avant de commencer ce didacticiel, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="fbbf5-119">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="fbbf5-120">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-120">**An Azure subscription**.</span></span> <span data-ttu-id="fbbf5-121">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbbf5-121">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="fbbf5-122">**Azure PowerShell 1.0 ou version ultérieure**.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-122">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="fbbf5-123">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fbbf5-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="fbbf5-124">**Principal du service Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-124">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="fbbf5-125">Étapes de ce didacticiel fournissent des instructions sur la façon de toocreate un principal de service dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-125">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="fbbf5-126">Toutefois, vous devez être un toocreate en mesure de Azure AD administrateur toobe un principal de service.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-126">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="fbbf5-127">Si vous êtes un administrateur Azure AD, vous pouvez ignorer cette condition préalable et poursuivre le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-127">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="fbbf5-128">**Si vous n’êtes pas un administrateur Azure AD**, vous ne serez pas en mesure de tooperform hello étapes requises toocreate un principal de service.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-128">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="fbbf5-129">Dans ce cas, votre administrateur Azure AD doit d’abord créer un principal du service. Vous pourrez ensuite créer un cluster HDInsight avec Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-129">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="fbbf5-130">En outre, hello principal du service doit être créé à l’aide d’un certificat, comme décrit dans [créer un principal de service avec certificat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="fbbf5-130">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a><span data-ttu-id="fbbf5-131">Créer un cluster HDInsight avec Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="fbbf5-131">Create an HDInsight cluster with Azure Data Lake Store</span></span>
<span data-ttu-id="fbbf5-132">modèle de gestionnaire de ressources Hello et conditions préalables de hello pour à l’aide du modèle de hello, sont disponibles sur GitHub à l’adresse [déployer un cluster HDInsight Linux avec la nouvelle Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="fbbf5-132">hello Resource Manager template, and hello prerequisites for using hello template, are available on GitHub at [Deploy a HDInsight Linux cluster with new Data Lake Store](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage).</span></span> <span data-ttu-id="fbbf5-133">Suivez les instructions de hello fournies à cette toocreate lien un cluster HDInsight avec Azure Data Lake Store en tant qu’espace de stockage supplémentaire hello.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-133">Follow hello instructions provided at this link toocreate an HDInsight cluster with Azure Data Lake Store as hello additional storage.</span></span>

<span data-ttu-id="fbbf5-134">les instructions de Hello au lien hello mentionnés ci-dessus requièrent PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-134">hello instructions at hello link mentioned above require PowerShell.</span></span> <span data-ttu-id="fbbf5-135">Avant de commencer avec ces instructions, vérifiez que vous vous connectez tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-135">Before you start with those instructions, make sure you log in tooyour Azure account.</span></span> <span data-ttu-id="fbbf5-136">À partir de votre bureau, ouvrez une nouvelle fenêtre Azure PowerShell et entrez hello suivant des extraits de code.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-136">From your desktop, open a new Azure PowerShell window, and enter hello following snippets.</span></span> <span data-ttu-id="fbbf5-137">Toolog demandée, assurez-vous que vous connectez en tant qu’un des admininistrators/propriétaire de l’abonnement hello :</span><span class="sxs-lookup"><span data-stu-id="fbbf5-137">When prompted toolog in, make sure you log in as one of hello subscription admininistrators/owner:</span></span>

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a><span data-ttu-id="fbbf5-138">Télécharger l’exemple données toohello Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="fbbf5-138">Upload sample data toohello Azure Data Lake Store</span></span>
<span data-ttu-id="fbbf5-139">modèle de gestionnaire de ressources Hello crée un nouveau compte Data Lake Store et l’associe à cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-139">hello Resource Manager template creates a new Data Lake Store account and associates it with hello HDInsight cluster.</span></span> <span data-ttu-id="fbbf5-140">Vous devez maintenant télécharger certaines toohello de données exemple Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-140">You must now upload some sample data toohello Data Lake Store.</span></span> <span data-ttu-id="fbbf5-141">Vous aurez besoin de ces données plus loin dans les tâches de didacticiel toorun hello à partir d’un cluster HDInsight qui accèdent aux données hello Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-141">You'll need this data later in hello tutorial toorun jobs from an HDInsight cluster that access data in hello Data Lake Store.</span></span> <span data-ttu-id="fbbf5-142">Pour obtenir des instructions sur la façon de tooupload de données, consultez [télécharger un fichier de tooyour Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span><span class="sxs-lookup"><span data-stu-id="fbbf5-142">For instructions on how tooupload data, see [Upload a file tooyour Data Lake Store](data-lake-store-get-started-portal.md#uploaddata).</span></span> <span data-ttu-id="fbbf5-143">Si vous recherchez des tooupload de données d’exemple, vous pouvez obtenir hello **Ambulance données** dossier hello [référentiel Git de LAC de données Azure](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="fbbf5-143">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

## <a name="set-relevant-acls-on-hello-sample-data"></a><span data-ttu-id="fbbf5-144">Définir les ACL appropriées sur les données d’exemple hello</span><span class="sxs-lookup"><span data-stu-id="fbbf5-144">Set relevant ACLs on hello sample data</span></span>
<span data-ttu-id="fbbf5-145">toomake que données exemple hello que vous chargez sont accessibles à partir du cluster HDInsight de hello, vous devez vous assurer qu’application hello Azure AD qui est l’identité tooestablish utilisée entre le cluster HDInsight de hello et Data Lake Store a accès toohello fichier/dossier que vous êtes la tentative de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-145">toomake sure hello sample data you upload is accessible from hello HDInsight cluster, you must ensure that hello Azure AD application that is used tooestablish identity between hello HDInsight cluster and Data Lake Store has access toohello file/folder you are trying tooaccess.</span></span> <span data-ttu-id="fbbf5-146">toodo, effectuer hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-146">toodo this, perform hello following steps.</span></span>

1. <span data-ttu-id="fbbf5-147">Rechercher le nom hello de hello application Azure AD qui est associée au cluster HDInsight et hello Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-147">Find hello name of hello Azure AD application that is associated with HDInsight cluster and hello Data Lake Store.</span></span> <span data-ttu-id="fbbf5-148">Une façon toolook pour le nom de hello tooopen panneau du cluster HDInsight de hello que vous avez créé à l’aide du modèle de gestionnaire de ressources hello, cliquez sur hello **Cluster AAD identité** onglet et recherchez la valeur hello **Principal du Service Nom d’affichage**.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-148">One way toolook for hello name is tooopen hello HDInsight cluster blade that you created using hello Resource Manager template, click hello **Cluster AAD Identity** tab, and look for hello value of **Service Principal Display Name**.</span></span>
2. <span data-ttu-id="fbbf5-149">Maintenant, fournir des accès toothis application Azure AD sur hello fichier/dossier que vous souhaitez tooaccess à partir du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-149">Now, provide access toothis Azure AD application on hello file/folder that you want tooaccess from hello HDInsight cluster.</span></span> <span data-ttu-id="fbbf5-150">tooset hello ACL sur le fichier/dossier hello dans Data Lake Store, voir [sécurisation des données dans Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span><span class="sxs-lookup"><span data-stu-id="fbbf5-150">tooset hello right ACLs on hello file/folder in Data Lake Store, see [Securing data in Data Lake Store](data-lake-store-secure-data.md#filepermissions).</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="fbbf5-151">Exécuter les tâches de test sur Bonjour HDInsight cluster toouse Bonjour Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="fbbf5-151">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="fbbf5-152">Après avoir configuré un cluster HDInsight, vous pouvez exécuter les travaux test sur hello cluster tootest que hello HDInsight peut accéder à Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-152">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="fbbf5-153">toodo par conséquent, nous allons exécuter un travail Hive exemple qui crée une table à l’aide des données d’exemple hello que vous avez téléchargé antérieures tooyour Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-153">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="fbbf5-154">Dans cette section sera SSH dans un cluster HDInsight Linux et une exécution hello un exemple de requête Hive.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-154">In this section you will SSH into an HDInsight Linux cluster and run hello a sample Hive query.</span></span> <span data-ttu-id="fbbf5-155">Si vous utilisez un client Windows, nous vous recommandons d’utiliser **PuTTY**, qui peut être téléchargé à partir de [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="fbbf5-155">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="fbbf5-156">Pour plus d’informations sur l’utilisation de PuTTY, consultez la rubrique [Utilisation de SSH avec Hadoop Linux dans HDInsight à partir de Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="fbbf5-156">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

1. <span data-ttu-id="fbbf5-157">Une fois connecté, démarrer hello CLI de la ruche à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="fbbf5-157">Once connected, start hello Hive CLI by using hello following command:</span></span>

   ```
   hive
   ```
2. <span data-ttu-id="fbbf5-158">À l’aide de hello CLI, entrez hello suivant les instructions toocreate une nouvelle table nommée **véhicules** à l’aide des données d’exemple hello Bonjour Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="fbbf5-158">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   <span data-ttu-id="fbbf5-159">Vous devez voir s’afficher une sortie similaire toohello :</span><span class="sxs-lookup"><span data-stu-id="fbbf5-159">You should see an output similar toohello following:</span></span>

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


## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="fbbf5-160">Accéder à Data Lake Store avec les commandes HDFS</span><span class="sxs-lookup"><span data-stu-id="fbbf5-160">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="fbbf5-161">Une fois que vous avez configuré le cluster HDInsight de hello toouse Data Lake Store, vous pouvez utiliser hello HDFS shell commandes tooaccess hello magasin.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-161">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="fbbf5-162">Dans cette section sera SSH dans un cluster HDInsight Linux et une exécution hello commandes HDFS.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-162">In this section you will SSH into an HDInsight Linux cluster and run hello HDFS commands.</span></span> <span data-ttu-id="fbbf5-163">Si vous utilisez un client Windows, nous vous recommandons d’utiliser **PuTTY**, qui peut être téléchargé à partir de [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="fbbf5-163">If you are using a Windows client, we recommend using **PuTTY**, which can be downloaded from [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span></span>

<span data-ttu-id="fbbf5-164">Pour plus d’informations sur l’utilisation de PuTTY, consultez la rubrique [Utilisation de SSH avec Hadoop Linux dans HDInsight à partir de Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="fbbf5-164">For more information on using PuTTY, see [Use SSH with Linux-based Hadoop on HDInsight from Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>

<span data-ttu-id="fbbf5-165">Une fois connecté, utilisez hello suivant fichiers HDFS filesystem commande toolist hello Bonjour Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-165">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

<span data-ttu-id="fbbf5-166">Elle doit répertorier fichier hello que vous avez téléchargé antérieures toohello Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-166">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

<span data-ttu-id="fbbf5-167">Vous pouvez également utiliser hello `hdfs dfs -put` commande tooupload certains toohello fichiers Data Lake Store, puis utilisez `hdfs dfs -ls` tooverify indique si les fichiers de hello ont été téléchargés avec succès.</span><span class="sxs-lookup"><span data-stu-id="fbbf5-167">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fbbf5-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fbbf5-168">Next steps</span></span>
* [<span data-ttu-id="fbbf5-169">Copier des données d’objets BLOB de stockage Azure tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="fbbf5-169">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-wasb-distcp.md)
