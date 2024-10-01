
# Energy intensity of internet data transmission

> [Paper](https://www.sciencedirect.com/science/article/pii/S0195925513001121) | [Code]()

Estimation of how much energy is necessary to transmit data over the internet (KWh / Gb).

New criteria is given, plus new estimate for 2015 of 0.06 KWh / Gb. This results in 50% less cost since 2000, which is comparable to the energy and performance increase in computing.

- Bottom-up approach: sum of all electricity consumption / data transmitted through equipment (underestimation)
- Top-down approach: network electricity used / total data transmitted (overestimation)

New method is weighted average of previous estimations + regression on historical data for validation. 

Subdivision is different groups of consumption: data centers; undersea cables; IP, access, home networks; and end-user devices.