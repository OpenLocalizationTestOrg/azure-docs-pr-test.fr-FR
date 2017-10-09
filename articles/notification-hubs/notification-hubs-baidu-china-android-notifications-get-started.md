---
title: "aaaGet main à l’aide de Baidu Azure Notification Hubs | Documents Microsoft"
description: "Dans ce didacticiel, vous apprendrez comment appareils tooAndroid toouse Azure Notification Hubs toopush des notifications à l’aide de Baidu."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a><span data-ttu-id="6c2f6-103">Prendre en main Notification Hubs à l’aide de Baidu</span><span class="sxs-lookup"><span data-stu-id="6c2f6-103">Get started with Notification Hubs using Baidu</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="6c2f6-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6c2f6-104">Overview</span></span>
<span data-ttu-id="6c2f6-105">Push de cloud Baidu est un service de cloud chinois que vous pouvez utiliser des périphériques de toomobile toosend push notifications.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-105">Baidu cloud push is a Chinese cloud service that you can use toosend push notifications toomobile devices.</span></span> <span data-ttu-id="6c2f6-106">Ce service est utile en Chine, où remettre des notifications push tooAndroid est complexe en raison de la présence de hello de magasins d’applications différents et par émission de données des services, en outre disponibilité toohello des appareils Android qui ne sont pas généralement connecté tooGCM (Google Le cloud de messagerie).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-106">This service is useful in China, where delivering push notifications tooAndroid is complex because of hello presence of different app stores and push services, in addition toohello availability of Android devices that are not typically connected tooGCM (Google Cloud Messaging).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c2f6-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="6c2f6-107">Prerequisites</span></span>
<span data-ttu-id="6c2f6-108">Ce didacticiel requiert les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="6c2f6-108">This tutorial requires:</span></span>

* <span data-ttu-id="6c2f6-109">SDK Android (nous supposons que vous utilisez Eclipse), que vous pouvez télécharger à partir de hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">site Android</a></span><span class="sxs-lookup"><span data-stu-id="6c2f6-109">Android SDK (we assume that you use Eclipse), which you can download from hello <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a></span></span>
* <span data-ttu-id="6c2f6-110">[Kit de développement logiciel (SDK) Mobile Services pour Android]</span><span class="sxs-lookup"><span data-stu-id="6c2f6-110">[Mobile Services Android SDK]</span></span>
* <span data-ttu-id="6c2f6-111">[Push Baidu Android SDK]</span><span class="sxs-lookup"><span data-stu-id="6c2f6-111">[Baidu Push Android SDK]</span></span>

> [!NOTE]
> <span data-ttu-id="6c2f6-112">toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-112">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="6c2f6-113">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6c2f6-114">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span></span>
> 
> 

## <a name="create-a-baidu-account"></a><span data-ttu-id="6c2f6-115">Création d’un compte Baidu</span><span class="sxs-lookup"><span data-stu-id="6c2f6-115">Create a Baidu account</span></span>
<span data-ttu-id="6c2f6-116">toouse Baidu, vous devez disposer d’un compte Baidu.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-116">toouse Baidu, you must have a Baidu account.</span></span> <span data-ttu-id="6c2f6-117">Si vous avez déjà un, ouvrez une session dans toohello [Baidu portail] et ignorer l’étape suivante de toohello.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-117">If you already have one, log in toohello [Baidu portal] and skip toohello next step.</span></span> <span data-ttu-id="6c2f6-118">Dans le cas contraire, consultez hello suivant les instructions sur la façon de toocreate un compte Baidu.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-118">Otherwise, see hello following instructions on how toocreate a Baidu account.</span></span>  

1. <span data-ttu-id="6c2f6-119">Accédez toohello [Baidu portail] et cliquez sur hello**登录**(**connexion**) lien.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-119">Go toohello [Baidu portal] and click hello **登录** (**Login**) link.</span></span> <span data-ttu-id="6c2f6-120">Cliquez sur**立即注册**toostart processus d’inscription hello.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-120">Click **立即注册** toostart hello account registration process.</span></span>
   
   ![][1]
