# TankLight: 3-minute pitch

Script for Hack for Humanity Ottawa 2026. About 420 spoken words (around 150 a minute) plus
three demo clicks, leaving time for pauses. Lines marked *(cut if short)* can go if a rehearsal runs over 3:00.

## Before you go on stage

- [ ] `python app.py serve` is running. Open **http://127.0.0.1:8008/?kitchen**: only the kitchen display, large.
- [ ] Press **Restart in January** once (in "Show the demo") so the town starts fresh, then go back to Kitchen mode.
- [ ] Zoom the browser to 125%; use light mode on a projector.
- [ ] On the table: two jars of tap water and a vitamin C tablet (the prop for the vitamin C moment).
- [ ] Backup: a terminal with `python app.py` already run (the same scenarios as text), and screenshots.
- [ ] Confirm with Amenda that it's OK to mention the pipeline plan (it came from a draft resolution).
- [ ] Rehearse once out loud with a timer.

## Timing

| Time | Section | On screen |
|---|---|---|
| 0:00–0:20 | Hook | Kitchen mode (the light alone) |
| 0:20–0:50 | The problem | Kitchen mode |
| 0:50–1:50 | Demo: three moments | "Show the demo", then tour steps 1, 6, 7 ("Show me") |
| 1:50–2:30 | Both tanks, both trucks, the office AI | Tour steps 9 (sewage), 12 (truck plan), 13 (office plan) |
| 2:30–2:50 | Different and honest | Tour step 15 |
| 2:50–3:00 | Close | Kitchen mode |

## Script

### 0:00 Hook
> In Inukjuak, a case of 24 water bottles costs seventy-six dollars.
> There are no pipes under the ground: rock and permafrost. A truck brings treated water to a tank
> inside the house, and another truck pumps the sewage tank outside. The water leaves the plant
> safe. What happens in the tank, nobody can see.

### 0:20 The problem
> Stored water is protected by chlorine; the minimum is 0.2 milligrams per litre.
> In Cambridge Bay, researchers found the truck water was fine, but many household tanks were low.
> A Nunavut risk study scored household tanks "no barriers, no monitoring". In Kangiqsualujjuaq, a
> third of households ran out of water in a single week. *(cut if short)* And this June, Inukjuak
> was on a boil-water advisory.

### 0:50 Demo: three moments
> TankLight puts one light in the kitchen, readable from across the room.

**[Press "Show the demo", "Take the tour", then "Show me: Fill a nearly empty tank"]** Green, Protected.
> Colour, shape, pulse and words, so it works without colour vision and without reading. Hours of
> protection left, days of water, and the chance you run out before the truck.

**[Drop the vitamin C tablet in a jar. Next to step 6, "Show me: Add vitamin C"]** Red, Boil first.
> Vitamin C removes chlorine. The light waits for two readings, so one noisy reading never
> causes an alarm, and then says: boil first.

**[Next to step 7, "Show me: Pull the probe out"]** Grey, Needs service.
> If a sensor fails, it goes grey. TankLight never shows green when it isn't sure.
> In a blizzard it warns a day and a half before the water runs out. It all runs on the
> device: offline, through the storm.

### 1:50 Both tanks, both trucks
**[Next to step 9: the sewage line]**
> The sewage tank outside gets the same care: how full it is, and a freezing warning if the
> heater fails in January.

**[Next to step 12: truck plan]**
> And the trucks. Instead of a fixed loop, trucks go where tanks are about to run dry and skip
> the full ones. In our simulated July, with the same number of stops, homes went from 534 hours
> without water to 188.

**[Next to step 13, press "Make the office plan" first: it takes about 6 seconds]**
> For the water office, AI runs on this laptop, offline. Google's TimesFM forecasts next week's
> demand with the blizzard forecast, and it's only used when it beats a simple guess. A tiny
> language model writes the note, and a check rejects it if a single number changes.

### 2:25 Different and honest
**[Next to step 15]**
> Our most important finding: in our simulation, truck chlorine fades below the minimum within a
> day or two in most tanks. That's evidence for the health board: a higher truck dose, or
> thresholds they set.
> TankLight tracks chlorine, not E. coli; official advisories come first; and the Inuktitut
> audio will be recorded with the community, not machine-translated.

