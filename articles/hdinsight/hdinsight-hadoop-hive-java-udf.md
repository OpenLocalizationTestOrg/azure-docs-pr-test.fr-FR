---
title: "Fonction définie par l’utilisateur (UDF) de Java avec Hive dans HDInsight - Azure | Documents Microsoft"
description: "Découvrez comment créer une fonction définie par l’utilisateur basée sur Java qui fonctionne avec Hive. Cet exemple UDF convertit un tableau de chaînes de texte en minuscules."
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
ms.openlocfilehash: 481d234eaf88bdb210821084ee4154159470eda0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a><span data-ttu-id="7a16b-104">Utiliser une fonction UDF Java avec Hive dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="7a16b-104">Use a Java UDF with Hive in HDInsight</span></span>

<span data-ttu-id="7a16b-105">Découvrez comment créer une fonction définie par l’utilisateur basée sur Java qui fonctionne avec Hive.</span><span class="sxs-lookup"><span data-stu-id="7a16b-105">Learn how to create a Java-based user-defined function (UDF) that works with Hive.</span></span> <span data-ttu-id="7a16b-106">L’UDF Java dans cet exemple convertit un tableau de chaînes de texte en caractères tous minuscules.</span><span class="sxs-lookup"><span data-stu-id="7a16b-106">The Java UDF in this example converts a table of text strings to all-lowercase characters.</span></span>

## <a name="requirements"></a><span data-ttu-id="7a16b-107">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="7a16b-107">Requirements</span></span>

* <span data-ttu-id="7a16b-108">Un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="7a16b-108">An HDInsight cluster</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="7a16b-109">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="7a16b-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7a16b-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7a16b-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

    <span data-ttu-id="7a16b-111">La plupart des étapes de ce document fonctionnent sur les deux clusters basés sur Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="7a16b-111">Most steps in this document work on both Windows- and Linux-based clusters.</span></span> <span data-ttu-id="7a16b-112">Toutefois, les étapes utilisées pour télécharger la fonction définie par l’utilisateur compilée dans le cluster et l’exécuter sont propres aux clusters basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="7a16b-112">However, the steps used to upload the compiled UDF to the cluster and run it are specific to Linux-based clusters.</span></span> <span data-ttu-id="7a16b-113">Vous trouverez des liens vers des informations qui peuvent être utilisées avec les clusters Windows.</span><span class="sxs-lookup"><span data-stu-id="7a16b-113">Links are provided to information that can be used with Windows-based clusters.</span></span>

* <span data-ttu-id="7a16b-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 ou ultérieur (ou un équivalent, par exemple, OpenJDK)</span><span class="sxs-lookup"><span data-stu-id="7a16b-114">[Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 or later (or an equivalent, such as OpenJDK)</span></span>

