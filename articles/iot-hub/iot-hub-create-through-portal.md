---
title: "Utiliser le portail Azure pour créer un IoT Hub | Microsoft Azure"
description: "Comment créer, gérer et supprimer des IoT Hubs Azure via le portail Azure. Inclut des informations sur les niveaux de tarification, l’évolutivité, la sécurité et la configuration de la messagerie."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0909cd2b-4c1e-49e0-b68a-75532caf0a6a
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: bca7eea5f44bbed3b784b56edaac235161b43e5e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-iot-hub-using-the-azure-portal"></a><span data-ttu-id="5e529-104">Création d’un IoT Hub à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="5e529-104">Create an IoT hub using the Azure portal</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="5e529-105">Cet article aborde les points suivants :</span><span class="sxs-lookup"><span data-stu-id="5e529-105">This article describes:</span></span>

* <span data-ttu-id="5e529-106">Comment trouver le service IoT Hub dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5e529-106">How to find the IoT Hub service in the Azure portal.</span></span>
* <span data-ttu-id="5e529-107">Comment créer et gérer des hubs IoT.</span><span class="sxs-lookup"><span data-stu-id="5e529-107">How to create and manage IoT hubs.</span></span>

## <a name="where-to-find-the-iot-hub-service"></a><span data-ttu-id="5e529-108">Où trouver le service IoT Hub</span><span class="sxs-lookup"><span data-stu-id="5e529-108">Where to find the IoT Hub service</span></span>

<span data-ttu-id="5e529-109">Vous pouvez trouver le service IoT Hub aux emplacements suivants sur le portail :</span><span class="sxs-lookup"><span data-stu-id="5e529-109">You can find the IoT Hub service in the following locations in the portal:</span></span>

* <span data-ttu-id="5e529-110">Choisissez **+ Nouveau**, puis **Internet des objets**.</span><span class="sxs-lookup"><span data-stu-id="5e529-110">Choose **+ New**, then choose **Internet of Things**.</span></span>
* <span data-ttu-id="5e529-111">Sur le marketplace, choisissez **Internet des objets**.</span><span class="sxs-lookup"><span data-stu-id="5e529-111">In the Marketplace, choose **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="5e529-112">Créer un hub IoT</span><span class="sxs-lookup"><span data-stu-id="5e529-112">Create an IoT hub</span></span>

<span data-ttu-id="5e529-113">Vous pouvez créer un hub IoT à l'aide des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5e529-113">You can create an IoT hub using the following methods:</span></span>

* <span data-ttu-id="5e529-114">L’option **+ Nouveau** ouvre le panneau indiqué dans la capture d’écran suivante.</span><span class="sxs-lookup"><span data-stu-id="5e529-114">The **+ New** option opens the blade shown in the following screen shot.</span></span> <span data-ttu-id="5e529-115">Les étapes de création du hub IoT via cette méthode et via le marketplace sont identiques.</span><span class="sxs-lookup"><span data-stu-id="5e529-115">The steps for creating the IoT hub through this method and through the marketplace are identical.</span></span>
* <span data-ttu-id="5e529-116">Sur le marketplace, choisissez **Créer** pour ouvrir le panneau indiqué dans la capture d’écran suivante.</span><span class="sxs-lookup"><span data-stu-id="5e529-116">In the Marketplace, choose **Create** to open the blade shown in the following screen shot.</span></span>

<span data-ttu-id="5e529-117">Les sections suivantes décrivent les différentes étapes permettant de créer un hub IoT :</span><span class="sxs-lookup"><span data-stu-id="5e529-117">The following sections describe the several steps to create an IoT hub:</span></span>

### <a name="choose-the-name-of-the-iot-hub"></a><span data-ttu-id="5e529-118">Choisir le nom du hub IoT</span><span class="sxs-lookup"><span data-stu-id="5e529-118">Choose the name of the IoT hub</span></span>

<span data-ttu-id="5e529-119">Pour créer un IoT Hub, vous devez le nommer.</span><span class="sxs-lookup"><span data-stu-id="5e529-119">To create an IoT hub, you must name the IoT hub.</span></span> <span data-ttu-id="5e529-120">Le nom doit être unique parmi tous les hubs IoT.</span><span class="sxs-lookup"><span data-stu-id="5e529-120">This name must be unique across all IoT hubs.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-the-pricing-tier"></a><span data-ttu-id="5e529-121">Choisir le niveau tarifaire.</span><span class="sxs-lookup"><span data-stu-id="5e529-121">Choose the pricing tier</span></span>

