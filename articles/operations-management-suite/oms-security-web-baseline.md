---
title: "Solution de sécurité et d’audit d’Operations Management Suite - Base de référence web | Microsoft Docs"
description: "Ce document explique comment utiliser la solution de sécurité et d’audit d’Operations Management Suite (OMS) pour effectuer une évaluation de la base de référence web pour l’ensemble des serveurs web surveillés, afin de déterminer leur niveau de conformité et de sécurité."
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
ms.openlocfilehash: 0d4707dc0c0ffbf40d0d10a6d12b9709a9655258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="06285-103">Évaluation de la base de référence web dans la solution de sécurité et d’audit d’Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="06285-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="06285-104">Ce document vous aide à utiliser les capacités d’évaluation de la base de référence web de [la solution de sécurité et d’audit d’Operations Management Suite](operations-management-suite-overview.md) pour accéder à l’état de sécurité des ressources analysées.</span><span class="sxs-lookup"><span data-stu-id="06285-104">This document helps you to use [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) web baseline assessment capabilities to access the secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="06285-105">Qu’est-ce qu’une évaluation de la base de référence web ?</span><span class="sxs-lookup"><span data-stu-id="06285-105">What is Web Baseline Assessment?</span></span>
<span data-ttu-id="06285-106">La solution de sécurité d’OMS permet actuellement d’évaluer la base de référence de sécurité pour les systèmes d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="06285-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="06285-107">Elle analyse les paramètres de système d’exploitation de vos serveurs toutes les 24 heures et affiche les paramètres potentiellement vulnérables.</span><span class="sxs-lookup"><span data-stu-id="06285-107">It scans the operating system settings of your servers every 24 hours and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="06285-108">Pour plus d’informations à ce sujet, consultez [Évaluation de la base de référence dans la solution de sécurité et d’audit d’Operations Management Suite](oms-security-baseline.md).</span><span class="sxs-lookup"><span data-stu-id="06285-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information on this.</span></span>

<span data-ttu-id="06285-109">L’objectif d’une évaluation de la base de référence web consiste à identifier les paramètres de serveur web potentiellement vulnérables.</span><span class="sxs-lookup"><span data-stu-id="06285-109">The goal of the web baseline assessment is to find potentially vulnerable web server settings.</span></span> <span data-ttu-id="06285-110">On distingue trois principales sources pour les configurations de base de référence web : les configurations .NET, ASP.NET et IIS.</span><span class="sxs-lookup"><span data-stu-id="06285-110">The three primary sources for the web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="06285-111">Tout comme l’évaluation de la base de référence du système d’exploitation, la solution de sécurité d’OMS va analyser vos serveurs web toutes les 24 heures et fournir un aperçu de leur état de sécurité.</span><span class="sxs-lookup"><span data-stu-id="06285-111">Just like the operating system baseline assessment, OMS Security is going to scan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="06285-112">Dans Internet Information Services (IIS), les configurations sont hautement personnalisables, ce qui permet de remplacer différents niveaux de site et d’application.</span><span class="sxs-lookup"><span data-stu-id="06285-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels to be overridden.</span></span> <span data-ttu-id="06285-113">L’analyseur vérifie les paramètres au niveau de chaque site/application en complément du niveau racine par défaut.</span><span class="sxs-lookup"><span data-stu-id="06285-113">The scanner checks the settings at each application/site level in addition to the default root level.</span></span> <span data-ttu-id="06285-114">Vous pouvez ainsi identifier l’emplacement des paramètres potentiellement vulnérables et y remédier rapidement.</span><span class="sxs-lookup"><span data-stu-id="06285-114">This helps you to identify potential vulnerability settings locations and quickly remediate.</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="06285-115">Évaluation de la base de référence de la sécurité web</span><span class="sxs-lookup"><span data-stu-id="06285-115">Web Security Baseline Assessment</span></span>
<span data-ttu-id="06285-116">Pour cette version préliminaire, cette fonctionnalité sera accessible à l’aide de l’option de recherche d’OMS.</span><span class="sxs-lookup"><span data-stu-id="06285-116">For this preview this feature is going to be accessed using the OMS Search option.</span></span> <span data-ttu-id="06285-117">Suivez les étapes ci-dessous pour exécuter la requête appropriée :</span><span class="sxs-lookup"><span data-stu-id="06285-117">Follow the steps below to perform the appropriated query:</span></span>

