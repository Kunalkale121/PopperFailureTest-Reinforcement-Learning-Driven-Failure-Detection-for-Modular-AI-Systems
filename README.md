# 🚀 PopperTest: Reinforcement Learning–Driven Failure Detection for Modular AI Systems
*A Multi-Agent UCB-Based Validation Framework Extending Humanitarians.AI Popper Architecture*

---

## 📌 Overview

**PopperTest** is a multi-agent reinforcement learning system designed to intelligently test modular AI or software systems, discover hidden weaknesses, and adapt testing behavior over time.

The project integrates a **UCB-based Reinforcement Learning controller** into a **Popper-style validation framework**, where multiple specialized agents collaborate to probe the reliability of a complex system under test (SUT).

Each component of the SUT contains a hidden failure probability, and the RL agent learns an optimal testing strategy that significantly outperforms random testing.

---

## ✅ Key Features

- Multi-agent architecture  
- UCB (Upper Confidence Bound) reinforcement learning  
- Adaptive failure detection and dynamic test prioritization  
- Coverage-based exploration  
- Scalable system (10–200+ modules)  
- Robust analysis using 200 independent training runs  
- Real-world relevance for software & AI reliability testing  

---

# 🧠 System Architecture Diagram

                 ┌──────────────────────────────────┐
                 │         RL Controller (UCB)       │
                 │ - Selects next component to test  │
                 │ - Balances exploration/exploitation│
                 └───────────────┬────────────────────┘
                                 │
                                 ▼
                 ┌──────────────────────────────────┐
                 │     Test Case Generator Agent     │
                 │ - Builds test case for component  │
                 └───────────────┬────────────────────┘
                                 │ test_case
                                 ▼
                 ┌──────────────────────────────────┐
                 │       Error Detector Agent        │
                 │ - Executes test case              │
                 │ - Returns pass/fail (reward)      │
                 └───────────────┬────────────────────┘
                                 │ reward
                                 ▼
                 ┌──────────────────────────────────┐
                 │       System Under Test (SUT)     │
                 │ - Contains N components           │
                 │ - Hidden failure probabilities    │
                 │ - Tracks coverage and test counts │
                 └───────────────┬────────────────────┘
                                 │ coverage update
                                 ▼
                 ┌──────────────────────────────────┐
                 │     Coverage Analyzer Agent       │
                 │ - Calculates % components tested  │
                 │ - Informs exploration behavior    │
                 └───────────────┬────────────────────┘
                                 │ feedback
                                 ▼
                 ┌──────────────────────────────────┐
                 │         RL Controller (UCB)       │
                 │ - Updates statistics & UCB scores │
                 └───────────────────────────────────┘

---

## 📐 Mathematical Formulation of RL (UCB)
We use the **UCB1 algorithm** to choose which component to test at each episode.

### **Action Selection Rule**
\[
a_t = \arg\max_{i} \left( \bar{X}_i + c \sqrt{\frac{2 \ln t}{n_i}} \right)
\]

### **Definitions**
| Symbol | Meaning |
|--------|---------|
| \( \bar{X}_i \) | Mean reward (failure rate) of component *i* |
| \( n_i \) | Number of times component *i* has been tested |
| \( t \) | Total number of tests performed |
| \( c \) | Exploration coefficient |
| Reward | 1 = failure found, 0 = no failure |

### **Interpretation**
- The first term encourages testing components that fail often (**exploitation**)  
- The second term ensures rarely-tested components are explored (**exploration**)  
- UCB naturally balances both, ideal for detecting hidden weaknesses  

---

## 🧩 Detailed Explanation of Design Choices
### **1. Multi-Agent Popper-Aligned Architecture**
We use four clearly-defined agents:
- **RL Controller** – selects module to test  
- **Test Generator** – constructs the test  
- **Error Detector** – executes tests and returns failures  
- **Coverage Analyzer** – tracks exploration and system coverage  

