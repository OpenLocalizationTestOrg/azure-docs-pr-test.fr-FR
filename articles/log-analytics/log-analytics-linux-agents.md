---
redirect_url: /azure/log-analytics/log-analytics-agent-linux
redirect_document_id: True
ROBOTS: NOINDEX
ms.openlocfilehash: 8b526144cd565f6750368e12970f008e66cc2023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-linux-computers-toolog-analytics"></a>Se connecter à votre tooLog d’ordinateurs Linux Analytique
Avec Log Analytics, vous pouvez collecter et exploiter les données générées par des ordinateurs Linux. Ajout des données collectées à partir de Linux tooOMS vous permet de toomanage les systèmes Linux et les solutions de conteneur comme Docker, quel que soit l’endroit où se trouvent vos ordinateurs, virtuellement n’importe où. Sources de données peuvent résider dans votre centre de données local en tant que serveurs physiques, des ordinateurs virtuels dans un service hébergé dans le cloud, comme Amazon Web Services (AWS) ou Microsoft Azure, ou même hello ordinateur portable sur votre bureau. De plus, OMS collecte les données des ordinateurs Windows de la même façon, prenant en charge un véritable environnement informatique hybride.

Vous pouvez afficher et gérer les données de toutes ces sources avec Log Analytics dans OMS, via un portail unique. Ceci réduit le besoin de hello toomonitor à l’aide de différents systèmes et les rend facile tooconsume, et vous pouvez exporter les données de votre choix toowhatever business analytique solution ou du système que vous avez déjà.

