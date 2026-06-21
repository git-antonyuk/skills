---
# diet-coach profile (Obsidian / markdown format)
# The skill reads these fields every run. Leave a value blank and the skill will
# ask you for it before computing. Edit anytime — targets recompute on the fly.

# --- Identity & body ---
sex:                 # male | female  (needed for BMR)
age:                 # years
height_cm:           # REQUIRED for BMR — no estimate
weight_kg:           # current weight; update regularly
goal_weight_kg:      #
target_rate_kg_per_week:   # 0.5–1.0 typical

# --- Activity & training ---
activity_level:      # sedentary | light | moderate | very | extra (job/lifestyle, not workouts)
training_source:     # gymtempo | manual | <other-mcp-name>
training_freq_per_week:    # used when training_source = manual

# --- Diet ---
diet_style:          # flexible | low-carb | low-fat | time-restricted | ...
calorie_target:      # current kcal target (skill recomputes & flags drift)
protein_target_g:    #
current_phase:       # grind | chill
phase_start_date:    # YYYY-MM-DD

# --- Context ---
sleep_quality:       # e.g. 1-5 or a note
stress_level:        # e.g. 1-5 or a note
dietary_restrictions:      # allergies, dislikes-as-rules, religious, etc.
foods_liked:         #
foods_disliked:      #

# --- Skill config ---
response_language: uk     # answer language (uk = Ukrainian)
data_dir:            # folder holding this profile + progress log
---

# Notes

Free-form notes about preferences, history, injuries, etc.
