This is a implementation of Photon-Driven Manifold Sampling on top of the original Specular Manifold Sampling Code base.
More specifically we implemented PMS inside SMS multi-scatter variant.

Build:
	Replacing the following file in the SMS code:
		include/mitsuba/render/manifold.h
		include/mitsuba/render/manifold_ms.cpp
		src/integrators/path_sms_ms.cpp
		src/librender/manfold_ms.cpp
	then just build it like a normal mitsuba 2 project, you should be good to go :)

here we also provide a sample scene - three slabs inside of the folder three_slabs.
do note that for both SMS and PMS, it is required to flag each specular object as "caustic_caster_multi", "caustic_emitter_multi" or "caustic_bouncer" with in the scene setup