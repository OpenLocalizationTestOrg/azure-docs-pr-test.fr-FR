---
title: aaaHow tooconfigure un service cloud (portail) | Documents Microsoft
description: "Découvrez comment tooconfigure cloud services dans Azure. En savoir plus de la configuration du service cloud tooupdate hello et configurer les instances de toorole d’accès à distance. Ces exemples utilisent hello portail Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a><span data-ttu-id="c165f-105">Comment les Services de cloud computing tooConfigure</span><span class="sxs-lookup"><span data-stu-id="c165f-105">How tooConfigure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c165f-106">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="c165f-106">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="c165f-107">portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="c165f-107">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="c165f-108">Vous pouvez configurer les paramètres de hello couramment utilisé pour un service cloud dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c165f-108">You can configure hello most commonly used settings for a cloud service in hello Azure portal.</span></span> <span data-ttu-id="c165f-109">Ou, si vous aimez tooupdate vos fichiers de configuration directement, téléchargez un tooupdate de fichier de configuration de service, puis téléchargez hello mise à jour de service de cloud de hello de fichier et de mise à jour avec les modifications de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="c165f-109">Or, if you like tooupdate your configuration files directly, download a service configuration file tooupdate, and then upload hello updated file and update hello cloud service with hello configuration changes.</span></span> <span data-ttu-id="c165f-110">Dans les deux cas, les mises à jour configuration hello sont émis tooall les instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="c165f-110">Either way, hello configuration updates are pushed out tooall role instances.</span></span>

