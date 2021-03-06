On2 algorithm:
    on big numbers:
        10000 and 23000 with 1 thread = 47896
                        with 4 threads = 29784
                        with 8 threads = 25734
                        with 16 threads = 26278

        10000 and 2300  with 16 threads = 3017
                        with 8 threads = 2974
                        with 4 threads = 3200
                        with 1 thread = 4829

        1000 and 2300   with 1 thread = 833
                        with 4 threads = 685
                        with 8 threads = 604
                        with 16 threads = 637

    The algorithm is based on a divide and conquer method.
    It splits each polynomial in halves and computes recursively the multiplication on each of the 4 resulting pairs.
    The parallelized version takes a maximum number of Threads. Using the Stencil pattern, Each thread starts
    the multiplication of each pair with a maximum number of threads equal to a quarter of the initial value.
    the First pair is computed on the parent thread.
    when a thread starts with a maximum no of threads equal to 1, the computations are run sequentially.
    To use the sequential algorithm, start the On2 with a maximum no of threads equal to 1.

Karatsuba algorithm:
    on big numbers:
        100000 and 23000 with 16 threads = 37062

        10000 and 23000 with 1 thread = 8055
                        with 4 threads = 6535
                        with 8 threads = 5534
                        with 16 threads = 4762

        10000 and 2300  with 16 threads = 1863
                        with 8 threads = 1977
                        with 4 threads = 1971
                        with 1 thread = 1853

        1000 and 2300   with 1 thread = 492
                        with 4 threads = 460
                        with 8 threads = 416
                        with 16 threads = 387

        The algorithm is based on a divide and conquer method.
        It splits each polynomial in halves, where half means factorizing the terms of degree at least N/2 with X^N/2.
        It then computes recursively the algorithm on three sets of pairs: D0: the two lower parts from each polynomial,
        D1: the upper parts, and D01: the parts of each polynomial summed together.

        The parallelized version takes a maximum number of Threads. Using the Stencil pattern, Each thread starts
        the algorithm for computing D1 and D01 on a different thread as long as there are still threads left,
        and computes D0 itself. The number of threads is divided equally between the three threads;
        when a thread starts with a maximum no of threads equal to 1, the computations are run sequentially.