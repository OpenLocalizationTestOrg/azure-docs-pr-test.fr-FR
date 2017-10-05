---
title: "Problème de connexion sur le site web du volet d’accès | Microsoft Docs"
description: "Conseils pour résoudre les problèmes que vous pouvez rencontrer lors de la connexion pour utiliser le volet d’accès"
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
ms.reviwer: japere
ms.openlocfilehash: 28d91237adf745e591b02322de7881c8122827ac
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-signing-in-to-the-access-panel-website"></a><span data-ttu-id="50891-103">Problème de connexion sur le site web du volet d’accès</span><span class="sxs-lookup"><span data-stu-id="50891-103">Problem signing in to the access panel website</span></span>

<span data-ttu-id="50891-104">Le volet d’accès est un portail Web qui permet à un utilisateur disposant d’un compte professionnel ou scolaire dans Azure Active Directory (Azure AD) d’afficher et de lancer des applications basées sur le cloud auxquelles l’administrateur Azure AD lui a accordé un accès.</span><span class="sxs-lookup"><span data-stu-id="50891-104">The Access Panel is a web-based portal which enables a user who has a work or school account in Azure Active Directory (Azure AD) to view and launch cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="50891-105">Un utilisateur disposant d’éditions Azure AD peut également utiliser des fonctionnalités de gestion de groupes et d’applications en libre-service par le biais du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="50891-105">A user who has Azure AD editions can also use self-service group and app management capabilities through the Access Panel.</span></span> <span data-ttu-id="50891-106">Le volet d’accès est distinct du portail Azure et n’exige pas des utilisateurs qu’ils aient un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="50891-106">The Access Panel is separate from the Azure portal and does not require users to have an Azure subscription.</span></span>

<span data-ttu-id="50891-107">Les utilisateurs peuvent se connecter au volet d’accès s’ils possèdent un compte professionnel ou scolaire dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50891-107">Users can sign in to the Access Panel if they have a work or school account in Azure AD.</span></span>

-   <span data-ttu-id="50891-108">Les utilisateurs peuvent être authentifiés par Azure AD directement.</span><span class="sxs-lookup"><span data-stu-id="50891-108">Users can be authenticated by Azure AD directly.</span></span>

-   <span data-ttu-id="50891-109">Les utilisateurs peuvent être authentifiés à l’aide d’Active Directory Federation Services (ADFS).</span><span class="sxs-lookup"><span data-stu-id="50891-109">Users can be authenticated by using Active Directory Federation Services (AD FS).</span></span>

-   <span data-ttu-id="50891-110">Les utilisateurs peuvent être authentifiés par Windows Server Active Directory.</span><span class="sxs-lookup"><span data-stu-id="50891-110">Users can be authenticated by Windows Server Active Directory.</span></span>

<span data-ttu-id="50891-111">Si un utilisateur dispose d’un abonnement Azure ou Office 365 et s’il utilise le portail Azure ou une application Office 365, il pourra utiliser le volet d’accès de façon transparente sans devoir se connecter à nouveau.</span><span class="sxs-lookup"><span data-stu-id="50891-111">If a user has a subscription for Azure or Office 365 and has been using the Azure portal or an Office 365 application, they'll be able to use the Access Panel seamlessly without needing to sign in again.</span></span> <span data-ttu-id="50891-112">Les utilisateurs qui ne sont pas authentifiés sont invités à se connecter à l’aide du nom d’utilisateur et du mot de passe correspondant à leur compte dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50891-112">Users who are not authenticated be prompted to sign in by using the username and password for their account in Azure AD.</span></span> <span data-ttu-id="50891-113">Si l’organisation a configuré la fédération, la saisie du nom d’utilisateur suffit.</span><span class="sxs-lookup"><span data-stu-id="50891-113">If the organization has configured federation, typing the username is sufficient.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="50891-114">Problèmes d’ordre général à vérifier en premier</span><span class="sxs-lookup"><span data-stu-id="50891-114">General issues to check first</span></span> 

