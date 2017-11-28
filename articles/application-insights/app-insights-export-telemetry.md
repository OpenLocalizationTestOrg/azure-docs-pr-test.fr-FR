---
title: "exportation d’aaaContinuous de télémétrie d’Application Insights | Documents Microsoft"
description: "Exporter toostorage de données de diagnostic et d’utilisation dans Microsoft Azure et la télécharger à partir de là."
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
ms.openlocfilehash: be9ed7e05922c1c8186df9ca4e642862adaa5fd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="ebbb8-103">Exporter la télémétrie depuis Application Insights</span><span class="sxs-lookup"><span data-stu-id="ebbb8-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="ebbb8-104">Vous souhaitez tookeep votre télémétrie plus longue que la période de rétention standard hello ?</span><span class="sxs-lookup"><span data-stu-id="ebbb8-104">Want tookeep your telemetry for longer than hello standard retention period?</span></span> <span data-ttu-id="ebbb8-105">Ou la traiter d’une façon spécialisée ?</span><span class="sxs-lookup"><span data-stu-id="ebbb8-105">Or process it in some specialized way?</span></span> <span data-ttu-id="ebbb8-106">L’exportation continue est idéale dans ce cas.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="ebbb8-107">événements Hello que vous voyez dans le portail d’Application Insights hello peuvent être exporté toostorage dans Microsoft Azure au format JSON.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-107">hello events you see in hello Application Insights portal can be exported toostorage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="ebbb8-108">À partir de là, vous pouvez télécharger vos données et écrire tout code que vous avez besoin de tooprocess il.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-108">From there you can download your data and write whatever code you need tooprocess it.</span></span>  

