---
title: 'Services de domaine Azure Active Directory : Activer la prise en charge du service Profil utilisateur SharePoint | Microsoft Docs'
description: "Configurer la synchronisation de profil de toosupport de domaines gérés Azure Active Directory Domain Services pour SharePoint Server"
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
ms.openlocfilehash: 9de4f810380309e8f6436fc24412701645978f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="7864d-103">Configurer une synchronisation de profil de domaine géré toosupport pour SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="7864d-103">Configure a managed domain toosupport profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="7864d-104">SharePoint Server inclut un service Profil utilisateur qui est utilisé pour la synchronisation des profils utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7864d-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="7864d-105">tooset des hello Service de profil utilisateur, les autorisations appropriées doivent toobe d’accorder sur un domaine Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7864d-105">tooset up hello User Profile Service, appropriate permissions need toobe granted on an Active Directory domain.</span></span> <span data-ttu-id="7864d-106">Pour plus d’informations, consultez [Accorder des autorisations Active Directory Domain Services pour la synchronisation de profils dans SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span><span class="sxs-lookup"><span data-stu-id="7864d-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="7864d-107">Cet article explique comment vous pouvez configurer le service de synchronisation de profil utilisateur SharePoint Server des Services de domaine Active Directory de Azure domaines gérés toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="7864d-107">This article explains how you can configure Azure AD Domain Services managed domains toodeploy hello SharePoint Server User Profile Sync service.</span></span>

## <a name="hello-aad-dc-service-accounts-group"></a><span data-ttu-id="7864d-108">groupe de « Comptes de Service de contrôleur de domaine AAD » Hello</span><span class="sxs-lookup"><span data-stu-id="7864d-108">hello 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="7864d-109">Un groupe de sécurité appelé «**des comptes de Service de contrôleur de domaine AAD**' n’est disponible dans l’unité d’organisation hello « Utilisateurs » sur votre domaine géré.</span><span class="sxs-lookup"><span data-stu-id="7864d-109">A security group called '**AAD DC Service Accounts**' is available within hello 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="7864d-110">Vous pouvez consulter ce groupe Bonjour **Active Directory Users and Computers** le composant logiciel enfichable MMC sur votre domaine géré.</span><span class="sxs-lookup"><span data-stu-id="7864d-110">You can see this group in hello **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![Groupe de sécurité Comptes de service de contrôleur de domaine AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="7864d-112">Les membres de ce groupe de sécurité sont hello délégué suivant des privilèges :</span><span class="sxs-lookup"><span data-stu-id="7864d-112">Members of this security group are delegated hello following privileges:</span></span>
- <span data-ttu-id="7864d-113">privilège de 'répliquer des modifications répertoire Hello sur la racine de hello DSE Hello géré de domaine.</span><span class="sxs-lookup"><span data-stu-id="7864d-113">hello 'Replicate Directory Changes' privilege on hello root DSE of hello managed domain.</span></span>
- <span data-ttu-id="7864d-114">Hello privilège « Répliquer les modifications de répertoire » sur le contexte d’appellation de Configuration hello (cn = configuration container) hello gérés domaine.</span><span class="sxs-lookup"><span data-stu-id="7864d-114">hello 'Replicate Directory Changes' privilege on hello Configuration naming context (cn=configuration container) of hello managed domain.</span></span>

<span data-ttu-id="7864d-115">Ce groupe de sécurité est également membre du groupe intégré de hello **accès Compatible pré-Windows 2000**.</span><span class="sxs-lookup"><span data-stu-id="7864d-115">This security group is also a member of hello built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![Groupe de sécurité Comptes de service de contrôleur de domaine AAD](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a><span data-ttu-id="7864d-117">Activer votre toosupport domaine géré synchronisation du profil utilisateur SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="7864d-117">Enable your managed domain toosupport SharePoint Server user profile sync</span></span>
<span data-ttu-id="7864d-118">Vous pouvez ajouter le compte de service hello utilisée pour SharePoint utilisateur profil synchronisation toohello **des comptes de Service de contrôleur de domaine AAD** groupe.</span><span class="sxs-lookup"><span data-stu-id="7864d-118">You can add hello service account used for SharePoint user profile synchronization toohello **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="7864d-119">Par conséquent, compte de synchronisation hello obtient Active toohello de privilèges adéquats tooreplicate modifications.</span><span class="sxs-lookup"><span data-stu-id="7864d-119">As a result, hello synchronization account gets adequate privileges tooreplicate changes toohello directory.</span></span> <span data-ttu-id="7864d-120">Cette étape de configuration permet de SharePoint Server utilisateur profil synchronisation toowork correctement.</span><span class="sxs-lookup"><span data-stu-id="7864d-120">This configuration step enables SharePoint Server user profile sync toowork correctly.</span></span>

![Comptes de service de contrôleur de domaine AAD – ajouter des membres](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![Comptes de service de contrôleur de domaine AAD – ajouter des membres](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="7864d-123">Contenu connexe</span><span class="sxs-lookup"><span data-stu-id="7864d-123">Related Content</span></span>
* [<span data-ttu-id="7864d-124">Informations techniques de référence – Accorder des autorisations Active Directory Domain Services pour la synchronisation de profils dans SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="7864d-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
