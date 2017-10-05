---
title: "Protéger les données personnelles dans Microsoft Azure | Microsoft Docs"
description: "Premier article d’une série visant à vous aider à utiliser Azure pour protéger des données personnelles"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: dfb046374397c8a19672ce6b67741903fff6e178
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="protect-personal-data-in-microsoft-azure"></a><span data-ttu-id="08096-103">Protéger les données personnelles dans Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="08096-103">Protect personal data in Microsoft Azure</span></span>

<span data-ttu-id="08096-104">Cet article présente une série d’articles qui vous aident à utiliser les services et technologies de sécurité Azure pour protéger des données personnelles.</span><span class="sxs-lookup"><span data-stu-id="08096-104">This article introduces a series of articles that help you use Azure security technologies and services to protect personal data.</span></span> <span data-ttu-id="08096-105">La sécurité est une exigence clé pour un grand nombre d’initiatives en matière de gouvernance et de mise en conformité des entreprises et de leurs activités.</span><span class="sxs-lookup"><span data-stu-id="08096-105">This is a key requirement for many corporate and industry compliance and governance initiatives.</span></span> <span data-ttu-id="08096-106">Le scénario, la définition du problème et les objectifs de l’entreprise sont inclus ici.</span><span class="sxs-lookup"><span data-stu-id="08096-106">The scenario, problem statement and company goals are included here.</span></span>

## <a name="scenario-and-problem-statement"></a><span data-ttu-id="08096-107">Scénario et définition du problème</span><span class="sxs-lookup"><span data-stu-id="08096-107">Scenario and problem statement</span></span>

<span data-ttu-id="08096-108">Une importante compagnie de croisière, dont le siège se situe aux États-Unis, étend ses opérations afin de proposer des circuits dans les Mers Méditerranée, Adriatique et Baltique, ainsi que dans les îles Britanniques.</span><span class="sxs-lookup"><span data-stu-id="08096-108">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, Adriatic, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="08096-109">Pour soutenir cet effort, elle a fait l’acquisition de plusieurs lignes de croisière plus petites basées en Italie, en Allemagne, au Danemark et au Royaume-Uni.</span><span class="sxs-lookup"><span data-stu-id="08096-109">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and the U.K.</span></span>

<span data-ttu-id="08096-110">La compagnie utilise Microsoft Azure pour stocker les données d’entreprise dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="08096-110">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="08096-111">Cela peut concerner des employés ou des informations sur les clients tels que :</span><span class="sxs-lookup"><span data-stu-id="08096-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="08096-112">Adresses</span><span class="sxs-lookup"><span data-stu-id="08096-112">addresses</span></span>
- <span data-ttu-id="08096-113">Numéros de téléphone</span><span class="sxs-lookup"><span data-stu-id="08096-113">phone numbers</span></span>
- <span data-ttu-id="08096-114">Numéros d’identification fiscale</span><span class="sxs-lookup"><span data-stu-id="08096-114">tax identification numbers</span></span>
- <span data-ttu-id="08096-115">informations médicales</span><span class="sxs-lookup"><span data-stu-id="08096-115">medical information</span></span>
- <span data-ttu-id="08096-116">Informations de carte de crédit</span><span class="sxs-lookup"><span data-stu-id="08096-116">credit card information</span></span>

<span data-ttu-id="08096-117">La société doit protéger la confidentialité des données d’employé et client lors de la rendre les données accessibles à ces services qui en ont besoin.</span><span class="sxs-lookup"><span data-stu-id="08096-117">The company must protect the privacy of employee and customer data while making data accessible to those departments that need it.</span></span> <span data-ttu-id="08096-118">(Notamment, les services de paie et de réservation.)</span><span class="sxs-lookup"><span data-stu-id="08096-118">(such as payroll and reservations departments)</span></span>

## <a name="company-goals"></a><span data-ttu-id="08096-119">Objectifs de l’entreprise</span><span class="sxs-lookup"><span data-stu-id="08096-119">Company goals</span></span> 

- <span data-ttu-id="08096-120">Les sources de données qui contiennent des données personnelles sont chiffrées quand elles se trouvent dans le stockage cloud.</span><span class="sxs-lookup"><span data-stu-id="08096-120">Data sources that contain personal data are encrypted when residing in cloud storage.</span></span>

