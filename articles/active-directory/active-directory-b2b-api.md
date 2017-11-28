---
title: aaaAzure Active Directory B2B collaboration API et la personnalisation | Documents Microsoft
description: "Azure Active Directory B2B collaboration prend en charge les relations de votre société croisée en activant tooselectively partenaires commerciaux un accès à vos applications d’entreprise"
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
ms.openlocfilehash: 2609971ffa5d2ebc9466c61f4e4af11f5b045ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2b-collaboration-api-and-customization"></a><span data-ttu-id="f0512-103">API et personnalisation d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="f0512-103">Azure Active Directory B2B collaboration API and customization</span></span>

<span data-ttu-id="f0512-104">Nous avons eu de nombreux clients nous dire qu’ils veulent des processus d’invitation hello toocustomize d’une manière qui convient le mieux à leur organisation.</span><span class="sxs-lookup"><span data-stu-id="f0512-104">We've had many customers tell us that they want toocustomize hello invitation process in a way that works best for their organizations.</span></span> <span data-ttu-id="f0512-105">Avec notre API, cela est possible.</span><span class="sxs-lookup"><span data-stu-id="f0512-105">With our API, you can do just that.</span></span> [<span data-ttu-id="f0512-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span><span class="sxs-lookup"><span data-stu-id="f0512-106">https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation</span></span>](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)

## <a name="capabilities-of-hello-invitation-api"></a><span data-ttu-id="f0512-107">Fonctionnalités de l’invitation hello API</span><span class="sxs-lookup"><span data-stu-id="f0512-107">Capabilities of hello invitation API</span></span>
<span data-ttu-id="f0512-108">Hello API offre hello suivant de fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="f0512-108">hello API offers hello following capabilities:</span></span>

1. <span data-ttu-id="f0512-109">Invitez un utilisateur externe avec *n’importe quelle* adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="f0512-109">Invite an external user with *any* email address.</span></span>

    ```
    "invitedUserDisplayName": "Sam"
    "invitedUserEmailAddress": "gsamoogle@gmail.com"
    ```

2. <span data-ttu-id="f0512-110">Personnaliser votre tooland utilisateurs où vous souhaitez une fois qu’ils acceptent leur invitation.</span><span class="sxs-lookup"><span data-stu-id="f0512-110">Customize where you want your users tooland after they accept their invitation.</span></span>

    ```
    "inviteRedirectUrl": "https://myapps.microsoft.com/"
    ```

3. <span data-ttu-id="f0512-111">Choisissez toosend hello invitation standard courrier par nous</span><span class="sxs-lookup"><span data-stu-id="f0512-111">Choose toosend hello standard invitation mail through us</span></span>

    ```
    "sendInvitationMessage": true
    ```

  <span data-ttu-id="f0512-112">avec un destinataire toohello message que vous pouvez personnaliser</span><span class="sxs-lookup"><span data-stu-id="f0512-112">with a message toohello recipient that you can customize</span></span>

    ```
    "customizedMessageBody": "Hello Sam, let's collaborate!"
    ```

4. <span data-ttu-id="f0512-113">Choisissez toocc : personnes tookeep Bonjour boucle sur votre invitation ce collaborateur.</span><span class="sxs-lookup"><span data-stu-id="f0512-113">And choose toocc: people you want tookeep in hello loop about your inviting this collaborator.</span></span>

5. <span data-ttu-id="f0512-114">Ou de personnaliser entièrement votre invitation et l’intégration de flux de travail en choisissant pas toosend notifications via Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0512-114">Or completely customize your invitation and onboarding workflow by choosing not toosend notifications through Azure AD.</span></span>

    ```
    "sendInvitationMessage": false
    ```

  <span data-ttu-id="f0512-115">Dans ce cas, vous récupérez une URL de remboursement des hello API que vous pouvez incorporer dans un modèle de courrier électronique, messagerie instantanée ou autre méthode de distribution de votre choix.</span><span class="sxs-lookup"><span data-stu-id="f0512-115">In this case, you get back a redemption URL from hello API that you can embed in an email template, IM, or other distribution method of your choice.</span></span>

6. <span data-ttu-id="f0512-116">Enfin, si vous êtes un administrateur, vous pouvez choisir utilisateur de hello tooinvite en tant que membre.</span><span class="sxs-lookup"><span data-stu-id="f0512-116">Finally, if you are an admin, you can choose tooinvite hello user as member.</span></span>

    ```
    "invitedUserType": "Member"
    ```


