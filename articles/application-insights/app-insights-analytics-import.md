---
title: "aaaImport tooAnalytics de vos données dans Azure Application Insights | Documents Microsoft"
description: "Importer des toojoin de données statiques avec les données de télémétrie application, ou importer une tooquery de flux de données distinct avec Analytique."
services: application-insights
keywords: "schéma ouvert, importation de données"
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: bwren
ms.openlocfilehash: 7a3a3c9155adc1885dd366ddb13dda80bb894adb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-into-analytics"></a>Importer des données dans Analytics

Importer des données tabulaires dans [Analytique](app-insights-analytics.md), soit toojoin avec [Application Insights](app-insights-overview.md) télémétrie à partir de votre application, ou que vous pouvez les analyser comme un flux séparé. Analytique est un flux de haut volume horodaté de requête puissantes language tooanalyzing convient parfaitement de télémétrie.

Vous pouvez importer des données dans Analytics à l’aide de votre propre schéma. Il n’a pas toouse hello Application Insights des schémas standard telles que la demande ou de trace.

Vous pouvez importer des fichiers JSON ou DSV (valeurs séparées par des délimiteurs : virgule, point-virgule ou tabulation).

Il existe trois situations où il est utile de l’importation tooAnalytics :

* **Association avec la télémétrie de l’application.** Par exemple, vous pouvez importer une table qui mappe des URL à partir de vos titres de page lisible toomore site Web. Dans Analytique, vous pouvez créer un rapport de graphique du tableau de bord qui affiche des pages les plus populaires dix hello dans votre site Web. Il peut désormais afficher hello titres des pages au lieu de l’URL de hello.
* **Mettre en corrélation la télémétrie de votre application** avec d’autres sources telles que le trafic réseau, les données de serveur ou les fichiers journaux CDN.
* **Appliquer le flux de données distinct tooa Analytique.** Application Insights Analytics est un outil puissant, qui fonctionne bien avec les flux horodatés partiellement alloués, et même beaucoup mieux que SQL dans la plupart des cas. Si vous avez un flux de ce type issu d’une autre source, vous pouvez l’analyser avec Analytics.

Envoi source de données tooyour est facile. 

1. (Une fois) Définir le schéma hello de vos données dans une source de données.
2. (Périodiquement) Télécharger des tooAzure de stockage de données, puis appelez hello API REST toonotify nouvelles données en attente pour l’ingestion. Dans quelques minutes, les données de salutation soient disponibles pour la requête Analytique.

fréquence de téléchargement de hello Hello est définie par vous et la vitesse à laquelle vous souhaitez que votre toobe de données disponible pour les requêtes. Il est plus efficace des données tooupload en blocs plus volumineux, mais pas supérieure à 1 Go.

