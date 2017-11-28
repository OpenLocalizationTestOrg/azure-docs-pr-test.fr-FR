---
title: "aaaOperations gestion Suite de sécurité et Audit Solution Web base | Documents Microsoft"
description: "Ce document explique comment solution de sécurité d’OMS et d’Audit toouse tooperform une évaluation de la ligne de base web de tous les serveurs web analysés fins de conformité et sécurité."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="cf2a0-103">Évaluation de la base de référence web dans la solution de sécurité et d’audit d’Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="cf2a0-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="cf2a0-104">Ce document vous aide à toouse [Operations Management Suite (OMS) Solution de sécurité et d’Audit](operations-management-suite-overview.md) web d’évaluation de la ligne de base fonctionnalités tooaccess hello état de sécurisation de vos ressources analysés.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-104">This document helps you toouse [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) web baseline assessment capabilities tooaccess hello secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="cf2a0-105">Qu’est-ce qu’une évaluation de la base de référence web ?</span><span class="sxs-lookup"><span data-stu-id="cf2a0-105">What is Web Baseline Assessment?</span></span>
<span data-ttu-id="cf2a0-106">La solution de sécurité d’OMS permet actuellement d’évaluer la base de référence de sécurité pour les systèmes d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="cf2a0-107">Il analyse les paramètres de système d’exploitation hello de vos serveurs toutes les 24 heures et fournit un affichage des paramètres potentiellement vulnérables.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-107">It scans hello operating system settings of your servers every 24 hours and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="cf2a0-108">Pour plus d’informations à ce sujet, consultez [Évaluation de la base de référence dans la solution de sécurité et d’audit d’Operations Management Suite](oms-security-baseline.md).</span><span class="sxs-lookup"><span data-stu-id="cf2a0-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information on this.</span></span>

<span data-ttu-id="cf2a0-109">Hello vise d’évaluation de la ligne de base hello web paramètres du serveur web potentiellement vulnérables toofind.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-109">hello goal of hello web baseline assessment is toofind potentially vulnerable web server settings.</span></span> <span data-ttu-id="cf2a0-110">Hello trois sources principales pour les configurations de base hello web sont : configuration .NET, ASP.NET et IIS.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-110">hello three primary sources for hello web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="cf2a0-111">Simplement comme hello évaluation de ligne de base du système d’exploitation, sécurité OMS va tooscan votre chaque 24 heures des serveurs web et fournissent une vue à l’état de sécurité d’eux.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-111">Just like hello operating system baseline assessment, OMS Security is going tooscan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="cf2a0-112">Dans les services Internet (IIS), la configurations sont hautement personnalisables, et qui permet à différents toobe niveaux de site et l’application remplacée.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels toobe overridden.</span></span> <span data-ttu-id="cf2a0-113">le scanneur Hello vérifie les paramètres de hello à chaque niveau de site/application de niveau racine d’addition toohello par défaut.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-113">hello scanner checks hello settings at each application/site level in addition toohello default root level.</span></span> <span data-ttu-id="cf2a0-114">Cela vous permet des emplacements des paramètres de la vulnérabilité potentielle tooidentify et résoudre rapidement.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-114">This helps you tooidentify potential vulnerability settings locations and quickly remediate.</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="cf2a0-115">Évaluation de la base de référence de la sécurité web</span><span class="sxs-lookup"><span data-stu-id="cf2a0-115">Web Security Baseline Assessment</span></span>
<span data-ttu-id="cf2a0-116">Cette fonctionnalité va toobe accédé à l’aide d’option de recherche d’OMS hello pour cette version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-116">For this preview this feature is going toobe accessed using hello OMS Search option.</span></span> <span data-ttu-id="cf2a0-117">Suivez les étapes de hello sous requête hello affecté de tooperform :</span><span class="sxs-lookup"><span data-stu-id="cf2a0-117">Follow hello steps below tooperform hello appropriated query:</span></span>

1. <span data-ttu-id="cf2a0-118">Bonjour **Microsoft Operations Management Suite** cliquez sur le tableau de bord principal **sécurité et Audit** vignette.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-118">In hello **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="cf2a0-119">Bonjour **sécurité et Audit** tableau de bord, cliquez sur **recherche de journal** bouton.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-119">In hello **Security and Audit** dashboard, click **Log Search** button.</span></span>
3. <span data-ttu-id="cf2a0-120">Hello première requête que vous pouvez utiliser est hello **résumé de l’évaluation de ligne de base Web**.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-120">hello first query that you can use is hello **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="cf2a0-121">Bonjour **rechercher ici** , tapez cette requête : Type*= SecurityBaselineSummary BaselineType = web*.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-121">In hello **Begin search here** field, type this query: Type*=SecurityBaselineSummary BaselineType=web*.</span></span> <span data-ttu-id="cf2a0-122">Hello suivant écran présente un exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="cf2a0-122">hello following screen has an output sample:</span></span>

