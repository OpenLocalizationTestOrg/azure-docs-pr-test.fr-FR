
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a>Exemple de programme C#

Hello sections suivantes vous permettront de cet article présente un programme c# qui utilise ADO.NET toosend Transact-SQL instructions toohello base de données SQL. programme de Hello c# exécute hello suivant des actions :

1. [Se connecte à base de données SQL tooour à l’aide d’ADO.NET](#cs_1_connect).
2. [Création de tableaux](#cs_2_createtables).
3. [Remplit les tables hello avec des données, en émettant des instructions T-SQL INSERT](#cs_3_insert).
4. [Mise à jour des données à l’aide d’une jointure](#cs_4_updatejoin).
5. [Suppression de données à l’aide d’une jointure](#cs_5_deletejoin).
6. [Sélection de lignes de données à l’aide d’une jointure](#cs_6_selectrows).
7. Ferme la connexion hello (qui supprime toutes les tables temporaires dans tempdb).

Hello c# contient :

- C# code tooconnect toohello base de données de.
- Méthodes qui retournent un code source hello T-SQL.
- Deux méthodes qui envoient la base de données toohello hello T-SQL.

#### <a name="toocompile-and-run"></a>toocompile et exécution

Ce programme C# est, en toute logique, un fichier .cs. Mais ici, programme de hello est physiquement divisée en plusieurs blocs de code, toomake chaque bloc toosee plus facile et à comprendre. toocompile et exécuter ce programme, hello suivant :

1. Créez un projet C# dans Visual Studio.
    - type de projet Hello doit être un *console* application, d’un élément comme hello suivant la hiérarchie : **modèles** > **Visual C#** > **De bureau Windows classique** > **Console application (.NET Framework)**.
3. Dans le fichier de hello **Program.cs**, effacer hello starter small de lignes de code.
3. Dans Program.cs, copie et collage de hello suivant les blocs, hello même séquence, qu'elles sont présentées ici.
4. Dans le fichier Program.cs, suivant hello de modifier les valeurs Bonjour **Main** méthode :

   - **cb.DataSource**
   - **cd.UserID**
   - **cb.Password**
   - **InitialCatalog**

5. Vérifiez que cet assembly hello **System.Data.dll** est référencé. tooverify, développez hello **références** nœud Bonjour **l’Explorateur de solutions** volet.
6. programme de hello toobuild dans Visual Studio, cliquez sur hello **générer** menu.
7. programme de hello toorun à partir de Visual Studio, cliquez sur hello **Démarrer** bouton. le résultat du rapport Hello s’affiche dans une fenêtre cmd.exe.

> [!NOTE]
> Vous pouvez hello modification hello T-SQL tooadd début  **#**  toohello les noms de table qui crée les tables temporaires que dans **tempdb**. Cela peut être utile lors de démonstrations, si aucune base de données test n’est disponible. Les tables temporaires sont automatiquement supprimés lors de la fermeture de la connexion hello. Toutes les références (REFERENCES) de clés étrangères ne sont pas appliquées pour les tables temporaires.
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a>Bloc 1 C# : Connexion via ADO.NET

- [Next](#cs_2_createtables)


```csharp
using System;
using System.Data.SqlClient;   // System.Data.dll 
//using System.Data;           // For:  SqlDbType , ParameterDirection

namespace csharp_db_test
{
   class Program
   {
      static void Main(string[] args)
      {
         try
         {
            var cb = new SqlConnectionStringBuilder();
            cb.DataSource = "your_server.database.windows.net";
            cb.UserID = "your_user";
            cb.Password = "your_password";
            cb.InitialCatalog = "your_database";

            using (var connection = new SqlConnection(cb.ConnectionString))
            {
               connection.Open();

               Submit_Tsql_NonQuery(connection, "2 - Create-Tables",
                  Build_2_Tsql_CreateTables());

               Submit_Tsql_NonQuery(connection, "3 - Inserts",
                  Build_3_Tsql_Inserts());

               Submit_Tsql_NonQuery(connection, "4 - Update-Join",
                  Build_4_Tsql_UpdateJoin(),
                  "@csharpParmDepartmentName", "Accounting");

               Submit_Tsql_NonQuery(connection, "5 - Delete-Join",
                  Build_5_Tsql_DeleteJoin(),
                  "@csharpParmDepartmentName", "Legal");

               Submit_6_Tsql_SelectEmployees(connection);
            }
         }
         catch (SqlException e)
         {
            Console.WriteLine(e.ToString());
         }
         Console.WriteLine("View hello report output here, then press any key tooend hello program...");
         Console.ReadKey();
      }
```


<a name="cs_2_createtables"/>
### <a name="c-block-2-t-sql-toocreate-tables"></a>Bloc c# 2 : tables toocreate de T-SQL

- [Précédent](#cs_1_connect)&nbsp; / &nbsp;[Suivant](#cs_3_insert)

```csharp
      static string Build_2_Tsql_CreateTables()
      {
         return @"
DROP TABLE IF EXISTS tabEmployee;
DROP TABLE IF EXISTS tabDepartment;  -- Drop parent table last.


CREATE TABLE tabDepartment
(
   DepartmentCode  nchar(4)          not null
      PRIMARY KEY,
   DepartmentName  nvarchar(128)     not null
);

CREATE TABLE tabEmployee
(
   EmployeeGuid    uniqueIdentifier  not null  default NewId()
      PRIMARY KEY,
   EmployeeName    nvarchar(128)     not null,
   EmployeeLevel   int               not null,
   DepartmentCode  nchar(4)              null
      REFERENCES tabDepartment (DepartmentCode)  -- (REFERENCES would be disallowed on temporary tables.)
);
";
      }
```

#### <a name="entity-relationship-diagram-erd"></a>Diagramme des relations d’entité (ERD)

les instructions CREATE TABLE ci-dessus Hello impliquent hello **références** mot clé toocreate un *clé étrangère* relation (FK) entre deux tables.  Si vous utilisez tempdb, commentez hello `--REFERENCES` (mot clé) à l’aide d’une paire de début des tirets.

L’élément suivant est une disquette qui affiche la relation de hello entre deux tables de hello. Hello valeurs hello #tabEmployee.DepartmentCode *enfant* colonne sont des valeurs de toohello limité présents dans hello #tabDepartment.Department *parent* colonne.

![Diagramme affichant la clé étrangère](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-tooinsert-data"></a>Bloc c# 3 : données tooinsert de T-SQL

- [Précédent](#cs_2_createtables)&nbsp; / &nbsp;[Suivant](#cs_4_updatejoin)


```csharp
      static string Build_3_Tsql_Inserts()
      {
         return @"
-- hello company has these departments.
INSERT INTO tabDepartment
   (DepartmentCode, DepartmentName)
      VALUES
   ('acct', 'Accounting'),
   ('hres', 'Human Resources'),
   ('legl', 'Legal');

-- hello company has these employees, each in one department.
INSERT INTO tabEmployee
   (EmployeeName, EmployeeLevel, DepartmentCode)
      VALUES
   ('Alison'  , 19, 'acct'),
   ('Barbara' , 17, 'hres'),
   ('Carol'   , 21, 'acct'),
   ('Deborah' , 24, 'legl'),
   ('Elle'    , 15, null);
";
      }
```


<a name="cs_4_updatejoin"/>
### <a name="c-block-4-t-sql-tooupdate-join"></a>Bloc c# 4 : jointure tooupdate T-SQL

- [Précédent](#cs_3_insert)&nbsp; / &nbsp;[Suivant](#cs_5_deletejoin)


```csharp
      static string Build_4_Tsql_UpdateJoin()
      {
         return @"
DECLARE @DName1  nvarchar(128) = @csharpParmDepartmentName;  --'Accounting';


-- Promote everyone in one department (see @parm...).
UPDATE empl
   SET
      empl.EmployeeLevel += 1
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName1;
";
      }
```


<a name="cs_5_deletejoin"/>
### <a name="c-block-5-t-sql-toodelete-join"></a>Bloc c# 5 : jointure toodelete T-SQL

- [Précédent](#cs_4_updatejoin)&nbsp; / &nbsp;[Suivant](#cs_6_selectrows)


```csharp
      static string Build_5_Tsql_DeleteJoin()
      {
         return @"
DECLARE @DName2  nvarchar(128);
SET @DName2 = @csharpParmDepartmentName;  --'Legal';


-- Right size hello Legal department.
DELETE empl
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName2

-- Disband hello Legal department.
DELETE tabDepartment
   WHERE DepartmentName = @DName2;
";
      }
```



<a name="cs_6_selectrows"/>
### <a name="c-block-6-t-sql-tooselect-rows"></a>Bloc c# 6 : lignes de tooselect T-SQL

- [Précédent](#cs_5_deletejoin)&nbsp; / &nbsp;[Suivant](#cs_6b_datareader)


```csharp
      static string Build_6_Tsql_SelectEmployees()
      {
         return @"
-- Look at all hello final Employees.
SELECT
      empl.EmployeeGuid,
      empl.EmployeeName,
      empl.EmployeeLevel,
      empl.DepartmentCode,
      dept.DepartmentName
   FROM
      tabEmployee   as empl
      LEFT OUTER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   ORDER BY
      EmployeeName;
";
      }
```


<a name="cs_6b_datareader"/>
### <a name="c-block-6b-executereader"></a>Bloc 6b C# : ExecuteReader

- [Précédent](#cs_6_selectrows)&nbsp; / &nbsp;[Suivant](#cs_7_executenonquery)

Cette méthode est l’instruction de T-SQL SELECT toorun conçue hello qui est générée par hello **Build_6_Tsql_SelectEmployees** (méthode).


```csharp
      static void Submit_6_Tsql_SelectEmployees(SqlConnection connection)
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("Now, SelectEmployees (6)...");

         string tsql = Build_6_Tsql_SelectEmployees();

         using (var command = new SqlCommand(tsql, connection))
         {
            using (SqlDataReader reader = command.ExecuteReader())
            {
               while (reader.Read())
               {
                  Console.WriteLine("{0} , {1} , {2} , {3} , {4}",
                     reader.GetGuid(0),
                     reader.GetString(1),
                     reader.GetInt32(2),
                     (reader.IsDBNull(3)) ? "NULL" : reader.GetString(3),
                     (reader.IsDBNull(4)) ? "NULL" : reader.GetString(4));
               }
            }
         }
      }
```


<a name="cs_7_executenonquery"/>
### <a name="c-block-7-executenonquery"></a>Bloc 7 C# : ExecuteNonQuery

- [Précédent](#cs_6b_datareader)&nbsp; / &nbsp;[Suivant](#cs_8_output)

Cette méthode est appelée pour les opérations qui modifient le contenu des données des tables hello sans retourner toutes les lignes de données.


```csharp
      static void Submit_Tsql_NonQuery(
         SqlConnection connection,
         string tsqlPurpose,
         string tsqlSourceCode,
         string parameterName = null,
         string parameterValue = null
         )
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("T-SQL too{0}...", tsqlPurpose);

         using (var command = new SqlCommand(tsqlSourceCode, connection))
         {
            if (parameterName != null)
            {
               command.Parameters.AddWithValue(  // Or, use SqlParameter class.
                  parameterName,
                  parameterValue);
            }
            int rowsAffected = command.ExecuteNonQuery();
            Console.WriteLine(rowsAffected + " = rows affected.");
         }
      }
   } // EndOfClass
}
```


<a name="cs_8_output"/>
### <a name="c-block-8-actual-test-output-toohello-console"></a>Bloc c# 8 : console de test réel sortie toohello

- [Précédent](#cs_7_executenonquery)

Cette section capture la sortie hello hello programme envoyés toohello console. Seules les valeurs guid hello varient entre les séries de tests.


```text
[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>> csharp_db_test.exe

=================================
Now, CreateTables (10)...

=================================
Now, Inserts (20)...

=================================
Now, UpdateJoin (30)...
2 rows affected, by UpdateJoin.

=================================
Now, DeleteJoin (40)...

=================================
Now, SelectEmployees (50)...
0199be49-a2ed-4e35-94b7-e936acf1cd75 , Alison , 20 , acct , Accounting
f0d3d147-64cf-4420-b9f9-76e6e0a32567 , Barbara , 17 , hres , Human Resources
cf4caede-e237-42d2-b61d-72114c7e3afa , Carol , 22 , acct , Accounting
cdde7727-bcfd-4f72-a665-87199c415f8b , Elle , 15 , NULL , NULL

[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>>
```
