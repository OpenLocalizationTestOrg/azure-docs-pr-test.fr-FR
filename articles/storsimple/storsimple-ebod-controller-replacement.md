---
title: "Remplacer un contrôleur EBOD StorSimple | Microsoft Docs"
description: "Explique comment retirer et remplacer un contrôleur ou les deux contrôleurs EBOD sur votre appareil StorSimple 8600."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8cbfa507-1a56-4e24-99dd-7db9abd3b850
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 23d819ddc3bbcbaf2847cdcc9191407ead0ff43d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="5dc9f-103">Remplacer un contrôleur EBOD sur votre appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="5dc9f-103">Replace an EBOD controller on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="5dc9f-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="5dc9f-104">Overview</span></span>
<span data-ttu-id="5dc9f-105">Ce didacticiel explique comment remplacer un module de contrôleur EBOD défectueux sur votre appareil Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-105">This tutorial explains how to replace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="5dc9f-106">Pour remplacer un module de contrôleur EBOD, vous devez :</span><span class="sxs-lookup"><span data-stu-id="5dc9f-106">To replace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="5dc9f-107">Retirer le contrôleur EBOD défectueux</span><span class="sxs-lookup"><span data-stu-id="5dc9f-107">Remove the faulty EBOD controller</span></span>
* <span data-ttu-id="5dc9f-108">Installer un nouveau contrôleur EBOD</span><span class="sxs-lookup"><span data-stu-id="5dc9f-108">Install a new EBOD controller</span></span>

<span data-ttu-id="5dc9f-109">Avant de commencer, tenez compte des informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="5dc9f-109">Consider the following information before you begin:</span></span>

