# Abstract
It is usually assumed that landscape heterogeneity influences animal movements, but understanding of such processes is limited. Understanding the effects of landscape heterogeneity on the movements of large herbivores such as North American elk is considered very important for their management. Most simu-lation studies on movements of large herbivores use predetermined behavioral rules based on empirical observations, or simply on what seems reasonable for animals to do. Here we did not impose movement rules but instead we considered that animals had higher fitness (hence better performance) when they managed to avoid predators, and when they acquired important fat reserves before winter. Individual decision-making was modeled with neural networks that received as input those variables suspected to be important in determining movement efficiency. Energetic gains and losses were tracked based on known physiological characteristics of ruminants. A genetic algorithm was used to improve the overall perfor- mance of the decision processes in different landscapes and ultimately to select certain movement behaviors. We found more variability in movement patterns in heterogeneous landscapes. Emergent properties of movement paths were concentration of activities in well-defined areas and an alternation between small,localized movement with larger, exploratory movements. Even though our simulated individuals moved shorter distances that actual elk, we found similarities in several aspects of their movement patterns such as in the distributions of distance moved and turning angles, and a tendency to return to previously visited areas.




# Intro 
Movement paths of large herbivores are usually
characterized by an alternation between relatively
small movements and larger scale excursions



Movement decisions should reflect trade-offs
between the various factors constraining fitness.
These decisions should vary dynamically as animal
activities change both the internal state of indi-
viduals, such as hunger and energy reserves (Jung
and Koong 1985; Kareiva and Odell 1987), and
the local and global environmental features, such
as resources distribution and abundance (Fryxell
et al. 1988; Fryxell 1991; Adler et al. 2001; Fortin 2003), and predation risk (Lewis and Murray
1993; Schmitz et al. 1997). The interplay between
the morphology and physiology of animals and the
characteristics of their food supply impose con-
straints that may further modulate the movement
of foraging individuals. For example, the interac-
tion between mouth characteristics such as incisor
breadth (Illius and Gordon 1987) and plant bio-
mass (plant size and density) imposes an ‘avail-
ability constraint’ to short-term rates of food
intake by large herbivores (Spalinger and Hobbs
1992; Bergman et al. 2000; Fortin et al. 2004),
whereas the interaction between fiber content of
plants, gut capacity and food turnover (Illius and
Gordon 1987) creates a ‘processing constraint’ on
long-term rates of energy intake (Belovsky 1984;
Fryxell 1991). Furthermore, internal and external
variables influencing foraging decisions by herbi-
vores are likely to change at different rates (e.g. fat
reserves accumulation compared to stomach con-
tent turnover, or rate of vegetation intake versus
rate of vegetation regrowth).


We developed spatially explicit individual-based
models where behavioral decisions are modeled
using feed-forward artificial neural networks
(ANNs) whose connection weights are subject to
‘‘evolution’’ through a genetic algorithm (GA).
Feed forward ANNs are capable of computing
arbitrary nonlinear functions while genetic algo-
rithms can approximate solutions to problems that
do not have a precisely defined solving method
(Whitley 2001).  Here, we test the general approach
in a homogeneous but dynamical landscape and in a patchy landscape with predation risk. As an example, and following a ‘‘pattern oriented ap-
proach’’ (Grimm et al. 1996), we run our model on
digitalized landscape maps from Alberta and
compared daily movement patterns of simulated
animals to those observed for eight GPS-collared
female elk.

