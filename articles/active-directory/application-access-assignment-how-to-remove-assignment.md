---
title: "Guide pratique pour retirer l’accès d’un utilisateur à une application | Microsoft Docs"
description: "Comprendre comment retirer l’accès d’un utilisateur à une application"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 497429e7bf62f7e1d67ea429d6b858725f843688
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-remove-a-users-access-to-an-application"></a><span data-ttu-id="f71b0-103">Guide pratique pour retirer l’accès d’un utilisateur à une application</span><span class="sxs-lookup"><span data-stu-id="f71b0-103">How to remove a user's access to an application</span></span>

<span data-ttu-id="f71b0-104">Cet article vous aide à comprendre comment retirer l’accès d’un utilisateur à une application.</span><span class="sxs-lookup"><span data-stu-id="f71b0-104">This article help you to understand how to remove a user's access to an application.</span></span>

## <a name="i-want-to-remove-a-specific-users-or-groups-assignment-to-an-application"></a><span data-ttu-id="f71b0-105">Je souhaite supprimer l’attribution d’une application à un utilisateur ou groupe spécifique</span><span class="sxs-lookup"><span data-stu-id="f71b0-105">I want to remove a specific user’s or group’s assignment to an application</span></span>

<span data-ttu-id="f71b0-106">Pour supprimer l’attribution d’une application à un utilisateur ou groupe, suivez les étapes répertoriées dans l’article [Supprimer l’attribution d’une application à un utilisateur ou groupe à partir d’une application d’entreprise dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="f71b0-106">To remove a user or group assignment to an application, follow the steps listed in the [Remove a user or group assignment from an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) article.</span></span>

<span data-ttu-id="f71b0-107">. ## je souhaite désactiver tous les accès à une application pour chaque utilisateur</span><span class="sxs-lookup"><span data-stu-id="f71b0-107">.## I want to disable all access to an application for every user</span></span>

<span data-ttu-id="f71b0-108">Pour désactiver toutes les connexions des utilisateurs à une application, suivez les étapes répertoriées dans l’article [Désactiver les connexions des utilisateurs à une application d’entreprise dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="f71b0-108">To disable all user sign-ins to an application, follow the steps listed in the [Disable user sign-ins for an enterprise app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) article.</span></span>

## <a name="i-want-to-delete-an-application-entirely"></a><span data-ttu-id="f71b0-109">Je veux complètement supprimer une passerelle d’application</span><span class="sxs-lookup"><span data-stu-id="f71b0-109">I want to delete an application entirely</span></span>

<span data-ttu-id="f71b0-110">Pour **supprimer une application**, suivez les instructions ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f71b0-110">To **delete an application**, follow the instructions below:</span></span>

1.  <span data-ttu-id="f71b0-111">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général** ou **coadministrateur.**</span><span class="sxs-lookup"><span data-stu-id="f71b0-111">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f71b0-112">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="f71b0-112">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f71b0-113">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f71b0-113">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f71b0-114">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f71b0-114">Click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="f71b0-115">Cliquez sur **Toutes les applications** pour afficher une liste de toutes vos applications.</span><span class="sxs-lookup"><span data-stu-id="f71b0-115">Click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="f71b0-116">Si l’application que vous recherchez n’apparaît pas, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications.**</span><span class="sxs-lookup"><span data-stu-id="f71b0-116">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="f71b0-117">Sélectionnez l’application que vous voulez supprimer.</span><span class="sxs-lookup"><span data-stu-id="f71b0-117">Select the application you want to delete.</span></span>

7.  <span data-ttu-id="f71b0-118">Une l’application chargée, cliquez sur l’icône **Supprimer** dans le panneau supérieur **Vue d’ensemble** de l’application.</span><span class="sxs-lookup"><span data-stu-id="f71b0-118">Once the application loads, click **Delete** icon from the top application’s **Overview** blade.</span></span>

## <a name="i-want-to-disable-all-future-user-consent-operations-to-any-application"></a><span data-ttu-id="f71b0-119">Je veux désactiver toutes les futures opérations de consentement de l’utilisateur pour n’importe quelle application</span><span class="sxs-lookup"><span data-stu-id="f71b0-119">I want to disable all future user consent operations to any application</span></span>

<span data-ttu-id="f71b0-120">La désactivation du consentement de l’utilisateur pour votre annuaire entier empêche les utilisateurs finaux de donner leur consentement pour n’importe quelle application.</span><span class="sxs-lookup"><span data-stu-id="f71b0-120">Disabling user consent for your entire directory prevent end users from consenting to any application.</span></span> <span data-ttu-id="f71b0-121">Les administrateurs peuvent toujours donner leur consentement au nom de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f71b0-121">Administrators can still consent on user’s behalves.</span></span> <span data-ttu-id="f71b0-122">Pour en savoir plus sur le consentement de l’application et les conditions pour donner ou refuser ce consentement, lisez la rubrique [Comprendre le consentement de l’utilisateur et de l’administrateur](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span><span class="sxs-lookup"><span data-stu-id="f71b0-122">To learn more about application consent, and why you may or may not wish to do this, read [Understanding user and admin consent](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).</span></span>

<span data-ttu-id="f71b0-123">Pour **désactiver toutes les futures opérations de consentement de l’utilisateur dans votre annuaire entier**, suivez les instructions ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="f71b0-123">To **disable all future user consent operations in your entire directory**, follow the instructions below:</span></span>

1.  <span data-ttu-id="f71b0-124">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général.**</span><span class="sxs-lookup"><span data-stu-id="f71b0-124">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="f71b0-125">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="f71b0-125">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="f71b0-126">Tapez « **Azure Active Directory** » dans la zone de recherche du filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f71b0-126">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f71b0-127">Cliquez sur **Utilisateurs et groupes** dans le menu de navigation.</span><span class="sxs-lookup"><span data-stu-id="f71b0-127">Click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="f71b0-128">Cliquez sur **Paramètres utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="f71b0-128">Click **User settings**.</span></span>

6.  <span data-ttu-id="f71b0-129">Désactivez toutes les futures opérations de consentement de l’utilisateur en définissant l’option **Les utilisateurs peuvent autoriser les applications à accéder à leurs données** sur **Non**, puis cliquez sur le bouton **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f71b0-129">Disable all future user consent operations by setting the **Users can allow apps to access their data** toggle to **No** and click the **Save** button.</span></span>


# <a name="next-steps"></a><span data-ttu-id="f71b0-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f71b0-130">Next steps</span></span>
[<span data-ttu-id="f71b0-131">Gestion de l’accès aux applications</span><span class="sxs-lookup"><span data-stu-id="f71b0-131">Managing access to apps</span></span>](active-directory-managing-access-to-apps.md)
