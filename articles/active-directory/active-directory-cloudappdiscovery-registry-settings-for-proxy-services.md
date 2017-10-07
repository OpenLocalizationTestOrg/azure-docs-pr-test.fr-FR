---
title: "aaaCloud paramètres du Registre application découverte pour les Services Proxy | Documents Microsoft"
description: "objectif Hello de cette rubrique est tooprovide vous hello étapes que vous devez port hello requis tooperform tooset ordinateurs hello exécutant l’agent de découverte d’application Cloud hello."
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
ms.openlocfilehash: bb1fe20016459160b4f67cb0125b1781a0260c4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="d1c2d-103">Paramètres de Registre de Cloud App Discovery pour les services de proxy</span><span class="sxs-lookup"><span data-stu-id="d1c2d-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="d1c2d-104">Par défaut, l’agent de découverte d’application Cloud hello est configuré toouse que hello les ports 80 ou 443.</span><span class="sxs-lookup"><span data-stu-id="d1c2d-104">By default, hello Cloud App Discovery agent is configured toouse only hello ports 80 or 443.</span></span> <span data-ttu-id="d1c2d-105">Si vous envisagez d’installer Cloud App Discovery dans un environnement avec un serveur proxy qui utilise un port personnalisé (443 ni 80), vous devez tooconfigure votre toouse agents ce port.</span><span class="sxs-lookup"><span data-stu-id="d1c2d-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need tooconfigure your agents toouse this port.</span></span> <span data-ttu-id="d1c2d-106">configuration de Hello est basée sur une clé de Registre.</span><span class="sxs-lookup"><span data-stu-id="d1c2d-106">hello configuration is based on a registry key.</span></span>

<span data-ttu-id="d1c2d-107">objectif Hello de cette rubrique est tooprovide vous hello étapes que vous devez port hello requis tooperform tooset ordinateurs hello exécutant l’agent de découverte d’application Cloud hello.</span><span class="sxs-lookup"><span data-stu-id="d1c2d-107">hello objective of this topic is tooprovide you with hello steps you need tooperform tooset hello required port on hello computers running hello Cloud App Discovery agent.</span></span>

<span data-ttu-id="d1c2d-108">**port de hello toomodify utilisé par ordinateur hello exécutant l’agent de découverte d’application Cloud hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="d1c2d-108">**toomodify hello port used by hello computer running hello Cloud App Discovery agent, perform hello following steps:**</span></span>

1. <span data-ttu-id="d1c2d-109">Démarrez l’Éditeur du Registre hello.</span><span class="sxs-lookup"><span data-stu-id="d1c2d-109">Start hello registry editor.</span></span> <br> ![Exécuter](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="d1c2d-111">Accédez tooor créer hello clé de Registre suivante :</span><span class="sxs-lookup"><span data-stu-id="d1c2d-111">Navigate tooor create hello following registry key:</span></span> <br> <span data-ttu-id="d1c2d-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span><span class="sxs-lookup"><span data-stu-id="d1c2d-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="d1c2d-113">Créez une valeur de **chaînes multiples** nommée **Ports**.</span><span class="sxs-lookup"><span data-stu-id="d1c2d-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="d1c2d-114">![Nouveau](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="d1c2d-114">![New](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="d1c2d-115">tooopen hello **modifier les chaînes multiples** boîte de dialogue, double-cliquez sur la valeur de Ports hello.</span><span class="sxs-lookup"><span data-stu-id="d1c2d-115">tooopen hello **Edit Multi-String** dialog, double-click hello Ports value.</span></span>
5. <span data-ttu-id="d1c2d-116">Dans la zone de texte des données de valeur de hello, tapez Bonjour valeurs suivantes et ajoutez tous les ports personnalisés utilisés par votre organisation :</span><span class="sxs-lookup"><span data-stu-id="d1c2d-116">In hello Value data textbox, type hello following values and add all custom ports that are used by your organization:</span></span> <br><br><span data-ttu-id="d1c2d-117">
   **80**</span><span class="sxs-lookup"><span data-stu-id="d1c2d-117">
   **80**</span></span> <br><span data-ttu-id="d1c2d-118">
   **8080**</span><span class="sxs-lookup"><span data-stu-id="d1c2d-118">
   **8080**</span></span> <br><span data-ttu-id="d1c2d-119">
   **8118**</span><span class="sxs-lookup"><span data-stu-id="d1c2d-119">
   **8118**</span></span> <br><span data-ttu-id="d1c2d-120">
   **8888**</span><span class="sxs-lookup"><span data-stu-id="d1c2d-120">
   **8888**</span></span> <br><span data-ttu-id="d1c2d-121">
   **81**</span><span class="sxs-lookup"><span data-stu-id="d1c2d-121">
   **81**</span></span> <br><span data-ttu-id="d1c2d-122">
   **12080**</span><span class="sxs-lookup"><span data-stu-id="d1c2d-122">
   **12080**</span></span> <br><span data-ttu-id="d1c2d-123">
   **6999**</span><span class="sxs-lookup"><span data-stu-id="d1c2d-123">
**6999**</span></span> <br><span data-ttu-id="d1c2d-124">
**30606**</span><span class="sxs-lookup"><span data-stu-id="d1c2d-124">
**30606**</span></span> <br><span data-ttu-id="d1c2d-125">
**31595**</span><span class="sxs-lookup"><span data-stu-id="d1c2d-125">
**31595**</span></span> <br><span data-ttu-id="d1c2d-126">
**4080**</span><span class="sxs-lookup"><span data-stu-id="d1c2d-126">
**4080**</span></span> <br><span data-ttu-id="d1c2d-127">
**443**</span><span class="sxs-lookup"><span data-stu-id="d1c2d-127">
**443**</span></span> <br><span data-ttu-id="d1c2d-128">
**1110**</span><span class="sxs-lookup"><span data-stu-id="d1c2d-128">
**1110**</span></span> <br><br><span data-ttu-id="d1c2d-129">
![Modifier les chaînes multiples](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="d1c2d-129">
![Edit Multi-String](./media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="d1c2d-130">Cliquez sur **OK** tooclose hello **modifier les chaînes multiples** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d1c2d-130">Click **OK** tooclose hello **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="d1c2d-131">**Ressources supplémentaires**</span><span class="sxs-lookup"><span data-stu-id="d1c2d-131">**Additional Resources**</span></span>

* [<span data-ttu-id="d1c2d-132">Comment puis-je détecter les applications cloud non approuvées utilisées au sein de mon organisation ?</span><span class="sxs-lookup"><span data-stu-id="d1c2d-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 

