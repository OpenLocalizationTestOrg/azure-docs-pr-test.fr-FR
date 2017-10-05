---
title: "Activation d’Azure Active Directory Identity Protection | Microsoft Docs"
description: "Découvrez comment activer Azure Active Directory Identity Protection."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestion d’applications, sécurité, risque, niveau de risque, vulnérabilité, stratégie de sécurité"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f7a7ffaf-76bf-4cc7-96a1-86c944275c82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: e0683e837086ca08f4b4b3f49695bdd2b4063ea4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="enabling-azure-active-directory-identity-protection"></a><span data-ttu-id="73ca4-104">Activer Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="73ca4-104">Enabling Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="73ca4-105">Active Directory Azure Identity Protection est une nouvelle fonctionnalité qui offre une vue consolidée des activités de connexion suspectes et des vulnérabilités potentielles, avec des notifications, des recommandations de correction et des stratégies basées sur les risques pour vous aider à protéger votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="73ca4-105">Azure Active Directory Identity Protection is a new capability that provides a consolidated view into suspicious sign-in activities and potential vulnerabilities and with notifications, remediation recommendations and risk-based policies helps you protect your business.</span></span> 

<span data-ttu-id="73ca4-106">Le service détecte les activités de connexion suspectes pour les utilisateurs finaux et les identités privilégiées (administrateurs) en fonction de signaux tels que les attaques par force brute, les fuites d’informations d’identification et les connexions provenant d’emplacements inconnus et d’appareils infectés, pour protéger contre ces activités en temps réel.</span><span class="sxs-lookup"><span data-stu-id="73ca4-106">The service detects suspicious activities for end user and privileged (admin) identities based on signals like brute force attacks, leaked credentials, sign ins from unfamiliar locations, infected devices, to protect against these activities in real-time.</span></span> <span data-ttu-id="73ca4-107">Plus important encore, sur la base de ces activités suspectes, un niveau de gravité du risque pour l’utilisateur est calculé, vous pouvez configurer des stratégies basées sur les risques et protéger automatiquement les identités de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="73ca4-107">More importantly, based on these suspicious activities, a user risk severity is computed and risk-based policies can be configured and automatically protect the identities of your organization.</span></span> <span data-ttu-id="73ca4-108">Pour plus de détails, consultez [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="73ca4-108">For more details, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

<span data-ttu-id="73ca4-109">Cette rubrique explique comment activer Azure Active Directory Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="73ca4-109">This topics shows how to enable Azure Active Directory Identity Protection.</span></span>

## <a name="steps-to-enable-azure-active-directory-identity-protection"></a><span data-ttu-id="73ca4-110">Étapes d’activation d’Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="73ca4-110">Steps to enable Azure Active Directory Identity Protection</span></span>
1. <span data-ttu-id="73ca4-111">[Connectez-vous](https://ms.portal.azure.com/) à votre portail Azure en tant qu’administrateur global.</span><span class="sxs-lookup"><span data-stu-id="73ca4-111">[Sign-on](https://ms.portal.azure.com/) to your Azure portal as global administrator.</span></span> 
2. <span data-ttu-id="73ca4-112">Dans le portail Azure, cliquez sur **Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="73ca4-112">In the Azure portal, click **Marketplace**.</span></span>
   
    <span data-ttu-id="73ca4-113">![Créer](./media/active-directory-identityprotection-enable/01.png "créer")</span><span class="sxs-lookup"><span data-stu-id="73ca4-113">![Create](./media/active-directory-identityprotection-enable/01.png "Create")</span></span>
3. <span data-ttu-id="73ca4-114">Dans la liste des applications, cliquez sur **Sécurité + Identité**.</span><span class="sxs-lookup"><span data-stu-id="73ca4-114">In the applications list, click **Security + Identity**.</span></span>
   
    <span data-ttu-id="73ca4-115">![Créer](./media/active-directory-identityprotection-enable/02.png "créer")</span><span class="sxs-lookup"><span data-stu-id="73ca4-115">![Create](./media/active-directory-identityprotection-enable/02.png "Create")</span></span>
4. <span data-ttu-id="73ca4-116">Cliquez sur **Azure AD Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="73ca4-116">Click **Azure AD Identity Protection**.</span></span>
   
    <span data-ttu-id="73ca4-117">![Créer](./media/active-directory-identityprotection-enable/03.png "créer")</span><span class="sxs-lookup"><span data-stu-id="73ca4-117">![Create](./media/active-directory-identityprotection-enable/03.png "Create")</span></span>
5. <span data-ttu-id="73ca4-118">Dans le panneau **d’Azure AD Identity Protection**, cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="73ca4-118">On the **Azure AD Identity Protection** blade, click **Create**.</span></span>
   
    <span data-ttu-id="73ca4-119">![Créer](./media/active-directory-identityprotection-enable/04.png "créer")</span><span class="sxs-lookup"><span data-stu-id="73ca4-119">![Create](./media/active-directory-identityprotection-enable/04.png "Create")</span></span>

## <a name="next-steps"></a><span data-ttu-id="73ca4-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="73ca4-120">Next Steps</span></span>
* [<span data-ttu-id="73ca4-121">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="73ca4-121">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

