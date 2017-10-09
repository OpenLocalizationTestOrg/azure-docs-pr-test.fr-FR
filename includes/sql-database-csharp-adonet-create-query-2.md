
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a><span data-ttu-id="b7712-101">Exemple de programme C#</span><span class="sxs-lookup"><span data-stu-id="b7712-101">C# program example</span></span>

<span data-ttu-id="b7712-102">Hello sections suivantes vous permettront de cet article présente un programme c# qui utilise ADO.NET toosend Transact-SQL instructions toohello base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="b7712-102">hello next sections of this article present a C# program that uses ADO.NET toosend Transact-SQL statements toohello SQL database.</span></span> <span data-ttu-id="b7712-103">programme de Hello c# exécute hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="b7712-103">hello C# program performs hello following actions:</span></span>

1. <span data-ttu-id="b7712-104">[Se connecte à base de données SQL tooour à l’aide d’ADO.NET](#cs_1_connect).</span><span class="sxs-lookup"><span data-stu-id="b7712-104">[Connects tooour SQL database using ADO.NET](#cs_1_connect).</span></span>
2. <span data-ttu-id="b7712-105">[Création de tableaux](#cs_2_createtables).</span><span class="sxs-lookup"><span data-stu-id="b7712-105">[Creates tables](#cs_2_createtables).</span></span>
3. <span data-ttu-id="b7712-106">[Remplit les tables hello avec des données, en émettant des instructions T-SQL INSERT](#cs_3_insert).</span><span class="sxs-lookup"><span data-stu-id="b7712-106">[Populates hello tables with data, by issuing T-SQL INSERT statements](#cs_3_insert).</span></span>
4. <span data-ttu-id="b7712-107">[Mise à jour des données à l’aide d’une jointure](#cs_4_updatejoin).</span><span class="sxs-lookup"><span data-stu-id="b7712-107">[Updates data by use of a join](#cs_4_updatejoin).</span></span>
5. <span data-ttu-id="b7712-108">[Suppression de données à l’aide d’une jointure](#cs_5_deletejoin).</span><span class="sxs-lookup"><span data-stu-id="b7712-108">[Deletes data by use of a join](#cs_5_deletejoin).</span></span>
6. <span data-ttu-id="b7712-109">[Sélection de lignes de données à l’aide d’une jointure](#cs_6_selectrows).</span><span class="sxs-lookup"><span data-stu-id="b7712-109">[Selects data rows by use of a join](#cs_6_selectrows).</span></span>
7. <span data-ttu-id="b7712-110">Ferme la connexion hello (qui supprime toutes les tables temporaires dans tempdb).</span><span class="sxs-lookup"><span data-stu-id="b7712-110">Closes hello connection (which drops any temporary tables from tempdb).</span></span>

<span data-ttu-id="b7712-111">Hello c# contient :</span><span class="sxs-lookup"><span data-stu-id="b7712-111">hello C# program contains:</span></span>

- <span data-ttu-id="b7712-112">C# code tooconnect toohello base de données de.</span><span class="sxs-lookup"><span data-stu-id="b7712-112">C# code tooconnect toohello database.</span></span>
- <span data-ttu-id="b7712-113">Méthodes qui retournent un code source hello T-SQL.</span><span class="sxs-lookup"><span data-stu-id="b7712-113">Methods that return hello T-SQL source code.</span></span>
- <span data-ttu-id="b7712-114">Deux méthodes qui envoient la base de données toohello hello T-SQL.</span><span class="sxs-lookup"><span data-stu-id="b7712-114">Two methods that submit hello T-SQL toohello database.</span></span>

#### <a name="toocompile-and-run"></a><span data-ttu-id="b7712-115">toocompile et exécution</span><span class="sxs-lookup"><span data-stu-id="b7712-115">toocompile and run</span></span>

<span data-ttu-id="b7712-116">Ce programme C# est, en toute logique, un fichier .cs.</span><span class="sxs-lookup"><span data-stu-id="b7712-116">This C# program is logically one .cs file.</span></span> <span data-ttu-id="b7712-117">Mais ici, programme de hello est physiquement divisée en plusieurs blocs de code, toomake chaque bloc toosee plus facile et à comprendre.</span><span class="sxs-lookup"><span data-stu-id="b7712-117">But here hello program is physically divided into several code blocks, toomake each block easier toosee and understand.</span></span> <span data-ttu-id="b7712-118">toocompile et exécuter ce programme, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b7712-118">toocompile and run this program, do hello following:</span></span>

1. <span data-ttu-id="b7712-119">Créez un projet C# dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b7712-119">Create a C# project in Visual Studio.</span></span>
    - <span data-ttu-id="b7712-120">type de projet Hello doit être un *console* application, d’un élément comme hello suivant la hiérarchie : **modèles** > **Visual C#** > **De bureau Windows classique** > **Console application (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="b7712-120">hello project type should be a *console* application, from something like hello following hierarchy: **Templates** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
3. <span data-ttu-id="b7712-121">Dans le fichier de hello **Program.cs**, effacer hello starter small de lignes de code.</span><span class="sxs-lookup"><span data-stu-id="b7712-121">In hello file **Program.cs**, erase hello small starter lines of code.</span></span>
3. <span data-ttu-id="b7712-122">Dans Program.cs, copie et collage de hello suivant les blocs, hello même séquence, qu'elles sont présentées ici.</span><span class="sxs-lookup"><span data-stu-id="b7712-122">Into Program.cs, copy and paste each of hello following blocks, in hello same sequence they are presented here.</span></span>
4. <span data-ttu-id="b7712-123">Dans le fichier Program.cs, suivant hello de modifier les valeurs Bonjour **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="b7712-123">In Program.cs, edit hello following values in hello **Main** method:</span></span>

   - <span data-ttu-id="b7712-124">**cb.DataSource**</span><span class="sxs-lookup"><span data-stu-id="b7712-124">**cb.DataSource**</span></span>
   - <span data-ttu-id="b7712-125">**cd.UserID**</span><span class="sxs-lookup"><span data-stu-id="b7712-125">**cd.UserID**</span></span>
   - <span data-ttu-id="b7712-126">**cb.Password**</span><span class="sxs-lookup"><span data-stu-id="b7712-126">**cb.Password**</span></span>
   - <span data-ttu-id="b7712-127">**InitialCatalog**</span><span class="sxs-lookup"><span data-stu-id="b7712-127">**InitialCatalog**</span></span>

5. <span data-ttu-id="b7712-128">Vérifiez que cet assembly hello **System.Data.dll** est référencé.</span><span class="sxs-lookup"><span data-stu-id="b7712-128">Verify that hello assembly **System.Data.dll** is referenced.</span></span> <span data-ttu-id="b7712-129">tooverify, développez hello **références** nœud Bonjour **l’Explorateur de solutions** volet.</span><span class="sxs-lookup"><span data-stu-id="b7712-129">tooverify, expand hello **References** node in hello **Solution Explorer** pane.</span></span>
6. <span data-ttu-id="b7712-130">programme de hello toobuild dans Visual Studio, cliquez sur hello **générer** menu.</span><span class="sxs-lookup"><span data-stu-id="b7712-130">toobuild hello program in Visual Studio, click hello **Build** menu.</span></span>
7. <span data-ttu-id="b7712-131">programme de hello toorun à partir de Visual Studio, cliquez sur hello **Démarrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="b7712-131">toorun hello program from Visual Studio, click hello **Start** button.</span></span> <span data-ttu-id="b7712-132">le résultat du rapport Hello s’affiche dans une fenêtre cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="b7712-132">hello report output is displayed in a cmd.exe window.</span></span>

> [!NOTE]
> <span data-ttu-id="b7712-133">Vous pouvez hello modification hello T-SQL tooadd début  **#**  toohello les noms de table qui crée les tables temporaires que dans **tempdb**.</span><span class="sxs-lookup"><span data-stu-id="b7712-133">You have hello option of editing hello T-SQL tooadd a leading **#** toohello table names, which creates them as temporary tables in **tempdb**.</span></span> <span data-ttu-id="b7712-134">Cela peut être utile lors de démonstrations, si aucune base de données test n’est disponible.</span><span class="sxs-lookup"><span data-stu-id="b7712-134">This can be useful for demonstration purposes, when no test database is available.</span></span> <span data-ttu-id="b7712-135">Les tables temporaires sont automatiquement supprimés lors de la fermeture de la connexion hello.</span><span class="sxs-lookup"><span data-stu-id="b7712-135">Temporary tables are deleted automatically when hello connection closes.</span></span> <span data-ttu-id="b7712-136">Toutes les références (REFERENCES) de clés étrangères ne sont pas appliquées pour les tables temporaires.</span><span class="sxs-lookup"><span data-stu-id="b7712-136">Any REFERENCES for foreign keys are not enforced for temporary tables.</span></span>
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a><span data-ttu-id="b7712-137">Bloc 1 C# : Connexion via ADO.NET</span><span class="sxs-lookup"><span data-stu-id="b7712-137">C# block 1: Connect by using ADO.NET</span></span>

- [<span data-ttu-id="b7712-138">Next</span><span class="sxs-lookup"><span data-stu-id="b7712-138">Next</span></span>](#cs_2_createtables)


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
### <a name="c-block-2-t-sql-toocreate-tables"></a><span data-ttu-id="b7712-139">Bloc c# 2 : tables toocreate de T-SQL</span><span class="sxs-lookup"><span data-stu-id="b7712-139">C# block 2: T-SQL toocreate tables</span></span>

- <span data-ttu-id="b7712-140">[Précédent](#cs_1_connect)&nbsp; / &nbsp;[Suivant](#cs_3_insert)</span><span class="sxs-lookup"><span data-stu-id="b7712-140">[Previous](#cs_1_connect) &nbsp; / &nbsp; [Next](#cs_3_insert)</span></span>

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

#### <a name="entity-relationship-diagram-erd"></a><span data-ttu-id="b7712-141">Diagramme des relations d’entité (ERD)</span><span class="sxs-lookup"><span data-stu-id="b7712-141">Entity Relationship Diagram (ERD)</span></span>

<span data-ttu-id="b7712-142">les instructions CREATE TABLE ci-dessus Hello impliquent hello **références** mot clé toocreate un *clé étrangère* relation (FK) entre deux tables.</span><span class="sxs-lookup"><span data-stu-id="b7712-142">hello preceding CREATE TABLE statements involve hello **REFERENCES** keyword toocreate a *foreign key* (FK) relationship between two tables.</span></span>  <span data-ttu-id="b7712-143">Si vous utilisez tempdb, commentez hello `--REFERENCES` (mot clé) à l’aide d’une paire de début des tirets.</span><span class="sxs-lookup"><span data-stu-id="b7712-143">If you are using tempdb, comment out hello `--REFERENCES` keyword using a pair of leading dashes.</span></span>

<span data-ttu-id="b7712-144">L’élément suivant est une disquette qui affiche la relation de hello entre deux tables de hello.</span><span class="sxs-lookup"><span data-stu-id="b7712-144">Next is an ERD that displays hello relationship between hello two tables.</span></span> <span data-ttu-id="b7712-145">Hello valeurs hello #tabEmployee.DepartmentCode *enfant* colonne sont des valeurs de toohello limité présents dans hello #tabDepartment.Department *parent* colonne.</span><span class="sxs-lookup"><span data-stu-id="b7712-145">hello values in hello #tabEmployee.DepartmentCode *child* column are limited toohello values present in hello #tabDepartment.Department *parent* column.</span></span>

![Diagramme affichant la clé étrangère](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-tooinsert-data"></a><span data-ttu-id="b7712-147">Bloc c# 3 : données tooinsert de T-SQL</span><span class="sxs-lookup"><span data-stu-id="b7712-147">C# block 3: T-SQL tooinsert data</span></span>

- <span data-ttu-id="b7712-148">[Précédent](#cs_2_createtables)&nbsp; / &nbsp;[Suivant](#cs_4_updatejoin)</span><span class="sxs-lookup"><span data-stu-id="b7712-148">[Previous](#cs_2_createtables) &nbsp; / &nbsp; [Next](#cs_4_updatejoin)</span></span>


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
### <a name="c-block-4-t-sql-tooupdate-join"></a><span data-ttu-id="b7712-149">Bloc c# 4 : jointure tooupdate T-SQL</span><span class="sxs-lookup"><span data-stu-id="b7712-149">C# block 4: T-SQL tooupdate-join</span></span>

- <span data-ttu-id="b7712-150">[Précédent](#cs_3_insert)&nbsp; / &nbsp;[Suivant](#cs_5_deletejoin)</span><span class="sxs-lookup"><span data-stu-id="b7712-150">[Previous](#cs_3_insert) &nbsp; / &nbsp; [Next](#cs_5_deletejoin)</span></span>


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
### <a name="c-block-5-t-sql-toodelete-join"></a><span data-ttu-id="b7712-151">Bloc c# 5 : jointure toodelete T-SQL</span><span class="sxs-lookup"><span data-stu-id="b7712-151">C# block 5: T-SQL toodelete-join</span></span>

- <span data-ttu-id="b7712-152">[Précédent](#cs_4_updatejoin)&nbsp; / &nbsp;[Suivant](#cs_6_selectrows)</span><span class="sxs-lookup"><span data-stu-id="b7712-152">[Previous](#cs_4_updatejoin) &nbsp; / &nbsp; [Next](#cs_6_selectrows)</span></span>


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
### <a name="c-block-6-t-sql-tooselect-rows"></a><span data-ttu-id="b7712-153">Bloc c# 6 : lignes de tooselect T-SQL</span><span class="sxs-lookup"><span data-stu-id="b7712-153">C# block 6: T-SQL tooselect rows</span></span>

- <span data-ttu-id="b7712-154">[Précédent](#cs_5_deletejoin)&nbsp; / &nbsp;[Suivant](#cs_6b_datareader)</span><span class="sxs-lookup"><span data-stu-id="b7712-154">[Previous](#cs_5_deletejoin) &nbsp; / &nbsp; [Next](#cs_6b_datareader)</span></span>


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
### <a name="c-block-6b-executereader"></a><span data-ttu-id="b7712-155">Bloc 6b C# : ExecuteReader</span><span class="sxs-lookup"><span data-stu-id="b7712-155">C# block 6b: ExecuteReader</span></span>

- <span data-ttu-id="b7712-156">[Précédent](#cs_6_selectrows)&nbsp; / &nbsp;[Suivant](#cs_7_executenonquery)</span><span class="sxs-lookup"><span data-stu-id="b7712-156">[Previous](#cs_6_selectrows) &nbsp; / &nbsp; [Next](#cs_7_executenonquery)</span></span>

<span data-ttu-id="b7712-157">Cette méthode est l’instruction de T-SQL SELECT toorun conçue hello qui est générée par hello **Build_6_Tsql_SelectEmployees** (méthode).</span><span class="sxs-lookup"><span data-stu-id="b7712-157">This method is designed toorun hello T-SQL SELECT statement that is built by hello **Build_6_Tsql_SelectEmployees** method.</span></span>


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
### <a name="c-block-7-executenonquery"></a><span data-ttu-id="b7712-158">Bloc 7 C# : ExecuteNonQuery</span><span class="sxs-lookup"><span data-stu-id="b7712-158">C# block 7: ExecuteNonQuery</span></span>

- <span data-ttu-id="b7712-159">[Précédent](#cs_6b_datareader)&nbsp; / &nbsp;[Suivant](#cs_8_output)</span><span class="sxs-lookup"><span data-stu-id="b7712-159">[Previous](#cs_6b_datareader) &nbsp; / &nbsp; [Next](#cs_8_output)</span></span>

<span data-ttu-id="b7712-160">Cette méthode est appelée pour les opérations qui modifient le contenu des données des tables hello sans retourner toutes les lignes de données.</span><span class="sxs-lookup"><span data-stu-id="b7712-160">This method is called for operations that modify hello data content of tables without returning any data rows.</span></span>


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
### <a name="c-block-8-actual-test-output-toohello-console"></a><span data-ttu-id="b7712-161">Bloc c# 8 : console de test réel sortie toohello</span><span class="sxs-lookup"><span data-stu-id="b7712-161">C# block 8: Actual test output toohello console</span></span>

- [<span data-ttu-id="b7712-162">Précédent</span><span class="sxs-lookup"><span data-stu-id="b7712-162">Previous</span></span>](#cs_7_executenonquery)

<span data-ttu-id="b7712-163">Cette section capture la sortie hello hello programme envoyés toohello console.</span><span class="sxs-lookup"><span data-stu-id="b7712-163">This section captures hello output that hello program sent toohello console.</span></span> <span data-ttu-id="b7712-164">Seules les valeurs guid hello varient entre les séries de tests.</span><span class="sxs-lookup"><span data-stu-id="b7712-164">Only hello guid values vary between test runs.</span></span>


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
