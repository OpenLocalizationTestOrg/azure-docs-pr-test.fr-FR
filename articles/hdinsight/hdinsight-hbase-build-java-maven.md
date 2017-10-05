---
title: "Créer une application Java HBase pour Azure HDInsight | Microsoft Docs"
description: "Découvrez comment utiliser Apache Maven pour créer une application Java Apache HBase, puis la déployer dans un cluster Azure HDInsight basé sur Windows."
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
ms.openlocfilehash: 59c9af5a91b107e68a676f02fe5a936f955b22fa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-maven-to-build-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a><span data-ttu-id="e5b8e-103">Utilisation de Maven pour créer des applications Java utilisant HBase avec HDInsight (Hadoop) sous Windows</span><span class="sxs-lookup"><span data-stu-id="e5b8e-103">Use Maven to build Java applications that use HBase with Windows-based HDInsight (Hadoop)</span></span>
<span data-ttu-id="e5b8e-104">Apprenez à créer et à générer une application [Apache HBase](http://hbase.apache.org/) dans Java à l'aide d'Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-104">Learn how to create and build an [Apache HBase](http://hbase.apache.org/) application in Java by using Apache Maven.</span></span> <span data-ttu-id="e5b8e-105">Utilisez ensuite l'application avec Azure HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="e5b8e-105">Then use the application with Azure HDInsight (Hadoop).</span></span>

<span data-ttu-id="e5b8e-106">[Maven](http://maven.apache.org/) est un outil de gestion de projets logiciels et d'inclusion qui vous permet de créer des logiciels, de la documentation et des rapports pour les projets Java.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-106">[Maven](http://maven.apache.org/) is a software project management and comprehension tool that allows you to build software, documentation, and reports for Java projects.</span></span> <span data-ttu-id="e5b8e-107">Dans cet article, vous apprendrez à l’utiliser de façon à créer une application Java de base permettant de créer ou de supprimer une table HBase dans un cluster Azure HDInsight, ainsi que de lui envoyer des requêtes.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-107">In this article, you learn how to use it to create a basic Java application that that creates, queries, and deletes an HBase table on an Azure HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5b8e-108">Les étapes décrites dans ce document nécessitent un cluster HDInsight utilisant Windows.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-108">The steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="e5b8e-109">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e5b8e-110">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e5b8e-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="requirements"></a><span data-ttu-id="e5b8e-111">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="e5b8e-111">Requirements</span></span>
* <span data-ttu-id="e5b8e-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 ou version supérieure</span><span class="sxs-lookup"><span data-stu-id="e5b8e-112">[Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 or later</span></span>
* [<span data-ttu-id="e5b8e-113">Maven</span><span class="sxs-lookup"><span data-stu-id="e5b8e-113">Maven</span></span>](http://maven.apache.org/)
* <span data-ttu-id="e5b8e-114">Un cluster HDInsight sous Windows avec HBase</span><span class="sxs-lookup"><span data-stu-id="e5b8e-114">A Windows-based HDInsight cluster with HBase</span></span>

    > [!NOTE]
    > <span data-ttu-id="e5b8e-115">Les étapes décrites dans ce document ont été testées avec des versions de cluster HDInsight 3.2 et 3.3.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-115">The steps in this document have been tested with HDInsight cluster versions 3.2 and 3.3.</span></span> <span data-ttu-id="e5b8e-116">Les valeurs par défaut fournies dans les exemples concernent un cluster HDInsight 3.3.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-116">The default values provided in examples are for a HDInsight 3.3 cluster.</span></span>

## <a name="create-the-project"></a><span data-ttu-id="e5b8e-117">Création du projet</span><span class="sxs-lookup"><span data-stu-id="e5b8e-117">Create the project</span></span>
1. <span data-ttu-id="e5b8e-118">À partir de la ligne de commande de votre environnement de développement, modifiez les répertoires pour indiquer l’emplacement auquel vous souhaitez créer le projet, par exemple `cd code\hdinsight`.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-118">From the command line in your development environment, change directories to the location where you want to create the project, for example, `cd code\hdinsight`.</span></span>
2. <span data-ttu-id="e5b8e-119">Utilisez la commande **mvn** , installée avec Maven, pour générer la structure du projet.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-119">Use the **mvn** command, which is installed with Maven, to generate the scaffolding for the project.</span></span>

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    <span data-ttu-id="e5b8e-120">Cette commande permet de créer un répertoire dans le répertoire actuel avec le nom spécifié par le paramètre **artifactID** (**hbaseapp** dans cet exemple.) Le répertoire contient les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e5b8e-120">This command creates a directory in the current location, with the name specified by the **artifactID** parameter (**hbaseapp** in this example.) This directory contains the following items:</span></span>

   * <span data-ttu-id="e5b8e-121">**pom.xml** : le modèle d’objet du projet ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contient les informations et la configuration utilisées pour générer le projet.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-121">**pom.xml**:  The Project Object Model ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contains information and configuration details used to build the project.</span></span>
   * <span data-ttu-id="e5b8e-122">**src** : répertoire contenant le répertoire **main\java\com\microsoft\examples**, dans lequel vous créerez l’application.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-122">**src**: The directory that contains the **main\java\com\microsoft\examples** directory, where you will author the application.</span></span>
3. <span data-ttu-id="e5b8e-123">Supprimez le fichier **src\test\java\com\microsoft\examples\apptest.java**, car il ne sera pas utilisé dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-123">Delete the **src\test\java\com\microsoft\examples\apptest.java** file because it is not used in this example.</span></span>

## <a name="update-the-project-object-model"></a><span data-ttu-id="e5b8e-124">Mise à jour du modèle d'objet du projet</span><span class="sxs-lookup"><span data-stu-id="e5b8e-124">Update the Project Object Model</span></span>
1. <span data-ttu-id="e5b8e-125">Modifiez le fichier **pom.xml** et ajoutez le code suivant dans la section `<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="e5b8e-125">Edit the **pom.xml** file and add the following code inside the `<dependencies>` section:</span></span>

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    <span data-ttu-id="e5b8e-126">Cette section indique à Maven que le projet nécessite **hbase-client** version **1.1.2**.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-126">This section tells Maven that the project requires **hbase-client** version **1.1.2**.</span></span> <span data-ttu-id="e5b8e-127">Au moment de la compilation, cette dépendance est téléchargée à partir du référentiel Maven par défaut.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-127">At compile time, this dependency is downloaded from the default Maven repository.</span></span> <span data-ttu-id="e5b8e-128">Vous pouvez utiliser la [Recherche du référentiel central Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) pour en savoir plus sur cette dépendance.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-128">You can use the [Maven Central Repository Search](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) to learn more about this dependency.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="e5b8e-129">Le numéro de version doit correspondre à la version de HBase fournie avec votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-129">The version number must match the version of HBase that is provided with your HDInsight cluster.</span></span> <span data-ttu-id="e5b8e-130">Utilisez le tableau suivant pour trouver le numéro de version correct.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-130">Use the following table to find the correct version number.</span></span>
   >
   >

   | <span data-ttu-id="e5b8e-131">Version de cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5b8e-131">HDInsight cluster version</span></span> | <span data-ttu-id="e5b8e-132">Version HBase à utiliser</span><span class="sxs-lookup"><span data-stu-id="e5b8e-132">HBase version to use</span></span> |
   | --- | --- |
   | <span data-ttu-id="e5b8e-133">3.2</span><span class="sxs-lookup"><span data-stu-id="e5b8e-133">3.2</span></span> |<span data-ttu-id="e5b8e-134">0.98.4-hadoop2</span><span class="sxs-lookup"><span data-stu-id="e5b8e-134">0.98.4-hadoop2</span></span> |
   | <span data-ttu-id="e5b8e-135">3.3</span><span class="sxs-lookup"><span data-stu-id="e5b8e-135">3.3</span></span> |<span data-ttu-id="e5b8e-136">1.1.2</span><span class="sxs-lookup"><span data-stu-id="e5b8e-136">1.1.2</span></span> |

    <span data-ttu-id="e5b8e-137">Pour plus d’informations sur les versions et composants HDInsight, voir [Quels sont les différents composants Hadoop disponibles avec HDInsight ?](hdinsight-component-versioning.md)</span><span class="sxs-lookup"><span data-stu-id="e5b8e-137">For more information on HDInsight versions and components, see [What are the different Hadoop components available with HDInsight](hdinsight-component-versioning.md).</span></span>
2. <span data-ttu-id="e5b8e-138">Si vous utilisez un cluster HDInsight 3.3, vous devez également ajouter le code suivant à la section `<dependencies>` :</span><span class="sxs-lookup"><span data-stu-id="e5b8e-138">If you are using an HDInsight 3.3 cluster, you must also add the following to the `<dependencies>` section:</span></span>

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    <span data-ttu-id="e5b8e-139">Cette dépendance charge les composants de base phoenix utilisés par HBase version 1.1.x.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-139">This dependency will load the phoenix-core components, which are used by Hbase version 1.1.x.</span></span>
3. <span data-ttu-id="e5b8e-140">Ajoutez le code suivant au fichier **pom.xml**.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-140">Add the following code to the **pom.xml** file.</span></span> <span data-ttu-id="e5b8e-141">Cette section doit être contenue entre les balises `<project>...</project>` dans le fichier, par exemple entre `</dependencies>` et `</project>`.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-141">This section must be inside the `<project>...</project>` tags in the file, for example, between `</dependencies>` and `</project>`.</span></span>

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

    <span data-ttu-id="e5b8e-142">La section `<resources>` configure une ressource (**conf\hbase-site.xml**) qui contient des informations de configuration pour HBase.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-142">The `<resources>` section configures a resource (**conf\hbase-site.xml**) that contains configuration information for HBase.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e5b8e-143">Vous pouvez également définir les valeurs de configuration par code.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-143">You can also set configuration values via code.</span></span> <span data-ttu-id="e5b8e-144">Consultez les commentaires de l’exemple **CreateTable** ci-dessous pour la marche à suivre.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-144">See the comments in the **CreateTable** example that follows for how to do this.</span></span>
   >
   >

    <span data-ttu-id="e5b8e-145">La section `<plugins>` configure également les plug-ins [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) et [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span><span class="sxs-lookup"><span data-stu-id="e5b8e-145">This `<plugins>` section configures the [Maven Compiler Plugin](http://maven.apache.org/plugins/maven-compiler-plugin/) and [Maven Shade Plugin](http://maven.apache.org/plugins/maven-shade-plugin/).</span></span> <span data-ttu-id="e5b8e-146">Le plug-in compiler est utilisé pour compiler la topologie.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-146">The compiler plug-in is used to compile the topology.</span></span> <span data-ttu-id="e5b8e-147">Le plug-in shade est utilisé pour empêcher la duplication de licence dans le package JAR généré par Maven.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-147">The shade plug-in is used to prevent license duplication in the JAR package that is built by Maven.</span></span> <span data-ttu-id="e5b8e-148">Il est utilisé, car les fichiers de licence dupliqués entraînent une erreur à l'exécution sur le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-148">The reason this is used is that the duplicate license files cause an error at run time on the HDInsight cluster.</span></span> <span data-ttu-id="e5b8e-149">Le fait d'utiliser le plug-in maven-shade-plugin avec l'implémentation `ApacheLicenseResourceTransformer` permet d'éviter cette erreur.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-149">Using maven-shade-plugin with the `ApacheLicenseResourceTransformer` implementation prevents this error.</span></span>

    <span data-ttu-id="e5b8e-150">Le plug-in maven-shade-plugin produit également un uber jar (ou fat jar) contenant toutes les dépendances requises par l’application.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-150">The maven-shade-plugin also produces an uber jar (or fat jar) that contains all the dependencies required by the application.</span></span>
4. <span data-ttu-id="e5b8e-151">Enregistrez le fichier **pom.xml** .</span><span class="sxs-lookup"><span data-stu-id="e5b8e-151">Save the **pom.xml** file.</span></span>
5. <span data-ttu-id="e5b8e-152">Créez un répertoire appelé **conf** dans le répertoire **hbaseapp**.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-152">Create a new directory named **conf** in the **hbaseapp** directory.</span></span> <span data-ttu-id="e5b8e-153">Dans le répertoire **conf**, créez un fichier nommé **hbase-site.xml**.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-153">In the **conf** directory, create a file named **hbase-site.xml**.</span></span> <span data-ttu-id="e5b8e-154">Utilisez les données suivantes comme contenu du fichier :</span><span class="sxs-lookup"><span data-stu-id="e5b8e-154">Use the following as the contents of the file:</span></span>

        <?xml version="1.0"?>
        <?xml-stylesheet type="text/xsl" href="configuration.xsl"?>
        <!--
        /**
          * Copyright 2010 The Apache Software Foundation
          *
          * Licensed to the Apache Software Foundation (ASF) under one
          * or more contributor license agreements.  See the NOTICE file
          * distributed with this work for additional information
          * regarding copyright ownership.  The ASF licenses this file
          * to you under the Apache License, Version 2.0 (the
          * "License"); you may not use this file except in compliance
          * with the License.  You may obtain a copy of the License at
          *
          *     http://www.apache.org/licenses/LICENSE-2.0
          *
          * Unless required by applicable law or agreed to in writing, software
          * distributed under the License is distributed on an "AS IS" BASIS,
          * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
          * See the License for the specific language governing permissions and
          * limitations under the License.
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

    <span data-ttu-id="e5b8e-155">Ce fichier sera utilisé pour charger la configuration HBase pour un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-155">This file will be used to load the HBase configuration for an HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e5b8e-156">Il s’agit d’un fichier hbase-site.xml de base contenant les paramètres minimaux pour le cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-156">This is a minimal hbase-site.xml file, and it contains the bare minimum settings for the HDInsight cluster.</span></span>

6. <span data-ttu-id="e5b8e-157">Enregistrez le fichier **hbase-site.xml**.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-157">Save the **hbase-site.xml** file.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="e5b8e-158">Création de l'application</span><span class="sxs-lookup"><span data-stu-id="e5b8e-158">Create the application</span></span>
1. <span data-ttu-id="e5b8e-159">Accédez au répertoire **hbaseapp\src\main\java\com\microsoft\examples** et renommez le fichier app.java en **CreateTable.java**.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-159">Go to the **hbaseapp\src\main\java\com\microsoft\examples** directory and rename the app.java file to **CreateTable.java**.</span></span>
2. <span data-ttu-id="e5b8e-160">Ouvrez le fichier **CreateTable.java** et remplacez le contenu existant par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="e5b8e-160">Open the **CreateTable.java** file and replace the existing contents with the following code:</span></span>

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
            // The following sets the znode root for Linux-based HDInsight
            //config.set("zookeeper.znode.parent","/hbase-unsecure");

            // create an admin object using the config
            HBaseAdmin admin = new HBaseAdmin(config);

            // create the table...
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

            // Add each person to the table
            //   Use the `name` column family for the name
            //   Use the `contactinfo` column family for the email
            for (int i = 0; i< people.length; i++) {
              Put person = new Put(Bytes.toBytes(people[i][0]));
              person.add(Bytes.toBytes("name"), Bytes.toBytes("first"), Bytes.toBytes(people[i][1]));
              person.add(Bytes.toBytes("name"), Bytes.toBytes("last"), Bytes.toBytes(people[i][2]));
              person.add(Bytes.toBytes("contactinfo"), Bytes.toBytes("email"), Bytes.toBytes(people[i][3]));
              table.put(person);
            }
            // flush commits and close the table
            table.flushCommits();
            table.close();
          }
        }

    <span data-ttu-id="e5b8e-161">Il s’agit de la classe **CreateTable**, qui crée une table appelée **people** et la remplit avec des utilisateurs prédéfinis.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-161">This is the **CreateTable** class, which will create a table named **people** and populate it with some predefined users.</span></span>
3. <span data-ttu-id="e5b8e-162">Enregistrez le fichier **CreateTable.java**.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-162">Save the **CreateTable.java** file.</span></span>
4. <span data-ttu-id="e5b8e-163">Dans le répertoire **hbaseapp\src\main\java\com\microsoft\examples**, créez un fichier nommé **SearchByEmail.java**.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-163">In the **hbaseapp\src\main\java\com\microsoft\examples** directory, create a new file named **SearchByEmail.java**.</span></span> <span data-ttu-id="e5b8e-164">Utilisez le code suivant comme contenu de ce fichier :</span><span class="sxs-lookup"><span data-stu-id="e5b8e-164">Use the following code as the contents of this file:</span></span>

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

            // Use GenericOptionsParser to get only the parameters to the class
            // and not all the parameters passed (when using WebHCat for example)
            String[] otherArgs = new GenericOptionsParser(config, args).getRemainingArgs();
            if (otherArgs.length != 1) {
              System.out.println("usage: [regular expression]");
              System.exit(-1);
            }

            // Open the table
            HTable table = new HTable(config, "people");

            // Define the family and qualifiers to be used
            byte[] contactFamily = Bytes.toBytes("contactinfo");
            byte[] emailQualifier = Bytes.toBytes("email");
            byte[] nameFamily = Bytes.toBytes("name");
            byte[] firstNameQualifier = Bytes.toBytes("first");
            byte[] lastNameQualifier = Bytes.toBytes("last");

            // Create a new regex filter
            RegexStringComparator emailFilter = new RegexStringComparator(otherArgs[0]);
            // Attach the regex filter to a filter
            //   for the email column
            SingleColumnValueFilter filter = new SingleColumnValueFilter(
              contactFamily,
              emailQualifier,
              CompareOp.EQUAL,
              emailFilter
            );

            // Create a scan and set the filter
            Scan scan = new Scan();
            scan.setFilter(filter);

            // Get the results
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

    <span data-ttu-id="e5b8e-165">La classe **SearchByEmail** peut être utilisée pour lancer des requêtes sur les lignes d’adresses électroniques.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-165">The **SearchByEmail** class can be used to query for rows by email address.</span></span> <span data-ttu-id="e5b8e-166">Puisqu'elle utilise un filtre d'expression régulière, vous pouvez fournir une chaîne ou une expression régulière lorsque vous utilisez la classe.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-166">Because it uses a regular expression filter, you can provide either a string or a regular expression when using the class.</span></span>
5. <span data-ttu-id="e5b8e-167">Enregistrez le fichier **SearchByEmail.java**.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-167">Save the **SearchByEmail.java** file.</span></span>
6. <span data-ttu-id="e5b8e-168">Dans le répertoire **hbaseapp\src\main\hava\com\microsoft\examples**, créez un fichier nommé **DeleteTable.java**.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-168">In the **hbaseapp\src\main\hava\com\microsoft\examples** directory, create a new file named **DeleteTable.java**.</span></span> <span data-ttu-id="e5b8e-169">Utilisez le code suivant comme contenu de ce fichier :</span><span class="sxs-lookup"><span data-stu-id="e5b8e-169">Use the following code as the contents of this file:</span></span>

        package com.microsoft.examples;
        import java.io.IOException;

        import org.apache.hadoop.conf.Configuration;
        import org.apache.hadoop.hbase.HBaseConfiguration;
        import org.apache.hadoop.hbase.client.HBaseAdmin;

        public class DeleteTable {
          public static void main(String[] args) throws IOException {
            Configuration config = HBaseConfiguration.create();

            // Create an admin object using the config
            HBaseAdmin admin = new HBaseAdmin(config);

            // Disable, and then delete the table
            admin.disableTable("people");
            admin.deleteTable("people");
          }
        }

    <span data-ttu-id="e5b8e-170">Cette classe permet de nettoyer cet exemple en désactivant puis en supprimant la table créée par la classe **CreateTable**.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-170">This class is for cleaning up this example by disabling and dropping the table created by the **CreateTable** class.</span></span>
7. <span data-ttu-id="e5b8e-171">Enregistrez le fichier **DeleteTable.java**.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-171">Save the **DeleteTable.java** file.</span></span>

## <a name="build-and-package-the-application"></a><span data-ttu-id="e5b8e-172">Génération et package de l'application</span><span class="sxs-lookup"><span data-stu-id="e5b8e-172">Build and package the application</span></span>
1. <span data-ttu-id="e5b8e-173">Ouvrez une invite de commandes et passez au répertoire **hbaseapp**.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-173">Open a command prompt and change directories to the **hbaseapp** directory.</span></span>
2. <span data-ttu-id="e5b8e-174">Utilisez la commande suivante pour générer un fichier JAR contenant l'application :</span><span class="sxs-lookup"><span data-stu-id="e5b8e-174">Use the following command to build a JAR file that contains the application:</span></span>

        mvn clean package

    <span data-ttu-id="e5b8e-175">Cela nettoie les artefacts de build précédents, télécharge toute dépendance non encore installée, puis génère et met l'application en package.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-175">This cleans any previous build artifacts, downloads any dependencies that have not already been installed, then builds and packages the application.</span></span>
3. <span data-ttu-id="e5b8e-176">Une fois la commande exécutée, le répertoire **hbaseapp\target** contient un fichier appelé **hbaseapp-1.0-SNAPSHOT.jar**.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-176">When the command completes, the **hbaseapp\target** directory contains a file named **hbaseapp-1.0-SNAPSHOT.jar**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e5b8e-177">Le fichier **hbaseapp-1.0-SNAPSHOT.jar** est un uber jar (parfois appelé fat jar) contenant toutes les dépendances requises pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-177">The **hbaseapp-1.0-SNAPSHOT.jar** file is an uber jar (sometimes called a fat jar,) which contains all the dependencies required to run the application.</span></span>

## <a name="upload-the-jar-file-and-start-a-job"></a><span data-ttu-id="e5b8e-178">Téléchargement du fichier JAR et démarrage d'une tâche</span><span class="sxs-lookup"><span data-stu-id="e5b8e-178">Upload the JAR file and start a job</span></span>
<span data-ttu-id="e5b8e-179">Il existe de nombreuses façons de télécharger un fichier vers votre cluster HDInsight, comme décrit dans la rubrique [Téléchargement de données pour les tâches Hadoop dans HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="e5b8e-179">There are many ways to upload a file to your HDInsight cluster, as described in [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span> <span data-ttu-id="e5b8e-180">Les étapes suivantes utilisent Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-180">The following steps use Azure PowerShell.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. <span data-ttu-id="e5b8e-181">Après avoir installé et configuré Azure PowerShell, créez un fichier appelé **hbase-runner.psm1**.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-181">After installing and configuring Azure PowerShell, create a new file named **hbase-runner.psm1**.</span></span> <span data-ttu-id="e5b8e-182">Utilisez les données suivantes comme contenu de ce fichier :</span><span class="sxs-lookup"><span data-stu-id="e5b8e-182">Use the following as the contents of this file:</span></span>

        <#
        .SYNOPSIS
        Copies a file to the primary storage of an HDInsight cluster.
        .DESCRIPTION
        Copies a file from a local directory to the blob container for
        the HDInsight cluster.
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
        #The class to run
        [Parameter(Mandatory = $true)]
        [String]$className,

        #The name of the HDInsight cluster
        [Parameter(Mandatory = $true)]
        [String]$clusterName,

        #Only used when using SearchByEmail
        [Parameter(Mandatory = $false)]
        [String]$emailRegex,

        #Use if you want to see stderr output
        [Parameter(Mandatory = $false)]
        [Switch]$showErr
        )

        Set-StrictMode -Version 3

        # Is the Azure module installed?
        FindAzure

        # Get the login for the HDInsight cluster
        $creds=Get-Credential -Message "Enter the login for the cluster" -UserName "admin"

        # The JAR
        $jarFile = "wasb:///example/jars/hbaseapp-1.0-SNAPSHOT.jar"

        # The job definition
        $jobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
            -JarFile $jarFile `
            -ClassName $className `
            -Arguments $emailRegex

        # Get the job output
        $job = Start-AzureRmHDInsightJob `
            -ClusterName $clusterName `
            -JobDefinition $jobDefinition `
            -HttpCredential $creds
        Write-Host "Wait for the job to complete ..." -ForegroundColor Green
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
        Write-Host "Display the standard output ..." -ForegroundColor Green
        Get-AzureRmHDInsightJobOutput `
                    -Clustername $clusterName `
                    -JobId $job.JobId `
                    -HttpCredential $creds
        }

        <#
        .SYNOPSIS
        Copies a file to the primary storage of an HDInsight cluster.
        .DESCRIPTION
        Copies a file from a local directory to the blob container for
        the HDInsight cluster.
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
                #The path to the local file.
                [Parameter(Mandatory = $true)]
                [String]$localPath,

                #The destination path and file name, relative to the root of the container.
                [Parameter(Mandatory = $true)]
                [String]$destinationPath,

                #The name of the HDInsight cluster
                [Parameter(Mandatory = $true)]
                [String]$clusterName,

                #If specified, overwrites existing files without prompting
                [Parameter(Mandatory = $false)]
                [Switch]$force
            )

            Set-StrictMode -Version 3

            # Is the Azure module installed?
            FindAzure

            # Get authentication for the cluster
            $creds=Get-Credential

            # Does the local path exist?
            if (-not (Test-Path $localPath))
            {
                throw "Source path '$localPath' does not exist."
            }

            # Get the primary storage container
            $storage = GetStorage -clusterName $clusterName

            # Upload file to storage, overwriting existing files if -force was used.
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
                throw "No active Azure subscription found! If you have a subscription, use the Login-AzureRmAccount cmdlet to login to your subscription."
            }
        }

        function GetStorage {
            param(
                [Parameter(Mandatory = $true)]
                [String]$clusterName
            )
            $hdi = Get-AzureRmHDInsightCluster -ClusterName $clusterName
            # Does the cluster exist?
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
            # Get the resource group, in case we need that
            $return.resourceGroup = $resourceGroup
            # Get the storage context, as we can't depend
            # on using the default storage context
            $return.context = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey
            # Get the container, so we know where to
            # find/store blobs
            $return.container = $container
            # Return storage accounts to support finding all accounts for
            # a cluster
            $return.storageAccount = $storageAccountName
            $return.storageAccountKey = $storageAccountKey

            return $return
        }
        # Only export the verb-phrase things
        export-modulemember *-*

    <span data-ttu-id="e5b8e-183">Ce fichier contient deux modules :</span><span class="sxs-lookup"><span data-stu-id="e5b8e-183">This file contains two modules:</span></span>

   * <span data-ttu-id="e5b8e-184">**Add-HDInsightFile** permet de télécharger des fichiers vers HDInsight</span><span class="sxs-lookup"><span data-stu-id="e5b8e-184">**Add-HDInsightFile** - used to upload files to HDInsight</span></span>
   * <span data-ttu-id="e5b8e-185">**Start-HBaseExample** permet d’exécuter les classes créées antérieurement</span><span class="sxs-lookup"><span data-stu-id="e5b8e-185">**Start-HBaseExample** - used to run the classes created earlier</span></span>
2. <span data-ttu-id="e5b8e-186">Enregistrez le fichier **hbase-runner.psm1**.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-186">Save the **hbase-runner.psm1** file.</span></span>
3. <span data-ttu-id="e5b8e-187">Ouvrez une nouvelle fenêtre Azure PowerShell, accédez au répertoire **hbaseapp**, puis exécutez la commande ci-après.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-187">Open a new Azure PowerShell window, change directories to the **hbaseapp** directory, and then run the following command.</span></span>

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    <span data-ttu-id="e5b8e-188">Remplacez le chemin d’accès par l’emplacement du fichier **hbase-runner.psm1** créé plus tôt.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-188">Change the path to the location of the **hbase-runner.psm1** file created earlier.</span></span> <span data-ttu-id="e5b8e-189">Cela enregistrera le module pour cette session Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-189">This registers the module for this Azure PowerShell session.</span></span>
4. <span data-ttu-id="e5b8e-190">Utilisez la commande ci-après pour télécharger le fichier **hbaseapp-1.0-SNAPSHOT.jar** sur votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-190">Use the following command to upload the **hbaseapp-1.0-SNAPSHOT.jar** to your HDInsight cluster.</span></span>

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    <span data-ttu-id="e5b8e-191">Remplacez **hdinsightclustername** par le nom de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-191">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span> <span data-ttu-id="e5b8e-192">Cette commande télécharge le fichier **hbaseapp-1.0-SNAPSHOT.jar** vers le répertoire **example/jars** du stockage principal de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-192">The command uploads the **hbaseapp-1.0-SNAPSHOT.jar** to the **example/jars** location in the primary storage for your HDInsight cluster.</span></span>
5. <span data-ttu-id="e5b8e-193">Une fois les fichiers téléchargés, utilisez le code suivant pour créer une table avec **hbaseapp** :</span><span class="sxs-lookup"><span data-stu-id="e5b8e-193">After the files are uploaded, use the following code to create a table using the **hbaseapp**:</span></span>

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    <span data-ttu-id="e5b8e-194">Remplacez **hdinsightclustername** par le nom de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-194">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="e5b8e-195">Cette commande crée une table appelée **people** sur votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-195">This command creates a new table named **people** in your HDInsight cluster.</span></span> <span data-ttu-id="e5b8e-196">Cette commande n'affiche aucune sortie dans la fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-196">This command does not show any output in the console window.</span></span>
6. <span data-ttu-id="e5b8e-197">Pour rechercher des entrées dans la table, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e5b8e-197">To search for entries in the table, use the following command:</span></span>

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    <span data-ttu-id="e5b8e-198">Remplacez **hdinsightclustername** par le nom de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-198">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="e5b8e-199">Cette commande utilise la classe **SearchByEmail** pour rechercher les lignes dans lesquelles la famille de colonnes **contactinformation** et la colonne **email** contiennent la chaîne **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-199">This command uses the **SearchByEmail** class to search for any rows where the **contactinformation** column family and the **email** column, contains the string **contoso.com**.</span></span> <span data-ttu-id="e5b8e-200">Les résultats suivants doivent s'afficher :</span><span class="sxs-lookup"><span data-stu-id="e5b8e-200">You should receive the following results:</span></span>

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    <span data-ttu-id="e5b8e-201">L’utilisation de **fabrikam.com** pour la valeur `-emailRegex` renvoie les utilisateurs dont le champ email contient **fabrikam.com**.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-201">Using **fabrikam.com** for the `-emailRegex` value returns the users that have **fabrikam.com** in the email field.</span></span> <span data-ttu-id="e5b8e-202">Cette recherche étant implémentée à l’aide d’un filtre d’expression régulière, vous pouvez également saisir des expressions régulières telles que **^r**, qui renvoie les entrées dont le champ email commence par la lettre r.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-202">Since this search is implemented by using a regular expression-based filter, you can also enter regular expressions, such as **^r**, which returns entries where the email begins with the letter 'r'.</span></span>

## <a name="delete-the-table"></a><span data-ttu-id="e5b8e-203">Suppression de la table</span><span class="sxs-lookup"><span data-stu-id="e5b8e-203">Delete the table</span></span>
<span data-ttu-id="e5b8e-204">Lorsque vous avez terminé, utilisez la commande ci-après dans la session Azure PowerShell pour supprimer la table **people** utilisée dans l’exemple :</span><span class="sxs-lookup"><span data-stu-id="e5b8e-204">When you are done with the example, use the following command from the Azure PowerShell session to delete the **people** table used in this example:</span></span>

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

<span data-ttu-id="e5b8e-205">Remplacez **hdinsightclustername** par le nom de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-205">Replace **hdinsightclustername** with the name of your HDInsight cluster.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e5b8e-206">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="e5b8e-206">Troubleshooting</span></span>
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a><span data-ttu-id="e5b8e-207">Aucun résultat ou résultat inattendu lors de l'utilisation de Start-HBaseExample</span><span class="sxs-lookup"><span data-stu-id="e5b8e-207">No results or unexpected results when using Start-HBaseExample</span></span>
<span data-ttu-id="e5b8e-208">Utilisez le paramètre `-showErr` pour afficher l’erreur standard (STDERR) produite lors de l'exécution de la tâche.</span><span class="sxs-lookup"><span data-stu-id="e5b8e-208">Use the `-showErr` parameter to view the standard error (STDERR) that is produced while running the job.</span></span>