1. <span data-ttu-id="06285-118">Dans le tableau de bord principal de **Microsoft Operations Management Suite**, cliquez sur la vignette **Sécurité et audit**.</span><span class="sxs-lookup"><span data-stu-id="06285-118">In the **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="06285-119">Dans le tableau de bord **Sécurité et audit**, cliquez sur le bouton **Recherche dans les journaux**.</span><span class="sxs-lookup"><span data-stu-id="06285-119">In the **Security and Audit** dashboard, click **Log Search** button.</span></span>
3. <span data-ttu-id="06285-120">La première requête que vous pouvez utiliser est le **résumé de l’évaluation de la base de référence Web**.</span><span class="sxs-lookup"><span data-stu-id="06285-120">The first query that you can use is the **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="06285-121">Dans le champ **Begin search here** (Lancer la recherche ici), tapez la requête suivante : Type*=SecurityBaselineSummary BaselineType=web*.</span><span class="sxs-lookup"><span data-stu-id="06285-121">In the **Begin search here** field, type this query: Type*=SecurityBaselineSummary BaselineType=web*.</span></span> <span data-ttu-id="06285-122">L’écran suivant présente un exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="06285-122">The following screen has an output sample:</span></span>

![Résumé de l’évaluation de la base de référence web](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> <span data-ttu-id="06285-124">Dans cette requête, chaque enregistrement indique un récapitulatif de l’évaluation sur un serveur donné.</span><span class="sxs-lookup"><span data-stu-id="06285-124">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="06285-125">Dans la zone **Recherche dans les journaux**, vous pouvez taper différentes requêtes pour obtenir davantage d’informations sur l’évaluation de la base de référence web.</span><span class="sxs-lookup"><span data-stu-id="06285-125">Once you are in the **Log Search**, you can type different queries to obtain more information about the web baseline assessment.</span></span> <span data-ttu-id="06285-126">En plus de la requête précédente, vous pouvez également utiliser les requêtes suivantes dans cette version préliminaire.</span><span class="sxs-lookup"><span data-stu-id="06285-126">In addition to the previous query, you can also use the following ones in this preview.</span></span>

<span data-ttu-id="06285-127">**Évaluation de la règle de base de référence web** : chaque enregistrement représente une seule évaluation de la règle de base de référence web sur un seul serveur.</span><span class="sxs-lookup"><span data-stu-id="06285-127">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="06285-128">Il inclut toutes les données de la règle, l’emplacement, le résultat attendu et le résultat réel.</span><span class="sxs-lookup"><span data-stu-id="06285-128">It includes all data for the rule, location, the expected result, and the actual result.</span></span>

<span data-ttu-id="06285-129">**Requête** : Type*=SecurityBaseline BaselineType=web*</span><span class="sxs-lookup"><span data-stu-id="06285-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span></span>

![Évaluation de la règle de base de référence web](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

<span data-ttu-id="06285-131">**Afficher tous les résultats d’un serveur spécifique** : cette requête montre comment afficher les résultats d’un serveur spécifique.</span><span class="sxs-lookup"><span data-stu-id="06285-131">**Show all results for a specific server**: This query shows how to see results of a specific server.</span></span>

<span data-ttu-id="06285-132">**Requête** : *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span><span class="sxs-lookup"><span data-stu-id="06285-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span></span>

![Tous les résultats](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="06285-134">Vous pouvez également utiliser ces enregistrements/requêtes pour créer vos propres tableaux de bord, rapports ou alertes.</span><span class="sxs-lookup"><span data-stu-id="06285-134">You can also use these records/queries to create your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="06285-135">L’écran ci-dessous présente un exemple de contrôle d’interface utilisateur que vous pouvez ajouter à votre tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="06285-135">The screen below has a sample UI control that you can add to your dashboard.</span></span> <span data-ttu-id="06285-136">Pour savoir comment visualiser vos données à l’aide du Concepteur de vue d’OMS, cliquez [ici](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span><span class="sxs-lookup"><span data-stu-id="06285-136">You can learn how to visualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="06285-137">L’écran ci-dessous montre à quoi ressemble la mosaïque une fois que vous avez effectué cette personnalisation.</span><span class="sxs-lookup"><span data-stu-id="06285-137">The screen below is an example of how the tile will look like once you make this customization.</span></span>

![Exemple d’interface utilisateur](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> <span data-ttu-id="06285-139">Si vous souhaitez connaître les paramètres qui sont vérifiés pour l’évaluation de la base de référence, vous pouvez télécharger [cette feuille de calcul Excel](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) qui contient ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="06285-139">If you would like to know the settings that are checked for the baseline assessment, you can download [this Excel spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) that contains these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="06285-140">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="06285-140">See also</span></span>
<span data-ttu-id="06285-141">Dans ce document, vous avez découvert la fonction d’évaluation de la base de référence web de la solution de sécurité et d’audit d’OMS.</span><span class="sxs-lookup"><span data-stu-id="06285-141">In this document, you learned about OMS Security and Audit web baseline assessment.</span></span> <span data-ttu-id="06285-142">Pour plus d’informations sur la sécurité OMS, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="06285-142">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="06285-143">Présentation - Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="06285-143">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="06285-144">Surveiller et répondre aux alertes de sécurité dans la solution de sécurité et d’audit d’Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="06285-144">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="06285-145">Surveillance des ressources dans la solution de sécurité et d’audit d’Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="06285-145">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

