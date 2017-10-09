---
title: "aaaProtect des données personnelles dans Microsoft Azure | Documents Microsoft"
description: "Tout d’abord l’article dans une série d’articles toohelp vous utilisez Azure tooprotect des données personnelles"
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
ms.openlocfilehash: cbffd3872552cbd0f12539535898c41ecf7789e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-in-microsoft-azure"></a><span data-ttu-id="605c7-103">Protéger les données personnelles dans Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="605c7-103">Protect personal data in Microsoft Azure</span></span>

<span data-ttu-id="605c7-104">Cet article présente une série d’articles qui vous aident à utiliser les données personnelles tooprotect services et technologies de sécurité Azure.</span><span class="sxs-lookup"><span data-stu-id="605c7-104">This article introduces a series of articles that help you use Azure security technologies and services tooprotect personal data.</span></span> <span data-ttu-id="605c7-105">La sécurité est une exigence clé pour un grand nombre d’initiatives en matière de gouvernance et de mise en conformité des entreprises et de leurs activités.</span><span class="sxs-lookup"><span data-stu-id="605c7-105">This is a key requirement for many corporate and industry compliance and governance initiatives.</span></span> <span data-ttu-id="605c7-106">scénario de Hello, objectifs d’entreprise et d’instruction problème sont inclus ici.</span><span class="sxs-lookup"><span data-stu-id="605c7-106">hello scenario, problem statement and company goals are included here.</span></span>

## <a name="scenario-and-problem-statement"></a><span data-ttu-id="605c7-107">Scénario et définition du problème</span><span class="sxs-lookup"><span data-stu-id="605c7-107">Scenario and problem statement</span></span>

<span data-ttu-id="605c7-108">Une société de croisière volumineux en hello États-Unis, étend ses itinéraires de toooffer d’opérations dans hello Méditerranée, Adriatique et mer Baltique, ainsi que hello britanniques.</span><span class="sxs-lookup"><span data-stu-id="605c7-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="605c7-109">toosupport ces efforts, elle a acquis plusieurs lignes croisière plus petits exercées en Italie, Allemagne, Danemark et hello Royaume-Uni</span><span class="sxs-lookup"><span data-stu-id="605c7-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span>

<span data-ttu-id="605c7-110">la société de Hello utilise des données d’entreprise de Microsoft Azure toostore dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="605c7-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="605c7-111">Cela peut concerner des employés ou des informations sur les clients tels que :</span><span class="sxs-lookup"><span data-stu-id="605c7-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="605c7-112">Adresses</span><span class="sxs-lookup"><span data-stu-id="605c7-112">addresses</span></span>
- <span data-ttu-id="605c7-113">Numéros de téléphone</span><span class="sxs-lookup"><span data-stu-id="605c7-113">phone numbers</span></span>
- <span data-ttu-id="605c7-114">Numéros d’identification fiscale</span><span class="sxs-lookup"><span data-stu-id="605c7-114">tax identification numbers</span></span>
- <span data-ttu-id="605c7-115">informations médicales</span><span class="sxs-lookup"><span data-stu-id="605c7-115">medical information</span></span>
- <span data-ttu-id="605c7-116">Informations de carte de crédit</span><span class="sxs-lookup"><span data-stu-id="605c7-116">credit card information</span></span>

<span data-ttu-id="605c7-117">société de Hello doit protection hello des données d’employé et client tout en effectuant des départements toothose accessible de données qui en ont besoin.</span><span class="sxs-lookup"><span data-stu-id="605c7-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="605c7-118">(Notamment, les services de paie et de réservation.)</span><span class="sxs-lookup"><span data-stu-id="605c7-118">(such as payroll and reservations departments)</span></span>

## <a name="company-goals"></a><span data-ttu-id="605c7-119">Objectifs de l’entreprise</span><span class="sxs-lookup"><span data-stu-id="605c7-119">Company goals</span></span> 

- <span data-ttu-id="605c7-120">Les sources de données qui contiennent des données personnelles sont chiffrées quand elles se trouvent dans le stockage cloud.</span><span class="sxs-lookup"><span data-stu-id="605c7-120">Data sources that contain personal data are encrypted when residing in cloud storage.</span></span>

