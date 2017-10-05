---
title: "Activer une connexion Bureau à distance pour un rôle dans Azure Cloud Services | Microsoft Docs"
description: "Configuration de l’application de service cloud Azure pour autoriser les connexions Bureau à distance"
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
ms.openlocfilehash: 0ff7fde5f3753aa6a24fb0af54d68d0dc0bd96a4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a><span data-ttu-id="4a032-103">Activer une connexion Bureau à distance pour un rôle dans Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="4a032-103">Enable Remote Desktop Connection for a Role in Azure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4a032-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="4a032-104">Azure portal</span></span>](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [<span data-ttu-id="4a032-105">Portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="4a032-105">Azure classic portal</span></span>](cloud-services-role-enable-remote-desktop.md)
> * [<span data-ttu-id="4a032-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a032-106">PowerShell</span></span>](cloud-services-role-enable-remote-desktop-powershell.md)
> * [<span data-ttu-id="4a032-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4a032-107">Visual Studio</span></span>](../vs-azure-tools-remote-desktop-roles.md)
>
>

<span data-ttu-id="4a032-108">Le Bureau à distance vous permet d'accéder au bureau d'un rôle en cours d'exécution dans Azure.</span><span class="sxs-lookup"><span data-stu-id="4a032-108">Remote Desktop enables you to access the desktop of a role running in Azure.</span></span> <span data-ttu-id="4a032-109">Vous pouvez utiliser une connexion Bureau à distance pour dépanner et diagnostiquer les problèmes rencontrés par votre application lorsqu'elle est en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="4a032-109">You can use a Remote Desktop connection to troubleshoot and diagnose problems with your application while it is running.</span></span>

<span data-ttu-id="4a032-110">Vous pouvez activer une connexion Bureau à distance dans votre rôle pendant le développement en incluant les modules Bureau à distance dans votre définition de service. Vous pouvez aussi activer le Bureau à distance via l’extension Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="4a032-110">You can enable a Remote Desktop connection in your role during development by including the Remote Desktop modules in your service definition or you can choose to enable Remote Desktop through the Remote Desktop Extension.</span></span> <span data-ttu-id="4a032-111">Cette deuxième approche est recommandée, car elle vous permet d’activer le Bureau à distance sans avoir à redéployer votre application.</span><span class="sxs-lookup"><span data-stu-id="4a032-111">The preferred approach is to use the Remote Desktop extension as you can enable Remote Desktop even after the application is deployed without having to redeploy your application.</span></span>

## <a name="configure-remote-desktop-from-the-azure-portal"></a><span data-ttu-id="4a032-112">Configurer le Bureau à distance à partir du portail Azure</span><span class="sxs-lookup"><span data-stu-id="4a032-112">Configure Remote Desktop from the Azure portal</span></span>
<span data-ttu-id="4a032-113">Le portail Azure utilise l’approche basée sur l’extension Bureau à distance, ce qui vous permet d’activer le Bureau à distance même après avoir déployé l’application.</span><span class="sxs-lookup"><span data-stu-id="4a032-113">The Azure portal uses the Remote Desktop Extension approach so you can enable Remote Desktop even after the application is deployed.</span></span> <span data-ttu-id="4a032-114">Le panneau **Bureau à distance** de votre service cloud vous permet d’activer le Bureau à distance, de changer le compte Administrateur local utilisé pour la connexion aux machines virtuelles ou le certificat employé dans l’authentification, et de définir la date d’expiration.</span><span class="sxs-lookup"><span data-stu-id="4a032-114">The **Remote Desktop** blade for your cloud service allows you to enable Remote Desktop, change the local Administrator account used to connect to the virtual machines, the certificate used in authentication and set the expiration date.</span></span>

1. <span data-ttu-id="4a032-115">Cliquez sur **Cloud Services**, cliquez sur le nom du service cloud, puis sur **Bureau à distance**.</span><span class="sxs-lookup"><span data-stu-id="4a032-115">Click **Cloud Services**, click the name of the cloud service, and then click **Remote Desktop**.</span></span>

    ![Bureau à distance des Services Cloud](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. <span data-ttu-id="4a032-117">Choisissez si vous souhaitez activer le Bureau à distance pour un rôle individuel ou pour tous les rôles, puis modifier la valeur du sélecteur en **Activé**.</span><span class="sxs-lookup"><span data-stu-id="4a032-117">Choose whether you want to enable Remote Desktop for an individual role or for all roles, then change the value of the switcher to **Enabled**.</span></span>

3. <span data-ttu-id="4a032-118">Renseignez les champs requis pour le nom d’utilisateur, le mot de passe, la date d’expiration et le certificat.</span><span class="sxs-lookup"><span data-stu-id="4a032-118">Fill in the required fields for user name, password, expiry, and certificate.</span></span>

    ![Bureau à distance des Services Cloud](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > <span data-ttu-id="4a032-120">toutes les instances de rôle sont redémarrées lorsque vous activez pour la première fois le Bureau à distance et cliquez sur OK (coche).</span><span class="sxs-lookup"><span data-stu-id="4a032-120">All role instances will be restarted when you first enable Remote Desktop and click OK (checkmark).</span></span> <span data-ttu-id="4a032-121">Pour éviter un redémarrage, le certificat utilisé pour chiffrer le mot de passe doit être installé sur le rôle.</span><span class="sxs-lookup"><span data-stu-id="4a032-121">To prevent a reboot, the certificate used to encrypt the password must be installed on the role.</span></span> <span data-ttu-id="4a032-122">Pour éviter un redémarrage, [téléchargez un certificat pour le service cloud](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) , puis revenez à cette boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4a032-122">To prevent a restart, [upload a certificate for the cloud service](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) and then return to this dialog.</span></span>
   >
   >
3. <span data-ttu-id="4a032-123">Dans **Roles**, sélectionnez le rôle que vous voulez mettre à jour ou sélectionnez **Tous** pour tous les rôles.</span><span class="sxs-lookup"><span data-stu-id="4a032-123">In **Roles**, select the role you want to update or select **All** for all roles.</span></span>

4. <span data-ttu-id="4a032-124">Lorsque les mises à jour de la configuration sont terminées, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4a032-124">When you finish your configuration updates, click **Save**.</span></span> <span data-ttu-id="4a032-125">Vos instances de rôles pourront recevoir les connexions quelques instants plus tard.</span><span class="sxs-lookup"><span data-stu-id="4a032-125">It will take a few moments before your role instances are ready to receive connections.</span></span>

## <a name="remote-into-role-instances"></a><span data-ttu-id="4a032-126">À distance dans les instances de rôle</span><span class="sxs-lookup"><span data-stu-id="4a032-126">Remote into role instances</span></span>
<span data-ttu-id="4a032-127">Une fois que le Bureau à distance est activé sur les rôles, vous pouvez initier une connexion directement à partir du portail Azure :</span><span class="sxs-lookup"><span data-stu-id="4a032-127">Once Remote Desktop is enabled on the roles, you can initiate a connection directly from the Azure Portal:</span></span>

1. <span data-ttu-id="4a032-128">Pour ouvrir le panneau **Instances**, cliquez sur **Instances**.</span><span class="sxs-lookup"><span data-stu-id="4a032-128">Click **Instances** to open the **Instances** blade.</span></span>
2. <span data-ttu-id="4a032-129">Sélectionnez une instance de rôle pour laquelle la fonctionnalité Bureau à distance est configurée.</span><span class="sxs-lookup"><span data-stu-id="4a032-129">Select a role instance that has Remote Desktop configured.</span></span>
3. <span data-ttu-id="4a032-130">Cliquez sur **Connecter** afin de télécharger un fichier RDP pour l’instance de rôle.</span><span class="sxs-lookup"><span data-stu-id="4a032-130">Click **Connect** to download an RDP file for the role instance.</span></span>

    ![Bureau à distance des Services Cloud](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. <span data-ttu-id="4a032-132">Cliquez sur **Ouvrir**, puis sur **Connecter** pour démarrer la connexion Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="4a032-132">Click **Open** and then **Connect** to start the Remote Desktop connection.</span></span>

>[!NOTE]
> <span data-ttu-id="4a032-133">Si votre service cloud se trouve derrière un groupe de sécurité réseau, il peut être nécessaire de créer des règles qui autorisent le trafic sur les ports **3389** et **20000**.</span><span class="sxs-lookup"><span data-stu-id="4a032-133">If your cloud service is sitting behind an NSG, you may need to create rules that allow traffic on ports **3389** and **20000**.</span></span>  <span data-ttu-id="4a032-134">Bureau à distance utilise le port **3389**.</span><span class="sxs-lookup"><span data-stu-id="4a032-134">Remote Desktop uses port **3389**.</span></span>  <span data-ttu-id="4a032-135">Les instances de service cloud sont soumis à l’équilibrage de charge, donc vous ne pouvez pas contrôler directement à quelle instance vous vous connectez.</span><span class="sxs-lookup"><span data-stu-id="4a032-135">Cloud Service instances are load balanced, so you can't directly control which instance to connect to.</span></span>  <span data-ttu-id="4a032-136">Les agents *RemoteForwarder* et *RemoteAccess* gèrent le trafic RDP, et permettent au client d’envoyer un cookie RDP et de spécifier une instance individuelle à laquelle se connecter.</span><span class="sxs-lookup"><span data-stu-id="4a032-136">The *RemoteForwarder* and *RemoteAccess* agents manage RDP traffic and allow the client to send an RDP cookie and specify an individual instance to connect to.</span></span>  <span data-ttu-id="4a032-137">Les agents *RemoteForwarder* et *RemoteAccess* nécessitent que ce port **20000*** soit ouvert : il peut être bloqué si vous avez un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="4a032-137">The *RemoteForwarder* and *RemoteAccess* agents require that port **20000*** be opened, which may be blocked if you have an NSG.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4a032-138">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4a032-138">Additional resources</span></span>

<span data-ttu-id="4a032-139">[Configuration des services cloud](cloud-services-how-to-configure.md)
[FAQ relatif aux services cloud : Bureau à distance](cloud-services-faq.md)</span><span class="sxs-lookup"><span data-stu-id="4a032-139">[How to Configure Cloud Services](cloud-services-how-to-configure.md)
[Cloud services FAQ - Remote Desktop](cloud-services-faq.md)</span></span>
