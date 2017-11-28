---
title: "Créer des clusters HDInsight avec Data Lake Store comme stockage par défaut à l’aide de PowerShell | Microsoft Docs"
description: "Utiliser Azure PowerShell pour créer et utiliser les clusters HDInsight avec Azure Data Lake Store"
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
ms.openlocfilehash: 77eb83b80312eca401e6f60d57ed6a5668ea442e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-as-default-storage-by-using-powershell"></a><span data-ttu-id="f81b1-103">Créer des clusters HDInsight avec Data Lake Store comme stockage par défaut à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="f81b1-103">Create HDInsight clusters with Data Lake Store as default storage by using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f81b1-104">Utiliser le portail Azure</span><span class="sxs-lookup"><span data-stu-id="f81b1-104">Use the Azure portal</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [<span data-ttu-id="f81b1-105">Utiliser PowerShell (pour le stockage par défaut)</span><span class="sxs-lookup"><span data-stu-id="f81b1-105">Use PowerShell (for default storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [<span data-ttu-id="f81b1-106">Utiliser PowerShell (pour le stockage supplémentaire)</span><span class="sxs-lookup"><span data-stu-id="f81b1-106">Use PowerShell (for additional storage)</span></span>](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [<span data-ttu-id="f81b1-107">Utiliser Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f81b1-107">Use Resource Manager</span></span>](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

<span data-ttu-id="f81b1-108">Apprenez à utiliser Azure PowerShell pour configurer un cluster Azure HDInsight avec Azure Data Lake Store comme stockage par défaut.</span><span class="sxs-lookup"><span data-stu-id="f81b1-108">Learn how to use Azure PowerShell to configure Azure HDInsight clusters with Azure Data Lake Store, as default storage.</span></span> <span data-ttu-id="f81b1-109">Pour obtenir des instructions sur la création d’un cluster HDInsight avec Data Lake Store comme stockage supplémentaire, consultez [Créer un cluster HDInsight avec Data Lake Store en tant que stockage supplémentaire](data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f81b1-109">For instructions on creating an HDInsight cluster with Data Lake Store as additional storage, see [Create an HDInsight cluster with Data Lake Store as additional storage](data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

<span data-ttu-id="f81b1-110">Voici quelques considérations importantes pour l’utilisation de HDInsight avec Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="f81b1-110">Here are some important considerations for using HDInsight with Data Lake Store:</span></span>

* <span data-ttu-id="f81b1-111">L’option permettant de créer des clusters HDInsight avec accès à Data Lake Store comme stockage par défaut est disponible si vous utilisez HDInsight versions 3.5 et 3.6.</span><span class="sxs-lookup"><span data-stu-id="f81b1-111">The option to create HDInsight clusters with access to Data Lake Store as default storage is available for HDInsight version 3.5 and 3.6.</span></span>

* <span data-ttu-id="f81b1-112">L’option permettant de créer des clusters HDInsight avec accès à Data Lake Store comme stockage par défaut n’est *pas disponible* pour les clusters HDInsight Premium.</span><span class="sxs-lookup"><span data-stu-id="f81b1-112">The option to create HDInsight clusters with access to Data Lake Store as default storage is *not available* for HDInsight Premium clusters.</span></span>

<span data-ttu-id="f81b1-113">Pour configurer HDInsight de façon à fonctionner avec Data Lake Store à l’aide de PowerShell, suivez les instructions des cinq prochaines sections.</span><span class="sxs-lookup"><span data-stu-id="f81b1-113">To configure HDInsight to work with Data Lake Store by using PowerShell, follow the instructions in the next five sections.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f81b1-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f81b1-114">Prerequisites</span></span>
<span data-ttu-id="f81b1-115">Avant de commencer le didacticiel, veillez à ce que vos mots de passe répondent aux exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="f81b1-115">Before you begin this tutorial, make sure that you meet the following requirements:</span></span>

* <span data-ttu-id="f81b1-116">**Un abonnement Azure** : consultez la page [Obtention d’un essai gratuit Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f81b1-116">**An Azure subscription**: Go to [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f81b1-117">**Azure PowerShell 1.0 ou version ultérieure** : consultez [Installation et configuration de PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f81b1-117">**Azure PowerShell 1.0 or greater**: See [How to install and configure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="f81b1-118">**Kit de développement logiciel (SDK) Windows** : pour l’installer, consultez [Téléchargements et outils pour Windows 10](https://dev.windows.com/en-us/downloads).</span><span class="sxs-lookup"><span data-stu-id="f81b1-118">**Windows Software Development Kit (SDK)**: To install Windows SDK, go to [Downloads and tools for Windows 10](https://dev.windows.com/en-us/downloads).</span></span> <span data-ttu-id="f81b1-119">Le Kit de développement logiciel (SDK) vous permet de créer un certificat de sécurité.</span><span class="sxs-lookup"><span data-stu-id="f81b1-119">The SDK is used to create a security certificate.</span></span>
* <span data-ttu-id="f81b1-120">**Principal de service Active Directory Azure** : ce didacticiel explique comment créer un principal de service dans Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f81b1-120">**Azure Active Directory service principal**: This tutorial describes how to create a service principal in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="f81b1-121">Toutefois, vous devez être administrateur Azure AD pour pouvoir créer un principal du service.</span><span class="sxs-lookup"><span data-stu-id="f81b1-121">However, to create a service principal, you must be an Azure AD administrator.</span></span> <span data-ttu-id="f81b1-122">Si vous êtes administrateur, vous pouvez ignorer ce prérequis et poursuivre le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f81b1-122">If you are an administrator, you can skip this prerequisite and proceed with the tutorial.</span></span>

    >[!NOTE]
    ><span data-ttu-id="f81b1-123">Vous pouvez créer un principal de service uniquement si vous être administrateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f81b1-123">You can create a service principal only if you are an Azure AD administrator.</span></span> <span data-ttu-id="f81b1-124">Votre administrateur Azure AD doit créer un principal de service. Vous pouvez ensuite créer un cluster HDInsight avec Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f81b1-124">Your Azure AD administrator must create a service principal before you can create an HDInsight cluster with Data Lake Store.</span></span> <span data-ttu-id="f81b1-125">Le principal de service doit être créé à l’aide d’un certificat, comme décrit dans [Créer un principal de service avec certificat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span><span class="sxs-lookup"><span data-stu-id="f81b1-125">The service principal must be created with a certificate, as described in [Create a service principal with certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).</span></span>
    >

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="f81b1-126">Créer un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f81b1-126">Create a Data Lake Store account</span></span>
<span data-ttu-id="f81b1-127">Pour créer un compte Data Lake Store, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f81b1-127">To create a Data Lake Store account, do the following:</span></span>

1. <span data-ttu-id="f81b1-128">Sur votre bureau, ouvrez une fenêtre PowerShell et entrez l’extrait de code ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f81b1-128">From your desktop, open a PowerShell window, and then enter the snippets below.</span></span> <span data-ttu-id="f81b1-129">Lorsque vous êtes invité à vous connecter, connectez-vous en tant qu’administrateur ou propriétaire de l’abonnement.</span><span class="sxs-lookup"><span data-stu-id="f81b1-129">When you are prompted to sign in, sign in as one of the subscription administrators or owners.</span></span> 

        # Sign in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"

    > [!NOTE]
    > <span data-ttu-id="f81b1-130">Si vous recevez une erreur similaire à `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid` pendant l’inscription du fournisseur de ressources Data Lake Store, il est possible que votre abonnement ne figure pas dans la liste approuvée pour Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f81b1-130">If you register the Data Lake Store resource provider and receive an error similar to `Register-AzureRmResourceProvider : InvalidResourceNamespace: The resource namespace 'Microsoft.DataLakeStore' is invalid`, your subscription might not be whitelisted for Data Lake Store.</span></span> <span data-ttu-id="f81b1-131">Pour activer votre abonnement Azure pour la préversion publique Data Lake Store, suivez les instructions à la page [Prise en main d’Azure Data Lake Store avec le portail Azure](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f81b1-131">To enable your Azure subscription for the Data Lake Store public preview, follow the instructions in [Get started with Azure Data Lake Store by using the Azure portal](data-lake-store-get-started-portal.md).</span></span>
    >

2. <span data-ttu-id="f81b1-132">Un compte Data Lake Store est associé à un groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="f81b1-132">A Data Lake Store account is associated with an Azure resource group.</span></span> <span data-ttu-id="f81b1-133">Commencez par créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f81b1-133">Start by creating a resource group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="f81b1-134">Vous devriez obtenir un résultat similaire à ceci :</span><span class="sxs-lookup"><span data-stu-id="f81b1-134">You should see an output like this:</span></span>

        ResourceGroupName : hdiadlgrp
        Location          : eastus2
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/<subscription-id>/resourceGroups/hdiadlgrp

3. <span data-ttu-id="f81b1-135">Créez un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f81b1-135">Create a Data Lake Store account.</span></span> <span data-ttu-id="f81b1-136">Le nom de compte que vous spécifiez doit contenir uniquement des lettres minuscules et des chiffres.</span><span class="sxs-lookup"><span data-stu-id="f81b1-136">The account name you specify must contain only lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="f81b1-137">Un résultat similaire à ce qui suit s’affiche normalement :</span><span class="sxs-lookup"><span data-stu-id="f81b1-137">You should see an output like the following:</span></span>

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

4. <span data-ttu-id="f81b1-138">L’utilisation de Data Lake Store en tant que stockage par défaut vous oblige à spécifier un chemin d’accès racine où les fichiers spécifiques au cluster sont copiés lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="f81b1-138">Using Data Lake Store as default storage requires you to specify a root path to which the cluster-specific files are copied during cluster creation.</span></span> <span data-ttu-id="f81b1-139">Pour créer un chemin d’accès racine, qui, dans l’extrait de code ci-dessous est **hdiadlcluster/clusters/**, utilisez les applets de commande ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f81b1-139">To create a root path, which is **/clusters/hdiadlcluster** in the  snippet, use the following cmdlets:</span></span>

        $myrootdir = "/"
        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/clusters/hdiadlcluster


## <a name="set-up-authentication-for-role-based-access-to-data-lake-store"></a><span data-ttu-id="f81b1-140">Configurer l'authentification pour définir un accès à Data Lake Store en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="f81b1-140">Set up authentication for role-based access to Data Lake Store</span></span>
<span data-ttu-id="f81b1-141">Chaque abonnement Azure est associé à une entité Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f81b1-141">Every Azure subscription is associated with an Azure AD entity.</span></span> <span data-ttu-id="f81b1-142">Les utilisateurs et services qui accèdent aux ressources par le biais du portail Azure ou de l’API Azure Resource Manager doivent au préalable s’authentifier auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f81b1-142">Users and services that access subscription resources by using the Azure portal or the Azure Resource Manager API must first authenticate with Azure AD.</span></span> <span data-ttu-id="f81b1-143">L’accès est accordé aux abonnements et services Azure en leur affectant le rôle approprié sur une ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="f81b1-143">Access is granted to Azure subscriptions and services by assigning them the appropriate role on an Azure resource.</span></span> <span data-ttu-id="f81b1-144">Pour les services, un principal de service identifie le service dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f81b1-144">For services, a service principal identifies the service in Azure AD.</span></span>

<span data-ttu-id="f81b1-145">Cette section montre comment accorder l'accès à une ressource Azure (le compte Azure Data Lake Store créé précédemment) à un service d’application, comme HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f81b1-145">This section illustrates how to grant an application service, such as HDInsight, access to an Azure resource (the Data Lake Store account that you created earlier).</span></span> <span data-ttu-id="f81b1-146">Pour ce faire, créez un principal de service pour l’application, puis attribuez-lui des rôles avec Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f81b1-146">You do so by creating a service principal for the application and assigning roles to it via PowerShell.</span></span>

<span data-ttu-id="f81b1-147">Pour configurer l’authentification Active Directory pour Azure Data Lake, effectuez les tâches présentées dans les deux sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="f81b1-147">To set up Active Directory authentication for Azure Data Lake, perform the tasks in the following two sections.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="f81b1-148">Créer un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="f81b1-148">Create a self-signed certificate</span></span>
<span data-ttu-id="f81b1-149">Assurez-vous que le [SDK Windows](https://dev.windows.com/en-us/downloads) est installé avant de suivre la procédure décrite dans cette section.</span><span class="sxs-lookup"><span data-stu-id="f81b1-149">Make sure you have [Windows SDK](https://dev.windows.com/en-us/downloads) installed before proceeding with the steps in this section.</span></span> <span data-ttu-id="f81b1-150">Vous devez également avoir créé un répertoire, comme *C:\mycertdir*, où sera créé le certificat.</span><span class="sxs-lookup"><span data-stu-id="f81b1-150">You must have also created a directory, such as *C:\mycertdir*, where you create the certificate.</span></span>

1. <span data-ttu-id="f81b1-151">Dans la fenêtre PowerShell, accédez à l’emplacement où vous avez installé le Kit de développement logiciel (SDK) Windows (en général, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) et utilisez l’utilitaire [MakeCert][makecert] pour créer un certificat auto-signé et une clé privée.</span><span class="sxs-lookup"><span data-stu-id="f81b1-151">From the PowerShell window, go to the location where you installed Windows SDK (typically, *C:\Program Files (x86)\Windows Kits\10\bin\x86*) and use the [MakeCert][makecert] utility to create a self-signed certificate and a private key.</span></span> <span data-ttu-id="f81b1-152">Utilisez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f81b1-152">Use the following commands:</span></span>

        $certificateFileDir = "<my certificate directory>"
        cd $certificateFileDir

        makecert -sv mykey.pvk -n "cn=HDI-ADL-SP" CertFile.cer -r -len 2048

    <span data-ttu-id="f81b1-153">Vous devrez entrer le mot de passe de la clé privée.</span><span class="sxs-lookup"><span data-stu-id="f81b1-153">You will be prompted to enter the private key password.</span></span> <span data-ttu-id="f81b1-154">Une fois la commande exécutée avec succès, **CertFile.cer** et **mykey.pvk** apparaissent dans le répertoire du certificat que vous avez spécifié.</span><span class="sxs-lookup"><span data-stu-id="f81b1-154">After the command is successfully executed, you should see **CertFile.cer** and **mykey.pvk** in the certificate directory that you specified.</span></span>
2. <span data-ttu-id="f81b1-155">Utilisez l’utilitaire [Pvk2Pfx][pvk2pfx] pour convertir en un fichier .pfx les fichiers .pvk et .cer créés par MakeCert.</span><span class="sxs-lookup"><span data-stu-id="f81b1-155">Use the [Pvk2Pfx][pvk2pfx] utility to convert the .pvk and .cer files that MakeCert created to a .pfx file.</span></span> <span data-ttu-id="f81b1-156">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f81b1-156">Run the following command:</span></span>

        pvk2pfx -pvk mykey.pvk -spc CertFile.cer -pfx CertFile.pfx -po <password>

    <span data-ttu-id="f81b1-157">Lorsque vous y êtes invité, entrez le mot de passe de la clé privée spécifié au préalable.</span><span class="sxs-lookup"><span data-stu-id="f81b1-157">When you are prompted, enter the private key password that you specified earlier.</span></span> <span data-ttu-id="f81b1-158">La valeur que vous donnez au paramètre **-po** est le mot de passe associé au fichier .pfx.</span><span class="sxs-lookup"><span data-stu-id="f81b1-158">The value you specify for the **-po** parameter is the password that's associated with the .pfx file.</span></span> <span data-ttu-id="f81b1-159">Une fois la commande exécutée avec succès, un **CertFile.pfx** est visible dans le répertoire du certificat que vous avez spécifié.</span><span class="sxs-lookup"><span data-stu-id="f81b1-159">After the command has been completed successfully, you should also see a **CertFile.pfx** in the certificate directory that you specified.</span></span>

### <a name="create-an-azure-ad-and-a-service-principal"></a><span data-ttu-id="f81b1-160">Créer une application Azure AD et un principal de service</span><span class="sxs-lookup"><span data-stu-id="f81b1-160">Create an Azure AD and a service principal</span></span>
<span data-ttu-id="f81b1-161">Cette section décrit les étapes pour créer un principal de service pour une application Azure AD, attribuer un rôle au principal de service et vous authentifier en tant que principal de service en fournissant un certificat.</span><span class="sxs-lookup"><span data-stu-id="f81b1-161">In this section, you create a service principal for an Azure AD application, assign a role to the service principal, and authenticate as the service principal by providing a certificate.</span></span> <span data-ttu-id="f81b1-162">Pour créer une application dans Azure AD, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="f81b1-162">To create an application in Azure AD, run the following commands:</span></span>

1. <span data-ttu-id="f81b1-163">Collez les applets de commande suivantes dans la fenêtre de la console PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f81b1-163">Paste the following cmdlets in the PowerShell console window.</span></span> <span data-ttu-id="f81b1-164">Vérifiez que la valeur que vous donnez à la propriété **-DisplayName** est unique.</span><span class="sxs-lookup"><span data-stu-id="f81b1-164">Make sure that the value you specify for the **-DisplayName** property is unique.</span></span> <span data-ttu-id="f81b1-165">Les valeurs pour **-HomePage** et **-IdentiferUris** sont des valeurs d’espace réservé et ne sont pas vérifiées.</span><span class="sxs-lookup"><span data-stu-id="f81b1-165">The values for **-HomePage** and **-IdentiferUris** are placeholder values and are not verified.</span></span>

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
2. <span data-ttu-id="f81b1-166">Créez un principal de service en utilisant l’ID d’application.</span><span class="sxs-lookup"><span data-stu-id="f81b1-166">Create a service principal by using the application ID.</span></span>

        $servicePrincipal = New-AzureRmADServicePrincipal -ApplicationId $applicationId

        $objectId = $servicePrincipal.Id
3. <span data-ttu-id="f81b1-167">Accordez au principal du service l’accès à la racine et à tous les dossiers du chemin d’accès racine spécifié précédemment.</span><span class="sxs-lookup"><span data-stu-id="f81b1-167">Grant the service principal access to the Data Lake Store root and all the folders in the root path that you specified earlier.</span></span> <span data-ttu-id="f81b1-168">Utilisez les applets de commande suivantes :</span><span class="sxs-lookup"><span data-stu-id="f81b1-168">Use the following cmdlets:</span></span>

        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path / -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters -AceType User -Id $objectId -Permissions All
        Set-AzureRmDataLakeStoreItemAclEntry -AccountName $dataLakeStoreName -Path /clusters/hdiadlcluster -AceType User -Id $objectId -Permissions All

## <a name="create-an-hdinsight-linux-cluster-with-data-lake-store-as-the-default-storage"></a><span data-ttu-id="f81b1-169">Création d’un cluster Linux HDInsight avec Data Lake Store comme stockage par défaut</span><span class="sxs-lookup"><span data-stu-id="f81b1-169">Create an HDInsight Linux cluster with Data Lake Store as the default storage</span></span>

<span data-ttu-id="f81b1-170">Dans cette section, vous allez créer un cluster HDInsight Hadoop Linux avec Data Lake Store comme stockage par défaut.</span><span class="sxs-lookup"><span data-stu-id="f81b1-170">In this section, you create an HDInsight Hadoop Linux cluster with Data Lake Store as the default storage.</span></span> <span data-ttu-id="f81b1-171">Pour cette version, le cluster HDInsight et Data Lake Store doivent se situer au même emplacement.</span><span class="sxs-lookup"><span data-stu-id="f81b1-171">For this release, the HDInsight cluster and Data Lake Store must be in the same location.</span></span>

1. <span data-ttu-id="f81b1-172">Récupérez l’ID de locataire d’abonnement et stockez-le pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f81b1-172">Retrieve the subscription tenant ID, and store it to use later.</span></span>

        $tenantID = (Get-AzureRmContext).Tenant.TenantId

2. <span data-ttu-id="f81b1-173">Créez le cluster HDInsight en utilisant les applets de commande suivantes :</span><span class="sxs-lookup"><span data-stu-id="f81b1-173">Create the HDInsight cluster by using the following cmdlets:</span></span>

        # Set these variables

        $location = "East US 2"
        $storageAccountName = $dataLakeStoreName                       # Data Lake Store account name
        $storageRootPath = "<Storage root path you specified earlier>" # E.g. /clusters/hdiadlcluster
        $clusterName = "<unique cluster name>"
        $clusterNodes = <ClusterSizeInNodes>            # The number of nodes in the HDInsight cluster
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

    <span data-ttu-id="f81b1-174">Après exécution de l’applet de commande, le résultat énumère les détails du cluster.</span><span class="sxs-lookup"><span data-stu-id="f81b1-174">After the cmdlet has been successfully completed, you should see an output that lists the cluster details.</span></span>

## <a name="run-test-jobs-on-the-hdinsight-cluster-to-use-data-lake-store"></a><span data-ttu-id="f81b1-175">Exécuter des tâches de test sur le cluster HDInsight pour utiliser Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f81b1-175">Run test jobs on the HDInsight cluster to use Data Lake Store</span></span>
<span data-ttu-id="f81b1-176">Une fois que vous avez configuré un cluster HDInsight, vous pouvez exécuter des tâches de test sur le cluster pour vérifier qu’il peut accéder à Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f81b1-176">After you have configured an HDInsight cluster, you can run test jobs on it to ensure that it can access Data Lake Store.</span></span> <span data-ttu-id="f81b1-177">Pour ce faire, exécutez un exemple de tâche Hive qui crée une table avec les exemples de données déjà disponibles dans Data Lake Store dans *<cluster root>/example/data/sample.log*.</span><span class="sxs-lookup"><span data-stu-id="f81b1-177">To do so, run a sample Hive job to create a table that uses the sample data that's already available in Data Lake Store at *<cluster root>/example/data/sample.log*.</span></span>

<span data-ttu-id="f81b1-178">Dans cette section, vous établissez une connexion SSH (Secure Shell) au cluster HDInsight Linux que vous avez créé, puis vous exécutez l’exemple de requête Hive.</span><span class="sxs-lookup"><span data-stu-id="f81b1-178">In this section, you make a Secure Shell (SSH) connection into the HDInsight Linux cluster that you created, and then you run a sample Hive query.</span></span>

* <span data-ttu-id="f81b1-179">Si vous utilisez un client Windows pour établir la connexion SSH au cluster, consultez [Utilisation de SSH avec Hadoop Linux sur HDInsight à partir de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="f81b1-179">If you are using a Windows client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="f81b1-180">Si vous utilisez un client Linux pour établir la connexion SSH au cluster, consultez [Utilisation de SSH avec Hadoop Linux sur HDInsight à partir de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f81b1-180">If you are using a Linux client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="f81b1-181">Une fois que vous avez établi la connexion, démarrez l'interface de ligne de commande Hive à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f81b1-181">After you have made the connection, start the Hive command-line interface (CLI) by using the following command:</span></span>

        hive
2. <span data-ttu-id="f81b1-182">À l’aide de l’interface de ligne de commande, entrez les instructions suivantes pour créer une table nommée **vehicles** en utilisant les exemples de données dans Data Lake Store :</span><span class="sxs-lookup"><span data-stu-id="f81b1-182">Use the CLI to enter the following statements to create a new table named **vehicles** by using the sample data in Data Lake Store:</span></span>

        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'adl:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="f81b1-183">Vous devriez voir la sortie de la requête dans la console SSH.</span><span class="sxs-lookup"><span data-stu-id="f81b1-183">You should see the query output on the SSH console.</span></span>

    >[!NOTE]
    ><span data-ttu-id="f81b1-184">Le chemin d’accès aux exemples de données de la commande CREATE TABLE ci-dessus est `adl:///example/data/`, où `adl:///` est la racine du cluster.</span><span class="sxs-lookup"><span data-stu-id="f81b1-184">The path to the sample data in the preceding CREATE TABLE command is `adl:///example/data/`, where `adl:///` is the cluster root.</span></span> <span data-ttu-id="f81b1-185">Pour l’exemple de la racine de cluster spécifiée dans ce didacticiel, la commande est `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span><span class="sxs-lookup"><span data-stu-id="f81b1-185">Following the example of the cluster root that's specified in this tutorial, the command is `adl://hdiadlstore.azuredatalakestore.net/clusters/hdiadlcluster`.</span></span> <span data-ttu-id="f81b1-186">Vous pouvez utiliser l’alternative la plus courte ou fournir le chemin d’accès complet vers la racine du cluster.</span><span class="sxs-lookup"><span data-stu-id="f81b1-186">You can either use the shorter alternative or provide the complete path to the cluster root.</span></span>
    >

## <a name="access-data-lake-store-by-using-hdfs-commands"></a><span data-ttu-id="f81b1-187">Accéder à Data Lake Store avec les commandes HDFS</span><span class="sxs-lookup"><span data-stu-id="f81b1-187">Access Data Lake Store by using HDFS commands</span></span>
<span data-ttu-id="f81b1-188">Une fois que vous avez configuré le cluster HDInsight pour qu’il utilise Data Lake Store, vous pouvez utiliser les commandes de l’interpréteur de commandes HDFS (Hadoop Distributed File System) pour accéder au magasin.</span><span class="sxs-lookup"><span data-stu-id="f81b1-188">After you have configured the HDInsight cluster to use Data Lake Store, you can use Hadoop Distributed File System (HDFS) shell commands to access the store.</span></span>

<span data-ttu-id="f81b1-189">Dans cette section, vous établissez une connexion SSH au cluster HDInsight Linux que vous avez créé, puis vous exécutez les commandes HDFS.</span><span class="sxs-lookup"><span data-stu-id="f81b1-189">In this section, you make an SSH connection into the HDInsight Linux cluster that you created, and then you run the HDFS commands.</span></span>

* <span data-ttu-id="f81b1-190">Si vous utilisez un client Windows pour établir la connexion SSH au cluster, consultez [Utilisation de SSH avec Hadoop Linux sur HDInsight à partir de Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span><span class="sxs-lookup"><span data-stu-id="f81b1-190">If you are using a Windows client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Windows](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).</span></span>
* <span data-ttu-id="f81b1-191">Si vous utilisez un client Linux pour établir la connexion SSH au cluster, consultez [Utilisation de SSH avec Hadoop Linux sur HDInsight à partir de Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f81b1-191">If you are using a Linux client to make an SSH connection into the cluster, see [Use SSH with Linux-based Hadoop on HDInsight from Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="f81b1-192">Une fois que vous avez établi la connexion, répertoriez les fichiers dans Data Lake Store en utilisant la commande HDFS suivante.</span><span class="sxs-lookup"><span data-stu-id="f81b1-192">After you've made the connection, list the files in Data Lake Store by using the following HDFS file system command.</span></span>

    hdfs dfs -ls adl:///

<span data-ttu-id="f81b1-193">Vous pouvez également utiliser la commande `hdfs dfs -put` pour charger des fichiers dans Data Lake Store, puis utiliser `hdfs dfs -ls` pour vérifier si les fichiers ont été chargés avec succès.</span><span class="sxs-lookup"><span data-stu-id="f81b1-193">You can also use the `hdfs dfs -put` command to upload some files to Data Lake Store, and then use `hdfs dfs -ls` to verify whether the files were successfully uploaded.</span></span>

## <a name="see-also"></a><span data-ttu-id="f81b1-194">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f81b1-194">See also</span></span>
* [<span data-ttu-id="f81b1-195">Portail Azure : Créer un cluster HDInsight pour utiliser Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f81b1-195">Azure portal: Create an HDInsight cluster to use Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
