# Section 2

Cette section présente les concepts fondamentaux du traitement des
signaux, essentiels pour comprendre et analyser les systèmes de
communication. Elle aborde les définitions, classifications et
opérations de base des signaux, tout en mettant en avant des exemples
pratiques. L’analyse de Fourier y est développée pour explorer la
décomposition des signaux en composantes fréquentielles. Les principes de modulation
d’amplitude et les systèmes linéaires invariants dans le temps (LTI)
sont également discutés, avec un accent sur des notions clés telles que
la largeur de bande, la densité spectrale de puissance,
l’autocorrélation et les filtres. Enfin, la section introduit les
signaux aléatoires, en se concentrant sur les distributions gaussiennes,
les moyennes statistiques et le théorème de la limite centrale,
établissant ainsi une base solide pour l’étude des signaux dans des
environnements variés.

## Signaux
 

(def-signal)=
Definition: Signal 
: Un **signal** est une fonction qui transmet des
informations sur un phénomène.

Les signaux constituent les entrées et les sorties des systèmes. Un
signal peut être classé selon différents critères. Les critères que nous
allons examiner sont énumérés ci-dessous.

1.  Signaux à temps continu et à temps discret:

    -   Un **signal à temps continu** est un signal $g(t)$ pour lequel
        la variable indépendante $t$ prend des nombres réels.

    -   Un **signal à temps discret**, noté $g[n]$, est un signal pour
        lequel la variable indépendante $n$ prend ses valeurs dans
        l’ensemble des entiers.

    -   En échantillonnant un signal à temps continu $g(t)$ à des
        instants séparés par $T_E$, nous pouvons définir le signal à
        temps discret $g[nT_E]$. Ici, $n$ est l’indice de temps,
        représentant le $n$ième échantillon.


```{figure} images/signal-class-1.png
:label: signal-class-1
:align: center
Signaux à temps continu et à temps discret (la période d'échantillonnage est de $T_E = 0.5$ unités de temps). 

```


2.  Signaux analogiques et numériques

    -   Un signal dont l’amplitude peut prendre n’importe quelle valeur
        dans une gamme continue est un **signal analogique**.

        -   Cela signifie que l’amplitude d’un **signal analogique**
            peut prendre un nombre (indénombrable) infini de valeurs.

    -   Un **signal numérique**, par contre, est un signal dont
        l’amplitude ne peut prendre qu’un nombre fini de valeurs.

```{figure} images/signal-class-2.png
:label: signal-class-2
:align: center
Signaux analogiques et numériques.

```

3.  Signaux périodiques et non périodiques.

    -   Un **signal périodique** se répète dans le temps ; il suffit
        donc de spécifier le signal dans un intervalle de base appelé
        période, $T_0$, Pour un signal signal périodique :
        $$g(t) = g(t + T_0), \, \forall t$$

    -   Un **signal non périodique** ne se répète pas dans le temps. 

```{figure} images/signal-class-3.png
:label: signal-class-3
:align: center
Signaux périodiques (où $T_0 = 6$ unités de temps) et non périodiques.  

```


4.  Signaux réels et complexes. 

    -   Un **signal réel** prend ses valeurs dans l'ensemble des nombres réels, $g(t)\in \mathbb{R}$

    -   Un **signal complexe** prend ses valeurs dans l'ensemble des nombres complexes $g(t)\in \mathbb{C}$.

```{figure} images/signal-class-4.png
:label: signal-class-4
:align: center
Signaux réels et complexes.  Le signal réel est l'onde sinusoïdale $g(t) = \sin(t)$. Le signal complexe est $g(t) = e^{jt} = \cos(t) + j\sin(t)$, dont les parties réelle $( \cos(t)) $ et imaginaire $( \sin(t) )$ sont tracées séparément.
```

 

5.  Signaux déterministes et aléatoires.

    -   Dans un **signal déterministe**, à tout instant $t$, la valeur
        de $g(t)$ est donnée comme une valeur réelle ou complexe.

    -   Dans un **signal aléatoire** (ou stochastique), à un instant
        donné $t$, $g(t)$ est une variable aléatoire, c’est-à-dire
        qu’elle est définie par une fonction de densité de probabilité.


