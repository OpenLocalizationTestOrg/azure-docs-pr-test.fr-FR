---
title: "Azure Data Lake Tools : Utiliser Azure Data Lake Tools pour Visual Studio Code | Microsoft Docs"
description: "Découvrez comment toouse Azure Data Lake Tools pour Visual Studio Code toocreate, tester et exécuter des scripts U-SQL. "
Keywords: "Chemin d’accès de le toostorage de téléchargement VScode, Azure Data Lake Tools, exécution, le fichier de stockage débogage Local, le débogage Local, version d’évaluation locale"
services: data-lake-analytics
documentationcenter: 
author: jejiang
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: dc9b21d8-c5f4-4f77-bcbc-eff458f48de2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/14/2017
ms.author: jejiang
ms.openlocfilehash: 77771c5d5dae3bfce4ad2df240ea6c6ef848f288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-tools-for-visual-studio-code"></a>Utiliser Azure Data Lake Tools pour Visual Studio Code

Découvrez comment toouse Azure Data Lake Tools pour Visual Studio Code (Code de Visual Studio), toocreate, tester et exécuter des scripts U-SQL. informations de Hello sont également décrite dans hello suivant vidéo :

<a href="https://www.youtube.com/watch?v=J_gWuyFnaGA&feature=youtu.be"><img src="./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-video.png"></a>

## <a name="prerequisites"></a>Composants requis

Outils de LAC de données peuvent être installés sur les plateformes hello pris en charge par le Code de Visual Studio. les plateformes de Hello pris en charge incluent Windows, Linux et MacOS. différentes plateformes de Hello ont hello suivant des conditions préalables :

