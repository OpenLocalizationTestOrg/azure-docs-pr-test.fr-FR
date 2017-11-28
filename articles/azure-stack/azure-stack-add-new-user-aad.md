---
title: aaaAdd un nouveau compte de locataire Azure pile dans Azure Active Directory | Documents Microsoft
description: "Après avoir déployé le Kit de développement de pile Microsoft Azure, vous devez toocreate au moins un compte d’utilisateur de client, vous pouvez explorer le portail de locataires hello."
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
ms.openlocfilehash: f0cd380d4fc0b52f4e5f6f0c9ef80d3dd0d64443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-new-azure-stack-tenant-account-in-azure-active-directory"></a><span data-ttu-id="e9e2e-103">Ajouter un nouveau compte de locataire Azure Stack dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9e2e-103">Add a new Azure Stack tenant account in Azure Active Directory</span></span>
<span data-ttu-id="e9e2e-104">Après avoir [déploiement hello Kit de développement Azure pile](azure-stack-run-powershell-script.md), vous aurez besoin à un compte d’utilisateur locataire pour pouvoir Explorer le portail de locataires hello et vos offres et les plans de test.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-104">After [deploying hello Azure Stack Development Kit](azure-stack-run-powershell-script.md), you'll need a tenant user account so you can explore hello tenant portal and test your offers and plans.</span></span> <span data-ttu-id="e9e2e-105">Vous pouvez créer un compte de locataire par [à l’aide de hello portail Azure](#create-an-azure-stack-tenant-account-using-the-azure-portal) ou par [à l’aide de PowerShell](#create-an-azure-stack-tenant-account-using-powershell).</span><span class="sxs-lookup"><span data-stu-id="e9e2e-105">You can create a tenant account by [using hello Azure portal](#create-an-azure-stack-tenant-account-using-the-azure-portal) or by [using PowerShell](#create-an-azure-stack-tenant-account-using-powershell).</span></span>

## <a name="create-an-azure-stack-tenant-account-using-hello-azure-portal"></a><span data-ttu-id="e9e2e-106">Créer un compte de locataire Azure pile à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="e9e2e-106">Create an Azure Stack tenant account using hello Azure portal</span></span>
<span data-ttu-id="e9e2e-107">Vous devez avoir un hello de toouse abonnement Azure portail Azure.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-107">You must have an Azure subscription toouse hello Azure portal.</span></span>

