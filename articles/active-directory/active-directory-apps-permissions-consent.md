---
title: Applications, autorisations et consentement dans Azure Active Directory | Microsoft Docs
description: "Azure AD Connect intègre vos répertoires locaux à Azure Active Directory. Cela vous permet de fournir une identité commune pour les applications Office 365, Azure et SaaS intégrées à Azure AD."
keywords: "introduction à Azure AD, applications, présentation d’Azure AD Connect, installation d’active directory"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 6f6baf5e1538fb280a899065c64ca5688473c04a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a><span data-ttu-id="ffb05-105">Applications, autorisations et consentement dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ffb05-105">Apps, permissions, and consent in Azure Active Directory</span></span>
<span data-ttu-id="ffb05-106">Dans Azure Active Directory, vous pouvez ajouter des applications à votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="ffb05-106">Within Azure Active Directory, you can add applications to your directory.</span></span>  <span data-ttu-id="ffb05-107">Les types d’applications peuvent varier.</span><span class="sxs-lookup"><span data-stu-id="ffb05-107">The applications can vary depending on the type of application.</span></span>  <span data-ttu-id="ffb05-108">Pour afficher des applications dans le portail classique, sélectionnez un répertoire et choisissez-en quelques-unes.</span><span class="sxs-lookup"><span data-stu-id="ffb05-108">To view applications in the classic portal, select a directory and choose applications.</span></span>

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> <span data-ttu-id="ffb05-109">Microsoft recommande de gérer Azure AD à l’aide du [Centre d’administration Azure AD](https://aad.portal.azure.com) dans le portail Azure au lieu d’utiliser le portail Azure classique référencé dans cet article.</span><span class="sxs-lookup"><span data-stu-id="ffb05-109">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span>

## <a name="types-of-apps"></a><span data-ttu-id="ffb05-110">Types d’applications</span><span class="sxs-lookup"><span data-stu-id="ffb05-110">Types of apps</span></span>

1. <span data-ttu-id="ffb05-111">**Applications à locataire unique**</span><span class="sxs-lookup"><span data-stu-id="ffb05-111">**Single-tenant apps**</span></span> </br>
    - <span data-ttu-id="ffb05-112">**Applications à locataire unique** : souvent appelées applications métiers.</span><span class="sxs-lookup"><span data-stu-id="ffb05-112">**Single-tenant apps** - Often referred to as line-of-business (LOB) apps.</span></span> <span data-ttu-id="ffb05-113">S’applique lorsqu’une personne de votre organisation développe sa propre application et souhaite que les utilisateurs s’y connectent.</span><span class="sxs-lookup"><span data-stu-id="ffb05-113">This is the case where someone within your organization develops their own app, and would like users in the organization to be able to sign in to the app.</span></span>
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - <span data-ttu-id="ffb05-114">**Applications de proxy d’application** : lorsque vous exposez une application locale avec le proxy d’application Azure AD, une application à locataire unique est inscrite dans votre client (en plus du service de proxy d’application).</span><span class="sxs-lookup"><span data-stu-id="ffb05-114">**App Proxy apps** - When you expose an on-prem application with Azure AD App Proxy, a single-tenant app is registered in your tenant (in addition to the App Proxy service).</span></span> <span data-ttu-id="ffb05-115">Cette application représente votre application locale pour toutes les interactions du cloud (par exemple, l’authentification).</span><span class="sxs-lookup"><span data-stu-id="ffb05-115">This app is what represents your on-prem application for all cloud interactions (for example, authentication).</span></span> <span data-ttu-id="ffb05-116">(Le proxy d’application nécessite Azure AD Standard ou une version ultérieure.)</span><span class="sxs-lookup"><span data-stu-id="ffb05-116">(App Proxy requires Azure AD Basic or higher.)</span></span>


2. <span data-ttu-id="ffb05-117">**Applications multi-locataires**</span><span class="sxs-lookup"><span data-stu-id="ffb05-117">**Multi-tenant apps**</span></span>
    - <span data-ttu-id="ffb05-118">**Applications multi-locataires pour lesquelles d’autres personnes peuvent donner leur consentement** : semblables aux « applications à locataire unique développées par votre organisation ».</span><span class="sxs-lookup"><span data-stu-id="ffb05-118">**Multi-tenant apps which others can consent to** - similar to “single-tenant apps that your organization develops”.</span></span> <span data-ttu-id="ffb05-119">La principale différence (en dehors de la logique de l’application elle-même) est que les utilisateurs d’autres clients peuvent également donner leur consentement et se connecter à l’application.</span><span class="sxs-lookup"><span data-stu-id="ffb05-119">The main difference (besides the logic in the app itself) is that users from other tenants can also consent to and sign in to the app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - <span data-ttu-id="ffb05-120">**Applications multi-locataires développées par d’autres personnes, pour lesquelles Contoso peut donner son consentement**</span><span class="sxs-lookup"><span data-stu-id="ffb05-120">**Multi-tenant apps others develop, which Contoso can consent to**.</span></span> <span data-ttu-id="ffb05-121">(ou « applications consenties », en version courte). C’est l’autre face des « applications multi-locataires développées par votre organisation ».</span><span class="sxs-lookup"><span data-stu-id="ffb05-121">(Or “consented apps”, for short.) This is the flip side of “multi-tenant apps your organization develops”.</span></span> <span data-ttu-id="ffb05-122">Lorsqu’une autre organisation développe une application multi-locataire, les utilisateurs de votre organisation peuvent donner leur consentement pour cette application et s’y connecter.</span><span class="sxs-lookup"><span data-stu-id="ffb05-122">When another organization develops a multi-tenant app, users of your organization can consent to the app and sign in to it.</span></span>
    - <span data-ttu-id="ffb05-123">**Applications internes Microsoft** : applications représentant des services Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ffb05-123">**Microsoft first-party apps** - Apps that represent Microsoft services.</span></span> <span data-ttu-id="ffb05-124">Le consentement se produit lorsque vous vous inscrivez au service.</span><span class="sxs-lookup"><span data-stu-id="ffb05-124">Consent is driven by the fact that you sign up for the service.</span></span> <span data-ttu-id="ffb05-125">Des expériences utilisateur et logiques spécifiques sont parfois utilisées pour les applications internes lors de l’établissement des stratégies relatives à l’accès aux applications.</span><span class="sxs-lookup"><span data-stu-id="ffb05-125">There is sometimes special UX and logic for certain first-party apps that is often used when establishing policies around access to the app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - <span data-ttu-id="ffb05-126">**Applications pré-intégrées** : applications disponibles dans la galerie d’applications Azure AD. Vous pouvez les ajouter à votre répertoire pour permettre l’authentification unique (et dans certains cas, l’approvisionnement) sur les applications SaaS.</span><span class="sxs-lookup"><span data-stu-id="ffb05-126">**Pre-integrated apps** - Apps available in the Azure AD App Gallery, which you can add to your directory to provide single sign-on (and in some cases, provisioning) to popular SaaS apps.</span></span>
    - <span data-ttu-id="ffb05-127">**Authentification unique Azure AD** : authentification unique « réelle ». Concerne les applications qui peuvent être intégrées à Azure AD via un protocole de connexion pris en charge, comme SAML 2.0 ou OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="ffb05-127">**Azure AD single sign-on**: “Real” SSO, for apps that can be integrated with Azure AD, through a supported sign-in protocol such as SAML 2.0 or OpenID Connect.</span></span> <span data-ttu-id="ffb05-128">L’Assistant vous guide tout au long du processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="ffb05-128">The wizard walks you through setting it up.</span></span>
    - <span data-ttu-id="ffb05-129">**Authentification unique par mot de passe** : Azure AD stocke en toute sécurité les informations d’identification de l’utilisateur pour l’application. Ces informations d’identification sont « injectées » dans le formulaire d’inscription par l’extension de navigateur d’accès aux applications Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ffb05-129">**Password single sign-on**: Azure AD securely stores the user’s credentials for the app, and the credentials are “injected” into the sign-in form by the Azure AD App Access browser extension.</span></span> <span data-ttu-id="ffb05-130">Également appelée « mise au coffre des mots de passe ».</span><span class="sxs-lookup"><span data-stu-id="ffb05-130">Also known as “password vaulting”.</span></span>

## <a name="permissions"></a><span data-ttu-id="ffb05-131">Autorisations</span><span class="sxs-lookup"><span data-stu-id="ffb05-131">Permissions</span></span>

<span data-ttu-id="ffb05-132">Quand une application est inscrite, l’utilisateur qui procède à l’inscription de l’application (c’est-à-dire, le développeur) définit les autorisations auxquelles l’application doit accéder, ainsi que les ressources</span><span class="sxs-lookup"><span data-stu-id="ffb05-132">When an app is registered, the user performing the app registration (that is, the developer) defines which permissions the app needs access to, and which resources.</span></span> <span data-ttu-id="ffb05-133">(les ressources sont, elles-mêmes, définies en tant qu’autres applications). Par exemple, un utilisateur créant une application de lecture de courriers va indiquer que son application exige l’autorisation « Accéder aux boîtes aux lettres en tant qu’utilisateur connecté » dans la ressource « Office 365 Exchange Online » :</span><span class="sxs-lookup"><span data-stu-id="ffb05-133">(The resources are, themselves, defined as other apps.) For example, someone building a mail reader app, would state that their app requires the “Access mailboxes as the signed-in user” permission in the “Office 365 Exchange Online” resource:</span></span>
    
![](media/active-directory-apps-permissions-consent/apps6.png)

<span data-ttu-id="ffb05-134">Pour qu’une application (le client) demande une autorisation spécifique à partir d’une autre application (la ressource), le développeur de l’application de ressource définit les autorisations existantes.</span><span class="sxs-lookup"><span data-stu-id="ffb05-134">In order for one app (the client) to request a certain permission from another app (the resource), the developer of the resource app defines the permissions that exist.</span></span> <span data-ttu-id="ffb05-135">Dans notre exemple, le propriétaire de l’application de ressource « Office 365 Exchange Online », Microsoft, a défini une autorisation nommée « Accéder aux boîtes aux lettres en tant qu’utilisateur connecté ».</span><span class="sxs-lookup"><span data-stu-id="ffb05-135">In our example, Microsoft, the owner of the “Office 365 Exchange Online” resource app, have defined a permission named “Access mailboxes as the signed-in user”.</span></span>

<span data-ttu-id="ffb05-136">Lorsque le développeur de l’application définit des autorisations, il doit spécifier si l’autorisation peut être consentie, ou si le consentement de l’administrateur est requis.</span><span class="sxs-lookup"><span data-stu-id="ffb05-136">When defining permissions, the app developer must define if the permission can be consented to, or if it requires admin consent.</span></span> <span data-ttu-id="ffb05-137">Ainsi, les développeurs peuvent autoriser les utilisateurs à donner eux-mêmes leur consentement pour les applications exigeant uniquement des autorisations peu sensibles. Ils peuvent aussi exiger que les administrateurs donnent leur consentement pour des autorisations plus sensibles.</span><span class="sxs-lookup"><span data-stu-id="ffb05-137">This allows developers to allow users to consent on their own to apps requesting only low-sensitivity permissions, but require admins to consent to more sensitive permissions.</span></span> <span data-ttu-id="ffb05-138">Par exemple, l’application de ressource « Azure Active Directory » a été définie pour que les utilisateurs puissent consentir aux applications, en demandant des autorisations de lecture seule limitées.</span><span class="sxs-lookup"><span data-stu-id="ffb05-138">For example, the “Azure Active Directory” resource app, has been defined, so users can consent to apps, requesting limited read-only permissions.</span></span>  <span data-ttu-id="ffb05-139">Toutefois, le consentement de l’administrateur est requis pour les autorisations de lecture complète et toutes les autorisations d’écriture.</span><span class="sxs-lookup"><span data-stu-id="ffb05-139">However, admin consent is required for full read permissions, and all write permissions.</span></span>

<span data-ttu-id="ffb05-140">Dans la mesure où les clients natifs ne sont pas authentifiés, une application définie comme application cliente native peut seulement demander des autorisations déléguées.</span><span class="sxs-lookup"><span data-stu-id="ffb05-140">Because native clients are not authenticated, an app defined as a native client app can only request delegated permissions.</span></span> <span data-ttu-id="ffb05-141">Cela signifie qu’il doit toujours y avoir un utilisateur réel impliqué lors de l’obtention d’un jeton.</span><span class="sxs-lookup"><span data-stu-id="ffb05-141">This means that there must always be an actual user involved when obtaining a token.</span></span> <span data-ttu-id="ffb05-142">Les applications web et les API web (clients confidentiels) doivent toujours s’authentifier auprès d’Azure AD lors de l’obtention d’un jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="ffb05-142">Web apps and web APIs (confidential clients), must always authenticate with Azure AD when getting an access token.</span></span> <span data-ttu-id="ffb05-143">Ce qui signifie qu’elles ont également la possibilité de demander des autorisations application seule.</span><span class="sxs-lookup"><span data-stu-id="ffb05-143">Meaning they also have the possibility of requesting app-only permissions.</span></span> <span data-ttu-id="ffb05-144">Par exemple, un service principal peut être obligé de s’authentifier auprès d’un autre service principal.</span><span class="sxs-lookup"><span data-stu-id="ffb05-144">For example, if one back-end service needs to authenticate to another back-end service.</span></span> <span data-ttu-id="ffb05-145">Les applications demandant des autorisations application seule nécessitent toujours le consentement de l’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ffb05-145">Applications requesting app-only permissions always require administrator consent.</span></span>

<span data-ttu-id="ffb05-146">En résumé :</span><span class="sxs-lookup"><span data-stu-id="ffb05-146">Summarizing:</span></span>



- <span data-ttu-id="ffb05-147">Une application (cliente) indique les autorisations dont elle a besoin pour les autres applications (ressources).</span><span class="sxs-lookup"><span data-stu-id="ffb05-147">An app (client) states the permissions it needs for other apps (resources).</span></span>
- <span data-ttu-id="ffb05-148">Une application (ressource) indique quelles autorisations sont exposées à d’autres applications (clientes).</span><span class="sxs-lookup"><span data-stu-id="ffb05-148">An app (resource) states what permissions are exposed to other apps (clients).</span></span>
- <span data-ttu-id="ffb05-149">Une autorisation peut être une autorisation application seule ou une autorisation déléguée.</span><span class="sxs-lookup"><span data-stu-id="ffb05-149">A permission can be an app-only permission, or a delegated permission.</span></span>
- <span data-ttu-id="ffb05-150">Une autorisation déléguée peut être marquée comme « autorise le consentement de l’utilisateur », ou « requiert le consentement de l’administrateur ».</span><span class="sxs-lookup"><span data-stu-id="ffb05-150">A delegated permission can be marked as “allows user consent”, or “requires admin consent”.</span></span>
- <span data-ttu-id="ffb05-151">Une application peut se comporter comme un client (en déclarant qu’elle a besoin d’autorisations pour une ressource), comme une ressource (en déclarant quelles autorisations sont exposées) ou les deux.</span><span class="sxs-lookup"><span data-stu-id="ffb05-151">An app can behave as a client (by declaring that it needs permissions to a resource), as a resource (by declaring which permissions it exposes), or as both.</span></span>

## <a name="controls"></a><span data-ttu-id="ffb05-152">Commandes</span><span class="sxs-lookup"><span data-stu-id="ffb05-152">Controls</span></span>

<span data-ttu-id="ffb05-153">Voici une liste des différents contrôles d’administration disponibles pour tous ces comportements.</span><span class="sxs-lookup"><span data-stu-id="ffb05-153">The following is a list of the different admin controls available for all this behavior.</span></span> <span data-ttu-id="ffb05-154">Les contrôles d’administration sont accessibles dans le portail classique via Configure (Configurer) sous le répertoire.</span><span class="sxs-lookup"><span data-stu-id="ffb05-154">The admin controls can be accessed in the classic portal from configure under the directory.</span></span>

![](media/active-directory-apps-permissions-consent/apps7.png)

<span data-ttu-id="ffb05-155">Dans le portail Azure, sous **manage** (gérer), choisissez **user settings** (paramètres utilisateur).</span><span class="sxs-lookup"><span data-stu-id="ffb05-155">In the Azure portal, under **manage**, **user settings**.</span></span>

![](media/active-directory-apps-permissions-consent/apps11.png)



- <span data-ttu-id="ffb05-156">Vous pouvez décider si les utilisateurs peuvent donner leur consentement pour des applications :</span><span class="sxs-lookup"><span data-stu-id="ffb05-156">You can control whether users can consent to apps:</span></span>

<span data-ttu-id="ffb05-157">Dans le portail classique, sélectionnez **Users may give applications permissions to access their data**
![](media/active-directory-apps-permissions-consent/apps8.png) (Les utilisateurs peuvent autoriser les applications à accéder à leurs données).</span><span class="sxs-lookup"><span data-stu-id="ffb05-157">In the classic portal, select **Users may give applications permissions to access their data.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span></span>

<span data-ttu-id="ffb05-158">Dans le portail Azure, sélectionnez **Les utilisateurs peuvent autoriser les applications à accéder à leurs données**.</span><span class="sxs-lookup"><span data-stu-id="ffb05-158">In the Azure portal, select **users can allow apps to access their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps12.png)



