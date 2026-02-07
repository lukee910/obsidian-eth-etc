## Idea
Simulate the [[Participating Media]] properly.

With Path Tracing etc., the [[Radiance]] stays constant on a ray. This will be different here.
## Examples
- Clouds
	- Lots of scattering
	- Don't absorb much light, paths stay relevant
	- Scattering usually happens in a similar direction as the original ray. Very "peaky" scattering, only few angles where it contributes.
- Fire
	- Emissive volume
- Water
	- E.g. Over longer distance things fade out
- Ice, Wax
	- Surface or Volume? Could model as both.
- Dust
	- Visible sun rays
- Aerial Perspective, Atmospheric Perspective
	- Objects in the distance become more faded
- Nebulae
	- Note: Most of this theory was initially developed for astrophysics before being adopted to CG
## Radiance
[[Participating Media Radiance]]