2. <span data-ttu-id="6c2f6-121">Entrez les détails de hello requis : code adresse, un mot de passe et la vérification de téléphone/messagerie, puis cliquez sur **inscription**.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-121">Enter hello required details—phone/email address, password, and verification code—and click **Signup**.</span></span>
   
   ![][2]
3. <span data-ttu-id="6c2f6-122">Vous recevrez une adresse de messagerie toohello par courrier électronique que vous avez entré avec un tooactivate lien votre compte Baidu.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-122">You will be sent an email toohello email address that you entered with a link tooactivate your Baidu account.</span></span>
   
   ![][3]
4. <span data-ttu-id="6c2f6-123">Connectez-vous au compte de messagerie tooyour, ouvrir la messagerie de l’activation de Baidu hello, cliquez sur tooactivate de lien d’activation hello votre compte Baidu.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-123">Log in tooyour email account, open hello Baidu activation mail, and click hello activation link tooactivate your Baidu account.</span></span>
   
   ![][4]

<span data-ttu-id="6c2f6-124">Une fois que vous avez un compte Baidu activé, connectez-vous à toohello [Baidu portail].</span><span class="sxs-lookup"><span data-stu-id="6c2f6-124">Once you have an activated Baidu account, log in toohello [Baidu portal].</span></span>

## <a name="register-as-a-baidu-developer"></a><span data-ttu-id="6c2f6-125">Inscription en tant que développeur Baidu</span><span class="sxs-lookup"><span data-stu-id="6c2f6-125">Register as a Baidu developer</span></span>
1. <span data-ttu-id="6c2f6-126">Une fois que vous avez ouvert une session dans toohello [Baidu portail], cliquez sur**更多 >>** (**plus**).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-126">Once you have logged in toohello [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="6c2f6-127">Faites défiler hello**站长与开发者服务 (administrateur Web et Services de développement)** et cliquez sur**百度开放云平台**(**Baidu ouvrir plateforme cloud**).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-127">Scroll down in hello **站长与开发者服务 (Webmaster and Developer Services)** section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="6c2f6-128">Dans la page suivante de hello, cliquez sur**开发者服务**(**Services de développement**) dans l’angle supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-128">On hello next page, click **开发者服务** (**Developer Services**) on hello top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="6c2f6-129">Dans la page suivante de hello, cliquez sur**注册开发者**(**inscrit les développeurs**) à partir du menu hello dans l’angle supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-129">On hello next page, click **注册开发者** (**Registered Developers**) from hello menu on hello top-right corner.</span></span>
   
      ![][8]
5. <span data-ttu-id="6c2f6-130">Entrez votre nom, une description et un numéro de téléphone portable pour la réception d’un message texte de vérification, puis cliquez sur **送验证码** (**Envoyer un code de vérification**).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-130">Enter your name, a description, and a mobile phone number for receiving a verification text message, and then click **送验证码** (**Send Verification Code**).</span></span> <span data-ttu-id="6c2f6-131">Pour les numéros de téléphone international, vous devez tooenclose indicatif du pays hello entre parenthèses.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-131">For international phone numbers, you need tooenclose hello country code in parentheses.</span></span> <span data-ttu-id="6c2f6-132">Voici un exemple de numéro en France : **(33)123456789**.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-132">For example, for a United States number, it is **(1)1234567890**.</span></span>
   
      ![][9]
6. <span data-ttu-id="6c2f6-133">Vous recevrez ensuite un message texte avec un code de vérification, comme indiqué dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6c2f6-133">You should then receive a text message with a verification number, as shown in hello following example:</span></span>
   
      ![][10]
