---
title: "Synchronisation Azure AD Connect : comment toomanage hello Azure AD compte de service | Documents Microsoft"
description: Cette rubrique explique comment toorestore hello Azure AD compte de service.
services: active-directory
keywords: "AADSTS70002, AADSTS50054, comment tooreset hello mot de passe pour hello synchronisation d’Azure AD Connect compte du service du connecteur"
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a><span data-ttu-id="7e696-104">Synchronisation Azure AD Connect : comment toomanage hello Azure AD compte de service</span><span class="sxs-lookup"><span data-stu-id="7e696-104">Azure AD Connect sync: How toomanage hello Azure AD service account</span></span>
<span data-ttu-id="7e696-105">compte de service Hello utilisé par le connecteur Azure AD de hello est supposée service toobe libre.</span><span class="sxs-lookup"><span data-stu-id="7e696-105">hello service account used by hello Azure AD Connector is supposed toobe service free.</span></span> <span data-ttu-id="7e696-106">Si vous devez tooreset ses informations d’identification, cette rubrique est pour vous.</span><span class="sxs-lookup"><span data-stu-id="7e696-106">If you need tooreset its credentials, then this topic is for you.</span></span> <span data-ttu-id="7e696-107">Par exemple, si un administrateur Global a par erreur réinitialisation hello un mot de passe sur le compte de service hello à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7e696-107">For example, if a Global Administrator has by mistake reset hello password on hello service account using PowerShell.</span></span>

## <a name="reset-hello-credentials"></a><span data-ttu-id="7e696-108">Réinitialiser les informations d’identification hello</span><span class="sxs-lookup"><span data-stu-id="7e696-108">Reset hello credentials</span></span>
<span data-ttu-id="7e696-109">Si le compte de service de hello défini sur hello connecteur Azure AD ne peut pas contacter Azure AD en raison de problèmes de tooauthentication, mot de passe hello peut être réinitialisé.</span><span class="sxs-lookup"><span data-stu-id="7e696-109">If hello service account defined on hello Azure AD Connector cannot contact Azure AD due tooauthentication problems, hello password can be reset.</span></span>

1. <span data-ttu-id="7e696-110">Connectez-vous au serveur de synchronisation Azure AD Connect toohello et démarrer PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7e696-110">Sign in toohello Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="7e696-111">Exécutez `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="7e696-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="7e696-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="7e696-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="7e696-113">Fournissez les informations d’identification de l’administrateur général Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e696-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="7e696-114">Cette applet de commande réinitialise le mot de passe hello pour le compte de service hello et mettre à jour dans Azure AD et dans le moteur de synchronisation hello.</span><span class="sxs-lookup"><span data-stu-id="7e696-114">This cmdlet resets hello password for hello service account and update it both in Azure AD and in hello sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="7e696-115">Problèmes connus pouvant être résolus par les procédures indiquées ci-après</span><span class="sxs-lookup"><span data-stu-id="7e696-115">Known issues these steps can solve</span></span>
<span data-ttu-id="7e696-116">Cette section est une liste d’erreurs signalées par les clients qui ont été résolus par un informations d’identification réinitialiser sur hello compte de service Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e696-116">This section is a list of errors reported by customers that were fixed by a credentials reset on hello Azure AD service account.</span></span>

- - -
<span data-ttu-id="7e696-117">Événement 6900</span><span class="sxs-lookup"><span data-stu-id="7e696-117">Event 6900</span></span>  
<span data-ttu-id="7e696-118">serveur de Hello a rencontré une erreur inattendue lors du traitement d’une notification de modification de mot de passe :</span><span class="sxs-lookup"><span data-stu-id="7e696-118">hello server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="7e696-119">AADSTS70002 : erreur de validation des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="7e696-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="7e696-120">AADSTS50054 : l’ancien mot de passe est utilisé pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="7e696-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="7e696-121">Événement 659</span><span class="sxs-lookup"><span data-stu-id="7e696-121">Event 659</span></span>  
<span data-ttu-id="7e696-122">Erreur lors de la récupération de la configuration de la synchronisation de stratégie de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7e696-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="7e696-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException :</span><span class="sxs-lookup"><span data-stu-id="7e696-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="7e696-124">AADSTS70002 : erreur de validation des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="7e696-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="7e696-125">AADSTS50054 : l’ancien mot de passe est utilisé pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="7e696-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e696-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7e696-126">Next steps</span></span>
<span data-ttu-id="7e696-127">**Rubriques de présentation**</span><span class="sxs-lookup"><span data-stu-id="7e696-127">**Overview topics**</span></span>

* [<span data-ttu-id="7e696-128">Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation</span><span class="sxs-lookup"><span data-stu-id="7e696-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="7e696-129">Intégration de vos identités locales avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e696-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

