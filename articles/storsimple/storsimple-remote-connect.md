---
title: "aaaConnect à distance à l’appareil StorSimple tooyour | Documents Microsoft"
description: "Explique comment tooconfigure votre appareil pour la gestion à distance et comment tooconnect tooWindows PowerShell pour StorSimple via HTTP ou HTTPS."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 55ed8fcdd997901301e0adc164a302216cde0332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a><span data-ttu-id="d6d91-103">Se connecter à distance les appareils tooyour StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="d6d91-103">Connect remotely tooyour StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="d6d91-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d6d91-104">Overview</span></span>
<span data-ttu-id="d6d91-105">Vous pouvez utiliser l’appareil StorSimple Windows PowerShell remoting tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="d6d91-105">You can use Windows PowerShell remoting tooconnect tooyour StorSimple device.</span></span> <span data-ttu-id="d6d91-106">Quand vous vous connectez de cette façon, vous ne voyez pas de menu.</span><span class="sxs-lookup"><span data-stu-id="d6d91-106">When you connect this way, you will not see a menu.</span></span> <span data-ttu-id="d6d91-107">(Vous consultez un menu uniquement si vous utilisez la console série de hello sur hello appareil tooconnect.) Avec accès à distance de Windows PowerShell, vous vous connectez tooa les instance d’exécution spécifique.</span><span class="sxs-lookup"><span data-stu-id="d6d91-107">(You see a menu only if you use hello serial console on hello device tooconnect.) With Windows PowerShell remoting, you connect tooa specific runspace.</span></span> <span data-ttu-id="d6d91-108">Vous pouvez également spécifier la langue d’affichage hello.</span><span class="sxs-lookup"><span data-stu-id="d6d91-108">You can also specify hello display language.</span></span> 

