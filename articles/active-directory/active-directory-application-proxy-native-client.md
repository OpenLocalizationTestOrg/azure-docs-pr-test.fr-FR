---
title: Publier des applications clientes natives - Azure AD | Microsoft Docs
description: "Explique comment activer des applications clientes natives de manière à communiquer avec le connecteur de proxy d'application Azure AD pour fournir un accès à distance sécurisé à vos applications locales."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: bdaa5af6ff5331bc310499586615b48a864c3c5e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-enable-native-client-apps-to-interact-with-proxy-applications"></a><span data-ttu-id="b8e4e-103">Activation d'applications clientes natives de manière à ce qu'elles interagissent avec des applications proxy</span><span class="sxs-lookup"><span data-stu-id="b8e4e-103">How to enable native client apps to interact with proxy Applications</span></span>

<span data-ttu-id="b8e4e-104">En plus des applications web, le proxy d’application Azure Active Directory peut également être utilisé pour publier des applications clientes natives.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-104">In addition to web applications, Azure Active Directory Application Proxy can also be used to publish native client apps.</span></span> <span data-ttu-id="b8e4e-105">Les applications clientes natives sont différentes des applications web du fait qu’elles sont installées sur un appareil alors que les applications web sont accessibles via un navigateur.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="b8e4e-106">Le proxy d’application prend en charge les applications clientes natives en acceptant les jetons générés par Azure AD qui sont envoyés dans des en-têtes d’autorisation HTTP standard.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![Relation entre les utilisateurs finaux, Azure Active Directory et les applications publiées](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="b8e4e-108">Utilisez la bibliothèque Azure AD Authentication, qui prend en charge l’authentification et de nombreux environnements clients, pour publier des applications natives.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-108">Use the Azure AD Authentication Library, which takes care of authentication and supports many client environments, to publish native applications.</span></span> <span data-ttu-id="b8e4e-109">Le proxy d'application est conforme au [scénario Application Native vers API Web](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="b8e4e-109">Application Proxy fits into the [Native Application to Web API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="b8e4e-110">Cet article vous guide dans quatre étapes pour publier une application native avec le proxy d’application et la bibliothèque Azure AD Authentication.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-110">This article walks you through the four steps to publish a native application with Application Proxy and the Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="b8e4e-111">Étape 1 : publier votre application</span><span class="sxs-lookup"><span data-stu-id="b8e4e-111">Step 1: Publish your application</span></span>
<span data-ttu-id="b8e4e-112">Publiez votre application proxy comme vous le feriez pour toute autre application et affectez des utilisateurs pour accéder à votre application.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-112">Publish your proxy application as you would any other application and assign users to access your application.</span></span> <span data-ttu-id="b8e4e-113">Pour plus d'informations, consultez [Publier des applications avec le proxy d'application](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="b8e4e-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="b8e4e-114">Étape 2 : configurer votre application</span><span class="sxs-lookup"><span data-stu-id="b8e4e-114">Step 2: Configure your application</span></span>
<span data-ttu-id="b8e4e-115">Configurez votre application native comme suit :</span><span class="sxs-lookup"><span data-stu-id="b8e4e-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="b8e4e-116">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b8e4e-116">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b8e4e-117">Accédez à **Azure Active Directory** > **Inscriptions d’application**.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-117">Navigate to **Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="b8e4e-118">Sélectionnez **Nouvelle inscription d’application**.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="b8e4e-119">Spécifiez un nom pour votre application, sélectionnez **Natif** comme type d’application et indiquez l’URI de redirection de votre application.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-119">Specify a name for your application, select **Native** as the application type, and provide the Redirect URI for your application.</span></span> 

   ![Créer une nouvelle inscription d’application](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="b8e4e-121">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-121">Select **Create**.</span></span>

<span data-ttu-id="b8e4e-122">Pour plus d’informations sur la création d’une nouvelle inscription d’application, consultez [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md) (Intégration d’applications à Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="b8e4e-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-to-other-applications"></a><span data-ttu-id="b8e4e-123">Étape 3: accorder l’accès à d’autres applications</span><span class="sxs-lookup"><span data-stu-id="b8e4e-123">Step 3: Grant access to other applications</span></span>
<span data-ttu-id="b8e4e-124">Activez l'application native à exposer à d'autres applications dans votre répertoire :</span><span class="sxs-lookup"><span data-stu-id="b8e4e-124">Enable the native application to be exposed to other applications in your directory:</span></span>

1. <span data-ttu-id="b8e4e-125">Toujours dans **Inscriptions d’application**, sélectionnez la nouvelle application native que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-125">Still in **App registrations**, select the new native application that you just created.</span></span>
2. <span data-ttu-id="b8e4e-126">Sélectionnez **Autorisations requises**.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="b8e4e-127">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-127">Select **Add**.</span></span>
4. <span data-ttu-id="b8e4e-128">Ouvrez la première étape, **Sélectionner une API**.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-128">Open the first step, **Select an API**.</span></span>
5. <span data-ttu-id="b8e4e-129">Utilisez la barre de recherche pour retrouver l’application de proxy d’application que vous avez publiée dans la première section.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-129">Use the search bar to find the Application Proxy app that you published in the first section.</span></span> <span data-ttu-id="b8e4e-130">Choisissez cette application, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-130">Choose that app, then click **Select**.</span></span> 

   ![Rechercher l’application de proxy](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="b8e4e-132">Ouvrez la deuxième étape, **Sélectionner les autorisations**.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-132">Open the second step, **Select permissions**.</span></span>
7. <span data-ttu-id="b8e4e-133">Utilisez la case à cocher pour accorder l’accès de votre application native à votre application de proxy, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-133">Use the checkbox to grant your native application access to your proxy application, then click **Select**.</span></span>

   ![Accorder l’accès à l’application de proxy](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="b8e4e-135">Sélectionnez **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-135">Select **Done**.</span></span>


## <a name="step-4-edit-the-active-directory-authentication-library"></a><span data-ttu-id="b8e4e-136">Étape 4 : modifier la bibliothèque d’authentification Active Directory</span><span class="sxs-lookup"><span data-stu-id="b8e4e-136">Step 4: Edit the Active Directory Authentication Library</span></span>
<span data-ttu-id="b8e4e-137">Modifiez le code de l’application native dans le contexte de l’authentification de l’Active Directory Authentication Library (ADAL) de manière à inclure le texte suivant :</span><span class="sxs-lookup"><span data-stu-id="b8e4e-137">Edit the native application code in the authentication context of the Active Directory Authentication Library (ADAL) to include the following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of the Native app>",
        new Uri("<Redirect Uri of the Native App>"),
        PromptBehavior.Never);

//Use the Access Token to access the Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="b8e4e-138">Les variables dans l’exemple de code doivent être remplacées comme suit :</span><span class="sxs-lookup"><span data-stu-id="b8e4e-138">The variables in the sample code should be replaced as follows:</span></span>

* <span data-ttu-id="b8e4e-139">L’**ID de locataire** est indiqué dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-139">**Tenant ID** can be found in the Azure portal.</span></span> <span data-ttu-id="b8e4e-140">Accédez à **Azure Active Directory** > **Propriétés** et copiez l’ID de répertoire.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-140">Navigate to **Azure Active Directory** > **Properties** and copy the Directory ID.</span></span> 
* <span data-ttu-id="b8e4e-141">L’**URL externe** est l’URL frontale que vous avez entrée dans l’application de proxy.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-141">**External URL** is the front-end URL you entered in the Proxy Application.</span></span> <span data-ttu-id="b8e4e-142">Pour retrouver cette valeur, accédez à la section **Proxy d’application** de l’application de proxy.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-142">To find this value, navigate to the **Application proxy** section of the proxy app.</span></span>
* <span data-ttu-id="b8e4e-143">**L’ID d’application** de l’application native est indiqué sur la page **Propriétés** de l’application native.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-143">**App ID** of the native app can be found on the **Properties** page of the native application.</span></span>
* <span data-ttu-id="b8e4e-144">L**URI de redirection de l’application native** est indiqué sur la page **URI de redirection** de l’application native.</span><span class="sxs-lookup"><span data-stu-id="b8e4e-144">**Redirect URI of the native app** can be found on the **Redirect URIs** page of the native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="b8e4e-145">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b8e4e-145">See also</span></span>

<span data-ttu-id="b8e4e-146">Pour plus d’informations sur le flux d’application native, consultez [Application native vers API web](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span><span class="sxs-lookup"><span data-stu-id="b8e4e-146">For more information about the native application flow, see [Native application to web API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="b8e4e-147">Pour les dernières nouvelles et mises à jour, consultez le site [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="b8e4e-147">For the latest news and updates, check out the [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
