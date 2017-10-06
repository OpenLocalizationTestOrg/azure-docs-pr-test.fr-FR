---
title: "données aaaSerialize dans Hadoop - Microsoft Avro Library - Azure | Documents Microsoft"
description: "Découvrez comment tooserialize et désérialiser des données dans Hadoop dans HDInsight à l’aide de hello Microsoft Avro Library toopersist toomemory, d’une base de données ou d’un fichier."
keywords: avro,hadoop avro
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: c78dc20d-5d8d-4366-94ac-abbe89aaac58
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jgao
ms.custom: hdiseo17may2017
ms.openlocfilehash: f364f8e855a54c0fc160e9a106ec8d5b30c6db23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="serialize-data-in-hadoop-with-hello-microsoft-avro-library"></a>Sérialisation des données dans Hadoop avec hello Microsoft Avro Library

>[!NOTE]
>Hello Avro SDK n’est plus pris en charge par Microsoft. bibliothèque de Hello est la Communauté open source pris en charge. sources de Hello pour la bibliothèque de hello se trouvent dans [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).

Cette rubrique montre comment toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize objets et autres données structures dans le flux de données toopersist les toomemory, une base de données ou un fichier. Il montre également comment toodeserialize les objets d’origine de toorecover hello.

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a>Apache Avro
Hello <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implémente hello système de sérialisation des données Apache Avro pour l’environnement de Microsoft.NET hello. Apache Avro fournit un format compact d'échange des données binaires pour la sérialisation. Il utilise <a href="http://www.json.org" target="_blank">JSON</a> toodefine un schéma indépendant du langage qui couvre l’interopérabilité des langages. Les données sérialisées dans un langage peuvent être lues dans un autre langage. Les langages C, C++, C#, Java, PHP, Python et Ruby sont actuellement pris en charge. Vous trouverez des informations détaillées sur le format de hello Bonjour <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro spécification</a>. 

>[!NOTE]
>Hello Microsoft Avro Library ne prend pas en charge hello procédure distante (RPC) les appels partie de cette spécification.
>

représentation sous forme de Hello sérialisée d’un objet Bonjour Avro système se compose de deux parties : schéma et la valeur réelle. schéma de Avro Hello décrit le modèle de données indépendant du langage hello de données hello sérialisé avec JSON. Il est présenté côte à côte avec une représentation binaire des données. Permet à chaque toobe objet écrit avec aucun frais généraux par valeur, effectuer sérialisation rapide et hello représentation sous forme de petits ayant schéma hello distinct à partir de la représentation binaire de hello.

## <a name="hello-hadoop-scenario"></a>scénario de Hadoop Hello
format de sérialisation Apache Avro Hello est largement utilisé dans Azure HDInsight et d’autres environnements d’Apache Hadoop. Avro fournit un moyen pratique de toorepresent des structures de données complexes au sein d’un travail Hadoop MapReduce. format Hello Avro fichiers (fichier conteneur d’objet Avro) a été modèle de programmation conçu toosupport hello distribué MapReduce. fonctionnalité de clé Hello qui permet la distribution de hello est les fichiers hello « divisible » dans les sens hello qu’un qui peut rechercher n’importe quel point dans un fichier et commence à lire à partir d’un bloc particulier.

## <a name="serialization-in-avro-library"></a>Sérialisation dans Avro Library
Hello bibliothèque .NET pour Avro prend en charge deux méthodes de sérialisation d’objets :

* **réflexion** -schéma JSON hello pour les types de hello est généré automatiquement à partir des données de hello attributs de contrat de toobe de types .NET hello sérialisé.
* **enregistrement générique** -JSON d’un schéma est explicitement spécifié dans un enregistrement représenté par hello [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) classe lorsque aucun des types .NET ne sont présent schéma toodescribe hello hello données toobe sérialisé.

Lorsque le schéma de données hello est connu writer de hello tooboth et lecteur de flux de hello, les données de salutation peuvent être envoyées sans son schéma. Dans le cas lorsqu’un fichier conteneur d’objet Avro est utilisé, schéma de hello est stocké dans le fichier de hello. Autres paramètres, tels que codec hello utilisé pour la compression de données, peuvent être spécifiés. Ces scénarios sont décrites plus en détail et notamment hello, exemple de code suivant :

