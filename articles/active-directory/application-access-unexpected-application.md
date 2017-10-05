---
title: "Application inattendue dans ma liste d’applications | Microsoft Docs"
description: "Guide pratique pour afficher toutes les applications dans votre client et comprendre comment les applications apparaissent dans votre liste Toutes les applications sous Applications d’entreprise"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 0f8136cb066fa6e3e4a8dd06e34b9f866e3916f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="unexpected-application-in-my-applications-list"></a><span data-ttu-id="52d2a-103">Application inattendue dans ma liste d’applications</span><span class="sxs-lookup"><span data-stu-id="52d2a-103">Unexpected application in my applications list</span></span>

<span data-ttu-id="52d2a-104">Cet article vous aide à comprendre comment les applications apparaissent dans votre liste **Toutes les applications** sous **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="52d2a-104">This article help you to understand how applications appear in your **All Applications** list under **Enterprise Applications**.</span></span> 

## <a name="how-to-see-all-applications-in-your-tenant"></a><span data-ttu-id="52d2a-105">Guide pratique pour afficher toutes les applications dans votre client</span><span class="sxs-lookup"><span data-stu-id="52d2a-105">How to see all applications in your tenant</span></span>

<span data-ttu-id="52d2a-106">Pour afficher toutes les applications dans votre client, vous devez utiliser le contrôle **Filtrer** pour afficher **Toutes les applications** sous la liste **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="52d2a-106">To see all the applications in your tenant, you need to use the **Filter** control to show **All Applications** under the **All Applications** list.</span></span> <span data-ttu-id="52d2a-107">Pour ce faire, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="52d2a-107">To do this, follow the steps below:</span></span>

1.  <span data-ttu-id="52d2a-108">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur.**</span><span class="sxs-lookup"><span data-stu-id="52d2a-108">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="52d2a-109">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="52d2a-109">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="52d2a-110">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52d2a-110">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="52d2a-111">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="52d2a-111">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="52d2a-112">Cliquez sur **Toutes les applications** pour afficher une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="52d2a-112">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="52d2a-113">Cliquez sur le contrôle **Filtrer** en haut de la **liste de toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="52d2a-113">click the use the **Filter** control at the top of the **All Applications List**.</span></span>

7.  <span data-ttu-id="52d2a-114">Sur le panneau **Filtrer**, définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="52d2a-114">On the **Filter** blade, set the **Show** option to **All Applications.**</span></span>

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a><span data-ttu-id="52d2a-115">Pourquoi une application spécifique apparaît-elle dans ma liste de toutes les applications ?</span><span class="sxs-lookup"><span data-stu-id="52d2a-115">Why does a specific application appear in my all applications list?</span></span>

<span data-ttu-id="52d2a-116">Lors du filtrage avec **Toutes les applications**, la **liste** **Toutes les applications** affiche chaque objet Principal de service dans votre client.</span><span class="sxs-lookup"><span data-stu-id="52d2a-116">When filtered to **All Applications**, the **All Applications** **List** shows every Service Principal object in your tenant.</span></span> <span data-ttu-id="52d2a-117">Les objets Principal de service peuvent apparaître dans cette liste de différentes façons :</span><span class="sxs-lookup"><span data-stu-id="52d2a-117">Service Principal objects can appear in this list in a various ways:</span></span>

1.  <span data-ttu-id="52d2a-118">Lorsque vous ajoutez une application à partir de la galerie d’applications, y compris :</span><span class="sxs-lookup"><span data-stu-id="52d2a-118">When you add any application from the application gallery, including:</span></span>

   1. <span data-ttu-id="52d2a-119">**Applications de la galerie Azure AD** : applications pré-intégrées pour l’authentification unique avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52d2a-119">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

   2. <span data-ttu-id="52d2a-120">**Applications du proxy d’application** : applications s’exécutant dans votre environnement local, pour lesquelles vous souhaitez utiliser l’authentification unique en externe.</span><span class="sxs-lookup"><span data-stu-id="52d2a-120">**Application Proxy Applications** – An application running in your on-premises environment that you want to provide secure single-sign on to externally.</span></span>

   3. <span data-ttu-id="52d2a-121">**Applications personnalisées** : applications que votre organisation souhaite développer sur la plateforme de développement d’applications Azure AD, mais qui n’existent pas encore.</span><span class="sxs-lookup"><span data-stu-id="52d2a-121">**Custom-developed Applications** – An application that your organization wishes to develop on the Azure AD Application Development Platform, but that may not exist yet.</span></span>

   4. <span data-ttu-id="52d2a-122">**Applications hors galerie** : créez vos propres applications !</span><span class="sxs-lookup"><span data-stu-id="52d2a-122">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="52d2a-123">Tous les liens web et toutes les applications disposant d’un champ de nom d’utilisateur et de mot de passe prennent en charge les protocoles SAML ou OpenID Connect, ou prennent en charge SCIM pour l’intégration à l’authentification unique avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52d2a-123">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish to integrate for single sign-on with Azure AD.</span></span>

