---
title: "Activer l'affinité de session à l'aide du kit de ressources Azure pour Eclipse"
description: "Découvrez comment activer l'affinité de session à l'aide du kit de ressources Azure pour Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 88c595ec-7d85-40bd-9078-8d6be7b3f0fa
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: ab8623d6f9751ed6d71d9a5b1c0d5e939c442862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="4d61d-103">Activer l'affinité de session</span><span class="sxs-lookup"><span data-stu-id="4d61d-103">Enable Session Affinity</span></span>
<span data-ttu-id="4d61d-104">Dans le Kit de ressources Azure pour Eclipse, vous pouvez activer l'affinité de session HTTP, ou « sessions temporaires », pour vos rôles.</span><span class="sxs-lookup"><span data-stu-id="4d61d-104">Within the Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="4d61d-105">L'illustration suivante montre la boîte de dialogue des propriétés de **l'équilibrage de charge** utilisé pour activer la fonctionnalité d'affinité de session :</span><span class="sxs-lookup"><span data-stu-id="4d61d-105">The following image shows the **Load Balancing** properties dialog used to enable the session affinity feature:</span></span>

![][ic719492]

## <a name="to-enable-session-affinity-for-your-role"></a><span data-ttu-id="4d61d-106">Pour activer l'affinité de session pour votre rôle</span><span class="sxs-lookup"><span data-stu-id="4d61d-106">To enable session affinity for your role</span></span>
1. <span data-ttu-id="4d61d-107">Cliquez avec le bouton droit sur le rôle dans l’Explorateur de projet Eclipse, cliquez sur **Azure**, puis sur **Équilibrage de charge**.</span><span class="sxs-lookup"><span data-stu-id="4d61d-107">Right-click the role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="4d61d-108">Dans la boîte de dialogue **Propriétés d'équilibrage de charge pour WorkerRole1** :</span><span class="sxs-lookup"><span data-stu-id="4d61d-108">In the **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="4d61d-109">a.</span><span class="sxs-lookup"><span data-stu-id="4d61d-109">a.</span></span> <span data-ttu-id="4d61d-110">Cochez **Activer l'affinité de session HTTP (sessions temporaires) pour ce rôle.**</span><span class="sxs-lookup"><span data-stu-id="4d61d-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="4d61d-111">b.</span><span class="sxs-lookup"><span data-stu-id="4d61d-111">b.</span></span> <span data-ttu-id="4d61d-112">Pour le **point de terminaison d’entrée à utiliser**, sélectionnez un point de terminaison d’entrée à utiliser, par exemple, **http (public:80, private:8080)**.</span><span class="sxs-lookup"><span data-stu-id="4d61d-112">For **Input endpoint to use**, select an input endpoint to use, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="4d61d-113">Votre application doit utiliser ce point de terminaison en tant que point de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="4d61d-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="4d61d-114">Vous pouvez activer plusieurs points de terminaison pour votre rôle, mais vous ne pouvez en sélectionner qu'un seul pour prendre en charge des sessions temporaires.</span><span class="sxs-lookup"><span data-stu-id="4d61d-114">You can enable multiple endpoints for your role, but you can select only one of them to support sticky sessions.</span></span>

   <span data-ttu-id="4d61d-115">c.</span><span class="sxs-lookup"><span data-stu-id="4d61d-115">c.</span></span> <span data-ttu-id="4d61d-116">Régénérez votre application.</span><span class="sxs-lookup"><span data-stu-id="4d61d-116">Rebuild your application.</span></span>

<span data-ttu-id="4d61d-117">Après l'activation, si vous avez plusieurs instances de rôle, les requêtes HTTP provenant d'un client particulier continueront d'être gérées par la même instance de rôle.</span><span class="sxs-lookup"><span data-stu-id="4d61d-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by the same role instance.</span></span>

