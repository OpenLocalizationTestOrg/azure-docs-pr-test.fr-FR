---
title: aaaCollect et analyser les messages Syslog dans OMS journal Analytique | Documents Microsoft
description: "Syslog est un protocole de journalisation d’événement qui est commun tooLinux. Cet article décrit comment collection tooconfigure des messages Syslog dans Analytique de journal et les détails des enregistrements de hello créent dans le référentiel d’OMS hello."
services: log-analytics
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: f1d5bde4-6b86-4b8e-b5c1-3ecbaba76198
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/12/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 8bfa0bca3f2f18287d1352c98bbaa2a70e41e276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a>Sources de données Syslog dans Log Analytics
Syslog est un protocole de journalisation d’événement qui est commun tooLinux.  Applications enverra les messages qui peuvent être stockées sur l’ordinateur local de hello ou remis tooa Syslog collecteur.  Lorsque hello Agent OMS pour Linux est installé, il configure hello Syslog démon tooforward messages toohello l’agent local.  l’agent de Hello envoie ensuite hello message tooLog Analytique où un enregistrement correspondant est créé dans le référentiel d’OMS hello.  

> [!NOTE]
> Analytique de journal prend en charge la collection de messages envoyés par rsyslog ou syslog-ng, où rsyslog est le démon de hello par défaut. démon syslog par défaut de Hello version 5 de Red Hat Enterprise Linux, CentOS et Oracle Linux (sysklog) n’est pas pris en charge pour la collecte d’événements syslog. toocollect les données syslog de cette version de ces distributions, hello [démon rsyslog](http://rsyslog.com) doit être installé et configuré tooreplace sysklog.
>
>

![Collecte de messages Syslog](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a>Configuration de Syslog
Hello Agent OMS pour Linux collecte uniquement les événements avec les installations hello et niveaux de gravité qui est spécifiés dans sa configuration.  Vous pouvez configurer Syslog par le biais du portail OMS hello ou par la gestion des fichiers de configuration sur vos agents de Linux.

### <a name="configure-syslog-in-hello-oms-portal"></a>Configurer Syslog dans portail OMS : hello
Configurer Syslog à partir de hello [menu données de paramètres de journal Analytique](log-analytics-data-sources.md#configuring-data-sources).  Cette configuration est remise le fichier de configuration toohello sur chaque agent Linux.

Vous pouvez ajouter une nouvelle installation en tapant son nom et en cliquant sur **+**.  Pour chaque fonctionnalité, seuls les messages avec des niveaux de gravité hello sélectionné seront collectés.  Vérifiez les niveaux de gravité hello pour la fonction de hello particulier que vous souhaitez toocollect.  Impossible d’indiquer des critères supplémentaires toofilter messages.

![Configurer les messages Syslog](media/log-analytics-data-sources-syslog/configure.png)

Par défaut, toutes les modifications de configuration sont automatiquement récupérées tooall agents.  Si vous souhaitez tooconfigure Syslog manuellement sur chaque agent Linux, puis hello désactivez case à cocher *appliquer ci-dessous les machines Linux configuration toomy*.

### <a name="configure-syslog-on-linux-agent"></a>Configurer l’agent Syslog sur Linux
Hello lorsque [agent OMS est installé sur un client Linux](log-analytics-linux-agents.md), il installe un fichier de configuration syslog par défaut qui définit la fonctionnalité de hello et gravité Hello les messages sont collectés.  Vous pouvez modifier cette configuration de hello toochange fichier.  fichier de configuration Hello est différente selon hello Syslog démon hello client a installé.

> [!NOTE]
> Si vous modifiez la configuration syslog hello, vous devez redémarrer le démon syslog hello hello modifications tootake effet.
>
>

#### <a name="rsyslog"></a>rsyslog
Hello rsyslog fichier de configuration se trouve à **/etc/rsyslog.d/95-omsagent.conf**.  Voici son contenu par défaut.  Collecte les messages syslog envoyés à partir de l’agent local de hello pour toutes les fonctions ayant un niveau d’avertissement ou une version ultérieure.

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

Vous pouvez supprimer une fonctionnalité en supprimant la partie du fichier de configuration hello.  Vous pouvez limiter les niveaux de gravité hello qui sont collectées pour une installation donnée en modifiant entrée de ce dispositif.  Par exemple, toolimit hello utilisateur fonctionnalité toomessages avec un degré de gravité supérieur ou d’erreur vous serez modifier cette ligne de toohello de fichier de configuration hello suivant :

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a>syslog-ng
fichier de configuration Hello syslog-ng est emplacement **/etc/syslog-ng/syslog-ng.conf**.  Voici son contenu par défaut.  Collecte les messages syslog envoyés à partir de l’agent local de hello pour toutes les fonctions et tous les niveaux de gravité.   

    #
    # Warnings (except iptables) in one file:
    #
    destination warn { file("/var/log/warn" fsync(yes)); };
    log { source(src); filter(f_warn); destination(warn); };

    #OMS_Destination
    destination d_oms { udp("127.0.0.1" port(25224)); };

    #OMS_facility = auth
    filter f_auth_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(auth); };
    log { source(src); filter(f_auth_oms); destination(d_oms); };

    #OMS_facility = authpriv
    filter f_authpriv_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(authpriv); };
    log { source(src); filter(f_authpriv_oms); destination(d_oms); };

    #OMS_facility = cron
    filter f_cron_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(cron); };
    log { source(src); filter(f_cron_oms); destination(d_oms); };

    #OMS_facility = daemon
    filter f_daemon_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(daemon); };
    log { source(src); filter(f_daemon_oms); destination(d_oms); };

    #OMS_facility = kern
    filter f_kern_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(kern); };
    log { source(src); filter(f_kern_oms); destination(d_oms); };

    #OMS_facility = local0
    filter f_local0_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local0); };
    log { source(src); filter(f_local0_oms); destination(d_oms); };

    #OMS_facility = local1
    filter f_local1_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(local1); };
    log { source(src); filter(f_local1_oms); destination(d_oms); };

    #OMS_facility = mail
    filter f_mail_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(mail); };
    log { source(src); filter(f_mail_oms); destination(d_oms); };

    #OMS_facility = syslog
    filter f_syslog_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(syslog); };
    log { source(src); filter(f_syslog_oms); destination(d_oms); };

    #OMS_facility = user
    filter f_user_oms { level(alert,crit,debug,emerg,err,info,notice,warning) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };

