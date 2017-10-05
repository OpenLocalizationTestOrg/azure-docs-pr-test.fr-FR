---
title: "Modifier les paramètres DATA 0 sur un appareil de la gamme StorSimple 8000 | Microsoft Docs"
description: "Découvrez comment utiliser Windows PowerShell for StorSimple pour reconfigurer l'interface réseau DATA 0 sur votre appareil StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: 90df43e22f17fd32fe642514df098b72700e77af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="modify-the-data-0-network-interface-settings-on-your-storsimple-8000-series-device"></a><span data-ttu-id="09502-103">Modifier les paramètres d’interface réseau DATA 0 sur votre appareils de la gamme StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="09502-103">Modify the DATA 0 network interface settings on your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="09502-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="09502-104">Overview</span></span>

<span data-ttu-id="09502-105">Votre appareil Microsoft Azure StorSimple dispose de six interfaces réseau, de DATA 0 à DATA 5.</span><span class="sxs-lookup"><span data-stu-id="09502-105">Your Microsoft Azure StorSimple device has six network interfaces, from DATA 0 to DATA 5.</span></span> <span data-ttu-id="09502-106">L’interface DATA 0 est toujours configurée via l'interface Windows PowerShell ou la console série, et elle est automatiquement activée pour le cloud.</span><span class="sxs-lookup"><span data-stu-id="09502-106">The DATA 0 interface is always configured through the Windows PowerShell interface or the serial console, and is automatically cloud-enabled.</span></span> <span data-ttu-id="09502-107">Vous ne pouvez pas configurer l’interface réseau DATA 0 via le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="09502-107">Note that you cannot configure DATA 0 network interface through the Azure portal.</span></span>

<span data-ttu-id="09502-108">L’interface DATA 0 est d'abord configuré via l’Assistant Installation lors du déploiement initial de l’appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="09502-108">The DATA 0 interface is first configured through the setup wizard during initial deployment of the StorSimple device.</span></span> <span data-ttu-id="09502-109">Si l’appareil est en cours d’exécution, vous devrez peut-être reconfigurer les paramètres DATA 0.</span><span class="sxs-lookup"><span data-stu-id="09502-109">When the device is in an operational mode, you may need to reconfigure DATA 0 settings.</span></span> <span data-ttu-id="09502-110">Ce didacticiel fournit deux méthodes permettant de modifier les paramètres de réseau DATA 0 via Windows PowerShell for StorSimple.</span><span class="sxs-lookup"><span data-stu-id="09502-110">This tutorial provides two methods to modify DATA 0 network settings, both through Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="09502-111">Après avoir lu ce didacticiel, vous pourrez :</span><span class="sxs-lookup"><span data-stu-id="09502-111">After reading this tutorial, you will be able to:</span></span>

* <span data-ttu-id="09502-112">Modification des paramètres réseau de DATA 0 via l'Assistant Installation</span><span class="sxs-lookup"><span data-stu-id="09502-112">Modify DATA 0 network setting through the setup wizard</span></span>
* <span data-ttu-id="09502-113">Modifier les paramètres réseau DATA 0 via l’applet de commande `Set-HcsNetInterface`</span><span class="sxs-lookup"><span data-stu-id="09502-113">Modify DATA 0 network settings through the `Set-HcsNetInterface` cmdlet</span></span>

## <a name="modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="09502-114">Modification des paramètres réseau de DATA 0 via l’Assistant Installation</span><span class="sxs-lookup"><span data-stu-id="09502-114">Modify DATA 0 network settings through setup wizard</span></span>
<span data-ttu-id="09502-115">Vous pouvez reconfigurer les paramètres réseau de DATA 0 en vous connectant à l'interface Windows PowerShell de votre appareil StorSimple et en ouvrant une session de l'Assistant Installation.</span><span class="sxs-lookup"><span data-stu-id="09502-115">You can reconfigure DATA 0 network settings by connecting to the Windows PowerShell interface of your StorSimple device and launching a setup wizard session.</span></span> <span data-ttu-id="09502-116">Pour modifier les paramètres de DATA 0, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="09502-116">Perform the following steps to modify DATA 0 settings:</span></span>

#### <a name="to-modify-data-0-network-settings-through-setup-wizard"></a><span data-ttu-id="09502-117">Pour modifier les paramètres réseau de DATA 0 via l’Assistant Installation</span><span class="sxs-lookup"><span data-stu-id="09502-117">To modify DATA 0 network settings through setup wizard</span></span>
1. <span data-ttu-id="09502-118">Dans le menu de la console série, sélectionnez l’option 1, **Ouvrir une session avec un accès total**.</span><span class="sxs-lookup"><span data-stu-id="09502-118">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="09502-119">Lorsque vous y êtes invité, fournissez le **mot de passe administrateur de l’appareil**.</span><span class="sxs-lookup"><span data-stu-id="09502-119">When prompted provide the **device administrator password**.</span></span> <span data-ttu-id="09502-120">Le mot de passe par défaut est `Password1`.</span><span class="sxs-lookup"><span data-stu-id="09502-120">The default password is `Password1`.</span></span>
2. <span data-ttu-id="09502-121"> À l’invite de commandes, tapez :</span><span class="sxs-lookup"><span data-stu-id="09502-121">At the command prompt, type:</span></span>
   
    `Invoke-HcsSetupWizard`
3. <span data-ttu-id="09502-122">Un assistant d’installation s’affiche pour vous aider à configurer l’interface DATA 0 de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="09502-122">A setup wizard appears to help configure the DATA 0 interface of your device.</span></span> <span data-ttu-id="09502-123">Indiquez les nouvelles valeurs de l'adresse IP, de la passerelle et du masque réseau.</span><span class="sxs-lookup"><span data-stu-id="09502-123">Provide new values for the IP address, gateway, and netmask.</span></span>

