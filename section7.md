# Section 7

Le codage de source vise à améliorer la représentation des données en
réduisant leur redondance tout en préservant leur contenu informatif.
Cette amélioration est essentielle pour minimiser l'utilisation des
ressources de communication, telles que la largeur de bande et
l'énergie, tout en garantissant une transmission efficace et fiable.
L'objectif principal du codage de source est d'atteindre une compression
maximale des données tout en respectant les limites théoriques établies
par l'entropie de Shannon.

Le codage de source est une technique essentielle pour réduire les
besoins en ressources tout en maintenant l'intégrité des données.

Les critères de performance clés du codage de source incluent la
longueur moyenne des codes, qui doit être proche de l'entropie de la
source, ainsi que la variance des longueurs de code, qui reflète la
régularité des représentations. Ces métriques permettent d'évaluer
l'efficacité d'un algorithme de codage et son adaptabilité aux
caractéristiques statistiques des données, garantissant ainsi une
transmission améliorée dans des systèmes de communication modernes.

## Types de sources

En télécommunications, une source génère des données qui doivent être
transmises ou stockées. Ces sources peuvent être classées en **sources
continues** et **sources discrètes**, selon la nature des données
produites.

Une source continue produit des données qui varient de manière continue
dans le temps ou dans leur amplitude (exemples: la parole, la musique).
Ces données peuvent prendre une infinité de valeurs dans un intervalle
donné. D'autre part, une source discrète génère des données sous forme
de séquences de symboles ou de valeurs distinctes, ayant chacune une
probabilité d'occurrence (exemples: texte, fichiers numériques, données
binaires). Le tableau ci-dessous donne un aperçu des deux types de
sources.

Notez que le **codage de source** s'applique uniquement aux sources
discrètes. Les sources continues, bien qu'importantes dans les
communications, nécessitent une étape de numérisation pour être adaptées
au codage de source **(Thème II)**. Cette distinction met en évidence le
rôle central des données discrètes dans l'optimisation des systèmes de
communication modernes.

  **Aspect**                                   **Source Continue**                         **Source Discrète**
  -------------------------------------------- ------------------------------------------- ---------------------------------------------
  **Nature**                                   Signaux analogiques, variations continues   Séquences discrètes de symboles
  **Exemples**                                 Parole, musique, vidéo analogique           Texte, images numériques, fichiers binaires
  **Probabilités**                             Non définies directement                    Bien définies pour chaque symbole
  **Compatibilité avec le codage de source**   Non, sauf après numérisation                Oui, directement applicable

  : Comparaison entre une source continue et une source discrète

## Paramètres d'une source discrète

Une **source discrète** produit des séquences de symboles distincts,
chacun ayant une probabilité d'occurrence. Ces symboles sont générés en
fonction des caractéristiques statistiques de la source.

### Ensemble de symboles

L'ensemble des symboles $\mathcal{S}$ représente toutes les valeurs
possibles qu'une source discrète peut produire.

::: tcolorbox
-   Pour une source textuelle en français :
    $\mathcal{S}= \{A, B, C, \dots, Z\}$.

-   Pour une source binaire : $\mathcal{S} = \{0, 1\}$.
:::

### Probabilités d'occurrence

La probabilité d'occurence $p_i$ d'un symbole $s_i$ représente la
fréquence relative avec laquelle ce symbole apparaît dans la sortie de
la source. Notez que

$\sum_{i=1}^{K} p_i = 1,$

où $K$ est le nombre total de symboles dans l'ensemble $\mathcal{S}$.

::: tcolorbox
-   Pour une source textuelle en anglais : $p(\text{E}) = 0.13$,
    $p(\text{T}) = 0.09$, $p(\text{Z}) = 0.0007$.

-   Pour une source binaire équilibrée : $p(0) = 0.5$, $p(1) = 0.5$.
:::

### Information d'un symbole

L'information apportée par un symbole $s_i$, en bits, est inversément
proportionnelle à sa probabilité d'occurrence. Elle est donnée par :

