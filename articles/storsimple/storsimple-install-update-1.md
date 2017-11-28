---
title: "aaaInstall 1.2 de mise à jour sur votre appareil StorSimple | Documents Microsoft"
description: "Explique comment tooinstall StorSimple 8000 Series Update 1.2 sur votre appareil de série StorSimple 8000."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 7a513923-eb77-4078-b0ab-f8e90183796a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0a7601dc0b1ce60eb854227243ecb02d6fb2c678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-12-on-your-storsimple-8000-series-device"></a><span data-ttu-id="c8ad2-103">Installer Update 1.2 sur votre appareil StorSimple série 8000</span><span class="sxs-lookup"><span data-stu-id="c8ad2-103">Install Update 1.2 on your StorSimple 8000 series device</span></span>
## <a name="overview"></a><span data-ttu-id="c8ad2-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c8ad2-104">Overview</span></span>
<span data-ttu-id="c8ad2-105">Ce didacticiel explique comment tooinstall mettre à jour 1.2 sur un appareil StorSimple qui s’exécute une version de logiciel préalable tooUpdate 1.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-105">This tutorial explains how tooinstall Update 1.2 on a StorSimple device that is running a software version prior tooUpdate 1.</span></span> <span data-ttu-id="c8ad2-106">didacticiel de Hello couvre également les étapes supplémentaires hello requis pour la mise à jour hello lorsqu’une passerelle est configurée sur une interface réseau autres que DATA 0 de l’appareil StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-106">hello tutorial also covers hello additional steps required for hello update when a gateway is configured on a network interface other than DATA 0 of hello StorSimple device.</span></span>

<span data-ttu-id="c8ad2-107">Update 1.2 comprend des mises à jour logicielles de l’appareil, des mises à jour du pilote LSI et des mises à jour du microprogramme de disque.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-107">Update 1.2 includes device software updates, LSI driver updates and disk firmware updates.</span></span> <span data-ttu-id="c8ad2-108">Bonjour logiciels et mises à jour du pilote LSI sont mises à jour sans interruption de service et peuvent être appliquées via hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-108">hello software and LSI driver updates are non-disruptive updates and can be applied via hello Azure classic portal.</span></span> <span data-ttu-id="c8ad2-109">mises à jour de microprogramme de disque Hello mises à jour et ne peuvent être appliqués via l’interface Windows PowerShell de hello du périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-109">hello disk firmware updates are disruptive updates and can only be applied via hello Windows PowerShell interface of hello device.</span></span>

<span data-ttu-id="c8ad2-110">Selon la version en cours d’exécution sur votre appareil, vous pouvez déterminer si Update 1.2 sera appliqué.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-110">Depending upon which version your device is running, you can determine if Update 1.2 will be applied.</span></span> <span data-ttu-id="c8ad2-111">Vous pouvez vérifier la version du logiciel hello de votre appareil en accédant toohello **coup de œil rapide** section de votre appareil **tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-111">You can check hello software version of your device by navigating toohello **quick glance** section of your device **Dashboard**.</span></span>

</br>

