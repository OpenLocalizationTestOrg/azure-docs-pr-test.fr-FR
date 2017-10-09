---
title: aaaUsing New Relic avec Azure | Documents Microsoft
description: "Découvrez comment toouse hello New Relic service toomanage et surveiller votre application Windows Azure."
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
ms.openlocfilehash: 81e5f1b694264e3586ac75d40edd8afe185493d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="new-relic-application-performance-management-on-azure"></a><span data-ttu-id="0e852-103">Gestion des performances des applications New Relic sur Azure</span><span class="sxs-lookup"><span data-stu-id="0e852-103">New Relic Application Performance Management on Azure</span></span>
<span data-ttu-id="0e852-104">Vous pouvez ajouter des performances de premier ordre de New Relic analyse tooyour Azure applications hébergées.</span><span class="sxs-lookup"><span data-stu-id="0e852-104">You can add New Relic's world-class performance monitoring tooyour Azure hosted applications.</span></span> <span data-ttu-id="0e852-105">En plus des fonctionnalités complètes pour la surveillance, la résolution des problèmes et le réglage de vos applications Azure, vous pouvez également bénéficier de prix réduits pour les produits New Relic à l’aide d’Azure.</span><span class="sxs-lookup"><span data-stu-id="0e852-105">Along with comprehensive capabilities for monitoring, troubleshooting, and tuning your Azure apps, you are also eligible for a discounted price for New Relic products by using Azure.</span></span>