```{figure} images/signal-class-5.png
:label: signal-class-5
:align: center
Signaux déterministes et aléatoires. Le signal déterministe $ g(t) = \sin(t)$ est parfaitement prévisible à tout instant $ t $. Chaque valeur est fixée et définie.
Le signal aléatoire est une superposition d'une onde sinusoïdale et d'un bruit gaussien aléatoire. La valeur de $g(t) $ à un instant donné est imprévisible et suit une distribution aléatoire (donc les valeurs sont imprévisibles).
```
 

Notez que toutes ces représentations sont du domaine temporel. Pour pouvoir
comprendre le comportement spectral, nous devons également analyser les
signaux dans le domaine fréquentiel. 

### Représentation fréquentielle des signaux

Dans ce cours, nous utiliserons la transformée de Fourier pour
représenter les signaux, même pour les signaux périodiques

(def-FT)=
Definition: Transformée de Fourier 
:  La transformée de Fourier d’un signal $g(t)$ est
représentée par $g(t) \iff G(f)$.

:::{hint} Transformation 
```{math}
:label: FT
G(f) = \int_{-\infty}^{\infty} g(t)e^{-j2\pi ft} \, dt
```
:::

:::{hint} Transformation inverse
```{math}
:label: InvFT
g(t) = \int_{-\infty}^{\infty} G(f)e^{j2\pi ft} \, df
```
:::


Propriétés :

 
- **homogénéité** de la transformée de Fourier stipule que la transformée de Fourier d'un signal multiplié par une constante scalaire est égale à la transformée de Fourier du signal, également multiplié par cette constante. Si $g(t)$ est un signal avec $g(t) \iff G(f)$ et $a$ est une constante scalaire, :
$$
\mathcal{F}\{a \cdot g(t)\} = a \cdot \mathcal{F}\{g(t)\}= aG(f)
$$
Cela montre que l'échelle d'amplitude dans le domaine temporel est directement reflétée dans le domaine fréquentiel.


- **superposition** de la transformée de Fourier découle directement de la linéarité. Si un signal $g(t)$ est composé de plusieurs composantes, telles que $g(t) = g_1(t) + g_2(t) + \cdots +g _n(t)$, avec $g_i(t) \iff G_i(f)$, $i \in \{1,2,\ldots, n\}$  sa transformée de Fourier est donnée par :
$$\mathcal{F}\{g(t)\} = \mathcal{F}\{g_1(t)\} + \mathcal{F}\{g_2(t)\} + \cdots + \mathcal{F}\{g_n(t)\} =\sum_{i=1}^nG_i(f).
$$




L'homogénéité et la superposition garantissent **la linéarité** de la transformée de Fourier, permettant ainsi que la transformée d'une combinaison linéaire de signaux, soit égale à la même combinaison linéaire, de leurs transformées respectives.  La linéarité est fondamentale en analyse de Fourier, car elles permettent de décomposer des signaux complexes en une somme de signaux plus simples.  



 
**Attention:** La transformée de Fourier exprime la composition
fréquentielle d’un signal par une fonction de densité. Ce concept est essentiel, car nous utiliserons la transformation de Fourier pour calculer la largeur de bande d'un signal. 

## Propriétés d’un signal 

 


### Valeur moyenne

:::{hint} Valeur moyenne d’un signal non périodiques
La **valeur moyenne  d’un signal complexé non périodique**, $g(t)$,   est $\overline{g(t)}$ ou  
```{math}
:label:energy
\overline{g(t)} = \lim_{T \to \infty} \frac{1}{T} \int_{-T/2}^{T/2} g(t) \, dt \hspace{1cm}  \textrm{Volts}
```
:::

:::{hint} Valeur moyenne d’un signal périodique
La **valeur moyenne  d’un signal complexé périodique**, $g_P(t)$  avec
une période de $T_0$,   est $\overline{g_P(t)}$ est obtenue par    
```{math}
:label:energy
\overline{g_P(t)} =   \frac{1}{T_0} \int_{-T_0/2}^{T_0/2} g_P(t) \, dt \hspace{1cm}  \textrm{Volts}
```
:::

