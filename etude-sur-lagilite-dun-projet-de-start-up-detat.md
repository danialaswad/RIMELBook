# Etude sur l'agilité d'un projet de start-up d'état

## Auteurs

Nous sommes quatre étudiants en dernière année à Polytech Nice-Sophia Antipolis, spécialisés en Architecture Logicielle.

* Alexandre Bar &lt;alexandre.bar83@gmail.com&gt;
* Gaspard Lacroix &lt;gaspard.lacroix@etu.unice.fr&gt;
* Anthonny Giroud &lt;giroud.anthonny@gmail.com&gt;
* Adrien Dengreville &lt;didienv2@gmail.com&gt;

## I. Contexte de recherche

Cette étude à été réalisé dans le cadre du module RIMEL. Nous avons décidé de travailler sur la rétro ingénierie d'un projet agile car de nos jours, tous les projets en entreprise tendent à utiliser cette méthodologie, qui est devenu incontournable. Il se trouve que nous utilisons tous plus ou moins les principes agiles en entreprise \(stage ou alternance\) bien que nos projets ne s'y prêtent pas tout le temps.

Par exemple, l'un d'entre nous travaille sur la réécriture d'un projet déjà existant, afin d'adopter une architecture plus adaptée au problème. Aussi, pour l'un d'entre nous, les lignes directrices du projet sont spécifiés par des autorités \(CNDA - Centre National de Dépot et d'Agrément\), ce qui oblige à respecter de nombreux cas de tests \(+1000\) avant de faire une release, ce qui empêche de faire un MVP, de le livrer et d'itérer autours pour apporter des améliorations aux utilisateurs.

Nous avons donc voulu voir comment fonctionnait un projet agile \(en l'occurence PIX : [https://github.com/betagouv/pix](https://github.com/betagouv/pix)\) qui se revendique comme tel, et qui est financé par l'état, ce qui devrait entraîner un certain niveau d'exigence et de perfection.

## II. Observations et question générale

Malgré le fait que ce projet soit financé par l'état comme startup suivant les principes de l'agilité. Nous avons assez rapidement repéré des anomalies, en effets, certains principes de cette méthodologies ne sont pas toujours respectés. Par exemple...

Nous avons donc orienté notre étude sur la question suivante:

_L'agilité d'une start-up d'état : Réalité ou illusion ?_

Pour affirmer cela, nous aimerions avoir un indicateur d'agilité, nous permettant de quantifier l'agilité d'un projet. Néanmoins, en commençant le projet, nous ne savions pas quoi mesurer ni comment regrouper toutes les mesures.

## III. Rassemblement d'informations

### A - Recherche d'indicateurs

Nous avons donc commencé par regrouper un certains nombre d'indicateurs ressorties de brainstormings. Deux catégories d'indicateurs sont ressorties:

* Les indicateurs humains

  * Stand-up Meeting, Sprint Planning, Sprint Review... \(Cérémonies agiles\)
  * Durée des sprints
  * Code review

* Les indicateurs techniques

  * Couverture de test
  * Ticketing
  * Erreurs de build
  * Dette technique
  * Commits \(Formattage, langue etc\)
  * Releases ...

Cependant, après avoir contacté l'équipe PIX, nous n'avons pas pu avoir accès à certains de ces indicateurs, comme par exemple leur outil de ticketing \(Jira\) pour des raisons de confidentialité. En effet, cet outil permet de mettre en exergue la quantité et les conditions de travail, ce qui peut poser des problèmes quand on est une start-up financé par l'état. Nous n'avons pas non plus pu en savoir beaucoup plus sur leur cérémonies agiles. Nous avons donc du nous concentrer majoritairement sur des indicateurs techniques issus de ce que nous avions, à savoir le repository git.

### B - Collecte d'informations

Avant d'attaquer l'étude des indicateurs, nous avons voulu situer chronologiquement le projet, afin de faire la correspondance entre certains événements et l'évolutions des indicateurs. En voici la timeline:

![](/assets/timeline.png)

Nous nous sommes donc concentrés sur les indicateurs suivants:

* #### Couverture de test

  * Outil : Coveralls

  * Résultat:

  Nous avons observé que la couverture de code est constante depuis le lancement de la première beta à 95%, à savoir un très bon chiffre. Néanmoins,  petit bémol, on observe avant le lancement de cette beta que la couverture n'était que d'environ 80%, ce qui est assez insuffisant.

  On peut aussi se poser la question de savoir si ils n'ont pas boosté leur couverture de test en appelant des méthodes qui ne sont pas vraiment testés dans le détail afin de faire bonne figure vu le nombre très important d'utilisateurs pendant cette beta. Néanmoins en étudiant certains de leurs tests \(de manière aléatoire et non exhaustive\), nous n'avons jamais rencontré de cas semblables.

* ![](/assets/coverage.png)

* #### Commits

  * Outil : [RepoDriller](http://repodriller.org/ "RepoDriller")
  * Résultat: Nous avons étudié les commits sur 2 Axes : La **langue** et la **forme**

  **La langue:**  
  Nous avons très vite repéré que certains commits étaient en anglais, et d'autres en français. C'est une des premières remarques que nous avons faites en analysant leur projet. Le problème étant qu'il est compliqué d'automatiser la détection d'une langue dans un script RepoDriller. Par manque de temps, nous avons donc étudié à la main un échantillon aléatoire de 100 commits récupérés par RepoDriller. En voici le résultat par langue:  
  ![](/assets/import.png)  
  On voit donc que même si la langue principale est le français, l'anglais est très présent, nous avons donc cherché à comprendre pourquoi certains commits étaient en anglais et en allant dans le détail, nous avons remarqué un certain type de commits que nous avons appelé les commits "automatisés".  
  En effet, dans les IDE les plus récents, quand on réalise des actions nécessitant un commit \(Merge, Release etc\), l'IDE prend la liberté de créer lui même un message résumant l'action que l'on vient de faire. Par exemple :

  ![](/assets/commit.png)

  Nous avons donc revu les mêmes commits en retirant ces commits automatisés et voici le résultat sur les 88 commits restant:

  ![](/assets/88com.png)

  Il restait donc des commits issus d’êtres humains étant rédigés en anglais. Nous avons donc voulu voir l'implication des membres dans cette incohérence en prenant un échantillon de commits aléatoires des contributeurs majoritaires. En voici le résultat:

  ![](/assets/contrib.png)

  On voit donc que globalement la répartition des commits anglais est bien répartie sur chacun et non pas sur un seul contributeur étranger comme nous le pensions avant de récupérer ces chiffres.

  **La forme:**

  Nous avons ensuite étudié la forme des messages de commits. Dans le forme donc compris les tags, le message et la tache liée. On dénombre 5 tags dans leur projet:

  * \[RELEASE\] - Tag présent à chaque commit de release

  * \[FEATURE\] - Tag Signifiant que le commit correspond à l'avancé d'une feature fonctionnelle

  * \[BUGFIX\] - Commit de débug

  * \[CLEANUP\] - Commit de nettoyage, réduction de la dette technique, refactor

  * \[TECH\] - Commit correspondant à une avancé purement technique \(Upgrade d'un composant ...\)

  Après avoir remarqué une organisation assez importante en terme de tags, nous avons voulu voir si cette organisation était toujours respectée. Nous avons donc étudié les commits du projet avec RepoDriller avec pour commit respectant une forme correct un commit ayant les critères suivants:

  * Etre rattaché à une tache

  * Comporter un des 5 tags dénombrés ci-dessus

  Voici le résultat: \(En retirant les commits Automatisés qui n'ont pas de taches associées dans tout les cas\)

  ![](/assets/format.png)

  La majorité des commits sont donc bien formatés. Nous avons donc cherché à comprendre ce qui poussait l'équipe à ne pas respecter les critères d'un commit au bon format. On a pu observer que pour la majorité de ces commits, on est sur des petits correctifs très mineurs pour lesquels il n'y a pas de taches associés et où ils n'ont même pas pris la peine d'ajouter un tag comme on peut le voir sur les commits ci-dessous:

  ![](/assets/commit2)![](/assets/commit3import.png)

  C'est une des limites pour nous de l'agilité. En effet, il faudrait que chaque commit soit associé à une tache, mais quand créer la tache prends plus de temps que de la réaliser, on peut se poser la question de l’intérêt de la créer.

* #### Erreurs de build

  * Outil : [CircleCI](https://circleci.com/ "CircleCI")
  * Résultat : L'un des principes de bases de l'agilité est de livrer de la valeur de façon continue et sans régression. CircleCI nous permet de voir sur chacun des commits, si une erreur de build \(test non passé, erreur de compil etc\). L’intérêt ici est de voir si il est fréquent d'avoir une régression sur un commit chez pix et si ce problème est réglé rapidement. Voici donc la proportion de builds avec erreurs.
    ![](/assets/buildpassed)
    On voit donc que la proportion d'erreurs de builds sont très faibles. On peut donc déjà imaginer que les erreurs de builds ne restent à priori pas sur de nombreux commits et qu'ils sont rapidement fixés en terme de commits. Nous avons cependant voulu savoir combien de temps restait une erreur de build en moyenne. Nous avons obtenu une moyenne de moins d'un jour.
* #### Dette technique

  * Outil : [CodeClimate](https://codeclimate.com/ "CodeClimate")
  * Résultat:
* #### Releases

  * Outil: [RepoDriller](http://repodriller.org/ "RepoDriller") 
  * Résultat:

/_/Comment on a rassemblé, ce qu'on a rassemblé_

## IV. Hypothèses et expériences

Nous avons donc voulu, à partir des critères d'agilités que nous avons déterminés dans la partie précédente, obtenir un indice d'agilité permettant de dire à quel point un projet est agile.

Nous voulions donc avoir un indice allant de 1 à 100. Pour cela, nous avons ramené chacun de nos critères d'agilité en une valeur allant de 1 à 100 et avons donné des coefficients à chacun d'entre eux en fonction de leur importance pour obtenir une moyenne étant notre indice. Voici le détail:

| Critère d'agilité | Coefficient | Méthode de calcul |
| :--- | :--- | :--- |
| % Commit bien formaté | 4 | Si tag et rattaché à une tache |
| % Commit dans la langue principale | 1 | La langue principale est la langue la + représentée |
| % Couverture de test moyen | 4 | Si &gt; 95% on passe à 100% |
| % Build passe | 4 | Sur chaque commit |
| Dette technique | 3 | 100 - Nombre de jours \(&gt; 0\) |
| % Pertinance des tests | 5 | Estimé par l'architecte / Tech lead |
| Outillage | 6 | On gagne des % par outil:                        - Couverture de test \(20%\)                     - CircleCI ou autre \(20%\)                         - Dette Technique \(20%\)                          - Ticketage  \(40%\) |
| Release | ? | ? |

## V. Analyse des résultats et conclusion

_À remplir._

//On ne peut pas forcément respecter a 100% scrum

//Pourquoi on ne peut pas faire un indicateur sur les releases \(Si c'est trop fréquent, fix, agile mais pas bien testé\)

## VI. Références

_À remplir._

