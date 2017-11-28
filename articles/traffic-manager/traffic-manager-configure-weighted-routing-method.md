---
title: "méthode de routage à l’aide de Azure Traffic Manager alternée aaaConfigure pondérée du trafic | Documents Microsoft"
description: "Cet article explique comment tooload équilibrer le trafic à l’aide d’une méthode du tourniquet dans Traffic Manager"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: 7e2866ead0b2b653845435dd420a763c5e175f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-weighted-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="92d9f-103">Configurer les méthode de routage de trafic hello pondérée dans Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="92d9f-103">Configure hello weighted traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="92d9f-104">Un modèle commun méthode de routage du trafic est tooprovide un ensemble de points de terminaison identiques, qui incluent des services de cloud computing et sites Web et envoyer le trafic tooeach de manière alternée.</span><span class="sxs-lookup"><span data-stu-id="92d9f-104">A common traffic routing method pattern is tooprovide a set of identical endpoints, which include cloud services and websites, and send traffic tooeach in a round-robin fashion.</span></span> <span data-ttu-id="92d9f-105">Hello suit montrer comment tooconfigure ce type de méthode de routage du trafic.</span><span class="sxs-lookup"><span data-stu-id="92d9f-105">hello following steps outline how tooconfigure this type of traffic routing method.</span></span>

> [!NOTE]
> <span data-ttu-id="92d9f-106">Azure Websites fournit déjà des fonctionnalités d’équilibrage de charge de tourniquet pour les sites web dans un centre de données (également appelé région).</span><span class="sxs-lookup"><span data-stu-id="92d9f-106">Azure Websites already provide round-robin load balancing functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="92d9f-107">Traffic Manager vous permet de méthode de routage du trafic de tourniquet toospecify pour les sites Web dans différents centres de données.</span><span class="sxs-lookup"><span data-stu-id="92d9f-107">Traffic Manager allows you toospecify round-robin traffic routing method for websites in different datacenters.</span></span>

## <a name="tooconfigure-hello-weighted-traffic-routing-method"></a><span data-ttu-id="92d9f-108">méthode de routage du trafic tooconfigure hello pondérée</span><span class="sxs-lookup"><span data-stu-id="92d9f-108">tooconfigure hello weighted traffic routing method</span></span>

