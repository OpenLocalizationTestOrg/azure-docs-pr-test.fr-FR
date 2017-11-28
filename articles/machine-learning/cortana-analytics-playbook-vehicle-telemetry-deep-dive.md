---
title: "Découvrir de manière approfondie la prédiction de l’état des véhicules et les habitudes de conduite | Microsoft Docs"
description: "Utilisez les fonctionnalités de Cortana Intelligence pour obtenir des informations en temps réel et prédictives sur l’état des véhicules et les habitudes de conduite."
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
ms.openlocfilehash: 0a4dba58445cf0fd9fd8f51d443576bacd92251b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-the-solution"></a><span data-ttu-id="7d9c2-103">Guide de la solution Vehicle Telemetry Analytics : découverte approfondie de la solution</span><span class="sxs-lookup"><span data-stu-id="7d9c2-103">Vehicle telemetry analytics solution playbook: deep dive into the solution</span></span>
<span data-ttu-id="7d9c2-104">Ce **menu** contient des liens vers les sections de ce manuel :</span><span class="sxs-lookup"><span data-stu-id="7d9c2-104">This **menu** links to the sections of this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="7d9c2-105">Cette section explore chacune des étapes présentées dans l’Architecture de la solution et contient des instructions et des pointeurs à des fins de personnalisation.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-105">This section drills down into each of the stages depicted in the Solution Architecture with instructions and pointers for customization.</span></span> 

## <a name="data-sources"></a><span data-ttu-id="7d9c2-106">Sources de données</span><span class="sxs-lookup"><span data-stu-id="7d9c2-106">Data Sources</span></span>
<span data-ttu-id="7d9c2-107">La solution utilise deux sources de données différentes :</span><span class="sxs-lookup"><span data-stu-id="7d9c2-107">The solution uses two different data sources:</span></span>

* <span data-ttu-id="7d9c2-108">**jeu de données de diagnostic et de signaux des véhicules simulés** et</span><span class="sxs-lookup"><span data-stu-id="7d9c2-108">**simulated vehicle signals and diagnostic dataset** and</span></span> 
* <span data-ttu-id="7d9c2-109">**catalogue de véhicules**</span><span class="sxs-lookup"><span data-stu-id="7d9c2-109">**vehicle catalog**</span></span>

<span data-ttu-id="7d9c2-110">Un simulateur de télématique des véhicules est intégré à cette solution.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-110">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="7d9c2-111">Ce simulateur émet des informations de diagnostic et des signaux correspondant à l’état du véhicule et au schéma de conduite à un moment donné dans le temps.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-111">It emits diagnostic information and signals corresponding to the state of the vehicle and to the driving pattern at a given point in time.</span></span> <span data-ttu-id="7d9c2-112">Cliquez sur [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) pour télécharger la **solution Vehicle Telematics Simulator Visual Studio** afin de la personnaliser en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-112">Click [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) to download the **Vehicle Telematics Simulator Visual Studio Solution** for customizations based on your requirements.</span></span> <span data-ttu-id="7d9c2-113">Le catalogue de véhicules contient un jeu de données de référence associé à un mappage VIN/modèle.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-113">The vehicle catalog contains a reference dataset with a VIN to model mapping.</span></span>

