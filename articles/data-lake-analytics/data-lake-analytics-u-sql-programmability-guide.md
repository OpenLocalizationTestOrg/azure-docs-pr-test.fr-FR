---
title: "Guide de programmabilité U-SQL pour Azure Data Lake | Microsoft Docs"
description: "Découvrez l’ensemble de services dans Azure Data Lake qui vous permettent de créer une plateforme Big Data basée sur le cloud."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
ms.assetid: 63be271e-7c44-4d19-9897-c2913ee9599d
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: saveenr
ms.openlocfilehash: e4e298475d7be7d51c8bd55be498371ed6ce77a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="4b0d4-103">Guide de programmabilité U-SQL</span><span class="sxs-lookup"><span data-stu-id="4b0d4-103">U-SQL programmability guide</span></span>

<span data-ttu-id="4b0d4-104">U-SQL est un langage de requête spécifiquement conçu pour les charges de travail de type Big Data.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="4b0d4-105">L’une des fonctionnalités uniques du langage U-SQL est la combinaison d’un langage déclaratif de type SQL avec l’extensibilité et la programmabilité offertes par C#.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-105">One of the unique features of U-SQL is the combination of the SQL-like declarative language with the extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="4b0d4-106">Ce guide se concentre sur l’extensibilité et la programmabilité du langage U-SQL que permet C#.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-106">In this guide, we concentrate on the extensibility and programmability of the U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="4b0d4-107">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="4b0d4-107">Requirements</span></span>

<span data-ttu-id="4b0d4-108">Téléchargez et installez [Azure Data Lake Tools pour Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="4b0d4-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="4b0d4-109">Prise en main de U-SQL</span><span class="sxs-lookup"><span data-stu-id="4b0d4-109">Get started with U-SQL</span></span>  

<span data-ttu-id="4b0d4-110">Intéressons-nous au script U-SQL suivant :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-110">Let’s look at the following U-SQL script:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso",   1500.0, "2017-03-39"),
            ("Woodgrove", 2700.0, "2017-04-10")
        ) AS 
              D( customer, amount );
@results =
    SELECT
        customer,
    amount,
    date
    FROM @a;    
```

<span data-ttu-id="4b0d4-111">Il définit un ensemble de lignes appelé @a et crée un ensemble de lignes appelé @results de @a.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="4b0d4-112">Types et expressions C# dans les scripts U-SQL</span><span class="sxs-lookup"><span data-stu-id="4b0d4-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="4b0d4-113">Une Expression U-SQL est une expression C# combinée à des opérations logiques U-SQL comme `AND`, `OR` et `NOT`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="4b0d4-114">Les expressions U-SQL peuvent être utilisées avec SELECT, EXTRACT, WHERE, HAVING, GROUP BY et DECLARE.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="4b0d4-115">Par exemple, le script suivant analyse une chaîne de valeur DateTime dans la clause SELECT.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-115">For example, the following script parses a string a DateTime value in the SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="4b0d4-116">Le script suivant analyse une chaîne de valeur DateTime dans une instruction DECLARE.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-116">The following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="4b0d4-117">Utiliser des expressions C# pour les conversions de types de données</span><span class="sxs-lookup"><span data-stu-id="4b0d4-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="4b0d4-118">L’exemple suivant montre comment faire une conversion de données datetime en utilisant des expressions C#.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-118">The following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="4b0d4-119">Dans ce scénario, les données datetime de chaîne sont converties en données datetime standard avec la notation d’heure 00:00:00 (minuit).</span><span class="sxs-lookup"><span data-stu-id="4b0d4-119">In this particular scenario, string datetime data is converted to standard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="4b0d4-120">Utiliser des expressions C# pour la date du jour</span><span class="sxs-lookup"><span data-stu-id="4b0d4-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="4b0d4-121">Pour extraire la date du jour, nous pouvons utiliser l’expression C# suivante :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-121">To pull today’s date, we can use the following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="4b0d4-122">Voici un exemple montrant comment utiliser cette expression dans un script :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-122">Here's an example of how to use this expression in a script:</span></span>

```
@rs1 =
    SELECT
        MAX(guid) AS start_id,
        MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        user,
        des
    FROM @rs0
    GROUP BY user, des;
