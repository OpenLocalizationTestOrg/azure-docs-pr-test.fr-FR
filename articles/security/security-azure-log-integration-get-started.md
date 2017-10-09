---
title: "aaaGet a démarré avec l’intégration d’Azure log | Documents Microsoft"
description: "Découvrez comment tooinstall hello Azure journal service d’intégration et intégrer des journaux de stockage Azure, les journaux d’Audit Azure et les alertes du centre de sécurité Azure."
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 53f67a7c-7e17-4c19-ac5c-a43fabff70e1
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 07/26/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 26c19070d76ff73b1bdbd32ba77fb04978af387e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-with-azure-diagnostics-logging-and-windows-event-forwarding"></a>Intégration des journaux Azure avec Azure Diagnostics Logging et Windows Event Forwarding
Intégration d’Azure journal (AzLog) vous permet de toointegrate les journaux brut à partir de vos ressources Azure dans vos systèmes d’informations sur la sécurité et de gestion des événements (SIEM) local. Cette intégration rend possible toohave un tableau de bord unifiée de la sécurité pour tous vos actifs, en local ou dans le cloud de hello, afin que vous pouvez agréger, mettre en corrélation, l’analyse et alerte pour les événements de sécurité associés à vos applications.
>[!NOTE]
Pour plus d’informations sur l’intégration des journaux Azure, vous pouvez consulter hello [vue d’ensemble de l’intégration du journal Azure](https://docs.microsoft.com/azure/security/security-azure-log-integration-overview).

Cet article vous aidera à commencer par en mettant l’accent sur l’installation de hello de hello Azlog service et l’intégration de service de hello avec Azure Diagnostics avec l’intégration des journaux Azure. Hello service d’intégration des journaux Azure sera alors en mesure de toocollect les informations de journal des événements Windows à partir de hello canal d’événement de sécurité de Windows à partir d’ordinateurs virtuels déployés dans Azure IaaS. Cela est très similaire trop « Transfert d’événements » que vous avez peut-être utilisé localement.

>[!NOTE]
>sortie de hello toobring Hello possibilité d’intégration d’Azure log dans toohello SIEM est fournie par hello SIEM lui-même. Consultez l’article de hello [intégration de l’intégration du journal Azure avec votre serveur SIEM local](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) pour plus d’informations.

toobe très claire - hello service d’intégration des journaux Azure s’exécute sur un ordinateur physique ou virtuel qui est à l’aide de hello Windows Server 2008 R2 ou version ultérieure de système d’exploitation (Windows Server 2012 R2 ou Windows Server 2016 sont par défaut).

ordinateur physique sur Hello puisse exécuter localement (ou sur un site de l’hébergeur). Si vous choisissez le service d’intégration des journaux Azure de hello toorun sur un ordinateur virtuel, que l’ordinateur virtuel peut être située localement ou dans un cloud public, tel que Microsoft Azure.

Hello physique ou machine virtuelle exécutant le service d’intégration des journaux Azure hello nécessite toohello de connectivité réseau cloud public Azure. Étapes de cet article fournissent des détails sur la configuration de hello.

## <a name="prerequisites"></a>Composants requis
Au minimum, l’installation de hello de AzLog nécessite hello éléments suivants :
* Un **abonnement Azure**. Si vous n’en possédez pas, vous pouvez vous inscrire pour créer dès aujourd’hui un [compte gratuit](https://azure.microsoft.com/free/).
* A **compte de stockage** qui peut être utilisé pour la journalisation des diagnostics Windows Azure (vous pouvez utiliser un compte de stockage préconfigurées, ou créer un nouveau – nous démontrer comment tooconfigure hello compte de stockage plus loin dans cet article)
  >[!NOTE]
  Selon votre scénario, un compte de stockage n’est peut-être pas nécessaire. Pourquoi le scénario de diagnostics Azure abordées dans cet article que nécessaire.
* **Deux systèmes**: un ordinateur qui exécutera le service d’intégration des journaux Azure hello et un ordinateur qui sera analysé et avoir ses informations de journalisation envoyées toohello Azlog ordinateur du service.
   * Un ordinateur que vous souhaitez toomonitor – il s’agit d’une machine virtuelle en cours d’exécution en tant qu’un [Machine virtuelle Azure](../virtual-machines/virtual-machines-windows-overview.md)
   * Un ordinateur qui exécutera le service d’intégration de Azure log hello ; Cet ordinateur collecte toutes les informations de journal hello plus tard à importer dans votre serveur SIEM.
    * Ce système peut être local ou dans Microsoft Azure.  
    * Il doit toobe en cours d’exécution un x64 version de Windows server 2008 R2 SP1 ou version ultérieure et que .NET 4.5.1 installé. Vous pouvez déterminer la version de .NET hello installée par hello ci-dessous intitulée [Comment : déterminer les .NET Framework Versions installées](https://msdn.microsoft.com/library/hh925568)  
    Il doit avoir le compte de stockage Azure connectivité toohello utilisé pour la journalisation des diagnostics Azure. Nous fournirons des instructions plus loin dans cet article sur la façon dont vous pouvez vérifier cette connectivité

Pour une démonstration rapide du processus de création d’un ordinateur virtuel à l’aide de hello portail Azure de hello Examinons hello vidéo ci-dessous.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Create-a-Virtual-Machine/player]



## <a name="deployment-considerations"></a>Points à prendre en considération pour le déploiement
Alors que vous testez l’intégration des journaux Azure, vous pouvez utiliser n’importe quel système qui répond aux exigences de configuration minimale du système d’exploitation hello. Toutefois, un Bonjour d’environnement de production charge peut nécessiter un tooplan vous mise à l’échelle de façon horizontale ou verticale.

Vous pouvez exécuter plusieurs instances du service d’intégration des journaux Azure hello (une seule instance par ordinateur physique ou virtuel) si le volume des événements est élevé. En outre, vous pouvez équilibrer la charge des comptes de stockage des Diagnostics Azure pour Windows (WAD) et le nombre hello d’instances de toohello tooprovide abonnements doivent être basés sur votre capacité.
>[!NOTE]
À ce stade ne pas avoir des recommandations spécifiques pour laquelle tooscale des instances d’Azure journal machines d’intégration (autrement dit, les ordinateurs qui exécutent le service d’intégration Azure log hello), ou pour les abonnements ou les comptes de stockage. Les décisions de mise à l’échelle doivent être basées sur vos observations de performances dans chacun de ces domaines.

Vous avez également tooscale d’option hello des toohelp de service d’intégration des journaux Azure hello améliorer les performances. Hello suivant des métriques de performances peut vous aider à dimensionner les machines hello que vous choisissez le service d’intégration Azure log toorun hello :
* Sur un ordinateur 8 processeurs (cœurs), une seule instance de l’intégrateur Azlog peut traiter environ 24 millions d’événements par jour (environ 1 million/heure).

* Sur un ordinateur 4 processeurs (cœurs), une seule instance de l’intégrateur Azlog peut traiter environ 1,5 million d’événements par jour (environ 62 500 millions/heure).

## <a name="install-azure-log-integration"></a>Installer l’intégration des journaux Azure
tooinstall intégration des journaux Azure, vous devez les hello toodownload [intégration d’Azure log](https://www.microsoft.com/download/details.aspx?id=53324) fichier d’installation. Exécutez via le programme d’installation de hello et décider si vous souhaitez tooprovide télémétrie informations tooMicrosoft.  

![Écran d’installation avec la case Télémétrie cochée](./media/security-azure-log-integration-get-started/telemetry.png)

*
> [!NOTE]
> Nous vous conseillons d’autoriser les données de télémétrie toocollect Microsoft. Vous pouvez désactiver la collecte des données de télémétrie en décochant cette option.
>


Hello service d’intégration des journaux Azure collecte les données de télémétrie d’ordinateur hello sur lequel il est installé.  

Les données de télémétrie recueillies sont les suivantes :

* Les exceptions qui se produisent pendant l’exécution de l’intégration des journaux Azure
* Métriques sur le nombre de hello de requêtes et des événements traités
* Des statistiques sur les options de ligne de commande Azlog.exe sont utilisées

processus d’installation Hello est abordée dans hello vidéo ci-dessous.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Install-Azure-Log-Integration/player]



## <a name="post-installation-and-validation-steps"></a>Étapes postérieures à l’installation et la validation
Après avoir effectué la routine de paramétrage de base hello, vous êtes prêt étape tooperform post validation et installation comme suit :
1. Ouvrez une fenêtre PowerShell avec élévation de privilèges et accédez trop**c:\Program Files\Microsoft Azure journal d’intégration**
2. Hello première étape tootake est hello tooget Qu'azlog Cmdlets importé. C’est également en exécutant le script de hello **LoadAzlogModule.ps1** (Notez hello ». \ « Bonjour commande suivante). Saisissez **.\LoadAzlogModule.ps1** et appuyez sur **Entrée**.  
Vous devez voir quelque chose comme ce qui apparaît dans la figure ci-dessous hello. </br></br>
![Écran d’installation avec la case Télémétrie cochée](./media/security-azure-log-integration-get-started/loaded-modules.png) </br></br>
3. Vous devez maintenant tooconfigure AzLog toouse un environnement Azure spécifique. Un « environnement Azure » est hello « type » du centre de données de cloud computing Azure avec que vous souhaitez toowork. Lorsqu’il existe plusieurs environnements Azure à ce stade, les options pertinentes actuellement hello sont **cloud Azure** ou **AzureUSGovernment**.   Dans votre environnement PowerShell avec élévation de privilèges, assurez-vous de vous trouver dans **c:\program files\Microsoft Azure Log Integration\** </br></br>
    Une fois, exécutez les commandes hello : </br>
    ``Set-AzlogAzureEnvironment -Name AzureCloud`` (pour Azure Commercial)

      >[!NOTE]
      Lors de la commande hello réussit, vous ne recevrez pas de vos commentaires.  Si vous souhaitez que le cloud de Azure de US Government toouse hello, vous utiliseriez **AzureUSGovernment** (pour hello - variable de nom) pour le cloud de gouvernement États-Unis de hello. Les autres clouds Azure ne sont pas pris en charge pour l’instant.  
4. Avant de pouvoir analyser un système vous devez nom hello hello du compte de stockage en cours d’utilisation pour les Diagnostics Azure.  Bonjour Azure portal accédez trop**virtuels** et recherchez la machine virtuelle hello que vous allez surveiller. Bonjour **propriétés** , choisissez **les paramètres de Diagnostic**.  Cliquez sur **Agent** et prenez note du nom de compte de stockage hello spécifié. Vous aurez besoin de ce nom de compte pour une étape ultérieure.
![Paramètres des diagnostics Azure](./media/security-azure-log-integration-get-started/storage-account-large.png) </br></br>

      ![Paramètres des diagnostics Azure](./media/security-azure-log-integration-get-started/azure-monitoring-not-enabled-large.png)
      >[!NOTE]
      Si l’analyse n’a pas été activé lors de la création de la machine virtuelle vous sera attribué hello option tooenable comme indiqué ci-dessus.
5. Maintenant, nous allons basculer notre toohello de retour attention machine d’intégration Azure log. Nous devons tooverify que vous avez connectivité toohello compte de stockage de système de hello où vous avez installé l’intégration du journal Azure. ordinateur physique de Hello ou de la machine virtuelle en cours d’exécution hello Azure journal d’intégration de service a besoin d’accéder aux informations de tooretrieve du compte de stockage toohello consignées par les Diagnostics Azure comme étant configuré sur chacun des hello analysé systèmes.  
  1. Vous pouvez télécharger l’Explorateur de stockage Azure [ici](http://storageexplorer.com/).
  2. Exécuter via le programme d’installation de hello
  3. Une fois l’installation de hello terminé cliquez **suivant** et laissez la case à cocher hello **lancer Microsoft Azure Storage Explorer** activée.  
  4. Ouvrez une session dans tooAzure.
  5. Vérifiez que vous pouvez voir le compte de stockage hello que vous avez configuré pour les Diagnostics Azure.  
![Comptes de stockage](./media/security-azure-log-integration-get-started/storage-account.jpg) </br></br>
   6. Notez qu’il existe quelques options sous Comptes de stockage. L’une d’entre elles est **Tables**. Sous **Tables**, vous devriez voir une table nommée **WADWindowsEventLogsTable**. </br></br>
   ![Comptes de stockage](./media/security-azure-log-integration-get-started/storage-explorer.png) </br>

## <a name="integrate-azure-diagnostic-logging"></a>Intégrer la journalisation des diagnostics Azure
Dans cette étape, vous allez configurer l’ordinateur hello hello Azure journal Integration service tooconnect toohello compte de stockage qui contient les fichiers journaux de hello en cours d’exécution.
toocomplete cette étape, nous aurons besoin de quelques éléments au préalable.  
* **FriendlyNameForSource :** il s’agit d’un nom convivial que vous pouvez appliquer toohello compte de stockage que vous avez configuré les informations toostore hello ordinateur virtuel à partir d’Azure Diagnostics
* **StorageAccountName :** il s’agit nom hello hello du compte de stockage que vous avez spécifié lors de la configuration de diagnostic Azure.  
* **Clé de stockage :** Voici hello stockage clé hello compte de stockage où hello informations de Diagnostics Azure est stockée pour cet ordinateur virtuel.  

Effectuez hello étapes tooobtain hello stockage clé suivante :
 1. Parcourir toohello [portail Azure](http://portal.azure.com).
 2. Dans le volet de navigation hello Hello Azure de la console, faites défiler toohello bas, cliquez sur **davantage de services.**

 ![Plus de services](./media/security-azure-log-integration-get-started/more-services.png)
 3. Entrez **stockage** Bonjour **filtre** zone de texte. Cliquez sur **Comptes de stockage** (option qui apparaît une fois que vous entrez **Stockage**)

   ![zone filtre](./media/security-azure-log-integration-get-started/filter.png)
 4. Une liste de comptes de stockage s’affiche, double-cliquez sur compte hello que vous avez affecté tooLog stockage.

   ![liste des comptes de stockage](./media/security-azure-log-integration-get-started/storage-accounts.png)
 5. Cliquez sur **clés d’accès** Bonjour **paramètres** section.

  ![clés d'accès](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 6. Copie **key1** et le placer dans un emplacement sécurisé auquel vous pouvez accéder à l’étape suivante de hello.

   ![deux clés d’accès](./media/security-azure-log-integration-get-started/storage-account-access-keys.png)
 7. Sur le serveur hello que vous avez installé l’intégration des journaux Azure, ouvrez une invite de commandes avec élévation de privilèges (Notez que nous utilisons ici une fenêtre d’invite de commandes avec élévation de privilèges, pas une console PowerShell avec élévation de privilèges).
 8. Accédez trop**c:\Program Files\Microsoft Azure journal d’intégration**
 9. Exécutez ``Azlog source add <FriendlyNameForTheSource> WAD <StorageAccountName> <StorageKey> ``. </br> Par exemple ``Azlog source add Azlogtest WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==`` si vous souhaitez que hello abonnement ID tooshow dans XML d’événement hello, ajoutez le nom convivial toohello ID d’abonnement hello : ``Azlog source add <FriendlyNameForTheSource>.<SubscriptionID> WAD <StorageAccountName> <StorageKey>`` ou, par exemple,``Azlog source add Azlogtest.YourSubscriptionID WAD Azlog9414 fxxxFxxxxxxxxywoEJK2xxxxxxxxxixxxJ+xVJx6m/X5SQDYc4Wpjpli9S9Mm+vXS2RVYtp1mes0t9H5cuqXEw==``

>[!NOTE]  
Attendez jusqu'à too60 minutes, puis afficher les événements de hello sont extraites de compte de stockage hello. tooview, ouvrez **Observateur d’événements > journaux Windows > événements transmis** sur hello Azlog intégrateur.

Ici, vous pouvez voir une vidéo sur les étapes de hello visées ci-dessus.
> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Enable-Diagnostics-and-Storage/player]


## <a name="what-if-data-is-not-showing-up-in-hello-forwarded-events-folder"></a>Que se passe-t-il si les données s’affichent pas dossier d’événements transmis hello ?
Si après une heure données s’affichent pas Bonjour **événements transmis** dossier, puis :

1. Vérifier le service de journal d’intégration de Azure hello machine en cours d’exécution hello et confirmer qu’il peut accéder à Azure. tootest connectivité, essayez tooopen hello [portail Azure](http://portal.azure.com) à partir du navigateur de hello.
2. Vérifiez que compte d’utilisateur hello **Azlog** a l’autorisation d’écriture sur le dossier de hello **users\Azlog**.
  <ol type="a">
   <li>Ouvrez l’**Explorateur Windows** </li>
  <li> Accédez trop**c:\users** </li>
  <li> Faites un clic droit sur **c:\users\Azlog** </li>
  <li> Cliquez sur **Sécurité**  </li>
  <li> Cliquez sur **NT Service\Azlog** et vérifier les autorisations hello pour le compte de hello. Si le compte de hello est absent de cet onglet, ou si les autorisations appropriées hello ne sont pas actuellement montrant vous pouvez accorder des droits de compte hello dans cet onglet.</li>
  </ol>
3.Que compte de stockage que hello ajouté dans la commande hello **Azlog source ajouter** figure lorsque vous exécutez la commande hello **liste des sources Azlog**.
4. Accédez trop**Observateur d’événements > journaux Windows > Application** toosee si des erreurs sont signalées à partir de l’intégration d’Azure log hello.


Si vous rencontrez des problèmes pendant l’installation de hello et de configuration, ouvrez un [demande de support](../azure-supportability/how-to-create-azure-support-request.md), sélectionnez **journal intégration** en tant que service hello pour lequel vous demandez la prise en charge.

Une autre option de prise en charge est hello [Forum MSDN de Azure journal intégration](https://social.msdn.microsoft.com/Forums/home?forum=AzureLogIntegration). Ici Communauté de hello peut prendre en charge l’autre avec des questions, des réponses, des conseils et astuces sur comment tooget hello plus en dehors de l’intégration du journal Azure. En outre, l’équipe d’intégration du journal Azure hello surveille ce forum et aidera à chaque fois que nous pouvons.

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur l’intégration des journaux Azure, consultez hello suivant des documents :

* [Microsoft Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) : Centre de téléchargement pour plus d’informations, la configuration système requise et les instructions d’installation sur l’intégration des journaux Azure.
* [Intégration du journal tooAzure introduction](security-azure-log-integration-overview.md) : ce document présente tooAzure journal intégration, ses fonctionnalités clées, et comment il fonctionne.
* [Étapes de configuration du partenaire](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – ce billet de blog montre comment tooconfigure Azure du journal toowork d’intégration avec les solutions de partenaire Splunk, HP ArcSight et QRadar d’IBM. Il s’agit de notre Conseil actuel sur comment tooconfigure hello les composants serveur SIEM. Pour plus d’informations, contactez d’abord votre fournisseur SIEM.
* [FAQ de l’intégration des journaux Azure](security-azure-log-integration-faq.md) : ce forum aux questions répond aux questions sur l’intégration des journaux Azure.
* [Intégration de centre de sécurité les alertes avec Azure journal intégration](../security-center/security-center-integrating-alerts-with-log-integration.md) – ce document vous montre comment le centre de sécurité toosync des alertes, ainsi que des événements de sécurité d’ordinateur virtuel collectées par Diagnostics Windows Azure et les journaux d’activité Azure, avec votre analytique de journal ou la solution SIEM.
* [Nouvelles fonctionnalités pour les diagnostics Azure et les journaux d’Audit Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) – ce billet de blog vous présente les journaux d’Audit de tooAzure et autres fonctionnalités qui vous aident à obtenir les opérations hello de vos ressources Azure.
