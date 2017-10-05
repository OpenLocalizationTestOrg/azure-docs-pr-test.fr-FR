---
title: "Configurer l’authentification et l’autorisation pour une application personnalisée qui appelle l’API Insights Azure Time Series | Microsoft Docs"
description: "Ce didacticiel explique comment configurer l’authentification et l’autorisation pour une application personnalisée qui appelle l’API Insights Azure Time Series"
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 4dd4865dc556e09a31d2cb7a32768aeb19ba9900
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a><span data-ttu-id="9e315-103">Authentification et autorisation pour l’API Insights Azure Time Series</span><span class="sxs-lookup"><span data-stu-id="9e315-103">Authentication and authorization for Azure Time Series Insights API</span></span>

<span data-ttu-id="9e315-104">Cet article explique comment configurer une application personnalisée qui appelle l’API Insights Azure Tuime Series.</span><span class="sxs-lookup"><span data-stu-id="9e315-104">This article explains how to configure a custom application that calls the Azure Time Series Insights API.</span></span>

## <a name="service-principal"></a><span data-ttu-id="9e315-105">Principal du service</span><span class="sxs-lookup"><span data-stu-id="9e315-105">Service principal</span></span>

<span data-ttu-id="9e315-106">Cette section explique comment configurer une application pour accéder à l’API Insights Azure Time Series pour le compte de l’application.</span><span class="sxs-lookup"><span data-stu-id="9e315-106">This section explains how to configure an application to access the Time Series Insights API on behalf of the application.</span></span> <span data-ttu-id="9e315-107">L’application peut ensuite interroger des données ou publier des données de référence dans l’environnement Time Series Insights avec les informations d’identification de l’application au lieu de celles de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9e315-107">The application can then query data or publish reference data in the Time Series Insights environment with application credentials and not the user credentials.</span></span>

<span data-ttu-id="9e315-108">Lorsque vous avez une application qui doit accéder à Time Series Insights, vous devez configurer une application Azure Active Directory et affecter des stratégies d’accès aux données dans l’environnement Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="9e315-108">When you have an application that needs to access Time Series Insights, you must set up an Azure Active Directory application and assign the data access policies in the Time Series Insights environment.</span></span> <span data-ttu-id="9e315-109">Cette approche est préférable à l’exécution de l’application avec vos propres informations d’identification, car :</span><span class="sxs-lookup"><span data-stu-id="9e315-109">This approach is preferable to running the app under your own credentials because:</span></span>

* <span data-ttu-id="9e315-110">Vous pouvez assigner à l’identité de l’application des autorisations différentes de vos propres autorisations.</span><span class="sxs-lookup"><span data-stu-id="9e315-110">You can assign permissions to the app identity that are different from your own permissions.</span></span> <span data-ttu-id="9e315-111">En règle générale, ces autorisations sont strictement limitées à ce que l’application doit faire.</span><span class="sxs-lookup"><span data-stu-id="9e315-111">Typically, these permissions are restricted to exactly what the app needs to do.</span></span> <span data-ttu-id="9e315-112">Par exemple, vous pouvez autoriser l’application à lire des données uniquement dans un environnement Time Series Insights particulier.</span><span class="sxs-lookup"><span data-stu-id="9e315-112">For example, you can allow the app to only read data in a particular Time Series Insights environment.</span></span>
* <span data-ttu-id="9e315-113">Il est inutile de modifier les informations d’identification de l’application si vos responsabilités évoluent.</span><span class="sxs-lookup"><span data-stu-id="9e315-113">You don't have to change the app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="9e315-114">Vous pouvez utiliser un certificat ou une clé d’application pour automatiser l’authentification lorsque vous exécutez un script sans assistance.</span><span class="sxs-lookup"><span data-stu-id="9e315-114">You can use a certificate or an application key to automate authentication when you're running an unattended script.</span></span>

<span data-ttu-id="9e315-115">Cet article explique comment effectuer ces étapes via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9e315-115">This article shows you how to perform those steps through the Azure portal.</span></span> <span data-ttu-id="9e315-116">Elle se concentre sur une application à client unique conçue pour s’exécuter au sein d’une seule organisation.</span><span class="sxs-lookup"><span data-stu-id="9e315-116">It focuses on a single-tenant application where the application is intended to run in only one organization.</span></span> <span data-ttu-id="9e315-117">Les applications à client unique sont généralement utilisées pour des applications métier exécutées au sein de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="9e315-117">You typically use single-tenant applications for line-of-business applications that run in your organization.</span></span>

<span data-ttu-id="9e315-118">Le flux d’installation se compose de trois étapes principales :</span><span class="sxs-lookup"><span data-stu-id="9e315-118">The setup flow consists of three high-level steps:</span></span>

1. <span data-ttu-id="9e315-119">Créer une application dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9e315-119">Create an application in Azure Active Directory.</span></span>
2. <span data-ttu-id="9e315-120">Autoriser cette application à accéder à l’environnement Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="9e315-120">Authorize this application to access the Time Series Insights environment.</span></span>
3. <span data-ttu-id="9e315-121">Utiliser l’ID et la clé d’application pour acquérir un jeton pour l’audience ou ressource `"https://api.timeseries.azure.com/"`.</span><span class="sxs-lookup"><span data-stu-id="9e315-121">Use the application ID and key to acquire a token to the `"https://api.timeseries.azure.com/"` audience or resource.</span></span> <span data-ttu-id="9e315-122">Le jeton permet ensuite d’appeler l’API Insights Azure Time Series.</span><span class="sxs-lookup"><span data-stu-id="9e315-122">The token can then be used to call the Time Series Insights API.</span></span>

