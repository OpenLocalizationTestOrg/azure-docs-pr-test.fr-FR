---
title: "Considérations relatives à la conception d’identités hybrides Azure Active Directory : vue d’ensemble | Microsoft Docs"
description: "Vue d'ensemble et plan du contenu du guide des considérations relatives à la conception des identités hybrides"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 100509c4-0b83-4207-90c8-549ba8372cf7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: e2a70f2474298618dd8ee11c583f8f445d7eba7d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-hybrid-identity-design-considerations"></a><span data-ttu-id="70b6f-103">Considérations relatives à la conception d'identités hybrides Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70b6f-103">Azure Active Directory Hybrid Identity Design Considerations</span></span>
<span data-ttu-id="70b6f-104">Les périphériques grand public se multiplient dans le monde de l'entreprise et les applications cloud software-as-a-service (SaaS) sont faciles à adopter.</span><span class="sxs-lookup"><span data-stu-id="70b6f-104">Consumer-based devices are proliferating the corporate world, and cloud-based software-as-a-service (SaaS) applications are easy to adopt.</span></span> <span data-ttu-id="70b6f-105">Par conséquent, le maintien du contrôle d'accès des utilisateurs aux applications sur les plateformes cloud et les centres de données internes est difficile.</span><span class="sxs-lookup"><span data-stu-id="70b6f-105">As a result, maintaining control of users’ application access across internal datacenters and cloud platforms is challenging.</span></span>  

<span data-ttu-id="70b6f-106">Les solutions d'identité de Microsoft regroupent des fonctionnalités, locales et cloud, de création d'une identité d'utilisateur unique pour l'authentification et l'autorisation d'accès à toutes les ressources, indépendamment de l'emplacement.</span><span class="sxs-lookup"><span data-stu-id="70b6f-106">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization to all resources, regardless of location.</span></span> <span data-ttu-id="70b6f-107">Nous appelons cette identité « identité hybride ».</span><span class="sxs-lookup"><span data-stu-id="70b6f-107">We call this Hybrid Identity.</span></span> <span data-ttu-id="70b6f-108">Il existe différentes possibilités de conception et de configuration de l'identité hybride avec les solutions Microsoft et, dans certains cas, il peut être difficile de déterminer quelle est la combinaison qui répond le mieux aux besoins de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="70b6f-108">There are different design and configuration options for hybrid identity using Microsoft solutions, and in some case it might be difficult to determine which combination will best meet the needs of your organization.</span></span> 

<span data-ttu-id="70b6f-109">Ce guide des considérations relatives à la conception des identités hybrides vous aidera à comprendre comment concevoir la solution d'identité hybride idéale en fonction des besoins métier et technologiques de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="70b6f-109">This Hybrid Identity Design Considerations Guide will help you to understand how to design a hybrid identity solution that best fits the business and technology needs for your organization.</span></span>  <span data-ttu-id="70b6f-110">Ce guide décrit en détail une série d’étapes et de tâches que vous pouvez suivre pour concevoir une solution d’identité hybride qui réponde aux exigences spécifiques de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="70b6f-110">This guide details a series of steps and tasks that you can follow to help you design a hybrid identity solution that meets your organization’s unique requirements.</span></span> <span data-ttu-id="70b6f-111">Au fil des étapes et des tâches, le guide présente les technologies et les options appropriées à la disposition des entreprises pour satisfaire aux exigences de niveau de qualité fonctionnelle et de qualité de service (par exemple de disponibilité, d'évolutivité, de performances, de facilité de gestion et de sécurité).</span><span class="sxs-lookup"><span data-stu-id="70b6f-111">Throughout the steps and tasks, the guide will present the relevant technologies and feature options available to organizations to meet functional and service quality (such as availability, scalability, performance, manageability, and security) level requirements.</span></span> 

<span data-ttu-id="70b6f-112">Plus précisément, les objectifs du guide des considérations relatives à la conception des identités hybrides sont de répondre aux questions suivantes :</span><span class="sxs-lookup"><span data-stu-id="70b6f-112">Specifically, the hybrid identity design considerations guide goals are to answer the following questions:</span></span> 

