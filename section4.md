# Section 4

La transmission de signaux repose sur l'utilisation de canaux, qui
peuvent être modélisés comme des systèmes. Ces systèmes, linéaires ou
non linéaires, déterminent la manière dont les signaux sont altérés ou
transformés lors de leur propagation. Cette subsection se concentre sur
les propriétés des systèmes modélisant les canaux de transmission, en
mettant l'accent sur les distorsions et les limites des performances.

## Définition d'un système

Un système est une entité qui prend un ou plusieurs signaux d'entrée et
produit un ou plusieurs signaux de sortie. Ces systèmes peuvent être
caractérisés par leur comportement lorsqu'ils transforment les entrées
en sorties. En fonction des propriétés de cette transformation, un
système peut être classé comme linéaire ou non linéaire. Un canal de
transmission peut également être modélisé comme un système, qui peut
être linéaire ou non linéaire, en fonction de ses propriétés.

### Systèmes linéaires

Un système est dit linéaire s'il respecte deux propriétés fondamentales
: la superposition et l'homogénéité. La superposition signifie que la
réponse du système à une somme d'entrées est égale à la somme des
réponses individuelles à chacune de ces entrées. L'homogénéité indique
que si une entrée est multipliée par une constante, la sortie sera
également multipliée par cette constante. Les systèmes linéaires sont
largement utilisés en communication et traitement du signal en raison de
leur simplicité analytique.

**Distorsion dans les systèmes linéaires :**\

-   Signal d'entrée : $x(t)\Longleftrightarrow X(f)$,

-   Réponse impulsionnelle du canal : $h(t)$,

-   Réponse fréquentielle du canal : $H(f)$,
    ($h(t)\Longleftrightarrow H(f)$)

-   Signal de sortie : $y(t)\Longleftrightarrow Y(f)$ où
    $y(t) = x(t) * h(t)  \Longleftrightarrow  Y(f) = X(f) H(f)$

Considérons un signal d'entrée $x(t) = \cos(2 \pi f_0 t)$ et une réponse
impulsionnelle du canal $h(t) = e^{-t} u(t)$ (où $u(t)$ est la fonction
échelon).

-   Réponse fréquentielle : $H(f) = \frac{1}{1 + j 2 \pi f}$.

-   Signal de sortie dans le domaine fréquentiel : $Y(f) = X(f) H(f)$.

-   Pour $f_0 = 10$ Hz, $H(10) \approx \frac{1}{1 + j 62.8}$, ce qui
    atténue le signal et introduit un déphasage.

### Systèmes non linéaires

Un système non linéaire ne respecte pas les principes de superposition
et d'homogénéité. Cela peut entraîner des comportements complexes, tels
que l'amplification disproportionnée, la génération de fréquences non
présentes dans le signal d'entrée (harmoniques), et l'intermodulation.
Ces systèmes sont souvent utilisés dans des contextes spécifiques où des
effets non linéaires sont souhaités ou inévitables, nécessitant des
méthodes d'analyse avancées.

**Distorsion dans les systèmes non linéaires :**\

-   Signal d'entrée : $x(t)$,

-   La sortie doit être calculée en fonction de $x(t)$ (ex. :
    $y(t) = \alpha x(t)+  \beta x^2(t) + \gamma x^3(t)$ )

Prenons un système non linéaire avec $y(t) = x(t) + 0.5 x^2(t)$ et
$x(t) = \cos(2 \pi f_0 t)$.

-   Le terme $x^2(t)$ produit une composante de fréquence $2f_0$.

-   Si $f_0 = 10$ Hz, la sortie contient les fréquences $10$ Hz
    (fondamentale) et $20$ Hz (harmonique).

-   Cette distorsion harmonique peut être observée dans le spectre de
    $y(t)$.

## Distorsion

### Distorsion dans les systèmes linéaires