-   <span data-ttu-id="50891-115">Assurez-vous que l’utilisateur se connecte à **l’URL correcte** : <https://myapps.microsoft.com></span><span class="sxs-lookup"><span data-stu-id="50891-115">Make sure the user is signing in to the **correct URL**: <https://myapps.microsoft.com></span></span>

-   <span data-ttu-id="50891-116">Vérifiez que l’URL figure dans la liste des **sites de confiance** du navigateur de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="50891-116">Make sure the user’s browser has added the URL to its **trusted sites**</span></span>

-   <span data-ttu-id="50891-117">Vérifiez que les connexions sont **activées** dans le compte de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="50891-117">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="50891-118">Vérifiez que le compte d’utilisateur **n’est pas verrouillé**.</span><span class="sxs-lookup"><span data-stu-id="50891-118">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="50891-119">Vérifiez que le **mot de passe de l’utilisateur n’a pas expiré ou qu’il n’a pas été oublié**.</span><span class="sxs-lookup"><span data-stu-id="50891-119">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="50891-120">Vérifiez que **Multi-Factor Authentication** ne bloque pas l’accès utilisateur.</span><span class="sxs-lookup"><span data-stu-id="50891-120">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="50891-121">Vérifiez qu’une **stratégie d’accès conditionnel** ou **stratégie de protection d’identité** ne bloque pas l’accès utilisateur.</span><span class="sxs-lookup"><span data-stu-id="50891-121">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="50891-122">Vérifiez que les **informations de contact d’authentification** de l’utilisateur sont à jour et permettent d’appliquer les stratégies d’accès conditionnel ou de Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="50891-122">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="50891-123">Essayez également d’effacer les cookies de votre navigateur, puis réessayez de vous connecter.</span><span class="sxs-lookup"><span data-stu-id="50891-123">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="meeting-browser-requirements-for-the-access-panel"></a><span data-ttu-id="50891-124">Configuration requise du navigateur pour le volet d’accès</span><span class="sxs-lookup"><span data-stu-id="50891-124">Meeting browser requirements for the Access Panel</span></span>

<span data-ttu-id="50891-125">Le volet d’accès nécessite un navigateur qui prend en charge JavaScript et dans lequel le CSS est activé.</span><span class="sxs-lookup"><span data-stu-id="50891-125">The Access Panel requires a browser that supports JavaScript and has CSS enabled.</span></span> <span data-ttu-id="50891-126">Pour utiliser l’authentification unique (SSO) par mot de passe dans le volet d’accès, l’extension du volet d’accès doit être installée dans le navigateur de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="50891-126">To use password-based single sign-on (SSO) in the Access Panel, the Access Panel extension must be installed in the user’s browser.</span></span> <span data-ttu-id="50891-127">Cette extension est téléchargée automatiquement lorsqu’un utilisateur sélectionne une application configurée pour l’authentification unique (SSO) avec mot de passe.</span><span class="sxs-lookup"><span data-stu-id="50891-127">This extension is downloaded automatically when a user selects an application that is configured for password-based SSO.</span></span>

<span data-ttu-id="50891-128">Pour l’authentification unique par mot de passe, les navigateurs de l’utilisateur final peuvent être :</span><span class="sxs-lookup"><span data-stu-id="50891-128">For password-based SSO, the end user’s browsers can be:</span></span>

-   <span data-ttu-id="50891-129">Internet Explorer 8, 9, 10, 11 -- sur Windows 7 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="50891-129">Internet Explorer 8, 9, 10, 11 -- on Windows 7 or later</span></span>

-   <span data-ttu-id="50891-130">Edge sur Windows 10 Édition anniversaire ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="50891-130">Edge on Windows 10 Anniversary Edition or later</span></span> 

