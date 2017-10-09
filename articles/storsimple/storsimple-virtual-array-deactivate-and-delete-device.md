---
title: "aaaDeactivate et supprimer une unité de stockage de Microsoft Azure StorSimple virtuelle | Documents Microsoft"
description: "Décrit comment l’appareil StorSimple tooremove service en désactiver tout d’abord, puis leur suppression."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a><span data-ttu-id="70a10-103">Désactiver et supprimer un StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="70a10-103">Deactivate and delete a StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="70a10-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="70a10-104">Overview</span></span>

<span data-ttu-id="70a10-105">Lorsque vous désactivez un StorSimple Virtual Array, vous rompez connexion hello entre l’appareil de hello et le service de gestionnaire de périphériques StorSimple hello correspondant.</span><span class="sxs-lookup"><span data-stu-id="70a10-105">When you deactivate a StorSimple Virtual Array, you break hello connection between hello device and hello corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="70a10-106">Ce didacticiel explique comment :</span><span class="sxs-lookup"><span data-stu-id="70a10-106">This tutorial explains how to:</span></span>

* <span data-ttu-id="70a10-107">Désactiver un appareil</span><span class="sxs-lookup"><span data-stu-id="70a10-107">Deactivate a device</span></span> 
* <span data-ttu-id="70a10-108">Supprimer un appareil désactivé</span><span class="sxs-lookup"><span data-stu-id="70a10-108">Delete a deactivated device</span></span>

