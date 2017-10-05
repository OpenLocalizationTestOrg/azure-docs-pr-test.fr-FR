---
title: "Azure Mobile Engagement - Intégration au serveur principal"
description: "Connexion d’Azure Mobile Engagement avec un serveur principal SharePoint pour créer des campagnes à partir de SharePoint"
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
ms.openlocfilehash: d49f1094f4c3f170f3618f3e19e42266f9ae8858
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement---api-integration"></a><span data-ttu-id="3a3d3-103">Azure Mobile Engagement - Intégration dans une API</span><span class="sxs-lookup"><span data-stu-id="3a3d3-103">Azure Mobile Engagement - API integration</span></span>
<span data-ttu-id="3a3d3-104">Dans un système marketing automatisé, la création et l'activation des campagnes marketing peuvent également être automatiques.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-104">In an automated marketing system, creating and activating the marketing campaigns also occur automatically.</span></span> <span data-ttu-id="3a3d3-105">À cette fin, Azure Mobile Engagement permet également de créer ces campagnes marketing automatisées à l'aide d’API.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-105">For this purpose - Azure Mobile Engagement enables creating such automated marketing campaigns using APIs as well.</span></span> 

<span data-ttu-id="3a3d3-106">En général, les clients utilisent l'interface frontale de Mobile Engagement pour créer des annonces/sondages et autres dans le cadre de leurs campagnes marketing.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-106">Typically customers use the Mobile Engagement front end interface to create announcements/polls etc as part of their marketing campaigns.</span></span> <span data-ttu-id="3a3d3-107">Toutefois, à mesure que les campagnes marketing mûrissent, il est nécessaire d'exploiter les données enfermées dans les systèmes principaux (comme n'importe quel système de  CRM ou CMS comme SharePoint) afin qu'un pipeline entièrement automatisé puisse être créé pour générer des campagnes de façon dynamique dans Mobile Engagement en se basant sur les données contenues dans les systèmes principaux.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-107">However as the marketing campaigns become mature, there is a need to leverage the data locked in the backend systems (like any CRM system or CMS system like SharePoint) so that a fully automated pipeline can be created which creates campaigns in Mobile Engagement dynamically based on the data flowing in from the backend systems.</span></span> 

![][5]

<span data-ttu-id="3a3d3-108">Ce didacticiel se base sur un scénario dans lequel un utilisateur SharePoint remplit une liste SharePoint de données marketing, dont les éléments sont récupérés par un processus automatisé qui se connecte au système Mobile Engagement à l'aide des API REST disponibles afin de créer une campagne marketing à partir des données SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-108">This tutorial goes through such a scenario where a SharePoint business user populates a SharePoint list with marketing data and an automated process picks up items from the list and connects with the Mobile Engagement system using the available REST APIs to create a marketing campaign from the SharePoint data.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="3a3d3-109">En général, vous pouvez utiliser cet exemple comme point de départ pour comprendre comment appeler les API REST Mobile Engagement, car il détaille les deux principaux aspects de l'appel des API : l’authentification et le passage des paramètres.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-109">In general, you can use this sample as a starting point for understanding how to call any Mobile Engagement REST API as it details the two key aspects of calling the APIs - authenticating and passing parameters.</span></span> 
> 
> 

## <a name="sharepoint-integration"></a><span data-ttu-id="3a3d3-110">Intégration de SharePoint</span><span class="sxs-lookup"><span data-stu-id="3a3d3-110">SharePoint integration</span></span>
1. <span data-ttu-id="3a3d3-111">L'exemple de liste SharePoint ressemble à ceci.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-111">Here is what the sample SharePoint list looks like.</span></span> <span data-ttu-id="3a3d3-112">**Titre**, **Catégorie**, **Titre de notification**, **Message** et **URL** sont utilisés pour créer l’annonce.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-112">**Title**, **Category**, **NotificationTitle**, **Message** and **URL** are used for creating the announcement.</span></span> <span data-ttu-id="3a3d3-113">Une colonne appelée **IsProcessed** est utilisée par l’exemple de processus d’automatisation sous la forme d’un programme de console.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-113">There is a column called **IsProcessed** which is used by the sample automation process in the form of a console program.</span></span> <span data-ttu-id="3a3d3-114">Vous pouvez exécuter ce programme de console comme un WebJob Azure de façon à le planifier. Vous pouvez également utiliser directement le flux de travail SharePoint pour programmer la création et l'activation de l'annonce lorsqu'un élément est inséré dans la liste SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-114">You can either run this console program as an Azure WebJob so that you can schedule it or you can directly use the SharePoint workflow to program creating and activating the announcement when an item is inserted into the SharePoint list.</span></span> <span data-ttu-id="3a3d3-115">Dans cet exemple, nous utilisons le programme de console qui parcourt les éléments de la liste SharePoint et crée une annonce dans Azure Mobile Engagement pour chacun d’eux avant de définir l’indicateur **IsProcessed** sur true lors de la réussite de la création de l’annonce.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-115">In this sample we use the console program which goes through the items in the SharePoint list and create announcement in Azure Mobile Engagement for each of them and then finally marks the **IsProcessed** flag to be true on successful announcement creation.</span></span>
   
    ![][1]
2. <span data-ttu-id="3a3d3-116">Nous utilisons le code de l'exemple *Authentification à distance dans SharePoint Online à l’aide du modèle objet client* [ici](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) pour s'authentifier avec la liste SharePoint.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-116">We are using the code from the sample *Remote Authentication in SharePoint Online Using the Client Object Model* [here](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) to authenticate with the SharePoint list.</span></span>
3. <span data-ttu-id="3a3d3-117">Une fois authentifiés, nous parcourons les éléments de la liste pour trouver les éléments nouvellement créés (pour lesquels **IsProcessed** = false).</span><span class="sxs-lookup"><span data-stu-id="3a3d3-117">Once authenticated, we loop through the list items to find out any newly created items (which will have **IsProcessed** = false).</span></span> 
   
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
   
                // Load the SharePoint list
                clientContext.Load(list);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
   
                // Loop through the list to go through all the items which are newly added
                foreach (ListItem item in items)
                    if (item["IsProcessed"].ToString() != "Yes")
                    {
                        string name = item["Title"].ToString();
                        string notificationTitle = item["NotificationTitle"].ToString();
                        string notificationMessage = item["Message"].ToString();
                        string category = item["Category"].ToString();
                        string actionURL = ((FieldUrlValue)item["URL"]).Url;
   
                        // Send an HTTP request to create AzME campaign
                        int campaignId = CreateAzMECampaign
                            (name, notificationTitle, notificationMessage, category, actionURL).Result;
   
                        if (campaignId != -1)
                        {
                            // If creating campaign is successful then set this to true
                            item["IsProcessed"] = "Yes";
   
                            // Now try to activate the campaign also
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

## <a name="mobile-engagement-integration"></a><span data-ttu-id="3a3d3-118">Intégration à Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="3a3d3-118">Mobile Engagement integration</span></span>
1. <span data-ttu-id="3a3d3-119">Lorsque nous trouvons un élément qui nécessite un traitement, nous extrayons les informations requises pour créer une annonce à partir de l'élément de liste et nous appelons `CreateAzMECampaign` pour le créer, puis `ActivateAzMECampaign` pour l'activer.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-119">Once we find an item which requires processing - we extract the information required to create an announcement from the list item and call `CreateAzMECampaign` to create it and subsequently `ActivateAzMECampaign` to activate it.</span></span> <span data-ttu-id="3a3d3-120">Il s'agit essentiellement d’appels d'API REST vers le serveur principal de Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-120">These are essentially REST API calls calling to the Mobile Engagement backend.</span></span> 
2. <span data-ttu-id="3a3d3-121">Les API REST Mobile Engagement requièrent un **en-tête d’autorisation HTTP de schéma d’authentification de base** composé des éléments `ApplicationId` et `ApiKey` obtenus à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-121">The Mobile Engagement REST APIs require a **Basic auth scheme authorization HTTP header** which is composed of the `ApplicationId` and the `ApiKey` which you get from the Azure portal.</span></span> <span data-ttu-id="3a3d3-122">Assurez-vous d’utiliser la clé de la section **clés api** et *non* celle de la section **clés sdk**.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-122">Make sure that you are using the Key from the **api keys** section and *not* from the **sdk keys** section.</span></span> 
   
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
3. <span data-ttu-id="3a3d3-123">Pour créer la campagne d’annonces, reportez-vous à la [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span><span class="sxs-lookup"><span data-stu-id="3a3d3-123">For creating the announcement type campaign - refer to the [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span></span> <span data-ttu-id="3a3d3-124">Vous devez vous assurer de spécifier la campagne `kind` comme *annonce* et [charge](https://msdn.microsoft.com/library/azure/mt683751.aspx) et de la passer comme FormUrlEncodedContent.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-124">You need to make sure that you are specifying the campaign `kind` as *announcement* and the [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) and passing it as FormUrlEncodedContent.</span></span> 
   
        static async Task<int> CreateAzMECampaign(string campaignName, string notificationTitle, 
            string notificationMessage, string notificationCategory, string actionURL)
        {
            string createURIFragment = "/reach/1/create";
   
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                // Create the payload to send the content
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
   
                // Send the POST request
                var response = await client.PostAsync(url + createURIFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                int campaignId = -1;
                if (response.StatusCode.ToString() == "OK")
                {
                    // This is the campaign id
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
4. <span data-ttu-id="3a3d3-125">Une fois l'annonce créée, vous devriez voir apparaître une chose similaire sur le portail Mobile Engagement (notez que State=Draft et Activated = N/A).</span><span class="sxs-lookup"><span data-stu-id="3a3d3-125">Once you have the announcement created, you will see something like the following on the Mobile Engagement portal (note that the State=Draft and Activated = N/A)</span></span>
   
    ![][3]
5. <span data-ttu-id="3a3d3-126">`CreateAzMECampaign` crée une campagne d’annonces et retourne son ID à l'appelant.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-126">`CreateAzMECampaign` creates an announcement campaign and returns its Id to the caller.</span></span> <span data-ttu-id="3a3d3-127">`ActivateAzMECampaign` requiert cet ID comme paramètre pour activer la campagne.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-127">`ActivateAzMECampaign` requires this Id as the parameter to activate the campaign.</span></span> 
   
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
   
                // Send the POST request
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
6. <span data-ttu-id="3a3d3-128">Une fois l'annonce activée, vous devriez voir apparaître une chose similaire sur le portail Mobile Engagement :</span><span class="sxs-lookup"><span data-stu-id="3a3d3-128">Once you have the announcement activated, you will see something like the following on the Mobile Engagement portal:</span></span>
   
    ![][4]
7. <span data-ttu-id="3a3d3-129">Dès que la campagne est activée, tous les appareils répondant aux critères de la campagne reçoivent des notifications.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-129">As soon as the campaign gets activated, any devices which satisfy the criterion on the campaign will start seeing notifications.</span></span> 
8. <span data-ttu-id="3a3d3-130">Vous remarquerez également que l'élément de liste marqué avec IsProcessed = false reçoit la valeur True une fois la campagne d'annonce créée.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-130">You will also notice that the list item marked with IsProcessed = false has been set to True once the announcement campaign is created.</span></span>  

<span data-ttu-id="3a3d3-131">Cet exemple permet de créer une campagne d’annonces simple en spécifiant principalement les propriétés obligatoires.</span><span class="sxs-lookup"><span data-stu-id="3a3d3-131">This sample created a simple announcement campaign specifying mostly the required properties.</span></span> <span data-ttu-id="3a3d3-132">Vous pouvez la personnaliser à votre guise à partir du portail en utilisant les informations indiquées [ici](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span><span class="sxs-lookup"><span data-stu-id="3a3d3-132">You can customize this as much as you can from the portal by using the information [here](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span></span> 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png



