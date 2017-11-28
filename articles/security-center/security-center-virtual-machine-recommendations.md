---
title: Protection de vos machines virtuelles dans Azure Security Center | Microsoft Docs
description: "Ce document traite des recommandations d’Azure Security Center qui peuvent vous aider à protéger vos machines virtuelles et à rester en conformité avec les stratégies de sécurité."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 47fa1f76-683d-4230-b4ed-d123fef9a3e8
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: 2b7f22e5c27f5ba2123d8a1d913887191a536740
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="protecting-your-virtual-machines-in-azure-security-center"></a><span data-ttu-id="f5ca5-103">Protection de vos machines virtuelles dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f5ca5-103">Protecting your virtual machines in Azure Security Center</span></span>
<span data-ttu-id="f5ca5-104">Le Centre de sécurité Azure analyse l’état de sécurité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="f5ca5-105">Lorsque Security Center identifie des failles de sécurité potentielles, il crée des recommandations qui vous guident tout au long du processus de configuration des contrôles nécessaires.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="f5ca5-106">Ces recommandations s’appliquent aux types de ressources Azure : machines virtuelles, mise en réseau, applications et SQL.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="f5ca5-107">Cet article traite des recommandations qui s’appliquent aux machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-107">This article addresses recommendations that apply to VMs.</span></span>  <span data-ttu-id="f5ca5-108">Les recommandations relatives aux machines virtuelles se concentrent autour de la collecte de données, de l’application des mises à jour du système, de la configuration du logiciel anti-programme malveillant, du chiffrement de vos disques de machines virtuelles, et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-108">VM recommendations center around data collection, applying system updates, provisioning antimalware, encrypting your VM disks, and more.</span></span>  <span data-ttu-id="f5ca5-109">Utilisez le tableau ci-dessous pour mieux comprendre les recommandations disponibles pour les machines virtuelles et leurs effets.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-109">Use the table below as a reference to help you understand the available VM recommendations and what each one will do if you apply it.</span></span>

