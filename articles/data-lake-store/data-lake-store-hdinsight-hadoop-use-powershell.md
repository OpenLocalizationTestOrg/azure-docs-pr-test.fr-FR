---
<span data-ttu-id="d8a85-101">titre : aaa « PowerShell : cluster Azure HDInsight avec Data Lake Store en tant que stockage complémentaire | Les services Microsoft Docs » : data lake store, hdinsight documentationcenter : '' auteur : Gestionnaire de nitinme : jhubbard éditeur : cgronlun</span><span class="sxs-lookup"><span data-stu-id="d8a85-101">title: aaa"PowerShell: Azure HDInsight cluster with Data Lake Store as add-on storage | Microsoft Docs" services: data-lake-store,hdinsight documentationcenter: '' author: nitinme manager: jhubbard editor: cgronlun</span></span>

<span data-ttu-id="d8a85-102">MS.AssetId : 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service : magasin de données lake ms.devlang : na ms.topic : article ms.tgt_pltfrm : na ms.workload : ms.date de données volumineuses : 06/08/2017 ms.author : nitinme</span><span class="sxs-lookup"><span data-stu-id="d8a85-102">ms.assetid: 164ada5a-222e-4be2-bd32-e51dbe993bc0 ms.service: data-lake-store ms.devlang: na ms.topic: article ms.tgt_pltfrm: na ms.workload: big-data ms.date: 06/08/2017 ms.author: nitinme</span></span>

---
# <a name="use-azure-powershell-toocreate-an-hdinsight-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="d8a85-103">Utiliser Azure PowerShell toocreate un cluster HDInsight avec Data Lake Store (en tant que stockage supplémentaire)</span><span class="sxs-lookup"><span data-stu-id="d8a85-103">Use Azure PowerShell toocreate an HDInsight cluster with Data Lake Store (as additional storage)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8a85-104">Utilisation du portail</span><span class="sxs-lookup"><span data-stu-id="d8a85-104">Using Portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="d8a85-105">Utilisation de PowerShell (pour le stockage par défaut)</span><span class="sxs-lookup"><span data-stu-id="d8a85-105">Using PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="d8a85-106">Utilisation de PowerShell (pour le stockage supplémentaire)</span><span class="sxs-lookup"><span data-stu-id="d8a85-106">Using PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="d8a85-107">Utilisation du gestionnaire des ressources</span><span class="sxs-lookup"><span data-stu-id="d8a85-107">Using Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

