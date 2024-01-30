## BetterThanAdolf: Evolutionary Algorithm for Image Replication

### Overview
The `BetterThanAdolf` class implements an evolutionary algorithm designed to replicate a target image using a collection of colored triangles. This approach mimics the process of natural selection, where a population of solutions (chromosomes) evolves over generations to approximate the desired outcome - in this case, an image.

### Algorithm Components

#### Chromosomes
Each chromosome in the population represents a potential solution. It consists of a sequence of triangles, each defined by its coordinates and color. The goal is to arrange these triangles so that when they're layered together, they resemble the target image.

#### Fitness Function
The fitness of each chromosome is determined by the Mean Squared Error (MSE) between the rendered image (from the chromosome) and the target image. The MSE is calculated as:

$$
MSE = \frac{1}{n} \sum (I_{target} - I_{rendered})^2
$$

Where $I_{target}$ is the pixel value of the target image, $I_{rendered}$ is the pixel value of the rendered image, and $n$ is the total number of pixels in the image.

### Class Methods

#### `__init__(self, target_image_path, ...)`
The constructor initializes the algorithm with parameters like the path to the target image, the number of triangles in each chromosome, population size, number of generations (iterations), and rates for various mutations.

#### `display_image(self, image)`
A static method to display an image.

#### `save_image(self, image, filepath)`
A static method to save an image to a file.

#### `draw_triangle(self, triangle, color, img)`
A static method to draw a triangle on an image. The triangle is defined by its vertices and color.

#### `create_image(self, triangles, colors, img)`
Creates an image by drawing a series of triangles with specified colors onto it.

#### `create_new_image(self, triangles, colors)`
Generates a new image based on the given triangles and colors, using the current image as a base.

#### `update_current_img(self, triangles, colors)`
Updates the current image with new triangles and colors.

#### `calculate_image_distance(self, triangles, colors)`
Calculates the MSE between the target image and a rendered image created from the given triangles and colors.

#### `generate_random_population(self)`
Generates a random initial population of triangles and colors.

#### `select_parents(self, current_population_objective_values)`
Selects parents for breeding based on their fitness, where fitness is inversely proportional to the MSE.

#### `generate_offspring(self, parent_indices)`
Generates offspring by averaging the properties (triangles and colors) of selected parents.

#### `mutate(self, children_triangles, children_colors)`
Applies mutations to the positions and colors of triangles in the offspring. Mutations are random changes that introduce variability.

#### `apply_domain_constraints(self, children_triangles, children_colors)`
Ensures that triangle coordinates and colors stay within their respective domains (valid ranges).

#### `evaluate_children(self, children_triangles, children_colors)`
Calculates the MSE for each child in the offspring, determining their fitness.

#### `update_population(self, current_population_objective_values, children_mse_values, children_triangles, children_colors)`
Updates the population with the new offspring, replacing less fit chromosomes with better ones.

#### `update_best_solution(self, current_population_objective_values, best_mse, best_triangles, best_colors)`
Keeps track of the best solution found so far across all generations.

#### `log_and_debug(self, iteration, current_population_objective_values)`
Provides logging and debugging capabilities, displaying the current best image and statistics at specified intervals.

#### `show_statistics(self)`
Displays the evolution of MSE values across iterations, providing insights into the algorithm's performance and convergence.

#### `evolve(self, debug=False)`
The core method where the evolutionary process occurs. It iterates through generations, applying selection, crossover, and mutation to evolve the population towards a solution that minimally differs from the target image in terms of MSE.

#### `save_results(self, title)`
Saves the final result as an image and optionally creates a GIF to showcase the evolutionary process.

### Usage
To use this class, instantiate it with the required parameters, and call the `evolve()` method. After the evolution process, you can call `show_statistics()` to view the performance and `save_results()` to save the final image.



## Recombination process

Global Intermediate Recombination is a method used in evolutionary algorithms, particularly genetic algorithms, for the recombination or crossover process. This method combines traits from multiple parents to create new offspring solutions.

### Understanding Global Intermediate Recombination:

1. **Intermediate Recombination:** 
   - Involves creating offspring by computing a weighted average of the parents' traits. 
   - Typically used with real-valued parameters in genetic algorithms.

2. **Global Aspect:** 
   - "Global" indicates the involvement of more than two parents in the recombination process.
   - The traits of multiple individuals in the population are considered for creating offspring.

3. **Process:** 
   - The offspring's traits are determined by averaging each trait across all selected parents.
   - The formula: 
   - `O_i = (1/N) * Σ(P_{ji})` where `O_i` is the offspring's trait, `P_{ji}` is the trait in parent `j`, and `N` is the number of parents.

4. **Benefits:** 
   - Helps in maintaining genetic diversity and avoiding premature convergence.
   - Useful for exploring a wide range of solutions in the search space.

5. **Use Cases:** 
   - Often used in continuous optimization problems.

6. **Considerations:** 
   - Risk of diluting high-quality genetic material if too many average parents are included.

7. **Variants:** 
   - Implementations may vary, such as using weighted averages where some parents have more influence based on their fitness.
