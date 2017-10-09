---
title: connexions aaaITSM dans le connecteur de gestion du Service OMS informatique | Documents Microsoft
description: "Connecter votre ITSM produits/services avec le connecteur de gestion du Service informatique dans OMS toocentrally analyse et gérer des éléments de travail ITSM hello."
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 8231b7ce-d67f-4237-afbf-465e2e397105
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: v-jysur
ms.openlocfilehash: 53ef51bf75fb8ed15ea3ce5072d9365c221f9f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-itsm-productsservices-with-it-service-management-connector-preview"></a>Connecter des produits/services ITSM à IT Service Management Connector (préversion)
Cet article fournit des informations sur la façon tooconnect votre tooIT de produits et services ITSM connecteur de gestion de Service dans OMS et de manière centralisée gérer vos éléments de travail. Pour plus d’informations sur IT Service Management Connector, voir la [Présentation](log-analytics-itsmc-overview.md).

Hello suite de produits ou services est pris en charge :

- [System Center Service Manager](#connect-system-center-service-manager-to-it-service-management-connector-in-oms)
- [ServiceNow](#connect-servicenow-to-it-service-management-connector-in-oms)
- [Provance](#connect-provance-to-it-service-management-connector-in-oms)
- [Cherwell](#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="connect-system-center-service-manager-tooit-service-management-connector-in-oms"></a>Se connecter à System Center Service Manager tooIT connecteur de gestion de Service dans OMS

Hello sections suivantes fournissent des détails sur la façon tooconnect votre toohello de produit System Center Service Manager connecteur de gestion de Service informatique dans OMS.

### <a name="prerequisites"></a>Composants requis

Assurez-vous de qu'avoir hello suivant les conditions préalables sont remplies :

- IT Service Management Connector installé.
Plus d’informations : [Configuration](log-analytics-itsmc-overview.md#configuration).
- Hello l’application Gestionnaire de services Web (application Web) est déployée et configurée. Pour plus d’informations sur l’application web, cliquez [ici](#create-and-deploy-service-manager-web-app-service).
- Connexion hybride créée et configurée. Plus d’informations : [hybride de hello configurer connexion](#configure-the-hybrid-connection).
- Versions prises en charge de Service Manager : 2012 R2 ou 2016.
- Rôle utilisateur : [opérateur avancé](https://technet.microsoft.com/library/ff461054.aspx).

### <a name="connection-procedure"></a>Procédure de connexion

Utilisez hello suivant la procédure tooconnect votre toohello d’instance de System Center Service Manager connecteur de gestion du Service informatique :

1. Accédez trop**OMS** >**paramètres** > **Sources connectées**.
2. Sélectionnez **ITSM Connector**, puis cliquez sur **Ajouter une nouvelle connexion**.

    ![Service Manager ](./media/log-analytics-itsmc/itsmc-service-manager-connection.png)
3. Fournir des informations de hello comme décrit dans hello tableau suivant, puis cliquez sur **enregistrer** connexion de hello toocreate :

> [!NOTE]
> Tous ces paramètres sont obligatoires.

| **Champ** | **Description** |
| --- | --- |
| **Name**   | Tapez un nom d’instance de System Center Service Manager hello que vous souhaitez tooconnect avec hello connecteur de gestion du Service informatique.  Vous utiliserez ce nom ultérieurement lorsque vous configurerez des éléments de travail dans cette instance ou afficherez une analyse de journal détaillée. |
| **Sélectionner un type de connexion**   | Sélectionnez **System Center Service Manager**. |
| **URL du serveur**   | Tapez l’URL hello Hello application Web de Service Manager. Pour plus d’informations sur l’application web Service Manager, cliquez [ici](#create-and-deploy-service-manager-web-app-service).
| **ID client**   | Tapez les ID de client hello généré (à l’aide d’un script automatique hello) pour l’authentification de l’application Web hello. Plus d’informations sur le script de hello automatisée est [ici.](log-analytics-itsmc-service-manager-script.md)|
| **Clé secrète client**   | Clé secrète de type hello client, générée pour ce code.   |
| **Étendue de la synchronisation des données**   | Sélectionnez des éléments de travail Service Manager hello que vous souhaitez toosync via hello connecteur de gestion du Service informatique.  Ces éléments de travail sont importés dans Log Analytics. **Options :** incidents, demandes de modification.|
| **Synchroniser les données** | Tapez hello les nombre de jours souhaité pour les données de salutation à partir de. **Limite maximale** : 120 jours. |
| **Create new configuration item in ITSM solution (Créer un élément de configuration dans la solution ITSM)** | Sélectionnez cette option si vous souhaitez que les éléments de configuration toocreate hello dans le produit ITSM hello. Lorsque sélectionnée, OMS crée les éléments de configuration hello affectée comme des éléments de configuration (en cas d’éléments de configuration non existant) Bonjour pris en charge le système ITSM. **Par défaut** : désactivée. |

En cas de connexion et de synchronisation réussies :

- Les éléments de travail sélectionnés dans Service Manager sont importés dans OMS **Log Analytics**. Vous pouvez afficher le résumé hello de ces éléments de travail sur la vignette du connecteur de gestion du Service informatique hello.

- Dans OMS, vous pouvez créer des incidents à partir d’alertes OMS ou de recherche dans les journaux, dans cette instance Service Manager.

Plus d’informations : [Create ITSM work items for OMS alerts (Créer des éléments de travail ITSM pour des alertes OMS)](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) et [Create ITSM work items from OMS logs (Créer des éléments de travail ITSM à partir de journaux OMS)](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="create-and-deploy-service-manager-web-app-service"></a>Créer et déployer l’application web Service Manager

tooconnect hello local Service Manager avec hello connecteur de gestion de Service informatique dans OMS, Microsoft a créé une application Web de Service Manager sur hello GitHub.

tooset hello ITSM Web de l’application pour votre Service Manager, procédez comme hello suivant :

- **L’application Web Deploy hello** : déployer l’application Web de hello, définir les propriétés de hello et s’authentifier auprès d’Azure AD. Vous pouvez déployer l’application hello web à l’aide de hello [automatisée script](log-analytics-itsmc-service-manager-script.md) que Microsoft vous a fourni.
- **Configurer la connexion hybride hello** - [configurer cette connexion](#configure-the-hybrid-connection)manuellement.

#### <a name="deploy-hello-web-app"></a>Déployer l’application web de hello
Hello d’utilisation automatisée [script](log-analytics-itsmc-service-manager-script.md) toodeploy hello Web app, définir les propriétés de hello et s’authentifier auprès d’Azure AD.

Exécuter le script de hello en fournissant hello les détails requis suivants :

- Détails de l’abonnement Azure
- Nom de groupe ressources
- Emplacement
- Détails du serveur Service Manager (nom du serveur, domaine, nom d’utilisateur et mot de passe)
- Préfixe de nom de site pour votre application Web
- Espace de noms ServiceBus.

script Hello crée hello Web app à l’aide du nom hello que vous avez spécifiées (ainsi que quelques autres chaînes toomake unique). Il génère hello **URL de l’application Web**, **ID client** et **clé secrète client**.

Enregistrez les valeurs hello, vous les utilisez lorsque vous créez une connexion avec le connecteur de gestion du Service informatique.

**Vérifiez l’installation de l’application hello Web**

1. Accédez trop**portail Azure** > **ressources**.
2. Sélectionnez l’application hello Web, cliquez sur **paramètres** > **paramètres de l’Application**.
3. Confirmer les informations de hello sur l’instance de Service Manager hello que vous avez fourni au moment de hello de déploiement d’application hello dans le script hello.

### <a name="configure-hello-hybrid-connection"></a>Configurer la connexion hybride hello

Utilisez hello suivant la procédure tooconfigure hello la connexion hybride qui connecte l’instance de Service Manager hello avec hello connecteur de gestion de Service informatique dans OMS.

1. Recherche hello application Web de Service Manager, sous **ressources Azure**.
2. Cliquez sur **Paramètres** > **Mise en réseau**.
3. Sous **Connexions hybrides**, cliquez sur **Configurer vos points de terminaison de connexion hybride**.

    ![Mise en réseau de connexions hybrides](./media/log-analytics-itsmc/itsmc-hybrid-connection-networking-and-end-points.png)
4. Bonjour **connexions hybrides** panneau, cliquez sur **ajouter une connexion hybride**.

    ![Ajout d’une connexion hybride](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-add.png)

5. Bonjour **ajouter des connexions hybrides** panneau, cliquez sur **hybride de créer nouvelle connexion**.

    ![Nouvelle connexion hybride](./media/log-analytics-itsmc/itsmc-create-new-hybrid-connection.png)

6. Tapez hello valeurs suivantes :

    - **Nom du point de terminaison**: spécifiez un nom pour la connexion hybride hello.
    -  **Hôte du point de terminaison**: nom de domaine complet du serveur d’administration Service Manager hello.
    - **Port du point de terminaison** : tapez 5724.
    - **Espace de noms Servicebus** : utilisez un espace de noms Servicebus existant ou créez-en un.
    - **Emplacement**: sélectionnez l’emplacement de hello.
    -  **Nom**: spécifiez un servicebus toohello de nom si vous la créez.

    ![Valeurs de connexion hybride](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-values.png)
6. Cliquez sur **OK** tooclose hello **créer la connexion hybride** lame et commencer à créer la connexion hybride hello.

    Une fois la connexion hybride hello est créée, il est affiché sous le panneau de hello.

7. Une fois la connexion hybride hello est créée, sélectionnez hello connexion et cliquez sur **ajouter sélectionné la connexion hybride**.

    ![Nouvelle connexion hybride](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-added.png)

#### <a name="configure-hello-listener-setup"></a>Configurer le programme d’installation de hello écouteur

Utilisez hello après l’installation d’écouteur procédure tooconfigure hello pour la connexion hybride hello.

1. Bonjour **connexions hybrides** panneau, cliquez sur **téléchargement hello Connection Manager** et l’installer sur l’ordinateur hello où l’instance System Center Service Manager est en cours d’exécution.

    Une fois terminée, l’installation de hello **Gestionnaire de connexions hybrides UI** option est disponible sous **Démarrer** menu.

2. Cliquez sur **Interface utilisateur du gestionnaire de connexions hybrides**. Vous êtes invité à entrer vos informations d’identification Azure.

3. Connectez-vous avec vos informations d’identification Azure et sélectionnez votre abonnement où hello connexion hybride a été créé.

4. Cliquez sur **Enregistrer**.

Votre connexion hybride est connectée avec succès.

![Connexion hybride réussie](./media/log-analytics-itsmc/itsmc-hybrid-connection-listener-set-up-successful.png)
> [!NOTE]

> Une fois la connexion hybride hello est créée, vérifier et tester la connexion en visitant hello hello déployé l’application Web de Service Manager. Vérifiez la connexion de hello est établie avant d’essayer de tooconnect toohello connecteur de gestion de Service informatique dans OMS.

Hello image suivante montre les détails de hello d’une connexion réussie :

![Test de connexion hybride](./media/log-analytics-itsmc/itsmc-hybrid-connection-test.png)

## <a name="connect-servicenow-tooit-service-management-connector-in-oms"></a>Se connecter ServiceNow tooIT connecteur de gestion de Service dans OMS

Hello sections suivantes fournissent des détails sur la façon tooconnect votre toohello de produit ServiceNow connecteur de gestion de Service informatique dans OMS.

### <a name="prerequisites"></a>Composants requis

Assurez-vous de qu'avoir hello suivant les conditions préalables sont remplies :

- IT Service Management Connector installé. Plus d’informations : [Configuration](log-analytics-itsmc-overview.md#configuration).
- Versions prises en charge de ServiceNow : Fuji, Genève, Helsinki.

ServiceNow Admins doit faire hello suivant leur instance ServiceNow :
- Générer des ID de client et question secrète du client pour le produit de ServiceNow hello. Pour plus d’informations sur comment les ID de client toogenerate et secret, consultez [l’installation d’OAuth](http://wiki.servicenow.com/index.php?title=OAuth_Setup).
- Installez hello application d’utilisateur pour l’intégration de Microsoft OMS (application ServiceNow). [En savoir plus](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 ).
- Créer le rôle d’utilisateur de l’intégration d’application utilisateur hello est installée. Plus d’informations sur la façon dont le rôle d’utilisateur de toocreate hello intégration est [ici](#create-integration-user-role-in-servicenow-app).


### <a name="connection-procedure"></a>**Procédure de connexion**

Hello, suivant la procédure toocreate une connexion de ServiceNow, utilisez :

1. Accédez trop**OMS** > **paramètres** > **Sources connectées**.
2. Sélectionnez **ITSM Connector**, puis cliquez sur **Ajouter une nouvelle connexion**.

    ![Connexion de ServiceNow](./media/log-analytics-itsmc/itsmc-servicenow-connection.png)

3. Fournir des informations de hello comme décrit dans hello tableau suivant, puis cliquez sur **enregistrer** connexion de hello toocreate :

> [!NOTE]
> Tous ces paramètres sont obligatoires.

| **Champ** | **Description** |
| --- | --- |
| **Name**   | Tapez un nom pour l’instance de ServiceNow hello que vous souhaitez tooconnect avec hello connecteur de gestion du Service informatique.  Vous utiliserez ce nom ultérieurement dans OMS lorsque vous configurerez des éléments de travail dans cette instance ITSM ou afficherez une analyse de journal détaillée. |
| **Sélectionner un type de connexion**   | Sélectionnez **ServiceNow**. |
| **Nom d’utilisateur**   | Tapez le nom d’utilisateur d’intégration hello que vous avez créé dans hello ServiceNow application toosupport hello connexion toohello connecteur de gestion du Service informatique. Plus d’informations : [Create ServiceNow app user role (Créer un rôle utilisateur pour l’application ServiceNow)](#create-integration-user-role-in-servicenow-app).|
| **Mot de passe**   | Tapez le mot de passe de hello associé à ce nom d’utilisateur. **Remarque**: nom d’utilisateur et mot de passe sont utilisés pour générer des jetons d’authentification et ne sont pas stockées n’importe où dans le service OMS de hello.  |
| **URL du serveur**   | Tapez les URL hello d’instance ServiceNow de hello que vous souhaitez tooconnect tooIT connecteur de Service Management. |
| **ID client**   | Tapez les ID de client hello toouse souhaité pour l’authentification OAuth2, ce qui vous avez généré précédemment.  Plus d’informations sur la génération de l’ID client et de la clé secrète : [Installation d’OAuth](http://wiki.servicenow.com/index.php?title=OAuth_Setup). |
| **Clé secrète client**   | Clé secrète de type hello client, générée pour ce code.   |
| **Étendue de la synchronisation des données**   | Sélectionnez hello ServiceNow des éléments de travail que vous souhaitez tooOMS toosync, via le connecteur de gestion du Service informatique de hello.  les valeurs Hello sélectionné sont importés dans analytique de journal.   **Options :** incidents et demandes de modification.|
| **Synchroniser les données** | Tapez hello les nombre de jours souhaité pour les données de salutation à partir de. **Limite maximale** : 120 jours. |
| **Create new configuration item in ITSM solution (Créer un élément de configuration dans la solution ITSM)** | Sélectionnez cette option si vous souhaitez que les éléments de configuration toocreate hello dans le produit ITSM hello. Lorsque sélectionnée, OMS crée les éléments de configuration hello affectée comme des éléments de configuration (en cas d’éléments de configuration non existant) Bonjour pris en charge le système ITSM. **Par défaut** : désactivée. |


En cas de connexion et de synchronisation réussies :

- Les éléments de travail sélectionnés dans la connexion ServiceNow sont importés dans OMS Log Analytics.  Vous pouvez afficher le résumé hello de ces éléments de travail sur la vignette du connecteur de gestion du Service informatique hello.
- Vous pouvez créer des incidents, des alertes et des événements à partir d’alertes OMS ou de recherche dans les journaux, dans cette instance ServiceNow.  


Plus d’informations : [Create ITSM work items for OMS alerts (Créer des éléments de travail ITSM pour des alertes OMS)](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) et [Create ITSM work items from OMS logs (Créer des éléments de travail ITSM à partir de journaux OMS)](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="create-integration-user-role-in-servicenow-app"></a>Créer un rôle utilisateur de l’intégration dans l’application ServiceNow

Hello utilisateur procédure :

1.  Visitez hello [ServiceNow magasin](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0) et installer hello **application utilisateur pour l’intégration de OMS de Microsoft et de ServiceNow** dans votre Instance ServiceNow.
2.  Après l’installation, visitez hello barre de navigation de l’instance ServiceNow de hello, la recherche et sélectionnez Microsoft OMS intégrateur de gauche.  
3.  Cliquez sur **Liste de vérifications d’installation**.

    état de Hello est affiché en tant que **pas terminer** si le rôle d’utilisateur hello est encore toobe créé.

4.  Dans le texte hello zones, ensuite trop**créer un utilisateur intégration**, entrez les nom d’utilisateur hello pour utilisateur hello qui peut se connecter toohello connecteur de gestion de Service informatique dans OMS.
5.  Entrez le mot de passe hello pour cet utilisateur, puis cliquez sur **OK**.  

>[!NOTE]

> Vous utilisez ces informations d’identification toomake hello ServiceNow de connexion d’OMS.

Hello utilisateur récemment créé est affiché avec les rôles par défaut de hello attribués.

Rôles par défaut :
- personalize_choices
- import_transformer
-   x_mioms_microsoft.user
-   itil
-   template_editor
-   view_changer

Une fois que l’utilisateur de hello est correctement créé, hello état de **vérifier une Installation Checklist** déplace tooCompleted, affichage des détails hello hello du rôle d’utilisateur créé pour une application hello.

> [!NOTE]

> tooallow un toocreate utilisateur **alertes** et **événements** dans ServiceNow d’OMS :

> - Assurez-vous de qu'avoir module de gestion des événements hello installé sur votre instance ServiceNow.

> - Ajoutez hello suivant utilisateur d’intégration toohello rôles :
>      - evt_mgmt_integration
>      - evt_mgmt_operator  


## <a name="connect-provance-tooit-service-management-connector-in-oms"></a>Se connecter Provance tooIT connecteur de gestion de Service dans OMS

Hello sections suivantes fournissent des détails sur la façon tooconnect votre toohello de produit Provance connecteur de gestion de Service informatique dans OMS.

### <a name="prerequisites"></a>Composants requis

Assurez-vous de qu'avoir hello suivant les conditions préalables sont remplies :

- IT Service Management Connector installé. Plus d’informations : [Configuration](log-analytics-itsmc-overview.md#configuration).
- L’application Provance doit être inscrite auprès d’Azure AD, et l’ID client est mis à disposition. Pour plus d’informations, consultez [comment l’authentification active directory de tooconfigure](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
- Rôle utilisateur : administrateur.

### <a name="connection-procedure"></a>Procédure de connexion

Utilisez hello suivant la procédure toocreate une connexion Provance :

1. Accédez trop**OMS** > **paramètres** > **Sources connectées**.
2. Sélectionnez **ITSM Connector**, puis cliquez sur **Ajouter une nouvelle connexion**.  

    ![Connexion Provance](./media/log-analytics-itsmc/itsmc-provance-connection.png)
3. Fournir des informations de hello comme décrit dans hello tableau suivant, puis cliquez sur **enregistrer** connexion de hello toocreate.

> [!NOTE]
> Tous ces paramètres sont obligatoires.

| **Champ** | **Description** |
| --- | --- |
| **Name**   | Tapez un nom pour l’instance de Provance hello que vous souhaitez tooconnect avec hello connecteur de gestion du Service informatique.  Vous utiliserez ce nom ultérieurement dans OMS lorsque vous configurerez des éléments de travail dans cette instance ITSM ou afficherez une analyse de journal détaillée. |
| **Sélectionner un type de connexion**   | Sélectionnez **Provance**. |
| **Nom d’utilisateur**   | Tapez le nom d’utilisateur de hello qui peut se connecter toohello connecteur de gestion du Service informatique.    |
| **Mot de passe**   | Tapez le mot de passe de hello associé à ce nom d’utilisateur. **Remarque :** nom d’utilisateur et mot de passe sont utilisés pour générer des jetons d’authentification et ne sont pas stockées n’importe où dans le service OMS de hello. _|
| **URL du serveur**   | Tapez l’URL hello de votre instance Provance que vous souhaitez tooconnect tooIT connecteur de Service Management. |
| **ID client**   | ID de client type hello pour authentifier cette connexion, vous avez généré dans votre instance Provance.  Plus d’informations sur l’ID de client, consultez [comment l’authentification active directory de tooconfigure](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). |
| **Étendue de la synchronisation des données**   | Sélectionnez hello Provance des éléments de travail que vous souhaitez tooOMS toosync, via le connecteur de gestion du Service informatique de hello.  Ces éléments de travail sont importés dans Log Analytics.   **Options :** incidents, demandes de modification.|
| **Synchroniser les données** | Tapez hello les nombre de jours souhaité pour les données de salutation à partir de. **Limite maximale** : 120 jours. |
| **Create new configuration item in ITSM solution (Créer un élément de configuration dans la solution ITSM)** | Sélectionnez cette option si vous souhaitez que les éléments de configuration toocreate hello dans le produit ITSM hello. Lorsque sélectionnée, OMS crée les éléments de configuration hello affectée comme des éléments de configuration (en cas d’éléments de configuration non existant) Bonjour pris en charge le système ITSM. **Par défaut** : désactivée.|

En cas de connexion et de synchronisation réussies :

- Les éléments de travail sélectionnés dans la connexion Provance sont importés dans OMS **Log Analytics**.  Vous pouvez afficher le résumé hello de ces éléments de travail sur la vignette du connecteur de gestion du Service informatique hello.
- Vous pouvez créer des incidents et des événements à partir d’alertes OMS ou de recherche dans les journaux, dans cette instance Provance.

Plus d’informations : [Create ITSM work items for OMS alerts (Créer des éléments de travail ITSM pour des alertes OMS)](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) et [Create ITSM work items from OMS logs (Créer des éléments de travail ITSM à partir de journaux OMS)](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

## <a name="connect-cherwell-tooit-service-management-connector-in-oms"></a>Se connecter à Cherwell tooIT connecteur de gestion de Service dans OMS

Hello sections suivantes fournissent des détails sur la façon tooconnect votre toohello de produit Cherwell connecteur de gestion de Service informatique dans OMS.

### <a name="prerequisites"></a>Composants requis

Assurez-vous de qu'avoir hello suivant les conditions préalables sont remplies :

- IT Service Management Connector installé. Plus d’informations : [Configuration](log-analytics-itsmc-overview.md#configuration).
- ID client généré. Plus d’informations : [Générer un ID client pour Cherwell](#generate-client-id-for-cherwell).
- Rôle utilisateur : administrateur.

### <a name="connection-procedure"></a>Procédure de connexion

Utilisez hello suivant la procédure toocreate une connexion Cherwell :

1. Accédez trop**OMS** >  **paramètres** > **Sources connectées**.
2. Sélectionnez **ITSM Connector**, puis cliquez sur **Ajouter une nouvelle connexion**.  

    ![Id utilisateur de Cherwell](./media/log-analytics-itsmc/itsmc-cherwell-connection.png)

3. Fournir des informations de hello comme décrit dans hello tableau suivant, puis cliquez sur **enregistrer** connexion de hello toocreate.

> [!NOTE]
> Tous ces paramètres sont obligatoires.

| **Champ** | **Description** |
| --- | --- |
| **Name**   | Tapez un nom pour l’instance de Cherwell hello que vous souhaitez tooconnect toohello connecteur de gestion du Service informatique.  Vous utiliserez ce nom ultérieurement dans OMS lorsque vous configurerez des éléments de travail dans cette instance ITSM ou afficherez une analyse de journal détaillée. |
| **Sélectionner un type de connexion**   | Sélectionnez **Cherwell**. |
| **Nom d’utilisateur**   | Tapez le nom d’utilisateur de Cherwell hello qui peut se connecter toohello connecteur de gestion du Service informatique. |
| **Mot de passe**   | Tapez le mot de passe de hello associé à ce nom d’utilisateur. **Remarque :** nom d’utilisateur et mot de passe sont utilisés pour générer des jetons d’authentification et ne sont pas stockées n’importe où dans le service OMS de hello.|
| **URL du serveur**   | Tapez l’URL hello de votre instance de Cherwell que vous souhaitez tooconnect tooIT connecteur de Service Management. |
| **ID client**   | ID de client type hello pour authentifier cette connexion, vous avez généré dans votre instance de Cherwell.   |
| **Étendue de la synchronisation des données**   | Sélectionnez hello Cherwell des éléments de travail que vous souhaitez toosync via hello connecteur de gestion du Service informatique.  Ces éléments de travail sont importés dans Log Analytics.   **Options :** incidents, demandes de modification. |
| **Synchroniser les données** | Tapez hello les nombre de jours souhaité pour les données de salutation à partir de. **Limite maximale** : 120 jours. |
| **Create new configuration item in ITSM solution (Créer un élément de configuration dans la solution ITSM)** | Sélectionnez cette option si vous souhaitez que les éléments de configuration toocreate hello dans le produit ITSM hello. Lorsque sélectionnée, OMS crée les éléments de configuration hello affectée comme des éléments de configuration (en cas d’éléments de configuration non existant) Bonjour pris en charge le système ITSM. **Par défaut** : désactivée. |

En cas de connexion et de synchronisation réussies :

- Les éléments de travail sélectionnés dans cette connexion Cherwell sont importés dans OMS Log Analytics. Vous pouvez afficher le résumé hello de ces éléments de travail sur la vignette du connecteur de gestion du Service informatique hello.
- Vous pouvez créer des incidents et des événements dans cette instance Cherwell à partir d’OMS. Plus d’informations : Create ITSM work items for OMS alerts (Créer des éléments de travail ITSM pour des alertes OMS) et Create ITSM work items from OMS logs (Créer des éléments de travail ITSM à partir de journaux OMS).

Plus d’informations : [Create ITSM work items for OMS alerts (Créer des éléments de travail ITSM pour des alertes OMS)](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) et [Create ITSM work items from OMS logs (Créer des éléments de travail ITSM à partir de journaux OMS)](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="generate-client-id-for-cherwell"></a>Générer un ID client pour Cherwell

toogenerate hello client ID et de clé pour Cherwell, utilisez hello procédure :

1. Ouvrez une session dans tooyour Cherwell instance en tant qu’administrateur.
2. Cliquez sur **Sécurité** > **Edit REST API client settings (Modifier les paramètres du client de l’API REST)**.
3. Sélectionnez **Créer un client** > **Clé secrète client**.

    ![Id utilisateur de Cherwell](./media/log-analytics-itsmc/itsmc-cherwell-client-id.png)


## <a name="next-steps"></a>Étapes suivantes
 - [Create ITSM work items for OMS alerts (Créer des éléments de travail ITSM pour des alertes OMS)](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)

 - [Create ITSM work items from OMS logs (Créer des éléments de travail ITSM à partir de journaux OMS)](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)

- [View log analytics for your connection (Afficher l’analyse des journaux correspondant à votre connexion)](log-analytics-itsmc-overview.md#using-the-solution)