- <span data-ttu-id="ffb05-159">Vous décider si les utilisateurs peuvent inscrire leurs propres applications métiers à locataire unique : dans le portail classique, sélectionnez **Les utilisateurs peuvent ajouter des applications intégrées**
![](media/active-directory-apps-permissions-consent/apps9.png).</span><span class="sxs-lookup"><span data-stu-id="ffb05-159">You can control whether users can register their own single-tenant LOB apps: In the classic portal select **Users may add integrated applications.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span></span>

<span data-ttu-id="ffb05-160">Dans le portail Azure, sélectionnez **Les utilisateurs peuvent autoriser les applications à accéder à leurs données**.</span><span class="sxs-lookup"><span data-stu-id="ffb05-160">In the Azure portal, select **users can allow apps to access their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
><span data-ttu-id="ffb05-161">Même si vous n’autorisez pas les utilisateurs à inscrire des applications métiers à locataire unique, les applications pouvant être inscrites sont limitées.</span><span class="sxs-lookup"><span data-stu-id="ffb05-161">Even if you do allow users to register single-tenant LOB apps, there are limits to what can be registered.</span></span>  
><span data-ttu-id="ffb05-162">Par exemple, les développeurs qui ne sont pas des administrateurs de répertoires.</span><span class="sxs-lookup"><span data-stu-id="ffb05-162">For example, developers who are not directory admins.</span></span>
>
>- <span data-ttu-id="ffb05-163">Les utilisateurs ne peuvent pas transformer une application à locataire unique en application multi-locataire.</span><span class="sxs-lookup"><span data-stu-id="ffb05-163">Users cannot make a single-tenant app a multi-tenant app.</span></span>
>- <span data-ttu-id="ffb05-164">Lorsque vous inscrivez des applications métiers à locataire unique, les utilisateurs ne peuvent pas demander d’autorisations application seule à d’autres applications.</span><span class="sxs-lookup"><span data-stu-id="ffb05-164">When registering single-tenant LOB apps, users cannot request app-only permissions to other apps.</span></span>
>- <span data-ttu-id="ffb05-165">Lorsque vous inscrivez des applications métiers à locataire unique, les utilisateurs ne peuvent pas demander d’autorisations déléguées à d’autres applications si ces autorisations nécessitent le consentement de l’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ffb05-165">When registering single-tenant LOB apps, users cannot request delegated permissions to other apps if those permissions require admin consent.</span></span>
>- <span data-ttu-id="ffb05-166">Les utilisateurs ne peuvent pas apporter de modifications aux applications dont ils sont propriétaires.</span><span class="sxs-lookup"><span data-stu-id="ffb05-166">Users cannot make changes to apps that they are not owners of.</span></span>