## <a name="install-avro-library"></a>Installation d’Avro Library
Hello Voici requis avant d’installer la bibliothèque de hello :

* <a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a>
* <a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (version 6.0.4 ou ultérieure)

Notez que hello Newtonsoft.Json.dll dépendance est automatiquement téléchargé avec installation hello Hello Microsoft Avro Library. procédure de Hello est fourni dans hello suivant la section :

Hello Microsoft Avro Library est distribuée comme package NuGet qui peut être installé à partir de Visual Studio via hello procédure :

1. Sélectionnez hello **projet** onglet -> **gérer les Packages NuGet...**
2. Recherchez « Microsoft.Hadoop.Avro » Bonjour **recherche en ligne** boîte.
3. Cliquez sur hello **installer** bouton ensuite trop**Microsoft Azure HDInsight Avro Library**.

Notez que hello Newtonsoft.Json.dll (> = 6.0.4) dépendance est également téléchargée automatiquement avec hello Microsoft Avro Library.

Hello code source Microsoft Avro Library est disponible à l’adresse [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).

## <a name="compile-schemas-using-avro-library"></a>Compiler des schémas à l'aide d’Avro Library
Hello Microsoft Avro Library contient une génération de code qui permet de créer des types c# automatiquement en fonction de hello précédemment défini un schéma JSON. utilitaire de génération de code Hello n’est pas distribuée sous forme binaire exécutable, mais peut être facilement créé via hello procédure :

1. Télécharger le fichier .zip de hello avec la version la plus récente du code source de HDInsight SDK à partir de hello <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK pour Hadoop</a>. (Cliquez sur hello **télécharger** icône, pas hello **télécharge** onglet.)
2. Extrayez hello répertoire tooa HDInsight SDK machine hello avec .NET Framework 4 installé et connecté toohello Internet pour télécharger les packages NuGet dépendance nécessaire. Ci-dessous, nous partons du principe que le code source de hello est tooC:\SDK extraits.
3. Atteindre le dossier toohello C:\SDK\src\Microsoft.Hadoop.Avro.Tools et exécutez build.bat. (hello appels de fichier MSBuild à partir de la distribution de 32 bits hello Hello .NET Framework. Si vous souhaitez que la version 64 bits de hello toouse, modifiez build.bat, suivant les commentaires hello à l’intérieur du fichier de hello.) Assurez-vous que la build de hello a réussi. (Sur certains systèmes, MSBuild peut générer des avertissements. Ces avertissements n’affectent pas les utilitaire hello tant qu’il n’y a aucune erreur de build.)
4. utilitaire de Hello compilé se trouve dans C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.

tooget familiarisé avec la syntaxe de ligne de commande hello, exécutez hello de commande suivante à partir du dossier hello où l’utilitaire de génération de code hello se trouve :`Microsoft.Hadoop.Avro.Tools help /c:codegen`

utilitaire de hello tootest, vous pouvez générer des classes c# à partir du fichier de schéma JSON exemple hello fourni avec le code source de hello. Exécutez hello de commande suivante :

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

Il est supposé tooproduce deux fichiers c# dans le répertoire en cours de hello : SensorData.cs et Location.cs.

logique de hello toounderstand utilitaire de génération de code hello est à l’aide lors de la conversion de types tooC # hello JSON schéma, consultez hello fichier GenerationVerification.feature dans C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.

Espaces de noms sont extraites à partir d’un schéma JSON hello, à l’aide de la logique de hello décrite dans le fichier hello mentionné dans le paragraphe précédent hello. Espaces de noms extraites hello schéma ont priorité sur tout ce qui est fourni avec le paramètre /n hello dans la ligne de commande d’utilitaire hello. Si vous souhaitez que les espaces de noms toooverride hello dans un schéma hello, utilisez le paramètre de /nf hello. Par exemple, toochange exécuter tous les espaces de noms hello SampleJSONSchema.avsc toomy.own.nspace, hello la commande suivante :

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-hello-samples"></a>À propos des exemples de hello
Six exemples fournis dans cette rubrique illustrent différents scénarios pris en charge par hello Microsoft Avro Library. Hello Microsoft Avro Library est conçue toowork avec n’importe quel flux de données. Dans ces exemples, les données sont manipulées à l’aide de flux de mémoire plutôt que de flux de fichiers ou de bases de données pour des questions de simplicité et de cohérence. approche Hello effectuée dans un environnement de production dépend des exigences de scénario hello, source de données et de volume, les contraintes de performances et d’autres facteurs.

