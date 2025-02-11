---

exports:
  - format: pdf
    template: plain_latex
    output: ./exports/section4.pdf
downloads:
  - file: ./exports/section4.pdf
    title: PDF
title: Section 4 - Procédures de transmission 
abstract: |
  Section 4 présente les principales techniques de modulation essentielles pour l’adaptation des signaux aux caractéristiques du canal de transmission. Elle commence par la modulation d’amplitude, qui consiste à faire varier l’amplitude de l’onde porteuse en fonction du signal modulant, incluant des variantes telles que la modulation à double bande latérale (DSB), la modulation à bande latérale unique (SSB)  et la modulation d’amplitude en quadrature (QAM). Ensuite, la section aborde la modulation d’angle, qui regroupe la modulation de fréquence (FM) et la modulation de phase (PM), deux techniques qui modifient respectivement la fréquence et la phase de la porteuse pour améliorer la robustesse aux interférences et aux distorsions. Enfin, la section explore les principes de la modulation numérique, où l’information est transmise sous forme de symboles discrets, englobant des schémas tels que ASK (Amplitude Shift Keying), PSK (Phase Shift Keying) et QAM numérique. L’objectif **O4** est de proposer les techniques de modulation les plus adaptées en fonction des caractéristiques du canal et du type d’information à transmettre, en mettant en lumière leurs avantages et leurs contraintes dans divers contextes de communication.

---

 


## Procédures de transmission

La modulation est une étape essentielle des procédures de transmission dans les systèmes de communication modernes. Elle permet d’adapter le signal aux caractéristiques du canal, d'améliorer la qualité de transmission et d’optimiser l’utilisation du spectre. Différents types de modulation sont utilisés en fonction des besoins et des contraintes spécifiques de la transmission, qu'elle soit analogique ou numérique.
 

(def-Modulation)=
Définition: Modulation 
: La **modulation** est une procédure de transmission qui consiste à superposer un signal d'information our une onde porteuse, $c(t)$, ou un train d'impulsions composé de $p(t)$, afin de permettre son acheminement à travers un canal de communication. Elle est indispensable pour configurer l'utilisation du spectre, réduire les interférences et adapter le signal aux caractéristiques du support de transmission. 


(def-Message)=
Définition: Signal de message   
: Le **signal de message**, $m(t)$, représente l’information avant toute modification ou modulation. Il peut être analogique  (continu dans le temps et en amplitude, comme la musique) ou numérique (discret en amplitude et en temps, comme des données binaires). Le signal $m(t)$  est souvent en bande de base (i.e. ses composantes fréquentielles sont centrées autour de $0$ Hz) avec une largeur de bande de $B$ Hz.  

 ```{figure} images/sec4-message.png
:label: sec4-message
:align: center
Un signal de message en bande de base avec une largeur de bande de $B$ Hz.  
```
:::{warning} Attention
Lorsque les signaux des messages sont aléatoires, nous devons utiliser leur spectre de densité de puissance, $S_m(f)$, pour déterminer sa largeur de bande. 
:::

La modulation peut être réalisée en utilisant soit une onde porteuse, soit un train d'impulsions.

(def-OndePorteuse)=
Définition: Onde Porteuse   
:  Une **onde porteuse** (*carrier waveform*), $c(t)$ (e.g.  $\cos(2\pi f_p t)$), est un signal sinusoïdal de fréquence $f_p$ utilisé en modulation pour transporter un signal de message en modifiant son amplitude, sa fréquence ou sa phase. **L'amplitude**, la **phase** ou la **fréquence** de la forme d'onde porteuse est modifiée en fonction du signal du message, $m(t)$, avec une largeur de bande $B$. La fréquence de la porteuse doit être choisie  plus grande que la largeur de bande, $$f_p > B$$

  
```{figure} images/sec4-DSB-SC.png
:label: sec4-message
:align: center 
Un signal de message et l'onde porteuse. Le signal modulé est $m(t)c(t)$. (Voir: Exemples Intéractifs: Procédures de transmission - Modulation DSB-SC)
```
 
(def-TrainImpulse)= 
Définition: Train d’impulsions 
:  Il est également possible de transmettre des signaux sans utiliser une porteuse haute fréquence. Dans ce cas, un **train d'impulsions** est nécessaire;
$$
\sum_{n=-\infty}^{\infty} p(t - nT_s)
$$
 Notez que la période du train d'impulsions est notée $ T_s $, et elle sera utilisée pour représenter la période du symbole. 





### Catégories de modulation
Les types de modulation peuvent être classés en fonction de la nature du signal de message. Si le signal de message  est **continu dans le temps et en amplitude**, le système est appelé modulation analogique. En revanche, si le message **discret en amplitude et en temps**, il est qualifié de modulation numérique.

Les types de modulation peuvent également être classés en fonction de la présence d’une fréquence porteuse. 
La transmission en **bande de base** signifie que le signal est envoyé directement sans être transposé sur une fréquence porteuse. Cette technique est généralement utilisée pour les transmissions sur des distances courtes, comme les réseaux informatiques ou certaines applications industrielles. Contrairement à la bande de base, **la transmission par onde porteuse** repose sur une porteuse haute fréquence $f_p$, ce qui permet d’envoyer les signaux sur de longues distances et d’optimiser l’utilisation du spectre.


