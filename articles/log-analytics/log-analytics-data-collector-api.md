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
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a>Envoyer des données tooLog Analytique avec hello API du collecteur de données HTTP
Cet article vous explique comment toouse hello API de collecteur de données HTTP toosend données tooLog Analytique d’un client de l’API REST.  Il décrit comment les tooformat les données collectées par le script ou l’application, incluez-le dans une demande et avoir cette demande d’autorisation de l’Analytique des journaux.  Il est illustré par des exemples pour PowerShell, C# et Python.

## <a name="concepts"></a>Concepts
Vous pouvez utiliser les API de collecteur de données HTTP toosend hello données tooLog Analytique à partir de n’importe quel client qui peut appeler une API REST.  Il peut s’agir d’un runbook dans Azure Automation qui recueille la gestion des données à partir d’Azure ou un autre cloud ou il peuvent être un système d’administration de remplacement qui utilise le journal Analytique tooconsolidate et analyser les données.

Toutes les données dans le référentiel d’Analytique de journal hello est stocké comme un enregistrement avec un type d’enregistrement particulier.  Vous mettre en forme votre toohello toosend de données API du collecteur de données HTTP en tant que plusieurs enregistrements dans JSON.  Quand vous envoyez des données de hello, un enregistrement est créé dans le référentiel hello pour chaque enregistrement dans la charge utile de demande hello.


