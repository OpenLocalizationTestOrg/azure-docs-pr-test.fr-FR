---
title: aaaTroubleshooting Azure Active Directory B2B collaboration | Documents Microsoft
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
ms.openlocfilehash: 6fcfd7e543cd7bb833225f8aa56e332e7a989faf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-b2b-collaboration"></a><span data-ttu-id="77d49-103">Résolution des problèmes d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="77d49-103">Troubleshooting Azure Active Directory B2B collaboration</span></span>

<span data-ttu-id="77d49-104">Voici des solutions pour les problèmes courants liés à Azure Active Directory (Azure AD) B2B Collaboration.</span><span class="sxs-lookup"><span data-stu-id="77d49-104">Here are some remedies for common problems with Azure Active Directory (Azure AD) B2B collaboration.</span></span>


## <a name="ive-added-an-external-user-but-do-not-see-them-in-my-global-address-book-or-in-hello-people-picker"></a><span data-ttu-id="77d49-105">Vous avez ajouté un utilisateur externe mais ne sont pas visibles dans le carnet d’adresses Global ou dans le sélecteur de personnes hello</span><span class="sxs-lookup"><span data-stu-id="77d49-105">I’ve added an external user but do not see them in my Global Address Book or in hello people picker</span></span>

<span data-ttu-id="77d49-106">Dans les cas où les utilisateurs externes ne sont pas renseignés dans la liste de hello, objet de hello peut prendre quelques minutes tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="77d49-106">In cases where external users are not populated in hello list, hello object might take a few minutes tooreplicate.</span></span>

## <a name="a-b2b-guest-user-is-not-showing-up-in-sharepoint-onlineonedrive-people-picker"></a><span data-ttu-id="77d49-107">Un utilisateur invité B2B ne s’affiche pas dans le sélecteur de personnes SharePoint Online/OneDrive</span><span class="sxs-lookup"><span data-stu-id="77d49-107">A B2B guest user is not showing up in SharePoint Online/OneDrive people picker</span></span> 
 
<span data-ttu-id="77d49-108">toosearch de capacité Hello pour les utilisateurs invités dans le sélecteur de personnes hello SharePoint Online (OFS) est désactivé par défaut hérités toomatch.</span><span class="sxs-lookup"><span data-stu-id="77d49-108">hello ability toosearch for existing guest users in hello SharePoint Online (SPO) people picker is OFF by default toomatch legacy behavior.</span></span>

<span data-ttu-id="77d49-109">Vous pouvez activer cette fonctionnalité à l’aide de hello la définition 'ShowPeoplePickerSuggestionsForGuestUsers' à la collection de site et de client hello niveau.</span><span class="sxs-lookup"><span data-stu-id="77d49-109">You can enable this feature by using hello setting 'ShowPeoplePickerSuggestionsForGuestUsers' at hello tenant and site collection level.</span></span> <span data-ttu-id="77d49-110">Vous pouvez définir la fonction hello hello Set-SPOTenant et SPOSite de jeu d’applets de commande, qui permettent aux membres toosearch tous les utilisateurs invités existants dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="77d49-110">You can set hello feature using hello Set-SPOTenant and Set-SPOSite cmdlets, which allow members toosearch all existing guest users in hello directory.</span></span> <span data-ttu-id="77d49-111">Modifications dans l’étendue de locataire hello n’affectent pas les sites simulé déjà configurés.</span><span class="sxs-lookup"><span data-stu-id="77d49-111">Changes in hello tenant scope do not affect already provisioned SPO sites.</span></span>

## <a name="invitations-have-been-disabled-for-directory"></a><span data-ttu-id="77d49-112">Des invitations ont été désactivées pour le répertoire</span><span class="sxs-lookup"><span data-stu-id="77d49-112">Invitations have been disabled for directory</span></span>

<span data-ttu-id="77d49-113">Si vous êtes informé que vous n’avez pas les autorisations accordées aux utilisateurs de tooinvite, vérifiez que votre compte d’utilisateur est autorisé tooinvite des utilisateurs externes sous Paramètres utilisateur :</span><span class="sxs-lookup"><span data-stu-id="77d49-113">If you are notified that you do not have permissions tooinvite users, verify that your user account is authorized tooinvite external users under User Settings:</span></span>

![](media/active-directory-b2b-troubleshooting/external-user-settings.png)

<span data-ttu-id="77d49-114">Si vous avez récemment modifié ces paramètres ou hello invité le rôle tooa utilisateur attribué, il peut y avoir un délai de 15 à 60 minutes que hello modifications prennent effet.</span><span class="sxs-lookup"><span data-stu-id="77d49-114">If you have recently modified these settings or assigned hello Guest Inviter role tooa user, there might be a 15-60 minute delay before hello changes take effect.</span></span>