La distorsion dans les systèmes linéaires résulte d'une réponse en
fréquence non uniforme. Cela signifie que certaines fréquences d'un
signal sont amplifiées ou atténuées différemment, entraînant une
déformation du signal transmis. Cette distorsion peut être atténuée en
utilisant des égalisateurs ou des filtres appropriés pour compenser les
variations de la réponse en fréquence.

### Distorsion non linéaire

La distorsion non linéaire survient lorsque le système introduit des
composantes fréquentielles non présentes dans le signal d'origine. Ces
nouvelles fréquences, appelées harmoniques ou produits
d'intermodulation, peuvent causer une interférence entre les signaux
transmis. Pour minimiser ce type de distorsion, il est essentiel de
maintenir le système dans une plage de fonctionnement linéaire.

## Canal de transmission

### Limite de Shannon

La limite de Shannon définit la capacité maximale d'un canal en bits par
seconde, compte tenu de la bande passante et du rapport signal sur
bruit. Cette limite est exprimée par la formule
$C = B \log_2(1 + \text{SNR})$, où $B$ est la bande passante et SNR est
le rapport signal sur bruit. Comprendre cette limite est crucial pour
concevoir des systèmes de communication efficaces qui maximisent le
débit tout en minimisant les erreurs.

**La capacité d'un canal de largeur de bande de $W$ Hz :**\

-   $C=W \log_2 \left( 1 + \frac{P_{message}}{P_{bruit}}\right)$
    bits/sec où $P_{message}$ est la puissance du message et $P_{bruit}$
    est la puissance du bruit. Noter que on veut $R_b  \leq C$.

### Exemples de canaux (modèle physique)

Les canaux de transmission physiques incluent des supports tels que les
paires torsadées, les câbles coaxiaux, les fibres optiques, et les
liaisons sans fil. Chaque type de canal a des caractéristiques
spécifiques, comme la bande passante et la susceptibilité aux
interférences. Par exemple, les fibres optiques offrent une très grande
capacité de transmission et une faible atténuation, mais nécessitent des
convertisseurs électro-optiques complexes.

## Modèle statistique du canal

### Modèle de canal binaire

Un modèle de canal binaire simplifie l'analyse en considérant uniquement
deux états, 0 et 1, pour chaque bit transmis. Les probabilités d'erreur
sont caractérisées par des transitions comme $P(D=1|E=0)$ et
$P(D=0|E=1)$, où $E$ est le bit émis et $D$ est le bit reçu. Ce modèle
est utile pour évaluer la performance des systèmes de communication en
termes de taux d'erreur.

### Taux d'erreur

Le taux d'erreur moyen est défini comme la probabilité qu'un bit soit
incorrectement reçu. Il est donné par
$P(\text{Erreur}) = P(D=0|E=1)P(E=1) + P(D=1|E=0)P(E=0)$. Pour des bits
équiprobables, cette probabilité se simplifie à
$P(D=0|E=1) + P(D=1|E=0)/2$. L'amélioration du taux d'erreur peut être
obtenue via des techniques de codage et de modulation avancées.

## Exemples Numériques

### Exemple 1: Analyse de distorsion d'amplitude

Considérons un signal à bande passante de 15 kHz centré sur 150 MHz
transmis dans un environnement où une réflexion sur un obstacle se
produit. Le récepteur capte à la fois le signal direct et le signal
réfléchi. Une analyse spectrale montre une légère distorsion
d'amplitude, car la différence de phase entre les signaux interfère avec
certaines composantes fréquentielles.

### Exemple 2: Capacité maximale d'un canal

Pour un canal sans fil avec une bande passante de 10 kHz et un rapport
signal sur bruit de 20 dB, la capacité maximale selon Shannon est
calculée comme suit : $$\begin{aligned}
C &= 10^4 \log_2(1 + 10^{20/10}) \\
  &= 10^4 \log_2(101) \\
  &\approx 66.4 \text{ kbps}.
\end{aligned}$$ Cela illustre l'importance d'augmenter la bande passante
ou le rapport signal sur bruit pour améliorer le débit maximal.
