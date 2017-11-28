---
title: "les applications avec Proxy d’Application Azure AD aaaPublish | Documents Microsoft"
description: "Bonjour portail Azure, publier cloud de toohello d’applications local avec le Proxy d’Application Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ed5458467fb7d4376f65a222f1ba5f23cfdfc57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="0a625-103">Publier des applications avec le Proxy d’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a625-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0a625-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="0a625-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="0a625-105">portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="0a625-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="0a625-106">Proxy d’Application Azure Active Directory (AD) vous permet de prendre en charge des travailleurs à distance en publiant toobe d’applications local accédé via hello internet.</span><span class="sxs-lookup"><span data-stu-id="0a625-106">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications toobe accessed over hello internet.</span></span> <span data-ttu-id="0a625-107">Vous pouvez publier ces applications via hello tooprovide portail Azure à distance un accès sécurisé à partir d’à l’extérieur de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="0a625-107">You can publish these applications through hello Azure portal tooprovide secure remote access from outside your network.</span></span>

<span data-ttu-id="0a625-108">Cet article vous guide tout au long des étapes de hello toopublish une application locale avec le Proxy d’Application.</span><span class="sxs-lookup"><span data-stu-id="0a625-108">This article walks you through hello steps toopublish an on-premises app with Application Proxy.</span></span> <span data-ttu-id="0a625-109">Après avoir terminé cet article, vos utilisateurs seront être, tooaccess en mesure de votre application à distance.</span><span class="sxs-lookup"><span data-stu-id="0a625-109">After you complete this article, your users will be able tooaccess your app remotely.</span></span> <span data-ttu-id="0a625-110">Et vous serez prêt tooconfigure des fonctionnalités supplémentaires pour l’application hello comme single sign-on, des informations personnalisées et exigences de sécurité.</span><span class="sxs-lookup"><span data-stu-id="0a625-110">And you'll be ready tooconfigure extra features for hello application like single sign-on, personalized information, and security requirements.</span></span>

