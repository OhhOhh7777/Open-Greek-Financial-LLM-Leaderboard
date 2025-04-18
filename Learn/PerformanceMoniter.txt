# PerformanceMonitor Component Documentation

## Overview
The PerformanceMonitor is a developer tool that provides real-time performance metrics for the
Open Greek Financial LLM Leaderboard application. It displays critical rendering, memory, and
network statistics in a floating panel to help identify performance bottlenecks during
development.


## Key Features
- Real-time FPS (frames per second) monitoring with color-coded feedback
- JavaScript memory usage tracking (heap size)
- React render cycle counting
- Network transfer size and compression ratio statistics
- GPU memory usage estimation
- First Contentful Paint (FCP) timing
- Toggleable visibility with keyboard shortcut
- Development-only visibility by default
- Non-intrusive overlay with theme-aware styling

## Internal Components

### MetricBox
A reusable component for displaying individual performance metrics:

Props:
- icon: React element representing the metric icon
- label: Short text label for the metric
- value: Current value to display (can be text or React element)
- tooltip: Explanatory text shown on hover

### getGPUStats
A utility function that estimates GPU information and memory usage:
- Creates a temporary WebGL context
- Measures memory usage through texture allocation
- Returns vendor, renderer, and estimated memory usage
- Properly cleans up resources after measurement

## Metrics Displayed

### Performance
- FPS: Current frames per second (color-coded by performance)
- FCP: First Contentful Paint timing in milliseconds
- React: Total number of React render cycles

### Memory
- Mem: JavaScript heap memory usage (used/total in MB)
- GPU: Estimated GPU memory usage in MB

### Network
- Net: Total network data transferred in KB
- Size: Decoded data size with compression savings percentage

## Implementation Details
- Uses React.memo to prevent unnecessary re-renders
- Implements keyboard shortcuts with event listeners
- Monkey patches React.createElement to count render cycles
- Uses requestAnimationFrame for smooth stat updates
- Leverages Performance API for network and timing data
- Cleans up all resources and event listeners on unmount
- Uses WebGL context for GPU information
- Formats large numbers with space separators for readability

## Usage
The component automatically renders in development mode and is hidden in production.
No props are required as it's completely self-contained.
