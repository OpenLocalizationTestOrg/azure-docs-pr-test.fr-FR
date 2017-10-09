---
title: "à l’aide de l’affinité de Session aaaEnable hello boîte à outils Azure pour Eclipse"
description: "Découvrez comment l’affinité de session tooenable à l’aide hello boîte à outils Azure pour Eclipse."
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
ms.openlocfilehash: 523e728c58bda95e7af4b242e831694eb6d75cb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-session-affinity"></a><span data-ttu-id="607a2-103">Activer l'affinité de session</span><span class="sxs-lookup"><span data-stu-id="607a2-103">Enable Session Affinity</span></span>
<span data-ttu-id="607a2-104">Dans la boîte à outils Azure pour Eclipse de hello, vous pouvez activer l’affinité de session HTTP, ou « sessions rémanentes » pour vos rôles.</span><span class="sxs-lookup"><span data-stu-id="607a2-104">Within hello Azure Toolkit for Eclipse, you can enable HTTP session affinity, or "sticky sessions", for your roles.</span></span> <span data-ttu-id="607a2-105">Hello image suivante montre hello **l’équilibrage de charge** fonctionnalité d’affinité de propriétés boîte de dialogue utilisée tooenable hello session :</span><span class="sxs-lookup"><span data-stu-id="607a2-105">hello following image shows hello **Load Balancing** properties dialog used tooenable hello session affinity feature:</span></span>

![][ic719492]

## <a name="tooenable-session-affinity-for-your-role"></a><span data-ttu-id="607a2-106">affinité de session tooenable pour votre rôle.</span><span class="sxs-lookup"><span data-stu-id="607a2-106">tooenable session affinity for your role</span></span>
1. <span data-ttu-id="607a2-107">Sur le rôle hello dans l’Explorateur de projets d’Eclipse, cliquez **Azure**, puis cliquez sur **l’équilibrage de charge**.</span><span class="sxs-lookup"><span data-stu-id="607a2-107">Right-click hello role in Eclipse's Project Explorer, click **Azure**, and then click **Load Balancing**.</span></span>

2. <span data-ttu-id="607a2-108">Bonjour **propriétés de l’équilibrage de charge WorkerRole1** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="607a2-108">In hello **Properties for WorkerRole1 Load Balancing** dialog:</span></span>

   <span data-ttu-id="607a2-109">a.</span><span class="sxs-lookup"><span data-stu-id="607a2-109">a.</span></span> <span data-ttu-id="607a2-110">Cochez **Activer l'affinité de session HTTP (sessions temporaires) pour ce rôle.**</span><span class="sxs-lookup"><span data-stu-id="607a2-110">Check **Enable HTTP session affinity (sticky sessions) for this role.**</span></span>

   <span data-ttu-id="607a2-111">b.</span><span class="sxs-lookup"><span data-stu-id="607a2-111">b.</span></span> <span data-ttu-id="607a2-112">Pour **d’entrée de point de terminaison toouse**, sélectionnez un point de terminaison d’entrée toouse, par exemple, **http (public : 80, privé : 8080)**.</span><span class="sxs-lookup"><span data-stu-id="607a2-112">For **Input endpoint toouse**, select an input endpoint toouse, for example, **http (public:80, private:8080)**.</span></span> <span data-ttu-id="607a2-113">Votre application doit utiliser ce point de terminaison en tant que point de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="607a2-113">Your application must use this endpoint as its HTTP endpoint.</span></span> <span data-ttu-id="607a2-114">Vous pouvez activer plusieurs points de terminaison pour votre rôle, mais vous pouvez sélectionner qu’un seul d'entre eux toosupport sessions rémanentes.</span><span class="sxs-lookup"><span data-stu-id="607a2-114">You can enable multiple endpoints for your role, but you can select only one of them toosupport sticky sessions.</span></span>

   <span data-ttu-id="607a2-115">c.</span><span class="sxs-lookup"><span data-stu-id="607a2-115">c.</span></span> <span data-ttu-id="607a2-116">Régénérez votre application.</span><span class="sxs-lookup"><span data-stu-id="607a2-116">Rebuild your application.</span></span>

<span data-ttu-id="607a2-117">Une fois activée, si vous avez plusieurs instances de rôle, les demandes HTTP provenant d’un client particulier continuera gérées par hello même instance de rôle.</span><span class="sxs-lookup"><span data-stu-id="607a2-117">Once enabled, if you have more than one role instance, HTTP requests coming from a particular client will continue being handled by hello same role instance.</span></span>

