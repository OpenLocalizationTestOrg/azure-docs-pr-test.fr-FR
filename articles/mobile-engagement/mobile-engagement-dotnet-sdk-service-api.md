---
title: "Utilisation du Kit de développement logiciel (SDK) .NET pour accéder aux API du service Azure Mobile Engagement"
description: "Décrit comment utiliser le Kit de développement logiciel (SDK) .NET Mobile Engagement pour accéder aux API du service Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: c07728aa-43f2-4238-8b4a-c9eddf9d838b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 6a497189268c5a1b7e269cc57904ebc77c1906fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="using-net-sdk-to-access-azure-mobile-engagement-service-apis"></a><span data-ttu-id="42710-103">Utilisation du Kit de développement logiciel (SDK) .NET pour accéder aux API du service Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="42710-103">Using .NET SDK to access Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="42710-104">Azure Mobile Engagement expose un ensemble d’API pour vous permettre de gérer des appareils, des campagnes Push/Reach, etc. Pour interagir avec ces API, nous vous fournissons également un [fichier Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) que vous pouvez utiliser avec des outils pour générer des SDK pour votre langue par défaut.</span><span class="sxs-lookup"><span data-stu-id="42710-104">Azure Mobile Engagement exposes a set of APIs for you to manage Devices, Reach/Push campaigns etc. To interact with these APIs, we also provide you a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools to generate SDKs for your preferred language.</span></span> <span data-ttu-id="42710-105">Nous vous recommandons d’utiliser l’outil [AutoRest](https://github.com/Azure/AutoRest)pour générer votre SDK à partir de notre fichier Swagger.</span><span class="sxs-lookup"><span data-stu-id="42710-105">We recommend using the [AutoRest](https://github.com/Azure/AutoRest) tool to generate your SDK from our Swagger file.</span></span>

