---
title: "Always Encrypted : Azure SQL Database - Magasin de certificats Windows | Microsoft Docs"
description: "Cet article vous explique comment toosecure des données sensibles dans une base de données SQL avec le chiffrement de base de données à l’aide de hello Assistant Always Encrypted dans SQL Server Management Studio (SSMS). Il vous montre également comment toostore stocker vos clés de chiffrement dans le certificat de Windows hello."
keywords: "chiffrer les données, chiffrement sql, chiffrement de base de données, données sensibles, chiffrement intégral"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: ce7e052e-8bf6-4d7c-9204-4c6f4afeba4b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: sstein
ms.openlocfilehash: 483f9a2120cc42b732142fc07807d3d8830a0c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-hello-windows-certificate-store"></a>Always Encrypted : Protéger les données sensibles dans la base de données SQL et de stocker vos clés de chiffrement dans le magasin de certificats Windows hello

Cet article vous explique comment toosecure des données sensibles dans un SQL de base de données avec le chiffrement de base de données à l’aide de hello [Assistant Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) dans [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx). Il vous montre également comment toostore stocker vos clés de chiffrement dans le certificat de Windows hello.

Always Encrypted est une nouvelle technologie de chiffrement de données dans la base de données SQL Azure et SQL Server qui vous aide à protéger les données sensibles au repos sur le serveur de hello, au cours de déplacement entre client et serveur, et pendant que les données de salutation sont en cours d’utilisation, garantissant que les données sensibles ne s’affiche en tant que texte en clair à l’intérieur du système de base de données hello. Une fois que vous chiffrez les données, uniquement les applications clientes ou les serveurs d’applications qui ont des clés d’accès toohello peuvent accéder aux données de texte en clair. Pour plus d’informations, consultez [Chiffrement intégral (moteur de base de données)](https://msdn.microsoft.com/library/mt163865.aspx).

Après avoir configuré hello toouse de base de données Always Encrypted, vous allez créer une application cliente en c# avec toowork de Visual Studio avec des données hello chiffré.

Suivez les étapes de hello dans cet article de toolearn comment tooset d’Always Encrypted pour une base de données SQL Azure. Dans cet article, vous allez apprendre des tâches de hello tooperform suivant :

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

## <a name="create-a-blank-sql-database"></a>Créer une base de données SQL vide
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Cliquez sur **Nouveau** > **Données + stockage** > **SQL Database**.
3. Créez une base de données **vide** nommée **Clinique** sur un serveur nouveau ou existant. Pour obtenir des instructions détaillées sur la création d’une base de données Bonjour portail Azure, consultez [votre première base de données SQL Azure](sql-database-get-started-portal.md).
   
    ![Créer une base de données vide](./media/sql-database-always-encrypted/create-database.png)

Vous devrez la chaîne de connexion hello plus loin dans le didacticiel de hello. Après la création de la base de données hello, accédez à toohello nouvelle clinique de base de données et copie hello chaîne de connexion. Vous pouvez obtenir la chaîne de connexion hello à tout moment, mais il est facile toocopy il lorsque vous êtes dans hello portail Azure.

1. Cliquez sur **Bases de données SQL** > **Clinique** > **Afficher les chaînes de connexion de la base de données**.
2. Copier la chaîne de connexion hello pour **ADO.NET**.
   
    ![Copier la chaîne de connexion hello](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a>Connexion de base de données toohello avec SSMS
Ouvrez SSMS et se connecter toohello server avec base de données de la clinique hello.

1. Ouvrez SSMS. (Cliquez sur **Connect** > **moteur de base de données** tooopen hello **connecter tooServer** fenêtre si elle n’est pas ouvert).
2. Entrez le nom du serveur et vos informations d’identification. nom du serveur Hello se trouve sur le panneau de base de données SQL hello et dans la chaîne de connexion hello que vous avez copiée précédemment. Notamment de nom complet du serveur de type hello *database.windows.net*.
   
    ![Copier la chaîne de connexion hello](./media/sql-database-always-encrypted/ssms-connect.png)

Si hello **nouvelle règle de pare-feu** s’affiche, connectez-vous à tooAzure et SSMS permettent de créer une règle de pare-feu pour vous.

## <a name="create-a-table"></a>Création d’une table
Dans cette section, vous allez créer des données patient toohold table. Ce sera une table normale au départ, vous allez configurer le chiffrement dans la section suivante de hello.

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
SSMS fournit un Assistant tooeasily configurer Always Encrypted en définissant hello CMK, CEK et les colonnes chiffrées pour vous.

1. Développez **Bases de données** > **Clinique** > **Tables**.
2. Avec le bouton hello **Patients** de table et sélectionnez **chiffrer les colonnes** Assistant de chiffrement intégral hello tooopen :
   
    ![Chiffrer les colonnes](./media/sql-database-always-encrypted/encrypt-columns.png)

Assistant Always Encrypted Hello comprend les sections suivantes de hello : **sélection de la colonne**, **Configuration de la clé principale de** (CMK), **Validation**, et  **Résumé**.

### <a name="column-selection"></a>Sélection de colonnes
Cliquez sur **suivant** sur hello **Introduction** hello tooopen de page **sélection de la colonne** page. Dans cette page, vous sélectionnerez quelles colonnes vous souhaitez tooencrypt, [hello du type de chiffrement et quelle clé de chiffrement de colonne (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.

Chiffrez les informations **SSN** et **BirthDate** pour chaque patient. Hello **SSN** colonne utilise le chiffrement déterministe, qui prend en charge les recherches d’égalité, de jointures et de group by. Hello **BirthDate** colonne utilise le chiffrement aléatoire, qui ne prend pas en charge les opérations.

Ensemble hello **le Type de chiffrement** pour hello **SSN** colonne trop**déterministe** et hello **BirthDate** colonne trop **Aléatoire**. Cliquez sur **Suivant**.

![Chiffrer les colonnes](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a>Configuration de la clé principale
Hello **Master Key Configuration** page est où vous configurez votre clé CMK et le fournisseur de magasin de clés hello sélectionnez où hello CMK sera stocké. Actuellement, vous pouvez stocker une clé CMK dans le magasin de certificats Windows hello, Azure Key Vault ou un module de sécurité matériel (HSM). Ce didacticiel montre comment toostore stocker vos clés de certificat de Windows hello.

Vérifiez que l’option **Magasin de certificats Windows** est sélectionnée, puis cliquez sur **Suivant**.

![Configuration de la clé principale](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a>Validation
Vous pouvez chiffrer les colonnes hello maintenant ou enregistrer un toorun de script PowerShell plus tard. Pour ce didacticiel, sélectionnez **continuer toofinish maintenant** et cliquez sur **suivant**.

### <a name="summary"></a>Résumé
Vérifiez que les paramètres de hello sont correctes, cliquez sur **Terminer** le programme d’installation de toocomplete hello pour Always Encrypted.

![Résumé](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-hello-wizards-actions"></a>Vérifier les actions de l’Assistant hello
Une fois hello Assistant terminé, votre base de données est configurée pour Always Encrypted. Bonjour Bonjour d’Assistant effectué suivant des actions :

* Création d’une CMK.
* Création d’une CEK.
* Hello configuré sélectionné des colonnes pour le chiffrement. Votre **Patients** table a actuellement pas de données, mais les données existantes dans les colonnes hello sélectionné sont désormais chiffrées.

Vous pouvez vérifier la création de hello de clés hello dans SSMS en accédant trop**Clinic** > **sécurité** > **clés Always Encrypted**. Vous pouvez maintenant voir hello nouvelles clés hello généré pour vous par un Assistant.

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a>Créer une application cliente qui fonctionne avec les données de salutation chiffrée
Maintenant que le chiffrement intégral est configuré, vous pouvez générer une application qui effectue *insère* et *sélectionne* sur hello des colonnes chiffrées. toosuccessfully exécuter hello, exemple d’application, vous devez l’exécuter sur hello même ordinateur où vous avez exécuté Assistant Always Encrypted de hello. application de hello toorun sur un autre ordinateur, vous devez déployer votre ordinateur de toohello de certificats Always Encrypted hello client application en cours d’exécution.  

> [!IMPORTANT]
> Votre application doit utiliser [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objets lors du passage du serveur de toohello de données de texte en clair avec des colonnes toujours chiffrées. La transmission de valeurs littérales sans objets SqlParameter entraînera une exception.
> 
> 

1. Ouvrez Visual Studio et créez une nouvelle application console C#. Assurez-vous que votre projet est trop**.NET Framework 4.6** ou version ultérieure.
2. Projet de hello nom **AlwaysEncryptedConsoleApp** et cliquez sur **OK**.

![Nouvelle application de console](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-tooenable-always-encrypted"></a>Modifier votre tooenable de chaîne de connexion Always Encrypted
Cette section explique comment tooenable toujours chiffré dans votre chaîne de connexion de base de données. Vous allez modifier les applications de console hello que vous venez de créer dans la section suivante hello, « Always Encrypted exemple d’application console. »

tooenable Always Encrypted, vous devez tooadd hello **Column Encryption Setting** connexion tooyour de mot clé de chaîne et la définir trop**activé**.

Vous pouvez définir cette option directement dans la chaîne de connexion hello, ou vous pouvez la définir en utilisant un [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx). exemple d’application Hello Bonjour section suivante montre comment toouse **SqlConnectionStringBuilder**.

> [!NOTE]
> Il s’agit de hello seul changement nécessaire dans une application de client spécifique tooAlways chiffré. Si vous avez une application existante qui stocke la chaîne de connexion en externe (autrement dit, dans un fichier de configuration), vous pouvez être en mesure de tooenable Always Encrypted sans modification de code.
> 
> 

### <a name="enable-always-encrypted-in-hello-connection-string"></a>Activer le chiffrement intégral dans la chaîne de connexion hello
Ajoutez hello suivant de chaîne de connexion mot clé tooyour :

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a>Activation du chiffrement intégral avec un paramètre SqlConnectionStringBuilder
Hello de code suivant montre comment tooenable Always Encrypted en définissant hello [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) trop[activé](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a>Exemple d’application console intégralement chiffrée
Cet exemple montre comment :

* Modifiez votre tooenable de chaîne de connexion Always Encrypted.
* Insérer des données dans des colonnes de hello chiffré.
* Sélectionner un enregistrement en filtrant une valeur spécifique dans une colonne chiffrée.

Remplacez le contenu hello de **Program.cs** avec hello suivant de code. Remplacez la chaîne de connexion hello pour la variable de connectionString global hello dans la ligne hello directement au-dessus de la méthode Main de hello avec votre chaîne de connexion valide à partir de hello portail Azure. Il s’agit de hello seule modification que vous avez besoin de toomake toothis code.

Exécuter toosee d’application hello Always Encrypted en action.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;

    namespace AlwaysEncryptedConsoleApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
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

            InsertPatient(new Patient() {
                SSN = "999-99-0001", FirstName = "Orlando", LastName = "Gee", BirthDate = DateTime.Parse("01/04/1964") });
            InsertPatient(new Patient() {
                SSN = "999-99-0002", FirstName = "Keith", LastName = "Harris", BirthDate = DateTime.Parse("06/20/1977") });
            InsertPatient(new Patient() {
                SSN = "999-99-0003", FirstName = "Donna", LastName = "Carreras", BirthDate = DateTime.Parse("02/09/1973") });
            InsertPatient(new Patient() {
                SSN = "999-99-0004", FirstName = "Janet", LastName = "Gates", BirthDate = DateTime.Parse("08/31/1985") });
            InsertPatient(new Patient() {
                SSN = "999-99-0005", FirstName = "Lucy", LastName = "Harrington", BirthDate = DateTime.Parse("05/06/1993") });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
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
Vous pouvez vérifier rapidement le chiffrement des données réelles de hello sur le serveur de hello en interrogeant hello **Patients** données à l’aide de SSMS. (Utilisez votre connexion actuelle où le paramètre de chiffrement de colonne hello n’est pas encore activé.)

Exécutez hello suivant de requête de base de données de la clinique hello.

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

Vous pouvez voir que les colonnes hello chiffré ne contiennent pas toutes les données en texte clair.

   ![Nouvelle application de console](./media/sql-database-always-encrypted/ssms-encrypted.png)

toouse SSMS tooaccess hello des données en texte brut, vous pouvez ajouter des hello **paramètre de chiffrement de colonne = activé** connexion toohello de paramètre.

1. Dans SSMS, cliquez avec le bouton droit sur votre serveur dans **l’Explorateur d’objets**, puis cliquez sur **Déconnexion**.
2. Cliquez sur **Connect** > **moteur de base de données** tooopen hello **connecter tooServer** fenêtre, puis cliquez sur **Options**.
3. Cliquez sur **Paramètres de connexion supplémentaires** et tapez **Column Encryption Setting=enabled**.
   
    ![Nouvelle application de console](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. Exécution hello requête sur hello suivante **Clinic** base de données.
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     Vous pouvez maintenant voir les données de texte en clair hello dans les colonnes hello chiffré.

    ![Nouvelle application de console](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> Si vous vous connectez avec SSMS (ou n’importe quel client) à partir d’un autre ordinateur, il n’aura pas accès aux clés de chiffrement de toohello et ne sera pas en mesure de toodecrypt les données de salutation.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Après avoir créé une base de données qui utilise le chiffrement intégral, vous souhaiterez peut-être suivant de hello toodo :

* Exécuter cet exemple à partir d'un autre ordinateur. Il n’avez pas accès aux clés de chiffrement toohello, donc il n’aura pas accès aux données de texte en clair toohello et ne fonctionnera pas correctement.
* [Faire pivoter et nettoyer vos clés](https://msdn.microsoft.com/library/mt607048.aspx).
* [Migrer des données déjà chiffrées avec le chiffrement intégral](https://msdn.microsoft.com/library/mt621539.aspx).
* [Déployer des ordinateurs du client des tooother de certificats Always Encrypted](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (voir la section de « Rendre tooApplications disponibles des certificats et les utilisateurs » hello).

## <a name="related-information"></a>Informations connexes
* [Chiffrement intégral (développement client)](https://msdn.microsoft.com/library/mt147923.aspx)
* [Chiffrement transparent des données](https://msdn.microsoft.com/library/bb934049.aspx)
* [Chiffrement SQL Server](https://msdn.microsoft.com/library/bb510663.aspx)
* [Assistant Chiffrement intégral.](https://msdn.microsoft.com/library/mt459280.aspx)
* [Blog Chiffrement intégral.](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

