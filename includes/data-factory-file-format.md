## <a name="specifying-formats"></a><span data-ttu-id="77aa6-101">Spécification des formats</span><span class="sxs-lookup"><span data-stu-id="77aa6-101">Specifying formats</span></span>
<span data-ttu-id="77aa6-102">Azure Data Factory prend en charge hello les types de format suivants :</span><span class="sxs-lookup"><span data-stu-id="77aa6-102">Azure Data Factory supports hello following format types:</span></span>

* [<span data-ttu-id="77aa6-103">Format Texte</span><span class="sxs-lookup"><span data-stu-id="77aa6-103">Text Format</span></span>](#specifying-textformat)
* [<span data-ttu-id="77aa6-104">Format JSON</span><span class="sxs-lookup"><span data-stu-id="77aa6-104">JSON Format</span></span>](#specifying-jsonformat)
* [<span data-ttu-id="77aa6-105">Format Avro</span><span class="sxs-lookup"><span data-stu-id="77aa6-105">Avro Format</span></span>](#specifying-avroformat)
* [<span data-ttu-id="77aa6-106">Format ORC</span><span class="sxs-lookup"><span data-stu-id="77aa6-106">ORC Format</span></span>](#specifying-orcformat)
* [<span data-ttu-id="77aa6-107">Format Parquet</span><span class="sxs-lookup"><span data-stu-id="77aa6-107">Parquet Format</span></span>](#specifying-parquetformat)

### <a name="specifying-textformat"></a><span data-ttu-id="77aa6-108">Définition de TextFormat</span><span class="sxs-lookup"><span data-stu-id="77aa6-108">Specifying TextFormat</span></span>
<span data-ttu-id="77aa6-109">Si vous souhaitez que les fichiers de texte hello tooparse ou écrivez les données de salutation au format texte, la valeur hello `format` `type` propriété trop**TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="77aa6-109">If you want tooparse hello text files or write hello data in text format, set hello `format` `type` property too**TextFormat**.</span></span> <span data-ttu-id="77aa6-110">Vous pouvez également spécifier les éléments suivants de hello **facultatif** propriétés Bonjour `format` section.</span><span class="sxs-lookup"><span data-stu-id="77aa6-110">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="77aa6-111">Consultez [TextFormat exemple](#textformat-example) section sur la façon de tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="77aa6-111">See [TextFormat example](#textformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="77aa6-112">Propriété</span><span class="sxs-lookup"><span data-stu-id="77aa6-112">Property</span></span> | <span data-ttu-id="77aa6-113">Description</span><span class="sxs-lookup"><span data-stu-id="77aa6-113">Description</span></span> | <span data-ttu-id="77aa6-114">Valeurs autorisées</span><span class="sxs-lookup"><span data-stu-id="77aa6-114">Allowed values</span></span> | <span data-ttu-id="77aa6-115">Requis</span><span class="sxs-lookup"><span data-stu-id="77aa6-115">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="77aa6-116">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="77aa6-116">columnDelimiter</span></span> |<span data-ttu-id="77aa6-117">caractère de Hello utilisé tooseparate colonnes dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="77aa6-117">hello character used tooseparate columns in a file.</span></span> <span data-ttu-id="77aa6-118">Vous pouvez envisager d’un caractère non imprimable rares qui se ne trouve pas probablement toouse dans vos données : par exemple, spécifiez « \u0001 » qui représente le début de titre (SOH).</span><span class="sxs-lookup"><span data-stu-id="77aa6-118">You can consider toouse a rare unprintable char which not likely exists in your data: e.g. specify "\u0001" which represents Start of Heading (SOH).</span></span> |<span data-ttu-id="77aa6-119">Un seul caractère est autorisé.</span><span class="sxs-lookup"><span data-stu-id="77aa6-119">Only one character is allowed.</span></span> <span data-ttu-id="77aa6-120">Hello **par défaut** valeur est **virgule («, »)**.</span><span class="sxs-lookup"><span data-stu-id="77aa6-120">hello **default** value is **comma (',')**.</span></span> <br/><br/><span data-ttu-id="77aa6-121">toouse un caractère Unicode, consultez trop[caractères Unicode](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello code correspondant pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="77aa6-121">toouse an Unicode character, refer too[Unicode Characters](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello corresponding code for it.</span></span> |<span data-ttu-id="77aa6-122">Non</span><span class="sxs-lookup"><span data-stu-id="77aa6-122">No</span></span> |
| <span data-ttu-id="77aa6-123">rowDelimiter</span><span class="sxs-lookup"><span data-stu-id="77aa6-123">rowDelimiter</span></span> |<span data-ttu-id="77aa6-124">caractère de Hello utilisé tooseparate lignes dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="77aa6-124">hello character used tooseparate rows in a file.</span></span> |<span data-ttu-id="77aa6-125">Un seul caractère est autorisé.</span><span class="sxs-lookup"><span data-stu-id="77aa6-125">Only one character is allowed.</span></span> <span data-ttu-id="77aa6-126">Hello **par défaut** valeur est une des valeurs suivantes lors de la lecture de hello : **[« \r\n », « \r », « \n »]** et **« \r\n »** lors de l’écriture.</span><span class="sxs-lookup"><span data-stu-id="77aa6-126">hello **default** value is any of hello following values on read: **["\r\n", "\r", "\n"]** and **"\r\n"** on write.</span></span> |<span data-ttu-id="77aa6-127">Non</span><span class="sxs-lookup"><span data-stu-id="77aa6-127">No</span></span> |
| <span data-ttu-id="77aa6-128">escapeChar</span><span class="sxs-lookup"><span data-stu-id="77aa6-128">escapeChar</span></span> |<span data-ttu-id="77aa6-129">un caractère spécial Hello utilisé tooescape un délimiteur de colonne dans le contenu du fichier d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="77aa6-129">hello special character used tooescape a column delimiter in hello content of input file.</span></span> <br/><br/><span data-ttu-id="77aa6-130">Vous ne pouvez pas spécifier à la fois escapeChar et quoteChar pour une table.</span><span class="sxs-lookup"><span data-stu-id="77aa6-130">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="77aa6-131">Un seul caractère est autorisé.</span><span class="sxs-lookup"><span data-stu-id="77aa6-131">Only one character is allowed.</span></span> <span data-ttu-id="77aa6-132">Aucune valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="77aa6-132">No default value.</span></span> <br/><br/><span data-ttu-id="77aa6-133">Exemple : Si vous utilisez une virgule («, ») comme délimiteur de colonne hello mais que vous voulez que virgule toohave hello dans le texte hello (exemple : « Hello, world »), vous pouvez définir « $» comme caractère d’échappement hello et utilisez la chaîne « $Hello, world » dans la source de hello.</span><span class="sxs-lookup"><span data-stu-id="77aa6-133">Example: if you have comma (',') as hello column delimiter but you want toohave hello comma character in hello text (example: "Hello, world"), you can define ‘$’ as hello escape character and use string "Hello$, world" in hello source.</span></span> |<span data-ttu-id="77aa6-134">Non</span><span class="sxs-lookup"><span data-stu-id="77aa6-134">No</span></span> |
| <span data-ttu-id="77aa6-135">quoteChar</span><span class="sxs-lookup"><span data-stu-id="77aa6-135">quoteChar</span></span> |<span data-ttu-id="77aa6-136">caractère de Hello utilisé tooquote une valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="77aa6-136">hello character used tooquote a string value.</span></span> <span data-ttu-id="77aa6-137">séparateurs de ligne et de colonne Hello à l’intérieur des guillemets hello sont traités en tant que partie de la valeur de chaîne hello.</span><span class="sxs-lookup"><span data-stu-id="77aa6-137">hello column and row delimiters inside hello quote characters would be treated as part of hello string value.</span></span> <span data-ttu-id="77aa6-138">Cette propriété est applicable tooboth entrée et de sortie des jeux de données.</span><span class="sxs-lookup"><span data-stu-id="77aa6-138">This property is applicable tooboth input and output datasets.</span></span><br/><br/><span data-ttu-id="77aa6-139">Vous ne pouvez pas spécifier à la fois escapeChar et quoteChar pour une table.</span><span class="sxs-lookup"><span data-stu-id="77aa6-139">You cannot specify both escapeChar and quoteChar for a table.</span></span> |<span data-ttu-id="77aa6-140">Un seul caractère est autorisé.</span><span class="sxs-lookup"><span data-stu-id="77aa6-140">Only one character is allowed.</span></span> <span data-ttu-id="77aa6-141">Aucune valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="77aa6-141">No default value.</span></span> <br/><br/><span data-ttu-id="77aa6-142">Par exemple, si vous utilisez une virgule («, ») comme délimiteur de colonne hello, mais vous voulez que virgule toohave dans le texte hello (exemple : < Hello, world >), vous pouvez définir « (guillemets doubles) comme hello guillemet et utilisez hello chaîne « Hello, world » dans la source de hello.</span><span class="sxs-lookup"><span data-stu-id="77aa6-142">For example, if you have comma (',') as hello column delimiter but you want toohave comma character in hello text (example: <Hello, world>), you can define " (double quote) as hello quote character and use hello string "Hello, world" in hello source.</span></span> |<span data-ttu-id="77aa6-143">Non</span><span class="sxs-lookup"><span data-stu-id="77aa6-143">No</span></span> |
| <span data-ttu-id="77aa6-144">nullValue</span><span class="sxs-lookup"><span data-stu-id="77aa6-144">nullValue</span></span> |<span data-ttu-id="77aa6-145">Un ou plusieurs caractères utilisés toorepresent une valeur null.</span><span class="sxs-lookup"><span data-stu-id="77aa6-145">One or more characters used toorepresent a null value.</span></span> |<span data-ttu-id="77aa6-146">Un ou plusieurs caractères.</span><span class="sxs-lookup"><span data-stu-id="77aa6-146">One or more characters.</span></span> <span data-ttu-id="77aa6-147">Hello **par défaut** les valeurs sont **« \N » et « NULL »** lors de la lecture et **« \N »** lors de l’écriture.</span><span class="sxs-lookup"><span data-stu-id="77aa6-147">hello **default** values are **"\N" and "NULL"** on read and **"\N"** on write.</span></span> |<span data-ttu-id="77aa6-148">Non</span><span class="sxs-lookup"><span data-stu-id="77aa6-148">No</span></span> |
| <span data-ttu-id="77aa6-149">encodingName</span><span class="sxs-lookup"><span data-stu-id="77aa6-149">encodingName</span></span> |<span data-ttu-id="77aa6-150">Spécifiez le nom de codage hello.</span><span class="sxs-lookup"><span data-stu-id="77aa6-150">Specify hello encoding name.</span></span> |<span data-ttu-id="77aa6-151">Une liste de noms d’encodage valides.</span><span class="sxs-lookup"><span data-stu-id="77aa6-151">A valid encoding name.</span></span> <span data-ttu-id="77aa6-152">Consultez : [Propriété Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span><span class="sxs-lookup"><span data-stu-id="77aa6-152">see [Encoding.EncodingName Property](https://msdn.microsoft.com/library/system.text.encoding.aspx).</span></span> <span data-ttu-id="77aa6-153">Exemple : windows-1250 ou shift_jis.</span><span class="sxs-lookup"><span data-stu-id="77aa6-153">Example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="77aa6-154">Hello **par défaut** valeur est **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="77aa6-154">hello **default** value is **UTF-8**.</span></span> |<span data-ttu-id="77aa6-155">Non</span><span class="sxs-lookup"><span data-stu-id="77aa6-155">No</span></span> |
| <span data-ttu-id="77aa6-156">firstRowAsHeader</span><span class="sxs-lookup"><span data-stu-id="77aa6-156">firstRowAsHeader</span></span> |<span data-ttu-id="77aa6-157">Spécifie si tooconsider hello la première ligne comme un en-tête.</span><span class="sxs-lookup"><span data-stu-id="77aa6-157">Specifies whether tooconsider hello first row as a header.</span></span> <span data-ttu-id="77aa6-158">Pour un jeu de données d’entrée, Data Factory lit la première ligne comme un en-tête.</span><span class="sxs-lookup"><span data-stu-id="77aa6-158">For an input dataset, Data Factory reads first row as a header.</span></span> <span data-ttu-id="77aa6-159">Pour un jeu de données de sortie, Data Factory écrit la première ligne comme un en-tête.</span><span class="sxs-lookup"><span data-stu-id="77aa6-159">For an output dataset, Data Factory writes first row as a header.</span></span> <br/><br/><span data-ttu-id="77aa6-160">Voir [Scénarios d’utilisation de `firstRowAsHeader` et `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) pour obtenir des exemples de scénarios.</span><span class="sxs-lookup"><span data-stu-id="77aa6-160">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="77aa6-161">true</span><span class="sxs-lookup"><span data-stu-id="77aa6-161">True</span></span><br/><span data-ttu-id="77aa6-162">**false (valeur par défaut)**</span><span class="sxs-lookup"><span data-stu-id="77aa6-162">**False (default)**</span></span> |<span data-ttu-id="77aa6-163">Non</span><span class="sxs-lookup"><span data-stu-id="77aa6-163">No</span></span> |
| <span data-ttu-id="77aa6-164">skipLineCount</span><span class="sxs-lookup"><span data-stu-id="77aa6-164">skipLineCount</span></span> |<span data-ttu-id="77aa6-165">Indique le nombre de hello de lignes tooskip lors de la lecture des données à partir des fichiers d’entrée.</span><span class="sxs-lookup"><span data-stu-id="77aa6-165">Indicates hello number of rows tooskip when reading data from input files.</span></span> <span data-ttu-id="77aa6-166">Si skipLineCount et firstRowAsHeader sont spécifiés, les lignes de hello sont ignorées tout d’abord, et ensuite les informations d’en-tête hello sont en lecture à partir du fichier d’entrée de hello.</span><span class="sxs-lookup"><span data-stu-id="77aa6-166">If both skipLineCount and firstRowAsHeader are specified, hello lines are skipped first and then hello header information is read from hello input file.</span></span> <br/><br/><span data-ttu-id="77aa6-167">Voir [Scénarios d’utilisation de `firstRowAsHeader` et `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) pour obtenir des exemples de scénarios.</span><span class="sxs-lookup"><span data-stu-id="77aa6-167">See [Scenarios for using `firstRowAsHeader` and `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount) for sample scenarios.</span></span> |<span data-ttu-id="77aa6-168">Entier </span><span class="sxs-lookup"><span data-stu-id="77aa6-168">Integer</span></span> |<span data-ttu-id="77aa6-169">Non</span><span class="sxs-lookup"><span data-stu-id="77aa6-169">No</span></span> |
| <span data-ttu-id="77aa6-170">treatEmptyAsNull</span><span class="sxs-lookup"><span data-stu-id="77aa6-170">treatEmptyAsNull</span></span> |<span data-ttu-id="77aa6-171">Spécifie si la valeur tootreat null ou une chaîne vide comme une valeur null lorsque la lecture des données à partir d’un fichier d’entrée.</span><span class="sxs-lookup"><span data-stu-id="77aa6-171">Specifies whether tootreat null or empty string as a null value when reading data from an input file.</span></span> |<span data-ttu-id="77aa6-172">**True (valeur par défaut)**</span><span class="sxs-lookup"><span data-stu-id="77aa6-172">**True (default)**</span></span><br/><span data-ttu-id="77aa6-173">False</span><span class="sxs-lookup"><span data-stu-id="77aa6-173">False</span></span> |<span data-ttu-id="77aa6-174">Non</span><span class="sxs-lookup"><span data-stu-id="77aa6-174">No</span></span> |

#### <a name="textformat-example"></a><span data-ttu-id="77aa6-175">Exemple pour TextFormat</span><span class="sxs-lookup"><span data-stu-id="77aa6-175">TextFormat example</span></span>
<span data-ttu-id="77aa6-176">Hello exemple suivant illustre certaines des propriétés de format hello pour TextFormat.</span><span class="sxs-lookup"><span data-stu-id="77aa6-176">hello following sample shows some of hello format properties for TextFormat.</span></span>

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

<span data-ttu-id="77aa6-177">toouse un `escapeChar` au lieu de `quoteChar`, remplacez la ligne hello avec `quoteChar` avec hello suivant dont :</span><span class="sxs-lookup"><span data-stu-id="77aa6-177">toouse an `escapeChar` instead of `quoteChar`, replace hello line with `quoteChar` with hello following escapeChar:</span></span>

```json
"escapeChar": "$",
```

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a><span data-ttu-id="77aa6-178">Scénarios d’utilisation de firstRowAsHeader et skipLineCount</span><span class="sxs-lookup"><span data-stu-id="77aa6-178">Scenarios for using firstRowAsHeader and skipLineCount</span></span>
* <span data-ttu-id="77aa6-179">Vous copiez à partir d’un fichier de texte source de fichier non tooa et que vous souhaitez tooadd une ligne d’en-tête contenant des métadonnées de schéma hello (par exemple : schéma SQL).</span><span class="sxs-lookup"><span data-stu-id="77aa6-179">You are copying from a non-file source tooa text file and would like tooadd a header line containing hello schema metadata (for example: SQL schema).</span></span> <span data-ttu-id="77aa6-180">Spécifiez `firstRowAsHeader` comme true dans le dataset de sortie hello pour ce scénario.</span><span class="sxs-lookup"><span data-stu-id="77aa6-180">Specify `firstRowAsHeader` as true in hello output dataset for this scenario.</span></span>
* <span data-ttu-id="77aa6-181">Vous copiez à partir d’un fichier texte contenant un récepteur les fichiers d’en-tête ligne tooa et que vous souhaitez toodrop de ligne.</span><span class="sxs-lookup"><span data-stu-id="77aa6-181">You are copying from a text file containing a header line tooa non-file sink and would like toodrop that line.</span></span> <span data-ttu-id="77aa6-182">Spécifiez `firstRowAsHeader` comme true dans le jeu de données d’entrée hello.</span><span class="sxs-lookup"><span data-stu-id="77aa6-182">Specify `firstRowAsHeader` as true in hello input dataset.</span></span>
* <span data-ttu-id="77aa6-183">Vous copiez à partir d’un fichier texte et que vous souhaitez tooskip quelques lignes au début de hello qui ne contiennent aucune information d’en-tête ou de données.</span><span class="sxs-lookup"><span data-stu-id="77aa6-183">You are copying from a text file and want tooskip a few lines at hello beginning that contain no data or header information.</span></span> <span data-ttu-id="77aa6-184">Spécifiez `skipLineCount` nombre de hello tooindicate de lignes toobe ignorés.</span><span class="sxs-lookup"><span data-stu-id="77aa6-184">Specify `skipLineCount` tooindicate hello number of lines toobe skipped.</span></span> <span data-ttu-id="77aa6-185">Si le reste hello du fichier de hello contient une ligne d’en-tête, vous pouvez également spécifier `firstRowAsHeader`.</span><span class="sxs-lookup"><span data-stu-id="77aa6-185">If hello rest of hello file contains a header line, you can also specify `firstRowAsHeader`.</span></span> <span data-ttu-id="77aa6-186">Si les deux `skipLineCount` et `firstRowAsHeader` sont spécifiés, les lignes de hello sont ignorées tout d’abord, et ensuite les informations d’en-tête hello sont en lecture à partir du fichier d’entrée de hello</span><span class="sxs-lookup"><span data-stu-id="77aa6-186">If both `skipLineCount` and `firstRowAsHeader` are specified, hello lines are skipped first and then hello header information is read from hello input file</span></span>

### <a name="specifying-jsonformat"></a><span data-ttu-id="77aa6-187">Définition de JsonFormat</span><span class="sxs-lookup"><span data-stu-id="77aa6-187">Specifying JsonFormat</span></span>
<span data-ttu-id="77aa6-188">trop**importation/exportation de fichiers JSON en tant que-est dans/à partir de la base de données Azure Cosmos**, consultez [documents JSON d’importation/exportation](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section dans le connecteur de base de données Azure Cosmos hello avec les détails.</span><span class="sxs-lookup"><span data-stu-id="77aa6-188">too**import/export JSON files as-is into/from Azure Cosmos DB**, see [Import/export JSON documents](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) section in hello Azure Cosmos DB connector with details.</span></span>

<span data-ttu-id="77aa6-189">Si vous souhaitez que les fichiers JSON tooparse hello ou écrivez des données de salutation au format JSON, définissez hello `format` `type` propriété trop**JsonFormat**.</span><span class="sxs-lookup"><span data-stu-id="77aa6-189">If you want tooparse hello JSON files or write hello data in JSON format, set hello `format` `type` property too**JsonFormat**.</span></span> <span data-ttu-id="77aa6-190">Vous pouvez également spécifier les éléments suivants de hello **facultatif** propriétés Bonjour `format` section.</span><span class="sxs-lookup"><span data-stu-id="77aa6-190">You can also specify hello following **optional** properties in hello `format` section.</span></span> <span data-ttu-id="77aa6-191">Consultez [JsonFormat exemple](#jsonformat-example) section sur la façon de tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="77aa6-191">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span>

| <span data-ttu-id="77aa6-192">Propriété</span><span class="sxs-lookup"><span data-stu-id="77aa6-192">Property</span></span> | <span data-ttu-id="77aa6-193">Description</span><span class="sxs-lookup"><span data-stu-id="77aa6-193">Description</span></span> | <span data-ttu-id="77aa6-194">Obligatoire</span><span class="sxs-lookup"><span data-stu-id="77aa6-194">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="77aa6-195">filePattern</span><span class="sxs-lookup"><span data-stu-id="77aa6-195">filePattern</span></span> |<span data-ttu-id="77aa6-196">Indiquer le motif hello des données stockées dans chaque fichier JSON.</span><span class="sxs-lookup"><span data-stu-id="77aa6-196">Indicate hello pattern of data stored in each JSON file.</span></span> <span data-ttu-id="77aa6-197">Les valeurs autorisées sont les suivantes : **setOfObjects** et **arrayOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="77aa6-197">Allowed values are: **setOfObjects** and **arrayOfObjects**.</span></span> <span data-ttu-id="77aa6-198">Hello **par défaut** valeur est **setOfObjects**.</span><span class="sxs-lookup"><span data-stu-id="77aa6-198">hello **default** value is **setOfObjects**.</span></span> <span data-ttu-id="77aa6-199">Consultez la section [Modèles de fichiers JSON](#json-file-patterns) pour en savoir plus sur ces modèles.</span><span class="sxs-lookup"><span data-stu-id="77aa6-199">See [JSON file patterns](#json-file-patterns) section for details about these patterns.</span></span> |<span data-ttu-id="77aa6-200">Non</span><span class="sxs-lookup"><span data-stu-id="77aa6-200">No</span></span> |
| <span data-ttu-id="77aa6-201">jsonNodeReference</span><span class="sxs-lookup"><span data-stu-id="77aa6-201">jsonNodeReference</span></span> | <span data-ttu-id="77aa6-202">Si vous souhaitez tooiterate et extrayez des données à partir des objets hello à l’intérieur d’un tableau de champ par hello même modèle, spécifiez le chemin d’accès JSON hello de ce tableau.</span><span class="sxs-lookup"><span data-stu-id="77aa6-202">If you want tooiterate and extract data from hello objects inside an array field with hello same pattern, specify hello JSON path of that array.</span></span> <span data-ttu-id="77aa6-203">Cette propriété est uniquement prise en charge lors de la copie de données de fichiers JSON.</span><span class="sxs-lookup"><span data-stu-id="77aa6-203">This property is supported only when copying data from JSON files.</span></span> | <span data-ttu-id="77aa6-204">Non</span><span class="sxs-lookup"><span data-stu-id="77aa6-204">No</span></span> |
| <span data-ttu-id="77aa6-205">jsonPathDefinition</span><span class="sxs-lookup"><span data-stu-id="77aa6-205">jsonPathDefinition</span></span> | <span data-ttu-id="77aa6-206">Spécifiez l’expression de chemin JSON hello pour chaque mappage de colonne avec un nom de colonne personnalisée (commencent par des minuscules).</span><span class="sxs-lookup"><span data-stu-id="77aa6-206">Specify hello JSON path expression for each column mapping with a customized column name (start with lowercase).</span></span> <span data-ttu-id="77aa6-207">Cette propriété est uniquement prise en charge lors de la copie de données à partir de fichiers JSON, et vous pouvez extraire des données d’un objet ou d’un tableau.</span><span class="sxs-lookup"><span data-stu-id="77aa6-207">This property is supported only when copying data from JSON files, and you can extract data from object or array.</span></span> <br/><br/> <span data-ttu-id="77aa6-208">Pour les champs sous l’objet racine, commencer par $ de la racine ; pour les champs de tableau hello choisi par `jsonNodeReference` propriété, lancement à partir de l’élément de tableau hello.</span><span class="sxs-lookup"><span data-stu-id="77aa6-208">For fields under root object, start with root $; for fields inside hello array chosen by `jsonNodeReference` property, start from hello array element.</span></span> <span data-ttu-id="77aa6-209">Consultez [JsonFormat exemple](#jsonformat-example) section sur la façon de tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="77aa6-209">See [JsonFormat example](#jsonformat-example) section on how tooconfigure.</span></span> | <span data-ttu-id="77aa6-210">Non</span><span class="sxs-lookup"><span data-stu-id="77aa6-210">No</span></span> |
| <span data-ttu-id="77aa6-211">encodingName</span><span class="sxs-lookup"><span data-stu-id="77aa6-211">encodingName</span></span> |<span data-ttu-id="77aa6-212">Spécifiez le nom de codage hello.</span><span class="sxs-lookup"><span data-stu-id="77aa6-212">Specify hello encoding name.</span></span> <span data-ttu-id="77aa6-213">Pour hello la liste des noms de codage valides, consultez : [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) propriété.</span><span class="sxs-lookup"><span data-stu-id="77aa6-213">For hello list of valid encoding names, see: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) Property.</span></span> <span data-ttu-id="77aa6-214">Par exemple : windows-1250 ou shift_jis.</span><span class="sxs-lookup"><span data-stu-id="77aa6-214">For example: windows-1250 or shift_jis.</span></span> <span data-ttu-id="77aa6-215">Hello **par défaut** valeur est : **UTF-8**.</span><span class="sxs-lookup"><span data-stu-id="77aa6-215">hello **default** value is: **UTF-8**.</span></span> |<span data-ttu-id="77aa6-216">Non</span><span class="sxs-lookup"><span data-stu-id="77aa6-216">No</span></span> |
| <span data-ttu-id="77aa6-217">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="77aa6-217">nestingSeparator</span></span> |<span data-ttu-id="77aa6-218">Caractère utilisé tooseparate des niveaux d’imbrication.</span><span class="sxs-lookup"><span data-stu-id="77aa6-218">Character that is used tooseparate nesting levels.</span></span> <span data-ttu-id="77aa6-219">Hello la valeur par défaut est «. » (point).</span><span class="sxs-lookup"><span data-stu-id="77aa6-219">hello default value is '.' (dot).</span></span> |<span data-ttu-id="77aa6-220">Non</span><span class="sxs-lookup"><span data-stu-id="77aa6-220">No</span></span> |

#### <a name="json-file-patterns"></a><span data-ttu-id="77aa6-221">Modèles de fichiers JSON</span><span class="sxs-lookup"><span data-stu-id="77aa6-221">JSON file patterns</span></span>

<span data-ttu-id="77aa6-222">L’activité de copie peut analyser les modèles de fichiers JSON ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="77aa6-222">Copy activity can parse below patterns of JSON files:</span></span>

- <span data-ttu-id="77aa6-223">**Type I : setOfObjects**</span><span class="sxs-lookup"><span data-stu-id="77aa6-223">**Type I: setOfObjects**</span></span>

    <span data-ttu-id="77aa6-224">Chaque fichier contient un objet unique, ou plusieurs objets concaténés/délimités par des lignes.</span><span class="sxs-lookup"><span data-stu-id="77aa6-224">Each file contains single object, or line-delimited/concatenated multiple objects.</span></span> <span data-ttu-id="77aa6-225">Quand cette option est sélectionnée dans un jeu de données de sortie, l’activité de copie produit un seul fichier JSON contenant un objet par ligne (format délimité par des lignes).</span><span class="sxs-lookup"><span data-stu-id="77aa6-225">When this option is chosen in an output dataset, copy activity produces a single JSON file with each object per line (line-delimited).</span></span>

    * <span data-ttu-id="77aa6-226">**Exemple de fichier JSON à un seul objet**</span><span class="sxs-lookup"><span data-stu-id="77aa6-226">**single object JSON example**</span></span>

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

    * <span data-ttu-id="77aa6-227">**Exemple de fichier JSON incluant des objets délimités par des lignes**</span><span class="sxs-lookup"><span data-stu-id="77aa6-227">**line-delimited JSON example**</span></span>

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * <span data-ttu-id="77aa6-228">**Exemple de fichier JSON incluant des objets concaténés**</span><span class="sxs-lookup"><span data-stu-id="77aa6-228">**concatenated JSON example**</span></span>

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

- <span data-ttu-id="77aa6-229">**Type II : arrayOfObjects**</span><span class="sxs-lookup"><span data-stu-id="77aa6-229">**Type II: arrayOfObjects**</span></span>

    <span data-ttu-id="77aa6-230">Chaque fichier contient un tableau d’objets.</span><span class="sxs-lookup"><span data-stu-id="77aa6-230">Each file contains an array of objects.</span></span>

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

#### <a name="jsonformat-example"></a><span data-ttu-id="77aa6-231">Exemple pour JsonFormat</span><span class="sxs-lookup"><span data-stu-id="77aa6-231">JsonFormat example</span></span>

<span data-ttu-id="77aa6-232">**Cas 1 : Copie de données à partir de fichiers JSON**</span><span class="sxs-lookup"><span data-stu-id="77aa6-232">**Case 1: Copying data from JSON files**</span></span>

<span data-ttu-id="77aa6-233">Consultez ci-dessous les deux types d’exemples lors de la copie des données à partir de fichiers JSON et hello points générique toonote :</span><span class="sxs-lookup"><span data-stu-id="77aa6-233">See below two types of samples when copying data from JSON files, and hello generic points toonote:</span></span>

<span data-ttu-id="77aa6-234">**Exemple 1 : Extraire des données d’objet et de tableau**</span><span class="sxs-lookup"><span data-stu-id="77aa6-234">**Sample 1: extract data from object and array**</span></span>

<span data-ttu-id="77aa6-235">Dans cet exemple, vous prévoyez un objet JSON de racine mappe enregistrement toosingle de résultats tabulaire.</span><span class="sxs-lookup"><span data-stu-id="77aa6-235">In this sample, you expect one root JSON object maps toosingle record in tabular result.</span></span> <span data-ttu-id="77aa6-236">Si vous disposez d’un fichier JSON avec hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="77aa6-236">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="77aa6-237">et que vous souhaitez toocopy dans une table SQL Azure suivante de hello mettre en forme, en extrayant les données à partir des objets et de tableau :</span><span class="sxs-lookup"><span data-stu-id="77aa6-237">and you want toocopy it into an Azure SQL table in hello following format, by extracting data from both objects and array:</span></span>

| <span data-ttu-id="77aa6-238">id</span><span class="sxs-lookup"><span data-stu-id="77aa6-238">id</span></span> | <span data-ttu-id="77aa6-239">deviceType</span><span class="sxs-lookup"><span data-stu-id="77aa6-239">deviceType</span></span> | <span data-ttu-id="77aa6-240">targetResourceType</span><span class="sxs-lookup"><span data-stu-id="77aa6-240">targetResourceType</span></span> | <span data-ttu-id="77aa6-241">resourceManagmentProcessRunId</span><span class="sxs-lookup"><span data-stu-id="77aa6-241">resourceManagmentProcessRunId</span></span> | <span data-ttu-id="77aa6-242">occurrenceTime</span><span class="sxs-lookup"><span data-stu-id="77aa6-242">occurrenceTime</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="77aa6-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span><span class="sxs-lookup"><span data-stu-id="77aa6-243">ed0e4960-d9c5-11e6-85dc-d7996816aad3</span></span> | <span data-ttu-id="77aa6-244">PC</span><span class="sxs-lookup"><span data-stu-id="77aa6-244">PC</span></span> | <span data-ttu-id="77aa6-245">Microsoft.Compute/virtualMachines</span><span class="sxs-lookup"><span data-stu-id="77aa6-245">Microsoft.Compute/virtualMachines</span></span> | <span data-ttu-id="77aa6-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span><span class="sxs-lookup"><span data-stu-id="77aa6-246">827f8aaa-ab72-437c-ba48-d8917a7336a3</span></span> | <span data-ttu-id="77aa6-247">13/01/2017 11:24:37</span><span class="sxs-lookup"><span data-stu-id="77aa6-247">1/13/2017 11:24:37 AM</span></span> |

<span data-ttu-id="77aa6-248">jeu de données d’entrée Hello avec **JsonFormat** type est défini comme suit : (définition partielle avec uniquement les parties pertinentes hello).</span><span class="sxs-lookup"><span data-stu-id="77aa6-248">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="77aa6-249">Plus précisément :</span><span class="sxs-lookup"><span data-stu-id="77aa6-249">More specifically:</span></span>

- <span data-ttu-id="77aa6-250">`structure`section définit les noms de colonne de hello personnalisé et type de données correspondant hello lors de la conversion des données de tootabular.</span><span class="sxs-lookup"><span data-stu-id="77aa6-250">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="77aa6-251">Cette section est **facultatif** , sauf si vous avez besoin de mappage de colonne toodo.</span><span class="sxs-lookup"><span data-stu-id="77aa6-251">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="77aa6-252">Pour en savoir plus, voir [Spécification de la définition de la structure des jeux de données rectangulaires](#specifying-structure-definition-for-rectangular-datasets).</span><span class="sxs-lookup"><span data-stu-id="77aa6-252">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="77aa6-253">`jsonPathDefinition`Spécifie le chemin d’accès JSON hello pour chaque colonne qui indique où tooextract hello des données à partir de.</span><span class="sxs-lookup"><span data-stu-id="77aa6-253">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="77aa6-254">toocopy des données à partir du tableau, vous pouvez utiliser **propriété de tableau [x]** tooextract valeur hello donné de propriété d’objet de x hello, ou vous pouvez utiliser  **tableau [*] propriété** toofind valeur Hello à partir de n’importe quel objet contenant la propriété de ce type.</span><span class="sxs-lookup"><span data-stu-id="77aa6-254">toocopy data from array, you can use **array[x].property** tooextract value of hello given property from hello xth object, or you can use **array[*].property** toofind hello value from any object containing such property.</span></span>

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

<span data-ttu-id="77aa6-255">**Exemple 2 : Cross-appliquer plusieurs objets avec hello même modèle de tableau**</span><span class="sxs-lookup"><span data-stu-id="77aa6-255">**Sample 2: cross apply multiple objects with hello same pattern from array**</span></span>

<span data-ttu-id="77aa6-256">Cet exemple, vous prévoyez d’un objet JSON racine tootransform en plusieurs enregistrements dans la table de résultats.</span><span class="sxs-lookup"><span data-stu-id="77aa6-256">In this sample, you expect tootransform one root JSON object into multiple records in tabular result.</span></span> <span data-ttu-id="77aa6-257">Si vous disposez d’un fichier JSON avec hello suivant le contenu :</span><span class="sxs-lookup"><span data-stu-id="77aa6-257">If you have a JSON file with hello following content:</span></span>  

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
<span data-ttu-id="77aa6-258">et vous souhaitez toocopy dans une table SQL Azure suivante de hello mettre en forme, par la mise à plat de données hello à l’intérieur du tableau de hello et cross join avec des informations racine commun hello :</span><span class="sxs-lookup"><span data-stu-id="77aa6-258">and you want toocopy it into an Azure SQL table in hello following format, by flattening hello data inside hello array and cross join with hello common root info:</span></span>

| <span data-ttu-id="77aa6-259">ordernumber</span><span class="sxs-lookup"><span data-stu-id="77aa6-259">ordernumber</span></span> | <span data-ttu-id="77aa6-260">orderdate</span><span class="sxs-lookup"><span data-stu-id="77aa6-260">orderdate</span></span> | <span data-ttu-id="77aa6-261">order_pd</span><span class="sxs-lookup"><span data-stu-id="77aa6-261">order_pd</span></span> | <span data-ttu-id="77aa6-262">order_price</span><span class="sxs-lookup"><span data-stu-id="77aa6-262">order_price</span></span> | <span data-ttu-id="77aa6-263">city</span><span class="sxs-lookup"><span data-stu-id="77aa6-263">city</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="77aa6-264">01</span><span class="sxs-lookup"><span data-stu-id="77aa6-264">01</span></span> | <span data-ttu-id="77aa6-265">20170122</span><span class="sxs-lookup"><span data-stu-id="77aa6-265">20170122</span></span> | <span data-ttu-id="77aa6-266">P1</span><span class="sxs-lookup"><span data-stu-id="77aa6-266">P1</span></span> | <span data-ttu-id="77aa6-267">23</span><span class="sxs-lookup"><span data-stu-id="77aa6-267">23</span></span> | <span data-ttu-id="77aa6-268">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="77aa6-268">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="77aa6-269">01</span><span class="sxs-lookup"><span data-stu-id="77aa6-269">01</span></span> | <span data-ttu-id="77aa6-270">20170122</span><span class="sxs-lookup"><span data-stu-id="77aa6-270">20170122</span></span> | <span data-ttu-id="77aa6-271">P2</span><span class="sxs-lookup"><span data-stu-id="77aa6-271">P2</span></span> | <span data-ttu-id="77aa6-272">13.</span><span class="sxs-lookup"><span data-stu-id="77aa6-272">13</span></span> | <span data-ttu-id="77aa6-273">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="77aa6-273">[{"sanmateo":"No 1"}]</span></span> |
| <span data-ttu-id="77aa6-274">01</span><span class="sxs-lookup"><span data-stu-id="77aa6-274">01</span></span> | <span data-ttu-id="77aa6-275">20170122</span><span class="sxs-lookup"><span data-stu-id="77aa6-275">20170122</span></span> | <span data-ttu-id="77aa6-276">P3</span><span class="sxs-lookup"><span data-stu-id="77aa6-276">P3</span></span> | <span data-ttu-id="77aa6-277">231</span><span class="sxs-lookup"><span data-stu-id="77aa6-277">231</span></span> | <span data-ttu-id="77aa6-278">[{"sanmateo":"No 1"}]</span><span class="sxs-lookup"><span data-stu-id="77aa6-278">[{"sanmateo":"No 1"}]</span></span> |

<span data-ttu-id="77aa6-279">jeu de données d’entrée Hello avec **JsonFormat** type est défini comme suit : (définition partielle avec uniquement les parties pertinentes hello).</span><span class="sxs-lookup"><span data-stu-id="77aa6-279">hello input dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="77aa6-280">Plus précisément :</span><span class="sxs-lookup"><span data-stu-id="77aa6-280">More specifically:</span></span>

- <span data-ttu-id="77aa6-281">`structure`section définit les noms de colonne de hello personnalisé et type de données correspondant hello lors de la conversion des données de tootabular.</span><span class="sxs-lookup"><span data-stu-id="77aa6-281">`structure` section defines hello customized column names and hello corresponding data type while converting tootabular data.</span></span> <span data-ttu-id="77aa6-282">Cette section est **facultatif** , sauf si vous avez besoin de mappage de colonne toodo.</span><span class="sxs-lookup"><span data-stu-id="77aa6-282">This section is **optional** unless you need toodo column mapping.</span></span> <span data-ttu-id="77aa6-283">Pour en savoir plus, voir [Spécification de la définition de la structure des jeux de données rectangulaires](#specifying-structure-definition-for-rectangular-datasets).</span><span class="sxs-lookup"><span data-stu-id="77aa6-283">See [Specifying structure definition for rectangular datasets](#specifying-structure-definition-for-rectangular-datasets) section for more details.</span></span>
- <span data-ttu-id="77aa6-284">`jsonNodeReference`Indique tooiterate et extraire des données à partir des objets hello avec hello même motif sous **tableau** orderlines.</span><span class="sxs-lookup"><span data-stu-id="77aa6-284">`jsonNodeReference` indicates tooiterate and extract data from hello objects with hello same pattern under **array** orderlines.</span></span>
- <span data-ttu-id="77aa6-285">`jsonPathDefinition`Spécifie le chemin d’accès JSON hello pour chaque colonne qui indique où tooextract hello des données à partir de.</span><span class="sxs-lookup"><span data-stu-id="77aa6-285">`jsonPathDefinition` specifies hello JSON path for each column indicating where tooextract hello data from.</span></span> <span data-ttu-id="77aa6-286">Dans cet exemple, « ordernumber », « date » et « city » sont sous l’objet racine avec le chemin d’accès JSON en commençant par « $»., alors que « order_pd » et « order_price » sont définies avec le chemin d’accès dérivée de l’élément de tableau hello sans « $»..</span><span class="sxs-lookup"><span data-stu-id="77aa6-286">In this example, "ordernumber", "orderdate" and "city" are under root object with JSON path starting with "$.", while "order_pd" and "order_price" are defined with path derived from hello array element without "$.".</span></span>

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

<span data-ttu-id="77aa6-287">**Hello Notez les points suivants :**</span><span class="sxs-lookup"><span data-stu-id="77aa6-287">**Note hello following points:**</span></span>

* <span data-ttu-id="77aa6-288">Si hello `structure` et `jsonPathDefinition` ne sont pas définis dans le jeu de données Data Factory hello, hello détecte de l’activité de copie hello de schéma à partir du premier objet de hello et aplatir la totalité de l’objet hello.</span><span class="sxs-lookup"><span data-stu-id="77aa6-288">If hello `structure` and `jsonPathDefinition` are not defined in hello Data Factory dataset, hello Copy Activity detects hello schema from hello first object and flatten hello whole object.</span></span>
* <span data-ttu-id="77aa6-289">Si l’entrée JSON hello possède un tableau, par défaut, hello activité de copie convertit hello tableau entier valeur en une chaîne.</span><span class="sxs-lookup"><span data-stu-id="77aa6-289">If hello JSON input has an array, by default hello Copy Activity converts hello entire array value into a string.</span></span> <span data-ttu-id="77aa6-290">Vous pouvez choisir à l’aide de données de tooextract `jsonNodeReference` et/ou `jsonPathDefinition`, ou la passer en ne spécifiant dans `jsonPathDefinition`.</span><span class="sxs-lookup"><span data-stu-id="77aa6-290">You can choose tooextract data from it using `jsonNodeReference` and/or `jsonPathDefinition`, or skip it by not specifying it in `jsonPathDefinition`.</span></span>
* <span data-ttu-id="77aa6-291">S’il existe en double noms à hello même niveau, hello activité de copie sélectionne hello dernière.</span><span class="sxs-lookup"><span data-stu-id="77aa6-291">If there are duplicate names at hello same level, hello Copy Activity picks hello last one.</span></span>
* <span data-ttu-id="77aa6-292">Les noms de propriété respectent la casse.</span><span class="sxs-lookup"><span data-stu-id="77aa6-292">Property names are case-sensitive.</span></span> <span data-ttu-id="77aa6-293">Quand deux propriétés de même nom ont une casse différente, elles sont considérées comme deux propriétés distinctes.</span><span class="sxs-lookup"><span data-stu-id="77aa6-293">Two properties with same name but different casings are treated as two separate properties.</span></span>

<span data-ttu-id="77aa6-294">**Cas 2 : L’écriture du fichier tooJSON de données**</span><span class="sxs-lookup"><span data-stu-id="77aa6-294">**Case 2: Writing data tooJSON file**</span></span>

<span data-ttu-id="77aa6-295">Vous disposez de la table ci-dessous dans votre base de données SQL :</span><span class="sxs-lookup"><span data-stu-id="77aa6-295">If you have below table in SQL Database:</span></span>

| <span data-ttu-id="77aa6-296">id</span><span class="sxs-lookup"><span data-stu-id="77aa6-296">id</span></span> | <span data-ttu-id="77aa6-297">order_date</span><span class="sxs-lookup"><span data-stu-id="77aa6-297">order_date</span></span> | <span data-ttu-id="77aa6-298">order_price</span><span class="sxs-lookup"><span data-stu-id="77aa6-298">order_price</span></span> | <span data-ttu-id="77aa6-299">order_by</span><span class="sxs-lookup"><span data-stu-id="77aa6-299">order_by</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="77aa6-300">1</span><span class="sxs-lookup"><span data-stu-id="77aa6-300">1</span></span> | <span data-ttu-id="77aa6-301">20170119</span><span class="sxs-lookup"><span data-stu-id="77aa6-301">20170119</span></span> | <span data-ttu-id="77aa6-302">2000</span><span class="sxs-lookup"><span data-stu-id="77aa6-302">2000</span></span> | <span data-ttu-id="77aa6-303">David</span><span class="sxs-lookup"><span data-stu-id="77aa6-303">David</span></span> |
| <span data-ttu-id="77aa6-304">2</span><span class="sxs-lookup"><span data-stu-id="77aa6-304">2</span></span> | <span data-ttu-id="77aa6-305">20170120</span><span class="sxs-lookup"><span data-stu-id="77aa6-305">20170120</span></span> | <span data-ttu-id="77aa6-306">3 500</span><span class="sxs-lookup"><span data-stu-id="77aa6-306">3500</span></span> | <span data-ttu-id="77aa6-307">Patrick</span><span class="sxs-lookup"><span data-stu-id="77aa6-307">Patrick</span></span> |
| <span data-ttu-id="77aa6-308">3</span><span class="sxs-lookup"><span data-stu-id="77aa6-308">3</span></span> | <span data-ttu-id="77aa6-309">20170121</span><span class="sxs-lookup"><span data-stu-id="77aa6-309">20170121</span></span> | <span data-ttu-id="77aa6-310">4000</span><span class="sxs-lookup"><span data-stu-id="77aa6-310">4000</span></span> | <span data-ttu-id="77aa6-311">Jason</span><span class="sxs-lookup"><span data-stu-id="77aa6-311">Jason</span></span> |

<span data-ttu-id="77aa6-312">et pour chaque enregistrement, vous attendez l’objet JSON tooa à toowrite dans au-dessous de format :</span><span class="sxs-lookup"><span data-stu-id="77aa6-312">and for each record, you expect toowrite tooa JSON object in below format:</span></span>
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

<span data-ttu-id="77aa6-313">dataset à l’aide de sortie Hello **JsonFormat** type est défini comme suit : (définition partielle avec uniquement les parties pertinentes hello).</span><span class="sxs-lookup"><span data-stu-id="77aa6-313">hello output dataset with **JsonFormat** type is defined as follows: (partial definition with only hello relevant parts).</span></span> <span data-ttu-id="77aa6-314">Plus spécifiquement, `structure` section définit les noms de propriété hello personnalisé dans le fichier de destination, `nestingSeparator` (valeur par défaut est «. ») sera couche d’imbrication de hello tooidentify utilisé à partir du nom de hello.</span><span class="sxs-lookup"><span data-stu-id="77aa6-314">More specifically, `structure` section defines hello customized property names in destination file, `nestingSeparator` (default is ".") will be used tooidentify hello nest layer from hello name.</span></span> <span data-ttu-id="77aa6-315">Cette section est **facultatif** sauf si vous souhaitez que le nom de la propriété hello toochange la comparaison avec le nom de la colonne source, ou imbriquer des propriétés de hello.</span><span class="sxs-lookup"><span data-stu-id="77aa6-315">This section is **optional** unless you want toochange hello property name comparing with source column name, or nest some of hello properties.</span></span>

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

### <a name="specifying-avroformat"></a><span data-ttu-id="77aa6-316">Définition d'AvroFormat</span><span class="sxs-lookup"><span data-stu-id="77aa6-316">Specifying AvroFormat</span></span>
<span data-ttu-id="77aa6-317">Si vous souhaitez que les fichiers de Avro tooparse hello ou écrivez des données de hello dans le format Avro, la valeur hello `format` `type` propriété trop**AvroFormat**.</span><span class="sxs-lookup"><span data-stu-id="77aa6-317">If you want tooparse hello Avro files or write hello data in Avro format, set hello `format` `type` property too**AvroFormat**.</span></span> <span data-ttu-id="77aa6-318">Il est inutile toospecify toutes les propriétés de la section de Format hello dans la section de typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="77aa6-318">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="77aa6-319">Exemple :</span><span class="sxs-lookup"><span data-stu-id="77aa6-319">Example:</span></span>

```json
"format":
{
    "type": "AvroFormat",
}
```

<span data-ttu-id="77aa6-320">le format Avro toouse dans une table Hive, vous pouvez faire référence trop[didacticiel d’Apache Hive](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span><span class="sxs-lookup"><span data-stu-id="77aa6-320">toouse Avro format in a Hive table, you can refer too[Apache Hive’s tutorial](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).</span></span>

<span data-ttu-id="77aa6-321">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="77aa6-321">Note hello following points:</span></span>  

* <span data-ttu-id="77aa6-322">[Les types de données complexes](http://avro.apache.org/docs/current/spec.html#schema_complex) ne sont pas pris en charge (enregistrements, enums, tableaux, cartes, unions et fixes).</span><span class="sxs-lookup"><span data-stu-id="77aa6-322">[Complex data types](http://avro.apache.org/docs/current/spec.html#schema_complex) are not supported (records, enums, arrays, maps, unions and fixed).</span></span>

### <a name="specifying-orcformat"></a><span data-ttu-id="77aa6-323">Spécification d’OrcFormat</span><span class="sxs-lookup"><span data-stu-id="77aa6-323">Specifying OrcFormat</span></span>
<span data-ttu-id="77aa6-324">Si vous souhaitez tooparse hello ORC fichiers ou écrivez des données de hello dans format ORC, définissez hello `format` `type` propriété trop**OrcFormat**.</span><span class="sxs-lookup"><span data-stu-id="77aa6-324">If you want tooparse hello ORC files or write hello data in ORC format, set hello `format` `type` property too**OrcFormat**.</span></span> <span data-ttu-id="77aa6-325">Il est inutile toospecify toutes les propriétés de la section de Format hello dans la section de typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="77aa6-325">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="77aa6-326">Exemple :</span><span class="sxs-lookup"><span data-stu-id="77aa6-326">Example:</span></span>

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> <span data-ttu-id="77aa6-327">Si vous ne copiez pas les fichiers ORC **comme-est** entre locaux et cloud magasins de données, vous devez tooinstall hello 8 de JRE (Java Runtime Environment) sur votre ordinateur de passerelle.</span><span class="sxs-lookup"><span data-stu-id="77aa6-327">If you are not copying ORC files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="77aa6-328">La passerelle 64 bits requiert un environnement JRE 64 bits et que la passerelle 32 bits nécessite un environnement JRE 32 bits.</span><span class="sxs-lookup"><span data-stu-id="77aa6-328">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="77aa6-329">Ces deux versions sont disponibles [ici](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="77aa6-329">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="77aa6-330">Choisir hello approprié.</span><span class="sxs-lookup"><span data-stu-id="77aa6-330">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="77aa6-331">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="77aa6-331">Note hello following points:</span></span>

* <span data-ttu-id="77aa6-332">Les types de données complexes ne sont pas pris en charge (STRUCT, MAP, LIST, UNION)</span><span class="sxs-lookup"><span data-stu-id="77aa6-332">Complex data types are not supported (STRUCT, MAP, LIST, UNION)</span></span>
* <span data-ttu-id="77aa6-333">Le fichier ORC a trois [options liées à la compression](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span><span class="sxs-lookup"><span data-stu-id="77aa6-333">ORC file has three [compression-related options](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB, SNAPPY.</span></span> <span data-ttu-id="77aa6-334">Data Factory prend en charge la lecture des données du fichier ORC dans tous ces formats compressés.</span><span class="sxs-lookup"><span data-stu-id="77aa6-334">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="77aa6-335">Il utilise la compression de hello codec est dans les données de salutation métadonnées tooread hello.</span><span class="sxs-lookup"><span data-stu-id="77aa6-335">It uses hello compression codec is in hello metadata tooread hello data.</span></span> <span data-ttu-id="77aa6-336">Toutefois, lors de l’écriture de fichier ORC de tooan, Data Factory choisit ZLIB, qui est la valeur par défaut de hello pour ORC.</span><span class="sxs-lookup"><span data-stu-id="77aa6-336">However, when writing tooan ORC file, Data Factory chooses ZLIB, which is hello default for ORC.</span></span> <span data-ttu-id="77aa6-337">Il n’existe actuellement aucune toooverride option ce comportement.</span><span class="sxs-lookup"><span data-stu-id="77aa6-337">Currently, there is no option toooverride this behavior.</span></span>

### <a name="specifying-parquetformat"></a><span data-ttu-id="77aa6-338">Spécification de ParquetFormat</span><span class="sxs-lookup"><span data-stu-id="77aa6-338">Specifying ParquetFormat</span></span>
<span data-ttu-id="77aa6-339">Si vous souhaitez que les fichiers de Parquet tooparse hello ou écrivez des données de hello au format de Parquet, définissez hello `format` `type` propriété trop**ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="77aa6-339">If you want tooparse hello Parquet files or write hello data in Parquet format, set hello `format` `type` property too**ParquetFormat**.</span></span> <span data-ttu-id="77aa6-340">Il est inutile toospecify toutes les propriétés de la section de Format hello dans la section de typeProperties hello.</span><span class="sxs-lookup"><span data-stu-id="77aa6-340">You do not need toospecify any properties in hello Format section within hello typeProperties section.</span></span> <span data-ttu-id="77aa6-341">Exemple :</span><span class="sxs-lookup"><span data-stu-id="77aa6-341">Example:</span></span>

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> <span data-ttu-id="77aa6-342">Si vous ne copiez pas les fichiers Parquet **comme-est** entre locaux et cloud magasins de données, vous devez tooinstall hello 8 de JRE (Java Runtime Environment) sur votre ordinateur de passerelle.</span><span class="sxs-lookup"><span data-stu-id="77aa6-342">If you are not copying Parquet files **as-is** between on-premises and cloud data stores, you need tooinstall hello JRE 8 (Java Runtime Environment) on your gateway machine.</span></span> <span data-ttu-id="77aa6-343">La passerelle 64 bits requiert un environnement JRE 64 bits et que la passerelle 32 bits nécessite un environnement JRE 32 bits.</span><span class="sxs-lookup"><span data-stu-id="77aa6-343">A 64-bit gateway requires 64-bit JRE and 32-bit gateway requires 32-bit JRE.</span></span> <span data-ttu-id="77aa6-344">Ces deux versions sont disponibles [ici](http://go.microsoft.com/fwlink/?LinkId=808605).</span><span class="sxs-lookup"><span data-stu-id="77aa6-344">You can find both versions from [here](http://go.microsoft.com/fwlink/?LinkId=808605).</span></span> <span data-ttu-id="77aa6-345">Choisir hello approprié.</span><span class="sxs-lookup"><span data-stu-id="77aa6-345">Choose hello appropriate one.</span></span>
>
>

<span data-ttu-id="77aa6-346">Hello Notez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="77aa6-346">Note hello following points:</span></span>

* <span data-ttu-id="77aa6-347">Les types de données complexes ne sont pas pris en charge (MAP, LIST)</span><span class="sxs-lookup"><span data-stu-id="77aa6-347">Complex data types are not supported (MAP, LIST)</span></span>
* <span data-ttu-id="77aa6-348">Fichier de parquet a hello liés à la compression des options suivantes : NONE, SNAPPY, GZIP et LZO.</span><span class="sxs-lookup"><span data-stu-id="77aa6-348">Parquet file has hello following compression-related options: NONE, SNAPPY, GZIP, and LZO.</span></span> <span data-ttu-id="77aa6-349">Data Factory prend en charge la lecture des données du fichier ORC dans tous ces formats compressés.</span><span class="sxs-lookup"><span data-stu-id="77aa6-349">Data Factory supports reading data from ORC file in any of these compressed formats.</span></span> <span data-ttu-id="77aa6-350">Elle utilise le codec de compression hello dans les données de salutation métadonnées tooread hello.</span><span class="sxs-lookup"><span data-stu-id="77aa6-350">It uses hello compression codec in hello metadata tooread hello data.</span></span> <span data-ttu-id="77aa6-351">Toutefois, lors de l’écriture du fichier de Parquet tooa, fabrique de données choisit SNAPPY, valeur par défaut de hello pour le format Parquet.</span><span class="sxs-lookup"><span data-stu-id="77aa6-351">However, when writing tooa Parquet file, Data Factory chooses SNAPPY, which is hello default for Parquet format.</span></span> <span data-ttu-id="77aa6-352">Il n’existe actuellement aucune toooverride option ce comportement.</span><span class="sxs-lookup"><span data-stu-id="77aa6-352">Currently, there is no option toooverride this behavior.</span></span>
