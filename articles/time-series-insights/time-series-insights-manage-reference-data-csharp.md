---
title: "aaaManage les données de référence pour un environnement Azure Insights de série de temps à l’aide de C# | Documents Microsoft"
description: "Ce didacticiel décrit comment toomanage données de référence pour un environnement Azure Insights de série de temps à l’aide de c#"
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 77b85aa7f9a5dc46c132afa56c82df48f41577fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-reference-data-for-an-azure-time-series-insights-environment-by-using-c"></a>Gérer des données de référence pour un environnement Azure Time Series Insights à l’aide de C#

Cet exemple c# montre comment toomanage référencer des données pour un environnement Azure Insights de série de temps.
Avant d’en cours d’exécution exemple hello, vérifiez hello suivant étapes est terminée.
1. Un jeu de données de référence a été créé à l’aide de [cet article](time-series-insights-add-reference-data-set.md).
2. jeton d’accès Hello utilisé lors de l’application hello en cours d’exécution est obtenu via hello API Azure Active Directory. Ce jeton doit être passé hello `Authorization` en-tête de chaque demande de requête API. Pour configurer les applications non interactives, consultez hello [authentification et autorisation](time-series-insights-authentication-and-authorization.md) l’article.
3. Toutes les constantes hello définies au début de hello d’exemple hello sont correctement définies.

## <a name="c-sample"></a>Exemple de code C#

