# Anti-aliasing in the Universal Render Pipeline

Aliasing is a side effect that happens when a digital sampler samples real-world information and attempts to digitize it. For example, when you sample audio or video, aliasing means that the shape of the digital signal doesn't match the shape of the original signal. This means when Unity renders a line, it may appear jagged as the pixels don't align perfectly with the line's intended path across the screen.

![An example of the rasterization process creating some aliasing.](Images/aliasing-example.png)</br>*An example of the rasterization process creating aliasing.*

To prevent aliasing, the Universal Render Pipeline (URP) has multiple methods of anti-aliasing, each with their own effectiveness and resource intensity.

The anti-aliasing methods available are:

- [Fast Approximate Anti-aliasing (FXAA)](#fxaa)
- [Subpixel Morphological Anti-aliasing (SMAA)](smaa)
- [Multisample Anti-aliasing (MSAA)](#msaa)

## Fast Approximate Anti-aliasing (FXAA)<a name="fxaa"></a>

FXAA uses a full screen pass that smooths edges on a per-pixel level. This is the least resource intensive anti-aliasing technique in URP.

To select FXAA for a Camera:

1. Select the Camera in the Scene view or Hierarchy window and view it in the Inspector.
2. Navigate to **Rendering** > **Anti-aliasing**, and select **Fast Approximate Anti-aliasing (FXAA)**.

## Subpixel Morphological Anti-aliasing (SMAA)<a name="smaa"></a>

SMAA finds patterns in the borders of an image and blends the pixels on these borders according to the pattern it finds. This anti-aliasing method has much sharper results than FXAA.

To select SMAA for a Camera:

1. Select the Camera in the Scene view or Hierarchy window and view it in the Inspector.
2. Navigate to **Rendering** > **Anti-aliasing**, and select **Subpixel Morphological Anti-aliasing (SMAA)**.

## Multisample Anti-aliasing (MSAA)<a name="msaa"></a>

MSAA samples the depth and stencil values of every pixel and combines these samples to produce the final pixel. Crucially, MSAA solves spatial aliasing issues and is better at solving triangle-edge aliasing issues than the other techniques. However, it does not fix shader aliasing issues such as specular or texture aliasing.

MSAA is more resource intensive than other forms of anti-aliasing on most hardware. However, when run on a tiled GPU with no post-processing anti-aliasing or custom render features in use, MSAA is a cheaper option than other anti-aliasing types.

MSAA is a hardware anti-aliasing method. This means you can use it with the other methods, as they are post-processing effects.

To enable MSAA:

1. Open a [URP Asset](universalrp-asset.md) in the Inspector.
2. Navigate to **Quality** > **Anti Aliasing (MSAA)** and select the level of MSAA you want.

For more information on the available settings, refer to [MSAA setings in the URP Asset](universalrp-asset.md#quality).

> [!NOTE]
> On mobile platforms that don't support the [StoreAndResolve](https://docs.unity3d.com/ScriptReference/Rendering.RenderBufferStoreAction.StoreAndResolve.html) store action, if **Opaque Texture** is selected in the **URP Asset**, Unity ignores the **MSAA** property at runtime (as if **MSAA** is set to **Disabled**).
