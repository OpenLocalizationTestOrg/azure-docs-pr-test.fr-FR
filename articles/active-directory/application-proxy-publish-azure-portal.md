---
title: "Publier des applications avec le proxy d’application Azure AD | Microsoft Docs"
description: "Publiez des applications locales dans le cloud avec le proxy d’application Azure AD dans le portail Azure."
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
ms.openlocfilehash: e00a939f2b20ab8e0a2ddf0ff91e59db440213ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="publish-applications-using-azure-ad-application-proxy"></a><span data-ttu-id="8e528-103">Publier des applications avec le Proxy d’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e528-103">Publish applications using Azure AD Application Proxy</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8e528-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="8e528-104">Azure portal</span></span>](application-proxy-publish-azure-portal.md)
> * [<span data-ttu-id="8e528-105">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="8e528-105">Azure classic portal</span></span>](active-directory-application-proxy-publish.md)

<span data-ttu-id="8e528-106">Le service Proxy d’application Azure Active Directory (AD) vous aide à prendre en charge les personnes qui travaillent à distance en publiant des applications locales afin de les rendre accessibles sur Internet.</span><span class="sxs-lookup"><span data-stu-id="8e528-106">Azure Active Directory (AD) Application Proxy helps you support remote workers by publishing on-premises applications to be accessed over the internet.</span></span> <span data-ttu-id="8e528-107">Vous pouvez publier ces applications sur le portail Azure et fournir un accès à distance sécurisé à partir de l’extérieur de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="8e528-107">You can publish these applications through the Azure portal to provide secure remote access from outside your network.</span></span>

<span data-ttu-id="8e528-108">Cet article vous guide au long des étapes de publication d’une application locale avec un proxy d’application.</span><span class="sxs-lookup"><span data-stu-id="8e528-108">This article walks you through the steps to publish an on-premises app with Application Proxy.</span></span> <span data-ttu-id="8e528-109">Une fois que vous aurez suivi cet article, vos utilisateurs seront en mesure d’accéder à votre application à distance.</span><span class="sxs-lookup"><span data-stu-id="8e528-109">After you complete this article, your users will be able to access your app remotely.</span></span> <span data-ttu-id="8e528-110">Et vous serez prêt à configurer des fonctionnalités supplémentaires pour l’application, comme l’authentification unique, les exigences de sécurité ou les informations personnalisées.</span><span class="sxs-lookup"><span data-stu-id="8e528-110">And you'll be ready to configure extra features for the application like single sign-on, personalized information, and security requirements.</span></span>