::: tcolorbox
$I(s_i) = \log_2 \frac{1}{p_i} = -\log_2 p_i.$ bits
:::

Notez que les symboles fréquents contiennent moins d'information quand
$I(s_i)$ est faible, et les symboles rares contiennent plus
d'information quand $I(s_i)$ est élevé.

::: tcolorbox
-   Pour $p(\text{A}) = 0.5$,
    $I(\text{A}) = \log_2 \frac{1}{0.5} = 1 \, \text{bit}$.

-   Pour $p(\text{Z}) = 0.01$,
    $I(\text{Z}) = \log_2 \frac{1}{0.01} = 6.64 \, \text{bits}$.
:::

### Entropie de la source

L'entropie de la source $H(\mathcal{S})$ est la quantité moyenne
d'information produite par symbole. Elle représente une mesure de
l'incertitude ou de la redondance d'une source discrète. Elle est
définie par :

::: tcolorbox
$H(\mathcal{S}) = -\sum_{i=1}^{K} p_i \log_2 p_i$ bits
:::

Une source avec des symboles équiprobables (tous les symboles ont des
probabilités égales), donc $p_i = \frac{1}{K}$ a une entropie maximale
$H(S) = \log_2 K$. Aucune autre source disposant de $K$ données ne peut
créer une entropie plus élevée.

$H(\mathcal{S}) = 0$ si un seul symbole a une probabilité de 1 (source
déterministe). Cela signifie qu'il n'y a pas d'incertitude associée à
cette source.

::: tcolorbox
-   Pour une source binaire équilibrée ($p(0) = 0.5$, $p(1) = 0.5$) :
    $H(\mathcal{S}) = -(0.5 \log_2 0.5 + 0.5 \log_2 0.5) = 1 \, \text{bit}.$

-   Pour une source de text avec $p(\text{A}) = 0.6$,
    $p(\text{B}) = 0.3$, $p(\text{C}) = 0.1$ :
    $H(\mathcal{S}) = -(0.6 \log_2 0.6 + 0.3 \log_2 0.3 + 0.1 \log_2 0.1) \approx 1.485 \, \text{bits}.$
:::

## Codage de source

Le **codage de source** peut être interprété comme une technique
d'étiquetage où chaque symbole produit par une source discrète est
associé à une séquence binaire unique (un code). Ce processus vise à
réduire la longueur moyenne des codes attribués aux symboles, en
fonction de leurs probabilités d'occurrence.

L'objectif est d'associer à chaque symbole $s_k$ **un mot de code
binaire**, exprimé par $\bf{d}_k$ de longueur $l_k$, comme:

::: center
        Donnée          $D_1$        $D_2$      $\ldots$     $D_K$
  ------------------ ------------ ------------ ---------- ------------
     Probabilité        $p_1$        $p_2$      $\ldots$     $p_K$
     Mot de code      $\bf{d}_1$   $\bf{d}_2$   $\ldots$   $\bf{d}_K$
   Longueur du code     $l_1$        $l_2$      $\ldots$     $l_K$
:::

::: tcolorbox
Pour une source générant les symboles $A, B, C, D$ avec des
probabilités; $p_A = 0.4, \, p_B = 0.3, \, p_C = 0.2, \, p_D = 0.1,$ le
codage de source attribue les mots de code suivants :

-   $\bf{d}$$_A = 0$, $l_A = 1$,

-   $\bf{d}$$_B = 10$, $l_B = 2$,

-   $\bf{d}$$_C = 110$, $l_C = 3$,

-   $\bf{d}$$_D = 111$, $l_D = 3$.
:::

## Critères de performance d'un codage de source

Pour évaluer son efficacité, plusieurs critères de performance sont pris
en compte, comme décrit ci-dessous. Ces critères permettent d'évaluer
l'efficacité et l'adéquation des algorithmes de codage de source pour
des applications spécifiques. Un bon algorithme doit minimiser la
longueur moyenne des codes et la redondance, tout en maximisant
l'efficacité de compression, tout cela avec une complexité raisonnable.

