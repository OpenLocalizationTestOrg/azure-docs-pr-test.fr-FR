---
title: Ajouter un nouveau compte client Azure Stack dans Azure Active Directory | Microsoft Docs
description: "Après le déploiement du Kit de développement Microsoft Azure Stack, vous devrez créer au moins un compte utilisateur client pour pouvoir explorer le portail client."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a75d5c88-5b9e-4e9a-a6e3-48bbfa7069a7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 4401de010dec808f080f5460298bb738ddd39312
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="add-a-new-azure-stack-tenant-account-in-azure-active-directory"></a><span data-ttu-id="4b4b1-103">Ajouter un nouveau compte de locataire Azure Stack dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b4b1-103">Add a new Azure Stack tenant account in Azure Active Directory</span></span>
<span data-ttu-id="4b4b1-104">Après le [déploiement du Kit de développement Azure Stack](azure-stack-run-powershell-script.md), vous aurez besoin d’un compte utilisateur client afin de pouvoir explorer le portail client et tester vos offres et vos plans.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-104">After [deploying the Azure Stack Development Kit](azure-stack-run-powershell-script.md), you'll need a tenant user account so you can explore the tenant portal and test your offers and plans.</span></span> <span data-ttu-id="4b4b1-105">Vous pouvez créer un compte client [à l’aide du portail Azure](#create-an-azure-stack-tenant-account-using-the-azure-portal) ou [à l’aide de PowerShell](#create-an-azure-stack-tenant-account-using-powershell).</span><span class="sxs-lookup"><span data-stu-id="4b4b1-105">You can create a tenant account by [using the Azure portal](#create-an-azure-stack-tenant-account-using-the-azure-portal) or by [using PowerShell](#create-an-azure-stack-tenant-account-using-powershell).</span></span>

## <a name="create-an-azure-stack-tenant-account-using-the-azure-portal"></a><span data-ttu-id="4b4b1-106">Création d’un compte de locataire Azure Stack à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="4b4b1-106">Create an Azure Stack tenant account using the Azure portal</span></span>
<span data-ttu-id="4b4b1-107">Pour utiliser le portail Azure, vous devez disposer d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-107">You must have an Azure subscription to use the Azure portal.</span></span>