* [<span data-ttu-id="7a16b-115">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="7a16b-115">Apache Maven</span></span>](http://maven.apache.org/)

* <span data-ttu-id="7a16b-116">Un éditeur de texte ou un IDE Java</span><span class="sxs-lookup"><span data-stu-id="7a16b-116">A text editor or Java IDE</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7a16b-117">Si vous créez les fichiers Python sur un client Windows, vous avez besoin d’un éditeur qui utilise LF comme fin de ligne.</span><span class="sxs-lookup"><span data-stu-id="7a16b-117">If you create the Python files on a Windows client, you must use an editor that uses LF as a line ending.</span></span> <span data-ttu-id="7a16b-118">Si vous ne savez pas si votre éditeur utilise LF ou CRLF, consultez la section [Dépannage](#troubleshooting) pour savoir comment supprimer le caractère CR.</span><span class="sxs-lookup"><span data-stu-id="7a16b-118">If you are not sure whether your editor uses LF or CRLF, see the [Troubleshooting](#troubleshooting) section for steps on removing the CR character.</span></span>

## <a name="create-an-example-java-udf"></a><span data-ttu-id="7a16b-119">Créer un exemple Java UDF</span><span class="sxs-lookup"><span data-stu-id="7a16b-119">Create an example Java UDF</span></span> 

1. <span data-ttu-id="7a16b-120">À partir d’une ligne de commande, utilisez ce qui suit pour créer un nouveau projet Maven :</span><span class="sxs-lookup"><span data-stu-id="7a16b-120">From a command line, use the following to create a new Maven project:</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > <span data-ttu-id="7a16b-121">Si vous utilisez PowerShell, vous devez placer les paramètres entre guillemets.</span><span class="sxs-lookup"><span data-stu-id="7a16b-121">If you are using PowerShell, you must put quotes around the parameters.</span></span> <span data-ttu-id="7a16b-122">Par exemple, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span><span class="sxs-lookup"><span data-stu-id="7a16b-122">For example, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.</span></span>

    <span data-ttu-id="7a16b-123">Cette commande crée un répertoire nommé **exampleudf**, qui contient le projet Maven.</span><span class="sxs-lookup"><span data-stu-id="7a16b-123">This command creates a directory named **exampleudf**, which contains the Maven project.</span></span>

2. <span data-ttu-id="7a16b-124">Une fois le projet créé, supprimez le répertoire **exampleudf/src/test** qui a été créé dans le cadre du projet.</span><span class="sxs-lookup"><span data-stu-id="7a16b-124">Once the project has been created, delete the **exampleudf/src/test** directory that was created as part of the project.</span></span>

3. <span data-ttu-id="7a16b-125">Ouvrez le fichier **exampleudf/pom.xml** et remplacez l’entrée `<dependencies>` existante par le fichier XML suivant :</span><span class="sxs-lookup"><span data-stu-id="7a16b-125">Open the **exampleudf/pom.xml**, and replace the existing `<dependencies>` entry with the following XML:</span></span>

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

    <span data-ttu-id="7a16b-126">Ces entrées spécifient la version de Hadoop et Hive fournie avec HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="7a16b-126">These entries specify the version of Hadoop and Hive included with HDInsight 3.5.</span></span> <span data-ttu-id="7a16b-127">Vous trouverez des informations sur les versions de Hadoop et Hive incluses dans HDInsight dans le document [Contrôle des versions du composant HDInsight](hdinsight-component-versioning.md) .</span><span class="sxs-lookup"><span data-stu-id="7a16b-127">You can find information on the versions of Hadoop and Hive provided with HDInsight from the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

    <span data-ttu-id="7a16b-128">Ajoutez une section `<build>` avant la ligne `</project>` à la fin du fichier.</span><span class="sxs-lookup"><span data-stu-id="7a16b-128">Add a `<build>` section before the `</project>` line at the end of the file.</span></span> <span data-ttu-id="7a16b-129">Cette section doit comporter le fichier XML suivant :</span><span class="sxs-lookup"><span data-stu-id="7a16b-129">This section should contain the following XML:</span></span>

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

    <span data-ttu-id="7a16b-130">Ces entrées définissent la génération du projet.</span><span class="sxs-lookup"><span data-stu-id="7a16b-130">These entries define how to build the project.</span></span> <span data-ttu-id="7a16b-131">Plus précisément, la version de java utilisée par le projet et la méthode de génération d’un uberjar pour le déploiement sur le cluster.</span><span class="sxs-lookup"><span data-stu-id="7a16b-131">Specifically, the version of Java that the project uses and how to build an uberjar for deployment to the cluster.</span></span>

    <span data-ttu-id="7a16b-132">Enregistrez le fichier une fois les modifications apportées.</span><span class="sxs-lookup"><span data-stu-id="7a16b-132">Save the file once the changes have been made.</span></span>

4. <span data-ttu-id="7a16b-133">Renommez **exampleudf/src/main/java/com/microsoft/examples/App.java** en **ExampleUDF.java**, puis ouvrez le fichier dans votre éditeur.</span><span class="sxs-lookup"><span data-stu-id="7a16b-133">Rename **exampleudf/src/main/java/com/microsoft/examples/App.java** to **ExampleUDF.java**, and then open the file in your editor.</span></span>

5. <span data-ttu-id="7a16b-134">Remplacez le contenu du fichier **ExampleUDF.java** par le code suivant, puis enregistrez-le.</span><span class="sxs-lookup"><span data-stu-id="7a16b-134">Replace the contents of the **ExampleUDF.java** file with the following, then save the file.</span></span>

    ```java
    package com.microsoft.examples;

    import org.apache.hadoop.hive.ql.exec.Description;
    import org.apache.hadoop.hive.ql.exec.UDF;
    import org.apache.hadoop.io.*;

    // Description of the UDF
    @Description(
        name="ExampleUDF",
        value="returns a lower case version of the input string.",
        extended="select ExampleUDF(deviceplatform) from hivesampletable limit 10;"
    )
    public class ExampleUDF extends UDF {
        // Accept a string input
        public String evaluate(String input) {
            // If the value is null, return a null
            if(input == null)
                return null;
            // Lowercase the input string and return it
            return input.toLowerCase();
        }
    }
    ```

    <span data-ttu-id="7a16b-135">Ce code permet d’implémenter une fonction définie par l’utilisateur qui accepte une valeur de chaîne et renvoie une version de la chaîne en minuscules.</span><span class="sxs-lookup"><span data-stu-id="7a16b-135">This code implements a UDF that accepts a string value, and returns a lowercase version of the string.</span></span>

## <a name="build-and-install-the-udf"></a><span data-ttu-id="7a16b-136">Générer et installer la fonction UDF</span><span class="sxs-lookup"><span data-stu-id="7a16b-136">Build and install the UDF</span></span>

1. <span data-ttu-id="7a16b-137">Utilisez la commande suivante pour compiler et empaqueter la fonction UDF :</span><span class="sxs-lookup"><span data-stu-id="7a16b-137">Use the following command to compile and package the UDF:</span></span>

    ```bash
    mvn compile package
    ```

    <span data-ttu-id="7a16b-138">Cette commande génère et conditionne l’UDF dans le fichier `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="7a16b-138">This command builds and packages the UDF into the `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` file.</span></span>

2. <span data-ttu-id="7a16b-139">Utilisez la commande `scp` pour copier le fichier sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7a16b-139">Use the `scp` command to copy the file to the HDInsight cluster.</span></span>

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    <span data-ttu-id="7a16b-140">Remplacez `myuser` par le compte utilisateur SSH de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="7a16b-140">Replace `myuser` with the SSH user account for your cluster.</span></span> <span data-ttu-id="7a16b-141">Remplacez `mycluster` par le nom du cluster.</span><span class="sxs-lookup"><span data-stu-id="7a16b-141">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="7a16b-142">Si vous utilisez un mot de passe pour sécuriser votre compte SSH, vous êtes invité à le saisir.</span><span class="sxs-lookup"><span data-stu-id="7a16b-142">If you used a password to secure the SSH account, you are prompted to enter the password.</span></span> <span data-ttu-id="7a16b-143">Si vous avez utilisé un certificat, vous devrez peut-être utiliser le paramètre `-i` pour spécifier le fichier de clé privée.</span><span class="sxs-lookup"><span data-stu-id="7a16b-143">If you used a certificate, you may need to use the `-i` parameter to specify the private key file.</span></span>

3. <span data-ttu-id="7a16b-144">Connectez-vous au cluster à l'aide de SSH.</span><span class="sxs-lookup"><span data-stu-id="7a16b-144">Connect to the cluster using SSH.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="7a16b-145">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7a16b-145">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

4. <span data-ttu-id="7a16b-146">À partir de la session SSH, copiez le fichier jar sur le stockage HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7a16b-146">From the SSH session, copy the jar file to HDInsight storage.</span></span>

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-the-udf-from-hive"></a><span data-ttu-id="7a16b-147">Utiliser la fonction UDF à partir de Hive</span><span class="sxs-lookup"><span data-stu-id="7a16b-147">Use the UDF from Hive</span></span>

1. <span data-ttu-id="7a16b-148">Utilisez la commande suivante pour démarrer le client Beeline depuis la session SSH.</span><span class="sxs-lookup"><span data-stu-id="7a16b-148">Use the following to start the Beeline client from the SSH session.</span></span>

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    <span data-ttu-id="7a16b-149">Cette commande suppose que vous avez utilisé la valeur par défaut d’ **admin** pour le compte de connexion de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="7a16b-149">This command assumes that you used the default of **admin** for the login account for your cluster.</span></span>

2. <span data-ttu-id="7a16b-150">Une fois sur l’invite `jdbc:hive2://localhost:10001/>` , entrez la commande suivante pour ajouter la fonction UDF dans Hive et l’exposer en tant que fonction.</span><span class="sxs-lookup"><span data-stu-id="7a16b-150">Once you arrive at the `jdbc:hive2://localhost:10001/>` prompt, enter the following to add the UDF to Hive and expose it as a function.</span></span>

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > <span data-ttu-id="7a16b-151">Cet exemple suppose que le stockage Azure est le stockage par défaut pour le cluster.</span><span class="sxs-lookup"><span data-stu-id="7a16b-151">This example assumes that Azure Storage is default storage for the cluster.</span></span> <span data-ttu-id="7a16b-152">Si votre cluster utilise Data Lake Store, remplacez la valeur `wasb:///` par `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="7a16b-152">If your cluster uses Data Lake Store instead, change the `wasb:///` value to `adl:///`.</span></span>

3. <span data-ttu-id="7a16b-153">Utilisez la fonction UDF pour convertir les valeurs extraites d’une table en chaînes de caractères minuscules.</span><span class="sxs-lookup"><span data-stu-id="7a16b-153">Use the UDF to convert values retrieved from a table to lower case strings.</span></span>

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    <span data-ttu-id="7a16b-154">Cette requête sélectionne la plateforme de l’appareil (Android, Windows, iOS, etc.) dans la table, convertit la chaîne en caractères minuscules, puis les affiche.</span><span class="sxs-lookup"><span data-stu-id="7a16b-154">This query selects the device platform (Android, Windows, iOS, etc.) from the table, convert the string to lower case, and then display them.</span></span> <span data-ttu-id="7a16b-155">Le résultat ressemble au texte suivant :</span><span class="sxs-lookup"><span data-stu-id="7a16b-155">The output appears similar to the following text:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7a16b-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7a16b-156">Next steps</span></span>

<span data-ttu-id="7a16b-157">Pour découvrir les autres façons de travailler avec Hive, consultez [Utilisation de Hive avec HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="7a16b-157">For other ways to work with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="7a16b-158">Pour plus d’informations sur les fonctions définies par l’utilisateur de Hive, consultez la section [Hive Operators and User-Defined Functions (Opérateurs et fonctions définies par l’utilisateur de Hive)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) du wiki Hive sur le site apache.org.</span><span class="sxs-lookup"><span data-stu-id="7a16b-158">For more information on Hive User-Defined Functions, see [Hive Operators and User-Defined Functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section of the Hive wiki at apache.org.</span></span>