```{table} Catégories de modulation
:name: tab-categories-modulation
:align: center
| **Catégories de modulation** | **Transmission en bande de base (avec train d'impulsion)** | **Transmission par onde porteuse** |
|------------------------------|----------------------------------|----------------------------------|
| **Analogique**               | **Modulation d’amplitude** : « PAM : Pulse Amplitude Modulation »  <br> **Modulation de durée** : « PWM : Pulse Width Modulation » <br> **Modulation de position** : « PPM : Pulse Position Modulation » | **Modulation linéaire (Modulation d’amplitude)** : « AM : Amplitude Modulation » et ses variations <br> **Modulation d’angle** : « PM : Phase Modulation » <br> « FM : Frequency Modulation » |
| **Numérique**                | **Modulation par impulsions codées** : « PCM : Pulse Code Modulation » <br> **Codage de ligne** : « Line coding » | **Modulations binaires** : « FSK : Frequency Shift Keying » <br> « BPSK : Binary Phase Shift Keying » <br> **Modulations multiniveaux (M)** : « QPSK : Quadrature Phase Shift Keying » <br> « M-FSK : Frequency Shift Keying » <br> « M-QAM : M-ary Quadrature AM » <br> « M-PSK : M-ary Phase Shift Keying » |
```
 

### Critères de performance des techniques de modulation

Les deux critères de performance sont l'efficacité énergétique et l'efficacité spectrale. 

(def-EE)= 
Définition: L’efficacité énergétique
:  **L'efficacité énergétique** (*energy efficiency*) est l'énergie (puissance) du signal de message divisée par l'énergie (puissance) du signal modulé 
$$
\eta_{\textrm{efficacité-énergétique}} = \frac{\textrm{Puissance utile}}{\textrm{Puissamce totale}}= \frac{E[ | m(t) |^2 ]}{E[ | \varphi(t) |^2 ]}
$$
L’efficacité énergétique mesure de la capabilité d’un système à utiliser efficacement l’énergie pour transmettre des signaux de message.  

(def-SE)= 
Définition: L’efficacité spectrale
: **L’efficacité spectrale** (*spectral efficiency*) mesure la quantité de signaux de message transmises par unité de largeur de bande. Pour les systèmes de modulation analogiques, elle est obtenue en divisant la largeur de bande du signal de message par la largeur de bande du signal modulé.  
$$
\eta_{\textrm{efficacité-spectrale}} = \frac{B}{\textrm{Largeur de bande de } \varphi(t)}
$$
Pour les systèmes de modulation numérique, nous le définirons comme le nombre de bits transmis par Hertz [bits/sec/Hz], qui change en fonction du type d'image et du type de modulation sélectionnés (plus de détails à venir). 

## Catégories de modulation par onde porteuse

La modulation par onde porteuse peut affecter **l’amplitude**, **la phase** ou **la fréquence** d’une onde porteuse pour transmettre un signal de message, qu’il soit **analogique** ou **numérique**. 

Le signal modulé, $\varphi(t)$, par une onde porteuse  est exprimée sous la forme 
$$
\varphi(t) = A(t) \cos(2\pi f_p(t) t + \phi(t))
$$
où  $A(t) $ représente l’**amplitude** du signal modulé, $ f_p (t)$ est la **fréquence porteuse** qui peut varier en temp, et  $ \phi(t)$ correspond à la **phase** du signal modulé.



Ci-dessous se trouve une explication de certains types de modulation: 
 

**1. Modulation d’amplitude analogique** (*Amplitude modulation - analog*)
- Le signal de message $ m(t) $ est **analogique**.
- L’amplitude de la porteuse $ A(t) $ varie en fonction de $ m(t) $.

**Types :**
-  Modulation à double bande latérale sans porteuse
**« DSB-SC : Double-sideband suppressed-carier »**
-  Modulation à double bande latérale
**« AM : Amplitude modulation »** 
-  Bande latérale unique
**« SSB : Single sideband »**
-  Modulation d'amplitude en quadrature (analogique)
**« QAM : Quadrature amplitude modulation»**



**2. Modulation d’angle analogique** (*Angle modulation - analog*)
Ce type de modulation concerne la phase ou la fréquence de la porteuse :
- Le signal de message $ m(t) $ est **analogique**.
- La phase $\phi(t) $ (ou la fréquence $ f_p(t)$) varie en fonction de  $m(t)$.

**Types :**
- Modulation de phase
**« PM : Phase modulation »** 
- Modulation de fréquence
**« FM : Frequency modulation »**




 **3. Modulation numérique**
Ce type de modulation s'applique aux signaux numériques :
- Le message $m(t)$ est **numérique** (valeurs discrètes, binaires ou multiniveaux).
- L’amplitude $A(t)$  **et/ou** la phase $ \phi(t)$ varient en fonction de $ m(t)$.

**Types :** 
- **« ASK : Amplitude Shift Keying »**  
- **« FSK : Frequency Shift Keying »**  
- **« PSK : Phase Shift Keying »** 
- **« QAM : Frequency Shift Keying »** 


 

 


###  Modulation d’amplitude (analogique) 

