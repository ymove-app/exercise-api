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

## Example apps

Built on the SDK: [workout generator](https://github.com/ymove-app/ymove-workout-generator), [exercise browser](https://github.com/ymove-app/ymove-exercise-browser), [Expo mobile app](https://github.com/ymove-app/ymove-mobile-fitness-expo).

## Links

- Product page: [ymove.app/exercise-api](https://ymove.app/exercise-api)
- Pricing: [ymove.app/exercise-api/pricing](https://ymove.app/exercise-api/pricing)
- Claude Code Skill: [ymove.app/exercise-api/skill](https://ymove.app/exercise-api/skill)
- Compared with ExerciseDB: [ymove.app/exercise-api/compare](https://ymove.app/exercise-api/compare)
- Contact: contact@ymove.app
