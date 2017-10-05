---
title: "Paramètres de Registre de Cloud App Discovery pour les services de proxy | Microsoft Docs"
description: "L’objectif de cette rubrique est de présenter les étapes que vous devez effectuer pour définir le port nécessaire sur les ordinateurs exécutant l’agent Cloud App Discovery."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: ea15dc9a9f20a296e622c8fb1011f7ee99de3e99
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="77d1e-103">Paramètres de Registre de Cloud App Discovery pour les services de proxy</span><span class="sxs-lookup"><span data-stu-id="77d1e-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="77d1e-104">Par défaut, l’agent Cloud App Discovery est configuré pour utiliser uniquement les ports 80 ou 443.</span><span class="sxs-lookup"><span data-stu-id="77d1e-104">By default, the Cloud App Discovery agent is configured to use only the ports 80 or 443.</span></span> <span data-ttu-id="77d1e-105">Si vous envisagez d’installer Cloud App Discovery dans un environnement avec un serveur proxy qui utilise un port personnalisé (ni 443, ni 80), vous devez configurer vos agents pour utiliser ce port.</span><span class="sxs-lookup"><span data-stu-id="77d1e-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need to configure your agents to use this port.</span></span> <span data-ttu-id="77d1e-106">La configuration est basée sur une clé de Registre.</span><span class="sxs-lookup"><span data-stu-id="77d1e-106">The configuration is based on a registry key.</span></span>

<span data-ttu-id="77d1e-107">L’objectif de cette rubrique est de présenter les étapes que vous devez effectuer pour définir le port nécessaire sur les ordinateurs exécutant l’agent Cloud App Discovery.</span><span class="sxs-lookup"><span data-stu-id="77d1e-107">The objective of this topic is to provide you with the steps you need to perform to set the required port on the computers running the Cloud App Discovery agent.</span></span>

<span data-ttu-id="77d1e-108">**Pour modifier le port utilisé par l’ordinateur exécutant l’agent Cloud App Discovery, effectuez les opérations suivantes :**</span><span class="sxs-lookup"><span data-stu-id="77d1e-108">**To modify the port used by the computer running the Cloud App Discovery agent, perform the following steps:**</span></span>

1. <span data-ttu-id="77d1e-109">Démarrez l’Éditeur du Registre.</span><span class="sxs-lookup"><span data-stu-id="77d1e-109">Start the registry editor.</span></span> <br> ![Exécuter](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="77d1e-111">Créez ou accédez à la clé de Registre suivante : </span><span class="sxs-lookup"><span data-stu-id="77d1e-111">Navigate to or create the following registry key:</span></span> <br> <span data-ttu-id="77d1e-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span><span class="sxs-lookup"><span data-stu-id="77d1e-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="77d1e-113">Créez une valeur de **chaînes multiples** nommée **Ports**.</span><span class="sxs-lookup"><span data-stu-id="77d1e-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="77d1e-114">![Nouveau](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="77d1e-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="77d1e-115">Pour ouvrir la boîte de dialogue **Modifier les chaînes multiples** , double-cliquez sur la valeur de Ports.</span><span class="sxs-lookup"><span data-stu-id="77d1e-115">To open the **Edit Multi-String** dialog, double-click the Ports value.</span></span>
5. <span data-ttu-id="77d1e-116">Dans la zone de texte Données de la valeur, tapez les valeurs suivantes et ajoutez tous les ports personnalisés qui sont utilisés par votre organisation : </span><span class="sxs-lookup"><span data-stu-id="77d1e-116">In the Value data textbox, type the following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="77d1e-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="77d1e-117">
   **80**</span></span> <br><span data-ttu-id="77d1e-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="77d1e-118">
   **8080**</span></span> <br><span data-ttu-id="77d1e-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="77d1e-119">
   **8118**</span></span> <br><span data-ttu-id="77d1e-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="77d1e-120">
   **8888**</span></span> <br><span data-ttu-id="77d1e-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="77d1e-121">
   **81**</span></span> <br><span data-ttu-id="77d1e-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="77d1e-122">
   **12080**</span></span> <br><span data-ttu-id="77d1e-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="77d1e-123">
**6999**</span></span> <br><span data-ttu-id="77d1e-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="77d1e-124">
**30606**</span></span> <br><span data-ttu-id="77d1e-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="77d1e-125">
**31595**</span></span> <br><span data-ttu-id="77d1e-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="77d1e-126">
**4080**</span></span> <br><span data-ttu-id="77d1e-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="77d1e-127">
**443**</span></span> <br><span data-ttu-id="77d1e-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="77d1e-128">
**1110**</span></span> <br><br><span data-ttu-id="77d1e-129">
![Modifier les chaînes multiples](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="77d1e-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="77d1e-130">Cliquez sur **OK** pour fermer la boîte de dialogue **Modifier les chaînes multiples**.</span><span class="sxs-lookup"><span data-stu-id="77d1e-130">Click **OK** to close the **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="77d1e-131">**Ressources supplémentaires**</span><span class="sxs-lookup"><span data-stu-id="77d1e-131">**Additional Resources**</span></span>

* [<span data-ttu-id="77d1e-132">Comment puis-je détecter les applications cloud non approuvées utilisées au sein de mon organisation ?</span><span class="sxs-lookup"><span data-stu-id="77d1e-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

