---
title: "aaaDeep approfondir prédire l’intégrité du véhicule et du pilotage habitudes - Azure | Documents Microsoft"
description: "Utiliser les fonctionnalités de hello des aperçus Cortana Intelligence toogain prédictives et en temps réel sur l’intégrité du véhicule et du pilotage habituelles."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a><span data-ttu-id="0bd7d-103">Scénario de solution véhicule télémétrie analytique : présentation approfondie d’une solution de hello</span><span class="sxs-lookup"><span data-stu-id="0bd7d-103">Vehicle telemetry analytics solution playbook: deep dive into hello solution</span></span>
<span data-ttu-id="0bd7d-104">Cela **menu** lie toohello des sections de ce manuel :</span><span class="sxs-lookup"><span data-stu-id="0bd7d-104">This **menu** links toohello sections of this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="0bd7d-105">Cette section permet d’Explorer chacune des étapes hello mentionnés dans hello Architecture de Solution avec des instructions et des pointeurs pour la personnalisation.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-105">This section drills down into each of hello stages depicted in hello Solution Architecture with instructions and pointers for customization.</span></span> 

## <a name="data-sources"></a><span data-ttu-id="0bd7d-106">Sources de données</span><span class="sxs-lookup"><span data-stu-id="0bd7d-106">Data Sources</span></span>
<span data-ttu-id="0bd7d-107">solution de Hello utilise deux sources de données différentes :</span><span class="sxs-lookup"><span data-stu-id="0bd7d-107">hello solution uses two different data sources:</span></span>

* <span data-ttu-id="0bd7d-108">**jeu de données de diagnostic et de signaux des véhicules simulés** et</span><span class="sxs-lookup"><span data-stu-id="0bd7d-108">**simulated vehicle signals and diagnostic dataset** and</span></span> 
* <span data-ttu-id="0bd7d-109">**catalogue de véhicules**</span><span class="sxs-lookup"><span data-stu-id="0bd7d-109">**vehicle catalog**</span></span>

