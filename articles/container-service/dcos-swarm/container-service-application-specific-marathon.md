---
title: "aaaApplication ou spécifiques à l’utilisateur Marathon service | Documents Microsoft"
description: "Créer un service Marathon lié à une application ou à un utilisateur donnés"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Conteneurs, Marathon, micro-services, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 1e6f69ed64e113a3a059788a71ddb57b6d3ad8da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="581a6-104">Créer un service Marathon lié à une application ou à un utilisateur donnés</span><span class="sxs-lookup"><span data-stu-id="581a6-104">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="581a6-105">Azure Container Service fournit un ensemble de serveurs maîtres sur lesquels nous préconfigurons Apache Mesos et Marathon.</span><span class="sxs-lookup"><span data-stu-id="581a6-105">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span></span> <span data-ttu-id="581a6-106">Ceux-ci peuvent être utilisé tooorchestrate vos applications sur un cluster de hello, mais elle ne meilleures pas toouse hello serveurs maîtres à cet effet.</span><span class="sxs-lookup"><span data-stu-id="581a6-106">These can be used tooorchestrate your applications on hello cluster, but it's best not toouse hello master servers for this purpose.</span></span> <span data-ttu-id="581a6-107">Par exemple, configuration hello de Marathon un ajustement nécessite la connexion à des serveurs maîtres hello eux-mêmes et apporter des modifications--ce encourage les serveurs maîtres uniques qui sont un peu différente de hello standard et toobe besoin s’et managé indépendamment.</span><span class="sxs-lookup"><span data-stu-id="581a6-107">For example, tweaking hello configuration of Marathon requires logging into hello master servers themselves and making changes--this encourages unique master servers that are a little different from hello standard and need toobe cared for and managed independently.</span></span> <span data-ttu-id="581a6-108">En outre, configuration hello requise par une équipe peut-être pas une configuration optimale hello pour une autre équipe.</span><span class="sxs-lookup"><span data-stu-id="581a6-108">Additionally, hello configuration required by one team might not be hello optimal configuration for another team.</span></span>

<span data-ttu-id="581a6-109">Dans cet article, nous expliquerons comment tooadd un service Marathon application ou spécifiques à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="581a6-109">In this article, we'll explain how tooadd an application or user-specific Marathon service.</span></span>

<span data-ttu-id="581a6-110">Étant donné que ce service appartiendra tooa seul utilisateur ou l’équipe, ils sont tooconfigure libre de toute manière qu’ils souhaitent.</span><span class="sxs-lookup"><span data-stu-id="581a6-110">Because this service will belong tooa single user or team, they are free tooconfigure it in any way that they desire.</span></span> <span data-ttu-id="581a6-111">En outre, Service de conteneur Azure garantit que le service de hello continue toorun.</span><span class="sxs-lookup"><span data-stu-id="581a6-111">Also, Azure Container Service will ensure that hello service continues toorun.</span></span> <span data-ttu-id="581a6-112">Si le service de hello échoue, le Service de conteneur Azure redémarre pour vous.</span><span class="sxs-lookup"><span data-stu-id="581a6-112">If hello service fails, Azure Container Service will restart it for you.</span></span> <span data-ttu-id="581a6-113">La plupart du temps de hello vous ne même remarquer qu’elle avait le temps d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="581a6-113">Most of hello time you won't even notice it had downtime.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="581a6-114">Composants requis</span><span class="sxs-lookup"><span data-stu-id="581a6-114">Prerequisites</span></span>
<span data-ttu-id="581a6-115">[Déployer une instance de Service de conteneur Azure](container-service-deployment.md) avec orchestrator le type de contrôleur de domaine/système d’exploitation et [vous assurer que votre client peut se connecter tooyour cluster](../container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="581a6-115">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect tooyour cluster](../container-service-connect.md).</span></span> <span data-ttu-id="581a6-116">En outre, hello comme suit.</span><span class="sxs-lookup"><span data-stu-id="581a6-116">Also, do hello following steps.</span></span>

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="581a6-117">Créer un service Marathon lié à une application ou à un utilisateur donnés</span><span class="sxs-lookup"><span data-stu-id="581a6-117">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="581a6-118">Commencez par créer un fichier de configuration JSON qui définit le nom de hello du service de l’application hello que vous souhaitez toocreate.</span><span class="sxs-lookup"><span data-stu-id="581a6-118">Begin by creating a JSON configuration file that defines hello name of hello application service that you want toocreate.</span></span> <span data-ttu-id="581a6-119">Ici, nous utilisons `marathon-alice` en tant que nom d’infrastructure hello.</span><span class="sxs-lookup"><span data-stu-id="581a6-119">Here we use `marathon-alice` as hello framework name.</span></span> <span data-ttu-id="581a6-120">Enregistrer le fichier de hello comme `marathon-alice.json`:</span><span class="sxs-lookup"><span data-stu-id="581a6-120">Save hello file as something like `marathon-alice.json`:</span></span>

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

<span data-ttu-id="581a6-121">Ensuite, utiliser hello CLI de contrôleur de domaine/système d’exploitation tooinstall hello Marathon instance avec les options hello qui sont définies dans votre fichier de configuration :</span><span class="sxs-lookup"><span data-stu-id="581a6-121">Next, use hello DC/OS CLI tooinstall hello Marathon instance with hello options that are set in your configuration file:</span></span>

```bash
dcos package install --options=marathon-alice.json marathon
```

<span data-ttu-id="581a6-122">Vous devez maintenant voir votre `marathon-alice` service en cours d’exécution dans l’onglet Services de hello de votre interface utilisateur de contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="581a6-122">You should now see your `marathon-alice` service running in hello Services tab of your DC/OS UI.</span></span> <span data-ttu-id="581a6-123">Hello l’interface utilisateur sera `http://<hostname>/service/marathon-alice/` si vous souhaitez tooaccess directement.</span><span class="sxs-lookup"><span data-stu-id="581a6-123">hello UI will be `http://<hostname>/service/marathon-alice/` if you want tooaccess it directly.</span></span>

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a><span data-ttu-id="581a6-124">Définir hello CLI de contrôleur de domaine/système d’exploitation tooaccess service de hello</span><span class="sxs-lookup"><span data-stu-id="581a6-124">Set hello DC/OS CLI tooaccess hello service</span></span>
<span data-ttu-id="581a6-125">Vous pouvez éventuellement configurer votre tooaccess CLI de contrôleur de domaine/système d’exploitation ce service en définissant un hello `marathon.url` propriété toopoint toohello `marathon-alice` de l’instance comme suit :</span><span class="sxs-lookup"><span data-stu-id="581a6-125">You can optionally configure your DC/OS CLI tooaccess this new service by setting hello `marathon.url` property toopoint toohello `marathon-alice` instance as follows:</span></span>

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

<span data-ttu-id="581a6-126">Vous pouvez vérifier quelle instance de Marathon utilisée par votre CLI contre hello `dcos config show` commande.</span><span class="sxs-lookup"><span data-stu-id="581a6-126">You can verify which instance of Marathon that your CLI is working against with hello `dcos config show` command.</span></span> <span data-ttu-id="581a6-127">Vous pouvez rétablir toousing votre service Marathon maître avec la commande hello `dcos config unset marathon.url`.</span><span class="sxs-lookup"><span data-stu-id="581a6-127">You can revert toousing your master Marathon service with hello command `dcos config unset marathon.url`.</span></span>

