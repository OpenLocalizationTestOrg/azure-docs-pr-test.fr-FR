---
title: "aaaModify hello DATA 0 paramètres sur un appareil StorSimple | Documents Microsoft"
description: "Découvrez comment toouse Windows PowerShell pour StorSimple tooreconfigure hello interface réseau DATA 0 sur votre appareil StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 58e3d509-f425-4a7f-b650-d496a7c85193
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: caec51c3344d953299253301c2a0d7577d553c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-device"></a><span data-ttu-id="4c9a7-103">Modifier les paramètres d’interface hello données réseau 0 sur votre appareil StorSimple</span><span class="sxs-lookup"><span data-stu-id="4c9a7-103">Modify hello DATA 0 network interface settings on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="4c9a7-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="4c9a7-104">Overview</span></span>
<span data-ttu-id="4c9a7-105">Votre appareil Microsoft Azure StorSimple a six interfaces réseau allant de DATA 0 tooDATA 5.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 tooDATA 5.</span></span> <span data-ttu-id="4c9a7-106">Hello interface de données 0 est toujours configurée via l’interface Windows PowerShell de hello ou de la console série de hello et est automatiquement activé pour le cloud.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-106">hello DATA 0 interface is always configured through hello Windows PowerShell interface or hello serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="4c9a7-107">Notez que vous ne pouvez pas configurer d’interface réseau DATA 0 via hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-107">Note that you cannot configure DATA 0 network interface through hello Azure classic portal.</span></span> 

