# Skyrim-SE-Performance-Advisory
points to some settings necessary for avoiding performance degredation.

real optimization isn’t about chasing raw FPS — it’s about minimizing worst-case performance and smoothing frame delivery.

significant discoveries so far: 

1. Do not set a target fps that deviates far from what the computer can sustain. 
2. Do not disable Hardware Accelerated GPU Scheduling. 
3. flip_discard is best at softening the blow caused by the two above.
edit: apparently nvidia suggests matching MFL to SBC (MaxFrameLatency and SwapBufferCount) when using flip_discard. flip_sequential seems depreciated as whatever lossiness discard has is either old news or a bit of a misnomer. so if prioritizing smoothness, flip_discard + MFL=8 and SBC=8. want to try verifying this because I've had my best results with MFL=16 and SBC=8.
4. You can bolster flip_discard by setting MaxFrameLatency and SwapBuffer to 16 and 8 respectively (have not tried values other than stock and this extreme config), but this may come at the cost of latency, you'll have to feel it out in game. SwapEffect, SwapBuffer, and MaxFrameLatency can be tweaked in SSEDisplayTweaks. 
5. At the very least, CS's implementation of DLSSG sees significant frametime degredation when using RTSS or Display Tweak's framepacing favoring method of frame limiting instead of NVCP. Do not own an AMD card, so can't verify that side of things. 
6. At the very least, Pure Dark's implementation of FG also sees signfiicant frametime degredation when using RTSS or Display Tweaks framepacing favoring method of frame limiting instead of NVCP. Still don't own an AMD card.  
7. CPU Affinity plugin for MO2 should be avoided unless you know what you're doing in which case its very unlikely you're going to be pinning Skyrim to just two physical cores and 0 and 2 specifically, which are very likely the most contentious cores on your system. placeholder. commit detailing soon. 

all of these have been repeatedly benchmarked for consistency. 
