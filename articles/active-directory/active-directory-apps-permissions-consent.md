---
title: Applications, autorisations et consentement dans Azure Active Directory | Microsoft Docs
description: "Azure AD Connect intègre vos répertoires locaux à Azure Active Directory. Cela vous permet de tooprovide une identité commune pour les applications Office 365, Azure et SaaS intégrée à Azure AD."
keywords: Introduction tooAzure AD, les applications, ce qui est Azure AD Connect, installer active directory
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
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a><span data-ttu-id="cd104-105">Applications, autorisations et consentement dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd104-105">Apps, permissions, and consent in Azure Active Directory</span></span>
<span data-ttu-id="cd104-106">Dans Azure Active Directory, vous pouvez ajouter le répertoire tooyour des applications.</span><span class="sxs-lookup"><span data-stu-id="cd104-106">Within Azure Active Directory, you can add applications tooyour directory.</span></span>  <span data-ttu-id="cd104-107">les applications Hello peuvent varier en fonction de type hello d’application.</span><span class="sxs-lookup"><span data-stu-id="cd104-107">hello applications can vary depending on hello type of application.</span></span>  <span data-ttu-id="cd104-108">applications tooview dans le portail classique hello, sélectionnez un répertoire et choisir les applications.</span><span class="sxs-lookup"><span data-stu-id="cd104-108">tooview applications in hello classic portal, select a directory and choose applications.</span></span>

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> <span data-ttu-id="cd104-109">Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article.</span><span class="sxs-lookup"><span data-stu-id="cd104-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

## <a name="types-of-apps"></a><span data-ttu-id="cd104-110">Types d’applications</span><span class="sxs-lookup"><span data-stu-id="cd104-110">Types of apps</span></span>

1. <span data-ttu-id="cd104-111">**Applications à locataire unique**</span><span class="sxs-lookup"><span data-stu-id="cd104-111">**Single-tenant apps**</span></span> </br>
    - <span data-ttu-id="cd104-112">**Applications du locataire unique** -communément tooas les applications line of business (LOB).</span><span class="sxs-lookup"><span data-stu-id="cd104-112">**Single-tenant apps** - Often referred tooas line-of-business (LOB) apps.</span></span> <span data-ttu-id="cd104-113">Il s’agit de cas de hello où une personne au sein de votre organisation développe leur propre application et souhaitez que les utilisateurs de hello organisation toobe en mesure de toosign dans toohello application.</span><span class="sxs-lookup"><span data-stu-id="cd104-113">This is hello case where someone within your organization develops their own app, and would like users in hello organization toobe able toosign in toohello app.</span></span>
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - <span data-ttu-id="cd104-114">**Applications du Proxy d’application** - lorsque vous exposez une application locale avec le Proxy d’application Azure AD, une application à locataire unique est enregistrée dans votre client (dans Ajout toohello service de Proxy d’application).</span><span class="sxs-lookup"><span data-stu-id="cd104-114">**App Proxy apps** - When you expose an on-prem application with Azure AD App Proxy, a single-tenant app is registered in your tenant (in addition toohello App Proxy service).</span></span> <span data-ttu-id="cd104-115">Cette application représente votre application locale pour toutes les interactions du cloud (par exemple, l’authentification).</span><span class="sxs-lookup"><span data-stu-id="cd104-115">This app is what represents your on-prem application for all cloud interactions (for example, authentication).</span></span> <span data-ttu-id="cd104-116">(Le proxy d’application nécessite Azure AD Standard ou une version ultérieure.)</span><span class="sxs-lookup"><span data-stu-id="cd104-116">(App Proxy requires Azure AD Basic or higher.)</span></span>


