---
title: aaaMigrating les Solutions EDI BizTalk Server tooBizTalk Guide technique des Services | Documents Microsoft
description: "Migrer EDI tooMABS ; Microsoft Azure BizTalk Services"
services: biztalk-services
documentationcenter: na
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 61c179fa-3f37-495b-8016-dee7474fd3a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 34cca3c939a6a7845a860ead6858287000d03ee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-biztalk-server-edi-solutions-toobiztalk-services-technical-guide"></a>Migrer des Services tooBizTalk les Solutions EDI BizTalk Server : Guide technique

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Auteurs : Tim Wieman et Nitin Mehrotra

Relecteurs : Karthik Bharthy

Écrit avec : Microsoft Azure BizTalk Services : version de février 2014.

## <a name="introduction"></a>Introduction
Données de l’échange EDI (Electronic) est un des hello plus répandues qui échange électronique des données, également appelé en tant que transactions Business-to-Business ou B2B. BizTalk Server a été prise en charge EDI de dix ans, depuis la version de BizTalk Server initiale hello. Avec les Services BizTalk, Microsoft continue de prise en charge de hello pour les solutions EDI sur la plateforme de Microsoft Azure hello. Les transactions B2B sont principalement externe tooan organisation, et par conséquent il est plus facile tooimplement si elle a été implémentée sur une plateforme cloud. Microsoft Azure fournit cette fonctionnalité via BizTalk Services.

Alors que certains clients adoptent les Services BizTalk comme plateforme « greenfield » pour les nouvelles solutions EDI, de nombreux clients disposent déjà de solutions EDI BizTalk Server peut également toomigrate tooAzure. BizTalk Services EDI étant hello en fonction de son architecture même clé entités architecture de EDI BizTalk Server (partenaires commerciaux, entités, accords), il est possible de toomigrate EDI BizTalk Server artefacts tooBizTalk de services.

