---
title: Collecter et analyser les messages Syslog dans OMS Log Analytics | Microsoft Docs
description: "Syslog est un protocole de journalisation d’événements commun à Linux. Cet article décrit comment configurer la collecte de messages Syslog dans Log Analytics et des détails des enregistrements qu’ils créent dans le référentiel OMS."
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
ms.openlocfilehash: 7513f405d5c7c05a8e6e2b7b0e6313f23a319c84
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="syslog-data-sources-in-log-analytics"></a><span data-ttu-id="cfbc9-104">Sources de données Syslog dans Log Analytics</span><span class="sxs-lookup"><span data-stu-id="cfbc9-104">Syslog data sources in Log Analytics</span></span>
<span data-ttu-id="cfbc9-105">Syslog est un protocole de journalisation d’événements commun à Linux.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-105">Syslog is an event logging protocol that is common to Linux.</span></span>  <span data-ttu-id="cfbc9-106">Les applications envoient les messages qui peuvent être stockés sur l’ordinateur local ou remis à un collecteur Syslog.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-106">Applications will send messages that may be stored on the local machine or delivered to a Syslog collector.</span></span>  <span data-ttu-id="cfbc9-107">Lorsque l’agent OMS pour Linux est installé, il configure le démon Syslog local pour qu’il transfère des messages à l’agent.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-107">When the OMS Agent for Linux is installed, it configures the local Syslog daemon to forward messages to the agent.</span></span>  <span data-ttu-id="cfbc9-108">L’agent envoie ensuite le message à Log Analytics où un enregistrement correspondant est créé dans le référentiel OMS.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-108">The agent then sends the message to Log Analytics where a corresponding record is created in the OMS repository.</span></span>  

