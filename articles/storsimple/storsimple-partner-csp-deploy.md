---
title: "Vue d’ensemble du programme des fournisseurs de solutions cloud et de Microsoft Azure StorSimple | Microsoft Docs"
description: "Vue d’ensemble de StorSimple et du programme des fournisseurs de solutions cloud pour les partenaires StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/08/2017
ms.author: alkohli
ms.openlocfilehash: c8cb51093142146fc7d43b51a62d949f6cc38988
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="c3238-103">Déployer StorSimple Virtual Array pour le programme des fournisseurs de solutions cloud</span><span class="sxs-lookup"><span data-stu-id="c3238-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="c3238-104">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="c3238-104">Overview</span></span>

<span data-ttu-id="c3238-105">StorSimple Virtual Array peut être déployé par les partenaires Fournisseurs de solutions cloud (CSP) pour leurs clients.</span><span class="sxs-lookup"><span data-stu-id="c3238-105">StorSimple Virtual Array can be deployed by the Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="c3238-106">Un partenaire CSP peut créer un service StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="c3238-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="c3238-107">Ce service peut ensuite être utilisé pour déployer et gérer StorSimple Virtual Array et les partages, volumes et sauvegardes associés.</span><span class="sxs-lookup"><span data-stu-id="c3238-107">This service can then be used to deploy and manage StorSimple Virtual Array and the associated shares, volumes, and backups.</span></span>

<span data-ttu-id="c3238-108">Cet article décrit comment un partenaire CSP peut ajouter un client ou un nouvel abonnement à un client existant, puis créer un service pour déployer StorSimple Virtual Array dans CSP.</span><span class="sxs-lookup"><span data-stu-id="c3238-108">This article describes how a CSP partner can add a customer or a new subscription to an existing customer and then create a service to deploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3238-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c3238-109">Prerequisites</span></span>

