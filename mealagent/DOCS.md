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

## What it stores

Your setup, pantry list and a plan per week are JSON files in the App's `/data` folder. Pantry photos are shrunk,
stripped of metadata such as location, and written to a temporary file or MQTT entity only while the AI Task reads them,
then removed. If the App is stopped mid-scan, the next start removes anything left over.

## Allergens

MealAgent compares ingredient names with the allergy list you enter. It does not know what is inside packaged products.
Always check product labels. MealAgent is not a medical device. See the full disclaimer on the Setup page.

## Photos and MQTT

If the Mosquitto broker is available, a photo is shown to the AI Task as a short-lived image entity whose id starts
with `mealagent_`. Otherwise it is written to `/media/mealagent/` and deleted straight after.
