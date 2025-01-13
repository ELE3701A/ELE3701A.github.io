# Section 6

Le codage pour le contrôle des erreurs est utilisé dans les systèmes de
communication numériques pour garantir une transmission fiable des
données malgré les perturbations du canal. Les données d'entrée, sous
forme numérique, sont encodées en mots de code contenant des bits
redondants qui permettent de détecter et corriger les erreurs. Ces
systèmes, comme les codes blocs ou convolutionnels, jouent un rôle
essentiel dans les applications telles que les réseaux sans fil, les
systèmes de stockage ou les transmissions par satellite, réduisant ainsi
les pertes de données et améliorant l'efficacité globale.

Le contrôle des erreurs est une composante essentielle des systèmes de
communication modernes. Son objectif principal est de garantir une
transmission fiable des données malgré les imperfections des canaux de
communication, tels que le bruit, les interférences ou les pertes de
signal. En introduisant des mécanismes de détection et de correction des
erreurs, le contrôle des erreurs permet d'assurer l'intégrité des
données tout en minimisant le besoin de retransmissions.

## Théorie du Codage

Le codage joue un rôle fondamental dans les systèmes de communication en
structurant les données de manière à faciliter la détection et la
correction des erreurs.

Les canaux de communication sont souvent imparfaits, ce qui introduit
des erreurs dans les données transmises. Ces erreurs peuvent provenir de
diverses sources, notamment le bruit thermique, les interférences et les
limitations physiques.

Les codes de contrôle des erreurs peuvent être classés en deux
catégories principales; les codes blocs, et les codes convolutionnels.
Les **codes blocs** transforment des blocs fixes de données en mots de
code plus longs, ajoutant une redondance pour détecter et corriger les
erreurs. Contrairement aux codes blocs, les **codes convolutionnels :**
génèrent des mots de code basés sur les bits actuels et précédents, ce
qui offre une protection continue. Dans ce cours, nous nous
concentrerons sur les types fondamentaux de codes blocs, tandis que les
codes convolutionnels seront introduits pour offrir un aperçu
complémentaire du sujet.

### Champs finis

Les calculs dans le codage reposent souvent sur des champs de Galois
(*Galois field*; GF), tels que GF($2$). Ces champs permettent de définir
des opérations binaires, comme l'addition et la multiplication modulo 2,
qui sont au cœur des algorithmes de codage.

Les opérations dans le champ de Galois GF(2) sont essentielles pour le
codage et le décodage dans les systèmes numériques. Voici les deux
opérations fondamentales :

#### Addition modulo 2

L'addition dans GF(2) est équivalente à l'opération XOR (ou exclusif)
entre deux bits. Cette opération est commutative et associative.

-   **Règles :** $0 + 0 = 0$, $1 + 1 = 0$, $0 + 1 = 1$, $1 + 0 = 1$.

-   **Propriétés :** Toute valeur ajoutée à elle-même donne 0
    ($a + a = 0$).

**Exemple :**

-   $1011 + 1101 = 0110$.

#### Multiplication modulo 2

La multiplication dans GF(2) est équivalente à l'opération AND logique
entre deux bits. Elle est également commutative et associative.

-   **Règles :** $0 \cdot 0 = 0$, $1 \cdot 1 = 1$, $0 \cdot 1 = 0$,
    $1 \cdot 0 = 0$.

-   **Propriétés :** Toute valeur multipliée par 0 donne 0, et par 1
    donne elle-même ($a \cdot 1 = a$).

**Exemple :**

-   $1011 \cdot 1101 = 1001$ (calcul bit à bit).

## Codes Blocs

Un code bloc est une méthode de codage où des blocs fixes de $k$ bits
d'information sont encodés en blocs de $n$ bits appelés mots de code, où
$n > k$. Les paramètres fondamentaux d'un code bloc sont :

-   **Dimension du code :** $(n, k)$, où $k$ est le nombre de bits
    d'information et $n$ le nombre total de bits dans le mot de code.

-   **Taux de code :** $R = \frac{k}{n}$, qui indique l'efficacité du
    code en termes de bits d'information transmis.

-   **Distance minimale :** $d_{\text{min}}$, la plus petite distance de
    Hamming entre deux mots de code distincts. Elle détermine la
    capacité de détection et de correction d'erreurs.

-   **Redondance :** $n - k$, le nombre de bits ajoutés pour assurer la
    protection contre les erreurs.

