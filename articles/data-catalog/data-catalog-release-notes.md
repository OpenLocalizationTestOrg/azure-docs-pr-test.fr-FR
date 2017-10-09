---
title: "Notes de mise à jour du catalogue de données aaaAzure | Documents Microsoft"
description: "Notes de publication d’Azure Data Catalog."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 3aca9c49-45a4-4352-92e6-bd25ee3eacf7
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 661826f66020ba72a885c6b14522b53c8b469d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-release-notes"></a>Notes de publication sur Azure Data Catalog
## <a name="notes-for-hello-november-20-2015-release-of-azure-data-catalog"></a>Notes de version de 20 novembre 2015 hello d’Azure Data Catalog
### <a name="opening-data-sources-in-power-bi-desktop"></a>Ouverture de sources de données dans Power BI Desktop
Lorsque l’option de « Ouvrir dans Power BI Desktop » hello de hello **Azure Data Catalog** portail, les utilisateurs peuvent rencontrer un des deux problèmes Bonjour application de Power BI Desktop :

* Une boîte de dialogue avec le titre hello « Ne peut pas tooOpen Document » s’affiche.
* Hello application de Power BI Desktop s’ouvre, mais les fichiers hello apparaît toobe vide

Pour chaque situation, problème de hello peut être résolu en téléchargeant et en installant la version la plus récente de Power BI Desktop à partir de hello [PowerBI.com](https://powerbi.com).

## <a name="notes-for-hello-november-13-2015-release-of-azure-data-catalog"></a>Notes de version de 13 novembre 2015 hello d’Azure Data Catalog
### <a name="registering-and-connecting-tooteradata"></a>L’inscription et connexion tooTeradata
Lors de la connexion des sources de données tooTeradata les utilisateurs doivent disposer de le pilote ODBC de Teradata hello qui correspondent au nombre de bits hello (32 bits ou 64 bits) du logiciel hello utilisé.

À compter de ce connecteur Active Directory, date de publication, hello plus récente [du pilote ODBC de Teradata pour windows (version 15.10)](http://downloads.teradata.com/download/connectivity/odbc-driver/windows) est compatible avec Office 2013, mais pas avec Office 2016.

## <a name="notes-for-hello-july-13-2015-release-of-azure-data-catalog"></a>Notes de version de 13 juillet 2015 hello d’Azure Data Catalog
### <a name="registering-and-connecting-toooracle-database"></a>L’inscription et connexion tooOracle de base de données
Lorsque la connexion des utilisateurs de base de données tooOracle des sources de données doit disposer de pilotes Oracle corrects hello qui correspondent au nombre de bits hello (32 bits ou 64 bits) du logiciel hello utilisé.

* Lorsque vous inscrivez des sources de données Oracle sur un ordinateur exécutant Windows 32 bits, les pilotes Oracle 32 bits hello seront utilisés.
* Lorsque vous inscrivez des sources de données Oracle sur un ordinateur exécutant Windows 64 bits, les pilotes Oracle hello 64 bits seront utilisés.
* Lors de la connexion tooOracle des sources de données à l’aide d’Excel sur un ordinateur exécutant la version 32 bits de hello de Microsoft Office, y compris sur Windows 64 bits, les pilotes Oracle 32 bits hello servira
* Lors de la connexion tooOracle des sources de données à l’aide d’Excel sur un ordinateur exécutant la version 64 bits de hello de Microsoft Office, les pilotes Oracle hello 64 bits seront utilisés.

### <a name="registering-and-connecting-toosql-server-reporting-services"></a>L’inscription et connexion tooSQL Server Reporting Services
Prise en charge des sources de données SQL Server Reporting Services (SSRS) est actuellement limitée tooNative Mode serveurs uniquement. La prise en charge de SSRS en mode SharePoint sera disponible dans une version ultérieure.

### <a name="opening-data-assets-in-excel"></a>Ouverture des ressources de données dans Excel
Lors de l’ouverture des ressources de données dans Microsoft Excel à partir de hello **Azure Data Catalog** portail, les utilisateurs peuvent être invités à un **avis de sécurité Microsoft Excel** boîte de dialogue. Standard, il s’agit du comportement attendu et les utilisateurs peuvent sélectionner **activer** toocontinue.

Pour plus d’informations, consultez [Activer ou désactiver les alertes de sécurité relatives aux liens et aux fichiers de sites web suspects](https://support.office.com/article/Enable-or-disable-security-alerts-about-links-and-files-from-suspicious-websites-A1AC6AE9-5C4A-4EB3-B3F8-143336039BBE).

### <a name="proxy-and-policy-configuration-and-data-source-registration"></a>Configuration du proxy et de la stratégie, et inscription de la source de données
Les utilisateurs peuvent rencontrer une situation où ils peuvent se connecter sur le portail Azure Data Catalog toohello, mais lorsqu’ils tentent de toolog sur l’outil de l’inscription de la source des données de toohello qu'elles rencontrent un message d’erreur qui empêche l’ouverture de session.

Deux causes possibles à ce problème de comportement :

**Cause 1 : Configuration d’Active Directory Federation Services** outil de l’enregistrement de source de données hello utilise l’authentification par formulaire toovalidate les ouvertures de session utilisateur Active Directory. Pour une connexion réussie, l’authentification par formulaire doit être activée à la Bonjour stratégie d’authentification globale par un administrateur Active Directory.

Dans certains cas, cette erreur peut également survenir uniquement lorsque l’utilisateur de hello est hello réseau d’entreprise, ou uniquement lorsque l’utilisateur de hello se connecte à partir du réseau d’entreprise en dehors de hello. Stratégie d’authentification globale de Hello permet toobe de méthodes d’authentification activé séparément pour les connexions intranet et extranet. Erreurs de connexion peuvent se produire si l’authentification par formulaire n’est pas activée pour le réseau hello à partir de quels hello utilisateur se connecte.

Pour plus d’informations, consultez [Configuration des stratégies d’authentification](https://technet.microsoft.com/library/dn486781.aspx).

**Cause 2 : Configuration du proxy réseau** si le réseau d’entreprise de hello utilise un serveur proxy, outil d’inscription de hello peut-être pas en mesure de tooconnect tooAzure Active Directory via le proxy hello. Les utilisateurs peuvent s’assurer cet outil d’inscription de hello en modifiant le fichier de configuration de l’outil hello, ajout de cet section du fichier toohello :

      <system.net>
        <defaultProxy useDefaultCredentials="true" enabled="true">
          <proxy usesystemdefault="True"
                          proxyaddress="http://<your corporate network proxy url>"
                          bypassonlocal="True"/>
        </defaultProxy>
      </system.net>


fichier de RegistrationTool.exe.config toolocate hello, lancez l’outil d’inscription de hello et ouvrez utilitaire du Gestionnaire des tâches Windows hello. Sur l’onglet Détails de hello dans le Gestionnaire des tâches, avec le bouton droit sur RegistrationTool.exe et choisissez l’emplacement des fichiers ouverts à partir du menu contextuel de hello.
