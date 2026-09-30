# Generations City

**Build your Friend. Build your district. Build the city.**

**Builder / contact:** [420JB](https://github.com/420JB) · Twitter: [@CallOfTheStars](https://twitter.com/CallOfTheStars)  
**Category:** **Token Activity** (primary) · **Economy Potential** (secondary)  
**Playable demo:** https://generations-city-production.up.railway.app/  
**Source:** https://github.com/420JB/generations-city/tree/ecb3d6ba8ce3576affbd656fa2a22b52fb4b91de

> **One sentence:** Generations City turns every simulated $RAREFRIENDS spend into visible, persistent development of a Rare Friend property, its family district, and the shared city around it.

## What it is

Generations City is a social strategy city built around nine Rare Friends family districts. Each active Friend receives a property; spending RF grows that building, unlocks architecture, earns patron recognition and badges, changes district monument control, and can swing the Capital or the individual City Crown.

The core idea is simple: **RF spending is not a fee attached to the game — spending RF is the action that physically builds the world.**

**Everything in this Vibeathon build is simulated.** All RF is labelled **SIMULATED RF**. No real tokens move, no wallet is connected, and nothing is written on-chain.

## 30-second judge path

1. Open **Build Board**.
2. Find **Demo Friend #812**, which starts **38 RF from Tier 4** and can capture **The Grand Fountain** from Sparkling.
3. Press **WARP**.
4. Contribute exactly **38 SIMULATED RF**.
5. Watch the building grow into Tier 4 and The Grand Fountain move to the **Family District**.
6. You earn **Closer** and **Kingmaker**, and **District Radio** records the event.
7. Reopen Build Board / Radio: **Demo Friend #288** is now **63 RF from Tier 3**, which can make Family the **Capital**.

The in-app **Demo Guide** walks through this path and updates from real game state. **Reset Demo** restores the starting scenario.

## What to try after the core loop

- **District Radio → Rally Calls:** live strategic recommendations recomputed after every move. Completed objectives disappear and new opportunities surface.
- **Architect Mode:** customize your own property. Owner spending separately raises Architect Level.
- **Property media:** install a billboard, upload an image, add a short owner message, then click the billboard in-world to open its media viewer. Links are intentionally blocked.
- **District competition:** capture tier-based civic monuments, fight for the prestige-only Capital, or chase the **City Crown** for tallest building.
- **Patronage:** contribute to another Friend's building and earn increasingly visible recognition on that property.
- **Demo Tools → Simulate Family growth:** activates deterministic simulated residents through the real plot allocator. The first click opens **Ward II**; the next fills Ward II and opens **Ward III**, demonstrating that districts expand independently as more Friends become active.

## RF rules and costs

Building tiers are based on cumulative RF built:

| Tier | Total RF built |
|---|---:|
| Tier 1 | 100 RF |
| Tier 2 | 500 RF |
| Tier 3 | 2,500 RF |
| Tier 4 | 10,000 RF |
| Tier 5 | 50,000 RF |
| Tier 6 | 250,000 RF |

**Total RF Built** includes both owner and community contributions. **Owner RF Built** is tracked separately and is the only spend that raises the owner's Architect progression.

Community patron recognition also grows with support to one property, from supporter-list presence through increasingly prominent exterior recognition. The Capital is **prestige only** and provides no scoring multiplier or economic snowball.

## City scale

The city does **not** pre-create every Rare Friend property. A building is created when a Friend becomes active.

The world hierarchy is:

`City → District → Ward → Plot → Building`

Each of the nine family districts expands independently. Wards are generated procedurally and deterministically as plots fill. The demo starts with roughly 180 buildings and uses level-of-detail rendering plus viewport culling so the city remains navigable as it grows.

The demo-only growth control uses the same `allocatePlot()` + `newBuilding()` path as the underlying model; it does not fake ward geometry by toggling a visual state.

## Stack / FriendSDK status

**Stack:** React · TypeScript · Vite · SVG world renderer · CSS · localStorage · Vitest · Playwright

**FriendSDK:** not used in this MVP.

Generations City needs a full-viewport shared-world model with persistent building/patron/history state, rich property customization, uploaded property media, procedural district growth, and its own city camera/renderer. For the Vibeathon build, those systems run as deterministic local state behind small identity/data boundaries. A production version would replace the demo identity/economy adapters with wallet ownership, backend/shared state, and chain/indexer integration.

## Production path / live readiness

The Vibeathon build is intentionally structured so taking the core experience live is an **integration and infrastructure step, not a gameplay rewrite**. The economy, allocation, progression, competition, ward-growth and strategy systems are already implemented as deterministic TypeScript game logic, while demo-only identity and persistence sit behind clear boundaries.

A production rollout would primarily replace or add:

- demo identity → wallet connection + Rare Friend ownership lookup;
- local browser state → authoritative shared backend/database state;
- SIMULATED RF balance changes → live RF settlement / transaction verification;
- local event history → indexed on-chain/backend history and reconciliation;
- browser-local billboard uploads → hosted media storage with moderation/reporting controls;
- demo rival/growth actions → real user activity and production indexing.

That means the existing city renderer, buildings, ward allocator, RF progression, Architect system, patronage, monuments, Capital, Crown, Rally Calls, billboards and judge-facing interaction model can remain largely intact while the adapters underneath them are connected to live services. Security review, transaction design, moderation and production operations would still be required before real funds are enabled.

## Wallet / network requirements

None for this demo.

- No wallet connection
- No chain/network selection
- No token approval or signature
- No real RF spending

## Controls

- **Click/tap** buildings, map controls, Build Board entries, Radio cards and HUD actions.
- **WARP** jumps the camera to a strategic building.
- **Mouse/touch pan and zoom** navigate the city.
- **City overview** returns to an automatically framed overview.
- **Reset Demo** restores the seeded judge scenario.

## Checks

Final submitted source commit: `ecb3d6ba8ce3576affbd656fa2a22b52fb4b91de`

- `npm run lint` — passed
- `npm run test` — **119/119 passed**
- `npm run test:e2e` — **28/28 passed**, parallel, first attempt on the final pass
- `npm run build` — passed
- `git diff --check` — clean
- Railway production deployment for the submitted commit — successful

Automated coverage includes the 38 RF monument-capture path, Capital progression, strategic Rally Calls, clickable property media and link blocking, mobile build reveal, deterministic district growth through Ward II/III, reset behavior, family art integrity, scaling/allocation, competition rules and production rendering behavior.

## Known limitations

- This is a deterministic browser demo using `localStorage`, not a live shared backend. Different browsers do not share city state.
- All Friends, users, RF balances, rival moves and district-growth residents in the demo are simulated.
- The hackathon monument/Capital model uses simplified cumulative tier counts. A production seasonal system should normalize competition against active seasonal participation rather than raw family supply.
- Uploaded billboard media is stored locally in the browser. Production media needs server storage, moderation, reporting and content controls.
- No live token settlement, wallet ownership verification, marketplace, ad rental system or chain indexer is included.

## Credits

Designed and built for the Rare Friends Vibeathon by **420JB**. Rare Friends family silhouette assets used for district identity were supplied for the hackathon build; the source repository documents their derivation/provenance and keeps the supplied source paths unchanged. The project was built with AI-assisted development and testing.
