---
title: Exemple de topologie Java Apache Storm - Azure HDInsight | Documents Microsoft
description: "Découvrez comment créer des topologies Apache Storm en Java en créant un exemple de topologie de comptage de mots."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: apache storm,exemple apache storm,storm java,exemple de topologie storm
ms.assetid: a8838f29-9c08-4fd9-99ef-26655d1bf6d7
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 36285fbaf1da3c566d338bd5612eebad327eaf50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a><span data-ttu-id="bf4ae-104">Créer une topologie Apache Storm en Java</span><span class="sxs-lookup"><span data-stu-id="bf4ae-104">Create an Apache Storm topology in Java</span></span>

<span data-ttu-id="bf4ae-105">Découvrez comment créer une topologie basée sur Java pour Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-105">Learn how to create a Java-based topology for Apache Storm.</span></span> <span data-ttu-id="bf4ae-106">Vous créez une topologie Storm qui implémente une application de comptage de mots.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-106">You create a Storm topology that implements a word-count application.</span></span> <span data-ttu-id="bf4ae-107">Vous utilisez Maven pour générer et empaqueter le projet.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-107">You use Maven to build and package the project.</span></span> <span data-ttu-id="bf4ae-108">Ensuite, vous allez apprendre à définir la topologie à l’aide de l’infrastructure Flux.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-108">Then, you learn how to define the topology using the Flux framework.</span></span>

> [!NOTE]
> <span data-ttu-id="bf4ae-109">L’infrastructure Flux est disponible dans Storm 0.10.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-109">The Flux framework is available in Storm 0.10.0 or later.</span></span> <span data-ttu-id="bf4ae-110">Storm 0.10.0 est disponible avec HDInsight 3.3 et 3.4.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-110">Storm 0.10.0 is available with HDInsight 3.3 and 3.4.</span></span>

<span data-ttu-id="bf4ae-111">Après avoir suivi les étapes décrites dans ce document, vous pourrez déployer la topologie sur Apache Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-111">After completing the steps in this document, you can deploy the topology to Apache Storm on HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="bf4ae-112">Une version complète des exemples de topologies Storm créés dans ce document est disponible à l’adresse [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="bf4ae-112">A completed version of the Storm topology examples created in this document is available at [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf4ae-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bf4ae-113">Prerequisites</span></span>