Hello premier deux exemples indiquent comment tooserialize et désérialiser les données en mémoire tampon de flux de données à l’aide de la réflexion et enregistrements génériques. Hello dans ces deux cas est supposé que le schéma toobe partagée entre hello lecteurs et writers hors-bande.

afficher des exemples de troisième et quatrième Hello comment tooserialize et désérialiser des données à l’aide de fichiers de conteneur objet hello Avro. Lorsque les données stockées dans un fichier de conteneur Avro, son schéma est toujours stockée avec lui, car le schéma de hello doit être partagé pour la désérialisation.

Hello contenant par exemple hello quatre premiers exemples peuvent être téléchargés à partir de hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">exemples de code Azure</a> site.

Hello cinquième exemple montre comment toouse un codec de compression personnalisé pour Avro les fichiers de conteneur d’objets. Un exemple contenant du code de hello pour cet exemple peut être téléchargé à partir de hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">exemples de code Azure</a> site.

Hello sixième montre comment toouse Avro sérialisation tooupload données tooAzure stockage d’objets Blob et puis les analyser à l’aide de la ruche avec un cluster HDInsight (Hadoop). Il peut être téléchargé à partir de hello <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">exemples de code Azure</a> site.

Voici des liens toohello six échantillons présentés dans la rubrique de hello :

* <a href="#Scenario1">**Sérialisation avec réflexion** </a> -toobe types sérialisé sur le schéma JSON hello est généré automatiquement à partir des données de hello attributs de contrat.
* <a href="#Scenario2">**Sérialisation avec enregistrement générique** </a> -hello JSON schéma est explicitement spécifié dans un enregistrement lorsqu’aucun type .NET n’est disponible pour la réflexion.
* <a href="#Scenario3">**Sérialisation à l’aide des fichiers de conteneur d’objets avec la réflexion** </a> -hello JSON schéma est automatiquement créé et partagé avec des données via un fichier conteneur d’objet Avro hello sérialisé.
* <a href="#Scenario4">**Sérialisation à l’aide des fichiers de conteneur d’objets avec enregistrement générique** </a> -schéma JSON hello est explicitement spécifié avant la sérialisation de hello et partagé avec des données via un fichier conteneur d’objet Avro hello.
* <a href="#Scenario5">**Sérialisation à l’aide des fichiers de conteneur d’objets avec un codec de compression personnalisé** </a> -hello montre comment toocreate un Avro de l’objet fichier conteneur avec une implémentation .NET personnalisé du codec de compression de données hello Deflate.
* <a href="#Scenario6">**À l’aide des données de tooupload Avro pourquoi le service Microsoft Azure HDInsight** </a> -hello illustre comment Avro sérialisation interagit avec hello service HDInsight. Un active Azure abonnement et accès tooan Azure HDInsight de cluster requis toorun cet exemple.

## <a name="Scenario1"></a>Exemple 1 : sérialisation avec réflexion
schéma JSON Hello pour les types de hello peut être automatiquement créé par hello Microsoft Avro Library via la réflexion à partir des données de hello attributs de contrat de toobe hello c# objets sérialisés. Hello Microsoft Avro Library crée un [ **IAvroSeralizer<T>**  ](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify hello champs toobe sérialisé.

Dans cet exemple, objets (un **SensorData** classe avec un membre **emplacement** struct) sont des flux de mémoire tooa sérialisé, et ce flux est ensuite désérialisé. Hello résultat est ensuite comparé toohello initiale d’instance tooconfirm que hello **SensorData** objet récupéré est identique toohello d’origine.

