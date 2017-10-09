---
title: "rapports d’aaaAccess et d’utilisation pour l’authentification Multifacteur Azure | Documents Microsoft"
description: "Cette section décrit comment toouse hello fonctionnalité Azure multi-Factor Authentication - rapports."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: curtand
ms.assetid: 3f6b33c4-04c8-47d4-aecb-aa39a61c4189
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: kgremban
ms.openlocfilehash: ae7ccceca4968d7ec7cf0cb1cf9e041d9997c840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reports-in-azure-multi-factor-authentication"></a><span data-ttu-id="b906b-103">Rapports dans Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="b906b-103">Reports in Azure Multi-Factor Authentication</span></span>
<span data-ttu-id="b906b-104">Azure Multi-Factor Authentication fournit plusieurs rapports qui peuvent être utilisés par vous et votre organisation.</span><span class="sxs-lookup"><span data-stu-id="b906b-104">Azure Multi-Factor Authentication provides several reports that can be used by you and your organization.</span></span> <span data-ttu-id="b906b-105">Ces rapports sont accessibles via le portail de gestion de l’authentification multifacteur de hello.</span><span class="sxs-lookup"><span data-stu-id="b906b-105">These reports can be accessed through hello Multi-Factor Authentication Management Portal.</span></span> <span data-ttu-id="b906b-106">Hello Voici une liste des rapports disponibles de hello :</span><span class="sxs-lookup"><span data-stu-id="b906b-106">hello following is a list of hello available reports:</span></span>

| <span data-ttu-id="b906b-107">Rapport</span><span class="sxs-lookup"><span data-stu-id="b906b-107">Report</span></span> | <span data-ttu-id="b906b-108">Description</span><span class="sxs-lookup"><span data-stu-id="b906b-108">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="b906b-109">Usage</span><span class="sxs-lookup"><span data-stu-id="b906b-109">Usage</span></span> |<span data-ttu-id="b906b-110">l’utilisation de Hello rapports affichent des informations sur l’utilisation globale et résumé utilisateur des détails de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b906b-110">hello usage reports display information on overall usage, user summary, and user details.</span></span> |
| <span data-ttu-id="b906b-111">État du serveur</span><span class="sxs-lookup"><span data-stu-id="b906b-111">Server Status</span></span> |<span data-ttu-id="b906b-112">Ce rapport affiche l’état de hello des serveurs de l’authentification multifacteur associé à votre compte.</span><span class="sxs-lookup"><span data-stu-id="b906b-112">This report displays hello status of Multi-Factor Authentication Servers associated with your account.</span></span> |
| <span data-ttu-id="b906b-113">Historique de l'utilisateur bloqué</span><span class="sxs-lookup"><span data-stu-id="b906b-113">Blocked User History</span></span> |<span data-ttu-id="b906b-114">Ces rapports présentent historique hello de demandes tooblock ou débloquer des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b906b-114">These reports show hello history of requests tooblock or unblock users.</span></span> |
| <span data-ttu-id="b906b-115">Historique de l'utilisateur contourné</span><span class="sxs-lookup"><span data-stu-id="b906b-115">Bypassed User History</span></span> |<span data-ttu-id="b906b-116">Affiche l’historique de hello de demandes toobypass multi-Factor Authentication pour le numéro de téléphone d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b906b-116">Shows hello history of requests toobypass Multi-Factor Authentication for a user's phone number.</span></span> |
| <span data-ttu-id="b906b-117">Alerte de fraude</span><span class="sxs-lookup"><span data-stu-id="b906b-117">Fraud Alert</span></span> |<span data-ttu-id="b906b-118">Affiche l’historique des alertes de fraude soumises au cours de la plage de dates hello spécifiée.</span><span class="sxs-lookup"><span data-stu-id="b906b-118">Shows a history of fraud alerts submitted during hello date range you specified.</span></span> |
| <span data-ttu-id="b906b-119">Mis en file d'attente.</span><span class="sxs-lookup"><span data-stu-id="b906b-119">Queued</span></span> |<span data-ttu-id="b906b-120">Répertorie les rapports en file d'attente de traitement et leur état.</span><span class="sxs-lookup"><span data-stu-id="b906b-120">Lists reports queued for processing and their status.</span></span> <span data-ttu-id="b906b-121">Un lien du rapport hello toodownload ou de la vue est fourni lorsque hello du rapport est terminée.</span><span class="sxs-lookup"><span data-stu-id="b906b-121">A link toodownload or view hello report is provided when hello report is complete.</span></span> |

## <a name="view-reports"></a><span data-ttu-id="b906b-122">Afficher des rapports</span><span class="sxs-lookup"><span data-stu-id="b906b-122">View reports</span></span>
1. <span data-ttu-id="b906b-123">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b906b-123">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="b906b-124">Sur la gauche de hello, sélectionnez Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b906b-124">On hello left, select Active Directory.</span></span>
3. <span data-ttu-id="b906b-125">Suivez l’une de ces deux options, selon que vous utilisez ou non des fournisseurs d’authentification :</span><span class="sxs-lookup"><span data-stu-id="b906b-125">Follow one of these two options, depending on whether you use Auth Providers:</span></span>
   * <span data-ttu-id="b906b-126">**Option 1**: cliquez sur onglet de fournisseurs d’authentification multifacteur hello. Sélectionnez votre fournisseur d’authentification Multifacteur et cliquez sur hello **gérer** bouton bas hello.</span><span class="sxs-lookup"><span data-stu-id="b906b-126">**Option 1**: Click hello Multi-Factor Auth Providers tab. Select your MFA provider and click hello **Manage** button at hello bottom.</span></span>
   * <span data-ttu-id="b906b-127">**Option 2**: sélectionnez votre toohello de répertoire et accédez **configurer** onglet. Sous la section de l’authentification multifacteur hello, sélectionnez **gérer les paramètres de service**.</span><span class="sxs-lookup"><span data-stu-id="b906b-127">**Option 2**: Select your directory and go toohello **Configure** tab. Under hello multi-factor authentication section, select **Manage service settings**.</span></span> <span data-ttu-id="b906b-128">En hello en bas de page de paramètres de Service d’authentification Multifacteur hello, cliquez sur lien vers le portail Go toohello de hello.</span><span class="sxs-lookup"><span data-stu-id="b906b-128">At hello bottom of hello MFA Service Settings page, click hello Go toohello portal link.</span></span>
4. <span data-ttu-id="b906b-129">Bonjour portail de gestion Azure multi-Factor Authentication, sélectionnez type hello de rapport souhaité dans hello **afficher un rapport** section Bonjour barre de navigation gauche.</span><span class="sxs-lookup"><span data-stu-id="b906b-129">In hello Azure Multi-Factor Authentication Management Portal, select hello type of report you want from hello **View a Report** section in hello left navigation.</span></span>

<span data-ttu-id="b906b-130"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span><span class="sxs-lookup"><span data-stu-id="b906b-130"><center>![Cloud](./media/multi-factor-authentication-manage-reports/report.png)</center></span></span>


<span data-ttu-id="b906b-131">**Ressources supplémentaires**</span><span class="sxs-lookup"><span data-stu-id="b906b-131">**Additional Resources**</span></span>

* [<span data-ttu-id="b906b-132">Pour les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="b906b-132">For Users</span></span>](end-user/multi-factor-authentication-end-user.md)
* [<span data-ttu-id="b906b-133">Azure Multi-Factor Authentication sur MSDN</span><span class="sxs-lookup"><span data-stu-id="b906b-133">Azure Multi-Factor Authentication on MSDN</span></span>](https://msdn.microsoft.com/library/azure/dn249471.aspx)
