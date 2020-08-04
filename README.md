# IBM3279

Usually when you repair stuff you need a schematic to understand how the units works. For IBM equipment this is normally not available. Thus I spent some time reverse engineering the IBM PSU fopr the 3279 terminal. This PSU is 220V only and probabnly designed in Europe, so the scematic will not be applicable to US units.
Most IBM hardware has components with proprietary markings on the components. Not just ICs have special markings, but also resistors and capacitors.

I spent some time trying to figuring out what IC taht was used in the design. I checked several standard switching PSU control ICs until I found a match. The Philips TDA 2640 IC. This IC was originally made for Philips own TV sets but has been used in many places both in other Philips equipment and elsewhere like in this PSU.

The design of the PSU is quite simple and takes most of the ideas directly from the reference design. It is a fly-back design with a main switch transformer with a tiny air gap to provide som inductance. As all flyback design there is no filtering inductors on the outputs.
The switch signal from the TDA 2640 chip is amplified in a drive transistor which feed a tranformer. The transformer themn feed the base of the main switching transistor.

To control the voltage there is a separate winding on the transformer that is in the feedback loop of the system. This means that the output voltages are not controled inidvidually, but through this feed back winding which means that the loading of the PSU need to be correct to get the right voltages out of it.
It is hard to estimate the power consumption but a guess is:

| Voltage  | Amps | Comment |
|----------|------|---------|
|   5V     |  6A  | 6 wires |
|   8.5V   |  4A  | 4 wires |
|   -5V    |  1A  | 2 wires |
|   +12V   |  1A  | 3 wires |
|   -12V   |  1A  | 2 wires |
|   103V   | 0.5A | 1 wire  |

Total power output is thus: 144.5W.

The trim potentiometer controling output voltage is set to 690 ohm when measured in circuit.




![Component designators.](https://i.imgur.com/i2lNYLG.jpg)
