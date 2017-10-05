---
title: "Se connecter à distance à votre appareil StorSimple | Microsoft Docs"
description: "Explique comment configurer votre appareil pour la gestion à distance et comment se connecter à Windows PowerShell for StorSimple par HTTP ou HTTPS."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff76884f020a0fb8a1b48bd371c419bd65e85fd3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-remotely-to-your-storsimple-8000-series-device"></a><span data-ttu-id="440fb-103">Connexion à distance à votre appareil StorSimple série 8000</span><span class="sxs-lookup"><span data-stu-id="440fb-103">Connect remotely to your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="440fb-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="440fb-104">Overview</span></span>

<span data-ttu-id="440fb-105">Vous pouvez vous connecter à distance à votre appareil via Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="440fb-105">You can remotely connect to your device via Windows PowerShell.</span></span> <span data-ttu-id="440fb-106">Quand vous vous connectez de cette façon, aucun menu ne s’affiche.</span><span class="sxs-lookup"><span data-stu-id="440fb-106">When you connect this way, you do not see a menu.</span></span> <span data-ttu-id="440fb-107">(Vous voyez un menu seulement si vous utilisez la console série sur l’appareil pour vous connecter). Avec l’accès distant Windows PowerShell, vous vous connectez à une instance d’exécution spécifique.</span><span class="sxs-lookup"><span data-stu-id="440fb-107">(You see a menu only if you use the serial console on the device to connect.) With Windows PowerShell remoting, you connect to a specific runspace.</span></span> <span data-ttu-id="440fb-108">Vous pouvez également spécifier la langue d’affichage.</span><span class="sxs-lookup"><span data-stu-id="440fb-108">You can also specify the display language.</span></span>