## <a name="available-vm-recommendations"></a><span data-ttu-id="f5ca5-110">Recommandations disponibles pour les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="f5ca5-110">Available VM recommendations</span></span>
| <span data-ttu-id="f5ca5-111">Recommandation</span><span class="sxs-lookup"><span data-stu-id="f5ca5-111">Recommendation</span></span> | <span data-ttu-id="f5ca5-112">Description</span><span class="sxs-lookup"><span data-stu-id="f5ca5-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="f5ca5-113">Activer la collecte des données pour des abonnements</span><span class="sxs-lookup"><span data-stu-id="f5ca5-113">Enable data collection for subscriptions</span></span>](security-center-enable-data-collection.md) |<span data-ttu-id="f5ca5-114">Recommande l’activation de la collecte des données dans la stratégie de sécurité pour chacun de vos abonnements et toutes les machines virtuelles de vos abonnements.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-114">Recommends that you turn on data collection in the security policy for each of your subscriptions and all virtual machines (VMs) in your subscriptions.</span></span> |
| [<span data-ttu-id="f5ca5-115">Activer le chiffrement pour le compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="f5ca5-115">Enable encryption for Azure Storage Account</span></span>](security-center-enable-encryption-for-storage-account.md) | <span data-ttu-id="f5ca5-116">Recommande d’activer Azure Storage Service Encryption pour les données au repos.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-116">Recommends that you enable Azure Storage Service Encryption for data at rest.</span></span> <span data-ttu-id="f5ca5-117">SSE (Storage Service Encryption) chiffre les données lorsqu’elles sont écrites dans le stockage Azure et les déchiffre avant récupération.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-117">Storage Service Encryption (SSE) works by encrypting the data when it is written to Azure storage and decrypts before retrieval.</span></span> <span data-ttu-id="f5ca5-118">SSE est actuellement disponible uniquement pour le service BLOB Azure et peut être utilisé pour les objets blob de blocs, les objets blob de pages les objets blob Append.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-118">SSE is currently available only for the Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span> <span data-ttu-id="f5ca5-119">Pour en savoir plus, consultez [Azure Storage Service Encryption pour les données au repos](../storage/common/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="f5ca5-119">To learn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span></br><span data-ttu-id="f5ca5-120">SSE est uniquement pris en charge sur les comptes de stockage Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-120">SSE is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="f5ca5-121">Les comptes de stockage Classic ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-121">Classic storage accounts are currently not supported.</span></span> <span data-ttu-id="f5ca5-122">Pour comprendre les modèles de déploiement de type classique et Resource Manager, consultez [Modèles de déploiement Azure](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="f5ca5-122">To understand the classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span> |
| [<span data-ttu-id="f5ca5-123">Corriger des vulnérabilités du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="f5ca5-123">Remediate OS vulnerabilities</span></span>](security-center-remediate-os-vulnerabilities.md) |<span data-ttu-id="f5ca5-124">Recommande d’aligner les configurations de votre système d’exploitation sur les règles de configuration recommandées, comme le fait de ne pas permettre l’enregistrement des mots de passe.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-124">Recommends that you align your OS configurations with the recommended configuration rules, e.g. do not allow passwords to be saved.</span></span> |
| [<span data-ttu-id="f5ca5-125">Appliquer des mises à jour système</span><span class="sxs-lookup"><span data-stu-id="f5ca5-125">Apply system updates</span></span>](security-center-apply-system-updates.md) |<span data-ttu-id="f5ca5-126">Recommande le déploiement des mises à jour de sécurité du système et des mises à jour critiques manquantes sur les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-126">Recommends that you deploy missing system security and critical updates to VMs.</span></span> |
| [<span data-ttu-id="f5ca5-127">Appliquer un contrôle d’accès réseau Juste à temps</span><span class="sxs-lookup"><span data-stu-id="f5ca5-127">Apply a Just-In-Time network access control</span></span>](security-center-just-in-time.md) | <span data-ttu-id="f5ca5-128">Recommande d’appliquer un accès Juste à temps à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-128">Recommends that you apply just in time VM access.</span></span> <span data-ttu-id="f5ca5-129">La fonctionnalité Juste à temps est disponible en préversion pour le niveau Standard de Security Center.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-129">The just in time feature is in preview and available on the Standard tier of Security Center.</span></span> <span data-ttu-id="f5ca5-130">Consultez [Tarification](security-center-pricing.md) pour en savoir plus sur les niveaux tarifaires de Security Center.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-130">See [Pricing](security-center-pricing.md) to learn more about Security Center's pricing tiers.</span></span> |
| [<span data-ttu-id="f5ca5-131">Redémarrage après des mises à jour système</span><span class="sxs-lookup"><span data-stu-id="f5ca5-131">Reboot after system updates</span></span>](security-center-apply-system-updates.md#reboot-after-system-updates) |<span data-ttu-id="f5ca5-132">Recommande de redémarrer une machine virtuelle pour terminer le processus de mise à jour du système.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-132">Recommends that you reboot a VM to complete the process of applying system updates.</span></span> |
| [<span data-ttu-id="f5ca5-133">Installer Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="f5ca5-133">Install Endpoint Protection</span></span>](security-center-install-endpoint-protection.md) |<span data-ttu-id="f5ca5-134">Recommande l’approvisionnement de logiciels anti-programme malveillant sur les machines virtuelles (Windows uniquement).</span><span class="sxs-lookup"><span data-stu-id="f5ca5-134">Recommends that you provision antimalware programs to VMs (Windows VMs only).</span></span> |
| [<span data-ttu-id="f5ca5-135">Résoudre les alertes d’intégrité Endpoint Protection</span><span class="sxs-lookup"><span data-stu-id="f5ca5-135">Resolve Endpoint Protection health alerts</span></span>](security-center-resolve-endpoint-protection-health-alerts.md) |<span data-ttu-id="f5ca5-136">Recommande la résolution des défaillances de protection de point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-136">Recommends that you resolve endpoint protection failures.</span></span> |
| [<span data-ttu-id="f5ca5-137">Activer l’agent de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f5ca5-137">Enable VM Agent</span></span>](security-center-enable-vm-agent.md) |<span data-ttu-id="f5ca5-138">Vous permet de connaître les machines virtuelles qui nécessitent l’agent de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-138">Enables you to see which VMs require the VM Agent.</span></span> <span data-ttu-id="f5ca5-139">L’agent de machine virtuelle doit être installé sur les machines virtuelles pour approvisionner l’analyse des correctifs, l’analyse des lignes de base et les logiciels anti-programme malveillant.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-139">The VM Agent must be installed on VMs in order to provision patch scanning, baseline scanning, and antimalware programs.</span></span> <span data-ttu-id="f5ca5-140">L’agent de machine virtuelle est installé par défaut sur les machines virtuelles déployées depuis Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-140">The VM Agent is installed by default for VMs that are deployed from the Azure Marketplace.</span></span> <span data-ttu-id="f5ca5-141">L’article [Installer l’agent de machine virtuelle – Deuxième partie](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) fournit des informations sur l’installation de l’agent de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-141">The article [VM Agent and Extensions – Part 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) provides information on how to install the VM Agent.</span></span> |
| [<span data-ttu-id="f5ca5-142">Apply disk encryption (Appliquer le chiffrement de disque Azure Disk Encryption)</span><span class="sxs-lookup"><span data-stu-id="f5ca5-142">Apply disk encryption</span></span>](security-center-apply-disk-encryption.md) |<span data-ttu-id="f5ca5-143">Recommande le chiffrement des disques des machines virtuelles à l’aide d’Azure Disk Encryption (Windows et Linux).</span><span class="sxs-lookup"><span data-stu-id="f5ca5-143">Recommends that you encrypt your VM disks using Azure Disk Encryption (Windows and Linux VMs).</span></span> <span data-ttu-id="f5ca5-144">Le chiffrement est recommandé pour les systèmes d’exploitation et les volumes de données de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-144">Encryption is recommended for both the OS and data volumes on your VM.</span></span> |
| [<span data-ttu-id="f5ca5-145">Mettre à jour la version du système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="f5ca5-145">Update OS version</span></span>](security-center-update-os-version.md) |<span data-ttu-id="f5ca5-146">Recommande de mettre à jour la version du système d’exploitation de votre service Cloud vers la version la plus récente disponible pour votre famille de systèmes d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-146">Recommends that you update the operating system (OS) version for your Cloud Service to the most recent version available for your OS family.</span></span>  <span data-ttu-id="f5ca5-147">Pour en savoir plus sur Cloud Services, consultez [Vue d’ensemble de Cloud Services](../cloud-services/cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="f5ca5-147">To learn more about Cloud Services, see the [Cloud Services overview](../cloud-services/cloud-services-choose-me.md).</span></span> |
| [<span data-ttu-id="f5ca5-148">Évaluation des vulnérabilités non installée</span><span class="sxs-lookup"><span data-stu-id="f5ca5-148">Vulnerability assessment not installed</span></span>](security-center-vulnerability-assessment-recommendations.md) |<span data-ttu-id="f5ca5-149">Recommande d’installer une solution d’évaluation des vulnérabilités sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-149">Recommends that you install a vulnerability assessment solution on your VM.</span></span> |
| [<span data-ttu-id="f5ca5-150">Corriger des vulnérabilités</span><span class="sxs-lookup"><span data-stu-id="f5ca5-150">Remediate vulnerabilities</span></span>](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |<span data-ttu-id="f5ca5-151">Vous permet de voir les vulnérabilités du système et des applications détectées par la solution d’évaluation des vulnérabilités installée sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-151">Enables you to see system and application vulnerabilities detected by the vulnerability assessment solution installed on your VM.</span></span> |

## <a name="see-also"></a><span data-ttu-id="f5ca5-152">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f5ca5-152">See also</span></span>
<span data-ttu-id="f5ca5-153">Pour en savoir plus sur les recommandations qui s’appliquent à d’autres types de ressources Azure, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="f5ca5-153">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="f5ca5-154">Protection de vos applications dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f5ca5-154">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="f5ca5-155">Protection de votre réseau dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f5ca5-155">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)
* [<span data-ttu-id="f5ca5-156">Protection de votre service SQL Azure dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="f5ca5-156">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="f5ca5-157">Pour plus d’informations sur le Centre de sécurité, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="f5ca5-157">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="f5ca5-158">[Définition des stratégies de sécurité dans Azure Security Center](security-center-policies.md) : découvrez comment configurer des stratégies de sécurité pour vos groupes de ressources et abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-158">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="f5ca5-159">[Gestion et résolution des alertes de sécurité dans Azure Security Center](security-center-managing-and-responding-alerts.md) : découvrez comment gérer et résoudre les alertes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-159">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="f5ca5-160">[FAQ Azure Security Center](security-center-faq.md) : forum aux questions concernant l’utilisation de ce service.</span><span class="sxs-lookup"><span data-stu-id="f5ca5-160">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>