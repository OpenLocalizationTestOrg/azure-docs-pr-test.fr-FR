---
title: "Modifier l’algorithme de hachage de signature pour l’approbation de partie de confiance Office 365 | Microsoft Docs"
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
ms.openlocfilehash: c581b1468630a9f28204592c936360b72f42f0d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="0ee72-104">Modifier l’algorithme de hachage de signature pour l’approbation de partie de confiance Office 365</span><span class="sxs-lookup"><span data-stu-id="0ee72-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="0ee72-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="0ee72-105">Overview</span></span>
<span data-ttu-id="0ee72-106">Azure Active Directory Federation Services (AD FS) signe ses jetons dans Microsoft Azure Active Directory pour vous assurer qu’ils sont infalsifiables.</span><span class="sxs-lookup"><span data-stu-id="0ee72-106">Active Directory Federation Services (AD FS) signs its tokens to Microsoft Azure Active Directory to ensure that they cannot be tampered with.</span></span> <span data-ttu-id="0ee72-107">Cette signature peut reposer sur SHA1 ou SHA256.</span><span class="sxs-lookup"><span data-stu-id="0ee72-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="0ee72-108">Azure Active Directory prend désormais en charge les jetons signés avec un algorithme SHA256 et recommande de configurer l’algorithme de signature de jetons SHA256 pour un niveau de sécurité optimal.</span><span class="sxs-lookup"><span data-stu-id="0ee72-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting the token-signing algorithm to SHA256 for the highest level of security.</span></span> <span data-ttu-id="0ee72-109">Cet article décrit comment configurer l’algorithme de signature de jetons sur le niveau de sécurité le plus élevé, SHA256.</span><span class="sxs-lookup"><span data-stu-id="0ee72-109">This article describes the steps needed to set the token-signing algorithm to the more secure SHA256 level.</span></span>

>[!NOTE]
><span data-ttu-id="0ee72-110">Microsoft recommande d’utiliser l’algorithme de signature de jetons SHA256, qui est plus sûr que SHA1. Cependant, SHA1 est toujours une option prise en charge.</span><span class="sxs-lookup"><span data-stu-id="0ee72-110">Microsoft recommends usage of SHA256 as the algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.</span></span>

## <a name="change-the-token-signing-algorithm"></a><span data-ttu-id="0ee72-111">Modification de l’algorithme de signature de jetons</span><span class="sxs-lookup"><span data-stu-id="0ee72-111">Change the token-signing algorithm</span></span>
<span data-ttu-id="0ee72-112">Une fois que vous avez défini l’algorithme de signature selon l’un des deux processus ci-dessous, ADFS signe les jetons avec SHA256 pour approuver la partie de confiance Office 365.</span><span class="sxs-lookup"><span data-stu-id="0ee72-112">After you have set the signature algorithm with one of the two processes below, AD FS signs the tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="0ee72-113">Aucune autre modification de la configuration n’est requise, et ce changement n’a aucun impact sur votre capacité à accéder à Office 365 ou à d’autres applications Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0ee72-113">You don't need to make any extra configuration changes, and this change has no impact on your ability to access Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="0ee72-114">Console de gestion AD FS</span><span class="sxs-lookup"><span data-stu-id="0ee72-114">AD FS management console</span></span>
1. <span data-ttu-id="0ee72-115">Ouvrez la console de gestion AD FS sur le serveur AD FS principal.</span><span class="sxs-lookup"><span data-stu-id="0ee72-115">Open the AD FS management console on the primary AD FS server.</span></span>
2. <span data-ttu-id="0ee72-116">Développez le nœud AD FS et cliquez sur **Approbations de la partie de confiance**.</span><span class="sxs-lookup"><span data-stu-id="0ee72-116">Expand the AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="0ee72-117">Faites un clic droit sur votre approbation de partie de confiance Office 365/Azure et sélectionnez **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="0ee72-117">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="0ee72-118">Sélectionnez l’onglet **Avancé** puis l’algorithme de hachage sécurisé SHA256.</span><span class="sxs-lookup"><span data-stu-id="0ee72-118">Select the **Advanced** tab and select the secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="0ee72-119">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0ee72-119">Click **OK**.</span></span>

![Algorithme de signature SHA256 - MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="0ee72-121">Applets de commande PowerShell d’AD FS</span><span class="sxs-lookup"><span data-stu-id="0ee72-121">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="0ee72-122">Sur un serveur AD FS, ouvrez PowerShell avec des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="0ee72-122">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="0ee72-123">Définissez l’algorithme de hachage sécurisé avec l’applet de commande **Set-AdfsRelyingPartyTrust** .</span><span class="sxs-lookup"><span data-stu-id="0ee72-123">Set the secure hash algorithm by using the **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="0ee72-124">À lire également</span><span class="sxs-lookup"><span data-stu-id="0ee72-124">Also read</span></span>
* [<span data-ttu-id="0ee72-125">Réparation de l’approbation Office 365 avec Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="0ee72-125">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

