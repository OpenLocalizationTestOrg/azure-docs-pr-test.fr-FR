---
title: guide de programmation aaaU-SQL pour Azure Data Lake | Documents Microsoft
description: "Obtenir des informations sur l’ensemble hello de services dans Azure Data Lake vous toocreate une plateforme en nuage big data."
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
ms.openlocfilehash: cc8f126234c6106a0dc633ce85a1d9ab1e634e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="d2f00-103">Guide de programmabilité U-SQL</span><span class="sxs-lookup"><span data-stu-id="d2f00-103">U-SQL programmability guide</span></span>

<span data-ttu-id="d2f00-104">U-SQL est un langage de requête spécifiquement conçu pour les charges de travail de type Big Data.</span><span class="sxs-lookup"><span data-stu-id="d2f00-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="d2f00-105">Une des fonctionnalités uniques de hello U-SQL est la combinaison de hello de langage déclaratif de type SQL hello extensibilité de hello et de programmabilité fournies par c#.</span><span class="sxs-lookup"><span data-stu-id="d2f00-105">One of hello unique features of U-SQL is hello combination of hello SQL-like declarative language with hello extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="d2f00-106">Dans ce guide, nous concentrer sur l’extensibilité de hello et de programmabilité de langue U-SQL hello prenant en charge par c#.</span><span class="sxs-lookup"><span data-stu-id="d2f00-106">In this guide, we concentrate on hello extensibility and programmability of hello U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="d2f00-107">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="d2f00-107">Requirements</span></span>

