---
title: "Installer une passerelle de données locale | Microsoft Docs"
description: "Découvrez comment installer et configurer une passerelle de données locale."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/22/2017
ms.author: owend
ms.openlocfilehash: 6ef296fb98478be9240f0231c8ad39cd2a0af995
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a><span data-ttu-id="b1b31-103">Installer et configurer une passerelle de données locale</span><span class="sxs-lookup"><span data-stu-id="b1b31-103">Install and configure an on-premises data gateway</span></span>
<span data-ttu-id="b1b31-104">Une passerelle de données locale est requise lorsqu’un ou plusieurs serveurs Azure Analysis Services de la même région se connectent aux sources de données locales.</span><span class="sxs-lookup"><span data-stu-id="b1b31-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in the same region connect to on-premises data sources.</span></span> <span data-ttu-id="b1b31-105">Pour en savoir plus sur la passerelle, consultez la page [Passerelle de données locale](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="b1b31-105">To learn more about the gateway, see [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1b31-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b1b31-106">Prerequisites</span></span>
<span data-ttu-id="b1b31-107">**Configuration minimale requise :**</span><span class="sxs-lookup"><span data-stu-id="b1b31-107">**Minimum Requirements:**</span></span>

* <span data-ttu-id="b1b31-108">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="b1b31-108">.NET 4.5 Framework</span></span>
* <span data-ttu-id="b1b31-109">Version 64 bits de Windows 7 / Windows Server 2008 R2 (ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="b1b31-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="b1b31-110">**Recommandé :**</span><span class="sxs-lookup"><span data-stu-id="b1b31-110">**Recommended:**</span></span>

* <span data-ttu-id="b1b31-111">Processeur 8 cœurs</span><span class="sxs-lookup"><span data-stu-id="b1b31-111">8 Core CPU</span></span>
* <span data-ttu-id="b1b31-112">8 Go de mémoire</span><span class="sxs-lookup"><span data-stu-id="b1b31-112">8 GB Memory</span></span>
* <span data-ttu-id="b1b31-113">Version 64 bits de Windows 2012 R2 (ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="b1b31-113">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="b1b31-114">**Points importants à prendre en compte :**</span><span class="sxs-lookup"><span data-stu-id="b1b31-114">**Important considerations:**</span></span>

* <span data-ttu-id="b1b31-115">Pendant la configuration, lors de l’inscription de votre passerelle auprès d’Azure, la région par défaut de votre abonnement est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="b1b31-115">During setup, when registering your gateway with Azure, the default region for your subscription is selected.</span></span> <span data-ttu-id="b1b31-116">Vous pouvez choisir une autre région.</span><span class="sxs-lookup"><span data-stu-id="b1b31-116">You can choose a different region.</span></span> <span data-ttu-id="b1b31-117">Si vous avez des serveurs dans plusieurs régions, vous devez installer une passerelle pour chaque région.</span><span class="sxs-lookup"><span data-stu-id="b1b31-117">If you have servers in more than one region, you must install a gateway for each region.</span></span> 
* <span data-ttu-id="b1b31-118">La passerelle ne peut pas être installée sur un contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="b1b31-118">The gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="b1b31-119">Une seule passerelle peut être installée sur un ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b1b31-119">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="b1b31-120">Installez la passerelle sur un ordinateur qui reste activé et qui ne se met pas en veille.</span><span class="sxs-lookup"><span data-stu-id="b1b31-120">Install the gateway on a computer that remains on and does not go to sleep.</span></span>
* <span data-ttu-id="b1b31-121">N’installez pas la passerelle sur un ordinateur sans fil connecté à votre réseau.</span><span class="sxs-lookup"><span data-stu-id="b1b31-121">Do not install the gateway on a computer wirelessly connected to your network.</span></span> <span data-ttu-id="b1b31-122">Les performances peuvent être réduites.</span><span class="sxs-lookup"><span data-stu-id="b1b31-122">Performance can be diminished.</span></span>


## <span data-ttu-id="b1b31-123"><a name="download"></a>Télécharger</span><span class="sxs-lookup"><span data-stu-id="b1b31-123"><a name="download"></a>Download</span></span>
 [<span data-ttu-id="b1b31-124">Télécharger la passerelle</span><span class="sxs-lookup"><span data-stu-id="b1b31-124">Download the gateway</span></span>](https://aka.ms/azureasgateway)

## <span data-ttu-id="b1b31-125"><a name="install"></a>Installer</span><span class="sxs-lookup"><span data-stu-id="b1b31-125"><a name="install"></a>Install</span></span>

1. <span data-ttu-id="b1b31-126">Exécutez le programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="b1b31-126">Run setup.</span></span>

2. <span data-ttu-id="b1b31-127">Sélectionnez un emplacement, acceptez les termes du contrat, puis cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="b1b31-127">Select a location, accept the terms, and then click **Install**.</span></span>

   ![Emplacement d’installation et termes du contrat de licence](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. <span data-ttu-id="b1b31-129">Sélectionnez **Passerelle de données locale (recommandé)**.</span><span class="sxs-lookup"><span data-stu-id="b1b31-129">Select **On-premises data gateway (recommended)**.</span></span> <span data-ttu-id="b1b31-130">Azure Analysis Services ne prend pas en charge le mode personnel.</span><span class="sxs-lookup"><span data-stu-id="b1b31-130">Azure Analysis Services does not support personal mode.</span></span>

   ![Choisir le type de passerelle](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. <span data-ttu-id="b1b31-132">Entrez un compte pour vous connecter à Azure.</span><span class="sxs-lookup"><span data-stu-id="b1b31-132">Enter an account to sign in to Azure.</span></span> <span data-ttu-id="b1b31-133">Le compte doit se trouver dans l’Azure Active Directory de votre locataire.</span><span class="sxs-lookup"><span data-stu-id="b1b31-133">The account must be in your tenant's Azure Active Directory.</span></span> <span data-ttu-id="b1b31-134">Ce compte est utilisé pour l’administrateur de passerelle.</span><span class="sxs-lookup"><span data-stu-id="b1b31-134">This account is used for the gateway administrator.</span></span> 

   ![Entrer un compte pour vous connecter à Azure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > <span data-ttu-id="b1b31-136">Si vous vous connectez avec un compte de domaine, il sera mappé à votre compte professionnel dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b1b31-136">If you sign in with a domain account, it will be mapped to your organizational account in Azure AD.</span></span> <span data-ttu-id="b1b31-137">Votre compte professionnel sert de compte d’administrateur de passerelle.</span><span class="sxs-lookup"><span data-stu-id="b1b31-137">Your organizational account will be used as the the gateway administrator.</span></span>

## <span data-ttu-id="b1b31-138"><a name="register"></a>S’inscrire</span><span class="sxs-lookup"><span data-stu-id="b1b31-138"><a name="register"></a>Register</span></span>
<span data-ttu-id="b1b31-139">Pour créer une ressource de passerelle dans Azure, vous devez inscrire l’instance locale que vous avez installée auprès du service cloud de passerelle.</span><span class="sxs-lookup"><span data-stu-id="b1b31-139">In order to create a gateway resource in Azure, you must register the local instance you installed with the Gateway Cloud Service.</span></span> 

1.  <span data-ttu-id="b1b31-140">Sélectionnez **Inscrivez une nouvelle passerelle sur cet ordinateur**.</span><span class="sxs-lookup"><span data-stu-id="b1b31-140">Select **Register a new gateway on this computer**.</span></span>

    ![S’inscrire](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. <span data-ttu-id="b1b31-142">Saisissez un nom et une clé de récupération pour votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="b1b31-142">Type a name and recovery key for your gateway.</span></span> <span data-ttu-id="b1b31-143">Par défaut, la passerelle utilise la région par défaut de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="b1b31-143">By default, the gateway uses your subscription's default region.</span></span> <span data-ttu-id="b1b31-144">Si vous souhaitez choisir une autre région, sélectionnez **Changer la région**.</span><span class="sxs-lookup"><span data-stu-id="b1b31-144">If you need to select a different region, select **Change Region**.</span></span>

   ![S’inscrire](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <span data-ttu-id="b1b31-146"><a name="create-resource"></a>Créer une ressource de passerelle Azure</span><span class="sxs-lookup"><span data-stu-id="b1b31-146"><a name="create-resource"></a>Create an Azure gateway resource</span></span>
<span data-ttu-id="b1b31-147">Une fois que vous avez installé et inscrit votre passerelle, vous devez créer une ressource de passerelle dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="b1b31-147">After you've installed and registered your gateway, you need to create a gateway resource in your Azure subscription.</span></span> <span data-ttu-id="b1b31-148">Connectez-vous à Azure avec le même compte que celui utilisé lors de l’inscription de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="b1b31-148">Sign in to Azure with the same account you used when registering the gateway.</span></span>

1. <span data-ttu-id="b1b31-149">Dans le portail Azure, cliquez sur **Création d’un nouveau service** > **Enterprise Integration** > **Passerelle de données locale** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b1b31-149">In Azure portal, click **Create a new service** > **Enterprise Integration** > **On-premises data gateway** > **Create**.</span></span>

   ![Créer une ressource de passerelle](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. <span data-ttu-id="b1b31-151">Dans **Créer une passerelle connexion**, entrez les paramètres suivants:</span><span class="sxs-lookup"><span data-stu-id="b1b31-151">In **Create connection gateway**, enter these settings:</span></span>

    * <span data-ttu-id="b1b31-152">**Nom** : entrez un nom pour votre ressource de passerelle.</span><span class="sxs-lookup"><span data-stu-id="b1b31-152">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="b1b31-153">**Abonnement** : sélectionnez l’abonnement Azure à associer à votre ressource de passerelle.</span><span class="sxs-lookup"><span data-stu-id="b1b31-153">**Subscription**: Select the Azure subscription to associate with your gateway resource.</span></span> 
    <span data-ttu-id="b1b31-154">Cet abonnement doit être le même que celui de vos serveurs.</span><span class="sxs-lookup"><span data-stu-id="b1b31-154">This subscription should be the same subscription your servers are in.</span></span>
   
      <span data-ttu-id="b1b31-155">L’abonnement par défaut est basé sur le compte Azure que vous avez utilisé pour vous connecter.</span><span class="sxs-lookup"><span data-stu-id="b1b31-155">The default subscription is based on the Azure account that you used to sign in.</span></span>

    * <span data-ttu-id="b1b31-156">**Groupe de ressources** : créez un groupe de ressources ou sélectionnez-en un.</span><span class="sxs-lookup"><span data-stu-id="b1b31-156">**Resource group**: Create a resource group or select an existing resource group.</span></span>

    * <span data-ttu-id="b1b31-157">**Emplacement** : sélectionnez la région dans laquelle vous avez inscrit votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="b1b31-157">**Location**: Select the region you registered your gateway in.</span></span>

    * <span data-ttu-id="b1b31-158">**Nom de l’installation** : si votre installation de passerelle n’est pas encore sélectionnée, sélectionnez la passerelle que vous avez inscrite.</span><span class="sxs-lookup"><span data-stu-id="b1b31-158">**Installation Name**: If your gateway installation isn't already selected, select the gateway registered.</span></span> 

    <span data-ttu-id="b1b31-159">Une fois ces opérations effectuées, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="b1b31-159">When you're done, click **Create**.</span></span>

## <span data-ttu-id="b1b31-160"><a name="connect-servers"></a>Connecter les serveurs à la ressource de passerelle</span><span class="sxs-lookup"><span data-stu-id="b1b31-160"><a name="connect-servers"></a>Connect servers to the gateway resource</span></span>

1. <span data-ttu-id="b1b31-161">Dans la vue d’ensemble du serveur Azure Analysis Services, cliquez sur **Passerelle de données locale**.</span><span class="sxs-lookup"><span data-stu-id="b1b31-161">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span></span>

   ![Connecter le serveur à la passerelle](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. <span data-ttu-id="b1b31-163">Dans la zone **Pick an On-Premises Data Gateway to connect** (Choisir une passerelle de données locale à connecter), sélectionnez votre ressource de passerelle, puis cliquez sur **Connect selected gateway** (Connecter la passerelle sélectionnée).</span><span class="sxs-lookup"><span data-stu-id="b1b31-163">In **Pick an On-Premises Data Gateway to connect**, select your gateway resource, and then click **Connect selected gateway**.</span></span>

   ![Connecter le serveur à la ressource de passerelle](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > <span data-ttu-id="b1b31-165">Si votre passerelle n’apparaît pas dans la liste, votre serveur se trouve probablement dans une autre région que celle spécifiée lors de l’inscription de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="b1b31-165">If your gateway does not appear in the list, your server is likely not in the same region as the region you specified when registering the gateway.</span></span> 

<span data-ttu-id="b1b31-166">Vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="b1b31-166">That's it.</span></span> <span data-ttu-id="b1b31-167">Si vous devez ouvrir des ports ou effectuer des opérations de dépannage, veillez à consulter la page [Passerelle de données locale](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="b1b31-167">If you need to open ports or do any troubleshooting, be sure to check out [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1b31-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b1b31-168">Next steps</span></span>
* [<span data-ttu-id="b1b31-169">Gérer Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b1b31-169">Manage Analysis Services</span></span>](analysis-services-manage.md)   
* [<span data-ttu-id="b1b31-170">Obtenir les données d’Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="b1b31-170">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