-   <span data-ttu-id="50891-131">Chrome -- sur Windows 7 ou ultérieur, et sur Mac OS X ou ultérieur</span><span class="sxs-lookup"><span data-stu-id="50891-131">Chrome -- on Windows 7 or later, and on MacOS X or later</span></span>

-   <span data-ttu-id="50891-132">Firefox 26.0 ou ultérieur -- sur Windows XP SP2 ou ultérieur, et sur Mac OS X 10.6 ou ultérieur</span><span class="sxs-lookup"><span data-stu-id="50891-132">Firefox 26.0 or later -- on Windows XP SP2 or later, and on Mac OS X 10.6 or later</span></span>


## <a name="problems-with-the-users-account"></a><span data-ttu-id="50891-133">Problèmes avec le compte de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="50891-133">Problems with the user’s account</span></span>

<span data-ttu-id="50891-134">L’accès au volet d’accès peut être bloqué en raison d’un problème avec le compte de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="50891-134">Access to the Access Panel can be blocked due to a problem with the user’s account.</span></span> <span data-ttu-id="50891-135">Voici quelques méthodes pour vous aider à résoudre les problèmes avec les utilisateurs et leurs paramètres de compte :</span><span class="sxs-lookup"><span data-stu-id="50891-135">Below are some ways you can troubleshoot and solve problems with users and their account settings:</span></span>