:::{warning} Attention
Concernant la valeur moyenne la linéarité s’applique
$$\overline{g_1(t)+g_2(t)}=\overline{g_1(t)}+\overline{g_2(t).} $$
:::





 

### Énergie

:::{hint} Énergie
L’**énergie d’un signal complexé**, $g(t)$,   est $E_g$ ou  
```{math}
:label:energy
E_g = \int_{-\infty}^{\infty} |g(t)|^2 dt  \hspace{1cm}  \textrm{Joules}
```
:::


Notez que, selon le **théorème de Parseval**  
$$\int_{-\infty}^{\infty} |g(t)|^2 \, dt = \int_{-\infty}^{\infty} |G(f)|^2 \, df$$


 
 

### Puissance
:::{hint} Puissance d’un signal non périodiques
La **puissance d’un signal non périodique**, $g(t)$,
est définie par :
```{math}
:label:power
P_g = \lim_{T \to \infty} \frac{1}{T} \int_{-T/2}^{T/2} |g(t)|^2 \ dt    \hspace{1cm} \textrm{Watts}
```
:::

 
:::{hint} Puissance d’un signal périodique
La **puissance d’un signal périodique**, $g_P(t)$ avec
une période de $T_0$ , est définie par 
```{math}
:label:power
 P_g =  \frac{1}{T} \int_{-T_0/2}^{T_0/2} |g_P(t)|^2 \ dt    \hspace{1cm} \textrm{Watts}
```
:::

 Notez que $P_g=\overline{|{g(t)}|^2}$.

:::{warning} Attention
Conversions d’unités 
$$   [10 \times \log_{10}(P_g)] \, \text{dBW ou } [30 + 10 \times \log_{10}(P_g)] \, \text{dBm}$$
:::




### Tension efficace
:::{hint} Tension efficace
La **tension efficace** (*root mean square*; RMS) d’un
signal périodiques  $g_P(t)$ est définie par
```{math}
:label:power
    RMS_g=   \sqrt{P_g} =  \frac{1}{T} \int_{-T_0/2}^{T_0/2} |g_P(t)|^2 \ dt     \hspace{1cm} \textrm{Volts}
```
:::
:::{warning} Attention
Conversions d’unités 
$$   [20 \times \log_{10}( RMS_g)] \, \text{dBW ou } [30 + 20 \times \log_{10}( RMS_g)] \, \text{dBm}$$
:::


:::{note} Informations supplémentaires pour  Travail Pratique - 1
```{figure} images/circuit.png
:label: TP1
:align: center
Un circuit d'une seule source avec une résistance

```

 Étant donné un circuit dont la source génère $g(t)$, la puissance instantanée dissipée dans une résistance $R$ est calculée selon la formule 
```{math}
:label:power
 P_{inst} =\frac{ |g(t)|^2 }{R}    \hspace{1cm} \textrm{Watts}
```
et pour le cas normalise, $R=1$, on obtient $|g(t)|^2 $.  En classe, nous nous intéressons principalement aux cas normalisés.
:::

 



## Signaux utiles

### Impulsion de Dirac (*Dirac impulse*)
(def-Dirac)=
Définition: Impulsion de Dirac 
: L’**impulsion de Dirac** est un outil mathématique idéal utilisé pour modéliser une impulsion infiniment brève et intense, qui ne peut pas être réalisée exactement dans la réalité physique.
 ```{math}
:label:power
\delta(t) =
\begin{cases} 
+\infty, & \text{si } t = 0, \\
0, & \text{si } t \neq 0,
\end{cases}
\quad \text{et} \quad \int_{-\infty}^{\infty} \delta(t) \, dt = 1.
```

```{figure} images/dirac-t.png
:label: dirac-t
:align: center
Impulsion de Dirac (en domaine temporel).
```
 

Propriétés: 
 
- Multiplication par l'impulsion de Dirac 
$$    \phi(t)\delta(t-T) = \phi(T)\delta(t-T)$$

- Échantillonnage pour obtenir une seule valeur à $T$
$$\int_{-\infty}^{\infty} \phi(t)\delta(t-T) \, dt = \phi(T) $$ 