7. <span data-ttu-id="6c2f6-134">Entrez le numéro de vérification hello à partir du message de type hello dans**验证码**(**code de Confirmation**).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-134">Enter hello verification number from hello message in **验证码** (**Confirmation code**).</span></span>
8. <span data-ttu-id="6c2f6-135">Pour finir, terminez l’inscription de développeur hello en cliquant sur Accepter hello Baidu contrat**提交**(**Submit**).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-135">Finally, complete hello developer registration by accepting hello Baidu agreement and clicking **提交** (**Submit**).</span></span> <span data-ttu-id="6c2f6-136">Vous verrez hello suivant page sur la réussite de l’inscription :</span><span class="sxs-lookup"><span data-stu-id="6c2f6-136">You will see hello following page on successful completion of registration:</span></span>
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a><span data-ttu-id="6c2f6-137">Créer un projet Baidu de transmission Push dans le cloud</span><span class="sxs-lookup"><span data-stu-id="6c2f6-137">Create a Baidu cloud push project</span></span>
<span data-ttu-id="6c2f6-138">Quand vous créez un projet Baidu de transmission Push dans le cloud, vous recevez un ID d’application, une clé API et une clé secrète.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-138">When you create a Baidu cloud push project, you receive your app ID, API key, and secret key.</span></span>

1. <span data-ttu-id="6c2f6-139">Une fois que vous avez ouvert une session dans toohello [Baidu portail], cliquez sur**更多 >>** (**plus**).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-139">Once you have logged in toohello [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="6c2f6-140">Faites défiler hello**站长与开发者服务**(**administrateur Web et des Services de développement**) et cliquez sur**百度开放云平台**(**Baidu ouvrir plateforme cloud**).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-140">Scroll down in hello **站长与开发者服务** (**Webmaster and Developer Services**) section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="6c2f6-141">Dans la page suivante de hello, cliquez sur**开发者服务**(**Services de développement**) dans l’angle supérieur droit de hello.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-141">On hello next page, click **开发者服务** (**Developer Services**) on hello top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="6c2f6-142">Dans la page suivante de hello, cliquez sur**云推送**(**Cloud Push**) à partir de hello**云服务**(**Services de cloud computing**) section.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-142">On hello next page, click **云推送** (**Cloud Push**) from hello **云服务** (**Cloud Services**) section.</span></span>
   
      ![][12]
5. <span data-ttu-id="6c2f6-143">Une fois que vous êtes un développeur inscrit, vous voyez**管理控制台**(**Console de gestion**) au menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-143">Once you are a registered developer, you see **管理控制台** (**Management Console**) at hello top menu.</span></span> <span data-ttu-id="6c2f6-144">Cliquez sur **开发者服务管理** (**Gestion des services des développeurs**).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-144">Click **开发者服务管理** (**Developers Service Management**).</span></span>
   
      ![][13]
6. <span data-ttu-id="6c2f6-145">Dans la page suivante de hello, cliquez sur**创建工程**(**créer un projet**).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-145">On hello next page, click **创建工程** (**Create Project**).</span></span>
   
      ![][14]
7. <span data-ttu-id="6c2f6-146">Entrez un nom d’application et cliquez sur **创建** (**Créer**).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-146">Enter an application name and click **创建** (**Create**).</span></span>
   
      ![][15]
8. <span data-ttu-id="6c2f6-147">Une fois qu’un projet push cloud Baidu a été créé, vous voyez apparaître une page présentant **l’ID d’application**, la **clé API** et la **clé secrète**.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-147">Upon successful creation of a Baidu cloud push project, you see a page with **AppID**, **API Key**, and **Secret Key**.</span></span> <span data-ttu-id="6c2f6-148">Prenez note de la clé d’API hello et une clé secrète, que nous utiliserons plus tard.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-148">Make a note of hello API key and secret key, which we will use later.</span></span>
   
      ![][16]
9. <span data-ttu-id="6c2f6-149">Configurez le projet hello pour les notifications push en cliquant sur**云推送**(**Cloud Push**) dans le volet gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-149">Configure hello project for push notifications by clicking **云推送** (**Cloud Push**) on hello left pane.</span></span>
   
      ![][31]