![Présentation la collecte de données HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a>Créer une demande
API de collecteur de données toouse hello HTTP, vous créez une demande POST qui comprend hello données toosend dans JavaScript Objet Notation (JSON).  Bonjour trois tables liste hello attributs qui sont requis pour chaque demande. Nous décrivons chaque attribut plus en détail plus loin dans l’article de hello.

### <a name="request-uri"></a>URI de demande
| Attribut | Propriété |
|:--- |:--- |
| Méthode |POST |
| URI |https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01 |
| Type de contenu |application/json |

### <a name="request-uri-parameters"></a>Paramètres de l’URI de demande
| Paramètre | Description |
|:--- |:--- |
| CustomerID |Bonjour identificateur unique pour l’espace de travail de Microsoft Operations Management Suite hello. |
| Ressource |nom de la ressource Hello API : / api/logs. |
| Version de l'API |version de Hello de toouse hello API avec cette demande. Actuellement, il s’agit de 2016-04-01. |

### <a name="request-headers"></a>En-têtes de requête
| En-tête | Description |
|:--- |:--- |
| Autorisation |signature de l’autorisation de Hello. Plus loin dans l’article hello, vous pouvez lire sur l’en-tête de toocreate un code HMAC-SHA256. |
| Log-Type |Spécifier le type d’enregistrement de hello de données hello sont envoyées. Actuellement, type de journal hello prend en charge uniquement des caractères alphanumériques. Il ne prend pas en charge les caractères numériques ou spéciaux. |
| x-ms-date |date de Hello cette demande hello a été traitée, au format RFC 1123. |
| time-generated-field |nom Hello d’un champ dans les données de salutation qui contient l’horodatage de hello d’élément de données hello. Si vous spécifiez un champ, son contenu est utilisé pour **TimeGenerated**. Si ce champ n’est pas spécifié, la valeur par défaut pour hello **TimeGenerated** est temps de hello que hello message est intégré. contenu Hello hello du champ de message doit suivre le format hello ISO 8601 aaaa-MM-JJThh. |

## <a name="authorization"></a>Autorisation
Les API du collecteur de données journal Analytique HTTP de toohello demande doit inclure un en-tête d’autorisation. tooauthenticate une demande, vous devez vous connecter demande hello avec hello primaire ou clé secondaire de hello pour espace de travail hello demande hello. Ensuite, passer cette signature dans le cadre de la demande de hello.   

Voici le format hello pour l’en-tête d’autorisation hello :

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

*Id_espace_de_travail* est l’identificateur unique de hello pour l’espace de travail Operations Management Suite hello. *Signature* est un [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) qui est construit à partir de la demande de hello et puis calculée à l’aide de hello [algorithme SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx). Ensuite, vous l’encodez à l’aide d’un encodage Base64.

Utilisez cette hello tooencode de format **SharedKey** chaîne de signature :

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

Voici un exemple de chaîne de signature :

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

Lorsque vous avez chaîne de signature hello, encoder à l’aide de hello l’algorithme HMAC-SHA256 sur hello encodée en UTF-8 de chaîne et puis encoder résultat hello en Base64. Utilisez le format suivant :

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

exemples de Hello dans les sections suivantes hello ont toohelp de code d’exemple vous créez un en-tête d’autorisation.

## <a name="request-body"></a>Corps de la demande
corps de Hello du message de type hello doit être au format JSON. Elle doit inclure un ou plusieurs enregistrements avec des paires de nom et la valeur de la propriété hello dans ce format :

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

Vous pouvez traiter plusieurs enregistrements dans une demande unique à l’aide de hello suivant le format. Tous les enregistrements de hello doivent être hello même type d’enregistrement.

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

## <a name="record-type-and-properties"></a>Type et propriétés d’enregistrement
Vous définissez un type d’enregistrement personnalisé lorsque vous envoyez des données via l’API du collecteur de données journal Analytique HTTP de hello. Actuellement, vous ne peut pas écrire les données tooexisting types d’enregistrements qui ont été créés par d’autres types de données et les solutions. Analytique de journal lit les données entrantes hello et crée ensuite des propriétés qui correspondent aux types de données hello de valeurs hello que vous entrez.

Chaque toohello demande API Analytique de journal doit inclure un **Type de journal** en-tête dont le nom hello pour le type d’enregistrement hello. suffixe de Hello **_CL** nom toohello ajoutée automatiquement vous entrez toodistinguish à partir du journal des autres types en tant qu’un journal personnalisé. Par exemple, si vous entrez le nom de hello **MyNewRecordType**, Analytique de journal crée un enregistrement avec le type de hello **MyNewRecordType_CL**. Cela évite tout conflit entre les noms de type créés par l’utilisateur et ceux fournis dans les solutions Microsoft actuelles ou futures.

type de données d’une propriété tooidentify, Analytique de journal ajoute un nom de propriété toohello suffixe. Si une propriété contient une valeur null, propriété de hello n’est pas incluse dans l’enregistrement. Ce tableau répertorie le type de données de propriété hello et le suffixe correspondant :

| Type de données de propriété | Suffixe |
|:--- |:--- |
| String |_s |
| Boolean |_b |
| Double |_d |
| Date/time |_t |
| GUID |_g |

type de données Hello Analytique de journal utilise pour chaque propriété dépend de si hello type d’enregistrement pour le nouvel enregistrement de hello existe déjà.

* Si le type d’enregistrement hello n’existe pas, Analytique de journal crée un nouveau. Analytique de journal utilise hello JSON inférence toodetermine hello type de données pour chaque propriété pour hello nouvel enregistrement.
* Si le type d’enregistrement hello existe, Analytique de journal tente de toocreate un nouvel enregistrement basé sur les propriétés existantes. Si hello type de données pour une propriété dans le nouvel enregistrement de hello ne correspond à et ne peut pas être convertie toohello existant de type ou si hello enregistrement inclut une propriété qui n’existe pas, Analytique de journal crée une nouvelle propriété qui a le suffixe approprié de hello.

Par exemple, l’entrée de soumission suivante créerait un enregistrement avec trois propriétés, **number_d**, **boolean_b**, et **string_s** :

![Exemple d’enregistrement 1](media/log-analytics-data-collector-api/record-01.png)

Si vous avez envoyé ensuite cette entrée suivante, avec toutes les valeurs mises en forme en tant que chaînes, les propriétés hello ne modifie pas. Ces valeurs peuvent être des types de données tooexisting converti :

![Exemple d’enregistrement 2](media/log-analytics-data-collector-api/record-02.png)

Mais, si vous avez ensuite cette soumission suivante, Analytique de journal créerait hello nouvelles propriétés **boolean_d** et **string_d**. Les valeurs suivantes ne peuvent pas être converties :

![Exemple d’enregistrement 3](media/log-analytics-data-collector-api/record-03.png)

Si vous avez envoyé puis hello suivant d’entrée, avant la création de type d’enregistrement hello, Analytique de journal créerait un enregistrement avec trois propriétés, **nombre_succès**, **boolean_s**, et **string_s**. Dans cette entrée, chacune des valeurs initiales de hello est sous forme de chaîne :

![Exemple d’enregistrement 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a>Limites de données
Il existe certaines contraintes autour des données hello validées toohello collecte des données d’Analytique de journal API.

* Maximum de 30 Mo par post tooLog API du collecteur de données Analytique. Il s’agit d’une limite de taille pour une publication unique. Si les données de salutation à partir d’une publication unique qui dépasse 30 Mo, vous devez fractionner hello données toosmaller taille blocs et les envoyer simultanément.
* Maximum de 32 Ko pour les valeurs de champ. Si la valeur du champ hello est supérieure à 32 Ko, les données de salutation seront tronquées.
* Le nombre maximal recommandé de champs pour un type donné est 50. Il s’agit d’une limite pratique du point de vue de la facilité d’utilisation et de l’expérience de recherche.  

## <a name="return-codes"></a>Codes de retour
Hello, code d’état HTTP 200 signifie que cette demande hello a été reçue pour le traitement. Cela indique que hello est terminée avec succès.

Ce tableau répertorie hello ensemble complet de codes d’état que le service de hello peut retourner :

| Code | État | Code d'erreur | Description |
|:--- |:--- |:--- |:--- |
| 200 |OK | |demande de Hello a été acceptée. |
| 400 |Demande incorrecte |InactiveCustomer |espace de travail Hello a été fermé. |
| 400 |Demande incorrecte |InvalidApiVersion |version de Hello API que vous avez spécifié n’est pas reconnue par le service de hello. |
| 400 |Demande incorrecte |InvalidCustomerId |ID d’espace de travail Hello spécifié n’est pas valide. |
| 400 |Demande incorrecte |InvalidDataFormat |Un JSON non valide a été envoyé. corps de réponse Hello peut contenir plus d’informations sur la façon dont tooresolve hello erreur. |
| 400 |Demande incorrecte |InvalidLogType |indiquer le type de journal Hello contenus des caractères spéciaux ou des valeurs numériques. |
| 400 |Demande incorrecte |MissingApiVersion |version de l’API Hello n’a pas été spécifiée. |
| 400 |Demande incorrecte |MissingContentType |type de contenu Hello n’a pas été spécifié. |
| 400 |Demande incorrecte |MissingLogType |Hello obligatoire type de journal de valeur n’a pas été spécifié. |
| 400 |Demande incorrecte |UnsupportedContentType |type de contenu Hello n’a pas été défini trop**application/json**. |
| 403 |Interdit |InvalidAuthorization |service de Hello Échec de la demande de hello tooauthenticate. Vérifiez que cette clé d’espace de travail hello ID et de connexion sont valides. |
| 404 |Introuvable | | URL de hello fourni est incorrect, ou demande de hello est trop grande. |
| 429 |Trop de demandes | | Hello service rencontre un volume important de données à partir de votre compte. Réessayez plus tard la demande de hello. |
| 500 |Erreur interne du serveur |UnspecifiedError |service de Hello a rencontré une erreur interne. Réessayez la demande de hello. |
| 503 |Service indisponible |ServiceUnavailable |service de Hello est actuellement indisponible tooreceive demandes. Relancez la requête. |

## <a name="query-data"></a>Données de requête
données tooquery soumises par hello API du collecteur de journal Analytique HTTP données, rechercher des enregistrements avec **Type** qui est égale toohello **LogType** assorti de valeur que vous avez spécifié, **_CL**. Par exemple, si vous avez utilisé **MyCustomLog**, vous devriez retourner tous les enregistrements avec **Type=MyCustomLog_CL**.

>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis hello au-dessus de requête pourrait être modifié toohello suivant.

> `MyCustomLog_CL`

## <a name="sample-requests"></a>Exemples de demandes
Dans les sections suivantes hello, vous trouverez des exemples de toosubmit données toohello API du collecteur de données journal Analytique HTTP à l’aide de différents langages de programmation.

Pour chaque échantillon, effectuez ces étapes tooset les variables de hello pour l’en-tête d’autorisation hello :

1. Dans le portail Operations Management Suite hello, sélectionnez hello **paramètres** vignette, puis sélectionnez hello **Sources connectées** onglet.
2. toohello à droite de **ID de l’espace de travail**, sélectionnez l’icône de copie hello, puis collez hello ID en tant que valeur hello Hello **ID de client** variable.
3. toohello à droite de **clé primaire**, sélectionnez l’icône de copie hello, puis collez hello ID en tant que valeur hello Hello **Shared Key** variable.

Vous pouvez également modifier variables hello pour le type de journal hello et les données JSON.

### <a name="powershell-sample"></a>Exemple de code PowerShell
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

### <a name="c-sample"></a>Exemple de code C#
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

### <a name="python-sample"></a>Exemple de code Python
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

## <a name="next-steps"></a>Étapes suivantes
- Hello d’utilisation [API de recherche de journal](log-analytics-log-search-api.md) tooretrieve des données à partir du référentiel d’Analytique de journal hello.