![Résumé de l’évaluation de la base de référence web](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> <span data-ttu-id="cf2a0-124">Dans cette requête, chaque enregistrement indique un récapitulatif de l’évaluation sur un serveur donné.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-124">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="cf2a0-125">Une fois que vous êtes dans hello **recherche de journal**, vous pouvez taper des requêtes différentes tooobtain plus d’informations sur l’évaluation de ligne de base hello web.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-125">Once you are in hello **Log Search**, you can type different queries tooobtain more information about hello web baseline assessment.</span></span> <span data-ttu-id="cf2a0-126">En outre toohello de requête précédente, vous pouvez également utiliser hello suivant celles dans cette version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-126">In addition toohello previous query, you can also use hello following ones in this preview.</span></span>

<span data-ttu-id="cf2a0-127">**Évaluation de la règle de base de référence web** : chaque enregistrement représente une seule évaluation de la règle de base de référence web sur un seul serveur.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-127">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="cf2a0-128">Elle inclut toutes les données de règle de hello, l’emplacement, les résultats hello attendu et de résultats réel hello.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-128">It includes all data for hello rule, location, hello expected result, and hello actual result.</span></span>

<span data-ttu-id="cf2a0-129">**Requête** : Type*=SecurityBaseline BaselineType=web*</span><span class="sxs-lookup"><span data-stu-id="cf2a0-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span></span>

![Évaluation de la règle de base de référence web](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

<span data-ttu-id="cf2a0-131">**Afficher tous les résultats d’un serveur spécifique**: cette requête montre l’affichage des résultats de toosee d’un serveur spécifique.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-131">**Show all results for a specific server**: This query shows how toosee results of a specific server.</span></span>

<span data-ttu-id="cf2a0-132">**Requête** : *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span><span class="sxs-lookup"><span data-stu-id="cf2a0-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span></span>

![Tous les résultats](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="cf2a0-134">Vous pouvez également utiliser ces toocreate enregistrements/requêtes vos propres tableaux de bord, rapports ou les alertes.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-134">You can also use these records/queries toocreate your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="cf2a0-135">écran de Hello ci-dessous présente un exemple de contrôle d’interface utilisateur que vous pouvez ajouter tooyour le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-135">hello screen below has a sample UI control that you can add tooyour dashboard.</span></span> <span data-ttu-id="cf2a0-136">Vous pouvez apprendre comment toovisualize vos données à l’aide du Concepteur de vue OMS [ici](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span><span class="sxs-lookup"><span data-stu-id="cf2a0-136">You can learn how toovisualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="cf2a0-137">écran Hello ci-dessous est un exemple de comment hello vignette ressemblera une fois que vous apportez cette personnalisation.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-137">hello screen below is an example of how hello tile will look like once you make this customization.</span></span>

![Exemple d’interface utilisateur](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> <span data-ttu-id="cf2a0-139">Si vous souhaitez que les paramètres de hello tooknow qui sont vérifiées pour l’évaluation de ligne de base hello, vous pouvez télécharger [cette feuille de calcul Excel](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) qui contient ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-139">If you would like tooknow hello settings that are checked for hello baseline assessment, you can download [this Excel spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) that contains these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="cf2a0-140">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="cf2a0-140">See also</span></span>
<span data-ttu-id="cf2a0-141">Dans ce document, vous avez découvert la fonction d’évaluation de la base de référence web de la solution de sécurité et d’audit d’OMS.</span><span class="sxs-lookup"><span data-stu-id="cf2a0-141">In this document, you learned about OMS Security and Audit web baseline assessment.</span></span> <span data-ttu-id="cf2a0-142">toolearn en savoir plus sur la sécurité d’OMS, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="cf2a0-142">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="cf2a0-143">Présentation - Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="cf2a0-143">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="cf2a0-144">Surveillance et réponse tooSecurity alertes Operations Management Suite de Solution de sécurité et d’Audit</span><span class="sxs-lookup"><span data-stu-id="cf2a0-144">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="cf2a0-145">Surveillance des ressources dans la solution de sécurité et d’audit d’Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="cf2a0-145">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