### Longueur moyenne des codes ($\bar{l}$)

La longueur moyenne des codes est la moyenne pondérée des longueurs des
codes attribués aux symboles de la source, calculée comme

::: tcolorbox
$\bar{l} = \sum_{i=1}^{K} p_i l_i$ bits
:::

L'objectif est de minimiser $\bar{l}$ tout en garantissant un codage
décodable de manière unique. Notez que même si $\bar{l}$ n'est pas un
nombre entier, chaque valeur de $l_i$ doit être un nombre entier.

::: tcolorbox
Considérons une source avec trois symboles $S = \{A, B, C\}$ ayant les
probabilités $p_A = 0.5$, $p_B = 0.3$, $p_C = 0.2$, et les longueurs de
codes $l_A = 1$, $l_B = 2$, $l_C = 3$. La longueur moyenne des codes est
:
$$\bar{l} = (0.5 \times 1) + (0.3 \times 2) + (0.2 \times 3) = 1.7 \text{ bits}.$$
:::

L'entropie est la limite inférieure théorique pour la longueur moyenne
des codes, donc

::: tcolorbox
$\bar{l} \geq H(S)$
:::

### Variance des Longueurs de Codes ($\sigma_l^2$)

La variance mesure la dispersion des longueurs des codes autour de la
moyenne

::: tcolorbox
$$\sigma_l^2 = \sum_{i=1}^{K} p_i (l_i - \bar{l})^2  \hspace{1cm}  \text{ bits$^2$}.$$
:::

L'objectif est de réduire la variance pour garantir une régularité dans
les longueurs des codes. Une variance faible simplifie la
synchronisation et le décodage.

::: tcolorbox
Avec les mêmes données :
$$\sigma_l^2 = (0.5 \times (1 - 1.7)^2) + (0.3 \times (2 - 1.7)^2) + (0.2 \times (3 - 1.7)^2) \approx 0.41 \text{ bits$^2$}$$
:::

### Redondance

La redondance mesure l'écart entre la longueur moyenne des codes et
l'entropie

::: tcolorbox
$R = \bar{l} - H(S) \hspace{1cm} \text{bits}$
:::

L'objectif est de réduire la redondance pour se rapprocher de
l'efficacité optimale ($\bar{l} \approx H(S)$).

::: tcolorbox
Avec les mêmes symboles et probabilités que ci-dessus :
$$H(S) = -(0.5 \log_2 0.5 + 0.3 \log_2 0.3 + 0.2 \log_2 0.2) \approx 1.485 \text{ bits}.$$
Avec $\bar{l} = 1.7$ et $H(S) = 1.485$, la redondance est :
$$R = 1.7 - 1.485 = 0.215 \text{ bits}.$$
:::

### Efficacité de compression

L'efficacité de compression est le rapport entre l'entropie et la
longueur moyenne des codes :

::: tcolorbox
$\text{Efficacité de compression} = \frac{H(S)}{\bar{l}} \times 100\%.$
:::

On veut maximiser l'efficacité de compression.

::: tcolorbox
Avec $H(S) = 1.485$ et $\bar{l} = 1.7$, l'efficacité est :
$$\text{Efficacité de compression} = \frac{1.485}{1.7} \times 100 \approx 87.35\%.$$
:::

### Taux de Compression

Pour un fichier, taux de compression mesure la réduction de la taille
des données grâce au codage

::: tcolorbox
$\text{Taux de compression} = \frac{\text{Taille originale}}{\text{Taille compressée}}.$
:::

L'objectif est d'obtenir un taux de compression élevé sans perte de
données pour le codage sans perte. Dans le cas limite d'un grand nombre
de données générées, le taux de compression devient égal à l'efficacité
de la compression.

::: tcolorbox
Un fichier texte compressé avec un taux de 4 signifie que sa taille est
divisée par 4.
:::

### Complexité de codage et décodage

La complexité est évaluée par le temps et les ressources nécessaires
pour encoder ou décoder les données.

