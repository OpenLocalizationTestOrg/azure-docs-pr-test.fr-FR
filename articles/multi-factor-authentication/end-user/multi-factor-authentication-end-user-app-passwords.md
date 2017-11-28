---
title: "aaaHow toouse mots de passe d’application dans Azure MFA ? | Microsoft Docs"
description: "Cette page sera aider les utilisateurs à comprendre quelles sont les mots de passe d’application et ce qu’ils sont utilisés pour avec respect tooAzure l’authentification Multifacteur."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 345b757b-5a2b-48eb-953f-d363313be9e5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: kgremban
ms.custom: end-user
ms.openlocfilehash: bf2c11edc0ca81f2950eff0f7a3a24c8a5b34623
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-app-passwords-in-azure-multi-factor-authentication"></a><span data-ttu-id="a449f-104">Que sont les mots de passe d’application dans Azure Multi-Factor Authentication ?</span><span class="sxs-lookup"><span data-stu-id="a449f-104">What are App Passwords in Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="a449f-105">Actuellement, certaines des applications non-Web, tels que hello Apple messagerie native client qui utilise Exchange Active Sync, ne prennent pas en charge l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="a449f-105">Certain non-browser apps, such as hello Apple native email client that uses Exchange Active Sync, currently do not support multi-factor authentication.</span></span> <span data-ttu-id="a449f-106">L’authentification multifacteur est activée par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a449f-106">Multi-factor authentication is enabled per user.</span></span> <span data-ttu-id="a449f-107">Cela signifie que si un utilisateur a été activé pour l’authentification multifacteur et ils essaient de toouse des applications non-Web, elles seront toodo Impossible donc.</span><span class="sxs-lookup"><span data-stu-id="a449f-107">This means that if a user has been enabled for multi-factor authentication and they are attempting toouse non-browser apps, they will be unable toodo so.</span></span> <span data-ttu-id="a449f-108">Un mot de passe permet cette toooccur.</span><span class="sxs-lookup"><span data-stu-id="a449f-108">An app password allows this toooccur.</span></span>

<span data-ttu-id="a449f-109">Une fois que vous disposez d’un mot de passe d’application, vous l’utilisez à la place de votre mot de passe d’origine avec ces applications sans navigateur.</span><span class="sxs-lookup"><span data-stu-id="a449f-109">Once you have an app password, you use this in place of your original password with these non-browser apps.</span></span> <span data-ttu-id="a449f-110">Il s’agit, car lorsque vous inscrivez pour la vérification en deux étapes, vous indiquez à Microsoft pas les toolet tout le monde vous connecter avec votre mot de passe si elles ne peut pas également effectuer la vérification de second hello.</span><span class="sxs-lookup"><span data-stu-id="a449f-110">This is because when you register for two-step verification, you're telling Microsoft not toolet anyone sign in with your password if they can't also perform hello second verification.</span></span> <span data-ttu-id="a449f-111">client de messagerie native Apple Hello sur votre téléphone ne peut pas se connecter en tant que vous, car il ne peut pas demander de vérification en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="a449f-111">hello Apple native email client on your phone can't sign in as you because it can't ask for two-step verification.</span></span> <span data-ttu-id="a449f-112">Pour résoudre ce Hello est toocreate un mot de passe d’application plus sécurisée que vous n’utilisez pas quotidiennes, mais uniquement pour les applications qui ne prennent pas en charge vérification en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="a449f-112">hello solution for this is toocreate a more secure app password that you don't use day-to-day, but only for those apps that can't support two-step verification.</span></span> <span data-ttu-id="a449f-113">Utilisez un mot de passe application hello afin que les applications qui peuvent contourner l’authentification multifacteur et continuer toowork.</span><span class="sxs-lookup"><span data-stu-id="a449f-113">Use hello app password so that apps can bypass multi-factor authentication and continue toowork.</span></span>

