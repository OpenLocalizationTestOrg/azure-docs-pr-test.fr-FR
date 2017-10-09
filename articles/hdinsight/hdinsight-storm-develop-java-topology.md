---
title: aaaApache renverser exemple de topologie Java - Azure HDInsight | Documents Microsoft
description: "Découvrez comment les topologies d’Apache Storm toocreate dans Java en créant un mot exemple compter topologie."
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
ms.openlocfilehash: 54fa9dc3c93ddad83ac861f3101f50f80117d804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-storm-topology-in-java"></a><span data-ttu-id="73a2b-104">Créer une topologie Apache Storm en Java</span><span class="sxs-lookup"><span data-stu-id="73a2b-104">Create an Apache Storm topology in Java</span></span>

<span data-ttu-id="73a2b-105">Découvrez comment toocreate une topologie basée sur Java d’Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="73a2b-105">Learn how toocreate a Java-based topology for Apache Storm.</span></span> <span data-ttu-id="73a2b-106">Vous créez une topologie Storm qui implémente une application de comptage de mots.</span><span class="sxs-lookup"><span data-stu-id="73a2b-106">You create a Storm topology that implements a word-count application.</span></span> <span data-ttu-id="73a2b-107">Vous utilisez Maven toobuild et package hello le projet.</span><span class="sxs-lookup"><span data-stu-id="73a2b-107">You use Maven toobuild and package hello project.</span></span> <span data-ttu-id="73a2b-108">Ensuite, vous allez apprendre comment l’à l’aide de topologie toodefine hello hello framework de Flux.</span><span class="sxs-lookup"><span data-stu-id="73a2b-108">Then, you learn how toodefine hello topology using hello Flux framework.</span></span>

> [!NOTE]
> <span data-ttu-id="73a2b-109">infrastructure de Flux Hello est disponible dans Storm 0.10.0 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="73a2b-109">hello Flux framework is available in Storm 0.10.0 or later.</span></span> <span data-ttu-id="73a2b-110">Storm 0.10.0 est disponible avec HDInsight 3.3 et 3.4.</span><span class="sxs-lookup"><span data-stu-id="73a2b-110">Storm 0.10.0 is available with HDInsight 3.3 and 3.4.</span></span>

