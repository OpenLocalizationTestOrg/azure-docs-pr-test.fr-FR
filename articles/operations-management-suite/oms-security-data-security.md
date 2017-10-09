---
title: "aaaOperations gestion Suite de sécurité et la sécurité des données d’Audit solutions | Documents Microsoft"
description: "Ce document explique de quelle manière les données sont gérées et protégées dans la solution de sécurité et d’audit d’Operations Management Suite."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a><span data-ttu-id="99418-103">Solution de sécurité et d’audit d’Operations Management Suite - Sécurité des données</span><span class="sxs-lookup"><span data-stu-id="99418-103">Operations Management Suite Security and Audit solution data security</span></span>
<span data-ttu-id="99418-104">les clients toohelp empêcher, détecter et répondre toothreats, [Operations Management Suite (OMS) Solution de sécurité et d’Audit](operations-management-suite-overview.md) recueille et traite les données sur vos ressources, notamment :</span><span class="sxs-lookup"><span data-stu-id="99418-104">toohelp customers prevent, detect, and respond toothreats, [Operations Management Suite  (OMS) Security and Audit Solution](operations-management-suite-overview.md) collects and processes data about your resources, which includes:</span></span>

* <span data-ttu-id="99418-105">Journaux des événements de sécurité</span><span class="sxs-lookup"><span data-stu-id="99418-105">Security event log</span></span>
* <span data-ttu-id="99418-106">Suivi d’événements pour les événements Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="99418-106">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="99418-107">Événements d’audit AppLocker</span><span class="sxs-lookup"><span data-stu-id="99418-107">AppLocker auditing events</span></span>
* <span data-ttu-id="99418-108">Journal du pare-feu Windows</span><span class="sxs-lookup"><span data-stu-id="99418-108">Windows Firewall log</span></span>
* <span data-ttu-id="99418-109">Événements Advanced Threat Analytics</span><span class="sxs-lookup"><span data-stu-id="99418-109">Advanced Threat Analytics events</span></span>
* <span data-ttu-id="99418-110">Résultats de l’évaluation de la base de référence</span><span class="sxs-lookup"><span data-stu-id="99418-110">Results of baseline assessment</span></span>
* <span data-ttu-id="99418-111">Résultats de l’analyse anti-programme malveillant</span><span class="sxs-lookup"><span data-stu-id="99418-111">Results of antimalware assessment</span></span>
* <span data-ttu-id="99418-112">Résultats de l’évaluation des correctifs/mises à jour</span><span class="sxs-lookup"><span data-stu-id="99418-112">Results of update/patch assessment</span></span>
* <span data-ttu-id="99418-113">Flux auditées qui sont explicitement activés sur l’agent de hello</span><span class="sxs-lookup"><span data-stu-id="99418-113">Syslogs streams that are explicitly enabled on hello agent</span></span>

<span data-ttu-id="99418-114">Nous faisons de confidentialité de hello tooprotect engagements forts et sécurité de ces données.</span><span class="sxs-lookup"><span data-stu-id="99418-114">We make strong commitments tooprotect hello privacy and security of this data.</span></span> <span data-ttu-id="99418-115">Microsoft respecte les instructions de sécurité et de conformité toostrict : du codage toooperating un service.</span><span class="sxs-lookup"><span data-stu-id="99418-115">Microsoft adheres toostrict compliance and security guidelines—from coding toooperating a service.</span></span>
<span data-ttu-id="99418-116">Cet article explique comment les données sont gérées et protégées dans la solution de sécurité et d’audit d’Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="99418-116">This article explains how data is managed and safeguarded in OMS Security and Audit Solution.</span></span>

## <a name="data-sources"></a><span data-ttu-id="99418-117">Sources de données</span><span class="sxs-lookup"><span data-stu-id="99418-117">Data sources</span></span>
<span data-ttu-id="99418-118">OMS Solution de sécurité et d’Audit analyser les données à partir de vos Machines virtuelles et les ordinateurs physiques où hello OMS Agent est installé.</span><span class="sxs-lookup"><span data-stu-id="99418-118">OMS Security and Audit Solution analyze data from your Virtual Machines and physical computers where hello OMS Agent is installed.</span></span> <span data-ttu-id="99418-119">Elle peut collecter les informations de configuration relatives aux événements de sécurité, tels que les journaux IIS, les journaux d’audit et les journaux des événements Windows, ainsi que les messages syslog.</span><span class="sxs-lookup"><span data-stu-id="99418-119">OMS Security and Audit Solution can collect configuration information about security events, such as Windows event, audit logs, IIS logs and syslog messages.</span></span> <span data-ttu-id="99418-120">Il peut s’agir des données suivantes : type et version de système d’exploitation, processus en cours d’exécution, nom de machine, adresses IP, utilisateur connecté et ID de locataire.</span><span class="sxs-lookup"><span data-stu-id="99418-120">Examples of such data are: operating system type and version, running processes, machine name, IP addresses, logged in user, and tenant ID.</span></span>  

