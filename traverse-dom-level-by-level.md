# Traverse DOM level by level

The link : https://bigfrontend.dev/problem/Traverse-DOM-level-by-level

Given a DOM tree, flatten it into an one dimensional array, in the order of layer by layer, like below.

![img](https://cdn.nlark.com/yuque/0/2024/png/26734946/1711718343091-fd65580f-f170-4834-a66c-f33f71754962.png)



```javascript
/**
 * @param { HTMLElement } root
 * @returns { HTMLElement[] }
 */
function flatten(root) {
  if (root === null) return []
  
  const queue = [root]
  
  const result = []
  
  while (queue.length > 0) {
    const head = queue.shift()
    result.push(head)
    queue.push(...head.children)
  }
  
  return result
}
```

we can use BFS to solve the problem. Bredth-first search(BFS) is an algorithm for traversing or searching tree or graph data structures. It starts at the tree root (or some arbitrary node of a graph, sometimes referred to as a 'search key), and explores the neighbor nodes first before moving to the next level neighbors.

Firstly, we need to convert the root to the queue array which store the child node.
Secondly,  we can use the while loop to check if there is any node in the queue. If there is node in the queue, we can remove the first element from the queue and push it into the result array which store the flatten node and if the node has its children, we need to get the child node, and push it int the queue, and continuously executes it this until the queue is empty.