<span data-ttu-id="607a2-118">Hello boîte à outils Eclipse permet cela en installant un module IIS spécial appelé Application Request Routing (ARR) dans chacune de vos instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="607a2-118">hello Eclipse Toolkit enables this by installing a special IIS module called Application Request Routing (ARR) into each of your role instances.</span></span> <span data-ttu-id="607a2-119">ARR redirige l’instance de rôle appropriée de toohello de demandes HTTP.</span><span class="sxs-lookup"><span data-stu-id="607a2-119">ARR reroutes HTTP requests toohello appropriate role instance.</span></span> <span data-ttu-id="607a2-120">Hello toolkit reconfigure automatiquement le point de terminaison hello sélectionné afin que le trafic HTTP entrant de hello est premier toohello routé ARR logiciel.</span><span class="sxs-lookup"><span data-stu-id="607a2-120">hello toolkit automatically reconfigures hello selected endpoint so that hello incoming HTTP traffic is first routed toohello ARR software.</span></span> <span data-ttu-id="607a2-121">boîte à outils Hello crée également un nouveau point de terminaison interne votre serveur Java est configuré toolisten à.</span><span class="sxs-lookup"><span data-stu-id="607a2-121">hello toolkit also creates a new internal endpoint that your Java server is configured toolisten to.</span></span> <span data-ttu-id="607a2-122">Qui est le point de terminaison hello utilisé par instance de rôle appropriée toohello le trafic HTTP de ARR tooreroute hello.</span><span class="sxs-lookup"><span data-stu-id="607a2-122">That is hello endpoint used by ARR tooreroute hello HTTP traffic toohello appropriate role instance.</span></span> <span data-ttu-id="607a2-123">De cette manière, chaque instance de rôle dans votre déploiement multi-instance sert de proxy inverse pour toutes les hello autres instances, en activant des sessions rémanentes.</span><span class="sxs-lookup"><span data-stu-id="607a2-123">This way, each role instance in your multi-instance deployment serves as a reverse proxy for all hello other instances, enabling sticky sessions.</span></span>

## <a name="notes-about-session-affinity"></a><span data-ttu-id="607a2-124">Remarques sur l'affinité de session</span><span class="sxs-lookup"><span data-stu-id="607a2-124">Notes about session affinity</span></span>
* <span data-ttu-id="607a2-125">Affinité de session ne fonctionne pas dans l’émulateur de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="607a2-125">Session affinity does not work in hello compute emulator.</span></span> <span data-ttu-id="607a2-126">Hello paramètres peuvent être appliquées dans l’émulateur de calcul hello sans interférer avec votre processus de génération ou de l’exécution de l’émulateur de calcul, mais la fonction hello elle-même ne fonctionne pas dans l’émulateur de calcul hello.</span><span class="sxs-lookup"><span data-stu-id="607a2-126">hello settings can be applied in hello compute emulator without interfering with your build process or compute emulator execution, but hello feature itself does not function within hello compute emulator.</span></span>

* <span data-ttu-id="607a2-127">L’activation de l’affinité de session entraîne une augmentation de la quantité hello d’espace disque pris en charge par votre déploiement dans Azure, comme des logiciels supplémentaires seront téléchargés et installés dans vos instances de rôle lorsque votre service est démarré en hello cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="607a2-127">Enabling session affinity will result in an increase in hello amount of disk space taken up by your deployment in Azure, as additional software will be downloaded and installed into your role instances when your service is started in hello Azure cloud.</span></span>

* <span data-ttu-id="607a2-128">Hello temps tooinitialize chaque rôle prend plus de temps.</span><span class="sxs-lookup"><span data-stu-id="607a2-128">hello time tooinitialize each role will take longer.</span></span>

* <span data-ttu-id="607a2-129">Un point de terminaison interne, toofunction comme un RE-routeur de trafic comme indiqué ci-dessus, est ajouté.</span><span class="sxs-lookup"><span data-stu-id="607a2-129">An internal endpoint, toofunction as a traffic rerouter as mentioned above, will be added.</span></span>


## <a name="see-also"></a><span data-ttu-id="607a2-130">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="607a2-130">See Also</span></span>
<span data-ttu-id="607a2-131">[Kit de ressources Azure pour Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="607a2-131">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="607a2-132">[Création d’une application Hello World pour Azure dans Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="607a2-132">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="607a2-133">[Lors de l’installation hello boîte à outils Azure pour Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="607a2-133">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="607a2-134">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez hello [centre de développement Java Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="607a2-134">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[How tooMaintain Session Data with Session Affinity]: http://go.microsoft.com/fwlink/?LinkID=699539
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic719492]: ./media/azure-toolkit-for-eclipse-enable-session-affinity/ic719492.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690950.aspx -->