<span data-ttu-id="0bd7d-110">Un simulateur de télématique des véhicules est intégré à cette solution.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-110">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="0bd7d-111">Il émet des informations de diagnostic et signale l’état toohello correspondant du véhicule de hello et toohello gérant le modèle à un moment donné dans le temps.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-111">It emits diagnostic information and signals corresponding toohello state of hello vehicle and toohello driving pattern at a given point in time.</span></span> <span data-ttu-id="0bd7d-112">Cliquez sur [véhicule télématique simulateur](http://go.microsoft.com/fwlink/?LinkId=717075) hello de toodownload **véhicule télématique simulateur Solution Visual Studio** pour les personnalisations en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-112">Click [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **Vehicle Telematics Simulator Visual Studio Solution** for customizations based on your requirements.</span></span> <span data-ttu-id="0bd7d-113">catalogue de véhicule Hello contient un dataset de référence avec un mappage de toomodel VIN.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-113">hello vehicle catalog contains a reference dataset with a VIN toomodel mapping.</span></span>

![Simulateur de télématique des véhicules](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

<span data-ttu-id="0bd7d-115">*Figure 1 – Simulateur de télématique des véhicules*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-115">*Figure 1 – Vehicle Telematics Simulator*</span></span>

<span data-ttu-id="0bd7d-116">Il s’agit d’un jeu de données au format JSON qui contient les hello suivant le schéma.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-116">This is a JSON-formatted dataset that contains hello following schema.</span></span>

| <span data-ttu-id="0bd7d-117">Colonne</span><span class="sxs-lookup"><span data-stu-id="0bd7d-117">Column</span></span> | <span data-ttu-id="0bd7d-118">Description</span><span class="sxs-lookup"><span data-stu-id="0bd7d-118">Description</span></span> | <span data-ttu-id="0bd7d-119">Valeurs</span><span class="sxs-lookup"><span data-stu-id="0bd7d-119">Values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0bd7d-120">VIN</span><span class="sxs-lookup"><span data-stu-id="0bd7d-120">VIN</span></span> |<span data-ttu-id="0bd7d-121">Numéro d’identification du véhicule généré de manière aléatoire</span><span class="sxs-lookup"><span data-stu-id="0bd7d-121">Randomly generated Vehicle Identification Number</span></span> |<span data-ttu-id="0bd7d-122">Ce numéro est obtenu à partir d’une liste de référence contenant 10 000 numéros d’identification de véhicule générés de manière aléatoire.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-122">This is obtained from a master list of 10,000 randomly generated vehicle identification numbers.</span></span> |
| <span data-ttu-id="0bd7d-123">Outside temperature</span><span class="sxs-lookup"><span data-stu-id="0bd7d-123">Outside temperature</span></span> |<span data-ttu-id="0bd7d-124">Hello en dehors de la température où véhicule de hello est conduite</span><span class="sxs-lookup"><span data-stu-id="0bd7d-124">hello outside temperature where hello vehicle is driving</span></span> |<span data-ttu-id="0bd7d-125">Nombre généré de manière aléatoire et compris entre 0 et 100</span><span class="sxs-lookup"><span data-stu-id="0bd7d-125">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="0bd7d-126">Engine temperature</span><span class="sxs-lookup"><span data-stu-id="0bd7d-126">Engine temperature</span></span> |<span data-ttu-id="0bd7d-127">température du moteur Hello du véhicule de hello</span><span class="sxs-lookup"><span data-stu-id="0bd7d-127">hello engine temperature of hello vehicle</span></span> |<span data-ttu-id="0bd7d-128">Nombre généré de manière aléatoire et compris entre 0 et 500</span><span class="sxs-lookup"><span data-stu-id="0bd7d-128">Randomly generated number from 0-500</span></span> |
| <span data-ttu-id="0bd7d-129">Vitesse</span><span class="sxs-lookup"><span data-stu-id="0bd7d-129">Speed</span></span> |<span data-ttu-id="0bd7d-130">vitesse du moteur Hello à quels hello véhicule est conduite</span><span class="sxs-lookup"><span data-stu-id="0bd7d-130">hello engine speed at which hello vehicle is driving</span></span> |<span data-ttu-id="0bd7d-131">Nombre généré de manière aléatoire et compris entre 0 et 100</span><span class="sxs-lookup"><span data-stu-id="0bd7d-131">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="0bd7d-132">Fuel</span><span class="sxs-lookup"><span data-stu-id="0bd7d-132">Fuel</span></span> |<span data-ttu-id="0bd7d-133">niveau de carburant Hello du véhicule de hello</span><span class="sxs-lookup"><span data-stu-id="0bd7d-133">hello fuel level of hello vehicle</span></span> |<span data-ttu-id="0bd7d-134">Nombre généré de manière aléatoire et compris entre 0 et 100 (indique le niveau de carburant en pourcentage)</span><span class="sxs-lookup"><span data-stu-id="0bd7d-134">Randomly generated number from 0-100 (indicates fuel level percentage)</span></span> |
| <span data-ttu-id="0bd7d-135">EngineOil</span><span class="sxs-lookup"><span data-stu-id="0bd7d-135">EngineOil</span></span> |<span data-ttu-id="0bd7d-136">niveau de pétrole Hello du moteur du véhicule de hello</span><span class="sxs-lookup"><span data-stu-id="0bd7d-136">hello engine oil level of hello vehicle</span></span> |<span data-ttu-id="0bd7d-137">Nombre généré de manière aléatoire et compris entre 0 et 100 (indique le niveau d’huile moteur en pourcentage)</span><span class="sxs-lookup"><span data-stu-id="0bd7d-137">Randomly generated number from 0-100 (indicates engine oil level percentage)</span></span> |
| <span data-ttu-id="0bd7d-138">Pression des pneus</span><span class="sxs-lookup"><span data-stu-id="0bd7d-138">Tire pressure</span></span> |<span data-ttu-id="0bd7d-139">pression des pneus Hello du véhicule de hello</span><span class="sxs-lookup"><span data-stu-id="0bd7d-139">hello tire pressure of hello vehicle</span></span> |<span data-ttu-id="0bd7d-140">Nombre généré de manière aléatoire et compris entre 0 et 50 (indique le niveau de pression des pneus en pourcentage)</span><span class="sxs-lookup"><span data-stu-id="0bd7d-140">Randomly generated number from 0-50 (indicates tire pressure level percentage)</span></span> |
| <span data-ttu-id="0bd7d-141">Odometer</span><span class="sxs-lookup"><span data-stu-id="0bd7d-141">Odometer</span></span> |<span data-ttu-id="0bd7d-142">kilométrique Hello du véhicule de hello</span><span class="sxs-lookup"><span data-stu-id="0bd7d-142">hello odometer reading of hello vehicle</span></span> |<span data-ttu-id="0bd7d-143">Nombre généré de manière aléatoire et compris entre 0 et 200 000</span><span class="sxs-lookup"><span data-stu-id="0bd7d-143">Randomly generated number from 0-200000</span></span> |
| <span data-ttu-id="0bd7d-144">Accelerator_pedal_position</span><span class="sxs-lookup"><span data-stu-id="0bd7d-144">Accelerator_pedal_position</span></span> |<span data-ttu-id="0bd7d-145">position de pédales accélérateur Hello du véhicule de hello</span><span class="sxs-lookup"><span data-stu-id="0bd7d-145">hello accelerator pedal position of hello vehicle</span></span> |<span data-ttu-id="0bd7d-146">Nombre généré de manière aléatoire et compris entre 0 et 100 (indique le niveau d’accélération en pourcentage)</span><span class="sxs-lookup"><span data-stu-id="0bd7d-146">Randomly generated number from 0-100 (indicates accelerator level percentage)</span></span> |
| <span data-ttu-id="0bd7d-147">Parking_brake_status</span><span class="sxs-lookup"><span data-stu-id="0bd7d-147">Parking_brake_status</span></span> |<span data-ttu-id="0bd7d-148">Indique si la récupération du véhicule hello est parqué ou non</span><span class="sxs-lookup"><span data-stu-id="0bd7d-148">Indicates whether hello vehicle is parked or not</span></span> |<span data-ttu-id="0bd7d-149">True ou False</span><span class="sxs-lookup"><span data-stu-id="0bd7d-149">True or False</span></span> |
| <span data-ttu-id="0bd7d-150">Headlamp_status</span><span class="sxs-lookup"><span data-stu-id="0bd7d-150">Headlamp_status</span></span> |<span data-ttu-id="0bd7d-151">Indique où projecteur de hello est activé ou non</span><span class="sxs-lookup"><span data-stu-id="0bd7d-151">Indicates where hello headlamp is on or not</span></span> |<span data-ttu-id="0bd7d-152">True ou False</span><span class="sxs-lookup"><span data-stu-id="0bd7d-152">True or False</span></span> |
| <span data-ttu-id="0bd7d-153">Brake_pedal_status</span><span class="sxs-lookup"><span data-stu-id="0bd7d-153">Brake_pedal_status</span></span> |<span data-ttu-id="0bd7d-154">Indique si les pédales de frein hello est enfoncé ou non</span><span class="sxs-lookup"><span data-stu-id="0bd7d-154">Indicates whether hello brake pedal is pressed or not</span></span> |<span data-ttu-id="0bd7d-155">True ou False</span><span class="sxs-lookup"><span data-stu-id="0bd7d-155">True or False</span></span> |
| <span data-ttu-id="0bd7d-156">Transmission_gear_position</span><span class="sxs-lookup"><span data-stu-id="0bd7d-156">Transmission_gear_position</span></span> |<span data-ttu-id="0bd7d-157">position de vitesse de transmission de Hello d’hello véhicule</span><span class="sxs-lookup"><span data-stu-id="0bd7d-157">hello transmission gear position of hello vehicle</span></span> |<span data-ttu-id="0bd7d-158">États : première, deuxième, troisième, quatrième, cinquième, sixième, septième, huitième</span><span class="sxs-lookup"><span data-stu-id="0bd7d-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span></span> |
| <span data-ttu-id="0bd7d-159">Ignition_status</span><span class="sxs-lookup"><span data-stu-id="0bd7d-159">Ignition_status</span></span> |<span data-ttu-id="0bd7d-160">Indique si la récupération du véhicule hello est en cours d’exécution ou arrêté</span><span class="sxs-lookup"><span data-stu-id="0bd7d-160">Indicates whether hello vehicle is running or stopped</span></span> |<span data-ttu-id="0bd7d-161">True ou False</span><span class="sxs-lookup"><span data-stu-id="0bd7d-161">True or False</span></span> |
| <span data-ttu-id="0bd7d-162">Windshield_wiper_status</span><span class="sxs-lookup"><span data-stu-id="0bd7d-162">Windshield_wiper_status</span></span> |<span data-ttu-id="0bd7d-163">Indique si essuie-glace hello est activé ou non</span><span class="sxs-lookup"><span data-stu-id="0bd7d-163">Indicates whether hello windshield wiper is turned or not</span></span> |<span data-ttu-id="0bd7d-164">True ou False</span><span class="sxs-lookup"><span data-stu-id="0bd7d-164">True or False</span></span> |
| <span data-ttu-id="0bd7d-165">ABS</span><span class="sxs-lookup"><span data-stu-id="0bd7d-165">ABS</span></span> |<span data-ttu-id="0bd7d-166">Indique si l’ABS est activé ou non</span><span class="sxs-lookup"><span data-stu-id="0bd7d-166">Indicates whether ABS is engaged or not</span></span> |<span data-ttu-id="0bd7d-167">True ou False</span><span class="sxs-lookup"><span data-stu-id="0bd7d-167">True or False</span></span> |
| <span data-ttu-id="0bd7d-168">Timestamp</span><span class="sxs-lookup"><span data-stu-id="0bd7d-168">Timestamp</span></span> |<span data-ttu-id="0bd7d-169">horodatage Hello lors de la création du point de données hello</span><span class="sxs-lookup"><span data-stu-id="0bd7d-169">hello timestamp when hello data point is created</span></span> |<span data-ttu-id="0bd7d-170">Date</span><span class="sxs-lookup"><span data-stu-id="0bd7d-170">Date</span></span> |
| <span data-ttu-id="0bd7d-171">City</span><span class="sxs-lookup"><span data-stu-id="0bd7d-171">City</span></span> |<span data-ttu-id="0bd7d-172">emplacement de Hello du véhicule de hello</span><span class="sxs-lookup"><span data-stu-id="0bd7d-172">hello location of hello vehicle</span></span> |<span data-ttu-id="0bd7d-173">4 villes dans cette solution : Bellevue, Redmond, Sammamish, Seattle</span><span class="sxs-lookup"><span data-stu-id="0bd7d-173">4 cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span></span> |

<span data-ttu-id="0bd7d-174">dataset de référence du modèle Hello véhicule contient un mappage toohello VIN.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-174">hello vehicle model reference dataset contains VIN toohello model mapping.</span></span> 

| <span data-ttu-id="0bd7d-175">VIN</span><span class="sxs-lookup"><span data-stu-id="0bd7d-175">VIN</span></span> | <span data-ttu-id="0bd7d-176">Modèle</span><span class="sxs-lookup"><span data-stu-id="0bd7d-176">Model</span></span> |
| --- | --- |
| <span data-ttu-id="0bd7d-177">FHL3O1SA4IEHB4WU1</span><span class="sxs-lookup"><span data-stu-id="0bd7d-177">FHL3O1SA4IEHB4WU1</span></span> |<span data-ttu-id="0bd7d-178">Berline</span><span class="sxs-lookup"><span data-stu-id="0bd7d-178">Sedan</span></span> |
| <span data-ttu-id="0bd7d-179">8J0U8XCPRGW4Z3NQE</span><span class="sxs-lookup"><span data-stu-id="0bd7d-179">8J0U8XCPRGW4Z3NQE</span></span> |<span data-ttu-id="0bd7d-180">Hybride</span><span class="sxs-lookup"><span data-stu-id="0bd7d-180">Hybrid</span></span> |
| <span data-ttu-id="0bd7d-181">WORG68Z2PLTNZDBI7</span><span class="sxs-lookup"><span data-stu-id="0bd7d-181">WORG68Z2PLTNZDBI7</span></span> |<span data-ttu-id="0bd7d-182">Berline familiale</span><span class="sxs-lookup"><span data-stu-id="0bd7d-182">Family Saloon</span></span> |
| <span data-ttu-id="0bd7d-183">JTHMYHQTEPP4WBMRN</span><span class="sxs-lookup"><span data-stu-id="0bd7d-183">JTHMYHQTEPP4WBMRN</span></span> |<span data-ttu-id="0bd7d-184">Berline</span><span class="sxs-lookup"><span data-stu-id="0bd7d-184">Sedan</span></span> |
| <span data-ttu-id="0bd7d-185">W9FTHG27LZN1YWO0Y</span><span class="sxs-lookup"><span data-stu-id="0bd7d-185">W9FTHG27LZN1YWO0Y</span></span> |<span data-ttu-id="0bd7d-186">Hybride</span><span class="sxs-lookup"><span data-stu-id="0bd7d-186">Hybrid</span></span> |
| <span data-ttu-id="0bd7d-187">MHTP9N792PHK08WJM</span><span class="sxs-lookup"><span data-stu-id="0bd7d-187">MHTP9N792PHK08WJM</span></span> |<span data-ttu-id="0bd7d-188">Berline familiale</span><span class="sxs-lookup"><span data-stu-id="0bd7d-188">Family Saloon</span></span> |
| <span data-ttu-id="0bd7d-189">EI4QXI2AXVQQING4I</span><span class="sxs-lookup"><span data-stu-id="0bd7d-189">EI4QXI2AXVQQING4I</span></span> |<span data-ttu-id="0bd7d-190">Berline</span><span class="sxs-lookup"><span data-stu-id="0bd7d-190">Sedan</span></span> |
| <span data-ttu-id="0bd7d-191">5KKR2VB4WHQH97PF8</span><span class="sxs-lookup"><span data-stu-id="0bd7d-191">5KKR2VB4WHQH97PF8</span></span> |<span data-ttu-id="0bd7d-192">Hybride</span><span class="sxs-lookup"><span data-stu-id="0bd7d-192">Hybrid</span></span> |
| <span data-ttu-id="0bd7d-193">W9NSZ423XZHAONYXB</span><span class="sxs-lookup"><span data-stu-id="0bd7d-193">W9NSZ423XZHAONYXB</span></span> |<span data-ttu-id="0bd7d-194">Berline familiale</span><span class="sxs-lookup"><span data-stu-id="0bd7d-194">Family Saloon</span></span> |
| <span data-ttu-id="0bd7d-195">26WJSGHX4MA5ROHNL</span><span class="sxs-lookup"><span data-stu-id="0bd7d-195">26WJSGHX4MA5ROHNL</span></span> |<span data-ttu-id="0bd7d-196">Cabriolet</span><span class="sxs-lookup"><span data-stu-id="0bd7d-196">Convertible</span></span> |
| <span data-ttu-id="0bd7d-197">GHLUB6ONKMOSI7E77</span><span class="sxs-lookup"><span data-stu-id="0bd7d-197">GHLUB6ONKMOSI7E77</span></span> |<span data-ttu-id="0bd7d-198">Break</span><span class="sxs-lookup"><span data-stu-id="0bd7d-198">Station Wagon</span></span> |
| <span data-ttu-id="0bd7d-199">9C2RHVRVLMEJDBXLP</span><span class="sxs-lookup"><span data-stu-id="0bd7d-199">9C2RHVRVLMEJDBXLP</span></span> |<span data-ttu-id="0bd7d-200">Voiture compacte</span><span class="sxs-lookup"><span data-stu-id="0bd7d-200">Compact Car</span></span> |
| <span data-ttu-id="0bd7d-201">BRNHVMZOUJ6EOCP32</span><span class="sxs-lookup"><span data-stu-id="0bd7d-201">BRNHVMZOUJ6EOCP32</span></span> |<span data-ttu-id="0bd7d-202">Petit SUV</span><span class="sxs-lookup"><span data-stu-id="0bd7d-202">Small SUV</span></span> |
| <span data-ttu-id="0bd7d-203">VCYVW0WUZNBTM594J</span><span class="sxs-lookup"><span data-stu-id="0bd7d-203">VCYVW0WUZNBTM594J</span></span> |<span data-ttu-id="0bd7d-204">Voiture de sport</span><span class="sxs-lookup"><span data-stu-id="0bd7d-204">Sports Car</span></span> |
| <span data-ttu-id="0bd7d-205">HNVCE6YFZSA5M82NY</span><span class="sxs-lookup"><span data-stu-id="0bd7d-205">HNVCE6YFZSA5M82NY</span></span> |<span data-ttu-id="0bd7d-206">SUV de taille moyenne</span><span class="sxs-lookup"><span data-stu-id="0bd7d-206">Medium SUV</span></span> |
| <span data-ttu-id="0bd7d-207">4R30FOR7NUOBL05GJ</span><span class="sxs-lookup"><span data-stu-id="0bd7d-207">4R30FOR7NUOBL05GJ</span></span> |<span data-ttu-id="0bd7d-208">Break</span><span class="sxs-lookup"><span data-stu-id="0bd7d-208">Station Wagon</span></span> |
| <span data-ttu-id="0bd7d-209">WYNIIY42VKV6OQS1J</span><span class="sxs-lookup"><span data-stu-id="0bd7d-209">WYNIIY42VKV6OQS1J</span></span> |<span data-ttu-id="0bd7d-210">Grand SUV</span><span class="sxs-lookup"><span data-stu-id="0bd7d-210">Large SUV</span></span> |
| <span data-ttu-id="0bd7d-211">8Y5QKG27QET1RBK7I</span><span class="sxs-lookup"><span data-stu-id="0bd7d-211">8Y5QKG27QET1RBK7I</span></span> |<span data-ttu-id="0bd7d-212">Grand SUV</span><span class="sxs-lookup"><span data-stu-id="0bd7d-212">Large SUV</span></span> |
| <span data-ttu-id="0bd7d-213">DF6OX2WSRA6511BVG</span><span class="sxs-lookup"><span data-stu-id="0bd7d-213">DF6OX2WSRA6511BVG</span></span> |<span data-ttu-id="0bd7d-214">Coupé</span><span class="sxs-lookup"><span data-stu-id="0bd7d-214">Coupe</span></span> |
| <span data-ttu-id="0bd7d-215">Z2EOZWZBXAEW3E60T</span><span class="sxs-lookup"><span data-stu-id="0bd7d-215">Z2EOZWZBXAEW3E60T</span></span> |<span data-ttu-id="0bd7d-216">Berline</span><span class="sxs-lookup"><span data-stu-id="0bd7d-216">Sedan</span></span> |
| <span data-ttu-id="0bd7d-217">M4TV6IEALD5QDS3IR</span><span class="sxs-lookup"><span data-stu-id="0bd7d-217">M4TV6IEALD5QDS3IR</span></span> |<span data-ttu-id="0bd7d-218">Hybride</span><span class="sxs-lookup"><span data-stu-id="0bd7d-218">Hybrid</span></span> |
| <span data-ttu-id="0bd7d-219">VHRA1Y2TGTA84F00H</span><span class="sxs-lookup"><span data-stu-id="0bd7d-219">VHRA1Y2TGTA84F00H</span></span> |<span data-ttu-id="0bd7d-220">Berline familiale</span><span class="sxs-lookup"><span data-stu-id="0bd7d-220">Family Saloon</span></span> |
| <span data-ttu-id="0bd7d-221">R0JAUHT1L1R3BIKI0</span><span class="sxs-lookup"><span data-stu-id="0bd7d-221">R0JAUHT1L1R3BIKI0</span></span> |<span data-ttu-id="0bd7d-222">Berline</span><span class="sxs-lookup"><span data-stu-id="0bd7d-222">Sedan</span></span> |
| <span data-ttu-id="0bd7d-223">9230C202Z60XX84AU</span><span class="sxs-lookup"><span data-stu-id="0bd7d-223">9230C202Z60XX84AU</span></span> |<span data-ttu-id="0bd7d-224">Hybride</span><span class="sxs-lookup"><span data-stu-id="0bd7d-224">Hybrid</span></span> |
| <span data-ttu-id="0bd7d-225">T8DNDN5UDCWL7M72H</span><span class="sxs-lookup"><span data-stu-id="0bd7d-225">T8DNDN5UDCWL7M72H</span></span> |<span data-ttu-id="0bd7d-226">Berline familiale</span><span class="sxs-lookup"><span data-stu-id="0bd7d-226">Family Saloon</span></span> |
| <span data-ttu-id="0bd7d-227">4WPYRUZII5YV7YA42</span><span class="sxs-lookup"><span data-stu-id="0bd7d-227">4WPYRUZII5YV7YA42</span></span> |<span data-ttu-id="0bd7d-228">Berline</span><span class="sxs-lookup"><span data-stu-id="0bd7d-228">Sedan</span></span> |
| <span data-ttu-id="0bd7d-229">D1ZVY26UV2BFGHZNO</span><span class="sxs-lookup"><span data-stu-id="0bd7d-229">D1ZVY26UV2BFGHZNO</span></span> |<span data-ttu-id="0bd7d-230">Hybride</span><span class="sxs-lookup"><span data-stu-id="0bd7d-230">Hybrid</span></span> |
| <span data-ttu-id="0bd7d-231">XUF99EW9OIQOMV7Q7</span><span class="sxs-lookup"><span data-stu-id="0bd7d-231">XUF99EW9OIQOMV7Q7</span></span> |<span data-ttu-id="0bd7d-232">Berline familiale</span><span class="sxs-lookup"><span data-stu-id="0bd7d-232">Family Saloon</span></span> |
| <span data-ttu-id="0bd7d-233">8OMCL3LGI7XNCC21U</span><span class="sxs-lookup"><span data-stu-id="0bd7d-233">8OMCL3LGI7XNCC21U</span></span> |<span data-ttu-id="0bd7d-234">Cabriolet</span><span class="sxs-lookup"><span data-stu-id="0bd7d-234">Convertible</span></span> |
| <span data-ttu-id="0bd7d-235">…….</span><span class="sxs-lookup"><span data-stu-id="0bd7d-235">…….</span></span> | |

### <a name="references"></a><span data-ttu-id="0bd7d-236">Références</span><span class="sxs-lookup"><span data-stu-id="0bd7d-236">References</span></span>
[<span data-ttu-id="0bd7d-237">Solution Vehicle Telematics Simulator Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0bd7d-237">Vehicle Telematics Simulator Visual Studio Solution</span></span>](http://go.microsoft.com/fwlink/?LinkId=717075) 

[<span data-ttu-id="0bd7d-238">Hub d'événement d'Azure</span><span class="sxs-lookup"><span data-stu-id="0bd7d-238">Azure Event Hub</span></span>](https://azure.microsoft.com/services/event-hubs/)

[<span data-ttu-id="0bd7d-239">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0bd7d-239">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a><span data-ttu-id="0bd7d-240">Ingestion</span><span class="sxs-lookup"><span data-stu-id="0bd7d-240">Ingestion</span></span>
<span data-ttu-id="0bd7d-241">Combinaisons d’Azure Event Hubs, flux de données Analytique et Data Factory sont optimisées tooingest hello véhicule des signaux, événements de diagnostic hello et en temps réel et analytique du lot.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-241">Combinations of Azure Event Hubs, Stream Analytics, and Data Factory are leveraged tooingest hello vehicle signals, hello diagnostic events, and real-time and batch analytics.</span></span> <span data-ttu-id="0bd7d-242">Tous ces composants sont créés et configurés en tant que partie du déploiement d’une solution hello.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-242">All these components are created and configured as part of hello solution deployment.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="0bd7d-243">Analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="0bd7d-243">Real-time analysis</span></span>
<span data-ttu-id="0bd7d-244">Hello les événements générés par hello véhicule télématique simulateur sont publiés à l’aide du concentrateur d’événements toohello hello SDK de concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-244">hello events generated by hello Vehicle Telematics Simulator are published toohello Event Hub using hello Event Hub SDK.</span></span> <span data-ttu-id="0bd7d-245">tâche de flux de données Analytique Hello reçoit ces événements à partir de hello concentrateur d’événements et processus hello des données dans le contrôle d’intégrité du véhicule hello tooanalyze en temps réel.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-245">hello Stream Analytics job ingests these events from hello Event Hub and processes hello data in real time tooanalyze hello vehicle health.</span></span> 

![Tableau de bord Event Hub](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

<span data-ttu-id="0bd7d-247">*Figure 4 - Tableau de bord Event Hub*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-247">*Figure 4 - Event Hub dashboard*</span></span>

![Données de traitement de la tâche Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

<span data-ttu-id="0bd7d-249">*Figure 5 - Données de traitement de la tâche Stream Analytics*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-249">*Figure 5 - Stream Analytics job processing data*</span></span>

<span data-ttu-id="0bd7d-250">tâche de flux de données Analytique Hello ;</span><span class="sxs-lookup"><span data-stu-id="0bd7d-250">hello Stream Analytics job;</span></span>

* <span data-ttu-id="0bd7d-251">reçoit des données à partir de hello concentrateur d’événements</span><span class="sxs-lookup"><span data-stu-id="0bd7d-251">ingests data from hello Event Hub</span></span> 
* <span data-ttu-id="0bd7d-252">effectue une jointure avec hello référence toomap hello véhicule VIN toohello correspondante modèle de données</span><span class="sxs-lookup"><span data-stu-id="0bd7d-252">performs a join with hello reference data toomap hello vehicle VIN toohello corresponding model</span></span> 
* <span data-ttu-id="0bd7d-253">conserve les données dans le stockage Blob Azure pour une analyse en mode batch approfondie.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-253">persists them into Azure blob storage for rich batch analytics.</span></span> 

<span data-ttu-id="0bd7d-254">Hello suivant la requête de flux de données Analytique donnée utilisé toopersist hello dans le stockage d’objets blob Azure.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-254">hello following Stream Analytics query is used toopersist hello data into Azure blob storage.</span></span> 

![Requête de tâche Stream Analytics pour l’ingestion de données](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

<span data-ttu-id="0bd7d-256">*Figure 6 - Requête de tâche Stream Analytics pour l’ingestion de données*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-256">*Figure 6 - Stream Analytics job query for data ingestion*</span></span>

### <a name="batch-analysis"></a><span data-ttu-id="0bd7d-257">Analyse en mode batch</span><span class="sxs-lookup"><span data-stu-id="0bd7d-257">Batch analysis</span></span>
<span data-ttu-id="0bd7d-258">Nous allons également générer un volume supplémentaire de signaux de véhicules simulés ainsi qu’un jeu de données de diagnostic pour permettre une analyse en mode batch approfondie.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-258">We are also generating an additional volume of simulated vehicle signals and diagnostic dataset for richer batch analytics.</span></span> <span data-ttu-id="0bd7d-259">Il s’agit d’un volume de données représentatif pour le traitement par lots de tooensure requis.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-259">This is required tooensure a good representative data volume for batch processing.</span></span> <span data-ttu-id="0bd7d-260">Pour cela, nous utilisons un pipeline nommé « PrepareSampleDataPipeline » dans toogenerate de flux de travail Azure Data Factory hello année une de signaux de véhicule simulé et de jeu de données de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-260">For this purpose, we are using a pipeline named "PrepareSampleDataPipeline" in hello Azure Data Factory workflow toogenerate one year's worth of simulated vehicle signals and diagnostic dataset.</span></span> <span data-ttu-id="0bd7d-261">Cliquez sur [activité personnalisée de Data Factory](http://go.microsoft.com/fwlink/?LinkId=717077) hello de toodownload l’activité personnalisée DotNet solution Visual Studio pour les personnalisations de fabrique de données selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-261">Click [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload hello Data Factory custom DotNet activity Visual Studio solution for customizations based on your requirements.</span></span> 

![Préparer des exemples de données pour le workflow de traitement par lots](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

<span data-ttu-id="0bd7d-263">*Figure 7 - Préparer des exemples de données pour le workflow de traitement par lots*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-263">*Figure 7 - Prepare Sample data for batch processing workflow*</span></span>

<span data-ttu-id="0bd7d-264">pipeline de Hello se compose de définition d’application .net personnalisée activité, afficher ici :</span><span class="sxs-lookup"><span data-stu-id="0bd7d-264">hello pipeline consists of a custom ADF .Net Activity, show here:</span></span>

![Activité PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

<span data-ttu-id="0bd7d-266">*Figure 8 - PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-266">*Figure 8 - PrepareSampleDataPipeline*</span></span>

<span data-ttu-id="0bd7d-267">Une fois que hello pipeline exécute avec succès et le jeu de données « RawCarEventsTable » est marqué comme « Prêt », un an intéressant de signaux du véhicule simulé et diagnostic les données sont produites.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-267">Once hello pipeline executes successfully and "RawCarEventsTable" dataset is marked "Ready", one-year worth of simulated vehicle signals and diagnostic data are produced.</span></span> <span data-ttu-id="0bd7d-268">Hello suivante créée dans votre compte de stockage sous le conteneur de « connectedcar » hello de fichiers et de dossiers :</span><span class="sxs-lookup"><span data-stu-id="0bd7d-268">You see hello following folder and file created in your storage account under hello "connectedcar" container:</span></span>

![Sortie de PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

<span data-ttu-id="0bd7d-270">*Figure 9 - Sortie de PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-270">*Figure 9 - PrepareSampleDataPipeline Output*</span></span>

### <a name="references"></a><span data-ttu-id="0bd7d-271">Références</span><span class="sxs-lookup"><span data-stu-id="0bd7d-271">References</span></span>
[<span data-ttu-id="0bd7d-272">Kit Azure Event Hub SDK pour la réception de flux</span><span class="sxs-lookup"><span data-stu-id="0bd7d-272">Azure Event Hub SDK for stream ingestion</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

<span data-ttu-id="0bd7d-273">[Fonctionnalités de déplacement de données Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="0bd7d-273">[Azure Data Factory data movement capabilities](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span></span>

[<span data-ttu-id="0bd7d-274">Solution Azure Data Factory DotNet Activity Visual Studio pour la préparation des exemples de données</span><span class="sxs-lookup"><span data-stu-id="0bd7d-274">Azure Data Factory DotNet activity visual studio solution for preparing sample data</span></span>](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a><span data-ttu-id="0bd7d-275">Jeu de données de partition hello</span><span class="sxs-lookup"><span data-stu-id="0bd7d-275">Partition hello dataset</span></span>
<span data-ttu-id="0bd7d-276">Hello brut véhicule semi-structurées signaux et le jeu de données de diagnostic sont partitionnées à l’étape de préparation des données hello dans un format année/mois.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-276">hello raw semi-structured vehicle signals and diagnostic dataset are partitioned in hello data preparation step into a YEAR/MONTH format.</span></span> <span data-ttu-id="0bd7d-277">Ce partitionnement promeut une interrogation plus efficace et évolutif stockage à long terme en activant la panne d’un basculement à partir d’un objet blob compte toohello ensuite en tant que compte de première hello est saturé.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-277">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over from one blob account toohello next as hello first account fills up.</span></span> 

>[!NOTE] 
><span data-ttu-id="0bd7d-278">Cette étape de la solution de hello est le traitement de toobatch uniquement applicable.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-278">This step in hello solution is applicable only toobatch processing.</span></span>

<span data-ttu-id="0bd7d-279">Gestion des données d’entrée et de sortie :</span><span class="sxs-lookup"><span data-stu-id="0bd7d-279">Input and output data data management:</span></span>

* <span data-ttu-id="0bd7d-280">Hello **les données de sortie** (étiqueté *PartitionedCarEventsTable*) est toobe conservée pendant une longue période de temps en tant que formulaire de base / « rawest » hello des données dans « Data Lake « hello client.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-280">hello **output data** (labeled *PartitionedCarEventsTable*) is toobe kept for a long period of time as hello foundational/"rawest" form of data in hello customer's "Data Lake".</span></span> 
* <span data-ttu-id="0bd7d-281">Hello **les données d’entrée** toothis pipeline serait éliminée généralement en tant que données de sortie hello ont toohello une fidélité optimale d’entrée - il est stocké uniquement (partitionnée) mieux pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-281">hello **input data** toothis pipeline would typically be discarded as hello output data has full fidelity toohello input - it's just stored (partitioned) better for subsequent use.</span></span>

![Workflow Partition Car Events](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

<span data-ttu-id="0bd7d-283">*Figure 10 - Workflow Partition Car Events*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-283">*Figure 10 – Partition Car Events workflow*</span></span>

<span data-ttu-id="0bd7d-284">les données brutes Hello sont partitionnées à l’aide d’une activité de la ruche de HDInsight dans « PartitionCarEventsPipeline ».</span><span class="sxs-lookup"><span data-stu-id="0bd7d-284">hello raw data is partitioned using a Hive HDInsight activity in "PartitionCarEventsPipeline".</span></span> <span data-ttu-id="0bd7d-285">données d’exemple Hello générées à l’étape 1 pour une année sont partitionnées par année/mois.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-285">hello sample data generated in step 1 for a year is partitioned by YEAR/MONTH.</span></span> <span data-ttu-id="0bd7d-286">les partitions de Hello sont utilisées toogenerate véhicule signaux et les données de diagnostic pour chaque mois (12 partitions au total) d’une année.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-286">hello partitions are used toogenerate vehicle signals and diagnostic data for each month (total 12 partitions) of a year.</span></span> 

![Activité PartitionCarEventsPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

<span data-ttu-id="0bd7d-288">*Figure 11 - PartitionCarEventsPipeline*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-288">*Figure 11 - PartitionCarEventsPipeline*</span></span>

<span data-ttu-id="0bd7d-289">***Script Hive PartitionConnectedCarEvents***</span><span class="sxs-lookup"><span data-stu-id="0bd7d-289">***PartitionConnectedCarEvents Hive Script***</span></span>

<span data-ttu-id="0bd7d-290">Hello script Hive suivant, nommé « partitioncarevents.hql », est utilisé pour le partitionnement et se trouve dans le dossier « \demo\src\connectedcar\scripts » hello hello téléchargé zip.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-290">hello following Hive script, named "partitioncarevents.hql", is used for partitioning and is located in hello "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

<span data-ttu-id="0bd7d-291">Une fois que le pipeline de hello est exécutée avec succès, vous voyez hello suivant générées dans votre compte de stockage sous le conteneur de « connectedcar » hello de partitions.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-291">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Sortie partitionnée](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

<span data-ttu-id="0bd7d-293">*Figure 12 - Sortie partitionnée*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-293">*Figure 12 - Partitioned Output*</span></span>

<span data-ttu-id="0bd7d-294">les données de salutation est maintenant optimisée, est plus facile à gérer et prêt pour traitement insights de lot riche toogain.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-294">hello data is now optimized, is more manageable and ready for further processing toogain rich batch insights.</span></span> 

## <a name="data-analysis"></a><span data-ttu-id="0bd7d-295">Analyse des données</span><span class="sxs-lookup"><span data-stu-id="0bd7d-295">Data Analysis</span></span>
<span data-ttu-id="0bd7d-296">Dans cette section, vous voyez comment toocombine Analytique de flux de données Azure, Azure Machine Learning, Azure Data Factory et Azure HDInsight pour enrichi avancé analytique sur l’intégrité du véhicule et du pilotage habituelles.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-296">In this section, you see how toocombine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory, and Azure HDInsight for rich advanced analytics on vehicle health and driving habits.</span></span> <span data-ttu-id="0bd7d-297">Elle est divisée en trois sous-sections :</span><span class="sxs-lookup"><span data-stu-id="0bd7d-297">There are three subsections here:</span></span>

1. <span data-ttu-id="0bd7d-298">**Apprentissage**: cette sous-section contient des informations sur l’expérience de détection d’anomalie hello que nous avons utilisé dans cette solution toopredict véhicule maintenance véhicules nécessitant des rappels en raison de problèmes de toosafety et maintenance.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-298">**Machine Learning**: This subsection contains information on hello anomaly detection experiment that we have used in this solution toopredict vehicles requiring servicing maintenance and vehicles requiring recalls due toosafety issues.</span></span>
2. <span data-ttu-id="0bd7d-299">**Analyse en temps réel**: cette sous-section contient des informations concernant analytique en temps réel hello à l’aide de hello langage de requête Analytique de flux et Opérationnalisation apprentissage hello faire des essais en temps réel à l’aide d’une application personnalisée.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-299">**Real-time analysis**: This subsection contains information regarding hello real-time analytics using hello Stream Analytics Query Language and operationalizing hello machine learning experiment in real time using a custom application.</span></span>
3. <span data-ttu-id="0bd7d-300">**Analyse du lot**: cette sous-section contient des informations hello transformation et le traitement des données de traitement par lots de hello à l’aide d’Azure HDInsight et Azure Machine Learning mis par Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-300">**Batch analysis**: This subsection contains information regarding hello transforming and processing of hello batch data using Azure HDInsight and Azure Machine Learning operationalized by Azure Data Factory.</span></span>

### <a name="machine-learning"></a><span data-ttu-id="0bd7d-301">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0bd7d-301">Machine Learning</span></span>
<span data-ttu-id="0bd7d-302">Notre objectif ici est véhicules hello toopredict qui nécessitent une maintenance ou rappel, en fonction de certaines statistiques de contrôle d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-302">Our goal here is toopredict hello vehicles that require maintenance or recall based on certain heath statistics.</span></span> <span data-ttu-id="0bd7d-303">Nous faisons hello suivant hypothèses</span><span class="sxs-lookup"><span data-stu-id="0bd7d-303">We make hello following assumptions</span></span>

* <span data-ttu-id="0bd7d-304">Si un des hello trois conditions suivantes est remplie, les véhicules hello nécessitent **maintenance maintenance**:</span><span class="sxs-lookup"><span data-stu-id="0bd7d-304">If one of hello following three conditions are true, hello vehicles require **servicing maintenance**:</span></span>
  
  * <span data-ttu-id="0bd7d-305">La pression des pneus faible</span><span class="sxs-lookup"><span data-stu-id="0bd7d-305">Tire pressure is low</span></span>
  * <span data-ttu-id="0bd7d-306">Le niveau d’huile moteur est faible</span><span class="sxs-lookup"><span data-stu-id="0bd7d-306">Engine oil level is low</span></span>
  * <span data-ttu-id="0bd7d-307">La température du moteur est élevée</span><span class="sxs-lookup"><span data-stu-id="0bd7d-307">Engine temperature is high</span></span>
* <span data-ttu-id="0bd7d-308">Si l’une des conditions suivantes de hello est true, les véhicules hello peuvent avoir un **problème de sécurité** et nécessitent **rappel**:</span><span class="sxs-lookup"><span data-stu-id="0bd7d-308">If one of hello following conditions are true, hello vehicles may have a **safety issue** and require **recall**:</span></span>
  
  * <span data-ttu-id="0bd7d-309">La température du moteur est élevée mais la température extérieure est faible</span><span class="sxs-lookup"><span data-stu-id="0bd7d-309">Engine temperature is high but outside temperature is low</span></span>
  * <span data-ttu-id="0bd7d-310">La température du moteur est faible mais la température extérieure est élevée</span><span class="sxs-lookup"><span data-stu-id="0bd7d-310">Engine temperature is low but outside temperature is high</span></span>

<span data-ttu-id="0bd7d-311">Selon les exigences précédentes hello, nous avons créé des anomalies de toodetect deux modèles séparés, un pour la détection de maintenance véhicule et un pour la détection de rappel véhicule.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-311">Based on hello previous requirements, we have created two separate models toodetect anomalies, one for vehicle maintenance detection, and one for vehicle recall detection.</span></span> <span data-ttu-id="0bd7d-312">Dans ces deux modèles, algorithme d’analyse du composant Principal (PCA) intégré hello est utilisé pour la détection d’anomalie.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-312">In both these models, hello built-in Principal Component Analysis (PCA) algorithm is used for anomaly detection.</span></span> 

<span data-ttu-id="0bd7d-313">**Modèle de détection de maintenance**</span><span class="sxs-lookup"><span data-stu-id="0bd7d-313">**Maintenance detection model**</span></span>

<span data-ttu-id="0bd7d-314">Si un des trois indicateurs de pression des pneus, pétrole du moteur ou température moteur - satisfait à sa condition respectif, modèle de détection de maintenance hello signale une anomalie.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-314">If one of three indicators - tire pressure, engine oil, or engine temperature - satisfies its respective condition, hello maintenance detection model reports an anomaly.</span></span> <span data-ttu-id="0bd7d-315">Par conséquent, nous avons besoin uniquement tooconsider ces trois variables de la création du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-315">As a result, we only need tooconsider these three variables in building hello model.</span></span> <span data-ttu-id="0bd7d-316">Dans notre expérience dans Azure Machine Learning, nous avons tout d’abord utiliser un **sélectionner les colonnes dans le jeu de données** module tooextract ces trois variables.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-316">In our experiment in Azure Machine Learning, we first use a **Select Columns in Dataset** module tooextract these three variables.</span></span> <span data-ttu-id="0bd7d-317">Ensuite, nous utilisons modèle de détection d’anomalie module toobuild hello hello d’anomalie basée sur l’ACP détection.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-317">Next we use hello PCA-based anomaly detection module toobuild hello anomaly detection model.</span></span> 

<span data-ttu-id="0bd7d-318">Analyse des composants principaux (PCA) est une technique d’apprentissage automatique qui peut être appliqué toofeature la détection d’anomalies, la classification et la sélection.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-318">Principal Component Analysis (PCA) is an established technique in machine learning that can be applied toofeature selection, classification, and anomaly detection.</span></span> <span data-ttu-id="0bd7d-319">PCA convertit un ensemble de cas contenant des variables potentiellement corrélées en un ensemble de valeurs appelées composants principaux.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-319">PCA converts a set of case containing possibly correlated variables, into a set of values called principal components.</span></span> <span data-ttu-id="0bd7d-320">idée de clé Hello de modélisation basés sur l’ACP est tooproject des données sur un espace 3D inférieur afin que les fonctionnalités et les anomalies peuvent être plus facilement identifiables.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-320">hello key idea of PCA-based modeling is tooproject data onto a lower-dimensional space so that features and anomalies can be more easily identified.</span></span>

<span data-ttu-id="0bd7d-321">Pour chaque nouvelle entrée hello trop de modèle de détection, détecteur d’anomalie de hello calcule d’abord sa projection sur des vecteurs propres de hello, et puis calcule hello normalisée erreur de reconstruction.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-321">For each new input too hello detection model, hello anomaly detector first computes its projection on hello eigenvectors, and then computes hello normalized reconstruction error.</span></span> <span data-ttu-id="0bd7d-322">Cette erreur normalisée est score d’anomalie hello.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-322">This normalized error is hello anomaly score.</span></span> <span data-ttu-id="0bd7d-323">Erreur de hello Hello supérieur, hello anormale hello instance est.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-323">hello higher hello error, hello more anomalous hello instance is.</span></span> 

<span data-ttu-id="0bd7d-324">Problème de détection de maintenance hello, chaque enregistrement peut être considéré comme un point dans un espace 3D défini par pression des pneus pétrole de moteur et la température du moteur coordonnées.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-324">In hello maintenance detection problem, each record can be considered as a point in a 3-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span></span> <span data-ttu-id="0bd7d-325">toocapture ces anomalies, nous pouvons hello d’origine données projet dans un espace 3D hello sur un espace de 2 dimensions à l’aide de l’ACP.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-325">toocapture these anomalies, we can project hello original data in hello 3-dimensional space onto a 2-dimensional space using PCA.</span></span> <span data-ttu-id="0bd7d-326">Par conséquent, nous avons défini le paramètre hello nombre de composants toouse dans l’ACP toobe 2.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-326">Thus, we set hello parameter Number of components toouse in PCA toobe 2.</span></span> <span data-ttu-id="0bd7d-327">Ce paramètre joue un rôle important dans l’application de la détection d’anomalies basée sur l’algorithme PCA.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-327">This parameter plays an important role in applying PCA-based anomaly detection.</span></span> <span data-ttu-id="0bd7d-328">Une fois les données projetées à l’aide de PCA, nous pouvons identifier plus facilement ces anomalies.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-328">After projecting data using PCA, we can identify these anomalies more easily.</span></span>

<span data-ttu-id="0bd7d-329">**Modèle de détection d’anomalie de rappel** dans le modèle de détection d’anomalies hello rappel, nous utilisons hello sélectionner les colonnes dans le jeu de données et d’anomalies basé sur l’ACP modules de détection de la même façon.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-329">**Recall anomaly detection model** In hello recall anomaly detection model, we use hello Select Columns in Dataset and PCA-based anomaly detection modules in a similar way.</span></span> <span data-ttu-id="0bd7d-330">Plus précisément, nous avons tout d’abord extraire trois variables - température du moteur, la température en dehors et vitesse - à l’aide de hello **sélectionner les colonnes dans le jeu de données** module.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-330">Specifically, we first extract three variables - engine temperature, outside temperature, and speed - using hello **Select Columns in Dataset** module.</span></span> <span data-ttu-id="0bd7d-331">Nous avons également inclure la vitesse hello variable étant donné que la température du moteur hello est généralement mis en corrélation toohello vitesse.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-331">We also include hello speed variable since hello engine temperature typically is correlated toohello speed.</span></span> <span data-ttu-id="0bd7d-332">Ensuite, nous utilisons les données hello tooproject du module de détection d’anomalie basée sur l’ACP d’espace 3D de hello sur un espace de 2 dimensions.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-332">Next we use PCA-based anomaly detection module tooproject hello data from hello 3-dimensional space onto a 2-dimensional space.</span></span> <span data-ttu-id="0bd7d-333">critères de rappel Hello sont satisfaites et véhicule de hello exige rappel lors de la température du moteur et température extérieure sont hautement négativement corrélés.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-333">hello recall criteria are satisfied and so hello vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span></span> <span data-ttu-id="0bd7d-334">À l’aide d’algorithme de détection d’anomalie basée sur l’ACP, nous pouvons capturer les anomalies hello après avoir effectué l’ACP.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-334">Using PCA-based anomaly detection algorithm, we can capture hello anomalies after performing PCA.</span></span> 

<span data-ttu-id="0bd7d-335">Lors de l’apprentissage d’un modèle, nous devons toouse données normales, qui ne nécessitent pas de maintenance ou rappel en tant que modèle de détection d’anomalie basée sur l’ACP hello des données d’entrée tootrain hello.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-335">When training either model, we need toouse normal data, which does not require maintenance or recall as hello input data tootrain hello PCA-based anomaly detection model.</span></span> <span data-ttu-id="0bd7d-336">Bonjour expérience de score, nous utilisons hello formé d’anomalie détection modèle toodetect véhicule de hello nécessite la maintenance ou rappel ou non.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-336">In hello scoring experiment, we use hello trained anomaly detection model toodetect whether or not hello vehicle requires maintenance or recall.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="0bd7d-337">Analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="0bd7d-337">Real-time analysis</span></span>
<span data-ttu-id="0bd7d-338">Hello suivant du flux de données Analytique la requête SQL est utilisé moyenne de hello tooget de toutes les hello paramètres véhicule importantes telles que la vitesse du véhicule, niveau de carburant, température du moteur, kilométrique, la pression des pneus, au niveau du moteur pétrole et d’autres.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-338">hello following Stream Analytics SQL Query is used tooget hello average of all hello important vehicle parameters like vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span></span> <span data-ttu-id="0bd7d-339">Hello moyennes sont utilisées toodetect anomalies, émettre des alertes et déterminer hello des conditions de contrôle d’intégrité global de véhicules utilisés dans une région spécifique et le corréler puis toodemographics.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-339">hello averages are used toodetect anomalies, issue alerts, and determine hello overall health conditions of vehicles operated in specific region and then correlate it toodemographics.</span></span> 

![Requête Stream Analytics pour le traitement en temps réel](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

<span data-ttu-id="0bd7d-341">*Figure 13 - Requête Stream Analytics pour le traitement en temps réel*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-341">*Figure 13 – Stream Analytics query for real-time processing*</span></span>

<span data-ttu-id="0bd7d-342">Toutes les moyennes de hello sont calculés sur un TumblingWindow de 3 secondes.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-342">All hello averages are calculated over a 3-second TumblingWindow.</span></span> <span data-ttu-id="0bd7d-343">Nous utilisons TubmlingWindow dans ce cas car nous avons besoin d’intervalles de temps contigus et sans chevauchement.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-343">We are using TubmlingWindow in this case since we require non-overlapping and contiguous time intervals.</span></span> 

<span data-ttu-id="0bd7d-344">toolearn en savoir plus sur toutes les fonctionnalités de « Fenêtrage » hello dans Azure Analytique de flux de données, cliquez sur [fenêtrage (Analytique de flux de données Azure)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span><span class="sxs-lookup"><span data-stu-id="0bd7d-344">toolearn more about all hello "Windowing" capabilities in Azure Stream Analytics, click [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

<span data-ttu-id="0bd7d-345">**Prédiction en temps réel**</span><span class="sxs-lookup"><span data-stu-id="0bd7d-345">**Real-time prediction**</span></span>

<span data-ttu-id="0bd7d-346">Une application est incluse dans le cadre du modèle d’apprentissage de solution toooperationalize hello hello en temps réel.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-346">An application is included as part of hello solution toooperationalize hello machine learning model in real time.</span></span> <span data-ttu-id="0bd7d-347">Cette application appelée « RealTimeDashboardApp » est créée et configurée en tant que partie du déploiement d’une solution hello.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-347">This application called “RealTimeDashboardApp” is created and configured as part of hello solution deployment.</span></span> <span data-ttu-id="0bd7d-348">application Hello exécute des actions suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="0bd7d-348">hello application performs hello following:</span></span>

1. <span data-ttu-id="0bd7d-349">Écoute l’instance de concentrateur d’événements tooan où Analytique de flux de données est événements de publication hello dans un modèle en permanence.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-349">Listens tooan Event Hub instance where Stream Analytics is publishing hello events in a pattern continuously.</span></span> <span data-ttu-id="0bd7d-350">![Requête Analytique de flux de données pour la publication des données de salutation](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 : requête Analytique de flux de données pour la publication hello données tooan instance de concentrateur d’événements de sortie*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-350">![Stream Analytics query for publishing hello data](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 – Stream Analytics query for publishing hello data tooan output Event Hub instance*</span></span> 
2. <span data-ttu-id="0bd7d-351">Pour chaque événement reçu par cette application :</span><span class="sxs-lookup"><span data-stu-id="0bd7d-351">For every event that this application receives:</span></span> 
   
   * <span data-ttu-id="0bd7d-352">Traite les données hello à l’aide du point de terminaison de Machine Learning demande-réponse de calcul de score (RR).</span><span class="sxs-lookup"><span data-stu-id="0bd7d-352">Processes hello data using Machine Learning Request-Response Scoring (RRS) endpoint.</span></span> <span data-ttu-id="0bd7d-353">point de terminaison RR Hello est automatiquement publié dans le cadre du déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-353">hello RRS endpoint is automatically published as part of hello deployment.</span></span>
   * <span data-ttu-id="0bd7d-354">sortie d’enregistrements de ressources Hello est publié tooa jeu de données de Power BI à l’aide de push de hello API.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-354">hello RRS output is published tooa Power BI dataset using hello push APIs.</span></span>

<span data-ttu-id="0bd7d-355">Ce modèle est également applicable tooscenarios dans lequel vous souhaitez toointegrate une application métier (LoB) avec un flux hello analytique en temps réel, des scénarios tels que des alertes, notifications et la messagerie.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-355">This pattern is also applicable tooscenarios in which you want toointegrate a Line of Business (LoB) application with hello real-time analytics flow, for scenarios such as alerts, notifications, and messaging.</span></span>

<span data-ttu-id="0bd7d-356">Cliquez sur [RealtimeDashboardApp téléchargement](http://go.microsoft.com/fwlink/?LinkId=717078) hello de toodownload solution RealtimeDashboardApp Visual Studio pour les personnalisations.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-356">Click [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) toodownload hello RealtimeDashboardApp Visual Studio solution for customizations.</span></span> 

<span data-ttu-id="0bd7d-357">**tooexecute hello Application de tableau de bord en temps réel**</span><span class="sxs-lookup"><span data-stu-id="0bd7d-357">**tooexecute hello Real-time Dashboard Application**</span></span>
1. <span data-ttu-id="0bd7d-358">Extrayez le fichier et enregistrez-le localement ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – Dossier RealtimeDashboardApp*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-358">Extract and save locally ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – RealtimeDashboardApp folder*</span></span>  
2. <span data-ttu-id="0bd7d-359">Exécutez l’application hello RealtimeDashboardApp.exe</span><span class="sxs-lookup"><span data-stu-id="0bd7d-359">Execute hello application RealtimeDashboardApp.exe</span></span>
3. <span data-ttu-id="0bd7d-360">Entrez des informations d’identification Power BI valides, connectez-vous, puis cliquez sur Accept</span><span class="sxs-lookup"><span data-stu-id="0bd7d-360">Provide valid Power BI credentials, sign in and click Accept</span></span> ![Application de tableau de bord en temps réel connectez-vous tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Application de tableau de bord en temps réel terminer connectez-vous tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

<span data-ttu-id="0bd7d-363">*Figure 17 – RealtimeDashboardApp : Connectez-vous tooPower BI*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-363">*Figure 17 – RealtimeDashboardApp: Sign-in tooPower BI*</span></span>

>[!NOTE] 
><span data-ttu-id="0bd7d-364">Si vous souhaitez que le jeu de données Power BI tooflush hello, exécutez hello RealtimeDashboardApp avec le paramètre « flushdata » hello :</span><span class="sxs-lookup"><span data-stu-id="0bd7d-364">If you want tooflush hello Power BI dataset, execute hello RealtimeDashboardApp with hello "flushdata" parameter:</span></span> 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a><span data-ttu-id="0bd7d-365">Analyse en mode batch</span><span class="sxs-lookup"><span data-stu-id="0bd7d-365">Batch analysis</span></span>
<span data-ttu-id="0bd7d-366">Hello ici vise tooshow comment Contoso auto utilise hello calcul Azure fonctionnalités tooharness données big toogain un éclairage sur gérant le modèle, le comportement de l’utilisation et d’intégrité du véhicule.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-366">hello goal here is tooshow how Contoso Motors utilizes hello Azure compute capabilities tooharness big data toogain rich insights on driving pattern, usage behavior, and vehicle health.</span></span> <span data-ttu-id="0bd7d-367">Il est ainsi possible :</span><span class="sxs-lookup"><span data-stu-id="0bd7d-367">This makes it possible to:</span></span>

* <span data-ttu-id="0bd7d-368">Améliorer l’expérience utilisateur hello et la rendre plus économique en fournissant des analyses sur la conduite des habitudes et les comportements de conduite efficace de carburant</span><span class="sxs-lookup"><span data-stu-id="0bd7d-368">Improve hello customer experience and make it cheaper by providing insights on driving habits and fuel efficient driving behaviors</span></span>
* <span data-ttu-id="0bd7d-369">En savoir plus proactive concernant les clients et leurs décisions toogovern connues conduite et fournir hello mieux classe produits et services</span><span class="sxs-lookup"><span data-stu-id="0bd7d-369">Learn proactively about customers and their driving patters toogovern business decisions and provide hello best in class products & services</span></span>

<span data-ttu-id="0bd7d-370">Dans cette solution, nous prévoyons hello suivant des métriques :</span><span class="sxs-lookup"><span data-stu-id="0bd7d-370">In this solution, we are targeting hello following metrics:</span></span>

1. <span data-ttu-id="0bd7d-371">**Agressif gèrent le comportement**: identifie la tendance de hello des modèles de hello, des emplacements, déterminant conditions et temps d’aperçus de toogain année hello sur les modèles de conduite agressives.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-371">**Aggressive driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on aggressive driving patterns.</span></span> <span data-ttu-id="0bd7d-372">Contoso Motors peut utiliser ces informations pour ses campagnes marketing, pour créer de nouvelles fonctionnalités personnalisées et pour proposer des assurances adaptées à l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-372">Contoso Motors can use these insights for marketing campaigns, driving new personalized features and usage-based insurance.</span></span>
2. <span data-ttu-id="0bd7d-373">**Comportement de conduite efficace de carburant**: identifie tendance hello de modèles de hello, emplacements, déterminant conditions et de temps d’aperçus de toogain année hello sur les modèles de conduite efficace de carburant.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-373">**Fuel efficient driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on fuel efficient driving patterns.</span></span> <span data-ttu-id="0bd7d-374">Moteurs de Contoso peut utiliser ces aperçus pour les campagnes marketing gérant les nouvelles fonctionnalités et proactive reporting toohello pilotes coûtent effectif et environnement convivial conduite des habitudes.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-374">Contoso Motors can use these insights for marketing campaigns, driving new features and proactive reporting toohello drivers for cost effective and environment friendly driving habits.</span></span> 
3. <span data-ttu-id="0bd7d-375">**Modèles de rappeler**: identifie les modèles nécessiter des rappels d’expérience d’apprentissage de la détection d’anomalie hello à mettre en application</span><span class="sxs-lookup"><span data-stu-id="0bd7d-375">**Recall models**: Identifies models requiring recalls by operationalizing hello anomaly detection machine learning experiment</span></span>

<span data-ttu-id="0bd7d-376">Nous allons examiner en détail chacune de ces métriques, hello</span><span class="sxs-lookup"><span data-stu-id="0bd7d-376">Let's look into hello details of each of these metrics,</span></span>

<span data-ttu-id="0bd7d-377">**Mode de conduite agressive**</span><span class="sxs-lookup"><span data-stu-id="0bd7d-377">**Aggressive driving pattern**</span></span>

<span data-ttu-id="0bd7d-378">Hello partitionnée véhicule signaux et les données de diagnostic sont traitées dans le pipeline de hello nommé « AggresiveDrivingPatternPipeline » à l’aide de modèles de ruche toodetermine hello, l’emplacement, véhicule, véhicule conditions et autres paramètres qui expose agressif modèle de commande.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-378">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "AggresiveDrivingPatternPipeline" using Hive toodetermine hello models, location, vehicle, driving conditions, and other parameters that exhibits aggressive driving pattern.</span></span>

<span data-ttu-id="0bd7d-379">![Workflow de modèle conduite agressive](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Workflow de modèle conduite agressive*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-379">![Aggressive driving pattern workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Aggressive driving pattern workflow*</span></span>


<span data-ttu-id="0bd7d-380">***Requête Hive de mode de conduite agressive***</span><span class="sxs-lookup"><span data-stu-id="0bd7d-380">***Aggressive driving pattern Hive query***</span></span>

<span data-ttu-id="0bd7d-381">Hello script Hive nommé « aggresivedriving.hql » est utilisé pour analyser le modèle de condition déterminant agressif se trouve dans le dossier « \demo\src\connectedcar\scripts » de hello téléchargé zip.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-381">hello Hive script named "aggresivedriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


<span data-ttu-id="0bd7d-382">Elle utilise la combinaison hello du véhicule position de vitesse de transmission, état pédales de frein et vitesse toodetect reckless/agressif gèrent le comportement en fonction de frein modèle à grande vitesse.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-382">It uses hello combination of vehicle's transmission gear position, brake pedal status, and speed toodetect reckless/aggressive driving behavior based on braking pattern at high speed.</span></span> 

<span data-ttu-id="0bd7d-383">Une fois que le pipeline de hello est exécutée avec succès, vous voyez hello suivant générées dans votre compte de stockage sous le conteneur de « connectedcar » hello de partitions.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-383">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Sortie AggressiveDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

<span data-ttu-id="0bd7d-385">*Figure 19 – Sortie AggressiveDrivingPatternPipeline*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-385">*Figure 19 – AggressiveDrivingPatternPipeline output*</span></span>

<span data-ttu-id="0bd7d-386">**Mode de conduite économe en carburant**</span><span class="sxs-lookup"><span data-stu-id="0bd7d-386">**Fuel efficient driving pattern**</span></span>

<span data-ttu-id="0bd7d-387">Hello partitionnée véhicule signaux et données de diagnostic sont traitées en pipeline hello nommé « FuelEfficientDrivingPatternPipeline ».</span><span class="sxs-lookup"><span data-stu-id="0bd7d-387">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "FuelEfficientDrivingPatternPipeline".</span></span> <span data-ttu-id="0bd7d-388">Ruche est utilisé toodetermine hello modèles, emplacement, véhicule, conditions de conduite et autres propriétés qui exposent le modèle conduite efficace de carburant.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-388">Hive is used toodetermine hello models, location, vehicle, driving conditions, and other properties that exhibit fuel efficient driving pattern.</span></span>

![Mode de conduite économe en carburant](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

<span data-ttu-id="0bd7d-390">*Figure 20 - Workflow du mode de conduite économe en carburant*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-390">*Figure 20 – Fuel-efficient driving pattern workflow*</span></span>

<span data-ttu-id="0bd7d-391">***Requête Hive du mode de conduite économe en carburant***</span><span class="sxs-lookup"><span data-stu-id="0bd7d-391">***Fuel efficient driving pattern Hive query***</span></span>

<span data-ttu-id="0bd7d-392">Hello script Hive nommé « fuelefficientdriving.hql » est utilisé pour analyser le modèle de condition déterminant agressif se trouve dans le dossier « \demo\src\connectedcar\scripts » de hello téléchargé zip.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-392">hello Hive script named "fuelefficientdriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


<span data-ttu-id="0bd7d-393">Il utilise combinaison de hello de position de vitesse de transmission du véhicule, l’état de pédales frein, vitesse et carburant de toodetect position pédales accélérateur comportement conduite efficace en fonction de l’accélération, frein, et accélérer les modèles.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-393">It uses hello combination of vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position toodetect fuel efficient driving behavior based on acceleration, braking, and speed patterns.</span></span> 

<span data-ttu-id="0bd7d-394">Une fois que le pipeline de hello est exécutée avec succès, vous voyez hello suivant générées dans votre compte de stockage sous le conteneur de « connectedcar » hello de partitions.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-394">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Sortie FuelEfficientDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

<span data-ttu-id="0bd7d-396">*Figure 21 – Sortie FuelEfficientDrivingPatternPipeline*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-396">*Figure 21 – FuelEfficientDrivingPatternPipeline output*</span></span>

<span data-ttu-id="0bd7d-397">**Prédictions des rappels**</span><span class="sxs-lookup"><span data-stu-id="0bd7d-397">**Recall Predictions**</span></span>

<span data-ttu-id="0bd7d-398">expérience d’apprentissage Hello est configuré et publié comme un service web dans le cadre du déploiement de solutions hello.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-398">hello machine learning experiment is provisioned and published as a web service as part of hello solution deployment.</span></span> <span data-ttu-id="0bd7d-399">lot Hello calcul du score du point de terminaison est exploitée dans ce flux de travail, mis à l’aide des activités de score par lot d’une fabrique de données et enregistré comme un service lié de fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-399">hello batch scoring end point is leveraged in this workflow, registered as a data factory linked service and operationalized using data factory batch scoring activity.</span></span>

![Point de terminaison Machine Learning](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

<span data-ttu-id="0bd7d-401">*Figure 22 – Point de terminaison Machine Learning enregistré comme service lié dans Data Factory*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-401">*Figure 22 – Machine learning endpoint registered as a linked service in data factory*</span></span>

<span data-ttu-id="0bd7d-402">Hello service lié inscrit est utilisé dans les données de salutation hello DetectAnomalyPipeline tooscore à l’aide du modèle de détection d’anomalie hello.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-402">hello registered linked service is used in hello DetectAnomalyPipeline tooscore hello data using hello anomaly detection model.</span></span> 

![Activité de notation par lot de Machine Learning dans Data Factory](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

<span data-ttu-id="0bd7d-404">*Figure 23 – Activité de notation par lot d’Azure Machine Learning dans Data Factory*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-404">*Figure 23 – Azure Machine Learning Batch Scoring activity in data factory*</span></span> 

<span data-ttu-id="0bd7d-405">Il existe quelques étapes effectuées dans ce pipeline pour préparer les données afin qu’il peut être operationalized avec lot hello calcul du score du service web.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-405">There are few steps performed in this pipeline for data preparation so that it can be operationalized with hello batch scoring web service.</span></span> 

![DetectAnomalyPipeline pour la prédiction des véhicules nécessitant des rappels](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

<span data-ttu-id="0bd7d-407">*Figure 24 – DetectAnomalyPipeline pour la prédiction des véhicules nécessitant des rappels*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-407">*Figure 24 – DetectAnomalyPipeline for predicting vehicles requiring recalls*</span></span> 

<span data-ttu-id="0bd7d-408">***Requête Hive de détection des anomalies***</span><span class="sxs-lookup"><span data-stu-id="0bd7d-408">***Anomaly detection Hive query***</span></span>

<span data-ttu-id="0bd7d-409">Une fois que le calcul de score hello est terminée, une activité HDInsight est tooprocess utilisé et les données d’agrégation hello sont classées en tant que les anomalies par modèle hello avec un score de probabilité de 0,60 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-409">Once hello scoring is completed, an HDInsight activity is used tooprocess and aggregate hello data that are categorized as anomalies by hello model with a probability score of 0.60 or higher.</span></span>

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


<span data-ttu-id="0bd7d-410">Une fois que le pipeline de hello est exécutée avec succès, vous voyez hello suivant générées dans votre compte de stockage sous le conteneur de « connectedcar » hello de partitions.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-410">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Sortie DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

<span data-ttu-id="0bd7d-412">*Figure 25 – Sortie DetectAnomalyPipeline*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-412">*Figure 25 – DetectAnomalyPipeline output*</span></span>

## <a name="publish"></a><span data-ttu-id="0bd7d-413">Publier</span><span class="sxs-lookup"><span data-stu-id="0bd7d-413">Publish</span></span>

### <a name="real-time-analysis"></a><span data-ttu-id="0bd7d-414">Analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="0bd7d-414">Real-time analysis</span></span>
<span data-ttu-id="0bd7d-415">Une des requêtes hello dans la tâche de flux de données Analytique hello publie la sortie des tooan événements hello instance de concentrateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-415">One of hello queries in hello Stream Analytics job publishes hello events tooan output Event Hub instance.</span></span> 

![Tâche de flux de données Analytique publie tooan sortie instance de concentrateur d’événements](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

<span data-ttu-id="0bd7d-417">*Figure 26 : tâche de flux de données Analytique publie la sortie de tooan instance de concentrateur d’événements*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-417">*Figure 26 – Stream Analytics job publishes tooan output Event Hub instance*</span></span>

![Instance de concentrateur d’événements de sortie de flux de données Analytique requête toopublish toohello](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

<span data-ttu-id="0bd7d-419">*Figure 27 : instance de concentrateur d’événements de sortie de flux de données Analytique requête toopublish toohello*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-419">*Figure 27 – Stream Analytics query toopublish toohello output Event Hub instance*</span></span>

<span data-ttu-id="0bd7d-420">Ce flux d’événements est consommé par hello que realtimedashboardapp inclus dans les solutions hello.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-420">This stream of events is consumed by hello RealTimeDashboardApp included in hello solution.</span></span> <span data-ttu-id="0bd7d-421">Cette application utilise le service de service web de requête-réponse de Machine Learning hello pour calculer les scores en temps réel et publie hello données résultantes tooa Power BI dataset pour la consommation.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-421">This application leverages hello Machine Learning Request-Response web service for real-time scoring and publishes hello resultant data tooa Power BI dataset for consumption.</span></span> 

### <a name="batch-analysis"></a><span data-ttu-id="0bd7d-422">Analyse en mode batch</span><span class="sxs-lookup"><span data-stu-id="0bd7d-422">Batch analysis</span></span>
<span data-ttu-id="0bd7d-423">résultats de Hello du lot de hello et de traitement en temps réel sont publiées toohello des tables de base de données SQL Azure pour la consommation.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-423">hello results of hello batch and real-time processing are published toohello Azure SQL Database tables for consumption.</span></span> <span data-ttu-id="0bd7d-424">Bonjour Azure SQL Server, base de données et les tables de hello sont créés automatiquement en tant que partie du script de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-424">hello Azure SQL Server, Database, and hello tables are created automatically as part of hello setup script.</span></span> 

![Résultats du traitement par lots Copier le flux de travail toodata mart](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

<span data-ttu-id="0bd7d-426">*Figure 28 – résultats de la copie toodata mart workflow de traitement par lots*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-426">*Figure 28 – Batch processing results copy toodata mart workflow*</span></span>

![Tâche de flux de données Analytique publie toodata mart](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

<span data-ttu-id="0bd7d-428">*Figure 29 : tâche de flux de données Analytique publie toodata mart*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-428">*Figure 29 – Stream Analytics job publishes toodata mart*</span></span>

![Configuration de l’entrepôt de données dans la tâche Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

<span data-ttu-id="0bd7d-430">*Figure 30 – Configuration de l’entrepôt de données dans la tâche Stream Analytics*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-430">*Figure 30 – Data mart setting in Stream Analytics job*</span></span>

## <a name="consume"></a><span data-ttu-id="0bd7d-431">Utiliser</span><span class="sxs-lookup"><span data-stu-id="0bd7d-431">Consume</span></span>
<span data-ttu-id="0bd7d-432">Power BI offre à cette solution un tableau de bord complet permettant de visualiser à la fois les données en temps réel et les analyses prédictives.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-432">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="0bd7d-433">Cliquez ici pour obtenir des instructions détaillées sur la configuration des rapports de Power BI hello et tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-433">Click here for detailed instructions on setting up hello Power BI reports and hello dashboard.</span></span> <span data-ttu-id="0bd7d-434">tableau de bord Hello final ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="0bd7d-434">hello final dashboard looks like this:</span></span>

![Tableau de bord Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

<span data-ttu-id="0bd7d-436">*Figure 31 - Tableau de bord Power BI*</span><span class="sxs-lookup"><span data-stu-id="0bd7d-436">*Figure 31 - Power BI Dashboard*</span></span>

## <a name="summary"></a><span data-ttu-id="0bd7d-437">Résumé</span><span class="sxs-lookup"><span data-stu-id="0bd7d-437">Summary</span></span>
<span data-ttu-id="0bd7d-438">Ce document contient une exploration détaillée de hello véhicule télémétrie Analytique Solution.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-438">This document contains a detailed drill-down of hello Vehicle Telemetry Analytics Solution.</span></span> <span data-ttu-id="0bd7d-439">Il présente un modèle d’architecture lambda pour une analyse en temps réel et par lots reposant sur des prédictions et des actions.</span><span class="sxs-lookup"><span data-stu-id="0bd7d-439">This showcases a lambda architecture pattern for real-time and batch analytics with predictions and actions.</span></span> <span data-ttu-id="0bd7d-440">Ce modèle s’applique tooa large éventail de cas d’usage qui requièrent chemin réactif (en temps réel) et analytique de chemin d’accès à froid (lot).</span><span class="sxs-lookup"><span data-stu-id="0bd7d-440">This pattern applies tooa wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span></span> 

