---
title: "Présentation de la gestion et surveillance de la sécurité Azure | Microsoft Docs"
description: " Azure propose divers mécanismes de sécurité pour favoriser la gestion et surveillance des services cloud et des machines virtuelles Azure.  Cet article fournit une vue d’ensemble de ces fonctionnalités et services clés de sécurité. "
services: security
documentationcenter: na
author: TerryLanfear
manager: StevenPo
editor: TomSh
ms.assetid: 5cf2827b-6cd3-434d-9100-d7411f7ed424
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: terrylan
ms.openlocfilehash: 6787877deabafd0b7308e190cb45b4036049b05b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-security-management-and-monitoring-overview"></a><span data-ttu-id="6da05-104">Présentation de la gestion et surveillance de la sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="6da05-104">Azure Security Management and Monitoring Overview</span></span>
<span data-ttu-id="6da05-105">Azure propose divers mécanismes de sécurité pour favoriser la gestion et surveillance des services cloud et des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="6da05-105">Azure provides security mechanisms to aid in the management and monitoring of Azure cloud services and virtual machines.</span></span> <span data-ttu-id="6da05-106">Cet article fournit une vue d’ensemble de ces fonctionnalités et services clés de sécurité.</span><span class="sxs-lookup"><span data-stu-id="6da05-106">This article provides an overview of these core security features and services.</span></span> <span data-ttu-id="6da05-107">Les liens renvoient à des articles qui fournissent des informations détaillées complémentaires sur chaque fonctionnalité ou service.</span><span class="sxs-lookup"><span data-stu-id="6da05-107">Links are provided to articles that give details of each so you can learn more.</span></span>

<span data-ttu-id="6da05-108">La sécurité de vos services Microsoft Cloud est une collaboration et une responsabilité partagée entre vous et Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6da05-108">The security of your Microsoft cloud services is a partnership and shared responsibility between you and Microsoft.</span></span> <span data-ttu-id="6da05-109">Une responsabilité partagée signifie que Microsoft est responsable de Microsoft Azure et de l’intégrité physique de ses centres de données (grâce à l’utilisation de mesures de protection telles que des portes sécurisées au moyen de badges, des clôtures et des gardes).</span><span class="sxs-lookup"><span data-stu-id="6da05-109">Shared responsibility means Microsoft is responsible for the Microsoft Azure and physical security of its data centers (by using security protections such as locked badge entry doors, fences, and guards).</span></span> <span data-ttu-id="6da05-110">En outre, Azure fournit des niveaux élevés de sécurité du cloud sur la couche logicielle, répondant aux attentes exigeantes de ses clients en matière de sécurité, de confidentialité et de conformité.</span><span class="sxs-lookup"><span data-stu-id="6da05-110">In addition, Azure provides strong levels of cloud security at the software layer that meets the security, privacy, and compliance needs of its demanding customers.</span></span>

<span data-ttu-id="6da05-111">Vos données et identités vous appartiennent, ainsi que la responsabilité de les protéger, la sécurité de vos ressources locales et celle des composants cloud que vous contrôlez.</span><span class="sxs-lookup"><span data-stu-id="6da05-111">You own your data and identities, the responsibility for protecting them, the security of your on-premises resources, and the security of cloud components over which you have control.</span></span> <span data-ttu-id="6da05-112">Microsoft vous fournit des fonctionnalités et des contrôles de sécurité pour vous aider à protéger vos données et applications.</span><span class="sxs-lookup"><span data-stu-id="6da05-112">Microsoft provides you with security controls and capabilities to help you protect your data and applications.</span></span> <span data-ttu-id="6da05-113">Votre niveau de responsabilité en matière de sécurité dépend du type de service cloud.</span><span class="sxs-lookup"><span data-stu-id="6da05-113">Your degree of responsibility for security is based on the type of cloud service.</span></span>