1. <span data-ttu-id="92d9f-109">À partir d’un navigateur, connectez-vous toohello [portail Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="92d9f-109">From a browser, sign in toohello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="92d9f-110">Si vous ne possédez pas encore de compte, vous pouvez [vous inscrire pour bénéficier d’un essai gratuit d’un mois](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="92d9f-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="92d9f-111">Dans la barre de recherche du portail hello, recherchez hello **profils Traffic Manager** puis cliquez sur nom du profil hello tooconfigure méthode de routage hello pour souhaitées.</span><span class="sxs-lookup"><span data-stu-id="92d9f-111">In hello portal’s search bar, search for hello **Traffic Manager profiles** and then click hello profile name that you want tooconfigure hello routing method for.</span></span>
3. <span data-ttu-id="92d9f-112">Bonjour **profil Traffic Manager** panneau, vérifiez que les deux hello services de cloud computing et sites Web que vous souhaitez tooinclude dans votre configuration sont présents.</span><span class="sxs-lookup"><span data-stu-id="92d9f-112">In hello **Traffic Manager profile** blade, verify that both hello cloud services and websites that you want tooinclude in your configuration are present.</span></span>
4. <span data-ttu-id="92d9f-113">Bonjour **paramètres** , cliquez sur **Configuration**et Bonjour **Configuration** panneau, terminée, comme suit :</span><span class="sxs-lookup"><span data-stu-id="92d9f-113">In hello **Settings** section, click **Configuration**, and in hello **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="92d9f-114">Pour **paramètres de méthode de routage du trafic**, vérifiez que la méthode de routage du trafic hello est **Weighted**.</span><span class="sxs-lookup"><span data-stu-id="92d9f-114">For **traffic routing method settings**, verify that hello traffic routing method is **Weighted**.</span></span> <span data-ttu-id="92d9f-115">Si elle n’est pas le cas, cliquez sur **Weighted** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="92d9f-115">If it is not, click **Weighted** from hello dropdown list.</span></span>
    2. <span data-ttu-id="92d9f-116">Ensemble hello **paramètres du moniteur de point de terminaison** identiques pour tous les chaque point de terminaison dans ce profil comme suit :</span><span class="sxs-lookup"><span data-stu-id="92d9f-116">Set hello **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="92d9f-117">Sélectionnez hello approprié **protocole**et spécifiez hello **Port** nombre.</span><span class="sxs-lookup"><span data-stu-id="92d9f-117">Select hello appropriate **Protocol**, and specify hello **Port** number.</span></span> 
        2. <span data-ttu-id="92d9f-118">Pour **Chemin d’accès**, entrez une barre oblique */*.</span><span class="sxs-lookup"><span data-stu-id="92d9f-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="92d9f-119">points de terminaison toomonitor, vous devez spécifier un chemin d’accès et le nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="92d9f-119">toomonitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="92d9f-120">Une barre oblique « / » est une entrée valide pour le chemin d’accès relatif de hello et implique que le fichier hello se trouve dans le répertoire racine de hello (par défaut).</span><span class="sxs-lookup"><span data-stu-id="92d9f-120">A forward slash "/" is a valid entry for hello relative path and implies that hello file is in hello root directory (default).</span></span>
        3. <span data-ttu-id="92d9f-121">En hello haut hello, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="92d9f-121">At hello top of hello page, click **Save**.</span></span>
5. <span data-ttu-id="92d9f-122">Testez les modifications hello dans votre configuration comme suit :</span><span class="sxs-lookup"><span data-stu-id="92d9f-122">Test hello changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="92d9f-123">Dans la barre de recherche du portail hello, recherchez le nom du profil Traffic Manager hello et cliquez sur le profil Traffic Manager hello dans les résultats de hello que hello affiché.</span><span class="sxs-lookup"><span data-stu-id="92d9f-123">In hello portal’s search bar, search for hello Traffic Manager profile name and click hello Traffic Manager profile in hello results that hello displayed.</span></span>
    2.  <span data-ttu-id="92d9f-124">Bonjour **Traffic Manager** panneau, cliquez sur **vue d’ensemble**.</span><span class="sxs-lookup"><span data-stu-id="92d9f-124">In hello **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="92d9f-125">Hello **profil Traffic Manager** panneau affiche le nom DNS de hello de votre profil Traffic Manager nouvellement créé.</span><span class="sxs-lookup"><span data-stu-id="92d9f-125">hello **Traffic Manager profile** blade displays hello DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="92d9f-126">Cela peut servir par les clients (par exemple, en accédant à l’aide d’un navigateur web de tooit) tooget routé toohello droite point de terminaison tel que déterminé par le type de routage hello.</span><span class="sxs-lookup"><span data-stu-id="92d9f-126">This can be used by any clients (for example,by navigating tooit using a web browser) tooget routed toohello right endpoint as determined by hello routing type.</span></span> <span data-ttu-id="92d9f-127">Dans ce cas, toutes les demandes sont routées vers chaque point de terminaison de manière alternée.</span><span class="sxs-lookup"><span data-stu-id="92d9f-127">In this case all requests are routed each endpoint in a round-robin fashion.</span></span>
6. <span data-ttu-id="92d9f-128">Une fois que votre profil Traffic Manager fonctionne, vous pouvez modifier enregistrement DNS de hello sur votre toopoint de serveur DNS faisant autorité votre nom de domaine de société domaine nom toohello Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="92d9f-128">Once your Traffic Manager profile is working, edit hello DNS record on your authoritative DNS server toopoint your company domain name toohello Traffic Manager domain name.</span></span>

![Configuration de la méthode de routage du trafic par pondération à l’aide de Traffic Manager][1]

## <a name="next-steps"></a><span data-ttu-id="92d9f-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="92d9f-130">Next steps</span></span>

- <span data-ttu-id="92d9f-131">En savoir plus sur la [méthode de routage du trafic prioritaire](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="92d9f-131">Learn about [priority traffic routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="92d9f-132">En savoir plus sur la [méthode de routage du trafic basé sur les performances](traffic-manager-configure-performance-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="92d9f-132">Learn about [performance traffic routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="92d9f-133">En savoir plus sur la [méthode de routage géographique](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="92d9f-133">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="92d9f-134">Découvrez comment trop[tester les paramètres de Traffic Manager](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="92d9f-134">Learn how too[test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
