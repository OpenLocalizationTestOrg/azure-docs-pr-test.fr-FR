---
title: aaaJava HBase client - Azure HDInsight | Documents Microsoft
description: "Découvrez comment toouse application de Apache HBase Apache Maven toobuild basé sur un Java, puis déployez-le tooHBase sur Azure HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: 
ms.assetid: 1d1ed180-e0f4-4d1c-b5ea-72e0eda643bc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 41ef92b2900280dd59089c4fa40686c44133b337
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-java-applications-for-apache-hbase"></a><span data-ttu-id="cf97a-103">Créer des applications Java pour Apache HBase</span><span class="sxs-lookup"><span data-stu-id="cf97a-103">Build Java applications for Apache HBase</span></span>

<span data-ttu-id="cf97a-104">Découvrez comment toocreate un [Apache HBase](http://hbase.apache.org/) application Java.</span><span class="sxs-lookup"><span data-stu-id="cf97a-104">Learn how toocreate an [Apache HBase](http://hbase.apache.org/) application in Java.</span></span> <span data-ttu-id="cf97a-105">Utilisez application hello avec HBase sur Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf97a-105">Then use hello application with HBase on Azure HDInsight.</span></span>

<span data-ttu-id="cf97a-106">Dans ce document, utilisez les étapes Hello [Maven](http://maven.apache.org/) toocreate et générer le projet hello.</span><span class="sxs-lookup"><span data-stu-id="cf97a-106">hello steps in this document use [Maven](http://maven.apache.org/) toocreate and build hello project.</span></span> <span data-ttu-id="cf97a-107">Maven est un outil de compréhension qui permet à votre logiciel toobuild, documentation et des rapports pour les projets de Java et de gestion de projets logiciels.</span><span class="sxs-lookup"><span data-stu-id="cf97a-107">Maven is a software project management and comprehension tool that allows you toobuild software, documentation, and reports for Java projects.</span></span>

> [!NOTE]
> <span data-ttu-id="cf97a-108">Hello étapes décrites dans ce document ont été récemment testés avec HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="cf97a-108">hello steps in this document were most recently tested with HDInsight 3.6.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf97a-109">étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Linux.</span><span class="sxs-lookup"><span data-stu-id="cf97a-109">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="cf97a-110">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="cf97a-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cf97a-111">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="cf97a-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="cf97a-112">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="cf97a-112">Requirements</span></span>

* <span data-ttu-id="cf97a-113">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 ou version supérieure.</span><span class="sxs-lookup"><span data-stu-id="cf97a-113">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 8 or later.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cf97a-114">HDInsight 3.5 et les versions ultérieures nécessitent Java 8.</span><span class="sxs-lookup"><span data-stu-id="cf97a-114">HDInsight 3.5 and greater requires Java 8.</span></span> <span data-ttu-id="cf97a-115">Les versions antérieures de HDInsight nécessitent Java 7.</span><span class="sxs-lookup"><span data-stu-id="cf97a-115">Earlier versions of HDInsight require Java 7.</span></span>

* [<span data-ttu-id="cf97a-116">Maven</span><span class="sxs-lookup"><span data-stu-id="cf97a-116">Maven</span></span>](http://maven.apache.org/)

* [<span data-ttu-id="cf97a-117">Un cluster Azure HDInsight sous Linux avec HBase</span><span class="sxs-lookup"><span data-stu-id="cf97a-117">A Linux-based Azure HDInsight cluster with HBase</span></span>](hdinsight-hbase-tutorial-get-started-linux.md#create-hbase-cluster)

  > [!NOTE]
  > <span data-ttu-id="cf97a-118">étapes Hello dans ce document ont été testés avec les versions de cluster HDInsight 3.4 et 3.5.</span><span class="sxs-lookup"><span data-stu-id="cf97a-118">hello steps in this document have been tested with HDInsight cluster versions 3.4 and 3.5.</span></span> <span data-ttu-id="cf97a-119">les valeurs par défaut Hello fournies dans les exemples sont pour un cluster HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="cf97a-119">hello default values provided in examples are for a HDInsight 3.5 cluster.</span></span>

## <a name="create-hello-project"></a><span data-ttu-id="cf97a-120">Créer le projet de hello</span><span class="sxs-lookup"><span data-stu-id="cf97a-120">Create hello project</span></span>

1. <span data-ttu-id="cf97a-121">À partir de la ligne de commande hello dans votre environnement de développement, modifiez les répertoires toohello emplacement souhaité projet hello de toocreate, par exemple, `cd code\hbase`.</span><span class="sxs-lookup"><span data-stu-id="cf97a-121">From hello command line in your development environment, change directories toohello location where you want toocreate hello project, for example, `cd code\hbase`.</span></span>

2. <span data-ttu-id="cf97a-122">Hello d’utilisation **mvn** commande, qui est installé avec Maven, hello toogenerate génération de modèles automatique pour le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="cf97a-122">Use hello **mvn** command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

    > [!NOTE]
    > <span data-ttu-id="cf97a-123">Si vous utilisez PowerShell, vous devez le placer hello `-D` paramètres dans des guillemets doubles.</span><span class="sxs-lookup"><span data-stu-id="cf97a-123">If you are using PowerShell, you must enclose hello `-D` parameters in double quotes.</span></span>
    >
    > `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=hbaseapp" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`

    <span data-ttu-id="cf97a-124">Cette commande crée un répertoire avec hello comme hello du même nom **artifactID** paramètre (**hbaseapp** dans cet exemple.) Ce répertoire contient hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="cf97a-124">This command creates a directory with hello same name as hello **artifactID** parameter (**hbaseapp** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="cf97a-125">**pom.XML**: hello du modèle objet Project ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contient des informations et la configuration du projet de hello détails utilisés toobuild.</span><span class="sxs-lookup"><span data-stu-id="cf97a-125">**pom.xml**:  hello Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used toobuild hello project.</span></span>
   * <span data-ttu-id="cf97a-126">**src**: répertoire hello contenant hello **principal/java/com/microsoft/exemples** répertoire, où vous créez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="cf97a-126">**src**: hello directory that contains hello **main/java/com/microsoft/examples** directory, where you author hello application.</span></span>

3. <span data-ttu-id="cf97a-127">Supprimer hello `src/test/java/com/microsoft/examples/apptest.java` fichier.</span><span class="sxs-lookup"><span data-stu-id="cf97a-127">Delete hello `src/test/java/com/microsoft/examples/apptest.java` file.</span></span> <span data-ttu-id="cf97a-128">Il n’est pas utilisé dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="cf97a-128">It is not be used in this example.</span></span>

## <a name="update-hello-project-object-model"></a><span data-ttu-id="cf97a-129">Mettre à jour hello modèle objet Project</span><span class="sxs-lookup"><span data-stu-id="cf97a-129">Update hello Project Object Model</span></span>

1. <span data-ttu-id="cf97a-130">Modifier hello `pom.xml` et ajoutez hello suivant du code à l’intérieur de hello `<dependencies>` section :</span><span class="sxs-lookup"><span data-stu-id="cf97a-130">Edit hello `pom.xml` file and add hello following code inside hello `<dependencies>` section:</span></span>

   ```xml
    <dependency>
        <groupId>org.apache.hbase</groupId>
        <artifactId>hbase-client</artifactId>
        <version>1.1.2</version>
    </dependency>
    <dependency>
        <groupId>org.apache.phoenix</groupId>
        <artifactId>phoenix-core</artifactId>
        <version>4.4.0-HBase-1.1</version>
    </dependency>
   ```

    <span data-ttu-id="cf97a-131">Cette section indique ce projet hello doit **hbase-client** et **phoenix cœur** composants.</span><span class="sxs-lookup"><span data-stu-id="cf97a-131">This section indicates that hello project needs **hbase-client** and **phoenix-core** components.</span></span> <span data-ttu-id="cf97a-132">Au moment de la compilation, ces dépendances sont téléchargés à partir du référentiel de Maven hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="cf97a-132">At compile time, these dependencies are downloaded from hello default Maven repository.</span></span> <span data-ttu-id="cf97a-133">Vous pouvez utiliser hello [recherche de référentiel centrale Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn plus d’informations sur cette dépendance.</span><span class="sxs-lookup"><span data-stu-id="cf97a-133">You can use hello [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="cf97a-134">numéro de version de Hello du client hello hbase doit correspondre au version hello de HBase qui est fourni avec votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf97a-134">hello version number of hello hbase-client must match hello version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="cf97a-135">Utilisez hello suivant le numéro de version correct de table toofind hello.</span><span class="sxs-lookup"><span data-stu-id="cf97a-135">Use hello following table toofind hello correct version number.</span></span>

   | <span data-ttu-id="cf97a-136">Version de cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="cf97a-136">HDInsight cluster version</span></span> | <span data-ttu-id="cf97a-137">HBase version toouse</span><span class="sxs-lookup"><span data-stu-id="cf97a-137">HBase version toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="cf97a-138">3.2</span><span class="sxs-lookup"><span data-stu-id="cf97a-138">3.2</span></span> |<span data-ttu-id="cf97a-139">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="cf97a-139">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="cf97a-140">3.3, 3.4, 3.5 et 3.6</span><span class="sxs-lookup"><span data-stu-id="cf97a-140">3.3, 3.4, 3.5, and 3.6</span></span> |<span data-ttu-id="cf97a-141">1.1.2</span><span class="sxs-lookup"><span data-stu-id="cf97a-141">1.1.2</span></span> |

    <span data-ttu-id="cf97a-142">Pour plus d’informations sur les composants et les versions de HDInsight, consultez [quels sont les composants Hadoop hello différents disponibles avec HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="cf97a-142">For more information on HDInsight versions and components, see [What are hello different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>

3. <span data-ttu-id="cf97a-143">Ajouter hello suivant code toohello **pom.xml** fichier.</span><span class="sxs-lookup"><span data-stu-id="cf97a-143">Add hello following code toohello **pom.xml** file.</span></span> <span data-ttu-id="cf97a-144">Ce texte doit être à l’intérieur de hello `<project>...</project>` balises Bonjour de fichiers, par exemple, entre `</dependencies>` et `</project>`.</span><span class="sxs-lookup"><span data-stu-id="cf97a-144">This text must be inside hello `<project>...</project>` tags in hello file, for example, between `</dependencies>` and `</project>`.</span></span>

   ```xml
    <build>
        <sourceDirectory>src</sourceDirectory>
        <resources>
        <resource>
            <directory>${basedir}/conf</directory>
            <filtering>false</filtering>
            <includes>
            <include>hbase-site.xml</include>
            </includes>
        </resource>
        </resources>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.3</version>
            <configuration>
                <source>1.8</source>
                <target>1.8</target>
            </configuration>
            </plugin>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-shade-plugin</artifactId>
            <version>2.3</version>
            <configuration>
            <transformers>
                <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer">
                </transformer>
            </transformers>
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

    <span data-ttu-id="cf97a-145">Cette section configure une ressource (`conf/hbase-site.xml`) contenant des informations de configuration pour HBase.</span><span class="sxs-lookup"><span data-stu-id="cf97a-145">This section configures a resource (`conf/hbase-site.xml`) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cf97a-146">Vous pouvez également définir les valeurs de configuration par code.</span><span class="sxs-lookup"><span data-stu-id="cf97a-146">You can also set configuration values via code.</span></span> <span data-ttu-id="cf97a-147">Consultez les commentaires hello Bonjour `CreateTable` exemple.</span><span class="sxs-lookup"><span data-stu-id="cf97a-147">See hello comments in hello `CreateTable` example.</span></span>

    <span data-ttu-id="cf97a-148">Cette section configure également hello [plug-in du compilateur Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) et [plug-in de la nuance Maven](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="cf97a-148">This section also configures hello [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="cf97a-149">compilateur Hello plug-in est utilisé toocompile hello topologie.</span><span class="sxs-lookup"><span data-stu-id="cf97a-149">hello compiler plug-in is used toocompile hello topology.</span></span> <span data-ttu-id="cf97a-150">ombre Hello plug-in est la duplication de licence tooprevent utilisés dans le package JAR hello qui est généré par Maven.</span><span class="sxs-lookup"><span data-stu-id="cf97a-150">hello shade plug-in is used tooprevent license duplication in hello JAR package that is built by Maven.</span></span> <span data-ttu-id="cf97a-151">Ce plug-in est tooprevent utilisé une erreur « dupliquer les fichiers de licence » en cours d’exécution sur le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="cf97a-151">This plugin is used tooprevent a "duplicate license files" error at run time on hello HDInsight cluster.</span></span> <span data-ttu-id="cf97a-152">À l’aide de maven-ton plug-in par hello `ApacheLicenseResourceTransformer` implémentation empêche l’erreur de hello.</span><span class="sxs-lookup"><span data-stu-id="cf97a-152">Using maven-shade-plugin with hello `ApacheLicenseResourceTransformer` implementation prevents hello error.</span></span>

    <span data-ttu-id="cf97a-153">Hello maven-ton-plugin génère également un fichier jar générale qui contient toutes les dépendances de hello requis par l’application hello.</span><span class="sxs-lookup"><span data-stu-id="cf97a-153">hello maven-shade-plugin also produces an uber jar that contains all hello dependencies required by hello application.</span></span>

4. <span data-ttu-id="cf97a-154">Enregistrer hello `pom.xml` fichier.</span><span class="sxs-lookup"><span data-stu-id="cf97a-154">Save hello `pom.xml` file.</span></span>

5. <span data-ttu-id="cf97a-155">Créez un répertoire nommé `conf` Bonjour `hbaseapp` active.</span><span class="sxs-lookup"><span data-stu-id="cf97a-155">Create a directory named `conf` in hello `hbaseapp` directory.</span></span> <span data-ttu-id="cf97a-156">Ce répertoire est toohold utilisé les informations de configuration pour la connexion tooHBase.</span><span class="sxs-lookup"><span data-stu-id="cf97a-156">This directory is used toohold configuration information for connecting tooHBase.</span></span>

6. <span data-ttu-id="cf97a-157">Configuration HBase toocopy hello hello HBase cluster toohello de commande suivant de hello utilisation `conf` active.</span><span class="sxs-lookup"><span data-stu-id="cf97a-157">Use hello following command toocopy hello HBase configuration from hello HBase cluster toohello `conf` directory.</span></span> <span data-ttu-id="cf97a-158">Remplacez `USERNAME` par nom hello de votre connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="cf97a-158">Replace `USERNAME` with hello name of your SSH login.</span></span> <span data-ttu-id="cf97a-159">Remplacez `CLUSTERNAME` par le nom de votre cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="cf97a-159">Replace `CLUSTERNAME` with your HDInsight cluster name:</span></span>

    ```bash
    scp USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml ./conf/hbase-site.xml
    ```

   <span data-ttu-id="cf97a-160">Pour plus d’informations sur l’utilisation de `ssh` et `scp`, voir [Utiliser SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="cf97a-160">For more information on using `ssh` and `scp`, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="cf97a-161">Créer l’application hello</span><span class="sxs-lookup"><span data-stu-id="cf97a-161">Create hello application</span></span>

1. <span data-ttu-id="cf97a-162">Accédez toohello `hbaseapp/src/main/java/com/microsoft/examples` active et renommer hello app.java fichier trop`CreateTable.java`.</span><span class="sxs-lookup"><span data-stu-id="cf97a-162">Go toohello `hbaseapp/src/main/java/com/microsoft/examples` directory and rename hello app.java file too`CreateTable.java`.</span></span>

2. <span data-ttu-id="cf97a-163">Ouvrez hello `CreateTable.java` de fichier et remplacez contenu hello hello suivant le texte :</span><span class="sxs-lookup"><span data-stu-id="cf97a-163">Open hello `CreateTable.java` file and replace hello existing contents with hello following text:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;
    import org.apache.hadoop.hbase.HTableDescriptor;
    import org.apache.hadoop.hbase.TableName;
    import org.apache.hadoop.hbase.HColumnDescriptor;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Put;
    import org.apache.hadoop.hbase.util.Bytes;

    public class CreateTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Example of setting zookeeper values for HDInsight
        // in code instead of an hbase-site.xml file
        //
        // config.set("hbase.zookeeper.quorum",
        //            "zookeepernode0,zookeepernode1,zookeepernode2");
        //config.set("hbase.zookeeper.property.clientPort", "2181");
        //config.set("hbase.cluster.distributed", "true");
        //
        //NOTE: Actual zookeeper host names can be found using Ambari:
        //curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/hosts"

        //Linux-based HDInsight clusters use /hbase-unsecure as hello znode parent
        config.set("zookeeper.znode.parent","/hbase-unsecure");

        // create an admin object using hello config
        HBaseAdmin admin = new HBaseAdmin(config);

        // create hello table...
        HTableDescriptor tableDescriptor = new HTableDescriptor(TableName.valueOf("people"));
        // ... with two column families
        tableDescriptor.addFamily(new HColumnDescriptor("name"));
        tableDescriptor.addFamily(new HColumnDescriptor("contactinfo"));
        admin.createTable(tableDescriptor);

        // define some people
        String[][] people = {
            { "1", "Marcel", "Haddad", "marcel@fabrikam.com"},
            { "2", "Franklin", "Holtz", "franklin@contoso.com" },
            { "3", "Dwayne", "McKee", "dwayne@fabrikam.com" },
            { "4", "Rae", "Schroeder", "rae@contoso.com" },
            { "5", "Rosalie", "burton", "rosalie@fabrikam.com"},
            { "6", "Gabriela", "Ingram", "gabriela@contoso.com"} };

        HTable table = new HTable(config, "people");

        // Add each person toohello table
        //   Use hello `name` column family for hello name
        //   Use hello `contactinfo` column family for hello email
        for (int i = 0; i< people.length; i++) {
            Put person = new Put(Bytes.toBytes(people[i][0]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
            person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
            person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
            table.put(person);
        }
        // flush commits and close hello table
        table.flushCommits();
        table.close();
        }
    }
   ```

    <span data-ttu-id="cf97a-164">Ce code est hello **CreateTable** (classe), ce qui crée une table nommée **personnes** et le remplir avec certains utilisateurs prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="cf97a-164">This code is hello **CreateTable** class, which creates a table named **people** and populate it with some predefined users.</span></span>

3. <span data-ttu-id="cf97a-165">Enregistrer hello `CreateTable.java` fichier.</span><span class="sxs-lookup"><span data-stu-id="cf97a-165">Save hello `CreateTable.java` file.</span></span>

4. <span data-ttu-id="cf97a-166">Bonjour `hbaseapp/src/main/java/com/microsoft/examples` répertoire, créez un fichier nommé `SearchByEmail.java`.</span><span class="sxs-lookup"><span data-stu-id="cf97a-166">In hello `hbaseapp/src/main/java/com/microsoft/examples` directory, create a file named `SearchByEmail.java`.</span></span> <span data-ttu-id="cf97a-167">Utilisez hello après le texte en tant que contenu hello de ce fichier :</span><span class="sxs-lookup"><span data-stu-id="cf97a-167">Use hello following text as hello contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HTable;
    import org.apache.hadoop.hbase.client.Scan;
    import org.apache.hadoop.hbase.client.ResultScanner;
    import org.apache.hadoop.hbase.client.Result;
    import org.apache.hadoop.hbase.filter.RegexStringComparator;
    import org.apache.hadoop.hbase.filter.SingleColumnValueFilter;
    import org.apache.hadoop.hbase.filter.CompareFilter.CompareOp;
    import org.apache.hadoop.hbase.util.Bytes;
    import org.apache.hadoop.util.GenericOptionsParser;

    public class SearchByEmail {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Use GenericOptionsParser tooget only hello parameters toohello class
        // and not all hello parameters passed (when using WebHCat for example)
        String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
        if (otherArgs.length != 1) {
            System.out.println("usage: [regular expression]");
            System.exit(-1);
        }

        // Open hello table
        HTable table = new HTable(config, "people");

        // Define hello family and qualifiers toobe used
        byte[] contactFamily = Bytes.toBytes("contactinfo");
        byte[] emailQualifier = Bytes.toBytes("email");
        byte[] nameFamily = Bytes.toBytes("name");
        byte[] firstNameQualifier = Bytes.toBytes("first");
        byte[] lastNameQualifier = Bytes.toBytes("last");

        // Create a regex filter
        RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
        // Attach hello regex filter tooa filter
        //   for hello email column
        SingleColumnValueFilter filter = new SingleColumnValueFilter(
            contactFamily,
            emailQualifier,
            CompareOp.EQUAL,
            emailFilter
        );

        // Create a scan and set hello filter
        Scan scan = new Scan();
        scan.setFilter(filter);

        // Get hello results
        ResultScanner results = table.getScanner(scan);
        // Iterate over results and print  values
        for (Result result : results ) {
            String id = new String(result.getRow());
            byte[] firstNameObj = result.getValue(nameFamily, firstNameQualifier);
            String firstName = new String(firstNameObj);
            byte[] lastNameObj = result.getValue(nameFamily, lastNameQualifier);
            String lastName = new String(lastNameObj);
            System.out.println(firstName + " " + lastName + " - ID: " + id);
            byte[] emailObj = result.getValue(contactFamily, emailQualifier);
            String email = new String(emailObj);
            System.out.println(firstName + " " + lastName + " - " + email + " - ID: " + id);
        }
        results.close();
        table.close();
        }
    }
   ```

    <span data-ttu-id="cf97a-168">Hello **SearchByEmail** classe peut être tooquery utilisé pour les lignes par adresse de messagerie.</span><span class="sxs-lookup"><span data-stu-id="cf97a-168">hello **SearchByEmail** class can be used tooquery for rows by email address.</span></span> <span data-ttu-id="cf97a-169">Car elle utilise un filtre d’expression régulière, vous pouvez fournir une chaîne ou une expression régulière lors de l’utilisation de classe hello.</span><span class="sxs-lookup"><span data-stu-id="cf97a-169">Because it uses a regular expression filter, you can provide either a string or a regular expression when using hello class.</span></span>

5. <span data-ttu-id="cf97a-170">Enregistrer hello `SearchByEmail.java` fichier.</span><span class="sxs-lookup"><span data-stu-id="cf97a-170">Save hello `SearchByEmail.java` file.</span></span>

6. <span data-ttu-id="cf97a-171">Bonjour `hbaseapp/src/main/hava/com/microsoft/examples` répertoire, créez un fichier nommé `DeleteTable.java`.</span><span class="sxs-lookup"><span data-stu-id="cf97a-171">In hello `hbaseapp/src/main/hava/com/microsoft/examples` directory, create a file named `DeleteTable.java`.</span></span> <span data-ttu-id="cf97a-172">Utilisez hello après le texte en tant que contenu hello de ce fichier :</span><span class="sxs-lookup"><span data-stu-id="cf97a-172">Use hello following text as hello contents of this file:</span></span>

   ```java
    package com.microsoft.examples;
    import java.io.IOException;

    import org.apache.hadoop.conf.Configuration;
    import org.apache.hadoop.hbase.HBaseConfiguration;
    import org.apache.hadoop.hbase.client.HBaseAdmin;

    public class DeleteTable {
        public static void main(String[] args) throws IOException {
        Configuration config = HBaseConfiguration.create();

        // Create an admin object using hello config
        HBaseAdmin admin = new HBaseAdmin(config);

        // Disable, and then delete hello table
        admin.disableTable("people");
        admin.deleteTable("people");
        }
    }
   ```

    <span data-ttu-id="cf97a-173">Cette classe nettoie les tables HBase créées dans cet exemple en désactivant hello et suppression hello table créée par hello `CreateTable` classe.</span><span class="sxs-lookup"><span data-stu-id="cf97a-173">This class cleans up hello HBase tables created in this example by disabling and dropping hello table created by hello `CreateTable` class.</span></span>

7. <span data-ttu-id="cf97a-174">Enregistrer hello `DeleteTable.java` fichier.</span><span class="sxs-lookup"><span data-stu-id="cf97a-174">Save hello `DeleteTable.java` file.</span></span>

## <a name="build-and-package-hello-application"></a><span data-ttu-id="cf97a-175">Génération et package d’application de hello</span><span class="sxs-lookup"><span data-stu-id="cf97a-175">Build and package hello application</span></span>

1. <span data-ttu-id="cf97a-176">À partir de hello `hbaseapp` répertoire, toobuild de commande suivant de hello utiliser un fichier JAR contenant une application hello :</span><span class="sxs-lookup"><span data-stu-id="cf97a-176">From hello `hbaseapp` directory, use hello following command toobuild a JAR file that contains hello application:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="cf97a-177">Cette commande génère et packages hello application dans un fichier JAR.</span><span class="sxs-lookup"><span data-stu-id="cf97a-177">This command builds and packages hello application into a .jar file.</span></span>

2. <span data-ttu-id="cf97a-178">Commande hello issue, hello `hbaseapp/target` répertoire contient un fichier nommé `hbaseapp-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="cf97a-178">When hello command completes, hello `hbaseapp/target` directory contains a file named `hbaseapp-1.0-SNAPSHOT.jar`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cf97a-179">Hello `hbaseapp-1.0-SNAPSHOT.jar` fichier est un fichier jar générale.</span><span class="sxs-lookup"><span data-stu-id="cf97a-179">hello `hbaseapp-1.0-SNAPSHOT.jar` file is an uber jar.</span></span> <span data-ttu-id="cf97a-180">Il contient toutes les applications de hello toorun requis dépendances hello.</span><span class="sxs-lookup"><span data-stu-id="cf97a-180">It contains all hello dependencies required toorun hello application.</span></span>


## <a name="upload-hello-jar-and-run-jobs-ssh"></a><span data-ttu-id="cf97a-181">Hello JAR de télécharger et exécuter des travaux (SSH)</span><span class="sxs-lookup"><span data-stu-id="cf97a-181">Upload hello JAR and run jobs (SSH)</span></span>

<span data-ttu-id="cf97a-182">Hello suivant l’utilisation d’étapes `scp` toocopy hello JAR toohello principal nœud principal de votre HBase sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf97a-182">hello following steps use `scp` toocopy hello JAR toohello primary head node of your HBase on HDInsight cluster.</span></span> <span data-ttu-id="cf97a-183">Hello `ssh` commande est ensuite utilisé tooconnect toohello cluster et exécutez hello exemple directement sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="cf97a-183">hello `ssh` command is then used tooconnect toohello cluster and run hello example directly on hello head node.</span></span>

1. <span data-ttu-id="cf97a-184">tooupload hello jar toohello cluster hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cf97a-184">tooupload hello jar toohello cluster, use hello following command:</span></span>

    ```bash
    scp ./target/hbaseapp-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:hbaseapp-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="cf97a-185">Remplacez `USERNAME` par nom hello de votre connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="cf97a-185">Replace `USERNAME` with hello name of your SSH login.</span></span> <span data-ttu-id="cf97a-186">Remplacez `CLUSTERNAME` par le nom de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf97a-186">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

2. <span data-ttu-id="cf97a-187">tooconnect toohello cluster HBase, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cf97a-187">tooconnect toohello HBase cluster, use hello following command:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="cf97a-188">Remplacez `USERNAME` nom hello de votre connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="cf97a-188">Replace `USERNAME` hello name of your SSH login.</span></span> <span data-ttu-id="cf97a-189">Remplacez `CLUSTERNAME` par le nom de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf97a-189">Replace `CLUSTERNAME` with your HDInsight cluster name.</span></span>

3. <span data-ttu-id="cf97a-190">une table HBase à l’aide de toocreate hello application Java, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cf97a-190">toocreate an HBase table using hello Java application, use hello following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.CreateTable
    ```

    <span data-ttu-id="cf97a-191">Cette commande crée une table HBase nommée **people** la remplit de données.</span><span class="sxs-lookup"><span data-stu-id="cf97a-191">This command creates a HBase table named **people**, and populates it with data.</span></span>

4. <span data-ttu-id="cf97a-192">toosearch pour les adresses de messagerie stockées dans table hello, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cf97a-192">toosearch for email addresses stored in hello table, use hello following command:</span></span>

    ```bash
    yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.SearchByEmail contoso.com
    ```

    <span data-ttu-id="cf97a-193">Vous recevez hello suivant des résultats :</span><span class="sxs-lookup"><span data-stu-id="cf97a-193">You receive hello following results:</span></span>

        Franklin Holtz - ID: 2
        Franklin Holtz - franklin@contoso.com - ID: 2
        Rae Schroeder - ID: 4
        Rae Schroeder - rae@contoso.com - ID: 4
        Gabriela Ingram - ID: 6
        Gabriela Ingram - gabriela@contoso.com - ID: 6

5. <span data-ttu-id="cf97a-194">table hello toodelete, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cf97a-194">toodelete hello table, use hello following command:</span></span>

    

## <a name="upload-hello-jar-and-run-jobs-powershell"></a><span data-ttu-id="cf97a-195">Hello JAR de télécharger et exécuter des travaux (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="cf97a-195">Upload hello JAR and run jobs (PowerShell)</span></span>

<span data-ttu-id="cf97a-196">Hello comme suit utilisent le stockage de Azure PowerShell tooupload hello JAR toohello par défaut pour votre cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="cf97a-196">hello following steps use Azure PowerShell tooupload hello JAR toohello default storage for your HBase cluster.</span></span> <span data-ttu-id="cf97a-197">Applets de commande HDInsight sont utilisé toorun hello exemples à distance.</span><span class="sxs-lookup"><span data-stu-id="cf97a-197">HDInsight cmdlets are then used toorun hello examples remotely.</span></span>

1. <span data-ttu-id="cf97a-198">Après avoir installé et configuré Azure PowerShell, créez un fichier nommé `hbase-runner.psm1`.</span><span class="sxs-lookup"><span data-stu-id="cf97a-198">After installing and configuring Azure PowerShell, create a file named `hbase-runner.psm1`.</span></span> <span data-ttu-id="cf97a-199">Utilisez hello après le texte en tant que contenu hello de ce fichier :</span><span class="sxs-lookup"><span data-stu-id="cf97a-199">Use hello following text as hello contents of this file:</span></span>

   ```powershell
    <#
    .SYNOPSIS
    Copies a file toohello primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory toohello blob container for
    hello HDInsight cluster.
    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.CreateTable"
    -clusterName "MyHDInsightCluster"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "contoso.com"

    .EXAMPLE
    Start-HBaseExample -className "com.microsoft.examples.SearchByEmail"
    -clusterName "MyHDInsightCluster"
    -emailRegex "^r" -showErr
    #>

    function Start-HBaseExample {
    [CmdletBinding(SupportsShouldProcess = $true)]
    param(
    #hello class toorun
    [Parameter(Mandatory = $true)]
    [String]$className,

    #hello name of hello HDInsight cluster
    [Parameter(Mandatory = $true)]
    [String]$clusterName,

    #Only used when using SearchByEmail
    [Parameter(Mandatory = $false)]
    [String]$emailRegex,

    #Use if you want toosee stderr output
    [Parameter(Mandatory = $false)]
    [Switch]$showErr
    )

    Set-StrictMode -Version 3

    # Is hello Azure module installed?
    FindAzure

    # Get hello login for hello HDInsight cluster
    $creds=Get-Credential -Message "Enter hello login for hello cluster" -UserName "admin"

    # hello JAR
    $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

    # hello job definition
    $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
        -JarFile $jarFile `
        -ClassName $className `
        -Arguments $emailRegex

    # Get hello job output
    $job = Start-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobDefinition $jobDefinition `
        -HttpCredential $creds
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureRmHDInsightJob `
        -ClusterName $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds
    if($showErr)
    {
    Write-Host "STDERR"
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds `
                -DisplayOutputType StandardError
    }
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
                -Clustername $clusterName `
                -JobId $job.JobId `
                -HttpCredential $creds
    }

    <#
    .SYNOPSIS
    Copies a file toohello primary storage of an HDInsight cluster.
    .DESCRIPTION
    Copies a file from a local directory toohello blob container for
    hello HDInsight cluster.
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    .EXAMPLE
    Add-HDInsightFile -localPath "C:\temp\data.txt"
    -destinationPath "example/data/data.txt"
    -ClusterName "MyHDInsightCluster"
    -Container "MyContainer"
    #>

    function Add-HDInsightFile {
        [CmdletBinding(SupportsShouldProcess = $true)]
        param(
            #hello path toohello local file.
            [Parameter(Mandatory = $true)]
            [String]$localPath,

            #hello destination path and file name, relative toohello root of hello container.
            [Parameter(Mandatory = $true)]
            [String]$destinationPath,

            #hello name of hello HDInsight cluster
            [Parameter(Mandatory = $true)]
            [String]$clusterName,

            #If specified, overwrites existing files without prompting
            [Parameter(Mandatory = $false)]
            [Switch]$force
        )

        Set-StrictMode -Version 3

        # Is hello Azure module installed?
        FindAzure

        # Get authentication for hello cluster
        $creds=Get-Credential

        # Does hello local path exist?
        if (-not (Test-Path $localPath))
        {
            throw "Source path '$localPath' does not exist."
        }

        # Get hello primary storage container
        $storage = GetStorage -clusterName $clusterName

        # Upload file toostorage, overwriting existing files if -force was used.
        Set-AzureStorageBlobContent -File $localPath `
            -Blob $destinationPath `
            -force:$force `
            -Container $storage.container `
            -Context $storage.context
    }

    function FindAzure {
        # Is there an active Azure subscription?
        $sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
        if(-not($sub))
        {
            throw "No active Azure subscription found! If you have a subscription, use hello Login-AzureRmAccount cmdlet toologin tooyour subscription."
        }
    }

    function GetStorage {
        param(
            [Parameter(Mandatory = $true)]
            [String]$clusterName
        )
        $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
        # Does hello cluster exist?
        if (!$hdi)
        {
            throw "HDInsight cluster '$clusterName' does not exist."
        }
        # Create a return object for context & container
        $return = @{}
        $storageAccounts = @{}

        # Get storage information
        $resourceGroup = $hdi.ResourceGroup
        $storageAccountName=$hdi.DefaultStorageAccount.split('.')[0]
        $container=$hdi.DefaultStorageContainer
        $storageAccountKey=(Get-AzureRmStorageAccountKey `
            -Name $storageAccountName `
        -ResourceGroupName $resourceGroup)[0].Value
        # Get hello resource group, in case we need that
        $return.resourceGroup = $resourceGroup
        # Get hello storage context, as we can't depend
        # on using hello default storage context
        $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
        # Get hello container, so we know where to
        # find/store blobs
        $return.container = $container
        # Return storage accounts toosupport finding all accounts for
        # a cluster
        $return.storageAccount = $storageAccountName
        $return.storageAccountKey = $storageAccountKey

        return $return
    }
    # Only export hello verb-phrase things
    export-modulemember *-*
   ```

    <span data-ttu-id="cf97a-200">Ce fichier contient deux modules :</span><span class="sxs-lookup"><span data-stu-id="cf97a-200">This file contains two modules:</span></span>

   * <span data-ttu-id="cf97a-201">**Ajouter-HDInsightFile** - utilisés cluster de toohello fichiers tooupload</span><span class="sxs-lookup"><span data-stu-id="cf97a-201">**Add-HDInsightFile** - used tooupload files toohello cluster</span></span>
   * <span data-ttu-id="cf97a-202">**Start-HBaseExample** -classes de hello toorun créés précédemment utilisées</span><span class="sxs-lookup"><span data-stu-id="cf97a-202">**Start-HBaseExample** - used toorun hello classes created earlier</span></span>

2. <span data-ttu-id="cf97a-203">Enregistrer hello `hbase-runner.psm1` fichier.</span><span class="sxs-lookup"><span data-stu-id="cf97a-203">Save hello `hbase-runner.psm1` file.</span></span>

3. <span data-ttu-id="cf97a-204">Ouvrir une nouvelle fenêtre Azure PowerShell, modifiez les répertoires toohello `hbaseapp` active, et en exécution hello commande suivant :</span><span class="sxs-lookup"><span data-stu-id="cf97a-204">Open a new Azure PowerShell window, change directories toohello `hbaseapp` directory, and then run hello following command:</span></span>

    ```powershell
    PS C:\ Import-Module c:\path\to\hbase-runner.psm1
    ```

    <span data-ttu-id="cf97a-205">Modifier hello chemin toohello l’emplacement de hello `hbase-runner.psm1` fichier créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="cf97a-205">Change hello path toohello location of hello `hbase-runner.psm1` file created earlier.</span></span> <span data-ttu-id="cf97a-206">Cette commande enregistre le module de hello avec Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cf97a-206">This command registers hello module with Azure PowerShell.</span></span>

4. <span data-ttu-id="cf97a-207">Suivant de hello utilisez commande hello de tooupload `hbaseapp-1.0-SNAPSHOT.jar` tooyour cluster.</span><span class="sxs-lookup"><span data-stu-id="cf97a-207">Use hello following command tooupload hello `hbaseapp-1.0-SNAPSHOT.jar` tooyour cluster.</span></span>

    ```powershell
    Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername
    ```

    <span data-ttu-id="cf97a-208">Remplacez `hdinsightclustername` avec nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="cf97a-208">Replace `hdinsightclustername` with hello name of your cluster.</span></span> <span data-ttu-id="cf97a-209">commande Hello télécharge hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` emplacement dans le stockage principal hello pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="cf97a-209">hello command uploads hello `hbaseapp-1.0-SNAPSHOT.jar` toohello `example/jars` location in hello primary storage for your cluster.</span></span>

5. <span data-ttu-id="cf97a-210">une table à l’aide de toocreate hello `hbaseapp`, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cf97a-210">toocreate a table using hello `hbaseapp`, use hello following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername
    ```

    <span data-ttu-id="cf97a-211">Remplacez `hdinsightclustername` avec nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="cf97a-211">Replace `hdinsightclustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="cf97a-212">Cette commande crée une table nommée **people** dans HBase sur votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cf97a-212">This command creates a table named **people** in HBase on your HDInsight cluster.</span></span> <span data-ttu-id="cf97a-213">Cette commande n’affiche pas de sortie dans la fenêtre de console hello.</span><span class="sxs-lookup"><span data-stu-id="cf97a-213">This command does not show any output in hello console window.</span></span>

6. <span data-ttu-id="cf97a-214">toosearch pour entrées de table hello, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="cf97a-214">toosearch for entries in hello table, use hello following command:</span></span>

    ```powershell
    Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com
    ```

    <span data-ttu-id="cf97a-215">Remplacez `hdinsightclustername` avec nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="cf97a-215">Replace `hdinsightclustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="cf97a-216">Cette commande utilise hello `SearchByEmail` classe toosearch pour toutes les lignes où hello `contactinformation` famille de colonne et hello `email` colonne, contient la chaîne de hello `contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="cf97a-216">This command uses hello `SearchByEmail` class toosearch for any rows where hello `contactinformation` column family and hello `email` column, contains hello string `contoso.com`.</span></span> <span data-ttu-id="cf97a-217">Vous devez recevoir hello suivant des résultats :</span><span class="sxs-lookup"><span data-stu-id="cf97a-217">You should receive hello following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="cf97a-218">À l’aide de **fabrikam.com** pour hello `-emailRegex` valeur retourne les utilisateurs hello ayant **fabrikam.com** dans le champ d’adresse de messagerie hello.</span><span class="sxs-lookup"><span data-stu-id="cf97a-218">Using **fabrikam.com** for hello `-emailRegex` value returns hello users that have **fabrikam.com** in hello email field.</span></span> <span data-ttu-id="cf97a-219">Vous pouvez également utiliser des expressions régulières comme terme de recherche hello.</span><span class="sxs-lookup"><span data-stu-id="cf97a-219">You can also use regular expressions as hello search term.</span></span> <span data-ttu-id="cf97a-220">Par exemple, **^ r** retourne les adresses qui commencent par la lettre de hello « r » de messagerie.</span><span class="sxs-lookup"><span data-stu-id="cf97a-220">For example, **^r** returns email addresses that begin with hello letter 'r'.</span></span>

### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="cf97a-221">Aucun résultat ou résultat inattendu lors de l'utilisation de Start-HBaseExample</span><span class="sxs-lookup"><span data-stu-id="cf97a-221">No results or unexpected results when using Start-HBaseExample</span></span>

<span data-ttu-id="cf97a-222">Hello d’utilisation `-showErr` paramètre tooview hello erreur standard (STDERR) qui est généré lors de la tâche de hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="cf97a-222">Use hello `-showErr` parameter tooview hello standard error (STDERR) that is produced while running hello job.</span></span>

## <a name="delete-hello-table"></a><span data-ttu-id="cf97a-223">Supprimer une table de hello</span><span class="sxs-lookup"><span data-stu-id="cf97a-223">Delete hello table</span></span>

<span data-ttu-id="cf97a-224">Lorsque vous avez terminé avec l’exemple de hello, utilisez hello suivant toodelete hello **personnes** table utilisée dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="cf97a-224">When you are done with hello example, use hello following toodelete hello **people** table used in this example:</span></span>

<span data-ttu-id="cf97a-225">__À partir d’une session `ssh`__ :</span><span class="sxs-lookup"><span data-stu-id="cf97a-225">__From an `ssh` session__:</span></span>

`yarn jar hbaseapp-1.0-SNAPSHOT.jar com.microsoft.examples.DeleteTable`

<span data-ttu-id="cf97a-226">__À partir d’Azure PowerShell__ :</span><span class="sxs-lookup"><span data-stu-id="cf97a-226">__From Azure PowerShell__:</span></span>

`Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername`

## <a name="next-steps"></a><span data-ttu-id="cf97a-227">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cf97a-227">Next steps</span></span>

[<span data-ttu-id="cf97a-228">Découvrez comment toouse SQL non avec HBase</span><span class="sxs-lookup"><span data-stu-id="cf97a-228">Learn how toouse SQuirreL SQL with HBase</span></span>](hdinsight-hbase-phoenix-squirrel-linux.md)
