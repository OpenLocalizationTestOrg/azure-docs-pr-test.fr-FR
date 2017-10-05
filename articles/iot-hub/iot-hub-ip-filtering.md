---
title: "Filtres de connexion IP d’Azure Hub IoT | Microsoft Docs"
description: "Utilisation de filtres IP pour bloquer les connexions à partir d’adresses IP spécifiques pour votre Azure IoT Hub. Vous pouvez bloquer les connexions à partir d’adresses IP individuelles ou de plages d’adresses IP."
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 85f5f044faddd5180f0c19d3f2c235b20f6373d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-ip-filters"></a><span data-ttu-id="5d55a-104">Utiliser des filtres IP</span><span class="sxs-lookup"><span data-stu-id="5d55a-104">Use IP filters</span></span>

<span data-ttu-id="5d55a-105">La sécurité est un aspect important de toute solution IoT basée sur Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5d55a-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="5d55a-106">Parfois, dans le cadre de votre configuration de sécurité, vous devez spécifier explicitement les adresses IP à partir desquelles les appareils peuvent se connecter.</span><span class="sxs-lookup"><span data-stu-id="5d55a-106">Sometimes you need to explicitly specify the IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="5d55a-107">La fonctionnalité _Filtre IP_ vous permet de configurer des règles de rejet ou d’acceptation du trafic provenant de certaines adresses IPv4.</span><span class="sxs-lookup"><span data-stu-id="5d55a-107">The _IP filter_ feature enables you to configure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-to-use"></a><span data-ttu-id="5d55a-108">Quand utiliser</span><span class="sxs-lookup"><span data-stu-id="5d55a-108">When to use</span></span>

<span data-ttu-id="5d55a-109">Il existe deux cas d’utilisation spécifiques illustrant lorsqu’il est utile de bloquer les points de terminaison IoT Hub pour certaines adresses IP :</span><span class="sxs-lookup"><span data-stu-id="5d55a-109">There are two specific use-cases when it is useful to block the IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="5d55a-110">Votre IoT Hub ne doit recevoir du trafic qu’à partir d’une plage spécifiée d’adresses IP et rejeter tout le reste.</span><span class="sxs-lookup"><span data-stu-id="5d55a-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="5d55a-111">Par exemple, vous utilisez votre IoT Hub avec [Azure Express Route] pour créer des connexions privées entre un IoT Hub et votre infrastructure locale.</span><span class="sxs-lookup"><span data-stu-id="5d55a-111">For example, you are using your IoT hub with [Azure Express Route] to create private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="5d55a-112">Vous devez refuser le trafic provenant d’adresses IP qui ont été identifiées comme suspectes par l’administrateur de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5d55a-112">You need to reject traffic from IP addresses that have been identified as suspicious by the IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="5d55a-113">Application des règles de filtre</span><span class="sxs-lookup"><span data-stu-id="5d55a-113">How filter rules are applied</span></span>

<span data-ttu-id="5d55a-114">Les règles de filtre IP sont appliquées au niveau du service IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5d55a-114">The IP filter rules are applied at the IoT Hub service level.</span></span> <span data-ttu-id="5d55a-115">Par conséquent, les règles de filtre IP s’appliquent à toutes les connexions issues des appareils et des applications principales utilisant n’importe quel protocole pris en charge.</span><span class="sxs-lookup"><span data-stu-id="5d55a-115">Therefore the IP filter rules apply to all connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="5d55a-116">Toute tentative de connexion à partir d’une adresse IP qui correspond à une règle IP de rejet dans votre IoT Hub reçoit un code d’état 401 non autorisé et une description.</span><span class="sxs-lookup"><span data-stu-id="5d55a-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="5d55a-117">Le message de réponse ne mentionne pas la règle IP.</span><span class="sxs-lookup"><span data-stu-id="5d55a-117">The response message does not mention the IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="5d55a-118">Paramètre par défaut</span><span class="sxs-lookup"><span data-stu-id="5d55a-118">Default setting</span></span>

<span data-ttu-id="5d55a-119">Par défaut, la grille **Filtre IP** dans le portail pour un IoT Hub est vide.</span><span class="sxs-lookup"><span data-stu-id="5d55a-119">By default, the **IP Filter** grid in the portal for an IoT hub is empty.</span></span> <span data-ttu-id="5d55a-120">Ce paramètre par défaut signifie que votre concentrateur accepte les connexions de n’importe quelle adresse IP.</span><span class="sxs-lookup"><span data-stu-id="5d55a-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="5d55a-121">Ce paramètre par défaut est équivalent à une règle qui accepte la plage d’adresses IP 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="5d55a-121">This default setting is equivalent to a rule that accepts the 0.0.0.0/0 IP address range.</span></span>