- Windows

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Java SE Runtime Environment version 8 mise à jour 77 ou ultérieure](https://java.com/download/manual.jsp). Ajoutez hello java.exe chemin d’accès toohello système variable d’environnement path. Pour obtenir des instructions de configuration, consultez [comment définir ou modifier la variable système Path hello ?]( https://www.java.com/download/help/path.xml). chemin d’accès Hello est tooC:\Program Files\Java\jdk1.8.0_77\jre\bin similaire.
    - [Kit SDK .NET Core 1.0.3 ou runtime .NET Core 1.1](https://www.microsoft.com/net/download).
    
- Linux (nous recommandons Ubuntu 14.04 LTS)

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx). tooinstall hello code, entrez hello de commande suivante :

              sudo dpkg -i code_<version_number>_amd64.deb

    - [Mono 4.2.x](http://www.mono-project.com/docs/getting-started/install/linux/). 

        - package de deb hello tooupdate source, entrez hello suivant de commandes :

                sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
                echo "deb http://download.mono-project.com/repo/debian wheezy/snapshots 4.2.4.4/main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list
                sudo apt-get update

        - tooinstall Mono, entrez hello de commande suivante :

                sudo apt-get install mono-complete

            > [!NOTE] 
            > Mono 4.6 n’est pas pris en charge. Désinstallez entièrement la version 4.6 avant d’installer la version 4.2.x.  

        - [Java SE Runtime Environment version 8 mise à jour 77 ou ultérieure](https://java.com/download/manual.jsp). Pour obtenir des instructions sur l’installation, consultez hello [des instructions d’installation Linux 64 bits pour Java]( https://java.com/en/download/help/linux_x64_install.xml) page.
        - [Kit SDK .NET Core 1.0.3 ou runtime .NET Core 1.1](https://www.microsoft.com/net/download).
- MacOS

    - [Visual Studio Code]( https://www.visualstudio.com/products/code-vs.aspx).
    - [Mono 4.2.4](http://download.mono-project.com/archive/4.2.4/macos-10-x86/). 
    - [Java SE Runtime Environment version 8 mise à jour 77 ou ultérieure](https://java.com/download/manual.jsp). Pour obtenir des instructions sur l’installation, consultez hello [des instructions d’installation Linux 64 bits pour Java](https://java.com/en/download/help/mac_install.xml) page.
    - [Kit SDK .NET Core 1.0.3 ou runtime .NET Core 1.1](https://www.microsoft.com/net/download).

## <a name="install-data-lake-tools"></a>Installer Data Lake Tools

Après avoir installé les composants requis de hello, vous pouvez installer les outils de LAC de données pour le Code de Visual Studio.

**tooinstall Data Lake Tools**

1. Ouvrez Visual Studio Code.
2. Sélectionnez Ctrl + P et entrez hello de commande suivante :
```
ext install usql-vscode-ext
```
Une liste des extensions de code Visual Studio s’affiche. L’une d’elles est **Azure Data Lake Tools**.

3. Sélectionnez **installer** suivant trop**Azure Data Lake Tools**. Après quelques secondes, hello **installer** bouton modifications trop**recharger**.
4. Sélectionnez **recharger** extension de hello tooactivate.
5. Sélectionnez **OK** tooconfirm. Vous pouvez voir Azure Data Lake Tools Bonjour **Extensions** volet.
    ![Volet Extensions de Data Lake Tools pour Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extensions.png)

## <a name="activate-azure-data-lake-tools"></a>Activer Azure Data Lake Tools
Créer un nouveau fichier .usql ou ouvrir une extension .usql fichier tooactivate hello. 

## <a name="connect-tooazure"></a>Se connecter tooAzure

Avant de pouvoir compiler et exécuter des scripts U-SQL dans Analytique lac de données, vous devez vous connecter tooyour compte Azure.

**tooconnect tooAzure**

1.  Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello. 
2.  Entrez **ADL: Login**. les informations de connexion Hello s’affiche dans hello **sortie** volet.

    ![Palette de commandes de Data Lake Tools pour Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login.png)
    ![Informations de connexion d’appareil Data Lake Tools pour Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-login-info.png)
3. Sélectionnez Ctrl + clic sur l’URL de connexion hello : page de connexion Web https://aka.ms/devicelogin tooopen hello. Entrez le code de hello **G567LX42V** dans la zone de texte hello et sélectionnez **continuer**.

   ![Data Lake Tools pour Visual Studio Code - Coller le code de connexion](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-extension-login-paste-code.png )   
4.  Suivez toosign d’instructions hello dans à partir de la page Web de hello. Lorsque vous êtes connecté, le nom de votre compte Azure s’affiche sur la barre d’état hello dans le coin inférieur gauche de hello Hello **VS Code** fenêtre. 

    > [!NOTE] 
    > Si votre compte a deux facteurs activés, nous vous recommandons d’utiliser l’authentification par téléphone plutôt qu’un code PIN.

toosign, entrez la commande hello **ADL : déconnexion**.

## <a name="list-your-data-lake-analytics-accounts"></a>Répertorier vos comptes Data Lake Analytics

connexion de hello tootest, obtenir une liste de vos comptes Analytique lac de données.

**comptes d’Analytique lac de données toolist hello sous votre abonnement Azure**

1. Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello.
2. Entrez **ADL: List Accounts**. Hello apparaissent dans hello **sortie** volet.

## <a name="open-hello-sample-script"></a>Exemple de script hello ouvert
Ouvrez la palette de commandes hello (Ctrl + Maj + P), puis entrez **ADL : exemple de Script Open**. Une autre instance de cet exemple s’ouvre. Vous pouvez également modifier, configurer et envoyer un script sur cette instance.

## <a name="work-with-u-sql"></a>Utilisation de U-SQL

Vous devez ouvrir un fichier U-SQL ou un dossier toowork avec U-SQL.

**tooopen un dossier pour votre projet U-SQL**

1. À partir du Code Visual Studio, sélectionnez hello **fichier** menu, puis sélectionnez **ouvrir le dossier**.
2. Spécifiez un dossier, puis sélectionnez **Sélectionner le dossier**.
3. Sélectionnez hello **fichier** menu, puis sélectionnez **nouveau**. Un fichier sans titre-1 est ajouté toohello projet.
4. Entrez hello après le code dans le fichier de hello sans titre-1 :

        @departments  = 
            SELECT * FROM 
                (VALUES
                    (31,    "Sales"),
                    (33,    "Engineering"), 
                    (34,    "Clerical"),
                    (35,    "Marketing")
                ) AS 
                      D( DepID, DepName );
         
        OUTPUT @departments
            TO “/Output/departments.csv”

    script de Hello crée un fichier de departments.csv avec des données incluses dans le dossier de Start hello.

5. Enregistrer le fichier hello sous **myUSQL.usql** Bonjour dossier ouvert. Un fichier de configuration adltools_settings.json est également ajouté toohello projet.
4. Ouvrez et configurez adltools_settings.json avec hello propriétés suivantes :

    - Compte : un compte Data Lake Analytics dans votre abonnement Azure.
    - Base de données : une base de données sous votre compte. valeur par défaut Hello est **master**.
    - Schéma : un schéma sous votre base de données. valeur par défaut Hello est **dbo**.
    - Paramètres facultatifs :
        - Priorité : plage de priorité hello est de 1 too1000 avec 1 comme priorité la plus élevée de hello. la valeur par défaut Hello est **1000**.
        - Parallélisme : plage de parallélisme hello est de 1 too150. valeur par défaut de Hello est hello maximal parallélisme autorisé dans votre compte Analytique de LAC de données Azure. 
        
        > [!NOTE] 
        > Si les paramètres hello ne sont pas valides, les valeurs par défaut de hello sont utilisés.

    ![Fichier de configuration de Data Lake Tools pour Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-configuration-file.png)

    Un calcul Analytique lac de données compte est nécessaire toocompile et exécuter les tâches de U-SQL. Vous devez configurer le compte d’ordinateur hello avant de pouvoir compiler et exécuter des travaux U-SQL.
    
Après que la configuration de hello est enregistrée, les informations de compte, de base de données et de schéma hello s’affiche sur la barre d’état hello en hello en bas à gauche du fichier de .usql hello correspondant. 
 
 
Comparés tooopening un fichier, lorsque vous ouvrez un dossier, que vous pouvez :

- Utiliser un fichier code-behind. En mode de fichier unique hello, code-behind n’est pas pris en charge.
- Utiliser un fichier de configuration. Lorsque vous ouvrez un dossier, les scripts hello Bonjour dossier de travail partagent un seul fichier de configuration.


Hello script U-SQL compile à distance via le service de données Lake Analytique de hello. Lorsque vous émettez hello **compiler** hello script U-SQL est envoyé de compte de tooyour Analytique lac de données de la commande. Une version ultérieure, Visual Studio Code reçoit de résultat de la compilation hello. En raison de la compilation à distance de toohello, Code de Visual Studio requiert que vous répertoriez les informations de hello tooconnect tooyour Analytique lac de données de compte dans le fichier de configuration hello.

**script de toocompile U-SQL**

1. Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello. 
2. Entrez **ADL: Compile Script**. Hello compilation résultats s’affichent dans hello **sortie** fenêtre. Vous pouvez également cliquez sur un fichier de script, puis sélectionnez **ADL : Script de compilation** toocompile U-SQL travail. résultat de la compilation Hello s’affiche dans hello **sortie** volet.
 

**script de toosubmit U-SQL**

1. Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello. 
2. Entrez **ADL: Submit Job**.  Vous pouvez également cliquer avec le bouton droit sur un fichier de script, puis sélectionner **ADL: Submit Job**. 

Une fois que vous envoyez un travail U-SQL, les journaux de soumission de hello s’affichent dans hello **sortie** fenêtre dans VS Code. Si l’envoi de hello est réussie, hello travail URL s’affiche également. Vous pouvez ouvrir les URL de tâche hello dans un état de travail en temps réel web navigateur tootrack hello.

sortie de hello tooenable des détails d’une tâche hello, définissez **jobInformationOutputPath** Bonjour **vs code pour hello u-sql_settings.json** fichier.
 
## <a name="use-a-code-behind-file"></a>Utiliser un fichier code-behind

Un fichier code-behind est un fichier C# associé à un script U-SQL. Vous pouvez définir un script dédié tooUDO UDA, UDT et UDF dans le fichier de code-behind hello. Hello UDO, agrégat, UDT et UDF peuvent servir directement dans le script de hello sans tout d’abord l’inscription d’assembly hello. Hello fichier code-behind est placé dans hello même dossier que son fichier de script U-SQL d’homologation. Si le script de hello est nommé xxx.usql, hello code-behind est nommé xxx.usql.cs. Si vous supprimez manuellement le fichier code-behind de hello, fonction de code-behind hello est désactivée pour son script U-SQL associé. Pour plus d’informations sur l’écriture de code client pour le script U-SQL, consultez [Écriture et utilisation de code personnalisé dans U-SQL - Fonctions définies par l’utilisateur]( https://blogs.msdn.microsoft.com/visualstudio/2015/10/28/writing-and-using-custom-code-in-u-sql-user-defined-functions/).

toosupport code-behind, vous devez ouvrir un dossier de travail. 

**toogenerate un fichier code-behind**

1. Ouvrez un fichier source. 
2. Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello.
3. Entrez **ADL: Generate Code Behind**. Un fichier code-behind est créé dans hello même dossier. 

Vous pouvez également cliquer avec le bouton droit sur un fichier de script, puis sélectionner **ADL: Generate Code Behind**. 

toocompile et envoi d’un script U-SQL avec un fichier code-behind est hello identique au fichier de script avec hello autonome U-SQL.

Hello suivant deux captures d’écran affiche un fichier code-behind et son fichier de script U-SQL associé :
 
![Data Lake Tools pour Visual Studio Code - code behind](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind.png)

![Data Lake Tools pour Visual Studio Code - fichier de script code behind](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-code-behind-call.png) 

## <a name="use-assemblies"></a>Utiliser les assemblys

Pour plus d’informations sur le développement d’assemblys, consultez [Développement d’assemblys U-SQL pour les tâches d’Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).

Vous pouvez utiliser Data Lake Tools tooregister assemblys personnalisés dans le catalogue de données Lake Analytique hello.

**tooregister un assembly**

Vous pouvez inscrire assembly hello via hello **ADL : enregistrer l’Assembly** ou **ADL : enregistrer l’Assembly via la Configuration** commandes.

**tooregister via hello ADL : commande d’enregistrer l’Assembly**
1.  Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello.
2.  Entrez **ADL: Register Assembly**. 
3.  Spécifiez le chemin d’accès de hello assembly local. 
4.  Sélectionnez un compte Data Lake Analytics.
5.  Sélectionnez une base de données.

Résultats : portail de hello est ouvert dans un navigateur et affiche le processus d’inscription d’assembly hello.  

Hello de tootrigger un autre moyen pratique **ADL : enregistrer l’Assembly** commande est le fichier clic tooright hello dans l’Explorateur de fichiers. 

**tooregister hello cependant ADL : enregistrer l’Assembly via la commande de Configuration**
1.  Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello.
2.  Entrez **ADL: Register Assembly through Configuration**. 
3.  Spécifiez le chemin d’accès de hello assembly local. 
4.  fichier JSON de Hello s’affiche. Examinez et modifiez les dépendances d’assembly hello et les paramètres de la ressource, si nécessaire. Instructions qui s’affichent dans hello **sortie** fenêtre. tooproceed toohello assembly l’inscription, enregistrez le fichier JSON de hello (Ctrl + S).

![Data Lake Tools pour Visual Studio Code - code behind](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-register-assembly-advance.png)
>[!NOTE]
>- Dépendances d’assembly : détecte automatiquement les Azure Data Lake Tools si hello DLL possède des dépendances. dépendances de Hello sont affichent dans le fichier JSON de hello lorsqu’elles sont détectées. 
>- Ressources : Vous pouvez télécharger vos ressources DLL (par exemple, .txt, .png et .csv) dans le cadre de l’inscription de l’assembly hello. 

Un autre hello tootrigger de façon **ADL : enregistrer l’Assembly via la Configuration** commande est le fichier clic tooright hello dans l’Explorateur de fichiers. 

Hello après U-SQL de code montre comment toocall un assembly. Dans l’exemple hello, nom de l’assembly hello est *test*.

```
REFERENCE ASSEMBLY [test];

@a = 
    EXTRACT 
        Iid int,
    Starts DateTime,
    Region string,
    Query string,
    DwellTime int,
    Results string,
    ClickedUrls string 
    FROM @"Sample/SearchLog.txt" 
    USING Extractors.Tsv();

@d =
    SELECT DISTINCT Region 
    FROM @a;

@d1 = 
    PROCESS @d
    PRODUCE 
        Region string,
    Mkt string
    USING new USQLApplication_codebehind.MyProcessor();

OUTPUT @d1 
    too@"Sample/SearchLogtest.txt" 
    USING Outputters.Tsv();
```


## <a name="access-hello-data-lake-analytics-catalog"></a>Catalogue de données Lake Analytique hello accès

Après que vous être connecté tooAzure, vous pouvez utiliser hello suivant du catalogue des étapes tooaccess hello U-SQL.

**métadonnées de tooaccess hello Analytique de LAC de données Azure**

1.  Sélectionnez Ctrl+Maj+P et entrez **ADL: List Tables**.
2.  Sélectionnez un des comptes de données Lake Analytique hello.
3.  Sélectionnez une des bases de données hello Analytique lac de données.
4.  Sélectionnez un des schémas de hello. Vous pouvez voir la liste hello des tables.

## <a name="view-data-lake-analytics-jobs"></a>Afficher les travaux Data Lake Analytics

**travaux de tooview Analytique lac de données**
1.  Ouvrez la palette de commandes hello (Ctrl + Maj + P), puis sélectionnez **ADL : afficher le travail**. 
2.  Sélectionnez un compte local ou Data Lake Analytics. 
3.  Attendez la liste des travaux hello pour hello compte tooappear.
4.  Sélectionnez une tâche à partir de la liste des travaux, Data Lake Tools ouvre les détails d’une tâche hello Bonjour portail Azure et affiche le fichier de JobInfo hello dans VS Code.

![Data Lake Tools pour Visual Studio Code - Types d’objets IntelliSense](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-show-job.png)

## <a name="azure-data-lake-storage-integration"></a>Intégration d’Azure Data Lake Storage

Vous pouvez utiliser les commandes Azure Data Lake Storage pour :
 - Rechercher les ressources de stockage de LAC de données Azure hello. 
 - Fichier de stockage de LAC de données Azure hello aperçu.  
 - Télécharger hello du fichier directement tooAzure stockage lac de données dans le Code de Visual Studio. 

### <a name="list-hello-storage-path"></a>Chemin d’accès de stockage liste hello 
Vous pouvez afficher le chemin d’accès du stockage hello via la palette de commandes hello ou avec le bouton droit.

**chemin d’accès de stockage de hello toolist via la palette de commandes hello**

1.  Ouvrez la palette de commandes hello (Ctrl + Maj + P), puis entrez **ADL : chemin d’accès de stockage de liste**.

    ![Data Lake Tools pour Visual Studio Code - Répertorier le chemin de stockage](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-storage.png)

2.  Sélectionnez votre meilleur moyen pour répertorier les chemin d’accès de stockage hello. Cette section utilise **Entrer un chemin d’accès** comme exemple.

    ![Data Lake Tools pour Visual Studio Code chemin d’accès de stockage de hello toolist unidirectionnel](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)

    > [!NOTE]
    >- VS Code conserve le chemin d’accès de hello visité en dernier dans chaque compte Analytique lac de données. Par exemple : /tt/ss.
    >- Navigateur à partir du chemin d’accès racine : chemin d’accès de la racine hello liste à partir de votre compte Analytique lac de données sélectionné ou un chemin d’accès local.
    >- Enter a path : indiquez un chemin spécifié à partir de votre compte Data Lake Analytics sélectionné ou un chemin local.
    
3. Sélectionnez un compte à partir de chemin d’accès local de hello ou un compte Analytique lac de données.

    ![Data Lake Tools pour Visual Studio Code - Sélectionner Plus](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4. Sélectionnez **plus** toolist plusieurs comptes d’Analytique lac de données et sélectionnez un compte Analytique lac de données.

    ![Data Lake Tools pour Visual Studio Code - Sélectionner un compte](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

5.  Entrez un chemin de stockage Azure. Par exemple : /output.

    ![Data Lake Tools pour Visual Studio Code - Entrer le chemin de stockage](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-path.png)

6.  Résultats : palette de commandes hello répertorie des informations de chemin d’accès de hello en fonction de vos entrées.

    ![Data Lake Tools pour Visual Studio Code - Répertorier le chemin de stockage, résultats](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-path.png)

Un chemin d’accès relatif de toolist hello est via hello plus pratique d’utiliser avec le bouton droit de menu contextuel.

**Cliquez sur le chemin d’accès de stockage de hello toolist via**

1.  Avec le bouton droit tooselect de chaîne de chemin d’accès hello **chemin d’accès de stockage de liste**.

       ![Data Lake Tools pour Visual Studio Code - Menu contextuel accessible par un clic droit](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-path.png)

2. chemin d’accès relatif Hello sélectionné s’affiche dans la palette de commandes hello.

   ![Data Lake Tools pour Visual Studio Code - Chemin relatif sélectionné](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-relative-path.png)

3.  Sélectionnez un compte à partir de chemin d’accès local de hello ou un compte Analytique lac de données.

       ![Data Lake Tools pour Visual Studio Code - Sélectionner un compte](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

4.  Résultats : palette de commandes hello répertorie les dossiers de hello et des fichiers pour le chemin d’accès actuel de hello.

       ![Outils de LAC de données pour la liste de Code de Visual Studio à partir du chemin d’accès actuel de hello](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-current.png)

### <a name="preview-hello-storage-file"></a>Fichier de stockage hello Preview
Vous pouvez afficher un aperçu des fichiers de stockage hello via la palette de commandes hello ou avec le bouton droit.

**fichier de stockage toopreview hello via la palette de commandes hello**

1.  Ouvrez la palette de commandes hello (Ctrl + Maj + P), puis entrez **ADL : fichier de stockage aperçu**.

       ![Data Lake Tools pour Visual Studio Code - Aperçu du fichier de stockage](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-preview.png)

2.  Sélectionnez un compte à partir de chemin d’accès local de hello ou un compte Analytique lac de données.

       ![Data Lake Tools pour Visual Studio Code - Répertorier un compte](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Sélectionnez **plus** toolist plusieurs comptes d’Analytique lac de données et sélectionnez un compte Analytique lac de données.

       ![Data Lake Tools pour Visual Studio Code - Sélectionner un compte](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-select-adla-account.png)

4.  Entrez un fichier ou chemin de stockage Azure. Par exemple : /output/SearchLog.txt.

       ![Data Lake Tools pour Visual Studio Code - Entrer le fichier et le chemin de stockage](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

5.  Résultats : palette de commandes hello répertorie des informations de chemin d’accès de hello en fonction de vos entrées.

       ![Data Lake Tools pour Visual Studio Code - Aperçu du fichier, résultats](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

**Cliquez sur le chemin d’accès de stockage de hello toolist via**

1.  toopreview un fichier, avec le bouton droit de la CheminAccèsFichier hello.

   ![Data Lake Tools pour Visual Studio Code - Menu contextuel accessible par un clic droit](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-right-click-preview.png) 

2.  Sélectionnez un compte à partir de chemin d’accès local de hello ou un compte Analytique lac de données.

       ![Data Lake Tools pour Visual Studio Code - Sélectionner un compte](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

3.  Résultats : VS Code affiche hello aperçu des résultats pour les fichiers hello.

       ![Data Lake Tools pour Visual Studio Code - Aperçu du fichier, résultats](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-preview-results.png)

### <a name="upload-a-file"></a>Charger un fichier 

Vous pouvez télécharger des fichiers en entrant les commandes hello **ADL : télécharger un fichier** ou **ADL : télécharger un fichier via la Configuration**.

**les fichiers tooupload hello cependant ADL : télécharger un fichier (commande)**
1. Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello ou éditeur de script hello et puis entrez **télécharger le fichier**.
2.  hello de tooupload de fichier, entrez un chemin d’accès local.

    ![Data Lake Tools pour Visual Studio Code - Entrer un chemin local](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-input-local-path.png)

3. Sélectionnez une des façons de hello du chemin d’accès de stockage annonce hello. Cette section utilise **Entrer un chemin d’accès** comme exemple.

    ![Data Lake Tools pour Visual Studio Code - Répertorier le chemin de stockage](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account-selectoneway.png)
    >[!NOTE]
    >- VS Code conserve le chemin d’accès de hello visité en dernier dans chaque compte Analytique lac de données. Par exemple : /tt/ss.
    >- Navigateur à partir du chemin d’accès racine : chemin d’accès de la racine hello liste à partir de votre compte Analytique lac de données sélectionné ou un chemin d’accès local.
    >- Enter a path : indiquez un chemin spécifié à partir de votre compte Data Lake Analytics sélectionné ou un chemin local.

4. Sélectionnez un compte à partir de chemin d’accès local de hello ou un compte Analytique lac de données.

    ![Data Lake Tools pour Visual Studio Code - Stockage accessible par un clic droit](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-list-account.png)

5. Entrez un chemin de stockage Azure. Par exemple : /output.

       ![Data Lake Tools for Visual Studio Code enter storage path](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-input-preview-file.png)

6. Recherchez votre chemin de stockage Azure. Sélectionnez **Choisir le dossier actuel**.

    ![Data Lake Tools pour Visual Studio Code - Sélectionner un dossier](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-choose-current-folder.png)

7.  Résultats : hello **sortie** fenêtre affiche l’état de téléchargement de fichier hello.

       ![Data Lake Tools pour Visual Studio Code - État du chargement](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)    

**les fichiers tooupload hello cependant ADL : télécharger un fichier via la commande de Configuration**
1.  Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello ou éditeur de script hello et puis entrez **télécharger un fichier via la Configuration**.
2.  VS Code affiche un fichier JSON. Vous pouvez entrer des chemins d’accès de fichier et télécharger plusieurs fichiers à hello même temps. Instructions qui s’affichent dans hello **sortie** fenêtre. fichiers de hello tooupload tooproceed, enregistrez le fichier JSON de hello (Ctrl + S).

       ![Chemin de fichier Data Lake Tools pour Visual Studio Code](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-file.png)

3.  Résultats : hello **sortie** fenêtre affiche l’état de téléchargement de fichier hello.

       ![Data Lake Tools pour Visual Studio Code - État du chargement](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-upload-status.png)     

Un autre tooupload de façon hello est un toostorage de fichier avec le bouton droit de menu sur les chemin d’accès complet du fichier hello ou un chemin relatif du fichier hello éditeur de script hello. Entrez le chemin d’accès du fichier local hello, puis sélectionnez le compte hello. Hello **sortie** fenêtre affiche l’état de téléchargement hello. 

### <a name="open-azure-storage-explorer"></a>Ouvrir l’Explorateur de stockage Azure
Vous pouvez ouvrir **Azure Storage Explorer** en entrant la commande hello **ADL : Ouvrez l’Explorateur de stockage Azure Web** ou en le sélectionnant dans le menu contextuel hello.

**tooopen Explorateur de stockage Azure**

1. Sélectionnez la palette de commandes Ctrl + Maj + P tooopen hello.
2. Entrez **ouvrir Explorateur de stockage Azure Web** ou avec le bouton droit sur un chemin d’accès relatif ou un chemin d’accès complet de hello dans l’éditeur de script hello, puis sélectionnez **ouvrir Explorateur de stockage Azure Web**.
3. Sélectionnez un compte Data Lake Analytics.

Outils de LAC de données ouvre le chemin d’accès de stockage Azure hello Bonjour portail Azure. Vous pouvez trouver hello chemin d’accès et aperçu hello le fichier à partir du web de hello.

### <a name="local-run-and-local-debug-for-windows-users"></a>Exécution locale et débogage local pour les utilisateurs de Windows
Exécution locale de U-SQL teste vos données locales et valide votre script localement, avant que votre code soit publié tooData Lake Analytique. Hello débogage local grâce à hello toocomplete vous tâches suivantes avant de votre code est soumis tooData Lake Analytique : 
- Déboguer votre code-behind C# 
- Parcourir le code de hello. 
- Valider votre script localement

Pour obtenir des instructions sur l’exécution locale et le débogage local, consultez [Exécution locale et débogage local U-SQL avec Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).

## <a name="additional-features"></a>Fonctionnalités supplémentaires

Data Lake Tools pour Visual Studio Code prend en charge hello suivant de fonctionnalités :

-   Saisie semi-automatique IntelliSense : des suggestions s’affichent dans des fenêtres indépendantes autour des éléments tels que les mots clés, les méthodes et les variables. Les icônes représentent différents types d’objets de hello :

    - Type de données Scala
    - Type de données complexe
    - Types définis par l’utilisateur (UDT) intégrés
    - Classes et collection .NET
    - Expressions C#
    - UDF, UDO et UDAAG C# intégrés 
    - Fonctions U-SQL
    - Fonction de fenêtrage U-SQL
 
    ![Data Lake Tools pour Visual Studio Code - Types d’objets IntelliSense](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-objects.png)
 
-   IntelliSense de saisie semi-automatique sur les métadonnées des données Lake Analytique : Data Lake Tools télécharge localement des informations de métadonnées Analytique lac de données hello. fonctionnalité IntelliSense de Hello remplit automatiquement les objets, y compris la base de données hello, schéma, table, vue, une fonction table, procédures et c# assemblys, à partir des métadonnées de données Lake Analytique hello.
 
    ![Data Lake Tools pour Visual Studio Code - Métadonnées IntelliSense](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-auto-complete-metastore.png)

-   IntelliSense erroné : Data Lake Tools souligne hello édition d’erreurs pour U-SQL et c#. 
-   Met en surbrillance de syntaxe : Data Lake Tools utilise des éléments de toodifferentiate des couleurs différentes, telles que les variables, les mots clés, les type de données et les fonctions. 

    ![Data Lake Tools pour Visual Studio Code - Points clés de la syntaxe](./media/data-lake-analytics-data-lake-tools-for-vscode/data-lake-tools-for-vscode-syntax-highlights.png)

## <a name="next-steps"></a>Étapes suivantes

- Pour l’exécution locale et le débogage local U-SQL avec Visual Studio Code, consultez [Exécution locale et débogage local U-SQL avec Visual Studio Code](data-lake-tools-for-vscode-local-run-and-debug.md).
- Pour obtenir des informations sur la prise en main de Data Lake Analytics, consultez [Didacticiel : bien démarrer avec Azure Data Lake Analytics](data-lake-analytics-get-started-portal.md).
- Pour obtenir des informations sur l’utilisation de Data Lake Tools pour Visual Studio, consultez [Didacticiel : développer des scripts U-SQL avec Data Lake Tools pour Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
- Pour plus d’informations sur le développement d’assemblys, consultez [Développement d’assemblys U-SQL pour les tâches d’Azure Data Lake Analytics](data-lake-analytics-u-sql-develop-assemblies.md).



