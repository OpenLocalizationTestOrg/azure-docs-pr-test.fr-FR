---
title: "les abonnements aaaNo a détecté l’erreur lorsque essayez toosign dans tooAzure portal ou centre des comptes Azure | Documents Microsoft"
description: "Fournit des solutions de hello pour un problème dans lequel les abonnements non trouvent une erreur se produit lorsque vous connecter tooAzure portail ou le centre de gestion Azure."
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: d1545298-99db-4941-8e97-f24a06bb7cb6
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: genli
ms.openlocfilehash: def4d4a1f883dd948fe8132f2d85abc4c23ae624
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="no-subscriptions-found-error-in-azure-portal-or-azure-account-center"></a><span data-ttu-id="22098-103">Erreur Aucun abonnement trouvé dans le portail Azure ou le centre des comptes Azure</span><span class="sxs-lookup"><span data-stu-id="22098-103">No subscriptions found error in Azure portal or Azure account center</span></span>
<span data-ttu-id="22098-104">Vous pouvez recevoir un message d’erreur « Aucun abonnement trouvé » lorsque vous essayez de toosign dans toohello [portail Azure](https://portal.azure.com/) ou hello [centre des comptes Azure](https://account.windowsazure.com/Subscriptions).</span><span class="sxs-lookup"><span data-stu-id="22098-104">You might receive a "No subscriptions found" error message when you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions).</span></span> <span data-ttu-id="22098-105">Cet article fournit une solution à ce problème.</span><span class="sxs-lookup"><span data-stu-id="22098-105">This article provides a solution for this problem.</span></span>

## <a name="symptom"></a><span data-ttu-id="22098-106">Symptôme</span><span class="sxs-lookup"><span data-stu-id="22098-106">Symptom</span></span>

<span data-ttu-id="22098-107">Lorsque vous essayez de toosign dans toohello [portail Azure](https://portal.azure.com/) ou hello [centre des comptes Azure](https://account.windowsazure.com/Subscriptions), vous recevez hello message d’erreur suivant : « Aucun abonnement trouvé ».</span><span class="sxs-lookup"><span data-stu-id="22098-107">When you try toosign in toohello [Azure portal](https://portal.azure.com/) or hello [Azure account center](https://account.windowsazure.com/Subscriptions), you receive hello following error message: "No subscriptions found".</span></span>

## <a name="cause"></a><span data-ttu-id="22098-108">Cause :</span><span class="sxs-lookup"><span data-stu-id="22098-108">Cause</span></span>

<span data-ttu-id="22098-109">Ce problème se produit si votre compte ne dispose pas des autorisations suffisantes.</span><span class="sxs-lookup"><span data-stu-id="22098-109">This problem occurs if your account doesn’t have sufficient permissions.</span></span> 

## <a name="solution"></a><span data-ttu-id="22098-110">Solution</span><span class="sxs-lookup"><span data-stu-id="22098-110">Solution</span></span>

<span data-ttu-id="22098-111">Assurez-vous que vous vous connecter en tant qu’administrateur correct de hello.</span><span class="sxs-lookup"><span data-stu-id="22098-111">Make sure that you log in as hello correct administrator.</span></span> <span data-ttu-id="22098-112">Un administrateur de compte peut accéder au centre des comptes hello uniquement.</span><span class="sxs-lookup"><span data-stu-id="22098-112">An Account Administrator can access only hello Account Center.</span></span> <span data-ttu-id="22098-113">Les administrateurs de service (SA) et Coadministrateurs (CA) ont accès autorisation toohello uniquement portail Azure ou hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="22098-113">Service Administrators (SA) and Co-Administrators (CA) have access permission only toohello Azure portal or hello Azure classic portal.</span></span>

### <a name="scenario-1-error-message-is-received-in-hello-azure-portalhttpsportalazurecom"></a><span data-ttu-id="22098-114">Scénario 1 : Message d’erreur est reçu dans hello [portail Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="22098-114">Scenario 1: Error message is received in hello [Azure portal](https://portal.azure.com)</span></span>

<span data-ttu-id="22098-115">toofix ce problème :</span><span class="sxs-lookup"><span data-stu-id="22098-115">toofix this issue:</span></span>

* <span data-ttu-id="22098-116">Vérifiez que hello correct de répertoire Azure est sélectionné en cliquant sur votre compte en haut de hello à droite.</span><span class="sxs-lookup"><span data-stu-id="22098-116">Make sure that hello correct Azure directory is selected by clicking your account at hello top right.</span></span>

  ![Répertoire hello sélectionnez hello haut à droite de hello portail Azure](./media/billing-no-subscriptions-found/directory-switch.png)

* <span data-ttu-id="22098-118">Si hello droite Azure directory est activée mais toujours le message hello, [votre compte a été ajouté en tant que propriétaire](billing-add-change-azure-subscription-administrator.md).</span><span class="sxs-lookup"><span data-stu-id="22098-118">If hello right Azure directory is selected but you still receive hello error message, [have your account added as an Owner](billing-add-change-azure-subscription-administrator.md).</span></span>

### <a name="scenario-2-error-message-is-received-in-hello-azure-account-centerhttpsaccountwindowsazurecomsubscriptions"></a><span data-ttu-id="22098-119">Scénario 2 : Message d’erreur est reçu dans hello [centre des comptes Azure](https://account.windowsazure.com/Subscriptions)</span><span class="sxs-lookup"><span data-stu-id="22098-119">Scenario 2: Error message is received in hello [Azure account center](https://account.windowsazure.com/Subscriptions)</span></span>

<span data-ttu-id="22098-120">Vérifiez si le compte hello que vous avez utilisé est hello administrateur de compte.</span><span class="sxs-lookup"><span data-stu-id="22098-120">Check whether hello account that you used is hello Account Administrator.</span></span> <span data-ttu-id="22098-121">tooverify qui hello compte administrateur est, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="22098-121">tooverify who hello Account Administrator is, follow these steps:</span></span>

1. <span data-ttu-id="22098-122">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="22098-122">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="22098-123">Dans le menu du Hub hello, sélectionnez **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="22098-123">On hello Hub menu, select **Subscription**.</span></span>
3. <span data-ttu-id="22098-124">Sélectionnez hello abonnement que vous souhaitez toocheck, puis sélectionnez **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="22098-124">Select hello subscription that you want toocheck, and then select **Settings**.</span></span>
4. <span data-ttu-id="22098-125">Sélectionner **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="22098-125">Select **Properties**.</span></span> <span data-ttu-id="22098-126">administrateur du compte d’abonnement de hello Hello s’affiche dans hello **Admin. compte** boîte.</span><span class="sxs-lookup"><span data-stu-id="22098-126">hello account administrator of hello subscription is displayed in hello **Account Admin** box.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="22098-127">Vous avez besoin d’aide ?</span><span class="sxs-lookup"><span data-stu-id="22098-127">Need help?</span></span> <span data-ttu-id="22098-128">Contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="22098-128">Contact support.</span></span>
<span data-ttu-id="22098-129">Si vous avez besoin d’aide, [contactez le support technique](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget votre problème résolu rapidement.</span><span class="sxs-lookup"><span data-stu-id="22098-129">If you still need help, [contact support](http://go.microsoft.com/fwlink/?linkid=544831&clcid=0x409) tooget your issue resolved quickly.</span></span> 
