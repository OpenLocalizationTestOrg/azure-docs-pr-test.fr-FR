---
title: "aaaAzure FAQ sur la gestion Active Directory périphérique | Documents Microsoft"
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
ms.openlocfilehash: 000eb6a930187e13cb24cf628793afd06813be23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-device-management-faq"></a><span data-ttu-id="71627-103">FAQ sur la gestion des appareils Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="71627-103">Azure Active Directory device management FAQ</span></span>

<span data-ttu-id="71627-104">**Q : j’inscrit les appareils hello récemment. Pourquoi ne peux pas voir les périphériques hello sous Mes infos utilisateur Bonjour portail Azure ?**</span><span class="sxs-lookup"><span data-stu-id="71627-104">**Q: I registered hello device recently. Why can’t I see hello device under my user info in hello Azure portal?**</span></span>

<span data-ttu-id="71627-105">**R :** les appareils Windows 10 qui sont joints à un domaine avec l’inscription automatique ne s’affichent pas sous les informations d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="71627-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under hello USER info.</span></span>
<span data-ttu-id="71627-106">Vous devez toouse PowerShell toosee tous les appareils.</span><span class="sxs-lookup"><span data-stu-id="71627-106">You need toouse PowerShell toosee all devices.</span></span> 

<span data-ttu-id="71627-107">Uniquement hello périphériques suivants sont répertoriés sous les informations d’utilisateur hello :</span><span class="sxs-lookup"><span data-stu-id="71627-107">Only hello following devices are listed under hello USER info:</span></span>

- <span data-ttu-id="71627-108">Tous les appareils personnels qui ne sont pas joints à une entreprise</span><span class="sxs-lookup"><span data-stu-id="71627-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="71627-109">Tous les appareils non Windows 10 / Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="71627-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="71627-110">Tous les appareils non Windows</span><span class="sxs-lookup"><span data-stu-id="71627-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="71627-111">**Q : Pourquoi ne puis-je pas voir tous les appareils hello inscrits dans Azure Active Directory Bonjour portail Azure ?**</span><span class="sxs-lookup"><span data-stu-id="71627-111">**Q: Why can I not see all hello devices registered in Azure Active Directory in hello Azure portal?**</span></span> 

