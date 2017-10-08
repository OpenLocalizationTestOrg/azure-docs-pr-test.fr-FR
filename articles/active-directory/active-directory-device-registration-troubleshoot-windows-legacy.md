---
title: ordinateurs joints au aaaTroubleshooting hello-inscription automatique de domaine Azure AD pour les clients de bas niveau Windows | Documents Microsoft
description: "Résolution des problèmes d’inscription automatique hello de domaine Azure AD joint les ordinateurs pour les clients de bas niveau de Windows."
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
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a><span data-ttu-id="05b6b-103">Résolution des problèmes d’enregistrement automatique du domaine joint tooAzure d’ordinateurs Active Directory pour les clients de bas niveau de Windows</span><span class="sxs-lookup"><span data-stu-id="05b6b-103">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span> 

<span data-ttu-id="05b6b-104">Cette rubrique est applicable toohello uniquement après les clients :</span><span class="sxs-lookup"><span data-stu-id="05b6b-104">This topic is applicable only toohello following clients:</span></span> 

- <span data-ttu-id="05b6b-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="05b6b-105">Windows 7</span></span> 
- <span data-ttu-id="05b6b-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="05b6b-106">Windows 8.1</span></span> 
- <span data-ttu-id="05b6b-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="05b6b-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="05b6b-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="05b6b-108">Windows Server 2012</span></span> 
- <span data-ttu-id="05b6b-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="05b6b-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="05b6b-110">Pour Windows 10 ou Windows Server 2016, consultez [résolution des problèmes d’enregistrement automatique du domaine joint ordinateurs tooAzure AD – Windows 10 et Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span><span class="sxs-lookup"><span data-stu-id="05b6b-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="05b6b-111">Cette rubrique suppose que vous avez configuré l’inscription automatique des appareils joints au domaine comme expliqué dans décrites dans [comment tooconfigure l’inscription automatique de Windows appartenant au domaine des appareils avec Azure Active Directory](active-directory-device-registration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="05b6b-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="05b6b-112">Cette rubrique fournit des conseils sur la façon dont des problèmes potentiels de tooresolve de résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="05b6b-112">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  
<span data-ttu-id="05b6b-113">Toonote de certains éléments de résultats :</span><span class="sxs-lookup"><span data-stu-id="05b6b-113">Some things toonote for successful outcomes:</span></span> 

- <span data-ttu-id="05b6b-114">L’inscription de ces clients sur Azure AD est par utilisateur/appareil.</span><span class="sxs-lookup"><span data-stu-id="05b6b-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="05b6b-115">Par exemple : Si jdoe et jharnett connecter toothis périphérique, un enregistrement distinct (DeviceID) est créé pour chacun de ces utilisateurs dans l’onglet info d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="05b6b-115">As an example: If jdoe and jharnett log in toothis device, a separate registration (DeviceID) is created for each of these users in hello USER info tab.</span></span>  

- <span data-ttu-id="05b6b-116">L’inscription de ces clients en dehors de la zone de hello est tootry configuré à l’ouverture et de verrouiller/déverrouiller et il peut y avoir de délai de 5 minutes que cela est déclenché à l’aide d’une tâche du Planificateur de tâches.</span><span class="sxs-lookup"><span data-stu-id="05b6b-116">Registration of these clients out of hello box is configured tootry at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="05b6b-117">Réinstallation du système d’exploitation de hello ou annuler l’inscription manuelle et réinscrire peut créer une nouvelle inscription sur Azure AD et entraîne plusieurs entrées sous l’onglet d’informations utilisateur hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="05b6b-117">A re-install of hello operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="05b6b-118">Étape 1 : Récupération de l’état de l’inscription de hello</span><span class="sxs-lookup"><span data-stu-id="05b6b-118">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="05b6b-119">**état de l’inscription de hello tooverify :**</span><span class="sxs-lookup"><span data-stu-id="05b6b-119">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="05b6b-120">Invite de commandes ouverte hello en tant qu’administrateur</span><span class="sxs-lookup"><span data-stu-id="05b6b-120">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="05b6b-121">Saisissez `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="05b6b-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="05b6b-122">Cette commande affiche une boîte de dialogue qui vous offre plus de détails sur l’état de jointure hello.</span><span class="sxs-lookup"><span data-stu-id="05b6b-122">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="05b6b-124">Étape 2 : Évaluer l’état de l’inscription de hello</span><span class="sxs-lookup"><span data-stu-id="05b6b-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="05b6b-125">Si la jointure de hello n’a pas réussi, boîte de dialogue hello vous offre plus d’informations sur le problème hello qui s’est produite.</span><span class="sxs-lookup"><span data-stu-id="05b6b-125">If hello join was not successful, hello dialog box provides you with details about hello issue that has occured.</span></span>

<span data-ttu-id="05b6b-126">**les problèmes les plus courants Hello sont :**</span><span class="sxs-lookup"><span data-stu-id="05b6b-126">**hello most common issues are:**</span></span>

- <span data-ttu-id="05b6b-127">Une mauvaise configuration d’AD FS ou d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="05b6b-127">A misconfigured AD FS or Azure AD</span></span>

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="05b6b-129">Vous n’êtes pas connecté en tant qu’utilisateur du domaine</span><span class="sxs-lookup"><span data-stu-id="05b6b-129">You are not signed on as a domain user</span></span>

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="05b6b-131">Un quota a été atteint.</span><span class="sxs-lookup"><span data-stu-id="05b6b-131">A quota has been reached</span></span>

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="05b6b-133">Hello service ne répond pas</span><span class="sxs-lookup"><span data-stu-id="05b6b-133">hello service is not responding</span></span> 

    ![Workplace Join pour Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="05b6b-135">Vous trouverez également des informations d’état hello dans le journal des événements hello sous **Applications et Services Log\Microsoft-jonction**.</span><span class="sxs-lookup"><span data-stu-id="05b6b-135">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="05b6b-136">**causes les plus courantes Hello pour un échec d’inscription sont :**</span><span class="sxs-lookup"><span data-stu-id="05b6b-136">**hello most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="05b6b-137">Votre ordinateur n’est pas sur le réseau interne de hello organisation ou un réseau privé virtuel sans connexion tooan locaux contrôleur de domaine Active Directory.</span><span class="sxs-lookup"><span data-stu-id="05b6b-137">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="05b6b-138">Vous êtes connecté sur l’ordinateur tooyour avec un compte d’ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="05b6b-138">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="05b6b-139">Problèmes de configuration du service :</span><span class="sxs-lookup"><span data-stu-id="05b6b-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="05b6b-140">Hello serveur de fédération a été configuré toosupport **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="05b6b-140">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="05b6b-141">Il n’existe aucun objet de Point de connexion qui pointe le nom de domaine vérifié tooyour dans Azure AD dans la forêt hello AD où appartient hello ordinateur.</span><span class="sxs-lookup"><span data-stu-id="05b6b-141">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="05b6b-142">Un utilisateur a atteint la limite de hello des périphériques.</span><span class="sxs-lookup"><span data-stu-id="05b6b-142">A user has reached hello limit of devices.</span></span> <span data-ttu-id="05b6b-143">Consultez Prise en main du service Azure Active Directory Device Registration.</span><span class="sxs-lookup"><span data-stu-id="05b6b-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05b6b-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="05b6b-144">Next steps</span></span>

<span data-ttu-id="05b6b-145">Pour plus d’informations, consultez hello [Forum aux questions sur l’inscription automatique](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="05b6b-145">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
