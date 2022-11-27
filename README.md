# Home Assistant Run Book

This guide details the design, implementation and troubleshooting tips for our Home Assistant installation.

## Design Theory

The physical and logical design of this Home Assistant installation is bound by the premise that the home should continue to function, with or without a functioning HA installation. The general requirements are as follows:

* Light switches should always turn on/turn off the downstream fixtures and outlets, regardless of if home assistant is offline
* All smart light fixtures will have a smart switch that controls them
* All lights should default power-on to sane illuminance values for any time of day
* Lighting should start the day with blue tones, and shift orange and lower in illuminance as the day progresses
* Modifications to the home should be limited to alterations that can be undone/replaced by any future home owner
* Teardown of the system in preparation for a move/home sale should be limited to 3-4 hours of work and all hardwired devices should be left behind
* Home Assistant configuration files should be backed-up to the cloud
* Spare compute hardware should be onsite for immediate installation
* One (1) spare of each hardwired device will be onsite for immediate installation
* All hardwired devices must use the Zigbee protocol
* All hardware in the system should default to local control only, where reasonable
* All connected appliances with cloud connectivity requirements must be put on an isolated wifi network
* All hardware must support a fail-to-safe condition, e.g., valves default to normally-closed, relays default to normally open
* Energy efficiency must be maximized - the smart home should "save" more energy than it consumes
* All connected appliances with cloud connectivity requirements must have unique accounts with unique, highly complex passwords
* Users may be tracked for the purposes of eventing within the system, but their historical location information may not be persisted
* Cloud-connected voice assistants and video solutions are prohibited
* Video solutions will be confined to publicly accessible spaces, e.g., no cameras within the home or where visual privacy is "expected"

## Reasoning

There are a primary concerns for us as a family: safety, sleep, noise, and independence. We have a child with extra support needs and an automated home can drastically reduce everyone's stress and the cognitive strain on us having to always be on top of things.

### Safety

Perhaps to the surprise of many, safety in this context has much less to do with alarm systems and keeping out intruders; but rather, about keeping us apprised of the location of a child who occasionally elopes (wanders off). By monitoring motion in the house, monitoring exit points from the house, we can provide our child with more freedom and stress less about them leaving the house without telling us. The house uses motion sensors, door open/closed sensors, and a series of notifying automation which informs us of unexpected egress.

### Sleep

For those familiar with cognitive disabilities, sleep challenges can be a symptom and/or side effect of medications. To combat sleep challenges, we use smart lights that are intense blues in the mornings and fade to soft oranges in the evenings. The changing color temperatures and intensities helps to combat the short PNW winter days and LONG PNW summer nights. Is this as effective as happy lamps and melatonin? No, but it's a tool in the tool box.

### Noise

Our child also deals with sensory processing challenges. One major issue in this space that our child deals with is mechanical noise. Mechanical noises can be distracting all the way through physically painful, depending on intensity. By limiting the mechanical sounds in the house to hours when the child isn't home (vacuums), ensuring that mechanical sounds are present for only as long as necessary (bathroom fans), or making sure that doors to mechanical rooms are closed (laundry), we can improve their experiences.

### Independence & Anxiety

When someone is not always taking in information (sensory overload or elevated anxiety) support mechanisms need to be set up to ensure they can be successful. Think about how distracting that transformer in the electrical closet at work is, or that CRT humming in the corner, or the intense smell of your coworkers perfume - all these things can lower your processing abilities, alter your mood, or trigger your anxiety.

If the environment can be controlled, then you are more likely to be successful in learning, growing, and making good decisions. We strive to give our child as much independence as possible, part of that is NOT hovering over them. But to ensure our peace of mind, and their safety some rules must be in place. An example is "don't go outside without telling us." On any given normal day, this rule can be followed well; but in times of high anxiety or if sensory issues are rising then the child may not always remember to ask. Rather than stay in the same room 24/7, we can rely on the automated home to inform us of unexpected exits if we are upstairs cleaning, or out working in the garden.

Lastly, parental attachment can be challenging for our child at times. The automated home can let folks in the house know "when mom will be home" or "where dad is" through self-service kiosks and announcements over the sound systems. This can help control anxiety and help set reasonable expectations.

## Hardware

One of the main features of our smart home is that all smart lighting fixtures have a smart switch upstream that controls their power.

```mermaid
  flowchart LR
      Line-->Switch("Smart Switch")
      Switch-->Light("Smart Light or Load")
```

This design choice ensures that light switches can be used as normal; motion detection systems can turn the power to the smart lights back on when switches have been manually toggled.
