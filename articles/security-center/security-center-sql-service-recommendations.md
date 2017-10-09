---
title: "aaaProtecting SQL Azure services et données dans le centre de sécurité Azure | Documents Microsoft"
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
ms.openlocfilehash: 75d782d3c2418f9645139e4cd6ecb7765c488f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-azure-sql-service-and-data-in-azure-security-center"></a><span data-ttu-id="afdb7-103">Protection des données et du service SQL Azure dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="afdb7-103">Protecting Azure SQL service and data in Azure Security Center</span></span>
<span data-ttu-id="afdb7-104">Centre de sécurité Azure analyse l’état de la sécurité de vos ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="afdb7-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="afdb7-105">Lorsque le centre de sécurité identifie les éventuelles failles de sécurité, il crée des recommandations qui vous guident tout au long des processus de hello de configuration de contrôles de hello nécessité.</span><span class="sxs-lookup"><span data-stu-id="afdb7-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="afdb7-106">Recommandations s’appliquent à des types de ressources tooAzure : machines virtuelles (VM), mise en réseau, SQL et les applications et les données.</span><span class="sxs-lookup"><span data-stu-id="afdb7-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL and data, and applications.</span></span>

<span data-ttu-id="afdb7-107">Cet article traite des recommandations qui s’appliquent tooAzure SQL services et des données.</span><span class="sxs-lookup"><span data-stu-id="afdb7-107">This article addresses recommendations that apply tooAzure SQL service and data.</span></span> <span data-ttu-id="afdb7-108">Les recommandations se concentrent autour de l’audit des bases de données et des serveurs SQL Azure, de l’activation du chiffrement pour les bases de données SQL et de l’activation du chiffrement pour votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="afdb7-108">Recommendations center around enabling auditing for Azure SQL servers and databases, enabling encryption for SQL databases, and enabling encryption of your Azure storage account.</span></span>  <span data-ttu-id="afdb7-109">Tableau hello ci-dessous comme un toohelp de référence que vous comprenez hello disponible SQL service recommandations et les données et ce que fait chacun d’eux si vous l’appliquez.</span><span class="sxs-lookup"><span data-stu-id="afdb7-109">Use hello table below as a reference toohelp you understand hello available SQL service and data recommendations and what each one does if you apply it.</span></span>

## <a name="available-sql-service-and-data-recommendations"></a><span data-ttu-id="afdb7-110">Recommandations disponibles pour les données et le service SQL</span><span class="sxs-lookup"><span data-stu-id="afdb7-110">Available SQL service and data recommendations</span></span>
| <span data-ttu-id="afdb7-111">Recommandation</span><span class="sxs-lookup"><span data-stu-id="afdb7-111">Recommendation</span></span> | <span data-ttu-id="afdb7-112">Description</span><span class="sxs-lookup"><span data-stu-id="afdb7-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="afdb7-113">Activer l’audit et la détection des menaces dans les serveurs SQL</span><span class="sxs-lookup"><span data-stu-id="afdb7-113">Enable auditing and threat detection on SQL servers</span></span>](security-center-enable-auditing-on-sql-servers.md) |<span data-ttu-id="afdb7-114">Recommande l’activation de l’audit et de la détection des menaces pour les serveurs SQL Azure (service Azure SQL uniquement ; ne comprend pas les serveurs SQL exécutés sur des machines virtuelles).</span><span class="sxs-lookup"><span data-stu-id="afdb7-114">Recommends that you turn on auditing and threat detection for Azure SQL servers (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="afdb7-115">Activer l’audit et la détection des menaces dans les bases de données SQL</span><span class="sxs-lookup"><span data-stu-id="afdb7-115">Enable auditing and threat detection on SQL databases</span></span>](security-center-enable-auditing-on-sql-databases.md) |<span data-ttu-id="afdb7-116">Recommande l’activation de l’audit et de la détection des menaces pour les bases de données SQL Azure (service Azure SQL uniquement ; ne comprend pas les serveurs SQL exécutés sur des machines virtuelles).</span><span class="sxs-lookup"><span data-stu-id="afdb7-116">Recommends that you turn on auditing and threat detection for Azure SQL databases (Azure SQL service only; doesn't include SQL running on your virtual machines).</span></span> |
| [<span data-ttu-id="afdb7-117">Activer le chiffrement transparent des données des bases de données SQL</span><span class="sxs-lookup"><span data-stu-id="afdb7-117">Enable Transparent Data Encryption on SQL databases</span></span>](security-center-enable-transparent-data-encryption.md) |<span data-ttu-id="afdb7-118">Recommande l’activation du chiffrement pour les bases de données SQL (service Azure SQL uniquement).</span><span class="sxs-lookup"><span data-stu-id="afdb7-118">Recommends that you enable encryption for SQL databases (Azure SQL service only).</span></span> |

## <a name="see-also"></a><span data-ttu-id="afdb7-119">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="afdb7-119">See also</span></span>
<span data-ttu-id="afdb7-120">toolearn en savoir plus sur les recommandations qui s’appliquent les types de ressources Azure tooother, voir hello :</span><span class="sxs-lookup"><span data-stu-id="afdb7-120">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="afdb7-121">Protection de vos machines virtuelles dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="afdb7-121">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="afdb7-122">Protection de vos applications dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="afdb7-122">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="afdb7-123">Protection de votre réseau dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="afdb7-123">Protecting your network in Azure Security Center</span></span>](security-center-network-recommendations.md)

<span data-ttu-id="afdb7-124">toolearn en savoir plus sur le centre de sécurité, voir hello :</span><span class="sxs-lookup"><span data-stu-id="afdb7-124">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="afdb7-125">[Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) --Découvrez comment tooconfigure des stratégies de sécurité pour vos abonnements Azure et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="afdb7-125">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="afdb7-126">[Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) --Découvrez comment les alertes toosecurity toomanage et y répondre.</span><span class="sxs-lookup"><span data-stu-id="afdb7-126">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="afdb7-127">[Forum aux questions sur Azure Security Center](security-center-faq.md) --rechercher Forum aux questions sur l’utilisation du service de hello.</span><span class="sxs-lookup"><span data-stu-id="afdb7-127">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