On veut réduire la complexité tout en maintenant une efficacité élevée.

::: tcolorbox
Le codage de Huffman a une complexité logarithmique pour le décodage
($O(\log K)$). Le codage de Huffman est expliqué dans la section
suivante.

La notation $O(\cdot)$ et les détails sont hors de contenu du cours.
:::

## Codage de Huffman

Le codage de Huffman est une méthode de codage de source optimale basée
sur les probabilités des symboles. C'est-à-dire que les codes de Huffman
donnent la longueur de code moyenne, $\bar{l}$, la plus courte possible.
Un codage optimal comme Huffman attribue des codes plus courts aux
symboles fréquents pour réduire .

Elle attribue des codes binaires plus courts aux symboles fréquents et
des codes plus longs aux symboles rares. Le codage de Huffman, avec ses
applications dans le texte, les images et les vidéos, constitue une
méthode efficace pour atteindre cet objectif. Cette approche illustre la
manière dont les principes mathématiques, tels que l'entropie de
Shannon, se traduisent en solutions pratiques pour les défis des
télécommunications modernes.

**Algorithme pour le codage de Huffman :**\

-   Construction de l'arbre de codage :

    1.  Trier les données par ordre décroissant de probabilité ; chaque
        donnée engendre une branche de l'arbre.

    2.  Associer les bits « 0 » et « 1 » aux deux branches les moins
        probables et relier celles-ci pour en former une seule.

    3.  L'arbre est-il réduit à deux branches ? Si oui, continuer ;
        sinon, aller à 2.

    4.  Associer les bits « 0 » et « 1 » aux deux branches restantes.

-   Obtention du tableau de codage :

    5.  Lire le code de chaque donnée de droite à gauche sur l'arbre.

### Exemple d'exécution

Considérons une source discrète ayant les symboles et probabilités
suivantes :
$$S = \{A, B, C, D, E\}, \quad P = \{p_A = 0.4, p_B = 0.3, p_C = 0.15, p_D = 0.1, p_E = 0.05\}.$$

Construction de l'Arbre de Codage

-   Trier les données par ordre décroissant de probabilité :

    1.  Initialement, les probabilités sont classées :
        $E (0.05), D (0.1), C (0.15), B (0.3), A (0.4)$.

    2.  Fusionner les deux branches les moins probables, ici $E$ et $D$,
        pour former un nœud de probabilité $0.05 + 0.1 = 0.15$. Nouvelle
        liste : $C (0.15), (ED, 0.15), B (0.3), A (0.4)$.

    3.  Répéter le processus : Fusionner $C$ et $(ED)$ pour créer $CED$
        avec $0.15 + 0.15 = 0.3$. Nouvelle liste :
        $(CED, 0.3), B (0.3), A (0.4)$.

    4.  Fusionner $(CED)$ et $B$ pour créer $BCED$ avec
        $0.3 + 0.3 = 0.6$. Nouvelle liste : $(BCED, 0.6), A (0.4)$.

    5.  Fusionner $(BCED)$ et $A$ pour créer la racine avec
        $0.4 + 0.6 = 1.0$.

-   Associer les bits \"0\" et \"1\" aux deux branches restantes.

Obtention du Tableau de Codage:

-   Lire le code de chaque donnée de droite à gauche sur l'arbre :

    -   $A = 0$

    -   $B = 10$

    -   $C = 110$

    -   $D = 1110$

    -   $E = 1111$

## Calcul de la Longueur Moyenne {#calcul-de-la-longueur-moyenne .unnumbered}

-   Longueur des codes : $l_A = 1$, $l_B = 2$, $l_C = 3$, $l_D = 4$,
    $l_E = 4$.

-   Longueur moyenne des codes :
    $$\bar{l} = \sum_{i=1}^{5} p_i l_i = (0.4 \times 1) + (0.3 \times 2) + (0.15 \times 3) + (0.1 \times 4) + (0.05 \times 4) = 2.05 \text{ bits}.$$

## Comparaison avec l'Entropie {#comparaison-avec-lentropie .unnumbered}

