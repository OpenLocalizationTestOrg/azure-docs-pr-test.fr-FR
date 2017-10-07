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
# <a name="u-sql-programmability-guide"></a>Guide de programmabilité U-SQL

U-SQL est un langage de requête spécifiquement conçu pour les charges de travail de type Big Data. Une des fonctionnalités uniques de hello U-SQL est la combinaison de hello de langage déclaratif de type SQL hello extensibilité de hello et de programmabilité fournies par c#. Dans ce guide, nous concentrer sur l’extensibilité de hello et de programmabilité de langue U-SQL hello prenant en charge par c#.

## <a name="requirements"></a>Configuration requise

Téléchargez et installez [Azure Data Lake Tools pour Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

## <a name="get-started-with-u-sql"></a>Bien démarrer avec U-SQL  

Examinons hello script U-SQL suivant :

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

Il définit un ensemble de lignes appelé @a et crée un ensemble de lignes appelé @results de @a.

## <a name="c-types-and-expressions-in-u-sql-script"></a>Types et expressions C# dans les scripts U-SQL

Une Expression U-SQL est une expression C# combinée à des opérations logiques U-SQL comme `AND`, `OR` et `NOT`. Les expressions U-SQL peuvent être utilisées avec SELECT, EXTRACT, WHERE, HAVING, GROUP BY et DECLARE.

Par exemple, hello script suivant analyse une chaîne représentant une valeur DateTime dans la clause SELECT de hello.

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

Hello script suivant analyse une chaîne représentant une valeur de date/heure dans une instruction DECLARE.

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a>Utiliser des expressions C# pour les conversions de types de données
Bonjour à l’exemple suivant montre comment vous pouvez faire une conversion de données datetime à l’aide d’expressions c#. Dans ce scénario particulier, les données de type datetime de chaîne sont de type datetime toostandard converti notation de l’heure 00:00:00 minuit.

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a>Utiliser des expressions C# pour la date du jour
toopull date d’aujourd'hui, nous pouvons utiliser hello expression c# suivante :

```
DateTime.Now.ToString("M/d/yyyy")
```

Voici un exemple de procédure toouse cette expression dans un script :

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



## <a name="using-net-assemblies"></a>Avec des assemblys .NET
Modèle d’extensibilité de U-SQL s’appuie sur un code personnalisé hello capacité tooadd. Actuellement, U-SQL vous fournit des méthodes faciles tooadd votre propre Microsoft. Code de basée sur le réseau (en particulier, C#). Toutefois, vous pouvez également ajouter du code personnalisé écrit dans d’autres langages .NET, tels que VB.NET ou F #. 

### <a name="register-a-net-assembly"></a>Enregistrer un assembly .NET

Utilisez hello CREATE ASSEMBLY instruction tooplace un assembly .NET dans une base de données U-SQL. Une fois un assembly dans une base de données, scripts U-SQL peuvent utiliser ces assemblys à l’aide d’instruction d’ASSEMBLY de référence hello. 

Hello suivant de code montre comment tooregister un assembly :

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

Hello suivant de code montre comment tooreference un assembly :

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

Consultez hello [instructions d’inscription d’assembly](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) qui traite ce sujet plus en détail.


### <a name="use-assembly-versioning"></a>Utilisez le contrôle de version des assemblys
Actuellement, U-SQL utilise hello .NET Framework version 4.5. Par conséquent, assurez-vous que vos propres assemblys sont compatibles avec cette version de runtime de hello.

Comme mentionné précédemment, U-SQL exécute le code dans un format 64 bits (x64). Par conséquent, assurez-vous que votre code est compilé toorun sur x64. Dans le cas contraire, vous obtenez erreur de format incorrect de hello présentée précédemment.

Chaque DLL d’assembly ou fichier de ressources chargé, comme un runtime différent, un assembly natif ou un fichier de configuration peut être de 400 Mo maximum. taille totale de Hello de ressources déployées, via le déploiement de ressources ou tooassemblies de références et de leurs fichiers supplémentaires, ne peut pas dépasser 3 Go.

Enfin, notez que chaque base de données U-SQL ne peut contenir qu’une seule version d’un assembly donné. Par exemple, si vous devez les versions 7 et 8 de hello NewtonSoft Json.Net bibliothèque, vous devez tooregister dans deux bases de données. En outre, chaque script peut uniquement faire référence version tooone d’une DLL d’assembly donné. À cet égard, U-SQL suit hello c# assembly gestion et le contrôle de version sémantique.


## <a name="use-user-defined-functions-udf"></a>Utiliser les fonctions définies par l’utilisateur : UDF
Fonctions U-SQL définies par l’utilisateur ou UDF, programmez des routines qui acceptent des paramètres, effectuer une action (par exemple, un calcul complexe) et retournent le résultat de hello de cette action en tant que valeur. Hello retournent la valeur de UDF ne peut être une valeur scalaire unique. Une fonction définie par l’utilisateur U-SQL peut être appelée dans un script U-SQL de base comme toute autre fonction scalaire C#.

Nous vous recommandons d’initialiser les fonctions définies par l’utilisateur U-SQL en tant que **publiques** et **statiques**.

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

Première Examinons hello un exemple simple de création d’un fichier UDF.

Dans ce scénario de cas d’utilisation, nous devons toodetermine hello période, y compris le trimestre fiscal de hello et mois fiscal de hello première connexion d’utilisateur spécifique de hello. Hello premier mois fiscal de l’année hello dans notre scénario est juin.

exercice toocalculate, nous introduisons hello suivant fonction c# :

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

La fonction calcule simplement le trimestre et le mois fiscaux, puis retourne une valeur de chaîne. De juin, hello premier mois de hello premier trimestre fiscal, nous utilisons « Q1:P1 ». Pour le mois de juillet, nous utilisons « Q1:P2 », etc.

Il s’agit d’une fonction c# régulière que nous sommes continu toouse dans notre projet U-SQL.

Voici l’aspect de la section de code-behind hello dans ce scénario :

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

Nous allons maintenant toocall cette fonction à partir du script U-SQL de la base hello. toodo, nous avons tooprovide un nom qualifié complet pour la fonction hello, y compris hello, espace de noms, qui est dans ce cas NameSpace.Class.Function(parameter).

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

Voici hello base script U-SQL réel :

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

Voici le fichier de sortie hello hello d’exécution du script :

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

Cet exemple illustre une utilisation simple d’une fonction définie par l’utilisateur inline dans U-SQL.

### <a name="keep-state-between-udf-invocations"></a>Conserver l’état entre des appels de fonction définie par l’utilisateur
Les objets de programmabilité c# U-SQL peuvent être plus sophistiquées, utilisant l’interactivité des variables globales du code-behind hello. Examinons hello suivant le scénario d’entreprise en cas d’utilisation.

Dans les grandes organisations, les utilisateurs peuvent basculer entre divers types d’applications internes. Celles-ci peuvent inclure Microsoft Dynamics CRM, Power BI, etc. Clients pourriez tooapply une analyse de télémétrie de la façon dont les utilisateurs basculent entre différentes applications, des tendances de consommation hello sont et ainsi de suite. objectif de Hello pour les entreprises hello est toooptimize l’utilisation des applications. Ils peuvent également toocombine différentes applications ou des routines d’authentification spécifiques.

tooachieve cet objectif, nous avons toodetermine ID de session et de retard entre hello dernière session s’est produite.

Nous devez toofind une connexion à précédente, puis d’affecter cette connexion tooall les sessions qui sont en cours toohello généré même application. premier test de Hello est que script de base U-SQL n’autorise pas nous tooapply des calculs sur les colonnes calculées déjà avec la fonction LAG. Hello deuxième défi est que nous avons session spécifique de tookeep hello pour toutes les sessions dans hello même période.

toosolve ce problème, nous utilisons une variable globale à l’intérieur d’une section de code-behind : `static public string globalSession;`.

Cette variable globale est ensemble de lignes entier toohello appliquée pendant l’exécution du script.

Voici la section de code-behind hello de notre programme U-SQL :

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

Cet exemple affiche hello variable globale `static public string globalSession;` utilisé à l’intérieur de hello `getStampUserSession` fonction et l’obtention de réinitialisation chaque hello temps Session paramètre est modifié.

Hello U-SQL script de base est la suivante :

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

Fonction `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` est appelée ici lors du calcul de hello deuxième mémoire ensemble de lignes. Il passe hello `UserSessionTimestamp` colonne et renvoie hello valeur jusqu'à ce que `UserSessionTimestamp` a changé.

fichier de sortie Hello est comme suit :

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

Cet exemple illustre un scénario de cas d’usage plus complexe dans lequel nous utilisons une variable globale à l’intérieur d’une section de code-behind qui est l’ensemble de lignes de mémoire complète toohello appliqué.

## <a name="use-user-defined-types-udt"></a>Utiliser des types définis par l’utilisateur (UDT)
Les types définis par l’utilisateur (ou UDT) sont une autre fonctionnalité de programmabilité de U-SQL. Un type défini par l’utilisateur U-SQL agit comme un type défini par l’utilisateur C# standard. C# est un langage fortement typé qui autorise l’utilisation de hello de types intégrés et personnalisés définis par l’utilisateur.

U-SQL ne peut pas implicitement sérialiser ou désérialiser l’UDT arbitraires est hello UDT est passé entre les sommets dans les ensembles de lignes. Cela signifie que l’utilisateur hello tooprovide un formateur explicite à l’aide hello IFormatter interface. Cela fournit U-SQL hello sérialiser et désérialiser des méthodes pour hello UDT.

> [!NOTE]
> U-SQL extracteurs intégrés et outputters actuellement ne peut pas sérialiser ou désérialiser tooor de données UDT à partir de fichiers, même avec hello IFormatter ensemble. Par conséquent, lorsque vous écrivez un fichier de tooa de données UDT avec hello instruction OUTPUT ou lire avec un extracteur de, vous avez toopass sous la forme d’un chaîne ou tableau d’octets. Puis vous appelez sérialisation de hello et de désérialisation explicitement de code (autrement dit, la méthode ToString() hello par l’utilisateur). Extracteurs de défini par l’utilisateur et outputters, sur hello autres main, peuvent lire et écrire les UDT.

Si nous essayons toouse UDT dans extracteur ou OUTPUTTER (hors SELECT précédente), comme indiqué ici :

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

Nous recevons hello l’erreur suivante :

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

toowork avec UDT dans outputter, nous avons soit tooserialize il toostring avec hello méthode ToString() ou créer un outputter personnalisé.

Il n’est actuellement pas possible d’utiliser des types définis par l’utilisateur dans une instruction GROUP BY. Si l’UDT est utilisé dans GROUP BY, hello l’erreur suivante est levée :

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

toodefine un UDT, il faut :

* Ajoutez hello suivant des espaces de noms :

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* Ajouter `Microsoft.Analytics.Interfaces`, ce qui est nécessaire pour les interfaces d’UDT hello. En outre, `System.IO` toodefine nécessaires hello IFormatter interface peut se.

* Définir un type défini par l’utilisateur avec l’attribut SqlUserDefinedType.

**SqlUserDefinedType** est toomark utilisé une définition de type dans un assembly comme étant un type défini par l’utilisateur (UDT) dans U-SQL. propriétés de Hello sur l’attribut de hello reflètent les caractéristiques physiques de hello Hello UDT. Cette classe ne peut pas être héritée.

SqlUserDefinedType est un attribut obligatoire pour la définition du type défini par l’utilisateur.

constructeur Hello de classe hello :  

* SqlUserDefinedTypeAttribute (formateur de type)

* Formateur de type : requis du paramètre toodefine du module de formatage de l’UDT--plus précisément, le type de hello Hello `IFormatter` interface doit être passé ici.

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* UDT classique requiert également la définition d’interface de IFormatter hello, comme indiqué dans hello l’exemple suivant :

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

Hello `IFormatter` interface sérialise et désérialise un graphique d’objet avec le type de racine hello \<typeparamref nom = « T » >.

\<typeparam nom = « T » > Bonjour type racine pour tooserialize de graphique d’objet hello et désérialiser.

* **Désérialiser**: données hello sur les flux hello fourni est désérialisée et reconstitue graphique hello d’objets.

* **Sérialiser**: sérialise un objet ou un graphique d’objets, avec hello racine toohello fourni flux donné.

`MyType`instance : Instance de type de hello.  
`IColumnWriter`enregistreur / `IColumnReader` lecteur : hello sous-jacent de flux de données de colonne.  
`ISerializationContext`contexte : énumération qui définit un ensemble d’indicateurs qui spécifie le contexte de source ou destination hello pour les flux hello pendant la sérialisation.

* **Intermédiaire**: Spécifie que contexte source ou la destination de hello n’est pas un magasin persistant.

* **Persistance**: Spécifie que contexte source ou la destination de hello est un magasin persistant.

En tant que type C# standard, une définition de type défini par l’utilisateur U-SQL peut inclure des remplacements pour des opérateurs tels que +/==/!=. Elle peut également inclure des méthodes statiques. Par exemple, si nous devons toouse cet UDT comme une fonction d’agrégation MIN de U-SQL de tooa paramètre, nous avons toodefine < remplacement de l’opérateur.

Plus haut dans ce guide, nous l’avons démontré un exemple pour l’identification de période fiscale à partir de la date spécifique de hello dans le format hello Qn:Pn (Q1:P10). Bonjour à l’exemple suivant montre comment toodefine personnalisé de type pour les valeurs de la période fiscales.

Vous trouverez ci-dessous un exemple de section code-behind avec un type défini par l’utilisateur et une interface personnalisée IFormatter :

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

type défini Hello inclut deux nombres : trimestre et mois. Les opérateurs ==/!=/>/< et la méthode statique ToString() sont définis ici.

Comme mentionné précédemment, le type défini par l’utilisateur peut être utilisé dans des expressions SELECT, mais pas dans un GÉNÉRATEUR DE SORTIE/EXTRACTEUR sans sérialisation personnalisée. Il a toobe sérialisées sous forme de chaîne avec ToString() ou utilisé avec un extracteur de OUTPUTTER/personnalisé.

Voyons à présent l’usage d’un type défini par l’utilisateur. Dans une section de code-behind, nous avons modifié nos suivant toohello de fonction GetFiscalPeriod :

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

Comme vous pouvez le voir, il retourne la valeur hello de notre type FiscalPeriod.

Nous proposons un exemple de comment toouse ultérieurement dans le script de base U-SQL. Cet exemple illustre différentes façons d’appeler un type défini par l’utilisateur à partir d’un script U-SQL.

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

Voici un exemple d’une section code-behind complète :

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

## <a name="use-user-defined-aggregates-udagg"></a>Utiliser des agrégats définis par l’utilisateur : UDAGG
Les agrégats définis par l’utilisateur sont toutes les fonctions d’agrégation qui ne sont pas fournies prêtes à l’emploi avec U-SQL. Hello exemple peut être une agrégation tooperform calculs mathématiques personnalisées, des concaténations de chaînes, les manipulations de chaînes et ainsi de suite.

définition de classe de base d’agrégation définies par l’utilisateur Hello est la suivante :

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

**SqlUserDefinedAggregate** indique que le type de hello doit être enregistré comme un agrégat défini par l’utilisateur. Cette classe ne peut pas être héritée.

L’attribut SqlUserDefinedType est **facultatif** pour la définition d’UDAGG.


Hello classe de base vous permet de paramètres de description toopass trois : deux comme paramètres d’entrée et l’autre comme résultat de hello. types de données Hello sont variable et doivent être définies lors de l’héritage de classe.

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

* **Init** appelle une seule fois chaque groupe pendant le calcul. Elle fournit une routine d’initialisation pour chaque groupe d’agrégation.  
* **Accumulate** est exécutée une fois pour chaque valeur. Il fournit des fonctionnalités principales de hello pour l’algorithme d’agrégation hello. Il peut être valeurs tooaggregate utilisés avec divers types de données qui sont définis lors de l’héritage de classe. Elle peut accepter deux paramètres de types de données variables.
* **Mettre fin à** est exécutée une fois par groupe d’agrégation à hello du traitement du résultat de hello toooutput pour chaque groupe.

entrée correcte de toodeclare et les types de données de sortie, utilisez définition de classe hello comme suit :

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* T1 : Premier paramètre tooaccumulate
* T2 : Premier paramètre tooaccumulate
* TResult : type de retour de la routine terminate

Par exemple :

```
public class GuidAggregate : IAggregate<string, int, int>
```

ou

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a>Utiliser UDAGG dans U-SQL
toouse UDAGG, tout d’abord la définir dans le code-behind ou référencer à partir de la programmabilité inexistant hello DLL comme indiqué précédemment.

Utilisez ensuite hello selon la syntaxe :

```
AGG<UDAGG_functionname>(param1,param2)
```

Voici l’exemple d’UDAGG :

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

Et le script U-SQL de base :

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

Dans ce scénario de cas d’utilisation, nous concaténer la classe GUID pour des utilisateurs spécifiques hello.

## <a name="use-user-defined-objects-udo"></a>Utiliser des objets définis par l’utilisateur : UDO
U-SQL vous permet de toodefine les objets de programmabilité personnalisés qui sont appelés objets définis par l’utilisateur ou l’opérateur.

Hello Voici une liste de UDO dans U-SQL :

* Extracteurs définis par l’utilisateur
    * Extraient ligne par ligne
    * Utilisé tooimplement d’extraction de données à partir de fichiers structurés personnalisés

* Générateurs de sortie définis par l’utilisateur
    * Sortent ligne par ligne
    * Utilisé toooutput les types de données personnalisés ou des formats de fichiers personnalisés

* Processeurs définis par l’utilisateur
    * Prennent une ligne et produisent une ligne
    * Tooreduce utilisé hello le nombre de colonnes ou produire de nouvelles colonnes avec des valeurs dérivées d’un ensemble existant de la colonne

* Applicateurs définis par l’utilisateur
    * Prendre une ligne et génère des lignes d’on à 0
    * Utilisés avec OUTER/CROSS APPLY

* Combinateurs définis par l’utilisateur
    * Combinent des ensembles de lignes et des jointures définies par l’utilisateur

* Réducteurs définis par l’utilisateur
    * Prennent n lignes et produisent une ligne
    * Nombre de hello tooreduce de lignes

OPÉRATEUR est généralement appelée explicitement dans le script U-SQL dans le cadre de hello suivant les instructions U-SQL :

* EXTRACT
* OUTPUT
* PROCESS
* COMBINE
* REDUCE

> [!NOTE]  
> OPÉRATEUR est limitées tooconsume 0,5 Go de mémoire.  Cette limitation de mémoire ne s’applique pas toolocal exécutions.

## <a name="use-user-defined-extractors"></a>Utiliser des extracteurs définis par l’utilisateur
U-SQL vous permet de tooimport des données externes à l’aide d’une instruction d’extraction. Une instruction EXTRACT peut utiliser des extracteurs UDO intégrés :  

* *Extractors.Text()* : produit une extraction à partir de fichiers texte délimités de codages différents.

* *Extractors.Csv()* : produit une extraction à partir de fichiers de valeurs séparées par des virgules (CSV) de codages différents.

* *Extractors.Tsv()* : produit une extraction à partir de fichiers de valeurs séparées par des tabulations (TSV) de codages différents.

Il peut être utile toodevelop un extracteur personnalisé. Cela peut être utile lors de l’importation de données si vous souhaitez toodo des hello tâches suivantes :

* Modifier des données d’entrée en fractionnant des colonnes et en modifiant des valeurs individuelles. Hello fonctionnalité du processeur est préférable pour la combinaison de colonnes.
* Analyser des données non structurées telles que des pages web et des messages électroniques, ou des données semi-structurées telles que des fichiers XML/JSON.
* Analyser des données dans un codage non pris en charge.

toodefine un extracteur de défini par l’utilisateur, ou URE, nous devons toocreate un `IExtractor` interface. Toutes les entrées d’extracteur de toohello de paramètres, tels que les séparateurs de colonnes/lignes et le codage, doivent toobe défini dans le constructeur de hello de classe hello. Hello `IExtractor` interface doit également contenir une définition pour hello `IEnumerable<IRow>` remplacer comme suit :

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

Hello **SqlUserDefinedExtractor** attribut indique que le type de hello doit être inscrite en tant qu’un extracteur de défini par l’utilisateur. Cette classe ne peut pas être héritée.

SqlUserDefinedExtractor est un attribut facultatif pour la définition d’UDE. Il utilisé toodefine AtomicFileProcessing propriété pour l’objet d’URE hello.

* bool     AtomicFileProcessing   

* **true** = indique que cet extracteur requiert des fichiers d’entrée atomique (JSON, XML, ...)
* **false** = indique que cet extracteur peut traiter des fichiers fractionnés/distribués (CSV, SEQ, ...)

principaux objets de programmabilité URE Hello sont **d’entrée** et **sortie**. objet d’entrée de Hello est utilisé tooenumerate des données d’entrée en tant que `IUnstructuredReader`. objet de sortie Hello est tooset utilisé les données de sortie à la suite d’activité d’extracteur hello.

les données d’entrée Hello sont accessible via `System.IO.Stream` et `System.IO.StreamReader`.

Pour l’énumération des colonnes d’entrée, nous avons tout d’abord fractionner les flux d’entrée hello à l’aide d’un séparateur de lignes.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

Ensuite, nous fractionnons la ligne d’entrée en parties de colonne.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

les données de sortie tooset, nous utilisons hello `output.Set` (méthode).

Il est important de toounderstand qui hello extracteur personnalisé génère uniquement des colonnes et les valeurs qui sont définies avec la sortie de hello. Définissez l’appel de méthode.

```
output.Set<string>(count, part);
```

Hello extracteur réel sont déclenchées en appelant `yield return output.AsReadOnly();`.

Voici un exemple d’extracteur hello :

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

Dans ce scénario de cas d’usage, extracteur de hello régénère hello GUID pour la colonne « guid » et convertit les valeurs hello du cas de tooupper de colonne « utilisateur ». Des extracteurs personnalisés peuvent produire des résultats plus complexes en analysant et manipulant des données d’entrée.

Le script U-SQL de base utilisant un extracteur personnalisé est le suivant :

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

## <a name="use-user-defined-outputters"></a>Utiliser des générateurs de sortie définis par l’utilisateur
Outputter de défini par l’utilisateur est un autre opérateur U-SQL qui vous permet de tooextend des fonctionnalités intégrées U-SQL. Extracteur de toohello similaires, il existe plusieurs outputters intégrés.

* *Outputters.Text()*: écrit les données toodelimited fichiers texte de codages différents.
* *Outputters.Csv()*: écrit les fichiers de (CSV) de différents encodages de valeurs séparées par des toocomma de données.
* *Outputters.Tsv()*: écrit les fichiers de (TSV) de différents encodages de valeurs séparées par des tootab de données.

Outputter personnalisée vous permet de toowrite données dans un format défini personnalisé. Cela peut être utile pour hello tâches suivantes :

* L’écriture de fichiers de données toosemi-structurées ou non structurées.
* Écrire des données dans des codages non pris en charge.
* Modifier des données de sortie ou ajouter des attributs personnalisés.

toodefine définie par l’utilisateur outputter, nous devons toocreate hello `IOutputter` interface.

Voici hello base `IOutputter` implémentation de la classe :

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

Toutes les entrées outputter toohello de paramètres, tels que les séparateurs de colonnes/lignes, le codage et ainsi de suite, doivent toobe défini dans le constructeur de hello de classe hello. Hello `IOutputter` interface doit également contenir une définition pour `void Output` remplacer. attribut de Hello `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` peut être défini pour le traitement de fichier atomique. Pour plus d’informations, consultez hello les détails suivants.

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

* `Output` est appelé pour chaque ligne d’entrée. Il renvoie hello `IUnstructuredWriter output` ensemble de lignes.
* Hello classe de constructeur est utilisé outputter définie par l’utilisateur de toopass paramètres toohello.
* `Close`est utilisé toooptionally remplacer l’état de coûteuses toorelease ou déterminer lorsque la dernière ligne de hello a été écrit.

**SqlUserDefinedOutputter** attribut indique que le type de hello doit être inscrite en tant qu’un outputter défini par l’utilisateur. Cette classe ne peut pas être héritée.

SqlUserDefinedOutputter est un attribut facultatif pour une définition d’un générateur de sortie défini par l’utilisateur. Il a utilisé la propriété de AtomicFileProcessing toodefine hello.

* bool     AtomicFileProcessing   

* **true** = indique que ce générateur de sortie requiert des fichiers de sortie atomique (JSON, XML, ...)
* **false** = indique que ce générateur de sortie peut traiter des fichiers fractionnés/distribués (CSV, SEQ, ...)

objets de programmabilité principal Hello sont **ligne** et **sortie**. Hello **ligne** objet est utilisé tooenumerate les données de sortie en tant que `IRow` interface. **Sortie** est le fichier cible toohello tooset utilisé sortie données.

données de sortie Hello sont accessible via hello `IRow` interface. Les données de sortie sont transmises une ligne à la fois.

les valeurs individuelles Hello sont énumérées en appelant la méthode Get hello interface IRow de hello :

```
row.Get<string>("column_name")
```

Les noms des colonnes peuvent être déterminés en appelant `row.Schema` :

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

Cette approche vous permet de toobuild un outputter flexible pour n’importe quel schéma de métadonnées.

Hello données de sortie sont écrite toofile à l’aide de `System.IO.StreamWriter`. paramètre de flux Hello est défini trop`output.BaseStrea` dans le cadre de `IUnstructuredWriter output`.

Notez qu’il est le fichier de toohello de la mémoire tampon de données important tooflush hello après chaque itération de la ligne. En outre, hello `StreamWriter` objet doit être utilisé avec hello supprimable attribut activé (valeur par défaut) et hello **à l’aide de** (mot clé) :

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

Autrement, appelez explicitement la méthode Flush() après chaque itération. Nous illustrent ce Bonjour l’exemple suivant.

### <a name="set-headers-and-footers-for-user-defined-outputter"></a>Définir des en-têtes et des pieds de page pour un générateur de sortie défini par l’utilisateur
tooset un en-tête, utilisez le flux d’exécution unique d’itération.

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

Hello code Bonjour tout d’abord `if (isHeaderRow)` bloc est exécuté une seule fois.

Pour le pied de page hello, utilisez l’instance de toohello de référence de hello de `System.IO.Stream` objet (`output.BaseStream`). Écrire un pied de page hello Bonjour méthode Close() Hello `IOutputter` interface.  (Pour plus d’informations, voir hello exemple suivant).

Voici un exemple d’un générateur de sortie défini par l’utilisateur :

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

Et le script U-SQL de base :

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

Il s’agit d’un générateur de sortie HTML qui crée un fichier HTML avec les données de la table.

### <a name="call-outputter-from-u-sql-base-script"></a>Appeler un générateur de sortie à partir du script U-SQL de base
toocall un outputter personnalisé à partir du script U-SQL de la base hello, hello de nouvelle instance d’objet d’outputter hello a toobe créé.

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

tooavoid création d’une instance de hello objet de script de base, nous pouvons créer un wrapper de la fonction, comme indiqué dans l’exemple précédent :

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

Dans ce cas, les appels d’origine hello ressemble à hello suivantes :

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a>Utiliser des processeurs définis par l’utilisateur
Défini par l’utilisateur de processeur ou UDP, est un type d’opérateur U-SQL qui vous permet des lignes entrantes tooprocess hello en appliquant des fonctionnalités de programmabilité. UDP vous toocombine colonnes, modifiez les valeurs et ajouter de nouvelles colonnes si nécessaire. En fait, il vous aide à tooprocess un ensemble de lignes tooproduce requis des éléments de données.

toodefine un UDP, nous devons toocreate un `IProcessor` interface avec hello `SqlUserDefinedProcessor` attribut, qui est facultatif pour le protocole UDP.

Cette interface doit contenir la définition de hello pour hello `IRow` ensemble de lignes interface remplacer, comme indiqué dans hello l’exemple suivant :

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

**SqlUserDefinedProcessor** indique que le type de hello doit être enregistré comme un processeur défini par l’utilisateur. Cette classe ne peut pas être héritée.

l’attribut SqlUserDefinedProcessor Hello est **facultatif** pour la définition de UDP.

objets de programmabilité principal Hello sont **d’entrée** et **sortie**. objet d’entrée de Hello est utilisé tooenumerate des colonnes d’entrée et de sortie et de tooset les données de sortie à la suite de l’activité du processeur hello.

Pour l’énumération des colonnes d’entrée, nous utilisons hello `input.Get` (méthode).

```
string column_name = input.Get<string>("column_name");
```

Hello paramètre `input.Get` méthode est une colonne qui est passée en tant que partie de hello `PRODUCE` clause Hello `PROCESS` instruction de script de base hello U-SQL. Nous devons toouse ici de type de données correct de hello.

Pour une sortie, utilisez hello `output.Set` (méthode).

Il est important toonote qu’un producteur personnalisé génère uniquement les colonnes et les valeurs qui sont définies avec hello `output.Set` appel de méthode.

```
output.Set<string>("mycolumn", mycolumn);
```

sortie du processeur réel Hello est déclenchée en appelant `return output.AsReadOnly();`.

Voici un exemple de processeur :

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

Dans ce scénario de cas d’usage, processeur de hello génère une nouvelle colonne nommée « full_description » en combinant hello les colonnes existantes--dans ce cas, « user » en majuscules et « des ». Aussi, il régénère un GUID et retourne hello d’origine et les nouvelles valeurs GUID.

Comme vous pouvez le voir à partir de l’exemple précédent de hello, vous pouvez appeler les méthodes c# pendant `output.Set` appel de méthode.

Vous trouverez ci-dessous un exemple de script U-SQL de base utilisant un processeur personnalisé :

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

## <a name="use-user-defined-appliers"></a>Utiliser des applicateurs définis par l’utilisateur
Un applicateur de U-SQL définie par l’utilisateur vous permet de fonction tooinvoke personnalisée c# pour chaque ligne retournée par l’expression de table externe hello d’une requête. entrée de droite Hello est évaluée pour chaque ligne à partir de l’entrée de gauche hello et lignes hello qui sont produites sont combinées pour la sortie finale hello. Hello liste de colonnes qui sont produites par l’opérateur APPLY de hello sont la combinaison hello du jeu hello de colonnes dans hello gauche et droit d’entrée de hello.

Applicateur de défini par l’utilisateur est appelé dans le cadre de hello USQL sélectionnez une expression.

Hello appel typique toohello définie par l’utilisateur pour ressemble hello suivantes :

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

Pour plus d’informations sur l’utilisation d’applicateurs dans une expression SELECT, voir [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx) (Sélection d’U-SQL SELECT à partir de CROSS APPLY et de OUTER APPLY).

définition Hello défini par l’utilisateur pour la classe de base est la suivante :

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

toodefine un applicateur défini par l’utilisateur, nous devons toocreate hello `IApplier` interface avec hello [`SqlUserDefinedApplier`] attribut, qui est facultatif pour une définition pour défini par l’utilisateur.

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

* Appliquer est appelée pour chaque ligne de table externe de hello. Il renvoie hello `IUpdatableRow` ensemble de lignes de sortie.
* classe de constructeur Hello est utilisé toopass paramètres toohello définie par l’utilisateur APPLICATEUR.

**SqlUserDefinedApplier** indique que le type de hello doit être inscrite en tant qu’un applicateur défini par l’utilisateur. Cette classe ne peut pas être héritée.

**SqlUserDefinedApplier** est **facultatif** pour une définition d’applicateur défini par l’utilisateur.


objets de programmabilité principal Hello sont les suivantes :

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

Les ensembles de lignes d’entrée sont transmis en tant qu’entrée `IRow`. Hello lignes de sortie sont générées en tant que `IUpdatableRow` interface de sortie.

Un nom de colonne peut être déterminé en appelant hello `IRow` méthode du schéma.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

valeurs de données réelles hello tooget de hello entrant `IRow`, nous utilisons la méthode hello Get() `IRow` interface.

```
mycolumn = row.Get<int>("mycolumn")
```

Ou bien, nous utilisons le nom de colonne de schéma hello :

```
row.Get<int>(row.Schema[0].Name)
```

Hello valeurs de sortie doivent être définies avec `IUpdatableRow` sortie :

```
output.Set<int>("mycolumn", mycolumn)
```

Il est important toounderstand qui appliers personnalisés sortie uniquement les colonnes et les valeurs qui sont définies avec `output.Set` appel de méthode.

le résultat réel Hello est déclenché en appelant `yield return output.AsReadOnly();`.

Hello défini par l’utilisateur des paramètres pour peuvent être passés toohello constructeur. APPLICATEUR peut retourner un nombre variable de colonnes qui doivent toobe défini pendant l’appel pour hello base Script U-SQL.

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

Voici hello défini par l’utilisateur pour exemple :

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

Voici hello base U-script SQL pour cette APPLICATEUR défini par l’utilisateur :

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

Dans ce scénario d’utilisation, définis par l’utilisateur pour joue un analyseur délimitée par des virgules de valeur pour les propriétés de flotte hello voiture. lignes du fichier d’entrée Hello ressemble à hello qui suit :

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

Il s’agit d’un fichier TSV standard de valeurs délimitées par des tabulations avec une colonne Propriétés contenant des propriétés de voitures telles que la marque et le modèle. Ces propriétés doivent être des colonnes de table toohello analysé. Applicateur de Hello fourni vous permet également de toogenerate dynamique plusieurs propriétés Bonjour entraîner ensemble de lignes, selon le paramètre hello qui est passé. Vous pouvez générer soit toutes les propriétés, soit un ensemble spécifique de propriétés.

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

Applicateur de Hello défini par l’utilisateur peut être appelé comme une nouvelle instance de l’objet pour :

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

Ou avec une méthode de fabrique wrapper appel hello :

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a>Utiliser des combinateurs définis par l’utilisateur
Défini par l’utilisateur un combinateur ou UDC, vous permet de toocombine les lignes à partir d’ensembles de lignes gauche et droit, selon une logique personnalisée. Un combinateur défini par l’utilisateur est utilisé avec l’expression COMBINE.

Une association est appelée avec expression combiner hello hello les informations requises sur les deux ensembles de lignes d’entrée hello, hello regroupement des colonnes, hello attendu schéma de résultats et des informations supplémentaires.

toocall un combinateur dans un script U-SQL de base, nous utilisons hello selon la syntaxe :

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

Pour plus d’informations, voir [Expression COMBINE (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).

toodefine un combinateur défini par l’utilisateur, nous devons toocreate hello `ICombiner` interface avec hello [`SqlUserDefinedCombiner`] attribut, qui est facultatif pour une définition COMBINATEUR défini par l’utilisateur.

Définition de classe `ICombiner` de base :

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

Hello implémentation personnalisée d’un `ICombiner` interface doit contenir la définition de hello pour une `IEnumerable<IRow>` combiner de remplacement.

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

Hello **SqlUserDefinedCombiner** attribut indique que le type de hello doit être inscrite en tant qu’un combinateur défini par l’utilisateur. Cette classe ne peut pas être héritée.

**SqlUserDefinedCombiner** est la propriété du mode utilisé toodefine hello COMBINATEUR. C’est un attribut facultatif pour une définition de combinateur défini par l’utilisateur.

CombinerMode     Mode

CombinerMode enum peut prendre hello valeurs suivantes :

* Complète (0) pour de que chaque ligne de sortie dépend potentiellement toutes les lignes d’entrée hello gauche et droite avec hello même valeur de clé.

* Gauche (1), chaque ligne de sortie dépend d’une seule ligne d’entrée de hello gauche (et potentiellement toutes les lignes de hello droite avec hello même valeur de clé).

* Droite (2), chaque ligne de sortie dépend d’une ligne d’entrée de hello droit (et potentiellement toutes les lignes de gauche hello avec hello même valeur de clé).

* Interne (3), chaque ligne de sortie dépend d’une seule entrée de ligne à partir de la gauche et droite avec hello même valeur.

Exemple :    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]


objets de programmabilité principal Hello sont :

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

Les ensembles de lignes d’entrée sont transmis en tant que type d’interface **gauche** et **droit** `IRowset`. Les deux ensembles de lignes doivent être énumérés pour le traitement. Vous pouvez uniquement énumérer chaque interface une seule fois, nous avons ont tooenumerate et mettre en cache si nécessaire.

Pour la mise en cache, nous pouvons créer un type List\<T\> de structure de mémoire résultant de l’exécution d’une requête LINQ, plus particulièrement List<`IRow`>. type de données anonymes de Hello peut être utilisé lors de l’énumération également.

Consultez [Introduction tooLINQ requêtes (c#)](https://msdn.microsoft.com/library/bb397906.aspx) pour plus d’informations sur les requêtes LINQ, et [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) pour plus d’informations sur IEnumerable\<T\> interface.

valeurs de données réelles hello tooget de hello entrant `IRowset`, nous utilisons la méthode hello Get() `IRow` interface.

```
mycolumn = row.Get<int>("mycolumn")
```

Un nom de colonne peut être déterminé en appelant hello `IRow` méthode du schéma.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

Ou à l’aide du nom de colonne de schéma hello :

```
c# row.Get<int>(row.Schema[0].Name)
```

énumération de général Hello avec LINQ ressemble à hello suivantes :

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

Après l’énumération des deux ensembles de lignes, nous allons tooloop dans toutes les lignes. Pour chaque ligne dans l’ensemble de lignes gauche hello, nous allons toofind toutes les lignes qui satisfont la condition hello de notre association.

Hello valeurs de sortie doivent être définies avec `IUpdatableRow` sortie.

```
output.Set<int>("mycolumn", mycolumn)
```

le résultat réel Hello est déclenché en appelant trop`yield return output.AsReadOnly();`.

Voici un exemple de combinateur :

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

Dans ce scénario de cas d’utilisation, nous allons créer un rapport analytique pour le site de vente hello. Hello vise toofind tous les produits dont le prix est supérieur à 20 000 $ et que vendent sur le site Web de hello plus rapidement qu’avec le site de vente régulière hello dans un intervalle de temps donné.

Voici le script U-SQL de la base hello. Vous pouvez comparer la logique de hello entre une jointure normale et une association :

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

Un combinateur défini par l’utilisateur peut être appelé comme une nouvelle instance de l’objet de hello pour :

```
USING new MyNameSpace.MyCombiner();
```


Ou avec une méthode de fabrique wrapper appel hello :

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a>Utiliser des réducteurs définis par l’utilisateur

U-SQL vous permet de REDUCTEURS d’ensemble de lignes personnalisée toowrite en c# à l’aide d’infrastructure d’extensibilité hello opérateur défini par l’utilisateur et l’implémentation d’une interface IReducer.

Réducteur de défini par l’utilisateur ou UDR, peut être des lignes inutiles tooeliminate utilisé lors de l’extraction de données (importation). Il peut être toomanipulate utilisé et évaluer les lignes et colonnes. Selon la logique de programmabilité, elle peut également définir les lignes doivent toobe extraite.

toodefine une classe UDR, nous devons toocreate un `IReducer` interface facultative `SqlUserDefinedReducer` attribut.

Cette interface de classe doit contenir une définition pour hello `IEnumerable` remplacer des lignes de l’interface.

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

Hello **SqlUserDefinedReducer** attribut indique que le type de hello doit être inscrite en tant qu’un réducteur défini par l’utilisateur. Cette classe ne peut pas être héritée.
**SqlUserDefinedReducer** est un attribut facultatif pour une définition de réducteur défini par l’utilisateur. Il a utilisé toodefine IsRecursive propriété.

* bool     IsRecursive    
* **true**  = indique si cette réduction est idempotente

objets de programmabilité principal Hello sont **d’entrée** et **sortie**. objet d’entrée de Hello est utilisé tooenumerate les lignes d’entrée. La sortie est utilisé tooset les lignes de sortie suite à la réduction de l’activité.

Pour l’énumération des lignes d’entrée, nous utilisons hello `Row.Get` (méthode).

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

Hello paramètre hello `Row.Get` méthode est une colonne qui est passée en tant que partie de hello `PRODUCE` classe Hello `REDUCE` instruction de script de base hello U-SQL. Nous devons toouse hello type de données correct ici également.

Pour une sortie, utilisez hello `output.Set` (méthode).

Il est important toounderstand qui réducteur personnalisé uniquement sorties des valeurs qui sont définies avec hello `output.Set` appel de méthode.

```
output.Set<string>("mycolumn", guid);
```

Hello réducteur réel sont déclenchées en appelant `yield return output.AsReadOnly();`.

Voici un exemple de réducteur :

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

Dans ce scénario de cas d’usage, réducteur de hello ignore les lignes avec un nom d’utilisateur vide. Pour chaque ligne dans l’ensemble de lignes, il lit chaque colonne requise, puis évalue la longueur du nom d’utilisateur hello hello. Il génère une ligne hello uniquement si la longueur de nom des utilisateurs à l’aide de la valeur est supérieure à 0.

Le script U-SQL de base utilisant un réducteur personnalisé est le suivant :

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