## <a name="data-protection"></a><span data-ttu-id="99418-121">Protection des données</span><span class="sxs-lookup"><span data-stu-id="99418-121">Data protection</span></span>
<span data-ttu-id="99418-122">**La segmentation des données**: données sont maintenues séparées logiquement sur chaque composant dans le service de hello.</span><span class="sxs-lookup"><span data-stu-id="99418-122">**Data segregation**: Data is kept logically separate on each component throughout hello service.</span></span> <span data-ttu-id="99418-123">Toutes les données sont balisées en fonction de l'organisation.</span><span class="sxs-lookup"><span data-stu-id="99418-123">All data is tagged per organization.</span></span> <span data-ttu-id="99418-124">Ce balisage est conservé tout au long du cycle de vie des données hello, et elle est appliquée à chaque couche de service de hello.</span><span class="sxs-lookup"><span data-stu-id="99418-124">This tagging persists throughout hello data lifecycle, and it is enforced at each layer of hello service.</span></span> 

<span data-ttu-id="99418-125">**Accès aux données**: recommandations de sécurité tooprovide et examiner les menaces de sécurité potentielles, le personnel de Microsoft peut accéder aux informations collectées ou analysé par les services.</span><span class="sxs-lookup"><span data-stu-id="99418-125">**Data access**: tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="99418-126">Nous respecter toohello [termes du contrat de Services en ligne Microsoft](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) et [déclaration de confidentialité](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), état que Microsoft ne sera pas utiliser les données clients ou dériver des informations à partir de celui-ci pour toute publication ou similaires à des fins commerciales.</span><span class="sxs-lookup"><span data-stu-id="99418-126">We adhere toohello [Microsoft Online Services Terms](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) and [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), which state that Microsoft will not use Customer Data or derive information from it for any advertising or similar commercial purposes.</span></span> <span data-ttu-id="99418-127">recommandations de sécurité tooprovide et examiner les menaces de sécurité potentielles, le personnel de Microsoft peut accéder aux informations collectées ou analysé par les services.</span><span class="sxs-lookup"><span data-stu-id="99418-127">tooprovide security recommendations and investigate potential security threats, Microsoft personnel may access information collected or analyzed by services.</span></span> <span data-ttu-id="99418-128">Nous utilisent uniquement les données client comme requis tooprovide vous avec Azure services, y compris à des fins compatible avec la fourniture de ces services.</span><span class="sxs-lookup"><span data-stu-id="99418-128">We only use Customer Data as needed tooprovide you with Azure services, including purposes compatible with providing those services.</span></span> <span data-ttu-id="99418-129">Vous conservez tous les droits tooyour possédant des données.</span><span class="sxs-lookup"><span data-stu-id="99418-129">You retain all rights tooyour own data.</span></span>

<span data-ttu-id="99418-130">**Utilisation des données**: Microsoft utilise des modèles et menaces vu sur plusieurs locataires tooenhance nos fonctions de détection et la prévention ; nous faire conformément aux engagements de confidentialité hello décrites dans nos [confidentialité Instruction](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span><span class="sxs-lookup"><span data-stu-id="99418-130">**Data use**: Microsoft uses patterns and threat intelligence seen across multiple tenants tooenhance our prevention and detection capabilities; we do so in accordance with hello privacy commitments described in our [Privacy Statement](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="99418-131">Emplacement des données est configuré au niveau d’espace de travail OMS hello, lors de la création d’espace de travail hello, qui fait partie hello initiale OMS sécurité et Audit du processus de configuration.</span><span class="sxs-lookup"><span data-stu-id="99418-131">Data location is configured at hello OMS workspace level, during hello workspace creation, which is part of hello initial OMS Security and Audit configuration process.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="99418-132">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="99418-132">See also</span></span>
<span data-ttu-id="99418-133">Ce document explique comment les données sont gérées et protégées dans OMS.</span><span class="sxs-lookup"><span data-stu-id="99418-133">In this document, you learned how data is managed and safeguarded in OMS.</span></span> <span data-ttu-id="99418-134">toolearn en savoir plus sur OMS solution de sécurité et d’Audit, consultez :</span><span class="sxs-lookup"><span data-stu-id="99418-134">toolearn more about OMS Security and Audit solution, see:</span></span>

* [<span data-ttu-id="99418-135">Présentation - Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="99418-135">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="99418-136">Surveillance et réponse tooSecurity alertes Operations Management Suite de Solution de sécurité et d’Audit</span><span class="sxs-lookup"><span data-stu-id="99418-136">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="99418-137">Surveillance des ressources dans la solution de sécurité et d’audit d’Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="99418-137">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

