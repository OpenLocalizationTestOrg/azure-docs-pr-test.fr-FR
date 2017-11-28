---
title: aaaUse hello toocreate portail Azure un IoT Hub | Documents Microsoft
description: "Comment toocreate, gérer et supprimer des hubs Azure IoT via hello portail Azure. Inclut des informations sur les niveaux de tarification, l’évolutivité, la sécurité et la configuration de la messagerie."
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
ms.openlocfilehash: 383968c90ee7ef3bff85a6c90efbf5f0e8fbb208
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-azure-portal"></a><span data-ttu-id="5a3fa-104">Créez un IoT hub à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="5a3fa-104">Create an IoT hub using hello Azure portal</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="5a3fa-105">Cet article explique :</span><span class="sxs-lookup"><span data-stu-id="5a3fa-105">This article describes:</span></span>

* <span data-ttu-id="5a3fa-106">Comment toofind hello service IoT Hub Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-106">How toofind hello IoT Hub service in hello Azure portal.</span></span>
* <span data-ttu-id="5a3fa-107">Comment toocreate et gérer les IoT hubs.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-107">How toocreate and manage IoT hubs.</span></span>

## <a name="where-toofind-hello-iot-hub-service"></a><span data-ttu-id="5a3fa-108">Où toofind hello IoT Hub service</span><span class="sxs-lookup"><span data-stu-id="5a3fa-108">Where toofind hello IoT Hub service</span></span>

<span data-ttu-id="5a3fa-109">Vous pouvez trouver hello IoT Hub service Bonjour emplacements dans le portail de hello suivants :</span><span class="sxs-lookup"><span data-stu-id="5a3fa-109">You can find hello IoT Hub service in hello following locations in hello portal:</span></span>

* <span data-ttu-id="5a3fa-110">Choisissez **+ Nouveau**, puis **Internet des objets**.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-110">Choose **+ New**, then choose **Internet of Things**.</span></span>
* <span data-ttu-id="5a3fa-111">Bonjour Marketplace, choisissez **Internet of Things**.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-111">In hello Marketplace, choose **Internet of Things**.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="5a3fa-112">Créer un hub IoT</span><span class="sxs-lookup"><span data-stu-id="5a3fa-112">Create an IoT hub</span></span>

<span data-ttu-id="5a3fa-113">Vous pouvez créer un IoT hub à l’aide de hello méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="5a3fa-113">You can create an IoT hub using hello following methods:</span></span>

* <span data-ttu-id="5a3fa-114">Hello **+ nouveau** option ouvre le panneau de hello illustré hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-114">hello **+ New** option opens hello blade shown in hello following screen shot.</span></span> <span data-ttu-id="5a3fa-115">étapes Hello pour la création de hub IoT de hello via cette méthode et marketplace de hello sont identiques.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-115">hello steps for creating hello IoT hub through this method and through hello marketplace are identical.</span></span>
* <span data-ttu-id="5a3fa-116">Bonjour Marketplace, choisissez **créer** Panneau de hello tooopen illustré hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-116">In hello Marketplace, choose **Create** tooopen hello blade shown in hello following screen shot.</span></span>

<span data-ttu-id="5a3fa-117">Hello sections suivantes décrivent des hello plusieurs étapes toocreate un IoT hub :</span><span class="sxs-lookup"><span data-stu-id="5a3fa-117">hello following sections describe hello several steps toocreate an IoT hub:</span></span>

### <a name="choose-hello-name-of-hello-iot-hub"></a><span data-ttu-id="5a3fa-118">Choisissez le nom hello de hub IoT de hello</span><span class="sxs-lookup"><span data-stu-id="5a3fa-118">Choose hello name of hello IoT hub</span></span>

<span data-ttu-id="5a3fa-119">toocreate un hub IoT, vous devez nommer hub IoT de hello.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-119">toocreate an IoT hub, you must name hello IoT hub.</span></span> <span data-ttu-id="5a3fa-120">Le nom doit être unique parmi tous les hubs IoT.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-120">This name must be unique across all IoT hubs.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

### <a name="choose-hello-pricing-tier"></a><span data-ttu-id="5a3fa-121">Choisissez hello niveau tarifaire</span><span class="sxs-lookup"><span data-stu-id="5a3fa-121">Choose hello pricing tier</span></span>

