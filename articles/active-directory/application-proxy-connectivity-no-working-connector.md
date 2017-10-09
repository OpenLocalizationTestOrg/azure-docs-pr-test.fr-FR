---
title: "groupe de connecteurs aaaNo travail trouvé pour une application de Proxy d’Application | Documents Microsoft"
description: "Résoudre les problèmes que vous pouvez rencontrer quand il n’existe aucun travail connecteur dans un groupe de connecteurs pour votre application avec hello Proxy d’Application Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4c4baf296b316db131929c9a7c618fb9960713e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="no-working-connector-group-found-for-an-application-proxy-application"></a><span data-ttu-id="179b8-103">Aucun groupe de connecteurs en fonctionnement n’est disponible pour une application de proxy d’application</span><span class="sxs-lookup"><span data-stu-id="179b8-103">No working connector group found for an Application Proxy application</span></span>

<span data-ttu-id="179b8-104">Cet article vous vous tooresolve hello problèmes rencontrés quand il n’est pas un connecteur détecté pour une application de Proxy d’Application intégré à Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="179b8-104">This article help you tooresolve hello common issues faced when there is not a connector detected for an Application Proxy application integrated with Azure Active Directory.</span></span>

## <a name="overview-of-steps"></a><span data-ttu-id="179b8-105">Vue d’ensemble des étapes</span><span class="sxs-lookup"><span data-stu-id="179b8-105">Overview of steps</span></span>
<span data-ttu-id="179b8-106">S’il n’existe aucun travail connecteur dans un groupe de connecteurs pour votre application, il existe quelques problème de hello tooresolve façons :</span><span class="sxs-lookup"><span data-stu-id="179b8-106">If there is no working Connector in a Connector Group for your application, there are a few ways tooresolve hello problem:</span></span>

-   <span data-ttu-id="179b8-107">Si vous n’avez aucun connecteur de groupe de hello, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="179b8-107">If you have no connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="179b8-108">Télécharger un nouveau connecteur sur serveur local à droite de hello et lui attribuer le groupe de toothis</span><span class="sxs-lookup"><span data-stu-id="179b8-108">Download a new Connector on hello right on-prem server, and assign it toothis group</span></span>

    -   <span data-ttu-id="179b8-109">Déplacez un connecteur actif dans hello</span><span class="sxs-lookup"><span data-stu-id="179b8-109">Move an active Connector into hello group</span></span>

-   <span data-ttu-id="179b8-110">Si vous n’avez aucun connecteur active dans le groupe de hello, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="179b8-110">If you have no active connectors in hello group, you can:</span></span>

    -   <span data-ttu-id="179b8-111">Identifier la raison hello que votre connecteur est inactif et résoudre</span><span class="sxs-lookup"><span data-stu-id="179b8-111">Identify hello reason your Connector is inactive and resolve</span></span>

    -   <span data-ttu-id="179b8-112">Déplacez un connecteur actif dans hello</span><span class="sxs-lookup"><span data-stu-id="179b8-112">Move an active Connector into hello group</span></span>

<span data-ttu-id="179b8-113">tooknow suivantes, laquelle est problème de hello, ouvrir le menu de « Proxy d’Application » hello dans votre Application et examinez le message d’avertissement hello groupe de connecteurs.</span><span class="sxs-lookup"><span data-stu-id="179b8-113">tooknow which of these is hello issue, open hello “Application Proxy” menu in your Application, and look at hello Connector Group warning message.</span></span> <span data-ttu-id="179b8-114">Il spécifier soit hello a besoin au moins un connecteur (vous avez aucun groupe de hello) ou qu’il ne dispose d’aucun connecteur active (même si vous avez probablement connecteurs inactifs).</span><span class="sxs-lookup"><span data-stu-id="179b8-114">It specify either that hello group needs at least one Connector (you have none in hello group) or that it has no active Connectors (though you likely have inactive Connectors).</span></span>

   ![Sélection du groupe de connecteurs dans le portail Azure](./media/application-proxy-connectivity-no-working-connector/no-active-connector.png)

<span data-ttu-id="179b8-116">Pour plus d’informations sur chacune de ces options, consultez la section correspondante de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="179b8-116">For details on each of these options, see hello corresponding section below.</span></span> <span data-ttu-id="179b8-117">Chacun de ces part du principe que vous démarrez à partir de la page de gestion du connecteur hello.</span><span class="sxs-lookup"><span data-stu-id="179b8-117">Each of these assumes that you are starting from hello Connector management page.</span></span> <span data-ttu-id="179b8-118">Si vous examinez le message d’erreur hello ci-dessus, vous pouvez accéder toothis page en cliquant sur le message d’avertissement hello.</span><span class="sxs-lookup"><span data-stu-id="179b8-118">If you are looking at hello error message above, you can go toothis page by clicking on hello warning message.</span></span> <span data-ttu-id="179b8-119">Sinon, ce sont accessibles en accédant trop**Azure Active Directory**, en cliquant sur **des Applications d’entreprise**, puis **le Proxy d’Application.**</span><span class="sxs-lookup"><span data-stu-id="179b8-119">Otherwise this can be found by going too**Azure Active Directory**, clicking on **Enterprise Applications**, then **Application Proxy.**</span></span>

   ![Gestion du groupe de connecteurs dans le portail Azure](./media/application-proxy-connectivity-no-working-connector/app-proxy.png)