```



## <a name="using-net-assemblies"></a><span data-ttu-id="4b0d4-123">Avec des assemblys .NET</span><span class="sxs-lookup"><span data-stu-id="4b0d4-123">Using .NET assemblies</span></span>
<span data-ttu-id="4b0d4-124">Le modèle d’extensibilité de U-SQL dépend largement de la possibilité d’ajouter du code personnalisé.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-124">U-SQL’s extensibility model relies heavily on the ability to add custom code.</span></span> <span data-ttu-id="4b0d4-125">Actuellement, U-SQL vous offre des moyens faciles pour ajouter votre propre code basé sur Microsoft .NET (en particulier, C#).</span><span class="sxs-lookup"><span data-stu-id="4b0d4-125">Currently, U-SQL provides you with easy ways to add your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="4b0d4-126">Toutefois, vous pouvez également ajouter du code personnalisé écrit dans d’autres langages .NET, tels que VB.NET ou F #.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="4b0d4-127">Enregistrer un assembly .NET</span><span class="sxs-lookup"><span data-stu-id="4b0d4-127">Register a .NET assembly</span></span>

<span data-ttu-id="4b0d4-128">Utilisez l’instruction CREATE ASSEMBLY pour placer un assembly .NET dans une base de données U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-128">Use the CREATE ASSEMBLY statement to place a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="4b0d4-129">Lorsqu’un assembly est placé dans une base de données, les scripts U-SQL peuvent utiliser ces assemblys à l’aide de l’instruction REFERENCE ASSEMBLY.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using the REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="4b0d4-130">Le code suivant illustre comment enregistrer un assembly :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-130">The following code shows how to register an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="4b0d4-131">Le code suivant illustre comment référencer un assembly :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-131">The following code shows how to reference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="4b0d4-132">Consultez les [instructions d’enregistrement des assemblys](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) qui traitent de ce sujet plus en détail.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-132">Consult the [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="4b0d4-133">Utilisez le contrôle de version des assemblys</span><span class="sxs-lookup"><span data-stu-id="4b0d4-133">Use assembly versioning</span></span>
<span data-ttu-id="4b0d4-134">Actuellement, U-SQL utilise .NET Framework version 4.5.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-134">Currently, U-SQL uses the .NET Framework version 4.5.</span></span> <span data-ttu-id="4b0d4-135">Par conséquent, vérifiez que vos propres assemblys sont compatibles avec cette version du runtime.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-135">So ensure that your own assemblies are compatible with that version of the runtime.</span></span>

<span data-ttu-id="4b0d4-136">Comme mentionné précédemment, U-SQL exécute le code dans un format 64 bits (x64).</span><span class="sxs-lookup"><span data-stu-id="4b0d4-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="4b0d4-137">Par conséquent, assurez-vous que votre code est compilé pour s’exécuter sur des systèmes x64.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-137">So make sure that your code is compiled to run on x64.</span></span> <span data-ttu-id="4b0d4-138">Dans le cas contraire, vous recevez l’erreur de format incorrect vue précédemment.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-138">Otherwise you get the incorrect format error shown earlier.</span></span>

<span data-ttu-id="4b0d4-139">Chaque DLL d’assembly ou fichier de ressources chargé, comme un runtime différent, un assembly natif ou un fichier de configuration peut être de 400 Mo maximum.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="4b0d4-140">La taille totale des ressources déployées, via l’instruction DEPLOY RESOURCE ou via des références aux assemblys et leurs fichiers supplémentaires, ne peut pas dépasser 3 Go.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-140">The total size of deployed resources, either via DEPLOY RESOURCE or via references to assemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="4b0d4-141">Enfin, notez que chaque base de données U-SQL ne peut contenir qu’une seule version d’un assembly donné.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="4b0d4-142">Par exemple, si vous avez besoin à la fois des versions 7 et 8 de la bibliothèque NewtonSoft Json.Net, vous devez les enregistrer dans deux bases de données distinctes.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-142">For example, if you need both version 7 and version 8 of the NewtonSoft Json.Net library, you need to register them in two different databases.</span></span> <span data-ttu-id="4b0d4-143">En outre, chaque script ne peut faire référence qu’à une seule version d’une DLL d’assembly donnée.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-143">Furthermore, each script can only refer to one version of a given assembly DLL.</span></span> <span data-ttu-id="4b0d4-144">À cet égard, U-SQL suit la sémantique de gestion et de contrôle de version d’assembly C#.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-144">In this respect, U-SQL follows the C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="4b0d4-145">Utiliser les fonctions définies par l’utilisateur : UDF</span><span class="sxs-lookup"><span data-stu-id="4b0d4-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="4b0d4-146">Les fonctions U-SQL définies par l’utilisateur (ou UDF) sont des routines de programmation qui acceptent des paramètres, effectuent une action (telle qu’un calcul complexe) et retournent le résultat de celle-ci en tant que valeur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return the result of that action as a value.</span></span> <span data-ttu-id="4b0d4-147">La valeur de retour d’une fonction définie par l’utilisateur ne peut être qu’une valeur scalaire unique.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-147">The return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="4b0d4-148">Une fonction définie par l’utilisateur U-SQL peut être appelée dans un script U-SQL de base comme toute autre fonction scalaire C#.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="4b0d4-149">Nous vous recommandons d’initialiser les fonctions définies par l’utilisateur U-SQL en tant que **publiques** et **statiques**.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="4b0d4-150">Examinons d’abord l’exemple simple de création d’une fonction définie par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-150">First let’s look at the simple example of creating a UDF.</span></span>

<span data-ttu-id="4b0d4-151">Dans ce scénario d’utilisation, nous devons déterminer la période fiscale, le trimestre et le mois fiscal de la première connexion de l’utilisateur spécifique inclus.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-151">In this use-case scenario, we need to determine the fiscal period, including the fiscal quarter and fiscal month of the first sign-in for the specific user.</span></span> <span data-ttu-id="4b0d4-152">Le premier mois fiscal de l’année dans notre scénario est juin.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-152">The first fiscal month of the year in our scenario is June.</span></span>

<span data-ttu-id="4b0d4-153">Pour calculer la période fiscale, nous introduisons la fonction C# suivante :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-153">To calculate fiscal period, we introduce the following C# function:</span></span>

```
public static string GetFiscalPeriod(DateTime dt)
{
    int FiscalMonth=0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter=0;
    if (FiscalMonth >=1 && FiscalMonth<=3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return "Q" + FiscalQuarter.ToString() + ":P" + FiscalMonth.ToString();
}
```

<span data-ttu-id="4b0d4-154">La fonction calcule simplement le trimestre et le mois fiscaux, puis retourne une valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="4b0d4-155">Pour le mois de juin, premier mois du premier trimestre fiscal, nous utilisons « Q1:P1 ».</span><span class="sxs-lookup"><span data-stu-id="4b0d4-155">For June, the first month of the first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="4b0d4-156">Pour le mois de juillet, nous utilisons « Q1:P2 », etc.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="4b0d4-157">Il s’agit d’une fonction C# standard que nous allons utiliser dans notre projet U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-157">This is a regular C# function that we are going to use in our U-SQL project.</span></span>

<span data-ttu-id="4b0d4-158">La section code-behind dans ce scénario se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-158">Here is how the code-behind section looks in this scenario:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        public static string GetFiscalPeriod(DateTime dt)
        {
            int FiscalMonth=0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter=0;
            if (FiscalMonth >=1 && FiscalMonth<=3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return "Q" + FiscalQuarter.ToString() + ":" + FiscalMonth.ToString();
        }

    }

}
```

<span data-ttu-id="4b0d4-159">Nous allons maintenant appeler cette fonction à partir du script U-SQL de base.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-159">Now we are going to call this function from the base U-SQL script.</span></span> <span data-ttu-id="4b0d4-160">Pour ce faire, nous devons fournir un nom complet pour la fonction, qui inclut l’espace de noms, dans ce cas : NameSpace.Class.Function(paramètre).</span><span class="sxs-lookup"><span data-stu-id="4b0d4-160">To do this, we have to provide a fully qualified name for the function, including the namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="4b0d4-161">Le script de base U-SQL réel est le suivant :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-161">Following is the actual U-SQL base script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt DateTime,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

DECLARE @default_dt DateTime = Convert.ToDateTime("06/01/2016");

@rs1 =
    SELECT
        MAX(guid) AS start_id,
    MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        user,
        des
    FROM @rs0
    GROUP BY user, des;

OUTPUT @rs1 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="4b0d4-162">Le fichier de sortie résultant de l’exécution du script est le suivant :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-162">Following is the output file of the script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="4b0d4-163">Cet exemple illustre une utilisation simple d’une fonction définie par l’utilisateur inline dans U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="4b0d4-164">Conserver l’état entre des appels de fonction définie par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4b0d4-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="4b0d4-165">Des objets de programmabilité C# U-SQL peuvent être plus sophistiqués en utilisant une interactivité via des variables globales code-behind.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through the code-behind global variables.</span></span> <span data-ttu-id="4b0d4-166">Examinons le scénario d’utilisation professionnelle suivant :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-166">Let’s look at the following business use-case scenario.</span></span>

<span data-ttu-id="4b0d4-167">Dans les grandes organisations, les utilisateurs peuvent basculer entre divers types d’applications internes.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="4b0d4-168">Celles-ci peuvent inclure Microsoft Dynamics CRM, Power BI, etc.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="4b0d4-169">Les clients pourraient souhaiter appliquer une analyse de télémétrie en relation avec la manière dont les utilisateurs basculent entre les différentes applications, la tendance d’utilisation, etc.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-169">Customers might want to apply a telemetry analysis of how users switch between different applications, what the usage trends are, and so on.</span></span> <span data-ttu-id="4b0d4-170">L’objectif de l’entreprise est d’optimiser l’utilisation des applications.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-170">The goal for the business is to optimize application usage.</span></span> <span data-ttu-id="4b0d4-171">Ils pourraient également avoir envie de combiner différentes applications ou routines de connexion spécifiques.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-171">They also might want to combine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="4b0d4-172">Pour atteindre cet objectif, nous devons déterminer des ID de session et un décalage avec la dernière session ayant eu lieu.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-172">To achieve this goal, we have to determine session IDs and lag time between the last session that occurred.</span></span>

<span data-ttu-id="4b0d4-173">Nous devons trouver une connexion précédente, puis affecter cette connexion à toutes les sessions générées pour la même application.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-173">We need to find a previous sign-in and then assign this sign-in to all sessions that are being generated to the same application.</span></span> <span data-ttu-id="4b0d4-174">La première difficulté est que le script U-SQL de base ne nous permet pas d’appliquer des calculs à des colonnes déjà calculées avec la fonction LAG.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-174">The first challenge is that U-SQL base script doesn't allow us to apply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="4b0d4-175">La deuxième difficulté est que nous devons garder la session spécifique pour toutes les sessions au cours de la même période.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-175">The second challenge is that we have to keep the specific session for all sessions within the same time period.</span></span>

<span data-ttu-id="4b0d4-176">Pour résoudre ce problème, nous utilisons une variable globale à l’intérieur de la section code-behind : `static public string globalSession;`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-176">To solve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="4b0d4-177">Cette variable globale est appliquée à l’ensemble de lignes lors de l’exécution de notre script.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-177">This global variable is applied to the entire rowset during our script execution.</span></span>

<span data-ttu-id="4b0d4-178">Voici la section code-behind de notre programme U-SQL :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-178">Here is the code-behind section of our U-SQL program:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQLApplication21
{
    public class UserSession
    {
        static public string globalSession;
        static public string StampUserSession(string eventTime, string PreviousRow, string Session)
        {

            if (!string.IsNullOrEmpty(PreviousRow))
            {
                double timeGap = Convert.ToDateTime(eventTime).Subtract(Convert.ToDateTime(PreviousRow)).TotalMinutes;
                if (timeGap <= 60) {return Session;}
                else {return Guid.NewGuid().ToString();}
            }
            else {return Guid.NewGuid().ToString();}

        }

        static public string getStampUserSession(string Session)
        {
            if (Session != globalSession && !string.IsNullOrEmpty(Session)) { globalSession = Session; }
            return globalSession;
        }

    }
}
```

<span data-ttu-id="4b0d4-179">Cet exemple montre la variable globale `static public string globalSession;` utilisée dans la fonction `getStampUserSession` et réinitialisée à chaque modification du paramètre Session.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-179">This example shows the global variable `static public string globalSession;` used inside the `getStampUserSession` function and getting reinitialized each time the Session parameter is changed.</span></span>

<span data-ttu-id="4b0d4-180">Le script de base U-SQL est le suivant :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-180">The U-SQL base script is as follows:</span></span>

```
DECLARE @in string = @"\UserSession\test1.tsv";
DECLARE @out1 string = @"\UserSession\Out1.csv";
DECLARE @out2 string = @"\UserSession\Out2.csv";
DECLARE @out3 string = @"\UserSession\Out3.csv";

@records =
    EXTRACT DataId string,
            EventDateTime string,           
            UserName string,
            UserSessionTimestamp string

    FROM @in
    USING Extractors.Tsv();

@rs1 =
    SELECT 
        EventDateTime,
        UserName,
    LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,          
        string.IsNullOrEmpty(LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,           
        USQLApplication21.UserSession.StampUserSession
           (
            EventDateTime,
            LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC),
            LAG(UserSessionTimestamp, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)
           ) AS UserSessionTimestamp
    FROM @records;

@rs2 =
    SELECT 
        EventDateTime,
        UserName,
        LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,
        string.IsNullOrEmpty( LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,
        USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp) AS UserSessionTimestamp
    FROM @rs1
    WHERE UserName != "UserName";

OUTPUT @rs2
    TO @out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

<span data-ttu-id="4b0d4-181">La fonction `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` est appelée ici pendant le deuxième calcul d’ensemble de lignes de mémoire.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during the second memory rowset calculation.</span></span> <span data-ttu-id="4b0d4-182">Elle transmet la colonne `UserSessionTimestamp` et retourne la valeur jusqu’à ce que `UserSessionTimestamp` soit modifié.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-182">It passes the `UserSessionTimestamp` column and returns the value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="4b0d4-183">Le fichier de sortie se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-183">The output file is as follows:</span></span>

```
"2016-02-19T07:32:36.8420000-08:00","User1",,True,"72a0660e-22df-428e-b672-e0977007177f"
"2016-02-17T11:52:43.6350000-08:00","User2",,True,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-17T11:59:08.8320000-08:00","User2","2016-02-17T11:52:43.6350000-08:00",False,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-11T07:04:17.2630000-08:00","User3",,True,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-11T07:10:33.9720000-08:00","User3","2016-02-11T07:04:17.2630000-08:00",False,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-15T21:27:41.8210000-08:00","User3","2016-02-11T07:10:33.9720000-08:00",False,"4d2bc48d-bdf3-4591-a9c1-7b15ceb8e074"
"2016-02-16T05:48:49.6360000-08:00","User3","2016-02-15T21:27:41.8210000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-16T06:22:43.6390000-08:00","User3","2016-02-16T05:48:49.6360000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-17T16:29:53.2280000-08:00","User3","2016-02-16T06:22:43.6390000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T16:39:07.2430000-08:00","User3","2016-02-17T16:29:53.2280000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T17:20:39.3220000-08:00","User3","2016-02-17T16:39:07.2430000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-19T05:23:54.5710000-08:00","User3","2016-02-17T17:20:39.3220000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T05:48:37.7510000-08:00","User3","2016-02-19T05:23:54.5710000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T06:40:27.4830000-08:00","User3","2016-02-19T05:48:37.7510000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T07:27:37.7550000-08:00","User3","2016-02-19T06:40:27.4830000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T19:35:40.9450000-08:00","User3","2016-02-19T07:27:37.7550000-08:00",False,"3f385f0b-3e68-4456-ac74-ff6cef093674"
"2016-02-20T00:07:37.8250000-08:00","User3","2016-02-19T19:35:40.9450000-08:00",False,"685f76d5-ca48-4c58-b77d-bd3a9ddb33da"
"2016-02-11T09:01:33.9720000-08:00","User4",,True,"9f0cf696-c8ba-449a-8d5f-1ca6ed8f2ee8"
"2016-02-17T06:30:38.6210000-08:00","User4","2016-02-11T09:01:33.9720000-08:00",False,"8b11fd2a-01bf-4a5e-a9af-3c92c4e4382a"
"2016-02-17T22:15:26.4020000-08:00","User4","2016-02-17T06:30:38.6210000-08:00",False,"4e1cb707-3b5f-49c1-90c7-9b33b86ca1f4"
"2016-02-18T14:37:27.6560000-08:00","User4","2016-02-17T22:15:26.4020000-08:00",False,"f4e44400-e837-40ed-8dfd-2ea264d4e338"
"2016-02-19T01:20:31.4800000-08:00","User4","2016-02-18T14:37:27.6560000-08:00",False,"2136f4cf-7c7d-43c1-8ae2-08f4ad6a6e08"
```

<span data-ttu-id="4b0d4-184">Cet exemple illustre un scénario d’utilisation plus complexe dans lequel nous utilisons une variable globale à l’intérieur de la section code-behind, qui est appliquée à l’ensemble de lignes de mémoire.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied to the entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="4b0d4-185">Utiliser des types définis par l’utilisateur (UDT)</span><span class="sxs-lookup"><span data-stu-id="4b0d4-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="4b0d4-186">Les types définis par l’utilisateur (ou UDT) sont une autre fonctionnalité de programmabilité de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="4b0d4-187">Un type défini par l’utilisateur U-SQL agit comme un type défini par l’utilisateur C# standard.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="4b0d4-188">C# est un langage fortement typé qui permet d’utiliser des types définis par l’utilisateur intégrés et personnalisés.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-188">C# is a strongly typed language that allows the use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="4b0d4-189">U-SQL ne peut pas implicitement sérialiser ou désérialiser des types définis par l’utilisateur arbitraires lorsque le type défini par l’utilisateur est transmis entre les sommets des jeux de lignes.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when the UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="4b0d4-190">Cela implique que l’utilisateur doit fournir un formateur explicite à l’aide de l’interface IFormatter.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-190">This means that the user has to provide an explicit formatter by using the IFormatter interface.</span></span> <span data-ttu-id="4b0d4-191">U-SQL connaît ainsi les méthodes de sérialisation et désérialisation pour le type défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-191">This provides U-SQL with the serialize and de-serialize methods for the UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="4b0d4-192">Les extracteurs et générateurs de sortie intégrés à U-SQL ne peuvent pas actuellement sérialiser ou désérialiser les données du type défini par l’utilisateur vers ou à partir de fichiers, même avec le jeu IFormatter.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data to or from files even with the IFormatter set.</span></span> <span data-ttu-id="4b0d4-193">Par conséquent, lors de l’écriture de données du type défini par l’utilisateur dans un fichier avec l’instruction OUTPUT, ou lors de sa lecture à l’aide d’un extracteur, vous devez les transmettre sous la forme d’une chaîne ou d’un tableau d’octets.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-193">So when you're writing UDT data to a file with the OUTPUT statement, or reading it with an extractor, you have to pass it as a string or byte array.</span></span> <span data-ttu-id="4b0d4-194">Puis appelez explicitement le code de sérialisation et de désérialisation (c’est-à-dire, la méthode ToString() du type défini par l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="4b0d4-194">Then you call the serialization and deserialization code (that is, the UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="4b0d4-195">Les extracteurs et les générateurs de sortie définis par l’utilisateur, quant à eux, peuvent lire et écrire les types définis par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-195">User-defined extractors and outputters, on the other hand, can read and write UDTs.</span></span>

<span data-ttu-id="4b0d4-196">Si nous essayons d’utiliser un type défini par l’utilisateur dans un EXTRACTEUR ou un GÉNÉRATEUR DE SORTIE (à partir de l’instruction SELECT précédente), comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-196">If we try to use UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="4b0d4-197">Nous recevons l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-197">We receive the following error:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used to output column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how to serialize this type, or call a serialization method on the type in
the preceding SELECT.   C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

<span data-ttu-id="4b0d4-198">Pour utiliser un type défini par l’utilisateur dans un générateur de sortie, nous devons soit le sérialiser en une chaîne avec la méthode ToString(), soit créer un générateur de sortie personnalisé.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-198">To work with UDT in outputter, we either have to serialize it to string with the ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="4b0d4-199">Il n’est actuellement pas possible d’utiliser des types définis par l’utilisateur dans une instruction GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="4b0d4-200">Si un type défini par l’utilisateur est utilisé dans une instruction GROUP BY, l’erreur suivante est levée :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-200">If UDT is used in GROUP BY, the following error is thrown:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want to use with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

<span data-ttu-id="4b0d4-201">Pour définir un type défini par l’utilisateur, nous devons effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-201">To define a UDT, we have to:</span></span>

* <span data-ttu-id="4b0d4-202">Ajoutez les espaces de noms suivants :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-202">Add the following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="4b0d4-203">Ajouter `Microsoft.Analytics.Interfaces`, qui est requis pour les interfaces du type défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-203">Add `Microsoft.Analytics.Interfaces`, which is required for the UDT interfaces.</span></span> <span data-ttu-id="4b0d4-204">En outre, `System.IO` peut être nécessaire pour définir l’interface IFormatter.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-204">In addition, `System.IO` might be needed to define the IFormatter interface.</span></span>

* <span data-ttu-id="4b0d4-205">Définir un type défini par l’utilisateur avec l’attribut SqlUserDefinedType.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="4b0d4-206">**SqlUserDefinedType** est utilisé pour marquer une définition de type dans un assembly en tant que type défini par l’utilisateur (UDT) dans U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-206">**SqlUserDefinedType** is used to mark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="4b0d4-207">Les propriétés de l’attribut reflètent les caractéristiques physiques du type défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-207">The properties on the attribute reflect the physical characteristics of the UDT.</span></span> <span data-ttu-id="4b0d4-208">Cette classe ne peut pas être héritée.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-208">This class cannot be inherited.</span></span>

<span data-ttu-id="4b0d4-209">SqlUserDefinedType est un attribut obligatoire pour la définition du type défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="4b0d4-210">Le constructeur de la classe :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-210">The constructor of the class:</span></span>  

* <span data-ttu-id="4b0d4-211">SqlUserDefinedTypeAttribute (formateur de type)</span><span class="sxs-lookup"><span data-stu-id="4b0d4-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="4b0d4-212">Formateur de type : paramètre requis pour définir un formateur de type défini par l’utilisateur. Plus précisément, le type de l’interface `IFormatter` doit être transmis ici.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-212">Type formatter: Required parameter to define an UDT formatter--specifically, the type of the `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="4b0d4-213">Un type défini par l’utilisateur standard nécessite également une définition de l’interface IFormatter, comme illustré dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-213">Typical UDT also requires definition of the IFormatter interface, as shown in the following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="4b0d4-214">L’interface `IFormatter` sérialise et désérialise un graphique d’objets avec le type de racine \<typeparamref name="T">.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-214">The `IFormatter` interface serializes and de-serializes an object graph with the root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="4b0d4-215">\<typeparam name="T">Type de racine pour le graphique d’objet à sérialiser et désérialiser.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-215">\<typeparam name="T">The root type for the object graph to serialize and de-serialize.</span></span>

* <span data-ttu-id="4b0d4-216">**Désérialiser** : désérialise les données sur le flux fourni et reconstitue le graphique d’objet.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-216">**Deserialize**: De-serializes the data on the provided stream and reconstitutes the graph of objects.</span></span>

* <span data-ttu-id="4b0d4-217">**Sérialiser** : sérialise un objet ou graphique d’objet avec la racine donnée dans le flux fourni.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-217">**Serialize**: Serializes an object, or graph of objects, with the given root to the provided stream.</span></span>

<span data-ttu-id="4b0d4-218">Instance `MyType` : instance du type.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-218">`MyType` instance: Instance of the type.</span></span>  
<span data-ttu-id="4b0d4-219">Enregistreur `IColumnWriter` / lecteur `IColumnReader` : flux de la colonne sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-219">`IColumnWriter` writer / `IColumnReader` reader: The underlying column stream.</span></span>  
<span data-ttu-id="4b0d4-220">Contexte `ISerializationContext` : énumération définissant un jeu d’indicateurs qui spécifie le contexte source ou cible pour le flux pendant la sérialisation.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-220">`ISerializationContext` context: Enum that defines a set of flags that specifies the source or destination context for the stream during serialization.</span></span>

* <span data-ttu-id="4b0d4-221">**Intermediate** : spécifie que le contexte source ou cible n’est pas un magasin persistant.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-221">**Intermediate**: Specifies that the source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="4b0d4-222">**Persistence** : spécifie que le contexte source ou cible est un magasin persistant.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-222">**Persistence**: Specifies that the source or destination context is a persisted store.</span></span>

<span data-ttu-id="4b0d4-223">En tant que type C# standard, une définition de type défini par l’utilisateur U-SQL peut inclure des remplacements pour des opérateurs tels que +/==/!=.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="4b0d4-224">Elle peut également inclure des méthodes statiques.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-224">It can also include static methods.</span></span> <span data-ttu-id="4b0d4-225">Par exemple, si nous prévoyons d’utiliser ce type défini par l’utilisateur en tant que paramètre pour une fonction d’agrégation U-SQL MIN, nous devons définir un remplacement de l’opérateur <.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-225">For example, if we are going to use this UDT as a parameter to a U-SQL MIN aggregate function, we have to define < operator override.</span></span>

<span data-ttu-id="4b0d4-226">Précédemment dans ce guide, nous avons présenté un exemple d’identification de période fiscale à partir de la date spécifiée au format Qn:Pn (Q1:P10).</span><span class="sxs-lookup"><span data-stu-id="4b0d4-226">Earlier in this guide, we demonstrated an example for fiscal period identification from the specific date in the format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="4b0d4-227">L’exemple suivant montre comment définir un type personnalisé pour les valeurs de période fiscale.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-227">The following example shows how to define a custom type for fiscal period values.</span></span>

<span data-ttu-id="4b0d4-228">Vous trouverez ci-dessous un exemple de section code-behind avec un type défini par l’utilisateur et une interface personnalisée IFormatter :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

```
[SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
public struct FiscalPeriod
{
    public int Quarter { get; private set; }

    public int Month { get; private set; }

    public FiscalPeriod(int quarter, int month):this()
    {
    this.Quarter = quarter;
    this.Month = month;
    }

    public override bool Equals(object obj)
    {
    if (ReferenceEquals(null, obj))
    {
        return false;
    }

    return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
    }

    public bool Equals(FiscalPeriod other)
    {
return this.Quarter.Equals(other.Quarter) && this.Month.Equals(other.Month);
    }

    public bool GreaterThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
    }

    public bool LessThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
    }

    public override int GetHashCode()
    {
    unchecked
    {
        return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
    }
    }

    public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
    {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
    }

    public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.Equals(c2);
    }

    public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
    {
    return !c1.Equals(c2);
    }
    public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.GreaterThan(c2);
    }
    public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.LessThan(c2);
    }
    public override string ToString()
    {
    return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
    }

}

