---
title: "Utilisation du Bureau à distance avec les rôles Azure | Microsoft Docs"
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
ms.openlocfilehash: eab135d10c0d6df8ca72ac47d6804017a998a3d2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a><span data-ttu-id="79a63-103">Utilisation du Bureau à distance avec des rôles Azure</span><span class="sxs-lookup"><span data-stu-id="79a63-103">Using Remote Desktop with Azure Roles</span></span>
<span data-ttu-id="79a63-104">En utilisant le kit de développement logiciel (SDK) Azure et les Services Bureau à distance, vous pouvez accéder aux rôles Azure et aux machines virtuelles hébergées par Azure.</span><span class="sxs-lookup"><span data-stu-id="79a63-104">By using the Azure SDK and Remote Desktop Services, you can access Azure roles and virtual machines that are hosted by Azure.</span></span> <span data-ttu-id="79a63-105">Dans Visual Studio, vous pouvez configurer les Services Bureau à distance à partir d’un projet de service cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="79a63-105">In Visual Studio, you can configure Remote Desktop Services from an Azure cloud service project.</span></span> <span data-ttu-id="79a63-106">Pour activer les Services Bureau à distance, vous devez créer un projet de travail qui contient un ou plusieurs rôles, puis le publier sur Azure.</span><span class="sxs-lookup"><span data-stu-id="79a63-106">To enable Remote Desktop Services, you must create a working project that contains one or more roles and then publish it to Azure.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79a63-107">L’accès aux rôles Azure est réservé au dépannage et au développement.</span><span class="sxs-lookup"><span data-stu-id="79a63-107">You should access an Azure role for troubleshooting or development only.</span></span> <span data-ttu-id="79a63-108">L'objectif de chaque machine virtuelle consiste à exécuter un rôle spécifique dans votre application Azure, et non à exécuter d'autres applications clientes.</span><span class="sxs-lookup"><span data-stu-id="79a63-108">The purpose of each virtual machine is to run a specific role in your Azure application, not to run other client applications.</span></span> <span data-ttu-id="79a63-109">Si vous souhaitez utiliser Azure pour héberger une machine virtuelle que vous pourrez utiliser à d’autres fins, consultez Accès aux machines virtuelles Azure à partir de l'Explorateur de serveurs.</span><span class="sxs-lookup"><span data-stu-id="79a63-109">If you want to use Azure to host a virtual machine that you can use for any purpose, see Accessing Azure Virtual Machines from Server Explorer.</span></span>
> 
> 

