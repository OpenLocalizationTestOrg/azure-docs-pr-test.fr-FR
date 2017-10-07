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
# <a name="use-a-java-udf-with-hive-in-hdinsight"></a>Utiliser une fonction UDF Java avec Hive dans HDInsight

Découvrez comment toocreate basé sur un Java défini par l’utilisateur (fonction) (UDF) qui fonctionne avec la ruche. Hello Java UDF dans cet exemple convertit un tableau de chaînes tooall-minuscules des caractères de texte.

## <a name="requirements"></a>Configuration requise

* Un cluster HDInsight 

    > [!IMPORTANT]
    > Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

    La plupart des étapes de ce document fonctionnent sur les deux clusters basés sur Windows et Linux. Toutefois, hello étapes utilisées tooupload hello compilée cluster de toohello UDF et exécuter sont des clusters tooLinux spécifiques. Des liens sont fournis tooinformation qui peut être utilisée avec des clusters basés sur Windows.

* [Java JDK](http://www.oracle.com/technetwork/java/javase/downloads/) 8 ou ultérieur (ou un équivalent, par exemple, OpenJDK)

* [Apache Maven](http://maven.apache.org/)

* Un éditeur de texte ou un IDE Java

    > [!IMPORTANT]
    > Si vous créez des fichiers de Python sur un client Windows hello, vous devez utiliser un éditeur qui utilise le saut de ligne comme une fin de ligne. Si vous n’êtes pas sûr que votre éditeur utilise LF ou CRLF, consultez hello [dépannage](#troubleshooting) section pour les étapes de suppression hello caractère de retour chariot.

## <a name="create-an-example-java-udf"></a>Créer un exemple Java UDF 

1. À partir d’une ligne de commande, utilisez hello suivant toocreate un nouveau projet Maven :

    ```bash
    mvn archetype:generate -DgroupId=com.microsoft.examples -DartifactId=ExampleUDF -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

   > [!NOTE]
   > Si vous utilisez PowerShell, vous devez placer entre guillemets les paramètres hello. Par exemple, `mvn archetype:generate "-DgroupId=com.microsoft.examples" "-DartifactId=ExampleUDF" "-DarchetypeArtifactId=maven-archetype-quickstart" "-DinteractiveMode=false"`.

    Cette commande crée un répertoire nommé **exampleudf**, qui contient le projet de Maven hello.

2. Une fois le projet de hello a été créé, supprimez hello **exampleudf/src/test** active a été créée dans le cadre du projet de hello.

3. Ouvrez hello **exampleudf/pom.xml**et remplacer hello `<dependencies>` entrée par hello XML suivant :

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

    Ces entrées spécifient la version de hello de Hadoop et Hive inclus avec HDInsight 3.5. Vous trouverez des informations sur les versions de hello de Hadoop et Hive fourni avec HDInsight à partir de hello [le contrôle de version HDInsight composant](hdinsight-component-versioning.md) document.

    Ajouter un `<build>` section avant hello `</project>` ligne à la fin de hello du fichier de hello. Cette section doit contenir hello XML suivant :

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

    Ces entrées définissent comment toobuild hello projet. Plus précisément, les version hello de Java qui hello projet utilise et comment toobuild un uberjar pour cluster toohello de déploiement.

    Enregistrer le fichier de hello une fois hello modifications ont été apportées.

4. Renommer **exampleudf/src/main/java/com/microsoft/examples/App.java** trop**ExampleUDF.java**, puis ouvrez le fichier de hello dans votre éditeur.

5. Remplacez le contenu hello Hello **ExampleUDF.java** de fichiers avec les éléments suivants de hello, puis enregistrez le fichier de hello.

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

    Ce code implémente une fonction qui accepte une valeur de chaîne et retourne une version en minuscules d’hello.

## <a name="build-and-install-hello-udf"></a>Générer et installer hello UDF

1. Utilisez hello suivant commande toocompile et hello UDF de package :

    ```bash
    mvn compile package
    ```

    Cette commande génère et packages hello UDF dans hello `exampleudf/target/ExampleUDF-1.0-SNAPSHOT.jar` fichier.

2. Hello d’utilisation `scp` commande toocopy hello toohello HDInsight de fichiers.

    ```bash
    scp ./target/ExampleUDF-1.0-SNAPSHOT.jar myuser@mycluster-ssh.azurehdinsight
    ```

    Remplacez `myuser` par hello compte d’utilisateur SSH pour votre cluster. Remplacez `mycluster` avec le nom du cluster hello. Si vous avez utilisé un Bonjour toosecure de mot de passe SSH compte, vous êtes un mot de passe hello tooenter demandées. Si vous avez utilisé un certificat, vous devrez peut-être toouse hello `-i` fichier clé privée de paramètre toospecify hello.

3. Connectez le cluster toohello à l’aide de SSH.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

    Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).

4. À partir de la session SSH hello, copiez tooHDInsight stockage hello jar.

    ```bash
    hdfs dfs -put ExampleUDF-1.0-SNAPSHOT.jar /example/jars
    ```

## <a name="use-hello-udf-from-hive"></a>Utilisez hello UDF à partir de la ruche

1. Utilisez hello suivant du client de Beeline hello toostart à partir de la session SSH hello.

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    Cette commande suppose que vous avez utilisé par défaut hello **admin** hello compte de connexion pour votre cluster.

2. Une fois que vous êtes parvenu à hello `jdbc:hive2://localhost:10001/>` invite, entrez hello suivant tooadd hello UDF tooHive et l’exposer en tant que fonction.

    ```hiveql
    ADD JAR wasb:///example/jars/ExampleUDF-1.0-SNAPSHOT.jar;
    CREATE TEMPORARY FUNCTION tolower as 'com.microsoft.examples.ExampleUDF';
    ```

    > [!NOTE]
    > Cet exemple suppose que le stockage Azure est le stockage par défaut pour le cluster de hello. Si votre cluster utilise Data Lake Store au lieu de cela, modifiez hello `wasb:///` valeur trop`adl:///`.

3. Utilisez hello UDF tooconvert valeurs récupérées à partir d’une table toolower casse des chaînes.

    ```hiveql
    SELECT tolower(deviceplatform) FROM hivesampletable LIMIT 10;
    ```

    Cette requête sélectionne hello plateforme d’appareil (Android, Windows, iOS, etc.) à partir de la table de hello, convertir en cas de toolower chaîne hello, puis les afficher. sortie de Hello apparaît toohello similaire après le texte :

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

## <a name="next-steps"></a>Étapes suivantes

Pour les autres toowork manières avec Hive, consultez [utilisez Hive hdinsight](hdinsight-use-hive.md).

Pour plus d’informations sur les fonctions de Hive User-Defined, consultez [Hive les opérateurs et les fonctions définies par l’utilisateur](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) section de wiki de ruche hello sur le site apache.org.
