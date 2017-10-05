---
title: 'Services de domaine Azure Active Directory : Activer la prise en charge du service Profil utilisateur SharePoint | Microsoft Docs'
description: "Configurer les domaines gérés des services de domaine Azure Active Directory pour prendre en charge la synchronisation de profils pour SharePoint Server"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: c3c923b5c9cd652f0c5b0ec98c1cda740f180122
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-managed-domain-to-support-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="7f5f0-103">Configurer un domaine géré pour prendre en charge la synchronisation de profils pour SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="7f5f0-103">Configure a managed domain to support profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="7f5f0-104">SharePoint Server inclut un service Profil utilisateur qui est utilisé pour la synchronisation des profils utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7f5f0-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="7f5f0-105">Pour configurer le service Profil utilisateur, les autorisations appropriées doivent être accordées sur un domaine Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7f5f0-105">To set up the User Profile Service, appropriate permissions need to be granted on an Active Directory domain.</span></span> <span data-ttu-id="7f5f0-106">Pour plus d’informations, consultez [Accorder des autorisations Active Directory Domain Services pour la synchronisation de profils dans SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f5f0-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="7f5f0-107">Cet article explique comment vous pouvez configurer des domaines gérés des services de domaine Azure Active Directory pour déployer le service de synchronisation de profils utilisateurs SharePoint Server.</span><span class="sxs-lookup"><span data-stu-id="7f5f0-107">This article explains how you can configure Azure AD Domain Services managed domains to deploy the SharePoint Server User Profile Sync service.</span></span>

## <a name="the-aad-dc-service-accounts-group"></a><span data-ttu-id="7f5f0-108">Le groupe « Comptes de Service de contrôleur de domaine AAD »</span><span class="sxs-lookup"><span data-stu-id="7f5f0-108">The 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="7f5f0-109">Un groupe de sécurité appelé « **Comptes de service de contrôleur de domaine AAD** » est disponible dans l’unité d’organisation « Utilisateurs » sur votre domaine géré.</span><span class="sxs-lookup"><span data-stu-id="7f5f0-109">A security group called '**AAD DC Service Accounts**' is available within the 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="7f5f0-110">Vous pouvez voir ce groupe dans le composant logiciel enfichable MMC **Utilisateurs et ordinateurs Active Directory** sur votre domaine géré.</span><span class="sxs-lookup"><span data-stu-id="7f5f0-110">You can see this group in the **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![Groupe de sécurité Comptes de service de contrôleur de domaine AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="7f5f0-112">Les privilèges suivants sont délégués aux membres de ce groupe de sécurité :</span><span class="sxs-lookup"><span data-stu-id="7f5f0-112">Members of this security group are delegated the following privileges:</span></span>
- <span data-ttu-id="7f5f0-113">Le privilège « Répliquer les modifications de répertoire » à la racine DSE du domaine géré.</span><span class="sxs-lookup"><span data-stu-id="7f5f0-113">The 'Replicate Directory Changes' privilege on the root DSE of the managed domain.</span></span>
- <span data-ttu-id="7f5f0-114">Le privilège « Répliquer les changements de répertoire » sur le contexte de nommage de configuration (cn=conteneur de configuration) du domaine géré.</span><span class="sxs-lookup"><span data-stu-id="7f5f0-114">The 'Replicate Directory Changes' privilege on the Configuration naming context (cn=configuration container) of the managed domain.</span></span>

<span data-ttu-id="7f5f0-115">Ce groupe de sécurité est également membre du groupe prédéfini **Accès compatible pré-Windows 2000**.</span><span class="sxs-lookup"><span data-stu-id="7f5f0-115">This security group is also a member of the built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![Groupe de sécurité Comptes de service de contrôleur de domaine AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-to-support-sharepoint-server-user-profile-sync"></a><span data-ttu-id="7f5f0-117">Activer votre domaine géré pour prendre en charge la synchronisation de profils utilisateurs SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="7f5f0-117">Enable your managed domain to support SharePoint Server user profile sync</span></span>
<span data-ttu-id="7f5f0-118">Vous pouvez ajouter le compte de service utilisé pour la synchronisation de profils utilisateurs SharePoint au groupe **Comptes de service de contrôleur de domaine AAD**.</span><span class="sxs-lookup"><span data-stu-id="7f5f0-118">You can add the service account used for SharePoint user profile synchronization to the **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="7f5f0-119">Par conséquent, le compte de synchronisation obtient les privilèges appropriés pour répliquer les modifications apportées au répertoire.</span><span class="sxs-lookup"><span data-stu-id="7f5f0-119">As a result, the synchronization account gets adequate privileges to replicate changes to the directory.</span></span> <span data-ttu-id="7f5f0-120">Cette étape de configuration permet à la synchronisation de profils utilisateurs SharePoint Server de fonctionner correctement.</span><span class="sxs-lookup"><span data-stu-id="7f5f0-120">This configuration step enables SharePoint Server user profile sync to work correctly.</span></span>

![Comptes de service de contrôleur de domaine AAD – ajouter des membres](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![Comptes de service de contrôleur de domaine AAD – ajouter des membres](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="7f5f0-123">Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="7f5f0-123">Related Content</span></span>
* [<span data-ttu-id="7f5f0-124">Informations techniques de référence – Accorder des autorisations Active Directory Domain Services pour la synchronisation de profils dans SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="7f5f0-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
