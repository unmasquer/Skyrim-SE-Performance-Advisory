# Skyrim-SE-Performance-Advisory

Real optimization isn’t about chasing raw FPS — it’s about minimizing worst-case performance and smoothing frame delivery.

This page points to some settings necessary for avoiding performance degredation.

Significant discoveries so far in no particular order: 

1. Do not set a target fps that deviates far from what the computer can sustain. 
   The more resources your PC wastes on simpler scenes rendering unconstrained, the less resources it'll have when transitioning to something more complex. this isn't just a resource issue, its a 
   swapchain/renderque one as well, which is an issue across virtually all games and render APIs afaik.
   
   (Frametime Performance impact: Very Very Very High)

3. Do not disable Hardware Accelerated GPU Scheduling.
   Skyrim is already CPU bottlenecked, and so when HAGS is off, every frame requires more CPU intervention, which severely harms performance based on my testing. 
  
   (Frametime Perf Impact: Very Very High)

4. flip_discard is best at softening the blow caused by the two above.
   edit: apparently nvidia suggests matching MFL to SBC (MaxFrameLatency and SwapBufferCount) when using flip_discard. flip_sequential seems depreciated as whatever lossiness discard has is either old news or a 
   bit of a misnomer. so if prioritizing smoothness, flip_discard + MFL=8 and SBC=8. want to try verifying this because I've had my best results with MFL=16 and SBC=8. 
   
   (Frametime Perf Impact: High, but only if PC 
   is rendering unconstrained (dont do that))

5. You can bolster flip_discard by setting MaxFrameLatency and SwapBuffer to 16 and 8 respectively (have not tried values other than stock and this extreme config), but this may come at the cost of latency, you'll 
   have to feel it out in game. SwapEffect, SwapBuffer, and MaxFrameLatency can be tweaked in SSEDisplayTweaks. 
   
   (Frametime Perf Impact: Moderate, but only if PC is 
   rendering unconstrained (dont do that))

6. At the very least, Community Shader's implementation of DLSSG sees significant frametime degredation when using Rivatuner Statistics Server or Display Tweak's framepacing favoring method of frame limiting 
   instead of NVCP. Do not own an AMD card, so can't verify that side of things. 
   
   (Frametime Performance impact: Very Very High)

7. At the very least, Pure Dark's implementation of Frame Generation also sees signfiicant frametime degredation when using Rivatuner Statistics Server or Display Tweaks framepacing favoring method of frame 
   limiting instead of Nvidia Control Panel. Still don't own an AMD card. 
   
   (Frametime Performance impact: Very Very Very High)

8. CPU Affinity control should be avoided unless you know what you're doing. 
  
   (Frametime Performance impact: Minimal to batshit insanely bad)
   
   
All of these have been repeatedly benchmarked for consistency. Stay tuned, I will be livestreaming benchmarks of these settings on top of what's already been personally verified. Youtube link here: 
https://www.youtube.com/@wellyouthoughtwrong3429
