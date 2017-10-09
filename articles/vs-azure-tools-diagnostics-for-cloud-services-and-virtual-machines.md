---
title: aaaConfiguring Diagnostics pour Azure Cloud Services et Machines virtuelles | Documents Microsoft
description: "Décrit comment tooconfigure les informations de diagnostic pour déboguer Azure cloud services et les machines virtuelles (VM) dans Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: e70cd7b4-6298-43aa-adea-6fd618414c26
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 74cdf49413d6d89a84195070dd9d817da2463373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-diagnostics-for-azure-cloud-services-and-virtual-machines"></a>Configuration de Diagnostics pour les services cloud et les machines virtuelles Azure
Lorsque vous avez besoin de tootroubleshoot un service cloud Azure ou une machine virtuelle Azure, vous pouvez configurer les diagnostics Azure plus facilement à l’aide de Visual Studio. Azure diagnostics capture les données système et les données de journalisation sur les ordinateurs virtuels de hello et instances de machine virtuelle qui exécutent votre service cloud et transfère les données dans un compte de stockage de votre choix. Pour plus d’informations sur la journalisation des diagnostics dans Azure, consultez [Activer la journalisation des diagnostics pour les applications web dans Azure App Service](app-service-web/web-sites-enable-diagnostic-log.md).

Cette rubrique vous montre comment tooenable et configurer les diagnostics Azure dans Visual Studio, à la fois avant et après le déploiement, ainsi que dans les machines virtuelles. Il montre également comment les types hello tooselect de toocollect des informations de diagnostics et comment tooview hello après lui sont recueillies.

Vous pouvez configurer les Diagnostics Azure Bonjour suivant façons :

* Vous pouvez modifier les paramètres de configuration de diagnostics par hello **Configuration des Diagnostics** boîte de dialogue dans Visual Studio. paramètres de Hello sont enregistrés dans un fichier nommé diagnostics.wadcfgx (diagnostics.wadcfg dans Azure SDK 2.4 ou version antérieure). Ou bien, vous pouvez modifier directement les fichiers de configuration hello. Si vous remplacez manuellement le fichier de hello, les modifications de configuration hello prendra hello d’effet prochaine fois que vous déployez tooAzure de service cloud hello ou un service d’exécution hello dans l’émulateur de hello.
* Utilisez **Cloud Explorer** ou **l’Explorateur de serveurs** dans les paramètres de diagnostic de Visual Studio toochange hello pour un ordinateur virtuel ou le service de cloud en cours d’exécution.

## <a name="azure-26-diagnostics-changes"></a>Modifications apportées aux diagnostics Azure 2.6
Pour les projets Azure SDK 2.6 dans Visual Studio, hello modifications suivantes ont été apportée. (Ces modifications s’appliquent également toolater les versions de Windows Azure SDK.)

* émulateur local de Hello prend désormais en charge les diagnostics. Cela signifie que vous pouvez collecter des données de diagnostic et vérifiez que votre application crée hello traces appropriées lorsque vous développez et testez dans Visual Studio. chaîne de connexion de Hello `UseDevelopmentStorage=true` permet la collecte de données de diagnostic lorsque vous exécutez votre projet de service cloud dans Visual Studio à l’aide d’émulateur de stockage Azure hello. Toutes les données de diagnostic sont collectées dans le compte de stockage hello (stockage de développement).
* chaîne de connexion de compte des stockage Hello diagnostics (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) est stocké à nouveau dans le fichier de configuration (.cscfg) de service hello. Compte de stockage de diagnostics hello Azure SDK 2.5 a été spécifié dans le fichier diagnostics.wadcfgx de hello.

Il existe des différences notables entre la chaîne de connexion hello travaillé dans Azure SDK 2.4 et versions antérieures, et comment il fonctionne dans Azure SDK 2.6 et versions ultérieures.

* Dans Azure SDK 2.4 et versions antérieures, chaîne de connexion hello a été utilisé comme un runtime par hello plug-in tooget hello stockage compte des informations de diagnostic pour le transfert des journaux de diagnostic.
* Dans Azure SDK 2.6 et versions ultérieures, la chaîne de connexion de diagnostics de hello est utilisée par l’extension de Visual Studio tooconfigure hello diagnostics avec les informations de compte de stockage approprié hello lors de la publication. chaîne de connexion Hello permet de définir les comptes de stockage différentes pour différentes configurations de service que Visual Studio utilisera lors de la publication. Toutefois, étant donné que le plug-in des diagnostics hello n’est plus disponible (après Azure SDK 2.5), fichier .cscfg de hello par lui-même ne peut pas activer hello Extension des Diagnostics. Vous disposez d’extension de hello tooenable séparément par le biais d’outils tels que Visual Studio ou PowerShell.
* processus de hello toosimplify de configuration de l’extension de diagnostics hello avec PowerShell, sortie hello du package à partir de Visual Studio contient également hello publique XML de configuration pour l’extension diagnostics hello pour chaque rôle. Visual Studio utilise hello diagnostics connexion chaîne toopopulate hello compte de stockage informations présente dans la configuration publique de hello. les fichiers de configuration publics Hello sont créés dans le dossier d’Extensions hello et suivent hello modèle PaaSDiagnostics. &lt;RoleName >. PubConfig.xml. Tout déploiement basé sur PowerShell peut utiliser toomap de ce modèle chaque tooa configuration rôle.
* chaîne de connexion Hello dans le fichier .cscfg de hello est également utilisé par hello [portail Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) tooaccess hello les données de diagnostic afin de pouvoir Bonjour **analyse** chaîne de connexion onglet hello est nécessaire. tooconfigure hello service tooshow données dans le portail de hello de surveillance détaillée.

