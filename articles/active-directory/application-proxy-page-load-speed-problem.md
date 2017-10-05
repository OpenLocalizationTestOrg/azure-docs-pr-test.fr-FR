---
title: "Le chargement d’une application Proxy d’application prend trop de temps | Microsoft Docs"
description: "Résolution des problèmes de performances associés au chargement de page avec le Proxy d’application Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: ce462c90746e6af0dc201686557121665b82b93d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="an-application-proxy-application-takes-too-long-to-load"></a><span data-ttu-id="07884-103">Le chargement d’une application Proxy d’application prend trop de temps</span><span class="sxs-lookup"><span data-stu-id="07884-103">An Application Proxy application takes too long to load</span></span>

<span data-ttu-id="07884-104">Cet article vous aide à comprendre pourquoi le chargement d’une application Proxy d’application peut prendre beaucoup de temps. Plusieurs solutions sont abordées pour résoudre ce problème.</span><span class="sxs-lookup"><span data-stu-id="07884-104">This article help you to understand why an Azure AD Application Proxy application may take a long time to load, and what you can do to resolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="07884-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="07884-105">Overview</span></span>
<span data-ttu-id="07884-106">Si vos applications fonctionnent mais que vous constatez un temps de latence important, vous pouvez tenter d’apporter quelques ajustements mineurs à votre topologie de réseau pour améliorer la vitesse.</span><span class="sxs-lookup"><span data-stu-id="07884-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider to improve the speed.</span></span> <span data-ttu-id="07884-107">Pour une évaluation des différentes topologies, consultez le [document des considérations sur la topologie du réseau](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span><span class="sxs-lookup"><span data-stu-id="07884-107">For an evaluation of different topologies, see the [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="07884-108">Si ces considérations ne vous aident pas à résoudre le problème, nous n’avons malheureusement pas d’autres recommandations relatives au réglage des performances.</span><span class="sxs-lookup"><span data-stu-id="07884-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="07884-109">À mesure que le service Proxy d’application s’étend à des centres de données qui peuvent être plus proches de vous, il est possible que vous constatiez directement une amélioration de la latence.</span><span class="sxs-lookup"><span data-stu-id="07884-109">As the Application Proxy service expands to more data centers that may be closer to you, you may start to see improved latency directly.</span></span> <span data-ttu-id="07884-110">Pour afficher la liste complète des centres de données Azure, consultez la [page de test de la latence](http://www.azurespeed.com/Azure/Latency).</span><span class="sxs-lookup"><span data-stu-id="07884-110">To see the full list of Azure data centers, you can see the [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="07884-111">Pour trouver les centres de données avec le service Proxy d’application, utilisez l’outil [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span><span class="sxs-lookup"><span data-stu-id="07884-111">The data centers with the Application Proxy service can be found with the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="07884-112">Commentaires sur les emplacements des centres de données du Proxy d’application</span><span class="sxs-lookup"><span data-stu-id="07884-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="07884-113">Même si certains centres de données Azure n’incluent pas encore le Proxy d’application, ils peuvent néanmoins améliorer considérablement vos temps de latence.</span><span class="sxs-lookup"><span data-stu-id="07884-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead to a great latency improvement for you.</span></span> <span data-ttu-id="07884-114">Envoyez vos commentaires sur l’emplacement du centre de données à <aadapfeedback@microsoft.com> pour que nous puissions en tenir compte dans nos futurs développements.</span><span class="sxs-lookup"><span data-stu-id="07884-114">The data center location at <aadapfeedback@microsoft.com> so we can use your feedback to plan as we expand.</span></span>

<span data-ttu-id="07884-115">Nous travaillons sur des fonctionnalités supplémentaires visant à améliorer la latence pour les locataires qui constatent actuellement des temps de latence longs. Nous ne manquerons pas de partager avec vous la documentation dès qu’elle sera disponible.</span><span class="sxs-lookup"><span data-stu-id="07884-115">We are working on some additional capabilities that help improve the latency for tenants that currently see long latencies, and be sure to share documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07884-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="07884-116">Next steps</span></span>
[<span data-ttu-id="07884-117">Travailler avec des serveurs proxy locaux existants</span><span class="sxs-lookup"><span data-stu-id="07884-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