<span data-ttu-id="71627-112">**R :** , il n’existe actuellement aucune toosee de façon tous les appareils inscrits Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="71627-112">**A:** Currently, there is no way toosee all registered devices in hello Azure portal.</span></span> <span data-ttu-id="71627-113">Vous pouvez utiliser Azure PowerShell toofind tous les appareils.</span><span class="sxs-lookup"><span data-stu-id="71627-113">You can use Azure PowerShell toofind all devices.</span></span> <span data-ttu-id="71627-114">Pour plus d’informations, consultez hello [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="71627-114">For more details, see hello [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="71627-115">**Q : comment savoir quel état de l’inscription de périphérique hello du client de hello est ?**</span><span class="sxs-lookup"><span data-stu-id="71627-115">**Q: How do I know what hello device registration state of hello client is?**</span></span>

<span data-ttu-id="71627-116">**R :** dépend de l’état de l’inscription de périphérique hello :</span><span class="sxs-lookup"><span data-stu-id="71627-116">**A:** hello device registration state depends on:</span></span>

- <span data-ttu-id="71627-117">Quel périphérique hello est</span><span class="sxs-lookup"><span data-stu-id="71627-117">What hello device is</span></span>
- <span data-ttu-id="71627-118">de la manière dont il a été inscrit ;</span><span class="sxs-lookup"><span data-stu-id="71627-118">How it was registered</span></span> 
- <span data-ttu-id="71627-119">Les informations relatives à tooit.</span><span class="sxs-lookup"><span data-stu-id="71627-119">Any details related tooit.</span></span> 
 

---

<span data-ttu-id="71627-120">**Q : Pourquoi est un périphérique que j’ai supprimé Bonjour Azure portal ou à l’aide de Windows PowerShell toujours répertoriés comme inscrit ?**</span><span class="sxs-lookup"><span data-stu-id="71627-120">**Q: Why is a device I have deleted in hello Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="71627-121">**R :** Il s’agit du comportement par défaut.</span><span class="sxs-lookup"><span data-stu-id="71627-121">**A:** This is by design.</span></span> <span data-ttu-id="71627-122">Appareil de Hello n’auront pas accès tooresources dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="71627-122">hello device will not have access tooresources in hello cloud.</span></span> <span data-ttu-id="71627-123">Si vous voulez tooremove hello périphérique et inscrivez de nouveau, une action manuelle doit être toobe effectuée sur le périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="71627-123">If you want tooremove hello device and register again, a manual action must be toobe taken on hello device.</span></span> 

<span data-ttu-id="71627-124">Pour Windows 10 et Windows Server 2016 sur site AD et joints à un domaine :</span><span class="sxs-lookup"><span data-stu-id="71627-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="71627-125">Ouvrez l’invite de commandes hello en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="71627-125">Open hello command prompt as an administrator.</span></span>

2.  <span data-ttu-id="71627-126">Saisissez `dsregcmd.exe /debug /leave`</span><span class="sxs-lookup"><span data-stu-id="71627-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="71627-127">Se déconnecter et se dans la tâche planifiée tootrigger hello qui inscrit le périphérique de hello à nouveau.</span><span class="sxs-lookup"><span data-stu-id="71627-127">Sign out and sign in tootrigger hello scheduled task that registers hello device again.</span></span> 

<span data-ttu-id="71627-128">Pour les autres plateformes Windows sur site AD et jointes à un domaine :</span><span class="sxs-lookup"><span data-stu-id="71627-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="71627-129">Ouvrez l’invite de commandes hello en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="71627-129">Open hello command prompt as an administrator.</span></span>
2.  <span data-ttu-id="71627-130">Saisissez `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span><span class="sxs-lookup"><span data-stu-id="71627-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="71627-131">Saisissez `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span><span class="sxs-lookup"><span data-stu-id="71627-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="71627-132">**Q : Pourquoi le portail Azure affiche-t-il des entrées d’appareils dupliquées ?**</span><span class="sxs-lookup"><span data-stu-id="71627-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="71627-133">**R :**</span><span class="sxs-lookup"><span data-stu-id="71627-133">**A:**</span></span>

-   <span data-ttu-id="71627-134">Pour Windows 10 et Windows Server 2016, s’ils sont des tentatives répétées toounjoin et joignez de nouveau hello même appareil, il peut y avoir des entrées en double.</span><span class="sxs-lookup"><span data-stu-id="71627-134">For Windows 10 and Windows Server 2016, if they are repeated attempts toounjoin and re-join hello same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="71627-135">Si vous avez utilisé Ajouter compte professionnel ou scolaire, chaque utilisateur de windows qui utilise Ajouter compte professionnel ou scolaire créera un nouvel enregistrement d’appareil avec hello même nom de périphérique.</span><span class="sxs-lookup"><span data-stu-id="71627-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with hello same device name.</span></span>

-   <span data-ttu-id="71627-136">Autres plates-formes Windows local AD appartenant au domaine à l’aide de l’inscription automatique créera un nouvel enregistrement d’appareil avec hello même nom de périphérique pour chaque utilisateur de domaine qui se connecte à un périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="71627-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with hello same device name for each domain user who logs into hello device.</span></span> 

-   <span data-ttu-id="71627-137">Un ordinateur AADJ qui a été réinitialisé, réinstallé et nouveau en souscrivant hello même nom, apparaîtront en tant qu’un autre enregistrement hello même nom de périphérique.</span><span class="sxs-lookup"><span data-stu-id="71627-137">An AADJ machine that has been wiped, re-installed and re-joined with hello same name, will show up as another record with hello same device name.</span></span>

---

<span data-ttu-id="71627-138">**Q : Pourquoi peut un utilisateur encore accéder aux ressources d’un appareil, que j’ai désactivé Bonjour portail Azure ?**</span><span class="sxs-lookup"><span data-stu-id="71627-138">**Q: Why can a user still access resources from a device I have disabled in hello Azure portal?**</span></span>

<span data-ttu-id="71627-139">**R :** peut prendre jusqu'à une heure tooan pour un toobe revoke appliqué.</span><span class="sxs-lookup"><span data-stu-id="71627-139">**A:** It can take up tooan hour for a revoke toobe applied.</span></span>

>[!Note] 
><span data-ttu-id="71627-140">Pour les appareils perdus, nous vous recommandons de réinitialisation hello tooensure de périphérique que les utilisateurs ne peut pas accéder à des appareils de hello.</span><span class="sxs-lookup"><span data-stu-id="71627-140">For lost devices, we recommend wiping hello device tooensure that users cannot access hello device.</span></span> <span data-ttu-id="71627-141">Pour plus d’informations, consultez [Inscrire des appareils pour la gestion dans Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span><span class="sxs-lookup"><span data-stu-id="71627-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="71627-142">**Q : Pourquoi mes utilisateurs voient-ils s’afficher « Vous ne pouvez pas accéder à cet emplacement à partir d’ici » ?**</span><span class="sxs-lookup"><span data-stu-id="71627-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="71627-143">**R :** si vous avez configuré certain toorequire de règles d’accès conditionnel un état de périphérique spécifique et les appareils hello ne répond pas aux critères de hello, les utilisateurs sont bloquées et ce message s’affiche.</span><span class="sxs-lookup"><span data-stu-id="71627-143">**A:** If you have configured certain conditional access rules toorequire a specific device state and hello device does not meet hello criteria, users are blocked and see this message.</span></span> <span data-ttu-id="71627-144">Veuillez évaluer les règles de hello et assurez-vous de cet appareil hello est en mesure de toomeet hello critères tooavoid ce message.</span><span class="sxs-lookup"><span data-stu-id="71627-144">Please evaluate hello rules and ensure that hello device is able toomeet hello criteria tooavoid this message.</span></span>

---


<span data-ttu-id="71627-145">**Q : je consultez enregistrement d’appareil hello sous les informations d’utilisateur hello Bonjour portail Azure et que vous pouvez voir l’état de hello tel qu’enregistré sur le client de hello. Ma configuration est-elle correcte pour l’utilisation de l’accès conditionnel ?**</span><span class="sxs-lookup"><span data-stu-id="71627-145">**Q: I see hello device record under hello USER info in hello Azure portal and can see hello state as registered on hello client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="71627-146">**R :** enregistrement d’appareil hello (deviceID) et son état sur hello portail Azure doivent correspondre à des clients de hello et répondent à tous les critères d’évaluation pour l’accès conditionnel.</span><span class="sxs-lookup"><span data-stu-id="71627-146">**A:** hello device record (deviceID) and state on hello Azure portal must match hello client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="71627-147">Pour plus d’informations, consultez [Bien démarrer avec le service Azure Active Directory Device Registration](active-directory-device-registration.md).</span><span class="sxs-lookup"><span data-stu-id="71627-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="71627-148">**Q : je reçois un message « nom d’utilisateur ou mot de passe est incorrect » pour un périphérique j’ai viennent de rejoindre tooAzure AD ?**</span><span class="sxs-lookup"><span data-stu-id="71627-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined tooAzure AD?**</span></span>

<span data-ttu-id="71627-149">**R :** Les raisons les plus courantes sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="71627-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="71627-150">Vos informations d’identification ne sont plus valides.</span><span class="sxs-lookup"><span data-stu-id="71627-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="71627-151">Votre ordinateur est toocommunicate impossible avec Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="71627-151">Your computer is unable toocommunicate with Azure Active Directory.</span></span> <span data-ttu-id="71627-152">Vérifiez les éventuels problèmes de connectivité réseau.</span><span class="sxs-lookup"><span data-stu-id="71627-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="71627-153">Bonjour Azure AD Join conditions préalables n’ont pas été respectées.</span><span class="sxs-lookup"><span data-stu-id="71627-153">hello Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="71627-154">Veuillez vous assurer que vous avez suivi les étapes de hello pour [extension cloud appareils tooWindows 10 de fonctionnalités via Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="71627-154">Please ensure that you have followed hello steps for [Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="71627-155">Connexions fédérées nécessite votre toosupport de serveur de fédération un point de terminaison WS-Trust active.</span><span class="sxs-lookup"><span data-stu-id="71627-155">Federated logins requires your federation server toosupport a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="71627-156">**Q : Pourquoi hello « Désolé... une erreur s’est produite ! « boîte de dialogue lors de le ne joignez pas mon ordinateur ?**</span><span class="sxs-lookup"><span data-stu-id="71627-156">**Q: Why do I see hello “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="71627-157">**R :** Cela résulte de la configuration de l’inscription Azure Active Directory avec Intune.</span><span class="sxs-lookup"><span data-stu-id="71627-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="71627-158">Pour plus d’informations, consultez [Configurer la gestion des appareils Windows](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span><span class="sxs-lookup"><span data-stu-id="71627-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="71627-159">**Q : Pourquoi mon toojoin tentative un PC échouer même si je n’ai reçu aucune information d’erreur ?**</span><span class="sxs-lookup"><span data-stu-id="71627-159">**Q: Why did my attempt toojoin a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="71627-160">**R :** une cause possible est que l’utilisateur hello est enregistré dans le périphérique toohello à l’aide du compte d’administrateur intégré hello.</span><span class="sxs-lookup"><span data-stu-id="71627-160">**A:** A likely cause is that hello user is logged in toohello device using hello built-in administrator account.</span></span> <span data-ttu-id="71627-161">Créez un autre compte local avant d’utiliser le programme d’installation de Azure Active Directory Join toocomplete hello.</span><span class="sxs-lookup"><span data-stu-id="71627-161">Please create a different local account before using Azure Active Directory Join toocomplete hello setup.</span></span> 

---

<span data-ttu-id="71627-162">**Q : où puis-je trouver des instructions d’inscription automatique pour le programme d’installation Bonjour ?**</span><span class="sxs-lookup"><span data-stu-id="71627-162">**Q: Where can I find instructions for hello setup of automatic device registration?**</span></span>

<span data-ttu-id="71627-163">**R :** pour obtenir des instructions détaillées, consultez [comment tooconfigure l’inscription automatique de Windows appartenant au domaine des appareils avec Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="71627-163">**A:** For detailed instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="71627-164">**Q : où puis-je trouver dépannage plus d’informations sur l’inscription automatique hello ?**</span><span class="sxs-lookup"><span data-stu-id="71627-164">**Q: Where can I find troubleshooting information about hello automatic device registration?**</span></span>

<span data-ttu-id="71627-165">**R :** Pour obtenir des informations de résolution des problèmes, consultez :</span><span class="sxs-lookup"><span data-stu-id="71627-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="71627-166">Résolution des problèmes d’enregistrement automatique du domaine joint ordinateurs tooAzure AD – Windows 10 et Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="71627-166">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="71627-167">Résolution des problèmes d’enregistrement automatique du domaine joint tooAzure d’ordinateurs Active Directory pour les clients de bas niveau de Windows</span><span class="sxs-lookup"><span data-stu-id="71627-167">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

