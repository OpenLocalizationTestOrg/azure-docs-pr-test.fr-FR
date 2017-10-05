---
title: "Résolution des problèmes de l’inscription automatique des ordinateurs joints au domaine Azure Active Directory pour les clients de bas niveau Windows | Microsoft Docs"
description: "Résolution des problèmes de l’inscription automatique des ordinateurs joints au domaine Azure Active Directory pour les clients de bas niveau Windows."
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a7c8ef4c59c53c21258f0c61963d8f994a3946ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad-for-windows-down-level-clients"></a><span data-ttu-id="c8db9-103">Résolution des problèmes de l’inscription automatique des ordinateurs joints au domaine Azure Active Directory pour les clients de bas niveau Windows</span><span class="sxs-lookup"><span data-stu-id="c8db9-103">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span> 

<span data-ttu-id="c8db9-104">Cette rubrique s’applique uniquement aux clients suivants :</span><span class="sxs-lookup"><span data-stu-id="c8db9-104">This topic is applicable only to the following clients:</span></span> 

- <span data-ttu-id="c8db9-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="c8db9-105">Windows 7</span></span> 
- <span data-ttu-id="c8db9-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="c8db9-106">Windows 8.1</span></span> 
- <span data-ttu-id="c8db9-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="c8db9-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="c8db9-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="c8db9-108">Windows Server 2012</span></span> 
- <span data-ttu-id="c8db9-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="c8db9-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="c8db9-110">Pour Windows 10 ou Windows Server 2016, voir [Résolution des problèmes de l’inscription automatique des ordinateurs joints au domaine Azure Active Directory pour Windows 10 et Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span><span class="sxs-lookup"><span data-stu-id="c8db9-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="c8db9-111">Cette rubrique suppose que vous avez configuré l’inscription automatique d’appareils joints à un domaine comme décrit dans [Configuration de l’inscription automatique auprès d’Azure Active Directory d’appareils Windows joints à un domaine](active-directory-device-registration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c8db9-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="c8db9-112">Cette rubrique vous fournit des conseils sur la façon de résoudre les problèmes potentiels.</span><span class="sxs-lookup"><span data-stu-id="c8db9-112">This topic provides you with troubleshooting guidance on how to resolve potential issues.</span></span>  
<span data-ttu-id="c8db9-113">Voici quelques points à noter pour obtenir des résultats corrects :</span><span class="sxs-lookup"><span data-stu-id="c8db9-113">Some things to note for successful outcomes:</span></span> 

- <span data-ttu-id="c8db9-114">L’inscription de ces clients sur Azure AD est par utilisateur/appareil.</span><span class="sxs-lookup"><span data-stu-id="c8db9-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="c8db9-115">Par exemple, si jdoe et jharnett se connectent à cet appareil, un enregistrement distinct (DeviceID) est créé pour chacun de ces utilisateurs dans l’onglet des informations UTILISATEUR.</span><span class="sxs-lookup"><span data-stu-id="c8db9-115">As an example: If jdoe and jharnett log in to this device, a separate registration (DeviceID) is created for each of these users in the USER info tab.</span></span>  

- <span data-ttu-id="c8db9-116">L’inscription prédéfinie de ces clients est configurée pour être tentée à l’ouverture de session ou au verrouillage/déverrouillage, et il peut y avoir un délai de 5 minutes déclenché par une tâche du Planificateur de tâches.</span><span class="sxs-lookup"><span data-stu-id="c8db9-116">Registration of these clients out of the box is configured to try at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="c8db9-117">Une réinstallation du système d’exploitation, ou une désinscription et une réinscription manuelles, peuvent créer une nouvelle inscription sur Azure AD et aboutir à plusieurs entrées sous l’onglet des informations UTILISATEUR dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="c8db9-117">A re-install of the operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under the USER info tab in the Azure portal.</span></span> 


## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="c8db9-118">Étape 1 : Récupérer l’état de l’inscription</span><span class="sxs-lookup"><span data-stu-id="c8db9-118">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="c8db9-119">**Pour vérifier l’état de l’inscription :**</span><span class="sxs-lookup"><span data-stu-id="c8db9-119">**To verify the registration status:**</span></span>  

1. <span data-ttu-id="c8db9-120">Ouvrez une invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="c8db9-120">Open the command prompt as an administrator</span></span> 

2. <span data-ttu-id="c8db9-121">Saisissez `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="c8db9-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="c8db9-122">Cette commande affiche une boîte de dialogue qui vous donne plus de détails sur l’état de la jonction.</span><span class="sxs-lookup"><span data-stu-id="c8db9-122">This command displays a dialog box that provides you with more details about the join status.</span></span>

![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="c8db9-124">Étape 2 : Évaluer l’état de l’inscription</span><span class="sxs-lookup"><span data-stu-id="c8db9-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="c8db9-125">Si la jonction n’a pas réussi, la boîte de dialogue vous fournit plus d’informations sur le problème qui s’est produit.</span><span class="sxs-lookup"><span data-stu-id="c8db9-125">If the join was not successful, the dialog box provides you with details about the issue that has occured.</span></span>

<span data-ttu-id="c8db9-126">**Les tâches les plus courantes sont :**</span><span class="sxs-lookup"><span data-stu-id="c8db9-126">**The most common issues are:**</span></span>

- <span data-ttu-id="c8db9-127">Une mauvaise configuration d’AD FS ou d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8db9-127">A misconfigured AD FS or Azure AD</span></span>

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="c8db9-129">Vous n’êtes pas connecté en tant qu’utilisateur du domaine</span><span class="sxs-lookup"><span data-stu-id="c8db9-129">You are not signed on as a domain user</span></span>

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="c8db9-131">Un quota a été atteint.</span><span class="sxs-lookup"><span data-stu-id="c8db9-131">A quota has been reached</span></span>

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="c8db9-133">Le service ne répond pas.</span><span class="sxs-lookup"><span data-stu-id="c8db9-133">The service is not responding</span></span> 

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="c8db9-135">Vous pouvez également trouver les informations d’état dans le journal des événements sous **Applications and Services Log\Microsoft-Workplace Join**.</span><span class="sxs-lookup"><span data-stu-id="c8db9-135">You can also find the status information in the event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="c8db9-136">**Les causes les plus courantes d’un échec d’inscription sont :**</span><span class="sxs-lookup"><span data-stu-id="c8db9-136">**The most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="c8db9-137">Votre ordinateur n’est pas sur le réseau interne de l’entreprise ou un réseau privé virtuel sans connexion à un contrôleur de domaine Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="c8db9-137">Your computer is not on the organization’s internal network or a VPN without connection to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="c8db9-138">Vous êtes connecté à votre ordinateur avec un compte d’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="c8db9-138">You are logged on to your computer with a local computer account.</span></span> 

- <span data-ttu-id="c8db9-139">Problèmes de configuration du service :</span><span class="sxs-lookup"><span data-stu-id="c8db9-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="c8db9-140">Le serveur de fédération a été configuré pour prendre en charge **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="c8db9-140">The federation server has been configured to support **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="c8db9-141">Il n’existe aucun objet de point de connexion de service qui pointe vers le nom de votre domaine vérifié dans Azure AD dans la forêt Active Directory à laquelle l’ordinateur appartient.</span><span class="sxs-lookup"><span data-stu-id="c8db9-141">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to.</span></span>

  - <span data-ttu-id="c8db9-142">Un utilisateur a atteint la limite d’appareils.</span><span class="sxs-lookup"><span data-stu-id="c8db9-142">A user has reached the limit of devices.</span></span> <span data-ttu-id="c8db9-143">Consultez Prise en main du service Azure Active Directory Device Registration.</span><span class="sxs-lookup"><span data-stu-id="c8db9-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8db9-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c8db9-144">Next steps</span></span>

<span data-ttu-id="c8db9-145">Pour plus d’informations, consultez le [FAQ sur l’inscription d’appareils automatique](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="c8db9-145">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
