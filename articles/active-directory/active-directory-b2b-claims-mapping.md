---
title: "collaboration aaaB2B prétend mappage dans Azure Active Directory | Documents Microsoft"
description: "référence de mappage des revendications pour Azure Active Directory B2B Collaboration"
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
ms.date: 03/15/2017
ms.author: sasubram
ms.openlocfilehash: 9e26085e91a6004b2f11286ae9c1df133bd47341
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="b2b-collaboration-user-claims-mapping-in-azure-active-directory"></a><span data-ttu-id="dad70-103">Mappage des revendications d’utilisateur B2B Collaboration dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dad70-103">B2B collaboration user claims mapping in Azure Active Directory</span></span>

<span data-ttu-id="dad70-104">Azure Active Directory (Azure AD) prend en charge la personnalisation des revendications hello émises dans un jeton SAML de hello pour les utilisateurs de collaboration B2B.</span><span class="sxs-lookup"><span data-stu-id="dad70-104">Azure Active Directory (Azure AD) supports customizing hello claims issued in hello SAML token for B2B collaboration users.</span></span> <span data-ttu-id="dad70-105">Lorsqu’un utilisateur s’authentifie toohello application, Azure AD émet une application toohello jeton SAML qui contient des informations (ou les revendications) sur l’utilisateur hello qui identifie de façon unique les.</span><span class="sxs-lookup"><span data-stu-id="dad70-105">When a user authenticates toohello application, Azure AD issues a SAML token toohello app that contains information (or claims) about hello user that uniquely identifies them.</span></span> <span data-ttu-id="dad70-106">Par défaut, cela inclut le nom d’utilisateur, adresse de messagerie, prénom et nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="dad70-106">By default, this includes hello user's user name, email address, first name, and last name.</span></span> <span data-ttu-id="dad70-107">Vous pouvez afficher ou modifier des revendications hello envoyées Bonjour application de toohello jeton SAML sous l’onglet attributs de hello.</span><span class="sxs-lookup"><span data-stu-id="dad70-107">You can view or edit hello claims sent in hello SAML token toohello application under hello Attributes tab.</span></span>

<span data-ttu-id="dad70-108">Il existe deux raisons pour lesquelles vous devrez peut-être les revendications de hello tooedit émises dans un jeton SAML de hello.</span><span class="sxs-lookup"><span data-stu-id="dad70-108">There are two possible reasons why you might need tooedit hello claims issued in hello SAML token.</span></span>

1. <span data-ttu-id="dad70-109">application Hello a été écrit toorequire une autre valeur de revendication URI ou des valeurs de revendication</span><span class="sxs-lookup"><span data-stu-id="dad70-109">hello application has been written toorequire a different set of claim URIs or claim values</span></span>

2. <span data-ttu-id="dad70-110">Votre application nécessite toobe de revendication NameIdentifier hello autre chose qu’un nom principal d’utilisateur hello stockée dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dad70-110">Your application requires hello NameIdentifier claim toobe something other than hello user principal name stored in Azure Active Directory.</span></span>

  ![Afficher les revendications dans le jeton SAML](media/active-directory-b2b-claims-mapping/view-claims-in-saml-token.png)

<span data-ttu-id="dad70-112">Pour plus d’informations sur comment tooadd et modifier des revendications, consultez cet article sur la personnalisation des revendications, [personnalisation des revendications émises dans un jeton SAML de hello pour les applications pré-intégrées dans Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span><span class="sxs-lookup"><span data-stu-id="dad70-112">For information on how tooadd and edit claims, check out this article on claims customization, [Customizing claims issued in hello SAML token for pre-integrated apps in Azure Active Directory](develop/active-directory-saml-claims-customization.md).</span></span> <span data-ttu-id="dad70-113">Pour les utilisateurs B2B Collaboration, le mappage entre locataires de NameID et UPN est empêché pour des raisons de sécurité.</span><span class="sxs-lookup"><span data-stu-id="dad70-113">For B2B collaboration users, mapping NameID and UPN cross-tenant are prevented for security reasons.</span></span>


## <a name="next-steps"></a><span data-ttu-id="dad70-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dad70-114">Next steps</span></span>

<span data-ttu-id="dad70-115">Consultez les autres articles sur la collaboration B2B d'Azure AD :</span><span class="sxs-lookup"><span data-stu-id="dad70-115">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="dad70-116">Qu’est-ce qu’Azure AD B2B Collaboration ?</span><span class="sxs-lookup"><span data-stu-id="dad70-116">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="dad70-117">Propriétés de l’utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="dad70-117">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="dad70-118">Ajout d’un rôle tooa B2B collaboration</span><span class="sxs-lookup"><span data-stu-id="dad70-118">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="dad70-119">Déléguer des invitations B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="dad70-119">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="dad70-120">Groupes dynamiques et B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="dad70-120">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="dad70-121">Code B2B Collaboration et exemples PowerShell</span><span class="sxs-lookup"><span data-stu-id="dad70-121">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="dad70-122">Configurer des applications SaaS pour B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="dad70-122">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="dad70-123">Partage externe d’Office 365</span><span class="sxs-lookup"><span data-stu-id="dad70-123">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
* [<span data-ttu-id="dad70-124">Jetons utilisateur B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="dad70-124">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="dad70-125">Limitations actuelles de B2B Collaboration</span><span class="sxs-lookup"><span data-stu-id="dad70-125">B2B collaboration current limitations</span></span>](active-directory-b2b-current-limitations.md)
