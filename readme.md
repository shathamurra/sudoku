## Algorithim Choice: 

For this Suduko Solver algorithim I used depth-first search with constraint satisfaction. It is clear that this is an example of a constraint satisfaction problem where there are a number of variables, each of which can take a number of values, subject to some constraints, the constrains being: 

1- No duplicate numbers in any of the rows
2- No duplicate numbers in any of the columns
3- No duplicate numbers in any of the 3x3 boxes 

Variables: each cell in the suduko can take a variable from this set {1,2,3,4,5,6,7,8,9}

Values: Domain of each empty cell given the constraints 


## Code Structure:

#### First I created a Sudoku_Solution class, which instatiates a Suduko Object with the following attributes: 

- suduko: is the state of the sudoku in the current moment
- possible_values: an array of possible numbers that can be assigned in the empty location
- unsolvable_sudoku: An array of -1, that is returned when no solution is found 

#### The sudoku object has these methods classified into 2 categories: 

##### 1- Main methods: 

   - get_next_empty_location: finds the next empty location 
   - get_updated_possible_values: finds possible values given the constraints 
   - set_value: it creates a new state after setting a possible value in an empty location
   - is_goal: checks if we reached a goal state, ie. if the suduko is solved
   - is_valid_suduko: checks if an entered starting sudoku is valid 

##### 2- Helper functions:

   - is_unique_row: checks if there are no duplicates in the row (excluding zeros)
   - is_unique_column:checks if there are no duplicates in the column(excluding zeros)
   - is_unique_subgrid: checks if there are no duplicates in the box (excluding zeros)
   - is_valid_entry: checks that an entry is valid within the row, column and subgrid
   - all_goal_numbers: check that all numbers in the sudoku are between 1 and 9
   - all_valid_numbers: check that all numbers in the sudoku are between 0 and 9
   - all_rows_valid: checks that there are no duplicates in rows 
   - all_columns_valid: checks that there are no duplicates in columns
   - all_boxes_valid: checks that there are no duplicates in boxes
   - fetch_subgrid: finds and returns the box for a ceratin cell 
   

### depth_first_search function:

Takes in Suduko object, checks if the suduko is at a goal state (if so sudoku is returned). Then it fetches the next empty location and the possible values for that given location. 

It loops over each value of the possible values and sets it to a new_state through the set_value method. 

If the new state is not valid, we return None and backtrace.  

If the new state is valid and is a goal state then that state is returned. 

If the new state is not goal but is valid, we call the depth_first_search recursively and assign it to deep_state, which is returned if it's goal. 



### sudoku_solver function:

Takes a suduko 2d array and creates a Sudoku_Solution object. It then checks if the given suduko is valid from the start or not. It then calls the depth_first_search function on that sudoku and returns the solution if there's one, otherwise it returns an array of negative ones.


## Optimization:

I started with a constraint-satisfaction first-depth search algorithim as it seemed to best suit the problem. But then I optimized within this algorithim. 

All very_easy, easy and medium sudukos ran within miliseconds, there were no issues whatsoever in terms of speed. However, only 4 out of the 15 hard sudukos were solved under 30 seconds, the others took longer time, some reaching 500 seconds. 

To increase speed, I needed to implement some code optimization, which include: 

- Adding a helper function is_valid_entry, which checks if a value is valid within a certain subgrid instead of checking if the entire sudoku board is valid.

- Adding a helper function is_valid_entry, which checks if a value is valid within a certain column instead of checking if all columns are valid.


- Adding a helper function is_valid_entry, which checks if a value is valid within a certain row instead of checking if the all rows are valid.


- Improving fetch_next_location to return only the upcoming empty location instead of returning all empty locations and looping over each one of the,

- Implemented get_updated_possible_values to only check a reduced number of valid values for a certain location instead of looping over all 9 possible values. 

- Improve general code structure, and using built in numpy functions where possible to increase speed. 


##### All of these optimization increased speed by a factor of 4. 


## Big O Notation:


O(n ^ m) where n is the number of possibilities for each square (i.e., 9 in classic Sudoku) and m is the number of spaces that are blank. Maximum value of n will be equal to 9. 















