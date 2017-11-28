---
title: "aaaVulnerabilities détectés par la Protection d’identité Azure Active Directory | Documents Microsoft"
description: "Vue d’ensemble des vulnérabilités hello détectés par la Protection d’identité Azure Active Directory."
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
ms.openlocfilehash: 5e1cb401f8b566a180eb46e3420a090bcfc66767
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="68b2d-104">Vulnérabilités détectées par Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="68b2d-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="68b2d-105">Les vulnérabilités sont des points faibles exploitables par un cybercriminel au sein de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="68b2d-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="68b2d-106">Nous vous recommandons de résoudre ces posture de sécurité hello tooimprove des vulnérabilités de votre organisation et d’empêcher les intrus de les exploiter.</span><span class="sxs-lookup"><span data-stu-id="68b2d-106">We recommend that you address these vulnerabilities tooimprove hello security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="68b2d-107">![vulnérabilités](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnérabilités")</span><span class="sxs-lookup"><span data-stu-id="68b2d-107">![vulnerabilities](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="68b2d-108">Hello sections suivantes fournissent une vue d’ensemble des vulnérabilités hello signalés par la Protection de l’identité.</span><span class="sxs-lookup"><span data-stu-id="68b2d-108">hello following sections provide you with an overview of hello vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="68b2d-109">Inscription à l’authentification multifacteur non configurée</span><span class="sxs-lookup"><span data-stu-id="68b2d-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="68b2d-110">Cette vulnérabilité vous permet de contrôler le déploiement de hello d’Azure multi-Factor Authentication dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="68b2d-110">This vulnerability helps you control hello deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="68b2d-111">L’authentification multifacteur Azure fournit une deuxième couche toouser d’authentification de sécurité.</span><span class="sxs-lookup"><span data-stu-id="68b2d-111">Azure multi-factor authentication provides a second layer of security toouser authentication.</span></span> <span data-ttu-id="68b2d-112">Il vous aide à toodata d’accès de sauvegarde et des applications tout en répondant à la demande de l’utilisateur pour un processus de connexion simple.</span><span class="sxs-lookup"><span data-stu-id="68b2d-112">It helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="68b2d-113">Il fournit une authentification forte via diverses options de vérification simples : appel téléphonique, message texte, notification par application mobile ou code de vérification et jetons OATH tiers.</span><span class="sxs-lookup"><span data-stu-id="68b2d-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="68b2d-114">Nous vous recommandons d’exiger l’authentification multifacteur d’Azure pour les connexions des utilisateurs. L’authentification multifacteur joue un rôle clé dans les stratégies d’accès conditionnel en fonction des risques disponibles via Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="68b2d-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins. Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="68b2d-115">Pour plus d’informations, consultez [Qu’est-ce qu’Azure Multi-Factor Authentication ?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="68b2d-115">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="68b2d-116">Applications cloud non gérées</span><span class="sxs-lookup"><span data-stu-id="68b2d-116">Unmanaged cloud apps</span></span>
<span data-ttu-id="68b2d-117">Cette vulnérabilité vous permet d’identifier les applications cloud non gérées au sein de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="68b2d-117">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="68b2d-118">Dans les entreprises modernes, les services informatiques sont souvent pas conscients de toutes les applications de cloud hello que les utilisateurs dans leur organisation utilisent toodo leur travail.</span><span class="sxs-lookup"><span data-stu-id="68b2d-118">In modern enterprises, IT departments are often unaware of all hello cloud applications that users in their organization are using toodo their work.</span></span> <span data-ttu-id="68b2d-119">Il est facile toosee pourquoi administrateurs auront des problèmes sur les données toocorporate de tout accès non autorisé, les fuites de données possibles et les autres risques de sécurité.</span><span class="sxs-lookup"><span data-stu-id="68b2d-119">It is easy toosee why administrators would have concerns about unauthorized access toocorporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="68b2d-120">Nous recommandons que votre organisation déployer des applications de cloud Cloud App Discovery toodiscover non managée et toomanage ces applications à l’aide d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="68b2d-120">We recommend that your organization deploy Cloud App Discovery toodiscover unmanaged cloud applications, and toomanage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="68b2d-121">Pour plus d’informations, consultez l’article [Détection des applications cloud non gérées avec Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="68b2d-121">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="68b2d-122">Alertes de sécurité du service Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="68b2d-122">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="68b2d-123">Cette vulnérabilité vous aide à détecter et à résoudre les alertes relatives aux identités privilégiées dans votre organisation.</span><span class="sxs-lookup"><span data-stu-id="68b2d-123">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="68b2d-124">toocarry d’utilisateurs tooenable opérations nécessitant des privilèges, les organisations ont besoin les utilisateurs toogrant temporaires ou définitives des privilèges d’accès dans Azure AD, les ressources Azure ou Office 365 ou autres applications SaaS.</span><span class="sxs-lookup"><span data-stu-id="68b2d-124">tooenable users toocarry out privileged operations, organizations need toogrant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="68b2d-125">Chacune de ces surface d’attaque hello augmente les utilisateurs privilégiés de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="68b2d-125">Each of these privileged users increases hello attack surface of your organization.</span></span> <span data-ttu-id="68b2d-126">Cette vulnérabilité vous aide à identifier les utilisateurs avec un accès privilégié inutile et prendre les mesures appropriées tooreduce ou éliminer le risque de hello qu’ils représentent.</span><span class="sxs-lookup"><span data-stu-id="68b2d-126">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action tooreduce or eliminate hello risk they pose.</span></span> 

<span data-ttu-id="68b2d-127">Il est recommandé que votre organisation utilise Azure AD Privileged Identity Management toomanage, contrôle et identités d’analyse privilégié et leurs tooresources d’accès dans Azure AD ainsi que d’autres services en ligne Microsoft comme Office 365 ou Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="68b2d-127">We recommend that your organization uses Azure AD Privileged Identity Management toomanage, control, and monitor privileged identities and their access tooresources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="68b2d-128">Pour plus d’informations, consultez l’article [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="68b2d-128">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="68b2d-129">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="68b2d-129">See also</span></span>
* [<span data-ttu-id="68b2d-130">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="68b2d-130">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