* <span data-ttu-id="5dc9f-110">Des modules EBOD vides doivent être insérés dans tous les emplacements non utilisés.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="5dc9f-111">Le boîtier ne se refroidit pas correctement si un emplacement est laissé ouvert.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-111">The enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="5dc9f-112">Le contrôleur EBOD est échangeable à chaud, et il peut être retiré ou remplacé.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-112">The EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="5dc9f-113">Ne retirez pas un module défectueux tant que vous ne disposez pas d’un remplacement.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="5dc9f-114">Quand vous commencez le processus de remplacement, vous devez le terminer dans les 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-114">When you initiate the replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5dc9f-115">Avant de tenter de retirer ou de remplacer un composant StorSimple, passez en revue les [conventions des icônes de sécurité](storsimple-safety.md#safety-icon-conventions) et les autres [précautions de sécurité](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="5dc9f-115">Before attempting to remove or replace any StorSimple component, make sure that you review the [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>
> 
> 

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="5dc9f-116">Retirer un contrôleur EBOD</span><span class="sxs-lookup"><span data-stu-id="5dc9f-116">Remove an EBOD controller</span></span>
<span data-ttu-id="5dc9f-117">Avant de retirer le module de contrôleur EBOD défectueux de votre appareil StorSimple, assurez-vous que l’autre module de contrôleur EBOD est actif et en fonctionnement.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-117">Before replacing the failed EBOD controller module in your StorSimple device, make sure that the other EBOD controller module is active and running.</span></span> <span data-ttu-id="5dc9f-118">La procédure et le tableau suivants expliquent comment retirer le module de contrôleur EBOD.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-118">The following procedure and table explain how to remove the EBOD controller module.</span></span>

#### <a name="to-remove-an-ebod-module"></a><span data-ttu-id="5dc9f-119">Pour retirer un module EBOD</span><span class="sxs-lookup"><span data-stu-id="5dc9f-119">To remove an EBOD module</span></span>
1. <span data-ttu-id="5dc9f-120">Ouvrez le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-120">Open the Azure classic portal.</span></span>
2. <span data-ttu-id="5dc9f-121">Accédez à **Appareils** > **Maintenance** > **Statut du matériel**, et vérifiez que l’état de la LED du module de contrôleur EBOD actif est en vert et que la LED pour le module de contrôleur EBOD défaillant est en rouge.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-121">Navigate to **Devices** > **Maintenance** > **Hardware Status**, and verify that the status of the LED for the active EBOD controller module is green and the LED for the failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="5dc9f-122">Localisez le module de contrôleur EBOD défectueux à l’arrière de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-122">Locate the failed EBOD controller module at the back of the device.</span></span>
4. <span data-ttu-id="5dc9f-123">Débranchez les câbles qui connectent le module de contrôleur EBOD au contrôleur avant d’enlever le module EBOD du système.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-123">Remove the cables that connect the EBOD controller module to the controller before taking the EBOD module out of the system.</span></span>
5. <span data-ttu-id="5dc9f-124">Notez le port SAS du module de contrôleur EBOD qui était connecté au contrôleur.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-124">Make a note of the exact SAS port of the EBOD controller module that was connected to the controller.</span></span> <span data-ttu-id="5dc9f-125">Vous devrez restaurer le système dans cette configuration après le remplacement du module EBOD.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-125">You will be required to restore the system to this configuration after you replace the EBOD module.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="5dc9f-126">En règle générale, il s’agit du Port A, qui est libellé **Entrée hôte** dans le diagramme suivant.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-126">Typically, this will be Port A, which is labeled as **Host in** in the following diagram.</span></span>
   > 
   > 
   
    ![Fond de panier du contrôleur EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="5dc9f-128">**Figure 1** : Arrière du module EBOD</span><span class="sxs-lookup"><span data-stu-id="5dc9f-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="5dc9f-129">Étiquette</span><span class="sxs-lookup"><span data-stu-id="5dc9f-129">Label</span></span> | <span data-ttu-id="5dc9f-130">Description</span><span class="sxs-lookup"><span data-stu-id="5dc9f-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="5dc9f-131">1</span><span class="sxs-lookup"><span data-stu-id="5dc9f-131">1</span></span> |<span data-ttu-id="5dc9f-132">LED indiquant une panne</span><span class="sxs-lookup"><span data-stu-id="5dc9f-132">Fault LED</span></span> |
   | <span data-ttu-id="5dc9f-133">2</span><span class="sxs-lookup"><span data-stu-id="5dc9f-133">2</span></span> |<span data-ttu-id="5dc9f-134">LED d’alimentation</span><span class="sxs-lookup"><span data-stu-id="5dc9f-134">Power LED</span></span> |
   | <span data-ttu-id="5dc9f-135">3</span><span class="sxs-lookup"><span data-stu-id="5dc9f-135">3</span></span> |<span data-ttu-id="5dc9f-136">Connecteurs SaaS</span><span class="sxs-lookup"><span data-stu-id="5dc9f-136">SAS connectors</span></span> |
   | <span data-ttu-id="5dc9f-137">4</span><span class="sxs-lookup"><span data-stu-id="5dc9f-137">4</span></span> |<span data-ttu-id="5dc9f-138">LED SAS</span><span class="sxs-lookup"><span data-stu-id="5dc9f-138">SAS LEDs</span></span> |
   | <span data-ttu-id="5dc9f-139">5</span><span class="sxs-lookup"><span data-stu-id="5dc9f-139">5</span></span> |<span data-ttu-id="5dc9f-140">Ports série (utilisation en usine uniquement)</span><span class="sxs-lookup"><span data-stu-id="5dc9f-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="5dc9f-141">6</span><span class="sxs-lookup"><span data-stu-id="5dc9f-141">6</span></span> |<span data-ttu-id="5dc9f-142">Port A (Entrée hôte)</span><span class="sxs-lookup"><span data-stu-id="5dc9f-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="5dc9f-143">7</span><span class="sxs-lookup"><span data-stu-id="5dc9f-143">7</span></span> |<span data-ttu-id="5dc9f-144">Port B (Sortie hôte)</span><span class="sxs-lookup"><span data-stu-id="5dc9f-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="5dc9f-145">8</span><span class="sxs-lookup"><span data-stu-id="5dc9f-145">8</span></span> |<span data-ttu-id="5dc9f-146">Port C (utilisation en usine uniquement)</span><span class="sxs-lookup"><span data-stu-id="5dc9f-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="5dc9f-147">Installer un nouveau contrôleur EBOD</span><span class="sxs-lookup"><span data-stu-id="5dc9f-147">Install a new EBOD controller</span></span>
<span data-ttu-id="5dc9f-148">La procédure et le tableau suivants expliquent comment installer un module de contrôleur EBOD dans votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-148">The following procedure and table explain how to install an EBOD controller module in your StorSimple device.</span></span>

#### <a name="to-install-an-ebod-controller"></a><span data-ttu-id="5dc9f-149">Pour installer un contrôleur EBOD</span><span class="sxs-lookup"><span data-stu-id="5dc9f-149">To install an EBOD controller</span></span>
1. <span data-ttu-id="5dc9f-150">Vérifiez que l’appareil EBOD n’est pas endommagé, en particulier le connecteur d’interface.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-150">Check the EBOD device for damage, especially to the interface connector.</span></span> <span data-ttu-id="5dc9f-151">N’installez pas le nouveau contrôleur EBOD si des broches sont tordues.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-151">Do not install the new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="5dc9f-152">Avec les verrous en position ouverte, faites glisser le module dans le boîtier jusqu’à ce que les verrous s’engagent.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-152">With the latches in the open position, slide the module into the enclosure until the latches engage.</span></span>
   
    ![Installation du contrôleur EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="5dc9f-154">**Figure 2** : Installation du module de contrôleur EBOD</span><span class="sxs-lookup"><span data-stu-id="5dc9f-154">**Figure 2**  Installing the EBOD controller module</span></span>
3. <span data-ttu-id="5dc9f-155">Fermez le verrou.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-155">Close the latch.</span></span> <span data-ttu-id="5dc9f-156">Vous devez entendre un clic quand le verrou s’engage.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-156">You should hear a click as the latch engages.</span></span>
   
    ![Libération du verrou EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="5dc9f-158">**Figure 3** : Fermeture du verrou du module EBOD</span><span class="sxs-lookup"><span data-stu-id="5dc9f-158">**Figure 3**  Closing the EBOD module latch</span></span>
4. <span data-ttu-id="5dc9f-159">Rebranchez les câbles.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-159">Reconnect the cables.</span></span> <span data-ttu-id="5dc9f-160">Utilisez la configuration exacte qui existait avant le remplacement.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-160">Use the exact configuration that was present before the replacement.</span></span> <span data-ttu-id="5dc9f-161">Consultez le diagramme et le tableau suivants pour des informations sur la façon de connecter les câbles.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-161">See the following diagram and table for details about how to connect the cables.</span></span>
   
    ![Raccorder votre appareil à l’alimentation électrique](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="5dc9f-163">**Figure 4**.</span><span class="sxs-lookup"><span data-stu-id="5dc9f-163">**Figure 4**.</span></span> <span data-ttu-id="5dc9f-164">Reconnexion des câbles</span><span class="sxs-lookup"><span data-stu-id="5dc9f-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="5dc9f-165">Étiquette</span><span class="sxs-lookup"><span data-stu-id="5dc9f-165">Label</span></span> | <span data-ttu-id="5dc9f-166">Description</span><span class="sxs-lookup"><span data-stu-id="5dc9f-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="5dc9f-167">1</span><span class="sxs-lookup"><span data-stu-id="5dc9f-167">1</span></span> |<span data-ttu-id="5dc9f-168">Boîtier principal</span><span class="sxs-lookup"><span data-stu-id="5dc9f-168">Primary enclosure</span></span> |
   | <span data-ttu-id="5dc9f-169">2</span><span class="sxs-lookup"><span data-stu-id="5dc9f-169">2</span></span> |<span data-ttu-id="5dc9f-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="5dc9f-170">PCM 0</span></span> |
   | <span data-ttu-id="5dc9f-171">3</span><span class="sxs-lookup"><span data-stu-id="5dc9f-171">3</span></span> |<span data-ttu-id="5dc9f-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="5dc9f-172">PCM 1</span></span> |
   | <span data-ttu-id="5dc9f-173">4</span><span class="sxs-lookup"><span data-stu-id="5dc9f-173">4</span></span> |<span data-ttu-id="5dc9f-174">Contrôleur 0</span><span class="sxs-lookup"><span data-stu-id="5dc9f-174">Controller 0</span></span> |
   | <span data-ttu-id="5dc9f-175">5</span><span class="sxs-lookup"><span data-stu-id="5dc9f-175">5</span></span> |<span data-ttu-id="5dc9f-176">Contrôleur 1</span><span class="sxs-lookup"><span data-stu-id="5dc9f-176">Controller 1</span></span> |
   | <span data-ttu-id="5dc9f-177">6</span><span class="sxs-lookup"><span data-stu-id="5dc9f-177">6</span></span> |<span data-ttu-id="5dc9f-178">Contrôleur 0 du boîtier EBOD</span><span class="sxs-lookup"><span data-stu-id="5dc9f-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="5dc9f-179">7</span><span class="sxs-lookup"><span data-stu-id="5dc9f-179">7</span></span> |<span data-ttu-id="5dc9f-180">Contrôleur 1 du boîtier EBOD</span><span class="sxs-lookup"><span data-stu-id="5dc9f-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="5dc9f-181">8</span><span class="sxs-lookup"><span data-stu-id="5dc9f-181">8</span></span> |<span data-ttu-id="5dc9f-182">Boîtier EBOD</span><span class="sxs-lookup"><span data-stu-id="5dc9f-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="5dc9f-183">9</span><span class="sxs-lookup"><span data-stu-id="5dc9f-183">9</span></span> |<span data-ttu-id="5dc9f-184">Unités de distribution de l’alimentation</span><span class="sxs-lookup"><span data-stu-id="5dc9f-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5dc9f-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5dc9f-185">Next steps</span></span>
<span data-ttu-id="5dc9f-186">En savoir plus sur le [remplacement des composants matériels StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="5dc9f-186">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

