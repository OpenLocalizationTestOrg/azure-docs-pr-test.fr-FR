---
title: "aaaMicrosoft Azure StorSimple et vue d’ensemble du programme fournisseur de Solutions Cloud | Documents Microsoft"
description: "Vue d’ensemble sur hello StorSimple et le fournisseur de services cryptographiques pour les partenaires de StorSimple."
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
ms.openlocfilehash: b5d999f2fbb9a27e7404ff454957b29dbef56af6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="908e6-103">Déployer StorSimple Virtual Array pour le programme des fournisseurs de solutions cloud</span><span class="sxs-lookup"><span data-stu-id="908e6-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="908e6-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="908e6-104">Overview</span></span>

<span data-ttu-id="908e6-105">StorSimple Virtual Array peuvent être déployé par les partenaires de fournisseur de solutions de Cloud (CSP) hello pour leurs clients.</span><span class="sxs-lookup"><span data-stu-id="908e6-105">StorSimple Virtual Array can be deployed by hello Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="908e6-106">Un partenaire CSP peut créer un service StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="908e6-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="908e6-107">Ce service peut ensuite être toodeploy utilisé et gérer StorSimple Virtual Array et hello associées des volumes, partages et les sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="908e6-107">This service can then be used toodeploy and manage StorSimple Virtual Array and hello associated shares, volumes, and backups.</span></span>

<span data-ttu-id="908e6-108">Cet article décrit comment un partenaire CSP peut ajouter un client ou un nouveau client existant de tooan d’abonnement, puis un toodeploy service un StorSimple Virtual Array CSP.</span><span class="sxs-lookup"><span data-stu-id="908e6-108">This article describes how a CSP partner can add a customer or a new subscription tooan existing customer and then create a service toodeploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="908e6-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="908e6-109">Prerequisites</span></span>

