---
title: "aaaGet démarré Azure MFA dans le cloud de hello | Documents Microsoft"
description: "Il s’agit de page d’authentification Microsoft Azure multi-Factor hello qui décrit comment tooget main d’Azure MFA dans hello cloud."
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
ms.openlocfilehash: a4aaf44bf08d96f2baad155072fdd6e0e727ce8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-in-hello-cloud"></a><span data-ttu-id="00a5e-103">Prise en main d’Azure multi-Factor Authentication dans le cloud de hello</span><span class="sxs-lookup"><span data-stu-id="00a5e-103">Getting started with Azure Multi-Factor Authentication in hello cloud</span></span>
<span data-ttu-id="00a5e-104">Cet article explique les comment tooget démarrer à l’aide de l’authentification multifacteur Azure dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="00a5e-104">This article walks through how tooget started using Azure Multi-Factor Authentication in hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="00a5e-105">Hello documentation suivante fournit des informations sur la façon dont les utilisateurs tooenable à l’aide de hello **portail classique Azure**.</span><span class="sxs-lookup"><span data-stu-id="00a5e-105">hello following documentation provides information on how tooenable users using hello **Azure Classic Portal**.</span></span> <span data-ttu-id="00a5e-106">Si vous recherchez des informations sur la façon de tooset d’Azure multi-Factor Authentication pour les utilisateurs d’Office 365, consultez [configurer l’authentification multifacteur pour Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span><span class="sxs-lookup"><span data-stu-id="00a5e-106">If you are looking for information on how tooset up Azure Multi-Factor Authentication for O365 users, see [Set up multi-factor authentication for Office 365.](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6?ui=en-US&rs=en-US&ad=US)</span></span>

![Authentification Multifacteur dans hello Cloud](./media/multi-factor-authentication-get-started-cloud/mfa_in_cloud.png)

## <a name="prerequisite"></a><span data-ttu-id="00a5e-108">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="00a5e-108">Prerequisite</span></span>
<span data-ttu-id="00a5e-109">[Souscrire un abonnement Azure](https://azure.microsoft.com/pricing/free-trial/) -si vous n’avez pas déjà un abonnement Azure, vous devez toosign à distance pour un.</span><span class="sxs-lookup"><span data-stu-id="00a5e-109">[Sign up for an Azure subscription](https://azure.microsoft.com/pricing/free-trial/) - If you do not already have an Azure subscription, you need toosign-up for one.</span></span> <span data-ttu-id="00a5e-110">Si vous êtes nouveau et que vous utilisez Azure MFA, vous pouvez utiliser un abonnement d’évaluation.</span><span class="sxs-lookup"><span data-stu-id="00a5e-110">If you are just starting out and using Azure MFA you can use a trial subscription</span></span>

## <a name="enable-azure-multi-factor-authentication"></a><span data-ttu-id="00a5e-111">Activation d’Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="00a5e-111">Enable Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="00a5e-112">Tant que vos utilisateurs ont des licences qui incluent l’authentification multifacteur Azure, aucune est que vous avez besoin de tooturn toodo sur Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="00a5e-112">As long as your users have licenses that include Azure Multi-Factor Authentication, there's nothing that you need toodo tooturn on Azure MFA.</span></span> <span data-ttu-id="00a5e-113">Vous pouvez commencer par demander une vérification en deux étapes pour les différents utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="00a5e-113">You can start requiring two-step verification on an individual user basis.</span></span> <span data-ttu-id="00a5e-114">licences Hello qui permettent l’authentification Multifacteur Azure sont :</span><span class="sxs-lookup"><span data-stu-id="00a5e-114">hello licenses that enable Azure MFA are:</span></span>
- <span data-ttu-id="00a5e-115">Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="00a5e-115">Azure Multi-Factor Authentication</span></span>
- <span data-ttu-id="00a5e-116">Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="00a5e-116">Azure Active Directory Premium</span></span>
- <span data-ttu-id="00a5e-117">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="00a5e-117">Enterprise Mobility + Security</span></span>

<span data-ttu-id="00a5e-118">Si vous n’avez pas un de ces trois licences, ou vous n’avez pas suffisamment toocover licences tous vos utilisateurs, que les OK trop.</span><span class="sxs-lookup"><span data-stu-id="00a5e-118">If you don't have one of these three licenses, or you don't have enough licenses toocover all of your users, that's ok too.</span></span> <span data-ttu-id="00a5e-119">Vous n’avez toodo une étape supplémentaire et [créer un fournisseur d’authentification multifacteur](multi-factor-authentication-get-started-auth-provider.md) dans votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="00a5e-119">You just have toodo an extra step and [Create a Multi-Factor Auth Provider](multi-factor-authentication-get-started-auth-provider.md) in your directory.</span></span>

## <a name="turn-on-two-step-verification-for-users"></a><span data-ttu-id="00a5e-120">Activer la vérification en deux étapes pour les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="00a5e-120">Turn on two-step verification for users</span></span>

<span data-ttu-id="00a5e-121">Utilisez une des procédures hello répertoriés dans [la vérification en deux étapes de toorequire pour un utilisateur ou groupe](multi-factor-authentication-get-started-user-states.md) toostart à l’aide de l’authentification Multifacteur Azure.</span><span class="sxs-lookup"><span data-stu-id="00a5e-121">Use one of hello procedures listed in [How toorequire two-step verification for a user or group](multi-factor-authentication-get-started-user-states.md) toostart using Azure MFA.</span></span> <span data-ttu-id="00a5e-122">Vous pouvez choisir la vérification en deux étapes de tooenforce pour toutes les connexions, ou vous pouvez créer la vérification en deux étapes de l’accès conditionnel stratégies toorequire uniquement quand elle est tooyou.</span><span class="sxs-lookup"><span data-stu-id="00a5e-122">You can choose tooenforce two-step verification for all sign-ins, or you can create conditional access policies toorequire two-step verification only when it matters tooyou.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00a5e-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="00a5e-123">Next Steps</span></span>
<span data-ttu-id="00a5e-124">Maintenant que vous avez configuré l’authentification multifacteur Azure dans le cloud de hello, vous pouvez configurer et configurer votre déploiement.</span><span class="sxs-lookup"><span data-stu-id="00a5e-124">Now that you have set up Azure Multi-Factor Authentication in hello cloud, you can configure and set up your deployment.</span></span> <span data-ttu-id="00a5e-125">Pour plus d’informations, consultez [Configuration d’Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md).</span><span class="sxs-lookup"><span data-stu-id="00a5e-125">See [Configuring Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md) for more details.</span></span>