- <span data-ttu-id="ffb05-167">Vous pouvez décider si les utilisateurs peuvent eux-mêmes ajouter des applications pré-intégrées qui utilisent l’authentification unique par mot de passe (également appelée « mise au coffre des mots de passe ») ![](media/active-directory-apps-permissions-consent/apps10.png)</span><span class="sxs-lookup"><span data-stu-id="ffb05-167">You can control whether users can themselves add pre-integrated apps that use password SSO (aka “password vaulting”) ![](media/active-directory-apps-permissions-consent/apps10.png)</span></span>



- <span data-ttu-id="ffb05-168">Vous pouvez contrôler dans quelles conditions les applications sont accessibles (c’est-à-dire, définir un accès conditionnel).</span><span class="sxs-lookup"><span data-stu-id="ffb05-168">You can control under which conditions applications can be accessed (that is, conditional access).</span></span> <span data-ttu-id="ffb05-169">Notez que cela s’applique à l’application cliente et à l’application de ressource.</span><span class="sxs-lookup"><span data-stu-id="ffb05-169">Be aware this applies both to the client app and to the resource app.</span></span> <span data-ttu-id="ffb05-170">Supposons que vous définissez une stratégie d’accès conditionnel spécifiant que l’application « Office 365 Exchange Online » est accessible seulement à partir des machines qui sont compatibles.</span><span class="sxs-lookup"><span data-stu-id="ffb05-170">So, say you set a conditional access policy that says that the “Office 365 Exchange Online” app can only be accessed from machines, which are compliant.</span></span>  <span data-ttu-id="ffb05-171">Cette stratégie s’applique également si un utilisateur tente d’utiliser une application cliente qui demande des autorisations à Exchange Online.</span><span class="sxs-lookup"><span data-stu-id="ffb05-171">This policy will also kick in when a user attempts to use a client app which requests permissions to Exchange Online.</span></span>