2. <span data-ttu-id="cd104-117">**Applications multi-locataires**</span><span class="sxs-lookup"><span data-stu-id="cd104-117">**Multi-tenant apps**</span></span>
    - <span data-ttu-id="cd104-118">**Applications mutualisées auxquelles d’autres peuvent donner son consentement à** - similaire trop « applications locataire unique qui se développe de votre organisation ».</span><span class="sxs-lookup"><span data-stu-id="cd104-118">**Multi-tenant apps which others can consent to** - similar too“single-tenant apps that your organization develops”.</span></span> <span data-ttu-id="cd104-119">Hello principale différence (en plus de logique hello dans l’application hello lui-même) fait que les utilisateurs à partir d’autres clients peuvent également de consentement tooand toohello application de connexion.</span><span class="sxs-lookup"><span data-stu-id="cd104-119">hello main difference (besides hello logic in hello app itself) is that users from other tenants can also consent tooand sign in toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - <span data-ttu-id="cd104-120">**Applications multi-locataires développées par d’autres personnes, pour lesquelles Contoso peut donner son consentement**</span><span class="sxs-lookup"><span data-stu-id="cd104-120">**Multi-tenant apps others develop, which Contoso can consent to**.</span></span> <span data-ttu-id="cd104-121">(ou « applications consenties », en version courte). Il s’agit d’inconvénient hello des « applications mutualisées que développe de votre organisation ».</span><span class="sxs-lookup"><span data-stu-id="cd104-121">(Or “consented apps”, for short.) This is hello flip side of “multi-tenant apps your organization develops”.</span></span> <span data-ttu-id="cd104-122">Lorsqu’une autre organisation développe une application mutualisée, les utilisateurs de votre organisation peuvent donner son consentement toohello application et connectez-vous à tooit.</span><span class="sxs-lookup"><span data-stu-id="cd104-122">When another organization develops a multi-tenant app, users of your organization can consent toohello app and sign in tooit.</span></span>
    - <span data-ttu-id="cd104-123">**Applications internes Microsoft** : applications représentant des services Microsoft.</span><span class="sxs-lookup"><span data-stu-id="cd104-123">**Microsoft first-party apps** - Apps that represent Microsoft services.</span></span> <span data-ttu-id="cd104-124">Consentement est piloté par le fait de hello que vous vous inscrivez pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="cd104-124">Consent is driven by hello fact that you sign up for hello service.</span></span> <span data-ttu-id="cd104-125">Il est parfois spéciaux UX et la logique pour certaines applications de tiers qui est souvent utilisée lors de l’établissement des stratégies autour de l’accès toohello application.</span><span class="sxs-lookup"><span data-stu-id="cd104-125">There is sometimes special UX and logic for certain first-party apps that is often used when establishing policies around access toohello app.</span></span></br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - <span data-ttu-id="cd104-126">**Les applications pré-intégrées** -applications disponibles dans la galerie d’applications Azure AD, que vous pouvez ajouter de hello tooyour Active tooprovide single sign-on (et dans certains cas, l’approvisionnement) toopopular les applications SaaS.</span><span class="sxs-lookup"><span data-stu-id="cd104-126">**Pre-integrated apps** - Apps available in hello Azure AD App Gallery, which you can add tooyour directory tooprovide single sign-on (and in some cases, provisioning) toopopular SaaS apps.</span></span>
    - <span data-ttu-id="cd104-127">**Authentification unique Azure AD** : authentification unique « réelle ». Concerne les applications qui peuvent être intégrées à Azure AD via un protocole de connexion pris en charge, comme SAML 2.0 ou OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="cd104-127">**Azure AD single sign-on**: “Real” SSO, for apps that can be integrated with Azure AD, through a supported sign-in protocol such as SAML 2.0 or OpenID Connect.</span></span> <span data-ttu-id="cd104-128">Assistant de Hello vous guide tout au long de sa configuration.</span><span class="sxs-lookup"><span data-stu-id="cd104-128">hello wizard walks you through setting it up.</span></span>
    - <span data-ttu-id="cd104-129">**Mot de passe l’authentification unique sur**: Azure AD stocke en toute sécurité les informations d’identification de l’utilisateur hello pour application hello et informations d’identification hello sont « injectées » dans le formulaire de connexion hello par hello extension de navigateur d’accéder à l’application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd104-129">**Password single sign-on**: Azure AD securely stores hello user’s credentials for hello app, and hello credentials are “injected” into hello sign-in form by hello Azure AD App Access browser extension.</span></span> <span data-ttu-id="cd104-130">Également appelée « mise au coffre des mots de passe ».</span><span class="sxs-lookup"><span data-stu-id="cd104-130">Also known as “password vaulting”.</span></span>

