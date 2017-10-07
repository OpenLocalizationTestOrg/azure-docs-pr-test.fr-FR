---
title: aaaJava fonction utilisateur (UDF) avec Hive dans HDInsight - Azure | Documents Microsoft
description: "Découvrez comment toocreate basé sur un Java défini par l’utilisateur (fonction) (UDF) qui fonctionne avec la ruche. Cet exemple UDF convertit un tableau de toolowercase des chaînes de texte."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 8d4f8efe-2f01-4a61-8619-651e873c7982
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 392b4cfb73299d2f6c1e8e825a4201b48d501388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a><span data-ttu-id="7036d-104">Utiliser une fonction UDF Java avec Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="7036d-104">Use a Java UDF with Hive in HDInsight</span></span>

<span data-ttu-id="7036d-105">Découvrez comment toocreate basé sur un Java défini par l’utilisateur (fonction) (UDF) qui fonctionne avec la ruche.</span><span class="sxs-lookup"><span data-stu-id="7036d-105">Learn how toocreate a Java-based user-defined function (UDF) that works with Hive.</span></span> <span data-ttu-id="7036d-106">Hello Java UDF dans cet exemple convertit un tableau de chaînes tooall-minuscules des caractères de texte.</span><span class="sxs-lookup"><span data-stu-id="7036d-106">hello Java UDF in this example converts a table of text strings tooall-lowercase characters.</span></span>

## <a name="requirements"></a><span data-ttu-id="7036d-107">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="7036d-107">Requirements</span></span>

* <span data-ttu-id="7036d-108">Un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="7036d-108">An HDInsight cluster</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="7036d-109">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="7036d-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7036d-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7036d-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

    <span data-ttu-id="7036d-111">La plupart des étapes de ce document fonctionnent sur les deux clusters basés sur Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="7036d-111">Most steps in this document work on both Windows- and Linux-based clusters.</span></span> <span data-ttu-id="7036d-112">Toutefois, hello étapes utilisées tooupload hello compilée cluster de toohello UDF et exécuter sont des clusters tooLinux spécifiques.</span><span class="sxs-lookup"><span data-stu-id="7036d-112">However, hello steps used tooupload hello compiled UDF toohello cluster and run it are specific tooLinux-based clusters.</span></span> <span data-ttu-id="7036d-113">Des liens sont fournis tooinformation qui peut être utilisée avec des clusters basés sur Windows.</span><span class="sxs-lookup"><span data-stu-id="7036d-113">Links are provided tooinformation that can be used with Windows-based clusters.</span></span>

* <span data-ttu-id="7036d-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 ou ultérieur (ou un équivalent, par exemple, OpenJDK)</span><span class="sxs-lookup"><span data-stu-id="7036d-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)</span></span>

