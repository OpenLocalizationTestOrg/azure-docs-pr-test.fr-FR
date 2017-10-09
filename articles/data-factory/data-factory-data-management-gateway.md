---
title: "aaaData passerelle de gestion de fabrique de données | Documents Microsoft"
description: "Configurer une passerelle de données toomove des données entre locaux et hello cloud. Utiliser la passerelle de gestion des données dans Azure Data Factory toomove vos données."
services: data-factory
documentationcenter: 
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: b9084537-2e1c-4e96-b5bc-0e2044388ffd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
ms.openlocfilehash: 6f523891a6230cbc7b407f46f4b02d91dfd2cf46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-management-gateway"></a><span data-ttu-id="7d731-104">Passerelle de gestion de données</span><span class="sxs-lookup"><span data-stu-id="7d731-104">Data Management Gateway</span></span>
<span data-ttu-id="7d731-105">passerelle de gestion des données Hello est un agent de client que vous devez installer dans vos données de toocopy environnement local entre des magasins de données locaux et cloud.</span><span class="sxs-lookup"><span data-stu-id="7d731-105">hello Data management gateway is a client agent that you must install in your on-premises environment toocopy data between cloud and on-premises data stores.</span></span> <span data-ttu-id="7d731-106">Hello des données localement magasins pris en charge par la fabrique de données sont répertoriées dans hello [prise en charge des sources de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) section.</span><span class="sxs-lookup"><span data-stu-id="7d731-106">hello on-premises data stores supported by Data Factory are listed in hello [Supported data sources](data-factory-data-movement-activities.md#supported-data-stores-and-formats) section.</span></span>

<span data-ttu-id="7d731-107">Cet article vient s’ajouter aux procédure pas à pas de hello Bonjour [déplacement des données entre locaux et cloud banques de données](data-factory-move-data-between-onprem-and-cloud.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="7d731-107">This article complements hello walkthrough in hello [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="7d731-108">Hello procédure pas à pas, vous créez un pipeline qui utilise des données de toomove hello passerelle à partir d’un tooan de base de données SQL Server locale blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7d731-108">In hello walkthrough, you create a pipeline that uses hello gateway toomove data from an on-premises SQL Server database tooan Azure blob.</span></span> <span data-ttu-id="7d731-109">Cet article fournit des informations détaillées sur la passerelle de gestion des données hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-109">This article provides detailed in-depth information about hello data management gateway.</span></span> 

<span data-ttu-id="7d731-110">Vous pouvez faire évoluer une passerelle de gestion des données en associant plusieurs machines locales de la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-110">You can scale out a data management gateway by associating multiple on-premises machines with hello gateway.</span></span> <span data-ttu-id="7d731-111">Vous pouvez monter en puissance une passerelle en augmentant le nombre de travaux de déplacement des données qui peuvent s’exécuter simultanément sur un nœud.</span><span class="sxs-lookup"><span data-stu-id="7d731-111">You can scale up by increasing number of data movement jobs that can run concurrently on a node.</span></span> <span data-ttu-id="7d731-112">Cette fonctionnalité est également disponible pour une passerelle logique à nœud unique.</span><span class="sxs-lookup"><span data-stu-id="7d731-112">This feature is also available for a logical gateway with a single node.</span></span> <span data-ttu-id="7d731-113">Consultez l’article [Mise à l’échelle de la passerelle de gestion des données dans Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="7d731-113">See [Scaling data management gateway in Azure Data Factory](data-factory-data-management-gateway-high-availability-scalability.md) article for details.</span></span>

> [!NOTE]
> <span data-ttu-id="7d731-114">Actuellement, passerelle prend en charge uniquement l’activité de copie hello et l’activité de procédure stockée dans la fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="7d731-114">Currently, gateway supports only hello copy activity and stored procedure activity in Data Factory.</span></span> <span data-ttu-id="7d731-115">Il n’est pas passerelle de hello toouse possible à partir de sources de données sur site tooaccess activité personnalisée.</span><span class="sxs-lookup"><span data-stu-id="7d731-115">It is not possible toouse hello gateway from a custom activity tooaccess on-premises data sources.</span></span>      

## <a name="overview"></a><span data-ttu-id="7d731-116">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="7d731-116">Overview</span></span>
### <a name="capabilities-of-data-management-gateway"></a><span data-ttu-id="7d731-117">Fonctionnalités de la passerelle de gestion des données</span><span class="sxs-lookup"><span data-stu-id="7d731-117">Capabilities of data management gateway</span></span>
<span data-ttu-id="7d731-118">Passerelle de gestion des données fournit hello suivant de fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="7d731-118">Data management gateway provides hello following capabilities:</span></span>

* <span data-ttu-id="7d731-119">Modèle des sources de données sur site et les sources de données cloud dans hello même fabrique de données et déplacement des données.</span><span class="sxs-lookup"><span data-stu-id="7d731-119">Model on-premises data sources and cloud data sources within hello same data factory and move data.</span></span>
* <span data-ttu-id="7d731-120">Avoir un point unique pour la surveillance et la gestion avec visibilité sur l’état de la passerelle à partir de la page de Data Factory hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-120">Have a single pane of glass for monitoring and management with visibility into gateway status from hello Data Factory page.</span></span>
* <span data-ttu-id="7d731-121">Gérer les sources de données access tooon local en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="7d731-121">Manage access tooon-premises data sources securely.</span></span>
  * <span data-ttu-id="7d731-122">Aucune modification requise toocorporate pare-feu.</span><span class="sxs-lookup"><span data-stu-id="7d731-122">No changes required toocorporate firewall.</span></span> <span data-ttu-id="7d731-123">Passerelle effectue uniquement les connexions HTTP sortant tooopen internet.</span><span class="sxs-lookup"><span data-stu-id="7d731-123">Gateway only makes outbound HTTP-based connections tooopen internet.</span></span>
  * <span data-ttu-id="7d731-124">Chiffrement des informations d’identification pour vos magasins de données locaux à l’aide de votre certificat.</span><span class="sxs-lookup"><span data-stu-id="7d731-124">Encrypt credentials for your on-premises data stores with your certificate.</span></span>
* <span data-ttu-id="7d731-125">Déplacer efficacement des données : les données sont transférées en parallèle, résilients toointermittent des problèmes de réseau avec la logique de nouvelle tentative automatique.</span><span class="sxs-lookup"><span data-stu-id="7d731-125">Move data efficiently – data is transferred in parallel, resilient toointermittent network issues with auto retry logic.</span></span>

### <a name="command-flow-and-data-flow"></a><span data-ttu-id="7d731-126">Flux de commandes et flux de données</span><span class="sxs-lookup"><span data-stu-id="7d731-126">Command flow and data flow</span></span>
<span data-ttu-id="7d731-127">Lorsque vous utilisez un copier activité toocopy des données entre locaux et cloud, activité hello utilise un passerelle tootransfer de données à partir de toocloud de source de données locale et vice versa.</span><span class="sxs-lookup"><span data-stu-id="7d731-127">When you use a copy activity toocopy data between on-premises and cloud, hello activity uses a gateway tootransfer data from on-premises data source toocloud and vice versa.</span></span>

<span data-ttu-id="7d731-128">Voici hello des flux de données de haut niveau pour et un récapitulatif des étapes de la copie avec la passerelle de données : ![des flux de données à l’aide de la passerelle](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span><span class="sxs-lookup"><span data-stu-id="7d731-128">Here is hello high-level data flow for and summary of steps for copy with data gateway: ![Data flow using gateway](./media/data-factory-data-management-gateway/data-flow-using-gateway.png)</span></span>

1. <span data-ttu-id="7d731-129">Développeur de données crée une passerelle pour une fabrique de données Azure à l’aide soit hello [portail Azure](https://portal.azure.com) ou [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d731-129">Data developer creates a gateway for an Azure Data Factory using either hello [Azure portal](https://portal.azure.com) or [PowerShell Cmdlet](https://msdn.microsoft.com/library/dn820234.aspx).</span></span>
2. <span data-ttu-id="7d731-130">Développeur de données crée un service lié pour une banque de données locale en spécifiant la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-130">Data developer creates a linked service for an on-premises data store by specifying hello gateway.</span></span> <span data-ttu-id="7d731-131">Comme partie de la configuration de hello le service lié, développeur de données utilise les informations d’identification et les types d’authentification toospecify application hello informations d’identification du paramètre.</span><span class="sxs-lookup"><span data-stu-id="7d731-131">As part of setting up hello linked service, data developer uses hello Setting Credentials application toospecify authentication types and credentials.</span></span>  <span data-ttu-id="7d731-132">informations d’identification du paramètre Hello boîte de dialogue application communique avec les données de salutation stocker tootest connexion et hello toosave d’identification de passerelle.</span><span class="sxs-lookup"><span data-stu-id="7d731-132">hello Setting Credentials application dialog communicates with hello data store tootest connection and hello gateway toosave credentials.</span></span>
3. <span data-ttu-id="7d731-133">Passerelle chiffre les informations d’identification de l’hello avec certificat hello associé passerelle hello (fourni par le développeur de données), avant d’enregistrer les informations d’identification hello dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-133">Gateway encrypts hello credentials with hello certificate associated with hello gateway (supplied by data developer), before saving hello credentials in hello cloud.</span></span>
4. <span data-ttu-id="7d731-134">Service de fabrique de données communique avec la passerelle hello pour la planification et la gestion des travaux via un canal de contrôle qui utilise une file d’attente du bus de service Azure partagé.</span><span class="sxs-lookup"><span data-stu-id="7d731-134">Data Factory service communicates with hello gateway for scheduling & management of jobs via a control channel that uses a shared Azure service bus queue.</span></span> <span data-ttu-id="7d731-135">Lorsqu’un travail d’activité de copie doit toobe lancé, fabrique de données des files d’attente demande hello en même temps que les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="7d731-135">When a copy activity job needs toobe kicked off, Data Factory queues hello request along with credential information.</span></span> <span data-ttu-id="7d731-136">Passerelle démarre le travail de hello après interrogation file d’attente hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-136">Gateway kicks off hello job after polling hello queue.</span></span>
5. <span data-ttu-id="7d731-137">passerelle de Hello déchiffre des informations d’identification de hello avec hello même certificat et connecte ensuite banque de données locale toohello avec les informations d’identification et le type d’authentification approprié.</span><span class="sxs-lookup"><span data-stu-id="7d731-137">hello gateway decrypts hello credentials with hello same certificate and then connects toohello on-premises data store with proper authentication type and credentials.</span></span>
6. <span data-ttu-id="7d731-138">passerelle de Hello copie des données à partir d’un stockage en nuage tooa magasin local ou vice versa, selon la configuration dans le pipeline de données hello hello activité de copie.</span><span class="sxs-lookup"><span data-stu-id="7d731-138">hello gateway copies data from an on-premises store tooa cloud storage, or vice versa depending on how hello Copy Activity is configured in hello data pipeline.</span></span> <span data-ttu-id="7d731-139">Pour cette étape, la passerelle de hello communique directement avec les services de stockage cloud, tels que le stockage Blob Azure sur un un canal sécurisé (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="7d731-139">For this step, hello gateway directly communicates with cloud-based storage services such as Azure Blob Storage over a secure (HTTPS) channel.</span></span>

### <a name="considerations-for-using-gateway"></a><span data-ttu-id="7d731-140">Considérations relatives à l’utilisation de la passerelle</span><span class="sxs-lookup"><span data-stu-id="7d731-140">Considerations for using gateway</span></span>
* <span data-ttu-id="7d731-141">Une seule instance de passerelle de gestion des données peut être utilisée pour plusieurs sources de données locales.</span><span class="sxs-lookup"><span data-stu-id="7d731-141">A single instance of data management gateway can be used for multiple on-premises data sources.</span></span> <span data-ttu-id="7d731-142">Toutefois, **une seule instance de passerelle est une fabrique de données Azure liée tooonly** et ne peut pas être partagé avec un autre Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="7d731-142">However, **a single gateway instance is tied tooonly one Azure data factory** and cannot be shared with another data factory.</span></span>
* <span data-ttu-id="7d731-143">Vous ne pouvez installer qu’**une seule instance de la passerelle de gestion de données** sur un même ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7d731-143">You can have **only one instance of data management gateway** installed on a single machine.</span></span> <span data-ttu-id="7d731-144">Supposons que vous avez deux fabriques de données qui doivent tooaccess des sources de données locale, vous devez les passerelles tooinstall sur deux ordinateurs locaux.</span><span class="sxs-lookup"><span data-stu-id="7d731-144">Suppose, you have two data factories that need tooaccess on-premises data sources, you need tooinstall gateways on two on-premises computers.</span></span> <span data-ttu-id="7d731-145">En d’autres termes, une passerelle est la fabrique de données spécifiques tooa liée</span><span class="sxs-lookup"><span data-stu-id="7d731-145">In other words, a gateway is tied tooa specific data factory</span></span>
* <span data-ttu-id="7d731-146">Hello **passerelle n’a pas besoin toobe sur hello même ordinateur en tant que source de données hello**.</span><span class="sxs-lookup"><span data-stu-id="7d731-146">hello **gateway does not need toobe on hello same machine as hello data source**.</span></span> <span data-ttu-id="7d731-147">Toutefois, source de données toohello plus proche passerelle réduit la durée hello pour la source de données hello passerelle tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="7d731-147">However, having gateway closer toohello data source reduces hello time for hello gateway tooconnect toohello data source.</span></span> <span data-ttu-id="7d731-148">Nous vous recommandons d’installer la passerelle de hello sur un ordinateur différent de hello une source de données hôtes locaux.</span><span class="sxs-lookup"><span data-stu-id="7d731-148">We recommend that you install hello gateway on a machine that is different from hello one that hosts on-premises data source.</span></span> <span data-ttu-id="7d731-149">Lors de la source de données et de la passerelle hello sont sur des ordinateurs différents, passerelle de hello n’est pas en concurrence pour les ressources avec la source de données.</span><span class="sxs-lookup"><span data-stu-id="7d731-149">When hello gateway and data source are on different machines, hello gateway does not compete for resources with data source.</span></span>
* <span data-ttu-id="7d731-150">Vous pouvez avoir **plusieurs passerelles sur différents ordinateurs connexion toohello même source de données locale**.</span><span class="sxs-lookup"><span data-stu-id="7d731-150">You can have **multiple gateways on different machines connecting toohello same on-premises data source**.</span></span> <span data-ttu-id="7d731-151">Par exemple, peut avoir deux passerelles desservant les fabriques de deux données mais hello même source de données locale est enregistré avec les fabriques de données hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-151">For example, you may have two gateways serving two data factories but hello same on-premises data source is registered with both hello data factories.</span></span>
* <span data-ttu-id="7d731-152">Si une passerelle est déjà installée sur votre ordinateur desservant un scénario **Power BI**, installez une **passerelle distincte pour Azure Data Factory** sur un autre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7d731-152">If you already have a gateway installed on your computer serving a **Power BI** scenario, install a **separate gateway for Azure Data Factory** on another machine.</span></span>
* <span data-ttu-id="7d731-153">Vous devez utiliser la passerelle même lorsque vous utilisez **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="7d731-153">Gateway must be used even when you use **ExpressRoute**.</span></span>
* <span data-ttu-id="7d731-154">Considérez votre source de données comme une source de données locale (derrière un pare-feu), même lorsque vous utilisez **ExpressRoute**.</span><span class="sxs-lookup"><span data-stu-id="7d731-154">Treat your data source as an on-premises data source (that is behind a firewall) even when you use **ExpressRoute**.</span></span> <span data-ttu-id="7d731-155">Utiliser une connexion de tooestablish hello passerelle entre le service de hello et de la source de données hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-155">Use hello gateway tooestablish connectivity between hello service and hello data source.</span></span>
* <span data-ttu-id="7d731-156">Vous devez **utiliser hello passerelle** même si le magasin de données hello est dans le cloud de hello sur un **Azure IaaS VM**.</span><span class="sxs-lookup"><span data-stu-id="7d731-156">You must **use hello gateway** even if hello data store is in hello cloud on an **Azure IaaS VM**.</span></span>

## <a name="installation"></a><span data-ttu-id="7d731-157">Installation</span><span class="sxs-lookup"><span data-stu-id="7d731-157">Installation</span></span>
### <a name="prerequisites"></a><span data-ttu-id="7d731-158">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7d731-158">Prerequisites</span></span>
* <span data-ttu-id="7d731-159">prise en charge de Hello **système d’exploitation** versions sont Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="7d731-159">hello supported **Operating System** versions are Windows 7, Windows 8/8.1, Windows 10, Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2.</span></span> <span data-ttu-id="7d731-160">Installation de la passerelle de gestion des données hello sur un contrôleur de domaine n’est actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7d731-160">Installation of hello data management gateway on a domain controller is currently not supported.</span></span>
* <span data-ttu-id="7d731-161">.NET framework 4.5.1 ou version ultérieure est requis.</span><span class="sxs-lookup"><span data-stu-id="7d731-161">.NET Framework 4.5.1 or above is required.</span></span> <span data-ttu-id="7d731-162">Si vous installez la passerelle sur un ordinateur Windows 7, installez .NET Framework 4.5 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7d731-162">If you are installing gateway on a Windows 7 machine, install .NET Framework 4.5 or later.</span></span> <span data-ttu-id="7d731-163">Consultez [Configuration système requise pour .NET Framework](https://msdn.microsoft.com/library/8z6watww.aspx) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="7d731-163">See [.NET Framework System Requirements](https://msdn.microsoft.com/library/8z6watww.aspx) for details.</span></span>
* <span data-ttu-id="7d731-164">Hello recommandé **configuration** pour ordinateur de passerelle hello est au moins 2 GHz, 4 cœurs, 8 Go de RAM et disque 80 Go.</span><span class="sxs-lookup"><span data-stu-id="7d731-164">hello recommended **configuration** for hello gateway machine is at least 2 GHz, 4 cores, 8-GB RAM, and 80-GB disk.</span></span>
* <span data-ttu-id="7d731-165">Si l’ordinateur hôte de hello en veille prolongée, passerelle de hello ne répond pas les demandes toodata.</span><span class="sxs-lookup"><span data-stu-id="7d731-165">If hello host machine hibernates, hello gateway does not respond toodata requests.</span></span> <span data-ttu-id="7d731-166">Par conséquent, configurer un approprié **de l’alimentation** sur ordinateur hello avant d’installer la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-166">Therefore, configure an appropriate **power plan** on hello computer before installing hello gateway.</span></span> <span data-ttu-id="7d731-167">Si la machine de hello est toohibernate configuré, installation de la passerelle hello vous invite à entrer un message.</span><span class="sxs-lookup"><span data-stu-id="7d731-167">If hello machine is configured toohibernate, hello gateway installation prompts a message.</span></span>
* <span data-ttu-id="7d731-168">Vous devez être administrateur sur hello machine tooinstall et configurer la passerelle de gestion des données hello avec succès.</span><span class="sxs-lookup"><span data-stu-id="7d731-168">You must be an administrator on hello machine tooinstall and configure hello data management gateway successfully.</span></span> <span data-ttu-id="7d731-169">Vous pouvez ajouter des utilisateurs supplémentaires toohello **passerelle de gestion des données utilisateurs** groupe Windows local.</span><span class="sxs-lookup"><span data-stu-id="7d731-169">You can add additional users toohello **data management gateway Users** local Windows group.</span></span> <span data-ttu-id="7d731-170">membres Hello de ce groupe sont en mesure de toouse hello **Gestionnaire de Configuration de passerelle de gestion de données** passerelle de hello tooconfigure outil.</span><span class="sxs-lookup"><span data-stu-id="7d731-170">hello members of this group are able toouse hello **Data Management Gateway Configuration Manager** tool tooconfigure hello gateway.</span></span>

<span data-ttu-id="7d731-171">Comme copier activité se produisent sur une fréquence spécifique, hello l’utilisation des ressources (processeur, mémoire) sur l’ordinateur de hello suit également hello même modèle avec des heures de pointe et les temps d’inactivité.</span><span class="sxs-lookup"><span data-stu-id="7d731-171">As copy activity runs happen on a specific frequency, hello resource usage (CPU, memory) on hello machine also follows hello same pattern with peak and idle times.</span></span> <span data-ttu-id="7d731-172">L’utilisation des ressources également dépend fortement hello quantité de données en cours de déplacement.</span><span class="sxs-lookup"><span data-stu-id="7d731-172">Resource utilization also depends heavily on hello amount of data being moved.</span></span> <span data-ttu-id="7d731-173">Lorsque plusieurs travaux sont en cours, vous constaterez une augmentation des ressources utilisées pendant les heures de pointe.</span><span class="sxs-lookup"><span data-stu-id="7d731-173">When multiple copy jobs are in progress, you see resource usage go up during peak times.</span></span>

### <a name="installation-options"></a><span data-ttu-id="7d731-174">Options d’installation</span><span class="sxs-lookup"><span data-stu-id="7d731-174">Installation options</span></span>
<span data-ttu-id="7d731-175">Passerelle de gestion des données peut être installé dans hello suivant façons :</span><span class="sxs-lookup"><span data-stu-id="7d731-175">Data management gateway can be installed in hello following ways:</span></span>

* <span data-ttu-id="7d731-176">En téléchargeant un package d’installation MSI de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="7d731-176">By downloading an MSI setup package from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>  <span data-ttu-id="7d731-177">Hello MSI peut également être utilisé tooupgrade existant données Gestion passerelle toohello version la plus récente, tous les paramètres sont conservés.</span><span class="sxs-lookup"><span data-stu-id="7d731-177">hello MSI can also be used tooupgrade existing data management gateway toohello latest version, with all settings preserved.</span></span>
* <span data-ttu-id="7d731-178">En cliquant sur le lien **Télécharger et installer la passerelle de données** sous INSTALLATION MANUELLE ou **Installer directement sur cet ordinateur** sous INSTALLATION RAPIDE.</span><span class="sxs-lookup"><span data-stu-id="7d731-178">By clicking **Download and install data gateway** link under MANUAL SETUP or **Install directly on this computer** under EXPRESS SETUP.</span></span> <span data-ttu-id="7d731-179">Pour des instructions pas à pas sur l’utilisation de l’installation rapide, consultez l’article [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="7d731-179">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on using express setup.</span></span> <span data-ttu-id="7d731-180">étape manuelle de Hello prend le centre de téléchargement toohello.</span><span class="sxs-lookup"><span data-stu-id="7d731-180">hello manual step takes you toohello download center.</span></span>  <span data-ttu-id="7d731-181">instructions de Hello pour télécharger et installer la passerelle de hello à partir du centre de téléchargement sont fournies dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-181">hello instructions for downloading and installing hello gateway from download center are in hello next section.</span></span>

### <a name="installation-best-practices"></a><span data-ttu-id="7d731-182">Meilleures pratiques d’installation :</span><span class="sxs-lookup"><span data-stu-id="7d731-182">Installation best practices:</span></span>
1. <span data-ttu-id="7d731-183">Configurer le mode d’alimentation sur l’ordinateur hôte de hello pour la passerelle de hello afin que hello machine ne pas en veille prolongée.</span><span class="sxs-lookup"><span data-stu-id="7d731-183">Configure power plan on hello host machine for hello gateway so that hello machine does not hibernate.</span></span> <span data-ttu-id="7d731-184">Si l’ordinateur hôte de hello en veille prolongée, passerelle de hello ne répond pas les demandes toodata.</span><span class="sxs-lookup"><span data-stu-id="7d731-184">If hello host machine hibernates, hello gateway does not respond toodata requests.</span></span>
2. <span data-ttu-id="7d731-185">Sauvegardez le certificat hello associé hello passerelle.</span><span class="sxs-lookup"><span data-stu-id="7d731-185">Back up hello certificate associated with hello gateway.</span></span>

### <a name="install-hello-gateway-from-download-center"></a><span data-ttu-id="7d731-186">Installer la passerelle de hello à partir du centre de téléchargement</span><span class="sxs-lookup"><span data-stu-id="7d731-186">Install hello gateway from download center</span></span>
1. <span data-ttu-id="7d731-187">Accédez trop[page de téléchargement de passerelle de gestion des données Microsoft](https://www.microsoft.com/download/details.aspx?id=39717).</span><span class="sxs-lookup"><span data-stu-id="7d731-187">Navigate too[Microsoft Data Management Gateway download page](https://www.microsoft.com/download/details.aspx?id=39717).</span></span>
2. <span data-ttu-id="7d731-188">Cliquez sur **télécharger**, sélectionnez hello version appropriée (**32 bits** Visual Studio. **64 bits**), puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="7d731-188">Click **Download**, select hello appropriate version (**32-bit** vs. **64-bit**), and click **Next**.</span></span>
3. <span data-ttu-id="7d731-189">Exécutez hello **MSI** directement ou enregistrez-le tooyour disque et les exécuter.</span><span class="sxs-lookup"><span data-stu-id="7d731-189">Run hello **MSI** directly or save it tooyour hard disk and run.</span></span>
4. <span data-ttu-id="7d731-190">Sur hello **Bienvenue** page, sélectionnez un **langage** cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="7d731-190">On hello **Welcome** page, select a **language** click **Next**.</span></span>
5. <span data-ttu-id="7d731-191">**Accepter** hello du contrat de licence utilisateur final et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="7d731-191">**Accept** hello End-User License Agreement and click **Next**.</span></span>
6. <span data-ttu-id="7d731-192">Sélectionnez **dossier** tooinstall hello passerelle, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="7d731-192">Select **folder** tooinstall hello gateway and click **Next**.</span></span>
7. <span data-ttu-id="7d731-193">Sur hello **tooinstall prêt** , cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="7d731-193">On hello **Ready tooinstall** page, click **Install**.</span></span>
8. <span data-ttu-id="7d731-194">Cliquez sur **Terminer** toocomplete installation.</span><span class="sxs-lookup"><span data-stu-id="7d731-194">Click **Finish** toocomplete installation.</span></span>
9. <span data-ttu-id="7d731-195">Obtenir la clé de hello hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7d731-195">Get hello key from hello Azure portal.</span></span> <span data-ttu-id="7d731-196">Consultez hello la section suivante pour obtenir des instructions pas à pas.</span><span class="sxs-lookup"><span data-stu-id="7d731-196">See hello next section for step-by-step instructions.</span></span>
10. <span data-ttu-id="7d731-197">Sur hello **Registre passerelle** page de **Gestionnaire de Configuration de passerelle de gestion de données** en cours d’exécution sur votre ordinateur, procédez comme hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7d731-197">On hello **Register gateway** page of **Data Management Gateway Configuration Manager** running on your machine, do hello following steps:</span></span>
    1. <span data-ttu-id="7d731-198">Collez la clé de hello texte hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-198">Paste hello key in hello text.</span></span>
    2. <span data-ttu-id="7d731-199">Si vous le souhaitez, cliquez sur **afficher la clé de passerelle** texte de la touche toosee hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-199">Optionally, click **Show gateway key** toosee hello key text.</span></span>
    3. <span data-ttu-id="7d731-200">Cliquez sur **S'inscrire**.</span><span class="sxs-lookup"><span data-stu-id="7d731-200">Click **Register**.</span></span>

### <a name="register-gateway-using-key"></a><span data-ttu-id="7d731-201">Inscrire la passerelle à l’aide de la clé</span><span class="sxs-lookup"><span data-stu-id="7d731-201">Register gateway using key</span></span>
#### <a name="if-you-havent-already-created-a-logical-gateway-in-hello-portal"></a><span data-ttu-id="7d731-202">Si vous n’avez pas déjà créé une passerelle logique dans le portail de hello</span><span class="sxs-lookup"><span data-stu-id="7d731-202">If you haven't already created a logical gateway in hello portal</span></span>
<span data-ttu-id="7d731-203">toocreate une passerelle dans hello portal et get hello la clé à partir de hello **configurer** page, suivez les étapes de procédure pas à pas Bonjour [déplacement des données entre locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="7d731-203">toocreate a gateway in hello portal and get hello key from hello **Configure** page, Follow steps from walkthrough in hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>    

#### <a name="if-you-have-already-created-hello-logical-gateway-in-hello-portal"></a><span data-ttu-id="7d731-204">Si vous avez déjà créé la passerelle logique de hello dans le portail de hello</span><span class="sxs-lookup"><span data-stu-id="7d731-204">If you have already created hello logical gateway in hello portal</span></span>
1. <span data-ttu-id="7d731-205">Dans le portail Azure, accédez toohello **Data Factory** page, puis cliquez sur **Services liés** vignette.</span><span class="sxs-lookup"><span data-stu-id="7d731-205">In Azure portal, navigate toohello **Data Factory** page, and click **Linked Services** tile.</span></span>

    ![Page Data Factory](media/data-factory-data-management-gateway/data-factory-blade.png)
2. <span data-ttu-id="7d731-207">Bonjour **Services liés** page, sélectionnez hello logique **passerelle** vous avez créé dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-207">In hello **Linked Services** page, select hello logical **gateway** you created in hello portal.</span></span>

    ![passerelle logique](media/data-factory-data-management-gateway/data-factory-select-gateway.png)  
3. <span data-ttu-id="7d731-209">Bonjour **passerelle de données** , cliquez sur **télécharger et installer la passerelle de données**.</span><span class="sxs-lookup"><span data-stu-id="7d731-209">In hello **Data Gateway** page, click **Download and install data gateway**.</span></span>

    ![Télécharger le lien dans le portail de hello](media/data-factory-data-management-gateway/download-and-install-link-on-portal.png)   
4. <span data-ttu-id="7d731-211">Bonjour **configurer** , cliquez sur **recréez clé**.</span><span class="sxs-lookup"><span data-stu-id="7d731-211">In hello **Configure** page, click **Recreate key**.</span></span> <span data-ttu-id="7d731-212">Cliquez sur Oui sur le message d’avertissement hello après leur lecture avec soin.</span><span class="sxs-lookup"><span data-stu-id="7d731-212">Click Yes on hello warning message after reading it carefully.</span></span>

    ![Recréer une clé](media/data-factory-data-management-gateway/recreate-key-button.png)
5. <span data-ttu-id="7d731-214">Cliquez sur Copier bouton suivant toohello la clé.</span><span class="sxs-lookup"><span data-stu-id="7d731-214">Click Copy button next toohello key.</span></span> <span data-ttu-id="7d731-215">clé de Hello est copié toohello Presse-papiers.</span><span class="sxs-lookup"><span data-stu-id="7d731-215">hello key is copied toohello clipboard.</span></span>

    ![Copier la clé](media/data-factory-data-management-gateway/copy-gateway-key.png)

### <a name="system-tray-icons-notifications"></a><span data-ttu-id="7d731-217">Icônes de la barre d’état système/notifications</span><span class="sxs-lookup"><span data-stu-id="7d731-217">System tray icons/ notifications</span></span>
<span data-ttu-id="7d731-218">Hello image suivante montre certains des hello des icônes de barre d’état que vous voyez.</span><span class="sxs-lookup"><span data-stu-id="7d731-218">hello following image shows some of hello tray icons that you see.</span></span>

![Icônes de la barre d’état système](./media/data-factory-data-management-gateway/gateway-tray-icons.png)

<span data-ttu-id="7d731-220">Si vous déplacez le curseur sur hello système barre d’état et l’avis de l’icône du message, vous consultez les détails sur l’état de hello d’opération de mise à jour de passerelle/hello dans une fenêtre contextuelle.</span><span class="sxs-lookup"><span data-stu-id="7d731-220">If you move cursor over hello system tray icon/notification message, you see details about hello state of hello gateway/update operation in a popup window.</span></span>

### <a name="ports-and-firewall"></a><span data-ttu-id="7d731-221">Ports et pare-feu</span><span class="sxs-lookup"><span data-stu-id="7d731-221">Ports and firewall</span></span>
<span data-ttu-id="7d731-222">Il existe deux pare-feu, vous devez tooconsider : **pare-feu d’entreprise** en cours d’exécution sur le routeur central de hello d’organisation de hello, et **pare-feu Windows** configuré comme un démon sur l’ordinateur local de hello où hello passerelle est installée.</span><span class="sxs-lookup"><span data-stu-id="7d731-222">There are two firewalls you need tooconsider: **corporate firewall** running on hello central router of hello organization, and **Windows firewall** configured as a daemon on hello local machine where hello gateway is installed.</span></span>  

![Pare-feu](./media/data-factory-data-management-gateway/firewalls2.png)

<span data-ttu-id="7d731-224">Au niveau du pare-feu d’entreprise, vous devez configurer les éléments suivants de hello domaines et les ports de sortie :</span><span class="sxs-lookup"><span data-stu-id="7d731-224">At corporate firewall level, you need configure hello following domains and outbound ports:</span></span>

| <span data-ttu-id="7d731-225">Noms de domaine</span><span class="sxs-lookup"><span data-stu-id="7d731-225">Domain names</span></span> | <span data-ttu-id="7d731-226">Ports</span><span class="sxs-lookup"><span data-stu-id="7d731-226">Ports</span></span> | <span data-ttu-id="7d731-227">Description</span><span class="sxs-lookup"><span data-stu-id="7d731-227">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7d731-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="7d731-228">*.servicebus.windows.net</span></span> |<span data-ttu-id="7d731-229">443, 80</span><span class="sxs-lookup"><span data-stu-id="7d731-229">443, 80</span></span> |<span data-ttu-id="7d731-230">Utilisé pour la communication avec le serveur principal du service Déplacement des données</span><span class="sxs-lookup"><span data-stu-id="7d731-230">Used for communication with Data Movement Service backend</span></span> |
| <span data-ttu-id="7d731-231">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="7d731-231">*.core.windows.net</span></span> |<span data-ttu-id="7d731-232">443</span><span class="sxs-lookup"><span data-stu-id="7d731-232">443</span></span> |<span data-ttu-id="7d731-233">Utilisé pour une copie intermédiaire à l’aide d’objets Blob Azure (si configuré)</span><span class="sxs-lookup"><span data-stu-id="7d731-233">Used for Staged copy using Azure Blob (if configured)</span></span>|
| <span data-ttu-id="7d731-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="7d731-234">*.frontend.clouddatahub.net</span></span> |<span data-ttu-id="7d731-235">443</span><span class="sxs-lookup"><span data-stu-id="7d731-235">443</span></span> |<span data-ttu-id="7d731-236">Utilisé pour la communication avec le serveur principal du service Déplacement des données</span><span class="sxs-lookup"><span data-stu-id="7d731-236">Used for communication with Data Movement Service backend</span></span> |


<span data-ttu-id="7d731-237">Au niveau du pare-feu Windows, ces ports de sortie sont normalement activés.</span><span class="sxs-lookup"><span data-stu-id="7d731-237">At Windows firewall level, these outbound ports are normally enabled.</span></span> <span data-ttu-id="7d731-238">Si non, vous pouvez configurer les ports et les domaines de hello en conséquence sur l’ordinateur de passerelle.</span><span class="sxs-lookup"><span data-stu-id="7d731-238">If not, you can configure hello domains and ports accordingly on gateway machine.</span></span>

> [!NOTE]
> 1. <span data-ttu-id="7d731-239">En fonction de votre source / récepteurs, vous avez peut-être toowhitelist d’autres domaines et les ports de sortie dans votre pare-feu d’entreprise et Windows.</span><span class="sxs-lookup"><span data-stu-id="7d731-239">Based on your source/ sinks, you may have toowhitelist additional domains and outbound ports in your corporate/Windows firewall.</span></span>
> 2. <span data-ttu-id="7d731-240">Pour certaines bases de données Cloud (par exemple : [base de données SQL Azure](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), vous devrez peut-être adresse toowhitelist de l’ordinateur de passerelle sur leur configuration de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="7d731-240">For some Cloud Databases (For example: [Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-configure-firewall-settings), [Azure Data Lake](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-secure-data#set-ip-address-range-for-data-access), etc.), you may need toowhitelist IP address of Gateway machine on their firewall configuration.</span></span>
>
>


#### <a name="copy-data-from-a-source-data-store-tooa-sink-data-store"></a><span data-ttu-id="7d731-241">Copier des données à partir d’un magasin de données du magasin tooa récepteur source données</span><span class="sxs-lookup"><span data-stu-id="7d731-241">Copy data from a source data store tooa sink data store</span></span>
<span data-ttu-id="7d731-242">Assurez-vous que les règles de pare-feu de hello sont activées correctement sur le pare-feu d’entreprise hello, le pare-feu Windows sur l’ordinateur de passerelle hello, et du magasin de données de hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="7d731-242">Ensure that hello firewall rules are enabled properly on hello corporate firewall, Windows firewall on hello gateway machine, and hello data store itself.</span></span> <span data-ttu-id="7d731-243">L’activation de ces règles permet hello source de passerelle tooconnect tooboth et récepteur avec succès.</span><span class="sxs-lookup"><span data-stu-id="7d731-243">Enabling these rules allows hello gateway tooconnect tooboth source and sink successfully.</span></span> <span data-ttu-id="7d731-244">Activer les règles pour chaque magasin de données impliquée dans une opération de copie hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-244">Enable rules for each data store that is involved in hello copy operation.</span></span>

<span data-ttu-id="7d731-245">Par exemple, toocopy de **un récepteur Azure SQL Database tooan de banque de données locale ou un récepteur d’Azure SQL Data Warehouse**, hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7d731-245">For example, toocopy from **an on-premises data store tooan Azure SQL Database sink or an Azure SQL Data Warehouse sink**, do hello following steps:</span></span>

* <span data-ttu-id="7d731-246">Autorisez le trafic **TCP** sortant sur le port **1433** pour le pare-feu Windows et le pare-feu d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="7d731-246">Allow outbound **TCP** communication on port **1433** for both Windows firewall and corporate firewall.</span></span>
* <span data-ttu-id="7d731-247">Configurez les paramètres de pare-feu hello de SQL Azure tooadd hello adresse IP du serveur de liste de toohello hello passerelle machine d’adresses IP autorisées.</span><span class="sxs-lookup"><span data-stu-id="7d731-247">Configure hello firewall settings of Azure SQL server tooadd hello IP address of hello gateway machine toohello list of allowed IP addresses.</span></span>

> [!NOTE]
> <span data-ttu-id="7d731-248">Si votre pare-feu n’autorise pas le port de sortie 1433, la passerelle ne peut pas accéder directement à Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="7d731-248">If your firewall does not allow outbound port 1433, Gateway can't access Azure SQL directly.</span></span> <span data-ttu-id="7d731-249">Dans ce cas, vous pouvez utiliser [intermédiaire de copie](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL de la base de données Azure / entrepôt de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="7d731-249">In this case, you may use [Staged Copy](https://docs.microsoft.com/azure/data-factory/data-factory-copy-activity-performance#staged-copy) tooSQL Azure Database/ SQL Azure DW.</span></span> <span data-ttu-id="7d731-250">Dans ce scénario, vous nécessiterait HTTPS (port 443) pour le déplacement des données de hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-250">In this scenario, you would only require HTTPS (port 443) for hello data movement.</span></span>
>
>


### <a name="proxy-server-considerations"></a><span data-ttu-id="7d731-251">Considérations relatives aux serveurs proxy</span><span class="sxs-lookup"><span data-stu-id="7d731-251">Proxy server considerations</span></span>
<span data-ttu-id="7d731-252">Si votre environnement de réseau d’entreprise utilise un proxy serveur tooaccess hello internet, configurer les paramètres de proxy appropriés de données Gestion passerelle toouse.</span><span class="sxs-lookup"><span data-stu-id="7d731-252">If your corporate network environment uses a proxy server tooaccess hello internet, configure data management gateway toouse appropriate proxy settings.</span></span> <span data-ttu-id="7d731-253">Vous pouvez définir le proxy de hello pendant la phase initiale d’inscription de hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-253">You can set hello proxy during hello initial registration phase.</span></span>

![Définir le serveur proxy lors de l’inscription](media/data-factory-data-management-gateway/SetProxyDuringRegistration.png)

<span data-ttu-id="7d731-255">Gateway utilise le service de cloud hello proxy server tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="7d731-255">Gateway uses hello proxy server tooconnect toohello cloud service.</span></span> <span data-ttu-id="7d731-256">Cliquez sur le lien **Modifier** pendant l’installation initiale.</span><span class="sxs-lookup"><span data-stu-id="7d731-256">Click **Change** link during initial setup.</span></span> <span data-ttu-id="7d731-257">Vous consultez hello **paramètre proxy** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7d731-257">You see hello **proxy setting** dialog.</span></span>

![Définir le proxy avec le gestionnaire de configuration](media/data-factory-data-management-gateway/SetProxySettings.png)

<span data-ttu-id="7d731-259">Il existe trois options de configuration :</span><span class="sxs-lookup"><span data-stu-id="7d731-259">There are three configuration options:</span></span>

* <span data-ttu-id="7d731-260">**N’utilisez pas de proxy**: passerelle n’utilise pas explicitement tous les services de toocloud tooconnect proxy.</span><span class="sxs-lookup"><span data-stu-id="7d731-260">**Do not use proxy**: Gateway does not explicitly use any proxy tooconnect toocloud services.</span></span>
* <span data-ttu-id="7d731-261">**Utiliser le proxy système**: passerelle utilise le proxy hello paramètre qui est configuré dans diahost.exe.config et diawp.exe.config.  Si aucun proxy n’est configuré dans diahost.exe.config et diawp.exe.config, passerelle connecte toocloud service directement sans passer par le proxy.</span><span class="sxs-lookup"><span data-stu-id="7d731-261">**Use system proxy**: Gateway uses hello proxy setting that is configured in diahost.exe.config and diawp.exe.config.  If no proxy is configured in diahost.exe.config and diawp.exe.config, gateway connects toocloud service directly without going through proxy.</span></span>
* <span data-ttu-id="7d731-262">**Utiliser le proxy personnalisé**: configurer hello HTTP proxy paramètre toouse pour la passerelle, au lieu d’utiliser des configurations dans diahost.exe.config et diawp.exe.config.  L’adresse et le port sont requis.</span><span class="sxs-lookup"><span data-stu-id="7d731-262">**Use custom proxy**: Configure hello HTTP proxy setting toouse for gateway, instead of using configurations in diahost.exe.config and diawp.exe.config.  Address and Port are required.</span></span>  <span data-ttu-id="7d731-263">Le nom d’utilisateur et le mot de passe sont facultatifs selon le paramètre d’authentification de votre proxy.</span><span class="sxs-lookup"><span data-stu-id="7d731-263">User Name and Password are optional depending on your proxy’s authentication setting.</span></span>  <span data-ttu-id="7d731-264">Tous les paramètres sont chiffrés par le certificat d’informations d’identification de hello de passerelle de hello et stockées localement sur l’ordinateur hôte de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-264">All settings are encrypted with hello credential certificate of hello gateway and stored locally on hello gateway host machine.</span></span>

<span data-ttu-id="7d731-265">passerelle de gestion des données Hello Service hôte redémarre automatiquement après avoir enregistré les paramètres de proxy hello mis à jour.</span><span class="sxs-lookup"><span data-stu-id="7d731-265">hello data management gateway Host Service restarts automatically after you save hello updated proxy settings.</span></span>

<span data-ttu-id="7d731-266">Une fois la passerelle a été inscrit avec succès, si vous souhaitez tooview ou mettre à jour les paramètres de proxy, utilisez le Gestionnaire de Configuration de passerelle de gestion de données.</span><span class="sxs-lookup"><span data-stu-id="7d731-266">After gateway has been successfully registered, if you want tooview or update proxy settings, use Data Management Gateway Configuration Manager.</span></span>

1. <span data-ttu-id="7d731-267">Lancez le **Gestionnaire de configuration de la passerelle de gestion des données**.</span><span class="sxs-lookup"><span data-stu-id="7d731-267">Launch **Data Management Gateway Configuration Manager**.</span></span>
2. <span data-ttu-id="7d731-268">Commutateur toohello **paramètres** onglet.</span><span class="sxs-lookup"><span data-stu-id="7d731-268">Switch toohello **Settings** tab.</span></span>
3. <span data-ttu-id="7d731-269">Cliquez sur **modification** lien dans **HTTP Proxy** hello toolaunch de section **définir le Proxy HTTP** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="7d731-269">Click **Change** link in **HTTP Proxy** section toolaunch hello **Set HTTP Proxy** dialog.</span></span>  
4. <span data-ttu-id="7d731-270">Après avoir cliqué sur hello **suivant** bouton, vous voyez une boîte de dialogue Avertissement demandant pour vos paramètres du proxy autorisation toosave hello et le redémarrage du Service hôte de passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-270">After you click hello **Next** button, you see a warning dialog asking for your permission toosave hello proxy setting and restart hello Gateway Host Service.</span></span>

<span data-ttu-id="7d731-271">Vous pouvez afficher et mettre à jour le proxy HTTP à l’aide de l’outil Gestionnaire de Configuration.</span><span class="sxs-lookup"><span data-stu-id="7d731-271">You can view and update HTTP proxy by using Configuration Manager tool.</span></span>

![Définir le proxy avec le gestionnaire de configuration](media/data-factory-data-management-gateway/SetProxyConfigManager.png)

> [!NOTE]
> <span data-ttu-id="7d731-273">Si vous configurez un serveur proxy avec l’authentification NTLM, le Service hôte de passerelle s’exécute sous un compte de domaine hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-273">If you set up a proxy server with NTLM authentication, Gateway Host Service runs under hello domain account.</span></span> <span data-ttu-id="7d731-274">Si vous modifiez le mot de passe hello pour le compte de domaine hello plus tard, n’oubliez pas de tooupdate les paramètres de configuration de service de hello et redémarrez-le en conséquence.</span><span class="sxs-lookup"><span data-stu-id="7d731-274">If you change hello password for hello domain account later, remember tooupdate configuration settings for hello service and restart it accordingly.</span></span> <span data-ttu-id="7d731-275">En raison de la spécification de toothis, nous vous suggérons de que vous utilisez un serveur dédié domaine compte tooaccess hello proxy qui ne nécessite pas un mot de passe tooupdate hello fréquemment.</span><span class="sxs-lookup"><span data-stu-id="7d731-275">Due toothis requirement, we suggest you use a dedicated domain account tooaccess hello proxy server that does not require you tooupdate hello password frequently.</span></span>
>
>

### <a name="configure-proxy-server-settings"></a><span data-ttu-id="7d731-276">Configurer les paramètres du serveur proxy</span><span class="sxs-lookup"><span data-stu-id="7d731-276">Configure proxy server settings</span></span>
<span data-ttu-id="7d731-277">Si vous sélectionnez **utiliser le proxy système** définition pour le proxy de hello HTTP, la passerelle utilise hello paramètre de proxy dans diahost.exe.config et diawp.exe.config.  Si aucun proxy n’est spécifié dans diahost.exe.config et diawp.exe.config, passerelle connecte toocloud service directement sans passer par le proxy.</span><span class="sxs-lookup"><span data-stu-id="7d731-277">If you select **Use system proxy** setting for hello HTTP proxy, gateway uses hello proxy setting in diahost.exe.config and diawp.exe.config.  If no proxy is specified in diahost.exe.config and diawp.exe.config, gateway connects toocloud service directly without going through proxy.</span></span> <span data-ttu-id="7d731-278">Hello procédure suivante fournit des instructions pour mettre à jour le fichier de diahost.exe.config hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-278">hello following procedure provides instructions for updating hello diahost.exe.config file.</span></span>  

1. <span data-ttu-id="7d731-279">Dans l’Explorateur de fichiers, constituent une copie de sauvegarde de C:\Program Files\Microsoft données Gestion Gateway\2.0\Shared\diahost.exe.config tooback fichier d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-279">In File Explorer, make a safe copy of C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config tooback up hello original file.</span></span>
2. <span data-ttu-id="7d731-280">Lancez Notepad.exe en tant qu’administrateur, puis ouvrez le fichier texte C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. Vous recherchez balise par défaut de hello system.net comme indiqué dans hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="7d731-280">Launch Notepad.exe running as administrator, and open text file “C:\Program Files\Microsoft Data Management Gateway\2.0\Shared\diahost.exe.config. You find hello default tag for system.net as shown in hello following code:</span></span>

         <system.net>
             <defaultProxy useDefaultCredentials="true" />
         </system.net>    

   <span data-ttu-id="7d731-281">Vous pouvez ensuite ajouter les détails du serveur proxy comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="7d731-281">You can then add proxy server details as shown in hello following example:</span></span>

         <system.net>
               <defaultProxy enabled="true">
                     <proxy bypassonlocal="true" proxyaddress="http://proxy.domain.org:8888/" />
               </defaultProxy>
         </system.net>

   <span data-ttu-id="7d731-282">Propriétés supplémentaires sont autorisées dans les paramètres hello proxy balise toospecify hello requis comme scriptLocation.</span><span class="sxs-lookup"><span data-stu-id="7d731-282">Additional properties are allowed inside hello proxy tag toospecify hello required settings like scriptLocation.</span></span> <span data-ttu-id="7d731-283">Consultez trop[proxy, élément (paramètres réseau)](https://msdn.microsoft.com/library/sa91de1e.aspx) sur la syntaxe.</span><span class="sxs-lookup"><span data-stu-id="7d731-283">Refer too[proxy Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on syntax.</span></span>

         <proxy autoDetect="true|false|unspecified" bypassonlocal="true|false|unspecified" proxyaddress="uriString" scriptLocation="uriString" usesystemdefault="true|false|unspecified "/>
3. <span data-ttu-id="7d731-284">Enregistrer le fichier de configuration hello dans l’emplacement d’origine de hello, puis redémarrez hello service hôte de passerelle de gestion de données, qui Récupère les modifications hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-284">Save hello configuration file into hello original location, then restart hello Data Management Gateway Host service, which picks up hello changes.</span></span> <span data-ttu-id="7d731-285">service de hello toorestart : utiliser l’applet services à partir du Panneau de configuration hello ou hello **Gestionnaire de Configuration de passerelle de gestion de données** > cliquez sur hello **arrêter le Service** , puis cliquez sur hello **Démarrer le Service**.</span><span class="sxs-lookup"><span data-stu-id="7d731-285">toorestart hello service: use services applet from hello control panel, or from hello **Data Management Gateway Configuration Manager** > click hello **Stop Service** button, then click hello **Start Service**.</span></span> <span data-ttu-id="7d731-286">Si le service de hello ne démarre pas, il est probable qu’une syntaxe de balise XML incorrecte a été ajoutée dans le fichier de configuration d’application hello qui a été modifié.</span><span class="sxs-lookup"><span data-stu-id="7d731-286">If hello service does not start, it is likely that an incorrect XML tag syntax has been added into hello application configuration file that was edited.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d731-287">N’oubliez pas de tooupdate **les deux** diahost.exe.config et diawp.exe.config.</span><span class="sxs-lookup"><span data-stu-id="7d731-287">Do not forget tooupdate **both** diahost.exe.config and diawp.exe.config.</span></span>  


<span data-ttu-id="7d731-288">En outre les points toothese, vous devez également toomake que Microsoft Azure se trouve dans la liste blanche d’adresses de votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="7d731-288">In addition toothese points, you also need toomake sure Microsoft Azure is in your company’s whitelist.</span></span> <span data-ttu-id="7d731-289">liste Hello des adresses IP de Microsoft Azure valides peut être téléchargée à partir de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="7d731-289">hello list of valid Microsoft Azure IP addresses can be downloaded from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

#### <a name="possible-symptoms-for-firewall-and-proxy-server-related-issues"></a><span data-ttu-id="7d731-290">Symptômes possibles des erreurs liées au pare-feu et au serveur proxy</span><span class="sxs-lookup"><span data-stu-id="7d731-290">Possible symptoms for firewall and proxy server-related issues</span></span>
<span data-ttu-id="7d731-291">Si vous rencontrez des erreurs toohello similaire après ceux, il est probable en raison de la configuration tooimproper de hello pare-feu ou un serveur proxy, qui bloque la passerelle de connexion tooauthenticate de fabrique tooData lui-même.</span><span class="sxs-lookup"><span data-stu-id="7d731-291">If you encounter errors similar toohello following ones, it is likely due tooimproper configuration of hello firewall or proxy server, which blocks gateway from connecting tooData Factory tooauthenticate itself.</span></span> <span data-ttu-id="7d731-292">Consultez tooensure de section tooprevious votre serveur proxy et de pare-feu sont configurés correctement.</span><span class="sxs-lookup"><span data-stu-id="7d731-292">Refer tooprevious section tooensure your firewall and proxy server are properly configured.</span></span>

1. <span data-ttu-id="7d731-293">Lorsque vous essayez de passerelle de hello tooregister, vous recevez hello l’erreur suivante : « clé de passerelle n’a pas pu tooregister hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-293">When you try tooregister hello gateway, you receive hello following error: "Failed tooregister hello gateway key.</span></span> <span data-ttu-id="7d731-294">Avant de réessayer la clé de passerelle tooregister hello, vérifiez que hello passerelle de gestion des données est dans un état connecté et hello Service hôte de passerelle de gestion des données est démarré. »</span><span class="sxs-lookup"><span data-stu-id="7d731-294">Before trying tooregister hello gateway key again, confirm that hello data management gateway is in a connected state and hello Data Management Gateway Host Service is Started."</span></span>
2. <span data-ttu-id="7d731-295">Lorsque vous ouvrez le Gestionnaire de configuration, l’état indiqué est « Déconnecté » ou « En cours de connexion ».</span><span class="sxs-lookup"><span data-stu-id="7d731-295">When you open Configuration Manager, you see status as “Disconnected” or “Connecting.”</span></span> <span data-ttu-id="7d731-296">Lors de l’affichage des journaux des événements Windows, sous « Observateur d’événements » > « Applications et Services Logs » > « Passerelle de gestion des données », vous voyez des messages d’erreur tels que hello l’erreur suivante :`Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span><span class="sxs-lookup"><span data-stu-id="7d731-296">When viewing Windows event logs, under “Event Viewer” > “Application and Services Logs” > “Data Management Gateway”, you see error messages such as hello following error: `Unable tooconnect toohello remote server`
   `A component of Data Management Gateway has become unresponsive and restarts automatically. Component name: Gateway.`</span></span>

### <a name="open-port-8050-for-credential-encryption"></a><span data-ttu-id="7d731-297">Ouvrir le port 8050 pour le chiffrement des informations d’identification</span><span class="sxs-lookup"><span data-stu-id="7d731-297">Open port 8050 for credential encryption</span></span>
<span data-ttu-id="7d731-298">Hello **informations d’identification du paramètre** application utilise hello port entrant **8050** passerelle de toohello toorelay informations d’identification lorsque vous configurez un site local lié à service Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7d731-298">hello **Setting Credentials** application uses hello inbound port **8050** toorelay credentials toohello gateway when you set up an on-premises linked service in hello Azure portal.</span></span> <span data-ttu-id="7d731-299">Pendant l’installation de la passerelle, par défaut, installation de la passerelle hello ouvre sur l’ordinateur de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-299">During gateway setup, by default, hello gateway installation opens it on hello gateway machine.</span></span>

<span data-ttu-id="7d731-300">Si vous utilisez un pare-feu tiers, vous pouvez ouvrir manuellement le port hello 8050.</span><span class="sxs-lookup"><span data-stu-id="7d731-300">If you are using a third-party firewall, you can manually open hello port 8050.</span></span> <span data-ttu-id="7d731-301">Si vous rencontrez des problème de pare-feu pendant l’installation de la passerelle, vous pouvez essayer d’utiliser hello suivant de passerelle de commande tooinstall hello sans configurer le pare-feu hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-301">If you run into firewall issue during gateway setup, you can try using hello following command tooinstall hello gateway without configuring hello firewall.</span></span>

    msiexec /q /i DataManagementGateway.msi NOFIREWALL=1

<span data-ttu-id="7d731-302">Si vous ne choisissez pas tooopen port hello 8050 sur l’ordinateur de passerelle hello, utilisent des mécanismes de différent à l’aide de hello **informations d’identification du paramètre** tooconfigure les données d’application stocke des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="7d731-302">If you choose not tooopen hello port 8050 on hello gateway machine, use mechanisms other than using hello **Setting Credentials** application tooconfigure data store credentials.</span></span> <span data-ttu-id="7d731-303">Vous pouvez par exemple utiliser l’applet de commande PowerShell [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) .</span><span class="sxs-lookup"><span data-stu-id="7d731-303">For example, you could use [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="7d731-304">Consultez la section [Configuration des informations d’identification et de la sécurité](#set-credentials-and-securityy) pour savoir comment configurer les informations d’identification de la banque de données.</span><span class="sxs-lookup"><span data-stu-id="7d731-304">See [Setting Credentials and Security](#set-credentials-and-securityy) section on how data store credentials can be set.</span></span>

## <a name="update"></a><span data-ttu-id="7d731-305">Mettre à jour</span><span class="sxs-lookup"><span data-stu-id="7d731-305">Update</span></span>
<span data-ttu-id="7d731-306">Par défaut, passerelle de gestion des données est automatiquement mis à jour lorsqu’une version plus récente de la passerelle de hello est disponible.</span><span class="sxs-lookup"><span data-stu-id="7d731-306">By default, data management gateway is automatically updated when a newer version of hello gateway is available.</span></span> <span data-ttu-id="7d731-307">passerelle de Hello n’est pas mis à jour jusqu'à ce que toutes les tâches planifiée de hello sont terminés.</span><span class="sxs-lookup"><span data-stu-id="7d731-307">hello gateway is not updated until all hello scheduled tasks are done.</span></span> <span data-ttu-id="7d731-308">Aucune autre tâche n’est traitées par la passerelle de hello avant la fin de l’opération de mise à jour hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-308">No further tasks are processed by hello gateway until hello update operation is completed.</span></span> <span data-ttu-id="7d731-309">En cas de mise à jour hello, passerelle est restaurée toohello une ancienne version.</span><span class="sxs-lookup"><span data-stu-id="7d731-309">If hello update fails, gateway is rolled back toohello old version.</span></span>

<span data-ttu-id="7d731-310">Vous consultez heure de mise à jour planifiée de hello Bonjour suivant place :</span><span class="sxs-lookup"><span data-stu-id="7d731-310">You see hello scheduled update time in hello following places:</span></span>

* <span data-ttu-id="7d731-311">page des propriétés passerelle Hello hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7d731-311">hello gateway properties page in hello Azure portal.</span></span>
* <span data-ttu-id="7d731-312">Page d’accueil du Gestionnaire de Configuration de passerelle de gestion de données de hello</span><span class="sxs-lookup"><span data-stu-id="7d731-312">Home page of hello Data Management Gateway Configuration Manager</span></span>
* <span data-ttu-id="7d731-313">Message de notification de la barre d’état du système.</span><span class="sxs-lookup"><span data-stu-id="7d731-313">System tray notification message.</span></span>

<span data-ttu-id="7d731-314">onglet Accueil de Hello Hello Gestionnaire de Configuration de passerelle de gestion de données affiche la planification de mise à jour de hello et passerelle de hello hello dernière heure a été installé ou mis à jour.</span><span class="sxs-lookup"><span data-stu-id="7d731-314">hello Home tab of hello Data Management Gateway Configuration Manager displays hello update schedule and hello last time hello gateway was installed/updated.</span></span>

![Planifier les mises à jour](media/data-factory-data-management-gateway/UpdateSection.png)

<span data-ttu-id="7d731-316">Vous pouvez installer les mises à jour hello immédiatement ou attendre hello passerelle toobe est automatiquement mis à jour au moment de hello planifiée.</span><span class="sxs-lookup"><span data-stu-id="7d731-316">You can install hello update right away or wait for hello gateway toobe automatically updated at hello scheduled time.</span></span> <span data-ttu-id="7d731-317">Par exemple, hello ci-dessous illustre image hello de message de notification montrée dans hello Gestionnaire de Configuration de passerelle en même temps que le bouton de mise à jour hello que vous pouvez cliquer sur tooinstall immédiatement.</span><span class="sxs-lookup"><span data-stu-id="7d731-317">For example, hello following image shows you hello notification message shown in hello Gateway Configuration Manager along with hello Update button that you can click tooinstall it immediately.</span></span>

![Mise à jour dans DMG Configuration Manager](./media/data-factory-data-management-gateway/gateway-auto-update-config-manager.png)

<span data-ttu-id="7d731-319">message de notification Hello dans la barre d’état système hello se présente comme dans hello suivant image :</span><span class="sxs-lookup"><span data-stu-id="7d731-319">hello notification message in hello system tray would look as shown in hello following image:</span></span>

![Message de barre d’état système](./media/data-factory-data-management-gateway/gateway-auto-update-tray-message.png)

<span data-ttu-id="7d731-321">Vous consultez État hello d’opération de mise à jour (manuelle ou automatique) dans la barre d’état système hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-321">You see hello status of update operation (manual or automatic) in hello system tray.</span></span> <span data-ttu-id="7d731-322">Lorsque vous lancez le Gestionnaire de Configuration de passerelle prochaine, vous voyez un message de notification hello cette passerelle hello a été mis à jour avec un lien trop[quelle est la nouvelle rubrique](data-factory-gateway-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="7d731-322">When you launch Gateway Configuration Manager next time, you see a message on hello notification bar that hello gateway has been updated along with a link too[what's new topic](data-factory-gateway-release-notes.md).</span></span>

### <a name="toodisableenable-auto-update-feature"></a><span data-ttu-id="7d731-323">fonctionnalité de mise à jour automatique toodisable/activer</span><span class="sxs-lookup"><span data-stu-id="7d731-323">toodisable/enable auto-update feature</span></span>
<span data-ttu-id="7d731-324">Vous pouvez désactiver/activer fonction hello en procédant comme hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="7d731-324">You can disable/enable hello auto-update feature by doing hello following steps:</span></span>

<span data-ttu-id="7d731-325">[Pour une passerelle à nœud unique]</span><span class="sxs-lookup"><span data-stu-id="7d731-325">[For single node gateway]</span></span>
1. <span data-ttu-id="7d731-326">Lancez Windows PowerShell sur l’ordinateur de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-326">Launch Windows PowerShell on hello gateway machine.</span></span>
2. <span data-ttu-id="7d731-327">Basculez le dossier C:\Program Files\Microsoft données Gestion Gateway\2.0\PowerShellScript de toohello.</span><span class="sxs-lookup"><span data-stu-id="7d731-327">Switch toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="7d731-328">Exécution hello suivant commande tooturn hello-mise à jour automatique des fonctionnalités (désactiver).</span><span class="sxs-lookup"><span data-stu-id="7d731-328">Run hello following command tooturn hello auto-update feature OFF (disable).</span></span>   

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off
    ```
4. <span data-ttu-id="7d731-329">tooturn à nouveau sur :</span><span class="sxs-lookup"><span data-stu-id="7d731-329">tooturn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on  
    ```
<span data-ttu-id="7d731-330">[[Pour une passerelle hautement disponible et évolutive à plusieurs nœuds (version préliminaire)](data-factory-data-management-gateway-high-availability-scalability.md)]</span><span class="sxs-lookup"><span data-stu-id="7d731-330">[[For multi-node highly available and scalable gateway (preview)](data-factory-data-management-gateway-high-availability-scalability.md)]</span></span>
1. <span data-ttu-id="7d731-331">Lancez Windows PowerShell sur l’ordinateur de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-331">Launch Windows PowerShell on hello gateway machine.</span></span>
2. <span data-ttu-id="7d731-332">Basculez le dossier C:\Program Files\Microsoft données Gestion Gateway\2.0\PowerShellScript de toohello.</span><span class="sxs-lookup"><span data-stu-id="7d731-332">Switch toohello C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript folder.</span></span>
3. <span data-ttu-id="7d731-333">Exécution hello suivant commande tooturn hello-mise à jour automatique des fonctionnalités (désactiver).</span><span class="sxs-lookup"><span data-stu-id="7d731-333">Run hello following command tooturn hello auto-update feature OFF (disable).</span></span>   

    <span data-ttu-id="7d731-334">Pour une passerelle avec une fonctionnalité de haute disponibilité (version préliminaire), un paramètre AuthKey supplémentaire est requis.</span><span class="sxs-lookup"><span data-stu-id="7d731-334">For gateway with high availability feature (preview), an extra AuthKey param is required.</span></span>
    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -off -AuthKey <your auth key>
    ```
4. <span data-ttu-id="7d731-335">tooturn à nouveau sur :</span><span class="sxs-lookup"><span data-stu-id="7d731-335">tooturn it back on:</span></span>

    ```PowerShell
    .\GatewayAutoUpdateToggle.ps1  -on -AuthKey <your auth key> 


## Configuration Manager
Once you install hello gateway, you can launch Data Management Gateway Configuration Manager in one of hello following ways:

1. In hello **Search** window, type **Data Management Gateway** tooaccess this utility.
2. Run hello executable **ConfigManager.exe** in hello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\Shared**

### Home page
hello Home page allows you toodo hello following actions:

* View status of hello gateway (connected toohello cloud service etc.).
* **Register** using a key from hello portal.
* **Stop** and start hello **Data Management Gateway Host service** on hello gateway machine.
* **Schedule updates** at a specific time of hello days.
* View hello date when hello gateway was **last updated**.

### Settings page
hello Settings page allows you toodo hello following actions:

* View, change, and export **certificate** used by hello gateway. This certificate is used tooencrypt data source credentials.
* Change **HTTPS port** for hello endpoint. hello gateway opens a port for setting hello data source credentials.
* **Status** of hello endpoint
* View **SSL certificate** is used for SSL communication between portal and hello gateway tooset credentials for data sources.  

### Diagnostics page
hello Diagnostics page allows you toodo hello following actions:

* Enable verbose **logging**, view logs in event viewer, and send logs tooMicrosoft if there was a failure.
* **Test connection** tooa data source.  

### Help page
hello Help page displays hello following information:  

* Brief description of hello gateway
* Version number
* Links tooonline help, privacy statement, and license agreement.  

## Monitor gateway in hello portal
In hello Azure portal, you can view near-real time snapshot of resource utilization (CPU, memory, network(in/out), etc.) on a gateway machine.  

1. In Azure portal, navigate toohello home page for your data factory, and click **Linked services** tile. 

    ![Data factory home page](./media/data-factory-data-management-gateway/monitor-data-factory-home-page.png) 
2. Select hello **gateway** in hello **Linked services** page.

    ![Linked services page](./media/data-factory-data-management-gateway/monitor-linked-services-blade.png)
3. In hello **Gateway** page, you can see hello memory and CPU usage of hello gateway.

    ![CPU and memory usage of gateway](./media/data-factory-data-management-gateway/gateway-simple-monitoring.png) 
4. Enable **Advanced settings** toosee more details such as network usage.
    
    ![Advanced monitoring of gateway](./media/data-factory-data-management-gateway/gateway-advanced-monitoring.png)

hello following table provides descriptions of columns in hello **Gateway Nodes** list:  

Monitoring Property | Description
:------------------ | :---------- 
Name | Name of hello logical gateway and nodes associated with hello gateway. Node is an on-premises Windows machine that has hello gateway installed on it. For information on having more than one node (up toofour nodes) in a single logical gateway, see [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md).    
Status | Status of hello logical gateway and hello gateway nodes. Example: Online/Offline/Limited/etc. For information about these statuses, See [Gateway status](#gateway-status) section. 
Version | Shows hello version of hello logical gateway and each gateway node. hello version of hello logical gateway is determined based on version of majority of nodes in hello group. If there are nodes with different versions in hello logical gateway setup, only hello nodes with hello same version number as hello logical gateway function properly. Others are in hello limited mode and need toobe manually updated (only in case auto-update fails). 
Available memory | Available memory on a gateway node. This value is a near real-time snapshot. 
CPU utilization | CPU utilization of a gateway node. This value is a near real-time snapshot. 
Networking (In/Out) | Network utilization of a gateway node. This value is a near real-time snapshot. 
Concurrent Jobs (Running/ Limit) | Number of jobs or tasks running on each node. This value is a near real-time snapshot. Limit signifies hello maximum concurrent jobs for each node. This value is defined based on hello machine size. You can increase hello limit tooscale up concurrent job execution in advanced scenarios, where CPU/memory/network is under-utilized, but activities are timing out. This capability is also available with a single-node gateway (even when hello scalability and availability feature is not enabled).  
Role | There are two types of roles in a multi-node gateway – Dispatcher and worker. All nodes are workers, which means they can all be used tooexecute jobs. There is only one dispatcher node, which is used toopull tasks/jobs from cloud services and dispatch them toodifferent worker nodes (including itself).

In this page, you see some settings that make more sense when there are two or more nodes (scale out scenario) in hello gateway. See [Data Management Gateway - high availability and scalability](data-factory-data-management-gateway-high-availability-scalability.md) for details about setting up a multi-node gateway.

### Gateway status
hello following table provides possible statuses of a **gateway node**: 

Status  | Comments/Scenarios
:------- | :------------------
Online | Node connected tooData Factory service.
Offline | Node is offline.
Upgrading | hello node is being auto-updated.
Limited | Due tooConnectivity issue. May be due tooHTTP port 8050 issue, service bus connectivity issue, or credential sync issue. 
Inactive | Node is in a configuration different from hello configuration of other majority nodes.<br/><br/> A node can be inactive when it cannot connect tooother nodes. 


hello following table provides possible statuses of a **logical gateway**. hello gateway status depends on statuses of hello gateway nodes. 

Status | Comments
:----- | :-------
Needs Registration | No node is yet registered toothis logical gateway
Online | Gateway Nodes are online
Offline | No node in online status.
Limited | Not all nodes in this gateway are in healthy state. This status is a warning that some node might be down! <br/><br/>Could be due toocredential sync issue on dispatcher/worker node. 

## Scale up gateway
You can configure hello number of **concurrent data movement jobs** that can run on a node tooscale up hello capability of moving data between on-premises and cloud data stores. 

When hello available memory and CPU are not utilized well, but hello idle capacity is 0, you should scale up by increasing hello number of concurrent jobs that can run on a node. You may also want tooscale up when activities are timing out because hello gateway is overloaded. In hello advanced settings of a gateway node, you can increase hello maximum capacity for a node. 
  

## Troubleshooting gateway issues
See [Troubleshooting gateway issues](data-factory-troubleshoot-gateway-issues.md) article for information/tips for troubleshooting issues with using hello data management gateway.  

## Move gateway from one machine tooanother
This section provides steps for moving gateway client from one machine tooanother machine.

1. In hello portal, navigate toohello **Data Factory home page**, and click hello **Linked Services** tile.

    ![Data Gateways Link](./media/data-factory-data-management-gateway/DataGatewaysLink.png)
2. Select your gateway in hello **DATA GATEWAYS** section of hello **Linked Services** page.

    ![Linked Services page with gateway selected](./media/data-factory-data-management-gateway/LinkedServiceBladeWithGateway.png)
3. In hello **Data gateway** page, click **Download and install data gateway**.

    ![Download gateway link](./media/data-factory-data-management-gateway/DownloadGatewayLink.png)
4. In hello **Configure** page, click **Download and install data gateway**, and follow instructions tooinstall hello data gateway on hello machine.

    ![Configure page](./media/data-factory-data-management-gateway/ConfigureBlade.png)
5. Keep hello **Microsoft Data Management Gateway Configuration Manager** open.

    ![Configuration Manager](./media/data-factory-data-management-gateway/ConfigurationManager.png)    
6. In hello **Configure** page in hello portal, click **Recreate key** on hello command bar, and click **Yes** for hello warning message. Click **copy button** next tookey text that copies hello key toohello clipboard. hello gateway on hello old machine stops functioning as soon you recreate hello key.  

    ![Recreate key](./media/data-factory-data-management-gateway/RecreateKey.png)
7. Paste hello **key** into text box in hello **Register Gateway** page of hello **Data Management Gateway Configuration Manager** on your machine. (optional) Click **Show gateway key** check box toosee hello key text.

    ![Copy key and Register](./media/data-factory-data-management-gateway/CopyKeyAndRegister.png)
8. Click **Register** tooregister hello gateway with hello cloud service.
9. On hello **Settings** tab, click **Change** tooselect hello same certificate that was used with hello old gateway, enter hello **password**, and click **Finish**.

   ![Specify Certificate](./media/data-factory-data-management-gateway/SpecifyCertificate.png)

   You can export a certificate from hello old gateway by doing hello following steps: launch Data Management Gateway Configuration Manager on hello old machine, switch toohello **Certificate** tab, click **Export** button and follow hello instructions.
10. After successful registration of hello gateway, you should see hello **Registration** set too**Registered** and **Status** set too**Started** on hello Home page of hello Gateway Configuration Manager.

## Encrypting credentials
tooencrypt credentials in hello Data Factory Editor, do hello following steps:

1. Launch web browser on hello **gateway machine**, navigate too[Azure portal](http://portal.azure.com). Search for your data factory if needed, open data factory in hello **DATA FACTORY** page and then click **Author & Deploy** toolaunch Data Factory Editor.   
2. Click an existing **linked service** in hello tree view toosee its JSON definition or create a linked service that requires a data management gateway (for example: SQL Server or Oracle).
3. In hello JSON editor, for hello **gatewayName** property, enter hello name of hello gateway.
4. Enter server name for hello **Data Source** property in hello **connectionString**.
5. Enter database name for hello **Initial Catalog** property in hello **connectionString**.    
6. Click **Encrypt** button on hello command bar that launches hello click-once **Credential Manager** application. You should see hello **Setting Credentials** dialog box.

    ![Setting credentials dialog](./media/data-factory-data-management-gateway/setting-credentials-dialog.png)
7. In hello **Setting Credentials** dialog box, do hello following steps:
   1. Select **authentication** that you want hello Data Factory service toouse tooconnect toohello database.
   2. Enter name of hello user who has access toohello database for hello **USERNAME** setting.
   3. Enter password for hello user for hello **PASSWORD** setting.  
   4. Click **OK** tooencrypt credentials and close hello dialog box.
8. You should see a **encryptedCredential** property in hello **connectionString** now.

    ```JSON
    {
        "name": "SqlServerLinkedService",
        "properties": {
            "type": "OnPremisesSqlServer",
            "description": "",
            "typeProperties": {
                "connectionString": "data source=myserver;initial catalog=mydatabase;Integrated Security=False;EncryptedCredential=eyJDb25uZWN0aW9uU3R",
                "gatewayName": "adftutorialgateway"
            }
        }
    }
    ```
<span data-ttu-id="7d731-336">Si vous accédez à portal de hello à partir d’un ordinateur différent de l’ordinateur de passerelle hello, il se peut que vous devez vous assurer que les applications du Gestionnaire d’informations d’identification hello peuvent se connecter toohello machine de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="7d731-336">If you access hello portal from a machine that is different from hello gateway machine, you must make sure that hello Credentials Manager application can connect toohello gateway machine.</span></span> <span data-ttu-id="7d731-337">Si l’application hello ne peut pas atteindre l’ordinateur de passerelle hello, il ne vous permet pas tooset les informations d’identification pour la source de données hello et la source de données toohello tootest connexion.</span><span class="sxs-lookup"><span data-stu-id="7d731-337">If hello application cannot reach hello gateway machine, it does not allow you tooset credentials for hello data source and tootest connection toohello data source.</span></span>  

<span data-ttu-id="7d731-338">Lorsque vous utilisez hello **informations d’identification du paramètre** , application de portail de hello chiffre les informations d’identification de l’hello avec certificat hello spécifié dans hello **certificat** onglet Hello **passerelle Gestionnaire de configuration** sur l’ordinateur de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-338">When you use hello **Setting Credentials** application, hello portal encrypts hello credentials with hello certificate specified in hello **Certificate** tab of hello **Gateway Configuration Manager** on hello gateway machine.</span></span>

<span data-ttu-id="7d731-339">Si vous recherchez une approche basée sur les API pour le chiffrement des informations d’identification hello, vous pouvez utiliser hello [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) informations d’identification de tooencrypt d’applet de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7d731-339">If you are looking for an API-based approach for encrypting hello credentials, you can use hello [New-AzureRmDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) PowerShell cmdlet tooencrypt credentials.</span></span> <span data-ttu-id="7d731-340">applet de commande Hello utilise un certificat hello que cette passerelle est configurée toouse tooencrypt hello références.</span><span class="sxs-lookup"><span data-stu-id="7d731-340">hello cmdlet uses hello certificate that gateway is configured toouse tooencrypt hello credentials.</span></span> <span data-ttu-id="7d731-341">Vous ajoutez des informations d’identification chiffrées toohello **EncryptedCredential** élément Hello **connectionString** Bonjour JSON.</span><span class="sxs-lookup"><span data-stu-id="7d731-341">You add encrypted credentials toohello **EncryptedCredential** element of hello **connectionString** in hello JSON.</span></span> <span data-ttu-id="7d731-342">Vous utilisez hello JSON avec hello [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) applet de commande ou Bonjour éditeur Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7d731-342">You use hello JSON with hello [New-AzureRmDataFactoryLinkedService](https://msdn.microsoft.com/library/mt603647.aspx) cmdlet or in hello Data Factory Editor.</span></span>

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

<span data-ttu-id="7d731-343">Il existe une autre approche pour définir les informations d’identification à l’aide de Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="7d731-343">There is one more approach for setting credentials using Data Factory Editor.</span></span> <span data-ttu-id="7d731-344">Si vous créez un serveur SQL Server lié service à l’aide de l’éditeur hello et que vous entrez des informations d’identification en texte brut, les informations d’identification hello sont chiffrées à l’aide d’un certificat qui est propriétaire de service de fabrique de données hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-344">If you create a SQL Server linked service by using hello editor and you enter credentials in plain text, hello credentials are encrypted using a certificate that hello Data Factory service owns.</span></span> <span data-ttu-id="7d731-345">Il n’utilise pas de certificat hello que cette passerelle est toouse configuré.</span><span class="sxs-lookup"><span data-stu-id="7d731-345">It does NOT use hello certificate that gateway is configured toouse.</span></span> <span data-ttu-id="7d731-346">Bien que cette approche puisse être un peu plus rapide dans certains cas, elle reste moins sécurisée.</span><span class="sxs-lookup"><span data-stu-id="7d731-346">While this approach might be a little faster in some cases, it is less secure.</span></span> <span data-ttu-id="7d731-347">Par conséquent, nous vous recommandons de suivre cette approche uniquement à des fins de développement/test.</span><span class="sxs-lookup"><span data-stu-id="7d731-347">Therefore, we recommend that you follow this approach only for development/testing purposes.</span></span>

## <a name="powershell-cmdlets"></a><span data-ttu-id="7d731-348">Applets de commande PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d731-348">PowerShell cmdlets</span></span>
<span data-ttu-id="7d731-349">Cette section décrit comment toocreate et inscrire une passerelle à l’aide des applets de commande PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="7d731-349">This section describes how toocreate and register a gateway using Azure PowerShell cmdlets.</span></span>

1. <span data-ttu-id="7d731-350">Lancez **Azure PowerShell** en mode administrateur.</span><span class="sxs-lookup"><span data-stu-id="7d731-350">Launch **Azure PowerShell** in administrator mode.</span></span>
2. <span data-ttu-id="7d731-351">Connectez-vous à tooyour compte Azure en exécutant hello suivant de commande et entrez vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="7d731-351">Log in tooyour Azure account by running hello following command and entering your Azure credentials.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="7d731-352">Hello d’utilisation **New-AzureRmDataFactoryGateway** toocreate de l’applet de commande une passerelle logique comme suit :</span><span class="sxs-lookup"><span data-stu-id="7d731-352">Use hello **New-AzureRmDataFactoryGateway** cmdlet toocreate a logical gateway as follows:</span></span>

    ```PowerShell
    $MyDMG = New-AzureRmDataFactoryGateway -Name <gatewayName> -DataFactoryName <dataFactoryName> -ResourceGroupName ADF –Description <desc>
    ```
    <span data-ttu-id="7d731-353">**Exemple de commande et de sortie**:</span><span class="sxs-lookup"><span data-stu-id="7d731-353">**Example command and output**:</span></span>

    ```
    PS C:\> $MyDMG = New-AzureRmDataFactoryGateway -Name MyGateway -DataFactoryName $df -ResourceGroupName ADF –Description “gateway for walkthrough”

    Name              : MyGateway
    Description       : gateway for walkthrough
    Version           :
    Status            : NeedRegistration
    VersionStatus     : None
    CreateTime        : 9/28/2014 10:58:22
    RegisterTime      :
    LastConnectTime   :
    ExpiryTime        :
    ProvisioningState : Succeeded
    Key               : ADF#00000000-0000-4fb8-a867-947877aef6cb@fda06d87-f446-43b1-9485-78af26b8bab0@4707262b-dc25-4fe5-881c-c8a7c3c569fe@wu#nfU4aBlq/heRyYFZ2Xt/CD+7i73PEO521Sj2AFOCmiI
    ```

1. <span data-ttu-id="7d731-354">Dans Azure PowerShell, basculez toohello dossier : **C:\Program Files\Microsoft données Gestion Gateway\2.0\PowerShellScript\**.</span><span class="sxs-lookup"><span data-stu-id="7d731-354">In Azure PowerShell, switch toohello folder: **C:\Program Files\Microsoft Data Management Gateway\2.0\PowerShellScript\**.</span></span> <span data-ttu-id="7d731-355">Exécutez **RegisterGateway.ps1** liées à la variable locale de hello **$Key** comme indiqué dans hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="7d731-355">Run **RegisterGateway.ps1** associated with hello local variable **$Key** as shown in hello following command.</span></span> <span data-ttu-id="7d731-356">Ce script enregistre l’agent du client hello installé sur votre ordinateur avec la passerelle logique de hello que vous créez précédemment.</span><span class="sxs-lookup"><span data-stu-id="7d731-356">This script registers hello client agent installed on your machine with hello logical gateway you create earlier.</span></span>

    ```PowerShell
    PS C:\> .\RegisterGateway.ps1 $MyDMG.Key
    ```
    ```
    Agent registration is successful!
    ```
    <span data-ttu-id="7d731-357">Vous pouvez inscrire la passerelle hello sur un ordinateur distant à l’aide du paramètre de IsRegisterOnRemoteMachine hello.</span><span class="sxs-lookup"><span data-stu-id="7d731-357">You can register hello gateway on a remote machine by using hello IsRegisterOnRemoteMachine parameter.</span></span> <span data-ttu-id="7d731-358">Exemple :</span><span class="sxs-lookup"><span data-stu-id="7d731-358">Example:</span></span>

    ```PowerShell
    .\RegisterGateway.ps1 $MyDMG.Key -IsRegisterOnRemoteMachine true
    ```
2. <span data-ttu-id="7d731-359">Vous pouvez utiliser hello **Get-AzureRmDataFactoryGateway** liste de hello tooget applet de commande de passerelles dans votre fabrique de données.</span><span class="sxs-lookup"><span data-stu-id="7d731-359">You can use hello **Get-AzureRmDataFactoryGateway** cmdlet tooget hello list of Gateways in your data factory.</span></span> <span data-ttu-id="7d731-360">Hello lorsque **état** montre **online**, cela signifie que votre passerelle est toouse prêt.</span><span class="sxs-lookup"><span data-stu-id="7d731-360">When hello **Status** shows **online**, it means your gateway is ready toouse.</span></span>

    ```PowerShell        
    Get-AzureRmDataFactoryGateway -DataFactoryName <dataFactoryName> -ResourceGroupName ADF
    ```
<span data-ttu-id="7d731-361">Vous pouvez supprimer une passerelle à l’aide de hello **Remove-AzureRmDataFactoryGateway** applet de commande et de mise à jour la description d’une passerelle à l’aide de hello **Set-AzureRmDataFactoryGateway** applets de commande.</span><span class="sxs-lookup"><span data-stu-id="7d731-361">You can remove a gateway using hello **Remove-AzureRmDataFactoryGateway** cmdlet and update description for a gateway using hello **Set-AzureRmDataFactoryGateway** cmdlets.</span></span> <span data-ttu-id="7d731-362">Pour obtenir la syntaxe et d’autres détails sur ces applets de commande, consultez la rubrique Référence des applets de commande Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="7d731-362">For syntax and other details about these cmdlets, see Data Factory Cmdlet Reference.</span></span>  

### <a name="list-gateways-using-powershell"></a><span data-ttu-id="7d731-363">Répertorier les passerelles à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d731-363">List gateways using PowerShell</span></span>

```PowerShell
Get-AzureRmDataFactoryGateway -DataFactoryName jasoncopyusingstoredprocedure -ResourceGroupName ADF_ResourceGroup
```

### <a name="remove-gateway-using-powershell"></a><span data-ttu-id="7d731-364">Supprimer une passerelle à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="7d731-364">Remove gateway using PowerShell</span></span>

```PowerShell
Remove-AzureRmDataFactoryGateway -Name JasonHDMG_byPSRemote -ResourceGroupName ADF_ResourceGroup -DataFactoryName jasoncopyusingstoredprocedure -Force
```


## <a name="next-steps"></a><span data-ttu-id="7d731-365">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7d731-365">Next steps</span></span>
* <span data-ttu-id="7d731-366">Consultez la page [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="7d731-366">See [Move data between on-premises and cloud data stores](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="7d731-367">Hello procédure pas à pas, vous créez un pipeline qui utilise des données de toomove hello passerelle à partir d’un tooan de base de données SQL Server locale blob Azure.</span><span class="sxs-lookup"><span data-stu-id="7d731-367">In hello walkthrough, you create a pipeline that uses hello gateway toomove data from an on-premises SQL Server database tooan Azure blob.</span></span>  