<span data-ttu-id="440fb-109">Pour plus d’informations sur l’utilisation de l’accès distant Windows PowerShell pour gérer votre appareil, consultez la rubrique [Administrer votre appareil StorSimple à l’aide de Windows PowerShell pour StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="440fb-109">For more information about using Windows PowerShell remoting to manage your device, go to [Use Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>

<span data-ttu-id="440fb-110">Ce didacticiel explique comment configurer votre appareil pour la gestion à distance, puis comment se connecter à Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="440fb-110">This tutorial explains how to configure your device for remote management and then how to connect to Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="440fb-111">Vous pouvez utiliser HTTP ou HTTPS pour vous connecter à distance via Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="440fb-111">You can use HTTP or HTTPS to remotely connect via Windows PowerShell.</span></span> <span data-ttu-id="440fb-112">Cependant, quand vous décidez comment vous connecter à Windows PowerShell pour StorSimple, prenez en compte les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="440fb-112">However, when you are deciding how to connect to Windows PowerShell for StorSimple, consider the following information:</span></span>

* <span data-ttu-id="440fb-113">Une connexion directe à la console série de l’appareil est sécurisée, mais une connexion à la console via des commutateurs réseau ne l’est pas.</span><span class="sxs-lookup"><span data-stu-id="440fb-113">Connecting directly to the device serial console is secure, but connecting to the serial console over network switches is not.</span></span> <span data-ttu-id="440fb-114">Méfiez-vous des risques de sécurité lors de la connexion à la console série d’un appareil via des commutateurs réseau.</span><span class="sxs-lookup"><span data-stu-id="440fb-114">Be cautious of the security risk when connecting to the device serial console over network switches.</span></span>
* <span data-ttu-id="440fb-115">Une connexion via une session HTTP peut offrir davantage de sécurité que la connexion via la console série sur le réseau.</span><span class="sxs-lookup"><span data-stu-id="440fb-115">Connecting through an HTTP session might offer more security than connecting through the serial console over the network.</span></span> <span data-ttu-id="440fb-116">Bien que cela ne soit pas la méthode la plus sécurisée, elle est acceptable sur des réseaux approuvés.</span><span class="sxs-lookup"><span data-stu-id="440fb-116">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>
* <span data-ttu-id="440fb-117">La connexion via une session HTTPS avec un certificat auto-signé est l’option la plus sécurisée et c’est celle qui est recommandée.</span><span class="sxs-lookup"><span data-stu-id="440fb-117">Connecting through an HTTPS session with a self-signed certificate is the most secure and the recommended option.</span></span>

<span data-ttu-id="440fb-118">Vous pouvez vous connecter à distance à l’interface Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="440fb-118">You can connect remotely to the Windows PowerShell interface.</span></span> <span data-ttu-id="440fb-119">Cependant, l’accès à distance à votre appareil StorSimple via l’interface Windows PowerShell n’est pas activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="440fb-119">However, remote access to your StorSimple device via the Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="440fb-120">Vous devez d’abord activer la gestion à distance sur l’appareil, puis sur le client qui est utilisé pour accéder à votre appareil.</span><span class="sxs-lookup"><span data-stu-id="440fb-120">You must enable remote management on the device first, and then on the client that is used to access your device.</span></span>

<span data-ttu-id="440fb-121">Les étapes décrites dans cet article ont été exécutées sur un système hôte exécutant Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="440fb-121">The steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="440fb-122">Se connecter via HTTP</span><span class="sxs-lookup"><span data-stu-id="440fb-122">Connect through HTTP</span></span>

<span data-ttu-id="440fb-123">La connexion à Windows PowerShell pour StorSimple via une session HTTP offre davantage de sécurité que la connexion via la console série de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="440fb-123">Connecting to Windows PowerShell for StorSimple through an HTTP session offers more security than connecting through the serial console of your StorSimple device.</span></span> <span data-ttu-id="440fb-124">Bien que cela ne soit pas la méthode la plus sécurisée, elle est acceptable sur des réseaux approuvés.</span><span class="sxs-lookup"><span data-stu-id="440fb-124">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="440fb-125">Vous pouvez utiliser le portail Azure ou la console série pour configurer la gestion à distance.</span><span class="sxs-lookup"><span data-stu-id="440fb-125">You can use either the Azure portal or the serial console to configure remote management.</span></span> <span data-ttu-id="440fb-126">Choisissez parmi les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="440fb-126">Select from the following procedures:</span></span>

* [<span data-ttu-id="440fb-127">Utiliser le portail Azure pour activer la gestion à distance via HTTP</span><span class="sxs-lookup"><span data-stu-id="440fb-127">Use the Azure portal to enable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="440fb-128">Utiliser la console série pour activer la gestion à distance via HTTP</span><span class="sxs-lookup"><span data-stu-id="440fb-128">Use the serial console to enable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="440fb-129">Après avoir activé la gestion à distance, procédez comme suit pour préparer le client pour une connexion à distance.</span><span class="sxs-lookup"><span data-stu-id="440fb-129">After you enable remote management, use the following procedure to prepare the client for a remote connection.</span></span>

* [<span data-ttu-id="440fb-130">Préparer le client pour une connexion à distance</span><span class="sxs-lookup"><span data-stu-id="440fb-130">Prepare the client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-the-azure-portal-to-enable-remote-management-over-http"></a><span data-ttu-id="440fb-131">Utiliser le portail Azure pour activer la gestion à distance via HTTP</span><span class="sxs-lookup"><span data-stu-id="440fb-131">Use the Azure portal to enable remote management over HTTP</span></span>

<span data-ttu-id="440fb-132">Procédez comme suit dans le portail Azure pour activer la gestion à distance via HTTP.</span><span class="sxs-lookup"><span data-stu-id="440fb-132">Perform the following steps in the Azure portal to enable remote management over HTTP.</span></span>

#### <a name="to-enable-remote-management-through-the-azure-portal"></a><span data-ttu-id="440fb-133">Pour activer la gestion à distance via le portail Azure</span><span class="sxs-lookup"><span data-stu-id="440fb-133">To enable remote management through the Azure portal</span></span>

1. <span data-ttu-id="440fb-134">Accédez à votre service StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="440fb-134">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="440fb-135">Sélectionnez **Appareils**, puis cliquez sur l’appareil à configurer pour la gestion à distance.</span><span class="sxs-lookup"><span data-stu-id="440fb-135">Select **Devices** and then select and click the device you want to configure for remote management.</span></span> <span data-ttu-id="440fb-136">Accédez à **Paramètres de l’appareil > Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="440fb-136">Go to **Device settings > Security**.</span></span>
2. <span data-ttu-id="440fb-137">Dans le panneau **Paramètres de sécurité**, cliquez sur **Gestion à distance**.</span><span class="sxs-lookup"><span data-stu-id="440fb-137">In the **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="440fb-138">Dans le panneau **Gestion à distance**, définissez **Activer la gestion à distance** sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="440fb-138">In the **Remote management** blade, set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="440fb-139">Vous pouvez maintenant choisir de vous connecter à l’aide de HTTP.</span><span class="sxs-lookup"><span data-stu-id="440fb-139">You can now choose to connect using HTTP.</span></span> <span data-ttu-id="440fb-140">(Le choix par défaut est de se connecter via HTTPS.) Assurez-vous que HTTP est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="440fb-140">(The default is to connect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="440fb-141">Une connexion via HTTP est acceptable uniquement sur des réseaux approuvés.</span><span class="sxs-lookup"><span data-stu-id="440fb-141">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   
5. <span data-ttu-id="440fb-142">Cliquez sur **Enregistrer** puis, lorsque vous êtes invité à confirmer l’opération, sélectionnez **Oui**.</span><span class="sxs-lookup"><span data-stu-id="440fb-142">Click **Save** and when prompted for confirmation, select **Yes**.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-http"></a><span data-ttu-id="440fb-143">Utiliser la console série pour activer la gestion à distance via HTTP</span><span class="sxs-lookup"><span data-stu-id="440fb-143">Use the serial console to enable remote management over HTTP</span></span>
<span data-ttu-id="440fb-144">Procédez comme suit sur la console série de l’appareil pour activer la gestion à distance.</span><span class="sxs-lookup"><span data-stu-id="440fb-144">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="440fb-145">Pour activer la gestion à distance via la console série de l’appareil</span><span class="sxs-lookup"><span data-stu-id="440fb-145">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="440fb-146">Dans le menu de la console série, sélectionnez l’option 1.</span><span class="sxs-lookup"><span data-stu-id="440fb-146">On the serial console menu, select option 1.</span></span> <span data-ttu-id="440fb-147">Pour plus d’informations sur l’utilisation de la console série sur l’appareil, consultez [Se connecter à Windows PowerShell pour StorSimple via la console série de l’appareil](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="440fb-147">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="440fb-148">À l’invite, tapez : `Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="440fb-148">At the prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="440fb-149">Vous êtes averti des vulnérabilités de sécurité résultant de l’utilisation de HTTP pour se connecter à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="440fb-149">You are notified about the security vulnerabilities of using HTTP to connect to the device.</span></span> <span data-ttu-id="440fb-150">Quand vous y êtes invité, confirmez en tapant **O**.</span><span class="sxs-lookup"><span data-stu-id="440fb-150">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="440fb-151">Vérifiez que HTTP est activé en tapant : `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="440fb-151">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="440fb-152">Vérifiez que le champ **RemoteManagementMode** affiche **HttpsAndHttpEnabled**. L’illustration suivante montre ces paramètres dans PuTTY.</span><span class="sxs-lookup"><span data-stu-id="440fb-152">Verify that the **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![HTTPS et HTTP en série activés](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-the-client-for-remote-connection"></a><span data-ttu-id="440fb-154">Préparer le client pour une connexion à distance</span><span class="sxs-lookup"><span data-stu-id="440fb-154">Prepare the client for remote connection</span></span>
<span data-ttu-id="440fb-155">Procédez comme suit sur le client pour activer la gestion à distance.</span><span class="sxs-lookup"><span data-stu-id="440fb-155">Perform the following steps on the client to enable remote management.</span></span>

#### <a name="to-prepare-the-client-for-remote-connection"></a><span data-ttu-id="440fb-156">Pour préparer le client pour une connexion à distance</span><span class="sxs-lookup"><span data-stu-id="440fb-156">To prepare the client for remote connection</span></span>
1. <span data-ttu-id="440fb-157">Démarrez une session Windows PowerShell en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="440fb-157">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="440fb-158">Tapez la commande suivante pour ajouter l’adresse IP de l’appareil StorSimple à la liste des hôtes approuvés du client :</span><span class="sxs-lookup"><span data-stu-id="440fb-158">Type the following command to add the IP address of the StorSimple device to the client’s trusted hosts list:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="440fb-159">Remplacez <*device_ip*> par l’adresse IP de votre appareil, par exemple :</span><span class="sxs-lookup"><span data-stu-id="440fb-159">Replace <*device_ip*> with the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="440fb-160">Tapez la commande suivante pour enregistrer les informations d’identification de l’appareil dans une variable :</span><span class="sxs-lookup"><span data-stu-id="440fb-160">Type the following command to save the device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="440fb-161">Dans la boîte de dialogue qui s’affiche :</span><span class="sxs-lookup"><span data-stu-id="440fb-161">In the dialog box that appears:</span></span>
   
   1. <span data-ttu-id="440fb-162">Entrez le nom d’utilisateur au format : *adresse_IP_appareil\AdministrateurSS*.</span><span class="sxs-lookup"><span data-stu-id="440fb-162">Type the user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="440fb-163">Tapez le mot de passe de l’administrateur de l’appareil qui a été défini quand l’appareil a été configuré avec l’Assistant Installation.</span><span class="sxs-lookup"><span data-stu-id="440fb-163">Type the device administrator password that was set when the device was configured with the setup wizard.</span></span> <span data-ttu-id="440fb-164">Le mot de passe par défaut est *Password1*.</span><span class="sxs-lookup"><span data-stu-id="440fb-164">The default password is *Password1*.</span></span>
5. <span data-ttu-id="440fb-165">Démarrez une session Windows PowerShell sur l’appareil en tapant cette commande :</span><span class="sxs-lookup"><span data-stu-id="440fb-165">Start a Windows PowerShell session on the device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="440fb-166">Pour créer une session Windows PowerShell pour une utilisation avec l’appareil virtuel StorSimple, ajoutez le paramètre `–Port` et spécifiez le port public que vous avez configuré dans l’accès distant pour l’appliance virtuelle StorSimple.</span><span class="sxs-lookup"><span data-stu-id="440fb-166">To create a Windows PowerShell session for use with the StorSimple virtual device, append the `–Port` parameter and specify the public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   
   
<span data-ttu-id="440fb-167">À ce stade, vous devez normalement disposer d’une session Windows PowerShell à distance active sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="440fb-167">At this point, you should have an active remote Windows PowerShell session to the device.</span></span>
   
![Accès distant PowerShell en utilisant HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="440fb-169">Se connecter via HTTPS</span><span class="sxs-lookup"><span data-stu-id="440fb-169">Connect through HTTPS</span></span>

<span data-ttu-id="440fb-170">La connexion à Windows PowerShell pour StorSimple via une session HTTPS est la méthode la plus sécurisée et elle est recommandée pour la connexion à distance à votre appareil Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="440fb-170">Connecting to Windows PowerShell for StorSimple through an HTTPS session is the most secure and recommended method of remotely connecting to your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="440fb-171">Les procédures suivantes expliquent comment configurer la console série et les ordinateurs clients pour pouvoir utiliser HTTPS pour se connecter à Windows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="440fb-171">The following procedures explain how to set up the serial console and client computers so that you can use HTTPS to connect to Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="440fb-172">Vous pouvez utiliser le portail Azure ou la console série pour configurer la gestion à distance.</span><span class="sxs-lookup"><span data-stu-id="440fb-172">You can use either the Azure portal or the serial console to configure remote management.</span></span> <span data-ttu-id="440fb-173">Choisissez parmi les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="440fb-173">Select from the following procedures:</span></span>

* [<span data-ttu-id="440fb-174">Utiliser le portail Azure pour activer la gestion à distance via HTTPS</span><span class="sxs-lookup"><span data-stu-id="440fb-174">Use the Azure portal to enable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="440fb-175">Utiliser la console série pour activer la gestion à distance via HTTPS</span><span class="sxs-lookup"><span data-stu-id="440fb-175">Use the serial console to enable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="440fb-176">Après avoir activé la gestion à distance, utilisez les procédures suivantes pour préparer l’hôte pour la gestion à distance et pour se connecter à l’appareil à partir de l’hôte distant.</span><span class="sxs-lookup"><span data-stu-id="440fb-176">After you enable remote management, use the following procedures to prepare the host for a remote management and connect to the device from the remote host.</span></span>

* [<span data-ttu-id="440fb-177">Préparer l’hôte pour la gestion à distance</span><span class="sxs-lookup"><span data-stu-id="440fb-177">Prepare the host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="440fb-178">Se connecter à l’appareil à partir de l’hôte distant</span><span class="sxs-lookup"><span data-stu-id="440fb-178">Connect to the device from the remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-the-azure-portal-to-enable-remote-management-over-https"></a><span data-ttu-id="440fb-179">Utiliser le portail Azure pour activer la gestion à distance via HTTPS</span><span class="sxs-lookup"><span data-stu-id="440fb-179">Use the Azure portal to enable remote management over HTTPS</span></span>

<span data-ttu-id="440fb-180">Procédez comme suit dans le portail Azure pour activer la gestion à distance via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="440fb-180">Perform the following steps in the Azure portal to enable remote management over HTTPS.</span></span>

#### <a name="to-enable-remote-management-over-https-from-the-azure-portal"></a><span data-ttu-id="440fb-181">Pour activer la gestion à distance via HTTPS à partir du portail Azure</span><span class="sxs-lookup"><span data-stu-id="440fb-181">To enable remote management over HTTPS from the Azure portal</span></span>

1. <span data-ttu-id="440fb-182">Accédez à votre service StorSimple Device Manager.</span><span class="sxs-lookup"><span data-stu-id="440fb-182">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="440fb-183">Sélectionnez **Appareils**, puis cliquez sur l’appareil à configurer pour la gestion à distance.</span><span class="sxs-lookup"><span data-stu-id="440fb-183">Select **Devices** and then select and click the device you want to configure for remote management.</span></span> <span data-ttu-id="440fb-184">Accédez à **Paramètres de l’appareil > Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="440fb-184">Go to **Device settings > Security**.</span></span>
2. <span data-ttu-id="440fb-185">Dans le panneau **Paramètres de sécurité**, cliquez sur **Gestion à distance**.</span><span class="sxs-lookup"><span data-stu-id="440fb-185">In the **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="440fb-186">Définissez **Activer la gestion à distance** sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="440fb-186">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="440fb-187">Vous pouvez maintenant choisir de vous connecter via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="440fb-187">You can now choose to connect using HTTPS.</span></span> <span data-ttu-id="440fb-188">(Le choix par défaut est de se connecter via HTTPS.) Assurez-vous que HTTPS est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="440fb-188">(The default is to connect over HTTPS.) Make sure that HTTPS is selected.</span></span>
5. <span data-ttu-id="440fb-189">Cliquez sur ... puis sur **Télécharger le certificat de gestion à distance**.</span><span class="sxs-lookup"><span data-stu-id="440fb-189">Click ... and then click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="440fb-190">Spécifiez un emplacement pour enregistrer ce fichier.</span><span class="sxs-lookup"><span data-stu-id="440fb-190">Specify a location to save this file.</span></span> <span data-ttu-id="440fb-191">Vous devez installer ce certificat sur l’ordinateur client ou sur l’ordinateur hôte que vous utiliserez pour vous connecter à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="440fb-191">You need to install this certificate on the client or host computer that you will use to connect to the device.</span></span>
6. <span data-ttu-id="440fb-192">Cliquez sur **Enregistrer**, puis cliquez sur **Oui** lorsque vous êtes invité à confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="440fb-192">Click **Save** and then click **Yes** when prompted for confirmation.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-https"></a><span data-ttu-id="440fb-193">Utiliser la console série pour activer la gestion à distance via HTTPS</span><span class="sxs-lookup"><span data-stu-id="440fb-193">Use the serial console to enable remote management over HTTPS</span></span>

<span data-ttu-id="440fb-194">Procédez comme suit sur la console série de l’appareil pour activer la gestion à distance.</span><span class="sxs-lookup"><span data-stu-id="440fb-194">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="440fb-195">Pour activer la gestion à distance via la console série de l’appareil</span><span class="sxs-lookup"><span data-stu-id="440fb-195">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="440fb-196">Dans le menu de la console série, sélectionnez l’option 1.</span><span class="sxs-lookup"><span data-stu-id="440fb-196">On the serial console menu, select option 1.</span></span> <span data-ttu-id="440fb-197">Pour plus d’informations sur l’utilisation de la console série sur l’appareil, consultez [Se connecter à Windows PowerShell pour StorSimple via la console série de l’appareil](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="440fb-197">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="440fb-198">À l’invite, tapez : </span><span class="sxs-lookup"><span data-stu-id="440fb-198">At the prompt, type:</span></span>
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="440fb-199">Ceci doit normalement activer HTTPS sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="440fb-199">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="440fb-200">Vérifiez que HTTPS a été activé en tapant :</span><span class="sxs-lookup"><span data-stu-id="440fb-200">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="440fb-201">Vérifiez que le champ **RemoteManagementMode** affiche **HttpsEnabled**. L’illustration suivante montre ces paramètres dans PuTTY.</span><span class="sxs-lookup"><span data-stu-id="440fb-201">Make sure that the **RemoteManagementMode** field shows **HttpsEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![HTTPS en série activé](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="440fb-203">Depuis la sortie de `Get-HcsSystem`, copiez le numéro de série de l’appareil et enregistrez-le pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="440fb-203">From the output of `Get-HcsSystem`, copy the serial number of the device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="440fb-204">Le numéro de série correspond au nom CN du certificat.</span><span class="sxs-lookup"><span data-stu-id="440fb-204">The serial number maps to the CN name in the certificate.</span></span>
   
5. <span data-ttu-id="440fb-205">Obtenez un certificat de gestion à distance en tapant :</span><span class="sxs-lookup"><span data-stu-id="440fb-205">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="440fb-206">Un certificat similaire à celui-ci apparaît.</span><span class="sxs-lookup"><span data-stu-id="440fb-206">A certificate similar to the following will appear.</span></span>
   
    ![Obtenir un certificat de gestion à distance](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="440fb-208">Copiez les informations du certificat de **-----BEGIN CERTIFICATE-----** à **-----END CERTIFICATE-----** dans un éditeur de texte comme le Bloc-notes et enregistrez-les dans un fichier .cer.</span><span class="sxs-lookup"><span data-stu-id="440fb-208">Copy the information in the certificate from **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="440fb-209">(Vous allez copier ce fichier sur votre hôte distant lors de la préparation de l’hôte).</span><span class="sxs-lookup"><span data-stu-id="440fb-209">(You will copy this file to your remote host when you prepare the host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="440fb-210">Pour générer un nouveau certificat, utilisez l’applet de commande `Set-HcsRemoteManagementCert`.</span><span class="sxs-lookup"><span data-stu-id="440fb-210">To generate a new certificate, use the `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   
### <a name="prepare-the-host-for-remote-management"></a><span data-ttu-id="440fb-211">Préparer l’hôte pour la gestion à distance</span><span class="sxs-lookup"><span data-stu-id="440fb-211">Prepare the host for remote management</span></span>

<span data-ttu-id="440fb-212">Pour préparer l’ordinateur hôte pour une connexion à distance qui utilise une session HTTPS, effectuez les procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="440fb-212">To prepare the host computer for a remote connection that uses an HTTPS session, perform the following procedures:</span></span>

* <span data-ttu-id="440fb-213">[Importez le fichier .cer dans le magasin racine du client ou de l’hôte distant](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="440fb-213">[Import the .cer file into the root store of the client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="440fb-214">[Ajoutez les numéros de série des appareils au fichier hosts sur l’hôte distant](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="440fb-214">[Add the device serial numbers to the hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="440fb-215">Chacune de ces procédures est décrite ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="440fb-215">Each of the preceding procedures, is described below.</span></span>

#### <a name="to-import-the-certificate-on-the-remote-host"></a><span data-ttu-id="440fb-216">Pour importer le certificat sur l’hôte distant</span><span class="sxs-lookup"><span data-stu-id="440fb-216">To import the certificate on the remote host</span></span>
1. <span data-ttu-id="440fb-217">Cliquez avec le bouton droit sur le fichier .cer et sélectionnez **Installer le certificat**.</span><span class="sxs-lookup"><span data-stu-id="440fb-217">Right-click the .cer file and select **Install certificate**.</span></span> <span data-ttu-id="440fb-218">L’Assistant Importation de certificat démarre.</span><span class="sxs-lookup"><span data-stu-id="440fb-218">This starts the Certificate Import Wizard.</span></span>
   
    ![Assistant Importation de certificat 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="440fb-220">Pour **Emplacement du magasin**, sélectionnez **Ordinateur local**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="440fb-220">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="440fb-221">Sélectionnez **Placer tous les certificats dans le magasin suivant**, puis cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="440fb-221">Select **Place all certificates in the following store**, and then click **Browse**.</span></span> <span data-ttu-id="440fb-222">Accédez au magasin racine de l’hôte distant, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="440fb-222">Navigate to the root store of your remote host, and then click **Next**.</span></span>
   
    ![Assistant Importation de certificat 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="440fb-224">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="440fb-224">Click **Finish**.</span></span> <span data-ttu-id="440fb-225">Un message indiquant que l’importation a réussi s’affiche.</span><span class="sxs-lookup"><span data-stu-id="440fb-225">A message that tells you that the import was successful appears.</span></span>
   
    ![Assistant Importation de certificat 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="to-add-device-serial-numbers-to-the-remote-host"></a><span data-ttu-id="440fb-227">Pour ajouter des numéros de série d’appareils à l’hôte distant</span><span class="sxs-lookup"><span data-stu-id="440fb-227">To add device serial numbers to the remote host</span></span>
1. <span data-ttu-id="440fb-228">Démarrez le Bloc-notes en tant qu’administrateur, puis ouvrez le fichier hosts qui se trouve dans \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="440fb-228">Start Notepad as an administrator, and then open the hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="440fb-229">Ajoutez les trois entrées suivantes à votre fichier hosts : **Adresse IP de DATA 0**, **Adresse IP fixe du contrôleur 0** et **Adresse IP fixe du contrôleur 1**.</span><span class="sxs-lookup"><span data-stu-id="440fb-229">Add the following three entries to your hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="440fb-230">Entrez le numéro de série de l’appareil que vous avez enregistré précédemment.</span><span class="sxs-lookup"><span data-stu-id="440fb-230">Enter the device serial number that you saved earlier.</span></span> <span data-ttu-id="440fb-231">Mappez ceci à l’adresse IP, comme le montre l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="440fb-231">Map this to the IP address as shown in the following image.</span></span> <span data-ttu-id="440fb-232">Pour Contrôleur 0 et Contrôleur 1, ajoutez **Controller0** et **Controller1** à la fin du numéro de série (nom CN).</span><span class="sxs-lookup"><span data-stu-id="440fb-232">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at the end of the serial number (CN name).</span></span>
   
    ![Ajout du nom CN au fichier Hosts](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="440fb-234">Enregistrez le fichier hosts.</span><span class="sxs-lookup"><span data-stu-id="440fb-234">Save the hosts file.</span></span>

### <a name="connect-to-the-device-from-the-remote-host"></a><span data-ttu-id="440fb-235">Se connecter à l’appareil à partir de l’hôte distant</span><span class="sxs-lookup"><span data-stu-id="440fb-235">Connect to the device from the remote host</span></span>

<span data-ttu-id="440fb-236">Utilisez Windows PowerShell et SSL pour entrer dans une session SSAdmin sur votre appareil à partir d’un hôte ou d’un client distant.</span><span class="sxs-lookup"><span data-stu-id="440fb-236">Use Windows PowerShell and SSL to enter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="440fb-237">La session SSAdmin est mappée à l’option 1 dans le menu de la [console série](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="440fb-237">The SSAdmin session maps to option 1 in the [serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="440fb-238">Effectuez la procédure suivante sur l’ordinateur à partir duquel vous voulez établir la connexion Windows PowerShell à distance.</span><span class="sxs-lookup"><span data-stu-id="440fb-238">Perform the following procedure on the computer from which you want to make the remote Windows PowerShell connection.</span></span>

#### <a name="to-enter-an-ssadmin-session-on-the-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="440fb-239">Pour entrer dans une session SSAdmin sur l’appareil en utilisant Windows PowerShell et SSL</span><span class="sxs-lookup"><span data-stu-id="440fb-239">To enter an SSAdmin session on the device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="440fb-240">Démarrez une session Windows PowerShell en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="440fb-240">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="440fb-241">Ajoutez l’adresse IP de l’appareil aux hôtes approuvés du client en tapant :</span><span class="sxs-lookup"><span data-stu-id="440fb-241">Add the device IP address to the client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="440fb-242">où <*device_ip*> par l’adresse IP de votre appareil, par exemple :</span><span class="sxs-lookup"><span data-stu-id="440fb-242">Where <*device_ip*> is the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="440fb-243">Pour créer des informations d’identification, saisissez :</span><span class="sxs-lookup"><span data-stu-id="440fb-243">To create a new credential, type:</span></span>
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="440fb-244">Où <*IP of target device*> est l’adresse IP de DATA 0 pour votre appareil, par exemple **10.126.173.90** comme dans l’image précédente du fichier hosts.</span><span class="sxs-lookup"><span data-stu-id="440fb-244">Where <*IP of target device*> is the IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in the preceding image of the hosts file.</span></span> <span data-ttu-id="440fb-245">Spécifiez également le mot de passe administrateur pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="440fb-245">Also, supply the administrator password for your device.</span></span>
4. <span data-ttu-id="440fb-246">Créer une session en tapant :</span><span class="sxs-lookup"><span data-stu-id="440fb-246">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="440fb-247">Pour le paramètre -ComputerName de l’applet de commande, vous devez fournir le <*numéro de série de l’appareil cible*>.</span><span class="sxs-lookup"><span data-stu-id="440fb-247">For the -ComputerName parameter in the cmdlet, provide the <*serial number of target device*>.</span></span> <span data-ttu-id="440fb-248">Ce numéro de série a été mappé à l’adresse IP de DATA 0 dans le fichier hosts sur l’hôte distant, par exemple, **SHX0991003G44MT** dans l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="440fb-248">This serial number was mapped to the IP address of DATA 0 in the hosts file on your remote host; for example, **SHX0991003G44MT** as shown in the following image.</span></span>
5. <span data-ttu-id="440fb-249">Entrez :</span><span class="sxs-lookup"><span data-stu-id="440fb-249">Type:</span></span>
   
     `Enter-PSSession $session`
6. <span data-ttu-id="440fb-250">Patientez quelques minutes, puis vous serez connecté à votre appareil via HTTPS sur SSL.</span><span class="sxs-lookup"><span data-stu-id="440fb-250">You will need to wait a few minutes, and then you will be connected to your device via HTTPS over SSL.</span></span> <span data-ttu-id="440fb-251">Un message indiquant que vous êtes connecté à votre appareil s’affiche.</span><span class="sxs-lookup"><span data-stu-id="440fb-251">You see a message that indicates you are connected to your device.</span></span>
   
    ![Accès distant PowerShell en utilisant HTTPS et SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="440fb-253">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="440fb-253">Next steps</span></span>

* <span data-ttu-id="440fb-254">En savoir plus sur [l’utilisation de Windows PowerShell pour gérer votre appareil StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="440fb-254">Learn more about [using Windows PowerShell to administer your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="440fb-255">Découvrez plus en détail comment [utiliser le service StorSimple Device Manager pour gérer votre appareil StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="440fb-255">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

