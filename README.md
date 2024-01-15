# cvmfs4hpc

**Rivanna method1: use cvmfsexec and a linux container to map the local cvmfs mount to /cvmfs in the container**
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
- run a container with path bound to /cvmfs (assumes we run the container from the cvmfsexec directory)
  - apptainer exec --bind `readlink -f dist/cvmfs/`:/cvmfs docker://library/ubuntu ls -l /cvmfs
  - apptainer run --bind `readlink -f dist/cvmfs/`:/cvmfs docker://library/ubuntu

**Rivanna method2: copy the directory tree of the release and use a container to mount it under /cvmfs**
- cp -a <release on cvmfs> <local directory>
  - eg 
