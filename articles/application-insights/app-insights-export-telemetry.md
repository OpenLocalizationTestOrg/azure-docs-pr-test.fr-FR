---
title: "Exportation continue des données de télémétrie d’Application Insights | Microsoft Docs"
description: "Exportez les données de diagnostic et les données d’utilisation dans le stockage Microsoft Azure et téléchargez-les à partir de là."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: bwren
ms.openlocfilehash: 6ac3bda5101593b5ca66b4c9035e2fdac9d1e833
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="0d6e8-103">Exporter la télémétrie depuis Application Insights</span><span class="sxs-lookup"><span data-stu-id="0d6e8-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="0d6e8-104">Vous souhaitez conserver votre télémétrie plus longtemps que la période de rétention standard ?</span><span class="sxs-lookup"><span data-stu-id="0d6e8-104">Want to keep your telemetry for longer than the standard retention period?</span></span> <span data-ttu-id="0d6e8-105">Ou la traiter d’une façon spécialisée ?</span><span class="sxs-lookup"><span data-stu-id="0d6e8-105">Or process it in some specialized way?</span></span> <span data-ttu-id="0d6e8-106">L’exportation continue est idéale dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="0d6e8-107">Les événements que vous voyez dans le portail Application Insights peuvent être exportés vers le stockage Microsoft Azure au format JSON.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-107">The events you see in the Application Insights portal can be exported to storage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="0d6e8-108">À partir de là, vous pouvez télécharger vos données et écrire le code pour pouvoir les traiter.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-108">From there you can download your data and write whatever code you need to process it.</span></span>  

