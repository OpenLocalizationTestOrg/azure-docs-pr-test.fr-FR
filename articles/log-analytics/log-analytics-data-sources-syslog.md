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
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="9ea1d-104">Sources de données Syslog dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9ea1d-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="9ea1d-105">Syslog est un protocole de journalisation d’événement qui est commun tooLinux.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-105">Syslog is an event logging protocol that is common tooLinux.</span></span>  <span data-ttu-id="9ea1d-106">Applications enverra les messages qui peuvent être stockées sur l’ordinateur local de hello ou remis tooa Syslog collecteur.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-106">Applications will send messages that may be stored on hello local machine or delivered tooa Syslog collector.</span></span>  <span data-ttu-id="9ea1d-107">Lorsque hello Agent OMS pour Linux est installé, il configure hello Syslog démon tooforward messages toohello l’agent local.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-107">When hello OMS Agent for Linux is installed, it configures hello local Syslog daemon tooforward messages toohello agent.</span></span>  <span data-ttu-id="9ea1d-108">l’agent de Hello envoie ensuite hello message tooLog Analytique où un enregistrement correspondant est créé dans le référentiel d’OMS hello.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-108">hello agent then sends hello message tooLog Analytics where a corresponding record is created in hello OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="9ea1d-109">Analytique de journal prend en charge la collection de messages envoyés par rsyslog ou syslog-ng, où rsyslog est le démon de hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is hello default daemon.</span></span> <span data-ttu-id="9ea1d-110">démon syslog par défaut de Hello version 5 de Red Hat Enterprise Linux, CentOS et Oracle Linux (sysklog) n’est pas pris en charge pour la collecte d’événements syslog.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-110">hello default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="9ea1d-111">toocollect les données syslog de cette version de ces distributions, hello [démon rsyslog](http://rsyslog.com) doit être installé et configuré tooreplace sysklog.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-111">toocollect syslog data from this version of these distributions, hello [rsyslog daemon](http://rsyslog.com) should be installed and configured tooreplace sysklog.</span></span>
>
>

![Collecte de messages Syslog](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="9ea1d-113">Configuration de Syslog</span><span class="sxs-lookup"><span data-stu-id="9ea1d-113">Configuring Syslog</span></span>
<span data-ttu-id="9ea1d-114">Hello Agent OMS pour Linux collecte uniquement les événements avec les installations hello et niveaux de gravité qui est spécifiés dans sa configuration.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-114">hello OMS Agent for Linux will only collect events with hello facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="9ea1d-115">Vous pouvez configurer Syslog par le biais du portail OMS hello ou par la gestion des fichiers de configuration sur vos agents de Linux.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-115">You can configure Syslog through hello OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-hello-oms-portal"></a><span data-ttu-id="9ea1d-116">Configurer Syslog dans portail OMS : hello</span><span class="sxs-lookup"><span data-stu-id="9ea1d-116">Configure Syslog in hello OMS portal</span></span>
<span data-ttu-id="9ea1d-117">Configurer Syslog à partir de hello [menu données de paramètres de journal Analytique](log-analytics-data-sources.md#configuring-data-sources).</span><span class="sxs-lookup"><span data-stu-id="9ea1d-117">Configure Syslog from hello [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="9ea1d-118">Cette configuration est remise le fichier de configuration toohello sur chaque agent Linux.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-118">This configuration is delivered toohello configuration file on each Linux agent.</span></span>

<span data-ttu-id="9ea1d-119">Vous pouvez ajouter une nouvelle installation en tapant son nom et en cliquant sur **+**.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="9ea1d-120">Pour chaque fonctionnalité, seuls les messages avec des niveaux de gravité hello sélectionné seront collectés.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-120">For each facility, only messages with hello selected severities will be collected.</span></span>  <span data-ttu-id="9ea1d-121">Vérifiez les niveaux de gravité hello pour la fonction de hello particulier que vous souhaitez toocollect.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-121">Check hello severities for hello particular facility that you want toocollect.</span></span>  <span data-ttu-id="9ea1d-122">Impossible d’indiquer des critères supplémentaires toofilter messages.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-122">You cannot provide any additional criteria toofilter messages.</span></span>

![Configurer les messages Syslog](media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="9ea1d-124">Par défaut, toutes les modifications de configuration sont automatiquement récupérées tooall agents.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-124">By default, all configuration changes are automatically pushed tooall agents.</span></span>  <span data-ttu-id="9ea1d-125">Si vous souhaitez tooconfigure Syslog manuellement sur chaque agent Linux, puis hello désactivez case à cocher *appliquer ci-dessous les machines Linux configuration toomy*.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-125">If you want tooconfigure Syslog manually on each Linux agent, then uncheck hello box *Apply below configuration toomy Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="9ea1d-126">Configurer l’agent Syslog sur Linux</span><span class="sxs-lookup"><span data-stu-id="9ea1d-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="9ea1d-127">Hello lorsque [agent OMS est installé sur un client Linux](log-analytics-linux-agents.md), il installe un fichier de configuration syslog par défaut qui définit la fonctionnalité de hello et gravité Hello les messages sont collectés.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-127">When hello [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines hello facility and severity of hello messages that are collected.</span></span>  <span data-ttu-id="9ea1d-128">Vous pouvez modifier cette configuration de hello toochange fichier.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-128">You can modify this file toochange hello configuration.</span></span>  <span data-ttu-id="9ea1d-129">fichier de configuration Hello est différente selon hello Syslog démon hello client a installé.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-129">hello configuration file is different depending on hello Syslog daemon that hello client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="9ea1d-130">Si vous modifiez la configuration syslog hello, vous devez redémarrer le démon syslog hello hello modifications tootake effet.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-130">If you edit hello syslog configuration, you must restart hello syslog daemon for hello changes tootake effect.</span></span>
>
>

#### <a name="rsyslog"></a><span data-ttu-id="9ea1d-131">rsyslog</span><span class="sxs-lookup"><span data-stu-id="9ea1d-131">rsyslog</span></span>
<span data-ttu-id="9ea1d-132">Hello rsyslog fichier de configuration se trouve à **/etc/rsyslog.d/95-omsagent.conf**.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-132">hello configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="9ea1d-133">Voici son contenu par défaut.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-133">Its default contents are shown below.</span></span>  <span data-ttu-id="9ea1d-134">Collecte les messages syslog envoyés à partir de l’agent local de hello pour toutes les fonctions ayant un niveau d’avertissement ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-134">This collects syslog messages sent from hello local agent for all facilities with a level of warning or higher.</span></span>

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

<span data-ttu-id="9ea1d-135">Vous pouvez supprimer une fonctionnalité en supprimant la partie du fichier de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-135">You can remove a facility by removing its section of hello configuration file.</span></span>  <span data-ttu-id="9ea1d-136">Vous pouvez limiter les niveaux de gravité hello qui sont collectées pour une installation donnée en modifiant entrée de ce dispositif.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-136">You can limit hello severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="9ea1d-137">Par exemple, toolimit hello utilisateur fonctionnalité toomessages avec un degré de gravité supérieur ou d’erreur vous serez modifier cette ligne de toohello de fichier de configuration hello suivant :</span><span class="sxs-lookup"><span data-stu-id="9ea1d-137">For example, toolimit hello user facility toomessages with a severity of error or higher you would modify that line of hello configuration file toohello following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="9ea1d-138">syslog-ng</span><span class="sxs-lookup"><span data-stu-id="9ea1d-138">syslog-ng</span></span>
<span data-ttu-id="9ea1d-139">fichier de configuration Hello syslog-ng est emplacement **/etc/syslog-ng/syslog-ng.conf**.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-139">hello configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="9ea1d-140">Voici son contenu par défaut.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-140">Its default contents are shown below.</span></span>  <span data-ttu-id="9ea1d-141">Collecte les messages syslog envoyés à partir de l’agent local de hello pour toutes les fonctions et tous les niveaux de gravité.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-141">This collects syslog messages sent from hello local agent for all facilities and all severities.</span></span>   

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

<span data-ttu-id="9ea1d-142">Vous pouvez supprimer une fonctionnalité en supprimant la partie du fichier de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-142">You can remove a facility by removing its section of hello configuration file.</span></span>  <span data-ttu-id="9ea1d-143">Vous pouvez limiter les niveaux de gravité hello qui sont collectées pour une installation donnée en les supprimant de sa liste.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-143">You can limit hello severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="9ea1d-144">Par exemple, toolimit hello utilisateur fonctionnalité toojust messages d’alerte et critiques, vous devez modifier cette section de toohello de fichier de configuration hello suivant :</span><span class="sxs-lookup"><span data-stu-id="9ea1d-144">For example, toolimit hello user facility toojust alert and critical messages, you would modify that section of hello configuration file toohello following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a><span data-ttu-id="9ea1d-145">Collecte de données à partir d’autres ports Syslog</span><span class="sxs-lookup"><span data-stu-id="9ea1d-145">Collecting data from additional Syslog ports</span></span>
<span data-ttu-id="9ea1d-146">agent d’OMS Hello écoute les messages Syslog sur le client local de hello sur le port 25224.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-146">hello OMS agent listens for Syslog messages on hello local client on port 25224.</span></span>  <span data-ttu-id="9ea1d-147">Lorsque l’agent hello est installé, une configuration de syslog par défaut est appliquée et trouve Bonjour à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="9ea1d-147">When hello agent is installed, a default syslog configuration is applied and found in hello following location:</span></span>

* <span data-ttu-id="9ea1d-148">Rsyslog : `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="9ea1d-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span></span>
* <span data-ttu-id="9ea1d-149">Syslog-ng : `/etc/syslog-ng/syslog-ng.conf`</span><span class="sxs-lookup"><span data-stu-id="9ea1d-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span></span>

<span data-ttu-id="9ea1d-150">Vous pouvez modifier le numéro de port hello en créant deux fichiers de configuration : un fichier de configuration FluentD et un fichier rsyslog-ou-syslog-ng selon le démon Syslog de hello que vous avez installé.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-150">You can change hello port number by creating two configuration files: a FluentD config file and a rsyslog-or-syslog-ng file depending on hello Syslog daemon you have installed.</span></span>  

* <span data-ttu-id="9ea1d-151">le fichier de configuration FluentD Hello doit être un fichier situé dans : `/etc/opt/microsoft/omsagent/conf/omsagent.d` et remplacez la valeur hello Bonjour **port** entrée avec votre numéro de port personnalisé.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-151">hello FluentD config file should be a new file located in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` and replace hello value in hello **port** entry with your custom port number.</span></span>

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

* <span data-ttu-id="9ea1d-152">Pour rsyslog, vous devez créer un nouveau fichier de configuration situé dans : `/etc/rsyslog.d/` et remplacez hello valeur SYSLOG_PORT % par votre numéro de port personnalisé.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-152">For rsyslog, you should create a new configuration file located in: `/etc/rsyslog.d/` and replace hello value %SYSLOG_PORT% with your custom port number.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="9ea1d-153">Si vous modifiez cette valeur dans le fichier de configuration hello `95-omsagent.conf`, il sera remplacé lors de l’agent de hello applique une configuration par défaut.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-153">If you modify this value in hello configuration file `95-omsagent.conf`, it will be overwritten when hello agent applies a default configuration.</span></span>
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* <span data-ttu-id="9ea1d-154">Hello syslog-ng config doit être modifié par copie de la configuration d’exemple hello ci-dessous et ajout de hello modifié des paramètres personnalisés toohello fin hello syslog-ng.conf du fichier de configuration situé dans `/etc/syslog-ng/`.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-154">hello syslog-ng config should be modified by copying hello example configuration shown below and adding hello custom modified settings toohello end of hello syslog-ng.conf configuration file located in `/etc/syslog-ng/`.</span></span>  <span data-ttu-id="9ea1d-155">Faire **pas** utiliser l’étiquette par défaut de hello **% WORKSPACE_ID % _oms** ou **% WORKSPACE_ID_OMS**, définir personnalisés étiquette toohelp distinguer vos modifications.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-155">Do **not** use hello default label **%WORKSPACE_ID%_oms** or **%WORKSPACE_ID_OMS**, define a custom label toohelp distinguish your changes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="9ea1d-156">Si vous modifiez les valeurs par défaut de hello dans le fichier de configuration hello, elles sont écrasées quand l’agent de hello s’applique à une configuration par défaut.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-156">If you modify hello default values in hello configuration file, they will be overwritten when hello agent applies a default configuration.</span></span>
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

<span data-ttu-id="9ea1d-157">Après avoir effectué les modifications de hello, hello Syslog et hello service de l’agent OMS doit toobe redémarré tooensure hello configuration modifications prennent effet.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-157">After completing hello changes, hello Syslog and hello OMS agent service needs toobe restarted tooensure hello configuration changes take effect.</span></span>   

## <a name="syslog-record-properties"></a><span data-ttu-id="9ea1d-158">Propriétés d’enregistrement Syslog</span><span class="sxs-lookup"><span data-stu-id="9ea1d-158">Syslog record properties</span></span>
<span data-ttu-id="9ea1d-159">Enregistrements syslog ont un type de **Syslog** et ont des propriétés de hello Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-159">Syslog records have a type of **Syslog** and have hello properties in hello following table.</span></span>

| <span data-ttu-id="9ea1d-160">Propriété</span><span class="sxs-lookup"><span data-stu-id="9ea1d-160">Property</span></span> | <span data-ttu-id="9ea1d-161">Description</span><span class="sxs-lookup"><span data-stu-id="9ea1d-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9ea1d-162">Ordinateur</span><span class="sxs-lookup"><span data-stu-id="9ea1d-162">Computer</span></span> |<span data-ttu-id="9ea1d-163">Ordinateur qui hello événements ont été collecté à partir de.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-163">Computer that hello event was collected from.</span></span> |
| <span data-ttu-id="9ea1d-164">Facility</span><span class="sxs-lookup"><span data-stu-id="9ea1d-164">Facility</span></span> |<span data-ttu-id="9ea1d-165">Définit la partie hello du système hello qui a généré le message de type hello.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-165">Defines hello part of hello system that generated hello message.</span></span> |
| <span data-ttu-id="9ea1d-166">HostIP</span><span class="sxs-lookup"><span data-stu-id="9ea1d-166">HostIP</span></span> |<span data-ttu-id="9ea1d-167">Adresse IP du système hello envoi de message de type hello.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-167">IP address of hello system sending hello message.</span></span> |
| <span data-ttu-id="9ea1d-168">HostName</span><span class="sxs-lookup"><span data-stu-id="9ea1d-168">HostName</span></span> |<span data-ttu-id="9ea1d-169">Nom du système hello envoi de message de type hello.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-169">Name of hello system sending hello message.</span></span> |
| <span data-ttu-id="9ea1d-170">SeverityLevel</span><span class="sxs-lookup"><span data-stu-id="9ea1d-170">SeverityLevel</span></span> |<span data-ttu-id="9ea1d-171">Niveau de gravité d’événement de hello.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-171">Severity level of hello event.</span></span> |
| <span data-ttu-id="9ea1d-172">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="9ea1d-172">SyslogMessage</span></span> |<span data-ttu-id="9ea1d-173">Texte du message de type hello.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-173">Text of hello message.</span></span> |
| <span data-ttu-id="9ea1d-174">ProcessID</span><span class="sxs-lookup"><span data-stu-id="9ea1d-174">ProcessID</span></span> |<span data-ttu-id="9ea1d-175">ID du processus hello qui a généré le message de type hello.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-175">ID of hello process that generated hello message.</span></span> |
| <span data-ttu-id="9ea1d-176">EventTime</span><span class="sxs-lookup"><span data-stu-id="9ea1d-176">EventTime</span></span> |<span data-ttu-id="9ea1d-177">Date et heure auxquelles l’événement de hello a été généré.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-177">Date and time that hello event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="9ea1d-178">Requêtes de journaux avec des enregistrements Syslog</span><span class="sxs-lookup"><span data-stu-id="9ea1d-178">Log queries with Syslog records</span></span>
<span data-ttu-id="9ea1d-179">Hello tableau suivant fournit des exemples de requêtes de journal qui extrait des enregistrements du journal système.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-179">hello following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="9ea1d-180">Interroger</span><span class="sxs-lookup"><span data-stu-id="9ea1d-180">Query</span></span> | <span data-ttu-id="9ea1d-181">Description</span><span class="sxs-lookup"><span data-stu-id="9ea1d-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9ea1d-182">Type = Syslog</span><span class="sxs-lookup"><span data-stu-id="9ea1d-182">Type=Syslog</span></span> |<span data-ttu-id="9ea1d-183">Tous les Syslog.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-183">All Syslogs.</span></span> |
| <span data-ttu-id="9ea1d-184">Type=Syslog SeverityLevel=error</span><span class="sxs-lookup"><span data-stu-id="9ea1d-184">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="9ea1d-185">Tous les enregistrements Syslog avec le niveau de gravité Erreur.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-185">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="9ea1d-186">Type=Syslog &#124; measure count() by Computer</span><span class="sxs-lookup"><span data-stu-id="9ea1d-186">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="9ea1d-187">Nombre d’enregistrements Syslog par ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-187">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="9ea1d-188">Type=Syslog &#124; measure count() by Facility</span><span class="sxs-lookup"><span data-stu-id="9ea1d-188">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="9ea1d-189">Nombre d’enregistrements Syslog par installation.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-189">Count of Syslog records by facility.</span></span> |

>[!NOTE]
> <span data-ttu-id="9ea1d-190">Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis hello ci-dessus requêtes modifierait toohello suivant.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-190">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above queries would change toohello following.</span></span>

> | <span data-ttu-id="9ea1d-191">Interroger</span><span class="sxs-lookup"><span data-stu-id="9ea1d-191">Query</span></span> | <span data-ttu-id="9ea1d-192">Description</span><span class="sxs-lookup"><span data-stu-id="9ea1d-192">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="9ea1d-193">syslog</span><span class="sxs-lookup"><span data-stu-id="9ea1d-193">Syslog</span></span> |<span data-ttu-id="9ea1d-194">Tous les Syslog.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-194">All Syslogs.</span></span> |
| <span data-ttu-id="9ea1d-195">Syslog &#124; where SeverityLevel == "error"</span><span class="sxs-lookup"><span data-stu-id="9ea1d-195">Syslog &#124; where SeverityLevel == "error"</span></span> |<span data-ttu-id="9ea1d-196">Tous les enregistrements Syslog avec le niveau de gravité Erreur.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-196">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="9ea1d-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span><span class="sxs-lookup"><span data-stu-id="9ea1d-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span></span> |<span data-ttu-id="9ea1d-198">Nombre d’enregistrements Syslog par ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-198">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="9ea1d-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span><span class="sxs-lookup"><span data-stu-id="9ea1d-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span></span> |<span data-ttu-id="9ea1d-200">Nombre d’enregistrements Syslog par installation.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-200">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9ea1d-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9ea1d-201">Next steps</span></span>
* <span data-ttu-id="9ea1d-202">En savoir plus sur [recherche de journal](log-analytics-log-searches.md) tooanalyze les données de salutation collectées à partir de sources de données et les solutions possibles.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span>
* <span data-ttu-id="9ea1d-203">Utilisez [les champs personnalisés](log-analytics-custom-fields.md) tooparse des données à partir d’enregistrements syslog dans des champs individuels.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-203">Use [Custom Fields](log-analytics-custom-fields.md) tooparse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="9ea1d-204">[Configurer les agents Linux](log-analytics-linux-agents.md) toocollect autres types de données.</span><span class="sxs-lookup"><span data-stu-id="9ea1d-204">[Configure Linux agents](log-analytics-linux-agents.md) toocollect other types of data.</span></span>