10. <span data-ttu-id="6c2f6-150">Sur la page suivante de hello, cliquez sur hello**推送设置**(**Push paramètres**) bouton.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-150">On hello next page, click hello **推送设置** (**Push settings**) button.</span></span>
    
    ![][32]  
11. <span data-ttu-id="6c2f6-151">Sur la page de configuration hello, ajouter le nom du package hello que vous utiliserez dans votre projet Android dans hello**应用包名**(**package d’Application**) champ, puis cliquez sur**保存设置**() **Enregistrer**).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-151">On hello configuration page, add hello package name that you will be using in your Android project in hello **应用包名** (**Application package**) field, and then click **保存设置** (**Save**).</span></span>  
    
    ![][33]

<span data-ttu-id="6c2f6-152">Vous consultez hello**保存成功 !** (**Enregistrement réussi !**).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-152">You see hello **保存成功！** (**Successfully saved!**) message.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="6c2f6-153">Configuration de votre hub de notification</span><span class="sxs-lookup"><span data-stu-id="6c2f6-153">Configure your notification hub</span></span>
1. <span data-ttu-id="6c2f6-154">Connectez-vous à toohello [portail classique Azure], puis cliquez sur **+ nouveau** bas hello écran hello.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-154">Sign in toohello [Azure Classic Portal], and then click **+NEW** at hello bottom of hello screen.</span></span>
2. <span data-ttu-id="6c2f6-155">Cliquez sur **Services d’application**, sur **Service Bus**, sur **Hub de notification**, puis cliquez sur **Création rapide**.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-155">Click **App Services**, click **Service Bus**, click **Notification Hub**, and then click **Quick Create**.</span></span>
3. <span data-ttu-id="6c2f6-156">Fournissez un nom pour votre **Hub de Notification**, sélectionnez hello **région** et hello **Namespace** où ce hub de notification est créé, puis cliquez sur  **Créer un Hub de Notification**.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-156">Provide a name for your **Notification Hub**, select hello **Region** and hello **Namespace** where this notification hub will be created, and then click **Create a New Notification Hub**.</span></span>  
   
      ![][17]
4. <span data-ttu-id="6c2f6-157">Espace de noms hello dans lequel vous avez créé votre hub de notification, puis **concentrateurs de Notification** haut hello.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-157">Click hello namespace in which you created your notification hub, and then click **Notification Hubs** at hello top.</span></span>
   
      ![][18]
5. <span data-ttu-id="6c2f6-158">Concentrateur de notification Sélectionnez hello créé, puis cliquez sur **configurer** à partir du menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-158">Select hello notification hub that you created, and then click **Configure** from hello top menu.</span></span>
   
      ![][19]
6. <span data-ttu-id="6c2f6-159">Faites défiler vers le bas toohello **les paramètres de notification baidu** section et entrez la clé d’API de hello et une clé secrète que vous avez obtenue à partir de la console de Baidu hello précédemment pour votre projet Baidu cloud push.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-159">Scroll down toohello **baidu notification settings** section and enter hello API key and secret key that you obtained from hello Baidu console previously for your Baidu cloud push project.</span></span> <span data-ttu-id="6c2f6-160">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-160">Click **Save**.</span></span>
   
      ![][20]
7. <span data-ttu-id="6c2f6-161">Cliquez sur hello **tableau de bord** onglet en haut de hello hello hub de notification, puis cliquez sur **afficher la chaîne de connexion**.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-161">Click hello **Dashboard** tab at hello top for hello notification hub, and then click **View Connection String**.</span></span>
   
      ![][21]
