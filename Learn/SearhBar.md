# SearchBar Component Documentation

## Overview
The SearchBar component provides a full-featured search interface for the Open Greek Financial LLM 
Leaderboard, allowing users to filter models by name and attributes. It includes an advanced query 
syntax, visual feedback for active filters, and integration with the leaderboard's filtering system.

## Component Location
Open-Greek-Financial-LLM-Leaderboard/frontend/src/pages/LeaderboardPage/components/Leaderboard/components/Filters/SearchBar.js

## Props
- onToggleFilters (Function): Toggles visibility of advanced filters panel
- filtersOpen (Boolean): Whether the advanced filters panel is currently open
- loading (Boolean): Whether data is currently loading
- data (Array): Array of filtered model data
- table (Object): Reference to the table instance

## Key Features
- Real-time search with debounced updates
- Advanced query syntax support (strict search, regex, attribute filters)
- Visual representation of complex search terms
- Filter count indicator showing matched/total models
- Reset button to clear all active filters
- Toggle for advanced filters panel
- Loading state with skeleton placeholders
- Help tooltip with search syntax guidance

## Internal Components

### SearchBarSkeleton
A placeholder component shown during loading states:
- Displays animated skeleton UI elements in place of search functionality
- Maintains consistent layout to prevent layout shifts when data loads

### SearchDescription
A component that visualizes complex search queries:
- Parses search terms into readable segments
- Applies color coding to different search groups
- Shows connectors between search terms
- Provides visual confirmation of current search parameters

## Special Behaviors
- Debounced search input to prevent excessive re-filtering
- Color-coded visualization of complex search terms
- Automatic detection of active filters from global state
- Dynamic reset button that appears only when filters are active
- Advanced filters button changes color when filters are active
- Maintains local input state for smooth typing experience
- Updates global filter state when search is confirmed

## Search Syntax Support
- Regular text search (e.g., "llama")
- Strict matching with quotes (e.g., "\"GPT-4\"")
- Multiple terms with semicolons (e.g., "llama; falcon")
- Attribute filters with @ syntax (e.g., "@architecture:transformer")
- Regular expressions (e.g., "/llama-\d+/")

## Usage Example
```jsx
<SearchBar
  onToggleFilters={handleToggleFilters}
  filtersOpen={isFiltersOpen}
  loading={isLoading}
  data={filteredModels}
  table={tableInstance}
/>