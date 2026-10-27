# Demo videos

Short demo videos: a robot policy under network delay, a robot controlled over a wireless link by two rate controllers, robot foundation models served over a wireless link, and sixteen cameras, each on its own wireless link. Each picture opens a page that plays the video in the browser.

## 1. Moving-ball task under network delay: 0–1000 ms vs. 0 ms

[![Moving-ball task under network delay: 0–1000 ms vs. 0 ms](posters/moving_ball_delay.png)](https://sonny0714.github.io/demo_video_robot/moving-ball-delay.html)

[Play in the browser](https://sonny0714.github.io/demo_video_robot/moving-ball-delay.html) · [video file](videos/moving_ball_delay_0-1000ms_vs_0ms.mp4)

A fine-tuned SmolVLA policy intercepts a moving ball (MIKASA-Robo InterceptSlow, simulation). Both sides see the same 5 ball launches. 0.75× speed, 28 s.

- Left: every action-chunk request draws a uniform random delay of 0–1000 ms (none before a task's first chunk), and the robot waits for the new chunk before it moves (synchronous execution).
- Right: no delay.

In this clip the left side succeeds on 0 of the 5 launches and the right side on 4. Over all 200 evaluation episodes the success rates are 3.0% and 55.5%.

## 2. Rate control for robot manipulation: STEER+XferQoE's WF vs. XferQoE

[![Rate control for robot manipulation: STEER+XferQoE's WF vs. XferQoE](posters/xferqoe_pokecube.png)](https://sonny0714.github.io/demo_video_robot/xferqoe-pokecube.html)

[Play in the browser](https://sonny0714.github.io/demo_video_robot/xferqoe-pokecube.html) · [video file](videos/xferqoe_pokecube.mp4)

The edge server runs the robot policy (a frozen ManiSkill3 PokeCube policy) and the rate controller, and only the robot's observations cross the wireless link. Both runs replay the same bandwidth trace with the same policy and tasks, so only the rate controller differs. STEER+XferQoE's WF (STEER with XferQoE's objective-weight fit) plays first, then XferQoE over the same 41.7 s span. 5× speed, 28 s.

- As the link drops, STEER+XferQoE's WF keeps a bitrate the link cannot carry, so ticks arrive without a frame and the arm stands still.
- Because XferQoE lowers its bitrate first, its frames keep arriving and the pokes go on.

## 3. Remote RFM serving: the control loop and two robot foundation model tasks

[![Remote RFM serving: the control loop and two robot foundation model tasks](posters/xferqoe_rfm_serving.png)](https://sonny0714.github.io/demo_video_robot/xferqoe-rfm-serving.html)

[Play in the browser](https://sonny0714.github.io/demo_video_robot/xferqoe-rfm-serving.html) · [video file](videos/xferqoe_rfm_serving.mp4)

The robot policy is a robot foundation model (RFM) on the edge server: π0.5 in a time-invariant task (LIBERO-Spatial) and SmolVLA in a time-varying one (MIKASA Intercept). It acts on the newest camera frame that arrives within its deadline, and the rate controller decides how the frames cross the wireless link. The video first animates this control loop on the system diagram. It then plays the first five tasks of each on one bandwidth trace with the same model and scene, STEER+XferQoE's WF first and XferQoE second. Only the rate controller differs between the two runs. 1.5× and 0.7× speed, 2 min 42 s.

- STEER+XferQoE's WF sends more than the link carries, so the RFM acts on a past scene and misses the bowl and the ball.
- Because XferQoE's frames arrive in time, the RFM completes the task.

## 4. Remote monitoring: the control loop and sixteen cameras on their own links

[![Remote monitoring: the control loop and sixteen cameras on their own links](posters/xferqoe_monitoring.png)](https://sonny0714.github.io/demo_video_robot/xferqoe-monitoring.html)

[Play in the browser](https://sonny0714.github.io/demo_video_robot/xferqoe-monitoring.html) · [video file](videos/xferqoe_monitoring.mp4)

Sixteen cameras each send frames over their own wireless link to a server whose recognition model detects objects in them, and every interval is scored by detection F1 against the current ground truth. The video first animates this control loop on the system diagram. It then shows the ground truth, STEER+XferQoE's WF, and XferQoE on the same bandwidth trace from 145 to 185 s at 1× speed. The per-camera link opens at 167 s.

- On the slow link STEER+XferQoE's WF sends above what the link carries, so its tiles turn yellow and red and the detector misses pedestrians.
- XferQoE's lower bitrate keeps frames current and detections up.