<span data-ttu-id="ebbb8-109">L’utilisation de l’exportation continue peut entraîner des frais supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="ebbb8-110">Consultez votre [modèle de tarification](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="ebbb8-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="ebbb8-111">Avant de configurer l’exportation continue, il existe des alternatives souhaité tooconsider :</span><span class="sxs-lookup"><span data-stu-id="ebbb8-111">Before you set up continuous export, there are some alternatives you might want tooconsider:</span></span>

* <span data-ttu-id="ebbb8-112">Hello bouton Exporter situé en haut hello un panneau metrics ou recherche permet de transférer des tables et graphiques de feuille de calcul de Excel de tooan.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-112">hello Export button at hello top of a metrics or search blade lets you transfer tables and charts tooan Excel spreadsheet.</span></span>

* <span data-ttu-id="ebbb8-113">[Analytics](app-insights-analytics.md) fournit un puissant langage de requête pour la télémétrie</span><span class="sxs-lookup"><span data-stu-id="ebbb8-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="ebbb8-114">et peut également en exporter les résultats.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-114">It can also export results.</span></span>
* <span data-ttu-id="ebbb8-115">Si vous envisagez d’utiliser trop[Explorer vos données dans Power BI](app-insights-export-power-bi.md), vous pouvez le faire sans l’aide de l’exportation continue.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-115">If you're looking too[explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="ebbb8-116">Hello [API REST d’accès aux données](https://dev.applicationinsights.io/) vous permet d’accéder par programmation de votre télémétrie.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-116">hello [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="ebbb8-117">Une fois l’exportation continue copie votre toostorage de données (où elle peut rester pour aussi longtemps que vous le souhaitez), il est toujours disponible dans Application Insights pour hello habituel [période de rétention](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="ebbb8-117">After Continuous Export copies your data toostorage (where it can stay for as long as you like), it's still available in Application Insights for hello usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="ebbb8-118"><a name="setup"></a> Créez une exportation continue.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="ebbb8-119">Bonjour ressource Application Insights pour votre application, ouvrez l’exportation continue et choisissez **ajouter**:</span><span class="sxs-lookup"><span data-stu-id="ebbb8-119">In hello Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![Faites défiler vers le bas, puis cliquez sur Exportation continue.](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="ebbb8-121">Choisissez des types de données de télémétrie de hello souhaité tooexport.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-121">Choose hello telemetry data types you want tooexport.</span></span>

3. <span data-ttu-id="ebbb8-122">Créez ou sélectionnez un [compte de stockage Azure](../storage/common/storage-introduction.md) où vous souhaitez toostore hello données.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want toostore hello data.</span></span>

    > [!Warning]
    > <span data-ttu-id="ebbb8-123">Par défaut, emplacement de stockage hello définira toohello même région géographique que votre ressource Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-123">By default, hello storage location will be set toohello same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="ebbb8-124">Si vous utilisez une autre région de stockage, vous risquez de subir des frais de transfert.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![Cliquez sur Ajouter, Destination de l’exportation, Compte de stockage, puis créez un nouveau magasin ou choisissez un magasin existant.](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="ebbb8-126">Créez ou sélectionnez un conteneur dans le stockage hello :</span><span class="sxs-lookup"><span data-stu-id="ebbb8-126">Create or select a container in hello storage:</span></span>

    ![Cliquez sur Choisir les types d’événements.](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="ebbb8-128">Une fois que vous avez créé l’exportation, elle démarre.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="ebbb8-129">Vous obtenez uniquement les données qui arrive après avoir créé l’exportation de hello.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-129">You only get data that arrives after you create hello export.</span></span>

<span data-ttu-id="ebbb8-130">Il peut y avoir un délai d’environ une heure avant que les données s’affichent dans le stockage hello.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-130">There can be a delay of about an hour before data appears in hello storage.</span></span>

### <a name="tooedit-continuous-export"></a><span data-ttu-id="ebbb8-131">exportation continue de tooedit</span><span class="sxs-lookup"><span data-stu-id="ebbb8-131">tooedit continuous export</span></span>

<span data-ttu-id="ebbb8-132">Si vous souhaitez que les types d’événements toochange hello plus tard, modifiez l’exportation de hello :</span><span class="sxs-lookup"><span data-stu-id="ebbb8-132">If you want toochange hello event types later, just edit hello export:</span></span>

![Cliquez sur Choisir les types d’événements.](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a><span data-ttu-id="ebbb8-134">exportation continue de toostop</span><span class="sxs-lookup"><span data-stu-id="ebbb8-134">toostop continuous export</span></span>

<span data-ttu-id="ebbb8-135">exportation de hello toostop, cliquez sur Désactiver.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-135">toostop hello export, click Disable.</span></span> <span data-ttu-id="ebbb8-136">Lorsque vous cliquez sur Activer à nouveau, exportation de hello redémarre avec de nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-136">When you click Enable again, hello export will restart with new data.</span></span> <span data-ttu-id="ebbb8-137">Vous n’obtiendrez données hello reçus dans le portail de hello lors de l’exportation a été désactivée.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-137">You won't get hello data that arrived in hello portal while export was disabled.</span></span>

<span data-ttu-id="ebbb8-138">exportation de hello toostop définitivement, supprimez-le.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-138">toostop hello export permanently, delete it.</span></span> <span data-ttu-id="ebbb8-139">Cette opération ne supprime pas vos données du stockage.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="ebbb8-140">Impossible d’ajouter ou de modifier une exportation ?</span><span class="sxs-lookup"><span data-stu-id="ebbb8-140">Can't add or change an export?</span></span>
* <span data-ttu-id="ebbb8-141">exportations tooadd ou de modification, vous devez propriétaire, collaborateur ou Application Insights collaborateurs des droits d’accès.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-141">tooadd or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="ebbb8-142">[En savoir plus sur les rôles][roles].</span><span class="sxs-lookup"><span data-stu-id="ebbb8-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="ebbb8-143"><a name="analyze"></a> Quels sont les événements que vous obtenez ?</span><span class="sxs-lookup"><span data-stu-id="ebbb8-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="ebbb8-144">Hello données exportées sont brutes de télémesure hello que nous recevons de votre application, sauf que nous ajoutons à laquelle il convient de calculer les données d’emplacement à partir de l’adresse IP du client hello.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-144">hello exported data is hello raw telemetry we receive from your application, except that we add location data which we calculate from hello client IP address.</span></span>

<span data-ttu-id="ebbb8-145">Les données qui a été rejetées par [échantillonnage](app-insights-sampling.md) n’est pas inclus dans les données de salutation exportée.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in hello exported data.</span></span>

<span data-ttu-id="ebbb8-146">Les autres mesures calculées ne sont pas incluses.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="ebbb8-147">Par exemple, nous ne pas exporter une utilisation moyenne de l’UC, mais nous exportez brutes de télémesure hello à partir de laquelle la moyenne de hello est calculée.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-147">For example, we don't export average CPU utilisation, but we do export hello raw telemetry from which hello average is computed.</span></span>

<span data-ttu-id="ebbb8-148">Hello données incluent également des résultats de n’importe quel hello [disponibilité des tests web](app-insights-monitor-web-app-availability.md) que vous avez définis.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-148">hello data also includes hello results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="ebbb8-149">**Échantillonnage.**</span><span class="sxs-lookup"><span data-stu-id="ebbb8-149">**Sampling.**</span></span> <span data-ttu-id="ebbb8-150">Si votre application envoie une grande quantité de données, fonctionnalité d’échantillonnage hello peut fonctionner et envoyer qu’une fraction des données de télémétrie hello généré.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-150">If your application sends a lot of data, hello sampling feature may operate and send only a fraction of hello generated telemetry.</span></span> [<span data-ttu-id="ebbb8-151">En savoir plus sur l’échantillonnage.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="ebbb8-152"><a name="get"></a>Inspecter les données de hello</span><span class="sxs-lookup"><span data-stu-id="ebbb8-152"><a name="get"></a> Inspect hello data</span></span>
<span data-ttu-id="ebbb8-153">Vous pouvez inspecter stockage hello directement dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-153">You can inspect hello storage directly in hello portal.</span></span> <span data-ttu-id="ebbb8-154">Cliquez sur **Parcourir**, sélectionnez votre compte de stockage, puis ouvrez **Conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="ebbb8-155">tooinspect stockage Azure dans Visual Studio, ouvrez **vue**, **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-155">tooinspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="ebbb8-156">(Si vous n’avez pas cette commande de menu, vous devez tooinstall hello Azure SDK : hello ouvrir **nouveau projet** boîte de dialogue, développez Visual C# / Cloud et choisissez **obtenir Microsoft Azure SDK pour .NET**.)</span><span class="sxs-lookup"><span data-stu-id="ebbb8-156">(If you don't have that menu command, you need tooinstall hello Azure SDK: Open hello **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="ebbb8-157">Lorsque vous ouvrez votre magasin d’objets blob, vous voyez un conteneur avec un ensemble de fichiers blob.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="ebbb8-158">Hello URI de chaque fichier dérivé de votre nom de la ressource Application Insights, sa clé d’instrumentation, la télémétrie-type/date/heure.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-158">hello URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="ebbb8-159">(nom de la ressource hello est en minuscule et clé d’instrumentation hello omet les tirets).</span><span class="sxs-lookup"><span data-stu-id="ebbb8-159">(hello resource name is all lowercase, and hello instrumentation key omits dashes.)</span></span>

![Inspecter le magasin d’objets blob hello avec un outil approprié](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="ebbb8-161">hello date et heure sont UTC et quand les données de télémétrie hello a été déposée dans le magasin de hello, pas les temps de hello a été généré.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-161">hello date and time are UTC and are when hello telemetry was deposited in hello store - not hello time it was generated.</span></span> <span data-ttu-id="ebbb8-162">Par conséquent, si vous écrivez des données de code toodownload hello, il peut parcourir linéairement hello données.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-162">So if you write code toodownload hello data, it can move linearly through hello data.</span></span>

<span data-ttu-id="ebbb8-163">Voici l’écran hello du chemin d’accès hello :</span><span class="sxs-lookup"><span data-stu-id="ebbb8-163">Here's hello form of hello path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="ebbb8-164">Where</span><span class="sxs-lookup"><span data-stu-id="ebbb8-164">Where</span></span>

* <span data-ttu-id="ebbb8-165">`blobCreationTimeUtc`heure de blob création Bonjour interne est mis en œuvre stockage</span><span class="sxs-lookup"><span data-stu-id="ebbb8-165">`blobCreationTimeUtc` is time when blob was created in hello internal staging storage</span></span>
* <span data-ttu-id="ebbb8-166">`blobDeliveryTimeUtc`est hello heure d’objet blob de stockage de destination d’exportation toohello copiés</span><span class="sxs-lookup"><span data-stu-id="ebbb8-166">`blobDeliveryTimeUtc` is hello time when blob is copied toohello export destination storage</span></span>

## <span data-ttu-id="ebbb8-167"><a name="format"></a> Format de données</span><span class="sxs-lookup"><span data-stu-id="ebbb8-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="ebbb8-168">Chaque objet blob est un fichier texte qui contient plusieurs lignes séparées par des \n.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="ebbb8-169">Il contient la télémétrie hello traitée sur une période d’environ la moitié d’une minute.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-169">It contains hello telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="ebbb8-170">Chaque ligne représente un point de données de télémétrie, par exemple une demande ou un affichage de page.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="ebbb8-171">Chaque ligne est un document JSON sans mise en forme.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="ebbb8-172">Si vous souhaitez toosit et vous fixez il, ouvrez dans Visual Studio et choisissez Modifier, options avancées, fichier de Format :</span><span class="sxs-lookup"><span data-stu-id="ebbb8-172">If you want toosit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![Télémétrie des consultations de hello avec un outil approprié](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="ebbb8-174">Les durées sont exprimées en nombre de cycles, où 10 000 cycles = 1 ms.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="ebbb8-175">Par exemple, ces valeurs indiquent un temps de 1 MS toosend une demande de navigateur hello, 3ms tooreceive et 1.8s tooprocess hello page dans le navigateur de hello :</span><span class="sxs-lookup"><span data-stu-id="ebbb8-175">For example, these values show a time of 1ms toosend a request from hello browser, 3ms tooreceive it, and 1.8s tooprocess hello page in hello browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="ebbb8-176">Informations de référence pour les types de propriété hello et les valeurs de modèle de données détaillées.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-176">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a><span data-ttu-id="ebbb8-177">Le traitement des données de hello</span><span class="sxs-lookup"><span data-stu-id="ebbb8-177">Processing hello data</span></span>
<span data-ttu-id="ebbb8-178">À petite échelle, vous pouvez écrire certaines toopull code séparer vos données, lire dans une feuille de calcul et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-178">On a small scale, you can write some code toopull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="ebbb8-179">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="ebbb8-179">For example:</span></span>

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

<span data-ttu-id="ebbb8-180">Pour un exemple de code plus long, consultez [Utilisation d’un rôle de travail][exportasa].</span><span class="sxs-lookup"><span data-stu-id="ebbb8-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="ebbb8-181"><a name="delete"></a>Supprimer les anciennes données</span><span class="sxs-lookup"><span data-stu-id="ebbb8-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="ebbb8-182">Notez que vous êtes responsable de la gestion de votre capacité de stockage et la suppression des anciennes données de hello si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-182">Please note that you are responsible for managing your storage capacity and deleting hello old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="ebbb8-183">Si vous régénérez votre clé de stockage...</span><span class="sxs-lookup"><span data-stu-id="ebbb8-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="ebbb8-184">Si vous modifiez le stockage de clés tooyour hello, exportation continue cesseront de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-184">If you change hello key tooyour storage, continuous export will stop working.</span></span> <span data-ttu-id="ebbb8-185">Vous voyez alors une notification dans votre compte Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="ebbb8-186">Ouvrir le panneau de l’exportation continue hello et modifier l’exportation.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-186">Open hello Continuous Export blade and edit your export.</span></span> <span data-ttu-id="ebbb8-187">Modifier hello Destination d’exportation, mais laissez hello même stockage sélectionné.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-187">Edit hello Export Destination, but just leave hello same storage selected.</span></span> <span data-ttu-id="ebbb8-188">Cliquez sur OK tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-188">Click OK tooconfirm.</span></span>

![Hello modifier continue exporter, ouvrir et fermer les trois destination de l’exportation.](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="ebbb8-190">exportation continue de Hello redémarre.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-190">hello continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="ebbb8-191">Exemples d’exportation</span><span class="sxs-lookup"><span data-stu-id="ebbb8-191">Export samples</span></span>

* <span data-ttu-id="ebbb8-192">[TooSQL d’exportation à l’aide de flux de données Analytique][exportasa]</span><span class="sxs-lookup"><span data-stu-id="ebbb8-192">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="ebbb8-193">Stream Analytics - Exemple 2</span><span class="sxs-lookup"><span data-stu-id="ebbb8-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="ebbb8-194">Sur les échelles plus volumineux, envisagez [HDInsight](https://azure.microsoft.com/services/hdinsight/) -Hadoop de clusters dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in hello cloud.</span></span> <span data-ttu-id="ebbb8-195">HDInsight fournit un éventail de technologies destinées à gérer et analyser les données volumineuses, et vous pouvez l’utiliser dans les données tooprocess qui a été exportées à partir de l’Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it tooprocess data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="ebbb8-196">Questions et réponses</span><span class="sxs-lookup"><span data-stu-id="ebbb8-196">Q & A</span></span>
* <span data-ttu-id="ebbb8-197">*Je veux simplement télécharger un graphique.*</span><span class="sxs-lookup"><span data-stu-id="ebbb8-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="ebbb8-198">Oui, vous pouvez le faire.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-198">Yes, you can do that.</span></span> <span data-ttu-id="ebbb8-199">Haut hello du Panneau de hello, cliquez sur **exporter les données**.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-199">At hello top of hello blade, click **Export Data**.</span></span>
* <span data-ttu-id="ebbb8-200">*J’ai configuré une exportation, mais il n’y a pas de données dans mon magasin.*</span><span class="sxs-lookup"><span data-stu-id="ebbb8-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="ebbb8-201">Application Insights reçue toutes les données de télémétrie de votre application dans la mesure où vous configurez l’exportation de hello ?</span><span class="sxs-lookup"><span data-stu-id="ebbb8-201">Did Application Insights receive any telemetry from your app since you set up hello export?</span></span> <span data-ttu-id="ebbb8-202">Vous recevrez uniquement les nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-202">You'll only receive new data.</span></span>
* <span data-ttu-id="ebbb8-203">*J’ai essayé tooset une exportation, mais a refusé l’accès*</span><span class="sxs-lookup"><span data-stu-id="ebbb8-203">*I tried tooset up an export, but was denied access*</span></span>

    <span data-ttu-id="ebbb8-204">Si le compte de hello est détenu par votre organisation, vous avez toobe un membre des groupes de propriétaires ou collaborateurs hello.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-204">If hello account is owned by your organization, you have toobe a member of hello owners or contributors groups.</span></span>
* <span data-ttu-id="ebbb8-205">*Puis-je exporter toomy droite propre banque locale ?*</span><span class="sxs-lookup"><span data-stu-id="ebbb8-205">*Can I export straight toomy own on-premises store?*</span></span>

    <span data-ttu-id="ebbb8-206">Non.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-206">No, sorry.</span></span> <span data-ttu-id="ebbb8-207">Pour le moment, notre moteur d’exportation fonctionne uniquement avec le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="ebbb8-208">*Existe-t-il un volume de données de que vous placer dans le magasin my toohello limite ?*</span><span class="sxs-lookup"><span data-stu-id="ebbb8-208">*Is there any limit toohello amount of data you put in my store?*</span></span>

    <span data-ttu-id="ebbb8-209">Non.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-209">No.</span></span> <span data-ttu-id="ebbb8-210">Nous allons conserver transmettre des données jusqu'à ce que vous supprimiez exportation de hello.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-210">We'll keep pushing data in until you delete hello export.</span></span> <span data-ttu-id="ebbb8-211">Nous allons arrêter si nous avons atteint la limite extérieure de hello pour le stockage d’objets blob, mais c’est assez volumineux.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-211">We'll stop if we hit hello outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="ebbb8-212">C’est tooyou toocontrol vous utilisez la quantité de stockage.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-212">It's up tooyou toocontrol how much storage you use.</span></span>  
* <span data-ttu-id="ebbb8-213">*Objets BLOB combien dois-je voir dans le stockage hello ?*</span><span class="sxs-lookup"><span data-stu-id="ebbb8-213">*How many blobs should I see in hello storage?*</span></span>

  * <span data-ttu-id="ebbb8-214">Pour toutes les données, vous tapez tooexport sélectionnée, un nouvel objet blob est créé chaque minute (si les données sont disponibles).</span><span class="sxs-lookup"><span data-stu-id="ebbb8-214">For every data type you selected tooexport, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="ebbb8-215">En outre, pour les applications avec un trafic élevé, des unités de partition supplémentaires sont allouées.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="ebbb8-216">Dans ce cas, chaque unité crée un objet blob toutes les minutes.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="ebbb8-217">*Je régénérées de stockage de clés toomy hello ou modifié nom hello du conteneur de hello et exportation de hello ne fonctionne pas.*</span><span class="sxs-lookup"><span data-stu-id="ebbb8-217">*I regenerated hello key toomy storage or changed hello name of hello container, and now hello export doesn't work.*</span></span>

    <span data-ttu-id="ebbb8-218">Modifier l’exportation de hello et ouvrez le panneau de destination d’exportation hello.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-218">Edit hello export and open hello export destination blade.</span></span> <span data-ttu-id="ebbb8-219">Laissez hello même stockage sélectionnée comme précédemment, puis cliquez sur OK tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-219">Leave hello same storage selected as before, and click OK tooconfirm.</span></span> <span data-ttu-id="ebbb8-220">L’exportation redémarre.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-220">Export will restart.</span></span> <span data-ttu-id="ebbb8-221">Si les modifications hello était dans hello au-delà de quelques jours, vous ne perdrez les données.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-221">If hello change was within hello past few days, you won't lose data.</span></span>
* <span data-ttu-id="ebbb8-222">*Puis-je suspendre exportation de hello ?*</span><span class="sxs-lookup"><span data-stu-id="ebbb8-222">*Can I pause hello export?*</span></span>

    <span data-ttu-id="ebbb8-223">Oui.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-223">Yes.</span></span> <span data-ttu-id="ebbb8-224">Cliquez sur Désactiver.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="ebbb8-225">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="ebbb8-225">Code samples</span></span>

* [<span data-ttu-id="ebbb8-226">Stream Analytics - Exemple</span><span class="sxs-lookup"><span data-stu-id="ebbb8-226">Stream Analytics sample</span></span>](app-insights-export-stream-analytics.md)
* <span data-ttu-id="ebbb8-227">[TooSQL d’exportation à l’aide de flux de données Analytique][exportasa]</span><span class="sxs-lookup"><span data-stu-id="ebbb8-227">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="ebbb8-228">Informations de référence pour les types de propriété hello et les valeurs de modèle de données détaillées.</span><span class="sxs-lookup"><span data-stu-id="ebbb8-228">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
