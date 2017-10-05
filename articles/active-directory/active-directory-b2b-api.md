---
title: "API et personnalisation d’Azure Active Directory B2B Collaboration | Microsoft Docs"
description: "Azure Active Directory B2B Collaboration prend en charge les relations interentreprises en permettant aux partenaires commerciaux d’accéder de façon sélective à vos applications d’entreprise"
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
ms.date: 04/11/2017
ms.author: sasubram
ms.openlocfilehash: c85e05b38b4a9525e13ec510a17b7ef4841198d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="6201f-103">API et personnalisation d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="6201f-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="6201f-104">De nombreux clients nous ont indiqué qu’ils souhaitent personnaliser le processus d’invitation d’une manière qui convient mieux à leurs organisations.</span><span class="sxs-lookup"><span data-stu-id="6201f-104">We've had many customers tell us that they want to customize the invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="6201f-105">Avec notre API, cela est possible.</span><span class="sxs-lookup"><span data-stu-id="6201f-105">With our API, you can do just that.</span></span> [<span data-ttu-id="6201f-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span><span class="sxs-lookup"><span data-stu-id="6201f-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span></span>](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-the-invitation-api"></a><span data-ttu-id="6201f-107">Fonctionnalités de l’API d’invitation</span><span class="sxs-lookup"><span data-stu-id="6201f-107">Capabilities of the invitation API</span></span>
<span data-ttu-id="6201f-108">L’API offre les fonctionnalités suivantes :</span><span class="sxs-lookup"><span data-stu-id="6201f-108">The API offers the following capabilities:</span></span>

1. <span data-ttu-id="6201f-109">Invitez un utilisateur externe avec *n’importe quelle* adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="6201f-109">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="6201f-110">Personnalisez l’emplacement vers lequel vous souhaitez diriger vos utilisateurs une fois qu’ils ont accepté l’invitation.</span><span class="sxs-lookup"><span data-stu-id="6201f-110">Customize where you want your users to land after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="6201f-111">Choisissez d’envoyer l’e-mail d’invitation standard par notre intermédiaire</span><span class="sxs-lookup"><span data-stu-id="6201f-111">Choose to send the standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="6201f-112">accompagné d’un message au destinataire que vous pouvez personnaliser</span><span class="sxs-lookup"><span data-stu-id="6201f-112">with a message to the recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="6201f-113">Et choisissez de mettre en copie des personnes que vous souhaitez informer de votre invitation de ce collaborateur.</span><span class="sxs-lookup"><span data-stu-id="6201f-113">And choose to cc: people you want to keep in the loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="6201f-114">Ou personnalisez entièrement votre flux de travail d’invitation et d’accueil en choisissant de ne pas envoyer des notifications via Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6201f-114">Or completely customize your invitation and onboarding workflow by choosing not to send notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="6201f-115">Dans ce cas, vous obtenez une URL d’échange de la part de l’API que vous pouvez incorporer dans un modèle d’e-mail, un message instantané ou toute autre méthode de distribution de votre choix.</span><span class="sxs-lookup"><span data-stu-id="6201f-115">In this case, you get back a redemption URL from the API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="6201f-116">Enfin, si vous êtes un administrateur, vous pouvez choisir d’inviter l’utilisateur en tant que membre.</span><span class="sxs-lookup"><span data-stu-id="6201f-116">Finally, if you are an admin, you can choose to invite the user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="6201f-117">Modèle d’autorisation</span><span class="sxs-lookup"><span data-stu-id="6201f-117">Authorization model</span></span>
<span data-ttu-id="6201f-118">L’API peut être exécutée dans les modes d’autorisation suivants :</span><span class="sxs-lookup"><span data-stu-id="6201f-118">The API can be run in the following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="6201f-119">Mode Application + Utilisateur</span><span class="sxs-lookup"><span data-stu-id="6201f-119">App + User mode</span></span>
<span data-ttu-id="6201f-120">Dans ce mode, toute personne utilisant l’API doit disposer des autorisations permettant de créer des invitations B2B.</span><span class="sxs-lookup"><span data-stu-id="6201f-120">In this mode, whoever is using the API needs to have the permissions to be create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="6201f-121">Mode Application uniquement</span><span class="sxs-lookup"><span data-stu-id="6201f-121">App only mode</span></span>
<span data-ttu-id="6201f-122">Dans le contexte Application uniquement, l’application a besoin des étendues User.ReadWrite.All ou Directory.ReadWrite.All pour que l’invitation réussisse.</span><span class="sxs-lookup"><span data-stu-id="6201f-122">In app only context, the app needs the User.ReadWrite.All or Directory.ReadWrite.All scopes for the invitation to succeed.</span></span>

<span data-ttu-id="6201f-123">Pour plus d’informations, consultez : https://graph.microsoft.io/docs/authorization/permission_scopes</span><span class="sxs-lookup"><span data-stu-id="6201f-123">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="6201f-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6201f-124">PowerShell</span></span>
<span data-ttu-id="6201f-125">Il est désormais possible d’utiliser PowerShell pour ajouter et inviter facilement des utilisateurs externes au sein d’une organisation.</span><span class="sxs-lookup"><span data-stu-id="6201f-125">It is now possible to use PowerShell to add and invite external users to an organization easily.</span></span> <span data-ttu-id="6201f-126">Créez une invitation à l’aide de l’applet de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6201f-126">Create an invitation using the cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="6201f-127">Vous pouvez utiliser les options suivantes :</span><span class="sxs-lookup"><span data-stu-id="6201f-127">You can use the following options:</span></span>

* <span data-ttu-id="6201f-128">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="6201f-128">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="6201f-129">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="6201f-129">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="6201f-130">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="6201f-130">-SendInvitationMessage</span></span>
* <span data-ttu-id="6201f-131">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="6201f-131">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="6201f-132">Vous pouvez également extraire la référence d’API d’invitation dans [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span><span class="sxs-lookup"><span data-stu-id="6201f-132">You can also check out the invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6201f-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6201f-133">Next steps</span></span>

<span data-ttu-id="6201f-134">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="6201f-134">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="6201f-135">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="6201f-135">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="6201f-136">Comment les administrateurs Azure Active Directory ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="6201f-136">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="6201f-137">Comment les professionnels de l’information ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="6201f-137">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="6201f-138">Éléments de l’e-mail d’invitation de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="6201f-138">The elements of the B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="6201f-139">Utilisation d’une invitation B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="6201f-139">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="6201f-140">Attribution de licences Azure AD B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="6201f-140">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="6201f-141">Résolution des problèmes d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="6201f-141">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="6201f-142">Questions fréquemment posées (FAQ) sur Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="6201f-142">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="6201f-143">Authentification multifacteur pour les utilisateurs B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="6201f-143">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="6201f-144">Ajouter des utilisateurs B2B Collaboration sans invitation</span><span class="sxs-lookup"><span data-stu-id="6201f-144">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="6201f-145">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6201f-145">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
