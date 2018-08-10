# GridAstar

This is an implementation of the A* path planning algorithm, specifically tailored for
2D rectangular grids.

It is inspired by other two open source implementations:

- [hjweide/a-star](https://github.com/hjweide/a-star)
- [daancode/a-star](https://github.com/daancode/a-star)

Nevertheless __GridAstar__ is 20% faster than the former and few orders (3>) of magnitude
faster than the latter.

To achied this speed, this library used a fairly large amount of RAM to perform many
operations in __O(1)__.

It requires between 10 and 18 bytes for each cell in the grid.

In other words, between 10 and 18 Mb of memory for a 1000x1000 gridmap.

## Usage 

You must pass the image using the method __setWorldData()__.

Note that the the image data must be arow-major and monochromatic.

A value of 0 (black) represents an obstacle, whilst 255 (white)
is a free cell.

```c++

    // You don't need to use this image parser, you can use your own.   
    Image image;
    ReadImageFromPGM("./data/maze_big.pgm", &image);

    AStar::PathFinder generator;

    generator.setWorldData( image.width, 
                            image.height, 
                            image.data.data() );
                
    AStar::Coord2D startPos (image.width/2, 0);
    AStar::Coord2D targetPos(image.width/2, image.height/2 -1);  
               
    auto path = generator.findPath(startPos, targetPos);

```

In the followin example, the algorithm required about 250 milliseconds
to find the solution in a 1586x1586 maze.

The pink pixels represent the cells of the grid visited by the algorithm.

![Large map](./map_out_big.png)


# License

Copyright 2018 Eurecat

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file 
except in compliance with the License. You may obtain a copy of the License at

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software distributed under the 
License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, 
either express or implied. See the License for the specific language governing permissions
 and limitations under the License.

