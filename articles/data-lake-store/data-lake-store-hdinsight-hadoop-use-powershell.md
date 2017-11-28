---
title: "PowerShell : cluster Azure HDInsight avec Data Lake Store comme stockage complémentaire | Microsoft Docs"
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/08/2017
ms.author: nitinme
ms.openlocfilehash: 7a7069adab5742a9dae2833c13a1db57337a41a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-powershell-to-create-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="47dcb-102">Utiliser Azure PowerShell pour créer un cluster HDInsight avec Data Lake Store (comme stockage complémentaire)</span><span class="sxs-lookup"><span data-stu-id="47dcb-102">Use Azure PowerShell to create an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="47dcb-103">Utilisation du portail</span><span class="sxs-lookup"><span data-stu-id="47dcb-103">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="47dcb-104">Utilisation de PowerShell (pour le stockage par défaut)</span><span class="sxs-lookup"><span data-stu-id="47dcb-104">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="47dcb-105">Utilisation de PowerShell (pour le stockage supplémentaire)</span><span class="sxs-lookup"><span data-stu-id="47dcb-105">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="47dcb-106">Utilisation du gestionnaire des ressources</span><span class="sxs-lookup"><span data-stu-id="47dcb-106">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="47dcb-107">Apprenez à utiliser Azure PowerShell pour configurer un cluster HDInsight avec Azure Data Lake Store **comme stockage supplémentaire**.</span><span class="sxs-lookup"><span data-stu-id="47dcb-107">Learn how to use Azure PowerShell to configure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="47dcb-108">Pour obtenir des instructions sur la création d’un cluster HDInsight avec Azure Data Lake Store comme stockage par défaut, voir [Créer un cluster HDInsight avec Data Lake Store comme stockage par défaut](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span><span class="sxs-lookup"><span data-stu-id="47dcb-108">For instructions on how to create an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

> [!NOTE]
> <span data-ttu-id="47dcb-109">Si vous vous apprêtez à utiliser Azure Data Lake Store en tant que stockage supplémentaire pour le cluster HDInsight, nous vous recommandons vivement de procéder ainsi lorsque vous créez le cluster comme décrit dans cet article.</span><span class="sxs-lookup"><span data-stu-id="47dcb-109">If you are going to use Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create the cluster as described in this article.</span></span> <span data-ttu-id="47dcb-110">L’ajout d’Azure Data Lake Store en tant que stockage supplémentaire à un cluster HDInsight existant est un processus complexe sujet aux erreurs.</span><span class="sxs-lookup"><span data-stu-id="47dcb-110">Adding Azure Data Lake Store as additional storage to an existing HDInsight cluster is a complicated process and prone to errors.</span></span>
>

<span data-ttu-id="47dcb-111">Pour les types de clusters pris en charge, Data Lake Store est utilisé comme compte de stockage par défaut ou supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="47dcb-111">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="47dcb-112">Lorsque Data Lake Store est utilisé comme espace de stockage supplémentaire, le compte de stockage par défaut pour les clusters est toujours Azure Storage Blob (WABS), et les fichiers associés au cluster (par exemple, les journaux, etc.) sont écrits dans le stockage par défaut, tandis que les données que vous souhaitez traiter peuvent être stockées dans un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="47dcb-112">When Data Lake Store is used as additional storage, the default storage account for the clusters will still be Azure Storage Blobs (WASB) and the cluster-related files (such as logs, etc.) are still written to the default storage, while the data that you want to process can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="47dcb-113">L’utilisation de Data Lake Store en tant que compte de stockage supplémentaire n’affecte pas les performances ni la capacité de lecture/écriture sur le stockage à partir du cluster.</span><span class="sxs-lookup"><span data-stu-id="47dcb-113">Using Data Lake Store as an additional storage account does not impact performance or the ability to read/write to the storage from the cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="47dcb-114">Utilisation de Data Lake Store pour le stockage de cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="47dcb-114">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="47dcb-115">Voici quelques considérations importantes pour l’utilisation de HDInsight avec Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="47dcb-115">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="47dcb-116">L’option permettant de créer des clusters HDInsight avec accès au Data Lake Store comme stockage supplémentaire est disponible si vous utilisez HDInsight versions 3.2, 3.4, 3.5 et 3.6.</span><span class="sxs-lookup"><span data-stu-id="47dcb-116">Option to create HDInsight clusters with access to Data Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="47dcb-117">Pour configurer HDInsight afin qu'il fonctionne avec Data Lake Store à l'aide de PowerShell, la procédure est la suivante :</span><span class="sxs-lookup"><span data-stu-id="47dcb-117">Configuring HDInsight to work with Data Lake Store using PowerShell involves the following steps:</span></span>

* <span data-ttu-id="47dcb-118">Créer un Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="47dcb-118">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="47dcb-119">Configurer l'authentification pour définir un accès à Data Lake Store en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="47dcb-119">Set up authentication for role-based access to Data Lake Store</span></span>
* <span data-ttu-id="47dcb-120">Créer un cluster HDInsight avec authentification à Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="47dcb-120">Create HDInsight cluster with authentication to Data Lake Store</span></span>
* <span data-ttu-id="47dcb-121">Lancer une tâche de test sur le cluster</span><span class="sxs-lookup"><span data-stu-id="47dcb-121">Run a test job on the cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47dcb-122">Composants requis</span><span class="sxs-lookup"><span data-stu-id="47dcb-122">Prerequisites</span></span>
<span data-ttu-id="47dcb-123">Avant de commencer ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="47dcb-123">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="47dcb-124">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="47dcb-124">**An Azure subscription**.</span></span> <span data-ttu-id="47dcb-125">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="47dcb-125">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="47dcb-126">**Azure PowerShell 1.0 ou version ultérieure**.</span><span class="sxs-lookup"><span data-stu-id="47dcb-126">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="47dcb-127">Consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="47dcb-127">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="47dcb-128">**Kit de développement logiciel (SDK) Windows**.</span><span class="sxs-lookup"><span data-stu-id="47dcb-128">**Windows SDK**.</span></span> <span data-ttu-id="47dcb-129">Vous pouvez l’installer à partir [d’ici](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="47dcb-129">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="47dcb-130">Il vous permet de créer un certificat de sécurité.</span><span class="sxs-lookup"><span data-stu-id="47dcb-130">You use this to create a security certificate.</span></span>
* <span data-ttu-id="47dcb-131">**Principal du service Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="47dcb-131">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="47dcb-132">Les étapes de ce didacticiel indiquent comment créer un principal du service dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="47dcb-132">Steps in this tutorial provide instructions on how to create a service principal in Azure AD.</span></span> <span data-ttu-id="47dcb-133">Toutefois, vous devez être administrateur Azure AD pour pouvoir créer un principal du service.</span><span class="sxs-lookup"><span data-stu-id="47dcb-133">However, you must be an Azure AD administrator to be able to create a service principal.</span></span> <span data-ttu-id="47dcb-134">Si vous êtes administrateur Azure AD, vous pouvez ignorer ce prérequis et poursuivre le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="47dcb-134">If you are an Azure AD administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    <span data-ttu-id="47dcb-135">**Si vous n’êtes pas administrateur Azure AD**, vous ne pouvez pas effectuer les étapes nécessaires à la création d’un principal du service.</span><span class="sxs-lookup"><span data-stu-id="47dcb-135">**If you are not an Azure AD administrator**, you will not be able to perform the steps required to create a service principal.</span></span> <span data-ttu-id="47dcb-136">Dans ce cas, votre administrateur Azure AD doit d’abord créer un principal du service. Vous pourrez ensuite créer un cluster HDInsight avec Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="47dcb-136">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="47dcb-137">En outre, le principal du service doit être créé à l’aide d’un certificat, comme décrit dans [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority) (Créer un principal du service avec certificat).</span><span class="sxs-lookup"><span data-stu-id="47dcb-137">Also, the service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="47dcb-138">Créer un Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="47dcb-138">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="47dcb-139">Pour créer un Data Lake Store, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="47dcb-139">Follow these steps to create a Data Lake Store.</span></span>

1. <span data-ttu-id="47dcb-140">Sur votre bureau, ouvrez une nouvelle fenêtre Azure PowerShell et entrez l'extrait de code suivant.</span><span class="sxs-lookup"><span data-stu-id="47dcb-140">From your desktop, open a new Azure PowerShell window, and enter the following snippet.</span></span> <span data-ttu-id="47dcb-141">Lorsque vous êtes invité à vous connecter, vérifiez que vous vous connectez en tant qu’administrateur/propriétaire de l’abonnement :</span><span class="sxs-lookup"><span data-stu-id="47dcb-141">When prompted to log in, make sure you log in as one of the subscription administrator/owner:</span></span>

        # Log in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > <span data-ttu-id="47dcb-142">Si vous recevez une erreur similaire à `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid` pendant l’inscription du fournisseur de ressources Data Lake Store, il est possible que votre abonnement ne figure pas dans la liste approuvée pour Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="47dcb-142">If you receive an error similar to `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid` when registering the Data Lake Store resource provider, it is possible that your subscription is not whitelisted for Azure Data Lake Store.</span></span> <span data-ttu-id="47dcb-143">Veillez à activer votre abonnement Azure pour la version préliminaire publique de Data Lake Store en suivant ces [instructions](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="47dcb-143">Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).</span></span>
   >
   >
2. <span data-ttu-id="47dcb-144">Un compte Azure Data Lake Store est associé à un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="47dcb-144">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="47dcb-145">Commencez par créer un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="47dcb-145">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="47dcb-146">Vous devriez obtenir un résultat similaire à ceci :</span><span class="sxs-lookup"><span data-stu-id="47dcb-146">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="47dcb-147">Créer un compte Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="47dcb-147">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="47dcb-148">Le nom de compte que vous spécifiez doit contenir uniquement des lettres minuscules et des chiffres.</span><span class="sxs-lookup"><span data-stu-id="47dcb-148">The account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="47dcb-149">Un résultat similaire à ce qui suit s’affiche normalement :</span><span class="sxs-lookup"><span data-stu-id="47dcb-149">You should see an output like the following:</span></span>

        ...
        ProvisioningState           : Succeeded
        State                       : Active
        CreationTime                : 5/5/2017 10:53:56 PM
        EncryptionState             : Enabled
        ...
        LastModifiedTime            : 5/5/2017 10:53:56 PM
        Endpoint                    : hdiadlstore.azuredatalakestore.net
        DefaultGroup                :
        Id                          : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp/providers/Microsoft.DataLakeStore/accounts/hdiadlstore
        Name                        : hdiadlstore
        Type                        : Microsoft.DataLakeStore/accounts
        Location                    : East US 2
        Tags                        : {}

5. <span data-ttu-id="47dcb-150">Téléchargez des exemples de données sur Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="47dcb-150">Upload some sample data to Azure Data Lake.</span></span> <span data-ttu-id="47dcb-151">Nous les utiliserons plus loin dans cet article pour vérifier que les données sont accessibles à partir d'un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47dcb-151">We'll use this later in this article to verify that the data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="47dcb-152">Si vous recherchez des exemples de données à charger, vous pouvez récupérer le dossier **Données Ambulance** dans le [Référentiel Git Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="47dcb-152">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path to data>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-to-data-lake-store"></a><span data-ttu-id="47dcb-153">Configurer l'authentification pour définir un accès à Data Lake Store en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="47dcb-153">Set up authentication for role-based access to Data Lake Store</span></span>
<span data-ttu-id="47dcb-154">Chaque abonnement Azure est associé à un Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="47dcb-154">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="47dcb-155">Les utilisateurs et services qui accèdent aux ressources de l’abonnement avec les API du portail Azure Classic ou d’Azure Resource Manager doivent au préalable s’authentifier avec cette application Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="47dcb-155">Users and services that access resources of the subscription using the Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="47dcb-156">L’accès est accordé aux abonnements et services Azure en leur affectant le rôle approprié sur une ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="47dcb-156">Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource.</span></span>  <span data-ttu-id="47dcb-157">Pour les services, un principal du service identifie le service dans Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="47dcb-157">For services, a service principal identifies the service in the Azure Active Directory (AAD).</span></span> <span data-ttu-id="47dcb-158">Cette section montre comment accorder l'accès à une ressource Azure (le compte Azure Data Lake Store créé précédemment) à un service d'application, comme HDInsight, en créant un principal du service pour l'application et en lui attribuant des rôles avec Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47dcb-158">This section illustrates how to grant an application service, like HDInsight, access to an Azure resource (the Azure Data Lake Store account you created earlier) by creating a service principal for the application and assigning roles to that via Azure PowerShell.</span></span>

<span data-ttu-id="47dcb-159">Pour configurer l'authentification Active Directory pour Azure Data Lake, vous devez effectuer les tâches suivantes.</span><span class="sxs-lookup"><span data-stu-id="47dcb-159">To set up Active Directory authentication for Azure Data Lake, you must perform the following tasks.</span></span>

* <span data-ttu-id="47dcb-160">Créer un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="47dcb-160">Create a self-signed certificate</span></span>
* <span data-ttu-id="47dcb-161">Créer une application dans Azure Active Directory et un principal du service</span><span class="sxs-lookup"><span data-stu-id="47dcb-161">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="47dcb-162">Créer un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="47dcb-162">Create a self-signed certificate</span></span>
<span data-ttu-id="47dcb-163">Assurez-vous que le [SDK Windows](https://dev.windows.com/en-us/downloads) est installé avant de suivre la procédure décrite dans cette section.</span><span class="sxs-lookup"><span data-stu-id="47dcb-163">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section.</span></span> <span data-ttu-id="47dcb-164">Vous devez également avoir créé un répertoire, comme **C:\mycertdir**, où sera créé le certificat.</span><span class="sxs-lookup"><span data-stu-id="47dcb-164">You must have also created a directory, such as **C:\mycertdir**, where the certificate will be created.</span></span>

1. <span data-ttu-id="47dcb-165">Dans la fenêtre PowerShell, accédez à l’emplacement où vous avez installé le Kit de développement logiciel (SDK) Windows (en général, `C:\Program Files (x86)\Windows Kits\10\bin\x86`) et utilisez l’utilitaire [MakeCert][makecert] pour créer un certificat auto-signé et une clé privée.</span><span class="sxs-lookup"><span data-stu-id="47dcb-165">From the PowerShell window, navigate to the location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key.</span></span> <span data-ttu-id="47dcb-166">Utilisez les commandes suivantes.</span><span class="sxs-lookup"><span data-stu-id="47dcb-166">Use the following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="47dcb-167">Vous devrez entrer le mot de passe de la clé privée.</span><span class="sxs-lookup"><span data-stu-id="47dcb-167">You will be prompted to enter the private key password.</span></span> <span data-ttu-id="47dcb-168">Une fois la commande exécutée avec succès, **CertFile.cer** et **mykey.pvk** apparaissent dans le répertoire du certificat que vous avez spécifié.</span><span class="sxs-lookup"><span data-stu-id="47dcb-168">After the command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in the certificate directory you specified.</span></span>
2. <span data-ttu-id="47dcb-169">Utilisez l’utilitaire [Pvk2Pfx][pvk2pfx] pour convertir en un fichier .pfx les fichiers .pvk et .cer créés par MakeCert.</span><span class="sxs-lookup"><span data-stu-id="47dcb-169">Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file.</span></span> <span data-ttu-id="47dcb-170">Exécutez la commande ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="47dcb-170">Run the following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="47dcb-171">Lorsque vous y êtes invité, entrez le mot de passe de la clé privée spécifié au préalable.</span><span class="sxs-lookup"><span data-stu-id="47dcb-171">When prompted enter the private key password you specified earlier.</span></span> <span data-ttu-id="47dcb-172">La valeur que vous donnez au paramètre **-po** est le mot de passe associé au fichier .pfx.</span><span class="sxs-lookup"><span data-stu-id="47dcb-172">The value you specify for the **-po** parameter is the password that is associated with the .pfx file.</span></span> <span data-ttu-id="47dcb-173">Une fois la commande exécutée avec succès, CertFile.pfx est visible dans le répertoire du certificat que vous avez spécifié.</span><span class="sxs-lookup"><span data-stu-id="47dcb-173">After the command successfully completes, you should also see a CertFile.pfx in the certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="47dcb-174">Créer une application Azure Active Directory et un principal du service</span><span class="sxs-lookup"><span data-stu-id="47dcb-174">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="47dcb-175">Cette section décrit les étapes pour créer un principal du service pour une application Azure Active Directory, attribuer un rôle au principal du service et vous authentifier en tant que principal du service en fournissant un certificat.</span><span class="sxs-lookup"><span data-stu-id="47dcb-175">In this section, you perform the steps to create a service principal for an Azure Active Directory application, assign a role to the service principal, and authenticate as the service principal by providing a certificate.</span></span> <span data-ttu-id="47dcb-176">Exécutez les commandes suivantes pour créer une application dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="47dcb-176">Run the following commands to create an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="47dcb-177">Collez les applets de commande suivantes dans la fenêtre de la console PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47dcb-177">Paste the following cmdlets in the PowerShell console window.</span></span> <span data-ttu-id="47dcb-178">Vérifiez que la valeur que vous donnez à la propriété **-DisplayName** est unique.</span><span class="sxs-lookup"><span data-stu-id="47dcb-178">Make sure the value you specify for the **-DisplayName** property is unique.</span></span> <span data-ttu-id="47dcb-179">En outre, les valeurs pour **-HomePage** et **-IdentiferUris** sont des valeurs d’espace réservé et ne sont pas vérifiées.</span><span class="sxs-lookup"><span data-stu-id="47dcb-179">Also, the values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter the password" # This is the password you specified for the .pfx file

        $certificatePFX = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2($certificateFilePath, $password)

        $rawCertificateData = $certificatePFX.GetRawCertData()

        $credential = [System.Convert]::ToBase64String($rawCertificateData)

        $application = New-AzureRmADApplication `
            -DisplayName "HDIADL" `
            -HomePage "https://contoso.com" `
            -IdentifierUris "https://mycontoso.com" `
            -CertValue $credential  `
            -StartDate $certificatePFX.NotBefore  `
            -EndDate $certificatePFX.NotAfter

        $applicationId = $application.ApplicationId
2. <span data-ttu-id="47dcb-180">Créez un principal du service avec l'ID d'application.</span><span class="sxs-lookup"><span data-stu-id="47dcb-180">Create a service principal using the application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="47dcb-181">Accordez au principal du service l’accès au dossier et au fichier Data Lake Store auxquels vous accéderez à partir du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47dcb-181">Grant the service principal access to the Data Lake Store folder and the file that you will access from the HDInsight cluster.</span></span> <span data-ttu-id="47dcb-182">L’extrait de code ci-dessous fournit l’accès à la racine du compte Data Lake Store (où vous avez copié l’exemple de fichier de données) et le fichier lui-même.</span><span class="sxs-lookup"><span data-stu-id="47dcb-182">The snippet below provides access to the root of the Data Lake Store account (where you copied the sample data file), and the file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="47dcb-183">Créer un cluster Linux HDInsight avec Data Lake Store comme stockage par supplémentaire</span><span class="sxs-lookup"><span data-stu-id="47dcb-183">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="47dcb-184">Dans cette section, nous créons un cluster HDInsight Hadoop Linux avec Data Lake Store comme stockage supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="47dcb-184">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="47dcb-185">Pour cette version, le cluster HDInsight et le Data Lake Store doivent se situer au même emplacement.</span><span class="sxs-lookup"><span data-stu-id="47dcb-185">For this release, the HDInsight cluster and the Data Lake Store must be in the same location.</span></span>

1. <span data-ttu-id="47dcb-186">Commencez par récupérer l’ID du client de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="47dcb-186">Start with retrieving the subscription tenant ID.</span></span> <span data-ttu-id="47dcb-187">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="47dcb-187">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="47dcb-188">Pour cette version, pour un cluster Hadoop, Data Lake Store ne peut être utilisé que comme stockage supplémentaire pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="47dcb-188">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for the cluster.</span></span> <span data-ttu-id="47dcb-189">Le stockage par défaut sera toujours les objets blob Azure Storage (WASB).</span><span class="sxs-lookup"><span data-stu-id="47dcb-189">The default storage will still be the Azure storage blobs (WASB).</span></span> <span data-ttu-id="47dcb-190">Par conséquent, nous allons tout d'abord créer le compte de stockage et les conteneurs de stockage requis par le cluster.</span><span class="sxs-lookup"><span data-stu-id="47dcb-190">So, we'll first create the storage account and storage containers required for the cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="47dcb-191">Créez le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47dcb-191">Create the HDInsight cluster.</span></span> <span data-ttu-id="47dcb-192">Utilisez les applets de commande suivantes.</span><span class="sxs-lookup"><span data-stu-id="47dcb-192">Use the following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have the same name for the cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # The number of nodes in the HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="47dcb-193">Après exécution de l'applet de commande, le résultat énumère les détails du cluster.</span><span class="sxs-lookup"><span data-stu-id="47dcb-193">After the cmdlet successfully completes, you should see an output listing the cluster details.</span></span>


## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-the-data-lake-store"></a><span data-ttu-id="47dcb-194">Exécuter des tâches de test sur le cluster HDInsight pour utiliser Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="47dcb-194">Run test jobs on the HDInsight cluster to use the Data Lake Store</span></span>
<span data-ttu-id="47dcb-195">Après avoir configuré un cluster HDInsight, vous pouvez exécuter des tâches de test sur le cluster pour vérifier que le cluster HDInsight peut accéder à Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="47dcb-195">After you have configured an HDInsight cluster, you can run test jobs on the cluster to test that the HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="47dcb-196">Pour ce faire, nous allons exécuter un exemple de tâche Hive qui crée une table avec les exemples de données que vous avez téléchargés précédemment dans votre Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="47dcb-196">To do so, we will run a sample Hive job that creates a table using the sample data that you uploaded earlier to your Data Lake Store.</span></span>

<span data-ttu-id="47dcb-197">Dans cette section, vous allez utiliser SSH dans le cluster HDInsight Linux que vous avez créé et exécuter l’exemple de requête Hive.</span><span class="sxs-lookup"><span data-stu-id="47dcb-197">In this section you will SSH into the HDInsight Linux cluster you created and run the a sample Hive query.</span></span>

* <span data-ttu-id="47dcb-198">Si vous utilisez un client Windows pour utiliser SSH dans le cluster, consultez la rubrique [Utilisation de SSH avec Hadoop Linux sur HDInsight à partir de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="47dcb-198">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="47dcb-199">Si vous utilisez un client Linux pour utiliser SSH dans le cluster, consultez la rubrique [Utilisation de SSH avec Hadoop Linux sur HDInsight à partir de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="47dcb-199">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="47dcb-200">Une fois connecté, démarrez l'interface de ligne de commande Hive à l'aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="47dcb-200">Once connected, start the Hive CLI by using the following command:</span></span>

        hive
2. <span data-ttu-id="47dcb-201">À l’aide de l’interface CLI, entrez les instructions suivantes pour créer une table nommée **vehicles** en utilisant les exemples de données dans Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="47dcb-201">Using the CLI, enter the following statements to create a new table named **vehicles** by using the sample data in the Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="47dcb-202">Le résultat doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="47dcb-202">You should see an output similar to the following:</span></span>

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

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="47dcb-203">Accéder à Data Lake Store avec les commandes HDFS</span><span class="sxs-lookup"><span data-stu-id="47dcb-203">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="47dcb-204">Une fois que vous avez configuré le cluster HDInsight pour qu'il utilise Data Lake Store, vous pouvez utiliser les commandes de l'interpréteur de commandes HDFS pour accéder au magasin.</span><span class="sxs-lookup"><span data-stu-id="47dcb-204">Once you have configured the HDInsight cluster to use Data Lake Store, you can use the HDFS shell commands to access the store.</span></span>

<span data-ttu-id="47dcb-205">Dans cette section, vous allez utiliser SSH dans le cluster HDInsight Linux que vous avez créé et exécuter les commandes HDFS.</span><span class="sxs-lookup"><span data-stu-id="47dcb-205">In this section you will SSH into the HDInsight Linux cluster you created and run the HDFS commands.</span></span>

* <span data-ttu-id="47dcb-206">Si vous utilisez un client Windows pour utiliser SSH dans le cluster, consultez la rubrique [Utilisation de SSH avec Hadoop Linux sur HDInsight à partir de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="47dcb-206">If you are using a Windows client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="47dcb-207">Si vous utilisez un client Linux pour utiliser SSH dans le cluster, consultez la rubrique [Utilisation de SSH avec Hadoop Linux sur HDInsight à partir de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="47dcb-207">If you are using a Linux client to SSH into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="47dcb-208">Une fois connecté, utilisez la commande du système de fichiers HDFS suivante pour répertorier les fichiers dans le Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="47dcb-208">Once connected, use the following HDFS filesystem command to list the files in the Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="47dcb-209">Le fichier que vous avez téléchargé dans Data Lake Store doit y figurer.</span><span class="sxs-lookup"><span data-stu-id="47dcb-209">This should list the file that you uploaded earlier to the Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="47dcb-210">Vous pouvez également utiliser la commande `hdfs dfs -put` pour charger des fichiers dans Data Lake Store, puis utiliser `hdfs dfs -ls` pour vérifier si les fichiers ont été chargés avec succès.</span><span class="sxs-lookup"><span data-stu-id="47dcb-210">You can also use the `hdfs dfs -put` command to upload some files to the Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="47dcb-211">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="47dcb-211">See Also</span></span>
* [<span data-ttu-id="47dcb-212">Portail : Créer un cluster HDInsight pour utiliser Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="47dcb-212">Portal: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