<span data-ttu-id="6da05-114">Le graphique suivant résume le partage de la responsabilité entre Microsoft et le client.</span><span class="sxs-lookup"><span data-stu-id="6da05-114">The following chart summarizes the balance of responsibility for both Microsoft and the customer.</span></span>

![Responsabilité partagée][1]

<span data-ttu-id="6da05-116">Pour aller plus loin sur la gestion de la sécurité, consultez [Gestion de la sécurité dans Azure](azure-security-management.md).</span><span class="sxs-lookup"><span data-stu-id="6da05-116">For a deeper dive into security management, see [Security management in Azure](azure-security-management.md).</span></span>

<span data-ttu-id="6da05-117">Voici les principales fonctionnalités abordées dans cet article :</span><span class="sxs-lookup"><span data-stu-id="6da05-117">Here are the core features to be covered in this article:</span></span>

* <span data-ttu-id="6da05-118">Contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="6da05-118">Role-Based Access Control</span></span>
* <span data-ttu-id="6da05-119">Logiciel anti-programme malveillant</span><span class="sxs-lookup"><span data-stu-id="6da05-119">Antimalware</span></span>
* <span data-ttu-id="6da05-120">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="6da05-120">Multi-Factor Authentication</span></span>
* <span data-ttu-id="6da05-121">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6da05-121">ExpressRoute</span></span>
* <span data-ttu-id="6da05-122">Passerelles de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="6da05-122">Virtual network gateways</span></span>
* <span data-ttu-id="6da05-123">Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="6da05-123">Privileged identity management</span></span>
* <span data-ttu-id="6da05-124">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="6da05-124">Identity protection</span></span>
* <span data-ttu-id="6da05-125">Centre de sécurité</span><span class="sxs-lookup"><span data-stu-id="6da05-125">Security Center</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="6da05-126">Contrôle d’accès en fonction du rôle</span><span class="sxs-lookup"><span data-stu-id="6da05-126">Role-Based Access Control</span></span>
<span data-ttu-id="6da05-127">Le contrôle d’accès en fonction du rôle (RBAC) Azure offre une gestion précise de l’accès pour les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="6da05-127">Role-Based Access Control (RBAC) provides fine-grained access management for Azure resources.</span></span> <span data-ttu-id="6da05-128">L’utilisation du RBAC vous permet de n’accorder aux utilisateurs que les droits d’accès dont ils ont besoin pour effectuer leur travail.</span><span class="sxs-lookup"><span data-stu-id="6da05-128">Using RBAC, you can grant people only the amount of access that they need to perform their jobs.</span></span>  <span data-ttu-id="6da05-129">Le RBAC peut également vous permettre de vous assurer que les utilisateurs perdent l’accès aux ressources dans le cloud lorsqu’ils quittent l’entreprise.</span><span class="sxs-lookup"><span data-stu-id="6da05-129">RBAC can also help you ensure that when people leave the organization they lose access to resources in the cloud.</span></span>

<span data-ttu-id="6da05-130">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="6da05-130">Learn more:</span></span>

