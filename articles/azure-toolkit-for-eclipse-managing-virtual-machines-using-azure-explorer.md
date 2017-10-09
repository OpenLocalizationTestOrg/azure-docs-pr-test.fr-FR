---
title: "machines virtuelles d’aaaManage à l’aide de hello Explorateur Azure pour Eclipse | Documents Microsoft"
description: "Découvrez comment toomanage vos machines virtuelles Azure à l’aide de hello Explorateur Azure pour Eclipse."
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
ms.openlocfilehash: aa83ec7546a0a8514842723b51ce8a5af81f98f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-by-using-hello-azure-explorer-for-eclipse"></a><span data-ttu-id="c8c2b-103">Gérer des ordinateurs virtuels à l’aide de hello Explorateur Azure pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="c8c2b-103">Manage virtual machines by using hello Azure Explorer for Eclipse</span></span>

<span data-ttu-id="c8c2b-104">Hello Explorateur Azure, qui fait partie de hello boîte à outils Azure pour Eclipse, fournit aux développeurs Java une solution facile à utiliser pour la gestion des ordinateurs virtuels de leur compte Azure à partir d’à l’intérieur de hello Eclipse environnement de développement intégré (IDE).</span><span class="sxs-lookup"><span data-stu-id="c8c2b-104">hello Azure Explorer, which is part of hello Azure Toolkit for Eclipse, provides Java developers with an easy-to-use solution for managing virtual machines in their Azure account from inside hello Eclipse integrated development environment (IDE).</span></span>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

[!INCLUDE [azure-toolkit-for-eclipse-show-azure-explorer](../includes/azure-toolkit-for-eclipse-show-azure-explorer.md)]

## <a name="create-a-virtual-machine-in-eclipse"></a><span data-ttu-id="c8c2b-105">Création d’une machine virtuelle dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="c8c2b-105">Create a virtual machine in Eclipse</span></span>

<span data-ttu-id="c8c2b-106">toocreate un ordinateur virtuel à l’aide de hello Explorateur Azure, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="c8c2b-106">toocreate a virtual machine by using hello Azure Explorer, do hello following:</span></span>

1. <span data-ttu-id="c8c2b-107">Se connecter à l’aide de hello tooyour compte Azure [instructions connectez-vous pour hello boîte à outils Azure pour Eclipse].</span><span class="sxs-lookup"><span data-stu-id="c8c2b-107">Sign in tooyour Azure account by using hello [Sign-in instructions for hello Azure Toolkit for Eclipse].</span></span>

2. <span data-ttu-id="c8c2b-108">Bonjour **Explorateur Azure** afficher, développez hello **Azure** nœud, avec le bouton droit **virtuels**, puis cliquez sur **créer un ordinateur virtuel**.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-108">In hello **Azure Explorer** view, expand hello **Azure** node, right-click **Virtual Machines**, and then click **Create VM**.</span></span>

   <span data-ttu-id="c8c2b-109">![Hello commande de créer un ordinateur virtuel][CR01]</span><span class="sxs-lookup"><span data-stu-id="c8c2b-109">![hello Create VM command][CR01]</span></span>  
   <span data-ttu-id="c8c2b-110">Hello **créer Machine virtuelle** Assistant s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-110">hello **Create new Virtual Machine** wizard opens.</span></span>

3. <span data-ttu-id="c8c2b-111">Bonjour **choisir un abonnement** fenêtre, sélectionnez votre abonnement, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-111">In hello **Choose a Subscription** window, select your subscription, and then click **Next**.</span></span>

   ![Hello fenêtre Choisir un abonnement][CR02]

