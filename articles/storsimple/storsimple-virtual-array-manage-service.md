---
title: "aaaDeploy service du Gestionnaire de périphériques StorSimple | Documents Microsoft"
description: "Explique comment toocreate et delete hello service Gestionnaire de périphériques StorSimple Bonjour portail Azure et décrit comment toomanage hello clé d’inscription de service."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="656e1-103">Déployer le service du Gestionnaire de périphériques StorSimple hello pour StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="656e1-103">Deploy hello StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="656e1-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="656e1-104">Overview</span></span>

<span data-ttu-id="656e1-105">Hello le Gestionnaire de périphériques StorSimple service s’exécute dans Microsoft Azure et connecte les appareils StorSimple toomultiple.</span><span class="sxs-lookup"><span data-stu-id="656e1-105">hello StorSimple Device Manager service runs in Microsoft Azure and connects toomultiple StorSimple devices.</span></span> <span data-ttu-id="656e1-106">Après avoir créé le service de hello, vous pouvez l’utiliser appareils hello toomanage hello Microsoft Azure portail s’exécutant dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="656e1-106">After you create hello service, you can use it toomanage hello devices from hello Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="656e1-107">Cela vous permet de toomonitor tous les périphériques hello connecté toohello StorSimple le Gestionnaire de périphériques de service à partir d’un emplacement unique et centralisé, réduisant les tâches administratives.</span><span class="sxs-lookup"><span data-stu-id="656e1-107">This allows you toomonitor all hello devices that are connected toohello StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="656e1-108">Hello courantes tâches connexes tooa service du Gestionnaire de périphériques StorSimple sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="656e1-108">hello common tasks related tooa StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="656e1-109">Créer un service</span><span class="sxs-lookup"><span data-stu-id="656e1-109">Create a service</span></span>
* <span data-ttu-id="656e1-110">Supprimer un service</span><span class="sxs-lookup"><span data-stu-id="656e1-110">Delete a service</span></span>
* <span data-ttu-id="656e1-111">Obtenir la clé d’inscription hello</span><span class="sxs-lookup"><span data-stu-id="656e1-111">Get hello service registration key</span></span>
* <span data-ttu-id="656e1-112">Régénérer la clé d’inscription hello</span><span class="sxs-lookup"><span data-stu-id="656e1-112">Regenerate hello service registration key</span></span>