* [<span data-ttu-id="7036d-115">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="7036d-115">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="7036d-116">Un éditeur de texte ou un IDE Java</span><span class="sxs-lookup"><span data-stu-id="7036d-116">A text editor or Java IDE</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7036d-117">Si vous créez des fichiers de Python sur un client Windows hello, vous devez utiliser un éditeur qui utilise le saut de ligne comme une fin de ligne.</span><span class="sxs-lookup"><span data-stu-id="7036d-117">If you create hello Python files on a Windows client, you must use an editor that uses LF as a line ending.</span></span> <span data-ttu-id="7036d-118">Si vous n’êtes pas sûr que votre éditeur utilise LF ou CRLF, consultez hello [dépannage](#troubleshooting) section pour les étapes de suppression hello caractère de retour chariot.</span><span class="sxs-lookup"><span data-stu-id="7036d-118">If you are not sure whether your editor uses LF or CRLF, see hello [Troubleshooting](#troubleshooting) section for steps on removing hello CR character.</span></span>

## <a name="create-an-example-java-udf"></a><span data-ttu-id="7036d-119">Créer un exemple Java UDF</span><span class="sxs-lookup"><span data-stu-id="7036d-119">Create an example Java UDF</span></span> 

1. <span data-ttu-id="7036d-120">À partir d’une ligne de commande, utilisez hello suivant toocreate un nouveau projet Maven :</span><span class="sxs-lookup"><span data-stu-id="7036d-120">From a command line, use hello following toocreate a new Maven project:</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > <span data-ttu-id="7036d-121">Si vous utilisez PowerShell, vous devez placer entre guillemets les paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="7036d-121">If you are using PowerShell, you must put quotes around hello parameters.</span></span> <span data-ttu-id="7036d-122">Par exemple, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span><span class="sxs-lookup"><span data-stu-id="7036d-122">For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span></span>

    <span data-ttu-id="7036d-123">Cette commande crée un répertoire nommé **exampleudf**, qui contient le projet de Maven hello.</span><span class="sxs-lookup"><span data-stu-id="7036d-123">This command creates a directory named **exampleudf**, which contains hello Maven project.</span></span>

2. <span data-ttu-id="7036d-124">Une fois le projet de hello a été créé, supprimez hello **exampleudf/src/test** active a été créée dans le cadre du projet de hello.</span><span class="sxs-lookup"><span data-stu-id="7036d-124">Once hello project has been created, delete hello **exampleudf/src/test** directory that was created as part of hello project.</span></span>

3. <span data-ttu-id="7036d-125">Ouvrez hello **exampleudf/pom.xml**et remplacer hello `<dependencies>` entrée par hello XML suivant :</span><span class="sxs-lookup"><span data-stu-id="7036d-125">Open hello **exampleudf/pom.xml**, and replace hello existing `<dependencies>` entry with hello following XML:</span></span>

    ```xml
    <dependencies>
        <dependency>
            <groupId>org.apache.hadoop</groupId>
            <artifactId>hadoop-client</artifactId>
            <version>2.7.3</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.hive</groupId>
            <artifactId>hive-exec</artifactId>
            <version>1.2.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>
    ```

    <span data-ttu-id="7036d-126">Ces entrées spécifient la version de hello de Hadoop et Hive inclus avec HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="7036d-126">These entries specify hello version of Hadoop and Hive included with HDInsight 3.5.</span></span> <span data-ttu-id="7036d-127">Vous trouverez des informations sur les versions de hello de Hadoop et Hive fourni avec HDInsight à partir de hello [le contrôle de version HDInsight composant](hdinsight-component-versioning.md) document.</span><span class="sxs-lookup"><span data-stu-id="7036d-127">You can find information on hello versions of Hadoop and Hive provided with HDInsight from hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

    <span data-ttu-id="7036d-128">Ajouter un `<build>` section avant hello `</project>` ligne à la fin de hello du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="7036d-128">Add a `<build>` section before hello `</project>` line at hello end of hello file.</span></span> <span data-ttu-id="7036d-129">Cette section doit contenir hello XML suivant :</span><span class="sxs-lookup"><span data-stu-id="7036d-129">This section should contain hello following XML:</span></span>

    ```xml
    <build>
        <plugins>
            <!-- build for Java 1.8. This is required by HDInsight 3.5  -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.3</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                </configuration>
            </plugin>
            <!-- build an uber jar -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-shade-plugin</artifactId>
                <version>2.3</version>
                <configuration>
                    <!-- Keep us from getting a can't overwrite file error -->
                    <transformers>
                        <transformer
                                implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                        </transformer>
                        <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer">
                        </transformer>
                    </transformers>
                    <!-- Keep us from getting a bad signature error -->
                    <filters>
                        <filter>
                            <artifact>*:*</artifact>
                            <excludes>
                                <exclude>META-INF/*.SF</exclude>
                                <exclude>META-INF/*.DSA</exclude>
                                <exclude>META-INF/*.RSA</exclude>
                            </excludes>
                        </filter>
                    </filters>
                </configuration>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>shade</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
    ```

    <span data-ttu-id="7036d-130">Ces entrées définissent comment toobuild hello projet.</span><span class="sxs-lookup"><span data-stu-id="7036d-130">These entries define how toobuild hello project.</span></span> <span data-ttu-id="7036d-131">Plus précisément, les version hello de Java qui hello projet utilise et comment toobuild un uberjar pour cluster toohello de déploiement.</span><span class="sxs-lookup"><span data-stu-id="7036d-131">Specifically, hello version of Java that hello project uses and how toobuild an uberjar for deployment toohello cluster.</span></span>

    <span data-ttu-id="7036d-132">Enregistrer le fichier de hello une fois hello modifications ont été apportées.</span><span class="sxs-lookup"><span data-stu-id="7036d-132">Save hello file once hello changes have been made.</span></span>

4. <span data-ttu-id="7036d-133">Renommer **exampleudf/src/main/java/com/microsoft/examples/App.java** trop**ExampleUDF.java**, puis ouvrez le fichier de hello dans votre éditeur.</span><span class="sxs-lookup"><span data-stu-id="7036d-133">Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** too**ExampleUDF.java**, and then open hello file in your editor.</span></span>

5. <span data-ttu-id="7036d-134">Remplacez le contenu hello Hello **ExampleUDF.java** de fichiers avec les éléments suivants de hello, puis enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="7036d-134">Replace hello contents of hello **ExampleUDF.java** file with hello following, then save hello file.</span></span>

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of hello UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of hello input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If hello value is null, return a null
            if(input == null)
                return null;
            // Lowercase hello input string and return it
            return input.toLowerCase();
        }
    }
    ```

    <span data-ttu-id="7036d-135">Ce code implémente une fonction qui accepte une valeur de chaîne et retourne une version en minuscules d’hello.</span><span class="sxs-lookup"><span data-stu-id="7036d-135">This code implements a UDF that accepts a string value, and returns a lowercase version of hello string.</span></span>

## <a name="build-and-install-hello-udf"></a><span data-ttu-id="7036d-136">Générer et installer hello UDF</span><span class="sxs-lookup"><span data-stu-id="7036d-136">Build and install hello UDF</span></span>

1. <span data-ttu-id="7036d-137">Utilisez hello suivant commande toocompile et hello UDF de package :</span><span class="sxs-lookup"><span data-stu-id="7036d-137">Use hello following command toocompile and package hello UDF:</span></span>

    ```bash
    mvn compile package
    ```

    <span data-ttu-id="7036d-138">Cette commande génère et packages hello UDF dans hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` fichier.</span><span class="sxs-lookup"><span data-stu-id="7036d-138">This command builds and packages hello UDF into hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span></span>