4. <span data-ttu-id="c8c2b-113">Bonjour **sélectionner une Image de Machine virtuelle** fenêtre, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c8c2b-113">In hello **Select a Virtual Machine Image** window, enter hello following information:</span></span>

   * <span data-ttu-id="c8c2b-114">**Emplacement**: spécifie l’emplacement où votre machine virtuelle sera créée (par exemple *États-Unis de l’Ouest*).</span><span class="sxs-lookup"><span data-stu-id="c8c2b-114">**Location**: Specifies where your virtual machine will be created (for example, *West US*).</span></span>

   * <span data-ttu-id="c8c2b-115">**Serveur de publication**: Spécifie le serveur de publication hello qui a créé l’image hello vous utiliserez toocreate votre machine virtuelle (par exemple, *Microsoft*).</span><span class="sxs-lookup"><span data-stu-id="c8c2b-115">**Publisher**: Specifies hello publisher that created hello image you'll use toocreate your virtual machine (for example, *Microsoft*).</span></span>

   * <span data-ttu-id="c8c2b-116">**Offre**: Spécifie l’ordinateur virtuel de hello offre toouse à partir du serveur de publication sélectionné hello (par exemple, *JDK*).</span><span class="sxs-lookup"><span data-stu-id="c8c2b-116">**Offer**: Specifies hello virtual machine offering toouse from hello selected publisher (for example, *JDK*).</span></span>

   * <span data-ttu-id="c8c2b-117">**Référence (SKU)**: Spécifie hello stock référence toouse à partir de l’offre de hello sélectionné (par exemple, *JDK_8*).</span><span class="sxs-lookup"><span data-stu-id="c8c2b-117">**Sku**: Specifies hello stockkeeping unit (SKU) toouse from hello selected offering (for example, *JDK_8*).</span></span>

   * <span data-ttu-id="c8c2b-118">**Version #**: Spécifie la version de hello sélectionné toouse de référence (SKU).</span><span class="sxs-lookup"><span data-stu-id="c8c2b-118">**Version #**: Specifies which version of hello selected SKU toouse.</span></span>

    ![Hello sélectionner une fenêtre de l’Image de Machine virtuelle][CR03]

5. <span data-ttu-id="c8c2b-120">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-120">Click **Next**.</span></span>

6. <span data-ttu-id="c8c2b-121">Bonjour **les paramètres de base de Machine virtuelle** fenêtre, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c8c2b-121">In hello **Virtual Machine Basic Settings** window, enter hello following information:</span></span>

   * <span data-ttu-id="c8c2b-122">**Nom de Machine virtuelle**: Spécifie le nom hello pour votre nouvel ordinateur virtuel, qui doit commencer par une lettre et contenir uniquement des lettres, des chiffres et des traits d’union.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-122">**Virtual Machine Name**: Specifies hello name for your new virtual machine, which must start with a letter and contain only letters, numbers, and hyphens.</span></span>

   * <span data-ttu-id="c8c2b-123">**Taille**: Spécifie le nombre de hello de cœurs et de tooallocate de mémoire pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-123">**Size**: Specifies hello number of cores and memory tooallocate for your virtual machine.</span></span>

   * <span data-ttu-id="c8c2b-124">**Nom d’utilisateur**: Spécifie hello toocreate de compte administrateur pour la gestion de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-124">**User name**: Specifies hello administrator account toocreate for managing your virtual machine.</span></span>

   * <span data-ttu-id="c8c2b-125">**Mot de passe** et **confirmer**: Spécifie le mot de passe hello pour votre compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-125">**Password** and **Confirm**: Specifies hello password for your administrator account.</span></span>

    ![fenêtre des paramètres de base de Machine virtuelle Hello][CR04]

7. <span data-ttu-id="c8c2b-127">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-127">Click **Next**.</span></span>

