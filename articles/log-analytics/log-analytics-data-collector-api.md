---
title: "API Collecte de données HTTP Log Analytics | Microsoft Docs"
description: "L’API Collecte de données HTTP Log Analytics permet d’ajouter des données POST JSON au référentiel de Log Analytics à partir de tout client pouvant appeler l’API REST. Cet article explique comment utiliser l’API, et contient des exemples montrant comment publier des données à l’aide de différents langages de programmation."
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
ms.openlocfilehash: b0c45ff8c1d4c9d35fbb3c8839b38a20df277055
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="send-data-to-log-analytics-with-the-http-data-collector-api"></a><span data-ttu-id="3b52f-104">Transmettre des données à Log Analytics avec l’API Collecte de données HTTP</span><span class="sxs-lookup"><span data-stu-id="3b52f-104">Send data to Log Analytics with the HTTP Data Collector API</span></span>
<span data-ttu-id="3b52f-105">Cet article vous montre comment utiliser l’API Collecte de données HTTP pour transmettre des données à Log Analytics à partir d’un client API REST.</span><span class="sxs-lookup"><span data-stu-id="3b52f-105">This article shows you how to use the HTTP Data Collector API to send data to Log Analytics from a REST API client.</span></span>  <span data-ttu-id="3b52f-106">Il explique comment mettre en forme les données collectées par le script ou l’application, les inclure dans une requête et faire en sorte que Log Analytics autorise cette requête.</span><span class="sxs-lookup"><span data-stu-id="3b52f-106">It describes how to format data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span></span>  <span data-ttu-id="3b52f-107">Il est illustré par des exemples pour PowerShell, C# et Python.</span><span class="sxs-lookup"><span data-stu-id="3b52f-107">Examples are provided for PowerShell, C#, and Python.</span></span>

## <a name="concepts"></a><span data-ttu-id="3b52f-108">Concepts</span><span class="sxs-lookup"><span data-stu-id="3b52f-108">Concepts</span></span>
<span data-ttu-id="3b52f-109">Vous pouvez utiliser l’API Collecte de données HTTP pour transmettre des données à Log Analytics à partir de tout client pouvant appeler l’API REST.</span><span class="sxs-lookup"><span data-stu-id="3b52f-109">You can use the HTTP Data Collector API to send data to Log Analytics from any client that can call a REST API.</span></span>  <span data-ttu-id="3b52f-110">Il peut s’agir d’un runbook dans Azure Automation qui collecte les données de gestion à partir d’Azure ou d’un autre cloud, ou il peut s’agit d’un système de gestion alternatif utilisant Log Analytics pour consolider et analyser les données.</span><span class="sxs-lookup"><span data-stu-id="3b52f-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics to consolidate and analyze data.</span></span>

<span data-ttu-id="3b52f-111">Toutes les données du référentiel Log Analysis sont stockées en tant qu’enregistrement avec un type d’enregistrement particulier.</span><span class="sxs-lookup"><span data-stu-id="3b52f-111">All data in the Log Analytics repository is stored as a record with a particular record type.</span></span>  <span data-ttu-id="3b52f-112">Vous formatez vos données à transmettre à l’API Collecte de données HTTP en tant qu’enregistrements multiples dans JSON.</span><span class="sxs-lookup"><span data-stu-id="3b52f-112">You format your data to send to the HTTP Data Collector API as multiple records in JSON.</span></span>  <span data-ttu-id="3b52f-113">Lorsque vous envoyez vos données, un enregistrement individuel est créé dans le référentiel pour chaque enregistrement dans la charge utile de la requête.</span><span class="sxs-lookup"><span data-stu-id="3b52f-113">When you submit the data, an individual record is created in the repository for each record in the request payload.</span></span>