- <span data-ttu-id="ffb05-172">Vous avez une vue des applications qui ont été consenties et de celles qui sont utilisées.</span><span class="sxs-lookup"><span data-stu-id="ffb05-172">You have visibility into which apps have been consented to and which ones are being used.</span></span>

1.  <span data-ttu-id="ffb05-173">Lorsqu’un utilisateur donne son consentement pour une application, un objet ServicePrincipal est créé dans le client.</span><span class="sxs-lookup"><span data-stu-id="ffb05-173">When a user consents to an app, a ServicePrincipal object is created in the tenant.</span></span> <span data-ttu-id="ffb05-174">La création de ServicePrincipal est incluse dans le rapport d’audit.</span><span class="sxs-lookup"><span data-stu-id="ffb05-174">ServicePrincipal creation is included in the audit report.</span></span>
2.  <span data-ttu-id="ffb05-175">Les rapports d’activité de connexion de l’utilisateur vous indiquent à quelle application l’utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="ffb05-175">User sign-in activity reports tell you which app the user is signing in to.</span></span> 

## <a name="example"></a><span data-ttu-id="ffb05-176">Exemple</span><span class="sxs-lookup"><span data-stu-id="ffb05-176">Example</span></span>

<span data-ttu-id="ffb05-177">Par exemple, prenons l’application « FabrikamMail pour Office 365 » à laquelle vous avez remarqué que les utilisateurs de votre client se connectent.</span><span class="sxs-lookup"><span data-stu-id="ffb05-177">As an example, let’s take the “FabrikamMail for Office 365” app, which you’ve noticed users in your tenant are signing in to.</span></span> <span data-ttu-id="ffb05-178">« FabrikamMail » est une application de lecture de courriers pour Android, publiée par « Fabrikam, Inc. ».</span><span class="sxs-lookup"><span data-stu-id="ffb05-178">“FabrikamMail” is a mail reader app for Android, published by “Fabrikam, Inc.”.</span></span> <span data-ttu-id="ffb05-179">Elle correspond à la définition « Applications multi-locataires développées par d’autres personnes, pour lesquelles Contoso peut donner son consentement ».</span><span class="sxs-lookup"><span data-stu-id="ffb05-179">This falls into the “multi-tenant apps other develop, which Contoso can consent to”.</span></span>

