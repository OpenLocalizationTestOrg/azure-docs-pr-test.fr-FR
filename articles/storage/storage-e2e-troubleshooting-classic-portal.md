---
title: "aaaTroubleshooting stockage Azure avec les diagnostics et de l’Analyseur de Message | Documents Microsoft"
description: "Didacticiel illustrant la résolution des problèmes de bout en bout avec Azure Storage Analytics, AzCopy et Microsoft Message Analyzer"
services: storage
documentationcenter: dotnet
author: robinsh
manager: timlt
ms.assetid: 6b23cba5-0d53-439e-870b-de8e406107d8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 74ee126bab30b9a45f4904a065b6fe3006f76101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="end-to-end-troubleshooting-using-azure-storage-metrics-and-logging-azcopy-and-message-analyzer"></a>Résolution des problèmes de bout en bout avec la journalisation et les mesures du stockage Azure, AzCopy et Message Analyzer
[!INCLUDE [storage-selector-portal-e2e-troubleshooting](../../includes/storage-selector-portal-e2e-troubleshooting.md)]

## <a name="overview"></a>Vue d’ensemble
Diagnostic et résolution des problèmes sont essentiels pour la création et la prise en charge d'applications clientes avec Microsoft Azure Storage. En raison de la nature toohello distribuée d’une application Azure, diagnostic et la résolution des erreurs et problèmes de performances peuvent être plus complexes que dans les environnements classiques.

Dans ce didacticiel, nous allons vous montrer comment les clients tooidentify certaines erreurs qui peuvent affecter les performances et résoudre les erreurs de bout en bout à l’aide des outils fournis par Microsoft et le stockage Azure, dans l’application cliente de commande toooptimize hello.

Ce didacticiel fournit une exploration pratique d'un scénario de dépannage de bout en bout. Pour un guide détaillé des conceptuel tootroubleshooting stockage Azure des applications, consultez [moniteur, diagnostiquer et résoudre les problèmes de Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).

## <a name="tools-for-troubleshooting-azure-storage-applications"></a>Outils de résolution des problèmes dans les applications Azure Storage
les applications clientes tootroubleshoot à l’aide de Microsoft Azure Storage, vous pouvez utiliser une combinaison des outils toodetermine lorsqu’un problème s’est produite et quelles hello problème de hello peut être dû de. Ces outils incluent :

