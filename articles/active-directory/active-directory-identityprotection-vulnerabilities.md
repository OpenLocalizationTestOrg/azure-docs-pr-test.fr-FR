---
title: "Vulnérabilités détectées par Azure Active Directory Identity Protection | Microsoft Docs"
description: "Présentation des vulnérabilités détectées par Azure Active Directory Identity Protection."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestion d’applications, sécurité, risque, niveau de risque, vulnérabilité, stratégie de sécurité"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 364873ff54099a6123e40b12e819d1745751f285
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="519ad-104">Vulnérabilités détectées par Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="519ad-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="519ad-105">Les vulnérabilités sont des points faibles exploitables par un cybercriminel au sein de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="519ad-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="519ad-106">Nous vous recommandons de les résoudre afin d’améliorer la posture de sécurité de votre organisation et d’empêcher des personnes malveillantes d’en tirer parti.</span><span class="sxs-lookup"><span data-stu-id="519ad-106">We recommend that you address these vulnerabilities to improve the security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="519ad-107">![vulnérabilités](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnérabilités")</span><span class="sxs-lookup"><span data-stu-id="519ad-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="519ad-108">Les sections suivantes fournissent une vue d’ensemble des vulnérabilités signalées par Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="519ad-108">The following sections provide you with an overview of the vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="519ad-109">Inscription à l’authentification multifacteur non configurée</span><span class="sxs-lookup"><span data-stu-id="519ad-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="519ad-110">Cette vulnérabilité vous permet de contrôler le déploiement d’Azure Multi-Factor Authentication, service d’authentification multifacteur d’Azure, dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="519ad-110">This vulnerability helps you control the deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="519ad-111">L’authentification multifacteur d’Azure ajoute une deuxième couche de sécurité à l’authentification utilisateur.</span><span class="sxs-lookup"><span data-stu-id="519ad-111">Azure multi-factor authentication provides a second layer of security to user authentication.</span></span> <span data-ttu-id="519ad-112">Elle contribue à sécuriser l’accès aux données et aux applications tout en répondant à la demande des utilisateurs souhaitant un processus d’authentification simple.</span><span class="sxs-lookup"><span data-stu-id="519ad-112">It helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="519ad-113">Il fournit une authentification forte via diverses options de vérification simples : appel téléphonique, message texte, notification par application mobile ou code de vérification et jetons OATH tiers.</span><span class="sxs-lookup"><span data-stu-id="519ad-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="519ad-114">Nous vous recommandons d’exiger l’authentification multifacteur d’Azure pour les connexions des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="519ad-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins.</span></span> <span data-ttu-id="519ad-115">L’authentification multifacteur joue un rôle clé dans les stratégies d’accès conditionnel en fonction des risques disponibles via Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="519ad-115">Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="519ad-116">Pour plus d’informations, consultez [Qu’est-ce qu’Azure Multi-Factor Authentication ?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="519ad-116">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="519ad-117">Applications cloud non gérées</span><span class="sxs-lookup"><span data-stu-id="519ad-117">Unmanaged cloud apps</span></span>
<span data-ttu-id="519ad-118">Cette vulnérabilité vous permet d’identifier les applications cloud non gérées au sein de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="519ad-118">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="519ad-119">Dans les entreprises modernes, les services informatiques n’ont souvent pas connaissance de toutes les applications cloud utilisées par les membres de l’organisation pour effectuer leur travail.</span><span class="sxs-lookup"><span data-stu-id="519ad-119">In modern enterprises, IT departments are often unaware of all the cloud applications that users in their organization are using to do their work.</span></span> <span data-ttu-id="519ad-120">Il est facile de comprendre pourquoi les administrateurs s’inquiètent d’un accès non autorisé aux données d'entreprise, de possibles fuites de données et autres risques de sécurité.</span><span class="sxs-lookup"><span data-stu-id="519ad-120">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="519ad-121">Nous vous recommandons de déployer Cloud App Discovery dans votre organisation pour détecter les applications cloud non gérées et de gérer ces applications à l’aide d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="519ad-121">We recommend that your organization deploy Cloud App Discovery to discover unmanaged cloud applications, and to manage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="519ad-122">Pour plus d’informations, consultez l’article [Détection des applications cloud non gérées avec Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="519ad-122">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="519ad-123">Alertes de sécurité du service Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="519ad-123">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="519ad-124">Cette vulnérabilité vous aide à détecter et à résoudre les alertes relatives aux identités privilégiées dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="519ad-124">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="519ad-125">Pour permettre aux utilisateurs d’effectuer des opérations privilégiées, les organisations doivent leur accorder un accès privilégié temporaire ou permanent à des ressources Azure AD, Azure ou Office 365 ou à d’autres applications SaaS.</span><span class="sxs-lookup"><span data-stu-id="519ad-125">To enable users to carry out privileged operations, organizations need to grant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="519ad-126">Chacun de ces utilisateurs privilégiés augmente la surface d’attaque de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="519ad-126">Each of these privileged users increases the attack surface of your organization.</span></span> <span data-ttu-id="519ad-127">Cette vulnérabilité vous permet d’identifier les utilisateurs disposant d’un accès privilégié inutile et de prendre les mesures qui s’imposent pour réduire ou éliminer le risque associé.</span><span class="sxs-lookup"><span data-stu-id="519ad-127">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action to reduce or eliminate the risk they pose.</span></span> 

<span data-ttu-id="519ad-128">Nous vous recommandons d’utiliser le service Azure AD Privileged Identity Management dans votre organisation pour gérer, contrôler et surveiller les identités privilégiées et leur accès aux ressources dans Azure AD et dans d’autres services en ligne Microsoft tels qu’Office 365 ou Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="519ad-128">We recommend that your organization uses Azure AD Privileged Identity Management to manage, control, and monitor privileged identities and their access to resources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="519ad-129">Pour plus d’informations, consultez l’article [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="519ad-129">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="519ad-130">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="519ad-130">See also</span></span>
* [<span data-ttu-id="519ad-131">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="519ad-131">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

