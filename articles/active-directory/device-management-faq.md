---
title: FAQ sur la gestion des appareils Azure Active Directory | Documents Microsoft
description: FAQ sur la gestion des appareils Azure Active Directory.
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
ms.openlocfilehash: 2934b64c693f6505ddb389766374e31a5e6f249b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-device-management-faq"></a><span data-ttu-id="fb79c-103">FAQ sur la gestion des appareils Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb79c-103">Azure Active Directory device management FAQ</span></span>

<span data-ttu-id="fb79c-104">**Q : J’ai enregistré récemment l’appareil. Pourquoi ne puis-je pas voir l’appareil sous mes informations d’utilisateur dans le portail Azure ?**</span><span class="sxs-lookup"><span data-stu-id="fb79c-104">**Q: I registered the device recently. Why can’t I see the device under my user info in the Azure portal?**</span></span>

<span data-ttu-id="fb79c-105">**R :** Les appareils Windows 10 qui sont joints à un domaine avec l’inscription d’appareils automatique ne s’affichent pas sous les informations UTILISATEUR.</span><span class="sxs-lookup"><span data-stu-id="fb79c-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under the USER info.</span></span>
<span data-ttu-id="fb79c-106">Vous devez utiliser PowerShell pour afficher tous les appareils.</span><span class="sxs-lookup"><span data-stu-id="fb79c-106">You need to use PowerShell to see all devices.</span></span> 

<span data-ttu-id="fb79c-107">Seuls les appareils suivants sont répertoriés sous les informations UTILISATEUR :</span><span class="sxs-lookup"><span data-stu-id="fb79c-107">Only the following devices are listed under the USER info:</span></span>

- <span data-ttu-id="fb79c-108">Tous les appareils personnels qui ne sont pas joints à une entreprise</span><span class="sxs-lookup"><span data-stu-id="fb79c-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="fb79c-109">Tous les appareils non Windows 10 / Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="fb79c-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="fb79c-110">Tous les appareils non Windows</span><span class="sxs-lookup"><span data-stu-id="fb79c-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="fb79c-111">**Q : Pourquoi ne puis-je pas voir tous les appareils inscrits auprès d’Azure Active Directory dans le portail Azure ?**</span><span class="sxs-lookup"><span data-stu-id="fb79c-111">**Q: Why can I not see all the devices registered in Azure Active Directory in the Azure portal?**</span></span> 

