---
title: "Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’API .NET | Microsoft Docs"
description: "Dans ce didacticiel, vous allez créer un pipeline Azure Data Factory avec une activité de copie à l’aide de l’API .NET."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 58fc4007-b46d-4c8e-a279-cb9e479b3e2b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 52f72da54cdd80691e09d7453bf6730454c4089e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a><span data-ttu-id="f4580-103">Didacticiel : Créer un pipeline avec l’activité de copie à l’aide de l’API .NET</span><span class="sxs-lookup"><span data-stu-id="f4580-103">Tutorial: Create a pipeline with Copy Activity using .NET API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f4580-104">Vue d’ensemble et étapes préalables requises</span><span class="sxs-lookup"><span data-stu-id="f4580-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="f4580-105">Assistant de copie</span><span class="sxs-lookup"><span data-stu-id="f4580-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="f4580-106">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="f4580-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="f4580-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f4580-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="f4580-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4580-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="f4580-109">Modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f4580-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="f4580-110">API REST</span><span class="sxs-lookup"><span data-stu-id="f4580-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="f4580-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="f4580-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="f4580-112">Dans cet article, vous apprendrez comment toouse [API .NET](https://portal.azure.com) toocreate une fabrique de données avec un pipeline qui copie les données à partir d’une base de données SQL Azure de tooan stockage blob Azure.</span><span class="sxs-lookup"><span data-stu-id="f4580-112">In this article, you learn how toouse [.NET API](https://portal.azure.com) toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="f4580-113">Si vous êtes tooAzure nouvelle fabrique de données, lisez hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article avant d’entamer ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f4580-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="f4580-114">Dans ce didacticiel, vous créez un pipeline avec une activité : activité de copie.</span><span class="sxs-lookup"><span data-stu-id="f4580-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="f4580-115">activité de copie Hello copie des données à partir d’un magasin de données de données pris en charge magasin tooa récepteur pris en charge.</span><span class="sxs-lookup"><span data-stu-id="f4580-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="f4580-116">Pour obtenir la liste des magasins de données pris en charge en tant que sources et récepteurs, consultez [Magasins de données pris en charge](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="f4580-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="f4580-117">activité Hello est rendue possible par un service globalement disponible qui permettre copier des données entre différentes banques de données de manière sécurisée, fiable et évolutive.</span><span class="sxs-lookup"><span data-stu-id="f4580-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="f4580-118">Pour plus d’informations sur l’activité de copie de hello, consultez [les activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="f4580-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="f4580-119">Un pipeline peut contenir plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="f4580-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="f4580-120">De plus, vous pouvez concaténer les deux activités (exécutée une activité après l’autre) en définissant le dataset de sortie hello d’une activité hello d’entrée dataset Hello autre activité.</span><span class="sxs-lookup"><span data-stu-id="f4580-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="f4580-121">Pour plus d’informations, consultez [Plusieurs activités dans un pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="f4580-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="f4580-122">Pour la documentation complète sur l’API .NET pour Data Factory, consultez [Informations de référence sur l’API .NET Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="f4580-122">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>
> 
> <span data-ttu-id="f4580-123">le pipeline de données Hello dans ce didacticiel copie des données à partir d’un magasin de données de destination source données magasin tooa.</span><span class="sxs-lookup"><span data-stu-id="f4580-123">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="f4580-124">Pour obtenir un didacticiel sur la façon de tootransform les données à l’aide d’Azure Data Factory, consultez [didacticiel : créer un pipeline de données tootransform à l’aide de cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="f4580-124">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4580-125">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f4580-125">Prerequisites</span></span>
* <span data-ttu-id="f4580-126">Passez en revue [vue d’ensemble et conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget une vue d’ensemble du didacticiel de hello et hello complète **condition préalable** étapes.</span><span class="sxs-lookup"><span data-stu-id="f4580-126">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget an overview of hello tutorial and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="f4580-127">Visual Studio 2012, 2013 ou 2015</span><span class="sxs-lookup"><span data-stu-id="f4580-127">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="f4580-128">Téléchargez et installez le [Kit de développement logiciel (SDK) Azure .NET](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="f4580-128">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span></span>
* <span data-ttu-id="f4580-129">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f4580-129">Azure PowerShell.</span></span> <span data-ttu-id="f4580-130">Suivez les instructions de [comment tooinstall et configurer Azure PowerShell](../powershell-install-configure.md) article tooinstall Azure PowerShell sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f4580-130">Follow instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="f4580-131">Vous utilisez Azure PowerShell toocreate une application Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f4580-131">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="f4580-132">Créer une application dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f4580-132">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="f4580-133">Créer une application Azure Active Directory, créez un principal de service pour l’application hello et affectez-le toohello **collaborateur de fabrique de données** rôle.</span><span class="sxs-lookup"><span data-stu-id="f4580-133">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="f4580-134">Lancez **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="f4580-134">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="f4580-135">Exécutez hello suivant de commande et entrez le nom d’utilisateur hello et le mot de passe que vous utilisez toosign dans toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f4580-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="f4580-136">Exécutez hello suivant commande tooview tous les abonnements hello pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="f4580-136">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="f4580-137">Tooselect hello abonnement toowork avec la commande suivante d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="f4580-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="f4580-138">Remplacez  **&lt;NameOfAzureSubscription** &gt; avec le nom de hello de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f4580-138">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="f4580-139">Notez **SubscriptionId** et **TenantId** à partir de la sortie de hello de cette commande.</span><span class="sxs-lookup"><span data-stu-id="f4580-139">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="f4580-140">Créer un groupe de ressources Azure nommé **ADFTutorialResourceGroup** en exécutant hello commande Bonjour PowerShell suivante.</span><span class="sxs-lookup"><span data-stu-id="f4580-140">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="f4580-141">Si groupe de ressources hello existe déjà, vous spécifiez si tooupdate il (Y) ou conserver en tant que (N).</span><span class="sxs-lookup"><span data-stu-id="f4580-141">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="f4580-142">Si vous utilisez un autre groupe de ressources, vous devez le nom de hello toouse de votre groupe de ressources à la place de ADFTutorialResourceGroup dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f4580-142">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="f4580-143">Créez une application Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f4580-143">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="f4580-144">Si vous obtenez hello l’erreur suivante, spécifiez une autre URL et réexécutez la commande hello.</span><span class="sxs-lookup"><span data-stu-id="f4580-144">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="f4580-145">Créer hello principal du service Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f4580-145">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="f4580-146">Ajouter toohello principal de service **collaborateur de fabrique de données** rôle.</span><span class="sxs-lookup"><span data-stu-id="f4580-146">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="f4580-147">Obtenir l’ID d’application hello.</span><span class="sxs-lookup"><span data-stu-id="f4580-147">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="f4580-148">Notez l’ID d’application hello (applicationID) à partir de la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="f4580-148">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="f4580-149">Vous devez avoir les quatre valeurs suivantes après ces étapes :</span><span class="sxs-lookup"><span data-stu-id="f4580-149">You should have following four values from these steps:</span></span>

* <span data-ttu-id="f4580-150">ID client</span><span class="sxs-lookup"><span data-stu-id="f4580-150">Tenant ID</span></span>
* <span data-ttu-id="f4580-151">Identifiant d’abonnement</span><span class="sxs-lookup"><span data-stu-id="f4580-151">Subscription ID</span></span>
* <span data-ttu-id="f4580-152">ID de l'application</span><span class="sxs-lookup"><span data-stu-id="f4580-152">Application ID</span></span>
* <span data-ttu-id="f4580-153">Mot de passe (spécifié dans la première commande de hello)</span><span class="sxs-lookup"><span data-stu-id="f4580-153">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="f4580-154">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="f4580-154">Walkthrough</span></span>
1. <span data-ttu-id="f4580-155">À l’aide de Visual Studio 2012/2013/2015, créez une application console C# .NET.</span><span class="sxs-lookup"><span data-stu-id="f4580-155">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="f4580-156">Lancez **Visual Studio** 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="f4580-156">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="f4580-157">Cliquez sur **fichier**, pointez trop**nouveau**, puis cliquez sur **projet**.</span><span class="sxs-lookup"><span data-stu-id="f4580-157">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="f4580-158">Développez **Modèles**, puis sélectionnez **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="f4580-158">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="f4580-159">Dans cette procédure pas à pas, vous utilisez C#, mais vous pouvez utiliser un autre langage .NET.</span><span class="sxs-lookup"><span data-stu-id="f4580-159">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="f4580-160">Sélectionnez **Application Console** à partir de la liste hello des types de projets sur hello droite.</span><span class="sxs-lookup"><span data-stu-id="f4580-160">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="f4580-161">Entrez **DataFactoryAPITestApp** pour hello nom.</span><span class="sxs-lookup"><span data-stu-id="f4580-161">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="f4580-162">Sélectionnez **C:\ADFGetStarted** pour hello emplacement.</span><span class="sxs-lookup"><span data-stu-id="f4580-162">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="f4580-163">Cliquez sur **OK** projet hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="f4580-163">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="f4580-164">Cliquez sur **outils**, pointez trop**Gestionnaire de Package NuGet**, puis cliquez sur **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="f4580-164">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="f4580-165">Bonjour **Package Manager Console**, hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f4580-165">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="f4580-166">Exécutez hello suivant du package de fabrique de données tooinstall de commande :`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="f4580-166">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="f4580-167">Exécutez hello suivant du package d’Azure Active Directory tooinstall commandes (vous utilisez les API d’Active Directory dans le code hello) :`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="f4580-167">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="f4580-168">Ajoutez hello suivant **appSetttings** section toohello **App.config** fichier.</span><span class="sxs-lookup"><span data-stu-id="f4580-168">Add hello following **appSetttings** section toohello **App.config** file.</span></span> <span data-ttu-id="f4580-169">Ces paramètres sont utilisés par la méthode d’assistance de hello : **GetAuthorizationHeader**.</span><span class="sxs-lookup"><span data-stu-id="f4580-169">These settings are used by hello helper method: **GetAuthorizationHeader**.</span></span>

    <span data-ttu-id="f4580-170">Remplacez les valeurs de **&lt;ID d’Application&gt;**, **&lt;Mot de passe&gt;**, **&lt;ID d’abonnement&gt;**, et **&lt;ID client&gt;** par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="f4580-170">Replace values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```

5. <span data-ttu-id="f4580-171">Ajoutez hello suivant **à l’aide de** instructions toohello source fichier (Program.cs) hello projet.</span><span class="sxs-lookup"><span data-stu-id="f4580-171">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```

6. <span data-ttu-id="f4580-172">Ajouter hello suivant le code qui crée une instance de **DataPipelineManagementClient** classe toohello **Main** (méthode).</span><span class="sxs-lookup"><span data-stu-id="f4580-172">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="f4580-173">Vous utilisez cette toocreate objet une fabrique de données, un service lié, les jeux de données d’entrée et de sortie et un pipeline.</span><span class="sxs-lookup"><span data-stu-id="f4580-173">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="f4580-174">Vous montre également comment utiliser cet objet toomonitor de plusieurs secteurs un jeu de données lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="f4580-174">You also use this object toomonitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client
    string resourceGroupName = "ADFTutorialResourceGroup";
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="f4580-175">Remplacez la valeur hello **resourceGroupName** avec nom hello de votre groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="f4580-175">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span>
   >
   > <span data-ttu-id="f4580-176">Nom de la mise à jour de hello données fabrique (dataFactoryName) toobe unique.</span><span class="sxs-lookup"><span data-stu-id="f4580-176">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="f4580-177">Nom de la fabrique de données hello doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="f4580-177">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="f4580-178">Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f4580-178">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>

7. <span data-ttu-id="f4580-179">Ajouter hello suivant le code qui crée un **fabrique de données** toohello **Main** (méthode).</span><span class="sxs-lookup"><span data-stu-id="f4580-179">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```

    <span data-ttu-id="f4580-180">Une fabrique de données peut avoir un ou plusieurs pipelines.</span><span class="sxs-lookup"><span data-stu-id="f4580-180">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="f4580-181">Un pipeline peut contenir une ou plusieurs activités.</span><span class="sxs-lookup"><span data-stu-id="f4580-181">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="f4580-182">Par exemple, un activité de copie toocopy des données d’un magasin de données de destination tooa source et un toorun d’activité HDInsight Hive un tootransform de script Hive données tooproduct sortie les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="f4580-182">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="f4580-183">Commençons par créer la fabrique de données hello dans cette étape.</span><span class="sxs-lookup"><span data-stu-id="f4580-183">Let's start with creating hello data factory in this step.</span></span>
8. <span data-ttu-id="f4580-184">Ajouter hello suivant le code qui crée un **service lié Azure Storage** toohello **Main** (méthode).</span><span class="sxs-lookup"><span data-stu-id="f4580-184">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f4580-185">Remplacez **storageaccountname** et **accountkey** par le nom et la clé de votre compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f4580-185">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```

    <span data-ttu-id="f4580-186">Vous créez des services liés dans un toolink de fabrique de données stocke de vos données et fabrique de données toohello de services de calcul.</span><span class="sxs-lookup"><span data-stu-id="f4580-186">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="f4580-187">Dans ce didacticiel, vous n’allez pas utiliser n’importe quel service de calcul comme Azure HDInsight ou Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="f4580-187">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="f4580-188">Vous utilisez deux magasins de données de type Stockage Azure (source) et Base de données SQL Azure (destination).</span><span class="sxs-lookup"><span data-stu-id="f4580-188">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

    <span data-ttu-id="f4580-189">Vous créez ainsi deux services liés nommés AzureStorageLinkedService et AzureSqlLinkedService de types : AzureStorage et AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="f4580-189">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

    <span data-ttu-id="f4580-190">Hello AzureStorageLinkedService lie votre fabrique de données toohello compte stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="f4580-190">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="f4580-191">Ce compte de stockage est hello une dans laquelle vous créé un conteneur et à télécharger des données de hello dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="f4580-191">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
9. <span data-ttu-id="f4580-192">Ajouter hello suivant le code qui crée un **service lié Azure SQL** toohello **Main** (méthode).</span><span class="sxs-lookup"><span data-stu-id="f4580-192">Add hello following code that creates an **Azure SQL linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="f4580-193">Remplacez **servername**, **databasename**, **username** et **password** par le nom de votre serveur SQL Azure, le nom de la base de données, le nom de l’utilisateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="f4580-193">Replace **servername**, **databasename**, **username**, and **password** with names of your Azure SQL server, database, user, and password.</span></span>

    ```csharp
    // create a linked service for output data store: Azure SQL Database
    Console.WriteLine("Creating Azure SQL Database linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureSqlLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureSqlDatabaseLinkedService("Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30")
                )
            }
        }
    );
    ```

    <span data-ttu-id="f4580-194">AzureSqlLinkedService lie votre fabrique de données de toohello de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f4580-194">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="f4580-195">données Hello sont copiées à partir du stockage d’objets blob hello sont stockées dans cette base de données.</span><span class="sxs-lookup"><span data-stu-id="f4580-195">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="f4580-196">Vous avez créé la table emp de hello dans cette base de données dans le cadre de [conditions préalables](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="f4580-196">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
10. <span data-ttu-id="f4580-197">Ajouter hello suivant le code qui crée **jeux de données d’entrée et de sortie** toohello **Main** (méthode).</span><span class="sxs-lookup"><span data-stu-id="f4580-197">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "InputDataset";
    string Dataset_Destination = "OutputDataset";

    Console.WriteLine("Creating input dataset of type: Azure Blob");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                Structure = new List<DataElement>()
                {
                    new DataElement() { Name = "FirstName", Type = "String" },
                    new DataElement() { Name = "LastName", Type = "String" }
                },
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },

                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });

    Console.WriteLine("Creating output dataset of type: Azure SQL");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new DatasetCreateOrUpdateParameters()
        {
            Dataset = new Dataset()
            {
                Name = Dataset_Destination,
                Properties = new DatasetProperties()
                {
                    Structure = new List<DataElement>()
                    {
                        new DataElement() { Name = "FirstName", Type = "String" },
                        new DataElement() { Name = "LastName", Type = "String" }
                    },
                    LinkedServiceName = "AzureSqlLinkedService",
                    TypeProperties = new AzureSqlTableDataset()
                    {
                        TableName = "emp"
                    },
                    Availability = new Availability()
                    {
                        Frequency = SchedulePeriod.Hour,
                        Interval = 1,
                    },
                }
            }
        });
    ```
    
    <span data-ttu-id="f4580-198">Dans l’étape précédente de hello, vous avez créé toolink de services liés de votre compte de stockage Azure et de la fabrique de données de tooyour de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f4580-198">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="f4580-199">Dans cette étape, vous définissez deux jeux de données nommées InputDataset et OutputDataset qui représentent une entrée et les données de sortie qui sont stockées dans des magasins de données hello visés par AzureStorageLinkedService et AzureSqlLinkedService, respectivement.</span><span class="sxs-lookup"><span data-stu-id="f4580-199">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

    <span data-ttu-id="f4580-200">service lié Azure storage de Hello spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="f4580-200">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="f4580-201">Et, le jeu de données objet blob d’entrée hello (InputDataset) spécifie le conteneur de hello et dossier hello qui contient les données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="f4580-201">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="f4580-202">De même, hello service de base de données SQL Azure lié spécifie la chaîne de connexion hello service Data Factory utilise au moment de l’exécution tooconnect tooyour Azure base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="f4580-202">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="f4580-203">Et, hello sortie de jeu de données de table SQL (OututDataset) spécifie la table de hello Bonjour de toowhich hello de base de données à partir du stockage d’objets blob hello, les données sont copiées.</span><span class="sxs-lookup"><span data-stu-id="f4580-203">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

    <span data-ttu-id="f4580-204">Dans cette étape, vous créez un dataset nommé InputDataset qui pointe le fichier d’objet blob tooa (emp.txt) dans le dossier racine de hello d’un conteneur d’objets blob (adftutorial) Bonjour Azure Storage est représenté par hello AzureStorageLinkedService lié service.</span><span class="sxs-lookup"><span data-stu-id="f4580-204">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="f4580-205">Si vous ne spécifiez une valeur pour le nom de fichier hello (ignorer), les données à partir de tous les objets BLOB dans le dossier d’entrée de hello sont copiés toohello destination.</span><span class="sxs-lookup"><span data-stu-id="f4580-205">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="f4580-206">Dans ce didacticiel, vous spécifiez une valeur pour le nom de fichier hello.</span><span class="sxs-lookup"><span data-stu-id="f4580-206">In this tutorial, you specify a value for hello fileName.</span></span>    

    <span data-ttu-id="f4580-207">Dans cette étape, vous créez un jeu de données de sortie nommé **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="f4580-207">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="f4580-208">Ce jeu de données pointe tooa SQL table dans la base de données SQL Azure hello représenté par **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="f4580-208">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span>
11. <span data-ttu-id="f4580-209">Ajoutez le code suivant de hello **crée et Active un pipeline** toohello **Main** (méthode).</span><span class="sxs-lookup"><span data-stu-id="f4580-209">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="f4580-210">Dans cette étape, vous créez un pipeline avec une **activité de copie** qui utilise **InputDataset** en entrée et **OutputDataset** en sortie.</span><span class="sxs-lookup"><span data-stu-id="f4580-210">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2017, 5, 11, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = new DateTime(2017, 5, 12, 0, 0, 0, 0, DateTimeKind.Utc);
    string PipelineName = "ADFTutorialPipeline";

    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new PipelineCreateOrUpdateParameters()
        {
            Pipeline = new Pipeline()
            {
                Name = PipelineName,
                Properties = new PipelineProperties()
                {
                    Description = "Demo Pipeline for data transfer between blobs",

                    // Initial value for pipeline's active period. With this, you won't need tooset slice status
                    Start = PipelineActivePeriodStartTime,
                    End = PipelineActivePeriodEndTime,

                    Activities = new List<Activity>()
                    {
                        new Activity()
                        {
                            Name = "BlobToAzureSql",
                            Inputs = new List<ActivityInput>()
                            {
                                new ActivityInput() {
                                    Name = Dataset_Source
                                }
                            },
                            Outputs = new List<ActivityOutput>()
                            {
                                new ActivityOutput()
                                {
                                    Name = Dataset_Destination
                                }
                            },
                            TypeProperties = new CopyActivity()
                            {
                                Source = new BlobSource(),
                                Sink = new BlobSink()
                                {
                                    WriteBatchSize = 10000,
                                    WriteBatchTimeout = TimeSpan.FromMinutes(10)
                                }
                            }
                        }
                    }
                }
            }
        });
    ```

    <span data-ttu-id="f4580-211">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="f4580-211">Note hello following points:</span></span>
   
    - <span data-ttu-id="f4580-212">Dans la section d’activités hello, il n'existe qu’une seule activité dont **type** est défini trop**copie**.</span><span class="sxs-lookup"><span data-stu-id="f4580-212">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="f4580-213">Pour plus d’informations sur l’activité de copie hello, consultez [les activités de déplacement des données](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="f4580-213">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="f4580-214">Dans les solutions Data Factory, vous pouvez également utiliser [Activités de transformation des données](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="f4580-214">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="f4580-215">Entrée d’activité hello est définie trop**InputDataset** et de sortie d’activité hello est définie trop**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="f4580-215">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="f4580-216">Bonjour **typeProperties** section, **BlobSource** est spécifié comme type de source de hello et **SqlSink** est spécifié comme type de récepteur hello.</span><span class="sxs-lookup"><span data-stu-id="f4580-216">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="f4580-217">Pour obtenir une liste complète des magasins de données pris en charge par l’activité de copie hello en tant que sources et récepteurs, consultez [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="f4580-217">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="f4580-218">toolearn comment toouse données pris en charge spécifiques stocker en tant que source/récepteur, cliquez sur lien hello dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="f4580-218">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
   
    <span data-ttu-id="f4580-219">Actuellement, le dataset de sortie est les lecteurs hello planification.</span><span class="sxs-lookup"><span data-stu-id="f4580-219">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="f4580-220">Dans ce didacticiel, le dataset de sortie est tooproduce configuré une tranche une fois par heure.</span><span class="sxs-lookup"><span data-stu-id="f4580-220">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="f4580-221">pipeline de Hello a une heure de début et l’heure de fin sont un jour séparé, ce qui est de 24 heures.</span><span class="sxs-lookup"><span data-stu-id="f4580-221">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="f4580-222">Par conséquent, 24 tranches du jeu de données de sortie produits par le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="f4580-222">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span>
