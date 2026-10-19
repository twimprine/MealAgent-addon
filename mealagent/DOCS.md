# MealAgent

Plans your household's meals with your Home Assistant AI Task, puts them in a calendar and puts what you need to buy
on a to-do list.

## Options

| Option | Default | What it is |
|--------|---------|------------|
| `ai_task_entity` | `ai_task.claude_ai_task` | The AI Task entity that proposes meals and reads pantry photos. |
| `calendar_entity` | `calendar.meal_plan` | The calendar that receives one event per meal. |
| `todo_entity` | `todo.groceries` | The to-do list that receives the shopping items. |

## First run

Open MealAgent from the sidebar: Setup, then Pantry (photos), then This week, Plan my week.

Every Home Assistant user sees MealAgent in the sidebar. Anyone with an HA login can change its settings and allergy profiles, so only give HA accounts to people you trust with that.

## What it stores

Your setup, pantry list and a plan per week are JSON files in the App's `/data` folder. Pantry photos are shrunk,
stripped of metadata such as location, and written to a temporary file or MQTT entity only while the AI Task reads them,
then removed. If the App is stopped mid-scan, the next start removes anything left over.

## Diets

Setup has a main diet to pick from a list (general, plant-based, low-carb, weight-loss programs and condition-focused
styles) and an optional "Other goals or notes" line. A diet is guidance for the AI task, not a rule MealAgent checks, and
it is not medical advice. Allergies always take precedence over the diet. "Points-based (Weight Watchers style)" does not
calculate official points; it favours typically low-point foods and shows an estimated calories per serving marked "est.".
Profiles saved before 0.1.1 keep working: a free-text diet that names a listed diet selects it, any other text moves to
"Other goals or notes" under Balanced.

## Allergens

MealAgent compares ingredient names with the allergy list you enter. It does not know what is inside packaged products.
Always check product labels. MealAgent is not a medical device. See the full disclaimer on the Setup page.

## Photos and MQTT

If the Mosquitto broker is available, a photo is shown to the AI Task as a short-lived image entity whose id starts
with `mealagent_`. Otherwise it is written to `/media/mealagent/` and deleted straight after.
