---
title: "mises à jour d’aaaInstall sur une unité de stockage de Microsoft Azure StorSimple virtuelle | Documents Microsoft"
description: "Décrit comment tooapply de l’interface utilisateur web toouse hello StorSimple Virtual Array met à jour à l’aide de la méthode de portail et le correctif logiciel hello"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 9997a97b-9382-43ed-b56e-61369335c987
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7424abc7e46d4f08b4eae1194642b263f32c4318
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array---azure-portal"></a><span data-ttu-id="8cc5e-103">Installation de mises à jour sur votre instance StorSimple Virtual Array - Portail Azure</span><span class="sxs-lookup"><span data-stu-id="8cc5e-103">Install Updates on your StorSimple Virtual Array - Azure portal</span></span>

## <a name="overview"></a><span data-ttu-id="8cc5e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="8cc5e-104">Overview</span></span>

<span data-ttu-id="8cc5e-105">Cet article décrit les mises à jour de hello étapes tooinstall requis sur votre tableau virtuel StorSimple via l’interface utilisateur de web locale hello et hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-105">This article describes hello steps required tooinstall updates on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="8cc5e-106">Vous devez tookeep des mises à jour ou correctifs logiciels tooapply votre tableau virtuel StorSimple mis à jour.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="8cc5e-107">N’oubliez pas que l’installation d’une mise à jour ou d’un correctif logiciel nécessite le redémarrage de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="8cc5e-108">Étant donné que hello StorSimple Virtual Array est un périphérique de nœud unique, l’interruption des e/s en cours d’exécution et indisponibilité de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-108">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="8cc5e-109">Avant d’appliquer une mise à jour, nous recommandons de prendre de volumes de hello ou partages en mode hors connexion sur hello hébergent tout d’abord et puis hello appareil.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-109">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="8cc5e-110">Vous réduisez ainsi toute possibilité d’altération des données.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8cc5e-111">Si vous exécutez la mise à jour 0.1 ou les versions des logiciels GA, vous devez utiliser la méthode de correctif logiciel de hello via la mise à jour l’interface utilisateur tooinstall 0,3 pour hello web local.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-111">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall update 0.3.</span></span> <span data-ttu-id="8cc5e-112">Si vous exécutez la mise à jour 0,2, nous vous recommandons d’installer les mises à jour hello via hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-112">If you are running Update 0.2, we recommend that you install hello updates via hello Azure classic portal.</span></span>
 

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="8cc5e-113">Utiliser l’interface utilisateur de web locale hello</span><span class="sxs-lookup"><span data-stu-id="8cc5e-113">Use hello local web UI</span></span>

<span data-ttu-id="8cc5e-114">Il existe deux étapes lors de l’utilisation de l’interface utilisateur de web local hello :</span><span class="sxs-lookup"><span data-stu-id="8cc5e-114">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="8cc5e-115">Télécharger la mise à jour hello ou un correctif logiciel de hello</span><span class="sxs-lookup"><span data-stu-id="8cc5e-115">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="8cc5e-116">Installer la mise à jour hello ou un correctif logiciel de hello</span><span class="sxs-lookup"><span data-stu-id="8cc5e-116">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="8cc5e-117">Télécharger la mise à jour hello ou un correctif logiciel de hello</span><span class="sxs-lookup"><span data-stu-id="8cc5e-117">Download hello update or hello hotfix</span></span>

<span data-ttu-id="8cc5e-118">Effectuer hello suivant étapes toodownload hello mise à jour à partir de hello catalogue Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-118">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="8cc5e-119">correctif de mise à jour ou hello de hello toodownload</span><span class="sxs-lookup"><span data-stu-id="8cc5e-119">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="8cc5e-120">Démarrez Internet Explorer et accédez trop[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="8cc5e-120">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="8cc5e-121">S’il s’agit de votre première utilisation hello catalogue Microsoft Update sur cet ordinateur, cliquez sur **installer** lorsque tooinstall demandée hello module complémentaire du catalogue Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-121">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="8cc5e-122">Dans la zone de recherche hello Hello catalogue Microsoft Update, entrez le nombre de Base de connaissances (KB) hello de hello correctif souhaité toodownload.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-122">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="8cc5e-123">Entrez **3182061** pour Update 0.3, puis cliquez sur **Rechercher**.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="8cc5e-124">Hello correctif liste s’affiche, par exemple, **mise à jour de tableau virtuel StorSimple 0,3**.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-124">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![Rechercher dans le catalogue](./media/storsimple-virtual-array-install-update/download1.png)

4. <span data-ttu-id="8cc5e-126">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-126">Click **Add**.</span></span> <span data-ttu-id="8cc5e-127">mise à jour Hello est ajouté toohello du panier d’achat.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-127">hello update is added toohello basket.</span></span>

5. <span data-ttu-id="8cc5e-128">Cliquez sur **Afficher le panier**.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-128">Click **View Basket**.</span></span>

6. <span data-ttu-id="8cc5e-129">Cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-129">Click **Download**.</span></span> <span data-ttu-id="8cc5e-130">Spécifiez ou **Parcourir** tooa local emplacement souhaité hello télécharge tooappear.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-130">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="8cc5e-131">Hello mises à jour sont téléchargées toohello l’emplacement spécifié et placé dans un sous-dossier portant le même nom qu’une mise à jour hello de hello.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-131">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="8cc5e-132">dossier de Hello peut également être tooa copié partage réseau accessible à partir de l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-132">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

