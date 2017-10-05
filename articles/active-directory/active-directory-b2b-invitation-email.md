---
title: "Éléments de l’e-mail d’invitation de collaboration d’Azure Active Directory B2B | Microsoft Docs"
description: "Modèle d’e-mail d’invitation de collaboration d’Azure Active Directory B2B"
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
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 458a2cab13b7e83f120e0926a95d454070181dfb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="the-elements-of-the-b2b-collaboration-invitation-email"></a><span data-ttu-id="4b34e-103">Éléments de l’e-mail d’invitation de collaboration B2B</span><span class="sxs-lookup"><span data-stu-id="4b34e-103">The elements of the B2B collaboration invitation email</span></span>

<span data-ttu-id="4b34e-104">Les e-mails d’invitation sont un composant essentiel pour intégrer des partenaires comme utilisateurs de collaboration B2B dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b34e-104">Invitation emails are a critical component to bring partners on board as B2B collaboration users in Azure AD.</span></span> <span data-ttu-id="4b34e-105">Vous pouvez les utiliser pour augmenter le niveau de confiance du destinataire.</span><span class="sxs-lookup"><span data-stu-id="4b34e-105">You can use them to increase the recipient's trust.</span></span> <span data-ttu-id="4b34e-106">Vous pouvez ajouter de la légitimité et une preuve sociale à l’e-mail de sorte ce que le destinataire sélectionne sans crainte le bouton **Prise en main** pour accepter l’invitation.</span><span class="sxs-lookup"><span data-stu-id="4b34e-106">you can add legitimacy and social proof to the email, to make sure the recipient feels comfortable with selecting the **Get Started** button to accept the invitation.</span></span> <span data-ttu-id="4b34e-107">Cette approbation est un élément clé pour réduire les problèmes de partage.</span><span class="sxs-lookup"><span data-stu-id="4b34e-107">This trust is a key means to reduce sharing friction.</span></span> <span data-ttu-id="4b34e-108">Et elle vous permet aussi d’envoyer de superbes e-mails !</span><span class="sxs-lookup"><span data-stu-id="4b34e-108">And you also want to make the email look great!</span></span>

![E-mail d’invitation Azure AD B2b](media/active-directory-b2b-invitation-email/invitation-email.png)

## <a name="explaining-the-email"></a><span data-ttu-id="4b34e-110">Explication de l’e-mail</span><span class="sxs-lookup"><span data-stu-id="4b34e-110">Explaining the email</span></span>
<span data-ttu-id="4b34e-111">Examinons quelques-uns des éléments de l’e-mail pour savoir comment utiliser au mieux ces fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="4b34e-111">Let's look at a few elements of the email so you know how best to use their capabilities.</span></span>

### <a name="subject"></a><span data-ttu-id="4b34e-112">Objet</span><span class="sxs-lookup"><span data-stu-id="4b34e-112">Subject</span></span>
<span data-ttu-id="4b34e-113">L’objet de l’email suit le modèle suivant : vous êtes invité à rejoindre l’organisation &lt;nom_locataire&gt;</span><span class="sxs-lookup"><span data-stu-id="4b34e-113">The subject of the email follows the following pattern: You're invited to the &lt;tenantname&gt; organization</span></span>

### <a name="from-address"></a><span data-ttu-id="4b34e-114">Adresse de l’expéditeur</span><span class="sxs-lookup"><span data-stu-id="4b34e-114">From address</span></span>
<span data-ttu-id="4b34e-115">Nous utilisons un modèle similaire à LinkedIn pour l’adresse De.</span><span class="sxs-lookup"><span data-stu-id="4b34e-115">We use a LinkedIn-like pattern for the From address.</span></span>  <span data-ttu-id="4b34e-116">Vous devez faire apparaître clairement qui est l’inviteur et à quelle entreprise il appartient, mais aussi indiquer que l’e-mail provient d’une adresse e-mail Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4b34e-116">You should be clear who the inviter is and from which company, and also clarify that the email is coming from a Microsoft email address.</span></span> <span data-ttu-id="4b34e-117">Le format est : &lt;nom d’affichage de l’inviteur&gt; de &lt;nom_locataire&gt; (par le biais de Microsoft)invites@microsoft.com&gt;</span><span class="sxs-lookup"><span data-stu-id="4b34e-117">The format is: &lt;Display name of inviter&gt; from &lt;tenantname&gt; (via Microsoft) <invites@microsoft.com&gt;</span></span>