## <a name="migrating-projects-tooazure-sdk-26-and-later"></a>Migration des projets tooAzure SDK 2.6 et versions ultérieur
Lors de la migration à partir d’Azure SDK 2.5 tooAzure SDK 2.6 ou version ultérieure, si vous avez un compte de stockage de diagnostics spécifié dans le fichier .wadcfgx de hello, puis il y restera. avantage tootake de flexibilité hello d’utilisation de stockage différents comptes pour diverses configurations de stockage, vous avez toomanually ajouter un projet de tooyour de chaîne de connexion hello. Si vous migrez un projet à partir d’Azure SDK 2.4 ou antérieure tooAzure 2.6 du Kit de développement logiciel, puis hello diagnostics des chaînes de connexion sont conservés. Toutefois, notez les modifications hello dans la façon dont les chaînes de connexion sont traitées dans Azure SDK 2.6 comme spécifié dans la section précédente de hello.

### <a name="how-visual-studio-determines-hello-diagnostics-storage-account"></a>Comment Visual Studio détermine le compte de stockage de diagnostics hello
* Si une chaîne de connexion de diagnostic est spécifiée dans le fichier .cscfg de hello, Visual Studio utilise extension de diagnostics tooconfigure hello lors de la publication et lors de la génération des fichiers xml de configuration publique hello lors de l’empaquetage.
* Si aucune chaîne de connexion de diagnostic n’est spécifié dans le fichier .cscfg de hello, puis Visual Studio revient compte de stockage toousing hello spécifié dans hello .wadcfgx tooconfigure hello diagnostics extension de fichier lors de la publication et la génération hello public fichiers de xml de configuration lors de la compression.
* chaîne de connexion des diagnostics Hello dans le fichier .cscfg de hello est prioritaire sur le compte de stockage hello dans le fichier .wadcfgx de hello. Si une chaîne de connexion de diagnostic est spécifiée dans le fichier .cscfg de hello, puis Visual Studio qui utilise et ignore le compte de stockage hello dans .wadcfgx.

### <a name="what-does-hello-update-development-storage-connection-strings-checkbox-do"></a>Ce qui hello « Mettre à jour les chaînes de connexion de stockage de développement... »  ?
Hello case à cocher pour **mettre à jour les chaînes de connexion de stockage de développement pour les Diagnostics et la mise en cache avec les informations d’identification de compte de stockage Microsoft Azure lors de la publication tooMicrosoft Azure** vous offre un moyen pratique de tooupdate tout chaînes de connexion de compte de stockage de développement avec le compte de stockage Azure hello spécifié lors de la publication.

Par exemple, supposons que vous sélectionnez cette case à cocher et la chaîne de connexion de diagnostic hello spécifie `UseDevelopmentStorage=true`. Lorsque vous publiez hello projet tooAzure, Visual Studio met automatiquement à jour chaîne de connexion des diagnostics hello avec compte de stockage hello que vous avez spécifié dans l’Assistant de publication hello. Toutefois, si un compte de stockage réel a été spécifié comme chaîne de connexion des diagnostics hello, ce compte est utilisé à la place.

## <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a>Différences entre les fonctionnalités de diagnostics du Kit de développement logiciel (SDK) Azure 2.4 et les versions antérieures et du Kit de développement logiciel (SDK) Azure 2.5 et les versions ultérieures
Si vous mettez à niveau votre projet à partir d’Azure SDK 2.4 tooAzure SDK 2.5 ou version ultérieure, vous devez garder à hello esprit suivant des différences de fonctionnalités de diagnostics.

* **Les API de configuration sont déconseillées** : la configuration par programmation des diagnostics est disponible dans le Kit de développement logiciel (SDK) Azure 2.4 ou les versions antérieures, mais déconseillée dans le Kit de développement logiciel (SDK) Azure 2.5 et les versions ultérieures. Si votre configuration des diagnostics est actuellement définie dans le code, vous devez tooreconfigure ces paramètres à partir de zéro dans le projet migré de hello dans l’ordre pour l’utilisation de diagnostics tookeep. fichier de configuration des diagnostics Hello pour Azure SDK 2.4 est diagnostics.wadcfg et diagnostics.wadcfgx pour Azure SDK 2.5 et versions ultérieures.
* **Diagnostics pour les applications de service cloud peuvent être configurées uniquement au niveau du rôle hello, pas au niveau de l’instance hello.**
* **Chaque fois que vous déployez votre application, la configuration des diagnostics hello est mise à jour** : cela peut entraîner des problèmes de parité si vous modifiez votre configuration des diagnostics à partir de l’Explorateur de serveurs et redéployez votre application.
* **Dans Azure SDK 2.5 et versions ultérieures, les vidages sur incident sont configurés dans le fichier de configuration de diagnostics hello, pas dans le code** – si vous avez des vidages sur incident configurés dans le code, vous aurez une configuration du transfert de hello toomanually toohello configuration fichier de code, Étant donné que les vidages sur incident de hello ne sont pas transférées au cours de la migration de hello tooAzure 2.6 du Kit de développement logiciel.