> [!NOTE]
> <span data-ttu-id="09502-124">Les adresses IP fixes des contrôleurs doivent être reconfigurées via le panneau **Paramètres réseau** de l’appareil StorSimple dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="09502-124">The fixed controllers IPs will need to be reconfigured through the **Network settings** blade of the StorSimple device in the Azure portal.</span></span> <span data-ttu-id="09502-125">Pour plus d'informations, consultez la rubrique [Modification des interfaces réseau](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span><span class="sxs-lookup"><span data-stu-id="09502-125">For more information, go to [Modify network interfaces](storsimple-8000-modify-device-config.md#modify-network-interfaces).</span></span>

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="09502-126">Modification des paramètres réseau de DATA 0 via l’applet de commande Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="09502-126">Modify DATA 0 network settings through Set-HcsNetInterface cmdlet</span></span>
<span data-ttu-id="09502-127">Vous pouvez également reconfigurer l’interface réseau DATA 0 via l’applet de commande `Set-HcsNetInterface` .</span><span class="sxs-lookup"><span data-stu-id="09502-127">An alternate way to reconfigure DATA 0 network interface is through the use of the `Set-HcsNetInterface` cmdlet.</span></span> <span data-ttu-id="09502-128">L’applet de commande est exécutée à partir de l’interface Windows PowerShell de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="09502-128">The cmdlet is executed from the Windows PowerShell interface of your StorSimple device.</span></span> <span data-ttu-id="09502-129">Lorsque vous utilisez cette procédure, les adresses IP fixes du contrôleur peuvent également être configurées.</span><span class="sxs-lookup"><span data-stu-id="09502-129">When using this procedure, the controller fixed IPs can also be configured here.</span></span> <span data-ttu-id="09502-130">Pour modifier les paramètres de DATA 0, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="09502-130">Perform the following steps to modify the DATA 0 settings:</span></span> 

#### <a name="to-modify-data-0-network-settings-through-the-set-hcsnetinterface-cmdlet"></a><span data-ttu-id="09502-131">Pour modifier les paramètres réseau de DATA 0 via l’applet de commande Set-HcsNetInterface</span><span class="sxs-lookup"><span data-stu-id="09502-131">To modify DATA 0 network settings through the Set-HcsNetInterface cmdlet</span></span>
1. <span data-ttu-id="09502-132">Dans le menu de la console série, sélectionnez l’option 1, **Ouvrir une session avec un accès total**.</span><span class="sxs-lookup"><span data-stu-id="09502-132">In the serial console menu, choose option 1, **Log in with full access**.</span></span> <span data-ttu-id="09502-133">Lorsque vous y êtes invité, fournissez le mot de passe administrateur de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="09502-133">When prompted provide the device administrator password.</span></span> <span data-ttu-id="09502-134">Le mot de passe par défaut est `Password1`.</span><span class="sxs-lookup"><span data-stu-id="09502-134">The default password is `Password1`.</span></span>
2. <span data-ttu-id="09502-135"> À l’invite de commandes, tapez :</span><span class="sxs-lookup"><span data-stu-id="09502-135">At the command prompt, type:</span></span>
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    <span data-ttu-id="09502-136">Entrez, entre crochets, les valeurs suivantes de DATA 0 :</span><span class="sxs-lookup"><span data-stu-id="09502-136">In the angled brackets, type the following values for DATA 0:</span></span>
   
   * <span data-ttu-id="09502-137">Adresse IPv4</span><span class="sxs-lookup"><span data-stu-id="09502-137">IPv4 address</span></span>
   * <span data-ttu-id="09502-138">Passerelle IPv4</span><span class="sxs-lookup"><span data-stu-id="09502-138">IPv4 gateway</span></span>
   * <span data-ttu-id="09502-139">Masque de sous-réseau IPv4</span><span class="sxs-lookup"><span data-stu-id="09502-139">IPv4 subnet mask</span></span>
   * <span data-ttu-id="09502-140">Adresse IPv4 fixe du contrôleur 0</span><span class="sxs-lookup"><span data-stu-id="09502-140">Fixed IPv4 address for Controller 0</span></span>
   * <span data-ttu-id="09502-141">Adresse IPv4 fixe du contrôleur 1</span><span class="sxs-lookup"><span data-stu-id="09502-141">Fixed IPv4 address for Controller 1</span></span>
     
     <span data-ttu-id="09502-142">Pour plus d’informations sur l’utilisation de cette applet de commande, consultez le [document de référence sur les applets de commande Windows PowerShell pour StorSimple](https://technet.microsoft.com/library/dn688161.aspx).</span><span class="sxs-lookup"><span data-stu-id="09502-142">For more information on the use of this cmdlet, go to [Windows PowerShell for StorSimple cmdlet reference](https://technet.microsoft.com/library/dn688161.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09502-143">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="09502-143">Next steps</span></span>
* <span data-ttu-id="09502-144">Pour configurer des interfaces réseau autres que DATA 0, vous pouvez utiliser la page [Configurer les paramètres réseau du portail Azure](storsimple-8000-modify-device-config.md).</span><span class="sxs-lookup"><span data-stu-id="09502-144">To configure network interfaces other than DATA 0, you can use the [Configure network settings in the Azure portal](storsimple-8000-modify-device-config.md).</span></span> 
* <span data-ttu-id="09502-145">Si vous rencontrez des problèmes lors de la configuration de vos interfaces réseau, consultez la page [Résolution des problèmes de déploiement](storsimple-troubleshoot-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="09502-145">If you experience any issues when configuring your network interfaces, refer to [Troubleshoot deployment issues](storsimple-troubleshoot-deployment.md).</span></span>

