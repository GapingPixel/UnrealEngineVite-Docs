# DDGI and Raytracing

## DDGI

NVIDIA Readme:

[UE5-PhysX-Vite/Engine/Plugins/Runtime/Nvidia/RTXGI at ue5Vite-release · GapingPixel/UE5-PhysX-Vite](https://github.com/GapingPixel/UE5-PhysX-Vite/tree/ue5Vite-release/Engine/Plugins/Runtime/Nvidia/RTXGI)

GDC Presentation

[Dynamic Diffuse Global Illumination](https://developer.download.nvidia.com/video/gputechconf/gtc/2019/presentation/s9900-irradiance-fields-rtx-diffuse-global-illumination-for-local-and-cloud-graphics.pdf)

Ray-Traced Irradiance Fields: </br>
[![Ray-Traced Irradiance Fields](https://img.youtube.com/vi/KufJBCTdn_o/0.jpg)](https://www.youtube.com/watch?v=KufJBCTdn_o)

DDGI Sample Scene, Setup, and combined usage with SSGI: </br>

[![DLSS and RTXGI Unreal Engine 4 Plugin: Settings Deep Dive](https://img.youtube.com/vi/ZefvmV1pdP8/0.jpg)](https://www.youtube.com/watch?v=ZefvmV1pdP8&t=1210s)

DDGI Plugin Settings: </br>

[![NVIDIA RTXGI Unreal Engine 4 Plugin: Settings Deep Dive](https://img.youtube.com/vi/U57_a3lGKOo/0.jpg)](https://www.youtube.com/watch?v=U57_a3lGKOo)

Full Official RTXGI Playlist:

[![Getting Started with NVIDIA RTXGI Unreal Engine 4 Plugin](https://img.youtube.com/vi/bxEVMnyXxqw/0.jpg)](https://www.youtube.com/playlist?list=PL4FII4B-zM0f5h75klcOfiO1v_atlp8Ky)

*DDGI in Vite has further integration with the RT pipeline from the NvRTX branches, in contrast to the 4.27 Launcher DDGI Plugin feature set. Including features such as Probe-Based RT Reflection (greatly improves the quality of RT reflections), among other integrations.

[DDGI 1.1.5 Plugin](https://github.com/GapingPixel/UE4-RTXGI-1.1.5-Latest-Official)

Launcher 4.27 Plugin: This is for Non Vite, Launcher 4.27 (do not use for Vite as it already has the plugin from the repo). Ideal for team members in a project who are not programmers. In many cases, a project can be developed using Vite, while artists and content creators continue to work on the same project through Unreal Engine 4.27 installed via the Epic Games Launcher.

## Raytracing

On top of the UE4 raytracing features, Vite integrates changes from Nvidia branches NvRTX 4.27 and most of NvRTX 5.0. Also, AMD Open RT optimizations have been integrated (Vite has several AMD specific GPU optimizations for consoles)

Major features from here are RTXDI(Megalights alternative), RT Caustics, Enhanced Translucency and DLSS 3  

At the End of Readme: [GapingPixel/UE5-PhysX-Vite: Hyper performant UE Fork with Full-Suite 9th Gen features distinct to Epic's UE5. DDGI, PhysX, RTXDI, TressFX, Tessellation, SMAA, improved Tooling and general optimizations](https://github.com/GapingPixel/UE5-PhysX-Vite)

Use the following commands to enable RT features:

```C++
IConsoleManager::Get().FindConsoleVariable(TEXT("r.GlobalIllumination.ExperimentalPlugin"))->Set(1);
IConsoleManager::Get().FindConsoleVariable(TEXT("r.SSGI.Enable"))->Set(1); // To be used in Tandem with DDGI for high frequency detail


IConsoleManager::Get().FindConsoleVariable(TEXT("r.RayTracing.AmbientOcclusion"))->Set(1);
IConsoleManager::Get().FindConsoleVariable(TEXT("r.RayTracing.Reflections"))->Set(1);
IConsoleManager::Get().FindConsoleVariable(TEXT("r.RayTracing.Shadows"))->Set(1);
IConsoleManager::Get().FindConsoleVariable(TEXT("r.RayTracing.Translucency"))->Set(1);
IConsoleManager::Get().FindConsoleVariable(TEXT("r.RayTracing.ForceAllRayTracingEffects"))->Set(1);
IConsoleManager::Get().FindConsoleVariable(TEXT("r.RayTracing.SampledDirectLighting"))->Set(1);
IConsoleManager::Get().FindConsoleVariable(TEXT("r.RayTracing.MeshCaustics.Enable"))->Set(1);
```

A well-known title that used these RT features is Black Myth Wukong

[![Black Myth: Wukong | Ray Tracing ON/OFF Comparison | RTX 4080 Super](https://img.youtube.com/vi/A5boaueGopg/0.jpg)](https://www.youtube.com/watch?v=A5boaueGopg)

Download the  Abandoned Apartment Demo Project (from Nvidia) </br>
[https://drive.google.com/file/d/1OCb9sW9xH3FsFUza0ZG1tKWOPMMus5XA/view?usp=sharing](https://drive.google.com/file/d/1OCb9sW9xH3FsFUza0ZG1tKWOPMMus5XA/view?usp=sharing)

Download the Attic Demo Project and Build (from Nvidia)


Download Vite Tech Samples Project: </br>
[Vite_TechSamples.7z - Google Drive](https://drive.google.com/file/d/1SuHlT4KC3nTQrB2rwVcwBpNgWa_r6yKh/view)