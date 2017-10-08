---
title: "aaaCreate des pipelines de données à l’aide du Kit de développement .NET Azure | Documents Microsoft"
description: "Découvrez comment tooprogrammatically créer, surveiller et gérer des fabriques de données Azure à l’aide du SDK de fabrique de données."
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
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="e4aeb-103">Créer, surveiller et gérer des fabriques de données Azure à l’aide du Kit de développement logiciel (SDK) Azure Data Factory .NET</span><span class="sxs-lookup"><span data-stu-id="e4aeb-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="e4aeb-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="e4aeb-104">Overview</span></span>
<span data-ttu-id="e4aeb-105">Vous pouvez créer, surveiller et gérer des fabriques de données Azure par programmation à l'aide du Kit SDK Data Factory .NET.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="e4aeb-106">Cet article contient une procédure pas à pas que vous pouvez suivre toocreate une exemple .NET d’application console qui crée et analyse d’une fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-106">This article contains a walkthrough that you can follow toocreate a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="e4aeb-107">Cet article ne couvre pas hello toutes les API .NET de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-107">This article does not cover all hello Data Factory .NET API.</span></span> <span data-ttu-id="e4aeb-108">Consultez [Informations de référence sur l’API .NET Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) pour la documentation complète sur l’API .NET pour Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e4aeb-109">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="e4aeb-109">Prerequisites</span></span>
* <span data-ttu-id="e4aeb-110">Visual Studio 2012, 2013 ou 2015</span><span class="sxs-lookup"><span data-stu-id="e4aeb-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="e4aeb-111">Téléchargez et installez le [Kit SDK Azure .NET](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e4aeb-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="e4aeb-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-112">Azure PowerShell.</span></span> <span data-ttu-id="e4aeb-113">Suivez les instructions de [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) article tooinstall Azure PowerShell sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-113">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="e4aeb-114">Vous utilisez Azure PowerShell toocreate une application Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-114">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="e4aeb-115">Créer une application dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e4aeb-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="e4aeb-116">Créer une application Azure Active Directory, créez un principal de service pour l’application hello et affectez-le toohello **collaborateur de fabrique de données** rôle.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-116">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="e4aeb-117">Lancez **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="e4aeb-118">Exécutez hello suivant de commande et entrez le nom d’utilisateur hello et le mot de passe que vous utilisez toosign dans toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-118">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="e4aeb-119">Exécutez hello suivant commande tooview tous les abonnements hello pour ce compte.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-119">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="e4aeb-120">Tooselect hello abonnement toowork avec la commande suivante d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-120">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="e4aeb-121">Remplacez  **&lt;NameOfAzureSubscription** &gt; avec le nom de hello de votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-121">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="e4aeb-122">Notez **SubscriptionId** et **TenantId** à partir de la sortie de hello de cette commande.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-122">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="e4aeb-123">Créer un groupe de ressources Azure nommé **ADFTutorialResourceGroup** en exécutant hello commande Bonjour PowerShell suivante.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="e4aeb-124">Si groupe de ressources hello existe déjà, vous spécifiez si tooupdate il (Y) ou conserver en tant que (N).</span><span class="sxs-lookup"><span data-stu-id="e4aeb-124">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="e4aeb-125">Si vous utilisez un autre groupe de ressources, vous devez le nom de hello toouse de votre groupe de ressources à la place de ADFTutorialResourceGroup dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-125">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="e4aeb-126">Créez une application Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="e4aeb-127">Si vous obtenez hello l’erreur suivante, spécifiez une autre URL et réexécutez la commande hello.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-127">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="e4aeb-128">Créer hello principal du service Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-128">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="e4aeb-129">Ajouter toohello principal de service **collaborateur de fabrique de données** rôle.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-129">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="e4aeb-130">Obtenir l’ID d’application hello.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-130">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="e4aeb-131">Notez l’ID d’application hello (applicationID) à partir de la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-131">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="e4aeb-132">Vous devez avoir les quatre valeurs suivantes après ces étapes :</span><span class="sxs-lookup"><span data-stu-id="e4aeb-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="e4aeb-133">ID client</span><span class="sxs-lookup"><span data-stu-id="e4aeb-133">Tenant ID</span></span>
* <span data-ttu-id="e4aeb-134">Identifiant d’abonnement</span><span class="sxs-lookup"><span data-stu-id="e4aeb-134">Subscription ID</span></span>
* <span data-ttu-id="e4aeb-135">ID de l'application</span><span class="sxs-lookup"><span data-stu-id="e4aeb-135">Application ID</span></span>
* <span data-ttu-id="e4aeb-136">Mot de passe (spécifié dans la première commande de hello)</span><span class="sxs-lookup"><span data-stu-id="e4aeb-136">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="e4aeb-137">Procédure pas à pas</span><span class="sxs-lookup"><span data-stu-id="e4aeb-137">Walkthrough</span></span>
<span data-ttu-id="e4aeb-138">Hello procédure pas à pas, vous créez une fabrique de données avec un pipeline qui contient une activité de copie.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-138">In hello walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="e4aeb-139">Hello activité de copie copie les données à partir d’un dossier dans le dossier tooanother stockage blob Azure hello même stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-139">hello copy activity copies data from a folder in your Azure blob storage tooanother folder in hello same blob storage.</span></span> 

