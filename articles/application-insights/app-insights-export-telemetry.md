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
# <a name="export-telemetry-from-application-insights"></a>Exporter la télémétrie depuis Application Insights
Vous souhaitez tookeep votre télémétrie plus longue que la période de rétention standard hello ? Ou la traiter d’une façon spécialisée ? L’exportation continue est idéale dans ce cas. événements Hello que vous voyez dans le portail d’Application Insights hello peuvent être exporté toostorage dans Microsoft Azure au format JSON. À partir de là, vous pouvez télécharger vos données et écrire tout code que vous avez besoin de tooprocess il.  

L’utilisation de l’exportation continue peut entraîner des frais supplémentaires. Consultez votre [modèle de tarification](http://azure.microsoft.com/pricing/details/application-insights/).

Avant de configurer l’exportation continue, il existe des alternatives souhaité tooconsider :

* Hello bouton Exporter situé en haut hello un panneau metrics ou recherche permet de transférer des tables et graphiques de feuille de calcul de Excel de tooan.

* [Analytics](app-insights-analytics.md) fournit un puissant langage de requête pour la télémétrie et peut également en exporter les résultats.
* Si vous envisagez d’utiliser trop[Explorer vos données dans Power BI](app-insights-export-power-bi.md), vous pouvez le faire sans l’aide de l’exportation continue.
* Hello [API REST d’accès aux données](https://dev.applicationinsights.io/) vous permet d’accéder par programmation de votre télémétrie.

Une fois l’exportation continue copie votre toostorage de données (où elle peut rester pour aussi longtemps que vous le souhaitez), il est toujours disponible dans Application Insights pour hello habituel [période de rétention](app-insights-data-retention-privacy.md).

## <a name="setup"></a> Créez une exportation continue.
1. Bonjour ressource Application Insights pour votre application, ouvrez l’exportation continue et choisissez **ajouter**:

    ![Faites défiler vers le bas, puis cliquez sur Exportation continue.](./media/app-insights-export-telemetry/01-export.png)

2. Choisissez des types de données de télémétrie de hello souhaité tooexport.

3. Créez ou sélectionnez un [compte de stockage Azure](../storage/common/storage-introduction.md) où vous souhaitez toostore hello données.

    > [!Warning]
    > Par défaut, emplacement de stockage hello définira toohello même région géographique que votre ressource Application Insights. Si vous utilisez une autre région de stockage, vous risquez de subir des frais de transfert.

    ![Cliquez sur Ajouter, Destination de l’exportation, Compte de stockage, puis créez un nouveau magasin ou choisissez un magasin existant.](./media/app-insights-export-telemetry/02-add.png)

4. Créez ou sélectionnez un conteneur dans le stockage hello :

    ![Cliquez sur Choisir les types d’événements.](./media/app-insights-export-telemetry/create-container.png)

Une fois que vous avez créé l’exportation, elle démarre. Vous obtenez uniquement les données qui arrive après avoir créé l’exportation de hello.

Il peut y avoir un délai d’environ une heure avant que les données s’affichent dans le stockage hello.

### <a name="tooedit-continuous-export"></a>exportation continue de tooedit

Si vous souhaitez que les types d’événements toochange hello plus tard, modifiez l’exportation de hello :

![Cliquez sur Choisir les types d’événements.](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a>exportation continue de toostop

exportation de hello toostop, cliquez sur Désactiver. Lorsque vous cliquez sur Activer à nouveau, exportation de hello redémarre avec de nouvelles données. Vous n’obtiendrez données hello reçus dans le portail de hello lors de l’exportation a été désactivée.

exportation de hello toostop définitivement, supprimez-le. Cette opération ne supprime pas vos données du stockage.

### <a name="cant-add-or-change-an-export"></a>Impossible d’ajouter ou de modifier une exportation ?
* exportations tooadd ou de modification, vous devez propriétaire, collaborateur ou Application Insights collaborateurs des droits d’accès. [En savoir plus sur les rôles][roles].

## <a name="analyze"></a> Quels sont les événements que vous obtenez ?
Hello données exportées sont brutes de télémesure hello que nous recevons de votre application, sauf que nous ajoutons à laquelle il convient de calculer les données d’emplacement à partir de l’adresse IP du client hello.

Les données qui a été rejetées par [échantillonnage](app-insights-sampling.md) n’est pas inclus dans les données de salutation exportée.

Les autres mesures calculées ne sont pas incluses. Par exemple, nous ne pas exporter une utilisation moyenne de l’UC, mais nous exportez brutes de télémesure hello à partir de laquelle la moyenne de hello est calculée.

Hello données incluent également des résultats de n’importe quel hello [disponibilité des tests web](app-insights-monitor-web-app-availability.md) que vous avez définis.

> [!NOTE]
> **Échantillonnage.** Si votre application envoie une grande quantité de données, fonctionnalité d’échantillonnage hello peut fonctionner et envoyer qu’une fraction des données de télémétrie hello généré. [En savoir plus sur l’échantillonnage.](app-insights-sampling.md)
>
>

## <a name="get"></a>Inspecter les données de hello
Vous pouvez inspecter stockage hello directement dans le portail de hello. Cliquez sur **Parcourir**, sélectionnez votre compte de stockage, puis ouvrez **Conteneurs**.

tooinspect stockage Azure dans Visual Studio, ouvrez **vue**, **Cloud Explorer**. (Si vous n’avez pas cette commande de menu, vous devez tooinstall hello Azure SDK : hello ouvrir **nouveau projet** boîte de dialogue, développez Visual C# / Cloud et choisissez **obtenir Microsoft Azure SDK pour .NET**.)

Lorsque vous ouvrez votre magasin d’objets blob, vous voyez un conteneur avec un ensemble de fichiers blob. Hello URI de chaque fichier dérivé de votre nom de la ressource Application Insights, sa clé d’instrumentation, la télémétrie-type/date/heure. (nom de la ressource hello est en minuscule et clé d’instrumentation hello omet les tirets).

![Inspecter le magasin d’objets blob hello avec un outil approprié](./media/app-insights-export-telemetry/04-data.png)

hello date et heure sont UTC et quand les données de télémétrie hello a été déposée dans le magasin de hello, pas les temps de hello a été généré. Par conséquent, si vous écrivez des données de code toodownload hello, il peut parcourir linéairement hello données.

Voici l’écran hello du chemin d’accès hello :

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

Where

* `blobCreationTimeUtc`heure de blob création Bonjour interne est mis en œuvre stockage
* `blobDeliveryTimeUtc`est hello heure d’objet blob de stockage de destination d’exportation toohello copiés

## <a name="format"></a> Format de données
* Chaque objet blob est un fichier texte qui contient plusieurs lignes séparées par des \n. Il contient la télémétrie hello traitée sur une période d’environ la moitié d’une minute.
* Chaque ligne représente un point de données de télémétrie, par exemple une demande ou un affichage de page.
* Chaque ligne est un document JSON sans mise en forme. Si vous souhaitez toosit et vous fixez il, ouvrez dans Visual Studio et choisissez Modifier, options avancées, fichier de Format :

![Télémétrie des consultations de hello avec un outil approprié](./media/app-insights-export-telemetry/06-json.png)

Les durées sont exprimées en nombre de cycles, où 10 000 cycles = 1 ms. Par exemple, ces valeurs indiquent un temps de 1 MS toosend une demande de navigateur hello, 3ms tooreceive et 1.8s tooprocess hello page dans le navigateur de hello :

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[Informations de référence pour les types de propriété hello et les valeurs de modèle de données détaillées.](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a>Le traitement des données de hello
À petite échelle, vous pouvez écrire certaines toopull code séparer vos données, lire dans une feuille de calcul et ainsi de suite. Par exemple :

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

Pour un exemple de code plus long, consultez [Utilisation d’un rôle de travail][exportasa].

## <a name="delete"></a>Supprimer les anciennes données
Notez que vous êtes responsable de la gestion de votre capacité de stockage et la suppression des anciennes données de hello si nécessaire.

## <a name="if-you-regenerate-your-storage-key"></a>Si vous régénérez votre clé de stockage...
Si vous modifiez le stockage de clés tooyour hello, exportation continue cesseront de fonctionner. Vous voyez alors une notification dans votre compte Azure.

Ouvrir le panneau de l’exportation continue hello et modifier l’exportation. Modifier hello Destination d’exportation, mais laissez hello même stockage sélectionné. Cliquez sur OK tooconfirm.

![Hello modifier continue exporter, ouvrir et fermer les trois destination de l’exportation.](./media/app-insights-export-telemetry/07-resetstore.png)

exportation continue de Hello redémarre.

## <a name="export-samples"></a>Exemples d’exportation

* [TooSQL d’exportation à l’aide de flux de données Analytique][exportasa]
* [Stream Analytics - Exemple 2](app-insights-export-stream-analytics.md)

Sur les échelles plus volumineux, envisagez [HDInsight](https://azure.microsoft.com/services/hdinsight/) -Hadoop de clusters dans le cloud de hello. HDInsight fournit un éventail de technologies destinées à gérer et analyser les données volumineuses, et vous pouvez l’utiliser dans les données tooprocess qui a été exportées à partir de l’Application Insights.

## <a name="q--a"></a>Questions et réponses
* *Je veux simplement télécharger un graphique.*  

    Oui, vous pouvez le faire. Haut hello du Panneau de hello, cliquez sur **exporter les données**.
* *J’ai configuré une exportation, mais il n’y a pas de données dans mon magasin.*

    Application Insights reçue toutes les données de télémétrie de votre application dans la mesure où vous configurez l’exportation de hello ? Vous recevrez uniquement les nouvelles données.
* *J’ai essayé tooset une exportation, mais a refusé l’accès*

    Si le compte de hello est détenu par votre organisation, vous avez toobe un membre des groupes de propriétaires ou collaborateurs hello.
* *Puis-je exporter toomy droite propre banque locale ?*

    Non. Pour le moment, notre moteur d’exportation fonctionne uniquement avec le stockage Azure.  
* *Existe-t-il un volume de données de que vous placer dans le magasin my toohello limite ?*

    Non. Nous allons conserver transmettre des données jusqu'à ce que vous supprimiez exportation de hello. Nous allons arrêter si nous avons atteint la limite extérieure de hello pour le stockage d’objets blob, mais c’est assez volumineux. C’est tooyou toocontrol vous utilisez la quantité de stockage.  
* *Objets BLOB combien dois-je voir dans le stockage hello ?*

  * Pour toutes les données, vous tapez tooexport sélectionnée, un nouvel objet blob est créé chaque minute (si les données sont disponibles).
  * En outre, pour les applications avec un trafic élevé, des unités de partition supplémentaires sont allouées. Dans ce cas, chaque unité crée un objet blob toutes les minutes.
* *Je régénérées de stockage de clés toomy hello ou modifié nom hello du conteneur de hello et exportation de hello ne fonctionne pas.*

    Modifier l’exportation de hello et ouvrez le panneau de destination d’exportation hello. Laissez hello même stockage sélectionnée comme précédemment, puis cliquez sur OK tooconfirm. L’exportation redémarre. Si les modifications hello était dans hello au-delà de quelques jours, vous ne perdrez les données.
* *Puis-je suspendre exportation de hello ?*

    Oui. Cliquez sur Désactiver.

## <a name="code-samples"></a>Exemples de code

* [Stream Analytics - Exemple](app-insights-export-stream-analytics.md)
* [TooSQL d’exportation à l’aide de flux de données Analytique][exportasa]
* [Informations de référence pour les types de propriété hello et les valeurs de modèle de données détaillées.](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
