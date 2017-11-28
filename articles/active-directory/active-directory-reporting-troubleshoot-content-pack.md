---
title: "Résolution des problèmes liés aux erreurs du pack de contenu des journaux d’activité Azure Active Directory | Microsoft Docs"
description: "Vous fournit une liste des messages d’erreur des toofix d’activité Active Directory de Azure de hello contenu de pack et suit les."
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
ms.openlocfilehash: 325de65ff1572a2f8f8319c0a52350bda03af3de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-active-directory-activity-logs-content-pack-errors"></a><span data-ttu-id="50501-103">Résolution des problèmes liés aux erreurs du pack de contenu des journaux d’activité Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50501-103">Troubleshooting Azure Active Directory Activity logs content pack errors</span></span> 


<span data-ttu-id="50501-104">Lorsque vous travaillez hello Pack de contenu Power BI pour la version préliminaire de Azure Active Directory, il est possible que vous rencontrez hello les erreurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="50501-104">When working with hello Power BI Content Pack for Azure Active Directory Preview, it is possible that you run into hello following errors:</span></span> 

- [<span data-ttu-id="50501-105">Échec de l’actualisation</span><span class="sxs-lookup"><span data-stu-id="50501-105">Refresh failed</span></span>](active-directory-reporting-troubleshoot-content-pack.md#refresh-failed) 
- [<span data-ttu-id="50501-106">Informations d’identification de source de données tooupdate ayant échoué</span><span class="sxs-lookup"><span data-stu-id="50501-106">Failed tooupdate data source credentials</span></span>](active-directory-reporting-troubleshoot-content-pack.md#failed-to-update-data-source-credentials) 
- [<span data-ttu-id="50501-107">L’importation de données prend trop de temps</span><span class="sxs-lookup"><span data-stu-id="50501-107">Importing of data is taking too long</span></span>](active-directory-reporting-troubleshoot-content-pack.md#importing-of-data-is-taking-too-long) 
 
<span data-ttu-id="50501-108">Cette rubrique vous fournit des informations sur les causes possibles de hello et comment toofix ces erreurs.</span><span class="sxs-lookup"><span data-stu-id="50501-108">This topic provides you with information about hello possible causes and how toofix these errors.</span></span>
 
## <a name="refresh-failed"></a><span data-ttu-id="50501-109">Échec de l’actualisation</span><span class="sxs-lookup"><span data-stu-id="50501-109">Refresh failed</span></span> 
 
<span data-ttu-id="50501-110">**Comment cette erreur est apparue**: courrier électronique à partir de Power BI ou état d’échec dans l’historique d’actualisation hello.</span><span class="sxs-lookup"><span data-stu-id="50501-110">**How this error is surfaced**: Email from Power BI or failed status in hello refresh history.</span></span> 


| <span data-ttu-id="50501-111">Cause :</span><span class="sxs-lookup"><span data-stu-id="50501-111">Cause</span></span> | <span data-ttu-id="50501-112">Comment toofix</span><span class="sxs-lookup"><span data-stu-id="50501-112">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="50501-113">Actualiser les erreurs peuvent être générées lorsque les informations d’identification hello d’utilisateurs hello connexion toohello pack de contenu ont été réinitialisées mais ne pas mis à jour dans les paramètres de connexion hello Hello du pack de contenu hello de défaillance.</span><span class="sxs-lookup"><span data-stu-id="50501-113">Refresh failure errors can be caused when hello credentials of hello users connecting toohello content pack have been reset but not updated in hello connection settings of hello of hello content pack.</span></span> | <span data-ttu-id="50501-114">Dans Power BI, recherchez hello dataset toohello correspondante du tableau de bord Azure Active Directory activité des journaux (journaux d’activité Active Directory de Azure), choisissez planifier l’actualisation, puis entrez vos informations d’identification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50501-114">In Power BI, locate hello dataset corresponding toohello Azure Active Directory Activity logs dashboard (Azure Active Directory Activity logs), choose schedule refresh, and then enter your Azure AD credentials.</span></span> |
| <span data-ttu-id="50501-115">Une actualisation peut échouer en raison de problèmes toodata Bonjour sous-jacent du pack de contenu.</span><span class="sxs-lookup"><span data-stu-id="50501-115">A refresh can fail due toodata issues in hello underlying content pack.</span></span> | <span data-ttu-id="50501-116">Soumettez un ticket de support.</span><span class="sxs-lookup"><span data-stu-id="50501-116">File a support ticket.</span></span> <span data-ttu-id="50501-117">Pour plus d’informations, consultez [comment tooget prennent en charge pour Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="50501-117">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 
 
## <a name="failed-tooupdate-data-source-credentials"></a><span data-ttu-id="50501-118">Informations d’identification de source de données tooupdate ayant échoué</span><span class="sxs-lookup"><span data-stu-id="50501-118">Failed tooupdate data source credentials</span></span> 
 
<span data-ttu-id="50501-119">**Comment cette erreur est apparue**: dans Power BI, lorsque vous vous connectez le pack de contenu toohello activité Active Directory de Azure (aperçu) de journaux.</span><span class="sxs-lookup"><span data-stu-id="50501-119">**How this error is surfaced**: In Power BI, when you are connecting toohello Azure Active Directory Activity logs (preview) content pack.</span></span> 

| <span data-ttu-id="50501-120">Cause :</span><span class="sxs-lookup"><span data-stu-id="50501-120">Cause</span></span> | <span data-ttu-id="50501-121">Comment toofix</span><span class="sxs-lookup"><span data-stu-id="50501-121">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="50501-122">utilisateur de connexion Hello est ni un administrateur global, ni un lecteur de sécurité ou un administrateur de sécurité.</span><span class="sxs-lookup"><span data-stu-id="50501-122">hello connecting user is neither a global admin nor a security reader or a security admin.</span></span> | <span data-ttu-id="50501-123">Utilisez un compte qui est un administrateur global ou d’un lecteur de sécurité ou d’une sécurité admin tooaccess hello les packs de contenu.</span><span class="sxs-lookup"><span data-stu-id="50501-123">Use an account that is either a global admin or a security reader or a security admin tooaccess hello content packs.</span></span> |
| <span data-ttu-id="50501-124">Votre locataire n’est pas de type Premium ou ne compte aucun utilisateur avec un fichier de licence Premium.</span><span class="sxs-lookup"><span data-stu-id="50501-124">Your tenant is not a Premium tenant or doesn't have at least one user with Premium license File.</span></span> | <span data-ttu-id="50501-125">Soumettez un ticket de support.</span><span class="sxs-lookup"><span data-stu-id="50501-125">File a support ticket.</span></span> <span data-ttu-id="50501-126">Pour plus d’informations, consultez [comment tooget prennent en charge pour Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="50501-126">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|
 

 

## <a name="importing-of-data-is-taking-too-long"></a><span data-ttu-id="50501-127">L’importation de données prend trop de temps</span><span class="sxs-lookup"><span data-stu-id="50501-127">Importing of data is taking too long</span></span> 
 
<span data-ttu-id="50501-128">**Comment cette erreur est apparue**: dans Power BI, une fois que vous avez connecté votre pack de contenu, processus d’importation de données de hello démarre tooprepare votre tableau de bord pour le journal d’activité Active Directory de Azure.</span><span class="sxs-lookup"><span data-stu-id="50501-128">**How this error is surfaced**: In Power BI, once you have connected your content pack, hello data import process starts tooprepare your dashboard for Azure Active Directory Activity log.</span></span> <span data-ttu-id="50501-129">Vous voyez le message de type hello : «*l’importation de données...* »</span><span class="sxs-lookup"><span data-stu-id="50501-129">You see hello message: “*Importing data...*”</span></span>  

| <span data-ttu-id="50501-130">Cause :</span><span class="sxs-lookup"><span data-stu-id="50501-130">Cause</span></span> | <span data-ttu-id="50501-131">Comment toofix</span><span class="sxs-lookup"><span data-stu-id="50501-131">How toofix</span></span> |
| ---   | ---        |
| <span data-ttu-id="50501-132">Selon la taille de hello de votre client, cette étape peut prendre de quelques minutes too30 minutes.</span><span class="sxs-lookup"><span data-stu-id="50501-132">Depending on hello size of your tenant, this step could take anywhere from a few mins too30 minutes.</span></span> | <span data-ttu-id="50501-133">Soyez patient.</span><span class="sxs-lookup"><span data-stu-id="50501-133">Just be patient.</span></span> <span data-ttu-id="50501-134">Si le message de type hello ne change pas tooshowing votre tableau de bord dans l’heure, veuillez soumettre un ticket de support.</span><span class="sxs-lookup"><span data-stu-id="50501-134">If hello message does not change tooshowing your dashboard within an hour, please file a support ticket.</span></span> <span data-ttu-id="50501-135">Pour plus d’informations, consultez [comment tooget prennent en charge pour Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span><span class="sxs-lookup"><span data-stu-id="50501-135">For more details, see [How tooget support for Azure Active Directory](active-directory-troubleshooting-support-howto.md).</span></span>|

## <a name="next-steps"></a><span data-ttu-id="50501-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="50501-136">Next steps</span></span>

<span data-ttu-id="50501-137">tooinstall hello Pack de contenu Power BI pour Azure Active Directory en version préliminaire, cliquez sur [ici](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span><span class="sxs-lookup"><span data-stu-id="50501-137">tooinstall hello Power BI Content Pack for Azure Active Directory Preview, click [here](https://powerbi.microsoft.com/en-us/blog/azure-active-directory-meets-power-bi/).</span></span>


