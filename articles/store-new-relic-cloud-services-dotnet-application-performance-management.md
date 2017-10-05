---
title: Utilisation de New Relic avec Azure | Microsoft Docs
description: "Apprenez à utiliser le service New Relic pour gérer et surveiller votre application Azure."
services: 
documentationcenter: .net
author: nickfloyd
manager: timlt
editor: 
ms.assetid: b01011be-c344-4e33-987d-c93dac1971fb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2016
ms.author: nickfloyd@newrelic.com
ms.openlocfilehash: f4f13c909a6ff640d403f5264004176c087925dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="new-relic-application-performance-management-on-azure"></a><span data-ttu-id="3cff1-103">Gestion des performances des applications New Relic sur Azure</span><span class="sxs-lookup"><span data-stu-id="3cff1-103">New Relic Application Performance Management on Azure</span></span>
<span data-ttu-id="3cff1-104">Vous pouvez ajouter la surveillance des performances New Relic de pointe à vos applications hébergées sur Azure.</span><span class="sxs-lookup"><span data-stu-id="3cff1-104">You can add New Relic's world-class performance monitoring to your Azure hosted applications.</span></span> <span data-ttu-id="3cff1-105">En plus des fonctionnalités complètes pour la surveillance, la résolution des problèmes et le réglage de vos applications Azure, vous pouvez également bénéficier de prix réduits pour les produits New Relic à l’aide d’Azure.</span><span class="sxs-lookup"><span data-stu-id="3cff1-105">Along with comprehensive capabilities for monitoring, troubleshooting, and tuning your Azure apps, you are also eligible for a discounted price for New Relic products by using Azure.</span></span>

