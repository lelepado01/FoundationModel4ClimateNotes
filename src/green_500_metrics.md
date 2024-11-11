# Green 500 Metrics

- GFlops/Watt: the number of floating-point operations per second that can be executed by a computer, divided by the power consumed by that computer 
- Power (kW): the power consumed by the system 
- RMax (PFlops/s): the maximum performance of the system (practically achieved)
- RPeak (PFlops/s): the theoretical peak performance of the system

# Utils

The heat dissipation is a problem with large clusters, this means that the delta between the power consumed and the power dissipated is not negligible (RMax - RPeak). This is a problem because the power consumed is the power that the system is drawing from the grid, and the power dissipated is the power that the system is actually using. This means that the system is not using all the power that it is drawing from the grid, and this is a waste of energy.

Green Destiny: low power supercomputer, no unscheduled downtimes despite no cooling, humidification or air filtration. 

Green500: treats both the power consumed and the performance 

- [SPEChpc](https://www.spec.org/power_ssj2008/).
- ED^n metric: Energy Delay product, the product of the energy consumed and the time taken to complete a task.
- FLOPS/Watt: the number of floating-point operations per second that can be executed by a computer, divided by the power consumed by that computer. (Might be biased towards small supercomputers, so measure one node only and then multiply by the number of nodes)

# Making the case for Green 500 List

- ED or ED^2 or ED^3: Energy Delay product, the product of the energy consumed and the time taken to complete a task.
- V_0 = E^(1-theta) * D^(1+theta) where theta is a parameter that can be adjusted to reflect the importance of energy and delay in the metric.

# Escapedes to Exascale

GreenIndex (TGI): measures the efficiency with regards to a reference system. Where i indicates a specific benchmark. 

- EE_i = Performance_i / Power_i
- Relative EE_i = EE_i / EE_ref
- TGI = sum_i (W_i * Relative EE_i)