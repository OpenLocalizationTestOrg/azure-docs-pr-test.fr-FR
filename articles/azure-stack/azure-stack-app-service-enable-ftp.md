---
title: Activer FTP dans App Service sur Azure Stack | Microsoft Docs
description: "Étapes à effectuer pour activer FTP dans App Service sur Azure Stack"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: anwestg
ms.openlocfilehash: bab69a9ff7e101f22713ba7f1ac2cbd0add7fdbd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-ftp-in-app-service-on-azure-stack"></a><span data-ttu-id="3c99d-103">Activer FTP dans App Service sur Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3c99d-103">Enable FTP in App Service on Azure Stack</span></span>

<span data-ttu-id="3c99d-104">Une fois que vous avez correctement déployé App Service sur Azure Stack, si vous souhaitez activer la publication FTP afin que vos clients puissent télécharger leurs fichiers d’application et leur contenu, vous devez effectuer quelques étapes supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="3c99d-104">Once you have successfully deployed App Service on Azure Stack if you wish to enable FTP publishing, so that your tenants can upload their application files and content, there are some additional steps that need to be completed.</span></span>  <span data-ttu-id="3c99d-105">Ces étapes seront automatisées dans les prochaines versions.</span><span class="sxs-lookup"><span data-stu-id="3c99d-105">In future releases these steps will be automated.</span></span>

> [!NOTE]
> <span data-ttu-id="3c99d-106">Ces étapes sont destinées aux administrateurs Service ou Entreprise qui souhaitent configurer un fournisseur de ressources App Service ou Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3c99d-106">These steps are for Service or Enterprise Administrators configuring an App Service on Azure Stack Resource Provider.</span></span>

## <a name="enable-ftp"></a><span data-ttu-id="3c99d-107">Activer FTP</span><span class="sxs-lookup"><span data-stu-id="3c99d-107">Enable FTP</span></span>

1.  <span data-ttu-id="3c99d-108">Connectez-vous au portail Azure Stack en tant qu’administrateur du service.</span><span class="sxs-lookup"><span data-stu-id="3c99d-108">Log in to the Azure Stack portal as the service administrator.</span></span>
2.  <span data-ttu-id="3c99d-109">Accédez à **Interfaces réseau** et sélectionnez **FTP-NIC** dans le **Groupe de ressources** - **AppService-LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="3c99d-109">Browse to **Network interfaces** and select the **FTP-NIC** under **Resource Group** - **AppService-LOCAL**.</span></span> <span data-ttu-id="3c99d-110">![Interfaces réseau Azure Stack][1]</span><span class="sxs-lookup"><span data-stu-id="3c99d-110">![Azure Stack Network Interfaces][1]</span></span>
3.  <span data-ttu-id="3c99d-111">Notez **l’adresse IP publique** de **FTP-NIC**.</span><span class="sxs-lookup"><span data-stu-id="3c99d-111">Note the **Public IP Address** of the **FTP-NIC**.</span></span> 
<span data-ttu-id="3c99d-112">![Détails de l’interface réseau Azure Stack][2]</span><span class="sxs-lookup"><span data-stu-id="3c99d-112">![Azure Stack Network Interface Details][2]</span></span>
4.  <span data-ttu-id="3c99d-113">Accédez ensuite à **Machines virtuelles** et sélectionnez **FTP0-VM**.</span><span class="sxs-lookup"><span data-stu-id="3c99d-113">Next Browse to **Virtual Machines** and select the **FTP0-VM**.</span></span> <span data-ttu-id="3c99d-114">![Machines virtuelles Azure Stack][3]</span><span class="sxs-lookup"><span data-stu-id="3c99d-114">![Azure Stack Virtual Machines][3]</span></span>
5.  <span data-ttu-id="3c99d-115">Ouvrez une session Bureau à distance sur la machine virtuelle à l’aide du bouton **Se connecter** et connectez-vous à la session en utilisant les informations d’identification de l’administrateur définies lors du déploiement d’App Service.</span><span class="sxs-lookup"><span data-stu-id="3c99d-115">Open a remote desktop session to the VM using the **Connect** button and login to the session using the Administrator credentials you set during App Service deployment.</span></span>  
<span data-ttu-id="3c99d-116">![Détails des machines virtuelles Azure Stack][4]</span><span class="sxs-lookup"><span data-stu-id="3c99d-116">![Azure Stack Virtual Machine Details][4]</span></span>
6.  <span data-ttu-id="3c99d-117">Ouvrez le **Gestionnaire des services IIS** sur la machine virtuelle FTP (FTP0-VM).</span><span class="sxs-lookup"><span data-stu-id="3c99d-117">Open **Internet Information Service (IIS) Manager** on the FTP VM (FTP0-VM).</span></span>
7.  <span data-ttu-id="3c99d-118">Sous **Sites**, sélectionnez **Hosting FTP Site** (Site d’hébergement FTP).</span><span class="sxs-lookup"><span data-stu-id="3c99d-118">Under **Sites** select **Hosting FTP Site**.</span></span>
8.  <span data-ttu-id="3c99d-119">Ouvrez **Prise en charge du pare-feu FTP**.</span><span class="sxs-lookup"><span data-stu-id="3c99d-119">Open **FTP Firewall Support**.</span></span> <span data-ttu-id="3c99d-120">![Gestionnaire des services IIS sur App Service FTP0-VM][5]</span><span class="sxs-lookup"><span data-stu-id="3c99d-120">![IIS Manager on App Service FTP0-VM][5]</span></span>
9.  <span data-ttu-id="3c99d-121">Entrez l’adresse IP publique de FTP-NIC et cliquez sur **Appliquer**. ![Prise en charge du pare-feu FTP dans le gestionnaire des services IIS][6].</span><span class="sxs-lookup"><span data-stu-id="3c99d-121">Enter the Public IP Address of the FTP-NIC and click **Apply** ![IIS Manager FTP Firewall Support][6]</span></span>