public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
{
    public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
    {
    using (var binaryWriter = new BinaryWriter(writer.BaseStream))
    {
        binaryWriter.Write(instance.Quarter);
        binaryWriter.Write(instance.Month);
        binaryWriter.Flush();
    }
    }

    public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
    {
    using (var binaryReader = new BinaryReader(reader.BaseStream))
    {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
        return result;
    }
    }
}
```

<span data-ttu-id="4b0d4-229">Le type défini inclut deux numéros, respectivement pour le trimestre et le mois.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-229">The defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="4b0d4-230">Les opérateurs ==/!=/>/< et la méthode statique ToString() sont définis ici.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="4b0d4-231">Comme mentionné précédemment, le type défini par l’utilisateur peut être utilisé dans des expressions SELECT, mais pas dans un GÉNÉRATEUR DE SORTIE/EXTRACTEUR sans sérialisation personnalisée.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="4b0d4-232">Il doit être sérialisé en tant que chaîne avec ToString(), ou utilisé avec un GÉNÉRATEUR DE SORTIE/EXTRACTEUR personnalisé.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-232">It either has to be serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="4b0d4-233">Voyons à présent l’usage d’un type défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="4b0d4-234">Dans une section code-behind, nous avons modifié notre fonction GetFiscalPeriod comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-234">In a code-behind section, we changed our GetFiscalPeriod function to the following:</span></span>

```
public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
{
    int FiscalMonth = 0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter = 0;
    if (FiscalMonth >= 1 && FiscalMonth <= 3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return new FiscalPeriod(FiscalQuarter, FiscalMonth);
}
```

<span data-ttu-id="4b0d4-235">Comme vous pouvez le voir, elle retourne la valeur de notre type FiscalPeriod.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-235">As you can see, it returns the value of our FiscalPeriod type.</span></span>

<span data-ttu-id="4b0d4-236">Voici un exemple montrant comment l’utiliser dans un script U-SQL de base.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-236">Here we provide an example of how to use it further in U-SQL base script.</span></span> <span data-ttu-id="4b0d4-237">Cet exemple illustre différentes façons d’appeler un type défini par l’utilisateur à partir d’un script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

```
DECLARE @input_file string = @"c:\work\cosmos\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"c:\work\cosmos\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid string,
        dt DateTime,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT 
        guid AS start_id,
        dt,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Quarter AS fiscalquarter,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Month AS fiscalmonth,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt) + new USQL_Programmability.CustomFunctions.FiscalPeriod(1,7) AS fiscalperiod_adjusted,
        user,
        des
    FROM @rs0;

@rs2 =
    SELECT 
           start_id,
           dt,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           fiscalquarter,
           fiscalmonth,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS fiscalperiod,

       // This user-defined type was created in the prior SELECT.  Passing the UDT to this subsequent SELECT would have failed if the UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="4b0d4-238">Voici un exemple d’une section code-behind complète :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-238">Here's an example of a full code-behind section:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        static public DateTime? ToDateTime(string dt)
        {
            DateTime dtValue;

            if (!DateTime.TryParse(dt, out dtValue))
                return Convert.ToDateTime(dt);
            else
                return null;
        }

        public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
        {
            int FiscalMonth = 0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter = 0;
            if (FiscalMonth >= 1 && FiscalMonth <= 3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return new FiscalPeriod(FiscalQuarter, FiscalMonth);
        }



        [SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
        public struct FiscalPeriod
        {
            public int Quarter { get; private set; }

            public int Month { get; private set; }

            public FiscalPeriod(int quarter, int month):this()
            {
                this.Quarter = quarter;
                this.Month = month;
            }

            public override bool Equals(object obj)
            {
                if (ReferenceEquals(null, obj))
                {
                    return false;
                }

                return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
            }

            public bool Equals(FiscalPeriod other)
            {
return this.Quarter.Equals(other.Quarter) &&    this.Month.Equals(other.Month);
            }

            public bool GreaterThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
            }

            public bool LessThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
            }

            public override int GetHashCode()
            {
                unchecked
                {
                    return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
                }
            }

            public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
            {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
            }

            public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.Equals(c2);
            }

            public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
            {
                return !c1.Equals(c2);
            }
            public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.GreaterThan(c2);
            }
            public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.LessThan(c2);
            }
            public override string ToString()
            {
                return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
            }

        }

        public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
        {
public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
            {
                using (var binaryWriter = new BinaryWriter(writer.BaseStream))
                {
                    binaryWriter.Write(instance.Quarter);
                    binaryWriter.Write(instance.Month);
                    binaryWriter.Flush();
                }
            }

public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
            {
                using (var binaryReader = new BinaryReader(reader.BaseStream))
                {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
                    return result;
                }
            }
        }
    }
}
```

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="4b0d4-239">Utiliser des agrégats définis par l’utilisateur : UDAGG</span><span class="sxs-lookup"><span data-stu-id="4b0d4-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="4b0d4-240">Les agrégats définis par l’utilisateur sont toutes les fonctions d’agrégation qui ne sont pas fournies prêtes à l’emploi avec U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="4b0d4-241">L’exemple peut être un agrégat effectuant des calculs mathématiques personnalisés, des concaténations de chaînes, des manipulations de chaînes, etc.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-241">The example can be an aggregate to perform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="4b0d4-242">La définition de classe de base d’agrégat défini par l’utilisateur est la suivante :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-242">The user-defined aggregate base class definition is as follows:</span></span>

```c#
    [SqlUserDefinedAggregate]
    public abstract class IAggregate<T1, T2, TResult> : IAggregate
    {
        protected IAggregate();

        public abstract void Accumulate(T1 t1, T2 t2);
        public abstract void Init();
        public abstract TResult Terminate();
    }