## <a name="what-is-new-relic"></a><span data-ttu-id="0e852-106">Présentation de New Relic</span><span class="sxs-lookup"><span data-stu-id="0e852-106">What is New Relic?</span></span>
<span data-ttu-id="0e852-107">Avec [produits de New Relic](https://newrelic.com/products), vous pouvez résoudre les erreurs d’application, maîtriser les problèmes potentiels et comprendre les performances de hello de tout votre environnement.</span><span class="sxs-lookup"><span data-stu-id="0e852-107">With [New Relic products](https://newrelic.com/products), you can solve app errors, stay ahead of potential issues, and understand hello performance of your entire environment.</span></span> <span data-ttu-id="0e852-108">Il est conçu toosave lors de l’identification et de diagnostiquer les problèmes de performances du temps, et qu’il place hello informations toosolve ces problèmes à portée de main.</span><span class="sxs-lookup"><span data-stu-id="0e852-108">It is designed toosave you time when identifying and diagnosing performance issues, and it puts hello information you need toosolve these issues at your fingertips.</span></span>

<span data-ttu-id="0e852-109">Nouvelle hello de pistes Relic charger le temps et le débit pour vos transactions web, à la fois de serveur de hello et les navigateurs de vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0e852-109">New Relic tracks hello load time and throughput for your web transactions, both from hello server and your users' browsers.</span></span> <span data-ttu-id="0e852-110">Il montre comment votre temps dans la base de données hello, analyse les requêtes lentes et fournit des demandes web, analyse des temps de fonctionnement et d’alerte, les exceptions d’application assure le suivi et beaucoup plus.</span><span class="sxs-lookup"><span data-stu-id="0e852-110">It shows how much time you spend in hello database, analyzes slow queries and web requests, provides uptime monitoring and alerting, tracks application exceptions, and a whole lot more.</span></span> 

## <a name="special-pricing"></a><span data-ttu-id="0e852-111">Tarification spéciale</span><span class="sxs-lookup"><span data-stu-id="0e852-111">Special pricing</span></span>
<span data-ttu-id="0e852-112">Nouvelle Relic Standard est libre tooAzure utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0e852-112">New Relic Standard is free tooAzure users.</span></span> <span data-ttu-id="0e852-113">New Relic Pro est fourni en fonction de la taille d’instance d’Azure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="0e852-113">New Relic Pro is offered based on instance size for Azure Cloud Services.</span></span> <span data-ttu-id="0e852-114">Pour plus d’informations de tarification, consultez hello [page de New Relic](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) dans hello Azure Marketplace ou contactez New Relic (sales@newrelic.com) pour la tarification de niveau entreprise.</span><span class="sxs-lookup"><span data-stu-id="0e852-114">For pricing information, see hello [New Relic page](https://azure.microsoft.com/marketplace/partners/newrelic/newrelic/) in hello Azure Marketplace or contact New Relic (sales@newrelic.com) for enterprise-level pricing.</span></span>

<span data-ttu-id="0e852-115">Les clients Azure recevoir un abonnement d’évaluation de deux semaines de nouveau Relic Pro lorsqu’ils déploient l’agent de New Relic hello.</span><span class="sxs-lookup"><span data-stu-id="0e852-115">Azure customers receive a two week trial subscription of New Relic Pro when they deploy hello New Relic agent.</span></span>

## <a name="sign-up-for-new-relic-using-hello-azure-store"></a><span data-ttu-id="0e852-116">S’inscrire à New Relic à l’aide de hello Azure Store</span><span class="sxs-lookup"><span data-stu-id="0e852-116">Sign up for New Relic using hello Azure Store</span></span>
<span data-ttu-id="0e852-117">New Relic s'intègre en toute transparence aux rôles Web et de travail Azure.</span><span class="sxs-lookup"><span data-stu-id="0e852-117">New Relic integrates seamlessly with Azure Web Roles and Worker roles.</span></span> <span data-ttu-id="0e852-118">Vous pouvez rapidement et facilement s’inscrire pour New Relic directement à partir de hello magasin Azure.</span><span class="sxs-lookup"><span data-stu-id="0e852-118">You can quickly and easily sign up for New Relic directly from hello Azure Store.</span></span> <span data-ttu-id="0e852-119">Pour obtenir des instructions, consultez hello [Azure stocker les instructions d’inscription](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) à partir de New Relic.</span><span class="sxs-lookup"><span data-stu-id="0e852-119">For instructions, see hello [Azure store sign-up instructions](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services#signup) from New Relic.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="0e852-120">Affichage de vos données</span><span class="sxs-lookup"><span data-stu-id="0e852-120">View your data</span></span>
<span data-ttu-id="0e852-121">Une fois inscrit, vous pouvez tirer parti des incroyables fonctions de surveillance des applications et d’analyses pilotées par les données de New Relic.</span><span class="sxs-lookup"><span data-stu-id="0e852-121">Once you've signed up, you can take advantage of New Relic's amazing application monitoring and data-driven analysis.</span></span> <span data-ttu-id="0e852-122">toocheck les performances de votre application dans New Relic :</span><span class="sxs-lookup"><span data-stu-id="0e852-122">toocheck your app's performance in New Relic:</span></span>

1. <span data-ttu-id="0e852-123">À partir de hello portail Azure, sélectionnez Gérer.</span><span class="sxs-lookup"><span data-stu-id="0e852-123">From hello Azure Portal, select Manage.</span></span>
2. <span data-ttu-id="0e852-124">Connectez-vous avec l'adresse électronique et le mot de passe de votre compte New Relic.</span><span class="sxs-lookup"><span data-stu-id="0e852-124">Sign in with your New Relic account email and password.</span></span>
3. <span data-ttu-id="0e852-125">Sélectionnez votre application à partir de hello Application index tooview les données de tous les votre application Bonjour [page de vue d’ensemble APM](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span><span class="sxs-lookup"><span data-stu-id="0e852-125">Select your app from hello Application index tooview all your app's data in hello [APM overview page](https://docs.newrelic.com/docs/apm/applications-menu/monitoring/apm-overview-page).</span></span>

## <a name="using-new-relic-with-azure"></a><span data-ttu-id="0e852-126">Utilisation de New Relic avec Azure</span><span class="sxs-lookup"><span data-stu-id="0e852-126">Using New Relic with Azure</span></span>
<span data-ttu-id="0e852-127">Pour plus d’informations sur l’utilisation de New Relic et d’Azure, consultez le [site de documentation de New Relic](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), notamment :</span><span class="sxs-lookup"><span data-stu-id="0e852-127">For more information about using New Relic and Azure, see [New Relic's Documentation site](https://docs.newrelic.com/docs/agents/net-agent/azure-installation), including:</span></span> 

* [<span data-ttu-id="0e852-128">New Relic for .NET (New Relic pour .NET)</span><span class="sxs-lookup"><span data-stu-id="0e852-128">New Relic for .NET</span></span>](https://docs.newrelic.com/docs/agents/net-agent/getting-started/new-relic-net)
* [<span data-ttu-id="0e852-129">Instrument a .NET Worker Role on Azure Cloud service (Instrumenter un rôle de travail .NET sur le service cloud Azure)</span><span class="sxs-lookup"><span data-stu-id="0e852-129">Instrument a .NET Worker Role on Azure Cloud service</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/instrument-net-worker-role-azure-cloud-service)
* [<span data-ttu-id="0e852-130">New Relic pour la plateforme de Cloud de Microsoft Azure hello</span><span class="sxs-lookup"><span data-stu-id="0e852-130">New Relic for hello Microsoft Azure Cloud platform</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-cloud-services)
* [<span data-ttu-id="0e852-131">New Relic pour hello Services d’application Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0e852-131">New Relic for hello Microsoft Azure App Services</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-installation/azure-portal)
* [<span data-ttu-id="0e852-132">New Relic/Azure troubleshooting (Résolution des problèmes New Relic/Azure)</span><span class="sxs-lookup"><span data-stu-id="0e852-132">New Relic/Azure troubleshooting</span></span>](https://docs.newrelic.com/docs/agents/net-agent/azure-troubleshooting)

