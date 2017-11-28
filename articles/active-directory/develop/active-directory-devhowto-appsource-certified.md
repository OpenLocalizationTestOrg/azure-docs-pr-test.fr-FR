---
title: Comment obtenir une certification AppSource pour Azure Active Directory | Microsoft Docs
description: "Plus d’informations sur l’obtention de votre application AppSource certifié pour Azure Active Directory."
services: active-directory
documentationcenter: 
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 21206407-49f8-4c0b-84d1-c25e17cd4183
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/03/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: d8e2f8fc19ff879e6a7b632f033fd0ed9d77392a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-get-appsource-certified-for-azure-active-directory"></a><span data-ttu-id="54368-103">Comment obtenir une certification AppSource pour Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="54368-103">How to get AppSource Certified for Azure Active Directory</span></span>
<span data-ttu-id="54368-104">[Microsoft AppSource](https://appsource.microsoft.com/) est une destination pour les utilisateurs professionnels permettant de découvrir, d’essayer et de gérer des applications SaaS métier (applications SaaS autonomes et module complémentaire pour des produits SaaS Microsoft existant).</span><span class="sxs-lookup"><span data-stu-id="54368-104">[Microsoft AppSource](https://appsource.microsoft.com/) is a destination for business users to discover, try, and manage line-of-business SaaS applications (standalone SaaS and add-on to existing Microsoft SaaS products).</span></span>

<span data-ttu-id="54368-105">Pour répertorier une application SaaS autonome sur AppSource, votre application doit accepter l’authentification unique des comptes professionnels d’une société ou d’une organisation qui dispose d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="54368-105">To list a standalone SaaS application on AppSource, your application must accept single sign-on from work accounts from any company or organization that has Azure Active Directory.</span></span> <span data-ttu-id="54368-106">Le processus de connexion doit utiliser les protocoles [OpenID Connect](./active-directory-protocols-openid-connect-code.md) ou [OAuth 2.0](./active-directory-protocols-oauth-code.md).</span><span class="sxs-lookup"><span data-stu-id="54368-106">The sign-in process must use the [OpenID Connect](./active-directory-protocols-openid-connect-code.md) or [OAuth 2.0](./active-directory-protocols-oauth-code.md) protocols.</span></span> <span data-ttu-id="54368-107">L’intégration SAML n’est pas acceptée pour la certification AppSource.</span><span class="sxs-lookup"><span data-stu-id="54368-107">SAML integration is not accepted for AppSource certification.</span></span>

## <a name="guides-and-code-samples"></a><span data-ttu-id="54368-108">Guides et exemples de code</span><span class="sxs-lookup"><span data-stu-id="54368-108">Guides and code samples</span></span>
<span data-ttu-id="54368-109">Si vous souhaitez en savoir plus sur la façon d’intégrer votre application à Azure Active Directory à l’aide d’Open ID Connect, suivez nos guides et exemples de code dans la section [Prise en main](./active-directory-developers-guide.md#get-started "d’Azure Active Directory pour les développeurs").</span><span class="sxs-lookup"><span data-stu-id="54368-109">If you want to learn about how to integrate your application with Azure Active Directory using Open ID connect, follow our guides and code samples in the [Azure Active Directory developer's guide](./active-directory-developers-guide.md#get-started "Get Started with Azure AD for developers").</span></span>

## <a name="multi-tenant-applications"></a><span data-ttu-id="54368-110">Applications multilocataires</span><span class="sxs-lookup"><span data-stu-id="54368-110">Multi-tenant applications</span></span>

<span data-ttu-id="54368-111">Une application qui accepte les connexions des utilisateurs de toutes les entreprises ou organisations qui disposent d’Azure Active Directory sans qu’une instance, une configuration ou un déploiement distincts ne soient nécessaires est appelée une *application multilocataire*.</span><span class="sxs-lookup"><span data-stu-id="54368-111">An application that accepts sign-ins from users from any company or organization that have Azure Active Directory without requiring a separate instance, configuration, or deployment is known as a *multi-tenant application*.</span></span> <span data-ttu-id="54368-112">AppSource recommande que les applications implémentent une architecture mutualisée pour activer l’expérience d’essai gratuit *d’un seul clic*.</span><span class="sxs-lookup"><span data-stu-id="54368-112">AppSource recommends that applications implement multi-tenancy to enable the *single-click* free trial experience.</span></span>

<span data-ttu-id="54368-113">Pour activer une architecture mutualisée sur votre application :</span><span class="sxs-lookup"><span data-stu-id="54368-113">In order to enable multi-tenancy on your application:</span></span>
- <span data-ttu-id="54368-114">Définissez la propriété `Multi-Tenanted` sur `Yes` dans les informations d’inscription de votre application dans le [portail Azure](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (par défaut, les applications créées dans le portail Azure sont configurées en tant que *locataires uniques*).</span><span class="sxs-lookup"><span data-stu-id="54368-114">Set `Multi-Tenanted` property to `Yes` on your application registration's information in the [Azure Portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) (by default, applications created in the Azure Portal are configured as *single-tenant*)</span></span>
- <span data-ttu-id="54368-115">Mettez à jour votre code pour envoyer des demandes au point de terminaison « `common` » (mettez à jour le point de terminaison *https://login.microsoftonline.com/{yourtenant}* en le remplaçant par *https://login.microsoftonline.com/common*).</span><span class="sxs-lookup"><span data-stu-id="54368-115">Update your code to send requests to the '`common`' endpoint (update the endpoint from *https://login.microsoftonline.com/{yourtenant}* to *https://login.microsoftonline.com/common*)</span></span>
- <span data-ttu-id="54368-116">Pour certaines plateformes, comme ASP.NET, vous devez également mettre à jour votre code afin d’accepter plusieurs émetteurs.</span><span class="sxs-lookup"><span data-stu-id="54368-116">For some platforms, like ASP.NET, you need also to update your code to accept multiple issuers</span></span>

<span data-ttu-id="54368-117">Pour plus d’informations sur l’architecture mutualisée, consultez : [Comment connecter un utilisateur Azure Active Directory (AD) à l’aide du modèle d’application mutualisée](./active-directory-devhowto-multi-tenant-overview.md).</span><span class="sxs-lookup"><span data-stu-id="54368-117">For more information about multi-tenancy, see: [How to sign in any Azure Active Directory (AD) user using the multi-tenant application pattern](./active-directory-devhowto-multi-tenant-overview.md).</span></span>

### <a name="single-tenant-applications"></a><span data-ttu-id="54368-118">Applications à locataire unique</span><span class="sxs-lookup"><span data-stu-id="54368-118">Single-tenant applications</span></span>
<span data-ttu-id="54368-119">Les applications qui acceptent uniquement les connexions des utilisateurs d’une instance Azure Active Directory définie sont appelées *applications à locataire unique*.</span><span class="sxs-lookup"><span data-stu-id="54368-119">Applications that only accept sign-ins from users of a defined Azure Active Directory instance are known as *single-tenant application*.</span></span> <span data-ttu-id="54368-120">Les utilisateurs externes (y compris les comptes professionnels ou scolaires d’autres organisations ou les comptes personnels) peuvent se connecter à une application à locataire unique après l’ajout de chaque utilisateur en tant que *compte invité* à l’instance Azure Active Directory auprès de laquelle l’application est inscrite.</span><span class="sxs-lookup"><span data-stu-id="54368-120">External users (including Work or School accounts from other organizations, or personal account) can sign in to a single-tenant application after adding each user as *guest account* to the Azure Active Directory instance that the application is registered.</span></span> <span data-ttu-id="54368-121">Vous pouvez ajouter des utilisateurs en tant que comptes invités à Azure Active Directory via la [*collaboration Azure AD B2B*](../active-directory-b2b-what-is-azure-ad-b2b.md), et cela peut être effectué [par programmation](../active-directory-b2b-code-samples.md).</span><span class="sxs-lookup"><span data-stu-id="54368-121">You can add users as guest accounts to an Azure Active Directory via the [*Azure AD B2B collaboration*](../active-directory-b2b-what-is-azure-ad-b2b.md) - and it can be done [programatically](../active-directory-b2b-code-samples.md).</span></span> <span data-ttu-id="54368-122">Lorsque vous ajoutez un utilisateur en tant que compte invité à Azure Active Directory, un e-mail d’invitation est envoyé à l’utilisateur, qui doit accepter l’invitation en cliquant sur le lien présent dans cet e-mail.</span><span class="sxs-lookup"><span data-stu-id="54368-122">When you add a user as guest account to an Azure Active Directory, an invitation email is sent to the user, who has to accept the invitation by clicking on the link in the invitation email.</span></span> <span data-ttu-id="54368-123">Les invitations qui sont envoyées à un utilisateur supplémentaire dans une organisation hôte qui est également membre de l’organisation partenaire ne doit pas accepter d’invitation pour se connecter.</span><span class="sxs-lookup"><span data-stu-id="54368-123">Invitations that are sent to an additional user in an inviting organization that is also a member of the partner organization are not required to accept an invitation to sign in.</span></span>

<span data-ttu-id="54368-124">Les applications à locataire unique peuvent activer l’expérience *Me contacter*, mais si vous souhaitez activer l’expérience d’essai gratuit/d’un simple clic qu’AppSource recommande, activez l’architecture mutualisée de votre application à la place.</span><span class="sxs-lookup"><span data-stu-id="54368-124">Single-tenant applications can enable the *Contact Me* experience, but if you want to enable the single-click/ free trial experience that AppSource recommends, enable multi-tenancy on your application instead.</span></span>


## <a name="appsource-trial-experiences"></a><span data-ttu-id="54368-125">Expérience d’essai gratuit AppSource</span><span class="sxs-lookup"><span data-stu-id="54368-125">AppSource trial experiences</span></span>

### <a name="free-trial-customer-led-trial-experience"></a><span data-ttu-id="54368-126">Essai gratuit (expérience d’essai gratuit menée par le client)</span><span class="sxs-lookup"><span data-stu-id="54368-126">Free Trial (Customer-led trial experience)</span></span> 
<span data-ttu-id="54368-127">*L’essai gratuit mené par le client* est l’expérience recommandée par AppSource, car elle offre un accès d’un simple clic à votre application.</span><span class="sxs-lookup"><span data-stu-id="54368-127">The *customer-led trial* is the experience that AppSource recommends as it offers a single-click access to your application.</span></span> <span data-ttu-id="54368-128">Vous trouverez ci-dessous une illustration de cette expérience :</span><span class="sxs-lookup"><span data-stu-id="54368-128">Below an illustration of how this experience looks like:</span></span><br/><br/>

<table >
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="54368-129">Un utilisateur trouve votre application sur le site web AppSource.</span><span class="sxs-lookup"><span data-stu-id="54368-129">User finds your application in AppSource Web Site</span></span></li><li><span data-ttu-id="54368-130">Il sélectionne l’option « Essai gratuit ».</span><span class="sxs-lookup"><span data-stu-id="54368-130">Selects ‘Free trial’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step2.png" width="85%" /><ul><li><span data-ttu-id="54368-131">AppSource redirige l’utilisateur vers une URL de votre site web.</span><span class="sxs-lookup"><span data-stu-id="54368-131">AppSource redirects user to a URL in your web site</span></span></li><li><span data-ttu-id="54368-132">Votre site web lance le processus <i>d’authentification unique</i> automatiquement (au chargement de la page).</span><span class="sxs-lookup"><span data-stu-id="54368-132">Your web site starts the <i>single-sign-on</i> process automatically (on page load)</span></span></li></ul></td>
    <td valign="top" width="33%">3.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="54368-133">L’utilisateur est redirigé vers la page de connexion à Microsoft.</span><span class="sxs-lookup"><span data-stu-id="54368-133">User is redirected to Microsoft Sign-in page</span></span></li><li><span data-ttu-id="54368-134">L’utilisateur fournit des informations d’identification pour se connecter.</span><span class="sxs-lookup"><span data-stu-id="54368-134">User provides credentials to sign in</span></span></li></ul></td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="54368-135">L’utilisateur donne son consentement pour votre application.</span><span class="sxs-lookup"><span data-stu-id="54368-135">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="54368-136">Le processus de connexion se termine et l’utilisateur est redirigé vers votre site web.</span><span class="sxs-lookup"><span data-stu-id="54368-136">Sign-in completes and user is redirected back to your web site</span></span></li><li><span data-ttu-id="54368-137">L’utilisateur commence l’essai gratuit.</span><span class="sxs-lookup"><span data-stu-id="54368-137">User starts the free trial</span></span></li></ul></td>
    <td></td>
</tr>
</table>

### <a name="contact-me-partner-led-trial-experience"></a><span data-ttu-id="54368-138">Me contacter (expérience d’essai gratuit menée par le partenaire)</span><span class="sxs-lookup"><span data-stu-id="54368-138">Contact Me (Partner-led trial experience)</span></span>
<span data-ttu-id="54368-139">*L’expérience d’essai gratuit menée par le partenaire* peut être utilisée quand une opération manuelle ou à long terme doit se produire pour approvisionner l’utilisateur/la société : par exemple, votre application doit approvisionner des machines virtuelles, des instances de base de données ou des opérations prenant beaucoup de temps.</span><span class="sxs-lookup"><span data-stu-id="54368-139">The *partner trial experience* can be used when a manual or a long-term operation needs to happen to provision the user/ company: for example, your application needs to provision virtual machines, database instances, or operations that take much time to complete.</span></span> <span data-ttu-id="54368-140">Dans ce cas, après que l’utilisateur a sélectionné le bouton *« Demander une version d’évaluation »* et a rempli un formulaire, AppSource vous envoie les informations de contact de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="54368-140">In this case, after user selects the *'Request Trial'* button and fills out a form, AppSource sends you the user's contact information.</span></span> <span data-ttu-id="54368-141">Suite à la réception de ces informations, vous pouvez approvisionner l’environnement et envoyer les instructions à l’utilisateur pour qu’il puisse accéder à l’expérience d’essai gratuit :</span><span class="sxs-lookup"><span data-stu-id="54368-141">Upon receiving this information, you then provision the environment and send the instructions to the user on how to access the trial experience:</span></span><br/><br/>

<table valign="top">
<tr>
    <td valign="top" width="33%">1.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step1.png" width="85%"/><ul><li><span data-ttu-id="54368-142">Un utilisateur trouve votre application sur le site web AppSource.</span><span class="sxs-lookup"><span data-stu-id="54368-142">User finds your application in AppSource web site</span></span></li><li><span data-ttu-id="54368-143">Il sélectionne l’option « Me contacter ».</span><span class="sxs-lookup"><span data-stu-id="54368-143">Selects ‘Contact Me’ option</span></span></li></ul></td>
    <td valign="top" width="33%">2.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step2.png" width="85%"/><ul><li><span data-ttu-id="54368-144">Il remplit un formulaire avec ses informations de contact.</span><span class="sxs-lookup"><span data-stu-id="54368-144">Fills out a form with contact information</span></span></li></ul></td>
     <td valign="top" width="33%">3.<br/><br/>
        <table bgcolor="#f7f7f7">
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/UserContact.png" width="55%"/></td>
            <td><span data-ttu-id="54368-145">Vous recevez les informations de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="54368-145">You receive user information</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/SetupEnv.png" width="55%"/></td>
            <td><span data-ttu-id="54368-146">Configurez l’environnement.</span><span class="sxs-lookup"><span data-stu-id="54368-146">Setup environment</span></span></td>
        </tr>
        <tr>
            <td><img src="media/active-directory-devhowto-appsource-certified/ContactCustomer.png" width="55%"/></td>
            <td><span data-ttu-id="54368-147">Contactez l’utilisateur avec les informations relatives à l’essai gratuit.</span><span class="sxs-lookup"><span data-stu-id="54368-147">Contact user with trial info</span></span></td>
        </tr>
        </table><br/><br/>
        <ul><li><span data-ttu-id="54368-148">Vous recevez les informations de l’utilisateur et configurez l’instance d’essai gratuit.</span><span class="sxs-lookup"><span data-stu-id="54368-148">You receive user's information and setup trial instance</span></span></li><li><span data-ttu-id="54368-149">Vous envoyez à l’utilisateur le lien hypertexte permettant d’accéder à votre application.</span><span class="sxs-lookup"><span data-stu-id="54368-149">You send the hyperlink to access your application to the user</span></span></li></ul>
    </td>
</tr>
<tr>
    <td valign="top" width="33%">4.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step3.png" width="85%"/><ul><li><span data-ttu-id="54368-150">L’utilisateur accède à votre application et termine le processus d’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="54368-150">User accesses your application and complete the single-sign-on process</span></span></li></ul></td>
    <td valign="top" width="33%">5.<br/><img src="media/active-directory-devhowto-appsource-certified/partner-led-trial-step4.png" width="85%"/><ul><li><span data-ttu-id="54368-151">L’utilisateur donne son consentement pour votre application.</span><span class="sxs-lookup"><span data-stu-id="54368-151">User gives consent for your application</span></span></li></ul></td>
    <td valign="top" width="33%">6.<br/><img src="media/active-directory-devhowto-appsource-certified/customer-led-trial-step5.png" width="85%"/><ul><li><span data-ttu-id="54368-152">Le processus de connexion se termine et l’utilisateur est redirigé vers votre site web.</span><span class="sxs-lookup"><span data-stu-id="54368-152">Sign-in completes and user is redirected back to your web site</span></span></li><li><span data-ttu-id="54368-153">L’utilisateur commence l’essai gratuit.</span><span class="sxs-lookup"><span data-stu-id="54368-153">User starts the free trial</span></span></li></ul></td>
   
</tr>
</table>

### <a name="more-information"></a><span data-ttu-id="54368-154">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="54368-154">More information</span></span>
<span data-ttu-id="54368-155">Pour plus d’informations sur l’expérience d’essai gratuit AppSource, regardez [cette vidéo](https://aka.ms/trialexperienceforwebapps).</span><span class="sxs-lookup"><span data-stu-id="54368-155">For more information about the AppSource trial experience, see [this video](https://aka.ms/trialexperienceforwebapps).</span></span> 
 
## <a name="next-steps"></a><span data-ttu-id="54368-156">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="54368-156">Next Steps</span></span>

- <span data-ttu-id="54368-157">Pour plus d’informations sur la création d’applications qui prennent en charge les connexions Azure Active Directory, consultez [Scénarios d’authentification pour Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).</span><span class="sxs-lookup"><span data-stu-id="54368-157">For more information on building applications that support Azure Active Directory sign-ins, see [Authentication Scenarios for Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios)</span></span> 

- <span data-ttu-id="54368-158">Pour plus d’informations sur comment répertorier votre application SaaS dans AppSource, consultez [les informations sur les partenaires AppSource](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="54368-158">For information on how to list your SaaS application in AppSource, go see [AppSource Partner Information](https://appsource.microsoft.com/partners)</span></span>


## <a name="get-support"></a><span data-ttu-id="54368-159">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="54368-159">Get Support</span></span>
<span data-ttu-id="54368-160">Pour l’intégration Azure Active Directory, nous utilisons [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) avec la communauté pour proposer de l’aide.</span><span class="sxs-lookup"><span data-stu-id="54368-160">For Azure Active Directory integration, we use [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory) with the community to provide support.</span></span> 

<span data-ttu-id="54368-161">Nous vous recommandons vivement de poser vos questions sur Stack Overflow d’abord et de parcourir les problèmes existants pour voir si quelqu’un d’autre a déjà posé la même question.</span><span class="sxs-lookup"><span data-stu-id="54368-161">We highly recommend you ask your questions on Stack Overflow first and browse existing issues to see if someone has asked your question before.</span></span> <span data-ttu-id="54368-162">Vérifiez que vos questions ou commentaires portent la mention `[azure-active-directory]`.</span><span class="sxs-lookup"><span data-stu-id="54368-162">Make sure that your questions or comments are tagged with `[azure-active-directory]`.</span></span>

<span data-ttu-id="54368-163">Utilisez la section Commentaires suivante pour donner votre avis et nous aider à affiner et à mettre en forme notre contenu.</span><span class="sxs-lookup"><span data-stu-id="54368-163">Use the following comments section to provide feedback and help us refine and shape our content.</span></span>

<!--Reference style links -->
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Auth-Scenarios-Browser-To-WebApp]: ./active-directory-authentication-scenarios.md#web-browser-to-web-application
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Howto-Multitenant-Overview]: ./active-directory-devhowto-multi-tenant-overview.md
[AAD-QuickStart-Web-Apps]: ./active-directory-developers-guide.md#get-started


<!--Image references-->