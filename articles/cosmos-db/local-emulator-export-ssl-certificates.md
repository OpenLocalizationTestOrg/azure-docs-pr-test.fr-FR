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
# <a name="export-hello-azure-cosmos-db-emulator-certificates-for-use-with-java-python-and-nodejs"></a><span data-ttu-id="e99c3-105">Exporter des certificats d’émulateur de base de données Azure Cosmos hello pour une utilisation avec Java, Python et Node.js</span><span class="sxs-lookup"><span data-stu-id="e99c3-105">Export hello Azure Cosmos DB Emulator certificates for use with Java, Python, and Node.js</span></span>

[<span data-ttu-id="e99c3-106">**Télécharger hello émulateur**</span><span class="sxs-lookup"><span data-stu-id="e99c3-106">**Download hello Emulator**</span></span>](https://aka.ms/cosmosdb-emulator)

<span data-ttu-id="e99c3-107">Bonjour Azure Cosmos DB émulateur fournit un environnement local qui émule hello service de base de données Azure Cosmos fins de développement, notamment son utilisation de connexions SSL.</span><span class="sxs-lookup"><span data-stu-id="e99c3-107">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes including its use of SSL connections.</span></span> <span data-ttu-id="e99c3-108">Ce billet illustre l’utilisation des certificats pour une utilisation dans les langues et runtimes qui ne s’intègrent pas hello le magasin de certificats Windows comme Java qui utilise son propre tooexport hello SSL [magasin de certificats](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) et Python qui utilise [wrappers de socket](https://docs.python.org/2/library/ssl.html) et Node.js qui utilise [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="e99c3-108">This post demonstrates how tooexport hello SSL certificates for use in languages and runtimes that do not integrate with hello Windows Certificate Store such as Java which uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) and Python which uses [socket wrappers](https://docs.python.org/2/library/ssl.html) and Node.js which uses [tlsSocket](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span> <span data-ttu-id="e99c3-109">Vous pouvez en savoir plus sur l’émulateur hello dans [hello utilisation Azure Cosmos DB émulateur pour le développement et test](./local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="e99c3-109">You can read more about hello emulator in [Use hello Azure Cosmos DB Emulator for development and testing](./local-emulator.md).</span></span>

<span data-ttu-id="e99c3-110">Ce didacticiel couvre hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="e99c3-110">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e99c3-111">Rotation des certificats</span><span class="sxs-lookup"><span data-stu-id="e99c3-111">Rotating certificates</span></span>
> * <span data-ttu-id="e99c3-112">Exportation du certificat SSL</span><span class="sxs-lookup"><span data-stu-id="e99c3-112">Exporting SSL certificate</span></span>
> * <span data-ttu-id="e99c3-113">Apprendre comment toouse hello certificat dans Java, Python et Node.js</span><span class="sxs-lookup"><span data-stu-id="e99c3-113">Learning how toouse hello certificate in Java, Python, and Node.js</span></span>

## <a name="certification-rotation"></a><span data-ttu-id="e99c3-114">Rotation de certification</span><span class="sxs-lookup"><span data-stu-id="e99c3-114">Certification rotation</span></span>

<span data-ttu-id="e99c3-115">Certificats Bonjour que émulateur Local de la base de données Azure Cosmos sont générés hello première exécution d’émulateur de hello.</span><span class="sxs-lookup"><span data-stu-id="e99c3-115">Certificates in hello Azure Cosmos DB Local Emulator are generated hello first time hello emulator is run.</span></span> <span data-ttu-id="e99c3-116">Il existe deux certificats.</span><span class="sxs-lookup"><span data-stu-id="e99c3-116">There are two certificates.</span></span> <span data-ttu-id="e99c3-117">Un est utilisé pour la connexion émulateur local de toohello et l’autre pour la gestion des clés secrètes dans l’émulateur de hello.</span><span class="sxs-lookup"><span data-stu-id="e99c3-117">One used for connecting toohello local emulator and one for managing secrets within hello emulator.</span></span> <span data-ttu-id="e99c3-118">certificat Hello tooexport est le certificat de connexion hello avec le nom convivial de hello « DocumentDBEmulatorCertificate ».</span><span class="sxs-lookup"><span data-stu-id="e99c3-118">hello certificate you want tooexport is hello connection certificate with hello friendly name "DocumentDBEmulatorCertificate".</span></span>

<span data-ttu-id="e99c3-119">Les deux certificats peuvent être régénérées en cliquant sur **réinitialiser les données** comme indiqué ci-dessous à partir de l’émulateur de base de données Azure Cosmos en cours d’exécution dans hello barre d’état Windows.</span><span class="sxs-lookup"><span data-stu-id="e99c3-119">Both certificates can be regenerated by clicking **Reset Data** as shown below from Azure Cosmos DB Emulator running in hello Windows Tray.</span></span> <span data-ttu-id="e99c3-120">Régénérer les certificats hello et installés dans le magasin de certificats hello Java ou les utilisés ailleurs, vous devez tooupdate leur, sinon votre application se connecte ne sont plus émulateur local de toohello.</span><span class="sxs-lookup"><span data-stu-id="e99c3-120">If you regenerate hello certificates and have installed them into hello Java certificate store or used them elsewhere you will need tooupdate them, otherwise your application will no longer connect toohello local emulator.</span></span>

![Réinitialiser les données de l’émulateur local Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-reset-data.png)

## <a name="how-tooexport-hello-azure-cosmos-db-ssl-certificate"></a><span data-ttu-id="e99c3-122">Comment tooexport hello certificat SSL de base de données Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="e99c3-122">How tooexport hello Azure Cosmos DB SSL certificate</span></span>

1. <span data-ttu-id="e99c3-123">Démarrez le Gestionnaire de certificats Windows hello en exécutant certlm.msc et accédez toohello personnel -> dossier de certificats et certificat hello ouvert avec le nom convivial de hello **DocumentDbEmulatorCertificate**.</span><span class="sxs-lookup"><span data-stu-id="e99c3-123">Start hello Windows Certificate manager by running certlm.msc and navigate toohello Personal->Certificates folder and open hello certificate with hello friendly name **DocumentDbEmulatorCertificate**.</span></span>

    ![Étape 1 - Exporter dans l’émulateur local Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-1.png)

2. <span data-ttu-id="e99c3-125">Cliquez sur **Détails**, puis sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e99c3-125">Click on **Details** then **OK**.</span></span>

    ![Étape 2 - Exporter dans l’émulateur local Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-2.png)

3. <span data-ttu-id="e99c3-127">Cliquez sur **copier tooFile...** .</span><span class="sxs-lookup"><span data-stu-id="e99c3-127">Click **Copy tooFile...**.</span></span>

    ![Étape 3 - Exporter dans l’émulateur local Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-3.png)

4. <span data-ttu-id="e99c3-129">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e99c3-129">Click **Next**.</span></span>

    ![Étape 4 - Exporter dans l’émulateur local Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-4.png)

5. <span data-ttu-id="e99c3-131">Cliquez sur l’option de **refus d’exportation de la clé privée**, puis sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e99c3-131">Click **No, do not export private key**, then click **Next**.</span></span>

    ![Étape 5 - Exporter dans l’émulateur local Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-5.png)

6. <span data-ttu-id="e99c3-133">Cliquez sur **X.509 encodé en base 64 (.cer)**, puis sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e99c3-133">Click on **Base-64 encoded X.509 (.CER)** and then **Next**.</span></span>

    ![Étape 6 - Exporter dans l’émulateur local Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-6.png)

7. <span data-ttu-id="e99c3-135">Nommez le certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="e99c3-135">Give hello certificate a name.</span></span> <span data-ttu-id="e99c3-136">Ici, cliquez sur **documentdbemulatorcert**, puis sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e99c3-136">In this case **documentdbemulatorcert** and then click **Next**.</span></span>

    ![Étape 7 - Exporter dans l’émulateur local Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-7.png)

8. <span data-ttu-id="e99c3-138">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="e99c3-138">Click **Finish**.</span></span>

    ![Étape 8 - Exporter dans l’émulateur local Azure Cosmos DB](./media/local-emulator-export-ssl-certificates/database-local-emulator-export-step-8.png)

## <a name="how-toouse-hello-certificate-in-java"></a><span data-ttu-id="e99c3-140">Comment toouse hello certificat dans Java</span><span class="sxs-lookup"><span data-stu-id="e99c3-140">How toouse hello certificate in Java</span></span>

<span data-ttu-id="e99c3-141">Lors de l’exécution des applications Java ou MongoDB les applications qui utilisent le client de Java hello il s’agit de plus facile certificat de hello tooinstall dans le magasin de certificats par défaut hello Java à passage hello »-Djavax.net.ssl.trustStore=<keystore> - Djavax.net.ssl.trustStorePassword= «<password>« indicateurs.</span><span class="sxs-lookup"><span data-stu-id="e99c3-141">When running Java applications or MongoDB applications that use hello Java client it is easier tooinstall hello certificate into hello Java default certificate store than passing hello "-Djavax.net.ssl.trustStore=<keystore> -Djavax.net.ssl.trustStorePassword="<password>" flags.</span></span> <span data-ttu-id="e99c3-142">Par exemple les hello inclus [application de démonstration de Java](https://localhost:8081/_explorer/index.html) varie selon le magasin de certificats par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="e99c3-142">For example hello included [Java Demo application](https://localhost:8081/_explorer/index.html) depends on hello default certificate store.</span></span>

<span data-ttu-id="e99c3-143">Suivez les instructions de hello Bonjour [Ajout d’un toohello certificat magasin de certificats d’autorité de certification Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello X.509 certificat dans le magasin de certificats Java hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="e99c3-143">Follow hello instructions in hello [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store) tooimport hello X.509 certificate into hello default Java certificate store.</span></span> <span data-ttu-id="e99c3-144">Gardez vous travaillerez dans le répertoire JAVA_HOME hello % lors de l’exécution keytool.</span><span class="sxs-lookup"><span data-stu-id="e99c3-144">Keep in mind you will be working in hello %JAVA_HOME% directory when running keytool.</span></span>

<span data-ttu-id="e99c3-145">Une fois hello « CosmosDBEmulatorCertificate » SSL certificat est installé votre application doit être en mesure de tooconnect et utilisez hello émulateur de base de données local Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="e99c3-145">Once hello "CosmosDBEmulatorCertificate" SSL certificate is installed your application should be able tooconnect and use hello local Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="e99c3-146">Si vous continuez à des difficultés à toohave vous souhaiterez peut-être toofollow hello [débogage des connexions SSL/TLS](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) l’article.</span><span class="sxs-lookup"><span data-stu-id="e99c3-146">If you continue toohave trouble you may want toofollow hello [Debugging SSL/TLS Connections](http://docs.oracle.com/javase/7/docs/technotes/guides/security/jsse/ReadDebug.html) article.</span></span> <span data-ttu-id="e99c3-147">Il est très probable certificat de hello n’est pas installé dans le magasin de %JAVA_HOME%/jre/lib/security/cacerts hello.</span><span class="sxs-lookup"><span data-stu-id="e99c3-147">It is very likely hello certificate is not installed into hello %JAVA_HOME%/jre/lib/security/cacerts store.</span></span> <span data-ttu-id="e99c3-148">Pour exemple, si vous avez plusieurs versions installées de Java votre application peut utiliser un magasin cacerts différents que hello une que mise à jour.</span><span class="sxs-lookup"><span data-stu-id="e99c3-148">For example if you have multiple installed versions of Java your application may be using a different cacerts store than hello one you updated.</span></span>

## <a name="how-toouse-hello-certificate-in-python"></a><span data-ttu-id="e99c3-149">Comment toouse hello certificat dans Python</span><span class="sxs-lookup"><span data-stu-id="e99c3-149">How toouse hello certificate in Python</span></span>

<span data-ttu-id="e99c3-150">Par hello de valeur par défaut [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) pour hello API DocumentDB pas essayer et utiliser le certificat SSL de hello lors de la connexion émulateur local de toohello.</span><span class="sxs-lookup"><span data-stu-id="e99c3-150">By default hello [Python SDK(version 2.0.0 or higher)](documentdb-sdk-python.md) for hello DocumentDB API will not try and use hello SSL certificate when connecting toohello local emulator.</span></span> <span data-ttu-id="e99c3-151">Si toutefois vous souhaitez que la validation de SSL toouse vous pouvez suivre les exemples hello Bonjour [Python de socket wrappers](https://docs.python.org/2/library/ssl.html) documentation.</span><span class="sxs-lookup"><span data-stu-id="e99c3-151">If however you want toouse SSL validation you can follow hello examples in hello [Python socket wrappers](https://docs.python.org/2/library/ssl.html) documentation.</span></span>

## <a name="how-toouse-hello-certificate-in-nodejs"></a><span data-ttu-id="e99c3-152">Comment toouse hello certificat dans Node.js</span><span class="sxs-lookup"><span data-stu-id="e99c3-152">How toouse hello certificate in Node.js</span></span>

<span data-ttu-id="e99c3-153">Par hello de valeur par défaut [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) pour hello API DocumentDB pas essayer et utiliser le certificat SSL de hello lors de la connexion émulateur local de toohello.</span><span class="sxs-lookup"><span data-stu-id="e99c3-153">By default hello [Node.js SDK(version 1.10.1 or higher)](documentdb-sdk-node.md) for hello DocumentDB API will not try and use hello SSL certificate when connecting toohello local emulator.</span></span> <span data-ttu-id="e99c3-154">Si toutefois vous souhaitez que la validation de SSL toouse vous pouvez suivre les exemples hello Bonjour [documentation sur Node.js](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span><span class="sxs-lookup"><span data-stu-id="e99c3-154">If however you want toouse SSL validation you can follow hello examples in hello [Node.js documentation](https://nodejs.org/api/tls.html#tls_tls_connect_options_callback).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e99c3-155">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e99c3-155">Next steps</span></span>

<span data-ttu-id="e99c3-156">Dans ce didacticiel, vous avez effectué les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="e99c3-156">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e99c3-157">Rotation des certificats</span><span class="sxs-lookup"><span data-stu-id="e99c3-157">Rotated certificates</span></span>
> * <span data-ttu-id="e99c3-158">Certificat SSL de hello exportée</span><span class="sxs-lookup"><span data-stu-id="e99c3-158">Exported hello SSL certificate</span></span>
> * <span data-ttu-id="e99c3-159">Appris comment toouse hello certificat dans Java, Python et Node.js</span><span class="sxs-lookup"><span data-stu-id="e99c3-159">Learned how toouse hello certificate in Java, Python and Node.js</span></span>

<span data-ttu-id="e99c3-160">Vous pouvez maintenant toohello section Concepts pour plus d’informations sur la base de données Cosmos.</span><span class="sxs-lookup"><span data-stu-id="e99c3-160">You can now proceed toohello Concepts section for more information about Cosmos DB.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e99c3-161">Diffusion mondiale</span><span class="sxs-lookup"><span data-stu-id="e99c3-161">Global distribution</span></span>](distribute-data-globally.md) 
