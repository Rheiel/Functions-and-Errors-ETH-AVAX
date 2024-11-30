// SPDX-License-Identifier: MIT
pragma solidity ^0.8.26;

contract DailyTaskRewardSystem {
    address public owner;
    uint256 public constant REWARD_POINTS = 10;
    uint256 public constant REDEEM_THRESHOLD = 30;
    uint256 public constant COMPLETION_WINDOW = 1 days;

    struct Task {
        string name;
        string description;
        uint256 timestamp;
        bool isCompleted;
    }

    mapping(address => Task[]) private userTasks;
    mapping(address => uint256) private userPoints;

    modifier onlyOwner() {
        require(msg.sender == owner, "Access restricted to the owner");
        _;
    }

    constructor() {
        owner = msg.sender;
    }

    // Register a new task for the sender
    function addTask(string calldata _name, string calldata _description) external {
        require(bytes(_name).length > 0, "Task name cannot be empty");
        require(bytes(_description).length > 0, "Task description cannot be empty");

        userTasks[msg.sender].push(Task(_name, _description, block.timestamp, false));
    }

    // Complete a task and earn points if completed within 24 hours
    function markTaskComplete(uint256 _taskIndex) external {
        require(_taskIndex < userTasks[msg.sender].length, "Invalid task index");

        Task storage task = userTasks[msg.sender][_taskIndex];
        require(!task.isCompleted, "Task already completed");
        require(block.timestamp <= task.timestamp + COMPLETION_WINDOW, "Completion window exceeded");

        task.isCompleted = true;
        userPoints[msg.sender] += REWARD_POINTS;
    }

    // Redeem points once the user has reached the threshold
    function redeemReward(uint256 _points) external {
        require(_points > 0, "Points to redeem must be greater than zero");
        require(userPoints[msg.sender] >= _points, "Insufficient points");

        uint256 initialPoints = userPoints[msg.sender];
        userPoints[msg.sender] -= _points;

        assert(userPoints[msg.sender] == initialPoints - _points);
    }

    // Remove a task by index
    function removeTask(uint256 _taskIndex) external {
        require(_taskIndex < userTasks[msg.sender].length, "Invalid task index");

        // Shift the last task into the deleted task's position and pop the last element
        userTasks[msg.sender][_taskIndex] = userTasks[msg.sender][userTasks[msg.sender].length - 1];
        userTasks[msg.sender].pop();
    }

    // Get the user's total points balance
    function getPoints() external view returns (uint256) {
        return userPoints[msg.sender];
    }

    // Get the user's tasks
    function viewTasks() external view returns (Task[] memory) {
        return userTasks[msg.sender];
    }
}
