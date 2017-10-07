---
title: "aaaScale U-SQL local exécuter et tester avec le Kit de développement logiciel Azure données Lake U-SQL | Documents Microsoft"
description: "Découvrez comment les travaux de tooscale U-SQL de SQL-U de LAC de données Azure SDK toouse local exécute et de test avec la ligne de commande et les interfaces de programmation sur votre station de travail locale."
services: data-lake-analytics
documentationcenter: 
author: 
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: yanacai
ms.openlocfilehash: 2b0a16229789268e333f723ff6fc2c3efdc29905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-u-sql-local-run-and-test-with-azure-data-lake-u-sql-sdk"></a>Mettre à l’échelle l’exécution et les tests U-SQL locaux avec le kit SDK Azure Data Lake U-SQL

Lors du développement de script U-SQL, il est commun toorun et le script de test U-SQL localement soumet avant toocloud. Azure Data Lake fournit un package NuGet appelé Kit SDK SQL Azure Data Lake U-SQL pour ce scénario, par le biais duquel vous pouvez facilement mettre à l’échelle l’exécution et les tests U-SQL locaux. Il est également possible de toointegrate cette U-SQL de test avec l’élément de configuration (intégration continue) système tooautomate hello compiler et tester.

Si vous vous souciez comment toomanually local exécuter et déboguer le script U-SQL avec les outils de l’interface utilisateur graphique, vous pouvez ensuite utiliser Azure Data Lake Tools pour Visual Studio pour que. Pour plus d’informations, cliquez [ici](data-lake-analytics-data-lake-tools-local-run.md).

## <a name="install-azure-data-lake-u-sql-sdk"></a>Installer le Kit SDK Azure Data Lake U-SQL

