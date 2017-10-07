---
title: "aaaUsing Bureau à distance avec des rôles Azure | Documents Microsoft"
description: "Utilisation du Bureau à distance avec des rôles Azure"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d35fd421cde8be9e3caa474db95974a54e528bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a><span data-ttu-id="76b8b-103">Utilisation du Bureau à distance avec des rôles Azure</span><span class="sxs-lookup"><span data-stu-id="76b8b-103">Using Remote Desktop with Azure Roles</span></span>
<span data-ttu-id="76b8b-104">À l’aide de hello Azure SDK et des Services Bureau à distance, vous pouvez accéder à des rôles Azure et les machines virtuelles qui sont hébergées par Azure.</span><span class="sxs-lookup"><span data-stu-id="76b8b-104">By using hello Azure SDK and Remote Desktop Services, you can access Azure roles and virtual machines that are hosted by Azure.</span></span> <span data-ttu-id="76b8b-105">Dans Visual Studio, vous pouvez configurer les Services Bureau à distance à partir d’un projet de service cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="76b8b-105">In Visual Studio, you can configure Remote Desktop Services from an Azure cloud service project.</span></span> <span data-ttu-id="76b8b-106">tooenable des Services Bureau à distance, vous devez créer un projet de travail qui contient un ou plusieurs rôles et publiez-le tooAzure.</span><span class="sxs-lookup"><span data-stu-id="76b8b-106">tooenable Remote Desktop Services, you must create a working project that contains one or more roles and then publish it tooAzure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76b8b-107">L’accès aux rôles Azure est réservé au dépannage et au développement.</span><span class="sxs-lookup"><span data-stu-id="76b8b-107">You should access an Azure role for troubleshooting or development only.</span></span> <span data-ttu-id="76b8b-108">Hello d’objet de chaque machine virtuelle est toorun un rôle spécifique dans votre application Windows Azure, toorun pas les autres applications clientes.</span><span class="sxs-lookup"><span data-stu-id="76b8b-108">hello purpose of each virtual machine is toorun a specific role in your Azure application, not toorun other client applications.</span></span> <span data-ttu-id="76b8b-109">Si vous souhaitez toouse Azure toohost une machine virtuelle que vous pouvez utiliser d’autres fins, reportez-vous à l’accès à des Machines virtuelles Azure à partir de l’Explorateur de serveurs.</span><span class="sxs-lookup"><span data-stu-id="76b8b-109">If you want toouse Azure toohost a virtual machine that you can use for any purpose, see Accessing Azure Virtual Machines from Server Explorer.</span></span>
> 
> 

