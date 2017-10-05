---
title: "Connecter Arduino (C) à Azure IoT - Leçon 1 : Configurer l’appareil | Microsoft Docs"
description: "Configurez Adafruit Feather M0 WiFi pour une première utilisation."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "configuration arduino, connecter arduino à un pc, configurer arduino, carte arduino"
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
ms.openlocfilehash: 9e319292e5d30dea7e45857e435825861aad1c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-your-device"></a><span data-ttu-id="36755-104">Configurer votre appareil</span><span class="sxs-lookup"><span data-stu-id="36755-104">Configure your device</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="36755-105">Procédure à suivre</span><span class="sxs-lookup"><span data-stu-id="36755-105">What you will do</span></span>
<span data-ttu-id="36755-106">Configurez votre carte Arduino Adafruit Feather M0 WiFi pour une première utilisation en assemblant la carte pour la mettre sous tension.</span><span class="sxs-lookup"><span data-stu-id="36755-106">Configure your Adafruit Feather M0 WiFi Arduino board for first-time use by assembling the board, powering it up.</span></span> <span data-ttu-id="36755-107">Si vous rencontrez des problèmes, recherchez des solutions dans la [page de résolution des problèmes](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="36755-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md).</span></span>

## <a name="what-you-need"></a><span data-ttu-id="36755-108">Ce dont vous avez besoin</span><span class="sxs-lookup"><span data-stu-id="36755-108">What you need</span></span>
<span data-ttu-id="36755-109">Pour cette opération, vous aurez besoin des composants suivants pour votre starter kit Adafruit Feather M0 WiFi :</span><span class="sxs-lookup"><span data-stu-id="36755-109">To complete this operation, you need the following parts for your Adafruit Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="36755-110">La carte Adafruit Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="36755-110">The Adafruit Feather M0 WiFi board</span></span>
* <span data-ttu-id="36755-111">Un câble Micro USB B vers Type A</span><span class="sxs-lookup"><span data-stu-id="36755-111">A Micro B to Type A USB cable</span></span>

![kit][kit]

<span data-ttu-id="36755-113">Vous aurez également besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="36755-113">You also need:</span></span>

* <span data-ttu-id="36755-114">Un ordinateur exécutant Windows, Mac ou Linux.</span><span class="sxs-lookup"><span data-stu-id="36755-114">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="36755-115">Une connexion sans fil pour la connexion de votre carte Arduino.</span><span class="sxs-lookup"><span data-stu-id="36755-115">A wireless connection for your Arduino board to connect to.</span></span>
* <span data-ttu-id="36755-116">Une connexion Internet pour télécharger l’outil de configuration.</span><span class="sxs-lookup"><span data-stu-id="36755-116">An Internet connection to download configuration tool.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="36755-117">Contenu</span><span class="sxs-lookup"><span data-stu-id="36755-117">What you will learn</span></span>
<span data-ttu-id="36755-118">Cet article portera sur les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="36755-118">In this article, you will learn:</span></span>

* <span data-ttu-id="36755-119">Comment assembler votre carte Arduino et la mettre sous tension pour les leçons suivantes.</span><span class="sxs-lookup"><span data-stu-id="36755-119">How to assemble your Arduino board and power it up for the following lessons.</span></span>
* <span data-ttu-id="36755-120">Comment ajouter des autorisations de port série sous Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="36755-120">How to add serial port permissions on Ubuntu.</span></span>

## <a name="connect-your-arduino-board-to-your-computer"></a><span data-ttu-id="36755-121">Connecter la carte Arduino à votre ordinateur</span><span class="sxs-lookup"><span data-stu-id="36755-121">Connect your Arduino board to your computer</span></span>

1. <span data-ttu-id="36755-122">Connectez le câble micro USB au port micro USB du haut.</span><span class="sxs-lookup"><span data-stu-id="36755-122">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Port micro USB du haut][top-micro-usb-port]

2. <span data-ttu-id="36755-124">Branchez l’autre extrémité du câble USB à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="36755-124">Plug the other end of USB cable into your computer.</span></span>

   ![USB de l’ordinateur][computer-usb]

