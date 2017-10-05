---
title: Validation des alertes dans Azure Security Center | Microsoft Docs
description: "Ce document est conçu pour vous aider à valider des alertes de sécurité dans Azure Security Center."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: f8f17a55-e672-4d86-8ba9-6c3ce2e71a57
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 121b5d8f023a9b663d0e7af26dce8f81db27672c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="alerts-validation-in-azure-security-center"></a><span data-ttu-id="3a427-103">Validation des alertes dans Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="3a427-103">Alerts Validation in Azure Security Center</span></span>
<span data-ttu-id="3a427-104">Ce document est conçu pour vous apprendre à vérifier si votre système est correctement configuré pour les alertes dans Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="3a427-104">This document helps you learn how to verify if your system is properly configured for Azure Security Center alerts.</span></span>

## <a name="what-are-security-alerts"></a><span data-ttu-id="3a427-105">Que sont les alertes de sécurité ?</span><span class="sxs-lookup"><span data-stu-id="3a427-105">What are security alerts?</span></span>
<span data-ttu-id="3a427-106">Security Center collecte, analyse et intègre automatiquement les données de journaux provenant de vos ressources Azure, du réseau et des solutions partenaires connectées, telles que les solutions de protection des points de terminaison et des pare-feux, pour détecter et pour vous avertir en cas de menace.</span><span class="sxs-lookup"><span data-stu-id="3a427-106">Security Center automatically collects, analyzes, and integrates log data from your Azure resources, the network, and connected partner solutions, like firewall and endpoint protection solutions, to detect and alert you to threats.</span></span> <span data-ttu-id="3a427-107">Pour plus d’informations sur les alertes de sécurité, lisez [Gestion et résolution des alertes de sécurité dans Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts), puis [Présentation des alertes de sécurité dans Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) pour en savoir plus sur les différents types d’alertes.</span><span class="sxs-lookup"><span data-stu-id="3a427-107">Read [Managing and responding to security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) for more information about security alerts, and read [Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type) to learn more about the different types of alerts.</span></span>

## <a name="alert-validation"></a><span data-ttu-id="3a427-108">Validation de l’alerte</span><span class="sxs-lookup"><span data-stu-id="3a427-108">Alert validation</span></span>
<span data-ttu-id="3a427-109">Après avoir installé l’agent de Security Center sur votre ordinateur, suivez les étapes ci-dessous depuis l’ordinateur sur lequel vous voulez configurer l’alerte de la ressource attaquée :</span><span class="sxs-lookup"><span data-stu-id="3a427-109">After Security Center agent is installed on your computer, follow the steps below from the computer where you want to be the attacked resource of the alert:</span></span>

1. <span data-ttu-id="3a427-110">Copiez un exécutable (calc.exe, par exemple) sur le bureau de votre ordinateur ou dans le répertoire de votre choix.</span><span class="sxs-lookup"><span data-stu-id="3a427-110">Copy an executable (for example calc.exe) to the computer’s desktop, or other directory of your convenience.</span></span>
2. <span data-ttu-id="3a427-111">Renommez ce fichier **ASC_AlertTest_662jfi039N.exe**.</span><span class="sxs-lookup"><span data-stu-id="3a427-111">Rename this file to **ASC_AlertTest_662jfi039N.exe**.</span></span>
3. <span data-ttu-id="3a427-112">Ouvrez l’invite de commandes et exécutez ce fichier avec un argument (un faux nom d’argument), tel que : *ASC_AlertTest_662jfi039N.exe -foo*</span><span class="sxs-lookup"><span data-stu-id="3a427-112">Open the command prompt and execute this file with an argument (just a fake argument name), such as: *ASC_AlertTest_662jfi039N.exe -foo*</span></span>
4. <span data-ttu-id="3a427-113">Patientez 5 à 10 minutes puis ouvrez les alertes dans Security Center.</span><span class="sxs-lookup"><span data-stu-id="3a427-113">Wait 5 to 10 minutes and open Security Center Alerts.</span></span> <span data-ttu-id="3a427-114">Vous devriez voir une alerte similaire à :</span><span class="sxs-lookup"><span data-stu-id="3a427-114">There you should find an alert similar to following one:</span></span>

    ![Validation de l’alerte](./media/security-center-alert-validation/security-center-alert-validation-fig1.png)

