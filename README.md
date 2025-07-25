# PMS
![未命名](https://hackmd.io/_uploads/ryi2RLlwxg.jpg)
This is an implementation of [Photon-Driven Manifold Sampling](https://dl.acm.org/doi/10.1145/3675375) (PMS), based on the original [Specular Manifold Sampling (SMS) codebase](https://github.com/tizian/specular-manifold-sampling)
- implement PMS inside SMS-multi-scatter integrator
- accompany with an example scene -- three slabs (modified from slab scene in SMS)
## Build Instructions
1. Clone the [Specular Manifold Sampling](https://github.com/tizian/specular-manifold-sampling) repository.
2. Replace the relevant files with the ones from this repository.
3. Follow the same build instructions provided for [Mitsuba 2](https://mitsuba2.readthedocs.io/en/latest/src/getting_started/compiling.html).
## Setup
- to use PMS, set the mitsuba scene to render using `path_sms_ms` integrator
- compare to SMS, there are additional integrator parameters can be adjust
    - example scene file can be found under three_slabs folder `three_slabs/3slab_sms.xml`.
```xml
<integer name="random_mode"             value="$random_mode"/>
<integer name="photon_count"            value="$photon_count"/>
<float 	 name="update_prob"             value="$update_prob"/>
<boolean name="photon_jitter"           value="$photon_jitter"/>
<float 	 name="photon_cone"             value="$photon_cone"/>
```
- `random_mode` decide how we choose photon
    - 0: choosing the closest photon
    - 1: uniformly selection photon
    - 2: closer photon have higher change to get selected (the effect of this can be tuned with this `update_prob`)
    - 3: using RIS
- `update_prob`: the probability (should be set between 0 and 1) to select the choser photon
    - this is only use when `random_mode` is set to 2
    - 1: will perform identical to choosing the closest photon
    - 0: will perform identical to uniformly selection photon
    - anything in between will basically be an interpolation of the two methods
- `photon_count` deicde how many photons are traced into the scene
- `photon_jitter` enable photon path purterbation (recommend to enable)
- `photon_cone` how big the perturbation cone should be set to (angle)
    - this is only used when `photon_jitter` is enabled
