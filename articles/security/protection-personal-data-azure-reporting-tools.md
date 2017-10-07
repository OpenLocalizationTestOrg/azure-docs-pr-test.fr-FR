---
title: "une protection des données personnelles avec les outils de rapport Azure aaaDocument | Documents Microsoft"
description: "Comment toouse toohelp de technologies et services de création de rapports Azure protéger la confidentialité des données personnelles."
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 3230d26ed308a8a0e72421c001793be06334a7c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="document-protection-of-personal-data-with-azure-reporting-tools"></a>Protection des données personnelles dans les documents avec les outils de rapport Azure

Cet article explique comment toouse Azure reporting services et technologies toohelp protéger la confidentialité des données personnelles.

## <a name="scenario"></a>Scénario

Une société de croisière volumineux en hello États-Unis, étend ses itinéraires de toooffer d’opérations dans hello Méditerranée, Adriatique et mer Baltique, ainsi que hello britanniques. toohelp ces efforts, elle a acquis plusieurs lignes croisière plus petits exercées en Italie, Allemagne, Danemark et hello Royaume-Uni

la société de Hello utilise Microsoft Azure pour le traitement et stockage des données d’entreprise. Ces dernières incluent des informations d’identification personnelle telles que les noms, les adresses, les numéros de téléphone et les informations de carte de crédit de sa base de clients globale. Il inclut également des informations de ressources humaines traditionnelles telles que les adresses et numéros de téléphone, numéros d’identification de taxe médicales plus d’informations sur les employés de la société dans tous les emplacements. ligne de croisière Hello gère également les bases de données volumineuses de membres du programme de récompense et fidélité qui inclut des informations personnelles tootrack des relations avec les clients en cours et passées.

Réseau de hello accès employés de l’entreprise à partir de sites distants et les agents de voyage société hello situés dans Bonjour tout le monde ont accès aux ressources de l’entreprise toosome.

## <a name="problem-statement"></a>Définition du problème

société de Hello doit protéger la confidentialité de hello des données personnelles des employés et des clients via une stratégie de sécurité multicouche qui utilise des fonctionnalités tooimpose stricte des contrôles de sécurité sur le traitement de tooand d’accès des données personnelles et de gestion Azure et doit être toodemonstrate en mesure de mesures de sa protection toointernal et les auditeurs externes.

## <a name="company-goal"></a>Objectif de l’entreprise

Dans le cadre de sa stratégie de sécurité de défense en profondeur, il est un tootrack d’objectif de société de traitement de tooand tous les accès des données personnelles et vous assurer que la documentation de protections adéquates confidentialité des données personnelles sont en place et fonctionne.

## <a name="solutions"></a>Solutions

Microsoft Azure fournit la journalisation de suivi, complète et toohelp des outils de diagnostics effectuer le suivi et enregistrer des activités et événements associés à l’accès et le traitement des données personnelles, géographique flux de données et les données de toopersonal accès tiers. Sécurité des données personnelles dans le cloud de hello étant une responsabilité partagée, Microsoft fournit également des clients avec :

- Informations détaillées sur son propre traitement des données des clients

- Mesures de sécurité administrées par Microsoft

- Emplacement et méthodes d’envoi des données des clients

- Détails du propre processus de révision de la confidentialité de Microsoft

### <a name="azure-active-directory"></a>Azure Active Directory

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) est le service Microsoft de gestion d’annuaires et d’identités multilocataire basé sur le cloud. Hello connectez-vous du service et les fonctions de rapport d’audit vous fournissent de connexion détaillées et application d’utilisation activité informations toohelp surveiller et vérifiez que les données de personnel toocustomers' accès approprié et les employés.

Il existe deux types de rapports d’activité :

- Hello [activité rapports/journaux d’audit](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) fournissent un enregistrement détaillé des activités/tâches système

