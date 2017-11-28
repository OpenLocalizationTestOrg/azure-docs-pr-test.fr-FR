---
title: "aaaEnable connexion Bureau à distance pour un rôle dans les Services de cloud computing Azure | Documents Microsoft"
description: "Tooconfigure votre azure cloud service connexions Bureau à distance tooallow d’application"
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="cd6f6-103">Activer une connexion Bureau à distance pour un rôle dans Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="cd6f6-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cd6f6-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="cd6f6-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="cd6f6-105">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="cd6f6-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="cd6f6-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd6f6-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="cd6f6-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cd6f6-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="cd6f6-108">Bureau à distance vous permet de bureau de hello tooaccess d’un rôle en cours d’exécution dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-108">Remote Desktop enables you tooaccess hello desktop of a role running in Azure.</span></span> <span data-ttu-id="cd6f6-109">Vous pouvez utiliser un tootroubleshoot de connexion Bureau à distance et diagnostiquer les problèmes avec votre application pendant son exécution.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-109">You can use a Remote Desktop connection tootroubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="cd6f6-110">Vous pouvez activer une connexion Bureau à distance dans votre rôle pendant le développement en incluant les modules de bureau à distance hello dans votre définition de service, ou vous pouvez choisir tooenable Bureau à distance via hello Extension Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-110">You can enable a Remote Desktop connection in your role during development by including hello Remote Desktop modules in your service definition or you can choose tooenable Remote Desktop through hello Remote Desktop Extension.</span></span> <span data-ttu-id="cd6f6-111">Hello approche par défaut est toouse hello Bureau à distance extension que vous pouvez activer le Bureau à distance même après que l’application hello est déployée sans tooredeploy votre application.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-111">hello preferred approach is toouse hello Remote Desktop extension as you can enable Remote Desktop even after hello application is deployed without having tooredeploy your application.</span></span>

## <a name="configure-remote-desktop-from-hello-azure-portal"></a><span data-ttu-id="cd6f6-112">Configurer le Bureau à distance à partir de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="cd6f6-112">Configure Remote Desktop from hello Azure portal</span></span>
<span data-ttu-id="cd6f6-113">Hello portail Azure utilise approche d’Extension Bureau à distance hello même après que l’application hello est déployée, vous pouvez activer Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-113">hello Azure portal uses hello Remote Desktop Extension approach so you can enable Remote Desktop even after hello application is deployed.</span></span> <span data-ttu-id="cd6f6-114">Hello **Bureau à distance** panneau pour votre service cloud vous permet de tooenable Bureau à distance, modifier le compte d’administrateur local hello utilisé tooconnect toohello virtuels, les certificats hello utilisés dans l’authentification et définir hello date d’expiration.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-114">hello **Remote Desktop** blade for your cloud service allows you tooenable Remote Desktop, change hello local Administrator account used tooconnect toohello virtual machines, hello certificate used in authentication and set hello expiration date.</span></span>