- La valeur moyenne, l’énergie et la puissance de l’impulsion de Dirac sont indéfinies

- La transformée de Fourier de $ \delta(t) $ est une fonction constante dans le domaine fréquentiel, donc $\delta(t) \iff 1$,  $\forall f$


```{figure} images/dirac-f.png
:label: dirac-f
:align: center
Impulsion de Dirac (en domaine fréquentiel).
```
 

### Train d'impulsions de Dirac (*Dirac impulse train*)
(def-sinc)=
Definition: Train d'impulsions de Dirac
: La fonction train d'impulsions de Dirac, notée $ \Delta_T(t) $, est définie comme une somme infinie d'impulsions de Dirac espacées de $T$ secondes : 
 ```{math}
:label:train
\Delta_T(t) = \sum_{n=-\infty}^{\infty} \delta(t - nT)
```
Propriétés: 
 
- La valeur moyenne :  $$\overline{ \Delta_T(t)} = \frac{1}{T}$$

- L’énergie : infinie

- La  puissance :  $$P_D = \frac{1}{T}$$

- La transformée de Fourier : $$\mathcal{F}\{\Delta_T(t)\} = \frac{1}{T} \sum_{k=-\infty}^{\infty} \delta\left(f - k\frac{1}{T}\right)$$



### Fonction sinc (*Sinc function*)
(def-sinc)=
Definition: Fonction sinc 
: La fonction $\textit{sinc}(t)$ est définie comme suit
 ```{math}
:label:sinc
x(t) = \text{sinc}(t) =
\begin{cases}
\frac{\sin(t)}{ t}, & \text{si } t \neq 0, \\
1, & \text{si } t = 0.
\end{cases}
```
```{figure} images/sinc-t.png
:label: sinc-t
:align: center
Fonction sinc  (en domaine temporel).
```
Propriétés: 
 
- La valeur moyenne :  $$\overline{x(t)}  = \frac{1}{2T} \int_{-T}^{T} \text{sinc}(t) \, dt,$$ et converge vers zéro lorsque \( T \to \infty \).

- L’énergie :  $$E_x = \int_{-T}^{T} |\text{sinc}(t)|^2 \, dt,$$ qui augmente indéfiniment lorsque $T \to \infty $.

- La  puissance :  $$P_x = \lim_{T \to \infty} \frac{1}{2T} \int_{-T}^{T} |\text{sinc}(t)|^2 \, dt = 0.$$

- La transformée de Fourier : $$\mathcal{F}\{\text{sinc}(t)\} = 
\begin{cases}
1, & \text{si } |f| \leq \frac{1}{2}, \\
0, & \text{sinon}.
\end{cases}$$
```{figure} images/sinc-f.png
:label: sinc-f
:align: center
Fonction sinc  (en domaine fréquentiel).
```

 

### L’onde rectangulaire (*Rectangular pulse*)
(def-rec)=
Définition: La fonction rectangulaire
: La fonction rectangulaire $ \text{rect}(t) $, définie sur l'intervalle  $ [-T_0/2, T_0/2] $ , avec une valeur constante  $  a  $ , est donnée par :
 ```{math}
:label:rect
g(t) =
\begin{cases}
a, & \text{si } -\frac{T_0}{2} \leq t \leq \frac{T_0}{2}, \\
0, & \text{sinon}.
\end{cases}
```
```{figure} images/rect-t.png
:label: rect-t
:align: center
Onde rectangulaire  (en domaine fréquentiel).
```

Propriétés: 
 
- La valeur moyenne :  $$\overline{g(t)} = \frac{1}{T_0} \int_{-T_0/2}^{T_0/2} g(t) \, dt = \frac{1}{T_0} \int_{-T_0/2}^{T_0/2} a \, dt = a. $$

- L’énergie : $$E = \int_{-\infty}^{\infty} |g(t)|^2 \, dt = \int_{-T_0/2}^{T_0/2} a^2 \, dt = a^2 T_0.$$

- La  puissance : $$P = \lim_{T \to \infty} \frac{1}{T} \int_{-T_0/2}^{T_0/2} |g(t)|^2 \, dt = \frac{1}{T_0} \int_{-T_0/2}^{T_0/2} a^2 \, dt = a^2.$$

