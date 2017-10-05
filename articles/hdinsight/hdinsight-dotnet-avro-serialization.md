---
title: "Sérialisation des données dans Hadoop - Microsoft Avro Library - Azure | Microsoft Docs"
description: "Découvrez comment sérialiser et désérialiser des données dans Hadoop sur HDInsight à l’aide de Microsoft Avro Library pour les conserver dans une mémoire, une base de données ou un fichier."
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
ms.openlocfilehash: d06bf8ff4a21e4f4b29593bac32bfa2b32601fc4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="serialize-data-in-hadoop-with-the-microsoft-avro-library"></a><span data-ttu-id="12357-104">Sérialisation des données dans Hadoop avec Microsoft Avro Library</span><span class="sxs-lookup"><span data-stu-id="12357-104">Serialize data in Hadoop with the Microsoft Avro Library</span></span>

>[!NOTE]
><span data-ttu-id="12357-105">Le SDK Avro n’est plus pris en charge par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="12357-105">The Avro SDK is no longer supported by Microsoft.</span></span> <span data-ttu-id="12357-106">La bibliothèque est prise en charge par la communauté open source.</span><span class="sxs-lookup"><span data-stu-id="12357-106">The library is open source community supported.</span></span> <span data-ttu-id="12357-107">Les sources de la bibliothèque se trouvent dans [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="12357-107">The sources for the library are located in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

<span data-ttu-id="12357-108">Cette rubrique illustre comment utiliser la bibliothèque [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) afin de sérialiser des objets et d’autres structures de données dans des flux pour les conserver dans une mémoire, une base de données ou un fichier.</span><span class="sxs-lookup"><span data-stu-id="12357-108">This topic shows how to use the [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) to serialize objects and other data structures into streams to persist them to memory, a database, or a file.</span></span> <span data-ttu-id="12357-109">Elle montre également comment les désérialiser pour récupérer les objets d’origine.</span><span class="sxs-lookup"><span data-stu-id="12357-109">It also shows how to deserialize them to recover the original objects.</span></span>

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a><span data-ttu-id="12357-110">Apache Avro</span><span class="sxs-lookup"><span data-stu-id="12357-110">Apache Avro</span></span>
<span data-ttu-id="12357-111">La bibliothèque <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> met en œuvre le système de sérialisation des données Apache Avro pour l’environnement Microsoft.NET.</span><span class="sxs-lookup"><span data-stu-id="12357-111">The <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implements the Apache Avro data serialization system for the Microsoft.NET environment.</span></span> <span data-ttu-id="12357-112">Apache Avro fournit un format compact d'échange des données binaires pour la sérialisation.</span><span class="sxs-lookup"><span data-stu-id="12357-112">Apache Avro provides a compact binary data interchange format for serialization.</span></span> <span data-ttu-id="12357-113">Elle utilise le format <a href="http://www.json.org" target="_blank">JSON</a> pour définir un schéma sans langage spécifié qui assure l’interopérabilité des langages.</span><span class="sxs-lookup"><span data-stu-id="12357-113">It uses <a href="http://www.json.org" target="_blank">JSON</a> to define a language-agnostic schema that underwrites language interoperability.</span></span> <span data-ttu-id="12357-114">Les données sérialisées dans un langage peuvent être lues dans un autre langage.</span><span class="sxs-lookup"><span data-stu-id="12357-114">Data serialized in one language can be read in another.</span></span> <span data-ttu-id="12357-115">Les langages C, C++, C#, Java, PHP, Python et Ruby sont actuellement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="12357-115">Currently C, C++, C#, Java, PHP, Python, and Ruby are supported.</span></span> <span data-ttu-id="12357-116">Vous pouvez trouver des informations détaillées sur ce format dans la <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Spécification Apache Avro</a>.</span><span class="sxs-lookup"><span data-stu-id="12357-116">Detailed information on the format can be found in the <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro Specification</a>.</span></span> 

>[!NOTE]
><span data-ttu-id="12357-117">Microsoft Avro Library ne prend pas en charge la partie RPC (appels de procédure distante) de cette spécification.</span><span class="sxs-lookup"><span data-stu-id="12357-117">The Microsoft Avro Library does not support the remote procedure calls (RPCs) part of this specification.</span></span>
>

<span data-ttu-id="12357-118">La représentation sérialisée d’un objet dans le système Avro est composée de deux parties : schéma et valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="12357-118">The serialized representation of an object in the Avro system consists of two parts: schema and actual value.</span></span> <span data-ttu-id="12357-119">Le schéma Avro décrit le modèle de données indépendant du langage des données sérialisées avec JSON.</span><span class="sxs-lookup"><span data-stu-id="12357-119">The Avro schema describes the language-independent data model of the serialized data with JSON.</span></span> <span data-ttu-id="12357-120">Il est présenté côte à côte avec une représentation binaire des données.</span><span class="sxs-lookup"><span data-stu-id="12357-120">It is presented side by side with a binary representation of data.</span></span> <span data-ttu-id="12357-121">Le fait de séparer le schéma de la représentation binaire permet l’écriture de chaque objet sans surcharge par valeur, ce qui permet d’accélérer la sérialisation et de réduire la représentation.</span><span class="sxs-lookup"><span data-stu-id="12357-121">Having the schema separate from the binary representation permits each object to be written with no per-value overheads, making serialization fast, and the representation small.</span></span>

## <a name="the-hadoop-scenario"></a><span data-ttu-id="12357-122">Scénario Hadoop</span><span class="sxs-lookup"><span data-stu-id="12357-122">The Hadoop scenario</span></span>
<span data-ttu-id="12357-123">Le format de sérialisation Apache Avro est largement utilisé dans Azure HDInsight et dans d’autres environnements Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="12357-123">The Apache Avro serialization format is widely used in Azure HDInsight and other Apache Hadoop environments.</span></span> <span data-ttu-id="12357-124">Avro offre un moyen pratique pour représenter des structures de données complexes dans une tâche Hadoop MapReduce.</span><span class="sxs-lookup"><span data-stu-id="12357-124">Avro provides a convenient way to represent complex data structures within a Hadoop MapReduce job.</span></span> <span data-ttu-id="12357-125">Le format des fichiers Avro (fichier conteneur d’objets Avro) a été conçu pour prendre en charge le modèle de programmation MapReduce distribué.</span><span class="sxs-lookup"><span data-stu-id="12357-125">The format of Avro files (Avro object container file) has been designed to support the distributed MapReduce programming model.</span></span> <span data-ttu-id="12357-126">La fonctionnalité clé qui permet la distribution est la possibilité de fractionner les fichiers : il est ainsi possible de rechercher un point quelconque dans un fichier et de commencer la lecture à partir d'un bloc particulier.</span><span class="sxs-lookup"><span data-stu-id="12357-126">The key feature that enables the distribution is that the files are “splittable” in the sense that one can seek any point in a file and start reading from a particular block.</span></span>

## <a name="serialization-in-avro-library"></a><span data-ttu-id="12357-127">Sérialisation dans Avro Library</span><span class="sxs-lookup"><span data-stu-id="12357-127">Serialization in Avro Library</span></span>
<span data-ttu-id="12357-128">La bibliothèque .NET pour Avro prend en charge deux types de sérialisations d'objets :</span><span class="sxs-lookup"><span data-stu-id="12357-128">The .NET Library for Avro supports two ways of serializing objects:</span></span>

* <span data-ttu-id="12357-129">**Réflexion** - Le schéma JSON des types est automatiquement généré à partir des attributs de contrat de données des types .NET à sérialiser.</span><span class="sxs-lookup"><span data-stu-id="12357-129">**reflection** - The JSON schema for the types is automatically built from the data contract attributes of the .NET types to be serialized.</span></span>
* <span data-ttu-id="12357-130">**Enregistrement générique** - Un schéma JSON est spécifié de manière explicite dans un enregistrement représenté par la classe [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) lorsqu’aucun type .NET n’est présent pour décrire le schéma des données à sérialiser.</span><span class="sxs-lookup"><span data-stu-id="12357-130">**generic record** - A JSON schema is explicitly specified in a record represented by the [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) class when no .NET types are present to describe the schema for the data to be serialized.</span></span>

<span data-ttu-id="12357-131">Lorsque le schéma de données est connu par l'enregistreur et le lecteur du flux, les données peuvent être envoyées sans le schéma associé.</span><span class="sxs-lookup"><span data-stu-id="12357-131">When the data schema is known to both the writer and reader of the stream, the data can be sent without its schema.</span></span> <span data-ttu-id="12357-132">Si un fichier conteneur d’objets Avro est utilisé, le schéma est stocké dans le fichier.</span><span class="sxs-lookup"><span data-stu-id="12357-132">In cases when an Avro object container file is used, the schema is stored within the file.</span></span> <span data-ttu-id="12357-133">D’autres paramètres, tels que le codec utilisé pour la compression des données, peuvent être spécifiés.</span><span class="sxs-lookup"><span data-stu-id="12357-133">Other parameters, such as the codec used for data compression, can be specified.</span></span> <span data-ttu-id="12357-134">Ces scénarios sont présentés plus en détail et illustrés dans les exemples de code ci-après :</span><span class="sxs-lookup"><span data-stu-id="12357-134">These scenarios are outlined in more detail and illustrated in the following code examples:</span></span>

## <a name="install-avro-library"></a><span data-ttu-id="12357-135">Installation d’Avro Library</span><span class="sxs-lookup"><span data-stu-id="12357-135">Install Avro Library</span></span>
<span data-ttu-id="12357-136">Les éléments suivants sont requis avant d’installer la bibliothèque :</span><span class="sxs-lookup"><span data-stu-id="12357-136">The following are required before you install the library:</span></span>

* <span data-ttu-id="12357-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span><span class="sxs-lookup"><span data-stu-id="12357-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span></span>
* <span data-ttu-id="12357-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (version 6.0.4 ou ultérieure)</span><span class="sxs-lookup"><span data-stu-id="12357-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 or later)</span></span>