> [!NOTE]
> <span data-ttu-id="42710-106">Le service Azure Mobile Engagement ne sera plus disponible à partir de mars 2018. Actuellement, il reste uniquement disponible pour les clients déjà abonnés à ce service.</span><span class="sxs-lookup"><span data-stu-id="42710-106">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="42710-107">Pour plus d’informations, consultez [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="42710-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="42710-108">Nous avons créé un Kit de développement logiciel (SDK) .NET de la même manière qui vous permet d’interagir avec ces API à l’aide d’un wrapper C#. Vous n’êtes pas obligé d’effectuer la négociation de jeton d'authentification et l’actualisation vous-même.</span><span class="sxs-lookup"><span data-stu-id="42710-108">We have created a .NET SDK in a similar manner which allows you to interact with these APIs using a C# wrapper and you don't have to do the authentication token negotiation and refresh yourself.</span></span>  

<span data-ttu-id="42710-109">Cet exemple parcourt l’ensemble des étapes à suivre pour utiliser le Kit de développement logiciel (SDK) .NET :</span><span class="sxs-lookup"><span data-stu-id="42710-109">This sample goes through the set of steps to follow to use the .NET SDK:</span></span>

1. <span data-ttu-id="42710-110">Tout d’abord, vous devez configurer l’authentification pour vos API à l’aide d’Azure Active Directory, comme décrit [ici](mobile-engagement-api-authentication.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="42710-110">First of all, you need to setup the authentication for your APIs using the Azure Active Directory as described [here](mobile-engagement-api-authentication.md#authentication).</span></span> <span data-ttu-id="42710-111">À la fin de ces étapes, vous devriez avoir des valeurs **SubscriptionId**, **TenantId**, **ApplicationId** et **Secret** valides.</span><span class="sxs-lookup"><span data-stu-id="42710-111">At the end of these steps, you should have a valid **SubscriptionId**, **TenantId**, **ApplicationId** and **Secret**.</span></span> 
2. <span data-ttu-id="42710-112">Nous allons utiliser une application console Windows simple pour illustrer l’utilisation du Kit de développement logiciel (SDK) .NET avec le scénario de création d’une campagne d’annonces.</span><span class="sxs-lookup"><span data-stu-id="42710-112">We will use a simple Windows Console app to demonstrate working with the .NET SDK with the scenario of creating an Announcement campaign.</span></span> <span data-ttu-id="42710-113">Donc, ouvrez Visual Studio et créez une **application console**.</span><span class="sxs-lookup"><span data-stu-id="42710-113">So open up Visual Studio and create a **Console Application**.</span></span>   
3. <span data-ttu-id="42710-114">Ensuite, vous devez télécharger le Kit de développement logiciel (SDK) .NET disponible en tant que **Bibliothèque de gestion Microsoft Azure Engagement** dans la galerie Nuget [ici](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span><span class="sxs-lookup"><span data-stu-id="42710-114">Next you need to download the .NET SDK which is available as **Microsoft Azure Engagement Management Library** in the Nuget gallery [here](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span></span>
   <span data-ttu-id="42710-115">Si vous installez Nuget à partir de Visual Studio, vous devez vous assurer que l’option **Inclure la version préliminaire** est activée lors de la recherche du package :</span><span class="sxs-lookup"><span data-stu-id="42710-115">If you are installing the Nuget from Visual Studio, you need to ensure that you have check marked the **Include prerelease** option while searching for the package:</span></span>
   
    ![][1]
4. <span data-ttu-id="42710-116">Dans le fichier `Program.cs` , ajoutez les espaces de noms suivants :</span><span class="sxs-lookup"><span data-stu-id="42710-116">In the `Program.cs` file, add the following namespaces:</span></span>
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. <span data-ttu-id="42710-117">Ensuite, vous devez définir les constantes suivantes que nous utiliserons pour l’authentification et l’interaction avec l’application Mobile Engagement dans laquelle vous créez la campagne d’annonces :</span><span class="sxs-lookup"><span data-stu-id="42710-117">Next you need to define the following constants that we will use for authentication and interacting with the Mobile Engagement App in which you are creating the Announcement campaign:</span></span>
   
        // For authentication
        const string TENANT_ID = "<Your TenantId>";
        const string CLIENT_ID = "<Your Application Id>";
        const string CLIENT_SECRET = "<Your Secret>";
        const string SUBSCRIPTION_ID = "<Your Subscription Id>";
   
        // This is the Azure Resource group concept for grouping together resources 
        //  see here: https://azure.microsoft.com/en-us/documentation/articles/resource-group-portal/
        const string RESOURCE_GROUP = "";
   
        // For Mobile Engagement operations
        // App Collection Name 
        const string APP_COLLECTION_NAME = "";
        // Application Resource Name - make sure you are using the one as specified in the Azure portal (NOT the App Name)
        const string APP_RESOURCE_NAME = "";
6. <span data-ttu-id="42710-118">Définissez la variable `EngagementManagementClient` que nous utiliserons pour appeler les méthodes du Kit de développement logiciel (SDK) Mobile Engagement :</span><span class="sxs-lookup"><span data-stu-id="42710-118">Define the `EngagementManagementClient` variable which we will use to call the Mobile Engagement SDK methods:</span></span>
   
        static EngagementManagementClient engagementClient; 
7. <span data-ttu-id="42710-119">Ajoutez ce qui suit dans votre méthode `Main` :</span><span class="sxs-lookup"><span data-stu-id="42710-119">Add the following to your `Main` method:</span></span>
   
        try
            {
                // Initialize the Engagement SDK to call out APIs. 
                InitEngagementClient().Wait();
   
                // Create a Reach campaign
                CreateCampaign().Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.InnerException.Message);
                throw ex;
            }
8. <span data-ttu-id="42710-120">Définissez la méthode suivante qui prend en charge l’initialisation de `EngagementManagementClient` en s’authentifiant et s’associant avec l’application Mobile Engagement, dans laquelle vous envisagez de créer la campagne d’annonces :</span><span class="sxs-lookup"><span data-stu-id="42710-120">Define the following method which takes care of initializing the `EngagementManagementClient` by first authenticating and then associating itself with the Mobile Engagement App in which you plan to create the Announcement campaign:</span></span>
   
        private static async Task InitEngagementClient()
        {
            var credentials = await ApplicationTokenProvider.LoginSilentAsync(TENANT_ID, CLIENT_ID, CLIENT_SECRET);
            engagementClient = new EngagementManagementClient(credentials) { SubscriptionId = SUBSCRIPTION_ID };
   
            // This is the Azure concept of ResourceGroup
            engagementClient.ResourceGroupName = RESOURCE_GROUP;
   
            // This is your Mobile Engagement App Collection & App Resource Name in which you create the campaign
            engagementClient.AppCollection = APP_COLLECTION_NAME;
            engagementClient.AppName = APP_RESOURCE_NAME;
        }
   
   > [!IMPORTANT]
   > <span data-ttu-id="42710-121">Notez que vous devez utiliser le **nom de la ressource d’application** tel que défini dans le portail de gestion Azure pour le paramètre AppName.</span><span class="sxs-lookup"><span data-stu-id="42710-121">Note that you need to use the **App Resource Name** as defined in the Azure management portal for the AppName parameter.</span></span> 
   > 
   > 
9. <span data-ttu-id="42710-122">Enfin, définissez la méthode CreateCampaign qui se charge de l’utilisation du client EngagementClient initialisé pour créer une campagne **AnyTime** & **Notification-only** simple avec un titre et un message :</span><span class="sxs-lookup"><span data-stu-id="42710-122">Lastly, define the CreateCampaign method which will take care of using the previously initialized EngagementClient to create a simple **AnyTime** & **Notification-only** campaign with a title and message:</span></span> 
   
        private async static Task CreateCampaign()
        {
            //  Refer to the Announcement Campaign format from here - 
            //      https://msdn.microsoft.com/en-us/library/azure/mt683751.aspx
            // Make sure you are passing all the non-optional parameters
            Campaign parameters = new Campaign(
                name:"WelcomeCampaign",
                notificationTitle: "Welcome", 
                notificationMessage: "Thank you for installing the app!",
                type:"only_notif",
                deliveryTime:"any"
                );
   
            // Refer to the Campaign Kinds from here - https://msdn.microsoft.com/en-us/library/azure/mt683742.aspx
            CampaignStateResult result = 
                await engagementClient.Campaigns.CreateAsync(CampaignKinds.Announcements, parameters);
            Console.WriteLine("Campaign Id '{0}' was created successfully and it is in '{1}' state", result.Id, result.State);
        }
10. <span data-ttu-id="42710-123">Exécutez l’application console. Les éléments suivants doivent s’afficher lors de la création réussie de la campagne :</span><span class="sxs-lookup"><span data-stu-id="42710-123">Run the console app and you will see the following on successful creation of the campaign:</span></span>
    
    <span data-ttu-id="42710-124">**Campaign Id '159' was created successfully and it is in 'draft' state**</span><span class="sxs-lookup"><span data-stu-id="42710-124">**Campaign Id '159' was created successfully and it is in 'draft' state**</span></span>

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