<span data-ttu-id="ffb05-180">Si les utilisateurs sont autorisés à donner leur consentement, ils sont invités à donner leur consentement la première fois qu’ils se connectent : ![](media/active-directory-apps-permissions-consent/apps14.png)</span><span class="sxs-lookup"><span data-stu-id="ffb05-180">If users are allowed to consent, they get a consent prompt the first time they sign in: ![](media/active-directory-apps-permissions-consent/apps14.png)</span></span>

<span data-ttu-id="ffb05-181">« Accéder à vos boîtes aux lettres » est la chaîne de consentement proposée à l’utilisateur pour l’autorisation « Accéder aux boîtes aux lettres en tant qu’utilisateur connecté » exposée par « Office 365 Exchange Online » (autrement dit, Exchange).</span><span class="sxs-lookup"><span data-stu-id="ffb05-181">“Access your mailboxes” is the user-facing consent string for the “Access mailboxes as the signed-in user” permission exposed by “Office 365 Exchange Online” (that is, Exchange).</span></span>

<span data-ttu-id="ffb05-182">Vous pouvez afficher les autorisations en recherchant l’objet ServicePrincipal pour Exchange (la ressource), qui a été ajouté lors de votre abonnement à Office 365.</span><span class="sxs-lookup"><span data-stu-id="ffb05-182">You can see the permissions by looking up the ServicePrincipal object for Exchange (the resource), which was added when you signed up for Office 365.</span></span> <span data-ttu-id="ffb05-183">Vous pouvez considérer l’objet ServicePrincipal comme une « instance » de l’application dans votre client, utilisée pour enregistrer les différentes options et configurations.</span><span class="sxs-lookup"><span data-stu-id="ffb05-183">You can think of the ServicePrincipal object of an “instance” of the app in your tenant, which is used for recording different options and configurations.</span></span>  <span data-ttu-id="ffb05-184">Vous pouvez le voir en utilisant `Get-AzureADServicePrincipal` dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ffb05-184">You can see this by using the `Get-AzureADServicePrincipal` in PowerShell.</span></span>

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows the app to have the same access to mailboxes as the signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as the signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows the app full access to your mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