<span data-ttu-id="e4aeb-140">Activité de copie de Hello effectue le déplacement des données de hello dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-140">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="e4aeb-141">activité Hello est rendue possible par un service globalement disponible qui permettre copier des données entre différentes banques de données de manière sécurisée, fiable et évolutive.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-141">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="e4aeb-142">Consultez [les activités de déplacement des données](data-factory-data-movement-activities.md) article pour plus d’informations sur l’activité de copie de hello.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

1. <span data-ttu-id="e4aeb-143">À l’aide de Visual Studio 2012/2013/2015, créez une application console C# .NET.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="e4aeb-144">Lancez **Visual Studio** 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="e4aeb-145">Cliquez sur **fichier**, pointez trop**nouveau**, puis cliquez sur **projet**.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-145">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="e4aeb-146">Développez **Modèles**, puis sélectionnez **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="e4aeb-147">Dans cette procédure pas à pas, vous utilisez C#, mais vous pouvez utiliser un autre langage .NET.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="e4aeb-148">Sélectionnez **Application Console** à partir de la liste hello des types de projets sur hello droite.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-148">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="e4aeb-149">Entrez **DataFactoryAPITestApp** pour hello nom.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-149">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="e4aeb-150">Sélectionnez **C:\ADFGetStarted** pour hello emplacement.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-150">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="e4aeb-151">Cliquez sur **OK** projet hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-151">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="e4aeb-152">Cliquez sur **outils**, pointez trop**Gestionnaire de Package NuGet**, puis cliquez sur **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-152">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="e4aeb-153">Bonjour **Package Manager Console**, hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e4aeb-153">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="e4aeb-154">Exécutez hello suivant du package de fabrique de données tooinstall de commande :`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="e4aeb-154">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="e4aeb-155">Exécutez hello suivant du package d’Azure Active Directory tooinstall commandes (vous utilisez les API d’Active Directory dans le code hello) :`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="e4aeb-155">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="e4aeb-156">Remplacez le contenu hello de **App.config** fichier projet hello avec hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="e4aeb-156">Replace hello contents of **App.config** file in hello project with hello following content:</span></span> 
    
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
5. <span data-ttu-id="e4aeb-157">Dans le fichier App.Config hello, mettre à jour les valeurs de  **&lt;ID d’Application&gt;**,  **&lt;mot de passe&gt;**,  **&lt; ID d’abonnement&gt;**, et  **&lt;ID de locataire&gt;**  avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-157">In hello App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="e4aeb-158">Ajoutez hello suivant **à l’aide de** instructions toohello **Program.cs** fichier hello projet.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-158">Add hello following **using** statements toohello **Program.cs** file in hello project.</span></span>

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
6. <span data-ttu-id="e4aeb-159">Ajouter hello suivant le code qui crée une instance de **DataPipelineManagementClient** classe toohello **Main** (méthode).</span><span class="sxs-lookup"><span data-stu-id="e4aeb-159">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="e4aeb-160">Vous utilisez cette toocreate objet une fabrique de données, un service lié, les jeux de données d’entrée et de sortie et un pipeline.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-160">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="e4aeb-161">Vous montre également comment utiliser cet objet toomonitor de plusieurs secteurs un jeu de données lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-161">You also use this object toomonitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="e4aeb-162">Remplacez la valeur hello **resourceGroupName** avec nom hello de votre groupe de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-162">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span> <span data-ttu-id="e4aeb-163">Vous pouvez créer un groupe de ressources à l’aide de hello [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-163">You can create a resource group using hello [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="e4aeb-164">Nom de la mise à jour de hello données fabrique (dataFactoryName) toobe unique.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-164">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="e4aeb-165">Nom de la fabrique de données hello doit être globalement unique.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-165">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="e4aeb-166">Consultez la rubrique [Data Factory - Règles d'affectation des noms](data-factory-naming-rules.md) pour savoir comment nommer les artefacts Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="e4aeb-167">Ajouter hello suivant le code qui crée un **fabrique de données** toohello **Main** (méthode).</span><span class="sxs-lookup"><span data-stu-id="e4aeb-167">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

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
8. <span data-ttu-id="e4aeb-168">Ajouter hello suivant le code qui crée un **service lié Azure Storage** toohello **Main** (méthode).</span><span class="sxs-lookup"><span data-stu-id="e4aeb-168">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="e4aeb-169">Remplacez **storageaccountname** et **accountkey** par le nom et la clé de votre compte Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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
9. <span data-ttu-id="e4aeb-170">Ajouter hello suivant le code qui crée **jeux de données d’entrée et de sortie** toohello **Main** (méthode).</span><span class="sxs-lookup"><span data-stu-id="e4aeb-170">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

    <span data-ttu-id="e4aeb-171">Hello **FolderPath** d’objet blob d’entrée de hello est défini trop**adftutorial /** où **adftutorial** est le nom hello du conteneur de hello dans votre stockage d’objets blob.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-171">hello **FolderPath** for hello input blob is set too**adftutorial/** where **adftutorial** is hello name of hello container in your blob storage.</span></span> <span data-ttu-id="e4aeb-172">Si ce conteneur n’existe pas dans votre stockage d’objets blob Azure, créer un conteneur portant ce nom : **adftutorial** et télécharger un conteneur de toohello du fichier texte.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file toohello container.</span></span>

    <span data-ttu-id="e4aeb-173">Hello FolderPath pour hello blob a la valeur de sortie : **adftutorial/apifactoryoutput / {Slice}** où **tranche** est la valeur calculée dynamiquement hello selon **SliceStart**(début de date et heure de chaque secteur).</span><span class="sxs-lookup"><span data-stu-id="e4aeb-173">hello FolderPath for hello output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on hello value of **SliceStart** (start date-time of each slice.)</span></span>

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
10. <span data-ttu-id="e4aeb-174">Ajoutez le code suivant de hello **crée et Active un pipeline** toohello **Main** (méthode).</span><span class="sxs-lookup"><span data-stu-id="e4aeb-174">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="e4aeb-175">Ce pipeline dispose d’une fonction **CopyActivity** qui accepte **BlobSource** en tant que source et **BlobSink** en tant que récepteur.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="e4aeb-176">Activité de copie de Hello effectue le déplacement des données de hello dans Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-176">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="e4aeb-177">activité Hello est rendue possible par un service globalement disponible qui permettre copier des données entre différentes banques de données de manière sécurisée, fiable et évolutive.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-177">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="e4aeb-178">Consultez [les activités de déplacement des données](data-factory-data-movement-activities.md) article pour plus d’informations sur l’activité de copie de hello.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

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
    
                // Initial value for pipeline's active period. With this, you won't need tooset slice status
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
12. <span data-ttu-id="e4aeb-179">Ajouter hello suivant code toohello **Main** jeu de données de sortie de statut de hello tooget de méthode d’une tranche de données de hello.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-179">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="e4aeb-180">Une seule tranche est attendue dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-180">There is only one slice expected in this sample.</span></span>

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
13. <span data-ttu-id="e4aeb-181">**(facultatif)**  Tooget exécuter les détails pour un toohello de tranche de données de code suivant de hello ajouter **Main** (méthode).</span><span class="sxs-lookup"><span data-stu-id="e4aeb-181">**(optional)** Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

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
    
    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```
14. <span data-ttu-id="e4aeb-182">Ajouter hello suivant la méthode d’assistance utilisée par hello **principal** méthode toohello **programme** classe.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-182">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span> <span data-ttu-id="e4aeb-183">Cette méthode affiche une boîte de dialogue qui vous permet de fournir **nom d’utilisateur** et **mot de passe** utiliser toolog dans tooAzure portal.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use toolog in tooAzure portal.</span></span>

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

15. <span data-ttu-id="e4aeb-184">Bonjour l’Explorateur de solutions, développez le projet de hello : **DataFactoryAPITestApp**, avec le bouton droit **références**, puis cliquez sur **ajouter une référence**.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-184">In hello Solution Explorer, expand hello project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="e4aeb-185">Cochez la case pour l’assembly `System.Configuration` et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="e4aeb-186">Créer une application de console hello.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-186">Build hello console application.</span></span> <span data-ttu-id="e4aeb-187">Cliquez sur **générer** sur hello menu et cliquez sur **générer la Solution**.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-187">Click **Build** on hello menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="e4aeb-188">Vérifiez qu’est au moins un fichier dans le conteneur d’adftutorial hello dans votre stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-188">Confirm that there is at least one file in hello adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="e4aeb-189">Si ce n’est pas le cas, créer à Emp.txt fichier dans le bloc-notes avec hello suivant contenu et le télécharger toohello adftutorial conteneur.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-189">If not, create Emp.txt file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="e4aeb-190">Exécuter l’exemple hello en cliquant sur **déboguer** -> **démarrer le débogage** menu hello.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-190">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="e4aeb-191">Lorsque vous consultez hello **détails d’une tranche de données mise en route de l’exécution**, attendez quelques minutes, puis appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-191">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="e4aeb-192">Utilisez hello tooverify portail Azure cette fabrique de données hello **APITutorialFactory** est créée avec hello suivant artefacts :</span><span class="sxs-lookup"><span data-stu-id="e4aeb-192">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
    * <span data-ttu-id="e4aeb-193">Service lié : **AzureStorageLinkedService**</span><span class="sxs-lookup"><span data-stu-id="e4aeb-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="e4aeb-194">Jeu de données : **DatasetBlobSource** et **DatasetBlobDestination**.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="e4aeb-195">Pipeline : **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="e4aeb-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="e4aeb-196">Vérifiez qu’un fichier de sortie est créé dans hello **apifactoryoutput** dossier Bonjour **adftutorial** conteneur.</span><span class="sxs-lookup"><span data-stu-id="e4aeb-196">Verify that an output file is created in hello **apifactoryoutput** folder in hello **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="e4aeb-197">Obtenir une liste des tranches de données en échec</span><span class="sxs-lookup"><span data-stu-id="e4aeb-197">Get a list of failed data slices</span></span> 

```csharp
// Parse hello resource path
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

## <a name="next-steps"></a><span data-ttu-id="e4aeb-198">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e4aeb-198">Next steps</span></span>
<span data-ttu-id="e4aeb-199">Consultez hello exemple pour la création d’un pipeline à l’aide du Kit de développement logiciel .NET qui copie les données à partir d’une base de données SQL Azure de tooan stockage blob Azure suivant :</span><span class="sxs-lookup"><span data-stu-id="e4aeb-199">See hello following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage tooan Azure SQL database:</span></span> 

- [<span data-ttu-id="e4aeb-200">Créer un pipeline de données de toocopy de tooSQL de stockage d’objets Blob de base de données</span><span class="sxs-lookup"><span data-stu-id="e4aeb-200">Create a pipeline toocopy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
