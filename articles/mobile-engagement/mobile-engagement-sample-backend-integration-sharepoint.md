---
title: "aaaAzure Mobile Engagement - intégration de serveur principal"
description: "Se connecter d’Azure Mobile Engagement avec un serveur principal SharePoint toocreate les campagnes à partir de SharePoint"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 06297b43-579f-46e6-8a58-961a68f9aa09
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 89e1ef57db607d63c326a760b20260ad439f08b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---api-integration"></a>Azure Mobile Engagement - Intégration dans une API
Dans un système automatisé de marketing, création et l’activation hello également des campagnes marketing se produisent automatiquement. À cette fin, Azure Mobile Engagement permet également de créer ces campagnes marketing automatisées à l'aide d’API. 

En général, les clients utiliser hello Mobile Engagement front-end interface toocreate annonces/interroge etc. dans le cadre de leurs campagnes marketing. Toutefois, en tant que hello adulte des campagnes marketing, il est nécessaire tooleverage les données de salutation verrouillé dans les systèmes back-end hello (comme n’importe quel système CRM ou un système CMS, tel que SharePoint) afin qu’un pipeline entièrement automatisé peut être créé, ce qui crée des campagnes dans Mobile Engagement dynamiquement selon les données de salutation provenance dans des systèmes principaux de hello. 

![][5]

Ce didacticiel atteint un scénario où un utilisateur SharePoint remplit une liste SharePoint avec les données de marketing et un processus automatisé récupère des éléments de liste de hello et se connecte à l’aide de système de Mobile Engagement hello hello API REST disponibles toocreate une campagne marketing à partir des données de SharePoint hello. 

> [!IMPORTANT]
> En règle générale, vous pouvez utiliser cet exemple comme point de départ pour comprendre comment toocall toutes les API de REST Mobile Engagement tel qu’il détaille hello deux principaux aspects de l’appel de hello API - authentification et en passant les paramètres. 
> 
> 

## <a name="sharepoint-integration"></a>Intégration de SharePoint
1. Voici les exemples hello SharePoint liste ressemble à. **Titre**, **catégorie**, **NotificationTitle**, **Message** et **URL** sont utilisés pour la création d’annonce de type hello. Il existe une colonne appelée **IsProcessed** qui est utilisé par le processus d’automatisation exemple hello sous forme de hello d’un programme de console. Vous pouvez exécuter ce programme de console en tant qu’une tâche Web Azure afin que vous pouvez la planifier, ou vous pouvez utiliser directement activation annonce de type hello et de création de tooprogram de flux de travail SharePoint hello lorsqu’un élément est inséré dans la liste SharePoint de hello. Dans cet exemple, nous utilisons programme de console hello qui passe à travers les éléments hello Bonjour SharePoint puis créez l’annonce dans Azure Mobile Engagement pour chacun d’eux et enfin marque ensuite hello **IsProcessed** la valeur true toobe indicateur en Création de l’annonce réussie.
   
    ![][1]
