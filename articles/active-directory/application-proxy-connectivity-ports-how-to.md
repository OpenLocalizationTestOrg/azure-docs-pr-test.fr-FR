---
title: "ports de pare-feu aaaHow tooopen hello requises pour une application de Proxy d’Application | Documents Microsoft"
description: "Découvrez quels tooopen ports pour hello AD Azure Proxy d’Application toowork correctement"
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
ms.openlocfilehash: cdc7badb7c15591689a3bfd6bb26da182b00fb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-hello-firewall-ports-required-for-an-application-proxy-application"></a><span data-ttu-id="53d68-103">Comment tooopen hello ports de pare-feu requises pour une application de Proxy d’Application</span><span class="sxs-lookup"><span data-stu-id="53d68-103">How tooopen hello firewall ports required for an Application Proxy application</span></span>

<span data-ttu-id="53d68-104">toosee une liste complète des ports de hello requis et de la fonction hello de chaque port, voir la section de configuration requise de hello Hello [documentation de Proxy d’Application](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span><span class="sxs-lookup"><span data-stu-id="53d68-104">toosee a full list of hello required ports and hello function of each port, see hello prerequisites section of hello [Application Proxy documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable).</span></span> <span data-ttu-id="53d68-105">Le proxy d’application utilise uniquement des ports de sortie.</span><span class="sxs-lookup"><span data-stu-id="53d68-105">note that Application Proxy only uses outbound ports.</span></span>

<span data-ttu-id="53d68-106">Vous pouvez également vérifier si vous avez tous hello requis ports ouverts en ouvrant le hello [connecteur Ports Test outil](https://aadap-portcheck.connectorporttest.msappproxy.net/) à partir de votre réseau local.</span><span class="sxs-lookup"><span data-stu-id="53d68-106">You can also check whether you have all hello required ports open by opening hello [Connector Ports Test Tool](https://aadap-portcheck.connectorporttest.msappproxy.net/) from your on-prem network.</span></span> <span data-ttu-id="53d68-107">Un nombre plus élevé de coches vertes signifie une résilience accrue.</span><span class="sxs-lookup"><span data-stu-id="53d68-107">More green checkmarks means greater resiliency.</span></span> 

## <a name="app-proxy-regions"></a><span data-ttu-id="53d68-108">Régions du proxy d’application</span><span class="sxs-lookup"><span data-stu-id="53d68-108">App Proxy regions</span></span>

<span data-ttu-id="53d68-109">Nous travaillons sur une méthode toolet connait de ces régions doit toobe verte pour vous.</span><span class="sxs-lookup"><span data-stu-id="53d68-109">We are working on a way toolet you know which of these regions needs toobe green for you.</span></span> <span data-ttu-id="53d68-110">Pour l’instant, assurez-vous que toutes le sont.</span><span class="sxs-lookup"><span data-stu-id="53d68-110">For now, make sure they all are.</span></span> <span data-ttu-id="53d68-111">La région États-Unis du Centre est également requise, quelle que soit la région où vous vous trouvez.</span><span class="sxs-lookup"><span data-stu-id="53d68-111">Central US is also required regardless of which region you are in.</span></span>

<span data-ttu-id="53d68-112">toomake vraiment hello outil donne hello de bons résultats, veillez à :</span><span class="sxs-lookup"><span data-stu-id="53d68-112">toomake sure hello tool gives you hello right results, be sure to:</span></span>

-   <span data-ttu-id="53d68-113">Outil hello ouvert sur un navigateur à partir du serveur hello où vous avez installé le connecteur de hello.</span><span class="sxs-lookup"><span data-stu-id="53d68-113">Open hello tool on a browser from hello server where you have installed hello Connector.</span></span>

-   <span data-ttu-id="53d68-114">Assurez-vous que les serveurs proxy ou pare-feu tooyour applicable connecteur sont également appliquées toothis page.</span><span class="sxs-lookup"><span data-stu-id="53d68-114">Ensure that any proxies or firewalls applicable tooyour Connector are also applied toothis page.</span></span> <span data-ttu-id="53d68-115">Cela est possible dans Internet Explorer en accédant trop**paramètres**  - &gt; **Options Internet**  - &gt; **connexions**  - &gt; **Paramètres Lan**.</span><span class="sxs-lookup"><span data-stu-id="53d68-115">This can be done in Internet Explorer by going too**Settings** -&gt; **Internet Options** -&gt; **Connections** -&gt; **Lan Settings**.</span></span> <span data-ttu-id="53d68-116">Dans cette page, vous consultez le champ hello « Utiliser un Proxy Server pour votre réseau local ».</span><span class="sxs-lookup"><span data-stu-id="53d68-116">On this page, you see hello field “Use a Proxy Server for your LAN”.</span></span> <span data-ttu-id="53d68-117">Activez cette case et placez l’adresse du proxy hello dans le champ « Address » de hello.</span><span class="sxs-lookup"><span data-stu-id="53d68-117">Select this box, and put hello proxy address into hello “Address” field.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53d68-118">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="53d68-118">Next steps</span></span>
[<span data-ttu-id="53d68-119">Présentation des connecteurs de proxy d’application Azure AD</span><span class="sxs-lookup"><span data-stu-id="53d68-119">Understand Azure AD Application Proxy connectors</span></span>](application-proxy-understand-connectors.md)