### Définition des Bits d'Entrée et du Code

Dans un code bloc, un vecteur d'information
$\textbf{d} = [d_1, d_2, \ldots, d_k]$ est encodé en un mot de code
$\textbf{c} = [c_1, c_2, \ldots, c_n]$, où $n > k$. Le processus
d'encodage introduit des bits de parité $[c_{k+1}, \ldots, c_n]$ qui
sont calculés à partir des bits d'information. Ces bits de parité
assurent la détection et la correction des erreurs.

### Équations de Parité

Les bits de parité $c_{k+1}, \ldots, c_n$ sont obtenus à partir des bits
d'information $d_1, \ldots, d_k$ à l'aide des relations linéaires
suivantes : $$\begin{aligned}
    c_{k+1} &= h_{1,1}d_1 \oplus h_{1,2}d_2 \oplus \ldots \oplus h_{1,k}d_k, \\
    c_{k+2} &= h_{2,1}d_1 \oplus h_{2,2}d_2 \oplus \ldots \oplus h_{2,k}d_k, \\
    &\vdots \\
    c_n &= h_{m,1}d_1 \oplus h_{m,2}d_2 \oplus \ldots \oplus h_{m,k}d_k,
\end{aligned}$$

où $\textbf{H} = [h_{i,j}]$ est une matrice $m \times k$ définissant les
relations de parité.

### Matrice Génératrice et Matrice de Vérification de Parité

-   **Matrice Génératrice $\textbf{G}$**

    -   La matrice $\textbf{G}$ combine une matrice identité
        $\textbf{I}_k$ et une matrice $\textbf{P}$ définissant les
        relations de parité.

    -   Forme générale : $\textbf{G} = [\textbf{I}_k \ | \ \textbf{P}]$.

-   **Matrice de Vérification de Parité $\textbf{H}$**

    -   La matrice $\textbf{H}$ est utilisée pour vérifier les mots de
        code reçus et détecter les erreurs.

    -   Forme générale :
        $\textbf{H} = [\textbf{P}^T \ | \ \textbf{I}_m]$, où
        $m = n - k$.

### Exemple Numérique

Considérons un code $(7, 4)$ avec les matrices suivantes :
$$\begin{aligned}
    \textbf{G} &= \begin{bmatrix}
        1 & 0 & 0 & 0 & 1 & 1 & 0 \\
        0 & 1 & 0 & 0 & 1 & 0 & 1 \\
        0 & 0 & 1 & 0 & 0 & 1 & 1 \\
        0 & 0 & 0 & 1 & 1 & 1 & 1
    \end{bmatrix}, \\
    \textbf{H} &= \begin{bmatrix}
        1 & 1 & 0 & 1 & 1 & 0 & 0 \\
        1 & 0 & 1 & 1 & 0 & 1 & 0 \\
        0 & 1 & 1 & 1 & 0 & 0 & 1
    \end{bmatrix}.
\end{aligned}$$

**Encodage :** Pour un vecteur d'information
$\textbf{d} = [1, 0, 1, 1]$, le mot de code est : $$\begin{aligned}
    \textbf{c} &= \textbf{dG} = [1, 0, 1, 1, 0, 1, 0].
\end{aligned}$$

**Décodage :** Si le mot reçu est $\textbf{r} = [1, 0, 1, 1, 1, 1, 0]$,
le syndrome est calculé comme : $$\begin{aligned}
    \textbf{s} &= \textbf{rH}^T = [1, 0, 1].
\end{aligned}$$ Ce syndrome indique une erreur au troisième bit. Après
correction, le mot de code devient : $$\begin{aligned}
    \textbf{c} &= [1, 0, 1, 1, 0, 1, 0].
\end{aligned}$$

### Stratégie de conception

La conception d'un code bloc implique les étapes suivantes :

1.  Identifier les contraintes du système, comme le type de canal, le
    taux d'erreur souhaité et la capacité de correction.

2.  Choisir les paramètres $(n, k)$ pour équilibrer la redondance et
    l'efficacité.

3.  Construire une matrice génératrice $\textbf{G}$ pour générer les
    mots de code.

4.  Construire une matrice de vérification de parité $\textbf{H}$ pour
    détecter et localiser les erreurs.

## Formation des matrices $\textbf{G}$ et $\textbf{H}$

