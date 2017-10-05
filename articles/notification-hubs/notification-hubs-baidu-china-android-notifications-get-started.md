---
title: "Prendre en main Azure Notification Hubs à l’aide de Baidu | Microsoft Docs"
description: "Dans ce didacticiel, vous découvrirez comment utiliser Azure Notification Hubs pour envoyer des notifications Push à un appareil Android à l’aide de Baidu."
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
ms.openlocfilehash: df3bbda15e1245b6068c2b8290d0c96856051f1f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a><span data-ttu-id="ef164-103">Prendre en main Notification Hubs à l’aide de Baidu</span><span class="sxs-lookup"><span data-stu-id="ef164-103">Get started with Notification Hubs using Baidu</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="ef164-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ef164-104">Overview</span></span>
<span data-ttu-id="ef164-105">Le service de transmission Push dans le cloud de Baidu est un service cloud chinois que vous pouvez utiliser pour envoyer des notifications Push à des appareils mobiles.</span><span class="sxs-lookup"><span data-stu-id="ef164-105">Baidu cloud push is a Chinese cloud service that you can use to send push notifications to mobile devices.</span></span> <span data-ttu-id="ef164-106">Ce service est utile en Chine, où la remise de notifications Push à Android est complexe en raison de la présence de différents magasins d’applications et de services de transmission de type push, outre la disponibilité d’appareils Android qui ne sont généralement pas connectés à Google Cloud Messaging (GCM).</span><span class="sxs-lookup"><span data-stu-id="ef164-106">This service is useful in China, where delivering push notifications to Android is complex because of the presence of different app stores and push services, in addition to the availability of Android devices that are not typically connected to GCM (Google Cloud Messaging).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef164-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ef164-107">Prerequisites</span></span>
<span data-ttu-id="ef164-108">Ce didacticiel requiert les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ef164-108">This tutorial requires:</span></span>

* <span data-ttu-id="ef164-109">Kit de développement logiciel Android SDK (nous supposons que vous utilisez Eclipse), que vous pouvez télécharger à partir du <a href="http://go.microsoft.com/fwlink/?LinkId=389797">site Android</a></span><span class="sxs-lookup"><span data-stu-id="ef164-109">Android SDK (we assume that you use Eclipse), which you can download from the <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android site</a></span></span>
* <span data-ttu-id="ef164-110">[Kit de développement logiciel (SDK) Mobile Services pour Android]</span><span class="sxs-lookup"><span data-stu-id="ef164-110">[Mobile Services Android SDK]</span></span>
* <span data-ttu-id="ef164-111">[Kit de développement logiciel (SDK) Android pour transmissions push Baidu]</span><span class="sxs-lookup"><span data-stu-id="ef164-111">[Baidu Push Android SDK]</span></span>

> [!NOTE]
> <span data-ttu-id="ef164-112">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="ef164-112">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="ef164-113">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="ef164-113">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ef164-114">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="ef164-114">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).</span></span>
> 
> 

## <a name="create-a-baidu-account"></a><span data-ttu-id="ef164-115">Création d’un compte Baidu</span><span class="sxs-lookup"><span data-stu-id="ef164-115">Create a Baidu account</span></span>
<span data-ttu-id="ef164-116">Pour utiliser Baidu, vous devez disposer d’un compte Baidu.</span><span class="sxs-lookup"><span data-stu-id="ef164-116">To use Baidu, you must have a Baidu account.</span></span> <span data-ttu-id="ef164-117">Si vous en avez déjà un, connectez-vous au [portail Baidu] et passez à l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="ef164-117">If you already have one, log in to the [Baidu portal] and skip to the next step.</span></span> <span data-ttu-id="ef164-118">Dans le cas contraire, consultez les instructions ci-après pour créer un compte Baidu.</span><span class="sxs-lookup"><span data-stu-id="ef164-118">Otherwise, see the following instructions on how to create a Baidu account.</span></span>  

1. <span data-ttu-id="ef164-119">Accédez au [portail Baidu] et cliquez sur le lien **登录** (**Connexion**).</span><span class="sxs-lookup"><span data-stu-id="ef164-119">Go to the [Baidu portal] and click the **登录** (**Login**) link.</span></span> <span data-ttu-id="ef164-120">Cliquez sur **立即注册** pour démarrer le processus d’inscription d’un compte.</span><span class="sxs-lookup"><span data-stu-id="ef164-120">Click **立即注册** to start the account registration process.</span></span>
   
   ![][1]