<span data-ttu-id="4d61d-118">Le Kit de ressources Eclipse le permet en installant un module IIS spécial appelé Application Request Routing (ARR) dans chacune de vos instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="4d61d-118">The Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="4d61d-119">ARR redirige les requêtes HTTP vers l'instance de rôle appropriée.</span><span class="sxs-lookup"><span data-stu-id="4d61d-119">ARR reroutes HTTP requests to the appropriate role instance.</span></span> <span data-ttu-id="4d61d-120">Le kit de ressources reconfigure automatiquement le point de terminaison sélectionné afin que le trafic HTTP entrant soit tout d'abord dirigé vers le logiciel ARR.</span><span class="sxs-lookup"><span data-stu-id="4d61d-120">The toolkit automatically reconfigures the selected endpoint so that the incoming HTTP traffic is first routed to the ARR software.</span></span> <span data-ttu-id="4d61d-121">Le kit de ressources crée également un nouveau point de terminaison interne que votre serveur Java est configuré pour écouter.</span><span class="sxs-lookup"><span data-stu-id="4d61d-121">The toolkit also creates a new internal endpoint that your Java server is configured to listen to.</span></span> <span data-ttu-id="4d61d-122">C'est le point de terminaison utilisé par ARR pour rediriger le trafic HTTP vers l'instance de rôle appropriée.</span><span class="sxs-lookup"><span data-stu-id="4d61d-122">That is the endpoint used by ARR to reroute the HTTP traffic to the appropriate role instance.</span></span> <span data-ttu-id="4d61d-123">De cette façon, chaque instance de rôle dans votre déploiement multi-instance sert de proxy inverse pour toutes les autres instances, activant ainsi les sessions temporaires.</span><span class="sxs-lookup"><span data-stu-id="4d61d-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all the other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="4d61d-124">Remarques sur l'affinité de session</span><span class="sxs-lookup"><span data-stu-id="4d61d-124">Notes about session affinity</span></span>
* <span data-ttu-id="4d61d-125">L'affinité de session ne fonctionne pas dans l'émulateur de calcul.</span><span class="sxs-lookup"><span data-stu-id="4d61d-125">Session affinity does not work in the compute emulator.</span></span> <span data-ttu-id="4d61d-126">Les paramètres peuvent être appliqués dans l'émulateur de calcul sans interférer avec votre processus de génération ou d'exécution de l'émulateur de calcul, mais la fonction elle-même ne fonctionne pas dans l'émulateur de calcul.</span><span class="sxs-lookup"><span data-stu-id="4d61d-126">The settings can be applied in the compute emulator without interfering with your build process or compute emulator execution, but the feature itself does not function within the compute emulator.</span></span>

* <span data-ttu-id="4d61d-127">L'activation de l'affinité de session entraîne une augmentation de la quantité d'espace disque pris par votre déploiement dans Azure, car des logiciels supplémentaires seront téléchargés et installés dans vos instances de rôle lorsque votre service est démarré dans le cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="4d61d-127">Enabling session affinity will result in an increase in the amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in the Azure cloud.</span></span>

* <span data-ttu-id="4d61d-128">Le temps d'initialisation de chaque rôle sera plus long.</span><span class="sxs-lookup"><span data-stu-id="4d61d-128">The time to initialize each role will take longer.</span></span>

* <span data-ttu-id="4d61d-129">Un point de terminaison interne, servant de dispositif de redirection de trafic comme indiqué ci-dessus, est ajouté.</span><span class="sxs-lookup"><span data-stu-id="4d61d-129">An internal endpoint, to function as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="4d61d-130">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4d61d-130">See Also</span></span>
<span data-ttu-id="4d61d-131">[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4d61d-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="4d61d-132">[Création d’une application Hello World pour Azure dans Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4d61d-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="4d61d-133">[Installation du kit de ressources Azure pour Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="4d61d-133">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="4d61d-134">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez le [Centre de développement Java pour Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="4d61d-134">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How to Maintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
