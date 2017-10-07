---
title: "aaaReplace un contrôleur StorSimple EBOD | Documents Microsoft"
description: "Explique comment tooremove et remplacer un ou deux contrôleurs EBOD sur un appareil StorSimple 8600."
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
ms.openlocfilehash: 5d29de2ee30bfdd70910050eee5cfa1d293d444f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-an-ebod-controller-on-your-storsimple-device"></a><span data-ttu-id="56f63-103">Remplacer un contrôleur EBOD sur votre appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="56f63-103">Replace an EBOD controller on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="56f63-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="56f63-104">Overview</span></span>
<span data-ttu-id="56f63-105">Ce didacticiel explique comment tooreplace un module de contrôleur EBOD défaillant sur votre appareil Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="56f63-105">This tutorial explains how tooreplace a faulty EBOD controller module on your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="56f63-106">tooreplace un module de contrôleur EBOD, vous devez :</span><span class="sxs-lookup"><span data-stu-id="56f63-106">tooreplace an EBOD controller module, you need to:</span></span>

* <span data-ttu-id="56f63-107">Supprimer le contrôleur EBOD en panne hello</span><span class="sxs-lookup"><span data-stu-id="56f63-107">Remove hello faulty EBOD controller</span></span>
* <span data-ttu-id="56f63-108">Installer un nouveau contrôleur EBOD</span><span class="sxs-lookup"><span data-stu-id="56f63-108">Install a new EBOD controller</span></span>

<span data-ttu-id="56f63-109">Tenez compte des hello informations suivantes avant de commencer :</span><span class="sxs-lookup"><span data-stu-id="56f63-109">Consider hello following information before you begin:</span></span>

* <span data-ttu-id="56f63-110">Des modules EBOD vides doivent être insérés dans tous les emplacements non utilisés.</span><span class="sxs-lookup"><span data-stu-id="56f63-110">Blank EBOD modules must be inserted into all unused slots.</span></span> <span data-ttu-id="56f63-111">boîtier de Hello ne se refroidira pas correctement si un emplacement est laissé ouvert.</span><span class="sxs-lookup"><span data-stu-id="56f63-111">hello enclosure will not cool properly if a slot is left open.</span></span>
* <span data-ttu-id="56f63-112">le contrôleur EBOD Hello est remplaçables à chaud et peut être supprimé ou remplacé.</span><span class="sxs-lookup"><span data-stu-id="56f63-112">hello EBOD controller is hot-swappable and can be removed or replaced.</span></span> <span data-ttu-id="56f63-113">Ne retirez pas un module défectueux tant que vous ne disposez pas d’un remplacement.</span><span class="sxs-lookup"><span data-stu-id="56f63-113">Do not remove a failed module until you have a replacement.</span></span> <span data-ttu-id="56f63-114">Lorsque vous lancez le processus de remplacement hello, vous devez la terminer pendant les 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="56f63-114">When you initiate hello replacement process, you must finish it within 10 minutes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56f63-115">Avant de tenter de tooremove ou remplacer n’importe quel composant StorSimple, assurez-vous que vous passez en revue les hello [conventions des icônes de sécurité](storsimple-safety.md#safety-icon-conventions) et d’autres [précautions de sécurité](storsimple-safety.md).</span><span class="sxs-lookup"><span data-stu-id="56f63-115">Before attempting tooremove or replace any StorSimple component, make sure that you review hello [safety icon conventions](storsimple-safety.md#safety-icon-conventions) and other [safety precautions](storsimple-safety.md).</span></span>
> 
> 

## <a name="remove-an-ebod-controller"></a><span data-ttu-id="56f63-116">Retirer un contrôleur EBOD</span><span class="sxs-lookup"><span data-stu-id="56f63-116">Remove an EBOD controller</span></span>
<span data-ttu-id="56f63-117">Avant de l’échec du module de contrôleur EBOD dans votre appareil StorSimple remplacement hello, assurez-vous que hello autre module de contrôleur EBOD est actif et en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="56f63-117">Before replacing hello failed EBOD controller module in your StorSimple device, make sure that hello other EBOD controller module is active and running.</span></span> <span data-ttu-id="56f63-118">Hello procédure et le tableau suivants expliquent comment tooremove hello module de contrôleur EBOD.</span><span class="sxs-lookup"><span data-stu-id="56f63-118">hello following procedure and table explain how tooremove hello EBOD controller module.</span></span>