<span data-ttu-id="0a625-111">Si vous êtes tooApplication nouveau Proxy, en savoir plus sur cette fonctionnalité avec l’article hello [comment tooprovide sécuriser l’accès à distance, applications locales tooon](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0a625-111">If you're new tooApplication Proxy, learn more about this feature with hello article [How tooprovide secure remote access tooon-premises applications](active-directory-application-proxy-get-started.md).</span></span>


## <a name="publish-an-on-premises-app-for-remote-access"></a><span data-ttu-id="0a625-112">Publier une application locale pour un accès à distance</span><span class="sxs-lookup"><span data-stu-id="0a625-112">Publish an on-premises app for remote access</span></span>

<span data-ttu-id="0a625-113">Suivez ces étapes toopublish vos applications avec Proxy d’Application.</span><span class="sxs-lookup"><span data-stu-id="0a625-113">Follow these steps toopublish your apps with Application Proxy.</span></span> <span data-ttu-id="0a625-114">Si vous n’avez pas déjà téléchargé et configuré un connecteur pour votre organisation, passez trop[prise en main le Proxy d’Application et d’installer le connecteur de hello](active-directory-application-proxy-enable.md) tout d’abord, puis publier votre application.</span><span class="sxs-lookup"><span data-stu-id="0a625-114">If you haven't already downloaded and configured a connector for your organization, go too[Get started with Application Proxy and install hello connector](active-directory-application-proxy-enable.md) first, and then publish your app.</span></span>

> [!TIP]
> <span data-ttu-id="0a625-115">Si vous testez des Proxy d’Application pour hello première fois, sélectionnez une application qui est configurée pour l’authentification basée sur mot de passe.</span><span class="sxs-lookup"><span data-stu-id="0a625-115">If you're testing out Application Proxy for hello first time, choose an application that's set up for password-based authentication.</span></span> <span data-ttu-id="0a625-116">Le Proxy d’application prend en charge d’autres types d’authentification, mais les applications basées sur le mot de passe sont tooget plus simple de hello haut et à exécuter rapidement.</span><span class="sxs-lookup"><span data-stu-id="0a625-116">Application Proxy supports other types of authentication, but password-based apps are hello easiest tooget up and running quickly.</span></span> 

1. <span data-ttu-id="0a625-117">Connectez-vous en tant qu’administrateur Bonjour [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0a625-117">Sign in as an administrator in hello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0a625-118">Sélectionnez **Azure Active Directory** > **Applications d’entreprise** > **Nouvelle application**.</span><span class="sxs-lookup"><span data-stu-id="0a625-118">Select **Azure Active Directory** > **Enterprise applications** > **New application**.</span></span>

  ![Ajouter une application d’entreprise](./media/application-proxy-publish-azure-portal/add-app.png)

3. <span data-ttu-id="0a625-120">Sélectionnez **Tout**, puis **Application locale**.</span><span class="sxs-lookup"><span data-stu-id="0a625-120">Select **All**, then select **On-premises application**.</span></span>  

  ![Ajout de votre propre application](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. <span data-ttu-id="0a625-122">Fournir hello suit les informations de votre application :</span><span class="sxs-lookup"><span data-stu-id="0a625-122">Provide hello following information about your application:</span></span>

   - <span data-ttu-id="0a625-123">**Nom**: nom hello d’application hello qui apparaîtra dans le volet d’accès hello et Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0a625-123">**Name**: hello name of hello application that will appear on hello access panel and in hello Azure portal.</span></span> 

   - <span data-ttu-id="0a625-124">**URL interne**: hello URL que vous utilisez l’application de hello tooaccess à partir de votre réseau privé.</span><span class="sxs-lookup"><span data-stu-id="0a625-124">**Internal URL**: hello URL that you use tooaccess hello application from inside your private network.</span></span> <span data-ttu-id="0a625-125">Vous pouvez fournir un chemin d’accès spécifique sur hello toopublish de serveur principal, tandis que le reste de hello du serveur de hello n’est pas publiée.</span><span class="sxs-lookup"><span data-stu-id="0a625-125">You can provide a specific path on hello backend server toopublish, while hello rest of hello server is unpublished.</span></span> <span data-ttu-id="0a625-126">De cette façon, vous pouvez publier des sites différents sur hello même serveur en tant qu’applications différentes et chacune d’elles fournissent des ses propres règles d’accès et le nom.</span><span class="sxs-lookup"><span data-stu-id="0a625-126">In this way, you can publish different sites on hello same server as different apps, and give each one its own name and access rules.</span></span>

     > [!TIP]
     > <span data-ttu-id="0a625-127">Si vous publiez un chemin d’accès, assurez-vous qu’il inclut toutes les images nécessaires de hello, des scripts et des feuilles de style pour votre application.</span><span class="sxs-lookup"><span data-stu-id="0a625-127">If you publish a path, make sure that it includes all hello necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="0a625-128">Par exemple, si votre application est à https://yourapp/app et utilise des images à https://yourapp/media, vous devez publier https://yourapp/ comme chemin d’accès hello.</span><span class="sxs-lookup"><span data-stu-id="0a625-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as hello path.</span></span> <span data-ttu-id="0a625-129">Page d’accueil hello toobe que vos utilisateurs voient ne dispose pas cette URL interne.</span><span class="sxs-lookup"><span data-stu-id="0a625-129">This internal URL doesn't have toobe hello landing page your users see.</span></span> <span data-ttu-id="0a625-130">Pour plus d’informations, consultez [Définir une page d’accueil personnalisée pour les applications publiées](application-proxy-office365-app-launcher.md).</span><span class="sxs-lookup"><span data-stu-id="0a625-130">For more information, see [Set a custom home page for published apps](application-proxy-office365-app-launcher.md).</span></span>

   - <span data-ttu-id="0a625-131">**URL externe**: hello adresse vos utilisateurs passera tooin commande tooaccess hello de l’application en dehors de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="0a625-131">**External URL**: hello address your users will go tooin order tooaccess hello app from outside your network.</span></span> <span data-ttu-id="0a625-132">Si vous ne souhaitez pas domaine de Proxy d’Application par défaut toouse hello, en savoir plus sur [des domaines personnalisés dans le Proxy d’Application Azure AD](active-directory-application-proxy-custom-domains.md).</span><span class="sxs-lookup"><span data-stu-id="0a625-132">If you don't want toouse hello default Application Proxy domain, read about [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md).</span></span>
   - <span data-ttu-id="0a625-133">**Pré-authentification**: comment le Proxy d’Application vérifie les utilisateurs avant d’en leur donnant accès tooyour application.</span><span class="sxs-lookup"><span data-stu-id="0a625-133">**Pre Authentication**: How Application Proxy verifies users before giving them access tooyour application.</span></span> 

     - <span data-ttu-id="0a625-134">Azure Active Directory : Le Proxy d’Application redirige toosign utilisateurs avec Azure AD, qui authentifie leurs autorisations pour le répertoire de hello et application.</span><span class="sxs-lookup"><span data-stu-id="0a625-134">Azure Active Directory: Application Proxy redirects users toosign in with Azure AD, which authenticates their permissions for hello directory and application.</span></span> <span data-ttu-id="0a625-135">Nous vous recommandons de laisser cette option comme valeur par défaut de hello, afin que vous pouvez tirer parti des fonctionnalités de sécurité Azure AD telles que les conditions d’accès et l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="0a625-135">We recommend keeping this option as hello default, so that you can take advantage of Azure AD security features like conditional access and Multi-Factor Authentication.</span></span>
     - <span data-ttu-id="0a625-136">Passthrough : Les utilisateurs n’aient tooauthenticate par rapport à l’application de hello tooaccess Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0a625-136">Passthrough: Users don't have tooauthenticate against Azure Active Directory tooaccess hello application.</span></span> <span data-ttu-id="0a625-137">Vous pouvez toujours configurer les exigences d’authentification sur le back-end hello.</span><span class="sxs-lookup"><span data-stu-id="0a625-137">You can still set up authentication requirements on hello backend.</span></span>
   - <span data-ttu-id="0a625-138">**Groupe de connecteurs**: application tooyour de connecteurs processus hello accès à distance et les groupes de connecteur vous aident à organiser les connecteurs et les applications par région, le réseau ou objectif.</span><span class="sxs-lookup"><span data-stu-id="0a625-138">**Connector Group**: Connectors process hello remote access tooyour application, and connector groups help you organize connectors and apps by region, network, or purpose.</span></span> <span data-ttu-id="0a625-139">Si vous n’avez pas les groupes de connecteurs encore créés, votre application est trop affectée**par défaut**.</span><span class="sxs-lookup"><span data-stu-id="0a625-139">If you don't have any connector groups created yet, your app is assigned too**Default**.</span></span>

   ![Configuration de votre application](./media/application-proxy-publish-azure-portal/configure-app.png)
5. <span data-ttu-id="0a625-141">Si nécessaire, configurez des paramètres supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="0a625-141">If necessary, configure additional settings.</span></span> <span data-ttu-id="0a625-142">Pour la plupart des applications, vous devez conserver ces paramètres dans leur état par défaut.</span><span class="sxs-lookup"><span data-stu-id="0a625-142">For most applications, you should keep these settings in their default states.</span></span> 
   - <span data-ttu-id="0a625-143">**Délai d’Application principal**: définissez cette valeur trop**Long** uniquement si votre application est lente tooauthenticate et se connecter.</span><span class="sxs-lookup"><span data-stu-id="0a625-143">**Backend Application Timeout**: Set this value too**Long** only if your application is slow tooauthenticate and connect.</span></span> 
   - <span data-ttu-id="0a625-144">**URL dans les en-têtes**: conserver cette valeur en tant que **Oui** , sauf si votre application requis d’en-tête d’hôte d’origine hello dans la demande d’authentification hello.</span><span class="sxs-lookup"><span data-stu-id="0a625-144">**Translate URLs in Headers**: Keep this value as **Yes** unless your application required hello original host header in hello authentication request.</span></span>
   - <span data-ttu-id="0a625-145">**URL dans le corps de l’Application**: conserver cette valeur en tant que **non** , sauf si vous avez codé en dur HTML liens tooother des applications locales et que vous n’utilisez pas des domaines personnalisés.</span><span class="sxs-lookup"><span data-stu-id="0a625-145">**Translate URLs in Application Body**: Keep this value as **No** unless you have hardcoded HTML links tooother on-premises applications, and don't use custom domains.</span></span> <span data-ttu-id="0a625-146">Pour plus d’informations, consultez [Rediriger les liens codés en dur pour les applications publiées avec le Proxy d’application Azure AD](application-proxy-link-translation.md).</span><span class="sxs-lookup"><span data-stu-id="0a625-146">For more information, see [Link translation with Application Proxy](application-proxy-link-translation.md).</span></span>
   
   ![Configuration de votre application](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. <span data-ttu-id="0a625-148">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0a625-148">Select **Add**.</span></span>


## <a name="add-a-test-user"></a><span data-ttu-id="0a625-149">Ajouter un utilisateur de test</span><span class="sxs-lookup"><span data-stu-id="0a625-149">Add a test user</span></span> 

<span data-ttu-id="0a625-150">tootest que votre application a été publiée correctement, ajoutez un compte d’utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="0a625-150">tootest that your app was published correctly, add a test user account.</span></span> <span data-ttu-id="0a625-151">Vérifiez que ce compte dispose déjà des autorisations tooaccess hello de l’application à l’intérieur du réseau d’entreprise de hello.</span><span class="sxs-lookup"><span data-stu-id="0a625-151">Verify that this account already has permissions tooaccess hello app from inside hello corporate network.</span></span>

1. <span data-ttu-id="0a625-152">Dans le panneau de démarrage rapide de hello, sélectionnez **affecter un utilisateur de test**.</span><span class="sxs-lookup"><span data-stu-id="0a625-152">Back on hello Quick start blade, select **Assign a user for testing**.</span></span>

  ![Attribuer un utilisateur à des fins de test](./media/application-proxy-publish-azure-portal/assign-user.png)

2. <span data-ttu-id="0a625-154">Sur les utilisateurs de hello et panneau de groupes, sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0a625-154">On hello Users and groups blade, select **Add**.</span></span>

  ![Ajouter un utilisateur ou groupe](./media/application-proxy-publish-azure-portal/add-user.png)

3. <span data-ttu-id="0a625-156">Dans le panneau de devoir ajouter hello, sélectionnez **utilisateurs et groupes** puis choisissez compte hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0a625-156">On hello Add assignment blade, select **Users and groups** then choose hello account you want tooadd.</span></span> 
4. <span data-ttu-id="0a625-157">Sélectionnez **Attribuer**.</span><span class="sxs-lookup"><span data-stu-id="0a625-157">Select **Assign**.</span></span>

## <a name="test-your-published-app"></a><span data-ttu-id="0a625-158">Tester votre application publiée</span><span class="sxs-lookup"><span data-stu-id="0a625-158">Test your published app</span></span>

<span data-ttu-id="0a625-159">Dans votre navigateur, accédez à toohello URL externe que vous avez configurés au cours de hello étape de publication.</span><span class="sxs-lookup"><span data-stu-id="0a625-159">In your browser, navigate toohello external URL that you configured during hello publish step.</span></span> <span data-ttu-id="0a625-160">Vous devez normalement voir écran d’accueil hello et être en mesure de toosign avec compte de test hello permet de paramétrer.</span><span class="sxs-lookup"><span data-stu-id="0a625-160">You should see hello start screen, and be able toosign in with hello test account you set up.</span></span>

![Tester votre application publiée](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a><span data-ttu-id="0a625-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0a625-162">Next steps</span></span>
- <span data-ttu-id="0a625-163">[Télécharger des connecteurs](active-directory-application-proxy-enable.md) et [créer des groupes de connecteurs](active-directory-application-proxy-connectors-azure-portal.md) toopublish des applications sur des réseaux distincts et emplacements.</span><span class="sxs-lookup"><span data-stu-id="0a625-163">[Download connectors](active-directory-application-proxy-enable.md) and [create connector groups](active-directory-application-proxy-connectors-azure-portal.md) toopublish applications on separate networks and locations.</span></span>

- <span data-ttu-id="0a625-164">[Configurer l’authentification unique](application-proxy-sso-azure-portal.md) pour votre application récemment publiée</span><span class="sxs-lookup"><span data-stu-id="0a625-164">[Set up single sign-on](application-proxy-sso-azure-portal.md) for your newly published app</span></span>
