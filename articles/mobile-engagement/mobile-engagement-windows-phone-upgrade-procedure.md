---
title: "aaaWindows les procédures de mise à niveau Phone Silverlight SDK"
description: "Procédures de mise à niveau du SDK Windows Phone Silverlight pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 87130026-9759-4659-9184-788a3627a165
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d72e7b8a59ef2c0a95b22efbf1e5257271399ddc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="2992d-103">Procédures de mise à niveau du Kit de développement Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="2992d-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="2992d-104">Si vous avez déjà intégré une ancienne version de notre kit de développement logiciel dans votre application, vous avez hello tooconsider hello Kit de développement logiciel de la mise à niveau les points suivants.</span><span class="sxs-lookup"><span data-stu-id="2992d-104">If you already have integrated an older version of our SDK into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="2992d-105">Vous avez peut-être toofollow plusieurs procédures issue de plusieurs versions du Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="2992d-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="2992d-106">Par exemple, si vous migrez à partir de 0.10.1 too0.11.0 avoir toofirst suivez hello » à partir de 0.9.0 too0.10.1 « procédure puis hello » à partir de 0.10.1 too0.11.0 « procédure.</span><span class="sxs-lookup"><span data-stu-id="2992d-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-200-too330"></a><span data-ttu-id="2992d-107">À partir de 2.0.0 too3.3.0</span><span class="sxs-lookup"><span data-stu-id="2992d-107">From 2.0.0 too3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="2992d-108">Journaux des tests</span><span class="sxs-lookup"><span data-stu-id="2992d-108">Test logs</span></span>
<span data-ttu-id="2992d-109">Journaux de la console produits par hello SDK peuvent être activé/désactivé/filtrées.</span><span class="sxs-lookup"><span data-stu-id="2992d-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="2992d-110">toocustomize, propriété hello de mise à jour `EngagementAgent.Instance.TestLogEnabled` tooone de valeur hello disponible à partir de hello `EngagementTestLogLevel` énumération, par exemple :</span><span class="sxs-lookup"><span data-stu-id="2992d-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-too200"></a><span data-ttu-id="2992d-111">À partir de 1.1.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="2992d-111">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="2992d-112">Hello suivante décrit comment toomigrate une intégration du Kit de développement logiciel de hello Capptain service offert par Capptain SAS dans une application grâce à Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="2992d-112">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2992d-113">Capptain et Mobile Engagement sont hello pas les mêmes services et procédure hello fourni ci-dessous uniquement met en évidence comment toomigrate hello application cliente.</span><span class="sxs-lookup"><span data-stu-id="2992d-113">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="2992d-114">Migration hello SDK dans l’application hello ne fait pas migrer vos données des hello Capptain toohello Mobile Engagement serveurs</span><span class="sxs-lookup"><span data-stu-id="2992d-114">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="2992d-115">Si vous effectuez une migration à partir d’une version antérieure, veuillez consultez hello Capptain site web toomigrate too1.1.1 tout d’abord, appliquez hello procédure</span><span class="sxs-lookup"><span data-stu-id="2992d-115">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="2992d-116">Package NuGet</span><span class="sxs-lookup"><span data-stu-id="2992d-116">Nuget package</span></span>
<span data-ttu-id="2992d-117">Remplacez **Capptain.WindowsPhone** par le package NuGet **MicrosoftAzure.MobileEngagement**.</span><span class="sxs-lookup"><span data-stu-id="2992d-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="2992d-118">Application d'Engagement Mobile</span><span class="sxs-lookup"><span data-stu-id="2992d-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="2992d-119">Hello SDK utilise le terme de hello `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="2992d-119">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="2992d-120">Vous devez tooupdate toomatch de votre projet cette modification.</span><span class="sxs-lookup"><span data-stu-id="2992d-120">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="2992d-121">Vous devez toouninstall votre package nuget Capptain.</span><span class="sxs-lookup"><span data-stu-id="2992d-121">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="2992d-122">Considérez que toutes vos modifications dans le dossier de ressources Capptain seront supprimées.</span><span class="sxs-lookup"><span data-stu-id="2992d-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="2992d-123">Si vous souhaitez tookeep ces fichiers, faites une copie d’eux.</span><span class="sxs-lookup"><span data-stu-id="2992d-123">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="2992d-124">Après cela, installer le nouveau package de nuget Microsoft Azure Engagement hello sur votre projet.</span><span class="sxs-lookup"><span data-stu-id="2992d-124">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="2992d-125">Vous le trouverez directement sur [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span><span class="sxs-lookup"><span data-stu-id="2992d-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="2992d-126">Ce remplace action tous les fichiers de ressources utilisées par l’Engagement et ajoute hello nouvelle DLL d’Engagement tooyour les références de projet.</span><span class="sxs-lookup"><span data-stu-id="2992d-126">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="2992d-127">Vous avez tooclean à vos références de projet et en supprimant les références Capptain DLL.</span><span class="sxs-lookup"><span data-stu-id="2992d-127">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="2992d-128">Si vous n’apportez pas cette option, version hello de Capptain est en conflit et erreur se produira.</span><span class="sxs-lookup"><span data-stu-id="2992d-128">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="2992d-129">Si vous avez personnalisé les ressources Capptain, copiez votre ancien contenu de fichiers et les coller dans des fichiers de Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="2992d-129">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="2992d-130">Notez que les fichiers xaml et cs ont toobe mis à jour.</span><span class="sxs-lookup"><span data-stu-id="2992d-130">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="2992d-131">Une fois ces étapes terminées il vous suffit tooreplace les anciennes références Capptain par nouvelles références d’Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="2992d-131">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="2992d-132">Tous les espaces de noms Capptain ont toobe mis à jour.</span><span class="sxs-lookup"><span data-stu-id="2992d-132">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="2992d-133">Avant la migration :</span><span class="sxs-lookup"><span data-stu-id="2992d-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="2992d-134">Après la migration :</span><span class="sxs-lookup"><span data-stu-id="2992d-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="2992d-135">Toutes les classes Capptain qui contiennent « Capptain » doivent contenir « Engagement ».</span><span class="sxs-lookup"><span data-stu-id="2992d-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="2992d-136">Avant la migration :</span><span class="sxs-lookup"><span data-stu-id="2992d-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="2992d-137">Après la migration :</span><span class="sxs-lookup"><span data-stu-id="2992d-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="2992d-138">Pour les fichiers xaml, les attributs et les espaces de noms Capptain changent également.</span><span class="sxs-lookup"><span data-stu-id="2992d-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="2992d-139">Avant la migration :</span><span class="sxs-lookup"><span data-stu-id="2992d-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="2992d-140">Après la migration :</span><span class="sxs-lookup"><span data-stu-id="2992d-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="2992d-141">Pourquoi autres ressources comme des images Capptain, notez qu’ils ont également été renommé toouse « Engagement ».</span><span class="sxs-lookup"><span data-stu-id="2992d-141">For hello other resources like Capptain pictures, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="2992d-142">ID de l'application / clé SDK</span><span class="sxs-lookup"><span data-stu-id="2992d-142">Application ID / SDK Key</span></span>
<span data-ttu-id="2992d-143">Engagement utilise une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="2992d-143">Engagement uses a connection string.</span></span> <span data-ttu-id="2992d-144">Vous n’avez pas toospecify un ID d’application et une clé de kit de développement logiciel avec Mobile Engagement, vous devez uniquement toospecify une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="2992d-144">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="2992d-145">Vous pouvez la configurer dans votre fichier EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="2992d-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="2992d-146">configuration d’Engagement Hello peut être définie dans votre `Resources\EngagementConfiguration.xml` le fichier de votre projet.</span><span class="sxs-lookup"><span data-stu-id="2992d-146">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="2992d-147">Modifiez cette toospecify de fichier :</span><span class="sxs-lookup"><span data-stu-id="2992d-147">Edit this file toospecify:</span></span>

* <span data-ttu-id="2992d-148">Votre chaîne de connexion d'application entre les balises `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="2992d-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="2992d-149">Si vous souhaitez toospecify il lors de l’exécution au lieu de cela, vous pouvez appeler suivant de hello méthode avant l’initialisation de l’agent hello Engagement :</span><span class="sxs-lookup"><span data-stu-id="2992d-149">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="2992d-150">chaîne de connexion Hello pour votre application s’affiche dans hello portail classique Azure.</span><span class="sxs-lookup"><span data-stu-id="2992d-150">hello connection string for your application is displayed in hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="2992d-151">Changement de noms d'éléments</span><span class="sxs-lookup"><span data-stu-id="2992d-151">Items name change</span></span>
<span data-ttu-id="2992d-152">Tous les éléments nommés *capptain* ont été renommés *engagement*.</span><span class="sxs-lookup"><span data-stu-id="2992d-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="2992d-153">De même pour *Capptain* trop*Engagement*.</span><span class="sxs-lookup"><span data-stu-id="2992d-153">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="2992d-154">Exemples d'éléments Capptain couramment utilisés :</span><span class="sxs-lookup"><span data-stu-id="2992d-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="2992d-155">CapptainConfiguration se nomme maintenant EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="2992d-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="2992d-156">CapptainAgent se nomme maintenant EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="2992d-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="2992d-157">CapptainReach se nomme maintenant EngagementReach</span><span class="sxs-lookup"><span data-stu-id="2992d-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="2992d-158">CapptainHttpConfig se nomme maintenant EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="2992d-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="2992d-159">GetCapptainPageName se nomme maintenant GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="2992d-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="2992d-160">Notez que ce changement affecte également les méthodes substituées.</span><span class="sxs-lookup"><span data-stu-id="2992d-160">Note that rename also affects overridden methods.</span></span>

