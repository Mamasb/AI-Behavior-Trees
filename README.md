# Binary Trees in AI Behavior Trees
## Overview
Binary trees are hierarchical data structures composed of nodes, where each node has at most two children: left and right. In game development, binary trees are frequently used to model decision-making processes and behaviors of non-player characters (NPCs) through what are known as AI behavior trees.

## Usage
### AI Behavior Trees
AI behavior trees organize decision-making into a hierarchical structure where each node represents an action or a decision point for an NPC. The tree structure allows game developers to define and control how NPCs react to different stimuli and events in the game environment.

#### Components of an AI Behavior Tree
Root Node: The starting point of the tree, often representing the overarching goal or objective of the NPC.

Action Nodes: Terminal nodes that represent specific actions an NPC can perform, such as attacking, defending, moving to a location, or interacting with objects.

Composite Nodes:

Sequence: Executes child nodes in order until one fails.
Selector: Executes child nodes in order until one succeeds.
Parallel: Executes child nodes simultaneously.
Decorator Nodes: Modify the behavior of child nodes (e.g., repeat until a condition is met, invert the result).

## Example
Consider an NPC in a game that needs to decide its next action based on current game state:

```shell
#include <stdio.h>
#include <stdlib.h>

typedef struct TreeNode {
    char *action;
    struct TreeNode *left;
    struct TreeNode *right;
} TreeNode;

TreeNode *createTreeNode(char *action) {
    TreeNode *newNode = (TreeNode *)malloc(sizeof(TreeNode));
    if (newNode == NULL) {
        perror("Error creating new node");
        exit(EXIT_FAILURE);
    }
    newNode->action = action;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

TreeNode *createBehaviorTree() {
    TreeNode *root = createTreeNode("Attack");
    root->left = createTreeNode("Chase");
    root->right = createTreeNode("Defend");
    root->left->left = createTreeNode("Approach");
    root->left->right = createTreeNode("Engage");
    root->right->left = createTreeNode("Protect");
    root->right->right = createTreeNode("Retreat");
    return root;
}

void printBehaviorTree(TreeNode *node, int depth) {
    if (node == NULL) return;
    for (int i = 0; i < depth; ++i) {
        printf("  ");
    }
    printf("- %s\n", node->action);
    printBehaviorTree(node->left, depth + 1);
    printBehaviorTree(node->right, depth + 1);
}

int main() {
    TreeNode *behaviorTree = createBehaviorTree();
    
    printf("Behavior Tree for NPC:\n");
    printBehaviorTree(behaviorTree, 0);
    
    return 0;
}
```
In this example:

Each node represents an action or decision point for an NPC.
createBehaviorTree constructs a simple behavior tree structure.
printBehaviorTree recursively prints the tree for visualization.
## Applications
Game AI: AI behavior trees enable NPCs to make complex decisions based on game state and environmental conditions.
Modularity: Trees can be easily modified to introduce new behaviors or adjust existing ones without rewriting large sections of code.
State Management: Facilitates smooth transitions between different NPC states (e.g., idle, attacking, defending) based on changing game conditions.
## Getting Started
To integrate AI behavior trees into your game:

Define Actions: Identify the actions and decisions your NPCs need to make.
Construct the Tree: Use binary tree nodes to structure these actions hierarchically.
Execution: Implement logic to traverse and execute the tree based on game events and conditions.
## Resources
Binary Trees on Wikipedia
Game AI Pro
Behavior Trees in Game AI
License
This project is licensed under the MIT License - see the LICENSE file for details.