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
ms.openlocfilehash: b3fab99ff9fab5bc67fa70113dc5b06fac775b09
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="19b3b-104">Forum Aux Questions sur la gestion des mots de passe</span><span class="sxs-lookup"><span data-stu-id="19b3b-104">Password management frequently asked questions</span></span>

<span data-ttu-id="19b3b-105">Voici quelques questions fréquemment posées concernant toutes les tâches liées à la réinitialisation des mots de passe.</span><span class="sxs-lookup"><span data-stu-id="19b3b-105">The following are some frequently asked questions for all things related to password reset.</span></span>

<span data-ttu-id="19b3b-106">Si vous avez une question générale sur Azure AD et la réinitialisation du mot de passe en libre-service, vous ne trouverez pas de réponse ici, mais vous pouvez demander de l’aide à la communauté sur les [forums d’Azure AD](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span><span class="sxs-lookup"><span data-stu-id="19b3b-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask the community for assistance on the [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="19b3b-107">Les membres de la communauté comprennent les ingénieurs, les chefs de produit, MVP et autres professionnels de l’informatique.</span><span class="sxs-lookup"><span data-stu-id="19b3b-107">Members of the community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="19b3b-108">Ce Forum Aux Questions est organisé de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="19b3b-108">This FAQ is split into the following sections:</span></span>

* [<span data-ttu-id="19b3b-109">**Questions relatives à l’inscription à la réinitialisation du mot de passe**</span><span class="sxs-lookup"><span data-stu-id="19b3b-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="19b3b-110">**Questions relatives à la réinitialisation du mot de passe**</span><span class="sxs-lookup"><span data-stu-id="19b3b-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="19b3b-111">**Questions relatives au changement du mot de passe**</span><span class="sxs-lookup"><span data-stu-id="19b3b-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="19b3b-112">**Questions relatives aux rapports de gestion des mots de passe**</span><span class="sxs-lookup"><span data-stu-id="19b3b-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="19b3b-113">**Questions relatives à l’écriture différée du mot de passe**</span><span class="sxs-lookup"><span data-stu-id="19b3b-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="19b3b-114">Inscription à la réinitialisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="19b3b-114">Password reset registration</span></span>
* <span data-ttu-id="19b3b-115">**Q : Mes utilisateurs peuvent-ils inscrire leurs propres données de réinitialisation du mot de passe ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="19b3b-116">**R :** Oui, tant que la réinitialisation de mot de passe est activée et qu’ils disposent d’une licence, vos utilisateurs peuvent accéder au portail d’inscription à la réinitialisation de mot de passe à l’adresse http://aka.ms/ssprsetup pour inscrire leurs informations d’authentification.</span><span class="sxs-lookup"><span data-stu-id="19b3b-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go to the Password Reset Registration portal at http://aka.ms/ssprsetup to register their authentication information.</span></span> <span data-ttu-id="19b3b-117">Les utilisateurs peuvent également s’inscrire via le volet d’accès à l’adresse http://myapps.microsoft.com, cliquer sur l’onglet du profil, puis sur l’option Réinitialiser mon mot de passe.</span><span class="sxs-lookup"><span data-stu-id="19b3b-117">Users can also register by going to the access panel at http://myapps.microsoft.com, clicking the profile tab, and clicking the Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="19b3b-118">**Q : Puis-je définir des données de réinitialisation de mot de passe pour le compte de mes utilisateurs ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="19b3b-119">**R :** Oui, vous pouvez le faire avec Azure AD Connect, PowerShell, le [portail Azure](https://portal.azure.com) ou le portail d’administration d’Office.</span><span class="sxs-lookup"><span data-stu-id="19b3b-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, the [Azure portal](https://portal.azure.com), or the Office Admin portal.</span></span> <span data-ttu-id="19b3b-120">Pour plus d’informations, consultez l’article [Données utilisées par la réinitialisation du mot de passe en libre-service Azure AD](active-directory-passwords-data.md).</span><span class="sxs-lookup"><span data-stu-id="19b3b-120">For more information, see the article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="19b3b-121">**Q : Puis-je synchroniser localement des données pour des questions de sécurité ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="19b3b-122">**R :** Ce n’est actuellement pas possible.</span><span class="sxs-lookup"><span data-stu-id="19b3b-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="19b3b-123">**Q : Mes utilisateurs peuvent-ils inscrire des données pour que les autres utilisateurs ne puissent pas les voir ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="19b3b-124">**R :** Oui, lorsque les utilisateurs inscrivent des données à l’aide du portail d’inscription à la réinitialisation de mot de passe, les données sont enregistrées dans des champs d’authentification privés uniquement visibles par les administrateurs généraux et l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="19b3b-124">**A:** Yes, when users register data using the Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and the user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="19b3b-125">Si un **compte d’administrateur Azure** enregistre son numéro de téléphone d’authentification, il est également rempli dans le champ téléphone mobile et est visible.</span><span class="sxs-lookup"><span data-stu-id="19b3b-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into the mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="19b3b-126">**Q : Mes utilisateurs doivent-ils être inscrits avant de pouvoir utiliser la réinitialisation de mot de passe ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-126">**Q:  Do my users have to be registered before they can use password reset?**</span></span>

  > <span data-ttu-id="19b3b-127">**R :** Non, si vous définissez suffisamment d’informations d’authentification en leur nom, les utilisateurs n’ont pas besoin de s’inscrire.</span><span class="sxs-lookup"><span data-stu-id="19b3b-127">**A:** No, if you define enough authentication information on their behalf, users do not have to register.</span></span> <span data-ttu-id="19b3b-128">La réinitialisation de mot de passe fonctionne tant que vous disposez de données correctement formatées stockées dans les champs appropriés de l’annuaire.</span><span class="sxs-lookup"><span data-stu-id="19b3b-128">Password reset works as long as you have properly formatted data stored in the appropriate fields in the directory.</span></span>
  >
  >
* <span data-ttu-id="19b3b-129">**Q : Puis-je synchroniser ou définir les champs Téléphone d’authentification, Adresse électronique d’authentification ou Téléphone d’authentification secondaire pour le compte de mes utilisateurs ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-129">**Q:  Can I synchronize or set the Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="19b3b-130">**R :** Ce n’est actuellement pas possible.</span><span class="sxs-lookup"><span data-stu-id="19b3b-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="19b3b-131">**Q : Comment le portail d’inscription sait-il quelles options proposer à mes utilisateurs ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-131">**Q:  How does the registration portal know which options to show my users?**</span></span>

  > <span data-ttu-id="19b3b-132">**R :** Le portail d’inscription de réinitialisation de mot de passe affiche uniquement les options que vous avez activées pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="19b3b-132">**A:** The password reset registration portal only shows the options that you have enabled for your users.</span></span> <span data-ttu-id="19b3b-133">Ces options se trouvent sous la section Stratégie de réinitialisation de mot de passe utilisateur de l’onglet Configurer de votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="19b3b-133">These options are found under the User Password Reset Policy section of your directory’s Configure tab.</span></span> <span data-ttu-id="19b3b-134">Par exemple, cela signifie que si vous n’activez pas les questions de sécurité, les utilisateurs ne sont pas en mesure de s’inscrire pour cette option.</span><span class="sxs-lookup"><span data-stu-id="19b3b-134">For example, this means that if you do not enable security questions, then users are not able to register for that option.</span></span>
  >
  >
* <span data-ttu-id="19b3b-135">**Q : Quand un utilisateur est-il considéré comme inscrit ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-135">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="19b3b-136">**R :** Un utilisateur est considéré comme inscrit pour la réinitialisation de mot de passe en libre-service lorsqu’il a enregistré au moins le **Nombre de méthodes requis pour la réinitialisation** défini dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="19b3b-136">**A:** A user is considered registered for SSPR when they have registered at least the **Number of methods required to reset** that you have set in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="19b3b-137">Réinitialisation de mot de passe</span><span class="sxs-lookup"><span data-stu-id="19b3b-137">Password reset</span></span>
* <span data-ttu-id="19b3b-138">**Q : Combien de temps dois-je attendre avant de recevoir un e-mail, un SMS ou un appel téléphonique de la réinitialisation du mot de passe ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-138">**Q:  How long should I wait to receive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="19b3b-139">**R :** Les messages électroniques, les SMS et les appels téléphoniques doivent arriver en moins d’une minute, la plupart du temps dans les 5 à 20 secondes suivant la réinitialisation.</span><span class="sxs-lookup"><span data-stu-id="19b3b-139">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with the normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="19b3b-140">Si vous ne recevez pas la notification dans ce laps de temps :</span><span class="sxs-lookup"><span data-stu-id="19b3b-140">If you do not receive the notification in this time frame:</span></span>
        > * <span data-ttu-id="19b3b-141">Vérifiez votre dossier de courrier indésirable.</span><span class="sxs-lookup"><span data-stu-id="19b3b-141">Check your junk folder.</span></span>
        > * <span data-ttu-id="19b3b-142">Vérifiez que le numéro ou que l’e-mail contacté est celui que vous attendez.</span><span class="sxs-lookup"><span data-stu-id="19b3b-142">Check the number or email being contacted is the one you expect.</span></span>
        > * <span data-ttu-id="19b3b-143">Vérifiez que les données d’authentification dans l’annuaire sont correctes.</span><span class="sxs-lookup"><span data-stu-id="19b3b-143">Check the authentication data in the directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="19b3b-144">Par exemple « +1 4255551234 » ou « user@contoso.com »</span><span class="sxs-lookup"><span data-stu-id="19b3b-144">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="19b3b-145">**Q : Quelles langues sont prises en charge pour la réinitialisation de mot de passe ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-145">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="19b3b-146">**R :** L’interface utilisateur pour la réinitialisation du mot de passe, les SMS et les appels vocaux sont localisés dans les mêmes langues que celles prises en charge dans Office 365.</span><span class="sxs-lookup"><span data-stu-id="19b3b-146">**A:** The password reset UI, SMS messages, and voice calls are localized in the same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="19b3b-147">**Q : Quelles parties de l’expérience de réinitialisation de mot de passe sont personnalisées quand je configure la personnalisation de l’organisation sous l’onglet Configurer de mon annuaire ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-147">**Q:  What parts of the password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="19b3b-148">**R :** Le portail de réinitialisation de mot de passe affiche le logo de votre organisation et vous permet également de configurer le lien Contactez votre administrateur pour qu’il pointe vers une URL ou une adresse de messagerie personnalisée.</span><span class="sxs-lookup"><span data-stu-id="19b3b-148">**A:** The password reset portal shows your organizational logo and allows you to configure the Contact your administrator link to point to a custom email or URL.</span></span> <span data-ttu-id="19b3b-149">Tout message électronique envoyé par la réinitialisation de mot de passe inclut le logo, les couleurs et le nom de votre organisation dans le corps du message électronique, ainsi que le nom personnalisé de l’émetteur.</span><span class="sxs-lookup"><span data-stu-id="19b3b-149">Any email that gets sent by password reset includes your organization’s logo, colors, name in the body of the email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="19b3b-150">**Q : Comment puis-je informer mes utilisateurs des liens sur lesquels ils peuvent cliquer pour réinitialiser leurs mots de passe ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-150">**Q:  How can I educate my users about where to go to reset their passwords?**</span></span>

  > <span data-ttu-id="19b3b-151">**R :** Vous pouvez diriger vos utilisateurs directement vers l’adresse https://passwordreset.microsoftonline.com ou leur demander de cliquer sur le lien **Vous ne parvenez pas à accéder à votre compte ?** qui figure sur n’importe quel écran de connexion à un compte professionnel ou scolaire.</span><span class="sxs-lookup"><span data-stu-id="19b3b-151">**A:** You can send your users to https://passwordreset.microsoftonline.com directly, or you can instruct them to click the **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="19b3b-152">Vous pouvez également publier ces liens dans un endroit facilement accessible à vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="19b3b-152">You can also publish these links in a place easily accessible to your users.</span></span>
  >
  >
* <span data-ttu-id="19b3b-153">**Q : Puis-je utiliser cette page à partir d’un appareil mobile ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-153">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="19b3b-154">**R :** Oui, cette page fonctionne sur les appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="19b3b-154">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="19b3b-155">**Q : Prenez-vous en charge le déverrouillage des comptes Active Directory locaux quand les utilisateurs réinitialisent leurs mots de passe ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-155">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="19b3b-156">**R :** oui, lorsqu’un utilisateur réinitialise son mot de passe et que l’écriture différée de mot de passe a été déployée à l’aide d’Azure AD Connect, ce compte d’utilisateur est déverrouillé automatiquement lorsqu’il réinitialise son mot de passe.</span><span class="sxs-lookup"><span data-stu-id="19b3b-156">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="19b3b-157">**Q : Comment puis-je intégrer la réinitialisation de mot de passe directement dans l’expérience de connexion de Bureau de mes utilisateurs ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-157">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="19b3b-158">**R :**  Si vous vous êtes client Azure AD Premium, vous pouvez installer le Gestionnaire d’identité Microsoft sans coût supplémentaire et déployer la solution locale de réinitialisation de mot de passe pour répondre à cette exigence.</span><span class="sxs-lookup"><span data-stu-id="19b3b-158">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy the on-premises password reset solution to meet this requirement.</span></span>
  >
  >
* <span data-ttu-id="19b3b-159">**Q : Puis-je définir des questions de sécurité différentes pour différents paramètres régionaux ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-159">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="19b3b-160">**R :** Ce n’est actuellement pas possible.</span><span class="sxs-lookup"><span data-stu-id="19b3b-160">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="19b3b-161">**Q : Combien de questions puis-je configurer pour l’option d’authentification Questions de sécurité ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-161">**Q:  How many questions can we configure for the Security Questions authentication option?**</span></span>

  > <span data-ttu-id="19b3b-162">**R :** Vous pouvez configurer jusqu’à 20 questions de sécurité personnalisées dans le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="19b3b-162">**A:** You can configure up to 20 custom security questions in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="19b3b-163">**Q : Quelle doit être la longueur des questions de sécurité ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-163">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="19b3b-164">**R :** Les questions de sécurité peuvent comprendre entre 3 et 200 caractères.</span><span class="sxs-lookup"><span data-stu-id="19b3b-164">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="19b3b-165">**Q : Quelle doit être la longueur des réponses aux questions de sécurité ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-165">**Q:  How long may answers to security questions be?**</span></span>

  > <span data-ttu-id="19b3b-166">**R :** Les réponses doivent comprendre entre 3 et 40 caractères.</span><span class="sxs-lookup"><span data-stu-id="19b3b-166">**A:** Answers may be 3 to 40 characters long.</span></span>
  >
  >
* <span data-ttu-id="19b3b-167">**Q : Les réponses dupliquées aux questions de sécurité sont-elles rejetées ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-167">**Q:  Are duplicate answers to security questions rejected?**</span></span>

  > <span data-ttu-id="19b3b-168">**R :** Oui, nous rejetons les réponses dupliquées aux questions de sécurité.</span><span class="sxs-lookup"><span data-stu-id="19b3b-168">**A:** Yes, we reject duplicate answers to security questions.</span></span>
  >
  >
* <span data-ttu-id="19b3b-169">**Q : Un utilisateur peut-il inscrire plusieurs fois la même question de sécurité ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-169">**Q:  May a user register the same security question more than once?**</span></span>

  > <span data-ttu-id="19b3b-170">**R :** Non, une fois qu’un utilisateur a inscrit une question particulière, il ne peut plus inscrire cette même question une deuxième fois.</span><span class="sxs-lookup"><span data-stu-id="19b3b-170">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="19b3b-171">**Q : Est-il possible de définir un nombre minimal de questions de sécurité pour l’inscription et la réinitialisation ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-171">**Q:  Is it possible to set a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="19b3b-172">**R :** Oui, vous pouvez définir une limite pour l’inscription et une autre pour la réinitialisation.</span><span class="sxs-lookup"><span data-stu-id="19b3b-172">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="19b3b-173">Vous pouvez poser entre 3 et 5 questions de sécurité pour l’inscription et entre 3 et 5 questions pour la réinitialisation.</span><span class="sxs-lookup"><span data-stu-id="19b3b-173">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="19b3b-174">**Q : Si un utilisateur a inscrit plus de questions que le nombre maximal requis pour la réinitialisation, comment les questions de sécurité sont-elles sélectionnées lors de la réinitialisation ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-174">**Q:  If a user has registered more than the maximum number of questions required to reset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="19b3b-175">**R :** N questions de sécurité sont sélectionnées au hasard à partir du nombre total de questions qu’un utilisateur a inscrit, N étant le **nombre de questions requises pour la réinitialisation**.</span><span class="sxs-lookup"><span data-stu-id="19b3b-175">**A:** N security questions are selected at random out of the total number of questions a user has registered for, where N is the **Number of questions required to reset**.</span></span> <span data-ttu-id="19b3b-176">Par exemple, si un utilisateur a inscrit 5 questions de sécurité, alors que seules 3 sont requises pour la réinitialisation, 3 de ces 5 questions sont sélectionnées au hasard et présentées au moment de la réinitialisation.</span><span class="sxs-lookup"><span data-stu-id="19b3b-176">For example, if a user has 5 security questions registered, but only 3 are required to reset, 3 of the 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="19b3b-177">Si l’utilisateur ne répond pas correctement aux questions, le processus de sélection se répète pour éviter de poser toujours les mêmes questions.</span><span class="sxs-lookup"><span data-stu-id="19b3b-177">If the user gets the answers to the questions wrong, the selection process reoccurs to prevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="19b3b-178">**Q : Limitez-vous les tentatives de réinitialisation de mot de passe effectuées en un bref laps de temps ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-178">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="19b3b-179">**R :** Oui, il existe des fonctionnalités de sécurité intégrées à la réinitialisation de mot de passe pour empêcher toute utilisation malveillante.</span><span class="sxs-lookup"><span data-stu-id="19b3b-179">**A:** Yes, there are security features built into password reset to protect from misuse.</span></span> <span data-ttu-id="19b3b-180">Les utilisateurs peuvent uniquement tenter 5 réinitialisations de mot de passe en une heure, après quoi leur compte est verrouillé pendant 24 heures.</span><span class="sxs-lookup"><span data-stu-id="19b3b-180">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="19b3b-181">De même, ils peuvent uniquement essayer de valider un numéro de téléphone 5 fois en une heure, après quoi leur compte est verrouillé pendant 24 heures.</span><span class="sxs-lookup"><span data-stu-id="19b3b-181">Users may only try to validate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="19b3b-182">Les utilisateurs peuvent également tenter une même méthode d’authentification seulement 5 fois en une heure, après quoi leur compte est verrouillé pendant 24 heures.</span><span class="sxs-lookup"><span data-stu-id="19b3b-182">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="19b3b-183">**Q : Quelle est la durée de validité du code secret à usage unique pour les e-mails et les SMS ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-183">**Q:  For how long are the email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="19b3b-184">**R :** La durée de vie de session pour la réinitialisation du mot de passe est de 105 minutes.</span><span class="sxs-lookup"><span data-stu-id="19b3b-184">**A:** The session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="19b3b-185">À compter du début de l’opération de réinitialisation du mot de passe, l’utilisateur dispose de 105 minutes pour le réinitialiser.</span><span class="sxs-lookup"><span data-stu-id="19b3b-185">From the beginning of the password reset operation, the user has 105 minutes to reset their password.</span></span> <span data-ttu-id="19b3b-186">Le code secret à usage unique pour les messages électroniques et les SMS perd sa validité à l’issue de cette période.</span><span class="sxs-lookup"><span data-stu-id="19b3b-186">The email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="19b3b-187">Modification de mot de passe</span><span class="sxs-lookup"><span data-stu-id="19b3b-187">Password change</span></span>
* <span data-ttu-id="19b3b-188">**Q : Où mes utilisateurs doivent-ils aller pour modifier leurs mots de passe ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-188">**Q:  Where should my users go to change their passwords?**</span></span>

  > <span data-ttu-id="19b3b-189">**R :** Les utilisateurs peuvent modifier leurs mots de passe partout où ils voient leur image ou leur icône de profil (par exemple, en haut à droite de leur interface [Office 365](https://portal.office.com) ou [Panneau d’accès](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="19b3b-189">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in the upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="19b3b-190">Les utilisateurs peuvent modifier leurs mots de passe à partir de la [page du profil Panneau d’accès](https://account.activedirectory.windowsazure.com/r#/profile).</span><span class="sxs-lookup"><span data-stu-id="19b3b-190">Users may change their passwords from the [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="19b3b-191">Ils peuvent également être invités à modifier automatiquement leurs mots de passe sur l’écran de connexion Azure AD si leurs mots de passe ont expiré.</span><span class="sxs-lookup"><span data-stu-id="19b3b-191">Users may also be asked to change their passwords automatically at the Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="19b3b-192">Enfin, les utilisateurs peuvent accéder directement au [portail de changement de mot de passe Azure AD](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) s’ils souhaitent modifier leur mot de passe.</span><span class="sxs-lookup"><span data-stu-id="19b3b-192">Finally, users may navigate to the [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish to change their passwords.</span></span>
  >
  >
* <span data-ttu-id="19b3b-193">**Q : Mes utilisateurs peuvent-ils être informés de l’expiration de leur mot de passe local dans le portail Office ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-193">**Q:  Can my users be notified in the Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="19b3b-194">**R :** Cela est actuellement possible si vous utilisez AD FS en suivant les instructions fournies ici : [Configurer AD FS pour envoyer des revendications d’expiration de mot de passe](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="19b3b-194">**A:** This is possible today if you are using ADFS by following the instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="19b3b-195">Si vous utilisez la synchronisation de hachage de mot de passe, ces notifications ne sont pas prises en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="19b3b-195">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="19b3b-196">Comme nous ne synchronisons pas les stratégies de mot de passe en local, nous ne sommes pas en mesure de publier des notifications d’expiration dans les expériences cloud.</span><span class="sxs-lookup"><span data-stu-id="19b3b-196">This is because we do not sync password policies from on-premises, so it is not possible for us to post expiry notifications to cloud experiences.</span></span> <span data-ttu-id="19b3b-197">Dans les deux cas, il est également possible de [notifier les utilisateurs dont les mots de passe sont sur le point d’expirer à l’aide de PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span><span class="sxs-lookup"><span data-stu-id="19b3b-197">In either case, it is also possible to [notify users whose passwords are about to expire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="19b3b-198">Rapports sur la gestion des mots de passe</span><span class="sxs-lookup"><span data-stu-id="19b3b-198">Password management reports</span></span>
* <span data-ttu-id="19b3b-199">**Q : Combien de temps faut-il pour que les données soient affichées dans les rapports de gestion des mots de passe ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-199">**Q:  How long does it take for data to show up on the password management reports?**</span></span>

  > <span data-ttu-id="19b3b-200">**R :** Les données doivent apparaître dans les rapports de gestion des mots de passe dans les cinq à dix minutes.</span><span class="sxs-lookup"><span data-stu-id="19b3b-200">**A:** Data should appear on the password management reports within 5-10 minutes.</span></span> <span data-ttu-id="19b3b-201">Dans certains cas, il faut attendre une heure avant qu’elles n’apparaissent.</span><span class="sxs-lookup"><span data-stu-id="19b3b-201">It some instances it may take up to an hour to appear.</span></span>
  >
  >
* <span data-ttu-id="19b3b-202">**Q : Comment faire pour filtrer les rapports de gestion des mots de passe ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-202">**Q:  How can I filter the password management reports?**</span></span>

  > <span data-ttu-id="19b3b-203">**R :** Vous pouvez filtrer les rapports de gestion des mots de passe en cliquant sur la petite loupe qui se trouve à l’extrême droite des étiquettes de colonnes, près du sommet du rapport.</span><span class="sxs-lookup"><span data-stu-id="19b3b-203">**A:** You can filter the password management reports by clicking the small magnifying glass to the extreme right of the column labels, near the top of the report.</span></span> <span data-ttu-id="19b3b-204">Pour effectuer un filtrage plus précis, vous pouvez télécharger le rapport dans Excel et créer un tableau croisé dynamique.</span><span class="sxs-lookup"><span data-stu-id="19b3b-204">If you want to do richer filtering, you can download the report to excel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="19b3b-205">**Q : quel est le nombre maximal d’événements stockés dans les rapports de gestion de mot de passe ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-205">**Q: What is the maximum number of events are stored in the password management reports?**</span></span>

  > <span data-ttu-id="19b3b-206">**R :** Jusqu’à 75 000 événements de réinitialisation de mot de passe ou d’inscription de réinitialisation de mot de passe sont stockés dans les rapports de gestion de mot de passe, pour une sauvegarde d’une durée de 30 jours.</span><span class="sxs-lookup"><span data-stu-id="19b3b-206">**A:** Up to 75,000 password reset or password reset registration events are stored in the password management reports, spanning back up to 30 days.</span></span>  <span data-ttu-id="19b3b-207">Nous travaillons à l’augmentation de ce nombre pour inclure davantage d’événements.</span><span class="sxs-lookup"><span data-stu-id="19b3b-207">We are working to expand this number to include more events.</span></span>
  >
  >
* <span data-ttu-id="19b3b-208">**Q : Jusqu’à quand remontent les rapports de gestion des mots de passe ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-208">**Q:  How far back do the password management reports go?**</span></span>

  > <span data-ttu-id="19b3b-209">**R :** Les rapports de gestion des mots de passe affichent les opérations qui ont eu lieu durant les 30 derniers jours.</span><span class="sxs-lookup"><span data-stu-id="19b3b-209">**A:** The password management reports show operations occurring within the last 30 days.</span></span> <span data-ttu-id="19b3b-210">Pour le moment, si vous devez archiver ces données, vous pouvez télécharger les rapports régulièrement et les enregistrer dans un emplacement distinct.</span><span class="sxs-lookup"><span data-stu-id="19b3b-210">For now, if you need to archive this data, you can download the reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="19b3b-211">**Q : Existe-t-il une limite au nombre de lignes qui peuvent apparaître dans les rapports de gestion des mots de passe ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-211">**Q:  Is there a maximum number of rows that can appear on the password management reports?**</span></span>

  > <span data-ttu-id="19b3b-212">**R :** Oui, 75 000 lignes au maximum peuvent apparaître dans un rapport de gestion des mots de passe, qu’elles soient téléchargées ou affichées dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="19b3b-212">**A:** Yes, a maximum of 75,000 rows may appear on either of the password management reports, whether they are being shown in the UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="19b3b-213">**Q : existe-t-il une API pour accéder aux données des rapports sur la réinitialisation de mot de passe ou sur l’inscription de réinitialisation de mot de passe ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-213">**Q:  Is there an API to access the password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="19b3b-214">**R :** Oui, consultez la documentation suivante pour savoir comment vous pouvez accéder au flux de données des rapports sur la réinitialisation de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="19b3b-214">**A:** Yes, see the following documentation to learn how you can access the password reset reporting data stream.</span></span>  <span data-ttu-id="19b3b-215">[Découvrez comment accéder par programmation aux événements des rapports sur la réinitialisation de mot de passe](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span><span class="sxs-lookup"><span data-stu-id="19b3b-215">[Learn how to access password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="19b3b-216">Écriture différée du mot de passe</span><span class="sxs-lookup"><span data-stu-id="19b3b-216">Password writeback</span></span>
* <span data-ttu-id="19b3b-217">**Q : Comment l’écriture différée du mot de passe fonctionne-t-elle en arrière-plan ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-217">**Q:  How does password writeback work behind the scenes?**</span></span>

  > <span data-ttu-id="19b3b-218">**R :** Consultez la rubrique [Fonctionnement de l’écriture différée du mot de passe](active-directory-passwords-writeback.md) pour obtenir une explication de ce qui se passe lorsque vous activez l’écriture différée du mot de passe et pour comprendre la manière dont les données circulent entre le système et votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="19b3b-218">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through the system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="19b3b-219">**Q : Combien de temps faut-il pour que l’écriture différée du mot de passe fonctionne ?  Y a-t-il un délai de synchronisation comme avec la synchronisation du hachage de mot de passe ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-219">**Q:  How long does password writeback take to work?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="19b3b-220">**R :** L’écriture différée du mot de passe est instantanée.</span><span class="sxs-lookup"><span data-stu-id="19b3b-220">**A:** Password writeback is instant.</span></span> <span data-ttu-id="19b3b-221">Il s’agit d’un pipeline synchrone qui fonctionne différemment de la synchronisation du hachage de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="19b3b-221">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="19b3b-222">L’écriture différée du mot de passe permet aux utilisateurs d’obtenir des commentaires en temps réel quant à la réussite de la modification ou de la réinitialisation de leur mot de passe.</span><span class="sxs-lookup"><span data-stu-id="19b3b-222">Password writeback allows users to get real-time feedback about the success of their password reset or change operation.</span></span> <span data-ttu-id="19b3b-223">L’écriture différée réussie d’un mot de passe dure en moyenne moins de 500 ms.</span><span class="sxs-lookup"><span data-stu-id="19b3b-223">The average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="19b3b-224">**Q : Si mon compte local est désactivé, comment mon compte/accès cloud est-il affecté ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-224">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="19b3b-225">**R :** Si votre ID local est désactivé, votre ID/accès cloud sera également désactivé lors du prochain intervalle de synchronisation via AAD Connect, par défaut toutes les 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="19b3b-225">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at the next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="19b3b-226">**Q : Si mon compte local est contraint par une stratégie de mot de passe Active Directory local, la réinitialisation de mot de passe en libre-service respecte-t-elle cette stratégie lorsque je modifie le mot de passe ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-226">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change the password?**</span></span>

  > <span data-ttu-id="19b3b-227">**R :** Oui, la réinitialisation de mot de passe en libre-service s’appuie sur et respecte la stratégie de mot de passe AD locale, y compris la stratégie de mot de passe de domaine AD habituelle, ainsi que toute stratégie de mot de passe affinée pour un utilisateur donné.</span><span class="sxs-lookup"><span data-stu-id="19b3b-227">**A:** Yes, SSPR relies on and abides by the on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted to a given user.</span></span>
  >
  >
* <span data-ttu-id="19b3b-228">**Q : Pour quels types de compte l’écriture différée du mot de passe fonctionne-t-elle ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-228">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="19b3b-229">**R :** L’écriture différée du mot de passe fonctionne pour les utilisateurs fédérés et ceux disposant de la synchronisation du hachage de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="19b3b-229">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="19b3b-230">**Q : L’écriture différée du mot de passe applique-t-elle les stratégies de mot de passe de mon domaine ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-230">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="19b3b-231">**R :** Oui, l’écriture différée du mot de passe applique l’âge du mot de passe, l’historique, la complexité, les filtres et toute autre restriction que vous pouvez mettre en place sur les mots de passe dans votre domaine local.</span><span class="sxs-lookup"><span data-stu-id="19b3b-231">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="19b3b-232">**Q : L’écriture différée du mot de passe est-elle sécurisée ?  Comment puis-je être sûr de ne pas être piraté ?**</span><span class="sxs-lookup"><span data-stu-id="19b3b-232">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="19b3b-233">**R :** Oui, l’écriture différée du mot de passe est sécurisée.</span><span class="sxs-lookup"><span data-stu-id="19b3b-233">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="19b3b-234">Pour en savoir plus sur les quatre couches de sécurité implémentées par le service d’écriture différée du mot de passe, consultez [Modèle de sécurité de l’écriture différée du mot de passe](active-directory-passwords-writeback.md#password-writeback-security-model) dans l’article Fonctionnement de l’écriture différée du mot de passe.</span><span class="sxs-lookup"><span data-stu-id="19b3b-234">To read more about the four layers of security implemented by the password writeback service, check out the [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="19b3b-235">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="19b3b-235">Next steps</span></span>

<span data-ttu-id="19b3b-236">Les liens suivants fournissent des informations supplémentaires sur la réinitialisation de mot de passe à l’aide d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19b3b-236">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="19b3b-237">[**Démarrage rapide**](active-directory-passwords-getting-started.md) : soyez rapidement opérationnel avec la gestion des mots de passe en libre-service Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19b3b-237">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="19b3b-238">[**Licences**](active-directory-passwords-licensing.md) : configurez vos licences Azure AD.</span><span class="sxs-lookup"><span data-stu-id="19b3b-238">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="19b3b-239">[**Données**](active-directory-passwords-data.md) : comprenez mieux les données requises et leur utilisation dans la gestion des mots de passe.</span><span class="sxs-lookup"><span data-stu-id="19b3b-239">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="19b3b-240">[**Déploiement**](active-directory-passwords-best-practices.md) : planifiez et déployez la réinitialisation de mot de passe en libre-service pour vos utilisateurs grâce aux conseils figurant ici.</span><span class="sxs-lookup"><span data-stu-id="19b3b-240">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="19b3b-241">[**Personnalisation**](active-directory-passwords-customize.md) : personnalisez l’apparence de l’interface de réinitialisation de mot de passe en libre-service de votre société.</span><span class="sxs-lookup"><span data-stu-id="19b3b-241">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="19b3b-242">[**Rapports**](active-directory-passwords-reporting.md) : découvrez si, quand et où vos utilisateurs accèdent aux fonctionnalités de réinitialisation de mot de passe en libre-service</span><span class="sxs-lookup"><span data-stu-id="19b3b-242">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="19b3b-243">[**Stratégie** ](active-directory-passwords-policy.md) : comprenez et définissez les stratégies de mot de passe d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="19b3b-243">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="19b3b-244">[**Écriture différée de mot de passe** ](active-directory-passwords-writeback.md) - fonctionnement de l’écriture différée de mot de passe avec votre annuaire local</span><span class="sxs-lookup"><span data-stu-id="19b3b-244">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="19b3b-245">[**Présentation technique approfondie** ](active-directory-passwords-how-it-works.md) : découvrez ce qu’il se passe sous le capot pour comprendre le fonctionnement</span><span class="sxs-lookup"><span data-stu-id="19b3b-245">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="19b3b-246">[**Résolution des problèmes** ](active-directory-passwords-troubleshoot.md) : découvrez comment résoudre les problèmes courants que nous observons avec la réinitialisation de mot de passe en libre-service</span><span class="sxs-lookup"><span data-stu-id="19b3b-246">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
