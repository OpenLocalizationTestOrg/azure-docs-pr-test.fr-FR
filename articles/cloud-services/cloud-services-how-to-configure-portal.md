---
title: "Configuration d’un service cloud (portail) | Microsoft Docs"
description: "Découvrez comment configurer des services cloud dans Azure. Apprenez à mettre à jour la configuration d'un service cloud et à configurer l'accès distant aux instances de rôle. Ces exemples utilisent le portail Azure."
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
ms.openlocfilehash: a7e891d05ffe4cc2b4f68dce072a81499cc6de80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-cloud-services"></a><span data-ttu-id="9ddb6-105">Configuration des services cloud</span><span class="sxs-lookup"><span data-stu-id="9ddb6-105">How to Configure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ddb6-106">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="9ddb6-106">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="9ddb6-107">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="9ddb6-107">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="9ddb6-108">Vous pouvez configurer les paramètres les plus couramment utilisés pour un service cloud dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-108">You can configure the most commonly used settings for a cloud service in the Azure portal.</span></span> <span data-ttu-id="9ddb6-109">Ou, si vous voulez mettre à jour directement vos fichiers de configuration, téléchargez un fichier de configuration de service pour le mettre à jour, puis chargez-le et mettez à jour le service cloud avec les modifications de la configuration.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-109">Or, if you like to update your configuration files directly, download a service configuration file to update, and then upload the updated file and update the cloud service with the configuration changes.</span></span> <span data-ttu-id="9ddb6-110">Dans les deux cas, les mises à jour de la configuration sont transmises à toutes les instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-110">Either way, the configuration updates are pushed out to all role instances.</span></span>