## <a name="authorization-model"></a><span data-ttu-id="f0512-117">Modèle d’autorisation</span><span class="sxs-lookup"><span data-stu-id="f0512-117">Authorization model</span></span>
<span data-ttu-id="f0512-118">Hello API peut être exécuté dans hello suivant les modes d’autorisation :</span><span class="sxs-lookup"><span data-stu-id="f0512-118">hello API can be run in hello following authorization modes:</span></span>

### <a name="app--user-mode"></a><span data-ttu-id="f0512-119">Mode Application + Utilisateur</span><span class="sxs-lookup"><span data-stu-id="f0512-119">App + User mode</span></span>
<span data-ttu-id="f0512-120">Dans ce mode, la personne qui utilise les besoins de hello API toohave hello autorisations toobe créer des invitations à participer à B2B.</span><span class="sxs-lookup"><span data-stu-id="f0512-120">In this mode, whoever is using hello API needs toohave hello permissions toobe create B2B invitations.</span></span>

### <a name="app-only-mode"></a><span data-ttu-id="f0512-121">Mode Application uniquement</span><span class="sxs-lookup"><span data-stu-id="f0512-121">App only mode</span></span>
<span data-ttu-id="f0512-122">Dans le contexte uniquement d’application, application hello doit hello User.ReadWrite.All ou Directory.ReadWrite.All étendues pour hello invitation toosucceed.</span><span class="sxs-lookup"><span data-stu-id="f0512-122">In app only context, hello app needs hello User.ReadWrite.All or Directory.ReadWrite.All scopes for hello invitation toosucceed.</span></span>

<span data-ttu-id="f0512-123">Pour plus d’informations, consultez : https://graph.microsoft.io/docs/authorization/permission_scopes</span><span class="sxs-lookup"><span data-stu-id="f0512-123">For more information, refer to: https://graph.microsoft.io/docs/authorization/permission_scopes</span></span>


## <a name="powershell"></a><span data-ttu-id="f0512-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f0512-124">PowerShell</span></span>
<span data-ttu-id="f0512-125">Il est maintenant possible toouse PowerShell tooadd et inviter des utilisateurs externes tooan organisation facilement.</span><span class="sxs-lookup"><span data-stu-id="f0512-125">It is now possible toouse PowerShell tooadd and invite external users tooan organization easily.</span></span> <span data-ttu-id="f0512-126">Créer une invitation à l’aide d’applet de commande hello :</span><span class="sxs-lookup"><span data-stu-id="f0512-126">Create an invitation using hello cmdlet:</span></span>

```
New-AzureADMSInvitation
```

<span data-ttu-id="f0512-127">Vous pouvez utiliser hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="f0512-127">You can use hello following options:</span></span>

* <span data-ttu-id="f0512-128">-InvitedUserDisplayName</span><span class="sxs-lookup"><span data-stu-id="f0512-128">-InvitedUserDisplayName</span></span>
* <span data-ttu-id="f0512-129">-InvitedUserEmailAddress</span><span class="sxs-lookup"><span data-stu-id="f0512-129">-InvitedUserEmailAddress</span></span>
* <span data-ttu-id="f0512-130">-SendInvitationMessage</span><span class="sxs-lookup"><span data-stu-id="f0512-130">-SendInvitationMessage</span></span>
* <span data-ttu-id="f0512-131">-InvitedUserMessageInfo</span><span class="sxs-lookup"><span data-stu-id="f0512-131">-InvitedUserMessageInfo</span></span>

<span data-ttu-id="f0512-132">Vous pouvez également extraire référence des API d’invitation hello dans [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span><span class="sxs-lookup"><span data-stu-id="f0512-132">You can also check out hello invitation API reference in [https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0512-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f0512-133">Next steps</span></span>

<span data-ttu-id="f0512-134">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="f0512-134">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="f0512-135">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="f0512-135">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="f0512-136">Comment les administrateurs Azure Active Directory ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="f0512-136">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="f0512-137">Comment les professionnels de l’information ajoutent-ils des utilisateurs B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="f0512-137">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="f0512-138">éléments Hello Hello e-mail d’invitation B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="f0512-138">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="f0512-139">Utilisation d’une invitation B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="f0512-139">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="f0512-140">Attribution de licences Azure AD B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="f0512-140">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="f0512-141">Résolution des problèmes d’Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="f0512-141">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="f0512-142">Questions fréquemment posées (FAQ) sur Azure Active Directory B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="f0512-142">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="f0512-143">Authentification multifacteur pour les utilisateurs B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="f0512-143">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="f0512-144">Ajouter des utilisateurs B2B Collaboration sans invitation</span><span class="sxs-lookup"><span data-stu-id="f0512-144">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="f0512-145">Index d’articles pour la gestion des applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0512-145">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