Les types de modulation d’amplitude analogique peuvent être classés en fonction de la manière dont l’information est transmise à travers l’onde porteuse. **La modulation à double bande latérale sans porteuse** (*Double-Sideband Suppressed-Carrier*; DSB-SC) supprime la composante continue de l’onde porteuse pour améliorer l’efficacité énergétique et spectrale. **La modulation à double bande latérale** (*Amplitude Modulation*; AM), quant à elle, transmet l’information en modulant l’amplitude d’une onde porteuse et en ajoutant une petite partie de la porteuse tout en deux bandes latérales. **La modulation à bande latérale unique** (*Single Sideband*; SSB) optimise encore plus l’utilisation du spectre en supprimant l’une des deux bandes latérales, réduisant ainsi la largeur de bande requise. Enfin, **la modulation d’amplitude en quadrature** (*Quadrature Amplitude Modulation*; QAM) combine deux signaux modulés en amplitude, déphasés de 90°, permettant ainsi une transmission plus efficace de l’information analogique avec une meilleure utilisation du spectre.  Les détails de ces types de modulations analogiques sont expliqués ci-dessous.

### Modulation à double bande latérale porteuse supprimée (DSB-SC)

Modulation à double bande latérale porteuse supprimée (*double sideband suppressed carrier*; DSB-SC)  implique la multiplication du signal du message, ($m(t)$ limité à une bande de fréquence de $B$ Hz), une porteuse (onde sinusoïdale) de fréquence $ f_p $, notée $ c(t)= \cos(2\pi f_p t)$.

- **Modulation**  

Le signal modulé $ \varphi_{DSB-SC}(t)$ est donné par :
   $$
   \varphi_{DSB-SC}(t) = m(t) \cos(2\pi f_p t)
   $$
Ce signal ne contient plus la porteuse mais uniquement les bandes latérales.

En transformée de Fourier, le spectre du signal modulé est :
   $$
   \Phi_{DSB-SC}(f) = \frac{1}{2} \left[ M(f + f_p) + M(f - f_p) \right]
   $$
   Cela montre que le spectre du signal est déplacé autour de $ \pm f_p $. 





```{figure} images/sec4-DSB-mod.png
:label: sec4-DSB-mod
:align: center 
Schéma de la modulation DSB-SC, où le signal $ m(t) $ est multiplié par une porteuse $ \cos(2\pi f_p t) $, déplaçant ainsi son spectre autour de $ \pm f_p $.
```




```{figure} images/sec4-envelope.png
:label: sec4-envelope
:align: center 
Une illustration de la modulation DSB-SC, où le signal $m(t) $ module la porteuse $\cos(2\pi f_p t)$ , pour générer  $\varphi_{DSB-SC}(t) = m(t) \cos(2\pi f_p t) $. 
```

 
- **Efficacité énergétique** 

 


L’efficacité énergétique est définie comme le rapport entre la puissance moyenne du signal message $ m(t) $ et celle du signal modulé $\varphi_{DSB-SC}(t) $. Dans le cas de la modulation **DSB-SC**, la puissance moyenne du signal modulé est :
$$
E[|\varphi_{DSB-SC}(t)|^2] = \frac{1}{2} E[|m(t)|^2]
$$

Donc, l’efficacité énergétique de la modulation DSB-SC est :
$$
\eta_{\text{efficacité-énergétique-DSB-SC}} = \frac{E[|m(t)|^2]}{E[|\varphi_{DSB-SC}(t)|^2]} = \frac{E[|m(t)|^2]}{\frac{1}{2} E[|m(t)|^2]} = 2
$$

Cela signifie que 50\% de la puissance du signal modulé est contenue dans le signal message $ m(t) $. La porteuse est supprimée (car il l y a pas une composante en $ f_p = 0 $), ce qui améliore l’efficacité énergétique du signal transmis. 

 

- **Efficacité spectrale**

Le spectre du signal modulé contient deux bandes latérales, ce qui double la largeur de bande du signal modulé par rapport au signal message, 
$$
\text{Largeur de bande de } \varphi_{DSB-SC}(t) = 2B
$$

Ainsi, l’efficacité spectrale de la modulation DSB-SC est :
$$
\eta_{\text{efficacité-spectrale-DSB-SC}} = \frac{B}{\text{Largeur de bande de } \varphi_{DSB-SC}(t)} = \frac{B}{2B} = \frac{1}{2}
$$

Cela signifie que seulement **50\%** de la largeur de bande du signal modulé est effectivement utilisée pour transmettre l’information.

```{figure} images/sec4-DSB-spectre.png
:label: sec4-DSB-spectre
:align: center 
L'image à gauche représente le spectre du signal de message $m(t)$. L'image à droite représente le spectre du signal après modulation DSB-SC. Les deux bandes latérales sont identiques et contiennent chacune la moitié de la puissance du signal d'origine, car   $ \Phi_{DSB-SC}(f) = \frac{1}{2} \left[ M(f + f_p) + M(f - f_p) \right]$.
 
```

- **Démodulation cohérente (synchrone)**


Le signal modulé reçu est filtré par un **filtre passe-bande**, qui réduit la puissance du bruit et ne laisse passer que les fréquences entre $ f_p - B $ et $ f_p + B $.  

Dans le cas idéal, Le filtre a une **réponse en fréquence** donnée par :
 $$
  H(f) =
  \begin{cases} 
  1, & f_p - B \leq |f| \leq f_p + B \\
  0, & \text{ailleurs}
  \end{cases}
$$

Le signal filtré est multiplié par une **porteuse locale** au récepteur :  
$$
  \cos(2\pi f_p t + \theta)
$$  
 La porteuse générée peut **ne pas être parfaitement alignée** avec celle de l'émetteur, ce qui introduit un décalage de phase $ \theta $ (**problème de synchronisation**).  

Après la multiplication avec la porteuse locale, le signal passe dans un **filtre passe-bas** avec une **fréquence de coupure $ f_0 \geq B$, et gain de **2** , qui supprime les hautes fréquences et ne conserve que la composante basse fréquence du signal.   