## <a name="add-serial-port-permissions-on-ubuntu"></a><span data-ttu-id="36755-126">Ajouter des autorisations de port série sous Ubuntu</span><span class="sxs-lookup"><span data-stu-id="36755-126">Add serial port permissions on Ubuntu</span></span>

<span data-ttu-id="36755-127">Vous pouvez ignorer cette section si vous utilisez Windows ou macOS.</span><span class="sxs-lookup"><span data-stu-id="36755-127">You can skip this section if you use Windows or macOS.</span></span> <span data-ttu-id="36755-128">Pour Ubuntu, vous devez suivre les étapes suivantes afin que l’utilisateur Linux normal dispose bien des autorisations nécessaires pour utiliser le port USB de votre carte Arduino.</span><span class="sxs-lookup"><span data-stu-id="36755-128">For Ubuntu, you need the following steps to make sure the normal linux user has the permissions to operate on the USB port of your Arduino board.</span></span>

1. <span data-ttu-id="36755-129">À présent, en tant qu’utilisateur normal à partir du terminal :</span><span class="sxs-lookup"><span data-stu-id="36755-129">Now as normal user from terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   # Or
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="36755-130">Vous obtenez le résultat suivant :</span><span class="sxs-lookup"><span data-stu-id="36755-130">You will get something like:</span></span>

   ```bash
   crw-rw---- 1 root uucp 188, 0 5 apr 23.01 ttyUSB0
   # Or
   crw-rw---- 1 root dialout 188, 0 5 apr 23.01 ttyACM0
   ```

   <span data-ttu-id="36755-131">Le « 0 » peut être un autre nombre, et plusieurs entrées peuvent être retournées.</span><span class="sxs-lookup"><span data-stu-id="36755-131">The "0" might be a different number, or multiple entries might be returned.</span></span> <span data-ttu-id="36755-132">Dans le premier cas, nous avons besoin de la donnée `uucp`, dans le second de la donnée `dialout`, qui est le propriétaire du groupe du fichier.</span><span class="sxs-lookup"><span data-stu-id="36755-132">In the first case the data we need is `uucp`, in the second is `dialout`, which is the group owner of the file.</span></span>

2. <span data-ttu-id="36755-133">Ajouter un utilisateur au groupe :</span><span class="sxs-lookup"><span data-stu-id="36755-133">Add user to the to the group:</span></span>

   ```bash
   sudo usermod -a -G group-name username
   ```

   <span data-ttu-id="36755-134">Où `group-name` correspond à la donnée trouvée lors de la première étape et `username` à votre nom d’utilisateur Linux.</span><span class="sxs-lookup"><span data-stu-id="36755-134">Where `group-name` is the data found in the first step, and `username` is your linux user name.</span></span>

3. <span data-ttu-id="36755-135">Vous devrez vous déconnecter et vous reconnecter pour que cette modification prenne effet et pour terminer l’installation.</span><span class="sxs-lookup"><span data-stu-id="36755-135">You will need to log out and in again for this change to take effect and complete the setup.</span></span>

## <a name="summary"></a><span data-ttu-id="36755-136">Résumé</span><span class="sxs-lookup"><span data-stu-id="36755-136">Summary</span></span>
<span data-ttu-id="36755-137">Dans cet article, vous avez appris à configurer votre carte Arduino.</span><span class="sxs-lookup"><span data-stu-id="36755-137">In this article, you’ve learned how to configure your Arduino board.</span></span> <span data-ttu-id="36755-138">La tâche suivante consiste à installer les outils et logiciels nécessaires en vue d’exécuter un exemple d’application sur votre carte Arduino.</span><span class="sxs-lookup"><span data-stu-id="36755-138">The next task is to install the necessary tools and software in preparation for running a sample application on your Arduino board.</span></span>

![Le matériel est prêt.][hardware-is-ready]

## <a name="next-steps"></a><span data-ttu-id="36755-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="36755-140">Next steps</span></span>
<span data-ttu-id="36755-141">[Obtenez les outils][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="36755-141">[Get the tools][get-the-tools]</span></span>
<!-- Images and links -->

[kit]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/kit.png
[top-micro-usb-port]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/top_usbport.jpg
[computer-usb]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/computer_usb.jpg
[hardware-is-ready]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/hardware_ready.jpg
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md