-   Entropie de la source :
    $$H(S) = -(0.4 \log_2 0.4 + 0.3 \log_2 0.3 + 0.15 \log_2 0.15 + 0.1 \log_2 0.1 + 0.05 \log_2 0.05) \approx 2.029 \text{ bits}.$$

-   La longueur moyenne ($\bar{l} = 2.05$) est proche de l'entropie
    ($H(S) = 2.029$), ce qui montre l'efficacité du codage.

## Arbre de Codage {#arbre-de-codage .unnumbered}

::: center
:::

::: tcolorbox
Un fichier contient 50 000 caractères codés initialement avec 7 bits par
caractère, soit $50,000 \times 7 = 350,000 \, \text{bits}$. Si
l'entropie de la source est $H(S) = 4 \, \text{bits}$, le codage de
Huffman peut réduire la taille à environ :
$50,000 \times 4 = 200,000 \, \text{bits}.$
:::

1.  [Section girisi - learning objectives]{style="color: magenta"}

2.  [Section cikisi -- onemli bilgi tablosu ]{style="color: magenta"}

3.  [Types de Codage de Source]{style="color: magenta"}

4.  [Huffman coding examples ]{style="color: magenta"}

5.  [Links]{style="color: magenta"}

6.  [Translations]{style="color: magenta"}

7.  [Detailed solutions]{style="color: magenta"}

8.  [Source coding sekli - discrete source - cikisi cahacter - clusteri
    donne pl occurece probability - souce codera giriyor d_k cikiyor -
    notationi belirle + performance citerlerini ekle
    sekle]{style="color: magenta"}

9.  [Links - section 1 baglantisini yap]{style="color: magenta"}

10. [bitleri baska font goster - Huffman algorithmasinda da var
    bu]{style="color: magenta"}

11. [kitapla baglantisini kur - further reading section ekle -
    problemler ekle]{style="color: magenta"}

## [Types de Codage de Source]{style="color: magenta"}

Le codage de source peut être classé en deux dimensions principales : 1.
\*\*Codage sans perte (lossless) vs codage avec perte (lossy)\*\* 2.
\*\*Codage à longueur fixe (fixed length) vs codage à longueur variable
(variable length)\*\*

Ces classifications définissent comment les symboles d'une source sont
représentés en séquences binaires, en fonction des besoins de
l'application (fidélité des données, efficacité de compression, etc.).

\#### \*\*Codage Sans Perte (Lossless coding)\*\* Le codage sans perte
garantit que les données originales peuvent être entièrement
reconstruites à partir des données compressées, sans aucune perte
d'information.

\*\*Exemples\*\* : - Codage de Huffman : Réduit la longueur moyenne des
codes en fonction des probabilités des symboles. - LZW
(Lempel-Ziv-Welch) : Utilisé dans les formats ZIP et GIF.

\*\*Applications\*\* : - Textes, bases de données, fichiers exécutables
où une perte d'information est inacceptable.

\*\*Avantages\*\* : - Fidélité absolue des données. - Utilisable dans
des contextes où la précision est essentielle.

\*\*Inconvénients\*\* : - Taux de compression limité, particulièrement
pour des données avec peu de redondance.

\#### \*\*Codage Avec Perte\*\* (Lossy coding) Le codage avec perte
élimine les données redondantes ou moins perceptibles pour réduire la
taille des données, mais les données originales ne peuvent pas être
totalement récupérées.

\*\*Exemples\*\* : - JPEG : Réduction de la taille des images en
supprimant des détails visuellement insignifiants. - MP3 : Compression
audio en réduisant les fréquences inaudibles.

\*\*Applications\*\* : - Multimédia (images, vidéos, audio) où une
légère perte d'information est tolérable.

\*\*Avantages\*\* : - Taux de compression élevé. - Efficace pour les
grandes quantités de données multimédia.

\*\*Inconvénients\*\* : - Perte irréversible d'information. - Qualité
dégradée si la compression est excessive.