<span data-ttu-id="908e6-110">Avant de commencer, assurez-vous de satisfaire les exigences suivantes :</span><span class="sxs-lookup"><span data-stu-id="908e6-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="908e6-111">Vous êtes inscrit sous le programme du fournisseur de services cryptographiques hello.</span><span class="sxs-lookup"><span data-stu-id="908e6-111">You are enrolled under hello CSP program.</span></span>
- <span data-ttu-id="908e6-112">Vous avez des informations d’identification valides pour [l’Espace Partenaires](http://partnercenter.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="908e6-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="908e6-113">informations d’identification Hello vous toosign de nouveaux clients toohello partenaire tooadd portail, rechercher des clients ou accédez tooa le compte client à partir du tableau de bord partenaires hello.</span><span class="sxs-lookup"><span data-stu-id="908e6-113">hello credentials enable you toosign in toohello Partner portal tooadd new customers, search for customers, or navigate tooa customer account from hello Partner dashboard.</span></span> <span data-ttu-id="908e6-114">Hello CSP peut fonctionner en tant qu’un administrateur StorSimple pour le compte client hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="908e6-114">hello CSP can function as a StorSimple administrator on behalf of hello customer in hello Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="908e6-115">Ajouter un client</span><span class="sxs-lookup"><span data-stu-id="908e6-115">Add a customer</span></span>

<span data-ttu-id="908e6-116">Si vous ajoutez un client, un abonnement est automatiquement créé.</span><span class="sxs-lookup"><span data-stu-id="908e6-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="908e6-117">tooadd un client (et créer automatiquement un abonnement), effectuer hello comme suit dans le portail du partenaire hello.</span><span class="sxs-lookup"><span data-stu-id="908e6-117">tooadd a customer (and automatically create a subscription), perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="908e6-118">Accédez toohello [Partner Center](http://partnercenter.microsoft.com/) et connectez-vous en utilisant vos informations d’identification du fournisseur de services cryptographiques.</span><span class="sxs-lookup"><span data-stu-id="908e6-118">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="908e6-119">Cliquez sur **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="908e6-119">Click **Dashboard**.</span></span>

     ![Tableau de bord dans l’Espace Partenaires](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="908e6-121">Dans le volet gauche du hello, cliquez sur **clients**.</span><span class="sxs-lookup"><span data-stu-id="908e6-121">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="908e6-122">Dans le volet droit du hello, cliquez sur **Ajouter clients**.</span><span class="sxs-lookup"><span data-stu-id="908e6-122">In hello right-pane, click **Add customers**.</span></span> <span data-ttu-id="908e6-123">Entrez les détails de hello du client de hello.</span><span class="sxs-lookup"><span data-stu-id="908e6-123">Enter hello details of hello customer.</span></span> <span data-ttu-id="908e6-124">Cliquez sur **suivant : abonnements** toocreate un abonnement client.</span><span class="sxs-lookup"><span data-stu-id="908e6-124">Click **Next: Subscriptions** toocreate a customer subscription.</span></span>

    ![Ajouter un client](./media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="908e6-126">Sélectionnez l’offre **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="908e6-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="908e6-127">Défiler vers le bas de la page de hello et cliquez sur toohello **révision**.</span><span class="sxs-lookup"><span data-stu-id="908e6-127">Scroll toohello bottom of hello page and click **Review**.</span></span>

    ![Revoir les informations d’abonnement](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="908e6-129">Passez en revue les informations hello et cliquez sur **Submit**.</span><span class="sxs-lookup"><span data-stu-id="908e6-129">Review hello information and click **Submit**.</span></span>

    ![Envoyer l’abonnement](./media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="908e6-131">Enregistrer les informations de confirmation hello pour référence ultérieure.</span><span class="sxs-lookup"><span data-stu-id="908e6-131">Save hello confirmation information for future reference.</span></span>

    ![Enregistrer la confirmation](./media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="908e6-133">Rechercher ou parcourir client toohello que vous venez d’ajouter.</span><span class="sxs-lookup"><span data-stu-id="908e6-133">Find or navigate toohello customer you just added.</span></span> <span data-ttu-id="908e6-134">Cliquez sur hello **nom de la société** toodrill vers le bas dans les détails de hello.</span><span class="sxs-lookup"><span data-stu-id="908e6-134">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Recherchez le hello client](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="908e6-136">Dans le volet gauche du hello, sélectionnez **gestion des services**.</span><span class="sxs-lookup"><span data-stu-id="908e6-136">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="908e6-137">Dans hello volet droit, sous **administrer les services**, cliquez sur **Microsoft Azure Management Portal** toosign en tant qu’administrateur pour votre client Azure.</span><span class="sxs-lookup"><span data-stu-id="908e6-137">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![Connectez-vous au portail de tooAzure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="908e6-139">toocreate un gestionnaire de périphériques StorSimple, cliquez sur **+ nouveau** et rechercher ou parcourir trop**série d’appareils virtuels StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="908e6-139">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="908e6-140">Pour plus d’informations, consultez trop[déployer un service Gestionnaire de périphériques StorSimple](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="908e6-140">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Créer un service StorSimple Device Manager](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="908e6-142">Ajouter un abonnement</span><span class="sxs-lookup"><span data-stu-id="908e6-142">Add a subscription</span></span>

<span data-ttu-id="908e6-143">Dans certains cas, vous avez peut-être un client existant, et vous devez tooadd un abonnement.</span><span class="sxs-lookup"><span data-stu-id="908e6-143">In some instances, you may have an existing customer, and you need tooadd a subscription.</span></span> <span data-ttu-id="908e6-144">tooadd un client existant de tooan d’abonnement, effectuez hello comme suit dans le portail du partenaire hello.</span><span class="sxs-lookup"><span data-stu-id="908e6-144">tooadd a subscription tooan existing customer, perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="908e6-145">Accédez toohello [Partner Center](http://partnercenter.microsoft.com/) et connectez-vous en utilisant vos informations d’identification du fournisseur de services cryptographiques.</span><span class="sxs-lookup"><span data-stu-id="908e6-145">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="908e6-146">Cliquez sur **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="908e6-146">Click **Dashboard**.</span></span>

     ![Tableau de bord dans l’Espace Partenaires](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="908e6-148">Dans le volet gauche du hello, cliquez sur **clients**.</span><span class="sxs-lookup"><span data-stu-id="908e6-148">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="908e6-149">Rechercher ou parcourir toohello client tooadd un abonnement à.</span><span class="sxs-lookup"><span data-stu-id="908e6-149">Find or navigate toohello customer you want tooadd a subscription to.</span></span> <span data-ttu-id="908e6-150">Cliquez sur hello ![développer une icône de coche](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) ligne de hello tooexpand icône pour le nom de la société hello pour votre client.</span><span class="sxs-lookup"><span data-stu-id="908e6-150">Click hello ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon tooexpand hello row for hello company name for your customer.</span></span> <span data-ttu-id="908e6-151">Dans Détails de hello, cliquez sur **ajouter des abonnements**.</span><span class="sxs-lookup"><span data-stu-id="908e6-151">In hello details, click **Add subscriptions**.</span></span>

    ![Clients](./media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="908e6-153">Vérifiez **Microsoft Azure** pour hello **premiers offres** dans l’abonnement de hello et cliquez sur **Submit**.</span><span class="sxs-lookup"><span data-stu-id="908e6-153">Check **Microsoft Azure** for hello **Top offers** in hello subscription and click **Submit**.</span></span> <span data-ttu-id="908e6-154">Ceci crée un nouvel abonnement.</span><span class="sxs-lookup"><span data-stu-id="908e6-154">This creates a new subscription.</span></span>

    ![Ajouter un nouvel abonnement](./media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="908e6-156">Après la création d’un nouvel abonnement, cliquez sur **<--clients** dans hello volet gauche tooreturn toohello **clients** page.</span><span class="sxs-lookup"><span data-stu-id="908e6-156">After a new subscription is created, click **<-- Customers** in hello left-pane tooreturn toohello **Customers** page.</span></span> <span data-ttu-id="908e6-157">Recherchez le client de hello pour lequel vous venez de créer un abonnement.</span><span class="sxs-lookup"><span data-stu-id="908e6-157">Search for hello customer for whom you just created a subscription.</span></span> <span data-ttu-id="908e6-158">Cliquez sur hello **nom de la société** toodrill vers le bas dans les détails de hello.</span><span class="sxs-lookup"><span data-stu-id="908e6-158">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Recherchez le hello client](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="908e6-160">Dans le volet gauche du hello, sélectionnez **gestion des services**.</span><span class="sxs-lookup"><span data-stu-id="908e6-160">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="908e6-161">Dans hello volet droit, sous **administrer les services**, cliquez sur **Microsoft Azure Management Portal** toosign en tant qu’administrateur pour votre client Azure.</span><span class="sxs-lookup"><span data-stu-id="908e6-161">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![Connectez-vous au portail de tooAzure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="908e6-163">toocreate un gestionnaire de périphériques StorSimple, cliquez sur **+ nouveau** et rechercher ou parcourir trop**série d’appareils virtuels StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="908e6-163">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="908e6-164">Pour plus d’informations, consultez trop[déployer un service Gestionnaire de périphériques StorSimple](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="908e6-164">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Créer un service StorSimple Device Manager](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="908e6-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="908e6-166">Next steps</span></span>

- <span data-ttu-id="908e6-167">Si vous avez d’autres questions concernant hello StorSimple dans le fournisseur de services cryptographiques, passez trop[StorSimple dans le fournisseur de services cryptographiques : Forum aux questions](storsimple-partner-csp-faq.md).</span><span class="sxs-lookup"><span data-stu-id="908e6-167">If you have more questions regarding hello StorSimple in CSP, go too[StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="908e6-168">Si vous êtes prêt toodeploy votre StorSimple, accédez trop[déployer votre appareil StorSimple dans le fournisseur de services cryptographiques](storsimple-partner-csp-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="908e6-168">If you are ready toodeploy your StorSimple, go too[Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>
