---
title: "aaaWhat est la pile de Azure ? | Microsoft Docs"
description: "Le Kit de développement Azure Stack est un environnement qui permet d’évaluer les scénarios et fonctionnalités d’Azure Stack."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d9e6aee1-4cba-4df5-b5a3-6f38da9627a3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: helaw
ms.custom: mvc
ms.openlocfilehash: 3f7c84f2302a6411f49a07de171501fbd72812e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-stack"></a><span data-ttu-id="b6026-104">Qu’est-ce qu’Azure Stack ?</span><span class="sxs-lookup"><span data-stu-id="b6026-104">What is Azure Stack?</span></span>

<span data-ttu-id="b6026-105">Microsoft Azure Stack est une plateforme cloud hybride permettant de créer des services Azure à partir du centre de données de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="b6026-105">Microsoft Azure Stack is a hybrid cloud platform that lets you deliver Azure services from your organization’s datacenter.</span></span>  <span data-ttu-id="b6026-106">Pile Azure est conçue toohelp dans des scénarios clés, telles que des exigences de sécurité et conformité, ou lorsque vous devez tooaccess des ressources Azure sans connectivité internet.</span><span class="sxs-lookup"><span data-stu-id="b6026-106">Azure Stack is designed toohelp you in key scenarios, like meeting security and compliance requirements, or where you need tooaccess Azure resources without internet connectivity.</span></span>  

## <a name="azure-stack-development-kit"></a><span data-ttu-id="b6026-107">Kit de développement Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b6026-107">Azure Stack Development Kit</span></span>
<span data-ttu-id="b6026-108">Kit de développement Microsoft Azure pile est une version à un seul nœud de pile Azure, que vous pouvez utiliser tooevaluate et en savoir plus sur la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="b6026-108">Microsoft Azure Stack Development Kit is a single-node version of Azure Stack, which you can use tooevaluate and learn about Azure Stack.</span></span>  <span data-ttu-id="b6026-109">Vous pouvez également utiliser le Kit de développement Azure Stack comme environnement de développement, où vous pouvez développer à l’aide d’API et d’outils cohérents.</span><span class="sxs-lookup"><span data-stu-id="b6026-109">You can also use Azure Stack Development Kit as a developer environment, where you can develop using consistent APIs and tooling.</span></span>  

<span data-ttu-id="b6026-110">Notez les points suivants concernant le Kit de développement Azure Stack :</span><span class="sxs-lookup"><span data-stu-id="b6026-110">You should be aware of these points with Azure Stack Development Kit:</span></span>

* <span data-ttu-id="b6026-111">Vous ne devez pas utiliser le Kit de développement Azure Stack comme un environnement de production, mais uniquement à des fins de test, d’évaluation et de démonstration.</span><span class="sxs-lookup"><span data-stu-id="b6026-111">Azure Stack Development Kit must not be used as a production environment and should only be used for testing, evaluation, and demonstration.</span></span>  
* <span data-ttu-id="b6026-112">Votre déploiement d’Azure Stack est associé à un seul fournisseur d’identité Azure Active Directory ou AD FS (Active Directory Federation Services).</span><span class="sxs-lookup"><span data-stu-id="b6026-112">Your deployment of Azure Stack is associated with a single Azure Active Directory or Active Directory Federation Services identity provider.</span></span> <span data-ttu-id="b6026-113">Vous pouvez créer plusieurs utilisateurs dans ce répertoire et affecter les abonnements tooeach utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b6026-113">You can create multiple users in this directory and assign subscriptions tooeach user.</span></span>
* <span data-ttu-id="b6026-114">Avec tous les composants sont déployés sur un seul ordinateur de hello, limité de ressources physiques sont disponibles pour les ressources du client.</span><span class="sxs-lookup"><span data-stu-id="b6026-114">With all components deployed on hello single machine, there are limited physical resources available for tenant resources.</span></span> <span data-ttu-id="b6026-115">Cette configuration n’est pas destinée à l’évaluation des performances ou de la mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="b6026-115">This configuration is not intended for scale or performance evaluation.</span></span>
* <span data-ttu-id="b6026-116">Scénarios de mise en réseau sont limités en raison de l’exigence de carte réseau/hôte unique toohello.</span><span class="sxs-lookup"><span data-stu-id="b6026-116">Networking scenarios are limited due toohello single host/NIC requirement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6026-117">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b6026-117">Next steps</span></span>
[<span data-ttu-id="b6026-118">Principaux concepts et fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="b6026-118">Key features and concepts</span></span>](azure-stack-key-features.md)

[<span data-ttu-id="b6026-119">Hybrid Application innovation with Azure and Azure Stack (pdf) (Innovation d’application hybride avec Azure et Azure Stack (pdf)</span><span class="sxs-lookup"><span data-stu-id="b6026-119">Hybrid Application innovation with Azure and Azure Stack (pdf)</span></span>](https://go.microsoft.com/fwlink/?LinkId=842846&clcid=0x409)