<span data-ttu-id="5a3fa-122">Vous pouvez choisir entre quatre niveaux : **Gratuit**, **Standard S1**, **Standard S2** et**Standard S3**.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-122">You can choose from four tiers: **Free**, **Standard 1** and **Standard 2**, and **Standard S3**.</span></span> <span data-ttu-id="5a3fa-123">gratuit Hello permet uniquement de 500 périphériques toobe connecté toohello IoT hub et too8, 000 messages par jour.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-123">hello free tier allows only 500 devices toobe connected toohello IoT hub and up too8,000 messages per day.</span></span>

<span data-ttu-id="5a3fa-124">**Standard S1**: édition de hello S1 d’utilisation pour les solutions IoT avec un grand nombre de périphériques que chaque générer de petites quantités de données.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-124">**Standard S1**: Use hello S1 edition for IoT solutions with a large number of devices that each generate small amounts of data.</span></span> <span data-ttu-id="5a3fa-125">Chaque unité de l’édition de hello S1 permet des too400, 000 messages par jour sur tous les périphériques connectés.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-125">Each unit of hello S1 edition allows up too400,000 messages per day across all connected devices.</span></span>

<span data-ttu-id="5a3fa-126">**Standard S2**: édition de hello S2 d’utilisation pour les solutions IoT dans lequel les appareils générer de grandes quantités de données.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-126">**Standard S2**: Use hello S2 edition for IoT solutions in which devices generate large amounts of data.</span></span> <span data-ttu-id="5a3fa-127">Chaque unité de l’édition de S2 hello permet des too6 millions de messages par jour entre tous les périphériques connectés.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-127">Each unit of hello S2 edition allows up too6 million messages per day between all connected devices.</span></span>

<span data-ttu-id="5a3fa-128">**Standard S3**: édition de hello S3 d’utilisation pour les solutions IoT qui génèrent de grandes quantités de données.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-128">**Standard S3**: Use hello S3 edition for IoT solutions that generate large amounts of data.</span></span> <span data-ttu-id="5a3fa-129">Chaque unité de l’édition de S3 hello permet des too300 millions de messages par jour entre tous les périphériques connectés.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-129">Each unit of hello S3 edition allows up too300 million messages per day between all connected devices.</span></span>

![][4]

> [!NOTE]
> <span data-ttu-id="5a3fa-130">IoT Hub ne permet qu’un hub gratuit par abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-130">IoT Hub only allows one free hub per Azure subscription.</span></span>

### <a name="iot-hub-units"></a><span data-ttu-id="5a3fa-131">Unités de hub IoT</span><span class="sxs-lookup"><span data-stu-id="5a3fa-131">IoT hub units</span></span>

<span data-ttu-id="5a3fa-132">nombre de Hello de messages autorisés par unité par jour dépend de la tarification de votre concentrateur.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-132">hello number of messages allowed per unit per day depends on your hub's pricing tier.</span></span> <span data-ttu-id="5a3fa-133">Par exemple, si vous souhaitez hello en entrée toosupport de hub IoT de 700 000 messages, vous choisissez deux unités de couche S1.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-133">For example, if you want hello IoT hub toosupport ingress of 700,000 messages, you choose two S1 tier units.</span></span>

### <a name="device-toocloud-partitions-and-resource-group"></a><span data-ttu-id="5a3fa-134">Partitions de toocloud de périphérique et le groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="5a3fa-134">Device toocloud partitions and resource group</span></span>

<span data-ttu-id="5a3fa-135">Vous pouvez modifier le nombre de hello de partitions pour un hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-135">You can change hello number of partitions for an IoT hub.</span></span> <span data-ttu-id="5a3fa-136">nombre de partitions par défaut de Hello est 4, vous pouvez choisir un nombre différent à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-136">hello default number of partitions is 4, you can choose a different number from hello drop-down list.</span></span>

<span data-ttu-id="5a3fa-137">Vous n’avez pas besoin tooexplicitly créer un groupe de ressources vide.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-137">You do not need tooexplicitly create an empty resource group.</span></span> <span data-ttu-id="5a3fa-138">Lorsque vous créez une ressource, vous pouvez choisir soit toocreate une nouvelle, ou utiliser un groupe de ressources existant.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-138">When you create a resource, you can choose either toocreate a new, or use an existing resource group.</span></span>

![][5]

### <a name="choose-subscription"></a><span data-ttu-id="5a3fa-139">Choisir un abonnement</span><span class="sxs-lookup"><span data-stu-id="5a3fa-139">Choose subscription</span></span>

