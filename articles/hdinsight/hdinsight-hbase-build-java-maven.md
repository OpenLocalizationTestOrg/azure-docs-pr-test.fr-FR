---
title: "aaaBuild une application Java HBase pour basé sur Windows Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toouse application de Apache HBase Apache Maven toobuild basé sur un Java, puis déployez-le tooa basé sur Windows Azure HDInsight cluster."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f4a4e02-45ab-40dd-842b-3ec034f256c9
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 33c2f3d12cb6a17b5406817e8bcd3accff239517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-maven-toobuild-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a><span data-ttu-id="bf072-103">Utiliser des applications Java Maven toobuild qui utilisent HBase hdinsight basés sur Windows (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="bf072-103">Use Maven toobuild Java applications that use HBase with Windows-based HDInsight (Hadoop)</span></span>
<span data-ttu-id="bf072-104">Découvrez comment toocreate et générer un [Apache HBase](http://hbase.apache.org/) application Java à l’aide d’Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="bf072-104">Learn how toocreate and build an [Apache HBase](http://hbase.apache.org/) application in Java by using Apache Maven.</span></span> <span data-ttu-id="bf072-105">Utilisez application hello avec Azure HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="bf072-105">Then use hello application with Azure HDInsight (Hadoop).</span></span>

<span data-ttu-id="bf072-106">[Maven](http://maven.apache.org/) est un outil de projet logiciel de gestion et compréhension qui vous permet de toobuild logiciel, la documentation et des rapports pour les projets de Java.</span><span class="sxs-lookup"><span data-stu-id="bf072-106">[Maven](http://maven.apache.org/) is a software project management and comprehension tool that allows you toobuild software, documentation, and reports for Java projects.</span></span> <span data-ttu-id="bf072-107">Dans cet article, vous apprendrez comment toouse il toocreate une application Java de base qui crée, interroge, et supprime un HBase sur un cluster Azure HDInsight de table.</span><span class="sxs-lookup"><span data-stu-id="bf072-107">In this article, you learn how toouse it toocreate a basic Java application that that creates, queries, and deletes an HBase table on an Azure HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bf072-108">étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Windows.</span><span class="sxs-lookup"><span data-stu-id="bf072-108">hello steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="bf072-109">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="bf072-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bf072-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="bf072-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="bf072-111">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="bf072-111">Requirements</span></span>
* <span data-ttu-id="bf072-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 ou version supérieure</span><span class="sxs-lookup"><span data-stu-id="bf072-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 or later</span></span>
* [<span data-ttu-id="bf072-113">Maven</span><span class="sxs-lookup"><span data-stu-id="bf072-113">Maven</span></span>](http://maven.apache.org/)
* <span data-ttu-id="bf072-114">Un cluster HDInsight sous Windows avec HBase</span><span class="sxs-lookup"><span data-stu-id="bf072-114">A Windows-based HDInsight cluster with HBase</span></span>

    > [!NOTE]
    > <span data-ttu-id="bf072-115">étapes Hello dans ce document ont été testés avec des versions 3.2 et 3.3 du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bf072-115">hello steps in this document have been tested with HDInsight cluster versions 3.2 and 3.3.</span></span> <span data-ttu-id="bf072-116">les valeurs par défaut Hello fournies dans les exemples sont pour un cluster HDInsight 3.3.</span><span class="sxs-lookup"><span data-stu-id="bf072-116">hello default values provided in examples are for a HDInsight 3.3 cluster.</span></span>

## <a name="create-hello-project"></a><span data-ttu-id="bf072-117">Créer le projet de hello</span><span class="sxs-lookup"><span data-stu-id="bf072-117">Create hello project</span></span>
1. <span data-ttu-id="bf072-118">À partir de la ligne de commande hello dans votre environnement de développement, modifiez les répertoires toohello emplacement souhaité projet hello de toocreate, par exemple, `cd code\hdinsight`.</span><span class="sxs-lookup"><span data-stu-id="bf072-118">From hello command line in your development environment, change directories toohello location where you want toocreate hello project, for example, `cd code\hdinsight`.</span></span>
2. <span data-ttu-id="bf072-119">Hello d’utilisation **mvn** commande, qui est installé avec Maven, hello toogenerate génération de modèles automatique pour le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="bf072-119">Use hello **mvn** command, which is installed with Maven, toogenerate hello scaffolding for hello project.</span></span>

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    <span data-ttu-id="bf072-120">Cette commande crée un répertoire dans l’emplacement actuel de hello, avec le nom hello spécifié par hello **artifactID** paramètre (**hbaseapp** dans cet exemple.) Ce répertoire contient hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bf072-120">This command creates a directory in hello current location, with hello name specified by hello **artifactID** parameter (**hbaseapp** in this example.) This directory contains hello following items:</span></span>

   * <span data-ttu-id="bf072-121">**pom.XML**: hello du modèle objet Project ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contient des informations et la configuration du projet de hello détails utilisés toobuild.</span><span class="sxs-lookup"><span data-stu-id="bf072-121">**pom.xml**:  hello Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used toobuild hello project.</span></span>
   * <span data-ttu-id="bf072-122">**src**: répertoire hello contenant hello **main\java\com\microsoft\examples** répertoire, où vous allez créer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="bf072-122">**src**: hello directory that contains hello **main\java\com\microsoft\examples** directory, where you will author hello application.</span></span>
3. <span data-ttu-id="bf072-123">Supprimer hello **src\test\java\com\microsoft\examples\apptest.java** , car il n’est pas utilisé dans cet exemple de fichier.</span><span class="sxs-lookup"><span data-stu-id="bf072-123">Delete hello **src\test\java\com\microsoft\examples\apptest.java** file because it is not used in this example.</span></span>

## <a name="update-hello-project-object-model"></a><span data-ttu-id="bf072-124">Mettre à jour hello modèle objet Project</span><span class="sxs-lookup"><span data-stu-id="bf072-124">Update hello Project Object Model</span></span>
1. <span data-ttu-id="bf072-125">Modifier hello **pom.xml** et ajoutez hello suivant du code à l’intérieur de hello `<dependencies>` section :</span><span class="sxs-lookup"><span data-stu-id="bf072-125">Edit hello **pom.xml** file and add hello following code inside hello `<dependencies>` section:</span></span>

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    <span data-ttu-id="bf072-126">Cette section explique Maven qui hello projet nécessite **hbase-client** version **1.1.2**.</span><span class="sxs-lookup"><span data-stu-id="bf072-126">This section tells Maven that hello project requires **hbase-client** version **1.1.2**.</span></span> <span data-ttu-id="bf072-127">Au moment de la compilation, cette dépendance est téléchargée à partir du référentiel de Maven hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="bf072-127">At compile time, this dependency is downloaded from hello default Maven repository.</span></span> <span data-ttu-id="bf072-128">Vous pouvez utiliser hello [recherche de référentiel centrale Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn plus d’informations sur cette dépendance.</span><span class="sxs-lookup"><span data-stu-id="bf072-128">You can use hello [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="bf072-129">numéro de version Hello doit correspondre au version hello de HBase qui est fourni avec votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bf072-129">hello version number must match hello version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="bf072-130">Utilisez hello suivant le numéro de version correct de table toofind hello.</span><span class="sxs-lookup"><span data-stu-id="bf072-130">Use hello following table toofind hello correct version number.</span></span>
   >
   >

   | <span data-ttu-id="bf072-131">Version de cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="bf072-131">HDInsight cluster version</span></span> | <span data-ttu-id="bf072-132">HBase version toouse</span><span class="sxs-lookup"><span data-stu-id="bf072-132">HBase version toouse</span></span> |
   | --- | --- |
   | <span data-ttu-id="bf072-133">3.2</span><span class="sxs-lookup"><span data-stu-id="bf072-133">3.2</span></span> |<span data-ttu-id="bf072-134">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="bf072-134">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="bf072-135">3.3</span><span class="sxs-lookup"><span data-stu-id="bf072-135">3.3</span></span> |<span data-ttu-id="bf072-136">1.1.2</span><span class="sxs-lookup"><span data-stu-id="bf072-136">1.1.2</span></span> |

    <span data-ttu-id="bf072-137">Pour plus d’informations sur les composants et les versions de HDInsight, consultez [quels sont les composants Hadoop hello différents disponibles avec HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="bf072-137">For more information on HDInsight versions and components, see [What are hello different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>
2. <span data-ttu-id="bf072-138">Si vous utilisez un cluster HDInsight 3.3, vous devez également ajouter hello suivant toohello `<dependencies>` section :</span><span class="sxs-lookup"><span data-stu-id="bf072-138">If you are using an HDInsight 3.3 cluster, you must also add hello following toohello `<dependencies>` section:</span></span>

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    <span data-ttu-id="bf072-139">Cette dépendance chargera hello phoenix-composants, qui sont utilisés par la version de Hbase 1.1.x.</span><span class="sxs-lookup"><span data-stu-id="bf072-139">This dependency will load hello phoenix-core components, which are used by Hbase version 1.1.x.</span></span>
3. <span data-ttu-id="bf072-140">Ajouter hello suivant code toohello **pom.xml** fichier.</span><span class="sxs-lookup"><span data-stu-id="bf072-140">Add hello following code toohello **pom.xml** file.</span></span> <span data-ttu-id="bf072-141">Cette section doit être à l’intérieur de hello `<project>...</project>` balises Bonjour de fichiers, par exemple, entre `</dependencies>` et `</project>`.</span><span class="sxs-lookup"><span data-stu-id="bf072-141">This section must be inside hello `<project>...</project>` tags in hello file, for example, between `</dependencies>` and `</project>`.</span></span>

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
                    <source>1.7</source>
                    <target>1.7</target>
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

    <span data-ttu-id="bf072-142">Hello `<resources>` section configure une ressource (**conf\hbase-site.XML**) qui contient des informations de configuration pour HBase.</span><span class="sxs-lookup"><span data-stu-id="bf072-142">hello `<resources>` section configures a resource (**conf\hbase-site.xml**) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bf072-143">Vous pouvez également définir les valeurs de configuration par code.</span><span class="sxs-lookup"><span data-stu-id="bf072-143">You can also set configuration values via code.</span></span> <span data-ttu-id="bf072-144">Consultez les commentaires hello Bonjour **CreateTable** exemple qui suit sur la manière de toodo cela.</span><span class="sxs-lookup"><span data-stu-id="bf072-144">See hello comments in hello **CreateTable** example that follows for how toodo this.</span></span>
   >
   >

    <span data-ttu-id="bf072-145">Cela `<plugins>` section configure hello [plug-in du compilateur Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) et [plug-in de la nuance Maven](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="bf072-145">This `<plugins>` section configures hello [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="bf072-146">compilateur Hello plug-in est utilisé toocompile hello topologie.</span><span class="sxs-lookup"><span data-stu-id="bf072-146">hello compiler plug-in is used toocompile hello topology.</span></span> <span data-ttu-id="bf072-147">ombre Hello plug-in est la duplication de licence tooprevent utilisés dans le package JAR hello qui est généré par Maven.</span><span class="sxs-lookup"><span data-stu-id="bf072-147">hello shade plug-in is used tooprevent license duplication in hello JAR package that is built by Maven.</span></span> <span data-ttu-id="bf072-148">Hello utilisé parce que les fichiers de licence en double de hello provoquent une erreur au moment de l’exécution sur le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="bf072-148">hello reason this is used is that hello duplicate license files cause an error at run time on hello HDInsight cluster.</span></span> <span data-ttu-id="bf072-149">À l’aide de maven-ton plug-in par hello `ApacheLicenseResourceTransformer` implémentation empêche cette erreur.</span><span class="sxs-lookup"><span data-stu-id="bf072-149">Using maven-shade-plugin with hello `ApacheLicenseResourceTransformer` implementation prevents this error.</span></span>

    <span data-ttu-id="bf072-150">Hello maven-ton plug-in génère également une uber jar (ou le jar fat) qui contient toutes les dépendances de hello requis par l’application hello.</span><span class="sxs-lookup"><span data-stu-id="bf072-150">hello maven-shade-plugin also produces an uber jar (or fat jar) that contains all hello dependencies required by hello application.</span></span>
4. <span data-ttu-id="bf072-151">Enregistrer hello **pom.xml** fichier.</span><span class="sxs-lookup"><span data-stu-id="bf072-151">Save hello **pom.xml** file.</span></span>
5. <span data-ttu-id="bf072-152">Créer un nouveau répertoire nommé **conf** Bonjour **hbaseapp** active.</span><span class="sxs-lookup"><span data-stu-id="bf072-152">Create a new directory named **conf** in hello **hbaseapp** directory.</span></span> <span data-ttu-id="bf072-153">Bonjour **conf** répertoire, créez un fichier nommé **hbase-site.XML**.</span><span class="sxs-lookup"><span data-stu-id="bf072-153">In hello **conf** directory, create a file named **hbase-site.xml**.</span></span> <span data-ttu-id="bf072-154">Utilisez les éléments suivants de hello en tant que contenu hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="bf072-154">Use hello following as hello contents of hello file:</span></span>

        <?xml version="1.0"?>
        <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
        <!--
        /**
          * Copyright 2010 hello Apache Software Foundation
          *
          * Licensed toohello Apache Software Foundation (ASF) under one
          * or more contributor license agreements.  See hello NOTICE file
          * distributed with this work for additional information
          * regarding copyright ownership.  hello ASF licenses this file
          * tooyou under hello Apache License, Version 2.0 (the
          * "License"); you may not use this file except in compliance
          * with hello License.  You may obtain a copy of hello License at
          *
          *     http://www.apache.org/licenses/LICENSE-2.0
          *
          * Unless required by applicable law or agreed tooin writing, software
          * distributed under hello License is distributed on an "AS IS" BASIS,
          * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
          * See hello License for hello specific language governing permissions and
          * limitations under hello License.
          */
        -->
        <configuration>
          <property>
            <name>hbase.cluster.distributed</name>
            <value>true</value>
          </property>
          <property>
            <name>hbase.zookeeper.quorum</name>
            <value>zookeeper0,zookeeper1,zookeeper2</value>
          </property>
          <property>
            <name>hbase.zookeeper.property.clientPort</name>
            <value>2181</value>
          </property>
        </configuration>

    <span data-ttu-id="bf072-155">Ce fichier sera utilisé tooload hello HBase pour un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bf072-155">This file will be used tooload hello HBase configuration for an HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bf072-156">Il s’agit d’un fichier minimal hbase-site.XML, et il contient des paramètres de configuration minimale bare hello pour le cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="bf072-156">This is a minimal hbase-site.xml file, and it contains hello bare minimum settings for hello HDInsight cluster.</span></span>

6. <span data-ttu-id="bf072-157">Enregistrer hello **hbase-site.XML** fichier.</span><span class="sxs-lookup"><span data-stu-id="bf072-157">Save hello **hbase-site.xml** file.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="bf072-158">Créer l’application hello</span><span class="sxs-lookup"><span data-stu-id="bf072-158">Create hello application</span></span>
1. <span data-ttu-id="bf072-159">Accédez toohello **hbaseapp\src\main\java\com\microsoft\examples** active et renommer hello trop app.java fichier**CreateTable.java**.</span><span class="sxs-lookup"><span data-stu-id="bf072-159">Go toohello **hbaseapp\src\main\java\com\microsoft\examples** directory and rename hello app.java file too**CreateTable.java**.</span></span>
2. <span data-ttu-id="bf072-160">Ouvrez hello **CreateTable.java** de fichier et remplacez contenu hello hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="bf072-160">Open hello **CreateTable.java** file and replace hello existing contents with hello following code:</span></span>

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
            // hello following sets hello znode root for Linux-based HDInsight
            //config.set("zookeeper.znode.parent","/hbase-unsecure");

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

    <span data-ttu-id="bf072-161">Il s’agit de hello **CreateTable** (classe), qui crée une table nommée **personnes** et le remplir avec certains utilisateurs prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="bf072-161">This is hello **CreateTable** class, which will create a table named **people** and populate it with some predefined users.</span></span>
3. <span data-ttu-id="bf072-162">Enregistrer hello **CreateTable.java** fichier.</span><span class="sxs-lookup"><span data-stu-id="bf072-162">Save hello **CreateTable.java** file.</span></span>
4. <span data-ttu-id="bf072-163">Bonjour **hbaseapp\src\main\java\com\microsoft\examples** répertoire, créez un nouveau fichier nommé **SearchByEmail.java**.</span><span class="sxs-lookup"><span data-stu-id="bf072-163">In hello **hbaseapp\src\main\java\com\microsoft\examples** directory, create a new file named **SearchByEmail.java**.</span></span> <span data-ttu-id="bf072-164">Utilisez hello après le code en tant que contenu hello de ce fichier :</span><span class="sxs-lookup"><span data-stu-id="bf072-164">Use hello following code as hello contents of this file:</span></span>

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

            // Create a new regex filter
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

    <span data-ttu-id="bf072-165">Hello **SearchByEmail** classe peut être tooquery utilisé pour les lignes par adresse de messagerie.</span><span class="sxs-lookup"><span data-stu-id="bf072-165">hello **SearchByEmail** class can be used tooquery for rows by email address.</span></span> <span data-ttu-id="bf072-166">Car elle utilise un filtre d’expression régulière, vous pouvez fournir une chaîne ou une expression régulière lors de l’utilisation de classe hello.</span><span class="sxs-lookup"><span data-stu-id="bf072-166">Because it uses a regular expression filter, you can provide either a string or a regular expression when using hello class.</span></span>
5. <span data-ttu-id="bf072-167">Enregistrer hello **SearchByEmail.java** fichier.</span><span class="sxs-lookup"><span data-stu-id="bf072-167">Save hello **SearchByEmail.java** file.</span></span>
6. <span data-ttu-id="bf072-168">Bonjour **hbaseapp\src\main\hava\com\microsoft\examples** répertoire, créez un nouveau fichier nommé **DeleteTable.java**.</span><span class="sxs-lookup"><span data-stu-id="bf072-168">In hello **hbaseapp\src\main\hava\com\microsoft\examples** directory, create a new file named **DeleteTable.java**.</span></span> <span data-ttu-id="bf072-169">Utilisez hello après le code en tant que contenu hello de ce fichier :</span><span class="sxs-lookup"><span data-stu-id="bf072-169">Use hello following code as hello contents of this file:</span></span>

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

    <span data-ttu-id="bf072-170">Cette classe est pour le nettoyage de cet exemple en désactivant et suppression hello table créée par hello **CreateTable** classe.</span><span class="sxs-lookup"><span data-stu-id="bf072-170">This class is for cleaning up this example by disabling and dropping hello table created by hello **CreateTable** class.</span></span>
7. <span data-ttu-id="bf072-171">Enregistrer hello **DeleteTable.java** fichier.</span><span class="sxs-lookup"><span data-stu-id="bf072-171">Save hello **DeleteTable.java** file.</span></span>

## <a name="build-and-package-hello-application"></a><span data-ttu-id="bf072-172">Génération et package d’application de hello</span><span class="sxs-lookup"><span data-stu-id="bf072-172">Build and package hello application</span></span>
1. <span data-ttu-id="bf072-173">Ouvrez une invite de commandes et modifiez les répertoires toohello **hbaseapp** active.</span><span class="sxs-lookup"><span data-stu-id="bf072-173">Open a command prompt and change directories toohello **hbaseapp** directory.</span></span>
2. <span data-ttu-id="bf072-174">Utilisez hello suivant commande toobuild un fichier JAR contenant une application hello :</span><span class="sxs-lookup"><span data-stu-id="bf072-174">Use hello following command toobuild a JAR file that contains hello application:</span></span>

        mvn clean package

    <span data-ttu-id="bf072-175">Cela nettoie les artefacts de build précédente, télécharge les dépendances qui n’ont pas déjà été installés, puis génère et packages d’application hello.</span><span class="sxs-lookup"><span data-stu-id="bf072-175">This cleans any previous build artifacts, downloads any dependencies that have not already been installed, then builds and packages hello application.</span></span>
3. <span data-ttu-id="bf072-176">Commande hello issue, hello **hbaseapp\target** répertoire contient un fichier nommé **hbaseapp-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="bf072-176">When hello command completes, hello **hbaseapp\target** directory contains a file named **hbaseapp-1.0-SNAPSHOT.jar**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bf072-177">Hello **hbaseapp-1.0-SNAPSHOT.jar** fichier est un uber jar (parfois appelé fichier jar fat,) qui contient toutes les dépendances de hello requis application hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="bf072-177">hello **hbaseapp-1.0-SNAPSHOT.jar** file is an uber jar (sometimes called a fat jar,) which contains all hello dependencies required toorun hello application.</span></span>

## <a name="upload-hello-jar-file-and-start-a-job"></a><span data-ttu-id="bf072-178">Télécharger le fichier JAR hello et démarrer un travail</span><span class="sxs-lookup"><span data-stu-id="bf072-178">Upload hello JAR file and start a job</span></span>
<span data-ttu-id="bf072-179">Il existe plusieurs tooupload de façons un tooyour HDInsight de fichiers, comme décrit dans [télécharger des données pour les travaux Hadoop dans HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="bf072-179">There are many ways tooupload a file tooyour HDInsight cluster, as described in [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span> <span data-ttu-id="bf072-180">Hello suit utilise Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf072-180">hello following steps use Azure PowerShell.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. <span data-ttu-id="bf072-181">Après avoir installé et configuré Azure PowerShell, créez un fichier appelé **hbase-runner.psm1**.</span><span class="sxs-lookup"><span data-stu-id="bf072-181">After installing and configuring Azure PowerShell, create a new file named **hbase-runner.psm1**.</span></span> <span data-ttu-id="bf072-182">Utilisez les éléments suivants de hello en tant que contenu hello de ce fichier :</span><span class="sxs-lookup"><span data-stu-id="bf072-182">Use hello following as hello contents of this file:</span></span>

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

    <span data-ttu-id="bf072-183">Ce fichier contient deux modules :</span><span class="sxs-lookup"><span data-stu-id="bf072-183">This file contains two modules:</span></span>

   * <span data-ttu-id="bf072-184">**Ajouter-HDInsightFile** -utilisé tooupload fichiers tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="bf072-184">**Add-HDInsightFile** - used tooupload files tooHDInsight</span></span>
   * <span data-ttu-id="bf072-185">**Start-HBaseExample** -classes de hello toorun créés précédemment utilisées</span><span class="sxs-lookup"><span data-stu-id="bf072-185">**Start-HBaseExample** - used toorun hello classes created earlier</span></span>
2. <span data-ttu-id="bf072-186">Enregistrer hello **hbase-runner.psm1** fichier.</span><span class="sxs-lookup"><span data-stu-id="bf072-186">Save hello **hbase-runner.psm1** file.</span></span>
3. <span data-ttu-id="bf072-187">Ouvrir une nouvelle fenêtre Azure PowerShell, modifiez les répertoires toohello **hbaseapp** active, et puis hello exécution suivant la commande.</span><span class="sxs-lookup"><span data-stu-id="bf072-187">Open a new Azure PowerShell window, change directories toohello **hbaseapp** directory, and then run hello following command.</span></span>

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    <span data-ttu-id="bf072-188">Modifier hello chemin toohello l’emplacement de hello **hbase-runner.psm1** fichier créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="bf072-188">Change hello path toohello location of hello **hbase-runner.psm1** file created earlier.</span></span> <span data-ttu-id="bf072-189">Module de hello est inscrit pour cette session Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf072-189">This registers hello module for this Azure PowerShell session.</span></span>
4. <span data-ttu-id="bf072-190">Suivant de hello utilisez commande hello de tooupload **hbaseapp-1.0-SNAPSHOT.jar** tooyour HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="bf072-190">Use hello following command tooupload hello **hbaseapp-1.0-SNAPSHOT.jar** tooyour HDInsight cluster.</span></span>

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    <span data-ttu-id="bf072-191">Remplacez **hdinsightclustername** avec nom hello de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bf072-191">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="bf072-192">commande Hello télécharge hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **exemple/JAR** emplacement dans le stockage principal hello pour votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bf072-192">hello command uploads hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **example/jars** location in hello primary storage for your HDInsight cluster.</span></span>
5. <span data-ttu-id="bf072-193">Une fois le téléchargement de fichiers de hello, utilisez hello de code suivant toocreate une table à l’aide de hello **hbaseapp**:</span><span class="sxs-lookup"><span data-stu-id="bf072-193">After hello files are uploaded, use hello following code toocreate a table using hello **hbaseapp**:</span></span>

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    <span data-ttu-id="bf072-194">Remplacez **hdinsightclustername** avec nom hello de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bf072-194">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="bf072-195">Cette commande crée une table appelée **people** sur votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bf072-195">This command creates a new table named **people** in your HDInsight cluster.</span></span> <span data-ttu-id="bf072-196">Cette commande n’affiche pas de sortie dans la fenêtre de console hello.</span><span class="sxs-lookup"><span data-stu-id="bf072-196">This command does not show any output in hello console window.</span></span>
6. <span data-ttu-id="bf072-197">toosearch pour entrées de table hello, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="bf072-197">toosearch for entries in hello table, use hello following command:</span></span>

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    <span data-ttu-id="bf072-198">Remplacez **hdinsightclustername** avec nom hello de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bf072-198">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="bf072-199">Cette commande utilise hello **SearchByEmail** classe toosearch pour toutes les lignes où hello **contactinformation** famille de colonne et hello **messagerie** colonne, contient la chaîne de hello **contoso.com**. Vous devez recevoir hello suivant des résultats :</span><span class="sxs-lookup"><span data-stu-id="bf072-199">This command uses hello **SearchByEmail** class toosearch for any rows where hello **contactinformation** column family and hello **email** column, contains hello string **contoso.com**. You should receive hello following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="bf072-200">À l’aide de **fabrikam.com** pour hello `-emailRegex` valeur retourne les utilisateurs hello ayant **fabrikam.com** dans le champ d’adresse de messagerie hello.</span><span class="sxs-lookup"><span data-stu-id="bf072-200">Using **fabrikam.com** for hello `-emailRegex` value returns hello users that have **fabrikam.com** in hello email field.</span></span> <span data-ttu-id="bf072-201">Étant donné que cette recherche est implémentée à l’aide d’un filtre basé sur une expression régulière, vous pouvez également entrer des expressions régulières, tels que **^ r**, les entrées qui retourne où commence l’e-mail de hello avec hello lettre « r ».</span><span class="sxs-lookup"><span data-stu-id="bf072-201">Since this search is implemented by using a regular expression-based filter, you can also enter regular expressions, such as **^r**, which returns entries where hello email begins with hello letter 'r'.</span></span>

## <a name="delete-hello-table"></a><span data-ttu-id="bf072-202">Supprimer une table de hello</span><span class="sxs-lookup"><span data-stu-id="bf072-202">Delete hello table</span></span>
<span data-ttu-id="bf072-203">Lorsque vous avez terminé avec l’exemple de hello, suivant de hello utilisez commande de hello de hello Azure PowerShell session toodelete **personnes** table utilisée dans cet exemple :</span><span class="sxs-lookup"><span data-stu-id="bf072-203">When you are done with hello example, use hello following command from hello Azure PowerShell session toodelete hello **people** table used in this example:</span></span>

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

<span data-ttu-id="bf072-204">Remplacez **hdinsightclustername** avec nom hello de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bf072-204">Replace **hdinsightclustername** with hello name of your HDInsight cluster.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="bf072-205">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="bf072-205">Troubleshooting</span></span>
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="bf072-206">Aucun résultat ou résultat inattendu lors de l'utilisation de Start-HBaseExample</span><span class="sxs-lookup"><span data-stu-id="bf072-206">No results or unexpected results when using Start-HBaseExample</span></span>
<span data-ttu-id="bf072-207">Hello d’utilisation `-showErr` paramètre tooview hello erreur standard (STDERR) qui est généré lors de la tâche de hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="bf072-207">Use hello `-showErr` parameter tooview hello standard error (STDERR) that is produced while running hello job.</span></span>
