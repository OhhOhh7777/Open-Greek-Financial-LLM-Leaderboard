# useLeaderboardData Hooks Documentation

## Overview
This file provides two essential hooks that handle data fetching, caching, and processing for
the Open Greek Financial LLM Leaderboard. The hooks abstract complex data handling operations
and integrate with the global context and React Query for efficient data management.

## Location
/Open-Greek-Financial-LLM-Leaderboard/frontend/src/pages/LeaderboardPage/components/Leaderboard/hooks/useLeaderboardData.js

## Exported Hooks

### useLeaderboardData
Manages data fetching with optimized caching strategies and error handling.

Parameters:
- None

Returns object with:
- data: The fetched leaderboard data
- isLoading: Boolean loading state
- error: Any error that occurred during fetching
- refetch: Function to manually trigger data refresh

Key features:
- Local Storage caching with 5-minute expiration
- API fetch fallback when cache expires
- React Query integration for global cache control
- Error handling with detailed logging
- Conditional refetching based on URL parameters
- Automatic stale-time configuration

### useLeaderboardProcessing
Connects raw data with filtering, sorting, and processing logic from the leaderboard context.

Parameters:
- None (uses context for all inputs)

Returns object with:
- table: Configured table instance with all behaviors
- minAverage/maxAverage: Score range for normalization
- getColorForValue: Function to convert scores to colors
- processedData: Raw data with standardized structure
- filteredData: Data after applying all active filters
- columns: Configured table columns with accessors
- columnVisibility: Current column visibility state
- loading: Global loading state
- error: Any error state from context

Key features:
- Memoized data and filter references to prevent redundant processing
- Integration with global leaderboard context
- Default sorting by average score (descending)
- Complex data processing through useDataProcessing hook
- Complete table configuration for presentation

## Implementation Details
- Uses React Query for efficient data fetching and caching
- Implements localStorage caching to reduce API calls
- Conditionally enables data fetching based on URL parameters
- Manages initial load state with a ref to prevent unnecessary fetches
- Memoizes data and filter objects for optimal rendering performance
- Default sorting configuration prioritizes best performing models
- Handles cache invalidation for manual refreshes

## Constants
- CACHE_KEY: "leaderboardData" - Key for localStorage caching
- CACHE_DURATION: 300000 (5 minutes) - How long to consider cached data fresh

## Usage Example
```jsx
// In a component that needs leaderboard data
function LeaderboardView() {
  // For just loading the data
  const { data, isLoading, error, refetch } = useLeaderboardData();
  
  // For getting processed data ready for display
  const {
    table,
    filteredData,
    getColorForValue,
    loading,
    error: processingError
  } = useLeaderboardProcessing();
  
  if (loading) return <LoadingIndicator />;
  if (error || processingError) return <ErrorMessage />;
  
  return (
    <>
      <RefreshButton onClick={refetch} />
      <LeaderboardTable 
        table={table} 
        data={filteredData} 
        colorizer={getColorForValue} 
      />
    </>
  );
}