```

<span data-ttu-id="4b0d4-243">**SqlUserDefinedAggregate** indique que le type doit être inscrit en tant qu’agrégat défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-243">**SqlUserDefinedAggregate** indicates that the type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="4b0d4-244">Cette classe ne peut pas être héritée.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-244">This class cannot be inherited.</span></span>

<span data-ttu-id="4b0d4-245">L’attribut SqlUserDefinedType est **facultatif** pour la définition d’UDAGG.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="4b0d4-246">La classe de base permet de transmettre trois paramètres abstraits : deux paramètres d’entrée et un de résultat.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-246">The base class allows you to pass three abstract parameters: two as input parameters and one as the result.</span></span> <span data-ttu-id="4b0d4-247">Les types de données sont variables et doivent être définis lors de l’héritage de classe.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-247">The data types are variable and should be defined during class inheritance.</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    { … }

    public override void Accumulate(string guid, string user)
    { … }

    public override string Terminate()
    { … }
}
```

* <span data-ttu-id="4b0d4-248">**Init** appelle une seule fois chaque groupe pendant le calcul.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="4b0d4-249">Elle fournit une routine d’initialisation pour chaque groupe d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="4b0d4-250">**Accumulate** est exécutée une fois pour chaque valeur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="4b0d4-251">Elle fournit la fonctionnalité principale pour l’algorithme d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-251">It provides the main functionality for the aggregation algorithm.</span></span> <span data-ttu-id="4b0d4-252">Elle peut être utilisée pour agréger des valeurs de différents types de données qui sont définis lors de l’héritage de classe.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-252">It can be used to aggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="4b0d4-253">Elle peut accepter deux paramètres de types de données variables.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="4b0d4-254">**Terminate** est exécutée une fois par groupe d’agrégation à la fin du traitement pour générer le résultat de chaque groupe.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-254">**Terminate** is executed once per aggregation group at the end of processing to output the result for each group.</span></span>

<span data-ttu-id="4b0d4-255">Pour déclarer des types de données d’entrée et de sortie corrects, utilisez la définition de classe suivante :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-255">To declare correct input and output data types, use the class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="4b0d4-256">T1 : premier paramètre pour la routine accumulate</span><span class="sxs-lookup"><span data-stu-id="4b0d4-256">T1: First parameter to accumulate</span></span>
* <span data-ttu-id="4b0d4-257">T2 : premier paramètre pour la routine accumulate</span><span class="sxs-lookup"><span data-stu-id="4b0d4-257">T2: First parameter to accumulate</span></span>
* <span data-ttu-id="4b0d4-258">TResult : type de retour de la routine terminate</span><span class="sxs-lookup"><span data-stu-id="4b0d4-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="4b0d4-259">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="4b0d4-260">ou</span><span class="sxs-lookup"><span data-stu-id="4b0d4-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="4b0d4-261">Utiliser UDAGG dans U-SQL</span><span class="sxs-lookup"><span data-stu-id="4b0d4-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="4b0d4-262">Pour utiliser UDAGG, commencez par le définir dans code-behind ou par le référencer à partir de la DLL de programmabilité existante, comme décrit précédemment.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-262">To use UDAGG, first define it in code-behind or reference it from the existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="4b0d4-263">Utilisez ensuite la syntaxe suivante :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-263">Then use the following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="4b0d4-264">Voici l’exemple d’UDAGG :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-264">Here is an example of UDAGG:</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    {
        guid_agg = "";
    }

    public override void Accumulate(string guid, string user)
    {
        if (user.ToUpper()== "USER1")
        {
        guid_agg += "{" + guid + "}";
        }
    }

    public override string Terminate()
    {
        return guid_agg;
    }

}
```

<span data-ttu-id="4b0d4-265">Et le script U-SQL de base :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-265">And base U-SQL script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @" \usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    SELECT
        user,
        AGG<USQL_Programmability.GuidAggregate>(guid,user) AS guid_list
    FROM @rs0
    GROUP BY user;

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="4b0d4-266">Dans ce scénario d’utilisation, nous concaténons des GUID de classe pour les utilisateurs spécifiés.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-266">In this use-case scenario, we concatenate class GUIDs for the specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="4b0d4-267">Utiliser des objets définis par l’utilisateur : UDO</span><span class="sxs-lookup"><span data-stu-id="4b0d4-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="4b0d4-268">U-SQL vous permet de définir des objets de programmabilité personnalisés, appelés objets définis par l’utilisateur (ou UDO).</span><span class="sxs-lookup"><span data-stu-id="4b0d4-268">U-SQL enables you to define custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="4b0d4-269">Voici une liste d’UDO dans U-SQL :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-269">The following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="4b0d4-270">Extracteurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4b0d4-270">User-defined extractors</span></span>
    * <span data-ttu-id="4b0d4-271">Extraient ligne par ligne</span><span class="sxs-lookup"><span data-stu-id="4b0d4-271">Extract row by row</span></span>
    * <span data-ttu-id="4b0d4-272">Utilisés pour implémenter une extraction de données à partir de fichiers structurés personnalisés</span><span class="sxs-lookup"><span data-stu-id="4b0d4-272">Used to implement data extraction from custom structured files</span></span>

* <span data-ttu-id="4b0d4-273">Générateurs de sortie définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4b0d4-273">User-defined outputters</span></span>
    * <span data-ttu-id="4b0d4-274">Sortent ligne par ligne</span><span class="sxs-lookup"><span data-stu-id="4b0d4-274">Output row by row</span></span>
    * <span data-ttu-id="4b0d4-275">Utilisés pour sortir des types de données personnalisées ou des formats de fichiers personnalisés</span><span class="sxs-lookup"><span data-stu-id="4b0d4-275">Used to output custom data types or custom file formats</span></span>

* <span data-ttu-id="4b0d4-276">Processeurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4b0d4-276">User-defined processors</span></span>
    * <span data-ttu-id="4b0d4-277">Prennent une ligne et produisent une ligne</span><span class="sxs-lookup"><span data-stu-id="4b0d4-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="4b0d4-278">Utilisés pour réduire le nombre de colonnes ou produire de nouvelles colonnes avec des valeurs dérivées d’un ensemble de colonnes existant</span><span class="sxs-lookup"><span data-stu-id="4b0d4-278">Used to reduce the number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="4b0d4-279">Applicateurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4b0d4-279">User-defined appliers</span></span>
    * <span data-ttu-id="4b0d4-280">Prennent une ligne et produisent de 0 à n lignes</span><span class="sxs-lookup"><span data-stu-id="4b0d4-280">Take one row and produce 0 to n rows</span></span>
    * <span data-ttu-id="4b0d4-281">Utilisés avec OUTER/CROSS APPLY</span><span class="sxs-lookup"><span data-stu-id="4b0d4-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="4b0d4-282">Combinateurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4b0d4-282">User-defined combiners</span></span>
    * <span data-ttu-id="4b0d4-283">Combinent des ensembles de lignes et des jointures définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4b0d4-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="4b0d4-284">Réducteurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4b0d4-284">User-defined reducers</span></span>
    * <span data-ttu-id="4b0d4-285">Prennent n lignes et produisent une ligne</span><span class="sxs-lookup"><span data-stu-id="4b0d4-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="4b0d4-286">Utilisés pour réduire le nombre de lignes</span><span class="sxs-lookup"><span data-stu-id="4b0d4-286">Used to reduce the number of rows</span></span>

<span data-ttu-id="4b0d4-287">UDO est généralement appelé explicitement dans un script U-SQL dans le cadre des instructions U-SQL suivantes :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-287">UDO is typically called explicitly in U-SQL script as part of the following U-SQL statements:</span></span>

* <span data-ttu-id="4b0d4-288">EXTRACT</span><span class="sxs-lookup"><span data-stu-id="4b0d4-288">EXTRACT</span></span>
* <span data-ttu-id="4b0d4-289">OUTPUT</span><span class="sxs-lookup"><span data-stu-id="4b0d4-289">OUTPUT</span></span>
* <span data-ttu-id="4b0d4-290">PROCESS</span><span class="sxs-lookup"><span data-stu-id="4b0d4-290">PROCESS</span></span>
* <span data-ttu-id="4b0d4-291">COMBINE</span><span class="sxs-lookup"><span data-stu-id="4b0d4-291">COMBINE</span></span>
* <span data-ttu-id="4b0d4-292">REDUCE</span><span class="sxs-lookup"><span data-stu-id="4b0d4-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="4b0d4-293">La consommation des UDO est limitée à 0,5 Go de mémoire.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-293">UDO’s are limited to consume 0.5Gb memory.</span></span>  <span data-ttu-id="4b0d4-294">La limite de mémoire ne s’applique pas aux exécutions locales.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-294">This memory limitation does not apply to local executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="4b0d4-295">Utiliser des extracteurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4b0d4-295">Use user-defined extractors</span></span>
<span data-ttu-id="4b0d4-296">U-SQL vous permet d’importer des données externes en utilisant une instruction EXTRACT.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-296">U-SQL allows you to import external data by using an EXTRACT statement.</span></span> <span data-ttu-id="4b0d4-297">Une instruction EXTRACT peut utiliser des extracteurs UDO intégrés :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="4b0d4-298">*Extractors.Text()* : produit une extraction à partir de fichiers texte délimités de codages différents.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="4b0d4-299">*Extractors.Csv()* : produit une extraction à partir de fichiers de valeurs séparées par des virgules (CSV) de codages différents.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="4b0d4-300">*Extractors.Tsv()* : produit une extraction à partir de fichiers de valeurs séparées par des tabulations (TSV) de codages différents.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="4b0d4-301">Il peut être utile de développer un extracteur personnalisé.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-301">It can be useful to develop a custom extractor.</span></span> <span data-ttu-id="4b0d4-302">C’est le cas lors de l’importation de données si vous souhaitez effectuer l’une des tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-302">This can be helpful during data import if we want to do any of the following tasks:</span></span>

* <span data-ttu-id="4b0d4-303">Modifier des données d’entrée en fractionnant des colonnes et en modifiant des valeurs individuelles.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="4b0d4-304">Il est préférable de combiner des colonnes à l’aide de la fonctionnalité PROCESSOR.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-304">The PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="4b0d4-305">Analyser des données non structurées telles que des pages web et des messages électroniques, ou des données semi-structurées telles que des fichiers XML/JSON.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="4b0d4-306">Analyser des données dans un codage non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="4b0d4-307">Pour définir un extracteur défini par l’utilisateur (ou UDE), nous devons créer une interface `IExtractor`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-307">To define a user-defined extractor, or UDE, we need to create an `IExtractor` interface.</span></span> <span data-ttu-id="4b0d4-308">Tous les paramètres d’entrée de l’extracteur, tels que les séparateurs de colonnes/lignes et le codage, doivent être définis dans le constructeur de la classe.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-308">All input parameters to the extractor, such as column/row delimiters, and encoding, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="4b0d4-309">L’interface `IExtractor` doit également contenir une définition pour le remplacement de `IEnumerable<IRow>` comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-309">The `IExtractor`  interface should also contain a definition for the `IEnumerable<IRow>` override as follows:</span></span>

```
[SqlUserDefinedExtractor]
public class SampleExtractor : IExtractor
{
     public SampleExtractor(string row_delimiter, char col_delimiter)
     { … }