<span data-ttu-id="4c9a7-108">Hello DATA 0 interface est d’abord configuré via l’Assistant d’installation hello lors du déploiement initial de l’appareil StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-108">hello DATA 0 interface is first configured through hello setup wizard during initial deployment of hello StorSimple device.</span></span> <span data-ttu-id="4c9a7-109">Lors de l’appareil de hello est dans un mode de fonctionnement, vous devrez peut-être tooreconfigure DATA 0 paramètres.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-109">When hello device is in an operational mode, you may need tooreconfigure DATA 0 settings.</span></span> <span data-ttu-id="4c9a7-110">Ce didacticiel fournit deux méthodes de paramètres de réseau 0 toomodify données, à la fois par le biais de Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-110">This tutorial provides two methods toomodify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="4c9a7-111">Après avoir lu ce didacticiel, vous pourrez :</span><span class="sxs-lookup"><span data-stu-id="4c9a7-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="4c9a7-112">Modifier des données 0 paramètre l’Assistant Installation hello réseau</span><span class="sxs-lookup"><span data-stu-id="4c9a7-112">Modify DATA 0 network setting through hello setup wizard</span></span>
* <span data-ttu-id="4c9a7-113">Modifier les paramètres de réseau 0 données via hello `Set-HcsNetInterface` applet de commande</span><span class="sxs-lookup"><span data-stu-id="4c9a7-113">Modify DATA 0 network settings through hello `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="4c9a7-114">Modification des paramètres réseau de DATA 0 via l’Assistant Installation</span><span class="sxs-lookup"><span data-stu-id="4c9a7-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="4c9a7-115">Vous pouvez reconfigurer les paramètres de réseau 0 de données en vous connectant interface Windows PowerShell de toohello de votre appareil StorSimple et de lancer une session de l’Assistant d’installation.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-115">You can reconfigure DATA 0 network settings by connecting toohello Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="4c9a7-116">Effectuer hello suivant les étapes toomodify DATA 0 paramètres :</span><span class="sxs-lookup"><span data-stu-id="4c9a7-116">Perform hello following steps toomodify DATA 0 settings:</span></span>

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="4c9a7-117">paramètres de réseau 0 toomodify données via l’Assistant Installation</span><span class="sxs-lookup"><span data-stu-id="4c9a7-117">toomodify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="4c9a7-118">Dans le menu de console série hello, sélectionnez l’option 1, **connecter avec un accès complet**.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-118">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="4c9a7-119">Lorsque vous y êtes invité fournir hello **mot de passe administrateur**.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-119">When prompted provide hello **device administrator password**.</span></span> <span data-ttu-id="4c9a7-120">mot de passe par défaut Hello est `Password1`.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-120">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="4c9a7-121">À l’invite de commandes hello, tapez :</span><span class="sxs-lookup"><span data-stu-id="4c9a7-121">At hello command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="4c9a7-122">Un Assistant d’installation s’affiche toohelp vous configurez hello DATA 0 interface de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-122">A setup wizard will appear toohelp you configure hello DATA 0 interface of your device.</span></span> <span data-ttu-id="4c9a7-123">Fournir de nouvelles valeurs de masque de réseau, la passerelle et adresse IP de hello.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-123">Provide new values for hello IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="4c9a7-124">Hello fixé contrôleurs IPs devez toobe reconfiguré via hello **configurer** page de l’appareil StorSimple hello Bonjour portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-124">hello fixed controllers IPs will need toobe reconfigured through hello **Configure** page of hello StorSimple device in hello Azure classic portal.</span></span> <span data-ttu-id="4c9a7-125">Pour plus d’informations, consultez trop[modifier des interfaces réseau](storsimple-modify-device-config.md#modify-network-interfaces).</span><span class="sxs-lookup"><span data-stu-id="4c9a7-125">For more information, go too[Modify network interfaces](storsimple-modify-device-config.md#modify-network-interfaces).</span></span>
> 
> 

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="4c9a7-126">Modification des paramètres réseau de DATA 0 via l’applet de commande Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="4c9a7-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="4c9a7-127">Un tooreconfigure autre façon DATA 0 est d’interface réseau via l’utilisation de hello de hello `Set-HcsNetInterface` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-127">An alternate way tooreconfigure DATA 0 network interface is through hello use of  hello `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="4c9a7-128">applet de commande Hello est exécuté à partir de l’interface Windows PowerShell de hello de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-128">hello cmdlet is executed from hello Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="4c9a7-129">Lorsque vous utilisez cette procédure, les IP fixé du contrôleur hello peut également être configuré ici.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-129">When using this procedure, hello controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="4c9a7-130">Effectuer hello suivant les étapes toomodify hello DATA 0 paramètres :</span><span class="sxs-lookup"><span data-stu-id="4c9a7-130">Perform hello following steps toomodify hello DATA 0 settings:</span></span> 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="4c9a7-131">paramètres de réseau 0 toomodify données via l’applet de commande Set-HcsNetInterface de hello</span><span class="sxs-lookup"><span data-stu-id="4c9a7-131">toomodify DATA 0 network settings through hello Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="4c9a7-132">Dans le menu de console série hello, sélectionnez l’option 1, **connecter avec un accès complet**.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-132">In hello serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="4c9a7-133">Lorsque vous y êtes invité fournir le mot de passe administrateur de périphérique hello.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-133">When prompted provide hello device administrator password.</span></span> <span data-ttu-id="4c9a7-134">mot de passe par défaut Hello est `Password1`.</span><span class="sxs-lookup"><span data-stu-id="4c9a7-134">hello default password is `Password1`.</span></span>
2. <span data-ttu-id="4c9a7-135">À l’invite de commandes hello, tapez :</span><span class="sxs-lookup"><span data-stu-id="4c9a7-135">At hello command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="4c9a7-136">Dans les crochets hello en angle, tapez hello valeurs suivantes pour DATA 0 :</span><span class="sxs-lookup"><span data-stu-id="4c9a7-136">In hello angled brackets, type hello following values for DATA 0:</span></span>
   
   * <span data-ttu-id="4c9a7-137">Adresse IPv4</span><span class="sxs-lookup"><span data-stu-id="4c9a7-137">IPv4 address</span></span>
   * <span data-ttu-id="4c9a7-138">Passerelle IPv4</span><span class="sxs-lookup"><span data-stu-id="4c9a7-138">IPv4 gateway</span></span>
   * <span data-ttu-id="4c9a7-139">Masque de sous-réseau IPv4</span><span class="sxs-lookup"><span data-stu-id="4c9a7-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="4c9a7-140">Adresse IPv4 fixe du contrôleur 0</span><span class="sxs-lookup"><span data-stu-id="4c9a7-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="4c9a7-141">Adresse IPv4 fixe du contrôleur 1</span><span class="sxs-lookup"><span data-stu-id="4c9a7-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="4c9a7-142">Pour plus d’informations sur l’utilisation de hello de cette applet de commande, accédez trop[Windows PowerShell pour la référence d’applet de commande StorSimple](https://technet.microsoft.com/library/dn688161.aspx).</span><span class="sxs-lookup"><span data-stu-id="4c9a7-142">For more information on hello use of this cmdlet, go too[Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c9a7-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4c9a7-143">Next steps</span></span>
* <span data-ttu-id="4c9a7-144">tooconfigure les interfaces réseau autres que DATA 0, vous pouvez utiliser hello [page Configurer Bonjour portail Azure classic](storsimple-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="4c9a7-144">tooconfigure network interfaces other than DATA 0, you can use hello [Configure page in hello Azure classic portal](storsimple-modify-device-config.md).</span></span> 
* <span data-ttu-id="4c9a7-145">Si vous rencontrez des problèmes lors de la configuration des interfaces réseau, consultez trop[résoudre les problèmes de déploiement](storsimple-troubleshoot-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="4c9a7-145">If you experience any issues when configuring your network interfaces, refer too[Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>

