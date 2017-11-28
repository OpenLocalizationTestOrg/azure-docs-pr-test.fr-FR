---
title: "Déployer le service StorSimple Device Manager | Microsoft Docs"
description: "Cet article décrit comment créer et supprimer le service StorSimple Device Manager dans le Portail Azure, ainsi que la procédure de gestion de la clé d’inscription du service."
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
ms.openlocfilehash: 1881a0625b107ae1a90e5b772f5296a4d728973d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-the-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="1de2e-103">Déployer le service StorSimple Device Manager pour StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="1de2e-103">Deploy the StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="1de2e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="1de2e-104">Overview</span></span>

<span data-ttu-id="1de2e-105">Le service StorSimple Device Manager s’exécute dans Microsoft Azure et se connecte à plusieurs appareils StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1de2e-105">The StorSimple Device Manager service runs in Microsoft Azure and connects to multiple StorSimple devices.</span></span> <span data-ttu-id="1de2e-106">Après avoir créé le service, vous pouvez l’utiliser pour gérer les appareils à partir du portail Microsoft Azure s’exécutant dans un navigateur.</span><span class="sxs-lookup"><span data-stu-id="1de2e-106">After you create the service, you can use it to manage the devices from the Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="1de2e-107">Vous pouvez ainsi surveiller tous les appareils qui sont connectés au service StorSimple Device Manager à partir d’un emplacement central unique, ce qui réduit la charge administrative.</span><span class="sxs-lookup"><span data-stu-id="1de2e-107">This allows you to monitor all the devices that are connected to the StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="1de2e-108">Les tâches courantes associées à un service StorSimple Device Manager sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="1de2e-108">The common tasks related to a StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="1de2e-109">Création d’un service</span><span class="sxs-lookup"><span data-stu-id="1de2e-109">Create a service</span></span>
* <span data-ttu-id="1de2e-110">Supprimer un service</span><span class="sxs-lookup"><span data-stu-id="1de2e-110">Delete a service</span></span>
* <span data-ttu-id="1de2e-111">Obtenir la clé d’inscription du service</span><span class="sxs-lookup"><span data-stu-id="1de2e-111">Get the service registration key</span></span>
* <span data-ttu-id="1de2e-112">Régénération de la clé d’inscription de service</span><span class="sxs-lookup"><span data-stu-id="1de2e-112">Regenerate the service registration key</span></span>

<span data-ttu-id="1de2e-113">Ce didacticiel explique comment exécuter chacune des tâches ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="1de2e-113">This tutorial describes how to perform each of the preceding tasks.</span></span> <span data-ttu-id="1de2e-114">Les informations contenues dans cet article s’appliquent uniquement aux tableaux virtuels StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1de2e-114">The information contained in this article is applicable only to StorSimple Virtual Arrays.</span></span> <span data-ttu-id="1de2e-115">Pour plus d’informations sur la gamme StorSimple 8000, consultez la page [déployer un service StorSimple Manager](storsimple-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="1de2e-115">For more information on StorSimple 8000 series, go to [deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="1de2e-116">Création d’un service</span><span class="sxs-lookup"><span data-stu-id="1de2e-116">Create a service</span></span>

<span data-ttu-id="1de2e-117">Pour créer un service, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1de2e-117">To create a service, you need to have:</span></span>

* <span data-ttu-id="1de2e-118">Un abonnement avec un contrat Entreprise</span><span class="sxs-lookup"><span data-stu-id="1de2e-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="1de2e-119">Un compte de stockage Microsoft Azure actif</span><span class="sxs-lookup"><span data-stu-id="1de2e-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="1de2e-120">Les informations de facturation utilisées pour la gestion des accès</span><span class="sxs-lookup"><span data-stu-id="1de2e-120">The billing information that is used for access management</span></span>

<span data-ttu-id="1de2e-121">Vous pouvez également choisir de générer un compte de stockage lorsque vous créez le service.</span><span class="sxs-lookup"><span data-stu-id="1de2e-121">You can also choose to generate a storage account when you create the service.</span></span>

