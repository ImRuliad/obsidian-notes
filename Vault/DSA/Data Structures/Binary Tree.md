## <u> Binary Tree Traversals </u>

#### (DFS) Depth First Search
*Explores down a branch, goes deep*
- **Inorder (Left, Root, Right)**
- **Postorder (Left, Right, Root)**
- **Preorder (Root, Left, Right)**
#### (BFS) Depth First Search
*Explores layer by layer, goes wide*
- **Level order**

## <u> Traversal Implementation (Recursive) </u>

#### Inorder
*Retrieves elements in their natural order*
```python
def inorder(root):
	if root is None:
		return
	inorder(root.left)
	print(root.val)
	inorder(root.right)
```

#### Postorder
```python
def postorder(root):
	if root is None:
		return
	postorder(root.left)
	postorder(root.right)
	print(root.val)
```

#### Preorder
```python
def preorder(root):
	if root is None:
		return
	print(root.val)
	preorder(root.left)
	preorder(root.right)
```

#### Level order
```python
from collections import deque

def level_order(root):
    if not root: return []
    out, q = [], deque([root])
    while q:
        node = q.popleft()
        out.append(node.key)
        if node.left:  q.append(node.left)
        if node.right: q.append(node.right)
    return out

```