     public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
     { … }
}
```

<span data-ttu-id="4b0d4-310">L’attribut **SqlUserDefinedExtractor** indique que le type doit être inscrit en tant qu’extracteur défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-310">The **SqlUserDefinedExtractor** attribute indicates that the type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="4b0d4-311">Cette classe ne peut pas être héritée.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-311">This class cannot be inherited.</span></span>

<span data-ttu-id="4b0d4-312">SqlUserDefinedExtractor est un attribut facultatif pour la définition d’UDE.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="4b0d4-313">Il est utilisé pour définir la propriété AtomicFileProcessing pour l’objet UDE.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-313">It used to define AtomicFileProcessing property for the UDE object.</span></span>

* <span data-ttu-id="4b0d4-314">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="4b0d4-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="4b0d4-315">**true** = indique que cet extracteur requiert des fichiers d’entrée atomique (JSON, XML, ...)</span><span class="sxs-lookup"><span data-stu-id="4b0d4-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="4b0d4-316">**false** = indique que cet extracteur peut traiter des fichiers fractionnés/distribués (CSV, SEQ, ...)</span><span class="sxs-lookup"><span data-stu-id="4b0d4-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="4b0d4-317">Les principaux objets de programmabilité d’UDE sont l’**entrée** et la **sortie**.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-317">The main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="4b0d4-318">L’objet d’entrée permet d’énumérer les données d’entrée en tant que `IUnstructuredReader`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-318">The input object is used to enumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="4b0d4-319">L’objet de sortie permet de définir les données de sortie en tant que résultat de l’activité de l’extracteur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-319">The output object is used to set output data as a result of the extractor activity.</span></span>

<span data-ttu-id="4b0d4-320">Les données d’entrée sont accessibles via `System.IO.Stream` et `System.IO.StreamReader`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-320">The input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="4b0d4-321">Pour l’énumération des colonnes d’entrée, nous fractionnons d’abord le flux d’entrée en utilisant un séparateur de lignes.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-321">For input columns enumeration, we first split the input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="4b0d4-322">Ensuite, nous fractionnons la ligne d’entrée en parties de colonne.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="4b0d4-323">Pour définir les données de sortie, nous utilisons la méthode `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-323">To set output data, we use the `output.Set` method.</span></span>

<span data-ttu-id="4b0d4-324">Il est important de comprendre que l’extracteur personnalisé ne génère que des colonnes et des valeurs qui sont définies avec la sortie.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-324">It's important to understand that the custom extractor only outputs columns and values that are defined with the output.</span></span> <span data-ttu-id="4b0d4-325">Définissez l’appel de méthode.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="4b0d4-326">La sortie réelle de l’extracteur est déclenchée par l’appel de `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-326">The actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="4b0d4-327">Voici l’exemple d’extracteur :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-327">Following is the extractor example:</span></span>

```
[SqlUserDefinedExtractor(AtomicFileProcessing = true)]
public class FullDescriptionExtractor : IExtractor
{
     private Encoding _encoding;
     private byte[] _row_delim;
     private char _col_delim;

    public FullDescriptionExtractor(Encoding encoding, string row_delim = "\r\n", char col_delim = '\t')
    {
         this._encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
         this._row_delim = this._encoding.GetBytes(row_delim);
         this._col_delim = col_delim;

    }

    public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
    {
         string line;
         //Read the input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split the input by the column delimiter
             string[] parts = line.Split(this._col_delim);
             int count = 0; // start with first column
             foreach (string part in parts)
             {
    if (count == 0)
             {  // for column “guid”, re-generated guid
                 Guid new_guid = Guid.NewGuid();
                 output.Set<Guid>(count, new_guid);
             }
             else if (count == 2)
             {
                 // for column “user”, convert to UPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep the rest of the columns as-is
                 output.Set<string>(count, part);
             }
             count += 1;
             }

         }
         yield return output.AsReadOnly();
         }
         yield break;
     }
}
```

<span data-ttu-id="4b0d4-328">Dans ce scénario d’utilisation, l’extracteur régénère le GUID pour la colonne « guid », et convertit les valeurs de la colonne « utilisateur » en majuscules.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-328">In this use-case scenario, the extractor regenerates the GUID for “guid” column and converts the values of “user” column to upper case.</span></span> <span data-ttu-id="4b0d4-329">Des extracteurs personnalisés peuvent produire des résultats plus complexes en analysant et manipulant des données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="4b0d4-330">Le script U-SQL de base utilisant un extracteur personnalisé est le suivant :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-330">Following is base U-SQL script that uses a custom extractor:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file
        USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a><span data-ttu-id="4b0d4-331">Utiliser des générateurs de sortie définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4b0d4-331">Use user-defined outputters</span></span>
<span data-ttu-id="4b0d4-332">Le générateur de sortie défini par l’utilisateur est un autre UDO U-SQL qui vous permet d’étendre les fonctionnalités U-SQL intégrées.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-332">User-defined outputter is another U-SQL UDO that allows you to extend built-in U-SQL functionality.</span></span> <span data-ttu-id="4b0d4-333">Comme pour l’extracteur, il existe plusieurs générateurs de sortie intégrés.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-333">Similar to the extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="4b0d4-334">*Outputters.Text()* : écrit des données dans des fichiers texte délimités de codages différents.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-334">*Outputters.Text()*: Writes data to delimited text files of different encodings.</span></span>
* <span data-ttu-id="4b0d4-335">*Outputters.Csv()* : écrit des données dans des fichiers de valeurs séparées par des virgules (CSV) de codages différents.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-335">*Outputters.Csv()*: Writes data to comma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="4b0d4-336">*Outputters.Tsv()* : écrit des données dans des fichiers de valeur séparées par des tabulations (TSV) de codages différents.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-336">*Outputters.Tsv()*: Writes data to tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="4b0d4-337">Un générateur de sortie personnalisé vous permet d’écrire des données dans un format défini personnalisé.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-337">Custom outputter allows you to write data in a custom defined format.</span></span> <span data-ttu-id="4b0d4-338">Cela peut être utile pour les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-338">This can be useful for the following tasks:</span></span>

* <span data-ttu-id="4b0d4-339">Écrire des données dans des fichiers semi-structurés ou non structurés.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-339">Writing data to semi-structured or unstructured files.</span></span>
* <span data-ttu-id="4b0d4-340">Écrire des données dans des codages non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="4b0d4-341">Modifier des données de sortie ou ajouter des attributs personnalisés.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="4b0d4-342">Pour définir un générateur de sortie défini par l’utilisateur, nous devons créer l’interface `IOutputter`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-342">To define user-defined outputter, we need to create the `IOutputter` interface.</span></span>

<span data-ttu-id="4b0d4-343">Voici l’implémentation de la classe `IOutputter` de base :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-343">Following is the base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="4b0d4-344">Tous les paramètres d’entrée du générateur de sortie, tels que les séparateurs de colonnes/lignes, le codage, et ainsi de suite, doivent être définis dans le constructeur de la classe.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-344">All input parameters to the outputter, such as column/row delimiters, encoding, and so on, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="4b0d4-345">L’interface `IOutputter` doit également contenir une définition pour le remplacement de `void Output`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-345">The `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="4b0d4-346">L’attribut `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` peut éventuellement être défini pour le traitement de fichier atomique.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-346">The attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="4b0d4-347">Pour plus d’informations, consultez les détails suivants :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-347">For more information, see the following details.</span></span>

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class MyOutputter : IOutputter
{

    public MyOutputter(myparam1, myparam2)
    {
      …
    }

    public override void Close()
    {
      …
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
      …
    }
}
```

* <span data-ttu-id="4b0d4-348">`Output` est appelé pour chaque ligne d’entrée.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-348">`Output` is called for each input row.</span></span> <span data-ttu-id="4b0d4-349">Il retourne l’ensemble de lignes `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-349">It returns the `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="4b0d4-350">La classe de constructeur est utilisée pour transmettre des paramètres au générateur de sortie défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-350">The Constructor class is used to pass parameters to the user-defined outputter.</span></span>
* <span data-ttu-id="4b0d4-351">`Close` est utilisé pour un remplacement éventuel pour libérer d’un état coûteux ou déterminer quand la dernière ligne a été écrite.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-351">`Close` is used to optionally override to release expensive state or determine when the last row was written.</span></span>

<span data-ttu-id="4b0d4-352">L’attribut **SqlUserDefinedOutputter** indique que le type doit être inscrit en tant que générateur de sortie défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-352">**SqlUserDefinedOutputter** attribute indicates that the type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="4b0d4-353">Cette classe ne peut pas être héritée.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-353">This class cannot be inherited.</span></span>

<span data-ttu-id="4b0d4-354">SqlUserDefinedOutputter est un attribut facultatif pour une définition d’un générateur de sortie défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="4b0d4-355">Il est utilisé pour définir la propriété de AtomicFileProcessing.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-355">It's used to define the AtomicFileProcessing property.</span></span>

* <span data-ttu-id="4b0d4-356">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="4b0d4-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="4b0d4-357">**true** = indique que ce générateur de sortie requiert des fichiers de sortie atomique (JSON, XML, ...)</span><span class="sxs-lookup"><span data-stu-id="4b0d4-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="4b0d4-358">**false** = indique que ce générateur de sortie peut traiter des fichiers fractionnés/distribués (CSV, SEQ, ...)</span><span class="sxs-lookup"><span data-stu-id="4b0d4-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="4b0d4-359">Les principaux objets de programmabilité sont **ligne** et **sortie**.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-359">The main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="4b0d4-360">L’objet **row** est utilisé pour énumérer les données de sortie en tant qu’interface `IRow`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-360">The **row** object is used to enumerate output data as `IRow` interface.</span></span> <span data-ttu-id="4b0d4-361">**Output** est utilisé pour définir les données de sortie dans le fichier cible.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-361">**Output** is used to set output data to the target file.</span></span>

<span data-ttu-id="4b0d4-362">Les données de sortie sont accessibles via l’interface `IRow`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-362">The output data is accessed through the `IRow` interface.</span></span> <span data-ttu-id="4b0d4-363">Les données de sortie sont transmises une ligne à la fois.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="4b0d4-364">Les valeurs individuelles sont énumérées en appelant la méthode Get de l’interface IRow :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-364">The individual values are enumerated by calling the Get method of the IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="4b0d4-365">Les noms des colonnes peuvent être déterminés en appelant `row.Schema` :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="4b0d4-366">Cette approche permet de créer un générateur de sortie flexible pour tout schéma de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-366">This approach enables you to build a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="4b0d4-367">Les données de sortie sont écrites dans le fichier en utilisant `System.IO.StreamWriter`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-367">The output data is written to file by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="4b0d4-368">Le paramètre stream est défini sur `output.BaseStrea` dans `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-368">The stream parameter is set to `output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="4b0d4-369">Notez qu’il est important de vider le tampon de données du fichier après chaque itération de la ligne.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-369">Note that it's important to flush the data buffer to the file after each row iteration.</span></span> <span data-ttu-id="4b0d4-370">En outre, l’objet `StreamWriter` doit être utilisé avec l’attribut Disposable activé (par défaut) et avec le mot clé **using** :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-370">In addition, the `StreamWriter` object must be used with the Disposable attribute enabled (default) and with the **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="4b0d4-371">Autrement, appelez explicitement la méthode Flush() après chaque itération.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="4b0d4-372">Cela est illustré dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-372">We show this in the following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="4b0d4-373">Définir des en-têtes et des pieds de page pour un générateur de sortie défini par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4b0d4-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="4b0d4-374">Pour définir un en-tête, utilisez un flux d’exécution d’itération unique.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-374">To set a header, use single iteration execution flow.</span></span>