<span data-ttu-id="5a3fa-140">IoT Hub Azure automatiquement hello de listes de compte d’utilisateur des abonnements Azure hello est lié.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-140">Azure IoT Hub automatically lists hello Azure subscriptions hello user account is linked to.</span></span> <span data-ttu-id="5a3fa-141">Vous pouvez choisir hello abonnement Azure tooassociate hello IoT hub pour.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-141">You can choose hello Azure subscription tooassociate hello IoT hub to.</span></span>

### <a name="choose-hello-location"></a><span data-ttu-id="5a3fa-142">Choisissez l’emplacement de hello</span><span class="sxs-lookup"><span data-stu-id="5a3fa-142">Choose hello location</span></span>

<span data-ttu-id="5a3fa-143">option d’emplacement Hello fournit une liste des régions hello où IoT Hub n’est disponible.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-143">hello location option provides a list of hello regions where IoT Hub is available.</span></span>

### <a name="create-hello-iot-hub"></a><span data-ttu-id="5a3fa-144">Créez hello IoT hub</span><span class="sxs-lookup"><span data-stu-id="5a3fa-144">Create hello IoT hub</span></span>

<span data-ttu-id="5a3fa-145">Une fois toutes les étapes précédentes terminées, vous pouvez créez hello IoT hub.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-145">When all previous steps are complete, you can create hello IoT hub.</span></span> <span data-ttu-id="5a3fa-146">Cliquez sur **créer** toostart hello principaux processus toocreate et déployer hello IoT hub avec options hello choisis.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-146">Click **Create** toostart hello back-end process toocreate and deploy hello IoT hub with hello options you chose.</span></span>

<span data-ttu-id="5a3fa-147">IoT hub de quelques minutes toocreate hello peut prendre comme le temps requis pour hello principal déploiement toorun sur des serveurs hello emplacement approprié.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-147">It can take a few minutes toocreate hello IoT hub as it takes time for hello back-end deployment toorun on hello appropriate location servers.</span></span>

## <a name="change-hello-settings-of-hello-iot-hub"></a><span data-ttu-id="5a3fa-148">Modifier les paramètres de hello de hub IoT de hello</span><span class="sxs-lookup"><span data-stu-id="5a3fa-148">Change hello settings of hello IoT hub</span></span>

<span data-ttu-id="5a3fa-149">Vous pouvez modifier les paramètres de hello d’un hub IoT existant après sa création à partir de hello Panneau de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-149">You can change hello settings of an existing IoT hub after it is created from hello IoT Hub blade.</span></span>

![][8]

<span data-ttu-id="5a3fa-150">**Stratégies d’accès partagé**: ces stratégies définissent des autorisations de hello pour les appareils et services tooconnect tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-150">**Shared access policies**: These policies define hello permissions for devices and services tooconnect tooIoT Hub.</span></span> <span data-ttu-id="5a3fa-151">Vous pouvez accéder à ces stratégies en cliquant sur **Stratégies d’accès partagé** sous **Général**.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-151">You can access these policies by clicking **Shared access policies** under **General**.</span></span> <span data-ttu-id="5a3fa-152">Dans ce panneau, vous pouvez soit modifier les stratégies existantes, soit ajouter une nouvelle stratégie.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-152">In this blade, you can either modify existing policies or add a new policy.</span></span>

### <a name="create-a-policy"></a><span data-ttu-id="5a3fa-153">Création d’une stratégie</span><span class="sxs-lookup"><span data-stu-id="5a3fa-153">Create a policy</span></span>

* <span data-ttu-id="5a3fa-154">Cliquez sur **ajouter** tooopen un panneau.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-154">Click **Add** tooopen a blade.</span></span> <span data-ttu-id="5a3fa-155">Ici vous pouvez entrer le nom de la nouvelle stratégie hello et autorisations hello que vous souhaitez tooassociate avec cette stratégie, comme indiqué dans les éléments suivants de hello figure :</span><span class="sxs-lookup"><span data-stu-id="5a3fa-155">Here you can enter hello new policy name and hello permissions that you want tooassociate with this policy, as shown in hello following figure:</span></span>

    <span data-ttu-id="5a3fa-156">Il existe plusieurs autorisations qui peuvent être associées à ces stratégies partagées.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-156">There are several permissions that can be associated with these shared policies.</span></span> <span data-ttu-id="5a3fa-157">Hello **lecture du Registre** et **de Registre** accordent des stratégies en lecture et Registre des identités de toohello droits accès en écriture.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-157">hello **Registry read** and **Registry write** policies grant read and write access rights toohello identity registry.</span></span> <span data-ttu-id="5a3fa-158">Choix d’option d’écriture hello automatiquement choisit hello lire les options.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-158">Choosing hello write option automatically chooses hello read option.</span></span>

    <span data-ttu-id="5a3fa-159">Hello **Service de se connecter** stratégie accorde l’autorisation tooaccess points de terminaison de service telles que **réception appareil-à-cloud**.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-159">hello **Service connect** policy grants permission tooaccess service endpoints such as **Receive device-to-cloud**.</span></span> <span data-ttu-id="5a3fa-160">Hello **connexion de périphérique** stratégie accorde des autorisations pour envoyer et recevoir des messages à l’aide de points de terminaison hello IoT Hub côté appareil.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-160">hello **Device connect** policy grants permissions for sending and receiving messages using hello IoT Hub device-side endpoints.</span></span>

