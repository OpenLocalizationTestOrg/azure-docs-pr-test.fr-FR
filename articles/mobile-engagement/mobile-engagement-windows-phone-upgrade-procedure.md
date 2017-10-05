---
title: "Procédures de mise à niveau du Kit de développement Windows Phone Silverlight"
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
ms.openlocfilehash: f87f65788075c7f4067e77946e1bcbc8f3709317
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-sdk-upgrade-procedures"></a><span data-ttu-id="964d1-103">Procédures de mise à niveau du Kit de développement Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="964d1-103">Windows Phone Silverlight SDK Upgrade Procedures</span></span>
<span data-ttu-id="964d1-104">Si vous avez déjà intégré une ancienne version de notre SDK à votre application, tenez compte des points suivants avant de procéder à la mise à niveau du SDK.</span><span class="sxs-lookup"><span data-stu-id="964d1-104">If you already have integrated an older version of our SDK into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="964d1-105">Vous devrez peut-être suivre quelques procédures si vous avez manqué plusieurs versions du kit SDK.</span><span class="sxs-lookup"><span data-stu-id="964d1-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="964d1-106">Par exemple, si vous migrez de la version 0.10.1 vers 0.11.0, vous devez tout d'abord suivre la procédure « Migration de 0.9.0 vers 0.10.1 », puis la procédure « Migration de 0.10.1 vers 0.11.0 ».</span><span class="sxs-lookup"><span data-stu-id="964d1-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-200-to-330"></a><span data-ttu-id="964d1-107">Migration de 2.0.0 vers 3.3.0</span><span class="sxs-lookup"><span data-stu-id="964d1-107">From 2.0.0 to 3.3.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="964d1-108">Journaux des tests</span><span class="sxs-lookup"><span data-stu-id="964d1-108">Test logs</span></span>
<span data-ttu-id="964d1-109">Les journaux de console produits par le Kit de développement logiciel (SDK) peuvent maintenant être activés/désactivés/filtrés.</span><span class="sxs-lookup"><span data-stu-id="964d1-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="964d1-110">Pour personnaliser ce résultat, mettez à jour la propriété `EngagementAgent.Instance.TestLogEnabled` avec une des valeurs disponibles à partir de l'énumération `EngagementTestLogLevel`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="964d1-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