- Hello [journal/rapport d’activité des connexions](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) vous indique qui a effectué chaque activité répertoriée dans le rapport d’audit de hello

L’utilisation conjointe de hello deux, vous pouvez suivre l’historique de hello de chaque tâche d’exécution et qui a effectué chacune. Les deux types de rapports sont personnalisables et peuvent être filtrés.

#### <a name="how-do-i-access-hello-audit-and-security-logs"></a>Comment accéder audit de hello et la sécurité des journaux ?

Hello journaux d’audit et de sécurité sont accessibles à partir du portail d’Active Directory hello de trois manières différentes : via hello **activité** section (sélectionnez **journaux d’Audit** ou **connexions**), ou à partir de **utilisateurs et groupes** ou **des applications d’entreprise** sous **gérer** dans Active Directory. Les rapports sont également accessibles via Azure Active Directory de hello API de création de rapports. 

1. Bonjour portail Azure, sélectionnez **Azure Active Directory.**

2. Bonjour **activité** section, sélectionnez **journaux d’Audit.**

    ![](media/protection-personal-data-azure-reporting-tools/image001.png)

3. Personnaliser l’affichage de liste hello en cliquant sur **colonnes** dans la barre d’outils hello.

4.  Sélectionnez un élément dans hello liste Vue toosee toutes les informations disponibles à ce sujet.

    ![](media/protection-personal-data-azure-reporting-tools/image003.png)

La création de rapports Azure Active Directory inclut également deux types de rapports de sécurité, **Utilisateurs avec indicateur de risque** et **Connexions à risque**, qui peuvent vous aider à surveiller les risques potentiels dans votre environnement Azure.

Pour plus d’informations sur hello reporting services, consultez [reporting d’Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal)

