# naive adjacency matrix [![Build Status](https://travis-ci.org/mkfifo/naive_adjacency_matrix.svg)](https://travis-ci.org/mkfifo/naive_adjacency_matrix) [![Coverage Status](https://coveralls.io/repos/mkfifo/naive_adjacency_matrix/badge.svg)](https://coveralls.io/github/mkfifo/naive_adjacency_matrix)

A naive adjacency matrix implementation

The `naive` comes from the fact that each edge is represented using a whole char,
which is poor utilisation of space since we only over store a '0' (no edge), or '1' (edge).

For a more space efficient solution see https://github.com/mkfifo/bitwise_adjacency_matrix

Time / Speed comparisons will come shortly.

Example usage
--------------

    #include <stdio.h>

    #include "naive_adj_mat.h"

    int main(void){
        /* create a new adjacency matrix with 3 nodes */
        struct naive_adj_mat *nam = nam_new(4);

        /* temporary integers used later */
        int i = 0;
        int j = 0;
        int n = 0;

        /* add some edges */
        /* 0 -> 1 */
        nam_add_edge(nam, 0, 1);
        /* 0 -> 2 */
        nam_add_edge(nam, 0, 2);
        /* 2 -> 3 */
        nam_add_edge(nam, 2, 3);

        /* test existing connections */
        if( nam_test_edge(nam, 0, 1) ){
            puts("edge exists from 0 to 1");
        }

        /* test non-existing connections */
        if( ! nam_test_edge(nam, 1, 0) ){
            puts("no edge exists from 1 to 0");
        }

        /* delete edge 0 -> 1 */
        nam_remove_edge(nam, 0, 1);

        /* test removed connections */
        if( ! nam_test_edge(nam, 0, 1) ){
            puts("removed edge from 0 to 1");
        }

        /* get number of nodes */
        n = nam_size(nam);

        puts("\nlist of all edges");

        /* iterate through nodes */
        for( i = 0; i<n; ++i ){
            for( j=0; j<n; ++j ){
                if( nam_test_edge(nam, i, j) ){
                    printf("%d -> %d\n", i, j);
                }
            }
        }

        /* cleanup
         *  destroy(nam, free_nam) */
        nam_destroy(nam, 1);

        return 0;
    }

output:

    chris@Ox1b naive_adjacency_matrix(master)-> make example

    running example
    ./example
    edge exists from 0 to 1
    no edge exists from 1 to 0
    removed edge from 0 to 1

    list of all edges
    0 -> 2
    2 -> 3