## <a name="from-111-to-200"></a><span data-ttu-id="964d1-111">Migration de 1.1.1 vers 2.0.0</span><span class="sxs-lookup"><span data-stu-id="964d1-111">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="964d1-112">La section qui suit décrit comment migrer une intégration du SDK à partir du service Capptain offert par Capptain SAS dans une application reposant sur Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="964d1-112">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="964d1-113">Capptain et Engagement Mobile ne sont pas les mêmes services et la procédure décrite ci-dessous explique uniquement comment migrer l'application cliente.</span><span class="sxs-lookup"><span data-stu-id="964d1-113">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="964d1-114">La migration du SDK dans l'application ne migre PAS vos données des serveurs Capptain vers les serveurs Engagement Mobile.</span><span class="sxs-lookup"><span data-stu-id="964d1-114">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="964d1-115">Si vous migrez à partir d'une version antérieure, consultez le site web de Capptain pour migrer tout d'abord vers 1.1.1, puis appliquez la procédure suivante.</span><span class="sxs-lookup"><span data-stu-id="964d1-115">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="964d1-116">Package NuGet</span><span class="sxs-lookup"><span data-stu-id="964d1-116">Nuget package</span></span>
<span data-ttu-id="964d1-117">Remplacez **Capptain.WindowsPhone** par le package NuGet **MicrosoftAzure.MobileEngagement**.</span><span class="sxs-lookup"><span data-stu-id="964d1-117">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="964d1-118">Application d'Engagement Mobile</span><span class="sxs-lookup"><span data-stu-id="964d1-118">Applying Mobile Engagement</span></span>
<span data-ttu-id="964d1-119">Le SDK utilise le terme `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="964d1-119">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="964d1-120">Vous devez mettre à jour votre projet pour qu'il corresponde à cette modification.</span><span class="sxs-lookup"><span data-stu-id="964d1-120">You need to update your project to match this change.</span></span>

<span data-ttu-id="964d1-121">Vous devez désinstaller votre package nuget Capptain actuel.</span><span class="sxs-lookup"><span data-stu-id="964d1-121">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="964d1-122">Considérez que toutes vos modifications dans le dossier de ressources Capptain seront supprimées.</span><span class="sxs-lookup"><span data-stu-id="964d1-122">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="964d1-123">Si vous souhaitez conserver ces fichiers, effectuez-en une copie.</span><span class="sxs-lookup"><span data-stu-id="964d1-123">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="964d1-124">Après cela, installez le nouveau package nuget Microsoft Azure Engagement sur votre projet.</span><span class="sxs-lookup"><span data-stu-id="964d1-124">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="964d1-125">Vous le trouverez directement sur [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span><span class="sxs-lookup"><span data-stu-id="964d1-125">You can find it directly on [Nuget](http://www.nuget.org/packages/MicrosoftAzure.MobileEngagement).</span></span> <span data-ttu-id="964d1-126">Cette action remplace tous les fichiers de ressources utilisés par Engagement et ajoute la nouvelle DLL Engagement à vos références de projet.</span><span class="sxs-lookup"><span data-stu-id="964d1-126">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="964d1-127">Vous devez nettoyer vos références de projet en supprimant les références à la DLL Capptain.</span><span class="sxs-lookup"><span data-stu-id="964d1-127">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="964d1-128">Si vous ne le faites pas, la version de Capptain génère un conflit et une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="964d1-128">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="964d1-129">Si vous avez personnalisé des ressources Capptain, copiez le contenu de vos anciens fichiers et collez-le dans les nouveaux fichiers Engagement.</span><span class="sxs-lookup"><span data-stu-id="964d1-129">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="964d1-130">Notez que les fichiers xaml et cs doivent être mis à jour.</span><span class="sxs-lookup"><span data-stu-id="964d1-130">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="964d1-131">Une fois ces étapes terminées, il vous suffit de remplacer les anciennes références Capptain par les nouvelles références Engagement.</span><span class="sxs-lookup"><span data-stu-id="964d1-131">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="964d1-132">Tous les espaces de noms Capptain doivent être mis à jour.</span><span class="sxs-lookup"><span data-stu-id="964d1-132">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="964d1-133">Avant la migration :</span><span class="sxs-lookup"><span data-stu-id="964d1-133">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="964d1-134">Après la migration :</span><span class="sxs-lookup"><span data-stu-id="964d1-134">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="964d1-135">Toutes les classes Capptain qui contiennent « Capptain » doivent contenir « Engagement ».</span><span class="sxs-lookup"><span data-stu-id="964d1-135">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="964d1-136">Avant la migration :</span><span class="sxs-lookup"><span data-stu-id="964d1-136">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="964d1-137">Après la migration :</span><span class="sxs-lookup"><span data-stu-id="964d1-137">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="964d1-138">Pour les fichiers xaml, les attributs et les espaces de noms Capptain changent également.</span><span class="sxs-lookup"><span data-stu-id="964d1-138">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="964d1-139">Avant la migration :</span><span class="sxs-lookup"><span data-stu-id="964d1-139">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="964d1-140">Après la migration :</span><span class="sxs-lookup"><span data-stu-id="964d1-140">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="964d1-141">Notez que les autres ressources, comme les images Capptain, ont aussi été renommées afin d'utiliser « Engagement ».</span><span class="sxs-lookup"><span data-stu-id="964d1-141">For the other resources like Capptain pictures, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="964d1-142">ID de l'application / clé SDK</span><span class="sxs-lookup"><span data-stu-id="964d1-142">Application ID / SDK Key</span></span>
<span data-ttu-id="964d1-143">Engagement utilise une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="964d1-143">Engagement uses a connection string.</span></span> <span data-ttu-id="964d1-144">Il est inutile de spécifier un ID d'application et une clé SDK avec Mobile Engagement. Il suffit de spécifier une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="964d1-144">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="964d1-145">Vous pouvez la configurer dans votre fichier EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="964d1-145">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="964d1-146">La configuration d'Engagement peut être définie dans le fichier `Resources\EngagementConfiguration.xml` de votre projet.</span><span class="sxs-lookup"><span data-stu-id="964d1-146">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="964d1-147">Modifiez ce fichier pour spécifier :</span><span class="sxs-lookup"><span data-stu-id="964d1-147">Edit this file to specify:</span></span>

* <span data-ttu-id="964d1-148">Votre chaîne de connexion d'application entre les balises `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="964d1-148">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="964d1-149">Si vous souhaitez plutôt la spécifier au moment de l'exécution, vous pouvez appeler la méthode suivante avant l'initialisation de l'agent Engagement :</span><span class="sxs-lookup"><span data-stu-id="964d1-149">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Initialize Engagement angent with above configuration. */
        EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="964d1-150">La chaîne de connexion de votre application est affichée sur le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="964d1-150">The connection string for your application is displayed in the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="964d1-151">Changement de noms d'éléments</span><span class="sxs-lookup"><span data-stu-id="964d1-151">Items name change</span></span>
<span data-ttu-id="964d1-152">Tous les éléments nommés *capptain* ont été renommés *engagement*.</span><span class="sxs-lookup"><span data-stu-id="964d1-152">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="964d1-153">De même pour *Capptain* (renommés *Engagement*).</span><span class="sxs-lookup"><span data-stu-id="964d1-153">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="964d1-154">Exemples d'éléments Capptain couramment utilisés :</span><span class="sxs-lookup"><span data-stu-id="964d1-154">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="964d1-155">CapptainConfiguration se nomme maintenant EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="964d1-155">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="964d1-156">CapptainAgent se nomme maintenant EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="964d1-156">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="964d1-157">CapptainReach se nomme maintenant EngagementReach</span><span class="sxs-lookup"><span data-stu-id="964d1-157">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="964d1-158">CapptainHttpConfig se nomme maintenant EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="964d1-158">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="964d1-159">GetCapptainPageName se nomme maintenant GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="964d1-159">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="964d1-160">Notez que ce changement affecte également les méthodes substituées.</span><span class="sxs-lookup"><span data-stu-id="964d1-160">Note that rename also affects overridden methods.</span></span>