<span data-ttu-id="d8a85-108">Découvrez comment toouse Azure PowerShell tooconfigure un HDInsight de cluster avec Azure Data Lake Store **en tant que stockage supplémentaire**.</span><span class="sxs-lookup"><span data-stu-id="d8a85-108">Learn how toouse Azure PowerShell tooconfigure an HDInsight cluster with Azure Data Lake Store, **as additional storage**.</span></span> <span data-ttu-id="d8a85-109">Pour savoir comment toocreate un HDInsight de cluster avec Azure Data Lake Store en tant que stockage par défaut, consultez [créer un cluster HDInsight avec Data Lake Store en tant que stockage de la valeur par défaut](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span><span class="sxs-lookup"><span data-stu-id="d8a85-109">For instructions on how toocreate an HDInsight cluster with Azure Data Lake Store as default storage, see [Create an HDInsight cluster with Data Lake Store as default storage](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d8a85-110">Si vous vous apprêtez toouse Azure Data Lake Store en tant que stockage supplémentaire pour le cluster HDInsight, nous vous recommandons vivement de procéder ainsi lorsque vous créez le cluster de hello comme décrit dans cet article.</span><span class="sxs-lookup"><span data-stu-id="d8a85-110">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="d8a85-111">Ajout d’Azure Data Lake Store en tant que stockage supplémentaire tooan cluster HDInsight existant est un processus complexe et susceptible d’engendrer des tooerrors.</span><span class="sxs-lookup"><span data-stu-id="d8a85-111">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

<span data-ttu-id="d8a85-112">Pour les types de clusters pris en charge, Data Lake Store est utilisé comme compte de stockage par défaut ou supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="d8a85-112">For supported cluster types, Data Lake Store can be used as a default storage or additional storage account.</span></span> <span data-ttu-id="d8a85-113">Lorsque Data Lake Store est utilisé comme espace de stockage supplémentaire, compte de stockage par défaut hello pour les clusters de hello sera toujours les objets BLOB de stockage Azure (WASB) et fichiers hello cluster (par exemple, les journaux, etc.) sont toujours enregistrées toohello du stockage par défaut, lors des données hello que vous avez choix tooprocess peuvent être stockées dans un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d8a85-113">When Data Lake Store is used as additional storage, hello default storage account for hello clusters will still be Azure Storage Blobs (WASB) and hello cluster-related files (such as logs, etc.) are still written toohello default storage, while hello data that you want tooprocess can be stored in a Data Lake Store account.</span></span> <span data-ttu-id="d8a85-114">À l’aide de Data Lake Store en tant qu’un compte de stockage supplémentaires n’affecte pas les performances ou le stockage de toohello hello capacité tooread/écriture à partir du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="d8a85-114">Using Data Lake Store as an additional storage account does not impact performance or hello ability tooread/write toohello storage from hello cluster.</span></span>

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a><span data-ttu-id="d8a85-115">Utilisation de Data Lake Store pour le stockage de cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="d8a85-115">Using Data Lake Store for HDInsight cluster storage</span></span>

<span data-ttu-id="d8a85-116">Voici quelques considérations importantes pour l’utilisation de HDInsight avec Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="d8a85-116">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="d8a85-117">Clusters de HDInsight option toocreate avec un accès tooData Lake Store en tant que stockage supplémentaire est disponible pour les versions 3.2, 3.4, 3.5 et 3.6 de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d8a85-117">Option toocreate HDInsight clusters with access tooData Lake Store as additional storage is available for HDInsight versions 3.2, 3.4, 3.5, and 3.6.</span></span>

<span data-ttu-id="d8a85-118">La configuration HDInsight toowork avec Data Lake Store à l’aide de PowerShell implique de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d8a85-118">Configuring HDInsight toowork with Data Lake Store using PowerShell involves hello following steps:</span></span>

* <span data-ttu-id="d8a85-119">Créer un Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d8a85-119">Create an Azure Data Lake Store</span></span>
* <span data-ttu-id="d8a85-120">Configurer l’authentification dans en fonction du rôle d’accès tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="d8a85-120">Set up authentication for role-based access tooData Lake Store</span></span>
* <span data-ttu-id="d8a85-121">Créer un cluster HDInsight avec authentification tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="d8a85-121">Create HDInsight cluster with authentication tooData Lake Store</span></span>
* <span data-ttu-id="d8a85-122">Exécuter une tâche de test sur le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="d8a85-122">Run a test job on hello cluster</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8a85-123">Composants requis</span><span class="sxs-lookup"><span data-stu-id="d8a85-123">Prerequisites</span></span>
<span data-ttu-id="d8a85-124">Avant de commencer ce didacticiel, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="d8a85-124">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="d8a85-125">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="d8a85-125">**An Azure subscription**.</span></span> <span data-ttu-id="d8a85-126">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d8a85-126">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d8a85-127">**Azure PowerShell 1.0 ou version ultérieure**.</span><span class="sxs-lookup"><span data-stu-id="d8a85-127">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="d8a85-128">Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d8a85-128">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="d8a85-129">**Kit de développement logiciel (SDK) Windows**.</span><span class="sxs-lookup"><span data-stu-id="d8a85-129">**Windows SDK**.</span></span> <span data-ttu-id="d8a85-130">Vous pouvez l’installer à partir d’ [ici](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="d8a85-130">You can install it from [here](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="d8a85-131">Vous utilisez ce toocreate un certificat de sécurité.</span><span class="sxs-lookup"><span data-stu-id="d8a85-131">You use this toocreate a security certificate.</span></span>
* <span data-ttu-id="d8a85-132">**Principal du service Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d8a85-132">**Azure Active Directory Service Principal**.</span></span> <span data-ttu-id="d8a85-133">Étapes de ce didacticiel fournissent des instructions sur la façon de toocreate un principal de service dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8a85-133">Steps in this tutorial provide instructions on how toocreate a service principal in Azure AD.</span></span> <span data-ttu-id="d8a85-134">Toutefois, vous devez être un toocreate en mesure de Azure AD administrateur toobe un principal de service.</span><span class="sxs-lookup"><span data-stu-id="d8a85-134">However, you must be an Azure AD administrator toobe able toocreate a service principal.</span></span> <span data-ttu-id="d8a85-135">Si vous êtes un administrateur Azure AD, vous pouvez ignorer cette condition préalable et poursuivre le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="d8a85-135">If you are an Azure AD administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    <span data-ttu-id="d8a85-136">**Si vous n’êtes pas un administrateur Azure AD**, vous ne serez pas en mesure de tooperform hello étapes requises toocreate un principal de service.</span><span class="sxs-lookup"><span data-stu-id="d8a85-136">**If you are not an Azure AD administrator**, you will not be able tooperform hello steps required toocreate a service principal.</span></span> <span data-ttu-id="d8a85-137">Dans ce cas, votre administrateur Azure AD doit d’abord créer un principal du service. Vous pourrez ensuite créer un cluster HDInsight avec Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d8a85-137">In such a case, your Azure AD administrator must first create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="d8a85-138">En outre, hello principal du service doit être créé à l’aide d’un certificat, comme décrit dans [créer un principal de service avec certificat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="d8a85-138">Also, hello service principal must be created using a certificate, as described at [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>

## <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="d8a85-139">Créer un Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d8a85-139">Create an Azure Data Lake Store</span></span>
<span data-ttu-id="d8a85-140">Suivez ces étapes de toocreate un Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d8a85-140">Follow these steps toocreate a Data Lake Store.</span></span>

1. <span data-ttu-id="d8a85-141">À partir de votre bureau, ouvrez une nouvelle fenêtre Azure PowerShell et entrez hello suivant extrait de code.</span><span class="sxs-lookup"><span data-stu-id="d8a85-141">From your desktop, open a new Azure PowerShell window, and enter hello following snippet.</span></span> <span data-ttu-id="d8a85-142">Toolog demandée, assurez-vous que vous vous connectez comme administrateur/propriétaire de l’abonnement hello :</span><span class="sxs-lookup"><span data-stu-id="d8a85-142">When prompted toolog in, make sure you log in as one of hello subscription administrator/owner:</span></span>

        # Log in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

   > [!NOTE]
   > <span data-ttu-id="d8a85-143">Si vous recevez un message d’erreur similaire trop`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` lorsque vous inscrivez le fournisseur de ressources Data Lake Store hello, il est possible que votre abonnement n’est pas dans la liste approuvée pour Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d8a85-143">If you receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid` when registering hello Data Lake Store resource provider, it is possible that your subscription is not whitelisted for Azure Data Lake Store.</span></span> <span data-ttu-id="d8a85-144">Veillez à activer votre abonnement Azure pour la version préliminaire publique de Data Lake Store en suivant ces [instructions](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d8a85-144">Make sure you enable your Azure subscription for Data Lake Store public preview by following these [instructions](data-lake-store-get-started-portal.md).</span></span>
   >
   >
2. <span data-ttu-id="d8a85-145">Un compte Azure Data Lake Store est associé à un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="d8a85-145">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="d8a85-146">Commencez par créer un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="d8a85-146">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="d8a85-147">Vous devriez obtenir un résultat similaire à ceci :</span><span class="sxs-lookup"><span data-stu-id="d8a85-147">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="d8a85-148">Créer un compte Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d8a85-148">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="d8a85-149">compte Hello nom que vous spécifiez doit contenir uniquement des lettres minuscules et chiffres.</span><span class="sxs-lookup"><span data-stu-id="d8a85-149">hello account name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="d8a85-150">Vous devez voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="d8a85-150">You should see an output like hello following:</span></span>

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

5. <span data-ttu-id="d8a85-151">Télécharger certaines tooAzure de données exemple lac de données.</span><span class="sxs-lookup"><span data-stu-id="d8a85-151">Upload some sample data tooAzure Data Lake.</span></span> <span data-ttu-id="d8a85-152">Nous l’utiliserons plus loin dans cette tooverify article que les données de salutation sont accessibles à partir d’un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d8a85-152">We'll use this later in this article tooverify that hello data is accessible from an HDInsight cluster.</span></span> <span data-ttu-id="d8a85-153">Si vous recherchez des tooupload de données d’exemple, vous pouvez obtenir hello **Ambulance données** dossier hello [référentiel Git de LAC de données Azure](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="d8a85-153">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span>

        $myrootdir = "/"
        Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\<path toodata>\vehicle1_09142014.csv" -Destination $myrootdir\vehicle1_09142014.csv


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="d8a85-154">Configurer l’authentification dans en fonction du rôle d’accès tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="d8a85-154">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="d8a85-155">Chaque abonnement Azure est associé à un Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8a85-155">Every Azure subscription is associated with an Azure Active Directory.</span></span> <span data-ttu-id="d8a85-156">Les utilisateurs et services qui accèdent aux ressources d’abonnement hello à l’aide de hello portail classique Azure ou des API Azure Resource Manager doivent s’authentifier avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8a85-156">Users and services that access resources of hello subscription using hello Azure Classic Portal or Azure Resource Manager API must first authenticate with that Azure Active Directory.</span></span> <span data-ttu-id="d8a85-157">L’accès est accordé tooAzure abonnements et services en leur attribuant le rôle approprié de hello sur une ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="d8a85-157">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span>  <span data-ttu-id="d8a85-158">Pour les services, un principal du service identifie le service hello Bonjour Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="d8a85-158">For services, a service principal identifies hello service in hello Azure Active Directory (AAD).</span></span> <span data-ttu-id="d8a85-159">Cette section illustre comment toogrant une application de service, telles que HDInsight, tooan d’accès aux ressources Azure (hello compte Azure Data Lake Store créé précédemment) en créant un principal de service pour l’application hello et en assignant des toothat rôles via Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d8a85-159">This section illustrates how toogrant an application service, like HDInsight, access tooan Azure resource (hello Azure Data Lake Store account you created earlier) by creating a service principal for hello application and assigning roles toothat via Azure PowerShell.</span></span>

<span data-ttu-id="d8a85-160">tooset l’authentification Active Directory pour Azure Data Lake, vous devez effectuer hello tâches suivantes.</span><span class="sxs-lookup"><span data-stu-id="d8a85-160">tooset up Active Directory authentication for Azure Data Lake, you must perform hello following tasks.</span></span>

* <span data-ttu-id="d8a85-161">Créer un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="d8a85-161">Create a self-signed certificate</span></span>
* <span data-ttu-id="d8a85-162">Créer une application dans Azure Active Directory et un principal du service</span><span class="sxs-lookup"><span data-stu-id="d8a85-162">Create an application in Azure Active Directory and a Service Principal</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="d8a85-163">Créer un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="d8a85-163">Create a self-signed certificate</span></span>
<span data-ttu-id="d8a85-164">Assurez-vous que vous avez [Kit de développement logiciel Windows](https://dev.windows.com/en-us/downloads) installé avant de poursuivre la hello étapes de cette section.</span><span class="sxs-lookup"><span data-stu-id="d8a85-164">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="d8a85-165">Vous devez également créer un répertoire, tel que **C:\mycertdir**, où hello certificat sera créé.</span><span class="sxs-lookup"><span data-stu-id="d8a85-165">You must have also created a directory, such as **C:\mycertdir**, where hello certificate will be created.</span></span>

1. <span data-ttu-id="d8a85-166">À partir de la fenêtre Windows PowerShell de hello, accédez à emplacement toohello où vous avez installé le Kit de développement logiciel Windows (en général, `C:\Program Files (x86)\Windows Kits\10\bin\x86` et utiliser hello [MakeCert] [ makecert] utilitaire toocreate un certificat auto-signé et un clé privée.</span><span class="sxs-lookup"><span data-stu-id="d8a85-166">From hello PowerShell window, navigate toohello location where you installed Windows SDK (typically, `C:\Program Files (x86)\Windows Kits\10\bin\x86` and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="d8a85-167">Utilisez hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="d8a85-167">Use hello following commands.</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="d8a85-168">Vous serez invité à tooenter hello privée clé mot de passe.</span><span class="sxs-lookup"><span data-stu-id="d8a85-168">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="d8a85-169">Une fois la commande hello est correctement exécutée, vous devez voir un **CertFile.cer** et **mykey.pvk** dans le répertoire de certificat hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="d8a85-169">After hello command successfully executes, you should see a **CertFile.cer** and **mykey.pvk** in hello certificate directory you specified.</span></span>
2. <span data-ttu-id="d8a85-170">Hello d’utilisation [Pvk2Pfx] [ pvk2pfx] utilitaire tooconvert hello .pvk et .cer fichiers fichier .pfx créé tooa MakeCert.</span><span class="sxs-lookup"><span data-stu-id="d8a85-170">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="d8a85-171">Exécutez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="d8a85-171">Run hello following command.</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="d8a85-172">Lorsque vous y êtes invité Entrez le mot de passe clé privée hello vous avez spécifié précédemment.</span><span class="sxs-lookup"><span data-stu-id="d8a85-172">When prompted enter hello private key password you specified earlier.</span></span> <span data-ttu-id="d8a85-173">Hello valeur que vous spécifiez pour hello **- bon de commande** paramètre est un mot de passe hello qui est associé au fichier .pfx de hello.</span><span class="sxs-lookup"><span data-stu-id="d8a85-173">hello value you specify for hello **-po** parameter is hello password that is associated with hello .pfx file.</span></span> <span data-ttu-id="d8a85-174">Une fois la commande hello terminée avec succès, vous devez également voir un CertFile.pfx dans le répertoire de certificat hello spécifié.</span><span class="sxs-lookup"><span data-stu-id="d8a85-174">After hello command successfully completes, you should also see a CertFile.pfx in hello certificate directory you specified.</span></span>

### <a name="create-an-azure-active-directory-and-a-service-principal"></a><span data-ttu-id="d8a85-175">Créer une application Azure Active Directory et un principal du service</span><span class="sxs-lookup"><span data-stu-id="d8a85-175">Create an Azure Active Directory and a service principal</span></span>
<span data-ttu-id="d8a85-176">Dans cette section, vous effectuez hello étapes toocreate un principal de service pour une application Azure Active Directory, attribuer un principal de service de rôle toohello et s’authentifier en tant que principal du service hello en fournissant un certificat.</span><span class="sxs-lookup"><span data-stu-id="d8a85-176">In this section, you perform hello steps toocreate a service principal for an Azure Active Directory application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="d8a85-177">Exécutez hello suivant de commandes toocreate une application dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8a85-177">Run hello following commands toocreate an application in Azure Active Directory.</span></span>

1. <span data-ttu-id="d8a85-178">Collez hello suivant d’applets de commande dans la fenêtre de console PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="d8a85-178">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="d8a85-179">Vous spécifiez pour hello assurer qu’une valeur hello **- DisplayName** propriété est unique.</span><span class="sxs-lookup"><span data-stu-id="d8a85-179">Make sure hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="d8a85-180">Hello en outre, les valeurs pour **- page d’accueil** et **- IdentiferUris** sont des valeurs d’espace réservé et ne sont pas vérifiées.</span><span class="sxs-lookup"><span data-stu-id="d8a85-180">Also, hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

        $certificateFilePath = "$certificateFileDir\CertFile.pfx"

        $password = Read-Host –Prompt "Enter hello password" # This is hello password you specified for hello .pfx file

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
2. <span data-ttu-id="d8a85-181">Créer un principal de service à l’aide des ID d’application hello.</span><span class="sxs-lookup"><span data-stu-id="d8a85-181">Create a service principal using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="d8a85-182">Accordez le dossier Data Lake Store toohello hello service principal l’accès et fichier hello sera accessible à partir de cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="d8a85-182">Grant hello service principal access toohello Data Lake Store folder and hello file that you will access from hello HDInsight cluster.</span></span> <span data-ttu-id="d8a85-183">extrait de code Hello ci-dessous fournit racine toohello accès hello Data Lake Store (où vous avez copié le fichier de données d’exemple hello) de compte et hello fichier lui-même.</span><span class="sxs-lookup"><span data-stu-id="d8a85-183">hello snippet below provides access toohello root of hello Data Lake Store account (where you copied hello sample data file), and hello file itself.</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /vehicle1_09142014.csv -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-additional-storage"></a><span data-ttu-id="d8a85-184">Créer un cluster Linux HDInsight avec Data Lake Store comme stockage par supplémentaire</span><span class="sxs-lookup"><span data-stu-id="d8a85-184">Create an HDInsight Linux cluster with Data Lake Store as additional storage</span></span>

<span data-ttu-id="d8a85-185">Dans cette section, nous créons un cluster HDInsight Hadoop Linux avec Data Lake Store comme stockage supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="d8a85-185">In this section, we create an HDInsight Hadoop Linux cluster with Data Lake Store as additional storage.</span></span> <span data-ttu-id="d8a85-186">Pour cette version, le cluster HDInsight de hello et hello Data Lake Store doivent être Bonjour même emplacement.</span><span class="sxs-lookup"><span data-stu-id="d8a85-186">For this release, hello HDInsight cluster and hello Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="d8a85-187">Commencer la récupération hello ID client d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="d8a85-187">Start with retrieving hello subscription tenant ID.</span></span> <span data-ttu-id="d8a85-188">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="d8a85-188">You will need that later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId
2. <span data-ttu-id="d8a85-189">Pour cette version, pour un cluster Hadoop, Data Lake Store peut uniquement servir en tant qu’un stockage supplémentaire pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="d8a85-189">For this release, for a Hadoop cluster, Data Lake Store can only be used as an additional storage for hello cluster.</span></span> <span data-ttu-id="d8a85-190">stockage par défaut de Hello sera toujours les objets BLOB de stockage Azure hello (WASB).</span><span class="sxs-lookup"><span data-stu-id="d8a85-190">hello default storage will still be hello Azure storage blobs (WASB).</span></span> <span data-ttu-id="d8a85-191">Par conséquent, nous allons tout d’abord créer hello conteneurs du compte et le stockage de stockage requis pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="d8a85-191">So, we'll first create hello storage account and storage containers required for hello cluster.</span></span>

        # Create an Azure storage account
        $location = "East US 2"
        $storageAccountName = "<StorageAcccountName>"   # Provide a Storage account name

        New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -StorageAccountName $storageAccountName -Location $location -Type Standard_GRS

        # Create an Azure Blob Storage container
        $containerName = "<ContainerName>"              # Provide a container name
        $storageAccountKey = (Get-AzureRmStorageAccountKey -Name $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        New-AzureStorageContainer -Name $containerName -Context $destContext
3. <span data-ttu-id="d8a85-192">Créer un cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="d8a85-192">Create hello HDInsight cluster.</span></span> <span data-ttu-id="d8a85-193">Utilisez hello suivant d’applets de commande.</span><span class="sxs-lookup"><span data-stu-id="d8a85-193">Use hello following cmdlets.</span></span>

        # Set these variables
        $clusterName = $containerName                   # As a best practice, have hello same name for hello cluster and container
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster -ClusterName $clusterName -ResourceGroupName $resourceGroupName -HttpCredential $httpCredentials -Location $location -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" -DefaultStorageAccountKey $storageAccountKey -DefaultStorageContainer $containerName  -ClusterSizeInNodes $clusterNodes -ClusterType Hadoop -Version "3.4" -OSType Linux -SshCredential $sshCredentials -ObjectID $objectId -AadTenantId $tenantID -CertificateFilePath $certificateFilePath -CertificatePassword $password

    <span data-ttu-id="d8a85-194">Une fois que l’applet de commande hello terminée avec succès, vous devez voir une sortie d’affichage des détails du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d8a85-194">After hello cmdlet successfully completes, you should see an output listing hello cluster details.</span></span>


## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a><span data-ttu-id="d8a85-195">Exécuter les tâches de test sur Bonjour HDInsight cluster toouse Bonjour Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d8a85-195">Run test jobs on hello HDInsight cluster toouse hello Data Lake Store</span></span>
<span data-ttu-id="d8a85-196">Après avoir configuré un cluster HDInsight, vous pouvez exécuter les travaux test sur hello cluster tootest que hello HDInsight peut accéder à Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d8a85-196">After you have configured an HDInsight cluster, you can run test jobs on hello cluster tootest that hello HDInsight cluster can access Data Lake Store.</span></span> <span data-ttu-id="d8a85-197">toodo par conséquent, nous allons exécuter un travail Hive exemple qui crée une table à l’aide des données d’exemple hello que vous avez téléchargé antérieures tooyour Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d8a85-197">toodo so, we will run a sample Hive job that creates a table using hello sample data that you uploaded earlier tooyour Data Lake Store.</span></span>

<span data-ttu-id="d8a85-198">Dans cette section, vous allez SSH dans hello HDInsight Linux cluster que vous avez créé et exécuté hello un exemple de requête Hive.</span><span class="sxs-lookup"><span data-stu-id="d8a85-198">In this section you will SSH into hello HDInsight Linux cluster you created and run hello a sample Hive query.</span></span>

* <span data-ttu-id="d8a85-199">Si vous utilisez un tooSSH de client Windows dans un cluster de hello, consultez [utilisation de SSH avec basés sur Linux de Hadoop dans HDInsight à partir de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="d8a85-199">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="d8a85-200">Si vous utilisez un tooSSH de client Linux dans un cluster de hello, consultez [utilisation de SSH avec basés sur Linux de Hadoop dans HDInsight à partir de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="d8a85-200">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

1. <span data-ttu-id="d8a85-201">Une fois connecté, démarrer hello CLI de la ruche à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d8a85-201">Once connected, start hello Hive CLI by using hello following command:</span></span>

        hive
2. <span data-ttu-id="d8a85-202">À l’aide de hello CLI, entrez hello suivant les instructions toocreate une nouvelle table nommée **véhicules** à l’aide des données d’exemple hello Bonjour Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="d8a85-202">Using hello CLI, enter hello following statements toocreate a new table named **vehicles** by using hello sample data in hello Data Lake Store:</span></span>

        DROP TABLE vehicles;
        CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
        SELECT * FROM vehicles LIMIT 10;

    <span data-ttu-id="d8a85-203">Vous devez voir s’afficher une sortie similaire toohello :</span><span class="sxs-lookup"><span data-stu-id="d8a85-203">You should see an output similar toohello following:</span></span>

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

## <a name="access-data-lake-store-using-hdfs-commands"></a><span data-ttu-id="d8a85-204">Accéder à Data Lake Store avec les commandes HDFS</span><span class="sxs-lookup"><span data-stu-id="d8a85-204">Access Data Lake Store using HDFS commands</span></span>
<span data-ttu-id="d8a85-205">Une fois que vous avez configuré le cluster HDInsight de hello toouse Data Lake Store, vous pouvez utiliser hello HDFS shell commandes tooaccess hello magasin.</span><span class="sxs-lookup"><span data-stu-id="d8a85-205">Once you have configured hello HDInsight cluster toouse Data Lake Store, you can use hello HDFS shell commands tooaccess hello store.</span></span>

<span data-ttu-id="d8a85-206">Dans cette section, vous allez SSH dans hello HDInsight Linux cluster que vous avez créé et exécuter des commandes HDFS hello.</span><span class="sxs-lookup"><span data-stu-id="d8a85-206">In this section you will SSH into hello HDInsight Linux cluster you created and run hello HDFS commands.</span></span>

* <span data-ttu-id="d8a85-207">Si vous utilisez un tooSSH de client Windows dans un cluster de hello, consultez [utilisation de SSH avec basés sur Linux de Hadoop dans HDInsight à partir de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="d8a85-207">If you are using a Windows client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="d8a85-208">Si vous utilisez un tooSSH de client Linux dans un cluster de hello, consultez [utilisation de SSH avec basés sur Linux de Hadoop dans HDInsight à partir de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="d8a85-208">If you are using a Linux client tooSSH into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

<span data-ttu-id="d8a85-209">Une fois connecté, utilisez hello suivant fichiers HDFS filesystem commande toolist hello Bonjour Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d8a85-209">Once connected, use hello following HDFS filesystem command toolist hello files in hello Data Lake Store.</span></span>

    hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/

<span data-ttu-id="d8a85-210">Elle doit répertorier fichier hello que vous avez téléchargé antérieures toohello Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d8a85-210">This should list hello file that you uploaded earlier toohello Data Lake Store.</span></span>

    15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
    Found 1 items
    -rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder

<span data-ttu-id="d8a85-211">Vous pouvez également utiliser hello `hdfs dfs -put` commande tooupload certains toohello fichiers Data Lake Store, puis utilisez `hdfs dfs -ls` tooverify indique si les fichiers de hello ont été téléchargés avec succès.</span><span class="sxs-lookup"><span data-stu-id="d8a85-211">You can also use hello `hdfs dfs -put` command tooupload some files toohello Data Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="d8a85-212">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d8a85-212">See Also</span></span>
* [<span data-ttu-id="d8a85-213">Portail : Créer un toouse du cluster HDInsight Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d8a85-213">Portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
