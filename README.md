# Exercise API

The [Your Move Exercise API](https://ymove.app/exercise-api) is an exercise database API with **2,005+ exercises and 2,600+ HD videos**, filmed with trainers and physiotherapists. No AI-generated clips, no GIFs. Every exercise ships with an HD video (HLS + MP4), thumbnails, step-by-step instructions and primary and secondary muscle data, across 15 muscle groups and 37 equipment types.

On the same key: workout generation, multi-week training programs and AI posture analysis.

- **Docs:** [ymove.app/exercise-api/docs](https://ymove.app/exercise-api/docs)
- **OpenAPI spec:** [exercise-api.ymove.app/api/v2/openapi.json](https://exercise-api.ymove.app/api/v2/openapi.json)
- **Get an API key:** [ymove.app/exercise-api/signup](https://ymove.app/exercise-api/signup) (trial key in minutes)

## Quickstart

### 1. REST

Base URL: `https://exercise-api.ymove.app/api/v2`. Send your key in the `X-API-Key` header.

```bash
curl -H "X-API-Key: your_api_key" \
  "https://exercise-api.ymove.app/api/v2/exercises?muscleGroup=chest&equipment=dumbbell&pageSize=5"
```

### 2. TypeScript SDK

```bash
npm install ymove-exercise-api
```

```typescript
import { YMoveClient } from 'ymove-exercise-api';

const ymove = new YMoveClient('your_api_key');

const { data: exercises } = await ymove.exercises.list({ muscleGroup: 'chest', equipment: 'dumbbell' });
const workout = await ymove.workouts.generate({ muscleGroup: 'chest', difficulty: 'intermediate', exerciseCount: 6 });
const program = await ymove.programs.generate({ goal: 'muscle_building', daysPerWeek: 4, weeks: 4 });
```

Repo: [ymove-app/exercise-api-sdk](https://github.com/ymove-app/exercise-api-sdk) | npm: [ymove-exercise-api](https://www.npmjs.com/package/ymove-exercise-api)

### 3. MCP server (Claude, Cursor and other AI tools)

Hosted, no install:

```bash
claude mcp add --transport http ymove https://exercise-api.ymove.app/mcp --header "X-API-Key: your_api_key"
```

Or run it locally with npx:

```bash
claude mcp add ymove -e YMOVE_API_KEY=your_api_key -- npx ymove-exercise-mcp
```

Tools: `search_exercises`, `get_exercise`, `generate_workout`, `generate_program`, `list_muscle_groups`, `list_exercise_types`.

Repo with Cursor and Claude Desktop config: [ymove-app/exercise-api-mcp](https://github.com/ymove-app/exercise-api-mcp) | npm: [ymove-exercise-mcp](https://www.npmjs.com/package/ymove-exercise-mcp)

## Endpoints

| Method | Endpoint | What it does |
|---|---|---|
| GET | `/exercises` | List and search exercises (muscle group, equipment, difficulty, type, text search) |
| GET | `/exercises/{id}` | One exercise by ID or slug, with video URLs, thumbnails, instructions and muscles |
| GET | `/exercises/muscle-groups` | Muscle groups with exercise counts |
| GET | `/exercises/equipment` | Equipment types with exercise counts |
| GET | `/exercises/{id}/body-map` | Muscles worked, as an SVG image |
| GET | `/workouts/generate` | A structured workout with sets, reps and rest |
| GET | `/programs/generate` | A multi-week training program |
| POST | `/posture/analyze` | AI form analysis from an exercise video |
| GET | `/usage` | Your usage and limits |

Full reference with parameters and response examples: [ymove.app/exercise-api/docs](https://ymove.app/exercise-api/docs).

## Exercise library

- **[Top 100 exercises](TOP-100.md)**: the exercises developers request most, with portrait thumbnails.
- **[Full exercise list](EXERCISES.md)**: every exercise, grouped by muscle group.

## 25 free exercise videos

Royalty-free HD exercise videos (MP4, 720p, portrait) in [`free-videos/`](free-videos), free for commercial use. Same set as [ymove.app/free-exercise-videos](https://ymove.app/free-exercise-videos); license in [free-videos/README.md](free-videos/README.md). Click a thumbnail for the MP4.

<table>
<tr><td align="center" valign="top" width="20%"><a href="free-videos/barbell-back-squat.mp4"><img src="free-videos/barbell-back-squat.jpg" width="150" alt="Barbell Back Squat exercise video"></a><br><sub><b>Barbell Back Squat</b><br>Quads · Barbell</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/barbell-bench-press-122b71.mp4"><img src="free-videos/barbell-bench-press-122b71.jpg" width="150" alt="Barbell Bench Press exercise video"></a><br><sub><b>Barbell Bench Press</b><br>Chest · Barbell</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/barbell-deadlift.mp4"><img src="free-videos/barbell-deadlift.jpg" width="150" alt="Barbell Deadlift exercise video"></a><br><sub><b>Barbell Deadlift</b><br>Full body · Barbell</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/dumbbell-lateral-raise-27a4de.mp4"><img src="free-videos/dumbbell-lateral-raise-27a4de.jpg" width="150" alt="Dumbbell Lateral Raise exercise video"></a><br><sub><b>Dumbbell Lateral Raise</b><br>Shoulders · Dumbbell</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/hammer-curls.mp4"><img src="free-videos/hammer-curls.jpg" width="150" alt="Hammer Curls exercise video"></a><br><sub><b>Hammer Curls</b><br>Biceps · Dumbbell</sub></td></tr>
<tr><td align="center" valign="top" width="20%"><a href="free-videos/single-arm-dumbbell-row-legs-apart.mp4"><img src="free-videos/single-arm-dumbbell-row-legs-apart.jpg" width="150" alt="Single Arm Dumbbell Row - Legs apart exercise video"></a><br><sub><b>Single Arm Dumbbell Row - Legs apart</b><br>Back · Dumbbell</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/dumbbell-goblet-squat-202e4f.mp4"><img src="free-videos/dumbbell-goblet-squat-202e4f.jpg" width="150" alt="Dumbbell Goblet Squat exercise video"></a><br><sub><b>Dumbbell Goblet Squat</b><br>Quads · Dumbbell</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/kettlebell-swing.mp4"><img src="free-videos/kettlebell-swing.jpg" width="150" alt="Kettlebell swing exercise video"></a><br><sub><b>Kettlebell swing</b><br>Core · Kettlebell</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/kettlebell-push-press.mp4"><img src="free-videos/kettlebell-push-press.jpg" width="150" alt="Kettlebell Push Press exercise video"></a><br><sub><b>Kettlebell Push Press</b><br>Shoulders · Kettlebell</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/kettlebell-romanian-deadlift.mp4"><img src="free-videos/kettlebell-romanian-deadlift.jpg" width="150" alt="Kettlebell Romanian Deadlift exercise video"></a><br><sub><b>Kettlebell Romanian Deadlift</b><br>Hamstrings · Kettlebell</sub></td></tr>
<tr><td align="center" valign="top" width="20%"><a href="free-videos/goblet-squat-with-kettlebell.mp4"><img src="free-videos/goblet-squat-with-kettlebell.jpg" width="150" alt="Goblet Squat with Kettlebell exercise video"></a><br><sub><b>Goblet Squat with Kettlebell</b><br>Quads · Kettlebell</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/cable-crossover-mid-b24dfe.mp4"><img src="free-videos/cable-crossover-mid-b24dfe.jpg" width="150" alt="Cable Crossover (Mid) exercise video"></a><br><sub><b>Cable Crossover (Mid)</b><br>Chest · Cable</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/lying-cable-leg-curl.mp4"><img src="free-videos/lying-cable-leg-curl.jpg" width="150" alt="Lying Cable Leg Curl exercise video"></a><br><sub><b>Lying Cable Leg Curl</b><br>Quads · Cable</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/cable-woodchop-high-to-low-842bc7.mp4"><img src="free-videos/cable-woodchop-high-to-low-842bc7.jpg" width="150" alt="Cable Woodchop (High to Low) exercise video"></a><br><sub><b>Cable Woodchop (High to Low)</b><br>Core · Cable</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/lat-pulldown.mp4"><img src="free-videos/lat-pulldown.jpg" width="150" alt="Lat Pulldown exercise video"></a><br><sub><b>Lat Pulldown</b><br>Back · Cable</sub></td></tr>
<tr><td align="center" valign="top" width="20%"><a href="free-videos/seated-cable-row-close-v-bar-bccf4f.mp4"><img src="free-videos/seated-cable-row-close-v-bar-bccf4f.jpg" width="150" alt="Seated Cable Row close V bar exercise video"></a><br><sub><b>Seated Cable Row close V bar</b><br>Back · Cable</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/seated-machine-chest-press.mp4"><img src="free-videos/seated-machine-chest-press.jpg" width="150" alt="Seated Machine Chest Press exercise video"></a><br><sub><b>Seated Machine Chest Press</b><br>Chest · Machine</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/cable-lateral-raise.mp4"><img src="free-videos/cable-lateral-raise.jpg" width="150" alt="Cable Lateral Raise exercise video"></a><br><sub><b>Cable Lateral Raise</b><br>Shoulders · Cable</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/cable-rope-face-pull.mp4"><img src="free-videos/cable-rope-face-pull.jpg" width="150" alt="Cable Rope Face Pull exercise video"></a><br><sub><b>Cable Rope Face Pull</b><br>Shoulders · Cable</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/cable-bicep-curl-rope-23790c.mp4"><img src="free-videos/cable-bicep-curl-rope-23790c.jpg" width="150" alt="Cable Bicep Curl rope exercise video"></a><br><sub><b>Cable Bicep Curl rope</b><br>Biceps · Cable</sub></td></tr>
<tr><td align="center" valign="top" width="20%"><a href="free-videos/cable-tricep-pushdown.mp4"><img src="free-videos/cable-tricep-pushdown.jpg" width="150" alt="Cable Tricep Pushdown exercise video"></a><br><sub><b>Cable Tricep Pushdown</b><br>Triceps · Cable</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/overhead-cable-rope-extension.mp4"><img src="free-videos/overhead-cable-rope-extension.jpg" width="150" alt="Overhead Cable Rope Extension exercise video"></a><br><sub><b>Overhead Cable Rope Extension</b><br>Triceps · Cable</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/leg-extension.mp4"><img src="free-videos/leg-extension.jpg" width="150" alt="Leg Extension exercise video"></a><br><sub><b>Leg Extension</b><br>Quads · Machine</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/leg-press.mp4"><img src="free-videos/leg-press.jpg" width="150" alt="Leg Press exercise video"></a><br><sub><b>Leg Press</b><br>Quads · Machine</sub></td><td align="center" valign="top" width="20%"><a href="free-videos/glute-kickback-machine.mp4"><img src="free-videos/glute-kickback-machine.jpg" width="150" alt="Glute Kickback Machine exercise video"></a><br><sub><b>Glute Kickback Machine</b><br>Glutes · Machine</sub></td></tr>
</table>

## Example apps

Built on the SDK: [workout generator](https://github.com/ymove-app/ymove-workout-generator), [exercise browser](https://github.com/ymove-app/ymove-exercise-browser), [Expo mobile app](https://github.com/ymove-app/ymove-mobile-fitness-expo).

## Links

- Product page: [ymove.app/exercise-api](https://ymove.app/exercise-api)
- Pricing: [ymove.app/exercise-api/pricing](https://ymove.app/exercise-api/pricing)
- Claude Code Skill: [ymove.app/exercise-api/skill](https://ymove.app/exercise-api/skill)
- Compared with ExerciseDB: [ymove.app/exercise-api/compare](https://ymove.app/exercise-api/compare)
- Contact: contact@ymove.app
