---
title: "aaaAn application de Proxy d’Application prend trop de temps tooload | Documents Microsoft"
description: "Les problèmes de performances de chargement de page avec hello Proxy d’Application Azure AD"
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
ms.openlocfilehash: 4c7a51f96840966a1d88933fa4e30f39479d8a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="an-application-proxy-application-takes-too-long-tooload"></a><span data-ttu-id="f7dfa-103">Une application de Proxy d’Application prend trop de temps tooload</span><span class="sxs-lookup"><span data-stu-id="f7dfa-103">An Application Proxy application takes too long tooload</span></span>

<span data-ttu-id="f7dfa-104">Cet article vous a-t-il toounderstand pourquoi une application de Proxy d’Application Azure AD peut prendre un tooload beaucoup de temps et ce que vous pouvez effectuer tooresolve ce problème.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-104">This article help you toounderstand why an Azure AD Application Proxy application may take a long time tooload, and what you can do tooresolve this issue.</span></span>

## <a name="overview"></a><span data-ttu-id="f7dfa-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f7dfa-105">Overview</span></span>
<span data-ttu-id="f7dfa-106">Si vos applications fonctionnent, mais que vous consultez un temps de latence, il peut être quelques modifications mineures dans votre topologie de réseau que vous pouvez envisager la vitesse tooimprove hello.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-106">If your applications are working but you see a long latency, there may be some minor tweaks in your network topology that you can consider tooimprove hello speed.</span></span> <span data-ttu-id="f7dfa-107">Pour une évaluation des différentes topologies, consultez hello [document de considérations réseau](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span><span class="sxs-lookup"><span data-stu-id="f7dfa-107">For an evaluation of different topologies, see hello [network considerations document](https://docs.microsoft.com/azure/active-directory/application-proxy-network-topology-considerations).</span></span>

<span data-ttu-id="f7dfa-108">Si ces considérations ne vous aident pas à résoudre le problème, nous n’avons malheureusement pas d’autres recommandations relatives au réglage des performances.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-108">If those considerations don’t help, we unfortunately don’t have currently have further recommendations for performance tuning.</span></span> <span data-ttu-id="f7dfa-109">Comme hello service Proxy d’Application développe toomore des centres de données qui peuvent être tooyou plus proche, vous pouvez démarrer une latence toosee améliorée directement.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-109">As hello Application Proxy service expands toomore data centers that may be closer tooyou, you may start toosee improved latency directly.</span></span> <span data-ttu-id="f7dfa-110">les centres de toosee hello la liste complète des données Azure, vous pouvez voir hello [page de test de latence](http://www.azurespeed.com/Azure/Latency).</span><span class="sxs-lookup"><span data-stu-id="f7dfa-110">toosee hello full list of Azure data centers, you can see hello [latency test page](http://www.azurespeed.com/Azure/Latency).</span></span> 

<span data-ttu-id="f7dfa-111">Hello centres de données avec le service de Proxy d’Application hello sont accessibles par hello [outil de Test des Ports connecteur](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span><span class="sxs-lookup"><span data-stu-id="f7dfa-111">hello data centers with hello Application Proxy service can be found with hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/).</span></span> 

## <a name="feedback-on-application-proxy-data-center-locations"></a><span data-ttu-id="f7dfa-112">Commentaires sur les emplacements des centres de données du Proxy d’application</span><span class="sxs-lookup"><span data-stu-id="f7dfa-112">Feedback on Application Proxy data center locations</span></span> 
<span data-ttu-id="f7dfa-113">Il peut y avoir des centres de données Azure qui n’incluent pas encore le Proxy d’Application, mais risque d’entraîner l’amélioration latence élevée tooa pour vous.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-113">There may be Azure data centers that don’t as yet include Application Proxy but would lead tooa great latency improvement for you.</span></span> <span data-ttu-id="f7dfa-114">emplacement du centre de données de Hello < aadapfeedback@microsoft.com > afin de pouvoir utiliser votre tooplan de commentaires que nous allons développer.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-114">hello data center location at <aadapfeedback@microsoft.com> so we can use your feedback tooplan as we expand.</span></span>

<span data-ttu-id="f7dfa-115">Nous travaillons sur certaines des fonctionnalités supplémentaires qui aident à améliorer la latence des hello pour les clients que vous consultez actuellement les latences et que vous être sûr de documentation de tooshare une fois disponible.</span><span class="sxs-lookup"><span data-stu-id="f7dfa-115">We are working on some additional capabilities that help improve hello latency for tenants that currently see long latencies, and be sure tooshare documentation once available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7dfa-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f7dfa-116">Next steps</span></span>
[<span data-ttu-id="f7dfa-117">Travailler avec des serveurs proxy locaux existants</span><span class="sxs-lookup"><span data-stu-id="f7dfa-117">Work with existing on-premises proxy servers</span></span>](application-proxy-working-with-proxy-servers.md)
