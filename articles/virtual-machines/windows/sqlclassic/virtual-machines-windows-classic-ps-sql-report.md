---
title: aaaUse PowerShell tooCreate une machine virtuelle avec un serveur en Mode natif rapport | Documents Microsoft
description: "Cette rubrique décrit et vous guide à travers le déploiement de hello et la configuration d’un serveur de rapports SQL Server Reporting Services en mode natif dans une Machine virtuelle Azure. "
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
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a><span data-ttu-id="ff34c-103">Utilisez PowerShell tooCreate un Azure VM avec un serveur en Mode natif rapport</span><span class="sxs-lookup"><span data-stu-id="ff34c-103">Use PowerShell tooCreate an Azure VM With a Native Mode Report Server</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="ff34c-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ff34c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ff34c-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="ff34c-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="ff34c-107">Cette rubrique décrit et vous guide à travers le déploiement de hello et la configuration d’un serveur de rapports SQL Server Reporting Services en mode natif dans une Machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="ff34c-107">This topic describes and walks you through hello deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span></span> <span data-ttu-id="ff34c-108">Hello étapes tooconfigure Reporting Services dans ce document utilisent une combinaison de machine virtuelle d’étapes manuelles toocreate hello et un script Windows PowerShell sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ff34c-108">hello steps in this document use a combination of manual steps toocreate hello virtual machine and a Windows PowerShell script tooconfigure Reporting Services on hello VM.</span></span> <span data-ttu-id="ff34c-109">script de configuration Hello inclut l’ouverture d’un port de pare-feu pour HTTP ou HTTPs.</span><span class="sxs-lookup"><span data-stu-id="ff34c-109">hello configuration script includes opening a firewall port for HTTP or HTTPs.</span></span>