```
public override void Output(IRow row, IUnstructuredWriter output)
{
 …
if (isHeaderRow)
{
    …                
}

 …
if (isHeaderRow)
{
    isHeaderRow = false;
}
 …
}
}
```

<span data-ttu-id="4b0d4-375">Le code du premier bloc `if (isHeaderRow)` n’est exécuté qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-375">The code in the first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="4b0d4-376">Pour le pied de page, utilisez la référence à l’instance de l’objet `System.IO.Stream` (`output.BaseStream`).</span><span class="sxs-lookup"><span data-stu-id="4b0d4-376">For the footer, use the reference to the instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="4b0d4-377">Écrivez le pied de page dans la méthode Close() de l’interface `IOutputter`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-377">Write the footer in the Close() method of the `IOutputter` interface.</span></span>  <span data-ttu-id="4b0d4-378">(Pour plus d’informations, consultez les exemples suivants.)</span><span class="sxs-lookup"><span data-stu-id="4b0d4-378">(For more information, see the following example.)</span></span>

<span data-ttu-id="4b0d4-379">Voici un exemple d’un générateur de sortie défini par l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-379">Following is an example of a user-defined outputter:</span></span>

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class HTMLOutputter : IOutputter
{
    // Local variables initialization
    private string row_delimiter;
    private char col_delimiter;
    private bool isHeaderRow;
    private Encoding encoding;
    private bool IsTableHeader = true;
    private Stream g_writer;

    // Parameters definition            
    public HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    this.isHeaderRow = isHeader;
    this.encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
    }

    // The Close method is used to write the footer to the file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference to IO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization to enumerate column names
    ISchema schema = row.Schema;

    // This is a data-independent header--HTML table definition
    if (IsTableHeader)
    {
        streamWriter.Write("<table border=1>");
        IsTableHeader = false;
    }

    // HTML table attributes
    string header_wrapper_on = "<th>";
    string header_wrapper_off = "</th>";
    string data_wrapper_on = "<td>";
    string data_wrapper_off = "</td>";

    // Header row output--runs only once
    if (isHeaderRow)
    {
        streamWriter.Write("<tr>");
        for (int i = 0; i < schema.Count(); i++)
        {
        var col = schema[i];
        streamWriter.Write(header_wrapper_on + col.Name + header_wrapper_off);
        }
        streamWriter.Write("</tr>");
    }

    // Data row output
    streamWriter.Write("<tr>");                
    for (int i = 0; i < schema.Count(); i++)
    {
        var col = schema[i];
        string val = "";
        try
        {
        // Data type enumeration--required to match the distinct list of types from OUTPUT statement
        switch (col.Type.Name.ToString().ToLower())
        {
            case "string": val = row.Get<string>(col.Name).ToString(); break;
            case "guid": val = row.Get<Guid>(col.Name).ToString(); break;
            default: break;
        }
        }
        // Handling NULL values--keeping them empty
        catch (System.NullReferenceException)
        {
        }
        streamWriter.Write(data_wrapper_on + val + data_wrapper_off);
    }
    streamWriter.Write("</tr>");

    if (isHeaderRow)
    {
        isHeaderRow = false;
    }
    // Reference to the instance of the IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define the factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

<span data-ttu-id="4b0d4-380">Et le script U-SQL de base :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-380">And U-SQL base script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.html";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
         FROM @input_file
         USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 
    TO @output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="4b0d4-381">Il s’agit d’un générateur de sortie HTML qui crée un fichier HTML avec les données de la table.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="4b0d4-382">Appeler un générateur de sortie à partir du script U-SQL de base</span><span class="sxs-lookup"><span data-stu-id="4b0d4-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="4b0d4-383">Pour appeler un générateur de sortie personnalisé à partir du script U-SQL de base, la nouvelle instance de l’objet générateur de sortie doit être créée.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-383">To call a custom outputter from the base U-SQL script, the new instance of the outputter object has to be created.</span></span>

```sql
OUTPUT @rs0 TO @output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="4b0d4-384">Pour éviter de créer une instance de l’objet dans le script de base, nous pouvons créer un wrapper de fonction, comme indiqué dans l’exemple précédent :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-384">To avoid creating an instance of the object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

```c#
        // Define the factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

<span data-ttu-id="4b0d4-385">Dans ce cas, l’appel d’origine ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-385">In this case, the original call looks like the following:</span></span>

```
OUTPUT @rs0 
TO @output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="4b0d4-386">Utiliser des processeurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4b0d4-386">Use user-defined processors</span></span>
<span data-ttu-id="4b0d4-387">Un processeur défini par l’utilisateur (ou UDP) est un type d’UDO U-SQL qui permet de traiter les lignes entrantes en appliquant des fonctionnalités de programmabilité.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you to process the incoming rows by applying programmability features.</span></span> <span data-ttu-id="4b0d4-388">Un UDP permet de combiner des colonnes, de modifier des valeurs et d’ajouter des colonnes si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-388">UDP enables you to combine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="4b0d4-389">En fait, il permet de traiter un ensemble de lignes pour produire des éléments de données requis.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-389">Basically, it helps to process a rowset to produce required data elements.</span></span>

<span data-ttu-id="4b0d4-390">Pour définir un UDP, nous devons créer une interface `IProcessor` avec l’attribut `SqlUserDefinedProcessor`, facultatif pour l’UDP.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-390">To define a UDP, we need to create an `IProcessor` interface with the `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="4b0d4-391">Cette interface doit contenir la définition pour le remplacement de l’ensemble de lignes de l’interface `IRow`, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-391">This interface should contain the definition for the `IRow` interface rowset override, as shown in the following example:</span></span>

```
[SqlUserDefinedProcessor]
public class MyProcessor: IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
        …
 }
}
```

<span data-ttu-id="4b0d4-392">**SqlUserDefinedProcessor** indique que le type doit être inscrit en tant que processeur défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-392">**SqlUserDefinedProcessor** indicates that the type should be registered as a user-defined processor.</span></span> <span data-ttu-id="4b0d4-393">Cette classe ne peut pas être héritée.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-393">This class cannot be inherited.</span></span>

<span data-ttu-id="4b0d4-394">L’attribut SqlUserDefinedProcessor est **facultatif** pour la définition d’UDP.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-394">The SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="4b0d4-395">Les principaux objets de programmabilité sont l’**entrée** et la **sortie**.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-395">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="4b0d4-396">L’objet d’entrée permet d’énumérer les colonnes d’entrée et la sortie, et de définir les données de sortie en tant que résultat de l’activité du processeur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-396">The input object is used to enumerate input columns and output, and to set output data as a result of the processor activity.</span></span>

<span data-ttu-id="4b0d4-397">Pour l’énumération des colonnes d’entrée, nous utilisons la méthode `input.Get`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-397">For input columns enumeration, we use the `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="4b0d4-398">Le paramètre pour la méthode `input.Get` est une colonne transmise dans une clause `PRODUCE` de l’instruction `PROCESS` du script U-SQL de base.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-398">The parameter for `input.Get` method is a column that's passed as part of the `PRODUCE` clause of the `PROCESS` statement of the U-SQL base script.</span></span> <span data-ttu-id="4b0d4-399">Nous devons utiliser le type de données ici.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-399">We need to use the correct data type here.</span></span>

<span data-ttu-id="4b0d4-400">Pour la sortie, utilisez la méthode `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-400">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="4b0d4-401">Il est important de noter qu’un producteur personnalisé ne génère que des colonnes et des valeurs qui sont définies avec l’appel de la méthode `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-401">It's important to note that custom producer only outputs columns and values that are defined with the `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="4b0d4-402">La sortie réelle du processeur est déclenchée par l’appel de `return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-402">The actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="4b0d4-403">Voici un exemple de processeur :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-403">Following is a processor example:</span></span>

```
[SqlUserDefinedProcessor]
public class FullDescriptionProcessor : IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
     string user = input.Get<string>("user");
     string des = input.Get<string>("des");
     string full_description = user.ToUpper() + "=>" + des;
     output.Set<string>("dt", input.Get<string>("dt"));
     output.Set<string>("full_description", full_description);
     output.Set<Guid>("new_guid", Guid.NewGuid());
     output.Set<Guid>("guid", input.Get<Guid>("guid"));
     return output.AsReadOnly();
 }
}
```

<span data-ttu-id="4b0d4-404">Dans ce scénario d’utilisation, le processeur génère une nouvelle colonne nommée « full_description » en combinant les colonnes existantes, dans ce cas, « user » en majuscules et « des ».</span><span class="sxs-lookup"><span data-stu-id="4b0d4-404">In this use-case scenario, the processor is generating a new column called “full_description” by combining the existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="4b0d4-405">Il génère également un GUID et retourne les valeurs de GUID d’origine et nouvelles.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-405">It also regenerates a GUID and returns the original and new GUID values.</span></span>

<span data-ttu-id="4b0d4-406">Comme vous pouvez le constater dans l’exemple précédent, vous pouvez appeler des méthodes C# durant l’appel de la méthode `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-406">As you can see from the previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="4b0d4-407">Vous trouverez ci-dessous un exemple de script U-SQL de base utilisant un processeur personnalisé :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
     PROCESS @rs0
     PRODUCE dt String,
             full_description String,
             guid Guid,
             new_guid Guid
     USING new USQL_Programmability.FullDescriptionProcessor();

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a><span data-ttu-id="4b0d4-408">Utiliser des applicateurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4b0d4-408">Use user-defined appliers</span></span>
<span data-ttu-id="4b0d4-409">Un applicateur U-SQL défini par l’utilisateur vous permet d’appeler une fonction C# personnalisée pour chaque ligne retournée par une expression de la table externe d’une requête.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-409">A U-SQL user-defined applier enables you to invoke a custom C# function for each row that's returned by the outer table expression of a query.</span></span> <span data-ttu-id="4b0d4-410">L’entrée appropriée est évaluée pour chaque ligne à partir de l’entrée de gauche et les lignes qui sont produites sont combinées pour la sortie finale.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-410">The right input is evaluated for each row from the left input, and the rows that are produced are combined for the final output.</span></span> <span data-ttu-id="4b0d4-411">La liste des colonnes produites par l’opérateur APPLY est la combinaison des jeux de colonnes dans les entrées de gauche et de droite.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-411">The list of columns that are produced by the APPLY operator are the combination of the set of columns in the left and the right input.</span></span>

<span data-ttu-id="4b0d4-412">Un applicateur défini par l’utilisateur est appelé dans l’expression U-SQL SELECT.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-412">User-defined applier is being invoked as part of the USQL SELECT expression.</span></span>

<span data-ttu-id="4b0d4-413">L’appel standard à l’applicateur défini par l’utilisateur se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-413">The typical call to the user-defined applier looks like the following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used to pass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="4b0d4-414">Pour plus d’informations sur l’utilisation d’applicateurs dans une expression SELECT, voir [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx) (Sélection d’U-SQL SELECT à partir de CROSS APPLY et de OUTER APPLY).</span><span class="sxs-lookup"><span data-stu-id="4b0d4-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="4b0d4-415">La définition de classe de base d’applicateur défini par l’utilisateur est la suivante :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-415">The user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="4b0d4-416">Pour définir un applicateur défini par l’utilisateur, nous devons créer l’interface `IApplier` avec l’attribut [`SqlUserDefinedApplier`] qui est facultatif pour une définition d’applicateur défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-416">To define a user-defined applier, we need to create the `IApplier` interface with the [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
    public ParserApplier()
    {
        …
    }

    public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
    {
        …
    }
}
```

* <span data-ttu-id="4b0d4-417">Apply est appelé pour chaque ligne de la table externe.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-417">Apply is called for each row of the outer table.</span></span> <span data-ttu-id="4b0d4-418">Il retourne l’ensemble de lignes de sortie `IUpdatableRow`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-418">It returns the `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="4b0d4-419">La classe de constructeur est utilisée pour transmettre des paramètres à l’applicateur défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-419">The Constructor class is used to pass parameters to the user-defined applier.</span></span>