* **Azure Storage Analytics**. [Azure Storage Analytics](http://msdn.microsoft.com/library/azure/hh343270.aspx) fournit des métriques et une journalisation pour Azure Storage.

  * **Storage Metrics** assure le suivi des métriques de transaction et des métriques de capacité pour votre compte de stockage. À l’aide de mesures, vous pouvez déterminer comment votre application s’exécute en fonction tooa diverses mesures différentes. Consultez [schéma de Table de métriques Storage Analytique](http://msdn.microsoft.com/library/azure/hh343264.aspx) pour plus d’informations sur les types hello de métriques suivies par stockage Analytique.
  * **La journalisation du stockage** enregistre chaque journal des demandes toohello Azure Storage services tooa côté serveur. Hello journal assure le suivi des données détaillées pour chaque demande, y compris les opération hello effectuée, état hello d’opération de hello et les informations de latence. Consultez [le Format de journal Analytique stockage](http://msdn.microsoft.com/library/azure/hh343259.aspx) pour plus d’informations sur les données de demande et de réponse hello écrit des journaux de toohello par stockage Analytique.

> [!NOTE]
> Les comptes de stockage avec un type de réplication de stockage redondance de Zone (ZRS) n’ont pas de métriques de hello ou la fonctionnalité de journalisation activée pour l’instant.
>
>

* **Portail Azure Classic**. Vous pouvez configurer des métriques et la journalisation pour votre compte de stockage Bonjour [portail classique Azure](https://manage.windowsazure.com). Vous pouvez également afficher des graphiques qui montrent le fonctionne de votre application au fil du temps et configurer toonotify alertes que vous attendu si votre application effectue différemment que pour une métrique spécifiée.

    Consultez [surveiller un compte de stockage Bonjour Azure Portal](storage-monitor-storage-account.md) pour plus d’informations sur la configuration de la surveillance Bonjour portail classique Azure.
* **AzCopy**. Journaux du serveur pour le stockage Azure sont stockés sous la forme d’objets BLOB, vous pouvez donc utiliser AzCopy toocopy hello journal BLOB tooa répertoire local pour l’analyse à l’aide de l’Analyseur de Message Microsoft. Consultez [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md) pour plus d’informations sur AzCopy.
* **Microsoft Message Analyzer**. L’Analyseur de message est un outil qui consomme des fichiers journaux et affiche les données de journal dans un format visuel, il est facile toofilter, recherche et groupe journaliser les données en ensembles utiles que vous pouvez utiliser tooanalyze erreurs et problèmes de performances. Pour plus d'informations sur Message Analyzer, consultez la page [Guide d'exploitation de Microsoft Message Analyzer](http://technet.microsoft.com/library/jj649776.aspx) .

## <a name="about-hello-sample-scenario"></a>À propos de l’exemple de scénario de hello
Pour ce didacticiel, nous allons examiner un scénario où les métriques Azure Storage indiquent un faible taux de réussite pour une application qui appelle le stockage Azure. Hello mesure du taux de faible pourcentage de réussite (indiqué en tant que **PercentSuccess** Bonjour portail classique Azure et dans les tables de métriques hello) effectue le suivi des opérations qui réussissent, mais qui retournent un code d’état HTTP est supérieur à 299. Dans les fichiers journaux de stockage côté serveur hello, ces opérations sont enregistrées avec un statut de transaction **ClientOtherErrors**. Pour plus d’informations sur la métrique de faible pourcentage de réussite hello, consultez [PercentSuccess basse affichent les métriques ou les entrées de journal analytique ont des opérations avec l’état de transaction de ClientOtherErrors](storage-monitoring-diagnosing-troubleshooting.md#metrics-show-low-percent-success).

Les opérations d’Azure Storage peuvent renvoyer les codes d’état HTTP supérieurs à 299 dans le cadre de leur fonctionnement normal. Mais dans certains cas, elles indiquent que vous pouvez être en mesure de toooptimize votre application cliente pour des performances accrues.

Dans ce scénario, nous allons étudier une toobe de fréquence faible pourcentage de réussite quoi que ce soit inférieure à 100 %. Vous pouvez choisir un autre métrique niveau, toutefois, selon les besoins de tooyour. Nous vous recommandons, pendant le test de votre application, d'établir une tolérance de référence pour les métriques de performances clés. Par exemple, vous pouvez déterminer, sur la base de tests, que votre application doit avoir un taux de réussite de 90 % ou 85 %. Si vos données métriques montrent qu’application hello est libertés avec ce nombre, vous pouvez examiner ce que susceptible de causer l’augmentation de hello.

Pour notre exemple de scénario, une fois que nous avons établi que la mesure du taux de pourcentage de réussite hello est inférieure à 100 %, nous examiner les erreurs de hello hello journaux toofind qui mettent en corrélation les mesures toohello et les utiliser toofigure comprendre ce qui est à l’origine hello plus faible pourcentage de réussite. Nous examinerons plus précisément les erreurs dans la plage de 400 hello. Ensuite, nous étudierons plus en détail les erreurs 404 (Introuvable).

### <a name="some-causes-of-400-range-errors"></a>Certaines causes d'erreurs dans la plage 400
exemples de Hello ci-dessous présente un échantillonnage de certaines erreurs 400-range pour les demandes sur le stockage d’objets Blob Azure et leurs causes possibles. Une de ces erreurs, ainsi que les erreurs dans la plage de 300 hello et plage de 500 hello, peuvent contribuer tooa faible pourcentage de réussite.

Notez que les listes de hello ci-dessous sont loin d’être terminée. Consultez [d’état et Codes d’erreur](http://msdn.microsoft.com/library/azure/dd179382.aspx) pour plus d’informations sur les erreurs générales de stockage Azure et sur les erreurs tooeach spécifique des services de stockage hello.

**Exemples de code d’état 404 (Introuvable)**

Se produit lorsqu’une opération de lecture pour un conteneur ou d’un objet blob échoue, car l’objet blob de hello ou un conteneur est introuvable.

* Se produit si un conteneur ou un objet blob a été supprimé par un autre client avant cette demande.
* Se produit si vous utilisez un appel d’API qui crée le conteneur de hello ou un objet blob après avoir vérifié si elle existe. Hello CreateIfNotExists APIs appeler une tête toocheck première existence hello de hello conteneur ou blob ; Si elle n’existe pas, une erreur 404 est retourné et un deuxième appel PUT est effectué toowrite hello conteneur ou blob.

**Exemples de code d'état 409 (Conflit)**

* Se produit si vous utilisez un toocreate de l’API de créer un nouveau conteneur ou un objet blob, sans vérification de l’existence de tout d’abord, un conteneur ou un objet blob portant ce nom existe déjà.
* Se produit si un conteneur est en cours de suppression et que vous essayez toocreate un conteneur avec hello même nom que celui avant l’opération de suppression hello est terminée.
* Se produit si vous spécifiez un bail sur un conteneur ou un objet blob, alors qu'il existe déjà un bail.

**Exemples de code d'état 412 (Échec de la précondition)**

* Se produit lorsque la condition de hello spécifiée par un en-tête conditionnel n’a pas été remplie.
* Se produit lorsque l’ID de bail hello spécifié ne correspond pas à des ID de bail hello sur le conteneur de hello ou un objet blob.

## <a name="generate-log-files-for-analysis"></a>Génération de fichiers journaux pour l'analyse
Dans ce didacticiel, nous allons utiliser l’Analyseur de Message toowork avec trois différents types de fichiers journaux, bien que vous pouvez choisir toowork avec l’une de ces :

* Hello **journal server**, qui est créé lorsque vous activez la journalisation du stockage Azure. Hello contient les données relatives à chaque opération appelée sur l’un des services de stockage Azure hello - objet blob, file d’attente, table et fichier. journal du serveur Hello indique quelle opération a été appelée et le code d’état a été retournés, ainsi que d’autres détails sur hello demande et de réponse.
* Hello **journal du client .NET**, qui est créé lorsque vous activez la journalisation côté client à partir de votre application .NET. journaux du client Hello comprend des informations détaillées sur le client de hello prépare hello demande et reçoit et traite la réponse de hello.
* Hello **journal des traces réseau HTTP**, qui collecte les données sur les données demande et de réponse HTTP/HTTPS, notamment pour les opérations sur le stockage Azure. Dans ce didacticiel, nous allez générer la trace de réseau hello via l’Analyseur de Message.

### <a name="configure-server-side-logging-and-metrics"></a>Configuration de la journalisation et des métriques côté serveur
Tout d’abord, nous avons besoin de journalisation d’Azure Storage tooconfigure et les mesures, afin que nous avons des données à partir de hello client application tooanalyze. Vous pouvez configurer la journalisation et les mesures dans de différentes façons : via hello [portail classique Azure](https://manage.windowsazure.com), à l’aide de PowerShell, ou par programme. Pour plus d’informations sur la configuration de la journalisation et des métriques, consultez les pages [Enabling Storage Metrics and Viewing Metrics Data (Activation de Storage Metrics et affichage des données de métriques)](http://msdn.microsoft.com/library/azure/dn782843.aspx) et [Enabling Storage Logging and Accessing Log Data (Activation de la journalisation du stockage et accès aux données de journal)](http://msdn.microsoft.com/library/azure/dn782840.aspx).

**Via hello portail classique Azure**

enregistrement de tooconfigure et les métriques pour votre compte de stockage à l’aide du portail de hello, suivez les instructions de hello à [surveiller un compte de stockage Bonjour Azure Portal](storage-monitor-storage-account.md).

> [!NOTE]
> Il n’est pas possible tooset mesure des minutes à l’aide de hello portail classique Azure. Toutefois, nous recommandons que vous ne les définissez hello pour ce didacticiel et pour rechercher les problèmes de performances avec votre application. Vous pouvez définir les métriques par minute à l’aide de PowerShell comme indiqué ci-dessous, ou par programmation ou via hello portail classique Azure.
>
> Notez que hello portail classique Azure ne peut pas afficher les métriques par minute, seules les métriques par heure.
>
>

**Via PowerShell**

tooget main de PowerShell pour Azure, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

1. Hello d’utilisation [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0) tooadd de l’applet de commande de votre utilisateur Azure compte toohello PowerShell fenêtre :

    ```powershell
     Add-AzureAccount
    ```

2. Bonjour **connecter tooMicrosoft Azure** fenêtre, adresse de messagerie de type hello et mot de passe associé à votre compte. Azure authentifie et enregistre les informations d’identification de hello, puis ferme la fenêtre hello.
3. Définir hello par défaut stockage compte toohello compte de stockage à l’aide d’un didacticiel de hello par l’exécution de ces commandes dans la fenêtre de PowerShell hello :

    ```powershell
    $SubscriptionName = 'Your subscription name'
    $StorageAccountName = 'yourstorageaccount'
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

4. Activer la journalisation pour hello service Blob du stockage :

    ```powershell
    Set-AzureStorageServiceLoggingProperty -ServiceType Blob -LoggingOperations Read,Write,Delete -PassThru -RetentionDays 7 -Version 1.0
    ```

5. Activer les métriques de stockage pour hello service Blob, rendre vraiment tooset **- MetricsType** trop`Minute`:

    ```powershell
    Set-AzureStorageServiceMetricsProperty -ServiceType Blob -MetricsType Minute -MetricsLevel ServiceAndApi -PassThru -RetentionDays 7 -Version 1.0
    ```

### <a name="configure-net-client-side-logging"></a>Configuration de la journalisation côté client .NET
tooconfigure côté client journalisation pour une application .NET, activer les diagnostics de .NET dans le fichier de configuration de l’application hello (web.config ou app.config). Consultez [journalisation avec hello bibliothèque cliente de stockage .NET côté Client](http://msdn.microsoft.com/library/azure/dn782839.aspx) et [journalisation avec hello SDK Microsoft Azure Storage pour Java côté Client](http://msdn.microsoft.com/library/azure/dn782844.aspx) pour plus d’informations.

journal de Hello côté client comprend des informations détaillées sur le client de hello prépare hello demande et reçoit et traite la réponse de hello.

Hello bibliothèque cliente de stockage stocke les données de journal côté client à l’emplacement de hello spécifié dans le fichier de configuration de l’application hello (web.config ou app.config).

### <a name="collect-a-network-trace"></a>Collecte d'un suivi réseau
Vous pouvez utiliser l’Analyseur de Message toocollect une trace réseau HTTP/HTTPS pendant l’exécution de votre application cliente. Utilisation de l’Analyseur de message [Fiddler](http://www.telerik.com/fiddler) sur hello back-end. Avant de collecter de la trace de réseau hello, nous vous recommandons de configurer le trafic HTTPS Fiddler toorecord non chiffré :

1. Installez [Fiddler](http://www.telerik.com/download/fiddler).
2. Lancez Fiddler.
3. Sélectionnez **Tools | Fiddler Options (Outils | Options de Fiddler)**.
4. Dans la boîte de dialogue Options hello, vérifiez que **capturer le connecte HTTPS** et **déchiffrer le trafic HTTPS** sont toutes deux activées, comme illustré ci-dessous.

![Configuration des options de Fiddler](./media/storage-e2e-troubleshooting-classic-portal/fiddler-options-1.png)

Didacticiel de hello, collecter et tout d’abord enregistrer une trace réseau dans l’Analyseur de Message, puis créer une trace de hello analyse session tooanalyze et hello des journaux. toocollect une trace réseau dans l’Analyseur de Message :

1. Dans Message Analyzer, sélectionnez **File | Quick Trace | Unencrypted HTTPS (Fichier | Suivi rapide | HTTPS non chiffré)**.
2. trace de Hello commence immédiatement. Sélectionnez **arrêter** toostop hello trace pour que nous pouvons configurer tootrace le trafic de stockage uniquement.
3. Sélectionnez **modifier** session de suivi tooedit hello.
4. Sélectionnez hello **configurer** lien toohello à droite de hello **Microsoft-Pef-WebProxy** fournisseur ETW.
5. Bonjour **paramètres avancés** boîte de dialogue, cliquez sur hello **fournisseur** onglet.
6. Bonjour **filtre de nom d’hôte** Indiquez vos points de terminaison de stockage, séparés par des espaces. Par exemple, vous pouvez spécifier vos points de terminaison comme suit : modifier `storagesample` nom toohello de votre compte de stockage :

    ```   
    storagesample.blob.core.windows.net storagesample.queue.core.windows.net storagesample.table.core.windows.net
    ```

7. Quitter la boîte de dialogue hello, puis cliquez sur **redémarrer** toobegin la collecte d’hello trace avec le filtre de nom d’hôte hello en place, afin que seul le trafic de réseau de stockage Azure est inclus dans la trace de hello.

> [!NOTE]
> Une fois que vous avez terminé la collecte de trace de votre réseau, nous vous recommandons vivement de rétablir les paramètres hello que vous a peut-être changé dans le trafic HTTPS Fiddler toodecrypt. Dans la boîte de dialogue Options de Fiddler hello, désélectionnez hello **capturer le connecte HTTPS** et **déchiffrer le trafic HTTPS** cases à cocher.
>
>

Consultez [à l’aide des fonctionnalités de suivi réseau hello](http://technet.microsoft.com/library/jj674819.aspx) sur Technet pour plus de détails.

## <a name="review-metrics-data-in-hello-azure-classic-portal"></a>Passez en revue les données de métriques Bonjour portail classique Azure
Une fois que votre application s’exécute pendant une période de temps, vous pouvez consulter les graphiques de métriques hello qui s’affichent dans hello portail classique Azure tooobserve de la façon dont votre service a été effectuée. Tout d’abord, nous allons ajouter hello **pourcentage de réussite** toohello métrique analyse page :

1. Accédez toohello du tableau de bord pour votre compte de stockage Bonjour [portail classique Azure](https://manage.windowsazure.com), puis sélectionnez **moniteur** hello tooview page d’analyse.
2. Cliquez sur **ajouter des métriques** toodisplay hello **choisir des métriques** boîte de dialogue.
3. Défilement vers le bas toofind hello **pourcentage de réussite de** groupe, développez-le, puis sélectionnez **d’agrégation**, comme illustré dans l’image hello ci-dessous. Cette métrique rassemble les données de pourcentage de réussite de toutes les opérations sur des objets blob.

![Choisir des métriques](./media/storage-e2e-troubleshooting-classic-portal/choose-metrics-portal-1.png)

Bonjour portail classique Azure, vous voyez **pourcentage de réussite** Bonjour graphique de surveillance, ainsi que toutes les autres mesures vous avez ajouté (les toosix peuvent être affichées sur hello graphique à la fois). Dans l’image hello ci-dessous, vous pouvez voir que ce taux de pourcentage de réussite hello est légèrement inférieure à 100 %, ce qui constitue le scénario hello que nous allons examiner ensuite en analysant les journaux hello dans l’Analyseur de Message :

![Graphique des métriques dans le portail](./media/storage-e2e-troubleshooting-classic-portal/portal-metrics-chart-1.png)

Pour plus d’informations sur l’ajout de page de supervision toohello métriques, consultez [Comment : ajouter la table des mesures métriques toohello](storage-monitor-storage-account.md#add-metrics-charts-to-the-portal-dashboard).

> [!NOTE]
> Il peut prendre un certain temps pour votre tooappear de données de métriques Bonjour portail classique Azure après avoir activé les métriques de stockage. Il s’agit, car les métriques pour hello heure précédente ne figurent pas dans hello portail classique Azure jusqu'à ce que hello heure actuelle a expiré. En outre, les métriques par minute ne sont pas affichés dans hello portail classique Azure. En fonction lorsque vous activez des mesures, qui peut prendre les données de métriques toosee tootwo heures.
>
>

## <a name="use-azcopy-toocopy-server-logs-tooa-local-directory"></a>Utilisez AzCopy toocopy serveur journaux tooa répertoire local
Le stockage Azure écrit tooblobs de données de journal de serveur, tandis que les mesures sont écrites tootables. Objets BLOB de journal est disponibles dans hello connue `$logs` conteneur pour votre compte de stockage. Objets BLOB de journal est nommés hiérarchiquement par année, mois, jour et les heures, afin que vous puissiez localiser facilement plage hello de fois que vous souhaitez tooinvestigate. Par exemple, dans hello `storagesample` conteneur hello pour les objets BLOB de journal hello pour 02/01/2015, à partir de 8-9 : 00, le compte est `https://storagesample.blob.core.windows.net/$logs/blob/2015/01/08/0800`. objets BLOB individuels de Hello dans ce conteneur sont nommés de manière séquentielle, à partir de `000000.log`.

Vous pouvez utiliser toodownload d’outil de ligne de commande AzCopy hello ces emplacement tooa des fichiers journaux du côté serveur de votre choix sur votre ordinateur local. Par exemple, vous pouvez utiliser hello suivant des fichiers journaux de commande toodownload hello pour placer des opérations d’objet blob qui ont mis sur le 2 janvier 2015 toohello dossier `C:\Temp\Logs\Server`; Remplacez `<storageaccountname>` avec nom hello de votre compte de stockage et `<storageaccountkey>` avec votre clé d’accès de compte :

```azcopy
AzCopy.exe /Source:http://<storageaccountname>.blob.core.windows.net/$logs /Dest:C:\Temp\Logs\Server /Pattern:"blob/2015/01/02" /SourceKey:<storageaccountkey> /S /V
```

AzCopy est disponible pour téléchargement sur hello [téléchargements Azure](https://azure.microsoft.com/downloads/) page. Pour plus d’informations sur l’utilisation de AzCopy, consultez [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md).

Pour plus d’informations sur le téléchargement des journaux côté serveur, consultez [Téléchargement des données de journal de la journalisation du stockage](http://msdn.microsoft.com/library/azure/dn782840.aspx#DownloadingStorageLogginglogdata).

## <a name="use-microsoft-message-analyzer-tooanalyze-log-data"></a>Utiliser les données du journal Microsoft Message Analyzer tooanalyze
Microsoft Message Analyzer est un outil de capture, d'affichage et d'analyse du trafic de messagerie de protocole, des événements et des autres messages du système ou des applications dans les scénarios de résolution des problèmes et de diagnostic. L’Analyseur de message également vous tooload, aggregate et analyser les données de journal et enregistré les fichiers de trace. Pour plus d'informations sur Message Analyzer, consultez la page [Guide d'exploitation de Microsoft Message Analyzer](http://technet.microsoft.com/library/jj649776.aspx).

L’Analyseur de message inclut des ressources pour le stockage Azure qui vous aident à tooanalyze serveur, client et journaux réseau. Dans cette section, nous expliquerons comment toouse ces tooaddress outils hello problème de faible pourcentage de réussite dans hello des journaux de stockage.

### <a name="download-and-install-message-analyzer-and-hello-azure-storage-assets"></a>Télécharger et installer l’Analyseur de Message et hello des ressources de stockage Azure
1. Télécharger [l’Analyseur de Message](http://www.microsoft.com/download/details.aspx?id=44226) de hello Microsoft Download Center, et exécuter le programme d’installation hello.
2. Lancez Message Analyzer.
3. À partir de hello **outils** menu, sélectionnez **Asset Manager**. Bonjour **Asset Manager** boîte de dialogue, sélectionnez **télécharge**, puis filtrez sur **Azure Storage**. Vous verrez des ressources de stockage Azure hello, comme indiqué dans l’image hello ci-dessous.
4. Cliquez sur **synchronisation affiche tous les éléments** tooinstall hello des ressources de stockage Azure. les ressources Hello disponibles sont les suivantes :
   * **Règles de couleur de stockage Azure :** règles de couleur de stockage Azure vous toodefine filtres spéciaux qui utilisent la couleur de texte, et toohighlight les messages qui contiennent des informations spécifiques dans une trace des styles de police.
   * **Graphiques Azure Storage :** il s’agit de représentations graphiques prédéfinies des données du journal du serveur. Notez que toouse graphiques de stockage Azure à ce stade, vous pouvez charger uniquement le journal de serveur hello en hello grille de l’analyse.
   * **Les analyseurs de stockage Azure :** hello client de stockage Azure analyseurs analyse hello stockage Azure, le serveur et HTTP dans l’ordre toodisplay les enregistre dans hello grille de l’analyse.
   * **Filtres de stockage Azure :** filtres de stockage Azure sont des critères prédéfinis que vous pouvez utiliser tooquery vos données Bonjour grille de l’analyse.
   * **Dispositions de mode de stockage Azure :** dispositions de mode de stockage Azure sont des présentations colonne prédéfinies et des regroupements dans hello grille de l’analyse.
5. Redémarrez l’Analyseur de Message après avoir installé les composants hello.

![Gestionnaire de biens de l’analyseur de message](./media/storage-e2e-troubleshooting-classic-portal/mma-start-page-1.png)

> [!NOTE]
> Installez toutes les ressources de stockage Azure hello indiqués hello pour ce didacticiel.
>
>

### <a name="import-your-log-files-into-message-analyzer"></a>Importation de vos fichiers journaux dans Message Analyzer
Vous pouvez importer tous vos fichiers journaux enregistrés (côté serveur, côté client et réseau) dans une session de Microsoft Message Analyzer pour l'analyse.

1. Sur hello **fichier** menu dans l’Analyseur de Message de Microsoft, cliquez sur **nouvelle Session**, puis cliquez sur **Session vide**. Bonjour **nouvelle Session** boîte de dialogue, entrez un nom pour votre session d’analyse. Bonjour **détails de la Session** du panneau, cliquez sur hello **fichiers** bouton.
2. données de trace tooload hello réseau générées par l’Analyseur de Message, cliquez sur **ajouter des fichiers**, rechercher l’emplacement de toohello où vous avez enregistré votre fichier .matp à partir de votre session de suivi web, fichier .matp de hello sélectionnez, puis cliquez sur **ouvrir**.
3. données de journal côté serveur hello tooload, cliquez sur **ajouter des fichiers**, rechercher l’emplacement de toohello où vous avez téléchargé vos journaux côté serveur, sélectionnez les fichiers de journal hello pour plage de temps hello vous souhaitez tooanalyze, puis cliquez sur **ouvrir**. Puis, dans hello **détails de la Session** Panneau de configuration, le jeu hello **Configuration des journaux texte** liste déroulante pour chaque fichier de journal côté serveur trop**AzureStorageLog** tooensure que Microsoft L’Analyseur de message peut analyser les fichier de journal hello correctement.
4. données de journal côté client tooload hello, cliquez sur **ajouter des fichiers**, rechercher l’emplacement de toohello où vous avez enregistré vos journaux côté client, sélectionnez les fichiers de journaux hello vous souhaitez tooanalyze, puis cliquez sur **ouvrir**. Puis, dans hello **détails de la Session** Panneau de configuration, le jeu hello **Configuration des journaux texte** liste déroulante pour chaque fichier de journal côté client trop**AzureStorageClientDotNetV4** tooensure qui L’Analyseur de Message Microsoft peut analyser les fichier de journal hello correctement.
5. Cliquez sur **Démarrer** Bonjour **nouvelle Session** dialogue tooload et l’analyse hello données du journal. affichent les données du journal Hello Bonjour Message Analyzer analyse grille.

image Hello ci-dessous montre un exemple de session configuré avec les fichiers journaux des traces réseau, client et serveur.

![Configuration d’une session de Message Analyzer](./media/storage-e2e-troubleshooting-classic-portal/configure-mma-session-1.png)

Notez que Message Analyzer charge les fichiers journaux en mémoire. Si vous avez un grand ensemble de données de journal, vous pouvez toofilter dans l’ordre tooget hello des performances optimales à partir de l’Analyseur de Message.

Tout d’abord, déterminez laps de temps hello qui vous intéressez et minimiser ce laps de temps. Dans de nombreux cas, vous devez tooreview une période de minutes ou heures au maximum. Importer hello plus petit jeu de fichiers journaux qui peuvent répondre à vos besoins.

Si vous avez toujours une grande quantité de données de journal, puis vous souhaiterez toospecify un toofilter de filtre de session vos données de journal avant de les charger. Bonjour **Session filtre** boîte, sélectionnez hello **bibliothèque** bouton toochoose un filtre prédéfini ; par exemple, choisir **filtre Global temps I** de hello filtres du stockage Azure toofilter sur un intervalle de temps. Vous pouvez ensuite modifier Bonjour Bonjour du toospecify critères de filtre démarrage et horodatage de fin de l’intervalle de salutation vous toosee. Vous pouvez également filtrer sur un code d’état particulier. par exemple, vous pouvez choisir les seules entrées de journal tooload où le code d’état hello est 404.

Pour plus d'informations sur l'importation des données de journal dans Microsoft Message Analyzer, consultez la page [Récupération des données des messages](http://technet.microsoft.com/library/dn772437.aspx) sur TechNet.

### <a name="use-hello-client-request-id-toocorrelate-log-file-data"></a>Utiliser les données de fichier journal de hello client demande ID toocorrelate
Hello bibliothèque cliente de stockage Azure génère automatiquement un ID de demande client unique pour chaque demande. Cette valeur est écrite toohello client, journaux de serveur hello, suivi et journaux hello réseau, vous pouvez l’utiliser toocorrelate données sur trois journaux dans l’Analyseur de Message. Consultez [ID de demande Client](storage-monitoring-diagnosing-troubleshooting.md#client-request-id) pour plus d’informations sur les clients hello ID de la demande

sections Hello ci-dessous décrivent comment toouse préconfiguré et les vues de disposition personnalisée toocorrelate et regrouper les données en fonction de la demande du client hello ID.

### <a name="select-a-view-layout-toodisplay-in-hello-analysis-grid"></a>Sélectionnez un toodisplay de mise en page de vue Bonjour grille d’analyse
Hello des ressources de stockage pour l’Analyseur de Message incluent les dispositions du mode de stockage Azure, qui sont des vues préconfigurées que vous pouvez utiliser toodisplay vos données avec des groupes utiles et des colonnes pour différents scénarios. Vous pouvez également créer des dispositions de vue personnalisées et les enregistrer pour pouvoir les réutiliser.

image Hello ci-dessous montre hello **mise en page de vue** menu, disponible en sélectionnant **mise en page de vue** à partir du ruban de barre d’outils hello. mises en page de vue Hello pour le stockage Azure sont regroupées sous hello **Azure Storage** nœud dans le menu de hello. Vous pouvez rechercher des `Azure Storage` dans toofilter de zone de recherche hello sur le stockage Azure permet d’afficher uniquement les dispositions. Vous pouvez également sélectionner hello en étoile suivant tooa vue disposition toomake informatique un favori et l’afficher en haut de hello du menu de hello.

![Menu Disposition de vue](./media/storage-e2e-troubleshooting-classic-portal/view-layout-menu.png)

toobegin avec select **regroupées par Module et ClientRequestID**. Cette disposition de vue regroupe les données des trois journaux, d'abord par ID de demande client, puis par fichier journal source (ou **Module** dans Message Analyzer). Avec cette vue, vous pouvez explorer de manière détaillée un ID de demande client particulier et afficher les données des trois fichiers journaux pour cette ID de demande client.

image Hello ci-dessous montre cette disposition affichage appliqué toohello journal des données d’échantillonnage, avec un sous-ensemble de colonnes affichées. Vous pouvez voir que pour un ID de demande client particulier, hello analyse grille affiche les données d’hello journal du client, les journaux de serveur et trace réseau.

![Disposition de vue Azure Storage](./media/storage-e2e-troubleshooting-classic-portal/view-layout-client-request-id-module.png)

> [!NOTE]
> Différents fichiers journaux ont des colonnes différentes, donc lorsque les données à partir de plusieurs fichiers journaux sont affichées dans hello analyse grille, certaines colonnes ne peuvent pas contenir de données pour une ligne donnée. Par exemple, dans l’image hello ci-dessus, les lignes de journal du client ne plus afficher toutes les données de hello **Timestamp**, **TimeElapsed**, **Source**, et **Destination** colonnes, car ces colonnes n’existent pas dans le journal du client hello, mais existent dans la trace de réseau hello. De même, hello **Timestamp** colonne affiche les données d’horodatage à partir du journal du serveur hello, mais aucune donnée ne s’affiche pour hello **TimeElapsed**, **Source**, et  **Destination** colonnes qui ne font pas partie du journal du serveur hello.
>
>

En outre toousing hello Azure Storage présentations, vous pouvez également définir et enregistrer vos propres mises en page de vue. Vous pouvez sélectionner d’autres champs de votre choisis pour le regroupement des données et enregistrer le regroupement de hello dans le cadre de votre disposition personnalisée ainsi.

### <a name="apply-color-rules-toohello-analysis-grid"></a>Appliquer des règles de couleur toohello analyse grille
Ressources de stockage Hello incluent également les règles de couleur, qui offrent qu'un élément visuel signifie tooidentify différents types d’erreurs Bonjour grille de l’analyse. Hello couleurs prédéfinies règles s’appliquent tooHTTP erreurs, afin qu’ils s’affichent uniquement pour la trace réseau et les journaux du serveur hello.

Sélectionnez des règles de couleur tooapply, **les règles de couleur** à partir du ruban de barre d’outils hello. Vous verrez les règles de couleur de stockage Azure hello dans le menu de hello. Pour hello didacticiel, sélectionnez **erreurs du Client (StatusCode compris entre 400 et 499)**, comme illustré dans l’image hello ci-dessous.

![Disposition de vue Azure Storage](./media/storage-e2e-troubleshooting-classic-portal/color-rules-menu.png)

En outre de couleur des règles toousing hello le stockage Azure, vous pouvez également définir et enregistrer vos propres règles de couleur.

### <a name="group-and-filter-log-data-toofind-400-range-errors"></a>Regrouper et filtrer consigner les erreurs de 400-plage de données toofind
Ensuite, nous regrouper et filtrer toofind de données de journal hello toutes les erreurs dans la plage de hello 400.

1. Recherchez hello **StatusCode** colonne Bonjour grille Analysis, colonne de hello avec le bouton droit, titre et sélectionnez **groupe**.
2. Ensuite, regrouper sur hello **ClientRequestId** colonne. Vous verrez que les données de hello Bonjour que grille de l’analyse est désormais organisée par état de code et à la demande du client ID.
3. Affichez la fenêtre filtre de la vue hello si elle n’est pas affichée. Sur le ruban de barre d’outils hello, sélectionnez **fenêtres Outil**, puis **filtre de la vue**.
4. toofilter hello données toodisplay uniquement 400-plage erreurs du journal, ajouter hello suivant toohello de critères de filtre **filtre de la vue** fenêtre, puis cliquez sur **appliquer**:

    ```   
    (AzureStorageLog.StatusCode >= 400 && AzureStorageLog.StatusCode <=499) || (HTTP.StatusCode >= 400 && HTTP.StatusCode <= 499)
    ```

image Hello ci-dessous montre les résultats de hello de ce regroupement et le filtre. Expansion hello **ClientRequestID** champ sous hello de regroupement pour le code d’état 409, par exemple, montre une opération qui a entraîné ce code d’état.

![Disposition de vue Azure Storage](./media/storage-e2e-troubleshooting-classic-portal/400-range-errors1.png)

Après avoir appliqué ce filtre, vous verrez que les lignes de journal du client hello sont exclues, comme hello journal client n’inclut pas un **StatusCode** colonne. toobegin avec, nous allons examiner du serveur de hello et toolocate réseau repérer les journaux des 404 erreurs, puis nous allons retourner toohello client journal tooexamine hello client les opérations qui ont conduit toothem.

> [!NOTE]
> Vous pouvez filtrer sur hello **StatusCode** colonne et toujours afficher les données de tous les journaux, y compris hello journal du client, si vous ajoutez un filtre d’expression de toohello qui comporte les entrées de journal dans lequel le code d’état hello est null. tooconstruct cette expression de filtre, utilisez :
>
> <code>&#42;StatusCode >= 400 or !&#42;StatusCode</code>
>
> Ce filtre retourne toutes les lignes de hello cliente journal et uniquement les lignes de journal du serveur hello et journal HTTP dont le code d’état hello est supérieur à 400. Si vous l’appliquez toohello regroupé par ID de demande client et le module de l’affichage de la disposition, vous pouvez rechercher ou défiler hello journal entrées toofind ceux où tous les trois journaux sont représentées.   
>
>

### <a name="filter-log-data-toofind-404-errors"></a>Filtrer les 404 erreurs du journal des données toofind
Ressources de stockage Hello incluent des filtres prédéfinis que vous pouvez utiliser toonarrow journal toofind hello erreurs de données ou les tendances que vous recherchez. Ensuite, nous allons appliquer deux filtres prédéfinis : une qui filtre les journaux de trace réseau pour les 404 erreurs et hello et une qui filtre les données hello sur un intervalle de temps spécifié.

1. Affichez la fenêtre filtre de la vue hello si elle n’est pas affichée. Sur le ruban de barre d’outils hello, sélectionnez **fenêtres Outil**, puis **filtre de la vue**.
2. Dans la fenêtre de filtre de la vue de hello, sélectionnez **bibliothèque**et effectuez une recherche sur `Azure Storage` hello toofind filtres de stockage Azure. Filtre sélectionnez hello pour **404 (introuvable) des messages dans tous les journaux**.
3. Hello d’affichage **bibliothèque** menu Nouveau, puis localisez et sélectionnez hello **filtre de temps Global**.
4. Modifier les horodatages hello indiqués dans la plage de hello filtre toohello que tooview vous le souhaitez. Cela permet de plage hello toonarrow tooanalyze de données.
5. Le filtre doit apparaître comme exemple toohello ci-dessous. Cliquez sur **appliquer** tooapply hello filtre toohello grille de l’analyse.

    ```   
    ((AzureStorageLog.StatusCode == 404 || HTTP.StatusCode == 404)) And
    (#Timestamp >= 2014-10-20T16:36:38 and #Timestamp <= 2014-10-20T16:36:39)
    ```

![Disposition de vue Azure Storage](./media/storage-e2e-troubleshooting-classic-portal/404-filtered-errors1.png)

### <a name="analyze-your-log-data"></a>Analyse des données du journal
Maintenant que vous avez groupées et filtré les données, vous pouvez examiner les détails de hello des requêtes individuelles qui ont généré des 404 erreurs. Dans la disposition d’affichage actuelle hello, les données de hello sont regroupées par ID de demande du client, puis par la source du journal. Étant donné que nous sommes le filtrage sur les demandes dont le champ de StatusCode hello contient 404, nous allons voir uniquement les serveur hello et données de trace du réseau, pas les données de journal client hello.

image Hello ci-dessous illustre une demande spécifique où une opération Get Blob générait une erreur 404, car l’objet blob de hello n’existe pas. Notez que certaines colonnes ont été supprimées à partir de la vue standard de hello dans les données pertinentes de commande toodisplay hello.

![Journaux de suivi du serveur et du réseau filtrés](./media/storage-e2e-troubleshooting-classic-portal/server-filtered-404-error.png)

Ensuite, nous allons corréler cet ID de demande client hello client journal données toosee client hello actions a été prise lors de l’hello erreur s’est produite. Vous pouvez afficher une nouvelle vue de grille de l’analyse pour cette session tooview hello client données du journal, qui s’ouvre dans un deuxième onglet :

1. D’abord, copiez la valeur hello hello **ClientRequestId** Presse-papiers toohello de champ. Vous pouvez ce faire, sélectionnez une ligne, localisation hello **ClientRequestId** champ, en cliquant sur la valeur de données hello et en choisissant **copie « ClientRequestId »**.
2. Sur le ruban de barre d’outils hello, sélectionnez **nouvelle visionneuse**, puis sélectionnez **analyse grille** tooopen un nouvel onglet hello nouvel onglet affiche toutes les données dans les fichiers journaux, sans les règles de couleur, de filtrage ou de regroupement.
3. Sur le ruban de barre d’outils hello, sélectionnez **mise en page de vue**, puis sélectionnez **toutes les colonnes de Client .NET** sous hello **Azure Storage** section. Cette disposition de la vue affiche les données journal hello du client ainsi que hello journaux des traces de serveur et réseau. Par défaut, il est trié sur hello **MessageNumber** colonne.
4. Ensuite, recherchez les journaux du client hello pour l’ID de demande client hello. Sur le ruban de barre d’outils hello, sélectionnez **rechercher des Messages**, puis spécifiez un filtre personnalisé sur l’ID de demande client hello Bonjour **trouver** champ. Utilisez la syntaxe de filtre hello, en spécifiant votre propre ID de demande client :

    ```  
    *ClientRequestId == "398bac41-7725-484b-8a69-2a9e48fc669a"
    ```

L’Analyseur de message localise et sélectionne la première entrée de journal hello où les critères de recherche hello correspond aux ID de demande client hello. Dans le journal du client hello, il existe plusieurs entrées pour chaque ID de demande client, vous pouvez donc toogroup à hello **ClientRequestId** champ toomake il toosee plus facilement les ensemble. image Hello ci-dessous montre tous les messages hello client de hello de journal pour hello spécifié ID de demande client.

![Journal client affichant des erreurs 404](./media/storage-e2e-troubleshooting-classic-portal/client-log-analysis-grid1.png)

À l’aide de données hello indiquées dans les dispositions de vue hello dans ces deux onglets, vous pouvez analyser hello demande données toodetermine ce qui peut avoir provoqué l’erreur de hello. Vous pouvez également consulter les demandes qui ont précédé cette un toosee si un événement précédent ont pu mener erreur 404 de toohello. Par exemple, vous pouvez consulter les entrées de journal client hello précédant cette toodetermine ID de demande client si l’objet blob de hello a peut-être été supprimé, ou si l’erreur de hello était en raison de l’application cliente de toohello appel d’une API de CreateIfNotExists dans un conteneur ou d’un objet blob. Dans le journal du client hello, vous pouvez trouver les adresses de l’objet blob de hello dans hello **Description** champ ; dans hello et les journaux de suivi réseau, ces informations s’affichent dans hello **Résumé** champ.

Une fois que vous connaissez adresse hello du blob hello ayant généré l’erreur de hello 404, vous pouvez étudier de plus près. Si vous recherchez des entrées de journal hello pour les autres messages associés à des opérations sur hello même blob, vous pouvez vérifier si les clients hello supprimé précédemment entité de hello.

## <a name="analyze-other-types-of-storage-errors"></a>Analyse des autres types d'erreur de stockage
Maintenant que vous connaissez à l’aide de l’Analyseur de Message tooanalyze vos données de journal, vous pouvez analyser les autres types d’erreurs à l’aide de la vue disposition, les règles de couleur et la recherche/le filtrage. Hello tables ci-dessous répertorie certains problèmes que vous pouvez rencontrer et hello des critères de filtre que vous pouvez utiliser toolocate les. Pour plus d’informations sur la construction des filtres et hello Analyseur de Message, le filtrage de langage, consultez [filtrage des données de Message](http://technet.microsoft.com/library/jj819365.aspx).

| tooInvestigate... | Utiliser l'expression de filtre... | Expression s’applique tooLog (Client, serveur, réseau, toutes les) |
| --- | --- | --- |
| Retards inattendus de la remise des messages dans une file d'attente |AzureStorageClientDotNetV4.Description contient "Retrying failed operation." |Client |
| HTTP, augmentation de la valeur PercentThrottlingError |HTTP.Response.StatusCode   == 500 &#124;&#124; HTTP.Response.StatusCode == 503 |Réseau |
| Augmentation de la valeur PercentTimeoutError |HTTP.Response.StatusCode   == 500 |Réseau |
| Augmentation de la valeur PercentTimeoutError (tous) |*StatusCode   == 500 |Tout |
| Augmentation de la valeur PercentNetworkError |AzureStorageClientDotNetV4.EventLogEntry.Level   < 2 |Client |
| Messages HTTP 403 (refusé) |HTTP.Response.StatusCode   == 403 |Réseau |
| Messages HTTP 404 (non trouvé) |HTTP.Response.StatusCode   == 404 |Réseau |
| 404 (tous) |*StatusCode   == 404 |Tout |
| Problème d'autorisation de la signature d'accès partagé (SAS) |AzureStorageLog.RequestStatus ==  "SASAuthorizationError" |Réseau |
| Messages HTTP 409 (conflit) |HTTP.Response.StatusCode   == 409 |Réseau |
| 409 (tous) |*StatusCode   == 409 |Tout |
| Les entrées à faible valeur PercentSuccess ou du journal   d’analyse incluent des opérations avec un statut de transaction ClientOtherErrors |AzureStorageLog.RequestStatus ==   "ClientOtherError" |Serveur |
| Avertissement   de Nagle |((AzureStorageLog.EndToEndLatencyMS   - AzureStorageLog.ServerLatencyMS) > (AzureStorageLog.ServerLatencyMS *   1.5)) et (AzureStorageLog.RequestPacketSize <1460) et (AzureStorageLog.EndToEndLatencyMS -   AzureStorageLog.ServerLatencyMS >= 200) |Serveur |
| Plage horaire   dans les journaux serveur et réseau |#Timestamp   >= 2014-10-20T16:36:38 and #Timestamp <= 2014-10-20T16:36:39 |Serveur, réseau |
| Plage horaire   dans les journaux serveur |AzureStorageLog.Timestamp >= 2014-10-20T16:36:38 et AzureStorageLog.Timestamp <= 2014-10-20T16:36:39 |Serveur |

## <a name="next-steps"></a>Étapes suivantes
Pour plus d'informations sur les scénarios de résolution des problèmes de bout en bout dans Azure Storage, consultez les ressources suivantes :

* [Analyser, diagnostiquer et dépanner Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md)
* [Analyse du stockage](http://msdn.microsoft.com/library/azure/hh343270.aspx)
* [Surveillance d’un compte de stockage Bonjour portail Azure](storage-monitor-storage-account.md)
* [Transfert de données avec hello utilitaire de ligne de commande AzCopy](storage-use-azcopy.md)
* [Microsoft Message Analyzer Operating Guide (Guide des opérations Microsoft Message Analyzer)](http://technet.microsoft.com/library/jj649776.aspx)
