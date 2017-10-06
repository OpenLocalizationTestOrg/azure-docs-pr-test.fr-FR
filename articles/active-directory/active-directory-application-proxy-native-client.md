---
title: "applications clientes natives d’aaaPublish - Azure AD | Documents Microsoft"
description: "Décrit comment tooenable native client applications toocommunicate avec tooyour de sécuriser l’accès à distance de connecteur Proxy d’Application Azure AD tooprovide localement les applications."
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
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a><span data-ttu-id="5b43d-103">Comment tooenable native client applications toointeract avec le proxy d’Applications</span><span class="sxs-lookup"><span data-stu-id="5b43d-103">How tooenable native client apps toointeract with proxy Applications</span></span>

<span data-ttu-id="5b43d-104">Dans les applications tooweb addition, Proxy d’Application Azure Active Directory peut également être utilisé toopublish native client applications.</span><span class="sxs-lookup"><span data-stu-id="5b43d-104">In addition tooweb applications, Azure Active Directory Application Proxy can also be used toopublish native client apps.</span></span> <span data-ttu-id="5b43d-105">Les applications clientes natives sont différentes des applications web du fait qu’elles sont installées sur un appareil alors que les applications web sont accessibles via un navigateur.</span><span class="sxs-lookup"><span data-stu-id="5b43d-105">Native client apps differ from web apps because they are installed on a device, while web apps are accessed through a browser.</span></span> 

<span data-ttu-id="5b43d-106">Le proxy d’application prend en charge les applications clientes natives en acceptant les jetons générés par Azure AD qui sont envoyés dans des en-têtes d’autorisation HTTP standard.</span><span class="sxs-lookup"><span data-stu-id="5b43d-106">Application Proxy supports native client apps by accepting Azure AD issued tokens that are sent in standard Authorize HTTP headers.</span></span>

![Relation entre les utilisateurs finaux, Azure Active Directory et les applications publiées](./media/active-directory-application-proxy-native-client/richclientflow.png)

