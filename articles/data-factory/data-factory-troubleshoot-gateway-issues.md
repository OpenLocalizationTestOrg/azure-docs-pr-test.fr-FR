---
title: "problèmes de passerelle de gestion des données aaaTroubleshoot | Documents Microsoft"
description: "Fournit des conseils tootroubleshoot problèmes connexes tooData passerelle de gestion."
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a>Résoudre les problèmes liés à l’utilisation de la passerelle de gestion des données
Cet article fournit des informations sur la résolution des problèmes liés à l’utilisation de la passerelle de gestion des données.

> [!NOTE]
> Consultez hello [passerelle de gestion des données](data-factory-data-management-gateway.md) article pour plus d’informations sur la passerelle de hello. Consultez hello [déplacement des données entre locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) article pour une procédure pas à pas de déplacement des données à partir d’un tooMicrosoft de base de données locale SQL Server le stockage Blob Azure à l’aide de passerelle de hello.
>
>

## <a name="failed-tooinstall-or-register-gateway"></a>Passerelle tooinstall ou le Registre en échec
### <a name="1-problem"></a>1. Problème
Vous voyez ce message d’erreur lors de l’installation et l’inscription d’une passerelle, en particulier, lors du téléchargement du fichier d’installation de passerelle hello.

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a>Cause :
ordinateur Hello sur lequel vous essayez de passerelle de hello tooinstall a échoué toodownload hello dernier passerelle fichier d’installation à partir du centre de téléchargement de hello en raison du problème de réseau tooa.

