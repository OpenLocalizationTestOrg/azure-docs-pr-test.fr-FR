---
title: "aaaEnable FTP dans le Service d’applications sur la pile de Azure | Documents Microsoft"
description: "Étapes toocomplete tooenable FTP dans le Service d’applications sur la pile de Azure"
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
ms.openlocfilehash: 9c02da6362085fdd9f8d285da04efe85cf352398
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-ftp-in-app-service-on-azure-stack"></a><span data-ttu-id="2ace7-103">Activer FTP dans App Service sur Azure Stack</span><span class="sxs-lookup"><span data-stu-id="2ace7-103">Enable FTP in App Service on Azure Stack</span></span>

<span data-ttu-id="2ace7-104">Une fois que vous avez correctement déployé sur Azure pile du Service d’applications si vous souhaitez que la publication tooenable FTP, afin que vos clients peuvent télécharger leurs fichiers d’application et le contenu, il existe quelques étapes supplémentaires qui doivent toobe s’est terminée.</span><span class="sxs-lookup"><span data-stu-id="2ace7-104">Once you have successfully deployed App Service on Azure Stack if you wish tooenable FTP publishing, so that your tenants can upload their application files and content, there are some additional steps that need toobe completed.</span></span>  <span data-ttu-id="2ace7-105">Ces étapes seront automatisées dans les prochaines versions.</span><span class="sxs-lookup"><span data-stu-id="2ace7-105">In future releases these steps will be automated.</span></span>

> [!NOTE]
> <span data-ttu-id="2ace7-106">Ces étapes sont destinées aux administrateurs Service ou Entreprise qui souhaitent configurer un fournisseur de ressources App Service ou Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="2ace7-106">These steps are for Service or Enterprise Administrators configuring an App Service on Azure Stack Resource Provider.</span></span>

## <a name="enable-ftp"></a><span data-ttu-id="2ace7-107">Activer FTP</span><span class="sxs-lookup"><span data-stu-id="2ace7-107">Enable FTP</span></span>

1.  <span data-ttu-id="2ace7-108">Ouvrez une session en tant qu’administrateur de service hello dans le portail d’Azure pile toohello.</span><span class="sxs-lookup"><span data-stu-id="2ace7-108">Log in toohello Azure Stack portal as hello service administrator.</span></span>
2.  <span data-ttu-id="2ace7-109">Parcourir trop**interfaces réseau** et sélectionnez hello **FTP-NIC** sous **groupe de ressources** - **AppService LOCAL**.</span><span class="sxs-lookup"><span data-stu-id="2ace7-109">Browse too**Network interfaces** and select hello **FTP-NIC** under **Resource Group** - **AppService-LOCAL**.</span></span> <span data-ttu-id="2ace7-110">![Interfaces réseau Azure Stack][1]</span><span class="sxs-lookup"><span data-stu-id="2ace7-110">![Azure Stack Network Interfaces][1]</span></span>
3.  <span data-ttu-id="2ace7-111">Hello de note **adresse IP publique** Hello **FTP-NIC**.</span><span class="sxs-lookup"><span data-stu-id="2ace7-111">Note hello **Public IP Address** of hello **FTP-NIC**.</span></span> 
<span data-ttu-id="2ace7-112">![Détails de l’interface réseau Azure Stack][2]</span><span class="sxs-lookup"><span data-stu-id="2ace7-112">![Azure Stack Network Interface Details][2]</span></span>
4.  <span data-ttu-id="2ace7-113">Ensuite parcourir trop**virtuels** et sélectionnez hello **FTP0-VM**.</span><span class="sxs-lookup"><span data-stu-id="2ace7-113">Next Browse too**Virtual Machines** and select hello **FTP0-VM**.</span></span> <span data-ttu-id="2ace7-114">![Machines virtuelles Azure Stack][3]</span><span class="sxs-lookup"><span data-stu-id="2ace7-114">![Azure Stack Virtual Machines][3]</span></span>
5.  <span data-ttu-id="2ace7-115">Ouvrez une session Bureau à distance de toohello machine virtuelle à l’aide de hello **Connect** bouton et connexion session toohello à l’aide des informations d’identification de l’administrateur hello vous définissez au cours du déploiement du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="2ace7-115">Open a remote desktop session toohello VM using hello **Connect** button and login toohello session using hello Administrator credentials you set during App Service deployment.</span></span>  
<span data-ttu-id="2ace7-116">![Détails des machines virtuelles Azure Stack][4]</span><span class="sxs-lookup"><span data-stu-id="2ace7-116">![Azure Stack Virtual Machine Details][4]</span></span>
6.  <span data-ttu-id="2ace7-117">Ouvrez **Internet Information Services (IIS) Manager** sur hello FTP machine virtuelle (VM-FTP0).</span><span class="sxs-lookup"><span data-stu-id="2ace7-117">Open **Internet Information Service (IIS) Manager** on hello FTP VM (FTP0-VM).</span></span>
7.  <span data-ttu-id="2ace7-118">Sous **Sites**, sélectionnez **Hosting FTP Site** (Site d’hébergement FTP).</span><span class="sxs-lookup"><span data-stu-id="2ace7-118">Under **Sites** select **Hosting FTP Site**.</span></span>
8.  <span data-ttu-id="2ace7-119">Ouvrez **Prise en charge du pare-feu FTP**.</span><span class="sxs-lookup"><span data-stu-id="2ace7-119">Open **FTP Firewall Support**.</span></span> <span data-ttu-id="2ace7-120">![Gestionnaire des services IIS sur App Service FTP0-VM][5]</span><span class="sxs-lookup"><span data-stu-id="2ace7-120">![IIS Manager on App Service FTP0-VM][5]</span></span>
9.  <span data-ttu-id="2ace7-121">Entrez hello adresse IP publique de hello FTP-NIC et cliquez sur **appliquer** ![prise en charge du pare-feu FTP IIS Manager][6]</span><span class="sxs-lookup"><span data-stu-id="2ace7-121">Enter hello Public IP Address of hello FTP-NIC and click **Apply** ![IIS Manager FTP Firewall Support][6]</span></span>

