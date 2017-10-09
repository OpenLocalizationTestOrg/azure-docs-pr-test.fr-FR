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
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a>Prise en main d’Azure Data Lake Store à l’aide du Kit de développement logiciel (SDK) .NET
> [!div class="op_single_selector"]
> * [Portail](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Kit SDK .NET](data-lake-store-get-started-net-sdk.md)
> * [Kit SDK Java](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.JS](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Découvrez comment toouse hello [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform les opérations de base telles que créer des dossiers, télécharger et télécharger les fichiers de données, etc.. Pour plus d’informations sur Data Lake, consultez [Azure Data Lake Store](data-lake-store-overview.md).

## <a name="prerequisites"></a>Composants requis
* **Visual Studio 2013, 2015 ou 2017**. instructions de Hello ci-dessous utilisent Visual Studio 2015 Update 2.

* **Un abonnement Azure**. Consultez la page [Obtention d’un essai gratuit d’Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Compte Azure Data Lake Store**. Pour obtenir des instructions sur la façon de toocreate un compte, consultez [prise en main Azure Data Lake Store](data-lake-store-get-started-portal.md)

* **Créez une application Azure Active Directory**. Vous utilisez hello Azure AD tooauthenticate hello Data Lake Store une application avec Azure AD. Il existe tooauthenticate différentes approches avec Azure AD, qui sont **l’authentification de l’utilisateur final** ou **l’authentification de service**. Pour plus d’informations sur la façon d’et tooauthenticate, consultez [l’authentification de l’utilisateur final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [l’authentification de service](data-lake-store-authenticate-using-active-directory.md).

## <a name="create-a-net-application"></a>Créer une application .NET
1. Ouvrez Visual Studio et créez une application console.
2. À partir de hello **fichier** menu, cliquez sur **nouveau**, puis cliquez sur **projet**.
3. À partir de **nouveau projet**, tapez ou sélectionnez hello valeurs suivantes :

   | Propriété | Valeur |
   | --- | --- |
   | Catégorie |Modèles/Visual C#/Windows |
   | Modèle |Application console |
   | Nom |CreateADLApplication |
4. Cliquez sur **OK** projet hello de toocreate.
5. Ajoutez hello Nuget packages tooyour projet.

   1. Cliquez sur le nom de projet hello Bonjour l’Explorateur de solutions, puis cliquez sur **gérer les Packages NuGet**.
   2. Bonjour **Gestionnaire de Package Nuget** onglet, vérifiez que **source du Package** est défini trop**nuget.org** et **inclure la version préliminaire** case à cocher est sélectionné.
   3. Rechercher et installer hello suivant les packages NuGet :

      * `Microsoft.Azure.Management.DataLake.Store` - Ce didacticiel utilise v2.1.3-preview.
      * `Microsoft.Rest.ClientRuntime.Azure.Authentication` - Ce didacticiel utilise v2.2.12.

        ![Ajouter une source Nuget](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Créer un compte Azure Data Lake")
   4. Fermer hello **Gestionnaire de Package Nuget**.
6. Ouvrez **Program.cs**, supprimer le code existant de hello et ensuite inclure hello suivant les instructions tooadd références toonamespaces.

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. Déclarer des variables hello comme indiqué ci-dessous et fournir les valeurs de hello pour nom Data Lake Store et le nom de groupe de ressources hello qui existent déjà. Assurez-vous également que nom de chemin d’accès et le fichier local hello que vous fournissez ici doit exister sur l’ordinateur de hello. Ajoutez hello suivant extrait de code après les déclarations d’espace de noms hello.

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

Bonjour restant des sections de hello article, vous pouvez voir comment toouse hello opérations tooperform de méthodes .NET disponibles telles que l’authentification, le transfert des fichiers, etc..

## <a name="authentication"></a>Authentification

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a>Si vous utilisez l’authentification de l’utilisateur final (recommandée pour ce didacticiel)

Utiliser votre application avec une tooauthenticate d’application native Azure AD existant **interactivement**, qui signifie que vous serez invité à tooenter vos informations d’identification Azure.

Facilité d’utilisation, extrait hello ci-dessous utilise les valeurs par défaut pour l’ID client et l’URI qui fonctionne avec n’importe quel abonnement Azure de redirection. toohelp accélère ce didacticiel, nous vous recommandons de qu'utiliser cette approche. Dans l’extrait de code hello ci-dessous, simplement enrichir hello pour votre ID de client. Vous pouvez récupérer à l’aide d’instructions hello fournies au [créer une Application Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

Quelques tooknow de choses sur cet extrait de code ci-dessus :

* toohelp accélère didacticiel de hello, cet extrait de code utilise une une annonce Azure ID de domaine et le client qui est disponible par défaut pour tous les abonnements Azure. Vous pouvez donc **utiliser cet extrait de code en l’état dans votre application**.
* Toutefois, si vous ne voulez que toouse votre propre domaine Azure AD et ID de client d’application, vous devez créer une application native d’Azure AD, utilisez hello Azure AD Client ID, ID de client, puis URI de redirection de l’application hello créé. Consultez la page [créer une Application Active Directory pour l’authentification de l’utilisateur final avec Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) pour obtenir des instructions.

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a>Si vous utilisez l’authentification de service à service avec une clé secrète client
Hello suivant extrait de code peut être utilisé tooauthenticate votre application **non interactive**, à l’aide de la clé secrète du client hello / la clé pour un principal de l’application ou le service. Utilisez-le avec une « application web » Azure AD existante. Pour obtenir des instructions sur le mode d’application de web toocreate hello Azure AD et comment tooretrieve hello ID client et question secrète du client requis dans l’extrait de code hello ci-dessous, consultez [créer une Application Active Directory pour l’authentification de service avec des données Lake Store](data-lake-store-authenticate-using-active-directory.md).

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a>Si vous utilisez l’authentification de service à service avec un certificat

Une troisième option, hello suivant extrait de code peut être utilisé tooauthenticate votre application **non interactive**, à l’aide du certificat de hello pour une application Azure Active Directory / principal de service. Utilisez-le avec une [Application Azure AD existante dotée de certificats](../azure-resource-manager/resource-group-authenticate-service-principal.md).

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a>Créer des objets clients
Hello extrait de code suivant crée hello Data Lake Store compte et le système de fichiers objets de client, qui sont utilisées tooissue demande toohello service.

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a>Répertorier tous les comptes Data Lake Store d’un abonnement
Hello extrait de code suivant répertorie tous les comptes Data Lake Store dans un abonnement Azure donné.

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

## <a name="create-a-directory"></a>Créer un répertoire
Hello ci-dessous extrait de code illustre un `CreateDirectory` méthode que vous pouvez utiliser toocreate un répertoire au sein d’un compte Data Lake Store.

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a>Charger un fichier
Hello ci-dessous extrait de code illustre un `UploadFile` compte Data Lake Store de tooa les fichiers que vous pouvez utiliser tooupload (méthode).

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

Hello SDK prend en charge le téléchargement entre un chemin d’accès local et un chemin d’accès du fichier Data Lake Store et récursive.    

## <a name="get-file-or-directory-info"></a>Obtenir des informations sur un fichier ou répertoire
Hello ci-dessous extrait de code illustre un `GetItemInfo` méthode que vous pouvez utiliser tooretrieve d’informations sur un fichier ou répertoire disponible dans Data Lake Store.

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a>Répertorier des fichiers ou répertoires
Hello ci-dessous extrait de code illustre un `ListItem` méthode qui permet de toolist hello fichiers et répertoires dans un compte Data Lake Store.

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a>Concaténation de fichiers
Hello ci-dessous extrait de code illustre un `ConcatenateFiles` méthode que vous utilisez des fichiers de tooconcatenate.

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a>Ajout d’un fichier tooa
Hello ci-dessous extrait de code illustre un `AppendToFile` méthode que vous utilisez Ajouter tooa fichier déjà stocké dans un compte Data Lake Store.

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a>Téléchargement d’un fichier
Hello ci-dessous extrait de code illustre un `DownloadFile` méthode que vous utilisez toodownload un fichier à partir d’un compte Data Lake Store.

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a>Étapes suivantes
* [Sécuriser les données dans Data Lake Store](data-lake-store-secure-data.md)
* [Utiliser Azure Data Lake Analytics avec Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Utiliser Azure HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Data Lake Store .NET SDK Reference (Informations de référence sur le Kit de développement logiciel (SDK) .NET Azure Data Lake Store)](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [Data Lake Store REST Reference (Informations de référence sur les API REST Data Lake Store)](https://msdn.microsoft.com/library/mt693424.aspx)
