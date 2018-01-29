---
title: "Ajout d'un certificat au magasin d'autorité de certification Java | Microsoft Docs"
description: "Découvrez comment ajouter un certificat d'autorité de certification au magasin de certificats (cacerts) de l'autorité de certification Java pour le service Twilio ou le Azure Service Bus."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: d3699b0a-835c-43fb-844d-9c25344e5cda
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: b6e1a305e19415ab1c4b4c208dac98ad1e2689c6
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/11/2017
---
# <a name="adding-a-certificate-to-the-java-ca-certificates-store"></a>Ajout d'un certificat au magasin de certificats d'autorité de certification Java
La procédure suivante présente l'ajout d'un certificat d'autorité de certification au magasin de certificats d'autorité de certification Java (cacerts). Prenons comme exemple un certificat d'autorité de certification requis par le service Twilio. Les informations fournies plus loin dans cette rubrique décrivent l’installation d’un certificat d’autorité de certification pour Azure Service Bus. 

Vous pouvez utiliser keytool pour ajouter le certificat d'autorité de certification avant de compresser le JDK et de l'ajouter au dossier **approot** de votre projet Azure. Vous pouvez également utiliser une tâche de démarrage Azure qui utilise keytool pour ajouter le certificat. Cet exemple part du principe que vous allez ajouter un certificat d'autorité de certification avant de compresser le JDK. Par ailleurs, nous allons utiliser un certificat d'autorité de certification spécifique. Si vous décidiez d'en obtenir un autre et de l'importer dans le magasin cacerts, la procédure serait semblable.

## <a name="to-add-a-certificate-to-the-cacerts-store"></a>Ajout d'un certificat au magasin cacerts
1. À une invite de commandes administrateur définie pour le dossier **jdk\jre\lib\security** de votre JDK, exécutez la commande ci-après pour afficher les certificats installés :
   
    `keytool -list -keystore cacerts`
   
    Vous êtes invité à entrer le mot de passe du magasin. Le mot de passe par défaut est **changeit**. (Pour le modifier, consultez la documentation relative à keytool à la page <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) Cet exemple suppose que le certificat avec l'empreinte numérique MD5 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 n'est pas répertorié, et que vous souhaitez l'importer (ce certificat spécifique est requis par le service de l'API Twilio).
2. Obtenez le certificat dans la liste de certificats répertoriée dans la page [Certificats racines GeoTrust](http://www.geotrust.com/resources/root-certificates/). Cliquez avec le bouton droit sur le lien du certificat avec le numéro de série 35:DE:F4:CF et enregistrez-le dans le dossier **jdk\jre\lib\security**. Dans le cadre de cet exemple, il est enregistré dans un fichier nommé **Equifax\_Secure\_Certificate\_Authority.cer**.
3. Importez le certificat via la commande suivante :
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    Lorsque vous êtes invité à approuver ce certificat, s'il possède l'empreinte numérique MD5 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, répondez en tapant **y**.
4. Exécutez la commande suivante pour vous assurer que le certificat d'autorité de certification a été correctement importé :
   
    `keytool -list -keystore cacerts`
5. Compressez le JDK et ajoutez-le au dossier **approot** de votre projet Azure.

Pour plus d'informations sur keytool, consultez la page <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.

## <a name="azure-root-certificates"></a>Certificats racines Azure
Les applications qui utilisent des services Azure (tels qu'Azure Service Bus) doivent approuver le certificat racine Baltimore CyberTrust. (Dès le 15 avril 2013, Azure a commencé à migrer du certificat racine GTE CyberTrust Global au certificat racine Baltimore CyberTrust. Cette migration a pris plusieurs mois.)

Il se peut que le certificat Baltimore soit déjà installé dans votre magasin cacerts. Il est donc préférable de commencer par exécuter la commande **keytool -list** pour vérifier si c'est le cas.

Si vous devez ajouter le certificat racine Baltimore CyberTrust, son numéro de série est le 02:00:00:b9 et son empreinte digitale SHA1 est la suivante : d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2 c: 78:db:28:52:ca:e4:74. Ce dernier peut être téléchargé à partir de <https://cacert.omniroot.com/bc2025.crt>, enregistré dans un fichier local avec l'extension **.cer**, puis importé à l'aide de **keytool** comme indiqué ci-dessus.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d'informations sur les certificats racines utilisés par Azure, consultez [Migration des certificats racines Azure](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).

Pour plus d’informations sur Java, consultez [Azure pour les développeurs Java](/java/azure).