<span data-ttu-id="12357-139">Notez que la dépendance Newtonsoft.Json.dll est également téléchargée automatiquement lors de l’installation de la bibliothèque Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="12357-139">Note that the Newtonsoft.Json.dll dependency is downloaded automatically with the installation of the Microsoft Avro Library.</span></span> <span data-ttu-id="12357-140">Cette procédure est indiquée dans la section suivante :</span><span class="sxs-lookup"><span data-stu-id="12357-140">The procedure is provided in the following section:</span></span>

<span data-ttu-id="12357-141">La bibliothèque Microsoft Avro Library est distribuée en tant que package NuGet pouvant être installé à partir de Visual Studio via la procédure suivante :</span><span class="sxs-lookup"><span data-stu-id="12357-141">The Microsoft Avro Library is distributed as a NuGet package that can be installed from Visual Studio via the following procedure:</span></span>

1. <span data-ttu-id="12357-142">Sélectionnez l'onglet **Projet** -> **Gérer les packages NuGet...**</span><span class="sxs-lookup"><span data-stu-id="12357-142">Select the **Project** tab -> **Manage NuGet Packages...**</span></span>
2. <span data-ttu-id="12357-143">Recherchez « Microsoft.Hadoop.Avro » dans la zone **Recherche en ligne** .</span><span class="sxs-lookup"><span data-stu-id="12357-143">Search for "Microsoft.Hadoop.Avro" in the **Search Online** box.</span></span>
3. <span data-ttu-id="12357-144">Cliquez sur le bouton **Installer** en regard de **Microsoft Azure HDInsight Avro Library**.</span><span class="sxs-lookup"><span data-stu-id="12357-144">Click the **Install** button next to **Microsoft Azure HDInsight Avro Library**.</span></span>

<span data-ttu-id="12357-145">Notez que la dépendance Newtonsoft.Json.dll (>= .6.0.4) est également téléchargée automatiquement avec Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="12357-145">Note that the Newtonsoft.Json.dll (>=6.0.4) dependency is also downloaded automatically with the Microsoft Avro Library.</span></span>

