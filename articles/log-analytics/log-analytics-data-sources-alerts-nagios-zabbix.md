---
title: "Collecte d’alertes Nagios et Zabbix dans OMS Log Analytics | Documents Microsoft"
description: "Nagios et Zabbix sont des outils de surveillance open source. Vous pouvez collecter des alertes à partir de ces outils dans Log Analytics afin de les analyser avec des alertes provenant d’autres sources.  Cet article décrit comment configurer l’agent OMS pour Linux pour la collecte d’alertes à partir de ces systèmes."
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
ms.openlocfilehash: 0b64c32e1031e704d50aab0b38eaea41e27d134b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="collect-alerts-from-nagios-and-zabbix-in-log-analytics-from-oms-agent-for-linux"></a><span data-ttu-id="07a9d-105">Collecte d’alertes à partir de Nagios et Zabbix dans Log Analytics à partir de l’agent OMS pour Linux</span><span class="sxs-lookup"><span data-stu-id="07a9d-105">Collect alerts from Nagios and Zabbix in Log Analytics from OMS Agent for Linux</span></span> 
<span data-ttu-id="07a9d-106">[Nagios](https://www.nagios.org/) et [Zabbix](http://www.zabbix.com/) sont des outils de surveillance open source.</span><span class="sxs-lookup"><span data-stu-id="07a9d-106">[Nagios](https://www.nagios.org/) and [Zabbix](http://www.zabbix.com/) are open source monitoring tools.</span></span>  <span data-ttu-id="07a9d-107">Vous pouvez collecter des alertes à partir de ces outils dans Log Analytics afin de les analyser avec des [alertes provenant d’autres sources](log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="07a9d-107">You can collect alerts from these tools into Log Analytics in order to analyze them along with [alerts from other sources](log-analytics-alerts.md).</span></span>  <span data-ttu-id="07a9d-108">Cet article décrit comment configurer l’agent OMS pour Linux pour la collecte d’alertes à partir de ces systèmes.</span><span class="sxs-lookup"><span data-stu-id="07a9d-108">This article describes how to configure the OMS Agent for Linux to collect alerts from these systems.</span></span>
 
## <a name="configure-alert-collection"></a><span data-ttu-id="07a9d-109">Configuration de la collecte d’alertes</span><span class="sxs-lookup"><span data-stu-id="07a9d-109">Configure alert collection</span></span>

### <a name="configuring-nagios-alert-collection"></a><span data-ttu-id="07a9d-110">Configuration de la collecte d’alertes Nagios</span><span class="sxs-lookup"><span data-stu-id="07a9d-110">Configuring Nagios alert collection</span></span>
<span data-ttu-id="07a9d-111">Procédez comme suit sur le serveur Nagios pour collecter les alertes.</span><span class="sxs-lookup"><span data-stu-id="07a9d-111">Perform the following steps on the Nagios server to collect alerts.</span></span>

1. <span data-ttu-id="07a9d-112">Octroyez à l’utilisateur **omsagent** l’accès en lecture au fichier journal Nagios (par exemple, `/var/log/nagios/nagios.log`).</span><span class="sxs-lookup"><span data-stu-id="07a9d-112">Grant the user **omsagent** read access to the Nagios log file (i.e. `/var/log/nagios/nagios.log`).</span></span> <span data-ttu-id="07a9d-113">Si le fichier nagios.log appartient au groupe `nagios`, vous pouvez ajouter l’utilisateur **omsagent** au groupe **nagios**.</span><span class="sxs-lookup"><span data-stu-id="07a9d-113">Assuming the nagios.log file is owned by the group `nagios`, you can add the user **omsagent** to the **nagios** group.</span></span> 

    <span data-ttu-id="07a9d-114">sudo usermod -a -G nagios omsagent</span><span class="sxs-lookup"><span data-stu-id="07a9d-114">sudo usermod -a -G nagios omsagent</span></span>

2.  <span data-ttu-id="07a9d-115">Modifiez le fichier de configuration dans (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="07a9d-115">Modify the configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="07a9d-116">Vérifiez que les entrées suivantes sont présentes et non mises en commentaire :</span><span class="sxs-lookup"><span data-stu-id="07a9d-116">Ensure the following entries are present and not commented out:</span></span>  

        <source>  
          type tail  
          #Update path to point to your nagios.log  
          path /var/log/nagios/nagios.log  
          format none  
          tag oms.nagios  
        </source>  
      
        <filter oms.nagios>  
          type filter_nagios_log  
        </filter>  

3. <span data-ttu-id="07a9d-117">Redémarrez le démon omsagent</span><span class="sxs-lookup"><span data-stu-id="07a9d-117">Restart the omsagent daemon</span></span>

    ```
    sudo sh /opt/microsoft/omsagent/bin/service_control restart
    ```

### <a name="configuring-zabbix-alert-collection"></a><span data-ttu-id="07a9d-118">Configuration de la collecte d’alertes Zabbix</span><span class="sxs-lookup"><span data-stu-id="07a9d-118">Configuring Zabbix alert collection</span></span>
<span data-ttu-id="07a9d-119">Pour collecter les alertes à partir d’un serveur Zabbix, vous devez indiquer un utilisateur et un mot de passe en *texte clair*.</span><span class="sxs-lookup"><span data-stu-id="07a9d-119">To collect alerts from a Zabbix server, you need to specify a user and password in *clear text*.</span></span> <span data-ttu-id="07a9d-120">Ce n’est pas l’idéal, mais nous vous recommandons de créer l’utilisateur et d’accorder des autorisations pour surveiller onlu.</span><span class="sxs-lookup"><span data-stu-id="07a9d-120">This is not ideal, but we recommend that you create the user and grant permissions to monitor onlu.</span></span>

<span data-ttu-id="07a9d-121">Procédez comme suit sur le serveur Nagios pour collecter les alertes.</span><span class="sxs-lookup"><span data-stu-id="07a9d-121">Perform the following steps on the Nagios server to collect alerts.</span></span>

1. <span data-ttu-id="07a9d-122">Modifiez le fichier de configuration dans (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span><span class="sxs-lookup"><span data-stu-id="07a9d-122">Modify the configuration file at (`/etc/opt/microsoft/omsagent/<workspace id>/conf/omsagent.conf`).</span></span> <span data-ttu-id="07a9d-123">Vérifiez que les entrées suivantes sont présentes et non commentées.</span><span class="sxs-lookup"><span data-stu-id="07a9d-123">Ensure the following entries are present and not commented out.</span></span>  <span data-ttu-id="07a9d-124">Remplacez le nom d’utilisateur et le mot de passe par des valeurs pour votre environnement Zabbix.</span><span class="sxs-lookup"><span data-stu-id="07a9d-124">Change the user name and password to values for your Zabbix environment.</span></span>

        <source>
         type zabbix_alerts
         run_interval 1m
         tag oms.zabbix
         zabbix_url http://localhost/zabbix/api_jsonrpc.php
         zabbix_username Admin
         zabbix_password zabbix
        </source>

2. <span data-ttu-id="07a9d-125">Redémarrez le démon omsagent</span><span class="sxs-lookup"><span data-stu-id="07a9d-125">Restart the omsagent daemon</span></span>

    <span data-ttu-id="07a9d-126">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span><span class="sxs-lookup"><span data-stu-id="07a9d-126">sudo sh /opt/microsoft/omsagent/bin/service_control restart</span></span>


## <a name="alert-records"></a><span data-ttu-id="07a9d-127">Enregistrements d’alerte</span><span class="sxs-lookup"><span data-stu-id="07a9d-127">Alert records</span></span>
<span data-ttu-id="07a9d-128">Vous pouvez récupérer les enregistrements d’alerte de Nagios et Zabbix à l’aide des [recherches dans les journaux](log-analytics-log-searches.md) dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="07a9d-128">You can retrieve alert records from Nagios and Zabbix using [log searches](log-analytics-log-searches.md) in Log Analytics.</span></span>

### <a name="nagios-alert-records"></a><span data-ttu-id="07a9d-129">Enregistrements d’alerte Nagios</span><span class="sxs-lookup"><span data-stu-id="07a9d-129">Nagios Alert records</span></span>

<span data-ttu-id="07a9d-130">Pour les enregistrements d’alerte collectés par Nagios, le **type** est **Alerte** et la valeur **SourceSystem** est **Nagios**.</span><span class="sxs-lookup"><span data-stu-id="07a9d-130">Alert records collected by Nagios have a **Type** of **Alert** and a **SourceSystem** of **Nagios**.</span></span>  <span data-ttu-id="07a9d-131">Les propriétés des enregistrements sont décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="07a9d-131">They have the properties in the following table.</span></span>

| <span data-ttu-id="07a9d-132">Propriété</span><span class="sxs-lookup"><span data-stu-id="07a9d-132">Property</span></span> | <span data-ttu-id="07a9d-133">Description</span><span class="sxs-lookup"><span data-stu-id="07a9d-133">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="07a9d-134">Type</span><span class="sxs-lookup"><span data-stu-id="07a9d-134">Type</span></span> |<span data-ttu-id="07a9d-135">*Alert*</span><span class="sxs-lookup"><span data-stu-id="07a9d-135">*Alert*</span></span> |
| <span data-ttu-id="07a9d-136">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="07a9d-136">SourceSystem</span></span> |<span data-ttu-id="07a9d-137">*Nagios*</span><span class="sxs-lookup"><span data-stu-id="07a9d-137">*Nagios*</span></span> |
| <span data-ttu-id="07a9d-138">AlertName</span><span class="sxs-lookup"><span data-stu-id="07a9d-138">AlertName</span></span> |<span data-ttu-id="07a9d-139">Nom de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="07a9d-139">Name of the alert.</span></span> |
| <span data-ttu-id="07a9d-140">AlertDescription</span><span class="sxs-lookup"><span data-stu-id="07a9d-140">AlertDescription</span></span> | <span data-ttu-id="07a9d-141">Description de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="07a9d-141">Description of the alert.</span></span> |
| <span data-ttu-id="07a9d-142">AlertState</span><span class="sxs-lookup"><span data-stu-id="07a9d-142">AlertState</span></span> | <span data-ttu-id="07a9d-143">État du service ou de l’hôte.</span><span class="sxs-lookup"><span data-stu-id="07a9d-143">Status of the service or host.</span></span><br><br><span data-ttu-id="07a9d-144">OK</span><span class="sxs-lookup"><span data-stu-id="07a9d-144">OK</span></span><br><span data-ttu-id="07a9d-145">AVERTISSEMENT</span><span class="sxs-lookup"><span data-stu-id="07a9d-145">WARNING</span></span><br><span data-ttu-id="07a9d-146">ACTIF</span><span class="sxs-lookup"><span data-stu-id="07a9d-146">UP</span></span><br><span data-ttu-id="07a9d-147">INACTIF</span><span class="sxs-lookup"><span data-stu-id="07a9d-147">DOWN</span></span> |
| <span data-ttu-id="07a9d-148">HostName</span><span class="sxs-lookup"><span data-stu-id="07a9d-148">HostName</span></span> | <span data-ttu-id="07a9d-149">Nom de l’hôte qui a créé l’alerte.</span><span class="sxs-lookup"><span data-stu-id="07a9d-149">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="07a9d-150">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="07a9d-150">PriorityNumber</span></span> | <span data-ttu-id="07a9d-151">Niveau de priorité de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="07a9d-151">Priority level of the alert.</span></span> |
| <span data-ttu-id="07a9d-152">StateType</span><span class="sxs-lookup"><span data-stu-id="07a9d-152">StateType</span></span> | <span data-ttu-id="07a9d-153">Type d’état de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="07a9d-153">The type of state of the alert.</span></span><br><br><span data-ttu-id="07a9d-154">LÉGER : problème qui n’a pas été revérifié.</span><span class="sxs-lookup"><span data-stu-id="07a9d-154">SOFT - Issue that has not been rechecked.</span></span><br><span data-ttu-id="07a9d-155">URGENT : problème qui a été revérifié un nombre spécifié de fois.</span><span class="sxs-lookup"><span data-stu-id="07a9d-155">HARD - Issue that has been rechecked a specified number of times.</span></span>  |
| <span data-ttu-id="07a9d-156">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="07a9d-156">TimeGenerated</span></span> |<span data-ttu-id="07a9d-157">Date et heure de la création de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="07a9d-157">Date and time the alert was created.</span></span> |


### <a name="zabbix-alert-records"></a><span data-ttu-id="07a9d-158">Enregistrements d’alerte Zabbix</span><span class="sxs-lookup"><span data-stu-id="07a9d-158">Zabbix alert records</span></span>
<span data-ttu-id="07a9d-159">Pour les enregistrements d’alerte collectés par Zabbix, le **type** est **Alerte** et la valeur **SourceSystem** est **Zabbix**.</span><span class="sxs-lookup"><span data-stu-id="07a9d-159">Alert records collected by Zabbix have a **Type** of **Alert** and a **SourceSystem** of **Zabbix**.</span></span>  <span data-ttu-id="07a9d-160">Les propriétés des enregistrements sont décrites dans le tableau suivant.</span><span class="sxs-lookup"><span data-stu-id="07a9d-160">They have the properties in the following table.</span></span>

| <span data-ttu-id="07a9d-161">Propriété</span><span class="sxs-lookup"><span data-stu-id="07a9d-161">Property</span></span> | <span data-ttu-id="07a9d-162">Description</span><span class="sxs-lookup"><span data-stu-id="07a9d-162">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="07a9d-163">Type</span><span class="sxs-lookup"><span data-stu-id="07a9d-163">Type</span></span> |<span data-ttu-id="07a9d-164">*Alert*</span><span class="sxs-lookup"><span data-stu-id="07a9d-164">*Alert*</span></span> |
| <span data-ttu-id="07a9d-165">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="07a9d-165">SourceSystem</span></span> |<span data-ttu-id="07a9d-166">*Zabbix*</span><span class="sxs-lookup"><span data-stu-id="07a9d-166">*Zabbix*</span></span> |
| <span data-ttu-id="07a9d-167">AlertName</span><span class="sxs-lookup"><span data-stu-id="07a9d-167">AlertName</span></span> | <span data-ttu-id="07a9d-168">Nom de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="07a9d-168">Name of the alert.</span></span> |
| <span data-ttu-id="07a9d-169">AlertPriority</span><span class="sxs-lookup"><span data-stu-id="07a9d-169">AlertPriority</span></span> | <span data-ttu-id="07a9d-170">Gravité de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="07a9d-170">Severity of the alert.</span></span><br><br><span data-ttu-id="07a9d-171">non classée</span><span class="sxs-lookup"><span data-stu-id="07a9d-171">not classified</span></span><br><span data-ttu-id="07a9d-172">information</span><span class="sxs-lookup"><span data-stu-id="07a9d-172">information</span></span><br><span data-ttu-id="07a9d-173">Avertissement</span><span class="sxs-lookup"><span data-stu-id="07a9d-173">warning</span></span><br><span data-ttu-id="07a9d-174">average</span><span class="sxs-lookup"><span data-stu-id="07a9d-174">average</span></span><br><span data-ttu-id="07a9d-175">élevée</span><span class="sxs-lookup"><span data-stu-id="07a9d-175">high</span></span><br><span data-ttu-id="07a9d-176">urgence</span><span class="sxs-lookup"><span data-stu-id="07a9d-176">disaster</span></span>  |
| <span data-ttu-id="07a9d-177">AlertState</span><span class="sxs-lookup"><span data-stu-id="07a9d-177">AlertState</span></span> | <span data-ttu-id="07a9d-178">État de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="07a9d-178">State of the alert.</span></span><br><br><span data-ttu-id="07a9d-179">0 - l’état est à jour.</span><span class="sxs-lookup"><span data-stu-id="07a9d-179">0 - State is up to date.</span></span><br><span data-ttu-id="07a9d-180">1 - l’état est inconnu.</span><span class="sxs-lookup"><span data-stu-id="07a9d-180">1 - State is unknown.</span></span>  |
| <span data-ttu-id="07a9d-181">AlertTypeNumber</span><span class="sxs-lookup"><span data-stu-id="07a9d-181">AlertTypeNumber</span></span> | <span data-ttu-id="07a9d-182">Indique si l’alerte peut générer plusieurs événements de problème.</span><span class="sxs-lookup"><span data-stu-id="07a9d-182">Specifies whether alert can generate multiple problem events.</span></span><br><br><span data-ttu-id="07a9d-183">0 - l’état est à jour.</span><span class="sxs-lookup"><span data-stu-id="07a9d-183">0 - State is up to date.</span></span><br><span data-ttu-id="07a9d-184">1 - l’état est inconnu.</span><span class="sxs-lookup"><span data-stu-id="07a9d-184">1 - State is unknown.</span></span>    |
| <span data-ttu-id="07a9d-185">Commentaires</span><span class="sxs-lookup"><span data-stu-id="07a9d-185">Comments</span></span> | <span data-ttu-id="07a9d-186">Commentaires supplémentaires pour l’alerte.</span><span class="sxs-lookup"><span data-stu-id="07a9d-186">Additional comments for alert.</span></span> |
| <span data-ttu-id="07a9d-187">HostName</span><span class="sxs-lookup"><span data-stu-id="07a9d-187">HostName</span></span> | <span data-ttu-id="07a9d-188">Nom de l’hôte qui a créé l’alerte.</span><span class="sxs-lookup"><span data-stu-id="07a9d-188">Name of the host that created the alert.</span></span> |
| <span data-ttu-id="07a9d-189">PriorityNumber</span><span class="sxs-lookup"><span data-stu-id="07a9d-189">PriorityNumber</span></span> | <span data-ttu-id="07a9d-190">Valeur qui indique la gravité de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="07a9d-190">Value indicating severity of the alert.</span></span><br><br><span data-ttu-id="07a9d-191">0 - non classée</span><span class="sxs-lookup"><span data-stu-id="07a9d-191">0 - not classified</span></span><br><span data-ttu-id="07a9d-192">1 - information</span><span class="sxs-lookup"><span data-stu-id="07a9d-192">1 - information</span></span><br><span data-ttu-id="07a9d-193">2 - avertissement</span><span class="sxs-lookup"><span data-stu-id="07a9d-193">2 - warning</span></span><br><span data-ttu-id="07a9d-194">3 - moyenne</span><span class="sxs-lookup"><span data-stu-id="07a9d-194">3 - average</span></span><br><span data-ttu-id="07a9d-195">4 - élevée</span><span class="sxs-lookup"><span data-stu-id="07a9d-195">4 - high</span></span><br><span data-ttu-id="07a9d-196">5 - urgence</span><span class="sxs-lookup"><span data-stu-id="07a9d-196">5 - disaster</span></span> |
| <span data-ttu-id="07a9d-197">TimeGenerated</span><span class="sxs-lookup"><span data-stu-id="07a9d-197">TimeGenerated</span></span> |<span data-ttu-id="07a9d-198">Date et heure de la création de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="07a9d-198">Date and time the alert was created.</span></span> |
| <span data-ttu-id="07a9d-199">TimeLastModified</span><span class="sxs-lookup"><span data-stu-id="07a9d-199">TimeLastModified</span></span> |<span data-ttu-id="07a9d-200">Date et heure de la dernière modification de l’état de l’alerte.</span><span class="sxs-lookup"><span data-stu-id="07a9d-200">Date and time the state of the alert was last changed.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="07a9d-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="07a9d-201">Next steps</span></span>
* <span data-ttu-id="07a9d-202">En savoir plus sur les [alertes](log-analytics-alerts.md) dans Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="07a9d-202">Learn about [alerts](log-analytics-alerts.md) in Log Analytics.</span></span>
* <span data-ttu-id="07a9d-203">En savoir plus sur les [recherches de journal](log-analytics-log-searches.md) pour analyser les données collectées dans des sources de données et des solutions.</span><span class="sxs-lookup"><span data-stu-id="07a9d-203">Learn about [log searches](log-analytics-log-searches.md) to analyze the data collected from data sources and solutions.</span></span> 
