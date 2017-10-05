---
title: "Services et technologies de sécurité Azure | Microsoft Docs"
description: "Cet article fournit une liste des services et technologies de sécurité Azure."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: a5a7f60a-97e2-49b4-a8c5-7c010ff27ef8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/02/2016
ms.author: yurid
ms.openlocfilehash: 0bea62a43cf6cac9132fe64f2d6c54e52def4c55
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-security-services-and-technologies"></a><span data-ttu-id="ef48e-103">Services et technologies de sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-103">Azure Security Services and Technologies</span></span>
<span data-ttu-id="ef48e-104">Dans nos discussions avec les clients Azure actuels et futurs, une question revient souvent : « Avez-vous une liste de tous les services et technologies de sécurité proposés par Azure ? ».</span><span class="sxs-lookup"><span data-stu-id="ef48e-104">In our discussions with current and future Azure customers, we’re often asked “do you have a list of all the security related services and technologies that Azure has to offer?”</span></span>

<span data-ttu-id="ef48e-105">Nous sommes conscients que lorsque vous évaluez les options techniques des fournisseurs de service Cloud, il est utile de disposer d’une telle liste pour analyser les différentes options plus profondément lorsque vous êtes prêt.</span><span class="sxs-lookup"><span data-stu-id="ef48e-105">We understand that when you’re evaluating your cloud service provider technical options, it’s helpful to have such a list available that you can use to dig down deeper when the time is right for you.</span></span>

<span data-ttu-id="ef48e-106">Ce document fournit une première version de cette liste.</span><span class="sxs-lookup"><span data-stu-id="ef48e-106">The following is our initial effort at providing a list.</span></span> <span data-ttu-id="ef48e-107">Au fil du temps, cette liste sera modifiée et développée, tout comme Azure.</span><span class="sxs-lookup"><span data-stu-id="ef48e-107">Over time, this list will change and grow, just as Azure does.</span></span> <span data-ttu-id="ef48e-108">La liste est classée par catégories, et la liste des catégories évoluera également au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="ef48e-108">The list is categorized, and the list of categories will also grow over time.</span></span> <span data-ttu-id="ef48e-109">Veillez à consulter cette page régulièrement pour vous tenir au courant de l’évolution de nos technologies et services liés à la sécurité.</span><span class="sxs-lookup"><span data-stu-id="ef48e-109">Make sure to check this page on a regular basis to stay up-to-date on our security-related services and technologies.</span></span>

