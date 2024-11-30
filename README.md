# Daily Task Reward System

This contract allows users to manage tasks, earn reward points upon completing them, and redeem those points. The contract features functionality for adding tasks, marking them as completed, tracking points, and redeeming rewards.



## Overview

The `DailyTaskRewardSystem` contract is designed to allow users to:
1. Register daily tasks and associate them with a name and description.
2. Mark tasks as completed to earn reward points.
3. Redeem reward points once a specified threshold is met.
4. View and manage the user's tasks and points.

The system uses a completion window of 1 day for tasks, and users receive a fixed number of reward points (10) for completing tasks within the specified window.

## Features
- **Task Registration**: Users can add tasks with a name and description.
- **Task Completion**: Users can mark tasks as completed to earn reward points within a 24-hour window.
- **Points Redemption**: Users can redeem their accumulated points if they reach the threshold.
- **Task Management**: Users can remove tasks from their list.

## Smart Contract Structure

The contract is composed of the following key components:
- **Owner**: The contract deployer has administrative access.
- **Tasks**: Users can create tasks with names, descriptions, and completion statuses.
- **Points**: Users earn points for completing tasks and can redeem them once a threshold is met.