## <a name="hello-user-that-i-invited-is-receiving-an-error-during-redemption"></a><span data-ttu-id="77d49-115">utilisateur Hello qui vous a invité reçoit une erreur au cours de l’échange</span><span class="sxs-lookup"><span data-stu-id="77d49-115">hello user that I invited is receiving an error during redemption</span></span>

<span data-ttu-id="77d49-116">Les erreurs courantes sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="77d49-116">Common errors include:</span></span>

### <a name="invitees-admin-has-disallowed-emailverified-users-from-being-created-in-their-tenant"></a><span data-ttu-id="77d49-117">L’administrateur de l’invité n’autorise pas la création d’utilisateurs EmailVerified dans leur client</span><span class="sxs-lookup"><span data-stu-id="77d49-117">Invitee’s Admin has disallowed EmailVerified Users from being created in their tenant</span></span>

<span data-ttu-id="77d49-118">Lorsque invitant les utilisateurs dont l’organisation utilise Azure Active Directory, mais où hello compte d’utilisateur spécifique n’existe pas (par exemple, hello utilisateur n’existe pas dans Azure AD contoso.com).</span><span class="sxs-lookup"><span data-stu-id="77d49-118">When inviting users whose organization is using Azure Active Directory, but where hello specific user’s account does not exist (for example, hello user does not exist in Azure AD contoso.com).</span></span> <span data-ttu-id="77d49-119">administrateur Hello contoso.com qui peut exister une stratégie empêchant les utilisateurs d’en cours de création.</span><span class="sxs-lookup"><span data-stu-id="77d49-119">hello administrator of contoso.com may have a policy in place preventing users from being created.</span></span> <span data-ttu-id="77d49-120">utilisateur de Hello doit vérifier avec leur toodetermine administrateur si des utilisateurs externes sont autorisés.</span><span class="sxs-lookup"><span data-stu-id="77d49-120">hello user must check with their admin toodetermine if external users are allowed.</span></span> <span data-ttu-id="77d49-121">Hello administrateur de l’utilisateur externe peut-être tooallow vérifié par courrier électronique des utilisateurs dans leur domaine (consultez ce [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) sur permettant aux utilisateurs de vérifié par courrier électronique).</span><span class="sxs-lookup"><span data-stu-id="77d49-121">hello external user’s admin may need tooallow Email Verified users in their domain (see this [article](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0) on allowing Email Verified Users).</span></span>

![](media/active-directory-b2b-troubleshooting/allow-email-verified-users.png)

### <a name="external-user-does-not-exist-already-in-a-federated-domain"></a><span data-ttu-id="77d49-122">L'utilisateur externe n’existe pas déjà dans un domaine fédéré</span><span class="sxs-lookup"><span data-stu-id="77d49-122">External user does not exist already in a federated domain</span></span>

<span data-ttu-id="77d49-123">Si vous utilisez l’authentification de la fédération et l’utilisateur de hello n’existe pas déjà dans Azure Active Directory, utilisateur de hello ne peut pas être invité.</span><span class="sxs-lookup"><span data-stu-id="77d49-123">If you are using federation authentication and hello user does not already exist in Azure Active Directory, hello user cannot be invited.</span></span>

<span data-ttu-id="77d49-124">tooresolve ce problème, hello administrateur de l’utilisateur externe doit synchroniser tooAzure de compte d’utilisateur hello Active Directory.</span><span class="sxs-lookup"><span data-stu-id="77d49-124">tooresolve this issue, hello external user’s admin must synchronize hello user’s account tooAzure Active Directory.</span></span>

## <a name="how-does--which-is-not-normally-a-valid-character-sync-with-azure-ad"></a><span data-ttu-id="77d49-125">Comment synchroniser « \# », qui n’est normalement pas un caractère valide, avec Azure AD ?</span><span class="sxs-lookup"><span data-stu-id="77d49-125">How does ‘\#’, which is not normally a valid character, sync with Azure AD?</span></span>

<span data-ttu-id="77d49-126">«\#» est un caractère réservé dans les noms d’utilisateurs principaux pour Azure AD B2B collaboration ou externes, parce que hello invité compte user@contoso.com devient user_contoso.com#EXT@fabrikam.onmicrosoft.com. Par conséquent, \# dans UPN provenant du site ne sont pas autorisés toosign dans toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="77d49-126">“\#” is a reserved character in UPNs for Azure AD B2B collaboration or external users, because hello invited account user@contoso.com becomes user_contoso.com#EXT@fabrikam.onmicrosoft.com. Therefore, \# in UPNs coming from on-premises aren't allowed toosign in toohello Azure portal.</span></span> 