<span data-ttu-id="8e528-111">Si vous n’êtes pas familiarisé avec le proxy d’application, vous pouvez en savoir plus en consultant l’article [Offrir un accès à distance sécurisé aux applications locales](active-directory-application-proxy-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8e528-111">If you're new to Application Proxy, learn more about this feature with the article [How to provide secure remote access to on-premises applications](active-directory-application-proxy-get-started.md).</span></span>


## <a name="publish-an-on-premises-app-for-remote-access"></a><span data-ttu-id="8e528-112">Publier une application locale pour un accès à distance</span><span class="sxs-lookup"><span data-stu-id="8e528-112">Publish an on-premises app for remote access</span></span>

<span data-ttu-id="8e528-113">Suivez ces étapes pour publier vos applications avec le proxy d’application.</span><span class="sxs-lookup"><span data-stu-id="8e528-113">Follow these steps to publish your apps with Application Proxy.</span></span> <span data-ttu-id="8e528-114">Si vous n’avez pas déjà téléchargé et configuré un connecteur pour votre organisation, accédez à [Bien démarrer avec le proxy d’application et l’installation du connecteur](active-directory-application-proxy-enable.md), puis publiez votre application.</span><span class="sxs-lookup"><span data-stu-id="8e528-114">If you haven't already downloaded and configured a connector for your organization, go to [Get started with Application Proxy and install the connector](active-directory-application-proxy-enable.md) first, and then publish your app.</span></span>

> [!TIP]
> <span data-ttu-id="8e528-115">Si vous testez le proxy d’application pour la première fois, choisissez une application qui est configurée pour l’authentification par mot de passe.</span><span class="sxs-lookup"><span data-stu-id="8e528-115">If you're testing out Application Proxy for the first time, choose an application that's set up for password-based authentication.</span></span> <span data-ttu-id="8e528-116">Le proxy d’application prend en charge d’autres types d’authentification, mais les applications basées sur un mot de passe sont les plus faciles à exploiter rapidement.</span><span class="sxs-lookup"><span data-stu-id="8e528-116">Application Proxy supports other types of authentication, but password-based apps are the easiest to get up and running quickly.</span></span> 

1. <span data-ttu-id="8e528-117">Connectez-vous au [portail Azure](https://portal.azure.com/) en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="8e528-117">Sign in as an administrator in the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8e528-118">Sélectionnez **Azure Active Directory** > **Applications d’entreprise** > **Nouvelle application**.</span><span class="sxs-lookup"><span data-stu-id="8e528-118">Select **Azure Active Directory** > **Enterprise applications** > **New application**.</span></span>

  ![Ajouter une application d’entreprise](./media/application-proxy-publish-azure-portal/add-app.png)

3. <span data-ttu-id="8e528-120">Sélectionnez **Tout**, puis **Application locale**.</span><span class="sxs-lookup"><span data-stu-id="8e528-120">Select **All**, then select **On-premises application**.</span></span>  

  ![Ajout de votre propre application](./media/application-proxy-publish-azure-portal/add-your-own.png)

4. <span data-ttu-id="8e528-122">Fournissez les informations suivantes sur votre application :</span><span class="sxs-lookup"><span data-stu-id="8e528-122">Provide the following information about your application:</span></span>

   - <span data-ttu-id="8e528-123">**Nom** : nom de l’application qui apparaît dans le panneau d’accès et sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8e528-123">**Name**: The name of the application that will appear on the access panel and in the Azure portal.</span></span> 

   - <span data-ttu-id="8e528-124">**URL interne** : URL permettant d’accéder à l’application à partir de votre réseau privé.</span><span class="sxs-lookup"><span data-stu-id="8e528-124">**Internal URL**: The URL that you use to access the application from inside your private network.</span></span> <span data-ttu-id="8e528-125">Vous pouvez spécifier un chemin spécifique sur le serveur principal à publier, alors que le reste du serveur n’est pas publié.</span><span class="sxs-lookup"><span data-stu-id="8e528-125">You can provide a specific path on the backend server to publish, while the rest of the server is unpublished.</span></span> <span data-ttu-id="8e528-126">De cette façon, vous pouvez publier des sites différents sur le même serveur en tant qu’applications distinctes et donner à chacun d’eux son propre nom et ses propres règles d’accès.</span><span class="sxs-lookup"><span data-stu-id="8e528-126">In this way, you can publish different sites on the same server as different apps, and give each one its own name and access rules.</span></span>

     > [!TIP]
     > <span data-ttu-id="8e528-127">Si vous publiez un chemin d’accès, vérifiez qu’il inclut l’ensemble des images, des scripts et des feuilles de style nécessaires pour votre application.</span><span class="sxs-lookup"><span data-stu-id="8e528-127">If you publish a path, make sure that it includes all the necessary images, scripts, and style sheets for your application.</span></span> <span data-ttu-id="8e528-128">Par exemple, si votre application est sur https://yourapp/app et utilise des images situées dans https://yourapp/media, vous devez publier https://yourapp/ comme chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="8e528-128">For example, if your app is at https://yourapp/app and uses images located at https://yourapp/media, then you should publish https://yourapp/ as the path.</span></span> <span data-ttu-id="8e528-129">Cette URL interne n’est pas nécessairement la page d’accueil que vos utilisateurs voient.</span><span class="sxs-lookup"><span data-stu-id="8e528-129">This internal URL doesn't have to be the landing page your users see.</span></span> <span data-ttu-id="8e528-130">Pour plus d’informations, consultez [Définir une page d’accueil personnalisée pour les applications publiées](application-proxy-office365-app-launcher.md).</span><span class="sxs-lookup"><span data-stu-id="8e528-130">For more information, see [Set a custom home page for published apps](application-proxy-office365-app-launcher.md).</span></span>

   - <span data-ttu-id="8e528-131">**URL externe** : adresse que vos utilisateurs utilisent pour accéder à l’application en dehors de votre réseau.</span><span class="sxs-lookup"><span data-stu-id="8e528-131">**External URL**: The address your users will go to in order to access the app from outside your network.</span></span> <span data-ttu-id="8e528-132">Si vous ne souhaitez pas utiliser le domaine de proxy d’application par défaut, lisez la documentation relative aux [domaines personnalisés dans le proxy d’application Azure AD](active-directory-application-proxy-custom-domains.md).</span><span class="sxs-lookup"><span data-stu-id="8e528-132">If you don't want to use the default Application Proxy domain, read about [custom domains in Azure AD Application Proxy](active-directory-application-proxy-custom-domains.md).</span></span>
   - <span data-ttu-id="8e528-133">**Pré-authentification** : façon dont le service Proxy d’application vérifie les utilisateurs avant de leur donner accès à votre application.</span><span class="sxs-lookup"><span data-stu-id="8e528-133">**Pre Authentication**: How Application Proxy verifies users before giving them access to your application.</span></span> 

     - <span data-ttu-id="8e528-134">Azure Active Directory : le proxy d’application redirige les utilisateurs pour la connexion à Azure AD, qui authentifie leurs autorisations pour le répertoire et l’application.</span><span class="sxs-lookup"><span data-stu-id="8e528-134">Azure Active Directory: Application Proxy redirects users to sign in with Azure AD, which authenticates their permissions for the directory and application.</span></span> <span data-ttu-id="8e528-135">Nous vous recommandons de laisser cette option par défaut, afin que vous puissiez tirer parti des fonctionnalités de sécurité Azure AD, comme l’accès conditionnel et l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="8e528-135">We recommend keeping this option as the default, so that you can take advantage of Azure AD security features like conditional access and Multi-Factor Authentication.</span></span>
     - <span data-ttu-id="8e528-136">Direct : les utilisateurs n’ont pas besoin de s’authentifier auprès d’Azure Active Directory pour accéder à l’application.</span><span class="sxs-lookup"><span data-stu-id="8e528-136">Passthrough: Users don't have to authenticate against Azure Active Directory to access the application.</span></span> <span data-ttu-id="8e528-137">Vous pouvez toujours configurer les exigences d’authentification sur le serveur principal.</span><span class="sxs-lookup"><span data-stu-id="8e528-137">You can still set up authentication requirements on the backend.</span></span>
   - <span data-ttu-id="8e528-138">**Groupe de connecteurs** : les connecteurs gèrent l’accès à distance à votre application et les groupes de connecteurs vous aident à organiser des connecteurs et des applications par région, réseau ou objectif.</span><span class="sxs-lookup"><span data-stu-id="8e528-138">**Connector Group**: Connectors process the remote access to your application, and connector groups help you organize connectors and apps by region, network, or purpose.</span></span> <span data-ttu-id="8e528-139">Si aucun groupe de connecteurs n’est encore créé, votre application est assignée au groupe **Par défaut**.</span><span class="sxs-lookup"><span data-stu-id="8e528-139">If you don't have any connector groups created yet, your app is assigned to **Default**.</span></span>

   ![Configuration de votre application](./media/application-proxy-publish-azure-portal/configure-app.png)
5. <span data-ttu-id="8e528-141">Si nécessaire, configurez des paramètres supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="8e528-141">If necessary, configure additional settings.</span></span> <span data-ttu-id="8e528-142">Pour la plupart des applications, vous devez conserver ces paramètres dans leur état par défaut.</span><span class="sxs-lookup"><span data-stu-id="8e528-142">For most applications, you should keep these settings in their default states.</span></span> 
   - <span data-ttu-id="8e528-143">**Expiration de l’application principale** : définissez cette valeur sur **Long** uniquement si l’authentification et la connexion de votre application sont lentes.</span><span class="sxs-lookup"><span data-stu-id="8e528-143">**Backend Application Timeout**: Set this value to **Long** only if your application is slow to authenticate and connect.</span></span> 
   - <span data-ttu-id="8e528-144">**Traduire l’URL dans les en-têtes** : conservez la valeur **Oui**, sauf si votre application a demandé l’en-tête d’hôte d’origine dans la requête d’authentification.</span><span class="sxs-lookup"><span data-stu-id="8e528-144">**Translate URLs in Headers**: Keep this value as **Yes** unless your application required the original host header in the authentication request.</span></span>
   - <span data-ttu-id="8e528-145">**Translate URLs in Application Body** (Traduire les URL dans le corps de l’application) : conservez la valeur **Non**, sauf si vous avez codé en dur des liens HTML vers d’autres applications locales et si vous n’utilisez pas les domaines personnalisés.</span><span class="sxs-lookup"><span data-stu-id="8e528-145">**Translate URLs in Application Body**: Keep this value as **No** unless you have hardcoded HTML links to other on-premises applications, and don't use custom domains.</span></span> <span data-ttu-id="8e528-146">Pour plus d’informations, consultez [Rediriger les liens codés en dur pour les applications publiées avec le Proxy d’application Azure AD](application-proxy-link-translation.md).</span><span class="sxs-lookup"><span data-stu-id="8e528-146">For more information, see [Link translation with Application Proxy](application-proxy-link-translation.md).</span></span>
   
   ![Configuration de votre application](./media/application-proxy-publish-azure-portal/additional-settings.png)

6. <span data-ttu-id="8e528-148">Sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8e528-148">Select **Add**.</span></span>


## <a name="add-a-test-user"></a><span data-ttu-id="8e528-149">Ajouter un utilisateur de test</span><span class="sxs-lookup"><span data-stu-id="8e528-149">Add a test user</span></span> 

<span data-ttu-id="8e528-150">Pour vérifier que votre application a été correctement publiée, ajoutez un compte d’utilisateur test.</span><span class="sxs-lookup"><span data-stu-id="8e528-150">To test that your app was published correctly, add a test user account.</span></span> <span data-ttu-id="8e528-151">Vérifiez que ce compte dispose déjà des autorisations d’accès à l’application à partir du réseau d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="8e528-151">Verify that this account already has permissions to access the app from inside the corporate network.</span></span>

1. <span data-ttu-id="8e528-152">Dans le panneau Démarrage rapide, sélectionnez **Assign a user for testing (Attribuer un utilisateur à des fins de test)**.</span><span class="sxs-lookup"><span data-stu-id="8e528-152">Back on the Quick start blade, select **Assign a user for testing**.</span></span>

  ![Attribuer un utilisateur à des fins de test](./media/application-proxy-publish-azure-portal/assign-user.png)

2. <span data-ttu-id="8e528-154">Dans le panneau Utilisateurs et groupes, sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8e528-154">On the Users and groups blade, select **Add**.</span></span>

  ![Ajouter un utilisateur ou groupe](./media/application-proxy-publish-azure-portal/add-user.png)

3. <span data-ttu-id="8e528-156">Dans le panneau Ajouter une attribution, sélectionnez **Utilisateurs et groupes**, puis le compte à ajouter.</span><span class="sxs-lookup"><span data-stu-id="8e528-156">On the Add assignment blade, select **Users and groups** then choose the account you want to add.</span></span> 
4. <span data-ttu-id="8e528-157">Sélectionnez **Attribuer**.</span><span class="sxs-lookup"><span data-stu-id="8e528-157">Select **Assign**.</span></span>

## <a name="test-your-published-app"></a><span data-ttu-id="8e528-158">Tester votre application publiée</span><span class="sxs-lookup"><span data-stu-id="8e528-158">Test your published app</span></span>

<span data-ttu-id="8e528-159">Dans votre navigateur, accédez à l’URL externe que vous avez configurée au cours de l’étape de publication.</span><span class="sxs-lookup"><span data-stu-id="8e528-159">In your browser, navigate to the external URL that you configured during the publish step.</span></span> <span data-ttu-id="8e528-160">L’écran d’accueil doit s’afficher et vous devez être en mesure de vous connecter avec le compte de test que vous avez configuré.</span><span class="sxs-lookup"><span data-stu-id="8e528-160">You should see the start screen, and be able to sign in with the test account you set up.</span></span>

![Tester votre application publiée](./media/application-proxy-publish-azure-portal/test-app.png)


## <a name="next-steps"></a><span data-ttu-id="8e528-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8e528-162">Next steps</span></span>
- <span data-ttu-id="8e528-163">[Télécharger des connecteurs](active-directory-application-proxy-enable.md) et [créer des groupes de connecteurs](active-directory-application-proxy-connectors-azure-portal.md) pour publier des applications sur des réseaux et emplacements distincts</span><span class="sxs-lookup"><span data-stu-id="8e528-163">[Download connectors](active-directory-application-proxy-enable.md) and [create connector groups](active-directory-application-proxy-connectors-azure-portal.md) to publish applications on separate networks and locations.</span></span>

- <span data-ttu-id="8e528-164">[Configurer l’authentification unique](application-proxy-sso-azure-portal.md) pour votre application récemment publiée</span><span class="sxs-lookup"><span data-stu-id="8e528-164">[Set up single sign-on](application-proxy-sso-azure-portal.md) for your newly published app</span></span>