2. <span data-ttu-id="7036d-139">Hello d’utilisation `scp` commande toocopy hello toohello HDInsight de fichiers.</span><span class="sxs-lookup"><span data-stu-id="7036d-139">Use hello `scp` command toocopy hello file toohello HDInsight cluster.</span></span>

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    <span data-ttu-id="7036d-140">Remplacez `myuser` par hello compte d’utilisateur SSH pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="7036d-140">Replace `myuser` with hello SSH user account for your cluster.</span></span> <span data-ttu-id="7036d-141">Remplacez `mycluster` avec le nom du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7036d-141">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="7036d-142">Si vous avez utilisé un Bonjour toosecure de mot de passe SSH compte, vous êtes un mot de passe hello tooenter demandées.</span><span class="sxs-lookup"><span data-stu-id="7036d-142">If you used a password toosecure hello SSH account, you are prompted tooenter hello password.</span></span> <span data-ttu-id="7036d-143">Si vous avez utilisé un certificat, vous devrez peut-être toouse hello `-i` fichier clé privée de paramètre toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="7036d-143">If you used a certificate, you may need toouse hello `-i` parameter toospecify hello private key file.</span></span>

3. <span data-ttu-id="7036d-144">Connectez le cluster toohello à l’aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="7036d-144">Connect toohello cluster using SSH.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="7036d-145">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7036d-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