> [!NOTE]
> <span data-ttu-id="cfbc9-109">Log Analytics prend en charge la collecte de messages envoyés par rsyslog ou syslog-ng, où rsyslog est le démon par défaut.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-109">Log Analytics supports collection of messages sent by rsyslog or syslog-ng, where rsyslog is the default daemon.</span></span> <span data-ttu-id="cfbc9-110">Le démon syslog par défaut sur la version 5 de Red Hat Enterprise Linux, CentOS et Oracle Linux (sysklog) ne prend pas en charge la collecte des événements syslog.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-110">The default syslog daemon on version 5 of Red Hat Enterprise Linux, CentOS, and Oracle Linux version (sysklog) is not supported for syslog event collection.</span></span> <span data-ttu-id="cfbc9-111">Pour collecter les données syslog avec cette version de ces distributions, le [démon rsyslog](http://rsyslog.com) doit être installé et configuré à la place de syslog.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-111">To collect syslog data from this version of these distributions, the [rsyslog daemon](http://rsyslog.com) should be installed and configured to replace sysklog.</span></span>
>
>

![Collecte de messages Syslog](media/log-analytics-data-sources-syslog/overview.png)

## <a name="configuring-syslog"></a><span data-ttu-id="cfbc9-113">Configuration de Syslog</span><span class="sxs-lookup"><span data-stu-id="cfbc9-113">Configuring Syslog</span></span>
<span data-ttu-id="cfbc9-114">L’agent OMS pour Linux collecte uniquement les événements avec les installations et les niveaux de gravité spécifiés dans sa configuration.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-114">The OMS Agent for Linux will only collect events with the facilities and severities that are specified in its configuration.</span></span>  <span data-ttu-id="cfbc9-115">Vous pouvez configurer Syslog avec le portail OMS ou en gérant les fichiers de configuration sur vos agents Linux.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-115">You can configure Syslog through the OMS portal or by managing configuration files on your Linux agents.</span></span>

### <a name="configure-syslog-in-the-oms-portal"></a><span data-ttu-id="cfbc9-116">Configurer Syslog dans le portail OMS</span><span class="sxs-lookup"><span data-stu-id="cfbc9-116">Configure Syslog in the OMS portal</span></span>
<span data-ttu-id="cfbc9-117">Configurez Syslog à partir du [menu Données dans Paramètres Log Analytics](log-analytics-data-sources.md#configuring-data-sources).</span><span class="sxs-lookup"><span data-stu-id="cfbc9-117">Configure Syslog from the [Data menu in Log Analytics Settings](log-analytics-data-sources.md#configuring-data-sources).</span></span>  <span data-ttu-id="cfbc9-118">Cette configuration est remise au fichier de configuration sur chaque agent Linux.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-118">This configuration is delivered to the configuration file on each Linux agent.</span></span>

<span data-ttu-id="cfbc9-119">Vous pouvez ajouter une nouvelle installation en tapant son nom et en cliquant sur **+**.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-119">You can add a new facility by typing in its name and clicking **+**.</span></span>  <span data-ttu-id="cfbc9-120">Pour chaque installation, seuls les messages avec les niveaux de gravité sélectionnés seront collectés.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-120">For each facility, only messages with the selected severities will be collected.</span></span>  <span data-ttu-id="cfbc9-121">Vérifiez les niveaux de gravité de l’installation que vous souhaitez collecter.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-121">Check the severities for the particular facility that you want to collect.</span></span>  <span data-ttu-id="cfbc9-122">Vous ne pouvez pas fournir de critères supplémentaires pour filtrer les messages.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-122">You cannot provide any additional criteria to filter messages.</span></span>

![Configurer les messages Syslog](media/log-analytics-data-sources-syslog/configure.png)

<span data-ttu-id="cfbc9-124">Par défaut, toutes les modifications de configuration sont automatiquement transmises à l’ensemble des agents.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-124">By default, all configuration changes are automatically pushed to all agents.</span></span>  <span data-ttu-id="cfbc9-125">Si vous souhaitez configurer Syslog manuellement sur chaque agent Linux, décochez la case *Appliquer la configuration ci-dessous à mes machines Linux*.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-125">If you want to configure Syslog manually on each Linux agent, then uncheck the box *Apply below configuration to my Linux machines*.</span></span>

### <a name="configure-syslog-on-linux-agent"></a><span data-ttu-id="cfbc9-126">Configurer l’agent Syslog sur Linux</span><span class="sxs-lookup"><span data-stu-id="cfbc9-126">Configure Syslog on Linux agent</span></span>
<span data-ttu-id="cfbc9-127">Lorsque [l’agent OMS est installé sur un client Linux](log-analytics-linux-agents.md), il installe un fichier de configuration syslog par défaut qui définit l’installation et le niveau de gravité des messages qui sont collectés.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-127">When the [OMS agent is installed on a Linux client](log-analytics-linux-agents.md), it installs a default syslog configuration file that defines the facility and severity of the messages that are collected.</span></span>  <span data-ttu-id="cfbc9-128">Vous pouvez modifier ce fichier pour changer la configuration.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-128">You can modify this file to change the configuration.</span></span>  <span data-ttu-id="cfbc9-129">Le fichier de configuration est différent selon le démon Syslog installé par le client.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-129">The configuration file is different depending on the Syslog daemon that the client has installed.</span></span>

> [!NOTE]
> <span data-ttu-id="cfbc9-130">Si vous modifiez cette configuration, vous devez redémarrer le démon syslog pour que les modifications prennent effet.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-130">If you edit the syslog configuration, you must restart the syslog daemon for the changes to take effect.</span></span>
>
>

#### <a name="rsyslog"></a><span data-ttu-id="cfbc9-131">rsyslog</span><span class="sxs-lookup"><span data-stu-id="cfbc9-131">rsyslog</span></span>
<span data-ttu-id="cfbc9-132">Le fichier de configuration de rsyslog se trouve dans **/etc/rsyslog.d/95-omsagent.conf**.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-132">The configuration file for rsyslog is located at **/etc/rsyslog.d/95-omsagent.conf**.</span></span>  <span data-ttu-id="cfbc9-133">Voici son contenu par défaut.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-133">Its default contents are shown below.</span></span>  <span data-ttu-id="cfbc9-134">Collecte les messages syslog envoyés à partir de l’agent local pour toutes les installations avec un niveau Avertissement ou supérieur.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-134">This collects syslog messages sent from the local agent for all facilities with a level of warning or higher.</span></span>

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

<span data-ttu-id="cfbc9-135">Vous pouvez supprimer une installation en supprimant sa section du fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-135">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="cfbc9-136">Vous pouvez limiter les niveaux de gravité qui sont collectés pour une installation donnée en modifiant l’entrée de cette installation.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-136">You can limit the severities that are collected for a particular facility by modifying that facility's entry.</span></span>  <span data-ttu-id="cfbc9-137">Par exemple, pour limiter l’installation de l’utilisateur aux messages avec un niveau Erreur ou supérieur, il vous faudrait modifier cette ligne du fichier de configuration pour obtenir la ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="cfbc9-137">For example, to limit the user facility to messages with a severity of error or higher you would modify that line of the configuration file to the following:</span></span>

    user.error    @127.0.0.1:25224


#### <a name="syslog-ng"></a><span data-ttu-id="cfbc9-138">syslog-ng</span><span class="sxs-lookup"><span data-stu-id="cfbc9-138">syslog-ng</span></span>
<span data-ttu-id="cfbc9-139">Le fichier de configuration de syslog-ng est situé dans **/etc/syslog-ng/syslog-ng.conf**.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-139">The configuration file for syslog-ng is location at **/etc/syslog-ng/syslog-ng.conf**.</span></span>  <span data-ttu-id="cfbc9-140">Voici son contenu par défaut.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-140">Its default contents are shown below.</span></span>  <span data-ttu-id="cfbc9-141">Collecte les messages syslog envoyés à partir de l’agent local pour toutes les installations et tous les niveaux de gravité.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-141">This collects syslog messages sent from the local agent for all facilities and all severities.</span></span>   

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

<span data-ttu-id="cfbc9-142">Vous pouvez supprimer une installation en supprimant sa section du fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-142">You can remove a facility by removing its section of the configuration file.</span></span>  <span data-ttu-id="cfbc9-143">Vous pouvez limiter les niveaux de gravité qui sont collectés pour une installation donnée en les supprimant de sa liste.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-143">You can limit the severities that are collected for a particular facility by removing them from its list.</span></span>  <span data-ttu-id="cfbc9-144">Par exemple, pour limiter l’installation de l’utilisateur aux messages de niveau Alerte et Critique, il vous faudrait modifier cette section du fichier de configuration pour obtenir la section suivante :</span><span class="sxs-lookup"><span data-stu-id="cfbc9-144">For example, to limit the user facility to just alert and critical messages, you would modify that section of the configuration file to the following:</span></span>

    #OMS_facility = user
    filter f_user_oms { level(alert,crit) and facility(user); };
    log { source(src); filter(f_user_oms); destination(d_oms); };


### <a name="collecting-data-from-additional-syslog-ports"></a><span data-ttu-id="cfbc9-145">Collecte de données à partir d’autres ports Syslog</span><span class="sxs-lookup"><span data-stu-id="cfbc9-145">Collecting data from additional Syslog ports</span></span>
<span data-ttu-id="cfbc9-146">L’agent OMS écoute les messages Syslog sur le client local sur le port 25224.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-146">The OMS agent listens for Syslog messages on the local client on port 25224.</span></span>  <span data-ttu-id="cfbc9-147">Quand l’agent est installé, une configuration syslog par défaut est appliquée et se trouve à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="cfbc9-147">When the agent is installed, a default syslog configuration is applied and found in the following location:</span></span>

* <span data-ttu-id="cfbc9-148">Rsyslog : `/etc/rsyslog.d/95-omsagent.conf`</span><span class="sxs-lookup"><span data-stu-id="cfbc9-148">Rsyslog: `/etc/rsyslog.d/95-omsagent.conf`</span></span>
* <span data-ttu-id="cfbc9-149">Syslog-ng : `/etc/syslog-ng/syslog-ng.conf`</span><span class="sxs-lookup"><span data-stu-id="cfbc9-149">Syslog-ng: `/etc/syslog-ng/syslog-ng.conf`</span></span>

<span data-ttu-id="cfbc9-150">Vous pouvez modifier le numéro de port en créant deux fichiers de configuration : un fichier de configuration FluentD et un fichier rsyslog-ou-syslog-ng selon le démon Syslog que vous avez installé.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-150">You can change the port number by creating two configuration files: a FluentD config file and a rsyslog-or-syslog-ng file depending on the Syslog daemon you have installed.</span></span>  

* <span data-ttu-id="cfbc9-151">Le fichier de configuration FluentD doit être un nouveau fichier situé dans `/etc/opt/microsoft/omsagent/conf/omsagent.d` et vous devez remplacer la valeur de l’entrée **port** par votre numéro de port personnalisé.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-151">The FluentD config file should be a new file located in: `/etc/opt/microsoft/omsagent/conf/omsagent.d` and replace the value in the **port** entry with your custom port number.</span></span>

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

* <span data-ttu-id="cfbc9-152">Pour rsyslog, vous devez créer un fichier de configuration situé dans `/etc/rsyslog.d/` et remplacer la valeur %SYSLOG_PORT% par votre numéro de port personnalisé.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-152">For rsyslog, you should create a new configuration file located in: `/etc/rsyslog.d/` and replace the value %SYSLOG_PORT% with your custom port number.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="cfbc9-153">Si vous modifiez cette valeur dans le fichier de configuration `95-omsagent.conf`, elle est remplacée quand l’agent applique une configuration par défaut.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-153">If you modify this value in the configuration file `95-omsagent.conf`, it will be overwritten when the agent applies a default configuration.</span></span>
    >

        # OMS Syslog collection for workspace %WORKSPACE_ID%
        kern.warning              @127.0.0.1:%SYSLOG_PORT%
        user.warning              @127.0.0.1:%SYSLOG_PORT%
        daemon.warning            @127.0.0.1:%SYSLOG_PORT%
        auth.warning              @127.0.0.1:%SYSLOG_PORT%

* <span data-ttu-id="cfbc9-154">La configuration syslog-ng doit être modifiée en copiant l’exemple de configuration indiqué ci-dessous et en ajoutant les paramètres modifiés personnalisés à la fin du fichier de configuration syslog-ng.conf situé dans `/etc/syslog-ng/`.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-154">The syslog-ng config should be modified by copying the example configuration shown below and adding the custom modified settings to the end of the syslog-ng.conf configuration file located in `/etc/syslog-ng/`.</span></span>  <span data-ttu-id="cfbc9-155">N’utilisez **pas** l’étiquette par défaut **%WORKSPACE_ID%_oms** ni **%WORKSPACE_ID_OMS**, mais définissez une étiquette personnalisée pour mieux distinguer vos modifications.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-155">Do **not** use the default label **%WORKSPACE_ID%_oms** or **%WORKSPACE_ID_OMS**, define a custom label to help distinguish your changes.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="cfbc9-156">Si vous modifiez les valeurs par défaut dans le fichier de configuration, elles sont remplacées quand l’agent applique une configuration par défaut.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-156">If you modify the default values in the configuration file, they will be overwritten when the agent applies a default configuration.</span></span>
    >

        filter f_custom_filter { level(warning) and facility(auth; };
        destination d_custom_dest { udp("127.0.0.1" port(%SYSLOG_PORT%)); };
        log { source(s_src); filter(f_custom_filter); destination(d_custom_dest); };

<span data-ttu-id="cfbc9-157">Après avoir effectué les modifications, Syslog et le service de l’agent OMS doivent être redémarrés pour garantir que les modifications de configuration entrent en vigueur.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-157">After completing the changes, the Syslog and the OMS agent service needs to be restarted to ensure the configuration changes take effect.</span></span>   

## <a name="syslog-record-properties"></a><span data-ttu-id="cfbc9-158">Propriétés d’enregistrement Syslog</span><span class="sxs-lookup"><span data-stu-id="cfbc9-158">Syslog record properties</span></span>
<span data-ttu-id="cfbc9-159">Les enregistrements Syslog sont de type **Syslog** et leurs propriétés sont décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-159">Syslog records have a type of **Syslog** and have the properties in the following table.</span></span>

| <span data-ttu-id="cfbc9-160">Propriété</span><span class="sxs-lookup"><span data-stu-id="cfbc9-160">Property</span></span> | <span data-ttu-id="cfbc9-161">Description</span><span class="sxs-lookup"><span data-stu-id="cfbc9-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cfbc9-162">Ordinateur</span><span class="sxs-lookup"><span data-stu-id="cfbc9-162">Computer</span></span> |<span data-ttu-id="cfbc9-163">Ordinateur sur lequel l’événement a été collecté.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-163">Computer that the event was collected from.</span></span> |
| <span data-ttu-id="cfbc9-164">Facility</span><span class="sxs-lookup"><span data-stu-id="cfbc9-164">Facility</span></span> |<span data-ttu-id="cfbc9-165">Définit la partie du système qui a généré le message.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-165">Defines the part of the system that generated the message.</span></span> |
| <span data-ttu-id="cfbc9-166">HostIP</span><span class="sxs-lookup"><span data-stu-id="cfbc9-166">HostIP</span></span> |<span data-ttu-id="cfbc9-167">Adresse IP du système qui envoie le message.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-167">IP address of the system sending the message.</span></span> |
| <span data-ttu-id="cfbc9-168">HostName</span><span class="sxs-lookup"><span data-stu-id="cfbc9-168">HostName</span></span> |<span data-ttu-id="cfbc9-169">Nom du système qui envoie le message.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-169">Name of the system sending the message.</span></span> |
| <span data-ttu-id="cfbc9-170">SeverityLevel</span><span class="sxs-lookup"><span data-stu-id="cfbc9-170">SeverityLevel</span></span> |<span data-ttu-id="cfbc9-171">Niveau de gravité de l’événement.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-171">Severity level of the event.</span></span> |
| <span data-ttu-id="cfbc9-172">SyslogMessage</span><span class="sxs-lookup"><span data-stu-id="cfbc9-172">SyslogMessage</span></span> |<span data-ttu-id="cfbc9-173">Texte du message.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-173">Text of the message.</span></span> |
| <span data-ttu-id="cfbc9-174">ProcessID</span><span class="sxs-lookup"><span data-stu-id="cfbc9-174">ProcessID</span></span> |<span data-ttu-id="cfbc9-175">ID du processus qui a généré le message.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-175">ID of the process that generated the message.</span></span> |
| <span data-ttu-id="cfbc9-176">EventTime</span><span class="sxs-lookup"><span data-stu-id="cfbc9-176">EventTime</span></span> |<span data-ttu-id="cfbc9-177">Date et heure de génération de l’événement.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-177">Date and time that the event was generated.</span></span> |

## <a name="log-queries-with-syslog-records"></a><span data-ttu-id="cfbc9-178">Requêtes de journaux avec des enregistrements Syslog</span><span class="sxs-lookup"><span data-stu-id="cfbc9-178">Log queries with Syslog records</span></span>
<span data-ttu-id="cfbc9-179">Le tableau suivant fournit plusieurs exemples de requêtes de journaux qui extraient des enregistrements Syslog.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-179">The following table provides different examples of log queries that retrieve Syslog records.</span></span>

| <span data-ttu-id="cfbc9-180">Requête</span><span class="sxs-lookup"><span data-stu-id="cfbc9-180">Query</span></span> | <span data-ttu-id="cfbc9-181">Description</span><span class="sxs-lookup"><span data-stu-id="cfbc9-181">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cfbc9-182">Type = Syslog</span><span class="sxs-lookup"><span data-stu-id="cfbc9-182">Type=Syslog</span></span> |<span data-ttu-id="cfbc9-183">Tous les Syslog.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-183">All Syslogs.</span></span> |
| <span data-ttu-id="cfbc9-184">Type=Syslog SeverityLevel=error</span><span class="sxs-lookup"><span data-stu-id="cfbc9-184">Type=Syslog SeverityLevel=error</span></span> |<span data-ttu-id="cfbc9-185">Tous les enregistrements Syslog avec le niveau de gravité Erreur.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-185">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="cfbc9-186">Type=Syslog &#124; measure count() by Computer</span><span class="sxs-lookup"><span data-stu-id="cfbc9-186">Type=Syslog &#124; measure count() by Computer</span></span> |<span data-ttu-id="cfbc9-187">Nombre d’enregistrements Syslog par ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-187">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="cfbc9-188">Type=Syslog &#124; measure count() by Facility</span><span class="sxs-lookup"><span data-stu-id="cfbc9-188">Type=Syslog &#124; measure count() by Facility</span></span> |<span data-ttu-id="cfbc9-189">Nombre d’enregistrements Syslog par installation.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-189">Count of Syslog records by facility.</span></span> |

>[!NOTE]
> <span data-ttu-id="cfbc9-190">Si vous avez mis à niveau votre espace de travail vers le [nouveau langage de requête Log Analytics](log-analytics-log-search-upgrade.md), les requêtes ci-dessus sont remplacées par les requêtes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-190">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above queries would change to the following.</span></span>

> | <span data-ttu-id="cfbc9-191">Interroger</span><span class="sxs-lookup"><span data-stu-id="cfbc9-191">Query</span></span> | <span data-ttu-id="cfbc9-192">Description</span><span class="sxs-lookup"><span data-stu-id="cfbc9-192">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="cfbc9-193">syslog</span><span class="sxs-lookup"><span data-stu-id="cfbc9-193">Syslog</span></span> |<span data-ttu-id="cfbc9-194">Tous les Syslog.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-194">All Syslogs.</span></span> |
| <span data-ttu-id="cfbc9-195">Syslog &#124; where SeverityLevel == "error"</span><span class="sxs-lookup"><span data-stu-id="cfbc9-195">Syslog &#124; where SeverityLevel == "error"</span></span> |<span data-ttu-id="cfbc9-196">Tous les enregistrements Syslog avec le niveau de gravité Erreur.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-196">All Syslog records with severity of error.</span></span> |
| <span data-ttu-id="cfbc9-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span><span class="sxs-lookup"><span data-stu-id="cfbc9-197">Syslog &#124; summarize AggregatedValue = count() by Computer</span></span> |<span data-ttu-id="cfbc9-198">Nombre d’enregistrements Syslog par ordinateur.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-198">Count of Syslog records by computer.</span></span> |
| <span data-ttu-id="cfbc9-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span><span class="sxs-lookup"><span data-stu-id="cfbc9-199">Syslog &#124; summarize AggregatedValue = count() by Facility</span></span> |<span data-ttu-id="cfbc9-200">Nombre d’enregistrements Syslog par installation.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-200">Count of Syslog records by facility.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cfbc9-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cfbc9-201">Next steps</span></span>
* <span data-ttu-id="cfbc9-202">Découvrez les [recherches de journal](log-analytics-log-searches.md) pour analyser les données collectées dans des sources de données et des solutions.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-202">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span>
* <span data-ttu-id="cfbc9-203">Utilisez les [Champs personnalisés](log-analytics-custom-fields.md) pour analyser les données des enregistrements syslog dans des champs individuels.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-203">Use [Custom Fields](log-analytics-custom-fields.md) to parse data from syslog records into individual fields.</span></span>
* <span data-ttu-id="cfbc9-204">[Configurez les agents Linux](log-analytics-linux-agents.md) pour qu’ils collectent d’autres types de données.</span><span class="sxs-lookup"><span data-stu-id="cfbc9-204">[Configure Linux agents](log-analytics-linux-agents.md) to collect other types of data.</span></span>