2. <span data-ttu-id="ef164-121">Entrez les informations requises (téléphone/adresse de messagerie, mot de passe et code de vérification), puis cliquez sur **Inscription**.</span><span class="sxs-lookup"><span data-stu-id="ef164-121">Enter the required details—phone/email address, password, and verification code—and click **Signup**.</span></span>
   
   ![][2]
3. <span data-ttu-id="ef164-122">Vous allez recevoir un courrier électronique à l’adresse e-mail que vous avez entrée avec un lien permettant d’activer votre compte Baidu.</span><span class="sxs-lookup"><span data-stu-id="ef164-122">You will be sent an email to the email address that you entered with a link to activate your Baidu account.</span></span>
   
   ![][3]
4. <span data-ttu-id="ef164-123">Connectez-vous à votre compte de messagerie, ouvrez le courrier électronique d’activation Baidu, puis cliquez sur le lien d’activation pour activer votre compte Baidu.</span><span class="sxs-lookup"><span data-stu-id="ef164-123">Log in to your email account, open the Baidu activation mail, and click the activation link to activate your Baidu account.</span></span>
   
   ![][4]

<span data-ttu-id="ef164-124">Une fois que vous possédez un compte Baidu activé, connectez-vous au [portail Baidu].</span><span class="sxs-lookup"><span data-stu-id="ef164-124">Once you have an activated Baidu account, log in to the [Baidu portal].</span></span>

