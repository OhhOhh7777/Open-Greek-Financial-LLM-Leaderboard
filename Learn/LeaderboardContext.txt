# LeaderboardContext Documentation

## Overview
LeaderboardContext provides centralized state management for the Open Greek Financial LLM Leaderboard, 
handling filter state, model data, display preferences, and URL synchronization. It enables consistent 
filtering and viewing preferences across the application.

## Component Location
Open-Greek-Financial-LLM-Leaderboard/frontend/src/pages/LeaderboardPage/components/Leaderboard/context/LeaderboardContext.js

## Main Exports
- LeaderboardProvider (default): Context provider component that wraps the application
- useLeaderboard: Custom hook to access leaderboard state and actions

## State Management
The context maintains the following state:
- models: Array of all model data
- loading: Loading/initialized state
- filters: Active filtering criteria
- display: Table display preferences
- pinnedModels: Array of pinned model IDs
- filterCounts: Statistics for each filter type
- error: Any error state

## Key Features

### URL Synchronization
- All filters and display preferences are synchronized with URL parameters
- Enables shareable links that preserve exact table configuration
- Handles loading initial state from URL on first render
- Updates URL when state changes without full page reloads

### Filtering Logic
- Implements comprehensive model filtering based on multiple criteria:
  - Text search (model names)
  - Precision format (FP16, BF16, etc.)
  - Model type (transformer, MoE, mixture, etc.)
  - Parameter count ranges
  - Boolean flags (is_moe, is_flagged, etc.)
  - Official models only

### Model Pinning
- Allows pinning specific models to top of table
- Persists pinned models in URL parameters
- Handles special count logic for pinned models

### Display Preferences
- Manages row size/density
- Controls score display format (normalized/raw)
- Configures average calculation method
- Sets ranking mode (static/dynamic)
- Tracks visible columns

### Statistics Tracking
- Calculates and updates counts for each filter category
- Maintains separate counters for normal and official-only views
- Tracks parameter ranges, model types, precision formats

## API

### State Object
- models: Array of all model data
- loading: Boolean loading state
- filters: Current filter configuration
- display: Current display preferences
- pinnedModels: Array of pinned model IDs
- filterCounts: Statistics for each filter category

### Actions
- setModels(models): Update model data
- setLoading(loading): Set loading state
- setFilter(key, value): Update specific filter
- setDisplayOption(key, value): Update display preference
- togglePinnedModel(modelId): Toggle model pinned state
- toggleOfficialProvider(): Toggle official models filter
- toggleFiltersExpanded(): Toggle filters panel visibility
- resetFilters(): Reset all filters to defaults
- resetAll(): Reset all filters, display options and pins

### Utility Functions
- getFilteredCounts(): Calculate filtered model counts
- checkModelMatchesFilters(model): Check if model matches filters

## Usage Example
```jsx
// Wrap application with provider
<LeaderboardProvider>
  <App />
</LeaderboardProvider>

// Access context in components
function ModelTable() {
  const { state, actions, utils } = useLeaderboard();
  
  // Access state
  const { models, loading, filters } = state;
  
  // Use actions
  const handlePin = (modelId) => actions.togglePinnedModel(modelId);
  
  // Use utility functions
  const filteredCount = utils.getFilteredCounts(tableRows, pinnedCount);
  
  // Render component using context values
}