<span data-ttu-id="4b0d4-420">**SqlUserDefinedApplier** indique que le type doit être inscrit en tant qu’un applicateur défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-420">**SqlUserDefinedApplier** indicates that the type should be registered as a user-defined applier.</span></span> <span data-ttu-id="4b0d4-421">Cette classe ne peut pas être héritée.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-421">This class cannot be inherited.</span></span>

<span data-ttu-id="4b0d4-422">**SqlUserDefinedApplier** est **facultatif** pour une définition d’applicateur défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="4b0d4-423">Les principaux objets de programmabilité sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-423">The main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="4b0d4-424">Les ensembles de lignes d’entrée sont transmis en tant qu’entrée `IRow`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="4b0d4-425">Les lignes de sortie sont générées en tant qu’interface de sortie `IUpdatableRow`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-425">The output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="4b0d4-426">Les noms des colonnes peuvent être déterminés en appelant la méthode de schéma `IRow`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-426">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="4b0d4-427">Pour obtenir les valeurs de données réelles du `IRow` entrant, nous utilisons la méthode Get() de l’interface `IRow`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-427">To get the actual data values from the incoming `IRow`, we use the Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="4b0d4-428">Ou bien, nous utilisons le nom de colonne de schéma :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-428">Or we use the schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="4b0d4-429">Les valeurs de sortie doivent être définies avec la sortie `IUpdatableRow` :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-429">The output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="4b0d4-430">Il est important de comprendre qu’un applicateur personnalisé génère uniquement des colonnes et des valeurs qui sont définies avec l’appel de la méthode `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-430">It is important to understand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="4b0d4-431">La sortie réelle est déclenchée par l’appel de `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-431">The actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="4b0d4-432">Les paramètres de l’applicateur défini par l’utilisateur peuvent être transmis au constructeur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-432">The user-defined applier parameters can be passed to the constructor.</span></span> <span data-ttu-id="4b0d4-433">Un applicateur peut retourner un nombre variable de colonnes, qui doit être défini durant l’appel de l’applicateur dans le script U-SQL de base.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-433">Applier can return a variable number of columns that need to be defined during the applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="4b0d4-434">Voici l’exemple d’applicateur défini par l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-434">Here is the user-defined applier example:</span></span>

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
private string parsingPart;

public ParserApplier(string parsingPart)
{
    if (parsingPart.ToUpper().Contains("ALL")
    || parsingPart.ToUpper().Contains("MAKE")
    || parsingPart.ToUpper().Contains("MODEL")
    || parsingPart.ToUpper().Contains("YEAR")
    || parsingPart.ToUpper().Contains("TYPE")
    || parsingPart.ToUpper().Contains("MILLAGE")
    )
    {
    this.parsingPart = parsingPart;
    }
    else
    {
    throw new ArgumentException("Incorrect parameter. Please use: 'ALL[MAKE|MODEL|TYPE|MILLAGE]'");
    }
}

