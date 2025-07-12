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

### AI-Powered Recipe Generation Pipeline (FUTURE)
**Goal**: Implement an automated AI agentic system to convert raw content into structured YAML recipes

**Content Input Types**:
- Food photography (plated dishes, ingredients, cooking process shots)
- Handwritten recipe cards and notes
- Screenshots of digital recipes from websites/apps
- Menu PDFs and printed materials
- Video content of food preparation
- Voice recordings of recipe instructions
- Mixed media content (photos + text + audio)

**AI Pipeline Architecture**:
```
Upload → Content Analysis → Multi-Modal Processing → YAML Generation → Human Review → Integration
```

**Processing Stages**:
1. **Content Classification**
   - Image analysis: food vs. text vs. mixed content
   - Document type detection (recipe card, menu, ingredient list)
   - Quality assessment and image enhancement
   - OCR readiness evaluation

2. **Multi-Modal Extraction**
   - **Vision AI**: Identify ingredients, cooking methods, plating styles
   - **OCR/Text Extraction**: Convert handwritten/printed text to digital
   - **NLP Processing**: Parse recipe instructions and ingredient lists
   - **Audio Processing**: Transcribe voice recordings of recipes

3. **Content Understanding**
   - **Ingredient Recognition**: Visual + text identification with quantities
   - **Cooking Method Detection**: Identify techniques (seared, roasted, etc.)
   - **Portion Analysis**: Estimate serving sizes from visual cues
   - **Cost Estimation**: Ingredient pricing based on market data
   - **Dietary Classification**: Auto-tag vegetarian, gluten-free, etc.

4. **YAML Generation**
   - **Structured Output**: Generate complete recipe YAML files
   - **Template Compliance**: Ensure compatibility with existing schema
   - **Validation**: Check completeness and data integrity
   - **Enhancement**: Add missing fields with intelligent defaults

**Implementation Components**:

**Backend Services**:
```python
# AI Processing Pipeline
services/
  image_processor.py      # Computer vision for food/ingredient recognition
  ocr_engine.py          # Text extraction from images/PDFs
  nlp_parser.py          # Recipe text parsing and structuring
  cost_estimator.py      # Ingredient pricing intelligence
  yaml_generator.py      # YAML output formatting and validation
  quality_checker.py     # Content validation and completeness scoring
```

**Frontend Upload Interface**:
```javascript
// Multi-file upload with progress tracking
upload/
  drag_drop_zone.js      # File upload interface
  preview_gallery.js     # Content preview before processing
  processing_status.js   # Real-time pipeline progress
  review_editor.js       # Human review and correction interface
```

**AI Model Integration**:
- **Vision Models**: Food recognition, ingredient identification
- **OCR Models**: Handwriting recognition, document processing
- **LLM Integration**: Recipe parsing, instruction generation, cost estimation
- **Specialized APIs**: Nutrition data, ingredient databases, pricing services

**User Workflow**:
1. **Upload Content** - Drag/drop images, PDFs, audio files
2. **AI Processing** - Automated content analysis and extraction
3. **Review & Edit** - Human validation with suggested corrections
4. **Generate Recipe** - Create final YAML file with all metadata
5. **Integration** - Add to recipe collection with proper tagging

**Advanced Features**:
- **Batch Processing**: Upload multiple recipes simultaneously
- **Learning System**: Improve accuracy based on user corrections
- **Template Recognition**: Auto-detect restaurant-specific formats
- **Brand Integration**: Apply current brand configuration to generated recipes
- **Multi-Language**: Generate Spanish translations automatically
- **Version Control**: Track recipe modifications and improvements

**Quality Assurance**:
- **Confidence Scoring**: Rate extraction accuracy for each field
- **Human-in-the-Loop**: Flag low-confidence items for manual review
- **Validation Rules**: Ensure logical consistency (costs, quantities, methods)
- **Duplicate Detection**: Identify similar recipes to prevent redundancy

**Technical Requirements**:
- **Cloud Infrastructure**: Scalable processing for image/document analysis
- **API Integration**: Vision AI, OCR services, LLM providers
- **Storage**: Secure handling of uploaded content and generated recipes
- **Performance**: Real-time processing with progress feedback
- **Privacy**: Secure handling of proprietary restaurant recipes

**Estimated Development Effort**: 6-8 weeks for MVP
- Week 1-2: Upload interface and basic image processing
- Week 3-4: OCR and text extraction pipeline
- Week 5-6: YAML generation and validation system
- Week 7-8: Human review interface and integration

**Success Metrics**:
- **Accuracy**: >90% correct ingredient identification
- **Completeness**: >85% of required YAML fields auto-populated
- **Speed**: <2 minutes processing time per recipe
- **User Satisfaction**: <10% recipes require major manual corrections

**Future Enhancements**:
- **Video Processing**: Extract recipes from cooking videos
- **Real-time Collaboration**: Multiple users reviewing same recipe
- **API Endpoints**: Allow external systems to submit content
- **Mobile App**: Native mobile upload and review capabilities
- **Integration Marketplace**: Connect with POS systems, inventory management