```csharp
// Copyright (c) Microsoft Corporation.  All rights reserved.

using System;
using System.IO;
using System.Net;
using System.Threading.Tasks;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

namespace TimeSeriesInsightsReferenceDataSampleApp
{
    public static class Program
    {
        // SET hello environment fqdn.
        private static string EnvironmentFqdn = "#DUMMY#.env.timeseries.azure.com";

        // SET hello environment reference data set name used when creating it.
        private static string EnvironmentReferenceDataSetName = "#DUMMY#";

        // For automated execution under application identity,
        // use application created in Active Directory.
        // toocreate hello application in AAD, follow hello steps provided here:
        // https://docs.microsoft.com/en-us/azure/time-series-insights/time-series-insights-authentication-and-authorization

        // SET hello application ID of application registered in your Azure Active Directory
        private static string ApplicationClientId = "#DUMMY#";

        // SET hello application key of hello application registered in your Azure Active Directory
        private static string ApplicationClientSecret = "#DUMMY#";

        // SET hello Azure Active Directory tenant.
        private static string Tenant = "#DUMMY#.onmicrosoft.com";

        private static async Task DemoReferenceDataAsync()
        {
            // 1. Acquire an access token.
            string accessToken = await AcquireAccessTokenAsync();

            // 2. Put a new reference data item.
            {
                HttpWebRequest request = CreateWebRequest(accessToken);
                string input = @"
{
    ""put"": [{
        ""DeviceId"": ""Fan1"",
        ""Type"": ""Fan"",
        ""BladeCount"": ""3""
    }]
}";
                await SendRequestAsync(request, input);
                string output = await GetResponseAsync(request);
                PrintInputOutput(action: "Put", input: input, output: output);
            }

            // 3. Get reference data item.
            {
                HttpWebRequest request = CreateWebRequest(accessToken);
                string input = @"
{
    ""get"": [{
        ""DeviceId"": ""Fan1""
    }]
}";
                await SendRequestAsync(request, input);
                string output = await GetResponseAsync(request);
                PrintInputOutput(action: "Get", input: input, output: output);
            }

            // 4. Patch an existing reference data item.
            // Update BladeCount and add Colour.
            {
                HttpWebRequest request = CreateWebRequest(accessToken);
                string input = @"
{
    ""patch"": [{
        ""DeviceId"": ""Fan1"",
        ""BladeCount"": ""4"",
        ""Colour"": ""Brown""
    }]
}";
                await SendRequestAsync(request, input);
                string output = await GetResponseAsync(request);
                PrintInputOutput(action: "Patch", input: input, output: output);
            }

            // 5. Delete a property from an existing reference data item.
            {
                HttpWebRequest request = CreateWebRequest(accessToken);
                string input = @"
{
    ""deleteproperties"": [{
        ""key"": {
            ""DeviceId"": ""Fan1""
        },
        ""properties"": [""BladeCount""]
    }]
}";
                await SendRequestAsync(request, input);
                string output = await GetResponseAsync(request);
                PrintInputOutput(action: "DeleteProperties", input: input, output: output);
            }

            // 6. Delete an existing reference data item.
            {
                HttpWebRequest request = CreateWebRequest(accessToken);
                string input = @"
{
    ""delete"": [{
        ""DeviceId"": ""Fan1""
    }]
}";
                await SendRequestAsync(request, input);
                string output = await GetResponseAsync(request);
                PrintInputOutput(action: "Delete", input: input, output: output);
            }
        }

        private static async Task<string> AcquireAccessTokenAsync()
        {
            if (ApplicationClientId == "#DUMMY#" || ApplicationClientSecret == "#DUMMY#" || Tenant.StartsWith("#DUMMY#"))
            {
                throw new Exception(
                    $"Use hello link {"https://docs.microsoft.com/en-us/azure/time-series-insights/time-series-insights-authentication-and-authorization"} tooupdate hello values of 'ApplicationClientId', 'ApplicationClientSecret' and 'Tenant'.");
            }

            var authenticationContext = new AuthenticationContext(
                $"https://login.windows.net/{Tenant}",
                TokenCache.DefaultShared);

            AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
                resource: "https://api.timeseries.azure.com/",
                clientCredential: new ClientCredential(
                    clientId: ApplicationClientId,
                    clientSecret: ApplicationClientSecret));

            // Show interactive logon dialog tooacquire token on behalf of hello user.
            // Suitable for native apps, and not on server-side of a web application.
            //AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
            //    resource: "https://api.timeseries.azure.com/",
            //    // Set well-known client ID for Azure PowerShell
            //    clientId: "1950a258-227b-4e31-a9cf-717495945fc2",
            //    // Set redirect URI for Azure PowerShell
            //    redirectUri: new Uri("urn:ietf:wg:oauth:2.0:oob"),
            //    parameters: new PlatformParameters(PromptBehavior.Auto));

            return token.AccessToken;
        }

        private static HttpWebRequest CreateWebRequest(string accessToken)
        {
            Uri uri = new UriBuilder("https", EnvironmentFqdn)
            {
                Path = $"referencedatasets/{EnvironmentReferenceDataSetName}/$batch",
                Query = "api-version=2016-12-12"
            }.Uri;
            HttpWebRequest request = WebRequest.CreateHttp(uri);
            request.Method = "POST";
            request.Headers.Add("x-ms-client-application-name", "TimeSeriesInsightsReferenceDataSample");
            request.Headers.Add("Authorization", "Bearer " + accessToken);
            return request;
        }

        private static async Task SendRequestAsync(HttpWebRequest request, string json)
        {
            using (var stream = await request.GetRequestStreamAsync())
            using (var streamWriter = new StreamWriter(stream))
            {
                await streamWriter.WriteAsync(json);
                await streamWriter.FlushAsync();
                streamWriter.Close();
            }
        }

        private static async Task<string> GetResponseAsync(HttpWebRequest request)
        {
            using (WebResponse webResponse = await request.GetResponseAsync())
            using (var sr = new StreamReader(webResponse.GetResponseStream()))
            {
                string result = await sr.ReadToEndAsync();
                return result;
            }
        }

        private static void PrintInputOutput(string action, string input, string output)
        {
            Console.WriteLine("=== {0} request ===", action);
            Console.WriteLine("Input: {0}", JsonConvert.SerializeObject(JsonConvert.DeserializeObject<JObject>(input), Formatting.Indented));
            Console.WriteLine("Output: {0}", JsonConvert.SerializeObject(JsonConvert.DeserializeObject<JObject>(output), Formatting.Indented));
            Console.WriteLine();
        }

        static void Main(string[] args)
        {
            Task.Run(async () => await DemoReferenceDataAsync()).Wait();
        }
    }
}
```

## <a name="next-steps"></a>Étapes suivantes

Pour la référence d’API complète hello, consultez [API de données de référence](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.