2.  <span data-ttu-id="52d2a-124">Lors de l’inscription ou de l’ouverture d’une session, une application <sup>tierce</sup> intégrée à Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="52d2a-124">When signing up for, or signing in to, a 3<sup>rd</sup> party application integrated with Azure Active Directory.</span></span> <span data-ttu-id="52d2a-125">Exemple : [Smartsheet](https://app.smartsheet.com/b/home) ou [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span><span class="sxs-lookup"><span data-stu-id="52d2a-125">One example of this is [Smartsheet](https://app.smartsheet.com/b/home) or [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).</span></span>

3.  <span data-ttu-id="52d2a-126">Lors de l’inscription ou de l’ajout d’une licence à un utilisateur ou à un groupe à une première application, par exemple [Microsoft Office 365](http://products.office.com/).</span><span class="sxs-lookup"><span data-stu-id="52d2a-126">When signing up for, or adding a license to a user or a group to a first party application, like [Microsoft Office 365](http://products.office.com/).</span></span>

4.  <span data-ttu-id="52d2a-127">Lorsque vous ajoutez une inscription pour une nouvelle ’application en créant une application personnalisée à l’aide du [Registre d’application](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span><span class="sxs-lookup"><span data-stu-id="52d2a-127">When you add a new application registration by creating a custom-developed application using the [Application Registry](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).</span></span>

5.  <span data-ttu-id="52d2a-128">Lorsque vous ajoutez une inscription pour une nouvelle ’application en créant une application personnalisée à l’aide du [Portail d’inscription des applications V2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span><span class="sxs-lookup"><span data-stu-id="52d2a-128">When you add a new application registration by creating a custom-developed application using the [V2.0 Application Registration Portal](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).</span></span>

6.  <span data-ttu-id="52d2a-129">Lorsque vous ajoutez une application que vous développez à l’aide des [méthodes d’authentification ASP.net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) ou des [Services connectés](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx) de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="52d2a-129">When you add an application you’re developing using Visual Studio’s [ASP.net Authentication Methods](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) or [Connected Services](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).</span></span>

7.  <span data-ttu-id="52d2a-130">Lorsque vous créez un objet Principal de service à l’aide du [module Azure AD PowerShell](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="52d2a-130">When you create a service principal object using the [Azure AD PowerShell Module](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

8.  <span data-ttu-id="52d2a-131">Lorsque vous [donnez votre consentement à une application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) en tant qu’administrateur afin d’utiliser les données dans votre client.</span><span class="sxs-lookup"><span data-stu-id="52d2a-131">When you [consent to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) as an administrator to use data in your tenant.</span></span>

9.  <span data-ttu-id="52d2a-132">Lorsqu’un [utilisateur donne son consentement à une application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) afin d’utiliser les données dans votre client.</span><span class="sxs-lookup"><span data-stu-id="52d2a-132">When a [user consents to an application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) to use data in your tenant.</span></span>

10. <span data-ttu-id="52d2a-133">Lorsque vous activez certains services qui stockent des données dans votre client.</span><span class="sxs-lookup"><span data-stu-id="52d2a-133">When you enable certain services that store data in your tenant.</span></span> <span data-ttu-id="52d2a-134">Un exemple est la réinitialisation du mot de passe, opération modélisée comme un principal de service pour stocker de façon sécurisée la stratégie de réinitialisation de votre mot de passe.</span><span class="sxs-lookup"><span data-stu-id="52d2a-134">One example of this is Password Reset, which is modeled as a service principal to store your password reset policy securely.</span></span>

<span data-ttu-id="52d2a-135">Pour plus d’informations sur la façon dont les applications sont ajoutées à votre annuaire, lisez [Comment et pourquoi les applications sont ajoutées à Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span><span class="sxs-lookup"><span data-stu-id="52d2a-135">To get more details on how apps are added to your directory, read [How and why applications are added to Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="52d2a-136">Je souhaite supprimer l’attribution d’une application à un utilisateur ou groupe spécifique</span><span class="sxs-lookup"><span data-stu-id="52d2a-136">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="52d2a-137">Pour supprimer l’attribution d’une application à un utilisateur ou groupe, suivez les étapes répertoriées dans l’article [Supprimer l’attribution d’une application à un utilisateur ou groupe à partir d’une application d’entreprise dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="52d2a-137">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

## <a name="i-want-to-disable-all-access-to-an-application-for-every-user"></a><span data-ttu-id="52d2a-138">Je souhaite désactiver tous les accès à une application pour chaque utilisateur</span><span class="sxs-lookup"><span data-stu-id="52d2a-138">I want to disable all access to an application for every user</span></span>

<span data-ttu-id="52d2a-139">Pour désactiver toutes les connexions des utilisateurs à une application, suivez les étapes répertoriées dans l’article [Désactiver les connexions des utilisateurs à une application d’entreprise dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="52d2a-139">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="52d2a-140">Je veux complètement supprimer une passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="52d2a-140">I want to delete an application entirely</span></span>

<span data-ttu-id="52d2a-141">Pour **supprimer une application**, suivez les instructions ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="52d2a-141">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="52d2a-142">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur.**</span><span class="sxs-lookup"><span data-stu-id="52d2a-142">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="52d2a-143">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="52d2a-143">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="52d2a-144">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52d2a-144">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="52d2a-145">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="52d2a-145">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="52d2a-146">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="52d2a-146">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="52d2a-147">Si l’application que vous recherchez n’apparaît pas, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="52d2a-147">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="52d2a-148">Sélectionnez l’application que vous voulez supprimer.</span><span class="sxs-lookup"><span data-stu-id="52d2a-148">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="52d2a-149">Une l’application chargée, cliquez sur l’icône **Supprimer** dans le panneau supérieur **Vue d’ensemble** de l’application.</span><span class="sxs-lookup"><span data-stu-id="52d2a-149">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="52d2a-150">Je veux désactiver toutes les futures opérations de consentement de l’utilisateur pour n’importe quelle application</span><span class="sxs-lookup"><span data-stu-id="52d2a-150">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="52d2a-151">La désactivation du consentement de l’utilisateur pour votre annuaire entier empêche les utilisateurs finaux de donner leur consentement pour n’importe quelle application.</span><span class="sxs-lookup"><span data-stu-id="52d2a-151">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="52d2a-152">Les administrateurs peuvent toujours donner leur consentement au nom de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="52d2a-152">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="52d2a-153">Pour en savoir plus sur le consentement de l’application et les conditions pour donner ou refuser ce consentement, lisez la rubrique [Comprendre le consentement de l’utilisateur et de l’administrateur](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="52d2a-153">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="52d2a-154">Pour **désactiver toutes les futures opérations de consentement de l’utilisateur dans votre annuaire entier**, suivez les instructions ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="52d2a-154">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="52d2a-155">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="52d2a-155">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="52d2a-156">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="52d2a-156">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="52d2a-157">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52d2a-157">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="52d2a-158">Cliquez sur **Utilisateurs et groupes** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="52d2a-158">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="52d2a-159">Cliquez sur **Paramètres utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="52d2a-159">click **User settings**.</span></span>

6.  <span data-ttu-id="52d2a-160">Désactivez toutes les futures opérations de consentement de l’utilisateur en définissant l’option **Les utilisateurs peuvent autoriser les applications à accéder à leurs données** sur **Non**, puis cliquez sur le bouton **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="52d2a-160">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52d2a-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="52d2a-161">Next steps</span></span>
[<span data-ttu-id="52d2a-162">Gestion des applications avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52d2a-162">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
