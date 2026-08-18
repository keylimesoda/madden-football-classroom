# Madden Football Classroom — product and curriculum v0

**Working promise:** Learn football. Play Madden better.

MFC is a public, open-source, browser-first curriculum for people who already play Madden but want to understand what they are seeing and decide better before, during, and after a snap. It is not a money-play catalog.

## Product decisions locked with Ric

- Target: Madden NFL 27 first. Madden 26 examples may support concepts, but all mechanics carry a game/version label.
- Audience: experienced Madden players without deep football knowledge.
- Context: realistic, full-length, Franchise-minded games. Teach the normal player who calls plays on both sides, plays QB/ballcarrier on offense, and users defenders on defense.
- Learning unit: a 5–10 minute micro-course with lessons, an interactive read, a short quiz, and a self-checked Practice Mode lab.
- Completion: local browser progress and an attractive MFC course badge. No account requirement.
- Voice: accurate, helpful, lightly collegiate, and fun enough that the learner comes back.
- Visual rule: original Xs-and-Os diagrams are the primary explanation. Use animated diagrams when motion teaches timing, spacing, rotation, or leverage.
- Community: recommendations and corrections enter a review queue; nothing publishes automatically.
- Publishing: GitHub-backed, static-hostable site. Content must remain structured and reviewable.

## Recommended platform

Use a static React/TypeScript site deployed through GitHub Pages, with lesson content stored as typed JSON/MDX and diagrams stored as versioned `PlaySpec` JSON.

Do **not** use generic Markdown as the visual/learning system. Markdown may hold light prose, but the page contract is component-driven:

- `ConceptCard`
- `ReadTheLook`
- `PlayDiagram`
- `MaddenTranslation`
- `FilmRoom`
- `KnowledgeCheck`
- `PracticeLab`
- `SourcesDrawer`
- `CourseBadge`

### Diagram engine: MFC Playboard

Build a small first-party SVG engine rather than adopting a generic graph editor. Football diagrams have a stable vocabulary: field, offense/defense tokens, assignments, routes, zones, ball path, phases, labels, and annotations. A custom engine can be:

- authored as semantic JSON rather than screenshots;
- responsive and accessible;
- animated with native Web Animations/CSS or Motion for React;
- replayable, scrub-able, and printable;
- testable (all diagrams can validate token/route references);
- reused for quizzes and contributor submissions.

A future contributor editor can sit above the same schema. Start with authored diagrams, not an editor.

### Minimal `PlaySpec` shape

```ts
interface PlaySpec {
  id: string;
  title: string;
  orientation: 'offense-bottom' | 'offense-top';
  tokens: Array<{ id: string; side: 'offense' | 'defense'; label: string; x: number; y: number }>;
  routes: Array<{ token: string; kind: 'route' | 'motion' | 'ball' | 'block'; points: [number, number][] }>;
  zones?: Array<{ label: string; kind: 'deep' | 'curl-flat' | 'hook'; x: number; y: number; width: number; height: number }>;
  phases: Array<{ label: string; atMs: number; show: string[]; note: string }>;
  sourceRefs: string[];
}
```

## Lesson contract

Every MFC micro-course should answer six questions in this order:

1. **Spot it** — What should I notice at the line?
2. **Name it** — What is the concept called in MFC language?
3. **Why it matters** — What advantage or danger does it create?
4. **Madden translation** — What can I actually call, adjust, or control?
5. **Counter / constraint** — What can punish the obvious answer?
6. **Practice it** — What can I set up in Practice Mode in under five minutes?

Each course includes:

- 1 immediate practical win;
- 1 animated playboard;
- 1–3 short knowledge checks;
- 1 self-checked lab;
- a concise source list with source type, title, version/date, and direct link;
- explicit labels: `Football concept`, `Madden 27 behavior`, `Madden 26 carryover`, or `Community observation`.

## Initial curriculum map

### MFC 101 — See the Field

| Course | Learner win |
| --- | --- |
| 101.1 The pre-snap scan | Identify personnel, shell, box count, and leverage before calling for the ball. |
| 101.2 Shells: one high and two high | Recognize the safety picture and make a one-sentence plan. |
| 101.3 Count the box | Decide whether the run has numbers before treating it as a personality test. |
| 101.4 Leverage is a clue, not a prophecy | Read inside/outside and press/off alignment without inventing certainty. |
| 101.5 Formation families | Recognize the geometry of singleback, pistol, gun, bunch, trips, stack, and empty. |
| 101.6 The calm plan | Make a primary answer and a checkdown/escape plan before the snap. |

**Badge:** Field Vision I

### MFC 102 — Run the Football

| Course | Learner win |
| --- | --- |
| 102.1 Gaps and numbers | Explain where a run is designed to hit and what the defense owns. |
| 102.2 Inside zone | Read the front-side double team and cutback lane. |
| 102.3 Outside zone and stretch | Identify edge leverage and make one decisive cut. |
| 102.4 Power and counter | Find the puller and the kick-out / wrap picture. |
| 102.5 Run defense for normal humans | User a fit without turning every safety into a guided missile. |
| 102.6 ID Mike in Madden 27 | Use Madden’s updated run/protection targeting deliberately. |

