---
title: "aaaCustomize Azure IoT Suite connecté fabrique | Documents Microsoft"
description: "Obtenir une description de l’interconnexion de comportement de hello toocustomize Hello fabrique de solution préconfigurée."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: c#
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 53f2fef7a76b5d8e6ad023945a7812dc7fabd12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-how-hello-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="d0a4c-103">Personnaliser l’interconnexion hello fabrique solution affiche les données à partir de vos serveurs OPC UA</span><span class="sxs-lookup"><span data-stu-id="d0a4c-103">Customize how hello connected factory solution displays data from your OPC UA servers</span></span>

## <a name="introduction"></a><span data-ttu-id="d0a4c-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="d0a4c-104">Introduction</span></span>

<span data-ttu-id="d0a4c-105">Hello fabrique connecté solution rassemble et affiche les données d’hello OPC UA serveurs connectés toohello solution.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-105">hello connected factory solution aggregates and displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="d0a4c-106">Vous pouvez parcourir et envoyer des commandes toohello OPC UA serveurs dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-106">You can browse and send commands toohello OPC UA servers in your solution.</span></span> <span data-ttu-id="d0a4c-107">Pour plus d’informations sur OPC UA, consultez hello [connecté fabrique FAQ](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="d0a4c-107">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

<span data-ttu-id="d0a4c-108">Les exemples de données agrégées en une solution de hello de hello l’efficacité des équipements globale (OEE) et les indicateurs de Performance clés (KPI) que vous pouvez afficher dans le tableau de bord hello à la fabrique de hello, des lignes et des niveaux de la station.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-108">Examples of aggregated data in hello solution include hello Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in hello dashboard at hello factory, line, and station levels.</span></span> <span data-ttu-id="d0a4c-109">Hello capture d’écran suivante affiche hello les valeurs OEE et d’indicateur de performance clé pour hello **Assembly** station sur **Production ligne 1**, Bonjour **Munich** usine :</span><span class="sxs-lookup"><span data-stu-id="d0a4c-109">hello following screenshot shows hello OEE and KPI values for hello **Assembly** station, on **Production line 1**, in hello **Munich** factory:</span></span>

![Exemple de valeurs OEE et l’indicateur de performance clé dans la solution de hello][img-oee-kpi]

<span data-ttu-id="d0a4c-111">permet de solution Hello vous tooview détaillée des informations à partir d’éléments de données spécifiques à partir de hello serveurs OPC UA, appelés *stations*.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-111">hello solution enables you tooview detailed information from specific data items from hello OPC UA servers, called *stations*.</span></span> <span data-ttu-id="d0a4c-112">Hello capture d’écran suivante montre les tracés de nombre hello des articles fabriqués à partir d’une station de travail spécifique :</span><span class="sxs-lookup"><span data-stu-id="d0a4c-112">hello following screenshot shows plots of hello number of manufactured items from a specific station:</span></span>

![Graphiques du nombre d’éléments fabriqués][img-manufactured-items]

<span data-ttu-id="d0a4c-114">Si vous cliquez sur un des graphiques de hello, vous pouvez explorer les données de hello à l’aide des temps série Insights (STI) :</span><span class="sxs-lookup"><span data-stu-id="d0a4c-114">If you click one of hello graphs, you can explore hello data further using Time Series Insights (TSI):</span></span>

![Explorer les données à l’aide de Time Series Insights][img-tsi]

<span data-ttu-id="d0a4c-116">Cet article explique :</span><span class="sxs-lookup"><span data-stu-id="d0a4c-116">This article describes:</span></span>

- <span data-ttu-id="d0a4c-117">Comment les données de salutation sont établie à toohello disponible différentes vues dans la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-117">How hello data is made available toohello various views in hello solution.</span></span>
- <span data-ttu-id="d0a4c-118">Comment vous pouvez personnaliser la solution de hello moyen hello affiche les données de hello.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-118">How you can customize hello way hello solution displays hello data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="d0a4c-119">Sources de données</span><span class="sxs-lookup"><span data-stu-id="d0a4c-119">Data sources</span></span>

<span data-ttu-id="d0a4c-120">Bonjour fabrique connecté solution affiche les données à partir de hello OPC UA serveurs connectés toohello solution.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-120">hello connected factory solution displays data from hello OPC UA servers connected toohello solution.</span></span> <span data-ttu-id="d0a4c-121">installation par défaut de Hello comprend plusieurs serveurs de OPC UA une simulation de fabrication en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-121">hello default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="d0a4c-122">Vous pouvez ajouter vos propres serveurs OPC UA qui [se connecter via une passerelle] [ lnk-connect-cf] tooyour solution.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-122">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] tooyour solution.</span></span>

<span data-ttu-id="d0a4c-123">Vous pouvez parcourir les éléments de données hello qu’un serveur OPC UA connecté peut envoyer tooyour solution dans le tableau de bord hello :</span><span class="sxs-lookup"><span data-stu-id="d0a4c-123">You can browse hello data items that a connected OPC UA server can send tooyour solution in hello dashboard:</span></span>

1. <span data-ttu-id="d0a4c-124">Accédez toohello **, sélectionnez un serveur OPC UA** vue :</span><span class="sxs-lookup"><span data-stu-id="d0a4c-124">Navigate toohello **Select an OPC UA server** view:</span></span>

    ![Accédez toohello sélectionner une vue du serveur OPC UA][img-select-server]

1. <span data-ttu-id="d0a4c-126">Sélectionnez un serveur et cliquez sur **Connect** (Connexion).</span><span class="sxs-lookup"><span data-stu-id="d0a4c-126">Select a server and click **Connect**.</span></span> <span data-ttu-id="d0a4c-127">Cliquez sur **continuer** lorsque l’avertissement de sécurité hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-127">Click **Proceed** when hello security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d0a4c-128">Cet avertissement apparaît une fois pour chaque serveur uniquement et établit une relation d’approbation entre le tableau de bord de solution hello et serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-128">This warning only appears once for each server and establishes a trust relationship between hello solution dashboard and hello server.</span></span>

1. <span data-ttu-id="d0a4c-129">Vous pouvez parcourir les éléments de données hello qui hello server peuvent envoyer toohello solution.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-129">You can now browse hello data items that hello server can send toohello solution.</span></span> <span data-ttu-id="d0a4c-130">Les éléments qui sont envoyés toohello solution ont une coche verte :</span><span class="sxs-lookup"><span data-stu-id="d0a4c-130">Items that are being sent toohello solution have a green check mark:</span></span>

    ![Éléments publiés][img-published]

1. <span data-ttu-id="d0a4c-132">Si vous êtes un *administrateur* dans la solution de hello, vous pouvez choisir toopublish un toomake d’élément de données accessibles dans hello connecté solution de fabrique.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-132">If you are an *Administrator* in hello solution, you can choose toopublish a data item toomake it available in hello connected factory solution.</span></span> <span data-ttu-id="d0a4c-133">En tant qu’administrateur, vous pouvez également modifier la valeur hello d’éléments de données et appeler les méthodes Bonjour server de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-133">As an Administrator, you can also change hello value of data items and call methods in hello OPC UA server.</span></span>

## <a name="map-hello-data"></a><span data-ttu-id="d0a4c-134">Mapper les données de salutation</span><span class="sxs-lookup"><span data-stu-id="d0a4c-134">Map hello data</span></span>

<span data-ttu-id="d0a4c-135">Hello connecté des mappages de solution de fabrique et hello d’agrégats publié des éléments de données à partir de hello OPC UA server toohello différentes vues dans la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-135">hello connected factory solution maps and aggregates hello published data items from hello OPC UA server toohello various views in hello solution.</span></span> <span data-ttu-id="d0a4c-136">Hello fabrique connecté solution déploie tooyour compte Azure lorsque vous configurez la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-136">hello connected factory solution deploys tooyour Azure account when you provision hello solution.</span></span> <span data-ttu-id="d0a4c-137">Un fichier JSON Bonjour Visual Studio connecté fabrique solution stocke ces informations de mappage.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-137">A JSON file in hello Visual Studio connected factory solution stores this mapping information.</span></span> <span data-ttu-id="d0a4c-138">Vous pouvez afficher et modifier ce fichier de configuration JSON dans la fabrique de hello connecté solution Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-138">You can view and modify this JSON configuration file in hello connected factory Visual Studio solution.</span></span> <span data-ttu-id="d0a4c-139">Vous pouvez redéployer la solution de hello après avoir apporté une modification.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-139">You can redeploy hello solution after you make a change.</span></span>

<span data-ttu-id="d0a4c-140">Vous pouvez utiliser le fichier de configuration hello pour :</span><span class="sxs-lookup"><span data-stu-id="d0a4c-140">You can use hello configuration file to:</span></span>

- <span data-ttu-id="d0a4c-141">Modifier les fabriques simulé existant de hello, les lignes de la production et les stations.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-141">Edit hello existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="d0a4c-142">Mapper des données à partir des serveurs OPC UA réels que vous vous connectez toohello solution.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-142">Map data from real OPC UA servers that you connect toohello solution.</span></span>

<span data-ttu-id="d0a4c-143">tooclone une copie de hello connecté solution Visual Studio de fabrique, hello utiliser git commande suivante :</span><span class="sxs-lookup"><span data-stu-id="d0a4c-143">tooclone a copy of hello connected factory Visual Studio solution, use hello following git command:</span></span>

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

<span data-ttu-id="d0a4c-144">fichier de Hello **ContosoTopologyDescription.json** définit hello vues de mappage à partir de hello données du serveur OPC UA éléments toohello tableau de bord de solution hello fabrique connecté.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-144">hello file **ContosoTopologyDescription.json** defines hello mapping from hello OPC UA server data items toohello views in hello connected factory solution dashboard.</span></span> <span data-ttu-id="d0a4c-145">Vous pouvez trouver ce fichier de configuration Bonjour **Contoso\Topology** dossier Bonjour **WebApp** projet Bonjour solution Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-145">You can find this configuration file in hello **Contoso\Topology** folder in hello **WebApp** project in hello Visual Studio solution.</span></span>

<span data-ttu-id="d0a4c-146">le contenu du fichier JSON de hello Hello est organisé comme une hiérarchie de fabrique, ligne de production et les nœuds de station.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-146">hello content of hello JSON file is organized as a hierarchy of factory, production line, and station nodes.</span></span> <span data-ttu-id="d0a4c-147">Cette hiérarchie définit la hiérarchie de navigation hello dans tableau de bord hello fabrique connecté.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-147">This hierarchy defines hello navigation hierarchy in hello connected factory dashboard.</span></span> <span data-ttu-id="d0a4c-148">Valeurs sur chaque nœud de hiérarchie de hello déterminent les informations hello affichées dans le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-148">Values at each node of hello hierarchy determine hello information displayed in hello dashboard.</span></span> <span data-ttu-id="d0a4c-149">Par exemple, le fichier JSON de hello contient hello valeurs pour hello fabrique de Munich suivantes :</span><span class="sxs-lookup"><span data-stu-id="d0a4c-149">For example, hello JSON file contains hello following values for hello Munich factory:</span></span>

```json
"Guid": "73B534AE-7C7E-4877-B826-F1C0EA339F65",
"Name": "Munich",
"Description": "Braking system",
"Location": {
    "City": "Munich",
    "Country": "Germany",
    "Latitude": 48.13641,
    "Longitude": 11.57754
},
"Image": "munich.jpg"
```

<span data-ttu-id="d0a4c-150">emplacement, la description et nom de hello s’affichent dans cette vue dans le tableau de bord hello :</span><span class="sxs-lookup"><span data-stu-id="d0a4c-150">hello name, description, and location appear on this view in hello dashboard:</span></span>

![Données Munich dans le tableau de bord hello][img-munich]

<span data-ttu-id="d0a4c-152">Chaque usine, ligne de production et poste présente une propriété image.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-152">Each factory, production line, and station have an image property.</span></span> <span data-ttu-id="d0a4c-153">Vous pouvez trouver ces fichiers JPEG Bonjour **Content\img** dossier Bonjour **WebApp** projet.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-153">You can find these JPEG files in hello **Content\img** folder in hello **WebApp** project.</span></span> <span data-ttu-id="d0a4c-154">Ces fichiers image s’affichent dans tableau de bord hello fabrique connecté.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-154">These image files display in hello connected factory dashboard.</span></span>

<span data-ttu-id="d0a4c-155">Chaque station comprend plusieurs propriétés détaillées qui définissent le mappage des éléments de données de hello OPC UA de hello.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-155">Each station includes several detailed properties that define hello mapping from hello OPC UA data items.</span></span> <span data-ttu-id="d0a4c-156">Ces propriétés sont décrites dans les sections suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="d0a4c-156">These properties are described in hello following sections:</span></span>

### <a name="opcuri"></a><span data-ttu-id="d0a4c-157">OpcUri</span><span class="sxs-lookup"><span data-stu-id="d0a4c-157">OpcUri</span></span>

<span data-ttu-id="d0a4c-158">Hello **OpcUri** valeur est hello OPC UA Application URI qui identifie de façon unique hello server de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-158">hello **OpcUri** value is hello OPC UA Application URI that uniquely identifies hello OPC UA server.</span></span> <span data-ttu-id="d0a4c-159">Par exemple, hello **OpcUri** valeur pour la station d’assembly hello sur la ligne de production 1 de Munich ressemble à hello suivantes : **urn : scada2194:ua:munich:productionline0:assemblystation**.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-159">For example, hello **OpcUri** value for hello assembly station on production line 1 in Munich looks like hello following: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span></span>

<span data-ttu-id="d0a4c-160">Vous pouvez afficher hello URI des serveurs OPC UA hello connecté dans le tableau de bord de solution hello :</span><span class="sxs-lookup"><span data-stu-id="d0a4c-160">You can view hello URIs of hello connected OPC UA servers in hello solution dashboard:</span></span>

![Afficher l’URI des serveurs OPC UA][img-server-uris]

### <a name="simulation"></a><span data-ttu-id="d0a4c-162">Simulation</span><span class="sxs-lookup"><span data-stu-id="d0a4c-162">Simulation</span></span>

<span data-ttu-id="d0a4c-163">Hello informations Bonjour **Simulation** nœud est toohello spécifique simulation OPC UA qui s’exécute dans hello serveurs OPC UA qui sont configurés par défaut.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-163">hello information in hello **Simulation** node is specific toohello OPC UA simulation that runs in hello OPC UA servers that are provisioned by default.</span></span> <span data-ttu-id="d0a4c-164">Elles ne sont pas utilisées pour un serveur OPC UA réel.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-164">It is not used for a real OPC UA server.</span></span>

### <a name="kpi1-and-kpi2"></a><span data-ttu-id="d0a4c-165">Kpi1 et Kpi2</span><span class="sxs-lookup"><span data-stu-id="d0a4c-165">Kpi1 and Kpi2</span></span>

<span data-ttu-id="d0a4c-166">Ces nœuds décrivent comment les données à partir de la station de hello contribuent toohello deux valeurs d’indicateur de performance clé dans le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-166">These nodes describe how data from hello station contributes toohello two KPI values in hello dashboard.</span></span> <span data-ttu-id="d0a4c-167">Dans un déploiement par défaut, ces valeurs de KPI sont des unités par heure et des kWh.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-167">In a default deployment, these KPI values are units per hour and kWh per hour.</span></span> <span data-ttu-id="d0a4c-168">solution de Hello calcule les valeurs d’indicateur de performance clé au niveau d’une station de hello et agrège les niveaux de fabrique et de la ligne de production hello.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-168">hello solution calculates KPI vales at hello level of a station and aggregates them at hello production line and factory levels.</span></span>

<span data-ttu-id="d0a4c-169">Chaque KPI présente une valeur minimale, maximale et cible.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-169">Each KPI has a minimum, maximum, and target value.</span></span> <span data-ttu-id="d0a4c-170">Chaque valeur d’indicateur de performance clé peut également définir des actions d’alerte pour hello connecté fabrique solution tooperform.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-170">Each KPI value can also define alert actions for hello connected factory solution tooperform.</span></span> <span data-ttu-id="d0a4c-171">Hello extrait de code suivant montre les définitions d’indicateur de performance clé hello pour station d’assembly hello sur la ligne de production 1 de Munich :</span><span class="sxs-lookup"><span data-stu-id="d0a4c-171">hello following snippet shows hello KPI definitions for hello assembly station on production line 1 in Munich:</span></span>

```json
"Kpi1": {
  "Minimum": 150,
  "Target": 300,
  "Maximum": 600
},
"Kpi2": {
  "Minimum": 50,
  "Target": 100,
  "Maximum": 200,
  "MinimumAlertActions": [
    {
      "Type": "None"
    }
  ]
}
```

<span data-ttu-id="d0a4c-172">Hello capture d’écran suivante montre hello KPI données dans le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-172">hello following screenshot shows hello KPI data in hello dashboard.</span></span>

![Informations d’indicateur de performance clé dans le tableau de bord hello][lnk-kpi]

### <a name="opcnodes"></a><span data-ttu-id="d0a4c-174">OpcNodes</span><span class="sxs-lookup"><span data-stu-id="d0a4c-174">OpcNodes</span></span>

<span data-ttu-id="d0a4c-175">Hello **OpcNodes** identifient les nœuds hello des éléments de données publiées à partir de hello server de OPC UA et spécifiez comment tooprocess ces données.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-175">hello **OpcNodes** nodes identify hello published data items from hello OPC UA server and specify how tooprocess that data.</span></span>

<span data-ttu-id="d0a4c-176">Hello **NodeId** valeur identifie hello NodeID de UA OPC spécifique à partir de hello server de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-176">hello **NodeId** value identifies hello specific OPC UA NodeID from hello OPC UA server.</span></span> <span data-ttu-id="d0a4c-177">Hello premier nœud station d’assembly hello pour la ligne de production 1 de Munich a la valeur **ns = 2 ; i = 385**.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-177">hello first node in hello assembly station for production line 1 in Munich has a value **ns=2;i=385**.</span></span> <span data-ttu-id="d0a4c-178">A **NodeId** valeur spécifie tooread d’élément de données hello hello server de OPC UA et hello **SymbolicName** fournit un nom convivial toouse dans le tableau de bord hello pour ces données.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-178">A **NodeId** value specifies hello data item tooread from hello OPC UA server, and hello **SymbolicName** provides a user-friendly name toouse in hello dashboard for that data.</span></span>

<span data-ttu-id="d0a4c-179">Autres valeurs associées à chaque nœud sont résumées dans hello tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="d0a4c-179">Other values associated with each node are summarized in hello following table:</span></span>

| <span data-ttu-id="d0a4c-180">Valeur</span><span class="sxs-lookup"><span data-stu-id="d0a4c-180">Value</span></span> | <span data-ttu-id="d0a4c-181">Description</span><span class="sxs-lookup"><span data-stu-id="d0a4c-181">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="d0a4c-182">Pertinence</span><span class="sxs-lookup"><span data-stu-id="d0a4c-182">Relevance</span></span>  | <span data-ttu-id="d0a4c-183">valeurs d’indicateur de performance clé et OEE Hello ces données contribuent à.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-183">hello KPI and OEE values this data contributes to.</span></span> |
| <span data-ttu-id="d0a4c-184">OpCode</span><span class="sxs-lookup"><span data-stu-id="d0a4c-184">OpCode</span></span>     | <span data-ttu-id="d0a4c-185">Comment les données de salutation sont agrégées.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-185">How hello data is aggregated.</span></span> |
| <span data-ttu-id="d0a4c-186">Units</span><span class="sxs-lookup"><span data-stu-id="d0a4c-186">Units</span></span>      | <span data-ttu-id="d0a4c-187">toouse d’unités Hello dans le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-187">hello units toouse in hello dashboard.</span></span>  |
| <span data-ttu-id="d0a4c-188">Visible</span><span class="sxs-lookup"><span data-stu-id="d0a4c-188">Visible</span></span>    | <span data-ttu-id="d0a4c-189">Si toodisplay cette valeur de tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-189">Whether toodisplay this value in hello dashboard.</span></span> <span data-ttu-id="d0a4c-190">Certaines valeurs sont utilisées dans les calculs mais ne sont pas affichées.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-190">Some values are used in calculations but not displayed.</span></span>  |
| <span data-ttu-id="d0a4c-191">Maximale</span><span class="sxs-lookup"><span data-stu-id="d0a4c-191">Maximum</span></span>    | <span data-ttu-id="d0a4c-192">valeur maximale Hello qui déclenche une alerte dans le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-192">hello maximum value that triggers an alert in hello dashboard.</span></span> |
| <span data-ttu-id="d0a4c-193">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="d0a4c-193">MaximumAlertActions</span></span> | <span data-ttu-id="d0a4c-194">Un tootake action dans l’alerte tooan de réponse.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-194">An action tootake in response tooan alert.</span></span> <span data-ttu-id="d0a4c-195">Par exemple, envoyer une station tooa de commande.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-195">For example, send a command tooa station.</span></span> |
| <span data-ttu-id="d0a4c-196">ConstValue</span><span class="sxs-lookup"><span data-stu-id="d0a4c-196">ConstValue</span></span> | <span data-ttu-id="d0a4c-197">Valeur constante utilisée dans un calcul.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-197">A constant value used in a calculation.</span></span> |

## <a name="deploy-hello-changes"></a><span data-ttu-id="d0a4c-198">Déployer les modifications de hello</span><span class="sxs-lookup"><span data-stu-id="d0a4c-198">Deploy hello changes</span></span>

<span data-ttu-id="d0a4c-199">Lorsque vous avez terminé d’apporter des modifications toohello **ContosoTopologyDescription.json** fichier, vous devez redéployer hello connecté fabrique solution tooyour compte Azure.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-199">When you have finished making changes toohello **ContosoTopologyDescription.json** file, you must redeploy hello connected factory solution tooyour Azure account.</span></span>

<span data-ttu-id="d0a4c-200">Hello **azure iot-connecté-usine** référentiel inclut un **build.ps1** script PowerShell vous pouvez utiliser toorebuild et déployer des solutions de hello.</span><span class="sxs-lookup"><span data-stu-id="d0a4c-200">hello **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use toorebuild and deploy hello solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0a4c-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d0a4c-201">Next Steps</span></span>

<span data-ttu-id="d0a4c-202">En savoir plus sur hello connecté fabrique préconfiguré solution hello lors de la lecture suivante d’articles :</span><span class="sxs-lookup"><span data-stu-id="d0a4c-202">Learn more about hello connected factory preconfigured solution by reading hello following articles:</span></span>

* <span data-ttu-id="d0a4c-203">[Procédure pas à pas de la solution préconfigurée d’usine connectée][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="d0a4c-203">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="d0a4c-204">[Déployer une passerelle pour une usine connectée][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="d0a4c-204">[Deploy a gateway for connected factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="d0a4c-205">[Autorisations sur le site de azureiotsuite.com hello][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="d0a4c-205">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="d0a4c-206">FAQ sur la fabrique connectée</span><span class="sxs-lookup"><span data-stu-id="d0a4c-206">Connected factory FAQ</span></span>](iot-suite-faq-cf.md)
* <span data-ttu-id="d0a4c-207">[FAQ][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="d0a4c-207">[FAQ][lnk-faq]</span></span>


[img-oee-kpi]: ./media/iot-suite-connected-factory-customize/oeenadkpi.png
[img-manufactured-items]: ./media/iot-suite-connected-factory-customize/manufactured.png
[img-tsi]: ./media/iot-suite-connected-factory-customize/tsi.png
[img-select-server]: ./media/iot-suite-connected-factory-customize/selectserver.png
[img-published]: ./media/iot-suite-connected-factory-customize/published.png
[img-munich]: ./media/iot-suite-connected-factory-customize/munich.png
[img-server-uris]: ./media/iot-suite-connected-factory-customize/serveruris.png
[lnk-kpi]: ./media/iot-suite-connected-factory-customize/kpidisplay.png

[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md