<span data-ttu-id="12357-146">Le code source Microsoft Avro Library est disponible dans [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="12357-146">The Microsoft Avro Library source code is available at [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

## <a name="compile-schemas-using-avro-library"></a><span data-ttu-id="12357-147">Compiler des schémas à l'aide d’Avro Library</span><span class="sxs-lookup"><span data-stu-id="12357-147">Compile schemas using Avro Library</span></span>
<span data-ttu-id="12357-148">La bibliothèque Microsoft Avro Library contient un utilitaire de génération de code qui permet de créer automatiquement des types C# basés sur le schéma JSON défini précédemment.</span><span class="sxs-lookup"><span data-stu-id="12357-148">The Microsoft Avro Library contains a code generation utility that allows creating C# types automatically based on the previously defined JSON schema.</span></span> <span data-ttu-id="12357-149">L’utilitaire de génération de code n’est pas distribué comme un code exécutable binaire, mais peut être créé sans difficulté via la procédure suivante :</span><span class="sxs-lookup"><span data-stu-id="12357-149">The code generation utility is not distributed as a binary executable, but can be easily built via the following procedure:</span></span>

1. <span data-ttu-id="12357-150">Téléchargez le fichier .zip avec la dernière version du code source du Kit de développement logiciel (SDK) HDInsight sur <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Kit de développement logiciel (SDK) Microsoft .NET pour Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="12357-150">Download the .zip file with the latest version of HDInsight SDK source code from <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK For Hadoop</a>.</span></span> <span data-ttu-id="12357-151">(Cliquez sur l’icône **Télécharger**, pas sur l’onglet **Téléchargements**.)</span><span class="sxs-lookup"><span data-stu-id="12357-151">(Click the **Download** icon, not the **Downloads** tab.)</span></span>
2. <span data-ttu-id="12357-152">Extrayez le Kit de développement logiciel (SDK) HDInsight dans un répertoire sur l’ordinateur où .NET Framework 4 a été installé et qui est connecté à Internet afin de télécharger les packages NuGet de dépendance nécessaires.</span><span class="sxs-lookup"><span data-stu-id="12357-152">Extract the HDInsight SDK to a directory on the machine with .NET Framework 4 installed and connected to the Internet for downloading necessary dependency NuGet packages.</span></span> <span data-ttu-id="12357-153">Nous supposons ci-après que le code source est extrait dans C:\SDK.</span><span class="sxs-lookup"><span data-stu-id="12357-153">Below, we assume that the source code is extracted to C:\SDK.</span></span>
3. <span data-ttu-id="12357-154">Accédez au dossier C:\SDK\src\Microsoft.Hadoop.Avro.Tools et exécutez build.bat.</span><span class="sxs-lookup"><span data-stu-id="12357-154">Go to the folder C:\SDK\src\Microsoft.Hadoop.Avro.Tools and run build.bat.</span></span> <span data-ttu-id="12357-155">(Le fichier appelle MSBuild à partir de la distribution 32 bits de .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="12357-155">(The file calls MSBuild from the 32-bit distribution of the .NET Framework.</span></span> <span data-ttu-id="12357-156">Si vous voulez utiliser la version 64 bits, modifiez build.bat en suivant les commentaires à l’intérieur du fichier.) Assurez-vous que la génération est réussie.</span><span class="sxs-lookup"><span data-stu-id="12357-156">If you would like to use the 64-bit version, edit build.bat, following the comments inside the file.) Ensure that the build is successful.</span></span> <span data-ttu-id="12357-157">(Sur certains systèmes, MSBuild peut générer des avertissements.</span><span class="sxs-lookup"><span data-stu-id="12357-157">(On some systems, MSBuild may produce warnings.</span></span> <span data-ttu-id="12357-158">Ceux-ci n’affectent pas l’utilitaire tant qu’il n’existe aucune erreur de génération.)</span><span class="sxs-lookup"><span data-stu-id="12357-158">These warnings do not affect the utility as long as there are no build errors.)</span></span>
4. <span data-ttu-id="12357-159">L’utilitaire compilé se trouve à l’emplacement suivant : C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span><span class="sxs-lookup"><span data-stu-id="12357-159">The compiled utility is located in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span></span>

<span data-ttu-id="12357-160">Pour vous familiariser avec la syntaxe de la ligne de commande, exécutez la commande suivante depuis le dossier où se trouve l’utilitaire de génération de code : `Microsoft.Hadoop.Avro.Tools help /c:codegen`.</span><span class="sxs-lookup"><span data-stu-id="12357-160">To get familiar with the command-line syntax, execute the following command from the folder where the code generation utility is located: `Microsoft.Hadoop.Avro.Tools help /c:codegen`</span></span>

<span data-ttu-id="12357-161">Pour tester l’utilitaire, vous pouvez générer des classes C# à partir du fichier de schéma JSON de l’exemple fourni avec le code source.</span><span class="sxs-lookup"><span data-stu-id="12357-161">To test the utility, you can generate C# classes from the sample JSON schema file provided with the source code.</span></span> <span data-ttu-id="12357-162">Exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="12357-162">Execute the following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

<span data-ttu-id="12357-163">Cette commande est censée créer deux fichiers C# dans le répertoire actif : SensorData.cs et Location.cs.</span><span class="sxs-lookup"><span data-stu-id="12357-163">This is supposed to produce two C# files in the current directory: SensorData.cs and Location.cs.</span></span>

<span data-ttu-id="12357-164">Pour comprendre la logique utilisée par l’utilitaire de génération de code lorsque le schéma JSON est converti en types C#, reportez-vous au fichier GenerationVerification.feature, situé à l’emplacement suivant : C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span><span class="sxs-lookup"><span data-stu-id="12357-164">To understand the logic that the code generation utility is using while converting the JSON schema to C# types, see the file GenerationVerification.feature located in C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span></span>

<span data-ttu-id="12357-165">Les espaces de noms sont extraits du schéma JSON suivant la logique décrite dans le fichier mentionné au paragraphe précédent.</span><span class="sxs-lookup"><span data-stu-id="12357-165">Namespaces are extracted from the JSON schema, using the logic described in the file mentioned in the previous paragraph.</span></span> <span data-ttu-id="12357-166">Les espaces de noms extraits du schéma sont prioritaires sur tout ce qui est fourni avec le paramètre /n sur la ligne de commande de l’utilitaire.</span><span class="sxs-lookup"><span data-stu-id="12357-166">Namespaces extracted from the schema take precedence over whatever is provided with the /n parameter in the utility command line.</span></span> <span data-ttu-id="12357-167">Si vous voulez remplacer les espaces de noms contenus dans le schéma, utilisez le paramètre /nf.</span><span class="sxs-lookup"><span data-stu-id="12357-167">If you want to override the namespaces contained within the schema, use the /nf parameter.</span></span> <span data-ttu-id="12357-168">Par exemple, pour changer tous les espaces de noms du schéma SampleJSONSchema.avsc en my.own.nspace, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="12357-168">For example, to change all namespaces from the SampleJSONSchema.avsc to my.own.nspace, execute the following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-the-samples"></a><span data-ttu-id="12357-169">À propos des exemples</span><span class="sxs-lookup"><span data-stu-id="12357-169">About the samples</span></span>
<span data-ttu-id="12357-170">Les six exemples fournis dans cette rubrique illustrent chacun un scénario différent pris en charge par Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="12357-170">Six examples provided in this topic illustrate different scenarios supported by the Microsoft Avro Library.</span></span> <span data-ttu-id="12357-171">Microsoft Avro Library est conçu pour fonctionner avec n'importe quel flux.</span><span class="sxs-lookup"><span data-stu-id="12357-171">The Microsoft Avro Library is designed to work with any stream.</span></span> <span data-ttu-id="12357-172">Dans ces exemples, les données sont manipulées à l’aide de flux de mémoire plutôt que de flux de fichiers ou de bases de données pour des questions de simplicité et de cohérence.</span><span class="sxs-lookup"><span data-stu-id="12357-172">In these examples, data is manipulated via memory streams rather than file streams or databases for simplicity and consistency.</span></span> <span data-ttu-id="12357-173">L’approche au sein d’un environnement de production dépend des exigences du scénario, de la source et du volume des données, des contraintes en matière de performances et d’autres facteurs.</span><span class="sxs-lookup"><span data-stu-id="12357-173">The approach taken in a production environment depends on the exact scenario requirements, data source and volume, performance constraints, and other factors.</span></span>

<span data-ttu-id="12357-174">Les deux premiers exemples montrent comment sérialiser et désérialiser des données dans des mémoires tampons de flux de mémoire à l’aide de la réflexion et d’enregistrements génériques.</span><span class="sxs-lookup"><span data-stu-id="12357-174">The first two examples show how to serialize and deserialize data into memory stream buffers by using reflection and generic records.</span></span> <span data-ttu-id="12357-175">Le schéma dans ces deux cas est supposé être partagé entre les lecteurs et les enregistreurs hors bande.</span><span class="sxs-lookup"><span data-stu-id="12357-175">The schema in these two cases is assumed to be shared between the readers and writers out-of-band.</span></span>

<span data-ttu-id="12357-176">Les troisième et quatrième exemples montrent comment sérialiser et désérialiser des données avec les fichiers conteneurs d’objets Avro.</span><span class="sxs-lookup"><span data-stu-id="12357-176">The third and fourth examples show how to serialize and deserialize data by using the Avro object container files.</span></span> <span data-ttu-id="12357-177">Lorsque les données sont stockées dans un fichier conteneur Avro, leur schéma est toujours stocké avec, car il doit être partagé pour la désérialisation.</span><span class="sxs-lookup"><span data-stu-id="12357-177">When data is stored in an Avro container file, its schema is always stored with it because the schema must be shared for deserialization.</span></span>

<span data-ttu-id="12357-178">L’échantillon contenant les quatre premiers exemples peut être téléchargé sur le site des <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">exemples de code Azure</a> .</span><span class="sxs-lookup"><span data-stu-id="12357-178">The sample containing the first four examples can be downloaded from the <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="12357-179">Le cinquième exemple montre comment utiliser un codec de compression personnalisé pour les fichiers conteneurs d’objets Avro.</span><span class="sxs-lookup"><span data-stu-id="12357-179">The fifth example shows how to use a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="12357-180">Un échantillon contenant le code de cet exemple peut être téléchargé sur le site des <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">exemples de code Azure</a> .</span><span class="sxs-lookup"><span data-stu-id="12357-180">A sample containing the code for this example can be downloaded from the <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="12357-181">Le sixième exemple montre comment utiliser la sérialisation Avro pour télécharger des données dans le stockage d’objets blob Azure, puis les analyser à l’aide de Hive avec un cluster HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="12357-181">The sixth sample shows how to use Avro serialization to upload data to Azure Blob storage and then analyze it by using Hive with an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="12357-182">Vous pouvez le télécharger sur le site <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">exemples de code Azure</a> .</span><span class="sxs-lookup"><span data-stu-id="12357-182">It can be downloaded from the <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="12357-183">Les liens suivants renvoient aux six exemples que nous avons examinés dans la rubrique :</span><span class="sxs-lookup"><span data-stu-id="12357-183">Here are links to the six samples discussed in the topic:</span></span>

* <span data-ttu-id="12357-184"><a href="#Scenario1">**Sérialisation avec réflexion**</a> - Le schéma JSON pour les types à sérialiser est automatiquement généré à partir des attributs de contrat de données.</span><span class="sxs-lookup"><span data-stu-id="12357-184"><a href="#Scenario1">**Serialization with reflection**</a> - The JSON schema for types to be serialized is automatically built from the data contract attributes.</span></span>
* <span data-ttu-id="12357-185"><a href="#Scenario2">**Sérialisation avec enregistrement générique**</a> - Le schéma JSON est spécifié de manière explicite dans un enregistrement lorsqu’aucun type .NET n’est disponible pour la réflexion.</span><span class="sxs-lookup"><span data-stu-id="12357-185"><a href="#Scenario2">**Serialization with generic record**</a> - The JSON schema is explicitly specified in a record when no .NET type is available for reflection.</span></span>
* <span data-ttu-id="12357-186"><a href="#Scenario3">**Sérialisation à l’aide de fichiers conteneurs d’objets avec réflexion**</a> - Le schéma JSON est automatiquement créé et partagé en même temps que les données sérialisées, via un fichier conteneur d’objets Avro.</span><span class="sxs-lookup"><span data-stu-id="12357-186"><a href="#Scenario3">**Serialization using object container files with reflection**</a> - The JSON schema is automatically built and shared together with the serialized data via an Avro object container file.</span></span>
* <span data-ttu-id="12357-187"><a href="#Scenario4">**Sérialisation à l’aide de fichiers conteneurs d’objets avec enregistrement générique**</a> - Le schéma JSON est spécifié de manière explicite avant la sérialisation et partagé en même temps que les données sérialisées, via un fichier conteneur d’objets Avro.</span><span class="sxs-lookup"><span data-stu-id="12357-187"><a href="#Scenario4">**Serialization using object container files with generic record**</a> - The JSON schema is explicitly specified before the serialization and shared together with the data via an Avro object container file.</span></span>
* <span data-ttu-id="12357-188"><a href="#Scenario5">**Sérialisation à l’aide de fichiers conteneurs d’objets avec un codec de compression personnalisé**</a> - L’exemple montre comment créer un fichier conteneur d’objets Avro avec une implémentation .NET personnalisée du codec de compression de données Deflate.</span><span class="sxs-lookup"><span data-stu-id="12357-188"><a href="#Scenario5">**Serialization using object container files with a custom compression codec**</a> - The example shows how to create an Avro object container file with a customized .NET implementation of the Deflate data compression codec.</span></span>
* <span data-ttu-id="12357-189"><a href="#Scenario6">**Utilisation d’Avro pour télécharger des données pour le service Microsoft Azure HDInsight**</a> - L’exemple illustre comment la sérialisation Avro interagit avec le service HDInsight.</span><span class="sxs-lookup"><span data-stu-id="12357-189"><a href="#Scenario6">**Using Avro to upload data for the Microsoft Azure HDInsight service**</a> - The example illustrates how Avro serialization interacts with the HDInsight service.</span></span> <span data-ttu-id="12357-190">Un abonnement Azure actif et l’accès à un cluster Azure HDInsight sont requis pour exécuter cet exemple.</span><span class="sxs-lookup"><span data-stu-id="12357-190">An active Azure subscription and access to an Azure HDInsight cluster are required to run this example.</span></span>

## <span data-ttu-id="12357-191"><a name="Scenario1"></a>Exemple 1 : sérialisation avec réflexion</span><span class="sxs-lookup"><span data-stu-id="12357-191"><a name="Scenario1"></a>Sample 1: Serialization with reflection</span></span>
<span data-ttu-id="12357-192">Le schéma JSON des types peut être généré automatiquement par la bibliothèque Microsoft Avro Library via la réflexion, à partir des attributs de contrat de données des objets C# à sérialiser.</span><span class="sxs-lookup"><span data-stu-id="12357-192">The JSON schema for the types can be automatically built by the Microsoft Avro Library via reflection from the data contract attributes of the C# objects to be serialized.</span></span> <span data-ttu-id="12357-193">La bibliothèque Microsoft Avro Library crée un [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) pour identifier les champs à sérialiser.</span><span class="sxs-lookup"><span data-stu-id="12357-193">The Microsoft Avro Library creates an [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) to identify the fields to be serialized.</span></span>

<span data-ttu-id="12357-194">Dans cet exemple, les objets (classe **SensorData** avec struct **Location** de membre) sont sérialisés dans un flux de mémoire qui est à son tour désérialisé.</span><span class="sxs-lookup"><span data-stu-id="12357-194">In this example, objects (a **SensorData** class with a member **Location** struct) are serialized to a memory stream, and this stream is in turn deserialized.</span></span> <span data-ttu-id="12357-195">Le résultat est ensuite comparé avec l’instance d’origine pour vérifier que l’objet **SensorData** récupéré est identique à l’original.</span><span class="sxs-lookup"><span data-stu-id="12357-195">The result is then compared to the initial instance to confirm that the **SensorData** object recovered is identical to the original.</span></span>

<span data-ttu-id="12357-196">Le schéma présenté dans cet exemple étant supposé partagé entre les lecteurs et les enregistreurs, le format de conteneur d'objet Avro n'est pas requis.</span><span class="sxs-lookup"><span data-stu-id="12357-196">The schema in this example is assumed to be shared between the readers and writers, so the Avro object container format is not required.</span></span> <span data-ttu-id="12357-197">Pour un exemple de sérialisation et de désérialisation de données dans des mémoires tampons à l’aide de la réflexion avec le format de conteneur d’objet lorsque le schéma doit être partagé avec les données, consultez le scénario relatif à la <a href="#Scenario3">Sérialisation à l’aide de fichiers conteneurs d’objets avec réflexion</a>.</span><span class="sxs-lookup"><span data-stu-id="12357-197">For an example of how to serialize and deserialize data into memory buffers by using reflection with the object container format when the schema must be shared with the data, see <a href="#Scenario3">Serialization using object container files with reflection</a>.</span></span>

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
        //the usage of Microsoft Avro Library
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

                    //Serialize the data to the specified stream
                    avroSerializer.Serialize(buffer, expected);


                    Console.WriteLine("Deserializing Sample Data Set...");

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Deserialize data from the stream and cast it to the same type used for serialization
                    var actual = avroSerializer.Deserialize(buffer);

                    Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                    //Finally, verify that deserialized data matches the original one
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

                //Serialization to memory using reflection
                Sample.SerializeDeserializeObjectUsingReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING REFLECTION
    //
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.


## <a name="sample-2-serialization-with-a-generic-record"></a><span data-ttu-id="12357-198">Exemple 2 : sérialisation avec enregistrement générique</span><span class="sxs-lookup"><span data-stu-id="12357-198">Sample 2: Serialization with a generic record</span></span>
<span data-ttu-id="12357-199">Un schéma JSON peut être spécifié de manière explicite dans un enregistrement générique lorsque la réflexion ne peut pas être utilisée, car les données ne peuvent pas être représentées à l’aide de classes .NET avec un contrat de données.</span><span class="sxs-lookup"><span data-stu-id="12357-199">A JSON schema can be explicitly specified in a generic record when reflection cannot be used because the data cannot be represented via .NET classes with a data contract.</span></span> <span data-ttu-id="12357-200">Cette méthode est plus lente que celle qui utilise la réflexion.</span><span class="sxs-lookup"><span data-stu-id="12357-200">This method is slower than using reflection.</span></span> <span data-ttu-id="12357-201">Dans ce cas, le schéma des données peut également être dynamique, c’est-à-dire inconnu au moment de la compilation.</span><span class="sxs-lookup"><span data-stu-id="12357-201">In such cases, the schema for the data may also be dynamic, that is, not known at compile time.</span></span> <span data-ttu-id="12357-202">Voici un exemple de ce type de scénario dynamique : des données représentées sous forme de fichiers CSV dont le schéma est inconnu tant qu’il n’a pas été transformé en format Avro au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="12357-202">Data represented as comma-separated values (CSV) files whose schema is unknown until it is transformed to the Avro format at run time is an example of this sort of dynamic scenario.</span></span>

<span data-ttu-id="12357-203">Cet exemple montre comment créer et utiliser un [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) pour spécifier explicitement un schéma JSON, comment le remplir avec les données, puis comment le sérialiser/désérialiser.</span><span class="sxs-lookup"><span data-stu-id="12357-203">This example shows how to create and use an [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) to explicitly specify a JSON schema, how to populate it with the data, and then how to serialize and deserialize it.</span></span> <span data-ttu-id="12357-204">Le résultat est ensuite comparé avec l’instance d’origine pour confirmer que l’enregistrement récupéré est identique à l’original.</span><span class="sxs-lookup"><span data-stu-id="12357-204">The result is then compared to the initial instance to confirm that the record recovered is identical to the original.</span></span>

<span data-ttu-id="12357-205">Le schéma présenté dans cet exemple étant supposé partagé entre les lecteurs et les enregistreurs, le format de conteneur d'objet Avro n'est pas requis.</span><span class="sxs-lookup"><span data-stu-id="12357-205">The schema in this example is assumed to be shared between the readers and writers, so the Avro object container format is not required.</span></span> <span data-ttu-id="12357-206">Pour un exemple de sérialisation et de désérialisation de données dans des mémoires tampons à l’aide d’un enregistrement générique avec le format de conteneur d’objet lorsque le schéma doit être inclus avec les données sérialisées, consultez l’exemple de <a href="#Scenario4">Sérialisation à l’aide de fichiers conteneurs d’objets avec enregistrement générique</a>.</span><span class="sxs-lookup"><span data-stu-id="12357-206">For an example of how to serialize and deserialize data into memory buffers by using a generic record with the object container format when the schema must be included with the serialized data, see the <a href="#Scenario4">Serialization using object container files with generic record</a> example.</span></span>

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
    //the usage of Microsoft Avro Library
    public class AvroSample
    {

        //Serialize and deserialize sample data set by using a generic record.
        //A generic record is a special class with the schema explicitly defined in JSON.
        //All serialized data should be mapped to the fields of the generic record,
        //which in turn is then serialized.
        public void SerializeDeserializeObjectUsingGenericRecords()
        {
            Console.WriteLine("SERIALIZATION USING GENERIC RECORD\n");
            Console.WriteLine("Defining the Schema and creating Sample Data Set...");

            //Define the schema in JSON
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

            //Create a generic serializer based on the schema
            var serializer = AvroSerializer.CreateGeneric(Schema);
            var rootSchema = serializer.WriterSchema as RecordSchema;

            //Create a memory stream buffer
            using (var stream = new MemoryStream())
            {
                //Create a generic record to represent the data
                dynamic location = new AvroRecord(rootSchema.GetField("Location").TypeSchema);
                location.Floor = 1;
                location.Room = 243;

                dynamic expected = new AvroRecord(serializer.WriterSchema);
                expected.Location = location;
                expected.Value = new byte[] { 1, 2, 3, 4, 5 };

                Console.WriteLine("Serializing Sample Data Set...");

                //Serialize the data
                serializer.Serialize(stream, expected);

                stream.Seek(0, SeekOrigin.Begin);

                Console.WriteLine("Deserializing Sample Data Set...");

                //Deserialize the data into a generic record
                dynamic actual = serializer.Deserialize(stream);

                Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                //Finally, verify the results
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

            //Serialization to memory using generic record
            Sample.SerializeDeserializeObjectUsingGenericRecords();

            Console.WriteLine(sectionDivider);
            Console.WriteLine("Press any key to exit.");
            Console.Read();
        }
    }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING GENERIC RECORD
    //
    // Defining the Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // Result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a><span data-ttu-id="12357-207">Exemple 3 : sérialisation à l'aide de fichiers conteneurs d'objets et sérialisation avec réflexion</span><span class="sxs-lookup"><span data-stu-id="12357-207">Sample 3: Serialization using object container files and serialization with reflection</span></span>
<span data-ttu-id="12357-208">Cet exemple est similaire au scénario du <a href="#Scenario1"> premier exemple</a> où le schéma est spécifié implicitement avec la réflexion.</span><span class="sxs-lookup"><span data-stu-id="12357-208">This example is similar to the scenario in the <a href="#Scenario1"> first example</a>, where the schema is implicitly specified with reflection.</span></span> <span data-ttu-id="12357-209">La différence est que, dans le présent exemple, le schéma n’est pas supposé être connu du lecteur qui le désérialise.</span><span class="sxs-lookup"><span data-stu-id="12357-209">The difference is that here, the schema is not assumed to be known to the reader that deserializes it.</span></span> <span data-ttu-id="12357-210">Les objets **SensorData** à sérialiser et leurs schémas associés spécifiés de manière implicite sont stockés dans un fichier conteneur d’objet représenté par la classe [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx).</span><span class="sxs-lookup"><span data-stu-id="12357-210">The **SensorData** objects to be serialized and their implicitly specified schema are stored in an Avro object container file represented by the [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span>

<span data-ttu-id="12357-211">Dans cet exemple, les données sont sérialisées avec [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) et désérialisées avec [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span><span class="sxs-lookup"><span data-stu-id="12357-211">The data is serialized in this example with [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) and deserialized with [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span></span> <span data-ttu-id="12357-212">Le résultat est ensuite comparé aux instances d’origine afin d’en vérifier l’identité.</span><span class="sxs-lookup"><span data-stu-id="12357-212">The result then is compared to the initial instances to ensure identity.</span></span>

<span data-ttu-id="12357-213">Les données du fichier conteneur d’objet sont compressées à l’aide du codec de compression [**Deflate**][deflate-100] par défaut issu de .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="12357-213">The data in the object container file is compressed via the default [**Deflate**][deflate-100] compression codec from .NET Framework 4.</span></span> <span data-ttu-id="12357-214">Consultez le <a href="#Scenario5">cinquième exemple</a> de cette rubrique pour savoir comment utiliser une version ultérieure et plus récente du codec de compression [**Deflate**][deflate-110] disponible dans .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="12357-214">See the <a href="#Scenario5"> fifth example</a> in this topic to learn how to use a more recent and superior version of the [**Deflate**][deflate-110] compression codec available in .NET Framework 4.5.</span></span>

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
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes the sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with the Deflate codec.
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

                //Serializing and saving data to file.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects to stream.
                    //Data is compressed using the Deflate codec.
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize the data to stream by using the sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream to file
                    Console.WriteLine("Saving serialized data to file...");
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

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from the given stream.
                    //It allows iterating over the deserialized objects because it implements the IEnumerable<T> interface.
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true)))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches the original one
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

                //Delete the file
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

            //Saving memory stream to a new file with the given path
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
                        Console.WriteLine("The following exception was thrown during creation and writing to the file \"{0}\"", path);
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

            //Reading a file content by using the given path to a memory stream
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
                    Console.WriteLine("The following exception was thrown during reading from the file \"{0}\"", path);
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
                        Console.WriteLine("The following exception was thrown during deleting the file \"{0}\"", path);
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

                //Serialization using reflection to Avro object container file
                Sample.SerializeDeserializeUsingObjectContainersReflection();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING REFLECTION AND AVRO OBJECT CONTAINER FILES
    //
    // Serializing Sample Data Set...
    // Saving serialized data to file...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a><span data-ttu-id="12357-215">Exemple 4 : sérialisation à l'aide de fichiers conteneurs d'objets et sérialisation avec enregistrement générique</span><span class="sxs-lookup"><span data-stu-id="12357-215">Sample 4: Serialization using object container files and serialization with generic record</span></span>
<span data-ttu-id="12357-216">Cet exemple est similaire au scénario du <a href="#Scenario2"> deuxième exemple</a> où le schéma est spécifié explicitement avec le format JSON.</span><span class="sxs-lookup"><span data-stu-id="12357-216">This example is similar to the scenario in the <a href="#Scenario2"> second example</a>, where the schema is explicitly specified with JSON.</span></span> <span data-ttu-id="12357-217">La différence est que, dans le présent exemple, le schéma n’est pas supposé être connu du lecteur qui le désérialise.</span><span class="sxs-lookup"><span data-stu-id="12357-217">The difference is that here, the schema is not assumed to be known to the reader that deserializes it.</span></span>

<span data-ttu-id="12357-218">Le jeu de données de test est collecté dans une liste d’objets [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) via un schéma JSON défini explicitement, puis stocké dans un fichier conteneur d’objet représenté par la classe [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx).</span><span class="sxs-lookup"><span data-stu-id="12357-218">The test data set is collected into a list of [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objects via an explicitly defined JSON schema and then stored in an object container file represented by the [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span> <span data-ttu-id="12357-219">Ce fichier conteneur crée un enregistreur qui permet de sérialiser les données décompressées dans un flux de mémoire qui est ensuite enregistré dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="12357-219">This container file creates a writer that is used to serialize the data, uncompressed, to a memory stream that is then saved to a file.</span></span> <span data-ttu-id="12357-220">Le paramètre [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) utilisé pour créer le lecteur spécifie que ces données ne sont pas compressées.</span><span class="sxs-lookup"><span data-stu-id="12357-220">The [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parameter used for creating the reader specifies that this data is not compressed.</span></span>

<span data-ttu-id="12357-221">Les données sont ensuite lues à partir du fichier et désérialisées dans une collection d'objets.</span><span class="sxs-lookup"><span data-stu-id="12357-221">The data is then read from the file and deserialized into a collection of objects.</span></span> <span data-ttu-id="12357-222">Cette dernière est ensuite comparée à la liste initiale d'enregistrements Avro pour confirmer qu'ils sont identiques.</span><span class="sxs-lookup"><span data-stu-id="12357-222">This collection is compared to the initial list of Avro records to confirm that they are identical.</span></span>

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
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes a sample data set by using a generic record and Avro object container files.
            //Serialized data is not compressed.
            public void SerializeDeserializeUsingObjectContainersGenericRecord()
            {
                Console.WriteLine("SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES\n");

                //Path for Avro object container file
                string path = "AvroSampleGenericRecordNullCodec.avro";

                Console.WriteLine("Defining the Schema and creating Sample Data Set...");

                //Define the schema in JSON
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

                //Create a generic serializer based on the schema
                var serializer = AvroSerializer.CreateGeneric(Schema);
                var rootSchema = serializer.WriterSchema as RecordSchema;

                //Create a generic record to represent the data
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

                //Serializing and saving data to file.
                //Create a MemoryStream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects to stream.
                    //Data is not compressed (Null compression codec).
                    using (var writer = AvroContainer.CreateGenericWriter(Schema, buffer, Codec.Null))
                    {
                        using (var streamWriter = new SequentialWriter<object>(writer, 24))
                        {
                            // Serialize the data to stream by using the sequential writer
                            testData.ForEach(streamWriter.Write);
                        }
                    }

                    Console.WriteLine("Saving serialized data to file...");

                    //Save stream to file
                    if (!WriteFile(buffer, path))
                    {
                        Console.WriteLine("Error during file operation. Quitting method");
                        return;
                    }
                }

                //Reading and deserializing the data.
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

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from the given stream.
                    //It allows iterating over the deserialized objects because it implements the IEnumerable<T> interface.
                    using (var reader = AvroContainer.CreateGenericReader(buffer))
                    {
                        using (var streamReader = new SequentialReader<object>(reader))
                        {
                            var results = streamReader.Objects;

                            Console.WriteLine("Comparing Initial and Deserialized Data Sets...");

                            //Finally, verify the results
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

                //Delete the file
                RemoveFile(path);
            }

            //
            //Helper methods
            //

            //Saving memory stream to a new file with the given path
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
                        Console.WriteLine("The following exception was thrown during creation and writing to the file \"{0}\"", path);
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

            //Reading a file content by using the given path to a memory stream
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
                    Console.WriteLine("The following exception was thrown during reading from the file \"{0}\"", path);
                    Console.WriteLine(e.Message);
                    return false;
                }
            }

            //Deleting file by using the given path
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
                        Console.WriteLine("The following exception was thrown during deleting the file \"{0}\"", path);
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

                //Create an instance of the AvroSample class and invoke methods
                //illustrating different serializing approaches
                AvroSample Sample = new AvroSample();

                //Serialization using generic record to Avro object container file
                Sample.SerializeDeserializeUsingObjectContainersGenericRecord();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING GENERIC RECORD AND AVRO OBJECT CONTAINER FILES
    //
    // Defining the Schema and creating Sample Data Set...
    // Serializing Sample Data Set...
    // Saving serialized data to file...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    // For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a><span data-ttu-id="12357-223">Exemple 5: sérialisation à l'aide de fichiers conteneurs d'objets avec un codec de compression personnalisé</span><span class="sxs-lookup"><span data-stu-id="12357-223">Sample 5: Serialization using object container files with a custom compression codec</span></span>
<span data-ttu-id="12357-224">Le cinquième exemple montre comment utiliser un codec de compression personnalisé pour les fichiers conteneurs d’objets Avro.</span><span class="sxs-lookup"><span data-stu-id="12357-224">The fifth example shows how to use a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="12357-225">Un échantillon contenant le code de cet exemple peut être téléchargé sur le site des [exemples de code Azure](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) .</span><span class="sxs-lookup"><span data-stu-id="12357-225">A sample containing the code for this example can be downloaded from the [Azure code samples](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span></span>

<span data-ttu-id="12357-226">La [Spécification Avro](http://avro.apache.org/docs/current/spec.html#Required+Codecs) autorise l'utilisation d'un codec de compression facultatif (outre les codecs **Null** et **Deflate** par défaut).</span><span class="sxs-lookup"><span data-stu-id="12357-226">The [Avro Specification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) allows usage of an optional compression codec (in addition to **Null** and **Deflate** defaults).</span></span> <span data-ttu-id="12357-227">Cet exemple n’implémente pas un nouveau codec tel que Snappy (mentionné comme codec facultatif pris en charge dans la [Spécification Avro](http://avro.apache.org/docs/current/spec.html#snappy)).</span><span class="sxs-lookup"><span data-stu-id="12357-227">This example is not implementing a new codec such as Snappy (mentioned as a supported optional codec in the [Avro Specification](http://avro.apache.org/docs/current/spec.html#snappy)).</span></span> <span data-ttu-id="12357-228">Il montre comment utiliser l’implémentation .NET Framework 4.5 du codec [**Deflate**][deflate-110], qui offre un algorithme de compression, basé sur la bibliothèque de compression [zlib](http://zlib.net/), plus efficace que celui de la version par défaut .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="12357-228">It shows how to use the .NET Framework 4.5 implementation of the [**Deflate**][deflate-110] codec, which provides a better compression algorithm based on the [zlib](http://zlib.net/) compression library than the default .NET Framework 4 version.</span></span>

    //
    // This code needs to be compiled with the parameter Target Framework set as ".NET Framework 4.5"
    // to ensure the desired implementation of the Deflate compression algorithm is used.
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
        //which are the key ones for data compression.
        //To enable a custom codec, one needs to implement these methods for the required codec.

        #region Defining Compression and Decompression Streams
        //DeflateStream (class from System.IO.Compression namespace that implements Deflate algorithm)
        //cannot be directly used for Avro because it does not support vital operations like Seek.
        //Thus one needs to implement two classes inherited from stream
        //(one for compressed and one for decompressed stream)
        //that use Deflate compression and implement all required features.
        internal sealed class CompressionStreamDeflate45 : Stream
        {
            private readonly Stream buffer;
            private DeflateStream compressionStream;

            public CompressionStreamDeflate45(Stream buffer)
            {
                Debug.Assert(buffer != null, "Buffer is not allowed to be null.");

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
        //Define the actual codec class containing the required methods for manipulating streams:
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
        //Define modified codec factory to be used in the reader.
        //It catches the attempt to use "Deflate" and provide  a custom codec.
        //For all other cases, it relies on the base class (CodecFactory).
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
        //the usage of Microsoft Avro Library
        public class AvroSample
        {

            //Serializes and deserializes sample data set by using reflection and Avro object container files.
            //Serialized data is compressed with the custom compression codec (Deflate of .NET Framework 4.5).
            //
            //This sample uses memory stream for all operations related to serialization, deserialization and
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

                //Serializing and saving data to file.
                //Creating a memory stream buffer.
                using (var buffer = new MemoryStream())
                {
                    Console.WriteLine("Serializing Sample Data Set...");

                    //Create a SequentialWriter instance for type SensorData, which can serialize a sequence of SensorData objects to stream.
                    //Here the custom codec is introduced. For convenience, the next commented code line shows how to use built-in Deflate.
                    //Note that because the sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var w = AvroContainer.CreateWriter<SensorData>(buffer, Codec.Deflate))
                    using (var w = AvroContainer.CreateWriter<SensorData>(buffer, new DeflateCodec45()))
                    {
                        using (var writer = new SequentialWriter<SensorData>(w, 24))
                        {
                            // Serialize the data to stream using the sequential writer
                            testData.ForEach(writer.Write);
                        }
                    }

                    //Save stream to file
                    Console.WriteLine("Saving serialized data to file...");
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

                    //Prepare the stream for deserializing the data
                    buffer.Seek(0, SeekOrigin.Begin);

                    //Because of SequentialReader<T> constructor signature, an AvroSerializerSettings instance is required
                    //when codec factory is explicitly specified.
                    //You may comment the line below if you want to use built-in Deflate (see next comment).
                    AvroSerializerSettings settings = new AvroSerializerSettings();

                    //Create a SequentialReader instance for type SensorData, which deserializes all serialized objects from the given stream.
                    //It allows iterating over the deserialized objects because it implements the IEnumerable<T> interface.
                    //Here the custom codec factory is introduced.
                    //For convenience, the next commented code line shows how to use built-in Deflate
                    //(no explicit Codec Factory parameter is required in this case).
                    //Note that because the sample deals with different IMPLEMENTATIONS of Deflate, built-in and custom codecs are interchangeable
                    //in read-write operations.
                    //using (var reader = new SequentialReader<SensorData>(AvroContainer.CreateReader<SensorData>(buffer, true)))
                    using (var reader = new SequentialReader<SensorData>(
                        AvroContainer.CreateReader<SensorData>(buffer, true, settings, new CodecFactoryDeflate45())))
                    {
                        var results = reader.Objects;

                        //Finally, verify that deserialized data matches the original one
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

                //Delete the file
                RemoveFile(path);
            }
        #endregion

            #region Helper Methods

            //Comparing two SensorData objects
            private bool Equal(SensorData left, SensorData right)
            {
                return left.Position.Equals(right.Position) && left.Value.SequenceEqual(right.Value);
            }

            //Saving memory stream to a new file with the given path
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
                        Console.WriteLine("The following exception was thrown during creation and writing to the file \"{0}\"", path);
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

            //Reading file content by using the given path to a memory stream
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
                    Console.WriteLine("The following exception was thrown during reading from the file \"{0}\"", path);
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
                        Console.WriteLine("The following exception was thrown during deleting the file \"{0}\"", path);
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

                //Serialization using reflection to Avro object container file using custom codec
                Sample.SerializeDeserializeUsingObjectContainersReflectionCustomCodec();

                Console.WriteLine(sectionDivider);
                Console.WriteLine("Press any key to exit.");
                Console.Read();
            }
        }
    }
    // The example is expected to display the following output:
    // SERIALIZATION USING REFLECTION, AVRO OBJECT CONTAINER FILES AND CUSTOM CODEC
    //
    // Serializing Sample Data Set...
    // Saving serialized data to file...
    // Reading data from file...
    // Deserializing Sample Data Set...
    // Comparing Initial and Deserialized Data Sets...
    // For Pair 1 result of Data Set Identity Comparison is True
    //For Pair 2 result of Data Set Identity Comparison is True
    // ----------------------------------------
    // Press any key to exit.

## <a name="sample-6-using-avro-to-upload-data-for-the-microsoft-azure-hdinsight-service"></a><span data-ttu-id="12357-229">Exemple 6 : utilisation d'Avro pour télécharger des données pour le service Microsoft Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="12357-229">Sample 6: Using Avro to upload data for the Microsoft Azure HDInsight service</span></span>
<span data-ttu-id="12357-230">Le sixième exemple illustre quelques techniques de programmation liées à l’interaction avec le service Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="12357-230">The sixth example illustrates some programming techniques related to interacting with the Azure HDInsight service.</span></span> <span data-ttu-id="12357-231">Un échantillon contenant le code de cet exemple peut être téléchargé sur le site des [exemples de code Azure](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) .</span><span class="sxs-lookup"><span data-stu-id="12357-231">A sample containing the code for this example can be downloaded from the [Azure code samples](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span></span>

<span data-ttu-id="12357-232">L’exemple effectue les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="12357-232">The sample does the following tasks:</span></span>

* <span data-ttu-id="12357-233">Établit la connexion à un cluster existant du service HDInsight.</span><span class="sxs-lookup"><span data-stu-id="12357-233">Connects to an existing HDInsight service cluster.</span></span>
* <span data-ttu-id="12357-234">Sérialise plusieurs fichiers CSV et télécharge le résultat dans le stockage d'objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="12357-234">Serializes several CSV files and uploads the result to Azure Blob storage.</span></span> <span data-ttu-id="12357-235">(Les fichiers CSV sont distribués avec l’exemple et représentent un extrait des données historiques de la bourse AMEX distribuées par [Infochimps](http://www.infochimps.com/) pour la période 1970-2010.</span><span class="sxs-lookup"><span data-stu-id="12357-235">(The CSV files are distributed together with the sample and represent an extract from AMEX Stock historical data distributed by [Infochimps](http://www.infochimps.com/) for the period 1970-2010.</span></span> <span data-ttu-id="12357-236">L’exemple lit les données du fichier CSV, convertit les enregistrements en instances de classe **Stock**, puis les sérialise en utilisant la réflexion.</span><span class="sxs-lookup"><span data-stu-id="12357-236">The sample reads CSV file data, converts the records to instances of the **Stock** class, and then serializes them by using reflection.</span></span> <span data-ttu-id="12357-237">La définition du type Stock est créée à partir d’un schéma JSON à l’aide de l’utilitaire de génération de code Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="12357-237">Stock type definition is created from a JSON schema via the Microsoft Avro Library code generation utility.</span></span>
* <span data-ttu-id="12357-238">Crée une nouvelle table externe nommée **Stocks** dans Hive et la lie aux données téléchargées à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="12357-238">Creates a new external table called **Stocks** in Hive, and links it to the data uploaded in the previous step.</span></span>
* <span data-ttu-id="12357-239">Exécute une requête avec Hive sur la table **Stocks** .</span><span class="sxs-lookup"><span data-stu-id="12357-239">Executes a query by using Hive over the **Stocks** table.</span></span>

<span data-ttu-id="12357-240">En outre, l'exemple exécute une procédure de nettoyage avant et après avoir effectué des opérations majeures.</span><span class="sxs-lookup"><span data-stu-id="12357-240">In addition, the sample performs a clean-up procedure before and after performing major operations.</span></span> <span data-ttu-id="12357-241">Pendant le nettoyage, l’ensemble des dossiers et des données d’objets blob Azure associés sont supprimés, ainsi que la table Hive.</span><span class="sxs-lookup"><span data-stu-id="12357-241">During the clean-up, all of the related Azure Blob data and folders are removed, and the Hive table is dropped.</span></span> <span data-ttu-id="12357-242">Vous pouvez également appeler la procédure de nettoyage à partir de la ligne de commande de l’exemple.</span><span class="sxs-lookup"><span data-stu-id="12357-242">You can also invoke the clean-up procedure from the sample command line.</span></span>

<span data-ttu-id="12357-243">L'exemple nécessite les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="12357-243">The sample has the following prerequisites:</span></span>

* <span data-ttu-id="12357-244">Un abonnement Microsoft Azure actif et son ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="12357-244">An active Microsoft Azure subscription and its subscription ID.</span></span>
* <span data-ttu-id="12357-245">Un certificat de gestion pour l’abonnement avec la clé privée correspondante.</span><span class="sxs-lookup"><span data-stu-id="12357-245">A management certificate for the subscription with the corresponding private key.</span></span> <span data-ttu-id="12357-246">Le certificat doit être installé dans le stockage privé de l’utilisateur actuel sur l’ordinateur utilisé pour exécuter l’exemple.</span><span class="sxs-lookup"><span data-stu-id="12357-246">The certificate should be installed in the current user private storage on the machine used to run the sample.</span></span>
* <span data-ttu-id="12357-247">Un cluster HDInsight actif.</span><span class="sxs-lookup"><span data-stu-id="12357-247">An active HDInsight cluster.</span></span>
* <span data-ttu-id="12357-248">Un compte Stockage Azure lié au cluster HDInsight par les conditions préalables précédentes, ainsi que la clé d’accès primaire ou secondaire correspondante.</span><span class="sxs-lookup"><span data-stu-id="12357-248">An Azure Storage account linked to the HDInsight cluster from the previous prerequisite, together with the corresponding primary, or secondary access key.</span></span>

<span data-ttu-id="12357-249">Toutes les informations des conditions préalables doivent être entrées dans le fichier de configuration de l’exemple avant que ce dernier ne soit exécuté.</span><span class="sxs-lookup"><span data-stu-id="12357-249">All of the information from the prerequisites should be entered to the sample configuration file before the sample is run.</span></span> <span data-ttu-id="12357-250">Il existe deux façons d'effectuer cette opération :</span><span class="sxs-lookup"><span data-stu-id="12357-250">There are two possible ways to do it:</span></span>

* <span data-ttu-id="12357-251">Modifier le fichier app.config dans le répertoire racine de l’exemple, puis créer l’exemple.</span><span class="sxs-lookup"><span data-stu-id="12357-251">Edit the app.config file in the sample root directory and then build the sample</span></span>
* <span data-ttu-id="12357-252">D’abord créer l’exemple, puis modifier AvroHDISample.exe.config dans le répertoire de build.</span><span class="sxs-lookup"><span data-stu-id="12357-252">First build the sample, and then edit AvroHDISample.exe.config in the build directory</span></span>

<span data-ttu-id="12357-253">Dans les deux cas, toutes les modifications doivent être effectuées dans la section des paramètres **<appSettings>**.</span><span class="sxs-lookup"><span data-stu-id="12357-253">In both cases, all edits should be done in the **<appSettings>** settings section.</span></span> <span data-ttu-id="12357-254">Suivez les commentaires dans le fichier.</span><span class="sxs-lookup"><span data-stu-id="12357-254">Follow the comments in the file.</span></span>
<span data-ttu-id="12357-255">L’exemple est exécuté à partir de la ligne de commande avec la commande suivante (où le fichier .zip avec l’exemple était censé avoir été extrait sous C:\AvroHDISample ; sinon, utilisez le chemin de fichier approprié) :</span><span class="sxs-lookup"><span data-stu-id="12357-255">The sample is run from the command line by executing the following command (where the .zip file with the sample was assumed to be extracted to C:\AvroHDISample; if otherwise, use the relevant file path):</span></span>

    AvroHDISample run C:\AvroHDISample\Data

<span data-ttu-id="12357-256">Pour nettoyer le cluster, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="12357-256">To clean up the cluster, run the following command:</span></span>

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