## <a name="to-enable-and-use-remote-desktop-for-an-azure-role"></a><span data-ttu-id="79a63-110">Pour activer et utiliser le Bureau à distance pour un rôle Azure</span><span class="sxs-lookup"><span data-stu-id="79a63-110">To enable and use Remote Desktop for an Azure Role</span></span>
1. <span data-ttu-id="79a63-111">Dans l’Explorateur de solutions, ouvrez le menu contextuel de votre projet de service cloud, puis choisissez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="79a63-111">In Solution Explorer, open the shortcut menu for your cloud service project, and then choose **Publish**.</span></span>
   
    <span data-ttu-id="79a63-112">L’Assistant **Publication d’application Azure** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="79a63-112">The **Publish Azure Application** wizard appears.</span></span>
   
    ![Commande Publier pour un projet de service cloud](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. <span data-ttu-id="79a63-114">En bas de la page **Paramètres de publication Microsoft Azure** de l’Assistant, cochez la case **Activer le Bureau à distance** pour tous les rôles.</span><span class="sxs-lookup"><span data-stu-id="79a63-114">At the bottom of **Microsoft Azure Publish Settings** page of the wizard, select the **Enable Remote Desktop** for all roles check box.</span></span> 
   
    <span data-ttu-id="79a63-115">La boîte de dialogue **Configuration du Bureau à distance** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="79a63-115">The **Remote Desktop Configuration** dialog box appears.</span></span>
3. <span data-ttu-id="79a63-116">En bas de la boîte de dialogue **Configuration du Bureau à distance**, sélectionnez le bouton **Plus d’options**.</span><span class="sxs-lookup"><span data-stu-id="79a63-116">At the bottom of the **Remote Desktop Configuration** dialog box, choose the **More Options** button.</span></span> 
   
    <span data-ttu-id="79a63-117">Cela affiche une liste déroulante qui vous permet de créer ou de sélectionner un certificat afin de chiffrer les informations d'identification lors de la connexion Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="79a63-117">This displays a dropdown list box that lets you create or choose a certificate so that you can encrypt credentials information when connecting via remote desktop.</span></span>
4. <span data-ttu-id="79a63-118">Dans la liste déroulante, sélectionnez **&lt;Créer>** ou sélectionnez un certificat existant dans la liste.</span><span class="sxs-lookup"><span data-stu-id="79a63-118">In the dropdown list, choose **&lt;Create>**, or choose an existing one from the list.</span></span> 
   
    <span data-ttu-id="79a63-119">Si vous sélectionnez un certificat existant, ignorez les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="79a63-119">If you choose an existing certificate, skip the following steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="79a63-120">Les certificats dont vous avez besoin pour une connexion Bureau à distance sont différents de ceux que vous utilisez pour d'autres opérations Azure.</span><span class="sxs-lookup"><span data-stu-id="79a63-120">The certificates that you need for a remote desktop connection are different from the certificates that you use for other Azure operations.</span></span> <span data-ttu-id="79a63-121">Le certificat de l'accès à distance doit avoir une clé privée.</span><span class="sxs-lookup"><span data-stu-id="79a63-121">The remote access certificate must have a private key.</span></span>
   > 
   > 
   
    <span data-ttu-id="79a63-122">La boîte de dialogue **Créer un certificat** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="79a63-122">The **Create Certificate** dialog box appears.</span></span>
   
   1. <span data-ttu-id="79a63-123">Donnez un nom convivial au nouveau certificat, puis sélectionnez le bouton **OK** .</span><span class="sxs-lookup"><span data-stu-id="79a63-123">Provide a friendly name for the new certificate, and then choose the **OK** button.</span></span> <span data-ttu-id="79a63-124">Le nouveau certificat s'affiche dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="79a63-124">The new certificate appears in the dropdown list box.</span></span>
   2. <span data-ttu-id="79a63-125">Dans la boîte de dialogue **Configuration du Bureau à distance** , entrez un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="79a63-125">In the **Remote Desktop Configuration** dialog box, provide a user name and a password.</span></span>
      
       <span data-ttu-id="79a63-126">Vous ne pouvez pas utiliser un compte existant.</span><span class="sxs-lookup"><span data-stu-id="79a63-126">You can’t use an existing account.</span></span> <span data-ttu-id="79a63-127">Ne spécifiez pas Administrateur comme nom d'utilisateur pour le nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="79a63-127">Don’t specify Administrator as the user name for the new account.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="79a63-128">Si le mot de passe ne répond pas aux exigences de complexité, une icône rouge apparaît en regard de la zone de texte du mot de passe.</span><span class="sxs-lookup"><span data-stu-id="79a63-128">If the password doesn’t meet the complexity requirements, a red icon appears next to the password text box.</span></span> <span data-ttu-id="79a63-129">Le mot de passe doit comporter des lettres majuscules, des lettres minuscules et des nombres ou des symboles.</span><span class="sxs-lookup"><span data-stu-id="79a63-129">The password must include capital letters, lowercase letters, and numbers or symbols.</span></span>
      > 
      > 
   3. <span data-ttu-id="79a63-130">Choisissez une date à laquelle le compte expirera et après laquelle les connexions Bureau à distance seront bloquées.</span><span class="sxs-lookup"><span data-stu-id="79a63-130">Choose a date on which the account will expire and after which remote desktop connections will be blocked.</span></span>
   4. <span data-ttu-id="79a63-131">Une fois que vous avez fourni toutes les informations requises, sélectionnez le bouton **OK** .</span><span class="sxs-lookup"><span data-stu-id="79a63-131">After you've provided all the required information, choose the **OK** button.</span></span>
      
       <span data-ttu-id="79a63-132">Plusieurs paramètres qui activent les Services d'accès à distance sont ajoutés aux fichiers .cscfg et .csdef.</span><span class="sxs-lookup"><span data-stu-id="79a63-132">Several settings that enable Remote Access Services are added to the .cscfg and .csdef files.</span></span>
5. <span data-ttu-id="79a63-133">Dans l’Assistant **Paramètres de publication Microsoft Azure**, sélectionnez le bouton **OK** quand vous êtes prêt à publier votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="79a63-133">In the **Microsoft Azure Publish Settings** wizard, choose the **OK** button when you’re ready to publish your cloud service.</span></span>
   
    <span data-ttu-id="79a63-134">Si vous n’êtes pas prêt à le publier, sélectionnez le bouton **Annuler** .</span><span class="sxs-lookup"><span data-stu-id="79a63-134">If you're not ready to publish, choose the **Cancel** button.</span></span> <span data-ttu-id="79a63-135">Les paramètres de configuration sont enregistrés, et vous pourrez publier votre service cloud ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="79a63-135">The configuration settings are saved, and you can publish your cloud service later.</span></span>

## <a name="connect-to-an-azure-role-by-using-remote-desktop"></a><span data-ttu-id="79a63-136">Se connecter à un rôle Azure à l'aide du Bureau à distance</span><span class="sxs-lookup"><span data-stu-id="79a63-136">Connect to an Azure Role by using Remote Desktop</span></span>
<span data-ttu-id="79a63-137">Après avoir publié votre service cloud sur Azure, vous pouvez utiliser l'Explorateur de serveurs pour vous connecter aux machines virtuelles hébergées par Azure.</span><span class="sxs-lookup"><span data-stu-id="79a63-137">After you publish your cloud service on Azure, you can use Server Explorer to log into the virtual machines that Azure hosts.</span></span> 

1. <span data-ttu-id="79a63-138">Dans l’Explorateur de serveurs, développez le nœud **Azure** , puis développez le nœud d’un service cloud et d’un de ses rôles pour afficher une liste d’instances.</span><span class="sxs-lookup"><span data-stu-id="79a63-138">In Server Explorer, expand the **Azure** node, and then expand the node for a cloud service and one of its roles to display a list of instances.</span></span>
2. <span data-ttu-id="79a63-139">Ouvrez le menu contextuel d’un nœud d’instance, puis sélectionnez **Connexion à l’aide de Bureau à distance**.</span><span class="sxs-lookup"><span data-stu-id="79a63-139">Open the shortcut menu for an instance node, and then choose **Connect Using Remote Desktop**.</span></span>
   
    ![Connexion Bureau à distance](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. <span data-ttu-id="79a63-141">Entrez le nom d'utilisateur et le mot de passe que vous avez créés précédemment.</span><span class="sxs-lookup"><span data-stu-id="79a63-141">Enter the user name and password that you created previously.</span></span> <span data-ttu-id="79a63-142">Vous êtes maintenant connecté à votre session à distance.</span><span class="sxs-lookup"><span data-stu-id="79a63-142">You are now logged into your remote session.</span></span>

