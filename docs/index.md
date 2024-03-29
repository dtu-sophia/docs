# Sophia HPC cluster

This website is a resource with technical details for users to make efficient use of the computing and storage resources of the Technical University of Denmark's high performance computing cluster *Sophia*.

The Sophia HPC cluster runs the Linux CentOS operating system and the cluster
installation is based on the [OpenHPC](https://openhpc.community) framework.

The default shell is [bash](https://www.gnu.org/software/bash/) and
users are [encouraged](https://devhints.io/bash) to use bash 
since Sophia's compute job scheduler primarily supports this shell.

## Acknowledgment of use

Please use DOI **10.57940/FAFC-6M81** in your publication; select citation format [here https://doi.datacite.org/dois/10.57940%2Ffafc-6m81](https://doi.datacite.org/dois/10.57940%2Ffafc-6m81), and e.g. use the following text as appropriate:

*The authors gratefully acknowledge the computational and data resources provided on the Sophia HPC Cluster at the Technical University of Denmark, DOI: 10.57940/FAFC-6M81.*

## Guidelines for use

Through constructive dialogue we wish on one hand to ensure continuity and progress
in on-going research activities and on the other hand to promote
the general use of HPC in research at DTU and other Danish universities.

Optimal use of the HPC resources available requires responsible and conscientious use from the
individual user. 

  1. Read these docs pages! 
  2. When in doubt, ask! Write the address at the bottom left.
  3. The HPC resources can be used for development and testing of applications; please ensure that
reserved HPC resources are utilised and not standing idle. E.g. do not reserve multiple nodes for
code that only utilise resources on a single node.
  4. Carefully consider the impact of reserving several nodes on other users' ability to carry out their work;
e.g. inspect current load prior to job submission, e.g. postpone resource-demanding compute jobs until evening, etc.
  5. Please strive to reserve **and <u>utilise</u>** full compute nodes to the extent feasible.
  6. Do not run code on the login node! Request an [interactive job](https://dtu-sophia.github.io/docs/scheduler/#interactive-jobs).
  7. Jobs or login node usage that negatively impacts general use will be stopped and access for the offending
user may be restricted or denied if this occurs repeatedly. The decision of restriction of access or closing
an account is taken in consensus between the DTU IT Department, DTU Wind Energi and DTU Mechanical Engineering, each having one representative.