<span data-ttu-id="5e529-122">Vous pouvez choisir entre quatre niveaux : **Gratuit**, **Standard S1**, **Standard S2** et**Standard S3**.</span><span class="sxs-lookup"><span data-stu-id="5e529-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="5e529-123">Le niveau gratuit permet la connexion de seulement 500 appareils au IoT Hub, avec jusqu’à 8 000 messages par jour.</span><span class="sxs-lookup"><span data-stu-id="5e529-123">The free tier allows only 500 devices to be connected to the IoT hub and up to 8,000 messages per day.</span></span>

<span data-ttu-id="5e529-124">**Standard S1** : utilisez l’édition S1 pour les solutions IoT avec un grand nombre d’appareils qui génèrent chacun de petites quantités de données.</span><span class="sxs-lookup"><span data-stu-id="5e529-124">**Standard S1**: Use the S1 edition for IoT solutions with a large number of devices that each generate small amounts of data.</span></span> <span data-ttu-id="5e529-125">Chaque unité de l’édition S1 permet de transmettre au maximum 400 000 messages par jour sur l’ensemble des appareils connectés.</span><span class="sxs-lookup"><span data-stu-id="5e529-125">Each unit of the S1 edition allows up to 400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="5e529-126">**Standard S2** : utilisez l’édition S2 pour les solutions IoT dans lesquelles les appareils génèrent de grandes quantités de données.</span><span class="sxs-lookup"><span data-stu-id="5e529-126">**Standard S2**: Use the S2 edition for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="5e529-127">Chaque unité de l’édition S2 permet de transmettre au maximum 6 millions de messages par jour sur l’ensemble des appareils connectés.</span><span class="sxs-lookup"><span data-stu-id="5e529-127">Each unit of the S2 edition allows up to 6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="5e529-128">**Standard S3** : utilisez l’édition S3 pour les solutions IoT qui génèrent de grandes quantités de données.</span><span class="sxs-lookup"><span data-stu-id="5e529-128">**Standard S3**: Use the S3 edition for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="5e529-129">Chaque unité de l’édition S3 permet de transmettre au maximum 300 millions de messages par jour sur l’ensemble des appareils connectés.</span><span class="sxs-lookup"><span data-stu-id="5e529-129">Each unit of the S3 edition allows up to 300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="5e529-130">IoT Hub ne permet qu’un hub gratuit par abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5e529-130">IoT Hub only allows one free hub per Azure subscription.</span></span>

### <a name="iot-hub-units"></a><span data-ttu-id="5e529-131">Unités de hub IoT</span><span class="sxs-lookup"><span data-stu-id="5e529-131">IoT hub units</span></span>

<span data-ttu-id="5e529-132">Le nombre de messages autorisés par unité par jour dépend du niveau de tarification de votre concentrateur.</span><span class="sxs-lookup"><span data-stu-id="5e529-132">The number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="5e529-133">Par exemple, si vous souhaitez qu’IoT Hub prenne en charge l’arrivée de 700 000 messages, vous choisissez deux unités de niveau S1.</span><span class="sxs-lookup"><span data-stu-id="5e529-133">For example, if you want the IoT hub to support ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-to-cloud-partitions-and-resource-group"></a><span data-ttu-id="5e529-134">Les partitions appareil-à-cloud et groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="5e529-134">Device to cloud partitions and resource group</span></span>

<span data-ttu-id="5e529-135">Vous pouvez modifier le nombre de partitions pour un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5e529-135">You can change the number of partitions for an IoT hub.</span></span> <span data-ttu-id="5e529-136">Le nombre de partitions par défaut est 4 ; vous pouvez choisir un nombre différent dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="5e529-136">The default number of partitions is 4, you can choose a different number from the drop-down list.</span></span>

<span data-ttu-id="5e529-137">Vous n’avez pas besoin de créer explicitement un groupe de ressources vide.</span><span class="sxs-lookup"><span data-stu-id="5e529-137">You do not need to explicitly create an empty resource group.</span></span> <span data-ttu-id="5e529-138">Lorsque vous créez une ressource, vous avez le choix entre créer un groupe de ressources ou utiliser un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="5e529-138">When you create a resource, you can choose either to create a new, or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscription"></a><span data-ttu-id="5e529-139">Choisir un abonnement</span><span class="sxs-lookup"><span data-stu-id="5e529-139">Choose subscription</span></span>