```{figure} images/sec4-DSB-demod.png
:label: sec4-DSB-demod
:align: center 
Schéma de la démodulation cohérente d'un signal DSB-SC. Un filtre passe-bande réduit le bruit avant la multiplication avec une porteuse locale. Un filtre passe-bas extrait ensuite le signal message, avec un effet de synchronisation dépendant du décalage de phase $\theta$.
``` 
:::{warning} Effet de la synchronisation 
  - **Idéalement**, $ \theta = 0 $ et le signal récupéré est **exactement \( m(t) \)**.
  - **En pratique**, $ \theta \neq 0 $, ce qui entraîne une atténuation proportionnelle à $ \cos(\theta)  \leq 1 $.  
:::









###  Modulation à double bande latérale (*Amplitude Modulation*; AM)

- **Modulation**  

Le signal de message $m(t)$ et l'onde porteuse $ \cos(2\pi f_p t)$ sont combinés pour former :  
$$ 
\varphi_{AM}(t) = [A + m(t)] \cos(2\pi f_p t)
$$  
Le terme $ A $ est un gain choisi pour garantir que $ A + m(t) \geq 0 $, évitant ainsi toute **inversion de phase** (pour détecteur d’enveloppe).   




Le spectre du signal modulé est :
   $$
   \Phi_{AM}(f) = \frac{1}{2} \left[ M(f + f_p) + M(f - f_p) \right] +  \frac{A}{2} \left[ \delta(f + f_p) +\delta(f - f_p) \right] 
   $$
Cela montre que le spectre du signal est déplacé autour de $ \pm f_p $, et  contient une composante en fréquence $f_p$​ correspondant à la porteuse.

(def-SE)= 
Définition: Indice de modulation (*Modulation index*)
: **Indice de modulation**,  $ \mu $ est défini  par :  
 $$
     \mu = \frac{m_p}{A}
$$
Il représente le rapport entre l’amplitude maximale du signal message $ m_p $  et l’amplitude de la porteuse $ A $.  


```{figure} images/sec4-AM-mod.png
:label: sec4-AM-mod
:align: center 
Schéma du processus de modulation d’amplitude (AM), où le signal de message $m(t)$ module l’amplitude d’une porteuse $ \cos(2\pi f_p t)$ , en ajoutant un terme constant $A$ pour éviter toute inversion de phase.
```

```{figure} images/sec4-spectre-AM.png
:label: sec4-spectre-AM
:align: center 
Représentation fréquentielle du signal AM. Le spectre du signal de message $M(f)$, initialement centré autour de 0 Hz, est déplacé autour de $ \pm f_p $. ​ après modulation, incluant une composante $  f_p $. ​ correspondant à la porteuse et une largeur de bande totale de $2B$.
```








- **Efficacité énergétique** 


L'efficacité énergétique est définie comme le rapport entre la puissance moyenne du signal message $m(t)$et celle du signal modulé $\varphi_{AM}(t) $.  
$$
\eta_{\text{efficacité-énergétique-AM}} = \frac{E[|m(t)|^2]}{E[|\varphi_{AM}(t)|^2]}
$$

D'après la puissance moyenne du signal AM donnée :
$$
E[|\varphi_{AM}(t)|^2] = \frac{1}{2} A^2 + \frac{1}{2} E[|m(t)|^2]
$$

L'efficacité énergétique devient donc :
$$
\eta_{\text{efficacité-énergétique-AM}} = \frac{E[|m(t)|^2]}{\frac{1}{2} A^2 + \frac{1}{2} E[|m(t)|^2]}
$$

En factorisant $ E[|m(t)|^2] $:
$$
\eta_{\text{efficacité-énergétique-AM}} = \frac{2 \mu^2}{1 + \mu^2}
$$
où $ \mu = \frac{m_p}{A} $ est l'indice de modulation.



:::{note} Exemple  illustratif :  **Travail pratique - 3**
 
Un signal AM est observé à l'aide d'un analyseur de spectre avec une impédance d'entrée de  50Ω.  La porteuse a une fréquence de $f_p = 1 $ MHz, et les bandes latérales sont espacées de 2,5 kHz. L'affaiblissement des bandes latérales par rapport à la porteuse est de 12 dB.  

Déterminez l’indice de modulation $\mu $ du signal AM.  

%**Réponse  : ** \( \mu = 0.5 \), Efficacité énergétique **11\ %**.
```{figure} images/sec4-TP3.png
:label: sec4-TP3
:align: center 
Le spectre d’un signal AM. Notez que seules les fréquences positives sont visibles sur un oscilloscope.
```


**Réponse :**  On observe une différence de puissance de **12 dB** entre la porteuse et les bandes latérales. En utilisant la relation logarithmique entre ces puissances :
$$
12 \text{ dB} = 10 \log \left( \frac{4}{m^2} \right)
$$
En résolvant cette équation, on obtient :
$$
m = \frac{A_m}{A_p} = 0.5
$$

L’efficacité énergétique,  est donnée par :
$$
\eta = \frac{2m^2}{4 + 2m^2}  = \frac{2(0.5)^2}{4 + 2(0.5)^2} = \frac{0.5}{4.5} \approx 11\%
$$ 
:::


- **Efficacité spectrale**

L'efficacité spectrale du signal AM est :
$$
\eta_{\text{efficacité-spectrale-AM}} = \frac{B}{2B} = \frac{1}{2}
$$
 


