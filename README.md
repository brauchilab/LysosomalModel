## LyModel: Mathematical Model for Lysosomal Homeostasis

This repository contains a Jupyter Notebook implementing a mathematical model for simulating lysosomal homeostasis using Python. The model is encapsulated within a class named LyModel, providing functionalities for parameter initialization, solving differential equations, and visualizing simulation results.

### Usage Example:

```python

# Define cytosolic and luminal concentrations
Na_C  = 0.01   # [M]
K_C   = 0.145  # [M]
Cl_C  = 0.01   # [M]
Ca_C  = 1e-7   # [M]
pH_C  = 7.2    # []

Na_L   = 0.05   # [M]
K_L    = 0.05   # [M]
Cl_L   = 0.06   # [M]
Ca_T_L = 0.0005 # [M]
pH_L   = 6      # []

C_cyt = [Na_C, K_C, Cl_C, Ca_C, pH_C]
C_lum = [Na_L, K_L, Cl_L, Ca_T_L, pH_L]

# Define channel and transporter states
# 0 = off  ; 1 = on
VATP_bool = 1
ch_na_bool = 1
ch_k_bool = 1
# ... (other channel and transporter states)

CH_EX_BOOL = [VATP_bool, ch_na_bool, ch_k_bool, ...]

# If onoff_bool is True, the mechanisms will be allowed to turn on or off during integration
onoff_bool = False

# Define times when channels and transporters change state during integration
# If times = 0, the mechanism remains in the same state (no toggle)

VATP_time = 0
ch_ca_time = 0
ch_k_time = 0
ch_h_time = 0
ch_na_time = 0
ch_cl_time = 0
ex_cax_time = 0
ex_clc7_time = 0
ex_nhe1_time = 0
ch_TRPML1_time = 0

# Create an array with labels, times, and initial states for channels and transporters
onoff = np.array([
    ["V-ATPase pumps", "Ca+2 leak", "K+ leak", "H+ leak", "TPC2", "VRAC", "CAX", "ClC-7", "NHE1", "TRPML1"],
    [VATP_time, ch_ca_time, ch_k_time, ch_h_time, ch_na_time, ch_cl_time, ex_cax_time, ex_clc7_time, ex_nhe1_time, ch_TRPML1_time],
    [VATP_bool, ch_ca_bool, ch_k_bool, ch_h_bool, ch_na_bool, ch_cl_bool, ex_cax_bool, ex_clc7_bool, ex_nhe1_bool, ch_TRPML1_bool]
])

# Simulation setup
psi_0 = 50
int_time = 1000

# Create LyModel instance
Sim_default = LyModel(C_cyt, C_lum, title="Simulation with default parameters")

# Print parameter information
Sim_default.print_parameters()

# Set additional parameters and prepare simulation
Sim_default.swell_r = 0.9
Sim_default.prepare_exp(psi_0, int_time, CH_EX_BOOL, onoff, onoff_bool=True)

# Plot initial scenario
Sim_default.plot_fig_initial()

# Solve ODEs using ODEINT method
Sim_default.solve("ODEINT")

# Get and plot simulation results
Sim_default.get_results(Sim_default.results_raw)
Sim_default.plot_data(Sim_default.results_all)

# Plot final scenario
Sim_default.plot_fig_final()
```

### Contributors:
- Cristian Castillo    (Universidad Austral de Chile)
- Ella Matamala    (Universidad Austral de Chile)
- Diego Becerra    (Universidad de Valparaíso)
- Patricio Orio    (Universidad de Valparaíso)
- Sebastián Braüchi    (Universidad Austral de Chile)

### License:
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

