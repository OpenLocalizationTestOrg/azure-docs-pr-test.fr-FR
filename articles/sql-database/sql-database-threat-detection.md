---
title: "aaaThreat détection - base de données SQL Azure | Documents Microsoft"
description: "La détection des menaces détecte des activités de base de données anormales indiquant de base de données des toohello des menaces de sécurité potentielles."
services: sql-database
documentationcenter: 
author: rmatchoro
manager: jhubbard
editor: v-romcal
ms.assetid: b50d232a-4225-46ed-91e7-75288f55ee84
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/19/2017
ms.author: ronmat; ronitr
ms.openlocfilehash: 0879d20eff515a4e69358b5a98ceccf57fbd0ea2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-threat-detection"></a><span data-ttu-id="1e4e3-103">Détection de menaces pour les bases de données SQL</span><span class="sxs-lookup"><span data-stu-id="1e4e3-103">SQL Database Threat Detection</span></span>

<span data-ttu-id="1e4e3-104">Détection des menaces SQL détecte des activités anormales indiquant les bases de données tooaccess ou exploiter tentatives inhabituel et potentiellement dangereux.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-104">SQL Threat Detection detects anomalous activities indicating unusual and potentially harmful attempts tooaccess or exploit databases.</span></span>

## <a name="overview"></a><span data-ttu-id="1e4e3-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="1e4e3-105">Overview</span></span>

<span data-ttu-id="1e4e3-106">Détection des menaces SQL fournit une nouvelle couche de sécurité, ce qui permet aux clients toodetect et de répond toopotential menaces qu’ils se produisent en fournissant des alertes de sécurité sur les activités anormales.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-106">SQL Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span>  <span data-ttu-id="1e4e3-107">Les utilisateurs reçoivent une alerte en cas d’activités de base de données suspectes, de vulnérabilités potentielles, d’attaques par injection de code SQL et de modèles d’accès anormaux à la base de données.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-107">Users will receive an alert upon suspicious database activities, potential vulnerabilities, and SQL injection attacks, as well as anomalous database access patterns.</span></span> <span data-ttu-id="1e4e3-108">Alertes de détection des menaces SQL fournissent des détails d’activité suspecte et recommandent la mesure sur la façon de tooinvestigate et d’atténuer les menaces de hello.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-108">SQL Threat Detection alerts provide details of suspicious activity and recommend action on how tooinvestigate and mitigate hello threat.</span></span> <span data-ttu-id="1e4e3-109">Les utilisateurs peuvent Explorer à l’aide d’événements suspects hello [l’audit de base de données SQL](sql-database-auditing.md) toodetermine s’ils résultent d’une tentative de tooaccess, violation, ou exploiter les données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-109">Users can explore hello suspicious events using [SQL Database Auditing](sql-database-auditing.md) toodetermine if they result from an attempt tooaccess, breach, or exploit data in hello database.</span></span> <span data-ttu-id="1e4e3-110">La détection des menaces rend tooaddress simple potentiels menaces toohello base de données sans nécessité de hello toobe un expert en sécurité ou gérer des systèmes de surveillance de la sécurité avancée.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-110">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="1e4e3-111">Par exemple, injection SQL est un des hello Web application problèmes de sécurité courants sur hello Internet, les applications utilisées tooattack piloté par les données.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-111">For example, SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="1e4e3-112">Les attaquants profiter d’application vulnérabilités tooinject des instructions SQL malveillantes dans les champs d’entrée application, violation ou modification des données dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-112">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, breaching or modifying data in hello database.</span></span>

