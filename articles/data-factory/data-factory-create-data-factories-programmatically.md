---
title: "Créer des pipelines de données à l’aide du Kit de développement logiciel (SDK) .NET Azure | Microsoft Docs"
description: "Découvrez comment créer, analyser et gérer par programmation des fabriques de données Azure à l'aide du Kit de développement logiciel (SDK) Data Factory."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 9d9dac75321c5d4e079f49320d9b7c6f56e48754
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="83187-103">Créer, surveiller et gérer des fabriques de données Azure à l’aide du Kit de développement logiciel (SDK) Azure Data Factory .NET</span><span class="sxs-lookup"><span data-stu-id="83187-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="83187-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="83187-104">Overview</span></span>
<span data-ttu-id="83187-105">Vous pouvez créer, surveiller et gérer des fabriques de données Azure par programmation à l'aide du Kit SDK Data Factory .NET.</span><span class="sxs-lookup"><span data-stu-id="83187-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="83187-106">Cet article contient une procédure pas à pas que vous pouvez suivre pour créer un exemple d'application console .NET qui crée et surveille une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="83187-106">This article contains a walkthrough that you can follow to create a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="83187-107">Cet article ne couvre pas toutes les API .NET Data Factory.</span><span class="sxs-lookup"><span data-stu-id="83187-107">This article does not cover all the Data Factory .NET API.</span></span> <span data-ttu-id="83187-108">Consultez [Informations de référence sur l’API .NET Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) pour la documentation complète sur l’API .NET pour Data Factory.</span><span class="sxs-lookup"><span data-stu-id="83187-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="83187-109">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="83187-109">Prerequisites</span></span>
* <span data-ttu-id="83187-110">Visual Studio 2012, 2013 ou 2015</span><span class="sxs-lookup"><span data-stu-id="83187-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="83187-111">Téléchargez et installez le [Kit SDK Azure .NET](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="83187-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="83187-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83187-112">Azure PowerShell.</span></span> <span data-ttu-id="83187-113">Suivez les instructions de l’article [Installation et configuration d’Azure PowerShell](/powershell/azure/overview) pour installer Azure PowerShell sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="83187-113">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install Azure PowerShell on your computer.</span></span> <span data-ttu-id="83187-114">Vous utilisez Azure PowerShell pour créer une application Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="83187-114">You use Azure PowerShell to create an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="83187-115">Créer une application dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83187-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="83187-116">Créez une application Azure Active Directory, créez un principal de service pour l’application et attribuez-lui le rôle **Contributeurs de Data Factory** .</span><span class="sxs-lookup"><span data-stu-id="83187-116">Create an Azure Active Directory application, create a service principal for the application, and assign it to the **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="83187-117">Lancez **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="83187-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="83187-118">Exécutez la commande suivante, puis saisissez le nom d’utilisateur et le mot de passe que vous avez utilisés pour la connexion au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="83187-118">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="83187-119">Exécutez la commande suivante pour afficher tous les abonnements de ce compte.</span><span class="sxs-lookup"><span data-stu-id="83187-119">Run the following command to view all the subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="83187-120">Exécutez la commande suivante pour sélectionner l’abonnement que vous souhaitez utiliser.</span><span class="sxs-lookup"><span data-stu-id="83187-120">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="83187-121">Remplacez **&lt;NameOfAzureSubscription**&gt; par le nom de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="83187-121">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="83187-122">Notez les éléments **SubscriptionId** et **TenantId** dans la sortie de cette commande.</span><span class="sxs-lookup"><span data-stu-id="83187-122">Note down **SubscriptionId** and **TenantId** from the output of this command.</span></span>

