# fitlens.ai

AI-native fitness and nutrition coach MVP. Upload a meal photo to receive a transparent estimate of ingredients, portion size, calories, macros, and uncertainty.

## Sprint 1 scope

- Vite + React frontend with responsive mobile, tablet, and desktop layouts
- OpenAI Responses API Vision analysis
- Canvas image preprocessing at 512 x 512 before analysis
- Local-only IndexedDB meal history; no server database
- Vercel SPA rewrite configuration
- Nutrition dashboard for calories, protein, carbohydrates, and fat

## Latest analysis schema

Each analysis stores the following fields locally:

```json
{
  "name": "food name",
  "ingredients": ["visible ingredient"],
  "portionBasis": "one visible plate",
  "calories": 420,
  "protein": 38,
  "carbs": 24,
  "fat": 18,
  "confidence": 86,
  "fieldConfidence": { "calories": 82, "protein": 89, "carbs": 78, "fat": 80 },
  "assumptions": ["estimated dressing quantity"],
  "caveats": ["photo analysis cannot verify exact weight"],
  "reasoning": "short evidence-based explanation"
}
```

The prompt requires visible ingredients, portion basis, reasoning, assumptions, caveats, and both overall and field-level confidence. The response is requested with a strict JSON Schema through the Responses API so the UI receives a predictable shape.

## UI and design updates

- Reworked the visual language around the supplied reference: soft lavender palette, luminous orb treatment, glass panels, serif display typography, light borders, and calm spacing.
- Added a latest insight panel with overall confidence, per-field confidence bars, assumptions/care notes, reasoning, portion basis, and visible ingredients.
- Added responsive breakpoints for compact phones, tablets, and wide desktop screens.
- Fixed the previous corrupted text/JSX encoding so the app builds cleanly again.

## Local setup

```bash
npm install
npm run dev -- --host 127.0.0.1 --port 5171
```

Copy `.env.example` to `.env.local` and set:

```env
VITE_OPENAI_API_KEY=your_openai_api_key
VITE_OPENAI_MODEL=gpt-4.1-mini
```

Without an API key, the app uses a clearly marked sample analysis so the local UI can still be reviewed. For a public deployment, move the OpenAI request behind a server-side Vercel function so the API key is never exposed in browser code.

## Validation

- `npm install` completed successfully
- `npm run build` completed successfully
- Vite development server verified on port `5171`
