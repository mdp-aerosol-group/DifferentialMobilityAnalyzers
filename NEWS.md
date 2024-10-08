# DifferentialdMobilityAnalyzers.jl NEWS

#### Notes on release changes and ongoing development
- v2.5.5 tested with Julia 1.6.1
- v2.4 supports Julia 1.5 (works on 1.4)
- v2.3 supports Julia 1.5 (works on 1.4)
- v2.2 supports Julia 1.5 (works on 1.4)
- v2.1 supports Julia 1.5 (works on 1.4)
- v2.0 supports Julia 1.1
- Version 1.0.0 is the last one to support Julia 0.6.4

---

# v3.0.1
- Fix broadcasting bug in vtoz for radial DMAs

# v3.0.0
- Rebase to different host (https://github.com/mdp-aerosol-group/DifferentialMobilityAnalyzers)
- Flatten repo by removing commit history. This was done to improve load times and remove stale files. The repo was changed so the old repo remains available for historical reasons.

# v2.5.6
- Add support for multiple gases. Currently Air() and N2() are implemented. The gas can be passed as argument to DMAconfig. Calling DMAconfig without specifying the gas defaults to Air(). Additional gas parameterizations can be added by adding dispatch to the mean free path and viscosity functions. 
- Merge CompatHelper: bump compat for CSV to 0.9
- Update Project/Manifest 
- remove PI function and gfk function 

# v2.5.5
- CompatHelper: bump compat for "BenchmarkTools" to "1.0" 
- Update Project/Manifest
- Fix not passing bounds for lambda1 and lambda2 to regularization solver
- Fix restrictive assumptions for diffusional broadening treatement
- Fix restrictive assumptions for tandem DMA transfer

# v2.5.4
- Merge CompatHelper: bump compat for "Distributions" to "0.25"

# v2.5.3
- Merge CompatHelper: bump compat for "DataFrames" to "1.0"

# v2.5.2
- Merge CompatHelper: bump compat for "BenchmarkTools" to "0.7"
- Tested for potential Julia 1.6 regressions (none found)

## v2.5.1
- Merge CompatHelper: bump compat for "BenchmarkTools" to "0.6"

## v2.5
- Add gfₖ function for multicharge treatment of mobility distribution function in HTDMA
- Add TDMA model functions for matrix based TDMA data inversion 
- Add memoization of slow functions (setupSMPS, setupDMA, setupSMPSdata, and 
initializeDefaultMatrices). This speeds up code when called with the same input parameters.
- Remove most global variables in dmafunctions; the globals resulted in sometimes
inconsistent results when multiple DMAs were initialized in the same script. 
- One global variable remains in the code for compatibility reasons, otherwise the code should be pure 
- Memoization means that rinv(R, δ) has no longer a performanc penalty when called multiple times with the same DMA δ. This makes the method rinv2(R) unnecessary and it is removed.  
- Removal of globals required moving the function Ωₐᵥ into setupSMPS, due to a previous implicit
dependence on a global. Reference to this function in the docs is removed.

## v2.4
- Update documentation for rinv2 and add logo
- Merged CompatHelper: bump compat for "Interpolations" to "0.13
- Add rinv2 function based on RegularizationTools.jl. Intended to supersede rinv and supports higher order inversions and performance gains.
- Revisions related to the addition of rinv2
- Thinned out Project.toml and added Compat section.

## v2.3
- Various small bugfixes discovered during documentation.
- Add benchmark scripts to track performance across CPU architectures and over time.
- Add self-contained examples folder with code that matches the docs.
- Add docstrings and write Documenter.jl documentation for the package.
- Add links to Docker container with precompiles sys image.
- Add links to narrated tutorial notes to manual.
- Add interpolateSizeDistributionOntoδ function. This is match grids for chained DMA systems.
- Add recommendation for MKL library for additional performance gain
- Signficant speedup in inversion by switching to Choleskey decomposition for computing the inverse
- Revise search functions for performance gain.
- Limit number of BLAS threads to 1 for factor 4 speedup in inversion.

## v2.2
- Add interpolateDataFrameOntoδ function. This is used to convert a  measured size distribution stored as a DataFrame and to a SizeDistribution that matches a DMA grid. The function simplifies using the package with real data.
- Preallocate identity matrix
- Fix performance regression caused by changes in 2.1
- Add subtraction operator: 𝕟1 - 𝕟2
- Remove Plots.jl/PlotlyJS.jl/ORCA.jl dependencies for core project. The packages are still needed for executing the notebooks but they don't need to be installed when the package is embedded for regular use and carry a lot of overhead.

## 2.1
- Fix deprecation warnings from DataFrames API
- Use generic types: AbstractFloat, Vector{<:AbstractFloat} and AbstractMatrix. This fixes an error for  𝐀 * 𝕟 if 𝐀 is of Adjoint type, the default output of Eq. 8 in the paper.
- Ensure symmetry to size distribution arithmetic, i.e. 𝐀 * 𝕟 == 𝕟 * 𝐀; a * 𝕟 == 𝕟 * a; T * 𝕟 == 𝕟 * T; a ⋅ 𝕟 == 𝕟 ⋅ a. 
- Update packages and tests to be compatible with Julia 1.5

## 2.0
- Fix deprecations to be compatible with Julia 1 series.
- Switch all Jupyter documentation graphs from javascript to svg. 
- Remove broadcasting . operator for all operations with size distributions (𝕟 * 𝕟 instead of 𝕟 .* 𝕟 and EF ⋅ 𝕟 instead of EF .⋅ 𝕟). 
- Designate DMA geometry :cylindrical or :radial in DMAconfig   

## 1.0.0
- Version released with the manuscript
