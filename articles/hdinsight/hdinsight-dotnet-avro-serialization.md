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
# <a name="serialize-data-in-hadoop-with-hello-microsoft-avro-library"></a><span data-ttu-id="4c3de-104">Sérialisation des données dans Hadoop avec hello Microsoft Avro Library</span><span class="sxs-lookup"><span data-stu-id="4c3de-104">Serialize data in Hadoop with hello Microsoft Avro Library</span></span>

>[!NOTE]
><span data-ttu-id="4c3de-105">Hello Avro SDK n’est plus pris en charge par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4c3de-105">hello Avro SDK is no longer supported by Microsoft.</span></span> <span data-ttu-id="4c3de-106">bibliothèque de Hello est la Communauté open source pris en charge.</span><span class="sxs-lookup"><span data-stu-id="4c3de-106">hello library is open source community supported.</span></span> <span data-ttu-id="4c3de-107">sources de Hello pour la bibliothèque de hello se trouvent dans [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="4c3de-107">hello sources for hello library are located in [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

<span data-ttu-id="4c3de-108">Cette rubrique montre comment toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize objets et autres données structures dans le flux de données toopersist les toomemory, une base de données ou un fichier.</span><span class="sxs-lookup"><span data-stu-id="4c3de-108">This topic shows how toouse hello [Microsoft Avro Library](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro) tooserialize objects and other data structures into streams toopersist them toomemory, a database, or a file.</span></span> <span data-ttu-id="4c3de-109">Il montre également comment toodeserialize les objets d’origine de toorecover hello.</span><span class="sxs-lookup"><span data-stu-id="4c3de-109">It also shows how toodeserialize them toorecover hello original objects.</span></span>

[!INCLUDE [windows-only](../../includes/hdinsight-windows-only.md)]

## <a name="apache-avro"></a><span data-ttu-id="4c3de-110">Apache Avro</span><span class="sxs-lookup"><span data-stu-id="4c3de-110">Apache Avro</span></span>
<span data-ttu-id="4c3de-111">Hello <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implémente hello système de sérialisation des données Apache Avro pour l’environnement de Microsoft.NET hello.</span><span class="sxs-lookup"><span data-stu-id="4c3de-111">hello <a href="https://hadoopsdk.codeplex.com/wikipage?title=Avro%20Library" target="_blank">Microsoft Avro Library</a> implements hello Apache Avro data serialization system for hello Microsoft.NET environment.</span></span> <span data-ttu-id="4c3de-112">Apache Avro fournit un format compact d'échange des données binaires pour la sérialisation.</span><span class="sxs-lookup"><span data-stu-id="4c3de-112">Apache Avro provides a compact binary data interchange format for serialization.</span></span> <span data-ttu-id="4c3de-113">Il utilise <a href="http://www.json.org" target="_blank">JSON</a> toodefine un schéma indépendant du langage qui couvre l’interopérabilité des langages.</span><span class="sxs-lookup"><span data-stu-id="4c3de-113">It uses <a href="http://www.json.org" target="_blank">JSON</a> toodefine a language-agnostic schema that underwrites language interoperability.</span></span> <span data-ttu-id="4c3de-114">Les données sérialisées dans un langage peuvent être lues dans un autre langage.</span><span class="sxs-lookup"><span data-stu-id="4c3de-114">Data serialized in one language can be read in another.</span></span> <span data-ttu-id="4c3de-115">Les langages C, C++, C#, Java, PHP, Python et Ruby sont actuellement pris en charge.</span><span class="sxs-lookup"><span data-stu-id="4c3de-115">Currently C, C++, C#, Java, PHP, Python, and Ruby are supported.</span></span> <span data-ttu-id="4c3de-116">Vous trouverez des informations détaillées sur le format de hello Bonjour <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro spécification</a>.</span><span class="sxs-lookup"><span data-stu-id="4c3de-116">Detailed information on hello format can be found in hello <a href="http://avro.apache.org/docs/current/spec.html" target="_blank">Apache Avro Specification</a>.</span></span> 

>[!NOTE]
><span data-ttu-id="4c3de-117">Hello Microsoft Avro Library ne prend pas en charge hello procédure distante (RPC) les appels partie de cette spécification.</span><span class="sxs-lookup"><span data-stu-id="4c3de-117">hello Microsoft Avro Library does not support hello remote procedure calls (RPCs) part of this specification.</span></span>
>

<span data-ttu-id="4c3de-118">représentation sous forme de Hello sérialisée d’un objet Bonjour Avro système se compose de deux parties : schéma et la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="4c3de-118">hello serialized representation of an object in hello Avro system consists of two parts: schema and actual value.</span></span> <span data-ttu-id="4c3de-119">schéma de Avro Hello décrit le modèle de données indépendant du langage hello de données hello sérialisé avec JSON.</span><span class="sxs-lookup"><span data-stu-id="4c3de-119">hello Avro schema describes hello language-independent data model of hello serialized data with JSON.</span></span> <span data-ttu-id="4c3de-120">Il est présenté côte à côte avec une représentation binaire des données.</span><span class="sxs-lookup"><span data-stu-id="4c3de-120">It is presented side by side with a binary representation of data.</span></span> <span data-ttu-id="4c3de-121">Permet à chaque toobe objet écrit avec aucun frais généraux par valeur, effectuer sérialisation rapide et hello représentation sous forme de petits ayant schéma hello distinct à partir de la représentation binaire de hello.</span><span class="sxs-lookup"><span data-stu-id="4c3de-121">Having hello schema separate from hello binary representation permits each object toobe written with no per-value overheads, making serialization fast, and hello representation small.</span></span>

## <a name="hello-hadoop-scenario"></a><span data-ttu-id="4c3de-122">scénario de Hadoop Hello</span><span class="sxs-lookup"><span data-stu-id="4c3de-122">hello Hadoop scenario</span></span>
<span data-ttu-id="4c3de-123">format de sérialisation Apache Avro Hello est largement utilisé dans Azure HDInsight et d’autres environnements d’Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="4c3de-123">hello Apache Avro serialization format is widely used in Azure HDInsight and other Apache Hadoop environments.</span></span> <span data-ttu-id="4c3de-124">Avro fournit un moyen pratique de toorepresent des structures de données complexes au sein d’un travail Hadoop MapReduce.</span><span class="sxs-lookup"><span data-stu-id="4c3de-124">Avro provides a convenient way toorepresent complex data structures within a Hadoop MapReduce job.</span></span> <span data-ttu-id="4c3de-125">format Hello Avro fichiers (fichier conteneur d’objet Avro) a été modèle de programmation conçu toosupport hello distribué MapReduce.</span><span class="sxs-lookup"><span data-stu-id="4c3de-125">hello format of Avro files (Avro object container file) has been designed toosupport hello distributed MapReduce programming model.</span></span> <span data-ttu-id="4c3de-126">fonctionnalité de clé Hello qui permet la distribution de hello est les fichiers hello « divisible » dans les sens hello qu’un qui peut rechercher n’importe quel point dans un fichier et commence à lire à partir d’un bloc particulier.</span><span class="sxs-lookup"><span data-stu-id="4c3de-126">hello key feature that enables hello distribution is that hello files are “splittable” in hello sense that one can seek any point in a file and start reading from a particular block.</span></span>

