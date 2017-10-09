---
title: "passerelle de données locale aaaInstall | Documents Microsoft"
description: "Découvrez comment tooinstall et configurez une passerelle de données local."
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
ms.openlocfilehash: e2878bf765c82910d452ae2cdd9264a343ec1990
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-an-on-premises-data-gateway"></a><span data-ttu-id="38aff-103">Installer et configurer une passerelle de données locale</span><span class="sxs-lookup"><span data-stu-id="38aff-103">Install and configure an on-premises data gateway</span></span>
<span data-ttu-id="38aff-104">Une passerelle de données local est requise lorsqu’un ou plusieurs serveurs Azure Analysis Services dans hello même région de se connecter à des sources de données tooon local.</span><span class="sxs-lookup"><span data-stu-id="38aff-104">An on-premises data gateway is required when one or more Azure Analysis Services servers in hello same region connect tooon-premises data sources.</span></span> <span data-ttu-id="38aff-105">toolearn en savoir plus sur la passerelle de hello, consultez [passerelle de données locale](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="38aff-105">toolearn more about hello gateway, see [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38aff-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="38aff-106">Prerequisites</span></span>
<span data-ttu-id="38aff-107">**Configuration minimale requise :**</span><span class="sxs-lookup"><span data-stu-id="38aff-107">**Minimum Requirements:**</span></span>

* <span data-ttu-id="38aff-108">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="38aff-108">.NET 4.5 Framework</span></span>
* <span data-ttu-id="38aff-109">Version 64 bits de Windows 7 / Windows Server 2008 R2 (ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="38aff-109">64-bit version of Windows 7 / Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="38aff-110">**Recommandé :**</span><span class="sxs-lookup"><span data-stu-id="38aff-110">**Recommended:**</span></span>

* <span data-ttu-id="38aff-111">Processeur 8 cœurs</span><span class="sxs-lookup"><span data-stu-id="38aff-111">8 Core CPU</span></span>
* <span data-ttu-id="38aff-112">8 Go de mémoire</span><span class="sxs-lookup"><span data-stu-id="38aff-112">8 GB Memory</span></span>
* <span data-ttu-id="38aff-113">Version 64 bits de Windows 2012 R2 (ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="38aff-113">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="38aff-114">**Points importants à prendre en compte :**</span><span class="sxs-lookup"><span data-stu-id="38aff-114">**Important considerations:**</span></span>

* <span data-ttu-id="38aff-115">Pendant l’installation, lors de l’inscription de votre passerelle avec Azure, la région par défaut hello pour votre abonnement est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="38aff-115">During setup, when registering your gateway with Azure, hello default region for your subscription is selected.</span></span> <span data-ttu-id="38aff-116">Vous pouvez choisir une autre région.</span><span class="sxs-lookup"><span data-stu-id="38aff-116">You can choose a different region.</span></span> <span data-ttu-id="38aff-117">Si vous avez des serveurs dans plusieurs régions, vous devez installer une passerelle pour chaque région.</span><span class="sxs-lookup"><span data-stu-id="38aff-117">If you have servers in more than one region, you must install a gateway for each region.</span></span> 
* <span data-ttu-id="38aff-118">passerelle de Hello ne peut pas être installé sur un contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="38aff-118">hello gateway cannot be installed on a domain controller.</span></span>
* <span data-ttu-id="38aff-119">Une seule passerelle peut être installée sur un ordinateur.</span><span class="sxs-lookup"><span data-stu-id="38aff-119">Only one gateway can be installed on a single computer.</span></span>
* <span data-ttu-id="38aff-120">Installez la passerelle de hello sur un ordinateur qui reste sur et ne passe pas toosleep.</span><span class="sxs-lookup"><span data-stu-id="38aff-120">Install hello gateway on a computer that remains on and does not go toosleep.</span></span>
* <span data-ttu-id="38aff-121">N’installez pas de passerelle de hello sur un réseau d’ordinateurs connectés sans fil tooyour.</span><span class="sxs-lookup"><span data-stu-id="38aff-121">Do not install hello gateway on a computer wirelessly connected tooyour network.</span></span> <span data-ttu-id="38aff-122">Les performances peuvent être réduites.</span><span class="sxs-lookup"><span data-stu-id="38aff-122">Performance can be diminished.</span></span>


## <span data-ttu-id="38aff-123"><a name="download"></a>Télécharger</span><span class="sxs-lookup"><span data-stu-id="38aff-123"><a name="download"></a>Download</span></span>
 [<span data-ttu-id="38aff-124">Télécharger hello passerelle</span><span class="sxs-lookup"><span data-stu-id="38aff-124">Download hello gateway</span></span>](https://aka.ms/azureasgateway)

## <span data-ttu-id="38aff-125"><a name="install"></a>Installer</span><span class="sxs-lookup"><span data-stu-id="38aff-125"><a name="install"></a>Install</span></span>

1. <span data-ttu-id="38aff-126">Exécutez le programme d’installation.</span><span class="sxs-lookup"><span data-stu-id="38aff-126">Run setup.</span></span>

2. <span data-ttu-id="38aff-127">Sélectionnez un emplacement, acceptez les termes du contrat de hello, puis cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="38aff-127">Select a location, accept hello terms, and then click **Install**.</span></span>

   ![Emplacement d’installation et termes du contrat de licence](media/analysis-services-gateway-install/aas-gateway-installer-accept.png)

3. <span data-ttu-id="38aff-129">Sélectionnez **Passerelle de données locale (recommandé)**.</span><span class="sxs-lookup"><span data-stu-id="38aff-129">Select **On-premises data gateway (recommended)**.</span></span> <span data-ttu-id="38aff-130">Azure Analysis Services ne prend pas en charge le mode personnel.</span><span class="sxs-lookup"><span data-stu-id="38aff-130">Azure Analysis Services does not support personal mode.</span></span>

   ![Choisir le type de passerelle](media/analysis-services-gateway-install/aas-gateway-installer-shared.png)

4. <span data-ttu-id="38aff-132">Entrez un compte toosign dans tooAzure.</span><span class="sxs-lookup"><span data-stu-id="38aff-132">Enter an account toosign in tooAzure.</span></span> <span data-ttu-id="38aff-133">compte de Hello doit être dans Azure Active Directory votre locataire.</span><span class="sxs-lookup"><span data-stu-id="38aff-133">hello account must be in your tenant's Azure Active Directory.</span></span> <span data-ttu-id="38aff-134">Ce compte est utilisé pour l’administrateur de la passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="38aff-134">This account is used for hello gateway administrator.</span></span> 

   ![Entrez un compte toosign dans tooAzure](media/analysis-services-gateway-install/aas-gateway-installer-account.png)

   > [!NOTE]
   > <span data-ttu-id="38aff-136">Si vous vous connectez avec un compte de domaine, il sera mappé tooyour compte de société dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38aff-136">If you sign in with a domain account, it will be mapped tooyour organizational account in Azure AD.</span></span> <span data-ttu-id="38aff-137">Votre compte professionnel sera utilisé en tant qu’administrateur de passerelle hello hello.</span><span class="sxs-lookup"><span data-stu-id="38aff-137">Your organizational account will be used as hello hello gateway administrator.</span></span>

## <span data-ttu-id="38aff-138"><a name="register"></a>S’inscrire</span><span class="sxs-lookup"><span data-stu-id="38aff-138"><a name="register"></a>Register</span></span>
<span data-ttu-id="38aff-139">Dans l’ordre toocreate une ressource de passerelle dans Azure, vous devez inscrire l’instance locale de hello que vous installé avec hello Service Cloud de passerelle.</span><span class="sxs-lookup"><span data-stu-id="38aff-139">In order toocreate a gateway resource in Azure, you must register hello local instance you installed with hello Gateway Cloud Service.</span></span> 

1.  <span data-ttu-id="38aff-140">Sélectionnez **Inscrivez une nouvelle passerelle sur cet ordinateur**.</span><span class="sxs-lookup"><span data-stu-id="38aff-140">Select **Register a new gateway on this computer**.</span></span>

    ![S’inscrire](media/analysis-services-gateway-install/aas-gateway-register-new.png)

2. <span data-ttu-id="38aff-142">Saisissez un nom et une clé de récupération pour votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="38aff-142">Type a name and recovery key for your gateway.</span></span> <span data-ttu-id="38aff-143">Par défaut, la passerelle de hello utilise la région par défaut de votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="38aff-143">By default, hello gateway uses your subscription's default region.</span></span> <span data-ttu-id="38aff-144">Si vous avez besoin de tooselect une autre région, sélectionnez **modification région**.</span><span class="sxs-lookup"><span data-stu-id="38aff-144">If you need tooselect a different region, select **Change Region**.</span></span>

   ![S’inscrire](media/analysis-services-gateway-install/aas-gateway-register-name.png)


## <span data-ttu-id="38aff-146"><a name="create-resource"></a>Créer une ressource de passerelle Azure</span><span class="sxs-lookup"><span data-stu-id="38aff-146"><a name="create-resource"></a>Create an Azure gateway resource</span></span>
<span data-ttu-id="38aff-147">Une fois que vous avez installé et inscrit votre passerelle, vous devez toocreate une ressource de passerelle dans votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="38aff-147">After you've installed and registered your gateway, you need toocreate a gateway resource in your Azure subscription.</span></span> <span data-ttu-id="38aff-148">Se connecter tooAzure avec hello même compte que celui utilisé lors de l’inscription de passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="38aff-148">Sign in tooAzure with hello same account you used when registering hello gateway.</span></span>

1. <span data-ttu-id="38aff-149">Dans le portail Azure, cliquez sur **Création d’un nouveau service** > **Enterprise Integration** > **Passerelle de données locale** > **Créer**.</span><span class="sxs-lookup"><span data-stu-id="38aff-149">In Azure portal, click **Create a new service** > **Enterprise Integration** > **On-premises data gateway** > **Create**.</span></span>

   ![Créer une ressource de passerelle](media/analysis-services-gateway-install/aas-gateway-new-azure-resource.png)

2. <span data-ttu-id="38aff-151">Dans **Créer une passerelle connexion**, entrez les paramètres suivants:</span><span class="sxs-lookup"><span data-stu-id="38aff-151">In **Create connection gateway**, enter these settings:</span></span>

    * <span data-ttu-id="38aff-152">**Nom** : entrez un nom pour votre ressource de passerelle.</span><span class="sxs-lookup"><span data-stu-id="38aff-152">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="38aff-153">**Abonnement**: sélectionnez hello tooassociate abonnement Azure avec votre ressource de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="38aff-153">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="38aff-154">Cet abonnement doit être hello même abonnement que vos serveurs sont dans.</span><span class="sxs-lookup"><span data-stu-id="38aff-154">This subscription should be hello same subscription your servers are in.</span></span>
   
      <span data-ttu-id="38aff-155">abonnement de Hello par défaut est basée sur hello compte Azure que vous avez utilisé toosign dans.</span><span class="sxs-lookup"><span data-stu-id="38aff-155">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="38aff-156">**Groupe de ressources** : créez un groupe de ressources ou sélectionnez-en un.</span><span class="sxs-lookup"><span data-stu-id="38aff-156">**Resource group**: Create a resource group or select an existing resource group.</span></span>

    * <span data-ttu-id="38aff-157">**Emplacement**: vous avez inscrit votre passerelle dans la région sélectionnez hello.</span><span class="sxs-lookup"><span data-stu-id="38aff-157">**Location**: Select hello region you registered your gateway in.</span></span>

    * <span data-ttu-id="38aff-158">**Nom de l’installation**: Si votre installation de la passerelle n’est pas déjà sélectionnée, sélectionnez hello enregistrée.</span><span class="sxs-lookup"><span data-stu-id="38aff-158">**Installation Name**: If your gateway installation isn't already selected, select hello gateway registered.</span></span> 

    <span data-ttu-id="38aff-159">Une fois ces opérations effectuées, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="38aff-159">When you're done, click **Create**.</span></span>

## <span data-ttu-id="38aff-160"><a name="connect-servers"></a>Connecter des ressources de serveurs toohello passerelle</span><span class="sxs-lookup"><span data-stu-id="38aff-160"><a name="connect-servers"></a>Connect servers toohello gateway resource</span></span>

1. <span data-ttu-id="38aff-161">Dans la vue d’ensemble du serveur Azure Analysis Services, cliquez sur **Passerelle de données locale**.</span><span class="sxs-lookup"><span data-stu-id="38aff-161">In your Azure Analysis Services server overview, click **On-Premises Data Gateway**.</span></span>

   ![Se connecter toogateway de serveur](media/analysis-services-gateway-install/aas-gateway-connect-server.png)

2. <span data-ttu-id="38aff-163">Dans **choisir une passerelle de données locale de tooconnect**, sélectionnez votre ressource de passerelle, puis cliquez sur **passerelle sélectionné de connexion**.</span><span class="sxs-lookup"><span data-stu-id="38aff-163">In **Pick an On-Premises Data Gateway tooconnect**, select your gateway resource, and then click **Connect selected gateway**.</span></span>

   ![Se connecter toogateway ressource du serveur](media/analysis-services-gateway-install/aas-gateway-connect-resource.png)

    > [!NOTE]
    > <span data-ttu-id="38aff-165">Si votre passerelle n’apparaît pas dans la liste de hello, votre serveur est probablement pas dans hello même région que vous avez spécifié lors de l’inscription de passerelle de hello de région de hello.</span><span class="sxs-lookup"><span data-stu-id="38aff-165">If your gateway does not appear in hello list, your server is likely not in hello same region as hello region you specified when registering hello gateway.</span></span> 

<span data-ttu-id="38aff-166">Vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="38aff-166">That's it.</span></span> <span data-ttu-id="38aff-167">Si vous avez besoin de tooopen ports ou que vous effectuez un dépannage, être vraiment toocheck out [passerelle de données locale](analysis-services-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="38aff-167">If you need tooopen ports or do any troubleshooting, be sure toocheck out [On-premises data gateway](analysis-services-gateway.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="38aff-168">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="38aff-168">Next steps</span></span>
* [<span data-ttu-id="38aff-169">Gérer Analysis Services</span><span class="sxs-lookup"><span data-stu-id="38aff-169">Manage Analysis Services</span></span>](analysis-services-manage.md)   
* [<span data-ttu-id="38aff-170">Obtenir les données d’Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="38aff-170">Get data from Azure Analysis Services</span></span>](analysis-services-connect.md)