## <a name="permissions"></a><span data-ttu-id="cd104-131">Autorisations</span><span class="sxs-lookup"><span data-stu-id="cd104-131">Permissions</span></span>

<span data-ttu-id="cd104-132">Lorsqu’une application est inscrite, utilisateur hello effectuant l’inscription d’une application hello (autrement dit, le développeur hello) définit les autorisations hello application a besoin d’accéder à et les ressources.</span><span class="sxs-lookup"><span data-stu-id="cd104-132">When an app is registered, hello user performing hello app registration (that is, hello developer) defines which permissions hello app needs access to, and which resources.</span></span> <span data-ttu-id="cd104-133">(hello les ressources sont, eux-mêmes, définis en tant que d’autres applications.) Par exemple, un utilisateur de création d’une application de lecture du courrier, indiquerait que leur application requiert l’autorisation de « Accès aux boîtes aux lettres en tant qu’utilisateur connecté hello » hello Bonjour ressource « Office 365 Exchange Online » :</span><span class="sxs-lookup"><span data-stu-id="cd104-133">(hello resources are, themselves, defined as other apps.) For example, someone building a mail reader app, would state that their app requires hello “Access mailboxes as hello signed-in user” permission in hello “Office 365 Exchange Online” resource:</span></span>
    
![](media/active-directory-apps-permissions-consent/apps6.png)

<span data-ttu-id="cd104-134">Dans l’ordre pour une application de (client hello) toorequest certaines autorisations à partir d’une autre application (ressource hello), développeur hello de l’application de ressource hello définit les autorisations de hello qui existent.</span><span class="sxs-lookup"><span data-stu-id="cd104-134">In order for one app (hello client) toorequest a certain permission from another app (hello resource), hello developer of hello resource app defines hello permissions that exist.</span></span> <span data-ttu-id="cd104-135">Dans notre exemple, Microsoft, propriétaire hello de l’application de ressource « Office 365 Exchange Online » hello, ont défini une autorisation nommée « Accès aux boîtes aux lettres en tant qu’utilisateur connecté hello ».</span><span class="sxs-lookup"><span data-stu-id="cd104-135">In our example, Microsoft, hello owner of hello “Office 365 Exchange Online” resource app, have defined a permission named “Access mailboxes as hello signed-in user”.</span></span>

<span data-ttu-id="cd104-136">Lorsque vous définissez des autorisations, le développeur d’application hello doit définir si hello autorisation peut être consentie, ou s’il requiert le consentement de l’administrateur.</span><span class="sxs-lookup"><span data-stu-id="cd104-136">When defining permissions, hello app developer must define if hello permission can be consented to, or if it requires admin consent.</span></span> <span data-ttu-id="cd104-137">Cela permet aux développeurs tooallow utilisateurs tooconsent sur leurs propres tooapps demande des autorisations de faible sensibilité uniquement, mais nécessitent des autorisations d’administrateurs tooconsent toomore sensibles.</span><span class="sxs-lookup"><span data-stu-id="cd104-137">This allows developers tooallow users tooconsent on their own tooapps requesting only low-sensitivity permissions, but require admins tooconsent toomore sensitive permissions.</span></span> <span data-ttu-id="cd104-138">Par exemple, hello application de ressource « Azure Active Directory », a été défini pour les utilisateurs peuvent accepter tooapps, demandant des autorisations limitées en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="cd104-138">For example, hello “Azure Active Directory” resource app, has been defined, so users can consent tooapps, requesting limited read-only permissions.</span></span>  <span data-ttu-id="cd104-139">Toutefois, le consentement de l’administrateur est requis pour les autorisations de lecture complète et toutes les autorisations d’écriture.</span><span class="sxs-lookup"><span data-stu-id="cd104-139">However, admin consent is required for full read permissions, and all write permissions.</span></span>

