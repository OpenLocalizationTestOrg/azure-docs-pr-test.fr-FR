---
title: "Utiliser PowerShell pour créer une machine virtuelle avec un serveur de rapports en mode natif | Microsoft Docs"
description: "Cette rubrique explique comment déployer et configurer un serveur de rapports SQL Server Reporting Services en mode natif dans une machine virtuelle Azure. "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 5e5c11251cd316e8161dbe362b300be76927ac01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-create-an-azure-vm-with-a-native-mode-report-server"></a><span data-ttu-id="80db6-103">Utiliser PowerShell pour créer une machine virtuelle Azure avec un serveur de rapports en mode natif</span><span class="sxs-lookup"><span data-stu-id="80db6-103">Use PowerShell to Create an Azure VM With a Native Mode Report Server</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="80db6-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="80db6-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="80db6-105">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="80db6-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="80db6-106">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="80db6-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="80db6-107">Cette rubrique explique comment déployer et configurer un serveur de rapports SQL Server Reporting Services en mode natif dans une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="80db6-107">This topic describes and walks you through the deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span></span> <span data-ttu-id="80db6-108">Les procédures décrites dans ce document comportent une combinaison d’étapes manuelles permettant de créer la machine virtuelle et un script Windows PowerShell afin de configurer Reporting Services sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-108">The steps in this document use a combination of manual steps to create the virtual machine and a Windows PowerShell script to configure Reporting Services on the VM.</span></span> <span data-ttu-id="80db6-109">Le script de configuration inclut l’ouverture d’un port de pare-feu pour HTTP ou HTTPs.</span><span class="sxs-lookup"><span data-stu-id="80db6-109">The configuration script includes opening a firewall port for HTTP or HTTPs.</span></span>