- La transformée de Fourier : $$ G(f) = \mathcal{F}\{g(t)\}  = a T_0 \text{sinc}(\pi f T_0).$$
```{figure} images/rect-f.png
:label: rect-f
:align: center
Onde rectangulaire  (en domaine temporel).
```



 

### Ondes porteuses  (*Carrier waveforms*)
(def-carriers)=
Définition: Ondes porteuses
: La majorité des systèmes de communication utilisent les formes d’onde
cosinus et sinus comme ondes porteuses. Leur fréquence fondamentale est
appelée la fréquence porteuse.

Un cosinus avec fréquence $f_p $ et amplitude $A_p$ est défini comme $c(t) = A_p \cos(2\pi f_p t + \phi)$ où
où :   

   - $A_p$ est l'amplitude,

   -  $f_p$ est la fréquence en Hertz,

   - $\phi$ est la phase initiale (en radians),

   -  $t$ est le temps.

Propriétés: 
 
- La valeur moyenne :  $$\overline{c(t)} = \frac{1}{T} \int_{0}^{T} A_p \cos(2\pi f_p t + \phi) \, dt = 0 $$

- L’énergie : infinie

- La  puissance : $$P_c = \lim_{T \to \infty} \frac{1}{T} \int_{0}^{T} |c(t)|^2 \, dt = \frac{A_p^2}{2}$$

- La transformée de Fourier : $$C(f) = \mathcal{F}\{c(t)\} = \frac{A_p}{2} \exp(j\phi ) \delta(f - f_p) + \frac{A_p}{2} \exp(-j \phi)  \delta(f + f_p),$$


Pour un sinus avec  les mêmes paramètres   $s(t) = A_p \sin(2\pi f_p t + \phi)$  

Propriétés: 
  
-  La valeur moyenne : 0
 
- L’énergie : infinie

- La  puissance :  $$P_s =   \frac{A_p^2}{2}$$

- La transformée de Fourier : $$S(f) = \mathcal{F}\{s(t)\} = \frac{A_p}{2j} \exp(j\phi ) \delta(f - f_p) -  \frac{A_p}{2j} \exp(-j \phi)  \delta(f + f_p),$$


## Systèmes


(def-system)=
Définition: Système
: Du point de vue d'un ingénieur en communication, un **système** est une loi qui attribue des signaux de sortie à divers signaux d'entrée.  
Le point le plus important dans la définition d'un système est que sa sortie doit être définie de manière unique pour toute entrée légitime.
Chaque
système possède donc **une entrée** ($x(t)$) **une sortie** $(y(t))$ et **une fonction de
transfert** $\left(\mathcal{T(\cdot)}\right)$, ou $y(t)=\mathcal{T}(x(t))$.

```{figure} images/system-gen.png
:label: system1
:align: center
Représentation d`un système

```

:::{important} Exemple pratique
Un circuit électrique avec une source de tension en entrée et un courant dans une certaine branche est un système.
:::
 


**Définition:** La **largeur de bande** correspond à l’étendue des
fréquences disponibles pour la transmission d’un signal. La bande
passante d’un signal est une mesure de l’étendue de fréquences contenues
dans le signal. En termes simples, elle représente la différence entre
les fréquences les plus élevées et les plus basses et significatives dans
le spectre du signal.

Si $|G(f)|^2$ représente la densité spectrale de puissance du signal, la
largeur de bande, $B$ est définie comme l’étendue de fréquences $f$ pour
lesquelles $|G(f)|^2$ est significatif (généralement au-dessus d’un
certain seuil, comme 3 dB en dessous de la valeur maximale). Le critère
de sélection $B$ dépend de la tolérance d’erreur dans une application
particulière. Nous pouvons par exemple choisir $B$ comme étant la
largeur de bande qui contient 95% de l’énergie du signal.

**Attention :** La largeur de bande doit toujours être définie
uniquement pour les fréquences positives.

**Attention:** Dans le contexte des systèmes de communication, nous nous
intéressons plus particulièrement à la puissance et à la largeur de
bande des signaux.