Vous pouvez supprimer une fonctionnalité en supprimant la partie du fichier de configuration hello.  Vous pouvez limiter les niveaux de gravité hello qui sont collectées pour une installation donnée en les supprimant de sa liste.  Par exemple, toolimit hello utilisateur fonctionnalité toojust messages d’alerte et critiques, vous devez modifier cette section de toohello de fichier de configuration hello suivant :

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a>Collecte de données à partir d’autres ports Syslog
agent d’OMS Hello écoute les messages Syslog sur le client local de hello sur le port 25224.  Lorsque l’agent hello est installé, une configuration de syslog par défaut est appliquée et trouve Bonjour à l’emplacement suivant :

* Rsyslog : `/etc/rsyslog.d/95-omsagent.conf`
* Syslog-ng : `/etc/syslog-ng/syslog-ng.conf`

Vous pouvez modifier le numéro de port hello en créant deux fichiers de configuration : un fichier de configuration FluentD et un fichier rsyslog-ou-syslog-ng selon le démon Syslog de hello que vous avez installé.  

* le fichier de configuration FluentD Hello doit être un fichier situé dans : `/etc/opt/microsoft/omsagent/conf/omsagent.d` et remplacez la valeur hello Bonjour **port** entrée avec votre numéro de port personnalisé.

        <source>
          type syslog
          port %SYSLOG_PORT%
          bind 127.0.0.1
          protocol_type udp
          tag oms.syslog
        </source>
        <filter oms.syslog.**>
          type filter_syslog
        </filter>