<span data-ttu-id="5e529-140">Azure IoT Hub montre automatiquement la liste des abonnements Azure auquel le compte utilisateur est lié.</span><span class="sxs-lookup"><span data-stu-id="5e529-140">Azure IoT Hub automatically lists the Azure subscriptions the user account is linked to.</span></span> <span data-ttu-id="5e529-141">Vous pouvez choisir l’abonnement Azure auquel associer le hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5e529-141">You can choose the Azure subscription to associate the IoT hub to.</span></span>

### <a name="choose-the-location"></a><span data-ttu-id="5e529-142">Choisir l’emplacement</span><span class="sxs-lookup"><span data-stu-id="5e529-142">Choose the location</span></span>

<span data-ttu-id="5e529-143">L’option d’emplacement fournit une liste des régions dans lesquelles IoT Hub est disponible.</span><span class="sxs-lookup"><span data-stu-id="5e529-143">The location option provides a list of the regions where IoT Hub is available.</span></span>

### <a name="create-the-iot-hub"></a><span data-ttu-id="5e529-144">Créer le hub IoT</span><span class="sxs-lookup"><span data-stu-id="5e529-144">Create the IoT hub</span></span>

<span data-ttu-id="5e529-145">Lorsque toutes les étapes précédentes sont terminées, vous pouvez créer le hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5e529-145">When all previous steps are complete, you can create the IoT hub.</span></span> <span data-ttu-id="5e529-146">Cliquez sur **Créer** pour démarrer le processus principal afin de créer et de déployer le hub IoT avec les options sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="5e529-146">Click **Create** to start the back-end process to create and deploy the IoT hub with the options you chose.</span></span>

<span data-ttu-id="5e529-147">La création du hub IoT peut prendre quelques minutes, car le déploiement principal doit s’effectuer sur les serveurs d’emplacement appropriés.</span><span class="sxs-lookup"><span data-stu-id="5e529-147">It can take a few minutes to create the IoT hub as it takes time for the back-end deployment to run on the appropriate location servers.</span></span>

## <a name="change-the-settings-of-the-iot-hub"></a><span data-ttu-id="5e529-148">Modifier les paramètres du hub IoT</span><span class="sxs-lookup"><span data-stu-id="5e529-148">Change the settings of the IoT hub</span></span>

<span data-ttu-id="5e529-149">Vous pouvez modifier les paramètres d’un hub IoT existant après sa création, dans le panneau IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5e529-149">You can change the settings of an existing IoT hub after it is created from the IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="5e529-150">**Stratégies d’accès partagé** : ces stratégies définissent les autorisations pour que les appareils et services se connectent au IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5e529-150">**Shared access policies**: These policies define the permissions for devices and services to connect to IoT Hub.</span></span> <span data-ttu-id="5e529-151">Vous pouvez accéder à ces stratégies en cliquant sur **Stratégies d’accès partagé** sous **Général**.</span><span class="sxs-lookup"><span data-stu-id="5e529-151">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="5e529-152">Dans ce panneau, vous pouvez soit modifier les stratégies existantes, soit ajouter une nouvelle stratégie.</span><span class="sxs-lookup"><span data-stu-id="5e529-152">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="5e529-153">Création d’une stratégie</span><span class="sxs-lookup"><span data-stu-id="5e529-153">Create a policy</span></span>

* <span data-ttu-id="5e529-154">Cliquez sur **Ajouter** pour ouvrir un panneau.</span><span class="sxs-lookup"><span data-stu-id="5e529-154">Click **Add** to open a blade.</span></span> <span data-ttu-id="5e529-155">Ici, vous pouvez ouvrir un panneau dans lequel vous pouvez saisir le nouveau nom de stratégie, et les autorisations que vous voulez associer à la stratégie, comme illustré dans la figure suivante :</span><span class="sxs-lookup"><span data-stu-id="5e529-155">Here you can enter the new policy name and the permissions that you want to associate with this policy, as shown in the following figure:</span></span>

    <span data-ttu-id="5e529-156">Il existe plusieurs autorisations qui peuvent être associées à ces stratégies partagées.</span><span class="sxs-lookup"><span data-stu-id="5e529-156">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="5e529-157">Les stratégies **Lecture de registre** et **Écriture de registre** accordent les autorisations en lecture et en écriture au registre d’identité.</span><span class="sxs-lookup"><span data-stu-id="5e529-157">The **Registry read** and **Registry write** policies grant read and write access rights to the identity registry.</span></span> <span data-ttu-id="5e529-158">Le choix de l'option en écriture active automatiquement l'option en lecture.</span><span class="sxs-lookup"><span data-stu-id="5e529-158">Choosing the write option automatically chooses the read option.</span></span>

    <span data-ttu-id="5e529-159">La stratégie de **connexion de service** autorise l’accès aux points de terminaison de service tels que la **réception appareil-à-cloud**.</span><span class="sxs-lookup"><span data-stu-id="5e529-159">The **Service connect** policy grants permission to access service endpoints such as **Receive device-to-cloud**.</span></span> <span data-ttu-id="5e529-160">La stratégie de **connexion d’appareil** accorde des autorisations pour envoyer et recevoir des messages à l’aide des points de terminaison côté appareil de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5e529-160">The **Device connect** policy grants permissions for sending and receiving messages using the IoT Hub device-side endpoints.</span></span>