## <a name="validate-the-enabling-of-ftp"></a><span data-ttu-id="3c99d-122">Valider l’activation de FTP</span><span class="sxs-lookup"><span data-stu-id="3c99d-122">Validate the enabling of FTP</span></span>

1.  <span data-ttu-id="3c99d-123">Connectez-vous au portail Azure Stack en tant qu’administrateur du service ou en tant que client.</span><span class="sxs-lookup"><span data-stu-id="3c99d-123">Log in to the Azure Stack portal as either the service administrator or as a tenant.</span></span>
2.  <span data-ttu-id="3c99d-124">Accédez à **App Services** et sélectionnez un application Web, mobile ou API que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="3c99d-124">Browse to **App Services** and select a Web, Mobile, or API App you have created.</span></span> <span data-ttu-id="3c99d-125">![Services d’application][7]</span><span class="sxs-lookup"><span data-stu-id="3c99d-125">![App Services][7]</span></span>
3.  <span data-ttu-id="3c99d-126">Dans les détails de l’application, notez le **Nom d’hôte FTP** et le **Nom d’utilisateur FTP/Déploiement**.</span><span class="sxs-lookup"><span data-stu-id="3c99d-126">In the application details note the **FTP Hostname** and **FTP/deployment username**.</span></span> <span data-ttu-id="3c99d-127">![Détails de l’application App Service][8]</span><span class="sxs-lookup"><span data-stu-id="3c99d-127">![App Service App Details][8]</span></span>
> [!NOTE]
> <span data-ttu-id="3c99d-128">Si vous ne voyez pas d’entrée sous **Nom d’utilisateur FTP/Déploiement**, vous devez d’abord définir les informations d’identification de déploiement à l’aide du panneau **Informations d’identification du déploiement**.</span><span class="sxs-lookup"><span data-stu-id="3c99d-128">If you do not see an entry under **FTP/deployment username**, you need to set the Deployment credentials first using the **Deployment Credentials** Blade.</span></span>

4.  <span data-ttu-id="3c99d-129">Ouvrez l’Explorateur Windows, entrez le nom d’hôte FTP dans la barre d’adresse du fichier, par exemple, ftp://ftp.appservice.azurestack.local.</span><span class="sxs-lookup"><span data-stu-id="3c99d-129">Open Windows Explorer, enter the FTP hostname into the file address bar for example, ftp://ftp.appservice.azurestack.local</span></span>
5.  <span data-ttu-id="3c99d-130">Lorsque vous y êtes invité, entrez les **Informations d’identification du déploiement** notées à l’étape 3. Si la fonctionnalité a été activée, vous verrez une liste de répertoires comportant les contenus de l’application App Service.</span><span class="sxs-lookup"><span data-stu-id="3c99d-130">When prompted enter the **Deployment credentials** you noted in step 3, if the feature has been enabled you will see a directory listing of the app service application's contents.</span></span> <span data-ttu-id="3c99d-131">![Liste de fichiers FTP][9]</span><span class="sxs-lookup"><span data-stu-id="3c99d-131">![FTP File Listing][9]</span></span>
<!--Image references-->
[1]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interfaces.png
[2]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interface-details.png
[3]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines.png
[4]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines-FTP0-VM.png
[5]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager.png
[6]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager-FTP-Firewall-Support.png
[7]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-services.png
[8]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-service-app-detail.png
[9]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-ftp-file-listing.png