<span data-ttu-id="3a427-116">En examinant cette alerte, veillez à ce que la valeur du champ Arguments Auditing Enabled (Audit pour arguments activé) soit true.</span><span class="sxs-lookup"><span data-stu-id="3a427-116">When reviewing this alert, make sure the field Arguments Auditing Enabled appears as true.</span></span> <span data-ttu-id="3a427-117">S’il affiche la valeur false, vous devez activer la ligne de commande d’audit pour arguments.</span><span class="sxs-lookup"><span data-stu-id="3a427-117">If it shows false, you need to enable command-line arguments auditing.</span></span> <span data-ttu-id="3a427-118">Pour activer cette option, utilisez la ligne de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="3a427-118">You can enable this option using the following command line:</span></span>

<span data-ttu-id="3a427-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span><span class="sxs-lookup"><span data-stu-id="3a427-119">*reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\Audit" /f /v "ProcessCreationIncludeCmdLine_Enabled"*</span></span>


## <a name="see-also"></a><span data-ttu-id="3a427-120">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3a427-120">See also</span></span>
<span data-ttu-id="3a427-121">Cet article vous a présenté le processus de validation des alertes.</span><span class="sxs-lookup"><span data-stu-id="3a427-121">This article introduced you to the alerts validation process.</span></span> <span data-ttu-id="3a427-122">Maintenant que vous êtes familiarisé avec la validation, vous pouvez consulter les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="3a427-122">Now that you're familiar with this validation, try the following articles:</span></span>

* <span data-ttu-id="3a427-123">[Gestion et résolution des alertes de sécurité dans Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span><span class="sxs-lookup"><span data-stu-id="3a427-123">[Managing and responding to security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts).</span></span> <span data-ttu-id="3a427-124">Apprenez à gérer les alertes et à répondre aux incidents de sécurité dans Security Center.</span><span class="sxs-lookup"><span data-stu-id="3a427-124">Learn how to manage alerts, and respond to security incidents in Security Center.</span></span>
* <span data-ttu-id="3a427-125">[Surveillance de l’intégrité de la sécurité dans Azure Security Center](security-center-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="3a427-125">[Security health monitoring in Azure Security Center](security-center-monitoring.md).</span></span> <span data-ttu-id="3a427-126">découvrez comment surveiller l’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="3a427-126">Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="3a427-127">[Présentation des alertes de sécurité dans Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span><span class="sxs-lookup"><span data-stu-id="3a427-127">[Understanding security alerts in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type).</span></span> <span data-ttu-id="3a427-128">En savoir plus sur les différents types d’alertes de sécurité.</span><span class="sxs-lookup"><span data-stu-id="3a427-128">Learn about the different types of security alerts.</span></span>
* <span data-ttu-id="3a427-129">[Guide de résolution des problèmes d’Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span><span class="sxs-lookup"><span data-stu-id="3a427-129">[Azure Security Center Troubleshooting Guide](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide).</span></span> <span data-ttu-id="3a427-130">Apprenez à résoudre les problèmes fréquents dans Azure Security Center.</span><span class="sxs-lookup"><span data-stu-id="3a427-130">Learn how to troubleshoot common issues in Security Center.</span></span> 
* <span data-ttu-id="3a427-131">[FAQ du Centre de sécurité Azure](security-center-faq.md).</span><span class="sxs-lookup"><span data-stu-id="3a427-131">[Azure Security Center FAQ](security-center-faq.md).</span></span> <span data-ttu-id="3a427-132">forum aux questions concernant l’utilisation de ce service.</span><span class="sxs-lookup"><span data-stu-id="3a427-132">Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="3a427-133">[Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/).</span><span class="sxs-lookup"><span data-stu-id="3a427-133">[Azure Security Blog](http://blogs.msdn.com/b/azuresecurity/).</span></span> <span data-ttu-id="3a427-134">accédez à des billets de blog sur la sécurité et la conformité Azure.</span><span class="sxs-lookup"><span data-stu-id="3a427-134">Find blog posts about Azure security and compliance.</span></span>