<span data-ttu-id="9e315-123">Voici les étapes détaillées :</span><span class="sxs-lookup"><span data-stu-id="9e315-123">Here are the detailed steps:</span></span>

1. <span data-ttu-id="9e315-124">Dans le portail Azure, sélectionnez **Azure Active Directory** > **Inscriptions des applications** > **Nouvelle inscription d’application**.</span><span class="sxs-lookup"><span data-stu-id="9e315-124">In the Azure portal, select **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

   ![Nouvelle inscription d’application dans Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. <span data-ttu-id="9e315-126">Donnez un nom à l’application, sélectionnez le type **Application web ou API**, sélectionnez un URI valide pour l’**URL de connexion**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="9e315-126">Give the application a name, select the type to be **Web app / API**, select any valid URI for **Sign-on URL**, and click **Create**.</span></span>

   ![Créer l’application dans Azure Active Directory](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. <span data-ttu-id="9e315-128">Sélectionnez votre application nouvellement créée, puis copiez son ID d’application dans votre éditeur de texte favori.</span><span class="sxs-lookup"><span data-stu-id="9e315-128">Select your newly created application and copy its application ID to your favorite text editor.</span></span>

   ![Copier l’ID de l’application](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. <span data-ttu-id="9e315-130">Sélectionnez **Clés**, entrez le nom de clé, sélectionnez la date d’expiration, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9e315-130">Select **Keys**, enter the key name, select the expiration, and click **Save**.</span></span>

   ![sélectionner des clés d’application](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Entrer le nom et la date d’expiration de la clé, puis cliquer sur Enregistrer](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. <span data-ttu-id="9e315-133">Copiez la clé dans votre éditeur de texte.</span><span class="sxs-lookup"><span data-stu-id="9e315-133">Copy the key to your favorite text editor.</span></span>

   ![Copier la clé de l’application](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. <span data-ttu-id="9e315-135">Pour l’environnement Time Series Insights, sélectionnez **Stratégies d’accès aux données**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9e315-135">For the Time Series Insights environment, select **Data Access Policies** and click **Add**.</span></span>

   ![Ajouter une nouvelle stratégie d’accès aux données à l’environnement Time Series Insights](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. <span data-ttu-id="9e315-137">Dans la boîte de dialogue **Sélectionner un utilisateur**, collez le nom de l’application (voir l’étape 2) ou l’ID de l’application (voir l’étape 3).</span><span class="sxs-lookup"><span data-stu-id="9e315-137">In the **Select User** dialog box, paste the application name (from step 2) or application ID (from step 3).</span></span>

   ![Rechercher une application dans la boîte de dialogue Sélectionner un utilisateur](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. <span data-ttu-id="9e315-139">Sélectionnez le rôle (**Lecteur** pour interroger des données, **Contributeur** pour interroger des données et modifier des données de référence), puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e315-139">Select the role (**Reader** for querying data, **Contributor** for querying data and changing reference data) and click **Ok**.</span></span>

   ![Choisir Lecteur ou Contributeur dans la boîte de dialogue Sélectionner un rôle](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. <span data-ttu-id="9e315-141">Enregistrer la stratégie en cliquant sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9e315-141">Save the policy by clicking **Ok**.</span></span>

10. <span data-ttu-id="9e315-142">Pour acquérir un jeton pour le compte de l’application, utilisez l’ID d’application (voir l’étape 3) et la clé de l’application (voir l’étape 5).</span><span class="sxs-lookup"><span data-stu-id="9e315-142">Use the application ID (from step 3) and application key (from step 5) to acquire the token on behalf of the application.</span></span> <span data-ttu-id="9e315-143">Le jeton peut ensuite être passé dans l’en-tête `Authorization` lorsque l’application appelle l’API Insights Azure Time Series.</span><span class="sxs-lookup"><span data-stu-id="9e315-143">The token can then be passed in the `Authorization` header when the application calls the Time Series Insights API.</span></span>

    <span data-ttu-id="9e315-144">Si vous utilisez C#, vous pouvez utiliser le code suivant pour acquérir le jeton pour le compte de l’application.</span><span class="sxs-lookup"><span data-stu-id="9e315-144">If you're using C#, you can use the following code to acquire the token on behalf of the application.</span></span> <span data-ttu-id="9e315-145">Pour obtenir un exemple complet, voir [Interroger des données à l’aide de C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="9e315-145">For a complete sample, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set the resource URI to the Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of the application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a><span data-ttu-id="9e315-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9e315-146">Next steps</span></span>

<span data-ttu-id="9e315-147">Utilisez l’ID et la clé de l’application dans votre application.</span><span class="sxs-lookup"><span data-stu-id="9e315-147">Use the application ID and key in your application.</span></span> <span data-ttu-id="9e315-148">Pour un exemple de code qui appelle l’API Time Series Insights, voir [Interroger des données à l’aide de C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="9e315-148">For sample code that calls the Time Series Insights API, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="9e315-149">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="9e315-149">See also</span></span>

* <span data-ttu-id="9e315-150">[API de requête](/rest/api/time-series-insights/time-series-insights-reference-queryapi) pour la référence d’API de requête complète</span><span class="sxs-lookup"><span data-stu-id="9e315-150">[Query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) for the full Query API reference</span></span>
* [<span data-ttu-id="9e315-151">Créer un principal du service dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="9e315-151">Create a service principal in the Azure portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
