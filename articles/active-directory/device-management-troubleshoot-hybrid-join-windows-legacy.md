---
title: "Dépanner des appareils hybrides de bas niveau joints à Azure Active Directory | Microsoft Docs"
description: "Dépannez des appareils hybrides de bas niveau joints à Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 715fca79e488ae3759926181c244a42026f4a554
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a><span data-ttu-id="0c1e0-103">Dépanner des appareils hybrides de bas niveau joints à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0c1e0-103">Troubleshooting hybrid Azure Active Directory joined down-level devices</span></span> 

<span data-ttu-id="0c1e0-104">Cette rubrique s’applique uniquement aux appareils suivants :</span><span class="sxs-lookup"><span data-stu-id="0c1e0-104">This topic is applicable only to the following devices:</span></span> 

- <span data-ttu-id="0c1e0-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="0c1e0-105">Windows 7</span></span> 
- <span data-ttu-id="0c1e0-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="0c1e0-106">Windows 8.1</span></span> 
- <span data-ttu-id="0c1e0-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="0c1e0-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="0c1e0-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="0c1e0-108">Windows Server 2012</span></span> 
- <span data-ttu-id="0c1e0-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0c1e0-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="0c1e0-110">Pour Windows 10 ou Windows Server 2016, consultez la page [Dépanner des appareils hybrides Windows 10 et Windows Server 2016 joints à Azure Active Directory](device-management-troubleshoot-hybrid-join-windows-current.md).</span><span class="sxs-lookup"><span data-stu-id="0c1e0-110">For Windows 10 or Windows Server 2016, see [Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices](device-management-troubleshoot-hybrid-join-windows-current.md).</span></span>

<span data-ttu-id="0c1e0-111">Cette rubrique suppose que vous avez [configuré les appareils hybrides joints à Azure Active Directory](device-management-hybrid-azuread-joined-devices-setup.md) de façon à prendre en charge les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="0c1e0-111">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) to support the following scenarios:</span></span>

- <span data-ttu-id="0c1e0-112">Accès conditionnel basé sur les appareils</span><span class="sxs-lookup"><span data-stu-id="0c1e0-112">Device-based conditional access</span></span>

- [<span data-ttu-id="0c1e0-113">Itinérance d’entreprise des paramètres</span><span class="sxs-lookup"><span data-stu-id="0c1e0-113">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="0c1e0-114">Windows Hello Entreprise</span><span class="sxs-lookup"><span data-stu-id="0c1e0-114">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md) 





<span data-ttu-id="0c1e0-115">Cette rubrique vous fournit des conseils sur la façon de résoudre les problèmes potentiels.</span><span class="sxs-lookup"><span data-stu-id="0c1e0-115">This topic provides you with troubleshooting guidance on how to resolve potential issues.</span></span>  

<span data-ttu-id="0c1e0-116">**Bon à savoir :**</span><span class="sxs-lookup"><span data-stu-id="0c1e0-116">**What you should know:**</span></span> 

- <span data-ttu-id="0c1e0-117">Le nombre maximal d’appareils par utilisateur dépend de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="0c1e0-117">The maximum number of devices per user is device-centric.</span></span> <span data-ttu-id="0c1e0-118">Par exemple, si *jdoe* et *jharnett* se connectent à un appareil, une inscription (DeviceID) distincte est créée pour chacun d’eux dans l’onglet d’informations **UTILISATEUR**.</span><span class="sxs-lookup"><span data-stu-id="0c1e0-118">For example, if *jdoe* and *jharnett* sign-in to a device, a separate registration (DeviceID) is created for each of them in the **USER** info tab.</span></span>  

- <span data-ttu-id="0c1e0-119">L’inscription / jointure d’appareils initiale est configurée pour effectuer une tentative à l’ouverture de session ou au verrouillage / déverrouillage.</span><span class="sxs-lookup"><span data-stu-id="0c1e0-119">The initial registration / join of devices is configured to perform an attempt at either logon or lock / unlock.</span></span> <span data-ttu-id="0c1e0-120">Un délai de cinq minutes peut être déclenché par une tâche du Planificateur de tâches.</span><span class="sxs-lookup"><span data-stu-id="0c1e0-120">There could be 5-minute delay triggered by a task scheduler task.</span></span> 

- <span data-ttu-id="0c1e0-121">La réinstallation du système d’exploitation de même qu’une désinscription / réinscription manuelle sont susceptibles de créer une nouvelle inscription sur Azure AD et d’aboutir à plusieurs entrées sous l’onglet d’informations UTILISATEUR sur le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0c1e0-121">A reinstall of the operating system or a manual unregister and re-register may create a new registration on Azure AD and results in multiple entries under the USER info tab in the Azure portal.</span></span> 


## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="0c1e0-122">Étape 1 : Récupérer l’état de l’inscription</span><span class="sxs-lookup"><span data-stu-id="0c1e0-122">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="0c1e0-123">**Pour vérifier l’état de l’inscription :**</span><span class="sxs-lookup"><span data-stu-id="0c1e0-123">**To verify the registration status:**</span></span>  

1. <span data-ttu-id="0c1e0-124">Ouvrez une invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="0c1e0-124">Open the command prompt as an administrator</span></span> 

2. <span data-ttu-id="0c1e0-125">Saisissez `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="0c1e0-125">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="0c1e0-126">Cette commande affiche une boîte de dialogue qui vous donne plus de détails sur l’état de la jonction.</span><span class="sxs-lookup"><span data-stu-id="0c1e0-126">This command displays a dialog box that provides you with more details about the join status.</span></span>

![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-the-hybrid-azure-ad-join-status"></a><span data-ttu-id="0c1e0-128">Étape 2 : Évaluer l’état de la jointure Azure AD hybride</span><span class="sxs-lookup"><span data-stu-id="0c1e0-128">Step 2: Evaluate the hybrid Azure AD join status</span></span> 

<span data-ttu-id="0c1e0-129">Si la jointure Azure AD hybride n’a pas réussi, la boîte de dialogue vous fournit des informations sur le problème qui s’est produit.</span><span class="sxs-lookup"><span data-stu-id="0c1e0-129">If the hybrid Azure AD join was not successful, the dialog box provides you with details about the issue that has occurred.</span></span>

<span data-ttu-id="0c1e0-130">**Les tâches les plus courantes sont :**</span><span class="sxs-lookup"><span data-stu-id="0c1e0-130">**The most common issues are:**</span></span>

- <span data-ttu-id="0c1e0-131">Une mauvaise configuration d’AD FS ou d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c1e0-131">A misconfigured AD FS or Azure AD</span></span>

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="0c1e0-133">Vous n’êtes pas connecté en tant qu’utilisateur du domaine</span><span class="sxs-lookup"><span data-stu-id="0c1e0-133">You are not signed on as a domain user</span></span>

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="0c1e0-135">Un quota a été atteint.</span><span class="sxs-lookup"><span data-stu-id="0c1e0-135">A quota has been reached</span></span>

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="0c1e0-137">Le service ne répond pas.</span><span class="sxs-lookup"><span data-stu-id="0c1e0-137">The service is not responding</span></span> 

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="0c1e0-139">Vous pouvez également trouver les informations d’état dans le journal des événements sous **Applications and Services Log\Microsoft-Workplace Join**.</span><span class="sxs-lookup"><span data-stu-id="0c1e0-139">You can also find the status information in the event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="0c1e0-140">**Voici les causes les plus courantes d’échec d’une jointure Azure AD hybride :**</span><span class="sxs-lookup"><span data-stu-id="0c1e0-140">**The most common causes for a failed hybrid Azure AD join are:**</span></span> 

- <span data-ttu-id="0c1e0-141">Votre ordinateur n’est pas sur le réseau interne de l’entreprise ou un réseau privé virtuel sans connexion à un contrôleur de domaine Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="0c1e0-141">Your computer is not on the organization’s internal network or a VPN without connection to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="0c1e0-142">Vous êtes connecté à votre ordinateur avec un compte d’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="0c1e0-142">You are logged on to your computer with a local computer account.</span></span> 

- <span data-ttu-id="0c1e0-143">Problèmes de configuration du service :</span><span class="sxs-lookup"><span data-stu-id="0c1e0-143">Service configuration issues:</span></span> 

  - <span data-ttu-id="0c1e0-144">Le serveur de fédération a été configuré pour prendre en charge **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="0c1e0-144">The federation server has been configured to support **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="0c1e0-145">Il n’existe aucun objet de point de connexion de service qui pointe vers le nom de votre domaine vérifié dans Azure AD dans la forêt Active Directory à laquelle l’ordinateur appartient.</span><span class="sxs-lookup"><span data-stu-id="0c1e0-145">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to.</span></span>

  - <span data-ttu-id="0c1e0-146">Un utilisateur a atteint la limite d’appareils.</span><span class="sxs-lookup"><span data-stu-id="0c1e0-146">A user has reached the limit of devices.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0c1e0-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0c1e0-147">Next steps</span></span>

<span data-ttu-id="0c1e0-148">Pour toute question, consultez [FAQ sur la gestion des appareils](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="0c1e0-148">For questions, see the [device management FAQ](device-management-faq.md)</span></span>  