<span data-ttu-id="c165f-111">Vous pouvez également gérer des instances de hello de vos rôles de service cloud ou le Bureau à distance dans les.</span><span class="sxs-lookup"><span data-stu-id="c165f-111">You can also manage hello instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="c165f-112">Azure assurer disponibilité de service 99,95 % au cours de hello mises à jour de la configuration si vous disposez d’au moins deux instances de rôle pour chaque rôle.</span><span class="sxs-lookup"><span data-stu-id="c165f-112">Azure can only ensure 99.95 percent service availability during hello configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="c165f-113">Qui permet de demandes de client d’ordinateur virtuel tooprocess pendant hello autres est en cours de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="c165f-113">That enables one virtual machine tooprocess client requests while hello other is being updated.</span></span> <span data-ttu-id="c165f-114">Pour plus d'informations, consultez la page [Contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="c165f-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="c165f-115">Modification d'un service cloud</span><span class="sxs-lookup"><span data-stu-id="c165f-115">Change a cloud service</span></span>
<span data-ttu-id="c165f-116">Après ouverture hello [portail Azure](https://portal.azure.com/), accédez tooyour le service cloud.</span><span class="sxs-lookup"><span data-stu-id="c165f-116">After opening hello [Azure portal](https://portal.azure.com/), navigate tooyour cloud service.</span></span> <span data-ttu-id="c165f-117">Vous pouvez alors gérer plusieurs aspects.</span><span class="sxs-lookup"><span data-stu-id="c165f-117">From here, you manage many aspects of it.</span></span>

![Page Paramètres](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="c165f-119">Hello **paramètres** ou **tous les paramètres** liens ouvriront hello **paramètres** panneau dans laquelle vous pouvez modifier hello **propriétés**, modifier hello **Configuration**, gérer hello **certificats**, le programme d’installation **règles d’alerte**et gérer hello **utilisateurs** qui ont accès service de cloud computing toothis.</span><span class="sxs-lookup"><span data-stu-id="c165f-119">hello **Settings** or **All settings** links will open up hello **Settings** blade where you can change hello **Properties**, change hello **Configuration**, manage hello **Certificates**, setup **Alert rules**, and manage hello **Users** who have access toothis cloud service.</span></span>

![Panneau Paramètres du service cloud Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="c165f-121">Gestion de la version de SE invité</span><span class="sxs-lookup"><span data-stu-id="c165f-121">Manage Guest OS version</span></span>

<span data-ttu-id="c165f-122">Par défaut, Azure met régulièrement à jour votre invité du système d’exploitation toohello dernière image pris en charge dans hello famille de systèmes d’exploitation que vous avez spécifié dans votre configuration de service (.cscfg), par exemple, Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="c165f-122">By default, Azure periodically updates your guest OS toohello latest supported image within hello OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="c165f-123">Si vous devez tootarget une version du système d’exploitation spécifique, vous pouvez la définir dans hello **Configuration** panneau.</span><span class="sxs-lookup"><span data-stu-id="c165f-123">If you need tootarget a specific OS version, you can set it in hello **Configuration** blade.</span></span>

![Définition de la version du système d’exploitation](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> <span data-ttu-id="c165f-125">Lorsque vous choisissez une version de système d’exploitation spécifique, les mises à jour de SE automatiques sont désactivées et l’application de correctifs relève alors de votre responsabilité.</span><span class="sxs-lookup"><span data-stu-id="c165f-125">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="c165f-126">Vous devez vous assurer que vos instances de rôle sont reçoit des mises à jour, ou vous pouvez exposer les vulnérabilités toosecurity application.</span><span class="sxs-lookup"><span data-stu-id="c165f-126">You must ensure that your role instances are receiving updates or you may expose your application toosecurity vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="c165f-127">Surveillance</span><span class="sxs-lookup"><span data-stu-id="c165f-127">Monitoring</span></span>
<span data-ttu-id="c165f-128">Vous pouvez ajouter le service de cloud tooyour des alertes.</span><span class="sxs-lookup"><span data-stu-id="c165f-128">You can add alerts tooyour cloud service.</span></span> <span data-ttu-id="c165f-129">Cliquez sur **Paramètres** > **Règles d’alerte** > **Ajouter une alerte**.</span><span class="sxs-lookup"><span data-stu-id="c165f-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="c165f-130">Vous pouvez alors configurer une alerte.</span><span class="sxs-lookup"><span data-stu-id="c165f-130">From here, you can setup an alert.</span></span> <span data-ttu-id="c165f-131">Avec hello **métrique** zone déroulante, vous pouvez configurer une alerte pour hello les types de données suivants.</span><span class="sxs-lookup"><span data-stu-id="c165f-131">With hello **Metric** drop down box, you can setup an alert for hello following types of data.</span></span>

* <span data-ttu-id="c165f-132">Lecture du disque</span><span class="sxs-lookup"><span data-stu-id="c165f-132">Disk read</span></span>
* <span data-ttu-id="c165f-133">Écriture sur le disque</span><span class="sxs-lookup"><span data-stu-id="c165f-133">Disk write</span></span>
* <span data-ttu-id="c165f-134">Entrée réseau</span><span class="sxs-lookup"><span data-stu-id="c165f-134">Network in</span></span>
* <span data-ttu-id="c165f-135">Sortie réseau</span><span class="sxs-lookup"><span data-stu-id="c165f-135">Network out</span></span>
* <span data-ttu-id="c165f-136">Pourcentage UC</span><span class="sxs-lookup"><span data-stu-id="c165f-136">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="c165f-137">Configuration de la surveillance à partir d’une vignette de métrique</span><span class="sxs-lookup"><span data-stu-id="c165f-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="c165f-138">Au lieu d’utiliser **paramètres** > **les règles d’alerte**, vous pouvez cliquer sur une des vignettes de métrique hello Bonjour **analyse** section Hello **Cloud service** panneau.</span><span class="sxs-lookup"><span data-stu-id="c165f-138">Instead of using **Settings** > **Alert Rules**, you can click on one of hello metric tiles in hello **Monitoring** section of hello **Cloud service** blade.</span></span>

![Surveillance du service cloud](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="c165f-140">À ce stade, vous pouvez personnaliser le graphique hello utilisé avec la vignette de hello, ou ajouter une règle d’alerte.</span><span class="sxs-lookup"><span data-stu-id="c165f-140">From here you can customize hello chart used with hello tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="c165f-141">Redémarrage, réinitialisation ou Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="c165f-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="c165f-142">À ce stade, vous ne pouvez pas configurer Bureau à distance à l’aide de hello **portail Azure**.</span><span class="sxs-lookup"><span data-stu-id="c165f-142">At this time you cannot configure remote desktop using hello **Azure portal**.</span></span> <span data-ttu-id="c165f-143">Toutefois, vous pouvez configurer il via hello [portail Azure classic](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), ou via [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="c165f-143">However, you can set it up through hello [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="c165f-144">Tout d’abord, cliquez sur l’instance de service cloud hello.</span><span class="sxs-lookup"><span data-stu-id="c165f-144">First, click on hello cloud service instance.</span></span>

![Instance de service cloud](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="c165f-146">Hello panneau qui s’ouvre, vous pouvez établir une connexion Bureau à distance, redémarrer à distance hello instance ou à distance réinitialisation (démarrage avec une image actualisée) hello instance.</span><span class="sxs-lookup"><span data-stu-id="c165f-146">From hello blade that opens you can initiate a remote desktop connection, remotely reboot hello instance, or remotely reimage (start with a fresh image) hello instance.</span></span>

![Boutons d’instance de service cloud](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="c165f-148">Reconfigurer votre fichier .cscfg</span><span class="sxs-lookup"><span data-stu-id="c165f-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="c165f-149">Vous devrez peut-être tooreconfigure votre service cloud via hello [la configuration de service (cscfg)](cloud-services-model-and-package.md#cscfg) fichier.</span><span class="sxs-lookup"><span data-stu-id="c165f-149">You may need tooreconfigure your cloud service through hello [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="c165f-150">Vous devez toodownload votre .cscfg de fichier, modifiez-le, puis téléchargez-le.</span><span class="sxs-lookup"><span data-stu-id="c165f-150">First you need toodownload your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="c165f-151">Cliquez sur hello **paramètres** icône ou hello **tous les paramètres** lien tooopen des hello **paramètres** panneau.</span><span class="sxs-lookup"><span data-stu-id="c165f-151">Click on hello **Settings** icon or hello **All settings** link tooopen up hello **Settings** blade.</span></span>

    ![Page Paramètres](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="c165f-153">Cliquez sur hello **Configuration** élément.</span><span class="sxs-lookup"><span data-stu-id="c165f-153">Click on hello **Configuration** item.</span></span>

    ![Panneau de configuration](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="c165f-155">Cliquez sur hello **télécharger** bouton.</span><span class="sxs-lookup"><span data-stu-id="c165f-155">Click on hello **Download** button.</span></span>

    ![Télécharger](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="c165f-157">Une fois que vous mettez à jour le fichier de configuration de service hello, télécharger et appliquer les mises à jour de la configuration hello :</span><span class="sxs-lookup"><span data-stu-id="c165f-157">After you update hello service configuration file, upload and apply hello configuration updates:</span></span>

    ![Télécharger](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="c165f-159">Sélectionnez le fichier .cscfg de hello et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c165f-159">Select hello .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c165f-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c165f-160">Next steps</span></span>
* <span data-ttu-id="c165f-161">Découvrez comment trop[déployer un service cloud](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c165f-161">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="c165f-162">Configurez un [nom de domaine personnalisé](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c165f-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="c165f-163">[Gérez votre service cloud](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c165f-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="c165f-164">Configurez des [certificats SSL](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c165f-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