- **Démodulation non cohérente : Détecteur d’enveloppe** (*Envelope detector*)

 
L’**enveloppe** d’un signal AM représente l’amplitude instantanée du signal modulé. Pour un signal AM donné par :  
$$
\varphi_{AM}(t) = [A + m(t)] \cos(2\pi f_p t)
$$
l’enveloppe est définie par :  
$$
E(t) = A + m(t)
$$
Elle suit l’évolution du signal de message $ m(t) $, assurant ainsi que l’information est préservée dans la modulation.
Le **détecteur d’enveloppe** permet d’extraire cette enveloppe à partir du signal modulé. Il est généralement constitué de :
1.  Un redresseur (diode) qui élimine la partie négative du signal.
2.  Un circuit RC (résistance-capacité) qui agit comme un filtre passe-bas pour lisser les variations de la porteuse et récupérer l’enveloppe $ E(t)$.



```{figure} images/sec4-Env-circuit.png
:label: sec4-Env-circuit
:align: center 
Schéma d’un détecteur d’enveloppe utilisé pour la démodulation AM. Le circuit est composé d’une diode pour redresser le signal, d’un condensateur CC pour stocker la charge et d’une résistance RR qui détermine la constante de temps RC, permettant de lisser l’enveloppe du signal modulé.
```

 
```{figure} images/sec4-Env-RC.png
:label: sec4-Env-RC
:align: center 
Illustration du fonctionnement du détecteur d’enveloppe pour un signal AM. L’entrée du détecteur est un signal AM (courbe noire). La courbe bleue représente une extraction correcte de l’enveloppe. Une mauvaise constante de temps RC peut soit ralentir la détection (courbe rouge supérieure) soit causer une distorsion (courbe rouge inférieure).
```

 
Pour que le détecteur d'enveloppe fonctionne correctement, deux conditions doivent être respectées :  
1.  Il faut que **l’amplitude instantanée du signal modulé ne devienne jamais négative** pour éviter toute **inversion de phase**.  La condition mathématique est :  
  $$
     A + m(t) \geq 0, \quad \forall t
     $$
Cela impose que $    0 \leq \mu \leq 1$
 
2. La fréquence du signal message $ B $ doit être **beaucoup plus petite** que la fréquence porteuse $ f_p$ :  
$$
     B \ll f_p
$$
 Cela garantit que l’enveloppe varie lentement par rapport aux oscillations rapides de la porteuse.
 

:::{note} Exemple  illustratif :  **L'indice de modulation** et démodulation
Illustration de l'effet de l'indice de modulation $\mu $ en modulation d'amplitude (AM).
```{figure} images/sec4-mod-index.png
:label: sec4-mod-index
:align: center 
Chaque signal représente une onde modulée en amplitude pour différentes valeurs de $\mu $, allant de 0.2 à 1. Lorsque $\mu $ augmente, l'amplitude de l'onde modulée varie davantage, influençant l'enveloppe du signal. À $\mu = 1 $, l'enveloppe atteint zéro à certains instants, ce qui correspond à une modulation à $100\%$.
```

 

La **surmodulation** (*overmodulation*) en modulation d'amplitude (AM) se produit lorsque $\mu > 1 $. Cela signifie que l'amplitude du signal message $ m(t) $ devient supérieure à celle de la porteuse$ A $, entraînant une **inversion de phase** dans l'onde modulée.  

Ce phénomène provoque une distorsion du signal, rendant difficile voire impossible sa démodulation correcte, en particulier avec un démodulateur à enveloppe. Pour éviter la surmodulation et assurer une transmission fidèle du signal, il est recommandé de maintenir $\mu \leq 1 $.


```{figure} images/sec4-surmodulation.png
:label: sec4-surmodulation
:align: center 
Illustration de la surmodulation $ \mu = 1.5 $ en modulation d'amplitude (AM). Lorsque l'indice de modulation dépasse 1, l'enveloppe du signal devient déformée et présente des **inversions de phase**, ce qui entraîne des distorsions non désirées et rend la démodulation plus complexe.  
```
:::


 
 

- **Démodulation cohérente (synchrone)**


```{figure} images/sec4-AM-Demod-Coh.png
:label: sec4-AM-Demod-Coh
:align: center 
Schéma d’un démodulateur cohérente  La figure illustre le principe de la  démodulation cohérente d'un signal AM en utilisant une  PLL (*phase locked  loop*). Cette méthode permet de récupérer avec précision le signal de message $ m(t)$ à partir du signal modulé, en synchronisant une porteuse locale avec celle du signal reçu.
```



Le signal modulé en entrée est donné par $ \varphi_{AM}(t) = [A + m(t)] \cos(2\pi f_p t) $. L'objectif est d'extraire uniquement $ m(t) $en éliminant la porteuse. Pour cela, le signal entre d’abord dans un **mélangeur** (*mixer*), qui effectue une multiplication avec un signal de référence $ \cos(2\pi f_p t) $. Cette opération produit deux termes : une **composante basse fréquence** correspondant à l’enveloppe $ A + m(t) $ et une **composante haute fréquence** centrée autour de $ 2f_p $.



Pour isoler le signal utile, un **filtre passe-bas** est appliqué après le mélangeur. Ce filtre élimine les hautes fréquences et ne conserve que la composante basse fréquence, soit $ A + m(t) $. Notez que, à  ce stade, bien que l’information du message soit récupérée, une erreur de phase pourrait perturber la démodulation si la porteuse locale utilisée dans le mélangeur n’est pas parfaitement synchronisée avec celle du signal reçu.

