---
title: "les applications de toodevelop du Kit de développement .NET aaaUse hello dans Azure Data Lake Store | Documents Microsoft"
description: "Utilisez Azure Data Lake Store .NET SDK toocreate un compte Data Lake Store et effectuer des opérations de base Bonjour Data Lake Store"
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
ms.openlocfilehash: cb3a1dfb2f6379f728069d66b0ee77ce0f838fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a><span data-ttu-id="e594c-103">Prise en main d’Azure Data Lake Store à l’aide du Kit de développement logiciel (SDK) .NET</span><span class="sxs-lookup"><span data-stu-id="e594c-103">Get started with Azure Data Lake Store using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e594c-104">Portail</span><span class="sxs-lookup"><span data-stu-id="e594c-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="e594c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e594c-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="e594c-106">Kit SDK .NET</span><span class="sxs-lookup"><span data-stu-id="e594c-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="e594c-107">Kit SDK Java</span><span class="sxs-lookup"><span data-stu-id="e594c-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="e594c-108">API REST</span><span class="sxs-lookup"><span data-stu-id="e594c-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="e594c-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e594c-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="e594c-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="e594c-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="e594c-111">Python</span><span class="sxs-lookup"><span data-stu-id="e594c-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="e594c-112">Découvrez comment toouse hello [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform les opérations de base telles que créer des dossiers, télécharger et télécharger les fichiers de données, etc.. Pour plus d’informations sur Data Lake, consultez [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e594c-112">Learn how toouse hello [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e594c-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e594c-113">Prerequisites</span></span>
* <span data-ttu-id="e594c-114">**Visual Studio 2013, 2015 ou 2017**.</span><span class="sxs-lookup"><span data-stu-id="e594c-114">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="e594c-115">instructions de Hello ci-dessous utilisent Visual Studio 2015 Update 2.</span><span class="sxs-lookup"><span data-stu-id="e594c-115">hello instructions below use Visual Studio 2015 Update 2.</span></span>

* <span data-ttu-id="e594c-116">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="e594c-116">**An Azure subscription**.</span></span> <span data-ttu-id="e594c-117">Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e594c-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="e594c-118">**Compte Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="e594c-118">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="e594c-119">Pour obtenir des instructions sur la façon de toocreate un compte, consultez [prise en main Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e594c-119">For instructions on how toocreate an account, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

* <span data-ttu-id="e594c-120">**Créez une application Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e594c-120">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="e594c-121">Vous utilisez hello Azure AD tooauthenticate hello Data Lake Store une application avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e594c-121">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="e594c-122">Il existe tooauthenticate différentes approches avec Azure AD, qui sont **l’authentification de l’utilisateur final** ou **l’authentification de service**.</span><span class="sxs-lookup"><span data-stu-id="e594c-122">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="e594c-123">Pour plus d’informations sur la façon d’et tooauthenticate, consultez [l’authentification de l’utilisateur final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [l’authentification de service](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="e594c-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="e594c-124">Créer une application .NET</span><span class="sxs-lookup"><span data-stu-id="e594c-124">Create a .NET application</span></span>
1. <span data-ttu-id="e594c-125">Ouvrez Visual Studio et créez une application console.</span><span class="sxs-lookup"><span data-stu-id="e594c-125">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="e594c-126">À partir de hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**.</span><span class="sxs-lookup"><span data-stu-id="e594c-126">From hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="e594c-127">À partir de **nouveau projet**, tapez ou sélectionnez hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="e594c-127">From **New Project**, type or select hello following values:</span></span>

   | <span data-ttu-id="e594c-128">Propriété</span><span class="sxs-lookup"><span data-stu-id="e594c-128">Property</span></span> | <span data-ttu-id="e594c-129">Valeur</span><span class="sxs-lookup"><span data-stu-id="e594c-129">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="e594c-130">Catégorie</span><span class="sxs-lookup"><span data-stu-id="e594c-130">Category</span></span> |<span data-ttu-id="e594c-131">Modèles/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="e594c-131">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="e594c-132">Modèle</span><span class="sxs-lookup"><span data-stu-id="e594c-132">Template</span></span> |<span data-ttu-id="e594c-133">Application console</span><span class="sxs-lookup"><span data-stu-id="e594c-133">Console Application</span></span> |
   | <span data-ttu-id="e594c-134">Nom</span><span class="sxs-lookup"><span data-stu-id="e594c-134">Name</span></span> |<span data-ttu-id="e594c-135">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="e594c-135">CreateADLApplication</span></span> |
4. <span data-ttu-id="e594c-136">Cliquez sur **OK** projet hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="e594c-136">Click **OK** toocreate hello project.</span></span>
5. <span data-ttu-id="e594c-137">Ajoutez hello Nuget packages tooyour projet.</span><span class="sxs-lookup"><span data-stu-id="e594c-137">Add hello Nuget packages tooyour project.</span></span>

   1. <span data-ttu-id="e594c-138">Cliquez sur le nom de projet hello Bonjour l’Explorateur de solutions, puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e594c-138">Right-click hello project name in hello Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="e594c-139">Bonjour **Gestionnaire de Package Nuget** onglet, vérifiez que **source du Package** est défini trop**nuget.org** et **inclure la version préliminaire** case à cocher est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="e594c-139">In hello **Nuget Package Manager** tab, make sure that **Package source** is set too**nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="e594c-140">Rechercher et installer hello suivant les packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="e594c-140">Search for and install hello following NuGet packages:</span></span>

      * <span data-ttu-id="e594c-141">`Microsoft.Azure.Management.DataLake.Store` - Ce didacticiel utilise v2.1.3-preview.</span><span class="sxs-lookup"><span data-stu-id="e594c-141">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span></span>
      * <span data-ttu-id="e594c-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - Ce didacticiel utilise v2.2.12.</span><span class="sxs-lookup"><span data-stu-id="e594c-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span></span>

        <span data-ttu-id="e594c-143">![Ajouter une source Nuget](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Créer un compte Azure Data Lake")</span><span class="sxs-lookup"><span data-stu-id="e594c-143">![Add a Nuget source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span></span>
   4. <span data-ttu-id="e594c-144">Fermer hello **Gestionnaire de Package Nuget**.</span><span class="sxs-lookup"><span data-stu-id="e594c-144">Close hello **Nuget Package Manager**.</span></span>
6. <span data-ttu-id="e594c-145">Ouvrez **Program.cs**, supprimer le code existant de hello et ensuite inclure hello suivant les instructions tooadd références toonamespaces.</span><span class="sxs-lookup"><span data-stu-id="e594c-145">Open **Program.cs**, delete hello existing code, and then include hello following statements tooadd references toonamespaces.</span></span>

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. <span data-ttu-id="e594c-146">Déclarer des variables hello comme indiqué ci-dessous et fournir les valeurs de hello pour nom Data Lake Store et le nom de groupe de ressources hello qui existent déjà.</span><span class="sxs-lookup"><span data-stu-id="e594c-146">Declare hello variables as shown below, and provide hello values for Data Lake Store name and hello resource group name that already exist.</span></span> <span data-ttu-id="e594c-147">Assurez-vous également que nom de chemin d’accès et le fichier local hello que vous fournissez ici doit exister sur l’ordinateur de hello.</span><span class="sxs-lookup"><span data-stu-id="e594c-147">Also, make sure hello local path and file name you provide here must exist on hello computer.</span></span> <span data-ttu-id="e594c-148">Ajoutez hello suivant extrait de code après les déclarations d’espace de noms hello.</span><span class="sxs-lookup"><span data-stu-id="e594c-148">Add hello following code snippet after hello namespace declarations.</span></span>

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
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with hello name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with hello name of hello resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

<span data-ttu-id="e594c-149">Bonjour restant des sections de hello article, vous pouvez voir comment toouse hello opérations tooperform de méthodes .NET disponibles telles que l’authentification, le transfert des fichiers, etc..</span><span class="sxs-lookup"><span data-stu-id="e594c-149">In hello remaining sections of hello article, you can see how toouse hello available .NET methods tooperform operations such as authentication, file upload, etc.</span></span>

## <a name="authentication"></a><span data-ttu-id="e594c-150">Authentification</span><span class="sxs-lookup"><span data-stu-id="e594c-150">Authentication</span></span>

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a><span data-ttu-id="e594c-151">Si vous utilisez l’authentification de l’utilisateur final (recommandée pour ce didacticiel)</span><span class="sxs-lookup"><span data-stu-id="e594c-151">If you are using end-user authentication (recommended for this tutorial)</span></span>

<span data-ttu-id="e594c-152">Utiliser votre application avec une tooauthenticate d’application native Azure AD existant **interactivement**, qui signifie que vous serez invité à tooenter vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="e594c-152">Use this with an existing Azure AD native application tooauthenticate your application **interactively**, which means you will be prompted tooenter your Azure credentials.</span></span>

<span data-ttu-id="e594c-153">Facilité d’utilisation, extrait hello ci-dessous utilise les valeurs par défaut pour l’ID client et l’URI qui fonctionne avec n’importe quel abonnement Azure de redirection.</span><span class="sxs-lookup"><span data-stu-id="e594c-153">For ease of use, hello snippet below uses default values for client ID and redirect URI that will work with any Azure subscription.</span></span> <span data-ttu-id="e594c-154">toohelp accélère ce didacticiel, nous vous recommandons de qu'utiliser cette approche.</span><span class="sxs-lookup"><span data-stu-id="e594c-154">toohelp you complete this tutorial faster, we recommend you use this approach.</span></span> <span data-ttu-id="e594c-155">Dans l’extrait de code hello ci-dessous, simplement enrichir hello pour votre ID de client.</span><span class="sxs-lookup"><span data-stu-id="e594c-155">In hello snippet below, just provide hello value for your tenant ID.</span></span> <span data-ttu-id="e594c-156">Vous pouvez récupérer à l’aide d’instructions hello fournies au [créer une Application Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="e594c-156">You can retrieve it using hello instructions provided at [Create an Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

<span data-ttu-id="e594c-157">Quelques tooknow de choses sur cet extrait de code ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="e594c-157">A couple of things tooknow about this snippet above:</span></span>

* <span data-ttu-id="e594c-158">toohelp accélère didacticiel de hello, cet extrait de code utilise une une annonce Azure ID de domaine et le client qui est disponible par défaut pour tous les abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="e594c-158">toohelp you complete hello tutorial faster, this snippet uses an an Azure AD domain and client ID that is available by default for all Azure subscriptions.</span></span> <span data-ttu-id="e594c-159">Vous pouvez donc **utiliser cet extrait de code en l’état dans votre application**.</span><span class="sxs-lookup"><span data-stu-id="e594c-159">So, you can **use this snippet as-is in your application**.</span></span>
* <span data-ttu-id="e594c-160">Toutefois, si vous ne voulez que toouse votre propre domaine Azure AD et ID de client d’application, vous devez créer une application native d’Azure AD, utilisez hello Azure AD Client ID, ID de client, puis URI de redirection de l’application hello créé.</span><span class="sxs-lookup"><span data-stu-id="e594c-160">However, if you do want toouse your own Azure AD domain and application client ID, you must create an Azure AD native application and then use hello Azure AD tenant ID, client ID, and redirect URI for hello application you created.</span></span> <span data-ttu-id="e594c-161">Consultez la page [créer une Application Active Directory pour l’authentification de l’utilisateur final avec Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) pour obtenir des instructions.</span><span class="sxs-lookup"><span data-stu-id="e594c-161">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span></span>

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a><span data-ttu-id="e594c-162">Si vous utilisez l’authentification de service à service avec une clé secrète client</span><span class="sxs-lookup"><span data-stu-id="e594c-162">If you are using service-to-service authentication with client secret</span></span>
<span data-ttu-id="e594c-163">Hello suivant extrait de code peut être utilisé tooauthenticate votre application **non interactive**, à l’aide de la clé secrète du client hello / la clé pour un principal de l’application ou le service.</span><span class="sxs-lookup"><span data-stu-id="e594c-163">hello following snippet can be used tooauthenticate your application **non-interactively**, using hello client secret / key for an application / service principal.</span></span> <span data-ttu-id="e594c-164">Utilisez-le avec une « application web » Azure AD existante.</span><span class="sxs-lookup"><span data-stu-id="e594c-164">Use this with an existing Azure AD "Web App" Application.</span></span> <span data-ttu-id="e594c-165">Pour obtenir des instructions sur le mode d’application de web toocreate hello Azure AD et comment tooretrieve hello ID client et question secrète du client requis dans l’extrait de code hello ci-dessous, consultez [créer une Application Active Directory pour l’authentification de service avec des données Lake Store](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="e594c-165">For instructions on how toocreate hello Azure AD web application and how tooretrieve hello client ID and client secret required in hello snippet below, see [Create an Active Directory Application for service-to-service authentication with Data Lake Store](data-lake-store-authenticate-using-active-directory.md).</span></span>

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a><span data-ttu-id="e594c-166">Si vous utilisez l’authentification de service à service avec un certificat</span><span class="sxs-lookup"><span data-stu-id="e594c-166">If you are using service-to-service authentication with certificate</span></span>

<span data-ttu-id="e594c-167">Une troisième option, hello suivant extrait de code peut être utilisé tooauthenticate votre application **non interactive**, à l’aide du certificat de hello pour une application Azure Active Directory / principal de service.</span><span class="sxs-lookup"><span data-stu-id="e594c-167">As a third option, hello following snippet can be used tooauthenticate your application **non-interactively**, using hello certificate for an Azure Active Directory application / service principal.</span></span> <span data-ttu-id="e594c-168">Utilisez-le avec une [Application Azure AD existante dotée de certificats](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="e594c-168">Use this with an existing [Azure AD Application with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a><span data-ttu-id="e594c-169">Créer des objets clients</span><span class="sxs-lookup"><span data-stu-id="e594c-169">Create client objects</span></span>
<span data-ttu-id="e594c-170">Hello extrait de code suivant crée hello Data Lake Store compte et le système de fichiers objets de client, qui sont utilisées tooissue demande toohello service.</span><span class="sxs-lookup"><span data-stu-id="e594c-170">hello following snippet creates hello Data Lake Store account and filesystem client objects, which are used tooissue requests toohello service.</span></span>

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a><span data-ttu-id="e594c-171">Répertorier tous les comptes Data Lake Store d’un abonnement</span><span class="sxs-lookup"><span data-stu-id="e594c-171">List all Data Lake Store accounts within a subscription</span></span>
<span data-ttu-id="e594c-172">Hello extrait de code suivant répertorie tous les comptes Data Lake Store dans un abonnement Azure donné.</span><span class="sxs-lookup"><span data-stu-id="e594c-172">hello following snippet lists all Data Lake Store accounts within a given Azure subscription.</span></span>

    // List all ADLS accounts within hello subscription
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

## <a name="create-a-directory"></a><span data-ttu-id="e594c-173">Créer un répertoire</span><span class="sxs-lookup"><span data-stu-id="e594c-173">Create a directory</span></span>
<span data-ttu-id="e594c-174">Hello ci-dessous extrait de code illustre un `CreateDirectory` méthode que vous pouvez utiliser toocreate un répertoire au sein d’un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e594c-174">hello following snippet shows a `CreateDirectory` method that you can use toocreate a directory within a Data Lake Store account.</span></span>

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a><span data-ttu-id="e594c-175">Charger un fichier</span><span class="sxs-lookup"><span data-stu-id="e594c-175">Upload a file</span></span>
<span data-ttu-id="e594c-176">Hello ci-dessous extrait de code illustre un `UploadFile` compte Data Lake Store de tooa les fichiers que vous pouvez utiliser tooupload (méthode).</span><span class="sxs-lookup"><span data-stu-id="e594c-176">hello following snippet shows an `UploadFile` method that you can use tooupload files tooa Data Lake Store account.</span></span>

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

<span data-ttu-id="e594c-177">Hello SDK prend en charge le téléchargement entre un chemin d’accès local et un chemin d’accès du fichier Data Lake Store et récursive.</span><span class="sxs-lookup"><span data-stu-id="e594c-177">hello SDK supports recursive upload and download between a local file path and a Data Lake Store file path.</span></span>    

## <a name="get-file-or-directory-info"></a><span data-ttu-id="e594c-178">Obtenir des informations sur un fichier ou répertoire</span><span class="sxs-lookup"><span data-stu-id="e594c-178">Get file or directory info</span></span>
<span data-ttu-id="e594c-179">Hello ci-dessous extrait de code illustre un `GetItemInfo` méthode que vous pouvez utiliser tooretrieve d’informations sur un fichier ou répertoire disponible dans Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e594c-179">hello following snippet shows a `GetItemInfo` method that you can use tooretrieve information about a file or directory available in Data Lake Store.</span></span>

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a><span data-ttu-id="e594c-180">Répertorier des fichiers ou répertoires</span><span class="sxs-lookup"><span data-stu-id="e594c-180">List file or directories</span></span>
<span data-ttu-id="e594c-181">Hello ci-dessous extrait de code illustre un `ListItem` méthode qui permet de toolist hello fichiers et répertoires dans un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e594c-181">hello following snippet shows a `ListItem` method that can use toolist hello file and directories in a Data Lake Store account.</span></span>

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a><span data-ttu-id="e594c-182">Concaténation de fichiers</span><span class="sxs-lookup"><span data-stu-id="e594c-182">Concatenate files</span></span>
<span data-ttu-id="e594c-183">Hello ci-dessous extrait de code illustre un `ConcatenateFiles` méthode que vous utilisez des fichiers de tooconcatenate.</span><span class="sxs-lookup"><span data-stu-id="e594c-183">hello following snippet shows a `ConcatenateFiles` method that you use tooconcatenate files.</span></span>

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a><span data-ttu-id="e594c-184">Ajout d’un fichier tooa</span><span class="sxs-lookup"><span data-stu-id="e594c-184">Append tooa file</span></span>
<span data-ttu-id="e594c-185">Hello ci-dessous extrait de code illustre un `AppendToFile` méthode que vous utilisez Ajouter tooa fichier déjà stocké dans un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e594c-185">hello following snippet shows a `AppendToFile` method that you use append data tooa file already stored in a Data Lake Store account.</span></span>

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a><span data-ttu-id="e594c-186">Téléchargement d’un fichier</span><span class="sxs-lookup"><span data-stu-id="e594c-186">Download a file</span></span>
<span data-ttu-id="e594c-187">Hello ci-dessous extrait de code illustre un `DownloadFile` méthode que vous utilisez toodownload un fichier à partir d’un compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e594c-187">hello following snippet shows a `DownloadFile` method that you use toodownload a file from a Data Lake Store account.</span></span>

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a><span data-ttu-id="e594c-188">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e594c-188">Next steps</span></span>
* [<span data-ttu-id="e594c-189">Sécuriser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e594c-189">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="e594c-190">Utiliser Azure Data Lake Analytics avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e594c-190">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="e594c-191">Utiliser Azure HDInsight avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e594c-191">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="e594c-192">Data Lake Store .NET SDK Reference (Informations de référence sur le Kit de développement logiciel (SDK) .NET Azure Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="e594c-192">Data Lake Store .NET SDK Reference</span></span>](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [<span data-ttu-id="e594c-193">Data Lake Store REST Reference (Informations de référence sur les API REST Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="e594c-193">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
