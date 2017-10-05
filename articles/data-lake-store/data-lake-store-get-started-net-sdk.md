---
title: "Utiliser le Kit de développement logiciel (SDK) .NET pour développer des applications dans Azure Data Lake Store | Microsoft Docs"
description: "Utiliser le Kit de développement logiciel (SDK) .NET Azure Data Lake Store pour créer un compte Data Lake Store et effectuer des opérations de base dans Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ea57d5a9-2929-4473-9d30-08227912aba7
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: nitinme
ms.openlocfilehash: 70f94a07b0102e3135eaf85e5877e3502762d7e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a><span data-ttu-id="a49e7-103">Prise en main d’Azure Data Lake Store à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="a49e7-103">Get started with Azure Data Lake Store using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a49e7-104">Portail</span><span class="sxs-lookup"><span data-stu-id="a49e7-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="a49e7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a49e7-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="a49e7-106">Kit SDK .NET</span><span class="sxs-lookup"><span data-stu-id="a49e7-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="a49e7-107">Kit SDK Java</span><span class="sxs-lookup"><span data-stu-id="a49e7-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="a49e7-108">API REST</span><span class="sxs-lookup"><span data-stu-id="a49e7-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="a49e7-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a49e7-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="a49e7-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="a49e7-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="a49e7-111">Python</span><span class="sxs-lookup"><span data-stu-id="a49e7-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="a49e7-112">Découvrez comment utiliser le [Kit de développement logiciel (SDK) .NET Azure Data Lake Store](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) pour effectuer des opérations de base comme créer des dossiers ou charger et télécharger des fichiers de données. Pour plus d’informations sur Data Lake, consultez [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a49e7-112">Learn how to use the [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a49e7-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a49e7-113">Prerequisites</span></span>
* <span data-ttu-id="a49e7-114">**Visual Studio 2013, 2015 ou 2017**.</span><span class="sxs-lookup"><span data-stu-id="a49e7-114">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="a49e7-115">Les instructions ci-dessous utilisent Visual Studio 2015 Update 2.</span><span class="sxs-lookup"><span data-stu-id="a49e7-115">The instructions below use Visual Studio 2015 Update 2.</span></span>

* <span data-ttu-id="a49e7-116">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="a49e7-116">**An Azure subscription**.</span></span> <span data-ttu-id="a49e7-117">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a49e7-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="a49e7-118">**Compte Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="a49e7-118">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="a49e7-119">Pour savoir comment créer un compte, consultez [Prise en main d’Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a49e7-119">For instructions on how to create an account, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

* <span data-ttu-id="a49e7-120">**Créez une application Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a49e7-120">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="a49e7-121">Vous utilisez l’application Azure AD pour authentifier l’application Data Lake Store auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a49e7-121">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="a49e7-122">Il existe différentes approches pour l’authentification auprès d’Azure AD : **authentification de l’utilisateur final** ou **authentification de service à service**.</span><span class="sxs-lookup"><span data-stu-id="a49e7-122">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="a49e7-123">Pour obtenir des instructions et plus d’informations sur l’authentification, consultez [l’authentification de l’utilisateur final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [l’authentification de service à service](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="a49e7-123">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="a49e7-124">Créer une application .NET</span><span class="sxs-lookup"><span data-stu-id="a49e7-124">Create a .NET application</span></span>
1. <span data-ttu-id="a49e7-125">Ouvrez Visual Studio et créez une application console.</span><span class="sxs-lookup"><span data-stu-id="a49e7-125">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="a49e7-126">Dans le menu **Fichier**, cliquez sur **Nouveau**, puis sur **Projet**.</span><span class="sxs-lookup"><span data-stu-id="a49e7-126">From the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="a49e7-127">Dans **Nouveau projet**, entrez ou sélectionnez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="a49e7-127">From **New Project**, type or select the following values:</span></span>

   | <span data-ttu-id="a49e7-128">Propriété</span><span class="sxs-lookup"><span data-stu-id="a49e7-128">Property</span></span> | <span data-ttu-id="a49e7-129">Valeur</span><span class="sxs-lookup"><span data-stu-id="a49e7-129">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="a49e7-130">Catégorie</span><span class="sxs-lookup"><span data-stu-id="a49e7-130">Category</span></span> |<span data-ttu-id="a49e7-131">Modèles/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="a49e7-131">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="a49e7-132">Modèle</span><span class="sxs-lookup"><span data-stu-id="a49e7-132">Template</span></span> |<span data-ttu-id="a49e7-133">Application console</span><span class="sxs-lookup"><span data-stu-id="a49e7-133">Console Application</span></span> |
   | <span data-ttu-id="a49e7-134">Nom</span><span class="sxs-lookup"><span data-stu-id="a49e7-134">Name</span></span> |<span data-ttu-id="a49e7-135">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="a49e7-135">CreateADLApplication</span></span> |
4. <span data-ttu-id="a49e7-136">Cliquez sur **OK** pour créer le projet.</span><span class="sxs-lookup"><span data-stu-id="a49e7-136">Click **OK** to create the project.</span></span>
5. <span data-ttu-id="a49e7-137">Ajoutez les packages Nuget à votre projet.</span><span class="sxs-lookup"><span data-stu-id="a49e7-137">Add the Nuget packages to your project.</span></span>

   1. <span data-ttu-id="a49e7-138">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le nom du projet, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a49e7-138">Right-click the project name in the Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="a49e7-139">Dans l’onglet **Gestionnaire de package NuGet**, vérifiez que **Source du package** a la valeur **nuget.org** et que la case **Inclure la version préliminaire** est cochée.</span><span class="sxs-lookup"><span data-stu-id="a49e7-139">In the **Nuget Package Manager** tab, make sure that **Package source** is set to **nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="a49e7-140">Recherchez et installez les packages NuGet suivants :</span><span class="sxs-lookup"><span data-stu-id="a49e7-140">Search for and install the following NuGet packages:</span></span>

      * <span data-ttu-id="a49e7-141">`Microsoft.Azure.Management.DataLake.Store` - Ce didacticiel utilise v2.1.3-preview.</span><span class="sxs-lookup"><span data-stu-id="a49e7-141">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span></span>
      * <span data-ttu-id="a49e7-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - Ce didacticiel utilise v2.2.12.</span><span class="sxs-lookup"><span data-stu-id="a49e7-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span></span>

        <span data-ttu-id="a49e7-143">![Ajouter une source Nuget](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Créer un compte Azure Data Lake")</span><span class="sxs-lookup"><span data-stu-id="a49e7-143">![Add a Nuget source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span></span>
   4. <span data-ttu-id="a49e7-144">Fermez le **Gestionnaire de package NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a49e7-144">Close the **Nuget Package Manager**.</span></span>
6. <span data-ttu-id="a49e7-145">Ouvrez **Program.cs**, supprimez le code existant, puis insérez les instructions suivantes pour ajouter des références aux espaces de noms.</span><span class="sxs-lookup"><span data-stu-id="a49e7-145">Open **Program.cs**, delete the existing code, and then include the following statements to add references to namespaces.</span></span>

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. <span data-ttu-id="a49e7-146">Déclarez les variables comme indiqué ci-dessous et indiquez les valeurs pour le nom du Data Lake Store et le nom du groupe de ressources qui existent déjà.</span><span class="sxs-lookup"><span data-stu-id="a49e7-146">Declare the variables as shown below, and provide the values for Data Lake Store name and the resource group name that already exist.</span></span> <span data-ttu-id="a49e7-147">En outre, assurez-vous que le chemin d'accès local et le nom de fichier que vous fournissez ici existent sur l'ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a49e7-147">Also, make sure the local path and file name you provide here must exist on the computer.</span></span> <span data-ttu-id="a49e7-148">Ajoutez l'extrait de code suivant après les déclarations d'espace de noms.</span><span class="sxs-lookup"><span data-stu-id="a49e7-148">Add the following code snippet after the namespace declarations.</span></span>

        namespace SdkSample
        {
            class Program
            {
                private static DataLakeStoreAccountManagementClient _adlsClient;
                private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;

                private static string _adlsAccountName;
                private static string _resourceGroupName;
                private static string _location;
                private static string _subId;

                private static void Main(string[] args)
                {
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with the name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with the name of the resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

<span data-ttu-id="a49e7-149">Dans les sections suivantes de cet article, vous pouvez découvrir comment utiliser les méthodes .NET pour effectuer des opérations telles que l’authentification des utilisateurs et le chargement de fichiers.</span><span class="sxs-lookup"><span data-stu-id="a49e7-149">In the remaining sections of the article, you can see how to use the available .NET methods to perform operations such as authentication, file upload, etc.</span></span>

## <a name="authentication"></a><span data-ttu-id="a49e7-150">Authentification</span><span class="sxs-lookup"><span data-stu-id="a49e7-150">Authentication</span></span>

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a><span data-ttu-id="a49e7-151">Si vous utilisez l’authentification de l’utilisateur final (recommandée pour ce didacticiel)</span><span class="sxs-lookup"><span data-stu-id="a49e7-151">If you are using end-user authentication (recommended for this tutorial)</span></span>

<span data-ttu-id="a49e7-152">Utilisez-le avec une application native Azure AD pour authentifier votre application **interactivement**, ce qui signifie que vous devrez entrer vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="a49e7-152">Use this with an existing Azure AD native application to authenticate your application **interactively**, which means you will be prompted to enter your Azure credentials.</span></span>

<span data-ttu-id="a49e7-153">Pour simplifier l’utilisation, l’extrait de code ci-dessous utilise les valeurs par défaut pour l’ID client et l’URI de redirection qui fonctionne avec n’importe quel abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="a49e7-153">For ease of use, the snippet below uses default values for client ID and redirect URI that will work with any Azure subscription.</span></span> <span data-ttu-id="a49e7-154">Pour effectuer ce didacticiel plus rapidement, nous vous recommandons d’utiliser cette approche.</span><span class="sxs-lookup"><span data-stu-id="a49e7-154">To help you complete this tutorial faster, we recommend you use this approach.</span></span> <span data-ttu-id="a49e7-155">Dans l’extrait de code ci-dessous, fournissez simplement la valeur de votre ID locataire.</span><span class="sxs-lookup"><span data-stu-id="a49e7-155">In the snippet below, just provide the value for your tenant ID.</span></span> <span data-ttu-id="a49e7-156">Vous pouvez les récupérer en suivant les instructions fournies sur la page [Créer une Application Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="a49e7-156">You can retrieve it using the instructions provided at [Create an Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

    // User login via interactive popup
    // Use the client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with the user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

<span data-ttu-id="a49e7-157">Voici quelques informations utiles concernant l’extrait de code ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="a49e7-157">A couple of things to know about this snippet above:</span></span>

* <span data-ttu-id="a49e7-158">Pour vous aider à effectuer le didacticiel plus rapidement, l’extrait de code ci-dessus utilise un domaine et un ID client Azure AD qui sont disponibles par défaut pour tous les abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="a49e7-158">To help you complete the tutorial faster, this snippet uses an an Azure AD domain and client ID that is available by default for all Azure subscriptions.</span></span> <span data-ttu-id="a49e7-159">Vous pouvez donc **utiliser cet extrait de code en l’état dans votre application**.</span><span class="sxs-lookup"><span data-stu-id="a49e7-159">So, you can **use this snippet as-is in your application**.</span></span>
* <span data-ttu-id="a49e7-160">Cependant, si vous souhaitez utiliser votre propre ID client application et domaine Azure AD, vous devez créer une application native Azure AD, puis utiliser l’ID locataire, l’ID client et l’URI de redirection Azure AD de l’application que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="a49e7-160">However, if you do want to use your own Azure AD domain and application client ID, you must create an Azure AD native application and then use the Azure AD tenant ID, client ID, and redirect URI for the application you created.</span></span> <span data-ttu-id="a49e7-161">Consultez la page [créer une Application Active Directory pour l’authentification de l’utilisateur final avec Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) pour obtenir des instructions.</span><span class="sxs-lookup"><span data-stu-id="a49e7-161">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span></span>

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a><span data-ttu-id="a49e7-162">Si vous utilisez l’authentification de service à service avec une clé secrète client</span><span class="sxs-lookup"><span data-stu-id="a49e7-162">If you are using service-to-service authentication with client secret</span></span>
<span data-ttu-id="a49e7-163">Vous pouvez faire appel à l’extrait de code suivant pour authentifier votre application en mode **non interactif**, en utilisant la clé secrète du client pour une application/un principal du service.</span><span class="sxs-lookup"><span data-stu-id="a49e7-163">The following snippet can be used to authenticate your application **non-interactively**, using the client secret / key for an application / service principal.</span></span> <span data-ttu-id="a49e7-164">Utilisez-le avec une « application web » Azure AD existante.</span><span class="sxs-lookup"><span data-stu-id="a49e7-164">Use this with an existing Azure AD "Web App" Application.</span></span> <span data-ttu-id="a49e7-165">Pour obtenir des instructions sur la création de l’application web Azure AD et comment récupérer l’ID et la clé secrète du client requis dans l’extrait de code ci-dessous, consultez la page [Créer une Application Active Directory pour l’authentification de service à service avec Data Lake Store](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="a49e7-165">For instructions on how to create the Azure AD web application and how to retrieve the client ID and client secret required in the snippet below, see [Create an Active Directory Application for service-to-service authentication with Data Lake Store](data-lake-store-authenticate-using-active-directory.md).</span></span>

    // Service principal / appplication authentication with client secret / key
    // Use the client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a><span data-ttu-id="a49e7-166">Si vous utilisez l’authentification de service à service avec un certificat</span><span class="sxs-lookup"><span data-stu-id="a49e7-166">If you are using service-to-service authentication with certificate</span></span>

<span data-ttu-id="a49e7-167">Vous pouvez également, utiliser l’extrait de code pour authentifier votre application en mode **non interactif**, en utilisant le certificat pour une application Azure Active Directory/un principal de service.</span><span class="sxs-lookup"><span data-stu-id="a49e7-167">As a third option, the following snippet can be used to authenticate your application **non-interactively**, using the certificate for an Azure Active Directory application / service principal.</span></span> <span data-ttu-id="a49e7-168">Utilisez-le avec une [Application Azure AD existante dotée de certificats](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="a49e7-168">Use this with an existing [Azure AD Application with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    // Service principal / application authentication with certificate
    // Use the client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a><span data-ttu-id="a49e7-169">Créer des objets clients</span><span class="sxs-lookup"><span data-stu-id="a49e7-169">Create client objects</span></span>
<span data-ttu-id="a49e7-170">L’extrait de code suivant crée le compte Data Lake Store et les objets clients filesystem, qui sont utilisés pour adresser des demandes au service.</span><span class="sxs-lookup"><span data-stu-id="a49e7-170">The following snippet creates the Data Lake Store account and filesystem client objects, which are used to issue requests to the service.</span></span>

    // Create client objects and set the subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a><span data-ttu-id="a49e7-171">Répertorier tous les comptes Data Lake Store d’un abonnement</span><span class="sxs-lookup"><span data-stu-id="a49e7-171">List all Data Lake Store accounts within a subscription</span></span>
<span data-ttu-id="a49e7-172">L’extrait de code suivant répertorie tous les comptes Data Lake Store d’un abonnement Azure donné.</span><span class="sxs-lookup"><span data-stu-id="a49e7-172">The following snippet lists all Data Lake Store accounts within a given Azure subscription.</span></span>

    // List all ADLS accounts within the subscription
    public static async Task<List<DataLakeStoreAccount>> ListAdlStoreAccounts()
    {
        var response = await _adlsClient.Account.ListAsync();
        var accounts = new List<DataLakeStoreAccount>(response);

        while (response.NextPageLink != null)
        {
            response = _adlsClient.Account.ListNext(response.NextPageLink);
            accounts.AddRange(response);
        }

        return accounts;
    }

## <a name="create-a-directory"></a><span data-ttu-id="a49e7-173">Créer un répertoire</span><span class="sxs-lookup"><span data-stu-id="a49e7-173">Create a directory</span></span>
<span data-ttu-id="a49e7-174">L’extrait de code suivant montre une méthode `CreateDirectory` que vous pouvez utiliser pour créer un répertoire dans un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a49e7-174">The following snippet shows a `CreateDirectory` method that you can use to create a directory within a Data Lake Store account.</span></span>

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a><span data-ttu-id="a49e7-175">Charger un fichier</span><span class="sxs-lookup"><span data-stu-id="a49e7-175">Upload a file</span></span>
<span data-ttu-id="a49e7-176">L’extrait de code suivant montre une méthode `UploadFile` que vous pouvez utiliser pour charger des fichiers vers un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a49e7-176">The following snippet shows an `UploadFile` method that you can use to upload files to a Data Lake Store account.</span></span>

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

<span data-ttu-id="a49e7-177">Le kit de développement logiciel (SDK) prend en charge le chargement et le téléchargement récursifs entre un chemin d’accès local et un chemin d’accès Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a49e7-177">The SDK supports recursive upload and download between a local file path and a Data Lake Store file path.</span></span>    

## <a name="get-file-or-directory-info"></a><span data-ttu-id="a49e7-178">Obtenir des informations sur un fichier ou répertoire</span><span class="sxs-lookup"><span data-stu-id="a49e7-178">Get file or directory info</span></span>
<span data-ttu-id="a49e7-179">L’extrait de code suivant montre une méthode `GetItemInfo` que vous pouvez utiliser pour récupérer des informations sur un fichier ou un répertoire disponibles dans Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a49e7-179">The following snippet shows a `GetItemInfo` method that you can use to retrieve information about a file or directory available in Data Lake Store.</span></span>

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a><span data-ttu-id="a49e7-180">Répertorier des fichiers ou répertoires</span><span class="sxs-lookup"><span data-stu-id="a49e7-180">List file or directories</span></span>
<span data-ttu-id="a49e7-181">L’extrait de code suivant montre une méthode `ListItem` que vous pouvez utiliser pour répertorier les fichiers et répertoires dans un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a49e7-181">The following snippet shows a `ListItem` method that can use to list the file and directories in a Data Lake Store account.</span></span>

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a><span data-ttu-id="a49e7-182">Concaténation de fichiers</span><span class="sxs-lookup"><span data-stu-id="a49e7-182">Concatenate files</span></span>
<span data-ttu-id="a49e7-183">L’extrait de code suivant montre une méthode `ConcatenateFiles` qui vous permet de concaténer des fichiers.</span><span class="sxs-lookup"><span data-stu-id="a49e7-183">The following snippet shows a `ConcatenateFiles` method that you use to concatenate files.</span></span>

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-to-a-file"></a><span data-ttu-id="a49e7-184">Ajout à un fichier</span><span class="sxs-lookup"><span data-stu-id="a49e7-184">Append to a file</span></span>
<span data-ttu-id="a49e7-185">L’extrait de code suivant montre une méthode `AppendToFile` qui permet d’ajouter des données à un fichier déjà stocké dans un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a49e7-185">The following snippet shows a `AppendToFile` method that you use append data to a file already stored in a Data Lake Store account.</span></span>

    // Append to file
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a><span data-ttu-id="a49e7-186">Téléchargement d’un fichier</span><span class="sxs-lookup"><span data-stu-id="a49e7-186">Download a file</span></span>
<span data-ttu-id="a49e7-187">L’extrait de code suivant montre une méthode `DownloadFile` que vous pouvez utiliser pour télécharger un fichier depuis un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a49e7-187">The following snippet shows a `DownloadFile` method that you use to download a file from a Data Lake Store account.</span></span>

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a><span data-ttu-id="a49e7-188">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a49e7-188">Next steps</span></span>
* [<span data-ttu-id="a49e7-189">Sécuriser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a49e7-189">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="a49e7-190">Utiliser Azure Data Lake Analytics avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a49e7-190">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="a49e7-191">Utiliser Azure HDInsight avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a49e7-191">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="a49e7-192">Data Lake Store .NET SDK Reference (Informations de référence sur le Kit de développement logiciel (SDK) .NET Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="a49e7-192">Data Lake Store .NET SDK Reference</span></span>](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [<span data-ttu-id="a49e7-193">Data Lake Store REST Reference (Informations de référence sur les API REST Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="a49e7-193">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