4. <span data-ttu-id="7036d-146">À partir de la session SSH hello, copiez tooHDInsight stockage hello jar.</span><span class="sxs-lookup"><span data-stu-id="7036d-146">From hello SSH session, copy hello jar file tooHDInsight storage.</span></span>

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a><span data-ttu-id="7036d-147">Utilisez hello UDF à partir de la ruche</span><span class="sxs-lookup"><span data-stu-id="7036d-147">Use hello UDF from Hive</span></span>

1. <span data-ttu-id="7036d-148">Utilisez hello suivant du client de Beeline hello toostart à partir de la session SSH hello.</span><span class="sxs-lookup"><span data-stu-id="7036d-148">Use hello following toostart hello Beeline client from hello SSH session.</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="7036d-149">Cette commande suppose que vous avez utilisé par défaut hello **admin** hello compte de connexion pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="7036d-149">This command assumes that you used hello default of **admin** for hello login account for your cluster.</span></span>

2. <span data-ttu-id="7036d-150">Une fois que vous êtes parvenu à hello `jdbc:hive2://localhost:10001/>` invite, entrez hello suivant tooadd hello UDF tooHive et l’exposer en tant que fonction.</span><span class="sxs-lookup"><span data-stu-id="7036d-150">Once you arrive at hello `jdbc:hive2://localhost:10001/>` prompt, enter hello following tooadd hello UDF tooHive and expose it as a function.</span></span>

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > <span data-ttu-id="7036d-151">Cet exemple suppose que le stockage Azure est le stockage par défaut pour le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="7036d-151">This example assumes that Azure Storage is default storage for hello cluster.</span></span> <span data-ttu-id="7036d-152">Si votre cluster utilise Data Lake Store au lieu de cela, modifiez hello `wasb:///` valeur trop`adl:///`.</span><span class="sxs-lookup"><span data-stu-id="7036d-152">If your cluster uses Data Lake Store instead, change hello `wasb:///` value too`adl:///`.</span></span>

3. <span data-ttu-id="7036d-153">Utilisez hello UDF tooconvert valeurs récupérées à partir d’une table toolower casse des chaînes.</span><span class="sxs-lookup"><span data-stu-id="7036d-153">Use hello UDF tooconvert values retrieved from a table toolower case strings.</span></span>

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    <span data-ttu-id="7036d-154">Cette requête sélectionne hello plateforme d’appareil (Android, Windows, iOS, etc.) à partir de la table de hello, convertir en cas de toolower chaîne hello, puis les afficher.</span><span class="sxs-lookup"><span data-stu-id="7036d-154">This query selects hello device platform (Android, Windows, iOS, etc.) from hello table, convert hello string toolower case, and then display them.</span></span> <span data-ttu-id="7036d-155">sortie de Hello apparaît toohello similaire après le texte :</span><span class="sxs-lookup"><span data-stu-id="7036d-155">hello output appears similar toohello following text:</span></span>

        +----------+--+
        |   _c0    |
        +----------+--+
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        | android  |
        +----------+--+

## <a name="next-steps"></a><span data-ttu-id="7036d-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7036d-156">Next steps</span></span>

<span data-ttu-id="7036d-157">Pour les autres toowork manières avec Hive, consultez [utilisez Hive hdinsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="7036d-157">For other ways toowork with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="7036d-158">Pour plus d’informations sur les fonctions de Hive User-Defined, consultez [Hive les opérateurs et les fonctions définies par l’utilisateur](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section de wiki de ruche hello sur le site apache.org.</span><span class="sxs-lookup"><span data-stu-id="7036d-158">For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of hello Hive wiki at apache.org.</span></span>