![Paramètres de filtre IP par défaut d’IoT Hub][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="5d55a-123">Ajouter ou modifier une règle de filtre IP</span><span class="sxs-lookup"><span data-stu-id="5d55a-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="5d55a-124">Lorsque vous ajoutez une règle de filtre IP, vous êtes invité à renseigner les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="5d55a-124">When you add an IP filter rule, you are prompted for the following values:</span></span>

- <span data-ttu-id="5d55a-125">Un **nom de règle de filtre IP** qui doit être une chaîne unique, ne respectant pas la casse, alphanumérique, comptant jusqu'à 128 caractères.</span><span class="sxs-lookup"><span data-stu-id="5d55a-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up to 128 characters long.</span></span> <span data-ttu-id="5d55a-126">Seuls les caractères alphanumériques ASCII 7 bits et `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` sont acceptés.</span><span class="sxs-lookup"><span data-stu-id="5d55a-126">Only the ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="5d55a-127">Sélectionnez **rejeter** ou **accepter** comme **action** pour la règle de filtre IP.</span><span class="sxs-lookup"><span data-stu-id="5d55a-127">Select a **reject** or **accept** as the **action** for the IP filter rule.</span></span>
- <span data-ttu-id="5d55a-128">Fournissez une adresse IPv4 unique ou un bloc d’adresses IP en notation CIDR.</span><span class="sxs-lookup"><span data-stu-id="5d55a-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="5d55a-129">Par exemple, dans la notation CIDR, 192.168.100.0/22 représente les 1024 adresses IPv4 allant de 192.168.100.0 à 192.168.103.255.</span><span class="sxs-lookup"><span data-stu-id="5d55a-129">For example, in CIDR notation 192.168.100.0/22 represents the 1024 IPv4 addresses from 192.168.100.0 to 192.168.103.255.</span></span>

![Ajouter une règle de filtre IP à un IoT Hub][img-ip-filter-add-rule]

<span data-ttu-id="5d55a-131">Une fois la règle enregistrée, une alerte s’affiche vous informant que la mise à jour est en cours.</span><span class="sxs-lookup"><span data-stu-id="5d55a-131">After you save the rule, you see an alert notifying you that the update is in progress.</span></span>

![Notification sur l’enregistrement d’une règle de filtre IP][img-ip-filter-save-new-rule]

<span data-ttu-id="5d55a-133">L’option **Ajouter** est désactivée lorsque vous atteignez le nombre maximal de dix règles de filtre IP.</span><span class="sxs-lookup"><span data-stu-id="5d55a-133">The **Add** option is disabled when you reach the maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="5d55a-134">Vous pouvez modifier une règle existante en double-cliquant sur la ligne qui contient la règle.</span><span class="sxs-lookup"><span data-stu-id="5d55a-134">You can edit an existing rule by double-clicking the row that contains the rule.</span></span>

> [!NOTE]
> <span data-ttu-id="5d55a-135">Le rejet d’adresses IP est de nature à empêcher d’autres services Azure (comme Azure Stream Analytics, Azure Virtual Machines ou l’Explorateur d’appareils dans le portail) d’interagir avec IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5d55a-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or the Device Explorer in the portal) from interacting with the IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="5d55a-136">Si vous utilisez Azure Stream Analytics (ASA) pour lire les messages à partir d’un hub IoT avec le filtrage IP activé, utilisez le nom compatible avec Event Hub et le point de terminaison de votre hub IoT dans la chaîne de connexion ASA.</span><span class="sxs-lookup"><span data-stu-id="5d55a-136">If you use Azure Stream Analytics (ASA) to read messages from an IoT hub with IP filtering enabled, use the Event Hub-compatible name and endpoint of your IoT Hub in the ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="5d55a-137">Suppression d’une règle de filtre IP</span><span class="sxs-lookup"><span data-stu-id="5d55a-137">Delete an IP filter rule</span></span>

<span data-ttu-id="5d55a-138">Pour supprimer une règle de filtre IP, sélectionnez une ou plusieurs règles dans la grille et cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="5d55a-138">To delete an IP filter rule, select one or more rules in the grid and click **Delete**.</span></span>

![Supprimer une règle de filtre IP de l’IoT Hub][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="5d55a-140">Évaluation de règle de filtre IP</span><span class="sxs-lookup"><span data-stu-id="5d55a-140">IP filter rule evaluation</span></span>

<span data-ttu-id="5d55a-141">Les règles de filtre IP sont appliquées dans l’ordre et la première règle qui correspond à l’adresse IP détermine l’action d’acceptation ou de rejet.</span><span class="sxs-lookup"><span data-stu-id="5d55a-141">IP filter rules are applied in order and the first rule that matches the IP address determines the accept or reject action.</span></span>

<span data-ttu-id="5d55a-142">Par exemple, si vous souhaitez accepter les adresses dans la plage 192.168.100.0/22 et rejeter tout le reste, la première règle de la grille doit accepter la plage d’adresses 192.168.100.0/22.</span><span class="sxs-lookup"><span data-stu-id="5d55a-142">For example, if you want to accept addresses in the range 192.168.100.0/22 and reject everything else, the first rule in the grid should accept the address range 192.168.100.0/22.</span></span> <span data-ttu-id="5d55a-143">La règle suivante doit rejeter toutes les adresses à l’aide de la plage 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="5d55a-143">The next rule should reject all addresses by using the range 0.0.0.0/0.</span></span>

<span data-ttu-id="5d55a-144">Vous pouvez modifier l’ordre de vos règles de filtre IP dans la grille en cliquant sur les trois points verticaux au début d’une ligne et en effectuant un glisser-déplacer.</span><span class="sxs-lookup"><span data-stu-id="5d55a-144">You can change the order of your IP filter rules in the grid by clicking the three vertical dots at the start of a row and using drag and drop.</span></span>

<span data-ttu-id="5d55a-145">Pour enregistrer le nouvel ordre de vos règles de filtre IP, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5d55a-145">To save your new IP filter rule order, click **Save**.</span></span>

![Modifier l’ordre de vos règles de filtre IP de l’IoT Hub][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="5d55a-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5d55a-147">Next steps</span></span>

<span data-ttu-id="5d55a-148">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="5d55a-148">To further explore the capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="5d55a-149">[Surveillance des opérations][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="5d55a-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="5d55a-150">[Métriques d’IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="5d55a-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
<span data-ttu-id="5d55a-151">[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services</span><span class="sxs-lookup"><span data-stu-id="5d55a-151">[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services</span></span>

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md