-   **Matrice génératrice $\textbf{G}$ :**

    -   Elle est composée de deux parties : une matrice identité
        $\textbf{I}_k$ de taille $k \times k$ et une matrice
        $\textbf{P}$ contenant les coefficients de parité.

    -   Forme générale : $\textbf{G} = [\textbf{I}_k \ | \ \textbf{P}]$.

-   **Matrice de vérification de parité $\textbf{H}$ :**

    -   Elle est construite pour vérifier la validité des mots de code.

    -   Forme générale :
        $\textbf{H} = [\textbf{P}^T \ | \ \textbf{I}_{n-k}]$, où
        $\textbf{P}^T$ est la transposée de $\textbf{P}$.

## Exemple numérique

Considérons un code $(7, 4)$ avec les matrices suivantes :
$$\begin{aligned}
    \textbf{G} &= \begin{bmatrix}
        1 & 0 & 0 & 0 & 1 & 1 & 0 \\
        0 & 1 & 0 & 0 & 1 & 0 & 1 \\
        0 & 0 & 1 & 0 & 0 & 1 & 1 \\
        0 & 0 & 0 & 1 & 1 & 1 & 1
    \end{bmatrix}, \\
    \textbf{H} &= \begin{bmatrix}
        1 & 1 & 0 & 1 & 1 & 0 & 0 \\
        1 & 0 & 1 & 1 & 0 & 1 & 0 \\
        0 & 1 & 1 & 1 & 0 & 0 & 1
    \end{bmatrix}.
\end{aligned}$$

**Encodage :** Pour un vecteur d'information
$\textbf{d} = [1, 0, 1, 1]$, le mot de code est calculé comme :
$$\begin{aligned}
    \textbf{c} &= \textbf{dG} = [1, 0, 1, 1, 0, 1, 0].
\end{aligned}$$

**Équations de parité :** Les bits de parité peuvent être vérifiés à
l'aide des équations suivantes : $$\begin{aligned}
    c_5 &= d_1 \oplus d_2 \oplus d_3, \\
    c_6 &= d_1 \oplus d_2 \oplus d_4, \\
    c_7 &= d_2 \oplus d_3 \oplus d_4.
\end{aligned}$$

**Décodage avec syndrome :** Si le mot reçu est
$\textbf{r} = [1, 0, 1, 1, 1, 1, 0]$, le syndrome est calculé comme :
$$\begin{aligned}
    \textbf{s} &= \textbf{rH}^T = [1, 0, 1].
\end{aligned}$$ Ce syndrome correspond à une erreur au troisième bit.
Après correction, le mot de code devient
$\textbf{c} = [1, 0, 1, 1, 0, 1, 0]$.

**Exemple : Hamming $(7,4)$** $$\begin{aligned}
\mathbf{G} &= \begin{bmatrix}
1 & 0 & 0 & 0 & 1 & 1 & 0 \\
0 & 1 & 0 & 0 & 1 & 0 & 1 \\
0 & 0 & 1 & 0 & 0 & 1 & 1 \\
0 & 0 & 0 & 1 & 1 & 1 & 1
\end{bmatrix}
\end{aligned}$$ **Matrice de vérification ($\mathbf{H}$)**
$$\begin{aligned}
\mathbf{H} &= \begin{bmatrix}
1 & 1 & 0 & 1 & 1 & 0 & 0 \\
1 & 0 & 1 & 1 & 0 & 1 & 0 \\
0 & 1 & 1 & 1 & 0 & 0 & 1
\end{bmatrix}
\end{aligned}$$

## Exemple numérique : Vérification de parité

Supposons un code $(4,3)$ avec
$\mathbf{G} = \begin{bmatrix} 1 & 0 & 0 & 1 \\ 0 & 1 & 0 & 1 \\ 0 & 0 & 1 & 1 \end{bmatrix}$.

-   Information transmise : $[1, 0, 1]$.

-   Mot de code émis : $[1, 0, 1, 0]$.

-   Mot reçu : $[1, 0, 0, 0]$.

-   Syndrome :
    $\mathbf{s} = \mathbf{r} \mathbf{H}^T = [1, 0, 0, 0] \begin{bmatrix} 1 & 1 & 0 & 1 \\ 0 & 1 & 1 & 1 \end{bmatrix}^T$.

**Définitions :**\

-   Addition modulo-2 : $1\oplus 1= 0 \oplus 0 = 0$ et
    $1\oplus 0= 1 \oplus 0 = 1$.\

