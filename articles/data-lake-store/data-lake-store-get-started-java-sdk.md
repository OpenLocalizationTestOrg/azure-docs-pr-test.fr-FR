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
# <a name="get-started-with-azure-data-lake-store-using-java"></a><span data-ttu-id="c61b7-103">Prise en main d’Azure Data Lake Store à l’aide de Java</span><span class="sxs-lookup"><span data-stu-id="c61b7-103">Get started with Azure Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c61b7-104">Portail</span><span class="sxs-lookup"><span data-stu-id="c61b7-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="c61b7-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c61b7-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="c61b7-106">Kit SDK .NET</span><span class="sxs-lookup"><span data-stu-id="c61b7-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="c61b7-107">Kit SDK Java</span><span class="sxs-lookup"><span data-stu-id="c61b7-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="c61b7-108">API REST</span><span class="sxs-lookup"><span data-stu-id="c61b7-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="c61b7-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c61b7-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="c61b7-110">Node.JS</span><span class="sxs-lookup"><span data-stu-id="c61b7-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="c61b7-111">Python</span><span class="sxs-lookup"><span data-stu-id="c61b7-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="c61b7-112">Découvrez comment toouse hello Azure Data Lake Store Java SDK tooperform des opérations de base telles que créent des dossiers, télécharger et télécharger les fichiers de données, etc.. Pour plus d’informations sur Data Lake, consultez [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c61b7-112">Learn how toouse hello Azure Data Lake Store Java SDK tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="c61b7-113">Vous pouvez accéder à des documents d’API du Kit de développement logiciel Java hello pour Azure Data Lake Store à [docs de l’API Java de Azure Data Lake Store](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span><span class="sxs-lookup"><span data-stu-id="c61b7-113">You can access hello Java SDK API docs for Azure Data Lake Store at [Azure Data Lake Store Java API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c61b7-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c61b7-114">Prerequisites</span></span>
* <span data-ttu-id="c61b7-115">Kit de développement Java (JDK 7 ou version ultérieure, utilisant Java version 1.7 ou ultérieure)</span><span class="sxs-lookup"><span data-stu-id="c61b7-115">Java Development Kit (JDK 7 or higher, using Java version 1.7 or higher)</span></span>
* <span data-ttu-id="c61b7-116">Compte Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c61b7-116">Azure Data Lake Store account.</span></span> <span data-ttu-id="c61b7-117">Suivez les instructions de hello à [prise en main Azure Data Lake Store à l’aide de hello Azure Portal](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c61b7-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="c61b7-118">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="c61b7-118">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="c61b7-119">Ce didacticiel utilise Maven pour les dépendances de build et de projet.</span><span class="sxs-lookup"><span data-stu-id="c61b7-119">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="c61b7-120">Bien qu’il soit possible de toobuild sans utiliser un système de génération comme Maven ou Gradle, assurez-vous de ces systèmes est beaucoup plus faciles dépendances de toomanage.</span><span class="sxs-lookup"><span data-stu-id="c61b7-120">Although it is possible toobuild without using a build system like Maven or Gradle, these systems make is much easier toomanage dependencies.</span></span>
* <span data-ttu-id="c61b7-121">(Facultatif) Et un environnement IDE comme [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) ou [Eclipse](https://www.eclipse.org/downloads/) ou similaire.</span><span class="sxs-lookup"><span data-stu-id="c61b7-121">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="c61b7-122">Comment s’authentifier à l’aide d’Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="c61b7-122">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="c61b7-123">Dans ce didacticiel, nous utilisons un tooretrieve secrète du client d’application Azure AD un jeton d’Azure Active Directory (authentification de service).</span><span class="sxs-lookup"><span data-stu-id="c61b7-123">In this tutorial we use a Azure AD application client secret tooretrieve an Azure Active Directory token (service-to-service authentication).</span></span> <span data-ttu-id="c61b7-124">Nous utilisons ce jeton toocreate un fichier d’opérations Data Lake Store client objet tooperform et les opérations d’annuaire.</span><span class="sxs-lookup"><span data-stu-id="c61b7-124">We use this token toocreate an Data Lake Store client object tooperform operations file and directory operations.</span></span> <span data-ttu-id="c61b7-125">Pour savoir comment tooauthenticate avec Azure Data Lake Store à l’aide hello question secrète du client, nous effectuer hello suivant les étapes principales :</span><span class="sxs-lookup"><span data-stu-id="c61b7-125">For instructions on how tooauthenticate with Azure Data Lake Store using hello client secret, we perform hello following high-level steps:</span></span>

1. <span data-ttu-id="c61b7-126">Créer une application web Azure AD</span><span class="sxs-lookup"><span data-stu-id="c61b7-126">Create an Azure AD web application</span></span>
2. <span data-ttu-id="c61b7-127">Récupérer l’ID de client hello, clé secrète client et le point de terminaison token pour hello application web de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c61b7-127">Retrieve hello client ID, client secret, and token endpoint for hello Azure AD web application.</span></span>
3. <span data-ttu-id="c61b7-128">Configurer l’accès pour l’application web de Azure AD hello sur hello Data Lake Store fichier/dossier tooaccess de hello application Java que vous créez.</span><span class="sxs-lookup"><span data-stu-id="c61b7-128">Configure access for hello Azure AD web application on hello Data Lake Store file/folder that you want tooaccess from hello Java application you are creating.</span></span>

<span data-ttu-id="c61b7-129">Pour obtenir des instructions sur tooperform ces étapes, voir [créer une application Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="c61b7-129">For instructions on how tooperform these steps, see [Create an Active Directory application](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="c61b7-130">Azure Active Directory fournit de qu'autres options ainsi tooretrieve un jeton.</span><span class="sxs-lookup"><span data-stu-id="c61b7-130">Azure Active Directory provides other options as well tooretrieve a token.</span></span> <span data-ttu-id="c61b7-131">Vous pouvez choisir parmi un certain nombre de toosuit de mécanismes d’authentification différents votre scénario, par exemple, une application en cours d’exécution dans un navigateur, une application distribuée en tant qu’une application de bureau ou une application serveur s’exécutent localement ou virtuelle Azure ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c61b7-131">You can pick from a number of different authentication mechanisms toosuit your scenario, for example, an application running in a browser, an application distributed as a desktop application, or a server application running on-premises or in an Azure virtual machine.</span></span> <span data-ttu-id="c61b7-132">Vous pouvez également choisir parmi différents types d’informations d’identification comme des mots de passe, des certificats, l’authentification à 2 facteurs, etc. En outre, Azure Active Directory vous permet de toosynchronize vos utilisateurs d’Active Directory local avec le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="c61b7-132">You can also pick from different types of credentials like passwords, certificates, 2-factor authentication, etc. In addition, Azure Active Directory allows you toosynchronize your on-premises Active Directory users with hello cloud.</span></span> <span data-ttu-id="c61b7-133">Pour plus de détails, consultez [Scénarios d’authentification pour Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="c61b7-133">For details, see [Authentication Scenarios for Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span></span> 

## <a name="create-a-java-application"></a><span data-ttu-id="c61b7-134">Création d’une application Java</span><span class="sxs-lookup"><span data-stu-id="c61b7-134">Create a Java application</span></span>
<span data-ttu-id="c61b7-135">exemple de code Hello disponible [sur GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) vous guide tout au long de hello processus de création de fichiers dans le magasin de hello, concaténation de fichiers, le téléchargement de fichier et supprimer des fichiers dans le magasin de hello.</span><span class="sxs-lookup"><span data-stu-id="c61b7-135">hello code sample available [on GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) walks you through hello process of creating files in hello store, concatenating files, downloading a file, and deleting some files in hello store.</span></span> <span data-ttu-id="c61b7-136">Cette section de hello article vous guide dans parties principales de hello du code de hello.</span><span class="sxs-lookup"><span data-stu-id="c61b7-136">This section of hello article walk you through hello main parts of hello code.</span></span>

1. <span data-ttu-id="c61b7-137">Créez un projet Maven en utilisant [mvn archétype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) de hello de ligne de commande ou à l’aide d’un IDE.</span><span class="sxs-lookup"><span data-stu-id="c61b7-137">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from hello command-line or using an IDE.</span></span> <span data-ttu-id="c61b7-138">Pour savoir comment toocreate Java de projet à l’aide de IntelliJ, consultez [ici](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span><span class="sxs-lookup"><span data-stu-id="c61b7-138">For instructions on how toocreate a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="c61b7-139">Pour obtenir des instructions sur la façon de toocreate un projet à l’aide d’Eclipse, consultez [ici](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span><span class="sxs-lookup"><span data-stu-id="c61b7-139">For instructions on how toocreate a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span> 
2. <span data-ttu-id="c61b7-140">Ajouter hello suivant dépendances tooyour Maven **pom.xml** fichier.</span><span class="sxs-lookup"><span data-stu-id="c61b7-140">Add hello following dependencies tooyour Maven **pom.xml** file.</span></span> <span data-ttu-id="c61b7-141">Ajouter hello suivant extrait de texte entre hello  **\</version >** balise et hello  **\</projet >** balise :</span><span class="sxs-lookup"><span data-stu-id="c61b7-141">Add hello following snippet of text between hello **\</version>** tag and hello **\</project>** tag:</span></span>
   
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
   
    <span data-ttu-id="c61b7-142">dépendance de premier Hello est toouse hello Data Lake Store SDK (`azure-data-lake-store-sdk`) à partir du référentiel de maven hello.</span><span class="sxs-lookup"><span data-stu-id="c61b7-142">hello first dependency is toouse hello Data Lake Store SDK (`azure-data-lake-store-sdk`) from hello maven repository.</span></span> <span data-ttu-id="c61b7-143">Hello deuxième dépendance (`slf4j-nop`) est toospecify le toouse framework de journalisation pour cette application.</span><span class="sxs-lookup"><span data-stu-id="c61b7-143">hello second dependency (`slf4j-nop`) is toospecify which logging framework toouse for this application.</span></span> <span data-ttu-id="c61b7-144">utilise Hello Data Lake Store SDK [slf4j](http://www.slf4j.org/) façade de journalisation, ce qui vous permet de choisir à partir d’un nombre d’infrastructures de journalisation populaires, tels que log4j, Java logging, logback, etc., ou aucun enregistrement.</span><span class="sxs-lookup"><span data-stu-id="c61b7-144">hello Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="c61b7-145">Pour cet exemple, nous désactiver la journalisation, par conséquent, nous utilisons hello **slf4j-nop** liaison.</span><span class="sxs-lookup"><span data-stu-id="c61b7-145">For this example, we will disable logging, hence we use hello **slf4j-nop** binding.</span></span> <span data-ttu-id="c61b7-146">toouse autres options de journalisation dans votre application, consultez [ici](http://www.slf4j.org/manual.html#projectDep).</span><span class="sxs-lookup"><span data-stu-id="c61b7-146">toouse other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

### <a name="add-hello-application-code"></a><span data-ttu-id="c61b7-147">Ajoutez le code de l’application hello</span><span class="sxs-lookup"><span data-stu-id="c61b7-147">Add hello application code</span></span>
<span data-ttu-id="c61b7-148">Il existe trois parties principales toohello code.</span><span class="sxs-lookup"><span data-stu-id="c61b7-148">There are three main parts toohello code.</span></span>

1. <span data-ttu-id="c61b7-149">Obtenir le jeton d’Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="c61b7-149">Obtain hello Azure Active Directory token</span></span>
2. <span data-ttu-id="c61b7-150">Utilisez toocreate de jeton hello un client Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c61b7-150">Use hello token toocreate a Data Lake Store client.</span></span>
3. <span data-ttu-id="c61b7-151">Utilisez des opérations de tooperform client hello Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c61b7-151">Use hello Data Lake Store client tooperform operations.</span></span>

#### <a name="step-1-obtain-an-azure-active-directory-token"></a><span data-ttu-id="c61b7-152">Étape 1 : Obtenir un jeton Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c61b7-152">Step 1: Obtain an Azure Active Directory token.</span></span>
<span data-ttu-id="c61b7-153">Hello Data Lake Store SDK fournit des méthodes utiles qui vous permettent de gérer les jetons de sécurité hello requise tootalk toohello compte Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c61b7-153">hello Data Lake Store SDK provides convenient methods that let you manage hello security tokens needed tootalk toohello Data Lake Store account.</span></span> <span data-ttu-id="c61b7-154">Toutefois, hello SDK n’impose pas qu’uniquement ces méthodes est utilisée.</span><span class="sxs-lookup"><span data-stu-id="c61b7-154">However, hello SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="c61b7-155">Vous pouvez utiliser tout autre moyen d’obtenir le jeton, comme à l’aide de hello [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), ou votre propre code personnalisé.</span><span class="sxs-lookup"><span data-stu-id="c61b7-155">You can use any other means of obtaining token as well, like using hello [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

<span data-ttu-id="c61b7-156">toouse hello jeton tooobtain Data Lake Store SDK hello Active Directory application Web vous créée précédemment, utilisez une des sous-classes de hello de `AccessTokenProvider` (exemple hello ci-dessous utilise `ClientCredsTokenProvider`).</span><span class="sxs-lookup"><span data-stu-id="c61b7-156">toouse hello Data Lake Store SDK tooobtain token for hello Active Directory Web application you created earlier, use one of hello subclasses of `AccessTokenProvider` (hello example below uses `ClientCredsTokenProvider`).</span></span> <span data-ttu-id="c61b7-157">Hello fournisseur de jetons caches hello creds utilisé le jeton de hello tooobtain en mémoire et renouvelle automatiquement le jeton de hello s’il s’agit sur tooexpire.</span><span class="sxs-lookup"><span data-stu-id="c61b7-157">hello token provider caches hello creds used tooobtain hello token in memory, and automatically renews hello token if it is about tooexpire.</span></span> <span data-ttu-id="c61b7-158">Il est possible de toocreate aux sous-classes de `AccessTokenProvider` jetons sont obtenus par votre code client, mais pour l’instant nous allons simplement utiliser hello celui fourni dans hello SDK.</span><span class="sxs-lookup"><span data-stu-id="c61b7-158">It is possible toocreate your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code, but for now let's just use hello one provided in hello SDK.</span></span>

<span data-ttu-id="c61b7-159">Remplacez **remplissage en ici** par des valeurs réelles de hello pour hello application Azure Active Directory Web.</span><span class="sxs-lookup"><span data-stu-id="c61b7-159">Replace **FILL-IN-HERE** with hello actual values for hello Azure Active Directory Web application.</span></span>

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a><span data-ttu-id="c61b7-160">Étape 2 : Créer un objet (ADLStoreClient) de client Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c61b7-160">Step 2: Create an Azure Data Lake Store client (ADLStoreClient) object</span></span>
<span data-ttu-id="c61b7-161">Création d’un [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) objet nécessite un toospecify hello Data Lake Store compte hello et nom de fournisseur de jetons générés à l’étape de dernière hello.</span><span class="sxs-lookup"><span data-stu-id="c61b7-161">Creating an [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object requires you toospecify hello Data Lake Store account name and hello token provider you generated in hello last step.</span></span> <span data-ttu-id="c61b7-162">Notez que hello compte Data Lake Store nom doit toobe un nom de domaine complet.</span><span class="sxs-lookup"><span data-stu-id="c61b7-162">Note that hello Data Lake Store account name needs toobe a fully qualified domain name.</span></span> <span data-ttu-id="c61b7-163">Par exemple, remplacez **FILL-IN-HERE** (à remplir) par quelque chose comme **mydatalakestore.azuredatalakestore.net**.</span><span class="sxs-lookup"><span data-stu-id="c61b7-163">For example, replace **FILL-IN-HERE** with something like **mydatalakestore.azuredatalakestore.net**.</span></span>

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a><span data-ttu-id="c61b7-164">Étape 3 : Utiliser des opérations de fichier et Active la tooperform des ADLStoreClient hello</span><span class="sxs-lookup"><span data-stu-id="c61b7-164">Step 3: Use hello ADLStoreClient tooperform file and directory operations</span></span>
<span data-ttu-id="c61b7-165">code Hello ci-dessous contient des extraits de code exemple de certaines opérations courantes.</span><span class="sxs-lookup"><span data-stu-id="c61b7-165">hello code below contains example snippets of some common operations.</span></span> <span data-ttu-id="c61b7-166">Vous pouvez examiner hello complète [docs de l’API de kit de développement logiciel Java Data Lake Store](https://azure.github.io/azure-data-lake-store-java/javadoc/) Hello **ADLStoreClient** toosee autres opérations de l’objet.</span><span class="sxs-lookup"><span data-stu-id="c61b7-166">You can look at hello full [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) of hello **ADLStoreClient** object toosee other operations.</span></span>

<span data-ttu-id="c61b7-167">Notez que les fichiers sont lus et écrits en utilisant des flux Java standard.</span><span class="sxs-lookup"><span data-stu-id="c61b7-167">Note that files are read from and written into using standard Java streams.</span></span> <span data-ttu-id="c61b7-168">Cela signifie que vous pouvez superposer des flux de Java hello par-dessus hello que Data Lake Store flux toobenefit de standard (par exemple, Print flux pour la sortie mise en forme ou l’un des flux de compression ou chiffrement hello pour des fonctionnalités supplémentaires sur la fonctionnalité de Java haut, etc.).</span><span class="sxs-lookup"><span data-stu-id="c61b7-168">This means that you can layer any of hello Java streams on top of hello Data Lake Store streams toobenefit from standard Java functionality (e.g., Print streams for formatted output, or any of hello compression or encryption streams for additional functionality on top, etc.).</span></span>

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

#### <a name="step-4-build-and-run-hello-application"></a><span data-ttu-id="c61b7-169">Étape 4 : Créer et exécuter l’application hello</span><span class="sxs-lookup"><span data-stu-id="c61b7-169">Step 4: Build and run hello application</span></span>
1. <span data-ttu-id="c61b7-170">toorun à partir d’un bus IDE, recherchez et appuyez sur hello **exécuter** bouton.</span><span class="sxs-lookup"><span data-stu-id="c61b7-170">toorun from within an IDE, locate and press hello **Run** button.</span></span> <span data-ttu-id="c61b7-171">toorun à partir de Maven, utilisez [exec : exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span><span class="sxs-lookup"><span data-stu-id="c61b7-171">toorun from Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span></span>
2. <span data-ttu-id="c61b7-172">tooproduce fichier jar autonome que vous pouvez exécuter à partir de la ligne de commande build hello jar avec toutes les dépendances sont inclus, à l’aide de hello [plug-in de Maven assembly](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span><span class="sxs-lookup"><span data-stu-id="c61b7-172">tooproduce a standalone jar that you can run from command-line build hello jar with all dependencies included, using hello [Maven assembly plugin](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span></span> <span data-ttu-id="c61b7-173">Hello pom.xml Bonjour [exemple de code source sur github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) contient un exemple de procédure toodo cela.</span><span class="sxs-lookup"><span data-stu-id="c61b7-173">hello pom.xml in hello [example source code on github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) has an example of how toodo this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c61b7-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c61b7-174">Next steps</span></span>
* [<span data-ttu-id="c61b7-175">Explorer les JavaDoc pour hello Kit de développement logiciel Java</span><span class="sxs-lookup"><span data-stu-id="c61b7-175">Explore JavaDoc for hello Java SDK</span></span>](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [<span data-ttu-id="c61b7-176">Sécuriser les données dans Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c61b7-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="c61b7-177">Utiliser Azure Data Lake Analytics avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c61b7-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="c61b7-178">Utiliser Azure HDInsight avec Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c61b7-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