<span data-ttu-id="5b43d-108">Utilisez hello Azure bibliothèque d’authentification Active Directory, qui prend en charge l’authentification et prend en charge de nombreux environnements clients, les applications natives toopublish.</span><span class="sxs-lookup"><span data-stu-id="5b43d-108">Use hello Azure AD Authentication Library, which takes care of authentication and supports many client environments, toopublish native applications.</span></span> <span data-ttu-id="5b43d-109">Le Proxy d’application s’adapte à hello [scénario de tooWeb API Application Native](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="5b43d-109">Application Proxy fits into hello [Native Application tooWeb API scenario](develop/active-directory-authentication-scenarios.md#native-application-to-web-api).</span></span> <span data-ttu-id="5b43d-110">Cet article vous guide tout au long des quatre étapes de hello toopublish une application native avec le Proxy d’Application et hello bibliothèque d’authentification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5b43d-110">This article walks you through hello four steps toopublish a native application with Application Proxy and hello Azure AD Authentication Library.</span></span> 

## <a name="step-1-publish-your-application"></a><span data-ttu-id="5b43d-111">Étape 1 : publier votre application</span><span class="sxs-lookup"><span data-stu-id="5b43d-111">Step 1: Publish your application</span></span>
<span data-ttu-id="5b43d-112">Publier votre application proxy comme vous le feriez pour toute autre application et affecter des utilisateurs tooaccess votre application.</span><span class="sxs-lookup"><span data-stu-id="5b43d-112">Publish your proxy application as you would any other application and assign users tooaccess your application.</span></span> <span data-ttu-id="5b43d-113">Pour plus d'informations, consultez [Publier des applications avec le proxy d'application](active-directory-application-proxy-publish.md).</span><span class="sxs-lookup"><span data-stu-id="5b43d-113">For more information, see [Publish applications with Application Proxy](active-directory-application-proxy-publish.md).</span></span>

## <a name="step-2-configure-your-application"></a><span data-ttu-id="5b43d-114">Étape 2 : configurer votre application</span><span class="sxs-lookup"><span data-stu-id="5b43d-114">Step 2: Configure your application</span></span>
<span data-ttu-id="5b43d-115">Configurez votre application native comme suit :</span><span class="sxs-lookup"><span data-stu-id="5b43d-115">Configure your native application as follows:</span></span>

1. <span data-ttu-id="5b43d-116">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5b43d-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="5b43d-117">Accédez trop**Azure Active Directory** > **inscriptions d’application**.</span><span class="sxs-lookup"><span data-stu-id="5b43d-117">Navigate too**Azure Active Directory** > **App registrations**.</span></span>
3. <span data-ttu-id="5b43d-118">Sélectionnez **Nouvelle inscription d’application**.</span><span class="sxs-lookup"><span data-stu-id="5b43d-118">Select **New application registration**.</span></span>
4. <span data-ttu-id="5b43d-119">Spécifiez un nom pour votre application, sélectionnez **natif** en tant que type d’application hello et fournir hello URI de redirection pour votre application.</span><span class="sxs-lookup"><span data-stu-id="5b43d-119">Specify a name for your application, select **Native** as hello application type, and provide hello Redirect URI for your application.</span></span> 

   ![Créer une nouvelle inscription d’application](./media/active-directory-application-proxy-native-client/create.png)
5. <span data-ttu-id="5b43d-121">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="5b43d-121">Select **Create**.</span></span>

<span data-ttu-id="5b43d-122">Pour plus d’informations sur la création d’une nouvelle inscription d’application, consultez [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md) (Intégration d’applications à Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="5b43d-122">For more detailed information about creating a new app registration, see [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md).</span></span>


## <a name="step-3-grant-access-tooother-applications"></a><span data-ttu-id="5b43d-123">Étape 3 : Applications de tooother accorder l’accès</span><span class="sxs-lookup"><span data-stu-id="5b43d-123">Step 3: Grant access tooother applications</span></span>
<span data-ttu-id="5b43d-124">Permettre aux applications hello application native toobe exposée tooother dans votre répertoire :</span><span class="sxs-lookup"><span data-stu-id="5b43d-124">Enable hello native application toobe exposed tooother applications in your directory:</span></span>

1. <span data-ttu-id="5b43d-125">Toujours dans **inscriptions d’application**, sélectionnez hello nouvelle application native que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="5b43d-125">Still in **App registrations**, select hello new native application that you just created.</span></span>
2. <span data-ttu-id="5b43d-126">Sélectionnez **Autorisations requises**.</span><span class="sxs-lookup"><span data-stu-id="5b43d-126">Select **Required permissions**.</span></span>
3. <span data-ttu-id="5b43d-127">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5b43d-127">Select **Add**.</span></span>
4. <span data-ttu-id="5b43d-128">Première étape de hello ouvert, **sélectionner une API**.</span><span class="sxs-lookup"><span data-stu-id="5b43d-128">Open hello first step, **Select an API**.</span></span>
5. <span data-ttu-id="5b43d-129">Utilisez hello barre toofind hello Proxy d’Application application de recherche que vous avez publiée dans la première section de hello.</span><span class="sxs-lookup"><span data-stu-id="5b43d-129">Use hello search bar toofind hello Application Proxy app that you published in hello first section.</span></span> <span data-ttu-id="5b43d-130">Choisissez cette application, puis cliquez sur **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="5b43d-130">Choose that app, then click **Select**.</span></span> 

   ![Recherche de l’application de proxy hello](./media/active-directory-application-proxy-native-client/select_api.png)
6. <span data-ttu-id="5b43d-132">Deuxième étape de hello ouvert, **sélectionner les autorisations**.</span><span class="sxs-lookup"><span data-stu-id="5b43d-132">Open hello second step, **Select permissions**.</span></span>
7. <span data-ttu-id="5b43d-133">Toogrant de case à cocher hello votre application proxy d’application native accès tooyour, puis cliquez sur **sélectionnez**.</span><span class="sxs-lookup"><span data-stu-id="5b43d-133">Use hello checkbox toogrant your native application access tooyour proxy application, then click **Select**.</span></span>

   ![Application de tooproxy grant access](./media/active-directory-application-proxy-native-client/select_perms.png)
8. <span data-ttu-id="5b43d-135">Sélectionnez **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="5b43d-135">Select **Done**.</span></span>


## <a name="step-4-edit-hello-active-directory-authentication-library"></a><span data-ttu-id="5b43d-136">Étape 4 : Modifier hello bibliothèque d’authentification Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b43d-136">Step 4: Edit hello Active Directory Authentication Library</span></span>
<span data-ttu-id="5b43d-137">Modifier le code de l’application native hello dans le contexte d’authentification hello Hello de tooinclude hello Active Directory Authentication Library (ADAL) après le texte :</span><span class="sxs-lookup"><span data-stu-id="5b43d-137">Edit hello native application code in hello authentication context of hello Active Directory Authentication Library (ADAL) tooinclude hello following text:</span></span>

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

<span data-ttu-id="5b43d-138">variables Hello dans l’exemple de code hello doivent être remplacés comme suit :</span><span class="sxs-lookup"><span data-stu-id="5b43d-138">hello variables in hello sample code should be replaced as follows:</span></span>

* <span data-ttu-id="5b43d-139">**ID de locataire** se trouvent dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5b43d-139">**Tenant ID** can be found in hello Azure portal.</span></span> <span data-ttu-id="5b43d-140">Accédez trop**Azure Active Directory** > **propriétés** et copie Bonjour ID de répertoire.</span><span class="sxs-lookup"><span data-stu-id="5b43d-140">Navigate too**Azure Active Directory** > **Properties** and copy hello Directory ID.</span></span> 
* <span data-ttu-id="5b43d-141">**URL externe** est hello frontal URL est saisie Bonjour Proxy d’Application.</span><span class="sxs-lookup"><span data-stu-id="5b43d-141">**External URL** is hello front-end URL you entered in hello Proxy Application.</span></span> <span data-ttu-id="5b43d-142">toofind cette valeur, accédez toohello **le proxy d’Application** section de l’application de proxy hello.</span><span class="sxs-lookup"><span data-stu-id="5b43d-142">toofind this value, navigate toohello **Application proxy** section of hello proxy app.</span></span>
* <span data-ttu-id="5b43d-143">**ID d’application** Hello application native se trouvent sur hello **propriétés** page de l’application native hello.</span><span class="sxs-lookup"><span data-stu-id="5b43d-143">**App ID** of hello native app can be found on hello **Properties** page of hello native application.</span></span>
* <span data-ttu-id="5b43d-144">**URI de redirection de l’application native hello** se trouvent sur hello **URI de redirection** page de l’application native hello.</span><span class="sxs-lookup"><span data-stu-id="5b43d-144">**Redirect URI of hello native app** can be found on hello **Redirect URIs** page of hello native application.</span></span>


## <a name="see-also"></a><span data-ttu-id="5b43d-145">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="5b43d-145">See also</span></span>

<span data-ttu-id="5b43d-146">Pour plus d’informations sur les flux de l’application native hello, consultez [application Native tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span><span class="sxs-lookup"><span data-stu-id="5b43d-146">For more information about hello native application flow, see [Native application tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)</span></span>

<span data-ttu-id="5b43d-147">Pour les informations les plus récentes hello et mises à jour, consultez hello [blog de Proxy d’Application](http://blogs.technet.com/b/applicationproxyblog/)</span><span class="sxs-lookup"><span data-stu-id="5b43d-147">For hello latest news and updates, check out hello [Application Proxy blog](http://blogs.technet.com/b/applicationproxyblog/)</span></span>
