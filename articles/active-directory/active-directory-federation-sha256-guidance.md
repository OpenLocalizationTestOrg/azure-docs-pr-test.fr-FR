---
title: algorithme de hachage de signature aaaChange pour Office 365 confiance | Documents Microsoft
description: "Cette page fournit des instructions permettant de modifier l’algorithme SHA pour l’approbation de fédération avec Office 365"
keywords: "SHA1, SHA256, O365, fédération, aadconnect, adfs, ad fs, modifier sha, approbation de fédération, approbation de partie de confiance"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: samueld
editor: 
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: anandy
ms.openlocfilehash: 3333d1384aff8bdf6b3bcc894f8c633fd9ccc3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="3453d-104">Modifier l’algorithme de hachage de signature pour l’approbation de partie de confiance Office 365</span><span class="sxs-lookup"><span data-stu-id="3453d-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="3453d-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="3453d-105">Overview</span></span>
<span data-ttu-id="3453d-106">Services de fédération Active Directory (AD FS) se connecte à son tooensure d’Azure Active Directory tooMicrosoft jetons qui ne peut pas être falsifiées.</span><span class="sxs-lookup"><span data-stu-id="3453d-106">Active Directory Federation Services (AD FS) signs its tokens tooMicrosoft Azure Active Directory tooensure that they cannot be tampered with.</span></span> <span data-ttu-id="3453d-107">Cette signature peut reposer sur SHA1 ou SHA256.</span><span class="sxs-lookup"><span data-stu-id="3453d-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="3453d-108">Azure Active Directory prend désormais en charge les jetons signés avec un algorithme SHA256, et nous vous recommandons de définir hello tooSHA256 d’algorithme signature de jetons pour hello plus haut niveau de sécurité.</span><span class="sxs-lookup"><span data-stu-id="3453d-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting hello token-signing algorithm tooSHA256 for hello highest level of security.</span></span> <span data-ttu-id="3453d-109">Cet article décrit les étapes hello nécessaire toohello des algorithme de signature de jetons hello tooset plus sécurisée au niveau du SHA256.</span><span class="sxs-lookup"><span data-stu-id="3453d-109">This article describes hello steps needed tooset hello token-signing algorithm toohello more secure SHA256 level.</span></span>

>[!NOTE]
><span data-ttu-id="3453d-110">Microsoft recommande l’utilisation de SHA256 comme algorithme de hello pour signer les jetons qu’il est plus sécurisé que SHA1 mais SHA1 reste toujours une option de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="3453d-110">Microsoft recommends usage of SHA256 as hello algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.</span></span>

## <a name="change-hello-token-signing-algorithm"></a><span data-ttu-id="3453d-111">Modifier l’algorithme de signature de jetons hello</span><span class="sxs-lookup"><span data-stu-id="3453d-111">Change hello token-signing algorithm</span></span>
<span data-ttu-id="3453d-112">Une fois que vous avez défini l’algorithme de signature hello avec l’un des deux processus hello ci-dessous, AD FS signe les jetons hello pour Office 365 confiance avec SHA256.</span><span class="sxs-lookup"><span data-stu-id="3453d-112">After you have set hello signature algorithm with one of hello two processes below, AD FS signs hello tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="3453d-113">Vous n’avez pas besoin toomake toutes les modifications de configuration supplémentaire, et cette modification n’a aucun impact sur votre capacité de tooaccess Office 365 ou d’autres applications Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3453d-113">You don't need toomake any extra configuration changes, and this change has no impact on your ability tooaccess Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="3453d-114">Console de gestion AD FS</span><span class="sxs-lookup"><span data-stu-id="3453d-114">AD FS management console</span></span>
1. <span data-ttu-id="3453d-115">Ouvrez la console de gestion hello AD FS sur le serveur de hello principal AD FS.</span><span class="sxs-lookup"><span data-stu-id="3453d-115">Open hello AD FS management console on hello primary AD FS server.</span></span>
2. <span data-ttu-id="3453d-116">Développez le nœud de hello AD FS et cliquez sur **confiance**.</span><span class="sxs-lookup"><span data-stu-id="3453d-116">Expand hello AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="3453d-117">Faites un clic droit sur votre approbation de partie de confiance Office 365/Azure et sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="3453d-117">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="3453d-118">Sélectionnez hello **avancé** onglet et l’algorithme de hachage sécurisé hello sélectionnez SHA256.</span><span class="sxs-lookup"><span data-stu-id="3453d-118">Select hello **Advanced** tab and select hello secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="3453d-119">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3453d-119">Click **OK**.</span></span>

![Algorithme de signature SHA256 - MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="3453d-121">Applets de commande PowerShell d’AD FS</span><span class="sxs-lookup"><span data-stu-id="3453d-121">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="3453d-122">Sur un serveur AD FS, ouvrez PowerShell avec des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="3453d-122">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="3453d-123">Algorithme de hachage sécurisé hello ensemble à l’aide de hello **Set-AdfsRelyingPartyTrust** applet de commande.</span><span class="sxs-lookup"><span data-stu-id="3453d-123">Set hello secure hash algorithm by using hello **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="3453d-124">À lire également</span><span class="sxs-lookup"><span data-stu-id="3453d-124">Also read</span></span>
* [<span data-ttu-id="3453d-125">Réparation de l’approbation Office 365 avec Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="3453d-125">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