* <span data-ttu-id="70b6f-113">Quelles sont les questions à poser et les réponses à obtenir pour mettre en place une conception d'identité hybride spécifique pour un domaine technologique ou une catégorie de problème qui réponde à mes exigences ?</span><span class="sxs-lookup"><span data-stu-id="70b6f-113">What questions do I need to ask and answer to drive a hybrid identity-specific design for a technology or problem domain that best meets my requirements?</span></span>
* <span data-ttu-id="70b6f-114">Quelle séquence d'activités dois-je effectuer pour concevoir une solution d'identité hybride pour ce domaine technologique ou cette catégorie de problème ?</span><span class="sxs-lookup"><span data-stu-id="70b6f-114">What sequence of activities should I complete to design a hybrid identity solution for the technology or problem domain?</span></span> 
* <span data-ttu-id="70b6f-115">Quelles options de technologie et de configuration d'identité hybride sont disponibles pour m'aider à répondre à mes exigences ?</span><span class="sxs-lookup"><span data-stu-id="70b6f-115">What hybrid identity technology and configuration options are available to help me meet my requirements?</span></span> <span data-ttu-id="70b6f-116">Quelles sont les compromis entre ces options afin que je puisse sélectionner la meilleure option pour mon entreprise ?</span><span class="sxs-lookup"><span data-stu-id="70b6f-116">What are the trade-offs between those options so that I can select the best option for my business?</span></span>

## <a name="who-is-this-guide-intended-for"></a><span data-ttu-id="70b6f-117">À qui ce guide est-il destiné ?</span><span class="sxs-lookup"><span data-stu-id="70b6f-117">Who is this guide intended for?</span></span>
 <span data-ttu-id="70b6f-118">Directeurs informatiques, directeurs des systèmes d'information, responsables de l'architecture des identités, architectes d'entreprise et architectes informatiques chargés de concevoir une solution d'identité hybride pour les entreprises de taille moyenne ou grande.</span><span class="sxs-lookup"><span data-stu-id="70b6f-118">CIO, CITO, Chief Identity Architects, Enterprise Architects and IT Architects responsible for designing a hybrid identity solution for medium or large organizations.</span></span>

## <a name="how-can-this-guide-help-you"></a><span data-ttu-id="70b6f-119">En quoi ce guide peut-il vous aider ?</span><span class="sxs-lookup"><span data-stu-id="70b6f-119">How can this guide help you?</span></span>
<span data-ttu-id="70b6f-120">Vous pouvez utiliser ce guide pour apprendre à concevoir une solution d'identité hybride en mesure d'intégrer un système cloud de gestion des identités avec votre solution d'identité locale actuelle.</span><span class="sxs-lookup"><span data-stu-id="70b6f-120">You can use this guide to understand how to design a hybrid identity solution that is able to integrate a cloud based identity management system with your current on-premises identity solution.</span></span> 

<span data-ttu-id="70b6f-121">Le schéma suivant illustre un exemple de solution d'identité hybride permettant aux administrateurs informatiques d'intégrer leur solution actuelle Windows Server Active Directory, locale, avec Microsoft Azure Active Directory pour permettre aux utilisateurs d'utiliser l'authentification unique sur l'ensemble des applications cloud et locales.</span><span class="sxs-lookup"><span data-stu-id="70b6f-121">The following graphic shows an example a hybrid identity solution that enables IT Admins to manage to integrate their current Windows Server Active Directory solution located on-premises with Microsoft Azure Active Directory to enable users to use Single Sign-On (SSO) across applications located in the cloud and on-premises.</span></span>

![](./media/hybrid-id-design-considerations/hybridID-example.png)