## <a name="what-is-new-relic"></a><span data-ttu-id="3cff1-106">Présentation de New Relic</span><span class="sxs-lookup"><span data-stu-id="3cff1-106">What is New Relic?</span></span>
<span data-ttu-id="3cff1-107">Avec les [produits New Relic](https://newrelic.com/products), vous pouvez résoudre les erreurs d’application, anticiper les problèmes potentiels et comprendre les performances de votre environnement tout entier.</span><span class="sxs-lookup"><span data-stu-id="3cff1-107">With [New Relic products](https://newrelic.com/products), you can solve app errors, stay ahead of potential issues, and understand the performance of your entire environment.</span></span> <span data-ttu-id="3cff1-108">Ce produit est conçu pour vous permettre de gagner du temps lors de l'identification et du diagnostic des problèmes de performances et il vous donne les informations requises pour résoudre ces problèmes en un instant.</span><span class="sxs-lookup"><span data-stu-id="3cff1-108">It is designed to save you time when identifying and diagnosing performance issues, and it puts the information you need to solve these issues at your fingertips.</span></span>

<span data-ttu-id="3cff1-109">New Relic effectue le suivi de la durée du chargement et du débit de vos transactions Web, à la fois à partir du serveur et des navigateurs des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="3cff1-109">New Relic tracks the load time and throughput for your web transactions, both from the server and your users' browsers.</span></span> <span data-ttu-id="3cff1-110">Il indique le temps que vous passez dans la base de données, analyse les requêtes lentes et les requêtes Web, fournit une surveillance et des alertes en matière de temps d'activité, effectue le suivi des exceptions d'application et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="3cff1-110">It shows how much time you spend in the database, analyzes slow queries and web requests, provides uptime monitoring and alerting, tracks application exceptions, and a whole lot more.</span></span> 

## <a name="special-pricing"></a><span data-ttu-id="3cff1-111">Tarification spéciale</span><span class="sxs-lookup"><span data-stu-id="3cff1-111">Special pricing</span></span>
<span data-ttu-id="3cff1-112">New Relic Standard est gratuit pour les utilisateurs d'Azure.</span><span class="sxs-lookup"><span data-stu-id="3cff1-112">New Relic Standard is free to Azure users.</span></span> <span data-ttu-id="3cff1-113">New Relic Pro est fourni en fonction de la taille d’instance d’Azure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="3cff1-113">New Relic Pro is offered based on instance size for Azure Cloud Services.</span></span> <span data-ttu-id="3cff1-114">Pour plus d’informations de tarification, consultez la [page de New Relic](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) dans le Azure Marketplace ou le contact New Relic (sales@newrelic.com) pour la tarification de niveau entreprise.</span><span class="sxs-lookup"><span data-stu-id="3cff1-114">For pricing information, see the [New Relic page](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in the Azure Marketplace or contact New Relic (sales@newrelic.com) for enterprise-level pricing.</span></span>

<span data-ttu-id="3cff1-115">Les clients d’Azure reçoivent un abonnement de deux semaines gratuit à New Relic Pro lorsqu’ils déploient l’agent New Relic.</span><span class="sxs-lookup"><span data-stu-id="3cff1-115">Azure customers receive a two week trial subscription of New Relic Pro when they deploy the New Relic agent.</span></span>

## <a name="sign-up-for-new-relic-using-the-azure-store"></a><span data-ttu-id="3cff1-116">Inscription à New Relic à l'aide de l'Azure Store</span><span class="sxs-lookup"><span data-stu-id="3cff1-116">Sign up for New Relic using the Azure Store</span></span>
<span data-ttu-id="3cff1-117">New Relic s'intègre en toute transparence aux rôles Web et de travail Azure.</span><span class="sxs-lookup"><span data-stu-id="3cff1-117">New Relic integrates seamlessly with Azure Web Roles and Worker roles.</span></span> <span data-ttu-id="3cff1-118">Vous pouvez vous inscrire rapidement et facilement à New Relic directement depuis l’Azure Store.</span><span class="sxs-lookup"><span data-stu-id="3cff1-118">You can quickly and easily sign up for New Relic directly from the Azure Store.</span></span> <span data-ttu-id="3cff1-119">Pour obtenir des instructions, consultez les [instructions d’inscription Azure Store](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) de New Relic.</span><span class="sxs-lookup"><span data-stu-id="3cff1-119">For instructions, see the [Azure store sign-up instructions](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) from New Relic.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="3cff1-120">Affichage de vos données</span><span class="sxs-lookup"><span data-stu-id="3cff1-120">View your data</span></span>
<span data-ttu-id="3cff1-121">Une fois inscrit, vous pouvez tirer parti des incroyables fonctions de surveillance des applications et d’analyses pilotées par les données de New Relic.</span><span class="sxs-lookup"><span data-stu-id="3cff1-121">Once you've signed up, you can take advantage of New Relic's amazing application monitoring and data-driven analysis.</span></span> <span data-ttu-id="3cff1-122">Pour vérifier les performances de votre application dans New Relic :</span><span class="sxs-lookup"><span data-stu-id="3cff1-122">To check your app's performance in New Relic:</span></span>

1. <span data-ttu-id="3cff1-123">Dans le portail Azure, sélectionnez Gérer.</span><span class="sxs-lookup"><span data-stu-id="3cff1-123">From the Azure Portal, select Manage.</span></span>
2. <span data-ttu-id="3cff1-124">Connectez-vous avec l'adresse électronique et le mot de passe de votre compte New Relic.</span><span class="sxs-lookup"><span data-stu-id="3cff1-124">Sign in with your New Relic account email and password.</span></span>
3. <span data-ttu-id="3cff1-125">Sélectionnez votre application à partir de l’index de l’application pour afficher toutes les données de votre application dans la [page de vue d’ensemble APM](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span><span class="sxs-lookup"><span data-stu-id="3cff1-125">Select your app from the Application index to view all your app's data in the [APM overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span></span>

## <a name="using-new-relic-with-azure"></a><span data-ttu-id="3cff1-126">Utilisation de New Relic avec Azure</span><span class="sxs-lookup"><span data-stu-id="3cff1-126">Using New Relic with Azure</span></span>
<span data-ttu-id="3cff1-127">Pour plus d’informations sur l’utilisation de New Relic et d’Azure, consultez le [site de documentation de New Relic](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), notamment :</span><span class="sxs-lookup"><span data-stu-id="3cff1-127">For more information about using New Relic and Azure, see [New Relic's Documentation site](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), including:</span></span> 

* [<span data-ttu-id="3cff1-128">New Relic for .NET (New Relic pour .NET)</span><span class="sxs-lookup"><span data-stu-id="3cff1-128">New Relic for .NET</span></span>](https://docs.newrelic.com/docs/agents/net-agent/getting-started/new-relic-net)
* [<span data-ttu-id="3cff1-129">Instrument a .NET Worker Role on Azure Cloud service (Instrumenter un rôle de travail .NET sur le service cloud Azure)</span><span class="sxs-lookup"><span data-stu-id="3cff1-129">Instrument a .NET Worker Role on Azure Cloud service</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/instrument-net-worker-role-azure-cloud-service)
* [<span data-ttu-id="3cff1-130">New Relic for the Microsoft Azure Cloud platform (New Relic pour la plateforme cloud Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="3cff1-130">New Relic for the Microsoft Azure Cloud platform</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services)
* [<span data-ttu-id="3cff1-131">New Relic for the Microsoft Azure App Services (New Relic pour Microsoft Azure App Services)</span><span class="sxs-lookup"><span data-stu-id="3cff1-131">New Relic for the Microsoft Azure App Services</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-portal)
* [<span data-ttu-id="3cff1-132">New Relic/Azure troubleshooting (Résolution des problèmes New Relic/Azure)</span><span class="sxs-lookup"><span data-stu-id="3cff1-132">New Relic/Azure troubleshooting</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-troubleshooting)

