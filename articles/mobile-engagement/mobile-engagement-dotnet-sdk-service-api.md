---
title: "aaaUsing tooaccess du Kit de développement .NET API de Service Azure Mobile Engagement"
description: "Décrit comment toouse hello tooaccess du Kit de développement .NET Mobile Engagement API des services Azure Mobile Engagement"
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
ms.openlocfilehash: 812be6f507b29f7b2de6454e06face8082c2d161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-sdk-tooaccess-azure-mobile-engagement-service-apis"></a>À l’aide du Kit de développement .NET tooaccess API des services Azure Mobile Engagement
Azure Mobile Engagement expose un ensemble d’API pour vous les appareils toomanage, portée/envoyer des campagnes toointeract etc. avec ces API, nous vous fournissent également un [fichier Swagger](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) toogenerate kits de développement logiciel de votre choix des outils que vous pouvez utiliser avec langage. Nous vous recommandons d’utiliser des hello [AutoRest](https://github.com/Azure/AutoRest) outil toogenerate votre Kit de développement logiciel à partir de notre fichier Swagger.

> [!NOTE]
> Hello Azure Mobile Engagement service mars 2018 est retirée et est actuellement que les clients tooexisting disponibles. Pour plus d’informations, consultez [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Nous avons créé un kit de développement .NET de la même manière qui vous permet de toointeract avec ces API à l’aide d’un wrapper c#, et vous n’avez toodo hello négociation du jeton d’authentification et d’actualiser vous-même.  

Cet exemple passe dans le jeu hello d’étapes toofollow toouse hello .NET SDK :

1. Tout d’abord, vous avez besoin d’authentification de toosetup hello pour votre API à l’aide de hello Azure Active Directory comme décrit [ici](mobile-engagement-api-authentication.md#authentication). Extrémité hello de ces étapes, vous devez avoir valide **SubscriptionId**, **TenantId**, **ApplicationId** et **Secret**. 
2. Nous allons utiliser une simple toodemonstrate d’application Console Windows fonctionne avec hello SDK .NET avec le scénario de création d’une campagne annonce hello. Donc, ouvrez Visual Studio et créez une **application console**.   
3. Ensuite, vous devez le hello toodownload .NET SDK, disponible en tant que **bibliothèque de gestion Microsoft Azure Engagement** dans la galerie Nuget de hello [ici](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).
   Si vous installez hello Nuget à partir de Visual Studio, vous devez tooensure que vous avez activé hello **inclure la version préliminaire** option lors de la recherche pour le package de hello :
   
    ![][1]
4. Bonjour `Program.cs` , ajoutez hello suivant des espaces de noms :
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. Ensuite, vous devez toodefine hello suivant les constantes que nous allons utiliser pour l’authentification et interagir avec l’application d’Engagement Mobile hello dans lequel vous créez une campagne d’annonce hello :
   
        // For authentication
        const string TENANT_ID = "<Your TenantId>";
        const string CLIENT_ID = "<Your Application Id>";
        const string CLIENT_SECRET = "<Your Secret>";
        const string SUBSCRIPTION_ID = "<Your Subscription Id>";
   
        // This is hello Azure Resource group concept for grouping together resources 
        //  see here: https://azure.microsoft.com/en-us/documentation/articles/resource-group-portal/
        const string RESOURCE_GROUP = "";
   
        // For Mobile Engagement operations
        // App Collection Name 
        const string APP_COLLECTION_NAME = "";
        // Application Resource Name - make sure you are using hello one as specified in hello Azure portal (NOT hello App Name)
        const string APP_RESOURCE_NAME = "";
6. Définir hello `EngagementManagementClient` variable que nous utiliserons méthodes de kit de développement logiciel de Mobile Engagement hello toocall :
   
        static EngagementManagementClient engagementClient; 
7. Ajouter hello suivant tooyour `Main` méthode :
   
        try
            {
                // Initialize hello Engagement SDK toocall out APIs. 
                InitEngagementClient().Wait();
   
                // Create a Reach campaign
                CreateCampaign().Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.InnerException.Message);
                throw ex;
            }
8. Définir hello suivant de méthode qui prend en charge l’initialisation hello `EngagementManagementClient` par tout d’abord l’authentification et en l’associant elle-même avec l’application d’Engagement Mobile hello dans lequel vous envisagez de campagne d’annonce toocreate hello :
   
        private static async Task InitEngagementClient()
        {
            var credentials = await ApplicationTokenProvider.LoginSilentAsync(TENANT_ID, CLIENT_ID, CLIENT_SECRET);
            engagementClient = new EngagementManagementClient(credentials) { SubscriptionId = SUBSCRIPTION_ID };
   
            // This is hello Azure concept of ResourceGroup
            engagementClient.ResourceGroupName = RESOURCE_GROUP;
   
            // This is your Mobile Engagement App Collection & App Resource Name in which you create hello campaign
            engagementClient.AppCollection = APP_COLLECTION_NAME;
            engagementClient.AppName = APP_RESOURCE_NAME;
        }
   
   > [!IMPORTANT]
   > Notez que vous devez toouse hello **nom de la ressource application** tel que défini dans le portail de gestion Azure hello pour le paramètre de AppName hello. 
   > 
   > 
9. Enfin, définissez méthode hello CreateCampaign s’occupe de l’utilisation de hello précédemment initialisé EngagementClient toocreate simple **à tout moment** & **Notification uniquement** campagne avec un titre et le message : 
   
        private async static Task CreateCampaign()
        {
            //  Refer toohello Announcement Campaign format from here - 
            //      https://msdn.microsoft.com/en-us/library/azure/mt683751.aspx
            // Make sure you are passing all hello non-optional parameters
            Campaign parameters = new Campaign(
                name:"WelcomeCampaign",
                notificationTitle: "Welcome", 
                notificationMessage: "Thank you for installing hello app!",
                type:"only_notif",
                deliveryTime:"any"
                );
   
            // Refer toohello Campaign Kinds from here - https://msdn.microsoft.com/en-us/library/azure/mt683742.aspx
            CampaignStateResult result = 
                await engagementClient.Campaigns.CreateAsync(CampaignKinds.Announcements, parameters);
            Console.WriteLine("Campaign Id '{0}' was created successfully and it is in '{1}' state", result.Id, result.State);
        }
10. Application de console hello d’exécution et que vous découvrez hello sur la création réussie de la campagne de hello :
    
    **Campaign Id '159' was created successfully and it is in 'draft' state**

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png