C’est à ce niveau qu’intervient la PLL (*Phase Lock Loop*). Ce circuit ajuste dynamiquement la fréquence et la phase de la porteuse locale pour s’assurer qu’elle est **en parfaite synchronisation** avec la porteuse du signal reçu. En maintenant cet alignement, la PLL permet d’éviter les erreurs de phase qui pourraient altérer la restitution du signal de message.

Finalement, à la sortie du filtre, on obtient $ A + m(t)$ , qui peut être traité pour supprimer la constante $  A $ , généralement via un **filtre passe-haut**. Cette dernière étape permet d’obtenir uniquement le signal $  m(t)$ , qui est la réplique exacte du signal de message initialement modulé à l’émission. Ainsi, grâce à cette méthode cohérente, la démodulation est réalisée avec une précision élevée, rendant cette approche particulièrement utile dans les communications nécessitant une forte immunité aux distorsions et aux interférences.


:::{important} Exemple pratique : 

```{figure} images/Sec4-RadioAM.png
:label: Sec4-RadioAM
:align: center 
Évolution de la bande de fréquences AM au Québec et au Canada. La bande AM, initialement comprise entre **535 kHz et 1605 kHz**, a été étendue jusqu'à **1705 kHz**, passant de 107 à 117 canaux de **10 kHz** chacun. Cette extension permet d’accueillir de nouvelles stations et d’améliorer la répartition des fréquences pour la radiodiffusion.
```

 
 
Auparavant, la bande AM était définie entre **535 kHz et 1605 kHz**, divisée en **107 canaux de 10 kHz** chacun. Actuellement, cette bande a été étendue jusqu'à **1705 kHz**, offrant désormais **117 canaux de 10 kHz**. Cette extension permet d’accueillir davantage de stations de radio et d’améliorer la disponibilité des fréquences pour la diffusion. 

L’illustration montre également une **représentation spectrale d’une station de radio AM**, où l’espacement entre les canaux est de **10 kHz**, ce qui correspond à la largeur de bande attribuée à chaque station. Étant donné que les signaux AM transmettent des fréquences audio allant jusqu'à **5 kHz**, chaque station doit occuper une bande de **10 kHz** (incluant la bande latérale supérieure et inférieure). 

Une indication est également donnée concernant l’**extension récente** de la bande AM, qui s’est élargie de **1605 kHz à 1705 kHz** pour accueillir des fréquences supplémentaires. Enfin, la figure précise que ces fréquences sont les mêmes aux **États-Unis**, soulignant une harmonisation des bandes de radiodiffusion en Amérique du Nord.
:::




Modulations efficaces du point au vue de la largeur de bande sont la Modulation à bande latérale unique (*single sideband*; SSB) et la modulation d'amplitude en quadrature (analogique)  (*quadrature amplitude modulation - analog*; QAM-Analogique). Elles sont décrites ci-dessous.  


###  Modulation à bande latérale unique (SSB)

 Dans une modulation AM classique, l’information transmise est redondante, car elle est contenue à la fois dans la **bande latérale supérieure** et la **bande latérale inférieure**. Il est donc possible d’envoyer le même message en utilisant **seulement une des deux bandes**, réduisant ainsi de moitié la largeur de bande nécessaire. 

 - **Modulation**  
```{figure} images/sec4-ssb-mod.png
:label: sec4-ssb-mod
:align: center 
 Illustration de la génération d’un signal **SSB (Single Sideband)** en utilisant la **méthode par déphasage**, qui permet de supprimer l’une des bandes latérales.
```
 



On utilise deux branches pour générer un signal modulé de SSB.    Dans la **première branche**, $m(t)$ est directement multiplié par la porteuse  $\cos(2\pi f_p t)$ pour obtenir 
$$
  s_1(t) = m(t) \cos(2\pi f_p t)
$$
 Dans la **deuxième branche**, le signal est d'abord transformé par un **filtre à déphasage** $ H(f)$, qui effectue un décalage de phase de  $ \frac{\pi}{2} $ (Transformée de Hilbert):
  $$
  s_2(t) = \hat{m}(t) = H(f) \cdot M(f) \quad \text{où} \quad H(f) = je^{-j\pi u(f)}
  $$
  Ce signal est ensuite multiplié par une **porteuse en quadrature** $ \sin(2\pi f_p t) $ :
  $$
  s_3(t) = \hat{m}(t) \sin(2\pi f_p t)
  $$

```{figure} images/sec4-hilbert.png
:label: sec4-hilbert
:align: center 
Représentation fréquentielle du filtre de Hilbert (déphasage) : la phase $\angle H(f) $ introduit un déphasage de $ \frac{\pi}{2} $  pour les fréquences positives et de $ -\frac{\pi}{2} $ pour les fréquences négatives, tandis que le module $|H(f)| $ reste constant à 1.
```


Finalement, les deux signaux obtenus sont combinés. Pour générer la **bande latérale supérieure** (*upper sideband*; USB), on effectue une addition :
$$
  \varphi_{SSB}^{USB}(t) = s_1(t) + s_3(t) = m(t) \cos(2\pi f_p t) + \hat{m}(t) \sin(2\pi f_p t)
