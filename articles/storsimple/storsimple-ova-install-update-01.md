---
title: "Installation de mises à jour sur une instance StorSimple Virtual Array | Microsoft Docs"
description: "Décrit comment utiliser l’interface utilisateur web de StorSimple Virtual Array pour installer des mises à jour à l’aide du portail et de la méthode des correctifs logiciels"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7f1b1e7d-04d0-4ca2-9dbb-77077ff19bb9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/07/2016
ms.author: alkohli
ms.openlocfilehash: bccb0d49c1959a690d513961c32d946763385a87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a><span data-ttu-id="43a7c-103">Installation de mises à jour sur votre instance StorSimple Virtual Array</span><span class="sxs-lookup"><span data-stu-id="43a7c-103">Install Updates on your StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="43a7c-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="43a7c-104">Overview</span></span>
<span data-ttu-id="43a7c-105">Cet article décrit les étapes requises pour installer des mises à jour sur votre instance StorSimple Virtual Array à l’aide de l’interface utilisateur web locale et du Portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="43a7c-105">This article describes the steps required to install updates on your StorSimple Virtual Array via the local web UI and via the Azure classic portal.</span></span> <span data-ttu-id="43a7c-106">Pour maintenir votre instance StorSimple Virtual Array à jour, vous devez appliquer des mises à jour ou des correctifs logiciels.</span><span class="sxs-lookup"><span data-stu-id="43a7c-106">You need to apply software updates or hotfixes to keep your StorSimple Virtual Array up-to-date.</span></span> 

<span data-ttu-id="43a7c-107">N’oubliez pas que l’installation d’une mise à jour ou d’un correctif logiciel nécessite le redémarrage de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="43a7c-107">Keep in mind that installing an update or hotfix restarts your device.</span></span> <span data-ttu-id="43a7c-108">Étant donné que StorSimple Virtual Array est un appareil à nœud unique, les E/S en cours seront interrompues et votre appareil subira des temps d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="43a7c-108">Given that the StorSimple Virtual Array is a single node device, any I/O in progress is disrupted and your device experiences downtime.</span></span> 

<span data-ttu-id="43a7c-109">Avant d’appliquer une mise à jour, nous vous recommandons de mettre les volumes ou les partages hors connexion sur l’ordinateur hôte puis sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="43a7c-109">Before you apply an update, we recommend that you take the volumes or shares offline on the host first and then the device.</span></span> <span data-ttu-id="43a7c-110">Vous réduisez ainsi toute possibilité d’altération des données.</span><span class="sxs-lookup"><span data-stu-id="43a7c-110">This minimizes any possibility of data corruption.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43a7c-111">Si vous utilisez Update 0.1 ou les versions logicielles GA, vous devez appliquer la méthode de correctif logiciel par le biais de l’interface utilisateur web locale pour installer Update 0.3.</span><span class="sxs-lookup"><span data-stu-id="43a7c-111">If you are running Update 0.1 or GA software versions, you must use the hotfix method via the local web UI to install update 0.3.</span></span> <span data-ttu-id="43a7c-112">Si vous utilisez Update 0.2, nous vous recommandons d’installer les mises à jour au moyen du Portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="43a7c-112">If you are running Update 0.2, we recommend that you install the updates via the Azure classic portal.</span></span>
> 
> 

## <a name="use-the-local-web-ui"></a><span data-ttu-id="43a7c-113">Utilisation de l’interface utilisateur web locale</span><span class="sxs-lookup"><span data-stu-id="43a7c-113">Use the local web UI</span></span>
<span data-ttu-id="43a7c-114">La procédure de mise à jour à l’aide de l’interface utilisateur web locale se déroule en deux étapes :</span><span class="sxs-lookup"><span data-stu-id="43a7c-114">There are two steps when using the local web UI:</span></span>

* <span data-ttu-id="43a7c-115">Téléchargement de la mise à jour ou du correctif</span><span class="sxs-lookup"><span data-stu-id="43a7c-115">Download the update or the hotfix</span></span>
* <span data-ttu-id="43a7c-116">Installation de la mise à jour ou du correctif</span><span class="sxs-lookup"><span data-stu-id="43a7c-116">Install the update or the hotfix</span></span>