- <span data-ttu-id="08096-121">Les données personnelles transférées d’un emplacement à un autre sont chiffrées pendant le transit.</span><span class="sxs-lookup"><span data-stu-id="08096-121">Personal data that is transferred from one location to another is encrypted while in-transit.</span></span> <span data-ttu-id="08096-122">Ce chiffrement a lieu si les données sont transmises sur le réseau virtuel ou sur Internet entre le centre de données d’entreprise et le cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="08096-122">This is true if the data is traveling across the virtual network or across the Internet between the corporate datacenter and the Azure cloud.</span></span>

- <span data-ttu-id="08096-123">La confidentialité et l’intégrité des données personnelles sont protégées contre tout accès non autorisé par de puissantes technologies de gestion des identités et de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="08096-123">Confidentiality and integrity of personal data is protected from unauthorized access by strong identity management and access control technologies.</span></span>

- <span data-ttu-id="08096-124">Les données personnelles sont protégées contre toute exposition par violation de la sécurité au moyen d’une surveillance des vulnérabilités et des menaces.</span><span class="sxs-lookup"><span data-stu-id="08096-124">Personal data is protected from exposure via data breach via monitoring for vulnerabilities and threats.</span></span>

- <span data-ttu-id="08096-125">L’état de la sécurité des services Azure qui stockent ou transmettent des données personnelles est évalué pour identifier les opportunités de mieux protéger les données personnelles.</span><span class="sxs-lookup"><span data-stu-id="08096-125">The security state of Azure services that store or transmit personal data is assessed to identify opportunities to better protect personal data.</span></span>

## <a name="data-protection-guidance"></a><span data-ttu-id="08096-126">Conseils de protection des données</span><span class="sxs-lookup"><span data-stu-id="08096-126">Data protection guidance</span></span>

<span data-ttu-id="08096-127">Les articles suivants contiennent des instructions techniques qui vous aideront à atteindre les objectifs de protection des données personnelles indiqués ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="08096-127">The following articles contain technical how-to guidance that will help you attain the personal data protection goals listed above:</span></span>

- [<span data-ttu-id="08096-128">Technologies de chiffrement Azure</span><span class="sxs-lookup"><span data-stu-id="08096-128">Azure encryption technologies</span></span>](protect-personal-data-at-rest.md)

- [<span data-ttu-id="08096-129">Technologies de chiffrement Azure</span><span class="sxs-lookup"><span data-stu-id="08096-129">Azure encryption technologies</span></span>](protect-personal-data-in-transit-encryption.md)

- [<span data-ttu-id="08096-130">Technologies d’identité et accès Azure</span><span class="sxs-lookup"><span data-stu-id="08096-130">Azure identity and access technologies</span></span>](protect-personal-data-identity-access-controls.md)

- [<span data-ttu-id="08096-131">Technologies de sécurité réseau Azure</span><span class="sxs-lookup"><span data-stu-id="08096-131">Azure network security technologies</span></span>](protect-personal-data-network-security.md)

- [<span data-ttu-id="08096-132">Centre de sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="08096-132">Azure Security Center</span></span>](protect-personal-data-azure-security-center.md)



## <a name="next-steps"></a><span data-ttu-id="08096-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="08096-133">Next steps</span></span>

- [<span data-ttu-id="08096-134">Site d’informations relatives à la sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="08096-134">Azure Security Information Site</span></span>](https://aka.ms/AzureSecInfo)

- [<span data-ttu-id="08096-135">Centre de gestion de la confidentialité Microsoft</span><span class="sxs-lookup"><span data-stu-id="08096-135">Microsoft Trust Center</span></span>](https://www.microsoft.com/TrustCenter/default.aspx)

- [<span data-ttu-id="08096-136">Centre de sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="08096-136">Azure Security Center</span></span>](https://azure.microsoft.com/services/security-center/)

- [<span data-ttu-id="08096-137">Blog de l’équipe de sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="08096-137">Azure Security Team Blog</span></span>](https://www.azuresecurityorg)

- [<span data-ttu-id="08096-138">Blog Azure.com - Sécurité</span><span class="sxs-lookup"><span data-stu-id="08096-138">Azure.com Blog - Security</span></span>](https://azure.microsoft.com/blog/topics/security/)
