Créer des informations d’identification de déploiement par hello [az webapp utilisateur de déploiement défini](/cli/azure/webapp/deployment/user#set) commande.

Un utilisateur du déploiement est requis pour FTP et Git déploiement tooa l’application web locale. mot de passe et le nom d’utilisateur hello sont au niveau du compte. _Ils sont différents des informations d’identification de votre abonnement Azure._

Bonjour suivant de commande, remplacez  *\<nom d’utilisateur >* et  *\<mot de passe >* avec un nouveau nom d’utilisateur et un mot de passe. nom d’utilisateur Hello doit être unique. Hello mot de passe doit comporter au moins huit caractères, avec deux hello suivant trois éléments : des lettres, des chiffres, des symboles. 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

Si vous obtenez un ` 'Conflict'. Details: 409` erreur, le nom d’utilisateur de modification hello. Si vous obtenez une erreur ` 'Bad Request'. Details: 400`, utilisez un mot de passe plus fort.

Vous ne devez créer cet utilisateur de déploiement qu’une fois. Vous pouvez l’utiliser pour tous vos déploiements Azure.

> [!NOTE]
> Nom de l’enregistrement hello utilisateur et mot de passe. Vous avez besoin de les toodeploy hello web application plus tard.
>
>