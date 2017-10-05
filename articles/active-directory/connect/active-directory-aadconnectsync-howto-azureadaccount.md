---
title: "Azure AD Connect Sync : comment gérer le compte de service Azure AD | Microsoft Docs"
description: Cette rubrique explique comment restaurer le compte de service Azure AD.
services: active-directory
keywords: "AADSTS70002, AADSTS50054, Comment réinitialiser le mot de passe du compte du service Connecteur de synchronisation Azure AD Connect"
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
ms.openlocfilehash: 8e9e8192ee4fcb636b5be91d2616acbc9120c8c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-how-to-manage-the-azure-ad-service-account"></a><span data-ttu-id="0df48-104">Azure AD Connect Sync : comment gérer le compte de service Azure AD</span><span class="sxs-lookup"><span data-stu-id="0df48-104">Azure AD Connect sync: How to manage the Azure AD service account</span></span>
<span data-ttu-id="0df48-105">Le compte de service utilisé par le connecteur Azure AD est censé être proposé en libre-service.</span><span class="sxs-lookup"><span data-stu-id="0df48-105">The service account used by the Azure AD Connector is supposed to be service free.</span></span> <span data-ttu-id="0df48-106">Si vous devez réinitialiser les informations d’identification, cette rubrique vous concerne.</span><span class="sxs-lookup"><span data-stu-id="0df48-106">If you need to reset its credentials, then this topic is for you.</span></span> <span data-ttu-id="0df48-107">Par exemple, un administrateur général peut avoir réinitialisé par erreur le mot de passe du compte de service à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0df48-107">For example, if a Global Administrator has by mistake reset the password on the service account using PowerShell.</span></span>

## <a name="reset-the-credentials"></a><span data-ttu-id="0df48-108">Réinitialisation des informations d'identification</span><span class="sxs-lookup"><span data-stu-id="0df48-108">Reset the credentials</span></span>
<span data-ttu-id="0df48-109">Si le compte de service défini sur le Connecteur Azure AD ne peut pas contacter Azure AD en raison de problèmes d’authentification, le mot de passe peut être réinitialisé.</span><span class="sxs-lookup"><span data-stu-id="0df48-109">If the service account defined on the Azure AD Connector cannot contact Azure AD due to authentication problems, the password can be reset.</span></span>

1. <span data-ttu-id="0df48-110">Connectez-vous au serveur de synchronisation Azure AD Connect et démarrez PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0df48-110">Sign in to the Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="0df48-111">Exécutez `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="0df48-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="0df48-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="0df48-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="0df48-113">Fournissez les informations d’identification de l’administrateur général Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0df48-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="0df48-114">Cette applet de commande réinitialise le mot de passe du compte de service et l’actualise dans Azure AD et dans le moteur de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="0df48-114">This cmdlet resets the password for the service account and update it both in Azure AD and in the sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="0df48-115">Problèmes connus pouvant être résolus par les procédures indiquées ci-après</span><span class="sxs-lookup"><span data-stu-id="0df48-115">Known issues these steps can solve</span></span>
<span data-ttu-id="0df48-116">Cette section est une liste d’erreurs signalées par les clients qui ont été résolues par une réinitialisation des informations d’identification sur le compte de service Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0df48-116">This section is a list of errors reported by customers that were fixed by a credentials reset on the Azure AD service account.</span></span>

- - -
<span data-ttu-id="0df48-117">Événement 6900</span><span class="sxs-lookup"><span data-stu-id="0df48-117">Event 6900</span></span>  
<span data-ttu-id="0df48-118">Le serveur a rencontré une erreur inattendue lors du traitement d’une notification de modification de mot de passe :</span><span class="sxs-lookup"><span data-stu-id="0df48-118">The server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="0df48-119">AADSTS70002 : erreur de validation des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="0df48-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="0df48-120">AADSTS50054 : l’ancien mot de passe est utilisé pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="0df48-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="0df48-121">Événement 659</span><span class="sxs-lookup"><span data-stu-id="0df48-121">Event 659</span></span>  
<span data-ttu-id="0df48-122">Erreur lors de la récupération de la configuration de la synchronisation de stratégie de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="0df48-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="0df48-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException :</span><span class="sxs-lookup"><span data-stu-id="0df48-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="0df48-124">AADSTS70002 : erreur de validation des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="0df48-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="0df48-125">AADSTS50054 : l’ancien mot de passe est utilisé pour l’authentification.</span><span class="sxs-lookup"><span data-stu-id="0df48-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0df48-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0df48-126">Next steps</span></span>
<span data-ttu-id="0df48-127">**Rubriques de présentation**</span><span class="sxs-lookup"><span data-stu-id="0df48-127">**Overview topics**</span></span>

* [<span data-ttu-id="0df48-128">Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation</span><span class="sxs-lookup"><span data-stu-id="0df48-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="0df48-129">Intégration de vos identités locales avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0df48-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

