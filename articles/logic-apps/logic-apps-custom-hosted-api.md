---
title: "aaaDeploy, appeler et s’authentifier web API et les API REST pour Azure Logic Apps | Documents Microsoft"
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
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="7f59c-104">Déployer, appeler et authentifier des API personnalisées en tant que connecteurs pour les applications logiques</span><span class="sxs-lookup"><span data-stu-id="7f59c-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="7f59c-105">Après avoir [créer des API personnalisées](./logic-apps-create-api-app.md) qui fournissent des actions ou des déclencheurs toouse dans la logique de flux de travail applications, vous devez déployer votre API avant de les appeler.</span><span class="sxs-lookup"><span data-stu-id="7f59c-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers toouse in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="7f59c-106">Bien que vous pouvez appeler une API à partir d’une application logique, pour une meilleure expérience de hello, ajoutez [Swagger métadonnées](http://swagger.io/specification/) qui décrit les opérations et les paramètres de votre API.</span><span class="sxs-lookup"><span data-stu-id="7f59c-106">And although you can call any API from a logic app, for hello best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="7f59c-107">Ce fichier Swagger améliore le fonctionnent de votre API et simplifie son intégration aux applications logiques.</span><span class="sxs-lookup"><span data-stu-id="7f59c-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="7f59c-108">Vous pouvez déployer votre API comme [les applications web](../app-service-web/app-service-web-overview.md), mais envisagez de déployer votre API comme [applications API](../app-service-api/app-service-api-apps-why-best-platform.md), qui peut simplifier votre travail lorsque vous générez, hébergez et consommer des API dans le cloud de hello et localement.</span><span class="sxs-lookup"><span data-stu-id="7f59c-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in hello cloud and on premises.</span></span> <span data-ttu-id="7f59c-109">Vous n’avez pas de code toochange dans votre API--simplement déployer votre application API de tooan code.</span><span class="sxs-lookup"><span data-stu-id="7f59c-109">You don't have toochange any code in your APIs -- just deploy your code tooan API app.</span></span> <span data-ttu-id="7f59c-110">Vous pouvez héberger votre API sur [Azure App Service](../app-service/app-service-value-prop-what-is.md), un platform-as-a-service (PaaS) qui fournit une des manières de meilleures, plus simple et plus évolutive hello pour l’hébergement de l’API de l’offre.</span><span class="sxs-lookup"><span data-stu-id="7f59c-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of hello best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="7f59c-111">tooauthenticate les appels d’applications de logique tooyour API, vous pouvez configurer Azure Active Directory Bonjour portail Azure, vous n’avez tooupdate votre code.</span><span class="sxs-lookup"><span data-stu-id="7f59c-111">tooauthenticate calls from logic apps tooyour APIs, you can set up Azure Active Directory in hello Azure portal so you don't have tooupdate your code.</span></span> <span data-ttu-id="7f59c-112">Vous pouvez également exiger et appliquer une authentification par le biais du code de votre API.</span><span class="sxs-lookup"><span data-stu-id="7f59c-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="7f59c-113">Déployer votre API en tant qu’application web ou application API</span><span class="sxs-lookup"><span data-stu-id="7f59c-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="7f59c-114">Avant de pouvoir appeler votre API personnalisée à partir d’une application logique, déployez votre API comme une application web ou l’API application tooAzure du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="7f59c-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app tooAzure App Service.</span></span> <span data-ttu-id="7f59c-115">En outre, toomake votre document Swagger lisible par hello Concepteur d’application logique, définition des propriétés de définition de hello API et activer [ressources cross-origin (CORS) de partage](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) pour votre application web ou d’une application API.</span><span class="sxs-lookup"><span data-stu-id="7f59c-115">Also, toomake your Swagger document readable by hello Logic App Designer, set hello API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="7f59c-116">Bonjour portail Azure, sélectionnez votre application web ou une application API.</span><span class="sxs-lookup"><span data-stu-id="7f59c-116">In hello Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="7f59c-117">Dans le panneau hello qui s’ouvre, sous **API**, choisissez **définition d’API**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-117">In hello blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="7f59c-118">Ensemble hello **emplacement de définition d’API** toohello des URL pour votre fichier swagger.json.</span><span class="sxs-lookup"><span data-stu-id="7f59c-118">Set hello **API definition location** toohello URL for your swagger.json file.</span></span>

   <span data-ttu-id="7f59c-119">En règle générale, hello URL s’affiche dans ce format :`https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="7f59c-119">Usually, hello URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![Fichier tooSwagger de lien de votre API personnalisée](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="7f59c-121">Sous **API**, choisissez **CORS**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="7f59c-122">Définir la stratégie CORS hello pour **autorisée origines** trop**'*'** (tous les autoriser).</span><span class="sxs-lookup"><span data-stu-id="7f59c-122">Set hello CORS policy for **Allowed origins** too**'*'** (allow all).</span></span>

   <span data-ttu-id="7f59c-123">Ce paramètre autorise les demandes à partir du concepteur d’application logique.</span><span class="sxs-lookup"><span data-stu-id="7f59c-123">This setting permits requests from Logic App Designer.</span></span>

   ![Autoriser les demandes à partir de l’API de concepteur d’application logique tooyour personnalisée](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="7f59c-125">Pour plus d’informations, voir les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="7f59c-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="7f59c-126">Utiliser l’interface utilisateur et les métadonnées d’API Swagger</span><span class="sxs-lookup"><span data-stu-id="7f59c-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="7f59c-127">Déployer ASP.NET web API tooAzure du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="7f59c-127">Deploy ASP.NET web APIs tooAzure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="7f59c-128">Appeler votre API personnalisée à partir de flux de travail d’application logique</span><span class="sxs-lookup"><span data-stu-id="7f59c-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="7f59c-129">Après avoir défini les propriétés de la définition hello API et CORS, déclencheurs et les actions de votre API personnalisée doivent être accessible pour vous tooinclude dans votre workflow d’application logique.</span><span class="sxs-lookup"><span data-stu-id="7f59c-129">After you set up hello API definition properties and CORS, your custom API's triggers and actions should become available for you tooinclude in your logic app workflow.</span></span> 

*  <span data-ttu-id="7f59c-130">tooview hello des sites Web ayant des URL de Swagger, vous pouvez parcourir vos sites Web d’abonnement Bonjour logique de concepteur d’applications.</span><span class="sxs-lookup"><span data-stu-id="7f59c-130">tooview hello websites that have Swagger URLs, you can browse your subscription websites in hello Logic Apps Designer.</span></span>

*  <span data-ttu-id="7f59c-131">tooview les actions disponibles et les entrées en pointant sur un document Swagger, utilisez hello [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span><span class="sxs-lookup"><span data-stu-id="7f59c-131">tooview available actions and inputs by pointing at a Swagger document, use hello [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="7f59c-132">toocall toute API, y compris les API qui n’ont ou exposer un document Swagger, vous pouvez toujours créer une demande avec hello [action HTTP](../connectors/connectors-native-http.md).</span><span class="sxs-lookup"><span data-stu-id="7f59c-132">toocall any API, including APIs that don't have or expose a Swagger document, you can always create a request with hello [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-tooyour-custom-api"></a><span data-ttu-id="7f59c-133">Authentifier les API d’appels tooyour personnalisée</span><span class="sxs-lookup"><span data-stu-id="7f59c-133">Authenticate calls tooyour custom API</span></span>

<span data-ttu-id="7f59c-134">Vous pouvez sécuriser les appels tooyour API personnalisée des façons suivantes :</span><span class="sxs-lookup"><span data-stu-id="7f59c-134">You can secure calls tooyour custom API in these ways:</span></span>

* <span data-ttu-id="7f59c-135">[Aucune modification de code](#no-code): protéger votre API avec [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) via hello portail Azure, par conséquent, vous n’avez tooupdate votre code ou redéployer votre API.</span><span class="sxs-lookup"><span data-stu-id="7f59c-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through hello Azure portal, so you don't have tooupdate your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="7f59c-136">Par défaut, d’authentification Azure AD hello que vous activez dans hello portail Azure ne fournit pas d’autorisations affinées.</span><span class="sxs-lookup"><span data-stu-id="7f59c-136">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="7f59c-137">Par exemple, cette authentification verrouille votre toojust API un client spécifique, pas tooa utilisateur ou application.</span><span class="sxs-lookup"><span data-stu-id="7f59c-137">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

* <span data-ttu-id="7f59c-138">[Mise à jour du code de votre API](#update-code) : protégez votre API en appliquant [l’authentification par certificat](#certificate), [l’authentification de base](#basic) ou [l’authentification Azure AD](#azure-ad-code) par le biais du code.</span><span class="sxs-lookup"><span data-stu-id="7f59c-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a><span data-ttu-id="7f59c-139">Authentifier les appels tooyour API sans modifier le code</span><span class="sxs-lookup"><span data-stu-id="7f59c-139">Authenticate calls tooyour API without changing code</span></span>

<span data-ttu-id="7f59c-140">Voici les étapes générales de hello pour cette méthode :</span><span class="sxs-lookup"><span data-stu-id="7f59c-140">Here's hello general steps for this method:</span></span>

1. <span data-ttu-id="7f59c-141">Créez deux [identités d’application Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md) : une pour votre application logique et l’autre pour votre application web (ou application API).</span><span class="sxs-lookup"><span data-stu-id="7f59c-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="7f59c-142">tooauthenticate appelle tooyour API, utilisez des informations d’identification de hello (ID client et secret) pour hello [principal du service](../app-service-api/app-service-api-dotnet-service-principal-auth.md) associé hello identité Azure AD de votre application logique.</span><span class="sxs-lookup"><span data-stu-id="7f59c-142">tooauthenticate calls tooyour API, use hello credentials (client ID and secret) for hello [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with hello Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="7f59c-143">Inclure les ID des applications hello dans votre définition de la logique d’application.</span><span class="sxs-lookup"><span data-stu-id="7f59c-143">Include hello application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="7f59c-144">Partie 1 : Créer une identité d’application Azure AD pour votre application logique</span><span class="sxs-lookup"><span data-stu-id="7f59c-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="7f59c-145">Votre application logique utilise cette tooauthenticate d’identité d’application Azure AD auprès d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f59c-145">Your logic app uses this Azure AD application identity tooauthenticate against Azure AD.</span></span> <span data-ttu-id="7f59c-146">Il vous suffit tooset cette identité une fois pour votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="7f59c-146">You only have tooset up this identity one time for your directory.</span></span> <span data-ttu-id="7f59c-147">Par exemple, vous pouvez choisir toouse hello même identité pour toutes vos applications logique, même si vous pouvez créer des identités uniques pour chaque application logique.</span><span class="sxs-lookup"><span data-stu-id="7f59c-147">For example, you can choose toouse hello same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="7f59c-148">Vous pouvez configurer ces identités Bonjour portail Azure, [portail Azure classic](#app-identity-logic-classic), ou utilisez [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="7f59c-148">You can set up these identities in hello Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="7f59c-149">**Créer l’identité de l’application hello pour votre application logique Bonjour portail Azure**</span><span class="sxs-lookup"><span data-stu-id="7f59c-149">**Create hello application identity for your logic app in hello Azure portal**</span></span>

1. <span data-ttu-id="7f59c-150">Bonjour [portail Azure](https://portal.azure.com "https://portal.azure.com"), choisissez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-150">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="7f59c-151">Confirmez que vous êtes dans hello même répertoire que votre application web ou d’une application API.</span><span class="sxs-lookup"><span data-stu-id="7f59c-151">Confirm that you're in hello same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="7f59c-152">répertoires de tooswitch, cliquez sur votre profil et sélectionnez un autre répertoire.</span><span class="sxs-lookup"><span data-stu-id="7f59c-152">tooswitch directories, click your profile and select another directory.</span></span> <span data-ttu-id="7f59c-153">Vous pouvez également sélectionner **Présentation** > **Changer de répertoire**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="7f59c-154">Dans le menu du répertoire hello, sous **gérer**, choisissez **inscriptions d’application** > **nouvelle inscription de l’application**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-154">On hello directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="7f59c-155">Par défaut, liste des enregistrements de l’application hello affiche toutes les inscriptions d’application dans votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="7f59c-155">By default, hello app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="7f59c-156">Sélectionnez des seules votre application les inscriptions, zone de recherche suivant toohello, tooview **mes applications**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-156">tooview only your app registrations, next toohello search box, select **My apps**.</span></span> 

   ![Créer une inscription d’application](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="7f59c-158">Donnez un nom à votre identité de l’application, laissez **type d’Application** défini trop**application Web / API**, fournir une valeur unique chaîne mise en forme en tant que domaine pour **URL de connexion**, puis choisissez  **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-158">Give your application identity a name, leave **Application type** set too**Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![Indication d’un nom et d’une URL de connexion pour l’identité de l’application](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="7f59c-160">identité d’application Hello que vous avez créé pour votre application logique maintenant s’affiche dans la liste des enregistrements de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="7f59c-160">hello application identity that you created for your logic app now appears in hello app registrations list.</span></span>

   ![Identité d’application pour votre application logique](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="7f59c-162">Dans la liste des enregistrements de l’application hello, sélectionnez votre nouvelle identité de l’application.</span><span class="sxs-lookup"><span data-stu-id="7f59c-162">In hello app registrations list, select your new application identity.</span></span> <span data-ttu-id="7f59c-163">Copiez et enregistrez hello **ID d’Application** toouse comme hello « ID de client » pour votre application de la logique dans la partie 3.</span><span class="sxs-lookup"><span data-stu-id="7f59c-163">Copy and save hello **Application ID** toouse as hello "client ID" for your logic app in Part 3.</span></span>

   ![Copie et enregistrement de l’ID de l’application pour l’application logique](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="7f59c-165">Si vos paramètres d’identité d’application ne sont pas visibles, choisissez **Paramètres** ou **Tous les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="7f59c-166">Sous **Accès d’API**, choisissez **Clés**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="7f59c-167">Sous **Description**, indiquez le nom de votre clé.</span><span class="sxs-lookup"><span data-stu-id="7f59c-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="7f59c-168">Sous **Date d’expiration**, sélectionnez la durée de votre clé.</span><span class="sxs-lookup"><span data-stu-id="7f59c-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="7f59c-169">clé Hello que vous créez joue le rôle de l’identité d’application hello « secret » ou mot de passe pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="7f59c-169">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

   ![Création d’une clé pour l’identité de l’application logique](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="7f59c-171">Dans la barre d’outils de hello, choisissez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-171">On hello toolbar, choose **Save**.</span></span> <span data-ttu-id="7f59c-172">Votre clé apparaît maintenant sous **Valeur**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="7f59c-173">**Assurez-vous que toocopy et enregistrer votre clé de** pour une utilisation ultérieure, car la clé de hello est masqué lorsque vous laissez les lames clé hello.</span><span class="sxs-lookup"><span data-stu-id="7f59c-173">**Make sure toocopy and save your key** for later use because hello key is hidden when you leave hello key blade.</span></span>

   <span data-ttu-id="7f59c-174">Lorsque vous configurez votre application de la logique dans la partie 3, vous spécifiez cette clé comme hello « secret » ou le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7f59c-174">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

   ![Copie et enregistrement de la clé pour une utilisation ultérieure](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="7f59c-176">**Créer l’identité de l’application hello pour votre application logique Bonjour portail Azure classic**</span><span class="sxs-lookup"><span data-stu-id="7f59c-176">**Create hello application identity for your logic app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="7f59c-177">Dans les hello portail Azure classic, choisissez [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="7f59c-177">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="7f59c-178">Sélectionnez hello même répertoire que vous utilisez pour votre application web ou d’une application API.</span><span class="sxs-lookup"><span data-stu-id="7f59c-178">Select hello same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="7f59c-179">Sur hello **Applications** , onglet choisir **ajouter** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="7f59c-179">On hello **Applications** tab, choose **Add** at hello bottom of hello page.</span></span>

4. <span data-ttu-id="7f59c-180">Donnez un nom à votre identité d’application, puis cliquez sur **Suivant** (flèche droite).</span><span class="sxs-lookup"><span data-stu-id="7f59c-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="7f59c-181">Sous **Propriétés de l’application**, indiquez une chaîne unique sous forme de domaine sous **URL de connexion** et **URI ID d’application**, puis choisissez **Terminer** (coche).</span><span class="sxs-lookup"><span data-stu-id="7f59c-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="7f59c-182">Sur hello **configurer** onglet, copiez et enregistrez hello **ID Client** pour votre toouse d’application logique dans la partie 3.</span><span class="sxs-lookup"><span data-stu-id="7f59c-182">On hello **Configure** tab, copy and save hello **Client ID** for your logic app toouse in Part 3.</span></span>

7. <span data-ttu-id="7f59c-183">Sous **clés**, ouvrez hello **sélectionner une durée** liste.</span><span class="sxs-lookup"><span data-stu-id="7f59c-183">Under **Keys**, open hello **Select duration** list.</span></span> <span data-ttu-id="7f59c-184">Sélectionnez la durée de votre clé.</span><span class="sxs-lookup"><span data-stu-id="7f59c-184">Select a duration for your key.</span></span>

   <span data-ttu-id="7f59c-185">clé Hello que vous créez joue le rôle de l’identité d’application hello « secret » ou mot de passe pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="7f59c-185">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="7f59c-186">Au bas de hello de page de hello, choisissez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-186">At hello bottom of hello page, choose **Save**.</span></span> <span data-ttu-id="7f59c-187">Vous pouvez avoir toowait quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="7f59c-187">You might have toowait a few seconds.</span></span>

9. <span data-ttu-id="7f59c-188">Sous **clés**, assurez-vous que toocopy et enregistrer la clé hello qui apparaît à présent.</span><span class="sxs-lookup"><span data-stu-id="7f59c-188">Under **Keys**, make sure toocopy and save hello key that now appears.</span></span> 

   <span data-ttu-id="7f59c-189">Lorsque vous configurez votre application de la logique dans la partie 3, vous spécifiez cette clé comme hello « secret » ou le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7f59c-189">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

<span data-ttu-id="7f59c-190">Pour plus d’informations, découvrez comment trop [configurer votre connexion de Service d’applications application toouse Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7f59c-190">For more information, learn how too [configure your App Service application toouse Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="7f59c-191">**Créer l’identité de l’application hello pour votre application logique dans PowerShell**</span><span class="sxs-lookup"><span data-stu-id="7f59c-191">**Create hello application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="7f59c-192">Vous pouvez effectuer cette tâche par le biais d’Azure Resource Manager avec PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f59c-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="7f59c-193">Dans PowerShell, exécutez ces commandes :</span><span class="sxs-lookup"><span data-stu-id="7f59c-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="7f59c-194">Assurez-vous que toocopy hello **ID client** hello de (GUID de votre client Azure AD), **ID de l’Application**et le mot de passe hello que vous avez utilisé.</span><span class="sxs-lookup"><span data-stu-id="7f59c-194">Make sure toocopy hello **Tenant ID** (GUID for your Azure AD tenant), hello **Application ID**, and hello password that you used.</span></span>

<span data-ttu-id="7f59c-195">Pour plus d’informations, découvrez comment trop [créer un principal de service avec PowerShell tooaccess ressources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="7f59c-195">For more information, learn how too [create a service principal with PowerShell tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="7f59c-196">Partie 2 : Créer une identité d’application Azure AD pour votre application web ou votre application API</span><span class="sxs-lookup"><span data-stu-id="7f59c-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="7f59c-197">Si votre application web ou une application API est déjà déployée, vous pouvez activer l’authentification et créer l’identité de l’application hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7f59c-197">If your web app or API app is already deployed, you can turn on authentication and create hello application identity in hello Azure portal.</span></span> <span data-ttu-id="7f59c-198">Sinon, vous pouvez [activer l’authentification lorsque vous effectuez un déploiement avec un modèle Azure Resource Manager](#authen-deploy).</span><span class="sxs-lookup"><span data-stu-id="7f59c-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="7f59c-199">**Créer l’identité de l’application hello et activer l’authentification Bonjour portail Azure pour les applications déployées**</span><span class="sxs-lookup"><span data-stu-id="7f59c-199">**Create hello application identity and turn on authentication in hello Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="7f59c-200">Bonjour [portail Azure](https://portal.azure.com "https://portal.azure.com"), recherchez et sélectionnez votre application web ou une application API.</span><span class="sxs-lookup"><span data-stu-id="7f59c-200">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="7f59c-201">Sous **Paramètres**, choisissez **Authentification/Autorisation**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="7f59c-202">Sous **Authentification App Service**, activez **l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="7f59c-203">Sous **Fournisseurs d’authentification**, sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![Activer l’authentification](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="7f59c-205">À présent, créez une identité d’application pour votre application web ou votre application API comme indiqué ici.</span><span class="sxs-lookup"><span data-stu-id="7f59c-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="7f59c-206">Sur hello **paramètres Azure Active Directory** panneau, définissez **mode de gestion** trop**Express**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-206">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Express**.</span></span> <span data-ttu-id="7f59c-207">Choisissez **Créer une application AD**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="7f59c-208">Donnez un nom à votre identité d’application, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![Créer une identité d’application pour votre application web ou votre application API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="7f59c-210">Sur hello **l’authentification / panneau d’autorisation**, choisissez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-210">On hello **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="7f59c-211">Vous devez maintenant trouver l’ID de client hello et ID de locataire pour l’identité d’application hello qui est associé à votre application web ou d’une application API.</span><span class="sxs-lookup"><span data-stu-id="7f59c-211">Now you must find hello client ID and tenant ID for hello application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="7f59c-212">Vous utiliserez ces ID dans la partie 3.</span><span class="sxs-lookup"><span data-stu-id="7f59c-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="7f59c-213">Donc continuer avec ces étapes pour hello portail Azure ou [portail Azure classic](#find-id-classic).</span><span class="sxs-lookup"><span data-stu-id="7f59c-213">So continue with these steps for hello Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="7f59c-214">**Rechercher l’ID de client de l’identité de l’application et l’ID de locataire pour votre application web ou d’une application API Bonjour portail Azure**</span><span class="sxs-lookup"><span data-stu-id="7f59c-214">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure portal**</span></span>

1. <span data-ttu-id="7f59c-215">Sous **Fournisseurs d’authentification**, sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   ![Sélectionner « Azure Active Directory »](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="7f59c-217">Sur hello **paramètres Azure Active Directory** panneau, définissez **mode de gestion** trop**avancé**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-217">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Advanced**.</span></span>

3. <span data-ttu-id="7f59c-218">Hello de copie **ID Client**et enregistrez ce GUID pour une utilisation dans la partie 3.</span><span class="sxs-lookup"><span data-stu-id="7f59c-218">Copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="7f59c-219">Si **ID Client** et **Url de l’émetteur** ne s’affichent, essayez d’actualiser hello portail Azure, et répétez l’étape 1.</span><span class="sxs-lookup"><span data-stu-id="7f59c-219">If **Client ID** and **Issuer Url** don't appear, try refreshing hello Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="7f59c-220">Sous **Url de l’émetteur**, copiez et enregistrez simplement hello GUID pour la partie 3.</span><span class="sxs-lookup"><span data-stu-id="7f59c-220">Under **Issuer Url**, copy and save just hello GUID for Part 3.</span></span> <span data-ttu-id="7f59c-221">Vous pouvez également utiliser ce GUID dans le modèle de déploiement de votre application web ou de votre application API si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="7f59c-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="7f59c-222">Ce GUID est celui de votre locataire spécifique (« ID de locataire ») et doit apparaître dans cette URL :`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="7f59c-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="7f59c-223">Sans enregistrer vos modifications, fermez hello **paramètres Azure Active Directory** panneau.</span><span class="sxs-lookup"><span data-stu-id="7f59c-223">Without saving your changes, close hello **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="7f59c-224">**Rechercher l’ID de client de l’identité de l’application et l’ID de locataire pour votre application web ou d’une application API Bonjour portail Azure classic**</span><span class="sxs-lookup"><span data-stu-id="7f59c-224">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="7f59c-225">Dans les hello portail Azure classic, choisissez [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="7f59c-225">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="7f59c-226">Sélectionnez le répertoire hello que vous utilisez pour votre application web ou d’une application API.</span><span class="sxs-lookup"><span data-stu-id="7f59c-226">Select hello directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="7f59c-227">Bonjour **recherche** zone, recherchez et sélectionnez l’identité de l’application hello pour votre application web ou d’une application API.</span><span class="sxs-lookup"><span data-stu-id="7f59c-227">In hello **Search** box, find and select hello application identity for your web app or API app.</span></span>

4. <span data-ttu-id="7f59c-228">Sur hello **configurer** hello de copie, onglet **ID Client**et enregistrez ce GUID pour une utilisation dans la partie 3.</span><span class="sxs-lookup"><span data-stu-id="7f59c-228">On hello **Configure** tab, copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="7f59c-229">Une fois que vous obtenez l’ID de client hello, bas hello hello **configurer** , onglet choisir **afficher les points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-229">After you get hello client ID, at hello bottom of hello **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="7f59c-230">Copier l’URL de hello pour **Document de métadonnées de fédération**et de parcourir les URL toothat.</span><span class="sxs-lookup"><span data-stu-id="7f59c-230">Copy hello URL for **Federation Metadata Document**, and browse toothat URL.</span></span>

7. <span data-ttu-id="7f59c-231">Dans le document de métadonnées hello qui s’ouvre, trouver la racine de hello **EntityDescriptor ID** élément, ce qui a un **entityID** attribut sous cette forme :`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="7f59c-231">In hello metadata document that opens, find hello root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="7f59c-232">Hello GUID dans cet attribut est le GUID de votre locataire spécifique (ID client).</span><span class="sxs-lookup"><span data-stu-id="7f59c-232">hello GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="7f59c-233">Copier l’ID de client hello et enregistrer cet ID pour une utilisation dans la partie 3 et également toouse dans votre application web ou un modèle de déploiement de l’application API, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="7f59c-233">Copy hello tenant ID and save that ID for use in Part 3, and also toouse in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="7f59c-234">Pour plus d’informations, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="7f59c-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="7f59c-235">Authentification utilisateur pour les applications API dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7f59c-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="7f59c-236">Authentification et autorisation dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="7f59c-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="7f59c-237">**Activer l’authentification lorsque vous effectuez un déploiement avec un modèle Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="7f59c-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="7f59c-238">Vous devez toujours créer une identité d’application Azure AD de votre application web ou d’une application API qui diffère d’identité d’application hello pour votre application logique.</span><span class="sxs-lookup"><span data-stu-id="7f59c-238">You must still create an Azure AD application identity for your web app or API app that differs from hello app identity for your logic app.</span></span> <span data-ttu-id="7f59c-239">identité de l’application hello toocreate, hello suivez précédentes étapes dans la partie 2 pour hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7f59c-239">toocreate hello application identity, follow hello previous steps in Part 2 for hello Azure portal.</span></span> <span data-ttu-id="7f59c-240">Vous pouvez également suivre les étapes de hello dans la partie 1 et rendre toouse que votre application web ou l’application API réel `https://{URL}` pour **URL de connexion** et **URI ID d’application**.</span><span class="sxs-lookup"><span data-stu-id="7f59c-240">You can also follow hello steps in Part 1, but make sure toouse your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="7f59c-241">À partir de ces étapes, vous avez toosave client hello ID et l’ID de client pour une utilisation dans le modèle de déploiement de votre application, ainsi que pour la partie 3.</span><span class="sxs-lookup"><span data-stu-id="7f59c-241">From these steps, you have toosave both hello client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="7f59c-242">Lorsque vous créez d’identité de l’application hello Azure AD de votre application web ou d’une application API, vous devez utiliser hello portail Azure ou portail Azure classic, plutôt que PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f59c-242">When you create hello Azure AD application identity for your web app or API app, you must use hello Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="7f59c-243">applet de commande PowerShell Hello ne configurer les autorisations de hello requis toosign des utilisateurs dans un site Web.</span><span class="sxs-lookup"><span data-stu-id="7f59c-243">hello PowerShell commandlet doesn't set up hello required permissions toosign users into a website.</span></span>

<span data-ttu-id="7f59c-244">Une fois que vous obtenez l’ID de client hello et l’ID de client, inclure ces ID comme un subresource de votre application web ou d’une application API dans votre modèle de déploiement :</span><span class="sxs-lookup"><span data-stu-id="7f59c-244">After you get hello client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

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

<span data-ttu-id="7f59c-245">tooautomatically déployer une application web vide et une application logique avec l’authentification Azure Active Directory, [afficher hello complète le modèle ici](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), ou cliquez sur **déployer tooAzure** ici :</span><span class="sxs-lookup"><span data-stu-id="7f59c-245">tooautomatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view hello complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy tooAzure** here:</span></span>

<span data-ttu-id="7f59c-246">[![Déployer tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="7f59c-246">[![Deploy tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a><span data-ttu-id="7f59c-247">Partie 3 : Remplir la section d’autorisation hello dans votre logique d’application</span><span class="sxs-lookup"><span data-stu-id="7f59c-247">Part 3: Populate hello Authorization section in your logic app</span></span>

<span data-ttu-id="7f59c-248">modèle précédent de Hello possède déjà cette section d’autorisation configurée, mais si vous créez directement hello logique application, vous devez inclure la section complète d’autorisation de hello.</span><span class="sxs-lookup"><span data-stu-id="7f59c-248">hello previous template already has this authorization section set up, but if you are directly authoring hello logic app, you must include hello full authorization section.</span></span>

<span data-ttu-id="7f59c-249">Ouvrez votre définition de la logique d’application dans la vue code, accédez toohello **HTTP** section Actions, rechercher hello **autorisation** section et ajoutez cette ligne :</span><span class="sxs-lookup"><span data-stu-id="7f59c-249">Open your logic app definition in code view, go toohello **HTTP** action section, find hello **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="7f59c-250">Élément</span><span class="sxs-lookup"><span data-stu-id="7f59c-250">Element</span></span> | <span data-ttu-id="7f59c-251">Description</span><span class="sxs-lookup"><span data-stu-id="7f59c-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="7f59c-252">locataire</span><span class="sxs-lookup"><span data-stu-id="7f59c-252">tenant</span></span> |<span data-ttu-id="7f59c-253">Hello GUID pour le client de hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f59c-253">hello GUID for hello Azure AD tenant</span></span> |
| <span data-ttu-id="7f59c-254">audience</span><span class="sxs-lookup"><span data-stu-id="7f59c-254">audience</span></span> |<span data-ttu-id="7f59c-255">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="7f59c-255">Required.</span></span> <span data-ttu-id="7f59c-256">Hello GUID pour la ressource cible de hello que vous souhaitez tooaccess - hello des ID de client à partir de l’identité de l’application hello pour votre application web ou d’une application API</span><span class="sxs-lookup"><span data-stu-id="7f59c-256">hello GUID for hello target resource that you want tooaccess - hello client ID from hello application identity for your web app or API app</span></span> |
| <span data-ttu-id="7f59c-257">clientId</span><span class="sxs-lookup"><span data-stu-id="7f59c-257">clientId</span></span> |<span data-ttu-id="7f59c-258">Hello GUID pour le client hello qui demandent l’accès - hello des ID de client à partir de l’identité de l’application hello pour votre application logique</span><span class="sxs-lookup"><span data-stu-id="7f59c-258">hello GUID for hello client requesting access - hello client ID from hello application identity for your logic app</span></span> |
| <span data-ttu-id="7f59c-259">secret</span><span class="sxs-lookup"><span data-stu-id="7f59c-259">secret</span></span> |<span data-ttu-id="7f59c-260">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="7f59c-260">Required.</span></span> <span data-ttu-id="7f59c-261">clé de Hello ou un mot de passe à partir de l’identité de l’application hello pour client hello qui demande le jeton d’accès hello</span><span class="sxs-lookup"><span data-stu-id="7f59c-261">hello key or password from hello application identity for hello client that's requesting hello access token</span></span> |
| <span data-ttu-id="7f59c-262">type</span><span class="sxs-lookup"><span data-stu-id="7f59c-262">type</span></span> |<span data-ttu-id="7f59c-263">type d’authentification Hello.</span><span class="sxs-lookup"><span data-stu-id="7f59c-263">hello authentication type.</span></span> <span data-ttu-id="7f59c-264">Pour l’authentification ActiveDirectoryOAuth, valeur de hello est `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="7f59c-264">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="7f59c-265">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="7f59c-265">For example:</span></span>

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

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="7f59c-266">Sécuriser les appels à l’API avec le code</span><span class="sxs-lookup"><span data-stu-id="7f59c-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="7f59c-267">Authentification par certificat</span><span class="sxs-lookup"><span data-stu-id="7f59c-267">Certificate authentication</span></span>

<span data-ttu-id="7f59c-268">toovalidate hello les demandes entrantes à partir de votre application web de logique application tooyour ou API, vous pouvez utiliser des certificats clients.</span><span class="sxs-lookup"><span data-stu-id="7f59c-268">toovalidate hello incoming requests from your logic app tooyour web app or API app, you can use client certificates.</span></span> <span data-ttu-id="7f59c-269">tooset votre code, en savoir plus [comment l’authentification mutuelle tooconfigure TLS](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span><span class="sxs-lookup"><span data-stu-id="7f59c-269">tooset up your code, learn [how tooconfigure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="7f59c-270">Bonjour **autorisation** section, ajoutez cette ligne :</span><span class="sxs-lookup"><span data-stu-id="7f59c-270">In hello **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="7f59c-271">Élément</span><span class="sxs-lookup"><span data-stu-id="7f59c-271">Element</span></span> | <span data-ttu-id="7f59c-272">Description</span><span class="sxs-lookup"><span data-stu-id="7f59c-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="7f59c-273">type</span><span class="sxs-lookup"><span data-stu-id="7f59c-273">type</span></span> |<span data-ttu-id="7f59c-274">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="7f59c-274">Required.</span></span> <span data-ttu-id="7f59c-275">type d’authentification Hello.</span><span class="sxs-lookup"><span data-stu-id="7f59c-275">hello authentication type.</span></span> <span data-ttu-id="7f59c-276">Pour les certificats clients SSL, la valeur de hello doit être `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="7f59c-276">For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="7f59c-277">password</span><span class="sxs-lookup"><span data-stu-id="7f59c-277">password</span></span> |<span data-ttu-id="7f59c-278">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="7f59c-278">Required.</span></span> <span data-ttu-id="7f59c-279">mot de passe Hello pour accéder au certificat de client hello (fichier PFX)</span><span class="sxs-lookup"><span data-stu-id="7f59c-279">hello password for accessing hello client certificate (PFX file)</span></span> |
| <span data-ttu-id="7f59c-280">pfx</span><span class="sxs-lookup"><span data-stu-id="7f59c-280">pfx</span></span> |<span data-ttu-id="7f59c-281">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="7f59c-281">Required.</span></span> <span data-ttu-id="7f59c-282">Contenu de codée en Base64 du certificat de client hello (fichier PFX)</span><span class="sxs-lookup"><span data-stu-id="7f59c-282">Base64-encoded contents of hello client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="7f59c-283">Authentification de base</span><span class="sxs-lookup"><span data-stu-id="7f59c-283">Basic authentication</span></span>

<span data-ttu-id="7f59c-284">toovalidate les demandes entrantes à partir de votre application web de logique application tooyour ou API, vous pouvez utiliser l’authentification de base, telles qu’un nom d’utilisateur et le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7f59c-284">toovalidate incoming requests from your logic app tooyour web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="7f59c-285">L’authentification de base est un modèle commun, et vous pouvez utiliser cette authentification dans n’importe quel toobuild langage utilisé votre application web ou une application API.</span><span class="sxs-lookup"><span data-stu-id="7f59c-285">Basic authentication is a common pattern, and you can use this authentication in any language used toobuild your web app or API app.</span></span>

<span data-ttu-id="7f59c-286">Bonjour **autorisation** section, ajoutez cette ligne :</span><span class="sxs-lookup"><span data-stu-id="7f59c-286">In hello **Authorization** section, include this line:</span></span>

<span data-ttu-id="7f59c-287">`{"type": "basic", "username": "username", "password": "password"}`.</span><span class="sxs-lookup"><span data-stu-id="7f59c-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="7f59c-288">Élément</span><span class="sxs-lookup"><span data-stu-id="7f59c-288">Element</span></span> | <span data-ttu-id="7f59c-289">Description</span><span class="sxs-lookup"><span data-stu-id="7f59c-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7f59c-290">type</span><span class="sxs-lookup"><span data-stu-id="7f59c-290">type</span></span> |<span data-ttu-id="7f59c-291">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="7f59c-291">Required.</span></span> <span data-ttu-id="7f59c-292">type d’authentification Hello.</span><span class="sxs-lookup"><span data-stu-id="7f59c-292">hello authentication type.</span></span> <span data-ttu-id="7f59c-293">L’authentification de base, la valeur de hello doit être `Basic`.</span><span class="sxs-lookup"><span data-stu-id="7f59c-293">For basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="7f59c-294">username</span><span class="sxs-lookup"><span data-stu-id="7f59c-294">username</span></span> |<span data-ttu-id="7f59c-295">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="7f59c-295">Required.</span></span> <span data-ttu-id="7f59c-296">nom d’utilisateur Hello pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="7f59c-296">hello username for authentication</span></span> |
| <span data-ttu-id="7f59c-297">password</span><span class="sxs-lookup"><span data-stu-id="7f59c-297">password</span></span> |<span data-ttu-id="7f59c-298">Obligatoire.</span><span class="sxs-lookup"><span data-stu-id="7f59c-298">Required.</span></span> <span data-ttu-id="7f59c-299">mot de passe Hello pour l’authentification</span><span class="sxs-lookup"><span data-stu-id="7f59c-299">hello password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="7f59c-300">Authentification Azure Active Directory avec le code</span><span class="sxs-lookup"><span data-stu-id="7f59c-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="7f59c-301">Par défaut, d’authentification Azure AD hello que vous activez dans hello portail Azure ne fournit pas d’autorisations affinées.</span><span class="sxs-lookup"><span data-stu-id="7f59c-301">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="7f59c-302">Par exemple, cette authentification verrouille votre toojust API un client spécifique, pas tooa utilisateur ou application.</span><span class="sxs-lookup"><span data-stu-id="7f59c-302">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

<span data-ttu-id="7f59c-303">application de logique tooyour toorestrict API accès via le code, extrayez en-tête hello qui comporte hello un jeton web JSON (JWT).</span><span class="sxs-lookup"><span data-stu-id="7f59c-303">toorestrict API access tooyour logic app through code, extract hello header that has hello JSON web token (JWT).</span></span> <span data-ttu-id="7f59c-304">Vérifier l’identité de l’appelant hello et rejeter les demandes qui ne correspondent pas.</span><span class="sxs-lookup"><span data-stu-id="7f59c-304">Check hello caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="7f59c-305">Aller plus loin, tooimplement cette authentification entièrement dans votre propre code et pas l’utilisation hello portail Azure, découvrez comment trop [s’authentifier auprès d’Active Directory locale dans votre application Azure](../app-service-web/web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="7f59c-305">Going further, tooimplement this authentication entirely in your own code, and not use hello Azure portal, learn how too [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="7f59c-306">toocreate une identité pour votre application de la logique d’application et utiliser ce toocall identité votre API, vous devez suivre les étapes précédentes hello.</span><span class="sxs-lookup"><span data-stu-id="7f59c-306">toocreate an application identity for your logic app and use that identity toocall your API, you must follow hello previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f59c-307">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7f59c-307">Next steps</span></span>

* [<span data-ttu-id="7f59c-308">Vérifier les performances de l’application logique avec des alertes et des journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="7f59c-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)