![Simulateur de télématique des véhicules](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

<span data-ttu-id="7d9c2-115">*Figure 1 – Simulateur de télématique des véhicules*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-115">*Figure 1 – Vehicle Telematics Simulator*</span></span>

<span data-ttu-id="7d9c2-116">Il s’agit d’un jeu de données au format JSON qui contient le schéma suivant.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-116">This is a JSON-formatted dataset that contains the following schema.</span></span>

| <span data-ttu-id="7d9c2-117">Colonne</span><span class="sxs-lookup"><span data-stu-id="7d9c2-117">Column</span></span> | <span data-ttu-id="7d9c2-118">Description</span><span class="sxs-lookup"><span data-stu-id="7d9c2-118">Description</span></span> | <span data-ttu-id="7d9c2-119">Valeurs</span><span class="sxs-lookup"><span data-stu-id="7d9c2-119">Values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7d9c2-120">VIN</span><span class="sxs-lookup"><span data-stu-id="7d9c2-120">VIN</span></span> |<span data-ttu-id="7d9c2-121">Numéro d’identification du véhicule généré de manière aléatoire</span><span class="sxs-lookup"><span data-stu-id="7d9c2-121">Randomly generated Vehicle Identification Number</span></span> |<span data-ttu-id="7d9c2-122">Ce numéro est obtenu à partir d’une liste de référence contenant 10 000 numéros d’identification de véhicule générés de manière aléatoire.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-122">This is obtained from a master list of 10,000 randomly generated vehicle identification numbers.</span></span> |
| <span data-ttu-id="7d9c2-123">Outside temperature</span><span class="sxs-lookup"><span data-stu-id="7d9c2-123">Outside temperature</span></span> |<span data-ttu-id="7d9c2-124">Température extérieure mesurée dans la zone de conduite du véhicule</span><span class="sxs-lookup"><span data-stu-id="7d9c2-124">The outside temperature where the vehicle is driving</span></span> |<span data-ttu-id="7d9c2-125">Nombre généré de manière aléatoire et compris entre 0 et 100</span><span class="sxs-lookup"><span data-stu-id="7d9c2-125">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="7d9c2-126">Engine temperature</span><span class="sxs-lookup"><span data-stu-id="7d9c2-126">Engine temperature</span></span> |<span data-ttu-id="7d9c2-127">Température moteur du véhicule</span><span class="sxs-lookup"><span data-stu-id="7d9c2-127">The engine temperature of the vehicle</span></span> |<span data-ttu-id="7d9c2-128">Nombre généré de manière aléatoire et compris entre 0 et 500</span><span class="sxs-lookup"><span data-stu-id="7d9c2-128">Randomly generated number from 0-500</span></span> |
| <span data-ttu-id="7d9c2-129">Vitesse</span><span class="sxs-lookup"><span data-stu-id="7d9c2-129">Speed</span></span> |<span data-ttu-id="7d9c2-130">Régime de conduite du véhicule</span><span class="sxs-lookup"><span data-stu-id="7d9c2-130">The engine speed at which the vehicle is driving</span></span> |<span data-ttu-id="7d9c2-131">Nombre généré de manière aléatoire et compris entre 0 et 100</span><span class="sxs-lookup"><span data-stu-id="7d9c2-131">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="7d9c2-132">Fuel</span><span class="sxs-lookup"><span data-stu-id="7d9c2-132">Fuel</span></span> |<span data-ttu-id="7d9c2-133">Niveau de carburant du véhicule</span><span class="sxs-lookup"><span data-stu-id="7d9c2-133">The fuel level of the vehicle</span></span> |<span data-ttu-id="7d9c2-134">Nombre généré de manière aléatoire et compris entre 0 et 100 (indique le niveau de carburant en pourcentage)</span><span class="sxs-lookup"><span data-stu-id="7d9c2-134">Randomly generated number from 0-100 (indicates fuel level percentage)</span></span> |
| <span data-ttu-id="7d9c2-135">EngineOil</span><span class="sxs-lookup"><span data-stu-id="7d9c2-135">EngineOil</span></span> |<span data-ttu-id="7d9c2-136">Niveau d’huile moteur du véhicule</span><span class="sxs-lookup"><span data-stu-id="7d9c2-136">The engine oil level of the vehicle</span></span> |<span data-ttu-id="7d9c2-137">Nombre généré de manière aléatoire et compris entre 0 et 100 (indique le niveau d’huile moteur en pourcentage)</span><span class="sxs-lookup"><span data-stu-id="7d9c2-137">Randomly generated number from 0-100 (indicates engine oil level percentage)</span></span> |
| <span data-ttu-id="7d9c2-138">Pression des pneus</span><span class="sxs-lookup"><span data-stu-id="7d9c2-138">Tire pressure</span></span> |<span data-ttu-id="7d9c2-139">Pression des pneus du véhicule</span><span class="sxs-lookup"><span data-stu-id="7d9c2-139">The tire pressure of the vehicle</span></span> |<span data-ttu-id="7d9c2-140">Nombre généré de manière aléatoire et compris entre 0 et 50 (indique le niveau de pression des pneus en pourcentage)</span><span class="sxs-lookup"><span data-stu-id="7d9c2-140">Randomly generated number from 0-50 (indicates tire pressure level percentage)</span></span> |
| <span data-ttu-id="7d9c2-141">Odometer</span><span class="sxs-lookup"><span data-stu-id="7d9c2-141">Odometer</span></span> |<span data-ttu-id="7d9c2-142">Valeur lue sur le compteur kilométrique du véhicule</span><span class="sxs-lookup"><span data-stu-id="7d9c2-142">The odometer reading of the vehicle</span></span> |<span data-ttu-id="7d9c2-143">Nombre généré de manière aléatoire et compris entre 0 et 200 000</span><span class="sxs-lookup"><span data-stu-id="7d9c2-143">Randomly generated number from 0-200000</span></span> |
| <span data-ttu-id="7d9c2-144">Accelerator_pedal_position</span><span class="sxs-lookup"><span data-stu-id="7d9c2-144">Accelerator_pedal_position</span></span> |<span data-ttu-id="7d9c2-145">Position de la pédale d’accélérateur du véhicule</span><span class="sxs-lookup"><span data-stu-id="7d9c2-145">The accelerator pedal position of the vehicle</span></span> |<span data-ttu-id="7d9c2-146">Nombre généré de manière aléatoire et compris entre 0 et 100 (indique le niveau d’accélération en pourcentage)</span><span class="sxs-lookup"><span data-stu-id="7d9c2-146">Randomly generated number from 0-100 (indicates accelerator level percentage)</span></span> |
| <span data-ttu-id="7d9c2-147">Parking_brake_status</span><span class="sxs-lookup"><span data-stu-id="7d9c2-147">Parking_brake_status</span></span> |<span data-ttu-id="7d9c2-148">Indique si le véhicule est stationné ou non</span><span class="sxs-lookup"><span data-stu-id="7d9c2-148">Indicates whether the vehicle is parked or not</span></span> |<span data-ttu-id="7d9c2-149">True ou False</span><span class="sxs-lookup"><span data-stu-id="7d9c2-149">True or False</span></span> |
| <span data-ttu-id="7d9c2-150">Headlamp_status</span><span class="sxs-lookup"><span data-stu-id="7d9c2-150">Headlamp_status</span></span> |<span data-ttu-id="7d9c2-151">Indique si les phares sont allumés ou non</span><span class="sxs-lookup"><span data-stu-id="7d9c2-151">Indicates where the headlamp is on or not</span></span> |<span data-ttu-id="7d9c2-152">True ou False</span><span class="sxs-lookup"><span data-stu-id="7d9c2-152">True or False</span></span> |
| <span data-ttu-id="7d9c2-153">Brake_pedal_status</span><span class="sxs-lookup"><span data-stu-id="7d9c2-153">Brake_pedal_status</span></span> |<span data-ttu-id="7d9c2-154">Indique si la pédale de frein est enfoncée ou non</span><span class="sxs-lookup"><span data-stu-id="7d9c2-154">Indicates whether the brake pedal is pressed or not</span></span> |<span data-ttu-id="7d9c2-155">True ou False</span><span class="sxs-lookup"><span data-stu-id="7d9c2-155">True or False</span></span> |
| <span data-ttu-id="7d9c2-156">Transmission_gear_position</span><span class="sxs-lookup"><span data-stu-id="7d9c2-156">Transmission_gear_position</span></span> |<span data-ttu-id="7d9c2-157">Position de la boîte de vitesses du véhicule</span><span class="sxs-lookup"><span data-stu-id="7d9c2-157">The transmission gear position of the vehicle</span></span> |<span data-ttu-id="7d9c2-158">États : première, deuxième, troisième, quatrième, cinquième, sixième, septième, huitième</span><span class="sxs-lookup"><span data-stu-id="7d9c2-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span></span> |
| <span data-ttu-id="7d9c2-159">Ignition_status</span><span class="sxs-lookup"><span data-stu-id="7d9c2-159">Ignition_status</span></span> |<span data-ttu-id="7d9c2-160">Indique si le véhicule roule ou s’il est arrêté</span><span class="sxs-lookup"><span data-stu-id="7d9c2-160">Indicates whether the vehicle is running or stopped</span></span> |<span data-ttu-id="7d9c2-161">True ou False</span><span class="sxs-lookup"><span data-stu-id="7d9c2-161">True or False</span></span> |
| <span data-ttu-id="7d9c2-162">Windshield_wiper_status</span><span class="sxs-lookup"><span data-stu-id="7d9c2-162">Windshield_wiper_status</span></span> |<span data-ttu-id="7d9c2-163">Indique si les essuie-glaces sont activés ou non</span><span class="sxs-lookup"><span data-stu-id="7d9c2-163">Indicates whether the windshield wiper is turned or not</span></span> |<span data-ttu-id="7d9c2-164">True ou False</span><span class="sxs-lookup"><span data-stu-id="7d9c2-164">True or False</span></span> |
| <span data-ttu-id="7d9c2-165">ABS</span><span class="sxs-lookup"><span data-stu-id="7d9c2-165">ABS</span></span> |<span data-ttu-id="7d9c2-166">Indique si l’ABS est activé ou non</span><span class="sxs-lookup"><span data-stu-id="7d9c2-166">Indicates whether ABS is engaged or not</span></span> |<span data-ttu-id="7d9c2-167">True ou False</span><span class="sxs-lookup"><span data-stu-id="7d9c2-167">True or False</span></span> |
| <span data-ttu-id="7d9c2-168">Timestamp</span><span class="sxs-lookup"><span data-stu-id="7d9c2-168">Timestamp</span></span> |<span data-ttu-id="7d9c2-169">Date et heure de création du point de données</span><span class="sxs-lookup"><span data-stu-id="7d9c2-169">The timestamp when the data point is created</span></span> |<span data-ttu-id="7d9c2-170">Date</span><span class="sxs-lookup"><span data-stu-id="7d9c2-170">Date</span></span> |
| <span data-ttu-id="7d9c2-171">City</span><span class="sxs-lookup"><span data-stu-id="7d9c2-171">City</span></span> |<span data-ttu-id="7d9c2-172">Emplacement du véhicule</span><span class="sxs-lookup"><span data-stu-id="7d9c2-172">The location of the vehicle</span></span> |<span data-ttu-id="7d9c2-173">4 villes dans cette solution : Bellevue, Redmond, Sammamish, Seattle</span><span class="sxs-lookup"><span data-stu-id="7d9c2-173">4 cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span></span> |

<span data-ttu-id="7d9c2-174">Le jeu de données de référence du modèle de véhicule contient un mappage entre le numéro d’identification du véhicule (VIN) et le modèle.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-174">The vehicle model reference dataset contains VIN to the model mapping.</span></span> 

| <span data-ttu-id="7d9c2-175">VIN</span><span class="sxs-lookup"><span data-stu-id="7d9c2-175">VIN</span></span> | <span data-ttu-id="7d9c2-176">Modèle</span><span class="sxs-lookup"><span data-stu-id="7d9c2-176">Model</span></span> |
| --- | --- |
| <span data-ttu-id="7d9c2-177">FHL3O1SA4IEHB4WU1</span><span class="sxs-lookup"><span data-stu-id="7d9c2-177">FHL3O1SA4IEHB4WU1</span></span> |<span data-ttu-id="7d9c2-178">Berline</span><span class="sxs-lookup"><span data-stu-id="7d9c2-178">Sedan</span></span> |
| <span data-ttu-id="7d9c2-179">8J0U8XCPRGW4Z3NQE</span><span class="sxs-lookup"><span data-stu-id="7d9c2-179">8J0U8XCPRGW4Z3NQE</span></span> |<span data-ttu-id="7d9c2-180">Hybride</span><span class="sxs-lookup"><span data-stu-id="7d9c2-180">Hybrid</span></span> |
| <span data-ttu-id="7d9c2-181">WORG68Z2PLTNZDBI7</span><span class="sxs-lookup"><span data-stu-id="7d9c2-181">WORG68Z2PLTNZDBI7</span></span> |<span data-ttu-id="7d9c2-182">Berline familiale</span><span class="sxs-lookup"><span data-stu-id="7d9c2-182">Family Saloon</span></span> |
| <span data-ttu-id="7d9c2-183">JTHMYHQTEPP4WBMRN</span><span class="sxs-lookup"><span data-stu-id="7d9c2-183">JTHMYHQTEPP4WBMRN</span></span> |<span data-ttu-id="7d9c2-184">Berline</span><span class="sxs-lookup"><span data-stu-id="7d9c2-184">Sedan</span></span> |
| <span data-ttu-id="7d9c2-185">W9FTHG27LZN1YWO0Y</span><span class="sxs-lookup"><span data-stu-id="7d9c2-185">W9FTHG27LZN1YWO0Y</span></span> |<span data-ttu-id="7d9c2-186">Hybride</span><span class="sxs-lookup"><span data-stu-id="7d9c2-186">Hybrid</span></span> |
| <span data-ttu-id="7d9c2-187">MHTP9N792PHK08WJM</span><span class="sxs-lookup"><span data-stu-id="7d9c2-187">MHTP9N792PHK08WJM</span></span> |<span data-ttu-id="7d9c2-188">Berline familiale</span><span class="sxs-lookup"><span data-stu-id="7d9c2-188">Family Saloon</span></span> |
| <span data-ttu-id="7d9c2-189">EI4QXI2AXVQQING4I</span><span class="sxs-lookup"><span data-stu-id="7d9c2-189">EI4QXI2AXVQQING4I</span></span> |<span data-ttu-id="7d9c2-190">Berline</span><span class="sxs-lookup"><span data-stu-id="7d9c2-190">Sedan</span></span> |
| <span data-ttu-id="7d9c2-191">5KKR2VB4WHQH97PF8</span><span class="sxs-lookup"><span data-stu-id="7d9c2-191">5KKR2VB4WHQH97PF8</span></span> |<span data-ttu-id="7d9c2-192">Hybride</span><span class="sxs-lookup"><span data-stu-id="7d9c2-192">Hybrid</span></span> |
| <span data-ttu-id="7d9c2-193">W9NSZ423XZHAONYXB</span><span class="sxs-lookup"><span data-stu-id="7d9c2-193">W9NSZ423XZHAONYXB</span></span> |<span data-ttu-id="7d9c2-194">Berline familiale</span><span class="sxs-lookup"><span data-stu-id="7d9c2-194">Family Saloon</span></span> |
| <span data-ttu-id="7d9c2-195">26WJSGHX4MA5ROHNL</span><span class="sxs-lookup"><span data-stu-id="7d9c2-195">26WJSGHX4MA5ROHNL</span></span> |<span data-ttu-id="7d9c2-196">Cabriolet</span><span class="sxs-lookup"><span data-stu-id="7d9c2-196">Convertible</span></span> |
| <span data-ttu-id="7d9c2-197">GHLUB6ONKMOSI7E77</span><span class="sxs-lookup"><span data-stu-id="7d9c2-197">GHLUB6ONKMOSI7E77</span></span> |<span data-ttu-id="7d9c2-198">Break</span><span class="sxs-lookup"><span data-stu-id="7d9c2-198">Station Wagon</span></span> |
| <span data-ttu-id="7d9c2-199">9C2RHVRVLMEJDBXLP</span><span class="sxs-lookup"><span data-stu-id="7d9c2-199">9C2RHVRVLMEJDBXLP</span></span> |<span data-ttu-id="7d9c2-200">Voiture compacte</span><span class="sxs-lookup"><span data-stu-id="7d9c2-200">Compact Car</span></span> |
| <span data-ttu-id="7d9c2-201">BRNHVMZOUJ6EOCP32</span><span class="sxs-lookup"><span data-stu-id="7d9c2-201">BRNHVMZOUJ6EOCP32</span></span> |<span data-ttu-id="7d9c2-202">Petit SUV</span><span class="sxs-lookup"><span data-stu-id="7d9c2-202">Small SUV</span></span> |
| <span data-ttu-id="7d9c2-203">VCYVW0WUZNBTM594J</span><span class="sxs-lookup"><span data-stu-id="7d9c2-203">VCYVW0WUZNBTM594J</span></span> |<span data-ttu-id="7d9c2-204">Voiture de sport</span><span class="sxs-lookup"><span data-stu-id="7d9c2-204">Sports Car</span></span> |
| <span data-ttu-id="7d9c2-205">HNVCE6YFZSA5M82NY</span><span class="sxs-lookup"><span data-stu-id="7d9c2-205">HNVCE6YFZSA5M82NY</span></span> |<span data-ttu-id="7d9c2-206">SUV de taille moyenne</span><span class="sxs-lookup"><span data-stu-id="7d9c2-206">Medium SUV</span></span> |
| <span data-ttu-id="7d9c2-207">4R30FOR7NUOBL05GJ</span><span class="sxs-lookup"><span data-stu-id="7d9c2-207">4R30FOR7NUOBL05GJ</span></span> |<span data-ttu-id="7d9c2-208">Break</span><span class="sxs-lookup"><span data-stu-id="7d9c2-208">Station Wagon</span></span> |
| <span data-ttu-id="7d9c2-209">WYNIIY42VKV6OQS1J</span><span class="sxs-lookup"><span data-stu-id="7d9c2-209">WYNIIY42VKV6OQS1J</span></span> |<span data-ttu-id="7d9c2-210">Grand SUV</span><span class="sxs-lookup"><span data-stu-id="7d9c2-210">Large SUV</span></span> |
| <span data-ttu-id="7d9c2-211">8Y5QKG27QET1RBK7I</span><span class="sxs-lookup"><span data-stu-id="7d9c2-211">8Y5QKG27QET1RBK7I</span></span> |<span data-ttu-id="7d9c2-212">Grand SUV</span><span class="sxs-lookup"><span data-stu-id="7d9c2-212">Large SUV</span></span> |
| <span data-ttu-id="7d9c2-213">DF6OX2WSRA6511BVG</span><span class="sxs-lookup"><span data-stu-id="7d9c2-213">DF6OX2WSRA6511BVG</span></span> |<span data-ttu-id="7d9c2-214">Coupé</span><span class="sxs-lookup"><span data-stu-id="7d9c2-214">Coupe</span></span> |
| <span data-ttu-id="7d9c2-215">Z2EOZWZBXAEW3E60T</span><span class="sxs-lookup"><span data-stu-id="7d9c2-215">Z2EOZWZBXAEW3E60T</span></span> |<span data-ttu-id="7d9c2-216">Berline</span><span class="sxs-lookup"><span data-stu-id="7d9c2-216">Sedan</span></span> |
| <span data-ttu-id="7d9c2-217">M4TV6IEALD5QDS3IR</span><span class="sxs-lookup"><span data-stu-id="7d9c2-217">M4TV6IEALD5QDS3IR</span></span> |<span data-ttu-id="7d9c2-218">Hybride</span><span class="sxs-lookup"><span data-stu-id="7d9c2-218">Hybrid</span></span> |
| <span data-ttu-id="7d9c2-219">VHRA1Y2TGTA84F00H</span><span class="sxs-lookup"><span data-stu-id="7d9c2-219">VHRA1Y2TGTA84F00H</span></span> |<span data-ttu-id="7d9c2-220">Berline familiale</span><span class="sxs-lookup"><span data-stu-id="7d9c2-220">Family Saloon</span></span> |
| <span data-ttu-id="7d9c2-221">R0JAUHT1L1R3BIKI0</span><span class="sxs-lookup"><span data-stu-id="7d9c2-221">R0JAUHT1L1R3BIKI0</span></span> |<span data-ttu-id="7d9c2-222">Berline</span><span class="sxs-lookup"><span data-stu-id="7d9c2-222">Sedan</span></span> |
| <span data-ttu-id="7d9c2-223">9230C202Z60XX84AU</span><span class="sxs-lookup"><span data-stu-id="7d9c2-223">9230C202Z60XX84AU</span></span> |<span data-ttu-id="7d9c2-224">Hybride</span><span class="sxs-lookup"><span data-stu-id="7d9c2-224">Hybrid</span></span> |
| <span data-ttu-id="7d9c2-225">T8DNDN5UDCWL7M72H</span><span class="sxs-lookup"><span data-stu-id="7d9c2-225">T8DNDN5UDCWL7M72H</span></span> |<span data-ttu-id="7d9c2-226">Berline familiale</span><span class="sxs-lookup"><span data-stu-id="7d9c2-226">Family Saloon</span></span> |
| <span data-ttu-id="7d9c2-227">4WPYRUZII5YV7YA42</span><span class="sxs-lookup"><span data-stu-id="7d9c2-227">4WPYRUZII5YV7YA42</span></span> |<span data-ttu-id="7d9c2-228">Berline</span><span class="sxs-lookup"><span data-stu-id="7d9c2-228">Sedan</span></span> |
| <span data-ttu-id="7d9c2-229">D1ZVY26UV2BFGHZNO</span><span class="sxs-lookup"><span data-stu-id="7d9c2-229">D1ZVY26UV2BFGHZNO</span></span> |<span data-ttu-id="7d9c2-230">Hybride</span><span class="sxs-lookup"><span data-stu-id="7d9c2-230">Hybrid</span></span> |
| <span data-ttu-id="7d9c2-231">XUF99EW9OIQOMV7Q7</span><span class="sxs-lookup"><span data-stu-id="7d9c2-231">XUF99EW9OIQOMV7Q7</span></span> |<span data-ttu-id="7d9c2-232">Berline familiale</span><span class="sxs-lookup"><span data-stu-id="7d9c2-232">Family Saloon</span></span> |
| <span data-ttu-id="7d9c2-233">8OMCL3LGI7XNCC21U</span><span class="sxs-lookup"><span data-stu-id="7d9c2-233">8OMCL3LGI7XNCC21U</span></span> |<span data-ttu-id="7d9c2-234">Cabriolet</span><span class="sxs-lookup"><span data-stu-id="7d9c2-234">Convertible</span></span> |
| <span data-ttu-id="7d9c2-235">…….</span><span class="sxs-lookup"><span data-stu-id="7d9c2-235">…….</span></span> | |

### <a name="references"></a><span data-ttu-id="7d9c2-236">Références</span><span class="sxs-lookup"><span data-stu-id="7d9c2-236">References</span></span>
[<span data-ttu-id="7d9c2-237">Solution Vehicle Telematics Simulator Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7d9c2-237">Vehicle Telematics Simulator Visual Studio Solution</span></span>](http://go.microsoft.com/fwlink/?LinkId=717075) 

[<span data-ttu-id="7d9c2-238">Hub d'événement d'Azure</span><span class="sxs-lookup"><span data-stu-id="7d9c2-238">Azure Event Hub</span></span>](https://azure.microsoft.com/services/event-hubs/)

[<span data-ttu-id="7d9c2-239">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7d9c2-239">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a><span data-ttu-id="7d9c2-240">Ingestion</span><span class="sxs-lookup"><span data-stu-id="7d9c2-240">Ingestion</span></span>
<span data-ttu-id="7d9c2-241">Les composants Event Hubs, Stream Analytics et Data Factory d’Azure sont combinés pour ingérer les signaux des véhicules, les événements de diagnostic, ainsi que les analyses de traitement par lots et en temps réel.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-241">Combinations of Azure Event Hubs, Stream Analytics, and Data Factory are leveraged to ingest the vehicle signals, the diagnostic events, and real-time and batch analytics.</span></span> <span data-ttu-id="7d9c2-242">Tous ces composants sont créés et configurés dans le cadre du déploiement de la solution.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-242">All these components are created and configured as part of the solution deployment.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="7d9c2-243">Analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="7d9c2-243">Real-time analysis</span></span>
<span data-ttu-id="7d9c2-244">Les événements générés par le composant Vehicle Telematics Simulator sont publiés dans Azure Event Hub à l’aide du SDK Event Hub.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-244">The events generated by the Vehicle Telematics Simulator are published to the Event Hub using the Event Hub SDK.</span></span> <span data-ttu-id="7d9c2-245">La tâche Stream Analytics ingère ces événements à partir d’Event Hub et traite les données en temps réel pour analyser l’état du véhicule.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-245">The Stream Analytics job ingests these events from the Event Hub and processes the data in real time to analyze the vehicle health.</span></span> 

![Tableau de bord Event Hub](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

<span data-ttu-id="7d9c2-247">*Figure 4 - Tableau de bord Event Hub*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-247">*Figure 4 - Event Hub dashboard*</span></span>

![Données de traitement de la tâche Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

<span data-ttu-id="7d9c2-249">*Figure 5 - Données de traitement de la tâche Stream Analytics*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-249">*Figure 5 - Stream Analytics job processing data*</span></span>

<span data-ttu-id="7d9c2-250">La tâche Stream Analytics :</span><span class="sxs-lookup"><span data-stu-id="7d9c2-250">The Stream Analytics job;</span></span>

* <span data-ttu-id="7d9c2-251">reçoit les données du composant Event Hub ;</span><span class="sxs-lookup"><span data-stu-id="7d9c2-251">ingests data from the Event Hub</span></span> 
* <span data-ttu-id="7d9c2-252">effectue une jointure avec les données de référence pour mapper le numéro d’identification du véhicule au modèle correspondant ;</span><span class="sxs-lookup"><span data-stu-id="7d9c2-252">performs a join with the reference data to map the vehicle VIN to the corresponding model</span></span> 
* <span data-ttu-id="7d9c2-253">conserve les données dans le stockage Blob Azure pour une analyse en mode batch approfondie.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-253">persists them into Azure blob storage for rich batch analytics.</span></span> 

<span data-ttu-id="7d9c2-254">La requête Stream Analytics suivante est utilisée pour conserver les données dans le stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-254">The following Stream Analytics query is used to persist the data into Azure blob storage.</span></span> 

![Requête de tâche Stream Analytics pour l’ingestion de données](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

<span data-ttu-id="7d9c2-256">*Figure 6 - Requête de tâche Stream Analytics pour l’ingestion de données*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-256">*Figure 6 - Stream Analytics job query for data ingestion*</span></span>

### <a name="batch-analysis"></a><span data-ttu-id="7d9c2-257">Analyse en mode batch</span><span class="sxs-lookup"><span data-stu-id="7d9c2-257">Batch analysis</span></span>
<span data-ttu-id="7d9c2-258">Nous allons également générer un volume supplémentaire de signaux de véhicules simulés ainsi qu’un jeu de données de diagnostic pour permettre une analyse en mode batch approfondie.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-258">We are also generating an additional volume of simulated vehicle signals and diagnostic dataset for richer batch analytics.</span></span> <span data-ttu-id="7d9c2-259">Cette étape est nécessaire pour garantir un volume de données représentatif dans le cadre d’un traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-259">This is required to ensure a good representative data volume for batch processing.</span></span> <span data-ttu-id="7d9c2-260">Nous utilisons pour cela un pipeline nommé « PrepareSampleDataPipeline » dans le flux de travail Azure Data Factory pour générer l’équivalent d’une année de signaux et de diagnostics de véhicules simulés.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-260">For this purpose, we are using a pipeline named "PrepareSampleDataPipeline" in the Azure Data Factory workflow to generate one year's worth of simulated vehicle signals and diagnostic dataset.</span></span> <span data-ttu-id="7d9c2-261">Cliquez sur [Activité personnalisée Data Factory](http://go.microsoft.com/fwlink/?LinkId=717077) pour télécharger la solution Data Factory custom DotNet activity Visual Studio afin de la personnaliser en fonction de vos besoins.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-261">Click [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) to download the Data Factory custom DotNet activity Visual Studio solution for customizations based on your requirements.</span></span> 

![Préparer des exemples de données pour le workflow de traitement par lots](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

<span data-ttu-id="7d9c2-263">*Figure 7 - Préparer des exemples de données pour le workflow de traitement par lots*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-263">*Figure 7 - Prepare Sample data for batch processing workflow*</span></span>

<span data-ttu-id="7d9c2-264">Le pipeline est composé d’un élément ADF .NET Activity personnalisé, illustré ici :</span><span class="sxs-lookup"><span data-stu-id="7d9c2-264">The pipeline consists of a custom ADF .Net Activity, show here:</span></span>

![Activité PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

<span data-ttu-id="7d9c2-266">*Figure 8 - PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-266">*Figure 8 - PrepareSampleDataPipeline*</span></span>

<span data-ttu-id="7d9c2-267">Une fois que le pipeline est correctement exécuté et que le jeu de données « RawCarEventsTable » est marqué comme « Prêt », l’équivalent d’une année de données de signaux et de diagnostics de véhicules simulés est généré.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-267">Once the pipeline executes successfully and "RawCarEventsTable" dataset is marked "Ready", one-year worth of simulated vehicle signals and diagnostic data are produced.</span></span> <span data-ttu-id="7d9c2-268">Le dossier et le fichier ci-dessous sont créés dans votre compte de stockage sous le conteneur « connectedcar » :</span><span class="sxs-lookup"><span data-stu-id="7d9c2-268">You see the following folder and file created in your storage account under the "connectedcar" container:</span></span>

![Sortie de PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

<span data-ttu-id="7d9c2-270">*Figure 9 - Sortie de PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-270">*Figure 9 - PrepareSampleDataPipeline Output*</span></span>

### <a name="references"></a><span data-ttu-id="7d9c2-271">Références</span><span class="sxs-lookup"><span data-stu-id="7d9c2-271">References</span></span>
[<span data-ttu-id="7d9c2-272">Kit Azure Event Hub SDK pour la réception de flux</span><span class="sxs-lookup"><span data-stu-id="7d9c2-272">Azure Event Hub SDK for stream ingestion</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

<span data-ttu-id="7d9c2-273">[Fonctionnalités de déplacement de données Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="7d9c2-273">[Azure Data Factory data movement capabilities](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span></span>

[<span data-ttu-id="7d9c2-274">Solution Azure Data Factory DotNet Activity Visual Studio pour la préparation des exemples de données</span><span class="sxs-lookup"><span data-stu-id="7d9c2-274">Azure Data Factory DotNet activity visual studio solution for preparing sample data</span></span>](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-the-dataset"></a><span data-ttu-id="7d9c2-275">Partitionner le jeu de données</span><span class="sxs-lookup"><span data-stu-id="7d9c2-275">Partition the dataset</span></span>
<span data-ttu-id="7d9c2-276">Les signaux et les données de diagnostic de véhicules bruts et semi-structurés sont partitionnés au cours de l’étape de préparation des données au format ANNÉE/MOIS.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-276">The raw semi-structured vehicle signals and diagnostic dataset are partitioned in the data preparation step into a YEAR/MONTH format.</span></span> <span data-ttu-id="7d9c2-277">Ce partitionnement favorise une interrogation plus efficace et un stockage extensible à long terme en permettant le basculement d’un compte de stockage d’objets blob à un autre dès que le premier est rempli.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-277">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over from one blob account to the next as the first account fills up.</span></span> 

>[!NOTE] 
><span data-ttu-id="7d9c2-278">Cette étape de la solution s’applique uniquement au traitement par lots.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-278">This step in the solution is applicable only to batch processing.</span></span>

<span data-ttu-id="7d9c2-279">Gestion des données d’entrée et de sortie :</span><span class="sxs-lookup"><span data-stu-id="7d9c2-279">Input and output data data management:</span></span>

* <span data-ttu-id="7d9c2-280">Les **données de sortie** (intitulées *PartitionedCarEventsTable*) doivent être conservées pendant une longue période sous une forme primaire/« la plus brute » dans le « Data Lake » (lac de données) du client.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-280">The **output data** (labeled *PartitionedCarEventsTable*) is to be kept for a long period of time as the foundational/"rawest" form of data in the customer's "Data Lake".</span></span> 
* <span data-ttu-id="7d9c2-281">Les **données d’entrée** de ce pipeline sont généralement ignorées, car les données de sortie représentent fidèlement les données d’entrée. Ces dernières sont simplement stockées (partitionnées) en vue d’être utilisées ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-281">The **input data** to this pipeline would typically be discarded as the output data has full fidelity to the input - it's just stored (partitioned) better for subsequent use.</span></span>

![Workflow Partition Car Events](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

<span data-ttu-id="7d9c2-283">*Figure 10 - Workflow Partition Car Events*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-283">*Figure 10 – Partition Car Events workflow*</span></span>

<span data-ttu-id="7d9c2-284">Les données brutes sont partitionnées à l’aide d’une activité Hive HDInsight dans « PartitionCarEventsPipeline ».</span><span class="sxs-lookup"><span data-stu-id="7d9c2-284">The raw data is partitioned using a Hive HDInsight activity in "PartitionCarEventsPipeline".</span></span> <span data-ttu-id="7d9c2-285">Les exemples de données générés à l’étape 1 pour une année sont partitionnés par ANNÉE/MOIS.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-285">The sample data generated in step 1 for a year is partitioned by YEAR/MONTH.</span></span> <span data-ttu-id="7d9c2-286">Les partitions sont utilisées pour générer les signaux et les données de diagnostic de véhicules pour chaque mois (12 partitions au total).</span><span class="sxs-lookup"><span data-stu-id="7d9c2-286">The partitions are used to generate vehicle signals and diagnostic data for each month (total 12 partitions) of a year.</span></span> 

![Activité PartitionCarEventsPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

<span data-ttu-id="7d9c2-288">*Figure 11 - PartitionCarEventsPipeline*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-288">*Figure 11 - PartitionCarEventsPipeline*</span></span>

<span data-ttu-id="7d9c2-289">***Script Hive PartitionConnectedCarEvents***</span><span class="sxs-lookup"><span data-stu-id="7d9c2-289">***PartitionConnectedCarEvents Hive Script***</span></span>

<span data-ttu-id="7d9c2-290">Le script Hive suivant, nommé « partitioncarevents.hql » et situé dans le dossier « \demo\src\connectedcar\scripts » de l’archive .zip téléchargée, est utilisé pour le partitionnement.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-290">The following Hive script, named "partitioncarevents.hql", is used for partitioning and is located in the "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 
    
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

<span data-ttu-id="7d9c2-291">Une fois le pipeline exécuté, les partitions suivantes sont générées dans votre compte de stockage sous le conteneur « connectedcar ».</span><span class="sxs-lookup"><span data-stu-id="7d9c2-291">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Sortie partitionnée](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

<span data-ttu-id="7d9c2-293">*Figure 12 - Sortie partitionnée*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-293">*Figure 12 - Partitioned Output*</span></span>

<span data-ttu-id="7d9c2-294">Les données sont maintenant optimisées, plus faciles à gérer et prêtes à être traitées pour obtenir des informations de traitement par lots complètes.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-294">The data is now optimized, is more manageable and ready for further processing to gain rich batch insights.</span></span> 

## <a name="data-analysis"></a><span data-ttu-id="7d9c2-295">Analyse des données</span><span class="sxs-lookup"><span data-stu-id="7d9c2-295">Data Analysis</span></span>
<span data-ttu-id="7d9c2-296">Cette section explique comment associer les composants Azure Stream Analytics, Azure Machine Learning, Azure Data Factory et Azure HDInsight pour analyser avec précision l’état des véhicules et les habitudes de conduite.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-296">In this section, you see how to combine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory, and Azure HDInsight for rich advanced analytics on vehicle health and driving habits.</span></span> <span data-ttu-id="7d9c2-297">Elle est divisée en trois sous-sections :</span><span class="sxs-lookup"><span data-stu-id="7d9c2-297">There are three subsections here:</span></span>

1. <span data-ttu-id="7d9c2-298">**Apprentissage automatique**: cette sous-section contient des informations relatives à l’expérience de détection des anomalies que nous avons utilisée dans cette solution pour identifier de manière proactive les véhicules ayant besoin d’une intervention de maintenance ainsi que les véhicules devant faire l’objet d’un rappel pour des raisons de sécurité.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-298">**Machine Learning**: This subsection contains information on the anomaly detection experiment that we have used in this solution to predict vehicles requiring servicing maintenance and vehicles requiring recalls due to safety issues.</span></span>
2. <span data-ttu-id="7d9c2-299">**Analyse en temps réel**: cette sous-section contient des informations concernant l’analyse en temps réel utilisant le langage de requête Stream Analytics et l’amélioration de l’expérience d’apprentissage automatique en temps réel à l’aide d’une application personnalisée.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-299">**Real-time analysis**: This subsection contains information regarding the real-time analytics using the Stream Analytics Query Language and operationalizing the machine learning experiment in real time using a custom application.</span></span>
3. <span data-ttu-id="7d9c2-300">**Analyse par lots**: cette sous-section contient des informations relatives à la transformation et au traitement des données par lots à l’aide des composants Azure HDInsight et Azure Machine Learning déployés par Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-300">**Batch analysis**: This subsection contains information regarding the transforming and processing of the batch data using Azure HDInsight and Azure Machine Learning operationalized by Azure Data Factory.</span></span>

### <a name="machine-learning"></a><span data-ttu-id="7d9c2-301">Apprentissage automatique</span><span class="sxs-lookup"><span data-stu-id="7d9c2-301">Machine Learning</span></span>
<span data-ttu-id="7d9c2-302">Notre objectif est ici de prédire quels véhicules devront faire l’objet d’une intervention de maintenance ou d’un rappel en fonction de certaines statistiques de contrôle d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-302">Our goal here is to predict the vehicles that require maintenance or recall based on certain heath statistics.</span></span> <span data-ttu-id="7d9c2-303">Nous formulons les hypothèses suivantes :</span><span class="sxs-lookup"><span data-stu-id="7d9c2-303">We make the following assumptions</span></span>

* <span data-ttu-id="7d9c2-304">Si l’une des trois conditions suivantes est remplie, les véhicules ont besoin d’une **intervention de maintenance**:</span><span class="sxs-lookup"><span data-stu-id="7d9c2-304">If one of the following three conditions are true, the vehicles require **servicing maintenance**:</span></span>
  
  * <span data-ttu-id="7d9c2-305">La pression des pneus faible</span><span class="sxs-lookup"><span data-stu-id="7d9c2-305">Tire pressure is low</span></span>
  * <span data-ttu-id="7d9c2-306">Le niveau d’huile moteur est faible</span><span class="sxs-lookup"><span data-stu-id="7d9c2-306">Engine oil level is low</span></span>
  * <span data-ttu-id="7d9c2-307">La température du moteur est élevée</span><span class="sxs-lookup"><span data-stu-id="7d9c2-307">Engine temperature is high</span></span>
* <span data-ttu-id="7d9c2-308">Si l’une des conditions suivantes est remplie, les véhicules peuvent présenter un **problème de sécurité** et nécessiter un **rappel** :</span><span class="sxs-lookup"><span data-stu-id="7d9c2-308">If one of the following conditions are true, the vehicles may have a **safety issue** and require **recall**:</span></span>
  
  * <span data-ttu-id="7d9c2-309">La température du moteur est élevée mais la température extérieure est faible</span><span class="sxs-lookup"><span data-stu-id="7d9c2-309">Engine temperature is high but outside temperature is low</span></span>
  * <span data-ttu-id="7d9c2-310">La température du moteur est faible mais la température extérieure est élevée</span><span class="sxs-lookup"><span data-stu-id="7d9c2-310">Engine temperature is low but outside temperature is high</span></span>

<span data-ttu-id="7d9c2-311">Compte tenu des exigences précédentes, nous avons créé deux modèles distincts afin de détecter des anomalies : le premier pour détecter les besoins de maintenance des véhicules, le second pour détecter les rappels de véhicules.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-311">Based on the previous requirements, we have created two separate models to detect anomalies, one for vehicle maintenance detection, and one for vehicle recall detection.</span></span> <span data-ttu-id="7d9c2-312">Dans ces deux modèles, l’algorithme Principal Component Analysis (PCA) intégré est utilisé pour la détection des anomalies.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-312">In both these models, the built-in Principal Component Analysis (PCA) algorithm is used for anomaly detection.</span></span> 

<span data-ttu-id="7d9c2-313">**Modèle de détection de maintenance**</span><span class="sxs-lookup"><span data-stu-id="7d9c2-313">**Maintenance detection model**</span></span>

<span data-ttu-id="7d9c2-314">Si l’un des trois indicateurs (pression des pneus, huile moteur ou température du moteur) remplit sa condition respective, le modèle de détection de maintenance signale une anomalie.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-314">If one of three indicators - tire pressure, engine oil, or engine temperature - satisfies its respective condition, the maintenance detection model reports an anomaly.</span></span> <span data-ttu-id="7d9c2-315">Nous devons donc uniquement prendre en compte ces trois variables dans la construction du modèle.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-315">As a result, we only need to consider these three variables in building the model.</span></span> <span data-ttu-id="7d9c2-316">Pour notre expérience dans Azure Machine Learning, nous utilisons tout d’abord le module **Sélectionner des colonnes dans le jeu de données** afin d’extraire ces trois variables.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-316">In our experiment in Azure Machine Learning, we first use a **Select Columns in Dataset** module to extract these three variables.</span></span> <span data-ttu-id="7d9c2-317">Nous utilisons ensuite le module de détection d’anomalies basé sur l’algorithme PCA pour générer le modèle de détection d’anomalies.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-317">Next we use the PCA-based anomaly detection module to build the anomaly detection model.</span></span> 

<span data-ttu-id="7d9c2-318">Principal Component Analysis (PCA) est une technique d’apprentissage automatique reconnue qui peut être appliquée à la sélection des fonctionnalités, à la classification et à la détection d’anomalies.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-318">Principal Component Analysis (PCA) is an established technique in machine learning that can be applied to feature selection, classification, and anomaly detection.</span></span> <span data-ttu-id="7d9c2-319">PCA convertit un ensemble de cas contenant des variables potentiellement corrélées en un ensemble de valeurs appelées composants principaux.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-319">PCA converts a set of case containing possibly correlated variables, into a set of values called principal components.</span></span> <span data-ttu-id="7d9c2-320">La modélisation PCA vise essentiellement à projeter des données dans un espace de plus faible dimension afin de faciliter l’identification des fonctionnalités et des anomalies.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-320">The key idea of PCA-based modeling is to project data onto a lower-dimensional space so that features and anomalies can be more easily identified.</span></span>

<span data-ttu-id="7d9c2-321">Pour chaque nouvelle entrée dans le modèle de détection, le détecteur d’anomalies calcule d’abord sa projection sur les vecteurs propres avant de calculer l’erreur de reconstruction normalisée.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-321">For each new input to  the detection model, the anomaly detector first computes its projection on the eigenvectors, and then computes the normalized reconstruction error.</span></span> <span data-ttu-id="7d9c2-322">Cette erreur normalisée représente le score d’anomalies.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-322">This normalized error is the anomaly score.</span></span> <span data-ttu-id="7d9c2-323">Plus l’erreur est élevée, plus l’instance est anormale.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-323">The higher the error, the more anomalous the instance is.</span></span> 

<span data-ttu-id="7d9c2-324">Dans le problème de la détection de maintenance, chaque enregistrement peut être considéré comme un point dans un espace tridimensionnel défini par les coordonnées « pression des pneus », « huile moteur » et « température du moteur ».</span><span class="sxs-lookup"><span data-stu-id="7d9c2-324">In the maintenance detection problem, each record can be considered as a point in a 3-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span></span> <span data-ttu-id="7d9c2-325">Pour capturer ces anomalies, nous pouvons projeter les données d’origine de l’espace 3D dans un espace 2D à l’aide de PCA.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-325">To capture these anomalies, we can project the original data in the 3-dimensional space onto a 2-dimensional space using PCA.</span></span> <span data-ttu-id="7d9c2-326">Nous définissons donc sur « 2 » le paramètre « nombre de composants à utiliser » dans PCA.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-326">Thus, we set the parameter Number of components to use in PCA to be 2.</span></span> <span data-ttu-id="7d9c2-327">Ce paramètre joue un rôle important dans l’application de la détection d’anomalies basée sur l’algorithme PCA.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-327">This parameter plays an important role in applying PCA-based anomaly detection.</span></span> <span data-ttu-id="7d9c2-328">Une fois les données projetées à l’aide de PCA, nous pouvons identifier plus facilement ces anomalies.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-328">After projecting data using PCA, we can identify these anomalies more easily.</span></span>

<span data-ttu-id="7d9c2-329">**Modèle de détection des anomalies de rappel** Dans le modèle de détection des anomalies de rappel, nous utilisons le module Sélectionner des colonnes dans le jeu de données et le module de détection d’anomalies reposant sur le PCA de manière similaire.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-329">**Recall anomaly detection model** In the recall anomaly detection model, we use the Select Columns in Dataset and PCA-based anomaly detection modules in a similar way.</span></span> <span data-ttu-id="7d9c2-330">Plus précisément, nous commençons par extraire trois variables (température du moteur, température extérieure et vitesse) à l’aide du module **Sélectionner des colonnes dans le jeu de données** .</span><span class="sxs-lookup"><span data-stu-id="7d9c2-330">Specifically, we first extract three variables - engine temperature, outside temperature, and speed - using the **Select Columns in Dataset** module.</span></span> <span data-ttu-id="7d9c2-331">Nous ajoutons également la variable vitesse étant donné que la température du moteur est généralement corrélée à la vitesse.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-331">We also include the speed variable since the engine temperature typically is correlated to the speed.</span></span> <span data-ttu-id="7d9c2-332">Nous utilisons ensuite le module de détection d’anomalies PCA pour projeter les données de l’espace 3D sur un espace 2D.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-332">Next we use PCA-based anomaly detection module to project the data from the 3-dimensional space onto a 2-dimensional space.</span></span> <span data-ttu-id="7d9c2-333">Les critères de rappel étant satisfaits, le véhicule nécessite un rappel lorsque de la température du moteur et la température extérieure sont corrélées de façon très négative.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-333">The recall criteria are satisfied and so the vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span></span> <span data-ttu-id="7d9c2-334">L’algorithme de détection d’anomalies PCA nous permet de regrouper les anomalies après l’exécution de l’algorithme PCA.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-334">Using PCA-based anomaly detection algorithm, we can capture the anomalies after performing PCA.</span></span> 

<span data-ttu-id="7d9c2-335">Lors de l’apprentissage des deux modèles, nous devons utiliser des données normales, c’est-à-dire de véhicules qui ne nécessitent ni maintenance ni rappel, comme données d’entrée pour former le modèle de détection d’anomalies basée sur PCA.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-335">When training either model, we need to use normal data, which does not require maintenance or recall as the input data to train the PCA-based anomaly detection model.</span></span> <span data-ttu-id="7d9c2-336">Dans l’expérience d’évaluation, nous utilisons le modèle de détection d’anomalies formé pour déterminer si le véhicule nécessite ou non une maintenance ou un rappel.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-336">In the scoring experiment, we use the trained anomaly detection model to detect whether or not the vehicle requires maintenance or recall.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="7d9c2-337">Analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="7d9c2-337">Real-time analysis</span></span>
<span data-ttu-id="7d9c2-338">La requête SQL suivante de Stream Analytics est utilisée pour calculer la moyenne de tous les paramètres de véhicule significatifs, tels que la vitesse du véhicule, le niveau de carburant, la température du moteur, le kilométrage, la pression des pneus, le niveau d’huile, etc.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-338">The following Stream Analytics SQL Query is used to get the average of all the important vehicle parameters like vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span></span> <span data-ttu-id="7d9c2-339">Les moyennes servent à détecter des anomalies, émettre des alertes et déterminer les conditions d’intégrité globale des véhicules utilisés dans une région spécifique, puis à les corréler à des données démographiques.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-339">The averages are used to detect anomalies, issue alerts, and determine the overall health conditions of vehicles operated in specific region and then correlate it to demographics.</span></span> 

![Requête Stream Analytics pour le traitement en temps réel](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

<span data-ttu-id="7d9c2-341">*Figure 13 - Requête Stream Analytics pour le traitement en temps réel*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-341">*Figure 13 – Stream Analytics query for real-time processing*</span></span>

<span data-ttu-id="7d9c2-342">Toutes les moyennes sont calculées sur un TumblingWindow de 3 secondes.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-342">All the averages are calculated over a 3-second TumblingWindow.</span></span> <span data-ttu-id="7d9c2-343">Nous utilisons TubmlingWindow dans ce cas car nous avons besoin d’intervalles de temps contigus et sans chevauchement.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-343">We are using TubmlingWindow in this case since we require non-overlapping and contiguous time intervals.</span></span> 

<span data-ttu-id="7d9c2-344">Pour en savoir plus sur les fonctionnalités de « fenêtrage » dans Azure Stream Analytics, cliquez sur [Fenêtrage (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d9c2-344">To learn more about all the "Windowing" capabilities in Azure Stream Analytics, click [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

<span data-ttu-id="7d9c2-345">**Prédiction en temps réel**</span><span class="sxs-lookup"><span data-stu-id="7d9c2-345">**Real-time prediction**</span></span>

<span data-ttu-id="7d9c2-346">Une application est incluse dans le cadre de la solution pour configurer le modèle d’apprentissage automatique en temps réel.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-346">An application is included as part of the solution to operationalize the machine learning model in real time.</span></span> <span data-ttu-id="7d9c2-347">Cette application appelée « RealTimeDashboardApp » est créée et configurée dans le cadre du déploiement de la solution.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-347">This application called “RealTimeDashboardApp” is created and configured as part of the solution deployment.</span></span> <span data-ttu-id="7d9c2-348">L’application exécute les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="7d9c2-348">The application performs the following:</span></span>

1. <span data-ttu-id="7d9c2-349">Écoute une instance Event Hub dans laquelle Stream Analytics publie les événements en continu.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-349">Listens to an Event Hub instance where Stream Analytics is publishing the events in a pattern continuously.</span></span> <span data-ttu-id="7d9c2-350">![Requête Stream Analytics pour la publication des données](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 - Requête Stream Analytics pour la publication des données dans une instance Event Hub de sortie*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-350">![Stream Analytics query for publishing the data](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 – Stream Analytics query for publishing the data to an output Event Hub instance*</span></span> 
2. <span data-ttu-id="7d9c2-351">Pour chaque événement reçu par cette application :</span><span class="sxs-lookup"><span data-stu-id="7d9c2-351">For every event that this application receives:</span></span> 
   
   * <span data-ttu-id="7d9c2-352">Traite les données à l’aide du point de terminaison Request-Response Scoring (RRS) de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-352">Processes the data using Machine Learning Request-Response Scoring (RRS) endpoint.</span></span> <span data-ttu-id="7d9c2-353">Le point de terminaison RRS est automatiquement publié dans le cadre du déploiement.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-353">The RRS endpoint is automatically published as part of the deployment.</span></span>
   * <span data-ttu-id="7d9c2-354">La sortie RRS est publiée dans un ensemble de données Power BI à l’aide d’API Push.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-354">The RRS output is published to a Power BI dataset using the push APIs.</span></span>

<span data-ttu-id="7d9c2-355">Ce modèle s’applique également aux scénarios dans lesquels vous souhaitez intégrer une application métier avec le flux d’analyse en temps réel pour des scénarios tels que les alertes, les notifications et la messagerie.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-355">This pattern is also applicable to scenarios in which you want to integrate a Line of Business (LoB) application with the real-time analytics flow, for scenarios such as alerts, notifications, and messaging.</span></span>

<span data-ttu-id="7d9c2-356">Cliquez sur [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) pour télécharger la solution RealtimeDashboardApp Visual Studio pour les personnalisations.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-356">Click [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) to download the RealtimeDashboardApp Visual Studio solution for customizations.</span></span> 

<span data-ttu-id="7d9c2-357">**Pour exécuter l’application de tableau de bord en temps réel**</span><span class="sxs-lookup"><span data-stu-id="7d9c2-357">**To execute the Real-time Dashboard Application**</span></span>
1. <span data-ttu-id="7d9c2-358">Extrayez le fichier et enregistrez-le localement ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – Dossier RealtimeDashboardApp*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-358">Extract and save locally ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – RealtimeDashboardApp folder*</span></span>  
2. <span data-ttu-id="7d9c2-359">Exécutez l’application RealtimeDashboardApp.exe</span><span class="sxs-lookup"><span data-stu-id="7d9c2-359">Execute the application RealtimeDashboardApp.exe</span></span>
3. <span data-ttu-id="7d9c2-360">Entrez des informations d’identification Power BI valides, connectez-vous, puis cliquez sur Accept</span><span class="sxs-lookup"><span data-stu-id="7d9c2-360">Provide valid Power BI credentials, sign in and click Accept</span></span> ![Connexion à Power BI avec l’application de tableau de bord en temps réel](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Fin de connexion à Power BI avec l’application de tableau de bord en temps réel](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

<span data-ttu-id="7d9c2-363">*Figure 17 – RealtimeDashboardApp : connexion à Power BI*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-363">*Figure 17 – RealtimeDashboardApp: Sign-in to Power BI*</span></span>

>[!NOTE] 
><span data-ttu-id="7d9c2-364">Si vous voulez vider le jeu de données Power BI, exécutez l’application RealtimeDashboardApp avec le paramètre « flushdata » :</span><span class="sxs-lookup"><span data-stu-id="7d9c2-364">If you want to flush the Power BI dataset, execute the RealtimeDashboardApp with the "flushdata" parameter:</span></span> 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a><span data-ttu-id="7d9c2-365">Analyse en mode batch</span><span class="sxs-lookup"><span data-stu-id="7d9c2-365">Batch analysis</span></span>
<span data-ttu-id="7d9c2-366">L’objectif ici est d’expliquer comment Contoso Motors exploite les capacités de calcul Azure pour tirer parti des Big Data afin d’obtenir de précieuses informations sur les schémas de conduite, le comportement d’utilisation et l’état du véhicule.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-366">The goal here is to show how Contoso Motors utilizes the Azure compute capabilities to harness big data to gain rich insights on driving pattern, usage behavior, and vehicle health.</span></span> <span data-ttu-id="7d9c2-367">Il est ainsi possible :</span><span class="sxs-lookup"><span data-stu-id="7d9c2-367">This makes it possible to:</span></span>

* <span data-ttu-id="7d9c2-368">d’améliorer l’expérience client à moindre coût en offrant des perspectives sur les habitudes de conduite et sur les comportements de conduite économes en carburant ;</span><span class="sxs-lookup"><span data-stu-id="7d9c2-368">Improve the customer experience and make it cheaper by providing insights on driving habits and fuel efficient driving behaviors</span></span>
* <span data-ttu-id="7d9c2-369">de s’informer de manière proactive sur les clients et leurs modèles de conduite afin d’orienter les décisions commerciales et de fournir des produits et services de meilleure qualité.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-369">Learn proactively about customers and their driving patters to govern business decisions and provide the best in class products & services</span></span>

<span data-ttu-id="7d9c2-370">Dans cette solution, nous ciblons les mesures suivantes :</span><span class="sxs-lookup"><span data-stu-id="7d9c2-370">In this solution, we are targeting the following metrics:</span></span>

1. <span data-ttu-id="7d9c2-371">**Comportement de conduite agressive**: Identifie la tendance des modèles, des emplacements, des conditions de conduite et de la période de l’année pour fournir des informations sur les modes de conduite agressive.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-371">**Aggressive driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of the year to gain insights on aggressive driving patterns.</span></span> <span data-ttu-id="7d9c2-372">Contoso Motors peut utiliser ces informations pour ses campagnes marketing, pour créer de nouvelles fonctionnalités personnalisées et pour proposer des assurances adaptées à l’utilisation.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-372">Contoso Motors can use these insights for marketing campaigns, driving new personalized features and usage-based insurance.</span></span>
2. <span data-ttu-id="7d9c2-373">**Comportement de conduite économe en carburant**: Identifie la tendance des modèles, des emplacements, des conditions de conduite et de la période de l’année pour fournir des informations sur les modes de conduite agressive.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-373">**Fuel efficient driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of the year to gain insights on fuel efficient driving patterns.</span></span> <span data-ttu-id="7d9c2-374">Contoso Motors peut utiliser ces informations pour ses campagnes marketing, et pour proposer aux conducteurs de nouvelles fonctionnalités et des rapports proactifs afin d’encourager les habitudes de conduite économique et respectueuses de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-374">Contoso Motors can use these insights for marketing campaigns, driving new features and proactive reporting to the drivers for cost effective and environment friendly driving habits.</span></span> 
3. <span data-ttu-id="7d9c2-375">**Modèles de rappel**: Identifie les modèles nécessitant des rappels en améliorant l’expérience d’apprentissage automatique pour la détection des anomalies.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-375">**Recall models**: Identifies models requiring recalls by operationalizing the anomaly detection machine learning experiment</span></span>

<span data-ttu-id="7d9c2-376">Examinons en détail chacune de ces mesures :</span><span class="sxs-lookup"><span data-stu-id="7d9c2-376">Let's look into the details of each of these metrics,</span></span>

<span data-ttu-id="7d9c2-377">**Mode de conduite agressive**</span><span class="sxs-lookup"><span data-stu-id="7d9c2-377">**Aggressive driving pattern**</span></span>

<span data-ttu-id="7d9c2-378">Les signaux et les données de diagnostic de véhicules partitionnés sont traités dans le pipeline nommé « AggresiveDrivingPatternPipeline », qui utilise Hive pour déterminer les modèles, l’emplacement, le véhicule, les conditions de conduite et d’autres paramètres dénotant un mode de conduite agressive.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-378">The partitioned vehicle signals and diagnostic data are processed in the pipeline named "AggresiveDrivingPatternPipeline" using Hive to determine the models, location, vehicle, driving conditions, and other parameters that exhibits aggressive driving pattern.</span></span>

<span data-ttu-id="7d9c2-379">![Workflow de modèle conduite agressive](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Workflow de modèle conduite agressive*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-379">![Aggressive driving pattern workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Aggressive driving pattern workflow*</span></span>


<span data-ttu-id="7d9c2-380">***Requête Hive de mode de conduite agressive***</span><span class="sxs-lookup"><span data-stu-id="7d9c2-380">***Aggressive driving pattern Hive query***</span></span>

<span data-ttu-id="7d9c2-381">Le script Hive nommé « aggresivedriving.hql » et utilisé pour analyser le modèle de condition de conduite agressive se trouve dans le dossier « \demo\src\connectedcar\scripts » du fichier zip téléchargé.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-381">The Hive script named "aggresivedriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 

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


<span data-ttu-id="7d9c2-382">Il utilise à la fois la position du levier de vitesses, l’état de la pédale de frein et la vitesse du véhicule pour détecter un comportement de conduite imprudent/agressif en fonction du schéma de freinage à vitesse élevée.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-382">It uses the combination of vehicle's transmission gear position, brake pedal status, and speed to detect reckless/aggressive driving behavior based on braking pattern at high speed.</span></span> 

<span data-ttu-id="7d9c2-383">Une fois le pipeline exécuté, les partitions suivantes sont générées dans votre compte de stockage sous le conteneur « connectedcar ».</span><span class="sxs-lookup"><span data-stu-id="7d9c2-383">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Sortie AggressiveDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

<span data-ttu-id="7d9c2-385">*Figure 19 – Sortie AggressiveDrivingPatternPipeline*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-385">*Figure 19 – AggressiveDrivingPatternPipeline output*</span></span>

<span data-ttu-id="7d9c2-386">**Mode de conduite économe en carburant**</span><span class="sxs-lookup"><span data-stu-id="7d9c2-386">**Fuel efficient driving pattern**</span></span>

<span data-ttu-id="7d9c2-387">Les signaux et les données de diagnostic de véhicules partitionnés sont traités dans le pipeline nommé « FuelEfficientDrivingPatternPipeline ».</span><span class="sxs-lookup"><span data-stu-id="7d9c2-387">The partitioned vehicle signals and diagnostic data are processed in the pipeline named "FuelEfficientDrivingPatternPipeline".</span></span> <span data-ttu-id="7d9c2-388">Hive est utilisé pour déterminer les modèles, l’emplacement, le véhicule, les conditions de conduite et d’autres propriétés dénotant un mode de conduite économe en carburant.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-388">Hive is used to determine the models, location, vehicle, driving conditions, and other properties that exhibit fuel efficient driving pattern.</span></span>

![Mode de conduite économe en carburant](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

<span data-ttu-id="7d9c2-390">*Figure 20 - Workflow du mode de conduite économe en carburant*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-390">*Figure 20 – Fuel-efficient driving pattern workflow*</span></span>

<span data-ttu-id="7d9c2-391">***Requête Hive du mode de conduite économe en carburant***</span><span class="sxs-lookup"><span data-stu-id="7d9c2-391">***Fuel efficient driving pattern Hive query***</span></span>

<span data-ttu-id="7d9c2-392">Le script Hive nommé « fuelefficientdriving.hql » et utilisé pour analyser le modèle de condition de conduite économe en carburant se trouve dans le dossier « \demo\src\connectedcar\scripts » du fichier zip téléchargé.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-392">The Hive script named "fuelefficientdriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 

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


<span data-ttu-id="7d9c2-393">Il utilise à la fois la position du levier de vitesses, l’état de la pédale de frein, la vitesse du véhicule et la position de la pédale d’accélérateur pour détecter un comportement de conduite économe en carburant en fonction des schémas d’accélération, de freinage et de vitesse élevée.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-393">It uses the combination of vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position to detect fuel efficient driving behavior based on acceleration, braking, and speed patterns.</span></span> 

<span data-ttu-id="7d9c2-394">Une fois le pipeline exécuté, les partitions suivantes sont générées dans votre compte de stockage sous le conteneur « connectedcar ».</span><span class="sxs-lookup"><span data-stu-id="7d9c2-394">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Sortie FuelEfficientDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

<span data-ttu-id="7d9c2-396">*Figure 21 – Sortie FuelEfficientDrivingPatternPipeline*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-396">*Figure 21 – FuelEfficientDrivingPatternPipeline output*</span></span>

<span data-ttu-id="7d9c2-397">**Prédictions des rappels**</span><span class="sxs-lookup"><span data-stu-id="7d9c2-397">**Recall Predictions**</span></span>

<span data-ttu-id="7d9c2-398">L’expérience d’apprentissage automatique est configurée et publiée en tant que service web dans le cadre du déploiement de la solution.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-398">The machine learning experiment is provisioned and published as a web service as part of the solution deployment.</span></span> <span data-ttu-id="7d9c2-399">Le point de terminaison de notation par lots est utilisé dans ce workflow, enregistré tant que service Data Factory lié et mis en œuvre à l’aide de l’activité de notation par lots de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-399">The batch scoring end point is leveraged in this workflow, registered as a data factory linked service and operationalized using data factory batch scoring activity.</span></span>

![Point de terminaison Machine Learning](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

<span data-ttu-id="7d9c2-401">*Figure 22 – Point de terminaison Machine Learning enregistré comme service lié dans Data Factory*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-401">*Figure 22 – Machine learning endpoint registered as a linked service in data factory*</span></span>

<span data-ttu-id="7d9c2-402">Le service lié enregistré est utilisé dans le DetectAnomalyPipeline pour noter les données à l’aide du modèle de détection d’anomalies.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-402">The registered linked service is used in the DetectAnomalyPipeline to score the data using the anomaly detection model.</span></span> 

![Activité de notation par lot de Machine Learning dans Data Factory](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

<span data-ttu-id="7d9c2-404">*Figure 23 – Activité de notation par lot d’Azure Machine Learning dans Data Factory*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-404">*Figure 23 – Azure Machine Learning Batch Scoring activity in data factory*</span></span> 

<span data-ttu-id="7d9c2-405">Quelques étapes sont exécutées dans ce pipeline pour préparer les données afin de les rendre opérationnelles avec le service web de notation par lots.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-405">There are few steps performed in this pipeline for data preparation so that it can be operationalized with the batch scoring web service.</span></span> 

![DetectAnomalyPipeline pour la prédiction des véhicules nécessitant des rappels](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

<span data-ttu-id="7d9c2-407">*Figure 24 – DetectAnomalyPipeline pour la prédiction des véhicules nécessitant des rappels*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-407">*Figure 24 – DetectAnomalyPipeline for predicting vehicles requiring recalls*</span></span> 

<span data-ttu-id="7d9c2-408">***Requête Hive de détection des anomalies***</span><span class="sxs-lookup"><span data-stu-id="7d9c2-408">***Anomaly detection Hive query***</span></span>

<span data-ttu-id="7d9c2-409">Une fois l’évaluation terminée, une activité HDInsight est utilisée pour traiter et agréger les données que le modèle considère comme des anomalies, avec un score de probabilité d’au moins 0,60.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-409">Once the scoring is completed, an HDInsight activity is used to process and aggregate the data that are categorized as anomalies by the model with a probability score of 0.60 or higher.</span></span>

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


<span data-ttu-id="7d9c2-410">Une fois le pipeline exécuté, les partitions suivantes sont générées dans votre compte de stockage sous le conteneur « connectedcar ».</span><span class="sxs-lookup"><span data-stu-id="7d9c2-410">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Sortie DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

<span data-ttu-id="7d9c2-412">*Figure 25 – Sortie DetectAnomalyPipeline*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-412">*Figure 25 – DetectAnomalyPipeline output*</span></span>

## <a name="publish"></a><span data-ttu-id="7d9c2-413">Publier</span><span class="sxs-lookup"><span data-stu-id="7d9c2-413">Publish</span></span>

### <a name="real-time-analysis"></a><span data-ttu-id="7d9c2-414">Analyse en temps réel</span><span class="sxs-lookup"><span data-stu-id="7d9c2-414">Real-time analysis</span></span>
<span data-ttu-id="7d9c2-415">L’une des requêtes de la tâche Stream Analytics publie les événements dans une instance Event Hub de sortie.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-415">One of the queries in the Stream Analytics job publishes the events to an output Event Hub instance.</span></span> 

![Publication des événements de la tâche Stream Analytics dans une instance Event Hub de sortie](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

<span data-ttu-id="7d9c2-417">*Figure 26 - Publication des événements de la tâche Stream Analytics dans une instance Event Hub de sortie*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-417">*Figure 26 – Stream Analytics job publishes to an output Event Hub instance*</span></span>

![Requête Stream Analytics pour la publication d’événements dans une instance Event Hub de sortie](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

<span data-ttu-id="7d9c2-419">*Figure 27 - Requête Stream Analytics pour la publication d’événements dans une instance Event Hub de sortie*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-419">*Figure 27 – Stream Analytics query to publish to the output Event Hub instance*</span></span>

<span data-ttu-id="7d9c2-420">Ce flux d’événements est utilisé par l’application RealTimeDashboardApp intégrée dans la solution.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-420">This stream of events is consumed by the RealTimeDashboardApp included in the solution.</span></span> <span data-ttu-id="7d9c2-421">Cette application s’appuie sur le service web Request-Response de Machine Learning pour calculer les scores en temps réel, et publie les données obtenues dans un jeu de données Power BI.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-421">This application leverages the Machine Learning Request-Response web service for real-time scoring and publishes the resultant data to a Power BI dataset for consumption.</span></span> 

### <a name="batch-analysis"></a><span data-ttu-id="7d9c2-422">Analyse en mode batch</span><span class="sxs-lookup"><span data-stu-id="7d9c2-422">Batch analysis</span></span>
<span data-ttu-id="7d9c2-423">Les résultats du traitement par lots et en temps réel sont publiés dans les tables de base de données SQL Azure pour être consommés.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-423">The results of the batch and real-time processing are published to the Azure SQL Database tables for consumption.</span></span> <span data-ttu-id="7d9c2-424">Le serveur SQL, la base de données et les tables Azure sont créés automatiquement dans le cadre du script d’installation.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-424">The Azure SQL Server, Database, and the tables are created automatically as part of the setup script.</span></span> 

![Copie des résultats du traitement par lots dans le workflow d’entrepôt de données](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

<span data-ttu-id="7d9c2-426">*Figure 28 – Copie des résultats du traitement par lots dans le workflow d’entrepôt de données*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-426">*Figure 28 – Batch processing results copy to data mart workflow*</span></span>

![Publication des événements de la tâche Stream Analytics dans un entrepôt de données](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

<span data-ttu-id="7d9c2-428">*Figure 29 - Publication des événements de la tâche Stream Analytics dans un entrepôt de données*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-428">*Figure 29 – Stream Analytics job publishes to data mart*</span></span>

![Configuration de l’entrepôt de données dans la tâche Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

<span data-ttu-id="7d9c2-430">*Figure 30 – Configuration de l’entrepôt de données dans la tâche Stream Analytics*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-430">*Figure 30 – Data mart setting in Stream Analytics job*</span></span>

## <a name="consume"></a><span data-ttu-id="7d9c2-431">Utiliser</span><span class="sxs-lookup"><span data-stu-id="7d9c2-431">Consume</span></span>
<span data-ttu-id="7d9c2-432">Power BI offre à cette solution un tableau de bord complet permettant de visualiser à la fois les données en temps réel et les analyses prédictives.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-432">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="7d9c2-433">Cliquez ici pour obtenir des instructions détaillées sur la configuration des rapports et du tableau de bord Power BI.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-433">Click here for detailed instructions on setting up the Power BI reports and the dashboard.</span></span> <span data-ttu-id="7d9c2-434">Le tableau de bord final doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="7d9c2-434">The final dashboard looks like this:</span></span>

![Tableau de bord Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

<span data-ttu-id="7d9c2-436">*Figure 31 - Tableau de bord Power BI*</span><span class="sxs-lookup"><span data-stu-id="7d9c2-436">*Figure 31 - Power BI Dashboard*</span></span>

## <a name="summary"></a><span data-ttu-id="7d9c2-437">Résumé</span><span class="sxs-lookup"><span data-stu-id="7d9c2-437">Summary</span></span>
<span data-ttu-id="7d9c2-438">Ce document explore de façon détaillée la solution Vehicle Telemetry Analytics.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-438">This document contains a detailed drill-down of the Vehicle Telemetry Analytics Solution.</span></span> <span data-ttu-id="7d9c2-439">Il présente un modèle d’architecture lambda pour une analyse en temps réel et par lots reposant sur des prédictions et des actions.</span><span class="sxs-lookup"><span data-stu-id="7d9c2-439">This showcases a lambda architecture pattern for real-time and batch analytics with predictions and actions.</span></span> <span data-ttu-id="7d9c2-440">Ce modèle s’applique à un large éventail de scénarios qui requièrent des analyses à chaud (en temps réel) et à froid (par lots).</span><span class="sxs-lookup"><span data-stu-id="7d9c2-440">This pattern applies to a wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span></span> 