-   Poids de Hamming : Nombre de "$1$" dans un mot de code ex.
    $w_H(0111)=3$.\

-   Distance de Hamming entre deux mots de code : Nombre de positions où
    les deux mots de codes sont différents, ex.
    $d_H(0111, 1111)= w_H(0111 \oplus 1111) = 1$.\

-   Distance minimal de Hamming d'un code $d_{min}$: la plus petite
    $d_H$.\

### Performance et critères

La performance des codes est mesurée par plusieurs critères :

-   **Distance minimale ($d_{\text{min}}$) :** Elle détermine le pouvoir
    de détection et de correction des erreurs. Par exemple, un code avec
    $d_{\text{min}} = 3$ peut corriger une erreur et détecter jusqu'à
    deux erreurs.

-   **Redondance :** Définie comme $n - k$, elle reflète le nombre de
    bits ajoutés pour protéger les données.

-   **Efficacité :** Mesurée par le taux de code $R = \frac{k}{n}$, elle
    indique la proportion de bits utiles dans le mot de code.

## Exemples de Codes

### Codes Hamming

Les codes Hamming sont des codes blocs capables de détecter jusqu'à deux
erreurs et de corriger une seule erreur.

-   **Structure :** Ils utilisent des matrices $\textbf{G}$ et
    $\textbf{H}$ spécifiques pour générer et vérifier les mots de code.

-   **Correction :** Le syndrome identifie la position de l'erreur à
    corriger.

-   **Exemple :** Un code $(7,4)$ avec
    $\textbf{r} = [1, 1, 0, 1, 1, 0, 1]$ et un syndrome calculé corrige
    l'erreur au bit 2.

### Codage par répétition

Le codage par répétition est une approche simple qui améliore la
fiabilité par redondance.

-   **Principe :** Chaque bit est répété plusieurs fois pour faciliter
    la détection et la correction des erreurs.

-   **Règle de majorité :** La valeur la plus fréquente dans les bits
    répétés est considérée comme correcte.

-   **Exemple :** Pour $\textbf{r} = [1, 1, 0]$, la règle de majorité
    donne $\textbf{c} = 1$.

### Codes CRC et polynomiaux

Les codes CRC (Cyclic Redundancy Check) sont largement utilisés pour la
détection des erreurs.

-   **Principe :** Basés sur la division polynomiale, ils ajoutent un
    résidu comme code de contrôle.

-   **Application :** Les CRC sont utilisés dans les protocoles réseau
    et les systèmes de stockage.

-   **Exemple :** Un polynôme générateur $P(x) = x^3 + x + 1$ peut être
    utilisé pour générer un CRC pour un message donné.

## Design des Codes

Le design des codes implique des décisions basées sur les besoins en
performance et en complexité.

-   **Choix des paramètres :**

    -   La taille des blocs ($n$, $k$) pour les codes blocs.

    -   La contrainte de longueur pour les codes convolutionnels.

-   **Critères de performance :**

    -   Maximisation du taux de code $R$ tout en garantissant une
        redondance suffisante.

    -   Optimisation pour un compromis entre la détection et la
        correction des erreurs.

-   **Applications :** Adapter le type de code en fonction du canal et
    des exigences du système (par exemple, codes Hamming pour le
    stockage, codes convolutionnels pour les communications sans fil).

### Comparaison entre codes blocs et codes convolutionnels

-   **Structure :**

    -   Les codes blocs encodent des blocs fixes de $k$ bits
        d'information en $n$ bits, où $n > k$.

    -   Les codes convolutionnels utilisent des registres à décalage
        pour produire une séquence codée continue.

-   **Redondance :**

    -   Les codes blocs ont une redondance déterminée par le rapport
        $R = \frac{k}{n}$.

    -   Les codes convolutionnels introduisent une redondance continue,
        généralement mesurée par la contrainte de longueur.

-   **Complexité de décodage :**

    -   Les codes blocs utilisent des algorithmes comme la détection par
        syndrome, souvent moins complexes.

    -   Les codes convolutionnels nécessitent des algorithmes tels que
        Viterbi, qui sont plus complexes mais efficaces.

-   **Applications :**

    -   Les codes blocs sont souvent utilisés dans le stockage de
        données et les transmissions fixes.

    -   Les codes convolutionnels sont préférés pour les communications
        continues, comme les transmissions sans fil.