<span data-ttu-id="1de2e-122">Un seul service peut gérer plusieurs appareils.</span><span class="sxs-lookup"><span data-stu-id="1de2e-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="1de2e-123">Cependant, un appareil ne peut pas couvrir plusieurs services.</span><span class="sxs-lookup"><span data-stu-id="1de2e-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="1de2e-124">Une grande entreprise peut avoir plusieurs instances de service pour utiliser différents abonnements, organisations ou même emplacements de déploiement.</span><span class="sxs-lookup"><span data-stu-id="1de2e-124">A large enterprise can have multiple service instances to work with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="1de2e-125">Vous devez créer des instances distinctes du service StorSimple Device Manager pour gérer les appareils de la gamme StorSimple 8000 et les baies StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="1de2e-125">You need separate instances of StorSimple Device Manager service to manage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="1de2e-126">Procédez comme suit pour créer un service.</span><span class="sxs-lookup"><span data-stu-id="1de2e-126">Perform the following steps to create a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="1de2e-127">Supprimer un service</span><span class="sxs-lookup"><span data-stu-id="1de2e-127">Delete a service</span></span>

<span data-ttu-id="1de2e-128">Avant de supprimer un service, assurez-vous qu’aucun appareil connecté ne l’utilise.</span><span class="sxs-lookup"><span data-stu-id="1de2e-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="1de2e-129">Si le service est en cours d’utilisation, désactivez les appareils connectés.</span><span class="sxs-lookup"><span data-stu-id="1de2e-129">If the service is in use, deactivate the connected devices.</span></span> <span data-ttu-id="1de2e-130">L’opération de désactivation rompt la connexion entre l’appareil et le service, mais conserve les données de l’appareil dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="1de2e-130">The deactivate operation will sever the connection between the device and the service, but preserve the device data in the cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1de2e-131">Après qu’un service a été supprimé, l’opération ne peut pas être annulée.</span><span class="sxs-lookup"><span data-stu-id="1de2e-131">After a service is deleted, the operation cannot be reversed.</span></span> <span data-ttu-id="1de2e-132">Un appareil qui utilisait le service doit être réinitialisé aux paramètres d’usine avant de pouvoir être utilisé avec un autre service.</span><span class="sxs-lookup"><span data-stu-id="1de2e-132">Any device that was using the service will need to be factory reset before it can be used with another service.</span></span> <span data-ttu-id="1de2e-133">Dans ce scénario, les données locales de l’appareil, ainsi que la configuration, seront perdues.</span><span class="sxs-lookup"><span data-stu-id="1de2e-133">In this scenario, the local data on the device, as well as the configuration, will be lost.</span></span>
 

<span data-ttu-id="1de2e-134">Pour supprimer un service, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="1de2e-134">Perform the following steps to delete a service.</span></span>

#### <a name="to-delete-a-service"></a><span data-ttu-id="1de2e-135">Pour supprimer un service</span><span class="sxs-lookup"><span data-stu-id="1de2e-135">To delete a service</span></span>

