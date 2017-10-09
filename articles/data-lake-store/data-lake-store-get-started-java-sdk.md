---
title: "les applications de toodevelop du Kit de développement logiciel Java aaaUse hello dans Azure Data Lake Store | Documents Microsoft"
description: "Utilisez le SDK Java magasin Azure Data Lake toocreate un compte Data Lake Store et effectuer des opérations de base Bonjour Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d10e09db-5232-4e84-bb50-52efc2c21887
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/28/2017
ms.author: nitinme
ms.openlocfilehash: d3bcee449c2a2a4bd2f7b241af46ecc010b6b62e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a>Prise en main d’Azure Data Lake Store à l’aide de Java
> [!div class="op_single_selector"]
> * [Portail](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Kit SDK .NET](data-lake-store-get-started-net-sdk.md)
> * [Kit SDK Java](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.JS](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

Découvrez comment toouse hello Azure Data Lake Store Java SDK tooperform des opérations de base telles que créent des dossiers, télécharger et télécharger les fichiers de données, etc.. Pour plus d’informations sur Data Lake, consultez [Azure Data Lake Store](data-lake-store-overview.md).

Vous pouvez accéder à des documents d’API du Kit de développement logiciel Java hello pour Azure Data Lake Store à [docs de l’API Java de Azure Data Lake Store](https://azure.github.io/azure-data-lake-store-java/javadoc/).

## <a name="prerequisites"></a>Composants requis
* Kit de développement Java (JDK 7 ou version ultérieure, utilisant Java version 1.7 ou ultérieure)
* Compte Azure Data Lake Store. Suivez les instructions de hello à [prise en main Azure Data Lake Store à l’aide de hello Azure Portal](data-lake-store-get-started-portal.md).
* [Maven](https://maven.apache.org/install.html). Ce didacticiel utilise Maven pour les dépendances de build et de projet. Bien qu’il soit possible de toobuild sans utiliser un système de génération comme Maven ou Gradle, assurez-vous de ces systèmes est beaucoup plus faciles dépendances de toomanage.
* (Facultatif) Et un environnement IDE comme [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) ou [Eclipse](https://www.eclipse.org/downloads/) ou similaire.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>Comment s’authentifier à l’aide d’Azure Active Directory ?
Dans ce didacticiel, nous utilisons un tooretrieve secrète du client d’application Azure AD un jeton d’Azure Active Directory (authentification de service). Nous utilisons ce jeton toocreate un fichier d’opérations Data Lake Store client objet tooperform et les opérations d’annuaire. Pour savoir comment tooauthenticate avec Azure Data Lake Store à l’aide hello question secrète du client, nous effectuer hello suivant les étapes principales :

1. Créer une application web Azure AD
2. Récupérer l’ID de client hello, clé secrète client et le point de terminaison token pour hello application web de Azure AD.
3. Configurer l’accès pour l’application web de Azure AD hello sur hello Data Lake Store fichier/dossier tooaccess de hello application Java que vous créez.

Pour obtenir des instructions sur tooperform ces étapes, voir [créer une application Active Directory](data-lake-store-authenticate-using-active-directory.md).

Azure Active Directory fournit de qu'autres options ainsi tooretrieve un jeton. Vous pouvez choisir parmi un certain nombre de toosuit de mécanismes d’authentification différents votre scénario, par exemple, une application en cours d’exécution dans un navigateur, une application distribuée en tant qu’une application de bureau ou une application serveur s’exécutent localement ou virtuelle Azure ordinateur. Vous pouvez également choisir parmi différents types d’informations d’identification comme des mots de passe, des certificats, l’authentification à 2 facteurs, etc. En outre, Azure Active Directory vous permet de toosynchronize vos utilisateurs d’Active Directory local avec le cloud de hello. Pour plus de détails, consultez [Scénarios d’authentification pour Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md). 

## <a name="create-a-java-application"></a>Création d’une application Java
exemple de code Hello disponible [sur GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) vous guide tout au long de hello processus de création de fichiers dans le magasin de hello, concaténation de fichiers, le téléchargement de fichier et supprimer des fichiers dans le magasin de hello. Cette section de hello article vous guide dans parties principales de hello du code de hello.

1. Créez un projet Maven en utilisant [mvn archétype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) de hello de ligne de commande ou à l’aide d’un IDE. Pour savoir comment toocreate Java de projet à l’aide de IntelliJ, consultez [ici](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html). Pour obtenir des instructions sur la façon de toocreate un projet à l’aide d’Eclipse, consultez [ici](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm). 
2. Ajouter hello suivant dépendances tooyour Maven **pom.xml** fichier. Ajouter hello suivant extrait de texte entre hello  **\</version >** balise et hello  **\</projet >** balise :
   
        <dependencies>
          <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-data-lake-store-sdk</artifactId>
            <version>2.1.5</version>
          </dependency>
          <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-nop</artifactId>
            <version>1.7.21</version>
          </dependency>
        </dependencies>
   
    dépendance de premier Hello est toouse hello Data Lake Store SDK (`azure-data-lake-store-sdk`) à partir du référentiel de maven hello. Hello deuxième dépendance (`slf4j-nop`) est toospecify le toouse framework de journalisation pour cette application. utilise Hello Data Lake Store SDK [slf4j](http://www.slf4j.org/) façade de journalisation, ce qui vous permet de choisir à partir d’un nombre d’infrastructures de journalisation populaires, tels que log4j, Java logging, logback, etc., ou aucun enregistrement. Pour cet exemple, nous désactiver la journalisation, par conséquent, nous utilisons hello **slf4j-nop** liaison. toouse autres options de journalisation dans votre application, consultez [ici](http://www.slf4j.org/manual.html#projectDep).

### <a name="add-hello-application-code"></a>Ajoutez le code de l’application hello
Il existe trois parties principales toohello code.

1. Obtenir le jeton d’Azure Active Directory hello
2. Utilisez toocreate de jeton hello un client Data Lake Store.
3. Utilisez des opérations de tooperform client hello Data Lake Store.

#### <a name="step-1-obtain-an-azure-active-directory-token"></a>Étape 1 : Obtenir un jeton Azure Active Directory.
Hello Data Lake Store SDK fournit des méthodes utiles qui vous permettent de gérer les jetons de sécurité hello requise tootalk toohello compte Data Lake Store. Toutefois, hello SDK n’impose pas qu’uniquement ces méthodes est utilisée. Vous pouvez utiliser tout autre moyen d’obtenir le jeton, comme à l’aide de hello [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), ou votre propre code personnalisé.

toouse hello jeton tooobtain Data Lake Store SDK hello Active Directory application Web vous créée précédemment, utilisez une des sous-classes de hello de `AccessTokenProvider` (exemple hello ci-dessous utilise `ClientCredsTokenProvider`). Hello fournisseur de jetons caches hello creds utilisé le jeton de hello tooobtain en mémoire et renouvelle automatiquement le jeton de hello s’il s’agit sur tooexpire. Il est possible de toocreate aux sous-classes de `AccessTokenProvider` jetons sont obtenus par votre code client, mais pour l’instant nous allons simplement utiliser hello celui fourni dans hello SDK.

Remplacez **remplissage en ici** par des valeurs réelles de hello pour hello application Azure Active Directory Web.

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a>Étape 2 : Créer un objet (ADLStoreClient) de client Azure Data Lake Store
Création d’un [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) objet nécessite un toospecify hello Data Lake Store compte hello et nom de fournisseur de jetons générés à l’étape de dernière hello. Notez que hello compte Data Lake Store nom doit toobe un nom de domaine complet. Par exemple, remplacez **FILL-IN-HERE** (à remplir) par quelque chose comme **mydatalakestore.azuredatalakestore.net**.

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a>Étape 3 : Utiliser des opérations de fichier et Active la tooperform des ADLStoreClient hello
code Hello ci-dessous contient des extraits de code exemple de certaines opérations courantes. Vous pouvez examiner hello complète [docs de l’API de kit de développement logiciel Java Data Lake Store](https://azure.github.io/azure-data-lake-store-java/javadoc/) Hello **ADLStoreClient** toosee autres opérations de l’objet.

Notez que les fichiers sont lus et écrits en utilisant des flux Java standard. Cela signifie que vous pouvez superposer des flux de Java hello par-dessus hello que Data Lake Store flux toobenefit de standard (par exemple, Print flux pour la sortie mise en forme ou l’un des flux de compression ou chiffrement hello pour des fonctionnalités supplémentaires sur la fonctionnalité de Java haut, etc.).

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is hello same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append toofile
    stream = client.getAppendStream(filename);
    stream.write(getSampleContent());
    stream.close();

    // Read File
    InputStream in = client.getReadStream(filename);
    byte[] b = new byte[64000];
    while (in.read(b) != -1) {
        System.out.write(b);
    }
    in.close();

    // concatenate hello two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename hello file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all hello subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-hello-application"></a>Étape 4 : Créer et exécuter l’application hello
1. toorun à partir d’un bus IDE, recherchez et appuyez sur hello **exécuter** bouton. toorun à partir de Maven, utilisez [exec : exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).
2. tooproduce fichier jar autonome que vous pouvez exécuter à partir de la ligne de commande build hello jar avec toutes les dépendances sont inclus, à l’aide de hello [plug-in de Maven assembly](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html). Hello pom.xml Bonjour [exemple de code source sur github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) contient un exemple de procédure toodo cela.

## <a name="next-steps"></a>Étapes suivantes
* [Explorer les JavaDoc pour hello Kit de développement logiciel Java](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [Sécuriser les données dans Data Lake Store](data-lake-store-secure-data.md)
* [Utiliser Azure Data Lake Analytics avec Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Utiliser Azure HDInsight avec Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