Cet article est un guide de démarrage rapide qui vous permet de collecter et de gérer les données de vos ordinateurs Linux à l’aide de hello Agent OMS pour Linux. Pour obtenir des détails plus techniques, tels que la configuration du serveur proxy, des informations sur les mesures CollectD, et des sources de données JSON personnalisées, consultez la [présentation de l’Agent OMS pour Linux](https://github.com/Microsoft/OMS-Agent-for-Linux) (en anglais) et la [documentation complète de l’Agent OMS pour Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md) (en anglais) sur GitHub.

Actuellement, vous pouvez collecter hello suivant les types de données à partir d’ordinateurs Linux :

* Mesures de performances
* Événements Syslog
* Alertes de Nagios et Zabbix
* Journaux, inventaire et mesures de performances du conteneur Docker

## <a name="supported-linux-versions"></a>Versions de Linux prises en charge
Les versions x86 et x64 sont officiellement prises en charge sur diverses distributions de Linux. Toutefois, hello Agent OMS pour Linux peut également s’exécuter sur les autres distributions non répertoriées.

* Amazon Linux 2012.09 à 2015.09
* CentOS Linux 5, 6 et 7
* Oracle Linux 5, 6 et 7
* Red Hat Enterprise Linux Server 5, 6 et 7
* Debian GNU/Linux 6, 7 et 8
* Ubuntu 12.04 LTS, 14.04 LTS, 15.04, 15.10
* SUSE Linux Enterprise Server 11 et 12

## <a name="oms-agent-for-linux"></a>Agent OMS pour Linux
Hello Operations Management Suite Agent pour Linux comprend plusieurs packages. fichier de la version Hello contient hello suivant des packages, disponibles en cours d’exécution offre groupée du noyau hello avec `--extract`.

| **Package** | **Version** | **Description** |
| --- | --- | --- |
| omsagent |1.1.0 |Hello Operations Management Suite Agent pour Linux |
| omsconfig |1.1.1 |Agent de configuration pour hello Agent OMS |
| omi |1.0.8.3 |Open Management Infrastructure (OMI) - Serveur CIM léger |
| scx |1.6.2 |Fournisseurs CIM OMI pour les mesures de performances des systèmes d’exploitation |
| apache-cimprov |1.0.0 |Fournisseur de surveillance des performances d’Apache HTTP Server pour OMI. Installé uniquement si Apache HTTP Server est détecté. |
| mysql-cimprov |1.0.0 |Fournisseur de surveillance des performances de MySQL Server pour OMI. Installé uniquement si MySQL/MariaDB Server est détecté. |
| docker-cimprov |0.1.0 |Fournisseur de Docker pour OMI. Installé uniquement si Docker est détecté. |

### <a name="additional-installation-artifacts"></a>Artefacts d’installation supplémentaires
Après avoir installé l’agent OMS de hello pour les packages Linux, hello les modifications de système de configuration supplémentaires suivantes sont appliquées. Ces artefacts sont supprimés lors de la désinstallation du package omsagent hello.

* Un utilisateur sans privilège nommé `omsagent` est créé. Il s’agit hello compte hello omsagent démon exécute en tant que
* Un fichier « include » de programmes sudo est créé à /etc/sudoers.d/omsagent ce qui autorise omsagent toorestart hello syslog et omsagent démons. Si les directives « include » de sudo ne sont pas pris en charge dans la version installée de hello de sudo, ces entrées sont écrites trop/etc/programmes sudo.
* configuration de syslog Hello est modifié tooforward un sous-ensemble de l’agent de toohello d’événements. Pour plus d’informations, consultez hello **collecte des données de configuration de** section ci-dessous

### <a name="linux-data-collection-details"></a>Détails sur la collecte de données Linux
Hello tableau suivant présente les méthodes de collecte de données et d’autres détails sur la façon dont les données sont collectées.

| source | Agent direct | Agent SCOM | Stockage Azure | SCOM requis ? | Données de l’agent SCOM envoyées via un groupe d’administration | Fréquence de collecte |
| --- | --- | --- | --- | --- | --- | --- |
| Zabbix |![Oui](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |1 minute |
| Nagios |![Oui](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |À l’arrivée |
| syslog |![Oui](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |Depuis Azure Storage : 10 minutes ; depuis l’agent : à l’arrivée |
| Compteurs de performances Linux |![Oui](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |Comme prévu, minimum de 10 secondes |
| Suivi des modifications |![Oui](./media/log-analytics-linux-agents/oms-bullet-green.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |![Non](./media/log-analytics-linux-agents/oms-bullet-red.png) |Toutes les heures |

### <a name="package-requirements"></a>Packages requis
| **Package requis** | **Description** | **Version minimum** |
| --- | --- | --- |
| Glibc |Bibliothèque C de GNU |2.5-12 |
| Openssl |Bibliothèques OpenSSL |0.9.8e ou 1.0 |
| Curl |Client web cURL |7.15.5 |
| Python-ctypes |Bibliothèques de fonctions |n/a |
| PAM |Pluggable Authentication Modules |n/a |

> [!NOTE]
> Rsyslog ou syslog-ng est des messages syslog toocollect requis. démon syslog par défaut de Hello version 5 de Red Hat Enterprise Linux, CentOS et Oracle Linux (sysklog) n’est pas pris en charge pour la collecte d’événements syslog. toocollect les données syslog de cette version de ces distributions, hello rsyslog démon doit être installé et configuré tooreplace sysklog.
>
>

## <a name="quick-install"></a>Installation rapide
Exécutez hello suivant de commandes toodownload hello omsagent, valider la somme de contrôle hello, puis installer et l’agent de hello intégré. Ces commandes sont de type 64 bits. Hello ID de l’espace de travail et la clé primaire sont trouvent dans le portail OMS de hello sous **paramètres** sur hello **Sources connectées** onglet.

![détails sur l’espace de travail](./media/log-analytics-linux-agents/oms-direct-agent-primary-key.png)

```
wget https://raw.githubusercontent.com/Microsoft/OMS-Agent-for-Linux/master/installer/scripts/onboard_agent.sh && sh onboard_agent.sh -w <YOUR OMS WORKSPACE ID> -s <YOUR OMS WORKSPACE PRIMARY KEY>
```

Il existe une multitude d’autres tooinstall méthodes hello agent et le mettre à niveau. Vous pouvez en savoir plus sur ces méthodes dans [hello de tooinstall étapes Agent OMS pour Linux](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#steps-to-install-the-oms-agent-for-linux).

Vous pouvez également afficher hello [procédure pas à pas vidéo Azure](https://www.youtube.com/watch?v=mF1wtHPEzT0).

## <a name="choose-your-linux-data-collection-method"></a>Choisir la mode de collecte des données Linux
Façon dont vous choisissez hello types de données que vous le feriez comme toocollect varie selon que vous souhaitez toouse du portail OMS hello ou si vous souhaitez modifier différents fichiers de configuration directement sur vos clients Linux. Si vous choisissez de portail de hello toouse, configuration de hello est envoyée automatiquement tooall vos clients Linux. Si vous avez besoin de configurations différentes pour différents clients Linux, vous avez besoin de fichiers du client tooedit individuellement ou utiliser une solution alternative comme PowerShell DSC, Chef ou Puppet.

Vous pouvez spécifier les événements syslog hello et des compteurs de performance que vous souhaitez toocollect à l’aide de fichiers de configuration sur les ordinateurs Linux hello. *Si vous avez choisi de collecte de données tooconfigure en modifiant les fichiers de configuration de l’agent, vous devez désactiver la configuration centralisée de hello.*  Les instructions sont fournies ci-dessous tooconfigure collecte des données dans l’agent hello les fichiers de configuration, ainsi que toodisable de configuration centrale pour tous les Agents OMS pour Linux ou des ordinateurs individuels.

### <a name="disable-oms-management-for-an-individual-linux-computer"></a>Désactiver la gestion OMS sur un ordinateur Linux
Collecte centralisée des données de configuration est désactivée pour un ordinateur Linux avec hello du script OMS_MetaConfigHelper.py. Ce script est très utile si quelques ordinateurs requièrent une configuration spéciale.

toodisable configuration centralisée :

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```

toore-activer une configuration centralisée :

```
sudo /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py –enable
```

## <a name="linux-performance-counters"></a>Compteurs de performances Linux
Compteurs de performances Linux sont des compteurs de performances tooWindows similaires, les deux fonctionnent de la même façon. Vous pouvez utiliser hello suivant les procédures tooadd et les configurer. Après que les avoir ajoutés tooOMS, données sont collectées pour ces toutes les 30 secondes.

### <a name="tooadd-a-linux-performance-counter-in-oms"></a>tooadd un compteur de performances Linux dans OMS
1. tooconfigure Agents OMS pour Linux à l’aide du portail OMS hello, vous pouvez ajouter des compteurs de performances Linux dans la page Paramètres de hello, cliquez sur **données**.  
2. Sur hello **paramètres** page sous **données** , cliquez sur **compteurs de performances Linux** , puis sélectionnez ou tapez hello nom du compteur de hello souhaité tooadd.  
    ![données](./media/log-analytics-linux-agents/oms-settings-data01.png)
3. Si vous ne connaissez le nom complet de hello du compteur de hello, vous pouvez commencer en tapant un nom partiel, et une liste des compteurs disponibles s’affiche. Lorsque vous avez trouvé le compteur de hello vous souhaitez tooadd, cliquez sur nom hello dans la liste de hello puis hello plus hello de tooadd icône compteur.
4. Après avoir ajouté le compteur de hello, il apparaît dans la liste hello des compteurs mis en surbrillance avec une barre de couleur.
5. Par défaut, hello **appliquer machines toomy de configuration ci-dessous** option est sélectionnée. Si vous souhaitez toodisable envoi de données de configuration, désactivez la sélection de hello.
6. Lorsque vous avez terminé la modification des compteurs de performance, en bas de hello de page de hello cliquez sur **enregistrer** toofinalize vos modifications. les modifications de configuration Hello que vous avez apportées sont ensuite envoyées tooall hello Agents OMS pour Linux qui sont inscrits auprès d’OMS, généralement dans les 5 minutes.

### <a name="configure-linux-performance-counters-in-oms"></a>Configurer des compteurs de performances Linux dans OMS
Pour les compteurs de performances Windows, vous pouvez choisir une instance spécifique de chaque compteur de performances. Toutefois, pour les compteurs de performances Linux, l’instance de compteur que vous choisissez s’applique ses compteurs enfants tooall compteur parent de hello. Hello tableau suivant montre les instances courantes hello les compteurs de performances Linux et Windows tooboth disponibles.

| **Nom de l’instance** | **Signification** |
| --- | --- |
| \_Total |Nombre total de toutes les instances de hello |
| \* |Toutes les instances |
| (/&#124;/var) |Correspond aux instances nommées : / ou /var |

De même, intervalle d’échantillonnage hello que vous choisissez pour un compteur parent s’applique tooall ses compteurs enfants. En d’autres termes, tous les intervalles d’échantillonnage compteur hello enfant et les instances sont tous liés entre eux.

### <a name="add-and-configure-performance-metrics-with-linux"></a>Ajouter et configurer des mesures de performances avec Linux
Toocollect des métriques de performances sont contrôlées par la configuration hello dans/etc/opt/microsoft/omsagent/&lt;id de l’espace de travail&gt;/conf/omsagent.conf. Consultez [métriques de performances disponibles](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#appendix-available-performance-metrics) pour connaître les classes et les métriques pour hello Agent OMS pour Linux.

Chaque objet ou la catégorie de toocollect des métriques de performances doit être définie dans le fichier de configuration hello en tant qu’un seul `<source>` élément. syntaxe de Hello suit le modèle hello ci-dessous.

```
<source>
  type oms_omi  
  object_name "Processor"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

Hello les paramètres configurables de cet élément sont :

* **Objet\_nom**: nom de l’objet de collection de hello hello.
* **Instance\_regex**: un *expression régulière* définissant l’instances toocollect. valeur de Hello : `.*` spécifie toutes les instances. métriques de processeur toocollect pour hello uniquement \_nombre Total d’instances, vous pouvez spécifier `_Total`. les métriques de processus toocollect pour hello uniquement les instances crond ou sshd uniquement, vous pouvez spécifier : `(crond|sshd)`.
* **Compteur\_nom\_regex**: un *expression régulière* définissant le toocollect compteurs (pour l’objet de hello). Spécifiez de tous les compteurs pour l’objet de hello, toocollect : `.*`. toocollect permutation compteurs d’espace pour l’objet de mémoire hello, vous pouvez spécifier :`.+Swap.+`
* **Intervalle :**: hello fréquence à quels hello les compteurs de l’objet sont collectés.

configuration par défaut de Hello pour les métriques de performances est la suivante :

```
<source>
  type oms_omi
  object_name "Physical Disk"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Logical Disk"
  instance_regex ".*
  counter_name_regex ".*"
  interval 5m
</source>

<source>
  type oms_omi
  object_name "Processor"
  instance_regex ".*
  counter_name_regex ".*"
  interval 30s
</source>

<source>
  type oms_omi
  object_name "Memory"
  instance_regex ".*"
  counter_name_regex ".*"
  interval 30s
</source>

```

### <a name="enable-mysql-performance-counters-using-linux-commands"></a>Activer des compteurs de performances MySQL à l’aide de commandes Linux
Si MySQL Server ou MariaDB Server est détecté sur l’ordinateur de hello lorsque hello du bundle omsagent, un fournisseur pour MySQL Server d’analyse des performances sont automatiquement installé. Ce fournisseur connecte toohello local MySQL/MariaDB server tooexpose les statistiques de performances. Vous avez besoin d’informations d’identification utilisateur MySQL de tooconfigure afin que hello fournisseur d’accéder à hello MySQL Server.

toodefine compte d’un utilisateur par défaut pour le serveur MySQL de hello sur localhost, hello utilisez exemple de commande suivant.

> [!NOTE]
> fichier d’informations d’identification de Hello doit être accessible en lecture hello omsagent compte. Est recommandé d’exécuter la commande mycimprovauth de hello pour omsgent.
>
>

```
sudo su omsagent -c '/opt/microsoft/mysql-cimprov/bin/mycimprovauth default 127.0.0.1 <username> <password>

sudo /opt/omi/bin/service_control restart
```


Vous pouvez également spécifier hello requis des informations d’identification MySQL dans un fichier, en créant un fichier hello : /var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth. Pour plus d’informations sur la gestion des informations d’identification MySQL pour l’analyse via le fichier de hello mysql-auth, consultez [MySQL gérer analyse les informations d’identification dans le fichier d’authentification hello](#manage-mysql-monitoring-credentials-in-the-authentication-file).

Consultez [de base de données des autorisations requises pour les compteurs de performances MySQL](#database-permissions-required-for-mysql-performance-counters) pour plus d’informations sur les autorisations d’objet requises par hello MySQL utilisateur toocollect données de performances MySQL Server.

### <a name="enable-apache-http-server-performance-counters-using-linux-commands"></a>Activer les compteurs de performances d’Apache HTTP Server à l’aide de commandes Linux
Si Apache HTTP Server est détecté sur l’ordinateur de hello lorsque hello du bundle omsagent, un fournisseur pour Apache HTTP Server d’analyse des performances sont automatiquement installé. Ce fournisseur repose sur un « module » Apache qui doit être chargé dans Apache HTTP Server de hello ordre tooaccess les données de performance.

Vous pouvez charger le module de hello avec hello de commande suivante :

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -c
```

toounload hello module d’analyse Apache, exécutez hello de commande suivante :

```
sudo /opt/microsoft/apache-cimprov/bin/apache_config.sh -u
```
### <a name="tooview-performance-data-with-log-analytics"></a>données de performances tooview avec Analytique de journal
1. Dans le portail Operations Management Suite hello, cliquez sur la vignette de recherche de journal hello.
2. Dans la barre de recherche de hello, tapez `* (Type=Perf)` tooview tous les compteurs de performances.

Comme OMS collecte également les données de compteur de performance Windows, vous devez limiter hello recherche tooLinux propres données. Par conséquent, hello exemple suivant affichera-t-il les performances données tooan spécifique exemple de serveur Linux nommé Chorizo21.

```
Type=Perf Computer=chorizo*
```

![exemple de serveur affiché dans les résultats de la recherche](./media/log-analytics-linux-agents/oms-perfsearch01.png)

Dans les résultats de hello, vous pouvez cliquer sur **métriques** compteurs hello tooview collectées pour les données. Les données en temps réel sont indiquées sous forme graphique pour chaque compteur.

![Mesures](./media/log-analytics-linux-agents/oms-perfmetrics01.png)

## <a name="syslog"></a>syslog
Syslog est un protocole tooWindows similaire des journaux des événements de journalisation des événements, les deux fonctionnent de manière similaire dans OMS.

### <a name="tooadd-a-new-linux-syslog-facility-in-oms"></a>tooadd une nouvelle fonction syslog de Linux dans OMS
1. Sur hello **paramètres** page sous **données** , cliquez sur **Syslog** puis toohello à gauche de l’icône plus hello, tapez hello nom de la fonction syslog de hello que vous souhaitez tooadd.
    ![syslog de Linux](./media/log-analytics-linux-agents/oms-linuxsyslog01.png)
2. Si vous ne connaissez le nom complet de hello de facilité de hello, vous pouvez commencer en tapant un nom partiel, et une liste des fonctions syslog disponibles s’affiche. Lorsque vous trouvez la fonction syslog de hello que vous souhaitez tooadd, cliquez sur nom hello dans la liste de hello puis hello plus hello de tooadd icône fonction syslog.
3. Après avoir ajouté la fonctionnalité de hello, il apparaît dans la liste hello de mise en surbrillance avec une barre de couleur. Ensuite, choisissez hello, niveaux de gravité (catégories d’information sur les fonctions syslog) que vous souhaitez toocollect.
4. Au bas de hello de page de hello cliquez sur **enregistrer** toofinalize vos modifications. les modifications de configuration Hello que vous avez apportées sont ensuite envoyées tooall hello Agents OMS pour Linux qui sont inscrits auprès d’OMS, généralement dans les 5 minutes.

### <a name="configure-linux-syslog-facilities-in-linux"></a>Configurer des fonctionnalités syslog Linux dans Linux
Événements syslog sont envoyés du démon syslog de hello, par exemple rsyslog ou syslog-ng, port local de tooa que l’agent hello écoute. Le port par défaut est 25224. Lorsque l’agent hello est installé, une configuration de syslog par défaut est appliquée. Elle se trouve à l’emplacement suivant :

Rsyslog : /etc/rsyslog.d/rsyslog-oms.conf

Syslog-ng : /etc/syslog-ng/syslog-ng.conf

configuration de syslog Hello par défaut OMS agent télécharge les événements syslog de toutes les fonctions ayant un niveau de gravité d’avertissement ou une version ultérieure.

> [!NOTE]
> Si vous modifiez la configuration syslog hello, vous devez redémarrer le démon syslog hello hello modifications tootake effet.
>
>

Hello configuration syslog par défaut pour hello Agent OMS pour Linux pour OMS est la suivante :

#### <a name="rsyslog"></a>Rsyslog
```
kern.warning       @127.0.0.1:25224
user.warning       @127.0.0.1:25224
daemon.warning     @127.0.0.1:25224
auth.warning       @127.0.0.1:25224
syslog.warning     @127.0.0.1:25224
uucp.warning       @127.0.0.1:25224
authpriv.warning   @127.0.0.1:25224
ftp.warning        @127.0.0.1:25224
cron.warning       @127.0.0.1:25224
local0.warning     @127.0.0.1:25224
local1.warning     @127.0.0.1:25224
local2.warning     @127.0.0.1:25224
local3.warning     @127.0.0.1:25224
local4.warning     @127.0.0.1:25224
local5.warning     @127.0.0.1:25224
local6.warning     @127.0.0.1:25224
local7.warning     @127.0.0.1:25224
```

#### <a name="syslog-ng"></a>Syslog-ng
```
#OMS_facility = all
filter f_warning_oms { level(warning); };
destination warning_oms { tcp("127.0.0.1" port(25224)); };
log { source(src); filter(f_warning_oms); destination(warning_oms); };
```

### <a name="tooview-all-syslog-events-with-log-analytics"></a>tooview tous les événements Syslog avec Analytique de journal
1. Dans le portail Operations Management Suite hello, cliquez sur hello **recherche de journal** vignette.
2. Bonjour **gestion du journal** de regroupement, sélectionnez une recherche syslog prédéfinie et puis sélectionnez un toorun il.

Cet exemple montre tous les événements Syslog.

![Événements syslog affichés dans Recherche de journal](./media/log-analytics-linux-agents/oms-linux-syslog.png)

Maintenant, vous pouvez examiner les résultats de la recherche plus en détail.

## <a name="linux-alerts"></a>Alertes Linux
Si vous utilisez Nagios ou Zabbix toomanage que vos ordinateurs Linux, puis OMS peut recevoir des alertes de hello générées à partir de ces outils. Toutefois, il n’existe actuellement aucune méthode tooconfigure données d’alerte entrantes à l’aide du portail OMS hello. Au lieu de cela, vous devez tooedit une tooOMS alertes config fichier toostart envoi.

### <a name="collect-alerts-from-nagios"></a>Collecter les alertes de Nagios
toocollect les alertes d’un serveur Nagios, vous devez hello toomake suit les modifications de configuration.

1. Utilisateur de subventions hello **omsagent** fichier de journal accès en lecture toohello Nagios (c'est-à-dire /var/log/nagios/nagios.log). En supposant que le fichier de hello nagios.log est détenu par groupe de hello **nagios** , vous pouvez ajouter hello utilisateur **omsagent** toohello **nagios** groupe.

    ```
    sudo usermod –a -G nagios omsagent
    ```
2. Modifier le fichier de configuration omsagent.conf hello (/ etc/opt/microsoft/omsagent/&lt;id de l’espace de travail&gt;/conf/omsagent.conf). Vérifiez que hello suivant entrées est présents et pas commentées :

    ```
    <source>
    type tail
    #Update path toopoint tooyour nagios.log
    path /var/log/nagios/nagios.log
    format none
    tag oms.nagios
    </source>

    <filter oms.nagios>
    type filter_nagios_log
    </filter>
    ```
3. Redémarrez le démon omsagent de hello :

    ```
    sudo /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="collect-alerts-from-zabbix"></a>Collecter les alertes de Zabbix
toocollect des alertes à partir d’un serveur Zabbix, à suivre est similaire étapes toothose de nagios décrite ci-dessus, mais vous devez toospecify un utilisateur et mot de passe dans *clair*. Cette solution n’est pas idéale, mais elle devrait changer rapidement. tooaddress ce problème, nous vous recommandons de créer un utilisateur de hello et de lui accorder toomonitor autorisation uniquement.

Une section de l’exemple de fichier de configuration omsagent.conf hello (/ etc/opt/microsoft/omsagent/&lt;id de l’espace de travail&gt;/conf/omsagent.conf) pour Zabbix suivant de hello :

```
<source>
  type zabbix_alerts
  run_interval 1m
  tag oms.zabbix
  zabbix_url http://localhost/zabbix/api_jsonrpc.php
  zabbix_username Admin
  zabbix_password zabbix
</source>

```

### <a name="view-alerts-in-log-analytics-search"></a>Afficher les alertes dans la recherche Log Analytics
Une fois que vous avez configuré votre tooOMS d’alertes Linux ordinateurs toosend, vous pouvez utiliser quelques du journal des simples requêtes tooview hello les alertes de recherche. Hello exemple de requête de recherche ci-dessous retourne toutes les alertes hello enregistrée qui ont été générées. Par exemple, si un problème quelconque se produit dans votre infrastructure informatique, puis les résultats pour hello exemple de requête peut-être indiquer où le problème de hello suivant. Et, vous pouvez explorer facilement dans les alertes de toohello par toohelp du système source étroit votre examen. Bonjour avantage est que vous ne sont pas nécessairement des systèmes de gestion toovarious toogo à partir du début de hello : condition que vos alertes sont envoyées tooOMS, vous pouvez commencer de là.

```
Type=Alert
```

#### <a name="tooview-all-nagios-alerts-with-log-analytics"></a>tooview Nagios toutes les alertes avec Analytique de journal
1. Dans le portail Operations Management Suite hello, cliquez sur hello **recherche de journal** vignette.
2. Dans la barre de requête hello, tapez Bonjour suivant la requête de recherche

    ```
    Type=Alert SourceSystem=Nagios
    ```
   ![Alertes Nagios affichées dans Recherche de journal](./media/log-analytics-linux-agents/oms-linux-nagios-alerts.png)

Une fois que vous voyez les résultats de la recherche hello, vous pouvez explorer des détails supplémentaires, comme *AlertState*.

### <a name="tooview-all-zabbix-alerts-with-log-analytics"></a>tooview toutes les alertes Zabbix Analytique de journal
1. Dans le portail Operations Management Suite hello, cliquez sur hello **recherche de journal** vignette.
2. Dans la barre de requête hello, tapez Bonjour suivant la requête de recherche

    ```
    Type=Alert SourceSystem=Zabbix
    ```
   ![Alertes Zabbix affichées dans Recherche de journal](./media/log-analytics-linux-agents/oms-linux-zabbix-alerts.png)

Une fois que vous voyez les résultats de la recherche hello, vous pouvez explorer des détails supplémentaires, comme *AlertName*.

## <a name="compatibility-with-system-center-operations-manager"></a>Compatibilité avec System Center Operations Manager
Hello Agent OMS pour Linux partage des fichiers binaires avec l’agent de System Center Operations Manager hello. Installation hello Agent OMS pour Linux sur un système actuellement géré par Operations Manager les mises à niveau hello packages OMI et SCX sur une version plus récente de hello ordinateur tooa. Hello Agent OMS pour Linux et System Center 2012 R2 sont compatibles. Toutefois, **System Center 2012 SP1 et les versions antérieures ne sont actuellement pas compatibles ni prises en charge avec hello Agent OMS pour Linux.**

> [!NOTE]
> Si hello Agent OMS pour Linux est installé tooa ordinateur qui n’est pas actuellement géré par Operations Manager et que vous décidez d’ordinateur de hello toomanage avec Operations Manager, vous devez modifier la configuration de hello OMI avant de découvrir hello ordinateur. **Cette étape n’est pas nécessaire si l’agent Operations Manager de hello est installé avant hello Agent OMS pour Linux.**
>
>

### <a name="tooenable-hello-oms-agent-for-linux-toocommunicate-with-operations-manager"></a>tooenable hello Agent OMS pour toocommunicate Linux avec Operations Manager
1. Modifier hello fichier /etc/opt/omi/conf/omiserver.conf
2. Vérifiez que hello ligne commençant par **httpsport =** définit le port 1270 hello. Par exemple `httpsport=1270`
3. Redémarrez le serveur OMI de hello :

    ```
    sudo /opt/omi/bin/service_control restart
    ```

## <a name="database-permissions-required-for-mysql-performance-counters"></a>Autorisations de base de données requises par l’utilisateur MySQL pour collecter les données de performances de MySQL Server
toogrant autorisations tooa utilisateur d’analyse MySQL, utilisateur hello doit avoir hello privilège « GRANT option », ainsi que des privilèges hello accordée.

Dans l’ordre pour hello MySQL utilisateur utilisateur de hello de données de performances tooreturn aura besoin d’accès toohello requêtes suivantes :

```
SHOW GLOBAL STATUS;
SHOW GLOBAL VARIABLES:
```

En outre, utilisateur de MySQL toothese requêtes hello requiert toohello accès choisi par défaut tables suivantes :

* information_schema
* mysql

Ces privilèges peuvent être accordés en exécutant hello suivant de commandes grant.

```
GRANT SELECT ON information_schema.* too‘monuser’@’localhost’;
GRANT SELECT ON mysql.* too‘monuser’@’localhost’;
```

## <a name="manage-mysql-monitoring-credentials-in-hello-authentication-file"></a>Gérer l’analyse des informations d’identification dans le fichier d’authentification hello MySQL
Hello sections suivantes vous gérez les informations d’identification MySQL.

### <a name="configure-hello-mysql-omi-provider"></a>Configurer hello fournisseur OMI MySQL
Hello fournisseur OMI MySQL requiert un utilisateur MySQL soit préconfiguré et les bibliothèques clientes MySQL installées dans les informations de performances/intégrité tooquery hello ordre à partir de l’instance de MySQL hello.

### <a name="mysql-omi-authentication-file"></a>Fichier d’authentification OMI de MySQL
Le fournisseur OMI MySQL utilise un toodetermine de fichier d’authentification quelle instance de MySQL hello adresse de liaison et le port d’écoute et les informations d’identification toouse toogather métriques. Au cours de hello d’installation OMI MySQL fournisseur recherchera les fichiers de configuration MySQL my.cnf (emplacements par défaut) adresse de liaison et un port et partiellement hello de jeu de fichier d’authentification OMI MySQL.

toocomplete d’analyse d’une instance de serveur MySQL, pour ajouter un fichier d’authentification OMI MySQL prégénéré dans le répertoire approprié de hello.

### <a name="authentication-file-format"></a>Format du fichier d’authentification
Hello fichier d’authentification OMI MySQL est un fichier texte qui contient des informations sur :

* Port
* Adresse de liaison
* Nom d’utilisateur MySQL
* Mot de passe encodé en base 64

Hello fichier d’authentification OMI MySQL accorde uniquement des droits en lecture/écriture toohello Linux utilisateur qui l’a généré.

```
[Port]=[Bind-Address], [username], [Base64 encoded Password]
(Port)=(Bind-Address), (username), (Base64 encoded Password)
(Port)=(Bind-Address), (username), (Base64 encoded Password)
AutoUpdate=[true|false]
```

Un fichier d’authentification OMI MySQL par défaut contient une instance par défaut et un numéro de port, selon les informations disponibles et analysé à partir de hello fichier de configuration MySQL trouvé.

instance par défaut de Hello un toomake signifie que la gestion de plusieurs instances MySQL sur un même hôte Linux plus facile et est représentée par l’instance de hello associée au port 0. Toutes les instances ajoutées héritent des propriétés définies à partir de l’instance par défaut de hello. Par exemple, si l’instance MySQL à l’écoute sur le port « 3308 » est ajoutée, l’instance par défaut de hello adresse de liaison, nom d’utilisateur et mot de passe codé en Base64 seront être tootry utilisé d’analyser hello instance à l’écoute du port 3308. Si instance hello du port 3308 est lié tooanother adresse et utilise hello le même nom d’utilisateur MySQL et paire mot de passe hello uniquement respecification Hello adresse de liaison est nécessaire et hello autres propriétés sont héritées.

Vous trouverez des exemples de fichier d’authentification hello suivant de hello.

Instance par défaut et instance avec port 3308 :

```
0=127.0.0.1, myuser, cnBwdA==3308=, ,AutoUpdate=true
```

Instance par défaut et instance avec port 3308 + mot de passe différent encodé en base 64 :

```
0=127.0.0.1, myuser, cnBwdA==3308=127.0.1.1, , AutoUpdate=true
```


| **Propriété** | **Description** |
| --- | --- |
| Port |Le port représente hello de port actuel hello MySQL instance écoute.  le port de Hello 0 implique que les propriétés hello suivantes sont utilisées pour l’instance par défaut. |
| Adresse de liaison |Adresse de liaison de Hello est hello actuel MySQL adresse de liaison |
| username |Ce nom d’utilisateur hello d’utilisateur MySQL de hello vous souhaitez instance toouse toomonitor hello MySQL server. |
| Mot de passe encodé en base 64 |Il s’agit d’un mot de passe hello de hello utilisateur d’analyse MySQL codé en Base64. |
| AutoUpdate |Quand hello fournisseur OMI MySQL est mis à niveau le fournisseur de hello pour les modifications dans le fichier my.cnf hello et remplacer le fichier d’authentification OMI MySQL hello. Définissez cet indicateur tootrue ou false en fonction de mises à jour requises toohello OMI MySQL fichier d’authentification. |

#### <a name="authentication-file-location"></a>Emplacement du fichier d’authentification
Hello fichier d’authentification OMI MySQL doit être situé dans hello l’emplacement suivant et nommé « mysql-auth » :

/var/opt/microsoft/mysql-cimprov/auth/omsagent/mysql-auth

fichier de Hello (et le répertoire auth/omsagent) doivent être possédés par l’utilisateur omsagent de hello.

## <a name="agent-logs"></a>Journaux de l’agent
journaux Hello pour hello Agent OMS pour Linux est à :

/var/opt/microsoft/omsagent/&lt;workspace id&gt;/log/

journaux Hello pour hello situé de l’Agent OMS pour Linux pour les programme omsconfig (configuration de l’agent) :

/var/opt/microsoft/omsconfig/log/

Les journaux des composants OMI et SCX hello (qui fournissent les données de métriques de performances) se trouve à :

/var/opt/omi/log/ et /var/opt/microsoft/scx/log

## <a name="troubleshooting-hello-oms-agent-for-linux"></a>Résolution des problèmes de hello Agent OMS pour Linux
Utilisez hello suivant informations toodiagnose et résoudre les problèmes courants.

Si aucun des hello informations de dépannage de cette section vous aide à vous, vous pouvez également utiliser hello suivant ressources toohelp résoudre votre problème.

* Les clients bénéficiant du Support Premier peuvent soumettre un cas de support via le site [Premier](https://premier.microsoft.com/)
* Clients avec les contrats de support Azure peuvent se connecter les cas de prise en charge hello [portail Azure](https://manage.windowsazure.com/?getsupport=true)
* Déposer un [problème GitHub](https://github.com/Microsoft/OMS-Agent-for-Linux/issues)
* Forum de commentaires pour les idées et toocreate un rapport de bogue [http://aka.ms/opinsightsfeedback](http://aka.ms/opinsightsfeedback)

### <a name="important-log-locations"></a>Emplacement de journaux importants
| Fichier | Chemin |
| --- | --- |
| Fichier journal de l’Agent OMS pour Linux |`/var/opt/microsoft/omsagent/<workspace id>/log/omsagent.log ` |
| Fichier journal de configuration de l’Agent OMS |`/var/opt/microsoft/omsconfig/omsconfig.log` |

### <a name="important-configuration-files"></a>Fichiers de configuration importants
| Catégorie | Emplacement du fichier |
| --- | --- |
| syslog |`/etc/syslog-ng/syslog-ng.conf` ou `/etc/rsyslog.conf` ou `/etc/rsyslog.d/95-omsagent.conf` |
| Performances, Nagios, Zabbix, sortie OMS et agent général |`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` |
| Configurations supplémentaires |`/etc/opt/microsoft/omsagent/<workspace id>/omsagent.d/*.conf` |

> [!NOTE]
> Les fichiers de changement de configuration pour les compteurs de performances et Syslog sont remplacés si la Configuration du portail OMS est activée. Vous pouvez désactiver la configuration Bonjour portail OMS (pour tous les nœuds) ou pour les nœuds uniques en exécutant hello suivante :
>
>

```
sudo su omsagent -c /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable
```


### <a name="enable-debug-logging"></a>Activer l’enregistrement du débogage
débogage de tooenable journalisation, vous pouvez utiliser le plug-in sortie hello OMS et la sortie des commentaires.

#### <a name="oms-output-plugin"></a>Plug-in de sortie OMS
FluentD permet hello plug-in toospecify niveaux de journalisation pour les niveaux de journal différent pour les entrées et sorties. toospecify un niveau de journal différent pour la sortie d’OMS, modifier la configuration de l’agent générales de hello Bonjour `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf` fichier.

Bas hello hello du fichier de configuration, modifiez hello `log_level` propriété à partir de `info` trop`debug`.

 ```
 <match oms.** docker.**>
  type out_oms
  log_level debug
  num_threads 5
  buffer_chunk_limit 5m
  buffer_type file
  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
  buffer_queue_limit 10
  flush_interval 20s
  retry_limit 10
  retry_wait 30s
</match>
 ```

Enregistrement de débogage vous permet de toohello de téléchargements toosee traités par lot Service OMS séparé par type, le nombre d’éléments de données et durée toosend.

*Exemple de journal activé pour le débogage :*

```
Success sending oms.nagios x 1 in 0.14s
Success sending oms.omi x 4 in 0.52s
Success sending oms.syslog.authpriv.info x 1 in 0.91s
```

#### <a name="verbose-output"></a>Sortie détaillée.
Au lieu d’utiliser le plug-in sortie hello OMS, vous pouvez également directement la sortie des éléments de données trop`stdout`, qui est visible dans hello Agent OMS pour Linux du journal.

Dans fichier de configuration générale de l’agent hello OMS à `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, commentez hello OMS plug-in de sortie en ajoutant un `#` devant chaque ligne.

```
#<match oms.** docker.**>
#  type out_oms
#  log_level info
#  num_threads 5
#  buffer_chunk_limit 5m
#  buffer_type file
#  buffer_path /var/opt/microsoft/omsagent/<workspace id>/state/out_oms*.buffer
#  buffer_queue_limit 10
#  flush_interval 20s
#  retry_limit 10
#  retry_wait 30s
#</match>
```

Hello plug-in de la sortie ci-dessous, de supprimer le commentaire hello Bonjour suivant la section en supprimant hello `#` symbole au début de hello de chaque ligne.

```
<match **>
  type stdout
</match>
```

### <a name="forwarded-syslog-messages-do-not-appear-in-hello-log"></a>Les messages Syslog transférés n’apparaissent pas dans le journal de hello
#### <a name="probable-causes"></a>Causes probables
* Hello configuration appliquée toohello Linux server ne pas autoriser la collecte d’installations de hello envoyé et/ou niveaux de journal
* Syslog n'est pas transmis correctement toohello Linux server
* nombre de Hello de messages transférés par seconde est trop élevée pour la configuration de base hello Hello Agent OMS pour Linux toohandle

#### <a name="resolutions"></a>Résolutions
* Vérifiez que la configuration hello Bonjour portail OMS pour Syslog a toutes les installations de hello et niveaux de journal correct hello
  * **Portail OMS &gt; Paramètres &gt; Données &gt; Syslog**
* Vérifiez que syslog natif démons de messagerie (`rsyslog`, `syslog-ng`) est en mesure de tooreceive messages hello transmis
* Vérifiez les paramètres de pare-feu sur hello Syslog serveur tooensure que les messages ne sont pas bloqués
* Simuler un tooOMS de message Syslog à l’aide de hello `logger` commande - par exemple :
  * `logger -p local0.err "This is my test message"`

### <a name="problems-connecting-toooms-when-using-a-proxy"></a>Problèmes de connexion tooOMS lors de l’utilisation d’un proxy
#### <a name="probable-causes"></a>Causes probables
* Hello de proxy spécifié lorsque l’agent de hello lors de l’installation et la configuration est incorrecte
* points de terminaison de Service OMS Hello ne sont pas whitelistested dans votre centre de données

#### <a name="resolutions"></a>Résolutions
* Réinstallez hello Agent OMS pour Linux à l’aide de hello suivant de commande avec l’option de hello `-v` activé. Ainsi, la sortie des commentaires de l’agent de hello qui se connectent via hello proxy toohello Service OMS.
  * `/opt/microsoft/omsagent/bin/omsadmin.sh -w <OMS Workspace ID> -s <OMS Workspace Key> -p <Proxy Conf> -v`
  * Passez en revue la documentation hello pour le proxy d’OMS à [agent hello de configuration pour une utilisation avec un serveur proxy HTTP](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#configuring-the-agent-for-use-with-an-http-proxy-server)
* Vérifiez que hello suivant les points de terminaison de Service OMS sont dans la liste approuvée

| Ressource de l'agent | Ports |
| --- | --- |
| &#42;.ods.opinsights.azure.com |Port 443 |
| &#42;.oms.opinsights.azure.com |Port 443 |
| ods.systemcenteradvisor.com |Port 443 |
| &#42;.blob.core.windows.net/ |Port 443 |

### <a name="a-403-error-is-displayed-when-onboarding"></a>Une erreur 403 s’affiche lors de l’intégration
#### <a name="probable-causes"></a>Causes probables
* hello date et l’heure sont incorrectes sur le serveur Linux
* Hello ID de l’espace de travail et la clé d’espace de travail utilisée sont incorrectes

#### <a name="resolution"></a>Résolution :
* Vérifiez le temps de hello sur votre serveur Linux avec hello `date` commande. Si hello données sont supérieures ou inférieure à 15 minutes à partir de hello heure actuelle, l’intégration échoue. toocorrect, mettre à jour la date de hello et/ou de fuseau horaire de votre serveur Linux.
* version la plus récente de l’Agent OMS pour Linux de hello Hello vous avertit si une différence de temps est entraînent l’échec de l’intégration
* À l’aide de RE-onboard hello correct ID et la clé de l’espace de travail. Consultez [l’intégration à l’aide de la ligne de commande hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) pour plus d’informations.

### <a name="a-500-error-or-404-error-appears-in-hello-log-file-after-onboarding"></a>Une erreur 500 ou erreur 404 s’affiche dans le fichier journal de hello après l’intégration
Il s’agit d’un problème connu qui se produit lors du chargement de première hello de données de Linux dans un espace de travail OMS. Cela n’affecte pas les données envoyées et ne génère pas d’autres problèmes. Vous pouvez ignorer les erreurs de hello lorsque initialement l’intégration.

### <a name="nagios-data-does-not-appear-in-hello-oms-portal"></a>Données de Nagios n’apparaissant pas dans hello portail OMS
#### <a name="probable-causes"></a>Causes probables
* utilisateur omsagent de Hello n’a pas les autorisations tooread à partir du fichier de journal Nagios hello
* Hello Nagios source et les sections de filtre sont toujours commentées dans le fichier de omsagent.conf hello

#### <a name="resolutions"></a>Résolutions
* Ajoutez hello omsagent utilisateur tooread de commande à partir du fichier de Nagios hello. Pour plus d’informations, voir [Nagios alerts](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#nagios-alerts) (Alertes Nagios).
* Dans hello Agent OMS pour le fichier de configuration générale de Linux à `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`, vérifiez que **les deux** hello Nagios source et filtre sections comportent des commentaires, supprimés, toohello similaire, l’exemple suivant.

```
<source>
  type tail
  path /var/log/nagios/nagios.log
  format none
  tag oms.nagios
</source>

<filter oms.nagios>
  type filter_nagios_log
</filter>
```


### <a name="linux-data-doesnt-appear-in-hello-oms-portal"></a>Les données Linux n’apparaissent pas dans hello portail OMS
#### <a name="probable-causes"></a>Causes probables
* Échec de l’intégration toohello Service OMS
* Connexion toohello Service OMS est bloquée.
* Hello Agent OMS pour Linux données est sauvegardée

#### <a name="resolutions"></a>Résolutions
* Vérifiez que l’intégration de toohello Service OMS a réussi en vérifiant que hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` existe.
* À l’aide de RE-onboard hello la ligne de commande omsadmin.sh. Consultez [l’intégration à l’aide de la ligne de commande hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) pour plus d’informations.
* Si vous utilisez un proxy, utilisez hello proxy étapes de dépannage ci-dessus
* Dans certains cas, lorsque hello Agent OMS pour Linux ne peuvent pas communiquer avec hello Service OMS, données sur l’Agent de hello sont taille de mémoire tampon saturée sauvegardé toohello de 50 Mo. Redémarrez hello Agent OMS pour Linux en exécutant hello `/opt/microsoft/omsagent/bin/service_control restart` commande.
  >[AZURE.NOTE] Ce problème est résolu dans l’Agent version 1.1.0-28 et versions ultérieures.

### <a name="syslog-linux-performance-counter-configuration-is-not-applied-in-hello-oms-portal"></a>Configuration de compteur de performances Syslog Linux n’est pas appliquée dans portail OMS : hello
#### <a name="probable-causes"></a>Causes probables
* l’agent de configuration Hello Bonjour Agent OMS pour Linux n’a pas récupéré configuration la plus récente hello à partir du portail OMS hello.
* Hello révision des paramètres dans le portail de hello n'ont pas été appliquées

#### <a name="resolutions"></a>Résolutions
`omsconfig`est de l’agent de configuration hello Bonjour Agent OMS pour Linux qui Récupère les modifications de configuration du portail OMS toutes les 5 minutes. Cette configuration est appliquée toohello Agent OMS pour Linux les fichiers de configuration situé à `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf`.

* Dans certains cas, les hello Agent OMS pour l’agent de configuration Linux peut-être pas en mesure de toocommunicate avec le service de configuration du portail hello résultant dans la configuration la plus récente ne s’applique ne pas.
* Vérifiez que hello `omsconfig` agent est installé avec les éléments suivants de hello :

  * `dpkg --list omsconfig` ou `rpm -qi omsconfig`
  * Le cas contraire, réinstaller la version la plus récente hello Hello Agent OMS pour Linux
* Vérifiez que hello `omsconfig` agent peut communiquer avec hello service OMS

  * Exécutez hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` commande
    * Hello commande ci-dessus retourne hello configuration que l’agent récupère à partir du portail hello, notamment les paramètres de Syslog, les compteurs de performances Linux et les journaux personnalisés
    * En cas d’échec de la commande hello ci-dessus, utilisez hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` commande. Cette commande force hello omsconfig agent toocommunicate avec hello OMS service tooretrieve hello configuration la plus récente.

### <a name="custom-linux-log-data-does-not-appear-in-hello-oms-portal"></a>Les données de journal Linux personnalisées n’apparaissent pas dans hello portail OMS
#### <a name="probable-causes"></a>Causes probables
* Échec du Service d’intégration tooOMS
* Hello **hello appliquer suivant toomy de configuration des serveurs Linux** paramètre n’a pas été sélectionné.
* omsconfig n’a pas récupéré de journal personnalisées de hello plus récente à partir du portail de hello
* Hello `omsagent` sert de journal personnalisées de hello tooaccess impossible en raison de problèmes d’autorisation tooa ou `omsagent` n’a été trouvé. Dans ce cas, vous verrez hello suivant de sortie :
  * `[DATETIME] [warn]: file not found. Continuing without tailing it.`
  * `[DATETIME] [error]: file not accessible by omsagent.`
* Il s’agit d’un problème connu avec hello Condition de concurrence qui a été résolu dans hello Agent OMS pour Linux version 1.1.0-217

#### <a name="resolutions"></a>Résolutions
* Vérifiez que vous avez correctement été intégré, en déterminant si hello `/etc/opt/microsoft/omsagent/<workspace id>/conf/omsadmin.conf` fichier existe.
  * Si nécessaire, intégrer à nouveau à l’aide de la ligne de commande omsadmin.sh hello. Consultez [l’intégration à l’aide de la ligne de commande hello](https://github.com/Microsoft/OMS-Agent-for-Linux/blob/master/docs/OMS-Agent-for-Linux.md#onboarding-using-the-command-line) pour plus d’informations.
* Dans hello portail OMS, sous **paramètres** sur hello **données** , vérifiez que hello **hello appliquer suivant toomy de configuration des serveurs Linux** paramètre est sélectionné.  
  ![appliquer la configuration](./media/log-analytics-linux-agents/customloglinuxenabled.png)
* Vérifiez que hello `omsconfig` agent peut communiquer avec hello service OMS

  * Exécutez hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/GetDscConfiguration.py'` commande
  * Hello commande ci-dessus retourne hello configuration que l’agent récupère à partir de hello portail, y compris les paramètres de Syslog, compteurs de performances Linux et des journaux personnalisés
  * En cas d’échec de la commande hello ci-dessus, utilisez hello `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/PerformRequiredConfigurationChecks.py` commande. Cette commande force hello omsconfig agent toocommunicate avec le service OMS et récupérer la configuration la plus récente hello.

Au lieu de hello Agent OMS pour utilisateur Linux en cours d’exécution en tant qu’un utilisateur doté de privilèges `root`, hello Agent OMS pour Linux s’exécute en tant que hello `omsagent` utilisateur. Dans la plupart des cas, l’autorisation explicite doit être octroyés à l’utilisateur de toohello dans l’ordre tooread certains fichiers.

autorisation de toogrant trop`omsagent` utilisateur, exécutez hello suivant de commandes :

1. Ajouter hello `omsagent` groupe spécifique d’utilisateurs tooa avec`sudo usermod -a -G <GROUPNAME> <USERNAME>`
2. Accorder l’accès en lecture universel toohello de fichier requis avec`sudo chmod -R ugo+rw <FILE DIRECTORY>`

Il existe un problème connu avec la Condition de concurrence qui a été résolu dans hello Agent OMS pour Linux version 1.1.0-217 de hello. Après la mise à jour de l’agent toohello plus récent, exécutez hello suivant commande tooget hello version la plus récente du plug-in de la sortie hello :

```
sudo cp /etc/opt/microsoft/omsagent/sysconf/omsagent.conf /etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf
```

## <a name="known-limitations"></a>Limites connues
Passez en revue hello suivant toolearn sections sur les limites actuelles de hello Agent OMS pour Linux.

### <a name="azure-diagnostics"></a>Azure Diagnostics
Pour les machines virtuelles Linux s’exécutant dans Azure, des étapes supplémentaires peuvent être collecte des données tooallow requis par les Diagnostics Azure et Operations Management Suite. **La version 2.2** hello Extension Diagnostics pour Linux est nécessaire pour la compatibilité avec hello Agent OMS pour Linux.

Pour plus d’informations sur l’installation et configuration de hello Extension Diagnostics pour Linux, consultez [utiliser tooenable de commande CLI d’Azure hello Extension Diagnostics Linux](../virtual-machines/linux/classic/diagnostic-extension-v2.md#use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension).

**Mise à niveau hello Extension de Diagnostics Linux à partir de 2.0 too2.2 ASM CLI de Azure :**

```
azure vm extension set -u <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.0
azure vm extension set <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

**ARM**

```
azure vm extension set -u <resource-group> <vm-name> Microsoft.Insights.VMDiagnosticsSettings Microsoft.OSTCExtensions 2.0
azure vm extension set <resource-group> <vm-name> LinuxDiagnostic Microsoft.OSTCExtensions 2.2 --private-config-path PrivateConfig.json
```

Ces exemples de commandes font référence à un fichier nommé PrivateConfig.json. format Hello de ce fichier doit ressembler à hello suivant l’exemple.

```
    {
    "storageAccountName":"hello storage account tooreceive data",
    "storageAccountKey":"hello key of hello account"
    }
```

### <a name="sysklog-is-not-supported"></a>Sysklog n’est pas pris en charge
Rsyslog ou syslog-ng est des messages syslog toocollect requis. démon syslog par défaut de Hello version 5 de Red Hat Enterprise Linux, CentOS et Oracle Linux (sysklog) n’est pas pris en charge pour la collecte d’événements syslog. toocollect les données syslog de cette version de ces distributions, hello rsyslog démon doit être installé et configuré tooreplace sysklog. Pour plus d’informations sur le remplacement de sysklog par rsyslog, consultez [installer le RPM rsyslog de hello nouvellement créé](http://wiki.rsyslog.com/index.php/Rsyslog_on_CentOS_success_story#Install_the_newly_built_rsyslog_RPM).

## <a name="next-steps"></a>Étapes suivantes
* [Ajouter des solutions d’Analytique de journal à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md) tooadd fonctionnalité et collecter les données.
* Se familiariser avec [recherche de journal](log-analytics-log-searches.md) tooview détaillées des informations collectées par les solutions.
* Utilisez [tableaux de bord](log-analytics-dashboards.md) toosave et afficher vos propres recherche.
