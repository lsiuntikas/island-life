# Island life

A tiny society that lives on its own. Watch a few dozen islanders survive, make friends, fight, trade, build homes, raise families and grow old over generations, or step into any one of their lives in first person.

Everything runs in a single HTML file in the browser: no install, no build step, no server.

> **Two versions**
> - **`index.html`** (version 2): watch the island **and** play as any islander in first person.
> - **`watch.html`** (version 1): the original watch-only simulation.

---

## What happens on the island

Every islander is an autonomous agent with:

- **Needs:** hunger, thirst, tiredness, loneliness and health.
- **A personality:** kindness, aggression and ambition, partly inherited from their parents.
- **Relationships:** an opinion of every other islander, from enemy to close friend.
- **Memory of the map:** they only know the springs, bushes and rocks they have seen, or have been told about.

Each moment, every islander scores everything they could do and picks what seems best right now (a "utility AI"). Nothing is scripted. Villages, friendships, feuds and reputations all emerge from those choices.

### Survival
- Drink at springs, eat or pick berries, sleep, and explore to find more resources.
- Fish from the beach, or build a boat and sail out to the fishing grounds.

### Helping and hurting
- **Helpful:** talking (which shares map knowledge), giving food or water, nursing the wounded, defending friends, helping build, giving wood.
- **Hostile:** stealing and attacking.
- **Witnesses:** onlookers change their opinion of whoever helped or hurt someone, so reputations spread.

### Economy
- Gather wood, mine stone, and trade goods. A trade happens only when both sides come out better off.
- Homes grow in four stages: **hut → cabin → house → manor**. Bigger homes give better sleep.
- **Sunberries** grow only on a second, faraway island. Islanders treat them as a luxury and pay well for them.

### Families and generations
- A man and a woman who stay close friends for long enough become partners.
- Healthy couples with a home can have children. Children follow and are fed by their parents, then grow up.
- Old islanders die of old age and pass their house, boat and car to their partner or eldest child.

### Crime and the labyrinth
- **Murder:** killing someone who didn't attack you first makes you *wanted*.
- **Arrest:** islanders hunt the killer down. A tough killer can fight off one person, but not a group.
- **The labyrinth:** prisoners are taken to a separate stone maze. They get bread and water, but must find the way out themselves.
- **Visiting:** a hatch in the middle of the main island lets anyone climb down and explore it.

---

## Playing in first person (version 2)

Press **Play as someone**, or open any islander's card and press **Play as …**. The other islanders treat you like anyone else. They remember what you did, gossip about it, may become your partner, or may come to arrest you. When you die, you can continue as one of your children.

### Controls (computer)

| Key | Action |
|---|---|
| **W A S D** | Walk (in a car or boat: drive or sail and steer) |
| **Shift** | Run, or go faster |
| **Mouse** | Look around (click the view to capture the mouse) |
| **E** | Main action for what you're facing: drink, eat, chop, mine, talk, fish, open the hatch… |
| **F** | Pick berries or sunberries to carry |
| **G** | Give food or water to the person you're facing |
| **V** | Trade with the person you're facing |
| **H** | Help someone build |
| **C** | Have a child with your partner |
| **T / K** | Steal / attack |
| **J** | Arrest a wanted killer |
| **B** | Build or upgrade your home |
| **N** | Build a boat at the shore; get in or out of your boat |
| **U** | Build a car; get in or out of your car |
| **Q / R** | Eat from your bag / drink from your water skin |
| **Z** | Sleep |
| **X** | Stop what you're doing |
| **Space** | Hard brake while driving |
| **Esc** | Pause, choose time speed, or stop playing |

Greyed-out actions always explain why they aren't possible yet, for example *"you need 4 more wood"*.

### Controls (phone)
- Joystick on the left to move, drag anywhere else to look.
- Tap an action button to do it, plus **Run** and **Pause** buttons.

### Time
- In first person a day lasts about a minute, so the other islanders walk at your pace. You can choose slow, normal or fast in the pause menu.
- Watch mode runs at 1×, 2×, 5× or 10×.

---

## How it's built

| Part | Language | Roughly |
|---|---|---|
| Simulation: agents, needs, decisions, economy, families, labyrinth | JavaScript | 1,300 lines |
| 3D view, first-person play, on-screen display, phone controls | JavaScript | 1,900 lines |
| Page layout and styles, light and dark mode | HTML and CSS | 500 lines |

- **3D graphics:** [Three.js](https://threejs.org/) r147, loaded from a CDN, plus its `OrbitControls` and `CSS2DRenderer` add-ons.
- **No other dependencies.**
- **Same island every time:** the island and its first settlers come from a seeded random number generator. The same *island number* in Settings always grows the same starting island, although what happens afterwards changes when you play.
- **Saved settings:** settings like shadows, names and time speed are saved in the visitor's own browser with `localStorage`.

### The decision loop, in short

```text
every tick, for every islander:
  needs grow (hunger, thirst, tiredness, loneliness)
  look around and remember new resources
  score every possible action, for example
      drink  = urgency(thirst) × closeness of known water
      help   = kindness × their need² × friendship
      attack = aggression² × hunger × dislike × (fewer friends nearby)
  keep doing the current action unless something else is clearly better
  carry out the action (walk there, then do it)
```

---

## Credits

- Built with [Three.js](https://threejs.org/).
- Fonts: [Bricolage Grotesque](https://fonts.google.com/specimen/Bricolage+Grotesque) and [Atkinson Hyperlegible](https://fonts.google.com/specimen/Atkinson+Hyperlegible) from Google Fonts.

## License

MIT
