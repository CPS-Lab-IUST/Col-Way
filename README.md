# Col-Way Cache Implementation in gem5

This repository contains an implementation of the Col-Way cache architecture, as described in the paper:

**Col-Way: Collocation-Way Set Associative Cache**
(Provide the full citation or a link to the paper here)

This implementation was done using the gem5 simulator.

## Submodule: gem5 

To manage the gem5 simulator code, this repository utilizes a submodule pointing to my personal gem5 repository hosted on GitHub. You can add the submodule using this command:

```
git submodule add <your_gem5_repo_url> gem5
```

**Note:** Replace `<your_gem5_repo_url>` with the actual URL of your gem5 repository on GitHub.

**To initialize the submodule after cloning this repo:**

```bash
git submodule init
git submodule update
```

## Purpose

The purpose of this project is to evaluate the effectiveness of the Col-Way cache architecture by simulating it in the gem5 environment and comparing its performance to traditional set-associative caches.

## Col-Way Cache Overview

The Col-Way cache is a novel set-associative cache design aimed at reducing conflict misses without increasing the number of ways. It achieves this through:

*   **Dynamic Set Merging:**  The cache monitors the number of replacements in each set and dynamically merges heavily used sets with underutilized sets.
*   **Workload Balancing:** This approach aims to balance the workload across the cache, preventing the accumulation of misses in specific sets.
*   **Reduced Conflict Misses:** By enabling sets to share resources, Col-Way reduces the overall number of evictions and improves cache hit rates.
*   **Col-Way Address Management:** Two strategies are implemented to accommodate merged sets (please refer to the paper for details).
*   **Col-Way Deallocation:** After each eviction from a split set, the state of the set is checked and deallocated if necessary, to provide balance in the cache. (See the paper for further details.)

## Implemented Features

The following key features of the Col-Way cache have been implemented based on the research paper:

*   [x] Dynamic set merging and splitting logic
*   [x] Mechanism for monitoring replacement counts
*   [x] Hardware configuration for different set states, as shown in the paper.
*   [x] Col-Way address management.
*   [x] Col-Way Deallocation.

## How to Run

To run the simulation:

1.  **Clone this repository:**

    ```bash
    git clone <this_repo_url>
    cd <this_repo_name>
    ```
2.  **Initialize the gem5 submodule:**

    ```bash
    git submodule init
    git submodule update
    ```
3.  **Build gem5:** (See the `gem5/README.md` in your submodule for detailed instructions). You will need to build gem5 using `scons`, please refer to the submodule README file to build gem5.
4.  **Place the `col-way.py` file:** Copy the `col-way.py` file from the root directory of this repository into the `gem5/configs/cache` directory within your gem5 submodule.
5.  **Run the simulation:** Use the following command in the root of the project, where `.` is this repositoy.

     ```bash
    ./gem5/build/ARM/gem5.opt -d <output_directory> ./gem5/configs/example/se.py  --caches --l2cache  --l2_config=col-way --l2_size=<L2_SIZE> --l2_assoc=<L2_ASSOC>  --cpu-clock=<CPU-CLOCK> --sys-clock=<SYS_CLOCK>  --mem-type=DDR3  --mem-size=<MEM_SIZE>  -c <benchamark>
    ```
    **Important:** 
    *  Replace the placeholder values (`<output_directory>`, `<L2_SIZE>`, `<L2_ASSOC>`, `<CPU-CLOCK>`, `<SYS_CLOCK>`, `<MEM_SIZE>`, and `<benchamark>`) with your desired simulation parameters.
    * You must choose a valid benchmark from the SPEC CPU2006 suite.

## Results

The results of the simulation will be stored in the directory specified by the `<output_directory>` parameter.

## Future Work

*   [ ] Add more flexibility to the simulation of cache parameters.
*   [ ] Add more benchmarks from SPEC CPU2006.
*   [ ] Implement the Col-Way cache in multi-level cache hierarchies.
*   [ ] Explore Col-Way's performance in multi-core environments.

## Author

[Your Name] - [Your GitHub Profile Link]

## License

[Your License Information]