> [!NOTE]
> <span data-ttu-id="80db6-110">Si vous n’avez pas besoin de **HTTPS** sur le serveur de rapports, **ignorez l’étape 2**.</span><span class="sxs-lookup"><span data-stu-id="80db6-110">If you do not require **HTTPS** on the report server, **skip step 2**.</span></span>
> 
> <span data-ttu-id="80db6-111">Après avoir créé la machine virtuelle à l’étape 1, passez à la section Utiliser un script pour configurer le serveur de rapports et HTTP.</span><span class="sxs-lookup"><span data-stu-id="80db6-111">After creating the VM in step 1, go to the section Use script to configure the report server and HTTP.</span></span> <span data-ttu-id="80db6-112">Le serveur de rapports est prêt à l’emploi après l’exécution du script.</span><span class="sxs-lookup"><span data-stu-id="80db6-112">After you run the script, the report server is ready to use.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="80db6-113">Configuration requise et hypothèses</span><span class="sxs-lookup"><span data-stu-id="80db6-113">Prerequisites and Assumptions</span></span>
* <span data-ttu-id="80db6-114">**Abonnement Azure**: vérifiez le nombre de mémoires à tores magnétiques disponibles dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="80db6-114">**Azure Subscription**: Verify the number of cores available in your Azure Subscription.</span></span> <span data-ttu-id="80db6-115">Si vous créez une machine virtuelle de la taille recommandée **A3**, vous devez disposer de **4** mémoires à tores magnétiques.</span><span class="sxs-lookup"><span data-stu-id="80db6-115">If you create the recommended VM size of **A3**, you need **4** available cores.</span></span> <span data-ttu-id="80db6-116">Si vous utilisez une machine virtuelle de taille **A2**, vous devez disposer de **2** mémoires à tores magnétiques.</span><span class="sxs-lookup"><span data-stu-id="80db6-116">If you use a VM size of **A2**, you need **2** available cores.</span></span>
  
  * <span data-ttu-id="80db6-117">Pour vérifier la limite de mémoires à tores magnétiques de votre abonnement, dans le portail Azure Classic, cliquez sur PARAMÈTRES dans le volet de gauche, puis sur UTILISATION dans le menu supérieur.</span><span class="sxs-lookup"><span data-stu-id="80db6-117">To verify the core limit of your subscription, in the Azure classic portal, click SETTINGS in the left pane and then Click USAGE in the top menu.</span></span>
  * <span data-ttu-id="80db6-118">Pour augmenter le quota de mémoires à tores magnétiques, contactez le [support technique Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="80db6-118">To increase the core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span></span> <span data-ttu-id="80db6-119">Pour plus d’informations sur les tailles de machines virtuelles, consultez la page [Tailles de machines virtuelles pour Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="80db6-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="80db6-120">**Écriture de scripts avec Windows PowerShell**: la rubrique part du principe que vous avez une connaissance de base de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="80db6-120">**Windows PowerShell Scripting**: The topic assumes that you have a basic working knowledge of Windows PowerShell.</span></span> <span data-ttu-id="80db6-121">Pour plus d’informations sur l’utilisation de Windows PowerShell, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="80db6-121">For more information about using Windows PowerShell, see the following:</span></span>
  
  * [<span data-ttu-id="80db6-122">Démarrage de Windows PowerShell sur Windows Server</span><span class="sxs-lookup"><span data-stu-id="80db6-122">Starting Windows PowerShell on Windows Server</span></span>](https://technet.microsoft.com/library/hh847814.aspx)
  * [<span data-ttu-id="80db6-123">Prise en main de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="80db6-123">Getting Started with Windows PowerShell</span></span>](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a><span data-ttu-id="80db6-124">Étape 1 : Approvisionner une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="80db6-124">Step 1: Provision an Azure Virtual Machine</span></span>
1. <span data-ttu-id="80db6-125">Connectez-vous au portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="80db6-125">Browse to the Azure classic portal.</span></span>
2. <span data-ttu-id="80db6-126">Cliquez sur **Machines virtuelles** dans le volet de gauche.</span><span class="sxs-lookup"><span data-stu-id="80db6-126">Click **Virtual Machines** in the left pane.</span></span>
   
    ![microsoft azure virtual machines](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. <span data-ttu-id="80db6-128">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="80db6-128">Click **New**.</span></span>
   
    ![bouton nouveau](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. <span data-ttu-id="80db6-130">Cliquez sur **À partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="80db6-130">Click **From Gallery**.</span></span>
   
    ![nouvelle machine virtuelle à partir de la galerie](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. <span data-ttu-id="80db6-132">Cliquez sur **SQL Server 2014 RTM Standard – Windows Server 2012 R2** , puis sur la flèche pour continuer.</span><span class="sxs-lookup"><span data-stu-id="80db6-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click the arrow to continue.</span></span>
   
    ![Suivant](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    <span data-ttu-id="80db6-134">Si vous avez besoin de la fonctionnalité d’abonnements pilotés par les données de Reporting Services, choisissez **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span><span class="sxs-lookup"><span data-stu-id="80db6-134">If you need the Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span></span> <span data-ttu-id="80db6-135">Pour plus d’informations sur les éditions de SQL Server et les fonctionnalités prises en charge, consultez la page [Fonctionnalités prises en charge par les éditions de SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span><span class="sxs-lookup"><span data-stu-id="80db6-135">For more information on SQL Server editions and feature support, see [Features Supported by the Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span></span>
6. <span data-ttu-id="80db6-136">Sur la page **Configuration de la machine virtuelle** , renseignez les champs suivants comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="80db6-136">On the **Virtual machine configuration** page, edit the following fields:</span></span>
   
   * <span data-ttu-id="80db6-137">S’il existe plusieurs **DATES DE SORTIE DE LA VERSION**, sélectionnez la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="80db6-137">If there is more than one **VERSION RELEASE DATE**, select the most recent version.</span></span>
   * <span data-ttu-id="80db6-138">**Nom de la machine virtuelle**: le nom de la machine est également utilisé sur la page de configuration suivante comme nom DNS par défaut du service cloud.</span><span class="sxs-lookup"><span data-stu-id="80db6-138">**Virtual Machine Name**: The machine name is also used on the next configuration page as the default Cloud Service DNS name.</span></span> <span data-ttu-id="80db6-139">Le nom DNS doit être unique dans le service Azure.</span><span class="sxs-lookup"><span data-stu-id="80db6-139">The DNS name must be unique across the Azure service.</span></span> <span data-ttu-id="80db6-140">Envisagez de configurer la machine virtuelle avec un nom qui décrit à quoi elle sert.</span><span class="sxs-lookup"><span data-stu-id="80db6-140">Consider configuring the VM with a computer name that describes what the VM is used for.</span></span> <span data-ttu-id="80db6-141">Par exemple, ssrsnativecloud.</span><span class="sxs-lookup"><span data-stu-id="80db6-141">For example ssrsnativecloud.</span></span>
   * <span data-ttu-id="80db6-142">**Niveau**: Standard</span><span class="sxs-lookup"><span data-stu-id="80db6-142">**Tier**: Standard</span></span>
   * <span data-ttu-id="80db6-143">**Taille : A3** est la taille de machine virtuelle recommandée pour les charges de travail SQL Server.</span><span class="sxs-lookup"><span data-stu-id="80db6-143">**Size:A3** is the recommended VM size for SQL Server workloads.</span></span> <span data-ttu-id="80db6-144">Si une machine virtuelle est utilisée uniquement comme serveur de rapports, la taille A2 est suffisante, sauf si la charge de travail du serveur est importante.</span><span class="sxs-lookup"><span data-stu-id="80db6-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless the report server experiences a large workload.</span></span> <span data-ttu-id="80db6-145">Pour connaître les informations de tarification des machines virtuelles, consultez la page [Tarification des machines virtuelles](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="80db6-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
   * <span data-ttu-id="80db6-146">**Nouveau nom d’utilisateur**: le nom que vous fournissez est créé en tant qu’administrateur sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-146">**New User Name**: the name you provide is created as an administrator on the VM.</span></span>
   * <span data-ttu-id="80db6-147">**Nouveau mot de passe** et **confirmation**.</span><span class="sxs-lookup"><span data-stu-id="80db6-147">**New Password** and **confirm**.</span></span> <span data-ttu-id="80db6-148">Ce mot de passe est utilisé pour le nouveau compte Administrateur. Il est recommandé d’utiliser un mot de passe fort.</span><span class="sxs-lookup"><span data-stu-id="80db6-148">This password is used for the new administrator account and it is recommended you use a strong password.</span></span>
   * <span data-ttu-id="80db6-149">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="80db6-149">Click **Next**.</span></span> <span data-ttu-id="80db6-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span><span class="sxs-lookup"><span data-stu-id="80db6-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span></span>
7. <span data-ttu-id="80db6-151">Sur la page suivante, renseignez les champs suivants comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="80db6-151">On the next page, edit the following fields:</span></span>
   
   * <span data-ttu-id="80db6-152">**Service cloud** : sélectionnez **Créer un service cloud**.</span><span class="sxs-lookup"><span data-stu-id="80db6-152">**Cloud Service**: select **Create a new Cloud Service**.</span></span>
   * <span data-ttu-id="80db6-153">**Nom DNS du service cloud**: il s’agit du nom DNS public du service cloud associé à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-153">**Cloud Service DNS Name**: This is the public DNS name of the Cloud Service that is associated with the VM.</span></span> <span data-ttu-id="80db6-154">Le nom par défaut est le nom que vous avez saisi comme nom de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-154">The default name is the name you typed in for the VM name.</span></span> <span data-ttu-id="80db6-155">Si, dans les étapes ultérieures de la rubrique, vous créez un certificat SSL approuvé, le nom DNS est utilisé pour la valeur «**Issued to**» du certificat.</span><span class="sxs-lookup"><span data-stu-id="80db6-155">If in later steps of the topic, you create a trusted SSL certificate and then the DNS name is used for the value of the “**Issued to**” of the certificate.</span></span>
   * <span data-ttu-id="80db6-156">**Région/Groupe d’affinités/Réseau virtuel**: sélectionnez la région la plus proche de vos utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="80db6-156">**Region/Affinity Group/Virtual Network**: Choose the region closest to your end users.</span></span>
   * <span data-ttu-id="80db6-157">**Compte de stockage**: utilisez un compte de stockage généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="80db6-157">**Storage Account**: Use an automatically generated storage account.</span></span>
   * <span data-ttu-id="80db6-158">**Groupe à haute disponibilité**: Aucun.</span><span class="sxs-lookup"><span data-stu-id="80db6-158">**Availability Set**: None.</span></span>
   * <span data-ttu-id="80db6-159">**POINTS DE TERMINAISON** Conservez les points de terminaison **Bureau à distance** et **PowerShell**, puis ajoutez un point de terminaison HTTP ou HTTPS, selon votre environnement.</span><span class="sxs-lookup"><span data-stu-id="80db6-159">**ENDPOINTS** Keep the **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span></span>
     
     * <span data-ttu-id="80db6-160">**HTTP** : les ports public et privé par défaut ont le numéro **80**.</span><span class="sxs-lookup"><span data-stu-id="80db6-160">**HTTP**: The default public and private ports are **80**.</span></span> <span data-ttu-id="80db6-161">Notez que si vous utilisez un port privé autre que 80, vous devez modifier **$HTTPport = 80** dans le script HTTP.</span><span class="sxs-lookup"><span data-stu-id="80db6-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in the http script.</span></span>
     * <span data-ttu-id="80db6-162">**HTTPS** : les ports public et privé par défaut sont **443**.</span><span class="sxs-lookup"><span data-stu-id="80db6-162">**HTTPS**: The default public and private ports are **443**.</span></span> <span data-ttu-id="80db6-163">Il est considéré comme meilleure pratique de sécurité de modifier le port privé et de configurer le pare-feu et le serveur de rapports pour qu’ils utilisent le port privé.</span><span class="sxs-lookup"><span data-stu-id="80db6-163">A security best practice is to change the private port and configure your firewall and the report server to use the private port.</span></span> <span data-ttu-id="80db6-164">Pour plus d’informations sur les points de terminaison, consultez la page [Comment configurer des points de terminaison sur une machine virtuelle](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="80db6-164">For more information on endpoints, see [How to Set Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="80db6-165">Notez que si vous utilisez un port autre que 443, vous devez modifier le paramètre **$HTTPsport = 443** dans le script HTTPS.</span><span class="sxs-lookup"><span data-stu-id="80db6-165">Note that if you use a port other than 443, change the parameter **$HTTPsport = 443** in the HTTPS script.</span></span>
   * <span data-ttu-id="80db6-166">Cliquez sur suivant.</span><span class="sxs-lookup"><span data-stu-id="80db6-166">Click next .</span></span> ![Suivant](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. <span data-ttu-id="80db6-168">Sur la dernière page de l’Assistant, conservez la valeur par défaut **Installer l’agent de machine virtuelle** sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="80db6-168">On the last page of the wizard, keep the default **Install the VM agent** selected.</span></span> <span data-ttu-id="80db6-169">Les étapes décrites dans cette rubrique n’utilisent pas l’agent de machine virtuelle, mais si vous envisagez de conserver cette machine virtuelle, l’agent de machine virtuelle et les extensions vous permettront d’améliorer la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-169">The steps in this topic do not utilize the VM agent but if you plan to keep this VM, the VM agent and extensions will allow you to enhance he CM.</span></span>  <span data-ttu-id="80db6-170">Pour plus d’informations, consultez le billet de blog [Agent de machine virtuelle et extensions – 1re partie](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span><span class="sxs-lookup"><span data-stu-id="80db6-170">For more information on the VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span></span> <span data-ttu-id="80db6-171">L’une des extensions par défaut installées et exécutées est l’extension « BGINFO », qui affiche sur le bureau de la machine virtuelle les informations système telles que l’adresse IP interne et l’espace libre sur le disque.</span><span class="sxs-lookup"><span data-stu-id="80db6-171">One of the default extensions installed ad running is the “BGINFO” extension that displays on the VM desktop, system information such as internal IP and free drive space.</span></span>
9. <span data-ttu-id="80db6-172">Cliquez Terminé .</span><span class="sxs-lookup"><span data-stu-id="80db6-172">Click complete .</span></span> ![OK](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. <span data-ttu-id="80db6-174">L’**État** de la machine virtuelle affiché indique **Démarrage (Approvisionnement)** pendant le processus d’approvisionnement, puis **En cours d’exécution** une fois que la machine virtuelle a été approvisionnée et qu’elle est prête à l’emploi.</span><span class="sxs-lookup"><span data-stu-id="80db6-174">The **Status** of the VM displays as **Starting (Provisioning)** during the provision process and then displays as **Running** when the VM is provisioned and ready to use.</span></span>

## <a name="step-2-create-a-server-certificate"></a><span data-ttu-id="80db6-175">Étape 2 : Créer un certificat de serveur</span><span class="sxs-lookup"><span data-stu-id="80db6-175">Step 2: Create a Server Certificate</span></span>
> [!NOTE]
> <span data-ttu-id="80db6-176">Si vous n’avez pas besoin de HTTPS sur le serveur de rapports, vous pouvez **ignorer l’étape 2** et accéder à la section **Utiliser un script pour configurer le serveur de rapports et HTTP**.</span><span class="sxs-lookup"><span data-stu-id="80db6-176">If you do not require HTTPS on the report server, you can **skip step 2** and go to the section **Use script to configure the report server and HTTP**.</span></span> <span data-ttu-id="80db6-177">Utilisez le script HTTP pour configurer rapidement le serveur de rapports afin qu’il soit prêt à l’emploi.</span><span class="sxs-lookup"><span data-stu-id="80db6-177">Use the HTTP script to quickly configure the report server and the report server will be ready to use.</span></span>

<span data-ttu-id="80db6-178">Pour utiliser HTTPS sur la machine virtuelle, vous devez disposer d’un certificat SSL approuvé.</span><span class="sxs-lookup"><span data-stu-id="80db6-178">In order to use HTTPS on the VM, you need a trusted SSL certificate.</span></span> <span data-ttu-id="80db6-179">Selon votre scénario, vous pouvez utiliser l’une des deux méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="80db6-179">Depending on your scenario, you can use one of the following two methods:</span></span>

* <span data-ttu-id="80db6-180">Un certificat SSL valide émis par une autorité de certification et approuvé par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="80db6-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span></span> <span data-ttu-id="80db6-181">Les certificats racines de l’autorité de certification doivent être distribués via le programme de certificat racine Microsoft.</span><span class="sxs-lookup"><span data-stu-id="80db6-181">The CA root certificates are required to be distributed via the Microsoft Root Certificate Program.</span></span> <span data-ttu-id="80db6-182">Pour plus d’informations sur ce programme, consultez les pages [Programme de certificat racine SSL Windows et Windows Phone 8 (autorités de certification membres)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) et [Introduction au programme de certificat racine Microsoft](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span><span class="sxs-lookup"><span data-stu-id="80db6-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction to The Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span></span>
* <span data-ttu-id="80db6-183">Un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="80db6-183">A self-signed certificate.</span></span> <span data-ttu-id="80db6-184">Les certificats auto-signés sont déconseillés pour les environnements de production.</span><span class="sxs-lookup"><span data-stu-id="80db6-184">Self-signed certificates are not recommended for production environments.</span></span>

### <a name="to-use-a-certificate-created-by-a-trusted-certificate-authority-ca"></a><span data-ttu-id="80db6-185">Pour utiliser un certificat créé par une autorité de certification approuvée</span><span class="sxs-lookup"><span data-stu-id="80db6-185">To use a certificate created by a trusted Certificate Authority (CA)</span></span>
1. <span data-ttu-id="80db6-186">**Demandez un certificat de serveur pour le site web auprès d’une autorité de certification**.</span><span class="sxs-lookup"><span data-stu-id="80db6-186">**Request a server certificate for the website from a certification authority**.</span></span> 
   
    <span data-ttu-id="80db6-187">Vous pouvez utiliser l’Assistant Certificat de serveur Web pour générer un fichier de demande de certificat (Certreq.txt) à envoyer à une autorité de certification ou générer une demande destinée à une autorité de certification en ligne.</span><span class="sxs-lookup"><span data-stu-id="80db6-187">You can use the Web Server Certificate Wizard either to generate a certificate request file (Certreq.txt) that you send to a certification authority, or to generate a request for an online certification authority.</span></span> <span data-ttu-id="80db6-188">Par exemple, les services de certificats Microsoft dans Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="80db6-188">For example, Microsoft Certificate Services in Windows Server 2012.</span></span> <span data-ttu-id="80db6-189">Selon le niveau d’assurance offert par votre certificat de serveur en termes d’identification, l’autorité de certification peut prendre plusieurs jours à plusieurs mois pour approuver votre demande et vous envoyer un fichier de certificat.</span><span class="sxs-lookup"><span data-stu-id="80db6-189">Depending on the level of identification assurance offered by your server certificate, it is several days to several months for the certification authority to approve your request and send you a certificate file.</span></span> 
   
    <span data-ttu-id="80db6-190">Pour plus d’informations sur la demande d’un certificat de serveur, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="80db6-190">For more information about requesting a server certificates, see the following:</span></span> 
   
   * <span data-ttu-id="80db6-191">Utiliser [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span><span class="sxs-lookup"><span data-stu-id="80db6-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span></span>
   * <span data-ttu-id="80db6-192">Outils de sécurité pour administrer Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="80db6-192">Security Tools to Administer Windows Server 2012.</span></span>
     
     [<span data-ttu-id="80db6-193">Outils de sécurité pour administrer Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="80db6-193">Security Tools to Administer Windows Server 2012</span></span>](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > <span data-ttu-id="80db6-194">Le champ **Délivré à** du certificat SSL approuvé doit être le même que le **NOM DNS du service cloud** utilisé pour la nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-194">The **issued to** field of the trusted SSL certificate should be the same as the **Cloud Service DNS NAME** you used for the new VM.</span></span>

2. <span data-ttu-id="80db6-195">**Installez le certificat de serveur sur le serveur web**.</span><span class="sxs-lookup"><span data-stu-id="80db6-195">**Install the server certificate on the Web server**.</span></span> <span data-ttu-id="80db6-196">Dans ce cas, le serveur web est la machine virtuelle qui héberge le serveur de rapports, et le site web est créé ultérieurement lors de la configuration de Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="80db6-196">The Web server in this case is the VM that hosts the report server and the website is created in later steps when you configure Reporting Services.</span></span> <span data-ttu-id="80db6-197">Pour plus d’informations sur l’installation du certificat de serveur sur le serveur web à l’aide du composant logiciel enfichable MMC Certificat, consultez la page [Installer un certificat de serveur](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="80db6-197">For more information about installing the server certificate on the Web server by using the Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
    <span data-ttu-id="80db6-198">Si vous souhaitez utiliser le script fourni dans cette rubrique pour configurer le serveur de rapports, la valeur **Empreinte numérique** des certificats est requise comme paramètre du script.</span><span class="sxs-lookup"><span data-stu-id="80db6-198">If you want to use the script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span></span> <span data-ttu-id="80db6-199">Consultez la section suivante pour plus d’informations sur la façon d’obtenir l’empreinte numérique du certificat.</span><span class="sxs-lookup"><span data-stu-id="80db6-199">See the next section for details on how to obtain the thumbprint of the certificate.</span></span>
3. <span data-ttu-id="80db6-200">Attribuez le certificat de serveur au serveur de rapports.</span><span class="sxs-lookup"><span data-stu-id="80db6-200">Assign the server certificate to the report server.</span></span> <span data-ttu-id="80db6-201">L’attribution s’effectue dans la section suivante, lors de la configuration du serveur de rapports.</span><span class="sxs-lookup"><span data-stu-id="80db6-201">The assignment is completed in the next section when you configure the report server.</span></span>

### <a name="to-use-the-virtual-machines-self-signed-certificate"></a><span data-ttu-id="80db6-202">Pour utiliser le certificat auto-signé Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="80db6-202">To use the Virtual Machines Self-signed Certificate</span></span>
<span data-ttu-id="80db6-203">Un certificat auto-signé a été créé sur la machine virtuelle lors de son approvisionnement.</span><span class="sxs-lookup"><span data-stu-id="80db6-203">A self-signed certificate was created on the VM when the VM was provisioned.</span></span> <span data-ttu-id="80db6-204">Le nom du certificat est le même que le nom DNS de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-204">The certificate has the same name as the VM DNS name.</span></span> <span data-ttu-id="80db6-205">Pour éviter les erreurs de certificat, il est nécessaire que le certificat soit approuvé sur la machine virtuelle elle-même et aussi par tous les utilisateurs du site.</span><span class="sxs-lookup"><span data-stu-id="80db6-205">In order to avoid certificate errors, it is required that the certificate is trusted on the VM itself, and also by all users of the site.</span></span>

1. <span data-ttu-id="80db6-206">Pour approuver l’autorité de certification racine du certificat sur la machine virtuelle locale, ajoutez le certificat aux **Autorités de certification racines de confiance**.</span><span class="sxs-lookup"><span data-stu-id="80db6-206">To trust the root CA of the certificate on the Local VM, add the certificate to the **Trusted Root Certification Authorities**.</span></span> <span data-ttu-id="80db6-207">Les instructions suivantes sont un résumé de la procédure requise.</span><span class="sxs-lookup"><span data-stu-id="80db6-207">The following is a summary of the steps required.</span></span> <span data-ttu-id="80db6-208">Pour obtenir la procédure détaillée d’approbation de l’autorité de certification, consultez la page [Installer un certificat de serveur](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="80db6-208">For detailed steps on how to trust the CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
   1. <span data-ttu-id="80db6-209">Dans le portail Azure Classic, sélectionnez la machine virtuelle, puis cliquez sur Connecter.</span><span class="sxs-lookup"><span data-stu-id="80db6-209">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="80db6-210">Selon la configuration de votre navigateur, vous pouvez être invité à enregistrer un fichier .rdp pour la connexion à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-210">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
      
       ![se connecter à une machine virtuelle azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="80db6-212">Utilisez le nom de machine virtuelle, le nom d’utilisateur et le mot de passe que vous avez configurés lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-212">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
      
       <span data-ttu-id="80db6-213">Par exemple, dans l’illustration suivante, le nom de la machine virtuelle est **ssrsnativecloud** et le nom d’utilisateur **testuser**.</span><span class="sxs-lookup"><span data-stu-id="80db6-213">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
      
       ![le nom de connexion inclut le nom de la machine virtuelle](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. <span data-ttu-id="80db6-215">Exécutez mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="80db6-215">Run mmc.exe.</span></span> <span data-ttu-id="80db6-216">Pour plus d’informations, consultez la page [Affichage de certificats à l’aide du composant logiciel enfichable MMC](https://msdn.microsoft.com/library/ms788967.aspx).</span><span class="sxs-lookup"><span data-stu-id="80db6-216">For more information, see [How to: View Certificates with the MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span></span>
   3. <span data-ttu-id="80db6-217">Dans le menu **Fichier** de l’application console, ajoutez le composant logiciel enfichable **Certificats**, sélectionnez **Compte d’ordinateur** lorsque vous y êtes invité, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="80db6-217">In the console application **File** menu, add the **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span></span>
   4. <span data-ttu-id="80db6-218">Sélectionnez l’**Ordinateur local** à gérer, puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="80db6-218">Select **Local Computer** to manage and then click **Finish**.</span></span>
   5. <span data-ttu-id="80db6-219">Cliquez sur **OK**, développez les nœuds **Certificats - Personnel**, puis cliquez sur **Certificats**.</span><span class="sxs-lookup"><span data-stu-id="80db6-219">Click **Ok** and then expand the **Certificates -Personal** nodes and then click **Certificates**.</span></span> <span data-ttu-id="80db6-220">Le certificat est nommé d’après le nom DNS de la machine virtuelle et se termine par **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="80db6-220">The certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span></span> <span data-ttu-id="80db6-221">Cliquez avec le bouton droit sur le nom du certificat, puis cliquez sur **Copier**.</span><span class="sxs-lookup"><span data-stu-id="80db6-221">Right-click the certificate name and click **Copy**.</span></span>
   6. <span data-ttu-id="80db6-222">Développez le nœud **Autorités de certification racines de confiance**, puis cliquez avec le bouton droit sur **Certificats** et cliquez sur **Coller**.</span><span class="sxs-lookup"><span data-stu-id="80db6-222">Expand the **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span></span>
   7. <span data-ttu-id="80db6-223">Pour valider, double-cliquez sur le nom du certificat sous **Autorités de certification racines de confiance** et vérifiez qu’il n’y a aucune erreur et que votre certificat est présent.</span><span class="sxs-lookup"><span data-stu-id="80db6-223">To validate, double click on the certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span></span> <span data-ttu-id="80db6-224">Si vous souhaitez utiliser le script HTTPS fourni dans cette rubrique pour configurer le serveur de rapports, la valeur **Empreinte numérique** des certificats est requise comme paramètre du script.</span><span class="sxs-lookup"><span data-stu-id="80db6-224">If you want to use the HTTPS script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span></span> <span data-ttu-id="80db6-225">**Pour obtenir la valeur d’empreinte numérique**, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="80db6-225">**To get the thumbprint value**, complete the following.</span></span> <span data-ttu-id="80db6-226">La section [Utiliser un script pour configurer le serveur de rapports et HTTPS](#use-script-to-configure-the-report-server-and-HTTPS)comprend un exemple PowerShell permettant de récupérer l’empreinte numérique.</span><span class="sxs-lookup"><span data-stu-id="80db6-226">There is also a PowerShell sample to retrieve the thumbprint in section [Use script to configure the report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span></span>
      
      1. <span data-ttu-id="80db6-227">Double-cliquez sur le nom du certificat, par exemple ssrsnativecloud.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="80db6-227">Double-click the name of the certificate, for example ssrsnativecloud.cloudapp.net.</span></span>
      2. <span data-ttu-id="80db6-228">Cliquez sur l’onglet **Détails** .</span><span class="sxs-lookup"><span data-stu-id="80db6-228">Click the **Details** tab.</span></span>
      3. <span data-ttu-id="80db6-229">Cliquez sur **Empreinte numérique**.</span><span class="sxs-lookup"><span data-stu-id="80db6-229">Click **Thumbprint**.</span></span> <span data-ttu-id="80db6-230">La valeur de l’empreinte numérique s’affiche dans le champ de détails, par exemple a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span><span class="sxs-lookup"><span data-stu-id="80db6-230">The value of the thumbprint is displayed in the details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span></span>
      4. <span data-ttu-id="80db6-231">Copiez l’empreinte numérique et enregistrez la valeur pour l’utiliser ultérieurement ou modifiez le script maintenant.</span><span class="sxs-lookup"><span data-stu-id="80db6-231">Copy the thumbprint and save the value for later or edit the script now.</span></span>
      5. <span data-ttu-id="80db6-232">(*) Avant d’exécuter le script, supprimez les espaces entre les paires de valeurs.</span><span class="sxs-lookup"><span data-stu-id="80db6-232">(*) Before you run the script, remove the spaces in between the pairs of values.</span></span> <span data-ttu-id="80db6-233">Par exemple, l’empreinte numérique susmentionnée devient ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span><span class="sxs-lookup"><span data-stu-id="80db6-233">For example the thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span></span>
      6. <span data-ttu-id="80db6-234">Attribuez le certificat de serveur au serveur de rapports.</span><span class="sxs-lookup"><span data-stu-id="80db6-234">Assign the server certificate to the report server.</span></span> <span data-ttu-id="80db6-235">L’attribution s’effectue dans la section suivante, lors de la configuration du serveur de rapports.</span><span class="sxs-lookup"><span data-stu-id="80db6-235">The assignment is completed in the next section when you configure the report server.</span></span>

<span data-ttu-id="80db6-236">Si vous utilisez un certificat SSL auto-signé, le nom du certificat correspond déjà au nom d’hôte de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-236">If you are using a self-signed SSL certificate, the name on the certificate already matches the hostname of the VM.</span></span> <span data-ttu-id="80db6-237">Par conséquent, le DNS de l’ordinateur est déjà enregistré globalement et accessible à partir de n’importe quel client.</span><span class="sxs-lookup"><span data-stu-id="80db6-237">Therefore, the DNS of the machine is already registered globally and can be accessed from any client.</span></span>

## <a name="step-3-configure-the-report-server"></a><span data-ttu-id="80db6-238">Étape 3 : Configurer le serveur de rapports</span><span class="sxs-lookup"><span data-stu-id="80db6-238">Step 3: Configure the Report Server</span></span>
<span data-ttu-id="80db6-239">Cette section vous explique comment configurer la machine virtuelle comme serveur de rapports Reporting Services en mode natif.</span><span class="sxs-lookup"><span data-stu-id="80db6-239">This section walks you through configuring the VM as a Reporting Services native mode report server.</span></span> <span data-ttu-id="80db6-240">Vous pouvez utiliser une des méthodes suivantes pour configurer le serveur de rapports :</span><span class="sxs-lookup"><span data-stu-id="80db6-240">You can use one of the following methods to configure the report server:</span></span>

* <span data-ttu-id="80db6-241">Utiliser le script pour configurer le serveur de rapports</span><span class="sxs-lookup"><span data-stu-id="80db6-241">Use the script to configure the report server</span></span>
* <span data-ttu-id="80db6-242">Utiliser le Gestionnaire de configuration pour configurer le serveur de rapports</span><span class="sxs-lookup"><span data-stu-id="80db6-242">Use Configuration Manager to Configure the Report Server.</span></span>

<span data-ttu-id="80db6-243">Pour obtenir la procédure détaillée, consultez la section [Se connecter à la machine virtuelle et démarrer le Gestionnaire de configuration de Reporting Services](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="80db6-243">For more detailed steps, see the section [Connect to the Virtual Machine and Start the Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span></span>

<span data-ttu-id="80db6-244">**Remarque sur l’authentification :** l’authentification Windows est la méthode d’authentification recommandée et l’authentification de Reporting Services par défaut.</span><span class="sxs-lookup"><span data-stu-id="80db6-244">**Authentication Note:** Windows authentication is the recommended authentication method and it is the default Reporting Services authentication.</span></span> <span data-ttu-id="80db6-245">Seuls les utilisateurs configurés sur la machine virtuelle peuvent accéder à Reporting Services et être affectés à  des rôles Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="80db6-245">Only users that are configured on the VM can access Reporting Services and assigned to Reporting Services roles.</span></span>

### <a name="use-script-to-configure-the-report-server-and-http"></a><span data-ttu-id="80db6-246">Utiliser un script pour configurer le serveur de rapports et HTTP</span><span class="sxs-lookup"><span data-stu-id="80db6-246">Use script to configure the report server and HTTP</span></span>
<span data-ttu-id="80db6-247">Pour utiliser le script Windows PowerShell afin de configurer le serveur de rapports, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="80db6-247">To use the Windows PowerShell script to configure the report server, complete the following steps.</span></span> <span data-ttu-id="80db6-248">La configuration inclut HTTP, pas HTTPS :</span><span class="sxs-lookup"><span data-stu-id="80db6-248">The configuration includes HTTP, not HTTPS:</span></span>

1. <span data-ttu-id="80db6-249">Dans le portail Azure Classic, sélectionnez la machine virtuelle, puis cliquez sur Connecter.</span><span class="sxs-lookup"><span data-stu-id="80db6-249">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="80db6-250">Selon la configuration de votre navigateur, vous pouvez être invité à enregistrer un fichier .rdp pour la connexion à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-250">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
   
    ![se connecter à une machine virtuelle azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="80db6-252">Utilisez le nom de machine virtuelle, le nom d’utilisateur et le mot de passe que vous avez configurés lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-252">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
   
    <span data-ttu-id="80db6-253">Par exemple, dans l’illustration suivante, le nom de la machine virtuelle est **ssrsnativecloud** et le nom d’utilisateur **testuser**.</span><span class="sxs-lookup"><span data-stu-id="80db6-253">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
   
    ![le nom de connexion inclut le nom de la machine virtuelle](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="80db6-255">Sur la machine virtuelle, ouvrez **Windows PowerShell ISE** avec des privilèges administratifs.</span><span class="sxs-lookup"><span data-stu-id="80db6-255">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="80db6-256">L’environnement d’écriture de scripts intégré PowerShell est installé par défaut sur Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="80db6-256">The PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="80db6-257">Nous vous recommandons d’utiliser l’environnement d’écriture de scripts intégré plutôt qu’une fenêtre Windows PowerShell standard afin de pouvoir coller le script dans l’environnement d’écriture de scripts intégré, le modifier, puis l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="80db6-257">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span></span>
3. <span data-ttu-id="80db6-258">Dans Windows PowerShell ISE, cliquez sur le menu **Affichage**, puis sur **Afficher le volet de script**.</span><span class="sxs-lookup"><span data-stu-id="80db6-258">In Windows PowerShell ISE, click the **View** menu and then click **Show Script Pane**.</span></span>
4. <span data-ttu-id="80db6-259">Copiez le script suivant et collez-le dans le volet de script Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="80db6-259">Copy the following script, and paste the script into the Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change the value if you used a different port for the private HTTP endpoint when the VM was created.
   
        ## Set PowerShell execution policy to be able to run scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change the version portion of the path to "v11" to use the script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting the web service URL ##
        write-host -foregroundcolor green "Setting the web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting the Database ##
        write-host -foregroundcolor green "Setting the Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating the database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script to create the database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes to sqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting the Report Manager URL ##
   
        write-host -foregroundcolor green "Setting the Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. <span data-ttu-id="80db6-260">Si vous avez créé la machine virtuelle avec un port HTTP autre que 80, modifiez le paramètre $HTTPport = 80.</span><span class="sxs-lookup"><span data-stu-id="80db6-260">If you created the VM with an HTTP port other than 80, modify the parameter $HTTPport = 80.</span></span>
6. <span data-ttu-id="80db6-261">Le script est actuellement configuré pour Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="80db6-261">The script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="80db6-262">Si vous souhaitez exécuter le script pour Reporting Services, remplacez la partie de la version du chemin d’accès à l’espace de noms « v11 » par l’instruction Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="80db6-262">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span></span>
7. <span data-ttu-id="80db6-263">Exécutez le script.</span><span class="sxs-lookup"><span data-stu-id="80db6-263">Run the script.</span></span>

<span data-ttu-id="80db6-264">**Validation**: pour vérifier que les fonctions de base du serveur de rapports fonctionnent, consultez la section [Vérifier la configuration](#verify-the-configuration) plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="80db6-264">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-configuration) section later in this topic.</span></span>

### <a name="use-script-to-configure-the-report-server-and-https"></a><span data-ttu-id="80db6-265">Utiliser un script pour configurer le serveur de rapports et HTTPS</span><span class="sxs-lookup"><span data-stu-id="80db6-265">Use script to configure the report server and HTTPS</span></span>
<span data-ttu-id="80db6-266">Pour utiliser Windows PowerShell afin de configurer le serveur de rapports, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="80db6-266">To use Windows PowerShell to configure the report server, complete the following steps.</span></span> <span data-ttu-id="80db6-267">La configuration inclut HTTPS, pas HTTP.</span><span class="sxs-lookup"><span data-stu-id="80db6-267">The configuration includes HTTPS, not HTTP.</span></span>

1. <span data-ttu-id="80db6-268">Dans le portail Azure Classic, sélectionnez la machine virtuelle, puis cliquez sur Connecter.</span><span class="sxs-lookup"><span data-stu-id="80db6-268">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="80db6-269">Selon la configuration de votre navigateur, vous pouvez être invité à enregistrer un fichier .rdp pour la connexion à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-269">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
   
    ![se connecter à une machine virtuelle azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="80db6-271">Utilisez le nom de machine virtuelle, le nom d’utilisateur et le mot de passe que vous avez configurés lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-271">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
   
    <span data-ttu-id="80db6-272">Par exemple, dans l’illustration suivante, le nom de la machine virtuelle est **ssrsnativecloud** et le nom d’utilisateur **testuser**.</span><span class="sxs-lookup"><span data-stu-id="80db6-272">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
   
    ![le nom de connexion inclut le nom de la machine virtuelle](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="80db6-274">Sur la machine virtuelle, ouvrez **Windows PowerShell ISE** avec des privilèges administratifs.</span><span class="sxs-lookup"><span data-stu-id="80db6-274">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="80db6-275">L’environnement d’écriture de scripts intégré PowerShell est installé par défaut sur Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="80db6-275">The PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="80db6-276">Nous vous recommandons d’utiliser l’environnement d’écriture de scripts intégré plutôt qu’une fenêtre Windows PowerShell standard afin de pouvoir coller le script dans l’environnement d’écriture de scripts intégré, le modifier, puis l’exécuter.</span><span class="sxs-lookup"><span data-stu-id="80db6-276">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span></span>
3. <span data-ttu-id="80db6-277">Pour activer les scripts en cours d’exécution, exécutez la commande Windows PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="80db6-277">To enable running scripts, run the following Windows PowerShell command:</span></span>
   
        Set-ExecutionPolicy RemoteSigned
   
    <span data-ttu-id="80db6-278">Vous pouvez ensuite exécuter la commande suivante pour vérifier la stratégie :</span><span class="sxs-lookup"><span data-stu-id="80db6-278">You can then run the following to verify the policy:</span></span>
   
        Get-ExecutionPolicy
4. <span data-ttu-id="80db6-279">Dans **Windows PowerShell ISE**, cliquez sur le menu **Affichage**, puis sur **Afficher le volet de script**.</span><span class="sxs-lookup"><span data-stu-id="80db6-279">In **Windows PowerShell ISE**, click the **View** menu and then click **Show Script Pane**.</span></span>
5. <span data-ttu-id="80db6-280">Copiez le script suivant et collez-le dans le volet de script Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="80db6-280">Copy the following script and paste it into the Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures the report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when the HTTPS endpoint was created.
   
        # You can run the following command to get (.cloudapp.net certificates) so you can copy the thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # The certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # the certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If the certificate is not a wildcard certificate, comment out the following line, and enable the full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "The script will use $DNSNameAndPort as the DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change the version portion of the path to "v11" to use the script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting the web service URL ##
        write-host -foregroundcolor green "Setting the web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting the Database ##
        write-host -foregroundcolor green "Setting the Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating the database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script to create the database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes to sqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting the Report Manager URL ##
   
        write-host -foregroundcolor green "Setting the Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. <span data-ttu-id="80db6-281">Modifiez le paramètre **$certificatehash** dans le script :</span><span class="sxs-lookup"><span data-stu-id="80db6-281">Modify the **$certificatehash** parameter in the script:</span></span>
   
   * <span data-ttu-id="80db6-282">Il s’agit d’un paramètre **obligatoire** .</span><span class="sxs-lookup"><span data-stu-id="80db6-282">This is a **required** parameter.</span></span> <span data-ttu-id="80db6-283">Si vous n’avez pas enregistré la valeur de certificat de la procédure précédente, utilisez une des méthodes suivantes pour copier la valeur de hachage du certificat à partir de l’empreinte numérique de certificats :</span><span class="sxs-lookup"><span data-stu-id="80db6-283">If you did not save the certificate value from the previous steps, use one of the following methods to copy the certificate hash value from the certificates thumbprint.:</span></span>
     
       <span data-ttu-id="80db6-284">Sur la machine virtuelle, ouvrez Windows PowerShell ISE et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="80db6-284">On the VM, open Windows PowerShell ISE and run the following command:</span></span>
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       <span data-ttu-id="80db6-285">Le résultat ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="80db6-285">The output will look similar to the following.</span></span> <span data-ttu-id="80db6-286">Si le script renvoie une ligne vide, par exemple que la machine virtuelle n’a pas de certificat configuré, consultez la section [Utiliser le certificat auto-signé Virtual Machines](#to-use-the-virtual-machines-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="80db6-286">If the script returns a blank line, the VM does not have a certificate configured for example, see the section [To use the Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span></span>
     
     <span data-ttu-id="80db6-287">OU</span><span class="sxs-lookup"><span data-stu-id="80db6-287">OR</span></span>
   * <span data-ttu-id="80db6-288">Sur la machine virtuelle, exécutez mmc.exe, puis ajoutez le composant logiciel enfichable **Certificats** .</span><span class="sxs-lookup"><span data-stu-id="80db6-288">On the VM Run mmc.exe and then add the **Certificates** snap-in.</span></span>
   * <span data-ttu-id="80db6-289">Sous le nœud **Autorités de certification racines de confiance** , double-cliquez sur le nom du certificat.</span><span class="sxs-lookup"><span data-stu-id="80db6-289">Under the **Trusted Root Certificate Authorities** node double-click your certificate name.</span></span> <span data-ttu-id="80db6-290">Si vous utilisez le certificat auto-signé de la machine virtuelle, le certificat est nommé d’après le nom DNS de la machine virtuelle et se termine par **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="80db6-290">If you are using the self-signed certificate of the VM, the certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span></span>
   * <span data-ttu-id="80db6-291">Cliquez sur l’onglet **Détails** .</span><span class="sxs-lookup"><span data-stu-id="80db6-291">Click the **Details** tab.</span></span>
   * <span data-ttu-id="80db6-292">Cliquez sur **Empreinte numérique**.</span><span class="sxs-lookup"><span data-stu-id="80db6-292">Click **Thumbprint**.</span></span> <span data-ttu-id="80db6-293">La valeur de l’empreinte numérique s’affiche dans le champ de détails, par exemple af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span><span class="sxs-lookup"><span data-stu-id="80db6-293">The value of the thumbprint is displayed in the details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span></span>
   * <span data-ttu-id="80db6-294">**Avant d’exécuter le script**, supprimez les espaces entre les paires de valeurs.</span><span class="sxs-lookup"><span data-stu-id="80db6-294">**Before you run the script**, remove the spaces in between the pairs of values.</span></span> <span data-ttu-id="80db6-295">Par exemple af1160b64b288d890a8212ff6ba9c3664f319048</span><span class="sxs-lookup"><span data-stu-id="80db6-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span></span>
7. <span data-ttu-id="80db6-296">Modifiez le paramètre **$httpsport** :</span><span class="sxs-lookup"><span data-stu-id="80db6-296">Modify the **$httpsport** parameter:</span></span> 
   
   * <span data-ttu-id="80db6-297">Si vous avez utilisé le port 443 pour le point de terminaison HTTPS, vous n’avez pas besoin de mettre à jour ce paramètre dans le script.</span><span class="sxs-lookup"><span data-stu-id="80db6-297">If you used port 443 for the HTTPS endpoint, then you do not need to update this parameter in the script.</span></span> <span data-ttu-id="80db6-298">Sinon, utilisez la valeur de port que vous avez sélectionnée lors de la configuration du point de terminaison privé HTTPS sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-298">Otherwise use the port value you selected when you configured the HTTPS private endpoint on the VM.</span></span>
8. <span data-ttu-id="80db6-299">Modifiez le paramètre **$DNSName** :</span><span class="sxs-lookup"><span data-stu-id="80db6-299">Modify the **$DNSName** parameter:</span></span> 
   
   * <span data-ttu-id="80db6-300">Le script est configuré pour un certificat à caractères génériques $DNSName = "+".</span><span class="sxs-lookup"><span data-stu-id="80db6-300">The script is configured for a wild card certificate $DNSName="+".</span></span> <span data-ttu-id="80db6-301">Si vous ne souhaitez pas configurer pour une liaison de certificat à caractères génériques, placez $DNSName ="+" en commentaires et activez la ligne suivante, la référence complète $DNSNAme, ##$DNSName="$server.cloudapp.net".</span><span class="sxs-lookup"><span data-stu-id="80db6-301">If you do no want to configure for a wildcard certificate binding, comment out $DNSName="+" and enable the following line, the full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span></span>
     
       <span data-ttu-id="80db6-302">Modifiez la valeur $DNSName si vous ne souhaitez pas utiliser le nom DNS de la machine virtuelle pour Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="80db6-302">Change the $DNSName value if you do not want to use the virtual machine’s DNS name for Reporting Services.</span></span> <span data-ttu-id="80db6-303">Si vous utilisez le paramètre, le certificat doit également utiliser ce nom, et vous inscrivez ce nom globalement sur un serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="80db6-303">If you use the parameter, the certificate must also use this name and you register the name globally on a DNS server.</span></span>
9. <span data-ttu-id="80db6-304">Le script est actuellement configuré pour Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="80db6-304">The script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="80db6-305">Si vous souhaitez exécuter le script pour Reporting Services, remplacez la partie de la version du chemin d’accès à l’espace de noms « v11 » par l’instruction Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="80db6-305">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span></span>
10. <span data-ttu-id="80db6-306">Exécutez le script.</span><span class="sxs-lookup"><span data-stu-id="80db6-306">Run the script.</span></span>

<span data-ttu-id="80db6-307">**Validation**: pour vérifier que les fonctions de base du serveur de rapports fonctionnent, consultez la section [Vérifier la configuration](#verify-the-connection) plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="80db6-307">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-connection) section later in this topic.</span></span> <span data-ttu-id="80db6-308">Pour vérifier la liaison de certificat, ouvrez une invite de commandes avec des privilèges administratifs, puis exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="80db6-308">To verify the certificate binding open a command prompt with administrative privileges, and then run the following command:</span></span>

    netsh http show sslcert

<span data-ttu-id="80db6-309">Le résultat comprend les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="80db6-309">The result will include the following:</span></span>

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-to-configure-the-report-server"></a><span data-ttu-id="80db6-310">Utiliser le Gestionnaire de configuration pour configurer le serveur de rapports</span><span class="sxs-lookup"><span data-stu-id="80db6-310">Use Configuration Manager to Configure the Report Server</span></span>
<span data-ttu-id="80db6-311">Si vous ne souhaitez pas exécuter le script PowerShell pour configurer le serveur de rapports, suivez la procédure décrite dans cette section pour utiliser le Gestionnaire de configuration de Reporting Services en mode natif afin de configurer le serveur de rapports.</span><span class="sxs-lookup"><span data-stu-id="80db6-311">If you do not want to run the PowerShell script to configure the report server, follow the steps in this section to use the Reporting Services native mode configuration manager to configure the report server.</span></span>

1. <span data-ttu-id="80db6-312">Dans le portail Azure Classic, sélectionnez la machine virtuelle, puis cliquez sur Connecter.</span><span class="sxs-lookup"><span data-stu-id="80db6-312">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="80db6-313">Utilisez le nom d’utilisateur et le mot de passe que vous avez configurés lors de la création de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-313">Use the user name and password you configured when you created the VM.</span></span>
   
    ![se connecter à une machine virtuelle azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. <span data-ttu-id="80db6-315">Exécutez Windows Update et installez les mises à jour de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-315">Run Windows update and install updates to the VM.</span></span> <span data-ttu-id="80db6-316">Si un redémarrage de la machine virtuelle est nécessaire, redémarrez la machine virtuelle et reconnectez-vous à celle-ci à partir du portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="80db6-316">If a restart of the VM is required, restart the VM and reconnect to the VM from the Azure classic portal.</span></span>
3. <span data-ttu-id="80db6-317">Dans le menu Démarrer de la machine virtuelle, saisissez **Reporting Services** et ouvrez le **Gestionnaire de configuration de Reporting Services**.</span><span class="sxs-lookup"><span data-stu-id="80db6-317">From the Start menu on the VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span></span>
4. <span data-ttu-id="80db6-318">Conservez les valeurs par défaut pour **Nom du serveur** et **Instance du serveur de rapports**.</span><span class="sxs-lookup"><span data-stu-id="80db6-318">Leave the default values for **Server Name** and **Report Server Instance**.</span></span> <span data-ttu-id="80db6-319">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="80db6-319">Click **Connect**.</span></span>
5. <span data-ttu-id="80db6-320">Dans le volet gauche, cliquez sur **URL du service Web**.</span><span class="sxs-lookup"><span data-stu-id="80db6-320">In the left pane, click **Web Service URL**.</span></span>
6. <span data-ttu-id="80db6-321">Par défaut, Reporting Services est configuré pour le port HTTP 80 avec l’adresse IP « entièrement affectée ».</span><span class="sxs-lookup"><span data-stu-id="80db6-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span></span> <span data-ttu-id="80db6-322">Pour ajouter HTTPS :</span><span class="sxs-lookup"><span data-stu-id="80db6-322">To add HTTPS:</span></span>
   
   1. <span data-ttu-id="80db6-323">Dans **Certificat SSL**: sélectionnez le certificat que vous souhaitez utiliser, par exemple [nom de la machine virtuelle].cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="80db6-323">In **SSL Certificate**: select the certificate you want to use, for example [VM name].cloudapp.net.</span></span> <span data-ttu-id="80db6-324">Si aucun certificat n’est répertorié, consultez la section **Étape 2 : Créer un certificat de serveur** pour obtenir les instructions d’installation et d’approbation du certificat sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-324">If no certificates are listed, see the section **Step 2: Create a Server Certificate** for information on how to install and trust the certificate on the VM.</span></span>
   2. <span data-ttu-id="80db6-325">Sous **Port SSL**: sélectionnez 443.</span><span class="sxs-lookup"><span data-stu-id="80db6-325">Under **SSL Port**: choose 443.</span></span> <span data-ttu-id="80db6-326">Si vous avez configuré le point de terminaison privé HTTPS dans la machine virtuelle avec un autre port privé, utilisez cette valeur ici.</span><span class="sxs-lookup"><span data-stu-id="80db6-326">If you configured the HTTPS private endpoint in the VM with a different private port, use that value here.</span></span>
   3. <span data-ttu-id="80db6-327">Cliquez sur **Appliquer** et attendez que l’opération soit terminée.</span><span class="sxs-lookup"><span data-stu-id="80db6-327">Click **Apply** and wait for the operation to complete.</span></span>
7. <span data-ttu-id="80db6-328">Dans le volet de gauche, cliquez sur **Base de données**.</span><span class="sxs-lookup"><span data-stu-id="80db6-328">In the left pane, click **Database**.</span></span>
   
   1. <span data-ttu-id="80db6-329">Cliquez sur **Changer la base de données**.</span><span class="sxs-lookup"><span data-stu-id="80db6-329">Click **Change Databas**e.</span></span>
   2. <span data-ttu-id="80db6-330">Cliquez sur **Créer une nouvelle base de données de serveur de rapports**, puis sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="80db6-330">Click **Create a new report server database** and then click **Next**.</span></span>
   3. <span data-ttu-id="80db6-331">Laissez la valeur par défaut **Nom du serveur** : comme nom de la machine virtuelle et la valeur par défaut **Type d’authentification** sur **Utilisateur actuel** – **Sécurité intégrée**.</span><span class="sxs-lookup"><span data-stu-id="80db6-331">Leave the default **Server Name**: as the VM name and leave the default **Authentication Type** as **Current User** – **Integrated Security**.</span></span> <span data-ttu-id="80db6-332">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="80db6-332">Click **Next**.</span></span>
   4. <span data-ttu-id="80db6-333">Laissez la valeur par défaut **Nom de la base de données** sur **ReportServer** et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="80db6-333">Leave the default **Database Name** as **ReportServer** and click **Next**.</span></span>
   5. <span data-ttu-id="80db6-334">Laissez la valeur par défaut **Type d’authentification** sur **Informations d’identification du service** et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="80db6-334">Leave the default **Authentication Type** as **Service Credentials** and click **Next**.</span></span>
   6. <span data-ttu-id="80db6-335">Cliquez sur **Suivant** on the **Suivant** .</span><span class="sxs-lookup"><span data-stu-id="80db6-335">Click **Next** on the **Summary** page.</span></span>
   7. <span data-ttu-id="80db6-336">Une fois la configuration terminée, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="80db6-336">When the configuration is complete, click **Finish**.</span></span>
8. <span data-ttu-id="80db6-337">Dans le volet de gauche, cliquez sur **URL du Gestionnaire de rapports**.</span><span class="sxs-lookup"><span data-stu-id="80db6-337">In the left pane, click **Report Manager URL**.</span></span> <span data-ttu-id="80db6-338">Laissez la valeur par défaut **Répertoire virtuel** sur **Rapports** et cliquez sur **Appliquer**.</span><span class="sxs-lookup"><span data-stu-id="80db6-338">Leave the default **Virtual Directory** as **Reports** and click **Apply**.</span></span>
9. <span data-ttu-id="80db6-339">Cliquez sur **Quitter** pour fermer le Gestionnaire de configuration de Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="80db6-339">Click **Exit** to close the Reporting Services Configuration Manager.</span></span>

## <a name="step-4-open-windows-firewall-port"></a><span data-ttu-id="80db6-340">Étape 4 : Ouvrir le port du pare-feu Windows</span><span class="sxs-lookup"><span data-stu-id="80db6-340">Step 4: Open Windows Firewall Port</span></span>
> [!NOTE]
> <span data-ttu-id="80db6-341">Si vous avez utilisé un des scripts pour configurer le serveur de rapports, vous pouvez ignorer cette section.</span><span class="sxs-lookup"><span data-stu-id="80db6-341">If you used one of the scripts to configure the report server, you can skip this section.</span></span> <span data-ttu-id="80db6-342">Le script inclut une étape pour ouvrir le port du pare-feu.</span><span class="sxs-lookup"><span data-stu-id="80db6-342">The script included a step to open the firewall port.</span></span> <span data-ttu-id="80db6-343">La valeur par défaut est le port 80 pour HTTP et le port 443 pour HTTPS.</span><span class="sxs-lookup"><span data-stu-id="80db6-343">The default was port 80 for HTTP and port 443 for HTTPS.</span></span>
> 
> 

<span data-ttu-id="80db6-344">Pour vous connecter à distance au Gestionnaire de rapports ou au serveur de rapports sur la machine virtuelle, vous devez disposer d’un point de terminaison TCP sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-344">To connect remotely to Report Manager or the Report Server on the virtual machine, a TCP Endpoint is required on the VM.</span></span> <span data-ttu-id="80db6-345">Il est nécessaire d’ouvrir le même port dans le pare-feu de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-345">It is required to open the same port in the VM’s firewall.</span></span> <span data-ttu-id="80db6-346">Le point de terminaison a été créé lors de l’approvisionnement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-346">The endpoint was created when the VM was provisioned.</span></span>

<span data-ttu-id="80db6-347">Cette section fournit des informations de base sur l’ouverture du port du pare-feu.</span><span class="sxs-lookup"><span data-stu-id="80db6-347">This section provides basic information on how to open the firewall port.</span></span> <span data-ttu-id="80db6-348">Pour plus d’informations, consultez la page [Configurer un pare-feu pour accéder au serveur de rapports](https://technet.microsoft.com/library/bb934283.aspx)</span><span class="sxs-lookup"><span data-stu-id="80db6-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="80db6-349">Si vous avez utilisé le script pour configurer le serveur de rapports, vous pouvez ignorer cette section.</span><span class="sxs-lookup"><span data-stu-id="80db6-349">If you used the script to configure the report server, you can skip this section.</span></span> <span data-ttu-id="80db6-350">Le script inclut une étape pour ouvrir le port du pare-feu.</span><span class="sxs-lookup"><span data-stu-id="80db6-350">The script included a step to open the firewall port.</span></span>
> 
> 

<span data-ttu-id="80db6-351">Si vous avez configuré un port privé pour HTTPS autre que 443, modifiez le script suivant en conséquence.</span><span class="sxs-lookup"><span data-stu-id="80db6-351">If you configured a private port for HTTPS other than 443, modify the following script appropriately.</span></span> <span data-ttu-id="80db6-352">Pour ouvrir le port **443** sur le pare-feu Windows, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="80db6-352">To open port **443** on the Windows Firewall, complete the following:</span></span>

1. <span data-ttu-id="80db6-353">Ouvrez une fenêtre Windows PowerShell avec des privilèges administratifs.</span><span class="sxs-lookup"><span data-stu-id="80db6-353">Open a Windows PowerShell window with administrative privileges.</span></span>
2. <span data-ttu-id="80db6-354">Si vous avez utilisé un port autre que 443 lors de la configuration du point de terminaison HTTPS sur la machine virtuelle, mettez à jour le port dans la commande suivante, puis exécutez la commande :</span><span class="sxs-lookup"><span data-stu-id="80db6-354">If you used a port other than 443 when you configured the HTTPS endpoint on the VM, update the port in the following command and then run the command:</span></span>
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. <span data-ttu-id="80db6-355">Lorsque la commande est terminée, **OK** s’affiche dans l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="80db6-355">When the command completes, **Ok** is displayed in the command prompt.</span></span>

<span data-ttu-id="80db6-356">Pour vérifier que le port est bien ouvert, ouvrez une fenêtre Windows PowerShell et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="80db6-356">To verify that the port is opened, open a Windows PowerShell window and run the following command:</span></span>

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-the-configuration"></a><span data-ttu-id="80db6-357">Vérifier la configuration</span><span class="sxs-lookup"><span data-stu-id="80db6-357">Verify the configuration</span></span>
<span data-ttu-id="80db6-358">Pour vérifier que les fonctions de base du serveur de rapports fonctionnent, ouvrez votre navigateur avec des privilèges administratifs, puis accédez aux URL de serveur de rapports et de Gestionnaire de rapports suivants :</span><span class="sxs-lookup"><span data-stu-id="80db6-358">To verify that the basic report server functionality is now working, open your browser with administrative privileges and then browse to the following report server ad report manager URLS:</span></span>

* <span data-ttu-id="80db6-359">Sur la machine virtuelle, accédez à l’URL du serveur de rapports :</span><span class="sxs-lookup"><span data-stu-id="80db6-359">On the VM, browse to the report server URL:</span></span>
  
        http://localhost/reportserver
* <span data-ttu-id="80db6-360">Sur la machine virtuelle, accédez à l’URL du Gestionnaire de rapports :</span><span class="sxs-lookup"><span data-stu-id="80db6-360">On the VM, browse to the report manger URL:</span></span>
  
        http://localhost/Reports
* <span data-ttu-id="80db6-361">À partir de votre ordinateur local, accédez au Gestionnaire de rapports **distant** sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-361">From your local computer, browse to the **remote** report Manager on the VM.</span></span> <span data-ttu-id="80db6-362">Mettez à jour le nom DNS dans l’exemple suivant, comme requis.</span><span class="sxs-lookup"><span data-stu-id="80db6-362">Update the DNS name in the following example as appropriate.</span></span> <span data-ttu-id="80db6-363">Lorsque vous êtes invité à entrer un mot de passe, utilisez les informations d’identification d’administrateur que vous avez créées lors de l’approvisionnement de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-363">When prompted for a password, use the administrator credentials you created when the VM was provisioned.</span></span> <span data-ttu-id="80db6-364">Le nom d’utilisateur est au format [Domaine]\[nom utilisateur], où le domaine correspond au nom de la machine virtuelle, par exemple ssrsnativecloud\testuser.</span><span class="sxs-lookup"><span data-stu-id="80db6-364">The user name is in the [Domain]\[user name] format, where the domain is the VM computer name, for example ssrsnativecloud\testuser.</span></span> <span data-ttu-id="80db6-365">Si vous n’utilisez pas HTTP**S**, supprimez le **s** dans l’URL.</span><span class="sxs-lookup"><span data-stu-id="80db6-365">If you are not using HTTP**S**, remove the **s** in the URL.</span></span> <span data-ttu-id="80db6-366">Pour plus d’informations sur la création d’utilisateurs supplémentaires sur la machine virtuelle, consultez la section suivante.</span><span class="sxs-lookup"><span data-stu-id="80db6-366">See the next section for information on creating additional users on VM.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/Reports
* <span data-ttu-id="80db6-367">À partir de votre ordinateur local, accédez à l’URL du serveur de rapports distant.</span><span class="sxs-lookup"><span data-stu-id="80db6-367">From your local computer, browse to the remote report server URL.</span></span> <span data-ttu-id="80db6-368">Mettez à jour le nom DNS dans l’exemple suivant, comme requis.</span><span class="sxs-lookup"><span data-stu-id="80db6-368">Update the DNS name in the following example as appropriate.</span></span> <span data-ttu-id="80db6-369">Si vous n’utilisez pas HTTPS, supprimez le « s » dans l’URL.</span><span class="sxs-lookup"><span data-stu-id="80db6-369">If you are not using HTTPS, remove the s in the URL.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a><span data-ttu-id="80db6-370">Créer des utilisateurs et attribuer des rôles</span><span class="sxs-lookup"><span data-stu-id="80db6-370">Create Users and Assign Roles</span></span>
<span data-ttu-id="80db6-371">Une fois le serveur de rapports configuré et vérifié, il est courant d’effectuer la tâche administrative consistant à créer un ou plusieurs utilisateurs et à affecter des utilisateurs aux rôles Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="80db6-371">After configuring and verifying the report server, a common administrative task is to create one or more users and assign users to Reporting Services roles.</span></span> <span data-ttu-id="80db6-372">Pour plus d’informations, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="80db6-372">For more information, see the following:</span></span>

* [<span data-ttu-id="80db6-373">Créer un compte d’utilisateur local</span><span class="sxs-lookup"><span data-stu-id="80db6-373">Create a local user account</span></span>](https://technet.microsoft.com/library/cc770642.aspx)
* <span data-ttu-id="80db6-374">[Accorder à un utilisateur l’accès à un serveur de rapports (Gestionnaire de rapports)](https://msdn.microsoft.com/library/ms156034.aspx)</span><span class="sxs-lookup"><span data-stu-id="80db6-374">[Grant User Access to a Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span></span>
* [<span data-ttu-id="80db6-375">Créer et gérer des attributions de rôles</span><span class="sxs-lookup"><span data-stu-id="80db6-375">Create and Manage Role Assignments</span></span>](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="to-create-and-publish-reports-to-the-azure-virtual-machine"></a><span data-ttu-id="80db6-376">Pour créer et publier des rapports sur la machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="80db6-376">To Create and Publish Reports to the Azure Virtual Machine</span></span>
<span data-ttu-id="80db6-377">Le tableau suivant résume certaines des options disponibles pour publier des rapports existants à partir d’un ordinateur local vers le serveur de rapports hébergé sur la machine virtuelle Microsoft Azure :</span><span class="sxs-lookup"><span data-stu-id="80db6-377">The following table summarizes some of the options available to publish existing reports from an on-premises computer to the report server hosted on the Microsoft Azure Virtual Machine:</span></span>

* <span data-ttu-id="80db6-378">**Script RS.exe**: utilisez le script RS.exe pour copier des éléments de rapport à partir du serveur de rapports existant vers la machine virtuelle Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="80db6-378">**RS.exe script**: Use RS.exe script to copy report items from and existing report server to your Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="80db6-379">Pour plus d’informations, consultez la section « Mode natif vers mode natif – Machine virtuelle Microsoft Azure » dans [Exemple de script Reporting Services rs.exe pour migrer le contenu entre des serveurs de rapports](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="80db6-379">For more information, see the section “Native mode to Native Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>
* <span data-ttu-id="80db6-380">**Générateur de rapports**: la machine virtuelle inclut la version un clic du Générateur de rapports Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="80db6-380">**Report Builder**: The virtual machine includes the click-once version of Microsoft SQL Server Report Builder.</span></span> <span data-ttu-id="80db6-381">Pour démarrer le Générateur de rapports la première fois sur la machine virtuelle:</span><span class="sxs-lookup"><span data-stu-id="80db6-381">To start Report builder the first time on the virtual machine:</span></span>
  
  1. <span data-ttu-id="80db6-382">Démarrez votre navigateur avec des privilèges administratifs.</span><span class="sxs-lookup"><span data-stu-id="80db6-382">Start your browser with administrative privileges.</span></span>
  2. <span data-ttu-id="80db6-383">Accédez au Gestionnaire de rapports sur la machine virtuelle et cliquez sur **Générateur de rapports** dans le ruban.</span><span class="sxs-lookup"><span data-stu-id="80db6-383">Browse to report manager on the virtual machine and click **Report Builder**  in the ribbon.</span></span>
     
     <span data-ttu-id="80db6-384">Pour plus d’informations, consultez [Installation, désinstallation et prise en charge du Générateur de rapports](https://technet.microsoft.com/library/dd207038.aspx).</span><span class="sxs-lookup"><span data-stu-id="80db6-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span></span>
* <span data-ttu-id="80db6-385">**SQL Server Data Tools : machine virtuelle** : si vous avez créé la machine virtuelle à l’aide de SQL Server 2012, SQL Server Data Tools est installé sur la machine virtuelle et peut être utilisé pour créer des **Projets de serveur de rapports** et des rapports sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-385">**SQL Server Data Tools: VM**:  If you created the VM with SQL Server 2012, then SQL Server Data Tools is installed on the virtual machine and can be used to create **Report Server Projects** and reports on the virtual machine.</span></span> <span data-ttu-id="80db6-386">SQL Server Data Tools peut publier les rapports vers le serveur de rapports sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-386">SQL Server Data Tools can publish the reports to the report server on the virtual machine.</span></span>
  
    <span data-ttu-id="80db6-387">Si vous avez créé la machine virtuelle à l’aide de SQL Server 2014, vous pouvez installer SQL Server Data Tools - Business Intelligence pour Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="80db6-387">If you created the VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span></span> <span data-ttu-id="80db6-388">Pour plus d’informations, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="80db6-388">For more information, see the following:</span></span>
  
  * [<span data-ttu-id="80db6-389">Microsoft SQL Server Data Tools - Business Intelligence pour Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="80db6-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span></span>](https://www.microsoft.com/download/details.aspx?id=42313)
  * [<span data-ttu-id="80db6-390">Microsoft SQL Server Data Tools - Business Intelligence pour Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="80db6-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=36843)
  * [<span data-ttu-id="80db6-391">SQL Server Data Tools et SQL Server Business Intelligence (SSDT-BI)</span><span class="sxs-lookup"><span data-stu-id="80db6-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span></span>](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* <span data-ttu-id="80db6-392">**SQL Server Data Tools : distant** : sur votre ordinateur local, créez un projet Reporting Services contenant des rapports Reporting Services dans SQL Server Data Tools.</span><span class="sxs-lookup"><span data-stu-id="80db6-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span></span> <span data-ttu-id="80db6-393">Configurez le projet pour la connexion à l’URL du service web.</span><span class="sxs-lookup"><span data-stu-id="80db6-393">Configure the project to connect to the web service URL.</span></span>
  
    ![propriétés de projet ssdt pour un projet SSRS](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* <span data-ttu-id="80db6-395">**Utiliser le script**: utilisez le script pour copier le contenu du serveur de rapports.</span><span class="sxs-lookup"><span data-stu-id="80db6-395">**Use script**: Use script to copy report server content.</span></span> <span data-ttu-id="80db6-396">Pour plus d’informations, consultez la page [Exemple de script Reporting Services rs.exe pour migrer le contenu entre des serveurs de rapports](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="80db6-396">For more information, see [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>

## <a name="minimize-cost-if-you-are-not-using-the-vm"></a><span data-ttu-id="80db6-397">Réduire les coûts si vous n’utilisez pas la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="80db6-397">Minimize cost if you are not using the VM</span></span>
> [!NOTE]
> <span data-ttu-id="80db6-398">Pour réduire les frais associés à vos machines virtuelles Azure lorsque vous ne les utilisez pas, arrêtez la machine virtuelle à partir du portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="80db6-398">To minimize charges for your Azure Virtual Machines when not in use, shut down the VM from the Azure classic portal.</span></span> <span data-ttu-id="80db6-399">Si vous utilisez les options d’alimentation Windows d’une machine virtuelle pour arrêter la machine virtuelle, vous êtes toujours facturé du même montant pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="80db6-399">If you use the Windows power options inside a VM to shut down the VM, you are still charged the same amount for the VM.</span></span> <span data-ttu-id="80db6-400">Pour réduire les frais, vous devez arrêter la machine virtuelle dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="80db6-400">To reduce charges, you need to shut down the VM in the Azure classic portal.</span></span> <span data-ttu-id="80db6-401">Si vous n’avez plus besoin de la machine virtuelle, n’oubliez pas de la supprimer, ainsi que les fichiers .vhd associés, pour éviter des frais de stockage. Pour plus d’informations, consultez la FAQ à la page [Tarification des machines virtuelles](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="80db6-401">If you no longer need the VM, remember to delete the VM and the associated .vhd files to avoid storage charges.For more information, see the FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>

## <a name="more-information"></a><span data-ttu-id="80db6-402">Informations complémentaires</span><span class="sxs-lookup"><span data-stu-id="80db6-402">More Information</span></span>
### <a name="resources"></a><span data-ttu-id="80db6-403">Ressources</span><span class="sxs-lookup"><span data-stu-id="80db6-403">Resources</span></span>
* <span data-ttu-id="80db6-404">Pour obtenir un contenu similaire relatif au déploiement sur un seul serveur de SQL Server Business Intelligence et SharePoint 2013, consultez la page [Utiliser Windows PowerShell pour créer une machine virtuelle Azure avec SQL Server BI et SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span><span class="sxs-lookup"><span data-stu-id="80db6-404">For similar content related to a single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell to Create an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span></span>
* <span data-ttu-id="80db6-405">Pour obtenir un contenu similaire relatif au déploiement sur plusieurs serveurs de SQL Server Business Intelligence et SharePoint 2013, consultez la page [Déployer SQL Server Business Intelligence dans Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span><span class="sxs-lookup"><span data-stu-id="80db6-405">For similar content related to a multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span></span>
* <span data-ttu-id="80db6-406">Pour des informations d’ordre général sur les déploiements de SQL Server Business Intelligence dans Azure Virtual Machines, consultez la page [SQL Server Business Intelligence dans Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span><span class="sxs-lookup"><span data-stu-id="80db6-406">For General information related to deployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span></span>
* <span data-ttu-id="80db6-407">Pour plus d’informations sur le montant des frais de calcul Azure, consultez l’onglet Virtual Machines de la [calculatrice de prix Azure](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="80db6-407">For more information about the cost of Azure compute charges, see the Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span></span>

### <a name="community-content"></a><span data-ttu-id="80db6-408">Contenu de la communauté</span><span class="sxs-lookup"><span data-stu-id="80db6-408">Community Content</span></span>
* <span data-ttu-id="80db6-409">Pour obtenir des instructions étape par étape sur la création d’un serveur de rapports Reporting Services en mode natif sans utiliser de script, consultez la page [Hébergement de SQL Reporting Services sur une machine virtuelle Azure](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span><span class="sxs-lookup"><span data-stu-id="80db6-409">For step by step instructions on how to create a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span></span>

### <a name="links-to-other-resources-for-sql-server-in-azure-vms"></a><span data-ttu-id="80db6-410">Liens vers d’autres ressources pour SQL Server dans les machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="80db6-410">Links to other resources for SQL Server in Azure VMs</span></span>
[<span data-ttu-id="80db6-411">Vue d’ensemble de SQL Server sur les machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="80db6-411">SQL Server on Azure Virtual Machines Overview</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

