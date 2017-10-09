---
title: "aaaAdd un magasin d’autorité de certification Java toohello | Documents Microsoft"
description: "Découvrez comment tooadd une autorité de certification certificat toohello Java autorité de certification (cacerts) stocker pour Twilio service ou Azure Service Bus."
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
ms.openlocfilehash: 030e43129580023942dee662e72d2f443167f308
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="adding-a-certificate-toohello-java-ca-certificates-store"></a>Ajout d’un certificat de toohello magasin de certificats d’autorité de certification Java
Hello suit vous montre comment tooadd stocker une autorité de certification certificat toohello Java autorité de certification (cacerts). certificat d’autorité de certification de hello exemple Hello utilisé est requis par hello Twilio service. Les informations fournies plus loin dans la rubrique de hello décrivent comment tooinstall hello autorité de certification du certificat pour hello Azure Service Bus. 

Vous pouvez utiliser toozipping préalable du certificat hello autorité de certification tooadd keytool votre JDK et en l’ajoutant tooyour projet Azure **approot** dossier, ou vous pouvez exécuter une tâche de démarrage Azure qui utilise le certificat de keytool tooadd hello. Cet exemple suppose que vous allez ajouter un certificat d’autorité de certification préalable toohello JDK est compressé. En outre, un certificat d’autorité de certification spécifique servira dans hello exemple, mais les étapes hello d’obtention d’un autre certificat d’autorité de certification et son importation dans hello cacerts magasin serait similaire.

## <a name="tooadd-a-certificate-toohello-cacerts-store"></a>stocker les tooadd un cacerts toohello de certificat
1. À l’invite de commande qui a la valeur du JDK tooyour **jdk\jre\lib\security** dossier, exécutez hello suivant toosee quels certificats sont installés :
   
    `keytool -list -keystore cacerts`
   
    Vous êtes invité à entrer de mot de passe de magasin hello. mot de passe Hello **modifier**. (Si vous souhaitez que le mot de passe toochange hello, consultez la documentation de keytool hello à <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.) Cet exemple suppose que ce certificat hello avec 67:CB:9 d’empreinte digitale MD5 D : C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 n’est pas répertorié, et que vous souhaitez tooimport informatique (ce certificat est requise par hello service Twilio API).
2. Obtenir des certificats de hello dans liste de hello des certificats répertoriés au [les certificats racines GeoTrust](http://www.geotrust.com/resources/root-certificates/). Cliquez sur le lien hello pour certificat hello avec numéro de série 35:DE:F4:CF et enregistrez-le toohello **jdk\jre\lib\security** dossier. Pour des raisons de cet exemple, il a été enregistré le fichier tooa nommé **Equifax\_Secure\_certificat\_Authority.cer**.
3. Importer un certificat hello via hello de commande suivante :
   
    `keytool -keystore cacerts -importcert -alias equifaxsecureca -file Equifax_Secure_Certificate_Authority.cer`
   
    Lorsque vous y êtes invité tootrust ce certificat, si les certificats hello a 67:CB:9 d’empreinte digitale MD5 D : C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4, répondre en tapant **y**.
4. Exécution hello suivant le certificat d’autorité de certification de hello commande tooensure a été importé :
   
    `keytool -list -keystore cacerts`
5. Code postal hello JDK et ajoutez-le tooyour projet Azure **approot** dossier.

Pour plus d'informations sur keytool, consultez la page <http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html>.

## <a name="azure-root-certificates"></a>Certificats racines Azure
Les applications qui utilisent des services Azure (par exemple, Azure Service Bus) doivent tootrust hello Baltimore CyberTrust certificat. (Depuis le 15 avril 2013, Azure a commencé la migration de hello GTE CyberTrust Root Global toohello Baltimore CyberTrust Root. Cette migration a eu plusieurs mois toocomplete.)

Hello Baltimore certificat peut-être déjà être installé dans votre magasin cacerts, par conséquent, n’oubliez pas toorun hello **keytool-liste** commande toosee première s’il existe déjà.

Si vous avez besoin de tooadd hello Baltimore CyberTrust Root, il a 02:00:00:b9 du numéro de série et SHA1 empreinte digitale d4:de:20:d0:5e:66:fc:53:fe:1a:50:88:2 c : 78:db:28:52:ca:e4:74. Il peut être téléchargé à partir de <https://cacert.omniroot.com/bc2025.crt>, enregistré le fichier local de tooa avec l’extension **.cer**, puis importé à l’aide de **keytool** comme indiqué ci-dessus.

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les certificats racine de hello utilisé par Azure, consultez [Migration de certificat racine Azure](http://blogs.msdn.com/b/windowsazure/archive/2013/03/15/windows-azure-root-certificate-migration.aspx).

Pour plus d’informations sur Java, consultez [Azure pour les développeurs Java](/java/azure).

