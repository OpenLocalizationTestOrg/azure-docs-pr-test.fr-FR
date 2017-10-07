---
title: "Always Encrypted : SQL Database - Azure Key Vault | Microsoft Docs"
description: "Cet article vous explique comment toosecure des données sensibles dans une base de données SQL à l’aide du chiffrement de données hello Assistant Always Encrypted dans SQL Server Management Studio. Il contient également des instructions qui vous indiquent comment toostore chaque clé de chiffrement dans Azure Key Vault."
keywords: "chiffrement des données, clé de chiffrement, chiffrement cloud"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: 6ca16644-5969-497b-a413-d28c3b835c9b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: sstein
ms.openlocfilehash: 8226bfef584e979643f5bb0747d4df16569f8204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a>Chiffrement intégral : Protéger les données sensibles dans Base de données SQL et stocker vos clés de chiffrement dans Azure Key Vault

Cet article vous explique comment toosecure des données sensibles dans un SQL de base de données avec le chiffrement de données à l’aide de hello [Assistant Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) dans [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx). Il contient également des instructions qui vous indiquent comment toostore chaque clé de chiffrement dans Azure Key Vault.

Always Encrypted est une nouvelle technologie de chiffrement de données dans la base de données SQL Azure et SQL Server qui vous aide à protéger les données sensibles au repos sur le serveur de hello, lors de déplacements entre client et serveur, et pendant que les données de salutation sont en cours d’utilisation. Always Encrypted garantit que les données sensibles n’apparaissent jamais en texte clair à l’intérieur du système de base de données hello. Après avoir configuré le chiffrement des données, uniquement les applications clientes ou les serveurs d’applications qui ont des clés d’accès toohello peuvent accéder aux données de texte en clair. Pour plus d’informations, consultez [Chiffrement intégral (moteur de base de données)](https://msdn.microsoft.com/library/mt163865.aspx).

Après avoir configuré hello toouse de base de données Always Encrypted, vous allez créer une application cliente en c# avec toowork de Visual Studio avec des données hello chiffré.

Suivez les étapes de hello dans cet article et découvrez comment tooset d’Always Encrypted pour une base de données SQL Azure. Dans cet article, vous allez apprendre des tâches de hello tooperform suivant :

* Utilisez l’Assistant Always Encrypted hello dans SSMS toocreate [clés Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).
  * Créer une [clé principale de colonne (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).
  * Créer une [clé de chiffrement de colonne (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).
* Créer une table de base de données et chiffrer des colonnes.
* Créer une application qui insère, sélectionne et affiche les données des colonnes de hello chiffré.

## <a name="prerequisites"></a>Composants requis
Pour ce didacticiel, vous devez disposer des éléments suivants :

* Un compte et un abonnement Azure. Si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).
* [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx) , version 13.0.700.242 ou ultérieure.
* [.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) ou version ultérieure (sur l’ordinateur client de hello).
* [Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).
* [Azure PowerShell](/powershell/azure/overview), version 1.0 ou ultérieure. Type **(Get-Module - ListAvailable azure). Version** toosee quelle version de PowerShell vous sont en cours d’exécution.

## <a name="enable-your-client-application-tooaccess-hello-sql-database-service"></a>Activer votre service de base de données SQL client application tooaccess hello
Vous devez activer votre service de base de données SQL client application tooaccess hello en configurant l’authentification obligatoire hello et hello lors de l’acquisition *ClientId* et *Secret* que vous devez tooauthenticate votre application Bonjour suivant de code.

1. Ouvrez hello [portail Azure classic](http://manage.windowsazure.com).
2. Sélectionnez **Active Directory** et cliquez sur une instance Active Directory hello que votre application utilisera.
3. Cliquez sur **Applications**, puis sur **AJOUTER**.
4. Tapez un nom pour votre application (par exemple : *myClientApp*), sélectionnez **APPLICATION WEB**, puis cliquez sur hello flèche toocontinue.
5. Pourquoi **URL de connexion** et **URI ID d’application** vous pouvez taper une URL valide (par exemple, *http://myClientApp*) et continuer.
6. Cliquez sur **CONFIGURER**.
7. Copiez votre **ID CLIENT**. (vous aurez besoin cette valeur dans votre code ultérieurement).
8. Bonjour **clés** section, sélectionnez **1 an** de hello **sélectionner une durée** liste déroulante. (Vous allez copier la clé de hello après avoir enregistré à l’étape 13.)
9. Faites défiler et cliquez sur **Ajouter une application**.
10. Laissez **afficher** défini trop**Microsoft Apps** et sélectionnez **API de gestion Microsoft Azure**. Cliquez sur hello coche toocontinue.
11. Sélectionnez **accéder à la gestion des services Azure...**  de hello **autorisations déléguées** liste déroulante.
12. Cliquez sur **ENREGISTRER**.
13. Après avoir hello de sauvegarde se termine, copiez la valeur de clé de hello Bonjour **clés** section. (vous aurez besoin cette valeur dans votre code ultérieurement).

## <a name="create-a-key-vault-toostore-your-keys"></a>Créer un coffre de clés de toostore vos clés
Maintenant que votre application cliente est configurée et que votre ID client, il est temps toocreate un coffre de clés et configurer sa stratégie d’accès pour vous et votre application peuvent accéder aux clés secrètes du coffre hello (clés de chiffrement intégral hello). Hello *créer*, *obtenir*, *liste*, *signe*, *vérifier*, *wrapKey*, et *unwrapKey* autorisations sont requises pour la création d’une nouvelle clé principale de colonne et de configuration de chiffrement avec SQL Server Management Studio.

Vous pouvez rapidement créer un coffre de clés en exécutant le script suivant de hello. Pour obtenir une explication détaillée de ces applets de commande et plus d’informations sur la création et la configuration d’un coffre de clés, voir [Prise en main d’Azure Key Vault](../key-vault/key-vault-get-started.md).

    $subscriptionName = '<your Azure subscription name>'
    $userPrincipalName = '<username@domain.com>'
    $clientId = '<client ID that you copied in step 7 above>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $vaultName = 'AeKeyVault'


    Login-AzureRmAccount
    $subscriptionId = (Get-AzureRmSubscription -SubscriptionName $subscriptionName).Id
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $resourceGroupName -Location $location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
    Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list




## <a name="create-a-blank-sql-database"></a>Créer une base de données SQL vide
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Accédez trop**nouveau** > **données + stockage** > **base de données SQL**.
3. Créez une base de données **vide** nommée **Clinique** sur un serveur nouveau ou existant. Pour obtenir des instructions détaillées sur toocreate une base de données hello portail Azure, voir [votre première base de données SQL Azure](sql-database-get-started-portal.md).
   
    ![Créer une base de données vide](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

Vous devez serez hello chaîne de connexion plus loin dans le didacticiel de hello, par conséquent, après avoir créé la base de données hello, parcourir toohello nouvelle clinique de base de données et copie hello chaîne de connexion. Vous pouvez obtenir la chaîne de connexion hello à tout moment, mais il est facile toocopy dans hello portail Azure.

1. Accédez trop**bases de données SQL** > **Clinic** > **afficher les chaînes de connexion de base de données**.
2. Copier la chaîne de connexion hello pour **ADO.NET**.
   
    ![Copier la chaîne de connexion hello](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a>Connexion de base de données toohello avec SSMS
Ouvrez SSMS et se connecter toohello server avec base de données de la clinique hello.

1. Ouvrez SSMS. (Accédez trop**Connect** > **moteur de base de données** tooopen hello **connecter tooServer** fenêtre si elle n’est pas ouverte.)
2. Entrez le nom du serveur et vos informations d’identification. nom du serveur Hello se trouve sur le panneau de base de données SQL hello et dans la chaîne de connexion hello que vous avez copiée précédemment. Nom de type hello complète du serveur, y compris *database.windows.net*.
   
    ![Copier la chaîne de connexion hello](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

Si hello **nouvelle règle de pare-feu** s’affiche, connectez-vous à tooAzure et SSMS permettent de créer une règle de pare-feu pour vous.

## <a name="create-a-table"></a>Création d’une table
Dans cette section, vous allez créer des données patient toohold table. Il n’est pas initialement chiffré--vous allez configurer le chiffrement dans la section suivante de hello.

1. Développez **Bases de données**.
2. Avec le bouton hello **Clinic** de base de données et cliquez sur **nouvelle requête**.
3. Hello coller suivant Transact-SQL (T-SQL) dans la nouvelle fenêtre de requête hello et **Execute** il.

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a>Chiffrer des colonnes (configurer le chiffrement intégral)
SSMS fournit un Assistant qui vous permet de facilement configurer Always Encrypted en définissant des colonnes chiffrées, clé principale de colonne hello et clé de chiffrement de colonne pour vous.

1. Développez **Bases de données** > **Clinique** > **Tables**.
2. Avec le bouton hello **Patients** de table et sélectionnez **chiffrer les colonnes** Assistant de chiffrement intégral hello tooopen :
   
    ![Chiffrer les colonnes](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

Assistant Always Encrypted Hello comprend les sections suivantes de hello : **sélection de la colonne**, **Configuration de la clé principale de**, **Validation**, et **résumé** .

### <a name="column-selection"></a>Sélection de colonnes
Cliquez sur **suivant** sur hello **Introduction** hello tooopen de page **sélection de la colonne** page. Dans cette page, vous sélectionnerez quelles colonnes vous souhaitez tooencrypt, [hello du type de chiffrement et quelle clé de chiffrement de colonne (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.

Chiffrez les informations **SSN** et **BirthDate** pour chaque patient. Hello SSN colonne utilise le chiffrement déterministe, qui prend en charge les recherches d’égalité, de jointures et de group by. colonne de date de naissance Hello utilise le chiffrement aléatoire, qui ne prend pas en charge les opérations.

Ensemble hello **le Type de chiffrement** pour la colonne de hello SSN trop**déterministe** et hello colonne BirthDate trop**aléatoire**. Cliquez sur **Suivant**.

![Chiffrer les colonnes](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a>Configuration de la clé principale
Hello **Master Key Configuration** page est où vous configurez votre clé CMK et le fournisseur de magasin de clés hello sélectionnez où hello CMK sera stocké. Actuellement, vous pouvez stocker une clé CMK dans le magasin de certificats Windows hello, Azure Key Vault ou un module de sécurité matériel (HSM).

Ce didacticiel montre comment toostore vos clés dans le coffre de clés Azure.

1. Sélectionnez **Azure Key Vault**.
2. Sélectionnez le coffre de clés souhaitée hello à partir de la liste déroulante de hello.
3. Cliquez sur **Suivant**.

![Configuration de la clé principale](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a>Validation
Vous pouvez chiffrer les colonnes hello maintenant ou enregistrer un toorun de script PowerShell plus tard. Pour ce didacticiel, sélectionnez **continuer toofinish maintenant** et cliquez sur **suivant**.

### <a name="summary"></a>Résumé
Vérifiez que les paramètres de hello sont correctes, cliquez sur **Terminer** le programme d’installation de toocomplete hello pour Always Encrypted.

![Résumé](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-hello-wizards-actions"></a>Vérifier les actions de l’Assistant hello
Une fois hello Assistant terminé, votre base de données est configurée pour Always Encrypted. Bonjour Bonjour d’Assistant effectué suivant des actions :

* Création d’une clé principale de colonne et stockage de celle-ci dans Azure Key Vault.
* Création d’une clé de chiffrement de colonne et stockage de celle-ci dans Azure Key Vault.
* Hello configuré sélectionné des colonnes pour le chiffrement. table de Patients Hello a actuellement pas de données, mais toutes les données existantes dans les colonnes hello sélectionné sont désormais chiffrées.

Vous pouvez vérifier la création de hello de clés hello dans SSMS en développant **Clinic** > **sécurité** > **clés Always Encrypted**.

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a>Créer une application cliente qui fonctionne avec les données de salutation chiffrée
Maintenant que le chiffrement intégral est configuré, vous pouvez générer une application qui effectue *insère* et *sélectionne* sur hello des colonnes chiffrées.  

> [!IMPORTANT]
> Votre application doit utiliser [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objets lors du passage du serveur de toohello de données de texte en clair avec des colonnes toujours chiffrées. La transmission de valeurs littérales sans objets SqlParameter entraînera une exception.
> 
> 

1. Ouvrez Visual Studio et créez une **application console** C# (Visual Studio 2015 et versions antérieures) ou une **application console (.NET Framework)** (Visual Studio 2017 et versions ultérieures). Assurez-vous que votre projet est trop**.NET Framework 4.6** ou version ultérieure.
2. Projet de hello nom **AlwaysEncryptedConsoleAKVApp** et cliquez sur **OK**.
3. Installer hello suivant les packages NuGet en accédant trop**outils** > **Gestionnaire de Package NuGet** > **Package Manager Console**.

Exécutez ces deux lignes de code dans la Console du Gestionnaire de Package de hello.

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-tooenable-always-encrypted"></a>Modifier votre tooenable de chaîne de connexion Always Encrypted
Cette section explique comment tooenable toujours chiffré dans votre chaîne de connexion de base de données.

tooenable Always Encrypted, vous devez tooadd hello **Column Encryption Setting** connexion tooyour de mot clé de chaîne et la définir trop**activé**.

Vous pouvez définir cette option directement dans la chaîne de connexion hello, ou vous pouvez la définir à l’aide de [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx). exemple d’application Hello Bonjour section suivante montre comment toouse **SqlConnectionStringBuilder**.

### <a name="enable-always-encrypted-in-hello-connection-string"></a>Activer le chiffrement intégral dans la chaîne de connexion hello
Ajoutez hello suivant de chaîne de connexion mot clé tooyour.

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a>Activer le chiffrement intégral avec le paramètre SqlConnectionStringBuilder
Hello suivant de code montre comment tooenable Always Encrypted en définissant [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) trop[activé](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-hello-azure-key-vault-provider"></a>Inscrire le fournisseur de coffre de clés Azure hello
Hello de code suivant montre comment tooregister hello fournisseur Azure Key Vault avec le pilote d’ADO.NET hello.

    private static ClientCredential _clientCredential;

    static void InitializeAzureKeyVaultProvider()
    {
       _clientCredential = new ClientCredential(clientId, clientSecret);

       SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
          new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

       Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
          new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

       providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
       SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
    }



## <a name="always-encrypted-sample-console-application"></a>Exemple d’application console intégralement chiffrée
Cet exemple montre comment :

* Modifiez votre tooenable de chaîne de connexion Always Encrypted.
* Inscrire Azure Key Vault comme fournisseur de magasin de clés de l’application de hello.  
* Insérer des données dans des colonnes de hello chiffré.
* Sélectionner un enregistrement en filtrant une valeur spécifique dans une colonne chiffrée.

Remplacez le contenu hello de **Program.cs** avec hello suivant de code. Remplacez la chaîne de connexion de hello pour la variable de connectionString global hello dans la ligne hello qui précède directement la méthode Main hello avec votre chaîne de connexion valide à partir de hello portail Azure. Il s’agit de hello seule modification que vous avez besoin de toomake toothis code.

Exécuter toosee d’application hello Always Encrypted en action.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider;

    namespace AlwaysEncryptedConsoleAKVApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"<connection string from hello portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

            InsertPatient(new Patient()
            {
                SSN = "999-99-0001",
                FirstName = "Orlando",
                LastName = "Gee",
                BirthDate = DateTime.Parse("01/04/1964")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0002",
                FirstName = "Keith",
                LastName = "Harris",
                BirthDate = DateTime.Parse("06/20/1977")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0003",
                FirstName = "Donna",
                LastName = "Carreras",
                BirthDate = DateTime.Parse("02/09/1973")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0004",
                FirstName = "Janet",
                LastName = "Gates",
                BirthDate = DateTime.Parse("08/31/1985")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0005",
                FirstName = "Lucy",
                LastName = "Harrington",
                BirthDate = DateTime.Parse("05/06/1993")
            });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter tooexit...");
            Console.ReadLine();
        }


        private static ClientCredential _clientCredential;

        static void InitializeAzureKeyVaultProvider()
        {

            _clientCredential = new ClientCredential(clientId, clientSecret);

            SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
              new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

            Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
              new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

            providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        }

        public async static Task<string> GetToken(string authority, string resource, string scope)
        {
            var authContext = new AuthenticationContext(authority);
            AuthenticationResult result = await authContext.AcquireTokenAsync(resource, _clientCredential);

            if (result == null)
                throw new InvalidOperationException("Failed tooobtain hello access token");
            return result.AccessToken;
        }

        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
     VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in hello Patients table tooreset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }



## <a name="verify-that-hello-data-is-encrypted"></a>Vérifiez que les données de salutation sont chiffrées.
Vous pouvez vérifier rapidement le chiffrement des données réelles de hello sur le serveur de hello en interrogeant les données de Patients hello avec SSMS (à l’aide de votre connexion actuelle où **Column Encryption Setting** n’est pas encore activée).

Exécutez hello suivant de requête de base de données de la clinique hello.

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

Vous pouvez voir que les colonnes hello chiffré ne contiennent pas toutes les données en texte clair.

   ![Nouvelle application de console](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

toouse SSMS tooaccess hello des données en texte brut, vous pouvez ajouter des hello *paramètre de chiffrement de colonne = activé* connexion toohello de paramètre.

1. Dans SSMS, cliquez avec le bouton droit sur votre serveur dans **l’Explorateur d’objets**, puis choisissez **Déconnecter**.
2. Cliquez sur **Connect** > **moteur de base de données** tooopen hello **connecter tooServer** fenêtre et cliquez sur **Options**.
3. Cliquez sur **Paramètres de connexion supplémentaires** et tapez **Column Encryption Setting=enabled**.
   
    ![Nouvelle application de console](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. Exécutez hello suivant de requête de base de données de la clinique hello.
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     Vous pouvez maintenant voir les données de texte en clair hello dans les colonnes hello chiffré.

    ![Nouvelle application de console](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a>Étapes suivantes
Après avoir créé une base de données qui utilise le chiffrement intégral, vous souhaiterez peut-être suivant de hello toodo :

* [Faire pivoter et nettoyer vos clés](https://msdn.microsoft.com/library/mt607048.aspx).
* [Migrer des données déjà chiffrées avec le chiffrement intégral](https://msdn.microsoft.com/library/mt621539.aspx).

## <a name="related-information"></a>Informations connexes
* [Chiffrement intégral (développement client)](https://msdn.microsoft.com/library/mt147923.aspx)
* [Chiffrement transparent des données](https://msdn.microsoft.com/library/bb934049.aspx)
* [Chiffrement SQL Server](https://msdn.microsoft.com/library/bb510663.aspx)
* [Assistant Chiffrement intégral](https://msdn.microsoft.com/library/mt459280.aspx)
* [Blog Chiffrement intégral](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

