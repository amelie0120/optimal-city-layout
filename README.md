# Green City Layout Optimization using Genetic Algorithm

## Project Overview

This project addresses the complex challenge of optimizing urban layouts using a Genetic Algorithm (GA). The primary objective is to determine the most effective distribution of different zones: residential (R), commercial (C), green spaces (G), and streets (S) within a city grid, taking into account varying elevations which influence the suitability of different areas for specific development types.

## Problem Definition

The optimization problem involves designing an urban layout that strategically distributes different zones across a city grid with these requirements:

- **Residential areas (R)**: Should be peaceful yet accessible, close to green spaces for environmental quality and recreational purposes, and near commercial zones for access to services and employment.
- **Commercial areas (C)**: Need high accessibility to maximize economic activity, benefiting from proximity to major streets and residential areas to ensure customer and employee access.
- **Green spaces (G)**: Essential for environmental sustainability, improving air quality, and providing recreational areas.
- **Streets (S)**: Must efficiently connect all areas of the city, facilitating smooth transit and access without fragmenting other functional spaces excessively.

## Constraints

- **Percentage of each zone type**:
  - R tiles: 25% - 40%
  - C tiles: 10% - 20%
  - G tiles: 15% - 25%
  - S tiles: 20% - 30%
- **Adjacency requirements**: Every group of R tiles needs to have at least one street tile adjacent.
- **Proximity of green areas**: At least one G tile at a maximum distance of 3 tiles from each R tile.
- **Street connectivity**: Streets should form a single continuous network.
- **Size of building groups**: Residential areas should be between 2 and 10 tiles.
- **Elevations**:
  - R tiles: Situated at lower elevations (less than 1/3 of the difference between the highest and lowest points).
  - C tiles: Positioned at elevations lower than 1/5 of the same difference.
  - G tiles: Preferred at higher elevations (exceeding 1/3 of the difference between the highest and lowest points).

## Genetic Algorithm Implementation

### Codification
- **Representation**: The city grid is codified as a linear string of characters, each representing a zone type ('R', 'C', 'S', 'G').
- **Chromosome**: Each chromosome in the population is a complete city layout.

### Implementation Details
- **Programming Language**: Python with the "inspyred" library for evolutionary algorithms.
- **Algorithm Structure**:
  1. Generate random initial population
  2. Evaluate population using the fitness function
  3. Choose best candidates based on selector
  4. Apply N-point Crossover (with n = number of rows) 
  5. Apply Random Reset Mutation
  6. Replace population with Crowding Replacement
  7. Continue until no improvement in fitness for 200 generations

### Fitness Function
The fitness function evaluates the effectiveness of each layout, considering:
- Zone type percentages
- Residential clusters
- Street adjacency
- Proximity to green spaces
- Street connectivity
- Elevation management

These factors are combined and weighted to produce a comprehensive fitness score that guides the evolutionary process.

## Experimental Results

After extensive experimentation with different selection methods, crossover types, mutation strategies, and replacement operators, our best configuration was:
- N-point crossover (n = number of rows)
- Random reset mutation
- Crowding replacement
- No improvement termination (after 200 generations)

We tested five selectors:
- Uniform selection
- Tournament selection (tournament size = 3)
- Fitness proportionate selection
- Default selection
- Truncation selection

Our experiments were conducted on eight different datasets with varying dimensions (6x6 to 10x10) and elevation characteristics. Each algorithm variant was executed 31 times per dataset to ensure statistical significance.

### Key Findings
- For grids of 7x7 or smaller, outcomes were very close to optimal with fitness scores around 90/100
- The best fitness scores were achieved by uniform selection, fitness proportionate selection, and default selection
- Street connectivity reached optimal levels (value of 1) most consistently with default selection and truncation selection
- The most balanced performance considering fitness, constraint satisfaction, and execution time was achieved by fitness proportionate selection

## References
The project utilized the inspyred library documentation and resources from the bio-inspired algorithms course.