* <span data-ttu-id="5a3fa-161">Cliquez sur **créer** tooadd nouvellement créé la liste de stratégie toohello existante.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-161">Click **Create** tooadd this newly created policy toohello existing list.</span></span>

![][10]

## <a name="endpoints"></a><span data-ttu-id="5a3fa-162">Points de terminaison</span><span class="sxs-lookup"><span data-stu-id="5a3fa-162">Endpoints</span></span>

<span data-ttu-id="5a3fa-163">Cliquez sur **points de terminaison** toodisplay une liste de points de terminaison de hub IoT hello que vous souhaitez modifier.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-163">Click **Endpoints** toodisplay a list of endpoints for hello IoT hub that you are modifying.</span></span> <span data-ttu-id="5a3fa-164">Il existe deux types de points de terminaison : points de terminaison qui sont intégrées à un hub IoT de hello et que vous ajoutez toohello IoT hub après sa création.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-164">There are two types of endpoints: endpoints that are built into hello IoT hub, and endpoints that you add toohello IoT hub after its creation.</span></span>

![][11]

### <a name="built-in-endpoints"></a><span data-ttu-id="5a3fa-165">Points de terminaison intégrés</span><span class="sxs-lookup"><span data-stu-id="5a3fa-165">Built-in endpoints</span></span>

<span data-ttu-id="5a3fa-166">Il existe deux points de terminaison intégrés : **Cloud toodevice commentaires** et **événements**.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-166">There are two built-in endpoints: **Cloud toodevice feedback** and **Events**.</span></span>

* <span data-ttu-id="5a3fa-167">**Cloud toodevice commentaires** paramètres : ce paramètre n’a deux sous-Paramètres : **Cloud tooDevice TTL** (time-to-live) et **durée de rétention** (en heures) pour les messages de type hello.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-167">**Cloud toodevice feedback** settings: This setting has two subsettings: **Cloud tooDevice TTL** (time-to-live) and **Retention time** (in hours) for hello messages.</span></span> <span data-ttu-id="5a3fa-168">Lorsque votre premier créez un IoT hub, ces deux paramètres ont par défaut hello d’une heure.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-168">When your first create an IoT hub, both these settings have hello default value of one hour.</span></span> <span data-ttu-id="5a3fa-169">tooadjust ces paramètres, utilisez les curseurs hello ou tapez les valeurs hello.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-169">tooadjust these settings, use hello sliders or type hello values.</span></span>
* <span data-ttu-id="5a3fa-170">Paramètres **Événements** : ils présentent plusieurs configurations secondaires, qui sont pour certaines en lecture seule.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-170">**Events** settings: This setting has several subsettings, some of which are read-only.</span></span> <span data-ttu-id="5a3fa-171">Hello suivant liste décrit ces paramètres :</span><span class="sxs-lookup"><span data-stu-id="5a3fa-171">hello following list describes these settings:</span></span>

  * <span data-ttu-id="5a3fa-172">**Partitions**: une valeur par défaut est définie lorsque hello IoT hub est créé.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-172">**Partitions**: A default value is set when hello IoT hub is created.</span></span> <span data-ttu-id="5a3fa-173">Vous pouvez modifier le nombre de hello de partitions avec ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-173">You can change hello number of partitions through this setting.</span></span>

  * <span data-ttu-id="5a3fa-174">**Nom de Hub compatible avec l’événement et le point de terminaison**: lorsque hello IoT concentrateur est créé, un concentrateur d’événements est créé en interne que vous pouvez peut-être accéder à toounder certaines circonstances.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-174">**Event Hub-compatible name and endpoint**: When hello IoT hub is created, an Event Hub is created internally that you may need access toounder certain circumstances.</span></span> <span data-ttu-id="5a3fa-175">Vous ne pouvez pas personnaliser les valeurs nom et le point de terminaison hello compatible concentrateur d’événements, mais vous pouvez les copier en cliquant sur **copie**.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-175">You cannot customize hello Event Hub-compatible name and endpoint values but you can copy them by clicking **Copy**.</span></span>

  * <span data-ttu-id="5a3fa-176">**Durée de rétention**: tooone jour la valeur par défaut mais vous pouvez modifier à l’aide de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-176">**Retention Time**: Set tooone day by default but you can change it using hello drop-down list.</span></span> <span data-ttu-id="5a3fa-177">Cette valeur est en jours pour le paramètre de périphérique dans le cloud hello.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-177">This value is in days for hello device-to-cloud setting.</span></span>

  * <span data-ttu-id="5a3fa-178">**Groupes de consommateurs**: groupes de consommateurs activer plusieurs messages tooread de lecteurs indépendamment de hub IoT de hello.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-178">**Consumer Groups**: Consumer groups enable multiple readers tooread messages independently from hello IoT hub.</span></span> <span data-ttu-id="5a3fa-179">Chaque hub IoT est créé avec un groupe de consommateurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-179">Every IoT hub is created with a default consumer group.</span></span> <span data-ttu-id="5a3fa-180">Toutefois, vous pouvez ajouter ou supprimer des concentrateurs d’IoT tooyour groupes consommateur à l’aide de ce paramètre.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-180">However, you can add or delete consumer groups tooyour IoT hubs using this setting.</span></span>

  > [!NOTE]
  > <span data-ttu-id="5a3fa-181">groupe de consommateurs Hello par défaut ne peut pas être modifié ou supprimé.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-181">hello default consumer group cannot be edited or deleted.</span></span>

