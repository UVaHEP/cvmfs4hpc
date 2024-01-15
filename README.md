# cvmfs4hpc

**Rivanna method1**
- module load apptainer
- clone https://github.com/cvmfs/cvmfsexec
  - ./makedist default  (one time)
- mounts
  - ./mountrepo  cms.cern.ch
  - ./mountrepo  sft.cern.ch
- unmount
  - ./umountrepo  cms.cern.ch
  - ./mountrepo sft.cern.ch
- get local path to cvmfs
  - readlink -f dist/cvmfs/
- run a container with path bound to /cvmfs
  - apptainer exec --bind `readlink -f dist/cvmfs/`:/cvmfs docker://library/ubuntu ls -l /cvmfs
  - apptainer run --bind `readlink -f dist/cvmfs/`:/cvmfs docker://library/ubuntu
