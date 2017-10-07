---
title: "aaaInstall mise à jour 0,5 sur StorSimple Virtual Array | Documents Microsoft"
description: "Décrit comment toouse hello StorSimple Virtual Array web UI tooapply mises à jour à l’aide de hello méthode Azure de portail et le correctif logiciel"
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2017
ms.author: alkohli
ms.openlocfilehash: c38daa85daa0086e67cf0206d76cb19d9c8b21b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-05-on-your-storsimple-virtual-array"></a><span data-ttu-id="f650b-103">Installation d’Update 0.5 sur StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="f650b-103">Install Update 0.5 on your StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="f650b-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f650b-104">Overview</span></span>

<span data-ttu-id="f650b-105">Cet article décrit hello étapes tooinstall obligatoire la mise à jour 0,5 sur votre tableau virtuel StorSimple via l’interface utilisateur de web locale hello et hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f650b-105">This article describes hello steps required tooinstall Update 0.5 on your StorSimple Virtual Array via hello local web UI and via hello Azure portal.</span></span> <span data-ttu-id="f650b-106">Vous devez tookeep des mises à jour ou correctifs logiciels tooapply votre tableau virtuel StorSimple mis à jour.</span><span class="sxs-lookup"><span data-stu-id="f650b-106">You need tooapply software updates or hotfixes tookeep your StorSimple Virtual Array up-to-date.</span></span>

