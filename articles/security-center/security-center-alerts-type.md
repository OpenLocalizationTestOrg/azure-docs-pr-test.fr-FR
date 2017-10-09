---
title: "aaaSecurity des alertes par type dans le centre de sécurité Azure | Documents Microsoft"
description: "Cet article décrit hello différents types d’alertes de sécurité disponibles dans le centre de sécurité Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b3e7b4bc-5ee0-4280-ad78-f49998675af1
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: yurid
ms.openlocfilehash: ee69cb9035c35f5bc2ed51f9b9d6f29486b4caf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-security-alerts-in-azure-security-center"></a>Présentation des alertes de sécurité dans Azure Security Center
Cet article vous aide à toounderstand hello différents types d’alertes de sécurité et informations connexes qui sont disponibles dans le centre de sécurité Azure. Pour plus d’informations sur comment toomanage alertes et des incidents, consultez [toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md).

> [!NOTE]
> tooset des détections avancées, mise à niveau tooAzure Security Center Standard. Une version d’évaluation gratuite de 60 jours est disponible. tooupgrade, sélectionnez **niveau tarifaire** Bonjour [stratégie de sécurité](security-center-policies.md). toolearn, voir hello [page de tarification](https://azure.microsoft.com/pricing/details/security-center/).
>

## <a name="what-type-of-alerts-are-available"></a>Quels types d’alertes sont disponibles ?
Centre de sécurité Azure utilise divers [des fonctionnalités de détection](security-center-detection-capabilities.md) tooalert clients toopotential attaques ciblant leurs environnements. Ces alertes contiennent des informations importantes sur hello ce qui a déclenché hello alerte, les ressources hello ciblés et hello source d’attaque de hello. informations Hello incluses dans une alerte varient en fonction de type hello de menace de hello toodetect analytique utilisé. Les incidents sont également susceptibles de contenir des informations contextuelles supplémentaires qui peuvent se révéler utiles lors de l’étude d’une menace.  Cet article fournit des informations sur hello les types d’alerte suivants :

* Analyse comportementale de la machine virtuelle (VMBA)
* Analyse du réseau
* Analyse des ressources
* Informations contextuelles

## <a name="virtual-machine-behavioral-analysis"></a>Analyse comportementale de la machine virtuelle
Centre de sécurité Azure peuvent utiliser des ressources de tooidentify compromis d’analytique comportementale basées sur l’analyse des journaux des événements de machine virtuelle. Par exemple, les événements de création de processus et les événements de connexion. En outre, il est corrélation avec les autres toocheck signaux pour prendre en charge de la preuve d’une campagne généralisée.

> [!NOTE]
> Pour plus d’informations sur le fonctionnement des fonctionnalités de détection de Security Center, voir [Fonctionnalités de détection d’Azure Security Center](security-center-detection-capabilities.md).
>

### <a name="crash-analysis"></a>Analyse des incidents
Analyse de mémoire de vidage sur incident est un toodetect de la méthode utilisée sophistiquées contre les programmes malveillants qui sont en mesure de tooevade de solutions de sécurité traditionnels. Essayez de différentes formes de programmes malveillants chance de hello tooreduce de détectées par les produits antivirus en écrivant des toodisk jamais, ou en chiffrant les composants logiciels écrits toodisk. Cela rend toodetect difficile de hello contre les programmes malveillants à l’aide des approches de logiciel anti-programme malveillant traditionnel. Toutefois, ce type de programme malveillant peut être détecté à l’aide de l’analyse de mémoire, car les programmes malveillants doivent conserver les traces en mémoire dans l’ordre toofunction.

Lorsque le logiciel tombe en panne, un vidage sur incident capture une partie de la mémoire lors de pannes de hello hello. panne de Hello peut être dû par contre les programmes malveillants, les généraux de l’application ou les problèmes liés au système. En analysant la mémoire hello dans le vidage sur incident de hello, centre de sécurité peut détecter des techniques utilisées tooexploit vulnérabilités dans le logiciel, accéder aux données confidentielles et subrepticement persistantes au sein d’un ordinateur compromis. Cela est établie avec toohosts d’impact sur les performances minimale hello l’analyse est effectuée par hello de fin dans le centre de sécurité.

Hello champs qui suivent est toohello incident vidage alerte exemples courants qui s’affichent plus loin dans cet article :

* Fichier de vidage : Le nom de fichier de vidage sur incident hello.
* PROCESSNAME : Nom Hello bloqué des processus.
* PROCESSVERSION : Version Hello bloqué des processus.

### <a name="shellcode-discovered"></a>Shellcode détecté
Code shell est la charge utile hello exécutée une fois les programmes malveillants à exploiter une faille du logiciel. Cette alerte indique que l’analyse de vidage sur incident a détecté du code exécutable présentant un comportement souvent associé à des charges utiles malveillantes. Bien que des logiciels non malveillants puissent présenter aussi ce comportement, il n’est pas typique des pratiques de développement logiciel normales.

exemple d’alerte Hello code shell fournit hello suivant champ supplémentaire :

* : Hello adresse en mémoire de code de shell hello.

Voici un exemple de ce type d’alerte :

![Alerte de shellcode](./media/security-center-alerts-type/security-center-alerts-type-fig2.png)

### <a name="module-hijacking-discovered"></a>Détournement de module détecté
Windows utilise les bibliothèques de liens dynamiques (DLL) tooallow logiciel tooutilize Windows système des fonctionnalités communes. Détournement de DLL se produit lorsque contre les programmes malveillants hello DLL charge ordre tooload malveillant charges utiles dans la mémoire, où le code arbitraire peut être exécuté. Cette alerte indique qu’analyse de vidage sur incident hello a détecté un module portant le même nom qui est chargé à partir de deux chemins d’accès différents. Un des chemins d’accès hello chargé provienne d’un emplacement de binaires système Windows commun.

Les développeurs de logiciels légitimes parfois modifier d’ordre de chargement DLL hello pour des raisons non malveillantes, telles que l’instrumentation, extension hello du système d’exploitation Windows ou étendre une application Windows. toohelp différencier les modifications malveillants et potentiellement sans gravité toohello ordre de chargement DLL, Azure Security Center vérifie si un module chargé est conforme profil suspecte de tooa. résultat de Hello de cette vérification est indiqué par le champ de « SIGNATURE » hello d’alerte de hello et est répercutée dans gravité hello d’alerte de hello, description de l’alerte et les étapes de l’alerte de mise à jour. tooresearch si le module de hello est légitime ou malveillantes, analyser hello sur la copie du disque de hello détournement de module. Par exemple, vous pouvez vérifier la signature numérique du fichier hello ou exécuter une analyse antivirus.

En outre toohello champs courants décrits dans la section précédente « code shell découverte » de hello, cette alerte fournit hello champs qui suivent :

* SIGNATURE : Indique si hello détournement de module est conforme à profil de comportement suspect tooa.
* HIJACKEDMODULE : nom hello Hello accès non autorisé au module de système de Windows.
* HIJACKEDMODULEPATH : chemin d’accès de hello Hello accès non autorisé au module de système de Windows.
* HIJACKINGMODULEPATH : chemin d’accès hello du module de détournement hello.

Voici un exemple de ce type d’alerte :

![Alerte de détournement de module](./media/security-center-alerts-type/security-center-alerts-type-fig3.png)

### <a name="masquerading-windows-module-detected"></a>Usurpation d’identité de module Windows détectée
Programme malveillant peut utiliser des noms communs des fichiers binaires du système Windows (par exemple, SVCHOST. (EXE) ou des modules (par exemple, NTDLL. DLL) trop*blend* et masquer la nature hello des logiciels malveillants de hello des administrateurs système. Cette alerte indique qu’analyse de vidage sur incident hello détecte que ce fichier de vidage sur incident hello contient des modules qui utilisent des noms de module de système de Windows, mais ne répondent pas à d’autres critères typiques des modules de Windows. Analyse hello sur la copie du disque du module d’usurpation d’identité hello peut fournir plus d’informations sur la nature de légitimes ou malveillantes hello de ce module. L’analyse peut inclure les opérations suivantes :

* Vérifiez que ce fichier hello en question est fourni en tant que partie d’un package de logiciels légitimes.
* Vérifier la signature numérique du fichier hello.
* Exécuter une analyse antivirus sur le fichier de hello.

En outre toohello champs courants décrits précédemment dans la section de « Code shell découvert » hello, cette alerte fournit hello suivant des champs supplémentaires :

* Détails : Décrit si les métadonnées du module hello sont valide, et indique si le module de hello a été chargé à partir d’un chemin d’accès système.
* NOM : nom de hello du module de Windows hello usurpation d’identité.
* Chemin d’accès : hello chemin d’accès toohello usurpation d’identité Windows module.

Cette alerte est également extrait et affiche certains champs à partir de l’en-tête PE du module hello, tels que « Somme de contrôle » et « TIMESTAMP ». Ces champs sont uniquement affichées si les champs de hello sont présents dans le module de hello. Consultez hello [spécification Microsoft PE et COFF](https://msdn.microsoft.com/windows/hardware/gg463119.aspx) pour plus d’informations sur ces champs.

Voici un exemple de ce type d’alerte :

![Alerte d’usurpation d’identité Windows](./media/security-center-alerts-type/security-center-alerts-type-fig4.png)

### <a name="modified-system-binary-discovered"></a>Fichier binaire système modifié détecté
Les programmes malveillants peuvent modifier des binaires système principaux dans les données d’accès ordre toocovertly ou subrepticement sont conservées sur un système infecté. Cette alerte indique qu’analyse de vidage sur incident hello a détecté que les fichiers binaires du système d’exploitation Windows core ont été modifiés en mémoire ou sur disque.

Les développeurs de logiciels légitimes modifient parfois des modules système dans la mémoire pour des raisons non malveillantes, par exemple avec Detours ou pour la compatibilité des applications. toohelp distinguer les modules malveillants et potentiellement légitimes, Azure Security Center vérifie si les module modifié de hello est conforme profil suspecte de tooa. résultat de Hello de cette vérification est indiqué par gravité hello d’alerte de hello, description de l’alerte et les étapes de l’alerte de mise à jour.

En outre toohello champs courants décrits précédemment dans la section de « Code shell découvert » hello, cette alerte fournit hello suivant des champs supplémentaires :

* Nom du module : Nom du hello modifié système binaire.
* MODULEVERSION : Version de hello modifiée système binaire.

Voici un exemple de ce type d’alerte :

![Alerte de fichier binaire système](./media/security-center-alerts-type/security-center-alerts-type-fig5.png)

### <a name="suspicious-process-executed"></a>Processus suspect exécuté
Centre de sécurité identifie un processus suspect s’exécute sur la machine virtuelle hello cible, puis déclenche une alerte. détection de Hello ne ressemble pas de nom spécifique de hello, mais recherche les paramètres du fichier exécutable hello. Par conséquent, même si la personne malveillante de hello renomme hello exécutable, centre de sécurité peut détecter toujours les processus suspects hello.

Voici un exemple de ce type d’alerte :

![Alerte de processus suspect](./media/security-center-alerts-type/security-center-alerts-type-fig6-new.png)

### <a name="multiple-domain-accounts-queried"></a>Plusieurs comptes de domaine interrogés
Centre de sécurité peut détecter plusieurs tentatives tooquery comptes de domaine Active Directory, qui est généralement effectuée par des personnes malveillantes au cours de la reconnaissance du réseau. Les pirates peuvent tirer parti de cette technique tooquery hello tooidentify hello les utilisateurs du domaine, identifier des comptes d’administrateur de domaine hello, identifier les ordinateurs hello qui sont des contrôleurs de domaine et également identifient hello potentielle de relation d’approbation avec d’autres domaines.

Voici un exemple de ce type d’alerte :

![Alerte de compte de domaines multiples](./media/security-center-alerts-type/security-center-alerts-type-fig7-new.png)

### <a name="local-administrators-group-members-were-enumerated"></a>Les membres du groupe Administrateurs locaux ont été énumérés

Centre de sécurité va tootrigger une alerte lorsque les événements de sécurité hello 4798, dans Windows Server 2016 et Windows 10, est déclenché. Cela se produit lorsque le groupe Administrateurs locaux est énuméré, ce qui est généralement effectué par des pirates au cours de la reconnaissance du réseau. Les pirates peuvent tirer parti de cette identité de hello tooquery technique des utilisateurs avec des privilèges d’administrateur.

Voici un exemple de ce type d’alerte :

![Administrateur local](./media/security-center-alerts-type/security-center-alerts-type-fig14-new.png)

### <a name="anomalous-mix-of-upper-and-lower-case-characters"></a>Combinaison anormale de majuscules et minuscules

Centre de sécurité déclenche une alerte lorsqu’il détecte l’utilisation de hello une combinaison de majuscules et minuscules à la ligne de commande hello. Certains des personnes malveillantes peuvent utiliser cette toohide technique à partir de la casse ou hachage en fonction de règle de l’ordinateur.

Voici un exemple de ce type d’alerte :

![Combinaison anormale](./media/security-center-alerts-type/security-center-alerts-type-fig15-new.png)

### <a name="suspected-kerberos-golden-ticket-attack"></a>Suspicion d’attaque de golden ticket Kerberos

Un compromis [krbtgt](https://technet.microsoft.com/library/dn745899.aspx) clé peut être utilisée par une personne malveillante de toocreate Kerberos « Tickets finale (Gold), « autorisant hello intrus tooimpersonate tout utilisateur qu’ils souhaitent. Centre de sécurité va tootrigger une alerte lorsqu’il détecte ce type d’activité.

> [!NOTE] 
> Pour plus d’informations sur les golden ticket Kerberos, lisez le [guide de prévention contre le vol d’informations d’identification Windows 10](http://download.microsoft.com/download/C/1/4/C14579CA-E564-4743-8B51-61C0882662AC/Windows%2010%20credential%20theft%20mitigation%20guide.docx).

Voici un exemple de ce type d’alerte :

![Golden ticket](./media/security-center-alerts-type/security-center-alerts-type-fig16-new.png)

### <a name="suspicious-account-created"></a>Création d’un compte suspect

Security Center déclenche une alerte lorsqu’un compte ressemblant fortement à un compte bénéficiant de privilèges d’administrateur intégré existant est créé. Cette technique peut être utilisée par toocreate des personnes malveillantes tooavoid en cours remarquer la vérification de compte non fiable.
 
Voici un exemple de ce type d’alerte :

![Compte suspect](./media/security-center-alerts-type/security-center-alerts-type-fig17-new.png)

### <a name="suspicious-firewall-rule-created"></a>Création d’une règle de pare-feu suspecte

Les attaquants peuvent tentent de sécurité de l’hôte toocircumvent en créant un pare-feu personnalisé règles tooallow applications malveillantes toocommunicate avec la commande et de contrôle, ou les attaques de toolaunch via réseau hello via hello compromis hôte. Security Center déclenche une alerte lorsqu’il détecte qu’une règle de pare-feu a été créée à partir d’un fichier exécutable à un emplacement suspect.
 
Voici un exemple de ce type d’alerte :

![Règle de pare-feu](./media/security-center-alerts-type/security-center-alerts-type-fig18-new.png)

### <a name="suspicious-combination-of-hta-and-powershell"></a>Combinaison suspecte de HTA et PowerShell

Security Center déclenche une alerte lorsqu’il détecte qu’un hôte d’application HTML (HTA) lance des commandes PowerShell. Il s’agit d’une technique utilisée par les pirates toolaunch PowerShell approuvée.
 
Voici un exemple de ce type d’alerte :

![HTA et PS](./media/security-center-alerts-type/security-center-alerts-type-fig19-new.png)


## <a name="network-analysis"></a>Analyse du réseau
La détection des menaces sur le réseau assurée par Azure Security Center fonctionne en collectant automatiquement les informations de sécurité à partir du trafic IPFIX (Internet Protocol Flow Information Export) Azure. Il analyse cette information, corrélation souvent des informations provenant de plusieurs sources, les menaces tooidentify.

### <a name="suspicious-outgoing-traffic-detected"></a>Trafic sortant suspect détecté
Périphériques réseau peuvent être détectés et profilés quantité hello même façon que d’autres types de systèmes. Les pirates commencent généralement par l’analyse des ports ou le balayage des ports. Dans l’exemple suivant de hello, vous avez suspectes Secure Shell (SSH) le trafic à partir d’une machine virtuelle. pouvant être en train de procéder à une attaque de force brute SSH ou à une attaque par balayage des ports contre une ressource externe.

![Alerte de trafic sortant suspect](./media/security-center-alerts-type/security-center-alerts-type-fig8.png)

Cette alerte fournit des informations que vous pouvez utiliser ressource hello tooidentify qui a été utilisé tooinitiate cette attaque. Cette alerte fournit également des informations tooidentify hello compromis machine, temps de détection de hello, plus les protocole hello et port qui a été utilisé. Ce panneau vous donne également une liste d’étapes de mise à jour qui peuvent être utilisé toomitigate ce problème.

### <a name="network-communication-with-a-malicious-machine"></a>Communication réseau avec un ordinateur malveillant
En exploitant les flux des informations sur les menaces de Microsoft, Azure Security Center peut détecter les ordinateurs compromis qui communiquent avec des adresses IP malveillantes. Dans de nombreux cas, les adresses malveillant hello sont un centre de contrôle et commande. Dans ce cas, le centre de sécurité a détecté que la communication de hello a été effectuée à l’aide du chargeur de poneys contre les programmes malveillants (également appelé [Fareit](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=PWS:Win32/Fareit.AF)).

![Alerte de communication réseau](./media/security-center-alerts-type/security-center-alerts-type-fig9.png)

Cette alerte fournit des informations qui vous permet de ressource hello tooidentify qui a été utilisé tooinitiate cette attaque, hello effectuées sur la ressource, hello victime IP, hello attaquant IP et les temps de détection hello.

> [!NOTE]
> Les adresses IP dynamiques ont été supprimés de cette capture d’écran à des fins de confidentialité.
>
>

### <a name="possible-outgoing-denial-of-service-attack-detected"></a>Attaque potentielle par déni de service sortant détectée
Le trafic réseau anormale provenant d’un ordinateur virtuel peut entraîner des tootrigger du centre de sécurité type d’attaque par déni de service potentiels.

Voici un exemple de ce type d’alerte :

![Déni de service sortant](./media/security-center-alerts-type/security-center-alerts-type-fig10-new.png)

## <a name="resource-analysis"></a>Analyse des ressources
Analyse des ressources de centre de sécurité se concentre sur la plateforme en tant que service (PaaS) services, tels que l’intégration de hello avec hello [détection des menaces de base de données SQL Azure](../sql-database/sql-database-threat-detection.md) fonctionnalité. Selon les résultats d’analyse hello à partir de ces zones, le centre de sécurité déclenche une alerte liée aux ressources.

### <a name="potential-sql-injection"></a>Injection potentielle de code SQL
Injection SQL est une attaque où insérer un code malveillant dans les chaînes transmises ultérieurement instance tooan de SQL Server pour l’analyse et de l’exécution. Toute procédure qui construit des instructions SQL doit être analysée pour rechercher les vulnérabilités d’injection, car SQL Server exécutera toutes les requêtes syntaxiquement valides qu’il reçoit. Détection des menaces SQL utilise l’apprentissage, l’analyse comportementale et anomalies détection toodetermine d’événements suspects qui peuvent être en cours dans vos bases de données SQL Azure. Par exemple :

* Tentative d’accès à la base de données par un ancien employé
* Attaques par injection de code SQL
* Base de données de production de tooa accès inhabituelle à partir d’un utilisateur à domicile

![Alerte d’injection potentielle de code SQL](./media/security-center-alerts-type/security-center-alerts-type-fig11.png)

informations Hello dans cette alerte peuvent être utilisé tooidentify hello attaqué ressource, heure de la détection hello et l’état de hello d’attaque de hello. Il fournit également un lien étapes d’enquête toofurther.

### <a name="vulnerability-toosql-injection"></a>Une vulnérabilité tooSQL d’Injection
Cette alerte est déclenchée lorsqu’une erreur d’application est détectée sur une base de données. Cette alerte peut indiquer qu’un exemple d’injection tooSQL éventuelle vulnérabilité des attaques.

![Alerte d’injection potentielle de code SQL](./media/security-center-alerts-type/security-center-alerts-type-fig12-new.png)

### <a name="unusual-access-from-unfamiliar-location"></a>Accès inhabituel depuis un emplacement inconnu
Cette alerte est déclenchée lorsqu’un événement d’accès à partir d’une adresse IP inconnu a été détecté sur le serveur hello, ce qui n’est pas visible dans hello dernière période.

![Alerte d’accès inhabituel](./media/security-center-alerts-type/security-center-alerts-type-fig13-new.png)

## <a name="contextual-information"></a>Informations contextuelles
Pendant une enquête, les analystes doivent un contexte supplémentaire tooreach un verdict sur la nature hello de menace de hello et comment toomitigate il.  Par exemple, une anomalie de réseau a été détectée, mais sans comprendre que se passe-t-il hello réseau ou ressource toohello ciblée de tenir compte il est, chaque disque dur toounderstand quel tootake actions suivant. tooaid avec qui, un Incident de sécurité peuvent inclure des artefacts, événements et informations connexes qui peuvent aider à responsable des essais hello. Hello disponibilité d’autres informations varient en fonction d’hello du type de menace détecté hello la configuration de votre environnement et ne seront pas disponibles pour tous les Incidents de sécurité.

Si des informations supplémentaires sont disponibles, il sera affiché dans hello Incident de sécurité ci-dessous liste hello des alertes. Cette section peut contenir des informations telles que :

- Événements d’effacement de journal
- Appareil Plug-and-Play branché à partir d’un appareil inconnu
- Alertes non actionnables 

![Alerte d’accès inhabituel](./media/security-center-alerts-type/security-center-alerts-type-fig20.png) 


## <a name="see-also"></a>Voir aussi
Dans cet article, vous avez appris hello différents types d’alertes de sécurité dans le centre de sécurité. toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Gestion des incidents de sécurité dans Azure Security Center](security-center-incident.md)
* [Fonctionnalités de détection d’Azure Security Center](security-center-detection-capabilities.md)
* [Guide des opérations et de planification d’Azure Security Center](security-center-planning-and-operations-guide.md)
* [Forum aux questions sur Azure Security Center](security-center-faq.md): Forum aux questions sur l’utilisation hello service de recherche.
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : recherchez des billets de blog sur la sécurité et la conformité Azure.
