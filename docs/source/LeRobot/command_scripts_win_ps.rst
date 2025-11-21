*******
Scripts
*******

lerobot-setup-motors --robot.type=so101_follower --robot.port=COM3

lerobot-calibrate  --robot.type=so101_follower --robot.port=COM3 --robot.id=my_awesome_follower_arm # <- Give the robot a unique name

lerobot-setup-motors --teleop.type=so101_leader --teleop.port=COM4  # <- paste here the port found at previous step

lerobot-calibrate  --teleop.type=so101_leader --teleop.port=COM4 --teleop.id=my_awesome_leader_arm # <- Give the robot a unique name

lerobot-teleoperate --robot.type=so101_follower --robot.port=COM3 --robot.id=my_awesome_follower_arm --teleop.type=so101_leader --teleop.port=COM4 --teleop.id=my_awesome_leader_arm

lerobot-teleoperate --robot.type=so101_follower  --robot.port=COM3 --robot.id=my_awesome_follower_arm --robot.cameras="{ front: {type: opencv, index_or_path: 0, width: 640, height: 480, fps: 30}}" --teleop.type=so101_leader --teleop.port=COM4 --teleop.id=my_awesome_leader_arm --display_data=true

# TODO add the ----dataset.single-task==""

lerobot-record   --robot.type=so101_follower  --robot.port=COM3 --robot.id=my_awesome_follower_arm --robot.cameras="{ front: {type: opencv, index_or_path: 0, width: 640, height: 480, fps: 30,  fourcc: 'MJPG'}}" --teleop.type=so101_leader --teleop.port=COM4 --teleop.id=my_awesome_leader_arm --display_data=true --dataset.repo_id=${HF_USER}/record-test --dataset.num_episodes=5 --dataset.single_task="Pick up banana." --dataset.push_to_hub=True

lerobot-train  --dataset.repo_id=${HF_USER}/record-testonline --policy.type=act --output_dir=outputs/train/act_so101_tes --job_name=act_so101_test --policy.device=cpu --wandb.enable=False --policy.repo_id=${HF_USER}/my_policy --dataset.single_task="Pick up banana."

lerobot-record   --robot.type=so101_follower  --robot.port=COM3 --robot.id=my_awesome_follower_arm --robot.cameras="{ front: {type: opencv, index_or_path: 0, width: 640, height: 480, fps: 30,  fourcc: 'MJPG'}}" --dataset.repo_id=JiaMinEsc/infre --policy.path=JiaMinEsc/record-testonline --dataset.single_task="Pick up banana."