\#### \*\*Codage à Longueur Fixe\*\* (Fixed length coding) Chaque
symbole de la source est représenté par un code binaire de longueur
constante, indépendamment de sa probabilité d'occurrence.

\*\*Exemples\*\* : - ASCII : Chaque caractère est codé sur 7 bits. -
Code binaire standard : Une source à 4 symboles ($S = \{A, B, C, D\}$)
utilise 2 bits par symbole.

\*\*Applications\*\* : - Systèmes où la simplicité de décodage est
prioritaire.

\*\*Avantages\*\* : - Décodage rapide et simple. - Bonne adaptabilité
pour des symboles de probabilité équivalente.

\*\*Inconvénients\*\* : - Inefficace si les symboles ont des
probabilités inégales.

\#### \*\*Codage à Longueur Variable\*\* (Variable length coding) Chaque
symbole est représenté par un code de longueur différente, les symboles
fréquents recevant des codes plus courts et les symboles rares des codes
plus longs.

\*\*Exemples\*\* : - Codage de Huffman : Optimise la longueur moyenne en
fonction des probabilités. - Codage arithmétique : Attribue des codes
fractionnaires pour une meilleure compression.

\*\*Applications\*\* : - Compression de données où l'efficacité est
cruciale.

\*\*Avantages\*\* : - Compression plus efficace pour des sources à
probabilités inégales. - Longueur moyenne proche de l'entropie.

\*\*Inconvénients\*\* : - Décodage plus complexe (nécessite une
condition de préfixe). - Sensibilité aux erreurs dans la séquence
binaire.

\#### Tableau Comparatif des Types de Codage de Source

\> Add blockquote

# Types de Codage et leurs Caractéristiques {#types-de-codage-et-leurs-caractéristiques .unnumbered}

  **Type de Codage**                        **Définition**                                                              **Exemples**            **Avantages**                                **Inconvénients**                                      **Applications**
  ----------------------------------------- --------------------------------------------------------------------------- ----------------------- -------------------------------------------- ------------------------------------------------------ ------------------------------------
  **Sans Perte (Lossless)**                 Fidélité totale, données reconstructibles                                   Huffman, LZW            Aucune perte d'information                   Taux de compression limité                             Textes, bases de données, archives
  **Avec Perte (Lossy)**                    Compression irréversible, données partiellement perdues                     JPEG, MP3               Taux de compression élevé                    Perte de qualité irréversible                          Images, vidéos, audio
  **Longueur Fixe (Fixed Length)**          Codes binaires de longueur constante pour tous les symboles                 ASCII, code binaire     Décodage simple, rapide                      Inefficace pour des symboles à probabilités inégales   Systèmes simples
  **Longueur Variable (Variable Length)**   Codes plus courts pour symboles fréquents, plus longs pour symboles rares   Huffman, arithmétique   Compression efficace, proche de l'entropie   Décodage plus complexe                                 Compression de données, multimédia

  : Comparaison entre une source continue et une source discrète

### Choix du design

Le choix du type de codage de source dépend des exigences spécifiques de
l'application. Le codage sans perte est indispensable pour les données
critiques, tandis que le codage avec perte convient aux scénarios
multimédias où un compromis entre qualité et compression est acceptable.
De même, les codages à longueur fixe sont adaptés aux systèmes simples
et uniformes, tandis que les codages à longueur variable sont optimaux
pour des sources avec des symboles de probabilités différentes,
permettant une utilisation plus efficace des ressources.

## Conclusion

Le codage de source en tant que technique d'étiquetage attribue des
séquences binaires aux symboles d'une source discrète, en optimisant la
longueur moyenne des codes ($\bar{l}$) pour minimiser la redondance.
Cette approche repose sur les probabilités des symboles ($p_k$) et leur
relation avec l'information contenue ($I(s_k)$). Le résultat est une
représentation efficace des données qui utilise des codes courts pour
les symboles fréquents et des codes plus longs pour les symboles rares,
respectant les contraintes de décodage unique et d'optimisation de la
compression.