## <a name="enable-diagnostics-in-cloud-service-projects-before-deploying-them"></a>Activation des diagnostics dans les projets de service cloud avant leur déploiement
Dans Visual Studio, vous pouvez choisir toocollect les données de diagnostic pour les rôles qui s’exécutent dans Azure, lorsque vous exécutez le service de hello dans l’émulateur de hello avant de le déployer. Tous les paramètres de toodiagnostics de modifications dans Visual Studio sont enregistrés dans le fichier de configuration diagnostics.wadcfgx hello. Ces paramètres de configuration spécifient le compte de stockage hello dans lequel les données de diagnostic sont enregistrées lorsque vous déployez votre service cloud.

[!INCLUDE [cloud-services-wad-warning](../includes/cloud-services-wad-warning.md)]

### <a name="tooenable-diagnostics-in-visual-studio-before-deployment"></a>tooenable des diagnostics dans Visual Studio avant le déploiement
1. Dans le menu contextuel hello rôle hello qui vous intéresse, choisissez **propriétés**, puis choisissez hello **Configuration** onglet du rôle hello **propriétés** fenêtre.
2. Bonjour **Diagnostics** section, assurez-vous que hello **activer les Diagnostics** case à cocher est activée.
   
    ![Option de hello activer les Diagnostics de l’accès à](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796660.png)
3. Choisissez hello points de suspension (...) bouton toospecify hello compte de stockage où vous souhaitez toobe de données de diagnostic hello stockée. compte de stockage Hello que vous choisissez sera l’emplacement hello où sont stockées les données de diagnostic.
   
    ![Spécifiez toouse de compte de stockage hello](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796661.png)
4. Bonjour **créer une chaîne de connexion stockage** boîte de dialogue, spécifiez si vous souhaitez tooconnect à l’aide de hello émulateur de stockage Azure, un abonnement Azure, ou manuellement les informations d’identification entrées.
   
    ![Boîte de dialogue Compte de stockage](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796662.png)
   
   * Si vous choisissez d’option de l’émulateur de stockage Microsoft Azure hello, chaîne de connexion hello a la valeur tooUseDevelopmentStorage = true.
   * Si vous choisissez hello votre option d’abonnement, vous pouvez choisir hello abonnement Azure que vous souhaitez toouse et hello nom de compte. Vous pouvez choisir de que gérer les comptes hello bouton toomanage vos abonnements Azure.
   * Si vous choisissez option des informations d’identification hello entrée manuellement, vous êtes nom de hello de tooenter demandée et la clé de hello Azure compte toouse.