1. <span data-ttu-id="4b4b1-108">Connectez-vous à [Azure](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="4b4b1-108">Log in to [Azure](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="4b4b1-109">Dans la barre de navigation gauche Microsoft Azure, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-109">In Microsoft Azure left navigation bar, click **Active Directory**.</span></span>
3. <span data-ttu-id="4b4b1-110">Dans la liste des répertoires, cliquez sur le répertoire que vous souhaitez utiliser pour Azure Stack, ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-110">In the directory list, click the directory that you want to use for Azure Stack, or create a new one.</span></span>
4. <span data-ttu-id="4b4b1-111">Sur la page de ce répertoire, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-111">On this directory page, click **Users**.</span></span>
5. <span data-ttu-id="4b4b1-112">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-112">Click **Add user**.</span></span>
6. <span data-ttu-id="4b4b1-113">Dans l’assistant **Ajouter un utilisateur**, dans la liste **Type d’utilisateur**, choisissez **Nouvel utilisateur dans votre organisation**.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-113">In the **Add user** wizard, in the **Type of user** list, choose **New user in your organization**.</span></span>
7. <span data-ttu-id="4b4b1-114">Dans la zone **Nom d’utilisateur** , saisissez le nom de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-114">In the **User name** box, type a name for the user.</span></span>
8. <span data-ttu-id="4b4b1-115">Dans l’assistant **@** , sélectionnez l’entrée appropriée.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-115">In the **@** box, choose the appropriate entry.</span></span>
9. <span data-ttu-id="4b4b1-116">Cliquez sur la flèche Suivant.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-116">Click the next arrow.</span></span>
10. <span data-ttu-id="4b4b1-117">Dans la page **Profil utilisateur** de l’assistant, tapez un **Prénom**, un **Nom** et un **Nom d’affichage**.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-117">In the **User profile** page of the wizard, type a **First name**, **Last name**, and **Display name**.</span></span>
11. <span data-ttu-id="4b4b1-118">Dans la liste **Rôle**, choisissez **Utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-118">In the **Role** list, choose **User**.</span></span>
12. <span data-ttu-id="4b4b1-119">Cliquez sur la flèche Suivant.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-119">Click the next arrow.</span></span>
13. <span data-ttu-id="4b4b1-120">Dans la page **Obtenir un mot de passe temporaire**, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-120">On the **Get temporary password** page, click **Create**.</span></span>
14. <span data-ttu-id="4b4b1-121">Copiez le **Nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-121">Copy the **New password**.</span></span>
15. <span data-ttu-id="4b4b1-122">Connectez-vous à Microsoft Azure avec le nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-122">Log in to Microsoft Azure with the new account.</span></span> <span data-ttu-id="4b4b1-123">Modifiez le mot de passe lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-123">Change the password when prompted.</span></span>
16. <span data-ttu-id="4b4b1-124">Connectez-vous à `https://portal.local.azurestack.external` avec le nouveau compte pour afficher le portail client.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-124">Log in to `https://portal.local.azurestack.external` with the new account to see the tenant portal.</span></span>

## <a name="create-an-azure-stack-tenant-account-using-powershell"></a><span data-ttu-id="4b4b1-125">Création d’un compte de locataire Azure Stack à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b4b1-125">Create an Azure Stack tenant account using PowerShell</span></span>
<span data-ttu-id="4b4b1-126">Si vous n’avez pas d’abonnement Azure, vous ne pouvez pas utiliser le portail Azure pour ajouter un compte utilisateur client.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-126">If you don't have an Azure subscription, you can't use the Azure portal to add a tenant user account.</span></span> <span data-ttu-id="4b4b1-127">Dans ce cas, vous pouvez utiliser le module Azure Active Directory pour Windows PowerShell à la place.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-127">In this case, you can use the Azure Active Directory Module for Windows PowerShell instead.</span></span>

> [!NOTE]
> <span data-ttu-id="4b4b1-128">Si vous utilisez un compte Microsoft (Live ID) pour déployer le Kit de développement Azure Stack, vous ne pouvez pas utiliser AAD PowerShell pour créer le compte client.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-128">If you are using Microsoft Account (Live ID) to deploy Azure Stack Development Kit, you can't use AAD PowerShell to create tenant account.</span></span> 
> 
> 

1. <span data-ttu-id="4b4b1-129">Installez [l’Assistant de connexion Microsoft Online Services pour les professionnels de l’informatique RTW](https://www.microsoft.com/en-us/download/details.aspx?id=41950).</span><span class="sxs-lookup"><span data-stu-id="4b4b1-129">Install the [Microsoft Online Services Sign-In Assistant for IT Professionals RTW](https://www.microsoft.com/en-us/download/details.aspx?id=41950).</span></span>
2. <span data-ttu-id="4b4b1-130">Installez le [module Azure Active Directory pour Windows PowerShell (version 64 bits)](http://go.microsoft.com/fwlink/p/?linkid=236297) et ouvrez-le.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-130">Install the [Azure Active Directory Module for Windows PowerShell (64-bit version)](http://go.microsoft.com/fwlink/p/?linkid=236297) and open it.</span></span>
3. <span data-ttu-id="4b4b1-131">Exécutez les applets de commande suivantes :</span><span class="sxs-lookup"><span data-stu-id="4b4b1-131">Run the following cmdlets:</span></span>

    ```powershell
    # Provide the AAD credential you use to deploy Azure Stack Development Kit

            $msolcred = get-credential

    # Add a tenant account "Tenant Admin <username>@<yourdomainname>" with the initial password "<password>".

            connect-msolservice -credential $msolcred
            $user = new-msoluser -DisplayName "Tenant Admin" -UserPrincipalName <username>@<yourdomainname> -Password <password>
            Add-MsolRoleMember -RoleName "Company Administrator" -RoleMemberType User -RoleMemberObjectId $user.ObjectId

    ```

1. <span data-ttu-id="4b4b1-132">Connectez-vous à Microsoft Azure avec le nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-132">Sign in to Microsoft Azure with the new account.</span></span> <span data-ttu-id="4b4b1-133">Modifiez le mot de passe lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-133">Change the password when prompted.</span></span>
2. <span data-ttu-id="4b4b1-134">Connectez-vous à `https://portal.local.azurestack.external` avec le nouveau compte pour afficher le portail client.</span><span class="sxs-lookup"><span data-stu-id="4b4b1-134">Sign in to `https://portal.local.azurestack.external` with the new account to see the tenant portal.</span></span>