## <a name="validate-hello-enabling-of-ftp"></a><span data-ttu-id="2ace7-122">Valider l’activation de hello du serveur FTP</span><span class="sxs-lookup"><span data-stu-id="2ace7-122">Validate hello enabling of FTP</span></span>

1.  <span data-ttu-id="2ace7-123">Ouvrez une session dans toohello portail de la pile d’Azure sous la forme d’un administrateur de service hello ou un client.</span><span class="sxs-lookup"><span data-stu-id="2ace7-123">Log in toohello Azure Stack portal as either hello service administrator or as a tenant.</span></span>
2.  <span data-ttu-id="2ace7-124">Parcourir trop**des Services d’application** et sélectionnez un Web, mobiles ou application API que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="2ace7-124">Browse too**App Services** and select a Web, Mobile, or API App you have created.</span></span> <span data-ttu-id="2ace7-125">![Services d’application][7]</span><span class="sxs-lookup"><span data-stu-id="2ace7-125">![App Services][7]</span></span>
3.  <span data-ttu-id="2ace7-126">Dans l’application hello détails Notez hello **nom d’hôte FTP** et **nom d’utilisateur FTP/déploiement**.</span><span class="sxs-lookup"><span data-stu-id="2ace7-126">In hello application details note hello **FTP Hostname** and **FTP/deployment username**.</span></span> <span data-ttu-id="2ace7-127">![Détails de l’application App Service][8]</span><span class="sxs-lookup"><span data-stu-id="2ace7-127">![App Service App Details][8]</span></span>
> [!NOTE]
> <span data-ttu-id="2ace7-128">Si vous ne voyez pas une entrée sous **nom d’utilisateur FTP/déploiement**, vous avez besoin d’informations d’identification du déploiement tooset hello à l’aide de première hello **informations d’identification de déploiement** panneau.</span><span class="sxs-lookup"><span data-stu-id="2ace7-128">If you do not see an entry under **FTP/deployment username**, you need tooset hello Deployment credentials first using hello **Deployment Credentials** Blade.</span></span>

4.  <span data-ttu-id="2ace7-129">Ouvrez l’Explorateur Windows, entrez des nom d’hôte hello FTP dans la barre ftp://ftp.appservice.azurestack.local, par exemple, d’adresses fichier hello</span><span class="sxs-lookup"><span data-stu-id="2ace7-129">Open Windows Explorer, enter hello FTP hostname into hello file address bar for example, ftp://ftp.appservice.azurestack.local</span></span>
5.  <span data-ttu-id="2ace7-130">Lorsque vous y êtes invité entrez hello **informations d’identification de déploiement** vous avez noté à l’étape 3, si la fonctionnalité de hello a été activée vous verrez une liste de répertoires de contenu de l’application de service application hello.</span><span class="sxs-lookup"><span data-stu-id="2ace7-130">When prompted enter hello **Deployment credentials** you noted in step 3, if hello feature has been enabled you will see a directory listing of hello app service application's contents.</span></span> <span data-ttu-id="2ace7-131">![Liste de fichiers FTP][9]</span><span class="sxs-lookup"><span data-stu-id="2ace7-131">![FTP File Listing][9]</span></span>
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
