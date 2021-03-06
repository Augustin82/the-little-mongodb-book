# À propos de ce livre #

## Licence ##
Le petit livre de MongoDB est sous licence Attribution-NonCommercial 3.0 Unported license. **Ce livre devrait vous avoir été fourni gratuitement.**

Vous êtes libre de copier, distribuer, modifier ou afficher ce livre. Cependant, je vous prie de bien vouloir attribuer ce livre à son auteur, Karl Seguin, et de ne pas en faire un usage commercial.

Vous pouvez consulter le texte intégral de la licence à l'adresse suivante&nbsp;:

<http://creativecommons.org/licenses/by-nc/3.0/legalcode.fr>

## À propos de l'auteur ##
Karl Seguin est un développeur expérimenté dans divers domaines et technologies. Il est expert en .NET et en Ruby. Il contribue semi-activement à des logiciels open source, écrit des articles techniques et présente parfois des conférences. En ce qui concerne MongoDB, il était l'un des contributeurs principaux à NoRM, la bibliothèque MongoDB pour C#, et a écrit le tutoriel interactif [mongly](http://mongly.com) ainsi que [Mongo Web Admin](https://github.com/karlseguin/Mongo-Web-Admin). Son service gratuit pour les développeurs de jeux *casual*, [mogade.com](http://mogade.com/), utilise MongoDB.