This mirrors Popper’s philosophy: use multiple specialized agents to validate system reliability.

### **2. Scalable, Modular System Under Test (SUT)**
Supports ANY number of components (10–200+), enabling realistic simulation of:
- microservices  
- pipelines  
- modular AI systems  
- API clusters  

### **3. Reward Function**
Reward = **1 only if a failure is detected**.  
This encourages aggressive bug-finding strategies.

### **4. Why UCB Instead of Deep RL**
- Lightweight  
- No neural networks needed  
- Excellent for sparse rewards  
- Strong theoretical guarantees  

---

## 🧪 Experimental Design & Results

### **Experiment Setup**
- Modules: 10–200  
- Episodes: 1,000–5,000  
- RL Method: UCB1  
- Baseline: Random uniform testing  
- Evaluation: **200 independent training runs**

### **Results Summary**
| Metric | RL (UCB) | Random |
|--------|----------|--------|
| **Mean Failures Found** | **346.30** | **276.47** |
| **Improvement** | **+25.2%** | — |
| **Prioritization Score** | **0.87** | 0.50 |
| **Coverage Efficiency** | Fast | Slow |

### **Observations**
- RL quickly identifies the riskiest modules
- <img width="2004" height="1100" alt="image" src="https://github.com/user-attachments/assets/da6956ed-91f6-4b7e-82e5-6e78ce279854" />

- Random testing wastes tests on low-risk modules  
- RL converges to high-value testing patterns
- <img width="2780" height="1184" alt="image" src="https://github.com/user-attachments/assets/4e191c98-af91-4121-b5d7-4ced40538a18" />
 
- High prioritization score shows strong risk-awareness
- <img width="1696" height="1094" alt="image" src="https://github.com/user-attachments/assets/c692dd7e-7cf1-45e7-bdfb-3d3aabfd137f" />


---

## 📈 Statistical Validation (200-Run Evaluation)
**Failures Found (mean ± std):**
RL: 346.30 ± 44.91
Random: 276.47 ± 43.86


**Prioritization Score:**
0.87 ± 0.06


### Interpretation
- RL consistently and significantly outperforms random  
- Low variance = stable learning  
- High prioritization score = RL learns true risk structure  
- Strong evidence of effective reinforcement learning  

---

## 🧵 Discussion of Challenges & Solutions

### **1. Sparse Rewards**
Failures are rare.  
**Solution:** UCB ensures broad exploration early.

### **2. Quick Coverage Saturation**
Small module sets reach 100% coverage too fast.  
**Solution:** Support larger module counts (50–200).

### **3. Noisy Runs**
High randomness across episodes.  
**Solution:** Use 200-run statistical averaging.

### **4. Agent Communication Complexity**
Coordinating 4 agents can create ambiguity.  
**Solution:** Strict class boundaries & clear interfaces.

---

## 🛡 Ethical Considerations
- Testing must not overwhelm production systems  
- RL should avoid overfitting to early failures  
- Decision-making must stay explainable & auditable  
- Resource management must respect compute limits  
- Automated systems must defer to human oversight  

---

## 🔮 Future Improvements & Research Directions
### **1. Integrate Real APIs or ML Models**
Move beyond simulated components.

### **2. Replace UCB with Advanced RL**
Explore:
- DQN  
- PPO  
- A3C  
- Contextual bandits  

### **3. Hierarchical Testing Agents**
Agents that plan multi-step tests.

### **4. Transfer Learning Across Systems**
Detect recurring failure patterns.

### **5. Curiosity-Driven Intrinsic Rewards**
Better exploration of rare edge cases.

### **6. Explainable Failure Prioritization**
Provide “why this module was tested”.

---

---

## 🙌 Acknowledgements
This project is inspired by the **Humanitarians.AI Popper Framework** and was developed for the **Reinforcement Learning for Agentic AI Systems** final assignment.


