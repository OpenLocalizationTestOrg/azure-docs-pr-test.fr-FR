les files d’attente de toobegin à l’aide du Service Bus dans Azure, vous devez d’abord créer un espace de noms avec un nom qui est unique dans Azure. Ce dernier fournit un conteneur d'étendue pour l'adressage des ressources Service Bus au sein de votre application.

toocreate un espace de noms :

1. Ouvrez une session sur toohello [portail Azure][Azure portal].
2. Dans le volet de navigation gauche hello du portail de hello, cliquez sur **nouveau**, puis cliquez sur **intégration**, puis cliquez sur **Service Bus**.
3. Bonjour **créer l’espace de noms** boîte de dialogue, entrez un nom d’espace de noms. système de Hello vérifie immédiatement toosee si le nom hello est disponible.
4. Une fois que nom d’espace de noms hello de fabrication est disponible, choisissez hello tarification (Basic, Standard ou Premium).
5. Bonjour **abonnement** champ, choisissez un abonnement Azure dans l’espace de noms toocreate hello.
6. Bonjour **groupe de ressources** champ, choisissez un groupe de ressources existant dans le hello espace de noms dynamique, ou créer un nouveau.      
7. Dans **emplacement**, choisissez hello pays ou une région dans laquelle votre espace de noms doit être hébergé.
   
    ![Créer un espace de noms][create-namespace]
8. Cliquez sur **Créer**. système de Hello maintenant crée votre espace de noms et active. Vous pouvez avoir toowait plusieurs minutes en tant que hello système configure des ressources pour votre compte.

### <a name="obtain-hello-management-credentials"></a>Obtenir des informations d’identification de gestion hello

1. Dans hello d’espaces de noms, cliquez sur hello nouvellement créée le nom de l’espace de noms.
2. Dans le panneau espace de noms de hello, cliquez sur **les stratégies d’accès partagé**.
3. Bonjour **les stratégies d’accès partagé** panneau, cliquez sur **RootManageSharedAccessKey**.
   
    ![informations de connexion][connection-info]
4. Bonjour **stratégie : RootManageSharedAccessKey** panneau, cliquez sur bouton hello suivant trop**la clé de chaîne – primary connexion**, toocopy hello connexion chaîne tooyour le Presse-papiers pour une utilisation ultérieure. Copiez cette valeur dans le Bloc-notes ou un autre emplacement temporaire.
   
    ![connection-string][connection-string]

5. Étape précédente hello répétition, copier et coller la valeur hello **clé primaire** tooa les emplacement temporaire pour une utilisation ultérieure.

<!--Image references-->

[create-namespace]: ./media/service-bus-create-namespace-portal/create-namespace.png
[connection-info]: ./media/service-bus-create-namespace-portal/connection-info.png
[connection-string]: ./media/service-bus-create-namespace-portal/connection-string.png
[Azure portal]: https://portal.azure.com
