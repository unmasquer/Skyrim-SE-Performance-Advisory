# Skyrim-SE-Performance-Guide
Instructs necessary settings, makes suggestions and inquiries. 

so far four significant discoveries: 

1. Do not set a target fps that deviates far from what the computer can sustain. 
2. Do not disable Hardware Accelerated GPU Scheduling. 
3. flip_discard is best at softening the blow caused by the two above, but it's visually lossy compared to flip_sequential. Think of flip_discard as performance focused, and flip_sequential as quality focused. You can read more on that yourself. 
edit: apparently nvidia suggests matching MFL to SBC (MaxFrameLatency and SwapBufferCount) when using flip_discard. flip_sequential seems depreciated as whatever lossiness discard has is either old news or a bit of a misnomer. so if prioritizing smoothness, flip_discard + MFL=8 and SBC=8. want to try verifying this because I've had my best results with MFL=16 and SBC=8.
4. You can bolster flip_discard by setting MaxFrameLatency and SwapBuffer to 16 and 8 respectively (have not tried values other than stock and this extreme config), but this may come at the cost of latency, you'll have to feel it out in game. SwapEffect, SwapBuffer, and MaxFrameLatency can be tweaked in SSEDisplayTweaks. 

All of these have been repeatedly benchmarked in a high fps environment. 
