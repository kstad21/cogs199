# FAVITES Configuration File for MSM Population in San Diego

## Contact Network: Through nodes (people) and edges (interactions), describe social interactions.
#### Model: `Barabasi-Albert (BA)`
- Uses preferential attachment, so nodes with more connections are likely to make connections (think about how someone with lots of friends might be more likely to make even more friends).
#### Number of nodes: `10000`
- Picked an even, easy to work with number.
#### m (number of edges attached from new to existing nodes): `2`
- There are estimates of between 3-4 sexual partners over 10 years: ~3 in Wertheim et al. (2017) and 3-4 in Rosenberg et al. (2017). Expected degree (number of partners) is equal to 2*m, so we set m to 2.

## Transmission Network: Describe how the virus moves through the contact network, based on transition rates for individuals in our simulation. Transition rates are based on the reciprocal of expected time to arrival (make sure to keep track of your 'time' units!).
#### Model: `Granich et al. (2008)`
- The model uses states based on HIV progression, including states for indidividuals on ART (antiretroviral therapy) and states for those who are not. Whether or not a node is on ART, there are 4 stages of progression: 1, 2, 3 and 4. Granich et al. (2008)
#### Duration: `10`
- Ten years!
#### N_NS: `0`
- This configuration file only looks at susceptible nodes, so there are no non-susceptible nodes in the network.
#### N_S: `9999`
- Every node that is not starting as infected will fall into the susceptible category.
#### N_I1: `1`
- Chose starting with 1 person in I1 to emphasize progression of the pandemic but this is easily changeable. Initial counts may have little to no effect on overall counts if the duration of the epidemic is long enough.
#### N_I2, N_I3, N_I4, N_A1, N_A2, N_A3, N_A4: `0`
#### S --> I1 (transition rate from susceptible to infected stage 1): `2`
- Based on MSM populations (Grey et al. (2016)), with San Diego County's estimation being 1,204,728. Between 2017 and 2021 in California, an average of 70% of new diagnoses came from male-to-male sexual contact (MMSC) (California HIV Suveillance Report -- 2021). In 2021, there were 379 new HIV diagnoses in San Diego (CA Surveillance Report). So out of 379 diagnoses and an estimated 70% of those coming from MMSC, we can estimate there are about 265 diagnoses for MSM. Looking at the whole population: 265/1,204,728 = 0.00022. Scaling this to our chosen number of nodes: 10,000 * 0.00022 = 2.2 diagnoses a year. In a Poisson distribution, the expected value (2) will be equal to the reciprocal of the time until next arrival.
#### S --> I1 induced by neighbors in I1: `0.1125`
- In the FAVITES paper, relative rates were scaled so that number of new cases over ten years was roughly accurate. This yielded a rate of infectiousness 0.1125.
#### S --> I1 induced by neighbors in I2: `0.0225`
- In the FAVITES paper, relative rates were scaled so that number of new cases over ten years was roughly accurate. Infectivity of chronic nodes was used as a baseline.
#### S --> I1 induced by neighbors in I3: `0.0225`
- Set this to be the same as above (??)
#### S --> I1 induced by neighbors in I4: `0.0225`
- In the FAVITES paper, relative rates were scaled so that number of new cases over ten years was roughly accurate. Infectivity of chronic nodes was used as a baseline.
#### S --> I1 induced by neighbors in A1: `0.005625`
- Those in the acute treated stage were found to have 1/20 the infectiousness of chronic untreated individuals (Cohen et al. (2011)).
#### S --> I1 induced by neighbors in A2: `0`
#### S --> I1 induced by neighbors in A3: `0`
#### S --> I1 induced by neighbors in A4: `0`
#### I1 --> D: `0`
- In this configuration, death is only a possible transition in either I4 or A4. 
#### I1 --> I2: `6`
- Individuals spend an expected 2 months in the acute state (Grani1ch et. al). Transition rates are in unit of reciprocal of next arrival so 2 months = 1/6 year; reciprocal of 1/6 is 6.
#### I1 --> A1: `1`
- Expected 1 year to start ART (FAVITES)
#### A1 --> D: `0`
- In this configuration, death is only a possible transition in either I4 or A4. 
#### A1 --> A2: `0.0883`
- Length of stay in A1 is expected to be 11.33 years, find the reciprocal. (Zingoni et. al, 2019)
#### A1 --> I1: `0.481`
- Expected time to stop ART is 25 months. 1/(25/12) ~ 0.481. (FAVITES)
#### I2 --> D: `0`
- In this configuration, death is only a possible transition in either I4 or A4. 
#### I2 --> I3: `0.125`
- Expected time in chronic state is 8 years (Granich et. al). 1/8 = 0.125
#### I2 --> A2: `1`
- Expected time to start ART is 1 year. (FAVITES)
#### A2 --> D: `0`
- In this configuration, death is only a possible transition in either I4 or A4. 
#### A2 --> A3: `0.181`
- Length of stay in A2 is estimated to be 5.51 years, 1/5.51 ~ 0.181. (Zingoni et. al, 2019)
#### A1 --> I2: `0?`
#### I3 --> D: `0`
- In this configuration, death is only a possible transition in either I4 or A4.
#### I3 --> I4: `0.5`
- Expected time in stage 3 is 2 years without ART. 1/2 = 0.5.
#### A3 --> D: `0`
- In this configuration, death is only a possible transition in either I4 or A4. 
#### A3 --> A4: `0.139`
- Length of stay in A3 is estimated to be 7.17 years, find reciprocal. (Zingoni et. al, 2019)
#### I4 --> D: `1.82`
- Expected time in stage 4 is 5% of survival time without ART, with mean survival time without ART being 11 years (Granich et. al). 0.05 * 11 = 0.55; 1/0.55 = 1.8181
#### I4 --> A4: `0.481`
- Expected time to stop ART is 1 year. (FAVITES)
#### A4 --> D: `0.146`
- Length of stay in A4 is expected to be 6.86 years (Zingoni et. al, 2019). 1/6.86 = 0.146
#### A4 --> I4: `0.481`
- Expected time to stop ART is 25 months. 1/(25/12) ~ 0.481. (FAVITES)

