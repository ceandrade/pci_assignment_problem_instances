Instance for the Physical Cell Identity (PCI) Assignment Problem
===============================================================================

<table>
<tr>
  <td>License</td>
  <td>
    <a href="https://github.com/ceandrade/pci_assignment_problem_instances/blob/master/LICENSE.md">
    <img src="https://img.shields.io/badge/license-BSD--like-blue" alt="License" />
    </a>
  </td>
</tr>
</table>

This project contains instances (test cases) for the 
Physical Cell Identity (PCI) Assignment Problem, also know as 
[PCI assigment](http://www.techplayon.com/5g-nr-physical-cell-id-pci-planning)
on 5G networks.

:black_nib: License and Citing
--------------------------------------------------------------------------------

This project uses a permissive BSD-like license and it can be used as it
pleases you. And since this framework is also part of an academic effort, we
kindly ask you to remember to cite the originating paper of this work.
Indeed, Clause 4 estipulates that "all publications, softwares, or any other
materials mentioning features or use of this software (as a whole package or
any parts of it) and/or the data used to test it must cite the following
article explicitly":

> C.E. Andrade, L.S. Pessoa, S. Stawiarski. The Physical Cell Identity
> Assignment Proble: a Practical Optimization Approach. IEEE Transactions
> on Evolutionary Computation. 2022, to appear.

[Check it out the full license.](https://github.com/ceandrade/pci_assignment_problem_instances/blob/master/LICENSE.md)

:books: Instances
-------------------------------------------------------------------------------

We have a total of 291 instances which are divided into three large groups:

- All/full PCIs: let `max_pci` be the mininum between the number of nodes and
  1006 (which is the maximum number of PCIs for 5G). The allowed PCIs are in
  the range `[1, max_pci + 1]`. This instance group is identified by
  prefix `full`. It should be easier to find feasible solutions for these
  instances, but hard to prove the optima, since the search space is very
  large (and symmetrical);

- Original PCIs: the allowed PCIs are in the range between the minimum and
  (maximum + 1) of the original PCIs excluding zero. This instance group is
  identified by prefix `orig`. This is the way it occurs most time in the
  practice;

- Maximum clique PCIs: let `min_pci` be the minimun of the original PCIs
  excluding zero and let `max_cliq` be the size of the
  [maximum clique](https://en.wikipedia.org/wiki/Clique_(graph_theory))
  in the graph. The allowed PCIs are in `[min_pci, min_pci + max_cliq]`.
  This instance group is identified by prefix `cliq`. For such instances,
  feasible solutions should be hard to find.


- Instances considering full PCI range `[0, 1007]`. This instance group is
  identified by suffix `full`. It should be easier to find feasible solutions
  for these instances, but hard to prove the optima, since the search space is
  very large (and symmetrical);

- Instances considering PCIs in the range between the minimum and maximum of
  the PCIs originally assigned to the nodes.  This instance group is identified
  by suffix `orig`.  This is the most common application in real life since
  usually operators restrict the allowed PCIs to a range due to operational
  constraints;

- Squeeze instances, where the idea is to find the smallest PCI range so that
  we have a feasible solution within.  Note that for such instances, feasible
  solutions should be harder to find due to a very limited number of available
  PCIs. This instance group is identified by suffix `squz`.  For more details
  in the generation of these instances, refer to
  [Section IV.B in the paper.](http://dx.doi.org) 

The naming convention is the following:
`pci_<id>_n<size>_<group>.{dat,txt,json}`.
For example, `pci_028_n0065_full`
indicates Instance 28 that allows all PCIs, and it has 65 nodes. The name
`pci_106_n1026_squz` describes Instance 106, which has 1026 nodes, and the
allowed PCIs are very limited.

Note that each instance ID has the three allowed PCI groups. In this case,
the underline graph is the same for all versions, as so as the original PCIs.
Only the allowed PCIs changes from instance to instance.

We have included a feasible solution (found by
[IBM ILOG CP Solver 12.10](https://www.ibm.com/products/ilog-cplex-optimization-studio))
for each one of the instances.
Therefore, all instances in this set are feasible. Such feasible solutions may
be a good jump start for local search heuristics, populational methods, or MIP
solvers. When reporting the total time, don't forget to include the time to
find such solutions in your final results. For example, suppose CP used 10
seconds to find a feasible solution for a given instance. Now, we allow 10 min
for our method run. So, we indeed must use 600 - 10 = 590 seconds in total. If
our method finds a good final solution in 2 minutes, we should report 130
seconds (2 min, 10 secs) since the first 10 seconds were used by CP.

All instances have the following fields:

- `instance_name`: a string with the instance name;

- `instance_group`: either "full", "orig", or "cliq";

- `min_allowed_pci` and `max_allowed_pci`: the mininum and maxinum of the range
   of the allowed PCIs;

- `module_k`: an integer indicating the module to be used;

- `num_nodes`: number of nodes or radios in the network. The node indices
   start on zero (0);

- `num_top_neighbors`: number of edges between the top neighbors, i.e.,
   nodes with highly handover between them, and for which PCI mod-k must be
   different;

- `top_neighbors`: a `num_top_neighbors X 2` matrix that indicates each edge
  of between the top neighbor;

- `num_regular_neighbors`: the number of non-top regular direct edges in the
  neighborhood network;

- `regular_neighbors`: a `num_regular_neighbors X 2` matrix that indicates
  the remaining direct edges in the network;

- `num_second_level_neighbors`: the number of edges between the second level
  neighbors, i.e., neighbor of neighbors;

- `second_level_neighbors`: a `num_second_level_neighbors X 2` matrix that
  indicates the 2nd-level edges in the network;

- `original_pcis`: the original PCIs assigned to these nodes;

- `cp_solver_time`: time in seconds for IBM ILOG CP Solver 12.10 find a feasible
  solution;

- `feasible_solution`: a list of `num_nodes` PCIs representing a feasible,
  not necessarily optimal solution;

- `num_inter_technology_neighbors` and `inter_technology_neighbors`: not used
  in this version.

Files with extension `.dat` can be read directly for most commercial MIP
solvers such as IBM ILOG CPLEX. Files ending in `.json` are in the widely used
JavaScript Object Notation, which can be easily read by most programming
languages such as C++ (using https://github.com/nlohmann/json) or Python.
Finally, files ending on `.txt` are plain text files for easy parsing
Each set of instances is enclosed in folders according to their format.

We also include the folder [`results`](https://github.com/ceandrade/pci_assignment_problem_instances/blob/master/results), 
which contains all the best results
obtained by the algorithms described [in the paper.](http://dx.doi.org) 

