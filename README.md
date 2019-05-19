# Challenge pour GAC Technology

Explication de ma démarche pour traiter le problème suivant :
*******************************************************************************************
En utilisant un perceptron multicouche, réaliser l'approximation de la fonction suivante : 
y = 2 * cos(x) + 4 sur l'intervalle [0 ; 10]
*******************************************************************************************

Pour traiter ce problème, j'ai choisi de privilégier la méthode au résultat. Il y a deux raisons à cela : 
- La méthode me semble plus importante que le résultat pour cet exercice. De plus, vu la nature de l'ennoncé, il n'y a 
pas de limite à la taille des données, avoir un résultat approchant la perfection semble donc assez facile en augmantant 
la taille des données. 
- Mon code tourne sur mon ordi (CPU), ce qui limite énormément la puissance de calcul. Je ne peux pas me permettre de 
prendre un trop grand volume de données, ni de construire un trop gros réseau de neuronnes. Ainsi, la méthode que j'ai  
suivie a été appliquée sur un nombre relativement faible de données ainsi que des réseaux de neuronnes pas trop gros. 

Pour traiter cet exercice, j'ai utilisé Python via Anaconda (nécessaire pour Tensorflow avec Windows) et Jupyter. 
Le perceptron multicouche à été codé avec Keras. 
Les bases du problème étant posées, je vais donc expliciter ma démarche, qui se divise en plusieurs étapes. 

## Etape 1 : Visualition du problème
Cette première étape est la plus importante. Elle consiste à comprendre et s'approprier le problème en analysant le  
domaine dans lequel il se situe. Dans notre cas, cela à été assez rapide car j'ai simplement tracé la fonction sur 
l'intervalle [0 ; 10]

## Etape 2 : Définition des données
Une fois le problème compris, il faut désormais inspecter les données disponible. Ici, elles ne sont pas explicitement 
données. Pour effectuer une approximation, on a généralement une base de points et on cherche à extrapoler à partir 
de ces derniers. Ainsi, j'ai décidé de prendre 1000 points équitablement répartis sur [0 ; 10] qui me serviront de données 
pour la phase d'apprentissage. De plus, j'ai également pris 1000 points aléatoirement sur [0 ; 10] pour la phase de test. 

## Etape 3 : Création du modèle
Les données étant propres et bien définies, il convient alors de choisir un modèle. Le choix étant imposé, j'ai donc 
implémenté un réseau de neuronnes. Son nombre de couches ou de neuronnes sera défini par la suite, lors de la phase 
de validation. 

## Etape 4 : Validation du modèle
C'est dans cette étape que j'ai favorisé la méthode au résultat. Cette  dernière consiste à trouver les paramètres 
optimaux pour le réseau de neuronnes. En premier lieu, j'ai voulu déterminer le nombre de niveaux cachés à utiliser. 
Un nombre entre 4 et 5 me semble le plus adapté, mais j'ai choisi d'utiliser deux niveaux dans la suite de cette étape 
pour des questions de vitesse d'exécution. 
Ensuite, j'ai été amené à trouver le nombre optimal de neuronnes à utiliser dans les couches. Pour cela, j'ai utilisé  
la MAE comme métrique pour mesurer la performance du modèle. J'ai alors séparé le training set en deux (25% pour la 
validation 75% pour l'apprentissage) et lancé une cross validation en calculant la MAE moyenne sur les partitions. La 
MAE est minimale pour 64 neuronnes. 
J'ai enfin cherché le nombre optimal d'epochs, toujours avec le même principe. Pour cela, j'ai figé le réseau avec 2 
niveaux cachés et 64 units. La meilleure MAE est obtenue pour 92 itération. Au delà, on commence à faire du sur - 
apprentissage.

## Etape 5 : Résultat
J'ai donc pu lancer l'algorithme avec ces paramètres et le tester avec 1000 points choisis au hasard. Pour la forme du 
résultat, j'ai préféré un aspect graphique à un aspect numérique car cela permet de mieux se rendre compte des résultats.
Ces derniers ne sont certes par parfaits (explicable par le choix d'un réseau à deux niveaux), mais on peut tout de même 
voir que l'approximation suit relativement bien la fonction de départ.

## Bonus
Dans le but d'obtenir un meilleur résultat, j'ai tout de même testé un réseau plus gros dont les paramètres ont en revanche 
été choisis arbitrairement : 4 niveaux cachés (respectivement 512, 512, 256 et 256 neuronnes), 10 000 points choisis pour 
les données, 200 epochs. Sans surprise, les résultats sont bien meilleurs et l'approximation embrasse très bien la vraie 
courbe.
