# FAVITES Configuration File for COVID in Wuhan, 2020

## Contact Network:
### Through nodes (people) and edges (interactions), describe social interaction.
#### Model: `Barabasi-Albert (BA)`
- rationale
#### Number of nodes: `10000`
- Picked an even, easy to work with number.
#### m (# edges attached from new to existing nodes): `8`
- rationale



## Transmission Network:
### Describe how the virus moves through the contact network, based on transition rates for individuals in our simulation. Transition rates are based on the reciprocal of expected time to arrival (make sure to keep track of your 'time' unites!). 
#### Model: SAPHIRE
- rationale
- S: Susceptible; A: Unascertained case; P: Presymptomatic Infectious Case; H: Hospitalized Case; I: Ascertained Infectious Case; R: Removed; E: Exposed

#### Duration: `100 days`
- rationale

#### N_S: `value`
##### The number of susceptible individuals at the start of the simulation
- rationale

#### N_A: `value `
##### The number of unascertained cases at the start of the simulation
- rationale

#### N_P: `value `
##### The number of presymptomatic individuals at the start of the simulation
- rationale

#### N_H: `value `
##### The number of hospitalized individuals at the start of the simulation
- rationale

#### N_I: `value`
##### The number of ascertained infectious cases at the start of the simulation
- rationale
#### N_R: `0`
##### The number of removed individuals at the start of the simulation
- rationale
#### N_E: `value`
##### The number of exposed individuals at the start of the simulation
- rationale
#### R_S-E: `value`
##### Transition rate from susceptible to exposed
- rationale
#### R_S-E_E: `value`
##### The transition rate from susceptible to exposed induced by exposed neighbors
- rationale
#### R_S-E_P: `value`
##### The transtion rate from susceptible to exposed induced by presymptomatic neighbors 
- rationale
#### R_S-E_I: `value`
##### The transition rate from susceptible to exposed induced by ascertained infectious neighbors
- rationale
#### R_S-E_A: `value`
##### The transition rate from susceptible to exposed induced by unascertained neighbors
- rationale
#### R_E-P: `value`
##### The transition rate from exposed to presymptomatic
- rationale
#### R_P-A: `value`
##### The transition rate from presymptomatic to unascertained
- rationale
#### R_P-I: `value`
##### The transition rate from presymptomatic to ascertained infectious 
- rationale
#### R_A-R: `value `
##### The transition rate from unascertained to removed
- rationale
#### R_I-H: `value`
##### The transition rate from ascertained infectious to hospitalized
- rationale
#### R_I-R: `value `
##### The transition rate from ascertained infectious to removed
- rationale
#### R_H-R: `value`
##### The transition rate from hospitalized to removed
- rationale
