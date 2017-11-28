---
title: "Protection des données et du service SQL Azure dans Azure Security Center | Microsoft Docs"
description: "Ce document traite des recommandations d’Azure Security Center qui peuvent vous aider à protéger vos données et le service SQL Azure et à rester en conformité avec les stratégies de sécurité."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: bcae6987-05d0-4208-bca8-6a6ce7c9a1e3
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/03/2017
ms.author: terrylan
ms.openlocfilehash: 0c3a11e9a86767641533b16de1b96b4c59bfdf51
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a><span data-ttu-id="d9dbf-103">Protection des données et du service SQL Azure dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="d9dbf-103">Protecting Azure SQL service and data in Azure Security Center</span></span>
<span data-ttu-id="d9dbf-104">Le Centre de sécurité Azure analyse l’état de sécurité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="d9dbf-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="d9dbf-105">Lorsque Security Center identifie des failles de sécurité potentielles, il crée des recommandations qui vous guident tout au long du processus de configuration des contrôles nécessaires.</span><span class="sxs-lookup"><span data-stu-id="d9dbf-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="d9dbf-106">Ces recommandations s’appliquent aux types de ressources Azure : machines virtuelles, mise en réseau, SQL et données et applications.</span><span class="sxs-lookup"><span data-stu-id="d9dbf-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span></span>

<span data-ttu-id="d9dbf-107">Cet article traite des recommandations qui s’appliquent aux données et au service SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="d9dbf-107">This article addresses recommendations that apply to Azure SQL service and data.</span></span> <span data-ttu-id="d9dbf-108">Les recommandations se concentrent autour de l’audit des bases de données et des serveurs SQL Azure, de l’activation du chiffrement pour les bases de données SQL et de l’activation du chiffrement pour votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="d9dbf-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span></span>  <span data-ttu-id="d9dbf-109">Utilisez le tableau ci-dessous pour mieux comprendre les recommandations disponibles pour les données et le service SQL et leurs effets.</span><span class="sxs-lookup"><span data-stu-id="d9dbf-109">Use the table below as a reference to help you understand the available SQL service and data recommendations and what each one does if you apply it.</span></span>

## <a name="available-sql-service-and-data-recommendations"></a><span data-ttu-id="d9dbf-110">Recommandations disponibles pour les données et le service SQL</span><span class="sxs-lookup"><span data-stu-id="d9dbf-110">Available SQL service and data recommendations</span></span>
| <span data-ttu-id="d9dbf-111">Recommandation</span><span class="sxs-lookup"><span data-stu-id="d9dbf-111">Recommendation</span></span> | <span data-ttu-id="d9dbf-112">Description</span><span class="sxs-lookup"><span data-stu-id="d9dbf-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="d9dbf-113">Activer l’audit et la détection des menaces dans les serveurs SQL</span><span class="sxs-lookup"><span data-stu-id="d9dbf-113">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="d9dbf-114">Recommande l’activation de l’audit et de la détection des menaces pour les serveurs SQL Azure (service Azure SQL uniquement ; ne comprend pas les serveurs SQL exécutés sur des machines virtuelles).</span><span class="sxs-lookup"><span data-stu-id="d9dbf-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="d9dbf-115">Activer l’audit et la détection des menaces dans les bases de données SQL</span><span class="sxs-lookup"><span data-stu-id="d9dbf-115">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="d9dbf-116">Recommande l’activation de l’audit et de la détection des menaces pour les bases de données SQL Azure (service Azure SQL uniquement ; ne comprend pas les serveurs SQL exécutés sur des machines virtuelles).</span><span class="sxs-lookup"><span data-stu-id="d9dbf-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="d9dbf-117">Activer le chiffrement transparent des données des bases de données SQL</span><span class="sxs-lookup"><span data-stu-id="d9dbf-117">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="d9dbf-118">Recommande l’activation du chiffrement pour les bases de données SQL (service Azure SQL uniquement).</span><span class="sxs-lookup"><span data-stu-id="d9dbf-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span></span> |

## <a name="see-also"></a><span data-ttu-id="d9dbf-119">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="d9dbf-119">See also</span></span>
<span data-ttu-id="d9dbf-120">Pour en savoir plus sur les recommandations qui s’appliquent à d’autres types de ressources Azure, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="d9dbf-120">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="d9dbf-121">Protection de vos machines virtuelles dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="d9dbf-121">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="d9dbf-122">Protection de vos applications dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="d9dbf-122">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="d9dbf-123">Protection de votre réseau dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="d9dbf-123">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)

<span data-ttu-id="d9dbf-124">Pour plus d’informations sur le Centre de sécurité, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="d9dbf-124">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="d9dbf-125">[Définition des stratégies de sécurité dans Azure Security Center](security-center-policies.md) : découvrez comment configurer des stratégies de sécurité pour vos groupes de ressources et abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="d9dbf-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="d9dbf-126">[Gestion et résolution des alertes de sécurité dans Azure Security Center](security-center-managing-and-responding-alerts.md) : découvrez comment gérer et résoudre les alertes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="d9dbf-126">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="d9dbf-127">[FAQ Azure Security Center](security-center-faq.md) : forum aux questions concernant l’utilisation de ce service.</span><span class="sxs-lookup"><span data-stu-id="d9dbf-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
