# LeaderboardFilters Component Documentation

## Overview
The LeaderboardFilters component provides an expandable interface with advanced filtering controls for the Open Greek Financial LLM Leaderboard. It allows users to filter models by precision, parameter count, model type, and various feature flags.

## Component Location
Open-Greek-Financial-LLM-Leaderboard/frontend/src/pages/LeaderboardPage/components/Leaderboard/components/Filters/Filters.js

## Main Features
- Precision format filtering (FP16, BF16, etc.)
- Parameter count range selection via slider
- Model type filtering (Transformer, MoE, Mixture, etc.) 
- Boolean flag toggles (Flagged models, MoE architecture, etc.)
- Official models toggle (only show models maintained by creators)
- Real-time count indicators showing available models per filter
- Responsive layout with different column arrangements
- Expandable/collapsible interface
- Custom animation for smooth expand/collapse

## Props
- selectedPrecisions: Array of selected precision formats
- onPrecisionsChange: Callback when precision selections change
- selectedTypes: Array of selected model types
- onTypesChange: Callback when model type selections change
- paramsRange: Array [min, max] of parameter count range
- onParamsRangeChange: Callback when parameter range changes
- selectedBooleanFilters: Array of toggled boolean filters
- onBooleanFiltersChange: Callback when boolean filters change
- data: Array of model data used for counts
- expanded: Boolean controlling expanded state
- onToggleExpanded: Callback for expand/collapse toggle
- loading: Boolean indicating loading state

## Key Components

### FilterGroup
A reusable container for grouping related filter controls with:
- Section title with optional tooltip
- Parameter slider with custom styling (when type is "Parameters")
- Flex container for filter tags

### CustomCollapse
A custom animation component for smooth expanding/collapsing of filter sections:
- Uses React's forwardRef for proper ref handling
- Implements height animation for smooth transitions
- Manages height calculation for dynamic content

## Layout Structure
- Main container with two card sections:
  1. Left section (9/12 width): Advanced Filters
     - Precision format filters
     - Parameter slider
     - Model type filters
     - Flag filters
  2. Right section (3/12 width): Official Models
     - Official provider toggle
     - Explanatory text

## Special Features
- Real-time count indicators showing how many models match each filter
- Debounced updates to prevent excessive re-renders
- Custom styled MUI Slider with improved visual appearance
- Context-aware filtering that adjusts counts based on active filters
- Official provider mode that switches count context

## Dependencies
- React hooks (useState, useEffect, useMemo, useRef)
- Material UI components (Box, Typography, Slider, Grid, etc.)
- Custom components (FilterTag, InfoIconWithTooltip)
- LeaderboardContext for shared state
- Configuration constants from various files

## Usage Example
```jsx
<LeaderboardFilters
  selectedPrecisions={["FP16", "BF16"]}
  onPrecisionsChange={handlePrecisionsChange}
  selectedTypes={["transformer", "mixture"]}
  onTypesChange={handleTypesChange}
  paramsRange={[7, 70]}
  onParamsRangeChange={handleParamsRangeChange}
  selectedBooleanFilters={["is_moe"]}
  onBooleanFiltersChange={handleBooleanFiltersChange}
  data={models}
  expanded={isExpanded}
  onToggleExpanded={toggleExpanded}
  loading={isLoading}
/>