schéma Hello dans cet exemple est supposé toobe partagée entre hello lecteurs et writers, le format de conteneur objet hello Avro n’est pas requis. Pour obtenir un exemple de procédure tooserialize et désérialiser des données dans les mémoires tampons en utilisant la réflexion avec le format de conteneur d’objet hello lorsque le schéma de hello doit être partagé avec les données de salutation, consultez <a href="#Scenario3">sérialisation à l’aide des fichiers de conteneur d’objets avec la réflexion</a>.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serialize and deserialize sample data set represented as an object using reflection.
            //No explicit schema definition is required - schema of serialized objects is automatically built.
            public void SerializeDeserializeObjectUsingReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION\n");
                Console.WriteLine("Serializing Sample Data Set...");

                //Create a new AvroSerializer instance and specify a custom serialization strategy AvroDataContractResolver
                //for serializing only properties attributed with DataContract/DateMember
                var avroSerializer = AvroSerializer.Create<SensorData>();

                //Create a memory stream buffer
                using (var buffer = new MemoryStream())
                {
                    //Create a data set by using sample class and struct
                    var expected = new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } };

                    //Serialize hello data toohello specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from hello stream and cast it toohello same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches hello original one
                    bool isEqual = this.Equal(expected, actual);

                    Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);

                }
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }



            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization toomemory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-2-serialization-with-a-generic-record"></a>Exemple 2 : sérialisation avec enregistrement générique
Un schéma JSON peut être explicitement spécifié dans un enregistrement générique quand la réflexion ne peut pas être utilisée, car il est impossible de représenter les données de salutation via les classes .NET avec un contrat de données. Cette méthode est plus lente que celle qui utilise la réflexion. Dans ce cas, schéma hello pour les données de salutation peut également être dynamique, autrement dit, ne pas connu au moment de la compilation. Données représentées en tant que valeurs séparées par des virgules (CSV) des fichiers dont le schéma est inconnu jusqu'à ce qu’il est transformé le format Avro toohello au moment de l’exécution est un exemple de ce type de scénario dynamique.

Cet exemple montre comment toocreate et utiliser une [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly spécifier un schéma JSON, comment toopopulate avec hello et comment puis tooserialize et de le désérialiser. résultat de Hello est ensuite comparé toohello initiale d’instance tooconfirm qui hello enregistrement récupéré est identique toohello d’origine.

schéma Hello dans cet exemple est supposé toobe partagée entre hello lecteurs et writers, le format de conteneur objet hello Avro n’est pas requis. Pour obtenir un exemple de procédure tooserialize et désérialiser des données dans les mémoires tampons à l’aide d’un enregistrement générique avec le format de conteneur d’objet hello lorsque le schéma de hello doit être incluse avec les données sérialisée de hello, consultez hello <a href="#Scenario4">sérialisation à l’aide du conteneur d’objets fichiers avec enregistrement générique</a> exemple.

    namespace Microsoft.Hadoop.Avro.Sample
    {
    using System;
    using System.Collections.Generic;
    using System.IO;
    using System.Linq;
    using System.Runtime.Serialization;
    using Microsoft.Hadoop.Avro.Container;
    using Microsoft.Hadoop.Avro.Schema;
    using Microsoft.Hadoop.Avro;

    //This class contains all methods demonstrating
    //hello usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with hello schema explicitly defined in JSON.
        //All serialized data should be mapped toohello fields of hello generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

            //Define hello schema in JSON
            const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

            //Create a generic serializer based on hello schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record toorepresent hello data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize hello data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize hello data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify hello results
                bool isEqual = expected.Location.Floor.Equals(actual.Location.Floor);
                isEqual = isEqual && expected.Location.Room.Equals(actual.Location.Room);
                isEqual = isEqual && ((byte[])expected.Value).SequenceEqual((byte[])actual.Value);
                Console.WriteLine("Result of Data Set Identity Comparison is {0}", isEqual);
            }
        }

        static void Main()
        {

            string sectionDivider = "---------------------------------------- ";

            //Create an instance of AvroSample class and invoke methods
            //illustrating different serializing approaches
            AvroSample Sample = new AvroSample();

            //Serialization toomemory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key tooexit.");
            Console.Read();
        }
    }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a>Exemple 3 : sérialisation à l'aide de fichiers conteneurs d'objets et sérialisation avec réflexion
Cet exemple est un scénario toohello similaire Bonjour <a href="#Scenario1"> premier exemple</a>, où les schémas hello sont implicitement spécifié avec la réflexion. Hello différence est qu’ici, schéma de hello n’est pas supposé que toobe connu du lecteur toohello qui désérialise ce paquet. Hello **SensorData** toobe d’objets sérialisés et leur schéma spécifié de manière implicite sont stockées dans un fichier conteneur d’objet Avro représenté par hello [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) classe.

