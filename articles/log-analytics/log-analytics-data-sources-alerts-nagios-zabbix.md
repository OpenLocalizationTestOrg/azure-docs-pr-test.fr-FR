---
title: alertes de Nagios et Zabbix aaaCollect dans Analytique des journaux OMS | Documents Microsoft
description: "Nagios et Zabbix sont des outils de surveillance open source. Vous pouvez collecter à partir des alertes ces outils dans Analytique de journal dans l’ordre tooanalyze les ainsi que des alertes à partir d’autres sources.  Cet article décrit comment tooconfigure hello Agent OMS pour Linux toocollect des alertes à partir de ces systèmes."
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
ms.date: 05/04/2017
ms.author: magoedte
ms.openlocfilehash: 23e2252e4fed8bc87baec063694a8472ca84220d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="ac80d-105">Collecte d’alertes à partir de Nagios et Zabbix dans Log Analytics à partir de l’agent OMS pour Linux</span><span class="sxs-lookup"><span data-stu-id="ac80d-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="ac80d-106">[Nagios](https://www.nagios.org/) et [Zabbix](http://www.zabbix.com/) sont des outils de surveillance open source.</span><span class="sxs-lookup"><span data-stu-id="ac80d-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="ac80d-107">Vous peut collecter des alertes à partir de ces outils dans Analytique de journal dans l’ordre tooanalyze les avec [alertes provenant d’autres sources](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="ac80d-107">You can collect alerts from these tools into Log Analytics in order tooanalyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="ac80d-108">Cet article décrit comment tooconfigure hello Agent OMS pour Linux toocollect des alertes à partir de ces systèmes.</span><span class="sxs-lookup"><span data-stu-id="ac80d-108">This article describes how tooconfigure hello OMS Agent for Linux toocollect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="ac80d-109">Configuration de la collecte d’alertes</span><span class="sxs-lookup"><span data-stu-id="ac80d-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="ac80d-110">Configuration de la collecte d’alertes Nagios</span><span class="sxs-lookup"><span data-stu-id="ac80d-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="ac80d-111">Effectuer hello sur les alertes de hello Nagios server toocollect comme suit.</span><span class="sxs-lookup"><span data-stu-id="ac80d-111">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="ac80d-112">Utilisateur de subventions hello **omsagent** fichier journal de l’accès en lecture toohello Nagios (c'est-à-dire `/var/log/nagios/nagios.log`).</span><span class="sxs-lookup"><span data-stu-id="ac80d-112">Grant hello user **omsagent** read access toohello Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="ac80d-113">En supposant que le fichier de hello nagios.log est détenu par groupe de hello `nagios`, vous pouvez ajouter hello utilisateur **omsagent** toohello **nagios** groupe.</span><span class="sxs-lookup"><span data-stu-id="ac80d-113">Assuming hello nagios.log file is owned by hello group `nagios`, you can add hello user **omsagent** toohello **nagios** group.</span></span> 

    <span data-ttu-id="ac80d-114">sudo usermod -a -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="ac80d-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="ac80d-115">Modifier le fichier de configuration hello à (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="ac80d-115">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="ac80d-116">Vérifiez que hello suivant entrées est présents et pas commentées :</span><span class="sxs-lookup"><span data-stu-id="ac80d-116">Ensure hello following entries are present and not commented out:</span></span>  

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

3. <span data-ttu-id="ac80d-117">Redémarrez le démon omsagent de hello</span><span class="sxs-lookup"><span data-stu-id="ac80d-117">Restart hello omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="ac80d-118">Configuration de la collecte d’alertes Zabbix</span><span class="sxs-lookup"><span data-stu-id="ac80d-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="ac80d-119">toocollect les alertes d’un serveur Zabbix, vous devez toospecify un utilisateur et mot de passe dans *clair*.</span><span class="sxs-lookup"><span data-stu-id="ac80d-119">toocollect alerts from a Zabbix server, you need toospecify a user and password in *clear text*.</span></span> <span data-ttu-id="ac80d-120">Cela n’est pas idéale, mais nous recommandons que vous créez hello utilisateur et accordez des autorisations toomonitor onlu.</span><span class="sxs-lookup"><span data-stu-id="ac80d-120">This is not ideal, but we recommend that you create hello user and grant permissions toomonitor onlu.</span></span>

<span data-ttu-id="ac80d-121">Effectuer hello sur les alertes de hello Nagios server toocollect comme suit.</span><span class="sxs-lookup"><span data-stu-id="ac80d-121">Perform hello following steps on hello Nagios server toocollect alerts.</span></span>

1. <span data-ttu-id="ac80d-122">Modifier le fichier de configuration hello à (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="ac80d-122">Modify hello configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="ac80d-123">Vérifiez que hello suivant entrées est présents et pas commentées.  Modifier utilisateur hello nom et mot de passe de toovalues pour votre environnement Zabbix.</span><span class="sxs-lookup"><span data-stu-id="ac80d-123">Ensure hello following entries are present and not commented out.  Change hello user name and password toovalues for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="ac80d-124">Redémarrez le démon omsagent de hello</span><span class="sxs-lookup"><span data-stu-id="ac80d-124">Restart hello omsagent daemon</span></span>

    <span data-ttu-id="ac80d-125">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="ac80d-125">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="ac80d-126">Enregistrements d’alerte</span><span class="sxs-lookup"><span data-stu-id="ac80d-126">Alert records</span></span>
<span data-ttu-id="ac80d-127">Vous pouvez récupérer les enregistrements d’alerte de Nagios et Zabbix à l’aide des [recherches dans les journaux](log-analytics-log-searches.md) dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="ac80d-127">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="ac80d-128">Enregistrements d’alerte Nagios</span><span class="sxs-lookup"><span data-stu-id="ac80d-128">Nagios Alert records</span></span>

<span data-ttu-id="ac80d-129">Pour les enregistrements d’alerte collectés par Nagios, le **type** est **Alerte** et la valeur **SourceSystem** est **Nagios**.</span><span class="sxs-lookup"><span data-stu-id="ac80d-129">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="ac80d-130">Elles ont des propriétés de hello Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="ac80d-130">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="ac80d-131">Propriété</span><span class="sxs-lookup"><span data-stu-id="ac80d-131">Property</span></span> | <span data-ttu-id="ac80d-132">Description</span><span class="sxs-lookup"><span data-stu-id="ac80d-132">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ac80d-133">Type</span><span class="sxs-lookup"><span data-stu-id="ac80d-133">Type</span></span> |<span data-ttu-id="ac80d-134">*Alert*</span><span class="sxs-lookup"><span data-stu-id="ac80d-134">*Alert*</span></span> |
| <span data-ttu-id="ac80d-135">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="ac80d-135">SourceSystem</span></span> |<span data-ttu-id="ac80d-136">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="ac80d-136">*Nagios*</span></span> |
| <span data-ttu-id="ac80d-137">AlertName</span><span class="sxs-lookup"><span data-stu-id="ac80d-137">AlertName</span></span> |<span data-ttu-id="ac80d-138">Nom de l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="ac80d-138">Name of hello alert.</span></span> |
| <span data-ttu-id="ac80d-139">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="ac80d-139">AlertDescription</span></span> | <span data-ttu-id="ac80d-140">Description de l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="ac80d-140">Description of hello alert.</span></span> |
| <span data-ttu-id="ac80d-141">AlertState</span><span class="sxs-lookup"><span data-stu-id="ac80d-141">AlertState</span></span> | <span data-ttu-id="ac80d-142">État du service de hello ou hôte.</span><span class="sxs-lookup"><span data-stu-id="ac80d-142">Status of hello service or host.</span></span><br><br><span data-ttu-id="ac80d-143">OK</span><span class="sxs-lookup"><span data-stu-id="ac80d-143">OK</span></span><br><span data-ttu-id="ac80d-144">AVERTISSEMENT</span><span class="sxs-lookup"><span data-stu-id="ac80d-144">WARNING</span></span><br><span data-ttu-id="ac80d-145">ACTIF</span><span class="sxs-lookup"><span data-stu-id="ac80d-145">UP</span></span><br><span data-ttu-id="ac80d-146">INACTIF</span><span class="sxs-lookup"><span data-stu-id="ac80d-146">DOWN</span></span> |
| <span data-ttu-id="ac80d-147">HostName</span><span class="sxs-lookup"><span data-stu-id="ac80d-147">HostName</span></span> | <span data-ttu-id="ac80d-148">Nom d’hôte hello qui a créé l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="ac80d-148">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="ac80d-149">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="ac80d-149">PriorityNumber</span></span> | <span data-ttu-id="ac80d-150">Niveau de priorité d’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="ac80d-150">Priority level of hello alert.</span></span> |
| <span data-ttu-id="ac80d-151">StateType</span><span class="sxs-lookup"><span data-stu-id="ac80d-151">StateType</span></span> | <span data-ttu-id="ac80d-152">type Hello de l’état d’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="ac80d-152">hello type of state of hello alert.</span></span><br><br><span data-ttu-id="ac80d-153">LÉGER : problème qui n’a pas été revérifié.</span><span class="sxs-lookup"><span data-stu-id="ac80d-153">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="ac80d-154">URGENT : problème qui a été revérifié un nombre spécifié de fois.</span><span class="sxs-lookup"><span data-stu-id="ac80d-154">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="ac80d-155">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="ac80d-155">TimeGenerated</span></span> |<span data-ttu-id="ac80d-156">Création de l’alerte hello date et heure.</span><span class="sxs-lookup"><span data-stu-id="ac80d-156">Date and time hello alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="ac80d-157">Enregistrements d’alerte Zabbix</span><span class="sxs-lookup"><span data-stu-id="ac80d-157">Zabbix alert records</span></span>
<span data-ttu-id="ac80d-158">Pour les enregistrements d’alerte collectés par Zabbix, le **type** est **Alerte** et la valeur **SourceSystem** est **Zabbix**.</span><span class="sxs-lookup"><span data-stu-id="ac80d-158">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="ac80d-159">Elles ont des propriétés de hello Bonjour tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="ac80d-159">They have hello properties in hello following table.</span></span>

| <span data-ttu-id="ac80d-160">Propriété</span><span class="sxs-lookup"><span data-stu-id="ac80d-160">Property</span></span> | <span data-ttu-id="ac80d-161">Description</span><span class="sxs-lookup"><span data-stu-id="ac80d-161">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ac80d-162">Type</span><span class="sxs-lookup"><span data-stu-id="ac80d-162">Type</span></span> |<span data-ttu-id="ac80d-163">*Alert*</span><span class="sxs-lookup"><span data-stu-id="ac80d-163">*Alert*</span></span> |
| <span data-ttu-id="ac80d-164">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="ac80d-164">SourceSystem</span></span> |<span data-ttu-id="ac80d-165">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="ac80d-165">*Zabbix*</span></span> |
| <span data-ttu-id="ac80d-166">AlertName</span><span class="sxs-lookup"><span data-stu-id="ac80d-166">AlertName</span></span> | <span data-ttu-id="ac80d-167">Nom de l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="ac80d-167">Name of hello alert.</span></span> |
| <span data-ttu-id="ac80d-168">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="ac80d-168">AlertPriority</span></span> | <span data-ttu-id="ac80d-169">Niveau de gravité d’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="ac80d-169">Severity of hello alert.</span></span><br><br><span data-ttu-id="ac80d-170">non classée</span><span class="sxs-lookup"><span data-stu-id="ac80d-170">not classified</span></span><br><span data-ttu-id="ac80d-171">information</span><span class="sxs-lookup"><span data-stu-id="ac80d-171">information</span></span><br><span data-ttu-id="ac80d-172">Avertissement</span><span class="sxs-lookup"><span data-stu-id="ac80d-172">warning</span></span><br><span data-ttu-id="ac80d-173">average</span><span class="sxs-lookup"><span data-stu-id="ac80d-173">average</span></span><br><span data-ttu-id="ac80d-174">élevée</span><span class="sxs-lookup"><span data-stu-id="ac80d-174">high</span></span><br><span data-ttu-id="ac80d-175">urgence</span><span class="sxs-lookup"><span data-stu-id="ac80d-175">disaster</span></span>  |
| <span data-ttu-id="ac80d-176">AlertState</span><span class="sxs-lookup"><span data-stu-id="ac80d-176">AlertState</span></span> | <span data-ttu-id="ac80d-177">État d’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="ac80d-177">State of hello alert.</span></span><br><br><span data-ttu-id="ac80d-178">0 - état est toodate.</span><span class="sxs-lookup"><span data-stu-id="ac80d-178">0 - State is up toodate.</span></span><br><span data-ttu-id="ac80d-179">1 - l’état est inconnu.</span><span class="sxs-lookup"><span data-stu-id="ac80d-179">1 - State is unknown.</span></span>  |
| <span data-ttu-id="ac80d-180">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="ac80d-180">AlertTypeNumber</span></span> | <span data-ttu-id="ac80d-181">Indique si l’alerte peut générer plusieurs événements de problème.</span><span class="sxs-lookup"><span data-stu-id="ac80d-181">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="ac80d-182">0 - état est toodate.</span><span class="sxs-lookup"><span data-stu-id="ac80d-182">0 - State is up toodate.</span></span><br><span data-ttu-id="ac80d-183">1 - l’état est inconnu.</span><span class="sxs-lookup"><span data-stu-id="ac80d-183">1 - State is unknown.</span></span>    |
| <span data-ttu-id="ac80d-184">Commentaires</span><span class="sxs-lookup"><span data-stu-id="ac80d-184">Comments</span></span> | <span data-ttu-id="ac80d-185">Commentaires supplémentaires pour l’alerte.</span><span class="sxs-lookup"><span data-stu-id="ac80d-185">Additional comments for alert.</span></span> |
| <span data-ttu-id="ac80d-186">HostName</span><span class="sxs-lookup"><span data-stu-id="ac80d-186">HostName</span></span> | <span data-ttu-id="ac80d-187">Nom d’hôte hello qui a créé l’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="ac80d-187">Name of hello host that created hello alert.</span></span> |
| <span data-ttu-id="ac80d-188">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="ac80d-188">PriorityNumber</span></span> | <span data-ttu-id="ac80d-189">Valeur qui indique la gravité d’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="ac80d-189">Value indicating severity of hello alert.</span></span><br><br><span data-ttu-id="ac80d-190">0 - non classée</span><span class="sxs-lookup"><span data-stu-id="ac80d-190">0 - not classified</span></span><br><span data-ttu-id="ac80d-191">1 - information</span><span class="sxs-lookup"><span data-stu-id="ac80d-191">1 - information</span></span><br><span data-ttu-id="ac80d-192">2 - avertissement</span><span class="sxs-lookup"><span data-stu-id="ac80d-192">2 - warning</span></span><br><span data-ttu-id="ac80d-193">3 - moyenne</span><span class="sxs-lookup"><span data-stu-id="ac80d-193">3 - average</span></span><br><span data-ttu-id="ac80d-194">4 - élevée</span><span class="sxs-lookup"><span data-stu-id="ac80d-194">4 - high</span></span><br><span data-ttu-id="ac80d-195">5 - urgence</span><span class="sxs-lookup"><span data-stu-id="ac80d-195">5 - disaster</span></span> |
| <span data-ttu-id="ac80d-196">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="ac80d-196">TimeGenerated</span></span> |<span data-ttu-id="ac80d-197">Création de l’alerte hello date et heure.</span><span class="sxs-lookup"><span data-stu-id="ac80d-197">Date and time hello alert was created.</span></span> |
| <span data-ttu-id="ac80d-198">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="ac80d-198">TimeLastModified</span></span> |<span data-ttu-id="ac80d-199">Dernière modification de date et heure état hello d’alerte de hello.</span><span class="sxs-lookup"><span data-stu-id="ac80d-199">Date and time hello state of hello alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="ac80d-200">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ac80d-200">Next steps</span></span>
* <span data-ttu-id="ac80d-201">En savoir plus sur les [alertes](log-analytics-alerts.md) dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="ac80d-201">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="ac80d-202">En savoir plus sur [recherche de journal](log-analytics-log-searches.md) tooanalyze les données de salutation collectées à partir de sources de données et les solutions possibles.</span><span class="sxs-lookup"><span data-stu-id="ac80d-202">Learn about [log searches](log-analytics-log-searches.md) tooanalyze hello data collected from data sources and solutions.</span></span> 