Vous pouvez obtenir hello SQL-U de LAC de données Azure SDK [ici](https://www.nuget.org/packages/Microsoft.Azure.DataLake.USQL.SDK/) sur Nuget.org. Et avant de l’utiliser, vous devez toomake que vous disposez des dépendances comme suit.

### <a name="dependencies"></a>Dépendances

Hello données Lake U-SQL SDK nécessite hello suivant des dépendances :

- [Microsoft .NET Framework 4.6 ou une version ultérieure](https://www.microsoft.com/download/details.aspx?id=17851).
- Microsoft Visual C++ 14 et le Kit SDK Windows 10.0.10240.0 ou une version plus récente (appelé CppSDK dans cet article). Il existe deux façons tooget CppSDK :

    - Installez [Visual Studio Community Edition](https://developer.microsoft.com/downloads/vs-thankyou). Vous avez un dossier \Windows Kits\10 sous le dossier Program Files hello : par exemple, C:\Program Files (x86) \Windows Kits\10\. Vous trouverez également la version du SDK Windows 10 hello sous \Windows Kits\10\Lib. Si vous ne voyez pas ces dossiers, réinstallez Visual Studio et que tooselect hello SDK Windows 10 lors de l’installation de hello. Si vous avez cela installé avec Visual Studio, compilateur local de hello U-SQL se trouve automatiquement.

    ![Data Lake Tools pour Visual Studio exécution locale Windows 10 SDK](./media/data-lake-analytics-data-lake-tools-local-run/data-lake-tools-for-visual-studio-local-run-windows-10-sdk.png)

    - Installez [Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs). Vous pouvez trouver des fichiers Visual C++ et le Kit de développement à l’emplacement C:\Program Files (x86) \Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\ADL Tools\X.X.XXXX.X\CppSDK en préemballages hello. Dans ce cas, compilateur local de hello U-SQL ne peut pas rechercher des dépendances de hello automatiquement. Vous devez le chemin d’accès CppSDK toospecify hello pour celle-ci. Vous pouvez copier l’emplacement des fichiers de tooanother hello ou utiliser tel quel.

## <a name="understand-basic-concepts"></a>Comprendre les concepts de base

### <a name="data-root"></a>Racine de données

dossier de données racine de Hello est un « magasin local » pour le compte de calcul local hello. Il est le compte d’Azure Data Lake Store toohello équivalent d’un compte Analytique lac de données. Dossier de données-racine différent tooa de commutation est identique à commutation tooa autre banque de compte. Si vous souhaitez tooaccess fréquemment les données partagées avec des dossiers racine de données différents, vous devez utiliser des chemins d’accès absolus dans vos scripts. Ou bien, créez des liens symboliques de système de fichier (par exemple, **mklink** sur NTFS) sous hello racine de données dossier toopoint toohello les données partagées.

dossier de données racine Hello est utilisé pour :

- Stocker les métadonnées locales, notamment des bases de données, des tables, des fonctions table (TVF) et des assemblys.
- Rechercher hello d’entrée et les chemins d’accès de sortie sont définies comme des chemins d’accès relatifs dans U-SQL. À l’aide de chemins d’accès relatifs rend plus facile toodeploy votre tooAzure de projets U-SQL.

### <a name="file-path-in-u-sql"></a>Chemin d’accès des fichiers dans U-SQL

Vous pouvez utiliser un chemin d’accès relatif et un chemin d’accès absolu local dans des scripts SQL-U. chemin d’accès relatif de Hello est le chemin d’accès au dossier toohello relatif racine de données spécifié. Il est recommandé que vous utilisez « / » comme hello toomake de séparateur de chemin d’accès de vos scripts compatibles avec SSI hello. Voici quelques exemples de chemins relatifs, avec leurs chemins absolus équivalents. Dans ces exemples, C:\LocalRunDataRoot est le dossier racine de données de hello.

|Chemin relatif|Chemin absolu|
|-------------|-------------|
|/abc/def/input.csv |C:\LocalRunDataRoot\abc\def\input.csv|
|abc/def/input.csv  |C:\LocalRunDataRoot\abc\def\input.csv|
|D:/abc/def/input.csv |D:\abc\def\input.csv|

### <a name="working-directory"></a>Répertoire de travail

Lorsque vous exécutez le script de hello U-SQL localement, un répertoire de travail est créé lors de la compilation sous le répertoire en cours d’exécution. En outre toohello compilation génère, hello nécessitent des fichiers d’exécution pour une exécution locale sera répertoire de travail copié toothis de clichés instantanés. Hello dossier racine de répertoire de travail est appelé « ScopeWorkDir » et les fichiers hello sous le répertoire de travail de hello sont les suivants :

|Répertoire/fichier|Répertoire/fichier|Répertoire/fichier|Définition|Description|
|--------------|--------------|--------------|----------|-----------|
|C6A101DDCB470506| | |Chaîne de hachage de la version exécutable|Cliché instantané des fichiers exécutables nécessaires à l'exécution locale|
| |Script_66AE4909AA0ED06C| |Nom de script + chaîne de hachage du chemin du script|Résultats de la compilation et journalisation des étapes d'exécution|
| | |\_script\_.abr|Sortie du compilateur|Fichier algèbre|
| | |\_ScopeCodeGen\_.*|Sortie du compilateur|Code géré généré|
| | |\_ScopeCodeGenEngine\_.*|Sortie du compilateur|Code natif généré|
| | |referenced assemblies|Référence d’assembly|Fichiers d’assemblys de référence|
| | |deployed_resources|Déploiement de ressources|Fichiers de déploiement de ressources|
| | |xxxxxxxx.xxx[1..n]\_\*.*|Journal d’exécution|Journal des étapes d'exécution|


## <a name="use-hello-sdk-from-hello-command-line"></a>Utilisez hello SDK à partir de la ligne de commande hello

### <a name="command-line-interface-of-hello-helper-application"></a>Interface de ligne de commande de l’application d’assistance de hello

Sous directory\build\runtime du Kit de développement logiciel, LocalRunHelper.exe est hello d’assistance de ligne de commande qui fournit des fonctions de toomost Hello couramment utilisées et exécution locale d’interfaces. Notez que les deux hello commande et les commutateurs d’arguments hello respectent la casse. tooinvoke il :

    LocalRunHelper.exe <command> <Required-Command-Arguments> [Optional-Command-Arguments]

Exécutez LocalRunHelper.exe sans argument ou avec hello **aide** passer les informations d’aide tooshow hello :

    > LocalRunHelper.exe help

        Command 'help' :  Show usage information
        Command 'compile' :  Compile hello script
        Required Arguments :
            -Script param
                    Script File Path
        Optional Arguments :
            -Shallow [default value 'False']
                    Shallow compile

Informations d’aide dans hello :

-  **Commande** donne hello nom de la commande.  
-  Le paramètre **Argument obligatoire** répertorie les arguments qui doivent être fournis.  
-  Le paramètre **Argument facultatif** répertorie les arguments facultatifs, avec des valeurs par défaut.  Facultatif pour les arguments booléens n’ont pas les paramètres, et leur apparence signifie tootheir négatif par défaut.

### <a name="return-value-and-logging"></a>Valeur de retour et journalisation

application d’assistance de Hello retourne **0** de réussite et **-1** de l’échec. Par défaut, le programme d’assistance hello envoie console actuelle de tous les messages toohello. Toutefois, la plupart des commandes hello prennent en charge hello **-(messageout) chemin_vers_fichier_journal** argument facultatif qui redirige hello génère le fichier de journal tooa.

### <a name="environment-variable-configuring"></a>Configuration de la variable d’environnement

L’exécution U-SQL locale requiert une racine de données spécifiée comme compte de stockage local, ainsi qu’un chemin d’accès CppSDK spécifié pour les dépendances. Vous pouvez à la fois argument de hello défini dans la variable d’environnement de ligne de commande ou est définie pour eux.

- Ensemble hello **SCOPE_CPP_SDK** variable d’environnement.

    Si vous obtenez Microsoft Visual C++ et hello Kit de développement logiciel Windows en installant Data Lake Tools pour Visual Studio, vérifiez que vous avez hello suivant du dossier :

        C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE\Extensions\Microsoft\Microsoft Azure Data Lake Tools for Visual Studio 2015\X.X.XXXX.X\CppSDK

    Définir une nouvelle variable d’environnement appelée **SCOPE_CPP_SDK** toopoint toothis active. Ou copiez hello dossier toohello autre emplacement et spécifier **SCOPE_CPP_SDK** que.

    Dans la variable d’environnement toosetting hello plus, vous pouvez spécifier hello **- CppSDK** argument lorsque vous utilisez la ligne de commande hello. Cet argument remplace votre variable d’environnement CppSDK par défaut.

- Ensemble hello **LOCALRUN_DATAROOT** variable d’environnement.

    Définir une nouvelle variable d’environnement appelée **LOCALRUN_DATAROOT** qui pointe toohello la racine de données.

    Dans la variable d’environnement toosetting hello plus, vous pouvez spécifier hello **- DataRoot** argument avec un chemin d’accès racine de données hello lorsque vous utilisez une ligne de commande. Cet argument remplace votre variable d’environnement de racine de données par défaut. Vous devez tooadd cet argument de ligne de commande tooevery que vous êtes en cours d’exécution afin que vous pouvez remplacer la variable d’environnement racine de données hello par défaut pour toutes les opérations.

### <a name="sdk-command-line-usage-samples"></a>Exemples d’utilisation en ligne de commande du Kit SDK

#### <a name="compile-and-run"></a>Compilation et exécution

Hello **exécuter** commande toocompile hello script et puis exécutez résultats compilés. Ses arguments de ligne de commande sont une combinaison des commandes **compile** et **execute**.

    LocalRunHelper run -Script path_to_usql_script.usql [optional_arguments]

Hello Voici les arguments facultatifs pour **exécuter**:


|Argument|Valeur par défaut|Description|
|--------|-------------|-----------|
|-CodeBehind|False|script de Hello associé au code .cs|
|-CppSDK| |Répertoire CppSDK|
|-DataRoot| Variable d’environnement DataRoot|DataRoot pour la série locale, par défaut trop variable d’environnement 'LOCALRUN_DATAROOT'|
|-MessageOut| |Vider les messages sur le fichier de console tooa|
|-Parallel|1|Exécutez hello plan avec hello spécifié de parallélisme|
|-References| |Liste des assemblys de référence tooextra de chemins d’accès ou les fichiers de données de code-behind, séparé par ';'|
|-UdoRedirect|False|Générer la configuration de redirection d’assembly Udo|
|-UseDatabase|master|Toouse de base de données pour le code-behind d’inscription de l’assembly temporaire|
|-Verbose|False|Afficher les sorties détaillées du runtime|
|-WorkDir|Répertoire actif|Répertoire des sorties et de l’utilisation du compilateur|
|-RunScopeCEP|0|ScopeCEP mode toouse|
|-ScopeCEPTempPath|temp|Toouse de chemin d’accès temporaire pour la diffusion en continu de données|
|-OptFlags| |Liste séparée par des virgules d’indicateurs d’optimiseur|


Voici un exemple :

    LocalRunHelper run -Script d:\test\test1.usql -WorkDir d:\test\bin -CodeBehind -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB –Parallel 5 -Verbose

Outre la combinaison **compiler** et **exécuter**, vous pouvez compiler et exécuter des exécutables de hello compilé séparément.

#### <a name="compile-a-u-sql-script"></a>Compiler un script U-SQL

Hello **compiler** commande est utilisée toocompile U-SQL script tooexecutables.

    LocalRunHelper compile -Script path_to_usql_script.usql [optional_arguments]

Hello Voici les arguments facultatifs pour **compiler**:


|Argument|Description|
|--------|-----------|
| -CodeBehind [valeur par défaut 'False']|script de Hello associé au code .cs|
| -CppSDK [valeur par défaut '']|Répertoire CppSDK|
| -DataRoot [valeur par défaut ’DataRoot environment variable’]|DataRoot pour la série locale, par défaut trop variable d’environnement 'LOCALRUN_DATAROOT'|
| -MessageOut [valeur par défaut '']|Vider les messages sur le fichier de console tooa|
| -References [valeur par défaut '']|Liste des assemblys de référence tooextra de chemins d’accès ou les fichiers de données de code-behind, séparé par ';'|
| -Shallow [valeur par défaut 'False']|Compilation superficielle|
| -UdoRedirect [valeur par défaut 'False']|Générer la configuration de redirection d’assembly Udo|
| -UseDatabase [valeur par défaut 'master']|Toouse de base de données pour le code-behind d’inscription de l’assembly temporaire|
| -WorkDir [valeur par défaut ’Current Directory’]|Répertoire des sorties et de l’utilisation du compilateur|
| -RunScopeCEP [valeur par défaut ’0’]|ScopeCEP mode toouse|
| -ScopeCEPTempPath [valeur par défaut ’temp’]|Toouse de chemin d’accès temporaire pour la diffusion en continu de données|
| -OptFlags [valeur par défaut ’’]|Liste séparée par des virgules d’indicateurs d’optimiseur|


Voici quelques exemples d’utilisation.

Compilez un script U-SQL :

    LocalRunHelper compile -Script d:\test\test1.usql

Compiler un script U-SQL et définir le dossier de données racine hello. Notez que cette opération va remplacer la variable d’environnement hello ensemble.

    LocalRunHelper compile -Script d:\test\test1.usql –DataRoot c:\DataRoot

Compilez un script U-SQL et définissez un répertoire de travail, un assembly de référence et une base de données :

    LocalRunHelper compile -Script d:\test\test1.usql -WorkDir d:\test\bin -References "d:\asm\ref1.dll;d:\asm\ref2.dll" -UseDatabase testDB

#### <a name="execute-compiled-results"></a>Exécuter les résultats compilés

Hello **exécuter** commande est utilisée tooexecute compilé résultats.   

    LocalRunHelper execute -Algebra path_to_compiled_algebra_file [optional_arguments]

Hello Voici les arguments facultatifs pour **exécuter**:

|Argument|Description|
|--------|-----------|
|-DataRoot [valeur par défaut '']|Racine de données pour l’exécution des métadonnées. Sa valeur par défaut toohello **LOCALRUN_DATAROOT** variable d’environnement.|
|-MessageOut [valeur par défaut '']|Vider les messages sur le fichier de tooa console hello.|
|-Parallel [valeur par défaut '1']|Étapes d’exécution locale indicateur toorun hello généré par hello spécifié au niveau de parallélisme.|
|-Verbose [valeur par défaut 'False']|Indicateur tooshow détaillées des sorties à partir de l’exécution.|

Voici un exemple d’utilisation :

    LocalRunHelper execute -Algebra d:\test\workdir\C6A101DDCB470506\Script_66AE4909AA0ED06C\__script__.abr –DataRoot c:\DataRoot –Parallel 5


## <a name="use-hello-sdk-with-programming-interfaces"></a>Utilisez hello Kit de développement logiciel avec les interfaces de programmation

interfaces de programmation Hello se trouvent dans hello LocalRunHelper.exe. Vous pouvez utiliser les fonctionnalités de hello de toointegrate Hello U-SQL SDK et hello c# test framework tooscale votre test local du script U-SQL. Dans cet article, je vais utiliser hello standard c# unité test projet tooshow toouse ces interfaces tootest votre script U-SQL.

### <a name="step-1-create-c-unit-test-project-and-configuration"></a>Étape 1 : Créer une configuration et un projet de test unitaire C#

- Créez un projet de test unitaire C# dans Fichier > Nouveau > Projet > Visual C# > Test > Projet de test unitaire.
- Ajoutez LocalRunHelper.exe comme référence pour le projet de hello. Hello LocalRunHelper.exe se trouve dans \build\runtime\LocalRunHelper.exe dans le package Nuget.

    ![Kit SDK Azure Data Lake U-SQL - Ajouter une référence](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-add-reference.png)

- Kit de développement logiciel U-SQL **uniquement** prise en charge x64, environnement, vérifiez que tooset build plateforme cible en tant que x64. Vous pouvez le faire dans Propriété du projet > Build > Plateforme cible.

    ![Kit SDK Azure Data Lake U-SQL - Configurer un projet x64](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-x64.png)

- Assurez-vous que tooset votre environnement de test en tant que x64. Dans Visual Studio, vous pouvez le faire dans Test > Paramètres de test > Architecture de processeur par défaut > x64.

    ![Kit SDK Azure Data Lake U-SQL - Configurer un environnement de test x64](./media/data-lake-analytics-u-sql-sdk/data-lake-analytics-u-sql-sdk-configure-test-x64.png)

- Assurez-vous que toocopy tous les fichiers de dépendance sous le répertoire de travail tooproject NugetPackage\build\runtime\ qui est habituellement sous ProjectFolder\bin\x64\Debug.

### <a name="step-2-create-u-sql-script-test-case"></a>Étape 2 : Créer des cas de test du script U-SQL

Voici un exemple de code hello pour le test de script U-SQL. Pour le test, vous devez tooprepare, scripts, fichiers d’entrée et sortie attendue.

    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;
    using System.IO;
    using System.Text;
    using System.Security.Cryptography;
    using Microsoft.Analytics.LocalRun;

    namespace UnitTestProject1
    {
        [TestClass]
        public class USQLUnitTest
        {
            [TestMethod]
            public void TestUSQLScript()
            {
                //Specify hello local run message output path
                StreamWriter MessageOutput = new StreamWriter("../../../log.txt");

                LocalRunHelper localrun = new LocalRunHelper(MessageOutput);

                //Configure hello DateRoot path, Script Path and CPPSDK path
                localrun.DataRoot = "../../../";
                localrun.ScriptPath = "../../../Script/Script.usql";
                localrun.CppSdkDir = "../../../CppSDK";

                //Run U-SQL script
                localrun.DoRun();

                //Script output 
                string Result = Path.Combine(localrun.DataRoot, "Output/result.csv");

                //Expected script output
                string ExpectedResult = "../../../ExpectedOutput/result.csv";

                Test.Helpers.FileAssert.AreEqual(Result, ExpectedResult);

                //Don't forget tooclose MessageOutput tooget logs into file
                MessageOutput.Close();
            }
        }
    }

    namespace Test.Helpers
    {
        public static class FileAssert
        {
            static string GetFileHash(string filename)
            {
                Assert.IsTrue(File.Exists(filename));

                using (var hash = new SHA1Managed())
                {
                    var clearBytes = File.ReadAllBytes(filename);
                    var hashedBytes = hash.ComputeHash(clearBytes);
                    return ConvertBytesToHex(hashedBytes);
                }
            }

            static string ConvertBytesToHex(byte[] bytes)
            {
                var sb = new StringBuilder();

                for (var i = 0; i < bytes.Length; i++)
                {
                    sb.Append(bytes[i].ToString("x"));
                }
                return sb.ToString();
            }

            public static void AreEqual(string filename1, string filename2)
            {
                string hash1 = GetFileHash(filename1);
                string hash2 = GetFileHash(filename2);

                Assert.AreEqual(hash1, hash2);
            }
        }
    }


### <a name="programming-interfaces-in-localrunhelperexe"></a>Interfaces de programmation dans LocalRunHelper.exe

LocalRunHelper.exe fournit hello interfaces de programmation pour la compilation locale U-SQL, exécuter, les interfaces hello etc. sont répertoriés comme suit.

**Constructeur**

public LocalRunHelper([System.IO.TextWriter messageOutput = null])

|Paramètre|Type|Description|
|---------|----|-----------|
|messageOutput|System.IO.TextWriter|pour les messages de sortie, définissez toonull toouse Console|

**Propriétés**

|Propriété|Type|Description|
|--------|----|-----------|
|AlgebraPath|string|Hello chemin d’accès tooalgebra fichier (fichier de l’algèbre est un des résultats de compilation hello)|
|CodeBehindReferences|string|Si le script de hello possède des références de code supplémentaire, spécifier des chemins d’accès de hello séparées par ';'|
|CppSdkDir|string|Répertoire CppSDK|
|CurrentDir|string|Répertoire actif|
|DataRoot|string|Chemin d’accès de la racine de données|
|DebuggerMailPath|string|Hello chemin d’accès toodebugger mailslot|
|GenerateUdoRedirect|bool|Si nous voulons que le chargement d’assemblys toogenerate la redirection de remplacer la configuration|
|HasCodeBehind|bool|Si le script de hello a code-behind|
|InputDir|string|Répertoire des données d’entrée|
|MessagePath|string|Chemin d’accès du fichier de vidage des messages|
|OutputDir|string|Répertoire des données de sortie|
|Parallélisme|int|Algèbre de parallélisme toorun hello|
|ParentPid|int|PID du parent hello sur quel hello service surveille tooexit, jeu too0 ou tooignore négatif|
|ResultPath|string|Chemin d’accès du fichier de vidage des résultats|
|RuntimeDir|string|Répertoire du runtime|
|ScriptPath|string|Où toofind hello script|
|Shallow|valeur booléenne|Compilation superficielle ou non|
|TempDir|string|Répertoire Temp|
|UseDataBase|string|Spécifiez toouse de base de données hello pour le code-behind d’enregistrement de l’assembly temporaire, maître par défaut|
|WorkDir|string|Répertoire de travail favori|


**Méthode**

|Méthode|Description|Renvoie|Paramètre|
|------|-----------|------|---------|
|public bool DoCompile()|Compiler hello U-SQL script|True en cas de réussite| |
|public bool DoExec()|Exécution du résultat de hello compilé|True en cas de réussite| |
|public bool DoRun()|Exécutez hello U-SQL script (compiler + exécuter)|True en cas de réussite| |
|public bool IsValidRuntimeDir(string chemin-d’accès)|Vérifier si hello chemin d’accès donné est le chemin d’accès d’exécution valide|True en cas de validité|chemin d’accès de Hello du répertoire du runtime|


## <a name="faq-about-common-issue"></a>FAQ sur les problèmes courants

### <a name="error-1"></a>Erreur 1 :
E_CSC_SYSTEM_INTERNAL : Erreur interne ! Impossible de charger le fichier ou l’assembly « ScopeEngineManaged.dll » ou une de ses dépendances. module de Hello spécifié est introuvable.

Vérifiez les suivant hello :

- Assurez-vous que vous avez un environnement x64. plateforme cible de build Hello et environnement de test hello doit être x64, consultez trop**étape 1 : créer c# unité projet de test et configuration** ci-dessus.
- Assurez-vous que vous avez copié tous les fichiers de dépendance sous le répertoire de travail NugetPackage\build\runtime\ tooproject.


## <a name="next-steps"></a>Étapes suivantes

* toolearn U-SQL, consultez [prise en main langage lac de données Azure Analytique U-SQL](data-lake-analytics-u-sql-get-started.md).
* toolog des informations de diagnostic, consultez [l’accès aux journaux de diagnostic pour l’Analytique de LAC de données Azure](data-lake-analytics-diagnostic-logs.md).
* toosee une requête plus complexe, consultez [analyser les journaux du site Web à l’aide d’Analytique de LAC de données Azure](data-lake-analytics-analyze-weblogs.md).
* Détails de la tâche tooview, consultez [navigateur de travail d’utilisation et de la vue des travaux pour les travaux de l’Analytique de LAC de données Azure](data-lake-analytics-data-lake-tools-view-jobs.md).
* vue de l’exécution toouse hello vertex, consultez [hello d’utilisation vue de l’exécution de sommets dans Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-use-vertex-execution-view.md).