les données de salutation sont sérialisées dans cet exemple par [ **SequentialWriter<SensorData>**  ](http://msdn.microsoft.com/library/dn627340.aspx) et désérialisés avec [ **SequentialReader<SensorData>** ](http://msdn.microsoft.com/library/dn627340.aspx). résultat de Hello est puis toohello comparés initial d’instances tooensure identité.

Bonjour Bonjour d’objet de données du fichier conteneur est compressé par défaut de hello [ **Deflate** ] [ deflate-100] codec de compression à partir de .NET Framework 4. Consultez hello <a href="#Scenario5"> cinquième exemple</a> dans cette rubrique toolearn comment toouse une version plus récente et supérieure de hello [ **Deflate** ] [ deflate-110] compression codec disponible dans .NET Framework 4.5.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes hello sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello Deflate codec.
            public void SerializeDeserializeUsingObjectContainersReflection()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is compressed using hello Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            bool isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual);
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a>Exemple 4 : sérialisation à l'aide de fichiers conteneurs d'objets et sérialisation avec enregistrement générique
Cet exemple est un scénario toohello similaire Bonjour <a href="#Scenario2"> deuxième exemple</a>, où les schémas hello sont spécifié explicitement avec JSON. Hello différence est qu’ici, schéma de hello n’est pas supposé que toobe connu du lecteur toohello qui désérialise ce paquet.