5. <span data-ttu-id="83187-123">Créez un groupe de ressources Azure nommé **ADFTutorialResourceGroup** en exécutant la commande suivante dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="83187-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="83187-124">Si le groupe de ressources existe, indiquez s’il faut le mettre à jour (Y) ou le conserver tel quel (N).</span><span class="sxs-lookup"><span data-stu-id="83187-124">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="83187-125">Si vous utilisez un autre groupe de ressources, vous devez remplacer ADFTutorialResourceGroup par le nom de votre groupe de ressources dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="83187-125">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="83187-126">Créez une application Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="83187-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="83187-127">Si vous obtenez l’erreur suivante, spécifiez une autre URL et relancez la commande.</span><span class="sxs-lookup"><span data-stu-id="83187-127">If you get the following error, specify a different URL and run the command again.</span></span>
    
    ```PowerShell
    Another object with the same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="83187-128">Créez le principal du service AD.</span><span class="sxs-lookup"><span data-stu-id="83187-128">Create the AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="83187-129">Ajoutez le principal du service au rôle **Contributeurs de Data Factory** .</span><span class="sxs-lookup"><span data-stu-id="83187-129">Add service principal to the **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="83187-130">Récupérez l’ID de l’application.</span><span class="sxs-lookup"><span data-stu-id="83187-130">Get the application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="83187-131">Notez l’ID d’application (applicationID) dans la sortie.</span><span class="sxs-lookup"><span data-stu-id="83187-131">Note down the application ID (applicationID) from the output.</span></span>

<span data-ttu-id="83187-132">Vous devez avoir les quatre valeurs suivantes après ces étapes :</span><span class="sxs-lookup"><span data-stu-id="83187-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="83187-133">ID client</span><span class="sxs-lookup"><span data-stu-id="83187-133">Tenant ID</span></span>
* <span data-ttu-id="83187-134">Identifiant d’abonnement</span><span class="sxs-lookup"><span data-stu-id="83187-134">Subscription ID</span></span>
* <span data-ttu-id="83187-135">ID de l'application</span><span class="sxs-lookup"><span data-stu-id="83187-135">Application ID</span></span>
* <span data-ttu-id="83187-136">Mot de passe (spécifié dans la première commande)</span><span class="sxs-lookup"><span data-stu-id="83187-136">Password (specified in the first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="83187-137">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="83187-137">Walkthrough</span></span>
<span data-ttu-id="83187-138">Dans la procédure pas à pas, vous créez une fabrique de données avec un pipeline qui contient une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="83187-138">In the walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="83187-139">L’activité de copie les données d’un dossier de votre stockage d’objets blob Azure vers un autre dossier dans le même stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="83187-139">The copy activity copies data from a folder in your Azure blob storage to another folder in the same blob storage.</span></span> 

<span data-ttu-id="83187-140">L’activité de copie effectue le déplacement des données dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="83187-140">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="83187-141">Elle est mise en œuvre par un service disponible dans le monde entier, capable de copier des données entre différents magasins de données de façon sécurisée, fiable et évolutive.</span><span class="sxs-lookup"><span data-stu-id="83187-141">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="83187-142">Pour plus d’informations sur l’activité de copie, consultez l’article [Activités de déplacement des données](data-factory-data-movement-activities.md) .</span><span class="sxs-lookup"><span data-stu-id="83187-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

1. <span data-ttu-id="83187-143">À l’aide de Visual Studio 2012/2013/2015, créez une application console C# .NET.</span><span class="sxs-lookup"><span data-stu-id="83187-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="83187-144">Lancez **Visual Studio** 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="83187-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="83187-145">Cliquez sur **Fichier**, pointez le curseur de la souris sur **Nouveau**, puis cliquez sur **Projet**.</span><span class="sxs-lookup"><span data-stu-id="83187-145">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="83187-146">Développez **Modèles**, puis sélectionnez **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="83187-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="83187-147">Dans cette procédure pas à pas, vous utilisez C#, mais vous pouvez utiliser un autre langage .NET.</span><span class="sxs-lookup"><span data-stu-id="83187-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="83187-148">Sélectionnez **Application console** dans la liste des types de projet située sur la droite.</span><span class="sxs-lookup"><span data-stu-id="83187-148">Select **Console Application** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="83187-149">Entrez **DataFactoryAPITestApp** dans le champ Nom.</span><span class="sxs-lookup"><span data-stu-id="83187-149">Enter **DataFactoryAPITestApp** for the Name.</span></span>
   6. <span data-ttu-id="83187-150">Sélectionnez **C:\ADFGetStarted** dans le champ Emplacement.</span><span class="sxs-lookup"><span data-stu-id="83187-150">Select **C:\ADFGetStarted** for the Location.</span></span>
   7. <span data-ttu-id="83187-151">Cliquez sur **OK** pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="83187-151">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="83187-152">Cliquez sur **Outils**, pointez le curseur de la souris sur **Gestionnaire de package NuGet**, puis cliquez sur **Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="83187-152">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="83187-153">Dans la **Console du Gestionnaire de package**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="83187-153">In the **Package Manager Console**, do the following steps:</span></span>
   1. <span data-ttu-id="83187-154">Exécutez la commande suivante pour installer le package Data Factory : `Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="83187-154">Run the following command to install Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="83187-155">Exécutez la commande suivante pour installer le package Azure Active Directory (vous utilisez l’API Active Directory dans le code) : `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="83187-155">Run the following command to install Azure Active Directory package (you use Active Directory API in the code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="83187-156">Remplacez le contenu du fichier **App.config** du projet par le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="83187-156">Replace the contents of **App.config** file in the project with the following content:</span></span> 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating the AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. <span data-ttu-id="83187-157">Dans le fichier App.Config, remplacez les valeurs de **&lt;ID d’Application&gt;**, **&lt;Mot de passe&gt;**, **&lt;ID d’abonnement&gt;**, et **&lt;ID client&gt;** par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="83187-157">In the App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="83187-158">Ajoutez les instructions **using** ci-après dans le fichier **Program.cs** du projet.</span><span class="sxs-lookup"><span data-stu-id="83187-158">Add the following **using** statements to the **Program.cs** file in the project.</span></span>

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
6. <span data-ttu-id="83187-159">Ajoutez à la méthode **Main** le code suivant, qui crée une instance de la classe **DataPipelineManagementClient**.</span><span class="sxs-lookup"><span data-stu-id="83187-159">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span></span> <span data-ttu-id="83187-160">Cet objet vous permet de créer une fabrique de données, un service lié, des jeux de données d’entrée et de sortie, ainsi qu’un pipeline.</span><span class="sxs-lookup"><span data-stu-id="83187-160">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="83187-161">Il vous permet également d’analyser les tranches d’un jeu de données lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="83187-161">You also use this object to monitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client

    //IMPORTANT: specify the name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: the name of the data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="83187-162">Remplacez la valeur de **resourceGroupName** par le nom de votre groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="83187-162">Replace the value of **resourceGroupName** with the name of your Azure resource group.</span></span> <span data-ttu-id="83187-163">Vous pouvez créer un groupe de ressources à l’aide du cmdlet [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) .</span><span class="sxs-lookup"><span data-stu-id="83187-163">You can create a resource group using the [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="83187-164">Mettez à jour le nom de la fabrique de données (dataFactoryName) pour le rendre unique.</span><span class="sxs-lookup"><span data-stu-id="83187-164">Update name of the data factory (dataFactoryName) to be unique.</span></span> <span data-ttu-id="83187-165">Le nom de la fabrique de données doit être un nom global unique.</span><span class="sxs-lookup"><span data-stu-id="83187-165">Name of the data factory must be globally unique.</span></span> <span data-ttu-id="83187-166">Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.</span><span class="sxs-lookup"><span data-stu-id="83187-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="83187-167">Ajoutez à la méthode **Main** le code suivant, qui crée une **fabrique de données**.</span><span class="sxs-lookup"><span data-stu-id="83187-167">Add the following code that creates a **data factory** to the **Main** method.</span></span>

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
8. <span data-ttu-id="83187-168">Ajoutez le code suivant pour créer un **service lié Azure Storage** dans la méthode **Main**.</span><span class="sxs-lookup"><span data-stu-id="83187-168">Add the following code that creates an **Azure Storage linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="83187-169">Remplacez **storageaccountname** et **accountkey** par le nom et la clé de votre compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="83187-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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
9. <span data-ttu-id="83187-170">Ajoutez à la méthode **Main** le code suivant, qui crée des **jeux de données d’entrée et de sortie**.</span><span class="sxs-lookup"><span data-stu-id="83187-170">Add the following code that creates **input and output datasets** to the **Main** method.</span></span>

    <span data-ttu-id="83187-171">Le paramètre **FolderPath** de l’objet blob d’entrée a la valeur **adftutorial/**, où **adftutorial** est le nom du conteneur dans votre stockage des objets blob.</span><span class="sxs-lookup"><span data-stu-id="83187-171">The **FolderPath** for the input blob is set to **adftutorial/** where **adftutorial** is the name of the container in your blob storage.</span></span> <span data-ttu-id="83187-172">Si ce conteneur n'existe pas dans votre stockage d'objets blob Azure, créez un conteneur nommé **adftutorial** et chargez un fichier texte sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="83187-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file to the container.</span></span>

    <span data-ttu-id="83187-173">Le paramètre FolderPath de l’objet blob de sortie est défini sur **adftutorial/apifactoryoutput/{Slice}** où la valeur **Slice** est calculée dynamiquement en fonction de la valeur de **SliceStart** (date/heure de début de chaque tranche).</span><span class="sxs-lookup"><span data-stu-id="83187-173">The FolderPath for the output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on the value of **SliceStart** (start date-time of each slice.)</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
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
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
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
10. <span data-ttu-id="83187-174">Ajoutez à la méthode **Main** le code suivant, qui **crée et active un pipeline**.</span><span class="sxs-lookup"><span data-stu-id="83187-174">Add the following code that **creates and activates a pipeline** to the **Main** method.</span></span> <span data-ttu-id="83187-175">Ce pipeline dispose d’une fonction **CopyActivity** qui accepte **BlobSource** en tant que source et **BlobSink** en tant que récepteur.</span><span class="sxs-lookup"><span data-stu-id="83187-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="83187-176">L’activité de copie effectue le déplacement des données dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="83187-176">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="83187-177">Elle est mise en œuvre par un service disponible dans le monde entier, capable de copier des données entre différents magasins de données de façon sécurisée, fiable et évolutive.</span><span class="sxs-lookup"><span data-stu-id="83187-177">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="83187-178">Pour plus d’informations sur l’activité de copie, consultez l’article [Activités de déplacement des données](data-factory-data-movement-activities.md) .</span><span class="sxs-lookup"><span data-stu-id="83187-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new PipelineCreateOrUpdateParameters()
    {
        Pipeline = new Pipeline()
        {
            Name = PipelineName,
            Properties = new PipelineProperties()
            {
                Description = "Demo Pipeline for data transfer between blobs",
    
                // Initial value for pipeline's active period. With this, you won't need to set slice status
                Start = PipelineActivePeriodStartTime,
                End = PipelineActivePeriodEndTime,
    
                Activities = new List<Activity>()
                {
                    new Activity()
                    {
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
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
    
                },
            }
        }
    });
    ```