## <a name="serialization-in-avro-library"></a><span data-ttu-id="4c3de-127">Sérialisation dans Avro Library</span><span class="sxs-lookup"><span data-stu-id="4c3de-127">Serialization in Avro Library</span></span>
<span data-ttu-id="4c3de-128">Hello bibliothèque .NET pour Avro prend en charge deux méthodes de sérialisation d’objets :</span><span class="sxs-lookup"><span data-stu-id="4c3de-128">hello .NET Library for Avro supports two ways of serializing objects:</span></span>

* <span data-ttu-id="4c3de-129">**réflexion** -schéma JSON hello pour les types de hello est généré automatiquement à partir des données de hello attributs de contrat de toobe de types .NET hello sérialisé.</span><span class="sxs-lookup"><span data-stu-id="4c3de-129">**reflection** - hello JSON schema for hello types is automatically built from hello data contract attributes of hello .NET types toobe serialized.</span></span>
* <span data-ttu-id="4c3de-130">**enregistrement générique** -JSON d’un schéma est explicitement spécifié dans un enregistrement représenté par hello [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) classe lorsque aucun des types .NET ne sont présent schéma toodescribe hello hello données toobe sérialisé.</span><span class="sxs-lookup"><span data-stu-id="4c3de-130">**generic record** - A JSON schema is explicitly specified in a record represented by hello [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) class when no .NET types are present toodescribe hello schema for hello data toobe serialized.</span></span>

<span data-ttu-id="4c3de-131">Lorsque le schéma de données hello est connu writer de hello tooboth et lecteur de flux de hello, les données de salutation peuvent être envoyées sans son schéma.</span><span class="sxs-lookup"><span data-stu-id="4c3de-131">When hello data schema is known tooboth hello writer and reader of hello stream, hello data can be sent without its schema.</span></span> <span data-ttu-id="4c3de-132">Dans le cas lorsqu’un fichier conteneur d’objet Avro est utilisé, schéma de hello est stocké dans le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="4c3de-132">In cases when an Avro object container file is used, hello schema is stored within hello file.</span></span> <span data-ttu-id="4c3de-133">Autres paramètres, tels que codec hello utilisé pour la compression de données, peuvent être spécifiés.</span><span class="sxs-lookup"><span data-stu-id="4c3de-133">Other parameters, such as hello codec used for data compression, can be specified.</span></span> <span data-ttu-id="4c3de-134">Ces scénarios sont décrites plus en détail et notamment hello, exemple de code suivant :</span><span class="sxs-lookup"><span data-stu-id="4c3de-134">These scenarios are outlined in more detail and illustrated in hello following code examples:</span></span>

## <a name="install-avro-library"></a><span data-ttu-id="4c3de-135">Installation d’Avro Library</span><span class="sxs-lookup"><span data-stu-id="4c3de-135">Install Avro Library</span></span>
<span data-ttu-id="4c3de-136">Hello Voici requis avant d’installer la bibliothèque de hello :</span><span class="sxs-lookup"><span data-stu-id="4c3de-136">hello following are required before you install hello library:</span></span>

* <span data-ttu-id="4c3de-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span><span class="sxs-lookup"><span data-stu-id="4c3de-137"><a href="http://www.microsoft.com/download/details.aspx?id=17851" target="_blank">Microsoft .NET Framework 4</a></span></span>
* <span data-ttu-id="4c3de-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (version 6.0.4 ou ultérieure)</span><span class="sxs-lookup"><span data-stu-id="4c3de-138"><a href="http://james.newtonking.com/json" target="_blank">Newtonsoft Json.NET</a> (6.0.4 or later)</span></span>

<span data-ttu-id="4c3de-139">Notez que hello Newtonsoft.Json.dll dépendance est automatiquement téléchargé avec installation hello Hello Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="4c3de-139">Note that hello Newtonsoft.Json.dll dependency is downloaded automatically with hello installation of hello Microsoft Avro Library.</span></span> <span data-ttu-id="4c3de-140">procédure de Hello est fourni dans hello suivant la section :</span><span class="sxs-lookup"><span data-stu-id="4c3de-140">hello procedure is provided in hello following section:</span></span>

<span data-ttu-id="4c3de-141">Hello Microsoft Avro Library est distribuée comme package NuGet qui peut être installé à partir de Visual Studio via hello procédure :</span><span class="sxs-lookup"><span data-stu-id="4c3de-141">hello Microsoft Avro Library is distributed as a NuGet package that can be installed from Visual Studio via hello following procedure:</span></span>

1. <span data-ttu-id="4c3de-142">Sélectionnez hello **projet** onglet -> **gérer les Packages NuGet...**</span><span class="sxs-lookup"><span data-stu-id="4c3de-142">Select hello **Project** tab -> **Manage NuGet Packages...**</span></span>
2. <span data-ttu-id="4c3de-143">Recherchez « Microsoft.Hadoop.Avro » Bonjour **recherche en ligne** boîte.</span><span class="sxs-lookup"><span data-stu-id="4c3de-143">Search for "Microsoft.Hadoop.Avro" in hello **Search Online** box.</span></span>
3. <span data-ttu-id="4c3de-144">Cliquez sur hello **installer** bouton ensuite trop**Microsoft Azure HDInsight Avro Library**.</span><span class="sxs-lookup"><span data-stu-id="4c3de-144">Click hello **Install** button next too**Microsoft Azure HDInsight Avro Library**.</span></span>

<span data-ttu-id="4c3de-145">Notez que hello Newtonsoft.Json.dll (> = 6.0.4) dépendance est également téléchargée automatiquement avec hello Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="4c3de-145">Note that hello Newtonsoft.Json.dll (>=6.0.4) dependency is also downloaded automatically with hello Microsoft Avro Library.</span></span>