<span data-ttu-id="d2f00-108">Téléchargez et installez [Azure Data Lake Tools pour Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="d2f00-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="d2f00-109">Bien démarrer avec U-SQL</span><span class="sxs-lookup"><span data-stu-id="d2f00-109">Get started with U-SQL</span></span>  

<span data-ttu-id="d2f00-110">Examinons hello script U-SQL suivant :</span><span class="sxs-lookup"><span data-stu-id="d2f00-110">Let’s look at hello following U-SQL script:</span></span>

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

<span data-ttu-id="d2f00-111">Il définit un ensemble de lignes appelé @a et crée un ensemble de lignes appelé @results de @a.</span><span class="sxs-lookup"><span data-stu-id="d2f00-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="d2f00-112">Types et expressions C# dans les scripts U-SQL</span><span class="sxs-lookup"><span data-stu-id="d2f00-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="d2f00-113">Une Expression U-SQL est une expression C# combinée à des opérations logiques U-SQL comme `AND`, `OR` et `NOT`.</span><span class="sxs-lookup"><span data-stu-id="d2f00-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="d2f00-114">Les expressions U-SQL peuvent être utilisées avec SELECT, EXTRACT, WHERE, HAVING, GROUP BY et DECLARE.</span><span class="sxs-lookup"><span data-stu-id="d2f00-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="d2f00-115">Par exemple, hello script suivant analyse une chaîne représentant une valeur DateTime dans la clause SELECT de hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-115">For example, hello following script parses a string a DateTime value in hello SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="d2f00-116">Hello script suivant analyse une chaîne représentant une valeur de date/heure dans une instruction DECLARE.</span><span class="sxs-lookup"><span data-stu-id="d2f00-116">hello following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="d2f00-117">Utiliser des expressions C# pour les conversions de types de données</span><span class="sxs-lookup"><span data-stu-id="d2f00-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="d2f00-118">Bonjour à l’exemple suivant montre comment vous pouvez faire une conversion de données datetime à l’aide d’expressions c#.</span><span class="sxs-lookup"><span data-stu-id="d2f00-118">hello following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="d2f00-119">Dans ce scénario particulier, les données de type datetime de chaîne sont de type datetime toostandard converti notation de l’heure 00:00:00 minuit.</span><span class="sxs-lookup"><span data-stu-id="d2f00-119">In this particular scenario, string datetime data is converted toostandard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="d2f00-120">Utiliser des expressions C# pour la date du jour</span><span class="sxs-lookup"><span data-stu-id="d2f00-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="d2f00-121">toopull date d’aujourd'hui, nous pouvons utiliser hello expression c# suivante :</span><span class="sxs-lookup"><span data-stu-id="d2f00-121">toopull today’s date, we can use hello following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="d2f00-122">Voici un exemple de procédure toouse cette expression dans un script :</span><span class="sxs-lookup"><span data-stu-id="d2f00-122">Here's an example of how toouse this expression in a script:</span></span>

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



## <a name="using-net-assemblies"></a><span data-ttu-id="d2f00-123">Avec des assemblys .NET</span><span class="sxs-lookup"><span data-stu-id="d2f00-123">Using .NET assemblies</span></span>
<span data-ttu-id="d2f00-124">Modèle d’extensibilité de U-SQL s’appuie sur un code personnalisé hello capacité tooadd.</span><span class="sxs-lookup"><span data-stu-id="d2f00-124">U-SQL’s extensibility model relies heavily on hello ability tooadd custom code.</span></span> <span data-ttu-id="d2f00-125">Actuellement, U-SQL vous fournit des méthodes faciles tooadd votre propre Microsoft. Code de basée sur le réseau (en particulier, C#).</span><span class="sxs-lookup"><span data-stu-id="d2f00-125">Currently, U-SQL provides you with easy ways tooadd your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="d2f00-126">Toutefois, vous pouvez également ajouter du code personnalisé écrit dans d’autres langages .NET, tels que VB.NET ou F #.</span><span class="sxs-lookup"><span data-stu-id="d2f00-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="d2f00-127">Enregistrer un assembly .NET</span><span class="sxs-lookup"><span data-stu-id="d2f00-127">Register a .NET assembly</span></span>

<span data-ttu-id="d2f00-128">Utilisez hello CREATE ASSEMBLY instruction tooplace un assembly .NET dans une base de données U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d2f00-128">Use hello CREATE ASSEMBLY statement tooplace a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="d2f00-129">Une fois un assembly dans une base de données, scripts U-SQL peuvent utiliser ces assemblys à l’aide d’instruction d’ASSEMBLY de référence hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using hello REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="d2f00-130">Hello suivant de code montre comment tooregister un assembly :</span><span class="sxs-lookup"><span data-stu-id="d2f00-130">hello following code shows how tooregister an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="d2f00-131">Hello suivant de code montre comment tooreference un assembly :</span><span class="sxs-lookup"><span data-stu-id="d2f00-131">hello following code shows how tooreference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="d2f00-132">Consultez hello [instructions d’inscription d’assembly](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) qui traite ce sujet plus en détail.</span><span class="sxs-lookup"><span data-stu-id="d2f00-132">Consult hello [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="d2f00-133">Utilisez le contrôle de version des assemblys</span><span class="sxs-lookup"><span data-stu-id="d2f00-133">Use assembly versioning</span></span>
<span data-ttu-id="d2f00-134">Actuellement, U-SQL utilise hello .NET Framework version 4.5.</span><span class="sxs-lookup"><span data-stu-id="d2f00-134">Currently, U-SQL uses hello .NET Framework version 4.5.</span></span> <span data-ttu-id="d2f00-135">Par conséquent, assurez-vous que vos propres assemblys sont compatibles avec cette version de runtime de hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-135">So ensure that your own assemblies are compatible with that version of hello runtime.</span></span>

<span data-ttu-id="d2f00-136">Comme mentionné précédemment, U-SQL exécute le code dans un format 64 bits (x64).</span><span class="sxs-lookup"><span data-stu-id="d2f00-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="d2f00-137">Par conséquent, assurez-vous que votre code est compilé toorun sur x64.</span><span class="sxs-lookup"><span data-stu-id="d2f00-137">So make sure that your code is compiled toorun on x64.</span></span> <span data-ttu-id="d2f00-138">Dans le cas contraire, vous obtenez erreur de format incorrect de hello présentée précédemment.</span><span class="sxs-lookup"><span data-stu-id="d2f00-138">Otherwise you get hello incorrect format error shown earlier.</span></span>

<span data-ttu-id="d2f00-139">Chaque DLL d’assembly ou fichier de ressources chargé, comme un runtime différent, un assembly natif ou un fichier de configuration peut être de 400 Mo maximum.</span><span class="sxs-lookup"><span data-stu-id="d2f00-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="d2f00-140">taille totale de Hello de ressources déployées, via le déploiement de ressources ou tooassemblies de références et de leurs fichiers supplémentaires, ne peut pas dépasser 3 Go.</span><span class="sxs-lookup"><span data-stu-id="d2f00-140">hello total size of deployed resources, either via DEPLOY RESOURCE or via references tooassemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="d2f00-141">Enfin, notez que chaque base de données U-SQL ne peut contenir qu’une seule version d’un assembly donné.</span><span class="sxs-lookup"><span data-stu-id="d2f00-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="d2f00-142">Par exemple, si vous devez les versions 7 et 8 de hello NewtonSoft Json.Net bibliothèque, vous devez tooregister dans deux bases de données.</span><span class="sxs-lookup"><span data-stu-id="d2f00-142">For example, if you need both version 7 and version 8 of hello NewtonSoft Json.Net library, you need tooregister them in two different databases.</span></span> <span data-ttu-id="d2f00-143">En outre, chaque script peut uniquement faire référence version tooone d’une DLL d’assembly donné.</span><span class="sxs-lookup"><span data-stu-id="d2f00-143">Furthermore, each script can only refer tooone version of a given assembly DLL.</span></span> <span data-ttu-id="d2f00-144">À cet égard, U-SQL suit hello c# assembly gestion et le contrôle de version sémantique.</span><span class="sxs-lookup"><span data-stu-id="d2f00-144">In this respect, U-SQL follows hello C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="d2f00-145">Utiliser les fonctions définies par l’utilisateur : UDF</span><span class="sxs-lookup"><span data-stu-id="d2f00-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="d2f00-146">Fonctions U-SQL définies par l’utilisateur ou UDF, programmez des routines qui acceptent des paramètres, effectuer une action (par exemple, un calcul complexe) et retournent le résultat de hello de cette action en tant que valeur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return hello result of that action as a value.</span></span> <span data-ttu-id="d2f00-147">Hello retournent la valeur de UDF ne peut être une valeur scalaire unique.</span><span class="sxs-lookup"><span data-stu-id="d2f00-147">hello return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="d2f00-148">Une fonction définie par l’utilisateur U-SQL peut être appelée dans un script U-SQL de base comme toute autre fonction scalaire C#.</span><span class="sxs-lookup"><span data-stu-id="d2f00-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="d2f00-149">Nous vous recommandons d’initialiser les fonctions définies par l’utilisateur U-SQL en tant que **publiques** et **statiques**.</span><span class="sxs-lookup"><span data-stu-id="d2f00-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="d2f00-150">Première Examinons hello un exemple simple de création d’un fichier UDF.</span><span class="sxs-lookup"><span data-stu-id="d2f00-150">First let’s look at hello simple example of creating a UDF.</span></span>

<span data-ttu-id="d2f00-151">Dans ce scénario de cas d’utilisation, nous devons toodetermine hello période, y compris le trimestre fiscal de hello et mois fiscal de hello première connexion d’utilisateur spécifique de hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-151">In this use-case scenario, we need toodetermine hello fiscal period, including hello fiscal quarter and fiscal month of hello first sign-in for hello specific user.</span></span> <span data-ttu-id="d2f00-152">Hello premier mois fiscal de l’année hello dans notre scénario est juin.</span><span class="sxs-lookup"><span data-stu-id="d2f00-152">hello first fiscal month of hello year in our scenario is June.</span></span>

<span data-ttu-id="d2f00-153">exercice toocalculate, nous introduisons hello suivant fonction c# :</span><span class="sxs-lookup"><span data-stu-id="d2f00-153">toocalculate fiscal period, we introduce hello following C# function:</span></span>

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

<span data-ttu-id="d2f00-154">La fonction calcule simplement le trimestre et le mois fiscaux, puis retourne une valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="d2f00-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="d2f00-155">De juin, hello premier mois de hello premier trimestre fiscal, nous utilisons « Q1:P1 ».</span><span class="sxs-lookup"><span data-stu-id="d2f00-155">For June, hello first month of hello first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="d2f00-156">Pour le mois de juillet, nous utilisons « Q1:P2 », etc.</span><span class="sxs-lookup"><span data-stu-id="d2f00-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="d2f00-157">Il s’agit d’une fonction c# régulière que nous sommes continu toouse dans notre projet U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d2f00-157">This is a regular C# function that we are going toouse in our U-SQL project.</span></span>

<span data-ttu-id="d2f00-158">Voici l’aspect de la section de code-behind hello dans ce scénario :</span><span class="sxs-lookup"><span data-stu-id="d2f00-158">Here is how hello code-behind section looks in this scenario:</span></span>

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

<span data-ttu-id="d2f00-159">Nous allons maintenant toocall cette fonction à partir du script U-SQL de la base hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-159">Now we are going toocall this function from hello base U-SQL script.</span></span> <span data-ttu-id="d2f00-160">toodo, nous avons tooprovide un nom qualifié complet pour la fonction hello, y compris hello, espace de noms, qui est dans ce cas NameSpace.Class.Function(parameter).</span><span class="sxs-lookup"><span data-stu-id="d2f00-160">toodo this, we have tooprovide a fully qualified name for hello function, including hello namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="d2f00-161">Voici hello base script U-SQL réel :</span><span class="sxs-lookup"><span data-stu-id="d2f00-161">Following is hello actual U-SQL base script:</span></span>

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
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="d2f00-162">Voici le fichier de sortie hello hello d’exécution du script :</span><span class="sxs-lookup"><span data-stu-id="d2f00-162">Following is hello output file of hello script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="d2f00-163">Cet exemple illustre une utilisation simple d’une fonction définie par l’utilisateur inline dans U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d2f00-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="d2f00-164">Conserver l’état entre des appels de fonction définie par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d2f00-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="d2f00-165">Les objets de programmabilité c# U-SQL peuvent être plus sophistiquées, utilisant l’interactivité des variables globales du code-behind hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through hello code-behind global variables.</span></span> <span data-ttu-id="d2f00-166">Examinons hello suivant le scénario d’entreprise en cas d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="d2f00-166">Let’s look at hello following business use-case scenario.</span></span>

<span data-ttu-id="d2f00-167">Dans les grandes organisations, les utilisateurs peuvent basculer entre divers types d’applications internes.</span><span class="sxs-lookup"><span data-stu-id="d2f00-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="d2f00-168">Celles-ci peuvent inclure Microsoft Dynamics CRM, Power BI, etc.</span><span class="sxs-lookup"><span data-stu-id="d2f00-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="d2f00-169">Clients pourriez tooapply une analyse de télémétrie de la façon dont les utilisateurs basculent entre différentes applications, des tendances de consommation hello sont et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="d2f00-169">Customers might want tooapply a telemetry analysis of how users switch between different applications, what hello usage trends are, and so on.</span></span> <span data-ttu-id="d2f00-170">objectif de Hello pour les entreprises hello est toooptimize l’utilisation des applications.</span><span class="sxs-lookup"><span data-stu-id="d2f00-170">hello goal for hello business is toooptimize application usage.</span></span> <span data-ttu-id="d2f00-171">Ils peuvent également toocombine différentes applications ou des routines d’authentification spécifiques.</span><span class="sxs-lookup"><span data-stu-id="d2f00-171">They also might want toocombine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="d2f00-172">tooachieve cet objectif, nous avons toodetermine ID de session et de retard entre hello dernière session s’est produite.</span><span class="sxs-lookup"><span data-stu-id="d2f00-172">tooachieve this goal, we have toodetermine session IDs and lag time between hello last session that occurred.</span></span>

<span data-ttu-id="d2f00-173">Nous devez toofind une connexion à précédente, puis d’affecter cette connexion tooall les sessions qui sont en cours toohello généré même application.</span><span class="sxs-lookup"><span data-stu-id="d2f00-173">We need toofind a previous sign-in and then assign this sign-in tooall sessions that are being generated toohello same application.</span></span> <span data-ttu-id="d2f00-174">premier test de Hello est que script de base U-SQL n’autorise pas nous tooapply des calculs sur les colonnes calculées déjà avec la fonction LAG.</span><span class="sxs-lookup"><span data-stu-id="d2f00-174">hello first challenge is that U-SQL base script doesn't allow us tooapply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="d2f00-175">Hello deuxième défi est que nous avons session spécifique de tookeep hello pour toutes les sessions dans hello même période.</span><span class="sxs-lookup"><span data-stu-id="d2f00-175">hello second challenge is that we have tookeep hello specific session for all sessions within hello same time period.</span></span>

<span data-ttu-id="d2f00-176">toosolve ce problème, nous utilisons une variable globale à l’intérieur d’une section de code-behind : `static public string globalSession;`.</span><span class="sxs-lookup"><span data-stu-id="d2f00-176">toosolve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="d2f00-177">Cette variable globale est ensemble de lignes entier toohello appliquée pendant l’exécution du script.</span><span class="sxs-lookup"><span data-stu-id="d2f00-177">This global variable is applied toohello entire rowset during our script execution.</span></span>

<span data-ttu-id="d2f00-178">Voici la section de code-behind hello de notre programme U-SQL :</span><span class="sxs-lookup"><span data-stu-id="d2f00-178">Here is hello code-behind section of our U-SQL program:</span></span>

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

<span data-ttu-id="d2f00-179">Cet exemple affiche hello variable globale `static public string globalSession;` utilisé à l’intérieur de hello `getStampUserSession` fonction et l’obtention de réinitialisation chaque hello temps Session paramètre est modifié.</span><span class="sxs-lookup"><span data-stu-id="d2f00-179">This example shows hello global variable `static public string globalSession;` used inside hello `getStampUserSession` function and getting reinitialized each time hello Session parameter is changed.</span></span>

<span data-ttu-id="d2f00-180">Hello U-SQL script de base est la suivante :</span><span class="sxs-lookup"><span data-stu-id="d2f00-180">hello U-SQL base script is as follows:</span></span>

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
    too@out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

<span data-ttu-id="d2f00-181">Fonction `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` est appelée ici lors du calcul de hello deuxième mémoire ensemble de lignes.</span><span class="sxs-lookup"><span data-stu-id="d2f00-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during hello second memory rowset calculation.</span></span> <span data-ttu-id="d2f00-182">Il passe hello `UserSessionTimestamp` colonne et renvoie hello valeur jusqu'à ce que `UserSessionTimestamp` a changé.</span><span class="sxs-lookup"><span data-stu-id="d2f00-182">It passes hello `UserSessionTimestamp` column and returns hello value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="d2f00-183">fichier de sortie Hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="d2f00-183">hello output file is as follows:</span></span>

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

<span data-ttu-id="d2f00-184">Cet exemple illustre un scénario de cas d’usage plus complexe dans lequel nous utilisons une variable globale à l’intérieur d’une section de code-behind qui est l’ensemble de lignes de mémoire complète toohello appliqué.</span><span class="sxs-lookup"><span data-stu-id="d2f00-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied toohello entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="d2f00-185">Utiliser des types définis par l’utilisateur (UDT)</span><span class="sxs-lookup"><span data-stu-id="d2f00-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="d2f00-186">Les types définis par l’utilisateur (ou UDT) sont une autre fonctionnalité de programmabilité de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d2f00-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="d2f00-187">Un type défini par l’utilisateur U-SQL agit comme un type défini par l’utilisateur C# standard.</span><span class="sxs-lookup"><span data-stu-id="d2f00-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="d2f00-188">C# est un langage fortement typé qui autorise l’utilisation de hello de types intégrés et personnalisés définis par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-188">C# is a strongly typed language that allows hello use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="d2f00-189">U-SQL ne peut pas implicitement sérialiser ou désérialiser l’UDT arbitraires est hello UDT est passé entre les sommets dans les ensembles de lignes.</span><span class="sxs-lookup"><span data-stu-id="d2f00-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when hello UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="d2f00-190">Cela signifie que l’utilisateur hello tooprovide un formateur explicite à l’aide hello IFormatter interface.</span><span class="sxs-lookup"><span data-stu-id="d2f00-190">This means that hello user has tooprovide an explicit formatter by using hello IFormatter interface.</span></span> <span data-ttu-id="d2f00-191">Cela fournit U-SQL hello sérialiser et désérialiser des méthodes pour hello UDT.</span><span class="sxs-lookup"><span data-stu-id="d2f00-191">This provides U-SQL with hello serialize and de-serialize methods for hello UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="d2f00-192">U-SQL extracteurs intégrés et outputters actuellement ne peut pas sérialiser ou désérialiser tooor de données UDT à partir de fichiers, même avec hello IFormatter ensemble.</span><span class="sxs-lookup"><span data-stu-id="d2f00-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data tooor from files even with hello IFormatter set.</span></span> <span data-ttu-id="d2f00-193">Par conséquent, lorsque vous écrivez un fichier de tooa de données UDT avec hello instruction OUTPUT ou lire avec un extracteur de, vous avez toopass sous la forme d’un chaîne ou tableau d’octets.</span><span class="sxs-lookup"><span data-stu-id="d2f00-193">So when you're writing UDT data tooa file with hello OUTPUT statement, or reading it with an extractor, you have toopass it as a string or byte array.</span></span> <span data-ttu-id="d2f00-194">Puis vous appelez sérialisation de hello et de désérialisation explicitement de code (autrement dit, la méthode ToString() hello par l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="d2f00-194">Then you call hello serialization and deserialization code (that is, hello UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="d2f00-195">Extracteurs de défini par l’utilisateur et outputters, sur hello autres main, peuvent lire et écrire les UDT.</span><span class="sxs-lookup"><span data-stu-id="d2f00-195">User-defined extractors and outputters, on hello other hand, can read and write UDTs.</span></span>

<span data-ttu-id="d2f00-196">Si nous essayons toouse UDT dans extracteur ou OUTPUTTER (hors SELECT précédente), comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="d2f00-196">If we try toouse UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="d2f00-197">Nous recevons hello l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="d2f00-197">We receive hello following error:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used toooutput column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how tooserialize this type, or call a serialization method on hello type in
hello preceding SELECT. C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

<span data-ttu-id="d2f00-198">toowork avec UDT dans outputter, nous avons soit tooserialize il toostring avec hello méthode ToString() ou créer un outputter personnalisé.</span><span class="sxs-lookup"><span data-stu-id="d2f00-198">toowork with UDT in outputter, we either have tooserialize it toostring with hello ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="d2f00-199">Il n’est actuellement pas possible d’utiliser des types définis par l’utilisateur dans une instruction GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="d2f00-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="d2f00-200">Si l’UDT est utilisé dans GROUP BY, hello l’erreur suivante est levée :</span><span class="sxs-lookup"><span data-stu-id="d2f00-200">If UDT is used in GROUP BY, hello following error is thrown:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want toouse with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

<span data-ttu-id="d2f00-201">toodefine un UDT, il faut :</span><span class="sxs-lookup"><span data-stu-id="d2f00-201">toodefine a UDT, we have to:</span></span>

* <span data-ttu-id="d2f00-202">Ajoutez hello suivant des espaces de noms :</span><span class="sxs-lookup"><span data-stu-id="d2f00-202">Add hello following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="d2f00-203">Ajouter `Microsoft.Analytics.Interfaces`, ce qui est nécessaire pour les interfaces d’UDT hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-203">Add `Microsoft.Analytics.Interfaces`, which is required for hello UDT interfaces.</span></span> <span data-ttu-id="d2f00-204">En outre, `System.IO` toodefine nécessaires hello IFormatter interface peut se.</span><span class="sxs-lookup"><span data-stu-id="d2f00-204">In addition, `System.IO` might be needed toodefine hello IFormatter interface.</span></span>

* <span data-ttu-id="d2f00-205">Définir un type défini par l’utilisateur avec l’attribut SqlUserDefinedType.</span><span class="sxs-lookup"><span data-stu-id="d2f00-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="d2f00-206">**SqlUserDefinedType** est toomark utilisé une définition de type dans un assembly comme étant un type défini par l’utilisateur (UDT) dans U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d2f00-206">**SqlUserDefinedType** is used toomark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="d2f00-207">propriétés de Hello sur l’attribut de hello reflètent les caractéristiques physiques de hello Hello UDT.</span><span class="sxs-lookup"><span data-stu-id="d2f00-207">hello properties on hello attribute reflect hello physical characteristics of hello UDT.</span></span> <span data-ttu-id="d2f00-208">Cette classe ne peut pas être héritée.</span><span class="sxs-lookup"><span data-stu-id="d2f00-208">This class cannot be inherited.</span></span>

<span data-ttu-id="d2f00-209">SqlUserDefinedType est un attribut obligatoire pour la définition du type défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="d2f00-210">constructeur Hello de classe hello :</span><span class="sxs-lookup"><span data-stu-id="d2f00-210">hello constructor of hello class:</span></span>  

* <span data-ttu-id="d2f00-211">SqlUserDefinedTypeAttribute (formateur de type)</span><span class="sxs-lookup"><span data-stu-id="d2f00-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="d2f00-212">Formateur de type : requis du paramètre toodefine du module de formatage de l’UDT--plus précisément, le type de hello Hello `IFormatter` interface doit être passé ici.</span><span class="sxs-lookup"><span data-stu-id="d2f00-212">Type formatter: Required parameter toodefine an UDT formatter--specifically, hello type of hello `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="d2f00-213">UDT classique requiert également la définition d’interface de IFormatter hello, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d2f00-213">Typical UDT also requires definition of hello IFormatter interface, as shown in hello following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="d2f00-214">Hello `IFormatter` interface sérialise et désérialise un graphique d’objet avec le type de racine hello \<typeparamref nom = « T » >.</span><span class="sxs-lookup"><span data-stu-id="d2f00-214">hello `IFormatter` interface serializes and de-serializes an object graph with hello root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="d2f00-215">\<typeparam nom = « T » > Bonjour type racine pour tooserialize de graphique d’objet hello et désérialiser.</span><span class="sxs-lookup"><span data-stu-id="d2f00-215">\<typeparam name="T">hello root type for hello object graph tooserialize and de-serialize.</span></span>

* <span data-ttu-id="d2f00-216">**Désérialiser**: données hello sur les flux hello fourni est désérialisée et reconstitue graphique hello d’objets.</span><span class="sxs-lookup"><span data-stu-id="d2f00-216">**Deserialize**: De-serializes hello data on hello provided stream and reconstitutes hello graph of objects.</span></span>

* <span data-ttu-id="d2f00-217">**Sérialiser**: sérialise un objet ou un graphique d’objets, avec hello racine toohello fourni flux donné.</span><span class="sxs-lookup"><span data-stu-id="d2f00-217">**Serialize**: Serializes an object, or graph of objects, with hello given root toohello provided stream.</span></span>

<span data-ttu-id="d2f00-218">`MyType`instance : Instance de type de hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-218">`MyType` instance: Instance of hello type.</span></span>  
<span data-ttu-id="d2f00-219">`IColumnWriter`enregistreur / `IColumnReader` lecteur : hello sous-jacent de flux de données de colonne.</span><span class="sxs-lookup"><span data-stu-id="d2f00-219">`IColumnWriter` writer / `IColumnReader` reader: hello underlying column stream.</span></span>  
<span data-ttu-id="d2f00-220">`ISerializationContext`contexte : énumération qui définit un ensemble d’indicateurs qui spécifie le contexte de source ou destination hello pour les flux hello pendant la sérialisation.</span><span class="sxs-lookup"><span data-stu-id="d2f00-220">`ISerializationContext` context: Enum that defines a set of flags that specifies hello source or destination context for hello stream during serialization.</span></span>

* <span data-ttu-id="d2f00-221">**Intermédiaire**: Spécifie que contexte source ou la destination de hello n’est pas un magasin persistant.</span><span class="sxs-lookup"><span data-stu-id="d2f00-221">**Intermediate**: Specifies that hello source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="d2f00-222">**Persistance**: Spécifie que contexte source ou la destination de hello est un magasin persistant.</span><span class="sxs-lookup"><span data-stu-id="d2f00-222">**Persistence**: Specifies that hello source or destination context is a persisted store.</span></span>

<span data-ttu-id="d2f00-223">En tant que type C# standard, une définition de type défini par l’utilisateur U-SQL peut inclure des remplacements pour des opérateurs tels que +/==/!=.</span><span class="sxs-lookup"><span data-stu-id="d2f00-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="d2f00-224">Elle peut également inclure des méthodes statiques.</span><span class="sxs-lookup"><span data-stu-id="d2f00-224">It can also include static methods.</span></span> <span data-ttu-id="d2f00-225">Par exemple, si nous devons toouse cet UDT comme une fonction d’agrégation MIN de U-SQL de tooa paramètre, nous avons toodefine < remplacement de l’opérateur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-225">For example, if we are going toouse this UDT as a parameter tooa U-SQL MIN aggregate function, we have toodefine < operator override.</span></span>

<span data-ttu-id="d2f00-226">Plus haut dans ce guide, nous l’avons démontré un exemple pour l’identification de période fiscale à partir de la date spécifique de hello dans le format hello Qn:Pn (Q1:P10).</span><span class="sxs-lookup"><span data-stu-id="d2f00-226">Earlier in this guide, we demonstrated an example for fiscal period identification from hello specific date in hello format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="d2f00-227">Bonjour à l’exemple suivant montre comment toodefine personnalisé de type pour les valeurs de la période fiscales.</span><span class="sxs-lookup"><span data-stu-id="d2f00-227">hello following example shows how toodefine a custom type for fiscal period values.</span></span>

<span data-ttu-id="d2f00-228">Vous trouverez ci-dessous un exemple de section code-behind avec un type défini par l’utilisateur et une interface personnalisée IFormatter :</span><span class="sxs-lookup"><span data-stu-id="d2f00-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

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

<span data-ttu-id="d2f00-229">type défini Hello inclut deux nombres : trimestre et mois.</span><span class="sxs-lookup"><span data-stu-id="d2f00-229">hello defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="d2f00-230">Les opérateurs ==/!=/>/< et la méthode statique ToString() sont définis ici.</span><span class="sxs-lookup"><span data-stu-id="d2f00-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="d2f00-231">Comme mentionné précédemment, le type défini par l’utilisateur peut être utilisé dans des expressions SELECT, mais pas dans un GÉNÉRATEUR DE SORTIE/EXTRACTEUR sans sérialisation personnalisée.</span><span class="sxs-lookup"><span data-stu-id="d2f00-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="d2f00-232">Il a toobe sérialisées sous forme de chaîne avec ToString() ou utilisé avec un extracteur de OUTPUTTER/personnalisé.</span><span class="sxs-lookup"><span data-stu-id="d2f00-232">It either has toobe serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="d2f00-233">Voyons à présent l’usage d’un type défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="d2f00-234">Dans une section de code-behind, nous avons modifié nos suivant toohello de fonction GetFiscalPeriod :</span><span class="sxs-lookup"><span data-stu-id="d2f00-234">In a code-behind section, we changed our GetFiscalPeriod function toohello following:</span></span>

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

<span data-ttu-id="d2f00-235">Comme vous pouvez le voir, il retourne la valeur hello de notre type FiscalPeriod.</span><span class="sxs-lookup"><span data-stu-id="d2f00-235">As you can see, it returns hello value of our FiscalPeriod type.</span></span>

<span data-ttu-id="d2f00-236">Nous proposons un exemple de comment toouse ultérieurement dans le script de base U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d2f00-236">Here we provide an example of how toouse it further in U-SQL base script.</span></span> <span data-ttu-id="d2f00-237">Cet exemple illustre différentes façons d’appeler un type défini par l’utilisateur à partir d’un script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d2f00-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

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

       // This user-defined type was created in hello prior SELECT.  Passing hello UDT toothis subsequent SELECT would have failed if hello UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="d2f00-238">Voici un exemple d’une section code-behind complète :</span><span class="sxs-lookup"><span data-stu-id="d2f00-238">Here's an example of a full code-behind section:</span></span>

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

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="d2f00-239">Utiliser des agrégats définis par l’utilisateur : UDAGG</span><span class="sxs-lookup"><span data-stu-id="d2f00-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="d2f00-240">Les agrégats définis par l’utilisateur sont toutes les fonctions d’agrégation qui ne sont pas fournies prêtes à l’emploi avec U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d2f00-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="d2f00-241">Hello exemple peut être une agrégation tooperform calculs mathématiques personnalisées, des concaténations de chaînes, les manipulations de chaînes et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="d2f00-241">hello example can be an aggregate tooperform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="d2f00-242">définition de classe de base d’agrégation définies par l’utilisateur Hello est la suivante :</span><span class="sxs-lookup"><span data-stu-id="d2f00-242">hello user-defined aggregate base class definition is as follows:</span></span>

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

<span data-ttu-id="d2f00-243">**SqlUserDefinedAggregate** indique que le type de hello doit être enregistré comme un agrégat défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-243">**SqlUserDefinedAggregate** indicates that hello type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="d2f00-244">Cette classe ne peut pas être héritée.</span><span class="sxs-lookup"><span data-stu-id="d2f00-244">This class cannot be inherited.</span></span>

<span data-ttu-id="d2f00-245">L’attribut SqlUserDefinedType est **facultatif** pour la définition d’UDAGG.</span><span class="sxs-lookup"><span data-stu-id="d2f00-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="d2f00-246">Hello classe de base vous permet de paramètres de description toopass trois : deux comme paramètres d’entrée et l’autre comme résultat de hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-246">hello base class allows you toopass three abstract parameters: two as input parameters and one as hello result.</span></span> <span data-ttu-id="d2f00-247">types de données Hello sont variable et doivent être définies lors de l’héritage de classe.</span><span class="sxs-lookup"><span data-stu-id="d2f00-247">hello data types are variable and should be defined during class inheritance.</span></span>

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

* <span data-ttu-id="d2f00-248">**Init** appelle une seule fois chaque groupe pendant le calcul.</span><span class="sxs-lookup"><span data-stu-id="d2f00-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="d2f00-249">Elle fournit une routine d’initialisation pour chaque groupe d’agrégation.</span><span class="sxs-lookup"><span data-stu-id="d2f00-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="d2f00-250">**Accumulate** est exécutée une fois pour chaque valeur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="d2f00-251">Il fournit des fonctionnalités principales de hello pour l’algorithme d’agrégation hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-251">It provides hello main functionality for hello aggregation algorithm.</span></span> <span data-ttu-id="d2f00-252">Il peut être valeurs tooaggregate utilisés avec divers types de données qui sont définis lors de l’héritage de classe.</span><span class="sxs-lookup"><span data-stu-id="d2f00-252">It can be used tooaggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="d2f00-253">Elle peut accepter deux paramètres de types de données variables.</span><span class="sxs-lookup"><span data-stu-id="d2f00-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="d2f00-254">**Mettre fin à** est exécutée une fois par groupe d’agrégation à hello du traitement du résultat de hello toooutput pour chaque groupe.</span><span class="sxs-lookup"><span data-stu-id="d2f00-254">**Terminate** is executed once per aggregation group at hello end of processing toooutput hello result for each group.</span></span>

<span data-ttu-id="d2f00-255">entrée correcte de toodeclare et les types de données de sortie, utilisez définition de classe hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="d2f00-255">toodeclare correct input and output data types, use hello class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="d2f00-256">T1 : Premier paramètre tooaccumulate</span><span class="sxs-lookup"><span data-stu-id="d2f00-256">T1: First parameter tooaccumulate</span></span>
* <span data-ttu-id="d2f00-257">T2 : Premier paramètre tooaccumulate</span><span class="sxs-lookup"><span data-stu-id="d2f00-257">T2: First parameter tooaccumulate</span></span>
* <span data-ttu-id="d2f00-258">TResult : type de retour de la routine terminate</span><span class="sxs-lookup"><span data-stu-id="d2f00-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="d2f00-259">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="d2f00-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="d2f00-260">ou</span><span class="sxs-lookup"><span data-stu-id="d2f00-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="d2f00-261">Utiliser UDAGG dans U-SQL</span><span class="sxs-lookup"><span data-stu-id="d2f00-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="d2f00-262">toouse UDAGG, tout d’abord la définir dans le code-behind ou référencer à partir de la programmabilité inexistant hello DLL comme indiqué précédemment.</span><span class="sxs-lookup"><span data-stu-id="d2f00-262">toouse UDAGG, first define it in code-behind or reference it from hello existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="d2f00-263">Utilisez ensuite hello selon la syntaxe :</span><span class="sxs-lookup"><span data-stu-id="d2f00-263">Then use hello following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="d2f00-264">Voici l’exemple d’UDAGG :</span><span class="sxs-lookup"><span data-stu-id="d2f00-264">Here is an example of UDAGG:</span></span>

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

<span data-ttu-id="d2f00-265">Et le script U-SQL de base :</span><span class="sxs-lookup"><span data-stu-id="d2f00-265">And base U-SQL script:</span></span>

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

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

<span data-ttu-id="d2f00-266">Dans ce scénario de cas d’utilisation, nous concaténer la classe GUID pour des utilisateurs spécifiques hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-266">In this use-case scenario, we concatenate class GUIDs for hello specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="d2f00-267">Utiliser des objets définis par l’utilisateur : UDO</span><span class="sxs-lookup"><span data-stu-id="d2f00-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="d2f00-268">U-SQL vous permet de toodefine les objets de programmabilité personnalisés qui sont appelés objets définis par l’utilisateur ou l’opérateur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-268">U-SQL enables you toodefine custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="d2f00-269">Hello Voici une liste de UDO dans U-SQL :</span><span class="sxs-lookup"><span data-stu-id="d2f00-269">hello following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="d2f00-270">Extracteurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d2f00-270">User-defined extractors</span></span>
    * <span data-ttu-id="d2f00-271">Extraient ligne par ligne</span><span class="sxs-lookup"><span data-stu-id="d2f00-271">Extract row by row</span></span>
    * <span data-ttu-id="d2f00-272">Utilisé tooimplement d’extraction de données à partir de fichiers structurés personnalisés</span><span class="sxs-lookup"><span data-stu-id="d2f00-272">Used tooimplement data extraction from custom structured files</span></span>

* <span data-ttu-id="d2f00-273">Générateurs de sortie définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d2f00-273">User-defined outputters</span></span>
    * <span data-ttu-id="d2f00-274">Sortent ligne par ligne</span><span class="sxs-lookup"><span data-stu-id="d2f00-274">Output row by row</span></span>
    * <span data-ttu-id="d2f00-275">Utilisé toooutput les types de données personnalisés ou des formats de fichiers personnalisés</span><span class="sxs-lookup"><span data-stu-id="d2f00-275">Used toooutput custom data types or custom file formats</span></span>

* <span data-ttu-id="d2f00-276">Processeurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d2f00-276">User-defined processors</span></span>
    * <span data-ttu-id="d2f00-277">Prennent une ligne et produisent une ligne</span><span class="sxs-lookup"><span data-stu-id="d2f00-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="d2f00-278">Tooreduce utilisé hello le nombre de colonnes ou produire de nouvelles colonnes avec des valeurs dérivées d’un ensemble existant de la colonne</span><span class="sxs-lookup"><span data-stu-id="d2f00-278">Used tooreduce hello number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="d2f00-279">Applicateurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d2f00-279">User-defined appliers</span></span>
    * <span data-ttu-id="d2f00-280">Prendre une ligne et génère des lignes d’on à 0</span><span class="sxs-lookup"><span data-stu-id="d2f00-280">Take one row and produce 0 toon rows</span></span>
    * <span data-ttu-id="d2f00-281">Utilisés avec OUTER/CROSS APPLY</span><span class="sxs-lookup"><span data-stu-id="d2f00-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="d2f00-282">Combinateurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d2f00-282">User-defined combiners</span></span>
    * <span data-ttu-id="d2f00-283">Combinent des ensembles de lignes et des jointures définies par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d2f00-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="d2f00-284">Réducteurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d2f00-284">User-defined reducers</span></span>
    * <span data-ttu-id="d2f00-285">Prennent n lignes et produisent une ligne</span><span class="sxs-lookup"><span data-stu-id="d2f00-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="d2f00-286">Nombre de hello tooreduce de lignes</span><span class="sxs-lookup"><span data-stu-id="d2f00-286">Used tooreduce hello number of rows</span></span>

<span data-ttu-id="d2f00-287">OPÉRATEUR est généralement appelée explicitement dans le script U-SQL dans le cadre de hello suivant les instructions U-SQL :</span><span class="sxs-lookup"><span data-stu-id="d2f00-287">UDO is typically called explicitly in U-SQL script as part of hello following U-SQL statements:</span></span>

* <span data-ttu-id="d2f00-288">EXTRACT</span><span class="sxs-lookup"><span data-stu-id="d2f00-288">EXTRACT</span></span>
* <span data-ttu-id="d2f00-289">OUTPUT</span><span class="sxs-lookup"><span data-stu-id="d2f00-289">OUTPUT</span></span>
* <span data-ttu-id="d2f00-290">PROCESS</span><span class="sxs-lookup"><span data-stu-id="d2f00-290">PROCESS</span></span>
* <span data-ttu-id="d2f00-291">COMBINE</span><span class="sxs-lookup"><span data-stu-id="d2f00-291">COMBINE</span></span>
* <span data-ttu-id="d2f00-292">REDUCE</span><span class="sxs-lookup"><span data-stu-id="d2f00-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="d2f00-293">OPÉRATEUR est limitées tooconsume 0,5 Go de mémoire.</span><span class="sxs-lookup"><span data-stu-id="d2f00-293">UDO’s are limited tooconsume 0.5Gb memory.</span></span>  <span data-ttu-id="d2f00-294">Cette limitation de mémoire ne s’applique pas toolocal exécutions.</span><span class="sxs-lookup"><span data-stu-id="d2f00-294">This memory limitation does not apply toolocal executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="d2f00-295">Utiliser des extracteurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d2f00-295">Use user-defined extractors</span></span>
<span data-ttu-id="d2f00-296">U-SQL vous permet de tooimport des données externes à l’aide d’une instruction d’extraction.</span><span class="sxs-lookup"><span data-stu-id="d2f00-296">U-SQL allows you tooimport external data by using an EXTRACT statement.</span></span> <span data-ttu-id="d2f00-297">Une instruction EXTRACT peut utiliser des extracteurs UDO intégrés :</span><span class="sxs-lookup"><span data-stu-id="d2f00-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="d2f00-298">*Extractors.Text()* : produit une extraction à partir de fichiers texte délimités de codages différents.</span><span class="sxs-lookup"><span data-stu-id="d2f00-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="d2f00-299">*Extractors.Csv()* : produit une extraction à partir de fichiers de valeurs séparées par des virgules (CSV) de codages différents.</span><span class="sxs-lookup"><span data-stu-id="d2f00-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="d2f00-300">*Extractors.Tsv()* : produit une extraction à partir de fichiers de valeurs séparées par des tabulations (TSV) de codages différents.</span><span class="sxs-lookup"><span data-stu-id="d2f00-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="d2f00-301">Il peut être utile toodevelop un extracteur personnalisé.</span><span class="sxs-lookup"><span data-stu-id="d2f00-301">It can be useful toodevelop a custom extractor.</span></span> <span data-ttu-id="d2f00-302">Cela peut être utile lors de l’importation de données si vous souhaitez toodo des hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="d2f00-302">This can be helpful during data import if we want toodo any of hello following tasks:</span></span>

* <span data-ttu-id="d2f00-303">Modifier des données d’entrée en fractionnant des colonnes et en modifiant des valeurs individuelles.</span><span class="sxs-lookup"><span data-stu-id="d2f00-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="d2f00-304">Hello fonctionnalité du processeur est préférable pour la combinaison de colonnes.</span><span class="sxs-lookup"><span data-stu-id="d2f00-304">hello PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="d2f00-305">Analyser des données non structurées telles que des pages web et des messages électroniques, ou des données semi-structurées telles que des fichiers XML/JSON.</span><span class="sxs-lookup"><span data-stu-id="d2f00-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="d2f00-306">Analyser des données dans un codage non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d2f00-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="d2f00-307">toodefine un extracteur de défini par l’utilisateur, ou URE, nous devons toocreate un `IExtractor` interface.</span><span class="sxs-lookup"><span data-stu-id="d2f00-307">toodefine a user-defined extractor, or UDE, we need toocreate an `IExtractor` interface.</span></span> <span data-ttu-id="d2f00-308">Toutes les entrées d’extracteur de toohello de paramètres, tels que les séparateurs de colonnes/lignes et le codage, doivent toobe défini dans le constructeur de hello de classe hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-308">All input parameters toohello extractor, such as column/row delimiters, and encoding, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="d2f00-309">Hello `IExtractor` interface doit également contenir une définition pour hello `IEnumerable<IRow>` remplacer comme suit :</span><span class="sxs-lookup"><span data-stu-id="d2f00-309">hello `IExtractor`  interface should also contain a definition for hello `IEnumerable<IRow>` override as follows:</span></span>

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

<span data-ttu-id="d2f00-310">Hello **SqlUserDefinedExtractor** attribut indique que le type de hello doit être inscrite en tant qu’un extracteur de défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-310">hello **SqlUserDefinedExtractor** attribute indicates that hello type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="d2f00-311">Cette classe ne peut pas être héritée.</span><span class="sxs-lookup"><span data-stu-id="d2f00-311">This class cannot be inherited.</span></span>

<span data-ttu-id="d2f00-312">SqlUserDefinedExtractor est un attribut facultatif pour la définition d’UDE.</span><span class="sxs-lookup"><span data-stu-id="d2f00-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="d2f00-313">Il utilisé toodefine AtomicFileProcessing propriété pour l’objet d’URE hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-313">It used toodefine AtomicFileProcessing property for hello UDE object.</span></span>

* <span data-ttu-id="d2f00-314">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="d2f00-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="d2f00-315">**true** = indique que cet extracteur requiert des fichiers d’entrée atomique (JSON, XML, ...)</span><span class="sxs-lookup"><span data-stu-id="d2f00-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="d2f00-316">**false** = indique que cet extracteur peut traiter des fichiers fractionnés/distribués (CSV, SEQ, ...)</span><span class="sxs-lookup"><span data-stu-id="d2f00-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="d2f00-317">principaux objets de programmabilité URE Hello sont **d’entrée** et **sortie**.</span><span class="sxs-lookup"><span data-stu-id="d2f00-317">hello main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="d2f00-318">objet d’entrée de Hello est utilisé tooenumerate des données d’entrée en tant que `IUnstructuredReader`.</span><span class="sxs-lookup"><span data-stu-id="d2f00-318">hello input object is used tooenumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="d2f00-319">objet de sortie Hello est tooset utilisé les données de sortie à la suite d’activité d’extracteur hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-319">hello output object is used tooset output data as a result of hello extractor activity.</span></span>

<span data-ttu-id="d2f00-320">les données d’entrée Hello sont accessible via `System.IO.Stream` et `System.IO.StreamReader`.</span><span class="sxs-lookup"><span data-stu-id="d2f00-320">hello input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="d2f00-321">Pour l’énumération des colonnes d’entrée, nous avons tout d’abord fractionner les flux d’entrée hello à l’aide d’un séparateur de lignes.</span><span class="sxs-lookup"><span data-stu-id="d2f00-321">For input columns enumeration, we first split hello input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="d2f00-322">Ensuite, nous fractionnons la ligne d’entrée en parties de colonne.</span><span class="sxs-lookup"><span data-stu-id="d2f00-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="d2f00-323">les données de sortie tooset, nous utilisons hello `output.Set` (méthode).</span><span class="sxs-lookup"><span data-stu-id="d2f00-323">tooset output data, we use hello `output.Set` method.</span></span>

<span data-ttu-id="d2f00-324">Il est important de toounderstand qui hello extracteur personnalisé génère uniquement des colonnes et les valeurs qui sont définies avec la sortie de hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-324">It's important toounderstand that hello custom extractor only outputs columns and values that are defined with hello output.</span></span> <span data-ttu-id="d2f00-325">Définissez l’appel de méthode.</span><span class="sxs-lookup"><span data-stu-id="d2f00-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="d2f00-326">Hello extracteur réel sont déclenchées en appelant `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="d2f00-326">hello actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="d2f00-327">Voici un exemple d’extracteur hello :</span><span class="sxs-lookup"><span data-stu-id="d2f00-327">Following is hello extractor example:</span></span>

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
         //Read hello input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split hello input by hello column delimiter
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
                 // for column “user”, convert tooUPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep hello rest of hello columns as-is
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

<span data-ttu-id="d2f00-328">Dans ce scénario de cas d’usage, extracteur de hello régénère hello GUID pour la colonne « guid » et convertit les valeurs hello du cas de tooupper de colonne « utilisateur ».</span><span class="sxs-lookup"><span data-stu-id="d2f00-328">In this use-case scenario, hello extractor regenerates hello GUID for “guid” column and converts hello values of “user” column tooupper case.</span></span> <span data-ttu-id="d2f00-329">Des extracteurs personnalisés peuvent produire des résultats plus complexes en analysant et manipulant des données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d2f00-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="d2f00-330">Le script U-SQL de base utilisant un extracteur personnalisé est le suivant :</span><span class="sxs-lookup"><span data-stu-id="d2f00-330">Following is base U-SQL script that uses a custom extractor:</span></span>

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

OUTPUT @rs0 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a><span data-ttu-id="d2f00-331">Utiliser des générateurs de sortie définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d2f00-331">Use user-defined outputters</span></span>
<span data-ttu-id="d2f00-332">Outputter de défini par l’utilisateur est un autre opérateur U-SQL qui vous permet de tooextend des fonctionnalités intégrées U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d2f00-332">User-defined outputter is another U-SQL UDO that allows you tooextend built-in U-SQL functionality.</span></span> <span data-ttu-id="d2f00-333">Extracteur de toohello similaires, il existe plusieurs outputters intégrés.</span><span class="sxs-lookup"><span data-stu-id="d2f00-333">Similar toohello extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="d2f00-334">*Outputters.Text()*: écrit les données toodelimited fichiers texte de codages différents.</span><span class="sxs-lookup"><span data-stu-id="d2f00-334">*Outputters.Text()*: Writes data toodelimited text files of different encodings.</span></span>
* <span data-ttu-id="d2f00-335">*Outputters.Csv()*: écrit les fichiers de (CSV) de différents encodages de valeurs séparées par des toocomma de données.</span><span class="sxs-lookup"><span data-stu-id="d2f00-335">*Outputters.Csv()*: Writes data toocomma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="d2f00-336">*Outputters.Tsv()*: écrit les fichiers de (TSV) de différents encodages de valeurs séparées par des tootab de données.</span><span class="sxs-lookup"><span data-stu-id="d2f00-336">*Outputters.Tsv()*: Writes data tootab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="d2f00-337">Outputter personnalisée vous permet de toowrite données dans un format défini personnalisé.</span><span class="sxs-lookup"><span data-stu-id="d2f00-337">Custom outputter allows you toowrite data in a custom defined format.</span></span> <span data-ttu-id="d2f00-338">Cela peut être utile pour hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="d2f00-338">This can be useful for hello following tasks:</span></span>

* <span data-ttu-id="d2f00-339">L’écriture de fichiers de données toosemi-structurées ou non structurées.</span><span class="sxs-lookup"><span data-stu-id="d2f00-339">Writing data toosemi-structured or unstructured files.</span></span>
* <span data-ttu-id="d2f00-340">Écrire des données dans des codages non pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d2f00-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="d2f00-341">Modifier des données de sortie ou ajouter des attributs personnalisés.</span><span class="sxs-lookup"><span data-stu-id="d2f00-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="d2f00-342">toodefine définie par l’utilisateur outputter, nous devons toocreate hello `IOutputter` interface.</span><span class="sxs-lookup"><span data-stu-id="d2f00-342">toodefine user-defined outputter, we need toocreate hello `IOutputter` interface.</span></span>

<span data-ttu-id="d2f00-343">Voici hello base `IOutputter` implémentation de la classe :</span><span class="sxs-lookup"><span data-stu-id="d2f00-343">Following is hello base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="d2f00-344">Toutes les entrées outputter toohello de paramètres, tels que les séparateurs de colonnes/lignes, le codage et ainsi de suite, doivent toobe défini dans le constructeur de hello de classe hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-344">All input parameters toohello outputter, such as column/row delimiters, encoding, and so on, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="d2f00-345">Hello `IOutputter` interface doit également contenir une définition pour `void Output` remplacer.</span><span class="sxs-lookup"><span data-stu-id="d2f00-345">hello `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="d2f00-346">attribut de Hello `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` peut être défini pour le traitement de fichier atomique.</span><span class="sxs-lookup"><span data-stu-id="d2f00-346">hello attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="d2f00-347">Pour plus d’informations, consultez hello les détails suivants.</span><span class="sxs-lookup"><span data-stu-id="d2f00-347">For more information, see hello following details.</span></span>

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

* <span data-ttu-id="d2f00-348">`Output` est appelé pour chaque ligne d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d2f00-348">`Output` is called for each input row.</span></span> <span data-ttu-id="d2f00-349">Il renvoie hello `IUnstructuredWriter output` ensemble de lignes.</span><span class="sxs-lookup"><span data-stu-id="d2f00-349">It returns hello `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="d2f00-350">Hello classe de constructeur est utilisé outputter définie par l’utilisateur de toopass paramètres toohello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-350">hello Constructor class is used toopass parameters toohello user-defined outputter.</span></span>
* <span data-ttu-id="d2f00-351">`Close`est utilisé toooptionally remplacer l’état de coûteuses toorelease ou déterminer lorsque la dernière ligne de hello a été écrit.</span><span class="sxs-lookup"><span data-stu-id="d2f00-351">`Close` is used toooptionally override toorelease expensive state or determine when hello last row was written.</span></span>

<span data-ttu-id="d2f00-352">**SqlUserDefinedOutputter** attribut indique que le type de hello doit être inscrite en tant qu’un outputter défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-352">**SqlUserDefinedOutputter** attribute indicates that hello type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="d2f00-353">Cette classe ne peut pas être héritée.</span><span class="sxs-lookup"><span data-stu-id="d2f00-353">This class cannot be inherited.</span></span>

<span data-ttu-id="d2f00-354">SqlUserDefinedOutputter est un attribut facultatif pour une définition d’un générateur de sortie défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="d2f00-355">Il a utilisé la propriété de AtomicFileProcessing toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-355">It's used toodefine hello AtomicFileProcessing property.</span></span>

* <span data-ttu-id="d2f00-356">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="d2f00-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="d2f00-357">**true** = indique que ce générateur de sortie requiert des fichiers de sortie atomique (JSON, XML, ...)</span><span class="sxs-lookup"><span data-stu-id="d2f00-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="d2f00-358">**false** = indique que ce générateur de sortie peut traiter des fichiers fractionnés/distribués (CSV, SEQ, ...)</span><span class="sxs-lookup"><span data-stu-id="d2f00-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="d2f00-359">objets de programmabilité principal Hello sont **ligne** et **sortie**.</span><span class="sxs-lookup"><span data-stu-id="d2f00-359">hello main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="d2f00-360">Hello **ligne** objet est utilisé tooenumerate les données de sortie en tant que `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="d2f00-360">hello **row** object is used tooenumerate output data as `IRow` interface.</span></span> <span data-ttu-id="d2f00-361">**Sortie** est le fichier cible toohello tooset utilisé sortie données.</span><span class="sxs-lookup"><span data-stu-id="d2f00-361">**Output** is used tooset output data toohello target file.</span></span>

<span data-ttu-id="d2f00-362">données de sortie Hello sont accessible via hello `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="d2f00-362">hello output data is accessed through hello `IRow` interface.</span></span> <span data-ttu-id="d2f00-363">Les données de sortie sont transmises une ligne à la fois.</span><span class="sxs-lookup"><span data-stu-id="d2f00-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="d2f00-364">les valeurs individuelles Hello sont énumérées en appelant la méthode Get hello interface IRow de hello :</span><span class="sxs-lookup"><span data-stu-id="d2f00-364">hello individual values are enumerated by calling hello Get method of hello IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="d2f00-365">Les noms des colonnes peuvent être déterminés en appelant `row.Schema` :</span><span class="sxs-lookup"><span data-stu-id="d2f00-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="d2f00-366">Cette approche vous permet de toobuild un outputter flexible pour n’importe quel schéma de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="d2f00-366">This approach enables you toobuild a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="d2f00-367">Hello données de sortie sont écrite toofile à l’aide de `System.IO.StreamWriter`.</span><span class="sxs-lookup"><span data-stu-id="d2f00-367">hello output data is written toofile by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="d2f00-368">paramètre de flux Hello est défini trop`output.BaseStrea` dans le cadre de `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="d2f00-368">hello stream parameter is set too`output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="d2f00-369">Notez qu’il est le fichier de toohello de la mémoire tampon de données important tooflush hello après chaque itération de la ligne.</span><span class="sxs-lookup"><span data-stu-id="d2f00-369">Note that it's important tooflush hello data buffer toohello file after each row iteration.</span></span> <span data-ttu-id="d2f00-370">En outre, hello `StreamWriter` objet doit être utilisé avec hello supprimable attribut activé (valeur par défaut) et hello **à l’aide de** (mot clé) :</span><span class="sxs-lookup"><span data-stu-id="d2f00-370">In addition, hello `StreamWriter` object must be used with hello Disposable attribute enabled (default) and with hello **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="d2f00-371">Autrement, appelez explicitement la méthode Flush() après chaque itération.</span><span class="sxs-lookup"><span data-stu-id="d2f00-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="d2f00-372">Nous illustrent ce Bonjour l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="d2f00-372">We show this in hello following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="d2f00-373">Définir des en-têtes et des pieds de page pour un générateur de sortie défini par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d2f00-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="d2f00-374">tooset un en-tête, utilisez le flux d’exécution unique d’itération.</span><span class="sxs-lookup"><span data-stu-id="d2f00-374">tooset a header, use single iteration execution flow.</span></span>

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

<span data-ttu-id="d2f00-375">Hello code Bonjour tout d’abord `if (isHeaderRow)` bloc est exécuté une seule fois.</span><span class="sxs-lookup"><span data-stu-id="d2f00-375">hello code in hello first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="d2f00-376">Pour le pied de page hello, utilisez l’instance de toohello de référence de hello de `System.IO.Stream` objet (`output.BaseStream`).</span><span class="sxs-lookup"><span data-stu-id="d2f00-376">For hello footer, use hello reference toohello instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="d2f00-377">Écrire un pied de page hello Bonjour méthode Close() Hello `IOutputter` interface.</span><span class="sxs-lookup"><span data-stu-id="d2f00-377">Write hello footer in hello Close() method of hello `IOutputter` interface.</span></span>  <span data-ttu-id="d2f00-378">(Pour plus d’informations, voir hello exemple suivant).</span><span class="sxs-lookup"><span data-stu-id="d2f00-378">(For more information, see hello following example.)</span></span>

<span data-ttu-id="d2f00-379">Voici un exemple d’un générateur de sortie défini par l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="d2f00-379">Following is an example of a user-defined outputter:</span></span>

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

    // hello Close method is used toowrite hello footer toohello file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference tooIO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization tooenumerate column names
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
        // Data type enumeration--required toomatch hello distinct list of types from OUTPUT statement
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
    // Reference toohello instance of hello IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define hello factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

<span data-ttu-id="d2f00-380">Et le script U-SQL de base :</span><span class="sxs-lookup"><span data-stu-id="d2f00-380">And U-SQL base script:</span></span>

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
    too@output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="d2f00-381">Il s’agit d’un générateur de sortie HTML qui crée un fichier HTML avec les données de la table.</span><span class="sxs-lookup"><span data-stu-id="d2f00-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="d2f00-382">Appeler un générateur de sortie à partir du script U-SQL de base</span><span class="sxs-lookup"><span data-stu-id="d2f00-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="d2f00-383">toocall un outputter personnalisé à partir du script U-SQL de la base hello, hello de nouvelle instance d’objet d’outputter hello a toobe créé.</span><span class="sxs-lookup"><span data-stu-id="d2f00-383">toocall a custom outputter from hello base U-SQL script, hello new instance of hello outputter object has toobe created.</span></span>

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="d2f00-384">tooavoid création d’une instance de hello objet de script de base, nous pouvons créer un wrapper de la fonction, comme indiqué dans l’exemple précédent :</span><span class="sxs-lookup"><span data-stu-id="d2f00-384">tooavoid creating an instance of hello object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

```c#
        // Define hello factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

<span data-ttu-id="d2f00-385">Dans ce cas, les appels d’origine hello ressemble à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="d2f00-385">In this case, hello original call looks like hello following:</span></span>

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="d2f00-386">Utiliser des processeurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d2f00-386">Use user-defined processors</span></span>
<span data-ttu-id="d2f00-387">Défini par l’utilisateur de processeur ou UDP, est un type d’opérateur U-SQL qui vous permet des lignes entrantes tooprocess hello en appliquant des fonctionnalités de programmabilité.</span><span class="sxs-lookup"><span data-stu-id="d2f00-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you tooprocess hello incoming rows by applying programmability features.</span></span> <span data-ttu-id="d2f00-388">UDP vous toocombine colonnes, modifiez les valeurs et ajouter de nouvelles colonnes si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d2f00-388">UDP enables you toocombine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="d2f00-389">En fait, il vous aide à tooprocess un ensemble de lignes tooproduce requis des éléments de données.</span><span class="sxs-lookup"><span data-stu-id="d2f00-389">Basically, it helps tooprocess a rowset tooproduce required data elements.</span></span>

<span data-ttu-id="d2f00-390">toodefine un UDP, nous devons toocreate un `IProcessor` interface avec hello `SqlUserDefinedProcessor` attribut, qui est facultatif pour le protocole UDP.</span><span class="sxs-lookup"><span data-stu-id="d2f00-390">toodefine a UDP, we need toocreate an `IProcessor` interface with hello `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="d2f00-391">Cette interface doit contenir la définition de hello pour hello `IRow` ensemble de lignes interface remplacer, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d2f00-391">This interface should contain hello definition for hello `IRow` interface rowset override, as shown in hello following example:</span></span>

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

<span data-ttu-id="d2f00-392">**SqlUserDefinedProcessor** indique que le type de hello doit être enregistré comme un processeur défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-392">**SqlUserDefinedProcessor** indicates that hello type should be registered as a user-defined processor.</span></span> <span data-ttu-id="d2f00-393">Cette classe ne peut pas être héritée.</span><span class="sxs-lookup"><span data-stu-id="d2f00-393">This class cannot be inherited.</span></span>

<span data-ttu-id="d2f00-394">l’attribut SqlUserDefinedProcessor Hello est **facultatif** pour la définition de UDP.</span><span class="sxs-lookup"><span data-stu-id="d2f00-394">hello SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="d2f00-395">objets de programmabilité principal Hello sont **d’entrée** et **sortie**.</span><span class="sxs-lookup"><span data-stu-id="d2f00-395">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="d2f00-396">objet d’entrée de Hello est utilisé tooenumerate des colonnes d’entrée et de sortie et de tooset les données de sortie à la suite de l’activité du processeur hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-396">hello input object is used tooenumerate input columns and output, and tooset output data as a result of hello processor activity.</span></span>

<span data-ttu-id="d2f00-397">Pour l’énumération des colonnes d’entrée, nous utilisons hello `input.Get` (méthode).</span><span class="sxs-lookup"><span data-stu-id="d2f00-397">For input columns enumeration, we use hello `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="d2f00-398">Hello paramètre `input.Get` méthode est une colonne qui est passée en tant que partie de hello `PRODUCE` clause Hello `PROCESS` instruction de script de base hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d2f00-398">hello parameter for `input.Get` method is a column that's passed as part of hello `PRODUCE` clause of hello `PROCESS` statement of hello U-SQL base script.</span></span> <span data-ttu-id="d2f00-399">Nous devons toouse ici de type de données correct de hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-399">We need toouse hello correct data type here.</span></span>

<span data-ttu-id="d2f00-400">Pour une sortie, utilisez hello `output.Set` (méthode).</span><span class="sxs-lookup"><span data-stu-id="d2f00-400">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="d2f00-401">Il est important toonote qu’un producteur personnalisé génère uniquement les colonnes et les valeurs qui sont définies avec hello `output.Set` appel de méthode.</span><span class="sxs-lookup"><span data-stu-id="d2f00-401">It's important toonote that custom producer only outputs columns and values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="d2f00-402">sortie du processeur réel Hello est déclenchée en appelant `return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="d2f00-402">hello actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="d2f00-403">Voici un exemple de processeur :</span><span class="sxs-lookup"><span data-stu-id="d2f00-403">Following is a processor example:</span></span>

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

<span data-ttu-id="d2f00-404">Dans ce scénario de cas d’usage, processeur de hello génère une nouvelle colonne nommée « full_description » en combinant hello les colonnes existantes--dans ce cas, « user » en majuscules et « des ».</span><span class="sxs-lookup"><span data-stu-id="d2f00-404">In this use-case scenario, hello processor is generating a new column called “full_description” by combining hello existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="d2f00-405">Aussi, il régénère un GUID et retourne hello d’origine et les nouvelles valeurs GUID.</span><span class="sxs-lookup"><span data-stu-id="d2f00-405">It also regenerates a GUID and returns hello original and new GUID values.</span></span>

<span data-ttu-id="d2f00-406">Comme vous pouvez le voir à partir de l’exemple précédent de hello, vous pouvez appeler les méthodes c# pendant `output.Set` appel de méthode.</span><span class="sxs-lookup"><span data-stu-id="d2f00-406">As you can see from hello previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="d2f00-407">Vous trouverez ci-dessous un exemple de script U-SQL de base utilisant un processeur personnalisé :</span><span class="sxs-lookup"><span data-stu-id="d2f00-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

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

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a><span data-ttu-id="d2f00-408">Utiliser des applicateurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d2f00-408">Use user-defined appliers</span></span>
<span data-ttu-id="d2f00-409">Un applicateur de U-SQL définie par l’utilisateur vous permet de fonction tooinvoke personnalisée c# pour chaque ligne retournée par l’expression de table externe hello d’une requête.</span><span class="sxs-lookup"><span data-stu-id="d2f00-409">A U-SQL user-defined applier enables you tooinvoke a custom C# function for each row that's returned by hello outer table expression of a query.</span></span> <span data-ttu-id="d2f00-410">entrée de droite Hello est évaluée pour chaque ligne à partir de l’entrée de gauche hello et lignes hello qui sont produites sont combinées pour la sortie finale hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-410">hello right input is evaluated for each row from hello left input, and hello rows that are produced are combined for hello final output.</span></span> <span data-ttu-id="d2f00-411">Hello liste de colonnes qui sont produites par l’opérateur APPLY de hello sont la combinaison hello du jeu hello de colonnes dans hello gauche et droit d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-411">hello list of columns that are produced by hello APPLY operator are hello combination of hello set of columns in hello left and hello right input.</span></span>

<span data-ttu-id="d2f00-412">Applicateur de défini par l’utilisateur est appelé dans le cadre de hello USQL sélectionnez une expression.</span><span class="sxs-lookup"><span data-stu-id="d2f00-412">User-defined applier is being invoked as part of hello USQL SELECT expression.</span></span>

<span data-ttu-id="d2f00-413">Hello appel typique toohello définie par l’utilisateur pour ressemble hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="d2f00-413">hello typical call toohello user-defined applier looks like hello following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="d2f00-414">Pour plus d’informations sur l’utilisation d’applicateurs dans une expression SELECT, voir [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx) (Sélection d’U-SQL SELECT à partir de CROSS APPLY et de OUTER APPLY).</span><span class="sxs-lookup"><span data-stu-id="d2f00-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="d2f00-415">définition Hello défini par l’utilisateur pour la classe de base est la suivante :</span><span class="sxs-lookup"><span data-stu-id="d2f00-415">hello user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="d2f00-416">toodefine un applicateur défini par l’utilisateur, nous devons toocreate hello `IApplier` interface avec hello [`SqlUserDefinedApplier`] attribut, qui est facultatif pour une définition pour défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-416">toodefine a user-defined applier, we need toocreate hello `IApplier` interface with hello [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

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

* <span data-ttu-id="d2f00-417">Appliquer est appelée pour chaque ligne de table externe de hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-417">Apply is called for each row of hello outer table.</span></span> <span data-ttu-id="d2f00-418">Il renvoie hello `IUpdatableRow` ensemble de lignes de sortie.</span><span class="sxs-lookup"><span data-stu-id="d2f00-418">It returns hello `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="d2f00-419">classe de constructeur Hello est utilisé toopass paramètres toohello définie par l’utilisateur APPLICATEUR.</span><span class="sxs-lookup"><span data-stu-id="d2f00-419">hello Constructor class is used toopass parameters toohello user-defined applier.</span></span>

<span data-ttu-id="d2f00-420">**SqlUserDefinedApplier** indique que le type de hello doit être inscrite en tant qu’un applicateur défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-420">**SqlUserDefinedApplier** indicates that hello type should be registered as a user-defined applier.</span></span> <span data-ttu-id="d2f00-421">Cette classe ne peut pas être héritée.</span><span class="sxs-lookup"><span data-stu-id="d2f00-421">This class cannot be inherited.</span></span>

<span data-ttu-id="d2f00-422">**SqlUserDefinedApplier** est **facultatif** pour une définition d’applicateur défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="d2f00-423">objets de programmabilité principal Hello sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="d2f00-423">hello main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="d2f00-424">Les ensembles de lignes d’entrée sont transmis en tant qu’entrée `IRow`.</span><span class="sxs-lookup"><span data-stu-id="d2f00-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="d2f00-425">Hello lignes de sortie sont générées en tant que `IUpdatableRow` interface de sortie.</span><span class="sxs-lookup"><span data-stu-id="d2f00-425">hello output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="d2f00-426">Un nom de colonne peut être déterminé en appelant hello `IRow` méthode du schéma.</span><span class="sxs-lookup"><span data-stu-id="d2f00-426">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="d2f00-427">valeurs de données réelles hello tooget de hello entrant `IRow`, nous utilisons la méthode hello Get() `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="d2f00-427">tooget hello actual data values from hello incoming `IRow`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="d2f00-428">Ou bien, nous utilisons le nom de colonne de schéma hello :</span><span class="sxs-lookup"><span data-stu-id="d2f00-428">Or we use hello schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="d2f00-429">Hello valeurs de sortie doivent être définies avec `IUpdatableRow` sortie :</span><span class="sxs-lookup"><span data-stu-id="d2f00-429">hello output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="d2f00-430">Il est important toounderstand qui appliers personnalisés sortie uniquement les colonnes et les valeurs qui sont définies avec `output.Set` appel de méthode.</span><span class="sxs-lookup"><span data-stu-id="d2f00-430">It is important toounderstand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="d2f00-431">le résultat réel Hello est déclenché en appelant `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="d2f00-431">hello actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="d2f00-432">Hello défini par l’utilisateur des paramètres pour peuvent être passés toohello constructeur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-432">hello user-defined applier parameters can be passed toohello constructor.</span></span> <span data-ttu-id="d2f00-433">APPLICATEUR peut retourner un nombre variable de colonnes qui doivent toobe défini pendant l’appel pour hello base Script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d2f00-433">Applier can return a variable number of columns that need toobe defined during hello applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="d2f00-434">Voici hello défini par l’utilisateur pour exemple :</span><span class="sxs-lookup"><span data-stu-id="d2f00-434">Here is hello user-defined applier example:</span></span>

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

<span data-ttu-id="d2f00-435">Voici hello base U-script SQL pour cette APPLICATEUR défini par l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="d2f00-435">Following is hello base U-SQL script for this user-defined applier:</span></span>

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

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

<span data-ttu-id="d2f00-436">Dans ce scénario d’utilisation, définis par l’utilisateur pour joue un analyseur délimitée par des virgules de valeur pour les propriétés de flotte hello voiture.</span><span class="sxs-lookup"><span data-stu-id="d2f00-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for hello car fleet properties.</span></span> <span data-ttu-id="d2f00-437">lignes du fichier d’entrée Hello ressemble à hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="d2f00-437">hello input file rows look like hello following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="d2f00-438">Il s’agit d’un fichier TSV standard de valeurs délimitées par des tabulations avec une colonne Propriétés contenant des propriétés de voitures telles que la marque et le modèle.</span><span class="sxs-lookup"><span data-stu-id="d2f00-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="d2f00-439">Ces propriétés doivent être des colonnes de table toohello analysé.</span><span class="sxs-lookup"><span data-stu-id="d2f00-439">Those properties must be parsed toohello table columns.</span></span> <span data-ttu-id="d2f00-440">Applicateur de Hello fourni vous permet également de toogenerate dynamique plusieurs propriétés Bonjour entraîner ensemble de lignes, selon le paramètre hello qui est passé.</span><span class="sxs-lookup"><span data-stu-id="d2f00-440">hello applier that's provided also enables you toogenerate a dynamic number of properties in hello result rowset, based on hello parameter that's passed.</span></span> <span data-ttu-id="d2f00-441">Vous pouvez générer soit toutes les propriétés, soit un ensemble spécifique de propriétés.</span><span class="sxs-lookup"><span data-stu-id="d2f00-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="d2f00-442">Applicateur de Hello défini par l’utilisateur peut être appelé comme une nouvelle instance de l’objet pour :</span><span class="sxs-lookup"><span data-stu-id="d2f00-442">hello user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="d2f00-443">Ou avec une méthode de fabrique wrapper appel hello :</span><span class="sxs-lookup"><span data-stu-id="d2f00-443">Or with hello invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="d2f00-444">Utiliser des combinateurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d2f00-444">Use user-defined combiners</span></span>
<span data-ttu-id="d2f00-445">Défini par l’utilisateur un combinateur ou UDC, vous permet de toocombine les lignes à partir d’ensembles de lignes gauche et droit, selon une logique personnalisée.</span><span class="sxs-lookup"><span data-stu-id="d2f00-445">User-defined combiner, or UDC, enables you toocombine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="d2f00-446">Un combinateur défini par l’utilisateur est utilisé avec l’expression COMBINE.</span><span class="sxs-lookup"><span data-stu-id="d2f00-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="d2f00-447">Une association est appelée avec expression combiner hello hello les informations requises sur les deux ensembles de lignes d’entrée hello, hello regroupement des colonnes, hello attendu schéma de résultats et des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="d2f00-447">A combiner is being invoked with hello COMBINE expression that provides hello necessary information about both hello input rowsets, hello grouping columns, hello expected result schema, and additional information.</span></span>

<span data-ttu-id="d2f00-448">toocall un combinateur dans un script U-SQL de base, nous utilisons hello selon la syntaxe :</span><span class="sxs-lookup"><span data-stu-id="d2f00-448">toocall a combiner in a base U-SQL script, we use hello following syntax:</span></span>

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

<span data-ttu-id="d2f00-449">Pour plus d’informations, voir [Expression COMBINE (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span><span class="sxs-lookup"><span data-stu-id="d2f00-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="d2f00-450">toodefine un combinateur défini par l’utilisateur, nous devons toocreate hello `ICombiner` interface avec hello [`SqlUserDefinedCombiner`] attribut, qui est facultatif pour une définition COMBINATEUR défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-450">toodefine a user-defined combiner, we need toocreate hello `ICombiner` interface with hello [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="d2f00-451">Définition de classe `ICombiner` de base :</span><span class="sxs-lookup"><span data-stu-id="d2f00-451">Base `ICombiner` class definition:</span></span>

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

<span data-ttu-id="d2f00-452">Hello implémentation personnalisée d’un `ICombiner` interface doit contenir la définition de hello pour une `IEnumerable<IRow>` combiner de remplacement.</span><span class="sxs-lookup"><span data-stu-id="d2f00-452">hello custom implementation of an `ICombiner` interface should contain hello definition for an `IEnumerable<IRow>` Combine override.</span></span>

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

<span data-ttu-id="d2f00-453">Hello **SqlUserDefinedCombiner** attribut indique que le type de hello doit être inscrite en tant qu’un combinateur défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-453">hello **SqlUserDefinedCombiner** attribute indicates that hello type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="d2f00-454">Cette classe ne peut pas être héritée.</span><span class="sxs-lookup"><span data-stu-id="d2f00-454">This class cannot be inherited.</span></span>

<span data-ttu-id="d2f00-455">**SqlUserDefinedCombiner** est la propriété du mode utilisé toodefine hello COMBINATEUR.</span><span class="sxs-lookup"><span data-stu-id="d2f00-455">**SqlUserDefinedCombiner** is used toodefine hello Combiner mode property.</span></span> <span data-ttu-id="d2f00-456">C’est un attribut facultatif pour une définition de combinateur défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="d2f00-457">CombinerMode     Mode</span><span class="sxs-lookup"><span data-stu-id="d2f00-457">CombinerMode     Mode</span></span>

<span data-ttu-id="d2f00-458">CombinerMode enum peut prendre hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="d2f00-458">CombinerMode enum can take hello following values:</span></span>

* <span data-ttu-id="d2f00-459">Complète (0) pour de que chaque ligne de sortie dépend potentiellement toutes les lignes d’entrée hello gauche et droite avec hello même valeur de clé.</span><span class="sxs-lookup"><span data-stu-id="d2f00-459">Full  (0) Every output row potentially depends on all hello input rows from left and right       with hello same key value.</span></span>

* <span data-ttu-id="d2f00-460">Gauche (1), chaque ligne de sortie dépend d’une seule ligne d’entrée de hello gauche (et potentiellement toutes les lignes de hello droite avec hello même valeur de clé).</span><span class="sxs-lookup"><span data-stu-id="d2f00-460">Left  (1) Every output row depends on a single input row from hello left (and potentially all rows       from hello right with hello same key value).</span></span>

* <span data-ttu-id="d2f00-461">Droite (2), chaque ligne de sortie dépend d’une ligne d’entrée de hello droit (et potentiellement toutes les lignes de gauche hello avec hello même valeur de clé).</span><span class="sxs-lookup"><span data-stu-id="d2f00-461">Right (2)     Every output row depends on a single input row from hello right (and potentially all rows       from hello left with hello same key value).</span></span>

* <span data-ttu-id="d2f00-462">Interne (3), chaque ligne de sortie dépend d’une seule entrée de ligne à partir de la gauche et droite avec hello même valeur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-462">Inner (3) Every output row depends on a single input row from left and right with hello same value.</span></span>

<span data-ttu-id="d2f00-463">Exemple :    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="d2f00-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="d2f00-464">objets de programmabilité principal Hello sont :</span><span class="sxs-lookup"><span data-stu-id="d2f00-464">hello main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="d2f00-465">Les ensembles de lignes d’entrée sont transmis en tant que type d’interface **gauche** et **droit** `IRowset`.</span><span class="sxs-lookup"><span data-stu-id="d2f00-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="d2f00-466">Les deux ensembles de lignes doivent être énumérés pour le traitement.</span><span class="sxs-lookup"><span data-stu-id="d2f00-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="d2f00-467">Vous pouvez uniquement énumérer chaque interface une seule fois, nous avons ont tooenumerate et mettre en cache si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d2f00-467">You can only enumerate each interface once, so we have tooenumerate and cache it if necessary.</span></span>

<span data-ttu-id="d2f00-468">Pour la mise en cache, nous pouvons créer un type List\<T\> de structure de mémoire résultant de l’exécution d’une requête LINQ, plus particulièrement List<`IRow`>.</span><span class="sxs-lookup"><span data-stu-id="d2f00-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="d2f00-469">type de données anonymes de Hello peut être utilisé lors de l’énumération également.</span><span class="sxs-lookup"><span data-stu-id="d2f00-469">hello anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="d2f00-470">Consultez [Introduction tooLINQ requêtes (c#)](https://msdn.microsoft.com/library/bb397906.aspx) pour plus d’informations sur les requêtes LINQ, et [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) pour plus d’informations sur IEnumerable\<T\> interface.</span><span class="sxs-lookup"><span data-stu-id="d2f00-470">See [Introduction tooLINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="d2f00-471">valeurs de données réelles hello tooget de hello entrant `IRowset`, nous utilisons la méthode hello Get() `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="d2f00-471">tooget hello actual data values from hello incoming `IRowset`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="d2f00-472">Un nom de colonne peut être déterminé en appelant hello `IRow` méthode du schéma.</span><span class="sxs-lookup"><span data-stu-id="d2f00-472">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="d2f00-473">Ou à l’aide du nom de colonne de schéma hello :</span><span class="sxs-lookup"><span data-stu-id="d2f00-473">Or by using hello schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="d2f00-474">énumération de général Hello avec LINQ ressemble à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="d2f00-474">hello general enumeration with LINQ looks like hello following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="d2f00-475">Après l’énumération des deux ensembles de lignes, nous allons tooloop dans toutes les lignes.</span><span class="sxs-lookup"><span data-stu-id="d2f00-475">After enumerating both rowsets, we are going tooloop through all rows.</span></span> <span data-ttu-id="d2f00-476">Pour chaque ligne dans l’ensemble de lignes gauche hello, nous allons toofind toutes les lignes qui satisfont la condition hello de notre association.</span><span class="sxs-lookup"><span data-stu-id="d2f00-476">For each row in hello left rowset, we are going toofind all rows that satisfy hello condition of our combiner.</span></span>

<span data-ttu-id="d2f00-477">Hello valeurs de sortie doivent être définies avec `IUpdatableRow` sortie.</span><span class="sxs-lookup"><span data-stu-id="d2f00-477">hello output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="d2f00-478">le résultat réel Hello est déclenché en appelant trop`yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="d2f00-478">hello actual output is triggered by calling too`yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="d2f00-479">Voici un exemple de combinateur :</span><span class="sxs-lookup"><span data-stu-id="d2f00-479">Following is a combiner example:</span></span>

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

<span data-ttu-id="d2f00-480">Dans ce scénario de cas d’utilisation, nous allons créer un rapport analytique pour le site de vente hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-480">In this use-case scenario, we are building an analytics report for hello retailer.</span></span> <span data-ttu-id="d2f00-481">Hello vise toofind tous les produits dont le prix est supérieur à 20 000 $ et que vendent sur le site Web de hello plus rapidement qu’avec le site de vente régulière hello dans un intervalle de temps donné.</span><span class="sxs-lookup"><span data-stu-id="d2f00-481">hello goal is toofind all products that cost more than $20,000 and that sell through hello website faster than through hello regular retailer within a certain time frame.</span></span>

<span data-ttu-id="d2f00-482">Voici le script U-SQL de la base hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-482">Here is hello base U-SQL script.</span></span> <span data-ttu-id="d2f00-483">Vous pouvez comparer la logique de hello entre une jointure normale et une association :</span><span class="sxs-lookup"><span data-stu-id="d2f00-483">You can compare hello logic between a regular JOIN and a combiner:</span></span>

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

OUTPUT @rs1 too@output_file1 USING Outputters.Tsv();
OUTPUT @rs2 too@output_file2 USING Outputters.Tsv();
```

<span data-ttu-id="d2f00-484">Un combinateur défini par l’utilisateur peut être appelé comme une nouvelle instance de l’objet de hello pour :</span><span class="sxs-lookup"><span data-stu-id="d2f00-484">A user-defined combiner can be called as a new instance of hello applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="d2f00-485">Ou avec une méthode de fabrique wrapper appel hello :</span><span class="sxs-lookup"><span data-stu-id="d2f00-485">Or with hello invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="d2f00-486">Utiliser des réducteurs définis par l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="d2f00-486">Use user-defined reducers</span></span>

<span data-ttu-id="d2f00-487">U-SQL vous permet de REDUCTEURS d’ensemble de lignes personnalisée toowrite en c# à l’aide d’infrastructure d’extensibilité hello opérateur défini par l’utilisateur et l’implémentation d’une interface IReducer.</span><span class="sxs-lookup"><span data-stu-id="d2f00-487">U-SQL enables you toowrite custom rowset reducers in C# by using hello user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="d2f00-488">Réducteur de défini par l’utilisateur ou UDR, peut être des lignes inutiles tooeliminate utilisé lors de l’extraction de données (importation).</span><span class="sxs-lookup"><span data-stu-id="d2f00-488">User-defined reducer, or UDR, can be used tooeliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="d2f00-489">Il peut être toomanipulate utilisé et évaluer les lignes et colonnes.</span><span class="sxs-lookup"><span data-stu-id="d2f00-489">It also can be used toomanipulate and evaluate rows and columns.</span></span> <span data-ttu-id="d2f00-490">Selon la logique de programmabilité, elle peut également définir les lignes doivent toobe extraite.</span><span class="sxs-lookup"><span data-stu-id="d2f00-490">Based on programmability logic, it can also define which rows need toobe extracted.</span></span>

<span data-ttu-id="d2f00-491">toodefine une classe UDR, nous devons toocreate un `IReducer` interface facultative `SqlUserDefinedReducer` attribut.</span><span class="sxs-lookup"><span data-stu-id="d2f00-491">toodefine a UDR class, we need toocreate an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="d2f00-492">Cette interface de classe doit contenir une définition pour hello `IEnumerable` remplacer des lignes de l’interface.</span><span class="sxs-lookup"><span data-stu-id="d2f00-492">This class interface should contain a definition for hello `IEnumerable` interface rowset override.</span></span>

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

<span data-ttu-id="d2f00-493">Hello **SqlUserDefinedReducer** attribut indique que le type de hello doit être inscrite en tant qu’un réducteur défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-493">hello **SqlUserDefinedReducer** attribute indicates that hello type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="d2f00-494">Cette classe ne peut pas être héritée.</span><span class="sxs-lookup"><span data-stu-id="d2f00-494">This class cannot be inherited.</span></span>
<span data-ttu-id="d2f00-495">**SqlUserDefinedReducer** est un attribut facultatif pour une définition de réducteur défini par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="d2f00-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="d2f00-496">Il a utilisé toodefine IsRecursive propriété.</span><span class="sxs-lookup"><span data-stu-id="d2f00-496">It's used toodefine IsRecursive property.</span></span>

* <span data-ttu-id="d2f00-497">bool     IsRecursive</span><span class="sxs-lookup"><span data-stu-id="d2f00-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="d2f00-498">**true**  = indique si cette réduction est idempotente</span><span class="sxs-lookup"><span data-stu-id="d2f00-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="d2f00-499">objets de programmabilité principal Hello sont **d’entrée** et **sortie**.</span><span class="sxs-lookup"><span data-stu-id="d2f00-499">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="d2f00-500">objet d’entrée de Hello est utilisé tooenumerate les lignes d’entrée.</span><span class="sxs-lookup"><span data-stu-id="d2f00-500">hello input object is used tooenumerate input rows.</span></span> <span data-ttu-id="d2f00-501">La sortie est utilisé tooset les lignes de sortie suite à la réduction de l’activité.</span><span class="sxs-lookup"><span data-stu-id="d2f00-501">Output is used tooset output rows as a result of reducing activity.</span></span>

<span data-ttu-id="d2f00-502">Pour l’énumération des lignes d’entrée, nous utilisons hello `Row.Get` (méthode).</span><span class="sxs-lookup"><span data-stu-id="d2f00-502">For input rows enumeration, we use hello `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="d2f00-503">Hello paramètre hello `Row.Get` méthode est une colonne qui est passée en tant que partie de hello `PRODUCE` classe Hello `REDUCE` instruction de script de base hello U-SQL.</span><span class="sxs-lookup"><span data-stu-id="d2f00-503">hello parameter for hello `Row.Get` method is a column that's passed as part of hello `PRODUCE` class of hello `REDUCE` statement of hello U-SQL base script.</span></span> <span data-ttu-id="d2f00-504">Nous devons toouse hello type de données correct ici également.</span><span class="sxs-lookup"><span data-stu-id="d2f00-504">We need toouse hello correct data type here as well.</span></span>

<span data-ttu-id="d2f00-505">Pour une sortie, utilisez hello `output.Set` (méthode).</span><span class="sxs-lookup"><span data-stu-id="d2f00-505">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="d2f00-506">Il est important toounderstand qui réducteur personnalisé uniquement sorties des valeurs qui sont définies avec hello `output.Set` appel de méthode.</span><span class="sxs-lookup"><span data-stu-id="d2f00-506">It is important toounderstand that custom reducer only outputs values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="d2f00-507">Hello réducteur réel sont déclenchées en appelant `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="d2f00-507">hello actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="d2f00-508">Voici un exemple de réducteur :</span><span class="sxs-lookup"><span data-stu-id="d2f00-508">Following is a reducer example:</span></span>

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

<span data-ttu-id="d2f00-509">Dans ce scénario de cas d’usage, réducteur de hello ignore les lignes avec un nom d’utilisateur vide.</span><span class="sxs-lookup"><span data-stu-id="d2f00-509">In this use-case scenario, hello reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="d2f00-510">Pour chaque ligne dans l’ensemble de lignes, il lit chaque colonne requise, puis évalue la longueur du nom d’utilisateur hello hello.</span><span class="sxs-lookup"><span data-stu-id="d2f00-510">For each row in rowset, it reads each required column, then evaluates hello length of hello user name.</span></span> <span data-ttu-id="d2f00-511">Il génère une ligne hello uniquement si la longueur de nom des utilisateurs à l’aide de la valeur est supérieure à 0.</span><span class="sxs-lookup"><span data-stu-id="d2f00-511">It outputs hello actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="d2f00-512">Le script U-SQL de base utilisant un réducteur personnalisé est le suivant :</span><span class="sxs-lookup"><span data-stu-id="d2f00-512">Following is base U-SQL script that uses a custom reducer:</span></span>

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
    too@output_file 
    USING Outputters.Text();
```