$$
Pour générer la **bande latérale inférieure** (*lower sideband; LSB ), on effectue une soustraction :
$$
  \varphi_{SSB}^{LSB}(t) = s_1(t) - s_3(t) = m(t) \cos(2\pi f_p t) - \hat{m}(t) \sin(2\pi f_p t)
$$

L’expression en fréquence du signal SSB est obtenue en utilisant la transformée de Fourier :
- Pour la **USB**, le spectre est :
  $$
  \Phi_{SSB}^{USB}(f) = M(f - f_p) u(f - f_p)
  $$
- Pour la **BLI**, le spectre est :
  $$
  \Phi_{SSB}^{LSB}(f) = M(f + f_p) u(-f - f_p)
  $$


Grâce à cette approche, seule **une des bandes latérales est transmise**, ce qui permet de réduire **de moitié la largeur de bande** par rapport à une modulation AM conventionnelle. Cette technique est particulièrement utilisée dans les communications à bande limitée, comme la radio HF et certains systèmes de télécommunications analogiques avancés.




```{figure} images/sec4-ssb-spectre.png
:label: sec4-ssb-spectre
:align: center 
Représentation spectrale des différentes techniques de modulation en amplitude : (1) Signal modulant en bande de base, (2) Modulation à double bande latérale (DSB), (3) Modulation à bande latérale unique supérieure (SSB-USB), et (4) Modulation à bande latérale unique inférieure (SSB-LSB). La modulation SSB permet de réduire la largeur de bande nécessaire en ne transmettant qu'une seule bande latérale du spectre du signal modulé.
```



- **Efficacité énergétique** 

Pour SSB (modulation à bande latérale unique) efficacité énergétique est
     $$
     \eta_{\text{efficacité-énergétique-SSB}}^{SSB} = 1
     $$

- **Efficacité spectrale**  
La largeur de bande occupée est **\( B \)**, donc :
$$
     \eta_{\text{efficacité-spectrale-SSB}} = \frac{B}{B} = 1
$$

 

- **Démodulation cohérente (synchrone)**

```{figure} images/sec4-ssb-demod.png
:label: sec4-ssb-demod
:align: center 
Démodulation d'un signal à bande latérale unique avec une erreur de phase dans l'oscillateur local. Un filtre passe-bas est utilisé pour récupérer le signal modulant, mais une erreur de phase $ \theta $ peut causer une distorsion du signal démodulé.
```

 Signal d'entrée est $ \varphi_{SSB}(t)$ est le signal modulé en bande latérale unique qui arrive au récepteur. Il est multiplié par une porteuse locale $\cos(2\pi f_p t + \theta) $, où $ \theta$  représente une erreur de phase potentielle 
   $$
   x(t) = \varphi_{SSB}(t) \cos(2\pi f_p t + \theta)
$$

Le signal obtenu après multiplication (*mixing*) est noté $x(t) $, et il peut contenir des composantes en bande de base ainsi que du bruit. Un filtre passe-bas $H(f)$ est appliqué pour éliminer les composantes haute fréquence indésirables, conservant uniquement le signal souhaité, 
$$
v(t) = H(f) * x(t)
$$

Finalement, $ v(t)$ est le signal démodulé en bande de base, qui peut être affecté par l’erreur de phase $ \theta $, entraînant une distorsion du message.


###  Modulation d'amplitude en quadrature (analogique)  (QAM-Analogique)

La modulation d’amplitude en quadrature (QAM-Analogique),  permet la transmission simultanée de deux signaux distincts $m_1(t)$ et $m_2(t)$ en utilisant une onde  porteuses  avec deux phases (*inphase* et *quadrature*).

-  **Modulation**   

 
Nous avons **deux signaux messages** distincts, $ m_1(t)$ et $ m_2(t) $, chacun d'eux possède une largeur de bande de $ B $ Hz.  Dans le cas d'une modulation en quadrature (QAM), ces deux signaux peuvent être transmis **simultanément** en les associant à des porteuses orthogonales, comme un cosinus et un sinus à une fréquence porteuse $ f_p $. L’utilisation de deux signaux de largeur de bande $ B $ permet d’augmenter l’utilisation du spectre tout en assurant une séparation correcte des informations transmises.

 ```{figure} images/sec4-qam-mod.png
:label: sec4-qam-mod
:align: center 
La modulation d’amplitude en quadrature (QAM-Analogique) permettant la transmission simultanée de deux signaux $m_1(t)$ et $m_2(t) $ grâce à l'utilisation de deux porteuses orthogonales en cosinus et en sinus avec $f_p$.
 ```

 Le signal $ m_1(t)$ module une porteuse en cosinus :  
 $$
     c_1(t) = \cos(2\pi f_p t)
$$
Le signal modulé  est :  
$$
     m_1(t) \cos(2\pi f_p t)
$$

Dans la deuxième branche, le signal $m_2(t)$ module une porteuse en sinus, obtenue par un déphasage de $ -\pi/2 $ :  
$$
     c_2(t) = \sin(2\pi f_p t)
$$
Le signal modulé correspondant est :  
$$
     m_2(t) \sin(2\pi f_p t)
$$


La somme des deux signaux forme le signal QAM-A :  
$$
     \varphi_{QAM-A}(t) = m_1(t) \cos(2\pi f_p t) + m_2(t) \sin(2\pi f_p t)
$$



- **Efficacité énergétique** 
 