12. <span data-ttu-id="83187-179">Ajoutez le code suivant à la méthode **Main** pour obtenir l’état d’une tranche de données du jeu de données de sortie.</span><span class="sxs-lookup"><span data-stu-id="83187-179">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span></span> <span data-ttu-id="83187-180">Une seule tranche est attendue dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="83187-180">There is only one slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling the slice status");
        // wait before the next status check
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
13. <span data-ttu-id="83187-181">**(facultatif)** Ajoutez à la méthode **Main** le code suivant pour obtenir les détails d’exécution d’une tranche de données.</span><span class="sxs-lookup"><span data-stu-id="83187-181">**(optional)** Add the following code to get run details for a data slice to the **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for the output slice to be ready
    Console.WriteLine("\nGive it a few minutes for the output slice to be ready and press any key.");
    Console.ReadKey();
    
    var datasliceRunListResponse = client.DataSliceRuns.List(
        resourceGroupName,
        dataFactoryName,
        Dataset_Destination,
        new DataSliceRunListParameters()
        {
            DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
        });
    
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
    
    Console.WriteLine("\nPress any key to exit.");
    Console.ReadKey();
    ```
14. <span data-ttu-id="83187-182">Ajoutez à la classe **Program** la méthode d’assistance suivante utilisée par la méthode **Main**.</span><span class="sxs-lookup"><span data-stu-id="83187-182">Add the following helper method used by the **Main** method to the **Program** class.</span></span> <span data-ttu-id="83187-183">Cette méthode affiche une boîte de dialogue qui vous permet de fournir un **nom d’utilisateur** et un **mot de passe** de connexion au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="83187-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use to log in to Azure portal.</span></span>

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

        throw new InvalidOperationException("Failed to acquire token");
    }
    ```

