This fork attempts to solve the [stochastic drift issue for symmetric motif input](https://github.com/RosettaCommons/RFdiffusion/issues/35). We set an RMSD threshold to the supplied motif and enforce this check each timestep along the diffusion. This problem is particularly prevalent for diffusing symmetric motifs, but presumably could occur on a sparsely trained or sufficiently complex monomeric motif.

Changes made to: model_runners.py, utils.py and run_inference.py

Set your RMSD threshold in utils.py:
```
if rms > 1.55:  # or whatever threshold you want
  self._log.warning(f"Motif RMSD too high ({rms:.2f}) — rejecting sample.")
  raise ValueError("Motif RMSD too high")
```

Default number of tries to correct RMSD under threshold is 20. Edit this value in model_runners.py:
```
max_retries = 20
```