<span data-ttu-id="70a10-109">les informations de Hello dans cet article s’appliquent tooStorSimple tableaux virtuels uniquement.</span><span class="sxs-lookup"><span data-stu-id="70a10-109">hello information in this article applies tooStorSimple Virtual Arrays only.</span></span> <span data-ttu-id="70a10-110">Pour plus d’informations sur la 8000 série, accédez toohow trop[désactiver ou supprimer un périphérique](storsimple-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="70a10-110">For information on 8000 series, go toohow too[deactivate or delete a device](storsimple-deactivate-and-delete-device.md).</span></span>

## <a name="when-toodeactivate"></a><span data-ttu-id="70a10-111">Lorsque toodeactivate ?</span><span class="sxs-lookup"><span data-stu-id="70a10-111">When toodeactivate?</span></span>

<span data-ttu-id="70a10-112">La désactivation est une opération DÉFINITIVE et ne peut pas être annulée.</span><span class="sxs-lookup"><span data-stu-id="70a10-112">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="70a10-113">Vous ne peut pas inscrire un appareil désactivé avec hello service du Gestionnaire de périphériques StorSimple à nouveau.</span><span class="sxs-lookup"><span data-stu-id="70a10-113">You cannot register a deactivated device with hello StorSimple Device Manager service again.</span></span> <span data-ttu-id="70a10-114">Vous pouvez peut-être toodeactivate et supprimer un groupe virtuel StorSimple Bonjour les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="70a10-114">You may need toodeactivate and delete a StorSimple Virtual Array in hello following scenarios:</span></span>

* <span data-ttu-id="70a10-115">**Le basculement planifié** : votre appareil est en ligne et que vous envisagez toofail sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="70a10-115">**Planned failover** : Your device is online and you plan toofail over your device.</span></span> <span data-ttu-id="70a10-116">Si vous envisagez de périphérique de tooupgrade tooa plus important, vous devrez peut-être toofail sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="70a10-116">If you are planning tooupgrade tooa larger device, you may need toofail over your device.</span></span> <span data-ttu-id="70a10-117">Une fois que la propriété des données hello est transférée et hello de basculement est terminé, hello source appareil est automatiquement supprimé.</span><span class="sxs-lookup"><span data-stu-id="70a10-117">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="70a10-118">**Basculement non planifié** : votre appareil est hors connexion et que vous devez toofail via un périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="70a10-118">**Unplanned failover** : Your device is offline and you need toofail over hello device.</span></span> <span data-ttu-id="70a10-119">Ce scénario peut se produire lors d’un incident lorsqu’il existe une panne dans le centre de données hello et votre appareil principal est arrêté.</span><span class="sxs-lookup"><span data-stu-id="70a10-119">This scenario may occur during a disaster when there is an outage in hello datacenter and your primary device is down.</span></span> <span data-ttu-id="70a10-120">Vous envisagez de toofail sur hello tooa secondaire un périphérique.</span><span class="sxs-lookup"><span data-stu-id="70a10-120">You plan toofail over hello device tooa secondary device.</span></span> <span data-ttu-id="70a10-121">Une fois que la propriété des données hello est transférée et hello de basculement est terminé, hello source appareil est automatiquement supprimé.</span><span class="sxs-lookup"><span data-stu-id="70a10-121">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="70a10-122">**Mettre hors service** : vous voulez toodecommission hello périphérique.</span><span class="sxs-lookup"><span data-stu-id="70a10-122">**Decommission** : You want toodecommission hello device.</span></span> <span data-ttu-id="70a10-123">Vous devez toofirst désactiver hello appareil, puis supprimez-le.</span><span class="sxs-lookup"><span data-stu-id="70a10-123">This requires you toofirst deactivate hello device and then delete it.</span></span> <span data-ttu-id="70a10-124">Si vous désactivez un appareil, il n’est plus possible d’accéder aux données stockées en local.</span><span class="sxs-lookup"><span data-stu-id="70a10-124">When you deactivate a device, you can no longer access any data that is stored locally.</span></span> <span data-ttu-id="70a10-125">Vous pouvez uniquement l’accès et restauration hello des données stockées dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="70a10-125">You can only access and recover hello data stored in hello cloud.</span></span> <span data-ttu-id="70a10-126">Si vous envisagez de données de l’appareil tookeep hello après la désactivation, vous devez prendre un instantané cloud de toutes vos données avant de désactiver un périphérique.</span><span class="sxs-lookup"><span data-stu-id="70a10-126">If you plan tookeep hello device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="70a10-127">Cet instantané cloud vous permet de toorecover tous hello des données à un stade ultérieur.</span><span class="sxs-lookup"><span data-stu-id="70a10-127">This cloud snapshot allows you toorecover all hello data at a later stage.</span></span>

## <a name="deactivate-a-device"></a><span data-ttu-id="70a10-128">Désactiver un appareil</span><span class="sxs-lookup"><span data-stu-id="70a10-128">Deactivate a device</span></span>

<span data-ttu-id="70a10-129">toodeactivate votre appareil, effectuer hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="70a10-129">toodeactivate your device, perform hello following steps.</span></span>

#### <a name="toodeactivate-hello-device"></a><span data-ttu-id="70a10-130">Appareil de hello toodeactivate</span><span class="sxs-lookup"><span data-stu-id="70a10-130">toodeactivate hello device</span></span>

1. <span data-ttu-id="70a10-131">Dans votre service, passez trop**Gestion > appareils**.</span><span class="sxs-lookup"><span data-stu-id="70a10-131">In your service, go too**Management > Devices**.</span></span> <span data-ttu-id="70a10-132">Bonjour **périphériques** panneau, cliquez sur Sélectionnez hello périphériques et que vous souhaitez toodeactivate.</span><span class="sxs-lookup"><span data-stu-id="70a10-132">In hello **Devices** blade, click and select hello device that you wish toodeactivate.</span></span>
   
    ![Sélectionnez le périphérique toodeactivate](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. <span data-ttu-id="70a10-134">Dans votre **tableau de bord périphérique** panneau, cliquez sur **... Plus** et dans la liste hello, sélectionnez **Deactivate**.</span><span class="sxs-lookup"><span data-stu-id="70a10-134">In your **Device dashboard** blade, click **… More** and from hello list, select **Deactivate**.</span></span>
   
    ![Clic sur Désactiver](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. <span data-ttu-id="70a10-136">Bonjour **Deactivate** panneau, le nom de périphérique de type hello et puis cliquez sur **Deactivate**.</span><span class="sxs-lookup"><span data-stu-id="70a10-136">In hello **Deactivate** blade, type hello device name and then click **Deactivate**.</span></span> 
   
    ![Confirmation de la désactivation](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    <span data-ttu-id="70a10-138">Hello désactiver le processus démarre et prend quelques minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="70a10-138">hello deactivate process starts and takes a few minutes toocomplete.</span></span>
   
    ![Désactivation en cours](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. <span data-ttu-id="70a10-140">Après la désactivation, la liste des appareils hello actualise.</span><span class="sxs-lookup"><span data-stu-id="70a10-140">After deactivation, hello list of devices refreshes.</span></span>
   
    ![Désactivation terminée](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    <span data-ttu-id="70a10-142">Vous pouvez maintenant supprimer cet appareil.</span><span class="sxs-lookup"><span data-stu-id="70a10-142">You can now delete this device.</span></span>

## <a name="delete-hello-device"></a><span data-ttu-id="70a10-143">Supprimer l’appareil de hello</span><span class="sxs-lookup"><span data-stu-id="70a10-143">Delete hello device</span></span>

<span data-ttu-id="70a10-144">Un périphérique a toodelete de désactivés premier toobe il.</span><span class="sxs-lookup"><span data-stu-id="70a10-144">A device has toobe first deactivated toodelete it.</span></span> <span data-ttu-id="70a10-145">Suppression d’un appareil supprime de la liste hello des périphériques connectés toohello service.</span><span class="sxs-lookup"><span data-stu-id="70a10-145">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="70a10-146">service de Hello puis ne peut plus gérer les appareils hello supprimé.</span><span class="sxs-lookup"><span data-stu-id="70a10-146">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="70a10-147">données Hello associées hello appareil restent cependant dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="70a10-147">hello data associated with hello device however remains in hello cloud.</span></span> <span data-ttu-id="70a10-148">Ensuite, les frais associés aux données s’accumulent.</span><span class="sxs-lookup"><span data-stu-id="70a10-148">This data then accrues charges.</span></span>

<span data-ttu-id="70a10-149">Appareil de hello toodelete, effectuer hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="70a10-149">toodelete hello device, perform hello following steps.</span></span>

#### <a name="toodelete-hello-device"></a><span data-ttu-id="70a10-150">Appareil de hello toodelete</span><span class="sxs-lookup"><span data-stu-id="70a10-150">toodelete hello device</span></span>

1. <span data-ttu-id="70a10-151">Dans le Gestionnaire de périphériques StorSimple, accédez trop**Gestion > appareils**.</span><span class="sxs-lookup"><span data-stu-id="70a10-151">In your StorSimple Device Manager, go too**Management > Devices**.</span></span> <span data-ttu-id="70a10-152">Bonjour **périphériques** panneau, sélectionnez un appareil désactivé que vous souhaitez toodelete.</span><span class="sxs-lookup"><span data-stu-id="70a10-152">In hello **Devices** blade, select a deactivated device that you wish toodelete.</span></span>
2. <span data-ttu-id="70a10-153">Bonjour **tableau de bord périphérique** panneau, cliquez sur **... Plus** puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="70a10-153">In hello **Device dashboard** blade, click **… More** and then click **Delete**.</span></span>
   
   ![Sélectionnez le périphérique toodelete](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. <span data-ttu-id="70a10-155">Bonjour **supprimer** panneau, entrez un nom hello de suppression d’un périphérique tooconfirm hello votre puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="70a10-155">In hello **Delete** blade, type hello name of your device tooconfirm hello deletion and then click **Delete**.</span></span> <span data-ttu-id="70a10-156">Appareil de hello suppression ne supprime pas les données de cloud de hello associées hello périphérique.</span><span class="sxs-lookup"><span data-stu-id="70a10-156">Deleting hello device does not delete hello cloud data associated with hello device.</span></span> 
   
   ![Confirmation de suppression](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. <span data-ttu-id="70a10-158">suppression de Hello démarre et prend quelques minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="70a10-158">hello deletion starts and takes a few minutes toocomplete.</span></span>
   
   ![Suppression en cours](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    <span data-ttu-id="70a10-160">Après la suppression des appareils de hello, vous pouvez afficher la liste des appareils hello mis à jour.</span><span class="sxs-lookup"><span data-stu-id="70a10-160">After hello device is deleted, you can view hello updated list of devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70a10-161">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="70a10-161">Next steps</span></span>

* <span data-ttu-id="70a10-162">Pour plus d’informations sur la façon de toofail, accédez trop[basculement et récupération d’urgence de votre tableau virtuel StorSimple](storsimple-virtual-array-failover-dr.md).</span><span class="sxs-lookup"><span data-stu-id="70a10-162">For information on how toofail over, go too[Failover and disaster recovery of your StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md).</span></span>

* <span data-ttu-id="70a10-163">toolearn savoir plus sur comment toouse hello service du Gestionnaire de périphériques StorSimple, accédez trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="70a10-163">toolearn more about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span> 