### <a name="reply-to"></a><span data-ttu-id="4b34e-118">Adresse de réponse</span><span class="sxs-lookup"><span data-stu-id="4b34e-118">Reply To</span></span>
<span data-ttu-id="4b34e-119">L’adresse e-mail de réponse est définie sur l’adresse e-mail de l’inviteur quand elle est disponible : ainsi, répondre à l’e-mail envoie un e-mail en retour à l’inviteur.</span><span class="sxs-lookup"><span data-stu-id="4b34e-119">The reply-to email is set to the inviter's email when available, so that replying to the email sends an email back to the inviter.</span></span>

### <a name="branding"></a><span data-ttu-id="4b34e-120">Personnalisation</span><span class="sxs-lookup"><span data-stu-id="4b34e-120">Branding</span></span>
<span data-ttu-id="4b34e-121">Les e-mails d’invitation de votre locataire utilisent la personnalisation d’entreprise que vous avez éventuellement définie pour votre locataire.</span><span class="sxs-lookup"><span data-stu-id="4b34e-121">The invitation emails from your tenant use the company branding that you may have set up for your tenant.</span></span> <span data-ttu-id="4b34e-122">Si vous voulez tirer parti de cette capacité, [voici](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) les informations de configuration.</span><span class="sxs-lookup"><span data-stu-id="4b34e-122">If you want to take advantage of this capability, [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) are the details on how to configure it.</span></span> <span data-ttu-id="4b34e-123">Le logo de la bannière s’affiche dans l’e-mail.</span><span class="sxs-lookup"><span data-stu-id="4b34e-123">The banner logo appears in the email.</span></span> <span data-ttu-id="4b34e-124">Suivez [ces instructions](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) relatives à la taille et à la qualité de l’image pour obtenir un résultat optimal.</span><span class="sxs-lookup"><span data-stu-id="4b34e-124">Follow the image size and quality instructions [here](https://docs.microsoft.com/azure/active-directory/active-directory-branding-custom-signon-azure-portal) for best results.</span></span> <span data-ttu-id="4b34e-125">En outre, le nom de l’entreprise apparaît également dans l’invite à l’action.</span><span class="sxs-lookup"><span data-stu-id="4b34e-125">In addition, the company name also shows up in the call to action.</span></span>

### <a name="call-to-action"></a><span data-ttu-id="4b34e-126">Invite à l’action</span><span class="sxs-lookup"><span data-stu-id="4b34e-126">Call to action</span></span>
<span data-ttu-id="4b34e-127">L’invite à l’action se compose de deux parties : explication de la raison pour laquelle le destinataire a reçu l’e-mail et ce qu’il est demandé comme action au destinataire.</span><span class="sxs-lookup"><span data-stu-id="4b34e-127">The call to action consists of two parts: explaining why the recipient has received the mail and what the recipient is being asked to do about it.</span></span>
- <span data-ttu-id="4b34e-128">La section « Pourquoi » peut être formulée selon le modèle suivant : Vous avez été invité à accéder à des applications dans l’organisation &lt;nom_locataire&gt;</span><span class="sxs-lookup"><span data-stu-id="4b34e-128">The "why" section can be addressed using the following pattern: You've been invited to access applications in the &lt;tenantname&gt; organization</span></span>

- <span data-ttu-id="4b34e-129">Et la section « Ce qu’il vous est demandé de faire » est indiquée par la présence du bouton **Bien démarrer**.</span><span class="sxs-lookup"><span data-stu-id="4b34e-129">And the "what you're being asked to do" section is indicated by the presence of the **Get Started** button.</span></span> <span data-ttu-id="4b34e-130">Quand le destinataire a été ajouté sans que des invitations soient nécessaires, ce bouton ne s’affiche pas.</span><span class="sxs-lookup"><span data-stu-id="4b34e-130">When the recipient has been added without the need for invitations, this button doesn't show up.</span></span>

### <a name="inviters-information"></a><span data-ttu-id="4b34e-131">Informations de l’inviteur</span><span class="sxs-lookup"><span data-stu-id="4b34e-131">Inviter's information</span></span>
<span data-ttu-id="4b34e-132">Le nom d’affichage de l’inviteur est inclus dans l’e-mail.</span><span class="sxs-lookup"><span data-stu-id="4b34e-132">The inviter's display name is included in the email.</span></span> <span data-ttu-id="4b34e-133">En outre, si vous avez configuré une image de profil pour votre compte Azure AD, l’e-mail d’invitation inclut également cette image.</span><span class="sxs-lookup"><span data-stu-id="4b34e-133">And in addition, if you've set up a profile picture for your Azure AD account, the inviting email will include that picture as well.</span></span> <span data-ttu-id="4b34e-134">Ces deux éléments sont destinés à améliorer la confiance de votre destinataire dans l’e-mail.</span><span class="sxs-lookup"><span data-stu-id="4b34e-134">Both are intended to increase your recipient's confidence in the email.</span></span>

<span data-ttu-id="4b34e-135">Si vous n’avez pas encore configuré votre image de profil, une icône comportant les initiales de l’inviteur remplace l’image, comme ceci :</span><span class="sxs-lookup"><span data-stu-id="4b34e-135">If you haven't yet set up your profile picture, an icon with the inviter's initials in place of the picture is shown:</span></span>

  ![affichage des initiales de l’inviteur](media/active-directory-b2b-invitation-email/inviters-initials.png)

### <a name="body"></a><span data-ttu-id="4b34e-137">body</span><span class="sxs-lookup"><span data-stu-id="4b34e-137">Body</span></span>
<span data-ttu-id="4b34e-138">Le corps contient le message que l’inviteur a composé ou transmis par le biais de l’API d’invitation.</span><span class="sxs-lookup"><span data-stu-id="4b34e-138">The body contains the message that the inviter composes or is passed through the invitation API.</span></span> <span data-ttu-id="4b34e-139">Il s’agit d’une simple zone de texte qui ne traite pas les balises HTML pour des raisons de sécurité.</span><span class="sxs-lookup"><span data-stu-id="4b34e-139">It is a text area, so it does not process HTML tags for security reasons.</span></span>

### <a name="footer-section"></a><span data-ttu-id="4b34e-140">Section Pied de page</span><span class="sxs-lookup"><span data-stu-id="4b34e-140">Footer section</span></span>
<span data-ttu-id="4b34e-141">Le pied de page contient la marque de la société Microsoft et permet au destinataire de savoir si l’e-mail a été envoyé à partir d’un alias non surveillé.</span><span class="sxs-lookup"><span data-stu-id="4b34e-141">The footer contains the Microsoft company brand and lets the recipient know if the email was sent from an unmonitored alias.</span></span> <span data-ttu-id="4b34e-142">Cas particuliers :</span><span class="sxs-lookup"><span data-stu-id="4b34e-142">Special cases:</span></span>

- <span data-ttu-id="4b34e-143">L’inviteur n’a pas d’adresse e-mail dans la location de l’inviteur</span><span class="sxs-lookup"><span data-stu-id="4b34e-143">The inviter doesn't have an email address in the inviting tenancy</span></span>

  ![image de l’inviteur sans adresse e-mail dans la location de l’inviteur](media/active-directory-b2b-invitation-email/inviter-no-email.png)


- <span data-ttu-id="4b34e-145">Le destinataire n’a pas besoin de réclamer l’invitation</span><span class="sxs-lookup"><span data-stu-id="4b34e-145">The recipient doesn't need to redeem the invitation</span></span>

  ![quand le destinataire n’a pas besoin de réclamer l’invitation](media/active-directory-b2b-invitation-email/when-recipient-doesnt-redeem.png)


## <a name="next-steps"></a><span data-ttu-id="4b34e-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4b34e-147">Next steps</span></span>

<span data-ttu-id="4b34e-148">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="4b34e-148">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="4b34e-149">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="4b34e-149">What is Azure AD B2B collaboration</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="4b34e-150">Comment les administrateurs Azure Active Directory ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="4b34e-150">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="4b34e-151">Comment les professionnels de l’information ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="4b34e-151">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="4b34e-152">Utilisation d’une invitation B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="4b34e-152">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="4b34e-153">Attribution de licences Azure AD B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="4b34e-153">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="4b34e-154">Résolution des problèmes d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="4b34e-154">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="4b34e-155">Questions fréquemment posées (FAQ) sur Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="4b34e-155">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="4b34e-156">API et personnalisation d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="4b34e-156">Azure Active Directory B2B collaboration API and customization</span></span>](active-directory-b2b-api.md)
* [<span data-ttu-id="4b34e-157">Authentification multifacteur pour les utilisateurs B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="4b34e-157">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="4b34e-158">Ajouter des utilisateurs B2B Collaboration sans invitation</span><span class="sxs-lookup"><span data-stu-id="4b34e-158">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="4b34e-159">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b34e-159">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