## <a name="download-a-new-connector"></a><span data-ttu-id="179b8-121">Télécharger un nouveau connecteur</span><span class="sxs-lookup"><span data-stu-id="179b8-121">Download a new Connector</span></span>

<span data-ttu-id="179b8-122">toodownload un nouveau connecteur, utiliser le bouton de « Télécharger le connecteur » hello en hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="179b8-122">toodownload a new Connector, use hello “Download Connector” button at hello top of hello page.</span></span>

<span data-ttu-id="179b8-123">besoins de connecteur hello Remarque toobe installé sur un ordinateur avec l’application de ligne de vue directe toohello principale et est généralement placé sur hello même serveur que l’application hello.</span><span class="sxs-lookup"><span data-stu-id="179b8-123">note hello Connector needs toobe installed on a machine with direct line of sight toohello backend application, and is typically placed on hello same server as hello application.</span></span> <span data-ttu-id="179b8-124">Après avoir téléchargé, hello connecteur doit apparaître dans ce menu.</span><span class="sxs-lookup"><span data-stu-id="179b8-124">After downloading, hello Connector should appear in this menu.</span></span> <span data-ttu-id="179b8-125">Cliquez sur le connecteur de hello et utilisez hello « Groupe de connecteurs » liste déroulante toomake qu’il appartient toohello des groupes appropriés.</span><span class="sxs-lookup"><span data-stu-id="179b8-125">click hello Connector, and use hello “Connector Group” drop-down toomake sure it belongs toohello right group.</span></span> <span data-ttu-id="179b8-126">Enregistrez les modifications hello.</span><span class="sxs-lookup"><span data-stu-id="179b8-126">Save hello change.</span></span>

   ![Téléchargez le connecteur de hello de hello portail Azure](./media/application-proxy-connectivity-no-working-connector/download-connector.png)
   
## <a name="move-an-active-connector"></a><span data-ttu-id="179b8-128">Déplacer un connecteur</span><span class="sxs-lookup"><span data-stu-id="179b8-128">Move an Active Connector</span></span>

<span data-ttu-id="179b8-129">Si vous avez un connecteur actif qui doit appartenir toohello groupe et qui possède l’application de ligne de vue toohello cible principale, vous pouvez déplacer hello connecteur dans le groupe de hello attribué.</span><span class="sxs-lookup"><span data-stu-id="179b8-129">If you have an active Connector that should belong toohello group and has line of sight toohello target backend application, you can move hello Connector into hello assigned group.</span></span> <span data-ttu-id="179b8-130">toodo, cliquez sur hello connecteur.</span><span class="sxs-lookup"><span data-stu-id="179b8-130">toodo so, click hello Connector.</span></span> <span data-ttu-id="179b8-131">Dans le champ de « Groupe de connecteurs » hello, utilisez groupe approprié du hello hello tooselect de liste déroulante, cliquez sur Enregistrer.</span><span class="sxs-lookup"><span data-stu-id="179b8-131">In hello “Connector Group” field, use hello drop-down tooselect hello correct group, and click Save.</span></span>

## <a name="resolve-an-inactive-connector"></a><span data-ttu-id="179b8-132">Résoudre le problème d’un connecteur inactif</span><span class="sxs-lookup"><span data-stu-id="179b8-132">Resolve an inactive Connector</span></span>

<span data-ttu-id="179b8-133">Si hello uniquement connecteurs dans le groupe de hello sont inactives, ils sont susceptibles de sur un ordinateur qui n’effectue pas aient tous les ports nécessaires hello est débloqué.</span><span class="sxs-lookup"><span data-stu-id="179b8-133">If hello only Connectors in hello group are inactive, they are likely on a machine that does not have all hello necessary ports unblocked.</span></span>

<span data-ttu-id="179b8-134">consultez les ports hello document de résolution des problèmes pour plus d’informations sur l’examen de ce problème.</span><span class="sxs-lookup"><span data-stu-id="179b8-134">see hello ports Troubleshoot document for details on investigating this problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="179b8-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="179b8-135">Next steps</span></span>
[<span data-ttu-id="179b8-136">Présentation des connecteurs de proxy d’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="179b8-136">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)


