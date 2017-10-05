---
title: "Personnaliser l’usine connectée Azure IoT Suite | Documents Microsoft"
description: "Découvrez comment personnaliser le comportement de la solution préconfigurée d’usine connectée."
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
ms.openlocfilehash: 90a6172dbd887ecda5a9f5d9082a4e136092bc10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="customize-how-the-connected-factory-solution-displays-data-from-your-opc-ua-servers"></a><span data-ttu-id="f70a7-103">Personnaliser le mode d’affichage des données de vos serveurs OPC UA par la solution d’usine connectée</span><span class="sxs-lookup"><span data-stu-id="f70a7-103">Customize how the connected factory solution displays data from your OPC UA servers</span></span>

## <a name="introduction"></a><span data-ttu-id="f70a7-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="f70a7-104">Introduction</span></span>

<span data-ttu-id="f70a7-105">La solution d’usine connectée agrège et affiche les données des serveurs OPC UA qui y sont connectés.</span><span class="sxs-lookup"><span data-stu-id="f70a7-105">The connected factory solution aggregates and displays data from the OPC UA servers connected to the solution.</span></span> <span data-ttu-id="f70a7-106">Vous pouvez parcourir les serveurs OPC UA et leur envoyer des commandes dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="f70a7-106">You can browse and send commands to the OPC UA servers in your solution.</span></span> <span data-ttu-id="f70a7-107">Pour plus d’informations sur OPC UA, consultez les [questions fréquentes (FAQ) sur l’usine connectée](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="f70a7-107">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>

<span data-ttu-id="f70a7-108">Des exemples de données agrégées dans la solution incluent l’efficacité globale des équipements (OEE) et les indicateurs de performance clés (KPI), que vous pouvez afficher dans le tableau de bord au niveau d’une usine, d’une ligne de production et d’un poste.</span><span class="sxs-lookup"><span data-stu-id="f70a7-108">Examples of aggregated data in the solution include the Overall Equipment Efficiency (OEE) and Key Performance Indicators (KPIs) that you can view in the dashboard at the factory, line, and station levels.</span></span> <span data-ttu-id="f70a7-109">La capture d’écran suivante illustre les valeurs d’OEE et de KPI pour le poste d’assemblage **Assembly** de la ligne de production **Production line 1** dans l’usine de **Munich** :</span><span class="sxs-lookup"><span data-stu-id="f70a7-109">The following screenshot shows the OEE and KPI values for the **Assembly** station, on **Production line 1**, in the **Munich** factory:</span></span>

![Exemple de valeurs d’OEE et de KPI dans la solution][img-oee-kpi]

<span data-ttu-id="f70a7-111">La solution permet d’afficher des informations détaillées pour des éléments de données spécifiques des serveurs OPC UA appelés *postes*.</span><span class="sxs-lookup"><span data-stu-id="f70a7-111">The solution enables you to view detailed information from specific data items from the OPC UA servers, called *stations*.</span></span> <span data-ttu-id="f70a7-112">La capture d’écran suivante illustre des graphiques du nombre d’articles fabriqués à partir d’un poste spécifique :</span><span class="sxs-lookup"><span data-stu-id="f70a7-112">The following screenshot shows plots of the number of manufactured items from a specific station:</span></span>

![Graphiques du nombre d’éléments fabriqués][img-manufactured-items]

<span data-ttu-id="f70a7-114">Si vous cliquez sur l’un des graphiques, vous pouvez explorer les données plus en détail à l’aide de Time Series Insights (TSI) :</span><span class="sxs-lookup"><span data-stu-id="f70a7-114">If you click one of the graphs, you can explore the data further using Time Series Insights (TSI):</span></span>

![Explorer les données à l’aide de Time Series Insights][img-tsi]

<span data-ttu-id="f70a7-116">Cet article aborde les points suivants :</span><span class="sxs-lookup"><span data-stu-id="f70a7-116">This article describes:</span></span>

- <span data-ttu-id="f70a7-117">Comment rendre disponibles les données dans les différentes vues de la solution.</span><span class="sxs-lookup"><span data-stu-id="f70a7-117">How the data is made available to the various views in the solution.</span></span>
- <span data-ttu-id="f70a7-118">Comment personnaliser le mode d’affichage des données par la solution.</span><span class="sxs-lookup"><span data-stu-id="f70a7-118">How you can customize the way the solution displays the data.</span></span>

## <a name="data-sources"></a><span data-ttu-id="f70a7-119">Sources de données</span><span class="sxs-lookup"><span data-stu-id="f70a7-119">Data sources</span></span>

<span data-ttu-id="f70a7-120">La solution d’usine connectée affiche les données des serveurs OPC UA qui y sont connectés.</span><span class="sxs-lookup"><span data-stu-id="f70a7-120">The connected factory solution displays data from the OPC UA servers connected to the solution.</span></span> <span data-ttu-id="f70a7-121">L’installation par défaut inclut plusieurs serveurs OPC UA exécutant une simulation d’usine.</span><span class="sxs-lookup"><span data-stu-id="f70a7-121">The default installation includes several OPC UA servers running a factory simulation.</span></span> <span data-ttu-id="f70a7-122">Vous pouvez ajouter vos propres serveurs OPC UA qui [se connectent via une passerelle][lnk-connect-cf] à votre solution.</span><span class="sxs-lookup"><span data-stu-id="f70a7-122">You can add your own OPC UA servers that [connect through a gateway][lnk-connect-cf] to your solution.</span></span>

<span data-ttu-id="f70a7-123">Vous pouvez parcourir les éléments de données qu’un serveur OPC UA peut envoyer à votre solution dans le tableau de bord :</span><span class="sxs-lookup"><span data-stu-id="f70a7-123">You can browse the data items that a connected OPC UA server can send to your solution in the dashboard:</span></span>

1. <span data-ttu-id="f70a7-124">Accédez à la vue **Select an OPC UA server** (Sélectionner un serveur OPC UA) :</span><span class="sxs-lookup"><span data-stu-id="f70a7-124">Navigate to the **Select an OPC UA server** view:</span></span>

    ![Accéder à la vue Select an OPC UA server (Sélectionner un serveur OPC UA)][img-select-server]

1. <span data-ttu-id="f70a7-126">Sélectionnez un serveur et cliquez sur **Connect** (Connexion).</span><span class="sxs-lookup"><span data-stu-id="f70a7-126">Select a server and click **Connect**.</span></span> <span data-ttu-id="f70a7-127">Lorsque l’avertissement de sécurité s’affiche, cliquez sur **Proceed** (Continuer).</span><span class="sxs-lookup"><span data-stu-id="f70a7-127">Click **Proceed** when the security warning appears.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f70a7-128">Cet avertissement s’affiche une seule fois pour chaque serveur et établit une relation d’approbation entre le tableau de bord de la solution et le serveur.</span><span class="sxs-lookup"><span data-stu-id="f70a7-128">This warning only appears once for each server and establishes a trust relationship between the solution dashboard and the server.</span></span>

1. <span data-ttu-id="f70a7-129">Vous pouvez maintenant parcourir les éléments de données que le serveur peut envoyer à la solution.</span><span class="sxs-lookup"><span data-stu-id="f70a7-129">You can now browse the data items that the server can send to the solution.</span></span> <span data-ttu-id="f70a7-130">Les éléments qui sont envoyés à la solution présentent une coche verte :</span><span class="sxs-lookup"><span data-stu-id="f70a7-130">Items that are being sent to the solution have a green check mark:</span></span>

    ![Éléments publiés][img-published]

1. <span data-ttu-id="f70a7-132">Si vous êtes un *administrateur* dans la solution, vous pouvez choisir de publier un élément de données pour le rendre disponible dans la solution d’usine connectée.</span><span class="sxs-lookup"><span data-stu-id="f70a7-132">If you are an *Administrator* in the solution, you can choose to publish a data item to make it available in the connected factory solution.</span></span> <span data-ttu-id="f70a7-133">En tant qu’administrateur, vous pouvez également modifier la valeur des éléments de données et appeler des méthodes sur le serveur OPC UA.</span><span class="sxs-lookup"><span data-stu-id="f70a7-133">As an Administrator, you can also change the value of data items and call methods in the OPC UA server.</span></span>

## <a name="map-the-data"></a><span data-ttu-id="f70a7-134">Mapper les données</span><span class="sxs-lookup"><span data-stu-id="f70a7-134">Map the data</span></span>

<span data-ttu-id="f70a7-135">La solution d’usine connectée mappe et agrège les éléments de données publiés à partir du serveur OPC UA dans les différentes vues de la solution.</span><span class="sxs-lookup"><span data-stu-id="f70a7-135">The connected factory solution maps and aggregates the published data items from the OPC UA server to the various views in the solution.</span></span> <span data-ttu-id="f70a7-136">La solution d’usine connectée se déploie sur votre compte Azure lorsque vous la configurez.</span><span class="sxs-lookup"><span data-stu-id="f70a7-136">The connected factory solution deploys to your Azure account when you provision the solution.</span></span> <span data-ttu-id="f70a7-137">Un fichier JSON de la solution Visual Studio d’usine connectée stocke ces informations de mappage.</span><span class="sxs-lookup"><span data-stu-id="f70a7-137">A JSON file in the Visual Studio connected factory solution stores this mapping information.</span></span> <span data-ttu-id="f70a7-138">Vous pouvez afficher et modifier ce fichier de configuration JSON dans la solution Visual Studio d’usine connectée.</span><span class="sxs-lookup"><span data-stu-id="f70a7-138">You can view and modify this JSON configuration file in the connected factory Visual Studio solution.</span></span> <span data-ttu-id="f70a7-139">Vous pouvez redéployer la solution une fois que vous apportez une modification.</span><span class="sxs-lookup"><span data-stu-id="f70a7-139">You can redeploy the solution after you make a change.</span></span>

<span data-ttu-id="f70a7-140">Vous pouvez utiliser le fichier de configuration pour :</span><span class="sxs-lookup"><span data-stu-id="f70a7-140">You can use the configuration file to:</span></span>

- <span data-ttu-id="f70a7-141">Modifier les usines, les lignes de production existantes et les postes simulés existants.</span><span class="sxs-lookup"><span data-stu-id="f70a7-141">Edit the existing simulated factories, production lines, and stations.</span></span>
- <span data-ttu-id="f70a7-142">Mapper les données des serveurs OPC UA réels que vous connectez à la solution.</span><span class="sxs-lookup"><span data-stu-id="f70a7-142">Map data from real OPC UA servers that you connect to the solution.</span></span>

<span data-ttu-id="f70a7-143">Pour cloner une copie de la solution Visual Studio d’usine connectée, utilisez la commande git suivante :</span><span class="sxs-lookup"><span data-stu-id="f70a7-143">To clone a copy of the connected factory Visual Studio solution, use the following git command:</span></span>

`git clone https://github.com/Azure/azure-iot-connected-factory.git`

<span data-ttu-id="f70a7-144">Le fichier **ContosoTopologyDescription.json** définit le mappage entre les éléments de données des serveurs OPC UA et les vues du tableau de bord de la solution d’usine connectée.</span><span class="sxs-lookup"><span data-stu-id="f70a7-144">The file **ContosoTopologyDescription.json** defines the mapping from the OPC UA server data items to the views in the connected factory solution dashboard.</span></span> <span data-ttu-id="f70a7-145">Ce fichier de configuration se trouve dans le dossier **Contoso\Topology** du projet **WebApp** dans la solution Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f70a7-145">You can find this configuration file in the **Contoso\Topology** folder in the **WebApp** project in the Visual Studio solution.</span></span>

<span data-ttu-id="f70a7-146">Le contenu du fichier JSON est organisé sous forme de hiérarchie de nœuds d’usines, de lignes de production et de postes.</span><span class="sxs-lookup"><span data-stu-id="f70a7-146">The content of the JSON file is organized as a hierarchy of factory, production line, and station nodes.</span></span> <span data-ttu-id="f70a7-147">Cette hiérarchie définit la hiérarchie de navigation du tableau de bord de l’usine connectée.</span><span class="sxs-lookup"><span data-stu-id="f70a7-147">This hierarchy defines the navigation hierarchy in the connected factory dashboard.</span></span> <span data-ttu-id="f70a7-148">Les valeurs de chaque nœud de la hiérarchie déterminent les informations affichées dans le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="f70a7-148">Values at each node of the hierarchy determine the information displayed in the dashboard.</span></span> <span data-ttu-id="f70a7-149">Par exemple, le fichier JSON contient les valeurs suivantes pour l’usine de Munich :</span><span class="sxs-lookup"><span data-stu-id="f70a7-149">For example, the JSON file contains the following values for the Munich factory:</span></span>

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

<span data-ttu-id="f70a7-150">Le nom, la description et l’emplacement apparaissent dans cette vue du tableau de bord :</span><span class="sxs-lookup"><span data-stu-id="f70a7-150">The name, description, and location appear on this view in the dashboard:</span></span>

![Données de l’usine de Munich dans le tableau de bord][img-munich]

<span data-ttu-id="f70a7-152">Chaque usine, ligne de production et poste présente une propriété image.</span><span class="sxs-lookup"><span data-stu-id="f70a7-152">Each factory, production line, and station have an image property.</span></span> <span data-ttu-id="f70a7-153">Ces fichiers JPEG se trouvent dans le dossier **Content\img** du projet **WebApp**.</span><span class="sxs-lookup"><span data-stu-id="f70a7-153">You can find these JPEG files in the **Content\img** folder in the **WebApp** project.</span></span> <span data-ttu-id="f70a7-154">Ces fichiers image s’affichent dans le tableau de bord de l’usine connectée.</span><span class="sxs-lookup"><span data-stu-id="f70a7-154">These image files display in the connected factory dashboard.</span></span>

<span data-ttu-id="f70a7-155">Chaque poste inclut plusieurs propriétés détaillées qui définissent le mappage à partir des éléments de données OPC UA.</span><span class="sxs-lookup"><span data-stu-id="f70a7-155">Each station includes several detailed properties that define the mapping from the OPC UA data items.</span></span> <span data-ttu-id="f70a7-156">Ces propriétés sont décrites dans les sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="f70a7-156">These properties are described in the following sections:</span></span>

### <a name="opcuri"></a><span data-ttu-id="f70a7-157">OpcUri</span><span class="sxs-lookup"><span data-stu-id="f70a7-157">OpcUri</span></span>

<span data-ttu-id="f70a7-158">La valeur **OpcUri** correspond à l’URI d’application OPC UA qui identifie de façon unique le serveur OPC UA.</span><span class="sxs-lookup"><span data-stu-id="f70a7-158">The **OpcUri** value is the OPC UA Application URI that uniquely identifies the OPC UA server.</span></span> <span data-ttu-id="f70a7-159">Par exemple, la valeur **OpcUri** pour le poste d’assemblage de la ligne de production 1 de Munich se présente comme suit : **urn:scada2194:ua:munich:productionline0:assemblystation**.</span><span class="sxs-lookup"><span data-stu-id="f70a7-159">For example, the **OpcUri** value for the assembly station on production line 1 in Munich looks like the following: **urn:scada2194:ua:munich:productionline0:assemblystation**.</span></span>

<span data-ttu-id="f70a7-160">Vous pouvez afficher l’URI des serveurs OPC UA connectés dans le tableau de bord de la solution :</span><span class="sxs-lookup"><span data-stu-id="f70a7-160">You can view the URIs of the connected OPC UA servers in the solution dashboard:</span></span>

![Afficher l’URI des serveurs OPC UA][img-server-uris]

### <a name="simulation"></a><span data-ttu-id="f70a7-162">Simulation</span><span class="sxs-lookup"><span data-stu-id="f70a7-162">Simulation</span></span>

<span data-ttu-id="f70a7-163">Les informations que contient le nœud **Simulation** sont propres à la simulation OPC UA exécutée sur les serveurs OPC UA configurés par défaut.</span><span class="sxs-lookup"><span data-stu-id="f70a7-163">The information in the **Simulation** node is specific to the OPC UA simulation that runs in the OPC UA servers that are provisioned by default.</span></span> <span data-ttu-id="f70a7-164">Elles ne sont pas utilisées pour un serveur OPC UA réel.</span><span class="sxs-lookup"><span data-stu-id="f70a7-164">It is not used for a real OPC UA server.</span></span>

### <a name="kpi1-and-kpi2"></a><span data-ttu-id="f70a7-165">Kpi1 et Kpi2</span><span class="sxs-lookup"><span data-stu-id="f70a7-165">Kpi1 and Kpi2</span></span>

<span data-ttu-id="f70a7-166">Ces nœuds décrivent la manière dont les données du poste contribuent aux deux valeurs de KPI dans le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="f70a7-166">These nodes describe how data from the station contributes to the two KPI values in the dashboard.</span></span> <span data-ttu-id="f70a7-167">Dans un déploiement par défaut, ces valeurs de KPI sont des unités par heure et des kWh.</span><span class="sxs-lookup"><span data-stu-id="f70a7-167">In a default deployment, these KPI values are units per hour and kWh per hour.</span></span> <span data-ttu-id="f70a7-168">La solution calcule les valeurs de KPI au niveau d’un poste et les agrège au niveau de la ligne de production et de l’usine.</span><span class="sxs-lookup"><span data-stu-id="f70a7-168">The solution calculates KPI vales at the level of a station and aggregates them at the production line and factory levels.</span></span>

<span data-ttu-id="f70a7-169">Chaque KPI présente une valeur minimale, maximale et cible.</span><span class="sxs-lookup"><span data-stu-id="f70a7-169">Each KPI has a minimum, maximum, and target value.</span></span> <span data-ttu-id="f70a7-170">Chaque valeur de KPI peut également définir des actions d’alerte à exécuter par la solution d’usine connectée.</span><span class="sxs-lookup"><span data-stu-id="f70a7-170">Each KPI value can also define alert actions for the connected factory solution to perform.</span></span> <span data-ttu-id="f70a7-171">L’extrait de code suivant illustre les définitions de KPI pour le poste d’assemblage de la ligne de production 1 à Munich :</span><span class="sxs-lookup"><span data-stu-id="f70a7-171">The following snippet shows the KPI definitions for the assembly station on production line 1 in Munich:</span></span>

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

<span data-ttu-id="f70a7-172">La capture d’écran suivante illustre les données des KPI dans le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="f70a7-172">The following screenshot shows the KPI data in the dashboard.</span></span>

![Informations des KPI dans le tableau de bord][lnk-kpi]

### <a name="opcnodes"></a><span data-ttu-id="f70a7-174">OpcNodes</span><span class="sxs-lookup"><span data-stu-id="f70a7-174">OpcNodes</span></span>

<span data-ttu-id="f70a7-175">Les nœuds **OpcNodes** identifient les éléments de données publiés à partir du serveur OPC UA et spécifient le mode de traitement de ces données.</span><span class="sxs-lookup"><span data-stu-id="f70a7-175">The **OpcNodes** nodes identify the published data items from the OPC UA server and specify how to process that data.</span></span>

<span data-ttu-id="f70a7-176">La valeur **NodeId** correspond à l’identifiant de nœud OPC UA spécifique du serveur OPC UA.</span><span class="sxs-lookup"><span data-stu-id="f70a7-176">The **NodeId** value identifies the specific OPC UA NodeID from the OPC UA server.</span></span> <span data-ttu-id="f70a7-177">Le premier nœud du poste d’assemblage pour la ligne de production 1 à Munich présente la valeur **ns=2;i=385**.</span><span class="sxs-lookup"><span data-stu-id="f70a7-177">The first node in the assembly station for production line 1 in Munich has a value **ns=2;i=385**.</span></span> <span data-ttu-id="f70a7-178">Une valeur **NodeId** spécifie l’élément de données à lire à partir du serveur OPC UA et la valeur **SymbolicName** fournit un nom convivial à utiliser dans le tableau de bord pour ces données.</span><span class="sxs-lookup"><span data-stu-id="f70a7-178">A **NodeId** value specifies the data item to read from the OPC UA server, and the **SymbolicName** provides a user-friendly name to use in the dashboard for that data.</span></span>

<span data-ttu-id="f70a7-179">Les autres valeurs associées à chaque nœud sont résumées dans le tableau suivant :</span><span class="sxs-lookup"><span data-stu-id="f70a7-179">Other values associated with each node are summarized in the following table:</span></span>

| <span data-ttu-id="f70a7-180">Valeur</span><span class="sxs-lookup"><span data-stu-id="f70a7-180">Value</span></span> | <span data-ttu-id="f70a7-181">Description</span><span class="sxs-lookup"><span data-stu-id="f70a7-181">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="f70a7-182">Pertinence</span><span class="sxs-lookup"><span data-stu-id="f70a7-182">Relevance</span></span>  | <span data-ttu-id="f70a7-183">Valeurs de KPI et d’OEE auxquelles ces données contribuent.</span><span class="sxs-lookup"><span data-stu-id="f70a7-183">The KPI and OEE values this data contributes to.</span></span> |
| <span data-ttu-id="f70a7-184">OpCode</span><span class="sxs-lookup"><span data-stu-id="f70a7-184">OpCode</span></span>     | <span data-ttu-id="f70a7-185">Mode d’agrégation des données.</span><span class="sxs-lookup"><span data-stu-id="f70a7-185">How the data is aggregated.</span></span> |
| <span data-ttu-id="f70a7-186">Units</span><span class="sxs-lookup"><span data-stu-id="f70a7-186">Units</span></span>      | <span data-ttu-id="f70a7-187">Unités à utiliser dans le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="f70a7-187">The units to use in the dashboard.</span></span>  |
| <span data-ttu-id="f70a7-188">Visible</span><span class="sxs-lookup"><span data-stu-id="f70a7-188">Visible</span></span>    | <span data-ttu-id="f70a7-189">Indique si cette valeur doit être affichée dans le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="f70a7-189">Whether to display this value in the dashboard.</span></span> <span data-ttu-id="f70a7-190">Certaines valeurs sont utilisées dans les calculs mais ne sont pas affichées.</span><span class="sxs-lookup"><span data-stu-id="f70a7-190">Some values are used in calculations but not displayed.</span></span>  |
| <span data-ttu-id="f70a7-191">Maximale</span><span class="sxs-lookup"><span data-stu-id="f70a7-191">Maximum</span></span>    | <span data-ttu-id="f70a7-192">Valeur maximale qui déclenche une alerte dans le tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="f70a7-192">The maximum value that triggers an alert in the dashboard.</span></span> |
| <span data-ttu-id="f70a7-193">MaximumAlertActions</span><span class="sxs-lookup"><span data-stu-id="f70a7-193">MaximumAlertActions</span></span> | <span data-ttu-id="f70a7-194">Action à effectuer en réponse à une alerte</span><span class="sxs-lookup"><span data-stu-id="f70a7-194">An action to take in response to an alert.</span></span> <span data-ttu-id="f70a7-195">(par exemple, envoyer une commande à un poste).</span><span class="sxs-lookup"><span data-stu-id="f70a7-195">For example, send a command to a station.</span></span> |
| <span data-ttu-id="f70a7-196">ConstValue</span><span class="sxs-lookup"><span data-stu-id="f70a7-196">ConstValue</span></span> | <span data-ttu-id="f70a7-197">Valeur constante utilisée dans un calcul.</span><span class="sxs-lookup"><span data-stu-id="f70a7-197">A constant value used in a calculation.</span></span> |

## <a name="deploy-the-changes"></a><span data-ttu-id="f70a7-198">Déployer les modifications</span><span class="sxs-lookup"><span data-stu-id="f70a7-198">Deploy the changes</span></span>

<span data-ttu-id="f70a7-199">Une fois que vous avez apporté toutes les modifications requises au fichier **ContosoTopologyDescription.json**, vous devez redéployer la solution d’usine connectée dans votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="f70a7-199">When you have finished making changes to the **ContosoTopologyDescription.json** file, you must redeploy the connected factory solution to your Azure account.</span></span>

<span data-ttu-id="f70a7-200">Le référentiel **azure-iot-connected-factory** inclut un script PowerShell **build.ps1** que vous pouvez utiliser pour régénérer et déployer la solution.</span><span class="sxs-lookup"><span data-stu-id="f70a7-200">The **azure-iot-connected-factory** repository includes a **build.ps1** PowerShell script you can use to rebuild and deploy the solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f70a7-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f70a7-201">Next Steps</span></span>

<span data-ttu-id="f70a7-202">Pour en savoir plus sur la solution préconfigurée d’usine connectée, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="f70a7-202">Learn more about the connected factory preconfigured solution by reading the following articles:</span></span>

* <span data-ttu-id="f70a7-203">[Procédure pas à pas de la solution préconfigurée d’usine connectée][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="f70a7-203">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="f70a7-204">[Déployer une passerelle pour une usine connectée][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="f70a7-204">[Deploy a gateway for connected factory][lnk-connect-cf]</span></span>
* <span data-ttu-id="f70a7-205">[Autorisations sur le site azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="f70a7-205">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>
* [<span data-ttu-id="f70a7-206">FAQ sur la fabrique connectée</span><span class="sxs-lookup"><span data-stu-id="f70a7-206">Connected factory FAQ</span></span>](iot-suite-faq-cf.md)
* <span data-ttu-id="f70a7-207">[FAQ][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="f70a7-207">[FAQ][lnk-faq]</span></span>


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