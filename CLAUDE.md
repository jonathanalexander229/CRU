# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

CRÙ Wine Bar Recipe Management System - A modern web-based recipe management system for a restaurant. Currently implemented as static HTML demo/proof-of-concept, but intended to be refactored into a data-driven system using JSON/YAML for recipe storage with dynamic HTML generation.

## Current State (Demo/POC)

The existing files serve as proof-of-concept with hardcoded recipe data:

- **menu.html**: Main recipe card interface with detailed recipes
- **condensed_all_menus.html**: Compact 4-column overview of all menus
- **brunch_menu.html**: Brunch-specific recipe cards
- **Individual menu files**: lunch_menu.html, dinner_menu.html, happy_hour_menu.html
- **menu pictures/**: Directory containing photographed recipes and menus (JPEG format)

## Content Sources

- **Existing data**: Recipe content extracted from photographs and existing HTML files
- **Processed images**: 15 new recipe images (IMG_4801-4815) have been successfully processed and converted to YAML
- **YAML recipe system**: 20 complete recipes now stored in structured YAML format in `/recipes/` directory
- **Image processing workflow**: New photos → content extraction → YAML conversion → menu generation

## Current Architecture (YAML-Based)

### Data Layer ✅ COMPLETED
- **Recipe storage**: 20 recipes stored in YAML format in `/recipes/` directory
- **Recipe schema**: Standardized YAML structure implemented with template
- **Menu organization**: Recipes tagged by menu periods (brunch, lunch, dinner, happy_hour)
- **Complete data**: Ingredients, methods, pricing, dietary info, cooking methods, source tracking

### Application Layer (NEXT PHASE)
- **Template system**: HTML templates for recipe cards and menu layouts  
- **Data processing**: JavaScript/Python to load YAML and populate templates
- **Menu generation**: Dynamic creation of menu views from YAML files

### Presentation Layer (NEXT PHASE)
- **Responsive design**: CSS Grid layouts maintained from current implementation
- **Theme system**: Color-coded themes for different meal periods
- **Print optimization**: Maintained print-friendly layouts

## Recipe Data Structure ✅ IMPLEMENTED

Current YAML schema includes:
```yaml
name: "Recipe Name"
menu_periods: [dinner, lunch, etc.]
plate_info: "Serving plate or presentation style"
status: complete|placeholder|draft

ingredients:
  - name: "Ingredient name"
    quantity: 1.0
    unit: "oz"
    cost_per_unit: 0.50
    total_cost: 0.50
    notes: "Optional notes"

method:
  prep_notes: "Preparation requirements"
  cooking_instructions: "Detailed cooking steps"
  plating_instructions: "Plating and presentation"
  timing_notes: "Important timing information"

pricing:
  ingredient_cost: 0.00
  sales_price: 0.00
  cost_percentage: 0.00
  contribution_margin: 0.00

tags: [appetizer, entree, pizza, etc.]
dietary: [vegetarian, vegan, gluten_free, etc.]
cooking_methods: [seared, roasted, etc.]

source:
  image_file: "IMG_XXXX.jpeg"
  date_added: "2025-06-28"
  notes: "Source information"
```

## Development Progress

1. **Extract data**: ✅ COMPLETED - 28 recipes converted to YAML (20 complete + 8 placeholders)
2. **Create dynamic system**: ✅ COMPLETED - Dynamic menu with dropdown filtering and recipe detail pages
3. **Build generator**: FUTURE - Python/JavaScript system to merge YAML + templates
4. **Maintain styling**: ✅ COMPLETED - Preserved existing CSS design system in dynamic interface
5. **Add management**: FUTURE - Easy ways to add/edit/remove recipes
6. **Spanish translation**: FUTURE - Add bilingual support to recipe system

## Key Benefits of Refactor

- **Easy updates**: Modify recipes without touching HTML/CSS
- **Consistency**: Standardized recipe format across all menus
- **Extensibility**: Simple to add new menu periods or recipe types
- **Maintenance**: Separate concerns (data, presentation, logic)
- **Validation**: Ensure recipe completeness and data integrity

## Current File Organization

```
/recipes/                    ✅ COMPLETED
  recipe-template.yaml       ✅ Schema template
  beet-salad.yaml           ✅ 20 complete recipes
  shaking-beef.yaml         ✅ with full ingredient
  margherita-pizza.yaml     ✅ and pricing data
  ... (17 more recipes)     ✅
  
/menu pictures/             ✅ Source images
  IMG_4801-4815.jpeg        ✅ 15 processed images
  (older reference images)  
  
Legacy HTML files:          ✅ Reference implementations
  menu.html                 ✅ Current recipe card design
  condensed_all_menus.html  ✅ Grid layout reference
  (other menu files)        ✅ Styling examples

NEXT PHASE:
/templates/                 🔄 HTML templates from YAML
/scripts/                   🔄 YAML → HTML generators
```

## Common Development Tasks

### Current YAML-Based Workflow:
- **Adding recipes**: Create new YAML files in `/recipes/` using template
- **Updating existing recipes**: Edit YAML files directly - no HTML changes needed
- **Processing new images**: Extract recipe data → convert to YAML format
- **Recipe validation**: Check YAML structure against template schema

### Next Phase (Template-Based):
- **Styling changes**: Update HTML templates and CSS
- **Menu generation**: Run generator script to create HTML from YAML
- **Menu configuration**: Adjust themes, layouts via config files
- **Data validation**: Automated checks before HTML generation

### Recipe Management Examples:
```bash
# Add new recipe
cp recipes/recipe-template.yaml recipes/new-dish.yaml
# Edit with recipe details

# Generate updated menus (future)
python generate_menus.py

# Validate all recipes (future)
python validate_recipes.py
```

## Future Development Roadmap

### Spanish Translation Implementation (FUTURE)
**Goal**: Add bilingual Spanish/English support to the recipe management system

**Approach**: Extend YAML schema with Spanish translation fields
- Add `_es` suffix fields for all user-facing content (name_es, ingredients.name_es, method.prep_notes_es, etc.)
- Implement language toggle in dynamic menu interface
- Create translation helper functions for graceful fallback to English when Spanish missing
- Update recipe detail pages with language switching capability

**Estimated Effort**: 2-3 hours for core implementation + ongoing translation work

**Key Considerations**:
- Spanish text typically 15-25% longer than English - may require CSS layout adjustments
- Maintain fallback to English for missing translations
- Consider keeping some culinary terms in English (EVOO, S&P, etc.)
- Implement user language preference persistence

**Translation Priority Order**:
1. Most popular dinner items and all brunch recipes
2. Common appetizers and shared menu items  
3. Complete remaining recipe collection
4. UI elements (buttons, labels, dropdown options)

**Schema Example**:
```yaml
name: "Beet Salad"
name_es: "Ensalada de Remolacha"
ingredients:
  - name: "Gold beets, roasted & wedged"
    name_es: "Remolachas doradas, asadas y cortadas"
    unit: "pc"
    unit_es: "pzs"
method:
  prep_notes: "Roast and wedge gold beets"
  prep_notes_es: "Asar y cortar remolachas doradas"
```