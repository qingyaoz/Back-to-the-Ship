# Back-to-the-Ship
This project is primarily a personal learning exercise, maintained on GitHub for documentation.

## Overview
Jack have just broken out of the detention level of a large and strangely moon-like space station. Jack need to find his way back to his old spacecraft of questionable space-worthiness to escape. This project aimes to find a possible path to the hangar of the spacecraft, with a given map, to assist Jack in his escape.

### Objectives
These are the skills and concepts I encountered in this project:
- 3D Maze: read, store, access, and write
- Breadth first search with queue
- Depth first search with stack)
- Map and coordinate list mode input
- Map and coordinate list mode output
- Use `getopt_long()` to handle command line arguments

## Getting Started
### Command Line
To run the project, `ship` take the following command line options:
- `--stack`, `-s`: The routing scheme will perform a depth first search. It accepts no arguments.
- `--queue`, `-q`: The routing scheme will perform a breadth first search. It accepts no arguments.
- `--output (M|L)`, `-o (M|L)`:  Indicates the output file format by the required argument, M (map format) or L (coordinate list format). If this option is not provided when running the program, the default output format is map format.
- `--help`, `-h`: This causes the program to print a helpful message about how to use the program.

Legal command lines must include exactly one of `--stack` or `--queue` (or `-s` or `-q`).

In general, a legal command line should be `$ ./ship --stack\--queue\-s\-q (--output\-o M\L) < infile > outfile`, \ indicates "or" and () indicates "optional".

### Space Station Layout
A space station is composed of up to 10 square levels with elevators to travel between levels. The description of a space station is provided by an input file using a 3-D coordinate system and special characters.

The special characters and what they represent:
- ’.’: floor space
- ’#’: walls (Cannot be walked on/through)
- ‘S’: Starting location at the detention level
- ‘H’: the hangar of the spacecraft location (the goal)
- ‘E’: Elevators that can transport from that location to the same row and column of the levels that have an elevator on the same location

## Input File Formats
The input file is a simple text file specifying the layout of the space station, compatible with two input modes: Map Mode (M) and coordinate list mode (L).

The first three lines of an input file is the “file header”, should be formatted as follows:
```
Input mode (M or L)
Number of levels l in the space station (1 <= l <= 10)
Size n of every level (n >= 2)
```
Comments may also be included in input file,  begin with // and are allowed anywhere in any file, after the file header. 

### Map Input Mode:
Input a 2D map of characters defining each level, starting with level 0 and ending with level $l-1$. For example,
```
//level 0
.H..
....
E..S
#..#
```
### Coordinate List Input Mode:
Input a list of coordinates for at least all non-floor space characters in the space station. 
A coordinate is specified in precisely the following form: `(level,row,column,character)`. 

The level values will be in the range $[0, l)$, and the row and column values will be in the range $[0, n)$. Only one coordinate will appear on each line, and the coordinates may be grouped by floor or ordered in any way. By default, all unspecified coordinates within the space station are of type ‘.’ . For example, 
```
(0,0,1,#)
(2,2,2,H)
(1,1,3,.)    -- Unnecessary, but valid
```

## Output File Format
### Map output mode (M):
Print the map of the all levels, the path showed by characters, replacing existing characters with ‘n’, ‘e’, ‘s’, ‘w’, or ‘0-9’, as needed to show the path Jack took. 

### Coordinate list output mode (L):
Print the coordinates of each step that make up the path Jack traveled as `(level,row,column,character)`.

## File Structure
- `ship.cpp`: Executable file
- `launch.json`: Script for debugging
- `Spec/`: Different input mode files for two maps and correct outputs for all combinations, designed for debugging.
- `tests/`: Ten tests with different search schemes and input modes.