public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
{

    string[] properties = input.Get<string>("properties").Split(',');

    //  only process with correct number of properties
    if (properties.Count() == 5)
    {

    string make = properties[0];
    string model = properties[1];
    string year = properties[2];
    string type = properties[3];
    int millage = -1;

    // Only return millage if it is number, otherwise, -1
    if (!int.TryParse(properties[4], out millage))
    {
        millage = -1;
    }

    if (parsingPart.ToUpper().Contains("MAKE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("make", make);
    if (parsingPart.ToUpper().Contains("MODEL") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("model", model);
    if (parsingPart.ToUpper().Contains("YEAR") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("year", year);
    if (parsingPart.ToUpper().Contains("TYPE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("type", type);
    if (parsingPart.ToUpper().Contains("MILLAGE") || parsingPart.ToUpper().Contains("ALL")) output.Set<int>("millage", millage);
    }
    yield return output.AsReadOnly();            
}
}
```

<span data-ttu-id="4b0d4-435">Le script U-SQL de base pour cet applicateur défini par l’utilisateur est le suivant :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-435">Following is the base U-SQL script for this user-defined applier:</span></span>

```
DECLARE @input_file string = @"c:\usql-programmability\car_fleet.tsv";
DECLARE @output_file string = @"c:\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        stocknumber int,
        vin String,
        properties String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT
        r.stocknumber,
        r.vin,
        properties.make,
        properties.model,
        properties.year,
        properties.type,
        properties.millage
    FROM @rs0 AS r
    CROSS APPLY
    new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="4b0d4-436">Dans ce scénario d’utilisation, l’applicateur défini par l’utilisateur agit comme un analyseur de valeurs délimitées par des virgules pour les propriétés d’une flotte de voitures.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for the car fleet properties.</span></span> <span data-ttu-id="4b0d4-437">Les lignes du fichier d’entrée ressemblent à ceci :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-437">The input file rows look like the following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="4b0d4-438">Il s’agit d’un fichier TSV standard de valeurs délimitées par des tabulations avec une colonne Propriétés contenant des propriétés de voitures telles que la marque et le modèle.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="4b0d4-439">Ces propriétés doivent être analysées dans les colonnes de table.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-439">Those properties must be parsed to the table columns.</span></span> <span data-ttu-id="4b0d4-440">L’applicateur fourni vous permet également de générer un nombre dynamique de propriétés dans l’ensemble de lignes de résultat, en fonction du paramètre transmis.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-440">The applier that's provided also enables you to generate a dynamic number of properties in the result rowset, based on the parameter that's passed.</span></span> <span data-ttu-id="4b0d4-441">Vous pouvez générer soit toutes les propriétés, soit un ensemble spécifique de propriétés.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="4b0d4-442">L’applicateur défini par l’utilisateur peut être appelé en tant que nouvelle instance de l’objet applicateur :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-442">The user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="4b0d4-443">Ou par l’appel d’une méthode de fabrique de wrapper :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-443">Or with the invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="4b0d4-444">Utiliser des combinateurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4b0d4-444">Use user-defined combiners</span></span>
<span data-ttu-id="4b0d4-445">Un combinateur défini par l’utilisateur (ou UDC) vous permet de combiner des lignes des ensembles de lignes gauche et droit, selon une logique personnalisée.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-445">User-defined combiner, or UDC, enables you to combine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="4b0d4-446">Un combinateur défini par l’utilisateur est utilisé avec l’expression COMBINE.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="4b0d4-447">Un combinateur est appelé avec l’expression COMBINE qui fournit les informations nécessaires sur les ensembles de lignes d’entrée, les colonnes de regroupement, le schéma de résultat attendu et des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-447">A combiner is being invoked with the COMBINE expression that provides the necessary information about both the input rowsets, the grouping columns, the expected result schema, and additional information.</span></span>

<span data-ttu-id="4b0d4-448">Pour appeler un combinateur dans un script U-SQL de base, nous utilisons la syntaxe suivante :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-448">To call a combiner in a base U-SQL script, we use the following syntax:</span></span>

```
Combine_Expression :=
    'COMBINE' Combine_Input
    'WITH' Combine_Input
    Join_On_Clause
    Produce_Clause
    [Readonly_Clause]
    [Required_Clause]
    USING_Clause.
```

<span data-ttu-id="4b0d4-449">Pour plus d’informations, voir [Expression COMBINE (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span><span class="sxs-lookup"><span data-stu-id="4b0d4-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="4b0d4-450">Pour définir un combinateur défini par l’utilisateur, nous devons créer une interface `ICombiner` avec l’attribut [`SqlUserDefinedCombiner`], qui est facultatif pour une définition de combinateur défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-450">To define a user-defined combiner, we need to create the `ICombiner` interface with the [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="4b0d4-451">Définition de classe `ICombiner` de base :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-451">Base `ICombiner` class definition:</span></span>

```
public abstract class ICombiner : IUserDefinedOperator
{
protected ICombiner();
public virtual IEnumerable<IRow> Combine(List<IRowset> inputs,
       IUpdatableRow output);
public abstract IEnumerable<IRow> Combine(IRowset left, IRowset right,
       IUpdatableRow output);
}
```

<span data-ttu-id="4b0d4-452">L’implémentation personnalisée d’une interface `ICombiner` doit contenir la définition pour un remplacement de `IEnumerable<IRow>` Combine.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-452">The custom implementation of an `ICombiner` interface should contain the definition for an `IEnumerable<IRow>` Combine override.</span></span>

```
[SqlUserDefinedCombiner]
public class MyCombiner : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    …
}
}
```

<span data-ttu-id="4b0d4-453">L’attribut **SqlUserDefinedCombiner** indique que le type doit être inscrit en tant que combinateur défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-453">The **SqlUserDefinedCombiner** attribute indicates that the type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="4b0d4-454">Cette classe ne peut pas être héritée.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-454">This class cannot be inherited.</span></span>

<span data-ttu-id="4b0d4-455">**SqlUserDefinedCombiner** est utilisée pour définir la propriété du mode de combinateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-455">**SqlUserDefinedCombiner** is used to define the Combiner mode property.</span></span> <span data-ttu-id="4b0d4-456">C’est un attribut facultatif pour une définition de combinateur défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="4b0d4-457">CombinerMode     Mode</span><span class="sxs-lookup"><span data-stu-id="4b0d4-457">CombinerMode     Mode</span></span>

<span data-ttu-id="4b0d4-458">L’énumération CombinerMode peut prendre les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-458">CombinerMode enum can take the following values:</span></span>

* <span data-ttu-id="4b0d4-459">Complète (0) Chaque ligne de sortie dépend potentiellement de toutes les lignes d’entrée de gauche et de droite avec la même valeur de clé.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-459">Full  (0) Every output row potentially depends on all the input rows from left and right       with the same key value.</span></span>

* <span data-ttu-id="4b0d4-460">Gauche (1) Chaque ligne de sortie dépend d’une seule ligne d’entrée de gauche (et potentiellement de toutes les lignes de droite avec la même valeur de clé).</span><span class="sxs-lookup"><span data-stu-id="4b0d4-460">Left  (1) Every output row depends on a single input row from the left (and potentially all rows       from the right with the same key value).</span></span>

* <span data-ttu-id="4b0d4-461">Droite (2) Chaque ligne de sortie dépend d’une seule ligne d’entrée de droite (et potentiellement de toutes les lignes de gauche avec la même valeur de clé).</span><span class="sxs-lookup"><span data-stu-id="4b0d4-461">Right (2)     Every output row depends on a single input row from the right (and potentially all rows       from the left with the same key value).</span></span>

* <span data-ttu-id="4b0d4-462">Interne (3) Chaque ligne de sortie dépend d’une seule ligne d’entrée de gauche et droite avec la même valeur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-462">Inner (3) Every output row depends on a single input row from left and right with the same value.</span></span>

<span data-ttu-id="4b0d4-463">Exemple :    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="4b0d4-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="4b0d4-464">Les principaux objets de programmabilité sont :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-464">The main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="4b0d4-465">Les ensembles de lignes d’entrée sont transmis en tant que type d’interface **gauche** et **droit** `IRowset`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="4b0d4-466">Les deux ensembles de lignes doivent être énumérés pour le traitement.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="4b0d4-467">Vous ne pouvez énumérer chaque interface qu’une seule fois. Il faut donc les énumérer et les mettre en cache si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-467">You can only enumerate each interface once, so we have to enumerate and cache it if necessary.</span></span>

<span data-ttu-id="4b0d4-468">Pour la mise en cache, nous pouvons créer un type List\<T\> de structure de mémoire résultant de l’exécution d’une requête LINQ, plus particulièrement List<`IRow`>.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="4b0d4-469">Le type de données anonymes peut également être utilisé pendant l’énumération.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-469">The anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="4b0d4-470">Pour plus d’informations sur les requêtes LINQ, voir [Introduction aux requêtes LINQ (C#)](https://msdn.microsoft.com/library/bb397906.aspx) et, pour plus d’informations sur l’interface IEnumerable\<T\>, voir [Interface IEnumerable\<T\>](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx).</span><span class="sxs-lookup"><span data-stu-id="4b0d4-470">See [Introduction to LINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="4b0d4-471">Pour obtenir les valeurs de données réelles du `IRowset` entrant, nous utilisons la méthode Get() de l’interface `IRow`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-471">To get the actual data values from the incoming `IRowset`, we use the Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="4b0d4-472">Les noms des colonnes peuvent être déterminés en appelant la méthode de schéma `IRow`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-472">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="4b0d4-473">Ou bien, en utilisant le nom de colonne de schéma :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-473">Or by using the schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="4b0d4-474">L’énumération générale avec LINQ prend la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-474">The general enumeration with LINQ looks like the following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="4b0d4-475">Après l’énumération des deux ensembles de lignes, nous allons exécuter une boucle sur toutes les lignes.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-475">After enumerating both rowsets, we are going to loop through all rows.</span></span> <span data-ttu-id="4b0d4-476">Pour chaque ligne de l’ensemble de lignes gauche, nous allons rechercher toutes les lignes remplissant la condition de notre combinateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-476">For each row in the left rowset, we are going to find all rows that satisfy the condition of our combiner.</span></span>

<span data-ttu-id="4b0d4-477">Les valeurs de sortie doivent être définies avec la sortie `IUpdatableRow`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-477">The output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="4b0d4-478">La sortie réelle est déclenchée par l’appel de `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-478">The actual output is triggered by calling to `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="4b0d4-479">Voici un exemple de combinateur :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-479">Following is a combiner example:</span></span>

```
[SqlUserDefinedCombiner]
public class CombineSales : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    var internetSales =
    (from row in left.Rows
          select new
          {
              ProductKey = row.Get<int>("ProductKey"),
              OrderDateKey = row.Get<int>("OrderDateKey"),
              SalesAmount = row.Get<decimal>("SalesAmount"),
              TaxAmt = row.Get<decimal>("TaxAmt")
          }).ToList();

    var resellerSales =
    (from row in right.Rows
     select new
     {
     ProductKey = row.Get<int>("ProductKey"),
     OrderDateKey = row.Get<int>("OrderDateKey"),
     SalesAmount = row.Get<decimal>("SalesAmount"),
     TaxAmt = row.Get<decimal>("TaxAmt")
     }).ToList();

    foreach (var row_i in internetSales)
    {
    foreach (var row_r in resellerSales)
    {

        if (
        row_i.OrderDateKey > 0
        && row_i.OrderDateKey < row_r.OrderDateKey
        && row_i.OrderDateKey == 20010701
        && (row_r.SalesAmount + row_r.TaxAmt) > 20000)
        {
        output.Set<int>("OrderDateKey", row_i.OrderDateKey);
        output.Set<int>("ProductKey", row_i.ProductKey);
        output.Set<decimal>("Internet_Sales_Amount", row_i.SalesAmount + row_i.TaxAmt);
        output.Set<decimal>("Reseller_Sales_Amount", row_r.SalesAmount + row_r.TaxAmt);
        }

    }
    }
    yield return output.AsReadOnly();
}
}
```

<span data-ttu-id="4b0d4-480">Dans ce scénario d’utilisation, nous créons un rapport analytique pour le détaillant.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-480">In this use-case scenario, we are building an analytics report for the retailer.</span></span> <span data-ttu-id="4b0d4-481">L’objectif est de rechercher tous les produits dont le prix est supérieur à 20 000 $, et dont la vente via le site web est plus rapide que via le détaillant standard au cours d’une période déterminée.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-481">The goal is to find all products that cost more than $20,000 and that sell through the website faster than through the regular retailer within a certain time frame.</span></span>

<span data-ttu-id="4b0d4-482">Voici le script U-SQL de base.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-482">Here is the base U-SQL script.</span></span> <span data-ttu-id="4b0d4-483">Vous pouvez comparer la logique entre une commande JOIN standard et un combinateur :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-483">You can compare the logic between a regular JOIN and a combiner:</span></span>

```sql
DECLARE @LocalURI string = @"\usql-programmability\";

DECLARE @input_file_internet_sales string = @LocalURI+"FactInternetSales.txt";
DECLARE @input_file_reseller_sales string = @LocalURI+"FactResellerSales.txt";
DECLARE @output_file1 string = @LocalURI+"output_file1.tsv";
DECLARE @output_file2 string = @LocalURI+"output_file2.tsv";

@fact_internet_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    CustomerKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_internet_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@fact_reseller_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    ResellerKey int ,
    EmployeeKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_reseller_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@rs1 =
SELECT
    fis.OrderDateKey,
    fis.ProductKey,
    fis.SalesAmount+fis.TaxAmt AS Internet_Sales_Amount,
    frs.SalesAmount+frs.TaxAmt AS Reseller_Sales_Amount
FROM @fact_internet_sales AS fis
     INNER JOIN @fact_reseller_sales AS frs
     ON fis.ProductKey == frs.ProductKey
WHERE
    fis.OrderDateKey < frs.OrderDateKey
    AND fis.OrderDateKey == 20010701
    AND frs.SalesAmount+frs.TaxAmt > 20000;

@rs2 =
COMBINE @fact_internet_sales AS fis
WITH @fact_reseller_sales AS frs
ON fis.ProductKey == frs.ProductKey
PRODUCE OrderDateKey int,
        ProductKey int,
        Internet_Sales_Amount decimal,
        Reseller_Sales_Amount decimal
USING new USQL_Programmability.CombineSales();

OUTPUT @rs1 TO @output_file1 USING Outputters.Tsv();
OUTPUT @rs2 TO @output_file2 USING Outputters.Tsv();
```

<span data-ttu-id="4b0d4-484">Un combinateur défini par l’utilisateur peut être appelé en tant que nouvelle instance de l’objet applicateur :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-484">A user-defined combiner can be called as a new instance of the applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="4b0d4-485">Ou par l’appel d’une méthode de fabrique de wrapper :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-485">Or with the invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="4b0d4-486">Utiliser des réducteurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="4b0d4-486">Use user-defined reducers</span></span>

<span data-ttu-id="4b0d4-487">U-SQL vous permet d’écrire des réducteurs d’ensemble de lignes personnalisés en C# en utilisant l’infrastructure d’extensibilité d’opérateur définie par l’utilisateur et en implémentant une interface IReducer.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-487">U-SQL enables you to write custom rowset reducers in C# by using the user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="4b0d4-488">Un réducteur défini par l’utilisateur (ou UDR) permet d’éliminer les lignes inutiles lors de l’extraction de données (importation).</span><span class="sxs-lookup"><span data-stu-id="4b0d4-488">User-defined reducer, or UDR, can be used to eliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="4b0d4-489">Il permet également de manipuler et d’évaluer les lignes et des colonnes.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-489">It also can be used to manipulate and evaluate rows and columns.</span></span> <span data-ttu-id="4b0d4-490">Sur la base d’une logique de programmabilité, il permet également de définir les lignes à extraire.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-490">Based on programmability logic, it can also define which rows need to be extracted.</span></span>

<span data-ttu-id="4b0d4-491">Pour définir une classe UDR, nous devons créer une interface `IReducer` avec un attribut facultatif `SqlUserDefinedReducer`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-491">To define a UDR class, we need to create an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="4b0d4-492">Cette interface de classe doit contenir une définition pour le remplacement de l’ensemble de lignes d’interface `IEnumerable`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-492">This class interface should contain a definition for the `IEnumerable` interface rowset override.</span></span>

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
        …
    }

}
```

<span data-ttu-id="4b0d4-493">L’attribut **SqlUserDefinedReducer** indique que le type doit être inscrit en tant que réducteur défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-493">The **SqlUserDefinedReducer** attribute indicates that the type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="4b0d4-494">Cette classe ne peut pas être héritée.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-494">This class cannot be inherited.</span></span>
<span data-ttu-id="4b0d4-495">**SqlUserDefinedReducer** est un attribut facultatif pour une définition de réducteur défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="4b0d4-496">Il est utilisé pour définir la propriété de IsRecursive.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-496">It's used to define IsRecursive property.</span></span>

* <span data-ttu-id="4b0d4-497">bool     IsRecursive</span><span class="sxs-lookup"><span data-stu-id="4b0d4-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="4b0d4-498">**true**  = indique si cette réduction est idempotente</span><span class="sxs-lookup"><span data-stu-id="4b0d4-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="4b0d4-499">Les principaux objets de programmabilité sont l’**entrée** et la **sortie**.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-499">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="4b0d4-500">L’objet d’entrée permet d’énumérer les lignes d’entrée.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-500">The input object is used to enumerate input rows.</span></span> <span data-ttu-id="4b0d4-501">La sortie est utilisée pour définir les lignes de sortie suite à l’activité de réduction.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-501">Output is used to set output rows as a result of reducing activity.</span></span>

<span data-ttu-id="4b0d4-502">Pour l’énumération des lignes d’entrée, nous utilisons la méthode `Row.Get`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-502">For input rows enumeration, we use the `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="4b0d4-503">Le paramètre pour la méthode `Row.Get` est une colonne transmise dans une classe `PRODUCE` de l’instruction `REDUCE` du script U-SQL de base.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-503">The parameter for the `Row.Get` method is a column that's passed as part of the `PRODUCE` class of the `REDUCE` statement of the U-SQL base script.</span></span> <span data-ttu-id="4b0d4-504">Nous devons utiliser le type de données correct ici également.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-504">We need to use the correct data type here as well.</span></span>

<span data-ttu-id="4b0d4-505">Pour la sortie, utilisez la méthode `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-505">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="4b0d4-506">Il est important de comprendre qu’un réducteur personnalisé ne génère que des valeurs définies avec l’appel de la méthode `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-506">It is important to understand that custom reducer only outputs values that are defined with the `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="4b0d4-507">La sortie réelle du réducteur est déclenchée par l’appel de `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-507">The actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="4b0d4-508">Voici un exemple de réducteur :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-508">Following is a reducer example:</span></span>

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
    string guid;
    DateTime dt;
    string user;
    string des;

    foreach (IRow row in input.Rows)
    {
        guid = row.Get<string>("guid");
        dt = row.Get<DateTime>("dt");
        user = row.Get<string>("user");
        des = row.Get<string>("des");

        if (user.Length > 0)
        {
        output.Set<string>("guid", guid);
        output.Set<DateTime>("dt", dt);
        output.Set<string>("user", user);
        output.Set<string>("des", des);

        yield return output.AsReadOnly();
        }
    }
    }

}
```

<span data-ttu-id="4b0d4-509">Dans ce scénario d’utilisation, le réducteur ignore les lignes dans lesquelles le nom d’utilisateur est vide.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-509">In this use-case scenario, the reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="4b0d4-510">Pour chaque ligne de l’ensemble de lignes, il lit chaque colonne requise, puis évalue la longueur du nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-510">For each row in rowset, it reads each required column, then evaluates the length of the user name.</span></span> <span data-ttu-id="4b0d4-511">Il génère la ligne réelle uniquement si la longueur du nom utilisateur est supérieure à 0.</span><span class="sxs-lookup"><span data-stu-id="4b0d4-511">It outputs the actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="4b0d4-512">Le script U-SQL de base utilisant un réducteur personnalisé est le suivant :</span><span class="sxs-lookup"><span data-stu-id="4b0d4-512">Following is base U-SQL script that uses a custom reducer:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file_reducer.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    REDUCE @rs0 PRESORT guid
    ON guid  
    PRODUCE guid string, dt DateTime, user String, des String
    USING new USQL_Programmability.EmptyUserReducer();

@rs2 =
    SELECT guid AS start_id,
           dt AS start_time,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS start_fiscalperiod,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    TO @output_file 
    USING Outputters.Text();
```