> [!NOTE]
> <span data-ttu-id="a449f-114">Les clients Office 2013 (y compris Outlook) prennent en charge de nouveaux protocoles d’authentification et peuvent être utilisés dans le cadre de la vérification en deux étapes.</span><span class="sxs-lookup"><span data-stu-id="a449f-114">Office 2013 clients (including Outlook) support new authentication protocols and can be used with two-step verification.</span></span>  <span data-ttu-id="a449f-115">Ainsi, une fois activés, les mots de passe d’application ne sont pas obligatoires avec les clients Office 2013.</span><span class="sxs-lookup"><span data-stu-id="a449f-115">This means that once enabled, app passwords are not required for use with Office 2013 clients.</span></span>  <span data-ttu-id="a449f-116">Pour plus d’informations, consultez [Version préliminaire publique de l’authentification moderne Office 2013 annoncée](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span><span class="sxs-lookup"><span data-stu-id="a449f-116">For more information, see [Office 2013 modern authentication public preview announced](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/).</span></span>


## <a name="how-toouse-app-passwords"></a><span data-ttu-id="a449f-117">Comment les mots de passe toouse application</span><span class="sxs-lookup"><span data-stu-id="a449f-117">How toouse app passwords</span></span>
<span data-ttu-id="a449f-118">Hello Voici certains tooremember de choses sur la façon de mots de passe d’application toouse.</span><span class="sxs-lookup"><span data-stu-id="a449f-118">hello following are some things tooremember on how toouse app passwords.</span></span>

* <span data-ttu-id="a449f-119">Vous ne pouvez pas créer vos propres mots de passe d’application.</span><span class="sxs-lookup"><span data-stu-id="a449f-119">You don't create your own app passwords.</span></span> <span data-ttu-id="a449f-120">En effet, ils sont générés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="a449f-120">Instead, they are automatically generated.</span></span> <span data-ttu-id="a449f-121">Étant donné que vous n’avez tooenter hello mot de passe une fois par application, il est plus sûr toouse un mot de passe plus complexe, générée automatiquement plutôt que d’effectuer une que vous pouvez mémoriser.</span><span class="sxs-lookup"><span data-stu-id="a449f-121">Since you only have tooenter hello app password once per app, it's safer toouse a more complex, automatically generated password rather than making one that you can remember.</span></span>
* <span data-ttu-id="a449f-122">À l’heure actuelle, un utilisateur peut posséder jusqu’à 40 mots de passe.</span><span class="sxs-lookup"><span data-stu-id="a449f-122">Currently there is a limit of 40 passwords per user.</span></span> <span data-ttu-id="a449f-123">Si vous essayez de toocreate un fois que vous avez atteint la limite de hello, vous serez toodelete invité à un de vos mots de passe d’application existant avant de créer un nouveau.</span><span class="sxs-lookup"><span data-stu-id="a449f-123">If you attempt toocreate one after you have reached hello limit, you will be prompted toodelete one of your existing app passwords before you create a new one.</span></span>
* <span data-ttu-id="a449f-124">Il est recommandé d’utiliser un mot de passe d’application par appareil, et non par application.</span><span class="sxs-lookup"><span data-stu-id="a449f-124">You should use one app password per device, not per application.</span></span> <span data-ttu-id="a449f-125">Par exemple, vous pouvez créer un mot de passe d’application pour votre ordinateur portable et utiliser ce mot de passe pour toutes vos applications sur cet ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a449f-125">For example, you can create one app password for your laptop and use that app password for all of your applications on that laptop.</span></span> <span data-ttu-id="a449f-126">Ensuite, créez une deuxième toouse de mot de passe d’application pour toutes vos applications sur votre bureau.</span><span class="sxs-lookup"><span data-stu-id="a449f-126">Then, create a second app password toouse for all your apps on your desktop.</span></span> 
* <span data-ttu-id="a449f-127">Première fois que vous inscrivez pour la vérification en deux étapes, vous pouvez soit un hello de mot de passe d’application.</span><span class="sxs-lookup"><span data-stu-id="a449f-127">You are given one app password hello first time you register for two-step verification.</span></span>  <span data-ttu-id="a449f-128">Si vous avez besoin d’autres mots de passe, vous pouvez les créer.</span><span class="sxs-lookup"><span data-stu-id="a449f-128">If you need additional ones, you can create them.</span></span>



## <a name="creating-and-deleting-app-passwords"></a><span data-ttu-id="a449f-129">Création et suppression des mots de passe d’application</span><span class="sxs-lookup"><span data-stu-id="a449f-129">Creating and deleting app passwords</span></span>
<span data-ttu-id="a449f-130">À la première connexion, vous obtenez un mot de passe d’application que vous pouvez utiliser.</span><span class="sxs-lookup"><span data-stu-id="a449f-130">During your initial sign-in you are given an app password that you can use.</span></span>  <span data-ttu-id="a449f-131">En outre, vous pouvez également créer et supprimer des mots de passe d’application par la suite.</span><span class="sxs-lookup"><span data-stu-id="a449f-131">Additionally you can also create and delete app passwords later on.</span></span>  <span data-ttu-id="a449f-132">La procédure à suivre dépend de l’utilisation de l’authentification multifacteur.</span><span class="sxs-lookup"><span data-stu-id="a449f-132">How you do this depends on how you use multi-factor authentication.</span></span> <span data-ttu-id="a449f-133">Toodetermine où vous devez adresser des mots de passe d’application toomanage de questions hello de réponse suivant :</span><span class="sxs-lookup"><span data-stu-id="a449f-133">Answer hello following questions toodetermine where you should go toomanage app passwords:</span></span> 

1. <span data-ttu-id="a449f-134">Utilisez-vous la vérification en deux étapes pour votre compte Microsoft personnel ?</span><span class="sxs-lookup"><span data-stu-id="a449f-134">Do you use two-step verification for your personal Microsoft account?</span></span> <span data-ttu-id="a449f-135">Si Oui, vous devez faire référence toohello [mots de passe d’application et de la vérification en deux étapes](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article d’aide.</span><span class="sxs-lookup"><span data-stu-id="a449f-135">If yes, you should refer toohello [App passwords and two-step verification](https://support.microsoft.com/help/12409/microsoft-account-app-passwords-two-step-verification) article for help.</span></span> <span data-ttu-id="a449f-136">Si non, continuer tooquestion deux.</span><span class="sxs-lookup"><span data-stu-id="a449f-136">If no, continue tooquestion two.</span></span>

2. <span data-ttu-id="a449f-137">Vous utilisez la vérification en deux étapes pour votre compte professionnel ou scolaire.</span><span class="sxs-lookup"><span data-stu-id="a449f-137">Ok, so you use two-step verification for your work or school account.</span></span> <span data-ttu-id="a449f-138">Vous l’utilisez toosign dans les applications tooOffice 365 ?</span><span class="sxs-lookup"><span data-stu-id="a449f-138">Do you use it toosign in tooOffice 365 apps?</span></span> <span data-ttu-id="a449f-139">Si Oui, vous devez faire référence trop[créer un mot de passe d’application pour Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) de l’aide.</span><span class="sxs-lookup"><span data-stu-id="a449f-139">If yes, you should refer too[Create an app password for Office 365](https://support.office.com/article/Create-an-app-password-for-Office-365-3e7c860f-bda4-4441-a618-b53953ee1183) for help.</span></span> <span data-ttu-id="a449f-140">Si non, continuer tooquestion trois.</span><span class="sxs-lookup"><span data-stu-id="a449f-140">If no, continue tooquestion three.</span></span> 

3. <span data-ttu-id="a449f-141">Utilisez-vous la vérification en deux étapes avec Microsoft Azure ?</span><span class="sxs-lookup"><span data-stu-id="a449f-141">Do you use two-step verification with Microsoft Azure?</span></span> <span data-ttu-id="a449f-142">Si Oui, continuer toohello [gérer les mots de passe d’application Bonjour Azure portal](#manage-app-passwords-in-the-Azure-portal) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="a449f-142">If yes, continue toohello [Manage app passwords in hello Azure portal](#manage-app-passwords-in-the-Azure-portal) section of this article.</span></span> <span data-ttu-id="a449f-143">Si non, continuer tooquestion quatre.</span><span class="sxs-lookup"><span data-stu-id="a449f-143">If no, continue tooquestion four.</span></span>

4. <span data-ttu-id="a449f-144">Vous ne savez pas exactement dans quels cas vous utilisez la vérification en deux étapes ?</span><span class="sxs-lookup"><span data-stu-id="a449f-144">Not sure where you use two-step verification?</span></span> <span data-ttu-id="a449f-145">Continuer toohello [gérer les mots de passe d’application avec le portail de MyApps hello](#manage-app-passwords-with-the-myapps-portal) section de cet article.</span><span class="sxs-lookup"><span data-stu-id="a449f-145">Continue toohello [Manage app passwords with hello MyApps portal](#manage-app-passwords-with-the-myapps-portal) section of this article.</span></span> 


## <a name="manage-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="a449f-146">Gérer les mots de passe d’application Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="a449f-146">Manage app passwords in hello Azure portal</span></span>
<span data-ttu-id="a449f-147">Si vous utilisez la vérification en deux étapes avec Azure, vous souhaitez que les mots de passe application toocreate via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a449f-147">If you use two-step verification with Azure, you want toocreate app passwords through hello Azure portal.</span></span>

### <a name="toocreate-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="a449f-148">mots de passe toocreate application Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="a449f-148">toocreate app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="a449f-149">Se connecter toohello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="a449f-149">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="a449f-150">En haut de hello, avec le bouton droit de votre nom d’utilisateur, puis sélectionnez Vérification de sécurité supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="a449f-150">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="a449f-151">Sur la page Vérification hello, en haut hello, sélectionnez les mots de passe d’application</span><span class="sxs-lookup"><span data-stu-id="a449f-151">On hello proofup page, at hello top, select app passwords</span></span>
4. <span data-ttu-id="a449f-152">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="a449f-152">Click **Create**.</span></span>
5. <span data-ttu-id="a449f-153">Entrez un nom pour le mot de passe hello et cliquez sur **suivant**</span><span class="sxs-lookup"><span data-stu-id="a449f-153">Enter a name for hello app password and click **Next**</span></span>
6. <span data-ttu-id="a449f-154">Copier le Presse-papiers toohello du mot de passe d’application hello et collez-le dans votre application.</span><span class="sxs-lookup"><span data-stu-id="a449f-154">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   
   ![Cloud](./media/multi-factor-authentication-end-user-app-passwords/app2.png)


### <a name="toodelete-app-passwords-in-hello-azure-portal"></a><span data-ttu-id="a449f-156">mots de passe toodelete application Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="a449f-156">toodelete app passwords in hello Azure portal</span></span>
1. <span data-ttu-id="a449f-157">Se connecter toohello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="a449f-157">Sign in toohello Azure classic portal.</span></span>
2. <span data-ttu-id="a449f-158">En haut de hello, avec le bouton droit de votre nom d’utilisateur, puis sélectionnez Vérification de sécurité supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="a449f-158">At hello top, right-click your user name and select Additional Security Verification.</span></span>
3. <span data-ttu-id="a449f-159">En haut hello, une vérification de sécurité tooadditional suivante, sélectionnez **mots de passe d’application.**</span><span class="sxs-lookup"><span data-stu-id="a449f-159">At hello top, next tooadditional security verification, select **app passwords.**</span></span>
4. <span data-ttu-id="a449f-160">Suivant toohello application un mot de passe toodelete, sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="a449f-160">Next toohello app password you want toodelete, select **Delete**.</span></span>
5. <span data-ttu-id="a449f-161">Confirmez la suppression de hello en cliquant sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="a449f-161">Confirm hello deletion by clicking **yes**.</span></span>
6. <span data-ttu-id="a449f-162">Une fois que le mot de passe hello est supprimé, vous pouvez cliquer sur **fermer**.</span><span class="sxs-lookup"><span data-stu-id="a449f-162">Once hello app password is deleted, you can click **close**.</span></span>


## <a name="manage-app-passwords-with-hello-myapps-portal"></a><span data-ttu-id="a449f-163">Gérer les mots de passe d’application avec le portail de MyApps hello.</span><span class="sxs-lookup"><span data-stu-id="a449f-163">Manage app passwords with hello MyApps portal.</span></span>
<span data-ttu-id="a449f-164">Si vous n’êtes pas sûr de la façon dont vous utilisez l’authentification multifacteur, vous pouvez toujours créer et supprimer des mots de passe d’application via le portail de myapps hello.</span><span class="sxs-lookup"><span data-stu-id="a449f-164">If you are not sure how you use multi-factor authentication, then you can always create and delete app passwords through hello myapps portal.</span></span>

### <a name="toocreate-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="a449f-165">un mot de passe d’application à l’aide de toocreate hello Myapps portail</span><span class="sxs-lookup"><span data-stu-id="a449f-165">toocreate an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="a449f-166">Connectez-vous trop[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="a449f-166">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="a449f-167">Cliquez sur votre nom en haut de hello à droite, puis choisissez **profil**.</span><span class="sxs-lookup"><span data-stu-id="a449f-167">Click your name at hello top right, and choose **Profile**.</span></span>
3. <span data-ttu-id="a449f-168">Sélectionnez **Vérification de sécurité supplémentaire**.</span><span class="sxs-lookup"><span data-stu-id="a449f-168">Select **Additional Security Verification**.</span></span>
   <span data-ttu-id="a449f-169">![Capture d’écran : Vérification de sécurité supplémentaire](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span><span class="sxs-lookup"><span data-stu-id="a449f-169">![Select additional security verification - screenshot](./media/multi-factor-authentication-end-user-manage/myapps1.png)</span></span>

4. <span data-ttu-id="a449f-170">Sélectionnez **Mots de passe d’application**.</span><span class="sxs-lookup"><span data-stu-id="a449f-170">Select **app passwords**.</span></span>
   <span data-ttu-id="a449f-171">![Capture d’écran : sélection de Mots de passe d’application](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span><span class="sxs-lookup"><span data-stu-id="a449f-171">![Select app passwords - screenshot](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)</span></span>

5. <span data-ttu-id="a449f-172">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="a449f-172">Click **Create**.</span></span>
6. <span data-ttu-id="a449f-173">Entrez un nom pour le mot de passe hello et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="a449f-173">Enter a name for hello app password and click **Next**.</span></span>
7. <span data-ttu-id="a449f-174">Copier le Presse-papiers toohello du mot de passe d’application hello et collez-le dans votre application.</span><span class="sxs-lookup"><span data-stu-id="a449f-174">Copy hello app password toohello clipboard and paste it into your app.</span></span>
   <span data-ttu-id="a449f-175">![Créer un mot de passe d’application](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span><span class="sxs-lookup"><span data-stu-id="a449f-175">![Create an app password](./media/multi-factor-authentication-end-user-app-passwords/create2.png)</span></span>

### <a name="toodelete-an-app-password-using-hello-myapps-portal"></a><span data-ttu-id="a449f-176">un mot de passe d’application à l’aide de toodelete hello Myapps portail</span><span class="sxs-lookup"><span data-stu-id="a449f-176">toodelete an app password using hello Myapps portal</span></span>
1. <span data-ttu-id="a449f-177">Connectez-vous trop[https://myapps.microsoft.com](https://myapps.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="a449f-177">Sign in too[https://myapps.microsoft.com](https://myapps.microsoft.com)</span></span>
2. <span data-ttu-id="a449f-178">En haut de hello, sélectionnez le profil.</span><span class="sxs-lookup"><span data-stu-id="a449f-178">At hello top, select profile.</span></span>
3. <span data-ttu-id="a449f-179">Sélectionnez **Vérification de sécurité supplémentaire**.</span><span class="sxs-lookup"><span data-stu-id="a449f-179">Select **Additional Security Verification**.</span></span>

   ![Capture d’écran : Vérification de sécurité supplémentaire](./media/multi-factor-authentication-end-user-manage/myapps1.png)

4. <span data-ttu-id="a449f-181">Sélectionnez **Mots de passe d’application**.</span><span class="sxs-lookup"><span data-stu-id="a449f-181">Select **app passwords**.</span></span>

   ![Capture d’écran : sélection de Mots de passe d’application](./media/multi-factor-authentication-end-user-app-passwords/apppass2.png)

5. <span data-ttu-id="a449f-183">Suivant toohello application un mot de passe toodelete, cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="a449f-183">Next toohello app password you want toodelete, click **Delete**.</span></span>

   ![Supprimer un mot de passe d’application](./media/multi-factor-authentication-end-user-app-passwords/delete1.png)

6. <span data-ttu-id="a449f-185">Confirmer que vous souhaitez toodelete ce mot de passe en cliquant sur **Oui**.</span><span class="sxs-lookup"><span data-stu-id="a449f-185">Confirm that you want toodelete that password by clicking **yes**.</span></span>
7. <span data-ttu-id="a449f-186">Une fois que le mot de passe hello est supprimé, vous pouvez cliquer sur **fermer**.</span><span class="sxs-lookup"><span data-stu-id="a449f-186">Once hello app password is deleted, you can click **close**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a449f-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a449f-187">Next steps</span></span>

- [<span data-ttu-id="a449f-188">Gérer les paramètres de la vérification en deux étapes</span><span class="sxs-lookup"><span data-stu-id="a449f-188">Manage your two-step verification settings</span></span>](multi-factor-authentication-end-user-manage-settings.md)

- <span data-ttu-id="a449f-189">Essayer hello [application Authenticator de Microsoft](microsoft-authenticator-app-how-to.md) tooverify vos connexions avec les notifications de l’application, au lieu de recevoir des appels ou textes.</span><span class="sxs-lookup"><span data-stu-id="a449f-189">Try out hello [Microsoft Authenticator app](microsoft-authenticator-app-how-to.md) tooverify your sign-ins with app notifications, instead of receiving texts or calls.</span></span> 