8. <span data-ttu-id="c8c2b-128">Bonjour **créer un nouveau compte de stockage** fenêtre, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c8c2b-128">In hello **Create New Storage Account** window, enter hello following information:</span></span>

   * <span data-ttu-id="c8c2b-129">**Groupe de ressources**: Spécifie le groupe de ressources hello pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-129">**Resource Group**: Specifies hello resource group for your virtual machine.</span></span> <span data-ttu-id="c8c2b-130">Sélectionnez une des options suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="c8c2b-130">Select one of hello following options:</span></span>
      * <span data-ttu-id="c8c2b-131">**Créer de nouveaux**: Spécifie que vous souhaitez toocreate un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-131">**Create new**: Specifies that you want toocreate a new resource group.</span></span>
      * <span data-ttu-id="c8c2b-132">**Utiliser l’existante**: Spécifie que vous souhaitez tooselect un groupe de ressources est déjà associé à votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-132">**Use existing**: Specifies that you want tooselect a resource group that is already associated with your Azure account.</span></span>

      ![boîte de dialogue Créer un nouveau compte de stockage Hello][CR05]

   * <span data-ttu-id="c8c2b-134">**Compte de stockage**: Spécifie toouse de compte de stockage hello pour le stockage de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-134">**Storage account**: Specifies hello storage account toouse for storing your virtual machine.</span></span> <span data-ttu-id="c8c2b-135">Vous pouvez utiliser un compte de stockage existant ou en créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-135">You can use an existing storage account or create a new account.</span></span>

   * <span data-ttu-id="c8c2b-136">**Réseau virtuel** et **sous-réseau**: Spécifie le réseau virtuel de hello et sous-réseau que votre machine virtuelle se connecte à.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-136">**Virtual Network** and **Subnet**: Specifies hello virtual network and subnet that your virtual machine will connect to.</span></span> <span data-ttu-id="c8c2b-137">Vous pouvez utiliser un réseau et un sous-réseau existants, ou créer un réseau et un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-137">You can use an existing network and subnet, or you can create a new network and subnet.</span></span> <span data-ttu-id="c8c2b-138">Si vous sélectionnez **nouvel**, hello suivant la boîte de dialogue s’affiche :</span><span class="sxs-lookup"><span data-stu-id="c8c2b-138">If you select **Create new**, hello following dialog box is displayed:</span></span>

      ![boîte de dialogue Créer un nouveau réseau virtuel Hello][CR06]

9. <span data-ttu-id="c8c2b-140">Bonjour **associés des ressources** fenêtre, entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="c8c2b-140">In hello **Associated Resources** window, enter hello following information:</span></span>

   * <span data-ttu-id="c8c2b-141">**Adresse IP publique** : spécifie l’adresse IP externe de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-141">**Public IP address**: Specifies an external-facing IP address for your virtual machine.</span></span> <span data-ttu-id="c8c2b-142">Vous pouvez choisir toocreate une nouvelle adresse IP ou, si votre machine virtuelle ne disposent pas d’une adresse IP publique, vous pouvez sélectionner **(aucun)**.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-142">You can choose toocreate a new IP address or, if your virtual machine will not have a public IP address, you can select **(None)**.</span></span>

   * <span data-ttu-id="c8c2b-143">**Groupe de sécurité réseau** : spécifie un pare-feu réseau facultatif pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-143">**Network security group**: Specifies an optional networking firewall for your virtual machine.</span></span> <span data-ttu-id="c8c2b-144">Vous pouvez sélectionner un pare-feu existant ou, si votre machine virtuelle n’a pas besoin de pare-feu réseau, vous pouvez sélectionner **(Aucun)**.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-144">You can select an existing firewall or, if your virtual machine will not use a network firewall, you can select **(None)**.</span></span>

   * <span data-ttu-id="c8c2b-145">**Groupe à haute disponibilité** : spécifie un groupe à haute disponibilité auquel votre machine virtuelle peut appartenir.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-145">**Availability set**: Specifies an optional availability set that your virtual machine can belong to.</span></span> <span data-ttu-id="c8c2b-146">Vous pouvez sélectionner un ensemble de disponibilité existant ou créer un nouvel ensemble de disponibilité ou, si votre machine virtuelle appartiendra pas tooan à haute disponibilité, vous pouvez sélectionner **(aucun)**.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-146">You can select an existing availability set or create a new availability set or, if your virtual machine will not belong tooan availability set, you can select **(None)**.</span></span>

   ![fenêtre de Hello associées de ressources][CR07]

9. <span data-ttu-id="c8c2b-148">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-148">Click **Finish**.</span></span>  
  <span data-ttu-id="c8c2b-149">Votre nouvel ordinateur virtuel s’affiche dans la fenêtre d’outil Explorateur Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-149">Your new virtual machine is displayed in hello Azure Explorer tool window.</span></span>

   ![Nouvelle machine virtuelle][CR08]