<span data-ttu-id="4c3de-146">Hello code source Microsoft Avro Library est disponible à l’adresse [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span><span class="sxs-lookup"><span data-stu-id="4c3de-146">hello Microsoft Avro Library source code is available at [Github](https://github.com/Azure/azure-sdk-for-net/tree/master/src/ServiceManagement/HDInsight/Microsoft.Hadoop.Avro).</span></span>

## <a name="compile-schemas-using-avro-library"></a><span data-ttu-id="4c3de-147">Compiler des schémas à l'aide d’Avro Library</span><span class="sxs-lookup"><span data-stu-id="4c3de-147">Compile schemas using Avro Library</span></span>
<span data-ttu-id="4c3de-148">Hello Microsoft Avro Library contient une génération de code qui permet de créer des types c# automatiquement en fonction de hello précédemment défini un schéma JSON.</span><span class="sxs-lookup"><span data-stu-id="4c3de-148">hello Microsoft Avro Library contains a code generation utility that allows creating C# types automatically based on hello previously defined JSON schema.</span></span> <span data-ttu-id="4c3de-149">utilitaire de génération de code Hello n’est pas distribuée sous forme binaire exécutable, mais peut être facilement créé via hello procédure :</span><span class="sxs-lookup"><span data-stu-id="4c3de-149">hello code generation utility is not distributed as a binary executable, but can be easily built via hello following procedure:</span></span>

1. <span data-ttu-id="4c3de-150">Télécharger le fichier .zip de hello avec la version la plus récente du code source de HDInsight SDK à partir de hello <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK pour Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="4c3de-150">Download hello .zip file with hello latest version of HDInsight SDK source code from <a href="http://hadoopsdk.codeplex.com/SourceControl/latest#" target="_blank">Microsoft .NET SDK For Hadoop</a>.</span></span> <span data-ttu-id="4c3de-151">(Cliquez sur hello **télécharger** icône, pas hello **télécharge** onglet.)</span><span class="sxs-lookup"><span data-stu-id="4c3de-151">(Click hello **Download** icon, not hello **Downloads** tab.)</span></span>
2. <span data-ttu-id="4c3de-152">Extrayez hello répertoire tooa HDInsight SDK machine hello avec .NET Framework 4 installé et connecté toohello Internet pour télécharger les packages NuGet dépendance nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4c3de-152">Extract hello HDInsight SDK tooa directory on hello machine with .NET Framework 4 installed and connected toohello Internet for downloading necessary dependency NuGet packages.</span></span> <span data-ttu-id="4c3de-153">Ci-dessous, nous partons du principe que le code source de hello est tooC:\SDK extraits.</span><span class="sxs-lookup"><span data-stu-id="4c3de-153">Below, we assume that hello source code is extracted tooC:\SDK.</span></span>
3. <span data-ttu-id="4c3de-154">Atteindre le dossier toohello C:\SDK\src\Microsoft.Hadoop.Avro.Tools et exécutez build.bat.</span><span class="sxs-lookup"><span data-stu-id="4c3de-154">Go toohello folder C:\SDK\src\Microsoft.Hadoop.Avro.Tools and run build.bat.</span></span> <span data-ttu-id="4c3de-155">(hello appels de fichier MSBuild à partir de la distribution de 32 bits hello Hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="4c3de-155">(hello file calls MSBuild from hello 32-bit distribution of hello .NET Framework.</span></span> <span data-ttu-id="4c3de-156">Si vous souhaitez que la version 64 bits de hello toouse, modifiez build.bat, suivant les commentaires hello à l’intérieur du fichier de hello.) Assurez-vous que la build de hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="4c3de-156">If you would like toouse hello 64-bit version, edit build.bat, following hello comments inside hello file.) Ensure that hello build is successful.</span></span> <span data-ttu-id="4c3de-157">(Sur certains systèmes, MSBuild peut générer des avertissements.</span><span class="sxs-lookup"><span data-stu-id="4c3de-157">(On some systems, MSBuild may produce warnings.</span></span> <span data-ttu-id="4c3de-158">Ces avertissements n’affectent pas les utilitaire hello tant qu’il n’y a aucune erreur de build.)</span><span class="sxs-lookup"><span data-stu-id="4c3de-158">These warnings do not affect hello utility as long as there are no build errors.)</span></span>
4. <span data-ttu-id="4c3de-159">utilitaire de Hello compilé se trouve dans C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span><span class="sxs-lookup"><span data-stu-id="4c3de-159">hello compiled utility is located in C:\SDK\Bin\Unsigned\Release\Microsoft.Hadoop.Avro.Tools.</span></span>

<span data-ttu-id="4c3de-160">tooget familiarisé avec la syntaxe de ligne de commande hello, exécutez hello de commande suivante à partir du dossier hello où l’utilitaire de génération de code hello se trouve :`Microsoft.Hadoop.Avro.Tools help /c:codegen`</span><span class="sxs-lookup"><span data-stu-id="4c3de-160">tooget familiar with hello command-line syntax, execute hello following command from hello folder where hello code generation utility is located: `Microsoft.Hadoop.Avro.Tools help /c:codegen`</span></span>

<span data-ttu-id="4c3de-161">utilitaire de hello tootest, vous pouvez générer des classes c# à partir du fichier de schéma JSON exemple hello fourni avec le code source de hello.</span><span class="sxs-lookup"><span data-stu-id="4c3de-161">tootest hello utility, you can generate C# classes from hello sample JSON schema file provided with hello source code.</span></span> <span data-ttu-id="4c3de-162">Exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4c3de-162">Execute hello following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:

<span data-ttu-id="4c3de-163">Il est supposé tooproduce deux fichiers c# dans le répertoire en cours de hello : SensorData.cs et Location.cs.</span><span class="sxs-lookup"><span data-stu-id="4c3de-163">This is supposed tooproduce two C# files in hello current directory: SensorData.cs and Location.cs.</span></span>

<span data-ttu-id="4c3de-164">logique de hello toounderstand utilitaire de génération de code hello est à l’aide lors de la conversion de types tooC # hello JSON schéma, consultez hello fichier GenerationVerification.feature dans C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span><span class="sxs-lookup"><span data-stu-id="4c3de-164">toounderstand hello logic that hello code generation utility is using while converting hello JSON schema tooC# types, see hello file GenerationVerification.feature located in C:\SDK\src\Microsoft.Hadoop.Avro.Tools\Doc.</span></span>

<span data-ttu-id="4c3de-165">Espaces de noms sont extraites à partir d’un schéma JSON hello, à l’aide de la logique de hello décrite dans le fichier hello mentionné dans le paragraphe précédent hello.</span><span class="sxs-lookup"><span data-stu-id="4c3de-165">Namespaces are extracted from hello JSON schema, using hello logic described in hello file mentioned in hello previous paragraph.</span></span> <span data-ttu-id="4c3de-166">Espaces de noms extraites hello schéma ont priorité sur tout ce qui est fourni avec le paramètre /n hello dans la ligne de commande d’utilitaire hello.</span><span class="sxs-lookup"><span data-stu-id="4c3de-166">Namespaces extracted from hello schema take precedence over whatever is provided with hello /n parameter in hello utility command line.</span></span> <span data-ttu-id="4c3de-167">Si vous souhaitez que les espaces de noms toooverride hello dans un schéma hello, utilisez le paramètre de /nf hello.</span><span class="sxs-lookup"><span data-stu-id="4c3de-167">If you want toooverride hello namespaces contained within hello schema, use hello /nf parameter.</span></span> <span data-ttu-id="4c3de-168">Par exemple, toochange exécuter tous les espaces de noms hello SampleJSONSchema.avsc toomy.own.nspace, hello la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4c3de-168">For example, toochange all namespaces from hello SampleJSONSchema.avsc toomy.own.nspace, execute hello following command:</span></span>

    Microsoft.Hadoop.Avro.Tools codegen /i:C:\SDK\src\Microsoft.Hadoop.Avro.Tools\SampleJSON\SampleJSONSchema.avsc /o:. /nf:my.own.nspace

## <a name="about-hello-samples"></a><span data-ttu-id="4c3de-169">À propos des exemples de hello</span><span class="sxs-lookup"><span data-stu-id="4c3de-169">About hello samples</span></span>
<span data-ttu-id="4c3de-170">Six exemples fournis dans cette rubrique illustrent différents scénarios pris en charge par hello Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="4c3de-170">Six examples provided in this topic illustrate different scenarios supported by hello Microsoft Avro Library.</span></span> <span data-ttu-id="4c3de-171">Hello Microsoft Avro Library est conçue toowork avec n’importe quel flux de données.</span><span class="sxs-lookup"><span data-stu-id="4c3de-171">hello Microsoft Avro Library is designed toowork with any stream.</span></span> <span data-ttu-id="4c3de-172">Dans ces exemples, les données sont manipulées à l’aide de flux de mémoire plutôt que de flux de fichiers ou de bases de données pour des questions de simplicité et de cohérence.</span><span class="sxs-lookup"><span data-stu-id="4c3de-172">In these examples, data is manipulated via memory streams rather than file streams or databases for simplicity and consistency.</span></span> <span data-ttu-id="4c3de-173">approche Hello effectuée dans un environnement de production dépend des exigences de scénario hello, source de données et de volume, les contraintes de performances et d’autres facteurs.</span><span class="sxs-lookup"><span data-stu-id="4c3de-173">hello approach taken in a production environment depends on hello exact scenario requirements, data source and volume, performance constraints, and other factors.</span></span>

<span data-ttu-id="4c3de-174">Hello premier deux exemples indiquent comment tooserialize et désérialiser les données en mémoire tampon de flux de données à l’aide de la réflexion et enregistrements génériques.</span><span class="sxs-lookup"><span data-stu-id="4c3de-174">hello first two examples show how tooserialize and deserialize data into memory stream buffers by using reflection and generic records.</span></span> <span data-ttu-id="4c3de-175">Hello dans ces deux cas est supposé que le schéma toobe partagée entre hello lecteurs et writers hors-bande.</span><span class="sxs-lookup"><span data-stu-id="4c3de-175">hello schema in these two cases is assumed toobe shared between hello readers and writers out-of-band.</span></span>

<span data-ttu-id="4c3de-176">afficher des exemples de troisième et quatrième Hello comment tooserialize et désérialiser des données à l’aide de fichiers de conteneur objet hello Avro.</span><span class="sxs-lookup"><span data-stu-id="4c3de-176">hello third and fourth examples show how tooserialize and deserialize data by using hello Avro object container files.</span></span> <span data-ttu-id="4c3de-177">Lorsque les données stockées dans un fichier de conteneur Avro, son schéma est toujours stockée avec lui, car le schéma de hello doit être partagé pour la désérialisation.</span><span class="sxs-lookup"><span data-stu-id="4c3de-177">When data is stored in an Avro container file, its schema is always stored with it because hello schema must be shared for deserialization.</span></span>

<span data-ttu-id="4c3de-178">Hello contenant par exemple hello quatre premiers exemples peuvent être téléchargés à partir de hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">exemples de code Azure</a> site.</span><span class="sxs-lookup"><span data-stu-id="4c3de-178">hello sample containing hello first four examples can be downloaded from hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-86055923" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="4c3de-179">Hello cinquième exemple montre comment toouse un codec de compression personnalisé pour Avro les fichiers de conteneur d’objets.</span><span class="sxs-lookup"><span data-stu-id="4c3de-179">hello fifth example shows how toouse a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="4c3de-180">Un exemple contenant du code de hello pour cet exemple peut être téléchargé à partir de hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">exemples de code Azure</a> site.</span><span class="sxs-lookup"><span data-stu-id="4c3de-180">A sample containing hello code for this example can be downloaded from hello <a href="http://code.msdn.microsoft.com/Serialize-data-with-the-67159111" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="4c3de-181">Hello sixième montre comment toouse Avro sérialisation tooupload données tooAzure stockage d’objets Blob et puis les analyser à l’aide de la ruche avec un cluster HDInsight (Hadoop).</span><span class="sxs-lookup"><span data-stu-id="4c3de-181">hello sixth sample shows how toouse Avro serialization tooupload data tooAzure Blob storage and then analyze it by using Hive with an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="4c3de-182">Il peut être téléchargé à partir de hello <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">exemples de code Azure</a> site.</span><span class="sxs-lookup"><span data-stu-id="4c3de-182">It can be downloaded from hello <a href="https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3" target="_blank">Azure code samples</a> site.</span></span>

<span data-ttu-id="4c3de-183">Voici des liens toohello six échantillons présentés dans la rubrique de hello :</span><span class="sxs-lookup"><span data-stu-id="4c3de-183">Here are links toohello six samples discussed in hello topic:</span></span>

* <span data-ttu-id="4c3de-184"><a href="#Scenario1">**Sérialisation avec réflexion** </a> -toobe types sérialisé sur le schéma JSON hello est généré automatiquement à partir des données de hello attributs de contrat.</span><span class="sxs-lookup"><span data-stu-id="4c3de-184"><a href="#Scenario1">**Serialization with reflection**</a> - hello JSON schema for types toobe serialized is automatically built from hello data contract attributes.</span></span>
* <span data-ttu-id="4c3de-185"><a href="#Scenario2">**Sérialisation avec enregistrement générique** </a> -hello JSON schéma est explicitement spécifié dans un enregistrement lorsqu’aucun type .NET n’est disponible pour la réflexion.</span><span class="sxs-lookup"><span data-stu-id="4c3de-185"><a href="#Scenario2">**Serialization with generic record**</a> - hello JSON schema is explicitly specified in a record when no .NET type is available for reflection.</span></span>
* <span data-ttu-id="4c3de-186"><a href="#Scenario3">**Sérialisation à l’aide des fichiers de conteneur d’objets avec la réflexion** </a> -hello JSON schéma est automatiquement créé et partagé avec des données via un fichier conteneur d’objet Avro hello sérialisé.</span><span class="sxs-lookup"><span data-stu-id="4c3de-186"><a href="#Scenario3">**Serialization using object container files with reflection**</a> - hello JSON schema is automatically built and shared together with hello serialized data via an Avro object container file.</span></span>
* <span data-ttu-id="4c3de-187"><a href="#Scenario4">**Sérialisation à l’aide des fichiers de conteneur d’objets avec enregistrement générique** </a> -schéma JSON hello est explicitement spécifié avant la sérialisation de hello et partagé avec des données via un fichier conteneur d’objet Avro hello.</span><span class="sxs-lookup"><span data-stu-id="4c3de-187"><a href="#Scenario4">**Serialization using object container files with generic record**</a> - hello JSON schema is explicitly specified before hello serialization and shared together with hello data via an Avro object container file.</span></span>
* <span data-ttu-id="4c3de-188"><a href="#Scenario5">**Sérialisation à l’aide des fichiers de conteneur d’objets avec un codec de compression personnalisé** </a> -hello montre comment toocreate un Avro de l’objet fichier conteneur avec une implémentation .NET personnalisé du codec de compression de données hello Deflate.</span><span class="sxs-lookup"><span data-stu-id="4c3de-188"><a href="#Scenario5">**Serialization using object container files with a custom compression codec**</a> - hello example shows how toocreate an Avro object container file with a customized .NET implementation of hello Deflate data compression codec.</span></span>
* <span data-ttu-id="4c3de-189"><a href="#Scenario6">**À l’aide des données de tooupload Avro pourquoi le service Microsoft Azure HDInsight** </a> -hello illustre comment Avro sérialisation interagit avec hello service HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4c3de-189"><a href="#Scenario6">**Using Avro tooupload data for hello Microsoft Azure HDInsight service**</a> - hello example illustrates how Avro serialization interacts with hello HDInsight service.</span></span> <span data-ttu-id="4c3de-190">Un active Azure abonnement et accès tooan Azure HDInsight de cluster requis toorun cet exemple.</span><span class="sxs-lookup"><span data-stu-id="4c3de-190">An active Azure subscription and access tooan Azure HDInsight cluster are required toorun this example.</span></span>

## <span data-ttu-id="4c3de-191"><a name="Scenario1"></a>Exemple 1 : sérialisation avec réflexion</span><span class="sxs-lookup"><span data-stu-id="4c3de-191"><a name="Scenario1"></a>Sample 1: Serialization with reflection</span></span>
<span data-ttu-id="4c3de-192">schéma JSON Hello pour les types de hello peut être automatiquement créé par hello Microsoft Avro Library via la réflexion à partir des données de hello attributs de contrat de toobe hello c# objets sérialisés.</span><span class="sxs-lookup"><span data-stu-id="4c3de-192">hello JSON schema for hello types can be automatically built by hello Microsoft Avro Library via reflection from hello data contract attributes of hello C# objects toobe serialized.</span></span> <span data-ttu-id="4c3de-193">Hello Microsoft Avro Library crée un [ **IAvroSeralizer<T>**  ](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify hello champs toobe sérialisé.</span><span class="sxs-lookup"><span data-stu-id="4c3de-193">hello Microsoft Avro Library creates an [**IAvroSeralizer<T>**](http://msdn.microsoft.com/library/dn627341.aspx) tooidentify hello fields toobe serialized.</span></span>

<span data-ttu-id="4c3de-194">Dans cet exemple, objets (un **SensorData** classe avec un membre **emplacement** struct) sont des flux de mémoire tooa sérialisé, et ce flux est ensuite désérialisé.</span><span class="sxs-lookup"><span data-stu-id="4c3de-194">In this example, objects (a **SensorData** class with a member **Location** struct) are serialized tooa memory stream, and this stream is in turn deserialized.</span></span> <span data-ttu-id="4c3de-195">Hello résultat est ensuite comparé toohello initiale d’instance tooconfirm que hello **SensorData** objet récupéré est identique toohello d’origine.</span><span class="sxs-lookup"><span data-stu-id="4c3de-195">hello result is then compared toohello initial instance tooconfirm that hello **SensorData** object recovered is identical toohello original.</span></span>

<span data-ttu-id="4c3de-196">schéma Hello dans cet exemple est supposé toobe partagée entre hello lecteurs et writers, le format de conteneur objet hello Avro n’est pas requis.</span><span class="sxs-lookup"><span data-stu-id="4c3de-196">hello schema in this example is assumed toobe shared between hello readers and writers, so hello Avro object container format is not required.</span></span> <span data-ttu-id="4c3de-197">Pour obtenir un exemple de procédure tooserialize et désérialiser des données dans les mémoires tampons en utilisant la réflexion avec le format de conteneur d’objet hello lorsque le schéma de hello doit être partagé avec les données de salutation, consultez <a href="#Scenario3">sérialisation à l’aide des fichiers de conteneur d’objets avec la réflexion</a>.</span><span class="sxs-lookup"><span data-stu-id="4c3de-197">For an example of how tooserialize and deserialize data into memory buffers by using reflection with hello object container format when hello schema must be shared with hello data, see <a href="#Scenario3">Serialization using object container files with reflection</a>.</span></span>

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


## <a name="sample-2-serialization-with-a-generic-record"></a><span data-ttu-id="4c3de-198">Exemple 2 : sérialisation avec enregistrement générique</span><span class="sxs-lookup"><span data-stu-id="4c3de-198">Sample 2: Serialization with a generic record</span></span>
<span data-ttu-id="4c3de-199">Un schéma JSON peut être explicitement spécifié dans un enregistrement générique quand la réflexion ne peut pas être utilisée, car il est impossible de représenter les données de salutation via les classes .NET avec un contrat de données.</span><span class="sxs-lookup"><span data-stu-id="4c3de-199">A JSON schema can be explicitly specified in a generic record when reflection cannot be used because hello data cannot be represented via .NET classes with a data contract.</span></span> <span data-ttu-id="4c3de-200">Cette méthode est plus lente que celle qui utilise la réflexion.</span><span class="sxs-lookup"><span data-stu-id="4c3de-200">This method is slower than using reflection.</span></span> <span data-ttu-id="4c3de-201">Dans ce cas, schéma hello pour les données de salutation peut également être dynamique, autrement dit, ne pas connu au moment de la compilation.</span><span class="sxs-lookup"><span data-stu-id="4c3de-201">In such cases, hello schema for hello data may also be dynamic, that is, not known at compile time.</span></span> <span data-ttu-id="4c3de-202">Données représentées en tant que valeurs séparées par des virgules (CSV) des fichiers dont le schéma est inconnu jusqu'à ce qu’il est transformé le format Avro toohello au moment de l’exécution est un exemple de ce type de scénario dynamique.</span><span class="sxs-lookup"><span data-stu-id="4c3de-202">Data represented as comma-separated values (CSV) files whose schema is unknown until it is transformed toohello Avro format at run time is an example of this sort of dynamic scenario.</span></span>

<span data-ttu-id="4c3de-203">Cet exemple montre comment toocreate et utiliser une [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly spécifier un schéma JSON, comment toopopulate avec hello et comment puis tooserialize et de le désérialiser.</span><span class="sxs-lookup"><span data-stu-id="4c3de-203">This example shows how toocreate and use an [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) tooexplicitly specify a JSON schema, how toopopulate it with hello data, and then how tooserialize and deserialize it.</span></span> <span data-ttu-id="4c3de-204">résultat de Hello est ensuite comparé toohello initiale d’instance tooconfirm qui hello enregistrement récupéré est identique toohello d’origine.</span><span class="sxs-lookup"><span data-stu-id="4c3de-204">hello result is then compared toohello initial instance tooconfirm that hello record recovered is identical toohello original.</span></span>

<span data-ttu-id="4c3de-205">schéma Hello dans cet exemple est supposé toobe partagée entre hello lecteurs et writers, le format de conteneur objet hello Avro n’est pas requis.</span><span class="sxs-lookup"><span data-stu-id="4c3de-205">hello schema in this example is assumed toobe shared between hello readers and writers, so hello Avro object container format is not required.</span></span> <span data-ttu-id="4c3de-206">Pour obtenir un exemple de procédure tooserialize et désérialiser des données dans les mémoires tampons à l’aide d’un enregistrement générique avec le format de conteneur d’objet hello lorsque le schéma de hello doit être incluse avec les données sérialisée de hello, consultez hello <a href="#Scenario4">sérialisation à l’aide du conteneur d’objets fichiers avec enregistrement générique</a> exemple.</span><span class="sxs-lookup"><span data-stu-id="4c3de-206">For an example of how tooserialize and deserialize data into memory buffers by using a generic record with hello object container format when hello schema must be included with hello serialized data, see hello <a href="#Scenario4">Serialization using object container files with generic record</a> example.</span></span>

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


## <a name="sample-3-serialization-using-object-container-files-and-serialization-with-reflection"></a><span data-ttu-id="4c3de-207">Exemple 3 : sérialisation à l'aide de fichiers conteneurs d'objets et sérialisation avec réflexion</span><span class="sxs-lookup"><span data-stu-id="4c3de-207">Sample 3: Serialization using object container files and serialization with reflection</span></span>
<span data-ttu-id="4c3de-208">Cet exemple est un scénario toohello similaire Bonjour <a href="#Scenario1"> premier exemple</a>, où les schémas hello sont implicitement spécifié avec la réflexion.</span><span class="sxs-lookup"><span data-stu-id="4c3de-208">This example is similar toohello scenario in hello <a href="#Scenario1"> first example</a>, where hello schema is implicitly specified with reflection.</span></span> <span data-ttu-id="4c3de-209">Hello différence est qu’ici, schéma de hello n’est pas supposé que toobe connu du lecteur toohello qui désérialise ce paquet.</span><span class="sxs-lookup"><span data-stu-id="4c3de-209">hello difference is that here, hello schema is not assumed toobe known toohello reader that deserializes it.</span></span> <span data-ttu-id="4c3de-210">Hello **SensorData** toobe d’objets sérialisés et leur schéma spécifié de manière implicite sont stockées dans un fichier conteneur d’objet Avro représenté par hello [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="4c3de-210">hello **SensorData** objects toobe serialized and their implicitly specified schema are stored in an Avro object container file represented by hello [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span>

<span data-ttu-id="4c3de-211">les données de salutation sont sérialisées dans cet exemple par [ **SequentialWriter<SensorData>**  ](http://msdn.microsoft.com/library/dn627340.aspx) et désérialisés avec [ **SequentialReader<SensorData>** ](http://msdn.microsoft.com/library/dn627340.aspx).</span><span class="sxs-lookup"><span data-stu-id="4c3de-211">hello data is serialized in this example with [**SequentialWriter<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx) and deserialized with [**SequentialReader<SensorData>**](http://msdn.microsoft.com/library/dn627340.aspx).</span></span> <span data-ttu-id="4c3de-212">résultat de Hello est puis toohello comparés initial d’instances tooensure identité.</span><span class="sxs-lookup"><span data-stu-id="4c3de-212">hello result then is compared toohello initial instances tooensure identity.</span></span>

<span data-ttu-id="4c3de-213">Bonjour Bonjour d’objet de données du fichier conteneur est compressé par défaut de hello [ **Deflate** ] [ deflate-100] codec de compression à partir de .NET Framework 4.</span><span class="sxs-lookup"><span data-stu-id="4c3de-213">hello data in hello object container file is compressed via hello default [**Deflate**][deflate-100] compression codec from .NET Framework 4.</span></span> <span data-ttu-id="4c3de-214">Consultez hello <a href="#Scenario5"> cinquième exemple</a> dans cette rubrique toolearn comment toouse une version plus récente et supérieure de hello [ **Deflate** ] [ deflate-110] compression codec disponible dans .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="4c3de-214">See hello <a href="#Scenario5"> fifth example</a> in this topic toolearn how toouse a more recent and superior version of hello [**Deflate**][deflate-110] compression codec available in .NET Framework 4.5.</span></span>

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


## <a name="sample-4-serialization-using-object-container-files-and-serialization-with-generic-record"></a><span data-ttu-id="4c3de-215">Exemple 4 : sérialisation à l'aide de fichiers conteneurs d'objets et sérialisation avec enregistrement générique</span><span class="sxs-lookup"><span data-stu-id="4c3de-215">Sample 4: Serialization using object container files and serialization with generic record</span></span>
<span data-ttu-id="4c3de-216">Cet exemple est un scénario toohello similaire Bonjour <a href="#Scenario2"> deuxième exemple</a>, où les schémas hello sont spécifié explicitement avec JSON.</span><span class="sxs-lookup"><span data-stu-id="4c3de-216">This example is similar toohello scenario in hello <a href="#Scenario2"> second example</a>, where hello schema is explicitly specified with JSON.</span></span> <span data-ttu-id="4c3de-217">Hello différence est qu’ici, schéma de hello n’est pas supposé que toobe connu du lecteur toohello qui désérialise ce paquet.</span><span class="sxs-lookup"><span data-stu-id="4c3de-217">hello difference is that here, hello schema is not assumed toobe known toohello reader that deserializes it.</span></span>

<span data-ttu-id="4c3de-218">jeu de données de test Hello sont collecté dans une liste de [ **AvroRecord** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objets via le schéma défini explicitement JSON et stockées dans un fichier conteneur d’objet représenté par hello [ **AvroContainer** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="4c3de-218">hello test data set is collected into a list of [**AvroRecord**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.avrorecord.aspx) objects via an explicitly defined JSON schema and then stored in an object container file represented by hello [**AvroContainer**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.avrocontainer.aspx) class.</span></span> <span data-ttu-id="4c3de-219">Ce fichier conteneur crée un writer qui est des données hello tooserialize utilisés, non compressées, flux de mémoire tooa qui est ensuite enregistrée tooa fichier.</span><span class="sxs-lookup"><span data-stu-id="4c3de-219">This container file creates a writer that is used tooserialize hello data, uncompressed, tooa memory stream that is then saved tooa file.</span></span> <span data-ttu-id="4c3de-220">Hello [ **Codec.Null** ](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) paramètre utilisé pour la création du lecteur de hello Spécifie que ces données ne sont pas compressées.</span><span class="sxs-lookup"><span data-stu-id="4c3de-220">hello [**Codec.Null**](http://msdn.microsoft.com/library/microsoft.hadoop.avro.container.codec.null.aspx) parameter used for creating hello reader specifies that this data is not compressed.</span></span>

<span data-ttu-id="4c3de-221">les données de salutation sont ensuite lire hello du fichier et désérialisées dans une collection d’objets.</span><span class="sxs-lookup"><span data-stu-id="4c3de-221">hello data is then read from hello file and deserialized into a collection of objects.</span></span> <span data-ttu-id="4c3de-222">Cette collection est comparé toohello la liste initiale de tooconfirm d’enregistrements Avro qu’ils sont identiques.</span><span class="sxs-lookup"><span data-stu-id="4c3de-222">This collection is compared toohello initial list of Avro records tooconfirm that they are identical.</span></span>

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




## <a name="sample-5-serialization-using-object-container-files-with-a-custom-compression-codec"></a><span data-ttu-id="4c3de-223">Exemple 5: sérialisation à l'aide de fichiers conteneurs d'objets avec un codec de compression personnalisé</span><span class="sxs-lookup"><span data-stu-id="4c3de-223">Sample 5: Serialization using object container files with a custom compression codec</span></span>
<span data-ttu-id="4c3de-224">Hello cinquième exemple montre comment toouse un codec de compression personnalisé pour Avro les fichiers de conteneur d’objets.</span><span class="sxs-lookup"><span data-stu-id="4c3de-224">hello fifth example shows how toouse a custom compression codec for Avro object container files.</span></span> <span data-ttu-id="4c3de-225">Un exemple contenant du code de hello pour cet exemple peut être téléchargé à partir de hello [exemples de code Azure](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span><span class="sxs-lookup"><span data-stu-id="4c3de-225">A sample containing hello code for this example can be downloaded from hello [Azure code samples](http://code.msdn.microsoft.com/Serialize-data-with-the-67159111) site.</span></span>

<span data-ttu-id="4c3de-226">Hello [Avro spécification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) permet l’utilisation d’un codec de compression facultatif (en outre trop**Null** et **Deflate** par défaut).</span><span class="sxs-lookup"><span data-stu-id="4c3de-226">hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#Required+Codecs) allows usage of an optional compression codec (in addition too**Null** and **Deflate** defaults).</span></span> <span data-ttu-id="4c3de-227">Cet exemple n’implémente pas un nouveau codec telles que Snappy (indiqué en tant qu’un codec facultatif pris en charge dans hello [Avro spécification](http://avro.apache.org/docs/current/spec.html#snappy)).</span><span class="sxs-lookup"><span data-stu-id="4c3de-227">This example is not implementing a new codec such as Snappy (mentioned as a supported optional codec in hello [Avro Specification](http://avro.apache.org/docs/current/spec.html#snappy)).</span></span> <span data-ttu-id="4c3de-228">Il montre comment toouse hello implémentation .NET Framework 4.5 de hello [ **Deflate** ] [ deflate-110] codec, qui offre un meilleur algorithme de compression en fonction de hello [zlib](http://zlib.net/) bibliothèque de compression à la version de .NET Framework 4 hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="4c3de-228">It shows how toouse hello .NET Framework 4.5 implementation of hello [**Deflate**][deflate-110] codec, which provides a better compression algorithm based on hello [zlib](http://zlib.net/) compression library than hello default .NET Framework 4 version.</span></span>

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

## <a name="sample-6-using-avro-tooupload-data-for-hello-microsoft-azure-hdinsight-service"></a><span data-ttu-id="4c3de-229">Exemple 6 : À l’aide de données de tooupload Avro pourquoi le service Microsoft Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4c3de-229">Sample 6: Using Avro tooupload data for hello Microsoft Azure HDInsight service</span></span>
<span data-ttu-id="4c3de-230">Hello sixième illustre certaines toointeracting de programmation techniques associées avec le service Azure HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="4c3de-230">hello sixth example illustrates some programming techniques related toointeracting with hello Azure HDInsight service.</span></span> <span data-ttu-id="4c3de-231">Un exemple contenant du code de hello pour cet exemple peut être téléchargé à partir de hello [exemples de code Azure](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span><span class="sxs-lookup"><span data-stu-id="4c3de-231">A sample containing hello code for this example can be downloaded from hello [Azure code samples](https://code.msdn.microsoft.com/Using-Avro-to-upload-data-ae81b1e3) site.</span></span>

<span data-ttu-id="4c3de-232">exemple Hello hello tâche suivantes :</span><span class="sxs-lookup"><span data-stu-id="4c3de-232">hello sample does hello following tasks:</span></span>

* <span data-ttu-id="4c3de-233">Se connecte tooan cluster du service HDInsight existant.</span><span class="sxs-lookup"><span data-stu-id="4c3de-233">Connects tooan existing HDInsight service cluster.</span></span>
* <span data-ttu-id="4c3de-234">Sérialise plusieurs fichiers CSV et télécharge le stockage d’objets Blob tooAzure hello résultat.</span><span class="sxs-lookup"><span data-stu-id="4c3de-234">Serializes several CSV files and uploads hello result tooAzure Blob storage.</span></span> <span data-ttu-id="4c3de-235">(fichiers CSV de hello sont distribuées avec l’exemple hello et représentent un extrait des données historiques de Stock de l’American Express distribués par [Infochimps](http://www.infochimps.com/) pendant hello 1970-2010.</span><span class="sxs-lookup"><span data-stu-id="4c3de-235">(hello CSV files are distributed together with hello sample and represent an extract from AMEX Stock historical data distributed by [Infochimps](http://www.infochimps.com/) for hello period 1970-2010.</span></span> <span data-ttu-id="4c3de-236">exemple Hello lit les données de fichier CSV, convertit hello tooinstances des enregistrements de hello **Stock** de classe et les sérialise ensuite en utilisant la réflexion.</span><span class="sxs-lookup"><span data-stu-id="4c3de-236">hello sample reads CSV file data, converts hello records tooinstances of hello **Stock** class, and then serializes them by using reflection.</span></span> <span data-ttu-id="4c3de-237">Définition du type de stock est créée à partir d’un schéma JSON via hello utilitaire de génération de code Microsoft Avro Library.</span><span class="sxs-lookup"><span data-stu-id="4c3de-237">Stock type definition is created from a JSON schema via hello Microsoft Avro Library code generation utility.</span></span>
* <span data-ttu-id="4c3de-238">Crée une table externe appelée **Stocks** dans la ruche et lie les données toohello téléchargé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="4c3de-238">Creates a new external table called **Stocks** in Hive, and links it toohello data uploaded in hello previous step.</span></span>
* <span data-ttu-id="4c3de-239">Exécute une requête à l’aide de la ruche sur hello **Stocks** table.</span><span class="sxs-lookup"><span data-stu-id="4c3de-239">Executes a query by using Hive over hello **Stocks** table.</span></span>

<span data-ttu-id="4c3de-240">En outre, exemple hello effectue une procédure de nettoyage avant et après avoir effectué les opérations principales.</span><span class="sxs-lookup"><span data-stu-id="4c3de-240">In addition, hello sample performs a clean-up procedure before and after performing major operations.</span></span> <span data-ttu-id="4c3de-241">Au cours de hello nettoyage, toutes hello liées dossiers et objets Blob Azure sont supprimés et hello ruche table est supprimée.</span><span class="sxs-lookup"><span data-stu-id="4c3de-241">During hello clean-up, all of hello related Azure Blob data and folders are removed, and hello Hive table is dropped.</span></span> <span data-ttu-id="4c3de-242">Vous pouvez également appeler la procédure de nettoyage hello à partir de la ligne de commande exemple hello.</span><span class="sxs-lookup"><span data-stu-id="4c3de-242">You can also invoke hello clean-up procedure from hello sample command line.</span></span>

<span data-ttu-id="4c3de-243">exemple Hello a hello suivant des conditions préalables :</span><span class="sxs-lookup"><span data-stu-id="4c3de-243">hello sample has hello following prerequisites:</span></span>

* <span data-ttu-id="4c3de-244">Un abonnement Microsoft Azure actif et son ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="4c3de-244">An active Microsoft Azure subscription and its subscription ID.</span></span>
* <span data-ttu-id="4c3de-245">Un certificat de gestion pour l’abonnement hello avec la clé privée correspondante de hello.</span><span class="sxs-lookup"><span data-stu-id="4c3de-245">A management certificate for hello subscription with hello corresponding private key.</span></span> <span data-ttu-id="4c3de-246">certificat de Hello doit être installé dans hello actuel utilisateur stockage privé sur toorun hello exemple hello machine utilisée.</span><span class="sxs-lookup"><span data-stu-id="4c3de-246">hello certificate should be installed in hello current user private storage on hello machine used toorun hello sample.</span></span>
* <span data-ttu-id="4c3de-247">Un cluster HDInsight actif.</span><span class="sxs-lookup"><span data-stu-id="4c3de-247">An active HDInsight cluster.</span></span>
* <span data-ttu-id="4c3de-248">Un compte Azure Storage lié de cluster HDInsight de toohello à partir de la condition préalable précédente hello, ainsi que de la clé d’accès primaire ou secondaire correspondante hello.</span><span class="sxs-lookup"><span data-stu-id="4c3de-248">An Azure Storage account linked toohello HDInsight cluster from hello previous prerequisite, together with hello corresponding primary, or secondary access key.</span></span>

<span data-ttu-id="4c3de-249">Toutes les informations de hello à la configuration requise de hello doivent être entré toohello exemple de fichier de configuration avant l’exécution d’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="4c3de-249">All of hello information from hello prerequisites should be entered toohello sample configuration file before hello sample is run.</span></span> <span data-ttu-id="4c3de-250">Il existe deux façons possibles toodo il :</span><span class="sxs-lookup"><span data-stu-id="4c3de-250">There are two possible ways toodo it:</span></span>

* <span data-ttu-id="4c3de-251">Modifier le fichier app.config de hello dans le répertoire racine de l’exemple hello et générer des exemple hello</span><span class="sxs-lookup"><span data-stu-id="4c3de-251">Edit hello app.config file in hello sample root directory and then build hello sample</span></span>
* <span data-ttu-id="4c3de-252">Tout d’abord créer exemple hello et modifiez AvroHDISample.exe.config dans le répertoire de build hello</span><span class="sxs-lookup"><span data-stu-id="4c3de-252">First build hello sample, and then edit AvroHDISample.exe.config in hello build directory</span></span>

<span data-ttu-id="4c3de-253">Dans les deux cas, toutes les modifications doivent être effectuées dans hello  **<appSettings>**  section de paramètres.</span><span class="sxs-lookup"><span data-stu-id="4c3de-253">In both cases, all edits should be done in hello **<appSettings>** settings section.</span></span> <span data-ttu-id="4c3de-254">Suivez les commentaires du fichier hello hello.</span><span class="sxs-lookup"><span data-stu-id="4c3de-254">Follow hello comments in hello file.</span></span>
<span data-ttu-id="4c3de-255">Hello exemple est exécuté à partir de la ligne de commande hello en exécutant la commande suivante (où hello fichier .zip avec l’exemple hello a été considérée comme toobe extrait tooC:\AvroHDISample ; si dans le cas contraire, utilisez hello pertinentes du fichier chemin d’accès) de hello :</span><span class="sxs-lookup"><span data-stu-id="4c3de-255">hello sample is run from hello command line by executing hello following command (where hello .zip file with hello sample was assumed toobe extracted tooC:\AvroHDISample; if otherwise, use hello relevant file path):</span></span>

    AvroHDISample run C:\AvroHDISample\Data

<span data-ttu-id="4c3de-256">tooclean cluster hello, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4c3de-256">tooclean up hello cluster, run hello following command:</span></span>

    AvroHDISample clean

[deflate-100]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.100).aspx
[deflate-110]: http://msdn.microsoft.com/library/system.io.compression.deflatestream(v=vs.110).aspx