Karl a depuis écrit [The Little Redis Book (en anglais)](http://openmymind.net/2012/1/23/The-Little-Redis-Book/)/[Le petit livre de Redis (en français)](http://url.to.translation)

Son blog se trouve à <http://openmymind.net> et il twitte depuis [@karlseguin](http://twitter.com/karlseguin).

## Remerciements ##
Un merci tout particulier à [Perry Neal](http://twitter.com/perryneal) pour m'avoir prêté ses yeux, son esprit et sa passion. Son aide m'a été inestimable. Merci.

## Dernière version ##
La version la plus récente de ce livre est disponible à&nbsp;:

<http://github.com/karlseguin/the-little-mongodb-book> (en anglais).
<http://url.to.translation> (en français).

# Introduction #
 > Si les chapitres sont courts, c'est qu'il est vraiment simple d'apprendre MongoDB.

On dit souvent que la technologie avance à un rythme effréné, et il est vrai que des nouvelles technologies et techniques apparaissent constamment. Et pourtant, j'ai longtemps pensé que les technologies fondamentales utilisées par les développeurs avançaient en fait plutôt lentement. On peut arrêter de se former pendant des années sans pour autant être complètement dépassé. Mais le plus étonnant, c'est la vitesse à laquelle les technologies sont remplacées. Du jour au lendemain, des technologies bien établies se retrouvent menacées par un changement d'approche des développeurs.

Rien n'illustre mieux ce changement soudain que la progression des technologies NoSQL en regard des vénérables bases de données relationnelles. Hier encore, le web semblait tourner sur quelques RDBMS (systèmes de gestion de bases de données relationnelles ou SGBD), et voilà qu'aujourd'hui, une demi-douzaine de solutions NoSQL se sont imposées comme des alternatives crédibles.

Bien que ces transitions puissent paraître soudaines, il faut en fait plusieurs années pour qu'elles soient acceptées. L'enthousiasme initial est porté par un nombre relativement restreint de développeurs et d'entreprises. Les solutions sont affinées, des leçons sont tirées, et c'est seulement quand la technologie paraît fermement installée que d'autres l'intègrent progressivement. Là encore, c'est particulièrement vrai pour NoSQL, où plusieurs solutions ne sont pas seulement des alternatives aux solutions de stockage traditionnelles mais répondent en plus à un nouveau besoin spécifique.

Cela étant dit, la première chose à faire est de préciser ce que l'on entend par NoSQL, un terme assez vague utilisé par différentes personnes pour signifier différentes choses. Personnellement, je l'utilise au sens large pour un système qui joue un rôle dans la gestion de données. Autrement dit, NoSQL signifie, à mon sens, que la couche de persistence des données n'est pas forcément de la responsabilité d'un système unique. Alors qe les vendeurs de bases de données relationnelles les ont historiquement présentées comme des solutions miracles, NoSQL tend vers uen organisation en unités plus petites, dans lesquelles l'outil le plus adapté peut être utilisé au mieux. Ainsi, une pile NoSQL pourra toujours s'appuyer sur une base de données relationnelle (disons, MySQL), mais utilisera également Redis pour assurer la persistence de certaines parties du système et Hadoop pour le traitement intensif des données. Pour faire simple, approche'l NoSQL consiste à être ouvert à des outils alternatifs pour gérer ses données.

Vous vous demandez peut-être où se situe MongoDB, dans tout ça. En tant que base de données orientée *document*, Mongo est une solution NoSQL plus généralisée. Il faut la voir comme une alternative aux bases relationnelles. Comme elles, Mongo peut tirer parti de certaines des solutions NoSQL les plus spécialisées. MongoDB a ses avantages et ses inconvénients, comme nous allons le voir par la suite.

Vous l'aurez remarqué&nbsp;: nous utilisons indifféremment les termes *MongoDB* et *Mongo*.

# Pour débuter #
La majeure partie de ce livre sera consacrée aux fonctionnalités principales de MongoDB. Nous nous appuierons donc sur la ligne de commande de MongoDB. Bien qu'étant un outil utile à l'apprentissage comme à l'administration, votre code, lui, utilisera un pilote MongoDB.

Cela nous amène à parler d'un élément essentiel de MongoDB&nbsp;: ses pilotes. Mongo dispose d'[un certain nombre de pilotes officiels](http://www.mongodb.org/display/DOCS/Drivers) pour divers langages. Ces pilotes sont semblables aux pilotes de bases de données avec lesquels vous êtes coutumier. En plus de ces pilotes, la communauté a produit d'autres bibliothèques spécifiques à des langages ou des *frameworks*. Ainsi, [NoRM](https://github.com/atheken/NoRM) est une bibliothèque C# qui implémente LINQ, et [MongoMapper](https://github.com/jnunemaker/mongomapper) est une bibliothèque Ruby compatible avec ActiveRecord.

Vous avez le choix d'utiliser directement les pilotes MongoDB dans votre code ou de passer par des bibliothèques haut niveau. Il s'agit d'une source habituelle de confusion pour les débutants, qui se demandent pourquoi il existe des pilotes officiels et des bibliothèques créées par la communauté. C'est que les premiers sont consacrés aux fonctionnalités de base de communication et de connectivité avec MongoDB alors que les seconds concernent des implémentations spécifiques à des langages ou des *frameworks*.

Lors de votre lecture, je vous encourage à jouer avec MongoDB pour reproduire ce que je présente, mais aussi pour répondre aux questions qui pourraient vous venir. Il est très facile de débuter avec MongoDB. Prenons quelques instants pour tout installer.

1. Rendez vous sur la [page de téléchargement officiel](http://www.mongodb.org/downloads) et récupérez les binaires de la première ligne (la version stable recommandée) pour le système d'exploitation de votre choix. Pour le développement, vous pouvez utiliser indifféremment les versions 32 et 64 bits.

2. Décompressez l'archive (où vous le souhaitez) et naviguez jusqu'au sous-répertoire `bin`. Ne lancez rien pour l'instant, mais sachez que `mongod` est le processus serveur et `mongo` le *shell* client. Ce sont les deux exécutables avec lesquels vous allez passer le plus de temps.

3. Créez un fichier texte dans le sous-répertoire `bin` et nommez-le `mongodb.config`

4. Ajoutez une ligne dans mongodb.config&nbsp;: `dbpath=PATH_TO_WHERE_YOU_WANT_TO_STORE_YOUR_DATABASE_FILES`. Ainsi, pour Windows, cela donnera quelque chose comme `dbpath=c:\mongodb\data`, et pour Linux `dbpath=/var/lib/mongodb/data`.

5. Assurez-vous que le chemin `dbpath` indiqué existe bien.

6. Lancez mongod avec le paramètre `--config /path/to/your/mongodb.config`.

Pour les utilisateurs de Windows, si vous avez extrait le fichier téléchargé dans `c:\mongodb\` et que vous avez créé `c:\mongodb\data\`, vous devrez indiquer `dbpath=c:\mongodb\data\` dans `c:\mongodb\bin\mongodb.config`. Vous pourrez alors lancer `mongod` depuis l'invite de commandes en utilisant `c:\mongodb\bin\mongod --config c:\mongodb\bin\mongodb.config`.

N'hésitez pas à ajouter le répertoire `bin` à votre *PATH* pour rendre tout ceci moins verbeux. Les utilisateurs de MacOS X et de Linux pourront suivre les mêmes instructions, à part que les chemins seront différents.

Si tout s'est bien passé, MongoDB sera fonctionnel. Si vous obtenez une erreur, lisez attentivement les messages d'erreur&nbsp;: le programme explique généralement très bien ce qui ne va pas.

Vous pouvez désormais lancer `mongo` (sans le *d* !), ce qui connectera un *shell* à votre serveur. Essayez de taper `db.version()` pour vérifier que tout fonctionne bien. Vous devriez obtenir le numéro de la version que vous avez installée.

# Chapitre 1 - Les bases #
Commençons par nous familiariser avec les mécanismes de base de MongoDB. Bien sûr, c'est crucial pour comprendre MongoDB, mais cela nous aidera également à répondre aux questions de plus haut niveau sur le rôle de MongoDB.

Pour débuter, il nous faut comprendre six concepts simples.

1. MongoDB dispose du concept de `databases` (base de données) qui vous est certainement familier (pour les utilisateurs d'Oracle, il s'agit des `schemas`). Une instance de MongoDB peut contenir zéro et plus bases de données, chacune étant un conteneur de haut niveau pour tout le reste.

2. Une base peut contenir zéro et plus `collections`. Une collection a suffisamment en commun avec les `tables` classiques pour les considérer comme équivalentes.

3. Une collection se compose de zéro et plus `documents`. Là encore, un document est semblable à un `row` (*ligne*).

4. Un document contient un ou plusieurs `fields` (*champs*), qui ressemblent étrangement aux `columns` (*colonnes*).

5. Dans MongoDB, les `indexes` (*index*) fonctionnent comme leur équivalent des SGBD.

6. Les `cursors` (*curseurs*) sont différents des autres concepts mais suffisamment importants (et souvent oubliés !) pour mériter qu'on s'y attarde. Ce qu'il faut comprendre, c'est que lorsque l'on demande des données à MongoDB, on obtient un curseur ; on peut le manipuler, le compter, le déplacer, sans *réellement* récupérer les données.

Pour résumer, MongoDB est composé de `databases` qui contiennent des `collections`. Une `collection` rassemble des `documents` formé par des `fields`. Les `collections` peuvent être `indexées`, ce qui améliore les performances de recherche et de tri. Enfin, lorsque l'on demande des données à MongoDB, on récupère en fait un `cursor`, dont l'exécution n'est effectuée que quand elle est vraiment nécessaire.

Pourquoi cette nouvelle terminologie (collection/table, document/row et field/column) ? Pas simplement pour rendre les choses plus compliquées&nbsp;: même si ces concepts sont proches de leurs équivalents relationnels, ils ne sont pas identiques. La principale différence repose sur le fait que les BDD relationnelles définissent leurs `columns` au niveau d'une `table` alors qu'une BDD orientée document définit ses `fields` au niveau d'un document. Autrement dit, chaque `document` au sein d'une `collection` peut contenir son propre ensemble de `fields` uniques. Ainsi, une `collection` n'est qu'un `table` simplifiée alors qu'un `document` contient bien plus d'informations qu'un `row`.

Même si ces concepts sont essentiels, ne paniquez pas si tout n'est pas encore clair pour vous. Après quelques *inserts*, vous comprendrez ce que cela signifie. Pour faire simple, une collection n'impose pas un format strict (on parle de *schema-less*), mais les fields sont contrôlés au sein de chaque document. Les avantages et inconvénients de cette méthode seront présentés plus loin.

Mettons la main à la pâte. Si vous ne l'avez pas encore fait, lancez le serveur `mongod` et un *shell* mongo. Le *shell* accepte le JavaScript. Vous pouvez exécuter des commandes globales, comme `help` ou `exit`. Les commandes que vous exécutez sur la base de données courante se lancent avec l'objet `db`, comme ceci&nbsp;: `db.help()` ou `db.stats()`. Les commandes appliquées à une collection spécifique, ce que nous allons souvent faire par la suite, se basent sur l'objet `db.NOM_DE_LA_COLLECTION`, par exemple&nbsp;: `db.unicorns.help()` ou `db.unicorns.count()`.

Tapez `db.help()`&nbsp;: vous obtenez la liste des commandes que vous pouvez appliquer à l'objet `db`.

Une remarque&nbsp;: comme il s'agit d'un *shell* JavaScript, si vous lancez une méthode sans les parenthèses `()` à la fin, vous verrez le code de la méthode au lieu de l'exécuter. Ne soyez pas surpris quand vous oublierez de les mettre et que vous aurez comme résultat `function (...){`. Ainsi, si vous tapez `db.help` sans les parenthèses, vous verrez l'implémentation interne de la méthode `help`.

Tout d'abord, nous allons utiliser la méthode globale `use` pour changer de BDD&nbsp;: tapez `use learn`. Peu importe que la base n'existe pas encore&nbsp;: la première collection que nous allons ajouter créera effectivement la base `learn`. Maintenant que vous êtes dans une base, vous pouvez commencer à exécuter des commandes de base, comme `db.getCollectionNames()`. Si vous tapez cela, vous devriez obtenir un tableau vide (`[]`). Puisque les collections sont *schema-less*, nous n'avons pas besoin de les créer&nbsp;: il suffit d'insérer un document dans une nouvelle collection. Pour ce faire, on utilise la commande `insert` à laquelle on fournit le document à insérer&nbsp;:

	db.unicorns.insert({name: 'Aurora', gender: 'f', weight: 450})

La ligne ci-dessus exécute `insert` dans la collection `unicorns` en lui fournissant un unique argument. En interne, MongoDB utilise un format JSON binaire sérialisé. En externe, cela veut dire qu'on utilise beaucoup JSON, comme pour nos paramètres ci-dessus. Si l'on exécute maintenant `db.getCollectionNames()`, on verra deux collections&nbsp;: `unicorns` et `system.indexes`. La collection `system.indexes` est créée une fois par base et contient l'information sur l'index de notre BDD.

Vous pouvez maintenant utiliser la commande `find` dans `unicorns` pour obtenir une liste de documents&nbsp;:

	db.unicorns.find()

Vous remarquerez que, en plus des données que vous avez spécifiées, il y a un champ `_id`. Chaque document doit contenir un champ `_id` unique. Vous pouvez l'indiquer vous-même, mais la plupart du temps vous laisserez sûrement MongoDB générer un *ObjectId* pour vous. Le champ `_id` est indexé par défaut, ce qui explique que la collection `system.indexes` ait été créée. Vous pouvez étudier `system.indexes`&nbsp;:

	db.system.indexes.find()

Vous voyez là le nom de l'index, la BDD et la collection pour lesquelles il a été créé, et les champs inclus dans l'index.

Revenons à nos collections *schema-less*. Essayez d'insérer un document totalement différent dans `unicorns`, par exemple&nbsp;:

	db.unicorns.insert({name: 'Leto', gender: 'm', planet: 'Arrakis', worm: false})


Là encore, utilisez `find` pour lister les documents. Quand nous en saurons un peu plus, nous discuterons de ce comportement intéressant de MongoDB, mais vous devriez déjà commencer à comprendre en quoi les solutions classiques ne convenaient plus.

## Maîtriser les selectors ##
En plus des six concepts que nous avons explorés, il y a un aspect pratique de MongoDB qu'il est important de bien comprendre, avant de pouvoir aborder des sujets plus complexes&nbsp;: il s'agit des *query selectors*, les selectors de requête. Un *query selector* est l'équivalent pour MongoDB de la clause `where` d'une requête SQL. On l'utilise pour trouver, compter, mettre à jour et effacer des documents dans des sélections. Un selector est un objet JSON ; le plus simple, `{}`, sélectionne tous les documents (`null` marche aussi). Si l'on voulait trouver toutes les unicorns femelles, on pourrait utiliser `{gender: 'f'}`.

Avant de se plonger plus avant dans les selectors, nous allons créer des données avec lesquelles jouer. D'abord, nous allons supprimer ce que nous avons mis précédemment dans `unicorns` avec `db.unicorns.remove()` (nous ne précisons pas de selector, donc tous les documents seront supprimés). Maintenant, saisissez les commandes suivantes pour obtenir des données (je vous recommande d'utiliser un coper-coller)&nbsp;:

	db.unicorns.insert({name: 'Horny', dob: new Date(1992,2,13,7,47), loves: ['carrot','papaya'], weight: 600, gender: 'm', vampires: 63});
	db.unicorns.insert({name: 'Aurora', dob: new Date(1991, 0, 24, 13, 0), loves: ['carrot', 'grape'], weight: 450, gender: 'f', vampires: 43});
	db.unicorns.insert({name: 'Unicrom', dob: new Date(1973, 1, 9, 22, 10), loves: ['energon', 'redbull'], weight: 984, gender: 'm', vampires: 182});
	db.unicorns.insert({name: 'Roooooodles', dob: new Date(1979, 7, 18, 18, 44), loves: ['apple'], weight: 575, gender: 'm', vampires: 99});
	db.unicorns.insert({name: 'Solnara', dob: new Date(1985, 6, 4, 2, 1), loves:['apple', 'carrot', 'chocolate'], weight:550, gender:'f', vampires:80});
	db.unicorns.insert({name: 'Ayna', dob: new Date(1998, 2, 7, 8, 30), loves: ['strawberry', 'lemon'], weight: 733, gender: 'f', vampires: 40});
	db.unicorns.insert({name: 'Kenny', dob: new Date(1997, 6, 1, 10, 42), loves: ['grape', 'lemon'], weight: 690,  gender: 'm', vampires: 39});
	db.unicorns.insert({name: 'Raleigh', dob: new Date(2005, 4, 3, 0, 57), loves: ['apple', 'sugar'], weight: 421, gender: 'm', vampires: 2});
	db.unicorns.insert({name: 'Leia', dob: new Date(2001, 9, 8, 14, 53), loves: ['apple', 'watermelon'], weight: 601, gender: 'f', vampires: 33});
	db.unicorns.insert({name: 'Pilot', dob: new Date(1997, 2, 1, 5, 3), loves: ['apple', 'watermelon'], weight: 650, gender: 'm', vampires: 54});
    db.unicorns.insert({name: 'Nimue', dob: new Date(1999, 11, 20, 16, 15), loves: ['grape', 'carrot'], weight: 540, gender: 'f'});
	db.unicorns.insert({name: 'Dunx', dob: new Date(1976, 6, 18, 18, 18), loves: ['grape', 'watermelon'], weight: 704, gender: 'm', vampires: 165});

Nous avons des données, nous allons pouvoir maîtriser les selectors. `{champ: valeur}` est utilisé pour trouver des documents où le `champ` est égal à `valeur`. Pour obtenir un `et`, on utilise `{champ1: valeur1, champ2: valeur2}`. Pour effectuer les comparaisons inférieur, inférieur ou égal, supérieur, supérieur ou égal, et différent, on utilise `$lt`, `$lte`, `$gt`, `$gte`, et `$ne`. Par exemple, pour trouver les unicorns mâles qui pèsent plus de 700 livres, on pourrait utiliser&nbsp;:

	db.unicorns.find({gender: 'm', weight: {$gt: 700}})
	// ou encore (pas strictement identique, mais utilisé pour montrer les possibilités)
	db.unicorns.find({gender: {$ne: 'f'}, weight: {$gte: 701}})

L'opérateur `$exists` est utilisé pour valider la présence ou l'absence d'un champ. Ainsi, l'exemple&nbsp;:

	db.unicorns.find({vampires: {$exists: false}})

ne devrait retourner qu'un seul document. Pour appliquer l'opérateur `ou` plutôt que `et`, on utilise `$or` et on lui assigne la liste des valeurs auxquelles appliquer le `ou`&nbsp;:

	db.unicorns.find({gender: 'f', $or: [{loves: 'apple'}, {loves: 'orange'}, {weight: {$lt: 500}}]})

La commande ci-dessus va retourner toutes les unicorns femelles qui soit aiment les apples, soit aiment les oranges, soit pèsent moins de 500 livres.

Cet exemple est très intéressant&nbsp;: vous l'avez peut-être déjà remarqué, mais le champ `loves` est un tableau. MongoDB accepte les tableaux comme objets à part entière, ce qui est extrêmement pratique. Une fois que vous commencerez à l'utiliser, vous vous demanderez comment vous faisiez, avant. Plus intéressant encore, la facilité avec laquelle on peut faire une sélection sur la valeur d'un tableau&nbsp;: `{loves: 'watermelon'}` va retourner tous les documents dans lesquels `watermelon` est une valeur de `loves`.

Il y a d'autres opérateurs que ceux que nous avons vus pour l'instant. Le plus flexible est `$where` qui permet de passer du JavaScript à exécuter sur le serveur. Ils sont tous décrits dans la section [Advanced Queries](http://www.mongodb.org/display/DOCS/Advanced+Queries#AdvancedQueries) du site de MongoDB. Ceux que nous avons vus jusqu'à présents sont ceux dont vous avez besoin pour démarrer. Ce sont aussi ceux que vous utiliserez le plus souvent.

Nous avons vu que ces selectors peuvent être utilisés avec la commande `find`. Ils peuvent aussi être utilisés avec la commande `remove` que nous avons abordée brièvement, la commande `count` dont vous devinez probablement l'utilité, et la commande `update` avec laquelle nous allons passer du temps plus tard.

Le `ObjectId` que MongoDB a généré pour notre champ `_id` peut être sélectionné comme ceci&nbsp;:

	db.unicorns.find({_id: ObjectId("monObjectId")})

## Résumé du chapitre ##
Nous n'avons pas encore abordé la commande `update` ou certaines utilisations avancées de `find`. Par contre, nous avons fait fonctionner MongoDB, survolé les commandes `insert` et `remove` (il n'y a pas grand chose de plus à savoir !), et présenté `find` et les `selectors` MongoDB. Nous sommes partis sur des bases solides. Croyez-le ou pas, mais vous connaissez désormais l'essentiel de ce qu'il y a à savoir sur MongoDB&nbsp;: c'est conçuç pour être rapide à apprendre et facile à utiliser. Je recommande vivement de jouer encore un peu avec votre BDD locale avant de passer à la suite. Insérez des documents différents, éventuellement dans de nouvelles collections, et familiarisez-vous avec les selectors. Utilisez `find`, `count`, et `remove`. Après quelques essais par vous-même, ce qui vous avait échappé au début devrait devenir plus clair.

# Chapitre 2 - Update #
Dans le premier chapitre, nous avons présenté trois des quatre opérations CRUD (*create*, *read*, *update*, et *delete* soit créer, lire, mettre à jour et effacer). Le présent chapitre est donc consacré à celle qui manque&nbsp;: `update`, et à son fonctionnement parfois un peu surprenant.

## Update&nbsp;: Replace ou $set ? ##
Dans sa forme la plus simple, `update` prend deux arguments&nbsp;: le selector (*where*) à utiliser, et le champ à mettre à jour. Si Roooooodles a pris un peu de poids, on peut exécuter&nbsp;:

	db.unicorns.update({name: 'Roooooodles'}, {weight: 590})

(Si vous avez joué avec votre collection `unicorns` et qu'elle ne contient plus les données originales, repartez de zéro en faisant `remove` puis en ré-utilisant le code du chapitre 1.)

S'il s'agissait de vrai code, on utiliserait sûrement `_id` pour mettre à jour les données. Mais comme je ne sais pas quel `_id` MongoDB a généré pour vous, nous allons utiliser le `name`. Jetons maintenant un œil sur la mise à jour&nbsp;:

	db.unicorns.find({name: 'Roooooodles'})

Première surprise d'`update`&nbsp;: aucun document n'est trouvé. En effet, le deuxième paramètre fourni est utilise pour **remplacer** l'original. Autrement dit, `update` a trouvé un document basé sur son `name` et a remplacé le document entier par le nouveau document (le second paramètre). Ce fonctionnement est différent de celui de la commande `update` en SQL. Dans certains cas, ce comportement est très utile pour des mises à jour vraiment dynamiques. Cependant, quand vous souhaitez simplement remplacer la valeur d'un ou plusieurs champs, il est mieux d'utiliser le modificateur `$set` de MongoDB&nbsp;:

    db.unicorns.update({weight: 590}, {$set: {name: 'Roooooodles', dob: new Date(1979, 7, 18, 18, 44), loves: ['apple'], gender: 'm', vampires: 99}})

Nous voilà de nouveau avec les champs du début. `poids` n'a pas été modifié puisque nous ne l'avons pas spécifié. Maintenant, si l'on exécute&nbsp;:

	db.unicorns.find({name: 'Roooooodles'})

on obtient le résultat attendu. La méthode qu'il aurait fallu utiliser pour mettre le poids à jour est donc&nbsp;:

	db.unicorns.update({name: 'Roooooodles'}, {$set: {weight: 590}})

## Modificateurs de update ##
En plus de `$set`, on peut utiliser d'autres modificateurs pour faire des trucs sympas. Tous ces modificateurs de update fonctionne sur les champs, donc vous n'allez pas effacer tout votre document. Ainsi, le modificateur `$inc` est utilisé pour incrémenter un champ d'une certaine quantité, positive ou négative. Par exemple, si on a attribué à Pilot trop de *kills* de vampires, on peut corriger l'erreur avec&nbsp;:

	db.unicorns.update({name: 'Pilot'}, {$inc: {vampires: -2}})

Si Aurora succombe à l'attrait des sucreries, on peut ajouter une valeur à son champ `loves` avec le modificateur `$push`&nbsp;:

	db.unicorns.update({name: 'Aurora'}, {$push: {loves: 'sugar'}})

La section [Updating](http://www.mongodb.org/display/DOCS/Updating) du site de MongoDB dispose de plus d'information sur les autres modificateurs disponibles.

## Upserts ##
L'une des bonnes surprises de `update` est qu'on peut utiliser un `upsert`. Un `upsert` met à jour un document s'il existe ou le crée sinon. C'est très utile dans certaines situations&nbsp;: vous les reconnaîtrez quand vous les verrez. Pour utiliser `upsert`, il faut utiliser un troisième paramètre, `true`.

Exemple trivial&nbsp;: un compteur de hits pour un site. Si on voulait avoir un compte total en temps réel, il faudrait vérifier si une entrée existe déjà pour la page, et décider d'utiliser `update` ou `insert`. Avec un troisième paramètre omis (ou `false`), les commandes suivantes ne feraient rien&nbsp;:

	db.hits.update({page: 'unicorns'}, {$inc: {hits: 1}});
	db.hits.find();

Par contre, si on active les upserts, le résultat est différent&nbsp;:

	db.hits.update({page: 'unicorns'}, {$inc: {hits: 1}}, true);
	db.hits.find();

Comme aucun document n'existe avec un champ `page` avec la valeur `unicorns`, un nouveau document est créé. Si la commande est exécutée à nouveau, le document existant est mis à jour et `hits` est incrémenté à 2.

	db.hits.update({page: 'unicorns'}, {$inc: {hits: 1}}, true);
	db.hits.find();

## Updates multiples ##
La dernière surprise que nous réserve `update`, c'est que, par défaut, un seul document est mis à jour. Dans les exemples que nous avons vus, cela paraît logique. En revanche, si l'on exécute quelque chose comme ça&nbsp;:

	db.unicorns.update({}, {$set: {vaccined: true }});
	db.unicorns.find({vaccined: true});

on s'attendrait à récupérer toutes nos chères unicorns qui doivent être vaccinées. Pour obtenir le comportement désiré, il faut ajouter un quatrième paramètre et lui assigner `true`&nbsp;:

	db.unicorns.update({}, {$set: {vaccined: true }}, false, true);
	db.unicorns.find({vaccined: true});

## Résumé du chapitre ##
Ce chapitre a conclu notre présentation des opérations CRUD disponibles pour une collection. Nous nous sommes intéressés en particulier à `update` et avons observé trois comportements intéressants. D'abord, contrairement à SQL, un `update` MongoDB remplace le document trouvé. Le modificateur `$set` est donc très utile. Ensuite, `update` propose une variante `upsert` très utile, surtout combinée au modificateur `$inc`. Enfin, par défaut, `update` ne met à jour que le premier document trouvé.

Rappelez-vous que nous utilisons MongoDB depuis son *shell*. Le pilote ou la bibliothèque que vous utiliserez pourront modifier ces comportements par défaut ou exposer une API différente. Ainsi, le pilote Ruby fusionne les deux derniers paramètres en un seul élément&nbsp;: `{:upsert => false, :multi => false}`. De même, les pilote PHP les fusionne dans un tableau&nbsp;: `array('upsert' => false, 'multiple' => false)`.

# Chapitre 3 - Maîtriser find #
Dans le chapitre 1, nous avons brièvement abordé la commande `find`. Mais il y a bien plus à savoir à son sujet que les `selectors`. Nous avons déjà vu que le résultat d'un `find` est un `cursor`. Nous allons maintenant voir en détail ce que cela signifie.

## Sélection de champ ##
Avant de s'occuper de `cursor`, il faut savoir que `find` prend un deuxième paramètre, optionnel&nbsp;: la liste des champs que l'on souhaite récupérer. Ainsi, on peut obtenir les noms de toutes les licornes en exécutant&nbsp;:

	db.unicorns.find(null, {name: 1});

Par défaut, le champ `_id` est toujours retourné. On peut l'exclure en spécifiant `{name:1, _id: 0}`.

À part pour le champ `_id`, on ne peut mélanger les inclusions et les exclusions. C'est logique, finalement&nbsp;: on veut soit sélectionner soit exclure un ou plusieurs champs explicitement.

## Classer ##
J'ai déjà dit plusieurs fois que `find` retourne un curseur dont l'exécution est retardée jusqu'à ce qu'on en ait besoin. Pourtant, vous avez sans doute remarque que, dans le *shell*, `find` s'exécute immédiatement. Ce comportement est propre au *shell* uniquement. On peut voir le véritable comportement d'un `cursor` en observant une méthode que l'on enchaîne avec `find`. La première que l'on va étudier est `sort`. `sort` est semblable à la sélection de champs vue à la section précédente. On spécifie les champs selon lesquels on veut classer, en utilisant 1 pour l'ordre croissant, -1 pour l'ordre décroissant. Par exemple&nbsp;:

	//Les licornes les plus lourdes en premier
	db.unicorns.find().sort({weight: -1})

	//Par nom de licorn puis par nombre de vampires tués
	db.unicorns.find().sort({name: 1, vampires: -1})

Comme pour les bases relationnelles, MongoDB peut utiliser un index pour le classement. Nous reviendrons sur les index un peu plus tard, mais sachez que MongoDB limite la taille des tris sans index. Autrement dit, si vous essayez de trier un grand ensemble de résultats qui n'utilisent pas d'index, vous recevrez une erreur. Certains voient ça comme une limitation ; je pense moi que plus de bases de données devraient pouvoir refuser d'exécuter des requêtes non optimisées. (Je ne vais pas essayer de faire passer tous les inconvénients de Mongo pour des avantages, mais j'ai vu tellement de bases mal optimisées que j'aimerais vraiment qu'elles disposent d'un mode strict.)

## Pagination ##
Les résultats peuvent être "mis en page" avec les méthodes `limit` et `skip`. Ainsi, pour obtenir les deuxième et troisième licornes les plus lourdes, on ferait&nbsp;:

	db.unicorns.find().sort({weight: -1}).limit(2).skip(1)

Attention&nbsp;: utiliser `limit` avec `sort`, c'est s'exposer à toutes sortes de problèmes si on travaille avec des champs non indexés.

## Compte ##
Le *shell* permet de faire un `count` directement sur une collection&nbsp;:

	db.unicorns.count({vampires: {$gt: 50}})

En fait, `count` est un raccourci du *shell* pour une méthode `cursor`. Les pilotes qui ne fournissent pas ce raccourci doivent utiliser la commande suivante, qui fonctionnera aussi dans le *shell*&nbsp;:

	db.unicorns.find({vampires: {$gt: 50}}).count()

## Dans ce chapitre ##
L'utilisation de `find` et `cursor` est relativement évidente. Il y a quelques autres commandes que nous verrons plus tard ou qui ne sont utiles que dans quelques cas spécifiques, mais vous devriez déjà être suffisamment à l'aise en utilisant le *shell* et commencer à comprendre les principes fondamentaux de MongoDB.

# Chapitre 4 - Modèle de données #
Passons à la vitesse supérieure et parlons de MongoDB de manière un peu plus abstraite. Expliquer quelques termes et une nouvelle syntaxe, c'est assez trivial. En revanche, parler de modélisation dans un nouveau paradigme, c'est plus compliqué. Pour être honnête, la plupart d'entre nous expérimentent encore pour trouver ce qui fonctionne et ce qui ne fonctionne pas pour la modélisation avec cette nouvelle technologie. Il est poible d'aborder quelques pistes, mais il vous faudra forcément pratiquer sur du vrai code pour apprendre.

De toutes les bases NoSQL, les bases orientées documents sont peut-être les plus proches des bases relationnelles, en tout cas en ce qui concerne la modélisation. Mais si les différences sont subtiles, elles n'en sont pas moins importantes.

## Pas de jointure ##
La première différence, fondamentale, avec laquelle il faut se familiariser, c'est le manque de jointure. J'ignore pourquoi il n'existe même pas de fonction plus ou moins équivalente dans MongoDB, mais je sais que les jointures sont généralement considérées comme non extensibles. C'est-à-dire que, quand on commence à séparer ses données horizontalement, on finit toujours par faire les jointures côté client (le serveur d'application). Qu'importent les raisons, le fait est que les données sont relationnelles, et MongoDB ne propose pas de jointure.

Pour survivre sans jointure, il faut les faire dans le code applicatif. Concrètement, il faut lancer une deuxième requête `find` pour obtenir les données souhaitées. Préparer les données pour cela n'est pas bien différent de déclarer une clef étrangère dans une BDD relationnelle. Délaissons un peu nos `unicorns` pour revenir vers nos `employees`. Commençons par créer un employé (avec un `_id` explicite pour que l'on puisse voir ensemble des exemples concrets)&nbsp;:

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d730"), name: 'Leto'})

Ajoutons deux employés et assignons-leur `Leto` comme manager&nbsp;:

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d731"), name: 'Duncan', manager: ObjectId("4d85c7039ab0fd70a117d730")});
	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d732"), name: 'Moneo', manager: ObjectId("4d85c7039ab0fd70a117d730")});

(On rappelle qu'un `_id` peut prendre n'importe quelle valeur. Il est probable que vous utiliserez `OjbectId` en situation réelle, c'est donc ce que nous utiliserons ici.)

Évidemment, pour trouver les employés de Leto, on exécute&nbsp;:

	db.employees.find({manager: ObjectId("4d85c7039ab0fd70a117d730")})

Rien de magique ici. Dans le pire des cas, la plupart du temps, l'absence de jointure pourra être compensée par une simple requête supplémentaire (probablement indexée).

## Tableaux et documents imbriqués ##
Mongo n'a pas de jointures mais ne manque pas d'atouts. Nous avions rapidement abordé le fait qu'un tableau pouvait être un objet de première classe d'un document. Il se trouve que c'est très utile quand on a affaire à des relations 1-n ou n-n. Par exemple, si un employé pouvait avoir deux managers, on pourrait les enregistrer dans un tableau&nbsp;:

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d733"), name: 'Siona', manager: [ObjectId("4d85c7039ab0fd70a117d730"), ObjectId("4d85c7039ab0fd70a117d732")] })

Encore plus intéressant&nbsp;: `manager` peut être une valeur normale pour certains documents et un tableau pour d'autres. Notre requête `find` du début marcherait pour les deux&nbsp;:

	db.employees.find({manager: ObjectId("4d85c7039ab0fd70a117d730")})

Vous vous rendrez vite compte que les tableaux de valeurs sont bien plus simples à manipuler que des jointures de tables n-n.

En plus des tableaux, Mongo gère les imbrications de documents. Essayez d'insérer un document dans un document, comme ceci&nbsp;:

	db.employees.insert({_id: ObjectId("4d85c7039ab0fd70a117d734"), name: 'Ghanima', family: {mother: 'Chani', father: 'Paul', brother: ObjectId("4d85c7039ab0fd70a117d730")}})

Si vous vous posez la question, on peut appeler les documents imbriqués en utilisant un .&nbsp;:

	db.employees.find({'family.mother': 'Chani'})

Nous allons parler brièvement de l'utilité des documents imbriqués et de comment les utiliser.

## DBRef ##
Mongo utilise une chose appelée `DBRef` qui est une convention supportée par de nombreux pilotes. Lorsqu'un pilote rencontre un `DBRef`, il peut automatiquement récupérer le document référence. Un `DBRef` contient la collection et l'id du document référencé. Généralement, son utilité est très spécifique&nbsp;: quand les documents d'une même collection peuvent référencer des documents d'une collection différente de la leur. Par exemple, le `DBRef` de document1 pourrait pointer vers un document dans `managers` et le `DBRef` de document2, vers un document dans `employees`.

## Dénormalisation ##
Une autre alternative à l'utilisation de jointures est de dénormaliser ses données. Historiquement, la dénormalisation était réservée à du code pour lequel les performances étaient importantes, ou quand on pouvait faire des sauvegardes des données (comme pour un journal d'audit). Cependant, du fait de la popularité grandissante des bases NoSQL, qui permettent rarement les jointures, la dénormalisation fait de plus en plus souvent partie de la modélisation normale. Ça ne veut pas dire qu'il faut dupliquer toutes les informations dans tous les documents, mais plutôt qu'il ne faut pas avoir de dupliquer des données si le modèle le réclame.

Imaginons que l'on développe un forum. La méthode habituelle est d'associer un `user` spécifique à un `post` via une colonne `userid` dans `posts`. Dans ce modèle, il n'est pas possible d'afficher des `posts` sans récupérer (via une jointure) `users`. On peut plutôt stocker le `name`, en plus du `userid`, avec chaque `post`. On pourrait même le faire avec un document imbriqué&nbsp;: `user: {id: ObjectId('Something'), name: 'Leto'}`. Et, oui, si l'utilisateur change de nom, il faudra mettre chaque document à jour (mais cela se fait en une seule requête).

Cette habitude peut être difficile à prendre pour certains. Dans de nombreux cas, elle ne sera même pas pertinente. Mais n'hésitez surtout pas à l'essayer&nbsp;: non seulement elle convient dans certains cas, mais c'est parfois la meilleure des solutions.

## Que choisir ? ##
Les tableaux d'identifiants sont souvent utiles dans les cas 1-n ou n-n. On peut dire que les `DBRefs` ne sont pas souvent utilisées, même si vous pouvez évidemment jouer avec. Généralement, les développeurs débutants ne savent pas quoi utiliser entre les documents imbriqués et le référencement manuel.

D'abord, il faut savoir qu'un document individuel est actuellement limité à une taille de 16 Mo. Cette limite, bien que généreuse, donne une idée de la manière dont les documents devraient être utilisés. La plupart des développeurs utilisent des références manuelles pour la majorité de leurs relations. Ils exploitent souvent les capacités des documents imbriqués, mais surtout pour des petites quantités de données qui sont souvent demandées en même temps que le document parent. Un exemple concret est de stocker un document `accounts` pour chaque utilisateur, comme ceci&nbsp;:

	db.users.insert({name: 'leto', email: 'leto@dune.gov', account: {allowed_gholas: 5, spice_ration: 10}})

Mais ne sous-estimez pas pour autant les documents imbriqués&nbsp;: ce sont bien plus que des gadgets. Pouvoir plaquer son modèle de données directement sur ses objets facilite vraiment la vie, et permet souvent de se dispenser des jointures. C'est particulièrement vrai dans le cas de Mongo, qui permet de faire des requêtes et d'indexer les champs d'un document imbriqué.

## Peu de collections, ou beaucoup ? ##
Les collections n'imposant aucun schéma, il est tout à fait possible de construire un système basé sur une seule collection et un amas de documents. Dans mon expérience, la plupart des systèmes MongoDB sont organisés de manière semblable aux systèmes relationnels. Autrement dit, ce qui serait une table dans une base relationnelle sera probablement une collection dans MongoDB ; l'exception de taille étant les tables n-n.

Pour pimenter les choses, prenons les documents imbriqués. L'exemple habituel est un blog. faut-il une collection de `posts` et une collection de `comments`, ou est-ce que chaque `post` devrait avoir son ensemble de `comments` imbriqué ? Sans tenir compte de la limite de 16 Mo pour la taille des documents (*Hamlet* pèse moins de 200 ko, votre blog ne fait pas le poids !), la plupart des développeurs préfèrent séparer les choses. C'est plus propre, plus clair.

Il n'y a pas de règle stricte (oui, bon, sauf les 16&nbsp;Mo)&nbsp;: essayez plusieurs approches pour vous rendre compte de ce qui marche et de ce qui marche moins.

## Dans ce chapitre ##
Notre but dans ce chapitre était de des fournir conseils, des pistes, pour modéliser ses données dans MongoDB. La modélisation dans un système orienté document est légèrement différente de celle d'un système relationnel. Il y a plus de flexibilité et une contrainte, mais pour un nouveau système, ça marche plutôt bien. La seule chance d'échouer est de ne pas essayer.

# Chapitre 5 - Quand utiliser MongoDB #
Vous devriez commencer à avoir une idée du rôle que pourrait avoir Mongo dans votre système existant. Il y a tellement de technologies de stockage concurrentes qu'il est facile de se perdre dans tous ces choix.

Pour moi, l'essentiel n'est pas MongoDB&nbsp;: c'est de ne plus devoir compter sur une seule solution pour ses données. Bien sûr, une solution unique a des avantages évidents ; pour la plupart des projets, c'est même le meilleur choix. L'idée n'est pas de *devoir* utiliser des technologies différentes, mais de *pouvoir* le faire. Vous êtes le mieux placé pour savoir si le bénéfice d'une solution supplémentaire en justifie les coûts.

Cela étant, j'espère qu'avec tout ce que nous avons vu, vous envisagez Mongo comme une solution générale. On a dit quelques fois que les BDD orientées document avaient beaucoup en commun avec les bases relationnelles. Arrêtons de tourner autour du pot&nbsp;: Mongo peut être une alternative aux bases relationnelles. Là où Lucene fournit l'indexation textuelle complète à une base relationnelle, là où Redis fournit une stockage clé-valeur persistant, Mongo est un dépôt central pour vos données.

Notez que je n'ai pas dit que Mongo pouvait *remplacer* les BDD relationnelles, mais pouvait être une *alternative*. C'est un outil qui peut faire ce que beaucoup d'autres outils font. Mongo fait certaines tâches mieux, d'autres moins bien. Creusons la question un peu plus.

## Schema-less ##
Un bénéfice souvent mentionné des bases orientées document est qu'elles sont *schema-less*, c'est-à-dire sans modèle. Elles sont donc bien plus flexibles que les bases traditionnelles. Je trouve aussi que l'absence de schéma est une propriété intéressante, mais pas pour les raisons habituellement avancées.

Les gens parlent de schema-less comme si vous alliez vous mettre à stocker des données complètement chaotiques. Il y a bien des domaines et des jeux de données très compliqués à modéliser dans des BDD relationnelles, mais ce sont des cas extrèmes. Vos données seront souvent très structurées, et s'il peut être pratique d'avoir une incohérence ici ou là quand on ajoute des fonctionnalités par exemple, ce n'est rien qu'une colonne à *null* ne pourraît résoudre aussi bien.

Pour moi, le vrai atout du schema-less, c'est l'absence de configuration et une meilleure compatibilité avec la programmation orientée objet. C'est particulièrement vrai pour les langages statiques. J'ai utilisé MongoDB avec C# et Ruby et la différence est frappante. Ruby est très dynamique et ses implémentations ActiveRecord limitent déjà grandement la friction entre objet et relationnel. Ça ne veut pas dire que Mongo n'est pas adapté à Ruby, au contraire. C'est simplement qu'un développeur Ruby verrait Mongo comme une simple amélioration. Pour un développeur C# ou Java, il s'agirait d'un changement fondamental dans l'interaction avec les données.

Mettez-vous à la place d'un développeur de driver. Vous voulez sauvegarder un objet? Vous le sérialisez en JSON (techniquement, en BSON, mais c'est équivalent) et l'envoyez à MongoDB. Pas de correspondance à faire entre propriétés ou types. Cette facilité d'utilisation se répercute forcément sur vous, le développeur.

## Écritures ##
Il est un domaine dans lequel MongoDB peut remplir un rôle spécifique&nbsp;: la journalisation. Il y a deux aspects de Mongo qui rendent les écritures très rapides. D'abord, il est possible d'envoyer une commande d'écriture et d'obtenir une réponse immédiate, sans avoir à attendre que l'écriture soit effective. Ensuite, depuis l'introduction de la journalisation dans la version 1.8 et les améliorations faites dans la 2.0, il est possible de contrôler le comportement des écritures en termes de durabilité des données. Ces réglages, en plus de permettre de spécifier combien de serveurs doivent avoir reçu vos données pour qu'une écriture soit considérée comme un succès, peuvent être configurés pour chaque écriture, permettant ainsi un grand degré de contrôle sur la performance de l'écriture et la durabilité des données.


Au-delà de ces facteurs de performance, les données de journalisation sont parmi les jeux de données qui tirent le plus parti des collections sans schéma. Pour fini, Mongo dispose des [collections limitées](http://www.mongodb.org/display/DOCS/Capped+Collections). Jusqu'ici, toutes les collections que nous avons créées implicitement sont des collections normales. On peut créer des collections limitées en utilisation la commande `db.createCollection` et en l'indiquant comme limitée&nbsp;:
	//on limite notre collection à 1 Mo.
	db.createCollection('logs', {capped: true, size: 1048576})

Lorsque notre collection atteint sa limite de 1 Mo, les documents les plus anciens sont automatiquement purgés. La limite peut être appliquée au nombre de documents plutôt qu'à la taille grâce à la commande `max`. Les collections limitées ont des propriétés intéressantes. Ainsi, on peut mettre un document à jour, mais pas augmenter sa taille. L'ordre des insertions est également préservé, de sorte qu'on peut se passer d'un index supplémentaire pour classer par date.

C'est le bon moment pour souligner que, si vous souhaitez savoir si votre écriture a rencontré une erreur (contrairement au comportement par défaut, où l'on demande l'écriture sans la vérifier ensuite), il suffit d'utiliser la commande suivante&nbsp;:
`db.getLastError()`.
La plupart des pilotes encapsulent cette commande dans un *safe write*, par exemple en spécifiant `{:safe => true}` comme deuxième paramètre de `insert`.

## Durabilité ##

Avant la version 1.8, MongoDB n'avait pas de durabilité sur un seul serveur. Un serveur tombé avait de fortes chances d'entraîner une perte de données. La solution a toujours été d'exécuter Mongo dans un contexte multi-serveur (Mongo gère la réplication). L'une des fonctionnalités majeures à être ajoutée à la version 1.8 était la journalisation. Pour l'activer, il faut ajouter une ligne avec `journal=true` au fichier `mongodb.config` que nous avons créé lors de la mise en place de MongoDB (et redémarrer le serveur si on souhaite l'activer immédiatement). En général, on souhaite activer cette fonctionnalité, qui le sera d'ailleurs par défaut dans une future version. Néanmoins, dans certains cas, le meilleur débit obtenu en désactivant la journalisation pourra valoir le risque encouru. C'est particulièrement vrai dans le cas d'applications pour lesquelles la perte de données est acceptable.

La durabilité est évoquée ici car on a beaucoup parlé du manque de durabilité de MongoDB sur un seul serveur. Il y a des chances que vous rencontriez ce genre de résultats dans des recherches Google pendant un moment. Sachez simplement que ces informations ne sont plus à jour.

## Recherche texte complète ##
La recherche complète en mode texte est une fonctionnalité qui, espérons-le, arrivera dans une version future de Mongo. Avec le support des tableaux, une recherche textuelle de base est plutôt facile à mettre en place. Pour quelque chose de plus puissant, il faudra s'appuyer sur une solution comme Lucene/Solr. Bien sûr, cela est vrai pour de nombreuses bases de données relationnelles.

## Transactions ##
MongoDB ne permet pas les transactions. Il existe deux alternatives&nbsp;: l'une est très bien mais avec un usage limité, l'autre est difficile à utiliser mais flexible.

Pour la première, il s'agit de ses nombreuses opérations atomiques. Elles sont géniales, tant qu'elles s'appliquent à votre problème. On a déjà vu certaines des plus simples, telles que `$inc` et `$set`. Il y a aussi des commandes comme `findAndModify` qui peuvent mettre à jour ou effacer un document et le renvoyer de manière atomique.

Pour la seconde, quand les opérations atomiques ne suffisent pas, il faut s'en remettre à un commit en deux temps, qui est aux transactions ce que le déréférencement manuel est aux jointures. Il s'agit d'une solution, indifférente aux méthodes de stockage, réalisée dans le code. Les commits en deux temps sont plutôt répandus dans le monde des DB relationnelles. Le site web de Mongo [a un exemple](http://www.mongodb.org/display/DOCS/two-phase+commit) qui illustre le scénario le plus courant (un transfert de fonds). L'idée globale est de conserver l'état de la transaction au sein du document en train d'être mis à jour et de dérouler les étapes initialisation-en cours-commit/rollback à la main.

MongoDB gère les documents imbriqués et les architectures sans schéma, ce qui rend les commits en deux temps un peu moins pénibles, mais ça reste un processus assez moyen, en particulier quand on le découvre juste.

## Traitement des données ##

Mongo s'appuie sur MapReduce pour la plupart des tâches de traitement des données. Il dispose de fonctionnalités d'[agrégation basique](http://www.mongodb.org/display/DOCS/Aggregation), mais pour des tâches un peu sérieuses, il faudra faire appel à MapReduce. Dans le chapitre suivant, nous nous y intéresserons en détail. Pour l'instant, dites-vous simplement que c'est une manière différent et très puissante (c'est un euphémisme) de procéder à des `group by`. L'une des forces de MapReduce est de pouvoir le paralléliser pour travailler sur d'immenses jeux de données. En revanche, l'implémentation de Mongo s'appuie sur JavaScript, qui n'est pas multithreadé. Concrètement, pour traiter de grandes quantités de données, il vous faudra utiliser autre chose, comme Hadoop. Mais, heureusement, comme les deux systèmes se complètent vraiment très bien, il existe un [adaptateur Mongo pour Hadoop](https://github.com/mongodb/mongo-hadoop).

Évidemment, le traitement parallèle de données n'est pas non plus le point fort des bases relationnelles. L'un des objectifs des versions futures de MongoDB est de rendre plus efficace sa gestion des grands ensembles de données.

## Géolocalisation ##
Une fonctionnalité particulièrement puissante de MongoDB est de gérer les index géospatiaux. Cela permet de stocker les coordonnées x et y dans les documents eux-même, puis de trouver ceux qui sont près de telles ou telles coordonnées (`$near`) ou comprises dans un rectangle ou un cercle autour (`$within`). Cette fonctionnalité est bien plus parlante avec un exemple visuel, donc je vous recommande de faire le [tutoriel géospatial interactif en 5 minutes](http://tutorial.mongly.com/geo/index) si vous souhaitez en savoir plus.

## Outils et maturité ##
Vous connaissez certainement la réponse à cette question, mais gardez en tête que Mongo est évidemment bien plus jeune que la plupart des systèmes de bases de données relationnelles. L'impact de cette immaturité sera plus ou moins important selon ce que vous faites avec, et comment. Néanmoins, une analyse honnête ne peut pas ignorer que Mongo est jeune, et que les outils disponibles autour ne sont pas géniaux (mais, après tout, les outils basés sur certaines BDD relationnelles très mûres ne sont pas fameux non plus !). Par exemple, le manque de support pour les nombres à virgule flottante en base 10 vont, naturellement, être un problème (pas forcément si bloquant que ça) pour les systèmes traitant de l'argent.

D'un autre côté, des pilotes existent pour un très grand nombre de langages, le protocole est moderne et simple, et des développements ont lieu à des vitesses hallucinantes. Mongo est utilisé en production dans suffisamment de sociétés pour ques les préoccupations sur sa maturité, bien que justifiée, disparaissent très rapidement.

## Dans ce chapitre ##
Ce qu'il faut retenir de ce chapitre est que Mongo, dans la plupart des cas, peut tout à fait remplacer des bases de données relationnelles. C'est beaucoup plus simple et clair, plus rapide, et impose moins de restrictions aux développeurs d'applications. Le manque de transactions est une inquiétude légimite et sérieuse. Néanmoins, quand les gens demandent "où se situe Mongo dans le paysage des nouvelles solutions de stockage ?", la réponse est simple&nbsp;: "en plein milieu".

# Chapter 6 - MapReduce #
MapReduce est une approche du traitement de données qui a deux gros avantages sur les solutions traditionnelles. D'abord, et c'est la raison pour laquelle elle a été développée, les performances sont bien supérieures. En théorie, MapReduce peut être parallélisé, ce qui permet de traiter de grands ensembles de données sur de nombreux cœurs/processeurs/machines. Comme on vient de le voir, cela n'est pas pour l'instant accessible à MongoDB. Le deuxième avantage de MapReduce est que l'on écrit du vrai code pour faire le traitement. Comparé à ce qu'il est possible de faire avec SQL, le code MapReduce est infiniment plus riche et permet de faire beaucoup plus de choses avant de devoir se tourner vers une solution plus spécialisée.

MapReduce est une approche qui a gagné en popularité, et qui peut être utilisée quasiment partout&nbsp;: il existe des implémentations en C#, Ruby, Java, Python, etc. Je tiens à préciser qu'au début, cela vous paraitra très différent et compliqué. Ne vous braquez pas, prenez votre temps, jouez avec. Cela vaut le coup d'être compris, que vous utilisiez MongoDB ou non.

## Un mélange de théorie et de pratique ##
MapReduce est un processus en deux étapes. D'abord, on "map" (associe), et ensuite on "reduce" (réduit). Le processus de "mapping" transforme les documents en entrée en une série de paires clé=>valeur (la clé comme la valeur peuvent être complexes). Ensuite, les paires clé/valeur sont groupées par clé, rassemblant ainsi les valeurs pour chaque clé dans un tableau. Le "reduce" prend une clé, la série de valeurs pour cette clé, et produit le résultat final. Nous allons nous intéresser à chaque étape et à leur sortie.

L'exemple que nous allons utiliser est le compte-rendu du nombre de consultations, par jour, d'une ressource (par exemple, une page web). Il s'agit-là du *"hello world"* de MapReduce. Pour cet exemple, nous utiliserons une collection de `hits` (visites) avec deux champs&nbsp;: `resource` et `date`. Nous souhaitons obtenir un classement par `resource`, `year`, `month`, `day` et `count`.

Ainsi, à partir des données suivantes dans `hits`&nbsp;:

	resource     date
	index        Jan 20 2010 4:30
	index        Jan 20 2010 5:30
	about        Jan 20 2010 6:00
	index        Jan 20 2010 7:00
	about        Jan 21 2010 8:00
	about        Jan 21 2010 8:30
	index        Jan 21 2010 8:30
	about        Jan 21 2010 9:00
	index        Jan 21 2010 9:30
	index        Jan 22 2010 5:00

Nous voulons obtenir&nbsp;:

	resource  year   month   day   count
	index     2010   1       20    3
	about     2010   1       20    1
	about     2010   1       21    3
	index     2010   1       21    2
	index     2010   1       22    1

L'avantage de ce type d'approche pour l'analyse de données et que, en classant le document de sortie, les rapports sont rapides à générer et le volume de données reste maîtrisé (au plus, on ajoute un document par jour et par ressource suivie).

Pour l'instant, concentrez-vous sur la compréhension de ce concept. À la fin du chapitre, vous trouverez des données et du code d'exemple pour essayer vous-même.

Pour commencer, regardons la fonction "map". Son but est d'émettre une valeur qui puisse être réduite. Elle peut émettre 0 fois ou plus. Dans notre cas, elle émettra toujours une fois (c'est un cas de figure courant). Représentez-vous "map" comme une boucle qui passe dans tous les documents de `hits`. Pour chacun, on veut émettre une clé contenant `resource`, `year`, `month` et `jour`, et une valeur de 1&nbsp;:

	function() {
		var key = {
		    resource: this.resource,
		    year: this.date.getFullYear(),
		    month: this.date.getMonth(),
		    day: this.date.getDate()
		};
		emit(key, {count: 1});
	}

`this` fait référence au document en cours d'inspection. Vous comprendrez peut-être mieux en voyant le résultat de l'étape de "mapping". À partir de nos données, on obtient la sortie complète suivante. Les valeurs de `emit` sont groupées ensemble dans un tableau, par clé.

	{resource: 'index', year: 2010, month: 0, day: 20} => [{count: 1}, {count: 1}, {count:1}]
	{resource: 'about', year: 2010, month: 0, day: 20} => [{count: 1}]
	{resource: 'about', year: 2010, month: 0, day: 21} => [{count: 1}, {count: 1}, {count:1}]
	{resource: 'index', year: 2010, month: 0, day: 21} => [{count: 1}, {count: 1}]
	{resource: 'index', year: 2010, month: 0, day: 22} => [{count: 1}]


Comprendre cette étape intermédiaire est essentielle pour comprendre MapReduce. Les développeurs .NET et Java peuvent se les représenter comme étant du type `IDictionary<object, IList<object>>` (.NET) ou `HashMap<Object, ArrayList>` (Java).

Rendons notre fonction "map" un peu plus tordue&nbsp;:

	function() {
		var key = {resource: this.resource, year: this.date.getFullYear(), month: this.date.getMonth(), day: this.date.getDate()};
		if (this.resource == 'index' && this.date.getHours() == 4) {
			emit(key, {count: 5});
		} else {
			emit(key, {count: 1});
		}
	}

Le premier résultat intermédiaire devient alors&nbsp;:

	{resource: 'index', year: 2010, month: 0, day: 20} => [{count: 5}, {count: 1}, {count:1}]

Remarquez que chaque `emit` génère une nouvelle valeur, groupée par clé.

La fonction de réduction prend chaque résultat intermédiaire et produit un résultat final. Dans notre cas&nbsp;:

	function(key, values) {
		var sum = 0;
		values.forEach(function(value) {
			sum += value['count'];
		});
		return {count: sum};
	};

Ce qui donne&nbsp;:

	{resource: 'index', year: 2010, month: 0, day: 20} => {count: 3}
	{resource: 'about', year: 2010, month: 0, day: 20} => {count: 1}
	{resource: 'about', year: 2010, month: 0, day: 21} => {count: 3}
	{resource: 'index', year: 2010, month: 0, day: 21} => {count: 2}
	{resource: 'index', year: 2010, month: 0, day: 22} => {count: 1}

Techniquement, le résultat dans MongoDB est&nbsp;:

	_id: {resource: 'index', year: 2010, month: 0, day: 20}, value: {count: 3}

Nous obtenons le résultat final que l'on cherchait au départ.

Si vous avez été très attentif, vous vous demandez peut-être pourquoi nous n'avons pas utilisé `sum = values.length`, qui est a priori une méthode efficace pour faire la somme de tableaux de "1". Pourtant, cela peut ne pas marcher. "Reduce" peut être appelée plusieurs fois avec seulement une partie des valeurs, ce qui permet de la distribuer sur plusieurs processus ou ordinateurs. Le résultat de plusieurs (au moins deux) fonctions de réduction est donné en entrée à cette même fonction (et ce, de nombreuses fois, dans le cas d'un grand ensemble de données).

Pour revenir à notre exemple, "reduce" peut être appelée une fois avec l'entrée suivante&nbsp;:

	{resource: 'index', year: 2010, month: 0, day: 20} => [{count: 1}, {count: 1}, {count:1}]

ou bien être appelée deux fois, la sortie de l'*étape 1* étant utilisée comme entrée de l'*étape 2*&nbsp;:

	//ÉTAPE 1
	{resource: 'index', year: 2010, month: 0, day: 20} => [{count: 1}, {count: 1}]
	//ÉTAPE 2
	{resource: 'index', year: 2010, month: 0, day: 20} => [{count: 2}, {count: 1}]

Si l'on utilisait `sum = values.length`, la deuxième étape retournerait `{count: 2}`, ce qui est incorrect.

Cela signifie que le structure de la sortie de "reduce" doit être la même que celle de son entrée, et qu'appeler "reduce" plusieurs fois doit retourner le même résultat (une propriété qu'on nomme *idempotence*).

Nous n'allons pas en parler ici, mais sachez qu'il est courant de chaîner les méthodes de réduction dans le cas d'analyses complexes.

## Mise en pratique pure ##
Avec MongoDB, on utilise la commande `mapReduce` sur une collection. `mapReduce` prend une fonction "map", une fonction "reduce", et une directive de sortie. Dans notre *shell*, on peut créer et passer une fonction JavaScript. Depuis la plupart des bibliothèques, il faut fournir une chaîne de caractères contenant les fonctions (ce qui est un peu moche). Mais d'abord, créons notre jeu de données&nbsp;:

	db.hits.insert({resource: 'index', date: new Date(2010, 0, 20, 4, 30)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 20, 5, 30)});
	db.hits.insert({resource: 'about', date: new Date(2010, 0, 20, 6, 0)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 20, 7, 0)});
	db.hits.insert({resource: 'about', date: new Date(2010, 0, 21, 8, 0)});
	db.hits.insert({resource: 'about', date: new Date(2010, 0, 21, 8, 30)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 21, 8, 30)});
	db.hits.insert({resource: 'about', date: new Date(2010, 0, 21, 9, 0)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 21, 9, 30)});
	db.hits.insert({resource: 'index', date: new Date(2010, 0, 22, 5, 0)});

Passons à la création de nos fonctions d'association et de réduction (le *shell* MongoDB accepte les expressions multilignes&nbsp;; vous verrez *...* après avoir appuyé sur Entrée pour signaler que du texte est attendu)&nbsp;:

	var map = function() {
		var key = {resource: this.resource, year: this.date.getFullYear(), month: this.date.getMonth(), day: this.date.getDate()};
		emit(key, {count: 1});
	};

	var reduce = function(key, values) {
		var sum = 0;
		values.forEach(function(value) {
			sum += value['count'];
		});
		return {count: sum};
	};

Passons nos fonctions `map` et `reduce` à la commande `mapReduce` en tapant&nbsp;:

	db.hits.mapReduce(map, reduce, {out: {inline:1}})

Si vous exécutez ce code, vous devriez obtenir le résultat escompté. Donner `inline` comme valeur pour `out` permet d'avoir le résultat de `mapReduce` directement renvoyé au terminal. C'est pour l'instant limité aux résultats qui font 16&nbsp;Mo ou moins. On pourrait à la place écrire `{out: 'hit_stats'}`, et stocker les résultats dans la collection `hit_stats`&nbsp;:

	db.hits.mapReduce(map, reduce, {out: 'hit_stats'});
	db.hit_stats.find();

Cela écrase toute donnée existante dans `hit_stats`. Si l'on écrit `{out: {merge: 'hit_stats'}}`, les clés existantes sont remplacées par les nouvelles valeurs, et les nouvelles clés sont insérées comme nouveaux documents. Enfin, il est possible de rediriger le `out` vers une fonction de réduction, pour traiter les cas les plus avancés (comme faire un upsert).

Le troisième paramètre prend des options supplémentaires. Par exemple, on pourrait filtrer, trier ou limiter les documents que l'on souhaite analyser. On pourrait également fournir une méthode `finalize` pour appliquer les résultats après l'étape de réduction.

## Dans ce chapitre ##
C'est le premier chapitre dans lequel nous avons traité quelque chose de vraiment différent. Si vous vous sentez un peu perdu, n'oubliez pas que vous pouvez toujours utiliser les autres [fonctionnalités d'agrégation](http://www.mongodb.org/display/DOCS/Aggregation) de MongoDB pour les cas les plus simples. Malgré tout, MapReduce reste l'une des fonctionnalités les plus intéressantes de Mongo. Le point essentiel pour écrire vos propres fonctions "map" et "reduce" est de visualiser et de comprendre comment vos données seront en sortant de l'étape d'association et en entrant dans l'étape de réduction.

# Chapitre 7 - Performance et Outils #
Dans ce dernier chapitre, nous allons discuter quelques points sur la performance ainsi que sur les outils disponibles pour les développeurs MongoDB. Nous n'allons pas rentrer dans les détails, mais nous allons parler des aspects les plus importants.

## Index ##
Au tout début du livre, nous avons vu la collection spéciale `system.indexes` qui contient des informations sur tous les index dans notre base de données. Les index dans MongoDB fonctionnent comme dans les bases relationnelles&nbsp;: ils permettent d'accélérer la recherche et le tri. Ils sont créés via `ensureIndex`&nbsp;:

	// où "name" est le nom du champ
	db.unicorns.ensureIndex({name: 1});

Ils sont détruits via `dropIndex`&nbsp;:

	db.unicorns.dropIndex({name: 1});

Un index unique peut être créé en fournissant un second paramètre et en mettant `unique` à `true`&nbsp;:

	db.unicorns.ensureIndex({name: 1}, {unique: true});

Les index peuvent être créés sur des champs imbriqués (là encore, en utilisant le .) et sur les champs tableau. On peut aussi créer des index composés&nbsp;:

	db.unicorns.ensureIndex({name: 1, vampires: -1});

L'ordre de l'index (1 pour ascendant, -1 pour descendant) n'a pas d'importance pour un index à une seule clé, mais peut avoir un impact pour les index composés si l'on utilise un tri ou un intervalle.

La [page sur les index](http://www.mongodb.org/display/DOCS/Indexes) contient de plus amples informations.

## Explain ##
Pour savoir si une requête utilise un index, on peut utiliser la méthode `explain` sur un curseur&nbsp;:

	db.unicorns.find().explain()

La sortie nous informe que c'est un `BasicCursor` qui a été utilisé (c'est-à-dire, pas indexé), que 12 objets ont été scannés, le temps que cela a pris, quel index a été utilisé si c'est le cas, et d'autres informations utiles.

Si l'on change la requête pour qu'elle utilise un index, on verra qu'un `BtreeCursor` a été utilisé, ainsi que l'index qui a été utilisé pour répondre à la requête.

	db.unicorns.find({name: 'Pilot'}).explain()

## Écriture sans vérification ##
Nous avons vu précédemment que, par défaut, les écritures dans MongoDB sont faites sans vérification postérieure. Cela conduit à de nets gains de performance, mais présente le risque d'une perte de données lors d'un crash. Un des effets de bord de ce fonctionnement est qu'aucune erreur n'est renvoyée lorsqu'un `insert` ou un `update` ne respecte pas une contrainte d'unicité. Pour savoir qu'une écriture a échoué, il faut appeler `db.getLastError()` après un `insert`. Beaucoup de pilotes abstraient cette étape et proposent une écriture *sûre*, souvent grâce à un paramètre additionnel.

Malheureusement, le *shell* fait automatiquement des insertions sûres, donc il n'est pas facile de voir ce comportement en action.

## Le sharding ##
MongoDB supporte le *sharding* automatique. Le *sharding* est une technique d'extensibilité qui répartit les données sur plusieurs serveurs. Pour prendre un exemple simpliste, mettre sur le serveur&nbsp;1 les données des utilisateurs dont le nom commence par A-M, et le reste sur le serveur&nbsp;2. Heureusement, les capacités de *sharding* de MongoDB sont bien supérieures. Ce livre n'a pas vocation à traiter en détails du *sharding*, qui est un sujet complexe. Gardez simplement en mémoire que cela existe et que vous pourriez l'utiliser, si vos besoins dépassent un seul serveur.

## Réplication ##
La réplication dans MongoDB fonctionne comme pour les bases relationnelles. Les écritures sont envoyées à un seul serveur, le maître, qui se synchronise avec un ou plusieurs autres serveurs, les esclaves. Il est possible de contrôler si la lecture peut se produire sur les escalves ou pas, ce qui peut permettre de distribuer la charge, au risque de lire des données légèrement périmées. Si un serveur maître tombe, un esclave peut devenir le nouveau maître. Là encore, ce livre n'a pas vocation à couvrir en détails la réplication dans MongoDB.

Si la réplication peut améliorer la performance (en distribuant les lectures), son but principal est d'améliorer la fiabilité. Il est courant de combiner le *sharding* et la réplication. Ainsi, chaque *shard* (tesson) pourrait se composer d'un maître et d'un esclave. Techniquement, il faut aussi un arbitre pour trancher si deux esclaves tentent de devenir maître, mais un arbitre ne requiert que très peu de ressources et peut être utilisé pour plusieurs tessons.

## Statistiques ##
Des statistiques sont disponibles en tapant `db.stats()`. En majeure partie, il s'agit d'informations sur la taille de la base. On peut obtenir des statistiques sur une collection, par exemple `unicorns`, en tapant `db.unicorns.stats()`. Là aussi, il s'agit principalement d'informations sur la taille de la collection.

## Interfaces web ##
Lors du démarrage de MongoDB, des informations étaient affichées, et en particulier un lien vers l'outil d'administration web (si vous scrollez votre terminal ou fenêtre de commande jusqu'au moment où vous avez démarré `mongod`, vous pourrez peut-être le voir). Vous pouvez y accéder en ouvrant votre navigateur et en vous rendant à l'adresse <http://localhost:28017/>. Pour l'utiliser au mieux, il vous faudra ajouter `rest=true` dans la configuration et redémarrer `mongod`. L'interface web fournit beaucoup d'informations sur l'état actuel du serveur.

## Profileur ##
Le profileur de MongoDB s'active en lançant&nbsp;:

	db.setProfilingLevel(2);

Une fois activé, on peut lancer une commande&nbsp;:

	db.unicorns.find({weight: {$gt: 600}});

Et examiner le profileur&nbsp;:

	db.system.profile.find()

La sortie nous montre ce qui a été lancé et quand, combien de documents ont été scannés, et combien de données ont été renvoyées.

Le profileur peut être désactivé en appelant `setProfileLevel`, mais avec la valeur `0`. On peut aussi utiliser la valeur `1`, pour ne profiler que les requêtes prenant plus de 100 millisecondes, ou ajouter un second paramètre pour spécifier la durée minimale (toujours en millisecondes)&nbsp;:

	//pour profiler tout ce qui prend plus d'une seconde
	db.setProfilingLevel(1, 1000);

## Sauvegarde et restauration ##
Dans le répertoire `bin` de MongoDB se trouve l'exécutable `mongodump`. Si on le lance, il se connecte à localhost et sauvegarde toutes les bases dans le sous-répertoire `dump`. Vous pouvez taper `mongodump --help` pour voir des options supplémentaires. Parmi celles-ci, les plus courantes sont `--db NOM_DE_LA_BASE` pour sauvegarder une base en particulier, ou `--collection NOM_DE_LA_COLLECTION` pour une collection. Il suffit ensuite d'exécuter `mongorestore`, lui aussi situé dans le répertoire `bin`, pour restaurer une sauvegarde précédente. Là aussi, les options `--db` et `--collection` peuvent être utilisées.

Par exemple, pour sauvegarder notre base `learn` dans le répertoire `backup`, il faut lancer la commande suivante. Il s'agit d'une commande indépendante, qui se lance depuis le terminal et pas depuis le *shell* Mongo.

	mongodump --db learn --out backup

Pour restaurer uniquement la collection `unicorns`, il faudrait faire&nbsp;:

	mongorestore --collection unicorns backup/learn/unicorns.bson

Il faut mentionner les exécutables `mongoexport` et `mongoimport` qui peuvent être utilisés pour importer et exporter des données au format JSON ou CSV. Ainsi, on peut obtenir du JSON en faisant&nbsp;:

	mongoexport --db learn -collection unicorns

Et du CSV avec&nbsp;:

	mongoexport --db learn -collection unicorns --csv -fields name,weight,vampires

Attention&nbsp;: `mongoexport` et `mongoimport` ne peuvent pas toujours représenter les données avec précision. Il est impératif de n'utiliser que `mongodump` et `mongorestore` pour des sauvegardes fiables.

## Dans ce chapitre ##
Dans ce chapitre, nous avons traité de différents outils, commandes et détails de performance de Mongo. Nous n'avons pas été exhaustifs mais nous avons vu les plus courants. Dans MongoDB, l'indexation comme la plupart des outils fonctionnent comme leur équivalent des bases relationnelles. La grande différence est qu'ils sont clairs et faciles à utiliser&nbsp;!

# Conclusion #
Vous devriez en savoir assez pour utiliser MongoDB dans un vrai projet. Mongo est bien plus riche que ce que nous avons vu, mais avant d'aller plus loin, vous devriez essayer de mettre en pratique ce que nous avons appris et de vous familiariser avec le pilote que vous allez utiliser. Le [site web de MongoDB](http://www.mongodb.com/) regorge d'informations utiles. Et si vous vous posez des questions, le [groupe officiel des utilisateurs de MongoDB](http://groups.google.com/group/mongodb-user) est l'endroit idéal.

NoSQL n'a pas été créé uniquement pour répondre à un besoin, mais aussi pour essayer de nouvelles approches. C'est une preuve manifeste que notre domaine progresse constamment et que, si l'on ne tente rien, au risque d'échouer parfois, on ne peut pas avancer.

C'est, je crois, un bon principe pour mener sa vie professionnelle.