<span data-ttu-id="c3238-110">Avant de commencer, assurez-vous de satisfaire les exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="c3238-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="c3238-111">Vous êtes inscrit dans le cadre du programme CSP.</span><span class="sxs-lookup"><span data-stu-id="c3238-111">You are enrolled under the CSP program.</span></span>
- <span data-ttu-id="c3238-112">Vous avez des informations d’identification valides pour [l’Espace Partenaires](http://partnercenter.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="c3238-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="c3238-113">Les informations d’identification vous permettent de vous connecter au portail Partenaire pour ajouter de nouveaux clients, rechercher des clients ou accéder à un compte client à partir du tableau de bord Partenaire.</span><span class="sxs-lookup"><span data-stu-id="c3238-113">The credentials enable you to sign in to the Partner portal to add new customers, search for customers, or navigate to a customer account from the Partner dashboard.</span></span> <span data-ttu-id="c3238-114">Le CSP peut fonctionner en tant qu’administrateur StorSimple au nom du client dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c3238-114">The CSP can function as a StorSimple administrator on behalf of the customer in the Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="c3238-115">Ajouter un client</span><span class="sxs-lookup"><span data-stu-id="c3238-115">Add a customer</span></span>

<span data-ttu-id="c3238-116">Si vous ajoutez un client, un abonnement est automatiquement créé.</span><span class="sxs-lookup"><span data-stu-id="c3238-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="c3238-117">Pour ajouter un client (et créer automatiquement un abonnement), effectuez les opérations suivantes dans le portail Partenaire.</span><span class="sxs-lookup"><span data-stu-id="c3238-117">To add a customer (and automatically create a subscription), perform the following steps in the Partner portal.</span></span>

1. <span data-ttu-id="c3238-118">Accédez à [l’Espace Partenaires](http://partnercenter.microsoft.com/) et connectez-vous en utilisant vos informations d’identification CSP.</span><span class="sxs-lookup"><span data-stu-id="c3238-118">Go to the [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="c3238-119">Cliquez sur **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="c3238-119">Click **Dashboard**.</span></span>

     ![Tableau de bord dans l’Espace Partenaires](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="c3238-121">Dans le panneau gauche, cliquez sur **Clients**.</span><span class="sxs-lookup"><span data-stu-id="c3238-121">In the left-pane, click **Customers**.</span></span> <span data-ttu-id="c3238-122">Dans le panneau droit, cliquez sur **Ajouter des clients**.</span><span class="sxs-lookup"><span data-stu-id="c3238-122">In the right-pane, click **Add customers**.</span></span> <span data-ttu-id="c3238-123">Entrez les détails du client.</span><span class="sxs-lookup"><span data-stu-id="c3238-123">Enter the details of the customer.</span></span> <span data-ttu-id="c3238-124">Cliquez sur **Suivant : Abonnements** pour créer un abonnement client.</span><span class="sxs-lookup"><span data-stu-id="c3238-124">Click **Next: Subscriptions** to create a customer subscription.</span></span>

    ![Ajouter un client](./media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="c3238-126">Sélectionnez l’offre **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="c3238-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="c3238-127">Faites défiler vers le bas de la page et cliquez sur **Révision**.</span><span class="sxs-lookup"><span data-stu-id="c3238-127">Scroll to the bottom of the page and click **Review**.</span></span>

    ![Revoir les informations d’abonnement](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="c3238-129">Révisez les informations et cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="c3238-129">Review the information and click **Submit**.</span></span>

    ![Envoyer l’abonnement](./media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="c3238-131">Enregistrez les informations de confirmation pour référence ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c3238-131">Save the confirmation information for future reference.</span></span>

    ![Enregistrer la confirmation](./media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="c3238-133">Recherchez le client que vous venez d’ajouter ou accédez à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="c3238-133">Find or navigate to the customer you just added.</span></span> <span data-ttu-id="c3238-134">Cliquez sur le **nom de la société** pour explorer les détails.</span><span class="sxs-lookup"><span data-stu-id="c3238-134">Click the **Company name** to drill down into the details.</span></span>

    ![Rechercher le client](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="c3238-136">Dans le panneau gauche, sélectionnez **Gestion des services**.</span><span class="sxs-lookup"><span data-stu-id="c3238-136">In the left-pane, select **Service management**.</span></span> <span data-ttu-id="c3238-137">Dans le panneau droit, sous **Administrer des services**, cliquez sur **Portail de gestion Microsoft Azure** pour vous connecter en tant qu’administrateur Azure pour votre client.</span><span class="sxs-lookup"><span data-stu-id="c3238-137">In the right-pane, under **Administer services**, click **Microsoft Azure Management Portal** to sign in as an Azure administrator for your customer.</span></span>

    ![Connexion au portail Azure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="c3238-139">Pour créer une instance StorSimple Device Manager, cliquez sur **+ Nouveau** et recherchez ou accédez à **Série d’appareils virtuels StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="c3238-139">To create a StorSimple Device Manager, click **+ New** and search for or navigate to **StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="c3238-140">Pour plus d’informations, accédez à la page [Déployer un service StorSimple Device Manager](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="c3238-140">For more information, go to [Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Créer un service StorSimple Device Manager](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="c3238-142">Ajouter un abonnement</span><span class="sxs-lookup"><span data-stu-id="c3238-142">Add a subscription</span></span>

<span data-ttu-id="c3238-143">Dans certains cas, vous avez peut-être un client existant et vous devez ajouter un abonnement.</span><span class="sxs-lookup"><span data-stu-id="c3238-143">In some instances, you may have an existing customer, and you need to add a subscription.</span></span> <span data-ttu-id="c3238-144">Pour ajouter un abonnement à un client existant, effectuez les opérations suivantes dans le portail Partenaire.</span><span class="sxs-lookup"><span data-stu-id="c3238-144">To add a subscription to an existing customer, perform the following steps in the Partner portal.</span></span>

1. <span data-ttu-id="c3238-145">Accédez à [l’Espace Partenaires](http://partnercenter.microsoft.com/) et connectez-vous en utilisant vos informations d’identification CSP.</span><span class="sxs-lookup"><span data-stu-id="c3238-145">Go to the [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="c3238-146">Cliquez sur **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="c3238-146">Click **Dashboard**.</span></span>

     ![Tableau de bord dans l’Espace Partenaires](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="c3238-148">Dans le panneau gauche, cliquez sur **Clients**.</span><span class="sxs-lookup"><span data-stu-id="c3238-148">In the left-pane, click **Customers**.</span></span> <span data-ttu-id="c3238-149">Recherchez le client auquel vous souhaitez ajouter un abonnement ou accédez à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="c3238-149">Find or navigate to the customer you want to add a subscription to.</span></span> <span data-ttu-id="c3238-150">Cliquez sur l’icône de ![développement de l’icône cochée](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) pour développer la ligne contenant le nom de la société de votre client.</span><span class="sxs-lookup"><span data-stu-id="c3238-150">Click the ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon to expand the row for the company name for your customer.</span></span> <span data-ttu-id="c3238-151">Dans les détails, cliquez sur **Ajouter des abonnements**.</span><span class="sxs-lookup"><span data-stu-id="c3238-151">In the details, click **Add subscriptions**.</span></span>

    ![Clients](./media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="c3238-153">Sélectionnez **Microsoft Azure** sous **Offres principales** dans l’abonnement et cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="c3238-153">Check **Microsoft Azure** for the **Top offers** in the subscription and click **Submit**.</span></span> <span data-ttu-id="c3238-154">Ceci crée un nouvel abonnement.</span><span class="sxs-lookup"><span data-stu-id="c3238-154">This creates a new subscription.</span></span>

    ![Ajouter un nouvel abonnement](./media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="c3238-156">Après la création d’un abonnement, cliquez sur **<-- Clients** dans le panneau gauche pour revenir à la page **Clients**.</span><span class="sxs-lookup"><span data-stu-id="c3238-156">After a new subscription is created, click **<-- Customers** in the left-pane to return to the **Customers** page.</span></span> <span data-ttu-id="c3238-157">Recherchez le client pour lequel vous venez de créer un abonnement.</span><span class="sxs-lookup"><span data-stu-id="c3238-157">Search for the customer for whom you just created a subscription.</span></span> <span data-ttu-id="c3238-158">Cliquez sur le **nom de la société** pour explorer les détails.</span><span class="sxs-lookup"><span data-stu-id="c3238-158">Click the **Company name** to drill down into the details.</span></span>

    ![Rechercher le client](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="c3238-160">Dans le panneau gauche, sélectionnez **Gestion des services**.</span><span class="sxs-lookup"><span data-stu-id="c3238-160">In the left-pane, select **Service management**.</span></span> <span data-ttu-id="c3238-161">Dans le panneau droit, sous **Administrer des services**, cliquez sur **Portail de gestion Microsoft Azure** pour vous connecter en tant qu’administrateur Azure pour votre client.</span><span class="sxs-lookup"><span data-stu-id="c3238-161">In the right-pane, under **Administer services**, click **Microsoft Azure Management Portal** to sign in as an Azure administrator for your customer.</span></span>

    ![Connexion au portail Azure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="c3238-163">Pour créer une instance StorSimple Device Manager, cliquez sur **+ Nouveau** et recherchez ou accédez à **Série d’appareils virtuels StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="c3238-163">To create a StorSimple Device Manager, click **+ New** and search for or navigate to **StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="c3238-164">Pour plus d’informations, accédez à la page [Déployer un service StorSimple Device Manager](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="c3238-164">For more information, go to [Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Créer un service StorSimple Device Manager](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="c3238-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c3238-166">Next steps</span></span>

- <span data-ttu-id="c3238-167">Si vous avez des questions supplémentaires concernant StorSimple dans le programme des fournisseurs de solutions cloud, accédez à [StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md) (StorSimple dans le programme des fournisseurs de solutions cloud : Forum Aux Questions).</span><span class="sxs-lookup"><span data-stu-id="c3238-167">If you have more questions regarding the StorSimple in CSP, go to [StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="c3238-168">Si vous êtes prêt à déployer votre instance StorSimple, accédez à [Deploy StorSimple Virtual Array for Cloud Solution Provider Program](storsimple-partner-csp-deploy.md) (Déployer StorSimple Virtual Array pour le programme des fournisseurs de solutions cloud).</span><span class="sxs-lookup"><span data-stu-id="c3238-168">If you are ready to deploy your StorSimple, go to [Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>
