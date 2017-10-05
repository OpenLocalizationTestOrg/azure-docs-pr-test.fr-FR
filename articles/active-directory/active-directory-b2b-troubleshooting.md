---
title: "Résolution des problèmes d’Azure Active Directory B2B Collaboration | Microsoft Docs"
description: "Solutions pour les problèmes courants liés à Azure Active Directory B2B Collaboration"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/25/2017
ms.author: sasubram
ms.openlocfilehash: 2009cfc956a2703e268c9364996aa2d0fbd8f279
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="bd711-103">Résolution des problèmes d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="bd711-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="bd711-104">Voici des solutions pour les problèmes courants liés à Azure Active Directory (Azure AD) B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="bd711-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-the-people-picker"></a><span data-ttu-id="bd711-105">J’ai ajouté un utilisateur externe, mais je ne le vois pas dans mon carnet d’adresses global ou dans le sélecteur de personnes</span><span class="sxs-lookup"><span data-stu-id="bd711-105">I’ve added an external user but do not see them in my Global Address Book or in the people picker</span></span>

<span data-ttu-id="bd711-106">Dans les cas où les utilisateurs externes ne sont pas renseignés dans la liste, la réplication de l’objet peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="bd711-106">In cases where external users are not populated in the list, the object might take a few minutes to replicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="bd711-107">Un utilisateur invité B2B ne s’affiche pas dans le sélecteur de personnes SharePoint Online/OneDrive</span><span class="sxs-lookup"><span data-stu-id="bd711-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="bd711-108">La fonctionnalité de recherche d’utilisateurs invités existants dans le sélecteur de personnes SharePoint Online (SPO) est désactivée par défaut pour correspondre au comportement hérité.</span><span class="sxs-lookup"><span data-stu-id="bd711-108">The ability to search for existing guest users in the SharePoint Online (SPO) people picker is OFF by default to match legacy behavior.</span></span>

<span data-ttu-id="bd711-109">Vous pouvez activer cette fonctionnalité à l’aide du paramètre ShowPeoplePickerSuggestionsForGuestUsers au niveau du client et de la collection du site.</span><span class="sxs-lookup"><span data-stu-id="bd711-109">You can enable this feature by using the setting 'ShowPeoplePickerSuggestionsForGuestUsers' at the tenant and site collection level.</span></span> <span data-ttu-id="bd711-110">Vous pouvez définir cette fonctionnalité à l’aide des applets de commande Set-SPOTenant et Set-SPOSite qui permettent aux membres de rechercher tous les utilisateurs invités existants dans le répertoire.</span><span class="sxs-lookup"><span data-stu-id="bd711-110">You can set the feature using the Set-SPOTenant and Set-SPOSite cmdlets, which allow members to search all existing guest users in the directory.</span></span> <span data-ttu-id="bd711-111">Les modifications apportées à la portée du client n’affectent pas les sites SPO déjà configurés.</span><span class="sxs-lookup"><span data-stu-id="bd711-111">Changes in the tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="bd711-112">Des invitations ont été désactivées pour le répertoire</span><span class="sxs-lookup"><span data-stu-id="bd711-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="bd711-113">Si un message vous indique que vous n’êtes pas autorisé à inviter des utilisateurs, vérifiez que votre compte d’utilisateur est autorisé à inviter des utilisateurs externes sous Paramètres utilisateur :</span><span class="sxs-lookup"><span data-stu-id="bd711-113">If you are notified that you do not have permissions to invite users, verify that your user account is authorized to invite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="bd711-114">Si vous avez récemment modifié ces paramètres ou affecté le rôle d’inviteur d’invités à un utilisateur, vous devrez peut-être attendre 15 à 60 minutes avant que les modifications ne prennent effet.</span><span class="sxs-lookup"><span data-stu-id="bd711-114">If you have recently modified these settings or assigned the Guest Inviter role to a user, there might be a 15-60 minute delay before the changes take effect.</span></span>

## <a name="the-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="bd711-115">L’utilisateur que j’ai invité reçoit une erreur au cours de l’utilisation de l'invitation</span><span class="sxs-lookup"><span data-stu-id="bd711-115">The user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="bd711-116">Les erreurs courantes sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="bd711-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="bd711-117">L’administrateur de l’invité n’autorise pas la création d’utilisateurs EmailVerified dans leur client</span><span class="sxs-lookup"><span data-stu-id="bd711-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="bd711-118">Si vous invitez des utilisateurs dont l’organisation utilise un Azure Active Directory dans lequel le compte d’utilisateur spécifique n’existe pas (par exemple, l’utilisateur n’existe pas dans Azure AD contoso.com).</span><span class="sxs-lookup"><span data-stu-id="bd711-118">When inviting users whose organization is using Azure Active Directory, but where the specific user’s account does not exist (for example, the user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="bd711-119">L’administrateur de contoso.com peut avoir mis en place une stratégie empêchant la création d'utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="bd711-119">The administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="bd711-120">L’utilisateur doit contacter son administrateur pour déterminer si les utilisateurs externes sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="bd711-120">The user must check with their admin to determine if external users are allowed.</span></span> <span data-ttu-id="bd711-121">L’administrateur de l’utilisateur externe devra peut-être autoriser les utilisateurs vérifiés par e-mail dans son domaine (consultez cet [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) sur l’autorisation d’utilisateurs vérifiés par e-mail).</span><span class="sxs-lookup"><span data-stu-id="bd711-121">The external user’s admin may need to allow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="bd711-122">L'utilisateur externe n’existe pas déjà dans un domaine fédéré</span><span class="sxs-lookup"><span data-stu-id="bd711-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="bd711-123">Si vous utilisez l’authentification par fédération et si l’utilisateur n’existe pas déjà dans Azure Active Directory, l’utilisateur ne peut pas être invité.</span><span class="sxs-lookup"><span data-stu-id="bd711-123">If you are using federation authentication and the user does not already exist in Azure Active Directory, the user cannot be invited.</span></span>