#### <a name="resolution"></a>Résolution :
Vérifiez votre toosee de paramètres de serveur proxy pare-feu si les paramètres hello bloquent la connexion de réseau de hello de hello ordinateur toohello [centre de téléchargement](https://download.microsoft.com/)et mettre à jour les paramètres de hello en conséquence.

Ou bien, vous pouvez télécharger le fichier d’installation hello pour la passerelle la plus récente hello de hello [centre de téléchargement](https://www.microsoft.com/download/details.aspx?id=39717) sur d’autres ordinateurs qui peuvent accéder au centre de téléchargement hello. Vous pouvez ensuite l’ordinateur hôte et l’exécuter manuellement tooinstall et mise à jour de la passerelle hello passerelle toohello de copie hello installer fichiers.

### <a name="2-problem"></a>2. Problème
Vous recevez cette erreur lorsque vous essayez de tooinstall une passerelle en cliquant sur **installer directement sur cet ordinateur** Bonjour portail Azure.

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a>Cause :
Une passerelle est déjà installée sur l’ordinateur de hello.

#### <a name="resolution"></a>Résolution :
Désinstaller la passerelle existante de hello sur l’ordinateur de hello et cliquez sur hello **installer directement sur cet ordinateur** lier de nouveau.

### <a name="3-problem"></a>3. Problème
Cette erreur peut s’afficher lorsque vous inscrivez une nouvelle passerelle.

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a>Cause :
Vous pouvez voir ce message pour l’une des hello suivant raisons :

* format Hello de clé de passerelle hello n’est pas valide.
* clé de passerelle Hello a été invalidée.
* clé de passerelle Hello a été régénérée à partir du portail de hello.  

#### <a name="resolution"></a>Résolution :
Vérifiez si vous utilisez la clé de passerelle appropriée hello à partir du portail de hello. Si nécessaire, régénérer une clé et utiliser la passerelle de hello tooregister clé hello.

### <a name="4-problem"></a>4. Problème
Vous pouvez voir hello message d’erreur suivant lorsque vous utilisez l’inscription d’une passerelle.

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![Contenu ou format de clé non valide](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a>Cause :
Hello contenu ou le format de clé de passerelle d’entrée hello est incorrect. Une des raisons de hello peut être que vous avez copié uniquement une partie de clé de hello à partir du portail de hello ou que vous utilisez une clé non valide.

#### <a name="resolution"></a>Résolution :
Générer une clé de passerelle dans le portail de hello et utiliser hello copie bouton toocopy hello toute clé. Puis collez-la dans cette passerelle de hello tooregister fenêtre.

### <a name="5-problem"></a>5. Problème
Vous pouvez voir hello message d’erreur suivant lorsque vous utilisez l’inscription d’une passerelle.

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![La clé de passerelle n’est pas valide ou est vide.](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a>Cause :
clé de passerelle Hello a été régénérée ou passerelle de hello a été supprimé dans hello portail Azure. Il peut également se produire si le programme d’installation de hello passerelle de gestion des données n’est pas la plus récente.

#### <a name="resolution"></a>Résolution :
Vérifiez si le programme d’installation de hello passerelle de gestion des données est la version la plus récente hello, vous trouverez une version la plus récente hello sur hello Microsoft [centre de téléchargement](https://go.microsoft.com/fwlink/p/?LinkId=271260).

Si le programme d’installation est en cours / dernière et passerelle existe toujours sur le portail, régénérer la clé de passerelle hello Bonjour portail Azure et utilisez hello copier bouton toocopy hello ensemble la clé, puis collez-la dans cette passerelle de hello tooregister fenêtre. Sinon, recréez la passerelle de hello et recommencer.

### <a name="6-problem"></a>6. Problème
Vous pouvez voir hello message d’erreur suivant lorsque vous utilisez l’inscription d’une passerelle.

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![La clé de passerelle n’est pas valide ou est vide.](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a>Cause :
Cette erreur peut se produire parce que hello passerelle a été supprimée ou hello passerelle associé a été régénérée.

#### <a name="resolution"></a>Résolution :
Si la passerelle de hello a été supprimée, recréez passerelle hello à partir du portail de hello, cliquez sur **inscrire**, copiez hello clé à partir du portail de hello, coller et essayez de passerelle de hello tooregister.

Si la passerelle de hello existe toujours, mais sa clé a été régénérée, utilisez hello tooregister clé hello passerelle. Si vous n’avez pas la clé de hello, régénérer la clé hello de portail de hello.

### <a name="7-problem"></a>7. Problème
Lorsque vous vous inscrivez une passerelle, vous devrez peut-être le chemin d’accès tooenter et le mot de passe pour un certificat.

![Indiquer un certificat](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a>Cause :
passerelle de Hello a été inscrit sur avant les autres ordinateurs. Au cours de hello l’inscription initiale d’une passerelle, un certificat de chiffrement a été associé à une passerelle de hello. certificat de Hello peut être généré automatiquement par la passerelle de hello ou fournie par l’utilisateur de hello.  Ce certificat est utilisé tooencrypt les informations d’identification hello du magasin de données (service lié).  

![Exportation du certificat](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

Lorsque la restauration passerelle hello sur un ordinateur hôte différent, l’Assistant Inscription hello demande pour ce toodecrypt certificat des informations d’identification précédemment chiffrées avec ce certificat.  Sans ce certificat, informations d’identification hello ne peut pas être déchiffrées par passerelle hello et exécutions d’activité de copie suivantes associées à cette nouvelle passerelle échouent.  

#### <a name="resolution"></a>Résolution :
Si vous avez exporté le certificat des informations d’identification hello à partir de l’ordinateur de passerelle hello d’origine à l’aide de hello **exporter** bouton sur hello **paramètres** onglet du Gestionnaire de Configuration passerelle de gestion de données, utilisez hello certificat ici.

Vous ne pouvez pas ignorer cette étape lors de la récupération d’une passerelle. Si le certificat de hello est manquant, vous devez de passerelle de hello toodelete à partir du portail de hello et recréez une nouvelle passerelle.  En outre, mettre à jour de tous les services liés qui sont associées toohello passerelle en tapant de nouveau leurs informations d’identification.

### <a name="8-problem"></a>8. Problème
Vous pouvez voir hello message d’erreur suivant.

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a>Cause :
Cette erreur se produit lorsque votre passerelle est dans un environnement qui nécessite une tooaccess de proxy HTTP ressources Internet, ou le mot de passe de votre proxy d’authentification est modifié, mais il n’est pas actualisé en conséquence dans votre passerelle.

#### <a name="resolution"></a>Résolution :
Suivez les instructions de hello Bonjour [considérations sur les serveurs Proxy](#proxy-server-considerations) section de cet article et configurer les paramètres de proxy du Gestionnaire de Configuration passerelle de gestion avec des données.

## <a name="gateway-is-online-with-limited-functionality"></a>La passerelle est en ligne avec des fonctionnalités limitées
### <a name="1-problem"></a>1. Problème
Vous consultez État hello de passerelle de hello en ligne avec des fonctionnalités limitées.

#### <a name="cause"></a>Cause :
Vous consultez État hello de passerelle de hello en ligne avec des fonctionnalités limitées pour l’une des hello suivant raisons :

* Impossible de connecter passerelle toocloud service via Azure Service Bus.
* Service cloud ne peut pas se connecter à toogateway via Service Bus.

Hello passerelle est en ligne avec des fonctionnalités limitées, vous peut-être pas en mesure de toouse hello Assistant Copier les données fabrique toocreate des pipelines de données pour la copie des données tooor à partir de banques de données locales. Comme solution de contournement, vous pouvez utiliser l’éditeur Data Factory dans le portail hello, Visual Studio ou Azure PowerShell.

#### <a name="resolution"></a>Résolution :
Résolution de ce problème (en ligne avec des fonctionnalités limitées) est basée sur la passerelle de hello ne peut pas se connecter le service de cloud computing toohello ou hello autre façon. Hello les sections suivantes fournit ces résolutions.

### <a name="2-problem"></a>2. Problème
Hello, l’erreur suivante s’affiche.

`Error: Gateway cannot connect toocloud service through service bus`

![Impossible de connecter passerelle toocloud service](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a>Cause :
Passerelle ne peut pas se connecter le service cloud toohello via Service Bus.

#### <a name="resolution"></a>Résolution :
Suivez ces étapes tooget hello passerelle qui en ligne :

1. Autoriser l’adresse IP des règles de trafic sortant sur l’ordinateur de passerelle hello et les pare-feu d’entreprise hello. Vous pouvez trouver les adresses IP à partir de hello journal des événements Windows (ID == 401) : une tentative a été effectuée tooaccess un socket de manière interdite par ses autorisations d’accès XX. XX. XX. XX:9350.
* Configurer les paramètres de proxy sur la passerelle hello. Consultez hello [considérations sur les serveurs Proxy](#proxy-server-considerations) pour plus d’informations.
* Activer les ports sortants 5671 et 9350-9354 sur les deux hello le pare-feu Windows sur l’ordinateur de passerelle hello et les pare-feu d’entreprise hello. Consultez hello [pare-feu et Ports](#ports-and-firewall) pour plus d’informations. Cette étape est facultative, mais elle est recommandée pour des questions de performances.

### <a name="3-problem"></a>3. Problème
Hello, l’erreur suivante s’affiche.

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a>Cause :
erreur temporaire de connectivité réseau.

#### <a name="resolution"></a>Résolution :
Suivez ces étapes tooget hello passerelle qui en ligne :

1. Attendez quelques minutes, la connectivité de hello est récupérée automatiquement lors de l’erreur de hello a disparu.
* Si hello erreur persiste, redémarrez le service de passerelle hello.

## <a name="failed-tooauthor-linked-service"></a>Service de tooauthor Échec lié
### <a name="problem"></a>Problème
Vous pouvez voir cette erreur lorsque vous essayez de toouse le Gestionnaire d’informations d’identification dans informations d’identification du portail tooinput hello pour un service lié, ou mettre à jour les informations d’identification pour un service lié existant.

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

Lorsque vous voyez cette erreur, page de paramètres hello du Gestionnaire de Configuration passerelle de gestion des données peut se présenter comme hello suivant capture d’écran.

![Impossible de contacter la base de données](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a>Cause :
certificat SSL de Hello peut avoir été perdu sur l’ordinateur de passerelle hello. ordinateur de passerelle Hello ne peut pas charger hello certificat actuellement utilisé pour le chiffrement SSL. Vous pouvez également voir un message d’erreur dans le journal des événements hello qui est similaire toohello message suivant.

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a>Résolution :
Suivez ces problèmes de hello toosolve comme suit :

1. Lancez le Gestionnaire de configuration de passerelle de gestion des données.
2. Commutateur toohello **paramètres** onglet.  
3. Cliquez sur hello **modification** certificat SSL de bouton toochange hello.

   ![Bouton de modification du certificat](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. Sélectionnez un nouveau certificat en tant que certificat SSL de hello. Vous pouvez utiliser n’importe quel certificat SSL généré par vos soins ou par une organisation quelconque.

   ![Indiquer un certificat](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a>Échec de l’activité de copie
### <a name="problem"></a>Problème
Vous pouvez remarquer hello après une panne de « UserErrorFailedToConnectToSqlserver » après avoir configuré un pipeline dans le portail de hello.

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a>Cause :
Cela peut se produire pour différentes raisons et la procédure de résolution varie en conséquence.

#### <a name="resolution"></a>Résolution :
Autoriser les connexions TCP sortantes sur le port TCP/1433 sur hello côté client de passerelle de gestion des données avant la connexion de base de données SQL tooan.

Si la base de données cible hello est une base de données SQL Azure, vérifiez SQL Server paramètres du pare-feu pour Azure également.

Consultez hello suivant du magasin de données local toohello de connexion de section tootest hello.

## <a name="data-store-connection-or-driver-related-errors"></a>Erreurs liées à la connexion à la banque de données ou au pilote
Si vous voyez les données à stocker de connexion ou des erreurs liées au pilote, effectuez hello comme suit :

1. Démarrez le Gestionnaire de Configuration de passerelle de gestion de données sur l’ordinateur de passerelle hello.
2. Commutateur toohello **Diagnostics** onglet.
3. Dans **tester la connexion**, ajouter des valeurs de groupe de passerelle hello.
4. Cliquez sur **Test** toosee si vous pouvez vous connecter toohello local source de données à partir de l’ordinateur de passerelle hello à l’aide des informations d’identification et les informations de connexion hello. En cas de tester la connexion hello toujours après l’installation d’un pilote, redémarrage hello passerelle pour qu’il toopick des modifications les plus récentes hello.

![Tester la connexion dans l’onglet Diagnostics](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a>Journaux de la passerelle
### <a name="send-gateway-logs-toomicrosoft"></a>Envoyer tooMicrosoft des journaux de passerelle
Lorsque vous contactez le Support technique de Microsoft tooget aide Résolution des problèmes de passerelle, vous pouvez être invité tooshare vos journaux de la passerelle. Avec la version de hello de passerelle de hello, vous pouvez partager des journaux de la passerelle requises avec deux clics de bouton du Gestionnaire de Configuration passerelle de gestion de données.    

1. Commutateur toohello **Diagnostics** onglet du Gestionnaire de Configuration passerelle de gestion de données.

    ![Onglet Diagnostics de la passerelle de gestion des données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. Cliquez sur **d’envoi de journaux** hello toosee suivant la boîte de dialogue.

    ![Lien Envoyer des journaux de la passerelle de gestion des données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. (Facultatif) Cliquez sur **afficher les journaux** tooreview journaux dans l’Observateur d’événements hello.
4. (Facultatif) Cliquez sur **confidentialité** déclaration de confidentialité des services web de Microsoft tooreview.
5. Lorsque vous êtes satisfait que vous êtes sur le tooupload, cliquez sur **d’envoi de journaux** tooactually envoyer les journaux de hello de hello dernière tooMicrosoft de sept jours pour la résolution des problèmes. Vous devez voir État hello d’opération d’envoi-journaux hello comme indiqué dans hello suivant capture d’écran.

    ![État de l’opération Envoyer des journaux pour la passerelle de gestion des données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. Après que l’opération de hello est terminée, vous voyez une boîte de dialogue comme illustré hello suivant capture d’écran.

    ![État de l’opération Envoyer des journaux pour la passerelle de gestion des données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. Enregistrer hello **ID état** et le partager avec le Support technique de Microsoft. ID du rapport Hello est toolocate utilisé les journaux de passerelle hello que vous avez téléchargé pour le dépannage.  ID du rapport Hello est également enregistrée dans l’Observateur d’événements hello.  Vous pouvez le trouver en examinant les ID d’événement hello « 25 » et vérifiez hello date et heure.

    ![ID du rapport de l’opération Envoyer des journaux pour la passerelle de gestion des données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a>La passerelle d’archive ouvre une session sur l’ordinateur hôte de la passerelle
Dans certains cas, il se peut que vous ayez des problèmes avec la passerelle et que vous ne puissiez pas partager directement les journaux de la passerelle :

* Manuellement, vous installez hello passerelle et inscrivez hello passerelle.
* Vous essayez de passerelle de hello tooregister avec une clé régénérée du Gestionnaire de Configuration passerelle de gestion de données.
* Vous essayez de toosend journaux et le service hôte de passerelle hello ne peut pas être connecté.

Dans ces cas de figure, vous pouvez enregistrer les journaux de la passerelle dans un fichier zip et fournir celui-ci au Support Microsoft. Par exemple, si vous recevez une erreur pendant que vous inscrivez la passerelle hello comme indiqué dans hello suivant capture d’écran.   

![Erreur d’inscription de la passerelle de gestion des données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

Cliquez sur hello **archiver les journaux de la passerelle** link tooarchive et enregistrer les journaux, puis partager le fichier zip de hello avec prise en charge de Microsoft.

![Lien Archiver les journaux de la passerelle de gestion de données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a>Rechercher dans les journaux de la passerelle
Vous trouverez des informations détaillées de passerelle du journal dans les journaux des événements Windows hello.

1. Démarrez l’**Observateur d’événements** Windows.
2. Recherchez les journaux Bonjour **journaux des applications et Services** > **passerelle de gestion des données** dossier.

 Lorsque vous êtes à résoudre les problèmes liés à la passerelle, recherchez les événements de niveau erreur dans l’Observateur d’événements hello.

![Journaux de la passerelle de gestion des données dans l’Observateur d’événements](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