12. <span data-ttu-id="f4580-223">Ajouter hello suivant code toohello **Main** jeu de données de sortie de statut de hello tooget de méthode d’une tranche de données de hello.</span><span class="sxs-lookup"><span data-stu-id="f4580-223">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="f4580-224">Une seule tranche est attendue dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="f4580-224">There is only slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;

    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");        
        // wait before hello next status check
        Thread.Sleep(1000 * 12);

        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });

        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```

13. <span data-ttu-id="f4580-225">Ajouter hello suivant détails tooget exécuter du code pour un toohello de tranche de données **Main** (méthode).</span><span class="sxs-lookup"><span data-stu-id="f4580-225">Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");

    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
    Console.ReadKey();

    var datasliceRunListResponse = client.DataSliceRuns.List(
            resourceGroupName,
            dataFactoryName,
            Dataset_Destination,
            new DataSliceRunListParameters()
            {
                DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
            }
        );

    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }

    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```

14. <span data-ttu-id="f4580-226">Ajouter hello suivant la méthode d’assistance utilisée par hello **principal** méthode toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="f4580-226">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f4580-227">Lorsque vous copiez et collez hello suivant de code, assurez-vous que hello code copié est à hello hello méthode Main de même niveau.</span><span class="sxs-lookup"><span data-stu-id="f4580-227">When you copy and paste hello following code, make sure that hello copied code is at hello same level as hello Main method.</span></span>

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed tooacquire token");
    }
    ```

15. <span data-ttu-id="f4580-228">Hello l’Explorateur de solutions, développez le projet hello (DataFactoryAPITestApp), avec le bouton droit dans **références**, puis cliquez sur **ajouter une référence**.</span><span class="sxs-lookup"><span data-stu-id="f4580-228">In hello Solution Explorer, expand hello project (DataFactoryAPITestApp), right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="f4580-229">Cochez la case de l’assemblage **System.Configuration**.</span><span class="sxs-lookup"><span data-stu-id="f4580-229">Select check box for **System.Configuration** assembly.</span></span> <span data-ttu-id="f4580-230">et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f4580-230">and click **OK**.</span></span>
16. <span data-ttu-id="f4580-231">Créer une application de console hello.</span><span class="sxs-lookup"><span data-stu-id="f4580-231">Build hello console application.</span></span> <span data-ttu-id="f4580-232">Cliquez sur **générer** sur hello menu et cliquez sur **générer la Solution**.</span><span class="sxs-lookup"><span data-stu-id="f4580-232">Click **Build** on hello menu and click **Build Solution**.</span></span>
17. <span data-ttu-id="f4580-233">Confirmer qu’il existe au moins un fichier Bonjour **adftutorial** conteneur dans votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="f4580-233">Confirm that there is at least one file in hello **adftutorial** container in your Azure blob storage.</span></span> <span data-ttu-id="f4580-234">Dans le cas contraire, créez **Emp.txt** fichier hello suivant contenu dans le bloc-notes, puis téléchargez-le toohello adftutorial conteneur.</span><span class="sxs-lookup"><span data-stu-id="f4580-234">If not, create **Emp.txt** file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
18. <span data-ttu-id="f4580-235">Exécuter l’exemple hello en cliquant sur **déboguer** -> **démarrer le débogage** menu hello.</span><span class="sxs-lookup"><span data-stu-id="f4580-235">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="f4580-236">Lorsque vous consultez hello **détails d’une tranche de données mise en route de l’exécution**, attendez quelques minutes, puis appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="f4580-236">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
19. <span data-ttu-id="f4580-237">Utilisez hello tooverify portail Azure cette fabrique de données hello **APITutorialFactory** est créée avec hello suivant artefacts :</span><span class="sxs-lookup"><span data-stu-id="f4580-237">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
   * <span data-ttu-id="f4580-238">Service lié : **LinkedService_AzureStorage**</span><span class="sxs-lookup"><span data-stu-id="f4580-238">Linked service: **LinkedService_AzureStorage**</span></span>
   * <span data-ttu-id="f4580-239">Jeu de données : **InputDataset** et **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="f4580-239">Dataset: **InputDataset** and **OutputDataset**.</span></span>
   * <span data-ttu-id="f4580-240">Pipeline : **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="f4580-240">Pipeline: **PipelineBlobSample**</span></span>
20. <span data-ttu-id="f4580-241">Vérifiez que les enregistrements d’employés hello deux sont créés dans hello **emp** table Bonjour spécifiée de la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="f4580-241">Verify that hello two employee records are created in hello **emp** table in hello specified Azure SQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4580-242">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f4580-242">Next steps</span></span>
<span data-ttu-id="f4580-243">Pour la documentation complète sur l’API .NET pour Data Factory, consultez [Informations de référence sur l’API .NET Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="f4580-243">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>

<span data-ttu-id="f4580-244">Dans ce didacticiel, vous avez utilisé le stockage Blob Azure comme magasin de données source et une base de données SQL Azure comme banque de données de destination dans une opération de copie.</span><span class="sxs-lookup"><span data-stu-id="f4580-244">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="f4580-245">Hello tableau suivant fournit une liste de banques de données pris en charge en tant que sources et destinations par l’activité de copie hello :</span><span class="sxs-lookup"><span data-stu-id="f4580-245">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="f4580-246">toolearn sur la banque de données de toocopy vers/à partir de données, cliquez sur lien hello hello magasin de données dans la table de hello.</span><span class="sxs-lookup"><span data-stu-id="f4580-246">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>