<span data-ttu-id="cd104-140">Dans la mesure où les clients natifs ne sont pas authentifiés, une application définie comme application cliente native peut seulement demander des autorisations déléguées.</span><span class="sxs-lookup"><span data-stu-id="cd104-140">Because native clients are not authenticated, an app defined as a native client app can only request delegated permissions.</span></span> <span data-ttu-id="cd104-141">Cela signifie qu’il doit toujours y avoir un utilisateur réel impliqué lors de l’obtention d’un jeton.</span><span class="sxs-lookup"><span data-stu-id="cd104-141">This means that there must always be an actual user involved when obtaining a token.</span></span> <span data-ttu-id="cd104-142">Les applications web et les API web (clients confidentiels) doivent toujours s’authentifier auprès d’Azure AD lors de l’obtention d’un jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="cd104-142">Web apps and web APIs (confidential clients), must always authenticate with Azure AD when getting an access token.</span></span> <span data-ttu-id="cd104-143">Ce qui signifie qu’ils ont également la possibilité de hello de demander des autorisations d’application uniquement.</span><span class="sxs-lookup"><span data-stu-id="cd104-143">Meaning they also have hello possibility of requesting app-only permissions.</span></span> <span data-ttu-id="cd104-144">Par exemple, si le service principal de tooanother tooauthenticate a besoin d’un service principal.</span><span class="sxs-lookup"><span data-stu-id="cd104-144">For example, if one back-end service needs tooauthenticate tooanother back-end service.</span></span> <span data-ttu-id="cd104-145">Les applications demandant des autorisations application seule nécessitent toujours le consentement de l’administrateur.</span><span class="sxs-lookup"><span data-stu-id="cd104-145">Applications requesting app-only permissions always require administrator consent.</span></span>

<span data-ttu-id="cd104-146">En résumé :</span><span class="sxs-lookup"><span data-stu-id="cd104-146">Summarizing:</span></span>



- <span data-ttu-id="cd104-147">Une application (client) indique que les autorisations hello dont il a besoin pour d’autres applications (ressources).</span><span class="sxs-lookup"><span data-stu-id="cd104-147">An app (client) states hello permissions it needs for other apps (resources).</span></span>
- <span data-ttu-id="cd104-148">Une application (ressource) indique quelles autorisations sont exposés tooother applications (clients).</span><span class="sxs-lookup"><span data-stu-id="cd104-148">An app (resource) states what permissions are exposed tooother apps (clients).</span></span>
- <span data-ttu-id="cd104-149">Une autorisation peut être une autorisation application seule ou une autorisation déléguée.</span><span class="sxs-lookup"><span data-stu-id="cd104-149">A permission can be an app-only permission, or a delegated permission.</span></span>
- <span data-ttu-id="cd104-150">Une autorisation déléguée peut être marquée comme « autorise le consentement de l’utilisateur », ou « requiert le consentement de l’administrateur ».</span><span class="sxs-lookup"><span data-stu-id="cd104-150">A delegated permission can be marked as “allows user consent”, or “requires admin consent”.</span></span>
- <span data-ttu-id="cd104-151">Une application peut se comporter comme un client (en déclarant qu’il nécessite de ressource d’autorisations tooa), sous la forme d’une ressource (en déclarant les autorisations qu’il expose) ou les deux.</span><span class="sxs-lookup"><span data-stu-id="cd104-151">An app can behave as a client (by declaring that it needs permissions tooa resource), as a resource (by declaring which permissions it exposes), or as both.</span></span>

## <a name="controls"></a><span data-ttu-id="cd104-152">Commandes</span><span class="sxs-lookup"><span data-stu-id="cd104-152">Controls</span></span>

<span data-ttu-id="cd104-153">Hello Voici une liste de contrôles d’administration différents hello disponibles pour tous les ce comportement.</span><span class="sxs-lookup"><span data-stu-id="cd104-153">hello following is a list of hello different admin controls available for all this behavior.</span></span> <span data-ttu-id="cd104-154">admin Hello contrôles accessibles dans le portail classique de hello de configurer sous le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="cd104-154">hello admin controls can be accessed in hello classic portal from configure under hello directory.</span></span>

![](media/active-directory-apps-permissions-consent/apps7.png)

<span data-ttu-id="cd104-155">Bonjour Azure portail, sous **gérer**, **paramètres utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="cd104-155">In hello Azure portal, under **manage**, **user settings**.</span></span>

![](media/active-directory-apps-permissions-consent/apps11.png)



- <span data-ttu-id="cd104-156">Vous pouvez contrôler si les utilisateurs peuvent accepter les tooapps :</span><span class="sxs-lookup"><span data-stu-id="cd104-156">You can control whether users can consent tooapps:</span></span>