## <a name="i-receive-an-error-when-adding-external-users-tooa-synchronized-group"></a><span data-ttu-id="77d49-127">Je reçois une erreur lors de l’ajout d’utilisateurs externes tooa synchronisé de groupe</span><span class="sxs-lookup"><span data-stu-id="77d49-127">I receive an error when adding external users tooa synchronized group</span></span>

<span data-ttu-id="77d49-128">Les utilisateurs externes peuvent être ajoutés uniquement trop « affecté » ou les groupes « Sécurité » et pas les toogroups sont contrôlées sur site.</span><span class="sxs-lookup"><span data-stu-id="77d49-128">External users can be added only too“assigned” or “Security” groups and not toogroups that are mastered on-premises.</span></span>

## <a name="my-external-user-did-not-receive-an-email-tooredeem"></a><span data-ttu-id="77d49-129">Mon utilisateur externe n’a pas reçu un tooredeem par courrier électronique</span><span class="sxs-lookup"><span data-stu-id="77d49-129">My external user did not receive an email tooredeem</span></span>

<span data-ttu-id="77d49-130">l’invité de Hello devez vérifier auprès de leur fournisseur de services Internet ou tooensure de filtre de courrier indésirable hello l’adresse suivante est autorisée :Invites@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="77d49-130">hello invitee should check with their ISP or spam filter tooensure that hello following address is allowed: Invites@microsoft.com</span></span>

## <a name="i-notice-that-hello-custom-message-does-not-get-included-with-invitation-messages-at-times"></a><span data-ttu-id="77d49-131">Je remarque que message personnalisé hello n’obtient pas inclus dans les messages d’invitation à des moments</span><span class="sxs-lookup"><span data-stu-id="77d49-131">I notice that hello custom message does not get included with invitation messages at times</span></span>

<span data-ttu-id="77d49-132">toocomply avec les lois sur la confidentialité, nos API n’inclure pas les messages personnalisés dans le message d’invitation hello lorsque :</span><span class="sxs-lookup"><span data-stu-id="77d49-132">toocomply with privacy laws, our APIs do not include custom messages in hello email invitation when:</span></span>

- <span data-ttu-id="77d49-133">émetteur de l’invitation Hello n’a pas une adresse de messagerie dans hello inviter les clients</span><span class="sxs-lookup"><span data-stu-id="77d49-133">hello inviter doesn’t have an email address in hello inviting tenant</span></span>
- <span data-ttu-id="77d49-134">Lorsqu’un principal de service d’applications envoie d’invitation hello</span><span class="sxs-lookup"><span data-stu-id="77d49-134">When an appservice principal sends hello invitation</span></span>

<span data-ttu-id="77d49-135">Si ce scénario est tooyou important, vous pouvez supprimer l’e-mail d’invitation de nos API et l’envoyer via le mécanisme de messagerie hello de votre choix.</span><span class="sxs-lookup"><span data-stu-id="77d49-135">If this scenario is important tooyou, you can suppress our API invitation email, and send it through hello email mechanism of your choice.</span></span> <span data-ttu-id="77d49-136">Consultez toomake de conseiller juridique de votre organisation que tout message électronique envoyer de cette façon est également conforme à la législation.</span><span class="sxs-lookup"><span data-stu-id="77d49-136">Consult your organization’s legal counsel toomake sure any email you send this way also complies with privacy laws.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77d49-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="77d49-137">Next steps</span></span>

<span data-ttu-id="77d49-138">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="77d49-138">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="77d49-139">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="77d49-139">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="77d49-140">Comment les administrateurs Azure Active Directory ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="77d49-140">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="77d49-141">Comment les professionnels de l’information ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="77d49-141">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="77d49-142">éléments Hello Hello e-mail d’invitation B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="77d49-142">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="77d49-143">Utilisation d’une invitation B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="77d49-143">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="77d49-144">Attribution de licences Azure AD B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="77d49-144">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="77d49-145">Questions fréquemment posées (FAQ) sur Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="77d49-145">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="77d49-146">API et personnalisation d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="77d49-146">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="77d49-147">Authentification multifacteur pour les utilisateurs B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="77d49-147">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="77d49-148">Ajouter des utilisateurs B2B Collaboration sans invitation</span><span class="sxs-lookup"><span data-stu-id="77d49-148">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="77d49-149">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77d49-149">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