## Sample Times: how are individuals in the transmission network sampled?
#### Model: `End`
- End was chosen to get a good idea of every node's state at the end of the simulation.
#### sampled_states (Comma-separated list of states in which individuals are sampled): `I1,I2,I3,I4,A1,A2,A3,A4`
- For this configuration, all states were sampled to get as much information as possible.
#### num_samples: `1`
- With this sampling configuration, we choose to sample every single individual once at the end of the simulation.

## Viral Phylogeny (Transmissions): With a coalescent framework, describe topology and branch lengths (in unit of time) of the viral phylogeny throughout the epidemic under the constraints of our chosen transmission network.
#### Model: `Transmission Tree`
- In a transmission tree, nodes are infected hosts; edges are transmission events. Coalescent events occur as late in time as possible.

## Viral Phylogeny (Seeds): Describe the topology and branch lengths (in unit of time) of the viral phylogeny of the seed individuals.
#### Model: `Non-Homogeneous Yule`
- asdf
#### rate_func (Rate function of the initial tree): e^-(t^2)+1
- Chosen to emulate short branches close to the base of the tree. (FAVITES)
#### height: 25
- Scaled so that height matches the 1980 estimate using SD. (???)

## Mutation Rates: how are mutation rates sampled along each branch of the viral time phylogeny?
#### Model: `Truncated Normal`
- Other distributions deviate significantly from real distributions, so we use Truncated Normal (FAVITES).
#### mu (Location parameter, analagous to the mean of a normal distribution): `0.0008`
- ????
#### sigma (Determines the width of the distribution's peak): `0.0005`
- Chosen to scale branch lengths from years to expected number of per-site mutations (FAVITES).
#### a (Minimum of Truncated Normal): `0`
#### b (Maximum of Truncated Normal): `infinity??`

## Ancestral Sequence: Describe how ancestral (root) sequence is generated/selected.
#### Model: `Exact Base Frequencies`
- A simple option with the ability to define the frequency of each base.
#### k (Length of ancestral sequence): `1000`
- An even number large enough for some detail but not large enough to take a long time (??)
#### p_A (Frequency of A): `0.25`
#### p_C (Frequency of C): `0.25`
#### p_G (Frequency of G): `0.25`
#### p_T (Frequency of T): `0.25`
- Easily changeable; chose a simple even distribution of all the bases.

## Sequence Evolution: Describe how sequences evolve down the phylogeny.
#### Model: `General Time-Reversible (GTR) + Gamma`
- General Time-Reversible "doesn't care" whether a sequence is an ancestor or descendent. The Gamma parameter allows the number of substitutions per site to change, as sampled from the Gamma distribution.
#### p_A (Frequency of A): `0.392`
#### p_C (Frequency of C): `0.164`
#### p_G (Frequency of G): `0.212`
#### p_T (Frequency of T): `0.232`
#### r_A-C (Transition rate between A and C): `0.182`
#### r_A-G (Transition rate between A and G): `9.934`
#### r_A-T (Transition rate between A and T): `0.718`
#### r_C-G (Transition rate between C and G): `0.971`
#### r_C-T (Transition rate between C and T): `9.934`
#### r_G-T (Transition rate between G and T): `1.000`
- These frequencies were pulled from the FAVITES paper, which used parameters inferred by IQ-TREE. (FAVITES)
#### alpha (Shape parameter of gamma model of rate heterogeneity): `0.405`
- A higher value of alpha leads to a more "peaked" distribution (University of Buffalo, https://www.acsu.buffalo.edu/~adamcunn/probability/gamma.html#:~:text=The%20parameter%20%CE%B1%20is%20known,%22spread%22%20of%20the%20distribution)
#### num_cats (Number of categories in discrete gamma model): `0`
#### prop_invariable (Proportion of invariable sites): `0`
- 0 categories was chosen for a continuous distribution, 0 sites were chosen to be invariable. 
