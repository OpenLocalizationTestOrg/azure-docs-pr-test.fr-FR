---
title: "aaaConfigure SSL décharger - passerelle d’Application Azure - Azure Portal | Documents Microsoft"
description: "Cette page fournit toocreate instructions déchargement d’une passerelle d’application avec SSL à l’aide du portail de hello"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 8373379a-a26a-45d2-aa62-dd282298eff3
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: e87ac0bbe10ac45e307c18802741c7bc31764a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-hello-portal"></a><span data-ttu-id="749b3-103">Configurer une passerelle d’application pour le déchargement SSL à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="749b3-103">Configure an application gateway for SSL offload by using hello portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="749b3-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="749b3-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="749b3-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="749b3-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="749b3-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="749b3-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="749b3-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="749b3-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="749b3-108">Passerelle d’Application Azure peut être configuré tooterminate hello Secure Sockets Layer (SSL) session à hello passerelle tooavoid coûteux SSL déchiffrement tâches toohappen au niveau de la batterie de serveurs web hello.</span><span class="sxs-lookup"><span data-stu-id="749b3-108">Azure Application Gateway can be configured tooterminate hello Secure Sockets Layer (SSL) session at hello gateway tooavoid costly SSL decryption tasks toohappen at hello web farm.</span></span> <span data-ttu-id="749b3-109">Déchargement SSL simplifie également la configuration de serveur frontal de hello et la gestion d’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="749b3-109">SSL offload also simplifies hello front-end server setup and management of hello web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="749b3-110">Scénario</span><span class="sxs-lookup"><span data-stu-id="749b3-110">Scenario</span></span>