**We modeled small-scale behavior that resulted
in many movement and foraging decisions during
the course of a day. The goal was to determine
how such fine-scale decisions eventually defined
broad-scale properties of movement trajectories,
and how in turn the evolution of these properties
was influenced by landscape characteristics. In
other words, our focus was not on the fine-scale
decisions, but rather on the spatial dynamics of
animal distribution that result from these deci-
sions. We concentrated on these properties be-
cause this is the type of information generally
available for real animals from tracing studies, and
because it is becoming increasingly clear that the
redistribution of individuals is a key process in
spatial ecology (COMMENT MIO 'hay que ver qué patrones emergen en términos de ecología espacial para usarlo como filtro del ABM. Esto lo vamos a sacar del análisis de datos en el objetivo 2.'')**





# Methods

Simulated animals could adopt two basic move-
ment behaviors: they could choose (1) to forage, or
(2) to explore (i.e. move without eating). The
outputs of an Artificial Neural Network dictated
which behavior to use, and for how long. When
the simulated animal decided to forage, an ANN
was used to determine diet selection, and another
one to choose movement direction. Given foraging
time and diet preference, the amount of food in-
gested was governed by a mechanistic functional
response (Appendix A), and was kept within the
limits set by digestive constraints.
Another ANN governed movements when the
individual explores instead of eating (Figure 1).

**Each day the individuals kept performing different
behaviors until they accumulate 13 h of daily
activity, which represents a time constraint that
arises from the need to carry out alternative
activities other than foraging (Wilmshurst et al.
1995).**

**The model kept track of (COMMENT 'ABM observation?') energetic gains and
 losses, and the time spent at different landscape
locations. In this implementation we simulated**
**foraging during the spring and summer months,
and animals were ranked according to their
percent of body fat at the end of the season. Pre-**
dation risk was represented by a map of risk per
unit time, and simulated individuals compounded
their experienced risk in proportion to the time
spent in each landscape cell. This experienced risk
translated into an individual survival probability
at the end of a simulation period (150 days). Our
 measure of ‘‘fitness’’  (COMMENT 'ABM observation?) was the product of fat re-
serves and survival probability. We took this
product of survival and accumulated reserves as
our surrogate for individual fitness because fat
reserves are critical for winter survival (Turner et
al. 1994; Cook et al. 2004), and are related to
pregnancy probabilities (Cook et al. 2004). Indi-
viduals reproduced in proportion to their fitness
and new ‘‘character’’ values were generated
according to a fixed ‘‘mutation’’ rate.

... genetic algorithm and NN stuff. 

The ‘‘Switch-ANN’’ decided
which behavior the simulated animal should per-
form, and for how long, by integrating informa-
tion from eight input nodes. These nodes perceived
the state of variables (COMMENT ' state variables for
our agents?') from both the internal and
external environment: fraction of gut filled, per-
cent body fat, fraction of daytime already past,
Julian date, local food biomass (one node for each
of three categories; see Vegetation characteristics
below), and local predation risk.

Elk position on the landscape was assumed to be
in the center of a 28.5-m landscape cell, and move-
ments were among neighboring landscape cells,
with the possibility of multiple inter-cell movements
within a simulated day. The main differences
between a foraging move and an exploratory move
were in the type and extent of the information per-
ceived and on the speed of the moves. Our simulated
animals were always on the move regardless of
whether they choose to forage or to explore. When
exploring, the animal always moved at a fixed speed
of 4 km/h, whereas the time spent in a landscape cell
while foraging was variable (minimum of 30 min
and maximum of 5 h), which resulted on varying
movement speed.

During exploratory movements, individuals had
broader spatial perception and perceived variables
that changed slower than when performing for-
aging movements.The ‘‘Exploratory-Move-
ANN’’ was sensitive to the internal state of the
simulated animal, which was quantified by body
fat. We assumed that the individuals knew the date
of the season (Julian date) and where they were in the landscape (given by x and y coordinates).
**Environmental variables (predation risks and
abundance of the different food types) were as-
sessed at three spatial scales using a hierarchical
perception framework (modified from Beecham
and Farnsworth 1998). The first order of percep-
tion corresponded to the eight nearest neighbor
cells from which the individual had perfect
knowledge of their characteristics. The next level
of perception corresponded to blocks of 3 by 3
cells adjacent to the nearest neighbor cells, and a
third level of perception corresponded to blocks of
9 by 9 cells. For these higher order perceptions
(levels 2 and 3), individuals perceived only aver-
aged values of landscape attributes.** 

Exploratory-Move-ANN and the Foraging-Move-
**ANN dictated movement direction based not only
on predation and abundance of the different food
types, but also on differences in elevation between
current position and neighboring landscape cells.**

**Any area would have a mixture of plants of
different sizes that would reflect the patterns of
vegetation growth and plant consumption by
grazers. Animals would have to choose among
these food items. As grasses matured, their size
increased and their nutritional value decreased
(Fryxell 1991).**

We represented individual body mass (kg) by the
state variable W, which was the sum of lean mass
(M) and body fat mass (F). Fat mass could be as
high as 25–30% of body mass (Moen et al. 1997;
Delgiudice et al. 2001). All our simulated individ-
uals were females that started the season with a
lean mass of 200 kg and with 20 kg of body fat.
Body fat was updated throughout the simulation
based on energy expenses and food intake. We
used summer estimates of energy requirements
from Jiang and Hudson (1992) and Cook (2002) to
assume a maintenance cost (Ed) of 445·W0.75 kJ of
metabolizable energy per day.

In our model, individuals tried to consume en-
ough food to meet their energetic demands and
potential growth. However, the amount of food
consumed was kept within the limits imposed by: (1)
the time available for foraging, (2) the amount of
food that can be ingested during that time given the
vegetation available and the forager’s functional
response, and (3) food processing time. The pro-
cessing time in the gut increased with the amount of
ﬁber in the diet (Illius and Gordon 1992). We
assumed that daily voluntary intake (DVI, in
grams) was a good proxy for the maximum amount
of food that could be ingested in a day due to
digestive constraints. We used the allometric equa-
tion reported by (Wilmshurst et al. 2000):
DVI ¼ 2:5  0:049NDF þ 0:061W0:9


where NDF was the percent neutral detergent ﬁber
of consumed vegetation. The value of NDF used in
equation (3) was the weighted average of the NDF
of the diﬀerent food items in the gut of the animals,
and the DVI value was updated as the animal ate
forage of diﬀerent qualities.
Short-term rate of vegetation intake (I, g/min)
by herbivores could be controlled either by the rate
of food handling in the mouth (cropping and
chewing) or by the encounter rate with food items
(Spalinger and Hobbs 1992; Farnsworth and Illius
1996; Fortin 2002). We modeled food intake rate
based on a mechanistic functional response that
accounted for both of these foraging processes (see
Appendix A for details). This functional response
considered that plants of type i of varying quality
were accepted in the diet with proportion ci (range:
0–1) of their individual encounter rate. The values
of ci corresponded to the output of the Diet-ANN
and could be aﬀected by food availability and
internal conditions.


#### Seasonal appetite and potential growth
Hudson and White (1985) suggest that the poten-
tial growth (PG, in kg/day) and seasonal appetite
(CYCL, range: 0–1) of female elk can be estimated
based on their body mass and the Julian date
(julday):

#### Energy balance
At the end of every simulated day we calculated
the energy that each individual spent and gained

during the day
Ebal ¼ Ef  Ed  ðEl  Eh Þ
ð6Þ
where Ef (in kJ) is metabolizable energy obtained
from food. The gross energy of grass tissues was
set to 18.5 kJ/g while the fraction of grass tissue
that could be digested was determined by size-
speciﬁc digestibility coeﬃcients as described
above.



#### Landscapes

We constructed diﬀerent landscapes by generating
raster maps and controlling the spatial distribution
of Qmax (maximum plant biomass). The growth
rate of vegetation was set as a fraction of local
Qmax and the decay rate was ﬁxed. Performance of
simulated animals was evaluated in the following
landscapes: (1) homogeneous, (2) patchy with
predation risk and (3) actual map of the upper
foothills of Alberta, a subset of the rocky moun-
tain foothills studied by Frair et al. this volume.
Their estimates of peak biomass were used to
distribute Qmax in a patchy manner that was re-
lated to terrain and elevation. A digital elevation
model was provided by Alberta Environment
(Edmonton, Alberta, Canada). Patchy landscapes
were generated by adding 30 bivariate Gaussian
distributions with user-deﬁned standard deviation
(r=30) and whose centers were at random loca-
tions within the landscape. For predation risk, we
used a static map generated by three Gaussian
surfaces (r=125) intended to represent predator
(e.g., wolf) territories.
All landscape cells represented areas of
28.5·28.5 m. Landscapes were ‘‘initiated’’ by let-
ting vegetation grow for 10 days. After that, 100
individuals were released at random locations
within a square of 9 ·9km in the center of the
landscape. Landscapes included 880·880 cells,
which resulted in a density of about 0.16 elk/km2.
For each landscape, we ran 1000 ‘‘generations’’ of
the GA, each consisting of 150 simulated days



### Analysis of movement paths 

We looked at several properties of movement
paths. Daily displacement was measured as the
Euclidean distance between the individual’s loca-
tions at the beginning of consecutive days. Turning
angles were measured as the angular diﬀerence
between consecutive daily movement directions.
Squared displacement (R2n) was the squared dis-
tance between the starting location of an animal
and its location at day n. Mean squared displace-
ment increases linearly with time for simple diﬀu-
sion, it increases exponentially for movement with
directional persistence and it stabilizes for home
range behavior (Turchin 1998). To further explore
temporal changes in the spatial redistribution of
simulated animals we ﬁt Weibull distributions to
displacement data (Rn , net distance from release
point and location at day n). These distributions
can be interpreted as the redistribution kernels for
diﬀerent landscapes. Redistributions kernels are
functions that describe the probability that an
individual moves a certain distance with time. The
Weibull distribution used to ﬁt the displacement
data was controlled by a scale parameter (a), and a
shape parameter (b). The distribution is quite
ﬂexible: It has a fat tail when b<1, it has an
exponential tail when b=1, and it has a bell shape,
similar to a Gaussian, when b is close to 3.6.
Furthermore, under simple diﬀusion the expected
shape parameter value for a Weibull distribution
describing displacement is equal to two (Cain
1991; Morales et al. 2004). Thus, the Weibull not
only describes distribution for distance moved
under simple diﬀusion but it also has a very ﬂexi-
ble shape, which may approximate distribution of
distance moved under other forms of movement
(Morales et al. 2004).

We compared movement patterns from our
simulations in the Rocky Mountain foothills of
Alberta with data from elk (eight females) equip-
ped with GPS collars that were relocated daily
throughout spring and summer of 2001, which
occupied the area within and around our test
landscape. Distributions of daily distance moved
and turning angles were compared using quantile–
quantile plots. If two distributions are the same (or
possibly linearly transformed), the points in a
quantile–quantile plot should form an approxi-
mately straight line. Visual inspection of move-
ment trajectories of both real and simulated
animals revealed returns to previously visited
areas. We quantiﬁed this property by the average
number of repeated landscape positions.



### Discussion
Our simulated animals moved considerably less
that real ones, which might be due in part to an
overestimation of food availability in the simu-
lated landscapes. For example, we assumed that
simulated herbivores consumed all the above-
ground biomass of vegetation, which is generally
not the case for actual large herbivores (Hudson
and Frank 1987; Fortin et al. 2002). We used a
‘‘generic grass’’ model that could have overesti-
mated vegetation regrowth capacity. For even
more realistic models, the generic grass could be
replaced with data driven models for vegetation
distribution and dynamics, which might include
variability due to weather patterns.

Furthermore, our models do not include a
number of forces that are likely to aﬀect move-
ment decisions such as social behavior and mating
systems. A rudimentary form of spatial cognition
was included in our model as individuals perceived 
spatial coordinates while performing exploratory
movements. This allowed for simple spatial
‘‘memory’’ to develop through generations of the
GA but better representations of spatial memory
could be implemented within the ANN-GA ap-
proach. Finally, predation risk was modeled in a
static manner but predators could adapt their home
ranges towards areas where prey are more abundant,
creating further incentives for the prey to move
(Mitchell and Lima 2002; Schmidt and Ostfeld 2003).
The movement trajectory of individuals repre-
sents the outcome of an interaction between
behavior and landscape structure (Wiens et al.
1993; Turchin 1998; Morales 2002).


This
approach, together with summaries of larger-scale
movement properties out of ﬁne-scale behavioral
decisions could be useful to understand the con-
nection between landscapes and animal movement
and ultimately in scaling from individuals to
populations in heterogeneous landscapes.


### Appendix. 