#### <a name="tooremove-an-ebod-module"></a><span data-ttu-id="56f63-119">tooremove un module EBOD</span><span class="sxs-lookup"><span data-stu-id="56f63-119">tooremove an EBOD module</span></span>
1. <span data-ttu-id="56f63-120">Ouvrez hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="56f63-120">Open hello Azure classic portal.</span></span>
2. <span data-ttu-id="56f63-121">Accédez trop**périphériques** > **Maintenance** > **état du matériel**et vérifiez que les DEL d’état de hello Hello pour hello EBOD active module de contrôleur est vert, hello DEL de module de contrôleur EBOD hello a échoué est rouge.</span><span class="sxs-lookup"><span data-stu-id="56f63-121">Navigate too**Devices** > **Maintenance** > **Hardware Status**, and verify that hello status of hello LED for hello active EBOD controller module is green and hello LED for hello failed EBOD controller module is red.</span></span>
3. <span data-ttu-id="56f63-122">Localiser le module de contrôleur EBOD hello a échoué à hello arrière appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="56f63-122">Locate hello failed EBOD controller module at hello back of hello device.</span></span>
4. <span data-ttu-id="56f63-123">Débranchez les câbles hello qui se connectent hello EBOD module toohello contrôleur avant d’effectuer le module EBOD hello système de hello.</span><span class="sxs-lookup"><span data-stu-id="56f63-123">Remove hello cables that connect hello EBOD controller module toohello controller before taking hello EBOD module out of hello system.</span></span>
5. <span data-ttu-id="56f63-124">Prenez note de hello exact du port SAS du module de contrôleur EBOD hello qui était connecté toohello contrôleur.</span><span class="sxs-lookup"><span data-stu-id="56f63-124">Make a note of hello exact SAS port of hello EBOD controller module that was connected toohello controller.</span></span> <span data-ttu-id="56f63-125">Vous sera nécessaire toorestore hello système toothis après le remplacement du module EBOD hello.</span><span class="sxs-lookup"><span data-stu-id="56f63-125">You will be required toorestore hello system toothis configuration after you replace hello EBOD module.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="56f63-126">En règle générale, il s’agit du Port A, qui porte le nom **héberger dans** Bonjour suivant schéma.</span><span class="sxs-lookup"><span data-stu-id="56f63-126">Typically, this will be Port A, which is labeled as **Host in** in hello following diagram.</span></span>
   > 
   > 
   
    ![Fond de panier du contrôleur EBOD](./media/storsimple-ebod-controller-replacement/IC741049.png)
   
     <span data-ttu-id="56f63-128">**Figure 1** : Arrière du module EBOD</span><span class="sxs-lookup"><span data-stu-id="56f63-128">**Figure 1** Back of EBOD module</span></span>
   
   | <span data-ttu-id="56f63-129">Étiquette</span><span class="sxs-lookup"><span data-stu-id="56f63-129">Label</span></span> | <span data-ttu-id="56f63-130">Description</span><span class="sxs-lookup"><span data-stu-id="56f63-130">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="56f63-131">1</span><span class="sxs-lookup"><span data-stu-id="56f63-131">1</span></span> |<span data-ttu-id="56f63-132">LED indiquant une panne</span><span class="sxs-lookup"><span data-stu-id="56f63-132">Fault LED</span></span> |
   | <span data-ttu-id="56f63-133">2</span><span class="sxs-lookup"><span data-stu-id="56f63-133">2</span></span> |<span data-ttu-id="56f63-134">LED d’alimentation</span><span class="sxs-lookup"><span data-stu-id="56f63-134">Power LED</span></span> |
   | <span data-ttu-id="56f63-135">3</span><span class="sxs-lookup"><span data-stu-id="56f63-135">3</span></span> |<span data-ttu-id="56f63-136">Connecteurs SaaS</span><span class="sxs-lookup"><span data-stu-id="56f63-136">SAS connectors</span></span> |
   | <span data-ttu-id="56f63-137">4</span><span class="sxs-lookup"><span data-stu-id="56f63-137">4</span></span> |<span data-ttu-id="56f63-138">LED SAS</span><span class="sxs-lookup"><span data-stu-id="56f63-138">SAS LEDs</span></span> |
   | <span data-ttu-id="56f63-139">5</span><span class="sxs-lookup"><span data-stu-id="56f63-139">5</span></span> |<span data-ttu-id="56f63-140">Ports série (utilisation en usine uniquement)</span><span class="sxs-lookup"><span data-stu-id="56f63-140">Serial ports for factory use only</span></span> |
   | <span data-ttu-id="56f63-141">6</span><span class="sxs-lookup"><span data-stu-id="56f63-141">6</span></span> |<span data-ttu-id="56f63-142">Port A (Entrée hôte)</span><span class="sxs-lookup"><span data-stu-id="56f63-142">Port A (Host in)</span></span> |
   | <span data-ttu-id="56f63-143">7</span><span class="sxs-lookup"><span data-stu-id="56f63-143">7</span></span> |<span data-ttu-id="56f63-144">Port B (Sortie hôte)</span><span class="sxs-lookup"><span data-stu-id="56f63-144">Port B (Host out)</span></span> |
   | <span data-ttu-id="56f63-145">8</span><span class="sxs-lookup"><span data-stu-id="56f63-145">8</span></span> |<span data-ttu-id="56f63-146">Port C (utilisation en usine uniquement)</span><span class="sxs-lookup"><span data-stu-id="56f63-146">Port C (Factory use only)</span></span> |