<span data-ttu-id="cd104-157">Dans le portail classique de hello, sélectionnez **les utilisateurs peuvent donner des applications autorisations tooaccess leurs données.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span><span class="sxs-lookup"><span data-stu-id="cd104-157">In hello classic portal, select **Users may give applications permissions tooaccess their data.**
![](media/active-directory-apps-permissions-consent/apps8.png)</span></span>

<span data-ttu-id="cd104-158">Bonjour portail Azure, sélectionnez **les utilisateurs peuvent autoriser des applications tooaccess leurs données**.</span><span class="sxs-lookup"><span data-stu-id="cd104-158">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps12.png)



- <span data-ttu-id="cd104-159">Vous pouvez contrôler si les utilisateurs peuvent inscrire leurs propres applications métier de locataire unique : dans, sélectionnez portail classique hello **les utilisateurs peuvent ajouter des applications intégrées.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span><span class="sxs-lookup"><span data-stu-id="cd104-159">You can control whether users can register their own single-tenant LOB apps: In hello classic portal select **Users may add integrated applications.**
![](media/active-directory-apps-permissions-consent/apps9.png)</span></span>

<span data-ttu-id="cd104-160">Bonjour portail Azure, sélectionnez **les utilisateurs peuvent autoriser des applications tooaccess leurs données**.</span><span class="sxs-lookup"><span data-stu-id="cd104-160">In hello Azure portal, select **users can allow apps tooaccess their data**.</span></span>
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
><span data-ttu-id="cd104-161">Même si vous autorisez les utilisateurs des applications métier tooregister locataire unique, il existe des limites toowhat peuvent être inscrits.</span><span class="sxs-lookup"><span data-stu-id="cd104-161">Even if you do allow users tooregister single-tenant LOB apps, there are limits toowhat can be registered.</span></span>  
><span data-ttu-id="cd104-162">Par exemple, les développeurs qui ne sont pas des administrateurs de répertoires.</span><span class="sxs-lookup"><span data-stu-id="cd104-162">For example, developers who are not directory admins.</span></span>
>
>- <span data-ttu-id="cd104-163">Les utilisateurs ne peuvent pas transformer une application à locataire unique en application multi-locataire.</span><span class="sxs-lookup"><span data-stu-id="cd104-163">Users cannot make a single-tenant app a multi-tenant app.</span></span>
>- <span data-ttu-id="cd104-164">Lors de l’inscription des applications métier locataire unique, les utilisateurs ne peuvent pas demander des autorisations d’application uniquement tooother applications.</span><span class="sxs-lookup"><span data-stu-id="cd104-164">When registering single-tenant LOB apps, users cannot request app-only permissions tooother apps.</span></span>
>- <span data-ttu-id="cd104-165">Lors de l’inscription des applications métier locataire unique, les utilisateurs ne peuvent pas demander des autorisations déléguées tooother applications si ces autorisations requièrent le consentement de l’administrateur.</span><span class="sxs-lookup"><span data-stu-id="cd104-165">When registering single-tenant LOB apps, users cannot request delegated permissions tooother apps if those permissions require admin consent.</span></span>
>- <span data-ttu-id="cd104-166">Les utilisateurs ne peuvent pas faire tooapps de modifications qu’ils ne sont pas propriétaires de.</span><span class="sxs-lookup"><span data-stu-id="cd104-166">Users cannot make changes tooapps that they are not owners of.</span></span>



- <span data-ttu-id="cd104-167">Vous pouvez décider si les utilisateurs peuvent eux-mêmes ajouter des applications pré-intégrées qui utilisent l’authentification unique par mot de passe (également appelée « mise au coffre des mots de passe ») ![](media/active-directory-apps-permissions-consent/apps10.png)</span><span class="sxs-lookup"><span data-stu-id="cd104-167">You can control whether users can themselves add pre-integrated apps that use password SSO (aka “password vaulting”) ![](media/active-directory-apps-permissions-consent/apps10.png)</span></span>



