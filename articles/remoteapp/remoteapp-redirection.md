---
title: "la redirection d’aaaUsing dans Azure RemoteApp | Documents Microsoft"
description: "Découvrez comment la redirection de tooconfigure et utilisation de RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a><span data-ttu-id="55d52-103">Utilisation de la redirection dans Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="55d52-103">Using redirection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="55d52-104">Azure RemoteApp ne sera plus disponible à partir du 31 août 2017.</span><span class="sxs-lookup"><span data-stu-id="55d52-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="55d52-105">Hello de lecture [annonce](https://go.microsoft.com/fwlink/?linkid=821148) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="55d52-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="55d52-106">La redirection du périphérique permet à vos utilisateurs interagissent avec les applications à distance à l’aide d’ordinateur local de hello périphériques attachés tootheir, téléphone ou tablette.</span><span class="sxs-lookup"><span data-stu-id="55d52-106">Device redirection lets your users interact with remote apps using hello devices attached tootheir local computer, phone, or tablet.</span></span> <span data-ttu-id="55d52-107">Par exemple, si vous avez fourni Skype via Azure RemoteApp, l’utilisateur doit caméra hello installée sur leur toowork PC avec Skype.</span><span class="sxs-lookup"><span data-stu-id="55d52-107">For example, if you have provided Skype through Azure RemoteApp, your user needs hello camera installed on their PC toowork with Skype.</span></span> <span data-ttu-id="55d52-108">Cela est également vrai pour les imprimantes, les haut-parleurs, les écrans et divers périphériques connectés à un port USB.</span><span class="sxs-lookup"><span data-stu-id="55d52-108">This is also true for printers, speakers, monitors, and a range of USB-connected peripherals.</span></span>

<span data-ttu-id="55d52-109">RemoteApp tire parti de la redirection de tooprovide de protocole RDP (Remote Desktop) et RemoteFX hello.</span><span class="sxs-lookup"><span data-stu-id="55d52-109">RemoteApp leverages hello Remote Desktop Protocol (RDP) and RemoteFX tooprovide redirection.</span></span>

## <a name="what-redirection-is-enabled-by-default"></a><span data-ttu-id="55d52-110">Quelle redirection est activée par défaut ?</span><span class="sxs-lookup"><span data-stu-id="55d52-110">What redirection is enabled by default?</span></span>
<span data-ttu-id="55d52-111">Lorsque vous utilisez RemoteApp, hello suit les redirections est activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="55d52-111">When you use RemoteApp, hello following redirections are enabled by default.</span></span> <span data-ttu-id="55d52-112">informations Hello entre parenthèses afficher les paramètres de protocole RDP hello.</span><span class="sxs-lookup"><span data-stu-id="55d52-112">hello information in parentheses show hello RDP setting.</span></span>

* <span data-ttu-id="55d52-113">Lire les sons sur l’ordinateur local de hello (**lire sur cet ordinateur**).</span><span class="sxs-lookup"><span data-stu-id="55d52-113">Play sounds on hello local computer (**Play on this computer**).</span></span> <span data-ttu-id="55d52-114">(audiomode:i:0)</span><span class="sxs-lookup"><span data-stu-id="55d52-114">(audiomode:i:0)</span></span>
* <span data-ttu-id="55d52-115">Capture audio depuis les ordinateurs local hello et envoi toohello à distance (**enregistrement à partir de cet ordinateur**).</span><span class="sxs-lookup"><span data-stu-id="55d52-115">Capture audio from hello local computer and send toohello remote computer (**Record from this computer**).</span></span> <span data-ttu-id="55d52-116">(audiocapturemode:i:1)</span><span class="sxs-lookup"><span data-stu-id="55d52-116">(audiocapturemode:i:1)</span></span>
* <span data-ttu-id="55d52-117">Imprimer des imprimantes toolocal (redirectprinters:i:1)</span><span class="sxs-lookup"><span data-stu-id="55d52-117">Print toolocal printers (redirectprinters:i:1)</span></span>
* <span data-ttu-id="55d52-118">Ports COM (redirectcomports:i:1)</span><span class="sxs-lookup"><span data-stu-id="55d52-118">COM ports (redirectcomports:i:1)</span></span>
* <span data-ttu-id="55d52-119">Périphérique à carte à puce (redirectsmartcards:i:1)</span><span class="sxs-lookup"><span data-stu-id="55d52-119">Smart card device (redirectsmartcards:i:1)</span></span>
* <span data-ttu-id="55d52-120">Presse-papiers (capacité toocopy et coller) (redirectclipboard:i:1)</span><span class="sxs-lookup"><span data-stu-id="55d52-120">Clipboard (ability toocopy and paste) (redirectclipboard:i:1)</span></span>
* <span data-ttu-id="55d52-121">Lissage des polices ClearType (allowfontsmoothing:i:1)</span><span class="sxs-lookup"><span data-stu-id="55d52-121">Clear type font smoothing (allow font smoothing:i:1)</span></span>
* <span data-ttu-id="55d52-122">Rediriger tous les périphériques Plug-and-Play pris en charge.</span><span class="sxs-lookup"><span data-stu-id="55d52-122">Redirect all supported Plug and Play devices.</span></span> <span data-ttu-id="55d52-123">(devicestoredirect:s:*)</span><span class="sxs-lookup"><span data-stu-id="55d52-123">(devicestoredirect:s:*)</span></span>

## <a name="what-other-redirection-is-available"></a><span data-ttu-id="55d52-124">Quelle autre redirection est disponible ?</span><span class="sxs-lookup"><span data-stu-id="55d52-124">What other redirection is available?</span></span>
<span data-ttu-id="55d52-125">Deux options de redirection sont désactivées par défaut :</span><span class="sxs-lookup"><span data-stu-id="55d52-125">Two redirection options are disabled by default:</span></span>

* <span data-ttu-id="55d52-126">La redirection du lecteur (mappage de lecteur) : lecteurs de votre ordinateur local deviennent les lecteurs mappés dans la session à distance de hello.</span><span class="sxs-lookup"><span data-stu-id="55d52-126">Drive redirection (drive mapping): Your local computer's drives become mapped drives in hello remote session.</span></span> <span data-ttu-id="55d52-127">Cela vous permet de vous enregistrer ou ouvrir des fichiers à partir de vos lecteurs locaux pendant que vous travaillez dans la session à distance de hello.</span><span class="sxs-lookup"><span data-stu-id="55d52-127">This lets you save or open files from your local drives while you work in hello remote session.</span></span>
* <span data-ttu-id="55d52-128">La redirection de USB : vous pouvez utiliser l’ordinateur local de hello USB périphériques tooyour attaché au sein de la session à distance de hello.</span><span class="sxs-lookup"><span data-stu-id="55d52-128">USB redirection: You can use hello USB devices attached tooyour local computer within hello remote session.</span></span>

## <a name="change-your-redirection-settings-in-remoteapp"></a><span data-ttu-id="55d52-129">Modification de vos paramètres de redirection dans RemoteApp</span><span class="sxs-lookup"><span data-stu-id="55d52-129">Change your redirection settings in RemoteApp</span></span>
<span data-ttu-id="55d52-130">Vous pouvez modifier les paramètres de redirection de périphérique hello pour une collection à l’aide de hello Microsoft Azure PowerShell avec le Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="55d52-130">You can change hello device redirection settings for a collection by using hello Microsoft Azure PowerShell with SDK.</span></span> <span data-ttu-id="55d52-131">Après avoir installé hello nouveau PowerShell et le Kit de développement logiciel, configurez tout d’abord toomanage votre abonnement comme décrit dans [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="55d52-131">After you install hello new PowerShell and SDK, first configure it toomanage your subscription as described in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="55d52-132">Utiliser un toohello similaire commande tooset hello personnalisé RDP propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="55d52-132">Then use a command similar toohello following tooset hello custom RDP properties:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="55d52-133">(Notez que  *\`n*  est utilisé comme séparateur entre les propriétés individuelles.)</span><span class="sxs-lookup"><span data-stu-id="55d52-133">(Note that *\`n* is used as a delimiter between individual properties.)</span></span>

<span data-ttu-id="55d52-134">tooget une liste de quelles propriétés RDP personnalisées sont configurées, exécutez hello suivant l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="55d52-134">tooget a list of what custom RDP properties are configured, run hello following cmdlet.</span></span> <span data-ttu-id="55d52-135">Notez que les propriétés personnalisées seulement sont affichées sous la forme d’un résultat et hello pas les propriétés par défaut :</span><span class="sxs-lookup"><span data-stu-id="55d52-135">Note that only custom properties are shown as output results and not hello default properties:</span></span>  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

<span data-ttu-id="55d52-136">Lorsque vous définissez des propriétés personnalisées vous devez spécifier toutes les propriétés personnalisées de chaque heure ; Sinon, paramètre de hello revient toodisabled.</span><span class="sxs-lookup"><span data-stu-id="55d52-136">When you set custom properties you must specify all custom properties each time; otherwise hello setting reverts toodisabled.</span></span>   

### <a name="common-examples"></a><span data-ttu-id="55d52-137">Exemples courants</span><span class="sxs-lookup"><span data-stu-id="55d52-137">Common examples</span></span>
<span data-ttu-id="55d52-138">Hello après la redirection du lecteur tooenable applet de commande, utilisez :</span><span class="sxs-lookup"><span data-stu-id="55d52-138">Use hello following cmdlet tooenable drive redirection:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

<span data-ttu-id="55d52-139">Utilisez cette applet de commande tooenable redirection USB et lecteur :</span><span class="sxs-lookup"><span data-stu-id="55d52-139">Use this cmdlet tooenable both USB and Drive redirection:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="55d52-140">Utilisez cette applet de commande toodisable le partage du Presse-papiers :</span><span class="sxs-lookup"><span data-stu-id="55d52-140">Use this cmdlet toodisable clipboard sharing:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> <span data-ttu-id="55d52-141">Être toocompletely vraiment déconnecter tous les utilisateurs de la collection de hello (et pas seulement les déconnecter) avant de tester les modifications hello.</span><span class="sxs-lookup"><span data-stu-id="55d52-141">Be sure toocompletely log off all users in hello collection (and not just disconnect them) before you test hello change.</span></span> <span data-ttu-id="55d52-142">tooensure complètement déconnexion des utilisateurs, accédez toohello **Sessions** onglet collection hello Bonjour portail Azure et de déconnexion de tous les utilisateurs sont déconnectés ou connectés.</span><span class="sxs-lookup"><span data-stu-id="55d52-142">tooensure users are completely logged off, go toohello **Sessions** tab in hello collection in hello Azure portal and log off any users who are disconnected or signed in.</span></span> <span data-ttu-id="55d52-143">Parfois, peut prendre plusieurs secondes hello lecteurs locaux tooshow dans l’Explorateur d’au sein de la session de hello.</span><span class="sxs-lookup"><span data-stu-id="55d52-143">Sometimes it can take several seconds for hello local drives tooshow in Explorer within hello session.</span></span>
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a><span data-ttu-id="55d52-144">Modification des paramètres de redirection USB sur votre client Windows</span><span class="sxs-lookup"><span data-stu-id="55d52-144">Change USB redirection settings on your Windows client</span></span>
<span data-ttu-id="55d52-145">Si vous souhaitez que la redirection de toouse USB sur un ordinateur qui se connecte tooRemoteApp, il existe 2 actions nécessitant toohappen.</span><span class="sxs-lookup"><span data-stu-id="55d52-145">If you want toouse USB redirection on a computer that connects tooRemoteApp, there are 2 actions that need toohappen.</span></span> <span data-ttu-id="55d52-146">1 - votre administrateur doit la redirection de USB tooenable au niveau de collection hello à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="55d52-146">1 - Your administrator needs tooenable USB redirection at hello collection level by using Azure PowerShell.</span></span> <span data-ttu-id="55d52-147">2 - sur chaque appareil sur lequel vous souhaitez la redirection de toouse USB, vous devez tooenable une stratégie de groupe qui l’autorise.</span><span class="sxs-lookup"><span data-stu-id="55d52-147">2 - On each device where you want toouse USB redirection, you need tooenable a group policy that permits it.</span></span> <span data-ttu-id="55d52-148">Cette étape doit toobe fait pour chaque utilisateur qui souhaite la redirection de toouse USB.</span><span class="sxs-lookup"><span data-stu-id="55d52-148">This step will need toobe done for each user that wants toouse USB redirection.</span></span>

> [!NOTE]
> <span data-ttu-id="55d52-149">La redirection USB avec Azure RemoteApp est prise en charge uniquement pour les ordinateurs Windows.</span><span class="sxs-lookup"><span data-stu-id="55d52-149">USB redirection with Azure RemoteApp is only supported for Windows computers.</span></span>
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a><span data-ttu-id="55d52-150">Activer la redirection de USB pour hello collection RemoteApp</span><span class="sxs-lookup"><span data-stu-id="55d52-150">Enable USB redirection for hello RemoteApp collection</span></span>
<span data-ttu-id="55d52-151">Utilisez hello après redirection de USB tooenable applet de commande au niveau de collection hello :</span><span class="sxs-lookup"><span data-stu-id="55d52-151">Use hello following cmdlet tooenable USB redirection at hello collection level:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a><span data-ttu-id="55d52-152">Activer la redirection de USB pour l’ordinateur client de hello</span><span class="sxs-lookup"><span data-stu-id="55d52-152">Enable USB redirection for hello client computer</span></span>
<span data-ttu-id="55d52-153">paramètres de redirection tooconfigure USB sur votre ordinateur :</span><span class="sxs-lookup"><span data-stu-id="55d52-153">tooconfigure USB redirection settings on your computer:</span></span>

1. <span data-ttu-id="55d52-154">Ouvrez hello éditeur de stratégie de groupe locale (GPEDIT. MSC).</span><span class="sxs-lookup"><span data-stu-id="55d52-154">Open hello Local Group Policy Editor (GPEDIT.MSC).</span></span> <span data-ttu-id="55d52-155">(Exécutez gpedit.msc à partir d'une invite de commandes.)</span><span class="sxs-lookup"><span data-stu-id="55d52-155">(Run gpedit.msc from a command prompt.)</span></span>
2. <span data-ttu-id="55d52-156">Ouvrez **Configuration ordinateur\Stratégies\Modèles d'administration\Composants Windows\Services Bureau à distance\Client Connexion Bureau à distance\Redirection des périphériques USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="55d52-156">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
3. <span data-ttu-id="55d52-157">Double-cliquez sur **Autoriser la redirection RDP d'autres périphériques USB RemoteFX pris en charge à partir de cet ordinateur**.</span><span class="sxs-lookup"><span data-stu-id="55d52-157">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
4. <span data-ttu-id="55d52-158">Sélectionnez **activé**, puis sélectionnez **administrateurs et utilisateurs Bonjour RemoteFX USB la Redirection des droits d’accès**.</span><span class="sxs-lookup"><span data-stu-id="55d52-158">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
5. <span data-ttu-id="55d52-159">Ouvrez une invite de commandes avec des privilèges d’administrateur et exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="55d52-159">Open a command prompt with administrative permissions, and run hello following command:</span></span>
   
        gpupdate /force
6. <span data-ttu-id="55d52-160">Redémarrez l’ordinateur de hello.</span><span class="sxs-lookup"><span data-stu-id="55d52-160">Restart hello computer.</span></span>

<span data-ttu-id="55d52-161">Vous pouvez également utiliser toocreate d’outil de gestion de stratégie de groupe hello et appliquer la stratégie de redirection hello USB pour tous les ordinateurs de votre domaine :</span><span class="sxs-lookup"><span data-stu-id="55d52-161">You can also use hello Group Policy Management tool toocreate and apply hello USB redirection policy for all computers in your domain:</span></span>

1. <span data-ttu-id="55d52-162">Connectez-vous à un contrôleur de domaine hello en tant qu’administrateur de domaine hello.</span><span class="sxs-lookup"><span data-stu-id="55d52-162">Log into hello domain controller as hello domain administrator.</span></span>
2. <span data-ttu-id="55d52-163">Ouvrez hello Group Policy Management Console.</span><span class="sxs-lookup"><span data-stu-id="55d52-163">Open hello Group Policy Management Console.</span></span> <span data-ttu-id="55d52-164">(Cliquez sur **Démarrer > Outils d'administration > Gestion des stratégies de groupe**.)</span><span class="sxs-lookup"><span data-stu-id="55d52-164">(Click **Start > Administrative Tools > Group Policy Management**.)</span></span>
3. <span data-ttu-id="55d52-165">Accédez toohello domaine ou unité d’organisation pour laquelle vous souhaitez que la stratégie de hello de toocreate.</span><span class="sxs-lookup"><span data-stu-id="55d52-165">Navigate toohello domain or organizational unit for which you want toocreate hello policy.</span></span>
4. <span data-ttu-id="55d52-166">Cliquez avec le bouton droit sur **Stratégie de domaine par défaut**, puis cliquez sur **Modifier**.</span><span class="sxs-lookup"><span data-stu-id="55d52-166">Right-click **Default Domain Policy**, and then click **Edit**.</span></span>
5. <span data-ttu-id="55d52-167">Ouvrez **Configuration ordinateur\Stratégies\Modèles d'administration\Composants Windows\Services Bureau à distance\Client Connexion Bureau à distance\Redirection des périphériques USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="55d52-167">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
6. <span data-ttu-id="55d52-168">Double-cliquez sur **Autoriser la redirection RDP d'autres périphériques USB RemoteFX pris en charge à partir de cet ordinateur**.</span><span class="sxs-lookup"><span data-stu-id="55d52-168">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
7. <span data-ttu-id="55d52-169">Sélectionnez **activé**, puis sélectionnez **administrateurs et utilisateurs Bonjour RemoteFX USB la Redirection des droits d’accès**.</span><span class="sxs-lookup"><span data-stu-id="55d52-169">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
8. <span data-ttu-id="55d52-170">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="55d52-170">Click **OK**.</span></span>  

