---
title: "aaaCreate HDInsight clusters avec Data Lake Store en tant que de stockage par défaut à l’aide de PowerShell | Des documents Microsoft"
description: Utiliser Azure PowerShell toocreate et utiliser des clusters HDInsight avec Azure Data Lake Store
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8917af15-8e37-46cf-87ad-4e6d5d67ecdb
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/08/2017
ms.author: nitinme
ms.openlocfilehash: a5c0ad416da6ad9bd07204af2ebb6b7470916085
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a><span data-ttu-id="3e7e8-103">Créer des clusters HDInsight avec Data Lake Store comme stockage par défaut à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="3e7e8-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3e7e8-104">Utilisez hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="3e7e8-104">Use hello Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="3e7e8-105">Utiliser PowerShell (pour le stockage par défaut)</span><span class="sxs-lookup"><span data-stu-id="3e7e8-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="3e7e8-106">Utiliser PowerShell (pour le stockage supplémentaire)</span><span class="sxs-lookup"><span data-stu-id="3e7e8-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="3e7e8-107">Utiliser Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3e7e8-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

<span data-ttu-id="3e7e8-108">Découvrez comment toouse Azure PowerShell tooconfigure Azure HDInsight clusters avec Azure Data Lake Store en tant que stockage de la valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-108">Learn how toouse Azure PowerShell tooconfigure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span></span> <span data-ttu-id="3e7e8-109">Pour obtenir des instructions sur la création d’un cluster HDInsight avec Data Lake Store comme stockage supplémentaire, consultez [Créer un cluster HDInsight avec Data Lake Store en tant que stockage supplémentaire](data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3e7e8-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

<span data-ttu-id="3e7e8-110">Voici quelques considérations importantes pour l’utilisation de HDInsight avec Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="3e7e8-110">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="3e7e8-111">clusters de HDInsight Hello option toocreate avec un accès tooData Lake Store en tant que stockage de la valeur par défaut est disponible pour HDInsight version 3.5 et 3.6.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-111">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="3e7e8-112">toocreate d’option Hello des clusters HDInsight avec accès tooData Lake Store car le stockage de la valeur par défaut est *non disponible* pour les clusters HDInsight Premium.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-112">hello option toocreate HDInsight clusters with access tooData Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

<span data-ttu-id="3e7e8-113">tooconfigure toowork de HDInsight avec Data Lake Store à l’aide de PowerShell, suivez les instructions de hello dans les cinq sections hello.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-113">tooconfigure HDInsight toowork with Data Lake Store by using PowerShell, follow hello instructions in hello next five sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e7e8-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3e7e8-114">Prerequisites</span></span>
<span data-ttu-id="3e7e8-115">Avant de commencer ce didacticiel, assurez-vous que vous remplissez hello suivant les exigences :</span><span class="sxs-lookup"><span data-stu-id="3e7e8-115">Before you begin this tutorial, make sure that you meet hello following requirements:</span></span>

