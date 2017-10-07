---
title: "certificats de Azure Cosmos DB émulateur hello aaaExport | Documents Microsoft"
description: "Lorsque vous développez dans les langues et runtimes qui n’utilisent pas de magasin de certificats Windows hello, vous devez tooexport et gérer des certificats SSL de hello. Cet article vous fournit des instructions pas à pas."
services: cosmos-db
documentationcenter: 
keywords: "Émulateur Azure Cosmos DB"
author: voellm
manager: jhubbard
editor: 
ms.assetid: ef43deda-c2e9-4193-99e2-7f6a88a0319f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: tvoellm
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: db56cda856fccf93d71ae5b21c4090ccb9aa40a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a>Exporter des certificats d’émulateur de base de données Azure Cosmos hello pour une utilisation avec Java, Python et Node.js

[**Télécharger hello émulateur**](https://aka.ms/cosmosdb-emulator)

Bonjour Azure Cosmos DB émulateur fournit un environnement local qui émule hello service de base de données Azure Cosmos fins de développement, notamment son utilisation de connexions SSL. Ce billet illustre l’utilisation des certificats pour une utilisation dans les langues et runtimes qui ne s’intègrent pas hello le magasin de certificats Windows comme Java qui utilise son propre tooexport hello SSL [magasin de certificats](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) et Python qui utilise [wrappers de socket](https://docs.python.org/2/library/ssl.html) et Node.js qui utilise [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback). Vous pouvez en savoir plus sur l’émulateur hello dans [hello utilisation Azure Cosmos DB émulateur pour le développement et test](./local-emulator.md).

Ce didacticiel couvre hello tâches suivantes :

> [!div class="checklist"]
> * Rotation des certificats
> * Exportation du certificat SSL
> * Apprendre comment toouse hello certificat dans Java, Python et Node.js

## <a name="certification-rotation"></a>Rotation de certification

Certificats Bonjour que émulateur Local de la base de données Azure Cosmos sont générés hello première exécution d’émulateur de hello. Il existe deux certificats. Un est utilisé pour la connexion émulateur local de toohello et l’autre pour la gestion des clés secrètes dans l’émulateur de hello. certificat Hello tooexport est le certificat de connexion hello avec le nom convivial de hello « DocumentDBEmulatorCertificate ».

Les deux certificats peuvent être régénérées en cliquant sur **réinitialiser les données** comme indiqué ci-dessous à partir de l’émulateur de base de données Azure Cosmos en cours d’exécution dans hello barre d’état Windows. Régénérer les certificats hello et installés dans le magasin de certificats hello Java ou les utilisés ailleurs, vous devez tooupdate leur, sinon votre application se connecte ne sont plus émulateur local de toohello.

![Réinitialiser les données de l’émulateur local Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a>Comment tooexport hello certificat SSL de base de données Azure Cosmos

1. Démarrez le Gestionnaire de certificats Windows hello en exécutant certlm.msc et accédez toohello personnel -> dossier de certificats et certificat hello ouvert avec le nom convivial de hello **DocumentDbEmulatorCertificate**.

    ![Étape 1 - Exporter dans l’émulateur local Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. Cliquez sur **Détails**, puis sur **OK**.

    ![Étape 2 - Exporter dans l’émulateur local Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. Cliquez sur **copier tooFile...** .

    ![Étape 3 - Exporter dans l’émulateur local Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. Cliquez sur **Suivant**.

    ![Étape 4 - Exporter dans l’émulateur local Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. Cliquez sur l’option de **refus d’exportation de la clé privée**, puis sur **Suivant**.

    ![Étape 5 - Exporter dans l’émulateur local Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. Cliquez sur **X.509 encodé en base 64 (.cer)**, puis sur **Suivant**.

    ![Étape 6 - Exporter dans l’émulateur local Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. Nommez le certificat de hello. Ici, cliquez sur **documentdbemulatorcert**, puis sur **Suivant**.

    ![Étape 7 - Exporter dans l’émulateur local Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. Cliquez sur **Terminer**.

    ![Étape 8 - Exporter dans l’émulateur local Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a>Comment toouse hello certificat dans Java

Lors de l’exécution des applications Java ou MongoDB les applications qui utilisent le client de Java hello il s’agit de plus facile certificat de hello tooinstall dans le magasin de certificats par défaut hello Java à passage hello »-Djavax.net.ssl.trustStore=<keystore> - Djavax.net.ssl.trustStorePassword= «<password>« indicateurs. Par exemple les hello inclus [application de démonstration de Java](https://localhost:8081/_explorer/index.html) varie selon le magasin de certificats par défaut hello.

Suivez les instructions de hello Bonjour [Ajout d’un toohello certificat magasin de certificats d’autorité de certification Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello X.509 certificat dans le magasin de certificats Java hello par défaut. Gardez vous travaillerez dans le répertoire JAVA_HOME hello % lors de l’exécution keytool.

Une fois hello « CosmosDBEmulatorCertificate » SSL certificat est installé votre application doit être en mesure de tooconnect et utilisez hello émulateur de base de données local Azure Cosmos. Si vous continuez à des difficultés à toohave vous souhaiterez peut-être toofollow hello [débogage des connexions SSL/TLS](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) l’article. Il est très probable certificat de hello n’est pas installé dans le magasin de %JAVA_HOME%/jre/lib/security/cacerts hello. Pour exemple, si vous avez plusieurs versions installées de Java votre application peut utiliser un magasin cacerts différents que hello une que mise à jour.

## <a name="how-toouse-hello-certificate-in-python"></a>Comment toouse hello certificat dans Python

Par hello de valeur par défaut [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) pour hello API DocumentDB pas essayer et utiliser le certificat SSL de hello lors de la connexion émulateur local de toohello. Si toutefois vous souhaitez que la validation de SSL toouse vous pouvez suivre les exemples hello Bonjour [Python de socket wrappers](https://docs.python.org/2/library/ssl.html) documentation.

## <a name="how-toouse-hello-certificate-in-nodejs"></a>Comment toouse hello certificat dans Node.js

Par hello de valeur par défaut [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) pour hello API DocumentDB pas essayer et utiliser le certificat SSL de hello lors de la connexion émulateur local de toohello. Si toutefois vous souhaitez que la validation de SSL toouse vous pouvez suivre les exemples hello Bonjour [documentation sur Node.js](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez effectué les éléments suivants de hello :

> [!div class="checklist"]
> * Rotation des certificats
> * Certificat SSL de hello exportée
> * Appris comment toouse hello certificat dans Java, Python et Node.js

Vous pouvez maintenant toohello section Concepts pour plus d’informations sur la base de données Cosmos.

> [!div class="nextstepaction"]
> [Diffusion mondiale](distribute-data-globally.md) 
