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
# <a name="azure-mobile-engagement---api-integration"></a><span data-ttu-id="13e7b-103">Azure Mobile Engagement - Intégration dans une API</span><span class="sxs-lookup"><span data-stu-id="13e7b-103">Azure Mobile Engagement - API integration</span></span>
<span data-ttu-id="13e7b-104">Dans un système automatisé de marketing, création et l’activation hello également des campagnes marketing se produisent automatiquement.</span><span class="sxs-lookup"><span data-stu-id="13e7b-104">In an automated marketing system, creating and activating hello marketing campaigns also occur automatically.</span></span> <span data-ttu-id="13e7b-105">À cette fin, Azure Mobile Engagement permet également de créer ces campagnes marketing automatisées à l'aide d’API.</span><span class="sxs-lookup"><span data-stu-id="13e7b-105">For this purpose - Azure Mobile Engagement enables creating such automated marketing campaigns using APIs as well.</span></span> 

<span data-ttu-id="13e7b-106">En général, les clients utiliser hello Mobile Engagement front-end interface toocreate annonces/interroge etc. dans le cadre de leurs campagnes marketing.</span><span class="sxs-lookup"><span data-stu-id="13e7b-106">Typically customers use hello Mobile Engagement front end interface toocreate announcements/polls etc as part of their marketing campaigns.</span></span> <span data-ttu-id="13e7b-107">Toutefois, en tant que hello adulte des campagnes marketing, il est nécessaire tooleverage les données de salutation verrouillé dans les systèmes back-end hello (comme n’importe quel système CRM ou un système CMS, tel que SharePoint) afin qu’un pipeline entièrement automatisé peut être créé, ce qui crée des campagnes dans Mobile Engagement dynamiquement selon les données de salutation provenance dans des systèmes principaux de hello.</span><span class="sxs-lookup"><span data-stu-id="13e7b-107">However as hello marketing campaigns become mature, there is a need tooleverage hello data locked in hello backend systems (like any CRM system or CMS system like SharePoint) so that a fully automated pipeline can be created which creates campaigns in Mobile Engagement dynamically based on hello data flowing in from hello backend systems.</span></span> 

![][5]

<span data-ttu-id="13e7b-108">Ce didacticiel atteint un scénario où un utilisateur SharePoint remplit une liste SharePoint avec les données de marketing et un processus automatisé récupère des éléments de liste de hello et se connecte à l’aide de système de Mobile Engagement hello hello API REST disponibles toocreate une campagne marketing à partir des données de SharePoint hello.</span><span class="sxs-lookup"><span data-stu-id="13e7b-108">This tutorial goes through such a scenario where a SharePoint business user populates a SharePoint list with marketing data and an automated process picks up items from hello list and connects with hello Mobile Engagement system using hello available REST APIs toocreate a marketing campaign from hello SharePoint data.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="13e7b-109">En règle générale, vous pouvez utiliser cet exemple comme point de départ pour comprendre comment toocall toutes les API de REST Mobile Engagement tel qu’il détaille hello deux principaux aspects de l’appel de hello API - authentification et en passant les paramètres.</span><span class="sxs-lookup"><span data-stu-id="13e7b-109">In general, you can use this sample as a starting point for understanding how toocall any Mobile Engagement REST API as it details hello two key aspects of calling hello APIs - authenticating and passing parameters.</span></span> 
> 
> 

