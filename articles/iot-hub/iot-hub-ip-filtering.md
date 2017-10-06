---
title: filtres de connexion IoT Hub IP aaaAzure | Documents Microsoft
description: "Comment les adresses IP de toouse tooblock des connexions à partir de l’adresse IP spécifique de filtrage pour tooyour Azure IoT hub. Vous pouvez bloquer les connexions à partir d’adresses IP individuelles ou de plages d’adresses IP."
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
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a><span data-ttu-id="9776b-104">Utiliser des filtres IP</span><span class="sxs-lookup"><span data-stu-id="9776b-104">Use IP filters</span></span>

<span data-ttu-id="9776b-105">La sécurité est un aspect important de toute solution IoT basée sur Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9776b-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="9776b-106">Vous devez parfois tooexplicitly spécifier hello, adresses de base de données à partir de laquelle les appareils peuvent se connecter en tant que partie de votre configuration de sécurité.</span><span class="sxs-lookup"><span data-stu-id="9776b-106">Sometimes you need tooexplicitly specify hello IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="9776b-107">Hello _filtre IP_ fonctionnalité vous permet de tooconfigure les règles de refus ou accepter le trafic provenant de certaines adresses IPv4.</span><span class="sxs-lookup"><span data-stu-id="9776b-107">hello _IP filter_ feature enables you tooconfigure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-toouse"></a><span data-ttu-id="9776b-108">Lorsque toouse</span><span class="sxs-lookup"><span data-stu-id="9776b-108">When toouse</span></span>

<span data-ttu-id="9776b-109">Il existe deux cas d’utilisation spécifiques lorsqu’il est utile de tooblock hello IoT Hub points de terminaison pour certaines adresses IP :</span><span class="sxs-lookup"><span data-stu-id="9776b-109">There are two specific use-cases when it is useful tooblock hello IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="9776b-110">Votre IoT Hub ne doit recevoir du trafic qu’à partir d’une plage spécifiée d’adresses IP et rejeter tout le reste.</span><span class="sxs-lookup"><span data-stu-id="9776b-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="9776b-111">Par exemple, vous utilisez votre IoT hub avec [Azure Expressroute] toocreate des connexions privées entre un IoT hub et votre infrastructure locale.</span><span class="sxs-lookup"><span data-stu-id="9776b-111">For example, you are using your IoT hub with [Azure Express Route] toocreate private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="9776b-112">Vous devez le trafic de tooreject à partir d’adresses IP qui ont été identifiées comme suspecte par l’administrateur de hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="9776b-112">You need tooreject traffic from IP addresses that have been identified as suspicious by hello IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="9776b-113">Application des règles de filtre</span><span class="sxs-lookup"><span data-stu-id="9776b-113">How filter rules are applied</span></span>

<span data-ttu-id="9776b-114">règles de filtre IP Hello sont appliqués au hello au niveau du service IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="9776b-114">hello IP filter rules are applied at hello IoT Hub service level.</span></span> <span data-ttu-id="9776b-115">Par conséquent, les règles de filtre IP hello appliquent tooall des connexions à partir de périphériques et les applications de serveur principal à l’aide de n’importe quel protocole pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9776b-115">Therefore hello IP filter rules apply tooall connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="9776b-116">Toute tentative de connexion à partir d’une adresse IP qui correspond à une règle IP de rejet dans votre IoT Hub reçoit un code d’état 401 non autorisé et une description.</span><span class="sxs-lookup"><span data-stu-id="9776b-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="9776b-117">message de réponse Hello ne mentionne pas la règle d’adresse IP hello.</span><span class="sxs-lookup"><span data-stu-id="9776b-117">hello response message does not mention hello IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="9776b-118">Paramètre par défaut</span><span class="sxs-lookup"><span data-stu-id="9776b-118">Default setting</span></span>

<span data-ttu-id="9776b-119">Par défaut, hello **filtre IP** grille dans le portail hello pour un hub IoT est vide.</span><span class="sxs-lookup"><span data-stu-id="9776b-119">By default, hello **IP Filter** grid in hello portal for an IoT hub is empty.</span></span> <span data-ttu-id="9776b-120">Ce paramètre par défaut signifie que votre concentrateur accepte les connexions de n’importe quelle adresse IP.</span><span class="sxs-lookup"><span data-stu-id="9776b-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="9776b-121">Ce paramètre par défaut est la règle tooa équivalente qui accepte une plage d’adresses IP hello 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="9776b-121">This default setting is equivalent tooa rule that accepts hello 0.0.0.0/0 IP address range.</span></span>