* [<span data-ttu-id="6da05-131">Blog de l’équipe Active Directory sur le RBAC</span><span class="sxs-lookup"><span data-stu-id="6da05-131">Active Directory team blog on RBAC</span></span>](http://i1.blogs.technet.com/b/ad/archive/2015/10/12/azure-rbac-is-ga.aspx)
* [<span data-ttu-id="6da05-132">Contrôle d’accès en fonction du rôle Azure</span><span class="sxs-lookup"><span data-stu-id="6da05-132">Azure Role-Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="antimalware"></a><span data-ttu-id="6da05-133">Logiciel anti-programme malveillant</span><span class="sxs-lookup"><span data-stu-id="6da05-133">Antimalware</span></span>
<span data-ttu-id="6da05-134">Azure met à votre disposition des logiciels anti-programmes malveillants provenant de fournisseurs de sécurité reconnus tels que Microsoft, Symantec, Trend Micro, McAfee et Kaspersky. Ceux-ci permettent de protéger vos machines virtuelles contre les fichiers malveillants, les logiciels de publicité et d’autres menaces.</span><span class="sxs-lookup"><span data-stu-id="6da05-134">With Azure, you can use antimalware software from major security vendors such as Microsoft, Symantec, Trend Micro, McAfee, and Kaspersky to help protect your virtual machines from malicious files, adware, and other threats.</span></span>

<span data-ttu-id="6da05-135">Microsoft Antimalware vous offre la possibilité d’installer un agent anti-programmes malveillants pour les rôles PaaS et les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="6da05-135">Microsoft Antimalware offers you the ability to install an antimalware agent for both PaaS roles and virtual machines.</span></span> <span data-ttu-id="6da05-136">Basée sur System Center Endpoint Protection, cette fonctionnalité offre une technologie de sécurité locale éprouvée sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="6da05-136">Based on System Center Endpoint Protection, this feature brings proven on-premises security technology to the cloud.</span></span>

<span data-ttu-id="6da05-137">Nous offrons également une intégration approfondie de produits Trend ([Deep Security](http://www.trendmicro.com/us/enterprise/cloud-solutions/deep-security/)™ et [SecureCloud](http://www.trendmicro.com/us/enterprise/cloud-solutions/secure-cloud/)™) dans la plateforme Azure.</span><span class="sxs-lookup"><span data-stu-id="6da05-137">We also offer deep integration for Trend’s [Deep Security](http://www.trendmicro.com/us/enterprise/cloud-solutions/deep-security/)™ and [SecureCloud](http://www.trendmicro.com/us/enterprise/cloud-solutions/secure-cloud/)™ products in the Azure platform.</span></span> <span data-ttu-id="6da05-138">DeepSecurity est une solution Antivirus et SecureCloud une solution de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="6da05-138">DeepSecurity is an Antivirus solution and SecureCloud is an encryption solution.</span></span> <span data-ttu-id="6da05-139">DeepSecurity est déployé sur des machines virtuelles à l’aide d’un modèle d’extension.</span><span class="sxs-lookup"><span data-stu-id="6da05-139">DeepSecurity is deployed inside VMs using an extension model.</span></span> <span data-ttu-id="6da05-140">À l’aide de l’interface utilisateur du portail et de PowerShell, vous pouvez choisir d’utiliser DeepSecurity à l’intérieur de nouvelles machines virtuelles en cours de lancement, ou de machines virtuelles existantes déjà déployées.</span><span class="sxs-lookup"><span data-stu-id="6da05-140">Using the portal UI and PowerShell, you can choose to use DeepSecurity inside new VMs that are being spun up, or existing VMs that are already deployed.</span></span>

<span data-ttu-id="6da05-141">Symantec Endpoint Protection (SEP) est également pris en charge sur Azure.</span><span class="sxs-lookup"><span data-stu-id="6da05-141">Symantec End Point Protection (SEP) is also supported on Azure.</span></span> <span data-ttu-id="6da05-142">Grâce à l’intégration dans le portail, les clients ont la possibilité d’indiquer qu’ils souhaitent utiliser SEP au sein d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6da05-142">Through portal integration, customers can specify that they intend to use SEP within a VM.</span></span> <span data-ttu-id="6da05-143">SEP peut être installé sur une toute nouvelle machine virtuelle par le biais du portail Azure, ou sur une machine virtuelle existante à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6da05-143">SEP can be installed on a brand new VM via the Azure portal or can be installed on an existing VM using PowerShell.</span></span>

<span data-ttu-id="6da05-144">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="6da05-144">Learn more:</span></span>

* [<span data-ttu-id="6da05-145">Déploiement de solutions anti-programmes malveillants sur des machines virtuelles Azure (en anglais)</span><span class="sxs-lookup"><span data-stu-id="6da05-145">Deploying Antimalware Solutions on Azure Virtual Machines</span></span>](https://azure.microsoft.com/blog/deploying-antimalware-solutions-on-azure-virtual-machines/)
* [<span data-ttu-id="6da05-146">Microsoft Antimalware pour Azure Cloud Services et les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="6da05-146">Microsoft Antimalware for Azure Cloud Services and Virtual Machines</span></span>](azure-security-antimalware.md)
* [<span data-ttu-id="6da05-147">Installation et configuration de Trend Micro Deep Security comme service sur une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="6da05-147">How to install and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>](../virtual-machines/windows/classic/install-trend.md)
* [<span data-ttu-id="6da05-148">Installation et configuration de Symantec Endpoint Protection sur une machine virtuelle Windows</span><span class="sxs-lookup"><span data-stu-id="6da05-148">How to install and configure Symantec Endpoint Protection on a Windows VM</span></span>](../virtual-machines/windows/classic/install-symantec.md)
* [<span data-ttu-id="6da05-149">Nouvelles options anti-programmes malveillants pour protéger les machines virtuelles – McAfee Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="6da05-149">New Antimalware Options for Protecting Azure Virtual Machines – McAfee Endpoint Protection</span></span>](https://azure.microsoft.com/blog/new-antimalware-options-for-protecting-azure-virtual-machines/)

## <a name="multi-factor-authentication"></a><span data-ttu-id="6da05-150">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="6da05-150">Multi-Factor Authentication</span></span>
<span data-ttu-id="6da05-151">Azure Multi-Factor Authentication (MFA) est une méthode d’authentification qui nécessite l’utilisation de plusieurs méthodes de vérification et ajoute une deuxième couche critique de sécurité aux connexions et transactions des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6da05-151">Azure Multi-factor authentication (MFA) is a method of authentication that requires the use of more than one verification method and adds a critical second layer of security to user sign-ins and transactions.</span></span> <span data-ttu-id="6da05-152">MFA contribue à sécuriser l’accès aux données et aux applications tout en répondant à la demande des utilisateurs souhaitant un processus d’authentification simple.</span><span class="sxs-lookup"><span data-stu-id="6da05-152">MFA helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="6da05-153">Elle fournit une authentification forte par le biais de diverses options de vérification : appel téléphonique, SMS, notification par application mobile ou code de vérification et jetons OATH tiers.</span><span class="sxs-lookup"><span data-stu-id="6da05-153">It delivers strong authentication via a range of verification options—phone call, text message, or mobile app notification or verification code and third party OATH tokens.</span></span>

<span data-ttu-id="6da05-154">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="6da05-154">Learn more:</span></span>

* [<span data-ttu-id="6da05-155">Authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="6da05-155">Multi-factor authentication</span></span>](https://azure.microsoft.com/documentation/services/multi-factor-authentication/)
* [<span data-ttu-id="6da05-156">Présentation d'Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="6da05-156">What is Azure Multi-Factor Authentication?</span></span>](../multi-factor-authentication/multi-factor-authentication.md)
* [<span data-ttu-id="6da05-157">Azure Multi-Factor Authentication : fonctionnement</span><span class="sxs-lookup"><span data-stu-id="6da05-157">How Azure Multi-Factor Authentication works</span></span>](../multi-factor-authentication/multi-factor-authentication-how-it-works.md)

## <a name="expressroute"></a><span data-ttu-id="6da05-158">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6da05-158">ExpressRoute</span></span>
<span data-ttu-id="6da05-159">Microsoft Azure ExpressRoute vous permet d'étendre vos réseaux locaux au cloud de Microsoft via une connexion privée dédiée assurée par un fournisseur de connectivité.</span><span class="sxs-lookup"><span data-stu-id="6da05-159">Microsoft Azure ExpressRoute lets you extend your on-premises networks into the Microsoft cloud over a dedicated private connection facilitated by a connectivity provider.</span></span> <span data-ttu-id="6da05-160">Grâce à ExpressRoute, vous pouvez établir des connexions aux services de cloud computing Microsoft, comme Microsoft Azure, Office 365 et CRM Online.</span><span class="sxs-lookup"><span data-stu-id="6da05-160">With ExpressRoute, you can establish connections to Microsoft cloud services, such as Microsoft Azure, Office 365, and CRM Online.</span></span> <span data-ttu-id="6da05-161">La connectivité peut provenir d'un réseau universel (IP VPN), d’un réseau Ethernet point à point ou d’une interconnexion virtuelle via un fournisseur de connectivité dans un centre de colocalisation.</span><span class="sxs-lookup"><span data-stu-id="6da05-161">Connectivity can be from an any-to-any (IP VPN) network, a point-to-point Ethernet network, or a virtual cross-connection through a connectivity provider at a co-location facility.</span></span> <span data-ttu-id="6da05-162">Les connexions ExpressRoute ne sont pas établies par le biais de l'Internet public.</span><span class="sxs-lookup"><span data-stu-id="6da05-162">ExpressRoute connections do not go over the public Internet.</span></span> <span data-ttu-id="6da05-163">Elles offrent ainsi de meilleurs niveaux de fiabilité, de rapidité, de latence et de sécurité que les connexions classiques sur Internet.</span><span class="sxs-lookup"><span data-stu-id="6da05-163">This allows ExpressRoute connections to offer more reliability, faster speeds, lower latencies, and higher security than typical connections over the Internet.</span></span>

<span data-ttu-id="6da05-164">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="6da05-164">Learn more:</span></span>

* [<span data-ttu-id="6da05-165">Présentation technique d’ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="6da05-165">ExpressRoute technical overview</span></span>](../expressroute/expressroute-introduction.md)

## <a name="virtual-network-gateways"></a><span data-ttu-id="6da05-166">Passerelles de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="6da05-166">Virtual network gateways</span></span>
<span data-ttu-id="6da05-167">Les passerelles VPN, aussi appelées passerelles de réseau virtuel Azure, sont conçues pour faire circuler le trafic réseau entre les réseaux virtuels et les emplacements sur site.</span><span class="sxs-lookup"><span data-stu-id="6da05-167">VPN Gateways, also called Azure Virtual Network Gateways, are used to send network traffic between virtual networks and on-premises locations.</span></span> <span data-ttu-id="6da05-168">Elles sont également utilisées pour acheminer le trafic entre plusieurs réseaux virtuels dans Azure (connexion de réseau virtuel à réseau virtuel).</span><span class="sxs-lookup"><span data-stu-id="6da05-168">They are also used to send traffic between multiple virtual networks within Azure (VNet-to-VNet).</span></span>  <span data-ttu-id="6da05-169">Les passerelles VPN garantissent la sécurisation de la connectivité entre les locaux entre Azure et votre infrastructure.</span><span class="sxs-lookup"><span data-stu-id="6da05-169">VPN gateways provide secure cross-premises connectivity between Azure and your infrastructure.</span></span>

<span data-ttu-id="6da05-170">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="6da05-170">Learn more:</span></span>

* [<span data-ttu-id="6da05-171">À propos des passerelles VPN</span><span class="sxs-lookup"><span data-stu-id="6da05-171">About VPN gateways</span></span>](../vpn-gateway/vpn-gateway-about-vpngateways.md)
* [<span data-ttu-id="6da05-172">Vue d’ensemble de la sécurité du réseau Azure</span><span class="sxs-lookup"><span data-stu-id="6da05-172">Azure Network Security Overview</span></span>](security-network-overview.md)

## <a name="privileged-identity-management"></a><span data-ttu-id="6da05-173">Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="6da05-173">Privileged Identity Management</span></span>
<span data-ttu-id="6da05-174">Les utilisateurs doivent parfois effectuer des opérations privilégiées dans des ressources Azure ou dans d’autres applications SaaS.</span><span class="sxs-lookup"><span data-stu-id="6da05-174">Sometimes users need to carry out privileged operations in Azure resources or other SaaS applications.</span></span> <span data-ttu-id="6da05-175">Cela signifie souvent que les entreprises doivent leur donner un accès privilégié permanent à Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="6da05-175">This often means organizations have to give them permanent privileged access in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="6da05-176">C’est un risque de sécurité croissant pour les ressources hébergées dans le cloud, car les entreprises ne peuvent pas suffisamment surveiller ce que ces utilisateurs font avec leur accès privilégié.</span><span class="sxs-lookup"><span data-stu-id="6da05-176">This is a growing security risk for cloud-hosted resources because organizations can't sufficiently monitor what those users are doing with their privileged access.</span></span>
<span data-ttu-id="6da05-177">En outre, si un compte d’utilisateur disposant d’un accès privilégié est compromis, cette seule faille peut affecter votre sécurité globale sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="6da05-177">Additionally, if a user account with privileged access is compromised, that one breach could impact your overall cloud security.</span></span> <span data-ttu-id="6da05-178">Azure AD Privileged Identity Management permet de résoudre ce risque en réduisant le temps d’exposition des privilèges et en augmentant la visibilité quant à leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="6da05-178">Azure AD Privileged Identity Management helps to resolve this risk by lowering the exposure time of privileges and increasing visibility into usage.</span></span>  

<span data-ttu-id="6da05-179">Privileged Identity Management introduit le concept d’un administrateur temporaire pour un rôle ou d’un accès administrateur immédiat, qui est un utilisateur devant terminer un processus d’activation pour ce rôle.</span><span class="sxs-lookup"><span data-stu-id="6da05-179">Privileged Identity Management introduces the concept of a temporary admin for a role or “just in time” administrator access, which is a user who needs to complete an activation process for that assigned role.</span></span> <span data-ttu-id="6da05-180">Le processus d'activation permet d’activer ou désactiver l'affectation de l'utilisateur à un rôle dans Azure AD pendant une période spécifiée, par exemple huit heures.</span><span class="sxs-lookup"><span data-stu-id="6da05-180">The activation process changes the assignment of the user to a role in Azure AD from inactive to active, for a specified time period such as eight hours.</span></span>

<span data-ttu-id="6da05-181">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="6da05-181">Learn more:</span></span>

* [<span data-ttu-id="6da05-182">Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="6da05-182">Azure AD Privileged Identity Management</span></span>](../active-directory/active-directory-privileged-identity-management-configure.md)
* [<span data-ttu-id="6da05-183">Prise en main d’Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="6da05-183">Get started with Azure AD Privileged Identity Management</span></span>](../active-directory/active-directory-privileged-identity-management-getting-started.md)

## <a name="identity-protection"></a><span data-ttu-id="6da05-184">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="6da05-184">Identity Protection</span></span>
<span data-ttu-id="6da05-185">Azure Active Directory (AD) Identity Protection fournit une vue consolidée des activités de connexion suspectes et des vulnérabilités potentielles pour vous aider à protéger votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="6da05-185">Azure Active Directory (AD) Identity Protection provides a consolidated view of suspicious sign-in activities and potential vulnerabilities to help protect your business.</span></span> <span data-ttu-id="6da05-186">Identity Protection détecte les activités de connexion suspectes pour les utilisateurs et les identités privilégiées (administrateurs) en fonction de signaux tels que les attaques par force brute, les fuites d’informations d’identification et les connexions provenant d’emplacements inconnus et d’appareils infectés.</span><span class="sxs-lookup"><span data-stu-id="6da05-186">Identity Protection detects suspicious activities for users and privileged (admin) identities, based on signals like brute-force attacks, leaked credentials, and sign-ins from unfamiliar locations and infected devices.</span></span>

<span data-ttu-id="6da05-187">En fournissant des notifications et des mises à jour recommandées, Identity Protection vous permet de limiter les risques en temps réel.</span><span class="sxs-lookup"><span data-stu-id="6da05-187">By providing notifications and recommended remediation, Identity Protection helps to mitigate risks in real time.</span></span> <span data-ttu-id="6da05-188">Il calcule la gravité des risques utilisateur, et vous pouvez configurer des stratégies basées sur les risques pour automatiquement contribuer à protéger l’accès à l’application contre les menaces futures.</span><span class="sxs-lookup"><span data-stu-id="6da05-188">It calculates user risk severity, and you can configure risk-based policies to automatically help safeguard application access from future threats.</span></span>

<span data-ttu-id="6da05-189">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="6da05-189">Learn more:</span></span>

* [<span data-ttu-id="6da05-190">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="6da05-190">Azure Active Directory Identity Protection</span></span>](../active-directory/active-directory-identityprotection.md)
* [<span data-ttu-id="6da05-191">Channel 9 : Azure AD and Identity Show: Identity Protection Preview (Émission sur Azure AD et l’identité : présentation d’Identity Protection)</span><span class="sxs-lookup"><span data-stu-id="6da05-191">Channel 9: Azure AD and Identity Show: Identity Protection Preview</span></span>](https://channel9.msdn.com/Series/Azure-AD-Identity/Azure-AD-and-Identity-Show-Identity-Protection-Preview)

## <a name="security-center"></a><span data-ttu-id="6da05-192">Centre de sécurité</span><span class="sxs-lookup"><span data-stu-id="6da05-192">Security Center</span></span>
<span data-ttu-id="6da05-193">Azure Security Center vous aide à prévenir, détecter et résoudre les menaces, en vous apportant une visibilité et un contrôle accrus de la sécurité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="6da05-193">Azure Security Center helps you prevent, detect, and respond to threats, and provides you increased visibility into, and control over, the security of your Azure resources.</span></span> <span data-ttu-id="6da05-194">Il fournit une surveillance de la sécurité et une gestion des stratégies intégrées pour l’ensemble de vos abonnements Azure, vous aidant ainsi à détecter les menaces qui pourraient passer inaperçues. De plus, il est compatible avec un vaste écosystème de solutions de sécurité.</span><span class="sxs-lookup"><span data-stu-id="6da05-194">It provides integrated security monitoring and policy management across your Azure subscriptions, helps detect threats that might otherwise go unnoticed, and works with a broad ecosystem of security solutions.</span></span>

<span data-ttu-id="6da05-195">Security Center vous permet d’optimiser et de surveiller la sécurité de vos ressources Azure grâce aux opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="6da05-195">Security Center helps you optimize and monitor the security of your Azure resources by:</span></span>

* <span data-ttu-id="6da05-196">Il vous permet de définir des stratégies pour vos abonnements aux ressources Azure en fonction des exigences de sécurité de votre société et du type d’applications ou du niveau de confidentialité des données de chaque abonnement.</span><span class="sxs-lookup"><span data-stu-id="6da05-196">Enabling you to define policies for your Azure subscription resources according to your company’s security needs and the type of applications or sensitivity of the data in each subscription.</span></span>
* <span data-ttu-id="6da05-197">Il analyse l’état de vos machines virtuelles, de votre réseau et de vos applications Azure.</span><span class="sxs-lookup"><span data-stu-id="6da05-197">Monitoring the state of your Azure virtual machines, networking, and applications.</span></span>
* <span data-ttu-id="6da05-198">Il fournit une liste hiérarchisée d’alertes de sécurité, notamment les alertes provenant de solutions de partenaires intégrées, ainsi que les informations nécessaires pour trouver rapidement la cause d’une attaque et des recommandations sur la façon d’y remédier.</span><span class="sxs-lookup"><span data-stu-id="6da05-198">Providing a list of prioritized security alerts, including alerts from integrated partner solutions, along with the information you need to quickly investigate and recommendations on how to remediate an attack.</span></span>

<span data-ttu-id="6da05-199">En savoir plus :</span><span class="sxs-lookup"><span data-stu-id="6da05-199">Learn more:</span></span>

* [<span data-ttu-id="6da05-200">Présentation d’Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="6da05-200">Introduction to Azure Security Center</span></span>](../security-center/security-center-intro.md)

<!--Image references-->
[1]: ./media/security-management-and-monitoring-overview/shared-responsibility.png