7. <span data-ttu-id="8cc5e-133">Ouvrez hello copié le dossier, vous devriez voir un fichier de Package autonome Microsoft `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-133">Open hello copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="8cc5e-134">Ce fichier est mise à jour de tooinstall utilisé hello ou un correctif logiciel.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-134">This file is used tooinstall hello update or hotfix.</span></span>

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="8cc5e-135">Installer la mise à jour hello ou un correctif logiciel de hello</span><span class="sxs-lookup"><span data-stu-id="8cc5e-135">Install hello update or hello hotfix</span></span>

<span data-ttu-id="8cc5e-136">Installation de mise à jour ou le correctif logiciel toohello préalable, assurez-vous que vous avez mise à jour hello ou hello correctif téléchargé localement sur votre ordinateur hôte ou accessible via un partage réseau.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-136">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="8cc5e-137">Utiliser les mises à jour tooinstall cette méthode sur un périphérique exécutant GA ou mettre à jour les versions des logiciels 0,1.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-137">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="8cc5e-138">Cette procédure est inférieure à 2 minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-138">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="8cc5e-139">Hello suivants étapes de mise à jour de tooinstall hello ou un correctif logiciel.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-139">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="8cc5e-140">correctif de mise à jour ou hello de hello tooinstall</span><span class="sxs-lookup"><span data-stu-id="8cc5e-140">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="8cc5e-141">Dans l’interface utilisateur de web locale hello, accédez trop**Maintenance** > **mise à jour logicielle**.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-141">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![mettre à jour l'appareil](./media/storsimple-virtual-array-install-update/update1m.png)

2. <span data-ttu-id="8cc5e-143">Dans **chemin d’accès du fichier de mise à jour**, entrez le nom du fichier de mise à jour hello hello ou hello correctif logiciel.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-143">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="8cc5e-144">Vous pouvez également parcourir le fichier d’installation de mise à jour ou le correctif logiciel toohello si placé sur un partage réseau.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-144">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="8cc5e-145">Cliquez sur **Apply**.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-145">Click **Apply**.</span></span>
   
    ![mettre à jour l'appareil](./media/storsimple-virtual-array-install-update/update2m.png)

3. <span data-ttu-id="8cc5e-147">Un avertissement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-147">A warning is displayed.</span></span> <span data-ttu-id="8cc5e-148">Étant donné ce est un périphérique à nœud unique, après la mise à jour hello, redémarrage du périphérique hello et il est temps d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-148">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="8cc5e-149">Cliquez sur une icône de coche hello.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-149">Click hello check icon.</span></span>
   
   ![mettre à jour l'appareil](./media/storsimple-virtual-array-install-update/update3m.png)

4. <span data-ttu-id="8cc5e-151">mise à jour Hello démarre.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-151">hello update starts.</span></span> <span data-ttu-id="8cc5e-152">Une fois que l’appareil de hello est correctement mise à jour, il redémarre.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-152">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="8cc5e-153">Hello d’interface utilisateur locale n’est pas accessible dans cette durée.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-153">hello local UI is not accessible in this duration.</span></span>
   
    ![mettre à jour l'appareil](./media/storsimple-virtual-array-install-update/update5m.png)

5. <span data-ttu-id="8cc5e-155">Après le redémarrage de hello est terminée, vous accédez toohello **connectez-vous** page.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-155">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="8cc5e-156">tooverify logiciel du périphérique hello a mis à jour, dans le site web local hello l’interface utilisateur, consultez trop**Maintenance** > **mise à jour logicielle**.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-156">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="8cc5e-157">version du logiciel Hello affiché doit être **10.0.0.0.0.10288.0** pour la mise à jour 0.3.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-157">hello displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8cc5e-158">Nous signaler les versions des logiciels hello d’une manière légèrement différente dans l’interface utilisateur de web locale hello et hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-158">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="8cc5e-159">Hello, par exemple, les rapports de l’interface utilisateur web locale **10.0.0.0.0.10288** et hello rapports portails Azure **10.0.10288.0** pour hello même version.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-159">For example, hello local web UI reports **10.0.0.0.0.10288** and hello Azure portal reports **10.0.10288.0** for hello same version.</span></span>
   
    ![mettre à jour l'appareil](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-hello-azure-portal"></a><span data-ttu-id="8cc5e-161">Utilisez hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="8cc5e-161">Use hello Azure portal</span></span>

<span data-ttu-id="8cc5e-162">Si la mise à jour 0,2 en cours d’exécution, nous vous recommandons d’installer via hello portail Azure, les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-162">If running Update 0.2, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="8cc5e-163">procédure de portail Hello requiert hello utilisateur tooscan, télécharger, puis installer les mises à jour hello.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-163">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="8cc5e-164">Cette procédure prend environ 7 minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-164">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="8cc5e-165">Hello suivants étapes de mise à jour de tooinstall hello ou un correctif logiciel.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-165">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal.md)]

<span data-ttu-id="8cc5e-166">Après avoir hello l’installation est tooyour accédez complète (comme indiqué par l’état du travail à 100 %), service de gestionnaire de périphériques StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-166">After hello installation is complete (as indicated by job status at 100 %), go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="8cc5e-167">Sélectionnez **périphériques** puis sélectionnez et cliquez sur périphérique hello tooupdate à partir de la liste de hello des périphériques connectés toothis service.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-167">Select **Devices** and then select and click hello device you want tooupdate from hello list of devices connected toothis service.</span></span> <span data-ttu-id="8cc5e-168">Bonjour **paramètres** panneau, accédez trop**gérer** section et sélectionnez **mises à jour de l’appareil**.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-168">In hello **Settings** blade, go too**Manage** section and select **Device updates**.</span></span> <span data-ttu-id="8cc5e-169">version du logiciel Hello affiché doit être **10.0.10288.0**.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-169">hello displayed software version should be **10.0.10288.0**.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8cc5e-170">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8cc5e-170">Next steps</span></span>

<span data-ttu-id="8cc5e-171">En savoir plus sur la [gestion de votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="8cc5e-171">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