<span data-ttu-id="d6d91-109">Pour plus d’informations sur l’utilisation de Windows PowerShell remoting toomanage votre appareil, consultez trop[utiliser Windows PowerShell pour StorSimple tooadminister votre appareil StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d6d91-109">For more information about using Windows PowerShell remoting toomanage your device, go too[Use Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>

<span data-ttu-id="d6d91-110">Ce didacticiel explique comment tooconfigure votre appareil pour l’administration à distance et puis tooconnect tooWindows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d6d91-110">This tutorial explains how tooconfigure your device for remote management and then how tooconnect tooWindows PowerShell for StorSimple.</span></span> <span data-ttu-id="d6d91-111">Vous pouvez utiliser HTTP ou HTTPS tooconnect via la communication à distance de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d6d91-111">You can use HTTP or HTTPS tooconnect via Windows PowerShell remoting.</span></span> <span data-ttu-id="d6d91-112">Toutefois, lorsque vous décidez comment tooconnect tooWindows PowerShell pour StorSimple, considérez les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="d6d91-112">However, when you are deciding how tooconnect tooWindows PowerShell for StorSimple, consider hello following:</span></span> 

* <span data-ttu-id="d6d91-113">Connexion directe toohello console série du périphérique est sécurisé, mais il connexion console série toohello sur les commutateurs de réseau n’est pas.</span><span class="sxs-lookup"><span data-stu-id="d6d91-113">Connecting directly toohello device serial console is secure, but connecting toohello serial console over network switches is not.</span></span> <span data-ttu-id="d6d91-114">Soyez prudent hello des risques de sécurité lors de la connexion de la console série du périphérique toohello sur les commutateurs réseau.</span><span class="sxs-lookup"><span data-stu-id="d6d91-114">Be cautious of hello security risk when connecting toohello device serial console over network switches.</span></span> 
* <span data-ttu-id="d6d91-115">Connexion via une session HTTP peut offrir davantage de sécurité que la connexion via la console série de hello réseau hello.</span><span class="sxs-lookup"><span data-stu-id="d6d91-115">Connecting through an HTTP session might offer more security than connecting through hello serial console over hello network.</span></span> <span data-ttu-id="d6d91-116">Bien que cela n’est pas la méthode hello plus sécurisée, il est acceptable sur des réseaux approuvés.</span><span class="sxs-lookup"><span data-stu-id="d6d91-116">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span> 
* <span data-ttu-id="d6d91-117">La connexion via une session HTTPS avec un certificat auto-signé est hello plus sûre et hello option recommandée.</span><span class="sxs-lookup"><span data-stu-id="d6d91-117">Connecting through an HTTPS session with a self-signed certificate is hello most secure and hello recommended option.</span></span>

<span data-ttu-id="d6d91-118">Vous pouvez vous connecter à distance interface Windows PowerShell de toohello.</span><span class="sxs-lookup"><span data-stu-id="d6d91-118">You can connect remotely toohello Windows PowerShell interface.</span></span> <span data-ttu-id="d6d91-119">Cependant, l’appareil StorSimple tooyour accès à distance via l’interface Windows PowerShell de hello n’est pas activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="d6d91-119">However, remote access tooyour StorSimple device via hello Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="d6d91-120">Vous devez tooenable la gestion à distance sur l’appareil de hello tout d’abord et que vous puis sur hello client qui est utilisé tooaccess votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d6d91-120">You need tooenable remote management on hello device first, and then on hello client that is used tooaccess your device.</span></span>

<span data-ttu-id="d6d91-121">les étapes de Hello décrites dans cet article ont été effectuées sur un système hôte exécutant Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="d6d91-121">hello steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="d6d91-122">Se connecter via HTTP</span><span class="sxs-lookup"><span data-stu-id="d6d91-122">Connect through HTTP</span></span>
<span data-ttu-id="d6d91-123">Connexion tooWindows PowerShell pour StorSimple via une session HTTP offre davantage de sécurité que la connexion via la console série de hello de votre appareil StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d6d91-123">Connecting tooWindows PowerShell for StorSimple through an HTTP session offers more security than connecting through hello serial console of your StorSimple device.</span></span> <span data-ttu-id="d6d91-124">Bien que cela n’est pas la méthode hello plus sécurisée, il est acceptable sur des réseaux approuvés.</span><span class="sxs-lookup"><span data-stu-id="d6d91-124">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="d6d91-125">Vous pouvez utiliser hello portail Azure classic ou gestion à distance du tooconfigure hello console série.</span><span class="sxs-lookup"><span data-stu-id="d6d91-125">You can use either hello Azure classic portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="d6d91-126">Sélectionnez hello procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="d6d91-126">Select from hello following procedures:</span></span>

* [<span data-ttu-id="d6d91-127">Utiliser la gestion à distance de tooenable de portail classique Azure hello sur HTTP</span><span class="sxs-lookup"><span data-stu-id="d6d91-127">Use hello Azure classic portal tooenable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="d6d91-128">Utiliser la gestion à distance de hello console série tooenable sur HTTP</span><span class="sxs-lookup"><span data-stu-id="d6d91-128">Use hello serial console tooenable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="d6d91-129">Après avoir activé la gestion à distance, utilisez hello suivant la procédure tooprepare hello du client pour une connexion à distance.</span><span class="sxs-lookup"><span data-stu-id="d6d91-129">After you enable remote management, use hello following procedure tooprepare hello client for a remote connection.</span></span>

* [<span data-ttu-id="d6d91-130">Préparer le client de hello pour la connexion à distance</span><span class="sxs-lookup"><span data-stu-id="d6d91-130">Prepare hello client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-http"></a><span data-ttu-id="d6d91-131">Utiliser la gestion à distance de tooenable de portail classique Azure hello sur HTTP</span><span class="sxs-lookup"><span data-stu-id="d6d91-131">Use hello Azure classic portal tooenable remote management over HTTP</span></span>
<span data-ttu-id="d6d91-132">Effectuer hello suivant les étapes de gestion à distance de tooenable de portail classique Azure hello sur HTTP.</span><span class="sxs-lookup"><span data-stu-id="d6d91-132">Perform hello following steps in hello Azure classic portal tooenable remote management over HTTP.</span></span>

#### <a name="tooenable-remote-management-through-hello-azure-classic-portal"></a><span data-ttu-id="d6d91-133">tooenable de gestion à distance via le portail Azure classic de hello</span><span class="sxs-lookup"><span data-stu-id="d6d91-133">tooenable remote management through hello Azure classic portal</span></span>
1. <span data-ttu-id="d6d91-134">Accédez à **Appareils** > **Configurer** pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d6d91-134">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="d6d91-135">Faites défiler vers le bas toohello **gestion à distance** section.</span><span class="sxs-lookup"><span data-stu-id="d6d91-135">Scroll down toohello **Remote Management** section.</span></span>
3. <span data-ttu-id="d6d91-136">Définissez **activer la gestion à distance** trop**Oui**.</span><span class="sxs-lookup"><span data-stu-id="d6d91-136">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="d6d91-137">Vous pouvez maintenant choisir tooconnect à l’aide de HTTP.</span><span class="sxs-lookup"><span data-stu-id="d6d91-137">You can now choose tooconnect using HTTP.</span></span> <span data-ttu-id="d6d91-138">(valeur par défaut hello est tooconnect via le protocole HTTPS). Assurez-vous que HTTP est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="d6d91-138">(hello default is tooconnect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d6d91-139">Une connexion via HTTP est acceptable uniquement sur des réseaux approuvés.</span><span class="sxs-lookup"><span data-stu-id="d6d91-139">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   > 
   > 
5. <span data-ttu-id="d6d91-140">Cliquez sur **enregistrer** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="d6d91-140">Click **Save** at hello bottom of hello page.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a><span data-ttu-id="d6d91-141">Utiliser la gestion à distance de hello console série tooenable sur HTTP</span><span class="sxs-lookup"><span data-stu-id="d6d91-141">Use hello serial console tooenable remote management over HTTP</span></span>
<span data-ttu-id="d6d91-142">Effectuer hello hello gestion des appareils console série tooenable à distance comme suit.</span><span class="sxs-lookup"><span data-stu-id="d6d91-142">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="d6d91-143">tooenable de gestion à distance via la console série du périphérique hello</span><span class="sxs-lookup"><span data-stu-id="d6d91-143">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="d6d91-144">Dans le menu de console série hello, sélectionnez l’option 1.</span><span class="sxs-lookup"><span data-stu-id="d6d91-144">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="d6d91-145">Pour plus d’informations sur l’utilisation de la console série de hello sur l’appareil de hello, accédez trop[connecter tooWindows PowerShell pour StorSimple via la console série du périphérique](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d6d91-145">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="d6d91-146">À l’invite de hello, tapez :`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="d6d91-146">At hello prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="d6d91-147">Vous serez notifié des failles de sécurité hello de l’unité de toohello tooconnect HTTP.</span><span class="sxs-lookup"><span data-stu-id="d6d91-147">You will be notified about hello security vulnerabilities of using HTTP tooconnect toohello device.</span></span> <span data-ttu-id="d6d91-148">Quand vous y êtes invité, confirmez en tapant **O**.</span><span class="sxs-lookup"><span data-stu-id="d6d91-148">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="d6d91-149">Vérifiez que HTTP est activé en tapant : `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="d6d91-149">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="d6d91-150">Vérifiez que hello **RemoteManagementMode** champ indique **HttpsAndHttpEnabled**.hello après l’illustration montre ces paramètres dans PuTTY.</span><span class="sxs-lookup"><span data-stu-id="d6d91-150">Verify that hello **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![HTTPS et HTTP en série activés](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a><span data-ttu-id="d6d91-152">Préparer le client de hello pour la connexion à distance</span><span class="sxs-lookup"><span data-stu-id="d6d91-152">Prepare hello client for remote connection</span></span>
<span data-ttu-id="d6d91-153">Effectuer hello sur la gestion à distance de hello client tooenable comme suit.</span><span class="sxs-lookup"><span data-stu-id="d6d91-153">Perform hello following steps on hello client tooenable remote management.</span></span>

#### <a name="tooprepare-hello-client-for-remote-connection"></a><span data-ttu-id="d6d91-154">client de hello tooprepare pour la connexion à distance</span><span class="sxs-lookup"><span data-stu-id="d6d91-154">tooprepare hello client for remote connection</span></span>
1. <span data-ttu-id="d6d91-155">Démarrez une session Windows PowerShell en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d6d91-155">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="d6d91-156">Tapez hello commande tooadd hello IP adresse de la liste des hôtes approuvés du client toohello hello StorSimple périphérique suivante :</span><span class="sxs-lookup"><span data-stu-id="d6d91-156">Type hello following command tooadd hello IP address of hello StorSimple device toohello client’s trusted hosts list:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="d6d91-157">Remplacez <*device_ip*> avec l’adresse IP de hello de votre appareil, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6d91-157">Replace <*device_ip*> with hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="d6d91-158">Tapez ce qui suit hello toosave hello appareil informations d’identification dans une variable de commande :</span><span class="sxs-lookup"><span data-stu-id="d6d91-158">Type hello following command toosave hello device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="d6d91-159">Dans la boîte de dialogue hello qui s’affiche :</span><span class="sxs-lookup"><span data-stu-id="d6d91-159">In hello dialog box that appears:</span></span>
   
   1. <span data-ttu-id="d6d91-160">Nom d’utilisateur de type hello dans ce format : *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="d6d91-160">Type hello user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="d6d91-161">Tapez le mot de passe administrateur de périphérique hello qui a été défini lors de l’appareil de hello a été configuré avec l’Assistant Installation de hello.</span><span class="sxs-lookup"><span data-stu-id="d6d91-161">Type hello device administrator password that was set when hello device was configured with hello setup wizard.</span></span> <span data-ttu-id="d6d91-162">mot de passe Hello *Password1*.</span><span class="sxs-lookup"><span data-stu-id="d6d91-162">hello default password is *Password1*.</span></span>
5. <span data-ttu-id="d6d91-163">Démarrer une session Windows PowerShell sur l’appareil de hello en tapant cette commande :</span><span class="sxs-lookup"><span data-stu-id="d6d91-163">Start a Windows PowerShell session on hello device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="d6d91-164">toocreate une session Windows PowerShell pour une utilisation avec un appareil virtuel StorSimple de hello, ajouter hello `–Port` paramètre et spécifiez le port public hello que vous avez configuré dans la communication à distance pour un équipement virtuel StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d6d91-164">toocreate a Windows PowerShell session for use with hello StorSimple virtual device, append hello `–Port` parameter and specify hello public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   > 
   > 
   
     <span data-ttu-id="d6d91-165">À ce stade, vous devez disposer d’un appareil actif toohello de session à distance Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d6d91-165">At this point, you should have an active remote Windows PowerShell session toohello device.</span></span>
   
    ![Accès distant PowerShell en utilisant HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="d6d91-167">Se connecter via HTTPS</span><span class="sxs-lookup"><span data-stu-id="d6d91-167">Connect through HTTPS</span></span>
<span data-ttu-id="d6d91-168">Connexion tooWindows PowerShell pour StorSimple via une session HTTPS est hello plus sûre et la méthode de connexion à distance appareil de Microsoft Azure StorSimple tooyour recommandée.</span><span class="sxs-lookup"><span data-stu-id="d6d91-168">Connecting tooWindows PowerShell for StorSimple through an HTTPS session is hello most secure and recommended method of remotely connecting tooyour Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="d6d91-169">Hello procédures suivantes explique comment tooset des hello séries console et les ordinateurs clients afin que vous puissiez utiliser HTTPS tooconnect tooWindows PowerShell pour StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d6d91-169">hello following procedures explain how tooset up hello serial console and client computers so that you can use HTTPS tooconnect tooWindows PowerShell for StorSimple.</span></span>

<span data-ttu-id="d6d91-170">Vous pouvez utiliser hello portail Azure classic ou gestion à distance du tooconfigure hello console série.</span><span class="sxs-lookup"><span data-stu-id="d6d91-170">You can use either hello Azure classic portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="d6d91-171">Sélectionnez hello procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="d6d91-171">Select from hello following procedures:</span></span>

* [<span data-ttu-id="d6d91-172">Utiliser la gestion à distance de tooenable de portail classique Azure hello sur HTTPS</span><span class="sxs-lookup"><span data-stu-id="d6d91-172">Use hello Azure classic portal tooenable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="d6d91-173">Utiliser la gestion à distance de hello console série tooenable sur HTTPS</span><span class="sxs-lookup"><span data-stu-id="d6d91-173">Use hello serial console tooenable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="d6d91-174">Après avoir activé la gestion à distance, utilisez hello suivant les procédures tooprepare hello ordinateur hôte pour une gestion à distance et se connecter toohello appareil à partir de l’hôte distant de hello.</span><span class="sxs-lookup"><span data-stu-id="d6d91-174">After you enable remote management, use hello following procedures tooprepare hello host for a remote management and connect toohello device from hello remote host.</span></span>

* [<span data-ttu-id="d6d91-175">Préparer l’hôte de hello pour la gestion à distance</span><span class="sxs-lookup"><span data-stu-id="d6d91-175">Prepare hello host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="d6d91-176">Se connecter toohello appareil à partir de l’hôte distant de hello</span><span class="sxs-lookup"><span data-stu-id="d6d91-176">Connect toohello device from hello remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-https"></a><span data-ttu-id="d6d91-177">Utiliser la gestion à distance de tooenable de portail classique Azure hello sur HTTPS</span><span class="sxs-lookup"><span data-stu-id="d6d91-177">Use hello Azure classic portal tooenable remote management over HTTPS</span></span>
<span data-ttu-id="d6d91-178">Effectuer hello suivant les étapes de gestion à distance de hello tooenable de portail classique Azure via le protocole HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d6d91-178">Perform hello following steps in hello Azure classic portal tooenable remote management over HTTPS.</span></span>

#### <a name="tooenable-remote-management-over-https-from-hello-azure-classic-portal"></a><span data-ttu-id="d6d91-179">tooenable de gestion à distance via HTTPS à partir de hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="d6d91-179">tooenable remote management over HTTPS from hello Azure classic portal</span></span>
1. <span data-ttu-id="d6d91-180">Accédez à **Appareils** > **Configurer** pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d6d91-180">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="d6d91-181">Faites défiler vers le bas toohello **gestion à distance** section.</span><span class="sxs-lookup"><span data-stu-id="d6d91-181">Scroll down toohello **Remote Management** section.</span></span>
3. <span data-ttu-id="d6d91-182">Définissez **activer la gestion à distance** trop**Oui**.</span><span class="sxs-lookup"><span data-stu-id="d6d91-182">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="d6d91-183">Vous pouvez maintenant choisir tooconnect à l’aide de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d6d91-183">You can now choose tooconnect using HTTPS.</span></span> <span data-ttu-id="d6d91-184">(valeur par défaut hello est tooconnect via le protocole HTTPS). Assurez-vous que HTTPS est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="d6d91-184">(hello default is tooconnect over HTTPS.) Make sure that HTTPS is selected.</span></span> 
5. <span data-ttu-id="d6d91-185">Cliquez sur **Télécharger le certificat de gestion à distance**.</span><span class="sxs-lookup"><span data-stu-id="d6d91-185">Click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="d6d91-186">Spécifiez un emplacement toosave ce fichier.</span><span class="sxs-lookup"><span data-stu-id="d6d91-186">Specify a location toosave this file.</span></span> <span data-ttu-id="d6d91-187">Vous devez tooinstall ce certificat sur l’ordinateur client ou l’hôte de hello que vous allez utiliser tooconnect toohello appareil.</span><span class="sxs-lookup"><span data-stu-id="d6d91-187">You will need tooinstall this certificate on hello client or host computer that you will use tooconnect toohello device.</span></span>
6. <span data-ttu-id="d6d91-188">Cliquez sur **enregistrer** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="d6d91-188">Click **Save** at hello bottom of hello page.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a><span data-ttu-id="d6d91-189">Utiliser la gestion à distance de hello console série tooenable sur HTTPS</span><span class="sxs-lookup"><span data-stu-id="d6d91-189">Use hello serial console tooenable remote management over HTTPS</span></span>
<span data-ttu-id="d6d91-190">Effectuer hello hello gestion des appareils console série tooenable à distance comme suit.</span><span class="sxs-lookup"><span data-stu-id="d6d91-190">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="d6d91-191">tooenable de gestion à distance via la console série du périphérique hello</span><span class="sxs-lookup"><span data-stu-id="d6d91-191">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="d6d91-192">Dans le menu de console série hello, sélectionnez l’option 1.</span><span class="sxs-lookup"><span data-stu-id="d6d91-192">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="d6d91-193">Pour plus d’informations sur l’utilisation de la console série de hello sur l’appareil de hello, accédez trop[connecter tooWindows PowerShell pour StorSimple via la console série du périphérique](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="d6d91-193">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="d6d91-194">À l’invite de hello, tapez :</span><span class="sxs-lookup"><span data-stu-id="d6d91-194">At hello prompt, type:</span></span> 
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="d6d91-195">Ceci doit normalement activer HTTPS sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d6d91-195">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="d6d91-196">Vérifiez que HTTPS a été activé en tapant :</span><span class="sxs-lookup"><span data-stu-id="d6d91-196">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="d6d91-197">Vérifiez que hello **RemoteManagementMode** champ indique **HttpsEnabled**.hello après l’illustration montre ces paramètres dans PuTTY.</span><span class="sxs-lookup"><span data-stu-id="d6d91-197">Make sure that hello **RemoteManagementMode** field shows **HttpsEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![HTTPS en série activé](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="d6d91-199">À partir de la sortie de hello de `Get-HcsSystem`, copiez le numéro de série hello du périphérique de hello et l’enregistrer pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d6d91-199">From hello output of `Get-HcsSystem`, copy hello serial number of hello device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d6d91-200">numéro de série Hello mappe le nom CN de toohello dans le certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="d6d91-200">hello serial number maps toohello CN name in hello certificate.</span></span>
   > 
   > 
5. <span data-ttu-id="d6d91-201">Obtenez un certificat de gestion à distance en tapant :</span><span class="sxs-lookup"><span data-stu-id="d6d91-201">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="d6d91-202">Une similaire toohello suivant du certificat s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d6d91-202">A certificate similar toohello following will appear.</span></span>
   
    ![Obtenir un certificat de gestion à distance](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="d6d91-204">Copier les informations de hello certificat hello de **---BEGIN CERTIFICATE---** trop**---END CERTIFICATE---** dans un éditeur de texte tel que le bloc-notes et enregistrez-le en tant que fichier .cer.</span><span class="sxs-lookup"><span data-stu-id="d6d91-204">Copy hello information in hello certificate from **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="d6d91-205">(Vous allez copier cet hôte distant tooyour de fichier lorsque vous préparez l’ordinateur hôte de hello.)</span><span class="sxs-lookup"><span data-stu-id="d6d91-205">(You will copy this file tooyour remote host when you prepare hello host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d6d91-206">toogenerate un nouveau certificat, utilisez hello `Set-HcsRemoteManagementCert` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="d6d91-206">toogenerate a new certificate, use hello `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   > 
   > 

### <a name="prepare-hello-host-for-remote-management"></a><span data-ttu-id="d6d91-207">Préparer l’hôte de hello pour la gestion à distance</span><span class="sxs-lookup"><span data-stu-id="d6d91-207">Prepare hello host for remote management</span></span>
<span data-ttu-id="d6d91-208">l’ordinateur hôte pour une connexion à distance qui utilise une session HTTPS, tooprepare hello effectuer hello procédures suivantes :</span><span class="sxs-lookup"><span data-stu-id="d6d91-208">tooprepare hello host computer for a remote connection that uses an HTTPS session, perform hello following procedures:</span></span>

* <span data-ttu-id="d6d91-209">[Importer le fichier .cer hello dans le magasin racine de hello du client de hello ou un hôte distant](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="d6d91-209">[Import hello .cer file into hello root store of hello client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="d6d91-210">[Ajouter hello appareil des numéros de série toohello fichier hosts sur votre hôte distant](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="d6d91-210">[Add hello device serial numbers toohello hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="d6d91-211">Chacune de ces procédures est décrite ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d6d91-211">Each of these procedures is described below.</span></span>

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a><span data-ttu-id="d6d91-212">certificat de hello tooimport sur l’hôte distant de hello</span><span class="sxs-lookup"><span data-stu-id="d6d91-212">tooimport hello certificate on hello remote host</span></span>
1. <span data-ttu-id="d6d91-213">Avec le bouton droit de fichier .cer hello et sélectionnez **installer le certificat**.</span><span class="sxs-lookup"><span data-stu-id="d6d91-213">Right-click hello .cer file and select **Install certificate**.</span></span> <span data-ttu-id="d6d91-214">Ceci démarrera hello Assistant Importation de certificat.</span><span class="sxs-lookup"><span data-stu-id="d6d91-214">This will start hello Certificate Import Wizard.</span></span>
   
    ![Assistant Importation de certificat 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="d6d91-216">Pour **Emplacement du magasin**, sélectionnez **Ordinateur local**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="d6d91-216">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="d6d91-217">Sélectionnez **placer tous les certificats dans hello suivant magasin**, puis cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="d6d91-217">Select **Place all certificates in hello following store**, and then click **Browse**.</span></span> <span data-ttu-id="d6d91-218">Accédez magasin racine de toohello de votre hôte distant, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="d6d91-218">Navigate toohello root store of your remote host, and then click **Next**.</span></span>
   
    ![Assistant Importation de certificat 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="d6d91-220">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="d6d91-220">Click **Finish**.</span></span> <span data-ttu-id="d6d91-221">Un message vous indiquant que hello importation a réussi s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d6d91-221">A message that tells you that hello import was successful appears.</span></span>
   
    ![Assistant Importation de certificat 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a><span data-ttu-id="d6d91-223">hôte distant toohello des numéros de série du périphérique tooadd</span><span class="sxs-lookup"><span data-stu-id="d6d91-223">tooadd device serial numbers toohello remote host</span></span>
1. <span data-ttu-id="d6d91-224">Démarrez le bloc-notes en tant qu’administrateur, puis ouvrez le fichier d’hôtes hello situé dans \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="d6d91-224">Start Notepad as an administrator, and then open hello hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="d6d91-225">Ajouter hello trois entrées tooyour hôtes fichier suivant : **adresse IP de DATA 0**, **adresse IP fixe du contrôleur 0**, et **adresse IP fixe du contrôleur 1**.</span><span class="sxs-lookup"><span data-stu-id="d6d91-225">Add hello following three entries tooyour hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="d6d91-226">Entrez le numéro de série hello appareil que vous avez enregistré précédemment.</span><span class="sxs-lookup"><span data-stu-id="d6d91-226">Enter hello device serial number that you saved earlier.</span></span> <span data-ttu-id="d6d91-227">Mapper cette adresse IP de toohello comme indiqué dans hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="d6d91-227">Map this toohello IP address as shown in hello following image.</span></span> <span data-ttu-id="d6d91-228">Pour les contrôleurs 0 et 1, ajoutez **Controller0** et **Controller1** à fin hello hello au numéro de série (nom CN).</span><span class="sxs-lookup"><span data-stu-id="d6d91-228">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at hello end of hello serial number (CN name).</span></span>
   
    ![Ajout du fichier toohosts nom CN](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="d6d91-230">Enregistrer le fichier hôtes hello.</span><span class="sxs-lookup"><span data-stu-id="d6d91-230">Save hello hosts file.</span></span>

### <a name="connect-toohello-device-from-hello-remote-host"></a><span data-ttu-id="d6d91-231">Se connecter toohello appareil à partir de l’hôte distant de hello</span><span class="sxs-lookup"><span data-stu-id="d6d91-231">Connect toohello device from hello remote host</span></span>
<span data-ttu-id="d6d91-232">Utiliser Windows PowerShell et SSL tooenter une session SSAdmin sur votre appareil à partir d’un client ou un hôte distant.</span><span class="sxs-lookup"><span data-stu-id="d6d91-232">Use Windows PowerShell and SSL tooenter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="d6d91-233">session de Hello SSAdmin mappe toooption 1 Bonjour [console série](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d6d91-233">hello SSAdmin session maps toooption 1 in hello [serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="d6d91-234">Effectuer hello suivant la procédure sur l’ordinateur hello à partir de laquelle vous voulez toomake hello à distance Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d6d91-234">Perform hello following procedure on hello computer from which you want toomake hello remote Windows PowerShell connection.</span></span>

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="d6d91-235">tooenter une session SSAdmin sur l’appareil hello à l’aide de Windows PowerShell et SSL</span><span class="sxs-lookup"><span data-stu-id="d6d91-235">tooenter an SSAdmin session on hello device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="d6d91-236">Démarrez une session Windows PowerShell en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="d6d91-236">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="d6d91-237">Ajoutez hello appareil IP adresse toohello hôtes approuvés du client en tapant :</span><span class="sxs-lookup"><span data-stu-id="d6d91-237">Add hello device IP address toohello client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="d6d91-238">Où <*device_ip*> est l’adresse IP de hello de votre appareil, par exemple :</span><span class="sxs-lookup"><span data-stu-id="d6d91-238">Where <*device_ip*> is hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="d6d91-239">Créez des informations d’identification en tapant :</span><span class="sxs-lookup"><span data-stu-id="d6d91-239">Create a new credential by typing:</span></span> 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="d6d91-240">Où <*IP du périphérique cible*> est l’adresse IP de hello de DATA 0 pour votre appareil, par exemple, **10.126.173.90** comme indiqué dans hello précédant l’image du fichier d’hôtes hello.</span><span class="sxs-lookup"><span data-stu-id="d6d91-240">Where <*IP of target device*> is hello IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in hello preceding image of hello hosts file.</span></span> <span data-ttu-id="d6d91-241">Vous devez également fournir un mot de passe administrateur hello pour votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d6d91-241">Also, supply hello administrator password for your device.</span></span>
4. <span data-ttu-id="d6d91-242">Créer une session en tapant :</span><span class="sxs-lookup"><span data-stu-id="d6d91-242">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="d6d91-243">Pour le paramètre - ComputerName hello dans l’applet de commande hello fournir hello <*numéro de série du périphérique cible*>.</span><span class="sxs-lookup"><span data-stu-id="d6d91-243">For hello -ComputerName parameter in hello cmdlet, provide hello <*serial number of target device*>.</span></span> <span data-ttu-id="d6d91-244">Ce numéro de série a été mappé adresse toohello de DATA 0 dans le fichier d’hôtes hello sur votre hôte distant. par exemple, **SHX0991003G44MT** comme indiqué dans hello suivant l’image.</span><span class="sxs-lookup"><span data-stu-id="d6d91-244">This serial number was mapped toohello IP address of DATA 0 in hello hosts file on your remote host; for example, **SHX0991003G44MT** as shown in hello following image.</span></span>
5. <span data-ttu-id="d6d91-245">Entrez :</span><span class="sxs-lookup"><span data-stu-id="d6d91-245">Type:</span></span> 
   
     `Enter-PSSession $session`
6. <span data-ttu-id="d6d91-246">Vous devez toowait quelques minutes, et vous serez ensuite appareil tooyour connecté via HTTPS sur SSL.</span><span class="sxs-lookup"><span data-stu-id="d6d91-246">You will need toowait a few minutes, and then you will be connected tooyour device via HTTPS over SSL.</span></span> <span data-ttu-id="d6d91-247">Vous verrez un message indiquant que vous êtes connecté tooyour appareil.</span><span class="sxs-lookup"><span data-stu-id="d6d91-247">You will see a message that indicates you are connected tooyour device.</span></span>
   
    ![Accès distant PowerShell en utilisant HTTPS et SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="d6d91-249">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d6d91-249">Next steps</span></span>
* <span data-ttu-id="d6d91-250">En savoir plus sur [votre appareil StorSimple à l’aide de Windows PowerShell tooadminister](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d6d91-250">Learn more about [using Windows PowerShell tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="d6d91-251">En savoir plus sur [à l’aide de hello tooadminister du service StorSimple Manager votre appareil StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="d6d91-251">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