| <span data-ttu-id="c8ad2-112">Si vous exécutez la version logicielle…</span><span class="sxs-lookup"><span data-stu-id="c8ad2-112">If running software version …</span></span> | <span data-ttu-id="c8ad2-113">Que se passe-t-il dans le portail de hello ?</span><span class="sxs-lookup"><span data-stu-id="c8ad2-113">What happens in hello portal?</span></span> |
| --- | --- |
| <span data-ttu-id="c8ad2-114">Version commerciale - GA</span><span class="sxs-lookup"><span data-stu-id="c8ad2-114">Release - GA</span></span> |<span data-ttu-id="c8ad2-115">Si vous exécutez la version commerciale (GA), n’appliquez pas cette mise à jour.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-115">If you are running Release version (GA), do not apply this update.</span></span> <span data-ttu-id="c8ad2-116">Veuillez [contactez le Support Microsoft](storsimple-contact-microsoft-support.md) tooupdate votre appareil.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-116">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) tooupdate your device.</span></span> |
| <span data-ttu-id="c8ad2-117">Update 0.1</span><span class="sxs-lookup"><span data-stu-id="c8ad2-117">Update 0.1</span></span> |<span data-ttu-id="c8ad2-118">Le portail applique Update 1.2.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-118">Portal applies Update 1.2.</span></span> |
| <span data-ttu-id="c8ad2-119">Update 0.2</span><span class="sxs-lookup"><span data-stu-id="c8ad2-119">Update 0.2</span></span> |<span data-ttu-id="c8ad2-120">Le portail applique Update 1.2.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-120">Portal applies Update 1.2.</span></span> |
| <span data-ttu-id="c8ad2-121">Update 0.3</span><span class="sxs-lookup"><span data-stu-id="c8ad2-121">Update 0.3</span></span> |<span data-ttu-id="c8ad2-122">Le portail applique Update 1.2.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-122">Portal applies Update 1.2.</span></span> |
| <span data-ttu-id="c8ad2-123">Update 1</span><span class="sxs-lookup"><span data-stu-id="c8ad2-123">Update 1</span></span> |<span data-ttu-id="c8ad2-124">Cette mise à jour ne sera pas disponible.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-124">This update will not be available.</span></span> |
| <span data-ttu-id="c8ad2-125">Update 1.1</span><span class="sxs-lookup"><span data-stu-id="c8ad2-125">Update 1.1</span></span> |<span data-ttu-id="c8ad2-126">Cette mise à jour ne sera pas disponible.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-126">This update will not be available.</span></span> |

</br>

