## <a name="what-are-service-bus-topics-and-subscriptions"></a>Présentation des rubriques et des abonnements Service Bus
Les rubriques et les abonnements Service Bus prennent en charge un modèle de communication de messagerie *de publication et d'abonnement* . Lors de l’utilisation de rubriques et d’abonnements, les composants d’une application distribuée ne communiquent pas directement entre eux ; ils échangent plutôt des messages via une rubrique, qui fait office d’intermédiaire.

![TopicConcepts](./media/howto-service-bus-topics/sb-topics-01.png)

Contrairement aux files d’attente Service Bus, où chaque message est traité par un seul consommateur, les rubriques et les abonnements fournissent une forme de communication « un-à-plusieurs », à l'aide d'un modèle de publication et d'abonnement. Il est possible d’inscrire la rubrique de tooa plusieurs abonnements. Lorsqu’un message est envoyé à tooa rubrique, il est alors effectuée indépendamment disponible tooeach toohandle/processus d’inscription.

Une rubrique de tooa abonnement ressemble à une file d’attente virtuelle qui reçoit des copies des messages de type hello qui ont été envoyés toohello rubrique. Vous pouvez éventuellement enregistrer les règles de filtre pour une rubrique à la fois par abonnement, qui vous permet de toofilter ou limiter le rubrique tooa de messages sont reçus par les abonnements de rubrique.

Les rubriques Service Bus et les abonnements vous tooscale et traitent un très grand nombre de messages entre plusieurs utilisateurs et applications.

## <a name="create-a-namespace"></a>Créer un espace de noms
toobegin à l’aide des rubriques et abonnements Service Bus dans Azure, vous devez d’abord créer un *espace de noms de service*. Ce dernier fournit un conteneur d'étendue pour l'adressage des ressources Service Bus au sein de votre application.

toocreate un espace de noms :

1. Ouvrez une session sur toohello [portail Azure][Azure portal].
2. Dans le volet de navigation gauche hello du portail de hello, cliquez sur **nouveau**, puis cliquez sur **intégration**, puis cliquez sur **Service Bus**.
3. Bonjour **créer l’espace de noms** boîte de dialogue, entrez un nom d’espace de noms. système de Hello vérifie immédiatement toosee si le nom hello est disponible.
4. Une fois que nom d’espace de noms hello de fabrication est disponible, choisissez hello tarification (Basic, Standard ou Premium).
5. Bonjour **abonnement** champ, choisissez un abonnement Azure dans l’espace de noms toocreate hello.
6. Bonjour **groupe de ressources** champ, choisissez un groupe de ressources existant dans le hello espace de noms dynamique, ou créer un nouveau.      
7. Dans **emplacement**, choisissez hello pays ou une région dans laquelle votre espace de noms doit être hébergé.
   
    ![Créer un espace de noms][create-namespace]
8. Cliquez sur hello **créer** bouton. système de Hello maintenant crée votre espace de noms et active. Vous pouvez avoir toowait plusieurs minutes en tant que hello système configure des ressources pour votre compte.

### <a name="obtain-hello-credentials"></a>Obtenir des informations d’identification hello
1. Dans hello d’espaces de noms, cliquez sur hello nouvellement créée le nom de l’espace de noms.
2. Bonjour **espace de noms Service Bus** panneau, cliquez sur **les stratégies d’accès partagé**.
3. Bonjour **les stratégies d’accès partagé** panneau, cliquez sur **RootManageSharedAccessKey**.
   
    ![informations de connexion][connection-info]
4. Bonjour **stratégie : RootManageSharedAccessKey** panneau, cliquez sur bouton hello suivant trop**la clé de chaîne – primary connexion**, toocopy hello connexion chaîne tooyour le Presse-papiers pour une utilisation ultérieure.
   
    ![connection-string][connection-string]

[Azure portal]: https://portal.azure.com
[create-namespace]: ./media/howto-service-bus-topics/create-namespace.png
[connection-info]: ./media/howto-service-bus-topics/connection-info.png
[connection-string]: ./media/howto-service-bus-topics/connection-string.png


