---
title: "aaaLog API de collecteur de données Analytique HTTP | Documents Microsoft"
description: "Vous pouvez utiliser hello API du collecteur de données journal Analytique HTTP tooadd POST JSON toohello Analytique de journal référentiel de données à partir de n’importe quel client peut appeler hello API REST. Cet article décrit comment toouse hello API et a des exemples de données toopublish à l’aide de différents langages de programmation."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a><span data-ttu-id="93aba-104">Envoyer des données tooLog Analytique avec hello API du collecteur de données HTTP</span><span class="sxs-lookup"><span data-stu-id="93aba-104">Send data tooLog Analytics with hello HTTP Data Collector API</span></span>
<span data-ttu-id="93aba-105">Cet article vous explique comment toouse hello API de collecteur de données HTTP toosend données tooLog Analytique d’un client de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="93aba-105">This article shows you how toouse hello HTTP Data Collector API toosend data tooLog Analytics from a REST API client.</span></span>  <span data-ttu-id="93aba-106">Il décrit comment les tooformat les données collectées par le script ou l’application, incluez-le dans une demande et avoir cette demande d’autorisation de l’Analytique des journaux.</span><span class="sxs-lookup"><span data-stu-id="93aba-106">It describes how tooformat data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span></span>  <span data-ttu-id="93aba-107">Il est illustré par des exemples pour PowerShell, C# et Python.</span><span class="sxs-lookup"><span data-stu-id="93aba-107">Examples are provided for PowerShell, C#, and Python.</span></span>

## <a name="concepts"></a><span data-ttu-id="93aba-108">Concepts</span><span class="sxs-lookup"><span data-stu-id="93aba-108">Concepts</span></span>
<span data-ttu-id="93aba-109">Vous pouvez utiliser les API de collecteur de données HTTP toosend hello données tooLog Analytique à partir de n’importe quel client qui peut appeler une API REST.</span><span class="sxs-lookup"><span data-stu-id="93aba-109">You can use hello HTTP Data Collector API toosend data tooLog Analytics from any client that can call a REST API.</span></span>  <span data-ttu-id="93aba-110">Il peut s’agir d’un runbook dans Azure Automation qui recueille la gestion des données à partir d’Azure ou un autre cloud ou il peuvent être un système d’administration de remplacement qui utilise le journal Analytique tooconsolidate et analyser les données.</span><span class="sxs-lookup"><span data-stu-id="93aba-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics tooconsolidate and analyze data.</span></span>

<span data-ttu-id="93aba-111">Toutes les données dans le référentiel d’Analytique de journal hello est stocké comme un enregistrement avec un type d’enregistrement particulier.</span><span class="sxs-lookup"><span data-stu-id="93aba-111">All data in hello Log Analytics repository is stored as a record with a particular record type.</span></span>  <span data-ttu-id="93aba-112">Vous mettre en forme votre toohello toosend de données API du collecteur de données HTTP en tant que plusieurs enregistrements dans JSON.</span><span class="sxs-lookup"><span data-stu-id="93aba-112">You format your data toosend toohello HTTP Data Collector API as multiple records in JSON.</span></span>  <span data-ttu-id="93aba-113">Quand vous envoyez des données de hello, un enregistrement est créé dans le référentiel hello pour chaque enregistrement dans la charge utile de demande hello.</span><span class="sxs-lookup"><span data-stu-id="93aba-113">When you submit hello data, an individual record is created in hello repository for each record in hello request payload.</span></span>


