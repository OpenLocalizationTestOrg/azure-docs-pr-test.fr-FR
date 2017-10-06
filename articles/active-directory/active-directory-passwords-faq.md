---
title: "Forum aux questions : réinitialisation du mot de passe en libre-service Azure AD | Microsoft Docs"
description: "Forum aux questions concernant la réinitialisation du mot de passe en libre-service Azure AD"
services: active-directory
keywords: "Gestion des mots de passe Active Directory, gestion des mots de passe, réinitialisation de mot de passe en libre-service Azure AD"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="1704b-104">Forum Aux Questions sur la gestion des mots de passe</span><span class="sxs-lookup"><span data-stu-id="1704b-104">Password management frequently asked questions</span></span>

<span data-ttu-id="1704b-105">Hello suivant est des questions fréquemment posées pour tous les éléments liés toopassword réinitialiser.</span><span class="sxs-lookup"><span data-stu-id="1704b-105">hello following are some frequently asked questions for all things related toopassword reset.</span></span>

<span data-ttu-id="1704b-106">Si vous avez une question générale sur Azure AD et le mot de passe libre-service réinitialisation, ce qui reste sans réponse ici, vous pouvez demander Communauté de hello pour obtenir une assistance sur hello [les forums Azure Ad](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span><span class="sxs-lookup"><span data-stu-id="1704b-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask hello community for assistance on hello [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="1704b-107">Les membres de la Communauté de hello inclure les ingénieurs, les chefs de produit, les MVP et autres professionnels de l’informatique.</span><span class="sxs-lookup"><span data-stu-id="1704b-107">Members of hello community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="1704b-108">Cette FAQ est divisée en hello les sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="1704b-108">This FAQ is split into hello following sections:</span></span>

* [<span data-ttu-id="1704b-109">**Questions relatives à l’inscription à la réinitialisation du mot de passe**</span><span class="sxs-lookup"><span data-stu-id="1704b-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="1704b-110">**Questions relatives à la réinitialisation du mot de passe**</span><span class="sxs-lookup"><span data-stu-id="1704b-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="1704b-111">**Questions relatives au changement du mot de passe**</span><span class="sxs-lookup"><span data-stu-id="1704b-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="1704b-112">**Questions relatives aux rapports de gestion des mots de passe**</span><span class="sxs-lookup"><span data-stu-id="1704b-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="1704b-113">**Questions relatives à l’écriture différée du mot de passe**</span><span class="sxs-lookup"><span data-stu-id="1704b-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="1704b-114">Inscription à la réinitialisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="1704b-114">Password reset registration</span></span>
* <span data-ttu-id="1704b-115">**Q : Mes utilisateurs peuvent-ils inscrire leurs propres données de réinitialisation du mot de passe ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="1704b-116">**R :** Oui, tant que la réinitialisation du mot de passe est activée et qu’ils sont concédés sous licence, ils peuvent accéder portail d’inscription de réinitialisation de mot de passe de toohello à http://aka.ms/ssprsetup tooregister leurs informations d’authentification.</span><span class="sxs-lookup"><span data-stu-id="1704b-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go toohello Password Reset Registration portal at http://aka.ms/ssprsetup tooregister their authentication information.</span></span> <span data-ttu-id="1704b-117">Les utilisateurs peuvent également inscrire en accédant volet d’accès toohello à http://myapps.microsoft.com, onglet hello du profil, puis sur hello Registre pour l’option de réinitialisation de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1704b-117">Users can also register by going toohello access panel at http://myapps.microsoft.com, clicking hello profile tab, and clicking hello Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="1704b-118">**Q : Puis-je définir des données de réinitialisation de mot de passe pour le compte de mes utilisateurs ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="1704b-119">**R :** Oui, vous pouvez le faire avec Azure AD Connect, PowerShell, hello [portail Azure](https://portal.azure.com), ou le portail d’administration Office hello.</span><span class="sxs-lookup"><span data-stu-id="1704b-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, hello [Azure portal](https://portal.azure.com), or hello Office Admin portal.</span></span> <span data-ttu-id="1704b-120">Pour plus d’informations, voir l’article hello [données utilisées par Azure AD libre-service mot de passe réinitialisé](active-directory-passwords-data.md).</span><span class="sxs-lookup"><span data-stu-id="1704b-120">For more information, see hello article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="1704b-121">**Q : Puis-je synchroniser localement des données pour des questions de sécurité ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="1704b-122">**R :** Ce n’est actuellement pas possible.</span><span class="sxs-lookup"><span data-stu-id="1704b-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="1704b-123">**Q : Mes utilisateurs peuvent-ils inscrire des données pour que les autres utilisateurs ne puissent pas les voir ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="1704b-124">**R :** Oui, lorsque les utilisateurs enregistrent des données à l’aide de hello portail de l’enregistrement de la réinitialisation du mot de passe, il est enregistré dans les champs d’authentification privés qui ne sont visibles que par les administrateurs globaux et hello de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1704b-124">**A:** Yes, when users register data using hello Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and hello user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="1704b-125">Si un **compte d’administrateur Azure** enregistre son numéro de téléphone d’authentification, il est également remplie dans le champ de téléphone mobile hello et est visible.</span><span class="sxs-lookup"><span data-stu-id="1704b-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into hello mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="1704b-126">**Q : Mes utilisateurs doivent-ils toobe enregistré avant de pouvoir utiliser la réinitialisation de mot de passe ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-126">**Q:  Do my users have toobe registered before they can use password reset?**</span></span>

  > <span data-ttu-id="1704b-127">**R :** non, si vous définissez suffisamment d’informations d’authentification de leur part, les utilisateurs n’ont pas tooregister.</span><span class="sxs-lookup"><span data-stu-id="1704b-127">**A:** No, if you define enough authentication information on their behalf, users do not have tooregister.</span></span> <span data-ttu-id="1704b-128">Mot de passe de réinitialisation, que vous avez correctement mis en forme des données stockées dans les champs appropriés de hello dans le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="1704b-128">Password reset works as long as you have properly formatted data stored in hello appropriate fields in hello directory.</span></span>
  >
  >
* <span data-ttu-id="1704b-129">**Q : puis-je synchroniser ou définir les champs téléphone d’authentification, E-mail d’authentification ou téléphone d’authentification secondaire hello pour le compte de mes utilisateurs ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-129">**Q:  Can I synchronize or set hello Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="1704b-130">**R :** Ce n’est actuellement pas possible.</span><span class="sxs-lookup"><span data-stu-id="1704b-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="1704b-131">**Q : comment portail de l’enregistrement hello connaît le tooshow options Mes utilisateurs ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-131">**Q:  How does hello registration portal know which options tooshow my users?**</span></span>

  > <span data-ttu-id="1704b-132">**R :** d’inscription portail de réinitialisation de mot de passe hello uniquement montre hello options que vous avez activées pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="1704b-132">**A:** hello password reset registration portal only shows hello options that you have enabled for your users.</span></span> <span data-ttu-id="1704b-133">Ces options sont trouvent sous hello section stratégie de réinitialisation de mot de passe utilisateur de l’onglet configurer de votre annuaire. Par exemple, cela signifie que si vous n’activez pas les questions de sécurité, puis les utilisateurs ne sont pas en mesure de tooregister pour cette option.</span><span class="sxs-lookup"><span data-stu-id="1704b-133">These options are found under hello User Password Reset Policy section of your directory’s Configure tab. For example, this means that if you do not enable security questions, then users are not able tooregister for that option.</span></span>
  >
  >
* <span data-ttu-id="1704b-134">**Q : Quand un utilisateur est-il considéré comme inscrit ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-134">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="1704b-135">**R :** un utilisateur est considéré comme inscrit pour SSPR lorsqu’ils ont enregistrés au moins hello **nombre de tooreset requis de méthodes** que vous avez définie dans hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1704b-135">**A:** A user is considered registered for SSPR when they have registered at least hello **Number of methods required tooreset** that you have set in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="1704b-136">Réinitialisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="1704b-136">Password reset</span></span>
* <span data-ttu-id="1704b-137">**Q : combien de temps dois-je attendre tooreceive un courrier électronique, SMS ou appel téléphonique de réinitialisation de mot de passe ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-137">**Q:  How long should I wait tooreceive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="1704b-138">**R :** par courrier électronique, messages SMS et appels téléphoniques doivent arriver dans inférieurs à une minute, avec hello situant 5 à 20 secondes.</span><span class="sxs-lookup"><span data-stu-id="1704b-138">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with hello normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="1704b-139">Si vous ne recevez pas de notification de hello dans ce laps de temps :</span><span class="sxs-lookup"><span data-stu-id="1704b-139">If you do not receive hello notification in this time frame:</span></span>
        > * <span data-ttu-id="1704b-140">Vérifiez votre dossier de courrier indésirable.</span><span class="sxs-lookup"><span data-stu-id="1704b-140">Check your junk folder.</span></span>
        > * <span data-ttu-id="1704b-141">Numéro hello ou adresse de messagerie utilisés est hello une souhaitées.</span><span class="sxs-lookup"><span data-stu-id="1704b-141">Check hello number or email being contacted is hello one you expect.</span></span>
        > * <span data-ttu-id="1704b-142">Vérifiez que les données d’authentification hello dans le répertoire de hello sont correctement formatées.</span><span class="sxs-lookup"><span data-stu-id="1704b-142">Check hello authentication data in hello directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="1704b-143">Par exemple « +1 4255551234 » ou « user@contoso.com »</span><span class="sxs-lookup"><span data-stu-id="1704b-143">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="1704b-144">**Q : Quelles langues sont prises en charge pour la réinitialisation de mot de passe ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-144">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="1704b-145">**R :** hello d’interface utilisateur de réinitialisation de mot de passe, les messages SMS et voix appels sont localisés dans hello mêmes langues sont prises en charge dans Office 365.</span><span class="sxs-lookup"><span data-stu-id="1704b-145">**A:** hello password reset UI, SMS messages, and voice calls are localized in hello same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="1704b-146">**Q : quelles parties de l’expérience de réinitialisation de mot de passe hello obtient marque lorsque je définis d’organisation dans mon annuaire de personnalisation de l’onglet Configurer ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-146">**Q:  What parts of hello password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="1704b-147">**R :** portail de réinitialisation du mot de passe hello affiche le logo de votre organisation et vous permet de tooconfigure hello contactez votre administrateur lien toopoint tooa personnalisé adresse de messagerie ou URL.</span><span class="sxs-lookup"><span data-stu-id="1704b-147">**A:** hello password reset portal shows your organizational logo and allows you tooconfigure hello Contact your administrator link toopoint tooa custom email or URL.</span></span> <span data-ttu-id="1704b-148">Tout message électronique envoyé par la réinitialisation du mot de passe inclut logo de votre organisation, de couleurs, de nom dans le corps hello de courrier électronique de hello et personnalisées à partir du nom.</span><span class="sxs-lookup"><span data-stu-id="1704b-148">Any email that gets sent by password reset includes your organization’s logo, colors, name in hello body of hello email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="1704b-149">**Q : Comment puis-je pour informer les utilisateurs sur l’emplacement toogo tooreset leurs mots de passe ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-149">**Q:  How can I educate my users about where toogo tooreset their passwords?**</span></span>

  > <span data-ttu-id="1704b-150">**R :** vous pouvez envoyer votre toohttps://passwordreset.microsoftonline.com utilisateurs directement, ou vous pouvez leur demander de tooclick hello **ne peut pas accéder au lien avec votre compte** sur la page de connexion de n’importe quel professionnel ou scolaire.</span><span class="sxs-lookup"><span data-stu-id="1704b-150">**A:** You can send your users toohttps://passwordreset.microsoftonline.com directly, or you can instruct them tooclick hello **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="1704b-151">Vous pouvez également publier ces liens dans un utilisateur de facilement accessibles tooyour sur place.</span><span class="sxs-lookup"><span data-stu-id="1704b-151">You can also publish these links in a place easily accessible tooyour users.</span></span>
  >
  >
* <span data-ttu-id="1704b-152">**Q : Puis-je utiliser cette page à partir d’un appareil mobile ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-152">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="1704b-153">**R :** Oui, cette page fonctionne sur les appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="1704b-153">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="1704b-154">**Q : Prenez-vous en charge le déverrouillage des comptes Active Directory locaux quand les utilisateurs réinitialisent leurs mots de passe ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-154">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="1704b-155">**R :** oui, lorsqu’un utilisateur réinitialise son mot de passe et que l’écriture différée de mot de passe a été déployée à l’aide d’Azure AD Connect, ce compte d’utilisateur est déverrouillé automatiquement lorsqu’il réinitialise son mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1704b-155">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="1704b-156">**Q : Comment puis-je intégrer la réinitialisation de mot de passe directement dans l’expérience de connexion de Bureau de mes utilisateurs ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-156">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="1704b-157">**R :** si vous êtes un client Azure AD Premium, vous pouvez installer le Gestionnaire d’identité Microsoft sans coût supplémentaire et déployer hello local mot de passe réinitialisation solution toomeet cette exigence.</span><span class="sxs-lookup"><span data-stu-id="1704b-157">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy hello on-premises password reset solution toomeet this requirement.</span></span>
  >
  >
* <span data-ttu-id="1704b-158">**Q : Puis-je définir des questions de sécurité différentes pour différents paramètres régionaux ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-158">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="1704b-159">**R :** Ce n’est actuellement pas possible.</span><span class="sxs-lookup"><span data-stu-id="1704b-159">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="1704b-160">**Q : combien de questions puis-je configurer pour l’option d’authentification hello Questions de sécurité ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-160">**Q:  How many questions can we configure for hello Security Questions authentication option?**</span></span>

  > <span data-ttu-id="1704b-161">**R :** vous pouvez configurer des questions de sécurité personnalisé too20 Bonjour [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1704b-161">**A:** You can configure up too20 custom security questions in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="1704b-162">**Q : Quelle doit être la longueur des questions de sécurité ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-162">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="1704b-163">**R :** Les questions de sécurité peuvent comprendre entre 3 et 200 caractères.</span><span class="sxs-lookup"><span data-stu-id="1704b-163">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="1704b-164">**Q : combien de temps peuvent être réponses toosecurity questions ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-164">**Q:  How long may answers toosecurity questions be?**</span></span>

  > <span data-ttu-id="1704b-165">**R :** réponses peuvent contenir 3 caractères too40.</span><span class="sxs-lookup"><span data-stu-id="1704b-165">**A:** Answers may be 3 too40 characters long.</span></span>
  >
  >
* <span data-ttu-id="1704b-166">**Q : des réponses en double toosecurity questions rejetées ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-166">**Q:  Are duplicate answers toosecurity questions rejected?**</span></span>

  > <span data-ttu-id="1704b-167">**R :** Oui, nous rejetons les réponses en double toosecurity questions.</span><span class="sxs-lookup"><span data-stu-id="1704b-167">**A:** Yes, we reject duplicate answers toosecurity questions.</span></span>
  >
  >
* <span data-ttu-id="1704b-168">**Q : mai un Registre utilisateur hello même question de sécurité plusieurs fois ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-168">**Q:  May a user register hello same security question more than once?**</span></span>

  > <span data-ttu-id="1704b-169">**R :** Non, une fois qu’un utilisateur a inscrit une question particulière, il ne peut plus inscrire cette même question une deuxième fois.</span><span class="sxs-lookup"><span data-stu-id="1704b-169">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="1704b-170">**Q : est-il possible tooset une limite minimale des questions de sécurité pour l’inscription et la réinitialisation ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-170">**Q:  Is it possible tooset a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="1704b-171">**R :** Oui, vous pouvez définir une limite pour l’inscription et une autre pour la réinitialisation.</span><span class="sxs-lookup"><span data-stu-id="1704b-171">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="1704b-172">Vous pouvez poser entre 3 et 5 questions de sécurité pour l’inscription et entre 3 et 5 questions pour la réinitialisation.</span><span class="sxs-lookup"><span data-stu-id="1704b-172">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="1704b-173">**Q : si un utilisateur a enregistré plus que hello le nombre maximal de tooreset requis de questions, comment les sont les questions de sécurité sélectionnées lors de la réinitialisation ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-173">**Q:  If a user has registered more than hello maximum number of questions required tooreset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="1704b-174">**R :** sécurité N questions sont sélectionnées au hasard nombre total de hello de questions auxquelles un utilisateur a inscrit, où N est hello **nombre de questions des tooreset requis**.</span><span class="sxs-lookup"><span data-stu-id="1704b-174">**A:** N security questions are selected at random out of hello total number of questions a user has registered for, where N is hello **Number of questions required tooreset**.</span></span> <span data-ttu-id="1704b-175">Par exemple, si un utilisateur a enregistré 5 questions de sécurité, mais seulement 3 sont tooreset requis, 3 Hello 5 sont sélectionnées de manière aléatoire et présentées à la réinitialisation.</span><span class="sxs-lookup"><span data-stu-id="1704b-175">For example, if a user has 5 security questions registered, but only 3 are required tooreset, 3 of hello 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="1704b-176">Si hello utilisateur obtient les questions de toohello les réponses hello incorrect, processus de sélection de hello reproduit tooprevent martelage de question.</span><span class="sxs-lookup"><span data-stu-id="1704b-176">If hello user gets hello answers toohello questions wrong, hello selection process reoccurs tooprevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="1704b-177">**Q : Limitez-vous les tentatives de réinitialisation de mot de passe effectuées en un bref laps de temps ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-177">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="1704b-178">**R :** Oui, il existe des fonctionnalités de sécurité intégrées tooprotect de réinitialisation de mot de passe d’une mauvaise utilisation.</span><span class="sxs-lookup"><span data-stu-id="1704b-178">**A:** Yes, there are security features built into password reset tooprotect from misuse.</span></span> <span data-ttu-id="1704b-179">Les utilisateurs peuvent uniquement tenter 5 réinitialisations de mot de passe en une heure, après quoi leur compte est verrouillé pendant 24 heures.</span><span class="sxs-lookup"><span data-stu-id="1704b-179">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="1704b-180">Ils peuvent uniquement essayer toovalidate un numéro de téléphone 5 fois au sein d’une heure avant d’être verrouillé pendant 24 heures.</span><span class="sxs-lookup"><span data-stu-id="1704b-180">Users may only try toovalidate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="1704b-181">Les utilisateurs peuvent également tenter une même méthode d’authentification seulement 5 fois en une heure, après quoi leur compte est verrouillé pendant 24 heures.</span><span class="sxs-lookup"><span data-stu-id="1704b-181">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="1704b-182">**Q : pour la durée pendant laquelle sont par courrier électronique hello et SMS code secret valide ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-182">**Q:  For how long are hello email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="1704b-183">**R :** hello durée de vie de session pour la réinitialisation du mot de passe est de 105 minutes.</span><span class="sxs-lookup"><span data-stu-id="1704b-183">**A:** hello session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="1704b-184">À partir du début de hello Hello opération de réinitialisation de mot de passe, utilisateur de hello a 105 minutes tooreset leur mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1704b-184">From hello beginning of hello password reset operation, hello user has 105 minutes tooreset their password.</span></span> <span data-ttu-id="1704b-185">Hello par courrier électronique et le code secret à usage unique de SMS ne sont pas valides après l’expiration de cette période.</span><span class="sxs-lookup"><span data-stu-id="1704b-185">hello email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="1704b-186">Modification de mot de passe</span><span class="sxs-lookup"><span data-stu-id="1704b-186">Password change</span></span>
* <span data-ttu-id="1704b-187">**Q : où les utilisateurs doivent accéder toochange leurs mots de passe ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-187">**Q:  Where should my users go toochange their passwords?**</span></span>

  > <span data-ttu-id="1704b-188">**R :** les utilisateurs peuvent modifier leurs mots de passe n’importe où ils voient leur photo de profil ou d’une icône (comme dans le coin supérieur droit hello de leurs [Office 365](https://portal.office.com) ou [volet d’accès](https://myapps.microsoft.com) rencontre.</span><span class="sxs-lookup"><span data-stu-id="1704b-188">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in hello upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="1704b-189">Les utilisateurs peuvent modifier leurs mots de passe à partir de hello [page de profil de panneau d’accès](https://account.activedirectory.windowsazure.com/r#/profile).</span><span class="sxs-lookup"><span data-stu-id="1704b-189">Users may change their passwords from hello [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="1704b-190">Les utilisateurs peuvent également être posées toochange leurs mots de passe automatiquement à l’écran de connexion hello Azure AD si leurs mots de passe ont expiré.</span><span class="sxs-lookup"><span data-stu-id="1704b-190">Users may also be asked toochange their passwords automatically at hello Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="1704b-191">Enfin, les utilisateurs peuvent naviguer toohello [portail de modification de mot de passe Azure AD](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directement s’ils le souhaitent toochange leurs mots de passe.</span><span class="sxs-lookup"><span data-stu-id="1704b-191">Finally, users may navigate toohello [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish toochange their passwords.</span></span>
  >
  >
* <span data-ttu-id="1704b-192">**Q : Mes utilisateurs notifiées Bonjour portail Office lors de l’expiration de leur mot de passe local ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-192">**Q:  Can my users be notified in hello Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="1704b-193">**R :** cela est possible aujourd'hui si vous utilisez AD FS en suivant les instructions hello ici : [envoyer des revendications de stratégie de mot de passe avec ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="1704b-193">**A:** This is possible today if you are using ADFS by following hello instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="1704b-194">Si vous utilisez la synchronisation de hachage de mot de passe, ces notifications ne sont pas prises en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="1704b-194">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="1704b-195">C’est parce que nous ne pas synchroniser les stratégies de mot de passe du site, il est donc pas possible pour nous toocloud de notifications d’expiration toopost rencontre.</span><span class="sxs-lookup"><span data-stu-id="1704b-195">This is because we do not sync password policies from on-premises, so it is not possible for us toopost expiry notifications toocloud experiences.</span></span> <span data-ttu-id="1704b-196">Dans les deux cas, il est également possible trop[avertir les utilisateurs dont les mots de passe sont sur tooexpire à l’aide de PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span><span class="sxs-lookup"><span data-stu-id="1704b-196">In either case, it is also possible too[notify users whose passwords are about tooexpire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="1704b-197">Rapports sur la gestion des mots de passe</span><span class="sxs-lookup"><span data-stu-id="1704b-197">Password management reports</span></span>
* <span data-ttu-id="1704b-198">**Q : combien de temps faut-il pour tooshow données haut sur les rapports de gestion des mots de passe hello ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-198">**Q:  How long does it take for data tooshow up on hello password management reports?**</span></span>

  > <span data-ttu-id="1704b-199">**R :** données doivent apparaître sur les rapports de gestion des mots de passe hello dans les 5 à 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="1704b-199">**A:** Data should appear on hello password management reports within 5-10 minutes.</span></span> <span data-ttu-id="1704b-200">Il certaines instances peut prendre jusqu'à tooan heure tooappear.</span><span class="sxs-lookup"><span data-stu-id="1704b-200">It some instances it may take up tooan hour tooappear.</span></span>
  >
  >
* <span data-ttu-id="1704b-201">**Q : Comment puis-je filtrer les rapports de gestion des mots de passe hello ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-201">**Q:  How can I filter hello password management reports?**</span></span>

  > <span data-ttu-id="1704b-202">**R :** vous pouvez filtrer les rapports de gestion des mots de passe hello en cliquant sur hello petite loupe toohello extrême droite des étiquettes de colonne hello, haut hello du rapport de hello.</span><span class="sxs-lookup"><span data-stu-id="1704b-202">**A:** You can filter hello password management reports by clicking hello small magnifying glass toohello extreme right of hello column labels, near hello top of hello report.</span></span> <span data-ttu-id="1704b-203">Si vous souhaitez toodo de filtrage plus précis, vous pouvez télécharger hello rapport tooexcel et créer un tableau croisé dynamique.</span><span class="sxs-lookup"><span data-stu-id="1704b-203">If you want toodo richer filtering, you can download hello report tooexcel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="1704b-204">**Q : quel est le nombre maximal de hello d’événements sont stockés dans les rapports de gestion des mots de passe hello ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-204">**Q: What is hello maximum number of events are stored in hello password management reports?**</span></span>

  > <span data-ttu-id="1704b-205">**R :** des too75, 000 mot de passe réinitialisation ou mot de passe réinitialisation d’inscription événements est stockée dans les rapports de gestion de mot de passe hello, fractionnement sauvegarder too30 jours.</span><span class="sxs-lookup"><span data-stu-id="1704b-205">**A:** Up too75,000 password reset or password reset registration events are stored in hello password management reports, spanning back up too30 days.</span></span>  <span data-ttu-id="1704b-206">Nous travaillons tooexpand ce numéro tooinclude davantage d’événements.</span><span class="sxs-lookup"><span data-stu-id="1704b-206">We are working tooexpand this number tooinclude more events.</span></span>
  >
  >
* <span data-ttu-id="1704b-207">**Q : comment lointaine faire hello des rapports de gestion de mot de passe ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-207">**Q:  How far back do hello password management reports go?**</span></span>

  > <span data-ttu-id="1704b-208">**R :** des rapports de gestion des mots de passe hello afficher les opérations qui se produisent au sein de hello 30 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="1704b-208">**A:** hello password management reports show operations occurring within hello last 30 days.</span></span> <span data-ttu-id="1704b-209">Pour l’instant, si vous devez tooarchive ces données, vous pouvez télécharger régulièrement des rapports de hello et les enregistrer dans un emplacement distinct.</span><span class="sxs-lookup"><span data-stu-id="1704b-209">For now, if you need tooarchive this data, you can download hello reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="1704b-210">**Q : existe-t-il un nombre maximal de lignes qui peuvent s’afficher dans les rapports de gestion des mots de passe hello ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-210">**Q:  Is there a maximum number of rows that can appear on hello password management reports?**</span></span>

  > <span data-ttu-id="1704b-211">**R :** Oui, un maximum de 75 000 lignes peut-être apparaître sur l’un des rapports de gestion de mot de passe hello, si elles sont en cours indiquées dans hello téléchargées ou l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1704b-211">**A:** Yes, a maximum of 75,000 rows may appear on either of hello password management reports, whether they are being shown in hello UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="1704b-212">**Q : existe-t-il une tooaccess API hello mot de passe réinitialisation ou enregistrement données de rapports ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-212">**Q:  Is there an API tooaccess hello password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="1704b-213">**R :** Oui, consultez hello suivants documentation toolearn comment vous pouvez accéder à un mot de passe hello réinitialiser les flux de données création de rapports.</span><span class="sxs-lookup"><span data-stu-id="1704b-213">**A:** Yes, see hello following documentation toolearn how you can access hello password reset reporting data stream.</span></span>  <span data-ttu-id="1704b-214">[Découvrez comment tooaccess le mot de passe réinitialisé les événements de rapports par programme](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span><span class="sxs-lookup"><span data-stu-id="1704b-214">[Learn how tooaccess password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="1704b-215">Réécriture du mot de passe</span><span class="sxs-lookup"><span data-stu-id="1704b-215">Password writeback</span></span>
* <span data-ttu-id="1704b-216">**Q : comment fonctionne l’écriture différée de mot de passe de travail coulisses hello ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-216">**Q:  How does password writeback work behind hello scenes?**</span></span>

  > <span data-ttu-id="1704b-217">**R :** consultez [le fonctionnement de l’écriture différée de mot de passe](active-directory-passwords-writeback.md) pour une explication de ce qui se produit lorsque vous activez l’écriture différée de mot de passe et le flux des données via le système de hello dans votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="1704b-217">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through hello system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="1704b-218">**Q : combien de temps l’écriture différée de mot de passe ne prend pas toowork ?  Y a-t-il un délai de synchronisation comme avec la synchronisation du hachage de mot de passe ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-218">**Q:  How long does password writeback take toowork?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="1704b-219">**R :** L’écriture différée du mot de passe est instantanée.</span><span class="sxs-lookup"><span data-stu-id="1704b-219">**A:** Password writeback is instant.</span></span> <span data-ttu-id="1704b-220">Il s’agit d’un pipeline synchrone qui fonctionne différemment de la synchronisation du hachage de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1704b-220">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="1704b-221">L’écriture différée de mot de passe permet aux utilisateurs tooget les commentaires en temps réel sur la réussite de leur mot de passe du hello réinitialiser ou modifier l’opération.</span><span class="sxs-lookup"><span data-stu-id="1704b-221">Password writeback allows users tooget real-time feedback about hello success of their password reset or change operation.</span></span> <span data-ttu-id="1704b-222">temps moyen de Hello pour une écriture différée réussie d’un mot de passe est inférieure à 500 ms.</span><span class="sxs-lookup"><span data-stu-id="1704b-222">hello average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="1704b-223">**Q : Si mon compte local est désactivé, comment mon compte/accès cloud est-il affecté ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-223">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="1704b-224">**R :** si votre ID local est désactivé, votre cloud ID ou d’y accéder seront également désactivée au prochain intervalle de synchronisation hello via la connexion à AAD par défaut de DECUBITUS Voici toutes les 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="1704b-224">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at hello next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="1704b-225">**Q : si mon compte local est contraint par une stratégie de mot de passe Active Directory local, SSPR obéissent aux règles de cette stratégie lors de la modification du mot de passe hello ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-225">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change hello password?**</span></span>

  > <span data-ttu-id="1704b-226">**R :** Oui, SSPR s’appuie sur et à respecter hello local stratégie de mot de passe AD, y compris classique stratégie de mot de passe de domaine Active Directory, ainsi que toutes les stratégies de mot de passe affinée définies ciblés tooa donné utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1704b-226">**A:** Yes, SSPR relies on and abides by hello on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted tooa given user.</span></span>
  >
  >
* <span data-ttu-id="1704b-227">**Q : Pour quels types de compte l’écriture différée du mot de passe fonctionne-t-elle ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-227">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="1704b-228">**R :** L’écriture différée du mot de passe fonctionne pour les utilisateurs fédérés et ceux disposant de la synchronisation du hachage de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1704b-228">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="1704b-229">**Q : L’écriture différée du mot de passe applique-t-elle les stratégies de mot de passe de mon domaine ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-229">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="1704b-230">**R :** Oui, l’écriture différée du mot de passe applique l’âge du mot de passe, l’historique, la complexité, les filtres et toute autre restriction que vous pouvez mettre en place sur les mots de passe dans votre domaine local.</span><span class="sxs-lookup"><span data-stu-id="1704b-230">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="1704b-231">**Q : L’écriture différée du mot de passe est-elle sécurisée ?  Comment puis-je être sûr de ne pas être piraté ?**</span><span class="sxs-lookup"><span data-stu-id="1704b-231">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="1704b-232">**R :** Oui, l’écriture différée du mot de passe est sécurisée.</span><span class="sxs-lookup"><span data-stu-id="1704b-232">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="1704b-233">tooread en savoir plus sur les couches de hello quatre de sécurité implémenté par le service de l’écriture différée de mot de passe hello, extraire hello [modèle de sécurité de l’écriture différée de mot de passe](active-directory-passwords-writeback.md#password-writeback-security-model) section dans le fonctionnement de l’écriture différée de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1704b-233">tooread more about hello four layers of security implemented by hello password writeback service, check out hello [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="1704b-234">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1704b-234">Next steps</span></span>

<span data-ttu-id="1704b-235">Hello suivant liens fournit des informations supplémentaires concernant le mot de passe réinitialisé à l’aide d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="1704b-235">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="1704b-236">[**Démarrage rapide**](active-directory-passwords-getting-started.md) : soyez rapidement opérationnel avec la gestion des mots de passe en libre-service d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1704b-236">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="1704b-237">[**Licences**](active-directory-passwords-licensing.md) : configurez vos licences Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1704b-237">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="1704b-238">[**Données** ](active-directory-passwords-data.md) : comprendre les données de hello est nécessaire et comment il est utilisé pour la gestion de mot de passe</span><span class="sxs-lookup"><span data-stu-id="1704b-238">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="1704b-239">[**Déploiement** ](active-directory-passwords-best-practices.md) -planifier et déployer des utilisateurs de tooyour SSPR hello d’aide est disponible ici</span><span class="sxs-lookup"><span data-stu-id="1704b-239">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="1704b-240">[**Personnaliser** ](active-directory-passwords-customize.md) -personnaliser hello apparence Hello SSPR expérience pour votre entreprise.</span><span class="sxs-lookup"><span data-stu-id="1704b-240">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="1704b-241">[**Rapports**](active-directory-passwords-reporting.md) : découvrez si, quand et où vos utilisateurs accèdent aux fonctionnalités de réinitialisation de mot de passe en libre-service</span><span class="sxs-lookup"><span data-stu-id="1704b-241">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="1704b-242">[**Stratégie**](active-directory-passwords-policy.md) : comprenez et définissez les stratégies de mot de passe d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="1704b-242">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="1704b-243">[**Écriture différée de mot de passe**](active-directory-passwords-writeback.md) - fonctionnement de l’écriture différée de mot de passe avec votre annuaire local</span><span class="sxs-lookup"><span data-stu-id="1704b-243">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="1704b-244">[**Présentation approfondie technique** ](active-directory-passwords-how-it-works.md) -accédez derrière hello RIDEAU toounderstand son fonctionnement</span><span class="sxs-lookup"><span data-stu-id="1704b-244">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="1704b-245">[**Résoudre les problèmes** ](active-directory-passwords-troubleshoot.md) -en savoir comment tooresolve commun problèmes que nous pouvons voir avec SSPR</span><span class="sxs-lookup"><span data-stu-id="1704b-245">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