### <a name="custom-endpoints"></a><span data-ttu-id="5a3fa-182">Points de terminaison personnalisés</span><span class="sxs-lookup"><span data-stu-id="5a3fa-182">Custom endpoints</span></span>

<span data-ttu-id="5a3fa-183">Vous pouvez ajouter des points de terminaison personnalisés sur votre IoT hub à l’aide du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-183">You can add custom endpoints on your IoT hub using hello portal.</span></span> <span data-ttu-id="5a3fa-184">À partir de hello **points de terminaison** panneau, cliquez sur **ajouter** à Bonjour tooopen supérieur Bonjour **ajouter le point de terminaison** panneau.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-184">From hello **Endpoints** blade, click **Add** at hello top tooopen hello **Add endpoint** blade.</span></span> <span data-ttu-id="5a3fa-185">Entrez les informations de hello requis, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-185">Enter hello required information, then click **OK**.</span></span> <span data-ttu-id="5a3fa-186">Votre point de terminaison personnalisé est maintenant répertoriée dans hello principal **points de terminaison** panneau.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-186">Your custom endpoint is now listed in hello main **Endpoints** blade.</span></span>

![][13]

<span data-ttu-id="5a3fa-187">Pour en savoir plus sur les points de terminaison personnalisés, consultez [Référence - Points de terminaison IoT Hub][lnk-devguide-endpoints].</span><span class="sxs-lookup"><span data-stu-id="5a3fa-187">You can read more about custom endpoints in [Reference - IoT hub endpoints][lnk-devguide-endpoints].</span></span>

## <a name="routes"></a><span data-ttu-id="5a3fa-188">Itinéraires</span><span class="sxs-lookup"><span data-stu-id="5a3fa-188">Routes</span></span>

<span data-ttu-id="5a3fa-189">Cliquez sur **itinéraires** toomanage comment IoT Hub distribue vos messages appareil-à-cloud.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-189">Click **Routes** toomanage how IoT Hub dispatches your device-to-cloud messages.</span></span>

![][14]

<span data-ttu-id="5a3fa-190">Vous pouvez ajouter le concentrateur de IoT itinéraires tooyour en cliquant sur **ajouter** haut hello hello **itinéraires*** panneau, la saisie des informations de hello requis, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-190">You can add routes tooyour IoT hub by clicking **Add** at hello top of hello **Routes*** blade, entering hello required information, and clicking **OK**.</span></span> <span data-ttu-id="5a3fa-191">L’itinéraire est ensuite répertorié dans hello principal **itinéraires** panneau.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-191">Your route is then listed in hello main **Routes** blade.</span></span> <span data-ttu-id="5a3fa-192">Vous pouvez modifier un itinéraire en cliquant dessus dans la liste hello des itinéraires.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-192">You can edit a route by clicking it in hello list of routes.</span></span> <span data-ttu-id="5a3fa-193">tooenable un itinéraire, cliquez dessus dans la liste hello des itinéraires et définir hello **activé** basculer trop**hors**.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-193">tooenable a route, click it in hello list of routes and set hello **Enabled** toggle too**Off**.</span></span> <span data-ttu-id="5a3fa-194">modification de hello toosave, cliquez sur **OK** bas hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-194">toosave hello change, click **OK** at hello bottom of hello blade.</span></span>

