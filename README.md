# Exercice WeCount : estimation de l'impact carbone d'une entreprise

## Contexte

L'objectif est de développer des fonctions d'API permettant de mettre en oeuvre un bilan carbone simplifié d'entreprise.

Pour cela on considère une entreprise avec trois catégories d'émission :

- Les déplacements domicile-travail
- L'énergie des bâtiments
- Les achats informatiques

### Données d'entrée

Une **catégorie** `data/categorie.json` est défini par les caractéristiques suivantes :

- `id` (int) : un index unique identifiant la catégorie
- `nom` (str) : le nom du la catégorie
- `activityIds` (List[int]) : la liste des identifiants uniques des zonesactivités constituant la catégorie


Les catégories sont découpées en **activités** `data/activite.json`. Les caractéristiques des activités sont les suivantes :

- `id` (int) : un index unique identifiant l'activités
- `nom` (str) : le nom de l'activité
- `donneesactivites` (List[Dict[int, float]]) : liste des éléments de données d'activités contenant leur identifiant unique ainsi que leurs inputs (dont l'unité est définie dans le facteur d'émission). Cette liste se présente sous la forme `[{id: 0, quantite: 20, quantite2: 5000}, ...]` et les quantités sont par la suite utilisées pour calculer les impacts de chaque élément de données d'une activité.

Les **facteurs d'émissions** `data/facteur_emissions.json` contiennent les impacts carbone unitaires de différentes actions/flux. Les champs du facteur d'émission sont les suivants :

- `id` (int) : un index unique identifiant le produit
- `nom` (str) : le nom du facteur
- `unite` (str) : l'unité du définition de l'action ou du flux
- `unite2` (str) : si pertinent, la deuxième unité du définition de l'action ou du flux
- `impactUnitaireRechauffementClimatique` (Dict[str, float]) : impact carbone unitaire en kgCO2e/unité ou en kgCO2e/unité.unité2 du facteur d'émission et cet impact unitaire est par la suite multiplié par les quantités des donnes activités présents dans les activités pour évaluer l'impact carbone.


## Comment démarrer

Cloner le dépôt afin de récupérer les données du projet :

- `data/categorie.json`
- `data/activite.json`
- `data/facteur_emissions.json`

## Partie 1 de l'exercice 

L'objectif est de créer des fonctions d'API RESTful retournant les informations demandées.

Le langage de programmation doit être du javascript/typescript. Le choix des outils, framework, bibliothèques utilisées pour vous aider dans l'implémentation est libre. 

### Calcul de l'impact carbone d'un bâtiment

Implémenter une fonction d'API calculant l'impact sur le réchauffement climatique de l'entreprise à partir des instructions de calculs suivantes 

#### Calcul d'impact d'une donnée d'activité

L'impact carbone
<a href="https://render.githubusercontent.com/render/math?math=I" target="_blank"><img src="https://render.githubusercontent.com/render/math?math=I" title="I"/></a>
 d'une donnée d'activité donnée est calculé à partir des impact unitaire
<a href="https://render.githubusercontent.com/render/math?math=I_U" target="_blank"><img src="https://render.githubusercontent.com/render/math?math=I_U" title="I_U"/></a>
du facteur des émissions et des quantités
<a href="https://render.githubusercontent.com/render/math?math=Q_j" target="_blank"><img src="https://render.githubusercontent.com/render/math?math=Q_j" title="Q_j"/></a>
présente dans l'activité {j}.

<a href="https://render.githubusercontent.com/render/math?math=I_{j} = I_{U} \times Q_{j} \times Q2_{j}" target="_blank"><img src="https://render.githubusercontent.com/render/math?math=I_{j} = I_{U} \times Q_{j} \times Q2_{j}" title="I_{j} = I_{U} \times Q_{j} \times Q2_{j}"/></a>

##### Cas particulier
Pour l'activité "Ordinateur", la quantité 2 est un amortissement, le calcul est alors le suivant :

<a href="https://render.githubusercontent.com/render/math?math=I_{j} = \frac{I_{U}\times Q_{j}}{Q2_{j}}" target="_blank"><img src="https://render.githubusercontent.com/render/math?math=I_{j} = \frac{I_{U} \times Q_{j}}{Q2_{j}}" title="I_{j} = \frac{I_{U} \times Q_{j}}{Q2_{j}}"/></a>

#### Calcul d'impact d'une activité

L'impact carbone sur d'une activité est la somme des impacts de ses données d'activités.

#### Calcul d'impact d'une catégorie

L'impact carbone d'une catégorie est la somme des impacts de ses activités.

#### Calcul d'impact de l'entreprise

L'impact carbone de l'entreprise est la somme des impacts de l'entreprise.

### Questions BONUS

1. Quel serait l'outil que vous utiliseriez pour documenter l'API
2. Ecrire un fichier de configuration Docker pour déployer cette API
3. Créer une mini app en react (site web) permettant de changer les quantités des données d'activités et de visualiser les résultats.


## Ce qu'on attend de vous

- Ce test sert de base à une discussion, les méthodes employées sont plus importantes que le résultat.
- En cas de questions, n'hésitez pas à envoyer un message pour demander des précisions ou des explications.