> [!NOTE]
> <span data-ttu-id="ff34c-110">Si vous n’avez pas besoin **HTTPS** sur le serveur de rapports hello, **ignorez l’étape 2**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-110">If you do not require **HTTPS** on hello report server, **skip step 2**.</span></span>
> 
> <span data-ttu-id="ff34c-111">Après avoir créé le hello machine virtuelle à l’étape 1, accédez à HTTP et le serveur de rapports toohello section Utilisation script tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-111">After creating hello VM in step 1, go toohello section Use script tooconfigure hello report server and HTTP.</span></span> <span data-ttu-id="ff34c-112">Après avoir exécuté le script de hello, le serveur de rapports hello est toouse prêt.</span><span class="sxs-lookup"><span data-stu-id="ff34c-112">After you run hello script, hello report server is ready toouse.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="ff34c-113">Configuration requise et hypothèses</span><span class="sxs-lookup"><span data-stu-id="ff34c-113">Prerequisites and Assumptions</span></span>
* <span data-ttu-id="ff34c-114">**Abonnement Azure**: vérifier le nombre de hello de cœurs disponibles dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ff34c-114">**Azure Subscription**: Verify hello number of cores available in your Azure Subscription.</span></span> <span data-ttu-id="ff34c-115">Si vous créez hello recommandée de machine virtuelle **A3**, vous devez **4** cœurs disponibles.</span><span class="sxs-lookup"><span data-stu-id="ff34c-115">If you create hello recommended VM size of **A3**, you need **4** available cores.</span></span> <span data-ttu-id="ff34c-116">Si vous utilisez une machine virtuelle de taille **A2**, vous devez disposer de **2** mémoires à tores magnétiques.</span><span class="sxs-lookup"><span data-stu-id="ff34c-116">If you use a VM size of **A2**, you need **2** available cores.</span></span>
  
  * <span data-ttu-id="ff34c-117">limite de cœurs hello tooverify de votre abonnement, hello portail Azure classic, cliquez sur paramètres dans le volet gauche de hello, puis cliquez sur l’utilisation dans le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-117">tooverify hello core limit of your subscription, in hello Azure classic portal, click SETTINGS in hello left pane and then Click USAGE in hello top menu.</span></span>
  * <span data-ttu-id="ff34c-118">tooincrease hello quota de cœurs, contactez [prise en charge Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="ff34c-118">tooincrease hello core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span></span> <span data-ttu-id="ff34c-119">Pour plus d’informations sur les tailles de machines virtuelles, consultez la page [Tailles de machines virtuelles pour Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ff34c-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="ff34c-120">**Exécution de scripts Windows PowerShell**: hello nous supposons que vous avez une connaissance de base de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff34c-120">**Windows PowerShell Scripting**: hello topic assumes that you have a basic working knowledge of Windows PowerShell.</span></span> <span data-ttu-id="ff34c-121">Pour plus d’informations sur l’utilisation de Windows PowerShell, voir hello :</span><span class="sxs-lookup"><span data-stu-id="ff34c-121">For more information about using Windows PowerShell, see hello following:</span></span>
  
  * [<span data-ttu-id="ff34c-122">Démarrage de Windows PowerShell sur Windows Server</span><span class="sxs-lookup"><span data-stu-id="ff34c-122">Starting Windows PowerShell on Windows Server</span></span>](https://technet.microsoft.com/library/hh847814.aspx)
  * [<span data-ttu-id="ff34c-123">Prise en main de Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff34c-123">Getting Started with Windows PowerShell</span></span>](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a><span data-ttu-id="ff34c-124">Étape 1 : Approvisionner une machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="ff34c-124">Step 1: Provision an Azure Virtual Machine</span></span>
1. <span data-ttu-id="ff34c-125">Parcourir toohello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="ff34c-125">Browse toohello Azure classic portal.</span></span>
2. <span data-ttu-id="ff34c-126">Cliquez sur **virtuels** dans le volet gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-126">Click **Virtual Machines** in hello left pane.</span></span>
   
    ![microsoft azure virtual machines](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. <span data-ttu-id="ff34c-128">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-128">Click **New**.</span></span>
   
    ![bouton nouveau](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. <span data-ttu-id="ff34c-130">Cliquez sur **À partir de la galerie**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-130">Click **From Gallery**.</span></span>
   
    ![nouvelle machine virtuelle à partir de la galerie](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. <span data-ttu-id="ff34c-132">Cliquez sur **SQL Server 2014 RTM Standard – Windows Server 2012 R2** puis cliquez sur hello flèche toocontinue.</span><span class="sxs-lookup"><span data-stu-id="ff34c-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click hello arrow toocontinue.</span></span>
   
    ![Suivant](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    <span data-ttu-id="ff34c-134">Si vous avez besoin de fonctionnalité d’abonnements pilotés par les données de Reporting Services salutation, choisissez **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-134">If you need hello Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span></span> <span data-ttu-id="ff34c-135">Pour plus d’informations sur les éditions de SQL Server et de prise en charge de la fonctionnalité, consultez [fonctionnalités prises en charge par les éditions de SQL Server 2012 de hello](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span><span class="sxs-lookup"><span data-stu-id="ff34c-135">For more information on SQL Server editions and feature support, see [Features Supported by hello Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span></span>
6. <span data-ttu-id="ff34c-136">Sur hello **configuration d’ordinateur virtuel** page, modifier hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="ff34c-136">On hello **Virtual machine configuration** page, edit hello following fields:</span></span>
   
   * <span data-ttu-id="ff34c-137">S’il existe plusieurs **DATE de publication de la VERSION**, sélectionnez hello version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="ff34c-137">If there is more than one **VERSION RELEASE DATE**, select hello most recent version.</span></span>
   * <span data-ttu-id="ff34c-138">**Nom de Machine virtuelle**: nom de l’ordinateur hello est également utilisé sur la page de configuration suivante hello en tant que nom de Cloud Service DNS par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-138">**Virtual Machine Name**: hello machine name is also used on hello next configuration page as hello default Cloud Service DNS name.</span></span> <span data-ttu-id="ff34c-139">nom DNS de Hello doit être unique sur hello service Azure.</span><span class="sxs-lookup"><span data-stu-id="ff34c-139">hello DNS name must be unique across hello Azure service.</span></span> <span data-ttu-id="ff34c-140">Envisagez de configurer hello machine virtuelle avec un nom qui décrit quelles hello pour que machine virtuelle est utilisée.</span><span class="sxs-lookup"><span data-stu-id="ff34c-140">Consider configuring hello VM with a computer name that describes what hello VM is used for.</span></span> <span data-ttu-id="ff34c-141">Par exemple, ssrsnativecloud.</span><span class="sxs-lookup"><span data-stu-id="ff34c-141">For example ssrsnativecloud.</span></span>
   * <span data-ttu-id="ff34c-142">**Niveau**: Standard</span><span class="sxs-lookup"><span data-stu-id="ff34c-142">**Tier**: Standard</span></span>
   * <span data-ttu-id="ff34c-143">**Taille : A3** hello est recommandé de taille de machine virtuelle pour les charges de travail SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ff34c-143">**Size:A3** is hello recommended VM size for SQL Server workloads.</span></span> <span data-ttu-id="ff34c-144">Si un ordinateur virtuel est utilisé uniquement comme un serveur de rapports, une taille de machine virtuelle A2 est suffisante, sauf si le serveur de rapports hello rencontre une grande charge de travail.</span><span class="sxs-lookup"><span data-stu-id="ff34c-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless hello report server experiences a large workload.</span></span> <span data-ttu-id="ff34c-145">Pour connaître les informations de tarification des machines virtuelles, consultez la page [Tarification des machines virtuelles](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="ff34c-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
   * <span data-ttu-id="ff34c-146">**Nouveau nom d’utilisateur**: nom hello que vous fournissez est créé en tant qu’administrateur sur la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-146">**New User Name**: hello name you provide is created as an administrator on hello VM.</span></span>
   * <span data-ttu-id="ff34c-147">**Nouveau mot de passe** et **confirmation**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-147">**New Password** and **confirm**.</span></span> <span data-ttu-id="ff34c-148">Ce mot de passe est utilisé pour le nouveau compte d’administrateur hello et il est recommandé de qu'utiliser un mot de passe fort.</span><span class="sxs-lookup"><span data-stu-id="ff34c-148">This password is used for hello new administrator account and it is recommended you use a strong password.</span></span>
   * <span data-ttu-id="ff34c-149">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-149">Click **Next**.</span></span> <span data-ttu-id="ff34c-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span><span class="sxs-lookup"><span data-stu-id="ff34c-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span></span>
7. <span data-ttu-id="ff34c-151">Sur la page suivante de hello, modifiez hello champs qui suivent :</span><span class="sxs-lookup"><span data-stu-id="ff34c-151">On hello next page, edit hello following fields:</span></span>
   
   * <span data-ttu-id="ff34c-152">**Service cloud** : sélectionnez **Créer un service cloud**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-152">**Cloud Service**: select **Create a new Cloud Service**.</span></span>
   * <span data-ttu-id="ff34c-153">**Nom DNS du Service de cloud computing**: le nom DNS public de hello Hello Service Cloud qui est associé à hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ff34c-153">**Cloud Service DNS Name**: This is hello public DNS name of hello Cloud Service that is associated with hello VM.</span></span> <span data-ttu-id="ff34c-154">nom par défaut de Hello est hello que vous avez tapé pour le nom d’ordinateur virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-154">hello default name is hello name you typed in for hello VM name.</span></span> <span data-ttu-id="ff34c-155">Si dans les étapes ultérieures de la rubrique de hello, vous créez un certificat SSL approuvé et le nom DNS de hello est utilisée pour valeur hello Hello »**délivré à**» du certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-155">If in later steps of hello topic, you create a trusted SSL certificate and then hello DNS name is used for hello value of hello “**Issued to**” of hello certificate.</span></span>
   * <span data-ttu-id="ff34c-156">**Affinité de la région/groupe/réseau virtuel**: choisissez hello région le plus proche tooyour les utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="ff34c-156">**Region/Affinity Group/Virtual Network**: Choose hello region closest tooyour end users.</span></span>
   * <span data-ttu-id="ff34c-157">**Compte de stockage**: utilisez un compte de stockage généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ff34c-157">**Storage Account**: Use an automatically generated storage account.</span></span>
   * <span data-ttu-id="ff34c-158">**Groupe à haute disponibilité**: Aucun.</span><span class="sxs-lookup"><span data-stu-id="ff34c-158">**Availability Set**: None.</span></span>
   * <span data-ttu-id="ff34c-159">**Points de terminaison** conserver hello **Bureau à distance** et **PowerShell** points de terminaison, puis ajoutez le point de terminaison HTTP ou HTTPS, selon votre environnement.</span><span class="sxs-lookup"><span data-stu-id="ff34c-159">**ENDPOINTS** Keep hello **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span></span>
     
     * <span data-ttu-id="ff34c-160">**HTTP**: hello par défaut des ports publics et privés sont **80**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-160">**HTTP**: hello default public and private ports are **80**.</span></span> <span data-ttu-id="ff34c-161">Notez que si vous utilisez un port privé autre que 80, modifiez **$HTTPport = 80** dans le script de http hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in hello http script.</span></span>
     * <span data-ttu-id="ff34c-162">**HTTPS**: hello par défaut des ports publics et privés sont **443**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-162">**HTTPS**: hello default public and private ports are **443**.</span></span> <span data-ttu-id="ff34c-163">Meilleure pratique de sécurité est un port privé toochange hello et configurer votre pare-feu et hello report server toouse hello port privé.</span><span class="sxs-lookup"><span data-stu-id="ff34c-163">A security best practice is toochange hello private port and configure your firewall and hello report server toouse hello private port.</span></span> <span data-ttu-id="ff34c-164">Pour plus d’informations sur les points de terminaison, consultez [comment configurer la Communication avec un ordinateur virtuel de tooSet](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ff34c-164">For more information on endpoints, see [How tooSet Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="ff34c-165">Notez que si vous utilisez un port autre que 443, modifiez le paramètre hello **$HTTPsport = 443** Bonjour script HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ff34c-165">Note that if you use a port other than 443, change hello parameter **$HTTPsport = 443** in hello HTTPS script.</span></span>
   * <span data-ttu-id="ff34c-166">Cliquez sur suivant.</span><span class="sxs-lookup"><span data-stu-id="ff34c-166">Click next .</span></span> ![Suivant](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. <span data-ttu-id="ff34c-168">Dans hello dernière page de l’Assistant de hello, conservez par défaut de hello **installer l’agent de machine virtuelle hello** sélectionné.</span><span class="sxs-lookup"><span data-stu-id="ff34c-168">On hello last page of hello wizard, keep hello default **Install hello VM agent** selected.</span></span> <span data-ttu-id="ff34c-169">Hello étapes décrites dans cette rubrique n’utilisent pas l’agent de machine virtuelle hello, mais si vous envisagez de tookeep cet ordinateur virtuel, agent de machine virtuelle hello et extensions vous permettra de tooenhance he CM.</span><span class="sxs-lookup"><span data-stu-id="ff34c-169">hello steps in this topic do not utilize hello VM agent but if you plan tookeep this VM, hello VM agent and extensions will allow you tooenhance he CM.</span></span>  <span data-ttu-id="ff34c-170">Pour plus d’informations sur l’agent de machine virtuelle hello, consultez [Agent de machine virtuelle et Extensions – partie 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span><span class="sxs-lookup"><span data-stu-id="ff34c-170">For more information on hello VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span></span> <span data-ttu-id="ff34c-171">L’un de l’annonce d’extensions installées par défaut hello en cours d’exécution est extension hello « BGINFO » qui s’affiche sur le bureau de machine virtuelle hello, espace de lecteur informations système telles que de l’adresse IP interne et libre.</span><span class="sxs-lookup"><span data-stu-id="ff34c-171">One of hello default extensions installed ad running is hello “BGINFO” extension that displays on hello VM desktop, system information such as internal IP and free drive space.</span></span>
9. <span data-ttu-id="ff34c-172">Cliquez Terminé .</span><span class="sxs-lookup"><span data-stu-id="ff34c-172">Click complete .</span></span> ![OK](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. <span data-ttu-id="ff34c-174">Hello **état** de machine virtuelle affiche sous la forme de hello **départ (Provisioning)** au cours de processus de fourniture de hello, puis en tant que **en cours d’exécution** lorsque hello machine virtuelle est configurée et prête toouse.</span><span class="sxs-lookup"><span data-stu-id="ff34c-174">hello **Status** of hello VM displays as **Starting (Provisioning)** during hello provision process and then displays as **Running** when hello VM is provisioned and ready toouse.</span></span>

## <a name="step-2-create-a-server-certificate"></a><span data-ttu-id="ff34c-175">Étape 2 : Créer un certificat de serveur</span><span class="sxs-lookup"><span data-stu-id="ff34c-175">Step 2: Create a Server Certificate</span></span>
> [!NOTE]
> <span data-ttu-id="ff34c-176">Si vous n’avez pas besoin de HTTPS sur le serveur de rapports hello, vous pouvez **ignorez l’étape 2** et consultez la section de toohello **utiliser HTTP et le serveur de rapports de script tooconfigure hello**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-176">If you do not require HTTPS on hello report server, you can **skip step 2** and go toohello section **Use script tooconfigure hello report server and HTTP**.</span></span> <span data-ttu-id="ff34c-177">Utilisez hello HTTP script tooquickly configurer le serveur de rapports hello et rapport hello serveur sera prêt toouse.</span><span class="sxs-lookup"><span data-stu-id="ff34c-177">Use hello HTTP script tooquickly configure hello report server and hello report server will be ready toouse.</span></span>

<span data-ttu-id="ff34c-178">Dans l’ordre toouse HTTPS sur hello machine virtuelle, vous devez un certificat SSL approuvé.</span><span class="sxs-lookup"><span data-stu-id="ff34c-178">In order toouse HTTPS on hello VM, you need a trusted SSL certificate.</span></span> <span data-ttu-id="ff34c-179">Selon votre scénario, vous pouvez utiliser une des deux méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="ff34c-179">Depending on your scenario, you can use one of hello following two methods:</span></span>

* <span data-ttu-id="ff34c-180">Un certificat SSL valide émis par une autorité de certification et approuvé par Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ff34c-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span></span> <span data-ttu-id="ff34c-181">certificats de Hello autorité de certification racine sont requis toobe distribué via hello programme de certificat racine Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ff34c-181">hello CA root certificates are required toobe distributed via hello Microsoft Root Certificate Program.</span></span> <span data-ttu-id="ff34c-182">Pour plus d’informations sur ce programme, consultez [Windows et Windows Phone 8 SSL Root Certificate Program (autorités de certification membres)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) et [Introduction toohello programme de certificat racine Microsoft](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff34c-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction toohello Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span></span>
* <span data-ttu-id="ff34c-183">Un certificat auto-signé.</span><span class="sxs-lookup"><span data-stu-id="ff34c-183">A self-signed certificate.</span></span> <span data-ttu-id="ff34c-184">Les certificats auto-signés sont déconseillés pour les environnements de production.</span><span class="sxs-lookup"><span data-stu-id="ff34c-184">Self-signed certificates are not recommended for production environments.</span></span>

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a><span data-ttu-id="ff34c-185">toouse un certificat créé par une autorité de certificat approuvé (CA)</span><span class="sxs-lookup"><span data-stu-id="ff34c-185">toouse a certificate created by a trusted Certificate Authority (CA)</span></span>
1. <span data-ttu-id="ff34c-186">**Demander un certificat de serveur pour le site Web de hello à partir d’une autorité de certification**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-186">**Request a server certificate for hello website from a certification authority**.</span></span> 
   
    <span data-ttu-id="ff34c-187">Vous pouvez utiliser hello Assistant certificat de serveur Web soit toogenerate un fichier de demande de certificat (Certreq.txt) que vous envoyez autorité de certification tooa ou toogenerate une demande pour une autorité de certification en ligne.</span><span class="sxs-lookup"><span data-stu-id="ff34c-187">You can use hello Web Server Certificate Wizard either toogenerate a certificate request file (Certreq.txt) that you send tooa certification authority, or toogenerate a request for an online certification authority.</span></span> <span data-ttu-id="ff34c-188">Par exemple, les services de certificats Microsoft dans Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="ff34c-188">For example, Microsoft Certificate Services in Windows Server 2012.</span></span> <span data-ttu-id="ff34c-189">Selon le niveau d’assurance d’identification proposé par votre certificat de serveur hello est plusieurs mois de tooseveral jours pour tooapprove d’autorité de certification hello votre demande et envoi d’un fichier de certificat.</span><span class="sxs-lookup"><span data-stu-id="ff34c-189">Depending on hello level of identification assurance offered by your server certificate, it is several days tooseveral months for hello certification authority tooapprove your request and send you a certificate file.</span></span> 
   
    <span data-ttu-id="ff34c-190">Pour plus d’informations sur la demande d’un certificat de serveur, voir hello :</span><span class="sxs-lookup"><span data-stu-id="ff34c-190">For more information about requesting a server certificates, see hello following:</span></span> 
   
   * <span data-ttu-id="ff34c-191">Utiliser [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff34c-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span></span>
   * <span data-ttu-id="ff34c-192">TooAdminister d’outils de sécurité Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="ff34c-192">Security Tools tooAdminister Windows Server 2012.</span></span>
     
     [<span data-ttu-id="ff34c-193">Outils de sécurité tooAdminister Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="ff34c-193">Security Tools tooAdminister Windows Server 2012</span></span>](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > <span data-ttu-id="ff34c-194">Hello **délivré à** champ Hello approuvé le certificat SSL doit être hello même comme hello **nom DNS du Service Cloud** vous avez utilisé pour hello nouvelle machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ff34c-194">hello **issued to** field of hello trusted SSL certificate should be hello same as hello **Cloud Service DNS NAME** you used for hello new VM.</span></span>

2. <span data-ttu-id="ff34c-195">**Installer le certificat de serveur hello sur le serveur Web de hello**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-195">**Install hello server certificate on hello Web server**.</span></span> <span data-ttu-id="ff34c-196">Dans ce cas, serveur Web de Hello est hello VM que hôtes hello serveur de rapports et le site Web de hello est créé dans les étapes ultérieures lorsque vous configurez Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="ff34c-196">hello Web server in this case is hello VM that hosts hello report server and hello website is created in later steps when you configure Reporting Services.</span></span> <span data-ttu-id="ff34c-197">Pour plus d’informations sur l’installation du certificat de serveur hello sur le serveur Web de hello en utilisant le composant logiciel enfichable MMC certificat hello, consultez [installer un certificat de serveur](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="ff34c-197">For more information about installing hello server certificate on hello Web server by using hello Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
    <span data-ttu-id="ff34c-198">Si vous voulez toouse hello script est inclus dans cette rubrique, le serveur de rapports tooconfigure hello, hello valeur des certificats de hello **l’empreinte numérique** est requis en tant que paramètre du script de hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-198">If you want toouse hello script included with this topic, tooconfigure hello report server, hello value of hello certificates **Thumbprint** is required as a parameter of hello script.</span></span> <span data-ttu-id="ff34c-199">Voir section suivante de hello pour plus d’informations sur la façon dont tooobtain hello empreinte numérique du certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-199">See hello next section for details on how tooobtain hello thumbprint of hello certificate.</span></span>
3. <span data-ttu-id="ff34c-200">Affecter hello certificat toohello de rapports server.</span><span class="sxs-lookup"><span data-stu-id="ff34c-200">Assign hello server certificate toohello report server.</span></span> <span data-ttu-id="ff34c-201">Hello s’effectue dans la section suivante de hello lorsque vous configurez le serveur de rapports hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-201">hello assignment is completed in hello next section when you configure hello report server.</span></span>

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a><span data-ttu-id="ff34c-202">toouse hello un certificat auto-signé Machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="ff34c-202">toouse hello Virtual Machines Self-signed Certificate</span></span>
<span data-ttu-id="ff34c-203">Un certificat auto-signé a été créé sur la machine virtuelle de hello hello machine virtuelle a été configuré.</span><span class="sxs-lookup"><span data-stu-id="ff34c-203">A self-signed certificate was created on hello VM when hello VM was provisioned.</span></span> <span data-ttu-id="ff34c-204">certificat de Hello a hello comme hello nom VM DNS du même nom.</span><span class="sxs-lookup"><span data-stu-id="ff34c-204">hello certificate has hello same name as hello VM DNS name.</span></span> <span data-ttu-id="ff34c-205">Des erreurs de certificat ordre tooavoid, il est nécessaire que le certificat hello est approuvé sur hello machine virtuelle proprement dite, ainsi que par tous les utilisateurs du site de hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-205">In order tooavoid certificate errors, it is required that hello certificate is trusted on hello VM itself, and also by all users of hello site.</span></span>

1. <span data-ttu-id="ff34c-206">autorité de certification de racine de hello tootrust du certificat hello sur hello Local de machine virtuelle, ajoutez hello certificat toohello **autorités de Certification racines de confiance**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-206">tootrust hello root CA of hello certificate on hello Local VM, add hello certificate toohello **Trusted Root Certification Authorities**.</span></span> <span data-ttu-id="ff34c-207">Hello Voici un résumé des étapes hello requises.</span><span class="sxs-lookup"><span data-stu-id="ff34c-207">hello following is a summary of hello steps required.</span></span> <span data-ttu-id="ff34c-208">Pour obtenir des instructions détaillées sur la façon dont tootrust hello autorité de certification, consultez [installer un certificat de serveur](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="ff34c-208">For detailed steps on how tootrust hello CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
   1. <span data-ttu-id="ff34c-209">À partir de hello portail Azure classic, sélectionnez hello machine virtuelle et cliquez sur se connecter.</span><span class="sxs-lookup"><span data-stu-id="ff34c-209">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="ff34c-210">Selon la configuration de votre navigateur, vous pouvez être demandées par invite toosave un fichier .rdp pour la connexion toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ff34c-210">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
      
       ![connecter l’ordinateur virtuel de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="ff34c-212">Utilisez le nom de machine virtuelle hello, nom d’utilisateur et mot de passe configurés lors de la création de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ff34c-212">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
      
       <span data-ttu-id="ff34c-213">Par exemple, Bonjour suivant image, nom d’ordinateur virtuel hello est **ssrsnativecloud** et le nom d’utilisateur hello est **testuser**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-213">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
      
       ![le nom de connexion inclut le nom de la machine virtuelle](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. <span data-ttu-id="ff34c-215">Exécutez mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="ff34c-215">Run mmc.exe.</span></span> <span data-ttu-id="ff34c-216">Pour plus d’informations, consultez [Comment : afficher les certificats avec hello le composant logiciel enfichable MMC](https://msdn.microsoft.com/library/ms788967.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff34c-216">For more information, see [How to: View Certificates with hello MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span></span>
   3. <span data-ttu-id="ff34c-217">Dans l’application de console hello **fichier** menu, ajouter hello **certificats** -composant logiciel enfichable, sélectionnez **compte d’ordinateur** lorsque vous y êtes invité, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-217">In hello console application **File** menu, add hello **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span></span>
   4. <span data-ttu-id="ff34c-218">Sélectionnez **ordinateur Local** toomanage puis cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-218">Select **Local Computer** toomanage and then click **Finish**.</span></span>
   5. <span data-ttu-id="ff34c-219">Cliquez sur **Ok** , puis développez hello **certificats - personnel** nœuds, puis cliquez sur **certificats**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-219">Click **Ok** and then expand hello **Certificates -Personal** nodes and then click **Certificates**.</span></span> <span data-ttu-id="ff34c-220">Hello certificat est nommé d’après le nom DNS hello hello machine virtuelle et se termine par **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-220">hello certificate is named after hello DNS name of hello VM and ends with **cloudapp.net**.</span></span> <span data-ttu-id="ff34c-221">Cliquez sur le nom de certificat hello et cliquez sur **copie**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-221">Right-click hello certificate name and click **Copy**.</span></span>
   6. <span data-ttu-id="ff34c-222">Développez hello **autorités de Certification racines de confiance** nœud et avec le bouton droit puis **certificats** puis cliquez sur **coller**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-222">Expand hello **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span></span>
   7. <span data-ttu-id="ff34c-223">toovalidate, double cliquez sur le nom de certificat hello sous **autorités de Certification racines de confiance** et vérifiez qu’aucun message d’erreur et que vous voyez le certificat.</span><span class="sxs-lookup"><span data-stu-id="ff34c-223">toovalidate, double click on hello certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span></span> <span data-ttu-id="ff34c-224">Si vous voulez toouse hello HTTPS script est inclus dans cette rubrique, le serveur de rapports tooconfigure hello, hello valeur des certificats de hello **l’empreinte numérique** est requis en tant que paramètre du script de hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-224">If you want toouse hello HTTPS script included with this topic, tooconfigure hello report server, hello value of hello certificates **Thumbprint** is required as a parameter of hello script.</span></span> <span data-ttu-id="ff34c-225">**valeur d’empreinte numérique hello tooget**, suivez hello suivantes.</span><span class="sxs-lookup"><span data-stu-id="ff34c-225">**tooget hello thumbprint value**, complete hello following.</span></span> <span data-ttu-id="ff34c-226">Il existe également une empreinte numérique de PowerShell exemple tooretrieve hello dans la section [utiliser le serveur de rapports de script tooconfigure hello et HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span><span class="sxs-lookup"><span data-stu-id="ff34c-226">There is also a PowerShell sample tooretrieve hello thumbprint in section [Use script tooconfigure hello report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span></span>
      
      1. <span data-ttu-id="ff34c-227">Double-cliquez sur nom hello certificat hello, par exemple ssrsnativecloud.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="ff34c-227">Double-click hello name of hello certificate, for example ssrsnativecloud.cloudapp.net.</span></span>
      2. <span data-ttu-id="ff34c-228">Cliquez sur hello **détails** onglet.</span><span class="sxs-lookup"><span data-stu-id="ff34c-228">Click hello **Details** tab.</span></span>
      3. <span data-ttu-id="ff34c-229">Cliquez sur **Empreinte numérique**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-229">Click **Thumbprint**.</span></span> <span data-ttu-id="ff34c-230">valeur de Hello de l’empreinte numérique hello est affichée dans le champ de détails hello, par exemple a6 08 3c df f9 0 b f7 e3 7C 25 ed a4 ed 7e CA 91 9c 2C fb 2f.</span><span class="sxs-lookup"><span data-stu-id="ff34c-230">hello value of hello thumbprint is displayed in hello details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span></span>
      4. <span data-ttu-id="ff34c-231">Copiez l’empreinte numérique hello et enregistrer la valeur de hello pour une date ultérieure ou modifier le script de hello maintenant.</span><span class="sxs-lookup"><span data-stu-id="ff34c-231">Copy hello thumbprint and save hello value for later or edit hello script now.</span></span>
      5. <span data-ttu-id="ff34c-232">(*) Avant d’exécuter les script hello, supprimez les espaces de hello entre les paires de hello de valeurs.</span><span class="sxs-lookup"><span data-stu-id="ff34c-232">(*) Before you run hello script, remove hello spaces in between hello pairs of values.</span></span> <span data-ttu-id="ff34c-233">Par exemple l’empreinte numérique hello indiquée précédemment est maintenant a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span><span class="sxs-lookup"><span data-stu-id="ff34c-233">For example hello thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span></span>
      6. <span data-ttu-id="ff34c-234">Affecter hello certificat toohello de rapports server.</span><span class="sxs-lookup"><span data-stu-id="ff34c-234">Assign hello server certificate toohello report server.</span></span> <span data-ttu-id="ff34c-235">Hello s’effectue dans la section suivante de hello lorsque vous configurez le serveur de rapports hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-235">hello assignment is completed in hello next section when you configure hello report server.</span></span>

<span data-ttu-id="ff34c-236">Si vous utilisez un certificat SSL auto-signé, nom hello sur le certificat de hello correspond déjà hostname hello Hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ff34c-236">If you are using a self-signed SSL certificate, hello name on hello certificate already matches hello hostname of hello VM.</span></span> <span data-ttu-id="ff34c-237">Par conséquent, hello DNS de l’ordinateur de hello est déjà enregistré globalement et sont accessibles à partir de n’importe quel client.</span><span class="sxs-lookup"><span data-stu-id="ff34c-237">Therefore, hello DNS of hello machine is already registered globally and can be accessed from any client.</span></span>

## <a name="step-3-configure-hello-report-server"></a><span data-ttu-id="ff34c-238">Étape 3 : Configurer le serveur de rapports de hello</span><span class="sxs-lookup"><span data-stu-id="ff34c-238">Step 3: Configure hello Report Server</span></span>
<span data-ttu-id="ff34c-239">Cette section vous guide tout au long de la configuration de hello machine virtuelle comme un serveur de rapports Reporting Services en mode natif.</span><span class="sxs-lookup"><span data-stu-id="ff34c-239">This section walks you through configuring hello VM as a Reporting Services native mode report server.</span></span> <span data-ttu-id="ff34c-240">Vous pouvez utiliser une des hello suivant du serveur de rapports de méthodes tooconfigure hello :</span><span class="sxs-lookup"><span data-stu-id="ff34c-240">You can use one of hello following methods tooconfigure hello report server:</span></span>

* <span data-ttu-id="ff34c-241">Utiliser le serveur de rapports hello script tooconfigure hello</span><span class="sxs-lookup"><span data-stu-id="ff34c-241">Use hello script tooconfigure hello report server</span></span>
* <span data-ttu-id="ff34c-242">Utilisez le Gestionnaire de Configuration tooConfigure hello serveur de rapports.</span><span class="sxs-lookup"><span data-stu-id="ff34c-242">Use Configuration Manager tooConfigure hello Report Server.</span></span>

<span data-ttu-id="ff34c-243">Pour plus d’étapes, consultez la section de hello [Connect toohello Machine virtuelle et démarrer hello Gestionnaire de Configuration de Reporting Services](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="ff34c-243">For more detailed steps, see hello section [Connect toohello Virtual Machine and Start hello Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span></span>

<span data-ttu-id="ff34c-244">**Remarque sur l’authentification :** l’authentification Windows est hello, méthode d’authentification recommandée et authentification de Reporting Services par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-244">**Authentication Note:** Windows authentication is hello recommended authentication method and it is hello default Reporting Services authentication.</span></span> <span data-ttu-id="ff34c-245">Seuls les utilisateurs qui sont configurés sur la machine virtuelle de hello peuvent accéder aux Services de création de rapports et attribué des rôles Services tooReporting.</span><span class="sxs-lookup"><span data-stu-id="ff34c-245">Only users that are configured on hello VM can access Reporting Services and assigned tooReporting Services roles.</span></span>

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a><span data-ttu-id="ff34c-246">Utiliser le serveur de rapports de script tooconfigure hello et HTTP</span><span class="sxs-lookup"><span data-stu-id="ff34c-246">Use script tooconfigure hello report server and HTTP</span></span>
<span data-ttu-id="ff34c-247">toouse hello Windows PowerShell script tooconfigure hello serveur de rapports, hello complète comme suit.</span><span class="sxs-lookup"><span data-stu-id="ff34c-247">toouse hello Windows PowerShell script tooconfigure hello report server, complete hello following steps.</span></span> <span data-ttu-id="ff34c-248">configuration de Hello inclut le protocole HTTP, HTTPS pas :</span><span class="sxs-lookup"><span data-stu-id="ff34c-248">hello configuration includes HTTP, not HTTPS:</span></span>

1. <span data-ttu-id="ff34c-249">À partir de hello portail Azure classic, sélectionnez hello machine virtuelle et cliquez sur se connecter.</span><span class="sxs-lookup"><span data-stu-id="ff34c-249">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="ff34c-250">Selon la configuration de votre navigateur, vous pouvez être demandées par invite toosave un fichier .rdp pour la connexion toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ff34c-250">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
   
    ![connecter l’ordinateur virtuel de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="ff34c-252">Utilisez le nom de machine virtuelle hello, nom d’utilisateur et mot de passe configurés lors de la création de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ff34c-252">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
   
    <span data-ttu-id="ff34c-253">Par exemple, Bonjour suivant image, nom d’ordinateur virtuel hello est **ssrsnativecloud** et le nom d’utilisateur hello est **testuser**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-253">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
   
    ![le nom de connexion inclut le nom de la machine virtuelle](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="ff34c-255">Sur la machine virtuelle de hello, ouvrez **Windows PowerShell ISE** avec des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ff34c-255">On hello VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="ff34c-256">Hello PowerShell ISE est installé par défaut sur Windows server 2012.</span><span class="sxs-lookup"><span data-stu-id="ff34c-256">hello PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="ff34c-257">Il est recommandé de qu'utiliser hello ISE plutôt qu’une fenêtre Windows PowerShell standard afin que vous pouvez coller le script de hello hello ISE, modifiez le script de hello et puis exécutez le script de hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-257">It is recommended you use hello ISE instead of a standard Windows PowerShell window so that you can paste hello script into hello ISE, modify hello script, and then run hello script.</span></span>
3. <span data-ttu-id="ff34c-258">Dans Windows PowerShell ISE, cliquez sur hello **vue** menu, puis sur **afficher le volet Script**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-258">In Windows PowerShell ISE, click hello **View** menu and then click **Show Script Pane**.</span></span>
4. <span data-ttu-id="ff34c-259">Hello script suivant de copier et coller le script de hello dans le volet de script Windows PowerShell ISE hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-259">Copy hello following script, and paste hello script into hello Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
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
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
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
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
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
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
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
5. <span data-ttu-id="ff34c-260">Si vous avez créé hello machine virtuelle avec un port HTTP autre que 80, modifiez le paramètre hello $HTTPport = 80.</span><span class="sxs-lookup"><span data-stu-id="ff34c-260">If you created hello VM with an HTTP port other than 80, modify hello parameter $HTTPport = 80.</span></span>
6. <span data-ttu-id="ff34c-261">Hello script est actuellement configuré pour Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="ff34c-261">hello script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="ff34c-262">Si vous souhaitez le script de hello toorun pour Reporting Services, modifier trop partie de version hello d’espace de noms toohello hello chemin d’accès « v11 » sur l’instruction de hello Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="ff34c-262">If you want toorun hello script for  Reporting Services, modify hello version portion of hello path toohello namespace too“v11”, on hello Get-WmiObject statement.</span></span>
7. <span data-ttu-id="ff34c-263">Exécutez le script de hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-263">Run hello script.</span></span>

<span data-ttu-id="ff34c-264">**Validation**: tooverify fonctionnalités du serveur de rapports de base hello fonctionnent, consultez hello [configuration de hello Vérifiez](#verify-the-configuration) section plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="ff34c-264">**Validation**: tooverify that hello basic report server functionality is working, see hello [Verify hello configuration](#verify-the-configuration) section later in this topic.</span></span>

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a><span data-ttu-id="ff34c-265">Utiliser le serveur de rapports de script tooconfigure hello et HTTPS</span><span class="sxs-lookup"><span data-stu-id="ff34c-265">Use script tooconfigure hello report server and HTTPS</span></span>
<span data-ttu-id="ff34c-266">toouse Windows PowerShell tooconfigure hello serveur de rapports, hello complète comme suit.</span><span class="sxs-lookup"><span data-stu-id="ff34c-266">toouse Windows PowerShell tooconfigure hello report server, complete hello following steps.</span></span> <span data-ttu-id="ff34c-267">configuration de Hello inclut le protocole HTTPS, non HTTP.</span><span class="sxs-lookup"><span data-stu-id="ff34c-267">hello configuration includes HTTPS, not HTTP.</span></span>

1. <span data-ttu-id="ff34c-268">À partir de hello portail Azure classic, sélectionnez hello machine virtuelle et cliquez sur se connecter.</span><span class="sxs-lookup"><span data-stu-id="ff34c-268">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="ff34c-269">Selon la configuration de votre navigateur, vous pouvez être demandées par invite toosave un fichier .rdp pour la connexion toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ff34c-269">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
   
    ![connecter l’ordinateur virtuel de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="ff34c-271">Utilisez le nom de machine virtuelle hello, nom d’utilisateur et mot de passe configurés lors de la création de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ff34c-271">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
   
    <span data-ttu-id="ff34c-272">Par exemple, Bonjour suivant image, nom d’ordinateur virtuel hello est **ssrsnativecloud** et le nom d’utilisateur hello est **testuser**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-272">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
   
    ![le nom de connexion inclut le nom de la machine virtuelle](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="ff34c-274">Sur la machine virtuelle de hello, ouvrez **Windows PowerShell ISE** avec des privilèges d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="ff34c-274">On hello VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="ff34c-275">Hello PowerShell ISE est installé par défaut sur Windows server 2012.</span><span class="sxs-lookup"><span data-stu-id="ff34c-275">hello PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="ff34c-276">Il est recommandé de qu'utiliser hello ISE plutôt qu’une fenêtre Windows PowerShell standard afin que vous pouvez coller le script de hello hello ISE, modifiez le script de hello et puis exécutez le script de hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-276">It is recommended you use hello ISE instead of a standard Windows PowerShell window so that you can paste hello script into hello ISE, modify hello script, and then run hello script.</span></span>
3. <span data-ttu-id="ff34c-277">tooenable en cours d’exécution des scripts, exécutez hello commande de Windows PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="ff34c-277">tooenable running scripts, run hello following Windows PowerShell command:</span></span>
   
        Set-ExecutionPolicy RemoteSigned
   
    <span data-ttu-id="ff34c-278">Vous pouvez ensuite exécuter hello suivant la stratégie de hello tooverify :</span><span class="sxs-lookup"><span data-stu-id="ff34c-278">You can then run hello following tooverify hello policy:</span></span>
   
        Get-ExecutionPolicy
4. <span data-ttu-id="ff34c-279">Dans **Windows PowerShell ISE**, cliquez sur hello **vue** menu, puis sur **afficher le volet Script**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-279">In **Windows PowerShell ISE**, click hello **View** menu and then click **Show Script Pane**.</span></span>
5. <span data-ttu-id="ff34c-280">Copiez hello suivants de script et collez-le dans le volet de script Windows PowerShell ISE hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-280">Copy hello following script and paste it into hello Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
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
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
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
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
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
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
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
6. <span data-ttu-id="ff34c-281">Modifier hello **$certificatehash** paramètre hello script :</span><span class="sxs-lookup"><span data-stu-id="ff34c-281">Modify hello **$certificatehash** parameter in hello script:</span></span>
   
   * <span data-ttu-id="ff34c-282">Il s’agit d’un paramètre **obligatoire** .</span><span class="sxs-lookup"><span data-stu-id="ff34c-282">This is a **required** parameter.</span></span> <span data-ttu-id="ff34c-283">Si vous n’avez pas enregistré la valeur du certificat hello des étapes précédentes de hello, utilisez une de hello suivant la valeur de hachage du certificat hello toocopy méthodes à partir de l’empreinte numérique des certificats hello. :</span><span class="sxs-lookup"><span data-stu-id="ff34c-283">If you did not save hello certificate value from hello previous steps, use one of hello following methods toocopy hello certificate hash value from hello certificates thumbprint.:</span></span>
     
       <span data-ttu-id="ff34c-284">Sur hello machine virtuelle, ouvrez Windows PowerShell ISE et exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ff34c-284">On hello VM, open Windows PowerShell ISE and run hello following command:</span></span>
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       <span data-ttu-id="ff34c-285">sortie de Hello recherche similaire toohello suivant.</span><span class="sxs-lookup"><span data-stu-id="ff34c-285">hello output will look similar toohello following.</span></span> <span data-ttu-id="ff34c-286">Si le script de hello renvoie une ligne vide, hello machine virtuelle n’a pas d’un certificat configuré par exemple, consultez la section de hello [toouse hello un certificat auto-signé Machines virtuelles](#to-use-the-virtual-machines-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="ff34c-286">If hello script returns a blank line, hello VM does not have a certificate configured for example, see hello section [toouse hello Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span></span>
     
     <span data-ttu-id="ff34c-287">OU</span><span class="sxs-lookup"><span data-stu-id="ff34c-287">OR</span></span>
   * <span data-ttu-id="ff34c-288">Hello de machine virtuelle, exécutez le mmc.exe et puis ajoutez hello **certificats** enfichable.</span><span class="sxs-lookup"><span data-stu-id="ff34c-288">On hello VM Run mmc.exe and then add hello **Certificates** snap-in.</span></span>
   * <span data-ttu-id="ff34c-289">Sous hello **autorités de certification racine de confiance** nœud double-cliquez sur le nom du certificat.</span><span class="sxs-lookup"><span data-stu-id="ff34c-289">Under hello **Trusted Root Certificate Authorities** node double-click your certificate name.</span></span> <span data-ttu-id="ff34c-290">Si vous utilisez un certificat auto-signé de hello Hello machine virtuelle, les certificats hello est nommé d’après le nom DNS hello hello machine virtuelle et se termine par **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-290">If you are using hello self-signed certificate of hello VM, hello certificate is named after hello DNS name of hello VM and ends with **cloudapp.net**.</span></span>
   * <span data-ttu-id="ff34c-291">Cliquez sur hello **détails** onglet.</span><span class="sxs-lookup"><span data-stu-id="ff34c-291">Click hello **Details** tab.</span></span>
   * <span data-ttu-id="ff34c-292">Cliquez sur **Empreinte numérique**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-292">Click **Thumbprint**.</span></span> <span data-ttu-id="ff34c-293">valeur de Hello de l’empreinte numérique hello est affichée dans le champ de détails hello, par exemple af 11 60 b6 4 b 28 8 d 89 0 a 82 12 ff 6 b a9 c3 66 4f 31 90 48</span><span class="sxs-lookup"><span data-stu-id="ff34c-293">hello value of hello thumbprint is displayed in hello details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span></span>
   * <span data-ttu-id="ff34c-294">**Avant d’exécuter les script hello**, supprimer les espaces entre les paires de hello de valeurs hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-294">**Before you run hello script**, remove hello spaces in between hello pairs of values.</span></span> <span data-ttu-id="ff34c-295">Par exemple af1160b64b288d890a8212ff6ba9c3664f319048</span><span class="sxs-lookup"><span data-stu-id="ff34c-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span></span>
7. <span data-ttu-id="ff34c-296">Modifier hello **$httpsport** paramètre :</span><span class="sxs-lookup"><span data-stu-id="ff34c-296">Modify hello **$httpsport** parameter:</span></span> 
   
   * <span data-ttu-id="ff34c-297">Si vous avez utilisé le port 443 pour le point de terminaison HTTPS hello, puis il est inutile tooupdate ce paramètre dans le script de hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-297">If you used port 443 for hello HTTPS endpoint, then you do not need tooupdate this parameter in hello script.</span></span> <span data-ttu-id="ff34c-298">Sinon, utilisez vous avez sélectionné lorsque vous avez configuré le point de terminaison privé hello HTTPS sur hello machine virtuelle de la valeur du port hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-298">Otherwise use hello port value you selected when you configured hello HTTPS private endpoint on hello VM.</span></span>
8. <span data-ttu-id="ff34c-299">Modifier hello **$DNSName** paramètre :</span><span class="sxs-lookup"><span data-stu-id="ff34c-299">Modify hello **$DNSName** parameter:</span></span> 
   
   * <span data-ttu-id="ff34c-300">script de Hello est configuré pour un certificat de caractère générique $DNSName = « + ».</span><span class="sxs-lookup"><span data-stu-id="ff34c-300">hello script is configured for a wild card certificate $DNSName="+".</span></span> <span data-ttu-id="ff34c-301">Si vous ne procédez à aucune tooconfigure que vous souhaitez pour une liaison de certificat avec caractères génériques, commentez $DNSName = « + « et activez hello suivant la ligne, référence $DNSNAme complète de hello, ## $DNSName="$server.cloudapp.net ».</span><span class="sxs-lookup"><span data-stu-id="ff34c-301">If you do no want tooconfigure for a wildcard certificate binding, comment out $DNSName="+" and enable hello following line, hello full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span></span>
     
       <span data-ttu-id="ff34c-302">Modifiez la valeur de hello $DNSName si vous ne souhaitez pas le nom DNS de l’ordinateur virtuel toouse hello pour Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="ff34c-302">Change hello $DNSName value if you do not want toouse hello virtual machine’s DNS name for Reporting Services.</span></span> <span data-ttu-id="ff34c-303">Si vous utilisez le paramètre hello, hello certificat doit également utiliser ce nom et vous inscrivez nom hello globalement sur un serveur DNS.</span><span class="sxs-lookup"><span data-stu-id="ff34c-303">If you use hello parameter, hello certificate must also use this name and you register hello name globally on a DNS server.</span></span>
9. <span data-ttu-id="ff34c-304">Hello script est actuellement configuré pour Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="ff34c-304">hello script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="ff34c-305">Si vous souhaitez le script de hello toorun pour Reporting Services, modifier trop partie de version hello d’espace de noms toohello hello chemin d’accès « v11 » sur l’instruction de hello Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="ff34c-305">If you want toorun hello script for  Reporting Services, modify hello version portion of hello path toohello namespace too“v11”, on hello Get-WmiObject statement.</span></span>
10. <span data-ttu-id="ff34c-306">Exécutez le script de hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-306">Run hello script.</span></span>

<span data-ttu-id="ff34c-307">**Validation**: tooverify fonctionnalités du serveur de rapports de base hello fonctionnent, consultez hello [configuration de hello Vérifiez](#verify-the-connection) section plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="ff34c-307">**Validation**: tooverify that hello basic report server functionality is working, see hello [Verify hello configuration](#verify-the-connection) section later in this topic.</span></span> <span data-ttu-id="ff34c-308">liaison de certificat tooverify hello ouvrir une invite de commandes avec des privilèges d’administrateur et puis exécutez hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ff34c-308">tooverify hello certificate binding open a command prompt with administrative privileges, and then run hello following command:</span></span>

    netsh http show sslcert

<span data-ttu-id="ff34c-309">résultat de Hello inclura hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="ff34c-309">hello result will include hello following:</span></span>

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a><span data-ttu-id="ff34c-310">Utilisez le Gestionnaire de Configuration tooConfigure hello serveur de rapports</span><span class="sxs-lookup"><span data-stu-id="ff34c-310">Use Configuration Manager tooConfigure hello Report Server</span></span>
<span data-ttu-id="ff34c-311">Si vous ne souhaitez pas de serveur de rapports toorun hello PowerShell script tooconfigure hello, suivez les étapes de hello dans cette section toouse hello Reporting Services en mode natif configuration manager tooconfigure hello serveur de rapports.</span><span class="sxs-lookup"><span data-stu-id="ff34c-311">If you do not want toorun hello PowerShell script tooconfigure hello report server, follow hello steps in this section toouse hello Reporting Services native mode configuration manager tooconfigure hello report server.</span></span>

1. <span data-ttu-id="ff34c-312">À partir de hello portail Azure classic, sélectionnez hello machine virtuelle et cliquez sur se connecter.</span><span class="sxs-lookup"><span data-stu-id="ff34c-312">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="ff34c-313">Utilisez le nom d’utilisateur hello et mot de passe configurés lors de la création de hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ff34c-313">Use hello user name and password you configured when you created hello VM.</span></span>
   
    ![connecter l’ordinateur virtuel de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. <span data-ttu-id="ff34c-315">Exécutez Windows update et installez les mises à jour toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ff34c-315">Run Windows update and install updates toohello VM.</span></span> <span data-ttu-id="ff34c-316">Si un redémarrage de hello machine virtuelle est nécessaire, redémarrez hello machine virtuelle et se reconnecter toohello machine virtuelle à partir de hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="ff34c-316">If a restart of hello VM is required, restart hello VM and reconnect toohello VM from hello Azure classic portal.</span></span>
3. <span data-ttu-id="ff34c-317">À partir du menu Démarrer hello hello machine virtuelle, tapez **Reporting Services** et ouvrez **Gestionnaire de Configuration de Reporting Services**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-317">From hello Start menu on hello VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span></span>
4. <span data-ttu-id="ff34c-318">Laissez les valeurs par défaut de hello **nom du serveur** et **Instance de serveur de rapports**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-318">Leave hello default values for **Server Name** and **Report Server Instance**.</span></span> <span data-ttu-id="ff34c-319">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-319">Click **Connect**.</span></span>
5. <span data-ttu-id="ff34c-320">Dans le volet gauche de hello, cliquez sur **URL du Service Web**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-320">In hello left pane, click **Web Service URL**.</span></span>
6. <span data-ttu-id="ff34c-321">Par défaut, Reporting Services est configuré pour le port HTTP 80 avec l’adresse IP « entièrement affectée ».</span><span class="sxs-lookup"><span data-stu-id="ff34c-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span></span> <span data-ttu-id="ff34c-322">tooadd HTTPS :</span><span class="sxs-lookup"><span data-stu-id="ff34c-322">tooadd HTTPS:</span></span>
   
   1. <span data-ttu-id="ff34c-323">Dans **certificat SSL**: hello select certificat toouse, par exemple [nom de la machine virtuelle]. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="ff34c-323">In **SSL Certificate**: select hello certificate you want toouse, for example [VM name].cloudapp.net.</span></span> <span data-ttu-id="ff34c-324">Si aucun certificat n’est répertorié, consultez la section de hello **étape 2 : créer un certificat de serveur** pour plus d’informations sur comment tooinstall et approbation hello certificat sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ff34c-324">If no certificates are listed, see hello section **Step 2: Create a Server Certificate** for information on how tooinstall and trust hello certificate on hello VM.</span></span>
   2. <span data-ttu-id="ff34c-325">Sous **Port SSL**: sélectionnez 443.</span><span class="sxs-lookup"><span data-stu-id="ff34c-325">Under **SSL Port**: choose 443.</span></span> <span data-ttu-id="ff34c-326">Si vous avez configuré le point de terminaison privé hello HTTPS Bonjour machine virtuelle avec un autre port privé, utilisez cette valeur ici.</span><span class="sxs-lookup"><span data-stu-id="ff34c-326">If you configured hello HTTPS private endpoint in hello VM with a different private port, use that value here.</span></span>
   3. <span data-ttu-id="ff34c-327">Cliquez sur **appliquer** et attendez hello opération toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ff34c-327">Click **Apply** and wait for hello operation toocomplete.</span></span>
7. <span data-ttu-id="ff34c-328">Dans le volet gauche de hello, cliquez sur **base de données**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-328">In hello left pane, click **Database**.</span></span>
   
   1. <span data-ttu-id="ff34c-329">Cliquez sur **Changer la base de données**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-329">Click **Change Databas**e.</span></span>
   2. <span data-ttu-id="ff34c-330">Cliquez sur **Créer une nouvelle base de données de serveur de rapports**, puis sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-330">Click **Create a new report server database** and then click **Next**.</span></span>
   3. <span data-ttu-id="ff34c-331">Laissez la valeur par défaut hello **nom du serveur**: hello machine virtuelle sous la forme nom et laissez la valeur par défaut hello **Type d’authentification** en tant que **utilisateur actuel** – **lasécuritéintégrée**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-331">Leave hello default **Server Name**: as hello VM name and leave hello default **Authentication Type** as **Current User** – **Integrated Security**.</span></span> <span data-ttu-id="ff34c-332">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-332">Click **Next**.</span></span>
   4. <span data-ttu-id="ff34c-333">Laissez la valeur par défaut hello **nom de la base de données** en tant que **ReportServer** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-333">Leave hello default **Database Name** as **ReportServer** and click **Next**.</span></span>
   5. <span data-ttu-id="ff34c-334">Laissez la valeur par défaut hello **Type d’authentification** en tant que **informations d’identification du Service** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-334">Leave hello default **Authentication Type** as **Service Credentials** and click **Next**.</span></span>
   6. <span data-ttu-id="ff34c-335">Cliquez sur **suivant** sur hello **Résumé** page.</span><span class="sxs-lookup"><span data-stu-id="ff34c-335">Click **Next** on hello **Summary** page.</span></span>
   7. <span data-ttu-id="ff34c-336">Lors de la configuration de hello est terminée, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-336">When hello configuration is complete, click **Finish**.</span></span>
8. <span data-ttu-id="ff34c-337">Dans le volet gauche de hello, cliquez sur **URL du Gestionnaire de rapports**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-337">In hello left pane, click **Report Manager URL**.</span></span> <span data-ttu-id="ff34c-338">Laissez la valeur par défaut hello **répertoire virtuel** en tant que **rapports** et cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="ff34c-338">Leave hello default **Virtual Directory** as **Reports** and click **Apply**.</span></span>
9. <span data-ttu-id="ff34c-339">Cliquez sur **Exit** tooclose hello Gestionnaire de Configuration de Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="ff34c-339">Click **Exit** tooclose hello Reporting Services Configuration Manager.</span></span>

## <a name="step-4-open-windows-firewall-port"></a><span data-ttu-id="ff34c-340">Étape 4 : Ouvrir le port du pare-feu Windows</span><span class="sxs-lookup"><span data-stu-id="ff34c-340">Step 4: Open Windows Firewall Port</span></span>
> [!NOTE]
> <span data-ttu-id="ff34c-341">Si vous avez utilisé un hello scripts tooconfigure hello serveur de rapports, vous pouvez ignorer cette section.</span><span class="sxs-lookup"><span data-stu-id="ff34c-341">If you used one of hello scripts tooconfigure hello report server, you can skip this section.</span></span> <span data-ttu-id="ff34c-342">script de Hello inclus un port de pare-feu étape tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-342">hello script included a step tooopen hello firewall port.</span></span> <span data-ttu-id="ff34c-343">par défaut de Hello est le port 80 pour HTTP et le port 443 pour HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ff34c-343">hello default was port 80 for HTTP and port 443 for HTTPS.</span></span>
> 
> 

<span data-ttu-id="ff34c-344">tooconnect à distance tooReport Manager ou hello rapports Server sur l’ordinateur virtuel de hello, d’un point de terminaison TCP est requis sur hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ff34c-344">tooconnect remotely tooReport Manager or hello Report Server on hello virtual machine, a TCP Endpoint is required on hello VM.</span></span> <span data-ttu-id="ff34c-345">Il est hello tooopen requis même port dans le pare-feu de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-345">It is required tooopen hello same port in hello VM’s firewall.</span></span> <span data-ttu-id="ff34c-346">point de terminaison Hello a été créé lors de la configuration hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ff34c-346">hello endpoint was created when hello VM was provisioned.</span></span>

<span data-ttu-id="ff34c-347">Cette section fournit des informations de base sur la façon dont tooopen hello port de pare-feu.</span><span class="sxs-lookup"><span data-stu-id="ff34c-347">This section provides basic information on how tooopen hello firewall port.</span></span> <span data-ttu-id="ff34c-348">Pour plus d’informations, consultez la page [Configurer un pare-feu pour accéder au serveur de rapports](https://technet.microsoft.com/library/bb934283.aspx)</span><span class="sxs-lookup"><span data-stu-id="ff34c-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="ff34c-349">Si vous avez utilisé le serveur de rapports hello hello script tooconfigure, vous pouvez ignorer cette section.</span><span class="sxs-lookup"><span data-stu-id="ff34c-349">If you used hello script tooconfigure hello report server, you can skip this section.</span></span> <span data-ttu-id="ff34c-350">script de Hello inclus un port de pare-feu étape tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-350">hello script included a step tooopen hello firewall port.</span></span>
> 
> 

<span data-ttu-id="ff34c-351">Si vous avez configuré un port privé pour HTTPS autre que 443, modifiez hello script suivant en conséquence.</span><span class="sxs-lookup"><span data-stu-id="ff34c-351">If you configured a private port for HTTPS other than 443, modify hello following script appropriately.</span></span> <span data-ttu-id="ff34c-352">port de tooopen **443** sur hello pare-feu Windows, suivez suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="ff34c-352">tooopen port **443** on hello Windows Firewall, complete hello following:</span></span>

1. <span data-ttu-id="ff34c-353">Ouvrez une fenêtre Windows PowerShell avec des privilèges administratifs.</span><span class="sxs-lookup"><span data-stu-id="ff34c-353">Open a Windows PowerShell window with administrative privileges.</span></span>
2. <span data-ttu-id="ff34c-354">Si vous avez utilisé un port autre que 443 lorsque vous avez configuré le point de terminaison HTTPS hello sur hello VM, mettre à jour le port hello Bonjour de commande suivante, puis exécutez commande hello :</span><span class="sxs-lookup"><span data-stu-id="ff34c-354">If you used a port other than 443 when you configured hello HTTPS endpoint on hello VM, update hello port in hello following command and then run hello command:</span></span>
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. <span data-ttu-id="ff34c-355">Lors de la commande hello se termine, **Ok** s’affiche dans l’invite de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-355">When hello command completes, **Ok** is displayed in hello command prompt.</span></span>

<span data-ttu-id="ff34c-356">tooverify que le port de hello est ouvert, ouvrez une fenêtre Windows PowerShell et l’exécution hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ff34c-356">tooverify that hello port is opened, open a Windows PowerShell window and run hello following command:</span></span>

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a><span data-ttu-id="ff34c-357">Vérifier la configuration de hello</span><span class="sxs-lookup"><span data-stu-id="ff34c-357">Verify hello configuration</span></span>
<span data-ttu-id="ff34c-358">tooverify fonctionnalités du serveur de rapports de base hello fonctionne à présent, ouvrez votre navigateur avec des privilèges d’administrateur et puis de signaler les Gestionnaire de rapports ad server URL Parcourir toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="ff34c-358">tooverify that hello basic report server functionality is now working, open your browser with administrative privileges and then browse toohello following report server ad report manager URLS:</span></span>

* <span data-ttu-id="ff34c-359">Sur la machine virtuelle de hello, accédez à toohello URL du serveur de rapports :</span><span class="sxs-lookup"><span data-stu-id="ff34c-359">On hello VM, browse toohello report server URL:</span></span>
  
        http://localhost/reportserver
* <span data-ttu-id="ff34c-360">Sur la machine virtuelle de hello, accédez à toohello URL du Gestionnaire de rapports :</span><span class="sxs-lookup"><span data-stu-id="ff34c-360">On hello VM, browse toohello report manger URL:</span></span>
  
        http://localhost/Reports
* <span data-ttu-id="ff34c-361">À partir de votre ordinateur local, accédez toohello **distant** au Gestionnaire de rapports sur la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-361">From your local computer, browse toohello **remote** report Manager on hello VM.</span></span> <span data-ttu-id="ff34c-362">Mettre à jour le nom de DNS hello Bonjour selon l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="ff34c-362">Update hello DNS name in hello following example as appropriate.</span></span> <span data-ttu-id="ff34c-363">Lors de l’invité à entrer un mot de passe, utiliser les informations d’identification de l’administrateur hello que vous avez créé lors de la configuration de machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-363">When prompted for a password, use hello administrator credentials you created when hello VM was provisioned.</span></span> <span data-ttu-id="ff34c-364">nom d’utilisateur Hello est Bonjour [domaine]\[nom d’utilisateur] format, où domaine de hello est le nom de l’ordinateur hello machine virtuelle, par exemple ssrsnativecloud\testuser.</span><span class="sxs-lookup"><span data-stu-id="ff34c-364">hello user name is in hello [Domain]\[user name] format, where hello domain is hello VM computer name, for example ssrsnativecloud\testuser.</span></span> <span data-ttu-id="ff34c-365">Si vous n’utilisez pas HTTP**S**, supprimez hello **s** dans l’URL de hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-365">If you are not using HTTP**S**, remove hello **s** in hello URL.</span></span> <span data-ttu-id="ff34c-366">Consultez la section suivante de hello pour plus d’informations sur la création d’utilisateurs supplémentaires sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ff34c-366">See hello next section for information on creating additional users on VM.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/Reports
* <span data-ttu-id="ff34c-367">À partir de votre ordinateur local, accédez toohello URL du serveur de rapports distant.</span><span class="sxs-lookup"><span data-stu-id="ff34c-367">From your local computer, browse toohello remote report server URL.</span></span> <span data-ttu-id="ff34c-368">Mettre à jour le nom de DNS hello Bonjour selon l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="ff34c-368">Update hello DNS name in hello following example as appropriate.</span></span> <span data-ttu-id="ff34c-369">Si vous n’utilisez pas HTTPS, supprimez hello s dans les URL hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-369">If you are not using HTTPS, remove hello s in hello URL.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a><span data-ttu-id="ff34c-370">Créer des utilisateurs et attribuer des rôles</span><span class="sxs-lookup"><span data-stu-id="ff34c-370">Create Users and Assign Roles</span></span>
<span data-ttu-id="ff34c-371">Une fois que le serveur de rapports de configuration et la vérification hello, une tâche administrative courante est toocreate un ou plusieurs utilisateurs et affecter des utilisateurs tooReporting rôles des Services.</span><span class="sxs-lookup"><span data-stu-id="ff34c-371">After configuring and verifying hello report server, a common administrative task is toocreate one or more users and assign users tooReporting Services roles.</span></span> <span data-ttu-id="ff34c-372">Pour plus d’informations, voir hello :</span><span class="sxs-lookup"><span data-stu-id="ff34c-372">For more information, see hello following:</span></span>

* [<span data-ttu-id="ff34c-373">Créer un compte d’utilisateur local</span><span class="sxs-lookup"><span data-stu-id="ff34c-373">Create a local user account</span></span>](https://technet.microsoft.com/library/cc770642.aspx)
* <span data-ttu-id="ff34c-374">[Accorder l’accès utilisateur tooa le serveur de rapports (Gestionnaire de rapports)](https://msdn.microsoft.com/library/ms156034.aspx))</span><span class="sxs-lookup"><span data-stu-id="ff34c-374">[Grant User Access tooa Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span></span>
* [<span data-ttu-id="ff34c-375">Créer et gérer des attributions de rôles</span><span class="sxs-lookup"><span data-stu-id="ff34c-375">Create and Manage Role Assignments</span></span>](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a><span data-ttu-id="ff34c-376">tooCreate et publier les rapports toohello Machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="ff34c-376">tooCreate and Publish Reports toohello Azure Virtual Machine</span></span>
<span data-ttu-id="ff34c-377">Hello tableau suivant récapitule certaines des rapports existants de hello options toopublish disponibles à partir d’un serveur de rapports local ordinateur toohello hébergé sur hello Machine virtuelle Microsoft Azure :</span><span class="sxs-lookup"><span data-stu-id="ff34c-377">hello following table summarizes some of hello options available toopublish existing reports from an on-premises computer toohello report server hosted on hello Microsoft Azure Virtual Machine:</span></span>

* <span data-ttu-id="ff34c-378">**Script RS.exe**: utilisez RS.exe script toocopy les éléments de rapports et tooyour de serveur de rapports existante Machine virtuelle Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ff34c-378">**RS.exe script**: Use RS.exe script toocopy report items from and existing report server tooyour Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="ff34c-379">Pour plus d’informations, consultez le section hello « en mode natif tooNative Mode – Machine virtuelle Microsoft Azure » dans [Sample Reporting Services rs.exe Script tooMigrate contenu entre des serveurs de rapports](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff34c-379">For more information, see hello section “Native mode tooNative Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>
* <span data-ttu-id="ff34c-380">**Générateur de rapports**: machine virtuelle de hello inclut hello cliquez-une fois la version du Générateur de rapports Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ff34c-380">**Report Builder**: hello virtual machine includes hello click-once version of Microsoft SQL Server Report Builder.</span></span> <span data-ttu-id="ff34c-381">hello de générateur de rapports toostart première fois sur l’ordinateur virtuel de hello :</span><span class="sxs-lookup"><span data-stu-id="ff34c-381">toostart Report builder hello first time on hello virtual machine:</span></span>
  
  1. <span data-ttu-id="ff34c-382">Démarrez votre navigateur avec des privilèges administratifs.</span><span class="sxs-lookup"><span data-stu-id="ff34c-382">Start your browser with administrative privileges.</span></span>
  2. <span data-ttu-id="ff34c-383">Recherchez gestionnaire tooreport sur l’ordinateur virtuel de hello et cliquez sur **le Générateur de rapports** dans le ruban de hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-383">Browse tooreport manager on hello virtual machine and click **Report Builder**  in hello ribbon.</span></span>
     
     <span data-ttu-id="ff34c-384">Pour plus d’informations, consultez [Installation, désinstallation et prise en charge du Générateur de rapports](https://technet.microsoft.com/library/dd207038.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff34c-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span></span>
* <span data-ttu-id="ff34c-385">**SQL Server Data Tools : Machine virtuelle**: Si vous avez créé hello machine virtuelle avec SQL Server 2012, SQL Server Data Tools est installé sur l’ordinateur virtuel de hello et peut être utilisé toocreate **projets Report Server** et des rapports sur hello virtuel ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ff34c-385">**SQL Server Data Tools: VM**:  If you created hello VM with SQL Server 2012, then SQL Server Data Tools is installed on hello virtual machine and can be used toocreate **Report Server Projects** and reports on hello virtual machine.</span></span> <span data-ttu-id="ff34c-386">SQL Server Data Tools peut publier le serveur de rapports hello rapports toohello sur l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="ff34c-386">SQL Server Data Tools can publish hello reports toohello report server on hello virtual machine.</span></span>
  
    <span data-ttu-id="ff34c-387">Si vous avez créé hello machine virtuelle avec SQL server 2014, vous pouvez installer SQL Server données Tools - Business Intelligence pour visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ff34c-387">If you created hello VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span></span> <span data-ttu-id="ff34c-388">Pour plus d’informations, voir hello :</span><span class="sxs-lookup"><span data-stu-id="ff34c-388">For more information, see hello following:</span></span>
  
  * [<span data-ttu-id="ff34c-389">Microsoft SQL Server Data Tools - Business Intelligence pour Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="ff34c-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span></span>](https://www.microsoft.com/download/details.aspx?id=42313)
  * [<span data-ttu-id="ff34c-390">Microsoft SQL Server Data Tools - Business Intelligence pour Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="ff34c-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=36843)
  * [<span data-ttu-id="ff34c-391">SQL Server Data Tools et SQL Server Business Intelligence (SSDT-BI)</span><span class="sxs-lookup"><span data-stu-id="ff34c-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span></span>](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* <span data-ttu-id="ff34c-392">**SQL Server Data Tools : distant** : sur votre ordinateur local, créez un projet Reporting Services contenant des rapports Reporting Services dans SQL Server Data Tools.</span><span class="sxs-lookup"><span data-stu-id="ff34c-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span></span> <span data-ttu-id="ff34c-393">Configurer l’URL du service web tooconnect toohello hello projet.</span><span class="sxs-lookup"><span data-stu-id="ff34c-393">Configure hello project tooconnect toohello web service URL.</span></span>
  
    ![propriétés de projet ssdt pour un projet SSRS](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* <span data-ttu-id="ff34c-395">**Utilisez le script**: utiliser le contenu du serveur de rapports toocopy script.</span><span class="sxs-lookup"><span data-stu-id="ff34c-395">**Use script**: Use script toocopy report server content.</span></span> <span data-ttu-id="ff34c-396">Pour plus d’informations, consultez [Sample Reporting Services rs.exe Script tooMigrate contenu entre des serveurs de rapports](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff34c-396">For more information, see [Sample Reporting Services rs.exe Script tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a><span data-ttu-id="ff34c-397">Réduire les coûts si vous n’utilisez pas hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="ff34c-397">Minimize cost if you are not using hello VM</span></span>
> [!NOTE]
> <span data-ttu-id="ff34c-398">pour vos Machines virtuelles de Azure inutilisés, des frais toominimize arrêter hello machine virtuelle à partir de hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="ff34c-398">toominimize charges for your Azure Virtual Machines when not in use, shut down hello VM from hello Azure classic portal.</span></span> <span data-ttu-id="ff34c-399">Si vous utilisez les options d’alimentation Windows hello à l’intérieur d’un tooshut de machine virtuelle vers le bas hello machine virtuelle, vous êtes toujours facturé hello montant pour hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ff34c-399">If you use hello Windows power options inside a VM tooshut down hello VM, you are still charged hello same amount for hello VM.</span></span> <span data-ttu-id="ff34c-400">les frais tooreduce, vous devez tooshut vers le bas hello VM Bonjour portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="ff34c-400">tooreduce charges, you need tooshut down hello VM in hello Azure classic portal.</span></span> <span data-ttu-id="ff34c-401">Si vous n’avez plus besoin hello machine virtuelle, n’oubliez pas de toodelete hello VM et hello des frais de stockage de tooavoid de fichiers .vhd associés. Pour plus d’informations, consultez la section hello FAQ à [détails de tarification des Machines virtuelles](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="ff34c-401">If you no longer need hello VM, remember toodelete hello VM and hello associated .vhd files tooavoid storage charges.For more information, see hello FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>

## <a name="more-information"></a><span data-ttu-id="ff34c-402">Informations complémentaires</span><span class="sxs-lookup"><span data-stu-id="ff34c-402">More Information</span></span>
### <a name="resources"></a><span data-ttu-id="ff34c-403">Ressources</span><span class="sxs-lookup"><span data-stu-id="ff34c-403">Resources</span></span>
* <span data-ttu-id="ff34c-404">Pour obtenir un contenu similaire liés au déploiement de serveur unique tooa de SQL Server Business Intelligence et SharePoint 2013, consultez [tooCreate d’utiliser Windows PowerShell une machine virtuelle Azure avec SQL Server BI et SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff34c-404">For similar content related tooa single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell tooCreate an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span></span>
* <span data-ttu-id="ff34c-405">Pour tooa connexe de contenu similaire déploiement multiserveur de SQL Server Business Intelligence et SharePoint 2013, consultez [déployer SQL Server Business Intelligence dans des Machines virtuelles Azure](https://msdn.microsoft.com/library/dn321998.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff34c-405">For similar content related tooa multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span></span>
* <span data-ttu-id="ff34c-406">Pour obtenir des informations générales toodeployments associées de SQL Server Business Intelligence dans des Machines virtuelles Azure, consultez [SQL Server Business Intelligence dans des Machines virtuelles Azure](virtual-machines-windows-classic-ps-sql-bi.md).</span><span class="sxs-lookup"><span data-stu-id="ff34c-406">For General information related toodeployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span></span>
* <span data-ttu-id="ff34c-407">Pour plus d’informations sur le coût de hello frais de calcul Azure, consultez onglet de Machines virtuelles hello de [calculatrice de prix Azure](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="ff34c-407">For more information about hello cost of Azure compute charges, see hello Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span></span>

### <a name="community-content"></a><span data-ttu-id="ff34c-408">Contenu de la communauté</span><span class="sxs-lookup"><span data-stu-id="ff34c-408">Community Content</span></span>
* <span data-ttu-id="ff34c-409">Pour obtenir des instructions étape par étape sur la façon dont toocreate un mode natif de Reporting Services serveur de rapports sans utiliser de script, consultez [SQL Reporting Service d’hébergement sur Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span><span class="sxs-lookup"><span data-stu-id="ff34c-409">For step by step instructions on how toocreate a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span></span>

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a><span data-ttu-id="ff34c-410">Ressources de tooother de liens pour SQL Server dans des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="ff34c-410">Links tooother resources for SQL Server in Azure VMs</span></span>
[<span data-ttu-id="ff34c-411">Vue d’ensemble de SQL Server sur les machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="ff34c-411">SQL Server on Azure Virtual Machines Overview</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