### <a name="download-the-update-or-the-hotfix"></a><span data-ttu-id="43a7c-117">Téléchargement de la mise à jour ou du correctif</span><span class="sxs-lookup"><span data-stu-id="43a7c-117">Download the update or the hotfix</span></span>
<span data-ttu-id="43a7c-118">Procédez comme suit pour télécharger la mise à jour logicielle à partir du Catalogue Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="43a7c-118">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

#### <a name="to-download-the-update-or-the-hotfix"></a><span data-ttu-id="43a7c-119">Pour téléchargement la mise à jour ou le correctif</span><span class="sxs-lookup"><span data-stu-id="43a7c-119">To download the update or the hotfix</span></span>
1. <span data-ttu-id="43a7c-120">Démarrez Internet Explorer et accédez à [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="43a7c-120">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="43a7c-121">Si vous utilisez le catalogue Microsoft Update pour la première fois sur cet ordinateur, cliquez sur **Installer** lorsque vous êtes invité à installer le module complémentaire Catalogue Microsoft Update.</span><span class="sxs-lookup"><span data-stu-id="43a7c-121">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
3. <span data-ttu-id="43a7c-122">Dans la zone de recherche du Catalogue Microsoft Update, entrez le numéro KB (Base de connaissances) du correctif que vous souhaitez télécharger.</span><span class="sxs-lookup"><span data-stu-id="43a7c-122">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download.</span></span> <span data-ttu-id="43a7c-123">Entrez **3182061** pour Update 0.3, puis cliquez sur **Rechercher**.</span><span class="sxs-lookup"><span data-stu-id="43a7c-123">Enter **3182061** for Update 0.3, and then click **Search**.</span></span>
   
    <span data-ttu-id="43a7c-124">La liste des correctifs s’affiche, par exemple **StorSimple Virtual Array Update 0.3**.</span><span class="sxs-lookup"><span data-stu-id="43a7c-124">The hotfix listing appears, for example, **StorSimple Virtual Array Update 0.3**.</span></span>
   
    ![Rechercher dans le catalogue](./media/storsimple-ova-install-update-01/download1.png)
4. <span data-ttu-id="43a7c-126">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="43a7c-126">Click **Add**.</span></span> <span data-ttu-id="43a7c-127">La mise à jour est ajoutée au panier.</span><span class="sxs-lookup"><span data-stu-id="43a7c-127">The update is added to the basket.</span></span>
5. <span data-ttu-id="43a7c-128">Cliquez sur **Afficher le panier**.</span><span class="sxs-lookup"><span data-stu-id="43a7c-128">Click **View Basket**.</span></span>
6. <span data-ttu-id="43a7c-129">Cliquez sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="43a7c-129">Click **Download**.</span></span> <span data-ttu-id="43a7c-130">Spécifiez ou **recherchez** l’emplacement local où vous voulez effectuer les téléchargements.</span><span class="sxs-lookup"><span data-stu-id="43a7c-130">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="43a7c-131">Les mises à jour sont téléchargées à l’emplacement spécifié et placées dans un sous-dossier portant le même nom que la mise à jour.</span><span class="sxs-lookup"><span data-stu-id="43a7c-131">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="43a7c-132">Ce dossier peut également être copié sur un partage réseau accessible à partir de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="43a7c-132">The folder can also be copied to a network share that is reachable from the device.</span></span>
7. <span data-ttu-id="43a7c-133">Ouvrez le dossier copié ; vous devriez voir un fichier de package autonome de mise à jour Microsoft `WindowsTH-KB3011067-x64`.</span><span class="sxs-lookup"><span data-stu-id="43a7c-133">Open the copied folder, you should see a Microsoft Update Standalone Package file `WindowsTH-KB3011067-x64`.</span></span> <span data-ttu-id="43a7c-134">Ce fichier est utilisé pour installer la mise à jour ou le correctif logiciel.</span><span class="sxs-lookup"><span data-stu-id="43a7c-134">This file is used to install the update or hotfix.</span></span>

### <a name="install-the-update-or-the-hotfix"></a><span data-ttu-id="43a7c-135">Installation de la mise à jour ou du correctif</span><span class="sxs-lookup"><span data-stu-id="43a7c-135">Install the update or the hotfix</span></span>
<span data-ttu-id="43a7c-136">Avant l'installation de la mise à jour ou du correctif, vérifiez que la mise à jour ou le correctif est téléchargé(e) localement sur votre ordinateur hôte ou accessible via un partage réseau.</span><span class="sxs-lookup"><span data-stu-id="43a7c-136">Prior to the update or hotfix installation, make sure that you have the update or the hotfix downloaded either locally on your host or accessible via a network share.</span></span> 

<span data-ttu-id="43a7c-137">Cette méthode permet d’installer les mises à jour sur un appareil exécutant les versions logicielles GA ou Update 0.1.</span><span class="sxs-lookup"><span data-stu-id="43a7c-137">Use this method to install updates on a device running GA or Update 0.1 software versions.</span></span> <span data-ttu-id="43a7c-138">Cette procédure prend moins de 2 minutes.</span><span class="sxs-lookup"><span data-stu-id="43a7c-138">This procedure takes less than 2 minutes to complete.</span></span> <span data-ttu-id="43a7c-139">Effectuez les opérations suivantes pour installer la mise à jour ou le correctif logiciel.</span><span class="sxs-lookup"><span data-stu-id="43a7c-139">Perform the following steps to install the update or hotfix.</span></span>

#### <a name="to-install-the-update-or-the-hotfix"></a><span data-ttu-id="43a7c-140">Pour installer la mise à jour ou le correctif</span><span class="sxs-lookup"><span data-stu-id="43a7c-140">To install the update or the hotfix</span></span>
1. <span data-ttu-id="43a7c-141">Dans l’interface utilisateur web locale, accédez à **Maintenance** > **Mise à jour logicielle**.</span><span class="sxs-lookup"><span data-stu-id="43a7c-141">In the local web UI, go to **Maintenance** > **Software Update**.</span></span>
   
    ![mettre à jour l'appareil](./media/storsimple-ova-install-update-01/update1m.png)
2. <span data-ttu-id="43a7c-143">Dans le **chemin d’accès au fichier de mise à jour**, entrez le nom du fichier de mise à jour ou de correctif.</span><span class="sxs-lookup"><span data-stu-id="43a7c-143">In **Update file path**, enter the file name for the update or the hotfix.</span></span> <span data-ttu-id="43a7c-144">Vous pouvez également accéder au fichier d'installation de la mise à jour ou du correctif si celui-ci est placé sur un partage réseau.</span><span class="sxs-lookup"><span data-stu-id="43a7c-144">You can also browse to the update or hotfix installation file if placed on a network share.</span></span> <span data-ttu-id="43a7c-145">Cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="43a7c-145">Click **Apply**.</span></span>
   
    ![mettre à jour l'appareil](./media/storsimple-ova-install-update-01/update2m.png)
3. <span data-ttu-id="43a7c-147">Un avertissement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="43a7c-147">A warning is displayed.</span></span> <span data-ttu-id="43a7c-148">Puisqu’il s’agit d’un appareil à nœud unique, l’application de la mise à jour entraîne le redémarrage de l’appareil et provoque un temps d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="43a7c-148">Given this is a single node device, after the update is applied, the device restarts and there is downtime.</span></span> <span data-ttu-id="43a7c-149">Cliquez sur l’icône en forme de coche.</span><span class="sxs-lookup"><span data-stu-id="43a7c-149">Click the check icon.</span></span>
   
   ![mettre à jour l'appareil](./media/storsimple-ova-install-update-01/update3m.png)
4. <span data-ttu-id="43a7c-151">La mise à jour démarre.</span><span class="sxs-lookup"><span data-stu-id="43a7c-151">The update starts.</span></span> <span data-ttu-id="43a7c-152">Une fois l’appareil correctement mis à jour, il est redémarré.</span><span class="sxs-lookup"><span data-stu-id="43a7c-152">After the device is successfully updated, it restarts.</span></span> <span data-ttu-id="43a7c-153">L’interface utilisateur locale n’est pas accessible pendant cet intervalle.</span><span class="sxs-lookup"><span data-stu-id="43a7c-153">The local UI is not accessible in this duration.</span></span>
   
    ![mettre à jour l'appareil](./media/storsimple-ova-install-update-01/update5m.png)
5. <span data-ttu-id="43a7c-155">Une fois le redémarrage effectué, vous êtes redirigé vers la page **Se connecter** .</span><span class="sxs-lookup"><span data-stu-id="43a7c-155">After the restart is complete, you are taken to the **Sign in** page.</span></span> <span data-ttu-id="43a7c-156">Pour vérifier que le logiciel de l’appareil a été mis à jour, accédez à **Maintenance** > **Mise à jour logicielle** dans l’interface utilisateur web locale.</span><span class="sxs-lookup"><span data-stu-id="43a7c-156">To verify that the device software has updated, in the local web UI, go to **Maintenance** > **Software Update**.</span></span> <span data-ttu-id="43a7c-157">La version du logiciel doit être **10.0.0.0.0.10288.0** pour Update 0.3.</span><span class="sxs-lookup"><span data-stu-id="43a7c-157">The displayed software version should be **10.0.0.0.0.10288.0** for Update 0.3.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="43a7c-158">L’affichage des versions logicielles diffère légèrement entre l’interface utilisateur web locale et le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="43a7c-158">We report the software versions in a slightly different way in the local web UI and the Azure classic portal.</span></span> <span data-ttu-id="43a7c-159">Par exemple, la même version est signalée par **10.0.0.0.0.10288** dans l’interface utilisateur web locale et par **10.0.10288.0** sur le Portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="43a7c-159">For example, the local web UI reports **10.0.0.0.0.10288** and the Azure classic portal reports **10.0.10288.0** for the same version.</span></span> 
   > 
   > 
   
    ![mettre à jour l'appareil](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-the-azure-classic-portal"></a><span data-ttu-id="43a7c-161">Utilisation du portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="43a7c-161">Use the Azure classic portal</span></span>
<span data-ttu-id="43a7c-162">Si vous utilisez Update 0.2, nous vous recommandons d’installer les mises à jour par le biais du Portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="43a7c-162">If running Update 0.2, we recommend that you install updates through the Azure classic portal.</span></span> <span data-ttu-id="43a7c-163">La procédure du portail oblige l’utilisateur à rechercher et télécharger les mises à jour avant de les installer.</span><span class="sxs-lookup"><span data-stu-id="43a7c-163">The portal procedure requires the user to scan, download, and then install the updates.</span></span> <span data-ttu-id="43a7c-164">Cette procédure prend environ sept minutes.</span><span class="sxs-lookup"><span data-stu-id="43a7c-164">This procedure takes around 7 minutes to complete.</span></span> <span data-ttu-id="43a7c-165">Effectuez les opérations suivantes pour installer la mise à jour ou le correctif logiciel.</span><span class="sxs-lookup"><span data-stu-id="43a7c-165">Perform the following steps to install the update or hotfix.</span></span>

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

<span data-ttu-id="43a7c-166">Une fois l’installation terminée (lorsque l’état du travail atteint 100 %), accédez à **Appareils > Maintenance > Mises à jour logicielles**.</span><span class="sxs-lookup"><span data-stu-id="43a7c-166">After the installation is complete (as indicated by job status at 100 %), go to **Devices > Maintenance > Software Updates**.</span></span> <span data-ttu-id="43a7c-167">La version du logiciel doit être 10.0.10288.0.</span><span class="sxs-lookup"><span data-stu-id="43a7c-167">The displayed software version should be 10.0.10288.0.</span></span>

![mettre à jour l'appareil](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a><span data-ttu-id="43a7c-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="43a7c-169">Next steps</span></span>
<span data-ttu-id="43a7c-170">En savoir plus sur la [gestion de votre StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="43a7c-170">Learn more about [administering your StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).</span></span>