8. <span data-ttu-id="6c2f6-162">Prenez note de hello **DefaultListenSharedAccessSignature** et **DefaultFullSharedAccessSignature** de hello **d’accéder aux informations de connexion** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-162">Make a note of hello **DefaultListenSharedAccessSignature** and **DefaultFullSharedAccessSignature** from hello **Access connection information** window.</span></span>
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="6c2f6-163">Se connecter à votre hub de notification d’application toohello</span><span class="sxs-lookup"><span data-stu-id="6c2f6-163">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="6c2f6-164">Dans Eclipse ADT, créez un projet Android (**File** > **New** > **Android Application Project**).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-164">In Eclipse ADT, create a new Android project (**File** > **New** > **Android Application Project**).</span></span>
   
    ![][23]
2. <span data-ttu-id="6c2f6-165">Entrez un **nom de l’Application** et assurez-vous que hello **Minimum nécessaire le Kit de développement** version est définie trop**API 16 : Android 4.1**.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-165">Enter an **Application Name** and ensure that hello **Minimum Required SDK** version is set too**API 16: Android 4.1**.</span></span>
   
    ![][24]
3. <span data-ttu-id="6c2f6-166">Cliquez sur **suivant** et continuer après l’Assistant de hello jusqu'à hello **créer une activité** fenêtre s’affiche.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-166">Click **Next** and continue following hello wizard until hello **Create Activity** window appears.</span></span> <span data-ttu-id="6c2f6-167">Assurez-vous que **activité vide** est sélectionné et enfin sélectionnez **Terminer** toocreate une Application Android.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-167">Make sure that **Blank Activity** is selected, and finally select **Finish** toocreate a new Android Application.</span></span>
   
    ![][25]
4. <span data-ttu-id="6c2f6-168">Vérifiez que hello **cible de Build de projet** est défini correctement.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-168">Make sure that hello **Project Build Target** is set correctly.</span></span>
   
    ![][26]