1. <span data-ttu-id="e9e2e-108">Connectez-vous trop[Azure](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e9e2e-108">Log in too[Azure](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e9e2e-109">Dans la barre de navigation gauche Microsoft Azure, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-109">In Microsoft Azure left navigation bar, click **Active Directory**.</span></span>
3. <span data-ttu-id="e9e2e-110">Dans la liste de répertoires hello, cliquez sur répertoire hello que vous souhaitez toouse pour la pile de Azure, ou créez un nouveau.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-110">In hello directory list, click hello directory that you want toouse for Azure Stack, or create a new one.</span></span>
4. <span data-ttu-id="e9e2e-111">Sur la page de ce répertoire, cliquez sur **Utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-111">On this directory page, click **Users**.</span></span>
5. <span data-ttu-id="e9e2e-112">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-112">Click **Add user**.</span></span>
6. <span data-ttu-id="e9e2e-113">Bonjour **ajouter un utilisateur** Assistant Bonjour **Type d’utilisateur** , choisissez **nouvel utilisateur dans votre organisation**.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-113">In hello **Add user** wizard, in hello **Type of user** list, choose **New user in your organization**.</span></span>
7. <span data-ttu-id="e9e2e-114">Bonjour **nom d’utilisateur** , tapez un nom d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-114">In hello **User name** box, type a name for hello user.</span></span>
8. <span data-ttu-id="e9e2e-115">Bonjour  **@**  , choisissez l’entrée appropriée de hello.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-115">In hello **@** box, choose hello appropriate entry.</span></span>
9. <span data-ttu-id="e9e2e-116">Cliquez sur flèche suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-116">Click hello next arrow.</span></span>
10. <span data-ttu-id="e9e2e-117">Bonjour **profil utilisateur** page de l’Assistant de hello, tapez un **prénom**, **nom**, et **nom d’affichage**.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-117">In hello **User profile** page of hello wizard, type a **First name**, **Last name**, and **Display name**.</span></span>
11. <span data-ttu-id="e9e2e-118">Bonjour **rôle** , choisissez **utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-118">In hello **Role** list, choose **User**.</span></span>
12. <span data-ttu-id="e9e2e-119">Cliquez sur flèche suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-119">Click hello next arrow.</span></span>
13. <span data-ttu-id="e9e2e-120">Sur hello **mot de passe temporaire Get** , cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-120">On hello **Get temporary password** page, click **Create**.</span></span>
14. <span data-ttu-id="e9e2e-121">Hello de copie **nouveau mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-121">Copy hello **New password**.</span></span>
15. <span data-ttu-id="e9e2e-122">Ouvrez une session dans tooMicrosoft Azure avec un nouveau compte de hello.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-122">Log in tooMicrosoft Azure with hello new account.</span></span> <span data-ttu-id="e9e2e-123">Modifier le mot de passe hello lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-123">Change hello password when prompted.</span></span>
16. <span data-ttu-id="e9e2e-124">Connectez-vous trop`https://portal.local.azurestack.external` avec le portail de locataires hello nouveau compte toosee hello.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-124">Log in too`https://portal.local.azurestack.external` with hello new account toosee hello tenant portal.</span></span>

## <a name="create-an-azure-stack-tenant-account-using-powershell"></a><span data-ttu-id="e9e2e-125">Création d’un compte de locataire Azure Stack à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9e2e-125">Create an Azure Stack tenant account using PowerShell</span></span>
<span data-ttu-id="e9e2e-126">Si vous n’avez pas un abonnement Azure, vous ne pouvez pas utiliser hello tooadd portail Azure un compte d’utilisateur client.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-126">If you don't have an Azure subscription, you can't use hello Azure portal tooadd a tenant user account.</span></span> <span data-ttu-id="e9e2e-127">Dans ce cas, vous pouvez utiliser les hello Azure Module Active Directory pour Windows PowerShell à la place.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-127">In this case, you can use hello Azure Active Directory Module for Windows PowerShell instead.</span></span>

> [!NOTE]
> <span data-ttu-id="e9e2e-128">Si vous utilisez Microsoft Account (Live ID) toodeploy Kit de développement de pile Azure, vous ne pouvez pas utiliser le compte client AAD PowerShell toocreate.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-128">If you are using Microsoft Account (Live ID) toodeploy Azure Stack Development Kit, you can't use AAD PowerShell toocreate tenant account.</span></span> 
> 
> 

1. <span data-ttu-id="e9e2e-129">Installer hello [Assistant Microsoft Online Services Sign-In pour RTW de professionnels de l’informatique](https://www.microsoft.com/en-us/download/details.aspx?id=41950).</span><span class="sxs-lookup"><span data-stu-id="e9e2e-129">Install hello [Microsoft Online Services Sign-In Assistant for IT Professionals RTW](https://www.microsoft.com/en-us/download/details.aspx?id=41950).</span></span>
2. <span data-ttu-id="e9e2e-130">Installer hello [Azure Module Active Directory pour Windows PowerShell (version 64 bits)](http://go.microsoft.com/fwlink/p/?linkid=236297) et ouvrez-le.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-130">Install hello [Azure Active Directory Module for Windows PowerShell (64-bit version)](http://go.microsoft.com/fwlink/p/?linkid=236297) and open it.</span></span>
3. <span data-ttu-id="e9e2e-131">Exécutez hello suivant d’applets de commande :</span><span class="sxs-lookup"><span data-stu-id="e9e2e-131">Run hello following cmdlets:</span></span>

    ```powershell
    # Provide hello AAD credential you use toodeploy Azure Stack Development Kit

            $msolcred = get-credential

    # Add a tenant account "Tenant Admin <username>@<yourdomainname>" with hello initial password "<password>".

            connect-msolservice -credential $msolcred
            $user = new-msoluser -DisplayName "Tenant Admin" -UserPrincipalName <username>@<yourdomainname> -Password <password>
            Add-MsolRoleMember -RoleName "Company Administrator" -RoleMemberType User -RoleMemberObjectId $user.ObjectId

    ```

1. <span data-ttu-id="e9e2e-132">Connectez-vous tooMicrosoft Azure avec un nouveau compte de hello.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-132">Sign in tooMicrosoft Azure with hello new account.</span></span> <span data-ttu-id="e9e2e-133">Modifier le mot de passe hello lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-133">Change hello password when prompted.</span></span>
2. <span data-ttu-id="e9e2e-134">Connectez-vous trop`https://portal.local.azurestack.external` avec le portail de locataires hello nouveau compte toosee hello.</span><span class="sxs-lookup"><span data-stu-id="e9e2e-134">Sign in too`https://portal.local.azurestack.external` with hello new account toosee hello tenant portal.</span></span>

