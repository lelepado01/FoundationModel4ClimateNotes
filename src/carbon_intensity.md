# Carbon Intensity Estimation

Embodied Carbon: from for example HW manufacturing

Operational Carbon: from execution of HW / programs

GHGP: corporate carbon reporting standard (the one with Scope1, Scope2...)

CUE: ISO standard quantifying the amount of carbon emission as kgCO2e per energy consumed in kWh
    = PUE (power usage effectiveness) * CEF (carbon emission factor)

### Methodology

CF = (IT_energy * PUE * <Energy Mix (% energy sources), Emission Factor (gCO2e/kWh)>) / Core_Hours
    = gCO2e / CoreH


### Market based carbon intensity estimation

A consumer who has invested in green energy can claim the credit for the reduction in emission (calculate entity of green part, then estimate the remaining with energy mix method). 

CI = sum((E_i -  Ei_p) * CEF_i) / (E - Ep)