Dans cette étape, vous créez un port de sonde pare-feu règle tooopen hello pour hello équilibrée point de terminaison (59 999, comme indiqué précédemment) et un autre port d’écoute tooopen hello disponibilité groupe de règles. Étant donné que vous avez créé un point de terminaison avec équilibrage de charge hello sur hello machines virtuelles qui contiennent des réplicas du groupe de disponibilité, vous devez tooopen hello sonde et le port port d’écoute hello sur hello machines virtuelles respectives.

1. Sur les machines virtuelles hébergeant les réplicas, démarrez le **Pare-feu Windows avec fonctions avancées de sécurité**.

2. Cliquez avec le bouton droit sur **Règles de trafic entrant**, puis cliquez sur **Nouvelle règle**.

3. Sur hello **le Type de règle** page, sélectionnez **Port**, puis cliquez sur **suivant**.

4. Sur hello **protocole et Ports** page, sélectionnez **TCP**, type **59999** Bonjour **ports locaux spécifiques** zone, puis cliquez sur **Suivant**.

5. Sur hello **Action** page, conservez **autoriser la connexion hello** sélectionné, puis cliquez sur **suivant**.

6. Sur hello **profil** page, acceptez les paramètres par défaut de hello et puis cliquez sur **suivant**.

7. Sur hello **nom** page hello **nom** texte, spécifiez un nom de la règle, tel que **toujours de sondage de Port d’écoute**, puis cliquez sur **Terminer**.

8. Répétez hello précédant les étapes pour le port d’écoute hello disponibilité groupe (comme indiqué plus haut dans le paramètre hello $EndpointPort du script de hello), puis spécifiez un nom de règle approprié, tel que **toujours sur Port d’écoute**.