![Présentation la collecte de données HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a><span data-ttu-id="3b52f-115">Créer une demande</span><span class="sxs-lookup"><span data-stu-id="3b52f-115">Create a request</span></span>
<span data-ttu-id="3b52f-116">Pour utiliser l’API Collecte de données HTTP, il vous suffit de créer une requête POST qui inclut les données à envoyer dans JavaScript Objet Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="3b52f-116">To use the HTTP Data Collector API, you create a POST request that includes the data to send in JavaScript Object Notation (JSON).</span></span>  <span data-ttu-id="3b52f-117">Les trois tableaux suivants répertorient les attributs requis pour chaque requête.</span><span class="sxs-lookup"><span data-stu-id="3b52f-117">The next three tables list the attributes that are required for each request.</span></span> <span data-ttu-id="3b52f-118">Nous décrivons chaque attribut de façon plus détaillée plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="3b52f-118">We describe each attribute in more detail later in the article.</span></span>

### <a name="request-uri"></a><span data-ttu-id="3b52f-119">URI de demande</span><span class="sxs-lookup"><span data-stu-id="3b52f-119">Request URI</span></span>
| <span data-ttu-id="3b52f-120">Attribut</span><span class="sxs-lookup"><span data-stu-id="3b52f-120">Attribute</span></span> | <span data-ttu-id="3b52f-121">Propriété</span><span class="sxs-lookup"><span data-stu-id="3b52f-121">Property</span></span> |
|:--- |:--- |
| <span data-ttu-id="3b52f-122">Méthode</span><span class="sxs-lookup"><span data-stu-id="3b52f-122">Method</span></span> |<span data-ttu-id="3b52f-123">POST</span><span class="sxs-lookup"><span data-stu-id="3b52f-123">POST</span></span> |
| <span data-ttu-id="3b52f-124">URI</span><span class="sxs-lookup"><span data-stu-id="3b52f-124">URI</span></span> |<span data-ttu-id="3b52f-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span><span class="sxs-lookup"><span data-stu-id="3b52f-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span></span> |
| <span data-ttu-id="3b52f-126">Type de contenu</span><span class="sxs-lookup"><span data-stu-id="3b52f-126">Content type</span></span> |<span data-ttu-id="3b52f-127">application/json</span><span class="sxs-lookup"><span data-stu-id="3b52f-127">application/json</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="3b52f-128">Paramètres de l’URI de demande</span><span class="sxs-lookup"><span data-stu-id="3b52f-128">Request URI parameters</span></span>
| <span data-ttu-id="3b52f-129">Paramètre</span><span class="sxs-lookup"><span data-stu-id="3b52f-129">Parameter</span></span> | <span data-ttu-id="3b52f-130">Description</span><span class="sxs-lookup"><span data-stu-id="3b52f-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3b52f-131">CustomerID</span><span class="sxs-lookup"><span data-stu-id="3b52f-131">CustomerID</span></span> |<span data-ttu-id="3b52f-132">Identificateur unique de l’espace de travail de Microsoft Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="3b52f-132">The unique identifier for the Microsoft Operations Management Suite workspace.</span></span> |
| <span data-ttu-id="3b52f-133">Ressource</span><span class="sxs-lookup"><span data-stu-id="3b52f-133">Resource</span></span> |<span data-ttu-id="3b52f-134">Nom de ressource de l’API : / api/logs.</span><span class="sxs-lookup"><span data-stu-id="3b52f-134">The API resource name: /api/logs.</span></span> |
| <span data-ttu-id="3b52f-135">Version de l'API</span><span class="sxs-lookup"><span data-stu-id="3b52f-135">API Version</span></span> |<span data-ttu-id="3b52f-136">Version de l’API à utiliser avec cette demande.</span><span class="sxs-lookup"><span data-stu-id="3b52f-136">The version of the API to use with this request.</span></span> <span data-ttu-id="3b52f-137">Actuellement, il s’agit de 2016-04-01.</span><span class="sxs-lookup"><span data-stu-id="3b52f-137">Currently, it's 2016-04-01.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3b52f-138">En-têtes de requête</span><span class="sxs-lookup"><span data-stu-id="3b52f-138">Request headers</span></span>
| <span data-ttu-id="3b52f-139">En-tête</span><span class="sxs-lookup"><span data-stu-id="3b52f-139">Header</span></span> | <span data-ttu-id="3b52f-140">Description</span><span class="sxs-lookup"><span data-stu-id="3b52f-140">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3b52f-141">Authorization</span><span class="sxs-lookup"><span data-stu-id="3b52f-141">Authorization</span></span> |<span data-ttu-id="3b52f-142">Signature de l’autorisation.</span><span class="sxs-lookup"><span data-stu-id="3b52f-142">The authorization signature.</span></span> <span data-ttu-id="3b52f-143">Plus loin dans cet article, vous pouvez lire comment créer un en-tête HMAC-SHA256.</span><span class="sxs-lookup"><span data-stu-id="3b52f-143">Later in the article, you can read about how to create an HMAC-SHA256 header.</span></span> |
| <span data-ttu-id="3b52f-144">Log-Type</span><span class="sxs-lookup"><span data-stu-id="3b52f-144">Log-Type</span></span> |<span data-ttu-id="3b52f-145">Spécifiez le type d’enregistrement des données envoyées.</span><span class="sxs-lookup"><span data-stu-id="3b52f-145">Specify the record type of the data that is being submitted.</span></span> <span data-ttu-id="3b52f-146">Actuellement, le type de journal prend en charge uniquement des caractères alphabétiques.</span><span class="sxs-lookup"><span data-stu-id="3b52f-146">Currently, the log type supports only alpha characters.</span></span> <span data-ttu-id="3b52f-147">Il ne prend pas en charge les caractères numériques ou spéciaux.</span><span class="sxs-lookup"><span data-stu-id="3b52f-147">It does not support numerics or special characters.</span></span> |
| <span data-ttu-id="3b52f-148">x-ms-date</span><span class="sxs-lookup"><span data-stu-id="3b52f-148">x-ms-date</span></span> |<span data-ttu-id="3b52f-149">Date à laquelle la requête a été traitée, au format RFC 1123.</span><span class="sxs-lookup"><span data-stu-id="3b52f-149">The date that the request was processed, in RFC 1123 format.</span></span> |
| <span data-ttu-id="3b52f-150">time-generated-field</span><span class="sxs-lookup"><span data-stu-id="3b52f-150">time-generated-field</span></span> |<span data-ttu-id="3b52f-151">Nom d’un champ de données qui contient l’horodateur de l’élément de données.</span><span class="sxs-lookup"><span data-stu-id="3b52f-151">The name of a field in the data that contains the timestamp of the data item.</span></span> <span data-ttu-id="3b52f-152">Si vous spécifiez un champ, son contenu est utilisé pour **TimeGenerated**.</span><span class="sxs-lookup"><span data-stu-id="3b52f-152">If you specify a field then its contents are used for **TimeGenerated**.</span></span> <span data-ttu-id="3b52f-153">Si ce champ n’est pas spécifié, la valeur par défaut de **TimeGenerated** est l’heure d’ingestion du message.</span><span class="sxs-lookup"><span data-stu-id="3b52f-153">If this field isn’t specified, the default for **TimeGenerated** is the time that the message is ingested.</span></span> <span data-ttu-id="3b52f-154">Le contenu du champ de message doit suivre le format ISO 8601 AAAA-MM-JJThh:mm:ssZ.</span><span class="sxs-lookup"><span data-stu-id="3b52f-154">The contents of the message field should follow the ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span></span> |

## <a name="authorization"></a><span data-ttu-id="3b52f-155">Autorisation</span><span class="sxs-lookup"><span data-stu-id="3b52f-155">Authorization</span></span>
<span data-ttu-id="3b52f-156">Toute demande adressée à l’API Collecte de données HTTP Log Analytics doit inclure un en-tête d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="3b52f-156">Any request to the Log Analytics HTTP Data Collector API must include an authorization header.</span></span> <span data-ttu-id="3b52f-157">Pour authentifier une demande, vous devez la signer avec la clé primaire ou secondaire de l’espace de travail qui effectue la demande.</span><span class="sxs-lookup"><span data-stu-id="3b52f-157">To authenticate a request, you must sign the request with either the primary or the secondary key for the workspace that is making the request.</span></span> <span data-ttu-id="3b52f-158">Ensuite, transmettez cette signature dans le cadre de la demande.</span><span class="sxs-lookup"><span data-stu-id="3b52f-158">Then, pass that signature as part of the request.</span></span>   

<span data-ttu-id="3b52f-159">Voici le format de l’en-tête d’autorisation :</span><span class="sxs-lookup"><span data-stu-id="3b52f-159">Here's the format for the authorization header:</span></span>

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

<span data-ttu-id="3b52f-160">*WorkspaceID* est l’identificateur unique de l’espace de travail Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="3b52f-160">*WorkspaceID* is the unique identifier for the Operations Management Suite workspace.</span></span> <span data-ttu-id="3b52f-161">*Signature* est une clé [HMAC](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) construite à partir de la demande, puis calculée à l’aide de l’[algorithme SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b52f-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from the request and then computed by using the [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span></span> <span data-ttu-id="3b52f-162">Ensuite, vous l’encodez à l’aide d’un encodage Base64.</span><span class="sxs-lookup"><span data-stu-id="3b52f-162">Then, you encode it by using Base64 encoding.</span></span>

<span data-ttu-id="3b52f-163">Utilisez ce format pour encoder la chaîne de signature **SharedKey** :</span><span class="sxs-lookup"><span data-stu-id="3b52f-163">Use this format to encode the **SharedKey** signature string:</span></span>

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

<span data-ttu-id="3b52f-164">Voici un exemple de chaîne de signature :</span><span class="sxs-lookup"><span data-stu-id="3b52f-164">Here's an example of a signature string:</span></span>

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

<span data-ttu-id="3b52f-165">Lorsque vous avez la chaîne de signature, encodez-la en utilisant l’algorithme HMAC-SHA256 sur la chaîne encodée en UTF-8, puis encodez le résultat en Base64.</span><span class="sxs-lookup"><span data-stu-id="3b52f-165">When you have the signature string, encode it by using the HMAC-SHA256 algorithm on the UTF-8-encoded string, and then encode the result as Base64.</span></span> <span data-ttu-id="3b52f-166">Utilisez le format suivant :</span><span class="sxs-lookup"><span data-stu-id="3b52f-166">Use this format:</span></span>

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

<span data-ttu-id="3b52f-167">Les exemples fournis dans les sections suivantes comportent un exemple de code pour vous aider à créer un en-tête d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="3b52f-167">The samples in the next sections have sample code to help you create an authorization header.</span></span>

## <a name="request-body"></a><span data-ttu-id="3b52f-168">Corps de la demande</span><span class="sxs-lookup"><span data-stu-id="3b52f-168">Request body</span></span>
<span data-ttu-id="3b52f-169">Le corps du message doit être au format JSON.</span><span class="sxs-lookup"><span data-stu-id="3b52f-169">The body of the message must be in JSON.</span></span> <span data-ttu-id="3b52f-170">Il doit inclure un ou plusieurs enregistrements avec les paires nom de propriété/valeur au format suivant :</span><span class="sxs-lookup"><span data-stu-id="3b52f-170">It must include one or more records with the property name and value pairs in this format:</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

<span data-ttu-id="3b52f-171">Vous pouvez regrouper plusieurs enregistrements par lot dans une seule requête en utilisant le format suivant.</span><span class="sxs-lookup"><span data-stu-id="3b52f-171">You can batch multiple records together in a single request by using the following format.</span></span> <span data-ttu-id="3b52f-172">Tous les enregistrements doivent être du même type.</span><span class="sxs-lookup"><span data-stu-id="3b52f-172">All the records must be the same record type.</span></span>

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

## <a name="record-type-and-properties"></a><span data-ttu-id="3b52f-173">Type et propriétés d’enregistrement</span><span class="sxs-lookup"><span data-stu-id="3b52f-173">Record type and properties</span></span>
<span data-ttu-id="3b52f-174">Vous définissez un type d’enregistrement personnalisé lorsque vous envoyez des données via l’API Collecte de données HTTP Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3b52f-174">You define a custom record type when you submit data through the Log Analytics HTTP Data Collector API.</span></span> <span data-ttu-id="3b52f-175">Actuellement, vous ne pouvez pas écrire de données dans des types d’enregistrements existants qui ont été créés par d’autres types de données et solutions.</span><span class="sxs-lookup"><span data-stu-id="3b52f-175">Currently, you can't write data to existing record types that were created by other data types and solutions.</span></span> <span data-ttu-id="3b52f-176">Log Analytics lit les données entrantes, puis crée des propriétés correspondant aux types de données des valeurs que vous entrez.</span><span class="sxs-lookup"><span data-stu-id="3b52f-176">Log Analytics reads the incoming data and then creates properties that match the data types of the values that you enter.</span></span>

<span data-ttu-id="3b52f-177">Chaque demande adressée à l’API Log Analytics doit inclure un en-tête **Log-Type** avec le nom du type d’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3b52f-177">Each request to the Log Analytics API must include a **Log-Type** header with the name for the record type.</span></span> <span data-ttu-id="3b52f-178">Le suffixe **_CL** est automatiquement ajouté au nom que vous entrez pour le distinguer d’autres types de journaux en tant que journal personnalisé.</span><span class="sxs-lookup"><span data-stu-id="3b52f-178">The suffix **_CL** is automatically appended to the name you enter to distinguish it from other log types as a custom log.</span></span> <span data-ttu-id="3b52f-179">Par exemple, si vous entrez le nom **MyNewRecordType**, Log Analytics crée un enregistrement du type **MyNewRecordType_CL**.</span><span class="sxs-lookup"><span data-stu-id="3b52f-179">For example, if you enter the name **MyNewRecordType**, Log Analytics creates a record with the type **MyNewRecordType_CL**.</span></span> <span data-ttu-id="3b52f-180">Cela évite tout conflit entre les noms de type créés par l’utilisateur et ceux fournis dans les solutions Microsoft actuelles ou futures.</span><span class="sxs-lookup"><span data-stu-id="3b52f-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span></span>

<span data-ttu-id="3b52f-181">Pour identifier le type de données d’une propriété, Log Analytics ajoute un suffixe au nom de celle-ci.</span><span class="sxs-lookup"><span data-stu-id="3b52f-181">To identify a property's data type, Log Analytics adds a suffix to the property name.</span></span> <span data-ttu-id="3b52f-182">Si une propriété contient une valeur null, elle n’est pas incluse dans cet enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3b52f-182">If a property contains a null value, the property is not included in that record.</span></span> <span data-ttu-id="3b52f-183">Ce tableau répertorie les types de données de propriété et les suffixes correspondants :</span><span class="sxs-lookup"><span data-stu-id="3b52f-183">This table lists the property data type and corresponding suffix:</span></span>

| <span data-ttu-id="3b52f-184">Type de données de propriété</span><span class="sxs-lookup"><span data-stu-id="3b52f-184">Property data type</span></span> | <span data-ttu-id="3b52f-185">Suffixe</span><span class="sxs-lookup"><span data-stu-id="3b52f-185">Suffix</span></span> |
|:--- |:--- |
| <span data-ttu-id="3b52f-186">String</span><span class="sxs-lookup"><span data-stu-id="3b52f-186">String</span></span> |<span data-ttu-id="3b52f-187">_s</span><span class="sxs-lookup"><span data-stu-id="3b52f-187">_s</span></span> |
| <span data-ttu-id="3b52f-188">Boolean</span><span class="sxs-lookup"><span data-stu-id="3b52f-188">Boolean</span></span> |<span data-ttu-id="3b52f-189">_b</span><span class="sxs-lookup"><span data-stu-id="3b52f-189">_b</span></span> |
| <span data-ttu-id="3b52f-190">Double</span><span class="sxs-lookup"><span data-stu-id="3b52f-190">Double</span></span> |<span data-ttu-id="3b52f-191">_d</span><span class="sxs-lookup"><span data-stu-id="3b52f-191">_d</span></span> |
| <span data-ttu-id="3b52f-192">Date/time</span><span class="sxs-lookup"><span data-stu-id="3b52f-192">Date/time</span></span> |<span data-ttu-id="3b52f-193">_t</span><span class="sxs-lookup"><span data-stu-id="3b52f-193">_t</span></span> |
| <span data-ttu-id="3b52f-194">GUID</span><span class="sxs-lookup"><span data-stu-id="3b52f-194">GUID</span></span> |<span data-ttu-id="3b52f-195">_g</span><span class="sxs-lookup"><span data-stu-id="3b52f-195">_g</span></span> |

<span data-ttu-id="3b52f-196">Le type de données que Log Analytics utilise pour chaque propriété dépend de l’existence préalable ou non du type d’enregistrement pour le nouvel enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3b52f-196">The data type that Log Analytics uses for each property depends on whether the record type for the new record already exists.</span></span>

* <span data-ttu-id="3b52f-197">Si le type d’enregistrement n’existe pas, Log Analytics en crée un.</span><span class="sxs-lookup"><span data-stu-id="3b52f-197">If the record type does not exist, Log Analytics creates a new one.</span></span> <span data-ttu-id="3b52f-198">Log Analytics utilise une inférence de type JSON pour déterminer le type de données pour chaque propriété du nouvel enregistrement.</span><span class="sxs-lookup"><span data-stu-id="3b52f-198">Log Analytics uses the JSON type inference to determine the data type for each property for the new record.</span></span>
* <span data-ttu-id="3b52f-199">Si le type d’enregistrement existe, Log Analytics tente de créer un enregistrement en fonction des propriétés existantes.</span><span class="sxs-lookup"><span data-stu-id="3b52f-199">If the record type does exist, Log Analytics attempts to create a new record based on existing properties.</span></span> <span data-ttu-id="3b52f-200">Si le type de données d’une propriété dans le nouvel enregistrement ne correspond pas et ne peut pas être converti vers le type existant, ou si l’enregistrement contient une propriété inexistante, Log Analytics crée une propriété portant le suffixe approprié.</span><span class="sxs-lookup"><span data-stu-id="3b52f-200">If the data type for a property in the new record doesn’t match and can’t be converted to the existing type, or if the record includes a property that doesn’t exist, Log Analytics creates a new property that has the relevant suffix.</span></span>

<span data-ttu-id="3b52f-201">Par exemple, l’entrée de soumission suivante créerait un enregistrement avec trois propriétés, **number_d**, **boolean_b**, et **string_s** :</span><span class="sxs-lookup"><span data-stu-id="3b52f-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span></span>

![Exemple d’enregistrement 1](media/log-analytics-data-collector-api/record-01.png)

<span data-ttu-id="3b52f-203">Si vous envoyiez ensuite l’entrée suivante, avec toutes les valeurs mises en forme de chaînes, les propriétés ne changeraient pas.</span><span class="sxs-lookup"><span data-stu-id="3b52f-203">If you then submitted this next entry, with all values formatted as strings, the properties would not change.</span></span> <span data-ttu-id="3b52f-204">Ces valeurs peuvent être converties en types de données existants :</span><span class="sxs-lookup"><span data-stu-id="3b52f-204">These values can be converted to existing data types:</span></span>

![Exemple d’enregistrement 2](media/log-analytics-data-collector-api/record-02.png)

<span data-ttu-id="3b52f-206">Mais, si vous faisiez ensuite l’envoi suivant, Log Analytics créerait les propriétés **boolean_d** et **string_d**.</span><span class="sxs-lookup"><span data-stu-id="3b52f-206">But, if you then made this next submission, Log Analytics would create the new properties **boolean_d** and **string_d**.</span></span> <span data-ttu-id="3b52f-207">Les valeurs suivantes ne peuvent pas être converties :</span><span class="sxs-lookup"><span data-stu-id="3b52f-207">These values can't be converted:</span></span>

![Exemple d’enregistrement 3](media/log-analytics-data-collector-api/record-03.png)

<span data-ttu-id="3b52f-209">Si vous envoyiez ensuite l’entrée suivante, avant que la création du type d’enregistrement, Log Analytics créerait un enregistrement avec trois propriétés, **number_s**, **boolean_s** **string_s**.</span><span class="sxs-lookup"><span data-stu-id="3b52f-209">If you then submitted the following entry, before the record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span></span> <span data-ttu-id="3b52f-210">Dans cette entrée, toutes les valeurs initiales sont au format de chaîne :</span><span class="sxs-lookup"><span data-stu-id="3b52f-210">In this entry, each of the initial values is formatted as a string:</span></span>

![Exemple d’enregistrement 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a><span data-ttu-id="3b52f-212">Limites de données</span><span class="sxs-lookup"><span data-stu-id="3b52f-212">Data limits</span></span>
<span data-ttu-id="3b52f-213">Il existe certaines contraintes sur les données publiées sur l’API de collecte de données de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3b52f-213">There are some constraints around the data posted to the Log Analytics Data collection API.</span></span>

* <span data-ttu-id="3b52f-214">Un maximum de 30 Mo par publication sur l’API de collecte de données de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3b52f-214">Maximum of 30 MB per post to Log Analytics Data Collector API.</span></span> <span data-ttu-id="3b52f-215">Il s’agit d’une limite de taille pour une publication unique.</span><span class="sxs-lookup"><span data-stu-id="3b52f-215">This is a size limit for a single post.</span></span> <span data-ttu-id="3b52f-216">Si les données d’une publication unique sont supérieures à 30 Mo, vous devrez fractionner les données en segments de plus petite taille et les envoyer simultanément.</span><span class="sxs-lookup"><span data-stu-id="3b52f-216">If the data from a single post that exceeds 30 MB, you should split the data up to smaller sized chunks and send them concurrently.</span></span>
* <span data-ttu-id="3b52f-217">Maximum de 32 Ko pour les valeurs de champ.</span><span class="sxs-lookup"><span data-stu-id="3b52f-217">Maximum of 32 KB limit for field values.</span></span> <span data-ttu-id="3b52f-218">Si la valeur de champ est supérieure à 32 Ko, les données seront tronquées.</span><span class="sxs-lookup"><span data-stu-id="3b52f-218">If the field value is greater than 32 KB, the data will be truncated.</span></span>
* <span data-ttu-id="3b52f-219">Le nombre maximal recommandé de champs pour un type donné est 50.</span><span class="sxs-lookup"><span data-stu-id="3b52f-219">Recommended maximum number of fields for a given type is 50.</span></span> <span data-ttu-id="3b52f-220">Il s’agit d’une limite pratique du point de vue de la facilité d’utilisation et de l’expérience de recherche.</span><span class="sxs-lookup"><span data-stu-id="3b52f-220">This is a practical limit from a usability and search experience perspective.</span></span>  

## <a name="return-codes"></a><span data-ttu-id="3b52f-221">Codes de retour</span><span class="sxs-lookup"><span data-stu-id="3b52f-221">Return codes</span></span>
<span data-ttu-id="3b52f-222">Le code d’état HTTP 200 signifie que la demande a été reçue et doit être traitée.</span><span class="sxs-lookup"><span data-stu-id="3b52f-222">The HTTP status code 200 means that the request has been received for processing.</span></span> <span data-ttu-id="3b52f-223">Cela indique que l’opération a été accomplie avec succès.</span><span class="sxs-lookup"><span data-stu-id="3b52f-223">This indicates that the operation completed successfully.</span></span>

<span data-ttu-id="3b52f-224">Ce tableau répertorie l’ensemble complet de codes d’état que le service peut retourner :</span><span class="sxs-lookup"><span data-stu-id="3b52f-224">This table lists the complete set of status codes that the service might return:</span></span>

| <span data-ttu-id="3b52f-225">Code</span><span class="sxs-lookup"><span data-stu-id="3b52f-225">Code</span></span> | <span data-ttu-id="3b52f-226">État</span><span class="sxs-lookup"><span data-stu-id="3b52f-226">Status</span></span> | <span data-ttu-id="3b52f-227">Code d'erreur</span><span class="sxs-lookup"><span data-stu-id="3b52f-227">Error code</span></span> | <span data-ttu-id="3b52f-228">Description</span><span class="sxs-lookup"><span data-stu-id="3b52f-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="3b52f-229">200</span><span class="sxs-lookup"><span data-stu-id="3b52f-229">200</span></span> |<span data-ttu-id="3b52f-230">OK</span><span class="sxs-lookup"><span data-stu-id="3b52f-230">OK</span></span> | |<span data-ttu-id="3b52f-231">La demande a été acceptée.</span><span class="sxs-lookup"><span data-stu-id="3b52f-231">The request was successfully accepted.</span></span> |
| <span data-ttu-id="3b52f-232">400</span><span class="sxs-lookup"><span data-stu-id="3b52f-232">400</span></span> |<span data-ttu-id="3b52f-233">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="3b52f-233">Bad request</span></span> |<span data-ttu-id="3b52f-234">InactiveCustomer</span><span class="sxs-lookup"><span data-stu-id="3b52f-234">InactiveCustomer</span></span> |<span data-ttu-id="3b52f-235">L’espace de travail a été fermé.</span><span class="sxs-lookup"><span data-stu-id="3b52f-235">The workspace has been closed.</span></span> |
| <span data-ttu-id="3b52f-236">400</span><span class="sxs-lookup"><span data-stu-id="3b52f-236">400</span></span> |<span data-ttu-id="3b52f-237">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="3b52f-237">Bad request</span></span> |<span data-ttu-id="3b52f-238">InvalidApiVersion</span><span class="sxs-lookup"><span data-stu-id="3b52f-238">InvalidApiVersion</span></span> |<span data-ttu-id="3b52f-239">La version d’API que vous avez spécifiée n’est pas reconnue par le service.</span><span class="sxs-lookup"><span data-stu-id="3b52f-239">The API version that you specified was not recognized by the service.</span></span> |
| <span data-ttu-id="3b52f-240">400</span><span class="sxs-lookup"><span data-stu-id="3b52f-240">400</span></span> |<span data-ttu-id="3b52f-241">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="3b52f-241">Bad request</span></span> |<span data-ttu-id="3b52f-242">InvalidCustomerId</span><span class="sxs-lookup"><span data-stu-id="3b52f-242">InvalidCustomerId</span></span> |<span data-ttu-id="3b52f-243">L’ID d’espace de travail spécifié n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="3b52f-243">The workspace ID specified is invalid.</span></span> |
| <span data-ttu-id="3b52f-244">400</span><span class="sxs-lookup"><span data-stu-id="3b52f-244">400</span></span> |<span data-ttu-id="3b52f-245">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="3b52f-245">Bad request</span></span> |<span data-ttu-id="3b52f-246">InvalidDataFormat</span><span class="sxs-lookup"><span data-stu-id="3b52f-246">InvalidDataFormat</span></span> |<span data-ttu-id="3b52f-247">Un JSON non valide a été envoyé.</span><span class="sxs-lookup"><span data-stu-id="3b52f-247">Invalid JSON was submitted.</span></span> <span data-ttu-id="3b52f-248">Il se peut que le corps de la réponse contiennent des informations supplémentaires sur la manière de résoudre l’erreur.</span><span class="sxs-lookup"><span data-stu-id="3b52f-248">The response body might contain more information about how to resolve the error.</span></span> |
| <span data-ttu-id="3b52f-249">400</span><span class="sxs-lookup"><span data-stu-id="3b52f-249">400</span></span> |<span data-ttu-id="3b52f-250">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="3b52f-250">Bad request</span></span> |<span data-ttu-id="3b52f-251">InvalidLogType</span><span class="sxs-lookup"><span data-stu-id="3b52f-251">InvalidLogType</span></span> |<span data-ttu-id="3b52f-252">Le type de journal spécifié contient des caractères spéciaux ou numériques.</span><span class="sxs-lookup"><span data-stu-id="3b52f-252">The log type specified contained special characters or numerics.</span></span> |
| <span data-ttu-id="3b52f-253">400</span><span class="sxs-lookup"><span data-stu-id="3b52f-253">400</span></span> |<span data-ttu-id="3b52f-254">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="3b52f-254">Bad request</span></span> |<span data-ttu-id="3b52f-255">MissingApiVersion</span><span class="sxs-lookup"><span data-stu-id="3b52f-255">MissingApiVersion</span></span> |<span data-ttu-id="3b52f-256">La version de l’API n’était pas spécifiée.</span><span class="sxs-lookup"><span data-stu-id="3b52f-256">The API version wasn’t specified.</span></span> |
| <span data-ttu-id="3b52f-257">400</span><span class="sxs-lookup"><span data-stu-id="3b52f-257">400</span></span> |<span data-ttu-id="3b52f-258">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="3b52f-258">Bad request</span></span> |<span data-ttu-id="3b52f-259">MissingContentType</span><span class="sxs-lookup"><span data-stu-id="3b52f-259">MissingContentType</span></span> |<span data-ttu-id="3b52f-260">Le type de contenu n’était pas spécifié.</span><span class="sxs-lookup"><span data-stu-id="3b52f-260">The content type wasn’t specified.</span></span> |
| <span data-ttu-id="3b52f-261">400</span><span class="sxs-lookup"><span data-stu-id="3b52f-261">400</span></span> |<span data-ttu-id="3b52f-262">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="3b52f-262">Bad request</span></span> |<span data-ttu-id="3b52f-263">MissingLogType</span><span class="sxs-lookup"><span data-stu-id="3b52f-263">MissingLogType</span></span> |<span data-ttu-id="3b52f-264">Le type de journal de valeur requis n’était pas spécifié.</span><span class="sxs-lookup"><span data-stu-id="3b52f-264">The required value log type wasn’t specified.</span></span> |
| <span data-ttu-id="3b52f-265">400</span><span class="sxs-lookup"><span data-stu-id="3b52f-265">400</span></span> |<span data-ttu-id="3b52f-266">Demande incorrecte</span><span class="sxs-lookup"><span data-stu-id="3b52f-266">Bad request</span></span> |<span data-ttu-id="3b52f-267">UnsupportedContentType</span><span class="sxs-lookup"><span data-stu-id="3b52f-267">UnsupportedContentType</span></span> |<span data-ttu-id="3b52f-268">Le type de contenu n’était pas défini sur **application/json**.</span><span class="sxs-lookup"><span data-stu-id="3b52f-268">The content type was not set to **application/json**.</span></span> |
| <span data-ttu-id="3b52f-269">403</span><span class="sxs-lookup"><span data-stu-id="3b52f-269">403</span></span> |<span data-ttu-id="3b52f-270">Interdit</span><span class="sxs-lookup"><span data-stu-id="3b52f-270">Forbidden</span></span> |<span data-ttu-id="3b52f-271">InvalidAuthorization</span><span class="sxs-lookup"><span data-stu-id="3b52f-271">InvalidAuthorization</span></span> |<span data-ttu-id="3b52f-272">Le serveur n’a pas pu authentifier la demande.</span><span class="sxs-lookup"><span data-stu-id="3b52f-272">The service failed to authenticate the request.</span></span> <span data-ttu-id="3b52f-273">Vérifiez que la clé de connexion et l’ID de l’espace de travail sont valides.</span><span class="sxs-lookup"><span data-stu-id="3b52f-273">Verify that the workspace ID and connection key are valid.</span></span> |
| <span data-ttu-id="3b52f-274">404</span><span class="sxs-lookup"><span data-stu-id="3b52f-274">404</span></span> |<span data-ttu-id="3b52f-275">Introuvable</span><span class="sxs-lookup"><span data-stu-id="3b52f-275">Not Found</span></span> | | <span data-ttu-id="3b52f-276">L’URL fournie est incorrecte, ou la demande est trop grande.</span><span class="sxs-lookup"><span data-stu-id="3b52f-276">Either the URL provided is incorrect, or the request is too large.</span></span> |
| <span data-ttu-id="3b52f-277">429</span><span class="sxs-lookup"><span data-stu-id="3b52f-277">429</span></span> |<span data-ttu-id="3b52f-278">Trop de demandes</span><span class="sxs-lookup"><span data-stu-id="3b52f-278">Too Many Requests</span></span> | | <span data-ttu-id="3b52f-279">Le service reçoit un volume important de données à partir de votre compte.</span><span class="sxs-lookup"><span data-stu-id="3b52f-279">The service is experiencing a high volume of data from your account.</span></span> <span data-ttu-id="3b52f-280">Relancez la requête ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="3b52f-280">Please retry the request later.</span></span> |
| <span data-ttu-id="3b52f-281">500</span><span class="sxs-lookup"><span data-stu-id="3b52f-281">500</span></span> |<span data-ttu-id="3b52f-282">Erreur interne du serveur</span><span class="sxs-lookup"><span data-stu-id="3b52f-282">Internal Server Error</span></span> |<span data-ttu-id="3b52f-283">UnspecifiedError</span><span class="sxs-lookup"><span data-stu-id="3b52f-283">UnspecifiedError</span></span> |<span data-ttu-id="3b52f-284">Le service a rencontré une erreur interne.</span><span class="sxs-lookup"><span data-stu-id="3b52f-284">The service encountered an internal error.</span></span> <span data-ttu-id="3b52f-285">Relancez la requête.</span><span class="sxs-lookup"><span data-stu-id="3b52f-285">Please retry the request.</span></span> |
| <span data-ttu-id="3b52f-286">503</span><span class="sxs-lookup"><span data-stu-id="3b52f-286">503</span></span> |<span data-ttu-id="3b52f-287">Service indisponible</span><span class="sxs-lookup"><span data-stu-id="3b52f-287">Service Unavailable</span></span> |<span data-ttu-id="3b52f-288">ServiceUnavailable</span><span class="sxs-lookup"><span data-stu-id="3b52f-288">ServiceUnavailable</span></span> |<span data-ttu-id="3b52f-289">Le service est actuellement indisponible pour recevoir des demandes.</span><span class="sxs-lookup"><span data-stu-id="3b52f-289">The service currently is unavailable to receive requests.</span></span> <span data-ttu-id="3b52f-290">Relancez la requête.</span><span class="sxs-lookup"><span data-stu-id="3b52f-290">Please retry your request.</span></span> |

## <a name="query-data"></a><span data-ttu-id="3b52f-291">Données de requête</span><span class="sxs-lookup"><span data-stu-id="3b52f-291">Query data</span></span>
<span data-ttu-id="3b52f-292">Pour interroger des données soumises par l’API Collecte de données HTTP Log Analytics, recherchez des enregistrements dont la valeur **Type** correspond à la valeur **LogType** que vous avez spécifiée, assortie de **_CL**.</span><span class="sxs-lookup"><span data-stu-id="3b52f-292">To query data submitted by the Log Analytics HTTP Data Collector API, search for records with **Type** that is equal to the **LogType** value that you specified, appended with **_CL**.</span></span> <span data-ttu-id="3b52f-293">Par exemple, si vous avez utilisé **MyCustomLog**, vous devriez retourner tous les enregistrements avec **Type=MyCustomLog_CL**.</span><span class="sxs-lookup"><span data-stu-id="3b52f-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span></span>

>[!NOTE]
> <span data-ttu-id="3b52f-294">Si vous avez mis à niveau votre espace de travail vers le [nouveau langage de requête dans Log Analytics](log-analytics-log-search-upgrade.md), remplacez la requête ci-dessus par la requête ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="3b52f-294">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>

> `MyCustomLog_CL`

## <a name="sample-requests"></a><span data-ttu-id="3b52f-295">Exemples de demandes</span><span class="sxs-lookup"><span data-stu-id="3b52f-295">Sample requests</span></span>
<span data-ttu-id="3b52f-296">Les sections suivantes contiennent des exemples montrant comment envoyer des données à l’API Collecte de données HTTP Log Analytics à l’aide de différents langages de programmation.</span><span class="sxs-lookup"><span data-stu-id="3b52f-296">In the next sections, you'll find samples of how to submit data to the Log Analytics HTTP Data Collector API by using different programming languages.</span></span>

<span data-ttu-id="3b52f-297">Pour chaque exemple, procédez comme suit pour définir les variables de l’en-tête d’autorisation :</span><span class="sxs-lookup"><span data-stu-id="3b52f-297">For each sample, do these steps to set the variables for the authorization header:</span></span>

1. <span data-ttu-id="3b52f-298">Dans le portail Operations Management Suite, sélectionnez la vignette **Paramètres**, puis l’onglet **Sources connectées**.</span><span class="sxs-lookup"><span data-stu-id="3b52f-298">In the Operations Management Suite portal, select the **Settings** tile, and then select the **Connected Sources** tab.</span></span>
2. <span data-ttu-id="3b52f-299">À droite de **ID de l’espace de travail**, sélectionnez l’icône de copie, puis collez l’ID en tant que valeur de la variable **ID client**.</span><span class="sxs-lookup"><span data-stu-id="3b52f-299">To the right of **Workspace ID**, select the copy icon, and then paste the ID as the value of the **Customer ID** variable.</span></span>
3. <span data-ttu-id="3b52f-300">À droite de **Clé primaire**, sélectionnez l’icône de copie, puis collez l’ID en tant que valeur de la variable **Clé partagée**.</span><span class="sxs-lookup"><span data-stu-id="3b52f-300">To the right of **Primary Key**, select the copy icon, and then paste the ID as the value of the **Shared Key** variable.</span></span>

<span data-ttu-id="3b52f-301">Vous pouvez également modifier les variables pour le type de journal et les données JSON.</span><span class="sxs-lookup"><span data-stu-id="3b52f-301">Alternatively, you can change the variables for the log type and JSON data.</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="3b52f-302">Exemple de code PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b52f-302">PowerShell sample</span></span>
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify the name of the record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with the created time for the records
$TimeStampField = "DateValue"


# Create two records with the same set of properties to create
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

# Create the function to create the authorization signature
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


# Create the function to create and post the request
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

# Submit the data to the API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a><span data-ttu-id="3b52f-303">Exemple de code C#</span><span class="sxs-lookup"><span data-stu-id="3b52f-303">C# sample</span></span>
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

        // Update customerId to your Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either the primary or the secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of the event type that is being submitted to Log Analytics
        static string LogName = "DemoExample";

        // You can use an optional field to specify the timestamp from the data. If the time field is not specified, Log Analytics assumes the time is the message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for the API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build the API signature
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

        // Send a request to the POST API endpoint
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

### <a name="python-sample"></a><span data-ttu-id="3b52f-304">Exemple de code Python</span><span class="sxs-lookup"><span data-stu-id="3b52f-304">Python sample</span></span>
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update the customer ID to your Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For the shared key, use either the primary or the secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# The log type is the name of the event that is being submitted
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

# Build the API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request to the POST API
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

## <a name="next-steps"></a><span data-ttu-id="3b52f-305">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3b52f-305">Next steps</span></span>
- <span data-ttu-id="3b52f-306">Utilisez l’[API Recherche de journal](log-analytics-log-search-api.md) pour récupérer des données à partir du référentiel Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3b52f-306">Use the [Log Search API](log-analytics-log-search-api.md) to retrieve data from the Log Analytics repository.</span></span>