## <a name="restart-a-virtual-machine-in-eclipse"></a><span data-ttu-id="c8c2b-151">Redémarrage d’une machine virtuelle dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="c8c2b-151">Restart a virtual machine in Eclipse</span></span>

<span data-ttu-id="c8c2b-152">toorestart un ordinateur virtuel à l’aide de hello Explorateur Azure dans Eclipse, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="c8c2b-152">toorestart a virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="c8c2b-153">Bonjour **Explorateur Azure** afficher, avec le bouton droit hello virtual machine, puis sélectionnez **redémarrer**.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-153">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Restart**.</span></span>

   ![commande de redémarrage Hello à une machine virtuelle][RE01]

2. <span data-ttu-id="c8c2b-155">Dans la fenêtre de confirmation hello, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-155">In hello confirmation window, click **Yes**.</span></span>

   ![fenêtre de confirmation du redémarrage Hello][RE02]

## <a name="shut-down-a-virtual-machine-in-eclipse"></a><span data-ttu-id="c8c2b-157">Arrêt d’une machine virtuelle dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="c8c2b-157">Shut down a virtual machine in Eclipse</span></span>

<span data-ttu-id="c8c2b-158">tooshut vers le bas d’une machine virtuelle en cours d’exécution à l’aide de hello Explorateur Azure dans Eclipse, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="c8c2b-158">tooshut down a running virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="c8c2b-159">Bonjour **Explorateur Azure** afficher, avec le bouton droit hello virtual machine, puis sélectionnez **arrêt**.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-159">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Shutdown**.</span></span>

   ![commande d’arrêt d’une machine virtuelle Hello][SH01]

2. <span data-ttu-id="c8c2b-161">Dans la fenêtre de confirmation hello, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-161">In hello confirmation window, click **Yes**.</span></span>

   ![fenêtre de confirmation de l’arrêt des machines virtuelles Hello][SH02]

## <a name="delete-a-virtual-machine-in-eclipse"></a><span data-ttu-id="c8c2b-163">Suppression d’une machine virtuelle dans Eclipse</span><span class="sxs-lookup"><span data-stu-id="c8c2b-163">Delete a virtual machine in Eclipse</span></span>

<span data-ttu-id="c8c2b-164">toodelete un ordinateur virtuel à l’aide de hello Explorateur Azure dans Eclipse, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="c8c2b-164">toodelete a virtual machine by using hello Azure Explorer in Eclipse, do hello following:</span></span>

1. <span data-ttu-id="c8c2b-165">Bonjour **Explorateur Azure** afficher, avec le bouton droit hello virtual machine, puis sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-165">In hello **Azure Explorer** view, right-click hello virtual machine, and then select **Delete**.</span></span>

   ![commande de suppression d’une machine virtuelle Hello][DE01]

2. <span data-ttu-id="c8c2b-167">Dans la fenêtre de confirmation hello, cliquez sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="c8c2b-167">In hello confirmation window, click **Yes**.</span></span>

   ![fenêtre de confirmation de suppression de la machine virtuelle Hello][DE02]

## <a name="next-steps"></a><span data-ttu-id="c8c2b-169">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c8c2b-169">Next steps</span></span>
<span data-ttu-id="c8c2b-170">Pour plus d’informations sur les tailles de machine virtuelle Azure et la tarification, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="c8c2b-170">For more information about Azure virtual-machine sizes and pricing, see hello following resources:</span></span>

* <span data-ttu-id="c8c2b-171">Tailles des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="c8c2b-171">Azure virtual-machine sizes</span></span>
  * <span data-ttu-id="c8c2b-172">[Tailles des machines virtuelles Windows dans Azure]</span><span class="sxs-lookup"><span data-stu-id="c8c2b-172">[Sizes for Windows virtual machines in Azure]</span></span>
  * <span data-ttu-id="c8c2b-173">[Tailles des machines virtuelles Linux dans Azure]</span><span class="sxs-lookup"><span data-stu-id="c8c2b-173">[Sizes for Linux virtual machines in Azure]</span></span>
