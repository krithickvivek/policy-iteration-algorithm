# POLICY ITERATION ALGORITHM

## AIM
To develop a Python program to find the optimal policy for the given MDP using the policy iteration algorithm.

## PROBLEM STATEMENT
The slippery walk problem in reinforcement learning involves an agent navigating a 7-state environment to reach a target state. Due to the environment’s unpredictable nature, the agent might end up moving in the opposite direction of its intended move, adding an extra layer of complexity to the task.

## POLICY ITERATION ALGORITHM
Initialize Policy:

Start with an arbitrary policy. In the provided code, the initial policy pi is randomly generated, where each state is assigned a random action. Policy Evaluation:

Evaluate the current policy by calculating the value function 𝑉 V for each state. This involves determining how good it is to be in each state under the current policy. This is done using the policy_evaluation function, which computes the value function 𝑉 V by solving a system of linear equations or using iterative methods until convergence (based on a threshold theta). Policy Improvement:

Improve the policy based on the value function 𝑉 V obtained from the evaluation step. This involves calculating the action-value function 𝑄 Q for each state-action pair and updating the policy to choose the action that maximizes the 𝑄 Q value. This is handled by the policy_improvement function, which returns a new policy pi where each state is assigned the action that has the highest value according to 𝑄 Q. Check for Convergence:

Compare the newly improved policy with the old policy. If the policy does not change (i.e., it is stable), then the algorithm has converged, and the process can stop. If the policy has changed, repeat the policy evaluation and policy improvement steps. Return Results:

Once the policy has converged, return the final value function 𝑉 V and the optimal policy pi.
## POLICY IMPROVEMENT FUNCTION
### Name : Krithick Vivekananda
### Register Number : 212223240075
```python
def policy_improvement(V, P, gamma=1.0):
    Q = np.zeros((len(P), len(P[0])), dtype=np.float64)

    for s in range(len(P)):
        for a in range(len(P[s])):
            for prob, next_state, reward, done in P[s][a]:
                Q[s][a] += prob * (reward + gamma * V[next_state] * (not done))

    new_pi = lambda s: {s: a for s, a in enumerate(np.argmax(Q, axis=1))}[s]

    return new_pi
```
## POLICY ITERATION FUNCTION
### Name : Krithick Vivekananda 
### Register Number : 212223240075
```python
def policy_iteration(P, gamma=1.0, theta=1e-10):
    random_actions = np.random.choice(tuple(P[0].keys()),len(P))
    pi = lambda s : {s:a for s,a in enumerate(random_actions)} [s]
    while True:
      old_pi = {s:pi(s) for s in range(len(P))}
      V=policy_evaluation(pi,P,gamma,theta)
      pi=policy_improvement(V,P,gamma)
      if old_pi=={s:pi(s) for s in range(len(P))}:
        break
    return V,pi
```

## OUTPUT:
### 1. Policy, Value function and success rate for the Adversarial Policy
<img width="885" height="176" alt="image" src="https://github.com/user-attachments/assets/788fefe4-3b01-4866-b0df-481c791f8cd9" />
<img width="809" height="42" alt="image" src="https://github.com/user-attachments/assets/5b0f88d9-6d3b-47b8-87c3-36d60189602d" />
<img width="739" height="169" alt="image" src="https://github.com/user-attachments/assets/b64f3b3b-f39a-4c5d-95ab-b1c80ee67e5b" />

### 2. Policy, Value function and success rate for the Improved Policy
<img width="846" height="173" alt="image" src="https://github.com/user-attachments/assets/0e2e4908-8356-476c-809d-ebb947461bc3" />
<img width="874" height="43" alt="image" src="https://github.com/user-attachments/assets/3ed24e52-1a64-4b9d-85ef-e9693e749233" />
<img width="851" height="178" alt="image" src="https://github.com/user-attachments/assets/ea2e7c7f-f37f-4cee-b07e-3d91054bbc6a" />

### 3. Policy, Value function and success rate after policy iteration
<img width="848" height="196" alt="image" src="https://github.com/user-attachments/assets/a51e8c06-15cf-4504-8af6-90937e32bd8a" />
<img width="843" height="46" alt="image" src="https://github.com/user-attachments/assets/f8fe9cf1-7ed3-4cb9-8962-e358019a0fe6" />
<img width="832" height="168" alt="image" src="https://github.com/user-attachments/assets/ac89ae9a-11cd-4275-876d-f3bfa2aa6c36" />

## RESULT:
Thus, a Python program is developed to find the optimal policy for the given MDP using the policy iteration algorithm.