* <span data-ttu-id="5e529-161">Cliquez sur **Créer** pour ajouter la stratégie créée à la liste existante.</span><span class="sxs-lookup"><span data-stu-id="5e529-161">Click **Create** to add this newly created policy to the existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="5e529-162">Endpoints</span><span class="sxs-lookup"><span data-stu-id="5e529-162">Endpoints</span></span>

<span data-ttu-id="5e529-163">Pour afficher la liste des points de terminaison associés à l’IoT Hub que vous essayez de modifier, cliquez sur **Points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="5e529-163">Click **Endpoints** to display a list of endpoints for the IoT hub that you are modifying.</span></span> <span data-ttu-id="5e529-164">Il existe deux types de points de terminaison : les points de terminaison intégrées à IoT Hub, et ceux que vous avez ajoutés à IoT Hub après sa création.</span><span class="sxs-lookup"><span data-stu-id="5e529-164">There are two types of endpoints: endpoints that are built into the IoT hub, and endpoints that you add to the IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="5e529-165">Points de terminaison intégrés</span><span class="sxs-lookup"><span data-stu-id="5e529-165">Built-in endpoints</span></span>

<span data-ttu-id="5e529-166">Il existe deux catégories de points de terminaison intégrés : les **commentaires de messages cloud-à-appareil** et les **événements**.</span><span class="sxs-lookup"><span data-stu-id="5e529-166">There are two built-in endpoints: **Cloud to device feedback** and **Events**.</span></span>

* <span data-ttu-id="5e529-167">Paramètres **Commentaire de messages cloud-à-appareil** : ce paramètre contient deux configurations secondaires : **Cloud vers appareil TTL** (durée de vie) et **Durée de rétention** (en heures) pour les messages.</span><span class="sxs-lookup"><span data-stu-id="5e529-167">**Cloud to device feedback** settings: This setting has two subsettings: **Cloud to Device TTL** (time-to-live) and **Retention time** (in hours) for the messages.</span></span> <span data-ttu-id="5e529-168">Lorsque vous créez une instance IoT Hub, ces deux paramètres sont paramétrés par défaut sur une heure.</span><span class="sxs-lookup"><span data-stu-id="5e529-168">When your first create an IoT hub, both these settings have the default value of one hour.</span></span> <span data-ttu-id="5e529-169">Pour les ajuster, utilisez les curseurs ou saisissez les valeurs de votre choix.</span><span class="sxs-lookup"><span data-stu-id="5e529-169">To adjust these settings, use the sliders or type the values.</span></span>
* <span data-ttu-id="5e529-170">Paramètres **Événements** : ils présentent plusieurs configurations secondaires, qui sont pour certaines en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="5e529-170">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="5e529-171">La liste ci-dessous décrit ces paramètres :</span><span class="sxs-lookup"><span data-stu-id="5e529-171">The following list describes these settings:</span></span>

  * <span data-ttu-id="5e529-172">**Partitions** : une valeur par défaut est définie lors de la création de l’instance IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5e529-172">**Partitions**: A default value is set when the IoT hub is created.</span></span> <span data-ttu-id="5e529-173">Vous pouvez ici modifier le nombre de partitions.</span><span class="sxs-lookup"><span data-stu-id="5e529-173">You can change the number of partitions through this setting.</span></span>

  * <span data-ttu-id="5e529-174">**Nom compatible et point de terminaison Concentrateur d'événements** : lorsque le concentrateur IoT est créé, un Concentrateur d'événements est créé en interne, et vous pouvez nécessiter l'accès dans certaines circonstances.</span><span class="sxs-lookup"><span data-stu-id="5e529-174">**Event Hub-compatible name and endpoint**: When the IoT hub is created, an Event Hub is created internally that you may need access to under certain circumstances.</span></span> <span data-ttu-id="5e529-175">S’il est impossible de personnaliser le nom compatible et les valeurs de points de terminaison du concentrateur d’événements, vous pouvez copier ces valeurs en cliquant sur **Copier**.</span><span class="sxs-lookup"><span data-stu-id="5e529-175">You cannot customize the Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

  * <span data-ttu-id="5e529-176">**Durée de rétention** : cette valeur est définie par défaut sur un jour, mais pouvez la modifier à l’aide de la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="5e529-176">**Retention Time**: Set to one day by default but you can change it using the drop-down list.</span></span> <span data-ttu-id="5e529-177">Cette valeur est exprimée en jours pour le paramètre d’appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="5e529-177">This value is in days for the device-to-cloud setting.</span></span>

  * <span data-ttu-id="5e529-178">**Groupes de consommateurs** : les groupes de consommateurs permettent à plusieurs lecteurs de lire les messages indépendamment à partir du hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5e529-178">**Consumer Groups**: Consumer groups enable multiple readers to read messages independently from the IoT hub.</span></span> <span data-ttu-id="5e529-179">Chaque hub IoT est créé avec un groupe de consommateurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="5e529-179">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="5e529-180">Toutefois, vous pouvez ajouter ou supprimer des groupes de consommateurs de vos instances IoT Hub via ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="5e529-180">However, you can add or delete consumer groups to your IoT hubs using this setting.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5e529-181">Le groupe de consommateurs par défaut ne peut être ni modifié ni supprimé.</span><span class="sxs-lookup"><span data-stu-id="5e529-181">The default consumer group cannot be edited or deleted.</span></span>