1. <span data-ttu-id="1de2e-136">Sélectionnez **Toutes les ressources**.</span><span class="sxs-lookup"><span data-stu-id="1de2e-136">Go to **All resources**.</span></span> <span data-ttu-id="1de2e-137">Recherchez votre service StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="1de2e-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="1de2e-138">Sélectionnez le service à supprimer.</span><span class="sxs-lookup"><span data-stu-id="1de2e-138">Select the service that you wish to delete.</span></span>
   
    ![Sélectionner le service à supprimer](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="1de2e-140">Accédez à votre tableau de bord des services pour vous assurer qu’aucun appareil n’est connecté au service.</span><span class="sxs-lookup"><span data-stu-id="1de2e-140">Go to your service dashboard to ensure there are no devices connected to the service.</span></span> <span data-ttu-id="1de2e-141">Si aucun appareil n’est inscrit auprès de ce service, vous en êtes également averti par un message de bannière.</span><span class="sxs-lookup"><span data-stu-id="1de2e-141">If there are no devices registered with this service, you will also see a banner message to the effect.</span></span> <span data-ttu-id="1de2e-142">Cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="1de2e-142">Click **Delete**.</span></span>
   
    ![Suppression du service](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="1de2e-144">Lorsque vous êtes invité à confirmer l’opération, cliquez sur **Oui** dans la notification de confirmation.</span><span class="sxs-lookup"><span data-stu-id="1de2e-144">When prompted for confirmation, click **Yes** in the confirmation notification.</span></span> 
   
    ![Confirmer la suppression du service](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="1de2e-146">La suppression du service peut nécessiter quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="1de2e-146">It may take a few minutes for the service to be deleted.</span></span> <span data-ttu-id="1de2e-147">Une fois le service supprimé, vous en êtes informé par un message.</span><span class="sxs-lookup"><span data-stu-id="1de2e-147">After the service is successfully deleted, you will be notified.</span></span>
   
    ![Suppression du service réussie](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="1de2e-149">La liste des services est actualisée.</span><span class="sxs-lookup"><span data-stu-id="1de2e-149">The list of services will be refreshed.</span></span>

 ![Liste des services mise à jour](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-the-service-registration-key"></a><span data-ttu-id="1de2e-151">Obtenir la clé d’inscription du service</span><span class="sxs-lookup"><span data-stu-id="1de2e-151">Get the service registration key</span></span>
<span data-ttu-id="1de2e-152">Une fois que vous avez créé un service, vous devez inscrire votre appareil StorSimple auprès du service.</span><span class="sxs-lookup"><span data-stu-id="1de2e-152">After you have successfully created a service, you will need to register your StorSimple device with the service.</span></span> <span data-ttu-id="1de2e-153">Pour inscrire votre premier appareil StorSimple, vous avez besoin de la clé d’inscription du service.</span><span class="sxs-lookup"><span data-stu-id="1de2e-153">To register your first StorSimple device, you will need the service registration key.</span></span> <span data-ttu-id="1de2e-154">Pour inscrire des appareils supplémentaires avec un service StorSimple existant, vous avez besoin de la clé d’inscription et de la clé de chiffrement des données du service (générée sur le premier appareil lors de l’inscription).</span><span class="sxs-lookup"><span data-stu-id="1de2e-154">To register additional devices with an existing StorSimple service, you will need both the registration key and the service data encryption key (which is generated on the first device during registration).</span></span> <span data-ttu-id="1de2e-155">Pour plus d’informations sur la clé de chiffrement des données du service, consultez la rubrique [Sécurité StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="1de2e-155">For more information about the service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="1de2e-156">Vous pouvez obtenir la clé d’inscription en accédant au panneau **Clés** relatif à votre service.</span><span class="sxs-lookup"><span data-stu-id="1de2e-156">You can get the registration key by accessing the **Keys** blade for your service.</span></span>

<span data-ttu-id="1de2e-157">Procédez comme suit pour obtenir la clé d’inscription du service.</span><span class="sxs-lookup"><span data-stu-id="1de2e-157">Perform the following steps to get the service registration key.</span></span>

#### <a name="to-get-the-service-registration-key"></a><span data-ttu-id="1de2e-158">Pour obtenir la clé d’inscription du service</span><span class="sxs-lookup"><span data-stu-id="1de2e-158">To get the service registration key</span></span>
1. <span data-ttu-id="1de2e-159">Dans le panneau **Instance de StorSimple Device Manager**, accédez à **Gestion &gt;** **Clés**.</span><span class="sxs-lookup"><span data-stu-id="1de2e-159">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![Panneau Clés](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="1de2e-161">Une clé d’inscription du service apparaît dans le panneau **Clés**.</span><span class="sxs-lookup"><span data-stu-id="1de2e-161">In the **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="1de2e-162">Copiez la clé d’inscription à l’aide de l’icône de copie.</span><span class="sxs-lookup"><span data-stu-id="1de2e-162">Copy the registration key using the copy icon.</span></span> 

<span data-ttu-id="1de2e-163">Conservez la clé d’inscription du service dans un emplacement sûr.</span><span class="sxs-lookup"><span data-stu-id="1de2e-163">Keep the service registration key in a safe location.</span></span> <span data-ttu-id="1de2e-164">Vous aurez besoin de cette clé, ainsi que de la clé de chiffrement des données du service, pour enregistrer des appareils supplémentaires auprès du service.</span><span class="sxs-lookup"><span data-stu-id="1de2e-164">You will need this key, as well as the service data encryption key, to register additional devices with this service.</span></span> <span data-ttu-id="1de2e-165">Après avoir obtenu la clé d’inscription du service, vous devez configurer votre appareil via l’interface Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1de2e-165">After obtaining the service registration key, you will need to configure your device through the Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-the-service-registration-key"></a><span data-ttu-id="1de2e-166">Régénérer la clé d’inscription du service</span><span class="sxs-lookup"><span data-stu-id="1de2e-166">Regenerate the service registration key</span></span>
<span data-ttu-id="1de2e-167">Vous devez régénérer une clé d’inscription du service si vous êtes amené à effectuer une rotation des clés ou si la liste des administrateurs du service a changé.</span><span class="sxs-lookup"><span data-stu-id="1de2e-167">You will need to regenerate a service registration key if you are required to perform key rotation or if the list of service administrators has changed.</span></span> <span data-ttu-id="1de2e-168">Lorsque vous régénérez la clé, la nouvelle clé est utilisée uniquement pour l’enregistrement des appareils suivants.</span><span class="sxs-lookup"><span data-stu-id="1de2e-168">When you regenerate the key, the new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="1de2e-169">Les appareils déjà enregistrés ne sont pas affectés par ce processus.</span><span class="sxs-lookup"><span data-stu-id="1de2e-169">The devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="1de2e-170">Procédez comme suit pour régénérer une clé d’inscription du service.</span><span class="sxs-lookup"><span data-stu-id="1de2e-170">Perform the following steps to regenerate a service registration key.</span></span>

#### <a name="to-regenerate-the-service-registration-key"></a><span data-ttu-id="1de2e-171">Pour régénérer la clé d’inscription du service</span><span class="sxs-lookup"><span data-stu-id="1de2e-171">To regenerate the service registration key</span></span>
1. <span data-ttu-id="1de2e-172">Dans le panneau **Instance de StorSimple Device Manager**, accédez à **Gestion &gt;** **Clés**.</span><span class="sxs-lookup"><span data-stu-id="1de2e-172">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![Panneau Clés](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="1de2e-174">Dans le panneau **Clés**, cliquez sur **Régénérer**.</span><span class="sxs-lookup"><span data-stu-id="1de2e-174">In the **Keys** blade, click **Regenerate**.</span></span>
   
   ![Cliquer sur Régénérer](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="1de2e-176">Dans le panneau **Régénérer la clé d’inscription du service**, vérifiez l’action requise lors de la régénération des clés.</span><span class="sxs-lookup"><span data-stu-id="1de2e-176">In the **Regenerate service registration key** blade, review the action required when the keys are regenerated.</span></span> <span data-ttu-id="1de2e-177">Tous les appareils qui seront inscrits auprès de ce service par la suite utiliseront la nouvelle clé d’inscription.</span><span class="sxs-lookup"><span data-stu-id="1de2e-177">All the subsequent devices that are registered with this service will use the new registration key.</span></span> <span data-ttu-id="1de2e-178">Cliquez sur **Régénérer** pour confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="1de2e-178">Click **Regenerate** to confirm.</span></span> <span data-ttu-id="1de2e-179">Une fois l’inscription terminée, vous en êtes informé par un message.</span><span class="sxs-lookup"><span data-stu-id="1de2e-179">You will be notified after the registration is complete.</span></span>
   
   ![Confirmer la régénération de la clé](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="1de2e-181">Une nouvelle clé d’inscription du service s’affiche.</span><span class="sxs-lookup"><span data-stu-id="1de2e-181">A new service registration key will appear.</span></span>
   
    ![Confirmer la régénération de la clé](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="1de2e-183">Copiez cette clé et sauvegardez-la pour enregistrer tout nouvel appareil auprès de ce service.</span><span class="sxs-lookup"><span data-stu-id="1de2e-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1de2e-184">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1de2e-184">Next steps</span></span>
* <span data-ttu-id="1de2e-185">Découvrez comment [prendre en main](storsimple-virtual-array-deploy1-portal-prep.md) une solution StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="1de2e-185">Learn how to [get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="1de2e-186">Découvrez comment [gérer votre appareil StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="1de2e-186">Learn how to [administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