![][15]

## <a name="pricing-and-scale"></a><span data-ttu-id="5a3fa-195">Tarification et mise à l'échelle</span><span class="sxs-lookup"><span data-stu-id="5a3fa-195">Pricing and scale</span></span>

<span data-ttu-id="5a3fa-196">Hello tarification d’un hub IoT existant peut être modifiée via hello **tarification** paramètres, par hello suivant des exceptions :</span><span class="sxs-lookup"><span data-stu-id="5a3fa-196">hello pricing of an existing IoT hub can be changed through hello **Pricing** settings, with hello following exceptions:</span></span>

* <span data-ttu-id="5a3fa-197">Dans l’implémentation actuelle de hello, un IoT hub avec une référence SKU libre ne peut pas modifier tooone niveaux de hello payé références (SKU), ou vice versa.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-197">In hello current implementation, an IoT hub with a free SKU cannot change tiers tooone of hello paid SKUs, or vice versa.</span></span>
* <span data-ttu-id="5a3fa-198">Il ne doit contenir qu’un seul hub IoT de niveau gratuit hello abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-198">There can only be one free tier IoT hub in hello Azure subscription.</span></span>

![][12]

<span data-ttu-id="5a3fa-199">Vous pouvez déplacer à partir d’un niveau supérieur de toolower uniquement lorsque le nombre hello de messages envoyés dans la journée dépasse le quota hello pour le niveau inférieur de hello.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-199">You can move from a higher toolower tier only when hello number of messages sent that day do exceed hello quota for hello lower tier.</span></span> <span data-ttu-id="5a3fa-200">Par exemple, si nombre hello de messages par jour dépasse 400 000, puis hello couche pour hello IoT hub peut être modifié.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-200">For example, if hello number of messages per day exceeds 400,000, then hello tier for hello IoT hub can be changed.</span></span> <span data-ttu-id="5a3fa-201">Toutefois, si vous modifiez le niveau de S1 toohello hub IoT de hello est limitée pour ce jour.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-201">However, if you change toohello S1 tier then hello IoT hub is throttled for that day.</span></span>

## <a name="delete-hello-iot-hub"></a><span data-ttu-id="5a3fa-202">Supprimer le hello IoT hub</span><span class="sxs-lookup"><span data-stu-id="5a3fa-202">Delete hello IoT hub</span></span>

<span data-ttu-id="5a3fa-203">Vous pouvez parcourir toohello IoT hub souhaité en cliquant sur toodelete **Parcourir**, et puis en choisissant hello toodelete de concentrateur approprié.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-203">You can browse toohello IoT hub you want toodelete by clicking **Browse**, and then choosing hello appropriate hub toodelete.</span></span> <span data-ttu-id="5a3fa-204">toodelete hello IoT hub, cliquez sur hello **supprimer** situé sous le nom de hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="5a3fa-204">toodelete hello IoT hub, click hello **Delete** button below hello IoT hub name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a3fa-205">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5a3fa-205">Next steps</span></span>

<span data-ttu-id="5a3fa-206">Suivez ces liens de toolearn plus d’informations sur la gestion de Azure IoT Hub :</span><span class="sxs-lookup"><span data-stu-id="5a3fa-206">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="5a3fa-207">[Gérer en bloc des appareils IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="5a3fa-207">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="5a3fa-208">[Métriques d’IoT Hub][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="5a3fa-208">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="5a3fa-209">[Surveillance des opérations][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="5a3fa-209">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="5a3fa-210">toofurther Explorez les fonctionnalités de hello d’IoT Hub, consultez :</span><span class="sxs-lookup"><span data-stu-id="5a3fa-210">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="5a3fa-211">[Guide du développeur IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="5a3fa-211">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="5a3fa-212">[Simulation d’un appareil avec IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="5a3fa-212">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="5a3fa-213">[Sécuriser votre solution IoT hello d’arrière-plan][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="5a3fa-213">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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