## <a name="install-a-new-ebod-controller"></a><span data-ttu-id="56f63-147">Installer un nouveau contrôleur EBOD</span><span class="sxs-lookup"><span data-stu-id="56f63-147">Install a new EBOD controller</span></span>
<span data-ttu-id="56f63-148">Hello procédure et le tableau suivants expliquent comment tooinstall un module de contrôleur EBOD dans votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="56f63-148">hello following procedure and table explain how tooinstall an EBOD controller module in your StorSimple device.</span></span>

#### <a name="tooinstall-an-ebod-controller"></a><span data-ttu-id="56f63-149">tooinstall un contrôleur EBOD</span><span class="sxs-lookup"><span data-stu-id="56f63-149">tooinstall an EBOD controller</span></span>
1. <span data-ttu-id="56f63-150">Vérifiez le périphérique, EBOD hello est endommagé, le connecteur d’interface toohello en particulier.</span><span class="sxs-lookup"><span data-stu-id="56f63-150">Check hello EBOD device for damage, especially toohello interface connector.</span></span> <span data-ttu-id="56f63-151">N’installez pas le contrôleur EBOD nouveau hello si des broches sont tordues.</span><span class="sxs-lookup"><span data-stu-id="56f63-151">Do not install hello new EBOD controller if any pins are bent.</span></span>
2. <span data-ttu-id="56f63-152">Avec les loquets hello Bonjour ouvrez position, module de hello diapositive dans boîtier hello jusqu'à ce que hello loquets s’engagent.</span><span class="sxs-lookup"><span data-stu-id="56f63-152">With hello latches in hello open position, slide hello module into hello enclosure until hello latches engage.</span></span>
   
    ![Installation du contrôleur EBOD](./media/storsimple-ebod-controller-replacement/IC741050.png)
   
    <span data-ttu-id="56f63-154">**Figure 2** module de contrôleur EBOD installation Bonjour</span><span class="sxs-lookup"><span data-stu-id="56f63-154">**Figure 2**  Installing hello EBOD controller module</span></span>
3. <span data-ttu-id="56f63-155">Verrou de fermer hello.</span><span class="sxs-lookup"><span data-stu-id="56f63-155">Close hello latch.</span></span> <span data-ttu-id="56f63-156">Vous devez entendre un clic comme les verrous hello s’engage.</span><span class="sxs-lookup"><span data-stu-id="56f63-156">You should hear a click as hello latch engages.</span></span>
   
    ![Libération du verrou EBOD](./media/storsimple-ebod-controller-replacement/IC741047.png)
   
    <span data-ttu-id="56f63-158">**Figure 3** fermeture du verrou du module EBOD hello</span><span class="sxs-lookup"><span data-stu-id="56f63-158">**Figure 3**  Closing hello EBOD module latch</span></span>