<span data-ttu-id="749b3-111">Hello scénario traverse configuration SSL décharger sur une passerelle d’application existant.</span><span class="sxs-lookup"><span data-stu-id="749b3-111">hello following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="749b3-112">Hello scénario part du principe que vous avez déjà suivi les étapes de hello trop[créer une passerelle d’Application](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="749b3-112">hello scenario assumes that you have already followed hello steps too[Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="749b3-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="749b3-113">Before you begin</span></span>

<span data-ttu-id="749b3-114">déchargement SSL tooconfigure avec une passerelle d’application, un certificat est requis.</span><span class="sxs-lookup"><span data-stu-id="749b3-114">tooconfigure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="749b3-115">Ce certificat est chargé sur la passerelle d’application hello et utilisé tooencrypt et le décryptage du trafic hello envoyé via SSL.</span><span class="sxs-lookup"><span data-stu-id="749b3-115">This certificate is loaded on hello application gateway and used tooencrypt and decrypt hello traffic sent via SSL.</span></span> <span data-ttu-id="749b3-116">certificat de Hello doit toobe au format d’échange d’informations personnelles (pfx).</span><span class="sxs-lookup"><span data-stu-id="749b3-116">hello certificate needs toobe in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="749b3-117">Ce format de fichier permet hello privé toobe clé exporté requis par hello application passerelle tooperform hello chiffrement et de déchiffrement du trafic.</span><span class="sxs-lookup"><span data-stu-id="749b3-117">This file format allows for hello private key toobe exported which is required by hello application gateway tooperform hello encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="749b3-118">Ajouter un écouteur HTTPS</span><span class="sxs-lookup"><span data-stu-id="749b3-118">Add an HTTPS listener</span></span>

<span data-ttu-id="749b3-119">port d’écoute HTTPS Hello recherche pour le trafic en fonction de sa configuration et vous aide au pools principaux toohello itinéraire hello du trafic.</span><span class="sxs-lookup"><span data-stu-id="749b3-119">hello HTTPS listener looks for traffic based on its configuration and helps route hello traffic toohello backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="749b3-120">Étape 1</span><span class="sxs-lookup"><span data-stu-id="749b3-120">Step 1</span></span>

<span data-ttu-id="749b3-121">Accédez toohello portail Azure et sélectionnez une passerelle d’application existant</span><span class="sxs-lookup"><span data-stu-id="749b3-121">Navigate toohello Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="749b3-122">Étape 2</span><span class="sxs-lookup"><span data-stu-id="749b3-122">Step 2</span></span>

<span data-ttu-id="749b3-123">Cliquez sur les écouteurs et cliquez sur tooadd de bouton hello ajouter un écouteur.</span><span class="sxs-lookup"><span data-stu-id="749b3-123">Click Listeners and click hello Add button tooadd a listener.</span></span>

![Panneau de vue d’ensemble de passerelle d’application][1]

### <a name="step-3"></a><span data-ttu-id="749b3-125">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="749b3-125">Step 3</span></span>

<span data-ttu-id="749b3-126">Remplissez les informations de hello requis pour hello écouteur et le téléchargement hello certificat .pfx, lorsque vous avez terminé cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="749b3-126">Fill out hello required information for hello listener and upload hello .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="749b3-127">**Nom** -cette valeur est un nom convivial de l’écouteur de hello.</span><span class="sxs-lookup"><span data-stu-id="749b3-127">**Name** - This value is a friendly name of hello listener.</span></span>

<span data-ttu-id="749b3-128">**Configuration IP de Frontend** -cette valeur est la configuration IP de serveur frontal hello qui est utilisée pour le port d’écoute hello.</span><span class="sxs-lookup"><span data-stu-id="749b3-128">**Frontend IP configuration** - This value is hello frontend IP configuration that is used for hello listener.</span></span>

<span data-ttu-id="749b3-129">**Le port frontal (nom/Port)** -un nom convivial pour le port hello utilisé sur les serveurs frontaux hello de passerelle d’application hello et port réelle de hello utilisé.</span><span class="sxs-lookup"><span data-stu-id="749b3-129">**Frontend port (Name/Port)** - A friendly name for hello port used on hello front end of hello application gateway and hello actual port used.</span></span>

<span data-ttu-id="749b3-130">**Protocole** -un toodetermine commutateur si https ou http est utilisé pour le serveur frontal hello.</span><span class="sxs-lookup"><span data-stu-id="749b3-130">**Protocol** - A switch toodetermine if https or http is used for hello front end.</span></span>

<span data-ttu-id="749b3-131">**Certificat (nom/mot de passe)** - si le déchargement SSL est utilisé, un certificat .pfx est requis pour ce paramètre, et un nom convivial et un mot de passe sont requis.</span><span class="sxs-lookup"><span data-stu-id="749b3-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![ajouter panneau d’écouteur][2]

## <a name="create-a-rule-and-associate-it-toohello-listener"></a><span data-ttu-id="749b3-133">Créer une règle et l’associer toohello écouteur</span><span class="sxs-lookup"><span data-stu-id="749b3-133">Create a rule and associate it toohello listener</span></span>

<span data-ttu-id="749b3-134">écouteur de Hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="749b3-134">hello listener has now been created.</span></span> <span data-ttu-id="749b3-135">Il est temps toocreate un règle toohandle hello du trafic à partir de l’écouteur de hello.</span><span class="sxs-lookup"><span data-stu-id="749b3-135">It is time toocreate a rule toohandle hello traffic from hello listener.</span></span> <span data-ttu-id="749b3-136">Les règles définissent comment le trafic est routé toohello pools de principaux en fonction de plusieurs paramètres de configuration, notamment si l’affinité de session basée sur le cookie est utilisée, protocole, port et sondes d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="749b3-136">Rules define how traffic is routed toohello backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="749b3-137">Étape 1</span><span class="sxs-lookup"><span data-stu-id="749b3-137">Step 1</span></span>

<span data-ttu-id="749b3-138">Cliquez sur hello **règles** de passerelle d’application hello, puis cliquez sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="749b3-138">Click hello **Rules** of hello application gateway, and then click Add.</span></span>

![Panneau de règles Application Gateway][3]

### <a name="step-2"></a><span data-ttu-id="749b3-140">Étape 2</span><span class="sxs-lookup"><span data-stu-id="749b3-140">Step 2</span></span>

<span data-ttu-id="749b3-141">Sur hello **ajouter une règle base** panneau, tapez Bonjour le nom convivial pour la règle de hello et choisissez écouteur hello créé à l’étape précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="749b3-141">On hello **Add basic rule** blade, type in hello friendly name for hello rule and choose hello listener created in hello previous step.</span></span> <span data-ttu-id="749b3-142">Choisissez le pool principal approprié de hello et configuration de http et cliquez sur **OK**</span><span class="sxs-lookup"><span data-stu-id="749b3-142">Choose hello appropriate backend pool and http setting and click **OK**</span></span>

![fenêtre de paramètres https][4]

<span data-ttu-id="749b3-144">paramètres de Hello sont à présent enregistrées toohello passerelle d’application.</span><span class="sxs-lookup"><span data-stu-id="749b3-144">hello settings are now saved toohello application gateway.</span></span> <span data-ttu-id="749b3-145">Hello processus pour ces paramètres d’enregistrement peut prendre un certain temps avant qu’elles soient tooview disponible via le portail de hello ou PowerShell.</span><span class="sxs-lookup"><span data-stu-id="749b3-145">hello save process for these settings may take a while before they are available tooview through hello portal or through PowerShell.</span></span> <span data-ttu-id="749b3-146">Passerelle d’application après avoir sauvegardé hello gère le chiffrement hello et le déchiffrement du trafic.</span><span class="sxs-lookup"><span data-stu-id="749b3-146">Once saved hello application gateway handles hello encryption and decryption of traffic.</span></span> <span data-ttu-id="749b3-147">Tout le trafic entre la passerelle d’application hello et serveurs web de principaux hello est géré via http.</span><span class="sxs-lookup"><span data-stu-id="749b3-147">All traffic between hello application gateway and hello backend web servers will be handled over http.</span></span> <span data-ttu-id="749b3-148">Client toohello chiffrée, n’importe quel client de retour toohello communication si lancé via le protocole https est retournée.</span><span class="sxs-lookup"><span data-stu-id="749b3-148">Any communication back toohello client if initiated over https will be returned toohello client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="749b3-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="749b3-149">Next steps</span></span>

<span data-ttu-id="749b3-150">toolearn tooconfigure un état personnalisé sonde avec la passerelle d’Application Azure, voir [créer une sonde d’intégrité personnalisé](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="749b3-150">toolearn how tooconfigure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
