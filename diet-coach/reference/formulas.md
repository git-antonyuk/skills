# Formulas & target ranges

All math in metric (kg, cm). Round final targets sensibly (calories to nearest 10,
protein to nearest 5 g).

## 1. BMR — Mifflin-St Jeor (most accurate general equation)

```
BMR (men)   = 10·weight_kg + 6.25·height_cm − 5·age + 5
BMR (women) = 10·weight_kg + 6.25·height_cm − 5·age − 161
```

Requires height — if missing, ask the user; do not estimate.

## 2. TDEE — apply activity multiplier (job/lifestyle activity, not training)

| Level             | Multiplier | Typical case |
|-------------------|-----------|--------------|
| Sedentary         | 1.20      | desk job, little movement |
| Lightly active    | 1.375     | light exercise 1–3×/wk |
| Moderately active | 1.55      | exercise 3–5×/wk |
| Very active       | 1.725     | hard exercise 6–7×/wk |
| Extra active      | 1.90      | physical job + training |

```
TDEE = BMR × multiplier
```

Training is counted separately via steps/NEAT and the multiplier — don't
double-count by also adding workout calories on top.

## 3. Calorie target (deficit)

```
calorie_target = TDEE − deficit
```

- Deficit **500–750 kcal/day** ≈ **0.5–1 kg/week**.
- Scale the deficit to the target rate, fatigue, and how much fat there is to
  lose. More body fat → can sustain a larger deficit; leaner → smaller.

**Calorie floor:** don't program below ~1500–1600 kcal/day for men or ~1200 for
women without professional supervision. If the floor forces a sub-target rate,
accept the slower rate or raise output (steps), don't starve.

## 4. Rate of loss

- Target **0.5–1.0% of body weight per week**.
- Faster than ~1%/wk risks muscle loss and rebound, especially as the user leans
  out. Re-evaluate the rate as weight drops.

## 5. Protein

```
protein_g = 1.8–2.7 g per kg of body weight
```

- Use the higher end during an aggressive deficit and to blunt hunger (up to
  ~3 g/kg helps satiety).
- Protein is the priority macro in a deficit — it preserves muscle so the result
  is "toned", not "skinny-fat".

## 6. Steps / NEAT

- Target **8,000–12,000 steps/day** as background fat-burning that doesn't tax
  recovery the way extra cardio can.

## 7. Recompute trigger

Recompute TDEE and all targets whenever weight changes meaningfully (≈ every
2–3 kg) or activity/training changes. Targets are not set once — they drift down
as weight drops.
