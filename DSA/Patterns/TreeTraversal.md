

Every tree problem reduces to one of these traversals with some logic added at the visit step. Nail the templates first, then the problems become obvious.


Traversal           OrderTypical                use

Inorder             Left → Node → Right         BST problems — gives sorted order
Preorder            Node → Left → Right         Serialize tree, copy tree
Postorder           Left → Right → Node         Delete tree, compute from children upLevel orderBFS row by rowShortest path, level-based problems


all are done through DFS



only level order traversal is done through BFS using queue