**Badge:** Ground Game I

### MFC 103 — Throw the Football

| Course | Learner win |
| --- | --- |
| 103.1 Route families and timing | Recognize the purpose of common routes. |
| 103.2 Spacing | Stop placing two receivers in the same defender’s lunch tray. |
| 103.3 Stick | Read a simple flat defender conflict. |
| 103.4 Flood | Create and read a three-level sideline stretch. |
| 103.5 Mesh | Find the man/zone answer without staring at the crossing traffic. |
| 103.6 Smash and Cover 2 | Read the corner and attack the high-low conflict. |
| 103.7 Passing tools | Apply hot routes, motion, protection, and Madden 27 check-and-release routes with intent. |

**Badge:** Passing Game I

### MFC 104 — Defend the Field

| Course | Learner win |
| --- | --- |
| 104.1 Fronts, boxes, and run fits | Pick a defense with an actual answer for the box. |
| 104.2 Cover 3 | Know the deep/flat stresses and user a middle defender responsibly. |
| 104.3 Cover 2 and Tampa 2 | Understand the middle opening and sideline constraint. |
| 104.4 Quarters, palms, Cover 6 | Learn the “why” before turning on match checks. |
| 104.5 User defense | Take away a real conflict instead of freelancing into orbit. |
| 104.6 Madden 27 coverage hubs and macros | Set a global/preset answer, then know its tradeoff. |

**Badge:** Defensive IQ I

### MFC 201 — Win Situations

Third down, red zone, backed-up offense, two-minute, four-minute, goal line, short yardage, and clock decisions.

**Badge:** Situational Football I

### MFC 202 — Build Your Scheme

Call sheets, audibles, core concepts, formation complements, personnel, custom adjustments, tendency management, and Franchise-style game plans.

**Badge:** Coordinator I

### MFC 301 — Film Room

Opponent scouting, self-scouting, postgame diagnosis, recognizing counters, version drift, and responsibly separating a sound concept from an animation exploit.

**Badge:** Film Room I

## Research and citation policy

Use a source ladder. Claims should cite the best available tier; do not cite a tutorial creator for a control mapping when EA documents it.

1. **Official Madden source** — EA controls hub, Gridiron Notes, in-game capture. Required for control mappings and stated game features.
2. **Direct Madden observation** — MFC-captured test steps, platform/version/patch date, replay evidence. Label as `observed`, not “verified.”
3. **Coaching / football analysis** — reputable coaching clinics, analyst film study, rules/terminology material. Required for football-concept claims.
4. **Madden specialists** — Deuce Close, Zag, Huddle.gg, MCS competitors, and others. Great for current practice, playbook locations, and counterexamples; label the game version and distinguish opinion from mechanic.
5. **Community reports** — leads for review, never sole support for an authoritative claim.

Every external video gets a `Watch` card with creator, exact title, URL, version context, why it is relevant, and a short cited takeaway. Embed/link rather than download or re-publish third-party video. Use original MFC diagrams and MFC-owned captures as the primary teaching media.

## Initial evidence register

- EA, *Madden NFL 27 — Gameplay Deep Dive*: official coverage of updated ID Mike, streamlined protection controls, Global Coverage Adjustment hub, and custom/preset adjustments. https://www.ea.com/games/madden-nfl/madden-nfl-27/news/madden-27-gameplay
- EA, *Madden NFL 27 Controls Hub*: official platform-specific control reference. https://www.ea.com/games/madden-nfl/madden-nfl-27/controls-hub
- EA, *Madden NFL 27 Gameplay*: official overview of WR/DB battles, short-yardage mechanics, timing-based catching, and gameplanning. https://www.ea.com/games/madden-nfl/madden-nfl-27/features/m27-gameplay
- Huddle.gg, *Madden 27 Playbooks*: searchable playbook/formation surface useful for mapping concepts to available plays. https://huddle.gg/playbooks
- Huddle.gg, *All Formations in Madden 27*: current formation family reference. https://huddle.gg/playbooks/formations
- Motion for React, *SVG animation*: supports a first-party SVG playboard with paths, token motion, and viewBox animation. https://motion.dev/docs/react-svg-animation

## Contribution model

GitHub issues/forms should offer four templates:

- **Correction** — claim URL, affected version, source/evidence, proposed change.
- **Source recommendation** — source, what it supports, creator/copyright context.
- **Lesson proposal** — learner win, concept, Madden translation, diagram outline, sources.
- **Madden version drift** — prior behavior, current behavior, game/platform/patch, reproduction steps, capture if available.

A maintainer must approve content. Contributors retain attribution. MFC uses original diagrams and only embeds/links third-party video unless the creator gives written permission.

## Design rules for attention and accessibility

- One screen, one decision.
- Never hide the answer behind a paragraph if a diagram can reveal it.
- Chunk all explanations into 30–90 second moments.
- Use replay, pause, reduced-motion, and static-diagram controls.
- Do not encode offense/defense or coverage zones with color alone; include token shape/labels/patterns.
- Show a progress bar and a visible finish line in every course.
- Award badges for demonstrated completion, not streaks or engagement farming.