Dans le cas de la modulation QAM-A avec deux signaux $m_1(t)$ et $m_2(t)$,   l’efficacité énergétique est :
$$
\eta_{\text{efficacité-énergétique-QAM}} = \frac{E[|m_1(t)|^2] + E[|m_2(t)|^2]}{E[|\varphi_{\text{QAM}}(t)|^2] }  
$$
Supposons que les deux signaux $m_1(t)$ et $m_2(t)$ ont la même puissance,

$$
\eta_{\text{efficacité-énergétique-QAM-A}} = 1 
$$ 
 

- **Efficacité spectrale**

Pour la modulation QAM-A, la largeur de bande du signal modulé est  égale à celle du message $B$, car chaque signal $ m_1(t) $ et $m_2(t) $ occupe la même bande de fréquence, et l'orthogonalité des porteuses permet d'éviter l'élargissement du spectre, donc
$$
\eta_{\text{efficacité-spectrale-QAM-A}} = \frac{B}{B} = 1
$$

  




- **Démodulation cohérente (synchrone)**

```{figure} images/sec4-qam-demod.png
:label: sec4-qam-demod
:align: center 
 Démodulation cohérente de la QAM : séparation des signaux $m_1(t) $ et $ m_2(t) $ en utilisant des porteuses en quadrature et un filtrage passe-bas.
```


La démodulation cohérente de la QAM-A consiste à extraire les deux signaux modulants $ m_1(t) $ et $m_2(t) $ en utilisant des signaux de référence synchrones. Ce procédé repose sur le produit du signal reçu $ \varphi_{\text{QAM-A}}(t)$ avec les mêmes porteuses utilisées lors de la modulation, suivi d’un filtrage passe-bas.

Le signal reçu est
 $$   \varphi_{\text{QAM-A}}(t) = m_1(t) \cos(2\pi f_p t) + m_2(t) \sin(2\pi f_p t)
   $$

Multiplication avec $ c_1(t) = \cos(2\pi f_p t) $ donne
$$
   x_1(t) = \varphi_{\text{QAM-A}}(t) \cos(2\pi f_p t) = m_1(t) \cos^2(2\pi f_p t) + m_2(t) \sin(2\pi f_p t) \cos(2\pi f_p t) 
  $$

Après filtrage passe-bas on obtient
$$
   m_1(t) = \frac{1}{2} m_1(t)
  $$


En plus, la multiplication avec $c_2(t) = \sin(2\pi f_p t) $  
$$
   x_2(t) = \varphi_{\text{QAM-A}}(t) \sin(2\pi f_p t) = m_1(t) \cos(2\pi f_p t) \sin(2\pi f_p t) + m_2(t) \sin^2(2\pi f_p t)
$$
  et après filtrage passe-bas on a 
$$
   m_2(t) = \frac{1}{2} m_2(t)
$$

 
Donc chaque signal modulant est extrait grâce aux signaux de référence synchrones et au filtrage passe-bas qui supprime les fréquences élevées. Notez que cette méthode nécessite une parfaite synchronisation pour éviter les interférences entre les deux canaux.

 

%```{figure} images/sec4-DSB-SC.png
%:label: sec4-message
%:align: center 
%Aciklama
%```



% - **Modulation**  
%- **Efficacité énergétique** 

%- **Efficacité spectrale**

%- **Démodulation cohérente (synchrone)**





%### **Propriétés clés de la démodulation cohérente :**  
%- **Nécessite une synchronisation précise** entre l’émetteur et le récepteur.  
%- **Un mauvais alignement de phase (\( \theta \)) cause une perte d’amplitude**, voire une distorsion du signal récupéré.  
%- **Utilisée dans les systèmes de communication nécessitant une récupération fidèle du signal message** (radio, télévision, télécommunications numériques).

%---








%L’information est contenue uniquement dans les **bandes latérales** (*side-bands*), nécessitant une démodulation synchrone pour la récupération du signal.

%La modulation **DSB-SC** est donc plus efficace en **énergie** que la modulation AM standard, mais elle n’optimise pas l’usage du **spectre**, contrairement à la modulation à bande latérale unique (SSB).




 %  , sans inclure , contrairement à la modulation AM classique.




%- Cette technique est utilisée dans certaines applications de radio et de transmission de données.






le reste est à venir

## Modulation d’angle (analogique) 

## Modulation numérique

 %Modulation par onde porteuse
%4.1. Modulation d'amplitude
%4.2. Modulation d’angle
%4.3. Modulation numérique

### Codage de ligne

### Systèmes de communication avec porteuse

#### ASK « Amplitude Shift Keying »
#### FSK « Frequency Shift Keying »
#### PSK « Phase Shift Keying »
#### QAM : Frequency Shift Keying »


%#### Largeur de Bande de Transmission - PCM Binaire

%Pour un **PCM binaire**, chaque échantillon est quantifié en utilisant $L$ niveaux de quantification, chaque échantillon est codé sur $N$ bits.  Si le signal analogique $ m(t)$ est **limité en fréquence** à $ B $ Hz, **le théorème de Nyquist** impose un minimum de $ 2B $ échantillons/sec pour une reconstruction parfaite.  Comme chaque échantillon est représenté par $ N $bits, le **débit binaire total** est :
%  $$
%  R_b = 2NB \quad \text{bits/sec}
%  $$
%et donc la **largeur de bande minimale** nécessaire pour la transmission de la sortie de PCM est :
 % $$
 % B_{T,\min} = \frac{R_b}{\eta_{\text{spectrale-binaire, max}}} = NB \quad \text{Hz}
 % $$
%[Lahti&Ding 5e édition:  Équation 5.37, page 312]. 
