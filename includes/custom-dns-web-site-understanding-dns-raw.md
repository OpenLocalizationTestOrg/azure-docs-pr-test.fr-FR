Hello système DNS (Domain Name) est utilisé toolocate ressources hello internet. Par exemple, lorsque vous entrez une adresse d’application web dans votre navigateur, ou cliquez sur un lien sur une page web, il utilise domaine de hello tootranslate DNS en adresse IP. adresse IP de Hello est comme une adresse postale, mais il n’est pas très humaine convivial. Par exemple, il est beaucoup plus facile tooremember un nom DNS, tel que **contoso.com** que celui qu’elle est tooremember une adresse IP comme 192.168.1.88 ou 2001:0:4137:1f67:24a2:3888:9cce:fea3.

Hello système DNS est basé sur *enregistrements*. Les enregistrements associent un *nom*spécifique, tel que **contoso.com**, à une adresse IP ou un autre nom DNS. Lorsqu’une application, comme un navigateur web, recherche un nom dans DNS, il trouve hello enregistrement et utilise ce que qu’elle pointe tooas hello adresse. Si hello valeur points toois une adresse IP, navigateur de hello utilise cette valeur. S’il pointe le nom DNS de tooanother, puis application hello a toodo résolution à nouveau. En fin de compte, toute résolution de nom génère une adresse IP.

Lorsque vous créez une application web dans le Service d’application, un nom DNS est automatiquement attribué toohello l’application web. Ce nom prend la forme hello  **&lt;yourwebappname&gt;. azurewebsites.net**. Il est également une adresse IP virtuelle disponible pour une utilisation lors de la création de DNS d’enregistrements, vous pouvez créer les enregistrements toohello de ce point de **. azurewebsites.net**, ou vous pouvez pointer toohello adresse.

> [!NOTE]
> adresse IP de Hello de votre application web change si vous supprimez et recréez votre application web ou modifiez hello en mode plan de Service de l’application trop**libre** une fois qu’elle a été définie trop**base**, **Shared**, ou **Standard**.
> 
> 

Il existe également plusieurs types d’enregistrements, présentant chacun ses propres fonctions et limites, mais les applications web n’en utilisent que deux : les enregistrements *A* et *CNAME*.

### <a name="address-record-a-record"></a>Enregistrement d'adresse (enregistrement A)
Un enregistrement A mappe à un domaine, tel que **contoso.com** ou **www.contoso.com**, *ou un domaine générique* comme  **\*. contoso.com**, adresse IP de tooan. Dans les cas de hello d’une application web dans le Service d’applications, soit hello adresse IP virtuelle du service de hello ou une adresse IP spécifique que vous avez achetées pour votre application web.

Hello principaux avantages d’un enregistrement sur un enregistrement CNAME existe :

* Vous pouvez mapper un domaine racine, tel que **contoso.com** adresse IP de tooan ; bureaux d’enregistrement de nombreux autorise uniquement à l’aide d’enregistrements A
* L’une de vos entrées peut utiliser un caractère générique (**\*.contoso.com**, par exemple) afin de gérer les demandes pour plusieurs sous-domaines, tels que **mail.contoso.com**, **blogs.contoso.com** ou **www.contoso.com**.

> [!NOTE]
> Dans la mesure où un enregistrement est mappé tooa adresse IP, il ne peut pas résoudre automatiquement les modifications toohello IP adresse de votre application web. Une adresse IP pour une utilisation avec un enregistrement est fournie lorsque vous configurez les paramètres de nom de domaine personnalisé pour votre application web ; Toutefois, cette valeur peut changer si vous supprimez et recréez votre application web ou modifiez hello tooback de mode plan App Service trop**libre**.
> 
> 

### <a name="alias-record-cname-record"></a>Enregistrement d'alias (enregistrement CNAME)
Un enregistrement CNAME associe un *spécifique* nom DNS, tel que **mail.contoso.com** ou **www.contoso.com**, nom de domaine (canonique) tooanother. Dans les cas de hello d’application de Service Web Apps, nom de domaine canonique hello est hello  **&lt;yourwebappname >. azurewebsites.net** nom de domaine de votre application web. Une fois créé, hello CNAME crée un alias pour hello  **&lt;yourwebappname >. azurewebsites.net** nom de domaine. Hello entrée CNAME peut résoudre l’adresse IP de toohello de votre  **&lt;yourwebappname >. azurewebsites.net** nom de domaine automatiquement, donc si l’adresse IP de hello de hello web application change, vous n’avez pas n’importe quelle action aux tootake.

> [!NOTE]
> Des bureaux d’enregistrement de domaine vous permettre uniquement de sous-domaines de toomap lors de l’utilisation d’un enregistrement CNAME, tel que **www.contoso.com**et non racine, les noms tels que **contoso.com**. Pour plus d’informations sur les enregistrements CNAME, consultez la documentation hello fournie par votre bureau d’enregistrement, <a href="http://en.wikipedia.org/wiki/CNAME_record">hello Wikipédia sur l’enregistrement CNAME</a>, ou hello <a href="http://tools.ietf.org/html/rfc1035">IETF de noms de domaine - implémentation et spécification</a> document.
> 
> 

### <a name="web-app-dns-specifics"></a>Spécifications DNS des applications web
À l’aide d’un enregistrement A avec Web Apps nécessite que vous toofirst créer l’un des hello les enregistrements TXT suivants :

* **Pour le domaine racine de hello** -enregistrement A DNS TXT de  **@**  trop  **&lt;yourwebappname&gt;. azurewebsites.net**.
* **Pour un sous-domaine spécifique** -nom DNS d’un de  **&lt;sous-domaine >** trop**&lt;yourwebappname&gt;. azurewebsites.net**. Par exemple, **blogs** si un enregistrement de hello concerne **blogs.contoso.com**.
* **Pour les caractères génériques de hello sub-dodmains** -enregistrement A DNS TXT de *** trop  **&lt;yourwebappname&gt;. azurewebsites.net**.

Cet enregistrement TXT est tooverify utilisé que vous possédez le domaine hello vous essayez de toouse. Il s’agit en outre toocreating un un enregistrement qui pointe de toohello une adresse IP virtuelle de votre application web.

Vous pouvez trouver d’adresse IP de hello et **. azurewebsites.net** hello de noms pour votre application web en procédant comme suit :

1. Dans votre navigateur, ouvrez hello [Azure Portal](https://portal.azure.com).
2. Bonjour **Web Apps** panneau, cliquez sur nom hello de votre application web, puis sélectionnez **les domaines personnalisés** bas hello de page de hello.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. Bonjour **les domaines personnalisés** panneau, vous verrez hello adresse IP virtuelle. Enregistrez ces informations, car elles serviront lors de la création d’enregistrements DNS.
   
    ![](./media/custom-dns-web-site/virtual-ip-address.png)
   
   > [!NOTE]
   > Vous ne pouvez pas utiliser des noms de domaine personnalisé avec un **libre** application web et doit mettre à niveau hello plan App Service trop**Shared**, **base**, **Standard**, ou **Premium** couche. Pour plus d’informations sur hello du Service d’applications plan de tarification niveaux, y compris comment toochange hello niveau tarifaire de votre application web, consultez [tooscale comment les applications web](../articles/app-service-web/web-sites-scale.md).
   > 
   > 