- <span data-ttu-id="cd104-168">Vous pouvez contrôler dans quelles conditions les applications sont accessibles (c’est-à-dire, définir un accès conditionnel).</span><span class="sxs-lookup"><span data-stu-id="cd104-168">You can control under which conditions applications can be accessed (that is, conditional access).</span></span> <span data-ttu-id="cd104-169">Sachez que cela s’applique à la fois toohello client application et application de ressource toohello.</span><span class="sxs-lookup"><span data-stu-id="cd104-169">Be aware this applies both toohello client app and toohello resource app.</span></span> <span data-ttu-id="cd104-170">Par conséquent, supposons que vous définissez une stratégie d’accès conditionnel qui indique que cette application « Office 365 Exchange Online » hello est accessible uniquement à partir d’ordinateurs qui sont conformes.</span><span class="sxs-lookup"><span data-stu-id="cd104-170">So, say you set a conditional access policy that says that hello “Office 365 Exchange Online” app can only be accessed from machines, which are compliant.</span></span>  <span data-ttu-id="cd104-171">Cette stratégie sera également entrer en action lorsqu’un utilisateur tente de toouse une application cliente qui demande tooExchange d’autorisations en ligne.</span><span class="sxs-lookup"><span data-stu-id="cd104-171">This policy will also kick in when a user attempts toouse a client app which requests permissions tooExchange Online.</span></span>



- <span data-ttu-id="cd104-172">Vous disposez de visibilité dans lequel les applications ont été consenti tooand celles qui est utilisés.</span><span class="sxs-lookup"><span data-stu-id="cd104-172">You have visibility into which apps have been consented tooand which ones are being used.</span></span>

1.  <span data-ttu-id="cd104-173">Quand un utilisateur a consenti tooan application, un objet de principal du service est créé dans le locataire de hello.</span><span class="sxs-lookup"><span data-stu-id="cd104-173">When a user consents tooan app, a ServicePrincipal object is created in hello tenant.</span></span> <span data-ttu-id="cd104-174">Création de principal du service est incluse dans le rapport d’audit de hello.</span><span class="sxs-lookup"><span data-stu-id="cd104-174">ServicePrincipal creation is included in hello audit report.</span></span>
2.  <span data-ttu-id="cd104-175">Rapports d’activité de connexion utilisateur vous indiquent quels utilisateurs de hello application se connecte à.</span><span class="sxs-lookup"><span data-stu-id="cd104-175">User sign-in activity reports tell you which app hello user is signing in to.</span></span> 

## <a name="example"></a><span data-ttu-id="cd104-176">Exemple</span><span class="sxs-lookup"><span data-stu-id="cd104-176">Example</span></span>

<span data-ttu-id="cd104-177">Par exemple, prenons l’application hello « FabrikamMail pour Office 365 », qui vous avez remarqué des utilisateurs dans votre locataire sont connectent.</span><span class="sxs-lookup"><span data-stu-id="cd104-177">As an example, let’s take hello “FabrikamMail for Office 365” app, which you’ve noticed users in your tenant are signing in to.</span></span> <span data-ttu-id="cd104-178">« FabrikamMail » est une application de lecture de courriers pour Android, publiée par « Fabrikam, Inc. ».</span><span class="sxs-lookup"><span data-stu-id="cd104-178">“FabrikamMail” is a mail reader app for Android, published by “Fabrikam, Inc.”.</span></span> <span data-ttu-id="cd104-179">Cela ne tombe hello « applications mutualisées autres développer, Contoso peut donner son consentement à ».</span><span class="sxs-lookup"><span data-stu-id="cd104-179">This falls into hello “multi-tenant apps other develop, which Contoso can consent to”.</span></span>

<span data-ttu-id="cd104-180">Si les utilisateurs sont autorisés à tooconsent, ils Obtient un Bonjour invite de consentement première fois, qu'ils se connectent :![](media/active-directory-apps-permissions-consent/apps14.png)</span><span class="sxs-lookup"><span data-stu-id="cd104-180">If users are allowed tooconsent, they get a consent prompt hello first time they sign in: ![](media/active-directory-apps-permissions-consent/apps14.png)</span></span>