5. Choisissez hello **configurer** hello tooview de bouton **configuration des Diagnostics** boîte de dialogue. Chaque onglet (à l’exception de **Général** et **Répertoires de journaux**) correspond à une source de données de diagnostic que vous pouvez collecter. onglet par défaut de Hello, **général**, offre vous hello suivant les options de collecte de données de diagnostic : **uniquement les erreurs**, **toutes les informations**, et **plan personnalisé** . Hello option par défaut, **erreurs uniquement**, prend hello moins de stockage, car elle ne transfère pas les avertissements ou messages de traçage. Hello tous les transferts en option informations hello la plupart des informations et est, hello par conséquent, l’option la plus coûteuse en termes de stockage.
   
    ![Activer les diagnostics Azure et la configuration](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
6. Dans cet exemple, sélectionnez hello **plan personnalisé** option afin que vous pouvez personnaliser les données de salutation collectées.
7. Hello **Quota de disque en Mo** zone spécifie la quantité d’espace souhaitée tooallocate dans votre stockage de compte pour les données de diagnostic. Vous pouvez modifier la valeur par défaut de hello si vous le souhaitez.
8. Sous chaque onglet des données de diagnostic vous souhaitez toocollect, sélectionnez son **activer le transfert de <log type>**  case à cocher. Par exemple, si vous souhaitez que les journaux d’application toocollect, sélectionnez hello **activer le transfert des journaux d’Application** case à cocher sur hello **journaux des applications** onglet. Spécifiez également toutes autres informations requises pour chaque type de données de diagnostic. Consultez la section de hello **configurer des sources de données de diagnostics** plus loin dans cette rubrique pour plus d’informations de configuration sur chaque onglet.
9. Après avoir activé la collection de toutes les données de diagnostic hello souhaité, choisissez hello **OK** bouton.
10. Exécutez votre projet de service cloud Azure dans Visual Studio comme d’habitude. Lorsque vous utilisez votre application, les informations de journal hello que vous avez activé sont enregistrées toohello compte de stockage Azure spécifié.

## <a name="enable-diagnostics-in-azure-virtual-machines"></a>Activation des diagnostics dans des machines virtuelles Azure
Dans Visual Studio, vous pouvez choisir toocollect les données de diagnostic pour les machines virtuelles.

### <a name="tooenable-diagnostics-in-azure-virtual-machines"></a>diagnostics de tooenable dans des machines virtuelles
1. Dans **l’Explorateur de serveurs**, choisissez hello nœud Azure et connectez-vous tooyour abonnement Azure, si vous n’êtes pas déjà connecté.
2. Développez hello **virtuels** nœud. Vous pouvez sélectionner ou créer une machine virtuelle.
3. Dans le menu contextuel de hello pour l’ordinateur virtuel hello qui vous intéresse, choisissez **configurer**. Cela affiche la boîte de dialogue de configuration de machine virtuelle hello.
   
    ![Configuration d’une machine virtuelle Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796663.png)
4. S’il n’est pas déjà installé, ajouter l’extension de Diagnostics de Microsoft Monitoring Agent hello. Cette extension vous permet de collecter des données de diagnostic pour hello machine virtuelle Azure. Dans la liste des Extensions installées hello, choisissez le menu de sélectionner une extension disponible liste déroulante hello, puis Diagnostics de Microsoft Monitoring Agent.
   
    ![Installation d’une extension de machine virtuelle Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766024.png)
   
   > [!NOTE]
   > D’autres extensions des diagnostics sont disponibles pour vos machines virtuelles. Pour plus d’informations, consultez Fonctionnalités et extensions de machine virtuelle Azure.
   > 
   > 
5. Choisissez hello **ajouter** bouton extension de hello tooadd et afficher ses **configuration des Diagnostics** boîte de dialogue.
6. Choisissez hello **configurer** bouton toospecify un compte de stockage, puis choisissez hello **OK** bouton.
   
    Chaque onglet (à l’exception de **Général** et **Répertoires de journaux**) correspond à une source de données de diagnostic que vous pouvez collecter.
   
    ![Activer les diagnostics Azure et la configuration](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758144.png)
   
    onglet par défaut de Hello, **général**, offre vous hello suivant les options de collecte de données de diagnostic : **uniquement les erreurs**, **toutes les informations**, et **plan personnalisé** . Hello option par défaut, **erreurs uniquement**, prend hello moins de stockage, car elle ne transfère pas les avertissements ou messages de traçage. Hello **toutes les informations** option transferts hello la plupart des informations et est, par conséquent, hello plus coûteuse en termes de stockage.
7. Dans cet exemple, sélectionnez hello **plan personnalisé** option afin que vous pouvez personnaliser les données de salutation collectées.
8. Hello **Quota de disque en Mo** zone spécifie la quantité d’espace souhaitée tooallocate dans votre stockage de compte pour les données de diagnostic. Vous pouvez modifier la valeur par défaut de hello si vous le souhaitez.
9. Sous chaque onglet des données de diagnostic vous souhaitez toocollect, sélectionnez son **activer le transfert de <log type>**  case à cocher.
   
    Par exemple, si vous souhaitez que les journaux d’application toocollect, sélectionnez hello **activer le transfert des journaux d’Application** case à cocher sur hello **journaux des applications** onglet. Spécifiez également toutes autres informations requises pour chaque type de données de diagnostic. Consultez la section de hello **configurer des sources de données de diagnostics** plus loin dans cette rubrique pour plus d’informations de configuration sur chaque onglet.
10. Après avoir activé la collection de toutes les données de diagnostic hello souhaité, choisissez hello **OK** bouton.
11. Enregistrer le projet de hello mis à jour.
    
     Vous verrez un message Bonjour **journal des activités Microsoft Azure** fenêtre hello d’ordinateur virtuel a été mis à jour.

## <a name="configure-diagnostics-data-sources"></a>Configuration des sources de données de diagnostic
Après avoir activé la collecte de données de diagnostic, vous pouvez choisir exactement quelles sources de données toocollect et les informations collectées. Hello Voici une liste des onglets de hello **configuration des Diagnostics** boîte de dialogue et les chaque option de configuration.

### <a name="application-logs"></a>Journaux d’application
**Un journal d’application** contient des informations de diagnostic produites par une application web. Si vous souhaitez que les journaux d’application toocapture, sélectionnez hello **activer le transfert des journaux des applications** case à cocher. Vous pouvez augmenter ou diminuer le nombre de hello de minutes pendant lesquelles les journaux d’application hello sont transférés tooyour compte de stockage en modifiant hello **période de transfert (min)** valeur. Vous pouvez également modifier la quantité de hello d’informations consignées dans le journal de hello en définissant la valeur de niveau de journal hello. Par exemple, vous pouvez choisir **Verbose** tooget plus d’informations ou choisir **critique** toocapture les erreurs critiques uniquement. Si vous avez un fournisseur de diagnostics spécifiques qui émet des journaux des applications, vous pouvez capturer ceux-ci en ajoutant toohello GUID du fournisseur hello **fournisseur GUID** boîte.

  ![Journaux d’application](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758145.png)

  Pour plus d’informations sur les journaux d’application, consultez [Activer la journalisation des diagnostics pour les applications web dans Azure App Service](app-service-web/web-sites-enable-diagnostic-log.md) .

### <a name="windows-event-logs"></a>Journaux des événements Windows
Si vous souhaitez que les journaux des événements Windows toocapture, sélectionnez hello **activer le transfert des journaux des événements Windows** case à cocher. Vous pouvez augmenter ou diminuer le nombre de hello de minutes pendant lesquelles les journaux des événements hello sont transférés tooyour compte de stockage en modifiant hello **période de transfert (min)** valeur. Activez les cases à cocher hello pour les types d’événements que vous souhaitez tootrack hello.

  ![Journaux d’événements](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796664.png)

Si vous utilisez Azure SDK 2.6 ou version ultérieur et que vous souhaitez toospecify une source de données personnalisée, entrez-la Bonjour  **<Data source name>**  texte zone, puis choisissez hello **ajouter** tooit suivant du bouton. source de données Hello est ajouté le fichier diagnostics.cfcfg de toohello.

Si vous utilisez Azure SDK 2.5 et que vous souhaitez toospecify une source de données personnalisé, vous pouvez l’ajouter toohello `WindowsEventLog` fichier section de hello diagnostics.wadcfgx, comme dans hello l’exemple suivant.

```
<WindowsEventLog scheduledTransferPeriod="PT1M">
   <DataSource name="Application!*" />
   <DataSource name="CustomDataSource!*" />
</WindowsEventLog>
```
### <a name="performance-counters"></a>Compteurs de performances
Les informations d’un compteur de performances peuvent vous aider à localiser des goulets d’étranglement système et à affiner les performances des applications et du système. Pour plus d’informations, consultez [Créer et utiliser des compteurs de performances dans une application Azure](https://msdn.microsoft.com/library/azure/hh411542.aspx) . Si vous souhaitez que les compteurs de performance toocapture, sélectionnez hello **activer le transfert des compteurs de Performance** case à cocher. Vous pouvez augmenter ou diminuer le nombre de hello de minutes pendant lesquelles les journaux des événements hello sont transférés tooyour compte de stockage en modifiant hello **période de transfert (min)** valeur. Activez les cases à cocher hello pour hello des compteurs de performance que vous souhaitez tootrack.

  ![Compteurs de performance](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758147.png)

tootrack un compteur de performance n’est pas répertorié, entrez-le en utilisant hello syntaxe suggérée, puis choisissez hello **ajouter** bouton. système d’exploitation de Hello sur l’ordinateur virtuel de hello détermine les compteurs de performance que vous pouvez effectuer le suivi. Pour plus d’informations sur la syntaxe, consultez [Spécifier le chemin d’un compteur](https://msdn.microsoft.com/library/windows/desktop/aa373193.aspx).

### <a name="infrastructure-logs"></a>Journaux d’infrastructure
Si vous souhaitez que les journaux d’infrastructure toocapture qui contiennent plus d’informations sur le module RemoteForwarder de hello hello infrastructure de diagnostics Azure et module RemoteAccess de hello, sélectionnez hello **activer le transfert des journaux d’Infrastructure**case à cocher. Vous pouvez augmenter ou diminuer le nombre hello de minutes lors du transfert des journaux de hello tooyour compte de stockage en modifiant la valeur de période de transfert (min) hello.

  ![Journaux d’infrastructure de diagnostics](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC758148.png)

  Pour plus d’informations, consultez [Recueillir des données de journaux à l’aide des diagnostics Azure](https://msdn.microsoft.com/library/azure/gg433048.aspx) .

### <a name="log-directories"></a>Répertoires de journaux
Si vous souhaitez que les répertoires de journaux toocapture, qui contiennent les données collectées à partir de répertoires de journaux pour les demandes Internet Information Services (IIS), les demandes ayant échoué, ou des dossiers que vous choisissez, sélectionnez hello **activer le transfert des répertoires de journaux**case à cocher. Vous pouvez augmenter ou diminuer le nombre hello de minutes lors du transfert des journaux de hello tooyour compte de stockage en modifiant hello **période de transfert (min)** valeur.

Vous pouvez activer les cases hello de hello journaux toocollect, telles que **journaux IIS** et **Échec de la demande** journaux. Les noms de conteneur de stockage par défaut sont fournis, mais vous pouvez modifier les noms de hello si vous le souhaitez.

Vous pouvez également capturer des journaux de tout dossier. Spécifiez simplement le chemin d’accès hello Bonjour **journal du répertoire absolu** section, puis choisissez hello **ajouter un répertoire** bouton. Hello journaux seront transférés toohello spécifié des conteneurs.

  ![Répertoires de journaux](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796665.png)

### <a name="etw-logs"></a>Journaux de suivi des événements ETW
Si vous utilisez [Event Tracing for Windows](https://msdn.microsoft.com/library/windows/desktop/bb968803\(v=vs.85\).aspx) (ETW) et souhaitez que les journaux ETW toocapture, sélectionnez hello **activer le transfert des journaux ETW** case à cocher. Vous pouvez augmenter ou diminuer le nombre hello de minutes lors du transfert des journaux de hello tooyour compte de stockage en modifiant hello **période de transfert (min)** valeur.

événements de Hello sont capturés à partir de sources d’événements et des manifestes d’événements que vous spécifiez. toospecify une source d’événement, entrez un nom dans hello **Sources d’événements** section, puis choisissez hello **Source d’événement ajouter** bouton. De même, vous pouvez spécifier un manifeste d’événements Bonjour **manifestes d’événements** section, puis choisissez hello **ajouter le manifeste d’événements** bouton.

  ![Journaux de suivi des événements ETW](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766025.png)

  Hello ETW framework est pris en charge dans ASP.NET via des classes dans hello [System.Diagnostics.aspx] (espace de noms https://msdn.microsoft.com/library/system.diagnostics (110). Hello Microsoft.WindowsAzure.Diagnostics espace de noms, qui hérite et étend la norme [System.Diagnostics.aspx] (classes https://msdn.microsoft.com/library/system.diagnostics (110), utilisation de hello permet de () [System.Diagnostics.aspx] https://msdn.Microsoft.com/library/System.Diagnostics (110) comme infrastructure de journalisation Bonjour environnement Azure. Pour plus d’informations, consultez [Contrôler la journalisation et le suivi dans Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) et [Activation de Diagnostics dans les services cloud et les machines virtuelles Azure](cloud-services/cloud-services-dotnet-diagnostics.md).

### <a name="crash-dumps"></a>Vidages sur incident
Si vous souhaitez toocapture informations quand une instance de rôle tombe en panne, sélectionnez hello **activer le transfert des vidages sur incident** case à cocher. (ASP.NET gérant la plupart des exceptions, cela n’est généralement utile que pour les rôles de travail.) Vous pouvez augmenter ou diminuer le pourcentage de hello de stockage espace consacré vidages sur incident de toohello en modifiant hello **le Quota de répertoire (%)** valeur. Vous pouvez modifier le conteneur de stockage hello où les vidages sur incident de hello sont stockées et vous pouvez sélectionner si vous souhaitez toocapture un **complète** ou **Mini** dump.

processus Hello actuellement suivis sont répertoriés. Activez les cases à cocher hello pour les processus hello que vous souhaitez toocapture. tooadd une autre liste de toohello de processus, entrez le nom du processus hello et puis choisissez hello **Ajouter processus** bouton.

  ![Vidages sur incident](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766026.png)

  Pour plus d’informations, consultez [Contrôler la journalisation et le suivi dans Microsoft Azure](https://msdn.microsoft.com/magazine/ff714589.aspx) et [Diagnostics Microsoft Azure, partie 4 : composants de journalisation personnalisés et modifications des diagnostics 1.3 Azure](http://justazure.com/microsoft-azure-diagnostics-part-4-custom-logging-components-azure-diagnostics-1-3-changes/).

## <a name="view-hello-diagnostics-data"></a>Afficher les données de diagnostics hello
Une fois que vous avez collecté les données de diagnostic hello pour un service cloud ou une machine virtuelle, vous pouvez l’afficher.

### <a name="tooview-cloud-service-diagnostics-data"></a>données de diagnostic tooview cloud service
1. Déployez votre service cloud comme d’habitude, puis exécutez-le.
2. Vous pouvez afficher les données de diagnostic hello dans un rapport généré par Visual Studio ou des tables dans votre compte de stockage. les données de salutation tooview dans un rapport, ouvrez **Cloud Explorer** ou **l’Explorateur de serveurs**, ouvrez le menu contextuel de hello du nœud hello pour rôle hello qui vous intéresse, puis choisissez **afficher les données de Diagnostic** .
   
    ![Afficher les données de diagnostic](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748912.png)
   
    Un rapport qui affiche les données disponibles hello s’affiche.
   
    ![Rapport de diagnostics Microsoft Azure dans Visual Studio](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796666.png)
   
    Si les données les plus récentes hello n’apparaissent pas, vous pouvez avoir toowait pour tooelapse période de transfert hello.
   
    Choisissez hello **Actualiser** lier des données de hello tooimmediately mise à jour, ou choisissez un intervalle Bonjour **actualisation automatique** déroulante liste toohave hello données mis à jour automatiquement. données d’erreur tooexport hello, choisissez hello **exporter tooCSV** bouton toocreate un fichier de valeurs séparées par des virgules que vous pouvez ouvrir dans une feuille de calcul.
   
    Dans **Cloud Explorer** ou **l’Explorateur de serveurs**, ouvrez le compte de stockage hello a associé à un déploiement de hello.
3. Ouvrir des tables de diagnostics hello dans la visionneuse de table hello et examinez les données de salutation que vous avez collectées. Pour les journaux IIS et les journaux personnalisés, vous pouvez ouvrir un conteneur d’objets blob. En consultant hello tableau suivant, vous pouvez trouver le conteneur hello table ou un objet blob qui contient les données hello qui vous intéressent. En outre toohello des données pour ce fichier journal, les entrées de table hello contiennent EventTickCount, DeploymentId, rôle, toohelp RoleInstance vous identifiez la machine virtuelle et rôle de la génération des données de hello et à quel moment. 
   
   | Données de diagnostic | Description | Lieu |
   | --- | --- | --- |
   | Journaux d’application |Journaux générés par l’appelant des méthodes de hello classe System.Diagnostics.Trace votre code. |WADLogsTable |
   | Journaux d’événements |Ces données sont à partir des journaux des événements Windows hello sur des machines virtuelles de hello. Windows stocke les informations dans ces journaux, mais les applications et services également les erreurs de tooreport ou enregistrement des informations. |WADWindowsEventLogsTable |
   | Compteurs de performance |Vous pouvez collecter des données sur n’importe quel compteur de performance qui est disponible sur l’ordinateur virtuel de hello. système d’exploitation de Hello fournit des compteurs de performances qui comprennent de nombreuses statistiques telles que le délai de processeur et de l’utilisation de mémoire. |WADPerformanceCountersTable |
   | Journaux d’infrastructure |Ces journaux sont générés à partir de l’infrastructure de diagnostics hello elle-même. |WADDiagnosticInfrastructureLogsTable |
   | Journaux IIS |Ces journaux enregistrent les requêtes web. Si votre service cloud obtient une quantité importante de trafic, ces journaux peuvent être assez longs. Il est donc conseillé de collecter et de stocker ces données uniquement en cas de besoin. |Vous pouvez trouver l’échec des journaux de requêtes dans le conteneur d’objets blob hello sous wad-iis-failedreqlogs, sous un chemin d’accès pour ce déploiement, le rôle et l’instance. Vous trouverez les journaux complets sous wad-iis-logfiles. Entrées pour chaque fichier sont effectuées dans la table de WADDirectories hello. |
   | Vidages sur incident |Ces informations fournissent des images binaires du processus de votre service cloud (généralement, un rôle de travail). |Conteneur d’objets blob wad-crush-dumps |
   | Fichiers journaux personnalisés |Journaux de données que vous avez prédéfinis. |Vous pouvez spécifier dans l’emplacement des fichiers journaux personnalisés hello du code dans votre compte de stockage. Par exemple, vous pouvez spécifier un conteneur d’objets blob personnalisé. |
4. Si les données de n’importe quel type sont tronquées, vous pouvez essayer croissante tampon hello pour ce type de données ou la réduction intervalle hello entre les transferts de données à partir du compte de stockage tooyour hello machine virtuelle.
5. (facultatif) Purger les données à partir du stockage de hello compte tooreduce parfois les coûts de stockage globaux.
6. Lorsque vous effectuez un déploiement complet, fichier de diagnostics.cscfg hello (.wadcfgx pour Azure SDK 2.5) est mis à jour dans Azure et votre service cloud récupère toute configuration de diagnostics de tooyour de modifications. Si vous, au lieu de cela, mettez à jour un déploiement existant, fichier .cscfg de hello n’est pas mis à jour dans Azure. Vous pouvez toujours modifier les paramètres de diagnostic, cependant, en suivant les étapes de hello dans la section suivante de hello. Pour plus d’informations sur l’exécution d’un déploiement complet et la mise à jour d’un déploiement existant, consultez [Assistant Publication d’application Azure](vs-azure-tools-publish-azure-application-wizard.md).

### <a name="tooview-virtual-machine-diagnostics-data"></a>données de diagnostic de machine virtuelle tooview
1. Dans le menu contextuel de hello pour la machine virtuelle de hello, choisissez **afficher les données de Diagnostics**.
   
    ![Afficher les données de diagnostic dans la machine virtuelle Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC766027.png)
   
    Cette opération ouvre hello **résumé des Diagnostics** fenêtre.
   
    ![Résumé des diagnostics de la machine virtuelle Azure](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC796667.png)  
   
    Si les données les plus récentes hello n’apparaissent pas, vous pouvez avoir toowait pour tooelapse période de transfert hello.
   
    Choisissez hello **Actualiser** lier des données de hello tooimmediately mise à jour, ou choisissez un intervalle Bonjour **actualisation automatique** déroulante liste toohave hello données mis à jour automatiquement. données d’erreur tooexport hello, choisissez hello **exporter tooCSV** bouton toocreate un fichier de valeurs séparées par des virgules que vous pouvez ouvrir dans une feuille de calcul.

## <a name="configure-cloud-service-diagnostics-after-deployment"></a>Configuration des diagnostics de service cloud après déploiement
Si vous recherchez un problème avec un service cloud en cours d’exécution, vous pourriez toocollect les données que vous n’avez pas spécifié avant le rôle hello déployé à l’origine de vous. Dans ce cas, vous pouvez démarrer toocollect que les données à l’aide des paramètres de hello dans l’Explorateur de serveurs. Vous pouvez configurer les diagnostics pour une instance unique ou de toutes les instances de hello dans un rôle, selon que vous ouvrez la boîte de dialogue de Configuration des Diagnostics hello à partir du menu contextuel de hello pour l’instance de hello ou un rôle de hello. Si vous configurez le nœud de rôle hello, toutes les modifications s’appliquent à des instances de tooall. Si vous configurez le nœud d’instance hello, toutes les modifications appliquées instance toothat uniquement.

### <a name="tooconfigure-diagnostics-for-a-running-cloud-service"></a>tooconfigure des diagnostics pour un service cloud en cours d’exécution
1. Dans l’Explorateur de serveurs, développez hello **Services de cloud computing** nœud, puis développez le rôle de nœuds toolocate hello ou d’instance que vous souhaitez tooinvestigate ou les deux.
   
    ![Configuration des diagnostics](./media/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines/IC748913.png)
2. Dans le menu contextuel de hello pour un nœud d’instance ou un nœud de rôle, choisissez **mise à jour les paramètres de diagnostic**, puis, choisissez les paramètres de diagnostic que vous souhaitez toocollect hello.
   
    Pour plus d’informations sur les paramètres de configuration hello, consultez **configurer des sources de données de diagnostics** dans cette rubrique. Pour plus d’informations sur la façon dont tooview hello les données de diagnostic, consultez **permet d’afficher les données de diagnostic hello** dans cette rubrique.
   
    Si vous modifiez la collecte de données dans l’ **Explorateur de serveurs**, ces modifications continuent à s’appliquer jusqu’au redéploiement complet de votre service cloud. Si vous utilisez des paramètres de publication par défaut de hello, modifications de hello ne sont pas remplacées, car de publication par défaut de hello paramètre déploiement existant de hello tooupdate, plutôt que de faire un redéploiement complet. paramètres de hello que toomake sont effacés au moment du déploiement, accédez toohello **paramètres avancés** onglet dans l’Assistant de publication hello et désactivez hello **mise à jour du déploiement** case à cocher. Lorsque vous redéployez cette case à cocher, les paramètres de hello reviennent toothose dans le fichier .wadcfgx (ou .wadcfg) de hello en tant qu’ensemble via l’éditeur de propriétés hello pour le rôle de hello. Si vous mettez à jour votre déploiement, Azure conserve les anciens paramètres de hello.

## <a name="troubleshoot-azure-cloud-service-issues"></a>Dépannage de problèmes de service cloud Azure
Si vous rencontrez des problèmes avec vos projets de service cloud, par exemple un rôle qui reste bloqué dans un état « occupé », à plusieurs reprises est recyclé, ou lève une erreur interne au serveur, il existe des outils et techniques que vous pouvez utiliser toodiagnose et résoudre ces problèmes. Pour des exemples spécifiques de problèmes courants et solutions, ainsi qu’une vue d’ensemble des concepts de hello et outils utilisés toodiagnose et corriger ces erreurs, consultez [données de diagnostic de calcul PaaS Azure](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

## <a name="q--a"></a>Questions et réponses
**Quelle est la taille de mémoire tampon hello et comment doit-elle être ?**

Sur chaque instance de la machine virtuelle, les quotas de limitent la quantité des données de diagnostic peuvent être stockées sur le système de fichiers local hello. De plus, vous pouvez spécifier une taille de mémoire tampon pour chaque type de données de diagnostic disponible. Cette taille de mémoire tampon joue le rôle de quota individuel pour ce type de données. En bas de hello de boîte de dialogue hello sur la vérification, vous pouvez déterminer hello quota global et quantité hello de mémoire restante. Si vous spécifiez des mémoires tampons plus volumineuses ou autres types de données, vous approchez hello quota global. Vous pouvez modifier hello quota global en modifiant le fichier de configuration diagnostics.wadcfg/.wadcfgx hello. diagnostics Hello données sont stockées sur hello même système de fichiers en tant que données de votre application, donc si votre application utilise beaucoup d’espace disque, vous ne devez pas augmenter hello quota global de diagnostics.

**Quelle est la période de transfert hello et la durée pendant laquelle il convient ?**

période de transfert Hello est hello temps qui s’écoule entre les données de capture. Après chaque période de transfert, les données sont déplacées à partir du système de fichiers local hello sur une machine virtuelle tootables dans votre compte de stockage. Si montant hello des données collectées dépasse le quota de hello avant la fin de hello d’une période de transfert, les données antérieures sont ignorées. Vous pouvez choisir la période de transfert hello toodecrease si vous perdez des données, car vos données dépassent la taille de mémoire tampon hello ou hello quota global.

**Quel fuseau horaire sont des horodatages dans hello ?**

les horodatages Hello se trouvent dans le fuseau horaire local de hello hello du centre de données qui héberge votre service cloud. Hello trois colonnes d’horodateur suivantes dans les tables de journal hello sont utilisées.

* **PreciseTimeStamp** est l’horodatage ETW de hello d’événement de hello. Autrement dit, événement hello hello est enregistré à partir du client de hello.
* **HORODATAGE** est la valeur PreciseTimeStamp arrondie toohello limite de fréquence de téléchargement. Par conséquent, si votre fréquence de téléchargement est de 5 minutes et les événements hello heure 00:17:12, TIMESTAMP sera 00:15:00.
* **Horodatage** est timestamp hello à quels hello entité a été créée dans hello table Azure.

**Comment gérer les coûts pendant la collecte d’informations de diagnostics ?**

Hello des paramètres par défaut (**niveau de journal** défini trop**erreur** et **période de transfert** défini trop**1 minute**) sont conçu toominimize de coût. Vos coûts de calcul augmente si collecter plus de données de diagnostic ou de réduire la période de transfert hello. Ne collectez pas plus de données que vous avez besoin et n’oubliez pas toodisable la collecte de données lorsque vous n’avez plus besoin. Vous pouvez toujours réactiver, même pendant l’exécution, comme indiqué dans la section précédente de hello.

**Comment recueillir des journaux de demandes IIS ayant échoué ?**

Par défaut, IIS ne collecte pas les journaux de demandes ayant échoué. Vous pouvez configurer toocollect IIS les si vous modifiez hello le fichier web.config pour votre rôle web.

**Je n’obtiens pas les informations des méthodes RoleEntryPoint comme OnStart. Que se passe-t-il ?**

méthodes de Hello de RoleEntryPoint sont appelées dans le contexte de hello de WAIISHost.exe, non d’IIS. Hello, par conséquent, les informations de configuration dans le fichier web.config qui normalement ne s’applique pas Active le traçage. tooresolve ce problème, ajoutez un projet de rôle web tooyour .config fichier et nommez hello fichier toomatch hello assembly de sortie qui contient le code de RoleEntryPoint hello. Dans le projet de rôle web par défaut hello nom hello du fichier de hello .config serait WAIISHost.exe.config. Ajoutez ensuite hello lignes toothis fichier suivant :

```
<system.diagnostics>
  <trace>
      <listeners>
          <add name “AzureDiagnostics” type=”Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener”>
              <filter type=”” />
          </add>
      </listeners>
  </trace>
</system.diagnostics>
```

Maintenant, dans hello **propriétés** fenêtre, jeu hello **copier tooOutput active** propriété trop**toujours copier**.

## <a name="next-steps"></a>Étapes suivantes
toolearn savoir plus sur les diagnostics de journalisation dans Azure, consultez [activation des Diagnostics dans Azure Cloud Services et Machines virtuelles](cloud-services/cloud-services-dotnet-diagnostics.md) et [activer la journalisation des diagnostics pour les applications web dans Azure App Service](app-service-web/web-sites-enable-diagnostic-log.md).