Ce document décrit certaines des différences de hello liés à la migration tooBizTalk d’artefacts EDI BizTalk Server Services. Ce document suppose une connaissance pratique du traitement EDI BizTalk Server et des accords de partenariat commercial. Pour plus d'informations sur l'EDI BizTalk Server, consultez [Gestion des partenaires commerciaux à l'aide de BizTalk Server](https://msdn.microsoft.com/library/bb259970.aspx).

## <a name="which-version-of-biztalk-server-edi-artifacts-can-be-migrated-toobiztalk-services"></a>La version d’artefacts EDI BizTalk Server peut être migrés tooBizTalk Services ?
Hello EDI BizTalk Server module a été nettement amélioré pour BizTalk Server 2010, lorsqu’elle était nouvelle version tooinclude partenaires, les profils et accords. Utilise des Services BizTalk hello même hello tooorganize de modèle des partenaires commerciaux et hello départements au sein de ces partenaires. Par conséquent, les artefacts à partir de BizTalk Server 2010 et tooBizTalk de versions ultérieur de migration EDI Services, est un processus beaucoup plus simple. toomigrate des artefacts EDI associés tooBizTalk de versions antérieures Server 2010, vous devez tout d’abord mettre à niveau tooBizTalk Server 2010, puis migrer vos artefacts EDI tooBizTalk Services.

## <a name="scenariosmessage-flow"></a>Flux de messages/scénarios
Comme avec BizTalk Server, le traitement EDI dans BizTalk Services repose sur une solution de gestion des partenaires commerciaux (TPM). Hello solution GPC a hello suivant composants clés :

* les partenaires commerciaux, qui représentent l'organisation dans une transaction B2B ;
* les profils, qui représentent les divisions d'un partenaire commercial ;
* Négociation des accords de partenariat (ou accords), qui représentent des accords commerciaux de hello entre deux partenaires/profils.

Hello suivant illustration décrit les similitudes hello, ainsi que les différences, entre une solution EDI BizTalk Server et de la solution EDI de BizTalk Services :

![][EDImessageflow]

Hello principales différences et similitudes, entre un flux de solution EDI dans BizTalk Server et les Services BizTalk sont :

* Comme BizTalk Server utilise un tooreceive du pipeline EDIReceive un message EDI et un toosend de pipeline EDISend un message EDI, les Services BizTalk utilise un tooreceive de pont de réception EDI et d’un toosend de pont d’envoi EDI messages EDI. Dans BizTalk Server, hello pipelines sont associés à un accord à l’aide d’envoi ou les ports de réception. Dans les Services BizTalk, accord hello proprement dit désigne hello envoi ou de pont de réception.
* Dans BizTalk Server, une fois le processus de pipeline EDIReceive hello hello message EDI, le message de type hello est enregistrée représente tooa de la base de données SQL Server. pipeline EdiSend de Hello puis récupère à partir de la base de données SQL Server hello message de type hello, traite, puis l’envoie toohello partenaire commercial.
  
    Dans les Services BizTalk, après hello EDI reçu de message de pont processus hello EDI, il achemine le processus externe du tooan message hello. les processus externes Hello peut s’exécuter sur Microsoft Azure ou localement. les processus externes Hello doivent acheminer hello toohello de message d’envoi EDI pont ; pont d’envoi Hello n’extrait pas intrinsèquement le message de type hello. Après le traitement du message hello, hello pont d’envoi EDI achemine le partenaire commercial du toohello message hello.

Les Services BizTalk fournit une tooquickly d’expérience faciles à utiliser la configuration créer et déployer un accord B2B entre partenaires commerciaux sans configurer tout calcul de Microsoft Azure instances (rôles Web ou de travail), les bases de données Microsoft Azure SQL ou tout autre Comptes de stockage Microsoft Azure. Des scénarios plus complexes nécessiteront le dans le flux de travail ou d’autres traitements « contours hello » d’un accord de partenariat commercial, autrement dit, avant ou après le traitement du pont EDI d’accord partenaire commercial. Dans les détails, hello séquences d’événements suivantes se produisent pendant un message EDI dans BizTalk Services.

1. Un message EDI est reçu du partenaire commercial Fabrikam.  Pour recevoir les messages EDI des partenaires commerciaux, BizTalk Services prend en charge les protocoles de transport comme FTP, SFTP, AS2 et HTTP/S.
2. Hello commerciaux traitement côté réception de l’accord partenaire désassemble le format de tooXML message hello EDI.  Vous pouvez acheminer hello désassemblé EDI message (au format XML) tooService Bus points de terminaison comme un point de terminaison de relais Service Bus, rubrique Service Bus, file d’attente du Bus de Service ou un pont BizTalk Services.
3. Hello des messages XML désassemblés peuvent ensuite être reçus à partir du point de terminaison hello pour leur traitement.  Ces points de terminaison pu être traités par un composant sur site ou un calcul de Microsoft Azure toofurther processus hello message d’instance dans un service Windows Workflow (WF) ou Windows Communication Foundation (WCF), par exemple.
4. Hello « traitement côté envoi » de l’accord de partenariat commercial hello puis assemble le message de salutation XML dans le format EDI et l’envoie tootrading partenaire, Contoso.  Pour envoyer des messages EDI tootrading partenaires, BizTalk Services prend en charge hello mêmes protocoles que ceux utilisés pour recevoir les messages EDI.

Ce document fournit des conseils conceptuels sur certaines tooBizTalk artefacts EDI BizTalk Server différent de hello migration des Services.

## <a name="sendreceive-ports-tootrading-partners"></a>Ports d’envoi/réception tooTrading partenaires
Dans BizTalk Server permet de paramétrer les messages EDI/XML tooreceive Ports de réception et les emplacements de réception des partenaires commerciaux, et vous configurez le partenaire tootrading messages Ports d’envoi toosend EDI/XML. Vous liez ensuite ces tooa de ports à l’aide de la console d’Administration de BizTalk Server hello d’accord de partenariat commercial. Dans les Services BizTalk, hello emplacements de réception des messages de partenaires commerciaux et où vous envoyez les partenaires de tootrading de messages sont configurés en tant que partie de hello lui-même (dans le cadre des paramètres de Transport) des accord de partenariat commercial Bonjour portail BizTalk Services .  Par conséquent, vous ne pas vraiment possèdent hello concept de « ports d’envoi » et « emplacements de réception », en soi, dans les Services BizTalk. Pour plus d’informations, consultez la page [Création d’accords](https://msdn.microsoft.com/library/windowsazure/hh689908.aspx).

## <a name="pipelines-bridges"></a>Pipelines (ponts)
Dans l’EDI de BizTalk Server, les pipelines sont des entités de traitement de message qui peuvent également inclure une logique personnalisée pour les fonctionnalités de traitement spécifiques, comme requis par l’application hello. Pour les Services BizTalk, hello équivalent serait un pont EDI. Toutefois dans BizTalk Services, pour l’instant, les ponts EDI hello sont « fermés ».  Autrement dit, vous ne peut pas ajouter votre propre pont EDI de tooan des activités personnalisées. Tout traitement personnalisé doit être effectuée en dehors de pont EDI de hello dans votre application, avant ou après le message de type hello passe à pont hello configuré dans le cadre de l’accord de partenariat commercial de hello. Les ponts IAE offrent un traitement personnalisé hello option toodo. Si vous souhaitez un traitement personnalisé, vous pouvez utiliser des ponts IAE avant ou après que le message de type hello est traité par le pont EDI de hello. Pour plus d’informations, consultez [comment tooInclude du Code personnalisé dans les ponts](https://msdn.microsoft.com/library/azure/dn232389.aspx).

Vous pouvez insérer un flux de publication/abonnement avec le code personnalisé et/ou utiliser les files d’attente et rubriques de messagerie avant hello accord de partenariat commercial reçoit le message de type hello ou après que l’accord de hello traite le message de type hello et achemine le point de terminaison de Service Bus tooa Service Bus.

Consultez **scénarios/flux de messages** dans cette rubrique pour le modèle de flux de messages hello.

## <a name="agreements"></a>Accords
Si vous êtes familiarisé avec hello Qu'accords de partenariat commercial BizTalk Server 2010 utilisés pour le traitement EDI, les Services BizTalk accords de partenariat commercial sembler très familière. La plupart des paramètres sont hello même contrat d’hello et utilisation hello même terminologie. Dans certains cas, hello paramètres de l’accord est beaucoup plus simple toohello comparé mêmes paramètres dans BizTalk Server. Microsoft Azure BizTalk Services prend en charge le transport X12, EDIFACT et AS2.

Microsoft Azure BizTalk Services fournit également un **TPM Data Migration** outil toomigrate des partenaires commerciaux et les contrats à partir de BizTalk Server Trading Partner module tooBizTalk portail de Services. outil de Migration de données GPC Hello est disponible dans le cadre d’un package d’outils, qui peut être téléchargé à partir de hello [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057). package de Hello comprend également un fichier qui fournit des instructions sur comment toouse hello outil et informations de dépannage de base pour hello outil.

## <a name="schemas"></a>Schémas
BizTalk Services fournit des schémas EDI qui peuvent être utilisés dans des solutions BizTalk Services.  En outre, les schémas EDI BizTalk Server permet également aux Services BizTalk, car le nœud racine de hello du schéma EDI de hello est identique à BizTalk Server, ainsi que les Services BizTalk. Par conséquent, vous être en mesure de toodirectly take vos schémas EDI BizTalk Server et les utiliser dans les solutions EDI hello que vous développez à l’aide de BizTalk Services. Vous pouvez également télécharger les schémas hello du hello [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057).

## <a name="maps-transforms"></a>Mappages (transformations)
Les mappages de BizTalk Server sont appelés transformations dans BizTalk Services. Migration des mappages depuis tooBizTalk BizTalk Server que peuvent prendre l’une des Services hello tooachieve de tâches plus complexe (selon la complexité du mappage). outil de mappage de Hello utilisé pour les Services BizTalk est différent dans le Mappeur BizTalk hello. Même si le Mappeur hello ressemble principalement hello identiques, format de mappage hello sous-jacent est différent. Hello fonctoids (appelé **opérations de mappage** dans les Services BizTalk) disponible toohello utilisateurs sont également différents.  En effet, vous ne pouvez pas utiliser directement un mappage BizTalk dans BizTalk Services. En outre, pas tous les fonctoids hello disponibles dans BizTalk Server sont disponibles sous la forme d’opérations de mappage dans BizTalk Services.

### <a name="new-transform-operations"></a>Nouvelles opérations de transformation
Lors de la liste de hello des opérations de mappage transformation peut paraître très différente de hello Mappeur BizTalk Server, BizTalk Services transforme ont nouvelles façons d’accomplir hello des mêmes tâches. Par exemple, les transformations BizTalk Services ont des **opérations de liste** . Cela n’était pas disponible dans le Mappeur BizTalk hello.  Hello **opérations de liste** vous toocreate et opérer sur une « liste », où une liste est un ensemble d’éléments (également appelée « ligne ») et chaque élément peut avoir plusieurs membres (également appelé « colonnes »).  Vous pouvez trier la liste hello, sélectionnez les éléments selon une condition, etc..

Un autre exemple de nouvelles fonctionnalités dans BizTalk Services transforme sont hello **opérations de boucle**.  Il est difficile toocreate imbriqué des boucles Bonjour Mappeur BizTalk Server.  Par conséquent, les opérations de mappage de boucle hello sont ajoutées pour hello transforme des Services BizTalk.

Un autre exemple est hello **If-Then-Else** opération de mappage d’Expression.  Effectuez une opération if-then-else était possible dans le Mappeur BizTalk hello, mais il obligatoire plusieurs fonctoids tooaccomplish une tâche apparemment simple.

### <a name="migrating-biztalk-server-maps"></a>Migration des mappages BizTalk Server
Microsoft Azure BizTalk Services fournit qu'un toomigrate outil BizTalk Server mappe les transformations de Services tooBizTalk. Hello **BTMMigrationTool** est disponible dans le cadre de hello **outils** package fourni avec hello [téléchargement du SDK des Services BizTalk](http://go.microsoft.com/fwlink/p/?LinkId=235057). Pour plus d’informations sur l’outil de hello, consultez [convertir un tooa de mappage BizTalk transformation BizTalk Services](https://msdn.microsoft.com/library/windowsazure/hh949812.aspx).

Vous pouvez également consulter un exemple de Sandro Pereira, MVP BizTalk sur comment trop[migrer les transformations de Services BizTalk Server maps tooBizTalk](http://social.technet.microsoft.com/wiki/contents/articles/23220.migrating-biztalk-server-maps-to-windows-azure-biztalk-services-wabs-maps.aspx).

## <a name="orchestrations"></a>Orchestrations
Si vous avez besoin de toomigrate tooMicrosoft de traitement de l’orchestration BizTalk Server Azure, les orchestrations hello doivent toobe réécrite car Microsoft Azure ne prend pas en charge les orchestrations BizTalk Server en cours d’exécution.  Vous pouvez réécrire la fonctionnalité d’orchestration hello dans un service Windows Workflow Foundation 4.0 (WF4).  Ce serait une réécriture complète, car il n’existe actuellement aucune migration des tooWF4 des orchestrations BizTalk Server. Voici quelques ressources pour Windows Workflow :

* [*Comment toointegrate un flux de travail WCF Service avec des files d’attente du Bus de Service et des rubriques* ](https://msdn.microsoft.com/library/azure/hh709041.aspx) par Paolo Salvatori. 
* [*Création d’applications avec Windows Workflow Foundation et Azure* session](http://go.microsoft.com/fwlink/p/?LinkId=237314) conférence Build 2011 de hello.
* [*Centre de développement Windows Workflow Foundation*](http://go.microsoft.com/fwlink/p/?LinkId=237315) sur MSDN.
* [*Documentation de Windows Workflow Foundation 4 (WF4)*](https://msdn.microsoft.com/library/dd489441.aspx) sur MSDN.

## <a name="other-considerations"></a>Autres considérations
Voici quelques éléments à prendre en compte lors de l'utilisation de BizTalk Services.

### <a name="fallback-agreements"></a>Accords de secours
Traitement EDI de BizTalk Server a un concept hello de « Accord de secours ».  BizTalk Services ne dispose **pas** d’accord de secours pour l’instant.  Consultez les rubriques de la documentation BizTalk [hello rôle des accords dans le traitement EDI](http://go.microsoft.com/fwlink/p/?LinkId=237317) et [configuration globale ou propriétés de l’accord de secours](https://msdn.microsoft.com/library/bb245981.aspx) pour plus d’informations sur l’utilisation des accords de secours dans BizTalk Server Serveur.

### <a name="routing-toomultiple-destinations"></a>Destinations de routage toomultiple
Les ponts BizTalk Services, dans son état actuel ne prend pas en charge destinations toomultiple routage des messages à l’aide d’une publication-abonnement modèle. Au lieu de cela vous pourriez router des messages à partir d’une rubrique de Service Bus tooa BizTalk Services bridge, qui peut ensuite avoir plusieurs abonnements tooreceive hello de message à plus d’un point de terminaison.

## <a name="conclusion"></a>Conclusion
Microsoft Azure BizTalk Services est mise à jour au niveau des étapes majeures régulière tooadd nouvelles fonctionnalités et possibilités. Avec chaque mise à jour, nous comptons toosupporting augmenté toofacilitate de la fonctionnalité Création de solutions de bout en bout à l’aide des Services BizTalk et autres technologies Azure.

## <a name="see-also"></a>Voir aussi
[Développement d'applications d'entreprise avec Azure](https://msdn.microsoft.com/library/azure/hh674490.aspx)

[EDImessageflow]: ./media/biztalk-migrating-to-edi-guide/IC719455.png