## <a name="register-as-a-baidu-developer"></a><span data-ttu-id="ef164-125">Inscription en tant que développeur Baidu</span><span class="sxs-lookup"><span data-stu-id="ef164-125">Register as a Baidu developer</span></span>
1. <span data-ttu-id="ef164-126">Une fois que êtes connecté au [portail Baidu], cliquez sur **更多>>** (**plus**).</span><span class="sxs-lookup"><span data-stu-id="ef164-126">Once you have logged in to the [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="ef164-127">Faites défiler la section **站长与开发者服务 (Administrateur Web et Services de développement)** et cliquez sur **百度开放云平台** (**Plateforme cloud ouverte Baidu**).</span><span class="sxs-lookup"><span data-stu-id="ef164-127">Scroll down in the **站长与开发者服务 (Webmaster and Developer Services)** section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="ef164-128">Sur la page suivante, cliquez sur **开发者服务** (**Services de développement**) dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="ef164-128">On the next page, click **开发者服务** (**Developer Services**) on the top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="ef164-129">Sur la page suivante, cliquez sur **注册开发者** (**Développeurs inscrits**) dans le menu dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="ef164-129">On the next page, click **注册开发者** (**Registered Developers**) from the menu on the top-right corner.</span></span>
   
      ![][8]
5. <span data-ttu-id="ef164-130">Entrez votre nom, une description et un numéro de téléphone portable pour la réception d’un message texte de vérification, puis cliquez sur **送验证码** (**Envoyer un code de vérification**).</span><span class="sxs-lookup"><span data-stu-id="ef164-130">Enter your name, a description, and a mobile phone number for receiving a verification text message, and then click **送验证码** (**Send Verification Code**).</span></span> <span data-ttu-id="ef164-131">Pour les numéros de téléphone internationaux, vous devez placer l’indicatif téléphonique du pays entre parenthèses.</span><span class="sxs-lookup"><span data-stu-id="ef164-131">For international phone numbers, you need to enclose the country code in parentheses.</span></span> <span data-ttu-id="ef164-132">Voici un exemple de numéro en France : **(33)123456789**.</span><span class="sxs-lookup"><span data-stu-id="ef164-132">For example, for a United States number, it is **(1)1234567890**.</span></span>
   
      ![][9]
6. <span data-ttu-id="ef164-133">Vous recevrez ensuite un message texte comportant un numéro de vérification, comme illustré dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ef164-133">You should then receive a text message with a verification number, as shown in the following example:</span></span>
   
      ![][10]
7. <span data-ttu-id="ef164-134">Entrez le numéro de vérification à partir du message dans **验证码** (**Code de confirmation**).</span><span class="sxs-lookup"><span data-stu-id="ef164-134">Enter the verification number from the message in **验证码** (**Confirmation code**).</span></span>
8. <span data-ttu-id="ef164-135">Enfin, terminez l’inscription du développeur en acceptant le contrat Baidu et en cliquant sur **提交** (**Envoyer**).</span><span class="sxs-lookup"><span data-stu-id="ef164-135">Finally, complete the developer registration by accepting the Baidu agreement and clicking **提交** (**Submit**).</span></span> <span data-ttu-id="ef164-136">Une fois l’inscription effectuée, la page ci-après s’affiche :</span><span class="sxs-lookup"><span data-stu-id="ef164-136">You will see the following page on successful completion of registration:</span></span>
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a><span data-ttu-id="ef164-137">Créer un projet Baidu de transmission Push dans le cloud</span><span class="sxs-lookup"><span data-stu-id="ef164-137">Create a Baidu cloud push project</span></span>
<span data-ttu-id="ef164-138">Quand vous créez un projet Baidu de transmission Push dans le cloud, vous recevez un ID d’application, une clé API et une clé secrète.</span><span class="sxs-lookup"><span data-stu-id="ef164-138">When you create a Baidu cloud push project, you receive your app ID, API key, and secret key.</span></span>

1. <span data-ttu-id="ef164-139">Une fois que êtes connecté au [portail Baidu], cliquez sur **更多>>** (**plus**).</span><span class="sxs-lookup"><span data-stu-id="ef164-139">Once you have logged in to the [Baidu portal], click **更多>>** (**more**).</span></span>
   
      ![][5]
2. <span data-ttu-id="ef164-140">Faites défiler la section **站长与开发者服** (**Administrateur Web et Services de développement**) et cliquez sur **百度开放云平台** (**Plateforme cloud ouverte Baidu**).</span><span class="sxs-lookup"><span data-stu-id="ef164-140">Scroll down in the **站长与开发者服务** (**Webmaster and Developer Services**) section and click **百度开放云平台** (**Baidu open cloud platform**).</span></span>
   
      ![][6]
3. <span data-ttu-id="ef164-141">Sur la page suivante, cliquez sur **开发者服务** (**Services de développement**) dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="ef164-141">On the next page, click **开发者服务** (**Developer Services**) on the top-right corner.</span></span>
   
      ![][7]
4. <span data-ttu-id="ef164-142">Sur la page suivante, cliquez sur **云推送** (**Cloud Push**) à partir de la section **云服务** (**Services cloud**).</span><span class="sxs-lookup"><span data-stu-id="ef164-142">On the next page, click **云推送** (**Cloud Push**) from the **云服务** (**Cloud Services**) section.</span></span>
   
      ![][12]
5. <span data-ttu-id="ef164-143">Une fois que vous êtes un développeur enregistré, vous voyez **管理控制台** (**Console de gestion**) dans le menu supérieur.</span><span class="sxs-lookup"><span data-stu-id="ef164-143">Once you are a registered developer, you see **管理控制台** (**Management Console**) at the top menu.</span></span> <span data-ttu-id="ef164-144">Cliquez sur **开发者服务管理** (**Gestion des services des développeurs**).</span><span class="sxs-lookup"><span data-stu-id="ef164-144">Click **开发者服务管理** (**Developers Service Management**).</span></span>
   
      ![][13]
6. <span data-ttu-id="ef164-145">Sur la page suivante, cliquez sur **创建工程** (**Créer un projet**).</span><span class="sxs-lookup"><span data-stu-id="ef164-145">On the next page, click **创建工程** (**Create Project**).</span></span>
   
      ![][14]
7. <span data-ttu-id="ef164-146">Entrez un nom d’application et cliquez sur **创建** (**Créer**).</span><span class="sxs-lookup"><span data-stu-id="ef164-146">Enter an application name and click **创建** (**Create**).</span></span>
   
      ![][15]
8. <span data-ttu-id="ef164-147">Une fois qu’un projet push cloud Baidu a été créé, vous voyez apparaître une page présentant **l’ID d’application**, la **clé API** et la **clé secrète**.</span><span class="sxs-lookup"><span data-stu-id="ef164-147">Upon successful creation of a Baidu cloud push project, you see a page with **AppID**, **API Key**, and **Secret Key**.</span></span> <span data-ttu-id="ef164-148">Prenez note de la clé API et de la clé secrète que nous utiliserons ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="ef164-148">Make a note of the API key and secret key, which we will use later.</span></span>
   
      ![][16]
9. <span data-ttu-id="ef164-149">Configurez le projet pour les notifications push en cliquant sur **云推送** (**Cloud Push**) dans le volet gauche.</span><span class="sxs-lookup"><span data-stu-id="ef164-149">Configure the project for push notifications by clicking **云推送** (**Cloud Push**) on the left pane.</span></span>
   
      ![][31]
10. <span data-ttu-id="ef164-150">Sur la page suivante, cliquez sur le bouton **推送设置** (**Paramètres Push**).</span><span class="sxs-lookup"><span data-stu-id="ef164-150">On the next page, click the **推送设置** (**Push settings**) button.</span></span>
    
    ![][32]  
11. <span data-ttu-id="ef164-151">Sur la page de configuration, ajoutez le nom du package que vous utiliserez dans votre projet Android dans le champ **应用包名** (**Package d’application**), puis cliquez sur **保存设置** (**Enregistrer**).</span><span class="sxs-lookup"><span data-stu-id="ef164-151">On the configuration page, add the package name that you will be using in your Android project in the **应用包名** (**Application package**) field, and then click **保存设置** (**Save**).</span></span>  
    
    ![][33]

<span data-ttu-id="ef164-152">Vous voyez apparaître le message **保存成功！** (**Enregistrement réussi !**).</span><span class="sxs-lookup"><span data-stu-id="ef164-152">You see the **保存成功！** (**Successfully saved!**) message.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="ef164-153">Configuration de votre hub de notification</span><span class="sxs-lookup"><span data-stu-id="ef164-153">Configure your notification hub</span></span>
1. <span data-ttu-id="ef164-154">Connectez-vous au [Portail Azure Classic], puis cliquez sur **+NOUVEAU** en bas de l’écran.</span><span class="sxs-lookup"><span data-stu-id="ef164-154">Sign in to the [Azure Classic Portal], and then click **+NEW** at the bottom of the screen.</span></span>
2. <span data-ttu-id="ef164-155">Cliquez sur **Services d’application**, sur **Service Bus**, sur **Hub de notification**, puis cliquez sur **Création rapide**.</span><span class="sxs-lookup"><span data-stu-id="ef164-155">Click **App Services**, click **Service Bus**, click **Notification Hub**, and then click **Quick Create**.</span></span>
3. <span data-ttu-id="ef164-156">Fournissez un nom dans le champ **Hub de notification**, renseignez les champs **Région** et **Espace de noms** pour indiquer où ce hub de notification sera créé, puis cliquez sur **Créer un hub de notification**.</span><span class="sxs-lookup"><span data-stu-id="ef164-156">Provide a name for your **Notification Hub**, select the **Region** and the **Namespace** where this notification hub will be created, and then click **Create a New Notification Hub**.</span></span>  
   
      ![][17]
4. <span data-ttu-id="ef164-157">Cliquez sur l’espace de noms dans lequel vous avez créé votre hub de notification, puis cliquez sur **Notification Hubs** dans la partie supérieure.</span><span class="sxs-lookup"><span data-stu-id="ef164-157">Click the namespace in which you created your notification hub, and then click **Notification Hubs** at the top.</span></span>
   
      ![][18]
5. <span data-ttu-id="ef164-158">Sélectionnez le hub de notification que vous avez créé, puis cliquez sur **Configurer** dans le menu supérieur.</span><span class="sxs-lookup"><span data-stu-id="ef164-158">Select the notification hub that you created, and then click **Configure** from the top menu.</span></span>
   
      ![][19]
6. <span data-ttu-id="ef164-159">Faites défiler l’écran vers le bas jusqu’à la section **Paramètres de notification Baidu** et entrez la clé API et la clé secrète que vous avez obtenues précédemment à partir de la console Baidu pour votre projet Baidu de transmission push dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="ef164-159">Scroll down to the **baidu notification settings** section and enter the API key and secret key that you obtained from the Baidu console previously for your Baidu cloud push project.</span></span> <span data-ttu-id="ef164-160">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="ef164-160">Click **Save**.</span></span>
   
      ![][20]
7. <span data-ttu-id="ef164-161">Cliquez sur l’onglet **Tableau de bord** dans la partie supérieure du hub de notification, puis cliquez sur **Afficher la chaîne de connexion**.</span><span class="sxs-lookup"><span data-stu-id="ef164-161">Click the **Dashboard** tab at the top for the notification hub, and then click **View Connection String**.</span></span>
   
      ![][21]
8. <span data-ttu-id="ef164-162">Prenez note des valeurs **DefaultListenSharedAccessSignature** et **DefaultFullSharedAccessSignature** dans la fenêtre **Accès aux informations de connexion**.</span><span class="sxs-lookup"><span data-stu-id="ef164-162">Make a note of the **DefaultListenSharedAccessSignature** and **DefaultFullSharedAccessSignature** from the **Access connection information** window.</span></span>
   
    ![][22]

## <a name="connect-your-app-to-the-notification-hub"></a><span data-ttu-id="ef164-163">Connexion de votre application au hub de notification</span><span class="sxs-lookup"><span data-stu-id="ef164-163">Connect your app to the notification hub</span></span>
1. <span data-ttu-id="ef164-164">Dans Eclipse ADT, créez un projet Android (**File** > **New** > **Android Application Project**).</span><span class="sxs-lookup"><span data-stu-id="ef164-164">In Eclipse ADT, create a new Android project (**File** > **New** > **Android Application Project**).</span></span>
   
    ![][23]
2. <span data-ttu-id="ef164-165">Entrez un **nom d’application** et vérifiez que la version de **Kit de développement logiciel (SDK) minimum obligatoire** est définie sur **API 16 : Android 4.1**.</span><span class="sxs-lookup"><span data-stu-id="ef164-165">Enter an **Application Name** and ensure that the **Minimum Required SDK** version is set to **API 16: Android 4.1**.</span></span>
   
    ![][24]
3. <span data-ttu-id="ef164-166">Cliquez sur **Next** et continuez à suivre l’Assistant jusqu’à ce que la fenêtre **Create Activity** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ef164-166">Click **Next** and continue following the wizard until the **Create Activity** window appears.</span></span> <span data-ttu-id="ef164-167">Assurez-vous que l’option **Blank Activity** est sélectionnée, puis cliquez sur **Finish** pour créer une application Android.</span><span class="sxs-lookup"><span data-stu-id="ef164-167">Make sure that **Blank Activity** is selected, and finally select **Finish** to create a new Android Application.</span></span>
   
    ![][25]
4. <span data-ttu-id="ef164-168">Assurez-vous que la **cible de génération du projet** est définie correctement.</span><span class="sxs-lookup"><span data-stu-id="ef164-168">Make sure that the **Project Build Target** is set correctly.</span></span>
   
    ![][26]
5. <span data-ttu-id="ef164-169">Téléchargez le fichier notification-hubs-0.4.jar à partir de l’onglet **Fichiers** du [Notification-Hubs-Android-SDK sur Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span><span class="sxs-lookup"><span data-stu-id="ef164-169">Download the notification-hubs-0.4.jar file from the **Files** tab of the [Notification-Hubs-Android-SDK on Bintray](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4).</span></span> <span data-ttu-id="ef164-170">Ajoutez le fichier au dossier **libs** de votre projet Eclipse, puis actualisez le dossier *libs* .</span><span class="sxs-lookup"><span data-stu-id="ef164-170">Add the file to the **libs** folder of your Eclipse project, and refresh the *libs* folder.</span></span>
6. <span data-ttu-id="ef164-171">Téléchargez et décompressez le [Kit de développement logiciel (SDK) Android pour transmissions push Baidu], ouvrez le dossier **libs**, puis copiez le fichier jar **pushservice-x.y.z** et les dossiers **armeabi** & **mips** dans le dossier **libs** de votre application Android.</span><span class="sxs-lookup"><span data-stu-id="ef164-171">Download and unzip the [Baidu Push Android SDK], open the **libs** folder, and then copy the **pushservice-x.y.z** jar file and the **armeabi** & **mips** folders in the **libs** folder of your Android application.</span></span>
7. <span data-ttu-id="ef164-172">Ouvrez le fichier **AndroidManifest.xml** de votre projet Android et ajoutez les autorisations requises par le Kit de développement logiciel (SDK) Baidu.</span><span class="sxs-lookup"><span data-stu-id="ef164-172">Open the **AndroidManifest.xml** file of your Android project and add the permissions that are required by the Baidu SDK.</span></span>
   
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
8. <span data-ttu-id="ef164-173">Ajoutez la propriété **android:name** à votre élément **application** dans le fichier **AndroidManifest.xml** en remplaçant *yourprojectname* par votre nom de projet (par exemple, **com.example.BaiduTest**).</span><span class="sxs-lookup"><span data-stu-id="ef164-173">Add the **android:name** property to your **application** element in **AndroidManifest.xml**, replacing *yourprojectname* (for example, **com.example.BaiduTest**).</span></span> <span data-ttu-id="ef164-174">Assurez-vous que ce nom de projet correspond à celui que vous avez configuré dans la console Baidu.</span><span class="sxs-lookup"><span data-stu-id="ef164-174">Make sure that this project name matches the one that you configured in the Baidu console.</span></span>
   
        <application android:name="yourprojectname.DemoApplication"
9. <span data-ttu-id="ef164-175">Ajoutez la configuration ci-après dans l’élément application après l’élément d’activité **.MainActivity** en remplaçant *yourprojectname* par votre nom de projet (par exemple, **com.example.BaiduTest**) :</span><span class="sxs-lookup"><span data-stu-id="ef164-175">Add the following configuration within the application element after the **.MainActivity** activity element, replacing *yourprojectname* (for example, **com.example.BaiduTest**):</span></span>
   
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
10. <span data-ttu-id="ef164-176">Ajoutez une nouvelle classe appelée **ConfigurationSettings.java** au projet.</span><span class="sxs-lookup"><span data-stu-id="ef164-176">Add a new class called **ConfigurationSettings.java** to the project.</span></span>
    
     ![][28]
    
     ![][29]
11. <span data-ttu-id="ef164-177">Ajoutez-lui le code suivant :</span><span class="sxs-lookup"><span data-stu-id="ef164-177">Add the following code to it:</span></span>
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    <span data-ttu-id="ef164-178">Définissez **API_KEY** sur la valeur que vous avez récupérée précédemment du projet cloud Baidu, **NotificationHubName** sur le nom de votre hub de notification issu du portail Azure Classic et **NotificationHubConnectionString** sur la valeur DefaultListenSharedAccessSignature issue du portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="ef164-178">Set the value of **API_KEY** with what you retrieved from the Baidu cloud project earlier, **NotificationHubName** with your notification hub name from the Azure Classic Portal and **NotificationHubConnectionString** with DefaultListenSharedAccessSignature from the Azure Classic Portal.</span></span>
12. <span data-ttu-id="ef164-179">Ajoutez une nouvelle classe appelée **DemoApplication.java**et ajoutez-lui le code suivant :</span><span class="sxs-lookup"><span data-stu-id="ef164-179">Add a new class called **DemoApplication.java**, and add the following code to it:</span></span>
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. <span data-ttu-id="ef164-180">Ajoutez une autre nouvelle classe appelée **MyPushMessageReceiver.java**et ajoutez-lui le code suivant.</span><span class="sxs-lookup"><span data-stu-id="ef164-180">Add another new class called **MyPushMessageReceiver.java**, and add the following code to it.</span></span> <span data-ttu-id="ef164-181">Il s’agit de la classe qui gère les notifications Push reçues à partir du serveur push Baidu.</span><span class="sxs-lookup"><span data-stu-id="ef164-181">It is the class that handles the push notifications that are received from the Baidu push server.</span></span>
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG to Log */
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
14. <span data-ttu-id="ef164-182">Ouvrez **MainActivity.java** et ajoutez le code suivant à la méthode **onCreate** :</span><span class="sxs-lookup"><span data-stu-id="ef164-182">Open **MainActivity.java**, and add the following to the **onCreate** method:</span></span>
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. <span data-ttu-id="ef164-183">Ouvrez les instructions d’importation suivantes en haut :</span><span class="sxs-lookup"><span data-stu-id="ef164-183">Open the following import statements at the top:</span></span>
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-to-your-app"></a><span data-ttu-id="ef164-184">Envoi de notifications à votre application</span><span class="sxs-lookup"><span data-stu-id="ef164-184">Send notifications to your app</span></span>
<span data-ttu-id="ef164-185">Vous pouvez tester rapidement la réception de notifications dans votre application en envoyant des notifications dans le [Portail Azure](https://portal.azure.com/) à l’aide du bouton **Envoyer** sur le hub de notification, comme illustré ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="ef164-185">You can quickly test receiving notifications in your app by sending notifications in the [Azure portal](https://portal.azure.com/) using the **Send** button on the notification hub, as shown in the following screen:</span></span>

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

<span data-ttu-id="ef164-186">Les notifications Push sont normalement envoyées dans un service principal tel que Mobile Services ou ASP.NET à l’aide d’une bibliothèque compatible.</span><span class="sxs-lookup"><span data-stu-id="ef164-186">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="ef164-187">Si une bibliothèque n’est pas disponible pour votre serveur principal, vous pouvez utiliser l’API REST directement pour envoyer des messages de notification.</span><span class="sxs-lookup"><span data-stu-id="ef164-187">If a library is not available for your back-end, you can use the REST API directly to send notification messages .</span></span>

<span data-ttu-id="ef164-188">Dans ce didacticiel, nous nous contentons pour plus de simplicité de tester votre application cliente en envoyant des notifications à l’aide du Kit de développement logiciel (SDK) .NET pour Notification Hubs dans une application console au lieu d’un service principal.</span><span class="sxs-lookup"><span data-stu-id="ef164-188">In this tutorial, we keep it simple and just demonstrate testing your client app by sending notifications using the .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="ef164-189">Nous vous recommandons de consulter le didacticiel [Utiliser Notification Hubs pour envoyer des notifications Push aux utilisateurs](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) comme prochaine étape pour envoyer des notifications à partir d’un serveur principal ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ef164-189">We recommend the [Use Notification Hubs to push notifications to users](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) tutorial as the next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="ef164-190">Toutefois, les approches suivantes peuvent servir à envoyer des notifications :</span><span class="sxs-lookup"><span data-stu-id="ef164-190">However, the following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="ef164-191">**Interface REST** : vous pouvez prendre en charge les notifications sur n’importe quel serveur principal à l’aide de [l’interface REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="ef164-191">**REST Interface**:  You can support notification on any backend platform using  the [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="ef164-192">**SDK .NET Microsoft Azure Notification Hubs**: dans le Gestionnaire de package Nuget pour Visual Studio, exécutez [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="ef164-192">**Microsoft Azure Notification Hubs .NET SDK**: In the Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="ef164-193">**Node.js** : [Utilisation de Notification Hubs à partir de Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="ef164-193">**Node.js**: [How to use Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="ef164-194">**Applications mobiles Azure**: pour découvrir un exemple de la procédure d’envoi de notifications à partir d’une application mobile Azure intégrée à Notification Hubs, consultez l’article [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) (Ajouter des notifications Push pour Mobile Apps).</span><span class="sxs-lookup"><span data-stu-id="ef164-194">**Mobile Apps**: For an example of how to send notifications from an Azure App Service Mobile Apps backend that's integrated with Notification Hubs, see [Add push notifications to your mobile app](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="ef164-195">**Java/PHP** : pour voir un exemple d’envoi de notifications au moyen des API REST, consultez « Utilisation de Notification Hubs depuis Java/PHP » ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="ef164-195">**Java / PHP**: For an example of how to send notifications by using the REST APIs, see "How to use Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-net-console-app"></a><span data-ttu-id="ef164-196">(Facultatif) Envoi de notifications à partir d’une application de console .NET.</span><span class="sxs-lookup"><span data-stu-id="ef164-196">(Optional) Send notifications from a .NET console app.</span></span>
<span data-ttu-id="ef164-197">Dans cette section, nous montrons comment envoyer une notification à l’aide d’une application console .NET.</span><span class="sxs-lookup"><span data-stu-id="ef164-197">In this section, we show sending a notification using a .NET console app.</span></span>

1. <span data-ttu-id="ef164-198">Créez une application console Visual C# :</span><span class="sxs-lookup"><span data-stu-id="ef164-198">Create a new Visual C# console application:</span></span>
   
    ![][30]
2. <span data-ttu-id="ef164-199">Dans la fenêtre Console du gestionnaire de package, choisissez **Projet par défaut** comme nouveau projet d’application console, puis exécutez la commande suivante dans la fenêtre de console :</span><span class="sxs-lookup"><span data-stu-id="ef164-199">In the Package Manager Console window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="ef164-200">Cette instruction ajoute une référence au Kit de développement logiciel (SDK) Azure Notification Hubs à l’aide du <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">package NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="ef164-200">This instruction adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. <span data-ttu-id="ef164-201">Ouvrez le fichier **Program.cs** et ajoutez l’instruction using suivante :</span><span class="sxs-lookup"><span data-stu-id="ef164-201">Open the file **Program.cs** and add the following using statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
4. <span data-ttu-id="ef164-202">Dans votre classe `Program`, ajoutez la méthode ci-après et remplacez *DefaultFullSharedAccessSignatureSASConnectionString* et *NotificationHubName* par les valeurs dont vous disposez.</span><span class="sxs-lookup"><span data-stu-id="ef164-202">In your `Program` class, add the following method and replace *DefaultFullSharedAccessSignatureSASConnectionString* and *NotificationHubName* with the values that you have.</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. <span data-ttu-id="ef164-203">Ajoutez les lignes suivantes dans votre méthode **Main** :</span><span class="sxs-lookup"><span data-stu-id="ef164-203">Add the following lines in your **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a><span data-ttu-id="ef164-204">Test de l'application</span><span class="sxs-lookup"><span data-stu-id="ef164-204">Test your app</span></span>
<span data-ttu-id="ef164-205">Pour tester cette application avec un téléphone réel, connectez simplement le téléphone à votre ordinateur à l’aide d’un câble USB.</span><span class="sxs-lookup"><span data-stu-id="ef164-205">To test this app with an actual phone, just connect the phone to your computer by using a USB cable.</span></span> <span data-ttu-id="ef164-206">Cette action charge votre application sur le téléphone attaché.</span><span class="sxs-lookup"><span data-stu-id="ef164-206">This action loads your app onto the attached phone.</span></span>

<span data-ttu-id="ef164-207">Pour tester cette application avec l’émulateur, dans la barre d’outils supérieure d’Eclipse, cliquez sur **Run**, puis sélectionnez votre application : elle démarre l’émulateur, puis charge et exécute l’application.</span><span class="sxs-lookup"><span data-stu-id="ef164-207">To test this app with the emulator, on the Eclipse top toolbar, click **Run**, and then select your app: it starts the emulator, loads, and runs the app.</span></span>

<span data-ttu-id="ef164-208">L’application récupère les paramètres userId et channelId à partir du service de notification push Baidu et s’inscrit auprès du hub de notification.</span><span class="sxs-lookup"><span data-stu-id="ef164-208">The app retrieves the 'userId' and 'channelId' from the Baidu Push notification service and registers with the notification hub.</span></span>

<span data-ttu-id="ef164-209">Pour envoyer une notification de test, vous pouvez utiliser l’onglet de débogage du Portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="ef164-209">To send a test notification, you can use the debug tab of the Azure Classic Portal.</span></span> <span data-ttu-id="ef164-210">Si vous avez intégré l’application de console .NET, appuyez sur la touche F5 dans Visual Studio pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="ef164-210">If you built the .NET console application for Visual Studio, just press the F5 key in Visual Studio to run the application.</span></span> <span data-ttu-id="ef164-211">L’application envoie une notification qui s’affiche dans la zone de notification supérieure de votre appareil ou de l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="ef164-211">The application sends a notification that appears in the top notification area of your device or emulator.</span></span>

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
<span data-ttu-id="ef164-212">[Kit de développement logiciel (SDK) Mobile Services pour Android]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409</span><span class="sxs-lookup"><span data-stu-id="ef164-212">[Mobile Services Android SDK]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409</span></span>
<span data-ttu-id="ef164-213">[Kit de développement logiciel (SDK) Android pour transmissions push Baidu]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk</span><span class="sxs-lookup"><span data-stu-id="ef164-213">[Baidu Push Android SDK]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk</span></span>
<span data-ttu-id="ef164-214">[Portail Azure Classic]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="ef164-214">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>
<span data-ttu-id="ef164-215">[portail Baidu]: http://www.baidu.com/</span><span class="sxs-lookup"><span data-stu-id="ef164-215">[Baidu portal]: http://www.baidu.com/</span></span>
