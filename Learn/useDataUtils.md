# useDataUtils Hooks Documentation

## Overview
The useDataUtils.js file provides a collection of specialized React hooks for data processing,
filtering, visualization, and management in the Open Greek Financial LLM Leaderboard. These hooks
handle everything from data normalization to complex filtering logic and score visualization.

## Location
Open-Greek-Financial-LLM-Leaderboard/frontend/src/pages/LeaderboardPage/components/Leaderboard/hooks/useDataUtils.js

## Exported Hooks

### useAverageRange
Calculates minimum and maximum average scores across all models for normalization.

Parameters:
- data (Array): Raw model data array

Returns:
- Object with:
  - minAverage: Lowest average score among models
  - maxAverage: Highest average score among models

### useColorGenerator
Creates a function that converts scores to color values for visual representation.

Parameters:
- minAverage (Number): Minimum score value for normalization
- maxAverage (Number): Maximum score value for normalization

Returns:
- Function that takes a score value and returns an RGBA color string
- Uses caching to optimize repeat calculations
- Generates colors on red to purple scale (lower to higher scores)

### useProcessedData
Standardizes and processes raw model data with calculated scores.

Parameters:
- data (Array): Raw model data array
- averageMode (String): Mode for calculating averages ("all" or "visible")
- visibleColumns (Array): List of currently visible columns

Returns:
- Array of processed model objects with:
  - Standardized boolean values
  - Calculated average scores based on selected mode
  - Static rank values (position in global performance order)
  - Consistent data structure

### useFilteredData
Applies comprehensive filtering logic to model data based on user selections.

Parameters:
- processedData (Array): Standardized model data
- selectedPrecisions (Array): Selected precision formats
- selectedTypes (Array): Selected model types
- paramsRange (Array): Parameter size range [min, max]
- searchValue (String): Search query text
- selectedBooleanFilters (Array): Boolean filter selections
- rankingMode (String): "static" or "dynamic" ranking
- pinnedModels (Array): IDs of pinned models
- isOfficialProviderActive (Boolean): Whether official provider filter is active

Returns:
- Array of filtered model data with:
  - Pinned models at the top (preserving pinned order)
  - Dynamic and static ranking values
  - Appropriate isPinned flag
  - Filtered based on all criteria

Key features:
- Advanced text search with attribute filtering, regex support
- Multi-criteria filtering with precision, model type, parameter size
- Special handling for pinned models that preserves their order
- Multi-level sorting for ties (score → name → submission date)
- Boolean filter support with appropriate logic

### useColumnVisibility
Creates a column visibility configuration object for the table.

Parameters:
- visibleColumns (Array): List of column keys to be visible

Returns:
- Object mapping column keys to visibility boolean values
- Includes error handling for malformed input

## Implementation Details
- All hooks use useMemo for performance optimization
- Advanced searching uses regex and attribute-based filtering
- Complex sorting logic handles ties and missing values
- Separation of filtering logic from UI components
- Error handling to prevent crashes from malformed data

## Usage Example
```jsx
// Calculate score range for color mapping
const { minAverage, maxAverage } = useAverageRange(data);

// Get color generator function
const getColor = useColorGenerator(minAverage, maxAverage);

// Process raw data with standardization
const processedData = useProcessedData(data, "all", visibleColumns);

// Apply all filters
const filteredData = useFilteredData(
  processedData,
  ["FP16", "BF16"], // precision formats
  ["transformer"], // model types
  [7, 70], // parameter range in billions
  "llama", // search term
  ["is_not_available_on_hub"], // boolean filters
  "dynamic", // ranking mode
  ["model-1", "model-2"], // pinned models
  false // official provider filter
);

// Get column visibility configuration
const columnVisibility = useColumnVisibility(["col1", "col2"]);