* <span data-ttu-id="3e7e8-116">**Un abonnement Azure**: accédez trop[version d’évaluation gratuite de Azure d’obtenir](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3e7e8-116">**An Azure subscription**: Go too[Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3e7e8-117">**Azure PowerShell 1.0 ou supérieur**: consultez [comment tooinstall et configurez PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3e7e8-117">**Azure PowerShell 1.0 or greater**: See [How tooinstall and configure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="3e7e8-118">**Kit de développement logiciel (SDK) Windows**: tooinstall Kit de développement logiciel Windows, accédez trop[téléchargements et outils pour Windows 10](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="3e7e8-118">**Windows Software Development Kit (SDK)**: tooinstall Windows SDK, go too[Downloads and tools for Windows 10](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="3e7e8-119">Hello SDK est toocreate utilisé un certificat de sécurité.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-119">hello SDK is used toocreate a security certificate.</span></span>
* <span data-ttu-id="3e7e8-120">**Principal du service Azure Active Directory**: ce didacticiel explique comment toocreate un principal de service dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3e7e8-120">**Azure Active Directory service principal**: This tutorial describes how toocreate a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="3e7e8-121">Toutefois, de le toocreate un principal de service, vous devez être un administrateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-121">However, toocreate a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="3e7e8-122">Si vous êtes un administrateur, vous pouvez ignorer cette condition préalable et poursuivre le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-122">If you are an administrator, you can skip this prerequisite and proceed with hello tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="3e7e8-123">Vous pouvez créer un principal de service uniquement si vous être administrateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-123">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="3e7e8-124">Votre administrateur Azure AD doit créer un principal de service. Vous pouvez ensuite créer un cluster HDInsight avec Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-124">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="3e7e8-125">Hello principal de service doit être créé avec un certificat, comme décrit dans [créer un principal de service avec certificat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="3e7e8-125">hello service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>
    >

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="3e7e8-126">Créer un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3e7e8-126">Create a Data Lake Store account</span></span>
<span data-ttu-id="3e7e8-127">toocreate un compte Data Lake Store, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="3e7e8-127">toocreate a Data Lake Store account, do hello following:</span></span>

1. <span data-ttu-id="3e7e8-128">À partir de votre bureau, ouvrez une fenêtre PowerShell, puis entrez des extraits de code hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-128">From your desktop, open a PowerShell window, and then enter hello snippets below.</span></span> <span data-ttu-id="3e7e8-129">Lorsque vous avez demandée toosign dans, connectez-vous en tant qu’un des administrateurs d’abonnements hello ou propriétaires.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-129">When you are prompted toosign in, sign in as one of hello subscription administrators or owners.</span></span> 

        # Sign in tooyour Azure account
        Login-AzureRmAccount

        # List all hello subscriptions associated tooyour account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > <span data-ttu-id="3e7e8-130">Si vous inscrivez le fournisseur de ressources Data Lake Store hello et que vous recevez un message d’erreur similaire trop`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, votre abonnement est peut-être pas dans la liste approuvée pour Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-130">If you register hello Data Lake Store resource provider and receive an error similar too`Register-AzureRmResourceProvider : InvalidResourceNamespace: hello resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store.</span></span> <span data-ttu-id="3e7e8-131">tooenable votre abonnement Azure pour hello Data Lake Store public preview, suivez les instructions de hello dans [prise en main Azure Data Lake Store à l’aide de hello Azure portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3e7e8-131">tooenable your Azure subscription for hello Data Lake Store public preview, follow hello instructions in [Get started with Azure Data Lake Store by using hello Azure portal](data-lake-store-get-started-portal.md).</span></span>
    >

2. <span data-ttu-id="3e7e8-132">Un compte Data Lake Store est associé à un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-132">A Data Lake Store account is associated with an Azure resource group.</span></span> <span data-ttu-id="3e7e8-133">Commencez par créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-133">Start by creating a resource group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="3e7e8-134">Vous devriez obtenir un résultat similaire à ceci :</span><span class="sxs-lookup"><span data-stu-id="3e7e8-134">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="3e7e8-135">Créez un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-135">Create a Data Lake Store account.</span></span> <span data-ttu-id="3e7e8-136">compte Hello nom que vous spécifiez doit contenir uniquement des lettres minuscules et chiffres.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-136">hello account name you specify must contain only lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="3e7e8-137">Vous devez voir une sortie semblable à hello suivante :</span><span class="sxs-lookup"><span data-stu-id="3e7e8-137">You should see an output like hello following:</span></span>

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

4. <span data-ttu-id="3e7e8-138">À l’aide de Data Lake Store en tant que stockage par défaut nécessite toospecify qu'un fichiers spécifiques à un cluster hello de toowhich de chemin d’accès racine sont copiés au cours de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-138">Using Data Lake Store as default storage requires you toospecify a root path toowhich hello cluster-specific files are copied during cluster creation.</span></span> <span data-ttu-id="3e7e8-139">toocreate un chemin d’accès racine, qui est **hdiadlcluster/clusters** dans l’extrait de code hello, utilisez hello suivant d’applets de commande :</span><span class="sxs-lookup"><span data-stu-id="3e7e8-139">toocreate a root path, which is **/clusters/hdiadlcluster** in hello  snippet, use hello following cmdlets:</span></span>

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-toodata-lake-store"></a><span data-ttu-id="3e7e8-140">Configurer l’authentification dans en fonction du rôle d’accès tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="3e7e8-140">Set up authentication for role-based access tooData Lake Store</span></span>
<span data-ttu-id="3e7e8-141">Chaque abonnement Azure est associé à une entité Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-141">Every Azure subscription is associated with an Azure AD entity.</span></span> <span data-ttu-id="3e7e8-142">Les utilisateurs et les services que les accès aux ressources de l’abonnement à l’aide de hello portail Azure ou hello API Azure Resource Manager doivent tout d’abord s’authentifier auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-142">Users and services that access subscription resources by using hello Azure portal or hello Azure Resource Manager API must first authenticate with Azure AD.</span></span> <span data-ttu-id="3e7e8-143">L’accès est accordé tooAzure abonnements et services en leur attribuant le rôle approprié de hello sur une ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-143">Access is granted tooAzure subscriptions and services by assigning them hello appropriate role on an Azure resource.</span></span> <span data-ttu-id="3e7e8-144">Pour les services, un principal du service identifie le service de hello dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-144">For services, a service principal identifies hello service in Azure AD.</span></span>

<span data-ttu-id="3e7e8-145">Cette section illustre comment toogrant une application de service, telles que HDInsight, tooan d’accès aux ressources Azure (hello compte Data Lake Store que vous avez créé précédemment).</span><span class="sxs-lookup"><span data-stu-id="3e7e8-145">This section illustrates how toogrant an application service, such as HDInsight, access tooan Azure resource (hello Data Lake Store account that you created earlier).</span></span> <span data-ttu-id="3e7e8-146">Pour faire en créant un service principal pour l’application hello et en assignant des tooit rôles via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-146">You do so by creating a service principal for hello application and assigning roles tooit via PowerShell.</span></span>

<span data-ttu-id="3e7e8-147">tooset l’authentification Active Directory pour Azure Data Lake, effectuer hello hello les deux sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-147">tooset up Active Directory authentication for Azure Data Lake, perform hello tasks in hello following two sections.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="3e7e8-148">Créer un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="3e7e8-148">Create a self-signed certificate</span></span>
<span data-ttu-id="3e7e8-149">Assurez-vous que vous avez [Kit de développement logiciel Windows](https://dev.windows.com/en-us/downloads) installé avant de poursuivre la hello étapes de cette section.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with hello steps in this section.</span></span> <span data-ttu-id="3e7e8-150">Vous devez également créer un répertoire, tel que *C:\mycertdir*, où vous créez le certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-150">You must have also created a directory, such as *C:\mycertdir*, where you create hello certificate.</span></span>

1. <span data-ttu-id="3e7e8-151">À partir de la fenêtre de PowerShell hello, accédez à emplacement toohello où vous avez installé le Kit de développement logiciel Windows (en général, *C:\Program Files (x86) \Windows Kits\10\bin\x86*) et utiliser hello [MakeCert] [ makecert] utilitaire toocreate un certificat auto-signé et une clé privée.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-151">From hello PowerShell window, go toohello location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use hello [MakeCert][makecert] utility toocreate a self-signed certificate and a private key.</span></span> <span data-ttu-id="3e7e8-152">Utilisez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="3e7e8-152">Use hello following commands:</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="3e7e8-153">Vous serez invité à tooenter hello privée clé mot de passe.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-153">You will be prompted tooenter hello private key password.</span></span> <span data-ttu-id="3e7e8-154">Une fois la commande hello est exécuté avec succès, vous devez voir **CertFile.cer** et **mykey.pvk** dans le répertoire de certificats hello que vous avez spécifié.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-154">After hello command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in hello certificate directory that you specified.</span></span>
2. <span data-ttu-id="3e7e8-155">Hello d’utilisation [Pvk2Pfx] [ pvk2pfx] utilitaire tooconvert hello .pvk et .cer fichiers fichier .pfx créé tooa MakeCert.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-155">Use hello [Pvk2Pfx][pvk2pfx] utility tooconvert hello .pvk and .cer files that MakeCert created tooa .pfx file.</span></span> <span data-ttu-id="3e7e8-156">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3e7e8-156">Run hello following command:</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="3e7e8-157">Lorsque vous êtes invité, entrez hello privée clé mot de passe que vous avez spécifié précédemment.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-157">When you are prompted, enter hello private key password that you specified earlier.</span></span> <span data-ttu-id="3e7e8-158">Hello valeur que vous spécifiez pour hello **- bon de commande** paramètre est un mot de passe hello a associé à un fichier .pfx de hello.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-158">hello value you specify for hello **-po** parameter is hello password that's associated with hello .pfx file.</span></span> <span data-ttu-id="3e7e8-159">Une fois la commande hello est terminée avec succès, vous devez également voir un **CertFile.pfx** dans le répertoire de certificats hello que vous avez spécifié.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-159">After hello command has been completed successfully, you should also see a **CertFile.pfx** in hello certificate directory that you specified.</span></span>

### <a name="create-an-azure-ad-and-a-service-principal"></a><span data-ttu-id="3e7e8-160">Créer une application Azure AD et un principal de service</span><span class="sxs-lookup"><span data-stu-id="3e7e8-160">Create an Azure AD and a service principal</span></span>
<span data-ttu-id="3e7e8-161">Dans cette section, vous créez un principal de service pour une application Azure AD, attribuer un principal de service de rôle toohello et authentifiez-vous en tant que principal du service hello en fournissant un certificat.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-161">In this section, you create a service principal for an Azure AD application, assign a role toohello service principal, and authenticate as hello service principal by providing a certificate.</span></span> <span data-ttu-id="3e7e8-162">toocreate une application dans Azure AD, exécutez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="3e7e8-162">toocreate an application in Azure AD, run hello following commands:</span></span>

1. <span data-ttu-id="3e7e8-163">Collez hello suivant d’applets de commande dans la fenêtre de console PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-163">Paste hello following cmdlets in hello PowerShell console window.</span></span> <span data-ttu-id="3e7e8-164">Assurez-vous que cette valeur hello que vous spécifiez pour hello **- DisplayName** propriété est unique.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-164">Make sure that hello value you specify for hello **-DisplayName** property is unique.</span></span> <span data-ttu-id="3e7e8-165">Hello pour les valeurs **- page d’accueil** et **- IdentiferUris** sont des valeurs d’espace réservé et ne sont pas vérifiées.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-165">hello values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

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
2. <span data-ttu-id="3e7e8-166">Créez un principal de service à l’aide de l’ID application hello.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-166">Create a service principal by using hello application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="3e7e8-167">Accordez le racine Data Lake Store toohello hello service accès principal et tous les dossiers hello dans le chemin d’accès racine hello que vous avez spécifié précédemment.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-167">Grant hello service principal access toohello Data Lake Store root and all hello folders in hello root path that you specified earlier.</span></span> <span data-ttu-id="3e7e8-168">Utilisez hello suivant d’applets de commande :</span><span class="sxs-lookup"><span data-stu-id="3e7e8-168">Use hello following cmdlets:</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-hello-default-storage"></a><span data-ttu-id="3e7e8-169">Créer un cluster HDInsight Linux avec Data Lake Store en tant que stockage par défaut de hello</span><span class="sxs-lookup"><span data-stu-id="3e7e8-169">Create an HDInsight Linux cluster with Data Lake Store as hello default storage</span></span>

<span data-ttu-id="3e7e8-170">Dans cette section, vous créez un cluster HDInsight Hadoop Linux avec Data Lake Store comme stockage par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as hello default storage.</span></span> <span data-ttu-id="3e7e8-171">Pour cette version, hello cluster HDInsight et Data Lake Store doit être Bonjour même emplacement.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-171">For this release, hello HDInsight cluster and Data Lake Store must be in hello same location.</span></span>

1. <span data-ttu-id="3e7e8-172">Extraire l’ID de client d’abonnement hello et stockez-le toouse plus tard.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-172">Retrieve hello subscription tenant ID, and store it toouse later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. <span data-ttu-id="3e7e8-173">Créer le cluster HDInsight de hello à l’aide de hello suivant d’applets de commande :</span><span class="sxs-lookup"><span data-stu-id="3e7e8-173">Create hello HDInsight cluster by using hello following cmdlets:</span></span>

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # hello number of nodes in hello HDInsight cluster
        $httpCredentials = Get-Credential
        $sshCredentials = Get-Credential

        New-AzureRmHDInsightCluster `
               -ClusterType Hadoop `
               -OSType Linux `
               -ClusterSizeInNodes $clusterNodes `
               -ResourceGroupName $resourceGroupName `
               -ClusterName $clusterName `
               -HttpCredential $httpCredentials `
               -Location $location `
               -DefaultStorageAccountType AzureDataLakeStore `
               -DefaultStorageAccountName "$storageAccountName.azuredatalakestore.net" `
               -DefaultStorageRootPath $storageRootPath `
               -Version "3.6" `
               -SshCredential $sshCredentials `
               -AadTenantId $tenantId `
               -ObjectId $objectId `
               -CertificateFilePath $certificateFilePath `
               -CertificatePassword $password

    <span data-ttu-id="3e7e8-174">Une fois que l’applet de commande hello est terminée, vous devez voir une sortie qui répertorie les détails du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-174">After hello cmdlet has been successfully completed, you should see an output that lists hello cluster details.</span></span>

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-data-lake-store"></a><span data-ttu-id="3e7e8-175">Exécuter les tâches de test sur hello HDInsight cluster toouse Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3e7e8-175">Run test jobs on hello HDInsight cluster toouse Data Lake Store</span></span>
<span data-ttu-id="3e7e8-176">Après avoir configuré un cluster HDInsight, vous pouvez exécuter les travaux test dessus tooensure qu’il peut accéder à Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-176">After you have configured an HDInsight cluster, you can run test jobs on it tooensure that it can access Data Lake Store.</span></span> <span data-ttu-id="3e7e8-177">toodo donc exécuter un toocreate de travail Hive exemple une table qui utilise les données d’exemple hello qui sont déjà disponibles dans Data Lake Store à  *<cluster root>/example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-177">toodo so, run a sample Hive job toocreate a table that uses hello sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span></span>

<span data-ttu-id="3e7e8-178">Dans cette section, vous établissez une connexion Secure Shell (SSH) dans hello cluster HDInsight Linux que vous avez créé, puis vous exécutez un exemple de requête Hive.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-178">In this section, you make a Secure Shell (SSH) connection into hello HDInsight Linux cluster that you created, and then you run a sample Hive query.</span></span>

* <span data-ttu-id="3e7e8-179">Si vous utilisez un toomake de client Windows à une connexion SSH en cluster de hello, consultez [utilisation de SSH avec basés sur Linux de Hadoop dans HDInsight à partir de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="3e7e8-179">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="3e7e8-180">Si vous utilisez un toomake de client à une connexion SSH en cluster de hello Linux, consultez [utilisation de SSH avec basés sur Linux de Hadoop dans HDInsight à partir de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3e7e8-180">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="3e7e8-181">Une fois que vous avez effectué la connexion de hello, démarrer une interface de ligne hello Hive (CLI) à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3e7e8-181">After you have made hello connection, start hello Hive command-line interface (CLI) by using hello following command:</span></span>

        hive
2. <span data-ttu-id="3e7e8-182">Utilisez Bonjour CLI tooenter Bonjour suivant les instructions toocreate une nouvelle table nommée **véhicules** à l’aide des données d’exemple hello dans Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="3e7e8-182">Use hello CLI tooenter hello following statements toocreate a new table named **vehicles** by using hello sample data in Data Lake Store:</span></span>

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="3e7e8-183">Vous devez voir le résultat de la requête hello sur la console SSH hello.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-183">You should see hello query output on hello SSH console.</span></span>

    >[!NOTE]
    ><span data-ttu-id="3e7e8-184">Bonjour chemin d’accès toohello échantillon de données hello précédant la commande CREATE TABLE est `adl:///example/data/`, où `adl:///` est hello cluster racine.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-184">hello path toohello sample data in hello preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is hello cluster root.</span></span> <span data-ttu-id="3e7e8-185">Exemple hello de la racine du cluster hello qui est spécifiée dans ce didacticiel, commande hello est `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-185">Following hello example of hello cluster root that's specified in this tutorial, hello command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span></span> <span data-ttu-id="3e7e8-186">Vous pouvez utiliser d’alternative plus courte hello ou fournir la racine du cluster toohello hello chemin d’accès complet.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-186">You can either use hello shorter alternative or provide hello complete path toohello cluster root.</span></span>
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a><span data-ttu-id="3e7e8-187">Accéder à Data Lake Store avec les commandes HDFS</span><span class="sxs-lookup"><span data-stu-id="3e7e8-187">Access Data Lake Store by using HDFS commands</span></span>
<span data-ttu-id="3e7e8-188">Une fois que vous avez configuré le cluster HDInsight de hello toouse Data Lake Store, vous pouvez utiliser le système de fichiers distribués Hadoop (HDFS) shell commandes tooaccess hello magasin.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-188">After you have configured hello HDInsight cluster toouse Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands tooaccess hello store.</span></span>

<span data-ttu-id="3e7e8-189">Dans cette section, vous effectuez une connexion SSH en hello cluster HDInsight Linux que vous avez créé, puis vous exécutez les commandes HDFS hello.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-189">In this section, you make an SSH connection into hello HDInsight Linux cluster that you created, and then you run hello HDFS commands.</span></span>

* <span data-ttu-id="3e7e8-190">Si vous utilisez un toomake de client Windows à une connexion SSH en cluster de hello, consultez [utilisation de SSH avec basés sur Linux de Hadoop dans HDInsight à partir de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="3e7e8-190">If you are using a Windows client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="3e7e8-191">Si vous utilisez un toomake de client à une connexion SSH en cluster de hello Linux, consultez [utilisation de SSH avec basés sur Linux de Hadoop dans HDInsight à partir de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3e7e8-191">If you are using a Linux client toomake an SSH connection into hello cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="3e7e8-192">Une fois que vous avez effectué la connexion de hello, répertorient les fichiers de hello dans Data Lake Store à l’aide de hello suivant de commande de système de fichiers HDFS.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-192">After you've made hello connection, list hello files in Data Lake Store by using hello following HDFS file system command.</span></span>

    hdfs dfs -ls adl:///

<span data-ttu-id="3e7e8-193">Vous pouvez également utiliser hello `hdfs dfs -put` commande tooupload certains fichiers tooData Lake Store, puis utilisez `hdfs dfs -ls` tooverify indique si les fichiers de hello ont été téléchargés avec succès.</span><span class="sxs-lookup"><span data-stu-id="3e7e8-193">You can also use hello `hdfs dfs -put` command tooupload some files tooData Lake Store, and then use `hdfs dfs -ls` tooverify whether hello files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="3e7e8-194">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3e7e8-194">See also</span></span>
* [<span data-ttu-id="3e7e8-195">Portail Azure : créer un toouse du cluster HDInsight Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3e7e8-195">Azure portal: Create an HDInsight cluster toouse Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
