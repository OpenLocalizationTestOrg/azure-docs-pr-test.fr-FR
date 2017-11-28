---
title: "Prise en main d’Azure MFA dans le cloud | Microsoft Docs"
description: "Cette page dédiée à Microsoft Azure Multi-Factor Authentication décrit la prise en main d’Azure MFA dans le cloud."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 6b2e6549-1a26-4666-9c4a-cbe5d64c4e66
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/24/2017
ms.author: kgremban
ms.openlocfilehash: 19f3228b874fc4e37bf83388dae4341428226482
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-the-cloud"></a><span data-ttu-id="94cbf-103">Prise en main avec Azure Multi-Factor Authentication dans le cloud</span><span class="sxs-lookup"><span data-stu-id="94cbf-103">Getting started with Azure Multi-Factor Authentication in the cloud</span></span>
<span data-ttu-id="94cbf-104">Cet article vous explique comment utiliser Azure Multi-Factor Authentication dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="94cbf-104">This article walks through how to get started using Azure Multi-Factor Authentication in the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="94cbf-105">La documentation suivante fournit des informations relatives à l’activation des utilisateurs à l’aide du **portail Azure Classic**.</span><span class="sxs-lookup"><span data-stu-id="94cbf-105">The following documentation provides information on how to enable users using the **Azure Classic Portal**.</span></span> <span data-ttu-id="94cbf-106">Si vous recherchez des informations sur la configuration d’Azure Multi-Factor Authentication pour les utilisateurs O365, consultez l’article [Configurer l’authentification multifacteur pour les utilisateurs d’Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span><span class="sxs-lookup"><span data-stu-id="94cbf-106">If you are looking for information on how to set up Azure Multi-Factor Authentication for O365 users, see [Set up multi-factor authentication for Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span></span>

![MFA dans le cloud](./media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a><span data-ttu-id="94cbf-108">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="94cbf-108">Prerequisite</span></span>
<span data-ttu-id="94cbf-109">[Souscrivez un abonnement Azure](https://azure.microsoft.com/pricing/free-trial/) : si vous n’avez pas encore d’abonnement Azure, vous devez en souscrire un.</span><span class="sxs-lookup"><span data-stu-id="94cbf-109">[Sign up for an Azure subscription](https://azure.microsoft.com/pricing/free-trial/) - If you do not already have an Azure subscription, you need to sign-up for one.</span></span> <span data-ttu-id="94cbf-110">Si vous êtes nouveau et que vous utilisez Azure MFA, vous pouvez utiliser un abonnement d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="94cbf-110">If you are just starting out and using Azure MFA you can use a trial subscription</span></span>

## <a name="enable-azure-multi-factor-authentication"></a><span data-ttu-id="94cbf-111">Activation d’Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="94cbf-111">Enable Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="94cbf-112">Tant que vos utilisateurs disposent de licences comprenant Azure Multi-Factor Authentication, vous n’avez rien à faire pour activer Azure Multi-Factor Authentication (MFA).</span><span class="sxs-lookup"><span data-stu-id="94cbf-112">As long as your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need to do to turn on Azure MFA.</span></span> <span data-ttu-id="94cbf-113">Vous pouvez commencer par demander une vérification en deux étapes pour les différents utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="94cbf-113">You can start requiring two-step verification on an individual user basis.</span></span> <span data-ttu-id="94cbf-114">Les licences suivantes prennent en charge Azure MFA :</span><span class="sxs-lookup"><span data-stu-id="94cbf-114">The licenses that enable Azure MFA are:</span></span>
- <span data-ttu-id="94cbf-115">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="94cbf-115">Azure Multi-Factor Authentication</span></span>
- <span data-ttu-id="94cbf-116">Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="94cbf-116">Azure Active Directory Premium</span></span>
- <span data-ttu-id="94cbf-117">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="94cbf-117">Enterprise Mobility + Security</span></span>

<span data-ttu-id="94cbf-118">Si vous ne disposez pas de l’une de ces trois licences ou que vous n’avez pas suffisamment de licences pour tous vos utilisateurs, vous pourrez tout de même utiliser la fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="94cbf-118">If you don't have one of these three licenses, or you don't have enough licenses to cover all of your users, that's ok too.</span></span> <span data-ttu-id="94cbf-119">Pour cela, il vous faudra effectuer une étape supplémentaire et [créer un fournisseur Multi-Factor Authentication](multi-factor-authentication-get-started-auth-provider.md) dans votre répertoire.</span><span class="sxs-lookup"><span data-stu-id="94cbf-119">You just have to do an extra step and [Create a Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md) in your directory.</span></span>

## <a name="turn-on-two-step-verification-for-users"></a><span data-ttu-id="94cbf-120">Activer la vérification en deux étapes pour les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="94cbf-120">Turn on two-step verification for users</span></span>

<span data-ttu-id="94cbf-121">Utilisez l’une des procédures répertoriées dans [How to require two-step verification for a user or group](multi-factor-authentication-get-started-user-states.md) (Exiger la vérification en deux étapes pour un utilisateur ou groupe) pour commencer à utiliser Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="94cbf-121">Use one of the procedures listed in [How to require two-step verification for a user or group](multi-factor-authentication-get-started-user-states.md) to start using Azure MFA.</span></span> <span data-ttu-id="94cbf-122">Vous pouvez choisir d’appliquer la vérification en deux étapes pour toutes les connexions, ou de créer des règles d’accès conditionnel, ce qui permet d’exiger la vérification en deux étapes lorsque vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="94cbf-122">You can choose to enforce two-step verification for all sign-ins, or you can create conditional access policies to require two-step verification only when it matters to you.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94cbf-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="94cbf-123">Next Steps</span></span>
<span data-ttu-id="94cbf-124">Maintenant que vous avez configuré Azure Multi-Factor Authentication dans le cloud, vous pouvez configurer et installer votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="94cbf-124">Now that you have set up Azure Multi-Factor Authentication in the cloud, you can configure and set up your deployment.</span></span> <span data-ttu-id="94cbf-125">Pour plus d’informations, consultez [Configuration d’Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="94cbf-125">See [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) for more details.</span></span>

