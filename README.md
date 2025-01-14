# An A-Life epidemiological model
Etienne Sagon
## Abstract
The increasing of computing power of these last few years has made complex systems simulations easier to carry out. In this article, we try to simulate the propagation of a disease among individuals, who are moving and interacting in an environment. We ran several simulations with different parameters in our model. We found out that a probability of reproduction around 0.5 was not too high and not too low: the population expands not too fast. The results show that the virulence level at which the disease begins is the one that has the biggest impact on the evolution of the system: a virulence too high leads to the end of the population, a virulence too low leads to the end of the disease and the survival of the individuals.

## Usage
### Installation
Run this to clone the project and install the required libraries:
```bash
git clone https://github.com/killian31/A-Life-Epidemiological-Model.git
cd A-Life-Epidemiological-Model
pip install -r requirements.txt
```

### Start the App
Simply run this command to launch the app:
```bash
python3 Main.py
```

## Context
In order to realize an epidemiological model, we have realized a complex system putting in interaction individuals with diseases. First, the relationship between hosts and diseases will be an emergent process instead of a single mathematical function. Second, both hosts and diseases will be agents in our system albeit with different behavioral rules. Third, diseases will have a much faster mutation rate but can only survive inside a host resulting in a delicate balance for their continued survival.
To begin with, we will study the characteristics of the model and then we will analyze the results generated by our simulations.

## Model
- **Hosts**: Each Host is characterized by :
  - a color (determined by three intensities of Red, Green and Blue). These three levels represent in a simplified way the genes of an individual;
  - a health level (between 0 and 1);
  - a life expectancy (determined randomly between 1000 and 1500 time steps);
  - the fact of being infected by a disease or not.

- **Diseases**: Each disease is characterized by:
  - a color (determined by three intensities of Red, Green and Blue) in the same way as for hosts;
  - a level of virulence identical to each disease at the beginning of the simulation then varying according to the mutations occuring at each time step;
  - a duration (randomly determined between 100 and 500 time steps).

In a similar way as for the hosts, it seemed coherent to us to introduce a maximum duration for diseases,
to allow hosts to heal when the disease does not kill them.

- **Reproduction**: The hosts can reproduce with their neighbors. This reproduction depends on a proba- bility defined at the beginning of the simulation. When the hosts reproduce, they give birth to a new host whose color intensities are defined by a random mix of the colors of the two parents. This new host has a minimal time before being able to reproduce (100 time steps), symbolizing the childhood period. The parents also have this minimal time before being able to reproduce again. We found it important to set up these minimal times because it allows us to control the speed of reproduction.

- **Infection**: In case a host is infected, it can transmit its disease by infecting its neighbors. The infection depends on a probability determined by multiplying the level of susceptibility of the host with the disease and the level of virulence of the disease. Indeed, we suppose that the more virulent a disease is the more it is transmitted in the population. The level of susceptibility between a disease and an individual is defined as the Euclidean distance between the host color and the disease color. This means that the closer individuals are genetically to the disease the more likely they are to be infected.

- **Mutation**: A disease mutates over time, we assume in our model that they mutate randomly. To do this our mutation function modifies very slightly and at each time step all the parameters of the disease (color, virulence, duration).

## Results
### Model 1

In this model, the population starts at **50 hosts**, with **15 infected** among them. They have a **probability of reproduction of 0.5**, and **the diseases start all with a virulence of 0.75**. In figure 1 (see [pdf file](Article.pdf)), we can see the population dynamics. First, we can see an exponential increase of the population, reaching the limit of 100 hosts that we fixed, very quickly. Then, the numbers of infected hosts follows the same pattern with a shift of about 500 time steps. Some hosts start to die due to the disease, their number stay steady before starting to shrink at about 2000 time steps: almost everyone has developed a disease. The disease stay among the population all along its decrease, and everyone died at almost 6000 time steps.

The data exposed in figure 2 show more details about the evolution of the diseases: in figure 2a and figure 2c (see [pdf file](Article.pdf)) we can see that the mutations have led to the persistence of a high virulence among the different hosts, that’s why they were quickly all sick. Figure 2b (see [pdf file](Article.pdf)) show that the duration of the disease is increasing along time because of the mutations, encouraging the quick end of the population.
There is no winner in this model: both hosts and disease die at the end. The mutations resulted in a high virulence and a disease that killed too fast. This pattern happens often when starting the simulation with a high virulence, we obtained similar results by starting with virulence between 0.3 and 0.8. That is why we will analyze another model with a lower virulence at the beginning.

### Model 2

This model introduce a single change, we lower the value of the **virulence to 0.1**. We can see in figure 3 (see [pdf file](Article.pdf)) that the disease has been slower to infect the hosts, it took about 500 time steps to start infecting, and we can see in figure 4 (see [pdf file](Article.pdf)) that this time corresponds to the point where the disease average virulence and duration started to increase. Then the population starts to decrease linearly, but as we can see in figure 4c (see [pdf file](Article.pdf)), the average virulence did not continue increasing, leading to the end of the disease.
In this model, the population has won quite quickly, it took only about **1750 time steps to get rid of the disease**, because it was not that virulent, and the duration did not go over 600 as shows figure 4b (see [pdf file](Article.pdf)). This pattern seem to be usual with virulence between 0.1 and 0.3 at the beginning, as we saw in different simulations we ran.

## Conclusion

To conclude, we have seen that our model is quite sensitive to the virulence we set at the beginning of the simulation. We ran additional simulations with virulence between 0.3 and 0.8, and we almost always have the same result: hosts and disease die at the end. Simulations with a virulence between 0.1 and 0.3 led to the extinction of the disease, with not that much loss for the hosts.
Concerning the limits of our project, the hypothesis we made can be unrealistic, in particular the fact that the disease duration can be almost a third of a individual’s life expectancy. A second issue is that we did not have enough calculation power to carry out a large number of simulations within the time we were given.
With more calculation power, we could imagine carry out a very large number of simulations, in order to get a lot of data, and to try to determine which parameters lead to a disease’s persistence within a population, or to predict how a disease will perform, given its characteristics.

