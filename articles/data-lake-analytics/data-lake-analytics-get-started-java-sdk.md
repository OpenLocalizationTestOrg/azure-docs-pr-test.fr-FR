---
title: "Utiliser le SDK Java Data Lake Analytics pour développer des applications | Microsoft Docs"
description: "Utiliser le SDK Java Azure Data Lake Analytics pour développer des applications"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 07830b36-2fe3-4809-a846-129cf67b6a9e
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 795d9ec0b0cac5d74673404f1d0d851393336df0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-java-sdk"></a><span data-ttu-id="a2a6c-103">Prise en main d’Azure Data Lake Analytics à l’aide du Kit de développement logiciel Java</span><span class="sxs-lookup"><span data-stu-id="a2a6c-103">Get started with Azure Data Lake Analytics using Java SDK</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="a2a6c-104">Apprenez à utiliser le Kit de développement logiciel (SDK) Java Azure Data Lake Analytics pour créer un compte Azure Data Lake et effectuer des opérations de base comme créer des dossiers, charger et télécharger des fichiers de données, supprimer votre compte et effectuer des travaux.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-104">Learn how to use the Azure Data Lake Analytics Java SDK to create an Azure Data Lake account and perform basic operations such as create folders, upload and download data files, delete your account, and work with jobs.</span></span> <span data-ttu-id="a2a6c-105">Pour plus d’informations sur Data Lake, consultez [Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2a6c-105">For more information about Data Lake, see [Azure Data Lake Analytics](data-lake-analytics-overview.md).</span></span>

<span data-ttu-id="a2a6c-106">Dans ce didacticiel, vous allez développer une application de console Java qui contient des exemples de tâches d’administration courantes. Vous créerez ensuite des données de test et soumettrez un travail.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-106">In this tutorial, you will develop a Java console application which contains samples of common administrative tasks as well as creating test data and submitting a job.</span></span>  <span data-ttu-id="a2a6c-107">Pour suivre ce didacticiel même à l'aide d'autres outils pris en charge, cliquez sur les onglets en haut de cette section.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-107">To go through the same tutorial using other supported tools, click the tabs on the top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2a6c-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a2a6c-108">Prerequisites</span></span>
* <span data-ttu-id="a2a6c-109">Kit de développement Java (JDK) 8 (avec Java version 1.8).</span><span class="sxs-lookup"><span data-stu-id="a2a6c-109">Java Development Kit (JDK) 8 (using Java version 1.8).</span></span>
* <span data-ttu-id="a2a6c-110">IntelliJ ou un autre environnement de développement Java approprié.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-110">IntelliJ or another suitable Java development environment.</span></span> <span data-ttu-id="a2a6c-111">Ceci étape est facultatif mais recommandé.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-111">This is optional but recommended.</span></span> <span data-ttu-id="a2a6c-112">Les instructions ci-dessous utilisent IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-112">The instructions below use IntelliJ.</span></span>
* <span data-ttu-id="a2a6c-113">**Un abonnement Azure**.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-113">**An Azure subscription**.</span></span> <span data-ttu-id="a2a6c-114">Consultez la rubrique [Obtenir une version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2a6c-114">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="a2a6c-115">Création d’une application Azure Active Directory (AAD) et récupération de ses **ID client**, **ID de locataire** et **Clé**.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-115">Create an Azure Active Directory (AAD) application and retrieve its **Client ID**, **Tenant ID**, and **Key**.</span></span> <span data-ttu-id="a2a6c-116">Pour plus d’informations sur les applications AAD et pour savoir comment obtenir un ID client, consultez [Création de l’application Active Directory et du principal du service à l’aide du portail](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a2a6c-116">For more information about AAD applications and instructions on how to get a client ID, see [Create Active Directory application and service principal using portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="a2a6c-117">L’URI de réponse et la Clé seront également disponibles sur le portail une fois l’application créée et la clé générée.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-117">The Reply URI and Key will also be available from the portal once you have the application created and key generated.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="a2a6c-118">Comment s’authentifier à l’aide d’Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a2a6c-118">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="a2a6c-119">L’extrait de code ci-dessous fournit le code pour une authentification **non interactive** , où l’application fournit ses propres informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-119">The code snippet below provides code for **non-interactive** authentication, where the application provides its own credentials.</span></span>

<span data-ttu-id="a2a6c-120">Vous devrez donner à votre application l’autorisation de créer des ressources dans Azure pour que ce didacticiel fonctionne.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-120">You will need to give your application permission to create resources in Azure for this tutorial to work.</span></span> <span data-ttu-id="a2a6c-121">Dans le cadre de ce didacticiel, il est **recommandé** de n’accorder à cette application que des autorisations de type Collaborateur pour un nouveau groupe de ressources, inutilisé et vide, dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-121">It is **highly recommended** that you only give this application Contributor permissions to a new, unused, and empty resource group in your Azure subscription for the purposes of this tutorial.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="a2a6c-122">Création d’une application Java</span><span class="sxs-lookup"><span data-stu-id="a2a6c-122">Create a Java application</span></span>
1. <span data-ttu-id="a2a6c-123">Ouvrez IntelliJ et créez un nouveau projet Java à l’aide du modèle **Application de ligne de commande** .</span><span class="sxs-lookup"><span data-stu-id="a2a6c-123">Open IntelliJ and create a new Java project using the **Command Line App** template.</span></span>
2. <span data-ttu-id="a2a6c-124">Cliquez avec le bouton droit sur le projet sur le côté gauche de l’écran et cliquez sur **Ajouter la prise en charge Framework**.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-124">Right-click on the project on the left-hand side of your screen and click **Add Framework Support**.</span></span> <span data-ttu-id="a2a6c-125">Choisissez **Maven** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-125">Choose **Maven** and click **OK**.</span></span>
3. <span data-ttu-id="a2a6c-126">Ouvrez le fichier **« pom.xml »** créé et ajoutez l’extrait de texte suivant entre la balise **\</version>** et la balise **\</project>** :</span><span class="sxs-lookup"><span data-stu-id="a2a6c-126">Open the newly created **"pom.xml"** file and add the following snippet of text between the **\</version>** tag and the **\</project>** tag:</span></span>

    >[!NOTE]
    ><span data-ttu-id="a2a6c-127">Cette étape est provisoire tant que le Kit de développement logiciel (SDK) Azure Data Lake Analytics n’est pas disponible dans Maven.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-127">This step is temporary until the Azure Data Lake Analytics SDK is available in Maven.</span></span> <span data-ttu-id="a2a6c-128">Cet article sera mis à jour une fois le Kit de développement logiciel (SDK) disponible dans Maven.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-128">This article will be updated once the SDK is available in Maven.</span></span> <span data-ttu-id="a2a6c-129">Toutes les futures mises à jour ce Kit de développement logiciel (SDK) seront disponibles via Maven.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-129">All future updates to this SDK will be availble through Maven.</span></span>
    >

        <repositories>
            <repository>
                <id>adx-snapshots</id>
                <name>Azure ADX Snapshots</name>
                <url>http://adxsnapshots.azurewebsites.net/</url>
                <layout>default</layout>
                <snapshots>
                    <enabled>true</enabled>
                </snapshots>
            </repository>
            <repository>
                <id>oss-snapshots</id>
                <name>Open Source Snapshots</name>
                <url>https://oss.sonatype.org/content/repositories/snapshots/</url>
                <layout>default</layout>
                <snapshots>
                    <enabled>true</enabled>
                    <updatePolicy>always</updatePolicy>
                </snapshots>
            </repository>
        </repositories>
        <dependencies>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-client-authentication</artifactId>
                <version>1.0.0-20160513.000802-24</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-client-runtime</artifactId>
                <version>1.0.0-20160513.000812-28</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.rest</groupId>
                <artifactId>client-runtime</artifactId>
                <version>1.0.0-20160513.000825-29</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-mgmt-datalake-store</artifactId>
                <version>1.0.0-SNAPSHOT</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-mgmt-datalake-analytics</artifactId>
                <version>1.0.0-SNAPSHOT</version>
            </dependency>
        </dependencies>
4. <span data-ttu-id="a2a6c-130">Accédez à **Fichier**, puis choisissez **Paramètres**, **Build**, **Exécution** et **Déploiement**.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-130">Go to **File**, then **Settings**, then **Build**, **Execution**, **Deployment**.</span></span> <span data-ttu-id="a2a6c-131">Sélectionnez **Outils de génération**, **Maven**, **Importation**.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-131">Select **Build Tools**, **Maven**, **Importing**.</span></span> <span data-ttu-id="a2a6c-132">Cochez ensuite **Importer les projets Maven automatiquement**.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-132">Then check **Import Maven projects automatically**.</span></span>
5. <span data-ttu-id="a2a6c-133">Ouvrez **Main.java** et remplacez le bloc de code existant par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-133">Open **Main.java** and replace the existing code block with the following code.</span></span> <span data-ttu-id="a2a6c-134">De même, indiquez les valeurs des paramètres inclus dans l’extrait de code, tels que **localFolderPath**, **_adlaAccountName**, **_adlsAccountName**, **_resourceGroupName** et remplacez les espaces réservés pour **CLIENT-ID**, **CLIENT-SECRET**, **TENANT-ID** et **SUBSCRIPTION-ID**.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-134">Also, provide the values for parameters called out in the code snippet, such as **localFolderPath**, **_adlaAccountName**, **_adlsAccountName**, **_resourceGroupName** and replace placeholders for **CLIENT-ID**, **CLIENT-SECRET**, **TENANT-ID**, and **SUBSCRIPTION-ID**.</span></span>

    <span data-ttu-id="a2a6c-135">Ce code mène à bien l’ensemble du processus, à savoir : création de comptes Data Lake Store et Data Lake Analytics, création de fichiers dans le magasin, exécution d’un travail, obtention de l’état du travail, téléchargement de la sortie du travail et enfin suppression du compte.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-135">This code goes through the process of creating Data Lake Store and Data Lake Analytics accounts, creating files in the store, running a job, getting job status, downloading job output, and finally deleting the account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a2a6c-136">Il existe actuellement un problème connu avec le service Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-136">There is currently a known issue with the Azure Data Lake Service.</span></span>  <span data-ttu-id="a2a6c-137">Si l’exemple d’application est interrompue ou rencontre une erreur, vous devrez peut-être supprimer manuellement les comptes Data Lake Store & Data Lake Analytics créés par le script.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-137">If the sample app is interrupted or encounters an error, you may need to manually delete the Data Lake Store & Data Lake Analytics accounts that the script creates.</span></span>  <span data-ttu-id="a2a6c-138">Si vous n’êtes pas familiarisé avec le portail, le guide [Gérer les analyses Azure Data Lake à l’aide du portail Azure](data-lake-analytics-manage-use-portal.md) vous aidera à démarrer.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-138">If you're not familiar with the Portal, the [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md) guide will get you started.</span></span>
   >
   >

        package com.company;

        import com.microsoft.azure.CloudException;
        import com.microsoft.azure.credentials.ApplicationTokenCredentials;
        import com.microsoft.azure.management.datalake.store.*;
        import com.microsoft.azure.management.datalake.store.models.*;
        import com.microsoft.azure.management.datalake.analytics.*;
        import com.microsoft.azure.management.datalake.analytics.models.*;
        import com.microsoft.rest.credentials.ServiceClientCredentials;
        import java.io.*;
        import java.nio.charset.Charset;
        import java.nio.file.Files;
        import java.nio.file.Paths;
        import java.util.ArrayList;
        import java.util.UUID;
        import java.util.List;

        public class Main {
            private static String _adlsAccountName;
            private static String _adlaAccountName;
            private static String _resourceGroupName;
            private static String _location;

            private static String _tenantId;
            private static String _subId;
            private static String _clientId;
            private static String _clientSecret;

            private static DataLakeStoreAccountManagementClient _adlsClient;
            private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;
            private static DataLakeAnalyticsAccountManagementClient _adlaClient;
            private static DataLakeAnalyticsJobManagementClient _adlaJobClient;
            private static DataLakeAnalyticsCatalogManagementClient _adlaCatalogClient;

            public static void main(String[] args) throws Exception {
                _adlsAccountName = "<DATA-LAKE-STORE-NAME>";
                _adlaAccountName = "<DATA-LAKE-ANALYTICS-NAME>";
                _resourceGroupName = "<RESOURCE-GROUP-NAME>";
                _location = "East US 2";

                _tenantId = "<TENANT-ID>";
                _subId =  "<SUBSCRIPTION-ID>";
                _clientId = "<CLIENT-ID>";

                _clientSecret = "<CLIENT-SECRET>"; // TODO: For production scenarios, we recommend that you replace this line with a more secure way of acquiring the application client secret, rather than hard-coding it in the source code.

                String localFolderPath = "C:\\local_path\\"; // TODO: Change this to any unused, new, empty folder on your local machine.

                // Authenticate
                ApplicationTokenCredentials creds = new ApplicationTokenCredentials(_clientId, _tenantId, _clientSecret, null);
                SetupClients(creds);

                // Create Data Lake Store and Analytics accounts
                WaitForNewline("Authenticated.", "Creating NEW accounts.");
                CreateAccounts();
                WaitForNewline("Accounts created.", "Displaying accounts.");

                // List Data Lake Store and Analytics accounts that this app can access
                System.out.println(String.format("All ADL Store accounts that this app can access in subscription %s:", _subId));
                List<DataLakeStoreAccount> adlsListResult = _adlsClient.getAccountOperations().list().getBody();
                for (DataLakeStoreAccount acct : adlsListResult) {
                    System.out.println(acct.getName());
                }
                System.out.println(String.format("All ADL Analytics accounts that this app can access in subscription %s:", _subId));
                List<DataLakeAnalyticsAccount> adlaListResult = _adlaClient.getAccountOperations().list().getBody();
                for (DataLakeAnalyticsAccount acct : adlaListResult) {
                    System.out.println(acct.getName());
                }
                WaitForNewline("Accounts displayed.", "Creating files.");

                // Create a file in Data Lake Store: input1.csv
                // TODO: these change order in the next patch
                byte[] bytesContents = "123,abc".getBytes();
                _adlsFileSystemClient.getFileSystemOperations().create(_adlsAccountName, "/input1.csv", bytesContents, true);

                WaitForNewline("File created.", "Submitting a job.");

                // Submit a job to Data Lake Analytics
                UUID jobId = SubmitJobByScript("@input =  EXTRACT Data string FROM \"/input1.csv\" USING Extractors.Csv(); OUTPUT @input TO @\"/output1.csv\" USING Outputters.Csv();", "testJob");
                WaitForNewline("Job submitted.", "Getting job status.");

                // Wait for job completion and output job status
                System.out.println(String.format("Job status: %s", GetJobStatus(jobId)));
                System.out.println("Waiting for job completion.");
                WaitForJob(jobId);
                System.out.println(String.format("Job status: %s", GetJobStatus(jobId)));
                WaitForNewline("Job completed.", "Downloading job output.");

                // Download job output from Data Lake Store
                DownloadFile("/output1.csv", localFolderPath + "output1.csv");
                WaitForNewline("Job output downloaded.", "Deleting file.");

                // Delete file from Data Lake Store
                DeleteFile("/output1.csv");
                WaitForNewline("File deleted.", "Deleting account.");

                // Delete account
                _adlsClient.getAccountOperations().delete(_resourceGroupName, _adlsAccountName);
                _adlaClient.getAccountOperations().delete(_resourceGroupName, _adlaAccountName);
                WaitForNewline("Account deleted.", "DONE.");
            }

            //Set up clients
            public static void SetupClients(ServiceClientCredentials creds)
            {
                _adlsClient = new DataLakeStoreAccountManagementClientImpl(creds);
                _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClientImpl(creds);
                _adlaClient = new DataLakeAnalyticsAccountManagementClientImpl(creds);
                _adlaJobClient = new DataLakeAnalyticsJobManagementClientImpl(creds);
                _adlaCatalogClient = new DataLakeAnalyticsCatalogManagementClientImpl(creds);
                _adlsClient.setSubscriptionId(_subId);
                _adlaClient.setSubscriptionId(_subId);
            }

            // Helper function to show status and wait for user input
            public static void WaitForNewline(String reason, String nextAction)
            {
                if (nextAction == null)
                    nextAction = "";

                System.out.println(reason + "\r\nPress ENTER to continue...");
                try{System.in.read();}
                catch(Exception e){}

                if (!nextAction.isEmpty())
                {
                    System.out.println(nextAction);
                }
            }

            // Create Data Lake Store and Analytics accounts
            public static void CreateAccounts() throws InterruptedException, CloudException, IOException {
                // Create ADLS account
                DataLakeStoreAccount adlsParameters = new DataLakeStoreAccount();
                adlsParameters.setLocation(_location);

                _adlsClient.getAccountOperations().create(_resourceGroupName, _adlsAccountName, adlsParameters);

                // Create ADLA account
                DataLakeStoreAccountInfo adlsInfo = new DataLakeStoreAccountInfo();
                adlsInfo.setName(_adlsAccountName);

                DataLakeStoreAccountInfoProperties adlsInfoProperties = new DataLakeStoreAccountInfoProperties();
                adlsInfo.setProperties(adlsInfoProperties);

                List<DataLakeStoreAccountInfo> adlsInfoList = new ArrayList<DataLakeStoreAccountInfo>();
                adlsInfoList.add(adlsInfo);

                DataLakeAnalyticsAccountProperties adlaProperties = new DataLakeAnalyticsAccountProperties();
                adlaProperties.setDataLakeStoreAccounts(adlsInfoList);
                adlaProperties.setDefaultDataLakeStoreAccount(_adlsAccountName);

                DataLakeAnalyticsAccount adlaParameters = new DataLakeAnalyticsAccount();
                adlaParameters.setLocation(_location);
                adlaParameters.setName(_adlaAccountName);
                adlaParameters.setProperties(adlaProperties);

                    /* If this line generates an error message like "The deep update for property 'DataLakeStoreAccounts' is not supported", please delete the ADLS and ADLA accounts via the portal and re-run your script. */

                _adlaClient.getAccountOperations().create(_resourceGroupName, _adlaAccountName, adlaParameters);
            }

            //todo: this changes in the next version of the API
            public static void CreateFile(String path, String contents, boolean force) throws IOException, CloudException {
                byte[] bytesContents = contents.getBytes();

                _adlsFileSystemClient.getFileSystemOperations().create(_adlsAccountName, path, bytesContents, force);
            }

            public static void DeleteFile(String filePath) throws IOException, CloudException {
                _adlsFileSystemClient.getFileSystemOperations().delete(filePath, _adlsAccountName);
            }

            // Download file
            public static void DownloadFile(String srcPath, String destPath) throws IOException, CloudException {
                InputStream stream = _adlsFileSystemClient.getFileSystemOperations().open(srcPath, _adlsAccountName).getBody();

                PrintWriter pWriter = new PrintWriter(destPath, Charset.defaultCharset().name());

                String fileContents = "";
                if (stream != null) {
                    Writer writer = new StringWriter();

                    char[] buffer = new char[1024];
                    try {
                        Reader reader = new BufferedReader(
                                new InputStreamReader(stream, "UTF-8"));
                        int n;
                        while ((n = reader.read(buffer)) != -1) {
                            writer.write(buffer, 0, n);
                        }
                    } finally {
                        stream.close();
                    }
                    fileContents =  writer.toString();
                }

                pWriter.println(fileContents);
                pWriter.close();
            }

            // Submit a U-SQL job by providing script contents.
            // Returns the job ID
            public static UUID SubmitJobByScript(String script, String jobName) throws IOException, CloudException {
                UUID jobId = java.util.UUID.randomUUID();
                USqlJobProperties properties = new USqlJobProperties();
                properties.setScript(script);
                JobInformation parameters = new JobInformation();
                parameters.setName(jobName);
                parameters.setJobId(jobId);
                parameters.setType(JobType.USQL);
                parameters.setProperties(properties);

                JobInformation jobInfo = _adlaJobClient.getJobOperations().create(_adlaAccountName, jobId, parameters).getBody();

                return jobId;
            }

            // Wait for job completion
            public static JobResult WaitForJob(UUID jobId) throws IOException, CloudException {
                JobInformation jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName, jobId).getBody();
                while (jobInfo.getState() != JobState.ENDED)
                {
                    jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName,jobId).getBody();
                }
                return jobInfo.getResult();
            }

            // Get job status
            public static String GetJobStatus(UUID jobId) throws IOException, CloudException {
                JobInformation jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName, jobId).getBody();
                return jobInfo.getState().toValue();
            }
        }