<span data-ttu-id="70b6f-122">L'illustration ci-dessus est un exemple de solution d'identité hybride qui exploite les services cloud et les intègre aux fonctionnalités locales afin de garantir une expérience unique pour le processus d'authentification de l'utilisateur final et de faciliter la gestion de ces ressources par le service informatique.</span><span class="sxs-lookup"><span data-stu-id="70b6f-122">The above illustration is an example of a hybrid identity solution that is leveraging cloud services to integrate with on-premises capabilities in order to provide a single experience to the end user authentication process and to facilitate IT managing those resources.</span></span> <span data-ttu-id="70b6f-123">Bien que ce scénario puisse être très courant, le modèle d'identité hybride de chaque entreprise est probablement différent de l'exemple illustré dans la Figure 1 en raison de la diversité des exigences.</span><span class="sxs-lookup"><span data-stu-id="70b6f-123">Although this can be a very common scenario, every organization’s hybrid identity design is likely to be different than the example illustrated in Figure 1 due to different requirements.</span></span> 

<span data-ttu-id="70b6f-124">Ce guide propose une série d'étapes et de tâches que vous pouvez suivre pour concevoir une solution d'identité hybride qui réponde aux exigences spécifiques de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="70b6f-124">This guide provides a series of steps and tasks that you can follow to design a hybrid identity solution that meets your organization’s unique requirements.</span></span> <span data-ttu-id="70b6f-125">Au fil des étapes et des tâches suivantes, le guide présente les technologies et les options appropriées à votre disposition pour satisfaire aux exigences de niveau de qualité fonctionnelle et de qualité de service de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="70b6f-125">Throughout the following steps and tasks, the guide presents the relevant technologies and feature options available to you to meet functional and service quality level requirements for your organization.</span></span>

<span data-ttu-id="70b6f-126">**Hypothèses**: vous avez un peu d'expérience avec Windows Server, les services de domaine Active Directory et Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="70b6f-126">**Assumptions**: You have some experience with Windows Server, Active Directory Domain Services and Azure Active Directory.</span></span> <span data-ttu-id="70b6f-127">Dans ce document, nous supposons que vous cherchez à savoir en quoi ces solutions peuvent répondre aux besoins de votre entreprise de façon autonome ou dans une solution intégrée.</span><span class="sxs-lookup"><span data-stu-id="70b6f-127">In this document, we assume you are looking for how these solutions can meet your business needs on their own or in an integrated solution.</span></span>

## <a name="design-considerations-overview"></a><span data-ttu-id="70b6f-128">Présentation des considérations relatives à la conception</span><span class="sxs-lookup"><span data-stu-id="70b6f-128">Design considerations overview</span></span>
<span data-ttu-id="70b6f-129">Ce document propose un ensemble d'étapes et de tâches que vous pouvez suivre pour concevoir la solution d'identité hybride idéale en fonction de vos exigences.</span><span class="sxs-lookup"><span data-stu-id="70b6f-129">This document provides a set of steps and tasks that you can follow to design a hybrid identity solution that best meets your requirements.</span></span> <span data-ttu-id="70b6f-130">Les étapes sont présentées dans un ordre précis.</span><span class="sxs-lookup"><span data-stu-id="70b6f-130">The steps are presented in an ordered sequence.</span></span> <span data-ttu-id="70b6f-131">Cependant, les considérations relatives à la conception que vous découvrirez dans les étapes suivantes pourront vous amener à revenir sur les décisions que vous aurez prises dans les étapes précédentes, en raison de conflits sur les choix de conception.</span><span class="sxs-lookup"><span data-stu-id="70b6f-131">Design considerations you learn in later steps may require you to change decisions you made in earlier steps, however, due to conflicting design choices.</span></span> <span data-ttu-id="70b6f-132">Tout est mis en œuvre pour vous avertir des risques de conflits de conception tout au long du document.</span><span class="sxs-lookup"><span data-stu-id="70b6f-132">Every attempt is made to alert you to potential design conflicts throughout the document.</span></span> 

<span data-ttu-id="70b6f-133">Vous n'atteindrez la conception idéale en fonction de vos exigences qu'après avoir répété les étapes autant de fois que nécessaire pour intégrer toutes les considérations présentes dans le document.</span><span class="sxs-lookup"><span data-stu-id="70b6f-133">You will arrive at the design that best meets your requirements only after iterating through the steps as many times as necessary to incorporate all of the considerations within the document.</span></span> 