> [!IMPORTANT]
> * <span data-ttu-id="c8ad2-127">Vous ne pouvez pas voir 1.2 de mise à jour immédiatement, car nous effectuer un déploiement échelonné des mises à jour hello.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-127">You may not see Update 1.2 immediately because we do a phased rollout of hello updates.</span></span> <span data-ttu-id="c8ad2-128">Revérifiez les mises à jour dans quelques jours, car celle-ci sera bientôt disponible.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-128">Scan for updates in a few days again as this Update will become available soon.</span></span>
> * <span data-ttu-id="c8ad2-129">Cette mise à jour comprend un ensemble de l’intégrité du manuel et automatique des vérifications préalables toodetermine hello périphérique en termes de matériel état et la connectivité réseau.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-129">This update includes a set of manual and automatic pre-checks toodetermine hello device health in terms of hardware state and network connectivity.</span></span> <span data-ttu-id="c8ad2-130">Ces vérifications préalables sont effectuées uniquement si vous appliquez des mises à jour hello de hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-130">These pre-checks are performed only if you apply hello updates from hello Azure classic portal.</span></span>
> * <span data-ttu-id="c8ad2-131">Nous recommandons que vous installez le logiciel de hello et mises à jour du pilote via hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-131">We recommend that you install hello software and driver updates via hello Azure classic portal.</span></span> <span data-ttu-id="c8ad2-132">Vous ne devez pas dépasser interface Windows PowerShell de toohello de l’appareil hello (tooinstall les mises à jour) en cas de vérification de mise à jour préalable passerelle hello dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-132">You should only go toohello Windows PowerShell interface of hello device (tooinstall updates) if hello pre-update gateway check fails in hello portal.</span></span> <span data-ttu-id="c8ad2-133">mises à jour Hello peuvent prendre tooinstall 5 à 10 heures (y compris les mises à jour Windows de hello).</span><span class="sxs-lookup"><span data-stu-id="c8ad2-133">hello updates may take 5-10 hours tooinstall (including hello Windows Updates).</span></span> <span data-ttu-id="c8ad2-134">mises à jour de mode de maintenance Hello doivent être installés via l’interface Windows PowerShell de hello du périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-134">hello maintenance mode updates must be installed via hello Windows PowerShell interface of hello device.</span></span> <span data-ttu-id="c8ad2-135">Les mises à jour du mode de maintenance étant des mises à jour perturbatrices, elles entraînent un temps d’arrêt pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-135">As maintenance mode updates are disruptive updates, these will result in a down time for your device.</span></span>
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-12-via-hello-azure-classic-portal"></a><span data-ttu-id="c8ad2-136">Installer 1.2 de mise à jour via hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="c8ad2-136">Install Update 1.2 via hello Azure classic portal</span></span>
<span data-ttu-id="c8ad2-137">Effectuer, hello suivant les étapes tooupdate votre appareil trop[mise à jour 1.2](storsimple-update1-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="c8ad2-137">Perform hello following steps tooupdate your device too[Update 1.2](storsimple-update1-release-notes.md).</span></span> <span data-ttu-id="c8ad2-138">Utilisez cette procédure uniquement si vous disposez d’une passerelle configurée sur l’interface réseau DATA 0 de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-138">Use this procedure only if you have a gateway configured on DATA 0 network interface on your device.</span></span>

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. <span data-ttu-id="c8ad2-139">Vérifiez que votre appareil exécute **StorSimple 8000 Series Update 1.2 (6.3.9600.17584)**.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-139">Verify that your device is running **StorSimple 8000 Series Update 1.2 (6.3.9600.17584)**.</span></span> <span data-ttu-id="c8ad2-140">Hello **dernière date de mise à jour** doit également être modifié.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-140">hello **Last updated date** should also be modified.</span></span> <span data-ttu-id="c8ad2-141">Vous verrez également que les mises à jour du mode de Maintenance sont disponibles (ce message peut continuer toobe affiché pour des too24 heures après l’installation de hello mises à jour).</span><span class="sxs-lookup"><span data-stu-id="c8ad2-141">You'll also see that Maintenance mode updates are available (this message might continue toobe displayed for up too24 hours after you install hello updates).</span></span>
   
   <span data-ttu-id="c8ad2-142">Mises à jour du mode de maintenance sont mises à jour qui entraîne un temps d’arrêt de l’appareil et ne peuvent être appliqués via l’interface Windows PowerShell de hello de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-142">Maintenance mode updates are disruptive updates that result in device downtime and can only be applied via hello Windows PowerShell interface of your device.</span></span>
   
   <span data-ttu-id="c8ad2-143">![Page Maintenance](./media/storsimple-install-update-1/InstallUpdate12_10M.png "Page Maintenance")</span><span class="sxs-lookup"><span data-stu-id="c8ad2-143">![Maintenance page](./media/storsimple-install-update-1/InstallUpdate12_10M.png "Maintenance page")</span></span>
2. <span data-ttu-id="c8ad2-144">Télécharger des mises à jour de mode de maintenance hello à l’aide des étapes hello répertoriées dans [toodownload correctifs](#to-download-hotfixes) toosearch pour et télécharger KB3063416, qui installe les mises à jour du microprogramme de disque (hello autres mises à jour doivent déjà être installés à ce stade).</span><span class="sxs-lookup"><span data-stu-id="c8ad2-144">Download hello maintenance mode updates by using hello steps listed in [toodownload hotfixes](#to-download-hotfixes) toosearch for and download KB3063416, which installs disk firmware updates (hello other updates should already be installed by now).</span></span>
3. <span data-ttu-id="c8ad2-145">Suivez les étapes de hello répertoriées dans [installer et vérifier les correctifs en mode de maintenance](#to-install-and-verify-maintenance-mode-hotfixes) mises à jour du mode maintenance tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-145">Follow hello steps listed in [Install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello maintenance mode updates.</span></span>
4. <span data-ttu-id="c8ad2-146">Dans l’hello portail Azure classic, accédez toohello **Maintenance** page et en bas de hello de page de hello, cliquez sur **d’analyse des mises à jour** toocheck pour toutes les mises à jour Windows puis cliquez sur **installer les mises à jour** .</span><span class="sxs-lookup"><span data-stu-id="c8ad2-146">In hello Azure classic portal, navigate toohello **Maintenance** page and at hello bottom of hello page, click **Scan Updates** toocheck for any Windows Updates and then click **Install Updates**.</span></span> <span data-ttu-id="c8ad2-147">Vous avez terminé une fois toutes les Hello mises à jour sont correctement installés.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-147">You're finished after all of hello updates are successfully installed.</span></span>

## <a name="install-update-12-on-a-device-that-has-a-gateway-configured-for-a-non-data-0-network-interface"></a><span data-ttu-id="c8ad2-148">Installation d’Update 1.2 sur un appareil présentant une passerelle configurée pour une interface réseau différente de DATA 0.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-148">Install Update 1.2 on a device that has a gateway configured for a non-DATA 0 network interface</span></span>
<span data-ttu-id="c8ad2-149">Vous devez utiliser cette procédure uniquement si vous ne parvenez pas à cocher de passerelle hello lors de la tentative de mises à jour de tooinstall hello hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-149">You should use this procedure only if you fail hello gateway check when trying tooinstall hello updates through hello Azure classic portal.</span></span> <span data-ttu-id="c8ad2-150">la vérification de Hello échoue car vous disposez d’une passerelle affectée tooa non-interface réseau DATA 0 et votre appareil exécute une version de logiciel préalable tooUpdate 1.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-150">hello check fails as you have a gateway assigned tooa non-DATA 0 network interface and your device is running a software version prior tooUpdate 1.</span></span> <span data-ttu-id="c8ad2-151">Si votre appareil ne dispose pas d’une passerelle sur une non-interface réseau DATA 0, vous pouvez mettre à jour votre appareil directement à partir de hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-151">If your device does not have a gateway on a non-DATA 0 network interface, you can update your device directly from hello Azure classic portal.</span></span> <span data-ttu-id="c8ad2-152">Consultez [installation mise à jour 1.2 via hello portail Azure classic](#install-update-1.2-via-the-azure-classic-portal).</span><span class="sxs-lookup"><span data-stu-id="c8ad2-152">See [Install update 1.2 via hello Azure classic portal](#install-update-1.2-via-the-azure-classic-portal).</span></span>

<span data-ttu-id="c8ad2-153">versions logicielles Hello pouvant être mis à niveau à l’aide de cette méthode sont mise à jour 0.1, mise à jour 0,2 et mise à jour 0.3.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-153">hello software versions that can be upgraded using this method are Update 0.1, Update 0.2, and Update 0.3.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="c8ad2-154">Si votre appareil exécute la version de la mise en production (GA), veuillez contacter [Support technique de Microsoft](storsimple-contact-microsoft-support.md) tooassist avec hello mise à jour.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-154">If your device is running Release (GA) version, please contact [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist you with hello update.</span></span>
> * <span data-ttu-id="c8ad2-155">Cette toobe de besoins procédure exécutée une seule fois tooapply 1.2 de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-155">This procedure needs toobe performed only once tooapply Update 1.2.</span></span> <span data-ttu-id="c8ad2-156">Vous pouvez utiliser les mises à jour ultérieures de hello tooapply de portail classique Azure.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-156">You can use hello Azure classic portal tooapply subsequent updates.</span></span>
> 
> 

<span data-ttu-id="c8ad2-157">Si votre appareil est en cours d’exécution avant mise à jour des 1 logiciels et a une passerelle définie pour une interface réseau autres que DATA 0, vous pouvez appliquer 1.2 de mise à jour de hello deux façons suivantes :</span><span class="sxs-lookup"><span data-stu-id="c8ad2-157">If your device is running pre-Update 1 software and it has a gateway set for a network interface other than DATA 0, you can apply Update 1.2 in hello following two ways:</span></span>

* <span data-ttu-id="c8ad2-158">**Option 1**: télécharger la mise à jour hello et l’appliquer à l’aide de hello `Start-HcsHotfix` applet de commande à partir de l’interface Windows PowerShell de hello du périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-158">**Option 1**: Download hello update and apply it by using hello `Start-HcsHotfix` cmdlet from hello Windows PowerShell interface of hello device.</span></span> <span data-ttu-id="c8ad2-159">Il s’agit de méthode recommandée de hello.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-159">This is hello recommended method.</span></span> <span data-ttu-id="c8ad2-160">**Si votre appareil exécute la mise à jour 1.0 ou 1.1 de la mise à jour, n’utilisez pas cette méthode de tooapply 1.2 de mise à jour.**</span><span class="sxs-lookup"><span data-stu-id="c8ad2-160">**Do not use this method tooapply Update 1.2 if your device is running Update 1.0 or Update 1.1.**</span></span>
* <span data-ttu-id="c8ad2-161">**Option 2**: configuration de la passerelle Remove hello et installation Bonjour mettre à jour directement à partir de hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-161">**Option 2**: Remove hello gateway configuration and install hello update directly from hello Azure classic portal.</span></span>

<span data-ttu-id="c8ad2-162">Instructions détaillées pour chacun d’eux sont fournies dans les sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-162">Detailed instructions for each of these are provided in hello following sections.</span></span>

## <a name="option-1-use-windows-powershell-for-storsimple-tooapply-update-12-as-a-hotfix"></a><span data-ttu-id="c8ad2-163">Option 1 : Utiliser Windows PowerShell pour StorSimple tooapply 1.2 de mise à jour en tant que correctif</span><span class="sxs-lookup"><span data-stu-id="c8ad2-163">Option 1: Use Windows PowerShell for StorSimple tooapply Update 1.2 as a hotfix</span></span>
<span data-ttu-id="c8ad2-164">Vous devez utiliser cette procédure uniquement si vous exécutez la mise à jour 0.1, 0,2, 0,3 et si votre vérification de la passerelle a échoué lors de la tentative de mises à jour tooinstall hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-164">You should use this procedure only if you are running Update 0.1, 0.2, 0.3 and if your gateway check has failed when trying tooinstall updates from hello Azure classic portal.</span></span> <span data-ttu-id="c8ad2-165">Si vous exécutez un logiciel de mise en production (GA), veuillez [Support technique de Microsoft](storsimple-contact-microsoft-support.md) tooupdate votre appareil.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-165">If you are running Release (GA) software, please [Microsoft Support](storsimple-contact-microsoft-support.md) tooupdate your device.</span></span>

<span data-ttu-id="c8ad2-166">tooinstall 1.2 de mise à jour en tant qu’un correctif logiciel, vous devez télécharger et installer hello suivant les correctifs logiciels :</span><span class="sxs-lookup"><span data-stu-id="c8ad2-166">tooinstall Update 1.2 as a hotfix, you must download and install hello following hotfixes:</span></span>

| <span data-ttu-id="c8ad2-167">Ordre</span><span class="sxs-lookup"><span data-stu-id="c8ad2-167">Order</span></span> | <span data-ttu-id="c8ad2-168">Ko</span><span class="sxs-lookup"><span data-stu-id="c8ad2-168">KB</span></span> | <span data-ttu-id="c8ad2-169">Description</span><span class="sxs-lookup"><span data-stu-id="c8ad2-169">Description</span></span> | <span data-ttu-id="c8ad2-170">Type de mise à jour</span><span class="sxs-lookup"><span data-stu-id="c8ad2-170">Update type</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c8ad2-171">1</span><span class="sxs-lookup"><span data-stu-id="c8ad2-171">1</span></span> |<span data-ttu-id="c8ad2-172">KB3063418</span><span class="sxs-lookup"><span data-stu-id="c8ad2-172">KB3063418</span></span> |<span data-ttu-id="c8ad2-173">Mise à jour logicielle</span><span class="sxs-lookup"><span data-stu-id="c8ad2-173">Software update</span></span> |<span data-ttu-id="c8ad2-174">Normal</span><span class="sxs-lookup"><span data-stu-id="c8ad2-174">Regular</span></span> |
| <span data-ttu-id="c8ad2-175">2</span><span class="sxs-lookup"><span data-stu-id="c8ad2-175">2</span></span> |<span data-ttu-id="c8ad2-176">KB3043005</span><span class="sxs-lookup"><span data-stu-id="c8ad2-176">KB3043005</span></span> |<span data-ttu-id="c8ad2-177">Mise à jour du contrôleur SAS LSI</span><span class="sxs-lookup"><span data-stu-id="c8ad2-177">LSI SAS controller update</span></span> |<span data-ttu-id="c8ad2-178">Normal</span><span class="sxs-lookup"><span data-stu-id="c8ad2-178">Regular</span></span> |
| <span data-ttu-id="c8ad2-179">3</span><span class="sxs-lookup"><span data-stu-id="c8ad2-179">3</span></span> |<span data-ttu-id="c8ad2-180">KB3063416</span><span class="sxs-lookup"><span data-stu-id="c8ad2-180">KB3063416</span></span> |<span data-ttu-id="c8ad2-181">Microprogramme de disque</span><span class="sxs-lookup"><span data-stu-id="c8ad2-181">Disk firmware</span></span> |<span data-ttu-id="c8ad2-182">Maintenance </span><span class="sxs-lookup"><span data-stu-id="c8ad2-182">Maintenance</span></span> |

<span data-ttu-id="c8ad2-183">Avant d’utiliser cette hello tooapply de procédure mise à jour, assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="c8ad2-183">Before using this procedure tooapply hello update, make sure that:</span></span>

* <span data-ttu-id="c8ad2-184">Les deux contrôleurs d’appareil sont en ligne.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-184">Both device controllers are online.</span></span>

<span data-ttu-id="c8ad2-185">Effectuer hello suivant les étapes tooapply 1.2 de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-185">Perform hello following steps tooapply Update 1.2.</span></span> <span data-ttu-id="c8ad2-186">**mises à jour Hello peut prendre environ 2 heures toocomplete (environ 30 minutes pour les logiciels, 30 minutes pour pilote, 45 minutes pour le microprogramme du disque).**</span><span class="sxs-lookup"><span data-stu-id="c8ad2-186">**hello updates could take around 2 hours toocomplete (approximately 30 minutes for software, 30 minutes for driver, 45 minutes for disk firmware).**</span></span>

[!INCLUDE [storsimple-install-update-option1](../../includes/storsimple-install-update-option1.md)]

## <a name="option-2-use-hello-azure-classic-portal-tooapply-update-12-after-removing-hello-gateway-configuration"></a><span data-ttu-id="c8ad2-187">Option 2 : Utiliser hello tooapply portail classique Azure 1.2 de mise à jour après la suppression de configuration de la passerelle hello</span><span class="sxs-lookup"><span data-stu-id="c8ad2-187">Option 2: Use hello Azure classic portal tooapply Update 1.2 after removing hello gateway configuration</span></span>
<span data-ttu-id="c8ad2-188">Cette procédure s’applique uniquement les appareils tooStorSimple qui exécutent une version de logiciel préalable tooUpdate 1 et ont une passerelle définie sur une interface réseau autres que DATA 0.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-188">This procedure applies only tooStorSimple devices that are running a software version prior tooUpdate 1 and have a gateway set on a network interface other than DATA 0.</span></span> <span data-ttu-id="c8ad2-189">Vous aurez besoin de mise à jour tooclear hello passerelle paramètre tooapplying préalable hello.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-189">You will need tooclear hello gateway setting prior tooapplying hello update.</span></span>

<span data-ttu-id="c8ad2-190">mise à jour Hello peut prendre quelques heures toocomplete.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-190">hello update may take a few hours toocomplete.</span></span> <span data-ttu-id="c8ad2-191">Si vos ordinateurs hôtes se trouvent dans des sous-réseaux différents, suppression de la configuration de passerelle hello sur des interfaces hello iSCSI peut entraîner un temps d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-191">If your hosts are in different subnets, removing hello gateway configuration on hello iSCSI interfaces could result in downtime.</span></span> <span data-ttu-id="c8ad2-192">Nous vous recommandons de configurer DATA 0 pour les temps d’arrêt du hello tooreduce le trafic iSCSI.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-192">We recommend that you configure DATA 0 for iSCSI traffic tooreduce hello downtime.</span></span>

<span data-ttu-id="c8ad2-193">Effectuer hello suivant l’interface de réseau étapes toodisable hello avec la passerelle de hello, puis appliquez la mise à jour de hello.</span><span class="sxs-lookup"><span data-stu-id="c8ad2-193">Perform hello following steps toodisable hello network interface with hello gateway and then apply hello update.</span></span>

[!INCLUDE [storsimple-install-update-option2](../../includes/storsimple-install-update-option2.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a><span data-ttu-id="c8ad2-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c8ad2-194">Next steps</span></span>
<span data-ttu-id="c8ad2-195">En savoir plus sur hello [version de mise à jour 1.2](storsimple-update1-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="c8ad2-195">Learn more about hello [Update 1.2 release](storsimple-update1-release-notes.md).</span></span>