* [<span data-ttu-id="bf4ae-114">Kit de développeur Java (JDK) version 7</span><span class="sxs-lookup"><span data-stu-id="bf4ae-114">Java Developer Kit (JDK) version 7</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* <span data-ttu-id="bf4ae-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven est un système de génération de projet pour les projets Java.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="bf4ae-116">Un éditeur de texte ou IDE.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-116">A text editor or IDE.</span></span>

## <a name="configure-environment-variables"></a><span data-ttu-id="bf4ae-117">Configuration des variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="bf4ae-117">Configure environment variables</span></span>

<span data-ttu-id="bf4ae-118">Les variables d’environnement suivantes peuvent être définies lors de l’installation de Java et du JDK.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-118">The following environment variables may be set when you install Java and the JDK.</span></span> <span data-ttu-id="bf4ae-119">Toutefois, vous devez vérifier qu’elles existent et qu’elles contiennent les valeurs correctes pour votre système.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-119">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="bf4ae-120">**JAVA_HOME** : doit pointer vers le répertoire d’installation de l’environnement d’exécution Java (JRE).</span><span class="sxs-lookup"><span data-stu-id="bf4ae-120">**JAVA_HOME** - should point to the directory where the Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="bf4ae-121">Par exemple, sur une distribution Unix ou Linux, il doit avoir une valeur semblable à `/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-121">For example, in a Unix or Linux distribution, it should have a value similar to `/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="bf4ae-122">Sous Windows, il a une valeur semblable à `c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="bf4ae-122">In Windows, it would have a value similar to `c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="bf4ae-123">**PATH** :doit contenir les chemins d’accès suivants :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-123">**PATH** - should contain the following paths:</span></span>

  * <span data-ttu-id="bf4ae-124">**JAVA_HOME** (ou le chemin d’accès équivalent)</span><span class="sxs-lookup"><span data-stu-id="bf4ae-124">**JAVA_HOME** (or the equivalent path)</span></span>

  * <span data-ttu-id="bf4ae-125">**JAVA_HOME\bin** (ou le chemin d’accès équivalent)</span><span class="sxs-lookup"><span data-stu-id="bf4ae-125">**JAVA_HOME\bin** (or the equivalent path)</span></span>

  * <span data-ttu-id="bf4ae-126">Le répertoire d’installation de Maven</span><span class="sxs-lookup"><span data-stu-id="bf4ae-126">The directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="bf4ae-127">Création d’un projet Maven</span><span class="sxs-lookup"><span data-stu-id="bf4ae-127">Create a Maven project</span></span>

<span data-ttu-id="bf4ae-128">À partir de la ligne de commande, utilisez la commande ci-après pour créer un projet Maven nommé **WordCount** :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-128">From the command line, use the following command to create a Maven project named **WordCount**:</span></span>

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> <span data-ttu-id="bf4ae-129">Si vous utilisez PowerShell, vous devez placer les paramètres `-D` entre guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-129">If you are using PowerShell, you must surround the`-D` parameters with double quotes.</span></span>
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

<span data-ttu-id="bf4ae-130">Cette commande crée un répertoire nommé `WordCount` à l’emplacement actuel, qui contient un projet Maven de base.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-130">This command creates a directory named `WordCount` at the current location, which contains a basic Maven project.</span></span> <span data-ttu-id="bf4ae-131">Le répertoire `WordCount` contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-131">The `WordCount` directory contains the following items:</span></span>

* <span data-ttu-id="bf4ae-132">`pom.xml` : contient les paramètres du projet Maven.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-132">`pom.xml`: Contains settings for the Maven project.</span></span>
* <span data-ttu-id="bf4ae-133">`src\main\java\com\microsoft\example` : contient votre code d’application.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-133">`src\main\java\com\microsoft\example`: Contains your application code.</span></span>
* <span data-ttu-id="bf4ae-134">`src\test\java\com\microsoft\example` : contient des tests pour votre application.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-134">`src\test\java\com\microsoft\example`: Contains tests for your application.</span></span> 

### <a name="remove-the-generated-example-code"></a><span data-ttu-id="bf4ae-135">Supprimer l’exemple de code généré</span><span class="sxs-lookup"><span data-stu-id="bf4ae-135">Remove the generated example code</span></span>

<span data-ttu-id="bf4ae-136">Supprimez le test généré et les fichiers d’application :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-136">Delete the generated test and the application files:</span></span>

* <span data-ttu-id="bf4ae-137">**src\test\java\com\microsoft\example\AppTest.java**</span><span class="sxs-lookup"><span data-stu-id="bf4ae-137">**src\test\java\com\microsoft\example\AppTest.java**</span></span>
* <span data-ttu-id="bf4ae-138">**src\main\java\com\microsoft\example\App.java**</span><span class="sxs-lookup"><span data-stu-id="bf4ae-138">**src\main\java\com\microsoft\example\App.java**</span></span>

## <a name="add-maven-repositories"></a><span data-ttu-id="bf4ae-139">Ajouter des référentiels Maven</span><span class="sxs-lookup"><span data-stu-id="bf4ae-139">Add Maven repositories</span></span>

<span data-ttu-id="bf4ae-140">HDInsight étant basé sur Hortonworks Data Platform (HDP), nous recommandons d’utiliser le référentiel Hortonworks pour télécharger les dépendances pour vos projets Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-140">HDInsight is based on the Hortonworks Data Platform (HDP), so we recommend using the Hortonworks repository to download dependencies for your Apache Storm projects.</span></span> <span data-ttu-id="bf4ae-141">Dans le fichier __pom.xml__, ajoutez le code XML suivant après la ligne `<url>http://maven.apache.org</url>`:</span><span class="sxs-lookup"><span data-stu-id="bf4ae-141">In the __pom.xml__ file, add the following XML after the `<url>http://maven.apache.org</url>` line:</span></span>

```xml
<repositories>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPReleases</id>
        <name>HDP Releases</name>
        <url>http://repo.hortonworks.com/content/repositories/releases/</url>
        <layout>default</layout>
    </repository>
    <repository>
        <releases>
            <enabled>true</enabled>
            <updatePolicy>always</updatePolicy>
            <checksumPolicy>warn</checksumPolicy>
        </releases>
        <snapshots>
            <enabled>false</enabled>
            <updatePolicy>never</updatePolicy>
            <checksumPolicy>fail</checksumPolicy>
        </snapshots>
        <id>HDPJetty</id>
        <name>Hadoop Jetty</name>
        <url>http://repo.hortonworks.com/content/repositories/jetty-hadoop/</url>
        <layout>default</layout>
    </repository>
</repositories>
```

## <a name="add-properties"></a><span data-ttu-id="bf4ae-142">Ajout de propriétés</span><span class="sxs-lookup"><span data-stu-id="bf4ae-142">Add properties</span></span>

<span data-ttu-id="bf4ae-143">Maven vous permet de définir des valeurs au niveau du projet appelées propriétés.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-143">Maven allows you to define project-level values called properties.</span></span> <span data-ttu-id="bf4ae-144">Dans le fichier __pom.xml__, ajoutez le texte suivant après la ligne `</repositories>` :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-144">In the __pom.xml__, add the following text after the `</repositories>` line:</span></span>

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from the Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

<span data-ttu-id="bf4ae-145">Vous pouvez maintenant utiliser cette valeur dans d’autres sections de `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-145">You can now use this value in other sections of the `pom.xml`.</span></span> <span data-ttu-id="bf4ae-146">Par exemple, lorsque vous spécifiez la version des composants Storm, vous pouvez utiliser `${storm.version}` plutôt que de coder en dur une valeur.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-146">For example, when specifying the version of Storm components, you can use `${storm.version}` instead of hard coding a value.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="bf4ae-147">Ajout de dépendances</span><span class="sxs-lookup"><span data-stu-id="bf4ae-147">Add dependencies</span></span>

<span data-ttu-id="bf4ae-148">Ajoutez une dépendance pour les composants Storm.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-148">Add a dependency for Storm components.</span></span> <span data-ttu-id="bf4ae-149">Ouvrez le fichier `pom.xml` et ajoutez le code suivant dans la section `<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-149">Open the `pom.xml` file and add the following code in the `<dependencies>` section:</span></span>

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of the jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

<span data-ttu-id="bf4ae-150">Au moment de la compilation, Maven utilise ces informations pour rechercher `storm-core` dans le référentiel Maven.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-150">At compile time, Maven uses this information to look up `storm-core` in the Maven repository.</span></span> <span data-ttu-id="bf4ae-151">Il recherche d’abord dans le référentiel sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-151">It first looks in the repository on your local computer.</span></span> <span data-ttu-id="bf4ae-152">Si les fichiers ne s’y trouvent pas, Maven les télécharge à partir du référentiel Maven public et les stocke dans le référentiel local.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-152">If the files aren't there, Maven downloads them from the public Maven repository and stores them in the local repository.</span></span>

> [!NOTE]
> <span data-ttu-id="bf4ae-153">Notez la ligne `<scope>provided</scope>` dans cette section.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-153">Notice the `<scope>provided</scope>` line in this section.</span></span> <span data-ttu-id="bf4ae-154">Ce paramètre indique à Maven d’exclure **storm-core** de tous les fichiers JAR créés, étant donné que ce dernier est fourni par le système.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-154">This setting tells Maven to exclude **storm-core** from any JAR files that are created, because it is provided by the system.</span></span>

## <a name="build-configuration"></a><span data-ttu-id="bf4ae-155">Configuration de build</span><span class="sxs-lookup"><span data-stu-id="bf4ae-155">Build configuration</span></span>

<span data-ttu-id="bf4ae-156">Les plug-ins Maven permettent de personnaliser les étapes de génération du projet,</span><span class="sxs-lookup"><span data-stu-id="bf4ae-156">Maven plug-ins allow you to customize the build stages of the project.</span></span> <span data-ttu-id="bf4ae-157">telles que la manière dont le projet est compilé ou empaqueté dans un fichier jar.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-157">For example, how the project is compiled or how to package it into a JAR file.</span></span> <span data-ttu-id="bf4ae-158">Ouvrez le fichier `pom.xml` et ajoutez le code suivant directement au-dessus de la ligne `</project>`.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-158">Open the `pom.xml` file and add the following code directly above the `</project>` line.</span></span>

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

<span data-ttu-id="bf4ae-159">Cette section est utilisée pour ajouter des plug-ins, des ressources et d’autres options de configuration de build.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-159">This section is used to add plug-ins, resources, and other build configuration options.</span></span> <span data-ttu-id="bf4ae-160">Pour accéder à la référence complète du fichier **pom.xml** , consultez [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span><span class="sxs-lookup"><span data-stu-id="bf4ae-160">For a full reference of the **pom.xml** file, see [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span></span>

### <a name="add-plug-ins"></a><span data-ttu-id="bf4ae-161">Ajout de plug-ins</span><span class="sxs-lookup"><span data-stu-id="bf4ae-161">Add plug-ins</span></span>

<span data-ttu-id="bf4ae-162">Pour les topologies Apache Storm implémentées en Java, le [plug-in Exec Maven ](http://www.mojohaus.org/exec-maven-plugin/) est utile, car il permet d’exécuter facilement la topologie localement dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-162">For Apache Storm topologies implemented in Java, the [Exec Maven Plugin](http://www.mojohaus.org/exec-maven-plugin/) is useful because it allows you to easily run the topology locally in your development environment.</span></span> <span data-ttu-id="bf4ae-163">Ajoutez le code suivant à la section `<plugins>` du fichier `pom.xml` pour inclure le plug-in Exec Maven :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-163">Add the following to the `<plugins>` section of the `pom.xml` file to include the Exec Maven plugin:</span></span>

```xml
<plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>1.4.0</version>
    <executions>
    <execution>
    <goals>
        <goal>exec</goal>
    </goals>
    </execution>
    </executions>
    <configuration>
    <executable>java</executable>
    <includeProjectDependencies>true</includeProjectDependencies>
    <includePluginDependencies>false</includePluginDependencies>
    <classpathScope>compile</classpathScope>
    <mainClass>${storm.topology}</mainClass>
    <cleanupDaemonThreads>false</cleanupDaemonThreads> 
    </configuration>
</plugin>
```

<span data-ttu-id="bf4ae-164">Le [plug-in du compilateur Maven Apache](http://maven.apache.org/plugins/maven-compiler-plugin/) est un autre plug-in utile, car il sert à modifier les options de compilation.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-164">Another useful plug-in is the [Apache Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/), which is used to change compilation options.</span></span> <span data-ttu-id="bf4ae-165">Il modifie la version de Java que Maven utilise pour la source et la cible de votre application.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-165">The changes the Java version that Maven uses for the source and target for your application.</span></span>

* <span data-ttu-id="bf4ae-166">Pour HDInsight __3.4 ou antérieure__, définissez la source et la cible de la version Java sur __1.7__.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-166">For HDInsight __3.4 or earlier__, set the source and target Java version to __1.7__.</span></span>

* <span data-ttu-id="bf4ae-167">Pour HDInsight __3.5__, définissez la source et la cible de la version Java sur __1.8__.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-167">For HDInsight __3.5__, set the source and target Java version to __1.8__.</span></span>

<span data-ttu-id="bf4ae-168">Ajoutez le texte ci-après à la section `<plugins>` du fichier `pom.xml` pour inclure le plug-in du compilateur Maven Apache.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-168">Add the following text in the `<plugins>` section of the `pom.xml` file to include the Apache Maven Compiler plugin.</span></span> <span data-ttu-id="bf4ae-169">Étant donné que cet exemple spécifie la valeur 1.8, la version cible de HDInsight est 3.5.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-169">This example specifies 1.8, so the target HDInsight version is 3.5.</span></span>

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-compiler-plugin</artifactId>
    <version>3.3</version>
    <configuration>
    <source>1.8</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

### <a name="configure-resources"></a><span data-ttu-id="bf4ae-170">Configuration des ressources</span><span class="sxs-lookup"><span data-stu-id="bf4ae-170">Configure resources</span></span>

<span data-ttu-id="bf4ae-171">La section des ressources vous permet d’inclure des ressources autres que du code comme les fichiers de configuration requis par les composants de la topologie.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-171">The resources section allows you to include non-code resources such as configuration files needed by components in the topology.</span></span> <span data-ttu-id="bf4ae-172">Pour cet exemple, ajoutez le texte ci-après à la section `<resources>` du fichier pom.xml.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-172">For this example, add the following text in the `<resources>` section of the \`pom.xml file.</span></span>

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

<span data-ttu-id="bf4ae-173">Cet exemple ajoute le répertoire des ressources à la racine du projet (`${basedir}`) en tant qu’emplacement contenant des ressources, et inclut le fichier nommé `log4j2.xml`.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-173">This example adds the resources directory in the root of the project (`${basedir}`) as a location that contains resources, and includes the file named `log4j2.xml`.</span></span> <span data-ttu-id="bf4ae-174">Ce fichier est utilisé pour configurer les informations qui sont enregistrées par la topologie.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-174">This file is used to configure what information is logged by the topology.</span></span>

## <a name="create-the-topology"></a><span data-ttu-id="bf4ae-175">Création de la topologie</span><span class="sxs-lookup"><span data-stu-id="bf4ae-175">Create the topology</span></span>

<span data-ttu-id="bf4ae-176">Une topologie Apache Storm basée sur Java comprend trois composants que vous devez créer (ou référencer) en tant que dépendance.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-176">A Java-based Apache Storm topology consists of three components that you must author (or reference) as a dependency.</span></span>

* <span data-ttu-id="bf4ae-177">**Les spouts**: lisent les données provenant de sources externes et émettent des flux de données dans la topologie.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-177">**Spouts**: Reads data from external sources and emits streams of data into the topology.</span></span>

* <span data-ttu-id="bf4ae-178">**Les bolts**: effectuent le traitement des flux de données émis par les spouts ou les autres bolts et émettent un ou plusieurs flux.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-178">**Bolts**: Performs processing on streams emitted by spouts or other bolts, and emits one or more streams.</span></span>

* <span data-ttu-id="bf4ae-179">**La topologie**: définit l’organisation des spouts et des bolts et fournit le point d’entrée pour la topologie.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-179">**Topology**: Defines how the spouts and bolts are arranged, and provides the entry point for the topology.</span></span>

### <a name="create-the-spout"></a><span data-ttu-id="bf4ae-180">Création du spout</span><span class="sxs-lookup"><span data-stu-id="bf4ae-180">Create the spout</span></span>

<span data-ttu-id="bf4ae-181">Afin de réduire les besoins de configuration de sources de données externes, le spout suivant émet des phrases aléatoires.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-181">To reduce requirements for setting up external data sources, the following spout simply emits random sentences.</span></span> <span data-ttu-id="bf4ae-182">Il s’agit d’une version modifiée d’un spout fourni dans les [exemples Storm-Starter](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span><span class="sxs-lookup"><span data-stu-id="bf4ae-182">It is a modified version of a spout that is provided with the [Storm-Starter examples](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span></span>

> [!NOTE]
> <span data-ttu-id="bf4ae-183">Pour obtenir un exemple de spout effectuant des lectures à partir d’une source de données externe, consultez un des exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-183">For an example of a spout that reads from an external data source, see one of the following examples:</span></span>
>
> * <span data-ttu-id="bf4ae-184">[TwitterSampleSpout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): un exemple de spout qui lit à partir de Twitter</span><span class="sxs-lookup"><span data-stu-id="bf4ae-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): An example spout that reads from Twitter</span></span>
> * <span data-ttu-id="bf4ae-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): un spout qui lit à partir de Kafka</span><span class="sxs-lookup"><span data-stu-id="bf4ae-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): A spout that reads from Kafka</span></span>

<span data-ttu-id="bf4ae-186">Pour le spout, créez un fichier nommé `RandomSentenceSpout.java` dans le répertoire `src\main\java\com\microsoft\example` puis utilisez le code Java suivant en guise de contenu :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-186">For the spout, create a file named `RandomSentenceSpout.java` in the `src\main\java\com\microsoft\example` directory and use the following Java code as the contents:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.spout.SpoutOutputCollector;
import org.apache.storm.task.TopologyContext;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseRichSpout;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Values;
import org.apache.storm.utils.Utils;

import java.util.Map;
import java.util.Random;

//This spout randomly emits sentences
public class RandomSentenceSpout extends BaseRichSpout {
  //Collector used to emit output
  SpoutOutputCollector _collector;
  //Used to generate a random number
  Random _rand;

  //Open is called when an instance of the class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set the instance collector to the one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data to the stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //The sentences that are randomly emitted
    String[] sentences = new String[]{ "the cow jumped over the moon", "an apple a day keeps the doctor away",
        "four score and seven years ago", "snow white and the seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit the sentence
    _collector.emit(new Values(sentence));
  }

  //Ack is not implemented since this is a basic example
  @Override
  public void ack(Object id) {
  }

  //Fail is not implemented since this is a basic example
  @Override
  public void fail(Object id) {
  }

  //Declare the output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> <span data-ttu-id="bf4ae-187">Bien que cette topologie utilise un seul spout, d’autres peuvent en avoir plusieurs, qui alimentent la topologie avec des données provenant de sources différentes.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-187">Although this topology uses only one spout, others may have several that feed data from different sources into the topology.</span></span>

### <a name="create-the-bolts"></a><span data-ttu-id="bf4ae-188">Création des bolts</span><span class="sxs-lookup"><span data-stu-id="bf4ae-188">Create the bolts</span></span>

<span data-ttu-id="bf4ae-189">Les bolts gèrent le traitement des données.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-189">Bolts handle the data processing.</span></span> <span data-ttu-id="bf4ae-190">Cette topologie utilise deux bolts :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-190">This topology uses two bolts:</span></span>

* <span data-ttu-id="bf4ae-191">**SplitSentence** : fractionne les phrases émises par **RandomSentenceSpout** en mots.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-191">**SplitSentence**: Splits the sentences emitted by **RandomSentenceSpout** into individual words.</span></span>

* <span data-ttu-id="bf4ae-192">**WordCount**: compte le nombre d’occurrences de chaque mot.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-192">**WordCount**: Counts how many times each word has occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="bf4ae-193">Les bolts peuvent tout faire : calculs, persistance, communication avec des composants externes, etc.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-193">Bolts can do anything, for example, computation, persistence, or talking to external components.</span></span>

<span data-ttu-id="bf4ae-194">Créez deux fichiers, `SplitSentence.java` et `WordCount.java`, dans le répertoire `src\main\java\com\microsoft\example`.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-194">Create two new files, `SplitSentence.java` and `WordCount.java` in the `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="bf4ae-195">Utilisez le texte ci-après comme contenu des fichiers :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-195">Use the following text as the contents for the files:</span></span>

#### <a name="splitsentence"></a><span data-ttu-id="bf4ae-196">SplitSentence</span><span class="sxs-lookup"><span data-stu-id="bf4ae-196">SplitSentence</span></span>

```java
package com.microsoft.example;

import java.text.BreakIterator;

import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class SplitSentence extends BaseBasicBolt {

  //Execute is called to process tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get the sentence content from the tuple
    String sentence = tuple.getString(0);
    //An iterator to get each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give the iterator the sentence
    boundary.setText(sentence);
    //Find the beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it to the output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get the word
      String word=sentence.substring(start,end);
      //If a word is whitespace characters, replace it with empty
      word=word.replaceAll("\\s+","");
      //if it's an actual word, emit it
      if (!word.equals("")) {
        collector.emit(new Values(word));
      }
    }
  }

  //Declare that emitted tuples contain a word field
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word"));
  }
}
```

#### <a name="wordcount"></a><span data-ttu-id="bf4ae-197">WordCount</span><span class="sxs-lookup"><span data-stu-id="bf4ae-197">WordCount</span></span>

```java
package com.microsoft.example;

import java.util.HashMap;
import java.util.Map;
import java.util.Iterator;

import org.apache.storm.Constants;
import org.apache.storm.topology.BasicOutputCollector;
import org.apache.storm.topology.OutputFieldsDeclarer;
import org.apache.storm.topology.base.BaseBasicBolt;
import org.apache.storm.tuple.Fields;
import org.apache.storm.tuple.Tuple;
import org.apache.storm.tuple.Values;
import org.apache.storm.Config;

// For logging
import org.apache.logging.log4j.Logger;
import org.apache.logging.log4j.LogManager;

//There are a variety of bolt types. In this case, use BaseBasicBolt
public class WordCount extends BaseBasicBolt {
  //Create logger for this class
  private static final Logger logger = LogManager.getLogger(WordCount.class);
  //For holding words and counts
  Map<String, Integer> counts = new HashMap<String, Integer>();
  //How often to emit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default to 60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used to trigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called to process tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //If it's a tick tuple, emit all words and counts
    if(tuple.getSourceComponent().equals(Constants.SYSTEM_COMPONENT_ID)
            && tuple.getSourceStreamId().equals(Constants.SYSTEM_TICK_STREAM_ID)) {
      for(String word : counts.keySet()) {
        Integer count = counts.get(word);
        collector.emit(new Values(word, count));
        logger.info("Emitting a count of " + count + " for word " + word);
      }
    } else {
      //Get the word contents from the tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment the count and store it
      count++;
      counts.put(word, count);
    }
  }

  //Declare that this emits a tuple containing two fields; word and count
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("word", "count"));
  }
}
```

### <a name="define-the-topology"></a><span data-ttu-id="bf4ae-198">Définition de la topologie</span><span class="sxs-lookup"><span data-stu-id="bf4ae-198">Define the topology</span></span>

<span data-ttu-id="bf4ae-199">La topologie lie les spouts et les bolts dans un graphique, qui définit la circulation des données entre les composants.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-199">The topology ties the spouts and bolts together into a graph, which defines how data flows between the components.</span></span> <span data-ttu-id="bf4ae-200">Elle fournit également des indicateurs de parallélisme que Storm utilise lors de la création des instances de composants au sein du cluster.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-200">It also provides parallelism hints that Storm uses when creating instances of the components within the cluster.</span></span>

<span data-ttu-id="bf4ae-201">L’image ci-dessous illustre un diagramme de base des composants de cette topologie.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-201">The following image is a basic diagram of the graph of components for this topology.</span></span>

![schéma montrant la disposition des spouts et bolts](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

<span data-ttu-id="bf4ae-203">Pour implémenter la topologie, créez un fichier nommé `WordCountTopology.java` dans le répertoire `src\main\java\com\microsoft\example`.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-203">To implement the topology, create a file named `WordCountTopology.java` in the `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="bf4ae-204">Utilisez le code Java suivant comme contenu du fichier :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-204">Use the following Java code as the contents of the file:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for the topology
  public static void main(String[] args) throws Exception {
  //Used to build the topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add the spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add the SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes to the spout, and equally distributes
    //tuples (sentences) across instances of the SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add the counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes to the split bolt, and
    //ensures that the same word is sent to the same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set to false to disable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint to set the number of workers
      conf.setNumWorkers(3);
      //submit the topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap the maximum number of executors that can be spawned
      //for a component to 3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used to run locally
      LocalCluster cluster = new LocalCluster();
      //submit the topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down the cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a><span data-ttu-id="bf4ae-205">Configuration de la journalisation</span><span class="sxs-lookup"><span data-stu-id="bf4ae-205">Configure logging</span></span>

<span data-ttu-id="bf4ae-206">Storm utilise Apache Log4j pour journaliser les informations.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-206">Storm uses Apache Log4j to log information.</span></span> <span data-ttu-id="bf4ae-207">Si vous ne configurez pas la journalisation, la topologie émet des informations de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-207">If you do not configure logging, the topology emits diagnostic information.</span></span> <span data-ttu-id="bf4ae-208">Pour contrôler ce qui est enregistré, créez un fichier nommé `log4j2.xml` dans le répertoire `resources`.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-208">To control what is logged, create a file named `log4j2.xml` in the `resources` directory.</span></span> <span data-ttu-id="bf4ae-209">Utilisez le code XML suivant comme contenu du fichier.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-209">Use the following XML as the contents of the file.</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration>
<Appenders>
    <Console name="STDOUT" target="SYSTEM_OUT">
        <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger{36} - %msg%n"/>
    </Console>
</Appenders>
<Loggers>
    <Logger name="com.microsoft.example" level="trace" additivity="false">
        <AppenderRef ref="STDOUT"/>
    </Logger>
    <Root level="error">
        <Appender-Ref ref="STDOUT"/>
    </Root>
</Loggers>
</Configuration>
```

<span data-ttu-id="bf4ae-210">Ce code XML configure un nouvel enregistreur pour la classe `com.microsoft.example`, qui inclut les composants de cet exemple de topologie.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-210">This XML configures a new logger for the `com.microsoft.example` class, which includes the components in this example topology.</span></span> <span data-ttu-id="bf4ae-211">Le niveau est défini pour effectuer le suivi de cet enregistreur d’événements, ce qui capture les informations de journalisation émises par les composants dans cette topologie.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-211">The level is set to trace for this logger, which captures any logging information emitted by components in this topology.</span></span>

<span data-ttu-id="bf4ae-212">La section `<Root level="error">` configure le niveau racine de journalisation (tout ce qui ne figure pas dans `com.microsoft.example`) pour enregistrer uniquement les informations d’erreur.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-212">The `<Root level="error">` section configures the root level of logging (everything not in `com.microsoft.example`) to only log error information.</span></span>

<span data-ttu-id="bf4ae-213">Pour plus d’informations sur la configuration de la journalisation pour Log4j, consultez [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span><span class="sxs-lookup"><span data-stu-id="bf4ae-213">For more information on configuring logging for Log4j, see [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span></span>

> [!NOTE]
> <span data-ttu-id="bf4ae-214">Storm version 0.10.0 et ultérieure utilisent Log4j 2.x.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-214">Storm version 0.10.0 and higher use Log4j 2.x.</span></span> <span data-ttu-id="bf4ae-215">Les versions antérieures de Storm utilisaient Log4j 1.x, qui utilisait un autre format pour la configuration du journal.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-215">Older versions of storm used Log4j 1.x, which used a different format for log configuration.</span></span> <span data-ttu-id="bf4ae-216">Pour plus d’informations sur la configuration antérieure, consultez [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span><span class="sxs-lookup"><span data-stu-id="bf4ae-216">For information on the older configuration, see [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span></span>

## <a name="test-the-topology-locally"></a><span data-ttu-id="bf4ae-217">Test local de la topologie</span><span class="sxs-lookup"><span data-stu-id="bf4ae-217">Test the topology locally</span></span>

<span data-ttu-id="bf4ae-218">Après avoir enregistré les fichiers, utilisez la commande suivante pour tester la topologie localement.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-218">After you save the files, use the following command to test the topology locally.</span></span>

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

<span data-ttu-id="bf4ae-219">Pendant son exécution, la topologie affiche les informations de démarrage.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-219">As it runs, the topology displays startup information.</span></span> <span data-ttu-id="bf4ae-220">Le texte ci-après est un exemple de sortie de statistiques :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-220">The following text is an example of the word count output:</span></span>

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

<span data-ttu-id="bf4ae-221">Cet exemple de journal indique que le mot « and » a été utilisé 113 fois.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-221">This example log indicates that the word 'and' has been emitted 113 times.</span></span> <span data-ttu-id="bf4ae-222">Le décompte continue d’augmenter tant que la topologie s’exécute, car le Spout émet continuellement les mêmes phrases.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-222">The count continues to go up as long as the topology runs because the spout continuously emits the same sentences.</span></span>

<span data-ttu-id="bf4ae-223">Il existe un intervalle de 5 secondes entre l’émission des mots et les décomptes.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-223">There is a 5-second interval between emission of words and counts.</span></span> <span data-ttu-id="bf4ae-224">Le composant **WordCount** est configuré pour émettre des informations uniquement lors de la réception d’un tuple de graduation.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-224">The **WordCount** component is configured to only emit information when a tick tuple arrives.</span></span> <span data-ttu-id="bf4ae-225">Il demande que tuples de graduation soient remis uniquement toutes les cinq secondes.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-225">It requests that tick tuples are only delivered every five seconds.</span></span>

## <a name="convert-the-topology-to-flux"></a><span data-ttu-id="bf4ae-226">Convertir la topologie vers Flux</span><span class="sxs-lookup"><span data-stu-id="bf4ae-226">Convert the topology to Flux</span></span>

<span data-ttu-id="bf4ae-227">Flux est une nouvelle infrastructure disponible avec Storm 0.10.0 et versions supérieures qui vous permet de séparer la configuration de la mise en œuvre.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-227">Flux is a new framework available with Storm 0.10.0 and higher, which allows you to separate configuration from implementation.</span></span> <span data-ttu-id="bf4ae-228">Vos composants sont toujours définis dans Java, mais la topologie est définie à l’aide d’un fichier YAML.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-228">Your components are still defined in Java, but the topology is defined using a YAML file.</span></span> <span data-ttu-id="bf4ae-229">Vous pouvez empaqueter une définition de la topologie par défaut avec votre projet, ou utiliser un fichier autonome lors de l’envoi de la topologie.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-229">You can package a default topology definition with your project, or use a standalone file when submitting the topology.</span></span> <span data-ttu-id="bf4ae-230">Lors de l’envoi de la topologie à Storm, vous pouvez utiliser des variables d’environnement ou des fichiers de configuration pour remplir les valeurs dans la définition de la topologie YAML.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-230">When submitting the topology to Storm, you can use environment variables or configuration files to populate values in the YAML topology definition.</span></span>

<span data-ttu-id="bf4ae-231">Le fichier YAML définit les composants à utiliser pour la topologie et le flux de données entre eux.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-231">The YAML file defines the components to use for the topology and the data flow between them.</span></span> <span data-ttu-id="bf4ae-232">Vous pouvez inclure un fichier YAML dans le fichier jar ou utiliser un fichier YAML externe.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-232">You can include a YAML file as part of the jar file or you can use an external YAML file.</span></span>

<span data-ttu-id="bf4ae-233">Pour plus d’informations sur Flux, voir [Infrastructure Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="bf4ae-233">For more information on Flux, see [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

> [!WARNING]
> <span data-ttu-id="bf4ae-234">En raison d’un [bogue (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) lié à Storm 1.0.1, vous devrez peut-être installer un [environnement de développement Storm](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) pour exécuter des topologies Flux localement.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-234">Due to a [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) with Storm 1.0.1, you may need to install a [Storm development environment](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) to run Flux topologies locally.</span></span>

1. <span data-ttu-id="bf4ae-235">Retirez le fichier `WordCountTopology.java` du projet.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-235">Move the `WordCountTopology.java` file out of the project.</span></span> <span data-ttu-id="bf4ae-236">Auparavant, ce fichier définissait la topologie, mais il n’est pas nécessaire avec Flux.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-236">Previously, this file defined the topology, but isn't needed with Flux.</span></span>

2. <span data-ttu-id="bf4ae-237">Dans le répertoire `resources`, créez un fichier nommé `topology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-237">In the `resources` directory, create a file named `topology.yaml`.</span></span> <span data-ttu-id="bf4ae-238">Utilisez le texte ci-après comme contenu de ce fichier.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-238">Use the following text as the contents of this file.</span></span>

        name: "wordcount"       # friendly name for the topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for the number of workers to create
        
        spouts:                 # Spout definitions
        - id: "sentence-spout"
            className: "com.microsoft.example.RandomSentenceSpout"
            parallelism: 1      # parallelism hint
        
        bolts:                  # Bolt definitions
        - id: "splitter-bolt"
            className: "com.microsoft.example.SplitSentence"
            parallelism: 1
         
        - id: "counter-bolt"
            className: "com.microsoft.example.WordCount"
            constructorArgs:
                - 10
            parallelism: 1
        
        streams:                # Stream definitions
            - name: "Spout --> Splitter" # name isn't used (placeholder for logging, UI, etc.)
            from: "sentence-spout"       # The stream emitter
            to: "splitter-bolt"          # The stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) to group on

3. <span data-ttu-id="bf4ae-239">Apportez les modifications suivantes au fichier `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-239">Make the following changes to the `pom.xml` file.</span></span>
   
   * <span data-ttu-id="bf4ae-240">Ajoutez la nouvelle dépendance suivante dans la section `<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-240">Add the following new dependency in the `<dependencies>` section:</span></span>
     
        ```xml
        <!-- Add a dependency on the Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * <span data-ttu-id="bf4ae-241">Ajoutez le plug-in suivant à la section `<plugins>` .</span><span class="sxs-lookup"><span data-stu-id="bf4ae-241">Add the following plugin to the `<plugins>` section.</span></span> <span data-ttu-id="bf4ae-242">Ce plug-in gère la création d’un package (fichier jar) pour le projet et applique certaines transformations spécifiques à Flux lors de la création du package.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-242">This plugin handles the creation of a package (jar file) for the project, and applies some transformations specific to Flux when creating the package.</span></span>
     
        ```xml
        <!-- build an uber jar -->
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
                <transformers>
                    <!-- Keep us from getting a "can't overwrite file error" -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer" />
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer" />
                    <!-- We're using Flux, so refer to it as main -->
                    <transformer implementation="org.apache.maven.plugins.shade.resource.ManifestResourceTransformer">
                        <mainClass>org.apache.storm.flux.Flux</mainClass>
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
        ```

   * <span data-ttu-id="bf4ae-243">Dans la section **exec-maven-plugin** `<configuration>`, remplacez la valeur de `<mainClass>` par `org.apache.storm.flux.Flux`.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-243">In the **exec-maven-plugin** `<configuration>` section, change the value for `<mainClass>` to `org.apache.storm.flux.Flux`.</span></span> <span data-ttu-id="bf4ae-244">Ce paramètre permet à Flux de gérer l’exécution de la topologie localement dans l’environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-244">This setting allows Flux to handle running the topology locally in development.</span></span>

   * <span data-ttu-id="bf4ae-245">Dans la section `<resources>`, ajoutez ce qui suit à `<includes>`.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-245">In the `<resources>` section, add the following to the `<includes>`.</span></span> <span data-ttu-id="bf4ae-246">Cela inclut le fichier YAML définissant la topologie en tant que partie du projet.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-246">This XML includes the YAML file that defines the topology as part of the project.</span></span>

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-the-flux-topology-locally"></a><span data-ttu-id="bf4ae-247">Tester la topologie Flux localement</span><span class="sxs-lookup"><span data-stu-id="bf4ae-247">Test the flux topology locally</span></span>

1. <span data-ttu-id="bf4ae-248">Utilisez le code ci-après pour compiler et exécuter la topologie Flux à l’aide de Maven :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-248">Use the following to compile and execute the Flux topology using Maven:</span></span>

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    <span data-ttu-id="bf4ae-249">Si vous utilisez PowerShell, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-249">If you are using PowerShell, use the following command:</span></span>

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > <span data-ttu-id="bf4ae-250">Si votre topologie utilise des bits Storm 1.0.1, cette commande échoue.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-250">If your topology uses Storm 1.0.1 bits, this command fails.</span></span> <span data-ttu-id="bf4ae-251">Cet échec est dû à [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span><span class="sxs-lookup"><span data-stu-id="bf4ae-251">This failure is caused by [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span></span> <span data-ttu-id="bf4ae-252">Au lieu de cela, [installez Storm dans votre environnement de développement](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) et utilisez les informations suivantes.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-252">Instead, [install Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) and use the following information.</span></span>

    <span data-ttu-id="bf4ae-253">Si vous avez [installé Storm dans votre environnement de développement](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), vous pouvez utiliser les commandes suivantes à la place :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-253">If you have [installed Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), you can use the following commands instead:</span></span>

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    <span data-ttu-id="bf4ae-254">Le paramètre `--local` exécute la topologie en mode local dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-254">The `--local` parameter runs the topology in local mode on your development environment.</span></span> <span data-ttu-id="bf4ae-255">Le paramètre `-R /topology.yaml` utilise la ressource de fichier `topology.yaml` à partir du fichier jar pour définir la topologie.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-255">The `-R /topology.yaml` parameter uses the `topology.yaml` file resource from the jar file to define the topology.</span></span>

    <span data-ttu-id="bf4ae-256">Pendant son exécution, la topologie affiche les informations de démarrage.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-256">As it runs, the topology displays startup information.</span></span> <span data-ttu-id="bf4ae-257">Le texte ci-après constitue un exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-257">The following text is an example of the output:</span></span>

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    <span data-ttu-id="bf4ae-258">Il existe un délai de 10 secondes entre chaque lot d’informations enregistrées.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-258">There is a 10-second delay between batches of logged information.</span></span>

2. <span data-ttu-id="bf4ae-259">Copiez le fichier `topology.yaml` à partir du projet.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-259">Make a copy of the `topology.yaml` file from the project.</span></span> <span data-ttu-id="bf4ae-260">Nommez le nouveau fichier `newtopology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-260">Name the new file `newtopology.yaml`.</span></span> <span data-ttu-id="bf4ae-261">Dans le fichier `newtopology.yaml`, recherchez la section ci-après et remplacez la valeur `10` par `5`.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-261">In the `newtopology.yaml` file, find the following section and change the value of `10` to `5`.</span></span> <span data-ttu-id="bf4ae-262">Cela a pour effet de modifier l’intervalle entre les émissions de lots de comptes de mots de 10 à 5 secondes.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-262">This modification changes the interval between emitting batches of word counts from 10 seconds to 5.</span></span>

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. To run the topology, use the following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    <span data-ttu-id="bf4ae-263">Ou, si vous avez Storm dans votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-263">Or, if you have Storm on your development environment:</span></span>

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    <span data-ttu-id="bf4ae-264">Remplacez `/path/to/newtopology.yaml` par le chemin d’accès au fichier newtopology.yaml que vous avez créé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-264">Change the `/path/to/newtopology.yaml` to the path to the newtopology.yaml file you created in the previous step.</span></span> <span data-ttu-id="bf4ae-265">Cette commande utilise le fichier newtopology.yaml en tant que définition de la topologie.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-265">This command uses the newtopology.yaml as the topology definition.</span></span> <span data-ttu-id="bf4ae-266">Étant donné que nous n’avons pas inclus le paramètre `compile`, Maven utilise la version du projet créée aux étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-266">Since we didn't include the `compile` parameter, Maven uses the version of the project built in previous steps.</span></span>

    <span data-ttu-id="bf4ae-267">Une fois que la topologie démarre, vous remarquerez que la durée entre les lots émis a changé pour refléter la valeur dans newtopology.yaml.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-267">Once the topology starts, you should notice that the time between emitted batches has changed to reflect the value in newtopology.yaml.</span></span> <span data-ttu-id="bf4ae-268">Par conséquent, vous pouvez voir que vous pouvez modifier votre configuration via un fichier YAML sans avoir à recompiler la topologie.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-268">So you can see that you can change your configuration through a YAML file without having to recompile the topology.</span></span>

<span data-ttu-id="bf4ae-269">Pour plus d’informations sur celles-ci et d’autres fonctionnalités de l’infrastructure Flux, consultez [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="bf4ae-269">For more information on these and other features of the Flux framework, see [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

## <a name="trident"></a><span data-ttu-id="bf4ae-270">Trident</span><span class="sxs-lookup"><span data-stu-id="bf4ae-270">Trident</span></span>

<span data-ttu-id="bf4ae-271">Trident est une abstraction de haut niveau fournie par Storm.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-271">Trident is a high-level abstraction that is provided by Storm.</span></span> <span data-ttu-id="bf4ae-272">Il prend en charge le traitement avec état.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-272">It supports stateful processing.</span></span> <span data-ttu-id="bf4ae-273">Le principal avantage de Trident est qu’il peut garantir que chaque message qui entre dans la topologie n’est traité qu’une seule fois,</span><span class="sxs-lookup"><span data-stu-id="bf4ae-273">The primary advantage of Trident is that it can guarantee that every message that enters the topology is processed only once.</span></span> <span data-ttu-id="bf4ae-274">Sans utilisation de Trident, votre topologie peut uniquement garantir que les messages sont traités au moins une fois.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-274">Without using Trident, your topology can only guarantee that messages are processed at least once.</span></span> <span data-ttu-id="bf4ae-275">Il existe aussi d'autres différences, comme les composants intégrés pouvant être utilisés, plutôt que de créer des bolts.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-275">There are also other differences, such as built-in components that can be used instead of creating bolts.</span></span> <span data-ttu-id="bf4ae-276">Les Bolts sont remplacés par des composants moins génériques, tels que des filtres, des projections et des fonctions.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-276">In fact, bolts are replaced by less-generic components, such as filters, projections, and functions.</span></span>

<span data-ttu-id="bf4ae-277">Les applications Trident peuvent être créées à l’aide de projets Maven.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-277">Trident applications can be created by using Maven projects.</span></span> <span data-ttu-id="bf4ae-278">Les étapes de base sont les mêmes que celles présentées plus haut dans cet article, seul le code est différent.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-278">You use the same basic steps as presented earlier in this article—only the code is different.</span></span> <span data-ttu-id="bf4ae-279">Trident est également inutilisable (actuellement) avec l’infrastructure Flux.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-279">Trident also cannot (currently) be used with the Flux framework.</span></span>

<span data-ttu-id="bf4ae-280">Pour plus d’informations sur Trident, consultez la [Présentation de l’API Trident](http://storm.apache.org/documentation/Trident-API-Overview.html).</span><span class="sxs-lookup"><span data-stu-id="bf4ae-280">For more information about Trident, see the [Trident API Overview](http://storm.apache.org/documentation/Trident-API-Overview.html).</span></span>

<span data-ttu-id="bf4ae-281">Pour obtenir un exemple d’application Trident, consultez les [Rubriques de tendances Twitter avec Apache Storm sur HDInsight](hdinsight-storm-twitter-trending.md).</span><span class="sxs-lookup"><span data-stu-id="bf4ae-281">For an example of a Trident application, see [Twitter trending topics with Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf4ae-282">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bf4ae-282">Next Steps</span></span>

<span data-ttu-id="bf4ae-283">Vous avez appris à créer une topologie Storm à l’aide de Java.</span><span class="sxs-lookup"><span data-stu-id="bf4ae-283">You have learned how to create a Storm topology by using Java.</span></span> <span data-ttu-id="bf4ae-284">Apprenez maintenant à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="bf4ae-284">Now learn how to:</span></span>

* [<span data-ttu-id="bf4ae-285">Déploiement et gestion des topologies Apache Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="bf4ae-285">Deploy and manage Apache Storm topologies on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)

* [<span data-ttu-id="bf4ae-286">Développement de topologies C# pour Apache Storm dans HDInsight à l'aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bf4ae-286">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="bf4ae-287">Vous trouverez davantage d’exemples de topologies Storm en vous rendant sur [Exemples de topologies Storm sur HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="bf4ae-287">You can find more example Storm topologies by visiting [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