## <a name="azure-security---general"></a><span data-ttu-id="ef48e-110">Sécurité de Windows Azure – Généralités</span><span class="sxs-lookup"><span data-stu-id="ef48e-110">Azure Security - General</span></span>
* [<span data-ttu-id="ef48e-111">Centre de sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-111">Azure Security Center</span></span>](https://azure.microsoft.com/documentation/services/security-center/)
* [<span data-ttu-id="ef48e-112">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="ef48e-112">Azure Key Vault</span></span>](https://azure.microsoft.com/documentation/services/key-vault/)
* [<span data-ttu-id="ef48e-113">Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="ef48e-113">Azure Disk Encryption</span></span>](azure-security-disk-encryption.md)
* [<span data-ttu-id="ef48e-114">Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ef48e-114">Log Analytics</span></span>](../log-analytics/log-analytics-overview.md)
* [<span data-ttu-id="ef48e-115">Dev/Test Labs Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-115">Azure Dev/Test Labs</span></span>](https://azure.microsoft.com/documentation/services/devtest-lab/)

## <a name="azure-storage-security"></a><span data-ttu-id="ef48e-116">Sécurité Azure Storage</span><span class="sxs-lookup"><span data-stu-id="ef48e-116">Azure Storage Security</span></span>
* [<span data-ttu-id="ef48e-117">Storage Service Encryption Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-117">Azure Storage Service Encryption</span></span>](../storage/common/storage-service-encryption.md)
* [<span data-ttu-id="ef48e-118">Stockage hybride chiffré StorSimple</span><span class="sxs-lookup"><span data-stu-id="ef48e-118">StorSimple Encrypted Hybrid Storage</span></span>](https://azure.microsoft.com/documentation/services/storsimple/)
* [<span data-ttu-id="ef48e-119">Chiffrement côté client Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-119">Azure Client-Side Encryption</span></span>](../storage/common/storage-client-side-encryption.md)
* [<span data-ttu-id="ef48e-120">Signatures d’accès partagé Azure Storage</span><span class="sxs-lookup"><span data-stu-id="ef48e-120">Azure Storage Shared Access Signatures</span></span>](../storage/common/storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="ef48e-121">Clés de compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-121">Azure Storage Account Keys</span></span>](../storage/common/storage-create-storage-account.md)
* [<span data-ttu-id="ef48e-122">Partages de fichiers Azure avec chiffrement SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="ef48e-122">Azure File shares with SMB 3.0 Encryption</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="ef48e-123">Azure Storage Analytics</span><span class="sxs-lookup"><span data-stu-id="ef48e-123">Azure Storage Analytics</span></span>](https://msdn.microsoft.com/library/hh343270.aspx)

## <a name="azure-database-security"></a><span data-ttu-id="ef48e-124">Sécurité des bases de données Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-124">Azure Database Security</span></span>
* [<span data-ttu-id="ef48e-125">Pare-feu SQL Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-125">Azure SQL Firewall</span></span>](../sql-database/sql-database-firewall-configure.md)
* [<span data-ttu-id="ef48e-126">Chiffrement au niveau des cellules SQL Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-126">Azure SQL Cell Level Encryption</span></span>](https://blogs.msdn.microsoft.com/sqlsecurity/2015/05/12/recommendations-for-using-cell-level-encryption-in-azure-sql-database/)
* [<span data-ttu-id="ef48e-127">Chiffrement de la connexion SQL Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-127">Azure SQL Connection Encryption</span></span>](../sql-database/sql-database-control-access.md)
* [<span data-ttu-id="ef48e-128">Authentification SQL Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-128">Azure SQL Authentication</span></span>](../sql-database/sql-database-control-access.md)
* [<span data-ttu-id="ef48e-129">Chiffrement systématique SQL Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-129">Azure SQL Always Encryption</span></span>](https://msdn.microsoft.com/library/mt163865.aspx)
* [<span data-ttu-id="ef48e-130">Chiffrement au niveau des colonnes SQL Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-130">Azure SQL Column Level Encryption</span></span>](https://msdn.microsoft.com/library/ms179331.aspx)
* [<span data-ttu-id="ef48e-131">Chiffrement transparent des données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-131">Azure SQL Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/dn948096.aspx)
* [<span data-ttu-id="ef48e-132">Audit de base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-132">Azure SQL Database Auditing</span></span>](../sql-database/sql-database-auditing.md)

## <a name="azure-identity-and-access-management"></a><span data-ttu-id="ef48e-133">Gestion de l’identité et de l’accès Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-133">Azure Identity and Access Management</span></span>
* [<span data-ttu-id="ef48e-134">Contrôle d’accès en fonction du rôle Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-134">Azure Role Based Access Control</span></span>](../active-directory/role-based-access-control-configure.md)
* [<span data-ttu-id="ef48e-135">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ef48e-135">Azure Active Directory</span></span>](../active-directory/active-directory-whatis.md)
* [<span data-ttu-id="ef48e-136">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="ef48e-136">Azure Active Directory B2C</span></span>](../active-directory-b2c/active-directory-b2c-get-started.md)
* [<span data-ttu-id="ef48e-137">Services de domaine Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ef48e-137">Azure Active Directory Domain Services</span></span>](../active-directory-domain-services/active-directory-ds-overview.md)
* [<span data-ttu-id="ef48e-138">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="ef48e-138">Azure Multi-Factor Authentication</span></span>](../multi-factor-authentication/multi-factor-authentication.md)

## <a name="backup-and-disaster-recovery"></a><span data-ttu-id="ef48e-139">Sauvegarde et récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="ef48e-139">Backup and Disaster Recovery</span></span>
* [<span data-ttu-id="ef48e-140">Sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-140">Azure Backup</span></span>](https://azure.microsoft.com/documentation/services/backup/)
* [<span data-ttu-id="ef48e-141">Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="ef48e-141">Azure Site Recovery</span></span>](https://azure.microsoft.com/documentation/services/site-recovery/)

## <a name="azure-networking"></a><span data-ttu-id="ef48e-142">Mise en réseau Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-142">Azure Networking</span></span>
* [<span data-ttu-id="ef48e-143">Groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ef48e-143">Network Security Groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="ef48e-144">Passerelle VPN Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-144">Azure VPN Gateway</span></span>](../vpn-gateway/vpn-gateway-about-vpngateways.md)
* [<span data-ttu-id="ef48e-145">Application Gateway Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-145">Azure Application Gateway</span></span>](../application-gateway/application-gateway-introduction.md)
* [<span data-ttu-id="ef48e-146">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="ef48e-146">Azure Load Balancer</span></span>](../load-balancer/load-balancer-overview.md)
* [<span data-ttu-id="ef48e-147">Azure ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="ef48e-147">Azure ExpressRoute</span></span>](../expressroute/expressroute-introduction.md)
* [<span data-ttu-id="ef48e-148">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="ef48e-148">Azure Traffic Manager</span></span>](../traffic-manager/traffic-manager-overview.md)
* [<span data-ttu-id="ef48e-149">Proxy d’application Azure</span><span class="sxs-lookup"><span data-stu-id="ef48e-149">Azure Application Proxy</span></span>](../active-directory/active-directory-application-proxy-enable.md)