<span data-ttu-id="1e4e3-113">Détection des menaces SQL intègre les alertes avec [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), et chaque serveur de base de données SQL protégé sera facturée selon hello même prix en tant que couche Azure Security Center Standard, à 15 $/ nœud/mois, où chaque protégé SQL Serveur de base de données est comptabilisée comme un seul nœud.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-113">SQL Threat Detection integrates alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), and, each protected SQL Database server will be billed at hello same price as Azure Security Center Standard tier, at $15/node/month, where each protected SQL Database server is counted as one node.</span></span> <span data-ttu-id="1e4e3-114">Nous vous invitons tootry son évolution horizontale pendant 60 jours pour le libérer.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-114">We invite you tootry it out for 60 days for free.</span></span> 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="1e4e3-115">Configurer la détection des menaces pour votre base de données Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="1e4e3-115">Set up threat detection for your database in hello Azure portal</span></span>
1. <span data-ttu-id="1e4e3-116">Lancez hello Azure portail à [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1e4e3-116">Launch hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1e4e3-117">Accédez à panneau de configuration de toohello de base de données SQL toomonitor de hello.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-117">Navigate toohello configuration blade of hello SQL Database you want toomonitor.</span></span> <span data-ttu-id="1e4e3-118">Dans le panneau des paramètres de hello, sélectionnez **audit et la détection des menaces**.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> 
    <span data-ttu-id="1e4e3-119">![Volet de navigation][1]</span><span class="sxs-lookup"><span data-stu-id="1e4e3-119">![Navigation pane][1]</span></span>
3. <span data-ttu-id="1e4e3-120">Bonjour **audit et la détection des menaces** activer Panneau de configuration **ON** l’audit, qui affiche les paramètres de détection de menace hello.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** Auditing, which will display hello threat detection settings.</span></span>
  
    ![Volet de navigation][2]
4. <span data-ttu-id="1e4e3-122">**Activez** la détection des menaces.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="1e4e3-123">Configurez la liste hello d’adresses de messagerie qui recevront les alertes de sécurité lors de la détection des activités anormales base de données.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-123">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>
6. <span data-ttu-id="1e4e3-124">Cliquez sur **enregistrer** Bonjour **détection d’audit et de menaces** panneau toosave hello nouveaux ou mis à jour l’audit et paramètres de la détection.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-124">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection settings.</span></span>
       
    ![Volet de navigation][3]

## <a name="set-up-threat-detection-using-powershell"></a><span data-ttu-id="1e4e3-126">Configurer la détection des menaces avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e4e3-126">Set up threat detection using PowerShell</span></span>

<span data-ttu-id="1e4e3-127">Pour obtenir un exemple de script, consultez [Configurer l’audit et la détection des menaces avec PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1e4e3-127">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="1e4e3-128">Explorer les activités anormales sur la base de données en cas de détection d’un événement suspect</span><span class="sxs-lookup"><span data-stu-id="1e4e3-128">Explore anomalous database activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="1e4e3-129">Vous recevrez une notification par courrier électronique lorsque des activités anormales sont détectées au niveau de la base de données.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-129">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="1e4e3-130">messagerie de Hello fournit des informations sur les événements de sécurité anormaux hello, y compris la nature hello d’activités anormales de hello, nom de la base de données, nom du serveur, nom de l’application et heure de l’événement hello.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-130">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name, application name, and hello event time.</span></span> <span data-ttu-id="1e4e3-131">En outre, par courrier électronique hello fournit des informations sur les causes possibles et recommandé actions tooinvestigate et atténuer la base de données du toohello de menaces potentielles hello.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-131">In addition, hello email will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
     
    ![Volet de navigation][4]
2. <span data-ttu-id="1e4e3-133">alerte par courrier électronique de Hello comprend un journal d’Audit SQL de toohello lien direct.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-133">hello email alert includes a direct link toohello SQL Audit log.</span></span> <span data-ttu-id="1e4e3-134">En cliquant sur cette hello lance de lien Azure portal et ouvre hello SQL les enregistrements d’Audit en temps hello d’événement de suspectes hello.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-134">Clicking on this link launches hello Azure portal and opens hello SQL Audit records around hello time of hello suspicious event.</span></span> <span data-ttu-id="1e4e3-135">Cliquez sur un tooview d’enregistrement d’audit plus de détails sur les activités de base de données suspecte hello, rend plus faciles instructions SQL toofind hello qui ont été exécutées (nom de l’utilisateur, qu’ils a et à quel moment) et déterminer si les événements hello était légitime ou malveillant (par exemple, application injection de tooSQL une vulnérabilité a été exploitée, un utilisateur une violation des données sensibles, etc.).</span><span class="sxs-lookup"><span data-stu-id="1e4e3-135">Click on an audit record tooview more details on hello suspicious database activities, making it easier toofind hello SQL statements that were executed (who accessed, what they did and when) and determine if hello event was legitimate or malicious (e.g. application vulnerability tooSQL injection was exploited, someone breached sensitive data, etc.).</span></span><br/><span data-ttu-id="1e4e3-136">
   ![Volet de navigation][5]</span><span class="sxs-lookup"><span data-stu-id="1e4e3-136">
![Navigation pane][5]</span></span>


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="1e4e3-137">Explorer les alertes de détection des menaces pour votre base de données Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="1e4e3-137">Explore threat detection alerts for your database in hello Azure portal</span></span>

<span data-ttu-id="1e4e3-138">SQL Database Threat Detection intègre ses alertes avec [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span><span class="sxs-lookup"><span data-stu-id="1e4e3-138">SQL Database Threat Detection integrates its alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span></span> <span data-ttu-id="1e4e3-139">Une vignette de sécurité SQL dynamique dans le panneau de base de données hello dans l’état de hello assure le suivi du portail Azure hello de menaces actives.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-139">A live SQL security tile within hello database blade in hello Azure portal tracks hello status of active threats.</span></span> 

   ![Volet de navigation][6]
   
1. <span data-ttu-id="1e4e3-141">En cliquant sur la vignette de sécurité SQL hello lance le panneau des alertes Azure Security Center hello et fournit une vue d’ensemble de menaces SQL actives détecté sur la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-141">Clicking on hello SQL security tile launches hello Azure Security Center alerts blade and provides an overview of active SQL threats detected on hello database.</span></span> 

  ![Volet de navigation][7]

2. <span data-ttu-id="1e4e3-143">En cliquant sur une alerte spécifique, vous obtenez des détails supplémentaires et des actions permettant d’examiner cette menace et d’atténuer les menaces futures.</span><span class="sxs-lookup"><span data-stu-id="1e4e3-143">Clicking on a specific alert provides additional details and actions for investigating this threat and remediating future threats.</span></span>

  ![Volet de navigation][8]


## <a name="next-steps"></a><span data-ttu-id="1e4e3-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1e4e3-145">Next steps</span></span>

* <span data-ttu-id="1e4e3-146">En savoir plus sur la détection des menaces, visitez hello [blog Azure](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span><span class="sxs-lookup"><span data-stu-id="1e4e3-146">Learn more about Threat Detection, visit hello [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span></span> 
* <span data-ttu-id="1e4e3-147">En savoir plus sur [Audit Azure SQL Database](sql-database-auditing.md)</span><span class="sxs-lookup"><span data-stu-id="1e4e3-147">Learn more about [Azure SQL Database Auditing](sql-database-auditing.md)</span></span>
* <span data-ttu-id="1e4e3-148">En savoir plus sur [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span><span class="sxs-lookup"><span data-stu-id="1e4e3-148">Learn more about [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span></span>
* <span data-ttu-id="1e4e3-149">Pour plus d’informations sur la tarification, consultez hello [page de tarification de base de données SQL](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="1e4e3-149">For more details on pricing, please see hello [SQL Database Pricing page](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span></span>  
* <span data-ttu-id="1e4e3-150">Pour obtenir un exemple de script PowerShell, consultez [Configurer l’audit et la détection des menaces avec PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1e4e3-150">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span></span>



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


