---
title: "Formats de fichiers et de compression pris en charge dans Azure Data Factory | Microsoft Docs"
description: "Découvrez plus d’informations sur les formats de fichier pris en charge par Azure Data Factory."
keywords: "données d’objets blob, copie d’objet blob azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: f4746e0dd249e417b8077a9bc733d2886daafdf2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a><span data-ttu-id="46d1d-104">Formats de fichiers et de compression pris en charge dans Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="46d1d-104">File and compression formats supported by Azure Data Factory</span></span>
<span data-ttu-id="46d1d-105">*Cette rubrique s’applique aux connecteurs suivants : [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Blob Azure](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [Système de fichiers](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md) et [SFTP](data-factory-sftp-connector.md).*</span><span class="sxs-lookup"><span data-stu-id="46d1d-105">*This topic applies to the following connectors: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [Azure Blob](data-factory-azure-blob-connector.md), [Azure Data Lake Store](data-factory-azure-datalake-connector.md), [File System](data-factory-onprem-file-system-connector.md), [FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), and [SFTP](data-factory-sftp-connector.md).*</span></span>

<span data-ttu-id="46d1d-106">Azure Data Factory prend en charge les types de format de fichier suivants :</span><span class="sxs-lookup"><span data-stu-id="46d1d-106">Azure Data Factory supports the following file format types:</span></span>

* [<span data-ttu-id="46d1d-107">Format Texte</span><span class="sxs-lookup"><span data-stu-id="46d1d-107">Text format</span></span>](#text-format)
* [<span data-ttu-id="46d1d-108">Format JSON</span><span class="sxs-lookup"><span data-stu-id="46d1d-108">JSON format</span></span>](#json-format)
* [<span data-ttu-id="46d1d-109">Format Avro</span><span class="sxs-lookup"><span data-stu-id="46d1d-109">Avro format</span></span>](#avro-format)
* [<span data-ttu-id="46d1d-110">Format ORC</span><span class="sxs-lookup"><span data-stu-id="46d1d-110">ORC format</span></span>](#orc-format)
* [<span data-ttu-id="46d1d-111">Format Parquet</span><span class="sxs-lookup"><span data-stu-id="46d1d-111">Parquet format</span></span>](#parquet-format)

## <a name="text-format"></a><span data-ttu-id="46d1d-112">Format Texte</span><span class="sxs-lookup"><span data-stu-id="46d1d-112">Text format</span></span>
<span data-ttu-id="46d1d-113">Si vous souhaitez lire ou écrire des données dans un fichier texte, définissez la propriété `type` dans la section `format` du jeu de données sur **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="46d1d-113">If you want to read from a text file or write to a text file, set the `type` property in the `format` section of the dataset to **TextFormat**.</span></span> <span data-ttu-id="46d1d-114">Vous pouvez également spécifier les propriétés **facultatives** suivantes, dans la section `format`.</span><span class="sxs-lookup"><span data-stu-id="46d1d-114">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="46d1d-115">Consultez la section [Exemple pour TextFormat](#textformat-example) pour en savoir plus sur la méthode de configuration à suivre.</span><span class="sxs-lookup"><span data-stu-id="46d1d-115">See [TextFormat example](#textformat-example) section on how to configure.</span></span>

| <span data-ttu-id="46d1d-116">Propriété</span><span class="sxs-lookup"><span data-stu-id="46d1d-116">Property</span></span> | <span data-ttu-id="46d1d-117">Description</span><span class="sxs-lookup"><span data-stu-id="46d1d-117">Description</span></span> | <span data-ttu-id="46d1d-118">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="46d1d-118">Allowed values</span></span> | <span data-ttu-id="46d1d-119">Requis</span><span class="sxs-lookup"><span data-stu-id="46d1d-119">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="46d1d-120">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="46d1d-120">columnDelimiter</span></span> |<span data-ttu-id="46d1d-121">Caractère utilisé pour séparer les colonnes dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="46d1d-121">The character used to separate columns in a file.</span></span> <span data-ttu-id="46d1d-122">Vous pouvez envisager d’utiliser un caractère non imprimable rare qui n’existe probablement pas dans vos données.</span><span class="sxs-lookup"><span data-stu-id="46d1d-122">You can consider to use a rare unprintable char that may not likely exists in your data.</span></span> <span data-ttu-id="46d1d-123">Par exemple, spécifiez « \u0001 », qui représente le début d’en-tête (SOH).</span><span class="sxs-lookup"><span data-stu-id="46d1d-123">For example, specify "\u0001", which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="46d1d-124">Un seul caractère est autorisé.</span><span class="sxs-lookup"><span data-stu-id="46d1d-124">Only one character is allowed.</span></span> <span data-ttu-id="46d1d-125">La valeur **par défaut** est la **virgule (,)**.</span><span class="sxs-lookup"><span data-stu-id="46d1d-125">The **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="46d1d-126">Pour utiliser un caractère Unicode, reportez-vous à l’article sur les [caractères Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) pour obtenir le code correspondant.</span><span class="sxs-lookup"><span data-stu-id="46d1d-126">To use a Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span></span> |<span data-ttu-id="46d1d-127">Non</span><span class="sxs-lookup"><span data-stu-id="46d1d-127">No</span></span> |
| <span data-ttu-id="46d1d-128">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="46d1d-128">rowDelimiter</span></span> |<span data-ttu-id="46d1d-129">Caractère utilisé pour séparer les lignes dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="46d1d-129">The character used to separate rows in a file.</span></span> |<span data-ttu-id="46d1d-130">Un seul caractère est autorisé.</span><span class="sxs-lookup"><span data-stu-id="46d1d-130">Only one character is allowed.</span></span> <span data-ttu-id="46d1d-131">La valeur **par défaut** est l’une des suivantes : **[« \r\n », « \r », « \n »]** en lecture et **« \r\n »** en écriture.</span><span class="sxs-lookup"><span data-stu-id="46d1d-131">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="46d1d-132">Non</span><span class="sxs-lookup"><span data-stu-id="46d1d-132">No</span></span> |
| <span data-ttu-id="46d1d-133">escapeChar</span><span class="sxs-lookup"><span data-stu-id="46d1d-133">escapeChar</span></span> |<span data-ttu-id="46d1d-134">Caractère spécial utilisé pour échapper au délimiteur de colonnes dans le contenu du fichier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="46d1d-134">The special character used to escape a column delimiter in the content of input file.</span></span> <br/><br/><span data-ttu-id="46d1d-135">Vous ne pouvez pas spécifier à la fois escapeChar et quoteChar pour une table.</span><span class="sxs-lookup"><span data-stu-id="46d1d-135">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="46d1d-136">Un seul caractère est autorisé.</span><span class="sxs-lookup"><span data-stu-id="46d1d-136">Only one character is allowed.</span></span> <span data-ttu-id="46d1d-137">Aucune valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="46d1d-137">No default value.</span></span> <br/><br/><span data-ttu-id="46d1d-138">Par exemple, si vous avez une virgule (,) comme séparateur de colonnes mais que vous voulez avoir le caractère virgule dans le texte (par exemple : « Hello, world »), vous pouvez définir « $ » comme caractère d’échappement et utiliser la chaîne « Hello$, world » dans la source.</span><span class="sxs-lookup"><span data-stu-id="46d1d-138">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span></span> |<span data-ttu-id="46d1d-139">Non</span><span class="sxs-lookup"><span data-stu-id="46d1d-139">No</span></span> |
| <span data-ttu-id="46d1d-140">quoteChar</span><span class="sxs-lookup"><span data-stu-id="46d1d-140">quoteChar</span></span> |<span data-ttu-id="46d1d-141">Le caractère utilisé pour entourer de guillemets une valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="46d1d-141">The character used to quote a string value.</span></span> <span data-ttu-id="46d1d-142">Les séparateurs de colonnes et de lignes à l'intérieur des caractères de guillemets sont considérés comme faisant partie de la valeur de la chaîne.</span><span class="sxs-lookup"><span data-stu-id="46d1d-142">The column and row delimiters inside the quote characters would be treated as part of the string value.</span></span> <span data-ttu-id="46d1d-143">Cette propriété s’applique aux jeux de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="46d1d-143">This property is applicable to both input and output datasets.</span></span><br/><br/><span data-ttu-id="46d1d-144">Vous ne pouvez pas spécifier à la fois escapeChar et quoteChar pour une table.</span><span class="sxs-lookup"><span data-stu-id="46d1d-144">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="46d1d-145">Un seul caractère est autorisé.</span><span class="sxs-lookup"><span data-stu-id="46d1d-145">Only one character is allowed.</span></span> <span data-ttu-id="46d1d-146">Aucune valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="46d1d-146">No default value.</span></span> <br/><br/><span data-ttu-id="46d1d-147">Par exemple, si vous avez une virgule (,) comme séparateur de colonnes mais que vous voulez avoir le caractère virgule dans le texte (par exemple : « Hello, world »), vous pouvez définir " (guillemet droit) comme caractère de guillemet et utiliser la chaîne "Hello, world" dans la source.</span><span class="sxs-lookup"><span data-stu-id="46d1d-147">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span></span> |<span data-ttu-id="46d1d-148">Non</span><span class="sxs-lookup"><span data-stu-id="46d1d-148">No</span></span> |
| <span data-ttu-id="46d1d-149">nullValue</span><span class="sxs-lookup"><span data-stu-id="46d1d-149">nullValue</span></span> |<span data-ttu-id="46d1d-150">Un ou plusieurs caractères utilisés pour représenter une valeur null.</span><span class="sxs-lookup"><span data-stu-id="46d1d-150">One or more characters used to represent a null value.</span></span> |<span data-ttu-id="46d1d-151">Un ou plusieurs caractères.</span><span class="sxs-lookup"><span data-stu-id="46d1d-151">One or more characters.</span></span> <span data-ttu-id="46d1d-152">Les valeurs **par défaut** sont **« \N » et « NULL »** en lecture, et **« \N »** en écriture.</span><span class="sxs-lookup"><span data-stu-id="46d1d-152">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="46d1d-153">Non</span><span class="sxs-lookup"><span data-stu-id="46d1d-153">No</span></span> |
| <span data-ttu-id="46d1d-154">encodingName</span><span class="sxs-lookup"><span data-stu-id="46d1d-154">encodingName</span></span> |<span data-ttu-id="46d1d-155">Spécifier le nom d'encodage.</span><span class="sxs-lookup"><span data-stu-id="46d1d-155">Specify the encoding name.</span></span> |<span data-ttu-id="46d1d-156">Une liste de noms d’encodage valides.</span><span class="sxs-lookup"><span data-stu-id="46d1d-156">A valid encoding name.</span></span> <span data-ttu-id="46d1d-157">Consultez : [Propriété Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="46d1d-157">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="46d1d-158">Exemple : windows-1250 ou shift_jis.</span><span class="sxs-lookup"><span data-stu-id="46d1d-158">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="46d1d-159">La valeur **par défaut** est **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="46d1d-159">The **default** value is **UTF-8**.</span></span> |<span data-ttu-id="46d1d-160">Non</span><span class="sxs-lookup"><span data-stu-id="46d1d-160">No</span></span> |
| <span data-ttu-id="46d1d-161">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="46d1d-161">firstRowAsHeader</span></span> |<span data-ttu-id="46d1d-162">Spécifie si la première ligne doit être considérée comme un en-tête.</span><span class="sxs-lookup"><span data-stu-id="46d1d-162">Specifies whether to consider the first row as a header.</span></span> <span data-ttu-id="46d1d-163">Pour un jeu de données d’entrée, Data Factory lit la première ligne comme un en-tête.</span><span class="sxs-lookup"><span data-stu-id="46d1d-163">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="46d1d-164">Pour un jeu de données de sortie, Data Factory écrit la première ligne comme un en-tête.</span><span class="sxs-lookup"><span data-stu-id="46d1d-164">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="46d1d-165">Voir [Scénarios d’utilisation de `firstRowAsHeader` et `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) pour obtenir des exemples de scénarios.</span><span class="sxs-lookup"><span data-stu-id="46d1d-165">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="46d1d-166">true</span><span class="sxs-lookup"><span data-stu-id="46d1d-166">True</span></span><br/><span data-ttu-id="46d1d-167"><b>false (valeur par défaut)</b></span><span class="sxs-lookup"><span data-stu-id="46d1d-167"><b>False (default)</b></span></span> |<span data-ttu-id="46d1d-168">Non</span><span class="sxs-lookup"><span data-stu-id="46d1d-168">No</span></span> |
| <span data-ttu-id="46d1d-169">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="46d1d-169">skipLineCount</span></span> |<span data-ttu-id="46d1d-170">Indique le nombre de lignes à ignorer lors de la lecture des données à partir des fichiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="46d1d-170">Indicates the number of rows to skip when reading data from input files.</span></span> <span data-ttu-id="46d1d-171">Si skipLineCount et firstRowAsHeader sont spécifiés, les lignes sont d’abord ignorées, puis les informations d’en-tête sont lues à partir du fichier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="46d1d-171">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span></span> <br/><br/><span data-ttu-id="46d1d-172">Voir [Scénarios d’utilisation de `firstRowAsHeader` et `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) pour obtenir des exemples de scénarios.</span><span class="sxs-lookup"><span data-stu-id="46d1d-172">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="46d1d-173">Entier </span><span class="sxs-lookup"><span data-stu-id="46d1d-173">Integer</span></span> |<span data-ttu-id="46d1d-174">Non</span><span class="sxs-lookup"><span data-stu-id="46d1d-174">No</span></span> |
| <span data-ttu-id="46d1d-175">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="46d1d-175">treatEmptyAsNull</span></span> |<span data-ttu-id="46d1d-176">Spécifie si une chaîne null ou vide doit être traitée comme une valeur null lors de la lecture des données à partir d’un fichier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="46d1d-176">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="46d1d-177">**True (valeur par défaut)**</span><span class="sxs-lookup"><span data-stu-id="46d1d-177">**True (default)**</span></span><br/><span data-ttu-id="46d1d-178">False</span><span class="sxs-lookup"><span data-stu-id="46d1d-178">False</span></span> |<span data-ttu-id="46d1d-179">Non</span><span class="sxs-lookup"><span data-stu-id="46d1d-179">No</span></span> |

### <a name="textformat-example"></a><span data-ttu-id="46d1d-180">Exemple pour TextFormat</span><span class="sxs-lookup"><span data-stu-id="46d1d-180">TextFormat example</span></span>
<span data-ttu-id="46d1d-181">Dans la définition JSON suivante d’un jeu de données, certaines propriétés facultatives sont spécifiées.</span><span class="sxs-lookup"><span data-stu-id="46d1d-181">In the following JSON definition for a dataset, some of the optional properties are specified.</span></span>

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

<span data-ttu-id="46d1d-182">Pour utiliser un caractère `escapeChar` au lieu de `quoteChar`, remplacez la ligne par `quoteChar`, avec le caractère escapeChar suivant :</span><span class="sxs-lookup"><span data-stu-id="46d1d-182">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span></span>

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="46d1d-183">Scénarios d’utilisation de firstRowAsHeader et skipLineCount</span><span class="sxs-lookup"><span data-stu-id="46d1d-183">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="46d1d-184">Vous copiez à partir d’une source hors fichier vers un fichier texte et vous souhaitez ajouter une ligne d’en-tête qui contient les métadonnées de schéma (par exemple : schéma SQL).</span><span class="sxs-lookup"><span data-stu-id="46d1d-184">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="46d1d-185">Définissez le paramètre `firstRowAsHeader` sur true dans le jeu de données de sortie pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="46d1d-185">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span></span>
* <span data-ttu-id="46d1d-186">Vous copiez à partir d’un fichier texte contenant une ligne d’en-tête vers un récepteur hors fichier et souhaitez supprimer cette ligne.</span><span class="sxs-lookup"><span data-stu-id="46d1d-186">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span></span> <span data-ttu-id="46d1d-187">Définissez le paramètre `firstRowAsHeader` sur true dans le jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="46d1d-187">Specify `firstRowAsHeader` as true in the input dataset.</span></span>
* <span data-ttu-id="46d1d-188">Vous copiez à partir d’un fichier texte et souhaitez ignorer quelques lignes au début, qui ne contiennent ni données, ni informations d’en-tête.</span><span class="sxs-lookup"><span data-stu-id="46d1d-188">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span></span> <span data-ttu-id="46d1d-189">Spécifiez le paramètre `skipLineCount` pour indiquer le nombre de lignes à ignorer.</span><span class="sxs-lookup"><span data-stu-id="46d1d-189">Specify `skipLineCount` to indicate the number of lines to be skipped.</span></span> <span data-ttu-id="46d1d-190">Si le reste du fichier contient une ligne d’en-tête, vous pouvez également spécifier `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="46d1d-190">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="46d1d-191">Si les paramètres `skipLineCount` et `firstRowAsHeader` sont tous deux spécifiés, les lignes sont d’abord ignorées, puis les informations d’en-tête sont lues à partir du fichier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="46d1d-191">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span></span>

## <a name="json-format"></a><span data-ttu-id="46d1d-192">Format JSON</span><span class="sxs-lookup"><span data-stu-id="46d1d-192">JSON format</span></span>
<span data-ttu-id="46d1d-193">Pour en savoir plus sur **l’importation ou l’exportation de fichiers JSON en l’état dans ou à partir d’Azure Cosmos DB**, consultez la section [Importation/exportation de documents JSON](data-factory-azure-documentdb-connector.md#importexport-json-documents) de l’article [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) (Déplacer des données vers et depuis Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="46d1d-193">To **import/export a JSON file as-is into/from Azure Cosmos DB**, the see [Import/export JSON documents](data-factory-azure-documentdb-connector.md#importexport-json-documents) section in [Move data to/from Azure Cosmos DB](data-factory-azure-documentdb-connector.md) article.</span></span>

<span data-ttu-id="46d1d-194">Si vous souhaitez analyser des fichiers JSON ou écrire des données au format JSON, définissez la propriété `type` de la section `format` sur **JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="46d1d-194">If you want to parse the JSON files or write the data in JSON format, set the `type` property in the `format` section to **JsonFormat**.</span></span> <span data-ttu-id="46d1d-195">Vous pouvez également spécifier les propriétés **facultatives** suivantes, dans la section `format`.</span><span class="sxs-lookup"><span data-stu-id="46d1d-195">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="46d1d-196">Consultez la section [Exemple pour JsonFormat](#jsonformat-example) pour en savoir plus sur la méthode de configuration à suivre.</span><span class="sxs-lookup"><span data-stu-id="46d1d-196">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span>

| <span data-ttu-id="46d1d-197">Propriété</span><span class="sxs-lookup"><span data-stu-id="46d1d-197">Property</span></span> | <span data-ttu-id="46d1d-198">Description</span><span class="sxs-lookup"><span data-stu-id="46d1d-198">Description</span></span> | <span data-ttu-id="46d1d-199">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="46d1d-199">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="46d1d-200">filePattern</span><span class="sxs-lookup"><span data-stu-id="46d1d-200">filePattern</span></span> |<span data-ttu-id="46d1d-201">Indiquez le modèle des données stockées dans chaque fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="46d1d-201">Indicate the pattern of data stored in each JSON file.</span></span> <span data-ttu-id="46d1d-202">Les valeurs autorisées sont les suivantes : **setOfObjects** et **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="46d1d-202">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="46d1d-203">La valeur **par défaut** est **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="46d1d-203">The **default** value is **setOfObjects**.</span></span> <span data-ttu-id="46d1d-204">Consultez la section [Modèles de fichiers JSON](#json-file-patterns) pour en savoir plus sur ces modèles.</span><span class="sxs-lookup"><span data-stu-id="46d1d-204">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="46d1d-205">Non</span><span class="sxs-lookup"><span data-stu-id="46d1d-205">No</span></span> |
| <span data-ttu-id="46d1d-206">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="46d1d-206">jsonNodeReference</span></span> | <span data-ttu-id="46d1d-207">Si vous souhaitez effectuer une itération et extraire des données à partir des objets situés à l’intérieur d’un champ de tableau présentant le même modèle, spécifiez le chemin d’accès JSON de ce tableau.</span><span class="sxs-lookup"><span data-stu-id="46d1d-207">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span></span> <span data-ttu-id="46d1d-208">Cette propriété est uniquement prise en charge lors de la copie de données de fichiers JSON.</span><span class="sxs-lookup"><span data-stu-id="46d1d-208">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="46d1d-209">Non</span><span class="sxs-lookup"><span data-stu-id="46d1d-209">No</span></span> |
| <span data-ttu-id="46d1d-210">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="46d1d-210">jsonPathDefinition</span></span> | <span data-ttu-id="46d1d-211">Spécifiez l’expression de chemin JSON pour chaque mappage de colonne avec un nom de colonne personnalisé (commencez par une lettre minuscule).</span><span class="sxs-lookup"><span data-stu-id="46d1d-211">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="46d1d-212">Cette propriété est uniquement prise en charge lors de la copie de données à partir de fichiers JSON, et vous pouvez extraire des données d’un objet ou d’un tableau.</span><span class="sxs-lookup"><span data-stu-id="46d1d-212">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="46d1d-213">Pour les champs situés sous l’objet racine, commencez par $ racine ; pour ceux qui se trouvent dans le tableau sélectionné par la propriété `jsonNodeReference`, commencez par l’élément de tableau.</span><span class="sxs-lookup"><span data-stu-id="46d1d-213">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span></span> <span data-ttu-id="46d1d-214">Consultez la section [Exemple pour JsonFormat](#jsonformat-example) pour en savoir plus sur la méthode de configuration à suivre.</span><span class="sxs-lookup"><span data-stu-id="46d1d-214">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span> | <span data-ttu-id="46d1d-215">Non</span><span class="sxs-lookup"><span data-stu-id="46d1d-215">No</span></span> |
| <span data-ttu-id="46d1d-216">encodingName</span><span class="sxs-lookup"><span data-stu-id="46d1d-216">encodingName</span></span> |<span data-ttu-id="46d1d-217">Spécifiez le nom du codage.</span><span class="sxs-lookup"><span data-stu-id="46d1d-217">Specify the encoding name.</span></span> <span data-ttu-id="46d1d-218">Pour obtenir une liste des noms d’encodage valides, consultez la propriété [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) .</span><span class="sxs-lookup"><span data-stu-id="46d1d-218">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="46d1d-219">Par exemple : windows-1250 ou shift_jis.</span><span class="sxs-lookup"><span data-stu-id="46d1d-219">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="46d1d-220">La valeur **par défaut** est : **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="46d1d-220">The **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="46d1d-221">Non</span><span class="sxs-lookup"><span data-stu-id="46d1d-221">No</span></span> |
| <span data-ttu-id="46d1d-222">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="46d1d-222">nestingSeparator</span></span> |<span data-ttu-id="46d1d-223">Caractère utilisé pour séparer les niveaux d'imbrication.</span><span class="sxs-lookup"><span data-stu-id="46d1d-223">Character that is used to separate nesting levels.</span></span> <span data-ttu-id="46d1d-224">La valeur par défaut est . (point).</span><span class="sxs-lookup"><span data-stu-id="46d1d-224">The default value is '.' (dot).</span></span> |<span data-ttu-id="46d1d-225">Non</span><span class="sxs-lookup"><span data-stu-id="46d1d-225">No</span></span> |

### <a name="json-file-patterns"></a><span data-ttu-id="46d1d-226">Modèles de fichiers JSON</span><span class="sxs-lookup"><span data-stu-id="46d1d-226">JSON file patterns</span></span>

<span data-ttu-id="46d1d-227">L’activité de copie peut analyser les modèles de fichiers JSON ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="46d1d-227">Copy activity can parse the following patterns of JSON files:</span></span>

- <span data-ttu-id="46d1d-228">**Type I : setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="46d1d-228">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="46d1d-229">Chaque fichier contient un objet unique, ou plusieurs objets concaténés/délimités par des lignes.</span><span class="sxs-lookup"><span data-stu-id="46d1d-229">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="46d1d-230">Quand cette option est sélectionnée dans un jeu de données de sortie, l’activité de copie produit un seul fichier JSON contenant un objet par ligne (format délimité par des lignes).</span><span class="sxs-lookup"><span data-stu-id="46d1d-230">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="46d1d-231">**Exemple de fichier JSON à un seul objet**</span><span class="sxs-lookup"><span data-stu-id="46d1d-231">**single object JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * <span data-ttu-id="46d1d-232">**Exemple de fichier JSON incluant des objets délimités par des lignes**</span><span class="sxs-lookup"><span data-stu-id="46d1d-232">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="46d1d-233">**Exemple de fichier JSON incluant des objets concaténés**</span><span class="sxs-lookup"><span data-stu-id="46d1d-233">**concatenated JSON example**</span></span>

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- <span data-ttu-id="46d1d-234">**Type II : arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="46d1d-234">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="46d1d-235">Chaque fichier contient un tableau d’objets.</span><span class="sxs-lookup"><span data-stu-id="46d1d-235">Each file contains an array of objects.</span></span>

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

### <a name="jsonformat-example"></a><span data-ttu-id="46d1d-236">Exemple pour JsonFormat</span><span class="sxs-lookup"><span data-stu-id="46d1d-236">JsonFormat example</span></span>

<span data-ttu-id="46d1d-237">**Cas 1 : Copie de données à partir de fichiers JSON**</span><span class="sxs-lookup"><span data-stu-id="46d1d-237">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="46d1d-238">Consultez les deux exemples suivants lors de la copie des données à partir de fichiers JSON.</span><span class="sxs-lookup"><span data-stu-id="46d1d-238">See the following two samples when copying data from JSON files.</span></span> <span data-ttu-id="46d1d-239">Voici quelques points généraux à prendre en compte :</span><span class="sxs-lookup"><span data-stu-id="46d1d-239">The generic points to note:</span></span>

<span data-ttu-id="46d1d-240">**Exemple 1 : Extraire des données d’objet et de tableau**</span><span class="sxs-lookup"><span data-stu-id="46d1d-240">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="46d1d-241">Dans cet exemple, un objet JSON racine doit correspondre à un seul enregistrement dans la table de résultats.</span><span class="sxs-lookup"><span data-stu-id="46d1d-241">In this sample, you expect one root JSON object maps to single record in tabular result.</span></span> <span data-ttu-id="46d1d-242">Prenons un fichier JSON avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="46d1d-242">If you have a JSON file with the following content:</span></span>  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
<span data-ttu-id="46d1d-243">Vous voulez copier ce contenu dans un tableau SQL Azure au format suivant, en extrayant les données des objets et du tableau :</span><span class="sxs-lookup"><span data-stu-id="46d1d-243">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="46d1d-244">id</span><span class="sxs-lookup"><span data-stu-id="46d1d-244">id</span></span> | <span data-ttu-id="46d1d-245">deviceType</span><span class="sxs-lookup"><span data-stu-id="46d1d-245">deviceType</span></span> | <span data-ttu-id="46d1d-246">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="46d1d-246">targetResourceType</span></span> | <span data-ttu-id="46d1d-247">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="46d1d-247">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="46d1d-248">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="46d1d-248">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="46d1d-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="46d1d-249">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="46d1d-250">PC</span><span class="sxs-lookup"><span data-stu-id="46d1d-250">PC</span></span> | <span data-ttu-id="46d1d-251">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="46d1d-251">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="46d1d-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="46d1d-252">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="46d1d-253">13/01/2017 11:24:37</span><span class="sxs-lookup"><span data-stu-id="46d1d-253">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="46d1d-254">Le jeu de données d’entrée présentant le type **JsonFormat** est défini comme suit : (définition partielle présentant uniquement les éléments pertinents).</span><span class="sxs-lookup"><span data-stu-id="46d1d-254">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="46d1d-255">Plus précisément :</span><span class="sxs-lookup"><span data-stu-id="46d1d-255">More specifically:</span></span>

- <span data-ttu-id="46d1d-256">La section `structure` définit les noms de colonne personnalisés et le type de données correspondant lors de la conversion des données au format tabulaire.</span><span class="sxs-lookup"><span data-stu-id="46d1d-256">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="46d1d-257">Cette section est **facultative**, sauf si vous avez besoin d’effectuer un mappage de colonne.</span><span class="sxs-lookup"><span data-stu-id="46d1d-257">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="46d1d-258">Pour plus d’informations, consultez [Mapper des colonnes d’un jeu de données source sur des colonnes d’un jeu de données de destination](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="46d1d-258">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="46d1d-259">Le paramètre `jsonPathDefinition` indique le chemin JSON de chaque colonne indiquant l’emplacement à partir duquel les données sont extraites.</span><span class="sxs-lookup"><span data-stu-id="46d1d-259">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="46d1d-260">Pour copier les données d’un tableau, vous pouvez utiliser **array[x].property** pour extraire la valeur de la propriété spécifiée à partir de l’objet x, ou vous pouvez utiliser **array[*].property** pour trouver la valeur de tout objet contenant cette propriété.</span><span class="sxs-lookup"><span data-stu-id="46d1d-260">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[*].property** to find the value from any object containing such property.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

<span data-ttu-id="46d1d-261">**Exemple 2 : application croisée de plusieurs objets avec le même modèle à partir d’un tableau**</span><span class="sxs-lookup"><span data-stu-id="46d1d-261">**Sample 2: cross apply multiple objects with the same pattern from array**</span></span>

<span data-ttu-id="46d1d-262">Dans cet exemple, vous voulez transformer un objet JSON racine en plusieurs enregistrements dans la table de résultats.</span><span class="sxs-lookup"><span data-stu-id="46d1d-262">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="46d1d-263">Prenons un fichier JSON avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="46d1d-263">If you have a JSON file with the following content:</span></span>  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
<span data-ttu-id="46d1d-264">Vous souhaitez copier ce fichier dans une table SQL Azure au format suivant, en mettant à plat les données se trouvant dans le tableau et en effectuant une jointure croisée avec les informations racines communes :</span><span class="sxs-lookup"><span data-stu-id="46d1d-264">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span></span>

| <span data-ttu-id="46d1d-265">ordernumber</span><span class="sxs-lookup"><span data-stu-id="46d1d-265">ordernumber</span></span> | <span data-ttu-id="46d1d-266">orderdate</span><span class="sxs-lookup"><span data-stu-id="46d1d-266">orderdate</span></span> | <span data-ttu-id="46d1d-267">order_pd</span><span class="sxs-lookup"><span data-stu-id="46d1d-267">order_pd</span></span> | <span data-ttu-id="46d1d-268">order_price</span><span class="sxs-lookup"><span data-stu-id="46d1d-268">order_price</span></span> | <span data-ttu-id="46d1d-269">city</span><span class="sxs-lookup"><span data-stu-id="46d1d-269">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="46d1d-270">01</span><span class="sxs-lookup"><span data-stu-id="46d1d-270">01</span></span> | <span data-ttu-id="46d1d-271">20170122</span><span class="sxs-lookup"><span data-stu-id="46d1d-271">20170122</span></span> | <span data-ttu-id="46d1d-272">P1</span><span class="sxs-lookup"><span data-stu-id="46d1d-272">P1</span></span> | <span data-ttu-id="46d1d-273">23</span><span class="sxs-lookup"><span data-stu-id="46d1d-273">23</span></span> | <span data-ttu-id="46d1d-274">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="46d1d-274">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="46d1d-275">01</span><span class="sxs-lookup"><span data-stu-id="46d1d-275">01</span></span> | <span data-ttu-id="46d1d-276">20170122</span><span class="sxs-lookup"><span data-stu-id="46d1d-276">20170122</span></span> | <span data-ttu-id="46d1d-277">P2</span><span class="sxs-lookup"><span data-stu-id="46d1d-277">P2</span></span> | <span data-ttu-id="46d1d-278">13.</span><span class="sxs-lookup"><span data-stu-id="46d1d-278">13</span></span> | <span data-ttu-id="46d1d-279">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="46d1d-279">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="46d1d-280">01</span><span class="sxs-lookup"><span data-stu-id="46d1d-280">01</span></span> | <span data-ttu-id="46d1d-281">20170122</span><span class="sxs-lookup"><span data-stu-id="46d1d-281">20170122</span></span> | <span data-ttu-id="46d1d-282">P3</span><span class="sxs-lookup"><span data-stu-id="46d1d-282">P3</span></span> | <span data-ttu-id="46d1d-283">231</span><span class="sxs-lookup"><span data-stu-id="46d1d-283">231</span></span> | <span data-ttu-id="46d1d-284">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="46d1d-284">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="46d1d-285">Le jeu de données d’entrée présentant le type **JsonFormat** est défini comme suit : (définition partielle présentant uniquement les éléments pertinents).</span><span class="sxs-lookup"><span data-stu-id="46d1d-285">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="46d1d-286">Plus précisément :</span><span class="sxs-lookup"><span data-stu-id="46d1d-286">More specifically:</span></span>

- <span data-ttu-id="46d1d-287">La section `structure` définit les noms de colonne personnalisés et le type de données correspondant lors de la conversion des données au format tabulaire.</span><span class="sxs-lookup"><span data-stu-id="46d1d-287">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="46d1d-288">Cette section est **facultative**, sauf si vous avez besoin d’effectuer un mappage de colonne.</span><span class="sxs-lookup"><span data-stu-id="46d1d-288">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="46d1d-289">Pour plus d’informations, consultez [Mapper des colonnes d’un jeu de données source sur des colonnes d’un jeu de données de destination](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="46d1d-289">See [Map source dataset columns to destination dataset columns](data-factory-map-columns.md) section for more details.</span></span>
- <span data-ttu-id="46d1d-290">Le paramètre `jsonNodeReference` indique que les données doivent être itérées et extraites des objets présentant le même modèle sous « orderlines » dans le **tableau**.</span><span class="sxs-lookup"><span data-stu-id="46d1d-290">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="46d1d-291">Le paramètre `jsonPathDefinition` indique le chemin JSON de chaque colonne indiquant l’emplacement à partir duquel les données sont extraites.</span><span class="sxs-lookup"><span data-stu-id="46d1d-291">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="46d1d-292">Dans cet exemple, les éléments « ordernumber », « orderdate » et « city » se trouvent sous l’objet racine associé au chemin JSON commençant par « $. », tandis que les éléments « order_pd » et « order_price » sont définis avec le chemin d’accès dérivé de l’élément de tableau sans « $.».</span><span class="sxs-lookup"><span data-stu-id="46d1d-292">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

<span data-ttu-id="46d1d-293">**Notez les points suivants :**</span><span class="sxs-lookup"><span data-stu-id="46d1d-293">**Note the following points:**</span></span>

* <span data-ttu-id="46d1d-294">Si les éléments `structure` et `jsonPathDefinition` ne sont pas définis dans le jeu de données Data Factory, l’activité de copie détecte le schéma à partir du premier objet et aplatit l’objet entier.</span><span class="sxs-lookup"><span data-stu-id="46d1d-294">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span></span>
* <span data-ttu-id="46d1d-295">Si l’entrée JSON contient un tableau, l’activité de copie convertit la valeur du tableau entier en une chaîne, par défaut.</span><span class="sxs-lookup"><span data-stu-id="46d1d-295">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span></span> <span data-ttu-id="46d1d-296">Vous pouvez choisir d’extraire des données de cette dernière à l’aide de `jsonNodeReference` et/ou `jsonPathDefinition`, ou ignorer cette opération en ne la spécifiant pas dans `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="46d1d-296">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="46d1d-297">S’il y a plusieurs noms identiques au même niveau, l’activité de copie sélectionne le dernier nom.</span><span class="sxs-lookup"><span data-stu-id="46d1d-297">If there are duplicate names at the same level, the Copy Activity picks the last one.</span></span>
* <span data-ttu-id="46d1d-298">Les noms de propriété respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="46d1d-298">Property names are case-sensitive.</span></span> <span data-ttu-id="46d1d-299">Quand deux propriétés de même nom ont une casse différente, elles sont considérées comme deux propriétés distinctes.</span><span class="sxs-lookup"><span data-stu-id="46d1d-299">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="46d1d-300">**Cas 2 : Écriture de données dans un fichier JSON**</span><span class="sxs-lookup"><span data-stu-id="46d1d-300">**Case 2: Writing data to JSON file**</span></span>

<span data-ttu-id="46d1d-301">Vous disposez de la table suivante dans votre base de données SQL :</span><span class="sxs-lookup"><span data-stu-id="46d1d-301">If you have the following table in SQL Database:</span></span>

| <span data-ttu-id="46d1d-302">id</span><span class="sxs-lookup"><span data-stu-id="46d1d-302">id</span></span> | <span data-ttu-id="46d1d-303">order_date</span><span class="sxs-lookup"><span data-stu-id="46d1d-303">order_date</span></span> | <span data-ttu-id="46d1d-304">order_price</span><span class="sxs-lookup"><span data-stu-id="46d1d-304">order_price</span></span> | <span data-ttu-id="46d1d-305">order_by</span><span class="sxs-lookup"><span data-stu-id="46d1d-305">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="46d1d-306">1</span><span class="sxs-lookup"><span data-stu-id="46d1d-306">1</span></span> | <span data-ttu-id="46d1d-307">20170119</span><span class="sxs-lookup"><span data-stu-id="46d1d-307">20170119</span></span> | <span data-ttu-id="46d1d-308">2000</span><span class="sxs-lookup"><span data-stu-id="46d1d-308">2000</span></span> | <span data-ttu-id="46d1d-309">David</span><span class="sxs-lookup"><span data-stu-id="46d1d-309">David</span></span> |
| <span data-ttu-id="46d1d-310">2</span><span class="sxs-lookup"><span data-stu-id="46d1d-310">2</span></span> | <span data-ttu-id="46d1d-311">20170120</span><span class="sxs-lookup"><span data-stu-id="46d1d-311">20170120</span></span> | <span data-ttu-id="46d1d-312">3 500</span><span class="sxs-lookup"><span data-stu-id="46d1d-312">3500</span></span> | <span data-ttu-id="46d1d-313">Patrick</span><span class="sxs-lookup"><span data-stu-id="46d1d-313">Patrick</span></span> |
| <span data-ttu-id="46d1d-314">3</span><span class="sxs-lookup"><span data-stu-id="46d1d-314">3</span></span> | <span data-ttu-id="46d1d-315">20170121</span><span class="sxs-lookup"><span data-stu-id="46d1d-315">20170121</span></span> | <span data-ttu-id="46d1d-316">4000</span><span class="sxs-lookup"><span data-stu-id="46d1d-316">4000</span></span> | <span data-ttu-id="46d1d-317">Jason</span><span class="sxs-lookup"><span data-stu-id="46d1d-317">Jason</span></span> |

<span data-ttu-id="46d1d-318">Pour chaque enregistrement, vous voulez écrire des données dans un objet JSON, en utilisant le format suivant :</span><span class="sxs-lookup"><span data-stu-id="46d1d-318">and for each record, you expect to write to a JSON object in the following format:</span></span>
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

<span data-ttu-id="46d1d-319">Le jeu de données de sortie présentant le type **JsonFormat** est défini comme suit : (définition partielle présentant uniquement les éléments pertinents).</span><span class="sxs-lookup"><span data-stu-id="46d1d-319">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="46d1d-320">Plus précisément, la section `structure` définit les noms de propriété personnalisés dans le fichier de destination ; le paramètre `nestingSeparator` (valeur par défaut : «. ») vous permet d’identifier la couche d’imbrication à partir du nom.</span><span class="sxs-lookup"><span data-stu-id="46d1d-320">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") are used to identify the nest layer from the name.</span></span> <span data-ttu-id="46d1d-321">Cette section est **facultative**, sauf si vous souhaitez modifier le nom de propriété par rapport au nom de la colonne source, ou imbriquer certaines propriétés.</span><span class="sxs-lookup"><span data-stu-id="46d1d-321">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span></span>

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

## <a name="avro-format"></a><span data-ttu-id="46d1d-322">Format AVRO</span><span class="sxs-lookup"><span data-stu-id="46d1d-322">AVRO format</span></span>
<span data-ttu-id="46d1d-323">Si vous souhaitez analyser des fichiers Avro ou écrire des données au format Avro, définissez la propriété `format` `type` sur **AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="46d1d-323">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span></span> <span data-ttu-id="46d1d-324">Il est inutile de spécifier des propriétés dans la partie Format de la section typeProperties.</span><span class="sxs-lookup"><span data-stu-id="46d1d-324">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="46d1d-325">Exemple :</span><span class="sxs-lookup"><span data-stu-id="46d1d-325">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="46d1d-326">Pour utiliser le format Avro dans une table Hive, vous pouvez faire référence au [didacticiel Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="46d1d-326">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="46d1d-327">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="46d1d-327">Note the following points:</span></span>  

* <span data-ttu-id="46d1d-328">[Les types de données complexes](http://avro.apache.org/docs/current/spec.html#schema_complex) ne sont pas pris en charge (enregistrements, enums, tables, cartes, unions et fixes).</span><span class="sxs-lookup"><span data-stu-id="46d1d-328">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions, and fixed).</span></span>

## <a name="orc-format"></a><span data-ttu-id="46d1d-329">Format ORC</span><span class="sxs-lookup"><span data-stu-id="46d1d-329">ORC format</span></span>
<span data-ttu-id="46d1d-330">Si vous souhaitez analyser des fichiers ORC ou écrire des données au format ORC, définissez la propriété `format` `type` sur **OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="46d1d-330">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span></span> <span data-ttu-id="46d1d-331">Il est inutile de spécifier des propriétés dans la partie Format de la section typeProperties.</span><span class="sxs-lookup"><span data-stu-id="46d1d-331">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="46d1d-332">Exemple :</span><span class="sxs-lookup"><span data-stu-id="46d1d-332">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="46d1d-333">Si vous ne copiez pas les fichiers ORC **tels quels** entre les magasins de données locaux et cloud, vous devez installer JRE 8 (Java Runtime Environment) sur votre machine de passerelle.</span><span class="sxs-lookup"><span data-stu-id="46d1d-333">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="46d1d-334">La passerelle 64 bits requiert un environnement JRE 64 bits et que la passerelle 32 bits nécessite un environnement JRE 32 bits.</span><span class="sxs-lookup"><span data-stu-id="46d1d-334">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="46d1d-335">Ces deux versions sont disponibles [ici](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="46d1d-335">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="46d1d-336">Sélectionnez la bonne version.</span><span class="sxs-lookup"><span data-stu-id="46d1d-336">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="46d1d-337">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="46d1d-337">Note the following points:</span></span>

* <span data-ttu-id="46d1d-338">Les types de données complexes ne sont pas pris en charge (STRUCT, MAP, LIST, UNION)</span><span class="sxs-lookup"><span data-stu-id="46d1d-338">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="46d1d-339">Le fichier ORC a trois [options liées à la compression](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="46d1d-339">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="46d1d-340">Data Factory prend en charge la lecture des données du fichier ORC dans tous ces formats compressés.</span><span class="sxs-lookup"><span data-stu-id="46d1d-340">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="46d1d-341">Il utilise le codec de compression se trouvant dans les métadonnées pour lire les données.</span><span class="sxs-lookup"><span data-stu-id="46d1d-341">It uses the compression codec is in the metadata to read the data.</span></span> <span data-ttu-id="46d1d-342">Toutefois, lors de l’écriture dans un fichier ORC, Data Factory choisit ZLIB, qui est la valeur par défaut pour ORC.</span><span class="sxs-lookup"><span data-stu-id="46d1d-342">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span></span> <span data-ttu-id="46d1d-343">Actuellement, il n’existe aucune option permettant de remplacer ce comportement.</span><span class="sxs-lookup"><span data-stu-id="46d1d-343">Currently, there is no option to override this behavior.</span></span>

## <a name="parquet-format"></a><span data-ttu-id="46d1d-344">Format Parquet</span><span class="sxs-lookup"><span data-stu-id="46d1d-344">Parquet format</span></span>
<span data-ttu-id="46d1d-345">Si vous souhaitez analyser des fichiers Parquet ou écrire des données au format Parquet, définissez la propriété `format` `type` sur **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="46d1d-345">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span></span> <span data-ttu-id="46d1d-346">Il est inutile de spécifier des propriétés dans la partie Format de la section typeProperties.</span><span class="sxs-lookup"><span data-stu-id="46d1d-346">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="46d1d-347">Exemple :</span><span class="sxs-lookup"><span data-stu-id="46d1d-347">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="46d1d-348">Si vous ne copiez pas les fichiers Parquet **tels quels** entre les magasins de données locaux et cloud, vous devez installer JRE 8 (Java Runtime Environment) sur votre machine de passerelle.</span><span class="sxs-lookup"><span data-stu-id="46d1d-348">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="46d1d-349">La passerelle 64 bits requiert un environnement JRE 64 bits et que la passerelle 32 bits nécessite un environnement JRE 32 bits.</span><span class="sxs-lookup"><span data-stu-id="46d1d-349">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="46d1d-350">Ces deux versions sont disponibles [ici](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="46d1d-350">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="46d1d-351">Sélectionnez la bonne version.</span><span class="sxs-lookup"><span data-stu-id="46d1d-351">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="46d1d-352">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="46d1d-352">Note the following points:</span></span>

* <span data-ttu-id="46d1d-353">Les types de données complexes ne sont pas pris en charge (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="46d1d-353">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="46d1d-354">Le fichier Parquet offre les options de compression suivantes : NONE, SNAPPY, GZIP et LZO.</span><span class="sxs-lookup"><span data-stu-id="46d1d-354">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="46d1d-355">Data Factory prend en charge la lecture des données du fichier ORC dans tous ces formats compressés.</span><span class="sxs-lookup"><span data-stu-id="46d1d-355">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="46d1d-356">Il utilise le codec de compression se trouvant dans les métadonnées pour lire les données.</span><span class="sxs-lookup"><span data-stu-id="46d1d-356">It uses the compression codec in the metadata to read the data.</span></span> <span data-ttu-id="46d1d-357">Toutefois, lors de l’écriture dans un fichier Parquet, Data Factory choisit SNAPPY, qui est la valeur par défaut pour le format Parquet.</span><span class="sxs-lookup"><span data-stu-id="46d1d-357">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span></span> <span data-ttu-id="46d1d-358">Actuellement, il n’existe aucune option permettant de remplacer ce comportement.</span><span class="sxs-lookup"><span data-stu-id="46d1d-358">Currently, there is no option to override this behavior.</span></span>

## <a name="compression-support"></a><span data-ttu-id="46d1d-359">Prise en charge de la compression</span><span class="sxs-lookup"><span data-stu-id="46d1d-359">Compression support</span></span>
<span data-ttu-id="46d1d-360">Le traitement de jeux de données de grande taille peut provoquer des goulots d’étranglement des E/S et du réseau.</span><span class="sxs-lookup"><span data-stu-id="46d1d-360">Processing large data sets can cause I/O and network bottlenecks.</span></span> <span data-ttu-id="46d1d-361">Par conséquent, les données compressées dans les magasins peuvent non seulement accélérer le transfert des données sur le réseau et économiser l’espace disque, mais également apporter des améliorations significatives des performances du traitement du Big Data.</span><span class="sxs-lookup"><span data-stu-id="46d1d-361">Therefore, compressed data in stores can not only speed up data transfer across the network and save disk space, but also bring significant performance improvements in processing big data.</span></span> <span data-ttu-id="46d1d-362">Actuellement, la compression est prise en charge pour les magasins de données de fichiers, comme les objets blob Azure ou un système de fichiers local.</span><span class="sxs-lookup"><span data-stu-id="46d1d-362">Currently, compression is supported for file-based data stores such as Azure Blob or On-premises File System.</span></span>  

<span data-ttu-id="46d1d-363">Pour spécifier la compression pour un jeu de données, utilisez la propriété **compression** du jeu de données JSON, comme dans l'exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="46d1d-363">To specify compression for a dataset, use the **compression** property in the dataset JSON as in the following example:</span></span>   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

<span data-ttu-id="46d1d-364">Partons du principe que l’exemple de jeu de données est utilisé en tant que sortie d’une activité de copie. Cette dernière va compresser les données de sortie avec le codec GZIP en utilisant le taux optimal, puis écrire les données compressées dans un fichier nommé pagecounts.csv.gz dans le Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="46d1d-364">Suppose the sample dataset is used as the output of a copy activity, the copy activity compresses the output data with GZIP codec using optimal ratio and then write the compressed data into a file named pagecounts.csv.gz in the Azure Blob Storage.</span></span>

> [!NOTE]
> <span data-ttu-id="46d1d-365">Les paramètres de compression ne sont pas pris en charge pour les données au format **AvroFormat**, **OrcFormat** ou **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="46d1d-365">Compression settings are not supported for data in the **AvroFormat**, **OrcFormat**, or **ParquetFormat**.</span></span> <span data-ttu-id="46d1d-366">Data Factory détecte et utilise le codec de compression se trouvant dans les métadonnées pour lire des fichiers présentant ces formats.</span><span class="sxs-lookup"><span data-stu-id="46d1d-366">When reading files in these formats, Data Factory detects and uses the compression codec in the metadata.</span></span> <span data-ttu-id="46d1d-367">Lors de l’écriture dans des fichiers présentant ces formats, Data Factory choisit le code de la compression par défaut pour ce format.</span><span class="sxs-lookup"><span data-stu-id="46d1d-367">When writing to files in these formats, Data Factory chooses the default compression codec for that format.</span></span> <span data-ttu-id="46d1d-368">Par exemple, ZLIB pour OrcFormat et SNAPPY pour ParquetFormat.</span><span class="sxs-lookup"><span data-stu-id="46d1d-368">For example, ZLIB for OrcFormat and SNAPPY for ParquetFormat.</span></span>   

<span data-ttu-id="46d1d-369">La section **compression** a deux propriétés :</span><span class="sxs-lookup"><span data-stu-id="46d1d-369">The **compression** section has two properties:</span></span>  

* <span data-ttu-id="46d1d-370">**Type** : le codec de compression, qui peut être **GZIP**, **Deflate**, **BZIP2** ou **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="46d1d-370">**Type:** the compression codec, which can be **GZIP**, **Deflate**, **BZIP2**, or **ZipDeflate**.</span></span>  
* <span data-ttu-id="46d1d-371">**Level** : le taux de compression, qui peut être **Optimal** ou **Fastest**.</span><span class="sxs-lookup"><span data-stu-id="46d1d-371">**Level:** the compression ratio, which can be **Optimal** or **Fastest**.</span></span>

  * <span data-ttu-id="46d1d-372">**Fastest** : l'opération de compression doit se terminer le plus rapidement possible, même si le fichier résultant n'est pas compressé de façon optimale.</span><span class="sxs-lookup"><span data-stu-id="46d1d-372">**Fastest:** The compression operation should complete as quickly as possible, even if the resulting file is not optimally compressed.</span></span>
  * <span data-ttu-id="46d1d-373">**Optimal**: l'opération de compression doit aboutir à une compression optimale, même si l'opération prend plus de temps.</span><span class="sxs-lookup"><span data-stu-id="46d1d-373">**Optimal**: The compression operation should be optimally compressed, even if the operation takes a longer time to complete.</span></span>

    <span data-ttu-id="46d1d-374">Pour plus d’informations, consultez la rubrique [Niveau de compression](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) .</span><span class="sxs-lookup"><span data-stu-id="46d1d-374">For more information, see [Compression Level](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx) topic.</span></span>

<span data-ttu-id="46d1d-375">Lorsque vous spécifiez la propriété `compression` dans un jeu de données JSON d’entrée, le pipeline peut lire les données compressées à partir de la source. Lorsque vous spécifiez la propriété dans un jeu de données JSON de sortie, l’activité de copie peut écrire les données compressées dans la destination.</span><span class="sxs-lookup"><span data-stu-id="46d1d-375">When you specify `compression` property in an input dataset JSON, the pipeline can read compressed data from the source; and when you specify the property in an output dataset JSON, the copy activity can write compressed data to the destination.</span></span> <span data-ttu-id="46d1d-376">Voici quelques exemples de scénarios :</span><span class="sxs-lookup"><span data-stu-id="46d1d-376">Here are a few sample scenarios:</span></span>

* <span data-ttu-id="46d1d-377">Lire les données compressées GZIP à partir d’un objet blob Azure, les décompresser et écrire des données du résultat dans une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="46d1d-377">Read GZIP compressed data from an Azure blob, decompress it, and write result data to an Azure SQL database.</span></span> <span data-ttu-id="46d1d-378">Dans ce cas, vous définissez le jeu de données d’objets Blob Azure d’entrée avec la propriété JSON `compression` `type` au format GZIP.</span><span class="sxs-lookup"><span data-stu-id="46d1d-378">You define the input Azure Blob dataset with the `compression` `type` JSON property as GZIP.</span></span>
* <span data-ttu-id="46d1d-379">Lire les données d’un fichier de texte brut dans le système de fichiers local, les compresser en utilisant le format GZIP et écrire les données compressées dans un objet blob Azure.</span><span class="sxs-lookup"><span data-stu-id="46d1d-379">Read data from a plain-text file from on-premises File System, compress it using GZip format, and write the compressed data to an Azure blob.</span></span> <span data-ttu-id="46d1d-380">Dans ce cas, vous définissez le jeu de données d’objets Blob Azure de sortie avec la propriété JSON `compression` `type` au format GZIP.</span><span class="sxs-lookup"><span data-stu-id="46d1d-380">You define an output Azure Blob dataset with the `compression` `type` JSON property as GZip.</span></span>
* <span data-ttu-id="46d1d-381">Lisez le fichier .zip à partir du serveur FTP, décompressez-le pour accéder aux fichiers qu’il contient et placez ces derniers dans Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="46d1d-381">Read .zip file from FTP server, decompress it to get the files inside, and land those files into Azure Data Lake Store.</span></span> <span data-ttu-id="46d1d-382">Dans ce cas, vous définissez le jeu de données FTP d’entrée avec la propriété JSON `compression` `type` au format ZipDeflate.</span><span class="sxs-lookup"><span data-stu-id="46d1d-382">You define an input FTP dataset with the `compression` `type` JSON property as ZipDeflate.</span></span>
* <span data-ttu-id="46d1d-383">Lire les données compressées au format GZIP à partir d’un objet blob Azure, les décompresser, les compresser en utilisant le format BZIP2 et écrire les données résultantes dans un objet blob Azure.</span><span class="sxs-lookup"><span data-stu-id="46d1d-383">Read a GZIP-compressed data from an Azure blob, decompress it, compress it using BZIP2, and write result data to an Azure blob.</span></span> <span data-ttu-id="46d1d-384">Dans ce cas, vous définissez le jeu de données d’objet blob Azure d’entrée avec le paramètre `compression` `type` défini sur GZIP et le jeu de données de sortie avec le paramètre `compression` `type` défini sur BZIP2.</span><span class="sxs-lookup"><span data-stu-id="46d1d-384">You define the input Azure Blob dataset with `compression` `type` set to GZIP and the output dataset with `compression` `type` set to BZIP2 in this case.</span></span>   


## <a name="next-steps"></a><span data-ttu-id="46d1d-385">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="46d1d-385">Next steps</span></span>
<span data-ttu-id="46d1d-386">Consultez les articles suivants pour connaître les magasins de données basés sur un fichier qui sont pris en charge par Azure Data Factory :</span><span class="sxs-lookup"><span data-stu-id="46d1d-386">See the following articles for file-based data stores supported by Azure Data Factory:</span></span>

- [<span data-ttu-id="46d1d-387">Stockage Blob Azure</span><span class="sxs-lookup"><span data-stu-id="46d1d-387">Azure Blob Storage</span></span>](data-factory-azure-blob-connector.md)
- [<span data-ttu-id="46d1d-388">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="46d1d-388">Azure Data Lake Store</span></span>](data-factory-azure-datalake-connector.md)
- [<span data-ttu-id="46d1d-389">FTP</span><span class="sxs-lookup"><span data-stu-id="46d1d-389">FTP</span></span>](data-factory-ftp-connector.md)
- [<span data-ttu-id="46d1d-390">HDFS</span><span class="sxs-lookup"><span data-stu-id="46d1d-390">HDFS</span></span>](data-factory-hdfs-connector.md)
- [<span data-ttu-id="46d1d-391">Système de fichiers</span><span class="sxs-lookup"><span data-stu-id="46d1d-391">File System</span></span>](data-factory-onprem-file-system-connector.md)
- [<span data-ttu-id="46d1d-392">Amazon S3</span><span class="sxs-lookup"><span data-stu-id="46d1d-392">Amazon S3</span></span>](data-factory-amazon-simple-storage-service-connector.md)