<span data-ttu-id="cd104-181">« Accéder à vos boîtes aux lettres » est la chaîne de consentement hello orientés utilisateur pour obtenir l’autorisation « Accès aux boîtes aux lettres en tant qu’utilisateur connecté hello » hello exposée par « Office 365 Exchange Online » (autrement dit, Exchange).</span><span class="sxs-lookup"><span data-stu-id="cd104-181">“Access your mailboxes” is hello user-facing consent string for hello “Access mailboxes as hello signed-in user” permission exposed by “Office 365 Exchange Online” (that is, Exchange).</span></span>

<span data-ttu-id="cd104-182">Vous pouvez voir les autorisations hello en recherchant des objets de principal du service hello Exchange (ressource hello), qui a été ajouté lorsque vous vous abonnez à Office 365.</span><span class="sxs-lookup"><span data-stu-id="cd104-182">You can see hello permissions by looking up hello ServicePrincipal object for Exchange (hello resource), which was added when you signed up for Office 365.</span></span> <span data-ttu-id="cd104-183">Vous pouvez considérer d’objet de principal du service hello d’une « instance » de l’application hello dans votre client, qui est utilisé pour enregistrer les configurations et les différentes options.</span><span class="sxs-lookup"><span data-stu-id="cd104-183">You can think of hello ServicePrincipal object of an “instance” of hello app in your tenant, which is used for recording different options and configurations.</span></span>  <span data-ttu-id="cd104-184">Vous pouvez le voir à l’aide de hello `Get-AzureADServicePrincipal` dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd104-184">You can see this by using hello `Get-AzureADServicePrincipal` in PowerShell.</span></span>

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
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
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

<span data-ttu-id="cd104-185">Consentement est lancé lorsque l’utilisateur de hello clique sur « Accepter ».</span><span class="sxs-lookup"><span data-stu-id="cd104-185">Consent is initiated when hello user clicks “Accept”.</span></span> <span data-ttu-id="cd104-186">Tout d’abord, un objet de principal du service pour « FabrikamMail pour Office 365 » est créé dans le locataire de hello.</span><span class="sxs-lookup"><span data-stu-id="cd104-186">First, a ServicePrincipal object for “FabrikamMail for Office 365” is created in hello tenant.</span></span> <span data-ttu-id="cd104-187">Hello principal du service ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="cd104-187">hello ServicePrincipal looks something like this:</span></span>

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

<span data-ttu-id="cd104-188">Terme autorisation tooan application crée un lien Oauth2PermissionGrant entre les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="cd104-188">Consenting tooan app creates an Oauth2PermissionGrant link between hello following:</span></span>
  
- <span data-ttu-id="cd104-189">objet d’utilisateur Hello</span><span class="sxs-lookup"><span data-stu-id="cd104-189">hello user object</span></span>
- <span data-ttu-id="cd104-190">applications clientes Hello ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="cd104-190">hello client apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="cd104-191">applications de ressources Hello ServicePrincipalName (SPN)</span><span class="sxs-lookup"><span data-stu-id="cd104-191">hello resource apps ServicePrincipalName (SPN)</span></span>
- <span data-ttu-id="cd104-192">autorisations dans l’application de ressource hello.</span><span class="sxs-lookup"><span data-stu-id="cd104-192">permissions in hello resource app.</span></span>  

<span data-ttu-id="cd104-193">Dans les cas de hello de FabrikamMail, il ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="cd104-193">In hello case of FabrikamMail, it looks something like this:</span></span>

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

<span data-ttu-id="cd104-194">(**ClientId** est l’ID d’objet principal du FabrikamMail service (hello celui créé uniquement), **PrincipalId** est l’ID d’objet utilisateur hello (de hello utilisateur qui a donné son consentement), **ResourceId**est service d’Exchange ID d’objet principal, l’étendue est l’autorisation hello dans Exchange a consenti à).</span><span class="sxs-lookup"><span data-stu-id="cd104-194">(**ClientId** is FabrikamMail’s service principal object ID (hello one that just got created), **PrincipalId** is hello user object ID (of hello user who consented), **ResourceId** is Exchange’s service principal object ID, Scope is hello permission in Exchange that was consented to).</span></span>

<span data-ttu-id="cd104-195">Si les utilisateurs ne sont pas autorisés tooconsent, ils verront un écran indiquant que cette autorisation est requis.</span><span class="sxs-lookup"><span data-stu-id="cd104-195">If users are not allowed tooconsent, they will see a screen that says that permission is required.</span></span>