1. <span data-ttu-id="a2a6c-139">Suivez les invites pour exécuter et terminer l’application.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-139">Follow the prompts to run and complete the application.</span></span>

## <a name="see-also"></a><span data-ttu-id="a2a6c-140">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="a2a6c-140">See also</span></span>
* <span data-ttu-id="a2a6c-141">Pour afficher le même didacticiel en utilisant d’autres outils, cliquez sur les sélecteurs d’onglet en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="a2a6c-141">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
* <span data-ttu-id="a2a6c-142">Pour voir une requête plus complexe, consultez [Analyse de journaux des sites web à l'aide d'Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="a2a6c-142">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="a2a6c-143">Pour commencer à développer des applications U-SQL, consultez [Développer des scripts U-SQL avec Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a2a6c-143">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="a2a6c-144">Pour découvrir U-SQL, consultez les articles [Prise en main du langage U-SQL Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md) et [Référence sur le langage U-SQL](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="a2a6c-144">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md), and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>
* <span data-ttu-id="a2a6c-145">Pour les tâches de gestion, consultez [Gestion d’Azure Data Lake Analytics à l’aide du portail Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a2a6c-145">For management tasks, see [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="a2a6c-146">Pour obtenir une vue d’ensemble de Data Lake Analytics, consultez [Présentation d’Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2a6c-146">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
