# FAVITES Configuration File for COVID in Wuhan, 2020

## Contact Network:
#### Through nodes (people) and edges (interactions), describe social interaction.
#### Model: `Barabasi-Albert (BA)`
- The Barabasi-Albert network's scale-free properties "recapitulate infectious disease spread" (Cite?). For example, scale-free networks can model "hubs", which illustrates the idea that somewhere with more infections would be more likely to accumulate even more infections.
#### Number of nodes: `10000`
- Picked an even, easy to work with number.
#### m (# edges attached from new to existing nodes): `8`
- 2m is equal to the expected degree, which is set to an intermediate value of 16 contacts per day (Mossong et al.).
___


## Transmission Network:
#### Describe how the virus moves through the contact network, based on transition rates for individuals in our simulation. Transition rates are based on the reciprocal of expected time to arrival (make sure to keep track of your 'time' units!). 
#### Model: SAPHIRE
- This model was developed specifically to illustrate the dynamics of COVID-19 transmission, with states to model presymptomatic phases, testing, hospitalization, and more. See below for each state and its abbreviation. 
- S: Susceptible; A: Unascertained case; P: Presymptomatic Infectious Case; H: Hospitalized Case; I: Ascertained Infectious Case; R: Removed; E: Exposed

#### Duration: `100 days`
- This simulation is meant to look at the start of the COVID-19 pandemic, so we look at a span of 100 days, or around 3 months. 

#### N_S: `9999`
- The number of susceptible individuals at the start of the simulation
- Whichever nodes that do not start as infected are susceptible.

#### N_A: `0`
- The number of unascertained cases at the start of the simulation
- At the start of the simulation, there are no unascertained (potentially including asymptomatic and mildly symptomatic individuals, Hao et al.) cases yet.

#### N_P: `0 `
- The number of presymptomatic individuals at the start of the simulation
- At the start of the simulation, no one is in the presymptomatic stage yet.

#### N_H: `0 `
- The number of hospitalized individuals at the start of the simulation
- At the start of the simulation, no one has been hospitalized yet.

#### N_I: `0`
- The number of ascertained infectious cases at the start of the simulation
- At the start of the simulation, one person is exposed but no one has tested positive yet.
#### N_R: `0`
- The number of removed individuals at the start of the simulation
- At the start of the simulation, no individuals have died or recovered. 
#### N_E: `1`
- The number of exposed individuals at the start of the simulation
- Start with one person exposed to witness how the virus spreads.
#### R_S-E: `0`
- Transition rate from susceptible to exposed
- See table S7, no infections from outside the contact network. 
#### R_S-E_E: `(???)`
- The transition rate from susceptible to exposed induced by exposed neighbors
- (???)
#### R_S-E_P: `4.83`
- The transtion rate from susceptible to exposed induced by presymptomatic neighbors 
- See table S7; 0.55*0.385*365/16
#### R_S-E_I: `8.78`
- The transition rate from susceptible to exposed induced by ascertained infectious neighbors
- See table S7; 0.385*365/16
#### R_S-E_A: `4.83`
- The transition rate from susceptible to exposed induced by unascertained neighbors
- See table S7; 0.55*0.385*365/16
#### R_E-P: `125.86`
- The transition rate from exposed to presymptomatic
- See table S7 for Timing of Covid Pandemic Pekar et al.; 365/2.9
#### R_P-A: `134.89`
- The transition rate from presymptomatic to unascertained
- See table S7; (1-0.15)*365/2.3
#### R_P-I: `23.80`
- The transition rate from presymptomatic to ascertained infectious 
- See table S7; 0.15*365/2.3
#### R_A-R: `125.86`
- The transition rate from unascertained to removed
- See table S7; 365/2.9 is the reciprocal of the expected time for arrival to move from an unascertained case to either being removed or recovered.
#### R_I-H: `17.38`
- The transition rate from ascertained infectious to hospitalized
- See table S7. The expected arrival time of hospitalization is 21 days / 365 days (1 year), and since transition rates are in terms of the reciprocal of expected arival, we use 365/21.
#### R_I-R: `125.86`
- The transition rate from ascertained infectious to removed
- See table S7; 365/2.9 is the reciprocal of the expected time for arrival to either be removed or recovered. 
#### R_H-R: `12.17`
- The transition rate from hospitalized to removed
- See table S7; 365/30 is the reciprocal of the expected time for someone in the hospital to either be removed or recovered.
___

## Sample Times:
#### Describe when the individuals in the transmission network are sampled (sequenced). 
#### Model: `value`
- (???) do we want to model that people get sequenced when they go to the hospital? Or just do normal? Or do state entry (all?)

___
## Viral Phylogeny (Transmissions):
#### Describe the topology and branch lengths (in time units) of the viral phylogeny thoughout the epidemic, constrained by the transmission network.
#### Model: `Transmission Tree`
- In a transmission tree, nodes are infected hosts; edges are transmission events. Coalescent events occur as late in time as possible.
___
## Viral Phylogeny (Seeds):
#### Describe the topology and branch lengths (in time units) of the viral phylogeny prior to the epidemic (viral phylogeny of the seed individuals).
#### Model: `(???)`
- (???)
___
## Mutation Rates:
#### Describe how mutation rates (mutations/time) are sample along each branch of the viral time phylogeny.
#### Model: `Constant`
- Each branch's length is multiplied by a constant rate (to convert from time units to mutations).
#### rate: `0.00092`
- The constant mutation rate, inferred from BEAST results in the multiple zoonotic origins paper (Pekar et al.).
___
## Ancestral Sequence:
#### Describe how the ancestral (root) sequence is generated/selected.
#### Model: `Exact base frequencies`
- We can looke at the COVID-19 genome and calculate base frequencies.
#### k: `29903`
- The value of the COVID-19 genome is around 30,000 bases.
- Frequencies (see below) were calculated using the [NCBI reference sequence for Wuhan-Hu-1, complete genome](https://www.ncbi.nlm.nih.gov/nuccore/1798174254).
#### p_A: `0.299`
- The frequency of base A is
#### p_C: `0.184`
- The frequency of base C is
#### p_G: `0.196`
- The frequency of base G is
#### p_T: `0.321`
- The frequency of base T is
___
## Sequence Evolution:
#### Describe how sequences evolve down the phylogeny.
#### Model: `General Time-Reversible (GTR) + Gamma`
- rationale (???)
#### p_A: `0.299`
#### p_C: `0.184`
#### p_G: `0.196`
#### p_T: `0.321`
#### r_A-C: `0.52433`
#### r_A-G: `2.65505`
#### r_A-T: `0.43262`
#### r_C-G: `0.38930`
#### r_C-T: `7.66544`
#### r_G-T: `1.00000`
#### alpha: `0.194`
- The shape parameter of Gamma model of rate heterogeneity
- rationale
#### num_cats: `0`
- The number of categories in discrete Gamma model (or 0 for continuous)
- rationale
#### prop_invariable: `(???)`
- Proportion of invariable sites
- (???)
