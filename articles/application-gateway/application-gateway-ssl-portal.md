---
title: "Configurer le déchargement SSL - Passerelle Azure Application Gateway - Portail Azure | Microsoft Docs"
description: "Cette page fournit des instructions pour la création d’une passerelle Application Gateway pour le déchargement SSL à l’aide du portail"
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
ms.openlocfilehash: f61be0cc4c9274c9914f7c468ce48a2a3d0a4f4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-portal"></a><span data-ttu-id="8c5da-103">Configurer une passerelle d’application pour le déchargement SSL en utilisant le portail</span><span class="sxs-lookup"><span data-stu-id="8c5da-103">Configure an application gateway for SSL offload by using the portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8c5da-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="8c5da-104">Azure portal</span></span>](application-gateway-ssl-portal.md)
> * [<span data-ttu-id="8c5da-105">Commandes PowerShell pour Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8c5da-105">Azure Resource Manager PowerShell</span></span>](application-gateway-ssl-arm.md)
> * [<span data-ttu-id="8c5da-106">Azure Classic PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c5da-106">Azure Classic PowerShell</span></span>](application-gateway-ssl.md)
> * [<span data-ttu-id="8c5da-107">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8c5da-107">Azure CLI 2.0</span></span>](application-gateway-ssl-cli.md)

<span data-ttu-id="8c5da-108">Il est possible de configurer Azure Application Gateway de façon à mettre fin à la session SSL (Secure Sockets Layer) sur la passerelle pour éviter les tâches de déchiffrement SSL coûteuses au niveau de la batterie de serveurs web.</span><span class="sxs-lookup"><span data-stu-id="8c5da-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="8c5da-109">Le déchargement SSL simplifie aussi la configuration de serveur principal et la gestion de l’application web.</span><span class="sxs-lookup"><span data-stu-id="8c5da-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="scenario"></a><span data-ttu-id="8c5da-110">Scénario</span><span class="sxs-lookup"><span data-stu-id="8c5da-110">Scenario</span></span>

<span data-ttu-id="8c5da-111">Le scénario suivant passe par la configuration du déchargement SSL sur une passerelle d’application existante.</span><span class="sxs-lookup"><span data-stu-id="8c5da-111">The following scenario goes through configuring SSL offload on an existing application gateway.</span></span> <span data-ttu-id="8c5da-112">Le scénario suppose que vous avez déjà suivi la procédure de [Création d’une passerelle Application Gateway](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8c5da-112">The scenario assumes that you have already followed the steps to [Create an Application Gateway](application-gateway-create-gateway-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8c5da-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="8c5da-113">Before you begin</span></span>

<span data-ttu-id="8c5da-114">Pour configurer le déchargement SSL avec une passerelle Application Gateway, un certificat est requis.</span><span class="sxs-lookup"><span data-stu-id="8c5da-114">To configure SSL offload with an application gateway, a certificate is required.</span></span> <span data-ttu-id="8c5da-115">Ce certificat est chargé sur la passerelle d’application et utilisé pour chiffrer et déchiffrer le trafic envoyé via SSL.</span><span class="sxs-lookup"><span data-stu-id="8c5da-115">This certificate is loaded on the application gateway and used to encrypt and decrypt the traffic sent via SSL.</span></span> <span data-ttu-id="8c5da-116">Le certificat doit être partagé au format Personal Information Exchange (.pfx).</span><span class="sxs-lookup"><span data-stu-id="8c5da-116">The certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="8c5da-117">Ce format de fichier permet d’exporter la clé privée requise par la passerelle d’application pour effectuer le chiffrement et le déchiffrement du trafic.</span><span class="sxs-lookup"><span data-stu-id="8c5da-117">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

## <a name="add-an-https-listener"></a><span data-ttu-id="8c5da-118">Ajouter un écouteur HTTPS</span><span class="sxs-lookup"><span data-stu-id="8c5da-118">Add an HTTPS listener</span></span>

<span data-ttu-id="8c5da-119">L’écouteur HTTPS recherche le trafic en fonction de sa configuration et aide à acheminer le trafic vers les pools principaux.</span><span class="sxs-lookup"><span data-stu-id="8c5da-119">The HTTPS listener looks for traffic based on its configuration and helps route the traffic to the backend pools.</span></span>

### <a name="step-1"></a><span data-ttu-id="8c5da-120">Étape 1</span><span class="sxs-lookup"><span data-stu-id="8c5da-120">Step 1</span></span>

<span data-ttu-id="8c5da-121">Accédez au portail Azure et sélectionnez une passerelle d’application existante.</span><span class="sxs-lookup"><span data-stu-id="8c5da-121">Navigate to the Azure portal and select an existing application gateway</span></span>

### <a name="step-2"></a><span data-ttu-id="8c5da-122">Étape 2</span><span class="sxs-lookup"><span data-stu-id="8c5da-122">Step 2</span></span>

<span data-ttu-id="8c5da-123">Cliquez sur Écouteurs et cliquez sur le bouton Ajouter pour ajouter un écouteur.</span><span class="sxs-lookup"><span data-stu-id="8c5da-123">Click Listeners and click the Add button to add a listener.</span></span>

![Panneau de vue d’ensemble de passerelle d’application][1]

### <a name="step-3"></a><span data-ttu-id="8c5da-125">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="8c5da-125">Step 3</span></span>

<span data-ttu-id="8c5da-126">Remplissez les informations requises pour l’écouteur, et téléchargez le certificat .pfx. Lorsque vous avez terminé, cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="8c5da-126">Fill out the required information for the listener and upload the .pfx certificate, when complete click OK.</span></span>

<span data-ttu-id="8c5da-127">**Nom** - il s’agit d’un nom convivial pour l’écouteur.</span><span class="sxs-lookup"><span data-stu-id="8c5da-127">**Name** - This value is a friendly name of the listener.</span></span>

<span data-ttu-id="8c5da-128">**Configuration IP frontale** - il s’agit de la configuration d’IP frontale utilisée pour l’écouteur.</span><span class="sxs-lookup"><span data-stu-id="8c5da-128">**Frontend IP configuration** - This value is the frontend IP configuration that is used for the listener.</span></span>

<span data-ttu-id="8c5da-129">**Port frontal (nom/port)** - un nom convivial pour le port utilisé sur le serveur frontal de la passerelle Application Gateway et le port utilisé.</span><span class="sxs-lookup"><span data-stu-id="8c5da-129">**Frontend port (Name/Port)** - A friendly name for the port used on the front end of the application gateway and the actual port used.</span></span>

<span data-ttu-id="8c5da-130">**Protocole** - un commutateur qui détermine si https ou http est utilisé pour le serveur frontal.</span><span class="sxs-lookup"><span data-stu-id="8c5da-130">**Protocol** - A switch to determine if https or http is used for the front end.</span></span>

<span data-ttu-id="8c5da-131">**Certificat (nom/mot de passe)** - si le déchargement SSL est utilisé, un certificat .pfx est requis pour ce paramètre, et un nom convivial et un mot de passe sont requis.</span><span class="sxs-lookup"><span data-stu-id="8c5da-131">**Certificate (Name/Password)** - If SSL offload is used, a .pfx certificate is required for this setting and a friendly name and password are required.</span></span>

![ajouter panneau d’écouteur][2]

## <a name="create-a-rule-and-associate-it-to-the-listener"></a><span data-ttu-id="8c5da-133">Créer une règle et l’associer à l’écouteur</span><span class="sxs-lookup"><span data-stu-id="8c5da-133">Create a rule and associate it to the listener</span></span>

<span data-ttu-id="8c5da-134">L’écouteur a été créé.</span><span class="sxs-lookup"><span data-stu-id="8c5da-134">The listener has now been created.</span></span> <span data-ttu-id="8c5da-135">Il est temps de créer une règle pour gérer le trafic de l’écouteur.</span><span class="sxs-lookup"><span data-stu-id="8c5da-135">It is time to create a rule to handle the traffic from the listener.</span></span> <span data-ttu-id="8c5da-136">Les règles définissent la façon dont le trafic est acheminé vers les pools principaux en fonction de plusieurs paramètres de configuration, dont l’utilisation ou non de l’affinité de session basée sur les cookies, le protocole, le port et les sondes d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="8c5da-136">Rules define how traffic is routed to the backend pools based on multiple configuration settings, including whether cookie-based session affinity is used, protocol, port, and health probes.</span></span>

### <a name="step-1"></a><span data-ttu-id="8c5da-137">Étape 1</span><span class="sxs-lookup"><span data-stu-id="8c5da-137">Step 1</span></span>

<span data-ttu-id="8c5da-138">Cliquez sur **Règles** dans la passerelle Application Gateway, puis cliquez sur Ajouter.</span><span class="sxs-lookup"><span data-stu-id="8c5da-138">Click the **Rules** of the application gateway, and then click Add.</span></span>

![Panneau de règles Application Gateway][3]

### <a name="step-2"></a><span data-ttu-id="8c5da-140">Étape 2</span><span class="sxs-lookup"><span data-stu-id="8c5da-140">Step 2</span></span>

<span data-ttu-id="8c5da-141">Sur le panneau **Ajouter une règle de base** , tapez le nom convivial de la règle et choisissez l’écouteur créé à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="8c5da-141">On the **Add basic rule** blade, type in the friendly name for the rule and choose the listener created in the previous step.</span></span> <span data-ttu-id="8c5da-142">Choisissez le pool principal approprié et la configuration http souhaitée, puis cliquez sur **OK**</span><span class="sxs-lookup"><span data-stu-id="8c5da-142">Choose the appropriate backend pool and http setting and click **OK**</span></span>

![fenêtre de paramètres https][4]

<span data-ttu-id="8c5da-144">Les paramètres sont maintenant enregistrés pour la passerelle Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="8c5da-144">The settings are now saved to the application gateway.</span></span> <span data-ttu-id="8c5da-145">Le processus d’enregistrement pour ces paramètres peut prendre un certain temps avant leur disponibilité sur le portail ou via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8c5da-145">The save process for these settings may take a while before they are available to view through the portal or through PowerShell.</span></span> <span data-ttu-id="8c5da-146">Une fois enregistrée, la passerelle Application Gateway gère le chiffrement et le déchiffrement du trafic.</span><span class="sxs-lookup"><span data-stu-id="8c5da-146">Once saved the application gateway handles the encryption and decryption of traffic.</span></span> <span data-ttu-id="8c5da-147">Tout le trafic entre la passerelle Application Gateway et les serveurs web principaux est géré via http.</span><span class="sxs-lookup"><span data-stu-id="8c5da-147">All traffic between the application gateway and the backend web servers will be handled over http.</span></span> <span data-ttu-id="8c5da-148">Toute communication lancée vers le client via le protocole https sera renvoyée chiffrée au client.</span><span class="sxs-lookup"><span data-stu-id="8c5da-148">Any communication back to the client if initiated over https will be returned to the client encrypted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c5da-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8c5da-149">Next steps</span></span>

<span data-ttu-id="8c5da-150">Pour savoir comment configurer une sonde d’intégrité personnalisée avec Azure Application Gateway, consultez [Créer une sonde d’intégrité personnalisée](application-gateway-create-gateway-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8c5da-150">To learn how to configure a custom health probe with Azure Application Gateway, see [Create a custom health probe](application-gateway-create-gateway-portal.md).</span></span>

[1]: ./media/application-gateway-ssl-portal/figure1.png
[2]: ./media/application-gateway-ssl-portal/figure2.png
[3]: ./media/application-gateway-ssl-portal/figure3.png
[4]: ./media/application-gateway-ssl-portal/figure4.png
