---
title: "aaaConfigure l’authentification avec Amazon Web Services | Documents Microsoft"
description: "Cet article décrit comment toocreate et valider les informations d’identification AWS pour les runbook dans Azure Automation, la gestion des ressources AWS."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
keywords: authentification AWS, configurer aws
ms.assetid: b6dde4bb-26ac-4876-9aa9-e586bed30d6b
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/14/2017
ms.author: magoedte
ms.openlocfilehash: 1e312df2422d9da3cd3331fe01aeaa3a43c8b9d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-amazon-web-services"></a>Authentification des Runbooks avec Amazon Web Services
Il est possible d’automatiser les tâches courantes avec les ressources Amazon Web Services (AWS) à l’aide des runbooks Automation dans Azure.  Vous pouvez automatiser de nombreuses tâches dans AWS à l’aide des runbooks Automation, tout comme avec les ressources dans Azure.  Pour ce faire, deux choses sont nécessaires :

* Un abonnement AWS et un ensemble d’informations d’identification.  Plus précisément, votre clé d’accès AWS et votre clé secrète.  Pour plus d’informations, consultez l’article de hello [utilisant les informations d’identification AWS](http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html).
* Un abonnement Azure et un compte Automation.  Pour plus d’informations sur la configuration d’un compte Azure Automation, consultez l’article de hello [configurer Azure compte d’identification](automation-sec-configure-azure-runas-account.md).  

tooauthenticate avec AWS, vous devez spécifier un ensemble de tooauthenticate des informations d’identification AWS vos runbook en cours d’exécution à partir d’Azure Automation. Si vous avez déjà un compte Automation créé et que vous souhaitez toouse que tooauthenticate avec AWS, vous pouvez suivre les étapes de hello Bonjour suivant la section.  Si vous voulez toodedicated un compte pour les ressources de procédures opérationnelles ciblé AWS, vous devez d’abord créer un nouveau [compte Automation](automation-offering-get-started.md) (ignorer hello option toocreate un principal de service), puis suivez les étapes de hello ci-dessous.

## <a name="configure-automation-account"></a>Configuration d’un compte Automation
Pour toocommunicate Azure Automation avec AWS, vous commencez par devez tooretrieve vos informations d’identification AWS et les stockez en tant que ressources dans Azure Automation.  Effectuer hello suivant les étapes décrites dans le document AWS hello [la gestion des clés d’accès pour votre compte AWS](http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html) toocreate une hello clé d’accès et de copie **ID de clé d’accès** et **cléd’accèsdeclésecrète** (vous pouvez également télécharger toostore de votre fichier de clé dans un endroit sûr il).

Une fois que vous avez créé et copié vos clés de sécurité AWS, vous devez toocreate une ressource d’informations d’identification avec un toosecurely de compte Azure Automation les stocker et de les référencer avec vos runbooks.  Suivez les étapes de hello dans la section de hello **toocreate une information d’identification** Bonjour [d’informations d’identification de ressources dans Azure Automation](automation-credentials.md#to-create-a-new-credential-asset-with-the-azure-portal) l’article et entrez hello informations suivantes :

1. Bonjour **nom** , entrez **AWScred** ou une valeur appropriée, suivant vos normes d’affectation de noms.  
2. Bonjour **nom d’utilisateur** zone votre **ID d’accès** et votre **clé d’accès Secret** Bonjour **mot de passe** et **confirmer mot de passe** boîte.   

## <a name="next-steps"></a>Étapes suivantes
* Article de solution hello Reivew [automatiser le déploiement d’une machine virtuelle dans Amazon Web Services](automation-scenario-aws-deployment.md) toolearn des tâches de toocreate runbooks tooautomate dans AWS.