### 2:50 Close
**[Kitchen mode]**
> Trucks today, pipes tomorrow: Inukjuak is already talking about a pipeline, and TankLight's
> records can give that plan evidence.
> TankLight: know your water is protected before you drink it. Thank you.

## If the demo fails

Say "here's the same run from the device logic" and show the terminal output of
`python app.py`: each scenario and the light it gives, in text. Don't debug on stage.

## Likely judge questions

| Question | Answer |
|---|---|
| How do you measure chlorine cheaply? | An ORP and pH probe, calibrated against a DPD test kit (the one water operators already use). For a real pilot, a reagent-free amperometric sensor that works in still water. |
| Does it detect E. coli? | No, and we say so. Pair it with a monthly field test that needs no electricity (Aquagenx CBT). TankLight covers the gap between those tests. |
| Won't the light be red all the time? | In our simulation it's often not green (82–94% of the time), because truck chlorine fades fast in a tank. That's the finding, not a bug: it's evidence for a higher truck dose, or thresholds set with the health board. They decide the thresholds, not us, and a pilot must settle it first, because a light that is always red gets ignored. |
| What about sewage? | The sewage tank outside has its own line on the display: how full, days until full, and a freezing warning if the tank heater fails. The sewage truck gets a pump-out plan; in simulation, 7–50% fewer hours with a full tank for the same stops. |
| What does it cost? | Prototype parts about $200–250 CAD; the target is under $100 at volume (an estimate). |
| Who maintains it? | Standard parts, a swappable probe cartridge, and local "water keepers" doing a monthly check. Spares go on the fall sealift. |
| Is the data real? | No, everything is simulated with placeholder numbers. Next step: real delivery logs and DPD readings with the municipality and KRG. |
| Where's the AI? | In the water office, not the kitchen. TimesFM 3.0 (Google's forecasting model, run locally on Apple silicon with MLX) forecasts next week's urgent-water demand, with blizzard days as a known input. It is scored against a "last 7 days" guess on the past 4 weeks and used only when it wins: in our simulated January it did (average error 1.21 vs 1.38 homes a day); in steadier July it didn't, so the plan used the simple guess. A 270M-parameter LLM (gemma3 through Ollama) rewords the plan in a graphflow workflow; a check keeps its note only if every home and number matches, otherwise the plain template goes out. The safety light stays plain rules, on purpose. |
| Why such small models? | They run offline on one office laptop, and the job is small: forecast one number a day, reword six lines. The check means a small model can't do harm. TimesFM's weights are non-commercial: fine for a demo; a real deployment needs Google's permission or another model. |
| Privacy? | Readings stay in the home. Community reports would be opt-in and combined, and the data belongs to the community. |

## Sources for the numbers

- $76.29 for 24 × 500 mL: photo in the challenge slides (Amenda Soucy).
- 0.2 mg/L minimum; "no barriers, no monitoring": [risk matrices, IJCH 2025](https://doi.org/10.1080/22423982.2025.2450877).
- Trucks fine, tanks low: [Cambridge Bay, Water Research 2025](https://pubmed.ncbi.nlm.nih.gov/41072346/).
- 33% ran out in a week, 37% don't drink tap water: [Kangiqsualujjuaq, J. Water & Health 2024](https://doi.org/10.2166/wh.2024.246).
- Inukjuak advisory, E. coli at the loading arm: [Nunatsiaq News, June 2026](https://nunatsiaq.com/stories/article/inukjuak-under-boil-water-advisory-after-e-coli-detected-at-water-plant/).
- SWOT: [York University Dahdaleh Institute](https://www.yorku.ca/dighr/project/safe-water-optimization-tool/).
- 534 → 188 hours without water (July; January 1,486 → 1,286): TankLight backtest, **simulated**.
- 7–50% fewer sewage-backup hours with priority pump-outs: **simulated**, 30 days, seeds 7 and 11, January and July.