<span data-ttu-id="bd711-124">Pour résoudre ce problème, administrateur de l’utilisateur externe doit synchroniser le compte d’utilisateur sur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bd711-124">To resolve this issue, the external user’s admin must synchronize the user’s account to Azure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="bd711-125">Comment synchroniser « \# », qui n’est normalement pas un caractère valide, avec Azure AD ?</span><span class="sxs-lookup"><span data-stu-id="bd711-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="bd711-126">« \# » est un caractère réservé dans les UPN pour les utilisateurs Azure AD B2B Collaboration ou externes, car le compte invité user@contoso.com devient user_contoso.com#EXT@fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="bd711-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because the invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com.</span></span> <span data-ttu-id="bd711-127">Par conséquent, il est impossible pour \# dans les UPN en local de se connecter au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bd711-127">Therefore, \# in UPNs coming from on-premises aren't allowed to sign in to the Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-to-a-synchronized-group"></a><span data-ttu-id="bd711-128">Je reçois une erreur lors de l’ajout d'utilisateurs externes à un groupe synchronisé</span><span class="sxs-lookup"><span data-stu-id="bd711-128">I receive an error when adding external users to a synchronized group</span></span>

<span data-ttu-id="bd711-129">Des utilisateurs externes peuvent être ajoutés uniquement à des groupes « affectés » ou « de sécurité » et non à des groupes contrôlés localement.</span><span class="sxs-lookup"><span data-stu-id="bd711-129">External users can be added only to “assigned” or “Security” groups and not to groups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-to-redeem"></a><span data-ttu-id="bd711-130">Mon utilisateur externe n’a pas reçu d'e-mail à utiliser</span><span class="sxs-lookup"><span data-stu-id="bd711-130">My external user did not receive an email to redeem</span></span>

<span data-ttu-id="bd711-131">L’invité doit contacter son fournisseur de services Internet ou contrôler son filtre de courriers indésirables pour s’assurer que l’adresse suivante est autorisée : Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="bd711-131">The invitee should check with their ISP or spam filter to ensure that the following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-the-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="bd711-132">Je remarque que le message personnalisé n’est parfois pas inclus dans les messages d’invitation</span><span class="sxs-lookup"><span data-stu-id="bd711-132">I notice that the custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="bd711-133">Par respect des lois sur la confidentialité, nos API n’incluent pas de messages personnalisés dans les invitations par e-mail lorsque :</span><span class="sxs-lookup"><span data-stu-id="bd711-133">To comply with privacy laws, our APIs do not include custom messages in the email invitation when:</span></span>

- <span data-ttu-id="bd711-134">L’inviteur n’a pas d’adresse e-mail dans le locataire à l’origine de l’invitation</span><span class="sxs-lookup"><span data-stu-id="bd711-134">The inviter doesn’t have an email address in the inviting tenant</span></span>
- <span data-ttu-id="bd711-135">Un principal AppService envoie l’invitation</span><span class="sxs-lookup"><span data-stu-id="bd711-135">When an appservice principal sends the invitation</span></span>

<span data-ttu-id="bd711-136">Si ce scénario est important pour vous, vous pouvez supprimer l’API qui envoie l’invitation par e-mail, et envoyer cette dernière au moyen d’un mécanisme de messagerie de votre choix.</span><span class="sxs-lookup"><span data-stu-id="bd711-136">If this scenario is important to you, you can suppress our API invitation email, and send it through the email mechanism of your choice.</span></span> <span data-ttu-id="bd711-137">Consultez un conseiller juridique dans votre organisation pour vous assurer que tout e-mail que vous envoyez est également conforme aux lois relatives à la vie privée.</span><span class="sxs-lookup"><span data-stu-id="bd711-137">Consult your organization’s legal counsel to make sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd711-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="bd711-138">Next steps</span></span>

<span data-ttu-id="bd711-139">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="bd711-139">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="bd711-140">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="bd711-140">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="bd711-141">Comment les administrateurs Azure Active Directory ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="bd711-141">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="bd711-142">Comment les professionnels de l’information ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="bd711-142">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="bd711-143">Éléments de l’e-mail d’invitation de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="bd711-143">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="bd711-144">Utilisation d’une invitation B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="bd711-144">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="bd711-145">Attribution de licences Azure AD B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="bd711-145">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="bd711-146">Questions fréquemment posées (FAQ) sur Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="bd711-146">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="bd711-147">API et personnalisation d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="bd711-147">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="bd711-148">Authentification multifacteur pour les utilisateurs B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="bd711-148">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="bd711-149">Ajouter des utilisateurs B2B Collaboration sans invitation</span><span class="sxs-lookup"><span data-stu-id="bd711-149">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="bd711-150">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd711-150">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
