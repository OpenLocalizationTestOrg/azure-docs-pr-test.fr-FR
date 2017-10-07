---
title: "Azure Active Directory B2C : Résoudre les problèmes liés à la création de locataires | Microsoft Docs"
description: "Problèmes et résolutions pour la création d’un locataire Azure Active Directory ou Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 7ba4c6b2-161b-45b5-b3bd-ccb662f5d7a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 4bb7ec6ec67d3368a0e36c098f290f582510714a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a><span data-ttu-id="05a63-103">Résoudre les problèmes de création d’un locataire Azure Active Directory ou Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="05a63-103">Troubleshoot creating an Azure Active Directory or Azure Active Directory B2C tenant</span></span> 

## <a name="create-an-azure-ad-tenant"></a><span data-ttu-id="05a63-104">Créer un locataire Azure AD</span><span class="sxs-lookup"><span data-stu-id="05a63-104">Create an Azure AD tenant</span></span>
<span data-ttu-id="05a63-105">Si vous ne peut pas créer un locataire Azure Active Directory (Azure AD) sur la première tentative de hello, essayez à nouveau.</span><span class="sxs-lookup"><span data-stu-id="05a63-105">If you can't create an Azure Active Directory (Azure AD) tenant on hello first attempt, try again.</span></span> <span data-ttu-id="05a63-106">Si hello problème persiste, contactez le Support de Azure.</span><span class="sxs-lookup"><span data-stu-id="05a63-106">If hello problem persists, contact Azure Support.</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="05a63-107">Créer un client Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="05a63-107">Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="05a63-108">Si vous rencontrez des problèmes lorsque vous [créer un B2C d’Active Directory de Azure (B2C Active Directory de Azure) client](active-directory-b2c-get-started.md), essayez hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="05a63-108">If you encounter issues when you [create an Azure Active Directory B2C (Azure AD B2C) tenant](active-directory-b2c-get-started.md), try hello following options:</span></span>

* <span data-ttu-id="05a63-109">Si le client de hello Azure AD B2C n’apparaît pas dans votre liste de clients, essayez à nouveau locataire de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="05a63-109">If hello Azure AD B2C tenant doesn't show up in your list of tenants, try again toocreate hello tenant.</span></span>
* <span data-ttu-id="05a63-110">Si locataire de hello Azure AD B2C s’affiche dans la liste des locataires hello message d’erreur suivant s’affiche, supprimer le client de hello et créez-en un nouveau :</span><span class="sxs-lookup"><span data-stu-id="05a63-110">If hello Azure AD B2C tenant does show up in your list of tenants and you see hello following  error message, delete hello tenant and create it again:</span></span>

    <span data-ttu-id="05a63-111">« Impossible de terminer la création de hello du client de B2C hello 'contosob2c'.</span><span class="sxs-lookup"><span data-stu-id="05a63-111">"Could not complete hello creation of hello B2C tenant 'contosob2c'.</span></span> <span data-ttu-id="05a63-112">Visitez ce [lien](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) pour plus d’informations. »</span><span class="sxs-lookup"><span data-stu-id="05a63-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance."</span></span>
* <span data-ttu-id="05a63-113">Il sont problèmes connus lorsque vous supprimez un B2C d’AD Azure existant du locataire et créer de nouveau à l’aide de hello même nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="05a63-113">There are known issues when you delete an existing Azure AD B2C tenant and re-create it by using hello same domain name.</span></span> <span data-ttu-id="05a63-114">Quand vous créez un locataire Azure AD B2C, vous devez utiliser un nom de domaine différent.</span><span class="sxs-lookup"><span data-stu-id="05a63-114">When you create a new Azure AD B2C tenant, you must use a different domain name.</span></span>
* <span data-ttu-id="05a63-115">Si aucune de ces solutions ne résout votre problème, contactez le support technique Azure.</span><span class="sxs-lookup"><span data-stu-id="05a63-115">If these resolutions don't work, contact Azure Support.</span></span> <span data-ttu-id="05a63-116">Pour plus d’informations, consultez [Prise en charge des demandes d’assistance pour Azure AD B2C](active-directory-b2c-support.md).</span><span class="sxs-lookup"><span data-stu-id="05a63-116">For more information, see [File support requests for Azure AD B2C](active-directory-b2c-support.md).</span></span>

