## <a name="specifying-formats"></a><span data-ttu-id="13133-101">Spécification des formats</span><span class="sxs-lookup"><span data-stu-id="13133-101">Specifying formats</span></span>
<span data-ttu-id="13133-102">Azure Data Factory prend en charge les types de format suivants :</span><span class="sxs-lookup"><span data-stu-id="13133-102">Azure Data Factory supports the following format types:</span></span>

* [<span data-ttu-id="13133-103">Format Texte</span><span class="sxs-lookup"><span data-stu-id="13133-103">Text Format</span></span>](#specifying-textformat)
* [<span data-ttu-id="13133-104">Format JSON</span><span class="sxs-lookup"><span data-stu-id="13133-104">JSON Format</span></span>](#specifying-jsonformat)
* [<span data-ttu-id="13133-105">Format Avro</span><span class="sxs-lookup"><span data-stu-id="13133-105">Avro Format</span></span>](#specifying-avroformat)
* [<span data-ttu-id="13133-106">Format ORC</span><span class="sxs-lookup"><span data-stu-id="13133-106">ORC Format</span></span>](#specifying-orcformat)
* [<span data-ttu-id="13133-107">Format Parquet</span><span class="sxs-lookup"><span data-stu-id="13133-107">Parquet Format</span></span>](#specifying-parquetformat)

### <a name="specifying-textformat"></a><span data-ttu-id="13133-108">Définition de TextFormat</span><span class="sxs-lookup"><span data-stu-id="13133-108">Specifying TextFormat</span></span>
<span data-ttu-id="13133-109">Si vous souhaitez analyser des fichiers texte ou écrire des données au format texte, définissez la propriété `format` `type` sur **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="13133-109">If you want to parse the text files or write the data in text format, set the `format` `type` property to **TextFormat**.</span></span> <span data-ttu-id="13133-110">Vous pouvez également spécifier les propriétés **facultatives** suivantes, dans la section `format`.</span><span class="sxs-lookup"><span data-stu-id="13133-110">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="13133-111">Consultez la section [Exemple pour TextFormat](#textformat-example) pour en savoir plus sur la méthode de configuration à suivre.</span><span class="sxs-lookup"><span data-stu-id="13133-111">See [TextFormat example](#textformat-example) section on how to configure.</span></span>

| <span data-ttu-id="13133-112">Propriété</span><span class="sxs-lookup"><span data-stu-id="13133-112">Property</span></span> | <span data-ttu-id="13133-113">Description</span><span class="sxs-lookup"><span data-stu-id="13133-113">Description</span></span> | <span data-ttu-id="13133-114">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="13133-114">Allowed values</span></span> | <span data-ttu-id="13133-115">Requis</span><span class="sxs-lookup"><span data-stu-id="13133-115">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="13133-116">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="13133-116">columnDelimiter</span></span> |<span data-ttu-id="13133-117">Caractère utilisé pour séparer les colonnes dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="13133-117">The character used to separate columns in a file.</span></span> <span data-ttu-id="13133-118">Vous pouvez envisager d’utiliser un caractère non imprimable rare qui n’existe probablement pas dans vos données ; par exemple, spécifiez « \u0001 », qui représente le début d’en-tête.</span><span class="sxs-lookup"><span data-stu-id="13133-118">You can consider to use a rare unprintable char which not likely exists in your data: e.g. specify "\u0001" which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="13133-119">Un seul caractère est autorisé.</span><span class="sxs-lookup"><span data-stu-id="13133-119">Only one character is allowed.</span></span> <span data-ttu-id="13133-120">La valeur **par défaut** est la **virgule (,)**.</span><span class="sxs-lookup"><span data-stu-id="13133-120">The **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="13133-121">Pour utiliser un caractère Unicode, reportez-vous à [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) (Caractères Unicode) pour obtenir le code correspondant.</span><span class="sxs-lookup"><span data-stu-id="13133-121">To use an Unicode character, refer to [Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) to get the corresponding code for it.</span></span> |<span data-ttu-id="13133-122">Non</span><span class="sxs-lookup"><span data-stu-id="13133-122">No</span></span> |
| <span data-ttu-id="13133-123">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="13133-123">rowDelimiter</span></span> |<span data-ttu-id="13133-124">Caractère utilisé pour séparer les lignes dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="13133-124">The character used to separate rows in a file.</span></span> |<span data-ttu-id="13133-125">Un seul caractère est autorisé.</span><span class="sxs-lookup"><span data-stu-id="13133-125">Only one character is allowed.</span></span> <span data-ttu-id="13133-126">La valeur **par défaut** est l’une des suivantes : **[« \r\n », « \r », « \n »]** en lecture et **« \r\n »** en écriture.</span><span class="sxs-lookup"><span data-stu-id="13133-126">The **default** value is any of the following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="13133-127">Non</span><span class="sxs-lookup"><span data-stu-id="13133-127">No</span></span> |
| <span data-ttu-id="13133-128">escapeChar</span><span class="sxs-lookup"><span data-stu-id="13133-128">escapeChar</span></span> |<span data-ttu-id="13133-129">Caractère spécial utilisé pour échapper au délimiteur de colonnes dans le contenu du fichier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="13133-129">The special character used to escape a column delimiter in the content of input file.</span></span> <br/><br/><span data-ttu-id="13133-130">Vous ne pouvez pas spécifier à la fois escapeChar et quoteChar pour une table.</span><span class="sxs-lookup"><span data-stu-id="13133-130">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="13133-131">Un seul caractère est autorisé.</span><span class="sxs-lookup"><span data-stu-id="13133-131">Only one character is allowed.</span></span> <span data-ttu-id="13133-132">Aucune valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="13133-132">No default value.</span></span> <br/><br/><span data-ttu-id="13133-133">Par exemple, si vous avez une virgule (,) comme séparateur de colonnes mais que vous voulez avoir le caractère virgule dans le texte (par exemple : « Hello, world »), vous pouvez définir « $ » comme caractère d’échappement et utiliser la chaîne « Hello$, world » dans la source.</span><span class="sxs-lookup"><span data-stu-id="13133-133">Example: if you have comma (',') as the column delimiter but you want to have the comma character in the text (example: "Hello, world"), you can define ‘$’ as the escape character and use string "Hello$, world" in the source.</span></span> |<span data-ttu-id="13133-134">Non</span><span class="sxs-lookup"><span data-stu-id="13133-134">No</span></span> |
| <span data-ttu-id="13133-135">quoteChar</span><span class="sxs-lookup"><span data-stu-id="13133-135">quoteChar</span></span> |<span data-ttu-id="13133-136">Le caractère utilisé pour entourer de guillemets une valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="13133-136">The character used to quote a string value.</span></span> <span data-ttu-id="13133-137">Les séparateurs de colonnes et de lignes à l'intérieur des caractères de guillemets sont considérés comme faisant partie de la valeur de la chaîne.</span><span class="sxs-lookup"><span data-stu-id="13133-137">The column and row delimiters inside the quote characters would be treated as part of the string value.</span></span> <span data-ttu-id="13133-138">Cette propriété s’applique aux jeux de données d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="13133-138">This property is applicable to both input and output datasets.</span></span><br/><br/><span data-ttu-id="13133-139">Vous ne pouvez pas spécifier à la fois escapeChar et quoteChar pour une table.</span><span class="sxs-lookup"><span data-stu-id="13133-139">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="13133-140">Un seul caractère est autorisé.</span><span class="sxs-lookup"><span data-stu-id="13133-140">Only one character is allowed.</span></span> <span data-ttu-id="13133-141">Aucune valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="13133-141">No default value.</span></span> <br/><br/><span data-ttu-id="13133-142">Par exemple, si vous avez une virgule (,) comme séparateur de colonnes mais que vous voulez avoir le caractère virgule dans le texte (par exemple : « Hello, world »), vous pouvez définir " (guillemet droit) comme caractère de guillemet et utiliser la chaîne "Hello, world" dans la source.</span><span class="sxs-lookup"><span data-stu-id="13133-142">For example, if you have comma (',') as the column delimiter but you want to have comma character in the text (example: <Hello, world>), you can define " (double quote) as the quote character and use the string "Hello, world" in the source.</span></span> |<span data-ttu-id="13133-143">Non</span><span class="sxs-lookup"><span data-stu-id="13133-143">No</span></span> |
| <span data-ttu-id="13133-144">nullValue</span><span class="sxs-lookup"><span data-stu-id="13133-144">nullValue</span></span> |<span data-ttu-id="13133-145">Un ou plusieurs caractères utilisés pour représenter une valeur null.</span><span class="sxs-lookup"><span data-stu-id="13133-145">One or more characters used to represent a null value.</span></span> |<span data-ttu-id="13133-146">Un ou plusieurs caractères.</span><span class="sxs-lookup"><span data-stu-id="13133-146">One or more characters.</span></span> <span data-ttu-id="13133-147">Les valeurs **par défaut** sont **« \N » et « NULL »** en lecture, et **« \N »** en écriture.</span><span class="sxs-lookup"><span data-stu-id="13133-147">The **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="13133-148">Non</span><span class="sxs-lookup"><span data-stu-id="13133-148">No</span></span> |
| <span data-ttu-id="13133-149">encodingName</span><span class="sxs-lookup"><span data-stu-id="13133-149">encodingName</span></span> |<span data-ttu-id="13133-150">Spécifier le nom d'encodage.</span><span class="sxs-lookup"><span data-stu-id="13133-150">Specify the encoding name.</span></span> |<span data-ttu-id="13133-151">Une liste de noms d’encodage valides.</span><span class="sxs-lookup"><span data-stu-id="13133-151">A valid encoding name.</span></span> <span data-ttu-id="13133-152">Consultez : [Propriété Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="13133-152">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="13133-153">Exemple : windows-1250 ou shift_jis.</span><span class="sxs-lookup"><span data-stu-id="13133-153">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="13133-154">La valeur **par défaut** est **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="13133-154">The **default** value is **UTF-8**.</span></span> |<span data-ttu-id="13133-155">Non</span><span class="sxs-lookup"><span data-stu-id="13133-155">No</span></span> |
| <span data-ttu-id="13133-156">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="13133-156">firstRowAsHeader</span></span> |<span data-ttu-id="13133-157">Spécifie si la première ligne doit être considérée comme un en-tête.</span><span class="sxs-lookup"><span data-stu-id="13133-157">Specifies whether to consider the first row as a header.</span></span> <span data-ttu-id="13133-158">Pour un jeu de données d’entrée, Data Factory lit la première ligne comme un en-tête.</span><span class="sxs-lookup"><span data-stu-id="13133-158">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="13133-159">Pour un jeu de données de sortie, Data Factory écrit la première ligne comme un en-tête.</span><span class="sxs-lookup"><span data-stu-id="13133-159">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="13133-160">Voir [Scénarios d’utilisation de `firstRowAsHeader` et `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) pour obtenir des exemples de scénarios.</span><span class="sxs-lookup"><span data-stu-id="13133-160">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="13133-161">true</span><span class="sxs-lookup"><span data-stu-id="13133-161">True</span></span><br/><span data-ttu-id="13133-162">**false (valeur par défaut)**</span><span class="sxs-lookup"><span data-stu-id="13133-162">**False (default)**</span></span> |<span data-ttu-id="13133-163">Non</span><span class="sxs-lookup"><span data-stu-id="13133-163">No</span></span> |
| <span data-ttu-id="13133-164">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="13133-164">skipLineCount</span></span> |<span data-ttu-id="13133-165">Indique le nombre de lignes à ignorer lors de la lecture des données à partir des fichiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="13133-165">Indicates the number of rows to skip when reading data from input files.</span></span> <span data-ttu-id="13133-166">Si skipLineCount et firstRowAsHeader sont spécifiés, les lignes sont d’abord ignorées, puis les informations d’en-tête sont lues à partir du fichier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="13133-166">If both skipLineCount and firstRowAsHeader are specified, the lines are skipped first and then the header information is read from the input file.</span></span> <br/><br/><span data-ttu-id="13133-167">Voir [Scénarios d’utilisation de `firstRowAsHeader` et `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) pour obtenir des exemples de scénarios.</span><span class="sxs-lookup"><span data-stu-id="13133-167">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="13133-168">Entier </span><span class="sxs-lookup"><span data-stu-id="13133-168">Integer</span></span> |<span data-ttu-id="13133-169">Non</span><span class="sxs-lookup"><span data-stu-id="13133-169">No</span></span> |
| <span data-ttu-id="13133-170">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="13133-170">treatEmptyAsNull</span></span> |<span data-ttu-id="13133-171">Spécifie si une chaîne null ou vide doit être traitée comme une valeur null lors de la lecture des données à partir d’un fichier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="13133-171">Specifies whether to treat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="13133-172">**True (valeur par défaut)**</span><span class="sxs-lookup"><span data-stu-id="13133-172">**True (default)**</span></span><br/><span data-ttu-id="13133-173">False</span><span class="sxs-lookup"><span data-stu-id="13133-173">False</span></span> |<span data-ttu-id="13133-174">Non</span><span class="sxs-lookup"><span data-stu-id="13133-174">No</span></span> |

#### <a name="textformat-example"></a><span data-ttu-id="13133-175">Exemple pour TextFormat</span><span class="sxs-lookup"><span data-stu-id="13133-175">TextFormat example</span></span>
<span data-ttu-id="13133-176">L'exemple suivant illustre certaines des propriétés de format pour TextFormat.</span><span class="sxs-lookup"><span data-stu-id="13133-176">The following sample shows some of the format properties for TextFormat.</span></span>

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

<span data-ttu-id="13133-177">Pour utiliser un caractère `escapeChar` au lieu de `quoteChar`, remplacez la ligne par `quoteChar`, avec le caractère escapeChar suivant :</span><span class="sxs-lookup"><span data-stu-id="13133-177">To use an `escapeChar` instead of `quoteChar`, replace the line with `quoteChar` with the following escapeChar:</span></span>

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="13133-178">Scénarios d’utilisation de firstRowAsHeader et skipLineCount</span><span class="sxs-lookup"><span data-stu-id="13133-178">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="13133-179">Vous copiez à partir d’une source hors fichier vers un fichier texte et vous souhaitez ajouter une ligne d’en-tête qui contient les métadonnées de schéma (par exemple : schéma SQL).</span><span class="sxs-lookup"><span data-stu-id="13133-179">You are copying from a non-file source to a text file and would like to add a header line containing the schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="13133-180">Définissez le paramètre `firstRowAsHeader` sur true dans le jeu de données de sortie pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="13133-180">Specify `firstRowAsHeader` as true in the output dataset for this scenario.</span></span>
* <span data-ttu-id="13133-181">Vous copiez à partir d’un fichier texte contenant une ligne d’en-tête vers un récepteur hors fichier et souhaitez supprimer cette ligne.</span><span class="sxs-lookup"><span data-stu-id="13133-181">You are copying from a text file containing a header line to a non-file sink and would like to drop that line.</span></span> <span data-ttu-id="13133-182">Définissez le paramètre `firstRowAsHeader` sur true dans le jeu de données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="13133-182">Specify `firstRowAsHeader` as true in the input dataset.</span></span>
* <span data-ttu-id="13133-183">Vous copiez à partir d’un fichier texte et souhaitez ignorer quelques lignes au début, qui ne contiennent ni données, ni informations d’en-tête.</span><span class="sxs-lookup"><span data-stu-id="13133-183">You are copying from a text file and want to skip a few lines at the beginning that contain no data or header information.</span></span> <span data-ttu-id="13133-184">Spécifiez le paramètre `skipLineCount` pour indiquer le nombre de lignes à ignorer.</span><span class="sxs-lookup"><span data-stu-id="13133-184">Specify `skipLineCount` to indicate the number of lines to be skipped.</span></span> <span data-ttu-id="13133-185">Si le reste du fichier contient une ligne d’en-tête, vous pouvez également spécifier `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="13133-185">If the rest of the file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="13133-186">Si les paramètres `skipLineCount` et `firstRowAsHeader` sont tous deux spécifiés, les lignes sont d’abord ignorées, puis les informations d’en-tête sont lues à partir du fichier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="13133-186">If both `skipLineCount` and `firstRowAsHeader` are specified, the lines are skipped first and then the header information is read from the input file</span></span>

### <a name="specifying-jsonformat"></a><span data-ttu-id="13133-187">Définition de JsonFormat</span><span class="sxs-lookup"><span data-stu-id="13133-187">Specifying JsonFormat</span></span>
<span data-ttu-id="13133-188">Pour en savoir plus sur **l’importation ou l’exportation de fichiers JSON en l’état dans ou à partir d’Azure Cosmos DB**, consultez la section [Importer/exporter des documents JSON](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) dans le connecteur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="13133-188">To **import/export JSON files as-is into/from Azure Cosmos DB**, see [Import/export JSON documents](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section in the Azure Cosmos DB connector with details.</span></span>

<span data-ttu-id="13133-189">Si vous souhaitez analyser des fichiers JSON ou écrire des données au format JSON, définissez la propriété `format` `type` sur **JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="13133-189">If you want to parse the JSON files or write the data in JSON format, set the `format` `type` property to **JsonFormat**.</span></span> <span data-ttu-id="13133-190">Vous pouvez également spécifier les propriétés **facultatives** suivantes, dans la section `format`.</span><span class="sxs-lookup"><span data-stu-id="13133-190">You can also specify the following **optional** properties in the `format` section.</span></span> <span data-ttu-id="13133-191">Consultez la section [Exemple pour JsonFormat](#jsonformat-example) pour en savoir plus sur la méthode de configuration à suivre.</span><span class="sxs-lookup"><span data-stu-id="13133-191">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span>

| <span data-ttu-id="13133-192">Propriété</span><span class="sxs-lookup"><span data-stu-id="13133-192">Property</span></span> | <span data-ttu-id="13133-193">Description</span><span class="sxs-lookup"><span data-stu-id="13133-193">Description</span></span> | <span data-ttu-id="13133-194">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="13133-194">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13133-195">filePattern</span><span class="sxs-lookup"><span data-stu-id="13133-195">filePattern</span></span> |<span data-ttu-id="13133-196">Indiquez le modèle des données stockées dans chaque fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="13133-196">Indicate the pattern of data stored in each JSON file.</span></span> <span data-ttu-id="13133-197">Les valeurs autorisées sont les suivantes : **setOfObjects** et **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="13133-197">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="13133-198">La valeur **par défaut** est **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="13133-198">The **default** value is **setOfObjects**.</span></span> <span data-ttu-id="13133-199">Consultez la section [Modèles de fichiers JSON](#json-file-patterns) pour en savoir plus sur ces modèles.</span><span class="sxs-lookup"><span data-stu-id="13133-199">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="13133-200">Non</span><span class="sxs-lookup"><span data-stu-id="13133-200">No</span></span> |
| <span data-ttu-id="13133-201">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="13133-201">jsonNodeReference</span></span> | <span data-ttu-id="13133-202">Si vous souhaitez effectuer une itération et extraire des données à partir des objets situés à l’intérieur d’un champ de tableau présentant le même modèle, spécifiez le chemin d’accès JSON de ce tableau.</span><span class="sxs-lookup"><span data-stu-id="13133-202">If you want to iterate and extract data from the objects inside an array field with the same pattern, specify the JSON path of that array.</span></span> <span data-ttu-id="13133-203">Cette propriété est uniquement prise en charge lors de la copie de données de fichiers JSON.</span><span class="sxs-lookup"><span data-stu-id="13133-203">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="13133-204">Non</span><span class="sxs-lookup"><span data-stu-id="13133-204">No</span></span> |
| <span data-ttu-id="13133-205">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="13133-205">jsonPathDefinition</span></span> | <span data-ttu-id="13133-206">Spécifiez l’expression de chemin JSON pour chaque mappage de colonne avec un nom de colonne personnalisé (commencez par une lettre minuscule).</span><span class="sxs-lookup"><span data-stu-id="13133-206">Specify the JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="13133-207">Cette propriété est uniquement prise en charge lors de la copie de données à partir de fichiers JSON, et vous pouvez extraire des données d’un objet ou d’un tableau.</span><span class="sxs-lookup"><span data-stu-id="13133-207">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="13133-208">Pour les champs situés sous l’objet racine, commencez par $ racine ; pour ceux qui se trouvent dans le tableau sélectionné par la propriété `jsonNodeReference`, commencez par l’élément de tableau.</span><span class="sxs-lookup"><span data-stu-id="13133-208">For fields under root object, start with root $; for fields inside the array chosen by `jsonNodeReference` property, start from the array element.</span></span> <span data-ttu-id="13133-209">Consultez la section [Exemple pour JsonFormat](#jsonformat-example) pour en savoir plus sur la méthode de configuration à suivre.</span><span class="sxs-lookup"><span data-stu-id="13133-209">See [JsonFormat example](#jsonformat-example) section on how to configure.</span></span> | <span data-ttu-id="13133-210">Non</span><span class="sxs-lookup"><span data-stu-id="13133-210">No</span></span> |
| <span data-ttu-id="13133-211">encodingName</span><span class="sxs-lookup"><span data-stu-id="13133-211">encodingName</span></span> |<span data-ttu-id="13133-212">Spécifiez le nom du codage.</span><span class="sxs-lookup"><span data-stu-id="13133-212">Specify the encoding name.</span></span> <span data-ttu-id="13133-213">Pour obtenir une liste des noms d’encodage valides, consultez la propriété [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) .</span><span class="sxs-lookup"><span data-stu-id="13133-213">For the list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="13133-214">Par exemple : windows-1250 ou shift_jis.</span><span class="sxs-lookup"><span data-stu-id="13133-214">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="13133-215">La valeur **par défaut** est : **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="13133-215">The **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="13133-216">Non</span><span class="sxs-lookup"><span data-stu-id="13133-216">No</span></span> |
| <span data-ttu-id="13133-217">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="13133-217">nestingSeparator</span></span> |<span data-ttu-id="13133-218">Caractère utilisé pour séparer les niveaux d'imbrication.</span><span class="sxs-lookup"><span data-stu-id="13133-218">Character that is used to separate nesting levels.</span></span> <span data-ttu-id="13133-219">La valeur par défaut est . (point).</span><span class="sxs-lookup"><span data-stu-id="13133-219">The default value is '.' (dot).</span></span> |<span data-ttu-id="13133-220">Non</span><span class="sxs-lookup"><span data-stu-id="13133-220">No</span></span> |

#### <a name="json-file-patterns"></a><span data-ttu-id="13133-221">Modèles de fichiers JSON</span><span class="sxs-lookup"><span data-stu-id="13133-221">JSON file patterns</span></span>

<span data-ttu-id="13133-222">L’activité de copie peut analyser les modèles de fichiers JSON ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="13133-222">Copy activity can parse below patterns of JSON files:</span></span>

- <span data-ttu-id="13133-223">**Type I : setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="13133-223">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="13133-224">Chaque fichier contient un objet unique, ou plusieurs objets concaténés/délimités par des lignes.</span><span class="sxs-lookup"><span data-stu-id="13133-224">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="13133-225">Quand cette option est sélectionnée dans un jeu de données de sortie, l’activité de copie produit un seul fichier JSON contenant un objet par ligne (format délimité par des lignes).</span><span class="sxs-lookup"><span data-stu-id="13133-225">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="13133-226">**Exemple de fichier JSON à un seul objet**</span><span class="sxs-lookup"><span data-stu-id="13133-226">**single object JSON example**</span></span>

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

    * <span data-ttu-id="13133-227">**Exemple de fichier JSON incluant des objets délimités par des lignes**</span><span class="sxs-lookup"><span data-stu-id="13133-227">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="13133-228">**Exemple de fichier JSON incluant des objets concaténés**</span><span class="sxs-lookup"><span data-stu-id="13133-228">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="13133-229">**Type II : arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="13133-229">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="13133-230">Chaque fichier contient un tableau d’objets.</span><span class="sxs-lookup"><span data-stu-id="13133-230">Each file contains an array of objects.</span></span>

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

#### <a name="jsonformat-example"></a><span data-ttu-id="13133-231">Exemple pour JsonFormat</span><span class="sxs-lookup"><span data-stu-id="13133-231">JsonFormat example</span></span>

<span data-ttu-id="13133-232">**Cas 1 : Copie de données à partir de fichiers JSON**</span><span class="sxs-lookup"><span data-stu-id="13133-232">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="13133-233">Vous trouverez ci-dessous deux types d’exemples de copie des données à partir de fichiers JSON, ainsi que les points génériques à noter :</span><span class="sxs-lookup"><span data-stu-id="13133-233">See below two types of samples when copying data from JSON files, and the generic points to note:</span></span>

<span data-ttu-id="13133-234">**Exemple 1 : Extraire des données d’objet et de tableau**</span><span class="sxs-lookup"><span data-stu-id="13133-234">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="13133-235">Dans cet exemple, un objet JSON racine doit correspondre à un seul enregistrement dans la table de résultats.</span><span class="sxs-lookup"><span data-stu-id="13133-235">In this sample, you expect one root JSON object maps to single record in tabular result.</span></span> <span data-ttu-id="13133-236">Prenons un fichier JSON avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="13133-236">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="13133-237">Vous voulez copier ce contenu dans un tableau SQL Azure au format suivant, en extrayant les données des objets et du tableau :</span><span class="sxs-lookup"><span data-stu-id="13133-237">and you want to copy it into an Azure SQL table in the following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="13133-238">id</span><span class="sxs-lookup"><span data-stu-id="13133-238">id</span></span> | <span data-ttu-id="13133-239">deviceType</span><span class="sxs-lookup"><span data-stu-id="13133-239">deviceType</span></span> | <span data-ttu-id="13133-240">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="13133-240">targetResourceType</span></span> | <span data-ttu-id="13133-241">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="13133-241">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="13133-242">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="13133-242">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="13133-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="13133-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="13133-244">PC</span><span class="sxs-lookup"><span data-stu-id="13133-244">PC</span></span> | <span data-ttu-id="13133-245">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="13133-245">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="13133-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="13133-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="13133-247">13/01/2017 11:24:37</span><span class="sxs-lookup"><span data-stu-id="13133-247">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="13133-248">Le jeu de données d’entrée présentant le type **JsonFormat** est défini comme suit : (définition partielle présentant uniquement les éléments pertinents).</span><span class="sxs-lookup"><span data-stu-id="13133-248">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="13133-249">Plus précisément :</span><span class="sxs-lookup"><span data-stu-id="13133-249">More specifically:</span></span>

- <span data-ttu-id="13133-250">La section `structure` définit les noms de colonne personnalisés et le type de données correspondant lors de la conversion des données au format tabulaire.</span><span class="sxs-lookup"><span data-stu-id="13133-250">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="13133-251">Cette section est **facultative**, sauf si vous avez besoin d’effectuer un mappage de colonne.</span><span class="sxs-lookup"><span data-stu-id="13133-251">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="13133-252">Pour en savoir plus, voir [Spécification de la définition de la structure des jeux de données rectangulaires](#specifying-structure-definition-for-rectangular-datasets).</span><span class="sxs-lookup"><span data-stu-id="13133-252">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="13133-253">Le paramètre `jsonPathDefinition` indique le chemin JSON de chaque colonne indiquant l’emplacement à partir duquel les données sont extraites.</span><span class="sxs-lookup"><span data-stu-id="13133-253">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="13133-254">Pour copier les données d’un tableau, vous pouvez utiliser **array[x].property** pour extraire la valeur de la propriété spécifiée à partir de l’objet x, ou vous pouvez utiliser **array[*].property** pour trouver la valeur de tout objet contenant cette propriété.</span><span class="sxs-lookup"><span data-stu-id="13133-254">To copy data from array, you can use **array[x].property** to extract value of the given property from the xth object, or you can use **array[*].property** to find the value from any object containing such property.</span></span>

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

<span data-ttu-id="13133-255">**Exemple 2 : application croisée de plusieurs objets avec le même modèle à partir d’un tableau**</span><span class="sxs-lookup"><span data-stu-id="13133-255">**Sample 2: cross apply multiple objects with the same pattern from array**</span></span>

<span data-ttu-id="13133-256">Dans cet exemple, vous voulez transformer un objet JSON racine en plusieurs enregistrements dans la table de résultats.</span><span class="sxs-lookup"><span data-stu-id="13133-256">In this sample, you expect to transform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="13133-257">Prenons un fichier JSON avec le contenu suivant :</span><span class="sxs-lookup"><span data-stu-id="13133-257">If you have a JSON file with the following content:</span></span>  

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
<span data-ttu-id="13133-258">Vous souhaitez copier ce fichier dans une table SQL Azure au format suivant, en mettant à plat les données se trouvant dans le tableau et en effectuant une jointure croisée avec les informations racines communes :</span><span class="sxs-lookup"><span data-stu-id="13133-258">and you want to copy it into an Azure SQL table in the following format, by flattening the data inside the array and cross join with the common root info:</span></span>

| <span data-ttu-id="13133-259">ordernumber</span><span class="sxs-lookup"><span data-stu-id="13133-259">ordernumber</span></span> | <span data-ttu-id="13133-260">orderdate</span><span class="sxs-lookup"><span data-stu-id="13133-260">orderdate</span></span> | <span data-ttu-id="13133-261">order_pd</span><span class="sxs-lookup"><span data-stu-id="13133-261">order_pd</span></span> | <span data-ttu-id="13133-262">order_price</span><span class="sxs-lookup"><span data-stu-id="13133-262">order_price</span></span> | <span data-ttu-id="13133-263">city</span><span class="sxs-lookup"><span data-stu-id="13133-263">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="13133-264">01</span><span class="sxs-lookup"><span data-stu-id="13133-264">01</span></span> | <span data-ttu-id="13133-265">20170122</span><span class="sxs-lookup"><span data-stu-id="13133-265">20170122</span></span> | <span data-ttu-id="13133-266">P1</span><span class="sxs-lookup"><span data-stu-id="13133-266">P1</span></span> | <span data-ttu-id="13133-267">23</span><span class="sxs-lookup"><span data-stu-id="13133-267">23</span></span> | <span data-ttu-id="13133-268">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="13133-268">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="13133-269">01</span><span class="sxs-lookup"><span data-stu-id="13133-269">01</span></span> | <span data-ttu-id="13133-270">20170122</span><span class="sxs-lookup"><span data-stu-id="13133-270">20170122</span></span> | <span data-ttu-id="13133-271">P2</span><span class="sxs-lookup"><span data-stu-id="13133-271">P2</span></span> | <span data-ttu-id="13133-272">13.</span><span class="sxs-lookup"><span data-stu-id="13133-272">13</span></span> | <span data-ttu-id="13133-273">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="13133-273">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="13133-274">01</span><span class="sxs-lookup"><span data-stu-id="13133-274">01</span></span> | <span data-ttu-id="13133-275">20170122</span><span class="sxs-lookup"><span data-stu-id="13133-275">20170122</span></span> | <span data-ttu-id="13133-276">P3</span><span class="sxs-lookup"><span data-stu-id="13133-276">P3</span></span> | <span data-ttu-id="13133-277">231</span><span class="sxs-lookup"><span data-stu-id="13133-277">231</span></span> | <span data-ttu-id="13133-278">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="13133-278">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="13133-279">Le jeu de données d’entrée présentant le type **JsonFormat** est défini comme suit : (définition partielle présentant uniquement les éléments pertinents).</span><span class="sxs-lookup"><span data-stu-id="13133-279">The input dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="13133-280">Plus précisément :</span><span class="sxs-lookup"><span data-stu-id="13133-280">More specifically:</span></span>

- <span data-ttu-id="13133-281">La section `structure` définit les noms de colonne personnalisés et le type de données correspondant lors de la conversion des données au format tabulaire.</span><span class="sxs-lookup"><span data-stu-id="13133-281">`structure` section defines the customized column names and the corresponding data type while converting to tabular data.</span></span> <span data-ttu-id="13133-282">Cette section est **facultative**, sauf si vous avez besoin d’effectuer un mappage de colonne.</span><span class="sxs-lookup"><span data-stu-id="13133-282">This section is **optional** unless you need to do column mapping.</span></span> <span data-ttu-id="13133-283">Pour en savoir plus, voir [Spécification de la définition de la structure des jeux de données rectangulaires](#specifying-structure-definition-for-rectangular-datasets).</span><span class="sxs-lookup"><span data-stu-id="13133-283">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="13133-284">Le paramètre `jsonNodeReference` indique que les données doivent être itérées et extraites des objets présentant le même modèle sous « orderlines » dans le **tableau**.</span><span class="sxs-lookup"><span data-stu-id="13133-284">`jsonNodeReference` indicates to iterate and extract data from the objects with the same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="13133-285">Le paramètre `jsonPathDefinition` indique le chemin JSON de chaque colonne indiquant l’emplacement à partir duquel les données sont extraites.</span><span class="sxs-lookup"><span data-stu-id="13133-285">`jsonPathDefinition` specifies the JSON path for each column indicating where to extract the data from.</span></span> <span data-ttu-id="13133-286">Dans cet exemple, les éléments « ordernumber », « orderdate » et « city » se trouvent sous l’objet racine associé au chemin JSON commençant par « $. », tandis que les éléments « order_pd » et « order_price » sont définis avec le chemin d’accès dérivé de l’élément de tableau sans « $.».</span><span class="sxs-lookup"><span data-stu-id="13133-286">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from the array element without "$.".</span></span>

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

<span data-ttu-id="13133-287">**Notez les points suivants :**</span><span class="sxs-lookup"><span data-stu-id="13133-287">**Note the following points:**</span></span>

* <span data-ttu-id="13133-288">Si les éléments `structure` et `jsonPathDefinition` ne sont pas définis dans le jeu de données Data Factory, l’activité de copie détecte le schéma à partir du premier objet et aplatit l’objet entier.</span><span class="sxs-lookup"><span data-stu-id="13133-288">If the `structure` and `jsonPathDefinition` are not defined in the Data Factory dataset, the Copy Activity detects the schema from the first object and flatten the whole object.</span></span>
* <span data-ttu-id="13133-289">Si l’entrée JSON contient un tableau, l’activité de copie convertit la valeur du tableau entier en une chaîne, par défaut.</span><span class="sxs-lookup"><span data-stu-id="13133-289">If the JSON input has an array, by default the Copy Activity converts the entire array value into a string.</span></span> <span data-ttu-id="13133-290">Vous pouvez choisir d’extraire des données de cette dernière à l’aide de `jsonNodeReference` et/ou `jsonPathDefinition`, ou ignorer cette opération en ne la spécifiant pas dans `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="13133-290">You can choose to extract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="13133-291">S’il y a plusieurs noms identiques au même niveau, l’activité de copie sélectionne le dernier nom.</span><span class="sxs-lookup"><span data-stu-id="13133-291">If there are duplicate names at the same level, the Copy Activity picks the last one.</span></span>
* <span data-ttu-id="13133-292">Les noms de propriété respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="13133-292">Property names are case-sensitive.</span></span> <span data-ttu-id="13133-293">Quand deux propriétés de même nom ont une casse différente, elles sont considérées comme deux propriétés distinctes.</span><span class="sxs-lookup"><span data-stu-id="13133-293">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="13133-294">**Cas 2 : Écriture de données dans un fichier JSON**</span><span class="sxs-lookup"><span data-stu-id="13133-294">**Case 2: Writing data to JSON file**</span></span>

<span data-ttu-id="13133-295">Vous disposez de la table ci-dessous dans votre base de données SQL :</span><span class="sxs-lookup"><span data-stu-id="13133-295">If you have below table in SQL Database:</span></span>

| <span data-ttu-id="13133-296">id</span><span class="sxs-lookup"><span data-stu-id="13133-296">id</span></span> | <span data-ttu-id="13133-297">order_date</span><span class="sxs-lookup"><span data-stu-id="13133-297">order_date</span></span> | <span data-ttu-id="13133-298">order_price</span><span class="sxs-lookup"><span data-stu-id="13133-298">order_price</span></span> | <span data-ttu-id="13133-299">order_by</span><span class="sxs-lookup"><span data-stu-id="13133-299">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="13133-300">1</span><span class="sxs-lookup"><span data-stu-id="13133-300">1</span></span> | <span data-ttu-id="13133-301">20170119</span><span class="sxs-lookup"><span data-stu-id="13133-301">20170119</span></span> | <span data-ttu-id="13133-302">2000</span><span class="sxs-lookup"><span data-stu-id="13133-302">2000</span></span> | <span data-ttu-id="13133-303">David</span><span class="sxs-lookup"><span data-stu-id="13133-303">David</span></span> |
| <span data-ttu-id="13133-304">2</span><span class="sxs-lookup"><span data-stu-id="13133-304">2</span></span> | <span data-ttu-id="13133-305">20170120</span><span class="sxs-lookup"><span data-stu-id="13133-305">20170120</span></span> | <span data-ttu-id="13133-306">3 500</span><span class="sxs-lookup"><span data-stu-id="13133-306">3500</span></span> | <span data-ttu-id="13133-307">Patrick</span><span class="sxs-lookup"><span data-stu-id="13133-307">Patrick</span></span> |
| <span data-ttu-id="13133-308">3</span><span class="sxs-lookup"><span data-stu-id="13133-308">3</span></span> | <span data-ttu-id="13133-309">20170121</span><span class="sxs-lookup"><span data-stu-id="13133-309">20170121</span></span> | <span data-ttu-id="13133-310">4000</span><span class="sxs-lookup"><span data-stu-id="13133-310">4000</span></span> | <span data-ttu-id="13133-311">Jason</span><span class="sxs-lookup"><span data-stu-id="13133-311">Jason</span></span> |

<span data-ttu-id="13133-312">Pour chaque enregistrement, vous voulez écrire des données dans un objet JSON, au format suivant :</span><span class="sxs-lookup"><span data-stu-id="13133-312">and for each record, you expect to write to a JSON object in below format:</span></span>
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

<span data-ttu-id="13133-313">Le jeu de données de sortie présentant le type **JsonFormat** est défini comme suit : (définition partielle présentant uniquement les éléments pertinents).</span><span class="sxs-lookup"><span data-stu-id="13133-313">The output dataset with **JsonFormat** type is defined as follows: (partial definition with only the relevant parts).</span></span> <span data-ttu-id="13133-314">Plus précisément, la section `structure` définit les noms des propriétés personnalisés dans le fichier de destination ; le paramètre `nestingSeparator` (valeur par défaut : «. ») vous permet d’identifier la couche d’imbrication à partir du nom.</span><span class="sxs-lookup"><span data-stu-id="13133-314">More specifically, `structure` section defines the customized property names in destination file, `nestingSeparator` (default is ".") will be used to identify the nest layer from the name.</span></span> <span data-ttu-id="13133-315">Cette section est **facultative**, sauf si vous souhaitez modifier le nom de propriété par rapport au nom de la colonne source, ou imbriquer certaines propriétés.</span><span class="sxs-lookup"><span data-stu-id="13133-315">This section is **optional** unless you want to change the property name comparing with source column name, or nest some of the properties.</span></span>

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

### <a name="specifying-avroformat"></a><span data-ttu-id="13133-316">Définition d'AvroFormat</span><span class="sxs-lookup"><span data-stu-id="13133-316">Specifying AvroFormat</span></span>
<span data-ttu-id="13133-317">Si vous souhaitez analyser des fichiers Avro ou écrire des données au format Avro, définissez la propriété `format` `type` sur **AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="13133-317">If you want to parse the Avro files or write the data in Avro format, set the `format` `type` property to **AvroFormat**.</span></span> <span data-ttu-id="13133-318">Il est inutile de spécifier des propriétés dans la partie Format de la section typeProperties.</span><span class="sxs-lookup"><span data-stu-id="13133-318">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="13133-319">Exemple :</span><span class="sxs-lookup"><span data-stu-id="13133-319">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="13133-320">Pour utiliser le format Avro dans une table Hive, vous pouvez faire référence au [didacticiel Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="13133-320">To use Avro format in a Hive table, you can refer to [Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="13133-321">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="13133-321">Note the following points:</span></span>  

* <span data-ttu-id="13133-322">[Les types de données complexes](http://avro.apache.org/docs/current/spec.html#schema_complex) ne sont pas pris en charge (enregistrements, enums, tableaux, cartes, unions et fixes).</span><span class="sxs-lookup"><span data-stu-id="13133-322">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions and fixed).</span></span>

### <a name="specifying-orcformat"></a><span data-ttu-id="13133-323">Spécification d’OrcFormat</span><span class="sxs-lookup"><span data-stu-id="13133-323">Specifying OrcFormat</span></span>
<span data-ttu-id="13133-324">Si vous souhaitez analyser des fichiers ORC ou écrire des données au format ORC, définissez la propriété `format` `type` sur **OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="13133-324">If you want to parse the ORC files or write the data in ORC format, set the `format` `type` property to **OrcFormat**.</span></span> <span data-ttu-id="13133-325">Il est inutile de spécifier des propriétés dans la partie Format de la section typeProperties.</span><span class="sxs-lookup"><span data-stu-id="13133-325">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="13133-326">Exemple :</span><span class="sxs-lookup"><span data-stu-id="13133-326">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="13133-327">Si vous ne copiez pas les fichiers ORC **tels quels** entre les magasins de données locaux et cloud, vous devez installer JRE 8 (Java Runtime Environment) sur votre machine de passerelle.</span><span class="sxs-lookup"><span data-stu-id="13133-327">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="13133-328">La passerelle 64 bits requiert un environnement JRE 64 bits et que la passerelle 32 bits nécessite un environnement JRE 32 bits.</span><span class="sxs-lookup"><span data-stu-id="13133-328">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="13133-329">Ces deux versions sont disponibles [ici](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="13133-329">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="13133-330">Sélectionnez la bonne version.</span><span class="sxs-lookup"><span data-stu-id="13133-330">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="13133-331">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="13133-331">Note the following points:</span></span>

* <span data-ttu-id="13133-332">Les types de données complexes ne sont pas pris en charge (STRUCT, MAP, LIST, UNION)</span><span class="sxs-lookup"><span data-stu-id="13133-332">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="13133-333">Le fichier ORC a trois [options liées à la compression](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="13133-333">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="13133-334">Data Factory prend en charge la lecture des données du fichier ORC dans tous ces formats compressés.</span><span class="sxs-lookup"><span data-stu-id="13133-334">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="13133-335">Il utilise le codec de compression se trouvant dans les métadonnées pour lire les données.</span><span class="sxs-lookup"><span data-stu-id="13133-335">It uses the compression codec is in the metadata to read the data.</span></span> <span data-ttu-id="13133-336">Toutefois, lors de l’écriture dans un fichier ORC, Data Factory choisit ZLIB, qui est la valeur par défaut pour ORC.</span><span class="sxs-lookup"><span data-stu-id="13133-336">However, when writing to an ORC file, Data Factory chooses ZLIB, which is the default for ORC.</span></span> <span data-ttu-id="13133-337">Actuellement, il n’existe aucune option permettant de remplacer ce comportement.</span><span class="sxs-lookup"><span data-stu-id="13133-337">Currently, there is no option to override this behavior.</span></span>

### <a name="specifying-parquetformat"></a><span data-ttu-id="13133-338">Spécification de ParquetFormat</span><span class="sxs-lookup"><span data-stu-id="13133-338">Specifying ParquetFormat</span></span>
<span data-ttu-id="13133-339">Si vous souhaitez analyser des fichiers Parquet ou écrire des données au format Parquet, définissez la propriété `format` `type` sur **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="13133-339">If you want to parse the Parquet files or write the data in Parquet format, set the `format` `type` property to **ParquetFormat**.</span></span> <span data-ttu-id="13133-340">Il est inutile de spécifier des propriétés dans la partie Format de la section typeProperties.</span><span class="sxs-lookup"><span data-stu-id="13133-340">You do not need to specify any properties in the Format section within the typeProperties section.</span></span> <span data-ttu-id="13133-341">Exemple :</span><span class="sxs-lookup"><span data-stu-id="13133-341">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="13133-342">Si vous ne copiez pas les fichiers Parquet **tels quels** entre les magasins de données locaux et cloud, vous devez installer JRE 8 (Java Runtime Environment) sur votre machine de passerelle.</span><span class="sxs-lookup"><span data-stu-id="13133-342">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need to install the JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="13133-343">La passerelle 64 bits requiert un environnement JRE 64 bits et que la passerelle 32 bits nécessite un environnement JRE 32 bits.</span><span class="sxs-lookup"><span data-stu-id="13133-343">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="13133-344">Ces deux versions sont disponibles [ici](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="13133-344">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="13133-345">Sélectionnez la bonne version.</span><span class="sxs-lookup"><span data-stu-id="13133-345">Choose the appropriate one.</span></span>
>
>

<span data-ttu-id="13133-346">Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="13133-346">Note the following points:</span></span>

* <span data-ttu-id="13133-347">Les types de données complexes ne sont pas pris en charge (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="13133-347">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="13133-348">Le fichier Parquet offre les options de compression suivantes : NONE, SNAPPY, GZIP et LZO.</span><span class="sxs-lookup"><span data-stu-id="13133-348">Parquet file has the following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="13133-349">Data Factory prend en charge la lecture des données du fichier ORC dans tous ces formats compressés.</span><span class="sxs-lookup"><span data-stu-id="13133-349">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="13133-350">Il utilise le codec de compression se trouvant dans les métadonnées pour lire les données.</span><span class="sxs-lookup"><span data-stu-id="13133-350">It uses the compression codec in the metadata to read the data.</span></span> <span data-ttu-id="13133-351">Toutefois, lors de l’écriture dans un fichier Parquet, Data Factory choisit SNAPPY, qui est la valeur par défaut pour le format Parquet.</span><span class="sxs-lookup"><span data-stu-id="13133-351">However, when writing to a Parquet file, Data Factory chooses SNAPPY, which is the default for Parquet format.</span></span> <span data-ttu-id="13133-352">Actuellement, il n’existe aucune option permettant de remplacer ce comportement.</span><span class="sxs-lookup"><span data-stu-id="13133-352">Currently, there is no option to override this behavior.</span></span>