## <a name="tooenable-and-use-remote-desktop-for-an-azure-role"></a><span data-ttu-id="76b8b-110">tooenable et utilisez Bureau à distance pour un rôle Azure</span><span class="sxs-lookup"><span data-stu-id="76b8b-110">tooenable and use Remote Desktop for an Azure Role</span></span>
1. <span data-ttu-id="76b8b-111">Dans l’Explorateur de solutions, ouvrez le menu contextuel de hello pour votre projet de service cloud, puis choisissez **publier**.</span><span class="sxs-lookup"><span data-stu-id="76b8b-111">In Solution Explorer, open hello shortcut menu for your cloud service project, and then choose **Publish**.</span></span>
   
    <span data-ttu-id="76b8b-112">Hello **publier l’Application Azure** Assistant s’affiche.</span><span class="sxs-lookup"><span data-stu-id="76b8b-112">hello **Publish Azure Application** wizard appears.</span></span>
   
    ![Commande Publier pour un projet de service cloud](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. <span data-ttu-id="76b8b-114">Bas hello **paramètres de publication Microsoft Azure** page d’Assistant hello, sélectionnez hello **activer le Bureau à distance** pour tous les rôles case à cocher.</span><span class="sxs-lookup"><span data-stu-id="76b8b-114">At hello bottom of **Microsoft Azure Publish Settings** page of hello wizard, select hello **Enable Remote Desktop** for all roles check box.</span></span> 
   
    <span data-ttu-id="76b8b-115">Hello **Configuration Bureau à distance** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="76b8b-115">hello **Remote Desktop Configuration** dialog box appears.</span></span>
3. <span data-ttu-id="76b8b-116">En bas de hello Hello **Configuration Bureau à distance** boîte de dialogue, choisissez hello **plus d’Options** bouton.</span><span class="sxs-lookup"><span data-stu-id="76b8b-116">At hello bottom of hello **Remote Desktop Configuration** dialog box, choose hello **More Options** button.</span></span> 
   
    <span data-ttu-id="76b8b-117">Cela affiche une liste déroulante qui vous permet de créer ou de sélectionner un certificat afin de chiffrer les informations d'identification lors de la connexion Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="76b8b-117">This displays a dropdown list box that lets you create or choose a certificate so that you can encrypt credentials information when connecting via remote desktop.</span></span>
4. <span data-ttu-id="76b8b-118">Dans la liste déroulante de hello, choisissez  **&lt;créer >**, ou choisissez un certificat existant à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="76b8b-118">In hello dropdown list, choose **&lt;Create>**, or choose an existing one from hello list.</span></span> 
   
    <span data-ttu-id="76b8b-119">Si vous choisissez un certificat existant, ignorez hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="76b8b-119">If you choose an existing certificate, skip hello following steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="76b8b-120">les certificats de Hello dont vous avez besoin pour une connexion Bureau à distance sont différents de certificats hello que vous utilisez pour d’autres opérations Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="76b8b-120">hello certificates that you need for a remote desktop connection are different from hello certificates that you use for other Azure operations.</span></span> <span data-ttu-id="76b8b-121">certificat d’accès à distance Hello doit avoir une clé privée.</span><span class="sxs-lookup"><span data-stu-id="76b8b-121">hello remote access certificate must have a private key.</span></span>
   > 
   > 
   
    <span data-ttu-id="76b8b-122">Hello **Create Certificate** boîte de dialogue s’affiche.</span><span class="sxs-lookup"><span data-stu-id="76b8b-122">hello **Create Certificate** dialog box appears.</span></span>
   
   1. <span data-ttu-id="76b8b-123">Fournissez un nom convivial pour le nouveau certificat de hello, puis choisissez hello **OK** bouton.</span><span class="sxs-lookup"><span data-stu-id="76b8b-123">Provide a friendly name for hello new certificate, and then choose hello **OK** button.</span></span> <span data-ttu-id="76b8b-124">Hello nouveau certificat apparaît dans la zone de liste déroulante hello.</span><span class="sxs-lookup"><span data-stu-id="76b8b-124">hello new certificate appears in hello dropdown list box.</span></span>
   2. <span data-ttu-id="76b8b-125">Bonjour **Configuration Bureau à distance** boîte de dialogue zone, fournissez un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="76b8b-125">In hello **Remote Desktop Configuration** dialog box, provide a user name and a password.</span></span>
      
       <span data-ttu-id="76b8b-126">Vous ne pouvez pas utiliser un compte existant.</span><span class="sxs-lookup"><span data-stu-id="76b8b-126">You can’t use an existing account.</span></span> <span data-ttu-id="76b8b-127">Ne spécifiez pas administrateur comme nom d’utilisateur de hello pour hello nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="76b8b-127">Don’t specify Administrator as hello user name for hello new account.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="76b8b-128">Si le mot de passe hello ne répond pas aux exigences de complexité hello, une icône rouge apparaît la zone de texte de mot de passe toohello suivante.</span><span class="sxs-lookup"><span data-stu-id="76b8b-128">If hello password doesn’t meet hello complexity requirements, a red icon appears next toohello password text box.</span></span> <span data-ttu-id="76b8b-129">mot de passe Hello doit inclure des lettres majuscules, lettres minuscules et nombres ou des symboles.</span><span class="sxs-lookup"><span data-stu-id="76b8b-129">hello password must include capital letters, lowercase letters, and numbers or symbols.</span></span>
      > 
      > 
   3. <span data-ttu-id="76b8b-130">Choisissez une date sur le compte hello expirera et après les connexions Bureau à distance seront bloquées.</span><span class="sxs-lookup"><span data-stu-id="76b8b-130">Choose a date on which hello account will expire and after which remote desktop connections will be blocked.</span></span>
   4. <span data-ttu-id="76b8b-131">Une fois que vous avez fourni toutes les hello les informations requises, choisissez hello **OK** bouton.</span><span class="sxs-lookup"><span data-stu-id="76b8b-131">After you've provided all hello required information, choose hello **OK** button.</span></span>
      
       <span data-ttu-id="76b8b-132">Plusieurs paramètres qui activent les Services d’accès distant sont ajoutés les fichiers .cscfg et .csdef toohello.</span><span class="sxs-lookup"><span data-stu-id="76b8b-132">Several settings that enable Remote Access Services are added toohello .cscfg and .csdef files.</span></span>
5. <span data-ttu-id="76b8b-133">Bonjour **paramètres de publication Microsoft Azure** Assistant, choisissez hello **OK** bouton quand vous êtes prêt à toopublish votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="76b8b-133">In hello **Microsoft Azure Publish Settings** wizard, choose hello **OK** button when you’re ready toopublish your cloud service.</span></span>
   
    <span data-ttu-id="76b8b-134">Si vous n’êtes pas prêt toopublish, choisissez hello **Annuler** bouton.</span><span class="sxs-lookup"><span data-stu-id="76b8b-134">If you're not ready toopublish, choose hello **Cancel** button.</span></span> <span data-ttu-id="76b8b-135">paramètres de configuration Hello sont enregistrés, et vous pouvez publier votre service cloud ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="76b8b-135">hello configuration settings are saved, and you can publish your cloud service later.</span></span>

## <a name="connect-tooan-azure-role-by-using-remote-desktop"></a><span data-ttu-id="76b8b-136">Se connecter tooan rôle Azure à l’aide du Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="76b8b-136">Connect tooan Azure Role by using Remote Desktop</span></span>
<span data-ttu-id="76b8b-137">Après avoir publié votre service cloud sur Azure, vous pouvez utiliser l’Explorateur de serveurs toolog dans les machines virtuelles hello hébergée par Azure.</span><span class="sxs-lookup"><span data-stu-id="76b8b-137">After you publish your cloud service on Azure, you can use Server Explorer toolog into hello virtual machines that Azure hosts.</span></span> 

1. <span data-ttu-id="76b8b-138">Dans l’Explorateur de serveurs, développez hello **Azure** nœud, puis développez le nœud hello pour un service cloud et un de ses rôles de toodisplay une liste d’instances.</span><span class="sxs-lookup"><span data-stu-id="76b8b-138">In Server Explorer, expand hello **Azure** node, and then expand hello node for a cloud service and one of its roles toodisplay a list of instances.</span></span>
2. <span data-ttu-id="76b8b-139">Ouvrez le menu contextuel de hello pour un nœud d’instance, puis choisissez **connexion de bureau à distance à l’aide de**.</span><span class="sxs-lookup"><span data-stu-id="76b8b-139">Open hello shortcut menu for an instance node, and then choose **Connect Using Remote Desktop**.</span></span>
   
    ![Connexion Bureau à distance](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. <span data-ttu-id="76b8b-141">Entrez le nom d’utilisateur hello et un mot de passe que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="76b8b-141">Enter hello user name and password that you created previously.</span></span> <span data-ttu-id="76b8b-142">Vous êtes maintenant connecté à votre session à distance.</span><span class="sxs-lookup"><span data-stu-id="76b8b-142">You are now logged into your remote session.</span></span>