2. Nous utilisons le code hello à partir de l’exemple hello *l’authentification à distance dans SharePoint Online à l’aide de hello modèle objet Client* [ici](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate avec une liste SharePoint de hello.
3. Une fois authentifié, nous boucle toofind d’éléments de liste hello les éléments nouvellement créée (qui a **IsProcessed** = false). 
   
         static async void CreateCampaignFromSharepoint()
        {
            using (ClientContext clientContext = ClaimClientContext.GetAuthenticatedContext(targetSharepointSite))
            {
                // Using https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c for authentication     
                Web site = clientContext.Web;
                List list = site.Lists.GetByTitle("VideoContent");
                CamlQuery query = new CamlQuery();
                query.ViewXml = "<View/>";
                ListItemCollection items = list.GetItems(query);
   
                // Load hello SharePoint list
                clientContext.Load(list);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
   
                // Loop through hello list toogo through all hello items which are newly added
                foreach (ListItem item in items)
                    if (item["IsProcessed"].ToString() != "Yes")
                    {
                        string name = item["Title"].ToString();
                        string notificationTitle = item["NotificationTitle"].ToString();
                        string notificationMessage = item["Message"].ToString();
                        string category = item["Category"].ToString();
                        string actionURL = ((FieldUrlValue)item["URL"]).Url;
   
                        // Send an HTTP request toocreate AzME campaign
                        int campaignId = CreateAzMECampaign
                            (name, notificationTitle, notificationMessage, category, actionURL).Result;
   
                        if (campaignId != -1)
                        {
                            // If creating campaign is successful then set this tootrue
                            item["IsProcessed"] = "Yes";
   
                            // Now try tooactivate hello campaign also
                            await ActivateAzMECampaign(campaignId);
                        }
                        else
                        {
                            item["IsProcessed"] = "Error";
                        }
                        item.Update();
                    }
                clientContext.ExecuteQuery();
            }
        }

## <a name="mobile-engagement-integration"></a>Intégration à Mobile Engagement
1. Une fois que nous trouver un élément qui requiert un traitement - nous extraire des informations de hello requis toocreate une annonce de hello d’élément de liste et appelez `CreateAzMECampaign` toocreate il et ensuite `ActivateAzMECampaign` tooactivate il. Il s’agit essentiellement les appels d’API REST appelant toohello Mobile Engagement principal. 
2. Hello Mobile Engagement REST API exigent un **en-tête d’autorisation HTTP authentification de base schéma** qui se compose de hello `ApplicationId` et hello `ApiKey` qui vous obtenez à partir de hello portail Azure. Assurez-vous que vous utilisez hello clé à partir de hello **clés api** section et *pas* de hello **clés du Kit de développement logiciel** section. 
   
   ![][2]
   
       static string CreateAuthZHeader()
       {
           string BasicAuthzHeaderString = "Basic " + EncodeTo64(ApplicationId + ":" + ApiKey);
           return BasicAuthzHeaderString;
       }
   
       static public string EncodeTo64(string toEncode)
       {
           byte[] toEncodeAsBytes = System.Text.ASCIIEncoding.ASCII.GetBytes(toEncode);
           string returnValue = System.Convert.ToBase64String(toEncodeAsBytes);
           return returnValue;
       }  
3. Pour créer le type d’annonce hello de campagne - consultez toohello [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx). Vous devez toomake que de spécifier les campagnes hello `kind` en tant que *annonce* et hello [charge utile](https://msdn.microsoft.com/library/azure/mt683751.aspx) et en lui passant comme FormUrlEncodedContent. 
   
        static async Task<int> CreateAzMECampaign(string campaignName, string notificationTitle, 
            string notificationMessage, string notificationCategory, string actionURL)
        {
            string createURIFragment = "/reach/1/create";
   
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                // Create hello payload toosend hello content
                // Reference -> https://msdn.microsoft.com/library/dn913749.aspx
                string data =
                    @"{""name"":""" + campaignName + @"""," + 
                    @"""type"":""only_notif""," + 
                    @"""deliveryTime"":""any"","" + 
                    @""notificationTitle"":""" + notificationTitle + 
                    @""",""notificationMessage"":""" + notificationMessage + 
                    @""",""actionUrl"":""" + actionURL + @"""}";
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("data", data),
                });
   
                // Send hello POST request
                var response = await client.PostAsync(url + createURIFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                int campaignId = -1;
                if (response.StatusCode.ToString() == "OK")
                {
                    // This is hello campaign id
                    campaignId = Convert.ToInt32(responseString);
                    Console.WriteLine("Campaign successfully created with id {0}", campaignId);
                }
                else
                {
                    Console.WriteLine("Campaign creation failed with error - '{0}'", responseString);
                }
                return campaignId;
            }
        }
4. Une fois que vous avez créé de l’annonce de type hello, vous verrez quelque chose comme hello suivant sur le portail Mobile Engagement hello (Notez que hello état = Brouillon et activé = non applicable)
   
    ![][3]
5. `CreateAzMECampaign`Crée une campagne annonce et retourne son appelant toohello de code. `ActivateAzMECampaign`requiert cet Id de campagne de hello paramètre tooactivate hello. 
   
        static async Task<bool> ActivateAzMECampaign(int campaignId)
        {
            string activateUriFragment = "/reach/1/activate";
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("id", campaignId.ToString()),
                });
   
                // Send hello POST request
                var response = await client.PostAsync(url + activateUriFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                if (response.StatusCode.ToString() == "OK")
                {
                    Console.WriteLine("Campaign successfully activated");
                    return true;
                }
                else
                {
                    Console.WriteLine("Campaign activation failed with error - '{0}'", responseString);
                    return false;
                }
            }
        }
6. Une fois que vous avez activé de l’annonce de type hello, vous verrez hello suivant sur le portail Mobile Engagement hello :
   
    ![][4]
7. Dès que la campagne de hello est activée, tous les périphériques qui satisfont le critère hello campagne de hello commencerez à voir des notifications. 
8. Vous remarquerez également cet élément de liste hello marquée avec IsProcessed = false a été défini tooTrue une fois la campagne d’annonce hello est créé.  

Cet exemple créé une campagne annonce simple définition principalement des propriétés hello requis. Vous pouvez le personnaliser autant que possible à partir du portail de hello en utilisant les informations de hello [ici](https://msdn.microsoft.com/library/azure/mt683751.aspx). 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



