---
title: "Connect Arduino (C) tooAzure IoT - leçon 1 : configurer l’appareil | Documents Microsoft"
description: "Configurez Adafruit Feather M0 WiFi pour une première utilisation."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino configuré, connectez-vous arduino toopc, le programme d’installation arduino, arduino carte"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: f5b334f0-a148-41aa-b374-ce7b9f5b305a
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 30b764e8ff6221995456283a226e79f064b2d74e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="c77fa-104">Configurer votre appareil</span><span class="sxs-lookup"><span data-stu-id="c77fa-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="c77fa-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="c77fa-105">What you will do</span></span>
<span data-ttu-id="c77fa-106">Configurer votre tableau Adafruit estompe M0 Wi-Fi Arduino pour la première utilisation en assemblant tableau hello, il sous tension.</span><span class="sxs-lookup"><span data-stu-id="c77fa-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling hello board, powering it up.</span></span> <span data-ttu-id="c77fa-107">Si vous rencontrez des problèmes, recherchez des solutions sur hello [page Résolution des problèmes](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c77fa-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c77fa-108">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="c77fa-108">What you need</span></span>
<span data-ttu-id="c77fa-109">toocomplete cette opération, vous devez hello composants suivants de votre Starter Kit pour Adafruit estompe M0 Wi-Fi :</span><span class="sxs-lookup"><span data-stu-id="c77fa-109">toocomplete this operation, you need hello following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="c77fa-110">Hello Adafruit estompe M0 WiFi tableau</span><span class="sxs-lookup"><span data-stu-id="c77fa-110">hello Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="c77fa-111">Un câble USB d’un de tooType Micro B</span><span class="sxs-lookup"><span data-stu-id="c77fa-111">A Micro B tooType A USB cable</span></span>

![kit][kit]

<span data-ttu-id="c77fa-113">Vous aurez également besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c77fa-113">You also need:</span></span>

* <span data-ttu-id="c77fa-114">Un ordinateur exécutant Windows, Mac ou Linux.</span><span class="sxs-lookup"><span data-stu-id="c77fa-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="c77fa-115">Une connexion sans fil pour votre tooconnect de carte Arduino à.</span><span class="sxs-lookup"><span data-stu-id="c77fa-115">A wireless connection for your Arduino board tooconnect to.</span></span>
* <span data-ttu-id="c77fa-116">Un outil de configuration toodownload de connexion Internet.</span><span class="sxs-lookup"><span data-stu-id="c77fa-116">An Internet connection toodownload configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c77fa-117">Contenu</span><span class="sxs-lookup"><span data-stu-id="c77fa-117">What you will learn</span></span>
<span data-ttu-id="c77fa-118">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c77fa-118">In this article, you will learn:</span></span>

* <span data-ttu-id="c77fa-119">Comment tooassemble votre Arduino carte et l’alimentation pour hello suivant leçons.</span><span class="sxs-lookup"><span data-stu-id="c77fa-119">How tooassemble your Arduino board and power it up for hello following lessons.</span></span>
* <span data-ttu-id="c77fa-120">Comment tooadd les autorisations de port série sur Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="c77fa-120">How tooadd serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-tooyour-computer"></a><span data-ttu-id="c77fa-121">Connectez votre ordinateur de tooyour Arduino du tableau</span><span class="sxs-lookup"><span data-stu-id="c77fa-121">Connect your Arduino board tooyour computer</span></span>

1. <span data-ttu-id="c77fa-122">Branchez les câbles USB micro hello le port USB supérieur micro hello.</span><span class="sxs-lookup"><span data-stu-id="c77fa-122">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Port micro USB du haut][top-micro-usb-port]

2. <span data-ttu-id="c77fa-124">Plug hello l’autre extrémité du câble USB à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="c77fa-124">Plug hello other end of USB cable into your computer.</span></span>

   ![USB de l’ordinateur][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="c77fa-126">Ajouter des autorisations de port série sous Ubuntu</span><span class="sxs-lookup"><span data-stu-id="c77fa-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="c77fa-127">Vous pouvez ignorer cette section si vous utilisez Windows ou macOS.</span><span class="sxs-lookup"><span data-stu-id="c77fa-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="c77fa-128">Ubuntu, vous devez hello suivant toomake étapes qu’utilisateur linux normal de hello a hello autorisations toooperate sur le port USB hello de votre tableau Arduino.</span><span class="sxs-lookup"><span data-stu-id="c77fa-128">For Ubuntu, you need hello following steps toomake sure hello normal linux user has hello permissions toooperate on hello USB port of your Arduino board.</span></span>

1. <span data-ttu-id="c77fa-129">À présent, en tant qu’utilisateur normal à partir du terminal :</span><span class="sxs-lookup"><span data-stu-id="c77fa-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="c77fa-130">Vous obtenez le résultat suivant :</span><span class="sxs-lookup"><span data-stu-id="c77fa-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="c77fa-131">Hello « 0 » peut être un nombre différent, ou plusieurs entrées peuvent être retournées.</span><span class="sxs-lookup"><span data-stu-id="c77fa-131">hello "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="c77fa-132">Dans les premières données hello cas hello, nous devons est `uucp`, Bonjour ensuite est `dialout`, qui est propriétaire du groupe de fichiers de hello hello.</span><span class="sxs-lookup"><span data-stu-id="c77fa-132">In hello first case hello data we need is `uucp`, in hello second is `dialout`, which is hello group owner of hello file.</span></span>

2. <span data-ttu-id="c77fa-133">Ajouter un groupe d’utilisateurs toohello toohello :</span><span class="sxs-lookup"><span data-stu-id="c77fa-133">Add user toohello toohello group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="c77fa-134">Où `group-name` est trouvées dans la première étape de hello, les données de salutation et `username` est votre nom d’utilisateur linux.</span><span class="sxs-lookup"><span data-stu-id="c77fa-134">Where `group-name` is hello data found in hello first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="c77fa-135">Vous devez toolog extraction et à nouveau pour cette modification tootake effet et du programme d’installation complète hello.</span><span class="sxs-lookup"><span data-stu-id="c77fa-135">You will need toolog out and in again for this change tootake effect and complete hello setup.</span></span>

## <a name="summary"></a><span data-ttu-id="c77fa-136">Résumé</span><span class="sxs-lookup"><span data-stu-id="c77fa-136">Summary</span></span>
<span data-ttu-id="c77fa-137">Dans cet article, vous avez appris comment tooconfigure votre tableau Arduino.</span><span class="sxs-lookup"><span data-stu-id="c77fa-137">In this article, you’ve learned how tooconfigure your Arduino board.</span></span> <span data-ttu-id="c77fa-138">la tâche suivante Hello est tooinstall hello outils et nécessaires logiciel en vue d’un exemple d’application en cours d’exécution sur votre tableau de Arduino.</span><span class="sxs-lookup"><span data-stu-id="c77fa-138">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![Le matériel est prêt.][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="c77fa-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c77fa-140">Next steps</span></span>
<span data-ttu-id="c77fa-141">[Obtenir les outils de hello][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="c77fa-141">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md