![Présentation la collecte de données HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a><span data-ttu-id="93aba-115">Créer une demande</span><span class="sxs-lookup"><span data-stu-id="93aba-115">Create a request</span></span>
<span data-ttu-id="93aba-116">API de collecteur de données toouse hello HTTP, vous créez une demande POST qui comprend hello données toosend dans JavaScript Objet Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="93aba-116">toouse hello HTTP Data Collector API, you create a POST request that includes hello data toosend in JavaScript Object Notation (JSON).</span></span>  <span data-ttu-id="93aba-117">Bonjour trois tables liste hello attributs qui sont requis pour chaque demande.</span><span class="sxs-lookup"><span data-stu-id="93aba-117">hello next three tables list hello attributes that are required for each request.</span></span> <span data-ttu-id="93aba-118">Nous décrivons chaque attribut plus en détail plus loin dans l’article de hello.</span><span class="sxs-lookup"><span data-stu-id="93aba-118">We describe each attribute in more detail later in hello article.</span></span>

### <a name="request-uri"></a><span data-ttu-id="93aba-119">URI de demande</span><span class="sxs-lookup"><span data-stu-id="93aba-119">Request URI</span></span>
| <span data-ttu-id="93aba-120">Attribut</span><span class="sxs-lookup"><span data-stu-id="93aba-120">Attribute</span></span> | <span data-ttu-id="93aba-121">Propriété</span><span class="sxs-lookup"><span data-stu-id="93aba-121">Property</span></span> |
|:--- |:--- |
| <span data-ttu-id="93aba-122">Méthode</span><span class="sxs-lookup"><span data-stu-id="93aba-122">Method</span></span> |<span data-ttu-id="93aba-123">POST</span><span class="sxs-lookup"><span data-stu-id="93aba-123">POST</span></span> |
| <span data-ttu-id="93aba-124">URI</span><span class="sxs-lookup"><span data-stu-id="93aba-124">URI</span></span> |<span data-ttu-id="93aba-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span><span class="sxs-lookup"><span data-stu-id="93aba-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span></span> |
| <span data-ttu-id="93aba-126">Type de contenu</span><span class="sxs-lookup"><span data-stu-id="93aba-126">Content type</span></span> |<span data-ttu-id="93aba-127">application/json</span><span class="sxs-lookup"><span data-stu-id="93aba-127">application/json</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="93aba-128">Paramètres de l’URI de demande</span><span class="sxs-lookup"><span data-stu-id="93aba-128">Request URI parameters</span></span>
| <span data-ttu-id="93aba-129">Paramètre</span><span class="sxs-lookup"><span data-stu-id="93aba-129">Parameter</span></span> | <span data-ttu-id="93aba-130">Description</span><span class="sxs-lookup"><span data-stu-id="93aba-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="93aba-131">CustomerID</span><span class="sxs-lookup"><span data-stu-id="93aba-131">CustomerID</span></span> |<span data-ttu-id="93aba-132">Bonjour identificateur unique pour l’espace de travail de Microsoft Operations Management Suite hello.</span><span class="sxs-lookup"><span data-stu-id="93aba-132">hello unique identifier for hello Microsoft Operations Management Suite workspace.</span></span> |
| <span data-ttu-id="93aba-133">Ressource</span><span class="sxs-lookup"><span data-stu-id="93aba-133">Resource</span></span> |<span data-ttu-id="93aba-134">nom de la ressource Hello API : / api/logs.</span><span class="sxs-lookup"><span data-stu-id="93aba-134">hello API resource name: /api/logs.</span></span> |
| <span data-ttu-id="93aba-135">Version de l'API</span><span class="sxs-lookup"><span data-stu-id="93aba-135">API Version</span></span> |<span data-ttu-id="93aba-136">version de Hello de toouse hello API avec cette demande.</span><span class="sxs-lookup"><span data-stu-id="93aba-136">hello version of hello API toouse with this request.</span></span> <span data-ttu-id="93aba-137">Actuellement, il s’agit de 2016-04-01.</span><span class="sxs-lookup"><span data-stu-id="93aba-137">Currently, it's 2016-04-01.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="93aba-138">En-têtes de requête</span><span class="sxs-lookup"><span data-stu-id="93aba-138">Request headers</span></span>
| <span data-ttu-id="93aba-139">En-tête</span><span class="sxs-lookup"><span data-stu-id="93aba-139">Header</span></span> | <span data-ttu-id="93aba-140">Description</span><span class="sxs-lookup"><span data-stu-id="93aba-140">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="93aba-141">Autorisation</span><span class="sxs-lookup"><span data-stu-id="93aba-141">Authorization</span></span> |<span data-ttu-id="93aba-142">signature de l’autorisation de Hello.</span><span class="sxs-lookup"><span data-stu-id="93aba-142">hello authorization signature.</span></span> <span data-ttu-id="93aba-143">Plus loin dans l’article hello, vous pouvez lire sur l’en-tête de toocreate un code HMAC-SHA256.</span><span class="sxs-lookup"><span data-stu-id="93aba-143">Later in hello article, you can read about how toocreate an HMAC-SHA256 header.</span></span> |
| <span data-ttu-id="93aba-144">Log-Type</span><span class="sxs-lookup"><span data-stu-id="93aba-144">Log-Type</span></span> |<span data-ttu-id="93aba-145">Spécifier le type d’enregistrement de hello de données hello sont envoyées.</span><span class="sxs-lookup"><span data-stu-id="93aba-145">Specify hello record type of hello data that is being submitted.</span></span> <span data-ttu-id="93aba-146">Actuellement, type de journal hello prend en charge uniquement des caractères alphanumériques.</span><span class="sxs-lookup"><span data-stu-id="93aba-146">Currently, hello log type supports only alpha characters.</span></span> <span data-ttu-id="93aba-147">Il ne prend pas en charge les caractères numériques ou spéciaux.</span><span class="sxs-lookup"><span data-stu-id="93aba-147">It does not support numerics or special characters.</span></span> |
| <span data-ttu-id="93aba-148">x-ms-date</span><span class="sxs-lookup"><span data-stu-id="93aba-148">x-ms-date</span></span> |<span data-ttu-id="93aba-149">date de Hello cette demande hello a été traitée, au format RFC 1123.</span><span class="sxs-lookup"><span data-stu-id="93aba-149">hello date that hello request was processed, in RFC 1123 format.</span></span> |
| <span data-ttu-id="93aba-150">time-generated-field</span><span class="sxs-lookup"><span data-stu-id="93aba-150">time-generated-field</span></span> |<span data-ttu-id="93aba-151">nom Hello d’un champ dans les données de salutation qui contient l’horodatage de hello d’élément de données hello.</span><span class="sxs-lookup"><span data-stu-id="93aba-151">hello name of a field in hello data that contains hello timestamp of hello data item.</span></span> <span data-ttu-id="93aba-152">Si vous spécifiez un champ, son contenu est utilisé pour **TimeGenerated**.</span><span class="sxs-lookup"><span data-stu-id="93aba-152">If you specify a field then its contents are used for **TimeGenerated**.</span></span> <span data-ttu-id="93aba-153">Si ce champ n’est pas spécifié, la valeur par défaut pour hello **TimeGenerated** est temps de hello que hello message est intégré.</span><span class="sxs-lookup"><span data-stu-id="93aba-153">If this field isn’t specified, hello default for **TimeGenerated** is hello time that hello message is ingested.</span></span> <span data-ttu-id="93aba-154">contenu Hello hello du champ de message doit suivre le format hello ISO 8601 aaaa-MM-JJThh.</span><span class="sxs-lookup"><span data-stu-id="93aba-154">hello contents of hello message field should follow hello ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span></span> |

## <a name="authorization"></a><span data-ttu-id="93aba-155">Autorisation</span><span class="sxs-lookup"><span data-stu-id="93aba-155">Authorization</span></span>
<span data-ttu-id="93aba-156">Les API du collecteur de données journal Analytique HTTP de toohello demande doit inclure un en-tête d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="93aba-156">Any request toohello Log Analytics HTTP Data Collector API must include an authorization header.</span></span> <span data-ttu-id="93aba-157">tooauthenticate une demande, vous devez vous connecter demande hello avec hello primaire ou clé secondaire de hello pour espace de travail hello demande hello.</span><span class="sxs-lookup"><span data-stu-id="93aba-157">tooauthenticate a request, you must sign hello request with either hello primary or hello secondary key for hello workspace that is making hello request.</span></span> <span data-ttu-id="93aba-158">Ensuite, passer cette signature dans le cadre de la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="93aba-158">Then, pass that signature as part of hello request.</span></span>   

<span data-ttu-id="93aba-159">Voici le format hello pour l’en-tête d’autorisation hello :</span><span class="sxs-lookup"><span data-stu-id="93aba-159">Here's hello format for hello authorization header:</span></span>

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

<span data-ttu-id="93aba-160">*Id_espace_de_travail* est l’identificateur unique de hello pour l’espace de travail Operations Management Suite hello.</span><span class="sxs-lookup"><span data-stu-id="93aba-160">*WorkspaceID* is hello unique identifier for hello Operations Management Suite workspace.</span></span> <span data-ttu-id="93aba-161">*Signature* est un [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) qui est construit à partir de la demande de hello et puis calculée à l’aide de hello [algorithme SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span><span class="sxs-lookup"><span data-stu-id="93aba-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from hello request and then computed by using hello [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span></span> <span data-ttu-id="93aba-162">Ensuite, vous l’encodez à l’aide d’un encodage Base64.</span><span class="sxs-lookup"><span data-stu-id="93aba-162">Then, you encode it by using Base64 encoding.</span></span>

<span data-ttu-id="93aba-163">Utilisez cette hello tooencode de format **SharedKey** chaîne de signature :</span><span class="sxs-lookup"><span data-stu-id="93aba-163">Use this format tooencode hello **SharedKey** signature string:</span></span>

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

<span data-ttu-id="93aba-164">Voici un exemple de chaîne de signature :</span><span class="sxs-lookup"><span data-stu-id="93aba-164">Here's an example of a signature string:</span></span>

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

<span data-ttu-id="93aba-165">Lorsque vous avez chaîne de signature hello, encoder à l’aide de hello l’algorithme HMAC-SHA256 sur hello encodée en UTF-8 de chaîne et puis encoder résultat hello en Base64.</span><span class="sxs-lookup"><span data-stu-id="93aba-165">When you have hello signature string, encode it by using hello HMAC-SHA256 algorithm on hello UTF-8-encoded string, and then encode hello result as Base64.</span></span> <span data-ttu-id="93aba-166">Utilisez le format suivant :</span><span class="sxs-lookup"><span data-stu-id="93aba-166">Use this format:</span></span>

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

<span data-ttu-id="93aba-167">exemples de Hello dans les sections suivantes hello ont toohelp de code d’exemple vous créez un en-tête d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="93aba-167">hello samples in hello next sections have sample code toohelp you create an authorization header.</span></span>

## <a name="request-body"></a><span data-ttu-id="93aba-168">Corps de la demande</span><span class="sxs-lookup"><span data-stu-id="93aba-168">Request body</span></span>
<span data-ttu-id="93aba-169">corps de Hello du message de type hello doit être au format JSON.</span><span class="sxs-lookup"><span data-stu-id="93aba-169">hello body of hello message must be in JSON.</span></span> <span data-ttu-id="93aba-170">Elle doit inclure un ou plusieurs enregistrements avec des paires de nom et la valeur de la propriété hello dans ce format :</span><span class="sxs-lookup"><span data-stu-id="93aba-170">It must include one or more records with hello property name and value pairs in this format:</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

<span data-ttu-id="93aba-171">Vous pouvez traiter plusieurs enregistrements dans une demande unique à l’aide de hello suivant le format.</span><span class="sxs-lookup"><span data-stu-id="93aba-171">You can batch multiple records together in a single request by using hello following format.</span></span> <span data-ttu-id="93aba-172">Tous les enregistrements de hello doivent être hello même type d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93aba-172">All hello records must be hello same record type.</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a><span data-ttu-id="93aba-173">Type et propriétés d’enregistrement</span><span class="sxs-lookup"><span data-stu-id="93aba-173">Record type and properties</span></span>
<span data-ttu-id="93aba-174">Vous définissez un type d’enregistrement personnalisé lorsque vous envoyez des données via l’API du collecteur de données journal Analytique HTTP de hello.</span><span class="sxs-lookup"><span data-stu-id="93aba-174">You define a custom record type when you submit data through hello Log Analytics HTTP Data Collector API.</span></span> <span data-ttu-id="93aba-175">Actuellement, vous ne peut pas écrire les données tooexisting types d’enregistrements qui ont été créés par d’autres types de données et les solutions.</span><span class="sxs-lookup"><span data-stu-id="93aba-175">Currently, you can't write data tooexisting record types that were created by other data types and solutions.</span></span> <span data-ttu-id="93aba-176">Analytique de journal lit les données entrantes hello et crée ensuite des propriétés qui correspondent aux types de données hello de valeurs hello que vous entrez.</span><span class="sxs-lookup"><span data-stu-id="93aba-176">Log Analytics reads hello incoming data and then creates properties that match hello data types of hello values that you enter.</span></span>

<span data-ttu-id="93aba-177">Chaque toohello demande API Analytique de journal doit inclure un **Type de journal** en-tête dont le nom hello pour le type d’enregistrement hello.</span><span class="sxs-lookup"><span data-stu-id="93aba-177">Each request toohello Log Analytics API must include a **Log-Type** header with hello name for hello record type.</span></span> <span data-ttu-id="93aba-178">suffixe de Hello **_CL** nom toohello ajoutée automatiquement vous entrez toodistinguish à partir du journal des autres types en tant qu’un journal personnalisé.</span><span class="sxs-lookup"><span data-stu-id="93aba-178">hello suffix **_CL** is automatically appended toohello name you enter toodistinguish it from other log types as a custom log.</span></span> <span data-ttu-id="93aba-179">Par exemple, si vous entrez le nom de hello **MyNewRecordType**, Analytique de journal crée un enregistrement avec le type de hello **MyNewRecordType_CL**.</span><span class="sxs-lookup"><span data-stu-id="93aba-179">For example, if you enter hello name **MyNewRecordType**, Log Analytics creates a record with hello type **MyNewRecordType_CL**.</span></span> <span data-ttu-id="93aba-180">Cela évite tout conflit entre les noms de type créés par l’utilisateur et ceux fournis dans les solutions Microsoft actuelles ou futures.</span><span class="sxs-lookup"><span data-stu-id="93aba-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span></span>

<span data-ttu-id="93aba-181">type de données d’une propriété tooidentify, Analytique de journal ajoute un nom de propriété toohello suffixe.</span><span class="sxs-lookup"><span data-stu-id="93aba-181">tooidentify a property's data type, Log Analytics adds a suffix toohello property name.</span></span> <span data-ttu-id="93aba-182">Si une propriété contient une valeur null, propriété de hello n’est pas incluse dans l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93aba-182">If a property contains a null value, hello property is not included in that record.</span></span> <span data-ttu-id="93aba-183">Ce tableau répertorie le type de données de propriété hello et le suffixe correspondant :</span><span class="sxs-lookup"><span data-stu-id="93aba-183">This table lists hello property data type and corresponding suffix:</span></span>

| <span data-ttu-id="93aba-184">Type de données de propriété</span><span class="sxs-lookup"><span data-stu-id="93aba-184">Property data type</span></span> | <span data-ttu-id="93aba-185">Suffixe</span><span class="sxs-lookup"><span data-stu-id="93aba-185">Suffix</span></span> |
|:--- |:--- |
| <span data-ttu-id="93aba-186">String</span><span class="sxs-lookup"><span data-stu-id="93aba-186">String</span></span> |<span data-ttu-id="93aba-187">_s</span><span class="sxs-lookup"><span data-stu-id="93aba-187">_s</span></span> |
| <span data-ttu-id="93aba-188">Boolean</span><span class="sxs-lookup"><span data-stu-id="93aba-188">Boolean</span></span> |<span data-ttu-id="93aba-189">_b</span><span class="sxs-lookup"><span data-stu-id="93aba-189">_b</span></span> |
| <span data-ttu-id="93aba-190">Double</span><span class="sxs-lookup"><span data-stu-id="93aba-190">Double</span></span> |<span data-ttu-id="93aba-191">_d</span><span class="sxs-lookup"><span data-stu-id="93aba-191">_d</span></span> |
| <span data-ttu-id="93aba-192">Date/time</span><span class="sxs-lookup"><span data-stu-id="93aba-192">Date/time</span></span> |<span data-ttu-id="93aba-193">_t</span><span class="sxs-lookup"><span data-stu-id="93aba-193">_t</span></span> |
| <span data-ttu-id="93aba-194">GUID</span><span class="sxs-lookup"><span data-stu-id="93aba-194">GUID</span></span> |<span data-ttu-id="93aba-195">_g</span><span class="sxs-lookup"><span data-stu-id="93aba-195">_g</span></span> |

<span data-ttu-id="93aba-196">type de données Hello Analytique de journal utilise pour chaque propriété dépend de si hello type d’enregistrement pour le nouvel enregistrement de hello existe déjà.</span><span class="sxs-lookup"><span data-stu-id="93aba-196">hello data type that Log Analytics uses for each property depends on whether hello record type for hello new record already exists.</span></span>

* <span data-ttu-id="93aba-197">Si le type d’enregistrement hello n’existe pas, Analytique de journal crée un nouveau.</span><span class="sxs-lookup"><span data-stu-id="93aba-197">If hello record type does not exist, Log Analytics creates a new one.</span></span> <span data-ttu-id="93aba-198">Analytique de journal utilise hello JSON inférence toodetermine hello type de données pour chaque propriété pour hello nouvel enregistrement.</span><span class="sxs-lookup"><span data-stu-id="93aba-198">Log Analytics uses hello JSON type inference toodetermine hello data type for each property for hello new record.</span></span>
* <span data-ttu-id="93aba-199">Si le type d’enregistrement hello existe, Analytique de journal tente de toocreate un nouvel enregistrement basé sur les propriétés existantes.</span><span class="sxs-lookup"><span data-stu-id="93aba-199">If hello record type does exist, Log Analytics attempts toocreate a new record based on existing properties.</span></span> <span data-ttu-id="93aba-200">Si hello type de données pour une propriété dans le nouvel enregistrement de hello ne correspond à et ne peut pas être convertie toohello existant de type ou si hello enregistrement inclut une propriété qui n’existe pas, Analytique de journal crée une nouvelle propriété qui a le suffixe approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="93aba-200">If hello data type for a property in hello new record doesn’t match and can’t be converted toohello existing type, or if hello record includes a property that doesn’t exist, Log Analytics creates a new property that has hello relevant suffix.</span></span>

<span data-ttu-id="93aba-201">Par exemple, l’entrée de soumission suivante créerait un enregistrement avec trois propriétés, **number_d**, **boolean_b**, et **string_s** :</span><span class="sxs-lookup"><span data-stu-id="93aba-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span></span>

![Exemple d’enregistrement 1](media/log-analytics-data-collector-api/record-01.png)

<span data-ttu-id="93aba-203">Si vous avez envoyé ensuite cette entrée suivante, avec toutes les valeurs mises en forme en tant que chaînes, les propriétés hello ne modifie pas.</span><span class="sxs-lookup"><span data-stu-id="93aba-203">If you then submitted this next entry, with all values formatted as strings, hello properties would not change.</span></span> <span data-ttu-id="93aba-204">Ces valeurs peuvent être des types de données tooexisting converti :</span><span class="sxs-lookup"><span data-stu-id="93aba-204">These values can be converted tooexisting data types:</span></span>

![Exemple d’enregistrement 2](media/log-analytics-data-collector-api/record-02.png)

<span data-ttu-id="93aba-206">Mais, si vous avez ensuite cette soumission suivante, Analytique de journal créerait hello nouvelles propriétés **boolean_d** et **string_d**.</span><span class="sxs-lookup"><span data-stu-id="93aba-206">But, if you then made this next submission, Log Analytics would create hello new properties **boolean_d** and **string_d**.</span></span> <span data-ttu-id="93aba-207">Les valeurs suivantes ne peuvent pas être converties :</span><span class="sxs-lookup"><span data-stu-id="93aba-207">These values can't be converted:</span></span>

![Exemple d’enregistrement 3](media/log-analytics-data-collector-api/record-03.png)

<span data-ttu-id="93aba-209">Si vous avez envoyé puis hello suivant d’entrée, avant la création de type d’enregistrement hello, Analytique de journal créerait un enregistrement avec trois propriétés, **nombre_succès**, **boolean_s**, et **string_s**.</span><span class="sxs-lookup"><span data-stu-id="93aba-209">If you then submitted hello following entry, before hello record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span></span> <span data-ttu-id="93aba-210">Dans cette entrée, chacune des valeurs initiales de hello est sous forme de chaîne :</span><span class="sxs-lookup"><span data-stu-id="93aba-210">In this entry, each of hello initial values is formatted as a string:</span></span>

![Exemple d’enregistrement 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a><span data-ttu-id="93aba-212">Limites de données</span><span class="sxs-lookup"><span data-stu-id="93aba-212">Data limits</span></span>
<span data-ttu-id="93aba-213">Il existe certaines contraintes autour des données hello validées toohello collecte des données d’Analytique de journal API.</span><span class="sxs-lookup"><span data-stu-id="93aba-213">There are some constraints around hello data posted toohello Log Analytics Data collection API.</span></span>

* <span data-ttu-id="93aba-214">Maximum de 30 Mo par post tooLog API du collecteur de données Analytique.</span><span class="sxs-lookup"><span data-stu-id="93aba-214">Maximum of 30 MB per post tooLog Analytics Data Collector API.</span></span> <span data-ttu-id="93aba-215">Il s’agit d’une limite de taille pour une publication unique.</span><span class="sxs-lookup"><span data-stu-id="93aba-215">This is a size limit for a single post.</span></span> <span data-ttu-id="93aba-216">Si les données de salutation à partir d’une publication unique qui dépasse 30 Mo, vous devez fractionner hello données toosmaller taille blocs et les envoyer simultanément.</span><span class="sxs-lookup"><span data-stu-id="93aba-216">If hello data from a single post that exceeds 30 MB, you should split hello data up toosmaller sized chunks and send them concurrently.</span></span>
* <span data-ttu-id="93aba-217">Maximum de 32 Ko pour les valeurs de champ.</span><span class="sxs-lookup"><span data-stu-id="93aba-217">Maximum of 32 KB limit for field values.</span></span> <span data-ttu-id="93aba-218">Si la valeur du champ hello est supérieure à 32 Ko, les données de salutation seront tronquées.</span><span class="sxs-lookup"><span data-stu-id="93aba-218">If hello field value is greater than 32 KB, hello data will be truncated.</span></span>
* <span data-ttu-id="93aba-219">Le nombre maximal recommandé de champs pour un type donné est 50.</span><span class="sxs-lookup"><span data-stu-id="93aba-219">Recommended maximum number of fields for a given type is 50.</span></span> <span data-ttu-id="93aba-220">Il s’agit d’une limite pratique du point de vue de la facilité d’utilisation et de l’expérience de recherche.</span><span class="sxs-lookup"><span data-stu-id="93aba-220">This is a practical limit from a usability and search experience perspective.</span></span>  

## <a name="return-codes"></a><span data-ttu-id="93aba-221">Codes de retour</span><span class="sxs-lookup"><span data-stu-id="93aba-221">Return codes</span></span>
<span data-ttu-id="93aba-222">Hello, code d’état HTTP 200 signifie que cette demande hello a été reçue pour le traitement.</span><span class="sxs-lookup"><span data-stu-id="93aba-222">hello HTTP status code 200 means that hello request has been received for processing.</span></span> <span data-ttu-id="93aba-223">Cela indique que hello est terminée avec succès.</span><span class="sxs-lookup"><span data-stu-id="93aba-223">This indicates that hello operation completed successfully.</span></span>

<span data-ttu-id="93aba-224">Ce tableau répertorie hello ensemble complet de codes d’état que le service de hello peut retourner :</span><span class="sxs-lookup"><span data-stu-id="93aba-224">This table lists hello complete set of status codes that hello service might return:</span></span>

| <span data-ttu-id="93aba-225">Code</span><span class="sxs-lookup"><span data-stu-id="93aba-225">Code</span></span> | <span data-ttu-id="93aba-226">État</span><span class="sxs-lookup"><span data-stu-id="93aba-226">Status</span></span> | <span data-ttu-id="93aba-227">Code d'erreur</span><span class="sxs-lookup"><span data-stu-id="93aba-227">Error code</span></span> | <span data-ttu-id="93aba-228">Description</span><span class="sxs-lookup"><span data-stu-id="93aba-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="93aba-229">200</span><span class="sxs-lookup"><span data-stu-id="93aba-229">200</span></span> |<span data-ttu-id="93aba-230">OK</span><span class="sxs-lookup"><span data-stu-id="93aba-230">OK</span></span> | |<span data-ttu-id="93aba-231">demande de Hello a été acceptée.</span><span class="sxs-lookup"><span data-stu-id="93aba-231">hello request was successfully accepted.</span></span> |
| <span data-ttu-id="93aba-232">400</span><span class="sxs-lookup"><span data-stu-id="93aba-232">400</span></span> |<span data-ttu-id="93aba-233">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="93aba-233">Bad request</span></span> |<span data-ttu-id="93aba-234">InactiveCustomer</span><span class="sxs-lookup"><span data-stu-id="93aba-234">InactiveCustomer</span></span> |<span data-ttu-id="93aba-235">espace de travail Hello a été fermé.</span><span class="sxs-lookup"><span data-stu-id="93aba-235">hello workspace has been closed.</span></span> |
| <span data-ttu-id="93aba-236">400</span><span class="sxs-lookup"><span data-stu-id="93aba-236">400</span></span> |<span data-ttu-id="93aba-237">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="93aba-237">Bad request</span></span> |<span data-ttu-id="93aba-238">InvalidApiVersion</span><span class="sxs-lookup"><span data-stu-id="93aba-238">InvalidApiVersion</span></span> |<span data-ttu-id="93aba-239">version de Hello API que vous avez spécifié n’est pas reconnue par le service de hello.</span><span class="sxs-lookup"><span data-stu-id="93aba-239">hello API version that you specified was not recognized by hello service.</span></span> |
| <span data-ttu-id="93aba-240">400</span><span class="sxs-lookup"><span data-stu-id="93aba-240">400</span></span> |<span data-ttu-id="93aba-241">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="93aba-241">Bad request</span></span> |<span data-ttu-id="93aba-242">InvalidCustomerId</span><span class="sxs-lookup"><span data-stu-id="93aba-242">InvalidCustomerId</span></span> |<span data-ttu-id="93aba-243">ID d’espace de travail Hello spécifié n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="93aba-243">hello workspace ID specified is invalid.</span></span> |
| <span data-ttu-id="93aba-244">400</span><span class="sxs-lookup"><span data-stu-id="93aba-244">400</span></span> |<span data-ttu-id="93aba-245">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="93aba-245">Bad request</span></span> |<span data-ttu-id="93aba-246">InvalidDataFormat</span><span class="sxs-lookup"><span data-stu-id="93aba-246">InvalidDataFormat</span></span> |<span data-ttu-id="93aba-247">Un JSON non valide a été envoyé.</span><span class="sxs-lookup"><span data-stu-id="93aba-247">Invalid JSON was submitted.</span></span> <span data-ttu-id="93aba-248">corps de réponse Hello peut contenir plus d’informations sur la façon dont tooresolve hello erreur.</span><span class="sxs-lookup"><span data-stu-id="93aba-248">hello response body might contain more information about how tooresolve hello error.</span></span> |
| <span data-ttu-id="93aba-249">400</span><span class="sxs-lookup"><span data-stu-id="93aba-249">400</span></span> |<span data-ttu-id="93aba-250">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="93aba-250">Bad request</span></span> |<span data-ttu-id="93aba-251">InvalidLogType</span><span class="sxs-lookup"><span data-stu-id="93aba-251">InvalidLogType</span></span> |<span data-ttu-id="93aba-252">indiquer le type de journal Hello contenus des caractères spéciaux ou des valeurs numériques.</span><span class="sxs-lookup"><span data-stu-id="93aba-252">hello log type specified contained special characters or numerics.</span></span> |
| <span data-ttu-id="93aba-253">400</span><span class="sxs-lookup"><span data-stu-id="93aba-253">400</span></span> |<span data-ttu-id="93aba-254">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="93aba-254">Bad request</span></span> |<span data-ttu-id="93aba-255">MissingApiVersion</span><span class="sxs-lookup"><span data-stu-id="93aba-255">MissingApiVersion</span></span> |<span data-ttu-id="93aba-256">version de l’API Hello n’a pas été spécifiée.</span><span class="sxs-lookup"><span data-stu-id="93aba-256">hello API version wasn’t specified.</span></span> |
| <span data-ttu-id="93aba-257">400</span><span class="sxs-lookup"><span data-stu-id="93aba-257">400</span></span> |<span data-ttu-id="93aba-258">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="93aba-258">Bad request</span></span> |<span data-ttu-id="93aba-259">MissingContentType</span><span class="sxs-lookup"><span data-stu-id="93aba-259">MissingContentType</span></span> |<span data-ttu-id="93aba-260">type de contenu Hello n’a pas été spécifié.</span><span class="sxs-lookup"><span data-stu-id="93aba-260">hello content type wasn’t specified.</span></span> |
| <span data-ttu-id="93aba-261">400</span><span class="sxs-lookup"><span data-stu-id="93aba-261">400</span></span> |<span data-ttu-id="93aba-262">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="93aba-262">Bad request</span></span> |<span data-ttu-id="93aba-263">MissingLogType</span><span class="sxs-lookup"><span data-stu-id="93aba-263">MissingLogType</span></span> |<span data-ttu-id="93aba-264">Hello obligatoire type de journal de valeur n’a pas été spécifié.</span><span class="sxs-lookup"><span data-stu-id="93aba-264">hello required value log type wasn’t specified.</span></span> |
| <span data-ttu-id="93aba-265">400</span><span class="sxs-lookup"><span data-stu-id="93aba-265">400</span></span> |<span data-ttu-id="93aba-266">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="93aba-266">Bad request</span></span> |<span data-ttu-id="93aba-267">UnsupportedContentType</span><span class="sxs-lookup"><span data-stu-id="93aba-267">UnsupportedContentType</span></span> |<span data-ttu-id="93aba-268">type de contenu Hello n’a pas été défini trop**application/json**.</span><span class="sxs-lookup"><span data-stu-id="93aba-268">hello content type was not set too**application/json**.</span></span> |
| <span data-ttu-id="93aba-269">403</span><span class="sxs-lookup"><span data-stu-id="93aba-269">403</span></span> |<span data-ttu-id="93aba-270">Interdit</span><span class="sxs-lookup"><span data-stu-id="93aba-270">Forbidden</span></span> |<span data-ttu-id="93aba-271">InvalidAuthorization</span><span class="sxs-lookup"><span data-stu-id="93aba-271">InvalidAuthorization</span></span> |<span data-ttu-id="93aba-272">service de Hello Échec de la demande de hello tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="93aba-272">hello service failed tooauthenticate hello request.</span></span> <span data-ttu-id="93aba-273">Vérifiez que cette clé d’espace de travail hello ID et de connexion sont valides.</span><span class="sxs-lookup"><span data-stu-id="93aba-273">Verify that hello workspace ID and connection key are valid.</span></span> |
| <span data-ttu-id="93aba-274">404</span><span class="sxs-lookup"><span data-stu-id="93aba-274">404</span></span> |<span data-ttu-id="93aba-275">Introuvable</span><span class="sxs-lookup"><span data-stu-id="93aba-275">Not Found</span></span> | | <span data-ttu-id="93aba-276">URL de hello fourni est incorrect, ou demande de hello est trop grande.</span><span class="sxs-lookup"><span data-stu-id="93aba-276">Either hello URL provided is incorrect, or hello request is too large.</span></span> |
| <span data-ttu-id="93aba-277">429</span><span class="sxs-lookup"><span data-stu-id="93aba-277">429</span></span> |<span data-ttu-id="93aba-278">Trop de demandes</span><span class="sxs-lookup"><span data-stu-id="93aba-278">Too Many Requests</span></span> | | <span data-ttu-id="93aba-279">Hello service rencontre un volume important de données à partir de votre compte.</span><span class="sxs-lookup"><span data-stu-id="93aba-279">hello service is experiencing a high volume of data from your account.</span></span> <span data-ttu-id="93aba-280">Réessayez plus tard la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="93aba-280">Please retry hello request later.</span></span> |
| <span data-ttu-id="93aba-281">500</span><span class="sxs-lookup"><span data-stu-id="93aba-281">500</span></span> |<span data-ttu-id="93aba-282">Erreur interne du serveur</span><span class="sxs-lookup"><span data-stu-id="93aba-282">Internal Server Error</span></span> |<span data-ttu-id="93aba-283">UnspecifiedError</span><span class="sxs-lookup"><span data-stu-id="93aba-283">UnspecifiedError</span></span> |<span data-ttu-id="93aba-284">service de Hello a rencontré une erreur interne.</span><span class="sxs-lookup"><span data-stu-id="93aba-284">hello service encountered an internal error.</span></span> <span data-ttu-id="93aba-285">Réessayez la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="93aba-285">Please retry hello request.</span></span> |
| <span data-ttu-id="93aba-286">503</span><span class="sxs-lookup"><span data-stu-id="93aba-286">503</span></span> |<span data-ttu-id="93aba-287">Service indisponible</span><span class="sxs-lookup"><span data-stu-id="93aba-287">Service Unavailable</span></span> |<span data-ttu-id="93aba-288">ServiceUnavailable</span><span class="sxs-lookup"><span data-stu-id="93aba-288">ServiceUnavailable</span></span> |<span data-ttu-id="93aba-289">service de Hello est actuellement indisponible tooreceive demandes.</span><span class="sxs-lookup"><span data-stu-id="93aba-289">hello service currently is unavailable tooreceive requests.</span></span> <span data-ttu-id="93aba-290">Relancez la requête.</span><span class="sxs-lookup"><span data-stu-id="93aba-290">Please retry your request.</span></span> |

## <a name="query-data"></a><span data-ttu-id="93aba-291">Données de requête</span><span class="sxs-lookup"><span data-stu-id="93aba-291">Query data</span></span>
<span data-ttu-id="93aba-292">données tooquery soumises par hello API du collecteur de journal Analytique HTTP données, rechercher des enregistrements avec **Type** qui est égale toohello **LogType** assorti de valeur que vous avez spécifié, **_CL**.</span><span class="sxs-lookup"><span data-stu-id="93aba-292">tooquery data submitted by hello Log Analytics HTTP Data Collector API, search for records with **Type** that is equal toohello **LogType** value that you specified, appended with **_CL**.</span></span> <span data-ttu-id="93aba-293">Par exemple, si vous avez utilisé **MyCustomLog**, vous devriez retourner tous les enregistrements avec **Type=MyCustomLog_CL**.</span><span class="sxs-lookup"><span data-stu-id="93aba-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span></span>

>[!NOTE]
> <span data-ttu-id="93aba-294">Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis hello au-dessus de requête pourrait être modifié toohello suivant.</span><span class="sxs-lookup"><span data-stu-id="93aba-294">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>

> `MyCustomLog_CL`

## <a name="sample-requests"></a><span data-ttu-id="93aba-295">Exemples de demandes</span><span class="sxs-lookup"><span data-stu-id="93aba-295">Sample requests</span></span>
<span data-ttu-id="93aba-296">Dans les sections suivantes hello, vous trouverez des exemples de toosubmit données toohello API du collecteur de données journal Analytique HTTP à l’aide de différents langages de programmation.</span><span class="sxs-lookup"><span data-stu-id="93aba-296">In hello next sections, you'll find samples of how toosubmit data toohello Log Analytics HTTP Data Collector API by using different programming languages.</span></span>

<span data-ttu-id="93aba-297">Pour chaque échantillon, effectuez ces étapes tooset les variables de hello pour l’en-tête d’autorisation hello :</span><span class="sxs-lookup"><span data-stu-id="93aba-297">For each sample, do these steps tooset hello variables for hello authorization header:</span></span>

1. <span data-ttu-id="93aba-298">Dans le portail Operations Management Suite hello, sélectionnez hello **paramètres** vignette, puis sélectionnez hello **Sources connectées** onglet.</span><span class="sxs-lookup"><span data-stu-id="93aba-298">In hello Operations Management Suite portal, select hello **Settings** tile, and then select hello **Connected Sources** tab.</span></span>
2. <span data-ttu-id="93aba-299">toohello à droite de **ID de l’espace de travail**, sélectionnez l’icône de copie hello, puis collez hello ID en tant que valeur hello Hello **ID de client** variable.</span><span class="sxs-lookup"><span data-stu-id="93aba-299">toohello right of **Workspace ID**, select hello copy icon, and then paste hello ID as hello value of hello **Customer ID** variable.</span></span>
3. <span data-ttu-id="93aba-300">toohello à droite de **clé primaire**, sélectionnez l’icône de copie hello, puis collez hello ID en tant que valeur hello Hello **Shared Key** variable.</span><span class="sxs-lookup"><span data-stu-id="93aba-300">toohello right of **Primary Key**, select hello copy icon, and then paste hello ID as hello value of hello **Shared Key** variable.</span></span>

<span data-ttu-id="93aba-301">Vous pouvez également modifier variables hello pour le type de journal hello et les données JSON.</span><span class="sxs-lookup"><span data-stu-id="93aba-301">Alternatively, you can change hello variables for hello log type and JSON data.</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="93aba-302">Exemple de code PowerShell</span><span class="sxs-lookup"><span data-stu-id="93aba-302">PowerShell sample</span></span>
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create hello function toocreate hello authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create hello function toocreate and post hello request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a><span data-ttu-id="93aba-303">Exemple de code C#</span><span class="sxs-lookup"><span data-stu-id="93aba-303">C# sample</span></span>
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request toohello POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a><span data-ttu-id="93aba-304">Exemple de code Python</span><span class="sxs-lookup"><span data-stu-id="93aba-304">Python sample</span></span>
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a><span data-ttu-id="93aba-305">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="93aba-305">Next steps</span></span>
- <span data-ttu-id="93aba-306">Hello d’utilisation [API de recherche de journal](log-analytics-log-search-api.md) tooretrieve des données à partir du référentiel d’Analytique de journal hello.</span><span class="sxs-lookup"><span data-stu-id="93aba-306">Use hello [Log Search API](log-analytics-log-search-api.md) tooretrieve data from hello Log Analytics repository.</span></span>
