# Reinforcement Learning Learning Series

A comprehensive educational series of Jupyter notebooks teaching reinforcement learning
algorithms from fundamentals to state-of-the-art. Each notebook demonstrates different
RL paradigms using **LunarLander-v3** for consistent comparison across all algorithms.

## 🚀 Our Learning Environment: LunarLander-v3

For this entire learning series, we use **LunarLander-v3** exclusively. This environment is perfect for RL education because it offers both discrete and continuous action spaces, rich vector observations, and clear success/failure conditions.

**Reference**: [Gymnasium Box2D Environments](https://gymnasium.farama.org/environments/box2d/)

### LunarLander-v3 🚀

Classic rocket trajectory optimization - land the lunar module safely on the landing pad.

**Observation**: `Box((8,), float32)` - Position, velocity, angle, angular velocity, leg ground contact
**Action Spaces**:
- **Discrete**: 4 actions [do_nothing, fire_left, fire_main, fire_right]
- **Continuous**: `Box(-1, +1, (2,), float32)` - [main_engine_throttle, lateral_booster_throttle]

**Rewards**: Distance/speed penalties, angle penalties, +10 per leg contact, engine costs, ±100 for crash/landing

### Why LunarLander-v3 for RL Education?

- **Dual Action Spaces**: Perfect for testing both discrete and continuous control algorithms
- **Vector Observations**: Rich, interpretable 8D state representation with physics-based features
- **Realistic Physics**: Box2D physics engine provides consistent, realistic dynamics
- **Clear Success Criteria**: Landing successfully gives +100, crashing gives -100
- **Fast Feedback**: Episodes are relatively short, enabling rapid experimentation
- **Educational Value**: Classic trajectory optimization problem that teaches fundamental RL concepts
- **No Visual Complexity**: Vector observations avoid the need for CNN architectures

## 📚 Notebook Series

### 1. REINFORCE (On-Policy Policy Gradients)

- **Focus**: Pure policy gradients, Monte Carlo returns
- **Action Space**: Both discrete AND continuous
- **Key Concepts**: Policy gradient theorem, REINFORCE algorithm, high variance
- **Variants**:
  - Discrete REINFORCE (categorical policy)
  - Continuous REINFORCE (Gaussian policy)

### 2. Vanilla DQN (Off-Policy Value-Based)

- **Focus**: Q-learning, Bellman equations, experience replay
- **Action Space**: Discrete only
- **Key Concepts**: Q-function approximation, target networks, ε-greedy exploration

### 3. Vanilla Actor-Critic (Bridge Methods)

- **Focus**: Combining value and policy methods, on-policy vs off-policy
- **Action Space**: Both discrete AND continuous
- **Key Concepts**: V(s) vs Q(s,a), Bellman expectation vs optimality equations
- **Variants**:
  - On-policy discrete (V-function critic)
  - Off-policy continuous (Q-function critic)

### 4. Off-Policy Continuous Control Evolution

- **Focus**: Algorithm debugging, systematic improvements, and theoretical breakthroughs
- **Action Space**: Continuous only

**Part A: DDPG - The Foundation (and its problems)**

- Basic off-policy actor-critic for continuous control
- Key issues: overestimation bias, instability, poor exploration

**Part B: TD3 - Systematic Debugging**

- **Key Concepts**: Twin critics, delayed updates, target policy smoothing
- **Educational Focus**: How to identify and fix specific RL problems
- **Meta-Skills**: Algorithm debugging methodology, ablation studies

**Part C: SAC - Theoretical Revolution**

- **Key Concepts**: Maximum entropy framework, automatic exploration tuning
- **Focus**: Principled approach to exploration and robustness

**Part D: Algorithm Comparison & Selection**

- When to use DDPG vs TD3 vs SAC
- Performance benchmarks and practical considerations

### 5. PPO (Modern On-Policy)

- **Focus**: Trust region concepts, clipped objectives
- **Action Space**: Both discrete AND continuous
- **Key Concepts**: Importance sampling, GAE, clipped surrogate objective
- **Variants**:
  - Discrete PPO (categorical policy)
  - Continuous PPO (Gaussian policy)

## 🎯 Learning Objectives

By completing this series, you will understand:

### Core RL Paradigms

- **Monte Carlo Methods**: REINFORCE with high variance, unbiased estimates
- **Temporal Difference Learning**: DQN, Actor-Critic with bootstrapping
- **On-Policy vs Off-Policy**: Data usage patterns and sample efficiency tradeoffs
- **Value-Based vs Policy-Based**: When to learn Q(s,a) vs π(a|s) directly

### Algorithm Development Skills

- **Systematic Debugging**: How to identify and fix specific RL problems (TD3 focus)
- **Algorithm Evolution**: Understanding how research progresses incrementally
- **Performance Analysis**: Comparing algorithms fairly across environments
- **Implementation Trade-offs**: Complexity vs performance vs stability

### Practical Implementation

- **Action Space Handling**: Discrete vs continuous action implementations
- **Network Architectures**: CNN feature extraction for visual inputs
- **Training Stability**: Target networks, experience replay, clipping techniques
- **Hyperparameter Sensitivity**: Understanding what matters most for each algorithm

## 📈 Algorithm Coverage Matrix

| Algorithm    | Paradigm   | Data Usage    | Action Space      | Key Innovation                |
| ------------ | ---------- | ------------- | ----------------- | ----------------------------- |
| REINFORCE    | On-Policy  | Fresh Only    | Both              | Pure policy gradients         |
| DQN          | Off-Policy | Replay Buffer | Discrete Only     | Deep Q-learning               |
| Actor-Critic | Both       | Both          | Both              | Value + Policy combination    |
| DDPG         | Off-Policy | Replay Buffer | Continuous Only   | Continuous control foundation |
| TD3          | Off-Policy | Replay Buffer | Continuous Only   | Systematic debugging          |
| SAC          | Off-Policy | Replay Buffer | Continuous Only   | Maximum entropy               |
| PPO          | On-Policy  | Fresh Only    | Both              | Stable policy updates         |

## 🛠️ Technical Implementation

### Package Structure

```
rl/
├── README.md                    # This documentation
├── 1.reinforce.ipynb          # REINFORCE algorithm notebook
├── 2.dqn.ipynb                # DQN algorithm notebook (coming soon)
├── rl_utils/                   # Shared utility package
│   ├── __init__.py            # Package initialization
│   ├── config.py              # Configuration management
│   ├── environment.py         # Environment wrappers and preprocessing
│   ├── networks.py            # Neural network architectures
│   └── visualization.py       # Plotting and analysis functions
└── videos/                     # Generated training/test videos
```

### RL Utils Package

To keep notebooks focused on algorithm learning, we've extracted common infrastructure into the `rl_utils` package:

**Environment utilities** (`rl_utils.environment`):
- `preprocess_state()`: Standardized state preprocessing for LunarLander
- `create_env_with_wrappers()`: Environment creation with video recording and statistics
- `test_agent()`: Standardized agent testing with visualization

**Neural networks** (`rl_utils.networks`):
- `PolicyNetwork`: Flexible policy network supporting both discrete and continuous actions
- Automatic parameter counting and network information printing
- Built-in action clipping for continuous control

**Visualization** (`rl_utils.visualization`):
- `plot_training_results()`: Standardized training curve plotting
- `plot_variance_analysis()`: REINFORCE-specific variance analysis
- `plot_comparison()`: Multi-algorithm comparison plotting
- `get_moving_average()`: Robust smoothing for noisy data

**Configuration** (`rl_utils.config`):
- `create_base_config()`: Consistent configuration across notebooks
- `set_seeds()`: Reproducible random seeding

### Notebook Organization

Each algorithm notebook now follows a consistent structure:
1. **Algorithm Introduction**: Theory and mathematical foundation
2. **Setup**: Import utilities and create configuration
3. **Agent Implementation**: Algorithm-specific code only
4. **Discrete Training**: Training with discrete action space
5. **Continuous Training**: Training with continuous action space (if supported)
6. **Comparative Analysis**: Performance comparison and insights

This separation allows:
- **Focused Learning**: Notebooks contain only algorithm-specific content
- **Code Reuse**: Common utilities shared across all notebooks
- **Easy Maintenance**: Infrastructure improvements benefit all algorithms
- **Clean Comparison**: Standardized evaluation across different methods

### Shared Architecture Components

- **Consistent Preprocessing**: Standardized state normalization across algorithms
- **Unified Visualization**: Comparable plots and metrics across all methods
- **Parameter Tracking**: Automatic network size reporting and gradient monitoring
- **Video Generation**: Consistent video recording for all training runs
- **Statistical Analysis**: Standardized variance and performance analysis

## 🎓 Educational Philosophy

### Learning Approach

- **Concepts First**: Intuitive explanations before mathematical details
- **Visual Learning**: Extensive plots, diagrams, and training visualizations
- **Hands-on Practice**: Interactive hyperparameter exploration
- **Comparative Analysis**: Side-by-side algorithm performance
- **Real Understanding**: Show both successes and failure modes

### Skill Development

- **Algorithm Intuition**: Why each method works and when it fails
- **Implementation Skills**: Clean, readable, and efficient code
- **Debugging Mindset**: How to diagnose and fix training issues
- **Research Thinking**: How algorithms evolve and improve over time

## 🚀 Getting Started

### Prerequisites

- Basic knowledge of neural networks and PyTorch
- Understanding of Markov Decision Processes (MDPs)
- Familiarity with gradient descent optimization

### Installation

```bash
# System dependencies for Box2D environment
sudo apt install swig build-essential python3-dev

# Python packages
pip install 'gymnasium[box2d]>=1.0' torch torchvision matplotlib numpy jupyter pprint

# Clone the repository
git clone <repository-url>
cd rl

# The rl_utils package is automatically available when running notebooks from the rl/ directory
```

### Running the Notebooks

1. Start Jupyter from the `rl/` directory:
```bash
cd rl/
jupyter notebook
```

2. Open `1.reinforce.ipynb` to start with the REINFORCE algorithm

3. Each notebook is self-contained but uses the shared `rl_utils` package

### Package Usage Example

```python
from rl_utils import create_base_config, PolicyNetwork, plot_training_results
from rl_utils import create_env_with_wrappers, test_agent

# Create standardized configuration
config = create_base_config()

# Create environment with standard wrappers
env = create_env_with_wrappers(config, is_continuous=False, record_videos=True)

# Create policy network with parameter counting
policy = PolicyNetwork(observation_dim=8, action_space=env.action_space, 
                      is_continuous=False, network_config=config["policy_network"])
policy.print_network_info()  # Prints parameter count and architecture info

# ... training code ...

# Standardized result visualization
plot_training_results(scores, losses, config, "Discrete")

# Test the trained agent
test_agent(policy, config, is_continuous=False, record_video=True)
```