### <a name="custom-endpoints"></a><span data-ttu-id="5e529-182">Points de terminaison personnalisés</span><span class="sxs-lookup"><span data-stu-id="5e529-182">Custom endpoints</span></span>

<span data-ttu-id="5e529-183">Vous pouvez ajouter des points de terminaison personnalisés sur votre IoT Hub par le biais de ce portail.</span><span class="sxs-lookup"><span data-stu-id="5e529-183">You can add custom endpoints on your IoT hub using the portal.</span></span> <span data-ttu-id="5e529-184">En haut du panneau **Points de terminaison**, cliquez sur **Ajouter** afin d’ouvrir le panneau **Ajouter un point de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="5e529-184">From the **Endpoints** blade, click **Add** at the top to open the **Add endpoint** blade.</span></span> <span data-ttu-id="5e529-185">Saisissez les informations requises, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5e529-185">Enter the required information, then click **OK**.</span></span> <span data-ttu-id="5e529-186">Votre point de terminaison personnalisé est désormais répertorié dans le panneau principal **Points de terminaison**.</span><span class="sxs-lookup"><span data-stu-id="5e529-186">Your custom endpoint is now listed in the main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="5e529-187">Pour en savoir plus sur les points de terminaison personnalisés, consultez [Référence - Points de terminaison IoT Hub][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="5e529-187">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="5e529-188">Itinéraires</span><span class="sxs-lookup"><span data-stu-id="5e529-188">Routes</span></span>

<span data-ttu-id="5e529-189">Cliquez sur **Itinéraires** pour gérer la façon dont IoT Hub distribue vos messages cloud-à-appareil.</span><span class="sxs-lookup"><span data-stu-id="5e529-189">Click **Routes** to manage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="5e529-190">Pour ajouter des itinéraires à votre IoT Hub, cliquez sur **Ajouter** en haut du panneau **Itinéraires*** , saisissez les informations requises, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5e529-190">You can add routes to your IoT hub by clicking **Add** at the top of the **Routes*** blade, entering the required information, and clicking **OK**.</span></span> <span data-ttu-id="5e529-191">Dès lors, votre itinéraire est répertorié dans le panneau principal **Itinéraires**.</span><span class="sxs-lookup"><span data-stu-id="5e529-191">Your route is then listed in the main **Routes** blade.</span></span> <span data-ttu-id="5e529-192">Pour modifier un itinéraire, cliquez dessus dans la liste des itinéraires.</span><span class="sxs-lookup"><span data-stu-id="5e529-192">You can edit a route by clicking it in the list of routes.</span></span> <span data-ttu-id="5e529-193">Pour activer un itinéraire, cliquez dessus dans la liste des itinéraires, puis définissez le paramètre **Activer/Désactiver** sur **Désactiver**.</span><span class="sxs-lookup"><span data-stu-id="5e529-193">To enable a route, click it in the list of routes and set the **Enabled** toggle to **Off**.</span></span> <span data-ttu-id="5e529-194">Pour enregistrer la modification, cliquez sur **OK** en bas du panneau.</span><span class="sxs-lookup"><span data-stu-id="5e529-194">To save the change, click **OK** at the bottom of the blade.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="5e529-195">Tarification et mise à l'échelle</span><span class="sxs-lookup"><span data-stu-id="5e529-195">Pricing and scale</span></span>