* <span data-ttu-id="c8c2b-174">Tarification des machines virtuelles Azure</span><span class="sxs-lookup"><span data-stu-id="c8c2b-174">Azure virtual-machine pricing</span></span>
  * <span data-ttu-id="c8c2b-175">[Tarification des machines virtuelles Windows]</span><span class="sxs-lookup"><span data-stu-id="c8c2b-175">[Windows virtual-machine pricing]</span></span>
  * <span data-ttu-id="c8c2b-176">[Tarification des machines virtuelles Linux]</span><span class="sxs-lookup"><span data-stu-id="c8c2b-176">[Linux virtual-machine pricing]</span></span>

<span data-ttu-id="c8c2b-177">Pour plus d’informations sur hello boîtes à outils Azure pour Java IDE, consultez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="c8c2b-177">For more information about hello Azure Toolkits for Java IDEs, see hello following resources:</span></span>

* <span data-ttu-id="c8c2b-178">[boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c8c2b-178">[Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c8c2b-179">[Nouveautés de hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c8c2b-179">[What's new in hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c8c2b-180">[Lors de l’installation hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c8c2b-180">[Installing hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c8c2b-181">[instructions connectez-vous pour hello boîte à outils Azure pour Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c8c2b-181">[Sign-in instructions for hello Azure Toolkit for Eclipse]</span></span>
  * <span data-ttu-id="c8c2b-182">[Créer une application web Hello World pour Azure dans Eclipse]</span><span class="sxs-lookup"><span data-stu-id="c8c2b-182">[Create a Hello World web app for Azure in Eclipse]</span></span>
* <span data-ttu-id="c8c2b-183">[Kit de ressources Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c8c2b-183">[Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c8c2b-184">[Quelles sont les nouveautés Bonjour Azure Toolkit pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c8c2b-184">[What's new in hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c8c2b-185">[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c8c2b-185">[Installing hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c8c2b-186">[Instructions d’authentification pour hello boîte à outils Azure pour IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c8c2b-186">[Sign-in instructions for hello Azure Toolkit for IntelliJ]</span></span>
  * <span data-ttu-id="c8c2b-187">[Créer une application web Hello World pour Azure dans IntelliJ]</span><span class="sxs-lookup"><span data-stu-id="c8c2b-187">[Create a Hello World web app for Azure in IntelliJ]</span></span>

<span data-ttu-id="c8c2b-188">Pour plus d’informations sur l’utilisation d’Azure avec Java, consultez [Centre de développement Java pour Azure] et [Outils Java pour Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="c8c2b-188">For more information about using Azure with Java, see [Azure Java Developer Center] and [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse.md
[Kit de ressources Azure pour IntelliJ]: ./azure-toolkit-for-intellij.md
[Créer une application web Hello World pour Azure dans Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Créer une application web Hello World pour Azure dans IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Lors de l’installation hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-installation.md
[Lors de l’installation Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[instructions connectez-vous pour hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Instructions d’authentification pour hello boîte à outils Azure pour IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Nouveautés de hello boîte à outils Azure pour Eclipse]: ./azure-toolkit-for-eclipse-whats-new.md
[Quelles sont les nouveautés Bonjour Azure Toolkit pour IntelliJ]: ./azure-toolkit-for-intellij-whats-new.md

[Centre de développement Java pour Azure]: https://azure.microsoft.com/develop/java/
[Outils Java pour Visual Studio Team Services]: https://java.visualstudio.com/

[Tailles des machines virtuelles Windows dans Azure]: /azure/virtual-machines/virtual-machines-windows-sizes
[Tailles des machines virtuelles Linux dans Azure]: /azure/virtual-machines/virtual-machines-linux-sizes
[Tarification des machines virtuelles Windows]: /pricing/details/virtual-machines/windows/
[Tarification des machines virtuelles Linux]: /pricing/details/virtual-machines/linux/

<!-- IMG List -->

[RE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE01.png
[RE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/RE02.png

[SH01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH01.png
[SH02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/SH02.png

[DE01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE01.png
[DE02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/DE02.png

[CR01]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR01.png
[CR02]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR02.png
[CR03]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR03.png
[CR04]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR04.png
[CR05]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR05.png
[CR06]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR06.png
[CR07]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR07.png
[CR08]: ./media/azure-toolkit-for-eclipse-managing-virtual-machines-using-azure-explorer/CR08.png