<span data-ttu-id="f650b-107">Avant d’appliquer une mise à jour, nous recommandons de prendre de volumes de hello ou partages en mode hors connexion sur hello hébergent tout d’abord et puis hello appareil.</span><span class="sxs-lookup"><span data-stu-id="f650b-107">Before you apply an update, we recommend that you take hello volumes or shares offline on hello host first and then hello device.</span></span> <span data-ttu-id="f650b-108">Vous réduisez ainsi toute possibilité d’altération des données.</span><span class="sxs-lookup"><span data-stu-id="f650b-108">This minimizes any possibility of data corruption.</span></span> <span data-ttu-id="f650b-109">Une fois hello volumes ou partages sont hors connexion, vous devez également prendre un manuel de sauvegarde de l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="f650b-109">After hello volumes or shares are offline, you should also take a manual backup of hello device.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="f650b-110">Mise à jour 0,5 correspond trop**10.0.10290.0** version du logiciel sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="f650b-110">Update 0.5 corresponds too**10.0.10290.0** software version on your device.</span></span> <span data-ttu-id="f650b-111">Pour plus d’informations sur les nouveautés de cette mise à jour, accédez trop[notes de publication pour la mise à jour 0,5](storsimple-virtual-array-update-05-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="f650b-111">For information on what is new in this update, go too[Release notes for Update 0.5](storsimple-virtual-array-update-05-release-notes.md).</span></span>
>
> - <span data-ttu-id="f650b-112">Si vous exécutez la mise à jour 0,2 ou une version ultérieure, nous recommandons que vous installez des mises à jour de la hello via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f650b-112">If you are running Update 0.2 or later, we recommend that you install hello updates via hello Azure portal.</span></span> <span data-ttu-id="f650b-113">Si vous exécutez la mise à jour 0.1 ou les versions des logiciels GA, vous devez utiliser la méthode de correctif logiciel hello via tooinstall de l’interface utilisateur web locale hello mise à jour de 0,5.</span><span class="sxs-lookup"><span data-stu-id="f650b-113">If you are running Update 0.1 or GA software versions, you must use hello hotfix method via hello local web UI tooinstall Update 0.5.</span></span>
>
> - <span data-ttu-id="f650b-114">N’oubliez pas que l’installation d’une mise à jour ou d’un correctif logiciel nécessite le redémarrage de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="f650b-114">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="f650b-115">Étant donné que hello StorSimple Virtual Array est un périphérique de nœud unique, l’interruption des e/s en cours d’exécution et indisponibilité de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="f650b-115">Given that hello StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span>

## <a name="use-hello-azure-portal"></a><span data-ttu-id="f650b-116">Utilisez hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f650b-116">Use hello Azure portal</span></span>

<span data-ttu-id="f650b-117">Si l’exécution de Update 0,2 et versions ultérieures, nous vous recommandons d’installer via hello portail Azure, les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="f650b-117">If running Update 0.2 and later, we recommend that you install updates through hello Azure portal.</span></span> <span data-ttu-id="f650b-118">procédure de portail Hello requiert hello utilisateur tooscan, télécharger, puis installer les mises à jour hello.</span><span class="sxs-lookup"><span data-stu-id="f650b-118">hello portal procedure requires hello user tooscan, download, and then install hello updates.</span></span> <span data-ttu-id="f650b-119">Cette procédure prend environ 7 minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f650b-119">This procedure takes around 7 minutes toocomplete.</span></span> <span data-ttu-id="f650b-120">Hello suivants étapes de mise à jour de tooinstall hello ou un correctif logiciel.</span><span class="sxs-lookup"><span data-stu-id="f650b-120">Perform hello following steps tooinstall hello update or hotfix.</span></span>

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

<span data-ttu-id="f650b-121">Après avoir hello l’installation est terminée, accédez tooyour service du Gestionnaire de périphériques StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f650b-121">After hello installation is complete, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="f650b-122">Sélectionnez **périphériques** puis sélectionnez et cliquez sur périphérique hello vous venez de mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="f650b-122">Select **Devices** and then select and click hello device you just updated.</span></span> <span data-ttu-id="f650b-123">Accédez trop**Paramètres > Gérer > mises à jour de l’appareil**.</span><span class="sxs-lookup"><span data-stu-id="f650b-123">Go too**Settings > Manage > Device Updates**.</span></span> <span data-ttu-id="f650b-124">version du logiciel Hello affiché doit être **10.0.10290.0**.</span><span class="sxs-lookup"><span data-stu-id="f650b-124">hello displayed software version should be **10.0.10290.0**.</span></span>

## <a name="use-hello-local-web-ui"></a><span data-ttu-id="f650b-125">Utiliser l’interface utilisateur de web locale hello</span><span class="sxs-lookup"><span data-stu-id="f650b-125">Use hello local web UI</span></span>

<span data-ttu-id="f650b-126">Il existe deux étapes lors de l’utilisation de l’interface utilisateur de web local hello :</span><span class="sxs-lookup"><span data-stu-id="f650b-126">There are two steps when using hello local web UI:</span></span>

* <span data-ttu-id="f650b-127">Télécharger la mise à jour hello ou un correctif logiciel de hello</span><span class="sxs-lookup"><span data-stu-id="f650b-127">Download hello update or hello hotfix</span></span>
* <span data-ttu-id="f650b-128">Installer la mise à jour hello ou un correctif logiciel de hello</span><span class="sxs-lookup"><span data-stu-id="f650b-128">Install hello update or hello hotfix</span></span>

### <a name="download-hello-update-or-hello-hotfix"></a><span data-ttu-id="f650b-129">Télécharger la mise à jour hello ou un correctif logiciel de hello</span><span class="sxs-lookup"><span data-stu-id="f650b-129">Download hello update or hello hotfix</span></span>

<span data-ttu-id="f650b-130">Effectuer hello suivant étapes toodownload hello mise à jour à partir de hello catalogue Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="f650b-130">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

#### <a name="toodownload-hello-update-or-hello-hotfix"></a><span data-ttu-id="f650b-131">correctif de mise à jour ou hello de hello toodownload</span><span class="sxs-lookup"><span data-stu-id="f650b-131">toodownload hello update or hello hotfix</span></span>

1. <span data-ttu-id="f650b-132">Démarrez Internet Explorer et accédez trop[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f650b-132">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>

2. <span data-ttu-id="f650b-133">S’il s’agit de votre première utilisation hello catalogue Microsoft Update sur cet ordinateur, cliquez sur **installer** lorsque tooinstall demandée hello module complémentaire du catalogue Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="f650b-133">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

3. <span data-ttu-id="f650b-134">Dans la zone de recherche hello Hello catalogue Microsoft Update, entrez le nombre de Base de connaissances (KB) hello de hello correctif souhaité toodownload.</span><span class="sxs-lookup"><span data-stu-id="f650b-134">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload.</span></span> <span data-ttu-id="f650b-135">Entrez **4021576** pour Update 0.5, puis cliquez sur **Rechercher**.</span><span class="sxs-lookup"><span data-stu-id="f650b-135">Enter **4021576** for Update 0.5, and then click **Search**.</span></span>
   
    <span data-ttu-id="f650b-136">Hello correctif liste s’affiche, par exemple, **mise à jour de tableau virtuel StorSimple 0,5**.</span><span class="sxs-lookup"><span data-stu-id="f650b-136">hello hotfix listing appears, for example, **StorSimple Virtual Array Update 0.5**.</span></span>
   
    ![Rechercher dans le catalogue](./media/storsimple-virtual-array-install-update-05/download1.png)

4. <span data-ttu-id="f650b-138">Cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="f650b-138">Click **Download**.</span></span> 

5. <span data-ttu-id="f650b-139">Vous devez voir deux toodownload de fichiers, un *.msu* et un *.cab* fichier.</span><span class="sxs-lookup"><span data-stu-id="f650b-139">You should see two files toodownload, a *.msu* and a *.cab* file.</span></span> <span data-ttu-id="f650b-140">Téléchargez tous ces tooa dossier des fichiers.</span><span class="sxs-lookup"><span data-stu-id="f650b-140">Download each of those files tooa folder.</span></span> <span data-ttu-id="f650b-141">dossier de Hello peut également être tooa copié partage réseau accessible à partir de l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="f650b-141">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

6. <span data-ttu-id="f650b-142">Ouvrez le dossier hello dans lequel se trouvent les fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="f650b-142">Open hello folder where hello files are located.</span></span>
    <span data-ttu-id="f650b-143">![Fichiers dans le package de hello](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span><span class="sxs-lookup"><span data-stu-id="f650b-143">![Files in hello package](./media/storsimple-virtual-array-install-update-05/update05folder.png)</span></span>

    <span data-ttu-id="f650b-144">Vous voyez :</span><span class="sxs-lookup"><span data-stu-id="f650b-144">You see:</span></span>
    -  <span data-ttu-id="f650b-145">Un fichier de package autonome Microsoft `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="f650b-145">A Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="f650b-146">Ce fichier est un logiciel de périphérique de hello tooupdate utilisé.</span><span class="sxs-lookup"><span data-stu-id="f650b-146">This file is used tooupdate hello device software.</span></span>
    - <span data-ttu-id="f650b-147">Un fichier de package d’agent de surveillance de Genève `GenevaMonitoringAgentPackageInstaller`.</span><span class="sxs-lookup"><span data-stu-id="f650b-147">A Geneva Monitoring Agent Package file `GenevaMonitoringAgentPackageInstaller`.</span></span> <span data-ttu-id="f650b-148">Ce fichier est utilisé tooupdate hello analyse et Diagnostics (MDS) agent du service.</span><span class="sxs-lookup"><span data-stu-id="f650b-148">This file is used tooupdate hello Monitoring and Diagnostics service (MDS) agent.</span></span> <span data-ttu-id="f650b-149">Double-cliquez sur le fichier cab de hello.</span><span class="sxs-lookup"><span data-stu-id="f650b-149">Double-click hello cab file.</span></span> <span data-ttu-id="f650b-150">Un .msi s’affiche.</span><span class="sxs-lookup"><span data-stu-id="f650b-150">A .msi is displayed.</span></span> <span data-ttu-id="f650b-151">Fichier de sélection hello, avec le bouton droit, puis **extraire** fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="f650b-151">Select hello file, right-click, and then **Extract** hello file.</span></span> <span data-ttu-id="f650b-152">Vous allez utiliser hello _.msi_ l’agent de fichiers tooupdate hello.</span><span class="sxs-lookup"><span data-stu-id="f650b-152">You will use hello _.msi_ file tooupdate hello agent.</span></span>

        ![Extraire le fichier de mise à jour de l’agent de MDS](./media/storsimple-virtual-array-install-update-05/extract-geneva-monitoring-agent-installer.png)
        
    

### <a name="install-hello-update-or-hello-hotfix"></a><span data-ttu-id="f650b-154">Installer la mise à jour hello ou un correctif logiciel de hello</span><span class="sxs-lookup"><span data-stu-id="f650b-154">Install hello update or hello hotfix</span></span>

<span data-ttu-id="f650b-155">Installation de mise à jour ou le correctif logiciel toohello préalable, assurez-vous que vous avez mise à jour hello ou hello correctif téléchargé localement sur votre ordinateur hôte ou accessible via un partage réseau.</span><span class="sxs-lookup"><span data-stu-id="f650b-155">Prior toohello update or hotfix installation, make sure that you have hello update or hello hotfix downloaded either locally on your host or accessible via a network share.</span></span>

<span data-ttu-id="f650b-156">Utiliser les mises à jour tooinstall cette méthode sur un périphérique exécutant GA ou mettre à jour les versions des logiciels 0,1.</span><span class="sxs-lookup"><span data-stu-id="f650b-156">Use this method tooinstall updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="f650b-157">Cette procédure est inférieure à 2 minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="f650b-157">This procedure takes less than 2 minutes toocomplete.</span></span> <span data-ttu-id="f650b-158">Hello suivants étapes de mise à jour de tooinstall hello ou un correctif logiciel.</span><span class="sxs-lookup"><span data-stu-id="f650b-158">Perform hello following steps tooinstall hello update or hotfix.</span></span>

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a><span data-ttu-id="f650b-159">correctif de mise à jour ou hello de hello tooinstall</span><span class="sxs-lookup"><span data-stu-id="f650b-159">tooinstall hello update or hello hotfix</span></span>

1. <span data-ttu-id="f650b-160">Dans l’interface utilisateur de web locale hello, accédez trop**Maintenance** > **mise à jour logicielle**.</span><span class="sxs-lookup"><span data-stu-id="f650b-160">In hello local web UI, go too**Maintenance** > **Software Update**.</span></span>
   
    ![mettre à jour l'appareil](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. <span data-ttu-id="f650b-162">Dans **chemin d’accès du fichier de mise à jour**, entrez le nom du fichier de mise à jour hello hello ou hello correctif logiciel.</span><span class="sxs-lookup"><span data-stu-id="f650b-162">In **Update file path**, enter hello file name for hello update or hello hotfix.</span></span> <span data-ttu-id="f650b-163">Vous pouvez également parcourir le fichier d’installation de mise à jour ou le correctif logiciel toohello si placé sur un partage réseau.</span><span class="sxs-lookup"><span data-stu-id="f650b-163">You can also browse toohello update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="f650b-164">Cliquez sur **Apply**.</span><span class="sxs-lookup"><span data-stu-id="f650b-164">Click **Apply**.</span></span>
   
    ![mettre à jour l'appareil](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. <span data-ttu-id="f650b-166">Un avertissement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="f650b-166">A warning is displayed.</span></span> <span data-ttu-id="f650b-167">Étant donné ce est un périphérique à nœud unique, après la mise à jour hello, redémarrage du périphérique hello et il est temps d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="f650b-167">Given this is a single node device, after hello update is applied, hello device restarts and there is downtime.</span></span> <span data-ttu-id="f650b-168">Cliquez sur une icône de coche hello.</span><span class="sxs-lookup"><span data-stu-id="f650b-168">Click hello check icon.</span></span>
   
   ![mettre à jour l'appareil](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. <span data-ttu-id="f650b-170">mise à jour Hello démarre.</span><span class="sxs-lookup"><span data-stu-id="f650b-170">hello update starts.</span></span> <span data-ttu-id="f650b-171">Une fois que l’appareil de hello est correctement mise à jour, il redémarre.</span><span class="sxs-lookup"><span data-stu-id="f650b-171">After hello device is successfully updated, it restarts.</span></span> <span data-ttu-id="f650b-172">Hello d’interface utilisateur locale n’est pas accessible dans cette durée.</span><span class="sxs-lookup"><span data-stu-id="f650b-172">hello local UI is not accessible in this duration.</span></span>
   
    ![mettre à jour l'appareil](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. <span data-ttu-id="f650b-174">Après le redémarrage de hello est terminée, vous accédez toohello **connectez-vous** page.</span><span class="sxs-lookup"><span data-stu-id="f650b-174">After hello restart is complete, you are taken toohello **Sign in** page.</span></span> <span data-ttu-id="f650b-175">tooverify logiciel du périphérique hello a mis à jour, dans le site web local hello l’interface utilisateur, consultez trop**Maintenance** > **mise à jour logicielle**.</span><span class="sxs-lookup"><span data-stu-id="f650b-175">tooverify that hello device software has updated, in hello local web UI, go too**Maintenance** > **Software Update**.</span></span> <span data-ttu-id="f650b-176">version du logiciel Hello affiché doit être **10.0.0.0.0.10290.0** pour la mise à jour 0,5.</span><span class="sxs-lookup"><span data-stu-id="f650b-176">hello displayed software version should be **10.0.0.0.0.10290.0** for Update 0.5.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f650b-177">Nous signaler les versions des logiciels hello d’une manière légèrement différente dans l’interface utilisateur de web locale hello et hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f650b-177">We report hello software versions in a slightly different way in hello local web UI and hello Azure portal.</span></span> <span data-ttu-id="f650b-178">Hello, par exemple, les rapports de l’interface utilisateur web locale **10.0.0.0.0.10290** et hello rapports portails Azure **10.0.10290.0** pour hello même version.</span><span class="sxs-lookup"><span data-stu-id="f650b-178">For example, hello local web UI reports **10.0.0.0.0.10290** and hello Azure portal reports **10.0.10290.0** for hello same version.</span></span>
   
    ![mettre à jour l'appareil](./media/storsimple-virtual-array-install-update-05/update6m.png)

6. <span data-ttu-id="f650b-180">étape suivante de Hello est l’agent de tooupdate hello MDS.</span><span class="sxs-lookup"><span data-stu-id="f650b-180">hello next step is tooupdate hello MDS agent.</span></span> <span data-ttu-id="f650b-181">Bonjour **mise à jour logicielle** page, aller toohello **chemin d’accès du fichier de mise à jour** et parcourir toohello `GenevaMonitoringAgentPackageInstaller.msi` fichier.</span><span class="sxs-lookup"><span data-stu-id="f650b-181">In hello **Software Update** page, go toohello **Update file path** and browse toohello `GenevaMonitoringAgentPackageInstaller.msi` file.</span></span> <span data-ttu-id="f650b-182">Répétez les étapes 2 à 4.</span><span class="sxs-lookup"><span data-stu-id="f650b-182">Repeat steps 2-4.</span></span> <span data-ttu-id="f650b-183">Après le redémarrage de l’unité de stockage virtuelle hello, connectez-vous à l’interface utilisateur de web locale hello.</span><span class="sxs-lookup"><span data-stu-id="f650b-183">After hello virtual array restarts, sign into hello local web UI.</span></span>

<span data-ttu-id="f650b-184">mise à jour Hello est maintenant terminée.</span><span class="sxs-lookup"><span data-stu-id="f650b-184">hello update is now complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f650b-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f650b-185">Next steps</span></span>

<span data-ttu-id="f650b-186">En savoir plus sur la [gestion de votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="f650b-186">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