> [!NOTE]
> *Vous avez un grand nombre de tooanalyze des sources de données ?* [*Envisagez d’utiliser* logstash *tooship vos données dans Application Insights.*](https://github.com/Microsoft/logstash-output-application-insights)
> 

## <a name="before-you-start"></a>Avant de commencer

Ce dont vous avez besoin :

1. Une ressource Application Insights dans Microsoft Azure.

 * Si vous souhaitez tooanalyze vos données séparément à partir de toutes les autres données de télémétrie, [créer une ressource Application Insights](app-insights-create-new-resource.md).
 * Si vous utilisez jointure ou la comparaison de vos données avec les données de télémétrie à partir d’une application qui est déjà configurée avec Application Insights, vous pouvez utiliser les ressources hello pour cette application.
 * Ressource de toothat accès contributeur ou propriétaire.
 
2. stockage Azure. Vous téléchargez tooAzure stockage et Analytique obtienne de vos données à partir de là. 

 * Nous vous recommandons de créer un compte de stockage dédié pour vos blobs. Si vos objets BLOB est partagés avec d’autres processus, il est plus long pour notre tooread processus vos objets BLOB.


## <a name="define-your-schema"></a>Définir votre schéma

Vous pouvez importer des données, vous devez au préalable définir une *source de données,* qui spécifie le schéma hello de vos données.
Vous pouvez avoir des sources de données too50 dans une seule ressource Application Insights

1. Démarrer l’Assistant source de données hello. Utilisez le bouton Ajouter une nouvelle source de données. Vous pouvez également cliquer sur le bouton Paramètres en haut à droite, puis choisir Sources de données dans le menu déroulant.

    ![Ajouter une source de données](./media/app-insights-analytics-import/add-new-data-source.png)

    Entrez un nom pour votre nouvelle source de données.

2. Définir le format des fichiers hello que vous allez télécharger.

    Vous pouvez définir le format de hello manuellement, ou télécharger un exemple de fichier.

    Si les données de salutation sont au format CSV, hello de première ligne d’exemple hello permettre être des en-têtes de colonne. Vous pouvez modifier les noms de champs hello dans l’étape suivante de hello.

    exemple Hello doit inclure au moins 10 lignes ou des enregistrements de données.

    Les noms de colonnes ou de champs doivent avoir des noms alphanumériques (sans espaces ni ponctuation).

    ![Charger un exemple de fichier](./media/app-insights-analytics-import/sample-data-file.png)


3. Schéma hello révision hello Assistant a. Si il déduit les types hello à partir d’un échantillon, vous devrez peut-être tooadjust des types de hello déduit des colonnes de hello.

    ![Schéma de hello déduit de révision](./media/app-insights-analytics-import/data-source-review-schema.png)

 * (Facultatif.) Téléchargez une définition de schéma. Voir format hello ci-dessous.

 * Sélectionnez un horodatage. Toutes les données dans Analytics doivent avoir un champ d’horodatage. Elle doit être de type `datetime`, mais il n’est pas toobe nommé « timestamp ». Si vos données possèdent une colonne contenant une date et une heure au format ISO, choisissez cette option en tant que colonne de type timestamp hello. Sinon, choisissez « en tant que données arrivé » et les processus d’importation hello ajoute un champ d’horodatage.

5. Créer la source de données hello.

### <a name="schema-definition-file-format"></a>Format de fichier de définition de schéma

Plutôt que de modifier le schéma de hello dans l’interface utilisateur, vous pouvez charger la définition de schéma hello à partir d’un fichier. format de définition de schéma Hello est comme suit : 

Format délimité 
```
[ 
    {"location": "0", "name": "RequestName", "type": "string"}, 
    {"location": "1", "name": "timestamp", "type": "datetime"}, 
    {"location": "2", "name": "IPAddress", "type": "string"} 
] 
```

Format JSON 
```
[ 
    {"location": "$.name", "name": "name", "type": "string"}, 
    {"location": "$.alias", "name": "alias", "type": "string"}, 
    {"location": "$.room", "name": "room", "type": "long"} 
]
```
 
Chaque colonne est identifié par type, nom et l’emplacement de hello. 

* Emplacement – pour le format de fichier délimité, il est position hello de valeur de hello mappé. Pour le format JSON, il est jpath hello de clé de hello mappé.
* Nom : hello affiche le nom de colonne de hello.
* Type : type de données hello de cette colonne.
 
Au cas où un exemple de données a été utilisé et format de fichier est délimité, définition de schéma hello doit mapper toutes les colonnes et ajouter de nouvelles colonnes à la fin de hello. 

JSON permet un mappage partiel des données de hello, par conséquent hello définition de schéma du format JSON ne dispose pas toomap toutes les clés qui se trouve dans les exemples de données. Il peut également mapper des colonnes qui ne font pas partie des données d’exemple hello. 

## <a name="import-data"></a>Importer des données

tooimport des données, vous téléchargez-le tooAzure stockage, créer une clé d’accès pour celle-ci et appeler une API REST.

![Ajouter une source de données](./media/app-insights-analytics-import/analytics-upload-process.png)

Vous pouvez effectuer hello suivant le processus manuellement, ou définir d’une toodo automatique du système à intervalles réguliers. Vous devez toofollow ces étapes pour chaque bloc de données que vous souhaitez tooimport.

1. Télécharger les données de salutation trop[stockage d’objets blob Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md). 

 * Objets BLOB peuvent être n’importe quelle taille des too1GB non compressé. Les blobs d’une centaine de Mo sont parfaits, du point de vue des performances.
 * Vous pouvez les compresser avec le temps de téléchargement tooimprove Gzip et la latence pour hello toobe de données disponible pour la requête. Hello d’utilisation `.gz` extension de nom de fichier.
 * Il est meilleure toouse un compte de stockage distinct à cet effet, les appels de tooavoid à partir de différents services ralentit les performances.
 * Lors de l’envoi des données de haute fréquence, après quelques secondes, il est recommandé de toouse plus que d’un compte de stockage, pour des raisons de performances.

 
2. [Créer une clé de Signature d’accès partagé pour l’objet blob de hello](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md). clé de Hello doit disposer d’un délai d’expiration d’un jour et fournir un accès en lecture.
3. Rendre un toonotify d’appel REST Application Insights qui attendant des données.

 * Point de terminaison : `https://dc.services.visualstudio.com/v2/track`
 * Méthode HTTP : POST
 * Charge utile :

```JSON

    {
       "data": {
            "baseType":"OpenSchemaData",
            "baseData":{
               "ver":"2",
               "blobSasUri":"<Blob URI with Shared Access Key>",
               "sourceName":"<Schema ID>",
               "sourceVersion":"1.0"
             }
       },
       "ver":1,
       "name":"Microsoft.ApplicationInsights.OpenSchema",
       "time":"<DateTime>",
       "iKey":"<instrumentation key>"
    }
```

espaces réservés de Hello sont :

* `Blob URI with Shared Access Key`: Vous obtenez cette procédure de hello pour la création d’une clé. Il s’agit d’objet blob de toohello spécifique.
* `Schema ID`: hello ID schéma généré pour votre schéma défini. données Hello dans cet objet blob doivent être conforme toohello schéma.
* `DateTime`: heure de hello à quels hello demande est soumise, UTC. Nous acceptons les formats suivants : ISO8601 (comme « 2016-01-01 13:45:01 ») ; RFC822 (« Mer, 14 déc 16 14:57:01 +0000 ») ; RFC850 (« Mercredi, 14-déc-16 14:57:00 UTC ») ; RFC1123 (« Mer, 14 déc 2016 14:57:00 +0000 »).
* `Instrumentation key` de votre ressource Application Insights.

les données de salutation sont disponibles dans Analytique après quelques minutes.

## <a name="error-responses"></a>Réponses d’erreur

* **400 demande incorrecte**: indique cette charge utile de demande hello n’est pas valide. Vérifiez les points suivants :
 * Clé d’instrumentation correcte.
 * Valeur de temps valide. Il doit être hello maintenant en heure UTC.
 * JSON d’événement de hello est conforme toohello schéma.
* **403 Interdit**: blob hello que vous avez envoyé n’est pas accessible. Assurez-vous que cette clé d’accès partagé hello est valide et n’a pas expiré.
* **404 Introuvable** :
 * objet blob de Hello n’existe pas.
 * Hello sourceId est incorrecte.

Des informations plus détaillées sont disponibles dans le message d’erreur de réponse de hello.


## <a name="sample-code"></a>Exemple de code

Ce code utilise hello [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) package NuGet.

### <a name="classes"></a>Classes

```C#
namespace IngestionClient 
{ 
    using System; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceIngestionRequest 
    { 
        #region Members 
        private const string BaseDataRequiredVersion = "2"; 
        private const string RequestName = "Microsoft.ApplicationInsights.OpenSchema"; 
        #endregion Members 

        public AnalyticsDataSourceIngestionRequest(string ikey, string schemaId, string blobSasUri, int version = 1) 
        { 
            Ver = version; 
            IKey = ikey; 
            Data = new Data 
            { 
                BaseData = new BaseData 
                { 
                    Ver = BaseDataRequiredVersion, 
                    BlobSasUri = blobSasUri, 
                    SourceName = schemaId, 
                    SourceVersion = version.ToString() 
                } 
            }; 
        } 


        [JsonProperty("data")] 
        public Data Data { get; set; } 

        [JsonProperty("ver")] 
        public int Ver { get; set; } 

        [JsonProperty("name")] 
        public string Name { get { return RequestName; } } 

        [JsonProperty("time")] 
        public DateTime Time { get { return DateTime.UtcNow; } } 

        [JsonProperty("iKey")] 
        public string IKey { get; set; } 
    } 

    #region Internal Classes 

    public class Data 
    { 
        private const string DataBaseType = "OpenSchemaData"; 

        [JsonProperty("baseType")] 
        public string BaseType 
        { 
            get { return DataBaseType; } 
        } 

        [JsonProperty("baseData")] 
        public BaseData BaseData { get; set; } 
    } 


    public class BaseData 
    { 
        [JsonProperty("ver")] 
        public string Ver { get; set; } 

        [JsonProperty("blobSasUri")] 
        public string BlobSasUri { get; set; } 

        [JsonProperty("sourceName")] 
        public string SourceName { get; set; } 

        [JsonProperty("sourceVersion")] 
        public string SourceVersion { get; set; } 
    } 

    #endregion Internal Classes 
} 


namespace IngestionClient 
{ 
    using System; 
    using System.IO; 
    using System.Net; 
    using System.Text; 
    using System.Threading.Tasks; 
    using Newtonsoft.Json; 

    public class AnalyticsDataSourceClient 
    { 
        #region Members 
        private readonly Uri endpoint = new Uri("https://dc.services.visualstudio.com/v2/track"); 
        private const string RequestContentType = "application/json; charset=UTF-8"; 
        private const string RequestAccess = "application/json"; 
        #endregion Members 

        #region Public 

        public async Task<bool> RequestBlobIngestion(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            HttpWebRequest request = WebRequest.CreateHttp(endpoint); 
            request.Method = WebRequestMethods.Http.Post; 
            request.ContentType = RequestContentType; 
            request.Accept = RequestAccess; 

            string notificationJson = Serialize(ingestionRequest); 
            byte[] notificationBytes = GetContentBytes(notificationJson); 
            request.ContentLength = notificationBytes.Length; 

            Stream requestStream = request.GetRequestStream(); 
            requestStream.Write(notificationBytes, 0, notificationBytes.Length); 
            requestStream.Close(); 

            try 
            { 
                using (var response = (HttpWebResponse)await request.GetResponseAsync())
                {
                    return response.StatusCode == HttpStatusCode.OK;
                }
            } 
            catch (WebException e) 
            { 
                HttpWebResponse httpResponse = e.Response as HttpWebResponse; 
                if (httpResponse != null) 
                { 
                    Console.WriteLine( 
                        "Ingestion request failed with status code: {0}. Error: {1}", 
                        httpResponse.StatusCode, 
                        httpResponse.StatusDescription); 
                    return false; 
                }
                throw; 
            } 
        } 
        #endregion Public 

        #region Private 
        private byte[] GetContentBytes(string content) 
        { 
            return Encoding.UTF8.GetBytes(content);
        } 


        private string Serialize(AnalyticsDataSourceIngestionRequest ingestionRequest) 
        { 
            return JsonConvert.SerializeObject(ingestionRequest); 
        } 
        #endregion Private 
    } 
} 
```

### <a name="ingest-data"></a>Réception de données

Utilisez ce code pour chaque blob. 

```C#
   AnalyticsDataSourceClient client = new AnalyticsDataSourceClient(); 

   var ingestionRequest = new AnalyticsDataSourceIngestionRequest("iKey", "sourceId", "blobUrlWithSas"); 

   bool success = await client.RequestBlobIngestion(ingestionRequest);
```

## <a name="next-steps"></a>Étapes suivantes

* [Visite guidée de hello langage de requête Analytique de journal](app-insights-analytics-tour.md)
* [Utilisez *Logstash* toosend données tooApplication Insights](https://github.com/Microsoft/logstash-output-application-insights)