<span data-ttu-id="5e529-196">La tarification d'un concentrateur IoT existant peut être modifiée via les paramètres de **tarification** avec les exceptions suivantes :</span><span class="sxs-lookup"><span data-stu-id="5e529-196">The pricing of an existing IoT hub can be changed through the **Pricing** settings, with the following exceptions:</span></span>

* <span data-ttu-id="5e529-197">Dans l’implémentation actuelle, un hub IoT avec une référence gratuite ne peut pas changer de niveau pour une référence payante, ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="5e529-197">In the current implementation, an IoT hub with a free SKU cannot change tiers to one of the paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="5e529-198">Il ne peut y avoir qu’un niveau gratuit de IoT Hub par abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5e529-198">There can only be one free tier IoT hub in the Azure subscription.</span></span>

![][12]

<span data-ttu-id="5e529-199">Vous ne pouvez changer de niveau que lorsque le nombre de messages envoyés dans la journée dépasse le quota défini pour le niveau inférieur.</span><span class="sxs-lookup"><span data-stu-id="5e529-199">You can move from a higher to lower tier only when the number of messages sent that day do exceed the quota for the lower tier.</span></span> <span data-ttu-id="5e529-200">Par exemple, si le nombre de messages par jour est supérieur à 400 000, le niveau correspondant au IoT Hub peut être modifié.</span><span class="sxs-lookup"><span data-stu-id="5e529-200">For example, if the number of messages per day exceeds 400,000, then the tier for the IoT hub can be changed.</span></span> <span data-ttu-id="5e529-201">En revanche, si vous modifiez le niveau S1, l’IoT Hub est limité pour ce jour.</span><span class="sxs-lookup"><span data-stu-id="5e529-201">However, if you change to the S1 tier then the IoT hub is throttled for that day.</span></span>

## <a name="delete-the-iot-hub"></a><span data-ttu-id="5e529-202">Supprimez IoT Hub</span><span class="sxs-lookup"><span data-stu-id="5e529-202">Delete the IoT hub</span></span>

<span data-ttu-id="5e529-203">Vous pouvez accéder au concentrateur IoT Hub en cliquant sur **Parcourir**, puis en choisissant le concentrateur à supprimer.</span><span class="sxs-lookup"><span data-stu-id="5e529-203">You can browse to the IoT hub you want to delete by clicking **Browse**, and then choosing the appropriate hub to delete.</span></span> <span data-ttu-id="5e529-204">Cliquez sur le bouton **Supprimer** situé sous le nom de l’IoT Hub pour supprimer celui-ci.</span><span class="sxs-lookup"><span data-stu-id="5e529-204">To delete the IoT hub, click the **Delete** button below the IoT hub name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e529-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5e529-205">Next steps</span></span>

<span data-ttu-id="5e529-206">Suivez ces liens pour en savoir plus sur la gestion de Azure IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="5e529-206">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="5e529-207">[Gérer en bloc des appareils IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="5e529-207">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="5e529-208">[Métriques d’IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="5e529-208">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="5e529-209">[Surveillance des opérations][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="5e529-209">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="5e529-210">Pour explorer davantage les capacités de IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="5e529-210">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="5e529-211">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="5e529-211">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="5e529-212">[Simulation d’un appareil avec IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="5e529-212">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="5e529-213">[Sécuriser votre solution IoT de bout en bout][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="5e529-213">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

[4]: ./media/iot-hub-create-through-portal/create-iothub.png
[5]: ./media/iot-hub-create-through-portal/location1.png
[8]: ./media/iot-hub-create-through-portal/portal-settings.png
[10]: ./media/iot-hub-create-through-portal/shared-access-policies.png
[11]: ./media/iot-hub-create-through-portal/messaging-settings.png
[12]: ./media/iot-hub-create-through-portal/pricing-error.png
[13]: ./media/iot-hub-create-through-portal/endpoint-creation.png
[14]: ./media/iot-hub-create-through-portal/routes-list.png
[15]: ./media/iot-hub-create-through-portal/route-edit.png

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
