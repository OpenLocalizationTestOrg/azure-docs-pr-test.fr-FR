---
title: "aaaDesigning les Applications hautement disponibles à l’aide du stockage de géo-redondant Azure avec accès en lecture (RA-GRS) | Documents Microsoft"
description: Comment tooarchitect de stockage Azure RA-GRS toouse une application hautement disponible flexible suffisamment pannes toohandle.
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: robinsh
ms.openlocfilehash: e4a9fe7ef33eecd894408b3c1ef59920a248d1bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="designing-highly-available-applications-using-ra-grs"></a>Conception d’applications hautement disponibles à l’aide du stockage RA-GRS

La fourniture d’une plateforme hautement disponible pour l’hébergement des applications est une caractéristique courante des infrastructures basées sur le cloud. Les développeurs d’applications basées sur le cloud doivent prendre en compte avec soin la façon dont tooleverage cette utilisateurs tootheir de plateforme toodeliver applications hautement disponibles. Cet article concentre spécifiquement sur la façon dont les développeurs peuvent utiliser hello Azure stockage Read Access Geo Redundant Storage (RA-GRS) toomake leurs applications plus disponibles.

Quatre options de redondance sont disponibles : le stockage localement redondant (LRS), le stockage redondant dans une zone (ZRS), le stockage géoredondant (GRS) et le stockage géoredondant avec accès en lecture (RA-GRS). Nous allons toodiscuss GRS et RA-GRS dans cet article. Avec GRS, trois copies de vos données sont conservées dans la région principale de hello que vous avez sélectionné lorsque vous configurez le compte de stockage hello. Trois copies supplémentaires sont conservées de façon asynchrone dans une région secondaire spécifiée par Azure. Est de RA-GRS hello même chose que GRS, sauf que vous avez copie secondaire de toohello accès en lecture. Pour plus d’informations sur les différentes options de redondance de stockage Azure hello, consultez [réplication de stockage Azure](https://docs.microsoft.com/en-us/azure/storage/storage-redundancy). article de réplication Hello montre également les couplages hello de régions principales et secondaires de hello.

Il existe des extraits de code inclus dans cet article et un exemple complet en lien tooa à fin hello que vous pouvez télécharger et exécuter.

## <a name="key-features-of-ra-grs"></a>Fonctionnalités clés du stockage RA-GRS

Avant d’aborder la façon de toouse stockage de RA-GRS, nous allons parler de ses propriétés et le comportement.

* Le stockage Azure conserve une copie en lecture seule des données de hello que vous stockez dans votre région primaire dans une région secondaire ; comme indiqué ci-dessus, le service de stockage hello détermine emplacement hello de région secondaire de hello.

* copie en lecture seule de Hello est [cohérente](https://en.wikipedia.org/wiki/Eventual_consistency) avec des données dans la région principale de hello hello.

* Pour les objets BLOB, tables et files d’attente, vous pouvez interroger la région secondaire hello pour un *dernière heure de synchronisation* valeur qui vous indique lorsque la réplication dernière hello à partir de la région de hello toohello principal secondaire s’est produite. (Cette fonctionnalité n’est pas prise en charge pour le stockage de fichiers Azure, qui n’a pas la redondance RA-GRS pour l’instant.)

* Vous pouvez utiliser hello bibliothèque cliente de stockage toointeract avec les données de salutation dans une région de hello principal ou secondaire. Vous pouvez également rediriger les demandes de lecture automatiquement toohello la région secondaire si l’expiration d’une région primaire toohello de demande de lecture.

* S’il existe un problème majeur affectant l’accessibilité hello de données hello dans la région principale de hello, hello équipe Azure peut déclencher un basculement géographique, à quel point les entrées DNS hello pointant vers la région principale de toohello sera toohello toopoint modifié la région secondaire.

* En cas d’un basculement géographique, Azure sera sélectionner un nouvel emplacement secondaire répliquer emplacement toothat des données hello, puis pointez hello tooit du entrées DNS secondaire. point de terminaison secondaire Hello n’est pas disponible tant que compte de stockage hello a terminé la réplication. Pour plus d’informations, consultez [le toodo en cas de panne de stockage Azure](https://docs.microsoft.com/en-us/azure/storage/storage-disaster-recovery-guidance).

## <a name="application-design-considerations-when-using-ra-grs"></a>Considérations relatives à la conception d’applications avec le stockage RA-GRS

Hello principal de cet article vise tooshow vous comment toodesign une application qui continuera toofunction (bien que dans une capacité limitée) même en cas de hello de sinistre majeur sur les données principales hello center. Pour cela, en ayant votre temporaire de toohandle d’application ou les problèmes d’exécution longue en basculant tooread à partir de la région secondaire hello tant qu’il reste un problème et que cette approche lors de la région principale de hello est à nouveau disponible.

### <a name="using-eventually-consistent-data"></a>Utilisation de données cohérentes

Cette solution suppose qu’il tooreturn OK ce qui peut être application appelante toohello de données périmées. Étant donné que les données secondaires hello soient cohérentes, il est possible que les données de salutation a été écrite toohello principal mais hello toohello de mise à jour secondaire n'avait pas terminé la réplication lors de la région principale de hello est devenu inaccessible.

Par exemple, votre client peut envoyer une mise à jour a réussi, et puis hello principal pourrait tomber en panne avant la mise à jour hello est propagé toohello secondaire. Dans ce cas, si hello client puis données hello tooread, il reçoit des données obsolètes hello au lieu des données de hello mis à jour. Vous devez décider si ce n’est acceptable et dans ce cas, comment vous serez un message client de hello. Vous verrez comment toocheck hello dernière heure de synchronisation des données secondaires de hello plus loin dans cet article de toosee si hello secondaire est à jour.

### <a name="handling-services-separately-or-all-together"></a>Gestion des services ensemble ou séparément

Lorsqu’il y a probablement pas, il est possible toobecome un service non disponible pendant hello d’autres services sont toujours entièrement fonctionnelles. Vous pouvant handle hello tentatives et le mode lecture seule pour chaque service séparément (objets BLOB, files d’attente, les tables), ou vous pouvez gérer les nouvelles tentatives de façon générique pour tous les services de stockage hello ensemble.

Par exemple, si vous utilisez des files d’attente et les objets BLOB dans votre application, vous pouvez décider tooput des erreurs de code séparé toohandle renouvelable pour chacun d’eux. Puis si vous obtenez une nouvelle tentative à partir du service d’objets blob hello, mais le service de file d’attente hello fonctionne toujours, qu’une partie de votre application qui gère les objets BLOB hello sera affectée. Si vous décidez de toohandle tous les services de stockage retente de façon générique et un service d’objets blob toohello appel renvoie une erreur renouvelable, puis les demandes tooboth hello blob service et le service de file d’attente hello seront affectées.

Au final, cela dépend de la complexité de hello de votre application. Vous pouvez décider pas les échecs de hello toohandle par service, mais au lieu de cela tooredirect lire les demandes de tous les services toohello secondaire région de stockage et exécuter l’application hello en mode lecture seule lorsque vous détectez un problème avec n’importe quel service de stockage dans la région principale de hello.

### <a name="other-considerations"></a>Autres points à considérer

Ceux-ci sont hello autres considérations, nous allons décrire dans reste hello de cet article.

*   La gestion des nouvelles tentatives de demandes de lecture à l’aide du modèle de disjoncteur hello

*   Données finalement cohérentes et hello dernière heure de synchronisation

*   Test

## <a name="running-your-application-in-read-only-mode"></a>Exécution de votre application en mode lecture seule

toouse stockage de RA-GRS, doit être en mesure de toohandle les deux échoué de demandes de lecture et mise à jour de demandes ayant échoué (avec mise à jour dans ce cas ce qui signifie que les insertions, mises à jour et suppressions). Si hello centre de données principal tombe en panne, de lecture les demandes peuvent être le centre de données secondaire toohello redirigé, mais les demandes de mise à jour ne peut pas car hello secondaire est en lecture seule. Pour cette raison, vous devez certaines toorun de façon à votre application en mode lecture seule.

Par exemple, vous pouvez définir un indicateur qui sera vérifié avant l’envoi de n’importe quel service de stockage toohello demandes mise à jour. Lorsqu’une des demandes de mise à jour hello est fourni par le biais, vous pouvez ignorer et retourner un client toohello de réponse appropriée. Vous pouvez même souhaitez toodisable totalement de certaines fonctionnalités jusqu'à ce que hello problème est résolu et informer les utilisateurs que ces fonctionnalités sont temporairement indisponibles.

Si vous décidez de toohandle des erreurs pour chaque service séparément, vous devez également toohandle hello capacité toorun votre application en mode lecture seule par service. Vous pouvez avoir des indicateurs en lecture seule pour chaque service qui peut être activée et désactivée et handle hello indicateur approprié dans hello aux emplacements appropriés dans votre code.

En cours toorun en mesure de votre application en mode lecture seule a un autre avantage de côté : elle vous donne hello capacité tooensure des fonctionnalités limitées au cours d’une mise à niveau de l’application principale. Vous pouvez déclencher toorun de votre application dans en lecture seule en mode et toohello de point de centre de données secondaire, vous être assuré de la que personne n’accède aux données hello dans la région principale de hello lorsque vous effectuez des mises à niveau.

## <a name="handling-updates-when-running-in-read-only-mode"></a>Gestion des mises à jour lors d’une exécution en mode lecture seule

Il existe de nombreuses façons les demandes de mise à jour toohandle lors de l’exécution en mode lecture seule. Nous n’abordons pas ce point de façon complète, mais vous pouvez généralement prendre quelques modèles en considération.

1.  Vous pouvez répondre tooyour utilisateur et en leur indiquant que les mises à jour ne sont pas actuellement autorisés. Par exemple, un système de gestion des contacts peut activer les informations de contact clients tooaccess mais pas mettre à jour.

2.  Vous pouvez empiler vos mises à jour dans une autre région. Dans ce cas, vous serez votre file d’attente tooa de mise à jour en attente les demandes d’écriture dans une autre région et puis ont un tooprocess de la façon dont ces demandes une fois le centre de données principal hello est à nouveau en ligne. Dans ce scénario, vous devez informer les clients hello cette mise à jour hello demandée est en attente pour un traitement ultérieur.

3.  Vous pouvez écrire vos mises à jour du compte de stockage tooa dans une autre région. Lorsque le centre de données principal hello revient en ligne, vous pouvez demander un toomerge de façon ces mises à jour des données de hello principal, en fonction de la structure de hello de données de hello dans. Par exemple, si vous créez des fichiers distincts avec un cachet de date/heure dans le nom de hello, vous pouvez copier ces fichiers toohello arrière principal la région. Cela fonctionne pour certaines charges de travail, notamment la journalisation et les données IoT.

## <a name="handling-retries"></a>Gestion des nouvelles tentatives

Comment savoir quelles sont les erreurs renouvelables ? Cela est déterminé par la bibliothèque cliente de stockage hello. Par exemple, une erreur 404 (ressource introuvable) n’est pas renouvelable, car une nouvelle tentative il n’est pas probable tooresult en cas de réussite. Sur hello autre part, une erreur 500 est renouvelable, car il s’agit d’une erreur de serveur, et il peut être simplement un problème temporaire. Pour plus d’informations, consultez hello [ouvrez source code hello ExponentialRetry classe](https://github.com/Azure/azure-storage-net/blob/87b84b3d5ee884c7adc10e494e2c7060956515d0/Lib/Common/RetryPolicies/ExponentialRetry.cs) dans la bibliothèque cliente de stockage de .NET hello. (Recherchez hello ShouldRetry méthode.)

### <a name="read-requests"></a>Demandes de lecture

Demandes de lecture peuvent être redirigé toosecondary stockage s’il existe un problème avec le stockage principal. Comme indiqué ci-dessus dans [à l’aide des données finalement cohérentes](#using-eventually-consistent-data), il doit être acceptable pour votre application toopotentially lire les données obsolètes. Si vous utilisez hello storage client library tooaccess les données de RA-GRS, vous pouvez spécifier le comportement des nouvelles tentatives hello d’une requête de lecture en définissant une valeur pour hello **LocationMode** tooone de propriété suivantes de hello :

*   **PrimaryOnly** (hello par défaut)

*   **PrimaryThenSecondary**

*   **SecondaryOnly**

*   **SecondaryThenPrimary**

Lorsque vous définissez hello **LocationMode** trop**PrimaryThenSecondary**, si hello initial de point de terminaison principal demande toohello échoue avec une erreur renouvelable, le client de hello effectue automatiquement une nouvelle lecture lecture point de terminaison secondaire toohello la demande. Si l’erreur de hello est un délai d’attente du serveur, puis hello disposera client toowait pour tooexpire de délai d’attente hello avant de recevoir une erreur renouvelable à partir du service de hello.

Il existe deux scénarios tooconsider lorsque vous décidez de la façon dont une erreur renouvelable toorespond tooa :

*   Il s’agit d’un problème isolé et le point de terminaison primaire les demandes suivantes toohello ne retourne pas une erreur renouvelable. Ceci peut se produire, par exemple, en cas d’erreur réseau temporaire.

    Dans ce scénario, il n’existe aucune baisse significative des performances dans ayant **LocationMode** défini trop**PrimaryThenSecondary** que cela ne se produit rarement.

*   Il s’agit d’un problème avec au moins un des services de stockage hello dans la région principale de hello et service de toothat toutes les demandes suivantes dans la région principale de hello sont tooreturn probablement des erreurs renouvelable pour une période donnée. Un exemple est si la région principale de hello est totalement inaccessible.

    Dans ce scénario, il est une baisse des performances, car toutes vos demandes de lecture seront essayer en premier point de terminaison principal hello, attendez hello du délai d’attente tooexpire, puis basculer le point de terminaison secondaire toohello.

Pour ces scénarios, vous devez identifier un problème en cours avec le point de terminaison principal hello et envoyer toutes les demandes de lecture directement hello du point de terminaison secondaire toohello en définissant **LocationMode** propriété trop **SecondaryOnly**. À ce stade, vous devez également modifier toorun d’application hello en mode lecture seule. Cette approche est appelée hello [modèle de disjoncteur](https://msdn.microsoft.com/library/dn589784.aspx).

### <a name="update-requests"></a>Demandes de mise à jour

modèle de disjoncteur Hello peut également être appliqué tooupdate demandes. Toutefois, les demandes de mise à jour ne peut pas être redirigé toosecondary stockage, qui est en lecture seule. Pour ces requêtes, vous devez laisser hello **LocationMode** propriété trop**PrimaryOnly** (hello par défaut). toohandle ces erreurs, vous pouvez appliquer un demandes toothese métrique – telles que des 10 défaillances dans une ligne et lorsque le seuil est atteint, basculer vers l’application hello en mode lecture seule. Vous pouvez utiliser hello les mêmes méthodes pour retourner le mode tooupdate que celles décrites ci-dessous dans la section suivante de hello sur le modèle de disjoncteur hello.

## <a name="circuit-breaker-pattern"></a>Modèle Disjoncteur

À l’aide du modèle de disjoncteur hello dans votre application peut l’empêcher d’une nouvelle tentative d’une opération qui est probablement toofail à plusieurs reprises. Il permet de hello application toocontinue toorun plutôt que de prendre le temps pendant l’opération de hello est retentée de manière exponentielle. Il détecte également lors de la défaillance de hello a été résolu, à laquelle application hello de temps peut réessayez hello.

### <a name="how-tooimplement-hello-circuit-breaker-pattern"></a>Comment tooimplement hello modèle de disjoncteur

tooidentify qu’il existe un problème en cours avec un point de terminaison principal, vous pouvez surveiller la fréquence à laquelle le client de hello rencontre une erreur renouvelable. Chaque cas sont différent, vous devez toodecide sur le seuil de hello souhaité de toouse pour hello décision tooswitch toohello point de terminaison secondaire et exécuter l’application hello en mode lecture seule. Par exemple, vous pouvez décider de commutateur de hello tooperform s’il existe des échecs de 10 dans une ligne sans succès. Un autre exemple est tooswitch cas d’échec de 90 % des demandes de hello dans une période de 2 minutes.

Pour le premier scénario de hello, vous pouvez conserver simplement un nombre d’échecs de hello et s’il existe un succès avant d’atteindre hello toozero arrière de nombre maximal, affectez la valeur hello. Pour le second scénario de hello, tooimplement monodirectionnelle, il est toouse hello objet MemoryCache (dans .NET). Pour chaque demande, ajouter un cache de toohello CacheItem, définir la valeur de hello toosuccess (1) ou échouer (0) et définir des minutes de too2 hello d’expiration du temps à partir de maintenant (ou tout ce qui est votre contrainte de temps). Lors de l’heure d’expiration d’une entrée est atteinte, hello entrée est automatiquement supprimée. Cela vous donne une fenêtre cumulative de 2 minutes. Chaque fois que vous apportez à un service de stockage toohello de demande, vous tout d’abord utiliser une requête Linq sur hello MemoryCache objet toocalculate hello pourcentage de réussite en additionnant les valeurs hello et en divisant par le nombre de hello. Lorsque le pourcentage de réussite hello est inférieur à un seuil (par exemple, 10 %), définissez hello **LocationMode** propriété pour des demandes de lecture trop**SecondaryOnly** et basculer vers l’application hello en mode lecture seule avant continuer.

seuil d’erreurs de Hello utilisé toodetermine lorsque le commutateur de hello toomake peut-être varier par tooservice de service dans votre application, vous devez donc considérer ce qui les rend paramètres configurables. C’est également lorsque vous décidez de toohandle des erreurs récupérables à partir de chaque service séparément ou comme un seul, comme indiqué précédemment.

Une autre considération est comment toohandle plusieurs instances d’une application et quelles toodo lorsque vous détectez une erreur renouvelable dans chaque instance. Par exemple, peut avoir 20 ordinateurs virtuels en cours d’exécution avec hello chargée de la même application. Gérez-vous chaque instance séparément ? Si une seule instance démarre rencontre des problèmes, voulez-vous toolimit hello réponse toojust qu’une seule instance, ou souhaitez-vous tootry toohave toutes les instances répondent Bonjour même quand une seule instance a un problème ? Gestion des instances de hello séparément sont beaucoup plus simple que la tentative de réponse de hello toocoordinate entre eux, mais comment cela dépend d’une architecture de votre application.

### <a name="options-for-monitoring-hello-error-frequency"></a>Options pour l’analyse de fréquence d’erreur hello

Vous avez trois options principales pour l’analyse de fréquence hello de nouvelles tentatives dans la région principale de hello dans l’ordre toodetermine lorsque tooswitch sur la région secondaire toohello et modification hello toorun d’application en mode lecture seule.

*   Ajoutez un gestionnaire pour hello [ **nouvelle tentative** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.operationcontext.retrying.aspx) événement sur hello [ **OperationContext** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.operationcontext.aspx) objet passer de demandes de stockage tooyour – il s’agit de hello méthode affiché dans cet article et utilisée dans hello accompagnant l’exemple. Ces événements se déclenchent à chaque fois qu’une demande de hello tentatives, activation tootrack la fréquence à laquelle le client de hello rencontre des erreurs récupérables sur un point de terminaison principal.

    ```csharp 
    operationContext.Retrying += (sender, arguments) =>
    {
        // Retrying in hello primary region
        if (arguments.Request.Host == primaryhostname)
            ...
    };
    ```

*   Bonjour [ **évaluer** ](http://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.retrypolicies.iextendedretrypolicy.evaluate.aspx) méthode dans une stratégie de nouvelle tentative personnalisée, vous pouvez exécuter du code personnalisé chaque fois qu’une nouvelle tentative a lieu. Dans Ajout toorecording lorsque se produit une nouvelle tentative, permet aussi de vous hello opportunité toomodify votre comportement des nouvelles tentatives.

    ```csharp 
    public RetryInfo Evaluate(RetryContext retryContext,
    OperationContext operationContext)
    {
        var statusCode = retryContext.LastRequestResult.HttpStatusCode;
        if (retryContext.CurrentRetryCount >= this.maximumAttempts
        || ((statusCode &gt;= 300 && statusCode &lt; 500 && statusCode != 408)
        || statusCode == 501 // Not Implemented
        || statusCode == 505 // Version Not Supported
            ))
        {
        // Do not retry
            return null;
        }

        // Monitor retries in hello primary location
        ...

        // Determine RetryInterval and TargetLocation
        RetryInfo info =
            CreateRetryInfo(retryContext.CurrentRetryCount);

        return info;
    }
    ```

*   troisième méthode Hello est tooimplement un composant de contrôle personnalisé dans votre application qui interroge en permanence de votre point de terminaison de stockage principal avec factice lire les demandes (par exemple, la lecture d’un objet blob de petits) toodetermine son intégrité. Dans ce cas, la quantité de ressources sollicitées est raisonnable. Lorsqu’un problème est détecté qui atteint le seuil, vous pouvez ensuite effectuer commutateur de hello trop**SecondaryOnly** et en lecture seule.

Dans certains cas, vous pouvez tooswitch toousing arrière hello point de terminaison principal et autoriser les mises à jour. Si vous utilisez une des hello deux premières méthodes répertoriées ci-dessus, vous pourriez simplement basculer le point de terminaison principal toohello précédent et activer le mode de mise à jour après qu’une durée arbitrairement sélectionnée ou le nombre d’opérations a été effectuée. Vous pourrez ensuite laisser parcourez logique de nouvelle tentative hello à nouveau. Si hello a été résolu, il continue de point de terminaison principal toouse hello et autoriser les mises à jour. S’il reste un problème, il bascule une fois de plus toohello précédent point de terminaison secondaire et le mode lecture seule après l’échec de que vous avez défini des critères de hello.

Pour le troisième scénario de hello, lorsque le point de terminaison de stockage principal ping hello redevient réussi, vous pouvez déclencher revenir à l’ancienne hello trop**PrimaryOnly** et continuer à autoriser les mises à jour.

## <a name="handling-eventually-consistent-data"></a>Gestion des données cohérentes

RA-GRS fonctionne par la réplication des transactions à partir de la région de hello toohello principal secondaire. Ce processus de réplication qui garantit que les données de salutation dans la région secondaire hello sont *cohérente*. Cela signifie que toutes les transactions hello dans la région principale de hello finalement apparaîtra dans la région secondaire hello, mais qu’il existe peut-être un retard avant qu’ils s’affichent, et qu’il n’existe aucune garantie des transactions hello arrivent dans la région secondaire hello Bonjour même ordre que qui dans lequel ils ont été appliquées à l’origine dans la région principale de hello. Si vos transactions arrivent dans la région secondaire hello dans le désordre, vous *peut* prendre en compte vos données dans toobe de région secondaire hello dans un état incohérent jusqu'à ce que le service de hello rattrape.

Hello tableau suivant montre un exemple de ce qui peut se produire lorsque vous mettez à jour Détails hello d’un employé de toomake son membre hello *administrateurs* rôle. Par souci de hello de cet exemple, cela nécessite la mise à jour hello **employé** entité et mise à jour un **rôle administrateur** entité avec le nombre total de hello du groupe Administrateurs. Notez comment les mises à jour de hello sont appliquées en désordre dans la région secondaire hello.

| **Time** | **Transaction**                                            | **Réplication**                       | **Dernière heure de synchronisation** | **Résultat** |
|----------|------------------------------------------------------------|---------------------------------------|--------------------|------------| 
| T0       | Transaction A : <br> Insérer l’entité d’employé <br> dans la région primaire |                                   |                    | La transaction A inséré tooprimary,<br> pas encore répliquée. |
| T1       |                                                            | Transaction A <br> répliquée sur<br> la région secondaire | T1 | La transaction A répliquées toosecondary. <br>Dernière heure de synchronisation mise à jour.    |
| T2       | Transaction B :<br>Mettre à jour<br> l’entité d’employé<br> dans la région primaire  |                                | T1                 | Transaction B écrite tooprimary,<br> pas encore répliquée.  |
| T3       | Transaction C :<br> Mettre à jour <br>administrator<br>entité de rôle dans<br>primary |                    | T1                 | Transaction C écrit tooprimary,<br> pas encore répliquée.  |
| *T4*     |                                                       | Transaction C <br>répliquée sur<br> la région secondaire | T1         | Transaction C répliquée toosecondary.<br>LastSyncTime pas encore mis à jour car <br>la transaction B n’a pas encore été répliquée.|
| *T5*     | Lire les entités <br>de la région secondaire                           |                                  | T1                 | Vous obtenez la valeur périmée de hello pour employé <br> car la transaction B n’a <br> pas encore été répliquée. Vous obtenez la nouvelle valeur de hello pour<br> l’entité de rôle d’administrateur car C a<br> été répliquée. La dernière heure de synchronisation n’a pas encore<br> été mise à jour car la transaction B<br> n’a pas été répliquée. Vous savez que<br>l’entité de rôle d’administrateur est cohérente <br>Étant donné que hello entité date/heure est après <br>Hello dernière heure de synchronisation. |
| *T6*     |                                                      | Transaction B<br> répliquée sur<br> la région secondaire | T6                 | *T6* – Toutes les transactions jusqu’à C ont <br>été répliquées. La dernière heure de synchronisation<br> est mise à jour. |

Dans cet exemple, supposons que tooreading de commutateurs hello client à partir de la région secondaire de hello à T5. Il peut lire correctement hello **rôle administrateur** entité à ce stade, mais les entités hello contient une valeur pour le nombre de hello des administrateurs qui n’est pas cohérent avec le nombre de hello de **employé** entités qui sont marquées en tant qu’administrateurs dans la région secondaire hello pour l’instant. Votre client peut afficher simplement cette valeur, avec des risques hello qu’il s’agit des informations incohérentes. Vous pouvez également hello client peut essayer toodetermine que hello **rôle administrateur** est dans un état potentiellement incohérent, car les mises à jour hello se sont produites dans le désordre et ensuite aux utilisateur hello de ce fait.

toorecognize qu’il possède des données potentiellement incohérentes, les clients hello peuvent utiliser la valeur hello hello *dernière heure de synchronisation* que vous pouvez obtenir à tout moment en interrogeant un service de stockage. Vous pouvez en déduire hello heure données hello dans la région secondaire hello dernière cohérent et lorsque le service de hello avait appliqué tous les hello transactions antérieures toothat point dans le temps. Dans l’exemple hello illustrée ci-dessus, une fois que le service de hello insère hello **employé** entité dans la région secondaire hello, hello dernière heure de synchronisation est défini trop*T1*. Il reste à *T1* jusqu'à ce que les mises à jour de service de hello hello **employé** entité dans la région de hello secondaire lorsqu’il est défini trop*T6*. Si le client de hello récupère hello dernière heure de synchronisation lorsqu’il lit entité hello à *T5*, elle peut le comparer avec l’horodateur hello sur l’entité de hello. Si timestamp hello sur l’entité de hello est ultérieure à hello heure, de la dernière synchronisation hello entité est dans un état potentiellement incohérent puis vous pouvez effectuer tout ce qui est la conséquence de hello pour votre application. À l’aide de ce champ, vous devez savoir quand toohello mise à jour hello dernière principal a été terminé.

## <a name="testing"></a>Test

Il est important tootest que votre application se comporte comme prévu quand il rencontre une erreur renouvelable. Par exemple, vous devez tootest qui hello toohello de commutateurs application secondaire et en mode lecture seule lorsqu’il détecte un problème et bascule lorsque la région primaire hello est à nouveau disponible. toodo, vous avez besoin d’une erreur renouvelable toosimulate de façon et contrôler la fréquence à laquelle ils se produisent.

Vous pouvez utiliser [Fiddler](http://www.telerik.com/fiddler) toointercept et modifier des réponses HTTP dans un script. Ce script peut identifier des réponses provenant de votre point de terminaison primaire et modifier hello HTTP état code tooone que hello que bibliothèque cliente de stockage reconnaît comme une erreur renouvelable. Cet extrait de code montre un exemple simple d’un script de Fiddler qui intercepte les demandes de tooread de réponses sur hello **employeedata** table tooreturn état 502 :

```java
static function OnBeforeResponse(oSession: Session) {
    ...
    if ((oSession.hostname == "\[yourstorageaccount\].table.core.windows.net")
      && (oSession.PathAndQuery.StartsWith("/employeedata?$filter"))) {
        oSession.responseCode = 502;
    }
}
```

Vous pouvez étendre cet exemple toointercept un éventail plus large de demandes et modifier uniquement hello **responseCode** sur certains d'entre eux toobetter simuler un scénario réel. Pour plus d’informations sur la personnalisation des scripts de Fiddler, consultez [modification d’une demande ou réponse](http://docs.telerik.com/fiddler/KnowledgeBase/FiddlerScript/ModifyRequestOrResponse) Bonjour documentation de Fiddler.

Si vous avez apporté des seuils hello pour le basculement de votre application tooread seule configurable, il sera comportement de hello tootest plus facile avec des volumes de production non transaction.

## <a name="next-steps"></a>Étapes suivantes

* Pour plus d’informations sur l’accès en lecture géo-redondance, y compris un autre exemple de comment hello LastSyncTime est définie, consultez [Options de redondance du stockage Windows Azure et Read Access Geo Redundant Storage](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

* Pour obtenir un exemple complet montrant comment toomake hello commutateur dans les deux sens entre les points de terminaison hello principaux et secondaires, consultez [exemples Azure – à l’aide de hello modèle de disjoncteur avec stockage de RA-GRS](https://github.com/Azure-Samples/storage-dotnet-circuit-breaker-pattern-ha-apps-using-ra-grs).