## <a name="sharepoint-integration"></a><span data-ttu-id="13e7b-110">Intégration de SharePoint</span><span class="sxs-lookup"><span data-stu-id="13e7b-110">SharePoint integration</span></span>
1. <span data-ttu-id="13e7b-111">Voici les exemples hello SharePoint liste ressemble à.</span><span class="sxs-lookup"><span data-stu-id="13e7b-111">Here is what hello sample SharePoint list looks like.</span></span> <span data-ttu-id="13e7b-112">**Titre**, **catégorie**, **NotificationTitle**, **Message** et **URL** sont utilisés pour la création d’annonce de type hello.</span><span class="sxs-lookup"><span data-stu-id="13e7b-112">**Title**, **Category**, **NotificationTitle**, **Message** and **URL** are used for creating hello announcement.</span></span> <span data-ttu-id="13e7b-113">Il existe une colonne appelée **IsProcessed** qui est utilisé par le processus d’automatisation exemple hello sous forme de hello d’un programme de console.</span><span class="sxs-lookup"><span data-stu-id="13e7b-113">There is a column called **IsProcessed** which is used by hello sample automation process in hello form of a console program.</span></span> <span data-ttu-id="13e7b-114">Vous pouvez exécuter ce programme de console en tant qu’une tâche Web Azure afin que vous pouvez la planifier, ou vous pouvez utiliser directement activation annonce de type hello et de création de tooprogram de flux de travail SharePoint hello lorsqu’un élément est inséré dans la liste SharePoint de hello.</span><span class="sxs-lookup"><span data-stu-id="13e7b-114">You can either run this console program as an Azure WebJob so that you can schedule it or you can directly use hello SharePoint workflow tooprogram creating and activating hello announcement when an item is inserted into hello SharePoint list.</span></span> <span data-ttu-id="13e7b-115">Dans cet exemple, nous utilisons programme de console hello qui passe à travers les éléments hello Bonjour SharePoint puis créez l’annonce dans Azure Mobile Engagement pour chacun d’eux et enfin marque ensuite hello **IsProcessed** la valeur true toobe indicateur en Création de l’annonce réussie.</span><span class="sxs-lookup"><span data-stu-id="13e7b-115">In this sample we use hello console program which goes through hello items in hello SharePoint list and create announcement in Azure Mobile Engagement for each of them and then finally marks hello **IsProcessed** flag toobe true on successful announcement creation.</span></span>
   
    ![][1]
