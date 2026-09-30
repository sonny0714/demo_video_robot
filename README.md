# Demo videos

Two short simulation videos: a robot controlled over a wireless link with two rate controllers, and a robot policy under network delay. Each picture opens a page that plays the video in the browser.

## 1. STEER vs. XferQoE on the same bandwidth trace (S-Sim)

[![STEER vs. XferQoE on the same bandwidth trace (S-Sim)](posters/xferqoe_vs_steer_ssim.png)](https://sonny0714.github.io/demo_video_robot/xferqoe-vs-steer.html)

[Play in the browser](https://sonny0714.github.io/demo_video_robot/xferqoe-vs-steer.html) · [video file](videos/xferqoe_vs_steer_ssim.mp4)

The edge server runs the robot policy and the rate controller, and only observations cross the wireless link. Both sides replay the same bandwidth trace in S-Sim, a packet-level network simulator, and run the same first 10 PokeCube tasks (ManiSkill3) with the same frozen robot policy; only the rate controller differs. 5× speed, 34 s.

- Left, STEER (a learning-based rate controller): mean frame quality 32.4%, a complete observation on 44.8% of the control ticks, 10 tasks finished in 146.5 s (10 succeeded).
- Right, XferQoE: mean frame quality 21.5%, a complete observation on 94.8% of the control ticks, 10 tasks finished in 108.4 s (7 succeeded, 3 failed).

## 2. Moving-ball task under network delay: 0 ms vs. 0–1000 ms

[![Moving-ball task under network delay: 0 ms vs. 0–1000 ms](posters/moving_ball_delay.png)](https://sonny0714.github.io/demo_video_robot/moving-ball-delay.html)

[Play in the browser](https://sonny0714.github.io/demo_video_robot/moving-ball-delay.html) · [video file](videos/moving_ball_delay_0ms_vs_0-1000ms.mp4)

A fine-tuned SmolVLA policy intercepts a moving ball (MIKASA-Robo InterceptSlow, simulation). Both sides see the same 10 ball launches. 0.75× speed, 52 s.

- Left: no delay.
- Right: every action-chunk request draws a uniform random delay of 0–1000 ms (the first chunk arrives immediately on both sides), and the robot waits for the new chunk before it moves (synchronous execution).

In this clip the left side succeeds on 5 of the 10 launches and the right side on none. Over all 200 evaluation episodes the success rates are 55.5% and 3.0%.
