# On-Off-Shim Simulation and Extension for Supply Voltage >5V

Two [LTspice XVII](https://www.analog.com/en/design-center/design-tools-and-calculators/ltspice-simulator.html) setups are provided:
1. Starting from the schematic provided in https://github.com/pimoroni/clean-shutdown/issues/18#issuecomment-456816943, the original circuit was modeled.
2. The circuit was modified to use an 18V supply with an additional 5V voltage regulator. The modification is targeted to the [HifiBerry Amp2](https://www.hifiberry.com/shop/boards/hifiberry-amp2/), but could be used in other cases where a supply voltage >5V needs to be switched.

The [BSS138 N-Channel Logic Level Enhancement Mode MOSFET simulation model](BSS138.lib) was downloaded from [onsemi's website](https://www.onsemi.com/design/resources/design-resources/models?rpn=BSS138).

## On-Off-Shim Simulation
<img width="959" alt="On-Off-Shim Schematic" src="https://github.com/matthias-bs/clean-shutdown/blob/master/simulation/onoff_shim_schematic.png">

[On-Off-Shim LTspice schematic](https://github.com/matthias-bs/clean-shutdown/blob/master/simulation/onoff_shim_schematic.asc)


* on-off push button: voltage controlled switch (S3) controlled by supply V3 configured with piecewise-linear sequence; switched on for 0.5s at t=[10, 20, 30]s
* Raspberry's on-board 3.3V regulator: voltage supply V2 and voltage controlled switch S1
* Raspberry's shutdown request GPIO (input): R10 (just for modeling an input port to the Raspberry Pi block)
* Raspberry's SW-controlled shutdown GPIO (output): voltage controlled switch S2 and voltage supply V4; switched on (logically 3s after shutwown request) for 0.5s at t=23s
* load at 5V and 3.3V supply: R6 and R7

<img width="959" alt="On-Off-Shim Waves" src="https://github.com/matthias-bs/clean-shutdown/blob/master/simulation/onoff_shim_waves.png">


## On-Off-Shim >5V Supply Voltage Extension Simulation
