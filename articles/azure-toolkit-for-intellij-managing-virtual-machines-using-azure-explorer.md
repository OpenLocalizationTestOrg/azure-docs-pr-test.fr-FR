---
title: "machines virtuelles d’aaaManage à l’aide de hello Explorateur Azure pour IntelliJ | Documents Microsoft"
description: "Découvrez comment toomanage vos machines virtuelles Azure à l’aide de hello Explorateur Azure pour IntelliJ."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: a73dd4f73b311dd3413f6712e3b76c36ee464de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-intellij"></a><span data-ttu-id="b6510-103">Gérer des ordinateurs virtuels à l’aide de hello Explorateur Azure pour IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b6510-103">Manage virtual machines by using hello Azure Explorer for IntelliJ</span></span>

<span data-ttu-id="b6510-104">Hello Explorateur Azure, qui fait partie de hello Azure Toolkit pour IntelliJ, fournit aux développeurs Java une solution facile à utiliser pour la gestion des ordinateurs virtuels de leur compte Azure à partir d’à l’intérieur de hello IntelliJ environnement de développement intégré (IDE).</span><span class="sxs-lookup"><span data-stu-id="b6510-104">hello Azure Explorer, which is part of hello Azure Toolkit for IntelliJ, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside hello IntelliJ integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-intellij-show-azure-explorer](../includes/azure-toolkit-for-intellij-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-intellij"></a><span data-ttu-id="b6510-105">Suppression d’une machine virtuelle dans IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b6510-105">Create a virtual machine in IntelliJ</span></span>

<span data-ttu-id="b6510-106">toocreate un ordinateur virtuel à l’aide de hello Explorateur Azure, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b6510-106">toocreate a virtual machine by using hello Azure Explorer, do hello following:</span></span> 

1. <span data-ttu-id="b6510-107">Se connecter à l’aide des étapes de hello Bonjour tooyour compte Azure [instructions d’authentification pour hello boîte à outils Azure pour IntelliJ] l’article.</span><span class="sxs-lookup"><span data-stu-id="b6510-107">Sign in tooyour Azure account by using hello steps in hello [Sign-in instructions for hello Azure Toolkit for IntelliJ] article.</span></span>

2. <span data-ttu-id="b6510-108">Bonjour **Explorateur Azure** afficher, développez hello **Azure** nœud, avec le bouton droit **virtuels**, puis cliquez sur **créer un ordinateur virtuel**.</span><span class="sxs-lookup"><span data-stu-id="b6510-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span> 

   <span data-ttu-id="b6510-109">![Hello commande de créer un ordinateur virtuel][CR01]</span><span class="sxs-lookup"><span data-stu-id="b6510-109">![hello Create VM command][CR01]</span></span>  
    <span data-ttu-id="b6510-110">Hello **créer Machine virtuelle** Assistant s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="b6510-110">hello **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="b6510-111">Bonjour **choisir un abonnement** fenêtre, sélectionnez votre abonnement, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="b6510-111">In hello **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span> 

   ![Hello fenêtre Choisir un abonnement][CR02]

4. <span data-ttu-id="b6510-113">Bonjour **sélectionner une Image de Machine virtuelle** fenêtre, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b6510-113">In hello **Select a Virtual Machine Image** window, enter hello following information:</span></span>

   * <span data-ttu-id="b6510-114">**Emplacement**: spécifie l’emplacement où votre machine virtuelle sera créée (par exemple *États-Unis de l’Ouest*).</span><span class="sxs-lookup"><span data-stu-id="b6510-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span> 

   * <span data-ttu-id="b6510-115">**Image recommandée** : spécifie que vous allez choisir une image dans une liste abrégée d’images couramment utilisées.</span><span class="sxs-lookup"><span data-stu-id="b6510-115">**Recommended image**: Specifies that you will choose an image from an abbreviated list of commonly used images.</span></span>

   * <span data-ttu-id="b6510-116">**Image personnalisée**: Spécifie que vous allez choisir une image personnalisée en fournissant hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b6510-116">**Custom image**: Specifies that you will choose a custom image by providing hello following information:</span></span>

      * <span data-ttu-id="b6510-117">**Serveur de publication**: Spécifie le serveur de publication hello créé hello image que vous utiliserez pour votre machine virtuelle (par exemple, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="b6510-117">**Publisher**: Specifies hello publisher that created hello image that you will use for your virtual machine (for example, *Microsoft*).</span></span>

      * <span data-ttu-id="b6510-118">**Offre**: Spécifie l’ordinateur virtuel de hello offre toouse à partir du serveur de publication sélectionné hello (par exemple, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="b6510-118">**Offer**: Specifies hello virtual machine offering toouse from hello selected publisher (for example, *JDK*).</span></span>

      * <span data-ttu-id="b6510-119">**Référence (SKU)**: Spécifie hello stock référence toouse à partir de l’offre de hello sélectionné (par exemple, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="b6510-119">**Sku**: Specifies hello stockkeeping unit (SKU) toouse from hello selected offering (for example, *JDK_8*).</span></span>

      * <span data-ttu-id="b6510-120">**Version #**: Spécifie la version de hello sélectionné toouse de référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="b6510-120">**Version #**: Specifies which version of hello selected SKU toouse.</span></span>

   ![Hello sélectionner une fenêtre de l’Image de Machine virtuelle][CR03]

5. <span data-ttu-id="b6510-122">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="b6510-122">Click **Next**.</span></span> 

6. <span data-ttu-id="b6510-123">Bonjour **les paramètres de base de Machine virtuelle** fenêtre, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b6510-123">In hello **Virtual Machine Basic Settings** window, enter hello following information:</span></span>

   * <span data-ttu-id="b6510-124">**Nom de machine virtuelle**: Spécifie le nom hello pour votre nouvel ordinateur virtuel, qui doit commencer par une lettre et contenir uniquement des lettres, des chiffres et des traits d’union.</span><span class="sxs-lookup"><span data-stu-id="b6510-124">**Virtual machine name**: Specifies hello name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="b6510-125">**Taille**: Spécifie le nombre de hello de cœurs et de tooallocate de mémoire pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6510-125">**Size**: Specifies hello number of cores and memory tooallocate for your virtual machine.</span></span>

   * <span data-ttu-id="b6510-126">**Nom d’utilisateur**: Spécifie hello toocreate de compte administrateur pour la gestion de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6510-126">**User name**: Specifies hello administrator account toocreate for managing your virtual machine.</span></span>

   * <span data-ttu-id="b6510-127">**Mot de passe** et **confirmer**: Spécifie le mot de passe hello pour votre compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="b6510-127">**Password** and **Confirm**: Specifies hello password for your administrator account.</span></span>

   ![fenêtre des paramètres de base de Machine virtuelle Hello][CR04]

7. <span data-ttu-id="b6510-129">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="b6510-129">Click **Next**.</span></span> 

8. <span data-ttu-id="b6510-130">Bonjour **associés des ressources** fenêtre, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b6510-130">In hello **Associated Resources** window, enter hello following information:</span></span>

   * <span data-ttu-id="b6510-131">**Groupe de ressources**: Spécifie le groupe de ressources hello pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6510-131">**Resource group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="b6510-132">Sélectionnez une des options suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="b6510-132">Select one of hello following options:</span></span>
      * <span data-ttu-id="b6510-133">**Créer de nouveaux**: Spécifie que vous souhaitez toocreate un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="b6510-133">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="b6510-134">**Utiliser l’existante**: Spécifie que vous souhaitez tooselect dans une liste de groupes de ressources qui sont associés à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="b6510-134">**Use existing**: Specifies that you want tooselect from a list of resource groups that are associated with your Azure account.</span></span>

       ![fenêtre de Hello associées de ressources][CR07]

   * <span data-ttu-id="b6510-136">**Compte de stockage**: Spécifie toouse de compte de stockage hello pour le stockage de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6510-136">**Storage account**: Specifies hello storage account toouse for storing your virtual machine.</span></span> <span data-ttu-id="b6510-137">Vous pouvez choisir un compte de stockage ou en créer un.</span><span class="sxs-lookup"><span data-stu-id="b6510-137">You can choose an existing storage account or create a new account.</span></span> <span data-ttu-id="b6510-138">Si vous choisissez **créer un nouveau**, hello suivant la boîte de dialogue s’affiche :</span><span class="sxs-lookup"><span data-stu-id="b6510-138">If you choose **Create New**, hello following dialog box appears:</span></span>

      ![boîte de dialogue Créer un compte de stockage Hello][CR05]

   * <span data-ttu-id="b6510-140">**Réseau virtuel** et **sous-réseau**: Spécifie le réseau virtuel de hello et sous-réseau que votre machine virtuelle se connecte à.</span><span class="sxs-lookup"><span data-stu-id="b6510-140">**Virtual Network** and **Subnet**: Specifies hello virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="b6510-141">Vous pouvez utiliser un réseau et un sous-réseau existants, ou créer un réseau et un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="b6510-141">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="b6510-142">Si vous sélectionnez **nouvel**, hello suivant la boîte de dialogue s’affiche :</span><span class="sxs-lookup"><span data-stu-id="b6510-142">If you select **Create new**, hello following dialog box appears:</span></span>

      ![boîte de dialogue Créer un réseau virtuel Hello][CR06]

   * <span data-ttu-id="b6510-144">**Adresse IP publique** : spécifie l’adresse IP externe de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6510-144">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="b6510-145">Vous pouvez choisir toocreate une nouvelle adresse IP ou, si votre machine virtuelle ne disposent pas d’une adresse IP publique, vous pouvez sélectionner **(aucun)**.</span><span class="sxs-lookup"><span data-stu-id="b6510-145">You can choose toocreate a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span> 

   * <span data-ttu-id="b6510-146">**Groupe de sécurité réseau** : spécifie un pare-feu réseau facultatif pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b6510-146">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="b6510-147">Vous pouvez sélectionner un pare-feu existant ou, si votre machine virtuelle n’a pas besoin de pare-feu réseau, vous pouvez sélectionner **(Aucun)**.</span><span class="sxs-lookup"><span data-stu-id="b6510-147">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span> 

   * <span data-ttu-id="b6510-148">**Groupe à haute disponibilité** : spécifie un groupe à haute disponibilité auquel votre machine virtuelle peut appartenir.</span><span class="sxs-lookup"><span data-stu-id="b6510-148">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="b6510-149">Vous pouvez sélectionner un ensemble de disponibilité existant, créez un nouveau jeu de disponibilité ou, si votre machine virtuelle n’appartiendra tooan à haute disponibilité, sélectionnez **(aucun)**.</span><span class="sxs-lookup"><span data-stu-id="b6510-149">You can select an existing availability set, create a new availability set or, if your virtual machine will not belong tooan availability set, select **(None)**.</span></span>

9. <span data-ttu-id="b6510-150">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="b6510-150">Click **Finish**.</span></span>  
    <span data-ttu-id="b6510-151">Votre nouvel ordinateur virtuel s’affiche dans la fenêtre d’outil Explorateur Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b6510-151">Your new virtual machine appears in hello Azure Explorer tool window.</span></span> 

   ![Machine virtuelle Bonjour Azure Explorateur][CR08]

## <a name="restart-a-virtual-machine-in-intellij"></a><span data-ttu-id="b6510-153">Redémarrer une machine virtuelle dans IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b6510-153">Restart a virtual machine in IntelliJ</span></span>

<span data-ttu-id="b6510-154">toorestart un ordinateur virtuel à l’aide de hello Explorateur Azure dans IntelliJ, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b6510-154">toorestart a virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="b6510-155">Bonjour **Explorateur Azure** afficher, avec le bouton droit hello virtual machine, puis sélectionnez **redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="b6510-155">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Restart**.</span></span>

   ![commande de redémarrage Hello à une machine virtuelle][RE01]

2. <span data-ttu-id="b6510-157">Dans la fenêtre de confirmation hello, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="b6510-157">In hello confirmation window, click **Yes**.</span></span> 

   ![Hello redémarrer la fenêtre de confirmation de machine virtuelle][RE02]

## <a name="shut-down-a-virtual-machine-in-intellij"></a><span data-ttu-id="b6510-159">Arrêter une machine virtuelle dans IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b6510-159">Shut down a virtual machine in IntelliJ</span></span>

<span data-ttu-id="b6510-160">tooshut vers le bas d’une machine virtuelle en cours d’exécution à l’aide de hello Explorateur Azure dans IntelliJ, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b6510-160">tooshut down a running virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="b6510-161">Bonjour **Explorateur Azure** afficher, avec le bouton droit hello virtual machine, puis sélectionnez **arrêt**.</span><span class="sxs-lookup"><span data-stu-id="b6510-161">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Shutdown**.</span></span>

   ![commande d’arrêt d’une machine virtuelle Hello][SH01]

2. <span data-ttu-id="b6510-163">Dans la fenêtre de confirmation hello, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="b6510-163">In hello confirmation window, click **Yes**.</span></span> 

   ![Hello arrêter de la fenêtre de confirmation de machine virtuelle][SH02]

## <a name="delete-a-virtual-machine-in-intellij"></a><span data-ttu-id="b6510-165">Supprimer une machine virtuelle dans IntelliJ</span><span class="sxs-lookup"><span data-stu-id="b6510-165">Delete a virtual machine in IntelliJ</span></span>

<span data-ttu-id="b6510-166">toodelete un ordinateur virtuel à l’aide de hello Explorateur Azure dans IntelliJ, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="b6510-166">toodelete a virtual machine by using hello Azure Explorer in IntelliJ, do hello following:</span></span>

1. <span data-ttu-id="b6510-167">Bonjour **Explorateur Azure** afficher, avec le bouton droit hello virtual machine, puis sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="b6510-167">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Delete**.</span></span>

   ![commande de suppression d’une machine virtuelle Hello][DE01]

2. <span data-ttu-id="b6510-169">Dans la fenêtre de confirmation hello, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="b6510-169">In hello confirmation window, click **Yes**.</span></span> 

   ![Hello supprimer la fenêtre de confirmation de machine virtuelle][DE02]

## <a name="next-steps"></a><span data-ttu-id="b6510-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b6510-171">Next steps</span></span>
<span data-ttu-id="b6510-172">Pour plus d’informations sur les tailles de machine virtuelle Azure et la tarification, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="b6510-172">For more information about Azure virtual-machine sizes and pricing, see hello following resources:</span></span>

* <span data-ttu-id="b6510-173">Tailles des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="b6510-173">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="b6510-174">[Tailles des machines virtuelles Windows dans Azure]</span><span class="sxs-lookup"><span data-stu-id="b6510-174">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="b6510-175">[Tailles des machines virtuelles Linux dans Azure]</span><span class="sxs-lookup"><span data-stu-id="b6510-175">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="b6510-176">Tarification des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="b6510-176">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="b6510-177">[Tarification des machines virtuelles Windows]</span><span class="sxs-lookup"><span data-stu-id="b6510-177">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="b6510-178">[Tarification des machines virtuelles Linux]</span><span class="sxs-lookup"><span data-stu-id="b6510-178">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="b6510-179">Pour plus d’informations sur hello boîtes à outils Azure pour Java IDE, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="b6510-179">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="b6510-180">[boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b6510-180">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b6510-181">[Nouveautés de hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b6510-181">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b6510-182">[Lors de l’installation hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b6510-182">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b6510-183">[Instructions de connexion pour hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b6510-183">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="b6510-184">[Créer une application web Hello World pour Azure dans Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b6510-184">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="b6510-185">[Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b6510-185">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b6510-186">[Quelles sont les nouveautés Bonjour Azure Toolkit pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b6510-186">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b6510-187">[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b6510-187">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b6510-188">[instructions d’authentification pour hello boîte à outils Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b6510-188">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="b6510-189">[Créer une application web Hello World pour Azure dans IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="b6510-189">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="b6510-190">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez [Centre de développement Java pour Azure] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="b6510-190">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md
[Créer une application web Hello World pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Créer une application web Hello World pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Lors de l’installation hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Instructions de connexion pour hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[instructions d’authentification pour hello boîte à outils Azure pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nouveautés de hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Quelles sont les nouveautés Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/

[Tailles des machines virtuelles Windows dans Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tailles des machines virtuelles Linux dans Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Tarification des machines virtuelles Windows]: /pricing/details/virtual-machines/windows/
[Tarification des machines virtuelles Linux]: /pricing/details/virtual-machines/linux/


<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-intellij-managing-virtual-machines-using-azure-explorer/CR08.png
