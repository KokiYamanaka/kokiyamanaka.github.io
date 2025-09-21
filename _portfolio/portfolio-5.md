---
title: "NeuroEvolution"
excerpt: "The Use Case Of NEAT"
collection: portfolio
---


# NeuroEvolution

## 1. Neuro Sime

This project uses [NEAT](https://nn.cs.utexas.edu/downloads/papers/stanley.ec02.pdf) to train an agent to beat another internal agent in volleyball.

### 1.1 The Setup 

We begin by outlining the overall setup of our experiment. Instead of focusing on maximizing the score to +5 points, our primary objective was to ensure that the agent could consistently keep the ball in play for 400 episodes without dropping it. To achieve this, we trained a NEAT-based agent using the following parameters: a population size of 170, input nodes, two hidden layers with two nodes each (tanh), one output node, a crossover probability of 0.4, and a mutation probability of 0.03. 

To clarify our setup, we outline both the neural network and genetic algorithm. The network takes a single input—the horizontal displacement between ball and agent (Δx)—instead of all eight inputs. Positive Δx means the ball is behind the yellow agent, negative means in front. A sigmoid output then decides whether to move forward or back. For the genetic algorithm, we initialized genomes with fixed five nodes and five edges, leaving others for future mutations. Crossover aligns connections by innovation IDs, after which mutations add new edges. 



### 1.2 Some Plays

Here we showcase plays from the fittest yellow agent of the final generation. Its main strategy is to shift back and forth, staying aligned with the ball horizontally to prevent it from falling.

The agent keeps the ball up, 
though random bounces may send it back.

![catch-bounce-back](https://github.com/user-attachments/assets/79eceb6d-2223-44d9-b458-30611efd0a2d)


### 1.3 Visualizations of Networks

We now present visualizations from key genomes. These genomes were tracked across successive generations to examine whether they underwent meaningful structural mutations. Mutations were monitored to preserve stability and exploration, supported by assigning each first-generation genome a unique identifier. 

Here are some key genomes. In each genome, a blue linear node corresponds to the input, while gray corresponds to the output. The key difference lies in whether each genome has 2→4, 2→5, 3→5 edges.

<img alt="image" src="https://github.com/user-attachments/assets/99e176c3-6fec-492f-b627-83bc18aa17be" />

<img alt="image" src="https://github.com/user-attachments/assets/761e5b39-31b2-4042-a658-f02de1f610cb" />


We have a couple key observations. Firstly, Evolution appears to favor nodes with more input edges. Across first-generation unique IDs, we observed a wide range of added edge combinations. For instance, E39 showed (2→4, 2→5, 3→5) and (2→4, 3→5) across generations, while CB2 had (2→4, 3→5). Overall, 2→4 appeared most frequently. Since 3→4 was fixed from the start, the repeated presence of both edges supports the idea that nodes integrating more hidden node—more “angles of reflection”—tend to enable better decisions.

Secondly, we observed that structural complexity increased as evolution maintained a balance between exploiting good lineages and exploring new variants. By tracking lineages derived from the first generation, we found that 6 out of the 8 possible edge additions actually appeared in later descendants. For example, the E39 genome started with a simple set of edges, but across generations its children accumulated different edge mutations. By the 50th generation, at least 6 out of 8 possible new edge combinations had been realized. This shows that structural evolution did not remain fixed; instead, lineages diversified through edge mutation.




Neatbackprop combines NEAT’s evolutionary search with gradient-based backpropagation. It evolves neural network structures through genetic operations while refining their weights via gradient descent, aiming for faster convergence and higher-performing architectures.


# BackpropNEAT

Neatbackprop combines NEAT’s evolutionary search with gradient-based backpropagation. It evolves neural network structures through genetic operations while refining their weights via gradient descent, aiming for faster convergence and higher-performing architectures.

<p align="center">
  <img src="https://github.com/user-attachments/assets/50f72a8e-f562-415d-84f6-3f1f5d650e4c" />
</p>



## 2.1 Setup  

Here, I’ll briefly explain how I evolve my network. At the beginning, each genome starts with a fixed configuration: a set number of nodes and layers, with 2 fixed connected edges. From this base, a genome may undergo crossover by innovation ID, or else add 2–3 random available edges. Here’s a sample of how it works.  

 

## 2.2 Motivation behind starting with a fix configuration, then evolve  

A fully connected network wastes time searching in an unnecessarily high-dimensional weight space. NEAT improves this by gradually adding useful edges, keeping the weight search space smaller.  

But for a human, NEAT can be hard to interpret—how do we know which evolved structure is genuinely useful if the fittest networks never repeat and instead drift into random, unrelated forms for each generation? It feels like trying to design the best paper plane without knowing what an airplane should look like.  

That’s why a hybrid—something between fully connected and NEAT—might be worth trying. (I do also recognize my implementation is a bit off the core essence of NEAT, but trying something different was worthwhile to me.)  


## 2.3 Results  

I parsed the **blob** and **circle** datasets into my network and evaluated fitness with both weight error and edge complexity.  

- **Blob dataset:** Fitness decreased steadily, accompanied by structural diversity across generations.  
- **Circle dataset:** Fitness improved little, with networks tending to stick to a default topology.  

 
 
## 2.4 Network Complexification  

For each shape, I collected the fittest networks from every generation and inspected their change in behavior.  

- **Blob dataset**  
  - **Early generations:** Input connections chosen more often.  
  - **Mid generations:** Mix of input and some output connections.  
  - **Late generations:** Gradually resulted in a fully connected edge.  
  - (I also overlooked the higher probability of selecting input connections, since there are more available edges for them.)  

- **Circle dataset**  
  - **Early generations:** Random input edges were connected.  
  - **Mid generations:** Networks kept switching between default edge configuration and some random edges.  
  - **Late generations:** Switching led back to the default edge.  

This tendency implies evolution didn’t favor new edges, mainly because the epoch count was set too low.  



## 2.5 Conclusion  

At the start, I simplified a sample repo to avoid complexity and unclear representations. For example, Kahn’s algorithm caused bugs, so I fixed node layers to make activation ordering straightforward. This led my implementation to begin with a fixed network configuration, which contradicts the essence of NEAT.  

While both my approach and classical NEAT avoid exploding the search space upfront, mine risks locking into a suboptimal structure from the beginning.  

**Ultimately, the results highlight a trade-off:** simplifying the setup improves stability and clarity but risks narrowing evolution’s creative search, suggesting that future work should seek a better balance between interpretability and exploratory power.  