15. <span data-ttu-id="83187-184">Dans l’Explorateur de solutions, développez le projet **DataFactoryAPITestApp**, cliquez avec le bouton droit sur **Références**, puis cliquez sur **Ajouter une référence**.</span><span class="sxs-lookup"><span data-stu-id="83187-184">In the Solution Explorer, expand the project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="83187-185">Cochez la case pour l’assembly `System.Configuration` et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="83187-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="83187-186">Générez l'application console.</span><span class="sxs-lookup"><span data-stu-id="83187-186">Build the console application.</span></span> <span data-ttu-id="83187-187">Dans le menu, cliquez sur **Générer**, puis sur **Générer la solution**.</span><span class="sxs-lookup"><span data-stu-id="83187-187">Click **Build** on the menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="83187-188">Vérifiez qu'il existe au moins un fichier dans le conteneur adftutorial de votre stockage d'objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="83187-188">Confirm that there is at least one file in the adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="83187-189">Si ce n'est pas le cas, créez le fichier Emp.txt dans le bloc-notes avec le contenu suivant, puis chargez-le sur le conteneur adftutorial.</span><span class="sxs-lookup"><span data-stu-id="83187-189">If not, create Emp.txt file in Notepad with the following content and upload it to the adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="83187-190">Exécutez l’exemple en cliquant dans le menu sur **Déboguer** -> **Démarrer le débogage**.</span><span class="sxs-lookup"><span data-stu-id="83187-190">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span></span> <span data-ttu-id="83187-191">Si **Obtention des détails d’exécution d’une tranche de données** s’affiche, patientez quelques minutes, puis appuyez sur **Entrée**.</span><span class="sxs-lookup"><span data-stu-id="83187-191">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="83187-192">Utilisez le portail Azure pour vérifier que la fabrique de données **APITutorialFactory** est créée avec les artefacts suivants :</span><span class="sxs-lookup"><span data-stu-id="83187-192">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span></span>
    * <span data-ttu-id="83187-193">Service lié : **AzureStorageLinkedService**</span><span class="sxs-lookup"><span data-stu-id="83187-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="83187-194">Jeu de données : **DatasetBlobSource** et **DatasetBlobDestination**.</span><span class="sxs-lookup"><span data-stu-id="83187-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="83187-195">Pipeline : **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="83187-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="83187-196">Vérifiez qu’un fichier de sortie est créé dans le dossier **apifactoryoutput** du conteneur **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="83187-196">Verify that an output file is created in the **apifactoryoutput** folder in the **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="83187-197">Obtenir une liste des tranches de données en échec</span><span class="sxs-lookup"><span data-stu-id="83187-197">Get a list of failed data slices</span></span> 

```csharp
// Parse the resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a><span data-ttu-id="83187-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="83187-198">Next steps</span></span>
<span data-ttu-id="83187-199">Consultez l’exemple suivant pour créer un pipeline à l’aide du Kit de développement logiciel .NET qui copie les données d’un stockage d’objets blob Azure dans une base de données SQL Azure :</span><span class="sxs-lookup"><span data-stu-id="83187-199">See the following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage to an Azure SQL database:</span></span> 

- [<span data-ttu-id="83187-200">Créer un pipeline pour copier des données de stockage d’objets Blob dans SQL Database</span><span class="sxs-lookup"><span data-stu-id="83187-200">Create a pipeline to copy data from Blob Storage to SQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