jeu de données de test Hello sont collecté dans une liste de [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objets via le schéma défini explicitement JSON et stockées dans un fichier conteneur d’objet représenté par hello [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) classe. Ce fichier conteneur crée un writer qui est des données hello tooserialize utilisés, non compressées, flux de mémoire tooa qui est ensuite enregistrée tooa fichier. Hello [ **Codec.Null** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) paramètre utilisé pour la création du lecteur de hello Spécifie que ces données ne sont pas compressées.

les données de salutation sont ensuite lire hello du fichier et désérialisées dans une collection d’objets. Cette collection est comparé toohello la liste initiale de tooconfirm d’enregistrements Avro qu’ils sont identiques.

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.IO;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro.Schema;
        using Microsoft.Hadoop.Avro;

        //This class contains all methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining hello Schema and creating Sample Data Set...");

                //Define hello schema in JSON
                const string Schema = @"{
                                ""type"":""record"",
                                ""name"":""Microsoft.Hadoop.Avro.Specifications.SensorData"",
                                ""fields"":
                                    [
                                        {
                                            ""name"":""Location"",
                                            ""type"":
                                                {
                                                    ""type"":""record"",
                                                    ""name"":""Microsoft.Hadoop.Avro.Specifications.Location"",
                                                    ""fields"":
                                                        [
                                                            { ""name"":""Floor"", ""type"":""int"" },
                                                            { ""name"":""Room"", ""type"":""int"" }
                                                        ]
                                                }
                                        },
                                        { ""name"":""Value"", ""type"":""bytes"" }
                                    ]
                            }";

                //Create a generic serializer based on hello schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record toorepresent hello data
                var testData = new List<AvroRecord>();

                dynamic expected1 = new AvroRecord(rootSchema);
                dynamic location1 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location1.Floor = 1;
                location1.Room = 243;
                expected1.Location = location1;
                expected1.Value = new byte[] { 1, 2, 3, 4, 5 };
                testData.Add(expected1);

                dynamic expected2 = new AvroRecord(rootSchema);
                dynamic location2 = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location2.Floor = 1;
                location2.Room = 244;
                expected2.Location = location2;
                expected2.Value = new byte[] { 6, 7, 8, 9 };
                testData.Add(expected2);

                //Serializing and saving data toofile.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize hello data toostream by using hello sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data toofile...");

                    //Save stream toofile
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing hello data.
                //Create a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify hello results
                            var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = (dynamic)serialized, actual = (dynamic)deserialized });
                            int count = 1;
                            foreach (var pair in pairs)
                            {
                                bool isEqual = pair.expected.Location.Floor.Equals(pair.actual.Location.Floor);
                                isEqual = isEqual && pair.expected.Location.Room.Equals(pair.actual.Location.Room);
                                isEqual = isEqual && ((byte[])pair.expected.Value).SequenceEqual((byte[])pair.actual.Value);
                                Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                                count++;
                            }
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading a file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using hello given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of hello AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record tooAvro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining hello Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a>Exemple 5: sérialisation à l'aide de fichiers conteneurs d'objets avec un codec de compression personnalisé
Hello cinquième exemple montre comment toouse un codec de compression personnalisé pour Avro les fichiers de conteneur d’objets. Un exemple contenant du code de hello pour cet exemple peut être téléchargé à partir de hello [exemples de code Azure](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.

Hello [Avro spécification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) permet l’utilisation d’un codec de compression facultatif (en outre trop**Null** et **Deflate** par défaut). Cet exemple n’implémente pas un nouveau codec telles que Snappy (indiqué en tant qu’un codec facultatif pris en charge dans hello [Avro spécification](http://avro.apache.org/docs/current/spec.html#snappy)). Il montre comment toouse hello implémentation .NET Framework 4.5 de hello [ **Deflate** ] [ deflate-110] codec, qui offre un meilleur algorithme de compression en fonction de hello [zlib](http://zlib.net/) bibliothèque de compression à la version de .NET Framework 4 hello par défaut.

    //
    // This code needs toobe compiled with hello parameter Target Framework set as ".NET Framework 4.5"
    // tooensure hello desired implementation of hello Deflate compression algorithm is used.
    // Ensure your C# project is set up accordingly.
    //

    namespace Microsoft.Hadoop.Avro.Sample
    {
        using System;
        using System.Collections.Generic;
        using System.Diagnostics;
        using System.IO;
        using System.IO.Compression;
        using System.Linq;
        using System.Runtime.Serialization;
        using Microsoft.Hadoop.Avro.Container;
        using Microsoft.Hadoop.Avro;

        #region Defining objects for serialization
        //Sample class used in serialization samples
        [DataContract(Name = "SensorDataValue", Namespace = "Sensors")]
        internal class SensorData
        {
            [DataMember(Name = "Location")]
            public Location Position { get; set; }

            [DataMember(Name = "Value")]
            public byte[] Value { get; set; }
        }

        //Sample struct used in serialization samples
        [DataContract]
        internal struct Location
        {
            [DataMember]
            public int Floor { get; set; }

            [DataMember]
            public int Room { get; set; }
        }
        #endregion

        #region Defining custom codec based on .NET Framework V.4.5 Deflate
        //Avro.NET codec class contains two methods,
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed),
        //which are hello key ones for data compression.
        //tooenable a custom codec, one needs tooimplement these methods for hello required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs tooimplement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed toobe null.");

                this.compressionStream = new DeflateStream(buffer, CompressionLevel.Fastest, true);
                this.buffer = buffer;
            }

            public override bool CanRead
            {
                get { return this.buffer.CanRead; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return this.buffer.CanWrite; }
            }

            public override void Flush()
            {
                this.compressionStream.Close();
            }

            public override long Length
            {
                get { return this.buffer.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.buffer.Position;
                }

                set
                {
                    this.buffer.Position = value;
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.buffer.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                return this.buffer.Seek(offset, origin);
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                this.compressionStream.Write(buffer, offset, count);
            }

            protected override void Dispose(bool disposed)
            {
                base.Dispose(disposed);

                if (disposed)
                {
                    this.compressionStream.Dispose();
                    this.compressionStream = null;
                }
            }
        }

        internal sealed class DecompressionStreamDeflate45 : Stream
        {
            private readonly DeflateStream decompressed;

            public DecompressionStreamDeflate45(Stream compressed)
            {
                this.decompressed = new DeflateStream(compressed, CompressionMode.Decompress, true);
            }

            public override bool CanRead
            {
                get { return true; }
            }

            public override bool CanSeek
            {
                get { return true; }
            }

            public override bool CanWrite
            {
                get { return false; }
            }

            public override void Flush()
            {
                this.decompressed.Close();
            }

            public override long Length
            {
                get { return this.decompressed.Length; }
            }

            public override long Position
            {
                get
                {
                    return this.decompressed.Position;
                }

                set
                {
                    throw new NotSupportedException();
                }
            }

            public override int Read(byte[] buffer, int offset, int count)
            {
                return this.decompressed.Read(buffer, offset, count);
            }

            public override long Seek(long offset, SeekOrigin origin)
            {
                throw new NotSupportedException();
            }

            public override void SetLength(long value)
            {
                throw new NotSupportedException();
            }

            public override void Write(byte[] buffer, int offset, int count)
            {
                throw new NotSupportedException();
            }

            protected override void Dispose(bool disposing)
            {
                base.Dispose(disposing);

                if (disposing)
                {
                    this.decompressed.Dispose();
                }
            }
        }
        #endregion

        #region Define Codec
        //Define hello actual codec class containing hello required methods for manipulating streams:
        //GetCompressedStreamOver(Stream uncompressed) and GetDecompressedStreamOver(Stream compressed).
        //Codec class uses classes for compressed and decompressed streams defined above.
        internal sealed class DeflateCodec45 : Codec
        {

            //We merely use different IMPLEMENTATIONS of Deflate, so CodecName remains "deflate"
            public static readonly string CodecName = "deflate";

            public DeflateCodec45()
                : base(CodecName)
            {
            }

            public override Stream GetCompressedStreamOver(Stream decompressed)
            {
                if (decompressed == null)
                {
                    throw new ArgumentNullException("decompressed");
                }

                return new CompressionStreamDeflate45(decompressed);
            }

            public override Stream GetDecompressedStreamOver(Stream compressed)
            {
                if (compressed == null)
                {
                    throw new ArgumentNullException("compressed");
                }

                return new DecompressionStreamDeflate45(compressed);
            }
        }
        #endregion

        #region Define modified Codec Factory
        //Define modified codec factory toobe used in hello reader.
        //It catches hello attempt toouse "Deflate" and provide  a custom codec.
        //For all other cases, it relies on hello base class (CodecFactory).
        internal sealed class CodecFactoryDeflate45 : CodecFactory
        {

            public override Codec Create(string codecName)
            {
                if (codecName == DeflateCodec45.CodecName)
                    return new DeflateCodec45();
                else
                    return base.Create(codecName);
            }
        }
        #endregion

        #endregion

        #region Sample Class with demonstration methods
        //This class contains methods demonstrating
        //hello usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with hello custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related tooserialization, deserialization and
            //object container manipulation, though file stream could be easily used.
            public void SerializeDeserializeUsingObjectContainersReflectionCustomCodec()
            {

                Console.WriteLine("SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC\n");

                //Path for Avro object container file
                string path = "AvroSampleReflectionDeflate45.avro";

                //Create a data set by using sample class and struct
                var testData = new List<SensorData>
                        {
                            new SensorData { Value = new byte[] { 1, 2, 3, 4, 5 }, Position = new Location { Room = 243, Floor = 1 } },
                            new SensorData { Value = new byte[] { 6, 7, 8, 9 }, Position = new Location { Room = 244, Floor = 1 } }
                        };

                //Serializing and saving data toofile.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects toostream.
                    //Here hello custom codec is introduced. For convenience, hello next commented code line shows how toouse built-in Deflate.
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize hello data toostream using hello sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream toofile
                    Console.WriteLine("Saving serialized data toofile...");
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing data.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Reading data from file...");

                    //Reading data from object container file
                    if (!ReadFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }

                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare hello stream for deserializing hello data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment hello line below if you want toouse built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from hello given stream.
                    //It allows iterating over hello deserialized objects because it implements hello IEnumerable<T> interface.
                    //Here hello custom codec factory is introduced.
                    //For convenience, hello next commented code line shows how toouse built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because hello sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches hello original one
                        Console.WriteLine("Comparing Initial and Deserialized Data Sets...");
                        bool isEqual;
                        int count = 1;
                        var pairs = testData.Zip(results, (serialized, deserialized) => new { expected = serialized, actual = deserialized });
                        foreach (var pair in pairs)
                        {
                            isEqual = this.Equal(pair.expected, pair.actual);
                            Console.WriteLine("For Pair {0} result of Data Set Identity Comparison is {1}", count, isEqual.ToString());
                            count++;
                        }
                    }
                }

                //Delete hello file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream tooa new file with hello given path
            private bool WriteFile(MemoryStream InputStream, string path)
            {
                if (!File.Exists(path))
                {
                    try
                    {
                        using (FileStream fs = File.Create(path))
                        {
                            InputStream.Seek(0, SeekOrigin.Begin);
                            InputStream.CopyTo(fs);
                        }
                        return true;
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during creation and writing toohello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                        return false;
                    }
                }
                else
                {
                    Console.WriteLine("Can not create file \"{0}\". File already exists", path);
                    return false;

                }
            }

            //Reading file content by using hello given path tooa memory stream
            private bool ReadFile(MemoryStream OutputStream, string path)
            {
                try
                {
                    using (FileStream fs = File.Open(path, FileMode.Open))
                    {
                        fs.CopyTo(OutputStream);
                    }
                    return true;
                }
                catch (Exception e)
                {
                    Console.WriteLine("hello following exception was thrown during reading from hello file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using given path
            private void RemoveFile(string path)
            {
                if (File.Exists(path))
                {
                    try
                    {
                        File.Delete(path);
                    }
                    catch (Exception e)
                    {
                        Console.WriteLine("hello following exception was thrown during deleting hello file \"{0}\"", path);
                        Console.WriteLine(e.Message);
                    }
                }
                else
                {
                    Console.WriteLine("Can not delete file \"{0}\". File does not exist", path);
                }
            }
            #endregion

            static void Main()
            {

                string sectionDivider = "---------------------------------------- ";

                //Create an instance of AvroSample Class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using reflection tooAvro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key tooexit.");
                Console.Read();
            }
        }
    }
    // hello example is expected toodisplay hello following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data toofile...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key tooexit.

## <a name="sample-6-using-avro-tooupload-data-for-hello-microsoft-azure-hdinsight-service"></a>Exemple 6 : À l’aide de données de tooupload Avro pourquoi le service Microsoft Azure HDInsight
Hello sixième illustre certaines toointeracting de programmation techniques associées avec le service Azure HDInsight de hello. Un exemple contenant du code de hello pour cet exemple peut être téléchargé à partir de hello [exemples de code Azure](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.

exemple Hello hello tâche suivantes :

* Se connecte tooan cluster du service HDInsight existant.
* Sérialise plusieurs fichiers CSV et télécharge le stockage d’objets Blob tooAzure hello résultat. (fichiers CSV de hello sont distribuées avec l’exemple hello et représentent un extrait des données historiques de Stock de l’American Express distribués par [Infochimps](http://www.infochimps.com/) pendant hello 1970-2010. exemple Hello lit les données de fichier CSV, convertit hello tooinstances des enregistrements de hello **Stock** de classe et les sérialise ensuite en utilisant la réflexion. Définition du type de stock est créée à partir d’un schéma JSON via hello utilitaire de génération de code Microsoft Avro Library.
* Crée une table externe appelée **Stocks** dans la ruche et lie les données toohello téléchargé à l’étape précédente de hello.
* Exécute une requête à l’aide de la ruche sur hello **Stocks** table.

En outre, exemple hello effectue une procédure de nettoyage avant et après avoir effectué les opérations principales. Au cours de hello nettoyage, toutes hello liées dossiers et objets Blob Azure sont supprimés et hello ruche table est supprimée. Vous pouvez également appeler la procédure de nettoyage hello à partir de la ligne de commande exemple hello.

exemple Hello a hello suivant des conditions préalables :

* Un abonnement Microsoft Azure actif et son ID d’abonnement.
* Un certificat de gestion pour l’abonnement hello avec la clé privée correspondante de hello. certificat de Hello doit être installé dans hello actuel utilisateur stockage privé sur toorun hello exemple hello machine utilisée.
* Un cluster HDInsight actif.
* Un compte Azure Storage lié de cluster HDInsight de toohello à partir de la condition préalable précédente hello, ainsi que de la clé d’accès primaire ou secondaire correspondante hello.

Toutes les informations de hello à la configuration requise de hello doivent être entré toohello exemple de fichier de configuration avant l’exécution d’exemple hello. Il existe deux façons possibles toodo il :

* Modifier le fichier app.config de hello dans le répertoire racine de l’exemple hello et générer des exemple hello
* Tout d’abord créer exemple hello et modifiez AvroHDISample.exe.config dans le répertoire de build hello

Dans les deux cas, toutes les modifications doivent être effectuées dans hello  **<appSettings>**  section de paramètres. Suivez les commentaires du fichier hello hello.
Hello exemple est exécuté à partir de la ligne de commande hello en exécutant la commande suivante (où hello fichier .zip avec l’exemple hello a été considérée comme toobe extrait tooC:\AvroHDISample ; si dans le cas contraire, utilisez hello pertinentes du fichier chemin d’accès) de hello :

    AvroHDISample run C:\AvroHDISample\Data

tooclean cluster hello, exécutez hello de commande suivante :

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
