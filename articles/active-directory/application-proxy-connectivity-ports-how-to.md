---
title: "Ouverture des ports de pare-feu requis pour une application de proxy d’application | Microsoft Docs"
description: "Découvrez quels ports ouvrir pour le bon fonctionnement du proxy d’application Azure AD"
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
ms.openlocfilehash: 8ecd6d7e666d362194126a4abba7a65f2c7b8b6b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-open-the-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="feaec-103">Ouverture des ports de pare-feu requis pour une application de proxy d’application</span><span class="sxs-lookup"><span data-stu-id="feaec-103">How to open the firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="feaec-104">Pour voir la liste complète des ports requis et la fonction de chaque port, consultez la section dédiée aux conditions préalables de la [documentation du proxy d’application](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span><span class="sxs-lookup"><span data-stu-id="feaec-104">To see a full list of the required ports and the function of each port, see the prerequisites section of the [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="feaec-105">Le proxy d’application utilise uniquement des ports de sortie.</span><span class="sxs-lookup"><span data-stu-id="feaec-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="feaec-106">Vous pouvez également vérifier si tous les ports requis sont ouverts par le biais de l’[outil de test des ports du connecteur](https://aadap-portcheck.connectorporttest.msappproxy.net/) à partir de votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="feaec-106">You can also check whether you have all the required ports open by opening the [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="feaec-107">Un nombre plus élevé de coches vertes signifie une résilience accrue.</span><span class="sxs-lookup"><span data-stu-id="feaec-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="feaec-108">Régions du proxy d’application</span><span class="sxs-lookup"><span data-stu-id="feaec-108">App Proxy regions</span></span>

<span data-ttu-id="feaec-109">Nous travaillons sur un moyen de vous informer des régions qui doivent vous apparaître en vert.</span><span class="sxs-lookup"><span data-stu-id="feaec-109">We are working on a way to let you know which of these regions needs to be green for you.</span></span> <span data-ttu-id="feaec-110">Pour l’instant, assurez-vous que toutes le sont.</span><span class="sxs-lookup"><span data-stu-id="feaec-110">For now, make sure they all are.</span></span> <span data-ttu-id="feaec-111">La région États-Unis du Centre est également requise, quelle que soit la région où vous vous trouvez.</span><span class="sxs-lookup"><span data-stu-id="feaec-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="feaec-112">Pour vous assurer que l’outil fournit des résultats corrects, veillez à :</span><span class="sxs-lookup"><span data-stu-id="feaec-112">To make sure the tool gives you the right results, be sure to:</span></span>

-   <span data-ttu-id="feaec-113">Ouvrir l’outil sur un navigateur à partir du serveur sur lequel vous avez installé le connecteur.</span><span class="sxs-lookup"><span data-stu-id="feaec-113">Open the tool on a browser from the server where you have installed the Connector.</span></span>

-   <span data-ttu-id="feaec-114">Vous assurer que les proxys ou pare-feu applicables à votre connecteur sont également appliqués à cette page.</span><span class="sxs-lookup"><span data-stu-id="feaec-114">Ensure that any proxies or firewalls applicable to your Connector are also applied to this page.</span></span> <span data-ttu-id="feaec-115">Cela peut être fait dans Internet Explorer. Pour cela, allez dans **Paramètres** -&gt; **Options Internet** -&gt; **Connexions** -&gt; **Paramètres de réseau local**.</span><span class="sxs-lookup"><span data-stu-id="feaec-115">This can be done in Internet Explorer by going to **Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="feaec-116">Cette page comporte le champ Utiliser un serveur proxy pour votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="feaec-116">On this page, you see the field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="feaec-117">Activez cette case et entrez l’adresse proxy dans le champ Adresse.</span><span class="sxs-lookup"><span data-stu-id="feaec-117">Select this box, and put the proxy address into the “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="feaec-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="feaec-118">Next steps</span></span>
[<span data-ttu-id="feaec-119">Présentation des connecteurs de proxy d’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="feaec-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