<span data-ttu-id="ffb05-185">Le consentement est initié lorsque l’utilisateur clique sur « Accepter ».</span><span class="sxs-lookup"><span data-stu-id="ffb05-185">Consent is initiated when the user clicks “Accept”.</span></span> <span data-ttu-id="ffb05-186">Tout d’abord, un objet ServicePrincipal pour « FabrikamMail pour Office 365 » est créé dans le client.</span><span class="sxs-lookup"><span data-stu-id="ffb05-186">First, a ServicePrincipal object for “FabrikamMail for Office 365” is created in the tenant.</span></span> <span data-ttu-id="ffb05-187">L’objet ServicePrincipal ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ffb05-187">The ServicePrincipal looks something like this:</span></span>

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

<span data-ttu-id="ffb05-188">Le fait de donner un consentement pour une application crée un lien Oauth2PermissionGrant entre les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ffb05-188">Consenting to an app creates an Oauth2PermissionGrant link between the following:</span></span>
  
- <span data-ttu-id="ffb05-189">l’objet utilisateur</span><span class="sxs-lookup"><span data-stu-id="ffb05-189">the user object</span></span>
- <span data-ttu-id="ffb05-190">les applications clientes ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="ffb05-190">the client apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="ffb05-191">les applications de ressource ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="ffb05-191">the resource apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="ffb05-192">les autorisations dans l’application de ressource.</span><span class="sxs-lookup"><span data-stu-id="ffb05-192">permissions in the resource app.</span></span>  

<span data-ttu-id="ffb05-193">Dans le cas de FabrikamMail, cela ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ffb05-193">In the case of FabrikamMail, it looks something like this:</span></span>

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

<span data-ttu-id="ffb05-194">(**ClientId** est l’ID de l’objet principal du service de FabrikamMail (celui qui vient d’être créé), **PrincipalId** est l’ID de l’objet utilisateur (de l’utilisateur qui a donné son consentement), **ResourceId** est l’ID de l’objet principal du service d’Exchange, Scope est l’autorisation dans Exchange qui a été consentie).</span><span class="sxs-lookup"><span data-stu-id="ffb05-194">(**ClientId** is FabrikamMail’s service principal object ID (the one that just got created), **PrincipalId** is the user object ID (of the user who consented), **ResourceId** is Exchange’s service principal object ID, Scope is the permission in Exchange that was consented to).</span></span>

<span data-ttu-id="ffb05-195">Si les utilisateurs ne sont pas autorisés à donner leur consentement, ils verront un écran indiquant qu’une autorisation est requise.</span><span class="sxs-lookup"><span data-stu-id="ffb05-195">If users are not allowed to consent, they will see a screen that says that permission is required.</span></span>