5. <span data-ttu-id="6c2f6-169">Téléchargez hello concentrateurs-notification-0.4.jar fichier hello **fichiers** onglet Hello [Notification-Hubs-Android-SDK sur Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-169">Download hello notification-hubs-0.4.jar file from hello **Files** tab of hello [Notification-Hubs-Android-SDK on Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span></span> <span data-ttu-id="6c2f6-170">Ajouter hello fichier toohello **libs** dossier de votre projet Eclipse et actualisation hello *libs* dossier.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-170">Add hello file toohello **libs** folder of your Eclipse project, and refresh hello *libs* folder.</span></span>
6. <span data-ttu-id="6c2f6-171">Téléchargez et décompressez hello [Push Baidu Android SDK], ouvrez hello **libs** dossier, puis hello de copie **pushservice-x.y.z** jar de fichiers et de hello **armeabi**  &  **mips** dossiers Bonjour **libs** dossier de votre application Android.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-171">Download and unzip hello [Baidu Push Android SDK], open hello **libs** folder, and then copy hello **pushservice-x.y.z** jar file and hello **armeabi** & **mips** folders in hello **libs** folder of your Android application.</span></span>
7. <span data-ttu-id="6c2f6-172">Ouvrez hello **AndroidManifest.xml** fichier de votre Android de projet et ajouter des autorisations hello requis par hello Baidu SDK.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-172">Open hello **AndroidManifest.xml** file of your Android project and add hello permissions that are required by hello Baidu SDK.</span></span>
   
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
8. <span data-ttu-id="6c2f6-173">Ajouter hello **android : name** propriété tooyour **application** élément **AndroidManifest.xml**, en remplaçant *votre_nom_de_projet* (pour exemple, **com.example.BaiduTest**).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-173">Add hello **android:name** property tooyour **application** element in **AndroidManifest.xml**, replacing *yourprojectname* (for example, **com.example.BaiduTest**).</span></span> <span data-ttu-id="6c2f6-174">Assurez-vous que ce nom de projet correspond à hello une que vous avez configuré dans la console hello Baidu.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-174">Make sure that this project name matches hello one that you configured in hello Baidu console.</span></span>
   
        <application android:name="yourprojectname.DemoApplication"
9. <span data-ttu-id="6c2f6-175">Ajouter hello configuration au sein de l’élément de l’application hello après hello suivante **. MainActivity** élément d’activité, en remplaçant *votre_nom_de_projet* (par exemple, **com.example.BaiduTest**) :</span><span class="sxs-lookup"><span data-stu-id="6c2f6-175">Add hello following configuration within hello application element after hello **.MainActivity** activity element, replacing *yourprojectname* (for example, **com.example.BaiduTest**):</span></span>
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. <span data-ttu-id="6c2f6-176">Ajouter une nouvelle classe nommée **ConfigurationSettings.java** toohello projet.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-176">Add a new class called **ConfigurationSettings.java** toohello project.</span></span>
    
     ![][28]
    
     ![][29]
11. <span data-ttu-id="6c2f6-177">Ajoutez hello suivant tooit de code :</span><span class="sxs-lookup"><span data-stu-id="6c2f6-177">Add hello following code tooit:</span></span>
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    <span data-ttu-id="6c2f6-178">Valeur hello **API_KEY** avec ce que vous avez récupérés sous projet hello Baidu cloud précédemment, **NotificationHubName** avec votre nom de hub de notification à partir de hello portail classique Azure et  **NotificationHubConnectionString** avec DefaultListenSharedAccessSignature de hello portail classique Azure.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-178">Set hello value of **API_KEY** with what you retrieved from hello Baidu cloud project earlier, **NotificationHubName** with your notification hub name from hello Azure Classic Portal and **NotificationHubConnectionString** with DefaultListenSharedAccessSignature from hello Azure Classic Portal.</span></span>
12. <span data-ttu-id="6c2f6-179">Ajouter une nouvelle classe nommée **DemoApplication.java**et ajoutez hello suivant tooit de code :</span><span class="sxs-lookup"><span data-stu-id="6c2f6-179">Add a new class called **DemoApplication.java**, and add hello following code tooit:</span></span>
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. <span data-ttu-id="6c2f6-180">Ajoutez une autre classe nommée **MyPushMessageReceiver.java**et ajoutez hello suivant tooit de code.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-180">Add another new class called **MyPushMessageReceiver.java**, and add hello following code tooit.</span></span> <span data-ttu-id="6c2f6-181">Il est la classe hello handles hello des notifications push reçus à partir du serveur de push Baidu hello.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-181">It is hello class that handles hello push notifications that are received from hello Baidu push server.</span></span>
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
                try {
                    if (hub == null) {
                        hub = new NotificationHub(
                                ConfigurationSettings.NotificationHubName,
                                ConfigurationSettings.NotificationHubConnectionString,
                                context);
                        Log.i(TAG, "Notification hub initialized");
                    }
                } catch (Exception e) {
                   Log.e(TAG, e.getMessage());
                }
    
                registerWithNotificationHubs();
            }
    
            private void registerWithNotificationHubs() {
               new AsyncTask<Void, Void, Void>() {
                  @Override
                  protected Void doInBackground(Void... params) {
                     try {
                         hub.registerBaidu(mUserId, mChannelId);
                         Log.i(TAG, "Registered with Notification Hub - '"
                                 + ConfigurationSettings.NotificationHubName + "'"
                                 + " with UserId - '"
                                 + mUserId + "' and Channel Id - '"
                                 + mChannelId + "'");
                     } catch (Exception e) {
                         Log.e(TAG, e.getMessage());
                     }
                     return null;
                 }
               }.execute(null, null, null);
            }
    
            @Override
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onListTags(Context context, int errorCode, List<String> tags,
                    String requestId) {
                String responseString = "onListTags errorCode=" + errorCode + " tags="
                        + tags;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onUnbind(Context context, int errorCode, String requestId) {
                String responseString = "onUnbind errorCode=" + errorCode
                        + " requestId = " + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. <span data-ttu-id="6c2f6-182">Ouvrez **MainActivity.java**et ajoutez hello suivant toohello **onCreate** méthode :</span><span class="sxs-lookup"><span data-stu-id="6c2f6-182">Open **MainActivity.java**, and add hello following toohello **onCreate** method:</span></span>
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. <span data-ttu-id="6c2f6-183">Ouvrez hello suivant les instructions d’importation haut hello :</span><span class="sxs-lookup"><span data-stu-id="6c2f6-183">Open hello following import statements at hello top:</span></span>
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a><span data-ttu-id="6c2f6-184">Envoyer des notifications tooyour application</span><span class="sxs-lookup"><span data-stu-id="6c2f6-184">Send notifications tooyour app</span></span>
<span data-ttu-id="6c2f6-185">Vous pouvez tester rapidement la réception de notifications dans votre application en envoyant des notifications Bonjour [portail Azure](https://portal.azure.com/) à l’aide de hello **envoyer** bouton sur le concentrateur de notification hello, comme indiqué dans hello suivant d’écran :</span><span class="sxs-lookup"><span data-stu-id="6c2f6-185">You can quickly test receiving notifications in your app by sending notifications in hello [Azure portal](https://portal.azure.com/) using hello **Send** button on hello notification hub, as shown in hello following screen:</span></span>

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

<span data-ttu-id="6c2f6-186">Les notifications Push sont normalement envoyées dans un service principal tel que Mobile Services ou ASP.NET à l’aide d’une bibliothèque compatible.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-186">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="6c2f6-187">Si une bibliothèque n’est pas disponible pour votre serveur principal, vous pouvez utiliser les API REST de hello toosend directement les messages de notification.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-187">If a library is not available for your back-end, you can use hello REST API directly toosend notification messages .</span></span>

<span data-ttu-id="6c2f6-188">Dans ce didacticiel, nous plus de simplicité et simplement montrent le test de votre application cliente en envoyant des notifications à l’aide de hello SDK .NET pour les concentrateurs de notification dans une application console à la place d’un service principal.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-188">In this tutorial, we keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="6c2f6-189">Nous vous recommandons de hello [utiliser Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) didacticiel en tant qu’étape suivante de hello pour envoyer des notifications à partir d’un serveur principal d’ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-189">We recommend hello [Use Notification Hubs toopush notifications toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="6c2f6-190">Toutefois, hello méthodes suivantes peut servir pour envoyer des notifications :</span><span class="sxs-lookup"><span data-stu-id="6c2f6-190">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="6c2f6-191">**Interface REST**: peut prendre en charge notification sur toute plateforme principale à l’aide de hello [interface REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-191">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="6c2f6-192">**Kit de développement logiciel Microsoft Azure Notification Hubs .NET**: Bonjour Gestionnaire de Package Nuget pour Visual Studio, exécutez [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-192">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="6c2f6-193">**Node.js**: [comment toouse concentrateurs de Notification à partir de Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-193">**Node.js**: [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="6c2f6-194">**Applications mobiles**: pour obtenir un exemple de notifications toosend à partir d’un serveur principal Azure App Service Mobile Apps intégré avec Notification Hubs, consultez [ajouter push notifications tooyour application mobile](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-194">**Mobile Apps**: For an example of how toosend notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications tooyour mobile app](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="6c2f6-195">**Java / PHP**: pour obtenir un exemple de comment toosend des notifications à l’aide de hello API REST, consultez « Comment toouse concentrateurs de Notification à partir de Java/PHP » ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="6c2f6-195">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-net-console-app"></a><span data-ttu-id="6c2f6-196">(Facultatif) Envoi de notifications à partir d’une application de console .NET.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-196">(Optional) Send notifications from a .NET console app.</span></span>
<span data-ttu-id="6c2f6-197">Dans cette section, nous montrons comment envoyer une notification à l’aide d’une application console .NET.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-197">In this section, we show sending a notification using a .NET console app.</span></span>

1. <span data-ttu-id="6c2f6-198">Créez une application console Visual C# :</span><span class="sxs-lookup"><span data-stu-id="6c2f6-198">Create a new Visual C# console application:</span></span>
   
    ![][30]
2. <span data-ttu-id="6c2f6-199">Dans la fenêtre de Console du Gestionnaire de Package de hello, définissez hello **projet par défaut** tooyour nouveau projet d’application console et puis, dans la fenêtre de console hello, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6c2f6-199">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="6c2f6-200">Cette instruction ajoute une référence de toohello Azure Notification Hubs SDK à l’aide de hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">package NuGet de concentrateurs Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-200">This instruction adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. <span data-ttu-id="6c2f6-201">Les fichiers ouverts hello **Program.cs** et ajoutez hello qui suit à l’aide d’instruction :</span><span class="sxs-lookup"><span data-stu-id="6c2f6-201">Open hello file **Program.cs** and add hello following using statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="6c2f6-202">Dans votre `Program` de classe, ajoutez hello suivant de méthode et remplacer *DefaultFullSharedAccessSignatureSASConnectionString* et *NotificationHubName* avec les valeurs hello dont vous disposez.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-202">In your `Program` class, add hello following method and replace *DefaultFullSharedAccessSignatureSASConnectionString* and *NotificationHubName* with hello values that you have.</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. <span data-ttu-id="6c2f6-203">Ajouter hello suivant des lignes dans votre **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="6c2f6-203">Add hello following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a><span data-ttu-id="6c2f6-204">Test de l'application</span><span class="sxs-lookup"><span data-stu-id="6c2f6-204">Test your app</span></span>
<span data-ttu-id="6c2f6-205">tootest cette application avec un téléphone réelle, seulement se connecter hello ordinateur tooyour de téléphone à l’aide d’un câble USB.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-205">tootest this app with an actual phone, just connect hello phone tooyour computer by using a USB cable.</span></span> <span data-ttu-id="6c2f6-206">Cette action charge votre application sur un téléphone de hello attaché.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-206">This action loads your app onto hello attached phone.</span></span>

<span data-ttu-id="6c2f6-207">Cliquez sur cette application avec l’émulateur hello, hello Eclipse haut la barre d’outils de tootest **exécuter**, puis sélectionnez votre application : il démarre hello émulateur, chargement, et s’exécute hello application.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-207">tootest this app with hello emulator, on hello Eclipse top toolbar, click **Run**, and then select your app: it starts hello emulator, loads, and runs hello app.</span></span>

<span data-ttu-id="6c2f6-208">application Hello récupère hello 'userId' et 'channelId' hello services de notifications Push de Baidu et inscrit avec le hub de notification hello.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-208">hello app retrieves hello 'userId' and 'channelId' from hello Baidu Push notification service and registers with hello notification hub.</span></span>

<span data-ttu-id="6c2f6-209">toosend une notification de test, vous pouvez utiliser l’onglet débogage de hello Hello portail classique Azure.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-209">toosend a test notification, you can use hello debug tab of hello Azure Classic Portal.</span></span> <span data-ttu-id="6c2f6-210">Si vous avez créé d’application de console .NET hello pour Visual Studio, appuyez sur touche F5 de hello dans l’application de Visual Studio toorun hello.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-210">If you built hello .NET console application for Visual Studio, just press hello F5 key in Visual Studio toorun hello application.</span></span> <span data-ttu-id="6c2f6-211">application Hello envoie une notification qui s’affiche dans la zone de notification supérieur de hello de votre appareil ou l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="6c2f6-211">hello application sends a notification that appears in hello top notification area of your device or emulator.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
[Kit de développement logiciel (SDK) Mobile Services pour Android]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Push Baidu Android SDK]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[portail classique Azure]: https://manage.windowsazure.com/
[Baidu portail]: http://www.baidu.com/