<span data-ttu-id="656e1-113">Ce didacticiel explique comment tooperform de hello les tâches précédentes.</span><span class="sxs-lookup"><span data-stu-id="656e1-113">This tutorial describes how tooperform each of hello preceding tasks.</span></span> <span data-ttu-id="656e1-114">informations Hello contenues dans cet article sont applicable uniquement tooStorSimple réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="656e1-114">hello information contained in this article is applicable only tooStorSimple Virtual Arrays.</span></span> <span data-ttu-id="656e1-115">Pour plus d’informations sur la série StorSimple 8000, accédez trop[déployer un service StorSimple Manager](storsimple-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="656e1-115">For more information on StorSimple 8000 series, go too[deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="656e1-116">Créer un service</span><span class="sxs-lookup"><span data-stu-id="656e1-116">Create a service</span></span>

<span data-ttu-id="656e1-117">toocreate un service, vous devez toohave :</span><span class="sxs-lookup"><span data-stu-id="656e1-117">toocreate a service, you need toohave:</span></span>

* <span data-ttu-id="656e1-118">Un abonnement avec un contrat Entreprise</span><span class="sxs-lookup"><span data-stu-id="656e1-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="656e1-119">Un compte de stockage Microsoft Azure actif</span><span class="sxs-lookup"><span data-stu-id="656e1-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="656e1-120">informations de facturation sont utilisées pour la gestion de l’accès de Hello</span><span class="sxs-lookup"><span data-stu-id="656e1-120">hello billing information that is used for access management</span></span>

<span data-ttu-id="656e1-121">Vous pouvez également choisir de toogenerate un compte de stockage lorsque vous créez le service de hello.</span><span class="sxs-lookup"><span data-stu-id="656e1-121">You can also choose toogenerate a storage account when you create hello service.</span></span>

<span data-ttu-id="656e1-122">Un seul service peut gérer plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="656e1-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="656e1-123">Cependant, un appareil ne peut pas couvrir plusieurs services.</span><span class="sxs-lookup"><span data-stu-id="656e1-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="656e1-124">Une grande entreprise peut avoir plusieurs toowork d’instances de service avec différents abonnements, organisations ou emplacements de déploiement.</span><span class="sxs-lookup"><span data-stu-id="656e1-124">A large enterprise can have multiple service instances toowork with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="656e1-125">Vous avez besoin des instances distinctes d’unités de gestionnaire de périphériques StorSimple service toomanage StorSimple 8000 series et les tableaux de virtuel StorSimple.</span><span class="sxs-lookup"><span data-stu-id="656e1-125">You need separate instances of StorSimple Device Manager service toomanage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="656e1-126">Effectuer hello suivant les étapes toocreate un service.</span><span class="sxs-lookup"><span data-stu-id="656e1-126">Perform hello following steps toocreate a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="656e1-127">Supprimer un service</span><span class="sxs-lookup"><span data-stu-id="656e1-127">Delete a service</span></span>

<span data-ttu-id="656e1-128">Avant de supprimer un service, assurez-vous qu’aucun appareil connecté ne l’utilise.</span><span class="sxs-lookup"><span data-stu-id="656e1-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="656e1-129">Si le service de hello est en cours d’utilisation, désactiver les périphériques de hello connecté.</span><span class="sxs-lookup"><span data-stu-id="656e1-129">If hello service is in use, deactivate hello connected devices.</span></span> <span data-ttu-id="656e1-130">Hello désactiver l’opération sera le serveur de connexion hello entre l’appareil de hello et service de hello, mais conserver les données d’appareil hello dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="656e1-130">hello deactivate operation will sever hello connection between hello device and hello service, but preserve hello device data in hello cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="656e1-131">Après la suppression d’un service, opération de hello ne peut pas être annulée.</span><span class="sxs-lookup"><span data-stu-id="656e1-131">After a service is deleted, hello operation cannot be reversed.</span></span> <span data-ttu-id="656e1-132">N’importe quel appareil qui utilise hello service devez toobe usine avant de pouvoir être utilisé avec un autre service.</span><span class="sxs-lookup"><span data-stu-id="656e1-132">Any device that was using hello service will need toobe factory reset before it can be used with another service.</span></span> <span data-ttu-id="656e1-133">Dans ce scénario, les données locales de hello sur le périphérique de hello, ainsi que la configuration de hello, seront perdues.</span><span class="sxs-lookup"><span data-stu-id="656e1-133">In this scenario, hello local data on hello device, as well as hello configuration, will be lost.</span></span>
 

<span data-ttu-id="656e1-134">Effectuer hello suivant les étapes toodelete un service.</span><span class="sxs-lookup"><span data-stu-id="656e1-134">Perform hello following steps toodelete a service.</span></span>

#### <a name="toodelete-a-service"></a><span data-ttu-id="656e1-135">toodelete un service</span><span class="sxs-lookup"><span data-stu-id="656e1-135">toodelete a service</span></span>

1. <span data-ttu-id="656e1-136">Accédez trop**toutes les ressources**.</span><span class="sxs-lookup"><span data-stu-id="656e1-136">Go too**All resources**.</span></span> <span data-ttu-id="656e1-137">Recherchez votre service StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="656e1-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="656e1-138">Sélectionnez service hello que vous souhaitez toodelete.</span><span class="sxs-lookup"><span data-stu-id="656e1-138">Select hello service that you wish toodelete.</span></span>
   
    ![Sélectionnez service toodelete](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="656e1-140">Accédez tooensure de tableau de bord de service tooyour il n’y aucun périphérique connecté toohello service.</span><span class="sxs-lookup"><span data-stu-id="656e1-140">Go tooyour service dashboard tooensure there are no devices connected toohello service.</span></span> <span data-ttu-id="656e1-141">S’il n’y a aucun appareil inscrit auprès de ce service, vous verrez également un effet de toohello de message de bannière.</span><span class="sxs-lookup"><span data-stu-id="656e1-141">If there are no devices registered with this service, you will also see a banner message toohello effect.</span></span> <span data-ttu-id="656e1-142">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="656e1-142">Click **Delete**.</span></span>
   
    ![Suppression du service](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="656e1-144">Lorsque vous êtes invité à confirmer l’opération, cliquez sur **Oui** dans la notification de confirmation hello.</span><span class="sxs-lookup"><span data-stu-id="656e1-144">When prompted for confirmation, click **Yes** in hello confirmation notification.</span></span> 
   
    ![Confirmer la suppression du service](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="656e1-146">Il peut prendre quelques minutes pour hello service toobe est supprimé.</span><span class="sxs-lookup"><span data-stu-id="656e1-146">It may take a few minutes for hello service toobe deleted.</span></span> <span data-ttu-id="656e1-147">Une fois hello service est correctement supprimé, vous serez averti.</span><span class="sxs-lookup"><span data-stu-id="656e1-147">After hello service is successfully deleted, you will be notified.</span></span>
   
    ![Suppression du service réussie](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="656e1-149">liste Hello des services va être actualisée.</span><span class="sxs-lookup"><span data-stu-id="656e1-149">hello list of services will be refreshed.</span></span>

 ![Liste des services mise à jour](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a><span data-ttu-id="656e1-151">Obtenir la clé d’inscription hello</span><span class="sxs-lookup"><span data-stu-id="656e1-151">Get hello service registration key</span></span>
<span data-ttu-id="656e1-152">Une fois que vous avez créé un service, vous devez tooregister votre appareil StorSimple hello service.</span><span class="sxs-lookup"><span data-stu-id="656e1-152">After you have successfully created a service, you will need tooregister your StorSimple device with hello service.</span></span> <span data-ttu-id="656e1-153">tooregister votre premier appareil StorSimple, vous devez serez hello clé d’inscription de service.</span><span class="sxs-lookup"><span data-stu-id="656e1-153">tooregister your first StorSimple device, you will need hello service registration key.</span></span> <span data-ttu-id="656e1-154">tooregister autres périphériques avec un service StorSimple existant, vous devez la clé d’enregistrement hello et hello clé de chiffrement (qui est généré sur le premier périphérique de hello lors de l’inscription).</span><span class="sxs-lookup"><span data-stu-id="656e1-154">tooregister additional devices with an existing StorSimple service, you will need both hello registration key and hello service data encryption key (which is generated on hello first device during registration).</span></span> <span data-ttu-id="656e1-155">Pour plus d’informations sur la clé de chiffrement de données de service hello, consultez [sécurité StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="656e1-155">For more information about hello service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="656e1-156">Vous pouvez obtenir la clé d’inscription de hello en accédant à hello **clés** panneau pour votre service.</span><span class="sxs-lookup"><span data-stu-id="656e1-156">You can get hello registration key by accessing hello **Keys** blade for your service.</span></span>

<span data-ttu-id="656e1-157">Effectuer hello après la clé d’inscription étapes tooget hello.</span><span class="sxs-lookup"><span data-stu-id="656e1-157">Perform hello following steps tooget hello service registration key.</span></span>

#### <a name="tooget-hello-service-registration-key"></a><span data-ttu-id="656e1-158">clé d’inscription tooget hello</span><span class="sxs-lookup"><span data-stu-id="656e1-158">tooget hello service registration key</span></span>
1. <span data-ttu-id="656e1-159">Bonjour **le Gestionnaire de périphériques StorSimple** panneau, accédez trop**gestion &gt;**  **clés**.</span><span class="sxs-lookup"><span data-stu-id="656e1-159">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![Panneau Clés](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="656e1-161">Bonjour **clés** blade, une clé d’inscription de service apparaît.</span><span class="sxs-lookup"><span data-stu-id="656e1-161">In hello **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="656e1-162">Copiez la clé d’inscription de hello à l’aide d’icône de copie hello.</span><span class="sxs-lookup"><span data-stu-id="656e1-162">Copy hello registration key using hello copy icon.</span></span> 

<span data-ttu-id="656e1-163">Conservez la clé d’inscription hello dans un emplacement sûr.</span><span class="sxs-lookup"><span data-stu-id="656e1-163">Keep hello service registration key in a safe location.</span></span> <span data-ttu-id="656e1-164">Vous devez cette clé, comme clé de chiffrement de données de service de hello, tooregister des appareils supplémentaires auprès de ce service.</span><span class="sxs-lookup"><span data-stu-id="656e1-164">You will need this key, as well as hello service data encryption key, tooregister additional devices with this service.</span></span> <span data-ttu-id="656e1-165">Après avoir obtenu la clé d’inscription hello, vous devez tooconfigure votre appareil via hello Windows PowerShell pour StorSimple interface.</span><span class="sxs-lookup"><span data-stu-id="656e1-165">After obtaining hello service registration key, you will need tooconfigure your device through hello Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-hello-service-registration-key"></a><span data-ttu-id="656e1-166">Régénérer la clé d’inscription hello</span><span class="sxs-lookup"><span data-stu-id="656e1-166">Regenerate hello service registration key</span></span>
<span data-ttu-id="656e1-167">Si vous êtes tooperform requis la rotation des clés ou si la liste hello des administrateurs de service a changé, vous devez tooregenerate une clé d’inscription de service.</span><span class="sxs-lookup"><span data-stu-id="656e1-167">You will need tooregenerate a service registration key if you are required tooperform key rotation or if hello list of service administrators has changed.</span></span> <span data-ttu-id="656e1-168">Lorsque vous régénérez la clé de hello, clé hello est utilisé uniquement pour l’inscription des appareils suivants.</span><span class="sxs-lookup"><span data-stu-id="656e1-168">When you regenerate hello key, hello new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="656e1-169">appareils Hello déjà inscrites ne sont pas affectés par ce processus.</span><span class="sxs-lookup"><span data-stu-id="656e1-169">hello devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="656e1-170">Effectuer hello suivant les étapes tooregenerate une clé d’inscription de service.</span><span class="sxs-lookup"><span data-stu-id="656e1-170">Perform hello following steps tooregenerate a service registration key.</span></span>

#### <a name="tooregenerate-hello-service-registration-key"></a><span data-ttu-id="656e1-171">clé d’inscription tooregenerate hello</span><span class="sxs-lookup"><span data-stu-id="656e1-171">tooregenerate hello service registration key</span></span>
1. <span data-ttu-id="656e1-172">Bonjour **le Gestionnaire de périphériques StorSimple** panneau, accédez trop**gestion &gt;**  **clés**.</span><span class="sxs-lookup"><span data-stu-id="656e1-172">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![Panneau Clés](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="656e1-174">Bonjour **clés** panneau, cliquez sur **régénérer**.</span><span class="sxs-lookup"><span data-stu-id="656e1-174">In hello **Keys** blade, click **Regenerate**.</span></span>
   
   ![Cliquer sur Régénérer](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="656e1-176">Bonjour **clé d’inscription régénérer** panneau, révision hello action requise lorsque hello les clés sont régénérées.</span><span class="sxs-lookup"><span data-stu-id="656e1-176">In hello **Regenerate service registration key** blade, review hello action required when hello keys are regenerated.</span></span> <span data-ttu-id="656e1-177">Tous les périphériques suivants hello qui sont inscrits auprès de ce service utilise la nouvelle clé d’inscription de hello.</span><span class="sxs-lookup"><span data-stu-id="656e1-177">All hello subsequent devices that are registered with this service will use hello new registration key.</span></span> <span data-ttu-id="656e1-178">Cliquez sur **régénérer** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="656e1-178">Click **Regenerate** tooconfirm.</span></span> <span data-ttu-id="656e1-179">Vous serez averti une fois l’inscription de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="656e1-179">You will be notified after hello registration is complete.</span></span>
   
   ![Confirmer la régénération de la clé](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="656e1-181">Une nouvelle clé d’inscription du service s’affiche.</span><span class="sxs-lookup"><span data-stu-id="656e1-181">A new service registration key will appear.</span></span>
   
    ![Confirmer la régénération de la clé](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="656e1-183">Copiez cette clé et sauvegardez-la pour enregistrer tout nouvel appareil auprès de ce service.</span><span class="sxs-lookup"><span data-stu-id="656e1-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="656e1-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="656e1-184">Next steps</span></span>
* <span data-ttu-id="656e1-185">Découvrez comment trop[prise en main](storsimple-virtual-array-deploy1-portal-prep.md) avec un tableau virtuel StorSimple.</span><span class="sxs-lookup"><span data-stu-id="656e1-185">Learn how too[get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="656e1-186">Découvrez comment trop[administrer votre appareil StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="656e1-186">Learn how too[administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