![Paramètres de filtre IP par défaut d’IoT Hub][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="9776b-123">Ajouter ou modifier une règle de filtre IP</span><span class="sxs-lookup"><span data-stu-id="9776b-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="9776b-124">Lorsque vous ajoutez une règle de filtrage IP, vous êtes invité pour hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="9776b-124">When you add an IP filter rule, you are prompted for hello following values:</span></span>

- <span data-ttu-id="9776b-125">Un **nom de règle de filtre IP** qui doit être une chaîne alphanumérique, unique et pas la casse des caractères too128.</span><span class="sxs-lookup"><span data-stu-id="9776b-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up too128 characters long.</span></span> <span data-ttu-id="9776b-126">Seul hello ASCII 7 bits des caractères alphanumériques plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` sont acceptées.</span><span class="sxs-lookup"><span data-stu-id="9776b-126">Only hello ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="9776b-127">Sélectionnez un **rejeter** ou **accepter** comme hello **action** pour la règle de filtre IP hello.</span><span class="sxs-lookup"><span data-stu-id="9776b-127">Select a **reject** or **accept** as hello **action** for hello IP filter rule.</span></span>
- <span data-ttu-id="9776b-128">Fournissez une adresse IPv4 unique ou un bloc d’adresses IP en notation CIDR.</span><span class="sxs-lookup"><span data-stu-id="9776b-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="9776b-129">Par exemple, CIDR notation 192.168.100.0/22 représente des adresses IPv4 hello 1024 provenant de 192.168.100.0 too192.168.103.255.</span><span class="sxs-lookup"><span data-stu-id="9776b-129">For example, in CIDR notation 192.168.100.0/22 represents hello 1024 IPv4 addresses from 192.168.100.0 too192.168.103.255.</span></span>

![Ajouter un hub IoT tooan de règle de filtre IP][img-ip-filter-add-rule]

<span data-ttu-id="9776b-131">Après avoir enregistré la règle de hello, vous voyez une alerte vous informe de que cette mise à jour hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="9776b-131">After you save hello rule, you see an alert notifying you that hello update is in progress.</span></span>

![Notification sur l’enregistrement d’une règle de filtre IP][img-ip-filter-save-new-rule]

<span data-ttu-id="9776b-133">Hello **ajouter** option est désactivée lorsque vous atteignez au maximum 10 règles de filtre IP hello.</span><span class="sxs-lookup"><span data-stu-id="9776b-133">hello **Add** option is disabled when you reach hello maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="9776b-134">Vous pouvez modifier une règle existante en double-cliquant sur la ligne hello qui contient la règle de hello.</span><span class="sxs-lookup"><span data-stu-id="9776b-134">You can edit an existing rule by double-clicking hello row that contains hello rule.</span></span>

> [!NOTE]
> <span data-ttu-id="9776b-135">Rejet IP adresses peuvent empêcher des autres Services Azure (par exemple, Analytique de flux de données Azure, les Machines virtuelles Azure ou hello Explorateur de périphérique dans le portail de hello) d’interagir avec IoT hub de hello.</span><span class="sxs-lookup"><span data-stu-id="9776b-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or hello Device Explorer in hello portal) from interacting with hello IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="9776b-136">Si vous utilisez des messages de tooread Analytique de flux de données Azure (ASA) à partir d’un IoT hub avec le filtrage IP est activé, utiliser le nom du concentrateur d’événements compatibles hello et le point de terminaison de votre IoT Hub Bonjour chaîne de connexion ASA.</span><span class="sxs-lookup"><span data-stu-id="9776b-136">If you use Azure Stream Analytics (ASA) tooread messages from an IoT hub with IP filtering enabled, use hello Event Hub-compatible name and endpoint of your IoT Hub in hello ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="9776b-137">Suppression d’une règle de filtre IP</span><span class="sxs-lookup"><span data-stu-id="9776b-137">Delete an IP filter rule</span></span>

<span data-ttu-id="9776b-138">toodelete une règle de filtre IP, sélectionnez une ou plusieurs règles dans la grille de hello et cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="9776b-138">toodelete an IP filter rule, select one or more rules in hello grid and click **Delete**.</span></span>

![Supprimer une règle de filtre IP de l’IoT Hub][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="9776b-140">Évaluation de règle de filtre IP</span><span class="sxs-lookup"><span data-stu-id="9776b-140">IP filter rule evaluation</span></span>

<span data-ttu-id="9776b-141">Les règles de filtre IP sont appliquées dans l’ordre et hello première règle que correspondances hello adresse détermine hello accepter ou rejeter l’action.</span><span class="sxs-lookup"><span data-stu-id="9776b-141">IP filter rules are applied in order and hello first rule that matches hello IP address determines hello accept or reject action.</span></span>

<span data-ttu-id="9776b-142">Par exemple, si vous voulez les adresses tooaccept hello plage 192.168.100.0/22 rejetez tout le reste, hello première règle de grille de hello doit accepter hello adresse plage 192.168.100.0/22.</span><span class="sxs-lookup"><span data-stu-id="9776b-142">For example, if you want tooaccept addresses in hello range 192.168.100.0/22 and reject everything else, hello first rule in hello grid should accept hello address range 192.168.100.0/22.</span></span> <span data-ttu-id="9776b-143">règle de Hello suivante doit rejeter toutes les adresses à l’aide de 0.0.0.0/0 de la plage hello.</span><span class="sxs-lookup"><span data-stu-id="9776b-143">hello next rule should reject all addresses by using hello range 0.0.0.0/0.</span></span>

<span data-ttu-id="9776b-144">Vous pouvez modifier l’ordre hello de vos règles de filtre IP dans la grille de hello en cliquant sur trois points verticaux hello au début de hello d’une ligne par glisser- déposer.</span><span class="sxs-lookup"><span data-stu-id="9776b-144">You can change hello order of your IP filter rules in hello grid by clicking hello three vertical dots at hello start of a row and using drag and drop.</span></span>

<span data-ttu-id="9776b-145">votre nouvelle adresse IP de filtre toosave ordre des règles, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9776b-145">toosave your new IP filter rule order, click **Save**.</span></span>

![Modifier l’ordre de vos règles de filtre IP du Hub IoT hello][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="9776b-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9776b-147">Next steps</span></span>

<span data-ttu-id="9776b-148">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="9776b-148">toofurther explore hello capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="9776b-149">[Surveillance des opérations][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="9776b-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="9776b-150">[Métriques d’IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="9776b-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Azure Expressroute]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md