1. <span data-ttu-id="cd6f6-115">Cliquez sur **Services de cloud computing**, cliquez sur nom hello du service de cloud hello, puis cliquez sur **Bureau à distance**.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-115">Click **Cloud Services**, click hello name of hello cloud service, and then click **Remote Desktop**.</span></span>

    ![Bureau à distance des Services Cloud](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="cd6f6-117">Choisissez si vous souhaitez tooenable Bureau à distance pour un rôle individuel ou pour tous les rôles, puis modifiez trop de valeur du sélecteur de hello hello**activé**.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-117">Choose whether you want tooenable Remote Desktop for an individual role or for all roles, then change hello value of hello switcher too**Enabled**.</span></span>

3. <span data-ttu-id="cd6f6-118">Renseignez les champs hello requis pour le nom d’utilisateur, mot de passe, d’expiration et certificat.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-118">Fill in hello required fields for user name, password, expiry, and certificate.</span></span>

    ![Bureau à distance des Services Cloud](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="cd6f6-120">toutes les instances de rôle sont redémarrées lorsque vous activez pour la première fois le Bureau à distance et cliquez sur OK (coche).</span><span class="sxs-lookup"><span data-stu-id="cd6f6-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="cd6f6-121">tooprevent un redémarrage, le mot de passe hello hello certificat tooencrypt utilisé doit être installé sur le rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-121">tooprevent a reboot, hello certificate used tooencrypt hello password must be installed on hello role.</span></span> <span data-ttu-id="cd6f6-122">tooprevent un redémarrage, [télécharger un certificat pour le service cloud hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) , puis revenez toothis la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-122">tooprevent a restart, [upload a certificate for hello cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return toothis dialog.</span></span>
   >
   >
3. <span data-ttu-id="cd6f6-123">Dans **rôles**, sélectionnez rôle hello souhaité tooupdate **tous les** pour tous les rôles.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-123">In **Roles**, select hello role you want tooupdate or select **All** for all roles.</span></span>

4. <span data-ttu-id="cd6f6-124">Lorsque les mises à jour de la configuration sont terminées, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="cd6f6-125">Il prendra un certain temps avant que vos instances de rôle sont des connexions de tooreceive prêt.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-125">It will take a few moments before your role instances are ready tooreceive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="cd6f6-126">À distance dans les instances de rôle</span><span class="sxs-lookup"><span data-stu-id="cd6f6-126">Remote into role instances</span></span>
<span data-ttu-id="cd6f6-127">Une fois que Bureau à distance est activé sur les rôles de hello, vous pouvez établir une connexion directement à partir de hello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="cd6f6-127">Once Remote Desktop is enabled on hello roles, you can initiate a connection directly from hello Azure Portal:</span></span>

1. <span data-ttu-id="cd6f6-128">Cliquez sur **Instances** tooopen hello **Instances** panneau.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-128">Click **Instances** tooopen hello **Instances** blade.</span></span>
2. <span data-ttu-id="cd6f6-129">Sélectionnez une instance de rôle pour laquelle la fonctionnalité Bureau à distance est configurée.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="cd6f6-130">Cliquez sur **Connect** toodownload un RDP de fichiers pour une instance de rôle hello.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-130">Click **Connect** toodownload an RDP file for hello role instance.</span></span>

    ![Bureau à distance des Services Cloud](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="cd6f6-132">Cliquez sur **ouvrir** , puis **Connect** toostart hello connexion Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-132">Click **Open** and then **Connect** toostart hello Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="cd6f6-133">Si votre service cloud se trouve derrière un groupe de sécurité réseau, vous devrez peut-être toocreate les règles qui autorisent le trafic sur les ports **3389** et **20000**.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-133">If your cloud service is sitting behind an NSG, you may need toocreate rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="cd6f6-134">Bureau à distance utilise le port **3389**.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="cd6f6-135">Les instances de Service cloud sont à charge équilibrée, donc vous ne pouvez pas contrôler directement le tooconnect d’instance pour.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-135">Cloud Service instances are load balanced, so you can't directly control which instance tooconnect to.</span></span>  <span data-ttu-id="cd6f6-136">Hello *RemoteForwarder* et *RemoteAccess* agents gérer le trafic RDP et hello client toosend un cookie RDP et de spécifier un tooconnect instance individuelle pour.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-136">hello *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow hello client toosend an RDP cookie and specify an individual instance tooconnect to.</span></span>  <span data-ttu-id="cd6f6-137">Hello *RemoteForwarder* et *RemoteAccess* agents nécessitent ce port **20000*** être ouvert, ce qui peut être bloqué si vous disposez d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="cd6f6-137">hello *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cd6f6-138">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="cd6f6-138">Additional resources</span></span>

<span data-ttu-id="cd6f6-139">[Comment tooConfigure Services de cloud computing](cloud-services-how-to-configure.md)
[Cloud FAQ - des services Bureau à distance](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="cd6f6-139">[How tooConfigure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
