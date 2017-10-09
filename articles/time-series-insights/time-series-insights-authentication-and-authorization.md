---
title: "aaaConfigure l’authentification et l’autorisation pour une application personnalisée qui appelle hello Azure temps série Insights API | Documents Microsoft"
description: "Ce didacticiel explique comment tooconfigure l’authentification et l’autorisation pour une application personnalisée qui appelle hello Azure temps série Insights API"
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
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a><span data-ttu-id="be5f1-103">Authentification et autorisation pour l’API Insights Azure Time Series</span><span class="sxs-lookup"><span data-stu-id="be5f1-103">Authentication and authorization for Azure Time Series Insights API</span></span>

<span data-ttu-id="be5f1-104">Cet article explique comment tooconfigure une application personnalisée qui appelle hello Azure temps série Insights API.</span><span class="sxs-lookup"><span data-stu-id="be5f1-104">This article explains how tooconfigure a custom application that calls hello Azure Time Series Insights API.</span></span>

## <a name="service-principal"></a><span data-ttu-id="be5f1-105">Principal du service</span><span class="sxs-lookup"><span data-stu-id="be5f1-105">Service principal</span></span>

<span data-ttu-id="be5f1-106">Cette section explique comment tooconfigure un tooaccess application hello temps série Insights API au nom de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="be5f1-106">This section explains how tooconfigure an application tooaccess hello Time Series Insights API on behalf of hello application.</span></span> <span data-ttu-id="be5f1-107">application Hello pouvez interroger les données ou publier les données de référence d’environnement d’heure série Insights hello avec les informations d’identification de l’application et les informations d’identification hello utilisateur pas.</span><span class="sxs-lookup"><span data-stu-id="be5f1-107">hello application can then query data or publish reference data in hello Time Series Insights environment with application credentials and not hello user credentials.</span></span>

<span data-ttu-id="be5f1-108">Lorsque vous avez une application qui doit tooaccess temps série Insights, vous devez configurer une application Azure Active Directory et affecter des stratégies d’accès données hello dans l’environnement de temps série Insights hello.</span><span class="sxs-lookup"><span data-stu-id="be5f1-108">When you have an application that needs tooaccess Time Series Insights, you must set up an Azure Active Directory application and assign hello data access policies in hello Time Series Insights environment.</span></span> <span data-ttu-id="be5f1-109">Cette approche est préférable toorunning hello application vos propres informations d’identification, car :</span><span class="sxs-lookup"><span data-stu-id="be5f1-109">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="be5f1-110">Vous pouvez affecter des autorisations identité d’application toohello différents de vos propres autorisations.</span><span class="sxs-lookup"><span data-stu-id="be5f1-110">You can assign permissions toohello app identity that are different from your own permissions.</span></span> <span data-ttu-id="be5f1-111">En règle générale, ces autorisations sont limitée tooexactly quelle application hello doit toodo.</span><span class="sxs-lookup"><span data-stu-id="be5f1-111">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span> <span data-ttu-id="be5f1-112">Par exemple, vous pouvez autoriser hello application tooonly lire les données dans un environnement de temps série Insights particulier.</span><span class="sxs-lookup"><span data-stu-id="be5f1-112">For example, you can allow hello app tooonly read data in a particular Time Series Insights environment.</span></span>
* <span data-ttu-id="be5f1-113">Vous n’avez les informations d’identification de l’application toochange hello si vos responsabilités changent.</span><span class="sxs-lookup"><span data-stu-id="be5f1-113">You don't have toochange hello app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="be5f1-114">Vous pouvez utiliser un certificat ou une authentification de clé tooautomate application lorsque vous exécutez un script sans assistance.</span><span class="sxs-lookup"><span data-stu-id="be5f1-114">You can use a certificate or an application key tooautomate authentication when you're running an unattended script.</span></span>

<span data-ttu-id="be5f1-115">Cet article explique comment tooperform celles parcourt hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="be5f1-115">This article shows you how tooperform those steps through hello Azure portal.</span></span> <span data-ttu-id="be5f1-116">Il se concentre sur une application à locataire unique où application hello est prévue toorun dans une seule organisation.</span><span class="sxs-lookup"><span data-stu-id="be5f1-116">It focuses on a single-tenant application where hello application is intended toorun in only one organization.</span></span> <span data-ttu-id="be5f1-117">Les applications à client unique sont généralement utilisées pour des applications métier exécutées au sein de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="be5f1-117">You typically use single-tenant applications for line-of-business applications that run in your organization.</span></span>

<span data-ttu-id="be5f1-118">flux de programme d’installation Hello se compose de trois étapes principales :</span><span class="sxs-lookup"><span data-stu-id="be5f1-118">hello setup flow consists of three high-level steps:</span></span>

1. <span data-ttu-id="be5f1-119">Créer une application dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="be5f1-119">Create an application in Azure Active Directory.</span></span>
2. <span data-ttu-id="be5f1-120">Autoriser cet environnement de temps série Insights application tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="be5f1-120">Authorize this application tooaccess hello Time Series Insights environment.</span></span>
3. <span data-ttu-id="be5f1-121">Utiliser les ID de l’application hello et clé tooacquire un jeton toohello `"https://api.timeseries.azure.com/"` audience ou une ressource.</span><span class="sxs-lookup"><span data-stu-id="be5f1-121">Use hello application ID and key tooacquire a token toohello `"https://api.timeseries.azure.com/"` audience or resource.</span></span> <span data-ttu-id="be5f1-122">jeton de Hello peut ensuite être utilisé toocall hello temps série Insights API.</span><span class="sxs-lookup"><span data-stu-id="be5f1-122">hello token can then be used toocall hello Time Series Insights API.</span></span>