- <span data-ttu-id="605c7-121">Les données personnelles qui sont transférées à partir d’un emplacement tooanother sont chiffrées pendant le transit.</span><span class="sxs-lookup"><span data-stu-id="605c7-121">Personal data that is transferred from one location tooanother is encrypted while in-transit.</span></span> <span data-ttu-id="605c7-122">Cela est vrai si hello données circulent entre les réseaux virtuels hello ou entre hello Internet entre hello de centre de données d’entreprise et hello cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="605c7-122">This is true if hello data is traveling across hello virtual network or across hello Internet between hello corporate datacenter and hello Azure cloud.</span></span>

- <span data-ttu-id="605c7-123">La confidentialité et l’intégrité des données personnelles sont protégées contre tout accès non autorisé par de puissantes technologies de gestion des identités et de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="605c7-123">Confidentiality and integrity of personal data is protected from unauthorized access by strong identity management and access control technologies.</span></span>

- <span data-ttu-id="605c7-124">Les données personnelles sont protégées contre toute exposition par violation de la sécurité au moyen d’une surveillance des vulnérabilités et des menaces.</span><span class="sxs-lookup"><span data-stu-id="605c7-124">Personal data is protected from exposure via data breach via monitoring for vulnerabilities and threats.</span></span>

- <span data-ttu-id="605c7-125">Hello état de la sécurité des services Azure qui stockent ou transmettre des données personnelles est évaluée tooidentify opportunités toobetter protéger les données personnelles.</span><span class="sxs-lookup"><span data-stu-id="605c7-125">hello security state of Azure services that store or transmit personal data is assessed tooidentify opportunities toobetter protect personal data.</span></span>

## <a name="data-protection-guidance"></a><span data-ttu-id="605c7-126">Conseils de protection des données</span><span class="sxs-lookup"><span data-stu-id="605c7-126">Data protection guidance</span></span>

<span data-ttu-id="605c7-127">Hello suivant articles contiennent des technique tooguidance procédure qui vous aideront à atteindre les objectifs de protection des données personnelles hello répertoriées ci-dessus :</span><span class="sxs-lookup"><span data-stu-id="605c7-127">hello following articles contain technical how-tooguidance that will help you attain hello personal data protection goals listed above:</span></span>

- [<span data-ttu-id="605c7-128">Technologies de chiffrement Azure</span><span class="sxs-lookup"><span data-stu-id="605c7-128">Azure encryption technologies</span></span>](protect-personal-data-at-rest.md)

- [<span data-ttu-id="605c7-129">Technologies de chiffrement Azure</span><span class="sxs-lookup"><span data-stu-id="605c7-129">Azure encryption technologies</span></span>](protect-personal-data-in-transit-encryption.md)

- [<span data-ttu-id="605c7-130">Technologies d’identité et accès Azure</span><span class="sxs-lookup"><span data-stu-id="605c7-130">Azure identity and access technologies</span></span>](protect-personal-data-identity-access-controls.md)

- [<span data-ttu-id="605c7-131">Technologies de sécurité réseau Azure</span><span class="sxs-lookup"><span data-stu-id="605c7-131">Azure network security technologies</span></span>](protect-personal-data-network-security.md)

- [<span data-ttu-id="605c7-132">Centre de sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="605c7-132">Azure Security Center</span></span>](protect-personal-data-azure-security-center.md)



## <a name="next-steps"></a><span data-ttu-id="605c7-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="605c7-133">Next steps</span></span>

- [<span data-ttu-id="605c7-134">Site d’informations relatives à la sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="605c7-134">Azure Security Information Site</span></span>](https://aka.ms/AzureSecInfo)

- [<span data-ttu-id="605c7-135">Centre de gestion de la confidentialité Microsoft</span><span class="sxs-lookup"><span data-stu-id="605c7-135">Microsoft Trust Center</span></span>](https://www.microsoft.com/TrustCenter/default.aspx)

- [<span data-ttu-id="605c7-136">Centre de sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="605c7-136">Azure Security Center</span></span>](https://azure.microsoft.com/services/security-center/)

- [<span data-ttu-id="605c7-137">Blog de l’équipe de sécurité Azure</span><span class="sxs-lookup"><span data-stu-id="605c7-137">Azure Security Team Blog</span></span>](https://www.azuresecurityorg)

- [<span data-ttu-id="605c7-138">Blog Azure.com - Sécurité</span><span class="sxs-lookup"><span data-stu-id="605c7-138">Azure.com Blog - Security</span></span>](https://azure.microsoft.com/blog/topics/security/)
