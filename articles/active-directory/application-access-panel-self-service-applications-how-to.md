---
title: "Guide pratique pour utiliser l’accès aux applications en libre-service | Microsoft Docs"
description: "Activer l’accès aux applications en libre-service pour permettre aux utilisateurs de rechercher leurs propres applications"
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
ms.reviewer: japere
ms.openlocfilehash: 08a05a70d976104d4e0a37b0a0dd15042b0212d8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-self-service-application-access"></a><span data-ttu-id="dfc0b-103">Guide pratique pour utiliser l’accès aux applications en libre-service</span><span class="sxs-lookup"><span data-stu-id="dfc0b-103">How to use self-service application access</span></span>

<span data-ttu-id="dfc0b-104">Pour permettre à vos utilisateurs de découvrir eux-mêmes des applications depuis leur panneau d’accès, vous devez activer l’option **Accès aux applications en libre-service** pour toutes les applications pour lesquelles vous souhaitez autoriser les utilisateurs à les découvrir eux-mêmes et en demander l’accès.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-104">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

<span data-ttu-id="dfc0b-105">Cette fonctionnalité est un excellent moyen pour un groupe informatique d’économiser du temps et de l’argent, et elle est recommandée dans le cadre d’un déploiement d’applications modernes avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-105">This feature is a great way for you to save time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="dfc0b-106">À l’aide de cette fonctionnalité, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="dfc0b-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="dfc0b-107">Autoriser les utilisateurs à découvrir eux-mêmes des applications depuis le [panneau d’accès aux applications](https://myapps.microsoft.com/) sans déranger le groupe informatique.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-107">Let users self-discover applications from the [Application Access Panel](https://myapps.microsoft.com/) without bothering the IT group.</span></span>

-   <span data-ttu-id="dfc0b-108">Ajouter ces utilisateurs à un groupe préconfiguré pour vous permettre de voir qui a demandé l’accès, de retirer l’accès et de gérer les rôles qui leur ont été attribués.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-108">Add those users to a pre-configured group so you can see who has requested access, remove access, and manage the roles assigned to them.</span></span>

-   <span data-ttu-id="dfc0b-109">Éventuellement, autoriser un approbateur d’entreprise à approuver les demandes d’accès aux applications à la place du groupe informatique.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-109">Optionally allow a business approver to approve application access requests so the IT group doesn’t have to.</span></span>

-   <span data-ttu-id="dfc0b-110">Éventuellement, configurer jusqu'à 10 personnes qui peuvent autoriser l’accès à cette application.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-110">Optionally configure up to 10 individuals who may approve access to this application.</span></span>

-   <span data-ttu-id="dfc0b-111">Éventuellement, autoriser un approbateur d’entreprise à définir des mots de passe dont ces utilisateurs peuvent se servir pour se connecter à l’application, directement depuis le [panneau d’accès aux applications](https://myapps.microsoft.com/) de l’approbateur d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-111">Optionally allow a business approver to set the passwords those users can use to sign in to the application, right from the business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="dfc0b-112">Éventuellement, attribuer automatiquement directement un rôle d’application à des utilisateurs affectés en libre-service.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-112">Optionally automatically assign self-service assigned users to an application role directly.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="dfc0b-113">Activer l’accès aux applications en libre-service pour permettre aux utilisateurs de rechercher leurs propres applications.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-113">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="dfc0b-114">L’accès aux applications en libre-service est un excellent moyen pour permettre aux utilisateurs de découvrir eux-mêmes des applications, et éventuellement de permettre au groupe d’entreprise d’approuver l’accès à ces applications.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-114">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="dfc0b-115">Vous pouvez autoriser le groupe d’entreprise à gérer les informations d’identification affectées à ces utilisateurs dans le cadre d’une authentification unique par mot de passe, directement depuis leurs volets d’accès.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-115">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="dfc0b-116">Pour activer l’accès en libre-service à une application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="dfc0b-116">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="dfc0b-117">Ouvrez le [**portail Azure**](https://portal.azure.com/) et connectez-vous en tant qu’**administrateur général**.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-117">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="dfc0b-118">Ouvrez **l’extension Azure Active Directory** en cliquant sur **Autres services** en bas du menu de navigation principal de gauche.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-118">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="dfc0b-119">Tapez « **Azure Active Directory** » dans la zone de recherche de filtre et sélectionnez l’élément **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-119">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="dfc0b-120">Cliquez sur **Applications d’entreprise** dans le menu de navigation de gauche d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-120">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="dfc0b-121">Cliquez sur **Toutes les applications** pour afficher la liste complète de vos applications.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-121">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="dfc0b-122">Si l’application que vous recherchez n’apparaît pas, utilisez la commande **Filtre** en haut de la **liste de toutes les applications** et définissez l’option **Afficher** sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-122">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="dfc0b-123">Sélectionnez l’application pour laquelle vous souhaitez activer l’accès en libre-service à partir de la liste.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-123">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="dfc0b-124">Une fois l’application chargée, cliquez sur **Libre-service** dans le menu de navigation gauche de l’application.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-124">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="dfc0b-125">Pour activer l’accès en libre-service à cette application, définissez l’option **Autoriser les utilisateurs à demander l’accès à cette application ?** sur **Oui.**</span><span class="sxs-lookup"><span data-stu-id="dfc0b-125">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="dfc0b-126">Ensuite, pour sélectionner le groupe auquel les utilisateurs qui demandent l’accès à cette application doivent être ajoutés, cliquez sur le sélecteur en regard de l’étiquette **À quel groupe les utilisateurs attribués doivent-ils être ajoutés ?** et sélectionnez un groupe.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-126">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="dfc0b-127">**Facultatif :** si vous souhaitez exiger une approbation d’entreprise avant d’accorder l’accès aux utilisateurs, définissez l’option **Demander une approbation avant d’accorder l’accès à cette application ?** sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-127">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="dfc0b-128">**Facultatif : pour les applications qui nécessitent une authentification unique par mot de passe uniquement,** si vous souhaitez autoriser ces approbateurs d’entreprise à spécifier les mots de passe envoyés à cette application pour les utilisateurs approuvés, définissez l’option **Autoriser les approbateurs à définir les mots de passe de l’utilisateur pour cette application ?** sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-128">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="dfc0b-129">**Facultatif :** pour spécifier les approbateurs d’entreprise autorisés à approuver l’accès à cette application, cliquez sur le sélecteur en regard de l’étiquette **Qui est autorisé à approuver l’accès à cette application ?** pour sélectionner jusqu’à 10 approbateurs d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-129">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

   * <span data-ttu-id="dfc0b-130">Les groupes ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-130">Groups are not supported.</span></span>

13. <span data-ttu-id="dfc0b-131">**Facultatif :** **pour les applications qui exposent des rôles**, si vous souhaitez attribuer un rôle à des utilisateurs approuvés en libre-service, cliquez sur le sélecteur en regard de l’option  **À quel rôle attribuer des utilisateurs dans cette application ?** pour sélectionner le rôle à affecter à ces utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-131">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="dfc0b-132">Cliquez sur le bouton **Enregistrer** en haut du volet pour terminer.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-132">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="dfc0b-133">Lorsque vous avez terminé la configuration d’applications en libre-service, les utilisateurs peuvent accéder à leur [volet d’accès aux applications](https://myapps.microsoft.com/) et cliquer sur le bouton **+Ajouter** pour choisir les applications pour lesquelles vous avez activé l’accès en libre-service.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-133">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="dfc0b-134">Les approbateurs d’entreprise reçoivent également une notification dans leur [volet d’accès aux applications](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="dfc0b-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="dfc0b-135">Vous pouvez leur envoyer une notification par e-mail les avertissant qu’un utilisateur a demandé l’accès à une application nécessitant leur approbation.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-135">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="dfc0b-136">Ces approbations prennent en charge les flux de travail avec approbation unique uniquement, ce qui signifie que si vous spécifiez plusieurs approbateurs, chaque approbateur peut approuver l’accès à l’application.</span><span class="sxs-lookup"><span data-stu-id="dfc0b-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfc0b-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dfc0b-137">Next steps</span></span>
[<span data-ttu-id="dfc0b-138">Configuration d’Azure Active Directory pour la gestion de groupe en libre-service</span><span class="sxs-lookup"><span data-stu-id="dfc0b-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