-   [<span data-ttu-id="50891-136">Vérifier l’existence d’un compte d’utilisateur dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50891-136">Check if a user account exists in Azure Active Directory</span></span>](#check-if-a-user-account-exists-in-azure-active-directory)

-   [<span data-ttu-id="50891-137">Vérifier l’état du compte d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="50891-137">Check a user’s account status</span></span>](#check-a-users-account-status)

-   [<span data-ttu-id="50891-138">Réinitialiser le mot de passe d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="50891-138">Reset a user’s password</span></span>](#reset-a-users-password)

-   [<span data-ttu-id="50891-139">Activer la réinitialisation du mot de passe libre-service</span><span class="sxs-lookup"><span data-stu-id="50891-139">Enable self-service password reset</span></span>](#enable-self-service-password-reset)

-   [<span data-ttu-id="50891-140">Vérifier l’état Multi-Factor Authentication d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="50891-140">Check a user’s multi-factor authentication status</span></span>](#check-a-users-multi-factor-authentication-status)

-   [<span data-ttu-id="50891-141">Vérifier les informations de contact de l’authentification d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="50891-141">Check a user’s authentication contact info</span></span>](#check-a-users-authentication-contact-info)

-   [<span data-ttu-id="50891-142">Vérifier les appartenances d’un utilisateur à des groupes</span><span class="sxs-lookup"><span data-stu-id="50891-142">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="50891-143">Vérifier les licences affectées à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="50891-143">Check a user’s assigned licenses</span></span>](#check-a-users-assigned-licenses)

-   [<span data-ttu-id="50891-144">Affecter une licence à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="50891-144">Assign a user a license</span></span>](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a><span data-ttu-id="50891-145">Vérifier l’existence d’un compte d’utilisateur dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50891-145">Check if a user account exists in Azure Active Directory</span></span>

<span data-ttu-id="50891-146">Pour vérifier si le compte d’un utilisateur est présent, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="50891-146">To check if a user’s account is present, follow the steps below:</span></span>

1.  <span data-ttu-id="50891-147">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général**.</span><span class="sxs-lookup"><span data-stu-id="50891-147">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="50891-148">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="50891-148">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="50891-149">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="50891-149">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="50891-150">Cliquez sur **Utilisateurs et groupes** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="50891-150">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="50891-151">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="50891-151">click **All users**.</span></span>

6.  <span data-ttu-id="50891-152">**Recherchez** l’utilisateur qui vous intéresse et **cliquez sur la ligne** à sélectionner.</span><span class="sxs-lookup"><span data-stu-id="50891-152">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="50891-153">Vérifiez les propriétés de l’objet utilisateur pour vous assurer qu’elles apparaissent comme prévu et qu’aucune donnée n’est manquante.</span><span class="sxs-lookup"><span data-stu-id="50891-153">Check the properties of the user object to be sure that they look as you expect and no data is missing.</span></span>

### <a name="check-a-users-account-status"></a><span data-ttu-id="50891-154">Vérifier l’état du compte d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="50891-154">Check a user’s account status</span></span>

<span data-ttu-id="50891-155">Pour vérifier l’état du compte d’un utilisateur, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="50891-155">To check a user’s account status, follow the steps below:</span></span>

1.  <span data-ttu-id="50891-156">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général**.</span><span class="sxs-lookup"><span data-stu-id="50891-156">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="50891-157">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="50891-157">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="50891-158">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="50891-158">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="50891-159">Cliquez sur **Utilisateurs et groupes** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="50891-159">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="50891-160">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="50891-160">click **All users**.</span></span>

6.  <span data-ttu-id="50891-161">**Recherchez** l’utilisateur qui vous intéresse et **cliquez sur la ligne** à sélectionner.</span><span class="sxs-lookup"><span data-stu-id="50891-161">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="50891-162">Cliquez sur **Profil**.</span><span class="sxs-lookup"><span data-stu-id="50891-162">click **Profile**.</span></span>

8.  <span data-ttu-id="50891-163">Sous **Paramètres**, assurez-vous que **Bloquer la connexion** est défini sur **Non**.</span><span class="sxs-lookup"><span data-stu-id="50891-163">Under **Settings** ensure that **Block sign in** is set to **No**.</span></span>

### <a name="reset-a-users-password"></a><span data-ttu-id="50891-164">Réinitialiser le mot de passe d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="50891-164">Reset a user’s password</span></span>

<span data-ttu-id="50891-165">Pour réinitialiser le mot de passe d’un utilisateur, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="50891-165">To reset a user’s password, follow the steps below:</span></span>

1.  <span data-ttu-id="50891-166">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général**.</span><span class="sxs-lookup"><span data-stu-id="50891-166">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="50891-167">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="50891-167">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="50891-168">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="50891-168">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="50891-169">Cliquez sur **Utilisateurs et groupes** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="50891-169">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="50891-170">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="50891-170">click **All users**.</span></span>

6.  <span data-ttu-id="50891-171">**Recherchez** l’utilisateur qui vous intéresse et **cliquez sur la ligne** à sélectionner.</span><span class="sxs-lookup"><span data-stu-id="50891-171">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="50891-172">Cliquez sur le bouton **Réinitialiser le mot de passe** en haut du panneau Utilisateur.</span><span class="sxs-lookup"><span data-stu-id="50891-172">click the **Reset password** button at the top of the user blade.</span></span>

8.  <span data-ttu-id="50891-173">Cliquez sur le bouton **Réinitialiser le mot de passe** sur le panneau **Réinitialiser le mot de passe** qui s’affiche.</span><span class="sxs-lookup"><span data-stu-id="50891-173">click the **Reset password** button on the **Reset password** blade that appears.</span></span>

9.  <span data-ttu-id="50891-174">Copiez le **mot de passe temporaire** ou **entrez un nouveau mot de passe** pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="50891-174">Copy the **temporary password** or **enter a new password** for the user.</span></span>

10. <span data-ttu-id="50891-175">Communiquez ce nouveau mot de passe à l’utilisateur. Ce dernier devra changer ce mot de passe lors de sa prochaine connexion à Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="50891-175">Communicate this new password to the user, they be required to change this password during their next sign in to Azure Active Directory.</span></span>

### <a name="enable-self-service-password-reset"></a><span data-ttu-id="50891-176">Activer la réinitialisation du mot de passe libre-service</span><span class="sxs-lookup"><span data-stu-id="50891-176">Enable self-service password reset</span></span>

<span data-ttu-id="50891-177">Pour activer la réinitialisation du mot de passe libre-service, suivez les étapes de déploiement ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="50891-177">To enable self-service password reset, follow the deployment steps below:</span></span>

-   [<span data-ttu-id="50891-178">Permettre aux utilisateurs de réinitialiser leur mot de passe Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50891-178">Enable users to reset their Azure Active Directory passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [<span data-ttu-id="50891-179">Permettre aux utilisateurs de réinitialiser ou de modifier leur mot de passe Active Directory Azure local</span><span class="sxs-lookup"><span data-stu-id="50891-179">Enable users to reset or change their Active Directory on-premises passwords</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a><span data-ttu-id="50891-180">Vérifier l’état Multi-Factor Authentication d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="50891-180">Check a user’s multi-factor authentication status</span></span>

<span data-ttu-id="50891-181">Pour vérifier l’état Multi-Factor Authentication d’un utilisateur, suivez les étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="50891-181">To check a user’s multi-factor authentication status, follow the steps below:</span></span>

1.  <span data-ttu-id="50891-182">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général**.</span><span class="sxs-lookup"><span data-stu-id="50891-182">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="50891-183">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="50891-183">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="50891-184">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="50891-184">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="50891-185">Cliquez sur **Utilisateurs et groupes** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="50891-185">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="50891-186">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="50891-186">click **All users**.</span></span>

6.  <span data-ttu-id="50891-187">Cliquez sur le bouton **Multi-Factor Authentication** en haut du panneau.</span><span class="sxs-lookup"><span data-stu-id="50891-187">click the **Multi-Factor Authentication** button at the top of the blade.</span></span>

7.  <span data-ttu-id="50891-188">Une fois le **portail d’administration Multi-Factor Authentication** chargé, assurez-vous de vous trouver sur l’onglet **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="50891-188">Once the **Multi-Factor Authentication Administration Portal** loads, ensure you are on the **Users** tab.</span></span>

8.  <span data-ttu-id="50891-189">Recherchez l’utilisateur dans la liste des utilisateurs au moyen de la recherche, du filtrage ou du tri.</span><span class="sxs-lookup"><span data-stu-id="50891-189">Find the user in the list of users by searching, filtering, or sorting.</span></span>

9.  <span data-ttu-id="50891-190">Sélectionnez l’utilisateur dans la liste des utilisateurs et **activez**, **désactivez** ou **appliquez** la Multi-Factor Authentication comme souhaité.</span><span class="sxs-lookup"><span data-stu-id="50891-190">Select the user from the list of users and **Enable**, **Disable**, or **Enforce** multi-factor authentication as desired.</span></span>

   >[!NOTE]
   ><span data-ttu-id="50891-191">Si un utilisateur est dans un état **Appliqué**, vous pouvez définir le définir sur **Désactivé** de façon temporaire pour lui permettre de revenir à son compte.</span><span class="sxs-lookup"><span data-stu-id="50891-191">If a user is in an **Enforced** state, you may set them to **Disabled** temporarily to let them back into their account.</span></span> <span data-ttu-id="50891-192">Une fois qu’il est revenu dans son compte, vous pouvez ensuite modifier son état en le redéfinissant sur **Activé** pour lui demander d’enregistrer à nouveau ses informations de contact à sa prochaine connexion.</span><span class="sxs-lookup"><span data-stu-id="50891-192">Once they are back in, you can then change their state to **Enabled** again to require them to re-register their contact information during their next sign in.</span></span> <span data-ttu-id="50891-193">Sinon, vous pouvez suivre les étapes décrites dans [Vérifier les informations de contact de l’authentification d’un utilisateur](#check-a-users-authentication-contact-info) pour vérifier ou définir ces données à sa place.</span><span class="sxs-lookup"><span data-stu-id="50891-193">Alternatively, you can follow the steps in the [Check a user’s authentication contact info](#check-a-users-authentication-contact-info) to verify or set this data for them.</span></span>
   >
   >

### <a name="check-a-users-authentication-contact-info"></a><span data-ttu-id="50891-194">Vérifier les informations de contact de l’authentification d’un utilisateur</span><span class="sxs-lookup"><span data-stu-id="50891-194">Check a user’s authentication contact info</span></span>

<span data-ttu-id="50891-195">Pour vérifier les informations de contact de l’authentification d’un utilisateur utilisées pour Multi-Factor Authentication, Accès conditionnel, Identity Protection et Réinitialisation de mot de passe, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="50891-195">To check a user’s authentication contact info used for Multi-factor authentication, Conditional Access, Identity Protection, and Password Reset, follow the steps below:</span></span>

1.  <span data-ttu-id="50891-196">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général**.</span><span class="sxs-lookup"><span data-stu-id="50891-196">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="50891-197">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="50891-197">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="50891-198">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="50891-198">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="50891-199">Cliquez sur **Utilisateurs et groupes** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="50891-199">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="50891-200">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="50891-200">click **All users**.</span></span>

6.  <span data-ttu-id="50891-201">**Recherchez** l’utilisateur qui vous intéresse et **cliquez sur la ligne** à sélectionner.</span><span class="sxs-lookup"><span data-stu-id="50891-201">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="50891-202">Cliquez sur **Profil**.</span><span class="sxs-lookup"><span data-stu-id="50891-202">click **Profile**.</span></span>

8.  <span data-ttu-id="50891-203">Faites défiler la page jusqu’aux **informations de contact d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="50891-203">Scroll down to **Authentication contact info**.</span></span>

9.  <span data-ttu-id="50891-204">**Passez en revue** les données enregistrées pour l’utilisateur et mettez-les à jour si besoin.</span><span class="sxs-lookup"><span data-stu-id="50891-204">**Review** the data registered for the user and update as needed.</span></span>

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="50891-205">Vérifier les appartenances d’un utilisateur à des groupes</span><span class="sxs-lookup"><span data-stu-id="50891-205">Check a user’s group memberships</span></span>

<span data-ttu-id="50891-206">Pour vérifier l’appartenance d’un utilisateur à des groupes, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="50891-206">To check a user’s group memberships, follow the steps below:</span></span>

1.  <span data-ttu-id="50891-207">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général**.</span><span class="sxs-lookup"><span data-stu-id="50891-207">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="50891-208">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="50891-208">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="50891-209">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="50891-209">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="50891-210">Cliquez sur **Utilisateurs et groupes** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="50891-210">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="50891-211">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="50891-211">click **All users**.</span></span>

6.  <span data-ttu-id="50891-212">**Recherchez** l’utilisateur qui vous intéresse et **cliquez sur la ligne** à sélectionner.</span><span class="sxs-lookup"><span data-stu-id="50891-212">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="50891-213">Cliquez sur **Groupes** pour afficher les groupes dont l’utilisateur est membre.</span><span class="sxs-lookup"><span data-stu-id="50891-213">click **Groups** to see which groups the user is a member of.</span></span>

### <a name="check-a-users-assigned-licenses"></a><span data-ttu-id="50891-214">Vérifier les licences affectées à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="50891-214">Check a user’s assigned licenses</span></span>

<span data-ttu-id="50891-215">Pour vérifier les licences affectées à un utilisateur, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="50891-215">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="50891-216">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="50891-216">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="50891-217">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="50891-217">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="50891-218">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="50891-218">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="50891-219">Cliquez sur **Utilisateurs et groupes** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="50891-219">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="50891-220">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="50891-220">click **All users**.</span></span>

6.  <span data-ttu-id="50891-221">**Recherchez** l’utilisateur qui vous intéresse et **cliquez sur la ligne** pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="50891-221">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="50891-222">Cliquez sur **Licences** pour voir quelles licences sont actuellement affectées à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="50891-222">click **Licenses** to see which licenses the user currently has assigned.</span></span>

### <a name="assign-a-user-a-license"></a><span data-ttu-id="50891-223">Affecter une licence à un utilisateur</span><span class="sxs-lookup"><span data-stu-id="50891-223">Assign a user a license</span></span> 

<span data-ttu-id="50891-224">Pour affecter une licence à un utilisateur, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="50891-224">To assign a license to a user, follow the steps below:</span></span>

1.  <span data-ttu-id="50891-225">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="50891-225">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="50891-226">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="50891-226">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="50891-227">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="50891-227">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="50891-228">Cliquez sur **Utilisateurs et groupes** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="50891-228">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="50891-229">Cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="50891-229">click **All users**.</span></span>

6.  <span data-ttu-id="50891-230">**Recherchez** l’utilisateur qui vous intéresse et **cliquez sur la ligne** pour le sélectionner.</span><span class="sxs-lookup"><span data-stu-id="50891-230">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="50891-231">Cliquez sur **Licences** pour voir quelles licences sont actuellement affectées à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="50891-231">click **Licenses** to see which licenses the user currently has assigned.</span></span>

8.  <span data-ttu-id="50891-232">Cliquez sur le bouton **Attribuer**.</span><span class="sxs-lookup"><span data-stu-id="50891-232">click the **Assign** button.</span></span>

9.  <span data-ttu-id="50891-233">Sélectionnez **un ou plusieurs produits** dans la liste des produits disponibles.</span><span class="sxs-lookup"><span data-stu-id="50891-233">Select **one or more products** from the list of available products.</span></span>

10. <span data-ttu-id="50891-234">**Facultatif** Cliquez sur l’élément **Options d’affectation** pour affecter les produits de façon granulaire.</span><span class="sxs-lookup"><span data-stu-id="50891-234">**Optional** click the **assignment options** item to granularly assign products.</span></span> <span data-ttu-id="50891-235">Cliquez sur **OK** lorsque l’opération est terminée.</span><span class="sxs-lookup"><span data-stu-id="50891-235">Click **Ok** when this is completed.</span></span>

11. <span data-ttu-id="50891-236">Cliquez sur le bouton **Attribuer** pour affecter ces licences à cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="50891-236">Click the **Assign** button to assign these licenses to this user.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="50891-237">Si ces étapes de dépannage ne résolvent pas le problème</span><span class="sxs-lookup"><span data-stu-id="50891-237">If these troubleshooting steps do not resolve the issue</span></span>

<span data-ttu-id="50891-238">Ouvrez un ticket de support en fournissant les informations suivantes, dans la mesure du possible :</span><span class="sxs-lookup"><span data-stu-id="50891-238">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="50891-239">ID d’erreur de corrélation</span><span class="sxs-lookup"><span data-stu-id="50891-239">Correlation error ID</span></span>

-   <span data-ttu-id="50891-240">Nom d’utilisateur principal (adresse de messagerie de l’utilisateur)</span><span class="sxs-lookup"><span data-stu-id="50891-240">UPN (user email address)</span></span>

-   <span data-ttu-id="50891-241">ID client</span><span class="sxs-lookup"><span data-stu-id="50891-241">Tenant ID</span></span>

-   <span data-ttu-id="50891-242">Type de navigateur</span><span class="sxs-lookup"><span data-stu-id="50891-242">Browser type</span></span>

-   <span data-ttu-id="50891-243">Fuseau horaire et heure/période à laquelle l’erreur se produit</span><span class="sxs-lookup"><span data-stu-id="50891-243">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="50891-244">Traces Fiddler</span><span class="sxs-lookup"><span data-stu-id="50891-244">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="50891-245">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="50891-245">Next steps</span></span>
[<span data-ttu-id="50891-246">Fournir une authentification unique à vos applications avec le proxy d’application</span><span class="sxs-lookup"><span data-stu-id="50891-246">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