<span data-ttu-id="be5f1-123">Voici les étapes détaillées de hello :</span><span class="sxs-lookup"><span data-stu-id="be5f1-123">Here are hello detailed steps:</span></span>

1. <span data-ttu-id="be5f1-124">Bonjour portail Azure, sélectionnez **Azure Active Directory** > **inscriptions d’application** > **nouvelle inscription de l’application**.</span><span class="sxs-lookup"><span data-stu-id="be5f1-124">In hello Azure portal, select **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

   ![Nouvelle inscription d’application dans Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. <span data-ttu-id="be5f1-126">Permettre à application hello un toobe de type hello nom, sélectionnez **application Web / API**, sélectionnez n’importe quel URI valide pour **URL de connexion**, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="be5f1-126">Give hello application a name, select hello type toobe **Web app / API**, select any valid URI for **Sign-on URL**, and click **Create**.</span></span>

   ![Créer l’application hello dans Azure Active Directory](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. <span data-ttu-id="be5f1-128">Sélectionnez votre application nouvellement créée et copiez son éditeur de texte favori application ID tooyour.</span><span class="sxs-lookup"><span data-stu-id="be5f1-128">Select your newly created application and copy its application ID tooyour favorite text editor.</span></span>

   ![Copiez l’ID de l’application hello](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. <span data-ttu-id="be5f1-130">Sélectionnez **clés**, entrez le nom de clé hello, d’expiration hello sélectionnez, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="be5f1-130">Select **Keys**, enter hello key name, select hello expiration, and click **Save**.</span></span>

   ![sélectionner des clés d’application](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Entrez l’expiration et le nom de la clé hello et cliquez sur Enregistrer](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. <span data-ttu-id="be5f1-133">Éditeur de texte hello tooyour clé copie.</span><span class="sxs-lookup"><span data-stu-id="be5f1-133">Copy hello key tooyour favorite text editor.</span></span>

   ![Copiez la clé de l’application hello](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. <span data-ttu-id="be5f1-135">Pour un environnement de temps série Insights hello, sélectionnez **des stratégies d’accès données** et cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="be5f1-135">For hello Time Series Insights environment, select **Data Access Policies** and click **Add**.</span></span>

   ![Ajouter nouveau données accès stratégie toohello temps série Insights environnement](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. <span data-ttu-id="be5f1-137">Bonjour **sélectionner un utilisateur** boîte de dialogue, nom de l’application hello Coller (de l’étape 2) ou ID de l’application (à l’étape 3).</span><span class="sxs-lookup"><span data-stu-id="be5f1-137">In hello **Select User** dialog box, paste hello application name (from step 2) or application ID (from step 3).</span></span>

   ![Rechercher une application dans la boîte de dialogue Sélectionner un utilisateur hello](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. <span data-ttu-id="be5f1-139">Rôle de hello Select (**lecteur** pour interroger des données, **collaborateur** pour l’interrogation de données et la modification des données de référence) et cliquez sur **Ok**.</span><span class="sxs-lookup"><span data-stu-id="be5f1-139">Select hello role (**Reader** for querying data, **Contributor** for querying data and changing reference data) and click **Ok**.</span></span>

   ![Choisir le lecteur ou contributeur dans la boîte de dialogue Sélectionner un rôle hello](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. <span data-ttu-id="be5f1-141">Enregistrer la stratégie de hello en cliquant sur **Ok**.</span><span class="sxs-lookup"><span data-stu-id="be5f1-141">Save hello policy by clicking **Ok**.</span></span>

10. <span data-ttu-id="be5f1-142">Utiliser l’ID d’application hello (à l’étape 3) et jeton de hello application tooacquire clé (à l’étape 5) au nom de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="be5f1-142">Use hello application ID (from step 3) and application key (from step 5) tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="be5f1-143">Hello jeton peut ensuite être transmis dans hello `Authorization` en-tête lors de l’application hello appelle hello temps série Insights API.</span><span class="sxs-lookup"><span data-stu-id="be5f1-143">hello token can then be passed in hello `Authorization` header when hello application calls hello Time Series Insights API.</span></span>

    <span data-ttu-id="be5f1-144">Si vous utilisez c#, vous pouvez utiliser hello suivant le jeton de hello tooacquire de code pour le compte d’application hello.</span><span class="sxs-lookup"><span data-stu-id="be5f1-144">If you're using C#, you can use hello following code tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="be5f1-145">Pour obtenir un exemple complet, voir [Interroger des données à l’aide de C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="be5f1-145">For a complete sample, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a><span data-ttu-id="be5f1-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="be5f1-146">Next steps</span></span>

<span data-ttu-id="be5f1-147">Utiliser l’ID de l’application hello et la clé dans votre application.</span><span class="sxs-lookup"><span data-stu-id="be5f1-147">Use hello application ID and key in your application.</span></span> <span data-ttu-id="be5f1-148">Pour un exemple de code qui appelle hello temps série Insights API, consultez [interroger des données à l’aide de C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="be5f1-148">For sample code that calls hello Time Series Insights API, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="be5f1-149">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="be5f1-149">See also</span></span>

* <span data-ttu-id="be5f1-150">[API de requête](/rest/api/time-series-insights/time-series-insights-reference-queryapi) pour la référence complète de l’API de requête de hello</span><span class="sxs-lookup"><span data-stu-id="be5f1-150">[Query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) for hello full Query API reference</span></span>
* [<span data-ttu-id="be5f1-151">Créer un service principal Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="be5f1-151">Create a service principal in hello Azure portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