| <span data-ttu-id="70b6f-134">Phase d'identité hybride</span><span class="sxs-lookup"><span data-stu-id="70b6f-134">Hybrid Identity Phase</span></span> | <span data-ttu-id="70b6f-135">Liste des rubriques</span><span class="sxs-lookup"><span data-stu-id="70b6f-135">Topic List</span></span> |
| --- | --- |
| <span data-ttu-id="70b6f-136">Déterminer les exigences en matière d'identité</span><span class="sxs-lookup"><span data-stu-id="70b6f-136">Determine identity requirements</span></span> |[<span data-ttu-id="70b6f-137">Déterminer les besoins métier</span><span class="sxs-lookup"><span data-stu-id="70b6f-137">Determine business needs</span></span>](active-directory-hybrid-identity-design-considerations-business-needs.md)<br> [<span data-ttu-id="70b6f-138">Déterminer les exigences de synchronisation de répertoire</span><span class="sxs-lookup"><span data-stu-id="70b6f-138">Determine directory synchronization requirements</span></span>](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)<br> [<span data-ttu-id="70b6f-139">Déterminer les exigences d’authentification multifacteur</span><span class="sxs-lookup"><span data-stu-id="70b6f-139">Determine multi-factor authentication requirements</span></span>](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)<br> [<span data-ttu-id="70b6f-140">Définir une stratégie d'adoption des identités hybrides</span><span class="sxs-lookup"><span data-stu-id="70b6f-140">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md) |
| <span data-ttu-id="70b6f-141">Planifier l'amélioration de la sécurité des données grâce à une solution d'identité solide</span><span class="sxs-lookup"><span data-stu-id="70b6f-141">Plan for enhancing data security through strong identity solution</span></span> |[<span data-ttu-id="70b6f-142">Déterminer les exigences de protection des données</span><span class="sxs-lookup"><span data-stu-id="70b6f-142">Determine data protection requirements</span></span>](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md) <br> [<span data-ttu-id="70b6f-143">Déterminer les exigences de gestion de contenu</span><span class="sxs-lookup"><span data-stu-id="70b6f-143">Determine content management requirements</span></span>](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)<br> [<span data-ttu-id="70b6f-144">Déterminer les exigences de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="70b6f-144">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)<br> [<span data-ttu-id="70b6f-145">Déterminer les exigences de réponse aux incidents</span><span class="sxs-lookup"><span data-stu-id="70b6f-145">Determine incident response requirements</span></span>](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) <br> [<span data-ttu-id="70b6f-146">Définir les options de protection des données</span><span class="sxs-lookup"><span data-stu-id="70b6f-146">Define data protection strategy</span></span>](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) |
| <span data-ttu-id="70b6f-147">Planifier le cycle de vie des identités hybrides</span><span class="sxs-lookup"><span data-stu-id="70b6f-147">Plan for hybrid identity lifecycle</span></span> |[<span data-ttu-id="70b6f-148">Déterminer les tâches de gestion des identités hybrides</span><span class="sxs-lookup"><span data-stu-id="70b6f-148">Determine hybrid identity management tasks</span></span>](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) <br> [<span data-ttu-id="70b6f-149">Gestion de la synchronisation</span><span class="sxs-lookup"><span data-stu-id="70b6f-149">Synchronization Management</span></span>](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)<br> [<span data-ttu-id="70b6f-150">Déterminer la stratégie d’adoption de la gestion des identités hybrides</span><span class="sxs-lookup"><span data-stu-id="70b6f-150">Determine hybrid identity management adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md) |

## <a name="download-this-guide"></a><span data-ttu-id="70b6f-151">Télécharger ce guide</span><span class="sxs-lookup"><span data-stu-id="70b6f-151">Download this guide</span></span>
<span data-ttu-id="70b6f-152">Vous pouvez télécharger une version pdf du guide sur les considérations pour la conception d'une identité hybride à partir de la [galerie Technet](https://gallery.technet.microsoft.com/Azure-Hybrid-Identity-b06c8288).</span><span class="sxs-lookup"><span data-stu-id="70b6f-152">You can download a pdf version of the Hybrid Identity Design Considerations guide from the [Technet gallery](https://gallery.technet.microsoft.com/Azure-Hybrid-Identity-b06c8288).</span></span> 