<span data-ttu-id="73a2b-111">Après avoir effectué les étapes de hello dans ce document, vous pouvez déployer hello topologie tooApache Storm sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="73a2b-111">After completing hello steps in this document, you can deploy hello topology tooApache Storm on HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="73a2b-112">Une version complète d’exemples de topologie Storm hello créé dans ce document est disponible à l’adresse [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="73a2b-112">A completed version of hello Storm topology examples created in this document is available at [https://github.com/Azure-Samples/hdinsight-java-storm-wordcount](https://github.com/Azure-Samples/hdinsight-java-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73a2b-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="73a2b-113">Prerequisites</span></span>

* [<span data-ttu-id="73a2b-114">Kit de développeur Java (JDK) version 7</span><span class="sxs-lookup"><span data-stu-id="73a2b-114">Java Developer Kit (JDK) version 7</span></span>](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)

* <span data-ttu-id="73a2b-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven est un système de génération de projet pour les projets Java.</span><span class="sxs-lookup"><span data-stu-id="73a2b-115">[Maven (https://maven.apache.org/download.cgi)](https://maven.apache.org/download.cgi): Maven is a project build system for Java projects.</span></span>

* <span data-ttu-id="73a2b-116">Un éditeur de texte ou IDE.</span><span class="sxs-lookup"><span data-stu-id="73a2b-116">A text editor or IDE.</span></span>

## <a name="configure-environment-variables"></a><span data-ttu-id="73a2b-117">Configuration des variables d’environnement</span><span class="sxs-lookup"><span data-stu-id="73a2b-117">Configure environment variables</span></span>

<span data-ttu-id="73a2b-118">Hello variables d’environnement suivantes peuvent être définis lors de l’installation de Java et hello JDK.</span><span class="sxs-lookup"><span data-stu-id="73a2b-118">hello following environment variables may be set when you install Java and hello JDK.</span></span> <span data-ttu-id="73a2b-119">Toutefois, vous devez vérifier qu’ils existent et qu’ils contiennent des valeurs correctes de hello pour votre système.</span><span class="sxs-lookup"><span data-stu-id="73a2b-119">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="73a2b-120">**JAVA_HOME** -doit pointer Active toohello où hello Java runtime environment (JRE) est installé.</span><span class="sxs-lookup"><span data-stu-id="73a2b-120">**JAVA_HOME** - should point toohello directory where hello Java runtime environment (JRE) is installed.</span></span> <span data-ttu-id="73a2b-121">Par exemple, dans une distribution Unix ou Linux, il doit avoir une valeur similaire trop`/usr/lib/jvm/java-7-oracle`.</span><span class="sxs-lookup"><span data-stu-id="73a2b-121">For example, in a Unix or Linux distribution, it should have a value similar too`/usr/lib/jvm/java-7-oracle`.</span></span> <span data-ttu-id="73a2b-122">Dans Windows, il aurait une valeur similaire trop`c:\Program Files (x86)\Java\jre1.7`</span><span class="sxs-lookup"><span data-stu-id="73a2b-122">In Windows, it would have a value similar too`c:\Program Files (x86)\Java\jre1.7`</span></span>

* <span data-ttu-id="73a2b-123">**Chemin d’accès** -doit contenir hello suivant des chemins d’accès :</span><span class="sxs-lookup"><span data-stu-id="73a2b-123">**PATH** - should contain hello following paths:</span></span>

  * <span data-ttu-id="73a2b-124">**JAVA_HOME** (ou les chemins d’accès équivalents hello)</span><span class="sxs-lookup"><span data-stu-id="73a2b-124">**JAVA_HOME** (or hello equivalent path)</span></span>

  * <span data-ttu-id="73a2b-125">**JAVA_HOME\bin** (ou les chemins d’accès équivalents hello)</span><span class="sxs-lookup"><span data-stu-id="73a2b-125">**JAVA_HOME\bin** (or hello equivalent path)</span></span>

  * <span data-ttu-id="73a2b-126">répertoire d’Hello installation Maven</span><span class="sxs-lookup"><span data-stu-id="73a2b-126">hello directory where Maven is installed</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="73a2b-127">Création d’un projet Maven</span><span class="sxs-lookup"><span data-stu-id="73a2b-127">Create a Maven project</span></span>

<span data-ttu-id="73a2b-128">À partir de la ligne de commande hello, utilisez hello commande suivante toocreate un projet Maven nommé **WordCount**:</span><span class="sxs-lookup"><span data-stu-id="73a2b-128">From hello command line, use hello following command toocreate a Maven project named **WordCount**:</span></span>

```bash
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -DgroupId=com.microsoft.example -DartifactId=WordCount -DinteractiveMode=false
```

> [!NOTE]
> <span data-ttu-id="73a2b-129">Si vous utilisez PowerShell, vous devez placer les paramètres `-D` entre guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="73a2b-129">If you are using PowerShell, you must surround the`-D` parameters with double quotes.</span></span>
>
> `mvn archetype:generate "-DarchetypeArtifactId=maven-archetype-quickstart" "-DgroupId=com.microsoft.example" "-DartifactId=WordCount" "-DinteractiveMode=false"`

<span data-ttu-id="73a2b-130">Cette commande crée un répertoire nommé `WordCount` à l’emplacement actuel de hello, qui contient un projet de base Maven.</span><span class="sxs-lookup"><span data-stu-id="73a2b-130">This command creates a directory named `WordCount` at hello current location, which contains a basic Maven project.</span></span> <span data-ttu-id="73a2b-131">Hello `WordCount` répertoire contient hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="73a2b-131">hello `WordCount` directory contains hello following items:</span></span>

* <span data-ttu-id="73a2b-132">`pom.xml`: Contient les paramètres de projet de Maven hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-132">`pom.xml`: Contains settings for hello Maven project.</span></span>
* <span data-ttu-id="73a2b-133">`src\main\java\com\microsoft\example` : contient votre code d’application.</span><span class="sxs-lookup"><span data-stu-id="73a2b-133">`src\main\java\com\microsoft\example`: Contains your application code.</span></span>
* <span data-ttu-id="73a2b-134">`src\test\java\com\microsoft\example` : contient des tests pour votre application.</span><span class="sxs-lookup"><span data-stu-id="73a2b-134">`src\test\java\com\microsoft\example`: Contains tests for your application.</span></span> 

### <a name="remove-hello-generated-example-code"></a><span data-ttu-id="73a2b-135">Supprimer l’exemple de code hello généré</span><span class="sxs-lookup"><span data-stu-id="73a2b-135">Remove hello generated example code</span></span>

<span data-ttu-id="73a2b-136">Supprimer les fichiers d’application hello et de test de hello généré :</span><span class="sxs-lookup"><span data-stu-id="73a2b-136">Delete hello generated test and hello application files:</span></span>

* <span data-ttu-id="73a2b-137">**src\test\java\com\microsoft\example\AppTest.java**</span><span class="sxs-lookup"><span data-stu-id="73a2b-137">**src\test\java\com\microsoft\example\AppTest.java**</span></span>
* <span data-ttu-id="73a2b-138">**src\main\java\com\microsoft\example\App.java**</span><span class="sxs-lookup"><span data-stu-id="73a2b-138">**src\main\java\com\microsoft\example\App.java**</span></span>

## <a name="add-maven-repositories"></a><span data-ttu-id="73a2b-139">Ajouter des référentiels Maven</span><span class="sxs-lookup"><span data-stu-id="73a2b-139">Add Maven repositories</span></span>

<span data-ttu-id="73a2b-140">HDInsight est basée sur hello Hortonworks Data Platform (HDP), nous vous recommandons d’à l’aide des dépendances de toodownload référentiel hello Hortonworks pour vos projets d’Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="73a2b-140">HDInsight is based on hello Hortonworks Data Platform (HDP), so we recommend using hello Hortonworks repository toodownload dependencies for your Apache Storm projects.</span></span> <span data-ttu-id="73a2b-141">Bonjour __pom.xml__ , ajoutez hello XML suivant après hello `<url>http://maven.apache.org</url>` ligne :</span><span class="sxs-lookup"><span data-stu-id="73a2b-141">In hello __pom.xml__ file, add hello following XML after hello `<url>http://maven.apache.org</url>` line:</span></span>

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

## <a name="add-properties"></a><span data-ttu-id="73a2b-142">Ajout de propriétés</span><span class="sxs-lookup"><span data-stu-id="73a2b-142">Add properties</span></span>

<span data-ttu-id="73a2b-143">Maven vous permet de valeurs au niveau du projet de toodefine appelées propriétés.</span><span class="sxs-lookup"><span data-stu-id="73a2b-143">Maven allows you toodefine project-level values called properties.</span></span> <span data-ttu-id="73a2b-144">Bonjour __pom.xml__, ajouter hello après le texte après hello `</repositories>` ligne :</span><span class="sxs-lookup"><span data-stu-id="73a2b-144">In hello __pom.xml__, add hello following text after hello `</repositories>` line:</span></span>

```xml
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <!--
    This is a version of Storm from hello Hortonworks repository that is compatible with HDInsight.
    -->
    <storm.version>1.0.1.2.5.3.0-37</storm.version>
</properties>
```

<span data-ttu-id="73a2b-145">Vous pouvez maintenant utiliser cette valeur dans d’autres sections de hello `pom.xml`.</span><span class="sxs-lookup"><span data-stu-id="73a2b-145">You can now use this value in other sections of hello `pom.xml`.</span></span> <span data-ttu-id="73a2b-146">Par exemple, lors de la spécification de version hello des composants de Storm, vous pouvez utiliser `${storm.version}` au lieu de manière irréversible une valeur.</span><span class="sxs-lookup"><span data-stu-id="73a2b-146">For example, when specifying hello version of Storm components, you can use `${storm.version}` instead of hard coding a value.</span></span>

## <a name="add-dependencies"></a><span data-ttu-id="73a2b-147">Ajout de dépendances</span><span class="sxs-lookup"><span data-stu-id="73a2b-147">Add dependencies</span></span>

<span data-ttu-id="73a2b-148">Ajoutez une dépendance pour les composants Storm.</span><span class="sxs-lookup"><span data-stu-id="73a2b-148">Add a dependency for Storm components.</span></span> <span data-ttu-id="73a2b-149">Ouvrez hello `pom.xml` et ajoutez hello suivant code Bonjour `<dependencies>` section :</span><span class="sxs-lookup"><span data-stu-id="73a2b-149">Open hello `pom.xml` file and add hello following code in hello `<dependencies>` section:</span></span>

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>${storm.version}</version>
    <!-- keep storm out of hello jar-with-dependencies -->
    <scope>provided</scope>
</dependency>
```

<span data-ttu-id="73a2b-150">Au moment de la compilation, Maven utilise cette toolook informations `storm-core` dans le référentiel de Maven hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-150">At compile time, Maven uses this information toolook up `storm-core` in hello Maven repository.</span></span> <span data-ttu-id="73a2b-151">Il recherche tout d’abord dans le référentiel hello sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="73a2b-151">It first looks in hello repository on your local computer.</span></span> <span data-ttu-id="73a2b-152">Si les fichiers hello ne sont pas, Maven les télécharge à partir du référentiel de Maven publique hello et les stocke dans le référentiel local de hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-152">If hello files aren't there, Maven downloads them from hello public Maven repository and stores them in hello local repository.</span></span>

> [!NOTE]
> <span data-ttu-id="73a2b-153">Hello d’avis `<scope>provided</scope>` ligne dans cette section.</span><span class="sxs-lookup"><span data-stu-id="73a2b-153">Notice hello `<scope>provided</scope>` line in this section.</span></span> <span data-ttu-id="73a2b-154">Ce paramètre indique à Maven tooexclude **storm cœur** à partir de tous les fichiers JAR créés, car elle est fournie par le système de hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-154">This setting tells Maven tooexclude **storm-core** from any JAR files that are created, because it is provided by hello system.</span></span>

## <a name="build-configuration"></a><span data-ttu-id="73a2b-155">Configuration de build</span><span class="sxs-lookup"><span data-stu-id="73a2b-155">Build configuration</span></span>

<span data-ttu-id="73a2b-156">Plug-ins de Maven autoriser étapes de build toocustomize hello du projet de hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-156">Maven plug-ins allow you toocustomize hello build stages of hello project.</span></span> <span data-ttu-id="73a2b-157">Par exemple, comment le projet de hello est compilé ou comment toopackage dans un fichier JAR.</span><span class="sxs-lookup"><span data-stu-id="73a2b-157">For example, how hello project is compiled or how toopackage it into a JAR file.</span></span> <span data-ttu-id="73a2b-158">Ouvrez hello `pom.xml` et ajoutez hello suivant code directement au-dessus hello `</project>` ligne.</span><span class="sxs-lookup"><span data-stu-id="73a2b-158">Open hello `pom.xml` file and add hello following code directly above hello `</project>` line.</span></span>

```xml
<build>
    <plugins>
    </plugins>
    <resources>
    </resources>
</build>
```

<span data-ttu-id="73a2b-159">Cette section est tooadd utilisé plug-ins, les ressources et les autres options de configuration de build.</span><span class="sxs-lookup"><span data-stu-id="73a2b-159">This section is used tooadd plug-ins, resources, and other build configuration options.</span></span> <span data-ttu-id="73a2b-160">Pour des informations complètes de hello **pom.xml** de fichiers, consultez [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span><span class="sxs-lookup"><span data-stu-id="73a2b-160">For a full reference of hello **pom.xml** file, see [http://maven.apache.org/pom.html](http://maven.apache.org/pom.html).</span></span>

### <a name="add-plug-ins"></a><span data-ttu-id="73a2b-161">Ajout de plug-ins</span><span class="sxs-lookup"><span data-stu-id="73a2b-161">Add plug-ins</span></span>

<span data-ttu-id="73a2b-162">Pour les topologies d’Apache Storm implémentées en Java, hello [plug-in de Maven Exec](http://www.mojohaus.org/exec-maven-plugin/) est utile car elle vous permet de tooeasily exécuter topologie de hello localement dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="73a2b-162">For Apache Storm topologies implemented in Java, hello [Exec Maven Plugin](http://www.mojohaus.org/exec-maven-plugin/) is useful because it allows you tooeasily run hello topology locally in your development environment.</span></span> <span data-ttu-id="73a2b-163">Ajouter hello suivant toohello `<plugins>` section Hello `pom.xml` fichier plug-in de tooinclude hello Exec Maven :</span><span class="sxs-lookup"><span data-stu-id="73a2b-163">Add hello following toohello `<plugins>` section of hello `pom.xml` file tooinclude hello Exec Maven plugin:</span></span>

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

<span data-ttu-id="73a2b-164">Un autre utile plug-in est hello [le plug-in du compilateur Apache Maven](http://maven.apache.org/plugins/maven-compiler-plugin/), qui est utilisé toochange options de compilation.</span><span class="sxs-lookup"><span data-stu-id="73a2b-164">Another useful plug-in is hello [Apache Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/), which is used toochange compilation options.</span></span> <span data-ttu-id="73a2b-165">modifications de Hello hello version Java Maven utilise pour la source de hello et la cible de votre application.</span><span class="sxs-lookup"><span data-stu-id="73a2b-165">hello changes hello Java version that Maven uses for hello source and target for your application.</span></span>

* <span data-ttu-id="73a2b-166">Pour HDInsight __3.4 ou une version antérieure__, définissez hello source et cible Java version too__1.7__.</span><span class="sxs-lookup"><span data-stu-id="73a2b-166">For HDInsight __3.4 or earlier__, set hello source and target Java version too__1.7__.</span></span>

* <span data-ttu-id="73a2b-167">Pour HDInsight __3.5__, définissez hello source et cible Java version too__1.8__.</span><span class="sxs-lookup"><span data-stu-id="73a2b-167">For HDInsight __3.5__, set hello source and target Java version too__1.8__.</span></span>

<span data-ttu-id="73a2b-168">Ajouter hello suit texte Bonjour `<plugins>` section Hello `pom.xml` fichier plug-in de tooinclude hello Apache Maven compilateur.</span><span class="sxs-lookup"><span data-stu-id="73a2b-168">Add hello following text in hello `<plugins>` section of hello `pom.xml` file tooinclude hello Apache Maven Compiler plugin.</span></span> <span data-ttu-id="73a2b-169">Cet exemple spécifie 1.8, afin de la version de HDInsight cible hello est 3.5.</span><span class="sxs-lookup"><span data-stu-id="73a2b-169">This example specifies 1.8, so hello target HDInsight version is 3.5.</span></span>

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

### <a name="configure-resources"></a><span data-ttu-id="73a2b-170">Configuration des ressources</span><span class="sxs-lookup"><span data-stu-id="73a2b-170">Configure resources</span></span>

<span data-ttu-id="73a2b-171">section de ressources Hello vous permet de ressources de non code tooinclude tels que les fichiers de configuration requis par les composants dans une topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-171">hello resources section allows you tooinclude non-code resources such as configuration files needed by components in hello topology.</span></span> <span data-ttu-id="73a2b-172">Pour cet exemple, ajoutez hello suit texte Bonjour `<resources>` section Hello ' pom.xml fichier.</span><span class="sxs-lookup"><span data-stu-id="73a2b-172">For this example, add hello following text in hello `<resources>` section of hello \`pom.xml file.</span></span>

```xml
<resource>
    <directory>${basedir}/resources</directory>
    <filtering>false</filtering>
    <includes>
        <include>log4j2.xml</include>
    </includes>
</resource>
```

<span data-ttu-id="73a2b-173">Cet exemple ajoute le répertoire des ressources hello dans racine hello du projet de hello (`${basedir}`) en tant qu’emplacement qui contient des ressources et inclut le fichier hello nommé `log4j2.xml`.</span><span class="sxs-lookup"><span data-stu-id="73a2b-173">This example adds hello resources directory in hello root of hello project (`${basedir}`) as a location that contains resources, and includes hello file named `log4j2.xml`.</span></span> <span data-ttu-id="73a2b-174">Ce fichier est utilisé tooconfigure quelles informations sont enregistrées par la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-174">This file is used tooconfigure what information is logged by hello topology.</span></span>

## <a name="create-hello-topology"></a><span data-ttu-id="73a2b-175">Créer la topologie de hello</span><span class="sxs-lookup"><span data-stu-id="73a2b-175">Create hello topology</span></span>

<span data-ttu-id="73a2b-176">Une topologie Apache Storm basée sur Java comprend trois composants que vous devez créer (ou référencer) en tant que dépendance.</span><span class="sxs-lookup"><span data-stu-id="73a2b-176">A Java-based Apache Storm topology consists of three components that you must author (or reference) as a dependency.</span></span>

* <span data-ttu-id="73a2b-177">**Becs verseurs amovibles**: lit les sources de données externes et émet des flux de données dans la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-177">**Spouts**: Reads data from external sources and emits streams of data into hello topology.</span></span>

* <span data-ttu-id="73a2b-178">**Les bolts**: effectuent le traitement des flux de données émis par les spouts ou les autres bolts et émettent un ou plusieurs flux.</span><span class="sxs-lookup"><span data-stu-id="73a2b-178">**Bolts**: Performs processing on streams emitted by spouts or other bolts, and emits one or more streams.</span></span>

* <span data-ttu-id="73a2b-179">**Topologie**: définit le mode hello becs verseurs amovibles et boulons sont organisées et fournit un point d’entrée hello pour la topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-179">**Topology**: Defines how hello spouts and bolts are arranged, and provides hello entry point for hello topology.</span></span>

### <a name="create-hello-spout"></a><span data-ttu-id="73a2b-180">Créer les bec hello</span><span class="sxs-lookup"><span data-stu-id="73a2b-180">Create hello spout</span></span>

<span data-ttu-id="73a2b-181">configuration tooreduce pour des sources de données externes, hello suivant bec émet simplement des phrases aléatoires.</span><span class="sxs-lookup"><span data-stu-id="73a2b-181">tooreduce requirements for setting up external data sources, hello following spout simply emits random sentences.</span></span> <span data-ttu-id="73a2b-182">Il s’agit d’une version modifiée d’un bec qui est fourni avec hello [exemples de Storm-Starter](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span><span class="sxs-lookup"><span data-stu-id="73a2b-182">It is a modified version of a spout that is provided with hello [Storm-Starter examples](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter).</span></span>

> [!NOTE]
> <span data-ttu-id="73a2b-183">Pour obtenir un exemple d’un bec qui lit à partir d’une source de données externes, consultez une des hello exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="73a2b-183">For an example of a spout that reads from an external data source, see one of hello following examples:</span></span>
>
> * <span data-ttu-id="73a2b-184">[TwitterSampleSpout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): un exemple de spout qui lit à partir de Twitter</span><span class="sxs-lookup"><span data-stu-id="73a2b-184">[TwitterSampleSPout](https://github.com/apache/storm/blob/0.10.x-branch/examples/storm-starter/src/jvm/storm/starter/spout/TwitterSampleSpout.java): An example spout that reads from Twitter</span></span>
> * <span data-ttu-id="73a2b-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): un spout qui lit à partir de Kafka</span><span class="sxs-lookup"><span data-stu-id="73a2b-185">[Storm-Kafka](https://github.com/apache/storm/tree/0.10.x-branch/external/storm-kafka): A spout that reads from Kafka</span></span>

<span data-ttu-id="73a2b-186">Pour un bec hello, créez un fichier nommé `RandomSentenceSpout.java` Bonjour `src\main\java\com\microsoft\example` hello active et l’utilisation suivante du code Java en tant que contenu de hello :</span><span class="sxs-lookup"><span data-stu-id="73a2b-186">For hello spout, create a file named `RandomSentenceSpout.java` in hello `src\main\java\com\microsoft\example` directory and use hello following Java code as hello contents:</span></span>

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
  //Collector used tooemit output
  SpoutOutputCollector _collector;
  //Used toogenerate a random number
  Random _rand;

  //Open is called when an instance of hello class is created
  @Override
  public void open(Map conf, TopologyContext context, SpoutOutputCollector collector) {
  //Set hello instance collector toohello one passed in
    _collector = collector;
    //For randomness
    _rand = new Random();
  }

  //Emit data toohello stream
  @Override
  public void nextTuple() {
  //Sleep for a bit
    Utils.sleep(100);
    //hello sentences that are randomly emitted
    String[] sentences = new String[]{ "hello cow jumped over hello moon", "an apple a day keeps hello doctor away",
        "four score and seven years ago", "snow white and hello seven dwarfs", "i am at two with nature" };
    //Randomly pick a sentence
    String sentence = sentences[_rand.nextInt(sentences.length)];
    //Emit hello sentence
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

  //Declare hello output fields. In this case, an sentence
  @Override
  public void declareOutputFields(OutputFieldsDeclarer declarer) {
    declarer.declare(new Fields("sentence"));
  }
}
```

> [!NOTE]
> <span data-ttu-id="73a2b-187">Bien que cette topologie n'utilise qu’un seul bec, d’autres peuvent en avoir plusieurs ce flux de données à partir de différentes sources dans une topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-187">Although this topology uses only one spout, others may have several that feed data from different sources into hello topology.</span></span>

### <a name="create-hello-bolts"></a><span data-ttu-id="73a2b-188">Créer hello boulons</span><span class="sxs-lookup"><span data-stu-id="73a2b-188">Create hello bolts</span></span>

<span data-ttu-id="73a2b-189">Boulons gèrent le traitement des données hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-189">Bolts handle hello data processing.</span></span> <span data-ttu-id="73a2b-190">Cette topologie utilise deux bolts :</span><span class="sxs-lookup"><span data-stu-id="73a2b-190">This topology uses two bolts:</span></span>

* <span data-ttu-id="73a2b-191">**SplitSentence**: fractionne les phrases hello émis par **RandomSentenceSpout** en mots individuels.</span><span class="sxs-lookup"><span data-stu-id="73a2b-191">**SplitSentence**: Splits hello sentences emitted by **RandomSentenceSpout** into individual words.</span></span>

* <span data-ttu-id="73a2b-192">**WordCount**: compte le nombre d’occurrences de chaque mot.</span><span class="sxs-lookup"><span data-stu-id="73a2b-192">**WordCount**: Counts how many times each word has occurred.</span></span>

> [!NOTE]
> <span data-ttu-id="73a2b-193">Boulons faire quoi que ce soit, par exemple, le calcul, persistance ou communiquer avec les composants tooexternal.</span><span class="sxs-lookup"><span data-stu-id="73a2b-193">Bolts can do anything, for example, computation, persistence, or talking tooexternal components.</span></span>

<span data-ttu-id="73a2b-194">Créez deux nouveaux fichiers, `SplitSentence.java` et `WordCount.java` Bonjour `src\main\java\com\microsoft\example` active.</span><span class="sxs-lookup"><span data-stu-id="73a2b-194">Create two new files, `SplitSentence.java` and `WordCount.java` in hello `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="73a2b-195">Utilisez hello après le texte en tant que contenu hello pour les fichiers de hello :</span><span class="sxs-lookup"><span data-stu-id="73a2b-195">Use hello following text as hello contents for hello files:</span></span>

#### <a name="splitsentence"></a><span data-ttu-id="73a2b-196">SplitSentence</span><span class="sxs-lookup"><span data-stu-id="73a2b-196">SplitSentence</span></span>

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

  //Execute is called tooprocess tuples
  @Override
  public void execute(Tuple tuple, BasicOutputCollector collector) {
    //Get hello sentence content from hello tuple
    String sentence = tuple.getString(0);
    //An iterator tooget each word
    BreakIterator boundary=BreakIterator.getWordInstance();
    //Give hello iterator hello sentence
    boundary.setText(sentence);
    //Find hello beginning first word
    int start=boundary.first();
    //Iterate over each word and emit it toohello output stream
    for (int end=boundary.next(); end != BreakIterator.DONE; start=end, end=boundary.next()) {
      //get hello word
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

#### <a name="wordcount"></a><span data-ttu-id="73a2b-197">WordCount</span><span class="sxs-lookup"><span data-stu-id="73a2b-197">WordCount</span></span>

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
  //How often tooemit a count of words
  private Integer emitFrequency;

  // Default constructor
  public WordCount() {
      emitFrequency=5; // Default too60 seconds
  }

  // Constructor that sets emit frequency
  public WordCount(Integer frequency) {
      emitFrequency=frequency;
  }

  //Configure frequency of tick tuples for this bolt
  //This delivers a 'tick' tuple on a specific interval,
  //which is used tootrigger certain actions
  @Override
  public Map<String, Object> getComponentConfiguration() {
      Config conf = new Config();
      conf.put(Config.TOPOLOGY_TICK_TUPLE_FREQ_SECS, emitFrequency);
      return conf;
  }

  //execute is called tooprocess tuples
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
      //Get hello word contents from hello tuple
      String word = tuple.getString(0);
      //Have we counted any already?
      Integer count = counts.get(word);
      if (count == null)
        count = 0;
      //Increment hello count and store it
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

### <a name="define-hello-topology"></a><span data-ttu-id="73a2b-198">Définir la topologie de hello</span><span class="sxs-lookup"><span data-stu-id="73a2b-198">Define hello topology</span></span>

<span data-ttu-id="73a2b-199">topologie de Hello lie becs verseurs de hello et boulons ensemble dans un graphique, qui définit comment les données circulent entre les composants de hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-199">hello topology ties hello spouts and bolts together into a graph, which defines how data flows between hello components.</span></span> <span data-ttu-id="73a2b-200">Il fournit également des indications de parallélisme Storm utilise lors de la création d’instances des composants hello au sein du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-200">It also provides parallelism hints that Storm uses when creating instances of hello components within hello cluster.</span></span>

<span data-ttu-id="73a2b-201">Hello image suivante est un schéma de base de graphique de hello des composants pour cette topologie.</span><span class="sxs-lookup"><span data-stu-id="73a2b-201">hello following image is a basic diagram of hello graph of components for this topology.</span></span>

![hello d’affichage de diagramme becs verseurs amovibles et boulons arrangement](./media/hdinsight-storm-develop-java-topology/wordcount-topology.png)

<span data-ttu-id="73a2b-203">tooimplement hello topologie, créez un fichier nommé `WordCountTopology.java` Bonjour `src\main\java\com\microsoft\example` active.</span><span class="sxs-lookup"><span data-stu-id="73a2b-203">tooimplement hello topology, create a file named `WordCountTopology.java` in hello `src\main\java\com\microsoft\example` directory.</span></span> <span data-ttu-id="73a2b-204">Utilisez hello suivant le code Java en tant que contenu hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="73a2b-204">Use hello following Java code as hello contents of hello file:</span></span>

```java
package com.microsoft.example;

import org.apache.storm.Config;
import org.apache.storm.LocalCluster;
import org.apache.storm.StormSubmitter;
import org.apache.storm.topology.TopologyBuilder;
import org.apache.storm.tuple.Fields;

import com.microsoft.example.RandomSentenceSpout;

public class WordCountTopology {

  //Entry point for hello topology
  public static void main(String[] args) throws Exception {
  //Used toobuild hello topology
    TopologyBuilder builder = new TopologyBuilder();
    //Add hello spout, with a name of 'spout'
    //and parallelism hint of 5 executors
    builder.setSpout("spout", new RandomSentenceSpout(), 5);
    //Add hello SplitSentence bolt, with a name of 'split'
    //and parallelism hint of 8 executors
    //shufflegrouping subscribes toohello spout, and equally distributes
    //tuples (sentences) across instances of hello SplitSentence bolt
    builder.setBolt("split", new SplitSentence(), 8).shuffleGrouping("spout");
    //Add hello counter, with a name of 'count'
    //and parallelism hint of 12 executors
    //fieldsgrouping subscribes toohello split bolt, and
    //ensures that hello same word is sent toohello same instance (group by field 'word')
    builder.setBolt("count", new WordCount(), 12).fieldsGrouping("split", new Fields("word"));

    //new configuration
    Config conf = new Config();
    //Set toofalse toodisable debug information when
    // running in production on a cluster
    conf.setDebug(false);

    //If there are arguments, we are running on a cluster
    if (args != null && args.length > 0) {
      //parallelism hint tooset hello number of workers
      conf.setNumWorkers(3);
      //submit hello topology
      StormSubmitter.submitTopology(args[0], conf, builder.createTopology());
    }
    //Otherwise, we are running locally
    else {
      //Cap hello maximum number of executors that can be spawned
      //for a component too3
      conf.setMaxTaskParallelism(3);
      //LocalCluster is used toorun locally
      LocalCluster cluster = new LocalCluster();
      //submit hello topology
      cluster.submitTopology("word-count", conf, builder.createTopology());
      //sleep
      Thread.sleep(10000);
      //shut down hello cluster
      cluster.shutdown();
    }
  }
}
```

### <a name="configure-logging"></a><span data-ttu-id="73a2b-205">Configuration de la journalisation</span><span class="sxs-lookup"><span data-stu-id="73a2b-205">Configure logging</span></span>

<span data-ttu-id="73a2b-206">Storm utilise Apache Log4j toolog informations.</span><span class="sxs-lookup"><span data-stu-id="73a2b-206">Storm uses Apache Log4j toolog information.</span></span> <span data-ttu-id="73a2b-207">Si vous ne configurez pas la journalisation, la topologie de hello émet des informations de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="73a2b-207">If you do not configure logging, hello topology emits diagnostic information.</span></span> <span data-ttu-id="73a2b-208">toocontrol éléments enregistrés, créez un fichier nommé `log4j2.xml` Bonjour `resources` active.</span><span class="sxs-lookup"><span data-stu-id="73a2b-208">toocontrol what is logged, create a file named `log4j2.xml` in hello `resources` directory.</span></span> <span data-ttu-id="73a2b-209">Utilisez hello XML suivant comme contenu hello du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-209">Use hello following XML as hello contents of hello file.</span></span>

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

<span data-ttu-id="73a2b-210">Ce code XML configure un nouvel enregistreur d’événements pour hello `com.microsoft.example` (classe), qui inclut les composants hello dans cet exemple de topologie.</span><span class="sxs-lookup"><span data-stu-id="73a2b-210">This XML configures a new logger for hello `com.microsoft.example` class, which includes hello components in this example topology.</span></span> <span data-ttu-id="73a2b-211">niveau de Hello a la valeur tootrace pour cet enregistreur d’événements, qui capture toutes les informations de journalisation émises par les composants dans cette topologie.</span><span class="sxs-lookup"><span data-stu-id="73a2b-211">hello level is set tootrace for this logger, which captures any logging information emitted by components in this topology.</span></span>

<span data-ttu-id="73a2b-212">Hello `<Root level="error">` section configure le niveau de journalisation racine du hello (pas dans tous les éléments `com.microsoft.example`) les informations sur l’erreur du journal tooonly.</span><span class="sxs-lookup"><span data-stu-id="73a2b-212">hello `<Root level="error">` section configures hello root level of logging (everything not in `com.microsoft.example`) tooonly log error information.</span></span>

<span data-ttu-id="73a2b-213">Pour plus d’informations sur la configuration de la journalisation pour Log4j, consultez [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span><span class="sxs-lookup"><span data-stu-id="73a2b-213">For more information on configuring logging for Log4j, see [http://logging.apache.org/log4j/2.x/manual/configuration.html](http://logging.apache.org/log4j/2.x/manual/configuration.html).</span></span>

> [!NOTE]
> <span data-ttu-id="73a2b-214">Storm version 0.10.0 et ultérieure utilisent Log4j 2.x.</span><span class="sxs-lookup"><span data-stu-id="73a2b-214">Storm version 0.10.0 and higher use Log4j 2.x.</span></span> <span data-ttu-id="73a2b-215">Les versions antérieures de Storm utilisaient Log4j 1.x, qui utilisait un autre format pour la configuration du journal.</span><span class="sxs-lookup"><span data-stu-id="73a2b-215">Older versions of storm used Log4j 1.x, which used a different format for log configuration.</span></span> <span data-ttu-id="73a2b-216">Pour plus d’informations sur la configuration antérieure hello, consultez [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span><span class="sxs-lookup"><span data-stu-id="73a2b-216">For information on hello older configuration, see [http://wiki.apache.org/logging-log4j/Log4jXmlFormat](http://wiki.apache.org/logging-log4j/Log4jXmlFormat).</span></span>

## <a name="test-hello-topology-locally"></a><span data-ttu-id="73a2b-217">Topologie de hello test localement</span><span class="sxs-lookup"><span data-stu-id="73a2b-217">Test hello topology locally</span></span>

<span data-ttu-id="73a2b-218">Après avoir enregistré les fichiers hello, utilisez hello suivant topologie commande tootest hello localement.</span><span class="sxs-lookup"><span data-stu-id="73a2b-218">After you save hello files, use hello following command tootest hello topology locally.</span></span>

```bash
mvn compile exec:java -Dstorm.topology=com.microsoft.example.WordCountTopology
```

<span data-ttu-id="73a2b-219">En cours d’exécution, la topologie de hello affiche des informations de démarrage.</span><span class="sxs-lookup"><span data-stu-id="73a2b-219">As it runs, hello topology displays startup information.</span></span> <span data-ttu-id="73a2b-220">Hello texte suivant est un exemple de sortie de nombre hello word :</span><span class="sxs-lookup"><span data-stu-id="73a2b-220">hello following text is an example of hello word count output:</span></span>

    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
    17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
    17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs
    17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word snow

<span data-ttu-id="73a2b-221">Cet exemple de journal indique le mot hello ' et ' a été émis 113 fois.</span><span class="sxs-lookup"><span data-stu-id="73a2b-221">This example log indicates that hello word 'and' has been emitted 113 times.</span></span> <span data-ttu-id="73a2b-222">Hello nombre continue toogo des tant que la topologie de hello s’exécute, car les bec hello émet en continu hello même phrase.</span><span class="sxs-lookup"><span data-stu-id="73a2b-222">hello count continues toogo up as long as hello topology runs because hello spout continuously emits hello same sentences.</span></span>

<span data-ttu-id="73a2b-223">Il existe un intervalle de 5 secondes entre l’émission des mots et les décomptes.</span><span class="sxs-lookup"><span data-stu-id="73a2b-223">There is a 5-second interval between emission of words and counts.</span></span> <span data-ttu-id="73a2b-224">Hello **WordCount** composant est configuré tooonly émettre des informations lors de l’arrivée d’un tuple de la graduation.</span><span class="sxs-lookup"><span data-stu-id="73a2b-224">hello **WordCount** component is configured tooonly emit information when a tick tuple arrives.</span></span> <span data-ttu-id="73a2b-225">Il demande que tuples de graduation soient remis uniquement toutes les cinq secondes.</span><span class="sxs-lookup"><span data-stu-id="73a2b-225">It requests that tick tuples are only delivered every five seconds.</span></span>

## <a name="convert-hello-topology-tooflux"></a><span data-ttu-id="73a2b-226">Convertir hello topologie tooFlux</span><span class="sxs-lookup"><span data-stu-id="73a2b-226">Convert hello topology tooFlux</span></span>

<span data-ttu-id="73a2b-227">Flux est une nouvelle infrastructure disponible avec Storm 0.10.0 et versions ultérieure, ce qui vous permet de configuration tooseparate à partir de l’implémentation.</span><span class="sxs-lookup"><span data-stu-id="73a2b-227">Flux is a new framework available with Storm 0.10.0 and higher, which allows you tooseparate configuration from implementation.</span></span> <span data-ttu-id="73a2b-228">Vos composants sont toujours définies dans Java, mais la topologie de hello est définie à l’aide d’un fichier YAML.</span><span class="sxs-lookup"><span data-stu-id="73a2b-228">Your components are still defined in Java, but hello topology is defined using a YAML file.</span></span> <span data-ttu-id="73a2b-229">Vous pouvez empaqueter une définition de la topologie par défaut avec votre projet, ou utiliser un fichier autonome lors de l’envoi de topologie de hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-229">You can package a default topology definition with your project, or use a standalone file when submitting hello topology.</span></span> <span data-ttu-id="73a2b-230">Lors de la soumission hello topologie tooStorm, vous pouvez utiliser les valeurs de toopopulate de fichiers de configuration ou les variables d’environnement dans la définition de la topologie YAML de hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-230">When submitting hello topology tooStorm, you can use environment variables or configuration files toopopulate values in hello YAML topology definition.</span></span>

<span data-ttu-id="73a2b-231">fichier YAML Hello définit toouse de composants hello pour la topologie de hello et hello des flux de données entre eux.</span><span class="sxs-lookup"><span data-stu-id="73a2b-231">hello YAML file defines hello components toouse for hello topology and hello data flow between them.</span></span> <span data-ttu-id="73a2b-232">Vous pouvez inclure un fichier YAML en tant que partie du fichier jar de hello, ou vous pouvez utiliser un fichier YAML externe.</span><span class="sxs-lookup"><span data-stu-id="73a2b-232">You can include a YAML file as part of hello jar file or you can use an external YAML file.</span></span>

<span data-ttu-id="73a2b-233">Pour plus d’informations sur Flux, voir [Infrastructure Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="73a2b-233">For more information on Flux, see [Flux framework (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

> [!WARNING]
> <span data-ttu-id="73a2b-234">Échéance tooa [bogue (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) Storm 1.0.1, vous devrez peut-être tooinstall un [environnement de développement Storm](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun les topologies de Flux localement.</span><span class="sxs-lookup"><span data-stu-id="73a2b-234">Due tooa [bug (https://issues.apache.org/jira/browse/STORM-2055)](https://issues.apache.org/jira/browse/STORM-2055) with Storm 1.0.1, you may need tooinstall a [Storm development environment](https://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) toorun Flux topologies locally.</span></span>

1. <span data-ttu-id="73a2b-235">Déplacer hello `WordCountTopology.java` fichier de projet de hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-235">Move hello `WordCountTopology.java` file out of hello project.</span></span> <span data-ttu-id="73a2b-236">Auparavant, ce fichier définis de topologie de hello, mais n’est pas nécessaire avec le Flux.</span><span class="sxs-lookup"><span data-stu-id="73a2b-236">Previously, this file defined hello topology, but isn't needed with Flux.</span></span>

2. <span data-ttu-id="73a2b-237">Bonjour `resources` répertoire, créez un fichier nommé `topology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="73a2b-237">In hello `resources` directory, create a file named `topology.yaml`.</span></span> <span data-ttu-id="73a2b-238">Utilisez hello après le texte en tant que contenu hello de ce fichier.</span><span class="sxs-lookup"><span data-stu-id="73a2b-238">Use hello following text as hello contents of this file.</span></span>

        name: "wordcount"       # friendly name for hello topology
        
        config:                 # Topology configuration
        topology.workers: 1     # Hint for hello number of workers toocreate
        
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
            from: "sentence-spout"       # hello stream emitter
            to: "splitter-bolt"          # hello stream consumer
            grouping:                    # Grouping type
                type: SHUFFLE
          
            - name: "Splitter -> Counter"
            from: "splitter-bolt"
            to: "counter-bolt"
            grouping:
            type: FIELDS
                args: ["word"]           # field(s) toogroup on

3. <span data-ttu-id="73a2b-239">Rendre hello suit les modifications toohello `pom.xml` fichier.</span><span class="sxs-lookup"><span data-stu-id="73a2b-239">Make hello following changes toohello `pom.xml` file.</span></span>
   
   * <span data-ttu-id="73a2b-240">Ajouter hello suivant nouvelle dépendance Bonjour `<dependencies>` section :</span><span class="sxs-lookup"><span data-stu-id="73a2b-240">Add hello following new dependency in hello `<dependencies>` section:</span></span>
     
        ```xml
        <!-- Add a dependency on hello Flux framework -->
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>flux-core</artifactId>
            <version>${storm.version}</version>
        </dependency>
        ```
   * <span data-ttu-id="73a2b-241">Ajouter hello suivant plug-in toohello `<plugins>` section.</span><span class="sxs-lookup"><span data-stu-id="73a2b-241">Add hello following plugin toohello `<plugins>` section.</span></span> <span data-ttu-id="73a2b-242">Ce plug-in gère la création d’un package (fichier jar) hello pour le projet de hello et applique certains tooFlux spécifique de transformations lors de la création de package de hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-242">This plugin handles hello creation of a package (jar file) for hello project, and applies some transformations specific tooFlux when creating hello package.</span></span>
     
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
                    <!-- We're using Flux, so refer tooit as main -->
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

   * <span data-ttu-id="73a2b-243">Bonjour **exec-maven plug-in** `<configuration>` section, modifiez la valeur hello pour `<mainClass>` trop`org.apache.storm.flux.Flux`.</span><span class="sxs-lookup"><span data-stu-id="73a2b-243">In hello **exec-maven-plugin** `<configuration>` section, change hello value for `<mainClass>` too`org.apache.storm.flux.Flux`.</span></span> <span data-ttu-id="73a2b-244">Ce paramètre permet de toohandle du Flux en cours d’exécution topologie de hello localement dans le développement.</span><span class="sxs-lookup"><span data-stu-id="73a2b-244">This setting allows Flux toohandle running hello topology locally in development.</span></span>

   * <span data-ttu-id="73a2b-245">Bonjour `<resources>` section, ajoutez hello suivant toohello `<includes>`.</span><span class="sxs-lookup"><span data-stu-id="73a2b-245">In hello `<resources>` section, add hello following toohello `<includes>`.</span></span> <span data-ttu-id="73a2b-246">Ce code XML inclut un fichier YAML hello qui définit la topologie de hello en tant que partie du projet de hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-246">This XML includes hello YAML file that defines hello topology as part of hello project.</span></span>

        ```xml
        <include>topology.yaml</include>
        ```

## <a name="test-hello-flux-topology-locally"></a><span data-ttu-id="73a2b-247">Topologie de flux hello test localement</span><span class="sxs-lookup"><span data-stu-id="73a2b-247">Test hello flux topology locally</span></span>

1. <span data-ttu-id="73a2b-248">Utilisez hello suivant toocompile et exécuter la topologie de Flux de hello à l’aide de Maven :</span><span class="sxs-lookup"><span data-stu-id="73a2b-248">Use hello following toocompile and execute hello Flux topology using Maven:</span></span>

    ```bash
    mvn compile exec:java -Dexec.args="--local -R /topology.yaml"
    ```

    <span data-ttu-id="73a2b-249">Si vous utilisez PowerShell, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="73a2b-249">If you are using PowerShell, use hello following command:</span></span>

    ```bash
    mvn compile exec:java "-Dexec.args=--local -R /topology.yaml"
    ```

    > [!WARNING]
    > <span data-ttu-id="73a2b-250">Si votre topologie utilise des bits Storm 1.0.1, cette commande échoue.</span><span class="sxs-lookup"><span data-stu-id="73a2b-250">If your topology uses Storm 1.0.1 bits, this command fails.</span></span> <span data-ttu-id="73a2b-251">Cet échec est dû à [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span><span class="sxs-lookup"><span data-stu-id="73a2b-251">This failure is caused by [https://issues.apache.org/jira/browse/STORM-2055](https://issues.apache.org/jira/browse/STORM-2055).</span></span> <span data-ttu-id="73a2b-252">Au lieu de cela, [installer Storm dans votre environnement de développement](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) et hello d’utiliser les informations suivantes.</span><span class="sxs-lookup"><span data-stu-id="73a2b-252">Instead, [install Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html) and use hello following information.</span></span>

    <span data-ttu-id="73a2b-253">Si vous avez [installé Storm dans votre environnement de développement](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), vous pouvez utiliser hello suivant à la place les commandes :</span><span class="sxs-lookup"><span data-stu-id="73a2b-253">If you have [installed Storm in your development environment](http://storm.apache.org/releases/0.10.0/Setting-up-development-environment.html), you can use hello following commands instead:</span></span>

    ```bash
    mvn compile package
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /topology.yaml
    ```

    <span data-ttu-id="73a2b-254">Hello `--local` paramètre exécute la topologie de hello en mode local sur votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="73a2b-254">hello `--local` parameter runs hello topology in local mode on your development environment.</span></span> <span data-ttu-id="73a2b-255">Hello `-R /topology.yaml` paramètre utilise hello `topology.yaml` ressource de fichier à partir de la topologie de hello jar fichier toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-255">hello `-R /topology.yaml` parameter uses hello `topology.yaml` file resource from hello jar file toodefine hello topology.</span></span>

    <span data-ttu-id="73a2b-256">En cours d’exécution, la topologie de hello affiche des informations de démarrage.</span><span class="sxs-lookup"><span data-stu-id="73a2b-256">As it runs, hello topology displays startup information.</span></span> <span data-ttu-id="73a2b-257">Hello suivant le texte est un exemple de sortie de hello :</span><span class="sxs-lookup"><span data-stu-id="73a2b-257">hello following text is an example of hello output:</span></span>

        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word snow
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 56 for word white
        17:33:27 [Thread-12-count] INFO  com.microsoft.example.WordCount - Emitting a count of 112 for word seven
        17:33:27 [Thread-16-count] INFO  com.microsoft.example.WordCount - Emitting a count of 195 for word the
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 113 for word and
        17:33:27 [Thread-30-count] INFO  com.microsoft.example.WordCount - Emitting a count of 57 for word dwarfs

    <span data-ttu-id="73a2b-258">Il existe un délai de 10 secondes entre chaque lot d’informations enregistrées.</span><span class="sxs-lookup"><span data-stu-id="73a2b-258">There is a 10-second delay between batches of logged information.</span></span>

2. <span data-ttu-id="73a2b-259">Effectuer une copie de hello `topology.yaml` fichier de projet de hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-259">Make a copy of hello `topology.yaml` file from hello project.</span></span> <span data-ttu-id="73a2b-260">Nouveau fichier de nom hello `newtopology.yaml`.</span><span class="sxs-lookup"><span data-stu-id="73a2b-260">Name hello new file `newtopology.yaml`.</span></span> <span data-ttu-id="73a2b-261">Bonjour `newtopology.yaml` de fichiers, Rechercher suivant de hello section et modifier la valeur hello `10` trop`5`.</span><span class="sxs-lookup"><span data-stu-id="73a2b-261">In hello `newtopology.yaml` file, find hello following section and change hello value of `10` too`5`.</span></span> <span data-ttu-id="73a2b-262">Compte de cet intervalle de hello modification modifications entre l’émission de lots de word à partir de too5 de 10 secondes.</span><span class="sxs-lookup"><span data-stu-id="73a2b-262">This modification changes hello interval between emitting batches of word counts from 10 seconds too5.</span></span>

    ```yaml
    - id: "counter-bolt"
    className: "com.microsoft.example.WordCount"
    constructorArgs:
    - 5
    parallelism: 1
    ```yaml

3. toorun hello topology, use hello following command:

    ```bash
    mvn exec:java -Dexec.args="--local /path/to/newtopology.yaml"
    ```

    <span data-ttu-id="73a2b-263">Ou, si vous avez Storm dans votre environnement de développement :</span><span class="sxs-lookup"><span data-stu-id="73a2b-263">Or, if you have Storm on your development environment:</span></span>

    ```bash
    storm jar target/WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local /path/to/newtopology.yaml
    ```

    <span data-ttu-id="73a2b-264">Hello de modification `/path/to/newtopology.yaml` toohello chemin d’accès toohello newtopology.yaml fichier créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-264">Change hello `/path/to/newtopology.yaml` toohello path toohello newtopology.yaml file you created in hello previous step.</span></span> <span data-ttu-id="73a2b-265">Cette commande utilise hello newtopology.yaml en tant que définition de la topologie hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-265">This command uses hello newtopology.yaml as hello topology definition.</span></span> <span data-ttu-id="73a2b-266">Étant donné que nous n’avez pas incluses hello `compile` paramètre, Maven utilise hello version de hello projet créé dans les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="73a2b-266">Since we didn't include hello `compile` parameter, Maven uses hello version of hello project built in previous steps.</span></span>

    <span data-ttu-id="73a2b-267">Une fois hello topologie démarre, vous devez remarquer que heure hello entre les traitements émis a changé de valeur hello tooreflect newtopology.yaml.</span><span class="sxs-lookup"><span data-stu-id="73a2b-267">Once hello topology starts, you should notice that hello time between emitted batches has changed tooreflect hello value in newtopology.yaml.</span></span> <span data-ttu-id="73a2b-268">Par conséquent, vous pouvez voir que vous pouvez modifier votre configuration via un fichier YAML sans avoir de topologie de hello toorecompile.</span><span class="sxs-lookup"><span data-stu-id="73a2b-268">So you can see that you can change your configuration through a YAML file without having toorecompile hello topology.</span></span>

<span data-ttu-id="73a2b-269">Pour plus d’informations sur d’autres fonctionnalités de l’infrastructure de Flux hello, consultez [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="73a2b-269">For more information on these and other features of hello Flux framework, see [Flux (https://storm.apache.org/releases/0.10.0/flux.html)](https://storm.apache.org/releases/0.10.0/flux.html).</span></span>

## <a name="trident"></a><span data-ttu-id="73a2b-270">Trident</span><span class="sxs-lookup"><span data-stu-id="73a2b-270">Trident</span></span>

<span data-ttu-id="73a2b-271">Trident est une abstraction de haut niveau fournie par Storm.</span><span class="sxs-lookup"><span data-stu-id="73a2b-271">Trident is a high-level abstraction that is provided by Storm.</span></span> <span data-ttu-id="73a2b-272">Il prend en charge le traitement avec état.</span><span class="sxs-lookup"><span data-stu-id="73a2b-272">It supports stateful processing.</span></span> <span data-ttu-id="73a2b-273">Hello principal avantage de Trident est qu’il peut garantir que chaque message qui entre dans la topologie de hello est traitée qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="73a2b-273">hello primary advantage of Trident is that it can guarantee that every message that enters hello topology is processed only once.</span></span> <span data-ttu-id="73a2b-274">Sans utilisation de Trident, votre topologie peut uniquement garantir que les messages sont traités au moins une fois.</span><span class="sxs-lookup"><span data-stu-id="73a2b-274">Without using Trident, your topology can only guarantee that messages are processed at least once.</span></span> <span data-ttu-id="73a2b-275">Il existe aussi d'autres différences, comme les composants intégrés pouvant être utilisés, plutôt que de créer des bolts.</span><span class="sxs-lookup"><span data-stu-id="73a2b-275">There are also other differences, such as built-in components that can be used instead of creating bolts.</span></span> <span data-ttu-id="73a2b-276">Les Bolts sont remplacés par des composants moins génériques, tels que des filtres, des projections et des fonctions.</span><span class="sxs-lookup"><span data-stu-id="73a2b-276">In fact, bolts are replaced by less-generic components, such as filters, projections, and functions.</span></span>

<span data-ttu-id="73a2b-277">Les applications Trident peuvent être créées à l’aide de projets Maven.</span><span class="sxs-lookup"><span data-stu-id="73a2b-277">Trident applications can be created by using Maven projects.</span></span> <span data-ttu-id="73a2b-278">Vous utilisez hello même étapes présenté plus haut dans cet article : uniquement le code hello est différent.</span><span class="sxs-lookup"><span data-stu-id="73a2b-278">You use hello same basic steps as presented earlier in this article—only hello code is different.</span></span> <span data-ttu-id="73a2b-279">Trident également (actuellement) sont inutilisables avec l’infrastructure de Flux hello.</span><span class="sxs-lookup"><span data-stu-id="73a2b-279">Trident also cannot (currently) be used with hello Flux framework.</span></span>

<span data-ttu-id="73a2b-280">Pour plus d’informations sur Trident, consultez hello [présentation de l’API Trident](http://storm.apache.org/documentation/Trident-API-Overview.html).</span><span class="sxs-lookup"><span data-stu-id="73a2b-280">For more information about Trident, see hello [Trident API Overview](http://storm.apache.org/documentation/Trident-API-Overview.html).</span></span>

<span data-ttu-id="73a2b-281">Pour obtenir un exemple d’application Trident, consultez les [Rubriques de tendances Twitter avec Apache Storm sur HDInsight](hdinsight-storm-twitter-trending.md).</span><span class="sxs-lookup"><span data-stu-id="73a2b-281">For an example of a Trident application, see [Twitter trending topics with Apache Storm on HDInsight](hdinsight-storm-twitter-trending.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="73a2b-282">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="73a2b-282">Next Steps</span></span>

<span data-ttu-id="73a2b-283">Vous avez appris comment toocreate une topologie Storm à l’aide de Java.</span><span class="sxs-lookup"><span data-stu-id="73a2b-283">You have learned how toocreate a Storm topology by using Java.</span></span> <span data-ttu-id="73a2b-284">Apprenez maintenant à effectuer les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="73a2b-284">Now learn how to:</span></span>

* [<span data-ttu-id="73a2b-285">Déploiement et gestion des topologies Apache Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="73a2b-285">Deploy and manage Apache Storm topologies on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)

* [<span data-ttu-id="73a2b-286">Développement de topologies C# pour Apache Storm dans HDInsight à l'aide de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="73a2b-286">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="73a2b-287">Vous trouverez davantage d’exemples de topologies Storm en vous rendant sur [Exemples de topologies Storm sur HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="73a2b-287">You can find more example Storm topologies by visiting [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