* Pour rsyslog, vous devez créer un nouveau fichier de configuration situé dans : `/etc/rsyslog.d/` et remplacez hello valeur SYSLOG_PORT % par votre numéro de port personnalisé.  

    > [!NOTE]
    > Si vous modifiez cette valeur dans le fichier de configuration hello `95-omsagent.conf`, il sera remplacé lors de l’agent de hello applique une configuration par défaut.
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* Hello syslog-ng config doit être modifié par copie de la configuration d’exemple hello ci-dessous et ajout de hello modifié des paramètres personnalisés toohello fin hello syslog-ng.conf du fichier de configuration situé dans `/etc/syslog-ng/`.  Faire **pas** utiliser l’étiquette par défaut de hello **% WORKSPACE_ID % _oms** ou **% WORKSPACE_ID_OMS**, définir personnalisés étiquette toohelp distinguer vos modifications.  

    > [!NOTE]
    > Si vous modifiez les valeurs par défaut de hello dans le fichier de configuration hello, elles sont écrasées quand l’agent de hello s’applique à une configuration par défaut.
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

Après avoir effectué les modifications de hello, hello Syslog et hello service de l’agent OMS doit toobe redémarré tooensure hello configuration modifications prennent effet.   

## <a name="syslog-record-properties"></a>Propriétés d’enregistrement Syslog
Enregistrements syslog ont un type de **Syslog** et ont des propriétés de hello Bonjour tableau suivant.

| Propriété | Description |
|:--- |:--- |
| Ordinateur |Ordinateur qui hello événements ont été collecté à partir de. |
| Facility |Définit la partie hello du système hello qui a généré le message de type hello. |
| HostIP |Adresse IP du système hello envoi de message de type hello. |
| HostName |Nom du système hello envoi de message de type hello. |
| SeverityLevel |Niveau de gravité d’événement de hello. |
| SyslogMessage |Texte du message de type hello. |
| ProcessID |ID du processus hello qui a généré le message de type hello. |
| EventTime |Date et heure auxquelles l’événement de hello a été généré. |

## <a name="log-queries-with-syslog-records"></a>Requêtes de journaux avec des enregistrements Syslog
Hello tableau suivant fournit des exemples de requêtes de journal qui extrait des enregistrements du journal système.

| Interroger | Description |
|:--- |:--- |
| Type = Syslog |Tous les Syslog. |
| Type=Syslog SeverityLevel=error |Tous les enregistrements Syslog avec le niveau de gravité Erreur. |
| Type=Syslog &#124; measure count() by Computer |Nombre d’enregistrements Syslog par ordinateur. |
| Type=Syslog &#124; measure count() by Facility |Nombre d’enregistrements Syslog par installation. |

>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis hello ci-dessus requêtes modifierait toohello suivant.

> | Interroger | Description |
|:--- |:--- |
| syslog |Tous les Syslog. |
| Syslog &#124; where SeverityLevel == "error" |Tous les enregistrements Syslog avec le niveau de gravité Erreur. |
| Syslog &#124; summarize AggregatedValue = count() by Computer |Nombre d’enregistrements Syslog par ordinateur. |
| Syslog &#124; summarize AggregatedValue = count() by Facility |Nombre d’enregistrements Syslog par installation. |

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [recherche de journal](log-analytics-log-searches.md) tooanalyze les données de salutation collectées à partir de sources de données et les solutions possibles.
* Utilisez [les champs personnalisés](log-analytics-custom-fields.md) tooparse des données à partir d’enregistrements syslog dans des champs individuels.
* [Configurer les agents Linux](log-analytics-linux-agents.md) toocollect autres types de données.