<span data-ttu-id="9ddb6-111">Vous pouvez également gérer les instances de vos rôles de service cloud ou le Bureau à distance qui s’y trouve.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-111">You can also manage the instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="9ddb6-112">Azure ne peut garantir que 99,95 % de disponibilité du service pendant les mises à jour de la configuration si vous avez au moins deux instances de rôle pour chaque rôle.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-112">Azure can only ensure 99.95 percent service availability during the configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="9ddb6-113">Cela permet à une machine virtuelle de traiter les demandes du client pendant que l'autre est mise à jour.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-113">That enables one virtual machine to process client requests while the other is being updated.</span></span> <span data-ttu-id="9ddb6-114">Pour plus d'informations, consultez la page [Contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="9ddb6-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="9ddb6-115">Modification d'un service cloud</span><span class="sxs-lookup"><span data-stu-id="9ddb6-115">Change a cloud service</span></span>
<span data-ttu-id="9ddb6-116">Dans le [portail Azure](https://portal.azure.com/), accédez à votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-116">After opening the [Azure portal](https://portal.azure.com/), navigate to your cloud service.</span></span> <span data-ttu-id="9ddb6-117">Vous pouvez alors gérer plusieurs aspects.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-117">From here, you manage many aspects of it.</span></span>

![Page Paramètres](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="9ddb6-119">Les liens **Paramètres** ou **Tous les paramètres** permettent d’accéder au panneau **Paramètres** où vous pouvez modifier les **propriétés**, modifier la **configuration**, gérer les **certificats**, configurer les **règles d’alerte** et gérer les **utilisateurs** qui ont accès à ce service cloud.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-119">The **Settings** or **All settings** links will open up the **Settings** blade where you can change the **Properties**, change the **Configuration**, manage the **Certificates**, setup **Alert rules**, and manage the **Users** who have access to this cloud service.</span></span>

![Panneau Paramètres du service cloud Azure](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="9ddb6-121">Gestion de la version de SE invité</span><span class="sxs-lookup"><span data-stu-id="9ddb6-121">Manage Guest OS version</span></span>

<span data-ttu-id="9ddb6-122">Par défaut, Azure met régulièrement à jour votre SE invité vers la dernière image prise en charge d’un produit de la famille de systèmes d’exploitation que vous avez spécifiée dans votre configuration de service (.cscfg), par exemple, Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-122">By default, Azure periodically updates your guest OS to the latest supported image within the OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="9ddb6-123">Si vous devez cibler une version de système d’exploitation spécifique, vous pouvez la définir dans le panneau **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-123">If you need to target a specific OS version, you can set it in the **Configuration** blade.</span></span>

![Définition de la version du système d’exploitation](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> <span data-ttu-id="9ddb6-125">Lorsque vous choisissez une version de système d’exploitation spécifique, les mises à jour de SE automatiques sont désactivées et l’application de correctifs relève alors de votre responsabilité.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-125">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="9ddb6-126">Vous devez vous assurer que vos instances de rôle reçoivent les mises à jour, sans quoi votre application serait exposée à des failles de sécurité.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-126">You must ensure that your role instances are receiving updates or you may expose your application to security vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="9ddb6-127">Analyse</span><span class="sxs-lookup"><span data-stu-id="9ddb6-127">Monitoring</span></span>
<span data-ttu-id="9ddb6-128">Vous pouvez ajouter des alertes à votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-128">You can add alerts to your cloud service.</span></span> <span data-ttu-id="9ddb6-129">Cliquez sur **Paramètres** > **Règles d’alerte** > **Ajouter une alerte**.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="9ddb6-130">Vous pouvez alors configurer une alerte.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-130">From here, you can setup an alert.</span></span> <span data-ttu-id="9ddb6-131">Avec la liste déroulante **Métrique** , vous pouvez configurer une alerte pour les types de données suivants.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-131">With the **Metric** drop down box, you can setup an alert for the following types of data.</span></span>

* <span data-ttu-id="9ddb6-132">Lecture du disque</span><span class="sxs-lookup"><span data-stu-id="9ddb6-132">Disk read</span></span>
* <span data-ttu-id="9ddb6-133">Écriture sur le disque</span><span class="sxs-lookup"><span data-stu-id="9ddb6-133">Disk write</span></span>
* <span data-ttu-id="9ddb6-134">Entrée réseau</span><span class="sxs-lookup"><span data-stu-id="9ddb6-134">Network in</span></span>
* <span data-ttu-id="9ddb6-135">Sortie réseau</span><span class="sxs-lookup"><span data-stu-id="9ddb6-135">Network out</span></span>
* <span data-ttu-id="9ddb6-136">Pourcentage UC</span><span class="sxs-lookup"><span data-stu-id="9ddb6-136">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="9ddb6-137">Configuration de la surveillance à partir d’une vignette de métrique</span><span class="sxs-lookup"><span data-stu-id="9ddb6-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="9ddb6-138">Au lieu d’utiliser **Paramètres** > **Règles d’alerte**, vous pouvez cliquer sur l’une des vignettes de métrique dans la section **Surveillance** du panneau **Service cloud**.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-138">Instead of using **Settings** > **Alert Rules**, you can click on one of the metric tiles in the **Monitoring** section of the **Cloud service** blade.</span></span>

![Surveillance du service cloud](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="9ddb6-140">Vous pouvez alors personnaliser le graphique utilisé avec la vignette ou ajouter une règle d’alerte.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-140">From here you can customize the chart used with the tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="9ddb6-141">Redémarrage, réinitialisation ou Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="9ddb6-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="9ddb6-142">À ce stade, vous ne pouvez pas configurer le Bureau à distance à l’aide du **portail Azure**.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-142">At this time you cannot configure remote desktop using the **Azure portal**.</span></span> <span data-ttu-id="9ddb6-143">Toutefois, vous pouvez le configurer par le biais du [portail Azure Classic](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md) ou [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="9ddb6-143">However, you can set it up through the [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="9ddb6-144">Tout d’abord, cliquez sur l’instance de service cloud.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-144">First, click on the cloud service instance.</span></span>

![Instance de service cloud](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="9ddb6-146">Dans le panneau qui s’affiche, vous pouvez initier une connexion Bureau à distance, redémarrer l’instance à distance ou réinitialiser l’instance à distance (pour commencer avec une toute nouvelle image).</span><span class="sxs-lookup"><span data-stu-id="9ddb6-146">From the blade that opens you can initiate a remote desktop connection, remotely reboot the instance, or remotely reimage (start with a fresh image) the instance.</span></span>

![Boutons d’instance de service cloud](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="9ddb6-148">Reconfigurer votre fichier .cscfg</span><span class="sxs-lookup"><span data-stu-id="9ddb6-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="9ddb6-149">Vous devrez peut-être reconfigurer votre service cloud via le fichier [configuration de service (cscfg)](cloud-services-model-and-package.md#cscfg).</span><span class="sxs-lookup"><span data-stu-id="9ddb6-149">You may need to reconfigure your cloud service through the [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="9ddb6-150">Vous devez d’abord télécharger le fichier .cscfg, puis le modifier et le charger.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-150">First you need to download your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="9ddb6-151">Cliquez sur l’icône **Paramètres** ou sur le lien **Tous les paramètres** pour ouvrir le panneau **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-151">Click on the **Settings** icon or the **All settings** link to open up the **Settings** blade.</span></span>

    ![Page Paramètres](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="9ddb6-153">Cliquez sur l’élément **Configuration** .</span><span class="sxs-lookup"><span data-stu-id="9ddb6-153">Click on the **Configuration** item.</span></span>

    ![Panneau de configuration](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="9ddb6-155">Cliquez sur le bouton **Download** .</span><span class="sxs-lookup"><span data-stu-id="9ddb6-155">Click on the **Download** button.</span></span>

    ![Download](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="9ddb6-157">Après la mise à jour du fichier de configuration de service, téléchargez et appliquez les mises à jour de la configuration :</span><span class="sxs-lookup"><span data-stu-id="9ddb6-157">After you update the service configuration file, upload and apply the configuration updates:</span></span>

    ![Télécharger](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="9ddb6-159">Sélectionnez le fichier .cscfg et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9ddb6-159">Select the .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ddb6-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9ddb6-160">Next steps</span></span>
* <span data-ttu-id="9ddb6-161">Découvrez comment [déployer un service cloud](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9ddb6-161">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="9ddb6-162">Configurez un [nom de domaine personnalisé](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9ddb6-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="9ddb6-163">[Gérez votre service cloud](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9ddb6-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="9ddb6-164">Configurez des [certificats SSL](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9ddb6-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>
