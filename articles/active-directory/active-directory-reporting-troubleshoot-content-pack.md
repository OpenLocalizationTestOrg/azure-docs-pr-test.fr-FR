---
title: "Résolution des problèmes liés aux erreurs du pack de contenu des journaux d’activité Azure Active Directory | Microsoft Docs"
description: "Fournit la liste des messages d’erreur du pack de contenu d’activité Azure Active Directory et les étapes à suivre pour les corriger."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c880e9eb6d48bd1e38075fbd867d3906ec67b547
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="8a0e1-103">Résolution des problèmes liés aux erreurs du pack de contenu des journaux d’activité Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8a0e1-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="8a0e1-104">Pendant que vous utilisez le pack de contenu Power BI pour Azure Active Directory Preview, vous pouvez rencontrer les erreurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="8a0e1-104">When working with the Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into the following errors:</span></span> 

- [<span data-ttu-id="8a0e1-105">Échec de l’actualisation</span><span class="sxs-lookup"><span data-stu-id="8a0e1-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="8a0e1-106">Échec de la mise à jour des informations d’identification de la source de données</span><span class="sxs-lookup"><span data-stu-id="8a0e1-106">Failed to update data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [<span data-ttu-id="8a0e1-107">L’importation de données prend trop de temps</span><span class="sxs-lookup"><span data-stu-id="8a0e1-107">Importing of data is taking too long</span></span>](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
<span data-ttu-id="8a0e1-108">Cette rubrique traite des causes possibles de ces erreurs et explique comment les corriger.</span><span class="sxs-lookup"><span data-stu-id="8a0e1-108">This topic provides you with information about the possible causes and how to fix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="8a0e1-109">Échec de l’actualisation</span><span class="sxs-lookup"><span data-stu-id="8a0e1-109">Refresh failed</span></span> 
 
<span data-ttu-id="8a0e1-110">**Circonstances de l’apparition de l’erreur** : message électronique en provenance de Power BI ou état d’échec dans l’historique d’actualisation.</span><span class="sxs-lookup"><span data-stu-id="8a0e1-110">**How this error is surfaced**: Email from Power BI or failed status in the refresh history.</span></span> 


| <span data-ttu-id="8a0e1-111">Cause :</span><span class="sxs-lookup"><span data-stu-id="8a0e1-111">Cause</span></span> | <span data-ttu-id="8a0e1-112">Procédure de résolution</span><span class="sxs-lookup"><span data-stu-id="8a0e1-112">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="8a0e1-113">Les erreurs d’échec d’actualisation peuvent être générées quand les informations d’identification des utilisateurs se connectant au pack de contenu ont été réinitialisées, mais pas mises à jour dans les paramètres de connexion du pack de contenu.</span><span class="sxs-lookup"><span data-stu-id="8a0e1-113">Refresh failure errors can be caused when the credentials of the users connecting to the content pack have been reset but not updated in the connection settings of the of the content pack.</span></span> | <span data-ttu-id="8a0e1-114">Dans Power BI, recherchez le jeu de données correspondant au tableau de bord Journaux d’activité Azure Active Directory (journaux d’activité Azure Active Directory), choisissez Planifier l’actualisation, puis entrez vos informations d’identification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8a0e1-114">In Power BI, locate the dataset corresponding to the Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="8a0e1-115">Une actualisation peut échouer à cause de problèmes de données dans le pack de contenu sous-jacent.</span><span class="sxs-lookup"><span data-stu-id="8a0e1-115">A refresh can fail due to data issues in the underlying content pack.</span></span> | <span data-ttu-id="8a0e1-116">Soumettez un ticket de support.</span><span class="sxs-lookup"><span data-stu-id="8a0e1-116">File a support ticket.</span></span> <span data-ttu-id="8a0e1-117">Pour plus d’informations, consultez [Comment obtenir une assistance pour Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="8a0e1-117">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-to-update-data-source-credentials"></a><span data-ttu-id="8a0e1-118">Échec de la mise à jour des informations d’identification de la source de données</span><span class="sxs-lookup"><span data-stu-id="8a0e1-118">Failed to update data source credentials</span></span> 
 
<span data-ttu-id="8a0e1-119">**Circonstances de l’apparition de cette erreur** : dans Power BI, pendant que vous vous connectez au pack de contenu des journaux d’activité Azure Active Directory (version préliminaire).</span><span class="sxs-lookup"><span data-stu-id="8a0e1-119">**How this error is surfaced**: In Power BI, when you are connecting to the Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="8a0e1-120">Cause :</span><span class="sxs-lookup"><span data-stu-id="8a0e1-120">Cause</span></span> | <span data-ttu-id="8a0e1-121">Procédure de résolution</span><span class="sxs-lookup"><span data-stu-id="8a0e1-121">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="8a0e1-122">L’utilisateur qui se connecte n’est ni administrateur général, ni lecteur sécurité, ni administrateur de sécurité.</span><span class="sxs-lookup"><span data-stu-id="8a0e1-122">The connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="8a0e1-123">Utilisez un compte ayant le rôle d’administrateur général, de lecteur sécurité ou d’administrateur de la sécurité pour accéder aux packs de contenu.</span><span class="sxs-lookup"><span data-stu-id="8a0e1-123">Use an account that is either a global admin or a security reader or a security admin to access the content packs.</span></span> |
| <span data-ttu-id="8a0e1-124">Votre locataire n’est pas de type Premium ou ne compte aucun utilisateur avec un fichier de licence Premium.</span><span class="sxs-lookup"><span data-stu-id="8a0e1-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="8a0e1-125">Soumettez un ticket de support.</span><span class="sxs-lookup"><span data-stu-id="8a0e1-125">File a support ticket.</span></span> <span data-ttu-id="8a0e1-126">Pour plus d’informations, consultez [Comment obtenir une assistance pour Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="8a0e1-126">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="8a0e1-127">L’importation de données prend trop de temps</span><span class="sxs-lookup"><span data-stu-id="8a0e1-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="8a0e1-128">**Circonstances de l’apparition de cette erreur** : dans Power BI, une fois que vous avez connecté votre pack de contenu, le processus d’importation de données démarre pour préparer votre tableau de bord pour le journal d’activité Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8a0e1-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, the data import process starts to prepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="8a0e1-129">Vous obtenez le message suivant : « *L’importation de données...* »</span><span class="sxs-lookup"><span data-stu-id="8a0e1-129">You see the message: “*Importing data...*”</span></span>  

| <span data-ttu-id="8a0e1-130">Cause :</span><span class="sxs-lookup"><span data-stu-id="8a0e1-130">Cause</span></span> | <span data-ttu-id="8a0e1-131">Procédure de résolution</span><span class="sxs-lookup"><span data-stu-id="8a0e1-131">How to fix</span></span> |
| ---   | ---        |
| <span data-ttu-id="8a0e1-132">Selon la taille de votre locataire, cette étape peut prendre de quelques minutes à 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="8a0e1-132">Depending on the size of your tenant, this step could take anywhere from a few mins to 30 minutes.</span></span> | <span data-ttu-id="8a0e1-133">Soyez patient.</span><span class="sxs-lookup"><span data-stu-id="8a0e1-133">Just be patient.</span></span> <span data-ttu-id="8a0e1-134">Si votre tableau de bord ne s’affiche pas à la place du message au bout d’une heure, soumettez un ticket de support.</span><span class="sxs-lookup"><span data-stu-id="8a0e1-134">If the message does not change to showing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="8a0e1-135">Pour plus d’informations, consultez [Comment obtenir une assistance pour Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="8a0e1-135">For more details, see [How to get support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="8a0e1-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8a0e1-136">Next steps</span></span>

<span data-ttu-id="8a0e1-137">Pour installer le pack de contenu Power BI pour Azure Active Directory Preview, cliquez [ici](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span><span class="sxs-lookup"><span data-stu-id="8a0e1-137">To install the Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