Visitez [rapports d’activité Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal#activity-reports) pour plus d’informations sur les rapports de hello disponibles dans Azure Active Directory. Ce site contient plus de détails sur la façon tooaccess et utiliser [rapports d’activité des journaux d’audit](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) et [rapports d’activité de connexion](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins) dans le portail de hello. Il inclut également des informations sur les rapports de sécurité [Utilisateurs avec indicateur de risque](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-user-at-risk) et [Connexions à risque](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-security-risky-sign-ins).

Visitez hello [l’audit Azure Active Directory référence d’API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-audit-reference) site pour plus d’informations sur la façon de tooconnect tooAzure répertoire reporting par programme.

### <a name="log-analytics"></a>Log Analytics

[Journal Analytique](https://azure.microsoft.com/services/log-analytics/) pouvez [collecter des données à partir du moniteur de Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage) toocorrelate avec les autres données et fournissent des analyses supplémentaires. Azure Monitor recueille et analyse les données de surveillance de votre environnement Azure. 

Les outils d’analyse de Log Analytics, tels que les recherches dans les journaux, les vues et les solutions fonctionnent avec toutes les données collectées. Vous disposez ainsi d’une analyse centralisée de l’ensemble de votre environnement. Analytique de journal pouvez agréger et analyser les journaux des événements Windows, les journaux IIS et auditées, ce qui peuvent aider à détecter d’éventuelles failles de données personnelles qui peut exposer les utilisateurs toounauthorized de données personnelles.

#### <a name="how-do-i-use-log-analytics"></a>Comment utiliser Log Analytics ?

Vous pouvez accéder Analytique de journal par le biais du portail OMS hello ou hello portail Azure, à partir de n’importe quel navigateur web. Analytique de journal inclut un récupérer de tooquickly de langage de requête et consolider les données dans le référentiel de hello. Vous pouvez créer et enregistrer des recherches de journaux toodirectly analyser les données dans le portail de hello.

toocreate un espace de travail Analytique de journal Bonjour portail Azure, procédez comme hello suivant :

1. Sélectionnez **Analytique de journal** à partir de la liste hello de services Bonjour Marketplace.

2. Sélectionnez **Create,** spécifier nom hello de votre espace de travail OMS, sélectionnez votre abonnement, le groupe de ressources, l’emplacement et niveau de tarification.

3. Cliquez sur **OK** toodisplay une liste de vos espaces de travail.

4. Sélectionnez un espace de travail toosee ses détails.

    ![](media/protection-personal-data-azure-reporting-tools/image004.png)

Visitez hello [documentation d’Analytique de journal](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) toolearn plus d’informations sur les service hello.

Visitez hello [prise en main avec un espace de travail Analytique des journaux](https://docs.microsoft.com/azure/log-analytics/log-analytics-get-started) toocreate didacticiel un espace de travail d’évaluation et les principes fondamentaux de la façon dont toouse hello service hello.

Visitez hello suivant des pages web pour plus d’informations sur comment tooconnect toouse Analytique de journal avec hello consigne décrites ci-dessus :

[Sources de données de journal d’événements Windows dans Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)

[Journaux IIS dans Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs)

[Sources de données Syslog dans Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-syslog)

### <a name="azure-monitorazure-activity-log"></a>Azure Monitor/Journal d’activité Azure 

[Azure Monitor](https://azure.microsoft.com/services/monitor/) fournit des métriques de niveau de base d’infrastructure et des journaux pour la plupart des services Microsoft Azure.
Analyse peut vous aider à toogain des informations détaillées sur vos applications Azure. Moniteur Azure s’appuie sur l’extension des diagnostics Azure hello (Windows ou Linux) pour collecter la plupart des métriques de niveau application et les journaux. [Hello journal des activités Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) est une des ressources hello vous pouvez afficher avec l’Analyseur de Azure. Il effectue le suivi de chaque appel d’API et fournit une multitude d’informations sur les activités qui se produisent dans [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview).
Vous pouvez rechercher hello journal d’activité (précédemment appelé opérationnelle ou les journaux d’Audit) pour plus d’informations sur votre ressource, comme indiqué par hello infrastructure Azure. 

Bien que la majorité des informations de hello enregistrées Bonjour activité journal relative tooperformance et intégrité des services, il existe également des informations connexe tooprotection de données. À l’aide de hello journal d’activité, vous pouvez déterminer hello », qui et à quel moment » pour toutes les opérations (PUT, POST, DELETE) effectuées sur des ressources dans votre abonnement Azure hello d’écriture.

Par exemple, il fournit un enregistrement lorsqu’un administrateur supprime un groupe de sécurité réseau, ce qui peut impacter protection hello des données personnelles. Les entrées du journal d’activité sont stockées dans Azure Monitor pendant 90 jours.

#### <a name="how-do-i-use-hello-data-collected-by-azure-monitor"></a>Comment utiliser les données hello collectées par le moniteur de Windows Azure ?

Il existe un nombre de données hello toouse dans le journal d’activité hello et d’autres ressources de moniteur de Windows Azure.

- Vous pouvez diffuser des emplacements de tooother données hello dans la ligne réelle.

- Vous pouvez stocker les données de hello plus longtemps que les valeurs par défaut de hello, en utilisant un [compte de stockage Azure](https://docs.microsoft.com/azure/storage/common/storage-introduction) et en définissant une stratégie de rétention.

- Vous pouvez les données visual hello dans les graphiques et les graphiques, à l’aide de hello [portail Azure](https://azure.microsoft.com/features/azure-portal/), [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), [Microsoft PowerBI](https://powerbi.microsoft.com/), ou les outils de visualisation de tiers.

- Vous pouvez interroger les données hello à l’aide de hello API REST de moniteur Azure, les commandes CLI, [PowerShell](https://docs.microsoft.com/powershell/) applets de commande, ou de bienvenue du SDK .NET.

tooget a démarré avec l’Analyseur de Azure, sélectionnez **plus Services** Bonjour portail Azure.

1. Faites défiler la liste trop**moniteur** Bonjour **analyse et la gestion** section.

    ![](media/protection-personal-data-azure-reporting-tools/image005.png)

2.  Moniteur s’ouvre dans hello **le journal d’activité** vue.

    ![](media/protection-personal-data-azure-reporting-tools/image007.png)

Vous pouvez créer et enregistrer des requêtes pour les filtres communs, puis pin hello plus importante requêtes tooa portail du tableau de bord pour que vous sachiez toujours si les événements qui répondent à vos critères se sont produites.

1. Vous pouvez filtrer la vue hello par groupe de ressources, timespan et catégorie d’événement.

    ![](media/protection-personal-data-azure-reporting-tools/image008.png)

2. Vous pouvez épingler puis des requêtes tooa portail du tableau de bord en cliquant sur hello **code confidentiel** bouton. Cela vous permet de créer une seule source d’informations pour les données opérationnelles sur vos services. nom de la requête Hello et le nombre de résultats seront affichera sur le tableau de bord hello.

Vous pouvez également utiliser des métriques de tooview moniteur hello pour toutes les ressources Azure, configurer des alertes et les paramètres de diagnostic et recherche hello journal. Pour plus d’informations sur comment toouse hello moniteur de Windows Azure et le journal d’activité, consultez [prise en main Azure analyse](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-get-started).

### <a name="azure-diagnostics"></a>Azure Diagnostics 

les fonctionnalités de diagnostic Hello dans Azure Active la collecte des données de plusieurs sources. journaux des événements Windows Hello, y compris le journal de sécurité hello, peuvent être particulièrement utiles dans le suivi et documenter la protection des données personnelles. journal de sécurité Hello effectue le suivi des événements de réussite et d’échec d’ouverture de session, ainsi que les modifications apportées aux autorisations, la détection des modèles indiquant de certains types d’attaques, les modifications apportées aux stratégies de sécurité, les modifications de l’appartenance au groupe de sécurité et bien plus encore.

Par exemple, 4695 d’ID d’événement avertit vous toohello a tenté d’unprotection des données protégées pouvant être auditées. Cela s’applique toohello API DPAPI (Data Protection), ce qui vous permet de tooprotect les données telles que les clés privées, les informations d’identification stockées et les autres informations confidentielles.

#### <a name="how-do-i-enable-hello-diagnostics-extension-for-windows-vms"></a>Comment activer les extension de diagnostics hello pour les machines virtuelles Windows ?

Vous pouvez utiliser extension des diagnostics PowerShell tooenable hello pour une machine virtuelle Windows, ainsi que les données de journal toocollect. procédure de Hello pour cela varie sur le modèle de déploiement que vous utilisez (Gestionnaire de ressources ou classique). extension des diagnostics hello tooenable sur un ordinateur virtuel existant qui a été créé via le modèle de déploiement du Gestionnaire de ressources hello, vous pouvez utiliser hello [applet de commande Set-AzureRMVMDiagnosticsExtension PowerShell](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension?view=azurermps-4.3.1).

   ![](media/protection-personal-data-azure-reporting-tools/image009.png)

*\$diagnosticsconfig_path* est hello chemin d’accès toohello fichier qui contient la configuration des diagnostics hello dans XML. Pour plus d’instructions sur l’activation des Diagnostics Windows Azure sur une machine virtuelle, consultez [utiliser PowerShell tooenable Diagnostics Azure dans une machine virtuelle exécutant Windows.](https://docs.microsoft.com/azure/virtual-machines/windows/ps-extensions-diagnostics)

Hello extension Azure diagnostics peut transférer le compte de stockage Azure hello collectée données tooan ou l’envoyer tooservices tels que Application Insights. Vous pouvez ensuite utiliser les données de salutation pour l’audit.

#### <a name="how-do-i-store-and-view-diagnostic-data"></a>Comment stocker et afficher les données de diagnostics ?

Il est important tooremember que des données de diagnostic ne sont pas définitivement stockées, sauf si vous transférez toohello Microsoft Azure emulator ou tooAzure de stockage. toostore et affichage des données de diagnostic dans le stockage Azure, procédez comme suit :

1. Spécifiez un compte de stockage dans le fichier ServiceConfiguration.cscfg de hello. Diagnostics Azure peut utiliser service d’objets Blob hello ou service de Table hello, en fonction de type hello de données. Les journaux des événements Windows sont stockés sous forme de tableau.

2. Transfert de données de salutation. Vous pouvez demander des données de diagnostic hello tootransfer via le fichier de configuration hello. Pour le SDK 2.4 et précédente, vous pouvez également rendre demande de hello par programme.

3. Afficher les données de hello, à l’aide de [Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer), [l’Explorateur de serveurs](https://docs.microsoft.com/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) dans Visual Studio, ou [Azure Diagnostics Manager](https://www.cerebrata.com/products/azure-diagnostics-manager) dans Azure Management Studio.

Pour plus d’informations sur la façon de tooperform de ces étapes, consultez [stocker et afficher des données de diagnostic dans le stockage Azure.](https://docs.microsoft.com/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)

### <a name="azure-storage-analytics"></a>Azure Storage Analytics 

Stockage Analytique enregistre des informations détaillées sur le service de stockage tooa demandes réussies et ayant échoué. Ces informations peuvent être utilisés toomonitor les requêtes individuelles, qui peuvent vous aider à accéder aux données de toopersonal stockées dans le service hello de documentation. Toutefois, la journalisation Storage Analytics n’est pas activée par défaut pour votre compte de stockage. Vous pouvez l’activer dans hello portail Azure.

#### <a name="how-do-i-configure-monitoring-for-a-storage-account"></a>Comment configurer la surveillance d’un compte de stockage ?

tooconfigure d’analyse pour un compte de stockage, procédez comme hello suivant :

1. Sélectionnez **comptes de stockage** Bonjour portail Azure, puis sélectionnez hello nom du compte hello toomonitor.

    ![](media/protection-personal-data-azure-reporting-tools/image011.png)

2. Bonjour **analyse** section, sélectionnez **Diagnostics.**

3.  Sélectionnez hello **type** de données de métriques souhaité toomonitor pour chaque service (fichier Blob, Table). journaux de diagnostics Azure Storage toosave tooinstruct pour la lecture, écriture et suppression des demandes pour hello services blob, table et file d’attente, sélectionnent **journaux d’objets Blob, Table des journaux** et **file d’attente de journaux.**

    ![](media/protection-personal-data-azure-reporting-tools/image013.png)

4. Curseur de hello bas hello, définissez hello **rétention** stratégie en jours (valeur de 1 à 365). Sept jours est par défaut de hello.

5. Sélectionnez **enregistrer** paramètres de configuration tooapply hello.

Entrées de journal de la journalisation de stockage contiennent hello suivant des informations sur les requêtes individuelles :

- Informations de minutage comme l’heure de début, la latence de bout en bout et la latence du serveur.

- Détails de l’opération de stockage hello comme type d’opération hello, clé hello du client de hello stockage objet hello est l’accès à, la réussite ou l’échec et le code d’état HTTP hello retourné toohello client.

- Détails de l’authentification, tels que de type hello du client hello d’authentification utilisé.

- Informations d’accès concurrentiel tels que la valeur de l’ETag hello et le dernier horodateur modifié.

- tailles de Hello hello messages de demande et réponse.

Pour plus d’instructions sur la façon de voir de tooenable Analytique Storage logging, [surveiller un compte de stockage Bonjour portail Azure.](https://docs.microsoft.com/azure/storage/common/storage-monitor-storage-account)

### <a name="azure-security-center"></a>Azure Security Center 

[Centre de sécurité Azure](https://azure.microsoft.com/services/security-center/) moniteurs hello l’état de sécurité de vos ressources Azure dans l’ordre tooprevent et détecter les menaces et fournit des recommandations pour répondre. Il fournit le document de toohelp plusieurs façons vos mesures de sécurité qui hello de protection des données personnelles.

La surveillance de l’intégrité de la sécurité vous permet d’assurer la conformité à vos stratégies de sécurité. Surveillance de la sécurité est une stratégie proactive des audits de vos systèmes de tooidentify de ressources qui ne répondent pas aux normes de l’organisation ou les meilleures pratiques. Vous pouvez surveiller l’état de sécurité hello Hello suivant des ressources :

- Calcul (machines virtuelles et services cloud)

- Mise en réseau (réseaux virtuels)

- Stockage et données (audit de serveur et base de données et détection des menaces, TDE, chiffrement de stockage)

- Applications (problèmes potentiels de sécurité)

Problèmes de sécurité dans un de ces catégories susceptible de constituer une confidentialité toohello de menace de données personnelles.

#### <a name="how-do-i-view-hello-security-state-of-my-azure-resources"></a>Comment afficher l’état de la sécurité de mes ressources Azure hello ?

Centre de sécurité analyse régulièrement l’état de la sécurité de vos ressources Azure hello. Vous pouvez afficher toutes les éventuelles failles de sécurité, il identifie Bonjour **prévention** section du tableau de bord hello.

   ![](media/protection-personal-data-azure-reporting-tools/image014.png)

1. Bonjour **prévention** section, sélectionnez hello **de calcul** vignette. Vous voyez ici une **vue d’ensemble,** avec hello **virtuels** affichage de la liste de tous les ordinateurs virtuels et de leur état de sécurité et hello **services de cloud computing** la liste des rôles web et de travail analysé par le centre de sécurité.

2. Sur hello **vue d’ensemble** , onglet de la deuxième une recommandation tooview plus d’informations.

3. Sur hello **virtuels** onglet, sélectionnez une machine virtuelle tooview les détails supplémentaires.

Lors de la collecte de données est activée dans le centre de sécurité Azure, hello Microsoft Monitoring Agent est automatiquement configuré sur toutes les existantes et nouvelles tout pris en charge les ordinateurs virtuels qui sont déployés. Les données collectées à partir de cet agent sont stockées dans un espace de travail [Log Analytics](https://azure.microsoft.com/services/log-analytics/) existant associé à votre abonnement ou dans un nouvel espace de travail.

Des [rapports d’informations sur les menaces](https://docs.microsoft.com/azure/security-center/security-center-threat-report) sont fournis par Security Center. Ils fournissent des informations utiles toohelp de déterminer la personne malveillante hello identité, objectifs, outils de campagnes et des stratégies, des attaques actuelles et historiques et les procédures utilisées. Des informations sur l’atténuation des risques et les corrections à apporter sont également incluses.

Hello principal objectif de ces rapports de menace est toohelp vous toorespond efficacement toohello immédiate des menaces et aide les mesures nécessaires par la suite problème de hello toomitigate. informations Hello dans les rapports de hello peuvent également être utiles lorsque vous documentez votre réponse aux incidents de rapports et à des fins d’audit.

Rapports de Hello Threat Intelligence sont présentés. Format PDF, accessibilité via un lien Bonjour **rapports** champ hello **suspectes processus exécuté** panneau pour chaque alerte de sécurité dans le centre de sécurité Azure.

Pour plus d’informations sur comment tooview et utilisez hello Threat Intelligence rapport, consultez [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)

## <a name="next-steps"></a>Étapes suivantes :

[Prise en main de hello Azure Active Directory API de création de rapports](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal)

[Présentation de Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

[Vue d’ensemble de l’analyse dans Microsoft Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

[Introduction toohello journal des activités Azure (vidéo)](https://azure.microsoft.com/resources/videos/intro-activity-log/)