<span data-ttu-id="0d6e8-109">L’utilisation de l’exportation continue peut entraîner des frais supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="0d6e8-110">Consultez votre [modèle de tarification](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="0d6e8-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="0d6e8-111">Avant de configurer l’exportation continue, d’autres options doivent être prises en considération :</span><span class="sxs-lookup"><span data-stu-id="0d6e8-111">Before you set up continuous export, there are some alternatives you might want to consider:</span></span>

* <span data-ttu-id="0d6e8-112">Le bouton Exporter en haut d’un panneau de métriques ou de recherche permet de transférer des tables et des graphiques dans une feuille de calcul Excel.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-112">The Export button at the top of a metrics or search blade lets you transfer tables and charts to an Excel spreadsheet.</span></span>

* <span data-ttu-id="0d6e8-113">[Analytics](app-insights-analytics.md) fournit un puissant langage de requête pour la télémétrie</span><span class="sxs-lookup"><span data-stu-id="0d6e8-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="0d6e8-114">et peut également en exporter les résultats.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-114">It can also export results.</span></span>
* <span data-ttu-id="0d6e8-115">Si vous cherchez à [explorer vos données dans Power BI](app-insights-export-power-bi.md), vous pouvez le faire sans utiliser l’exportation continue.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-115">If you're looking to [explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="0d6e8-116">[L’API REST d’accès aux données](https://dev.applicationinsights.io/) vous permet d’accéder à vos données de télémétrie par programme.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-116">The [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="0d6e8-117">Une fois que l’exportation continue a copié vos données vers l’espace de stockage (où elles peuvent rester aussi longtemps que vous le souhaitez), elles restent disponibles dans Application Insights pendant la [période de rétention](app-insights-data-retention-privacy.md) habituelle.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-117">After Continuous Export copies your data to storage (where it can stay for as long as you like), it's still available in Application Insights for the usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="0d6e8-118"><a name="setup"></a> Créez une exportation continue.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="0d6e8-119">Dans la ressource Application Insights de votre application, ouvrez Exportation continue et choisissez **ajouter** :</span><span class="sxs-lookup"><span data-stu-id="0d6e8-119">In the Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![Faites défiler vers le bas, puis cliquez sur Exportation continue.](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="0d6e8-121">Choisissez les types de données de télémétrie que vous souhaitez exporter.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-121">Choose the telemetry data types you want to export.</span></span>

3. <span data-ttu-id="0d6e8-122">Créez ou sélectionnez le [compte de stockage Azure](../storage/common/storage-introduction.md) sur lequel vous voulez stocker les données.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want to store the data.</span></span>

    > [!Warning]
    > <span data-ttu-id="0d6e8-123">Par défaut, l’emplacement de stockage est défini dans la même région géographique que votre ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-123">By default, the storage location will be set to the same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="0d6e8-124">Si vous utilisez une autre région de stockage, vous risquez de subir des frais de transfert.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![Cliquez sur Ajouter, Destination de l’exportation, Compte de stockage, puis créez un nouveau magasin ou choisissez un magasin existant.](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="0d6e8-126">Créez ou sélectionnez un conteneur dans votre stockage :</span><span class="sxs-lookup"><span data-stu-id="0d6e8-126">Create or select a container in the storage:</span></span>

    ![Cliquez sur Choisir les types d’événements.](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="0d6e8-128">Une fois que vous avez créé l’exportation, elle démarre.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="0d6e8-129">Vous n’obtenez que les données qui arrivent après la création de l’exportation.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-129">You only get data that arrives after you create the export.</span></span>

<span data-ttu-id="0d6e8-130">Il peut y avoir un délai d'environ une heure avant que les données n’apparaissent dans le stockage.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-130">There can be a delay of about an hour before data appears in the storage.</span></span>

### <a name="to-edit-continuous-export"></a><span data-ttu-id="0d6e8-131">Pour modifier une exportation continue</span><span class="sxs-lookup"><span data-stu-id="0d6e8-131">To edit continuous export</span></span>

<span data-ttu-id="0d6e8-132">Si vous souhaitez modifier les types d’événement plus tard, modifiez simplement l’exportation :</span><span class="sxs-lookup"><span data-stu-id="0d6e8-132">If you want to change the event types later, just edit the export:</span></span>

![Cliquez sur Choisir les types d’événements.](./media/app-insights-export-telemetry/05-edit.png)

### <a name="to-stop-continuous-export"></a><span data-ttu-id="0d6e8-134">Pour suspendre une exportation continue</span><span class="sxs-lookup"><span data-stu-id="0d6e8-134">To stop continuous export</span></span>

<span data-ttu-id="0d6e8-135">Pour arrêter l’exportation, cliquez sur Désactiver.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-135">To stop the export, click Disable.</span></span> <span data-ttu-id="0d6e8-136">Lorsque vous cliquez de nouveau sur Activer, l’exportation redémarre avec de nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-136">When you click Enable again, the export will restart with new data.</span></span> <span data-ttu-id="0d6e8-137">Vous n’obtiendrez pas les données qui sont arrivées sur le portail alors que l’exportation était désactivée.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-137">You won't get the data that arrived in the portal while export was disabled.</span></span>

<span data-ttu-id="0d6e8-138">Pour arrêter définitivement l’exportation, supprimez-la simplement.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-138">To stop the export permanently, delete it.</span></span> <span data-ttu-id="0d6e8-139">Cette opération ne supprime pas vos données du stockage.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="0d6e8-140">Impossible d’ajouter ou de modifier une exportation ?</span><span class="sxs-lookup"><span data-stu-id="0d6e8-140">Can't add or change an export?</span></span>
* <span data-ttu-id="0d6e8-141">Pour ajouter ou modifier des exportations, vous devez disposer de droits d’accès de propriétaire, de collaborateur ou de collaborateur Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-141">To add or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="0d6e8-142">[En savoir plus sur les rôles][roles].</span><span class="sxs-lookup"><span data-stu-id="0d6e8-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="0d6e8-143"><a name="analyze"></a> Quels sont les événements que vous obtenez ?</span><span class="sxs-lookup"><span data-stu-id="0d6e8-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="0d6e8-144">Les données exportées sont les données de télémétrie brutes que nous recevons de votre application. Toutefois, nous ajoutons les données d’emplacement que nous calculons à partir de l’adresse IP du client.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-144">The exported data is the raw telemetry we receive from your application, except that we add location data which we calculate from the client IP address.</span></span>

<span data-ttu-id="0d6e8-145">Les données qui ont été ignorées par l’ [échantillonnage](app-insights-sampling.md) ne sont pas incluses dans les données exportées.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in the exported data.</span></span>

<span data-ttu-id="0d6e8-146">Les autres mesures calculées ne sont pas incluses.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="0d6e8-147">Par exemple, nous n’exportons pas l’utilisation moyenne du processeur, mais nous exportons la télémétrie brute à partir de laquelle la moyenne est calculée.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-147">For example, we don't export average CPU utilisation, but we do export the raw telemetry from which the average is computed.</span></span>

<span data-ttu-id="0d6e8-148">Les données incluent également les résultats de n’importe quel [test web de disponibilité](app-insights-monitor-web-app-availability.md) que vous avez configuré.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-148">The data also includes the results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="0d6e8-149">**Échantillonnage.**</span><span class="sxs-lookup"><span data-stu-id="0d6e8-149">**Sampling.**</span></span> <span data-ttu-id="0d6e8-150">Si votre application envoie beaucoup de données, la fonctionnalité d’échantillonnage peut fonctionner et envoyer seulement une partie des données de télémétrie générées.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-150">If your application sends a lot of data, the sampling feature may operate and send only a fraction of the generated telemetry.</span></span> [<span data-ttu-id="0d6e8-151">En savoir plus sur l'échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="0d6e8-152"><a name="get"></a> Inspection des données</span><span class="sxs-lookup"><span data-stu-id="0d6e8-152"><a name="get"></a> Inspect the data</span></span>
<span data-ttu-id="0d6e8-153">Vous pouvez inspecter le stockage directement sur le portail.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-153">You can inspect the storage directly in the portal.</span></span> <span data-ttu-id="0d6e8-154">Cliquez sur **Parcourir**, sélectionnez votre compte de stockage, puis ouvrez **Conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="0d6e8-155">Pour examiner le stockage Azure dans Visual Studio, ouvrez **Afficher**, **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-155">To inspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="0d6e8-156">(Si vous n’avez pas cette commande, vous devez installer le Kit de développement logiciel (SDK) Azure : ouvrez la boîte de dialogue **Nouveau projet**, développez Visual C#/Cloud et sélectionnez **Obtenir Microsoft Azure SDK pour .NET**.)</span><span class="sxs-lookup"><span data-stu-id="0d6e8-156">(If you don't have that menu command, you need to install the Azure SDK: Open the **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="0d6e8-157">Lorsque vous ouvrez votre magasin d’objets blob, vous voyez un conteneur avec un ensemble de fichiers blob.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="0d6e8-158">L'URI de chaque fichier est dérivé du nom de votre ressource Application Insights, sa clé d'instrumentation, le type/la date/l'heure de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-158">The URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="0d6e8-159">(Le nom de la ressource est tout en minuscules et la clé d'instrumentation omet les tirets.)</span><span class="sxs-lookup"><span data-stu-id="0d6e8-159">(The resource name is all lowercase, and the instrumentation key omits dashes.)</span></span>

![Inspectez le magasin d’objets blob avec un outil adapté.](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="0d6e8-161">La date et l’heure sont au format UTC et correspondent au moment où la télémétrie a été placée dans le magasin, et pas au moment où elle a été générée.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-161">The date and time are UTC and are when the telemetry was deposited in the store - not the time it was generated.</span></span> <span data-ttu-id="0d6e8-162">Par conséquent, si vous écrivez du code pour télécharger les données, il peut parcourir les données de façon linéaire.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-162">So if you write code to download the data, it can move linearly through the data.</span></span>

<span data-ttu-id="0d6e8-163">Voici le format du chemin d’accès :</span><span class="sxs-lookup"><span data-stu-id="0d6e8-163">Here's the form of the path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="0d6e8-164">Where</span><span class="sxs-lookup"><span data-stu-id="0d6e8-164">Where</span></span>

* <span data-ttu-id="0d6e8-165">`blobCreationTimeUtc` est l’heure de création de l’objet blob dans le stockage intermédiaire interne</span><span class="sxs-lookup"><span data-stu-id="0d6e8-165">`blobCreationTimeUtc` is time when blob was created in the internal staging storage</span></span>
* <span data-ttu-id="0d6e8-166">`blobDeliveryTimeUtc` est l’heure de copie de l’objet blob vers le stockage de destination d’exportation</span><span class="sxs-lookup"><span data-stu-id="0d6e8-166">`blobDeliveryTimeUtc` is the time when blob is copied to the export destination storage</span></span>

## <span data-ttu-id="0d6e8-167"><a name="format"></a> Format de données</span><span class="sxs-lookup"><span data-stu-id="0d6e8-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="0d6e8-168">Chaque objet blob est un fichier texte qui contient plusieurs lignes séparées par des \n.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="0d6e8-169">Il contient les données de télémétrie traitées sur une période de trente secondes environ.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-169">It contains the telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="0d6e8-170">Chaque ligne représente un point de données de télémétrie, par exemple une demande ou un affichage de page.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="0d6e8-171">Chaque ligne est un document JSON sans mise en forme.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="0d6e8-172">Si vous souhaitez l'examiner, ouvrez-le dans Visual Studio et choisissez Modifier, Options avancées, Formater le fichier :</span><span class="sxs-lookup"><span data-stu-id="0d6e8-172">If you want to sit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![Consultez la télémétrie avec un outil approprié.](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="0d6e8-174">Les durées sont exprimées en nombre de cycles, où 10 000 cycles = 1 ms.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="0d6e8-175">Par exemple, ces valeurs indiquent une durée de 1 ms pour envoyer une demande à partir du navigateur, 3 ms pour la recevoir et 1,8 s pour traiter la page dans le navigateur :</span><span class="sxs-lookup"><span data-stu-id="0d6e8-175">For example, these values show a time of 1ms to send a request from the browser, 3ms to receive it, and 1.8s to process the page in the browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="0d6e8-176">Référence de modèle de données détaillé pour les valeurs et types de propriétés.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-176">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-the-data"></a><span data-ttu-id="0d6e8-177">Traitement des données</span><span class="sxs-lookup"><span data-stu-id="0d6e8-177">Processing the data</span></span>
<span data-ttu-id="0d6e8-178">À petite échelle, vous pouvez écrire du code pour décomposer vos données, les lire dans une feuille de calcul et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-178">On a small scale, you can write some code to pull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="0d6e8-179">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="0d6e8-179">For example:</span></span>

    private IEnumerable<T> DeserializeMany<T>(string folderName)
    {
      var files = Directory.EnumerateFiles(folderName, "*.blob", SearchOption.AllDirectories);
      foreach (var file in files)
      {
         using (var fileReader = File.OpenText(file))
         {
            string fileContent = fileReader.ReadToEnd();
            IEnumerable<string> entities = fileContent.Split('\n').Where(s => !string.IsNullOrWhiteSpace(s));
            foreach (var entity in entities)
            {
                yield return JsonConvert.DeserializeObject<T>(entity);
            }
         }
      }
    }

<span data-ttu-id="0d6e8-180">Pour un exemple de code plus long, consultez [Utilisation d’un rôle de travail][exportasa].</span><span class="sxs-lookup"><span data-stu-id="0d6e8-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="0d6e8-181"><a name="delete"></a>Supprimer les anciennes données</span><span class="sxs-lookup"><span data-stu-id="0d6e8-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="0d6e8-182">Notez que vous êtes responsable de la gestion de votre capacité de stockage et de la suppression des anciennes données si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-182">Please note that you are responsible for managing your storage capacity and deleting the old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="0d6e8-183">Si vous régénérez votre clé de stockage...</span><span class="sxs-lookup"><span data-stu-id="0d6e8-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="0d6e8-184">Si vous modifiez la clé de votre stockage, l’exportation continue cesse de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-184">If you change the key to your storage, continuous export will stop working.</span></span> <span data-ttu-id="0d6e8-185">Vous voyez alors une notification dans votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="0d6e8-186">Ouvrez le panneau Exportation continue et modifiez votre exportation.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-186">Open the Continuous Export blade and edit your export.</span></span> <span data-ttu-id="0d6e8-187">Modifiez la destination de l’exportation, mais laissez le même stockage sélectionné.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-187">Edit the Export Destination, but just leave the same storage selected.</span></span> <span data-ttu-id="0d6e8-188">Cliquez sur OK pour confirmer.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-188">Click OK to confirm.</span></span>

![Modifiez l’exportation continue, ouvrez puis fermez la destination de l’exportation.](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="0d6e8-190">L’exportation continue redémarre.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-190">The continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="0d6e8-191">Exemples d’exportation</span><span class="sxs-lookup"><span data-stu-id="0d6e8-191">Export samples</span></span>

* <span data-ttu-id="0d6e8-192">[Exporter vers SQL à l’aide de Stream Analytics][exportasa]</span><span class="sxs-lookup"><span data-stu-id="0d6e8-192">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="0d6e8-193">Stream Analytics - Exemple 2</span><span class="sxs-lookup"><span data-stu-id="0d6e8-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="0d6e8-194">À plus grande échelle, envisagez d’utiliser des clusters [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in the cloud.</span></span> <span data-ttu-id="0d6e8-195">HDInsight propose de nombreuses technologies pour gérer et analyser Big Data, et vous pouvez l’utiliser pour traiter les données qui ont été exportées depuis Application Insights.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it to process data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="0d6e8-196">Questions et réponses</span><span class="sxs-lookup"><span data-stu-id="0d6e8-196">Q & A</span></span>
* <span data-ttu-id="0d6e8-197">*Je veux simplement télécharger un graphique.*</span><span class="sxs-lookup"><span data-stu-id="0d6e8-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="0d6e8-198">Oui, vous pouvez le faire.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-198">Yes, you can do that.</span></span> <span data-ttu-id="0d6e8-199">En haut du panneau, cliquez sur **Exporter les données**.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-199">At the top of the blade, click **Export Data**.</span></span>
* <span data-ttu-id="0d6e8-200">*J’ai configuré une exportation, mais il n’y a pas de données dans mon magasin.*</span><span class="sxs-lookup"><span data-stu-id="0d6e8-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="0d6e8-201">Application Insights a-t-il reçu de la télémétrie de votre application depuis que vous avez configuré l’exportation ?</span><span class="sxs-lookup"><span data-stu-id="0d6e8-201">Did Application Insights receive any telemetry from your app since you set up the export?</span></span> <span data-ttu-id="0d6e8-202">Vous recevrez uniquement les nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-202">You'll only receive new data.</span></span>
* <span data-ttu-id="0d6e8-203">*J’ai essayé de configurer une exportation, mais l’accès lui a été refusé.*</span><span class="sxs-lookup"><span data-stu-id="0d6e8-203">*I tried to set up an export, but was denied access*</span></span>

    <span data-ttu-id="0d6e8-204">Si le compte appartient à votre organisation, vous devez être membre du groupe des propriétaires ou des collaborateurs.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-204">If the account is owned by your organization, you have to be a member of the owners or contributors groups.</span></span>
* <span data-ttu-id="0d6e8-205">*Puis-je exporter directement vers mon propre magasin local ?*</span><span class="sxs-lookup"><span data-stu-id="0d6e8-205">*Can I export straight to my own on-premises store?*</span></span>

    <span data-ttu-id="0d6e8-206">Non.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-206">No, sorry.</span></span> <span data-ttu-id="0d6e8-207">Pour le moment, notre moteur d’exportation fonctionne uniquement avec le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="0d6e8-208">*Existe-t-il une limite à la quantité de données qu’il est possible de placer dans mon magasin ?*</span><span class="sxs-lookup"><span data-stu-id="0d6e8-208">*Is there any limit to the amount of data you put in my store?*</span></span>

    <span data-ttu-id="0d6e8-209">Non.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-209">No.</span></span> <span data-ttu-id="0d6e8-210">Nous transmettons les données jusqu’à ce que vous supprimiez l’exportation.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-210">We'll keep pushing data in until you delete the export.</span></span> <span data-ttu-id="0d6e8-211">Nous arrêtons si nous atteignons les limites extérieures du stockage d’objets blob, mais ceci représente un volume très important.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-211">We'll stop if we hit the outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="0d6e8-212">C’est à vous de contrôler la quantité de stockage vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-212">It's up to you to control how much storage you use.</span></span>  
* <span data-ttu-id="0d6e8-213">*Combien d’objets blob devrais-je voir dans le stockage ?*</span><span class="sxs-lookup"><span data-stu-id="0d6e8-213">*How many blobs should I see in the storage?*</span></span>

  * <span data-ttu-id="0d6e8-214">Pour chaque type de données que vous avez choisi d'exporter un objet blob est créé toutes les minutes (si les données sont disponibles).</span><span class="sxs-lookup"><span data-stu-id="0d6e8-214">For every data type you selected to export, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="0d6e8-215">En outre, pour les applications avec un trafic élevé, des unités de partition supplémentaires sont allouées.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="0d6e8-216">Dans ce cas, chaque unité crée un objet blob toutes les minutes.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="0d6e8-217">*J’ai régénéré la clé de mon espace de stockage ou modifié le nom du conteneur et l’exportation ne fonctionne plus.*</span><span class="sxs-lookup"><span data-stu-id="0d6e8-217">*I regenerated the key to my storage or changed the name of the container, and now the export doesn't work.*</span></span>

    <span data-ttu-id="0d6e8-218">Modifiez l’exportation et ouvrez le panneau de destination d’exportation.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-218">Edit the export and open the export destination blade.</span></span> <span data-ttu-id="0d6e8-219">Conservez le même stockage que celui sélectionné auparavant, puis cliquez sur OK pour confirmer.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-219">Leave the same storage selected as before, and click OK to confirm.</span></span> <span data-ttu-id="0d6e8-220">L’exportation redémarre.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-220">Export will restart.</span></span> <span data-ttu-id="0d6e8-221">Si la modification a eu lieu dans les derniers jours, vous ne perdrez pas de données.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-221">If the change was within the past few days, you won't lose data.</span></span>
* <span data-ttu-id="0d6e8-222">*Est-il possible de suspendre l’exportation ?*</span><span class="sxs-lookup"><span data-stu-id="0d6e8-222">*Can I pause the export?*</span></span>

    <span data-ttu-id="0d6e8-223">Oui.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-223">Yes.</span></span> <span data-ttu-id="0d6e8-224">Cliquez sur Désactiver.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="0d6e8-225">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="0d6e8-225">Code samples</span></span>

* [<span data-ttu-id="0d6e8-226">Stream Analytics - Exemple</span><span class="sxs-lookup"><span data-stu-id="0d6e8-226">Stream Analytics sample</span></span>](app-insights-export-stream-analytics.md)
* <span data-ttu-id="0d6e8-227">[Exporter vers SQL à l’aide de Stream Analytics][exportasa]</span><span class="sxs-lookup"><span data-stu-id="0d6e8-227">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="0d6e8-228">Référence de modèle de données détaillé pour les valeurs et types de propriétés.</span><span class="sxs-lookup"><span data-stu-id="0d6e8-228">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
