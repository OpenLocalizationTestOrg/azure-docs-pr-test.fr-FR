---
title: "Déployer, appeler et authentifier des API web et REST pour Azure Logic Apps | Microsoft Docs"
description: "Déployer, authentifier et appeler des API web et REST dans les flux de travail d’intégration système avec Azure Logic Apps"
keywords: "API web, API REST, connecteurs, flux de travail, intégration système, authentifier"
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 88c62d5ab046d8cf4bce5d23b776e517bb0e1d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="e091d-104">Déployer, appeler et authentifier des API personnalisées en tant que connecteurs pour les applications logiques</span><span class="sxs-lookup"><span data-stu-id="e091d-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="e091d-105">Après avoir [créé des API personnalisées](./logic-apps-create-api-app.md) qui fournissent des actions ou des déclencheurs à utiliser dans les flux de travail d’application logique, vous devez déployer vos API avant de pouvoir les appeler.</span><span class="sxs-lookup"><span data-stu-id="e091d-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers to use in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="e091d-106">Même si vous pouvez appeler n’importe quelle API à partir d’une application logique, vous bénéficierez d’une expérience optimale si vous ajoutez des [métadonnées Swagger](http://swagger.io/specification/) décrivant les opérations et paramètres de votre API.</span><span class="sxs-lookup"><span data-stu-id="e091d-106">And although you can call any API from a logic app, for the best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="e091d-107">Ce fichier Swagger améliore le fonctionnent de votre API et simplifie son intégration aux applications logiques.</span><span class="sxs-lookup"><span data-stu-id="e091d-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="e091d-108">Vous pouvez déployer vos API en tant [qu’applications web](../app-service-web/app-service-web-overview.md). Cependant, envisagez de les déployer en tant [qu’applications API](../app-service-api/app-service-api-apps-why-best-platform.md) pour simplifier votre travail lorsque vous générez, hébergez et consommez des API dans le cloud et en local.</span><span class="sxs-lookup"><span data-stu-id="e091d-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in the cloud and on premises.</span></span> <span data-ttu-id="e091d-109">Vous n’êtes pas obligé de modifier le code dans vos API. Il vous suffit de déployer votre code dans une application API.</span><span class="sxs-lookup"><span data-stu-id="e091d-109">You don't have to change any code in your APIs -- just deploy your code to an API app.</span></span> <span data-ttu-id="e091d-110">Vous pouvez héberger vos API sur [Azure App Service](../app-service/app-service-value-prop-what-is.md), une offre PaaS (Platform-as-a-Service) qui fournit l’une des méthodes les plus efficaces, les plus simples et les plus évolutives pour héberger des API.</span><span class="sxs-lookup"><span data-stu-id="e091d-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of the best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="e091d-111">Pour authentifier des appels à partir d’applications logiques vers vos API, vous pouvez configurer Azure Active Directory dans le Portail Azure, ce qui vous évite de mettre à jour votre code.</span><span class="sxs-lookup"><span data-stu-id="e091d-111">To authenticate calls from logic apps to your APIs, you can set up Azure Active Directory in the Azure portal so you don't have to update your code.</span></span> <span data-ttu-id="e091d-112">Vous pouvez également exiger et appliquer une authentification par le biais du code de votre API.</span><span class="sxs-lookup"><span data-stu-id="e091d-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="e091d-113">Déployer votre API en tant qu’application web ou application API</span><span class="sxs-lookup"><span data-stu-id="e091d-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="e091d-114">Pour pouvoir appeler votre API personnalisée à partir d’une application logique, déployez votre API en tant qu’application web ou application API sur Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="e091d-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app to Azure App Service.</span></span> <span data-ttu-id="e091d-115">Par ailleurs, pour vous assurer de la lisibilité du document Swagger par le concepteur d’application logique, définissez les propriétés de définition d’API et activez le [partage des ressources Cross-Origin (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) pour votre application web ou votre application API.</span><span class="sxs-lookup"><span data-stu-id="e091d-115">Also, to make your Swagger document readable by the Logic App Designer, set the API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="e091d-116">Dans le portail Azure, sélectionnez votre application web ou votre application API.</span><span class="sxs-lookup"><span data-stu-id="e091d-116">In the Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="e091d-117">Dans le panneau qui s’ouvre, sous **API**, choisissez **Définition de l’API**.</span><span class="sxs-lookup"><span data-stu-id="e091d-117">In the blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="e091d-118">Sous **Emplacement de la définition de l’API**, spécifiez l’URL de votre fichier swagger.json.</span><span class="sxs-lookup"><span data-stu-id="e091d-118">Set the **API definition location** to the URL for your swagger.json file.</span></span>

   <span data-ttu-id="e091d-119">En règle générale, l’URL se présente sous le format suivant :`https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="e091d-119">Usually, the URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![Lien vers le fichier Swagger pour votre API personnalisée](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="e091d-121">Sous **API**, choisissez **CORS**.</span><span class="sxs-lookup"><span data-stu-id="e091d-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="e091d-122">Dans le cadre de la stratégie CORS, sous **Origines autorisées**, spécifiez **'*'** (tout autoriser).</span><span class="sxs-lookup"><span data-stu-id="e091d-122">Set the CORS policy for **Allowed origins** to **'*'** (allow all).</span></span>

   <span data-ttu-id="e091d-123">Ce paramètre autorise les demandes à partir du concepteur d’application logique.</span><span class="sxs-lookup"><span data-stu-id="e091d-123">This setting permits requests from Logic App Designer.</span></span>

   ![Autoriser les demandes du concepteur d’application logique à votre API personnalisée](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="e091d-125">Pour plus d’informations, voir les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="e091d-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="e091d-126">Utiliser l’interface utilisateur et les métadonnées d’API Swagger</span><span class="sxs-lookup"><span data-stu-id="e091d-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="e091d-127">Prise en main d’API Apps, d’ASP.NET et de Swagger dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e091d-127">Deploy ASP.NET web APIs to Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="e091d-128">Appeler votre API personnalisée à partir de flux de travail d’application logique</span><span class="sxs-lookup"><span data-stu-id="e091d-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="e091d-129">Une fois les propriétés de définition d’API et le partage CORS configurés, les déclencheurs et actions de votre API personnalisée doivent devenir disponibles, de sorte que vous puissiez les inclure dans votre flux de travail d’application logique.</span><span class="sxs-lookup"><span data-stu-id="e091d-129">After you set up the API definition properties and CORS, your custom API's triggers and actions should become available for you to include in your logic app workflow.</span></span> 

*  <span data-ttu-id="e091d-130">Pour afficher les sites web possédant des URL Swagger, vous pouvez parcourir vos sites web d’abonnement dans le concepteur d’application logique.</span><span class="sxs-lookup"><span data-stu-id="e091d-130">To view the websites that have Swagger URLs, you can browse your subscription websites in the Logic Apps Designer.</span></span>

*  <span data-ttu-id="e091d-131">Pour afficher les actions et entrées disponibles en pointant sur un document Swagger, utilisez [l’action HTTP + Swagger](../connectors/connectors-native-http-swagger.md).</span><span class="sxs-lookup"><span data-stu-id="e091d-131">To view available actions and inputs by pointing at a Swagger document, use the [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="e091d-132">Pour appeler n’importe quelle API, y compris celles qui n’ont pas ou n’exposent pas de document Swagger, vous pouvez aussi créer une requête à l’aide de [l’action HTTP](../connectors/connectors-native-http.md).</span><span class="sxs-lookup"><span data-stu-id="e091d-132">To call any API, including APIs that don't have or expose a Swagger document, you can always create a request with the [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-to-your-custom-api"></a><span data-ttu-id="e091d-133">Authentifier les appels à votre API personnalisée</span><span class="sxs-lookup"><span data-stu-id="e091d-133">Authenticate calls to your custom API</span></span>

<span data-ttu-id="e091d-134">Vous pouvez sécuriser les appels à votre API personnalisée en appliquant les méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="e091d-134">You can secure calls to your custom API in these ways:</span></span>

* <span data-ttu-id="e091d-135">[Aucune modification de code](#no-code) : protégez votre API avec [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) par le biais du Portail Azure, ce qui vous évite de mettre à jour votre code ou de redéployer votre API.</span><span class="sxs-lookup"><span data-stu-id="e091d-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through the Azure portal, so you don't have to update your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e091d-136">Par défaut, l’authentification Azure AD que vous activez dans le Portail Azure ne fournit pas une autorisation affinée.</span><span class="sxs-lookup"><span data-stu-id="e091d-136">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="e091d-137">Par exemple, cette authentification verrouille votre API vis-à-vis d’un locataire spécifique et non d’un utilisateur ou d’une application spécifique.</span><span class="sxs-lookup"><span data-stu-id="e091d-137">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span></span> 

* <span data-ttu-id="e091d-138">[Mise à jour du code de votre API](#update-code) : protégez votre API en appliquant [l’authentification par certificat](#certificate), [l’authentification de base](#basic) ou [l’authentification Azure AD](#azure-ad-code) par le biais du code.</span><span class="sxs-lookup"><span data-stu-id="e091d-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-to-your-api-without-changing-code"></a><span data-ttu-id="e091d-139">Authentifier les appels à votre API sans modifier le code</span><span class="sxs-lookup"><span data-stu-id="e091d-139">Authenticate calls to your API without changing code</span></span>

<span data-ttu-id="e091d-140">Voici les étapes générales de cette méthode :</span><span class="sxs-lookup"><span data-stu-id="e091d-140">Here's the general steps for this method:</span></span>

1. <span data-ttu-id="e091d-141">Créez deux [identités d’application Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md) : une pour votre application logique et l’autre pour votre application web (ou application API).</span><span class="sxs-lookup"><span data-stu-id="e091d-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="e091d-142">Pour authentifier les appels à votre API, utilisez les informations d’identification (ID et clé secrète client) pour le [principal de service](../app-service-api/app-service-api-dotnet-service-principal-auth.md) associé à l’identité d’application Azure AD pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="e091d-142">To authenticate calls to your API, use the credentials (client ID and secret) for the [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with the Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="e091d-143">Incluez les ID d’application dans votre définition d’application logique.</span><span class="sxs-lookup"><span data-stu-id="e091d-143">Include the application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="e091d-144">Partie 1 : Créer une identité d’application Azure AD pour votre application logique</span><span class="sxs-lookup"><span data-stu-id="e091d-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="e091d-145">Votre application logique utilise cette identité d’application Azure AD pour s’authentifier auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e091d-145">Your logic app uses this Azure AD application identity to authenticate against Azure AD.</span></span> <span data-ttu-id="e091d-146">Vous n’avez besoin de configurer cette identité qu’une seule fois pour votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="e091d-146">You only have to set up this identity one time for your directory.</span></span> <span data-ttu-id="e091d-147">Par exemple, vous pouvez choisir d’utiliser la même identité pour toutes vos applications logiques, même si vous pouvez créer des identités uniques pour chaque application logique.</span><span class="sxs-lookup"><span data-stu-id="e091d-147">For example, you can choose to use the same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="e091d-148">Vous pouvez configurer ces identités dans le Portail Azure, dans le [Portail Azure Classic](#app-identity-logic-classic) ou à l’aide de [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="e091d-148">You can set up these identities in the Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="e091d-149">**Créer l’identité d’application pour votre application logique dans le Portail Azure**</span><span class="sxs-lookup"><span data-stu-id="e091d-149">**Create the application identity for your logic app in the Azure portal**</span></span>

1. <span data-ttu-id="e091d-150">Dans le [Portail Azure](https://portal.azure.com "https://portal.azure.com"), choisissez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e091d-150">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="e091d-151">Vérifiez que vous vous trouvez dans le même répertoire que votre application web ou votre application API.</span><span class="sxs-lookup"><span data-stu-id="e091d-151">Confirm that you're in the same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="e091d-152">Pour changer de répertoire, cliquez sur votre profil et sélectionnez un autre répertoire.</span><span class="sxs-lookup"><span data-stu-id="e091d-152">To switch directories, click your profile and select another directory.</span></span> <span data-ttu-id="e091d-153">Vous pouvez également sélectionner **Présentation** > **Changer de répertoire**.</span><span class="sxs-lookup"><span data-stu-id="e091d-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="e091d-154">Dans le menu du répertoire, sous **Gérer**, choisissez **Inscriptions des applications** > **Nouvelle inscription d’application**.</span><span class="sxs-lookup"><span data-stu-id="e091d-154">On the directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="e091d-155">Par défaut, la liste des inscriptions d’application affiche toutes les inscriptions d’application de votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="e091d-155">By default, the app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="e091d-156">Pour afficher uniquement vos inscriptions d’application, sélectionnez **Mes applications** en regard de la zone de recherche.</span><span class="sxs-lookup"><span data-stu-id="e091d-156">To view only your app registrations, next to the search box, select **My apps**.</span></span> 

   ![Créer une inscription d’application](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="e091d-158">Donnez un nom à votre identité d’application, laissez le champ **Type d’application** défini sur **Application/API web**, indiquez une chaîne unique sous forme de domaine sous **URL de connexion**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="e091d-158">Give your application identity a name, leave **Application type** set to **Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![Indication d’un nom et d’une URL de connexion pour l’identité de l’application](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="e091d-160">L’identité d’application que vous avez créée pour votre application logique s’affiche maintenant dans la liste des inscriptions d’application.</span><span class="sxs-lookup"><span data-stu-id="e091d-160">The application identity that you created for your logic app now appears in the app registrations list.</span></span>

   ![Identité d’application pour votre application logique](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="e091d-162">Dans la liste des inscriptions d’application, sélectionnez votre nouvelle identité d’application.</span><span class="sxs-lookup"><span data-stu-id="e091d-162">In the app registrations list, select your new application identity.</span></span> <span data-ttu-id="e091d-163">Copiez et enregistrez **l’ID de l’application** à utiliser en tant qu’ID client pour votre application logique dans la partie 3.</span><span class="sxs-lookup"><span data-stu-id="e091d-163">Copy and save the **Application ID** to use as the "client ID" for your logic app in Part 3.</span></span>

   ![Copie et enregistrement de l’ID de l’application pour l’application logique](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="e091d-165">Si vos paramètres d’identité d’application ne sont pas visibles, choisissez **Paramètres** ou **Tous les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="e091d-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="e091d-166">Sous **Accès d’API**, choisissez **Clés**.</span><span class="sxs-lookup"><span data-stu-id="e091d-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="e091d-167">Sous **Description**, indiquez le nom de votre clé.</span><span class="sxs-lookup"><span data-stu-id="e091d-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="e091d-168">Sous **Date d’expiration**, sélectionnez la durée de votre clé.</span><span class="sxs-lookup"><span data-stu-id="e091d-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="e091d-169">La clé que vous créez joue le rôle de clé secrète ou de mot de passe de l’identité de l’application pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="e091d-169">The key that you're creating acts as the application identity's "secret" or password for your logic app.</span></span>

   ![Création d’une clé pour l’identité de l’application logique](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="e091d-171">Dans la barre d’outils, choisissez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e091d-171">On the toolbar, choose **Save**.</span></span> <span data-ttu-id="e091d-172">Votre clé apparaît maintenant sous **Valeur**.</span><span class="sxs-lookup"><span data-stu-id="e091d-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="e091d-173">**Veillez à copier et enregistrer votre clé** en vue d’une utilisation ultérieure. En effet, la clé est masquée lorsque vous quittez le panneau correspondant.</span><span class="sxs-lookup"><span data-stu-id="e091d-173">**Make sure to copy and save your key** for later use because the key is hidden when you leave the key blade.</span></span>

   <span data-ttu-id="e091d-174">Lorsque vous configurez votre application logique dans la partie 3, vous spécifiez cette clé comme clé secrète ou mot de passe.</span><span class="sxs-lookup"><span data-stu-id="e091d-174">When you configure your logic app in Part 3, you specify this key as the "secret" or password.</span></span>

   ![Copie et enregistrement de la clé pour une utilisation ultérieure](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="e091d-176">**Créer l’identité d’application pour votre application logique dans le Portail Azure Classic**</span><span class="sxs-lookup"><span data-stu-id="e091d-176">**Create the application identity for your logic app in the Azure classic portal**</span></span>

1. <span data-ttu-id="e091d-177">Dans le Portail Azure Classic, choisissez [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="e091d-177">In the Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="e091d-178">Sélectionnez le répertoire utilisé pour votre application web ou votre application API.</span><span class="sxs-lookup"><span data-stu-id="e091d-178">Select the same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="e091d-179">Dans l’onglet **Applications**, cliquez sur **Ajouter** au bas de la page.</span><span class="sxs-lookup"><span data-stu-id="e091d-179">On the **Applications** tab, choose **Add** at the bottom of the page.</span></span>

4. <span data-ttu-id="e091d-180">Donnez un nom à votre identité d’application, puis cliquez sur **Suivant** (flèche droite).</span><span class="sxs-lookup"><span data-stu-id="e091d-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="e091d-181">Sous **Propriétés de l’application**, indiquez une chaîne unique sous forme de domaine sous **URL de connexion** et **URI ID d’application**, puis choisissez **Terminer** (coche).</span><span class="sxs-lookup"><span data-stu-id="e091d-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="e091d-182">Dans l’onglet **Configurer**, copiez et enregistrez **l’ID client** pour votre application logique. Vous l’utiliserez dans la partie 3.</span><span class="sxs-lookup"><span data-stu-id="e091d-182">On the **Configure** tab, copy and save the **Client ID** for your logic app to use in Part 3.</span></span>

7. <span data-ttu-id="e091d-183">Sous **Clés**, ouvrez la liste **Sélectionner une durée**.</span><span class="sxs-lookup"><span data-stu-id="e091d-183">Under **Keys**, open the **Select duration** list.</span></span> <span data-ttu-id="e091d-184">Sélectionnez la durée de votre clé.</span><span class="sxs-lookup"><span data-stu-id="e091d-184">Select a duration for your key.</span></span>

   <span data-ttu-id="e091d-185">La clé que vous créez joue le rôle de clé secrète ou de mot de passe de l’identité d’application pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="e091d-185">The key that you're creating acts as the application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="e091d-186">En bas de la page, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e091d-186">At the bottom of the page, choose **Save**.</span></span> <span data-ttu-id="e091d-187">Vous devrez peut-être patienter quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="e091d-187">You might have to wait a few seconds.</span></span>

9. <span data-ttu-id="e091d-188">Sous **Clés**, veillez à copier et enregistrer la clé qui s’affiche à présent.</span><span class="sxs-lookup"><span data-stu-id="e091d-188">Under **Keys**, make sure to copy and save the key that now appears.</span></span> 

   <span data-ttu-id="e091d-189">Lorsque vous configurez votre application logique dans la partie 3, vous spécifiez cette clé comme clé secrète ou mot de passe.</span><span class="sxs-lookup"><span data-stu-id="e091d-189">When you configure your logic app in Part 3, you specify this key as the "secret" or password.</span></span>

<span data-ttu-id="e091d-190">Pour plus d’informations, voir [Configurer votre application App Service pour utiliser la connexion Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="e091d-190">For more information, learn how to [configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="e091d-191">**Créer l’identité d’application pour votre application logique dans PowerShell**</span><span class="sxs-lookup"><span data-stu-id="e091d-191">**Create the application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="e091d-192">Vous pouvez effectuer cette tâche par le biais d’Azure Resource Manager avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e091d-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="e091d-193">Dans PowerShell, exécutez ces commandes :</span><span class="sxs-lookup"><span data-stu-id="e091d-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="e091d-194">Veillez à copier **l’ID de locataire** (GUID pour votre locataire Azure AD), **l’ID d’application** et le mot de passe que vous avez utilisé.</span><span class="sxs-lookup"><span data-stu-id="e091d-194">Make sure to copy the **Tenant ID** (GUID for your Azure AD tenant), the **Application ID**, and the password that you used.</span></span>

<span data-ttu-id="e091d-195">Pour plus d’informations, consultez la page [Créer un principal du service pour accéder aux ressources à l’aide d’Azure PowerShell](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="e091d-195">For more information, learn how to [create a service principal with PowerShell to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="e091d-196">Partie 2 : Créer une identité d’application Azure AD pour votre application web ou votre application API</span><span class="sxs-lookup"><span data-stu-id="e091d-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="e091d-197">Si votre application web ou votre application API est déjà déployée, vous pouvez activer l’authentification et créer l’identité de l’application dans le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e091d-197">If your web app or API app is already deployed, you can turn on authentication and create the application identity in the Azure portal.</span></span> <span data-ttu-id="e091d-198">Sinon, vous pouvez [activer l’authentification lorsque vous effectuez un déploiement avec un modèle Azure Resource Manager](#authen-deploy).</span><span class="sxs-lookup"><span data-stu-id="e091d-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="e091d-199">**Créer l’identité d’application et activer l’authentification dans le Portail Azure pour les applications déployées**</span><span class="sxs-lookup"><span data-stu-id="e091d-199">**Create the application identity and turn on authentication in the Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="e091d-200">Dans le [Portail Azure](https://portal.azure.com "https://portal.azure.com"), recherchez et sélectionnez votre application web ou votre application API.</span><span class="sxs-lookup"><span data-stu-id="e091d-200">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="e091d-201">Sous **Paramètres**, choisissez **Authentification/Autorisation**.</span><span class="sxs-lookup"><span data-stu-id="e091d-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="e091d-202">Sous **Authentification App Service**, activez **l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="e091d-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="e091d-203">Sous **Fournisseurs d’authentification**, sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e091d-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![Activer l’authentification](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="e091d-205">À présent, créez une identité d’application pour votre application web ou votre application API comme indiqué ici.</span><span class="sxs-lookup"><span data-stu-id="e091d-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="e091d-206">Dans le panneau **Paramètres Azure Active Directory**, définissez le **Mode d’administration** sur **Express**.</span><span class="sxs-lookup"><span data-stu-id="e091d-206">On the **Azure Active Directory Settings** blade, set **Management mode** to **Express**.</span></span> <span data-ttu-id="e091d-207">Choisissez **Créer une application AD**.</span><span class="sxs-lookup"><span data-stu-id="e091d-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="e091d-208">Donnez un nom à votre identité d’application, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e091d-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![Créer une identité d’application pour votre application web ou votre application API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="e091d-210">Dans le panneau **Authentification/Autorisation**, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="e091d-210">On the **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="e091d-211">Vous devez à présent rechercher l’ID client et l’ID de locataire pour l’identité d’application associée à votre application web ou votre application API.</span><span class="sxs-lookup"><span data-stu-id="e091d-211">Now you must find the client ID and tenant ID for the application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="e091d-212">Vous utiliserez ces ID dans la partie 3.</span><span class="sxs-lookup"><span data-stu-id="e091d-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="e091d-213">Poursuivez cette procédure avec le Portail Azure ou le [Portail Azure Classic](#find-id-classic).</span><span class="sxs-lookup"><span data-stu-id="e091d-213">So continue with these steps for the Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="e091d-214">**Rechercher l’ID client et l’ID de locataire de l’identité de l’application pour votre application web ou votre application API dans le Portail Azure**</span><span class="sxs-lookup"><span data-stu-id="e091d-214">**Find application identity's client ID and tenant ID for your web app or API app in the Azure portal**</span></span>

1. <span data-ttu-id="e091d-215">Sous **Fournisseurs d’authentification**, sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e091d-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   ![Sélectionner « Azure Active Directory »](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="e091d-217">Dans le panneau **Paramètres Azure Active Directory**, définissez le **Mode d’administration** sur **Avancé**.</span><span class="sxs-lookup"><span data-stu-id="e091d-217">On the **Azure Active Directory Settings** blade, set **Management mode** to **Advanced**.</span></span>

3. <span data-ttu-id="e091d-218">Copiez **l’ID client** et enregistrez ce GUID en vue de son utilisation dans la partie 3.</span><span class="sxs-lookup"><span data-stu-id="e091d-218">Copy the **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="e091d-219">Si **l’ID client** et **l’URL de l’émetteur** ne s’affichent, essayez d’actualiser le Portail Azure et répétez l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="e091d-219">If **Client ID** and **Issuer Url** don't appear, try refreshing the Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="e091d-220">Sous **URL de l’émetteur**, copiez et enregistrez simplement le GUID pour la partie 3.</span><span class="sxs-lookup"><span data-stu-id="e091d-220">Under **Issuer Url**, copy and save just the GUID for Part 3.</span></span> <span data-ttu-id="e091d-221">Vous pouvez également utiliser ce GUID dans le modèle de déploiement de votre application web ou de votre application API si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e091d-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="e091d-222">Ce GUID est celui de votre locataire spécifique (« ID de locataire ») et doit apparaître dans cette URL :`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="e091d-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="e091d-223">Sans enregistrer vos modifications, fermez le panneau **Paramètres Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e091d-223">Without saving your changes, close the **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="e091d-224">**Rechercher l’ID client et l’ID de locataire de l’identité d’application pour votre application web ou votre application API dans le Portail Azure Classic**</span><span class="sxs-lookup"><span data-stu-id="e091d-224">**Find application identity's client ID and tenant ID for your web app or API app in the Azure classic portal**</span></span>

1. <span data-ttu-id="e091d-225">Dans le Portail Azure Classic, choisissez [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="e091d-225">In the Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="e091d-226">Sélectionnez le répertoire utilisé pour votre application web ou votre application API.</span><span class="sxs-lookup"><span data-stu-id="e091d-226">Select the directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="e091d-227">Dans la zone **Rechercher**, recherchez et sélectionnez l’identité d’application pour votre application web ou votre application API.</span><span class="sxs-lookup"><span data-stu-id="e091d-227">In the **Search** box, find and select the application identity for your web app or API app.</span></span>

4. <span data-ttu-id="e091d-228">Dans l’onglet **Configurer**, copiez **l’ID client** et enregistrez ce GUID en vue de son utilisation dans la partie 3.</span><span class="sxs-lookup"><span data-stu-id="e091d-228">On the **Configure** tab, copy the **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="e091d-229">Après avoir obtenu l’ID client, au bas de l’onglet **Configurer**, choisissez **Points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="e091d-229">After you get the client ID, at the bottom of the **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="e091d-230">Copiez l’URL du **Document de métadonnées de fédération**, puis accédez à cette URL.</span><span class="sxs-lookup"><span data-stu-id="e091d-230">Copy the URL for **Federation Metadata Document**, and browse to that URL.</span></span>

7. <span data-ttu-id="e091d-231">Dans le document de métadonnées qui s’ouvre, recherchez l’élément racine **EntityDescriptor ID**, qui possède un attribut **entityID** sous cette forme :`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="e091d-231">In the metadata document that opens, find the root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="e091d-232">Le GUID de cet attribut est celui de votre locataire spécifique (ID de locataire).</span><span class="sxs-lookup"><span data-stu-id="e091d-232">The GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="e091d-233">Copiez l’ID de locataire et enregistrez-le en vue de son utilisation dans la partie 3. Vous l’utiliserez également dans le modèle de déploiement de votre application web ou de votre application API si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e091d-233">Copy the tenant ID and save that ID for use in Part 3, and also to use in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="e091d-234">Pour plus d’informations, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="e091d-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="e091d-235">Authentification utilisateur pour les applications API dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e091d-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="e091d-236">Authentification et autorisation dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e091d-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="e091d-237">**Activer l’authentification lorsque vous effectuez un déploiement avec un modèle Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="e091d-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="e091d-238">Vous devez toujours créer une identité d’application Azure AD pour votre application web ou votre application API, différente de l’identité d’application pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="e091d-238">You must still create an Azure AD application identity for your web app or API app that differs from the app identity for your logic app.</span></span> <span data-ttu-id="e091d-239">Pour créer l’identité d’application, suivez les étapes précédentes de la partie 2 avec le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e091d-239">To create the application identity, follow the previous steps in Part 2 for the Azure portal.</span></span> <span data-ttu-id="e091d-240">Vous pouvez également suivre les étapes décrites dans la partie 1. Cependant, veillez à utiliser l’adresse `https://{URL}` réelle de votre application web ou de votre application API sous **URL de connexion** et **URI ID d’application**.</span><span class="sxs-lookup"><span data-stu-id="e091d-240">You can also follow the steps in Part 1, but make sure to use your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="e091d-241">À partir de ces étapes, vous devez enregistrer l’ID client et l’ID de locataire en vue de leur utilisation dans le modèle de déploiement de votre application. Vous les utiliserez également dans la partie 3.</span><span class="sxs-lookup"><span data-stu-id="e091d-241">From these steps, you have to save both the client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="e091d-242">Lorsque vous créez l’identité d’application Azure AD pour votre application web ou votre application API, vous devez utiliser le Portail Azure ou le Portail Azure Classic plutôt que PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e091d-242">When you create the Azure AD application identity for your web app or API app, you must use the Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="e091d-243">L’applet de commande PowerShell ne configure pas les autorisations requises pour connecter les utilisateurs à un site web.</span><span class="sxs-lookup"><span data-stu-id="e091d-243">The PowerShell commandlet doesn't set up the required permissions to sign users into a website.</span></span>

<span data-ttu-id="e091d-244">Une fois que vous disposez de l’ID client et de l’ID de locataire, incluez-les en tant que sous-ressource de votre application web ou de votre application API dans votre modèle de déploiement :</span><span class="sxs-lookup"><span data-stu-id="e091d-244">After you get the client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

<span data-ttu-id="e091d-245">Pour déployer automatiquement une application web et une application logique vides avec l’authentification Azure Active Directory, [consultez le modèle complet](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json) ou cliquez sur **Déploiement sur Azure** ici :</span><span class="sxs-lookup"><span data-stu-id="e091d-245">To automatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view the complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy to Azure** here:</span></span>

<span data-ttu-id="e091d-246">[![Déploiement sur Azure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="e091d-246">[![Deploy to Azure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-the-authorization-section-in-your-logic-app"></a><span data-ttu-id="e091d-247">Partie 3 : Remplir la section Autorisation dans votre application logique</span><span class="sxs-lookup"><span data-stu-id="e091d-247">Part 3: Populate the Authorization section in your logic app</span></span>

<span data-ttu-id="e091d-248">Cette section d’autorisation est déjà configurée dans le modèle précédent, mais si vous créez l’application logique directement, vous devez inclure la section d’autorisation complète.</span><span class="sxs-lookup"><span data-stu-id="e091d-248">The previous template already has this authorization section set up, but if you are directly authoring the logic app, you must include the full authorization section.</span></span>

<span data-ttu-id="e091d-249">Ouvrez votre définition d’application logique en mode code, accédez à la section d’action **HTTP**, recherchez la section **Autorisation** et ajoutez cette ligne :</span><span class="sxs-lookup"><span data-stu-id="e091d-249">Open your logic app definition in code view, go to the **HTTP** action section, find the **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="e091d-250">Élément</span><span class="sxs-lookup"><span data-stu-id="e091d-250">Element</span></span> | <span data-ttu-id="e091d-251">Description</span><span class="sxs-lookup"><span data-stu-id="e091d-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="e091d-252">locataire</span><span class="sxs-lookup"><span data-stu-id="e091d-252">tenant</span></span> |<span data-ttu-id="e091d-253">GUID du locataire Azure AD</span><span class="sxs-lookup"><span data-stu-id="e091d-253">The GUID for the Azure AD tenant</span></span> |
| <span data-ttu-id="e091d-254">audience</span><span class="sxs-lookup"><span data-stu-id="e091d-254">audience</span></span> |<span data-ttu-id="e091d-255">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="e091d-255">Required.</span></span> <span data-ttu-id="e091d-256">GUID de la ressource cible à laquelle vous souhaitez accéder - l’ID client de l’identité d’application pour votre application web ou votre application API</span><span class="sxs-lookup"><span data-stu-id="e091d-256">The GUID for the target resource that you want to access - the client ID from the application identity for your web app or API app</span></span> |
| <span data-ttu-id="e091d-257">clientId</span><span class="sxs-lookup"><span data-stu-id="e091d-257">clientId</span></span> |<span data-ttu-id="e091d-258">GUID pour le client demandant l’accès - l’ID client de l’identité d’application pour votre application logique</span><span class="sxs-lookup"><span data-stu-id="e091d-258">The GUID for the client requesting access - the client ID from the application identity for your logic app</span></span> |
| <span data-ttu-id="e091d-259">secret</span><span class="sxs-lookup"><span data-stu-id="e091d-259">secret</span></span> |<span data-ttu-id="e091d-260">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="e091d-260">Required.</span></span> <span data-ttu-id="e091d-261">Clé ou mot de passe de l’identité d’application pour le client qui demande le jeton d’accès</span><span class="sxs-lookup"><span data-stu-id="e091d-261">The key or password from the application identity for the client that's requesting the access token</span></span> |
| <span data-ttu-id="e091d-262">Type</span><span class="sxs-lookup"><span data-stu-id="e091d-262">type</span></span> |<span data-ttu-id="e091d-263">Type d’authentification.</span><span class="sxs-lookup"><span data-stu-id="e091d-263">The authentication type.</span></span> <span data-ttu-id="e091d-264">Pour l’authentification ActiveDirectoryOAuth, la valeur est `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="e091d-264">For ActiveDirectoryOAuth authentication, the value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="e091d-265">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e091d-265">For example:</span></span>

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="e091d-266">Sécuriser les appels à l’API avec le code</span><span class="sxs-lookup"><span data-stu-id="e091d-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="e091d-267">Authentification par certificat</span><span class="sxs-lookup"><span data-stu-id="e091d-267">Certificate authentication</span></span>

<span data-ttu-id="e091d-268">Vous pouvez utiliser des certificats clients pour valider les demandes entrantes de votre application logique parvenant à votre application web ou votre application API.</span><span class="sxs-lookup"><span data-stu-id="e091d-268">To validate the incoming requests from your logic app to your web app or API app, you can use client certificates.</span></span> <span data-ttu-id="e091d-269">Pour configurer votre code, consultez [Configuration de l’authentification mutuelle TLS pour une application web](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span><span class="sxs-lookup"><span data-stu-id="e091d-269">To set up your code, learn [how to configure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="e091d-270">Dans la section **Autorisation**, ajoutez cette ligne :</span><span class="sxs-lookup"><span data-stu-id="e091d-270">In the **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="e091d-271">Élément</span><span class="sxs-lookup"><span data-stu-id="e091d-271">Element</span></span> | <span data-ttu-id="e091d-272">Description</span><span class="sxs-lookup"><span data-stu-id="e091d-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="e091d-273">type</span><span class="sxs-lookup"><span data-stu-id="e091d-273">type</span></span> |<span data-ttu-id="e091d-274">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="e091d-274">Required.</span></span> <span data-ttu-id="e091d-275">Type d’authentification.</span><span class="sxs-lookup"><span data-stu-id="e091d-275">The authentication type.</span></span> <span data-ttu-id="e091d-276">Pour les certificats client SSL, la valeur doit être `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="e091d-276">For SSL client certificates, the value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="e091d-277">password</span><span class="sxs-lookup"><span data-stu-id="e091d-277">password</span></span> |<span data-ttu-id="e091d-278">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="e091d-278">Required.</span></span> <span data-ttu-id="e091d-279">Mot de passe pour l’accès au certificat client (fichier PFX)</span><span class="sxs-lookup"><span data-stu-id="e091d-279">The password for accessing the client certificate (PFX file)</span></span> |
| <span data-ttu-id="e091d-280">pfx</span><span class="sxs-lookup"><span data-stu-id="e091d-280">pfx</span></span> |<span data-ttu-id="e091d-281">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="e091d-281">Required.</span></span> <span data-ttu-id="e091d-282">Contenu codé en base64 pour le certificat client (fichier PFX)</span><span class="sxs-lookup"><span data-stu-id="e091d-282">Base64-encoded contents of the client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="e091d-283">Authentification de base</span><span class="sxs-lookup"><span data-stu-id="e091d-283">Basic authentication</span></span>

<span data-ttu-id="e091d-284">Pour valider les demandes entrantes de votre application logique à l’attention de votre application web ou de votre application API, vous pouvez utiliser l’authentification de base, par exemple, un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="e091d-284">To validate incoming requests from your logic app to your web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="e091d-285">L’authentification de base est une méthode courante que vous pouvez utiliser dans n’importe quel langage utilisé pour générer votre application web ou votre application API.</span><span class="sxs-lookup"><span data-stu-id="e091d-285">Basic authentication is a common pattern, and you can use this authentication in any language used to build your web app or API app.</span></span>

<span data-ttu-id="e091d-286">Dans la section **Autorisation**, ajoutez cette ligne :</span><span class="sxs-lookup"><span data-stu-id="e091d-286">In the **Authorization** section, include this line:</span></span>

<span data-ttu-id="e091d-287">`{"type": "basic", "username": "username", "password": "password"}`.</span><span class="sxs-lookup"><span data-stu-id="e091d-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="e091d-288">Élément</span><span class="sxs-lookup"><span data-stu-id="e091d-288">Element</span></span> | <span data-ttu-id="e091d-289">Description</span><span class="sxs-lookup"><span data-stu-id="e091d-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e091d-290">type</span><span class="sxs-lookup"><span data-stu-id="e091d-290">type</span></span> |<span data-ttu-id="e091d-291">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="e091d-291">Required.</span></span> <span data-ttu-id="e091d-292">Type d’authentification.</span><span class="sxs-lookup"><span data-stu-id="e091d-292">The authentication type.</span></span> <span data-ttu-id="e091d-293">Pour l’authentification de base, la valeur doit être `Basic`.</span><span class="sxs-lookup"><span data-stu-id="e091d-293">For basic authentication, the value must be `Basic`.</span></span> |
| <span data-ttu-id="e091d-294">username</span><span class="sxs-lookup"><span data-stu-id="e091d-294">username</span></span> |<span data-ttu-id="e091d-295">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="e091d-295">Required.</span></span> <span data-ttu-id="e091d-296">Nom d’utilisateur pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="e091d-296">The username for authentication</span></span> |
| <span data-ttu-id="e091d-297">password</span><span class="sxs-lookup"><span data-stu-id="e091d-297">password</span></span> |<span data-ttu-id="e091d-298">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="e091d-298">Required.</span></span> <span data-ttu-id="e091d-299">Mot de passe pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="e091d-299">The password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="e091d-300">Authentification Azure Active Directory avec le code</span><span class="sxs-lookup"><span data-stu-id="e091d-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="e091d-301">Par défaut, l’authentification Azure AD que vous activez dans le Portail Azure ne fournit pas une autorisation affinée.</span><span class="sxs-lookup"><span data-stu-id="e091d-301">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="e091d-302">Par exemple, cette authentification verrouille votre API vis-à-vis d’un locataire spécifique et non d’un utilisateur ou d’une application spécifique.</span><span class="sxs-lookup"><span data-stu-id="e091d-302">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span></span> 

<span data-ttu-id="e091d-303">Pour restreindre l’accès des API à votre application logique à l’aide du code, extrayez l’en-tête contenant le jeton JWT (JSON Web Token).</span><span class="sxs-lookup"><span data-stu-id="e091d-303">To restrict API access to your logic app through code, extract the header that has the JSON web token (JWT).</span></span> <span data-ttu-id="e091d-304">Vérifiez l’identité de l’appelant et rejetez les demandes qui ne correspondent pas.</span><span class="sxs-lookup"><span data-stu-id="e091d-304">Check the caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="e091d-305">Pour aller plus loin, si vous souhaitez implémenter cette authentification en totalité dans votre code et ne pas utiliser le Portail Azure, consultez [Authentification avec Active Directory en local dans votre application Azure](../app-service-web/web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="e091d-305">Going further, to implement this authentication entirely in your own code, and not use the Azure portal, learn how to [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="e091d-306">Pour créer une identité d’application pour votre application logique, puis utiliser cette identité pour appeler votre API, vous devez suivre les étapes précédentes.</span><span class="sxs-lookup"><span data-stu-id="e091d-306">To create an application identity for your logic app and use that identity to call your API, you must follow the previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e091d-307">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e091d-307">Next steps</span></span>

* [<span data-ttu-id="e091d-308">Vérifier les performances de l’application logique avec des alertes et des journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="e091d-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)