<span data-ttu-id="fb79c-112">**R :** Actuellement, il n’existe aucun moyen d’afficher tous les appareils inscrits dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="fb79c-112">**A:** Currently, there is no way to see all registered devices in the Azure portal.</span></span> <span data-ttu-id="fb79c-113">Vous pouvez utiliser Azure PowerShell pour rechercher tous les appareils.</span><span class="sxs-lookup"><span data-stu-id="fb79c-113">You can use Azure PowerShell to find all devices.</span></span> <span data-ttu-id="fb79c-114">Pour plus d’informations, consultez l’applet de commande [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="fb79c-114">For more details, see the [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="fb79c-115">**Q : Comment puis-je connaître l’état de l’inscription d’appareils du client ?**</span><span class="sxs-lookup"><span data-stu-id="fb79c-115">**Q: How do I know what the device registration state of the client is?**</span></span>

<span data-ttu-id="fb79c-116">**R :** L’état de l’inscription d’appareils dépend des facteurs suivants :</span><span class="sxs-lookup"><span data-stu-id="fb79c-116">**A:** The device registration state depends on:</span></span>

- <span data-ttu-id="fb79c-117">du type d’appareil concerné ;</span><span class="sxs-lookup"><span data-stu-id="fb79c-117">What the device is</span></span>
- <span data-ttu-id="fb79c-118">de la manière dont il a été inscrit ;</span><span class="sxs-lookup"><span data-stu-id="fb79c-118">How it was registered</span></span> 
- <span data-ttu-id="fb79c-119">de tous les détails qui lui sont associés.</span><span class="sxs-lookup"><span data-stu-id="fb79c-119">Any details related to it.</span></span> 
 

---

<span data-ttu-id="fb79c-120">**Q : Pourquoi un appareil que j’ai supprimé dans le portail Azure ou à l’aide de Windows PowerShell est-il toujours répertorié comme inscrit ?**</span><span class="sxs-lookup"><span data-stu-id="fb79c-120">**Q: Why is a device I have deleted in the Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="fb79c-121">**R :** Il s’agit du comportement par défaut.</span><span class="sxs-lookup"><span data-stu-id="fb79c-121">**A:** This is by design.</span></span> <span data-ttu-id="fb79c-122">L’appareil n’aura pas accès aux ressources dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="fb79c-122">The device will not have access to resources in the cloud.</span></span> <span data-ttu-id="fb79c-123">Si vous souhaitez supprimer l’appareil et l’inscrire à nouveau, vous devez effectuer une action manuelle sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="fb79c-123">If you want to remove the device and register again, a manual action must be to be taken on the device.</span></span> 

<span data-ttu-id="fb79c-124">Pour Windows 10 et Windows Server 2016 sur site AD et joints à un domaine :</span><span class="sxs-lookup"><span data-stu-id="fb79c-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="fb79c-125">Ouvrez une invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="fb79c-125">Open the command prompt as an administrator.</span></span>

2.  <span data-ttu-id="fb79c-126">Saisissez `dsregcmd.exe /debug /leave`</span><span class="sxs-lookup"><span data-stu-id="fb79c-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="fb79c-127">Déconnectez puis reconnectez-vous pour déclencher la tâche planifiée qui inscrit à nouveau l’appareil.</span><span class="sxs-lookup"><span data-stu-id="fb79c-127">Sign out and sign in to trigger the scheduled task that registers the device again.</span></span> 

<span data-ttu-id="fb79c-128">Pour les autres plateformes Windows sur site AD et jointes à un domaine :</span><span class="sxs-lookup"><span data-stu-id="fb79c-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="fb79c-129">Ouvrez une invite de commandes en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="fb79c-129">Open the command prompt as an administrator.</span></span>
2.  <span data-ttu-id="fb79c-130">Saisissez `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span><span class="sxs-lookup"><span data-stu-id="fb79c-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="fb79c-131">Saisissez `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span><span class="sxs-lookup"><span data-stu-id="fb79c-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="fb79c-132">**Q : Pourquoi le portail Azure affiche-t-il des entrées d’appareils dupliquées ?**</span><span class="sxs-lookup"><span data-stu-id="fb79c-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="fb79c-133">**R :**</span><span class="sxs-lookup"><span data-stu-id="fb79c-133">**A:**</span></span>

-   <span data-ttu-id="fb79c-134">Pour Windows 10 et Windows Server 2016, en cas de tentatives répétées visant à disjoindre et à joindre à nouveau le même appareil, des entrées dupliquées peuvent s’afficher.</span><span class="sxs-lookup"><span data-stu-id="fb79c-134">For Windows 10 and Windows Server 2016, if they are repeated attempts to unjoin and re-join the same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="fb79c-135">Si vous avez utilisé « Ajouter un compte professionnel ou scolaire », chaque utilisateur Windows qui utilise « Ajouter un compte professionnel ou scolaire » créera un nouvel enregistrement d’appareil avec le même nom d’appareil.</span><span class="sxs-lookup"><span data-stu-id="fb79c-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with the same device name.</span></span>

-   <span data-ttu-id="fb79c-136">Les autres plateformes Windows sur site AD jointes à un domaine à l’aide de l’inscription automatique créeront un nouvel enregistrement d’appareil avec le même nom d’appareil pour chaque utilisateur du domaine qui se connecte à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="fb79c-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with the same device name for each domain user who logs into the device.</span></span> 

-   <span data-ttu-id="fb79c-137">Une machine AADJ qui a été réinitialisée, réinstallée et jointe à nouveau avec le même nom s’affichera en tant que nouvel enregistrement avec le même nom d’appareil.</span><span class="sxs-lookup"><span data-stu-id="fb79c-137">An AADJ machine that has been wiped, re-installed and re-joined with the same name, will show up as another record with the same device name.</span></span>

---

<span data-ttu-id="fb79c-138">**Q : Pourquoi un utilisateur peut-il toujours accéder aux ressources à partir d’un appareil que j’ai désactivé dans le portail Azure ?**</span><span class="sxs-lookup"><span data-stu-id="fb79c-138">**Q: Why can a user still access resources from a device I have disabled in the Azure portal?**</span></span>

<span data-ttu-id="fb79c-139">**R :** Une opération de révocation peut prendre jusqu’à une heure pour être entièrement appliquée.</span><span class="sxs-lookup"><span data-stu-id="fb79c-139">**A:** It can take up to an hour for a revoke to be applied.</span></span>

>[!Note] 
><span data-ttu-id="fb79c-140">Pour les appareils perdus, nous vous recommandons de réinitialiser l’appareil pour vous assurer que les utilisateurs ne puissent pas y accéder.</span><span class="sxs-lookup"><span data-stu-id="fb79c-140">For lost devices, we recommend wiping the device to ensure that users cannot access the device.</span></span> <span data-ttu-id="fb79c-141">Pour plus d’informations, consultez [Inscrire des appareils pour la gestion dans Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span><span class="sxs-lookup"><span data-stu-id="fb79c-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="fb79c-142">**Q : Pourquoi mes utilisateurs voient-ils s’afficher « Vous ne pouvez pas accéder à cet emplacement à partir d’ici » ?**</span><span class="sxs-lookup"><span data-stu-id="fb79c-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="fb79c-143">**R :** Si vous avez configuré certaines règles d’accès conditionnel pour exiger un état d’appareil spécifique et que l’appareil ne respecte pas les critères, les utilisateurs sont bloqués et ce message s’affiche.</span><span class="sxs-lookup"><span data-stu-id="fb79c-143">**A:** If you have configured certain conditional access rules to require a specific device state and the device does not meet the criteria, users are blocked and see this message.</span></span> <span data-ttu-id="fb79c-144">Veuillez évaluer les règles et vous assurer que l’appareil est en mesure de respecter les critères pour éviter l’affichage de ce message.</span><span class="sxs-lookup"><span data-stu-id="fb79c-144">Please evaluate the rules and ensure that the device is able to meet the criteria to avoid this message.</span></span>

---


<span data-ttu-id="fb79c-145">**Q : Je vois l’enregistrement d’appareil sous les informations UTILISATEUR dans le portail Azure, ainsi que l’état en tant qu’inscrit sur le client. Ma configuration est-elle correcte pour l’utilisation de l’accès conditionnel ?**</span><span class="sxs-lookup"><span data-stu-id="fb79c-145">**Q: I see the device record under the USER info in the Azure portal and can see the state as registered on the client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="fb79c-146">**R :** L’enregistrement d’appareil (deviceID) et l’état sur le portail Azure doivent correspondre au client et respecter les critères d’évaluation de l’accès conditionnel.</span><span class="sxs-lookup"><span data-stu-id="fb79c-146">**A:** The device record (deviceID) and state on the Azure portal must match the client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="fb79c-147">Pour plus d’informations, consultez [Bien démarrer avec le service Azure Active Directory Device Registration](active-directory-device-registration.md).</span><span class="sxs-lookup"><span data-stu-id="fb79c-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="fb79c-148">**Q : Pourquoi est-ce que je reçois le message « nom d’utilisateur ou mot de passe incorrect » pour un appareil que je viens juste de joindre à Azure AD ?**</span><span class="sxs-lookup"><span data-stu-id="fb79c-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined to Azure AD?**</span></span>

<span data-ttu-id="fb79c-149">**R :** Les raisons les plus courantes sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="fb79c-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="fb79c-150">Vos informations d’identification ne sont plus valides.</span><span class="sxs-lookup"><span data-stu-id="fb79c-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="fb79c-151">Votre ordinateur n’est pas en mesure de communiquer avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fb79c-151">Your computer is unable to communicate with Azure Active Directory.</span></span> <span data-ttu-id="fb79c-152">Vérifiez les éventuels problèmes de connectivité réseau.</span><span class="sxs-lookup"><span data-stu-id="fb79c-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="fb79c-153">Les conditions préalables pour la jonction à Azure AD n’ont pas été respectées.</span><span class="sxs-lookup"><span data-stu-id="fb79c-153">The Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="fb79c-154">Veuillez vous assurer que vous avez respecté les étapes de la section [Extension des fonctionnalités du cloud aux appareils Windows 10 via Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fb79c-154">Please ensure that you have followed the steps for [Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="fb79c-155">Les connexions fédérées nécessitent que votre serveur de fédération prenne en charge un point de terminaison WS-Trust actif.</span><span class="sxs-lookup"><span data-stu-id="fb79c-155">Federated logins requires your federation server to support a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="fb79c-156">**Q : Pourquoi la boîte de dialogue « Désolé... une erreur s’est produite ! » s’affiche-t-elle lorsque j’essaye d’inscrire mon ordinateur ?**</span><span class="sxs-lookup"><span data-stu-id="fb79c-156">**Q: Why do I see the “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="fb79c-157">**R :** Cela résulte de la configuration de l’inscription Azure Active Directory avec Intune.</span><span class="sxs-lookup"><span data-stu-id="fb79c-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="fb79c-158">Pour plus d’informations, consultez [Configurer la gestion des appareils Windows](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span><span class="sxs-lookup"><span data-stu-id="fb79c-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="fb79c-159">**Q : Pourquoi ma tentative d’inscription d’un ordinateur a-t-elle échoué alors que je n’ai reçu aucune information d’erreur ?**</span><span class="sxs-lookup"><span data-stu-id="fb79c-159">**Q: Why did my attempt to join a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="fb79c-160">**R :** Une cause possible est que l’utilisateur est connecté à l’appareil à l’aide du compte administrateur intégré.</span><span class="sxs-lookup"><span data-stu-id="fb79c-160">**A:** A likely cause is that the user is logged in to the device using the built-in administrator account.</span></span> <span data-ttu-id="fb79c-161">Créez un compte local distinct avant d’utiliser Azure Active Directory Join pour terminer la configuration.</span><span class="sxs-lookup"><span data-stu-id="fb79c-161">Please create a different local account before using Azure Active Directory Join to complete the setup.</span></span> 

---

<span data-ttu-id="fb79c-162">**Q : Où puis-je trouver des instructions pour la configuration de l’inscription automatique  d’appareils ?**</span><span class="sxs-lookup"><span data-stu-id="fb79c-162">**Q: Where can I find instructions for the setup of automatic device registration?**</span></span>

<span data-ttu-id="fb79c-163">**R :** Pour plus d’instructions, consultez [Configuration de l’inscription automatique auprès d’Azure Active Directory d’appareils Windows joints à un domaine](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="fb79c-163">**A:** For detailed instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="fb79c-164">**Q : Où puis-je trouver des informations de résolution des problèmes concernant l’inscription d’appareils automatique ?**</span><span class="sxs-lookup"><span data-stu-id="fb79c-164">**Q: Where can I find troubleshooting information about the automatic device registration?**</span></span>

<span data-ttu-id="fb79c-165">**R :** Pour obtenir des informations de résolution des problèmes, consultez :</span><span class="sxs-lookup"><span data-stu-id="fb79c-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="fb79c-166">Résolution des problèmes de l’inscription automatique des ordinateurs joints au domaine à Azure AD – Windows 10 et Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="fb79c-166">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="fb79c-167">Résolution des problèmes de l’inscription automatique des ordinateurs joints au domaine à Azure AD pour les clients de bas niveau Windows</span><span class="sxs-lookup"><span data-stu-id="fb79c-167">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