2. <span data-ttu-id="13e7b-116">Nous utilisons le code hello à partir de l’exemple hello *l’authentification à distance dans SharePoint Online à l’aide de hello modèle objet Client* [ici](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate avec une liste SharePoint de hello.</span><span class="sxs-lookup"><span data-stu-id="13e7b-116">We are using hello code from hello sample *Remote Authentication in SharePoint Online Using hello Client Object Model* [here](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate with hello SharePoint list.</span></span>
3. <span data-ttu-id="13e7b-117">Une fois authentifié, nous boucle toofind d’éléments de liste hello les éléments nouvellement créée (qui a **IsProcessed** = false).</span><span class="sxs-lookup"><span data-stu-id="13e7b-117">Once authenticated, we loop through hello list items toofind out any newly created items (which will have **IsProcessed** = false).</span></span> 
   
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

## <a name="mobile-engagement-integration"></a><span data-ttu-id="13e7b-118">Intégration à Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="13e7b-118">Mobile Engagement integration</span></span>
1. <span data-ttu-id="13e7b-119">Une fois que nous trouver un élément qui requiert un traitement - nous extraire des informations de hello requis toocreate une annonce de hello d’élément de liste et appelez `CreateAzMECampaign` toocreate il et ensuite `ActivateAzMECampaign` tooactivate il.</span><span class="sxs-lookup"><span data-stu-id="13e7b-119">Once we find an item which requires processing - we extract hello information required toocreate an announcement from hello list item and call `CreateAzMECampaign` toocreate it and subsequently `ActivateAzMECampaign` tooactivate it.</span></span> <span data-ttu-id="13e7b-120">Il s’agit essentiellement les appels d’API REST appelant toohello Mobile Engagement principal.</span><span class="sxs-lookup"><span data-stu-id="13e7b-120">These are essentially REST API calls calling toohello Mobile Engagement backend.</span></span> 
2. <span data-ttu-id="13e7b-121">Hello Mobile Engagement REST API exigent un **en-tête d’autorisation HTTP authentification de base schéma** qui se compose de hello `ApplicationId` et hello `ApiKey` qui vous obtenez à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="13e7b-121">hello Mobile Engagement REST APIs require a **Basic auth scheme authorization HTTP header** which is composed of hello `ApplicationId` and hello `ApiKey` which you get from hello Azure portal.</span></span> <span data-ttu-id="13e7b-122">Assurez-vous que vous utilisez hello clé à partir de hello **clés api** section et *pas* de hello **clés du Kit de développement logiciel** section.</span><span class="sxs-lookup"><span data-stu-id="13e7b-122">Make sure that you are using hello Key from hello **api keys** section and *not* from hello **sdk keys** section.</span></span> 
   
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
3. <span data-ttu-id="13e7b-123">Pour créer le type d’annonce hello de campagne - consultez toohello [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span><span class="sxs-lookup"><span data-stu-id="13e7b-123">For creating hello announcement type campaign - refer toohello [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span></span> <span data-ttu-id="13e7b-124">Vous devez toomake que de spécifier les campagnes hello `kind` en tant que *annonce* et hello [charge utile](https://msdn.microsoft.com/library/azure/mt683751.aspx) et en lui passant comme FormUrlEncodedContent.</span><span class="sxs-lookup"><span data-stu-id="13e7b-124">You need toomake sure that you are specifying hello campaign `kind` as *announcement* and hello [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) and passing it as FormUrlEncodedContent.</span></span> 
   
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
4. <span data-ttu-id="13e7b-125">Une fois que vous avez créé de l’annonce de type hello, vous verrez quelque chose comme hello suivant sur le portail Mobile Engagement hello (Notez que hello état = Brouillon et activé = non applicable)</span><span class="sxs-lookup"><span data-stu-id="13e7b-125">Once you have hello announcement created, you will see something like hello following on hello Mobile Engagement portal (note that hello State=Draft and Activated = N/A)</span></span>
   
    ![][3]
5. <span data-ttu-id="13e7b-126">`CreateAzMECampaign`Crée une campagne annonce et retourne son appelant toohello de code.</span><span class="sxs-lookup"><span data-stu-id="13e7b-126">`CreateAzMECampaign` creates an announcement campaign and returns its Id toohello caller.</span></span> <span data-ttu-id="13e7b-127">`ActivateAzMECampaign`requiert cet Id de campagne de hello paramètre tooactivate hello.</span><span class="sxs-lookup"><span data-stu-id="13e7b-127">`ActivateAzMECampaign` requires this Id as hello parameter tooactivate hello campaign.</span></span> 
   
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
6. <span data-ttu-id="13e7b-128">Une fois que vous avez activé de l’annonce de type hello, vous verrez hello suivant sur le portail Mobile Engagement hello :</span><span class="sxs-lookup"><span data-stu-id="13e7b-128">Once you have hello announcement activated, you will see something like hello following on hello Mobile Engagement portal:</span></span>
   
    ![][4]
7. <span data-ttu-id="13e7b-129">Dès que la campagne de hello est activée, tous les périphériques qui satisfont le critère hello campagne de hello commencerez à voir des notifications.</span><span class="sxs-lookup"><span data-stu-id="13e7b-129">As soon as hello campaign gets activated, any devices which satisfy hello criterion on hello campaign will start seeing notifications.</span></span> 
8. <span data-ttu-id="13e7b-130">Vous remarquerez également cet élément de liste hello marquée avec IsProcessed = false a été défini tooTrue une fois la campagne d’annonce hello est créé.</span><span class="sxs-lookup"><span data-stu-id="13e7b-130">You will also notice that hello list item marked with IsProcessed = false has been set tooTrue once hello announcement campaign is created.</span></span>  

<span data-ttu-id="13e7b-131">Cet exemple créé une campagne annonce simple définition principalement des propriétés hello requis.</span><span class="sxs-lookup"><span data-stu-id="13e7b-131">This sample created a simple announcement campaign specifying mostly hello required properties.</span></span> <span data-ttu-id="13e7b-132">Vous pouvez le personnaliser autant que possible à partir du portail de hello en utilisant les informations de hello [ici](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span><span class="sxs-lookup"><span data-stu-id="13e7b-132">You can customize this as much as you can from hello portal by using hello information [here](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span></span> 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



