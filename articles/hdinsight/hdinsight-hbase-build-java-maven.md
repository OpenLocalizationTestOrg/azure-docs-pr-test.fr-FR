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
# <a name="use-maven-toobuild-java-applications-that-use-hbase-with-windows-based-hdinsight-hadoop"></a>Utiliser des applications Java Maven toobuild qui utilisent HBase hdinsight basés sur Windows (Hadoop)
Découvrez comment toocreate et générer un [Apache HBase](http://hbase.apache.org/) application Java à l’aide d’Apache Maven. Utilisez application hello avec Azure HDInsight (Hadoop).

[Maven](http://maven.apache.org/) est un outil de projet logiciel de gestion et compréhension qui vous permet de toobuild logiciel, la documentation et des rapports pour les projets de Java. Dans cet article, vous apprendrez comment toouse il toocreate une application Java de base qui crée, interroge, et supprime un HBase sur un cluster Azure HDInsight de table.

> [!IMPORTANT]
> étapes de Hello dans ce document nécessitent un cluster HDInsight qui utilise Windows. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="requirements"></a>Configuration requise
* [Java platform JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 7 ou version supérieure
* [Maven](http://maven.apache.org/)
* Un cluster HDInsight sous Windows avec HBase

    > [!NOTE]
    > étapes Hello dans ce document ont été testés avec des versions 3.2 et 3.3 du cluster HDInsight. les valeurs par défaut Hello fournies dans les exemples sont pour un cluster HDInsight 3.3.

## <a name="create-hello-project"></a>Créer le projet de hello
1. À partir de la ligne de commande hello dans votre environnement de développement, modifiez les répertoires toohello emplacement souhaité projet hello de toocreate, par exemple, `cd code\hdinsight`.
2. Hello d’utilisation **mvn** commande, qui est installé avec Maven, hello toogenerate génération de modèles automatique pour le projet de hello.

        mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=hbaseapp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

    Cette commande crée un répertoire dans l’emplacement actuel de hello, avec le nom hello spécifié par hello **artifactID** paramètre (**hbaseapp** dans cet exemple.) Ce répertoire contient hello éléments suivants :

   * **pom.XML**: hello du modèle objet Project ([POM](http://maven.apache.org/guides/introduction/introduction-to-the-pom.html)) contient des informations et la configuration du projet de hello détails utilisés toobuild.
   * **src**: répertoire hello contenant hello **main\java\com\microsoft\examples** répertoire, où vous allez créer l’application hello.
3. Supprimer hello **src\test\java\com\microsoft\examples\apptest.java** , car il n’est pas utilisé dans cet exemple de fichier.

## <a name="update-hello-project-object-model"></a>Mettre à jour hello modèle objet Project
1. Modifier hello **pom.xml** et ajoutez hello suivant du code à l’intérieur de hello `<dependencies>` section :

        <dependency>
          <groupId>org.apache.hbase</groupId>
          <artifactId>hbase-client</artifactId>
          <version>1.1.2</version>
        </dependency>

    Cette section explique Maven qui hello projet nécessite **hbase-client** version **1.1.2**. Au moment de la compilation, cette dépendance est téléchargée à partir du référentiel de Maven hello par défaut. Vous pouvez utiliser hello [recherche de référentiel centrale Maven](http://search.maven.org/#artifactdetails%7Corg.apache.hbase%7Chbase-client%7C0.98.4-hadoop2%7Cjar) toolearn plus d’informations sur cette dépendance.

   > [!IMPORTANT]
   > numéro de version Hello doit correspondre au version hello de HBase qui est fourni avec votre cluster HDInsight. Utilisez hello suivant le numéro de version correct de table toofind hello.
   >
   >

   | Version de cluster HDInsight | HBase version toouse |
   | --- | --- |
   | 3.2 |0.98.4-hadoop2 |
   | 3.3 |1.1.2 |

    Pour plus d’informations sur les composants et les versions de HDInsight, consultez [quels sont les composants Hadoop hello différents disponibles avec HDInsight](hdinsight-component-versioning.md).
2. Si vous utilisez un cluster HDInsight 3.3, vous devez également ajouter hello suivant toohello `<dependencies>` section :

        <dependency>
            <groupId>org.apache.phoenix</groupId>
            <artifactId>phoenix-core</artifactId>
            <version>4.4.0-HBase-1.1</version>
        </dependency>

    Cette dépendance chargera hello phoenix-composants, qui sont utilisés par la version de Hbase 1.1.x.
3. Ajouter hello suivant code toohello **pom.xml** fichier. Cette section doit être à l’intérieur de hello `<project>...</project>` balises Bonjour de fichiers, par exemple, entre `</dependencies>` et `</project>`.

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

    Hello `<resources>` section configure une ressource (**conf\hbase-site.XML**) qui contient des informations de configuration pour HBase.

   > [!NOTE]
   > Vous pouvez également définir les valeurs de configuration par code. Consultez les commentaires hello Bonjour **CreateTable** exemple qui suit sur la manière de toodo cela.
   >
   >

    Cela `<plugins>` section configure hello [plug-in du compilateur Maven](http://maven.apache.org/plugins/maven-compiler-plugin/) et [plug-in de la nuance Maven](http://maven.apache.org/plugins/maven-shade-plugin/). compilateur Hello plug-in est utilisé toocompile hello topologie. ombre Hello plug-in est la duplication de licence tooprevent utilisés dans le package JAR hello qui est généré par Maven. Hello utilisé parce que les fichiers de licence en double de hello provoquent une erreur au moment de l’exécution sur le cluster HDInsight de hello. À l’aide de maven-ton plug-in par hello `ApacheLicenseResourceTransformer` implémentation empêche cette erreur.

    Hello maven-ton plug-in génère également une uber jar (ou le jar fat) qui contient toutes les dépendances de hello requis par l’application hello.
4. Enregistrer hello **pom.xml** fichier.
5. Créer un nouveau répertoire nommé **conf** Bonjour **hbaseapp** active. Bonjour **conf** répertoire, créez un fichier nommé **hbase-site.XML**. Utilisez les éléments suivants de hello en tant que contenu hello du fichier de hello :

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

    Ce fichier sera utilisé tooload hello HBase pour un cluster HDInsight.

   > [!NOTE]
   > Il s’agit d’un fichier minimal hbase-site.XML, et il contient des paramètres de configuration minimale bare hello pour le cluster HDInsight de hello.

6. Enregistrer hello **hbase-site.XML** fichier.

## <a name="create-hello-application"></a>Créer l’application hello
1. Accédez toohello **hbaseapp\src\main\java\com\microsoft\examples** active et renommer hello trop app.java fichier**CreateTable.java**.
2. Ouvrez hello **CreateTable.java** de fichier et remplacez contenu hello hello suivant de code :

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

    Il s’agit de hello **CreateTable** (classe), qui crée une table nommée **personnes** et le remplir avec certains utilisateurs prédéfinis.
3. Enregistrer hello **CreateTable.java** fichier.
4. Bonjour **hbaseapp\src\main\java\com\microsoft\examples** répertoire, créez un nouveau fichier nommé **SearchByEmail.java**. Utilisez hello après le code en tant que contenu hello de ce fichier :

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

    Hello **SearchByEmail** classe peut être tooquery utilisé pour les lignes par adresse de messagerie. Car elle utilise un filtre d’expression régulière, vous pouvez fournir une chaîne ou une expression régulière lors de l’utilisation de classe hello.
5. Enregistrer hello **SearchByEmail.java** fichier.
6. Bonjour **hbaseapp\src\main\hava\com\microsoft\examples** répertoire, créez un nouveau fichier nommé **DeleteTable.java**. Utilisez hello après le code en tant que contenu hello de ce fichier :

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

    Cette classe est pour le nettoyage de cet exemple en désactivant et suppression hello table créée par hello **CreateTable** classe.
7. Enregistrer hello **DeleteTable.java** fichier.

## <a name="build-and-package-hello-application"></a>Génération et package d’application de hello
1. Ouvrez une invite de commandes et modifiez les répertoires toohello **hbaseapp** active.
2. Utilisez hello suivant commande toobuild un fichier JAR contenant une application hello :

        mvn clean package

    Cela nettoie les artefacts de build précédente, télécharge les dépendances qui n’ont pas déjà été installés, puis génère et packages d’application hello.
3. Commande hello issue, hello **hbaseapp\target** répertoire contient un fichier nommé **hbaseapp-1.0-SNAPSHOT.jar**.

   > [!NOTE]
   > Hello **hbaseapp-1.0-SNAPSHOT.jar** fichier est un uber jar (parfois appelé fichier jar fat,) qui contient toutes les dépendances de hello requis application hello de toorun.

## <a name="upload-hello-jar-file-and-start-a-job"></a>Télécharger le fichier JAR hello et démarrer un travail
Il existe plusieurs tooupload de façons un tooyour HDInsight de fichiers, comme décrit dans [télécharger des données pour les travaux Hadoop dans HDInsight](hdinsight-upload-data.md). Hello suit utilise Azure PowerShell.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

1. Après avoir installé et configuré Azure PowerShell, créez un fichier appelé **hbase-runner.psm1**. Utilisez les éléments suivants de hello en tant que contenu hello de ce fichier :

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

    Ce fichier contient deux modules :

   * **Ajouter-HDInsightFile** -utilisé tooupload fichiers tooHDInsight
   * **Start-HBaseExample** -classes de hello toorun créés précédemment utilisées
2. Enregistrer hello **hbase-runner.psm1** fichier.
3. Ouvrir une nouvelle fenêtre Azure PowerShell, modifiez les répertoires toohello **hbaseapp** active, et puis hello exécution suivant la commande.

        PS C:\ Import-Module c:\path\to\hbase-runner.psm1

    Modifier hello chemin toohello l’emplacement de hello **hbase-runner.psm1** fichier créé précédemment. Module de hello est inscrit pour cette session Azure PowerShell.
4. Suivant de hello utilisez commande hello de tooupload **hbaseapp-1.0-SNAPSHOT.jar** tooyour HDInsight cluster.

        Add-HDInsightFile -localPath target\hbaseapp-1.0-SNAPSHOT.jar -destinationPath example/jars/hbaseapp-1.0-SNAPSHOT.jar -clusterName hdinsightclustername

    Remplacez **hdinsightclustername** avec nom hello de votre cluster HDInsight. commande Hello télécharge hello **hbaseapp-1.0-SNAPSHOT.jar** toohello **exemple/JAR** emplacement dans le stockage principal hello pour votre cluster HDInsight.
5. Une fois le téléchargement de fichiers de hello, utilisez hello de code suivant toocreate une table à l’aide de hello **hbaseapp**:

        Start-HBaseExample -className com.microsoft.examples.CreateTable -clusterName hdinsightclustername

    Remplacez **hdinsightclustername** avec nom hello de votre cluster HDInsight.

    Cette commande crée une table appelée **people** sur votre cluster HDInsight. Cette commande n’affiche pas de sortie dans la fenêtre de console hello.
6. toosearch pour entrées de table hello, hello utilisez commande suivante :

        Start-HBaseExample -className com.microsoft.examples.SearchByEmail -clusterName hdinsightclustername -emailRegex contoso.com

    Remplacez **hdinsightclustername** avec nom hello de votre cluster HDInsight.

    Cette commande utilise hello **SearchByEmail** classe toosearch pour toutes les lignes où hello **contactinformation** famille de colonne et hello **messagerie** colonne, contient la chaîne de hello **contoso.com**. Vous devez recevoir hello suivant des résultats :

          Franklin Holtz - ID: 2
          Franklin Holtz - franklin@contoso.com - ID: 2
          Rae Schroeder - ID: 4
          Rae Schroeder - rae@contoso.com - ID: 4
          Gabriela Ingram - ID: 6
          Gabriela Ingram - gabriela@contoso.com - ID: 6

    À l’aide de **fabrikam.com** pour hello `-emailRegex` valeur retourne les utilisateurs hello ayant **fabrikam.com** dans le champ d’adresse de messagerie hello. Étant donné que cette recherche est implémentée à l’aide d’un filtre basé sur une expression régulière, vous pouvez également entrer des expressions régulières, tels que **^ r**, les entrées qui retourne où commence l’e-mail de hello avec hello lettre « r ».

## <a name="delete-hello-table"></a>Supprimer une table de hello
Lorsque vous avez terminé avec l’exemple de hello, suivant de hello utilisez commande de hello de hello Azure PowerShell session toodelete **personnes** table utilisée dans cet exemple :

    Start-HBaseExample -className com.microsoft.examples.DeleteTable -clusterName hdinsightclustername

Remplacez **hdinsightclustername** avec nom hello de votre cluster HDInsight.

## <a name="troubleshooting"></a>Résolution des problèmes
### <a name="no-results-or-unexpected-results-when-using-start-hbaseexample"></a>Aucun résultat ou résultat inattendu lors de l'utilisation de Start-HBaseExample
Hello d’utilisation `-showErr` paramètre tooview hello erreur standard (STDERR) qui est généré lors de la tâche de hello en cours d’exécution.
