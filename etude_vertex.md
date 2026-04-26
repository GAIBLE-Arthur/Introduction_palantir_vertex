# Cas d’utilisation de Palantir Vertex : utilisation des

graphes de relation pour traquer les communications entre entités suspectes.

## Cas d’usage et prompt :

Ce cas d’usage s’intéresse à la rapidité de Palantir Foundry pour effectuer des graphes de relations entre des entités. Nous partons d’un cas simple, différentes transactions de différents montants, des

communications et des entités suspectes. Le cas est généré par IA (Gemini 3) et les données sont aléatoires.

Prompt :

*Rôle : Tu es un ingénieur Solutions chez Palantir, expert en déploiement de l'Ontologie et de Vertex pour la lutte contre la criminalité organisée.*

*Objectif : Créer un Use Case complet pour traquer un réseau criminel (blanchiment d'argent et logistique illicite) via Palantir Vertex.*

*Livrables attendus :*

*Génération de données (Python/Colab) : Fournis un script Python complet pour générer 4 fichiers CSV réalistes et corrélés :*

*Entities.csv (Individus)*

*Financial_Transactions.csv (Virements)*

*Logistics_Events.csv (Mouvements de conteneurs)*

*Communications.csv (Métadonnées d'appels et messages).*

![placeholder](https://markdowntoword.io/placeholder.png" />		![placeholder](https://markdowntoword.io/placeholder.png)

*Data cleaning dans le pipeline*

Le lien entre le pipeline de données et le reste de la plateforme permet de créer des objets ontologiques (*objects*) et les liens entre objets (*links*) directement dans le pipeline.

*Rappel : l’ontologie permet de définir les différents objets utilisés non comme des tables, mais des clés uniques ayant des propriétés (exemple : Chaise possède 1 dossier, 2 accoudoirs, 4 pieds) permettant de les intégrer directement dans les logiques métier.*

*Les liens entre objets ne sont pas de simples jointures, mais une manière de modéliser le réel (dans notre cas : chaque « entité » passe plusieurs transactions mais chaque transaction est unique par entité)*

![placeholder](https://markdowntoword.io/placeholder.png)

*Les objets sont ajoutés dans l’ontologie et les liens réalisés entre eux*

Note : le nœud central du graphe est l’entité (entities) lié aux autres éléments. On note que les doubles liens (en haut) correspondent aux flux d’appels entrant (id_caller) et entrants (id_receiver).

# Utilisation de Vertex pour définir les relations entre les entités

Vertex permet de créer des graphes de relation entre les entités pour effectuer des liens. Dans notre cas, nous cherchons à identifier les transactions financières et communications entre entités pour définir des cibles de recherche.

Pour ne pas sélectionner toutes les entités, nous devons faire un premier filtre :

![placeholder](https://markdowntoword.io/placeholder.png)

*Seules les entités avec un risque supérieur à 40% sont mises dans le graphe*

*![placeholder](https://markdowntoword.io/placeholder.png)*

*Graphe circulaire des entités*

Pour trier de manière plus efficace, on ajoute ici les transactions financières supérieures à 8000 euros

![placeholder](https://markdowntoword.io/placeholder.png)

![placeholder](https://markdowntoword.io/placeholder.png)

*Transactions financières <8000 euros liées aux entités*

En croisant les relations financières entre entités, nous pouvons obtenir une constellation de transactions à surveiller :

![placeholder](https://markdowntoword.io/placeholder.png)

*Le graphique permet d’isoler les nœuds suspects via les transactions financières*

*![placeholder](https://markdowntoword.io/placeholder.png)*

*Focus : un noeud du graphe de relations*

Pour finir, nous devons établir les communications établies entre entités, à propos de transactions financières. Pour procéder, il suffit de croiser les liens ontologiques entité appelante <> communication <> entités receveuse d’appels

Le graphe final est de la forme suivante, établissant des relations entre les entités suspectes :

![placeholder](https://markdowntoword.io/placeholder.png)

## Conclusion :

Utilisé pour l’analyse multiforme de données, Palantir Foundry s’adapte à une multitude d’usages permettant de modéliser rapidement des outils permettant de se concentrer sur l’aspect métier (via l’ontologie).

L’utilisation de Vertex permet de voir des liens directement dans des cartes visuelles, permettant de gagner du temps sur l’analyse ligne par ligne, les jointures, ou bien les représentations graphiques.