4. <span data-ttu-id="56f63-159">Rebranchez les câbles hello.</span><span class="sxs-lookup"><span data-stu-id="56f63-159">Reconnect hello cables.</span></span> <span data-ttu-id="56f63-160">Utiliser la configuration exacte hello qui existait avant le remplacement de hello.</span><span class="sxs-lookup"><span data-stu-id="56f63-160">Use hello exact configuration that was present before hello replacement.</span></span> <span data-ttu-id="56f63-161">Consultez hello suivant schéma et de table pour plus d’informations sur la façon de câbles de hello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="56f63-161">See hello following diagram and table for details about how tooconnect hello cables.</span></span>
   
    ![Raccorder votre appareil à l’alimentation électrique](./media/storsimple-ebod-controller-replacement/IC770723.png)
   
    <span data-ttu-id="56f63-163">**Figure 4**.</span><span class="sxs-lookup"><span data-stu-id="56f63-163">**Figure 4**.</span></span> <span data-ttu-id="56f63-164">Reconnexion des câbles</span><span class="sxs-lookup"><span data-stu-id="56f63-164">Reconnecting cables</span></span>
   
   | <span data-ttu-id="56f63-165">Étiquette</span><span class="sxs-lookup"><span data-stu-id="56f63-165">Label</span></span> | <span data-ttu-id="56f63-166">Description</span><span class="sxs-lookup"><span data-stu-id="56f63-166">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="56f63-167">1</span><span class="sxs-lookup"><span data-stu-id="56f63-167">1</span></span> |<span data-ttu-id="56f63-168">Boîtier principal</span><span class="sxs-lookup"><span data-stu-id="56f63-168">Primary enclosure</span></span> |
   | <span data-ttu-id="56f63-169">2</span><span class="sxs-lookup"><span data-stu-id="56f63-169">2</span></span> |<span data-ttu-id="56f63-170">PCM 0</span><span class="sxs-lookup"><span data-stu-id="56f63-170">PCM 0</span></span> |
   | <span data-ttu-id="56f63-171">3</span><span class="sxs-lookup"><span data-stu-id="56f63-171">3</span></span> |<span data-ttu-id="56f63-172">PCM 1</span><span class="sxs-lookup"><span data-stu-id="56f63-172">PCM 1</span></span> |
   | <span data-ttu-id="56f63-173">4</span><span class="sxs-lookup"><span data-stu-id="56f63-173">4</span></span> |<span data-ttu-id="56f63-174">Contrôleur 0</span><span class="sxs-lookup"><span data-stu-id="56f63-174">Controller 0</span></span> |
   | <span data-ttu-id="56f63-175">5</span><span class="sxs-lookup"><span data-stu-id="56f63-175">5</span></span> |<span data-ttu-id="56f63-176">Contrôleur 1</span><span class="sxs-lookup"><span data-stu-id="56f63-176">Controller 1</span></span> |
   | <span data-ttu-id="56f63-177">6</span><span class="sxs-lookup"><span data-stu-id="56f63-177">6</span></span> |<span data-ttu-id="56f63-178">Contrôleur 0 du boîtier EBOD</span><span class="sxs-lookup"><span data-stu-id="56f63-178">EBOD controller 0</span></span> |
   | <span data-ttu-id="56f63-179">7</span><span class="sxs-lookup"><span data-stu-id="56f63-179">7</span></span> |<span data-ttu-id="56f63-180">Contrôleur 1 du boîtier EBOD</span><span class="sxs-lookup"><span data-stu-id="56f63-180">EBOD controller 1</span></span> |
   | <span data-ttu-id="56f63-181">8</span><span class="sxs-lookup"><span data-stu-id="56f63-181">8</span></span> |<span data-ttu-id="56f63-182">Boîtier EBOD</span><span class="sxs-lookup"><span data-stu-id="56f63-182">EBOD enclosure</span></span> |
   | <span data-ttu-id="56f63-183">9</span><span class="sxs-lookup"><span data-stu-id="56f63-183">9</span></span> |<span data-ttu-id="56f63-184">Unités de distribution de l’alimentation</span><span class="sxs-lookup"><span data-stu-id="56f63-184">Power Distribution Units</span></span> |

## <a name="next-steps"></a><span data-ttu-id="56f63-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="56f63-185">Next steps</span></span>
<span data-ttu-id="56f63-186">En savoir plus sur le [remplacement des composants matériels StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="56f63-186">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

